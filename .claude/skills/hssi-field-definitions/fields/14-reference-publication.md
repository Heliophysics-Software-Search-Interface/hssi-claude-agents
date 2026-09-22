# Field 14 — Reference Publication

**Level:** OPTIONAL · **API:** `referencePublication` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** T4.3 (name) · **Field-search code:** `reference_publication`, `publication`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 338-346; other sections are authored in Phase 2. -->

## What it is

**Type:** DataCite DOI

**What it is:** The DOI for the publication describing the software, sometimes used as the preferred citation for the software in addition to the version-specific citation to the code itself.

**How to fill it:** Enter the DOI for the publication describing the software (e.g., a JOSS paper).

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
7. **Reference Publication** tends to be obvious when it exists:
   - CITATION.cff file
   - README recommendations for how to cite the package
11. **DOIs** (Persistent Identifier, Version PID, Reference Publication) may be in:
    - CITATION.cff
    - README badges
    - Zenodo integration
    - codemeta.json

<!-- moved from .claude/agents/hssi-metadata-extractor.md:389-390 -->
- For a field that a publication could supply (Fields 14, 25, 26, 27), check the paper's
  Acknowledgments and Data Availability Statement before concluding it isn't there — see Step 1d

<!-- moved from .claude/agents/hssi-metadata-validator.md:70-70 -->
- **DOIs** must be full URLs: `https://doi.org/10.XXXX/XXXXX` (Fields 2, 12, 14, 27, 28, 29, 30). **Field 31 (Instrument Identifier) is normally a SPASE Resource ID URL** (`https://spase-metadata.org/...`), not a DOI — do **not** flag a SPASE identifier as a malformed DOI (a DOI there is only a manual exception).

<!-- moved from .claude/agents/hssi-metadata-validator.md:135-137 -->
**Field 14 (Reference Publication):**
- Verify DOI resolves
- Cross-check against CITATION.cff preferred-citation and README citation sections

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 338-346 on 2026-09-22.
