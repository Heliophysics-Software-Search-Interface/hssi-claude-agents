# Field 22 — Related Phenomena

**Level:** OPTIONAL · **API:** `relatedPhenomena[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/Phenomena/rows/all/`
**Filter tab:** Phenomena (tab coded, currently disabled) · **Free-text search tier:** T3 · **Field-search code:** `phenomena`

## What it is

**Type:** Multi-select dropdown (**closed** controlled vocabulary — custom entries are rejected)

**What it is:** The phenomena the software supports science functionality for.

**How to fill it:** Select phenomena terms from the controlled vocabulary below. Despite the web form's free-text affordance, the API path is strict: `related_phenomena` resolves through `_get_graph_list_item`, which raises `Unknown value` on anything not in the list. A phenomenon the software supports that has no row belongs in **Keywords** (Field 16, the open vocabulary), not here.

**Level:** OPTIONAL on the live form (the form source declares `RequirementLevel.OPTIONAL`); older guidance
that grouped it with Fields 4 and 5 as RECOMMENDED was wrong.

<!-- vocab:Phenomena begin -->
**Possible Values** — *7 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/Phenomena/rows/all/` is authoritative.*

- Coronal Heating
- Coronal Mass Ejections
- Geomagnetic Storms
- Solar Corona
- Solar Flares
- Solar Wind
- X-ray emission
<!-- vocab:Phenomena end -->

The vocabulary is flat: every row is a top-level value, no `Parent:Child` form, and no row implies any
other. The rows carry no identifiers and no definitions. `Coronal Holes` is **not** a value and is
rejected on submission.

## Why it exists

Some searchers start from a phenomenon — a flare, a storm, the solar wind — rather than from a region or a
technique, and this field is how the catalogue answers them. A correct value returns software built to
analyse, model, or detect that phenomenon. A padded value (every phenomenon the software could in
principle be applied to, or the phenomena of a library it wraps) fills those result lists with tools that
do nothing specific for the phenomenon, and an arbitrary subset gives unhelpful hits in some filters and
unexplained misses in others. Because the vocabulary is short, most entries correctly carry few or no
values.

## How it appears on the site

- **Detail page:** in the "Science Context" section, as "Related Phenomena" — one tag per stored row
  showing the row `name` (the raw identifier if the name is `UNKNOWN`). A row with an identifier links to
  it; the current rows have none, so they render as plain tags. Tags appear in stored order.
- **Filter:** a Phenomena tab exists in the frontend code but is disabled (commented out of the filter
  menu), so the field drives no sidebar filter today.
- **Free-text search:** tier T3 (`related_phenomena__name`).
- **Field search:** `phenomena:"…"` matches `related_phenomena__name__icontains`.
- **JSON-LD:** each row is emitted in `keywords` as a `DefinedTerm` with description `relatedPhenomena`.

## Rubric: include / exclude

Apply per row, top to bottom; stop at the first rule that fires. The vocabulary is small enough to walk
whole: give each of the seven rows a verdict on every extraction and refresh.

1. **Only live rows; anything else goes to Keywords.** A value must be an exact row of the live
   `/api/models/Phenomena/rows/all/` vocabulary. A phenomenon the software genuinely addresses that has no
   row (an instability mode, cosmic-ray access, cutoff suppression) is recorded as a Field 16 keyword, not
   forced onto the nearest row by name. Fires on: a candidate that is not a live row.

2. **A wrapper has no phenomena of its own.** Software with no phenomenon-specific code — a bridge that runs
   another library, a templating or I/O layer — gets none, whatever the wrapped library covers. Fires on:
   the only link to the phenomenon is the reach of a library the software calls. Record the rows as
   rejected so they are not re-inherited.

3. **The arbitrariness test.** If the software's relation to every row is identical and indirect, no
   principled subset exists: select none. Fires on: no fact about the software explains why it would carry
   one row and not another.

4. **A technique is not a phenomenon; downstream use does not count.** Software that implements a general
   method (flow tracking, coordinate conversion, a climatological model interface) does not carry the
   phenomena its outputs are later used to study. Fires on: the connection to the phenomenon runs through a
   consumer of the software's output, one or more steps removed, and no source states it.

5. **Include a phenomenon the software analyses, models, or detects as a primary function.** Evidence is
   code that works on the phenomenon itself: detecting or classifying events (flare lists, flare-class
   conversion), computing its standard diagnostics (Dst, SMR and auroral-electrojet indices for storms),
   modelling or simulating it (the solar wind out to 1 AU), processing its defining measurement (soft
   X-ray irradiance for `X-ray emission`), or a function whose whole point is a phenomenon-specific effect
   (a Kp-dependent storm-time cutoff correction). The software need not name the phenomenon in prose when
   the code computes it; state the inferential step in the dossier. Fires on: such code or a primary
   source stating that capability.

6. **An activity index as an input is not the phenomenon.** A general climatology or index interface that
   takes ap, Kp, or Dst as a parameter across all activity levels does not carry `Geomagnetic Storms`.
   Fires on: the index only parameterises a quiet-time or general-purpose model (rule 5's storm-time
   function is the contrast case).

7. **Prefer the row that names the process.** `Solar Corona` names a region-like container; when the
   evidence supports a coronal process row (`Coronal Heating`) and gives `Solar Corona` no additional
   support, record the process row only.

8. **Decide independently of Field 5.** `Solar Wind` is a row in both vocabularies; the Region row is a
   place, the Phenomena row a process. Field 5 has a "solar, region unspecified" row (`Solar Environment`)
   and this field has no "solar generally" row, so the same evidence can legitimately fill Field 5 and
   leave this field empty. Never select several phenomena to mean "solar".

9. **Incumbents are re-derived.** On a refresh give every stored row its own verdict under rules 1–8.
   Keep a row the evidence supports; add a row that now passes; clear a row that fails (an inherited
   "typical use case", a downstream application, an arbitrary subset). A stored value a fair reading of
   the evidence supports is kept — removal needs evidence that it is wrong, not that it is arguably
   imprecise.

10. **Empty is a legitimate outcome.** Never invent a phenomenon. An empty field with the seven rows
    examined and the near-misses recorded is correct for most software; an unexamined blank is the only
    defect.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. The code: event detection, phenomenon-specific diagnostics, models and simulations of the phenomenon,
   processing of its defining measurement.
2. The project's own description, README and docs.
3. The reference publication and the algorithm papers the docs name.
4. The software's institutional home, when the code computes that home's phenomenon (the analysis package
   of a storm-research centre that computes storm indices).

**Verification steps:**
- Fetch and print the live vocabulary:
  `curl -s <target>/api/models/Phenomena/rows/all/ | python3 -c 'import json,sys; [print(r["name"]) for r in json.load(sys.stdin)["data"]]'`.
- For each kept row, cite the function, module, or passage; for each near-miss, record why it fails.
- When a term sweep drives a claim, read every match: a search for `CME` also matches identifiers such as
  `RCMEq`, and a search for `storm` may match only an institution's name.

**Traps:**
- **`Coronal Holes` is not a row**, and `Geomagnetic Storms` and `Solar Wind` are; stale lists have had
  both errors.
- **Region and phenomenon are different questions** (rule 8).
- **An institution or program name is not evidence** by itself; what the code computes is.
- **A value no source states and no code computes is an inference dressed as metadata** — pyflct's
  `Solar Flares` rested only on what flow maps are later used for.

## Payload and roundtrip notes

- **Key:** `relatedPhenomena` — an array of exact row names.
- **Binding:** graph-list lookup; a value without a colon matches `name__iexact` and takes the first row.
  An unknown value raises `Unknown value '<value>'` and rejects the whole atomic request.
- **Order is stored data.** `related_phenomena` is a sorted many-to-many field (sortedm2m); the order sent
  is the order stored and returned. On a refresh, preserve the stored order and append new rows after it.
- **PATCH replaces the whole list.** Enrichment sends the stored rows plus the new ones; an approved
  removal sends the complete final list. `[]` or `null` clears the field; an omitted key is unchanged.

## Worked examples

- **Bridge to SolarSoft (hissw).** Four solar phenomena were stored as "typical SSW use cases". The package
  implements no phenomenon-specific science; its relation to every row is identical. Rules 2 and 3: all
  four are cleared, while Field 5 keeps `Solar Environment` (rule 8).
- **Global geospace model analysis package (Kaipy).** It computes Dst, SMR and SME/SML/SMU and simulates the
  solar wind. Rule 5 adds `Geomagnetic Storms` and `Solar Wind`, although the word "storm" appears only in
  the centre's name; `Coronal Mass Ejections` is rejected because its term matches were identifiers, not
  CME code.
- **Magnetospheric coordinate and cutoff library (python-magnetosphere).** A function exists to correct
  cutoff rigidity for Kp and local time — a storm-time effect and that function's whole purpose. Rule 5
  records `Geomagnetic Storms`; the physically exact terms (cosmic ray, cutoff rigidity) have no row and go
  to Keywords (rule 1).
- **Horizontal wind climatology (HWM-93).** Ap is an input switch to a quiet-time model. Rule 6: no
  `Geomagnetic Storms`; the field is evidenced-empty.
- **Solar-wind instability classifier (SAVIC).** The instabilities it classifies have no rows (Keywords carries
  `plasma instabilities`); the solar wind is the medium whose kinetic behaviour it characterises, so rule 5 adds
  `Solar Wind`, decided separately from Field 5's `Solar Wind` row.

## Provenance

- Vocabulary block `vocab:Phenomena` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 568-591 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
