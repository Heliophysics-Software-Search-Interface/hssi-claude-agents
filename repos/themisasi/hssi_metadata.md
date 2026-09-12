# HSSI Metadata Extraction Results

**HSSI Software ID:** 1d43d4b3-1562-4ccc-9729-49d31aa5309e
**Repository:** https://github.com/space-physics/themisasi
**Source Revision:** 397b9506cc3a82f4f53a0ea2c6f602e46cff2153
**Extraction Date:** 2026-09-12
**Validation Date:** 2026-09-12
**Validation Status:** PASS

---

## Scope note — how to read the evidence in this file

`themisasi` is a small, single-author Python package (38 tracked files at the pinned revision) that
reads, calibrates, projects and plots ground-based all-sky imager video from the THEMIS Ground-Based
Observatory network. It has no CITATION.cff, no `.zenodo.json`, no `codemeta.json` and no AUTHORS
file — none of those has ever existed anywhere in the pinned revision's ancestry — so almost every
field here is grounded in the source tree itself, the Zenodo/DataCite deposit, the GitHub API and the
PyHC unevaluated registry rather than in packaged metadata.

Two characteristics of the repository shape several fields and are worth knowing up front:

1. **The README is partly stale relative to the code it documents.** Where the two disagree, this
   file follows the code at the pinned revision and records the discrepancy, because a catalogue
   entry that repeats a stale README misleads the searcher.
2. **The package is not confined to Python.** It ships a working IDL rescue script and a working
   MATLAB reader/plotter alongside the Python package. That affects Fields 13, 18 and 19.

The pinned revision `397b9506` (2026-03-11, subject `batch download`) is also the tip of the
project's `main` branch. The newest release, `v1.2.0`, is 17 commits behind it; see Field 12.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The form requires a submitter, but it is a property of the submission act rather than of the
software, so it is left as a placeholder here and supplied at submission time.

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.595411

This is the Zenodo **concept** DOI — the identifier that always resolves to the newest deposit rather
than freezing on one release. Zenodo's own record confirms the relationship directly: every deposit
in the series carries `conceptrecid: 595411` and `conceptdoi: 10.5281/zenodo.595411`, and there are
12 deposits in the series. Resolved on 2026-09-12, the concept DOI landed on record 4722490
(`https://zenodo.org/records/4722490`), which is both the most recently created deposit and the
highest version (`v1.2.0`), so the series carries none of the backport hazard where a late-created
deposit of an old version captures the concept.

**Rejected alternative — the DOI the README advertises.** The badge at the top of `README.md` at the
pinned revision points at `10.5281/zenodo.215309`. That is not the concept DOI; it is the **version**
DOI of the very first deposit, titled `THEMIS ASI GBO data reader` and published 2016-12-21 for
`v1.0`. A visitor who followed the README badge would land on the 2016-12-21 snapshot of the
software. The value recorded here is therefore deliberately *not* the repository's own advertised
DOI, and a future refresh should not "correct" it back to the badge. The README badge is a
repository defect; fixing it is an upstream matter.

**Rejected alternative — the v1.2.0 version DOI** `https://doi.org/10.5281/zenodo.4722490`. That
identifier belongs in Field 12 (Version PID), where it is recorded, not in Field 2. Field 2 should
identify the software across versions.

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/space-physics/themisasi

Confirmed live on 2026-09-12: the GitHub API returned `full_name: "space-physics/themisasi"` with no
rename redirect, `fork: false`, `archived: false`, `default_branch: "main"`. On the same date the
PyPI JSON record for the `themisasi` distribution gave
`Homepage: https://github.com/space-physics/themisasi`, which ties the published package to this
repository rather than merely to a taken name.

The project's git remote is written `https://github.com/space-physics/themisasi.git`. The `.git`
suffix is a clone-transport form; the human-facing repository URL recorded here is the correct value
for a catalogue link.

### 4. Software Functionality (RECOMMENDED — treated as critical)

**The order below is data, not presentation.** HSSI stores this field as a sorted many-to-many
relation, so the sequence is part of the stored value. The sequence here preserves the previously
stored order and inserts each new member *inside its own parent's block*. A later pass must not
regroup or re-alphabetise the list as a whole.

Every subcategory is written `Parent: Child` because 13 subcategory names in the vocabulary sit on
more than one parent — `Analysis`, `Calibration` and `Processing` all appear under both
`Data Processing and Analysis` and `Mission-related`. An unqualified child name would bind
arbitrarily to one of the twins. A child never implies its parent either, so each parent is listed
explicitly alongside its children.

- Coordinate Transforms
- Coordinate Transforms: Mission-Specific
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Data Visualization: Movies

**Evidence for each value.**

- *Coordinate Transforms* / *Mission-Specific* — `src/themisasi/projections.py` converts the
  imager's per-pixel azimuth/elevation plate scale into geodetic latitude/longitude at a
  user-supplied projection altitude (`pm.aer2geodetic`) and into right ascension/declination
  (`pm.azel2radec`); `src/themisasi/fov.py` converts between geodetic, ENU, AER and ECEF to find the
  overlap between two cameras' fields of view. These are user-facing entry points, not internal
  plumbing: `python -m themisasi.radec` is a console command whose entire purpose is the RA/Dec
  projection. The *Mission-Specific* child is the right one because the transforms start from a
  specific instrument's own pointing calibration (the THEMIS star-registered skymap), which is what
  that category covers — instrument pointing, attitude and field of view.
- *Data Access and Retrieval* — `src/themisasi/download.py` fetches both video and calibration
  files from the THEMIS archive over HTTPS, driven by `asyncio.TaskGroup` batches. The user-facing
  entry point is the module-level function `themisasi.download.download(treq, site, odir, urls)`,
  which is how the repository's own callers invoke it: `Examples/Projection.py` does
  `import themisasi.download as tw` and then `tw.download(time_query, "mcgr", datadir, urls=urls)`,
  and `src/themisasi/tests/test_download.py` does `tw.download("2006-09-29T14", "gako", R, urls)`.
  **Neither invocation `README.md` advertises works at the pinned revision** — a further instance of
  the stale-README pattern in the scope note above. `ta.download(...)`, which `README.md` shows three
  times, raises `AttributeError`: `src/themisasi/__init__.py` binds only `load`, `loadcal` and
  `filetimes`, nothing inside the package imports the `download` submodule, and importing the package
  from `src/` at the pinned revision gives `hasattr(themisasi, "download") == False`.
  `python -m themisasi.download` raises `TypeError`: `cli()` at `download.py:32` calls
  `download(P.startend, P.site, P.odir, P.overwrite, urls)`, whereas the function declared at
  `download.py:51` takes its parameters in the order `treq, site, odir, urls, overwrite=False`
  (names in source order, type annotations elided) — `urls` is the fourth positional parameter and
  has no default — so the boolean binds to `urls` and the subscript
  `urls["cal_stem"]` at `download.py:130` is applied to a `bool`. The category is unaffected: remote
  retrieval is implemented and reachable through the documented module function. Recorded so that a
  later refresh does not copy the README's two broken forms into the catalogue as usage examples.
- *Calibration* — `loadcal`, `loadcal_file` and `_findcal` in `src/themisasi/io.py` read the THEMIS
  skymap/plate-scale products in four formats and attach `az`, `el`, `lat`, `lon` and `alt_m` to the
  image stack; `_findcal` selects the calibration whose epoch precedes the requested image time, and
  `load` raises if the calibration post-dates the images. Turning raw pixel indices into pointing
  angles via instrument calibration products is exactly what this category describes, and it is the
  software's headline capability after reading the video itself. The repository also ships the
  imager's spectral response data (`data/icx249al_response.csv`, `data/ir_filter.csv`) with a
  plotting script.
- *Analysis* — `src/themisasi/fov.py` computes the angular separation of each pixel from magnetic
  zenith, fits a cubic to extract a one-dimensional cut plane through two cameras, maps sky angles
  to beam angles for a tomography algorithm, and prints the inter-camera great-circle distance. That
  is derived scientific quantity computation rather than data handling, which is what this catch-all
  subcategory is for.
- *Data Reduction* — `_downsample` in `io.py` decimates the calibration az/el grid to match the
  image grid, deliberately choosing plain decimation over resampling because the calibration field
  is discontinuous.
- *File Format Conversion* — `idl/sav2nc.pro` converts a corrupted IDL `.sav` skymap into netCDF,
  and `io.py` reads four different calibration container formats into one common `xarray.Dataset`.
- *Image Processing* — `projections.py` censors low-elevation pixels where the plate scale is
  unreliable, and `pcolormesh_nan` in `plots.py` repairs non-finite coordinate grids so masked image
  data can be drawn on a geographic mesh.
- *Processing* — the `load` pipeline: time-slice selection with tolerance, merge of image and
  calibration datasets, site consistency checks, longitude rewrapping from [0,360] to [-180,180].
- *2D Graphics* — `plotasi` draws the image with `imshow` under a log norm; `plotazel` draws labelled
  azimuth and elevation contour maps; `asi_projection` draws the image on a geographic mesh.
- *Line Plots* — `plottimeseries` plots pixel brightness against time, driven by
  `python -m themisasi.pixels`.
- *Movies* — `plotasi` and `asi_projection` both animate the full image stack frame by frame and
  optionally write each frame to disk; `python -m themisasi.video` exists solely for playback. The
  bundled MATLAB `plotTHEMIS.m` additionally writes a Motion JPEG AVI.

The stored value previously held twelve functionality rows, and neither
`Data Processing and Analysis: Analysis` nor `Data Processing and Analysis: Calibration` was
among them; both are recorded on the evidence above.

**Considered and not selected.**

- *Coordinate Transforms: Ionospheric* — tempting because the projection altitude defaults to the
  auroral E-region, but that category covers magnetic coordinate systems (AACGM, apex, magnetic
  local time). The software computes none of those; its projection is a straight geometric
  slant-range mapping to geodetic coordinates.
