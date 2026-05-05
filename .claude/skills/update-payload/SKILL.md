---
name: update-payload
description: >
  HSSI Update API specification. Contains the partial update endpoint contract,
  lookup endpoint, field classification (static/dynamic/enrich-only), diff
  methodology, and payload structure. Use when building or reasoning about
  HSSI metadata updates.
user-invocable: false
---

# HSSI Update Payload Specification

Build partial update payloads for existing HSSI software entries. Only changed fields are sent; omitted fields are preserved.

> **WARNING: Every PATCH to `/api/data/software/<uid>/` modifies the production database permanently.** There is no undo. Build the payload correctly, get user approval, and submit once. Do not retry on failure.

---

## Authentication

The `PATCH` update endpoint requires a bearer token. The `GET` lookup endpoint is public.

```
Authorization: Bearer <token>
```

The token is resolved via cascade:
1. `.env` file in the `hssi-claude-agents` repo root (key: `HSSI_UPDATE_TOKEN`)
2. `HSSI_UPDATE_TOKEN` environment variable
3. Ask the user to provide it

The token is **never** hardcoded in agent definitions or committed to git.

---

## Endpoints

### PATCH /api/data/software/<uid>/ — Partial Update

Updates only the provided fields on an existing visible Software entry. Omitted fields are untouched. The `softwareId` is in the URL path; the body contains only the fields to change.

The endpoint runs the request through `SubmissionSerializer` in **USER view with `partial=True`**, so accepted field names and shapes are identical to the `/api/submission/` payload — minus the `submitter` field, which the update path explicitly rejects.

**Request:**

```
PATCH /api/data/software/<uid>/
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
  "developmentStatus": "Active",
  "version": {
    "number": "v2.0.0",
    "releaseDate": "2026-01-15",
    "description": "Major rewrite",
    "versionPid": "https://doi.org/10.5281/zenodo.99999999"
  }
}
```

**Response (success, 200):**

```json
{
  "status": "ok",
  "softwareId": "uuid",
  "fieldsUpdated": ["development_status", "version"]
}
```

`fieldsUpdated` returns serializer field names (snake_case) — incoming camelCase keys are auto-decamelized before validation.

**Error responses:**
- `403` — Missing, malformed, or invalid bearer token; or `HSSI_UPDATE_TOKEN` unset on the server
- `400` — Validation error (unknown field, wrong type, controlled-list miss, `submitter` provided)
- `404` — Software not found, or not visible
- `405` — Wrong HTTP method

**Key behaviors:**
- The URL `<uid>` must reference a visible Software entry (404 otherwise)
- Only fields present in the body are updated; omitted fields are untouched
- For M2M fields (authors, keywords, etc.), the provided list **fully replaces** that field
- Empty list `[]` clears the M2M; `null` clears nullable scalars
- `submitter` is rejected with 400 — partial updates cannot rewrite the submitter
- Touches the most recent `SubmissionInfo` on success: sets `modification_description = "Partial update via API: <fields>"` and bumps `date_modified` (auto_now). Does NOT create a new SubmissionInfo
- Does NOT send confirmation emails
- Wrapped in `transaction.atomic()`

### GET /api/list/software/?repo_url=<url> — Software Lookup

Exact-match (case-insensitive) lookup of visible Software by code repository URL. Public — no token required.

**Request:**

```
GET /api/list/software/?repo_url=https://github.com/user/repo
```

**Response (200):**

```json
{
  "data": [
    { "id": "uuid", "name": "PackageName" }
  ]
}
```

The response only includes `id` and `name` — not the repo URL or any other fields. With no `?repo_url=` filter, the endpoint returns all visible software.

**Behavior:** Pure exact-match — no URL normalization (no `.git` stripping, no trailing-slash collapse, no GitHub/GitLab path canonicalization). The agent must canonicalize the repo URL itself before calling this endpoint:

1. Strip trailing `/` and `.git`
2. Lowercase the host (`github.com`, `gitlab.com`)
3. For GitHub URLs of the form `.../tree/<branch>/...` or `.../blob/<branch>/...`, drop everything after the second path segment

If the canonical form returns no match, fall back to a name search via `/api/search/?q=<name>`.

---

## Field Shapes in the PATCH Body

The PATCH body uses the **same key names and shapes** as the `/api/submission/` payload (both go through `SubmissionSerializer` in USER view). `submitter` is the only field rejected by the update path.

| API Field | Shape | Notes |
|-----------|-------|-------|
| `softwareName` | String | |
| `description` | String | |
| `conciseDescription` | String (max 200 chars) | |
| `codeRepositoryUrl` | String URL | Lowercase `Url` |
| `persistentIdentifier` | String (DOI URL) | |
| `documentation` | String URL | |
| `developmentStatus` | String | Must match RepoStatus controlled list |
| `referencePublication` | String (DOI URL) | |
| `publicationDate` | String (`YYYY-MM-DD`) | |
| `logo` | String URL | |
| `licenseFileURL` | String URL | |
| `authors` | Array of Person objects | `{givenName, familyName, identifier, affiliation: [{name, identifier}, ...]}` |
| `publisher` | Organization object | `{name, identifier}` |
| `license` | String | License name only — must match an existing `License.name` (case-insensitive) |
| `version` | Object | `{number, releaseDate, description, versionPid}` |
| `programmingLanguage` | Array of strings | |
| `softwareFunctionality` | Array of strings (`"Parent: Child"`) | |
| `relatedRegion` | Array of strings | |
| `keywords` | Array of strings | |
| `dataSources` | Array of strings | |
| `inputFormats` | Array of strings | |
| `outputFormats` | Array of strings | |
| `operatingSystem` | Array of strings | |
| `cpuArchitecture` | Array of strings | |
| `relatedPhenomena` | Array of strings | |
| `relatedPublications` | Array of strings (URLs) | |
| `relatedDatasets` | Array of strings (URLs) | |
| `relatedSoftware` | Array of strings (URLs) | |
| `interoperableSoftware` | Array of strings (URLs) | |
| `funder` | Array of Organization objects | `{name, identifier}` |
| `awardTitle` | Array of Award objects | `{name, identifier}` |
| `relatedInstruments` | Array of Instrument objects | `{name, identifier}` |
| `relatedObservatories` | Array of Observatory objects | `{name, identifier}` |

