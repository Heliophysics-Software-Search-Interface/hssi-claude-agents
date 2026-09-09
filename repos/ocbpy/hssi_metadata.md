# HSSI Metadata Extraction Results

**HSSI Software ID:** 7fe5501b-aab0-4b70-9fef-08933ccf7480
**Repository:** https://github.com/aburrell/ocbpy
**Source Revision:** 3ced0dec8cabf055b9e0a75a5eb1a57c017740be
**Extraction Date:** 2026-09-08
**Validation Date:** 2026-09-08
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

All repository evidence below is read at the pinned revision
`3ced0dec8cabf055b9e0a75a5eb1a57c017740be`, which is the commit tag `0.7.0` points at and was the tip
of `origin/main` when this extraction was made. That tree carries 124 tracked files.

Two properties of this repository shape almost every field:

1. **OCBpy ships its boundary data inside the package.** `ocbpy/boundaries/` contains six `.ocb` and
   six `.eab` boundary files derived from the IMAGE FUV imagers and from AMPERE, and the DMSP SSJ
   boundaries are downloaded and written in the same two formats on demand. They are *data*, not
   source, but they are the reason this software is genuinely tied to specific
   instruments, observatories, datasets and publications rather than being an instrument-agnostic
   utility. Fields 27, 28, 31 and 32 all rest on them.
2. **The software's user-facing product is coordinates and gridded data, not files.** Its central API
   returns transformed coordinates and modified in-memory objects; only three code paths write files.
   That asymmetry is why Field 18 is richer than Field 19.

The catalogue record still described release `0.6.0` when this refresh began, so the field that tracks
a release (12) and the fields the 0.6.0 and 0.7.0 work extended (4, 27) lagged the pinned tree. Where a field's value is being carried
forward unchanged, the note says on what evidence; where it is being changed, the note says what
supersedes the previous value and why.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Placeholder by design. The submitter identifies the person filing the record, not an attribute of the
software, and this dossier is not a submission.

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.1179230

This is the correct value and it is not in doubt. It is the Zenodo **concept** DOI: the DataCite record
for it carries a `HasVersion` relation to every release deposit — nine of them when read on
2026-09-08, namely `10.5281/zenodo.20562260`, `7236462`, `1217177`, `14756066`, `4289226`,
`16802585`, `3978784`, `11520809` and `1179231`. Its publisher is `Zenodo`, and its `version`
attribute tracked the newest release (`0.7.0`) on that date. A concept DOI that resolves to whichever
release is current is exactly what Field 2 is for; the version-specific DOI belongs in Field 12 and is
recorded there.

The project asserts the same DOI in three independent places at the pin: `ocbpy/__init__.py` line 3 is
the comment `# DOI: 10.5281/zenodo.1179230` (the same comment heads `ocbpy/boundaries/__init__.py`,
`ocbpy/instruments/__init__.py`, `ocbpy/boundaries/README.md` and the other package modules);
`README.md` carries a Zenodo badge pointing at `https://zenodo.org/badge/latestdoi/96153180`; and the
BibTeX block in `docs/citing.rst` gives `doi    = {10.5281/zenodo.1179230}`.

Considered and rejected: the version DOI `https://doi.org/10.5281/zenodo.20562260` (it identifies one
release, so pinning Field 2 to it would make the record's primary identifier go stale at every
release), and `https://doi.org/10.1029/2018JA025877` (a publication DOI — Field 14's business, and it
is recorded there as the reference publication).

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/aburrell/ocbpy

The canonical repository. `pyproject.toml` declares `source = "https://github.com/aburrell/ocbpy"`,
the PyHC community registry gives the same `code:` value, and the GitHub API reports
`full_name aburrell/ocbpy`, `fork false`, `archived false`, `default_branch main`.

### 4. Software Functionality (RECOMMENDED — treated as critical)
- **Values:**
  - Coordinate Transforms
  - Coordinate Transforms: Ionospheric
  - Coordinate Transforms: Magnetospheric
  - Data Processing and Analysis
  - Data Processing and Analysis: Analysis
  - Data Processing and Analysis: Data Access and Retrieval
  - Data Processing and Analysis: File Format Conversion
  - Data Processing and Analysis: Processing
  - Models and Simulations
  - Models and Simulations: Data Guided
  - Models and Simulations: Empirical

The first five values were already correct and are carried forward. Six are added by this refresh:
three name long-standing capabilities the record had never reflected (`Processing`, `Analysis` and
`File Format Conversion` under `Data Processing and Analysis`), and three cover the boundary-model
capability introduced in 0.6.0 and extended in 0.7.0.

Evidence, value by value:

- **Coordinate Transforms**, **Coordinate Transforms: Ionospheric** — the package's entire purpose.
  `ocbpy/_boundary.py` exposes `OCBoundary`, `EABoundary` and `DualBoundary`, whose
  `normal_coord`/`revert_coord` methods convert between AACGM magnetic coordinates and a
  boundary-relative magnetic latitude/local-time grid, and `ocbpy/vectors.py` provides the vector
  rotation that goes with it (`adjust_vector`, `calc_dest_polar_angle`, `calc_dest_vec_sign`). The
  transform is ionospheric in kind: the base system is AACGM (via the `aacgmv2` dependency, called as
  `get_aacgm_coord_arr`, `convert_latlon_arr` and `convert_mlt` in `_boundary.py`, `ocb_scaling.py`
  and `boundaries/dmsp_ssj_files.py`), and the boundaries are ionospheric footprints.
- **Coordinate Transforms: Magnetospheric** — the boundary that defines the grid is a magnetospheric
  one. The open–closed field line boundary separates open (lobe-connected) from closed magnetic flux,
  and the AMPERE boundaries are derived from Birkeland-current radii, so the coordinate system encodes
  magnetospheric topology rather than a purely ionospheric feature. Retained on that reasoning.
- **Data Processing and Analysis** and **Data Processing and Analysis: Data Access and Retrieval** —
  `ocbpy/boundaries/dmsp_ssj_files.py` fetches DMSP SSJ boundary files from a Zenodo deposit
  (`fetch_ssj_boundary_files`, whose `doi` keyword defaults to `'10.5281/zenodo.3373811'`, using
  `zenodo_get`), verifies them against the deposit checksum, and `fetch_format_ssj_boundary_files`
  wraps fetch-and-convert in one call. This is a user-facing download API, not an internal fetch.
- **Data Processing and Analysis: Processing** *(addition)* — `ocbpy/instruments/supermag.py` and
  `ocbpy/instruments/vort.py` implement whole pipelines: read an instrument file, match every record
  to a boundary in time, transform coordinates, scale vector quantities, write the augmented result
  (`supermag2ascii_ocb`, `vort2ascii_ocb`). `ocbpy/instruments/pysat_instruments.py::add_ocb_to_data`
  does the same in-place against a loaded pysat `Instrument`. Pipeline data processing is a primary
  user-facing capability and the record did not reflect it.
- **Data Processing and Analysis: Analysis** *(addition)* — `ocbpy/ocb_scaling.py` computes derived
  physical quantities rather than merely reshaping data: `normal_evar` and `normal_curl_evar`
  normalise quantities proportional to the electric field and to its curl for the difference between
  the observed and the reference boundary radius, and `VectorData` decomposes and re-projects vector
  components (with `hav`/`archav` haversine helpers). `ocbpy/cycle_boundary.py::satellite_track`
  determines whether a point lies along a satellite track. These are analysis operations on science
  data.
- **Data Processing and Analysis: File Format Conversion** *(addition)* —
  `boundaries/dmsp_ssj_files.py::format_ssj_boundary_files` reads DMSP SSJ `*_boundaries.csv` files
  (`data = np.loadtxt(infile, skiprows=skiprows, delimiter=',')`) and writes OCBpy-format `.ocb` and
  `.eab` boundary files, one per hemisphere and boundary type — reading one format and writing
  another, which is precisely this subcategory.
- **Models and Simulations**, **Models and Simulations: Empirical** *(additions)* — `ocbpy/boundaries/models.py`
  is a boundary-model module added in 0.6.0 and extended in 0.7.0. `docs/ocb_models.rst` describes it
  as "empirically derived mathematical models are included in" the module, and it implements three:
  `starkov_auroral_boundary` (Starkov 1994, driven by the AL index), `gussenhoven_equatorward_auroral_boundary`
  (Gussenhoven 1983, driven by Kp) and `ch_aurora_2014_boundary` (Xiong and Lühr 2014, driven by the
  time-integrated Newell coupling function), plus their coefficient functions and a `circle_fit`
  helper. `Changelog.rst` records the two 0.7.0 arrivals: "* ENH: Added the Gussenhoven (1983) model
  for the EAB" and "* ENH: Added the CH-Aurora-2014 model for the OCB and EAB". These are empirical
  fits to observed boundary locations, so `Empirical` is the right subcategory.
- **Models and Simulations: Data Guided** *(addition)* — the models are index-driven rather than
  free-running: `docs/ocb_models.rst` says these "models typically depend on magnetic local time (MLT)
  and a geomagnetic or solar" wind index, and `ch_aurora_2014_boundary` additionally accepts
  `obs_colat`/`obs_mlt` ("CHAMP, or other, boundary observation co-latitudes") and shifts the model
  boundary by the mean model-minus-observation offset. `docs/ocb_models.rst` notes that for that model
  "the authors recommend adjusting the model output" with CHAMP FAC measurements. Observationally
  driven model output is what this subcategory names.

Considered and rejected, with reasons — these are the classifications most likely to be re-proposed:

- **Data Visualization** and every subcategory of it. The installed package contains no plotting code:
  a `git grep -F 'matplotlib'` over the recursive path `ocbpy` at the pin returns no files. The positive
  control shows the instrument works: the same pattern under `docs` matches four example pages
  (`ex_dmsp.rst`, `ex_general.rst`, `ex_init.rst`, `ex_vector.rst`) plus, as binary matches, the
  figures those examples generate. The nine PNGs in `docs/figures/` are documentation artifacts made
  by user code in the examples, not output of a package API.
- **Data Processing and Analysis: Data Assimilation.** Tempting because `docs/citing.rst` describes
  CH-Aurora-2014 as offering "an assimilated location based on FAC observations of the auroral"
  boundaries, and the code does blend observations into the model. But the implementation is a single
  mean-offset correction (`del_lat = np.nanmean(obs_colat - mod_colat)`), and a user filtering HSSI
  for data assimilation is looking for assimilation schemes — a variational or Kalman-type method.
  They would be disappointed to land here. The observational drive is recorded as
  `Models and Simulations: Data Guided` instead, which is accurate about what the code does.
