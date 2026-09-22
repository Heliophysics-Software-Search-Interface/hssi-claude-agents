# Field 26 — Award Title

**Level:** OPTIONAL · **API:** `award[]` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.5 (name), T4.6 (identifier) · **Field-search code:** `award`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 637-651; other sections are authored in Phase 2. -->

## What it is

**Type:** Multi-entry nested group

**What it is:** The title of the specific grant or award that funded the work.

**How to fill it:** Copy the full title of the award.

**Agent guidance — where funding information comes from.** Prefer the reference publication's **Acknowledgments** section, and read its **Data Availability Statement** too. Crossref's funding metadata flattens distinct tiers into one undifferentiated list — support for the software's authors, an input mission's own funding, and a validation-only data service's funding can all appear together. Record only what funded *this software*; note the others' actual roles as rejected alternatives, so a later refresh doesn't reintroduce them from Crossref. This applies equally to Field 25.

**Sub-fields:**
- **Award Title** (OPTIONAL, multi-entry): Full award title
- **Award Number** (RECOMMENDED): Identifier associated with the award (e.g., NNG19PQ28C). Used by funding agencies to track impact.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- phase2 -->

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from .claude/agents/hssi-metadata-extractor.md:207-209 -->
- **A paper's Acknowledgments and Data Availability Statement are the best source for Fields 25/26,**
  and are where code/data DOIs surface. See Field 25 in `hssi-field-definitions` for why they beat
  Crossref's funding block.

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 637-651 on 2026-09-22.
