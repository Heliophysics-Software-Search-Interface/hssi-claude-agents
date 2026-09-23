# Field 32 — Related Observatories

**Level:** OPTIONAL · **API:** `relatedObservatories[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/InstrumentObservatory/rows/all/` — (type 2)
**Filter tab:** none · **Free-text search tier:** T4.2 (name), T4.3 (abbreviation) · **Field-search code:** `observatory`

## What it is

**Type:** Multi-entry nested group

**What it is:** The mission, observatory, and/or group of instruments the software is designed to support.

**When to include it (relevance):** List a mission/observatory only if the software is *designed to support* it — it directly works with that observatory's/mission's data or data products, implements its data conventions, is purpose-built or a mission-team tool for it, or models/visualizes its measurements as a primary function. Sanity check: would a user searching HSSI for `observatory:"X"`, or a scientist working with X's data, expect this software back? If not, leave it out. **Exclude** observatory-agnostic tools (general models/utilities support none specifically), tutorial/demo/example name-drops and "platforms you *could* support," "configurable for a location/observatory" general tools, and links that belong to another field — a **generic/multi-mission** *data archive/source* (e.g. CDAWeb broadly) → Data Sources, or a generic *file convention* → Input/Output File Formats. **But** if the software directly supports a **specific named mission's** data — including via that mission's own archive, API, or format — that mission *is* designed-to-support: list it here **and** select `Observatory/Mission-specific` in Data Sources (Field 17 instructs this cross-listing). A mission/observatory the software genuinely supports but that isn't in the controlled vocabulary is still *related* — don't drop it at the relevance stage. Carry it into the Field 31 resolution ladder, which decides between a flag and a documented omission. "Related but unresolvable" is never a licence to invent a value.

**How to fill it:** Begin typing the name. Matches from HSSI's controlled instrument/observatory vocabulary appear in the dropdown; choose the correct one. The live form's tooltip still tells submitters the matches come from "the IVOA" — that on-page text is stale: the vocabulary is actually sourced from the heliophysics.net API and resolved to SPASE identifiers (the IVOA-based list is retired). If no entry matches, type the full name. **(That last sentence describes what the web form lets a *human* submitter do. Agents must never free-type a value — see Field 31, rule 22.)**

**Sub-fields:**
- **Observatory Name** (OPTIONAL): Name of the observatory/mission — the matched controlled-list row's `name`, copied verbatim
- **Observatory Identifier** (OPTIONAL): Globally unique persistent identifier — the SPASE Resource ID URL from the controlled list (e.g. `https://spase-metadata.org/SMWG/Observatory/...`). Optional on the form, but **for agents it is mandatory in practice**: an entry without one is not submittable (Field 31, rule 22). Enables improved linking and reliable matching.

## Why it exists

A user working with one mission's or observatory's data wants the software built for it: mission-team
pipelines, readers for that mission's archive, tools purpose-built for a ground network. The
association puts the software in front of them through an `observatory:` search — including by the
mission's short name when the row carries one — and ties the record to a resolvable SPASE resource. As
with instruments, a single association for an agnostic tool misleads by implying a specialisation, and a
bare or mismatched name mis-links or mints a row in the shared vocabulary.

## How it appears on the site

- **Detail page:** in the "Science Context" section, under "Related Observatories", one tag per row.
  The tag links to the row's `landing_url` — a HelioData mission page when the vocabulary refresh has
  confirmed one — otherwise to its SPASE `identifier` (tooltip "View this observatory on HelioData" or
  "… on SPASE"). The tag text is the row's `name` (the raw URL when the name is `UNKNOWN`); the
  abbreviation is not shown on the detail page.
- **Filter:** none.
- **Free-text search:** tier T4.2 on the row `name`, tier T4.3 on its `abbreviation`.
- **Field search:** `observatory:"…"` matches `related_observatories__name__icontains` or
  `related_observatories__abbreviation__icontains`; the value must be quoted. A row with an empty
  abbreviation is not found by the mission's short form.
- **`/api/view/` (plain JSON):** renders the row as `name (abbreviation)` when an abbreviation is set.
- **JSON-LD:** each row is emitted under `mentions` with `description` `relatedObservatories`, `@type`
  `ResearchProject` / `prov:Entity` / `sosa:Platform`, `name` = the row name, and `@id` and `url` = the
  identifier.

## Rubric: include / exclude

**Resolve exactly as Field 31, with `type` 2.** Field 31's Rubric (`31-related-instruments.md`) holds
the single copy of the relevance gate (Stage A, rules 1–8), the resolution procedure (Stage B, rules
9–16), the outcomes (Stage C, rules 17–22) and the incumbent, validation and empty-value rules (23–25).
Apply them unchanged, reading "observatory/mission" for "instrument". Only the following differ or add;
apply them within the Field 31 stages where they fall.

1. **Mission/platform rather than instrument.** List the observatory when the software targets the
   platform — a mission's data products, archive, API or conventions as a whole, a mission-team tool, a
   ground network — and the instrument (Field 31) when it targets one instrument. List both only when both
   are genuinely supported (Field 31, rule 7): when an instrument row is recorded for each unit of a
   fleet, the per-unit observatory row for each of those units belongs here too, because each is
   supported, not for symmetry. A fleet-level row that is independently right (the software supports the
   series broadly) is kept alongside per-unit rows, not displaced by them.

2. **Mission observational record only → this field alone.** When the software's content is derived
   entirely from a named mission's observations but it reads none of that mission's instrument data
   products, record the spacecraft rows the evidence names here and leave Field 31 empty (Field 31,
   rule 7). The evidence decides between per-spacecraft rows and a single grouping row: when the sources
   name each spacecraft, prefer the per-spacecraft rows.

