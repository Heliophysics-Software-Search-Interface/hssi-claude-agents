---
name: submission-payload
description: >
  HSSI API submission payload specification. Contains field mapping from
  hssi_metadata.md to API JSON, payload structure, controlled-list endpoints,
  and normalization rules. Use when building or reasoning about HSSI submissions.
user-invocable: false
---

# HSSI Submission Payload Specification

Build a high-fidelity HSSI submission payload by mapping `hssi_metadata.md` sections to API JSON fields.

> **WARNING: Every POST to `/api/submission/` is irreversible.** It creates a permanent database record and sends a confirmation email to the submitter. There is no sandbox, dry-run, undo, or delete. Build the payload correctly here — do not probe the API with test or partial payloads. If you're unsure about a field's format, consult the example payload or ask the user.

The authoritative API specification lives in the `hssi-website` repo:
- `concept/import_submission_notes.md` — endpoint spec, field list, object schemas
- `concept/import_submission.json` — curated example payload in the new format
- `django/website/views/api/software_api.py` — the DRF `SubmissionAPI` view
- `django/website/models/serializers/submission.py` — the `SubmissionSerializer` (validation + creation logic)

This skill distills that spec into actionable mapping rules. If anything here conflicts with those files, the `hssi-website` source wins.

---

## API Endpoint

- **Method:** `POST /api/submission/` (note the trailing slash)
- **Content-Type:** `application/json`
- **Root format:** JSON array (even for a single submission)
- Each array item is one submission object
- **Success status:** HTTP 201 Created
- **Response:** `{"status": "ok", "count": N, "results": [{"index": 0, "softwareId": "<uuid>"}, ...]}`

### Field name convention

The new DRF-based endpoint uses `CamelCaseJSONRenderer` and `decamelize_data()` to automatically convert camelCase JSON keys to snake_case internally. **Submit with camelCase keys** (e.g., `softwareName`, `codeRepositoryUrl`, `givenName`, `familyName`). The backend serializer accesses the snake_case equivalents (`software_name`, `code_repository_url`, `given_name`, `family_name`) after decamelization.

Snake_case keys will also work because decamelizing an already-snake_case key is a no-op, but camelCase is the documented convention for this endpoint.

---

## Required Fields (Per Object)

Each submission object **must** include these five fields:

### `submitter` (array of Submitter objects)
```json
"submitter": [
  {
    "email": "user@example.org",
    "person": {
      "givenName": "Jane",
      "familyName": "Doe",
      "identifier": "https://orcid.org/0000-0000-0000-0000"
    }
  }
]
```
- DB match is on `email` (case-insensitive)
- `person` is a Person object (see Object Specifications below)

### `softwareName` (string)
```json
"softwareName": "PackageName"
```

### `codeRepositoryUrl` (string URL)
```json
"codeRepositoryUrl": "https://github.com/org/repo"
```
**Note:** The payload key is `codeRepositoryUrl` (lowercase `rl`). Some response representations may render this as `codeRepositoryURL` (uppercase `RL`). Always use lowercase in submissions.

### `authors` (array of Person objects)
```json
"authors": [
  {
    "givenName": "Jane",
    "familyName": "Doe",
    "identifier": "https://orcid.org/0000-0000-0000-0000",
    "affiliation": [
      {
        "name": "Laboratory for Atmospheric and Space Physics",
        "identifier": "https://ror.org/012345678"
      }
    ]
  }
]
```
- `givenName` and `familyName` are required per author
- DB hard match is on `identifier` (when present); falls back to `givenName` + `familyName`

### `description` (string)
```json
"description": "Full description of the software..."
```

---

## Object Specifications

### Person
- `givenName` (required) — string
- `familyName` (required) — string
- `identifier` — URL (typically ORCID)
- `affiliation` — array of Organization objects

### Submitter
- `email` (required) — string
- `person` (required) — Person object

### Organization
- `name` (required) — string
- `identifier` — URL (typically ROR for institutions)

### Instrument / Observatory
- `name` (required) — string
- `identifier` — URL

