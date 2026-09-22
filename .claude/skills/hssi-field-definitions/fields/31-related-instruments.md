# Field 31 — Related Instruments

**Level:** OPTIONAL · **API:** `relatedInstruments[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/InstrumentObservatory/rows/all/` — (type 1)
**Filter tab:** none · **Free-text search tier:** T4.2 (name, abbreviation) · **Field-search code:** `instrument`

<!-- Sections below follow the template in ../SKILL.md. "What it is" and "Where to find it" carry text moved
     verbatim from resource_submission_form_fields.md (RSFF) lines 704-735; other sections are authored in Phase 2. -->

## What it is

**Type:** Multi-entry nested group

**What it is:** The instrument the software is designed to support.

**When to include it (relevance):** List an instrument only if the software is *designed to support* it — it directly reads/writes/parses/calibrates/processes that specific instrument's data, implements a data format/convention specific to it (as a means of supporting it), is purpose-built or an instrument-team tool for it, or models/visualizes its measurements as a primary function. Sanity check: would a user searching HSSI for `instrument:"X"`, or someone working with X's data, expect this software back? If not, leave it out. **Exclude** instrument-agnostic tools (general models/utilities/frameworks support none specifically), tutorial/demo/example name-drops, "configurable for" / "commonly used with" / "optimized for" mentions of an otherwise-agnostic tool, and links that belong to another field — **generic** support for a multi-instrument *file format* (FITS/CDF/netCDF) → Input/Output File Formats, or a **generic/multi-mission** *data archive/source* (e.g. CDAWeb broadly) → Data Sources. **But** an instrument-**specific** parser, format, convention, or data source/API *does* count as designed-to-support — list that instrument here. Note: an instrument the software genuinely supports but that isn't in the controlled vocabulary is still *related* — don't drop it at the relevance stage. Carry it into the resolution ladder below, which decides between an observatory-level association and a documented omission. "Related but unresolvable" is never a licence to invent a value.

**How to fill it:** Begin typing the instrument name. Matches from HSSI's controlled instrument/observatory vocabulary appear in the dropdown; choose the correct one. The live form's tooltip still tells submitters the matches come from "the IVOA" — that on-page text is stale: the vocabulary is actually sourced from the heliophysics.net API and resolved to SPASE identifiers (the IVOA-based list is retired). If no entry matches, type the full name. **(That last sentence describes what the web form lets a *human* submitter do. Agents must never free-type a value — see Agent guidance below.)**

**Agent guidance — the SPASE resolution ladder.** This is the canonical procedure for **both** Field 31 and Field 32; everything else in this repo refers back to it.

