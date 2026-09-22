# Field 9 — Concise Description

**Level:** OPTIONAL · **API:** `conciseDescription` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T1 · **Field-search code:** `description`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 259-267; other sections are authored in Phase 2. -->

## What it is

**Type:** Text area (max 200 characters)

**What it is:** A description of the item limited to 150-200 characters. If the first 150-200 characters of the description do not provide the desired preview, you may enter an alternate text here.

**How to fill it:** The text should be short and provide a concise preview of the longer description.

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
3. **Description** and **Concise Description** are often in README.md or package metadata

## Payload and roundtrip notes

<!-- moved from .claude/agents/hssi-metadata-submitter.md:106-106 -->
**B. Format and types** — Required fields present and non-empty; objects/arrays match required shapes; dates are ISO `YYYY-MM-DD`; URLs are valid; `conciseDescription` is ≤200 characters.

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 259-267 on 2026-09-22.