- **Data Processing and Analysis: Time Series Analysis.** `ocbpy/cycle_boundary.py::match_data_ocb`
  matches time-ordered data records to boundary records within a tolerance, and `ocbpy/ocb_time.py`
  converts between time representations. That is temporal *matching and bookkeeping*, not analysis of
  time-series properties (no filtering, spectral estimation, trend or correlation analysis anywhere in
  the tree). Excluded so the subcategory keeps its meaning.
- **Models and Simulations: First Principles**, **Physics-Based**, **Forecasting**,
  **Forward-Fitting**. The three boundary models are empirical fits; nothing solves a physical system,
  and nothing predicts a future state (all three take a contemporaneous index). `circle_fit` fits a
  circle to boundary estimates using the method of Umbach and Jones (2003) — curve fitting inside an
  empirical model, not forward-fitting synthetic observations.
- **Data Processing and Analysis: Data Reduction.** Boundary-relative gridding preserves each
  measurement; it neither averages nor downsamples. The averaging a user might do afterwards is the
  user's, and the README's own framing is that fixed-grid averaging is the problem OCBpy exists to
  avoid.

All values are written fully qualified as `Parent: Child`. This matters here rather than being
cosmetic: `FunctionCategory` reuses subcategory names across parents (for example `Mission-Specific`
and `ML/AI` each appear under several parents, and `Analysis` and `Processing` appear under both
`Data Processing and Analysis` and `Mission-related`), so a bare child name can bind to the wrong
branch. The seed dossier's unspaced `Coordinate Transforms:Ionospheric` form is the legacy spelling of
the same value.

### 5. Related Region (RECOMMENDED — treated as critical)
- **Values:**
  - Earth Atmosphere
  - Earth Auroral Subregion
  - Earth Ionosphere
  - Earth Magnetosphere
  - Earth Thermosphere

`Earth Atmosphere` and `Earth Magnetosphere` were already recorded and are kept. Three more specific
regions are added by this refresh. The `Region` vocabulary is flat — no row has a parent or a child — so a coarse
value never implies a fine one and a fine value never displaces a coarse one; adding the specific
regions is additive, and the two incumbents continue to earn their place as the broad regions a user
may browse by.

- **Earth Auroral Subregion** *(addition)* — the closest match in the vocabulary to what this software
  actually is. Every boundary it handles is an auroral boundary: the open–closed field line boundary
  (poleward edge of the auroral oval), the equatorward auroral boundary, and the equatorward edge of
  the diffuse aurora. `ocbpy/__init__.py`'s module docstring is "Auroral oval and polar cap normalised
  location calculation tools." A user browsing the auroral subregion would be surprised *not* to find
  this package.
- **Earth Ionosphere** *(addition)* — the coordinate system is ionospheric. `docs/overview.rst` frames
  the problem in the "Magnetosphere-Ionosphere-Thermosphere (MIT) system"; the coordinate-system method paper
  it implements is about high-latitude ionospheric climatologies; the supported datasets are ionospheric
  (SuperDARN ionospheric vorticity, DMSP precipitating-particle boundaries, ground magnetometer
  equivalent currents); and the base coordinates are AACGM, an ionospheric magnetic coordinate system
  evaluated at an assumed altitude (`ref_alt=830.0` in the DMSP reformatting path).
- **Earth Thermosphere** *(addition)* — supported by the project's own framing and by the curated PyHC
  registry rather than by inference: `docs/overview.rst` names the
  "Magnetosphere-Ionosphere-Thermosphere (MIT) system" as the domain, `pyproject.toml`'s `keywords`
  list includes `"thermosphere"`, and the PyHC community registry classifies OCBpy under the
  discipline keyword `ionosphere_thermosphere_mesosphere`. High-latitude thermospheric measurements are
  exactly the kind of data the gridding is applied to.

Considered and rejected:

- **Solar Wind** and **Interplanetary Space** — `pyproject.toml`'s keyword list also contains
  `"heliosphere"`, and CH-Aurora-2014 is driven by a solar-wind coupling function. Neither is enough:
  the software reads no solar-wind data and models nothing there, and the coupling function enters as
  a scalar index supplied by the user. Someone browsing solar-wind software would find this out of
  place. This also shows the `pyproject.toml` keyword list is a loose discovery set rather than a
  region declaration, which is why `Earth Thermosphere` above rests on `docs/overview.rst` and PyHC as
  well as on that list.
- **Earth Magnetotail**, **Earth Outer Magnetosphere**, **Earth Inner Magnetosphere** — the polar cap
  maps along open flux to the lobes, so a tail association is arguable in principle, but OCBpy handles
  no magnetotail data and performs no magnetic-field-line mapping. `Earth Magnetosphere` carries the
  magnetospheric association at the level the software actually supports.
- **Earth Lower and Middle Atmosphere** — nothing in the package concerns altitudes below the
  ionosphere.

### 6. Authors (MANDATORY)

- **Author 1:**
  - **Name:** Angeline Burrell
  - **Author Identifier:** https://orcid.org/0000-0001-8875-9326
  - **Affiliation:**
    - **Organization:** United States Naval Research Laboratory
    - **Affiliation Identifier:** https://ror.org/04d23a975
- **Author 2:**
  - **Name:** Gareth Chisham
  - **Author Identifier:** https://orcid.org/0000-0003-1151-5934
  - **Affiliation:**
    - **Organization:** British Antarctic Survey
    - **Affiliation Identifier:** https://ror.org/01rhff309
- **Author 3:**
  - **Name:** Jone Reistad
  - **Author Identifier:** https://orcid.org/0000-0003-3509-5479
  - **Affiliation:**
    - **Organization:** Birkeland Centre for Space Science
    - **Affiliation Identifier:** Not found — see below

Three authors, in the order the project itself gives them. Corroborated by two independent sources:
`AUTHORS.rst` lists "Angeline G. Burrell", "Gareth Chisham" and "Jone P. Reistad" under `Authors`, and
`.zenodo.json`'s `creators` array gives the same three people with the same three ORCIDs and the same
three affiliation strings, which is what DataCite serves for both the concept DOI and the 0.7.0
version DOI. All three ORCIDs are already recorded correctly.

The affiliation for author 1 is recorded under the full institutional name **United States Naval
Research Laboratory** with ROR `https://ror.org/04d23a975`, rather than the bare "Naval Research
Laboratory" that `.zenodo.json` supplies. The expanded, ROR-bound form is the better value: Field 6's
guidance is to avoid abbreviated or ambiguous organisation names, and the ROR fixes the identity
beyond argument.

**Birkeland Centre for Space Science has no ROR record to supply — this is a controlled negative, not
an unfilled gap.** Fielded ROR v2 queries (`query.advanced=names.value:"…"`) return zero results for
`"Birkeland Centre for Space Science"`, `"Birkeland Centre"`, `"Birkeland Center for Space Science"`
and the Norwegian form `"Birkeland Senter for romforskning"`. A fielded query for the bare name
`"Birkeland"` returns exactly one record, `https://ror.org/03pf0r360` "Br. Birkeland (Norway)", a Norwegian company in
Storebø and not the research centre. The instrument demonstrably works: the positive control
`"British Antarctic Survey"` returns exactly one record, `https://ror.org/01rhff309`, which is the ROR
recorded above, and a nonsense-institute control returns zero. So a later refresh should not go
hunting: there is no identifier to record until ROR registers the centre. (If re-running this, note
that in the ROR v2 API `name`, `aliases` and `labels` do not exist at the top level — every form is
nested in a `names` array of `{value, types}` objects — so reading `name` yields `None` and an
existing record can look empty.)

**Two of the three author names are stored in a shorter form than the project's own writing, and
that has been adjudicated: the stored forms are retained deliberately, and no database-side change
is made.** It is set down as a settled decision so that a later refresh reads a judgement here
rather than an oversight.

The stored forms are the given/family pairs `Angeline` / `Burrell` and `Jone` / `Reistad`, while the
project writes both names with a middle initial. `AUTHORS.rst` line 4 gives "Angeline G. Burrell" and
line 6 "Jone P. Reistad"; `LICENSE` line 1 opens
"Copyright (c) 2017, Angeline G. Burrell (AGB) and Gareth Chisham (GC)"; and `docs/citing.rst` uses
the initialised citation style, with "Burrell, A. G., et al." at line 16 and the BibTeX author field
`{Burrell, A. G. and Chisham, G. and Reistad, J. P.}` at line 22. Both are valid renderings of the
same people — a middle initial is a citation-style choice, not a different person — and the stored
forms are retained because they are also how the other catalogue entries carrying these authors hold
them, so the catalogue stays internally consistent about who these authors are.

**The two cases are not alike against ORCID, and the difference must not be collapsed.** For Burrell,
ORCID `0000-0001-8875-9326` records given-names `Angeline` and family-name `Burrell` and carries no
other-names, so the stored form is that record's own structured name; the same record's credit
(published) name is "Angeline G. Burrell", which is ORCID's preferred display of that same structured
name. For Reistad, ORCID `0000-0003-3509-5479` records given-names `Jone Peter` as its primary name
and `Jone Reistad` only as an other-name, so the stored form matches a recorded other-name rather
than the primary. One sentence asserting that the stored form "is the ORCID record's own name" would
hold for Burrell and be false for Reistad, and that near-miss is precisely how a confident wrong
correction gets made later. **Gareth Chisham** needs none of this reasoning: ORCID
`0000-0003-1151-5934` records `Gareth` / `Chisham`, exactly as stored.

Should a later refresh nonetheless conclude that the initialled forms belong in the catalogue, that
is not a field update: a person's stored name is not writable through the metadata API, so it takes a
database-side change to a shared `Person` row. Burrell's row is referenced by several other catalogue
entries, so renaming it is a campaign-level action that has to be checked against every one of those
references rather than an OCBpy-scoped one.

The verification rule behind all of this is worth stating, because the sources disagree with each
other: `.zenodo.json`'s `creators` array writes "Jone Reistad" without the initial (line 34) while
writing "Angeline G. Burrell" with it (line 24). An author-name check that consults only the Zenodo
metadata will therefore miss a middle initial that the project's own author list and its citation
guide both carry, so such a check has to read `AUTHORS.rst`, `LICENSE`, `docs/citing.rst`,
`.zenodo.json` and the ORCID record together.

