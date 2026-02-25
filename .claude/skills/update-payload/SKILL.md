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

> **WARNING: Every POST to `/api/update` modifies the production database permanently.** There is no undo. Build the payload correctly, get user approval, and submit once. Do not retry on failure.

---

## Authentication

Both endpoints require a bearer token:

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

### POST /api/update — Partial Update

Updates only the specified fields on an existing VisibleSoftware entry. Omitted fields are untouched.

**Request:**

```json
{
  "softwareId": "uuid-of-visible-software",
  "fields": {
    "developmentStatus": "Active",
    "version": {
      "number": "v2.0.0",
      "release_date": "2026-01-15",
      "description": "Major rewrite",
      "version_pid": "https://doi.org/10.5281/zenodo.99999999"
    }
  }
}
```

**Response (success):**

```json
{
  "status": "ok",
  "softwareId": "uuid",
  "fieldsUpdated": ["developmentStatus", "versionNumber"]
}
```

**Error responses:**
- `403` — Missing, malformed, or invalid bearer token
- `400` — Invalid JSON, missing softwareId, empty fields, software not found, update failed
- `405` — Wrong HTTP method

**Key behaviors:**
- `softwareId` must reference a VisibleSoftware entry (rejects non-visible)
- Only fields present in `fields` are updated; omitted fields are untouched
- For M2M fields (authors, keywords, etc.), the provided value **fully replaces** that field (clear + re-add)
- Updates `dateModified` on the existing SubmissionInfo — does NOT create a new one
- Does NOT send confirmation emails
- Wrapped in `transaction.atomic()`

### GET /api/update/lookup — Software Lookup

Exact-match lookup of VisibleSoftware by code repository URL.

**Request:**

```
GET /api/update/lookup?repo_url=https://github.com/user/repo
Authorization: Bearer <token>
```

**Response (single match):**

```json
{
  "softwareId": "uuid",
  "softwareName": "PackageName",
  "codeRepositoryUrl": "https://github.com/user/repo"
}
```

**Response (zero or multiple matches):**

```json
{
  "results": [...]
}
```

---

## Field Shapes in `fields` Object

The `fields` object uses the **same key names and shapes** as the `/api/submit` payload, with these notes:

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
| `authors` | Array of Person objects | `{firstName, lastName, identifier, affiliation}` |
| `publisher` | Organization object | `{name, identifier}` |
| `license` | Object or string | `{name, url}` or just the name |
| `version` | Object | `{number, release_date, description, version_pid}` |
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

## Key Differences from `/api/submit`

| Aspect | `/api/submit` | `/api/update` |
|--------|--------------|---------------|
| Root format | JSON array | JSON object |
| Auth | None | Bearer token required |
| Target | Creates new Software | Updates existing VisibleSoftware |
| Required fields | 5 (submitter, name, repo, authors, description) | Only `softwareId` |
| Submitter | Required | Not used |
| Field behavior | All fields set (missing = null) | Only provided fields updated |
| Email | Sends confirmation | No email |
| SubmissionInfo | Creates new | Updates existing `dateModified` |
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
- **One POST only** — If it fails, report and stop. No retries.
- **Present diff before submitting** — Always show the user what will change

---

## Roundtrip Verification

After a successful update:

1. Re-fetch `GET /api/view/<softwareId>/` from the target URL
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
