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
- [ ] `submitter` array is non-empty; each entry has `email` and `person` with `firstName`/`lastName`
- [ ] `authors` array is non-empty; each entry has `firstName` and `lastName`
- [ ] Submitter email appears valid (contains `@`)
- [ ] Target site responds (GET the base URL to confirm it's up)

---

## Submit

- `POST /api/submit` with `Content-Type: application/json`
- Capture the full response body

### Expected Success Response

```json
{
  "status": "ok",
  "count": 1,
  "results": [
    {
      "submissionId": "...",
      "softwareId": "..."
    }
  ]
}
```

- `count` should match the number of objects submitted
- Each result has `submissionId` and `softwareId`

---

## Verification Endpoints

After a successful submit, use these endpoints to verify persistence:

### Public View: `GET /api/view/<softwareId>/`

Returns the public-facing representation of the submitted software. Use to confirm key fields are visible:
- `softwareName`
- `codeRepositoryURL` (note: uppercase `URL` in view output)
- `description`
- `authors`
- `submitterName`

### Curator-Level Data: `GET /sapi/software_edit_data/<queueId>/`

Returns the full stored representation at curator fidelity. This is the primary endpoint for roundtrip verification because it preserves more detail than the public view.

To find the `queueId`:
- Check the submit response for queue-related IDs
- Or query `GET /api/models/SoftwareEditQueue/rows/all/` and find the matching entry
- The curator edit link is: `/curate/edit_submission/?uid=<queueId>`

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

2. **`submitter[].person/email` → `submitterName.submitterName/submitterEmail`** — Submitter object is flattened; person name may be combined into a single string

3. **`version.number/release_date/description/version_pid` → `versionNumber/versionDate/versionDescription/...`** — Version sub-object may be flattened to top-level fields with different key names

4. **`relatedObservatories[].identifier` → `relatedObservatories[].relatedObservatoryIdentifier`** — Identifier key may be renamed in stored form

5. **Controlled-list values as objects vs strings** — Arrays of strings in the submission may appear as arrays of objects with a `name` field (or vice versa), or as database IDs

6. **`award` vs stored representation** — Award objects may be restructured

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
| `POST expected` on `/api/submit` | Wrong HTTP method (e.g., GET) | Use POST |
| `400` but submission appears in DB | Email send failed after DB commit | Check `/api/view/<softwareId>/` — the record likely persisted despite the error |
| `500` or timeout | Server-side error | Check server logs; retry if transient |

### Email-Related False Failures

The submit endpoint sends notification emails after the DB write. If the email recipient is rejected or the mail server is unavailable, the API may return an error even though the submission was successfully stored. Always check `/api/view/<softwareId>/` before concluding that a submission failed.

### Verifying Without Queue ID

If you don't have the `queueId`:
1. Use the `softwareId` from the submit response
2. Check `/api/view/<softwareId>/` for the public view
3. Query `/api/models/SoftwareEditQueue/rows/all/` and search for the matching software name or submission time

---

## Verification Report Format

After roundtrip verification, produce a summary:

```
## Roundtrip Verification Report

**Submitted:** [timestamp]
**Software ID:** [softwareId]
**Queue ID:** [queueId]

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
