# Field 2 — Persistent Identifier

**Level:** RECOMMENDED · **API:** `persistentIdentifier` · **Change class:** static
**Vocabulary:** free text / no controlled list
**Filter tab:** none · **Free-text search tier:** not searched · **Field-search code:** `pid`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 61-69; other sections are authored in Phase 2. -->

## What it is

**Type:** DataCite DOI lookup with autofill

**What it is:** The globally unique persistent identifier for the software (e.g., the concept DOI for all versions).

**How to fill it:** If the software already has a concept DOI, enter the full DOI here (e.g., https://doi.org/10.5281/zenodo.13287868). Entering the concept DOI enables automatic population of metadata from that DOI.

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
11. **DOIs** (Persistent Identifier, Version PID, Reference Publication) may be in:
    - CITATION.cff
    - README badges
    - Zenodo integration
    - codemeta.json

<!-- moved from .claude/agents/hssi-metadata-validator.md:70-70 -->
- **DOIs** must be full URLs: `https://doi.org/10.XXXX/XXXXX` (Fields 2, 12, 14, 27, 28, 29, 30). **Field 31 (Instrument Identifier) is normally a SPASE Resource ID URL** (`https://spase-metadata.org/...`), not a DOI — do **not** flag a SPASE identifier as a malformed DOI (a DOI there is only a manual exception).

<!-- moved from .claude/agents/hssi-metadata-validator.md:85-87 -->
**Field 2 (Persistent Identifier) & Field 12 (Version PID):**
- Verify DOIs resolve: `curl -s -o /dev/null -w "%{http_code}" https://doi.org/{DOI}`
- Cross-check against CITATION.cff, README badges, codemeta.json

<!-- moved from .claude/agents/hssi-metadata-validator.md:178-181 -->
1. **Search for DOIs** the extractor may not have found:
   - Grep for `doi` (case-insensitive) across the repo
   - Check README badges for DOI shields
   - Check for `.zenodo.json` or `codemeta.json`

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 61-69 on 2026-09-22.
