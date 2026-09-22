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
- For M2M fields (authors, keywords, etc.), the provided list **fully replaces** that field — the API does **not** merge. To *add* to an M2M field without dropping anything, send the full intended identity-aware set = **`existing ∪ new`** (fetch the current values, union in the new ones). This is why enriching a shallow-but-non-empty M2M list (e.g. adding Software Functionality values to an entry that already has one) still requires sending the existing values alongside the new ones.
- Empty list `[]` clears the M2M; `null` clears nullable scalars
- `submitter` is rejected with 400 — partial updates cannot rewrite the submitter
- Touches the most recent `SubmissionInfo` on success: sets `modification_description = "Partial update via API: <fields>"` and bumps `date_modified` (auto_now). Does NOT create a new SubmissionInfo
- Does NOT send confirmation emails
- Wrapped in `transaction.atomic()`

**Shared structured-entity limitations:**

- Top-level M2M associations such as `authors`, `funder`, `award`, `relatedInstruments`, and `relatedObservatories` are replaced by the complete submitted list.
- People, organizations, awards, instruments, and observatories are shared database entities. When an identifier matches an existing entity, PATCH reuses it and does **not** overwrite its nonblank name. Identity matching therefore prevents duplicates but does not make a conflicting label equivalent or patchable.
- Author affiliations are added to the matched Person; the endpoint does not remove existing affiliations. Union affiliations for matched authors. Treat any requested affiliation removal as NON-PATCHABLE.
- Publications, datasets and software share `RelatedItem` rows matched by identifier alone. Reusing an
  identifier does **not** change the row's existing semantic `type`; moving a URL between relation
  fields can therefore leave JSON-LD with the old type. Treat the type correction as NON-PATCHABLE
  and verify the serialized type independently.
- Omit shared-entity renames and nested affiliation removals from the PATCH and report them as hard blockers requiring the CSV/manual database workflow. Top-level association removals are still supported when the user approves the complete replacement list.

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

If the canonical form returns no match, fall back to a name search via `/api/search/?q=<name>&mode=id`, which returns `{"results": ["<uuid>", ...]}`. **`mode=id` is required**: since hssi-website PR #55 this endpoint defaults to `mode=jsonld` (full JSON-LD objects), not a UUID list.

---

## Transient Update Plan

PREPARE and EXECUTE communicate through a transient update-plan file under the gitignored `payloads/` directory. The wrapper preserves the exact approved target, identity, baseline, and PATCH body across separate agent invocations:

```json
{
  "softwareId": "<uuid>",
  "softwareName": "<display name>",
  "mode": "apply",
  "targetUrl": "https://hssi.hsdcloud.org",
  "metadataFile": "<working hssi_metadata.md path>",
  "preparedAt": "<ISO-8601 timestamp>",
  "baseline": {
    "<only fields in patch>": "<normalized current HSSI values>"
  },
  "patch": {
    "<only approved changed fields>": "<approved final API values>"
  },
  "blockers": []
}
```

- `softwareId` and `targetUrl` identify the exact PATCH URL; EXECUTE must not infer or override either.
- `mode` records the actual Updater mode; the file-driven full-refresh workflow uses `apply`.
- `baseline` contains exactly the fields in `patch`, represented in the same normalized API shapes used for comparison.
- `patch` contains only changed metadata fields and never `submitter`.
- `blockers` must exist and be empty before the plan can be approved or executed.
- The HTTP body is the nested `patch` object only, never the wrapper.
- The plan is disposable operational state. Do not commit it or treat it as the canonical metadata record.

