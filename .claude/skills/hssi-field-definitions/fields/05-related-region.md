# Field 5 — Related Region

**Level:** RECOMMENDED · **API:** `relatedRegion[]` · **Change class:** enrich-only
**Vocabulary:** `/api/models/Region/rows/all/`
**Filter tab:** Region · **Free-text search tier:** T3 · **Field-search code:** `region`

## What it is

**Type:** Multi-select dropdown

**What it is:** The physical region the software supports science functionality for.

**How to fill it:** Select all physical regions the software's functionality is commonly used or intended for.

The vocabulary is currently flat — every row is a top-level value, no `Parent:Child` form. The 24 rows
carry no parent/child links, no identifiers and no definitions, so no row implies any other: selecting
`Earth Magnetotail` does not make an entry findable under `Earth Magnetosphere`, and the reverse is
equally false.

<!-- vocab:Region begin -->
**Possible Values** — *24 values, snapshot 2026-07-29, verified identical on `https://hssi.hsdcloud.org` and `http://localhost`. Live `/api/models/Region/rows/all/` is authoritative.*

- Chromosphere
- Corona
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Inner Magnetosphere
- Earth Ionosphere
- Earth Lower and Middle Atmosphere
- Earth Magnetosheath
- Earth Magnetosphere
- Earth Magnetotail
- Earth Outer Magnetosphere
- Earth Thermosphere
- Heliosheath
- Interplanetary Space
- Jupiter Magnetosphere
- Mars Magnetosphere
- Neptune Magnetosphere
- Photosphere
- Planetary Magnetospheres
- Saturn Magnetosphere
- Solar Environment
- Solar Interior
- Solar Wind
- Uranus Magnetosphere
<!-- vocab:Region end -->

**The old five are not the vocabulary.** Older instructions listed only five values (`Earth Atmosphere`,
`Earth Magnetosphere`, `Interplanetary Space`, `Planetary Magnetospheres`, `Solar Environment`). Those
are the keys of `REGION_MAPPING_TTL` in `models/vocab.py` — a mapping used for TTL export, **not** the
selectable vocabulary. All 24 rows above are offered by `/api/models/Region/choices/`. The five survive
as the coarse rows of the containment pairing in the rubric below.

## Why it exists

A heliophysicist browsing the catalogue usually starts from a place — the ionosphere, the corona, the
magnetotail — and the Region filter is how they narrow several hundred entries to the tools that work
there. A correct value puts the software in front of exactly the people who study that region. A missing
fine value hides it from anyone who filters on the specific region; a missing coarse value hides it from
anyone who browses at the broad level, because the filter does not inherit. A padded value — a region
copied from a registry facet, a downstream consumer, or a test fixture — spends every such searcher's
attention on a tool that does nothing there, and costs the filter its trust.

## How it appears on the site

- **Detail page:** in the "Science Context" section, as "Related Regions" — one tag per stored row,
  showing the row `name` (the raw identifier if the name is `UNKNOWN`; Region rows currently carry no
  identifier), each linking to the homepage filtered by that region. Tags appear in stored order.
- **Filter:** the sidebar **Region** tab lists all 24 rows as flat, independent items. Filtering matches
  the exact row; there is no parent/child inheritance, so an entry appears under a region only if it
  stores that row.
- **Free-text search:** tier T3 (`related_region__name`).
- **Field search:** `region:"…"` matches `related_region__name__icontains`.
- **JSON-LD:** each row is emitted in `spatialCoverage` as a `Place`/`DefinedTerm` with description
  `RelatedRegion` and the Helio-KNOW `hk_region.ttl` term set.

## Rubric: include / exclude

Apply per candidate region, top to bottom. Rules 1–4 decide each fine row — stop at the first of them
that fires. Rule 5 then runs for every fine row that passed and is never skipped: its coarse row is
added whether or not the coarse row has evidence of its own. Walk **all 24 rows** on
every extraction and refresh, asking which new rows now apply — validating only the recorded values reads
as complete while missing the point.

**Containment pairing used by rules 5–6.** The vocabulary carries no links, so this rubric supplies them:

| Coarse row | Fine rows it contains |
|---|---|
| Earth Atmosphere | Earth Lower and Middle Atmosphere, Earth Thermosphere, Earth Ionosphere, Earth Auroral Subregion |
| Earth Magnetosphere | Earth Inner Magnetosphere, Earth Outer Magnetosphere, Earth Magnetotail, Earth Magnetosheath |
| Interplanetary Space | Solar Wind, Heliosheath |
| Planetary Magnetospheres | Mars Magnetosphere, Jupiter Magnetosphere, Saturn Magnetosphere, Uranus Magnetosphere, Neptune Magnetosphere |
| Solar Environment | Solar Interior, Photosphere, Chromosphere, Corona |

