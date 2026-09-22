# Field 25 — Funder

**Level:** OPTIONAL · **API:** `funder[]` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.5 (name, abbreviation) · **Field-search code:** `funder`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 624-636; other sections are authored in Phase 2. -->

## What it is

**Type:** Multi-entry nested group

**What it is:** A person or organization that supports (sponsors) something through some kind of financial contribution.

**How to fill it:** The name of the organization that provided the funding (e.g., National Aeronautics and Space Administration). Avoid acronyms and enter one organization per field.

**Sub-fields:**
- **Organization** (RECOMMENDED): Funder name
- **Funder Identifier** (RECOMMENDED): ROR identifier if available (e.g., https://ror.org/027ka1x80)

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- moved from .claude/agents/hssi-metadata-extractor.md:273-273 -->
**Organization names (Author Affiliation, Funder) — expand acronyms.** When you encounter an acronym for an affiliation (Field 6) or funder (Field 25), record the full institutional name instead. Example: `NASA` → `National Aeronautics and Space Administration`. If the source only contains an ambiguous acronym you can't confidently expand, leave it as-is and note it so the validator/user can resolve it.

<!-- moved from .claude/agents/hssi-metadata-validator.md:154-156 -->
**Field 25 (Funder):**
- **Funder organization names should be the full institutional name, not acronyms.** Flag any funder value that is a bare acronym (e.g., `ESA` instead of `European Space Agency`) as a WARNING with `Suggested fix: expand to the full institutional name`. Do not flag values that include an acronym alongside the full name (e.g., "European Space Agency (ESA)").
- Each funder entry should be a single organization — flag entries that combine multiple organizations.

<!-- moved from .claude/agents/hssi-metadata-updater.md:409-413 -->
When extracting fresh values for **Author Affiliation (Field 6)** or **Funder (Field 25)**, record the full institutional name instead of an acronym (example: `NASA` → `National Aeronautics and Space Administration`). When diffing against HSSI, do not flag an existing full name as STALE just because the fresh source uses an acronym — prefer the full-name form. For Funder, also keep one organization per entry rather than combining multiple into a single value.

When an author is itself an **organization** (a lab, consortium, or institution credited as an author), its identifier is a **ROR** (`https://ror.org/…`) rather than an ORCID, and HSSI treats such an author as an organization. During refresh/enrich, match and dedupe these authors by that ROR identifier (exactly as ORCID is used for people), and don't flag a `ror.org` author identifier as invalid.

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from .claude/agents/hssi-metadata-extractor.md:207-209 -->
- **A paper's Acknowledgments and Data Availability Statement are the best source for Fields 25/26,**
  and are where code/data DOIs surface. See Field 25 in `hssi-field-definitions` for why they beat
  Crossref's funding block.

<!-- moved from .claude/agents/hssi-metadata-validator.md:74-74 -->
- **ROR identifiers** must be full URLs: `https://ror.org/XXXXXXXXX` (Fields 6, 11, 25)

## Payload and roundtrip notes

<!-- moved from .claude/agents/hssi-metadata-submitter.md:113-113 -->
**D. Organization-name sanity** — For `affiliation[].name` (Field 6) and `funder[].name` (Field 25), if a value is a bare acronym (e.g., `ESA` rather than `European Space Agency`), surface it in the verification report and ask the user before submitting. Do not auto-expand — the value should already be expanded upstream by the extractor. Also flag funder entries that combine multiple organizations into one value (the form expects one organization per entry).

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 624-636 on 2026-09-22.