Resolve against the controlled list at `/api/models/InstrumentObservatory/rows/all/` (fetch the ~7,700-row list once to a file with `?columns=id,name,identifier,type,abbreviation` and filter locally — keep `id` or the API returns an empty `data[]`; don't load every row into context). Match by `type` (1 = instrument → Field 31, 2 = observatory → Field 32), comparing against the row `name`, its `abbreviation`, source parenthetical aliases, and the SPASE identifier path segments (repos often mention only an acronym like `MFI`/`AIA`, and the path carries platform evidence, e.g. `.../GOES/17/SUVI`). Treat `.html` and bare identifiers as the same resource (prefer the bare one). Prefer `SMWG/...` only as a tie-breaker among same-name duplicates — a single non-SMWG match is still correct (Solar Orbiter is `ESA/Observatory/SolarOrbiter`). **Copy the matched row's `name` verbatim.**

**Vocabulary state (verify, don't assume).** As of the PR #54 backfill (2026-07-07) the vocabulary is 100% SPASE-backed — 7,648 rows, 0 non-SPASE — re-verified 2026-07-27. Treat that as a **dated observation, not an invariant**. Keep `identifier.startswith("https://spase-metadata.org/")` as a **real guard**: any row failing it means either upstream drift or a row an agent wrongly created, and must be **reported, never used**.

Then apply the ladder in order and stop at the first rule that fires:

1. **Exactly one row matches** → emit that row's `name` (verbatim) + its `identifier`. Done.
2. **Several rows match and specific in-repo evidence names which ones** → emit **all** the evidenced rows, and cite the evidence in the source note. Evidence means a concrete artifact — a supported-version list (`VALID_SPACECRAFT = [16, 17, 18, 19]` → the four GOES SUVI rows), a station table (THEMIS ASI → its 24 `SMWG/Instrument/THEMIS/Ground/*/ASI` rows), an explicit doc/API statement (DMSP SSJ → the F16/F17/F18 rows; SECCHI → STEREO-A and STEREO-B). A plausible guess is not evidence.
3. **Several rows match and nothing in the repo selects among them** → record `NEEDS MANUAL RESOLUTION (ambiguous instrument/observatory)` listing the candidate identifiers. Non-submittable; the user picks.
4. **No row for the instrument, but its platform/mission has one** → associate the **observatory** row instead and note the substitution. (SPASE/HDRL guidance, 2026-07-01: a missing instrument record should not block the software's association; prefer the observatory/platform record. PR #54 precedent: MGS Radio Science Subsystem → `SMWG/Observatory/MGS`; GOES-13 Imager → `SMWG/Observatory/GOES/13`; GOES-16 ABI → `SMWG/Observatory/GOES/16`.)
5. **Nothing defensible resolves** — a generic class label (`Ionosonde`, `Digital All Sky Cameras`), or something outside heliophysics scope (`NEXRAD`) → **omit the entry and document why.** A documented omission is a correct outcome, not a failure.
6. **Never emit a `name` without an `identifier`.** There is no free-type path for agents. The backend's no-identifier fallback is a case-sensitive `filter(name=…, type=…).first()` that either binds to an arbitrary same-name row or **creates a new identifierless row** (`serializers/submission.py`) — reintroducing exactly the legacy rows PR #54 deleted (63 → 0). If an entry does not resolve, it is omitted (5) or flagged (3) — never invented. A genuinely new instrument enters the vocabulary through the heliophysics.net refresh, not through a submission.

See the `submission-payload` / `update-payload` skills for the payload-level restatement.

**Sub-fields:**
- **Instrument Name** (OPTIONAL): Name of the instrument — the matched controlled-list row's `name`, copied verbatim
- **Instrument Identifier** (OPTIONAL): Globally unique persistent identifier — for controlled-list resolution this is the SPASE Resource ID URL from the list (e.g. `https://spase-metadata.org/SMWG/Instrument/...`). Optional on the form, but **for agents it is mandatory in practice**: an entry without one is not submittable (ladder rule 6). A human may supply a DOI as a manual exception, but **agents must not substitute a DOI to satisfy controlled-list resolution** — resolve to SPASE, or omit per rule 5. (A genuine repo-provided instrument DOI may be recorded in the source note as out-of-vocab context, but it never becomes the identifier.) Enables improved linking and reliable matching.

## Why it exists

<!-- phase2 -->

## How it appears on the site

<!-- phase2 -->

## Rubric: include / exclude

<!-- moved from .claude/agents/hssi-metadata-extractor.md:298-321 -->
**Related Instruments / Observatories (Fields 31 & 32) — decide relevance first, then resolve.** When the repo references an instrument, mission, or observatory, work in two stages: (A) decide whether it's actually "related" enough to list, then (B) for the ones that pass, resolve them against the SPASE vocab instead of free-typing.

**(A) Relevance gate — "designed to support."** List an instrument/observatory only if the software is *designed to support* it — i.e. it directly reads/writes/parses/calibrates/processes that specific instrument's or observatory's data, implements a format/convention specific to it (as a means of supporting it), is purpose-built or an instrument/mission-team tool for it, or models/visualizes its measurements as a primary function. Two sanity checks: would a user searching HSSI for `instrument:"X"` / `observatory:"X"` expect this software back, and would someone working with X's data actually reach for it? If both are clearly "no," **don't list it.** Specifically **exclude** (and record a brief `Note:` for anything you considered and dropped, so there's an audit trail):
- instrument/observatory-**agnostic** tools (general models, utilities, frameworks) — they support none specifically;
- **tutorial / demo / example** mentions and "platforms you *could* write a module for";
- "**configurable for**" or "**optimized for / commonly used with**" a specific instrument while the software is otherwise agnostic;
- links that **belong to another field** — a *generic* multi-instrument format (FITS/CDF/netCDF) → Input/Output File Formats, a *generic/multi-mission* data source/archive (e.g. CDAWeb) → Data Sources, a *phenomenon* → Related Phenomena. **But** an instrument/mission-**specific** format, parser, archive, or API *does* count as designed-to-support — list it under 31/32 (and for an observatory-specific data source, also select `observatory-specific` in Data Sources per Field 17);
- instruments belonging to a separate **ecosystem/plugin package** → that package's record, not the umbrella framework's.

Do **not** confuse "not related" with "related but hard to resolve": a genuinely-supported instrument that is ambiguous or missing from the vocab is still related — carry it into stage (B), which decides between an observatory-level association, a flag, or a documented omission. Never drop it as *irrelevant*, and never resolve it by inventing a value. Prefer the specific instrument (Field 31) when the software targets an instrument and the mission/observatory (Field 32) when it targets the platform; list both only when both are genuinely supported, and don't expand a single example into many sub-instruments.

**(B) Resolve each instrument/observatory that passes the gate** against HSSI's controlled vocabulary at `/api/models/InstrumentObservatory/rows/all/`. Use the submission target's base URL if one has been given; **in extract-only mode (no target), resolve against production `https://hssi.hsdcloud.org`** — SPASE identifiers are global, so the choice of HSSI instance doesn't change the result.

1. **Fetch once to a file; filter locally.** The endpoint returns the entire vocabulary (~7,700 rows) in `data[]` — save it (e.g. with `curl`) and filter with `grep`/`jq`/`python` rather than loading every row into context (`?columns=id,name,identifier,type,abbreviation` drops the large `definition` field — keep `id`, or the API returns an empty `data[]`).
2. **Vocabulary state — verify, don't assume.** As of the PR #54 backfill (2026-07-07) the vocabulary is 100% SPASE-backed (7,648 rows, 0 non-SPASE; re-verified 2026-07-27). That is a **dated observation, not an invariant**. Keep `identifier.startswith("https://spase-metadata.org/")` as a **real guard** — a row failing it means upstream drift or a row an agent wrongly created, and must be **reported, never used**.
3. **Normalize `.html`** — ~40+ identifiers exist in both bare and `.html` forms (e.g. `.../SDO/AIA` and `.../SDO/AIA.html`); treat them as one resource and prefer the non-`.html` row.
4. **Match on multiple signals**, restricted to the right `type` (1 = instrument → Field 31, 2 = observatory → Field 32): the row `name`, its `abbreviation`, the source's parenthetical aliases (repos often mention only `AIA`/`PSP`/`SUVI`), and the SPASE **identifier path segments** (platform/mission evidence, e.g. `.../GOES/17/SUVI`). Abbreviations are often non-unique, so they feed the collision check below.
5. **Prefer `SMWG/...` only as a tie-breaker** among same-name duplicates; a single non-SMWG match is still correct (Solar Orbiter is `ESA/Observatory/SolarOrbiter`). The canonical SMWG name is sometimes the long form (e.g. `SMWG/Observatory/THEMIS` is "Time History of Events and Macroscale Interactions during Substorms"). **Copy the matched row's `name` verbatim.**
6. **Exactly one row matches** → record both its canonical `name` (verbatim) and SPASE `identifier`. The identifier is the reliable de-duplication key on submission.
7. **Several rows match, and specific in-repo evidence names which ones** → record **all** the evidenced rows, and cite that evidence in the source note. Evidence means a concrete artifact: a supported-version list (`VALID_SPACECRAFT = [16, 17, 18, 19]` → the four GOES SUVI rows), a station table (THEMIS ASI → its 24 `SMWG/Instrument/THEMIS/Ground/*/ASI` rows), or an explicit doc/API statement (DMSP SSJ → F16/F17/F18; SECCHI → STEREO-A and STEREO-B). A plausible guess is not evidence — if you are inferring rather than reading, go to step 8.
8. **Several rows match and nothing in the repo selects among them** (e.g. `Solar Ultraviolet Imager` → four GOES rows with no version evidence), **or** no row matches exactly but a plausible same-type row exists (case-insensitive/trimmed, or a parenthetical-abbreviation variant like `ACE (Advanced Composition Explorer)` vs `ACE`) → do **not** record it as a normal Field 31/32 value. Record it under an explicit **`NEEDS MANUAL RESOLUTION (ambiguous instrument/observatory)`** note listing the candidate SPASE identifiers, so the validator/submitter treat it as **non-submittable**.
9. **No instrument row, but its platform/mission has one** → record the **observatory** row (Field 32) instead, and note the substitution. Per SPASE/HDRL guidance (2026-07-01), a missing instrument record must not block the association: MGS Radio Science Subsystem → `SMWG/Observatory/MGS`; GOES-13 Imager → `SMWG/Observatory/GOES/13`; GOES-16 ABI → `SMWG/Observatory/GOES/16`.
10. **Nothing defensible resolves** — a generic class label (`Ionosonde`, `Digital All Sky Cameras`) or something out of heliophysics scope (`NEXRAD`) → **omit the entry and record a `Note:` explaining why.** A documented omission is a correct outcome, not a failure.
11. **Never record a `name` with no identifier.** There is no free-type path. A bare name either binds to an arbitrary same-name row (`filter(name=…, type=…).first()`, case-sensitive over the whole table) or **creates a new identifierless row**, reintroducing exactly the legacy rows PR #54 deleted (63 → 0). If it doesn't resolve, it is omitted (10) or flagged (8) — never invented. Genuinely new instruments enter the vocabulary via the heliophysics.net refresh, not via a submission.

<!-- moved from .claude/agents/hssi-metadata-validator.md:201-251 -->
6. **Check for related instruments/observatories** not mentioned:
   - Search README and docs for instrument or mission names
   - **Apply the "designed to support" relevance bar to what's listed and what's missing.** An
     instrument/observatory belongs in Field 31/32 only if the software directly works with that
     specific instrument's/observatory's data or is purpose-built for it. Flag **over-inclusion** —
     entries that look like instrument/observatory-agnostic claims, tutorial/demo name-drops,
     "configurable for" / "optimized for" mentions, or links that really belong to another field (a
     *generic* file format → Input/Output Formats, a *generic/multi-mission* data source → Data Sources,
     a *phenomenon* → Related Phenomena — but an instrument/mission-**specific** format or data source
     legitimately stays, and an observatory-specific data source should be cross-listed here per
     Field 17) — and recommend removing or moving only the genuinely-misfiled ones. Flag
     **under-inclusion** — an instrument/observatory the software is genuinely designed to support but
     that is missing from 31/32. (A genuinely-supported instrument that is merely hard to resolve is
     still *related* — the valid outcomes are a resolved identifier, an observatory-level substitution,
     `NEEDS MANUAL RESOLUTION`, or an omission with a recorded reason. Never a bare name.)
   - For any instrument/mission found, check it resolves to HSSI's controlled vocabulary at
     `/api/models/InstrumentObservatory/rows/all/`. The endpoint returns the whole vocabulary
     (~7,700 rows) in `data[]` — fetch it once to a file and filter with `grep`/`jq`/`python` rather
     than loading every row into context (`?columns=id,name,identifier,type,abbreviation` drops the large
     `definition`; keep `id`, or the API returns an empty `data[]`). **Vocabulary state — verify, don't
     assume:** as of the PR #54 backfill (2026-07-07) it is 100% SPASE-backed (7,648 rows, 0 non-SPASE;
     re-verified 2026-07-27), but treat that as a **dated observation, not an invariant**. Keep
     `identifier.startswith("https://spase-metadata.org/")` as a **real guard** — a row failing it means
     upstream drift or a row an agent wrongly created; **report it, never endorse it**.
     **Normalize `.html`** — ~40+ identifiers
     exist in both bare and `.html` forms (e.g. `.../SDO/AIA` and `.../SDO/AIA.html`); treat them as one
     and prefer the non-`.html` row. Match on multiple signals restricted to the right `type`
     (1 = instrument, 2 = observatory): the row `name`, its `abbreviation`, source parenthetical
     aliases, and the SPASE **identifier path segments** (platform/mission evidence, e.g.
     `.../GOES/17/SUVI`). Prefer `SMWG/...` only as a tie-breaker among same-name duplicates (a single
     non-SMWG match like `ESA/Observatory/SolarOrbiter` is still correct). Recommend that row's
     canonical `name` (verbatim) and SPASE `identifier`. Validate against the **SPASE resolution ladder**
     in the `hssi-field-definitions` skill (Field 31) — it is the authoritative procedure. In particular:
     - **An entry with a `name` but no SPASE `identifier` is always an ERROR.** Never endorse one, under
       any circumstances — there is no "no plausible match, so free-typing is fine" exception. The
       backend turns such a value into either an arbitrary same-name binding or a **brand-new
       identifierless row**, reintroducing the legacy rows PR #54 deleted (63 → 0). The correct outcomes
       are a resolved identifier, an observatory-level substitution, `NEEDS MANUAL RESOLUTION`, or a
       documented omission.
     - **Several candidates with cited in-repo evidence** naming which ones (a supported-version list, a
       station table, an explicit doc/API statement) → a multi-row expansion is **correct**; verify the
       evidence actually appears in the repo, then PASS it. Without such evidence (e.g. `Solar Ultraviolet
       Imager` → GOES-16/17/18/19 with nothing selecting among them), flag an **unresolved collision that
       must be manually resolved before submission**.
     - **A missing instrument whose platform/mission does resolve** → recommend the observatory-level
       association rather than an omission (SPASE/HDRL guidance, 2026-07-01).
     - **A documented omission is a valid, passing outcome** for a generic class label (`Ionosonde`,
       `Digital All Sky Cameras`) or an out-of-heliophysics-scope entry (`NEXRAD`) — do not flag it as
       under-inclusion when the reason is recorded.
     Treat any extractor entry already marked `NEEDS MANUAL RESOLUTION` as unresolved (don't silently
     "fix" it into a submittable value). Also flag embedded-abbreviation names (e.g. `Parker Solar Probe (PSP)`).

<!-- moved from .claude/agents/hssi-metadata-updater.md:180-180 -->
**Relevance gate (Fields 31 & 32):** when this extraction produces Related Instruments/Observatories, apply the **same "designed to support" relevance gate as the `hssi-metadata-extractor`** (stage A of its Fields 31/32 rule) — only enrich in an instrument/observatory the software is genuinely designed to support, not tutorial/agnostic/format-only mentions. Relevance (whether to list) precedes resolution (which SPASE row).

## Ask the user only when

<!-- phase2 -->

## Where to find it, and traps

<!-- phase2 -->

## Payload and roundtrip notes

<!-- moved from .claude/skills/submission-payload/SKILL.md:128-183 -->
**First apply the relevance gate, then resolve.** Only list instruments/observatories the software is *designed to support* (see Fields 31/32 "When to include it" in the field definitions / extractor relevance gate); the steps below resolve the entries that have already passed it.

**How to resolve against the controlled list** (`/api/models/InstrumentObservatory/rows/all/`):

1. **Fetch once to a file; filter locally.** The endpoint returns the entire vocabulary (~7,700 rows)
   in `data[]` — do **not** load it all into context. Save the response to a file (e.g. `curl`/Bash)
   and filter it with `grep`/`jq`/`python`. You can request
   `?columns=id,name,identifier,type,abbreviation` to drop the large `definition` field (keep `id` —
   the API returns an empty `data[]` if it's omitted).
2. **Vocabulary state — verify, don't assume.** As of the PR #54 backfill (2026-07-07) the vocabulary
   is 100% SPASE-backed (7,648 rows, 0 non-SPASE; re-verified 2026-07-27). Treat that as a **dated
   observation, not an invariant.** Keep `identifier.startswith("https://spase-metadata.org/")` as a
   **real guard**: a row failing it signals upstream drift or a row an agent wrongly created, and must
   be **reported, never used**.
3. **Normalize `.html` identifiers.** ~40+ SPASE identifiers exist in both a bare and a `.html` form
   (e.g. `.../SMWG/Instrument/SDO/AIA` and `.../SMWG/Instrument/SDO/AIA.html`). Treat them as the same
   resource and **prefer the non-`.html` identifier** when both are present, so you don't split links
   across two rows for one instrument.
4. **Match on multiple signals**, not just the canonical name. Repos often mention only an acronym or
   platform (`AIA`, `SDO`, `PSP`, `SUVI`). Compare your candidate against each row's `name`, its
   `abbreviation`, the source's parenthetical aliases, and the **SPASE identifier path segments**
   (which carry platform/mission evidence, e.g. `.../GOES/17/SUVI`). Restrict to the right `type`
   (1 = instrument, 2 = observatory). Abbreviations are themselves often non-unique (e.g. `ELECTRON`
   appears on both SMWG and CNES rows), so treat them as candidate signals that feed the collision
   rule below — not as unique keys.
5. **Prefer the `SMWG/...` namespace as a tie-breaker** among same-name duplicates (the authoritative
   registry) over project archives like `CNES/...`. This is *only* a tie-breaker: a single non-SMWG
   match is still correct (e.g. Solar Orbiter's canonical row is `ESA/Observatory/SolarOrbiter`).
   The canonical SMWG `name` is sometimes the long form (e.g. `SMWG/Observatory/THEMIS` is named
   "Time History of Events and Macroscale Interactions during Substorms", not "THEMIS"). **Copy the
   matched row's `name` verbatim** — don't re-derive it.
6. **On an unresolved collision, omit the entry entirely.** If more than one SPASE candidate still
   remains after namespace and platform/mission evidence (e.g. `Solar Ultraviolet Imager` matches four
   instrument rows, one each for GOES-16/17/18/19), **do not include the instrument/observatory in the
   payload at all** — leave it out and flag it for user/manual review. Do **not** fall back to emitting
   the bare `name`: the backend's no-identifier path is a case-sensitive `filter(name=…, type=…).first()`
   (see Backend Quirks), so a bare name that matches several identically-named rows silently binds to an
   **arbitrary** one — the same mis-link a wrong identifier would cause. Omission is the only safe
   option, and the orchestrator's approval gate must treat a collision flag as a **hard blocker**.
7. Otherwise emit the chosen row's `name` + SPASE `identifier`, following the **SPASE resolution ladder**
   in the `hssi-field-definitions` skill (Field 31), which is authoritative. At payload level it reduces to:
   - **Several rows match with cited in-repo evidence** naming which ones (a supported-version list, a
     station table, an explicit doc/API statement) → emit **all** the evidenced rows, each with its
     identifier. This is a legitimate one-to-many expansion, not a collision.
   - **Several rows match with nothing selecting among them** → **omit the entry and flag it for manual
     review.**
   - **No instrument row but the platform/mission has one** → emit the **observatory** row instead and
     note the substitution.
   - **Nothing defensible resolves** (generic class label, out of heliophysics scope) → **omit and
     document why.**
   - **Never emit a `name` with no `identifier`.** There is no free-type path and no "zero plausible
     matches" exception. The backend's no-identifier fallback is a case-sensitive
     `filter(name=…, type=…).first()` over the **whole table**: it either binds to an arbitrary
     same-name row or falls through to `InstrumentObservatory.objects.create(name=…, type=…)`, creating
     a **new identifierless row** — exactly the legacy rows PR #54 deleted (63 → 0).
   Always surface omitted entries to the user.

<!-- moved from .claude/skills/update-payload/SKILL.md:339-378 -->
**Instruments / Observatories matching:** First apply the **relevance gate** — only list instruments/observatories the software is *designed to support* (see Fields 31/32 "When to include it"); the resolution below is for entries that have already passed it. Resolve those names against
`/api/models/InstrumentObservatory/rows/all/`. The endpoint returns the whole vocabulary (~7,700 rows)
in `data[]` — **fetch it once to a file and filter locally** (`grep`/`jq`/`python`); don't load every
row into context (`?columns=id,name,identifier,type,abbreviation` drops the large `definition` field;
keep `id`, or the API returns an empty `data[]`).
Then:

- **Vocabulary state — verify, don't assume.** As of the PR #54 backfill (2026-07-07) the vocabulary is
  100% SPASE-backed (7,648 rows, 0 non-SPASE; re-verified 2026-07-27) — a **dated observation, not an
  invariant**. Keep `identifier.startswith("https://spase-metadata.org/")` as a **real guard**: a row
  failing it signals upstream drift or a row an agent wrongly created, and must be **reported, never used**.
- **Normalize `.html`** — ~40+ identifiers exist in both bare and `.html` forms (e.g.
  `.../SDO/AIA` and `.../SDO/AIA.html`); treat them as one resource and prefer the non-`.html` row.
- **Match on multiple signals** — the row `name`, its `abbreviation`, source parenthetical aliases,
  and the SPASE **identifier path segments** (platform/mission evidence, e.g. `.../GOES/17/SUVI`),
  restricted to the right `type` (1 = instrument, 2 = observatory). Abbreviations are often non-unique,
  so they feed the collision rule rather than resolve uniquely.
- **Prefer `SMWG/...` only as a tie-breaker** among same-name duplicates (over `CNES/...` archives); a
  single non-SMWG match is still correct (Solar Orbiter is `ESA/Observatory/SolarOrbiter`). The
  canonical SMWG name is sometimes the long form (e.g. `SMWG/Observatory/THEMIS` is
  "Time History of Events and Macroscale Interactions during Substorms"). Copy the matched row's `name`
  verbatim.
- **On an unresolved collision, omit the entry entirely** — if more than one SPASE candidate remains
  after namespace/platform evidence (e.g. `Solar Ultraviolet Imager` matches four GOES-16/17/18/19
  rows), **drop the instrument/observatory from the payload** and flag for user/manual review. Do
  **not** send a bare `name`: the no-identifier path is a case-sensitive `filter(name=…, type=…).first()`,
  so a bare name matching several identically-named rows binds to an arbitrary one — the same silent
  mis-link a wrong identifier causes. A collision flag is a hard blocker for the approval gate.
- Otherwise send the chosen row's `name` plus its SPASE `identifier`, following the **SPASE resolution
  ladder** in the `hssi-field-definitions` skill (Field 31), which is authoritative. At payload level:
  several rows with cited in-repo evidence → send **all** the evidenced rows (a legitimate one-to-many
  expansion, not a collision); several rows with nothing selecting among them → **omit and flag**; no
  instrument row but a resolvable platform/mission → send the **observatory** row instead and note the
  substitution; nothing defensible → **omit and document why**. **Never send a `name` with no
  `identifier`** — there is no free-type path and no "zero plausible matches" exception. The
  no-identifier fallback `filter(name=…, type=…).first()` runs case-sensitively over the **whole table**
  and, failing that, *creates a new identifierless row* — exactly the legacy rows PR #54 deleted
  (63 → 0). Backend matching is `identifier` first, then the case-sensitive `name`+`type` match, so the
  identifier is the reliable key. Never send `landing_url` (server-derived — a HelioData mission page when one is
  confirmed, otherwise empty so the link falls back to the SPASE `identifier`).

<!-- moved from .claude/agents/hssi-metadata-submitter.md:96-96 -->
- Strip any source annotations or prose notes from values — extract only the actual data. **Exception:** a `relatedInstruments`/`relatedObservatories` entry that is marked `NEEDS MANUAL RESOLUTION` **or that carries no SPASE `identifier`** is **non-submittable** — do **not** strip the marker and submit the bare name. Omit that entry from the payload and carry it into the verification report (see Step 3E).

<!-- moved from .claude/agents/hssi-metadata-submitter.md:115-115 -->
**E. Instrument/Observatory SPASE gate** — Every `relatedInstruments`/`relatedObservatories` entry in the payload **must carry a `https://spase-metadata.org/` identifier.** An entry must have been **omitted** from the payload if it: was marked `NEEDS MANUAL RESOLUTION` by the extractor; was flagged by the validator / `submission-payload` resolution as an **unresolved match** (a name matching several controlled-list rows with no evidence selecting among them, e.g. the four `Solar Ultraviolet Imager` GOES-16/17/18/19 rows); **or carries a `name` with no identifier at all**. A bare name is never sent — the backend would bind it to an arbitrary same-name row or create a new identifierless row (see `submission-payload`). A *multi-row expansion* backed by cited in-repo evidence (a supported-version list, a station table) is legitimate and not a collision — verify each row has an identifier and let it through. Surface every omission in the report. This is a **hard blocker for EXECUTE:** PREPARE may produce the report, but do **not** POST while any unresolved or identifierless instrument/observatory entry remains — the user must pick the right SPASE identifier (or confirm dropping the entry) first.

<!-- moved from .claude/agents/hssi-metadata-updater.md:254-254 -->
5. **Instrument/Observatory SPASE gate.** Every `relatedInstruments`/`relatedObservatories` value you send **must carry a `https://spase-metadata.org/` identifier.** **Omit that entry** from the payload (and flag it in the diff report as requiring manual resolution) if resolving it hits an **unresolved match** — a name matching several controlled-list rows with no in-repo evidence selecting among them (e.g. the four `Solar Ultraviolet Imager` GOES-16/17/18/19 rows) — **or if it has a `name` but no identifier at all.** Never send a bare name (see `update-payload`): there is no "zero plausible matches, so it's safe" exception, because that path creates a new identifierless row. A *multi-row expansion* backed by cited in-repo evidence is legitimate and not a collision — pass it through once each row has an identifier. If an upstream extractor pass already marked an entry `NEEDS MANUAL RESOLUTION` (enrich mode reuses extraction), treat that marker as the same hard blocker — do not re-resolve it into a submittable value. This is a **hard blocker for EXECUTE:** PREPARE may report it, but do not PATCH while any unresolved or identifierless instrument/observatory entry remains.

## Worked examples

<!-- phase2 -->

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 704-735 on 2026-09-22.