1. **Only live rows.** A value must be an exact row of the live `/api/models/Region/rows/all/`
   vocabulary. **Never flag a specific region as invalid just because it isn't one of the old five.**
   Fires on: a candidate string not in the live list — drop it (or map it to the row it misspells).

2. **Domain-independent software is evidenced-empty.** A file-format library, a metadata-schema tool, a
   generic REST client, a coordinate converter with no region-specific behaviour — software that behaves
   identically whatever physical domain the data describe — gets no region. Fires on: no region-specific
   code, data handling, or stated purpose anywhere in the pinned tree and the project's own description.
   Record the sweep and the rejected candidates so the blank is evidenced.

3. **Decide from the software's own purpose, not from borrowed labels.** None of these is evidence for a
   region: a PyHC registry facet tag or a Zenodo subject tag (`ionosphere_thermosphere_mesosphere`,
   `magnetosphere`, `solar`); a PyPI trove topic such as `Atmospheric Science`; the regions of downstream
   pipelines or missions that consume the software; the missions whose files appear as test fixtures; the
   regions peer packages list. Fires on: a candidate whose only support is one of these — exclude it,
   and record the source so a later refresh recognises it on sight.

4. **Region is where the physics the software handles happens, not where the instrument sits or where
   a quantity happens to be evaluated.** An all-sky-imager tool works in `Earth Ionosphere` and
   `Earth Auroral Subregion`, not at the ground station; a magnetometer or field model works in the
   magnetospheric regions it models. A coordinate library whose frames are used everywhere does not
   thereby work in every region those frames describe, and a geomagnetic quantity evaluated at 450 km is
   not ionospheric physics. **A region row is not a planet filter:** software about a planetary surface,
   atmosphere, or ionosphere gets no `<Planet> Magnetosphere` row, because the vocabulary has no row for
   what it studies. Fires on: evidence in code, documentation, the reference paper, or the project's
   stated purpose that the software computes, models, processes, or analyses the physics of that region.

5. **List every fine row the software works in, and the coarse row that contains each — always.** Per
   the containment table, `Earth Magnetotail` brings `Earth Magnetosphere`, `Earth Ionosphere` brings
   `Earth Atmosphere`, `Photosphere` brings `Solar Environment`, and so on. This is required because the
   vocabulary is flat and the Region filter does not inherit: without the coarse row the entry is
   invisible to anyone browsing at that level. A fine row is never implied by its coarse row either, so
   each fine row needs its own evidence under rule 4. Fires on: a fine row that passes rule 4.

6. **Coarse alone only when nothing finer applies.** When the evidence supports a domain but no
   particular region inside it, record the coarse row by itself (`Solar Environment` for a bridge whose
   whole purpose is running the solar-physics library it wraps). Never add a fine row to make the record
   look specific. Fires on: a coarse domain evidenced under rule 4 with no fine row that passes it.

7. **A wrapper takes the regions of its own purpose, not its wrapped library's reach.** A wrapper whose
   entire purpose is one domain gets that domain (rule 6); a wrapper around a domain-independent core, or
   a general tool that a region's scientists merely happen to use, is evidenced-empty (rule 2). Fires on:
   software with no domain code of its own.

