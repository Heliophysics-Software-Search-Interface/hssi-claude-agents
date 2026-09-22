# Field 7 — Software Name

**Level:** MANDATORY · **API:** `softwareName` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T1 · **Field-search code:** `name`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 241-249; other sections are authored in Phase 2. -->

## What it is

**Type:** Text

**What it is:** The name of the software.

**How to fill it:** The name of the software package as listed on the code repository.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- moved from .claude/agents/hssi-metadata-extractor.md:48-48 -->
- **Preserve editorial intent.** Do not replace a software name, description, concise description, or other subjective wording merely because you would phrase it differently. A stylistic alternative is not "fresh metadata." Keep the seeded value and note the alternative only if it reveals a material ambiguity.

<!-- moved from .claude/agents/hssi-metadata-updater.md:215-215 -->
- **Preserve intentional representation.** A different name, description, concise description, or other subjective wording is not stale merely because the prepared file phrases it differently. Keep HSSI by default; classify the alternative as CONFLICT only when it is materially different and evidence gives the user a real choice. STALE requires objective evidence that HSSI is older, factually wrong, broken, or materially incomplete.

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from RSFF "Notes for AI Agents" -->
2. **Software Name** is typically in the repository name or README

<!-- moved from .claude/agents/hssi-metadata-validator.md:116-118 -->
**Field 7 (Software Name):**
- Compare against: repo name, README title, package name in config files
- Note any inconsistencies (e.g., repo is "pydarn" but package is "pyDARN")

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 241-249 on 2026-09-22.