- *Mission-related* and any of its children — the natural error to make with a mission-named
  package. This is a third-party reader written outside the THEMIS project; it is not part of the
  THEMIS ground system, pipeline, archive or operations. The distinction that matters is that
  reading a mission's data is `Data Processing and Analysis`, whereas being part of the mission's
  ground system is `Mission-related`.
- *Data Processing and Analysis: Time Series Analysis* — `_timeslice` and `pixels.py` select and
  extract time-ordered samples but perform no temporal analysis (no filtering, detrending or
  correlation). The plotting side is already covered by *Data Visualization: Line Plots*.
- *Data Visualization: 2D Slices* and *Data Processing and Analysis: 2D Slices* — the "1-D cut"
  in `fov.py` is a line through an image, not a plane through a volume; `_timeslice` selects frames
  from a time series rather than cross-sections from a 3-D physical volume.
- *Data Processing and Analysis: Spectrogram* — no time-frequency transform anywhere in the package.
  The spectral response CSVs are a static instrument datasheet, not a computed spectrum.

### 5. Related Region (RECOMMENDED — treated as critical)

The Region vocabulary is **flat**: no row implies any other, so a coarse region does not entail its
fine-grained members and vice versa. Each value below is therefore selected on its own evidence.

**This sequence is stored data, not presentation.** Field 5 is a sorted many-to-many relation like
Field 4, so its order is part of the stored value. That order is alphabetical by choice rather
than by accident: sorting alphabetically also reproduces the stored relative order of
`Earth Atmosphere` and `Earth Magnetosphere`, the two members the record already held, so the
three finer-grained additions disturbed nothing that was already sequenced. Field 4's rule of
inserting each new member inside its own parent's block belongs to that field's hierarchical
vocabulary and does not govern this flat one; a later pass should keep this list alphabetical.

- Earth Atmosphere
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Magnetosphere
- Earth Thermosphere

**Why these.** The software exists to read and project optical aurora. `Earth Auroral Subregion` is
the single most precise available description of what THEMIS ASI observes, and a visitor browsing
that region who did not find an auroral all-sky imager reader would rightly think the catalogue
incomplete. `Earth Ionosphere` and `Earth Thermosphere` follow from the altitude the software works
at: `README.md` states that "Typically the brightest aurora is in the 100-110 km altitude range, so
a common approximate is to assume "all" of the brightness comes from a single altitude in this
region", and `projections.py` takes that projection altitude as its central parameter. That altitude
band is the E-region ionosphere and the lower thermosphere; a searcher in either region is served by
software that maps auroral emission there. `Earth Atmosphere` is the coarse parent of the optical
emission itself. `Earth Magnetosphere` reflects that the THEMIS ground-based imager array exists to
observe the ionospheric footprint of magnetotail substorm dynamics, which is what the mission's
users come to this data for; the PyHC registry entry for this package likewise carries the
`magnetosphere` keyword.

The record previously carried only `Earth Atmosphere` and `Earth Magnetosphere`; the three
finer-grained regions are recorded on the evidence above.

**Considered and not selected.**

- *Earth Magnetotail* — THEMIS's spacecraft study substorm onset in the tail, but this package
  reads only ground-based optical data and computes nothing in the tail. Someone browsing
  magnetotail software would find an all-sky camera reader out of place.
- *Earth Inner Magnetosphere*, *Earth Outer Magnetosphere*, *Earth Magnetosheath* — the software
  makes no claim about, and does no work in, any particular magnetospheric sub-region.
- *Earth Lower and Middle Atmosphere* — auroral emission at 100–110 km is above this band.

### 6. Authors (MANDATORY)

- **Author 1:**
  - **Given Name:** Michael
  - **Family Name:** Hirsch
  - **Author Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliation 1:** Boston University — https://ror.org/05qwgg493
  - **Affiliation 2:** Scivision, Inc. — no identifier (see below)

**Single author, established mechanically.** Every commit author identity in the pinned revision's
whole ancestry resolves to the same person: `scivision <scivision@users.noreply.github.com>`,
`Michael Hirsch, Ph.D <scivision@users.noreply.github.com>`,
`Michael Hirsch <scivision@users.noreply.github.com>`,
`Michael Hirsch, Ph.D <10931741+scivision@users.noreply.github.com>`,
`Michael Hirsch <10931741+scivision@users.noreply.github.com>`,
`scivision <scivision@noreply.users.gitlab.com>` and
`irs4 <scivision@users.noreply.github.com>`. The last is the only one whose display name is not
obviously Michael Hirsch; it shares the GitHub noreply address of the `scivision` account, and
`10931741+scivision@users.noreply.github.com` is that account's numeric-form noreply address. The
DataCite record for the concept DOI likewise lists exactly one creator, `Hirsch, Michael`, and the
PyHC registry gives `contact: Michael Hirsch`.

**ORCID verified, not assumed.** A bare-name ORCID search would not be safe evidence, so the stored
identifier was checked against the record itself. ORCID `0000-0002-1637-6526` gives given name
`Michael`, family name `Hirsch`, no credit name and no other names, with a single employment —
Boston University, Research Scientist, from 2018-08. Its works list includes *PyMap3D: 3-D coordinate
conversions for terrestrial and geospace environments* (the library this package depends on for its
coordinate transforms) together with *Reconstruction of Fine-Scale Auroral Dynamics*, *The Mysterious
Green Streaks Below STEVE* and other auroral and ionospheric papers. That is conclusively the author
of this package and not a namesake.

**Affiliations.** Boston University is corroborated independently by the ORCID employment record and
by the earliest Zenodo deposit in this series (record 215309), whose creator entry is
`{"name": "Hirsch, Michael", "affiliation": "Boston University"}`. The stored organisation name
matches the ROR record's `ror_display` name for `https://ror.org/05qwgg493` exactly. Scivision is
corroborated by `LICENSE.txt` at the pinned revision, whose first line reads
`Copyright 2017 SciVision`; by nine of the twelve Zenodo deposits in the series — 1294305, 1308222,
1309019, 1405759, 1405778, 1409829, 1419262, 1419294 and 2529524 each give the creator
`"affiliation": "SciVision, Inc."` verbatim — and by the author's long-standing `scivision` identity
across the project's history.

**A spelling divergence that is parked, not open.** HSSI stores the organisation as `Scivision, Inc.`
with a lower-case `v`, which is the value recorded above and is left exactly as it stands. Every
independent source spells it with a capital `V`: `LICENSE.txt` line 1 at the pinned revision, and the
nine Zenodo deposits just named. This is **not** offered as a field change and must not be
re-proposed as one, for two durable reasons. First, the `Scivision`/`SciVision` spelling is parked
catalogue-wide by campaign decision, so it is not this entry's to settle. Second, even once settled
it could not be applied by a routine metadata update: the organisation is a shared row, and a PATCH
carrying the alternative spelling resolves case-insensitively back to the row already stored rather
than renaming it, so the update is a silent no-op. Correcting the spelling needs a direct database
edit, and that edit would change the name for every other catalogue entry sharing the row. Recorded
so a later refresh recognises this as a known, deliberately unchanged divergence rather than a fresh
finding.

**Negative research — do not attach a ROR to Scivision.** A ROR v2 query for `Scivision`, run
2026-09-12, returned exactly one organisation: `https://ror.org/011qev639`, whose `ror_display` name
is `SciVision Biotech Inc. (Taiwan)` and which is located in Kaohsiung, Taiwan. That is an unrelated
biotechnology company, not Michael Hirsch's consultancy. Michael Hirsch's Scivision, Inc. has no ROR
record, so the affiliation is correctly stored without
an identifier and a later pass must not bind it to the Taiwanese ROR on a name match. ORCID's
employment record for this person carries only a RINGGOLD disambiguation identifier (1846, for
Boston University) and lists no Scivision employment at all.

**Zenodo affiliations across the whole series.** All twelve deposits were read, not just the first
and last: 215309, 1294305, 1308222, 1309019, 1405759, 1405778, 1409829, 1419262, 1419294, 2529524,
3247914 and 4722490. Each has exactly one creator carrying exactly one `affiliation` string, so not
one of them packs several institutions into a single field — the trap that silently drops an
affiliation when only the first institution is stored. The values are `Boston University` (215309),
`SciVision, Inc.` (the nine deposits listed above) and `null` (3247914 and 4722490). No deposit in
the series records a contributor at all: the `contributors` key is absent from all twelve records'
metadata, so there is nobody to union in. The DataCite record for the concept DOI likewise has an
empty `affiliation` array and empty `contributors`.

### 7. Software Name (MANDATORY)
- **Value:** THEMISasi

This is the project's own registry-facing name: the PyHC unevaluated registry entry reads
`name: THEMISasi`. Three other spellings exist and were each considered and rejected as the catalogue
value:

- `themisasi` — the importable module name, the PyPI distribution name and the repository name. It is
  correct as an identifier but is a package name rather than a title.
- `THEMIS GBO ASI Reader` — the `README.md` H1 heading. This is descriptive rather than a name, and
  recording it would make the entry hard to find for anyone searching the package name. It is
  preserved here for reference and remains the best short gloss of what the software is.
- `space-physics/themisasi` — the Zenodo deposit titles are of the form
  `space-physics/themisasi: update for newer numpy.datetime64`. That is the GitHub-Zenodo
  integration's automatic `owner/repo: release-name` construction, not a chosen title.

### 8. Description (MANDATORY)
- **Value:**

  Read & plot 256x256 "high resolution" THEMIS ASI ground-based imager data from Python. THEMIS ASI
  data are collected with the original 2002 design, using Starlight-Xpress Lodestar MX716 cameras
  with monochrome Sony ICX249AL imaging chips. A subregion from full-size 752 x 582 pixels (512 x 512
  pixels) are 2x2 binned to 256 x 256 pixels and retrieved over USB 1.1 for disk storage. This
  package also reads the THEMIS ASI star registered plate scale, giving azimuth and elevation for
  each pixel. The software supports downloading data concurrently using asyncio, loading calibration
  data with azimuth/elevation information, coordinate conversion to RA/Dec, video playback, and
  plotting pixel time series.