8. **Incumbents are re-derived, not inherited.** On a refresh every stored row gets its own verdict under
   rules 1–7. Keep a stored row the evidence supports; add every row that now passes rules 5–6, including
   a coarse row missing beside a stored fine row; clear a stored row that fails (a legacy-five default,
   a registry facet, a downstream consumer's region). A stored value a fair reading of the evidence
   supports is kept — removal needs evidence that it is wrong, not that it is arguably imprecise.

9. **RECOMMENDED, but treated as critical.** Never invent a region. An empty value is legitimate only when
   the dossier carries durable evidence that no value applies (rules 2, 4, 7); an unexamined blank is an
   **ERROR**.

## Ask the user only when

Nothing — the rubric decides every known case.

## Where to find it, and traps

**Sources, in priority order:**
1. The code: what physical system the modules compute, model, process, or analyse (model domains,
   altitude grids with their physics, variable tables, region-specific guards such as a latitude cut to
   auroral latitudes). Read the code, not just the README.
2. The project's own description, README, docs, and package metadata `description`.
3. The reference publication and the papers the documentation names for its algorithm.
4. Peer-reviewed uses of the software (Field 27) — corroboration of what it is used for, never a
   substitute for rule 4.

**Verification steps:**
- Fetch the live vocabulary and print it — it is small enough to read whole:
  `curl -s <target>/api/models/Region/rows/all/ | python3 -c 'import json,sys; [print(r["name"]) for r in json.load(sys.stdin)["data"]]'`.
- For each candidate: is it in the live list; what file, function, or passage evidences it; does rule 4
  hold; is its coarse row (or fine rows) handled per rules 5–6?
- Check that the software actually operates in every listed region, and that no region it supports is
  missing.

**Traps:**
- **"X encompasses Y" is not an argument here.** The rows are flat; a coarse row never stands in for a
  fine one and a fine row never stands in for its coarse row. Each row is earned on its own evidence, and
  rule 5 adds the coarse row explicitly.
- **Legacy-five defaults.** A stored `Earth Atmosphere` or `Earth Magnetosphere` with no recorded
  evidence is often a leftover from the old five-item dropdown. Re-derive it: it stays when it is the
  coarse row of an evidenced fine row or itself evidenced, and goes otherwise.
- **Registry facet tags propagate.** The same PyHC Science Area tag sits on unrelated entries (a Zenodo
  REST client, a grid-square converter). Its presence says nothing about the software.
- **Test fixtures and example data** are chosen for structural variety, not scope. A format library's
  test corpus of mission files is not a list of regions.
- **Downstream use two steps removed** (FLCT velocities feed coronal simulations) does not make the
  downstream region the software's.
- **`Solar Wind` is a row in both Region and Phenomena** (Field 22); one is a place, the other a process.
  Decide each on its own evidence.
- **No `Not applicable` row exists.** An evidenced-empty field is the only way to say a region does not
  apply; never pick a placeholder row to fill it.

## Payload and roundtrip notes

- **Key:** `relatedRegion` — an array of exact row names.
- **Binding:** each value resolves through the graph-list lookup; a value without a colon matches
  `name__iexact` and takes the first row. An unknown value raises `Unknown value '<value>'` and rejects
  the whole atomic request.
- **Order is stored data.** `related_region` is a sorted many-to-many field (sortedm2m): the order sent is
  the order stored, `/api/view/` returns it, and the detail page renders tags in it. A set comparison hides
  a reorder. On a refresh, **preserve the stored order and append new rows after it**; never reorder
  stored rows as a side effect. For a new entry, write each coarse row followed by the fine rows it
  contains.
- **PATCH replaces the whole list.** Enrichment is identity-aware set-union in stored order: send the
  stored rows, then the new ones. An approved removal sends the complete final list. `[]` or `null`
  clears the field; an omitted key is unchanged.
- **`/api/data/` returns row UUIDs**, not names; resolve them against the vocabulary before believing a
  baseline shows drift.

## Worked examples

- **Auroral precipitation model.** A model restricted by an explicit guard to auroral latitudes, with an
  altitude grid spanning the thermosphere, stored only `Earth Atmosphere`. Rules 4–5 add
  `Earth Ionosphere`, `Earth Auroral Subregion`, and `Earth Thermosphere` and keep `Earth Atmosphere` as
  their coarse row; `Earth Lower and Middle Atmosphere` is rejected because the model does nothing below
  the mesopause. The stored row keeps its position and the three are appended.
- **Photospheric flow tracker (pyflct).** The algorithm papers recover photospheric velocities from
  magnetograms, so `Photosphere` is added and `Solar Environment` kept as its coarse row. `Corona` is
  rejected: coronal simulations are downstream consumers of the output (rule 4 trap).
- **Python bridge to SolarSoft (hissw).** No module implements solar physics, but the package exists to run
  the solar-physics IDL library. Rule 6 records `Solar Environment` alone; no finer row is supported.
- **Zenodo REST client (PyZenodo).** Three stored regions restated the PyHC registry's facet tags; the
  code contains no heliophysics term. Rule 3 then rule 2: all three are cleared and the field is
  evidenced-empty, decided together with the same tags in Field 16.
- **Mars radio-science reader (MGSutils).** The data concern the Martian surface and atmosphere; the only
  Mars row is a magnetosphere row, and the software cannot read magnetometer data. Rule 4 (not a planet
  filter): the stored `Planetary Magnetospheres` is cleared and the field is evidenced-empty.

## Provenance

- Vocabulary block `vocab:Region` is regenerated by the `update-api-spec` skill (Step A); everything else is hand-written.
- Migrated from RSFF 180-224 on 2026-09-22.
- Rubric authored 2026-09-22 from prior guidance and past refresh decisions.