---

## Key Differences from `/api/submission/`

| Aspect | `POST /api/submission/` | `PATCH /api/data/software/<uid>/` |
|--------|------------------------|-----------------------------------|
| HTTP method | POST | PATCH |
| Root format | JSON array of submission objects | JSON object of fields to change |
| Software identity | Created — UUID returned | Existing — UUID in URL path |
| Auth | None | Bearer token required |
| Target | Creates new Software | Updates an existing visible Software |
| Required fields | 5 (submitter, name, repo, authors, description) | None — any subset is valid |
| Submitter | Required | **Rejected with 400** |
| Field behavior | All fields set (missing = null) | Only provided fields updated; omitted fields untouched |
| Email | Sends confirmation | No email |
| SubmissionInfo | Creates new | Touches `modification_description` + `date_modified` on existing |
| Reversibility | Creates permanent record | Modifies existing record permanently |

---

## Field Classification

### Static fields (skip during refresh — these don't go stale)

| # | Field | Why static |
|---|-------|-----------|
| 1 | Submitter | Meta-field, not software data |
| 2 | Persistent Identifier | Concept DOI is permanent |
| 3 | Code Repository | Repo URL doesn't move |
| 7 | Software Name | Rarely changes |
| 8 | Description | Subjective, curator-curated |
| 9 | Concise Description | Derived from description |
| 10 | Publication Date | Historical fact |
| 11 | Publisher | Where DOI was issued |
| 14 | Reference Publication | The paper doesn't change |

### Dynamic fields (checked during refresh)

| # | Field | What changes | How to detect |
|---|-------|-------------|--------------|
| 6 | Authors | New contributors | CITATION.cff, Zenodo API |
| 12 | Version | New releases | Git tags, pyproject.toml, Zenodo API |
| 13 | Programming Language | Language additions | File extensions, repo stats |
| 15 | License | License type changes | LICENSE file, pyproject.toml |
| 16 | Keywords | New topics | PyHC registry, repo topics |
| 23 | Development Status | Activity changes | Commit recency |
| 24 | Documentation | URL changes | Verify URL resolves |
| 25 | Funder | New grants | Zenodo/DataCite APIs |
| 26 | Award Title | New awards | Zenodo/DataCite APIs |
| 27 | Related Publications | New papers | Zenodo/DataCite APIs |
| 33 | Logo | URL changes | Verify URL resolves |

### Enrich-only fields (checked only in enrich mode)

| # | Field |
|---|-------|
| 4 | Software Functionality* |
| 5 | Related Region |
| 17 | Data Sources |
| 18 | Input File Formats |
| 19 | Output File Formats |
| 20 | Operating System |
| 21 | CPU Architecture |
| 22 | Related Phenomena |
| 28 | Related Datasets |
| 29 | Related Software |
| 30 | Interoperable Software |
| 31 | Related Instruments |
| 32 | Related Observatories |

*Software Functionality is enrich-only by default but can be refreshed if the user specifically requests it.

---

## Diff Methodology

When comparing fresh metadata against HSSI data, classify each field as:

| Status | Meaning | Action |
|--------|---------|--------|
| **MATCH** | Values equivalent | No update needed |
| **STALE** | HSSI value differs, fresh value is clearly newer | Update (with approval) |
| **ENRICHMENT** | HSSI field is empty, fresh metadata has a value | Add (with approval) |
| **CONFLICT** | Both have values, unclear which is correct | User decides |
| **HSSI-ONLY** | HSSI has value, fresh metadata doesn't | Keep — never remove without explicit approval |

### Safety rules:

- **Additive by default** — Never remove data (reduce authors, remove keywords) unless the user explicitly approves with a warning
- **One PATCH only** — If it fails, report and stop. No retries.
- **Present diff before submitting** — Always show the user what will change

---

## Roundtrip Verification

After a successful update:

1. Re-fetch `GET /api/view/software/<uid>/` from the target URL (no auth required)
2. For each field that was updated, confirm the new value is reflected
3. Report any discrepancies

This is simpler than the submit verification because we only need to check the fields we changed, not all 33.

---

## Controlled-List Endpoints

Same endpoints as the submission payload — use these to normalize values before sending:

| Field | Endpoint |
|-------|----------|
| Software Functionality | `/api/models/FunctionCategory/rows/all/` |
| Related Region | `/api/models/Region/rows/all/` |
| Programming Language | `/api/models/ProgrammingLanguage/rows/all/` |
| Input/Output File Formats | `/api/models/FileFormat/rows/all/` |
| Operating System | `/api/models/OperatingSystem/rows/all/` |
| CPU Architecture | `/api/models/CPUArchitecture/rows/all/` |
| Development Status | `/api/models/RepoStatus/rows/all/` |
| Data Sources | `/api/models/DataInput/rows/all/` |
| Related Phenomena | `/api/models/Phenomena/rows/all/` |
| License | `/api/models/License/rows/all/` |