### Award
- `name` (required) — string
- `identifier` — string (award number/code — not validated as URL)

### Version
- `number` (required) — string (semantic version)
- `releaseDate` — string (ISO `YYYY-MM-DD`)
- `description` — string
- `versionPid` — URL (typically a DOI)

---

## Complete Section-to-API-Field Mapping

| # | Metadata Section | API Field | Type/Shape |
|---|-----------------|-----------|------------|
| 1 | Submitter | `submitter[]` | Array of Submitter objects |
| 2 | Persistent Identifier | `persistentIdentifier` | String (DOI URL) |
| 3 | Code Repository | `codeRepositoryUrl` | String (URL) |
| 4 | Software Functionality | `softwareFunctionality[]` | Array of strings (`"Parent: Child"`) |
| 5 | Related Region | `relatedRegion[]` | Array of strings |
| 6 | Authors | `authors[]` | Array of Person objects |
| 7 | Software Name | `softwareName` | String |
| 8 | Description | `description` | String |
| 9 | Concise Description | `conciseDescription` | String (max 200 chars) |
| 10 | Publication Date | `publicationDate` | String (ISO `YYYY-MM-DD`) |
| 11 | Publisher | `publisher` | Organization object `{name, identifier}` |
| 12 | Version | `version` | Object: `{number, releaseDate, description, versionPid}` |
| 13 | Programming Language | `programmingLanguage[]` | Array of strings |
| 14 | Reference Publication | `referencePublication` | String (DOI URL) |
| 15 | License | `license` | **String** (license name — see below) |
| 16 | Keywords | `keywords[]` | Array of strings |
| 17 | Data Sources | `dataSources[]` | Array of strings |
| 18 | Input File Formats | `inputFormats[]` | Array of strings |
| 19 | Output File Formats | `outputFormats[]` | Array of strings |
| 20 | Operating System | `operatingSystem[]` | Array of strings |
| 21 | CPU Architecture | `cpuArchitecture[]` | Array of strings |
| 22 | Related Phenomena | `relatedPhenomena[]` | Array of strings |
| 23 | Development Status | `developmentStatus` | String |
| 24 | Documentation | `documentation` | String (URL) |
| 25 | Funder | `funder[]` | Array of Organization objects |
| 26 | Award Title | `award[]` | Array of Award objects `{name, identifier}` |
| 27 | Related Publications | `relatedPublications[]` | Array of strings (URLs) |
| 28 | Related Datasets | `relatedDatasets[]` | Array of strings (URLs) |
| 29 | Related Software | `relatedSoftware[]` | Array of strings (URLs) |
| 30 | Interoperable Software | `interoperableSoftware[]` | Array of strings (URLs) |
| 31 | Related Instruments | `relatedInstruments[]` | Array of Instrument objects |
| 32 | Related Observatories | `relatedObservatories[]` | Array of Observatory objects |
| 33 | Logo | `logo` | String (URL) |

**Important:** The API field for Award Title (section 26) is `award`, **not** `awardTitle`.

### License is a plain string

The `license` field is a **plain string** containing the license name — not an object. The serializer looks up `License.objects.filter(name__iexact=<value>)` against the controlled list, so the value must match an entry from `/api/models/License/rows/all/` exactly (case-insensitive).

```json
"license": "BSD 3-Clause \"New\" or \"Revised\" License"
```

### Publisher has no `publisherIdentifier` key

The publisher object uses `{name, identifier}` only. There is no `publisherIdentifier` key — use `identifier` for the ROR or other organizational ID.

```json
"publisher": {
  "name": "Zenodo",
  "identifier": "https://zenodo.org"
}
```

### Version sub-keys are camelCase

The version object uses `releaseDate` and `versionPid` (camelCase). Snake_case (`release_date`, `version_pid`) also works due to auto-decamelization, but camelCase is the documented convention to match the rest of the payload.

