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

The authoritative API specification lives in the `hssi-website` repo:
- `concept/import_submission_notes.md` — endpoint spec, field list, object schemas
- `concept/import_submission.json` — curated example payload (kept up-to-date by HSSI developers)

This skill distills that spec into actionable mapping rules. If anything here conflicts with those files, the `hssi-website` source wins.

---

## API Endpoint

- **Method:** `POST /api/submit`
- **Content-Type:** `application/json`
- **Root format:** JSON array (even for a single submission)
- Each array item is one submission object

---

## Required Fields (Per Object)

Each submission object **must** include these five fields:

### `submitter` (array of Submitter objects)
```json
"submitter": [
  {
    "email": "user@example.org",
    "person": {
      "firstName": "Jane",
      "lastName": "Doe",
      "identifier": "https://orcid.org/0000-0000-0000-0000"
    }
  }
]
```
- DB match is on `email`
- `person` is a Person object (see Object Specifications below)

### `softwareName` (string)
```json
"softwareName": "PackageName"
```

### `codeRepositoryUrl` (string URL)
```json
"codeRepositoryUrl": "https://github.com/org/repo"
```
**Note:** The payload key is `codeRepositoryUrl` (lowercase `rl`). The `/api/view` response may show `codeRepositoryURL` (uppercase `RL`). Always use lowercase in submissions.

### `authors` (array of Person objects)
```json
"authors": [
  {
    "firstName": "Jane",
    "lastName": "Doe",
    "identifier": "https://orcid.org/0000-0000-0000-0000",
    "affiliation": [
      {
        "name": "Laboratory for Atmospheric and Space Physics",
        "abbreviation": "LASP",
        "identifier": "https://ror.org/012345678"
      }
    ]
  }
]
```
- `firstName` and `lastName` are required per author
- DB hard match is on `identifier`; falls back to `firstName` + `lastName`

### `description` (string)
```json
"description": "Full description of the software..."
```

---

## Object Specifications

### Person
- `firstName` (required) — string
- `lastName` (required) — string
- `identifier` — URL (typically ORCID)
- `affiliation` — array of Organization objects

### Submitter
- `email` (required) — string
- `person` (required) — Person object

### Organization
- `name` (required) — string
- `abbreviation` — string
- `identifier` — URL (typically ROR)

### Instrument / Observatory
- `name` (required) — string
- `abbreviation` — string
- `identifier` — URL
- `definition` — text description

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
| 11 | Publisher | `publisher` | Organization object |
| 12 | Version | `version` | Object: `{number, release_date, description, version_pid}` |
| 13 | Programming Language | `programmingLanguage[]` | Array of strings |
| 14 | Reference Publication | `referencePublication` | String (DOI URL) |
| 15 | License | `license` | Object: `{name, url}` |
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
| 26 | Award Title | `award[]` | Array of `{name, identifier}` |
| 27 | Related Publications | `relatedPublications[]` | Array of strings (URLs) |
| 28 | Related Datasets | `relatedDatasets[]` | Array of strings (URLs) |
| 29 | Related Software | `relatedSoftware[]` | Array of strings (URLs) |
| 30 | Interoperable Software | `interoperableSoftware[]` | Array of strings (URLs) |
| 31 | Related Instruments | `relatedInstruments[]` | Array of Instrument objects |
| 32 | Related Observatories | `relatedObservatories[]` | Array of Observatory objects |
| 33 | Logo | `logo` | String (URL) |

**Important:** The API field for Award Title (section 26) is `award`, **not** `awardTitle`.

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

**Software Functionality format:** Use `"Parent: Child"` (with space after colon). Values must be exact matches from the endpoint.

---

## Normalization Rules

1. **"Not found" means omit** — If a metadata section says "Not found", omit that field from the payload entirely. Do not include `"fieldName": "Not found"`.

2. **Strip source/note prose** — Metadata values may include annotations like `(Source: CITATION.cff)` or `Note: ...`. Strip these to extract only the actual value.

3. **Preserve URLs as-is** — Do not modify URL values. Keep them exactly as extracted.

4. **Exact controlled-list strings** — For fields backed by controlled lists, use the exact string from the endpoint's `name` field. No close-enough matching.

5. **Author name splitting** — If the metadata has full names (e.g., "Jane M. Doe"), split into `firstName: "Jane M."` and `lastName: "Doe"`. Use the last space-separated token as `lastName`, everything before as `firstName`.

6. **Date normalization** — All dates must be ISO format `YYYY-MM-DD`. If only a year is given, use `YYYY-01-01`.

7. **DOI normalization** — DOIs should be full URLs: `https://doi.org/10.XXXX/XXXXX`.

---

## Known Backend Quirks

1. **`codeRepositoryUrl` vs `codeRepositoryURL`** — Submit with lowercase `Url`. The view API may return `URL` (uppercase). Both refer to the same field.

2. **Email timing** — Email sending happens after the DB commit during the submit flow. If the email send fails (e.g., rejected recipient), the API can return an error status even though the submission was successfully stored. Always check `/api/view/<softwareId>/` if you get an error that might be email-related.

3. **Version field reshaping** — The submission payload uses `version.number`, `version.release_date`, `version.description`, `version.version_pid`. The stored/view representation may reshape these to `versionNumber`, `versionDate`, `versionDescription`, etc.

4. **Object deduplication** — The backend matches existing DB records: Person by `identifier` then `firstName`+`lastName`, Submitter by `email`, Organization by `identifier`, Instrument/Observatory by `identifier`. If a match is found with fewer fields, the DB record is updated. If a match is found with conflicting fields, the existing DB values win.

5. **`import_submission.json` may lag behind the actual API** — The HSSI developers' curated example (`concept/import_submission.json` in hssi-website) is the intended spec but may be out of sync with the actual backend implementation (e.g., PR #11 proposes camelCase version fields and removing `abbreviation`/`definition`). When in doubt, trust the field names and shapes used in `payloads/gemini3d_submission.json`, which successfully submitted and passed roundtrip verification against the live API.

---

## Example Payloads

**Primary reference:** `payloads/gemini3d_submission.json` in this repo — a complex, real-world payload that successfully submitted and passed roundtrip verification against the live HSSI API. Covers all common fields including optional ones.

**Simple reference:** `payloads/ACE_magnetometer_submission.json` — a simpler payload with fewer optional fields.

**HSSI developers' curated example:** `concept/import_submission.json` in the [hssi-website repo](https://github.com/Heliophysics-Software-Search-Interface/hssi-website). This is the intended spec but may lag behind the actual API implementation (see quirk #5 above). Use the `update-api-spec` skill to check for updates.
