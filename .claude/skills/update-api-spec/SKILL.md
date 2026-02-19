---
name: update-api-spec
description: >
  Update the submitter's API reference files from the hssi-website source code.
  Use when the HSSI API has changed and reference files need syncing.
  Clones or pulls the hssi-website repo, reads the relevant source files,
  and updates submission-payload and submission-verification skills.
---

# Update API Spec

Sync the submitter's reference files with the latest HSSI API source code.

**When to use:** The HSSI API has changed (new fields, renamed keys, changed shapes, new quirks) and the `submission-payload` and `submission-verification` skills need updating.

**How often:** Rarely. The API is relatively stable. Run this when you notice submission failures due to field name mismatches, or when the HSSI team announces API changes.

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

1. **`concept/import_submission_notes.md`** — Official API documentation. Field list, required/recommended/optional classification, object schemas.

2. **`concept/import_submission.json`** — HSSI developers' curated example payload. Check this for the latest field names, shapes, and conventions. **Note:** This file may lag behind the actual API implementation; cross-reference with the parser source.

3. **`django/website/views/api_submit.py`** — The submission endpoint handler. Shows what the backend actually does with submitted data.

4. **`django/website/data_parser.py`** — Contains `api_submission_to_formdict()` and related functions. This is the authoritative field mapping and transformation logic — it defines how submitted JSON is parsed and stored.

5. **`django/website/forms/names.py`** — Field name constants used by the backend. Reveals the canonical internal field names.

### Step 3: Compare Against Current Skills

Read the current versions of:
- `.claude/skills/submission-payload/SKILL.md`
- `.claude/skills/submission-verification/SKILL.md`

Compare the source files against the current skill content. Look for:
- New fields added to the API
- Renamed keys (e.g., snake_case → camelCase changes)
- Changed shapes (e.g., string → object, array → single value)
- New or changed controlled-list endpoints
- New backend quirks or representation differences
- Changes to required vs optional field classification

### Step 4: Update the Skill Files

Update `submission-payload/SKILL.md` and `submission-verification/SKILL.md` to reflect any changes found. Specifically:

- Update the Section-to-API-Field Mapping table
- Update Object Specifications if schemas changed
- Update Known Backend Quirks with any new findings
- Update the controlled-list endpoint table if endpoints changed
- Update the known representation differences in `submission-verification`

### Step 5: Report Changes

Produce a summary of what changed and why:
- List each change made to the skill files
- Note any discrepancies between `import_submission.json` and the actual parser behavior
- Flag any breaking changes that might affect existing payloads

### Step 6: Cleanup

- If you cloned to `/tmp/hssi-website`, either leave it (for future runs) or remove it based on user preference
- If using the user's local clone, leave it as-is
