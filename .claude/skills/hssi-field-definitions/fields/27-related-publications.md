# Field 27 — Related Publications

**Level:** OPTIONAL · **API:** `relatedPublications[]` · **Change class:** dynamic
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.3 (name) · **Field-search code:** `publication`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 654-662; other sections are authored in Phase 2. -->

## What it is

**Type:** Multi-entry URL (RelatedItem lookup — DOI URL preferred)

**What it is:** Publications that describe, cite, or use the software that the software developer prioritizes but are different from the reference publication.

**How to fill it:** Enter the URLs — ideally DOIs — for all notable publications the software is cited in, one URL per entry (the form's "+ add" button adds a field per URL). Only a URL is accepted per entry; free-text citations are rejected. For a publication with no DOI, use any permanent link (e.g., its ADS abstract page, `https://ui.adsabs.harvard.edu/abs/<bibcode>/abstract`) and record the full citation in the dossier prose instead.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- phase2 -->

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- moved from .claude/agents/hssi-metadata-extractor.md:389-390 -->
- For a field that a publication could supply (Fields 14, 25, 26, 27), check the paper's
  Acknowledgments and Data Availability Statement before concluding it isn't there — see Step 1d

## Payload and roundtrip notes

<!-- moved from .claude/skills/submission-payload/SKILL.md:239-239 -->
**Important — RelatedItem URL fields (27–30):** each entry must be a real URL. Free text fails the serializer's `URLValidator` (`Invalid URL: '<value>'`) and rejects the whole atomic request. Keep each URL ≤128 characters: `_get_or_create_related` stores the URL as both `identifier` and the 128-capped `name`, so a longer URL passes validation and then fails at the database write.

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 654-662 on 2026-09-22.