The first four sentences are the opening of `README.md` at the pinned revision, flattened in two
ways rather than one: its inline Markdown links are reduced to their link text (the Sony chip
datasheet, the Calgary plate-scale archive), and its bold emphasis is dropped — the README writes
`giving **azimuth and elevation** for each pixel`, while the description carries the same words
unemphasised. The closing sentence is a summary of the package's capabilities that has no single
source sentence in the repository. All of it remains accurate at the pinned revision, and the
wording is left as it stands.

**One deliberate divergence from the README, worth preserving.** `README.md` states that "The data is
downloaded concurrently using `asyncio` and `aiohttp_requests`." At the pinned revision
`src/themisasi/download.py` imports `requests`, not `aiohttp_requests`, and runs blocking
`requests.get` calls inside `asyncio` tasks; `aiohttp_requests` appears nowhere in `pyproject.toml`.
The description recorded here says only "downloading data concurrently using asyncio", which is
correct. A future refresh that re-derives this field from the README would reintroduce the stale
`aiohttp_requests` claim; it should not.

### 9. Concise Description (OPTIONAL)
- **Value:** Reads and plots THEMIS ASI video data of aurora, including calibration for
  azimuth/elevation and coordinate transformations.

Derived from the project's own one-line summary — `pyproject.toml` has
`description = "reads and plots THEMIS ASI video data of aurora."` — extended with the two
capabilities that distinguish this package from a bare CDF reader. The extension is editorial and is
left as it stands.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2015-02-11

The date the software first became public. The first commit in the pinned revision's ancestry,
`2fddb65` (`Initial commit`), is dated 2015-02-11, and the GitHub API reports
`created_at: "2015-02-11T05:37:12Z"` for the repository — the same instant.

**Rejected alternative — 2016-12-21**, the publication date of the earliest Zenodo deposit. That is
the date the software was first *archived*, not the date it was first published. The repository
predates it by nearly two years, under its original name `scienceopen/themis-asi-reader` (visible in
the third commit's merge message).

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

From the DataCite record for the concept DOI, whose `publisher` attribute is `Zenodo`. Zenodo is the
publisher of the archived software artefact; GitHub hosts the source but does not publish it in the
DataCite sense.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.2.0
- **Version Date:** 2021-04-27
- **Version Description:** Update for newer numpy.datetime64
- **Version PID:** https://doi.org/10.5281/zenodo.4722490

**There has been no release since 2021-04-27, and the current release is genuine — not a stale
declaration.** This was checked specifically, because a repository whose newest commit is dated
2026-03-11 while its newest release is dated 2021-04-27 can hide several different anomalies:

- *Not an orphan-lineage tag.* `v1.2.0` resolves to commit `b83cf03b32ce1cc7039874583abe123499b99f5c`
  and `git merge-base --is-ancestor v1.2.0 397b9506...` succeeds, so the release is genuinely on the
  line of development that leads to the pinned revision. There are 17 commits between them, in two
  bursts (ten on 2025-03-01 and seven on 2026-03-11).
- *Not a declared-but-unreleased bump.* `pyproject.toml` takes the version dynamically from
  `themisasi.__version__`, and `src/themisasi/__init__.py` at the pinned revision reads
  `__version__ = "1.2.0"`. The project has not declared a newer version that it failed to tag, so
  there is no unreleased version number to record.
- *Not a missing tag.* Eleven tags exist (`v0.7.0` through `v1.2.0`) and eleven GitHub releases
  exist, one per tag. `v1.2.0` is the newest of both. PyPI's newest `themisasi` release is also
  `1.2.0`.
- *Not a backport dragging the concept DOI backwards.* Zenodo's concept DOI resolves to record
  4722490, which is simultaneously the most recently created deposit and the highest version in the
  series of 12.

The 17 post-release commits are real work — dependency-API modernisation, a move to `pre-commit`,
replacement of `dateutil.parse` with `datetime.fromisoformat`, and the `asyncio.TaskGroup` batched
downloader at the pinned revision itself — but the maintainer has not cut a release for them. The
version recorded here is the newest *released* version, which is what Field 12 asks for.

The version description is the release's own title: the GitHub release for tag `v1.2.0` carries
`name: "update for newer numpy.datetime64"` with an empty `body`, and the corresponding Zenodo deposit
is titled `space-physics/themisasi: update for newer numpy.datetime64`. The recorded value
capitalises the first word; the substance is the release's own wording.

**Prior release history**, from the eleven GitHub releases (tag — date — release title):

| Tag | Date | Release title |
|---|---|---|
| v1.2.0 | 2021-04-27 | update for newer numpy.datetime64 |
| v1.1.0 | 2020-07-17 | src/ layout, entry_points, add examples |
| v1.0.0 | 2019-06-17 | asyncio downloading, base url is a parameter, parametrize tests |
| v0.8.4 | 2018-12-31 | improved project structure |
| v0.8.3.1 | 2018-09-14 | bugfix: not autofinding cal files |
| v0.8.3 | 2018-09-14 | fix corner cases, auto-download cal files |
| v0.8.2 | 2018-09-05 | autoload most recent prior cal file if available |
| v0.8.1 | 2018-08-29 | SpacePy=>CDFlib, robust time handling |
| v0.7.2 | 2018-07-10 | Robustify |
| v0.7.1 | 2018-07-09 | modernization |
| v0.7.0 | 2018-06-21 | Initial release |

The project has never had a `CHANGELOG`, `CHANGES` or `NEWS` file, and has never used towncrier-style
changelog fragments — no such path appears anywhere in the pinned revision's ancestry. Release notes
live only in the GitHub release objects, where the `name` field carries the substance and the `body`
adds little. Read from the releases API on 2026-09-12, three of the eleven bodies are empty —
`v1.2.0`, `v1.0.0` and `v0.8.3.1` — and the other eight hold only a short one- or two-line note. The
newest release is one of the empty ones, so a refresh that reads bodies alone will wrongly conclude
the current release is undocumented.

### 13. Programming Language (RECOMMENDED)
- **Values:**
  - IDL
  - MATLAB
  - Python 3.x

**The criterion.** The form asks for "The computer programming languages most important for the
software" and states plainly that it "is not meant to be an exhaustive list". Read from the
searcher's side, that means: list a language when someone filtering the catalogue by it would find
working, usable code for this software in that language, and omit a language whose presence is
incidental. All three inclusions and every exclusion below follow from that one test.

- **Python 3.x** — the package itself. `pyproject.toml` declares `requires-python = ">=3.12"`, and the
  code depends on that floor concretely: `download.py` uses `itertools.batched` and
  `asyncio.TaskGroup`. CI at the pinned revision builds on Python 3.12 only. The `Python 2.x` row was
  considered and rejected outright; nothing in the pinned revision supports it.
- **IDL** — `idl/sav2nc.pro` is a complete, working IDL procedure that rescues THEMIS skymap `.sav`
  files corrupted by an IDL 8.0 bug and rewrites them as netCDF. It is not a leftover: `README.md`
  directs users to it as the documented fallback when a calibration file cannot be read, and the
  script is written to run under GDL as well as IDL.
- **MATLAB** — `matlab/readTHEMIS.m` and `matlab/plotTHEMIS.m` read THEMIS ASI CDF video and play it
  back while optionally writing a Motion JPEG AVI, driven by `matlab/demo.m`. These are maintained
  rather than abandoned: they were repaired on 2025-03-01 (`matlab make work again`, `matlab lint`).
  A MATLAB user looking for a way into THEMIS ASI data is genuinely served by this repository.

**The tension in the MATLAB inclusion, recorded so it is not rediscovered as a surprise.**
`matlab/Readme.md` reads in full: "You should use the Python code, it has many more features." and
"This file is archived as an example of using Matlab to read CDF files." The maintainer therefore
deprecates the MATLAB path in favour of Python. It is retained here anyway because the deprecation is
about *preference*, not *function*. What is demonstrable at the pinned revision is that the MATLAB
path is maintained rather than rotting — `d9b261c` ("matlab make work again") and `262199a`
("matlab lint"), both 2025-03-01, are more recent than the last Python release of 2021-04-27 — that
it targets this specific instrument's data (`readTHEMIS.m` extracts the four-character site code from
a `thg_l<n>_as<x>_<site>_…` CDF filename and cites the THEMIS level-1 archive in its header
comments), and that nothing in the repository marks it broken. Whether the MATLAB code *executes* is
deliberately not asserted: settling that needs a MATLAB interpreter, and none was available by any
route here, so the claim would be unsupported.

**A caveat for anyone who tries the MATLAB demo.** `matlab/demo.m:3` hard-codes
`fn = "../src/themisasi/tests/thg_l1_asf_fykn_2006093004_v01.cdf";`, and that file is not tracked at
the pinned revision — the tracked CDF fixtures are the `gako` ones. Since `readTHEMIS.m` declares
`file (1,1) string {mustBeFile}`, `demo.m` errors on entry unless the fixture is fetched first;
`src/themisasi/tests/test_download.py::test_multi_site` downloads exactly that file into exactly that
directory, which is the shortest way to make the demo runnable.

The "archived" wording is also ambiguous: it is singular ("This file") in a directory holding three
`.m` files. Recorded so that a later refresh weighing removal has the evidence in front of it rather
than re-deriving it.

**Considered and not selected — reducing this field to Python 3.x alone.** The form asks for the
languages "most important" to the software, and the maintainer's own note quoted above pulls that
way. It was rejected on the criterion stated at the top of this field: a MATLAB or IDL user filtering
the catalogue by language finds working, THEMIS-specific code in this repository rather than a dead
end, and a statement of preference does not make that code absent. The tension is left recorded above
rather than resolved by deletion.

