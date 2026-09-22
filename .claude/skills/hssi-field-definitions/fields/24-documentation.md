# Field 24 — Documentation

**Level:** RECOMMENDED · **API:** `documentation` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.8 · **Field-search code:** `docs`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 615-623; other sections are authored in Phase 2. -->

## What it is

**Type:** URL

**What it is:** Link to the documentation and installation instructions. If this is the same as the access URL, then enter that link here.

**How to fill it:** Documentation link including installation instructions. Should be entered as a complete URL.

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
8. **Documentation** URL is often in:
   - README.md links
   - docs/ folder
   - .readthedocs.yml or other doc configuration

<!-- moved from .claude/agents/hssi-metadata-validator.md:71-71 -->
- **URLs** must be complete with protocol (Fields 3, 24, 33)

<!-- moved from .claude/agents/hssi-metadata-validator.md:144-146 -->
**Field 24 (Documentation):**
- Verify URL resolves: `curl -s -o /dev/null -w "%{http_code}" {URL}`
- Cross-check against README links and docs/ folder

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 615-623 on 2026-09-22.
