# Field 31 — Related Instruments

**Level:** OPTIONAL · **API:** `relatedInstruments[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/InstrumentObservatory/rows/all/` — (type 1)
**Filter tab:** none · **Free-text search tier:** T4.2 (name, abbreviation) · **Field-search code:** `instrument`

## What it is

**Type:** Multi-entry nested group

**What it is:** The instrument the software is designed to support.

**When to include it (relevance):** List an instrument only if the software is *designed to support* it — it directly reads/writes/parses/calibrates/processes that specific instrument's data, implements a data format/convention specific to it (as a means of supporting it), is purpose-built or an instrument-team tool for it, or models/visualizes its measurements as a primary function. Sanity check: would a user searching HSSI for `instrument:"X"`, or someone working with X's data, expect this software back? If not, leave it out. **Exclude** instrument-agnostic tools (general models/utilities/frameworks support none specifically), tutorial/demo/example name-drops, "configurable for" / "commonly used with" / "optimized for" mentions of an otherwise-agnostic tool, and links that belong to another field — **generic** support for a multi-instrument *file format* (FITS/CDF/netCDF) → Input/Output File Formats, or a **generic/multi-mission** *data archive/source* (e.g. CDAWeb broadly) → Data Sources. **But** an instrument-**specific** parser, format, convention, or data source/API *does* count as designed-to-support — list that instrument here. Note: an instrument the software genuinely supports but that isn't in the controlled vocabulary is still *related* — don't drop it at the relevance stage. Carry it into the resolution ladder below, which decides between an observatory-level association and a documented omission. "Related but unresolvable" is never a licence to invent a value.

**How to fill it:** Begin typing the instrument name. Matches from HSSI's controlled instrument/observatory vocabulary appear in the dropdown; choose the correct one. The live form's tooltip still tells submitters the matches come from "the IVOA" — that on-page text is stale: the vocabulary is actually sourced from the heliophysics.net API and resolved to SPASE identifiers (the IVOA-based list is retired). If no entry matches, type the full name. **(That last sentence describes what the web form lets a *human* submitter do. Agents must never free-type a value — see the Rubric, rule 22.)**

**Sub-fields:**
- **Instrument Name** (OPTIONAL): Name of the instrument — the matched controlled-list row's `name`, copied verbatim
- **Instrument Identifier** (OPTIONAL): Globally unique persistent identifier — for controlled-list resolution this is the SPASE Resource ID URL from the list (e.g. `https://spase-metadata.org/SMWG/Instrument/...`). Optional on the form, but **for agents it is mandatory in practice**: an entry without one is not submittable (rule 22). A human may supply a DOI as a manual exception, but **agents must not substitute a DOI to satisfy controlled-list resolution** — resolve to SPASE, or omit per rule 21. (A genuine repo-provided instrument DOI may be recorded in the source note as out-of-vocab context, but it never becomes the identifier.) Enables improved linking and reliable matching.

This file holds the **single canonical copy** of the relevance gate and the SPASE resolution ladder for
**both** Field 31 and Field 32; Field 32 applies it with `type` 2 and states only what differs. Every
other file in this repo refers back to it.

## Why it exists

A scientist working with one instrument's data wants the software that reads, calibrates or analyses
exactly that instrument — the association answers "what can I use on these files?" A correct entry
puts the software in front of that user through an `instrument:` search and ties the record to a
resolvable SPASE resource. A wrong entry does real harm in both directions: an instrument-agnostic tool
listed against one facility implies a specialisation it does not have (and is then absent from every
other facility it serves equally), and a bare or mismatched name can bind the record to the wrong row or
mint a new identifierless row in the shared vocabulary.

## How it appears on the site

- **Detail page:** in the "Science Context" section (shown when any of instruments, observatories,
  phenomena or regions is set), under "Related Instruments", one tag per row. The tag links to the row's
  `landing_url` if set, otherwise its SPASE `identifier`; for instruments the vocabulary refresh leaves
  `landing_url` empty, so the link goes to the SPASE page (tooltip "View this instrument on SPASE"). The
  tag text is the row's `name` (the raw URL when the name is `UNKNOWN`); a row with no URL renders as a
  plain tag with its name. The abbreviation is not shown on the detail page.
