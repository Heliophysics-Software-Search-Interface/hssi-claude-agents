# HSSI Metadata Extraction Results

**HSSI Software ID:** afcb9669-1336-48ff-ad58-a7446b8b09f0
**Repository:** https://github.com/amisr/amisrsynthdata
**Source Revision:** ba35a765e4370aefcf7ebc607765e489c84ed709
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-10-28
**Validation Status:** PASS
**Final HSSI state:** Fields 2–33 match the validated record as of 2026-10-28.

Who submitted amisrsynthdata to HSSI is not exposed by the API (Field 1). The record's values stand
unless authoritative evidence shows them stale, incomplete or factually wrong; each correction is
justified with its field.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Not part of the stored record; the live view API does not expose the original submitter.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.12210900

- Verified as the Zenodo *concept* (all-versions) DOI: the Zenodo API
  for record 14174414 reports `"conceptdoi": "10.5281/zenodo.12210900"` and
  `"conceptrecid": "12210900"`. DataCite resolves it with `relationType: HasVersion` links to all
  seven version DOIs, v1.1.3 through v1.2.0 (read 2026-10-27). This is the correct value for this
  field; the version DOI belongs in Field 12.
- What the concept presents: its DataCite `version` is `v1.2.0` and its title is the v1.2.0
  integration deposit's `amisr/amisrsynthdata: v1.2.0`, matching the current tag `v1.2.0` (revision
  `8baaf296413d2f529b7ab85561fe1546343c8e3d`).

### 3. Code Repository (MANDATORY)
https://github.com/amisr/amisrsynthdata

- Confirmed via the GitHub API (`full_name: amisr/amisrsynthdata`,
  `archived: false`, `default_branch: main`) and as the `Homepage` project URL in `pyproject.toml`.

### 4. Software Functionality (RECOMMENDED)

`Models and Simulations` was present in the record at its first refresh (July 2026); the other
twelve values rest on the code evidence given with each. Every subcategory is listed together with
its parent.

- **Coordinate Transforms**
  - Parent of the ionospheric transform below; also covers the geodetic/AER/ENU/UVW frame
    conversions that define the radar geometry (`radar.py` uses `pymap3d.aer2geodetic`,
    `aer2enu`, `enu2uvw`, `uvw2enu`; `syntheticdata.py` uses `enu2geodetic`, `geodetic2enu`).
    These are user-facing: the `radar.lat`, `radar.lon` and `radar.alt` gate coordinates appear in
    the usage example in `docs/source/usage.rst`, and `Radar.kvec_all_gates()` is documented through
    the API reference (`docs/source/reference.rst`, which autodocuments the `Radar` class with
    `:members:`).
- **Coordinate Transforms: Ionospheric**
  - `ionosphere.py` instantiates `apexpy.Apex`; `syntheticdata.py` calls
    `self.iono.apex.geo2apex(...)` for magnetic latitude/longitude and
    `self.iono.apex.convert(..., 'geo', 'mlt', ...)` for magnetic local time, writing
    `MagneticLatitude`, `MagneticLongitude`, `MagneticLocalTimeMidnight` and
    `MagneticLocalTimeSite` into the output file. `velocity.py` provides a
    `uniform_mlat_aligned` state function that works in apex magnetic coordinates.
- **Data Processing and Analysis**
  - Parent of the three subcategories below; the package reads YAML configuration
    (`yaml.safe_load`), reads bundled HDF5 beamcode tables (`h5py.File(bc_file, 'r')`), reads
    GEMINI model output, computes derived quantities, and writes a structured HDF5 product.
- **Data Processing and Analysis: 2D Slices**
  - `SyntheticData.create_summary_plots()` builds horizontal ENU grids
    (`slice_xrng`/`slice_yrng`) at five altitudes (`alt_slices` defaults to `[100000., 200000.,
    300000., 400000., 500000.]` m, i.e. 100–500 km) and
    evaluates the 3D ionospheric state on each slice. `gemini_utils.query_model()` samples the 3D
    GEMINI volume at arbitrary geographic points via `model2pointsgeogcoords`.
- **Data Processing and Analysis: Data Reduction**
  - `Radar.calculate_gates()` averages the high-resolution ACF range gates into coarser altitude
    bins with `np.nanmean` over each bin, reproducing the radar's pre-summing/fitting resolution
    reduction. `Radar.calculate_acf_gates()` defines the higher-resolution grid it reduces from.
- **Data Processing and Analysis: Processing**
  - The CLI (`amisrsynthdata.syntheticdata:main`) runs a complete pipeline: config parse →
    ionosphere + radar construction → measurement generation → error generation → optional Gaussian
    noise (`noisy_measurements`) → structured HDF5 output → optional summary plots.
- **Data Visualization**
  - Parent of the three subcategories below; `create_summary_plots()` is a documented user-facing
    capability, enabled by the `[plots]` extra (`matplotlib`, `cartopy`).
- **Data Visualization: 2D Graphics**
  - `ax.contourf` altitude-slice maps on a Cartopy `AzimuthalEquidistant` projection,
    `ax.pcolormesh` range-time-intensity panels, and `ax.quiver` plasma-velocity vector fields.
- **Data Visualization: 2D Slices**
  - The top row of every summary figure displays the ionospheric state on the five horizontal
    altitude slices, with beam positions overplotted at each altitude.