3. **Matching signals** are as Field 31, rule 13 — the row `name`, its `abbreviation`, source
   parenthetical aliases (repos often mention only `PSP`/`MMS`), the SPASE identifier path segments, and
   the definition. The canonical SMWG name is often the long form — `SMWG/Observatory/THEMIS` is named
   "Time History of Events and Macroscale Interactions during Substorms", not "THEMIS" — so copy the
   row's `name` verbatim rather than re-deriving it.

4. **One observatory, one row.** A CNES/CDPP-AMDA duplicate of an observatory already recorded under
   SMWG denotes the same observatory; recording both double-counts the mission. Choose by identifier
   (Field 31, rule 15) and state why.

5. **No instrument-to-observatory fallback here.** Field 31, rule 20 (instrument → observatory
   substitution) has no analogue: an observatory that doesn't resolve goes to Field 31, rule 19 (flag) or
   rule 21 (documented omission). A substitution made under Field 31, rule 20 lands in this field and is
   noted as such. Field 31, rule 22 applies unchanged — **never emit an observatory name without an
   identifier.**

6. **Field 17 coupling.** When a Field 32 entry rests on the software reading that mission's data through
   the mission's own archive, API or format, Field 17 also carries `Observatory/Mission-specific`. When
   it rests on something other than ingesting the mission's data (models trained on its observations),
   Field 17 is decided on its own terms. `Observatory/Mission-specific` in Field 17 with an empty Field 32
   needs its reason checked: when the mission's data access is evidenced but no SPASE row exists for the
   observatory, the Field 17 value stands and the omission is documented (never a bare-name row); clear
   the Field 17 value only when its own source claim is unsupported.

7. **An unfamiliar name on the right row is kept.** A stored row that is the correct entity under the
   canonical authority stays even when its name is not the one users say (a mission's original full
   name, a program-prefixed name). Do not switch to another authority's row for a friendlier name.
   Rows follow the naming policy full name in `name`, short form in `abbreviation`; a missing or wrong
   abbreviation on a shared row is a database correction (see Ask), not a patch value.

## Ask the user only when

Field 31's list applies unchanged: an unresolved collision (Field 31, rule 19), and a proposed
correction to a shared vocabulary row's `name` or `abbreviation` (including adding the short form a
mission is searched by). Every other case is decided by the rubric.

## Where to find it, and traps

Sources, fetch commands and traps are as in Field 31. In addition:

- **Launch-designator names.** Upstream SPASE names some observatory records by COSPAR launch designator
  (GOES 5–8 upstream are `1981-049A`, `1983-041A`, `1987-022A`, `1994-022A`); HSSI rows can hold a
  readable name instead, deliberately. A stored name that differs from its upstream page is checked
  against the row, not "corrected" to the designator.
- **Identical names across scopes.** `…/Observatory/GOES/4` carries exactly the fleet-level
  `…/Observatory/GOES` row's name; a name-only match binds either one. Match on identifier.
- **Program-prefixed names.** Some SMWG rows carry program names (`ISTP/Wind`) or the original mission
  name (`International Solar Polar Mission` for Ulysses) while a CNES archive twin carries the short
  name; that is not a reason to switch rows (rule 7).
- **Authority spellings.** Search by prefix, not by one spelling: `SolarOrbiter` / `Solar_Orbiter` /
  `SolO`.
- **Planned missions and venues are not support.** A mission named as future training data or as the
  audience of a talk is not a supported observatory.

## Payload and roundtrip notes

- **Key:** `relatedObservatories` — an array of `{name, identifier}` objects, built exactly as Field 31's
  (`name` verbatim from the matched row, `identifier` the SPASE Resource ID URL, never `landing_url`).
- **Backend matching, the SPASE gate, the post-patch gate computation, PATCH semantics and the
  non-submittable handling** are identical to Field 31's payload notes; the gate covers
  `relatedInstruments` and `relatedObservatories` together.
- **Readback:** the stored/curator form renames `relatedObservatories[].identifier` →
  `relatedObservatories[].relatedObservatoryIdentifier`; verify on the renamed key. `/api/view/` plain
  JSON renders `name (abbreviation)`; `/api/data/` returns row UUIDs.
- **ORM:** `InstrumentObservatory.observatories` lists the entries citing a row as an observatory
  (`.softwares` is the instrument side).

## Worked examples

- **Provenance of a training set (SAVIC).** SAVIC's shipped models are fits to Helios ion distribution
  data from both spacecraft, but the package reads no Helios data product. Rule 2 fires: `Helios-A`
  (`SMWG/Observatory/Helios1`) and `Helios-B` (`SMWG/Observatory/Helios2`) are recorded here, the SMWG rows
  chosen over their identically named CNES/CDPP-AMDA twins by identifier, Field 31 stays empty, and
  Field 17 keeps its own value. Wind, named only as planned future training data, is excluded.
- **Per-satellite rows follow per-satellite support (sunkit-instruments).** Field 31 records instrument
  rows for eleven GOES satellites, so the observatory row for each of those satellites is added beside
  the fleet-level GOES row, which is kept (rule 1). The observatory rows for the rest of the admissible
  satellite range are not added: a numeric gate is not support for each satellite's data.
- **The right row with an unfamiliar name (PyGS).** The README says "Ulysses" and "WIND"; the stored SMWG
  rows are named `International Solar Polar Mission` and `ISTP/Wind`. They are the correct entities, so
  they are kept (rule 7); switching to CNES rows named `Ulysses` and `Wind` would trade the canonical
  authority for a label. Adding the short forms as abbreviations on the shared rows is a database write
  with its own approval.
- **A data-source value with nothing behind it (pyflct).** Field 32 is empty because the software is
  mission-agnostic, so the stored `Observatory/Mission-specific` data source has no observatory to name
  and is cleared (rule 6).

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 736-754 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