Immediately before PATCH, re-fetch the same UUID from the exact target and compare every recorded baseline field. Abort without sending anything if a value changed; return to PREPARE so the user can review and approve a newly based plan.

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
| `logo` | String URL | ≤200 chars (`URLField(max_length=200)`). A git-hosted URL must be commit-pinned (`raw.githubusercontent.com/<owner>/<repo>/<40-hex-sha>/<path>`, or `media.githubusercontent.com/media/…` for Git-LFS paths) — never a branch or a `/blob/` page. |
| `authors` | Array of Person objects | `{givenName, familyName, identifier, affiliation: [{name, identifier}, ...]}` |
| `publisher` | Organization object | `{name, identifier}` |
| `license` | String | License name only — must match an existing `License.name` (case-insensitive) |
| `version` | Object | `{number, releaseDate, description, versionPid}` |
| `programmingLanguage` | Array of strings | |
| `softwareFunctionality` | Array of strings (`"Parent: Child"`) | **Always also include the bare parent top-level category as its own array entry** (e.g. `"Data Processing and Analysis"` alongside `"Data Processing and Analysis: Data Access and Retrieval"`). Selecting a subcategory does NOT auto-add its parent. See the `software-functionality` skill. |
| `relatedRegion` | Array of strings | |
| `keywords` | Array of strings | |
| `dataSources` | Array of strings | |
| `inputFormats` | Array of strings | |
| `outputFormats` | Array of strings | |
| `operatingSystem` | Array of strings | |
| `cpuArchitecture` | Array of strings | |
| `relatedPhenomena` | Array of strings | |
| `relatedPublications` | Array of strings (URLs) | real URLs only, each ≤128 chars (see note below) |
| `relatedDatasets` | Array of strings (URLs) | real URLs only, each ≤128 chars (see note below) |
| `relatedSoftware` | Array of strings (URLs) | real URLs only, each ≤128 chars (see note below) |
| `interoperableSoftware` | Array of strings (URLs) | real URLs only, each ≤128 chars (see note below) |
| `funder` | Array of Organization objects | `{name, identifier}` |
| `award` | Array of Award objects | `{name, identifier}` (the API field is `award`, **not** `awardTitle`) |
| `relatedInstruments` | Array of Instrument objects | `{name, identifier}` |
| `relatedObservatories` | Array of Observatory objects | `{name, identifier}` |

**RelatedItem URL note (`relatedPublications`/`relatedDatasets`/`relatedSoftware`/`interoperableSoftware`):** each entry must be a real URL — free text fails the serializer's `URLValidator` (`Invalid URL: '<value>'`) and rejects the whole atomic PATCH. Keep each URL ≤128 characters: `_get_or_create_related` stores the URL as both `identifier` and the 128-capped `name`, so a longer URL passes validation and then fails at the database write.

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
| 33 | Logo | URL changes; a git-hosted URL still on a branch or `/blob/` must be repointed at a commit SHA | `curl -sIL` — require `image/*`; a 200 with `text/plain` (LFS pointer) or `text/html` (`blob/` page) is a broken logo |

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
| **ENRICHMENT** | HSSI field is empty **— or, for an M2M field, the fresh set contains values HSSI lacks** | Add the new value(s), keeping any existing ones (with approval) |
| **CONFLICT** | Both have values, unclear which is correct | User decides |
| **HSSI-ONLY** | HSSI has value, fresh metadata doesn't | Keep — never remove without explicit approval |
| **NON-PATCHABLE** | The desired change targets a shared-entity attribute or nested affiliation removal that PATCH cannot perform | Block PATCH; route to CSV/manual correction |

### Safety rules:

- **Additive by default** — Never remove data (reduce authors, remove keywords) unless the user explicitly approves with a warning
- **M2M enrichment is identity-aware set-union** — to add values to an M2M field, send `existing ∪ new` (the API replaces the whole field, it does not merge). Expand shallow non-empty lists (e.g. Software Functionality with only 1–2 values) rather than skipping them as "already populated." If the user explicitly approves a removal, send the complete approved final set; do not union the removed member back in.
- **Match structured entries by stable identity before name without ignoring attributes** — authors by ORCID, then normalized name; author affiliations and organizations by ROR, then normalized name; awards by identifier, then normalized name; instruments and observatories by normalized SPASE identifier, then canonical name. For matched authors, union affiliations. After identity matching, separately compare labels and nested values; route non-PATCHable shared-entity differences through the blocker rule above. Compare scalar controlled-value and URL collections as normalized sets.
- **Submitter is out of scope** — never include Field 1 in an update diff, baseline, or PATCH.
- **One PATCH only** — If it fails, report and stop. No retries.
- **Present the exact plan before submitting** — Always show the diff, complete update plan, and nested PATCH body the user is approving.

---

## Roundtrip Verification

After a successful update:

1. Re-fetch `GET /api/view/software/<uid>/` from the target URL (no auth required)
2. For each field that was updated, confirm the new value is reflected
3. Confirm the response did not report a field outside the nested `patch` as updated
4. Report any discrepancies without retrying

This is simpler than the submit verification because we only need to check the fields we changed, not all 33.

---

## Controlled-List Endpoints

Same endpoints as the submission payload; the single field → model table is `hssi-field-definitions/sources/vocabulary-authority.md`. Normalize values to exact `name` strings before sending.

**Instruments / Observatories:** apply the relevance gate and the SPASE resolution ladder in `hssi-field-definitions/fields/31-related-instruments.md` — the single authoritative copy. Never send a `name` without a SPASE `identifier`; never send `landing_url`.