- **Data Visualization: 3D Graphics**
  - `fig.add_subplot(gs[:, -1], projection='3d')` renders the full radar field of view as a 3D
    scatter of synthetic measurements (JOSS paper, Figure 1 **left** panel — the caption in
    `manuscript/paper.md` reads "Left: A 3D visualization of beam positions with synthetic density
    measurements…").
- **Models and Simulations**
  - Present in the record at its first refresh, and the package's core purpose: forward-model
    synthetic AMISR data from a specified ionospheric state.
- **Models and Simulations: Empirical**
  - The ionospheric state functions are analytic/empirical parameterizations:
    `density.py` provides `uniform`, `chapman`, `epstein`, `gradient`, `tubular_patch`,
    `circle_patch`, `wave`; `temperature.py` provides `uniform`, `hypertan`; `velocity.py` provides
    `uniform`, `uniform_mlat_aligned`, `uniform_glat_aligned`.
- **Models and Simulations: Observatory/Instrument Models**
  - The package models the AMISR observing system itself — beam pointing from beamcode tables or
    az/el, range-gate geometry, look vectors, integration period, and a range-squared error model —
    and produces synthetic observations as the radar would record them. README: 'This can be used
    to generate synthetic data in the "SRI data format" both for the three existing AMISRs and for
    hypothetical future "AMISR-like" systems.'

**Considered and deliberately excluded** (audit trail):

- `Models and Simulations: Instrument Response` — the README states explicitly that the package
  "does NOT attempt to simulate any aspect of fundamental ISR theory", and its Limitations section
  excludes "Any kind of proper treatment or simulation of ISR theory"; the `ksys`
  calibration constants are NaN placeholders. Claiming instrument-response modelling would
  contradict the author's own scope statement.
- `Models and Simulations: Forward-Fitting` — amisrsynthdata is a forward model, but it performs no
  fitting or optimization; the `chi2`/`fitcode`/`nfev` fields it writes are constant placeholders.
  Its role is to provide truth data *for* other groups' inversion codes.
- `Models and Simulations: First Principles` / `MHD` / `Physics-Based` — no equations are solved by
  this package; GEMINI (external) does the first-principles work.
- `Models and Simulations: Data Guided` — the state is specified by configuration, not driven by
  observations.
- `Models and Simulations: Mission-Specific` and `Data Visualization: Mission-Specific` — AMISR is a
  ground-based facility, not a space mission.
- `Mission-related` (and `: Operations`) — a defensible case exists (the package is an AMISR-facility
  tool from the `amisr` GitHub organization, authored at SRI International which operates AMISR,
  funded in part by the AMISR cooperative agreement, and its documented use case #2 is designing and
  optimizing radar observational modes). Excluded because the category is defined as supporting a
  *space mission's* operations or ground system.
- `Data Processing and Analysis: Analysis` — the package synthesizes rather than analyses data; the
  derived quantities it computes (line-of-sight projection, MLT, error estimates) are generation
  steps, not analysis products.
- `Data Processing and Analysis: File Format Conversion` — sampling a model onto radar geometry is
  not a format conversion.
- `Data Processing and Analysis: Calibration` — no calibration is performed (`beam_ksys` is NaN).
- `Data Processing and Analysis: Spectrogram` / `Data Visualization: Spectrogram` — the RTI panel is
  range-versus-time, not a time-frequency representation.
- `Data Processing and Analysis: Data Access and Retrieval` — nothing is retrieved from a remote
  archive.
- `Data Visualization: Movies`, `: Line Plots` — no animation output; no 1D line plots.
- `Servers and Environments` — no server, container, or HPC component.

### 5. Related Region (RECOMMENDED)

- **Earth Atmosphere** — the coarse row of both fine rows below. Field 5 rule 5 lists every fine
  row together with the coarse row that contains it, because the Region filter does not inherit:
  without `Earth Atmosphere` the entry would be invisible to anyone browsing at that level.
- **Earth Ionosphere** — the package models and samples ionospheric plasma state parameters (Ne,
  Ti, Te, Vlos); the JOSS paper opens by describing AMISR as radars "used to study plasma dynamics in
  the ionosphere", and the README describes "a complete picture of ionospheric state parameters from
  discrete measurements".
- **Earth Auroral Subregion** — the three supported radars sit in the auroral zone and
  polar cap (PFISR at Poker Flat, Alaska; RISR-N/RISR-C at Resolute Bay, Nunavut), the JOSS paper
  motivates the package by "the radars' locations in regions that are key for
  magnetosphere-ionosphere coupling," and one of its cited use cases is inverting auroral E-region
  precipitating-electron spectra (Semeter & Kamalabadi 2005). This is a moderate-confidence
  inclusion based on the software's supported facilities and documented science use.

*Considered and excluded:* `Earth Thermosphere` — the modelled altitudes (100–500 km) are
thermospheric, but the package represents only the ionized component; no neutral thermosphere
parameters are produced.

### 6. Authors (MANDATORY)

Reconciled by identity-aware union across the HSSI record, `pyproject.toml`, `manuscript/paper.md`,
Crossref (JOSS), Zenodo and DataCite. Every source names Leslie Lamarche, the single author; no one
is dropped. The only other names found, Warrick Ball and Asti Bhatt, are rejected below.

**Author 1**
- **Name:** Leslie Lamarche
- **Author Identifier:** https://orcid.org/0000-0001-7098-0524
- **Affiliations:**
  - Organization: SRI International — https://ror.org/05s570m15
  - Organization: University of Alaska Fairbanks — https://ror.org/01j7nq853

- Corroboration: `manuscript/paper.md` front matter
  (`Leslie J. Lamarche`, `orcid: 0000-0001-7098-0524`, affiliation "SRI International, Menlo Park,
  CA, USA"); Crossref for the JOSS paper (`given: "Leslie J."`, `family: "Lamarche"`, same ORCID);
  `pyproject.toml` (`L. Lamarche <leslie.lamarche@sri.com>`); creator "Leslie Lamarche" on every
  Zenodo deposit and in DataCite (no ORCID or affiliation recorded there). Both organizations match
  the ROR identifiers shown.
- The peer-reviewed byline is "Leslie J. Lamarche", but the ORCID person record gives
  `given-names: "Leslie"` and `family-name: "Lamarche"` with no credit-name override, so `Leslie` /
  `Lamarche` is the right form (Field 6 rule 10); the middle initial appears only in the
  JOSS/Crossref byline.
- Both affiliations are corroborated by the author's own ORCID affiliation records:
  - **SRI International** — ORCID *employment*, department "Center for Geospace Studies", from
    2017-04-03 (ongoing). Matches the JOSS paper affiliation "SRI International, Menlo Park, CA, USA".
  - **University of Alaska Fairbanks** — ORCID *education*, department "Physics", Ph.D., 2013-09 to
    2017-02. This is the author's doctoral institution. It appears in no repository or publication
    source, but it is an authentic prior affiliation, not merely a plausible one.

**Considered and rejected:**

- **Warrick Ball is not an author.** He is a creator, with affiliation "University of Birmingham",
  on the v1.2.0 Zenodo deposit (`10.5281/zenodo.21908138`), and so on the concept DOI's DataCite
  record since v1.2.0. The GitHub integration evidently built that list from the repository's
  contributors, since the repository has no `.zenodo.json`, `CITATION.cff` or `codemeta.json`
  (checked at revision `8baaf296`). His only commits are `3bd27be` "Editorial tweaks for
  publication in JOSS" and `3de26ee` "revert a comma change now that I understood sentence"
  (2024-11-26, merged through PR #21, whose description reads "A few minor changes ahead of
  publication in JOSS following a successful review", link omitted). They touch only
  `manuscript/paper.md` and `manuscript/paper.bib`, so they
  are edits to the paper, not to the software. No other source names him: the `pyproject.toml`
  authors, the JOSS byline, the JOSS paper record (editor Monica Bobra, reviewers @rweigel and
  @peijin94) and the curated v1.1.8 deposit all list Lamarche alone. Field 6 rule 8 read literally
  admits any Zenodo creator, but this list is the commit graph relabelled, git history is never an
  attestation of authorship, and a site user would find a manuscript copy-editor listed as a
  software author out of place. Decided when v1.2.0 was recorded (October 2026). Do not re-add him
  from a later integration deposit unless a source the project maintains (`CITATION.cff`,
  `.zenodo.json`, package authors) names him. The only fielded ORCID match for him,
  `0000-0002-4773-1017`, has no link to this work (rule 14).
- **Asti Bhatt is not an author** (rule 7). She is co-author with Lamarche of the 2023 AGU abstract
  about the software (weighed in Field 27), but she appears in no software-metadata source
  (`pyproject.toml`, any Zenodo deposit, the JOSS byline) and has no commits.

### 7. Software Name (MANDATORY)
amisrsynthdata

- Matches the repository name, the `pyproject.toml` project name, the
  PyPI distribution name, and the console-script entry point.

### 8. Description (MANDATORY)

> This module provides tools to create synthetic data files for the AMISR (Advanced Modular Incoherent Scatter Radar) systems. The files are based on both a specified ionospheric state and a radar configuration. This can be used to generate synthetic data in the "SRI data format" both for the three existing AMISRs and for hypothetical future "AMISR-like" systems. Primarily, it was designed to help test the functionality of various inversion algorithms that attempt to create a complete picture of ionospheric state parameters from discrete measurements by creating a way to check the output of these algorithms against known "truth" data. Please note that this module does NOT attempt to simulate any aspect of fundamental ISR theory.

- **One word differs from the README.** `README.rst`, and the description as first submitted (until
  the July 2026 refresh), read "Advanced **Module** Incoherent Scatter Radar" (emphasis added), but
  the AMISR acronym expands to "Advanced **Modular** Incoherent Scatter Radar" (emphasis added);
  five independent authorities agree, including the author's own writing:
  1. the author's JOSS paper title — "amisrsynthdata: A Python package for generating synthetic data
     for the Advanced **Modular** Incoherent Scatter Radars" (emphasis added);
  2. Crossref's record for that paper (DOI 10.21105/joss.07248);
  3. the title of the software's v1.1.8 Zenodo deposit (`10.5281/zenodo.14174414`, edited during
     the JOSS review) and its DataCite record. Since v1.2.0 the concept DOI presents that release's
     integration title, `amisr/amisrsynthdata: v1.2.0`, which does not expand the acronym;
  4. the canonical SPASE observatory record `spase://SMWG/Observatory/AMISR`, whose `ResourceName` is
     "Advanced Modular Incoherent Scatter Radar (AMISR)";
  5. the PyHC registry description of this package.
- The error originates upstream in `README.rst`, so it is the author's own slip rather than a
  transcription error introduced during submission; correcting it here does not misrepresent the
  author's intent, and the package's own peer-reviewed paper uses the corrected form.
- **Everything else is byte-identical to the README sentence**: the description is the opening
  paragraph of `README.rst`, with the author's double spaces after sentences normalized to single
  spaces. Editorial intent is otherwise fully preserved.

### 9. Concise Description (OPTIONAL)
Module for generating synthetic AMISR data files

- **One word differs from the source.** The GitHub repository description, and the concise
  description as first submitted (until the July 2026 refresh), read "Module for generating
  syn**e**thetic AMISR data files" (emphasis added). Only that word differs; the rest of the
  string is byte-identical to the GitHub description.
- The typo is present upstream in the GitHub repository's own description field, so it is the
  author's rather than a submission artifact — but it is unambiguously a misspelling of "synthetic",
  not a stylistic choice, so correcting it preserves the author's intent rather than overriding it.
- This string is the **search-results preview** for the record. Left uncorrected, the preview
  misspelled the package's own core term, so the entry could not be matched on "synthetic" — the
  single most likely word a user would search for when looking for a synthetic-data generator.

### 10. Publication Date (RECOMMENDED)
2023-09-12

- **The date of first publication of the initial version**, which is what Field 10 asks for: "Date
  of first broadcast/publication." (the form's definition), "Used for the initial version of the
  software." (its instructions).
- Evidence: the earliest of the repository's GitHub releases is `v0.0.1`, `published_at:
  2023-09-12T22:24:53Z`. It is tagged as a pre-release on GitHub, but it is the first publicly
  published release of the software. The first non-pre-release, `v0.0.4`, followed one day later
  (`2023-09-13T19:31:39Z`) and was the first upload to PyPI (`0.0.4`, `2023-09-13T19:32:42`).
  `2023-09-13`, the first non-pre-release, was considered and rejected: a release published on
  GitHub is public whether or not it is marked pre-release, so `2023-09-12` is the first
  publication.
- **Why the record held `2024-11-17` until the July 2026 refresh:** it is DataCite's `Issued` date
  on the **concept** DOI (`10.5281/zenodo.12210900`). Zenodo advances the concept DOI's issue date
  to the newest version, so that value tracked v1.1.8 rather than the initial release (with v1.2.0
  it advanced again, to 2026-08-12). It was almost certainly supplied by the form's DataCite
  autofill. (For completeness, the software's first Zenodo deposit
  was later still — `v1.1.3` on 2024-06-21 — so no Zenodo-derived date can represent the initial
  release.)
- **Field 10 and Field 12 are legitimately different dates.** Field 10
  (`2023-09-12`) is when the software was *first* published; Field 12's Version Date
  (`2026-08-12`) is when the *current* version, v1.2.0, was released. A future reader should not
  "fix" either one to match the other.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

- Correct per Field 11 guidance (the DOI was obtained through the
  GitHub–Zenodo workflow); DataCite reports `publisher: "Zenodo"`.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.2.0
- **Version Date:** 2026-08-12
- **Version Description:**

  ```
  This minor release includes:
  - Removing the maximum cap for the required version of python
  - Altering the automatic unit tests to run on python 3.9-3.14
  ```

- **Version PID:** https://doi.org/10.5281/zenodo.21908138

- **v1.2.0 is the newest release** (read at revision `8baaf296413d2f529b7ab85561fe1546343c8e3d`,
  the head of `main`, which the lightweight tag `v1.2.0` points to): GitHub release `v1.2.0`,
  `published_at: 2026-08-12T18:12:29Z`, not a pre-release, target `main`; PyPI `1.2.0`, wheel and
  sdist uploaded 2026-08-12T18:12:53Z / 18:12:54Z, with `project_urls` pointing at this repository;
  `pyproject.toml` at the tag declares `version = "1.2.0"`; and the Zenodo integration deposit
  `10.5281/zenodo.21908138` carries `version: v1.2.0`. `v1.1.8` is an ancestor of `v1.2.0`, both on
  `main`'s lineage, and no commit follows the tag. Under Field 12 rule 3 the newer release replaces
  the stored row. The number keeps the leading `v` the stored number used, matching the tag; PyPI's
  `1.2.0` is the same release written without it, and neither form should be "fixed" to the other.
  The view API's `amisrsynthdata - v1.2.0` is a render-time prefix, not the stored number.
- **Superseded value.** HSSI held v1.1.8 until the v1.2.0 update in October 2026 (Version Date
  2024-11-17, Version PID
  `https://doi.org/10.5281/zenodo.14174414`, description "Minor release primarily to update
  documentation and how it is compiled on ReadTheDocs.  This should not introduce new
  functionality."). That description is v1.1.8's own release body; it is not carried onto v1.2.0.
- **Version Date** is the release event's UTC day: the GitHub release above, corroborated by the
  tagged commit (2026-08-12T18:10:18Z), the PyPI upload and the Zenodo deposit's
  `publication_date: 2026-08-12`. All sources agree. (The v1.1.8 row once carried 2024-12-02, that
  deposit's Zenodo `updated` timestamp from metadata edits during the JOSS review; it was corrected
  to the release day in July 2026. The v1.2.0 deposit was created and last modified on 2026-08-12,
  but a Zenodo date never overrides the release event.)
- **Version Description** is the GitHub release body, verbatim; the release title is only the tag,
  so the body is the source, and the Zenodo deposit's description reproduces it. Both items are kept
  because both tell a user which Pythons the release runs on: the first is the removal of the
  `<3.12` cap (`requires-python` went from `">=3.7,<3.12"` at v1.1.8 to `">=3.7"`), and the second
  is the tested range that `docs/source/installation.rst` now states to users ("This package has
  been tested with python versions 3.9-3.14."), not CI housekeeping. The body's CRLF line breaks are
  written as LF; the words are unchanged.
- **Also in the v1.1.8..v1.2.0 range but not in the notes, and correctly not recorded:** the
  dependency list moved from `pyproject.toml` into a new `setup.py` so Read the Docs can install
  the package without `apexpy`; GitHub Actions versions were raised; a unit-test tolerance was
  loosened; and the JOSS editorial edits to `manuscript/` and documentation-example updates made on
  `develop` in November–December 2024 were merged. None changes what the software does, and no file
  under `src/` changed.
- **Version PID** is the version DOI of exactly this release: it is in the concept's `HasVersion`
  list, the deposit's `version` is `v1.2.0`, its `IsSupplementTo` link is
  `https://github.com/amisr/amisrsynthdata/tree/v1.2.0`, and the DOI resolves. Never the concept
  DOI, which is Field 2.
- Only the latest version is recorded, as before; earlier releases are deliberately not recorded
  as separate version rows.
- **This Version Date (`2026-08-12`) and Field 10's Publication Date (`2023-09-12`) are supposed to
  differ.** Field 12 dates the *current* version, v1.2.0; Field 10 dates the *first* publication of
  the software (`v0.0.1`). Neither should be "fixed" to match the other.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

- `Python 3.x` is well evidenced at revision `8baaf296` (v1.2.0): the
  package is pure Python (`requires-python = ">=3.7"`; v1.2.0 removed the former `<3.12` cap), every
  source file under `src/amisrsynthdata/` is `.py`, the unit-test CI matrix runs Python 3.9–3.14,
  and `docs/source/installation.rst` states "This package has been tested with python versions
  3.9-3.14." Python 2 is not targeted anywhere.
- `Other`, which the record carried until the July 2026 refresh, does not describe an
  implementation language for this package and should not be restored:
  - **No non-Python implementation source exists.** The entire package is Python. The other
    tracked files (at revision `8baaf296`) are configuration (YAML, TOML), documentation and its
    Sphinx build files (reStructuredText, a `Makefile`, `make.bat`, a requirements list), the JOSS
    manuscript (Markdown and BibTeX), two HDF5 data files (the bundled beamcode table and a test
    fixture), PNG figures, the licence and one Jupyter notebook. None of these is a second
    implementation language, and none is what a reader would expect "Other" to denote.
  - **`Other` is almost certainly a language-detection artifact.** GitHub reports the repository's
    primary language as "Jupyter Notebook" solely because `tutorial.ipynb` outweighs the Python
    source in its byte count; a submission-time autofill mapping that unrecognized label onto
    `Other` explains the value exactly. It carries no information about how the software is
    written, and its presence implies — wrongly — that part of the package is implemented in
    something other than Python.
  - Without it the field says precisely what is true: amisrsynthdata is a pure-Python 3 package.

### 14. Reference Publication (OPTIONAL)
https://doi.org/10.21105/joss.07248

- **Verified against Crossref** (JOSS DOIs are registered with Crossref, not DataCite —
  `api.datacite.org` returns 404 for this DOI, which is expected and not a problem):
  title "amisrsynthdata: A Python package for generating synthetic data for the Advanced Modular
  Incoherent Scatter Radars"; container *Journal of Open Source Software*; volume 9, issue 104,
  page 7248; published 2024-12-05; publisher The Open Journal; sole author Leslie J. Lamarche with
  ORCID `0000-0001-7098-0524` and affiliation "SRI International, Menlo Park, CA, USA"; Crossref
  `relation.has-review` points at `openjournals/joss-reviews#7248` and
  `relation.references` cites the software DOI `10.5281/zenodo.14174414`.
- In-repo corroboration: the manuscript source is `manuscript/paper.md` with `manuscript/paper.bib`,
  and `.github/workflows/draft-pdf.yml` builds the JOSS PDF.
- This is exactly what Field 14 asks for: "The DOI for the publication describing the software"
  (the form's definition), entered as "the DOI for the publication describing the software (e.g., a
  JOSS paper)" (its instructions). The record lacked it until the July 2026 refresh.

### 15. License (RECOMMENDED)
- **License:** GNU General Public License v3.0 or later
- **License URI:** https://spdx.org/licenses/GPL-3.0-or-later.html

- The name is the exact name of the vocabulary's GNU GPL v3.0 row. Evidence at revision
  `8baaf296`: `LICENSE` is the
  full, unmodified GPL-3.0 text (unchanged since 2021); no source file carries a licence header;
  `pyproject.toml` declares `license = { file = "LICENSE" }` and the unversioned classifier
  `License :: OSI Approved :: GNU General Public License (GPL)`.
- **The repository makes no "only" / "or later" election, and the Zenodo deposits disagree on it.**
  The v1.1.8 deposit (`10.5281/zenodo.14174414`, edited by hand during the JOSS review) records
  Zenodo `license.id: gpl-3.0-or-later` (DataCite `"GNU General Public License v3.0 or later"`,
  `rightsIdentifier: gpl-3.0+`); the v1.2.0 integration deposit records `gpl-3.0`, so since v1.2.0
  the concept DOI's DataCite `rightsList` reads `"GNU General Public License v3.0 only"`. Under
  Field 15 rule 4 either election maps to this row (the vocabulary has no GPL-3.0-only row), so the
  deposits' disagreement is not a reason to change the value.
- The License URI above is that row's own `url`; HSSI stores no per-software licence URI.
  (DataCite instead carries `https://www.gnu.org/licenses/gpl-3.0-standalone.html`; both denote
  the same licence, and the vocabulary row's URL is used to avoid gratuitous drift.) GitHub's
  repository API reports the coarser `GPL-3.0`, which is consistent.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

Stored identities are lower-case (the view renders them Title Case — `Amisr`, `Data`, `Synthetic` —
which is a rendering artifact and is not reproduced here).

- amisr
- data
- synthetic
- ionosphere
- incoherent scatter radar
- radar
- electron density
- ion temperature
- electron temperature
- plasma parameters
- simulation
- pyhc package

- `amisr`, `data` and `synthetic` are the project's declared keywords (`pyproject.toml`:
  `keywords = ["AMISR", "synthetic", "data"]`), present in the record at its first refresh.
- `ionosphere` through `simulation` describe the four ISR parameters the package generates
  (`generate_radar_measurements()` returns Ne, Ti, Te, Vlos) and its subject matter. One keyword
  per entry, lower case, per the field guidance.
- `pyhc package` (rendered `Pyhc Package`) is HSSI's catalogue-wide keyword for official PyHC
  packages, required by Field 16 rule 15 whatever the other sources say. amisrsynthdata is listed in
  the PyHC registry's `_data/projects.yml` (registry commit `7bc0bef6`, 2026-10-01), so the keyword
  belongs on this record. It was added to the live record after the July 2026 refresh, which is why
  that refresh did not list it. Write it exactly `pyhc package`, never a variant.
- Considered and rejected: `python`, `hdf5`, `space physics`, `magnetic apex coordinates` — each is
  already carried by a dedicated field (13, 18/19, 5, 4) and would only duplicate it (Field 16
  rule 6, which governs additions). Stored keywords that overlap another field, such as
  `ionosphere` and `simulation`, are kept under rule 13.

### 17. Data Sources (OPTIONAL)
Not found — intentionally empty.

- amisrsynthdata retrieves no data from any archive or
  service: its inputs are a local YAML configuration file, a beamcode table shipped inside the
  package (`src/amisrsynthdata/beamcodes.h5`), and optionally a local GEMINI model output directory.
  There is no HTTP/FTP/S3/HAPI/CDAWeb/Madrigal client anywhere in the source.
- `Madrigal` was explicitly considered and rejected: `README.rst` lists "Madrigal data format" under
  **Limitations** — "Currently files are only generated in the SRI data format."
- `Observatory/Mission-specific` was considered because Field 32 normally cross-lists with it. It is
  **not** selected: that value denotes an observatory-specific *data input source*, and this package
  ingests no observational data at all. Selecting it would misrepresent the software as an AMISR
  data reader.

### 18. Input File Formats (RECOMMENDED)
- HDF5
- Other

- `HDF5` — `radar.py` opens the packaged beamcode table with `h5py.File(bc_file, 'r')` and indexes
  it by radar abbreviation; the optional GEMINI ionosphere reads GEMINI's HDF5 output through
  `gemini3d.read.grid()` / `gemini3d.read.frame()` in `state_functions/gemini_utils.py`.
- `Other` — the package's primary user input is a **YAML** configuration file
  (`yaml.safe_load` in `syntheticdata.main`; see `example_synth_config.yaml` and
  `docs/source/configfile.rst`). YAML has no row in the `FileFormat` vocabulary, so
  `Other` is the correct representation. Noted explicitly here so a reader knows what `Other` means.

### 19. Output File Formats (RECOMMENDED)
- HDF5
- Other

- `HDF5` — `SyntheticData.create_hdf5_output()` writes the synthetic data file with `h5py`,
  building the AMISR "SRI data format" group structure (`/BeamCodes`, `/FittedParams`,
  `/FittedParams/FitInfo`, `/NeFromPower`, `/Calibration`, `/Geomag`, `/MSIS`, `/ProcessingParams`,
  `/Site`, `/Time`). `tests/synthetic_data.h5` is a checked-in example output.
- `Other` — the optional summary plots are written as **PNG** image files
  (`fig.savefig(output_prefix + 'ne.png')` and equivalents for Ti, Te, Vlos). PNG has no row in the
  `FileFormat` vocabulary, hence `Other`.

### 20. Operating System (RECOMMENDED)
- Operating System Independent

- `pyproject.toml` declares the classifier `Operating System :: OS Independent`; `README.rst` says
  "The amisrsynthdata package is pure python and can be installed with pip:" and
  `docs/source/installation.rst` says "The amisrsynthdata package is pure python and can be
  installed easily with pip." No compiled
  extension, shell script, or platform-specific path handling exists in the package.
- The exact row name is `Operating System Independent` (spelled out); `OS Independent` is not a
  row and would be rejected.
- Note: CI (`.github/workflows/unit-tests.yml`) exercises only `ubuntu-latest`, so Linux is the only
  *tested* platform, but the package makes no platform-specific claims. The practical limit is its
  dependency `apexpy`, which PyPI distributes mainly as a source distribution that needs a Fortran
  compiler to build (the latest release, 2.1.1, adds a single macOS x86-64 wheel; `setup.py` notes
  that "The apexpy dependency cannot install on RTD due to requiring a FORTRAN compiler"). That
  affects installation on essentially every platform and does not tie the package to an operating
  system.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

- Pure-Python package with no compiled component, no
  SIMD/GPU code, no MPI, and no architecture-specific dependency pins.

### 22. Related Phenomena (OPTIONAL)
Not found — no applicable row exists in the vocabulary.

- The `Phenomena` vocabulary has exactly 7 rows (read 2026-10-27) —
  Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares,
  Solar Wind, X-ray emission — and all of them are solar/heliospheric. The phenomena this package
  actually represents (travelling ionospheric disturbances, polar-cap patches, plasma density
  gradients, auroral E-region precipitation, Chapman/Epstein layers) have no rows. The field is a
  **closed** vocabulary, so inventing entries would fail submission; per the field guidance those
  concepts belong in Keywords instead (Field 16 already carries the ionospheric terms).

### 23. Development Status (RECOMMENDED)
Active

- `Active` is the repostatus.org term for a project that "has reached a stable, usable state and is
  being actively developed". Decided by Field 23 rule 6, since rules 1–5 do not fire:
  - no move: the README names no successor, and `github.com/amisr/amisrsynthdata` is the repository
    itself, not a redirect;
  - not archived or disabled (GitHub API, read 2026-10-27);
  - no repostatus.org badge (the README's only images are two science figures) and no status
    statement; `README.rst` and `CONTRIBUTING.rst` still invite contributions;
  - the software reached a stable, usable state long ago: releases on PyPI since 2023 and a JOSS
    paper (2024-12-05).
- **Dated anchors for rule 6** (re-apply the rule from these, not from an elapsed span): the last
  commit on the default branch `main` is `8baaf296413d2f529b7ab85561fe1546343c8e3d`, committed
  2026-08-12T18:10:18Z; the last release is v1.2.0, published 2026-08-12, and the last PyPI upload
  is 1.2.0 on the same day. Under six months before 2026-10-27, so `Active`. From 2027-02-12 the
  middle band keeps a stored `Active`; from 2028-08-12, with no newer commit, rule 6 gives
  `Inactive`.
- **Superseded value.** HSSI held `Inactive` until the v1.2.0 update in October 2026. It was
  chosen in July 2026, when the
  default branch had been quiet since November 2024 and the only later commits (on `develop` and
  `joss`, through 2024-12-03) were JOSS-review and Read the Docs fixes. Development resumed with the
  v1.2.0 work merged to `main` in August 2026, which supersedes it.

### 24. Documentation (RECOMMENDED)
https://amisrsynthdata.readthedocs.io

- Confirmed by `README.rst` ("Full documentation for amisrsynthdata is available on ReadTheDocs",
  rendered text of a link) and `.readthedocs.yaml`. Installation instructions live at
  `docs/source/installation.rst`, satisfying the field's "including installation instructions"
  requirement.

### 25. Funder (OPTIONAL)

- **Organization:** U.S. National Science Foundation — https://ror.org/021nxhr62
- **Organization:** National Aeronautics and Space Administration — https://ror.org/027ka1x80

- Source: the Acknowledgements section of
  `manuscript/paper.md` — "The AMISR facilities are funded by the National Science Foundation
  through cooperative agreement AGS-1840962 to SRI International. The development of
  `amisrsynthdata` was funded in part by NASA awards 80NSSC21K0458, 80NSSC21K1354, and 80NSSC21K1318
  and NSF award 2027300."
- Both organization names and ROR identifiers use HSSI's canonical organization identities. The
  canonical NSF name is "U.S. National Science Foundation".
- SRI International is deliberately **not** listed as a funder: it is the award recipient, not the
  funding agency.

### 26. Award Title (OPTIONAL)

- **Award Title:** Advanced Modular Incoherent Scatter Radar (AMISR) Operations and Maintenance
  **Award Number:** AGS-1840962
- **Award Title:** Characterizing High-latitude Ionospheric Fluid Turbulence and Radio Scintillation with New Observations and Data-Driven Modeling
  **Award Number:** 2027300
- **Award Title:** National Aeronautics and Space Administration grant
  **Award Number:** 80NSSC21K0458
- **Award Title:** National Aeronautics and Space Administration grant
  **Award Number:** 80NSSC21K1354
- **Award Title:** National Aeronautics and Space Administration grant
  **Award Number:** 80NSSC21K1318

- Award numbers are exactly as acknowledged in
  `manuscript/paper.md`: "The AMISR facilities are funded by the National Science Foundation through
  cooperative agreement AGS-1840962 to SRI International. The development of `amisrsynthdata` was
  funded in part by NASA awards 80NSSC21K0458, 80NSSC21K1354, and 80NSSC21K1318 and NSF award
  2027300." That acknowledgement is the authoritative basis for including all five.
- Both NSF titles were retrieved from the NSF Awards API and are authoritative. Award `1840962` —
  "Advanced Modular Incoherent Scatter Radar (AMISR) Operations and Maintenance", awardee SRI
  International, 2019-03-01 to 2026-11-30. Award `2027300` — awardee SRI International, 2020-09-01
  to 2024-08-31, whose abstract concerns the Resolute Bay incoherent scatter radar (RISR), directly
  relevant to this package; its full title is preserved verbatim below.
- The award number is recorded as `AGS-1840962`, the form used by the author; NSF's own award
  identifier for the same cooperative agreement is `1840962` (AGS is the NSF division prefix).

**NSF 2027300: the stored title is shortened to fit HSSI's schema.** The two strings below are given
unwrapped so there is no ambiguity about either one.

*Authoritative NSF award name (152 characters) — the real title, preserved here for the record:*

```
Collaborative Research: Characterizing High-latitude Ionospheric Fluid Turbulence and Radio Scintillation with New Observations and Data-Driven Modeling
```

*Value stored in HSSI (128 characters) — the authoritative title minus its prefix:*

```
Characterizing High-latitude Ionospheric Fluid Turbulence and Radio Scintillation with New Observations and Data-Driven Modeling
```

- The **only** difference is the removal of the leading `Collaborative Research: ` (24 characters,
  including the trailing space). That prefix is NSF's marker for a collaborative proposal — an
  administrative label on the award, not part of the scientific title — so dropping it loses no
  scientific meaning, and the award number `2027300` remains the unambiguous identifier either way.
- **Why it had to be shortened: a hard HSSI schema constraint.** `Award.name` is a
  `CharField(max_length=128)`, so 152 characters cannot be stored. The stored value above is exactly
  128 characters (128 UTF-8 bytes, pure ASCII, no leading or trailing whitespace) — it fits with
  zero headroom, so it must not be reflowed, re-prefixed, or otherwise edited.
- **This is a technical accommodation, not an editorial preference.** If the column is widened, the
  full 152-character authoritative title above is the value to restore.

**The three NASA awards were resolved, but NASA assigns them no title.** Each was confirmed against
the USAspending award search, all three awarded by the National Aeronautics and Space
Administration:

| Award number | Recipient | Period of performance |
|---|---|---|
| `80NSSC21K0458` | SRI International | 2021-03-01 → 2026-02-28 |
| `80NSSC21K1354` | Embry-Riddle Aeronautical University, Inc. | 2021-09-01 → 2026-08-31 |
| `80NSSC21K1318` | New Jersey Institute of Technology | 2021-07-15 → 2027-07-14 |

- **Why the generic name rather than a derived one.** USAspending exposes each award's *abstract*,
  not a title: all three are all-caps prose, and `80NSSC21K1318`'s runs to over 3,000 characters.
  An abstract is not a title, and condensing one into a title would invent a designation NASA never
  assigned. The name `National Aeronautics and Space Administration grant` follows HSSI's
  established convention for title-less NASA grants. The **award number** carries the identifying
  information in every case.
- Two of the three NASA awards are prime-funded at Embry-Riddle Aeronautical University and the New
  Jersey Institute of Technology rather than at SRI International, so the author was presumably a
  collaborator or co-investigator on those. The paper's acknowledgement remains the basis for listing
  them; the funding relationship itself is not in doubt.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2026JA035137

- **The LLITED paper is included.** Swanson, D. J., Clemmons, J. H., Liu, H., Bishop, R.,
  Debchoudhury, S., Barjatya, A., & Bhatt, A. (2026), "High Latitude Thermosphere and Ionosphere
  Density Response to the May 2024 Geomagnetic Storm Observed by the LLITED CubeSat Mission",
  *Journal of Geophysical Research: Space Physics*, `10.1029/2026JA035137`. A peer-reviewed journal
  article is an eligible publication (Field 27, *Eligible publication types*), and this one uses
  the software: its Availability Statement says "PFISR plotting routines were adapted from publicly
  available code (Lamarche, 2024)", and that reference is the amisrsynthdata JOSS paper. So the
  paper's own PFISR figures come from code adapted from this software's plotting routines, and the
  paper credits that deliberately in its data and software statement. That is substantive use
  (rule 5), not a passing citation (rule 6), and it is still news: it is the only publication found
  citing the software. As an entry already on the record it is kept under rule 7. The words
  "amisrsynthdata" and "synthetic" do not appear in the article's body text, only in its
  reference-list entry for the JOSS paper; the credit is the citation. Its Acknowledgments credit no
  software, and its NASA grant `80NSSC17K044` funds that study, not this software, so it is not a
  Field 25/26 value. Wiley refuses scripted fetches of the article (403), but it is open access and
  readable in a browser.
- **The 2023 AGU abstract is excluded under rule 1**, because a conference or meeting abstract is
  never an eligible publication (Field 27, *Eligible publication types*): Lamarche, L. J. & Bhatt,
  A., "amisrsynthdata: Designing Expandability into Packages", AGU Fall Meeting 2023 (AGU23), poster
  SH33E-3087 in the session "Implementations in Python for Solar and Space Physics Poster", dated
  2023-12-13 (ADS `2023AGUFMSH33E3087L`, permalink
  `https://ui.adsabs.harvard.edu/abs/2023AGUFMSH33E3087L/abstract`; AGU meeting record
  `Paper/1421366`). Its subject is this software and its first author is the software's author, so
  a deposit of the poster itself would enter under rule 3; the abstract cannot. It was listed here
  when v1.2.0 was recorded (October 2026), under an earlier version of the rule that admitted
  conference abstracts.
- **No deposit of the poster was found (searched 2026-10-28), so nothing replaces the abstract:**
  - Zenodo: creator-keyed searches on `Lamarche, Leslie`, `Leslie Lamarche`, `Lamarche, L`, the
    ORCID `0000-0001-7098-0524` and `Bhatt, Asti` together list the author's papers, datasets and
    software deposits, including every amisrsynthdata release (the positive control), but no poster
    or presentation. Title searches for "Designing Expandability" find nothing (control: a title
    search for "Ion heating in the polar cap" finds that paper; a nonsense token finds nothing), and
    poster-type searches for AMISR, PFISR and RISR find no poster by the developers.
  - ESS Open Archive, through Crossref (`10.22541/essoar.*` and `10.1002/essoar.*`): author and
    title queries return Lamarche's other ESSOAr preprints (the polar-cap patch studies and the
    MANGO network paper, the positive control) but nothing on amisrsynthdata.
  - The AGU23 meeting record itself: typed "Abstract", presented as an onsite poster, with its
    iPoster URL, ESS Open Archive upload, ePoster, DOI, file and media fields all empty. No other
    record in session SH33E has those fields populated either, so the empty fields are consistent
    with no deposit but do not prove it on their own.
  - DataCite and OpenAlex title searches find nothing (DataCite control:
    `titles.title:amisrsynthdata` finds the software's deposits).
  - The repository (`main`, `develop` and `joss`) and its documentation mention no AGU poster,
    deposit or DOI for it.

  A later refresh should add the poster under rule 3 only if a deposit of the poster itself
  appears.
- HSSI held no related publications before October 2026.
- The publication that *describes* the software is the JOSS paper, which belongs in Field 14 and is
  recorded there (rule 2); Field 27 is for *other* publications that describe, cite, or use the
  software.
- `manuscript/paper.bib` was reviewed in full and every entry was rejected for this field, because
  each is background material cited **by** the paper rather than a publication about
  amisrsynthdata, and all of them predate the software:
  Kelly & Heinselman 2009 (`10.1016/j.jastp.2009.01.009`, PFISR initial results);
  Heinselman & Nicolls 2008 (`10.1029/2007RS003805`); Nicolls et al. 2014
  (`10.1002/2014RS005519`); Lamarche et al. 2020 (`10.1029/2019JA027112`); Semeter & Kamalabadi 2005
  (`10.1029/2004RS003042`) — these four are the inversion/interpolation algorithms the synthetic
  data is meant to validate; Zettergren & Snively 2015 (`10.1002/2015JA021116`, the GEMINI model);
  National Research Council 2013 (`10.17226/13060`, the decadal survey); plus the software-tool
  citations for numpy, h5py, pymap3d, matplotlib and cartopy.
- **Literature search, 2026-10-27 to 2026-10-28, covering all dates** (no earlier literature
  search had been recorded):
  - ADS full text `full:"amisrsynthdata"` finds only the JOSS paper and the AGU abstract (the
    control `pyspedas` returns hits);
  - ADS `citations()` of the JOSS paper finds only the LLITED paper, and of the AGU abstract none;
  - Crossref's cited-by count and OpenAlex `cites:` each give the LLITED paper alone;
  - an OpenAlex search for `amisrsynthdata` finds only the JOSS paper (controls: `pyspedas`
    returns hits, a nonsense token none);
  - Semantic Scholar lists the same single citation;
  - DataCite reports no citations of the concept DOI.

  A later refresh needs to look only for publications after 2026-10-28.

### 28. Related Datasets (OPTIONAL)
Not found.

- The package consumes no published dataset. Its only bundled
  data are the AMISR beamcode tables in `src/amisrsynthdata/beamcodes.h5` (package data, not a
  citable dataset) and the test fixture `tests/synthetic_data.h5`. Optional GEMINI input is model
  output the user generates or supplies locally; no DOI-bearing dataset is referenced anywhere in
  the repository or documentation.

### 29. Related Software (OPTIONAL)

- **apexpy** — https://github.com/aburrell/apexpy

- apexpy qualifies as a *domain-specific* dependency whose presence characterizes the software:
  `src/amisrsynthdata/ionosphere.py` does `from apexpy import Apex` and constructs
  `Apex(date=starttime)`; `syntheticdata.py` calls `geo2apex` and `convert(..., 'geo', 'mlt', ...)`
  to write magnetic coordinates and magnetic local time into the output product;
  `state_functions/velocity.py` uses the shared `apex` object for its `uniform_mlat_aligned` state
  function. It is also the dependency the documentation singles out as installation-critical
  (`docs/source/installation.rst` devotes a paragraph to apexpy install failures). This is a
  heliophysics-specific library, not generic infrastructure.

**Considered and excluded** (audit trail):

- `numpy`, `h5py`, `pyyaml`, `matplotlib`, `cartopy`, `importlib_resources`, `pytest` — Tier A
  generic scientific-Python/tooling stack. Being a dependency is not a relationship worth recording;
  each would read identically for most packages in HSSI.
- `pymap3d` (https://github.com/geospace-code/pymap3d, JOSS `10.21105/joss.00580`) — a genuinely
  important dependency (it implements essentially all of the radar geometry: `aer2geodetic`,
  `aer2enu`, `enu2uvw`, `uvw2enu`, `enu2geodetic`, `geodetic2enu`). Excluded nonetheless because it
  is a general terrestrial geodesy/coordinate library that would be equally at home in an aviation,
  surveying or mapping application — generic geospatial infrastructure by the field's own test, not
  a heliophysics peer tool. `pymap3d` was weighed and not added for the reason above.
- No predecessor, fork parent, or similar-purpose package is identified anywhere in the repository.
  Other AMISR/ISR simulators exist in the wild, but nothing in this repository references one, and
  inventing a "similar tool" link would not be evidence-based.

### 30. Interoperable Software (OPTIONAL)

- **PyGemini** — https://github.com/gemini3d/pygemini

- This is a demonstrated data exchange with a named heliophysics domain tool, not a dependency
  claim. Specific evidence:
  - `src/amisrsynthdata/state_functions/gemini_utils.py` imports
    `gemini3d.grid.gridmodeldata.model2pointsgeogcoords` and `gemini3d.read`, and its
    `ModuleNotFoundError` handler names the package and its URL verbatim: "the optional module
    pygemini (https://github.com/gemini3d/pygemini) must be installed."
  - `gemini_helper.query_model()` calls `read.grid()` and `read.frame()` on a GEMINI output
    directory and interpolates the GEMINI model volume onto arbitrary geodetic points.
  - Three user-selectable state functions consume that output — `Density.gemini`,
    `Temperature.gemini` and `Velocity.gemini` — so a user can drive amisrsynthdata directly from a
    GEMINI run via the configuration file.
  - `docs/source/installation.rst`: "Utilizing output from the GEMINI non-linear ionospheric
    dynamics model to specify the ionospheric state requires pygemini to be installed." (rendered
    text; the link target on "pygemini" is omitted)
  - `docs/source/usage.rst` benchmarks a GEMINI-driven "complex case", and the JOSS paper's third
    figure (`docs/synthdata_gemini_plot.png`) shows synthetic AMISR data generated from GEMINI
    output, citing Zettergren & Snively 2015 (`10.1002/2015JA021116`).
- PyGemini is the Python interface to the GEMINI model (https://github.com/gemini3d/gemini); the
  repository interoperates specifically through the `gemini3d` Python package, so PyGemini is the
  correct entry.
- **Considered and excluded:** everything in Field 29's exclusion list, for the same reasons —
  in particular `h5py` (Tier B: used for plain file I/O, with no documented interchange contract)
  and `apexpy` (a coordinate dependency used internally; recorded in Field 29 instead, since no data
  is exchanged in either direction).

### 31. Related Instruments (OPTIONAL)
Not found; represented at the observatory level instead (see Field 32).

The package unambiguously targets three specific instruments — the README says it generates data
"for the three existing AMISRs", and `src/amisrsynthdata/beamcodes.h5` contains exactly three
beamcode tables keyed by radar abbreviation: **PFISR** (481 beams), **RISR-C** (3277 beams) and
**RISR-N** (3277 beams), looked up by `Radar.beams_from_beam_codes()` via
`h5[self.radar_abbrev]`. `docs/source/configfile.rst` footnote 2 confirms this is the complete set:
"If a non-AMISR site is listed (not PFISR, RISR-N, or RISR-C), you will not be able to specify beams
by their beamcodes …" So these three pass the relevance gate decisively.

They do **not**, however, resolve in the controlled vocabulary. The HSSI instrument vocabulary was
searched case-insensitively and word-anchored across `name`, `abbreviation`, `identifier` and
`definition` (re-run 2026-10-27, with `SUVI` as a positive and a nonsense token as a negative
control) for `pfisr`, `risr`, `amisr`, `poker`, `resolute`, `incoherent` and `isr`:

- `pfisr`, `risr`, `RISR-N` and `RISR-C` match **no instrument row**; the only row that names them
  is the AMISR observatory row itself, in its definition.
- The `poker` and `resolute` instrument matches are all *co-located but unrelated* facilities —
  magnetometers (`SMWG/Instrument/Ground/Poker.Flat/Magnetometer`,
  `SMWG/Instrument/WDC/Resolute/Magnetometer`, THEMIS GBO and WDC Kyoto rows), aurora cameras and
  all-sky imagers, and an MF radar. None is an incoherent scatter radar and none may be substituted.
- The incoherent scatter radars that do have instrument rows are other facilities: Millstone Hill
  (`SMWG/Instrument/MEASURE/Millstone.Hill/ISR`) and EISCAT's Tromsø, Kiruna, Sodankylä and
  Svalbard radars (IUGONET and CNES rows).

Per the Field 31 resolution ladder this is **rule 4**: no instrument row exists, but the platform
does, so the association is made at the **observatory** level in Field 32. The canonical SPASE
record for that observatory explicitly encompasses all three radars — `spase://SMWG/Observatory/AMISR`
states "The first AMISR face was deployed in Poker Flat, Alaska in 2006 (the Poker Flat ISR, or
PFISR), and the remaining two faces were deployed in Resolute Bay, Nunavut, Canada (RISR-N and
RISR-C)" — so no coverage is lost by the substitution. **No name is emitted without a SPASE
identifier** (ladder rule 6).

### 32. Related Observatories (OPTIONAL)

- **Observatory Name:** Advanced Modular Incoherent Scatter Radar
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/AMISR

Until the July 2026 refresh the record pointed at a duplicate `.html` form of this identifier. The
two identifiers describe the same observatory, and four independent grounds select the bare row
above:

1. **Canonical SPASE identifier.** `https://spase-metadata.org/SMWG/Observatory/AMISR.xml` returns
   `<ResourceID>spase://SMWG/Observatory/AMISR</ResourceID>` — the bare form, with no `.html`. The
   `.html` variant is a web-page URL, not the resource ID.
2. **The `.html` identifier was a duplicate web-page form.** It had a bare twin for the same SPASE
   resource; the resolution ladder treats such twins as one resource and prefers the bare
   identifier.
3. **Correct spelling.** The `.html` row's name said "Advanced **Module** Incoherent Scatter
   Radar" (emphasis added); the authoritative SPASE `ResourceName` is "Advanced **Modular**
   Incoherent Scatter Radar (AMISR)" (emphasis added), as is the author's own JOSS paper title. (The
   README makes the same one-word error; see Field 8.)
4. **Correct name/abbreviation split.** The selected row stores the acronym in `abbreviation`
   (`"AMISR"`), which HSSI renders as `name (abbreviation)` — reproducing the SPASE `ResourceName`
   exactly. The `.html` row baked the parenthetical into `name` and left `abbreviation` empty.

Relevance is not in doubt: the software is purpose-built for AMISR (README, JOSS paper title,
`amisr` GitHub organization, AMISR-specific beamcode tables, AMISR "SRI data format" output), so a
user searching HSSI for `observatory:"AMISR"` would certainly expect it back. Per Field 31, this
single observatory row also carries the association for all three supported radars, since the SPASE
record itself names PFISR, RISR-N and RISR-C.

Catalogue-wide consolidation of `.html` rows is separate vocabulary curation; this record uses the
canonical ResourceID.

### 33. Logo (OPTIONAL)
Not found.

- No logo file, badge image, or logo URL exists in the
  repository. The only images are scientific figures (`docs/synthdata_summary_ne.png`,
  `docs/synthdata_gemini_plot.png`, `manuscript/amisr_fov.png`).
- amisrsynthdata **is** listed in the PyHC project registry
  (`heliophysicsPy/heliophysicsPy.github.io`, `_data/projects.yml`), but that registry carries no
  per-project logo — `img/project_logos/` holds only funder logos (NASA, NSF) — so no curated PyHC
  logo is available and "Not found" remains correct.

---

## Record notes

- Field 10 dates the first published release (`v0.0.1`, 2023-09-12), while Field 12 dates the current
  version (`v1.2.0`, 2026-08-12). These dates describe different events and are intentionally
  different.
- Field 13 contains only `Python 3.x`. The repository is pure Python; `Other` would describe the
  Jupyter notebook detected by GitHub rather than an implementation language.
- Field 26 stores NSF award `2027300` without its `Collaborative Research: ` prefix because the full
  authoritative title exceeds HSSI's 128-character award-name limit. The full title is preserved
  with the field.
- Field 32 uses the bare SPASE ResourceID for AMISR rather than its duplicate `.html` web-page form.
- Field 6 stores `Leslie Lamarche`, matching the author's ORCID record; the middle initial appears
  only in the JOSS/Crossref byline.
