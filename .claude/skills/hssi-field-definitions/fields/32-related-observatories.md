# Field 32 — Related Observatories

**Level:** OPTIONAL · **API:** `relatedObservatories[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/InstrumentObservatory/rows/all/` — (type 2)
**Filter tab:** none · **Free-text search tier:** T4.2 (name), T4.3 (abbreviation) · **Field-search code:** `observatory`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 736-754; other sections are authored in Phase 2. -->

## What it is

**Type:** Multi-entry nested group

**What it is:** The mission, observatory, and/or group of instruments the software is designed to support.

**When to include it (relevance):** List a mission/observatory only if the software is *designed to support* it — it directly works with that observatory's/mission's data or data products, implements its data conventions, is purpose-built or a mission-team tool for it, or models/visualizes its measurements as a primary function. Sanity check: would a user searching HSSI for `observatory:"X"`, or a scientist working with X's data, expect this software back? If not, leave it out. **Exclude** observatory-agnostic tools (general models/utilities support none specifically), tutorial/demo/example name-drops and "platforms you *could* support," "configurable for a location/observatory" general tools, and links that belong to another field — a **generic/multi-mission** *data archive/source* (e.g. CDAWeb broadly) → Data Sources, or a generic *file convention* → Input/Output File Formats. **But** if the software directly supports a **specific named mission's** data — including via that mission's own archive, API, or format — that mission *is* designed-to-support: list it here **and** mark the source `observatory-specific` in Data Sources (Field 17 already instructs this cross-listing). A mission/observatory the software genuinely supports but that isn't in the controlled vocabulary is still *related* — don't drop it at the relevance stage. Carry it into the Field 31 resolution ladder, which decides between a broader platform association and a documented omission. "Related but unresolvable" is never a licence to invent a value.

**How to fill it:** Begin typing the name. Matches from HSSI's controlled instrument/observatory vocabulary appear in the dropdown; choose the correct one. The live form's tooltip still tells submitters the matches come from "the IVOA" — that on-page text is stale: the vocabulary is actually sourced from the heliophysics.net API and resolved to SPASE identifiers (the IVOA-based list is retired). If no entry matches, type the full name. **(That last sentence describes what the web form lets a *human* submitter do. Agents must never free-type a value — see Agent guidance below.)**

**Agent guidance:** Apply the **SPASE resolution ladder under Field 31** — it governs Field 32 identically, matching on `type` 2 (observatory) instead of 1. Do not restate or reinterpret it here.

Field-32-specific notes: match against the row `name`, its `abbreviation`, source parenthetical aliases (repos often mention only `PSP`/`MMS`), and the SPASE identifier path segments. The canonical SMWG name is often the long form — `SMWG/Observatory/THEMIS` is named "Time History of Events and Macroscale Interactions during Substorms", not "THEMIS" — so copy the row's `name` verbatim rather than re-deriving it. Ladder rule 4 (instrument → observatory fallback) has no analogue here: an observatory that doesn't resolve goes to rule 3 or rule 5. Rule 6 applies unchanged — **never emit an observatory name without an identifier.**

**Sub-fields:**
- **Observatory Name** (OPTIONAL): Name of the observatory/mission — the matched controlled-list row's `name`, copied verbatim
- **Observatory Identifier** (OPTIONAL): Globally unique persistent identifier — the SPASE Resource ID URL from the controlled list (e.g. `https://spase-metadata.org/SMWG/Observatory/...`). Optional on the form, but **for agents it is mandatory in practice**: an entry without one is not submittable (ladder rule 6). Enables improved linking and reliable matching.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- phase2 -->

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- phase2 -->

## Payload and roundtrip notes

<!-- phase2 -->

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 736-754 on 2026-09-22.