- **Filter:** none.
- **Free-text search:** tier T4.2, matching the row's `name` and `abbreviation`.
- **Field search:** `instrument:"…"` matches `related_instruments__name__icontains` or
  `related_instruments__abbreviation__icontains`; the value must be quoted.
- **`/api/view/` (plain JSON):** renders the row as `name (abbreviation)` when an abbreviation is set.
- **JSON-LD:** each row is emitted under `mentions` with `description` `relatedInstruments`, `@type`
  `IndividualProduct` / `prov:Entity` / `sosa:System`, `name` = the row name, and `@id` and `url` = the
  identifier.

## Rubric: include / exclude

Work in stages. **Stage A** decides whether a candidate is related enough to list; **Stage B** is the
procedure for resolving each candidate that passes; **Stage C** picks the outcome. In Stages A and C,
apply the rules top to bottom and stop at the first rule that fires. Record a short `Note:` for every
candidate considered and dropped, so there is an audit trail.

**Stage A — relevance: "designed to support"**

1. **A link that belongs to another field — exclude here.** A *generic* multi-instrument file format
   (FITS/CDF/netCDF) → Input/Output File Formats (Fields 18/19); a *generic/multi-mission* data archive or
   source (e.g. CDAWeb broadly) → Data Sources (Field 17); a *phenomenon* → Related Phenomena (Field 22).
   Does **not** fire on an instrument/mission-**specific** format, parser, archive or API — that is
   designed-to-support; go on to rule 6.

2. **An instrument-agnostic tool — exclude.** General models, utilities and frameworks support no
   instrument specifically. So does an archive-wide client whose facility is chosen by the user at run
   time: listing the one facility named in its examples would imply a specialisation it lacks and leave
   it absent from every other facility it serves equally.

3. **A mention that is not support — exclude.** Tutorial, demo and example name-drops; docstring example
   values; a gallery page or smoke test that calls one instrument's routine to prove a generic path
   works; "platforms you *could* write a module for"; a test fixture left behind after support was
   removed; planned future work. Support must exist in the software at the pinned revision.

4. **"Configurable for", "optimized for" or "commonly used with" an otherwise-agnostic tool — exclude.**
   This includes an implementation convenience in vendored code that happens to hold for one
   instrument's products (a comment that a projection's grid spacing matches that instrument's remapped
   data), and a technique that is usually applied to one instrument's data.

5. **An instrument served through a separate ecosystem or plugin package** belongs to that package's
   record, not the umbrella framework's — exclude here.

6. **Designed to support — include.** The software directly reads/writes/parses/calibrates/processes
   that specific instrument's data, implements a format/convention specific to it (as a means of
   supporting it), is purpose-built or an instrument-team tool for it, or models/visualizes its
   measurements as a primary function. Evidence is concrete: a dedicated reader or loader, a calibration
   or response routine, a code branch written for that instrument, an instrument-specific archive API
   call. Two sanity checks: would a user searching HSSI for `instrument:"X"` expect this software back,
   and would someone working with X's data actually reach for it? If both are clearly "no", **don't list
   it** — decide from the searcher's side.

7. **Choose the level the evidence supports.** Prefer the specific instrument (Field 31) when the
   software targets an instrument and the mission/observatory (Field 32) when it targets the platform;
   list both only when both are genuinely supported, and don't expand a single example into many
   sub-instruments. When the software's relation is to a mission's observational record rather than to
   any instrument's data products — shipped models fitted entirely to one mission's observations, with no
   reader for its data — record the observatory rows the evidence names in Field 32 and leave this field
   empty. A numeric admissibility range (a satellite-number gate of 1–19) does not by itself justify one
   row per number; record a row where the tree shows support for that specific unit (named in the docs,
   a special-case branch, a per-unit table index or supported list) and the vocabulary has the row.