**Excluded by the same criterion.** `C`, `C++`, `Fortran` in any dialect, `Java`, `Javascript`,
`Julia`, `Rust`, `SQL`, `Typescript` and `C#` — the repository contains no source in any of them, and
the package ships no compiled extension. `Other` is unnecessary because every language actually
present has its own vocabulary row.

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found.

**This is a considered emptiness, weighed and settled rather than an unexamined gap.**

Field 14 means *the* paper that describes this software. No such paper exists. The repository cites
two articles, both recorded at Field 27, and neither is a paper about this Python package:

- **Mende et al. (2008)**, *The THEMIS Array of Ground-based Observatories for the Study of Auroral
  Substorms*, Space Science Reviews **141**, 357–387, https://doi.org/10.1007/s11214-008-9380-x.
  This describes the **instrument array**, and it was published seven years before this repository's
  first commit.
- **Jackel et al. (2014)**, *Auroral spectral estimation with wide-band color mosaic CCDs*,
  Geoscientific Instrumentation, Methods and Data Systems **3**, 71–94,
  https://doi.org/10.5194/gi-3-71-2014. `README.md` introduces this one as "color instrument based
  on Themis", so it describes a *different* instrument that derives from THEMIS.

`README.md` frames both together as articles that "give vital descriptions of THEMIS GBO ASI" — that
is, descriptions of the hardware and its data, not of the code. Recording either at Field 14 would
tell a user of this catalogue that citing that paper is how one credits this software, which would
misattribute the work. The software's own citable artefact is the Zenodo concept DOI at Field 2.

**Considered and not selected — promoting Mende et al. (2008) into this field.** For software that is
purely an instrument-data reader, the instrument paper is the closest thing in existence to a
description of what the code does, so that reading is not unreasonable, and it is recorded here
rather than dismissed. It was rejected because HSSI renders Field 14 as the citable reference for the
software, and the misattribution would run in both directions: it would credit this package to
authors who did not write it, and credit an instrument paper with describing code that did not exist
when it was published. Field 14 stays empty; both articles stay at Field 27.

### 15. License (RECOMMENDED)
- **Value:** MIT License

**Read by content at the pinned revision, not inferred from a filename.** `LICENSE.txt` carries no
title line; it opens `Copyright 2017 SciVision` and continues with the MIT permission grant. Compared
mechanically against the SPDX canonical `MIT.txt` — with the title line and the copyright line
removed and all whitespace collapsed, to neutralise the fact that the repository's copy is unwrapped
into long single lines — the two are identical, 1020 characters each. GitHub's own licence detection
independently reported `spdx_id: "MIT"` for this repository when checked on 2026-09-12.

**The licence has not always been MIT, which matters for anyone reading older artefacts.** By
content across the whole ancestry of the pinned revision:

| Commit | Date | Licence state |
|---|---|---|
| `2fddb65` | 2015-02-11 | `LICENSE` added — **GNU General Public License v3** |
| `0c3e607` | 2017-02-06 | `LICENSE` changed to the **MIT** permission grant, `Copyright 2017 Michael Hirsch, Ph.D.` |
| `b4e5bee` | 2019-06-17 | `LICENSE` renamed to `LICENSE.txt`, content byte-identical |
| `efa97f1` | 2025-03-01 | copyright line changed to `Copyright 2017 SciVision`; grant text unchanged |

A future agent encountering a GPL-3.0 statement attached to this software is looking at something
from before 2017-02-06 and should not treat it as current.

**Rejected alternatives among the live licence rows.** `Other` is unnecessary because an exact `MIT
License` row exists. The GPL and LGPL rows are ruled out by the content comparison above, not merely
by name. No row was chosen on a near-name match.

**Rejected source — the Zenodo/DataCite licence.** Every one of the twelve Zenodo deposits in this
series records `license: {"id": "other-open"}` — all twelve were checked, not a sample of them — and
DataCite's `rightsList` for the concept DOI gives only `"Open Access"` with
`info:eu-repo/semantics/openAccess`. Neither identifies MIT, and no deposit in the series ever has.
The deposit metadata is wrong about the licence, and the repository is authoritative here.

**Note on how HSSI stores this.** `Software.license` is a foreign key to a shared licence row that
carries its own URL; there is no per-software licence URI to record. The shared `MIT License` row's
URL is `https://spdx.org/licenses/MIT`. An earlier extraction of this software recorded a
per-software licence URI of `https://spdx.org/licenses/MIT.html`, which is neither a stored field nor
the row's URL; it should not be reintroduced.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Values** (recorded as the stored, lower-case forms — the site renders them title-cased, which is
  a display transform and not the stored value):
  - all-sky-camera
  - all-sky-imager
  - aurora
  - geoscience
  - ionosphere_thermosphere_mesosphere
  - magnetosphere
  - python
  - themis
  - xarray

Every one is traceable to a project-controlled source. `pyproject.toml` declares
`keywords = ["all-sky-camera", "aurora"]`. The GitHub repository's topics are `all-sky-imager`,
`geoscience`, `python`, `themis`, `xarray`. The PyHC unevaluated registry entry declares
`keywords: ["magnetosphere","ionosphere_thermosphere_mesosphere","specific"]`.

Keywords are the one open vocabulary in the form: an unmatched value creates a new row rather than
failing. That makes case discipline load-bearing — a title-cased variant would bind to a different
row than the existing lower-case one — so the stored forms above are the values to use.

**Considered and not selected.**

- `specific` — the third PyHC registry keyword. It is a registry-internal classification marker, not
  a domain term, and would be meaningless to a catalogue searcher.
- `substorm` — an obvious candidate given that THEMIS stands for *Time History of Events and
  Macroscale Interactions during Substorms* and that substorm study is what THEMIS ASI data is for.
  It is **not** recorded, because the word appears nowhere in the tracked text of the pinned revision
  (searched across `*.py`, `*.md`, `*.m`, `*.pro`, `*.toml`, `*.yml`, `*.cfg`; the same search shape
  for `aurora` matched four files, so the search would have found it). Adding it would be inference
  rather than evidence. Noted so a later refresh knows the omission was deliberate.
- `cdf`, `calibration`, `skymap` — accurate but not used as keywords by the project in any of its
  three keyword-bearing sources.

### 17. Data Sources (OPTIONAL)
- **Values:**
  - HTTP/HTTPS Directories
  - Observatory/Mission-specific

`src/themisasi/download.py` retrieves data by constructing paths under two hard-coded HTTPS
directory roots — `https://themis.ssl.berkeley.edu/data/themis/thg/l1/asi/` for video and
`https://themis.ssl.berkeley.edu/data/themis/thg/l2/asi/cal/` for calibration — both overridable from
the command line. That is a plain HTTPS directory hierarchy, not a query service, which is why
`HTTP/HTTPS Directories` is right. It is simultaneously observatory-specific: the URLs, the
`thg_l1_asf_<site>_<YYYYMMDDHH>_v01.cdf` filename template and the CDF variable names are all
particular to the THEMIS ground-based array.

**Considered and not selected:** `CDAWeb`, `HAPI`, `Madrigal`, `SSCWeb`, `OMNIWeb`, `AMDA`, `VirES`,
`das2`, `TAP`, `WDC`, `GFZ`, `The Virtual Solar Observatory.`, `S3/Cloud-aware` and `FTP/FTPS
Directories` — the package speaks to none of these. In particular it holds no CDAWeb client despite
reading CDF files, and it makes no FTP requests.

### 18. Input File Formats (RECOMMENDED)
- **Values:**
  - CDF
  - HDF5
  - IDL.sav
  - netCDF3/4

All four are read by `loadcal_file` in `src/themisasi/io.py`, which dispatches on the file suffix:
`.cdf` via `cdflib`, `.sav` via `scipy.io.readsav`, `.h5` via `h5py`, `.nc` via `netCDF4`. Image
video is read from `.cdf` only. `h5py` and `netCDF4` are optional imports guarded by `try/except`
and are declared in the `io` extra of `pyproject.toml`, but the code paths are real and reachable.

**Considered and not selected.**

- `csv` — `PlotCameraResponse.py` at the repository root reads `data/icx249al_response.csv` and
  `data/ir_filter.csv` with pandas. That is a bundled instrument datasheet plotted by a standalone
  script, not a data format users bring to the package. Someone filtering the catalogue for CSV-input
  software would not be looking for this.
- `ISTP-Compliant` — the THEMIS `thg_l1_asf` files are ISTP-conformant CDFs, but the package does not
  implement a generic ISTP reader: it addresses variables by hard-coded THEMIS names such as
  `thg_asf_{site}_epoch` and would not open an arbitrary ISTP file. Claiming this would over-promise.
- `FITS` — read by `dascutils`/`dascasi` in the bundled `Examples/`, not by this package.
- `ascii`, `JSON`, `Zarr` — absent.

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - netCDF3/4
  - Other

`Other` covers the two image/video products the software writes, neither of which has a vocabulary
row: PNG frames, written by `matplotlib` `savefig`; and Motion JPEG AVI, written by
`matlab/plotTHEMIS.m` line 43 through MATLAB's `VideoWriter(vidFN, 'Motion JPEG AVI')`.

**Which routes actually write PNG, because the `-o/--odir` flags are misleading.** The tracked tree
at the pinned revision has exactly three `savefig` call sites — `plots.py:25` in `jointazel`,
`plots.py:140` in `plotasi` and `projections.py:76` in `asi_projection` — and each fires only when
its caller supplies an output path. The one command-line route that reaches any of them is
`python -m themisasi.video`, whose `-o/--odir` value is passed to `plotasi` at `video.py:28`. The
other two `-o/--odir` options do nothing. `pixels.py` declares the option at line 36 and never reads
`P.odir` anywhere in the module. `radec.py:26` calls `asi_radec(imgs, P.odir)` against the signature
declared at `projections.py:81`:
`def asi_radec(dat: xarray.Dataset, min_el: float = 10.0, ofn: Path | None = None):`. The directory
therefore binds positionally to `min_el`, `ofn` stays `None` — and `asi_radec`
contains no `savefig` at all, so it could not write a file even with `ofn` set. `asi_projection` and
`jointazel` are reachable only from Python; the bundled `Examples/` call `jointazel` with an output
filename. The value `Other` is unaffected — PNG output exists and is reachable, and the MATLAB AVI
is written independently of all of this — but a later refresh should not re-derive the claim from
the three `-o/--odir` declarations, which is how the overstatement arose.