Considered and rejected: **Dominic Jodoin**. `AUTHORS.rst` lists him under `Contributors`, a heading
the project keeps separate from `Authors`; `.zenodo.json`'s `creators` array does not include him; and
his single commit in the repository's history is authored from a `travis-ci.com` address, i.e. a CI
integration commit. He is absent from the author side of every authoritative source, so he is not a
Field 6 author. Recorded here so a future union of author lists does not add him.

### 7. Software Name (MANDATORY)
- **Value:** OCBpy

The project's own name, spelled this way in `pyproject.toml` (`name = "ocbpy"` as the distribution
name), in the README heading, in the PyHC registry (`name: "OCBpy"`), and in the logo artwork. The
mixed-case form is the presentation spelling and the right one for a catalogue display name; the
lowercase `ocbpy` is the import and PyPI name.

### 8. Description (MANDATORY)
- **Value:** OCBpy is a Python module that converts between AACGM coordinates and a magnetic coordinate system that adjusts latitude and local time relative to the Open Closed field line Boundary (OCB), Equatorial Auroral Boundary (EAB), or both. This is particulary useful for statistical studies of the poles, where gridding relative to a fixed magnetic coordinate system would cause averaging of different physical regions, such as auroral and polar cap measurements. The coordinate system methodology is described in Chisham (2017). Boundaries must be obtained from observations or models for this coordinate transformation. Several boundary data sets are included within this package, including northern hemisphere boundaries from the IMAGE satellite, northern and southern hemisphere OCBs from AMPERE, and single-point boundary locations from DMSP.