8. **Related but hard to resolve is still related.** A genuinely supported instrument that is ambiguous
   or missing from the vocabulary passes Stage A; carry it into Stages B and C, which decide between a
   resolved row, an observatory-level substitution, a flag, or a documented omission. Never drop it as
   *irrelevant*, and never resolve it by inventing a value.

**Stage B — resolution procedure (for every candidate that passed Stage A)**

9. **Resolve against the controlled vocabulary** at `/api/models/InstrumentObservatory/rows/all/`, on the
   submission target's base URL if one has been given; **in extract-only mode (no target), resolve
   against production `https://hssi.hsdcloud.org`** — SPASE identifiers are global, so the choice of HSSI
   instance doesn't change the result.

10. **Fetch once to a file; filter locally.** The endpoint returns the entire vocabulary (about 7,600
    rows) as `{"data": [...], "total": N}`. Save it (e.g. with `curl`) and filter with
    `grep`/`jq`/`python` rather than loading every row into context. `?columns=id,name,identifier,type,abbreviation`
    drops the large `definition` field — **keep `id`, or the API returns an empty `data[]`**. A sweep
    meant to establish that something is *absent*, or to match by concept, must include `definition`:
    omitting it changes the counts materially.

11. **Vocabulary state — verify, don't assume.** The vocabulary has been observed to be 100%
    SPASE-backed after a backfill that removed every legacy non-SPASE row (measured 2026-09-22:
    `http://localhost` 7,602 rows, 0 non-SPASE; `https://hssi.hsdcloud.org` 7,602 rows, 0 non-SPASE). That is a
    **dated observation, not an invariant** — `update-api-spec` Step A re-measures and re-dates it. Keep `identifier.startswith("https://spase-metadata.org/")` as a **real guard**
    on every fetch: a row failing it means upstream drift or a row an agent wrongly created, and must be
    **reported, never used**.

12. **Normalize `.html`.** An identifier can exist in both bare and `.html` forms (e.g.
    `.../SMWG/Instrument/SDO/AIA` and `.../SMWG/Instrument/SDO/AIA.html`); treat them as one resource and
    **prefer the non-`.html` row**, so links for one instrument are not split across two rows. The
    vocabulary refresh writes only bare identifiers; `.html` rows come from submissions that pasted a
    browser URL, so they can appear on any instance even after a cleanup, and they typically carry the
    abbreviation inside the name (`Atmospheric Imaging Assembly (AIA)`, empty `abbreviation`) where the
    bare row has `Atmospheric Imaging Assembly` + `AIA`. Check for them on every fetch rather than
    assuming either state.

13. **Match on multiple signals**, restricted to the right `type` (1 = instrument → Field 31, 2 =
    observatory → Field 32): the row `name`, its `abbreviation`, the source's parenthetical aliases
    (repos often mention only `MFI`/`AIA`/`SUVI`), the SPASE **identifier path segments** (which carry
    platform/mission evidence, e.g. `.../GOES/17/SUVI`), and the row `definition`. Search **by concept
    and by naming-authority prefix**, not only by the recorded name: authority paths and spellings vary
    (`SolarOrbiter` / `Solar_Orbiter` / `SolO`; SMWG vs CNES; the same GOES solar X-ray instrument is
    `XRS` on some satellites and `SXM` on others), so match on the prefix and inspect rather than
    enumerating spellings in advance, and run the name side ("Solar X-ray") as well. Count a family by
    identifier namespace (`/SMWG/Instrument/THEMIS/Ground/…/ASI`), not by a name substring — names within
    a family are not uniform. Abbreviations are often non-unique (e.g. `ELECTRON` appears on both SMWG and
    CNES rows), so treat them as candidate signals that feed the collision check, not as unique keys.
    Read the definition before accepting a place-name match: rows sharing a place name can be different
    facilities (a university geomagnetic observatory and a radar at the same site).

