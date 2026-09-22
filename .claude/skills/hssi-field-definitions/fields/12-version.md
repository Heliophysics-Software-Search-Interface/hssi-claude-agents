# Field 12 — Version

**Level:** RECOMMENDED · **API:** `version` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** not searched · **Field-search code:** `version` (number)

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 290-304; other sections are authored in Phase 2. -->

## What it is

**Type:** Nested group

**What it is:** Version of the software instance.

**How to fill it:** The version number is often an alphanumeric value, easily accessible on the code repository page (e.g., v1.0.0).

**Sub-fields:**
- **Version Number** (RECOMMENDED): The version identifier
- **Version Date** (RECOMMENDED): Date the specified version was released
- **Version Description** (RECOMMENDED): Brief summary of major changes in the new version (deprecated/new functionalities, features, resolved bugs, etc.)
- **Version PID** (RECOMMENDED): The globally unique persistent identifier for this specific version (e.g., the DOI for the version). Enter full DOI (e.g., https://doi.org/10.5281/zenodo.13287868)

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- phase2 -->

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from RSFF "Notes for AI Agents" -->
9. **Version** information may be in:
   - Git tags
   - Release notes
   - Package version files
   - CHANGELOG.md
11. **DOIs** (Persistent Identifier, Version PID, Reference Publication) may be in:
    - CITATION.cff
    - README badges
    - Zenodo integration
    - codemeta.json

<!-- moved from .claude/agents/hssi-metadata-validator.md:69-69 -->
- **Dates** must be YYYY-MM-DD (Fields 10, 12)

<!-- moved from .claude/agents/hssi-metadata-validator.md:85-87 -->
**Field 2 (Persistent Identifier) & Field 12 (Version PID):**
- Verify DOIs resolve: `curl -s -o /dev/null -w "%{http_code}" https://doi.org/{DOI}`
- Cross-check against CITATION.cff, README badges, codemeta.json

<!-- moved from .claude/agents/hssi-metadata-validator.md:125-128 -->
**Field 12 (Version):**
- Run `git tag --sort=-creatordate` and compare latest tag
- Check pyproject.toml, setup.cfg, setup.py, package.json for version
- Verify version date against git tag date

## Payload and roundtrip notes

<!-- moved from .claude/skills/submission-payload/SKILL.md:260-271 -->
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

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 290-304 on 2026-09-22.