`netCDF3/4` rests on the bundled IDL helper. `idl/sav2nc.pro` writes netCDF — `ncdf_create`,
`ncdf_dimdef`, `ncdf_vardef`, `ncdf_varput`, `ncdf_close` — and that is the script's entire
purpose: to rewrite a corrupted skymap `.sav` as a `.nc` file, which `io.py` then reads back
through its `.nc` branch. `README.md` documents this as the supported fallback path. The netCDF
writing therefore lives in the bundled IDL helper rather than in the Python package; that
distinction is recorded explicitly, because it is what supports the value.

**Considered and not selected — recording only `Other`.** Restricting this field to what the
importable Python package writes is a defensible reading, since the Python code itself never writes
netCDF. It was rejected because `idl/sav2nc.pro` is tracked in this repository, `README.md` documents
it as the supported recovery path, and the `.nc` file it produces is read straight back by `io.py`. A
user following the project's own documented workflow produces netCDF with this software, and that is
what a searcher filtering on netCDF output needs to know.

**Considered and not selected — HDF5 output.** `idl/sav2nc.pro` defines a `var2hdf` helper and is
named `SAV2HDF5`, which makes HDF5 output look supported. It is not: the HDF5 write path is commented
out in the script with the note "works in IDL, not in GDL", and only the netCDF path executes. The
procedure name is a leftover from an earlier design. This is the sort of thing a later refresh would
misread from a filename alone.

**Considered and not selected — CDF output.** The package reads CDF and never writes it.

### 20. Operating System (RECOMMENDED)
- **Values:**
  - Linux
  - Mac
  - Windows

`.github/workflows/ci.yml` runs the full test suite on a matrix of `ubuntu-latest`,
`windows-latest` and `macos-latest`, so all three are demonstrated rather than asserted.

**Rejected alternative — `Operating System Independent`.** `pyproject.toml` carries the classifier
`"Operating System :: OS Independent"`, which would justify that single row. The three explicit rows
are preferred because they are what the project actually tests, and because a searcher filtering for
a specific platform gets a concrete answer rather than a claim. Recorded so this is not re-litigated
from the classifier alone.

### 21. CPU Architecture (RECOMMENDED)
- **Value:** CPU Independent

The package is pure Python: `pyproject.toml` declares no extension modules and the build requires
only `setuptools` and `wheel`. There is no architecture dimension in the CI matrix and no
architecture-specific code. Nothing in the repository would behave differently on x86-64, arm64 or
ppc64le.

### 22. Related Phenomena (OPTIONAL)
- **Value:** Not found — evidenced empty, not an unexamined blank.

This software images **aurora**, which would be the obvious value. The live Phenomena vocabulary
contains exactly seven rows, and it is worth listing them in full because the complete list is the
reason this field is correctly empty:

`Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`,
`Solar Wind`, `X-ray emission`.

There is no `Aurora` row, no substorm row, and no auroral or optical-emission row of any kind. The
vocabulary is solar and heliospheric in emphasis and has no term for what this software observes.
The vocabulary is also **flat** — no row implies or is implied by any other — so no coarser value can
stand in for the missing one.

**`Geomagnetic Storms` considered and rejected.** It is the only row with any conceivable connection,
since auroral imagery is a storm-time diagnostic. It is rejected on two grounds. First, factually:
THEMIS exists to study *substorms*, which are not geomagnetic storms, and the word "storm" appears
nowhere in the tracked text of the pinned revision (searched across `*.py`, `*.md`, `*.m`, `*.pro`,
`*.toml`, `*.yml`, `*.cfg`; the same search shape for `aurora` matched four files). Second, from the
searcher's side: someone browsing geomagnetic-storm software wants storm indices, models and
forecasts, and would find a ground-based camera file reader out of place there.

An earlier extraction of this software proposed `Aurora` and "Auroral emissions (visible wavelength,
particularly 557.7 nm based on spectral response data)" for this field. Neither string exists in the
vocabulary, and this field cannot accept free text, so neither was recordable. The correct outcome
is the documented emptiness above. If an auroral row is ever added to the Phenomena vocabulary, this
entry should be among the first to take it.

### 23. Development Status (RECOMMENDED)
- **Value:** Active

The vocabulary row's own definition is "The project has reached a stable, usable state and is being
actively developed." Both halves hold:

- *Stable and usable* — `pyproject.toml` carries the classifier
  `"Development Status :: 5 - Production/Stable"`, eleven releases exist, and the package is
  published on PyPI.
- *Actively developed* — the pinned revision is dated 2026-03-11 and is the tip of `main`. It is not
  a housekeeping commit: the 2026-03-11 burst replaced the downloader's concurrency with
  `asyncio.TaskGroup` and added batched multi-site downloading, and replaced `dateutil.parse` with
  `datetime.fromisoformat`. The repository is not archived (`archived: false`) and is not disabled.

**`Inactive` considered and rejected.** Its definition is "The project has reached a stable, usable
state but is no longer being actively developed; support/maintenance will be provided as time
allows." The case for it is real and worth stating: there has been no release since 2021-04-27, and
development since then has come in two short annual bursts rather than continuously. It is rejected
because a functional change committed at the pinned revision directly falsifies "no longer being
actively developed". If a future refresh finds no commits after 2026-03-11 and still no release, the
case for `Inactive` becomes much stronger and this paragraph is the record of why it was not chosen
now.

**`Unsupported` considered and rejected** — its definition is "The project has reached a stable,
usable state but the author(s) have ceased all work on it. A new maintainer may be desired.", and
neither half applies: work has not ceased (the pinned revision is itself a functional change, dated
2026-03-11) and nothing in the repository seeks a new maintainer. The row is about ceased work, not
about archival — archival is `Abandoned`'s territory, ruled out separately next. `Abandoned`,
`Suspended`, `WIP` and `Concept` are all ruled out by the existence of eleven stable releases.
`Moved` is ruled out because the repository resolves directly with no rename redirect.

### 24. Documentation (RECOMMENDED)
- **Value:** https://github.com/space-physics/themisasi/blob/main/README.md

`README.md` is the whole of this project's user documentation: installation, the `load` API with
worked examples, calibration loading, coordinate conversion, the three
`python -m themisasi.<module>` commands it documents (`download`, `video`, `pixels`) with sample
invocations, the site map, the spectral response, the reference articles, the data resources, and the
IDL `.sav` corruption workaround.

**Rejected alternative — the project's GitHub Pages site,
`https://space-physics.github.io/themisasi/`.** This deserves an explicit record because the GitHub
API advertises it as the repository's `homepage`, so a future refresh will find it and be tempted.
It is a pdoc-generated API reference (the served page carries
`<meta name="generator" content="pdoc 0.6.2" />`), it served content when checked on 2026-09-12, and
it is **stale relative to the code it documents**. The `gh-pages` branch tip is commit
`7300673ee56b4f9cd11d732af9ea3de4efeb6101`, dated 2019-06-17. The site documents five submodules —
`fov`, `io`, `plots`, `projections` and `web` — of which `web` no longer exists under that name. Its
history: added 2019-03-11 as `themisasi/web.py` (`b8ebabe`, "modularize web"), moved to
`src/themisasi/web.py` by the layout change of 2020-07-17 (`a601464`, "use src/ layout"), and renamed
to `download.py` on 2021-04-27 in `b83cf03` — the very commit tagged `v1.2.0`. Conversely the site
documents none of `download`, `pixels`, `radec` or `video`, the four modules that carry the package's
command-line interfaces at the pinned revision. Sending a user there would document a module name
that is gone and hide every command-line interface the package has.

**Those four are `python -m` modules, not installed console entry points.** The distinction is worth
recording because the repository still contains fossils that suggest otherwise. `b83cf03`, the same
2021-04-27 commit, deleted the `console_scripts` block from `setup.cfg`, which had declared
`themisasi_pixels`, `themisasi_video`, `themisasi_radec` and `themisasi_download`; `pyproject.toml`
at the pinned revision declares no `[project.scripts]` at all, so none of those four commands is
installed by `pip install`. Two leftovers survive and will mislead a reader:
`src/themisasi/tests/test_scripts.py:30` still shells out to a bare `themisasi_pixels`, and the
module docstrings of `pixels.py` and `radec.py` still show the older `PlotThemisPixels` and
`ThemisRadec` invocations.

**Negative research — there is no wiki.** The GitHub API reports `has_wiki: false`, but that flag is
not reliable evidence on its own, so the wiki was probed as the separate repository it would be:
`git ls-remote https://github.com/space-physics/themisasi.wiki.git` exits 128 with "Repository not
found", while the same command against `themisasi.git` exits 0. No wiki exists.

There is no ReadTheDocs site, no `docs/` directory and no documentation build configuration anywhere
in the pinned revision.

### 25. Funder (OPTIONAL)
- **Value:** Not found.

### 26. Award Title / Award Number (OPTIONAL)
- **Award Title:** Not found.
- **Award Number:** Not found.

Fields 25 and 26 record what funded **this software**. Nothing in the repository or its deposit
metadata identifies any such funding.

**Everything searched, and why each came up empty.** There is no acknowledgements section anywhere in
the repository — no `README.md` acknowledgement, no funding statement in `pyproject.toml`, no
`CITATION.cff`, no `.zenodo.json`. The DataCite record for the concept DOI carries no funding
references, and neither Zenodo deposit records a grant.

**Rejected — the GitHub funding file.** The only funding-shaped artefact the project has ever had is
`.github/FUNDING.yml`, added 2019-10-02 and deleted 2021-04-27, whose only funding entries were
`github: [scivision]` and `ko_fi: scivision` — the rest of that four-line file is the platform
template's comment and a blank line. Those are personal donation links for the maintainer, not
research awards, and neither names a funder organisation or an award.