Carried forward unchanged. It is the README's own Overview text, lightly reflowed into prose, and it
remains accurate at the pin: the README's opening paragraph, its "coordinate system is described
in:" pointer to Chisham (2017), its statement that "Boundaries must be obtained from observations or
models for this coordinate" transformation, and its list of the bundled IMAGE, AMPERE and DMSP
boundary sets all still read as described. (Both quotations are cut at the source's own line breaks.)

Two deliberate retentions. The misspelling **"particulary"** is the README's own spelling at the pin,
so the description is faithful to its source; correcting it here would silently diverge the catalogue
from the project's wording. And the description does not mention the boundary **models** added in
0.6.0/0.7.0 — that omission is worth noting for a future refresh, because the README's Overview does
not mention them either, so any addition would be new wording rather than a quotation of the source.
Since Field 8 is the author-facing prose a maintainer may have chosen, it is left as submitted rather
than rewritten to suit this refresh.

### 9. Concise Description (OPTIONAL)
- **Value:** A Python module that converts between AACGM coordinates and an adjustable magnetic coordinate system based on the location of the polar cap boundary.

Carried forward unchanged. Its source is the PyHC community registry entry, whose `description:` field
reads "A Python module that converts between AACGM coordinates and an adjustable magnetic coordinate
system based on the location of the polar cap" — the stored value adds the closing word "boundary",
which is a small improvement in accuracy (the grid is set by the boundary's location, not by the polar
cap as a region). Kept as stored; the divergence from the registry is recorded so it is not mistaken
for drift.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2018-02-19

Correct and corroborated twice over. This is the date of the project's **first release**: tag `0.1a1`
points at commit `da710a840e700e3e679c8dde7b6db4a16eb02a06`, whose author and commit dates are both
`2018-02-19 14:59:24 -0600` (2018-02-19 20:59:24 UTC). It is also the date the concept DOI was
registered: the DataCite record for `10.5281/zenodo.1179230` gives `created` and `registered` as
`2018-02-19T21:38:27.000Z`, about 39 minutes after the tag — the ordinary GitHub-to-Zenodo release
sequence.

Considered and rejected, so neither is re-proposed as a "correction": the first commit
`6424368b86f540c8e31d8a0f4f09ac9aca329faf` (2017-07-03, more than seven months before any release,
and the date GitHub reports as `created_at`), and the first version deposit `10.5281/zenodo.1217177` (`0.2b1`,
issued 2018-04-12, which is a later release than the one this date belongs to).

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

The DataCite records for the concept DOI and for every version deposit give `publisher` as `Zenodo`,
which is where the software is deposited and from which its DOIs are minted.

### 12. Version (RECOMMENDED)
- **Version Number:** 0.7.0
- **Version Date:** 2026-06-05
- **Version PID:** https://doi.org/10.5281/zenodo.20562260
- **Version Description:** This release provides support for Python 3.14, updates dependency usage, and introduces two new auroral boundary models.

The recorded release advances from `0.6.0` to `0.7.0`. Four independent sources agree on the number
and date:

- `pyproject.toml` line 7 is `version = "0.7.0"`.
- `Changelog.rst`'s newest section heads `0.7.0 (06-05-2026)`.
- Tag `0.7.0` points at the pinned commit; the GitHub release for that tag has `name` `v0.7.0` and
  `published_at` `2026-06-05T19:30:06Z`.
- The DataCite record for `10.5281/zenodo.20562260` has title `aburrell/ocbpy: v0.7.0`, `version`
  `0.7.0`, a single `Issued` date of `2026-06-05`, `IsVersionOf 10.5281/zenodo.1179230`, and
  `IsSupplementTo https://github.com/aburrell/ocbpy/tree/0.7.0`.

That last pair of relations — a `/tree/<tag>` supplement plus a deposit titled
`<owner>/<repo>: <release name>` matching a GitHub release whose `name` is `v0.7.0` — is the
signature of the GitHub–Zenodo integration, so this is an automatic release deposit rather than a
manual upload, and `20562260` is the authoritative version PID for 0.7.0.

The previously recorded PID `https://doi.org/10.5281/zenodo.16802585` was correct **for 0.6.0** (title
`aburrell/ocbpy: v0.6.0`, `Issued` 2025-08-11) and is superseded here only because the release it
identifies is superseded.

**The description is the release's own lead sentence**, on the governing principle that a version
description should assert what the source itself says rather than what a synthesis of adjacent
evidence could defensibly claim. Two independent publications of that sentence agree on it: the
GitHub release body for tag `0.7.0` opens with exactly this sentence, and the DataCite `Abstract` of
the deposit `10.5281/zenodo.20562260` opens with the identical sentence. It also covers all three
strands of the release — the new models, the dependency work, and the Python 3.14 support — rather
than only the most scientifically interesting one.

Considered and not determinative: a concise curator line in the house style. The 0.6.0 row that this
refresh supersedes carried a curator-written sentence rather than the release body
(`Added boundary models to the potential sources of boundary locations.`), and the matching 0.7.0
line would have been something like *"Added the Gussenhoven (1983) and CH-Aurora-2014 auroral
boundary models."* That is a defensible value, not a wrong one: it keeps the entry's established
voice and points straight at the scientifically significant change. It was set aside because it is a
synthesis of the changelog rather than a quotation of any source, and because it drops the Python
3.14 support the release itself leads with. Recorded here so a later refresh can see the alternative
was weighed rather than missed — and so that a refresh which decides house-style consistency
outweighs source fidelity knows exactly what it is changing.

Supporting facts about the release's content, independent of the wording recorded:
`Changelog.rst` under `0.7.0 (06-05-2026)` lists
`* ENH: Added the Gussenhoven (1983) model for the EAB` and
`* ENH: Added the CH-Aurora-2014 model for the OCB and EAB` alongside `* MAINT: Added support for
Python 3.14` and the removal of support for older `zenodo_get` versions.

Note for a future refresh: this field is many-to-many, and exactly one release row was attached when
this refresh began, which is the correct shape — two attached rows would be a defect to investigate
rather than a second version to keep.

### 13. Programming Language (RECOMMENDED)
- **Values:**
  - Python 3.x

**The criterion, stated so a later refresh inherits it rather than re-litigating it:** a language is
recorded when the repository contains source that implements the software's functionality in that
language. Data files, documentation, build and CI configuration, and generated artifacts do not count,
whatever their extension.

Applying it: the 124 tracked files at the pin comprise 34 `.py`, 23 `.rst`, 9 `.png`, 8 `.ocb`, 8
`.eab`, 6 `.md`, 4 `.yml`, 2 `.txt`, single `.toml`, `.json`, `.cfg`, `.cdf`, `.csv`, `.gif`, `.in`
and `.bat` files, a `Makefile`, a `.gitignore`, a `LICENSE`, and 19 extension-less ASCII fixtures under
`ocbpy/tests/test_data/`. Every implementation file is Python. The `.ocb` and `.eab` files are bundled
boundary *data*; `docs/make.bat` and `docs/Makefile` are Sphinx build wrappers, not software the user
runs.

So the single value is right, and it is right on a stated principle rather than by absence of
searching — the vocabulary would have admitted a mixed tree (it carries `IDL`, `MATLAB`, `Julia`, `C`,
`C++`, `Rust` and several Fortran editions), and this tree simply is not one.

`Python 3.x` is the correct granularity: `pyproject.toml` sets `requires-python = ">=3.10"` and
classifies 3.10 through 3.14, and the README states "This module currently supports Python version
3.10 - 3.14." The vocabulary distinguishes only `Python 2.x` from `Python 3.x`, so the supported-minor
range is recorded here as evidence rather than as a value.

### 14. Reference Publication (RECOMMENDED)
- **Value:** https://doi.org/10.1029/2018JA025877

This value is correct and this refresh leaves it as it stands. The paper is Burrell, Halford,
Klenzing, Stoneback, Morley, Annex, Laundal, Kellerman, Stansby and Ma, "Snakes on a Spaceship—An
Overview of Python in Heliophysics", *JGR: Space Physics*, issued 2018-12, resolved at Crossref.

**The deciding evidence is the project speaking about its own package.** `docs/citing.rst` says
"This package was first described in the python in heliophysics over article," and
"which may also be cited if a description of the package is desired." A description of the *package*
is exactly what this field asks for, and the project nominates this paper by name for that purpose.
(The missing "view" in "over article" is the source's own typo.) The paper demonstrably discusses
OCBpy: an ADS full-text query for `OCBpy` restricted to that paper's bibcode returns it, while a
nonsense-token and a nonsense-term control both return nothing and the bibcode filter alone returns
the paper — so the full text really is indexed and the hit is not an artifact. Its one weakness is
recorded here so it is not rediscovered later as an objection: it is a ten-author, multi-package
community survey, so it describes OCBpy in a section rather than being a paper about OCBpy.

There is no software paper of OCBpy's own to prefer instead. An ADS title search for `OCBpy` returns
only the package's own Zenodo release deposits, and the project's citation guide nominates no
dedicated software article.

**Considered and not determinative: `https://doi.org/10.1002/2016JA023235`** (Chisham, "A new
methodology for the development of high‐latitude ionospheric climatologies and empirical models",
*JGR: Space Physics*, issued 2017-01). The case for it is genuine and must not be mistaken for
something we overlooked: it is the method the code implements, `README.md` introduces it with
"coordinate system is described in:", `ocbpy/ocb_scaling.py`'s docstring cites it as reference [1],
and `ocbpy/boundaries/README.md` requires users of the IMAGE boundaries to cite it. Under a reading
of "the publication describing the software" as "the publication describing what the software does
and how", it is the closest thing OCBpy has to a method paper, and it is the value an earlier
extraction chose. It is not determinative because it predates the package and does not describe it:
it describes the coordinate-system methodology and a climatology built from it, and OCBpy — which
came later — is not mentioned in it. That paper is recorded in Field 27 instead, with its own
evidence, and it belongs there rather than here.

Worth knowing under either reading: the catalogue page renders this field under a "Reference
Publication" heading distinct from the related-publication list, so a reader sees which paper plays
which role and the split loses nothing from the record.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License

Byte-exact match for the controlled vocabulary row. The repository's `LICENSE` at the pin is a
three-clause BSD text — copyright line "Copyright (c) 2017, Angeline G. Burrell (AGB) and Gareth
Chisham (GC)", the two redistribution clauses, and a third clause beginning "Neither the name of
ocbpy nor the names of its contributors may be used to" that withholds the right to use the project
or contributor names to endorse derived products. GitHub's licence detection agrees
(`spdx_id: BSD-3-Clause`), `pyproject.toml` classifies `License :: OSI Approved :: BSD License` and
declares `license = {file = "LICENSE"}`, and the PyPI release metadata for `ocbpy` carries that same
three-clause text as its licence — so the artifact users actually install agrees with the repository.

**Durable rejected alternative — do not "correct" this field from the DOI record.** Every Zenodo
deposit checked (the concept DOI and the 0.6.0 and 0.7.0 version DOIs) carries `rightsList`
`BSD 1-Clause License` with `rightsIdentifier` `bsd-1-clause`, and the concept record's `rightsUri` is
`https://svnweb.freebsd.org/base/head/include/ifaddrs.h?revision=326823` — a FreeBSD header file page,
plainly not a licence document for this project. The upstream cause is visible in the repository:
`.zenodo.json` declares its licence as `"id": "bsd-license"`, an ambiguous identifier that the
deposit pipeline resolved to the 1-clause licence. The repository's `LICENSE` text governs, so the catalogue
value is right and the DOI metadata is wrong.

No **License URI** is recorded, and none should be proposed: the licence is stored as a reference to a
shared licence entry that carries its own URL, so there is no per-software URI to set. The SPDX page
`https://opensource.org/licenses/BSD-3-Clause` is good *evidence* for the choice of row and is cited
here for that purpose only.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Values:**
  - conversion
  - converting
  - coordinate conversion
  - coordinate systems
  - coordinate transformation
  - heliophysics
  - ionosphere
  - magnetic coordinates
  - magnetic field
  - magnetosphere
  - space
  - space physics
  - aacgm
  - ampere
  - aurora
  - auroral oval
  - coordinates
  - dmsp
  - field-line boundary
  - polar
  - polar cap
  - pysat
  - superdarn
  - supermag
  - thermosphere

Keywords are stored in lower case; the catalogue's display layer title-cases them, so comparisons here
are against stored spellings. The twelve values the record already carried — the first twelve above,
`conversion` through `space physics` — are kept. They derive **topically** from
`.zenodo.json`'s `keywords` array at the pin — the array DataCite serves as the deposit's `subjects` —
but that derivation is not a byte correspondence, and it is worth spelling out precisely, because this
field's own spelling rule below turns on exactly the distinction involved. The source array holds
**thirteen** strings, and reaching these twelve from those thirteen takes two kinds of change beyond
lower-casing:

- **Three hyphen→space respellings.** `coordinate-transformation`, `coordinate-systems` and
  `space-physics` are stored as `coordinate transformation`, `coordinate systems` and `space physics`.
  Those are *different strings*, not case variants — the very fact the "Spelling matters" paragraph
  below relies on.
- **One two-into-one collapse.** `space-physics` and `Space Physics` are two separate source strings
  that both land on the single stored `space physics`, which is why thirteen source strings yield
  twelve stored values.

Case differences are genuinely not part of this problem, because lookup is case-insensitive:
`Conversion`, `Coordinate Conversion`, `Converting`, `Magnetic Field`, `Space Physics` and
`Heliophysics` bind their lower-case stored forms exactly. The four remaining source strings —
`magnetic coordinates`, `space`, `ionosphere` and `magnetosphere` — are stored verbatim.

The thirteen added by this refresh — `aacgm` through `thermosphere` above — are the terms a user would
plausibly search for and would be glad to be brought here by, each anchored in the repository:

- `aacgm` — the input/output coordinate system throughout (`aacgmv2` calls in `_boundary.py`,
  `ocb_scaling.py`, `boundaries/dmsp_ssj_files.py`).
- `aurora`, `auroral oval`, `polar`, `polar cap` — the package docstring is "Auroral oval and polar cap
  normalised location calculation tools.", and `auroral oval` and `polar cap` are the authors' own
  declared keywords in `pyproject.toml`.
- `field-line boundary` — also an authors' `pyproject.toml` keyword, and the single most central
  concept in the package: the open–closed field line boundary is what the coordinate system is built
  around, named in the software's own description and in every boundary class.
- `coordinates`, `thermosphere`, `pysat` — also authors' own `pyproject.toml` keywords;
  `thermosphere` is additionally supported by `docs/overview.rst`'s MIT-system framing and by PyHC's
  `ionosphere_thermosphere_mesosphere` classification, and `pysat` by the shipped
  `ocbpy/instruments/pysat_instruments.py`.
- `supermag`, `superdarn`, `dmsp`, `ampere` — the four data programmes the package reads or ships
  boundaries from, named across `README.md` (which lists SuperMAG and SuperDARN Vorticity as supported
  datasets, and IMAGE, AMPERE and DMSP as boundary sources) and `ocbpy/boundaries/README.md` (which
  documents the AMPERE and IMAGE file formats).

**Spelling matters more than it looks.** Keyword lookup is case-insensitive and strips surrounding
whitespace, so a case variant binds an existing entry, but a hyphenation or spacing variant does not —
it creates a near-duplicate. Concretely, `coordinate systems` (spaced) is already recorded here, while
the GitHub topic form `coordinate-systems` (hyphenated) is a different string and would create a twin.
Ten of the thirteen additions above are given in the spelling that binds an entry the catalogue
already holds. The remaining three, `auroral oval`, `polar cap` and `field-line boundary`, are new
terms with no existing near-equivalent — `aurora` and `polar` are distinct concepts, not variants of
them — and their inclusion is deliberate: all three are the authors' own declared keywords, in the
authors' own spelling, and they name what this software is about more precisely than anything already
available.

**Rejected on that same ground: importing the repository's GitHub topic list verbatim.** The
repository carries nine topics, and all nine are accounted for here so that a later refresh
inheriting the list does not have to guess which were considered:

- `coordinates` — **taken**, as one of the additions above; the topic and the stored spelling agree.
- `ionosphere`, `space` — **already among the twelve kept values**, in the same spelling.
- `coordinate-systems`, `coordinate-transformation`, `magnetic-coordinates`, `space-physics` —
  **rejected as hyphenated twins.** Each names a concept this record already carries in spaced form
  (`coordinate systems`, `coordinate transformation`, `magnetic coordinates`, `space physics`), so
  adding one would not extend the record — it would give one concept a second, differently-spelled
  entry. Whether a given hyphenated spelling already exists in the catalogue or would be created
  fresh differs between these four and does **not** change the verdict: the objection is the duplicated
  concept, not the mechanics of the write.
- `magnetic` — **rejected as a fragment.** It is a bare adjective, subsumed by the stored
  `magnetic coordinates` and `magnetic field`, and it tells a searcher nothing on its own.
- `python` — **rejected as a language tag.** Field 13 records the implementation language, and as a
  search term it distinguishes nothing in a catalogue that is largely Python.

Also considered and rejected: `heliosphere` (a `pyproject.toml` keyword, but the software has no
heliospheric content — see Field 5), `image` (the IMAGE mission is a genuine association, but as a
bare keyword the string is dominated by "image" in the image-processing sense and would mislead
searchers; the association is carried precisely by Field 32's IMAGE observatory), and the generic
`observations`, `models`, `satellites`, `analysis`, `atmosphere` (author keywords that describe no
distinguishing property of this package).

### 17. Data Sources (OPTIONAL)
- **Values:**
  - Observatory/Mission-specific
  - Other

Both values are carried forward, and no new value in the vocabulary applies.

`Observatory/Mission-specific` is correct and is the value that pairs with Fields 31 and 32: the
package's readers are written for named programmes — `ocbpy/instruments/supermag.py` for SuperMAG,
`ocbpy/instruments/vort.py` for the SuperDARN vorticity product, and
`ocbpy/boundaries/dmsp_ssj_files.py` for DMSP SSJ — and the README lists exactly those, "SuperMAG
(available at http://supermag.jhuapl.edu)", "SuperDARN Vorticity (contact GC at gchi@bas.ac.uk)" and
"Any pysat Instrument (available at https://github.com/pysat/pysat)".

`Other` covers the two routes that fit no listed source: the Zenodo deposit from which DMSP SSJ
boundary files are downloaded, and data arriving as an already-loaded pysat `Instrument` object, where
the retrieval was pysat's rather than OCBpy's.

Considered and rejected:

- **HTTP/HTTPS Directories** — the DMSP SSJ retrieval is an HTTPS download, but it is keyed by DOI
  through `zenodo_get` against a Zenodo deposit and verified against that deposit's checksum file; it
  does not traverse an HTTP directory listing. A user filtering for software that pulls from web
  directories would not be looking for this.
- **CDAWeb**, **Madrigal**, **HAPI**, **OMNIWeb** and the other archive-specific sources — reachable
  *through* pysat, but OCBpy contains no client for any of them and never selects one. Attributing
  pysat's connectors to OCBpy would make the record wrong about what it supports. Madrigal is the case
  worth naming, because it is not merely reachable in principle: `docs/examples/ex_general.rst` loads a
  Madrigal-derived ASCII file and `docs/examples/ex_pysat_eab.rst` loads Madrigal vertical TEC through
  `pysatMadrigal`. Both are tutorial demonstrations in which the user, or pysat, does the retrieving —
  the kind of mention this field's guidance excludes — and the ASCII reading they exercise is already
  recorded in Field 18.

### 18. Input File Formats (RECOMMENDED)
- **Values:**
  - ascii
  - csv
  - Other

`ascii` and `Other` are carried forward; `csv` is added by this refresh.

- **ascii** — the dominant input. `ocbpy/instruments/general.py::load_ascii_data` is a general ASCII
  loader (`np.genfromtxt` with a header-line count, used by the SuperMAG and vorticity readers), the
  bundled `.ocb`/`.eab` boundary files are plain text with a documented column layout
  (`ocbpy/boundaries/README.md` specifies the IMAGE and AMPERE layouts field by field), and
  `load_supermag_ascii_data` and `load_vorticity_ascii_data` open their inputs in text mode.
- **csv** *(addition)* — `ocbpy/boundaries/dmsp_ssj_files.py` reads DMSP SSJ boundary files as
  comma-separated values: `data = np.loadtxt(infile, skiprows=skiprows, delimiter=',')`, over files
  matching `dmsp-fII_ssj_precipitating-electrons-ions_YYYYMMDD_vXXX_boundaries.csv` (the pattern is
  documented in `evaluate_dmsp_boundary_file`'s docstring, and a real example ships as a test fixture).
  This is a first-party reader for a distinct format and the record did not reflect it.
- **Other** — retained for input reaching the package through pysat, where the on-disk format is
  whatever that pysat instrument uses and OCBpy never sees it.

Considered and rejected: **CDF**. A CDF file is tracked in the tree
(`ocbpy/tests/test_data/dmsp-f16_ssj_precipitating-electrons-ions_20101231_v1.1.2.cdf`), which looks
like CDF support until it is checked. No module reads it. At the pin the literal string `.cdf`
occurs in exactly one line of any tracked file, and that line is the *CSV* fixture's own header
comment naming the CDF it was derived from; a wider case-insensitive search for `CDF` as a word adds
only that fixture's column comment ("row of DMSP SSJ CDF file corresponding to boundary"), the binary
fixture itself, and one stale comment in `ocbpy/tests/test_dmsp_ssj_files.py` whose test in fact
asserts on an "empty list of input CSV" error from `format_ssj_boundary_files`. No import of any CDF
library appears anywhere in the package. The history explains the leftover — CDF-reading
capability came from the third-party `ssj_auroral_boundary` package, whose dependent functions were
deprecated in 0.4.0 and, per `Changelog.rst` at 0.5.0, "* DEP: Removed deprecated functions that
depend on ssj_auroral_boundary package". At the pin `ssj_auroral_boundary` is imported by no module;
it survives only in the changelog, in one documentation example and in one test that checks the import
failure path. Recording CDF would claim a capability the package deliberately shed.

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - ascii

Newly populated by this refresh; before it the field held no value, and the earlier extraction
recorded "Not found" on the reasoning that the software "appears to primarily return transformed coordinates programmatically
rather than writing output files". That is true of the main API but not of the whole package: three
code paths write files, and all three write ASCII text.

- `ocbpy/instruments/supermag.py::supermag2ascii_ocb` opens its destination with
  `with open(outfile, 'w') as fout:` and writes a header and one text line per record; the function's
  name states the format.
- `ocbpy/instruments/vort.py::vort2ascii_ocb` does the same for the SuperDARN vorticity product.
- `ocbpy/boundaries/dmsp_ssj_files.py::format_ssj_boundary_files` opens four text destinations at once
  (poleward and equatorward, northern and southern) and writes the `.ocb`/`.eab` boundary files whose
  ASCII column layout is documented in `ocbpy/boundaries/README.md`.

Considered and rejected: **csv** as an output (the reformatting path reads CSV but writes the
space-delimited OCBpy boundary layout, not CSV), and **Other** (the `.ocb`/`.eab` files are ASCII text
in a documented column layout, so `ascii` already describes them; no output path produces a binary or
otherwise unlisted format). The pysat integration writes nothing — `add_ocb_to_data` assigns new
variables and metadata into the in-memory `Instrument`, leaving persistence to pysat.

Also considered and rejected: **netCDF3/4**. `docs/examples/ex_save_boundaries.rst` documents saving
boundary data as netCDF, but the split of labour matters: OCBpy's `to_dict(xarray_style=True)` returns
a dictionary, and the netCDF file is written by `xarray` in user code (`xr.Dataset(...).to_netcdf(...)`).
The package supports no netCDF writer of its own, so claiming the format here would overstate what it
generates. That export route is real and is recorded where it belongs, as the documented interchange
with xarray in Field 30.

### 20. Operating System (RECOMMENDED)
- **Values:**
  - Linux
  - Mac
  - Windows

Carried forward; still exactly right. `.github/workflows/main.yml` runs the test matrix on
`os: ["ubuntu-latest", "macos-latest", "windows-latest"]` across Python 3.10–3.14 and two dependency
configurations, so all three platforms are continuously verified rather than merely claimed.
`pyproject.toml` classifies `Operating System :: Unix`, `POSIX`, `POSIX :: Linux`,
`MacOS :: MacOS X` and `Microsoft :: Windows`.

Considered and rejected: `Operating System Independent`. It would be a defensible reading of a pure
Python package, but the project enumerates specific platforms in both its classifiers and its CI, and
the three concrete values tell a user more than the abstract one.

### 21. CPU Architecture (RECOMMENDED)
- **Values:**
  - CPU Independent

Pure Python with no compiled extension: `pyproject.toml` uses the `setuptools.build_meta` backend with
no extension modules, declares no architecture-specific dependency, and the CI matrix builds by plain
`pip install .` on all three runner architectures. Nothing in the package selects on architecture.

### 22. Related Phenomena (OPTIONAL)
- **Value:** Not found — correctly empty

This is an evidenced empty, not an unexamined gap. The `Phenomena` vocabulary is flat and consists of
`Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`,
`Solar Wind` and `X-ray emission`. Every one of those except `Geomagnetic Storms` is a solar or
heliospheric phenomenon that OCBpy has nothing to do with, and `Geomagnetic Storms` is the only
candidate worth arguing. It fails: the string "storm" does not occur anywhere in the tracked tree at
the pin, the software neither models nor identifies storms, and the geomagnetic dependence it does have is a boundary-model input
parameter (the AL index for Starkov, Kp for Gussenhoven, the Newell coupling function for
CH-Aurora-2014) rather than a phenomenon it studies. A user browsing storm-related software would find
it out of place.

The phenomena this software actually concerns — the auroral oval, the polar cap, the open–closed field
line boundary, auroral precipitation — have no rows in the vocabulary. Should any be added upstream,
this is the field that should be revisited first.

### 23. Development Status (RECOMMENDED)
- **Value:** Active

Newly populated by this refresh; before it the field held no value. `RepoStatus` rows carry
definitions, and `Active` is defined
as "The project has reached a stable, usable state and is being actively developed." Both halves hold
at the pin:

- *Stable, usable state* — `pyproject.toml` classifies `Development Status :: 5 - Production/Stable`,
  the project is on its ninth tagged release, and it is distributed on PyPI.
- *Actively developed* — release `0.7.0` was published 2026-06-05, which is also the date of the
  newest commit on `main`; the repository is not archived (`archived: false`) and not disabled; and,
  when checked on 2026-09-08, it had three open issues and no open pull requests.

Rejected alternatives, from the same definitions: `Inactive` ("no longer being actively developed")
and `Unsupported` ("the author(s) have ceased all work on it") are contradicted by the release published on
2026-06-05 — and note that `Unsupported`'s definition adds only that a new maintainer "may be
desired", a conditional that must not be read as a requirement. `Concept` and `WIP` require the
absence of a stable public release. `Moved` and `Abandoned` require an upstream statement that does
not exist.

One artifact a future refresh will meet again: GitHub's `pushed_at` for this repository is three days
later than the newest commit on `main`, because `origin/develop` sits one commit ahead of the pin while
being tree-identical to it (that commit merges `main` back into `develop`). `pushed_at` is not commit
activity on the default branch, and the extra commit changes no file.

### 24. Documentation (RECOMMENDED)
- **Value:** https://ocbpy.readthedocs.io/en/latest/

Carried forward and re-checked: the URL returned HTTP 200 on 2026-09-08. It is the project's declared documentation
home — `pyproject.toml` sets `documentation = "https://ocbpy.readthedocs.io/en/latest/"`, the README's
Overview links "Full [documentation](https://ocbpy.readthedocs.io/en/latest/)", a
Read-the-Docs build badge heads the README, and `.readthedocs.yml` configures the Sphinx build from
`docs/conf.py`. The PyHC registry gives the shorter `http://ocbpy.readthedocs.io`, which redirects to
the same site; the stored form is the explicit HTTPS `latest` URL and is preferable.

Considered and rejected: a repository wiki. GitHub reports `has_wiki: true` for this repository, but
that flag only means the wiki feature is enabled. A wiki lives in a separate Git repository, and
`git ls-remote https://github.com/aburrell/ocbpy.wiki.git` returns "Repository not found" — no wiki
content has ever been created, so there is nothing to record.

### 25. Funder (OPTIONAL)
- **Organization:** Office of Naval Research
- **Funder Identifier:** https://ror.org/00rk2pe57

Newly populated. Two independent sources name the same funder for the same person.

The repository states it directly: `AUTHORS.rst` carries an `Acknowledgements` block whose sole entry
reads "Angeline G. Burrell is supported by the Office of Naval Research" (with the parenthetical
"(2018-Present)" on the following line). That is the project's own attribution of support to its lead
author and maintainer, it names an organisation rather than an acronym, and it is recorded verbatim as
the funder name. The ROR `https://ror.org/00rk2pe57` is an active record whose display name is exactly
"Office of Naval Research" (acronym ONR).

The reference publication's Acknowledgements say the same thing in the Navy's own idiom:
"A.G. Burrell is supported by the Chief of Naval Research." — the Chief of Naval Research being the
officer who heads ONR. (The publisher's page returns 403 to plain fetches; the accepted manuscript of
the same paper, arXiv:1901.00143, carries the identical Acknowledgements section and is readable, which
is where this quotation and the ones below come from.) Between the two sources the repository's
organisation name is the better value for a funder field, so ONR is recorded rather than the officer's
title.

Considered and rejected, because that same paragraph is a textbook case of the tier conflation this
field's guidance warns about — and it attributes each item by name, so nothing has to be inferred:

- **U.K. Science and Technology Facilities Council** and the **U.S. Department of Energy** — the
  paragraph continues "D. Stansby is supported by the U.K. Science and Technology Facilities Council
  studentship ST/N504336/1." and credits S.K. Morley's contributions to the U.S. Department of Energy
  with Laboratory Directed Research and Development grant 20170047DR. Both fund *other* co-authors of
  a ten-author community survey, not OCBpy.
- **National Aeronautics and Space Administration** — NASA appears in the same section, but not as a
  funder of anything: "We acknowledge use of NASA/GSFC’s Space Physics Data Facility’s OMNIWeb service
  and OMNI data by many of these Python packages". That is a data-service acknowledgement on behalf of
  the surveyed packages collectively, and OCBpy is not among the packages that use it — it retrieves
  no OMNI data, and every geomagnetic index its models need (Kp, AL, the Newell coupling function) is
  a function argument the user supplies.

### 26. Award Title (OPTIONAL)
- **Value:** Not found
- **Award Number:** Not found

No award title or number exists for this software in any source consulted, and the strongest evidence
for that is the same Acknowledgements paragraph quoted in Field 25: it gives award numbers for two of
the paper's other authors (studentship ST/N504336/1 and grant 20170047DR) and gives none for
A.G. Burrell, whose support it states without an identifier. `AUTHORS.rst` matches, describing
continuing support ("2018-Present") rather than a specific award — the normal shape of United States
Navy in-house base funding for a government laboratory employee. Neither the DataCite records for the
concept and version DOIs nor `.zenodo.json` carries any funding or award element, and no award number
appears anywhere in the tracked tree.

So this is a documented absence, not an unsearched field, and the two award numbers that do exist
nearby belong to other people and must not be attached here. Fields 25 and 26 are separate nested
groups, so the funder above stands without an award; and since an award entry cannot exist without a
title, nothing should be invented to carry it.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Values:**
  - https://doi.org/10.1002/2016JA023235
  - https://doi.org/10.5194/angeo-38-481-2020
  - https://doi.org/10.1002/2015JA021680
  - https://doi.org/10.1002/2016JA023342
  - https://doi.org/10.1029/2022JA030622
  - https://doi.org/10.1029/JA088iA07p05692
  - https://doi.org/10.5194/angeo-32-623-2014

**The bar applied, stated so it can be checked and inherited:** a publication belongs here when the
package's own code or data documentation rests on it — the article describes a method OCBpy implements,
or supplies a criterion the code applies by default — or when the publication describes or uses the
software. Publications that describe only the *instruments* that produced the bundled boundaries are
excluded, because Fields 31 and 32 carry those associations, and publications that describe the
*datasets* are excluded because Field 28 carries those. Applying one bar to incumbents and candidates
alike:

Already in the record before this refresh, and both pass:

- `10.1002/2016JA023235` — Chisham (2017), "A new methodology for the development of high‐latitude
  ionospheric climatologies and empirical models", *JGR: Space Physics*. The coordinate-system method
  the package implements; cited as reference [1] in `ocbpy/ocb_scaling.py`, introduced in `README.md`
  with "coordinate system is described in:", and required by `ocbpy/boundaries/README.md` for
  users of the IMAGE boundaries. It stays in this field rather than moving up to Field 14: that field
  records the paper the project nominates as describing the package, and this one predates the package
  and does not describe it (the reasoning is set out in Field 14).
- `10.5194/angeo-38-481-2020` — Burrell, Chisham, Milan, Kilcommons, Chen, Thomas and Anderson (2020),
  "AMPERE polar cap boundaries", *Annales Geophysicae*. The AMPERE OCB derivation and its correction
  method, cited as reference [4] in `ocbpy/ocb_correction.py`, whose `elliptical` and `harmonic`
  functions implement that correction.

Added by this refresh, each with its code anchor:

- `10.1029/2022JA030622` — Chisham, Burrell, Thomas and Chen (2022), "Ionospheric Boundaries Derived
  From Auroral Images", *JGR: Space Physics*. Reference [6] in `ocbpy/ocb_correction.py`, and the
  source of a code default: `ocbpy/boundaries/README.md` explains that the boundary-quality selection
  now uses `R_MERIT`, "with recommended merit values documented in Chisham" et al. (2022), and states
  that those ranges are the defaults in `OCBoundary.get_next_good_ocb_ind`. The package's data
  documentation instructs users to cite either Chisham (2017) or this paper when using the IMAGE
  boundaries.
- `10.1002/2016JA023342` — Kilcommons, Redmon and Knipp (2017), "A new DMSP magnetometer and auroral
  boundary data set and estimates of field‐aligned currents in dynamic auroral boundary coordinates",
  *JGR: Space Physics*. Reference [5] in `ocbpy/boundaries/dmsp_ssj_files.py`: the boundary
  identification method behind the DMSP SSJ files that module downloads and reformats, and a required
  citation in `docs/citing.rst`.
- `10.1002/2015JA021680` — Milan, Carter, Korth and Anderson (2015), "Principal component analysis of
  Birkeland currents determined by the Active Magnetosphere and Planetary Electrodynamics Response
  Experiment", *JGR: Space Physics*. Supplies a code default for the bundled AMPERE boundaries:
  `ocbpy/boundaries/README.md` states that certain `J_MAG` ranges should not be trusted, that the
  limitation "is explained in Milan et al. (2015), doi:10.1002/2015JA021680." and that this range is
  the default in `OCBoundary.get_next_good_ocb_ind`.
- `10.5194/angeo-32-623-2014` — Xiong and Lühr (2014), "An empirical model of the auroral oval derived
  from CHAMP field-aligned current signatures – Part 2", *Annales Geophysicae*. Reference [11] in
  `ocbpy/boundaries/models.py` and the article that defines the CH-Aurora-2014 model implemented there
  (the module's `em` argument is documented as "The time-integrated Newell Coupling Function, as
  described in Equation 2" of reference [11]).
- `10.1029/JA088iA07p05692` — Gussenhoven, Hardy and Heinemann (1983), "Systematics of the equatorward
  diffuse auroral boundary", *JGR*. Reference [9] in `ocbpy/boundaries/models.py`, implemented as
  `gussenhoven_equatorward_auroral_boundary` and added in 0.7.0.

Considered and rejected, with reasons — this is the set most at risk of being re-proposed:

- **Starkov (1994), "Mathematical model of the auroral boundaries", *Geomagnetism and Aeronomy*
  (English Translation) 34(3), 331–336** — reference [8] in `ocbpy/boundaries/models.py` and
  implemented as `starkov_auroral_boundary`, so it passes the bar on substance but **cannot be
  recorded: it has no DOI and no permanent landing page.** A title search of ADS for
  "Mathematical model of the auroral boundaries" returns nothing, and the only Starkov record in that
  journal's volume 34 is a different 1994 article (bibcode `1994Ge&Ae..34...36S`, no DOI). The control
  query for a paper known to be indexed returns it, so the search instrument works. Field 27 accepts
  only URLs, so this article is documented here instead. If it is ever indexed, it qualifies.
- **Umbach and Jones (2003), "A few methods for fitting circles to data"** (`10.1109/TIM.2003.820472`)
  — reference [10] in `ocbpy/boundaries/models.py`, used by `circle_fit`. Rejected as a general
  numerical-methods article in an instrumentation journal: it tells a heliophysics user nothing about
  this software, and would be equally at home in the bibliography of any curve-fitting package.
- **Shepherd (2014), "Altitude‐adjusted corrected geomagnetic coordinates"**
  (`10.1002/2014JA020264`) — reference [3] in `ocbpy/_boundary.py`, and the definition of the AACGM
  coordinate system OCBpy converts to and from. Rejected because it is the reference publication of
  the **AACGMv2** catalogue entry, which holds exactly this DOI in that role; OCBpy reaches it through
  Fields 29 and 30, and duplicating a dependency's bibliography here would blur that structure.
- **Mende et al. (2000), "Far ultraviolet imaging from the IMAGE spacecraft" parts 2 and 3**
  (`10.1023/A:1005227915363`, `10.1023/A:1005292301251`) and **Waters, Anderson and Liou (2001)**
  (`10.1029/2000GL012725`) — cited by `docs/citing.rst` and `ocbpy/boundaries/README.md` as the
  instrument and technique descriptions for the bundled IMAGE and AMPERE boundaries. Rejected as
  instrument papers: no code rests on them, and the associations they represent are carried by
  Field 31 (IMAGE FUV) and Field 32 (IMAGE, AMPERE).
- **Xiong et al. (2014) Part 1** (`10.5194/angeo-32-609-2014`) — listed in `docs/citing.rst` beside
  Part 2, but it describes the CHAMP FAC data used to *adjust* the model rather than the model the code
  implements, and it is not in the module's own reference block. Part 2 carries the model.
- **Papers that use OCBpy.** Several exist, and the full-text index will keep finding more; the field
  definition asks for publications "that the software developer prioritizes", and the developer's own
  citation guide nominates none of them. Selecting a few from a changing index would be arbitrary and
  would need maintenance forever, so the field is built from the project's own documentation instead.
  ("Snakes on a Spaceship" is the one paper the developer does nominate, and it is recorded as the
  reference publication in Field 14.)

### 28. Related Datasets (OPTIONAL)
- **Values:**
  - https://doi.org/10.5281/zenodo.3373812
  - https://www.bas.ac.uk/project/image-auroral-boundary-data/
  - https://doi.org/10.5285/8EEDC594-730B-4AAD-B9CE-827912320C3A
  - https://doi.org/10.5285/fa592594-93e0-4ee1-8268-b031ce21c3ca
  - https://doi.org/10.25392/leicester.data.22241338.v3

Field 28 is for datasets the software supports. For OCBpy that has an unusually crisp meaning: every
boundary file it ships or downloads comes from one of three published datasets — the IMAGE, AMPERE and
DMSP SSJ boundary sets — and its vorticity reader is written for a fourth.

Already in the record before this refresh, and both kept:

- `10.5281/zenodo.3373812` — Kilcommons, Redmon and Knipp (2019), "Defense Meteorology Satellite
  Program (DMSP) Electron Precipitation (SSJ) Auroral Boundaries, 2010-2014". The dataset
  `ocbpy/boundaries/dmsp_ssj_files.py` downloads; cited as reference [7] in that module and in
  `docs/citing.rst`, and linked from the README as "DMSP SSJ Boundaries". Note for a future refresh:
  the module's own `doi` default is the neighbouring `10.5281/zenodo.3373811` (the concept DOI of the
  same deposit), while the README, the citation guide and this field use the version DOI `…3812`. Both
  identify the same data; the version DOI is what the authors ask users to cite.
- `https://www.bas.ac.uk/project/image-auroral-boundary-data/` — the BAS project page the README links
  as "IMAGE Auroral Boundary data". Kept because it is the project's own pointer and is the portal a
  reader would want, even though it is a landing page rather than a dataset DOI.

Added by this refresh, each verified to resolve:

- `10.5285/8EEDC594-730B-4AAD-B9CE-827912320C3A` — Chisham (2023), "Ionospheric vorticity across the
  northern hemisphere ionosphere determined from particular SuperDARN radar pairs - 2000 to 2005
  inclusive", NERC EDS UK Polar Data Centre. This is the dataset `ocbpy/instruments/vort.py` exists to
  read: the module's docstring cites it by name and DOI, and its `Notes` describe a "Specialised
  SuperDARN data product, available from the British Antarctic Survey." Resolved through DataCite (the
  DOI is a DataCite/NERC registration and is absent from Crossref, as expected).
- `10.5285/fa592594-93e0-4ee1-8268-b031ce21c3ca` — Chisham (2022), "Ionospheric boundaries derived
  from IMAGE satellite mission data (May 2000 - October 2002) - VERSION 2.0", NERC EDS UK Polar Data
  Centre. The published, citable form of the IMAGE boundary data shipped as
  `ocbpy/boundaries/image_north_circle.ocb`/`.eab` and the SI12/SI13/WIC files; `docs/citing.rst`
  lists it among the required IMAGE citations. It complements rather than replaces the BAS project
  page above: the page is the portal, this is the versioned dataset.
- `10.25392/leicester.data.22241338.v3` — Milan (2023), "AMPERE R1/R2 FAC radii v2", University of
  Leicester. The source of the bundled AMPERE boundaries: `ocbpy/boundaries/README.md` states that
  "These boundaries were obtained from Milan (2023)" and asks users to cite that data source, and
  `docs/citing.rst` gives this DOI.

Considered and rejected: the AACGM coefficient data distributed with the `aacgmv2` dependency (it is
that package's, and OCBpy's relation to it is recorded in Fields 29 and 30), and the SuperMAG
data holdings (the reader supports them, but SuperMAG distributes data through a request interface
under its own rules rather than as a citable dataset with a DOI; the association is carried by
Fields 31 and 32).

### 29. Related Software (OPTIONAL)
- **Values:**
  - https://github.com/aburrell/aacgmv2
  - https://github.com/pysat/pysat

Both relations pre-date this refresh, and both survive review on their merits; what this refresh
changes is the URL form. Because this field replaces its whole list rather than merging into it, the
complete outgoing list is recorded here in its exact previous form, so a later reader can see what
was there:

- `https://doi.org/10.5281/zenodo.3598705` — `aburrell/aacgmv2: Version 2.6.0`, issued 2020-01-06
- `https://doi.org/10.5281/zenodo.15059161` — `pysat/pysat: v3.2.2`, issued 2025-03-20

Neither was wrong about which software was meant, but both were **version-specific release
deposits**: each pinned the relation to one old release, and neither matched the identifier of the
corresponding catalogue entry (AACGMv2's is `10.5281/zenodo.1212694`, pysat's is
`10.5281/zenodo.1199703`), so a reader following either one landed on a release deposit rather than
on the related software.

**The repository URL is the right value for a relation to another catalogue entry**, and that is the
settled choice here. A related item is displayed as its raw URL, so the URL *is* the visible link
text: `https://github.com/pysat/pysat` reads as *pysat* to a visitor, whereas
`https://doi.org/10.5281/zenodo.15059161` reads as nothing at all. Each value used here is the exact
`code_repository_url` its target entry stores, so the relation points at the entry the reader expects
to reach.

The reverse condition, recorded so a later refresh can re-derive this choice instead of
re-litigating it: **if the catalogue ever rendered resolved titles rather than raw URLs, the DOI
would win** — legibility would no longer be at stake and a DOI's persistence across repository moves
and renames would be the stronger property. The choice rests on how the value is displayed, not on
DOIs being unsuitable.

Why each package qualifies:

- **aacgmv2** — the required runtime dependency (`pyproject.toml` lists `"aacgmv2>=2.7.1"` and
  `"numpy"` under `dependencies`) and a domain-specific one: it implements the AACGM-v2 magnetic
  coordinate system that is the input and output coordinate system of everything OCBpy does. It is called directly in three
  modules (`_boundary.py`, `ocb_scaling.py`, `boundaries/dmsp_ssj_files.py`). "Important dependency"
  is meant literally, and this is one.
- **pysat** — an optional dependency (`pysat_instruments = [ "pysat>=3.2.1" ]`) for which the package
  ships a dedicated integration module, `ocbpy/instruments/pysat_instruments.py`, and a documentation
  example. A companion relationship of exactly the kind this field describes.

Considered and rejected:

- **numpy** — a required dependency, and excluded on principle: it is generic scientific
  infrastructure, equally at home in a web application or a finance model, and saying OCBpy depends on
  it distinguishes nothing.
- **zenodo_get** (`https://github.com/dvolgyes/zenodo_get`) — the optional `dmsp_ssj` dependency
  (`zenodo-get>=2.0.0`) that performs the DMSP boundary download. Excluded by the same test: it
  downloads records from Zenodo for any purpose whatsoever and is domain-agnostic plumbing.
- **ssj_auroral_boundary** (`https://github.com/lkilcommons/ssj_auroral_boundary`) — a former
  dependency that computed DMSP SSJ boundaries locally; the functions depending on it were deprecated
  in 0.4.0 and removed in 0.5.0, and the package now downloads pre-computed boundaries instead. It is
  still named in `docs/examples/ex_dmsp.rst`. Excluded because the dependency no longer exists at the
  pin, and it is neither a predecessor of OCBpy nor a fork parent — the relation that does persist is
  to the *dataset* its authors published, which Field 28 records.
- **ApexPy** — performs a comparable job (geodetic-to-magnetic coordinate conversion in a different
  system) and is in the catalogue. Excluded because the repository never refers to the package. The
  word "apex" occurs once in the whole tree, in `ocbpy/boundaries/models.py`, where the
  CH-Aurora-2014 boundary is documented as being returned in apex geomagnetic coordinates — a remark
  about that model's native coordinate system, not a relation to ApexPy, and worth knowing on its own
  since every other boundary in the package is expressed in AACGM. Beyond that, "converts between
  magnetic coordinate systems" is a similarity so broad that it would pull in a whole family of
  packages while telling a reader nothing specific about OCBpy; the coordinate-conversion relation
  that *is* specific to this software is aacgmv2, recorded above.
- **pyDARN** — excluded *from this field* because it performs a different job (reading and plotting
  SuperDARN data) and is not a dependency of any kind. It is not excluded from the record: OCBpy's own
  vector example imports SuperDARN grid records through pydarn, which is a demonstrated exchange, so
  it belongs in Field 30 and is recorded there.

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - https://github.com/aburrell/aacgmv2
  - https://github.com/SuperDARN/pydarn
  - https://github.com/pydata/xarray
  - https://github.com/pysat/pysat

The pysat relation pre-dates this refresh; its URL form changes for the same reason as in Field 29,
the outgoing value being `https://doi.org/10.5281/zenodo.15059161`, the v3.2.2 release deposit. The
demonstrated exchange is concrete and first-party: `ocbpy/instruments/pysat_instruments.py::add_ocb_to_data` takes a loaded
pysat `Instrument`, reads its magnetic latitude, local time and height variables, computes
boundary-relative coordinates and scaled vector components, and assigns them back into the instrument
with `pysat_inst.data.assign(**set_data)`; `add_ocb_to_metadata` writes matching entries into
`pysat_inst.meta` using pysat's own metadata labels. It handles both of pysat's data models — there
are distinct code paths for `pysat_inst.pandas_format` and for the xarray-backed case — and the
integration is exercised by `ocbpy/tests/test_pysat.py` and documented in
`docs/examples/ex_pysat_eab.rst`. This is a plugin-style adapter, not a shared runtime.

**aacgmv2 is recorded here as well as in Field 29.** The exchange is a coordinate-system one and it runs in both
directions inside the public API: OCBpy accepts geodetic or geographic input and converts it with
`aacgmv2.get_aacgm_coord_arr` before locating it relative to a boundary, and converts back with
`aacgmv2.convert_latlon_arr` and `aacgmv2.convert_mlt` when a user asks for output in other
coordinates; the bundled boundary files are themselves expressed in AACGM coordinates, so the two
packages share a data model rather than merely coexisting. `docs/examples/ex_vector.rst` shows a user
calling `aacgmv2.convert_mlt` to prepare input for OCBpy, which is the interoperation seen from the
user's side. Two further reasons to record it: the AACGMv2 catalogue entry names OCBpy in its own
interoperable-software list, so before this refresh the catalogue recorded this relation in one
direction only, and a reader arriving from that page and finding no reciprocal link would reasonably
conclude the relation had been withdrawn.

**pydarn is recorded on a documented data handoff.** The exchange is one package's output imported into the other,
and OCBpy's own documentation is where it happens: `docs/examples/ex_vector.rst` reads a SuperDARN
grid file with `pydarn.SuperDARNRead(filename)` and `read_grid()`, then passes those grid records
straight into `ocbpy.ocb_scaling.VectorData` — `grd_data[0]['vector.mlat']` as the latitude,
`grd_data[0]['vector.mlon']` converted to magnetic local time, and `vector.kvect` with
`vector.vel.median` resolved into north and east components — for boundary-relative gridding and
scaling. That is the whole worked
example for vector data, not an incidental mention, and pydarn is the named reader for it. The URL is
the exact repository URL the pyDARN catalogue entry stores.

**xarray is recorded on a documented interchange** rather than on
dependency presence — which it does not even have, since OCBpy declares no xarray requirement. All
three boundary classes expose `to_dict(xarray_style=False)` in `ocbpy/_boundary.py`, and
`docs/examples/ex_save_boundaries.rst` — the page titled "Export and Save Boundaries" — states that
the dictionary "may be formatted to allow the creation of an :py:class:`xarray.Dataset`" and then does
exactly that: `dual_data, dual_info = dual.to_dict(xarray_style=True)` followed by
`dual_dataset = xr.Dataset(dual_data, attrs=dual_info)`. Both output styles are exercised in the test
suite (`test_boundary_ocb.py` and `test_boundary_dual.py` iterate over `xarray_style=True/False`). So
an `xarray`-shaped dictionary is a first-party, documented export format of the public API, which is
the standard this kind of foundational-but-domain-adjacent package has to meet.

All four packages appear in Field 30, and two of them — aacgmv2 and pysat — appear in Field 29 as
well. That overlap is deliberate rather than a duplication error: Field 29's remit explicitly includes
important domain-specific dependencies, and those two are exactly that, while Field 30 asks for a
demonstrated exchange, which all four have. It follows from OCBpy declaring only two dependencies
beyond numpy, both of them peer heliophysics tools it integrates with rather than infrastructure it
merely consumes.

Considered and rejected:

- **numpy** — Tier A generic infrastructure. Never eligible, on any evidence.
- **zenodo_get** and **matplotlib** — domain-agnostic plumbing, and a plotting library that appears
  only in documentation examples written by the user.
- **Radar Software Toolkit (RST)** — named in `docs/examples/ex_vector.rst` as how the example's
  SuperDARN grid file was produced ("FitACF v3.0 was used", the example says, to make it). Rejected because that
  is upstream data preparation, not an exchange with OCBpy: the file reaches OCBpy through pydarn,
  which is the entry recorded above.

On URL form: pydarn's value is the exact repository URL the pyDARN catalogue entry stores, for the
same legibility reason set out in Field 29 (which also records the condition under which a DOI would
be the better value instead). xarray is not a catalogue entry, so there is no stored URL to match;
its concept DOI is `https://doi.org/10.5281/zenodo.598201` and would also be a valid value, but the
repository URL is used for consistency with the other three and because it reads as the package's
name where the raw URL is the visible link text.

### 31. Related Instruments (OPTIONAL)
- **Values:**
  - DMSP/F16, SESS Special Sensor Precipitating Electron and Ion Spectrometer 5, SESS/SSJ5 — https://spase-metadata.org/SMWG/Instrument/DMSP_5D-3/F16/SESS/SSJ5
  - DMSP/F17, SESS Special Sensor Precipitating Electron and Ion Spectrometer 5, SESS/SSJ5 — https://spase-metadata.org/SMWG/Instrument/DMSP_5D-3/F17/SESS/SSJ5
  - DMSP/F18, SESS Special Sensor Precipitating Electron and Ion Spectrometer 5, SESS/SSJ5 — https://spase-metadata.org/SMWG/Instrument/DMSP_5D-3/F18/SESS/SSJ5
  - Far Ultraviolet Imager — https://spase-metadata.org/SMWG/Instrument/IMAGE/FUV
  - SuperDARN Radars — https://spase-metadata.org/SMWG/Instrument/SuperDARN/Radars
  - SuperMAG Magnetometers — https://spase-metadata.org/SMWG/Instrument/SuperMAG/Magnetometers

Each name above is copied verbatim from its controlled-vocabulary row and each carries its SPASE
identifier, which is the reliable key for this field; a bare name is never a valid value here.

Four of the six pre-date this refresh, and all four are correct and evidenced:

- The three **DMSP SSJ5** rows match the code exactly. `ocbpy/boundaries/dmsp_ssj_files.py` sets
  `known_sats = [16, 17, 18]` and rejects any other satellite number, so F16, F17 and F18 are the
  supported platforms — not a guess among the DMSP flight models but an enumeration read from the
  source.
- **Far Ultraviolet Imager** (IMAGE FUV) is the instrument behind the bundled IMAGE boundary files.
  It also, usefully, covers all three of them: the package ships `si12_north_circle`,
  `si13_north_circle` and `wic_north_circle` boundary files, and `ocbpy/boundaries/README.md`
  attributes them to the "Spectrographic Imager SI12", "Spectrographic Imager SI13" and "Wideband
  Imaging Camera (WIC)". No finer vocabulary row exists for any of them: a word-anchored,
  case-insensitive sweep of every instrument and observatory row, across all four of their text
  columns (`name`, `abbreviation`, `identifier`, `definition`), finds no match for `SI12` or `SI13`
  and exactly one match for `WIC` — the FUV row itself, matched through its definition text,
  which names the Wideband Imaging Camera and the Spectrographic Imager as its channels. So the FUV row
  is the correct and complete representation of the three, and a future refresh should not go looking
  for per-channel rows.

The two this refresh added are both first-party readers rather than incidental mentions:

- **SuperMAG Magnetometers** — `ocbpy/instruments/supermag.py` is a dedicated SuperMAG reader
  (`load_supermag_ascii_data`, `supermag2ascii_ocb`), the README lists "SuperMAG (available at
  http://supermag.jhuapl.edu)" among the supported datasets, and `docs/supported_datasets.rst` gives it
  its own section. A user working with SuperMAG data would reach for this, and a user browsing the
  SuperMAG magnetometers would be unsurprised to find it.
- **SuperDARN Radars** — `ocbpy/instruments/vort.py` reads the SuperDARN ionospheric vorticity product
  derived from radar pairs, and the README lists "SuperDARN Vorticity" among the supported datasets.
  The SuperDARN *observatory* row is recorded in Field 32; carrying the instrument row alongside it
  completes the association at the level a radar-data user would search.

Considered and rejected:

- **The individual SuperDARN station rows** — the vocabulary also carries per-station IUGONET rows
  (Hokkaido East and West, King Salmon, Syowa East and South). Rejected because nothing in the
  repository names which radars contribute: the vorticity product is derived from "particular
  SuperDARN radar pairs" across the northern hemisphere, and enumerating stations would be invention.
  The programme-level row above is the honest granularity. One station *is* named anywhere in the
  project — `docs/examples/ex_vector.rst` works through a file from PGR, "a Canadian radar" — and it
  is a worked example rather than a supported station. It also carries a trap worth recording: the
  vocabulary has no SuperDARN PGR row at all, and a search for "Prince George" instead returns THEMIS
  ground magnetometer and all-sky-imager rows plus a ground station code, none of which is this radar.
  A future refresh must not bind the example's radar to any of them.
- **CHAMP instruments** (`SMWG/Instrument/CHAMP/FGM` and its siblings) — the CH-Aurora-2014 model
  implemented in `ocbpy/boundaries/models.py` was *derived from* CHAMP field-aligned-current
  signatures, and its `obs_colat` argument is documented as "CHAMP, or other, boundary observation
  co-latitudes". Rejected because OCBpy reads no CHAMP data and parses no CHAMP format: the observation
  enters as a co-latitude the user has already computed. Someone browsing CHAMP instruments for
  software that handles CHAMP data would find this out of place.

### 32. Related Observatories (OPTIONAL)
- **Values:**
  - Active Magnetosphere and Planetary Electrodynamics Response Experiment — https://spase-metadata.org/SMWG/Observatory/AMPERE
  - Defense Meteorological Satellite Program — https://spase-metadata.org/SMWG/Observatory/DMSP
  - Imager for Magnetopause-to-Aurora Global Exploration — https://spase-metadata.org/SMWG/Observatory/IMAGE
  - SuperDARN — https://spase-metadata.org/SMWG/Observatory/SuperDARN
  - SuperMAG — https://spase-metadata.org/SMWG/Observatory/SuperMAG

Names copied verbatim from their vocabulary rows, each with its SPASE identifier.

Four of the five pre-date this refresh and all four are correct. **AMPERE** and **IMAGE** are the
sources of boundary files shipped inside the package (`amp_north_radii`/`amp_south_radii` and the IMAGE circle files,
attributed in `ocbpy/boundaries/README.md`); **DMSP** is the platform whose SSJ boundaries the package
downloads and reformats; and **SuperDARN** is the source of the vorticity product
`ocbpy/instruments/vort.py` reads. AMPERE is correctly an observatory-level association rather than an
instrument one — its SPASE identity exists only under `SMWG/Observatory/`.

**SuperMAG** is recorded for the same reason as its instrument row in Field 31: a dedicated
first-party reader plus an explicit listing in the README's supported datasets. Carrying the
observatory alongside the instrument matches how the other supported programmes are represented here.

Considered and rejected: **CHAMP** (`SMWG/Observatory/CHAMP`), for the reason given in Field 31 — the
software implements a model derived from CHAMP data without ever reading CHAMP data. Also rejected: the
per-station SuperDARN observatory rows, on the same evidence grounds as their instrument counterparts.

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/aburrell/ocbpy/3ced0dec8cabf055b9e0a75a5eb1a57c017740be/docs/figures/ocbpy_logo.gif

Correct as recorded, and verified rather than assumed. Fetching the URL on 2026-09-08 returned HTTP 200 with
`content-type: image/gif` and 20,968 bytes, and those bytes are identical to the blob at
`docs/figures/ocbpy_logo.gif` in the pinned tree (SHA-256
`e25e20e9aebc42d9d005de03477a76755c7f8aceedc4e70d8c79b3c80cd1906a`). The file is a 400×400 GIF89a
image and is not Git-LFS-tracked (the pinned tree carries no `.gitattributes`), so the raw-content URL
serves the image itself rather than a pointer.

The image is a genuine project logo, not an example figure: a blue planet showing the auroral oval,
with a blue python arching over it and a gold python crossing it, and the wordmark "OCBpy". The
project's own README describes it with the alt text "Planet with auroral oval and two pythons
representing closed and open magnetic field lines" and the title "OCBpy Logo", and
`docs/overview.rst` displays it as the documentation banner.

The URL is pinned to a 40-hex commit SHA, with no branch name and no `blob/` segment, and is 117
characters long. Both sources that publish this logo give an unpinned `main`-branch URL instead — the
README's `<img src>` and the PyHC registry's `logo:` field — and the pinned form is deliberately
preferred: a branch URL breaks silently if the file is renamed, moved or deleted, and the catalogue has
no way to notice. The counter-argument that a branch URL would always serve the current artwork is
rejected on purpose: a logo redesign is a change a metadata refresh should notice and record
deliberately, not one the catalogue should inherit silently.
