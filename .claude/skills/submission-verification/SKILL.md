---
name: submission-verification
description: >
  Post-submission verification workflow for HSSI API. Contains roundtrip diff
  methodology, verification endpoints, known representation differences, and
  troubleshooting. Use when verifying HSSI submissions.
user-invocable: false
---

# HSSI Submission Verification

Verify that an HSSI submission was correctly persisted by the backend using roundtrip comparison.

---

## Pre-Submit Validation Checklist

Before submitting, confirm:

- [ ] Payload is valid JSON
- [ ] Root JSON value is an array (`[...]`), even for a single submission
- [ ] Each object contains all five required fields: `submitter`, `softwareName`, `codeRepositoryUrl`, `authors`, `description`
- [ ] `submitter` array is non-empty; each entry has `email` and `person` with `givenName`/`familyName`
- [ ] `authors` array is non-empty; each entry has `givenName` and `familyName`
- [ ] `license` (if present) is a plain string, not an object
- [ ] `publisher` (if present) uses `{name, identifier}` — no `publisherIdentifier` key
- [ ] Submitter email appears valid (contains `@`)
- [ ] Submitter email is the real submitter's email address — this is the genuine submission, not a test or probe
- [ ] This is the one and only submission attempt for this metadata — not a test, probe, or iterative experiment
- [ ] Target site responds (GET the base URL to confirm it's up)

---

## Submit

- `POST /api/submission/` (note the trailing slash) with `Content-Type: application/json`
- Capture the full response body
- Success status: **HTTP 201 Created**

### Expected Success Response

```json
{
  "status": "ok",
  "count": 1,
  "results": [
    {
      "index": 0,
      "softwareId": "..."
    }
  ]
}
```

- `count` should match the number of objects submitted
- Each result has `index` and `softwareId` — **no `submissionId`** (the new endpoint does not return one)
- `queueId` is also not in the response — look it up via the SoftwareEditQueue endpoint (see below)

---

## Verification Endpoints

After a successful submit, use these endpoints to verify persistence:

### Curator-Level Data: `GET /sapi/software_edit_data/<queueId>/` (primary)

Returns the full stored representation at curator fidelity. This is the **primary endpoint** for roundtrip verification because it preserves the most detail.

The new `/api/submission/` endpoint creates a `SoftwareEditQueue` entry (90-day edit window) for every submission, so this flow works — but the `queueId` is not returned in the submit response. To find it:

1. Query `GET /api/models/SoftwareEditQueue/rows/all/`
2. Find the entry whose `software` (or equivalent FK) matches the `softwareId` returned from submit
3. Use that row's `id` as the `queueId`

The curator edit link is: `/curate/edit_submission/?uid=<queueId>`

### Public View: `GET /api/view/software/<softwareId>/` (secondary)

Returns the public-facing representation of the submitted software. **Caveat:** this endpoint only returns records that are already in `VerifiedSoftware` — fresh submissions usually aren't verified yet, so expect 404 until a curator approves the entry. Use as a secondary check only.

Key visible fields when available:
- `softwareName`
- `codeRepositoryURL` (note: uppercase `URL` in view output)
- `description`
- `authors`
- `submitterName`

---

## Roundtrip Diff Methodology

Compare every field in the submitted payload against what's stored in `/sapi/software_edit_data/<queueId>/`.

### Classification

For each submitted field, classify the stored result as:

| Status | Meaning |
|--------|---------|
| **Match** | Stored value is identical to submitted value |
| **Equivalent** | Same meaning, different representation (see known differences below) |
| **Degraded/Lost** | Value is missing, materially changed, or truncated |

### Known Representation Differences (Treat as Equivalent)

These differences are expected between submitted and stored forms:

1. **`codeRepositoryUrl` → `codeRepositoryURL`** — Key name changes from lowercase `Url` to uppercase `URL`

2. **Person fields** — Submitted `givenName`/`familyName` may appear in stored form under the same names, or combined into a single display string (e.g., `submitterName`). The underlying DB columns are `given_name`/`family_name`.

3. **Submitter flattening** — The submitted `submitter[].person/email` object may be flattened in stored form to fields like `submitterName`/`submitterEmail`.

4. **Version sub-keys** — Submitted `version.number/releaseDate/description/versionPid` may be flattened to top-level fields (`versionNumber`, `versionDate`, `versionDescription`, etc.) or stored under snake_case (`release_date`, `version_pid`).

5. **`relatedObservatories[].identifier` → `relatedObservatories[].relatedObservatoryIdentifier`** — Identifier key may be renamed in stored form.

6. **Controlled-list values as objects vs strings** — Arrays of strings in the submission may appear as arrays of objects with a `name` field (or vice versa), or as database IDs.

7. **`license` string → object** — The submission `license` is a plain string (license name). The stored form may represent it as an object `{name, url, ...}` looked up from the `License` model.

8. **`publisher` identifier** — Submitted `publisher.identifier` may be stored under a renamed key (e.g., `publisherIdentifier`) in the curator view, even though submission uses `identifier`.

9. **`award` vs stored representation** — Award objects may be restructured.

### Verification Pass

1. Fetch `/sapi/software_edit_data/<queueId>/`
2. For each field in the submitted payload:
   - Find the corresponding field in the stored data (accounting for known key renames)
   - Compare values, accounting for known representation differences
   - Classify as Match, Equivalent, or Degraded/Lost
3. Any **Degraded/Lost** field is a verification failure unless the user explicitly accepts it

---

## Troubleshooting

### Common Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `400 Root JSON value must be an array` | Submitted a bare object instead of an array | Wrap the object in `[...]` |
| `FunctionCategory ... does not exist` | Software Functionality value doesn't match controlled list | Normalize to exact strings from `/api/models/FunctionCategory/rows/all/` |
| `License ... not found` | License string doesn't match any row in the `License` model | Normalize to exact `name` from `/api/models/License/rows/all/` |
| `405 Method Not Allowed` on `/api/submission/` | Wrong HTTP method (e.g., GET) | Use POST |
| `404` on `/api/submission` (no trailing slash) | Missing trailing slash | Use `/api/submission/` exactly |
| `400` but submission appears in DB | Email send failed after DB commit (outside atomic block) | Check `/api/models/SoftwareEditQueue/rows/all/` — the record likely persisted despite the error |
| `500` or timeout | Server-side error | Check server logs; retry if transient |

### Email-Related False Failures

The new endpoint creates the `SoftwareEditQueue` entry and sends the notification email **outside** the atomic transaction (after DB commit). If the email recipient is rejected or the mail server is unavailable, the API can return an error response even though the submission was successfully stored. Always check `/api/models/SoftwareEditQueue/rows/all/` (looking up by `softwareId` if available) before concluding that a submission failed.

### Duplicate Prevention

**If a submission appears to fail but the record exists, do NOT resubmit.** The record was persisted successfully — the error was caused by a downstream issue (typically email). Resubmitting would create a duplicate permanent record and send another confirmation email. Instead, report the error and the existing record to the user and let them decide how to proceed.

### Verifying Without a Queue ID

If you haven't yet located the `queueId`:
1. Use the `softwareId` from the submit response
2. Query `/api/models/SoftwareEditQueue/rows/all/` and match the row whose software FK equals `softwareId`
3. Use that row's `id` as `queueId`, then GET `/sapi/software_edit_data/<queueId>/`

---

## Verification Report Format

After roundtrip verification, produce a summary:

```
## Roundtrip Verification Report

**Submitted:** [timestamp]
**Software ID:** [softwareId]
**Queue ID:** [queueId — looked up via SoftwareEditQueue]

### Results

| Field | Status | Notes |
|-------|--------|-------|
| softwareName | Match | |
| codeRepositoryUrl | Equivalent | Key renamed to codeRepositoryURL |
| description | Match | |
| ... | ... | ... |

### Summary
- Matches: X
- Equivalent: Y
- Degraded/Lost: Z

**Verdict:** [PASS / FAIL]
```

A submission passes verification if there are zero Degraded/Lost fields (or all Degraded/Lost fields are explicitly accepted by the user).