**Rejected — funding acknowledged in the cited papers.** Mende et al. (2008) and Jackel et al. (2014)
describe the THEMIS instrument array and a THEMIS-derived colour instrument respectively. Any award
they acknowledge funded the *instrument* or *their authors*, not this Python package, which was
written years later by someone who is an author of neither. This follows the campaign's settled
treatment of "X is supported by …" clauses in related papers as author-level support rather than
software funding.

**Rejected — the author's own grant support.** Michael Hirsch's auroral research (the HiST work whose
traces appear in `Examples/` and in `fov.py`'s magnetic-zenith machinery) was grant-funded, but
support for an author is not funding for a package, and no award is named anywhere in this
repository.

Recording an unsupported funder here would create a shared `Award` row that other catalogue entries
could inherit. The correct value is the documented emptiness above.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Values:**
  - https://doi.org/10.1007/s11214-008-9380-x
  - https://doi.org/10.5194/gi-3-71-2014

These are the two articles `README.md` lists under its "Articles" heading, introduced there as
articles that "give vital descriptions of THEMIS GBO ASI":

- **Mende, S. B., Harris, S. E., Frey, H. U., Angelopoulos, V., Russell, C. T., Donovan, E., Jackel,
  B., Greffen, M., et al. (2008).** *The THEMIS Array of Ground-based Observatories for the Study of
  Auroral Substorms.* Space Science Reviews **141**, 357–387.
  https://doi.org/10.1007/s11214-008-9380-x
- **Jackel, B. J., Unick, C., Syrjäsuo, M. T., Partamies, N., Wild, J. A., Woodfield, E. E.,
  McWhirter, I., Kendall, E., & Spanswick, E. (2014).** *Auroral spectral estimation with wide-band
  color mosaic CCDs.* Geoscientific Instrumentation, Methods and Data Systems **3**, 71–94.
  https://doi.org/10.5194/gi-3-71-2014

**Both values are DOIs; the record previously held bare institutional PDF URLs.**
The superseded values were
`http://www.igpp.ucla.edu/public/THEMIS/SCI/Pubs/2008_Refereed/mende_ssr_onlinefirst.pdf` and
`http://eprints.lancs.ac.uk/68180/4/gi_3_71_2014.pdf` — the same two paths `README.md` links,
recorded under `http://` rather than the README's `https://`. The distinction matters because the
scheme is not incidental: searching `README.md` at the pinned revision for `https?://[^ )"]+` yields
24 URLs and not one of them is `http://`, so no `http://` form of either paper appears anywhere in
this project's own text. They were replaced for three reasons. The form itself prefers a DOI URL for
this field. HSSI renders a related
item's raw URL as the visible link text, so the entry page previously displayed two long file paths
instead of citable references. And an institutional PDF path is a fragile target: a repository
reorganisation silently breaks it, whereas a DOI is maintained by the publisher. Both DOIs were
verified against Crossref — title, container title, volume, page range, year and author list all
match the articles the README intends — and the Lancaster PDF was fetched and its text checked,
which prints `doi:10.5194/gi-3-71-2014` and `Geosci. Instrum. Method. Data Syst., 3, 71–94, 2014` on
its first page, confirming that the superseded URL and the recorded DOI are the same paper.

**Access note for a future refresh.** The Jackel article is fully open access (Copernicus, CC
Attribution 3.0) and its DOI resolves to free full text. The Mende article is a Springer *Space
Science Reviews* paper and may be paywalled at the publisher landing page; the UCLA-hosted preprint
PDF was the open copy. This is a deliberate trade of one open PDF for a durable citable identifier.

**Unverified by route, not reported as absent.** On 2026-09-12 `www.igpp.ucla.edu` was unreachable from
the extraction host — connections to the superseded PDF path and to the site root
`https://www.igpp.ucla.edu/` both timed out without any response, while every other URL named in
this file responded normally. That is a missing route, not proof that the PDF has rotted. The DOI
replacement above does not depend on whether the UCLA copy is alive; it is preferred on durability
and citability grounds regardless.

**Considered and not selected — citing literature.** Papers that merely cite or use this package were
not sought out for this field. The form scopes Field 27 to publications "the software developer
prioritizes", and the developer's own prioritisation is exactly the two-item "Articles" list in the
README.

### 28. Related Datasets (OPTIONAL)
- **Values:**
  - https://data.phys.ucalgary.ca/sort_by_project/THEMIS/asi/skymaps/
  - https://themis.ssl.berkeley.edu/data/themis/thg/l1/asi/
  - https://themis.ssl.berkeley.edu/themisdata/thg/l2/asi/cal/

These are the three data resources the software is built to consume: the level-1 all-sky imager video
archive at Berkeley, the level-2 calibration (skymap / plate scale) archive at Berkeley, and the
star-registered plate scale distribution at the University of Calgary. The two Berkeley URLs are
linked from `README.md` exactly as recorded. The Calgary entry is **not**: both in-repository
references — the README link and the docstring of `loadcal_file` at `src/themisasi/io.py:293` — name
the `new_style/` child,
`https://data.phys.ucalgary.ca/sort_by_project/THEMIS/asi/skymaps/new_style/`, which is the
superseded path. The docstring is therefore corroboration that the software consumes
this archive, not corroboration of the parent URL recorded here; the correction below is what
supports the parent.

**The Calgary URL is corrected; the path the record previously held no longer serves the
data.** The record previously held
`http://data.phys.ucalgary.ca/sort_by_project/THEMIS/asi/skymaps/new_style/`. `README.md` still links
that same `new_style/` child at the pinned revision, writing it as `https://`.

The breakage is worth setting out hop by hop, because the two schemes behave differently and a
scheme-blind check attributes it to the wrong URL. Measured on 2026-09-12:

- `http://data.phys.ucalgary.ca/sort_by_project/THEMIS/asi/skymaps/new_style/` — the superseded
  recorded value — returns HTTP 301 **with** an ordinary
  `Location: https://data.phys.ucalgary.ca/sort_by_project/THEMIS/asi/skymaps/new_style/` upgrade
  header and a 169-byte nginx redirect body. There is nothing wrong with this hop in itself.
- `https://data.phys.ucalgary.ca/sort_by_project/THEMIS/asi/skymaps/new_style/` returns HTTP 301
  **with no `Location` header**, and a 70,491-byte body whose title is `SRS Open Science Platform`,
  the UCalgary Space Remote Sensing portal landing page. This is the broken hop, and it belongs to
  the `https` form — which is the form `README.md` links.

Following the superseded value end to end therefore terminates at the `https` `new_style/` URL with
status 301 after one redirect: a person lands on a generic portal page instead of the skymaps, and an
automated client has no `Location` to follow onwards. On the same date the parent directory
`https://data.phys.ucalgary.ca/sort_by_project/THEMIS/asi/skymaps/` returned HTTP 200 and a
4,131-byte working directory listing — 24 four-character station directories plus `_archival/` and
`z_spedas/` — in which the string `new_style` did not occur at all. The parent directory is therefore
the current authoritative location and is what is recorded. The repository's own link is stale here;
that is an upstream matter.

**All three are recorded as `https://`.** The record previously held all three as `http://`. The two
Berkeley URLs redirected from `http` to `https` and served their listings when checked on 2026-09-12,
so for those two this is a durability and presentation improvement rather than a repair: HSSI
displays the raw URL as the link text, and `README.md` writes both Berkeley URLs with `https://` at
the pinned revision. The appeal to the project's own usage is scoped to those two deliberately — the
Calgary **parent** recorded here appears nowhere in `README.md`, which links the `new_style/` child
instead, so the repository cannot be cited in support of the parent's scheme. For the Calgary entry
the scheme choice rests on the measurement above: the `http` form only redirects to the `https` form
anyway.

**Considered and not selected — a second calibration URL.** `src/themisasi/download.py` fetches
calibration files from `https://themis.ssl.berkeley.edu/data/themis/thg/l2/asi/cal/`, a *different*
path from the `/themisdata/thg/l2/asi/cal/` one that `README.md` links and that is recorded here.
Both paths served the same level-2 calibration products when checked on 2026-09-12. Listing both would put
two links to the same dataset on the entry page, which helps no one. The README's form is kept as the
project's own public-facing citation of the resource. Noted so that a future refresh reading
`download.py` rather than the README does not add the second path as a fourth dataset.

**Considered and not selected — the THEMIS site coordinate spreadsheet** at
`https://themis.ssl.berkeley.edu/images/ASI/THEMIS_ASI_Station_List_Nov_2011.xls`, listed under the
README's "Resources" heading. It is a station metadata table from 2011, not a dataset the software
reads or analyses. The same applies to the mosaic browse page
`https://themis.ssl.berkeley.edu/gbo/display.py?`, which is a human-facing display tool.

### 29. Related Software (OPTIONAL)
- **Values:**
  - https://github.com/geospace-code/pymap3d
  - https://github.com/space-physics/dascasi
  - https://github.com/space-physics/histutils

Field 29 is for software that *distinguishes* this package — a similar-purpose tool, a predecessor, a
companion, or a domain-specific dependency whose presence characterises the software. Each entry
below is a heliophysics or geospace-specific package, and none would be at home in a web application,
a finance model or a biology pipeline.

- **pymap3d** — the coordinate-conversion library every geometric operation in this package routes
  through. `src/themisasi/projections.py` and `src/themisasi/fov.py` both import it;
  `src/themisasi/tests/test_scripts.py` has `pytest.importorskip("pymap3d")`; `pyproject.toml`
  declares it in the `fov` extra; and `README.md` devotes a "Coordinate conversion" section to it.
  It is by the same author and is itself indexed in this catalogue.
- **dascasi** — the reader for the University of Alaska Geophysical Institute Digital All-Sky
  Cameras (the bundled examples use Poker Flat data), the closest thing this package has to a
  sibling: another all-sky imager reader for auroral optical data, by the same author. It is a
  declared optional dependency: `pyproject.toml` gives the `cameras` extra exactly one member,
  `"dascutils"`. It is imported by `Examples/DascThemisFOV.py` and `Examples/DascThemisSlice.py`.
  **The URL is not the one the code names.** The repository `space-physics/dascutils` was renamed.
  Checked on 2026-09-12: the GitHub API answered the `dascutils` path with HTTP 301, and the target
  it named returned `full_name: "space-physics/dascasi"`; the PyPI `dascutils` distribution gave
  `home_page: https://github.com/space-physics/dascasi`. The current repository URL is recorded so
  that the catalogue link does not depend on a GitHub rename redirect that a future rename could
  break. It is also exactly the code repository URL of the in-catalogue HSSI entry **DASCutils**, so
  the relation points at the same place that entry does.
- **histutils** — the HiST project's data-reading utilities. `src/themisasi/fov.py` imports it
  unconditionally at module level (`import histutils.findnearest as fnd`) and its `findClosestAzel`
  is the primitive on which the entire multi-camera field-of-view overlap calculation rests;
  `pyproject.toml` declares it in the `fov` extra and `test_scripts.py` has
  `pytest.importorskip("histutils")`. The repository `space-physics/histutils` was confirmed to
  exist, described as "HiST project raw data reading utilities", and to contain
  `src/histutils/findnearest.py` — the exact module imported. Its presence is what tells a reader
  that this package's field-of-view machinery grew out of auroral tomography work rather than
  general imaging.

The record previously held `https://github.com/geospace-code/pymap3d` alone; `dascasi` and
`histutils` are recorded on the evidence above.

**Considered and not selected.**

- **numpy, scipy, matplotlib, requests, pandas, pytest, mypy, setuptools, wheel** — generic
  scientific-Python and tooling infrastructure: each would be equally at home in a web application,
  a finance model or a biology pipeline, which is the test that excludes them. This exclusion applies
  to Field 29 exactly as it does to Field 30; a package rejected from Field 30 does not thereby land
  here.
- **scipy, specifically** — worth an explicit note because `README.md` tells a story that invites
  the mistake: the author contributed a patch to SciPy so that it could read THEMIS's corrupted
  `.sav` files, "which was incorporated into SciPy 0.18.0". That is an upstream contribution history,
  not a relationship that distinguishes this software. SciPy remains generic infrastructure here.
- **cdflib, h5py, netCDF4, xarray** — file-format and array libraries. `xarray` is recorded at Field
  30 on specific interchange evidence; see there. The others are internal I/O plumbing.
- **histfeas** — `Examples/ThemisHistApr14T854.py` reads precomputed calibration from a hard-coded
  `~/code/histfeas/precompute/` path. That is a local path in an example script, not a declared
  dependency or a documented integration, so it does not meet the bar.

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - https://github.com/geospace-code/pymap3d
  - https://github.com/space-physics/dascasi
  - https://github.com/pydata/xarray

The bar for this field is a *demonstrated exchange*, not a dependency relationship. Each entry meets
it with a specific, citable artefact.

- **pymap3d** — `README.md` documents the exchange explicitly, in a worked example that feeds this
  package's output object straight into pymap3d's API:
  `rasc, decl = pm.azel2radec(dat.az, dat.el, dat.lat, dat.lon, dat.time)`, where `dat` is the
  `xarray.Dataset` returned by `ta.load(...)`. That is one tool's output consumed by the other
  across a documented boundary.
- **dascasi** — `Examples/DascThemisFOV.py` and `Examples/DascThemisSlice.py` load DASC imagery
  through `dascutils.io` and THEMIS imagery through this package, then compute the shared field of
  view and a cut plane between the two cameras in one analysis. Two peer instrument readers
  producing compatible datasets that are combined in a single computation is the paradigm case for
  this field.
- **xarray** — a Tier B package, admitted only on documented interchange evidence, which exists
  here. `xarray.Dataset` is not an internal detail of this package: it is its entire public return
  type. `README.md` lines 47-49 read, with ` / ` standing here for the source's line breaks,
  "THEMIS-ASI output /
  [xarray.Dataset](https://xarray.pydata.org/en/stable/generated/xarray.Dataset.html), / which is
  used throughout geosciences and astronomy." — and the README then documents how to use it
  (`dat['imgs']`, `dat.time`, `dat.x`, `dat.y`, and the `az`/`el`/`lat`/`lon` attributes added when
  calibration is present). Both public functions, `load` and `loadcal`, are annotated
  `-> xarray.Dataset`, and `xarray` is one of the project's own GitHub topics. This is the
  documented interchange format, which is precisely the qualifying case for a Tier B package — as
  distinct from "uses xarray internally", which would not qualify. Excluding it as a Tier B package
  that had not cleared the bar was the alternative considered, and it was rejected on that same
  evidence — deliberately rather than by default, since a Tier B admission should never be
  automatic.

The record previously held `https://github.com/geospace-code/pymap3d` alone; `dascasi` and
`xarray` are recorded on the evidence above.

**Considered and not selected.**

- **numpy, scipy, matplotlib, requests, pandas** — Tier A generic infrastructure, excluded without
  exception. Depending on an array, dataframe or plotting library is not an exchange between peer
  tools; it is the ordinary substrate that scientific Python is written on.
- **cdflib** — Tier B, and it fails the Tier B test. This package imports cdflib to open THEMIS CDF
  files; that is internal file reading, not an exchange between peer tools. No cdflib object crosses
  this package's public API.
- **h5py, netCDF4** — same reasoning as cdflib, and both are optional guarded imports used only to
  open calibration containers.
- **histutils** — recorded at Field 29 rather than here. `fov.py` calls one utility function from it
  (`findClosestAzel`); no data model or object is exchanged between the two packages in either
  direction. The distinction between a domain-specific dependency and a demonstrated interoperation
  is what separates Field 29 from Field 30, and histutils falls on the Field 29 side.
- **MATLAB** — Tier B, and the relationship is not interoperation. The bundled `matlab/` scripts are
  an independent reimplementation of part of the package's functionality in another language, not a
  bridge between the Python package and MATLAB. Nothing passes between them. The MATLAB presence is
  recorded at Field 13 instead, which is where it belongs.
- **The PyHC ecosystem as a whole** — this package appears in the PyHC unevaluated registry, but
  registry membership is never on its own evidence of interoperation with any particular package.

### 31. Related Instruments (OPTIONAL)

Twenty-four instruments, each recorded with the vocabulary row's canonical name copied byte for byte
and its SPASE identifier, which is the reliable de-duplication key:

| Instrument name | SPASE identifier |
|---|---|
| THEMIS Ground Athabasca All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/ATHA/ASI |
| THEMIS Ground Chibougamau All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/CHBG/ASI |
| THEMIS Ground Ekati All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/EKAT/ASI |
| THEMIS Ground Fort Simpson All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/FSIM/ASI |
| THEMIS Ground Fort Smith All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/FSMI/ASI |
| THEMIS Ground Fort Yukon All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/FYKN/ASI |
| THEMIS Ground Gakona All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/GAKO/ASI |
| THEMIS Ground Gillam All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/GILL/ASI |
| THEMIS Ground Goose Bay All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/GBAY/ASI |
| THEMIS Ground Inuvik All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/INUV/ASI |
| THEMIS Ground Kapuskasing All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/KAPU/ASI |
| THEMIS Ground Kiana All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/KIAN/ASI |
| THEMIS Ground Kuujjuaq All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/KUUJ/ASI |
| THEMIS Ground McGrath All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/MCGR/ASI |
| THEMIS Ground Narsarsuaq All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/NRSQ/ASI |
| THEMIS Ground Pinawa All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/PINA/ASI |
| THEMIS Ground Prince George All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/PGEO/ASI |
| THEMIS Ground Rankin Inlet All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/RANK/ASI |
| THEMIS Ground Sanikiluaq All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/SNKQ/ASI |
| THEMIS Ground Snap Lake All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/SNAP/ASI |
| THEMIS Ground Taloyoak All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/TALO/ASI |
| THEMIS Ground The Pas All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/TPAS/ASI |
| THEMIS Ground White Horse All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/WHIT/ASI |
| THEMIS Ground Yellowknife All Sky Imager | https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/YKNF/ASI |

**Why the whole array and not a subset.** This is the question worth recording, because a 24-entry
list looks like over-listing until the evidence is in front of you. The software is **not** built
around a fixed station list: `site` is a free parameter to `ta.load(...)` and to
`themisasi.download.download(...)` (the README's `ta.download(...)` spelling does not resolve at the
pinned revision — see Field 4), and `_urlgen` in `download.py` builds the archive path by string
interpolation (`thg_l1_asf_{site}_{YYYYMMDDHH}_v01.cdf`) for whatever four-character code the user
supplies. There
is no `VALID_SITES` constant anywhere in the pinned revision; the only list-shaped thing is
`sites = ['fykn', 'gako']` in a README example of looping over sites, which is an illustration, not a
restriction. Site codes that do appear in the repository — `gako`, `fykn`, `mcgr`, `whit`, `kian`,
`inuv` — occur only in examples, tests and docstrings. The software therefore supports every station
in the array equally, and a visitor arriving from any one imager's page would be correctly served.

**Corroboration that 24 is the right cardinality.** Two independent sources agree exactly. The
vocabulary contains 24 rows under `https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/*/ASI`,
and the UCalgary skymap archive that this software reads its plate scales from lists 24 station
directories: `atha`, `chbg`, `ekat`, `fsim`, `fsmi`, `fykn`, `gako`, `gbay`, `gill`, `inuv`, `kapu`,
`kian`, `kuuj`, `mcgr`, `nrsq`, `pgeo`, `pina`, `rank`, `snap`, `snkq`, `talo`, `tpas`, `whit`,
`yknf`. Those two sets are identical, station for station. The set recorded here is exactly that set.

**Identifier integrity.** All 24 identifiers begin `https://spase-metadata.org/`. None of the 24 has
a `.html` duplicate row in the vocabulary, so there is no bare-versus-`.html` normalisation choice to
make here. Every row resolves uniquely; none required an observatory-level substitution and none is
ambiguous. There are no unresolved entries in this field.

**Considered and not selected.**

- **TREx all-sky imagers** — the vocabulary holds three other rows whose names end in "All Sky
  Imager": `Blue All Sky Imager`, `Near Infrared All Sky Imager` and `Red-Green-Blue All Sky Imager`,
  all under `https://spase-metadata.org/SMWG/Instrument/TREX/`. TREx is a different (and later)
  Canadian imaging array; this package reads none of its data and implements none of its formats.
  Recorded because a name-similarity search will surface them.
- **THEMIS ground magnetometers** — the vocabulary holds a large family of
  `.../THEMIS/Ground/*/MAG` fluxgate magnetometer rows at many of the same stations, plus
  `THEMIS Ground Magnetometers`. This package reads no magnetometer data whatsoever; it handles only
  `thg_l1_asf` optical video and `thg_l2_asc` / skymap calibration. Someone browsing magnetometer
  instruments would find an image reader out of place.
- **The THEMIS spacecraft instruments** — the non-ground THEMIS instrument rows for probes A
  through E, which span ten suffix families: `EFI`, `ESA`, `Ephemeris`, `FBK`, `FGM`, `MOM`,
  `Models`, `SCM`, `SpacecraftMode` and `SST`. They live under three identifier families, which is
  why the same suffix recurs more than once: `.../SMWG/Instrument/THEMIS/<probe>/…`,
  `.../CNES/Instrument/CDPP-AMDA/THEMIS/<probe>/…` and
  `.../CNES/Instrument/CDPP-Archive/THEMIS-<probe>/…`. This package reads only ground-based data, so
  none of them applies. This is the most likely future mis-proposal, because the mission name matches
  exactly — and `Models` and `SpacecraftMode` are named explicitly here because they are the two the
  eye skips when this family is scanned as "the instrument rows".
- **The colour imager of Jackel et al. (2014)** — cited in the README as a "color instrument based
  on Themis", but the software neither reads its data nor implements its formats. The citation is
  background reading, which is why that paper is at Field 27 and not here.

### 32. Related Observatories (OPTIONAL)

- **Time History of Events and Macroscale Interactions during Substorms** —
  https://spase-metadata.org/SMWG/Observatory/THEMIS
- **NASA THEMIS GBO Ground Stations** —
  https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/UCLA-GBO

**Choosing among same-named rows.** Several rows carry THEMIS-related names and the choice was made
on the identifier rather than the name. `https://spase-metadata.org/SMWG/Observatory/THEMIS` is the
mission-level record in the SMWG naming authority, which is the tie-breaker among duplicates. The
CNES row `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/Themis` describes the same mission
but under a different naming authority and with a different canonical name
(`Time History of Events and Macroscale Interactions during Substorms; NASA Magnetospheric
Mission`); it was not selected. The five probe-level rows
`.../SMWG/Observatory/THEMIS/A` through `/E` were not selected because this package reads no
spacecraft data.

**Why the ground-based network row is recorded alongside the mission-level one.** This was decided
by the user, on what the searcher sees: someone arriving at the THEMIS GBO ground-stations page and
asking "what software works with this?" should be shown a THEMIS GBO all-sky-imager reader, and this
package is exactly that. `https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/UCLA-GBO` is the
observatory record for the ground-based network the software exists to serve, and it is the row in
the vocabulary that names that network. Before this refresh the entry carried only the mission-level
row, which answered that visitor's question only at the scale of the whole mission — a THEMIS
spacecraft-data user and a THEMIS ground-imager user were given the same single association.

**The partial-coverage objection, and why it is weaker than it looks.** Seven of the twenty-four
instrument identifiers recorded at Field 31 — Athabasca, Fort Simpson, Fort Smith, Gillam, Pinawa,
Rankin Inlet and Sanikiluaq — sit on the `.../Instrument/THEMIS/Ground/CANMAG/<STN>/ASI` path rather
than the `UCLA-GBO` one, which makes the GBO row look as though it covers only part of the array.
SPASE's own naming says otherwise. The per-station observatory rows on the `CANMAG` path are
themselves named `NASA THEMIS GBO Athabasca Station`, `NASA THEMIS GBO Fort Simpson Station`,
`NASA THEMIS GBO Fort Smith Station`, `NASA THEMIS GBO Fort Yukon Station`,
`NASA THEMIS GBO Gakona Station`, `NASA THEMIS GBO Gillam Station`, `NASA THEMIS GBO Pinawa Station`,
`NASA THEMIS GBO Rankin Station` and `NASA THEMIS GBO Sanikiluaq Station` — every one of them a GBO
station by name. The GBO designation is therefore not confined to the `UCLA-GBO` path segment; the
`CANMAG` segment marks an operating and data-path distinction inside the same ground-based observing
programme, not a different programme. This is the durable point: a later refresh reading the path
segments alone will reach for the coverage objection, and the station names are what answer it.

**Considered and not selected.**

- **Canadian Magnetometer Array** — `https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/CANMAG`
  is the parent identifier of seven of the imagers at Field 31, which makes it look like the natural
  companion to the GBO row, and coverage is precisely the argument a later refresh would reach for.
  It is rejected on what the searcher actually sees: the row's name presents it as a magnetometer
  array, someone browsing a magnetometer-array page is looking for magnetometer data, and this
  package reads none. Its imagers are already listed individually at Field 31, so nothing is lost by
  omitting the parent.
- **THEMIS-Associated Ground Magnetometer Stations** — the name carried by both
  `.../SMWG/Observatory/THEMIS/Ground`, the parent of the `CANMAG` and `UCLA-GBO` branches alike, and
  `.../SMWG/Observatory/Ground/GMAG` — and **Athabasca University THEMIS UCLA Magnetometer Network**
  (`.../SMWG/Observatory/AUTUMN`): magnetometer networks, rejected for the same reason as CANMAG.
  That the THEMIS ground parent is itself named for magnetometers is a further reason the GBO row,
  rather than that parent, is the right home for an imager reader.
- **NASA THEMIS EPO Ground Stations** (`.../SMWG/Observatory/THEMIS/Ground/UCLA-EPO`) and **NASA
  THEMIS Ground Stations in Alaska** (`.../SMWG/Observatory/THEMIS/Ground/GIMA`) — THEMIS ground
  station sets, but different station sets from the ones this software reads. The EPO stations are
  Bay Mills, Carson City, Derby, Fort Yates, Hot Springs, Loysburg, Pine Ridge, Petersburg, Remus,
  Shawano and Ukiah; not one of the stations at Field 31 has its observatory record under either
  identifier.
- **The station-level observatory rows** — `NASA THEMIS GBO Gakona Station` and its peers, one for
  each station whose imager is listed at Field 31, the two sets matching station for station. They
  are not selected because Field 31 already carries this software's coverage at station granularity;
  repeating that observatory by observatory would lengthen the entry page without telling a visitor
  anything the instrument list has not already told them. Their paths do not mirror the imager paths
  either — Fort Yukon's and Gakona's observatory records sit under `CANMAG` while their imagers sit
  under `UCLA-GBO` — so the set would not even read as a clean parallel. Recorded so a later refresh
  does not add them in the name of completeness.
- **THEMIS at the TEIDE Observatory** (`.../SMWG/Instrument/Ground/TEIDE/THEMIS`) — an unrelated
  solar telescope that shares the acronym. Recorded because any name-based search for "THEMIS" will
  return it.

### 33. Logo (OPTIONAL)
- **Value:** https://i.ibb.co/Jyx1nNd/thm-gbo-logo.jpg

**Verified as an image, and looked at.** Fetched on 2026-09-12, the URL returned
`Content-Type: image/jpeg` and 16,122 bytes of a valid JPEG, 309 × 85 pixels. Rendered and inspected
at magnification, it is a wide banner read left to right: a bright orange Sun at the left edge with
striped rays streaming rightward; across the centre a purple-and-blue cutaway of Earth's
magnetosphere — bow shock, magnetopause and nested lobes — with a small peach Earth at its nose;
several small boxy spacecraft strung out along the magnetotail below and to the right of Earth, the
nearest of them the largest; and, occupying the right third, the white serif wordmark "THEMIS" above
"GBO". It is legible and clearly an intentional graphic, not a data plot or a screenshot.

**Provenance.** It comes from the project's own PyHC unevaluated registry entry, which as fetched on
2026-09-12 declared `logo: https://i.ibb.co/Jyx1nNd/thm-gbo-logo.jpg` alongside `name: THEMISasi`,
`code: https://github.com/space-physics/themisasi` and `contact: Michael Hirsch`. That is the project
presenting this image as its logo.

**Two caveats, weighed and recorded rather than acted on.** First, it is a THEMIS **GBO mission**
banner rather than a mark for this Python package specifically; a different THEMIS GBO tool could
legitimately use the same image. Second, `i.ibb.co` is a free image-hosting service (imgbb), which
sits uneasily with the form's requirement that the logo be "stored online in a permanent place" —
there is no versioning, no institutional custodian and no guarantee of persistence. Neither caveat
was judged disqualifying and the value is kept: the project itself presents this image as its logo,
which is stronger evidence of what its logo is than either caveat is against it. The alternative
weighed was an empty Field 33 — never a substitute image, since the repository offers no candidate,
as the next paragraph records — and that remains the correct outcome if a later reviewer judges the
host or the subject disqualifying.

**No alternative exists in the repository.** The pinned revision contains one tracked image,
`data/spectral_response.png`, which is a plot of the imager's spectral response curve — genuine
documentation content, embedded in the README, but not a logo. There is no logo file, no
`docs/` directory and no Sphinx `html_logo` setting anywhere in the pinned revision, so there is no
git-hosted asset to pin to a commit SHA and no in-repository candidate to prefer.