14. **A collision is one entity with several candidate rows** — not several distinct entities that share
    a display name. Three `LP` rows for three Swarm spacecraft, or four `Solar Ultraviolet Imager` rows
    for four GOES satellites, are distinct instruments; each is fine when sent with its own identifier.
    The test is "does this entity resolve to exactly one row once platform and namespace evidence is
    applied?" — never "is this row's display name unique?" A candidate instrument row whose SPASE
    `ObservatoryID` points at an observatory row already selected is that observatory's child, which can
    decide between competing namespaces.

15. **Prefer `SMWG/...` only as a tie-breaker** among same-name duplicates of one entity (the
    authoritative registry over project-archive twins such as `CNES/…/CDPP-AMDA/…`). This is *only* a
    tie-breaker: a single non-SMWG match is still correct (Solar Orbiter is `ESA/Observatory/SolarOrbiter`;
    the GOES-16–19 SUVI rows are under `NOAA/`). Choose by identifier and state the reason in the source
    note. Never switch to another authority's row because its name reads more familiarly.

16. **Copy the matched row's `name` byte for byte** — never re-derive it. Row names can carry double
    spaces, newlines or edge spaces (`Solar X-ray Monitor on GOES  8` has two spaces), can be the long
    form (`SMWG/Observatory/THEMIS` is "Time History of Events and Macroscale Interactions during
    Substorms", not "THEMIS"), and can differ from the prose on their own SPASE page. Quote the row, and
    say it is the row being quoted.

**Stage C — outcome (stop at the first rule that fires)**

17. **Exactly one row matches** → record that row's `name` (verbatim) and its SPASE `identifier`. The
    identifier is the reliable de-duplication key on submission. Done.

18. **Several rows match, and specific in-repo evidence names which ones** → record **all** the evidenced
    rows, and cite that evidence in the source note. Evidence means a concrete artifact: a supported-version
    list (`VALID_SPACECRAFT = [16, 17, 18, 19]` → the four GOES SUVI rows), a station table (THEMIS ASI →
    its 24 `SMWG/Instrument/THEMIS/Ground/*/ASI` rows), or an explicit doc/API statement (DMSP SSJ →
    F16/F17/F18; SECCHI → STEREO-A and STEREO-B). This is a legitimate one-to-many expansion, not a
    collision. A plausible guess is not evidence — if you are inferring rather than reading, go to rule 19.

19. **Several rows match and nothing in the repo selects among them** (e.g. `Solar Ultraviolet Imager` →
    four GOES rows with no version evidence), **or** no row matches on any signal exactly but a plausible
    same-type row exists (only case-insensitive/trimmed, or a parenthetical-abbreviation variant like
    `ACE (Advanced Composition Explorer)` vs `ACE`) → do **not** record it as a normal value. Record it
    under an explicit **`NEEDS MANUAL RESOLUTION (ambiguous instrument/observatory)`** note listing the
    candidate SPASE identifiers. The entry is **non-submittable**: the submitter and updater omit it from
    the payload and report it, and it is a **hard blocker for EXECUTE** until the user picks the row(s),
    accepts an observatory-level substitution, or drops it. Never silently "fix" a marked entry into a
    submittable value.

20. **No row for the instrument, but its platform/mission has one** → record the **observatory** row
    (Field 32) instead, and note the substitution. Per SPASE/HDRL guidance, a missing instrument record
    must not block the software's association: MGS Radio Science Subsystem → `SMWG/Observatory/MGS`;
    GOES-13 Imager → `SMWG/Observatory/GOES/13`; GOES-16 ABI → `SMWG/Observatory/GOES/16`.

21. **Nothing defensible resolves** — a generic class label (`Ionosonde`, `Digital All Sky Cameras`), or
    something outside heliophysics scope (`NEXRAD`) → **omit the entry and record a `Note:` explaining
    why.** A documented omission is a correct outcome, not a failure.

22. **Never record a `name` without an `identifier`, and never an identifier the vocabulary does not
    hold.** There is no free-type path for agents and no "zero plausible matches, so it's safe"
    exception. The backend (`_get_or_create_observatory` in `serializers/submission.py`) matches on the
    exact `identifier` first; with no identifier it falls back to a case-sensitive
    `filter(name=…, type=…).first()` over the **whole table**, which either binds to an arbitrary
    same-name row — the same silent mis-link a wrong identifier causes — or **creates a new identifierless
    row**, reintroducing exactly the legacy rows the backfill deleted. An identifier that matches no row
    (one completed from a sibling's pattern, or a pasted `.html` form with no row) creates a **new row**
    with whatever name was sent. So copy identifiers from the fetched vocabulary, never compose them
    (`https://spase-metadata.org/SMWG/Observatory/AE-B` does not exist). If an entry does not resolve, it
    is omitted (rule 21) or flagged (rule 19) — never invented. A genuinely new instrument enters the
    vocabulary through the heliophysics.net refresh, not through a submission.

**Incumbents, validation and empty values**

23. **Stored rows get the same gate on a refresh.** Keep a stored row only with an argument under Stage A;
    remove one that fails it. A stored row that names the right entity under the canonical authority is
    kept even when its name is unfamiliar (a mission's original full name) — record why it reads that
    way. A row whose stored name is an upstream defect (the `PROBA2/LYRA` row carries the expansion of
    SWAP, a different instrument) still binds correctly by identifier: record the defect, and never swap
    in a different row to fix a display name. Deliberate local name divergences from the upstream page
    are recorded as such and not "corrected" back. Both fields are enrich-only, so an enrichment run is
    how an unrelated row would reach a live entry: apply Stage A before Stage B, and never enrich in a
    tutorial, agnostic or format-only mention.

24. **Validation applies the same rules and adds these checks.** Flag **over-inclusion** (agnostic
    claims, tutorial/demo name-drops, "configurable for"/"optimized for" mentions, misfiled format,
    archive or phenomenon links — recommending removal or moving only the genuinely misfiled ones) and
    **under-inclusion** (an instrument the software is designed to support that is missing). **An entry
    with a `name` but no SPASE `identifier` is always an ERROR**, never endorsed under any circumstances.
    A multi-row expansion with cited evidence is **correct** once the evidence is verified in the repo; the
    same expansion without evidence is an unresolved collision that must be manually resolved before
    submission. A missing instrument whose platform resolves gets a recommendation for the observatory
    substitution rather than an omission. A documented omission (rule 21) passes and is not flagged as
    under-inclusion. An entry already marked `NEEDS MANUAL RESOLUTION` stays unresolved. Also flag
    embedded-abbreviation names (e.g. `Parker Solar Probe (PSP)`), usually the sign of an `.html`
    orphan row.

25. **Empty is legitimate when examined.** Record the vocabulary sweep behind an empty field — terms,
    the four columns searched (`name`, `abbreviation`, `identifier`, `definition`), and a positive and a
    negative control — so the blank reads as a relevance decision rather than a lookup failure. When a
    candidate row exists and is deliberately not used, name it and its identifier, so a later refresh
    sees the question was settled.

## Ask the user only when

- **An unresolved collision (rule 19).** The user picks the SPASE identifier(s), accepts an
  observatory-level substitution, or drops the entry. It is a hard blocker for EXECUTE until answered.
- **A shared vocabulary row itself needs correcting** (its `name` or `abbreviation`). The entry's own
  value is decided by the rubric; a database write to a shared row changes every entry that cites it and
  needs its own approval — it is never a patch value.

Every other case is decided by the rubric.

## Where to find it, and traps

**Sources, in priority order:**
1. Code at the pinned revision: reader/loader modules and functions named for instruments, calibration
   and response routines, per-instrument branches, supported-version lists, station tables.
2. README and docs statements of what data the software handles.
3. The reference publication's data description (which instrument's data the method was built on).
4. Tests — as evidence of a supported code path only, never a fixture on its own.
5. The controlled vocabulary (`/api/models/InstrumentObservatory/rows/all/`), and for which rows the
   upstream refresh maintains, `https://api.heliophysics.net/api/instruments/` and
   `.../observatories/`.

**Fetch and sweep:**

```bash
# Full rows (includes definition) — use for concept sweeps and absence claims
curl -s "https://hssi.hsdcloud.org/api/models/InstrumentObservatory/rows/all/" -o io_vocab.json
# Slim rows — keep id or data[] comes back empty
curl -s "https://hssi.hsdcloud.org/api/models/InstrumentObservatory/rows/all/?columns=id,name,identifier,type,abbreviation" -o io_vocab_slim.json
python3 - <<'PY2'
import json, re
rows = json.load(open("io_vocab.json"))["data"]   # json.load fails loudly on an HTML error page
bad = [r for r in rows if not (r.get("identifier") or "").startswith("https://spase-metadata.org/")]
print("rows", len(rows), "non-SPASE", len(bad))     # report any non-SPASE row; never use it
def sweep(term, typ=None):
    pat = re.compile(r"(?<![0-9A-Za-z])%s(?![0-9A-Za-z])" % re.escape(term), re.I)
    return [r for r in rows if (typ is None or r["type"] == typ) and
            any(pat.search(str(r.get(k) or "")) for k in ("name", "abbreviation", "identifier", "definition"))]
for t in ("SUVI", "xylophonic"):                     # a positive and a negative control beside every sweep
    print(t, [(r["type"], r["name"], r["identifier"]) for r in sweep(t)])
PY2
```

**Traps:**
- `?columns=` silently drops unknown column names, and omitting `id` returns an empty `data[]`; both read
  as a clean zero. A wrong model name on the endpoint returns an HTML error page — `json.load` every file.
- Omitting `definition` from a sweep changes its counts; an absence claim needs all four columns.
- Spelling splits inside one instrument family (`XRS` vs `SXM` for GOES solar X-ray) make a
  single-spelling sweep structurally blind; search both path spellings and the name side.
- False friends: `GOES/12/SXI` is the Solar X-Ray *Imager*, not the X-ray monitor; a spacecraft pointing
  file archived under another instrument's directory tree (Fermi's `lat/weekly/spacecraft/`) is not that
  instrument's data; a closed station listing a facility as "collaborator" is not that facility.
- Identical names on different rows: `…/Observatory/GOES/4` is named exactly like the fleet-level
  `…/Observatory/GOES` row; "Solar X-ray Sensor on GOES" names three rows. Match on identifier, never on
  name.
- A grep hit for an instrument name in a leftover test fixture, a docstring example or a vendored
  third-party comment is not support (rules 3–4).
- Unanchored greps inflate (`TEC` in "protections"); anchored `git grep -P '\bTEC\b'` does not — and
  `git grep -E` reads `\b` as a literal `b`.
- Row names can differ from their own SPASE page; a validator comparing a quoted row name to the page
  will report a false "altered quotation". Check the row.

## Payload and roundtrip notes

- **Key:** `relatedInstruments` — an array of `{name, identifier}` objects. `name` is the matched row's
  `name` copied verbatim (typically the SPASE name with any parenthetical abbreviation already stripped —
  e.g. `Parker Solar Probe`, not `Parker Solar Probe (PSP)`); `identifier` is the SPASE Resource ID URL
  (`https://spase-metadata.org/...`) from the controlled list.
- **Never send `landing_url`.** It is server-derived during the vocabulary refresh (a HelioData mission
  page when one is confirmed to exist, otherwise empty so the link falls back to the SPASE
  `identifier`) and is ignored on submission. Agents only ever set `name` and `identifier`.
- **Backend matching:** the name is stripped of edge whitespace, the identifier is stripped and
  URL-validated; an **exact** identifier match returns the existing row and **ignores the sent name** (a
  shared row's nonblank name is never overwritten, so a PATCH cannot rename it). An identifier with no
  matching row **creates a new row** with the sent name; no identifier falls back to the case-sensitive
  `filter(name=…, type=…).first()` or creates an identifierless row (rule 22). No `.html`
  normalization happens server-side.
- **Strip annotations, except the blocker.** The submitter strips source annotations and prose notes
  from values, but an entry marked `NEEDS MANUAL RESOLUTION` **or carrying no SPASE `identifier`** is
  non-submittable: do **not** strip the marker and submit the bare name. Omit it from the payload,
  carry it into the verification or diff report, and always surface every omitted entry to the user.
- **SPASE gate — a hard blocker for EXECUTE.** Every `relatedInstruments`/`relatedObservatories` entry
  must carry a `https://spase-metadata.org/` identifier. An entry must have been omitted if it was marked
  `NEEDS MANUAL RESOLUTION`; was flagged as an unresolved match (several rows, no evidence selecting
  among them); or carries a `name` with no identifier. A multi-row expansion backed by cited evidence is
  legitimate — verify each row has an identifier and let it through. PREPARE may produce the report, but
  no POST or PATCH while any unresolved or identifierless entry remains. If an upstream extraction
  already marked an entry, treat the marker as the same blocker — do not re-resolve it into a submittable
  value.
- **The gate tests the list the request sends.** Compute it on the post-patch state: per field, the list
  in `patch` if the key is present, otherwise the list HSSI already stores. A check over stored rows can
  never see the row being added. Assert for each entry: the SPASE prefix; exactly one vocabulary row for
  the identifier (no miss, no collision); the row's stored name equals the sent name byte for byte; no
  `.html` duplicate for the same resource. Control the gate with inputs that must **fail** — a non-SPASE
  identifier, a well-formed SPASE identifier with no row, and a name differing by one trailing space.
- **PATCH** replaces the whole list; every element sent is a fresh resolution (retained values carry the
  mint hazard too), a stored member left out is removed, `[]` or `null` clears, an omitted key leaves the
  field unchanged. Compare as a multiset.
- **Readback:** in the stored/curator form the identifier key is renamed —
  `relatedInstruments[].identifier` → `relatedInstruments[].relatedInstrumentIdentifier` — so verify on
  the renamed key, not the submitted one. `/api/data/` returns row UUIDs (resolve them before comparing);
  `/api/view/` plain JSON renders `name (abbreviation)`.
- **ORM:** `InstrumentObservatory.softwares` lists the entries citing a row as an *instrument*;
  `.observatories` lists those citing it as an *observatory*.

## Worked examples

- **Evidence selects many rows, and a spelling hides some (sunkit-instruments).** The package reads
  GOES SUVI files for satellites 16–19 and computes GOES X-ray temperatures with per-satellite code, so
  the four SUVI rows are recorded under rule 18. A sweep keyed on `XRS` alone missed the GOES 6–8 rows,
  which the vocabulary spells `SXM`; they are added on specific evidence (a docstring naming GOES 7 as the
  calibration reference, a correction branch for GOES 6 alone, per-satellite table indexing). The GOES 8
  row's double space is copied as stored (rule 16).
- **Resolves cleanly, still excluded (hissw).** AIA appears only as an example argument, an example page
  and a smoke test that calls an SSW routine. The `Atmospheric Imaging Assembly` row exists, but rule 3
  fires; the field is empty, and the dossier names the row so a later refresh sees a relevance decision,
  not a lookup failure.
- **An archive-wide client (MadrigalWeb).** Facility names in the tree are docstring examples and CLI
  usage strings, and the user chooses the server at run time. Rule 2 fires. The closest row for the
  example facility has the bare name `Incoherent Scatter Radar`, and other rows sharing its place name
  are a magnetometer observatory and a digisonde — recorded as considered and declined.
- **A vendored comment (pyflct).** One line in vendored C notes that a projection's grid spacing holds
  for HMI's remapped data. It is an implementation convenience in third-party code, not an HMI reader —
  rule 4 — so Fields 31 and 32 are empty, with the HMI and SDO rows named for the record.
- **Counting a family by namespace (PyAuroraX).** The package has a dedicated reader for THEMIS ASI data;
  filtering identifiers on `/SMWG/Instrument/THEMIS/Ground/` and the terminal segment `ASI` yields all
  24 stations, none of the magnetometer rows, and all 24 are recorded (rule 18). A name-substring sweep
  undercounts because the family's names are not uniform.

## Provenance

- No regenerated blocks; hand-written.
- Migrated from RSFF 704-735 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
