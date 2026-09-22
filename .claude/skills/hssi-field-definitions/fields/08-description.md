# Field 8 — Description

**Level:** MANDATORY · **API:** `description` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T1 · **Field-search code:** `description`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 250-258; other sections are authored in Phase 2. -->

## What it is

**Type:** Text area

**What it is:** A description of the item. The first 150-200 characters will be used as the preview.

**How to fill it:** The description should be sufficiently detailed to provide the potential user with information to determine if the software is useful to their work. Include what the software does, why to use it, assumptions it makes, and similar information. Should be written with proper capitalization, grammar, and punctuation.

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

<!-- moved from .claude/agents/hssi-metadata-validator.md:120-123 -->
**Field 8 (Description):**
- Compare against README and package metadata descriptions
- Is it accurate? Does it mischaracterize the software?
- Is the first 150-200 characters a reasonable preview?

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 250-258 on 2026-09-22.
