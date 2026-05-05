---
name: update-api-spec
description: >
  Sync the submitter's and updater's API reference skills with the hssi-website
  source code. Use when the HSSI API has changed and reference files need
  syncing. Clones or pulls the hssi-website repo, reads the relevant source
  files, and updates submission-payload, submission-verification, and
  update-payload skills.
---

# Update API Spec

Sync the submitter's and updater's reference files with the latest HSSI API source code.

**When to use:** The HSSI API has changed (new fields, renamed keys, changed shapes, new quirks) and the `submission-payload`, `submission-verification`, or `update-payload` skills need updating.

**How often:** Rarely. The API is relatively stable. Run this when you notice submission/update failures due to field name mismatches, or when the HSSI team announces API changes.

---

## Workflow

### Step 1: Get the hssi-website Source

Clone or pull the HSSI website repository:

```bash
# Clone to a temp location if not already present
git clone https://github.com/Heliophysics-Software-Search-Interface/hssi-website.git /tmp/hssi-website

# Or pull if already cloned
cd /tmp/hssi-website && git pull
```

If the user already has a local clone (e.g., `~/git/hssi-website`), use that instead.

### Step 2: Read the Relevant Source Files

Read these specific files:

#### Shared (covers both submit and update paths)

1. **`concept/import_submission_notes.md`** — Official API documentation. Field list, required/recommended/optional classification, object schemas.

2. **`concept/import_submission.json`** — HSSI developers' curated example payload. Authoritative template for the new-format payload shape; cross-reference with the serializer source.

3. **`django/website/models/serializers/submission.py`** — The DRF `SubmissionSerializer`. Authoritative field mapping and transformation logic for both `POST /api/submission/` (full create) and `PATCH /api/data/software/<uid>/` (partial update — same serializer with `partial=True`). Pay special attention to:
   - `to_internal_value_user()` — required field validation (skipped under `partial=True`)
   - `_get_or_create_person()` — Person dedup and field names (`given_name`/`family_name`)
   - `_get_or_create_org()` — Organization dedup
   - License handling (plain string input, `License.objects.filter(name__iexact=...)`)
   - Version object handling (`number`, `release_date`, `description`, `version_pid`)
   - `update_user()` / `_apply_user_fields()` — the partial-update branch invoked by PATCH

4. **`django/hssi/camel_case_renderer.py`** — `decamelize_data()` and `CamelCaseJSONRenderer`. Explains how incoming camelCase JSON keys are auto-converted to snake_case before the serializer sees them.

5. **`django/website/models/serializers/util.py`** — `SerialView` enum and shared serializer utilities used by submission and software serializers; `HssiSerializer.update()` dispatches to `update_user()` for the USER view.

6. **`django/website/urls.py`** — URL routing. Confirms the current endpoint paths.

#### Submit path

7. **`django/website/views/api/software_api.py`** — `SubmissionAPI` (the `POST /api/submission/` view). Shows the request/response shape, status codes, and the post-commit side effects (`SoftwareEditQueue` creation, email notification) that run outside the atomic transaction.

#### Update path

8. **`django/website/views/api/software_api.py`** (also for update) — `SoftwareDetailAPI`. The `patch()` method is the canonical update endpoint. `get_permissions()` switches to `HasUpdateToken` for PATCH; `get_serializer_class()` switches to `SubmissionSerializer` for PATCH. `SoftwareListAPI.get()` implements the `?repo_url=<url>` filter used by the updater's lookup step.

9. **`django/website/views/api/permissions.py`** — `HasUpdateToken` bearer-token permission class used by `SoftwareDetailAPI.patch()`. Uses `secrets.compare_digest`; fails closed when `HSSI_UPDATE_TOKEN` is unset.

10. **`django/website/test_update_api.py`** — Regression tests for `PATCH /api/data/software/<uid>/` and the `/api/list/software/?repo_url=` lookup. Treat as the authoritative behavioral spec for the update path: response shape, error codes, M2M replacement, `null`-clears-scalar, empty-list-clears-M2M, `submitter` rejection, token unset/invalid.

### Step 3: Compare Against Current Skills

Read the current versions of:
- `.claude/skills/submission-payload/SKILL.md`
- `.claude/skills/submission-verification/SKILL.md`
- `.claude/skills/update-payload/SKILL.md`

Compare the source files against the current skill content. Look for:
- New fields added to the API
- Renamed keys (e.g., snake_case → camelCase changes)
- Changed shapes (e.g., string → object, array → single value)
- New or changed controlled-list endpoints
- New backend quirks or representation differences
- Changes to required vs optional field classification
- Endpoint route or HTTP method changes (especially in `urls.py` and the view classes)

### Step 4: Update the Skill Files

Update `submission-payload/SKILL.md`, `submission-verification/SKILL.md`, and `update-payload/SKILL.md` to reflect any changes found. Specifically:

- Update the Section-to-API-Field Mapping table
- Update Object Specifications if schemas changed
- Update Known Backend Quirks with any new findings
- Update the controlled-list endpoint table if endpoints changed
- Update the known representation differences in `submission-verification`
- For `update-payload`: keep the PATCH endpoint contract, lookup endpoint, and field-shapes table aligned with `software_api.py` + `test_update_api.py`

### Step 5: Report Changes

Produce a summary of what changed and why:
- List each change made to the skill files
- Note any discrepancies between `import_submission.json` and the actual serializer behavior
- Flag any breaking changes that might affect existing payloads

### Step 6: Cleanup

- If you cloned to `/tmp/hssi-website`, either leave it (for future runs) or remove it based on user preference
- If using the user's local clone, leave it as-is