```json
"version": {
  "number": "2.4.1",
  "releaseDate": "2025-05-01",
  "description": "Adds GPU acceleration.",
  "versionPid": "https://doi.org/10.XXXX/example"
}
```

---

## Controlled-List Endpoints

Normalize values to **exact** strings from the `name` field in these endpoints on the target base URL:

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

**How to use:** Fetch each relevant endpoint, extract the `name` field from each row, and normalize your metadata values to match exactly. If an extracted value doesn't match any controlled-list entry, flag it for user review rather than silently dropping it.

**Software Functionality format:** Use `"Parent: Child"` (with space after colon). Values must be exact matches from the endpoint. Graph-list lookup walks the parent → child chain.

---

## Normalization Rules

1. **"Not found" means omit** — If a metadata section says "Not found", omit that field from the payload entirely. Do not include `"fieldName": "Not found"`.

2. **Strip source/note prose** — Metadata values may include annotations like `(Source: CITATION.cff)` or `Note: ...`. Strip these to extract only the actual value.

3. **Preserve URLs as-is** — Do not modify URL values. Keep them exactly as extracted.

4. **Exact controlled-list strings** — For fields backed by controlled lists, use the exact string from the endpoint's `name` field. No close-enough matching.

5. **Author name splitting** — If the metadata has full names (e.g., "Jane M. Doe"), split into `givenName: "Jane M."` and `familyName: "Doe"`. Use the last space-separated token as `familyName`, everything before as `givenName`.

6. **Date normalization** — All dates must be ISO format `YYYY-MM-DD`. If only a year is given, use `YYYY-01-01`.

7. **DOI normalization** — DOIs should be full URLs: `https://doi.org/10.XXXX/XXXXX`.

---

## Known Backend Quirks

1. **`codeRepositoryUrl` vs `codeRepositoryURL`** — Submit with lowercase `Url`. Some response representations may return `URL` (uppercase). Both refer to the same field.

2. **Email notifications** — The endpoint sends a confirmation email to the submitter after the DB commit, via `email_existing_edit_link()`. The email send happens **outside** the atomic transaction (after it commits), so an email failure will NOT roll back the submission — but it can still produce an error response even though the DB record was created. Always check the record exists before concluding that a submission failed.

3. **Object deduplication** — The backend matches existing DB records:
   - Person: by `identifier` (ORCID) first, then by `givenName`+`familyName`
   - Submitter: by `email` (case-insensitive)
   - Organization: by `identifier` first, then by `name` (case-insensitive)
   - InstrumentObservatory: by `identifier` first, then by `name`+`type`
   - Award: by `identifier` first, then by `name` (case-insensitive)
   - RelatedItem (publications/datasets/software): by `identifier` (URL)
   - Keyword: case-insensitive name match, created if missing
   
   If a match is found with fewer fields, the DB record is enriched (empty fields filled in). If a match is found with conflicting fields, the existing DB values win.

4. **SoftwareEditQueue creation** — A 90-day edit queue entry is created for each submission (outside the atomic block, after the serializer commits). The `queueId` is not returned in the response — look it up via `/api/models/SoftwareEditQueue/rows/all/` if you need it for verification.

5. **No `submissionId` in response** — Unlike the legacy `/api/submit` endpoint, the new endpoint returns only `softwareId` per result (no `submissionId`).

6. **No dry-run or test mode** — The HSSI API has no sandbox endpoint, no dry-run flag, no email suppression option, and no mechanism to delete submitted records. Every `POST /api/submission/` unconditionally creates a permanent database record and sends a confirmation email. The `submitter.email` field is required. There is no way to submit "silently" or "for testing." Treat every POST as a production action with permanent consequences.

---

## Example Payload

**Primary reference:** `payloads/example_submission.json` in this repo — a clean example payload in the new format. Covers all common fields and object shapes.

**HSSI developers' curated example:** `concept/import_submission.json` in the [hssi-website repo](https://github.com/Heliophysics-Software-Search-Interface/hssi-website). This is the authoritative template maintained by the HSSI developers. Use the `update-api-spec` skill to check for updates.
