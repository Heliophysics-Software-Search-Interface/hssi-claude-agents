# Field 3 — Code Repository

**Level:** MANDATORY · **API:** `codeRepositoryUrl` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.8 · **Field-search code:** `repo`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 70-78; other sections are authored in Phase 2. -->

## What it is

**Type:** URL with repository autofill (SoMEF)

**What it is:** Link to the repository where the un-compiled, human readable code and related code is located (SVN, GitHub, CodePlex, institutional GitLab instance, etc.). If the software is restricted, put a link to where a potential user could request access.

**How to fill it:** Navigate to the root page of your repository, copy the entire link, and paste it into this field.

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
1. **Code Repository URL** can be found directly from the repository URL

<!-- moved from .claude/agents/hssi-metadata-validator.md:71-71 -->
- **URLs** must be complete with protocol (Fields 3, 24, 33)

<!-- moved from .claude/agents/hssi-metadata-validator.md:89-90 -->
**Field 3 (Code Repository):**
- Run `git remote -v` in the repo directory and compare

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 70-78 on 2026-09-22.
