# HSSI Metadata Extraction Results

**HSSI Software ID:** 40b44149-d3f3-45a5-8d44-424b4c886b7a
**Repository:** https://github.com/space-physics/lowtran
**Source Revision:** 5b8d38714b204eaa12595f5f15e2babec1dbdfb5
**Extraction Date:** 2026-09-04
**Validation Date:** 2026-09-05
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

This repository is two things at once, and several fields turn on which of the two the metadata
describes.

1. A **vendored third-party program**: `src/lowtran/fortran/lowtran7.f` (19086 lines) is the U.S. Air
   Force Geophysics Laboratory's LOWTRAN 7 radiative-transfer code, whose own header reads
   `C     LOWTRAN7  (LAST REVISED FEB 1 1992)   REVISION 4.2` and names eight AFGL-era authors.
   `archive/` holds twelve further files from the same 1994 distribution, alongside model card decks
   and retired CI configuration.
2. A **first-party wrapper** by Michael Hirsch: the Python package under `src/lowtran/`, the MATLAB
   package `+lowtran/`, the CMake/f2py build glue, and a Fortran CLI test harness in `test/`.

The HSSI entry describes the *distributed software* — the wrapper plus the model it ships — which is
why the author list holds one name while the science credit for the underlying model belongs to the
AFGL team (Field 6), and why the programming-language answer depends on an explicit criterion
(Field 13).

`.gitattributes` marks exactly `src/lowtran/fortran/*` and `archive/*` as `linguist-vendored`, so the
first-party Fortran in `test/` sits outside both globs. That directive governs GitHub's language
statistics only; it is not an attestation about what the installed package contains.

Three README references are stale at this revision and are upstream's to fix, not ours: the gallery
link `./doc/txgnd2space.png` (the file is `gfx/txgnd2space.png`), and, in the "Reference" section,
`reference/lowtran7.10.f` and `reference/lowtran7.13.f` (the files are `archive/lowtran7.10.f` and
`archive/lowtran7.13.f`). They are recorded here so a later refresh does not read them as evidence of
files that do not exist.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This placeholder is the catalogue convention for an entry not originally submitted by this workflow.

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.598359

This is the Zenodo **concept** DOI, which always resolves to the newest deposited version. The Zenodo
API confirms `conceptdoi: 10.5281/zenodo.598359` on both the v1.0 record (`10.5281/zenodo.213475`)
and the v3.1.0 record (`10.5281/zenodo.7654888`).

The README badge cites the **version** DOI for v1.0 (`10.5281/zenodo.213475`) rather than the concept
DOI. That is a rendering choice by the author, not a conflict: a concept DOI is the correct Field 2
value because the software's identity outlives any one release, and the version DOI is separately
recorded on Field 12.

Considered and not selected: clearing Field 2 (which would remove the software citation block from
the entry's page entirely) and moving the DOI to Fields 14/27 (which would misrepresent a software
deposit as a reference publication). Neither serves a reader looking for how to cite this code.

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/space-physics/lowtran

Two older spellings of the same repository appear in the historical record, and at this extraction
both still redirected here: `scienceopen/lowtran` (the v1.0 Zenodo record's `isSupplementTo`
identifier, `https://github.com/scienceopen/lowtran/tree/v1.0`) and `scivision/lowtran` (the links
inside the project wiki). Neither is a current value; they are noted so a later refresh recognises
them as the same project rather than a different one.

### 4. Software Functionality (RECOMMENDED — treated as critical)
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Physics-Based
- Models and Simulations: Data Guided
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots

Values are written in the qualified `Parent: Child` form throughout, because several child names
(`Analysis`, `Processing`, `Calibration`, `ML/AI`, `Field-line Tracing` and others) recur under more
than one parent and are ambiguous unqualified.

**Models and Simulations / Empirical / Physics-Based.** LOWTRAN 7 is a band-model radiative-transfer
code: its own header block describes it as a low-resolution propagation model for calculating
atmospheric transmittance and background radiance from 0 to 50,000 cm-1, built on tabulated
molecular band parameters and six representative model atmospheres. Empirical (fitted band
parameters, climatological profiles) and Physics-Based (spherical-refractive path geometry, single
and multiple scattering) both hold; they describe different aspects of the same engine.

**Models and Simulations: Data Guided** is recorded in this refresh because the package exposes a
first-class mode in which the simulation is driven by measured atmospheric data rather than by a
climatological profile. `src/lowtran/scenarios.py` sets `"model": 0,  # 0: user meterological data`
in both `horizrad()` and `userhoriztrans()`, and `horizrad()` reads a CSV of observations
(`PTdata = read_csv(infn)`, then pressure, ambient temperature, relative humidity and timestamps).
The project wiki devotes an entire page, "Local meteorological measurements", to this
workflow, and the wiki's front page calls it "A
currently [ongoing project](https://github.com/scivision/lowtran/projects/1)". Considered against a
narrower reading of "Data Guided" (data-assimilating or observationally-constrained boundary
conditions in a forecast model): under that reading the value would not apply, but the searcher's
question — "can I drive this model with my own measurements?" — is answered yes by a documented,
tested code path, and that is the question the value serves.

**Data Processing and Analysis / Analysis / Processing.** The wrapper does more than call Fortran: it
converts wavelength to the wavenumber grid the model requires (`nm2lt7`), loops the model over angle
and time and merges results (`loopangle`, `loopuserdef`), assembles labelled `xarray.Dataset` output,
and reads and writes scenario files.

**Data Visualization / 2D Graphics / Line Plots.** `src/lowtran/plot.py` provides six plotting
entry points (`scatter`, `radiance`, `radtime`, `transmission`, `irradiance`, `horiz`) and
`+lowtran/plot_transmission.m` provides the MATLAB equivalent. Note for a future refresh: every plot
produced is a curve on 2D axes; there is no contour, heat-map or image rendering anywhere in the
tree. `Data Visualization: 2D Graphics` is retained as the general statement that the package emits
static two-dimensional figures — the value was already recorded before this refresh and re-litigating
it would not change what a reader finds.

Considered and rejected, with reasons a later refresh should not have to rediscover:
- **Coordinate Transforms** — `nm2lt7()` and `example/Wavelength2LowtranWavenumber.py` convert
  wavelength to wavenumber. That is a unit conversion, not a change of coordinate system or reference
  frame; no spatial or temporal frame is transformed anywhere in the package.
- **Data Processing and Analysis: Energy Spectra** — the spectra here are transmission and radiance
  against wavelength, not particle energy spectra.
- **Data Visualization: Spectrogram** and **Data Processing and Analysis: Spectrogram** — no
  time-frequency representation is computed or drawn.
- **Models and Simulations: First Principles** — LOWTRAN is explicitly a low-resolution band model
  built on fitted parameters, the opposite of a line-by-line first-principles calculation.
  `Physics-Based` already carries the physical-model claim.
- **Data Processing and Analysis: File Format Conversion** — reading CSV and writing HDF5/NetCDF is
  ordinary I/O around a simulation, not a conversion utility offered to users.
- **Data Processing and Analysis: Time Series Analysis** — `horizrad()` indexes results by time and
  `plot.radtime()` draws one figure per time step, but nothing analyses a time series.

### 5. Related Region (RECOMMENDED — treated as critical)
- Earth Atmosphere
- Earth Lower and Middle Atmosphere

The Region vocabulary is **flat**: no row implies any other, and every row's `definition` is empty, so
a value must be earned on its own evidence rather than inherited from a broader or narrower term.
`Earth Atmosphere` was already recorded before this refresh and is kept; a coarse region and a
specific one coexist rather than replace one another.

This refresh records `Earth Lower and Middle Atmosphere` because that is where essentially all of
this model's physics lives. The absorbers it parameterises (water vapour, carbon dioxide, ozone) and
the aerosol, cloud, rain and desert models it carries are troposphere-to-mesosphere phenomena; the
package's own keywords name `mesosphere` and `stratosphere`; and the default scenario in
`src/lowtran/tests/test_scenarios.py` is `"model": 5` — subarctic winter — a lower-atmosphere
climatology. A user browsing HSSI for lower- and middle-atmosphere software would expect an
atmospheric transmission model to be there.

**Considered and not determinative: `Earth Thermosphere`.** The value is deliberately not recorded,
and the evidence that pointed the other way is kept here so a later refresh sees that it was weighed
rather than missed. For: the model's standard profile grid does reach thermospheric altitudes; the
`DATA ALT/` block in `src/lowtran/fortran/lowtran7.f` lists fifty levels from 0.0 to 120.0 km, and
the vendored reference list in `archive/TAPE1` cites
"AFGL ATMOSPHERIC CONSTITUENT PROFILES (0 TO 120KM)". The package's own `pyproject.toml` keyword list
includes `thermosphere`. Against, and decisive: nothing in the code models a thermospheric process.
The profile simply continues upward through a region that contributes almost nothing to transmittance
in the modelled bands, so that grid is coverage, not thermospheric physics; and a searcher filtering
on `Earth Thermosphere` is looking for thermospheric models and would find a lower-atmosphere
transmission code out of place.

**Considered and rejected: `Earth Ionosphere`.** The HSSI keyword
`ionosphere_thermosphere_mesosphere` on this entry comes from the PyHC registry's domain
classification (`keywords: ['ionosphere_thermosphere_mesosphere', 'specific']` in the registry's
unevaluated-projects list), not from the software. That tag propagates across many PyHC entries and
is not evidence about any particular one. This package contains no plasma physics, no electron
density and no ionospheric quantity of any kind; the single occurrence of the word "ionosphere" in
the tracked tree is a comment in `test/lowtran_driver.f90` explaining how the author points a camera.

### 6. Authors (MANDATORY)

#### Author 1
- **Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493
- **Affiliation 2:**
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found

Michael Hirsch is the sole author of the wrapper: `LICENSE.txt` reads
`Copyright (c) 2015 Michael Hirsch`, the PyHC registry lists him as the contact, the Zenodo v1.0
record's creator is `Hirsch, Michael` with affiliation `Boston University`, and `test/lowtran_driver.f90`
carries `!! Michael Hirsch, Ph.D. https://www.scivision.dev`. The ORCID and both affiliations were
already stored before this refresh; the earlier extraction that recorded "Author Identifier: Not
found", and gave the affiliation block neither an organization nor an identifier, was simply older
evidence, and its emptiness must not be read as a proposal to remove anything.

The Zenodo v3.1.0 deposit credits the creator as `scivision` — the author's GitHub login, carried
across by the GitHub–Zenodo integration (DataCite renders the same creator as `Scivision`).
`Michael Hirsch` is the person's name and is the correct stored value; the login is not an
alternative author.

**No ROR exists for Scivision, Inc.** A ROR query for "Scivision" returns exactly one organization,
`https://ror.org/011qev639`, one of whose labels is "SciVision Biotech Inc." and whose location is
Kaohsiung, Taiwan — an unrelated biotechnology company. A future refresh must not attach that
identifier to this affiliation. The stored organization label's capitalisation differs from the
company's own styling of the name; that difference is parked as a wider catalogue matter and is
deliberately not changed here.

**Considered and rejected: adding the LOWTRAN 7 model authors.** `src/lowtran/fortran/lowtran7.f`
names F.X. Kneizys, E.P. Shettle, G.P. Anderson, L.W. Abreu, J.H. Chetwynd, J.E.A. Selby,
S.A. Clough and W.O. Gallery under an `AUTHORS` heading, and the model's users guide carries the
same eight names. They authored the vendored 1988/1992 model, not this software, and none of them
published, released or maintains this repository. Their credit is carried instead by Field 27, which
points at their users guide. Listing them as authors of an HSSI software entry they had no part in
would misattribute the packaging work and would not match how anyone cites either artifact.

**Considered and rejected: the one external contributor.** Exactly one pull request from another
account has ever been merged into this repository — #32, `jkrimmer`, "Update README.md for Python
3.12", merged 2024-03-05. A documentation correction is not authorship.

There is no `CITATION.cff`, `codemeta.json` or `.zenodo.json` at this revision, and the PyPI record's
author fields are empty, so the sources above are the whole of the available author evidence.

### 7. Software Name (MANDATORY)
- **Name:** LOWTRAN

This matches the PyHC registry's official name for the project (`name: LOWTRAN`) and the way the
model is universally referred to in the literature.

Alternatives, all rejected: `lowtran` (the PyPI distribution and repository name — lowercase because
of packaging convention, not because it is the project's name); `Lowtran in Python` (the README's H1,
a page title rather than a software name); `space-physics/lowtran` (an org-qualified repository
path).

### 8. Description (MANDATORY)
LOWTRAN7 atmospheric absorption extinction model. Updated to be platform independent and easily accessible from Python and Matlab. The main LOWTRAN program is accessible from Python by using direct memory transfers instead of the cumbersome and error-prone process of writing/reading text files. xarray.Dataset high-performance, simple N-D array data is passed out, with appropriate metadata. LOWTRAN models Earth atmosphere absorption and transmission vs. wavelength and location, including atmospheric scattering and radiance calculations.

The first four sentences are the README's opening paragraphs with Markdown formatting removed —
compare README lines 7–12, which read "LOWTRAN7 atmospheric absorption extinction model." and
"`xarray.Dataset` high-performance, simple N-D array data is passed out, with appropriate metadata."
The closing sentence is a summary added by the submitter, not drawn from any source file. It is
accurate (`src/lowtran/scenarios.py` exposes transmittance, radiance, irradiance and single-scatter
paths) and is kept as the submitter's editorial choice.

### 9. Concise Description (OPTIONAL)
Model of Earth atmosphere absorption and transmission vs. wavelength and location.

This is `pyproject.toml`'s `description` value. Note for anyone comparing the two byte for byte: the
`pyproject.toml` string begins with a leading space, which the stored value does not carry. The
stored form is the correct one; the leading space is an upstream typo and the value here is
deliberately not a verbatim copy of that line.

### 10. Publication Date (RECOMMENDED)
- **Date:** 2015-03-31

The date this software was first published: the repository's initial commit `225a20e` is dated
2015-03-31 and GitHub's `created_at` for the repository is `2015-03-31T19:19:59Z`.

Considered and rejected: 1988 or 1992, the dates of the underlying AFGL model. Field 10 is the
publication date of *this* software, and dating the entry to the vendored engine would put the
package two decades before the language it is written in.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

DataCite records `publisher: "Zenodo"` for this DOI. The deposits were made through the
GitHub–Zenodo integration rather than uploaded by hand — the v3.1.0 record carries the integration's
signature, a related identifier `https://github.com/space-physics/lowtran/tree/v3.1.0` with relation
`isSupplementTo` — and Zenodo remains the publisher of record either way.

### 12. Version (RECOMMENDED)

#### Version Number
- **Value:** v3.1.0

#### Version Date
- **Value:** 2023-02-19

#### Version Description
Use pyproject.toml alone. f2py builds on first use of import lowtran function e.g. lowtran.check() or pytest or similar. Patched to work again on Windows with Python >= 3.8.

#### Version PID
- **Value:** https://doi.org/10.5281/zenodo.7654888

v3.1.0 is the newest version in existence: it is the newest GitHub release, the newest Zenodo deposit,
the current PyPI release, and `pyproject.toml` at this revision reads `version = "3.1.0"`. It is
therefore the recorded version.

The stored description is the GitHub release body with its Markdown code formatting removed; the
release body itself reads "Use pyproject.toml alone. f2py builds on first use of `import lowtran`
function e.g. `lowtran.check()` or `pytest` or similar. Patched to work again on Windows with Python
>= 3.8." Note that this author also summarises each release in the release *name* — v3.1.0's name is
"New f2py build using CMake" — so a future refresh reading only the body sees half the release note.

Every clause of that description is attributable to work inside the release's own range. Tag `v2.5.1`
is the previous ancestor tag, and each clause maps to a commit between the two: "use pyproject.toml
alone" (`e33d8e2`, 2023-02-10), the lazy f2py build behind `lowtran.check()` (`cd901e8`, "add
lowtran.check() to quick check / build Lowtran if needed"), and the Windows fix (`66de7eb`, "on
Windows, use WSL", which introduced the `os.add_dll_directory` search-path handling into
`src/lowtran/__init__.py`). `cd901e8` then moved that block out of `__init__.py` and into
`import_f2py_mod()` in `src/lowtran/base.py` later the same day, 2023-02-19, so the release carries
the handling in `base.py`; the call is absent from the tree at `v2.5.1`. Nothing in the description
is inherited from an earlier release or unattributable.

A trap for any later version work in this repository: tags `v1.0` and `v2.2` are **not** ancestors of
the current tip — they sit on lineages abandoned in an early history rewrite. `v2.3.0` and everything
after it are ancestors. Walking tags with `git log --all` will mix the two lineages and attribute
commits to the wrong releases; check ancestry explicitly before attributing anything.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- Fortran77
- MATLAB

**The criterion, stated explicitly, because the answer depends on it.** The form defines the field as "The
computer programming languages most important for the software." and adds "This is not meant to be an
exhaustive list." The values above are therefore chosen as *the languages a user of this software
writes or has compiled on their behalf*:

- **Python 3.x** — the package's own API (`src/lowtran/`), `requires-python = ">=3.9"`, CI across
  3.9–3.12.
- **Fortran77** — the vendored engine, `src/lowtran/fortran/lowtran7.f`, which the pip install path
  compiles on first use. The label describes the code's fixed-form FORTRAN-77-era character, which is
  also why the build must relax the compiler: `src/lowtran/cmake/compilers.cmake` sets
  `add_compile_options("$<$<COMPILE_LANGUAGE:Fortran>:-std=legacy;-w>")` for GNU compilers.
- **MATLAB** — a supported front end, not a demo. The repository ships the `+lowtran` package
  (`transmission.m`, `plot_transmission.m`, `TestLowtran.m`, `private/xarray2mat.m`), the driver
  `RunLowtran.m`, a `buildfile.m` build plan, and a root CMake `matlab` option whose test runs
  `runtests('lowtran')`.

Everything excluded follows from the same criterion. The first-party Fortran in `test/` —
`lowtran_driver.f90` (246 lines) and `assert.f90` (157 lines) — is a CTest harness built only by the
root CMake path; it is not installed by pip (`MANIFEST.in` grafts only `src/lowtran/cmake` and
`src/lowtran/fortran`) and a user of the library never invokes it. So `Fortran90`, `Fortran 2003` and
`Fortran 2008` are not recorded, even though constructs of those editions appear in those two files.
CMake is a build system, and has no row in the vocabulary in any case.

**The alternative criterion, and why it is not used.** One could instead name the *minimum language
standard a conforming compiler must accept*. Measured with gfortran 14.1.0 in `-fsyntax-only` mode,
that criterion gives a different and less useful answer: `lowtran7.f` is rejected under `-std=f95`
and also under `-std=f2018` (which deleted the DO-termination form it uses), and is accepted under
`-std=f2008` and `-std=legacy`; `test/lowtran_driver.f90` is first accepted at `-std=f2008`; and
`test/assert.f90` is first accepted at `-std=f2018`. Under that criterion `Fortran77` would be
justified by nothing at all, the answer for the engine would be `Fortran 2008`, and the harness's
requirement could not be expressed because the vocabulary has no `Fortran 2018` row. It would also
mislead: a reader who sees `Fortran 2008` expects modern Fortran, whereas what this project actually
hands a packager is nineteen thousand lines of fixed-form 1992 code that needs `-std=legacy`.

Note the vocabulary's inconsistent spelling when writing any of these: `Fortran77` and `Fortran90`
have no space; `Fortran 2003`, `Fortran 2008` and `Fortran 2023` do.

### 14. Reference Publication (OPTIONAL)
Not found — there is no publication describing this software.

This is a negative result with evidence behind it, not an unexamined blank. An ADS query for
`author:"Hirsch, Michael" title:lowtran` returns exactly one record, and it is the Zenodo software
deposit itself (`2016zndo....213475H`, DOI `10.5281/zenodo.213475`) — no journal article, no JOSS
paper, no conference proceeding. A Zenodo full-text query for `lowtran` returns the v3.1.0 software
deposit and one unrelated 2002 paper about atmospheric Cherenkov photons. A creator-keyed Zenodo
query on `scivision` (the identity under which the deposits were made, which a repository-name search
would miss) returns no further LOWTRAN artifact of any kind.

The LOWTRAN 7 users guide describes the vendored *model*, not this software, and is recorded on
Field 27 where it belongs.

### 15. License (RECOMMENDED)
- **License:** MIT License

HSSI held no license value for this entry before this refresh. `LICENSE.txt` at this revision is the
MIT licence text, opening `The MIT License (MIT)` and `Copyright (c) 2015 Michael Hirsch`, and
`MIT License` is the exact vocabulary row name.

**The licence has never changed.** Established by content rather than by path history, which matters
here because a plain "when was this file added" query reports the 2019 rename as a creation. Only two
revisions in the tip's ancestry touch a licence path at all — the 2015 initial commit `225a20e` (as
`LICENSE`) and the 2019 rename `cb4c084` "metadata and Matlab CI" (as `LICENSE.txt`) — and those two
files and the file at the current tip hash identically (SHA-256
`99ad1e29dc165b446c5b7e2dcb95c18520dbd95816ffe9007e1ef1fdaaf3d8f3`). The released `v3.1.0` tag
carries a file with that same hash, so the version HSSI publishes is MIT too.

**Zenodo's `other-open` is wrong and must not be copied.** Both Zenodo records — v1.0 and v3.1.0 —
record `license: {'id': 'other-open'}`, a deposit-form default that the GitHub–Zenodo integration
never revisited. A DOI-driven autofill would carry that value straight into the catalogue, so the
repository, not the deposit, is the source of truth for this field.

**No License URI is recorded, and none can be.** An earlier extraction proposed
`https://spdx.org/licenses/MIT.html` as a Field 15 sub-value. That string is wrong twice: the
`MIT License` vocabulary row's own URL is `https://spdx.org/licenses/MIT`, without the `.html`; and
more fundamentally there is no per-software licence URI in HSSI at all — the software's licence is a
reference to a shared licence row, and the URL lives on that shared row. Recording a URI here would
create the impression of a storable value that does not exist.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- atmosphere
- atmospheric-modelling
- f2py
- fortran
- geoscience
- ionosphere_thermosphere_mesosphere
- lowtran
- matlab
- matlab-python-interface
- mesosphere
- python
- stratosphere
- thermosphere

Stored lowercase, and the set is the union of three authoritative sources: the repository's GitHub
topics (`atmosphere`, `atmospheric-modelling`, `f2py`, `fortran`, `geoscience`, `lowtran`, `matlab`,
`matlab-python-interface`, `python`), the `keywords` list in `pyproject.toml` (`mesosphere`,
`stratosphere`, `thermosphere`, `atmosphere`), and the PyHC registry's domain tag
`ionosphere_thermosphere_mesosphere`.

The PyHC registry's second tag, `specific`, is deliberately excluded: it is that registry's own
classification of a project as domain-specific rather than general-purpose, not a subject keyword.
The domain tag that *is* kept describes PyHC's categorisation of the project and should not be read
as evidence for any Region value — see Field 5.

### 17. Data Sources (OPTIONAL)
Not found — correctly empty.

The Data Sources vocabulary offers seventeen values: AMDA, CDAWeb, das2, FTP/FTPS Directories, GFZ,
HAPI, HTTP/HTTPS Directories, Madrigal, Observatory/Mission-specific, OMNIWeb, Other, S3/Cloud-aware,
SSCWeb, TAP, The Virtual Solar Observatory., VirES and WDC. Setting aside the catch-all, every one
names a remote archive, service or access protocol. This package retrieves nothing from anywhere:
its inputs are function arguments and, in the user-atmosphere scenarios, a local CSV file of the
user's own measurements, and there is no network code in the tree.

`Other` was considered and rejected: selecting it would return this entry to a searcher filtering for
software with external data access, which it does not have. An evidenced empty value is the correct
answer for a self-contained model.

### 18. Input File Formats (RECOMMENDED)
- csv
- HDF5

`src/lowtran/scenarios.py` supplies both: `horizrad()` reads a user's meteorological table with
`PTdata = read_csv(infn)` (time, relative humidity, ambient temperature, total pressure — see the
CLI help text in `example/UserDataHorizontalRadiance.py`), and the same function short-circuits to
reload a previously saved result when `infn.suffix == ".h5"`, via `xarray.open_dataset(infn)`.

**Considered and rejected: `ascii`.** Two ASCII paths exist and neither is a user input format. The
original Fortran can read the classic TAPE5 card deck, but the wrapper deliberately bypasses it —
the README's premise is "direct memory transfers instead of the cumbersome and error-prone process of
writing/reading text files", and `test/lowtran_driver.f90` hard-codes
`logical, parameter :: Python= .true.` above the comment
`!     Python .false.: Read the Tape5 file (like it's the 1960s again)`. Separately, that driver
opens `test/testfort_trans.asc` and `test/testfort_solarrad.asc`, but those are CTest reference
values compared against computed output, not data a user supplies.

### 19. Output File Formats (RECOMMENDED)
- HDF5
- netCDF3/4

The README states "In these examples, optionally write to HDF5 with the `-o` option", and the
examples implement that option as `TR.to_netcdf(outfn)` on the `xarray.Dataset`. The two names in the
examples' own help text reflect the same call: `example/UserDataHorizontalRadiance.py` describes `-o`
as "HDF5 file to write" while `example/ScatterRadiance.py` describes it as "NetCDF4 file to write".
Both stored values are therefore correct and neither is redundant — netCDF4 is itself an HDF5-based
container, and a searcher filtering on either format should find this software.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

`.github/workflows/ci.yml` builds and tests on `ubuntu-24.04` and `macos-latest` in the `core` job and
on `windows-latest` in a dedicated `windows` job that installs `mingw-w64-x86_64-gcc-fortran` through
MSYS2. All three run the full sequence — build, import, `pytest`, and the CMake/CTest workflow.

Considered and rejected: `Operating System Independent`, which `pyproject.toml`'s classifier list
asserts. That classifier is a packaging convention about the Python code; the software as delivered
requires a Fortran compiler and CMake, and the three tested platforms are the concrete, defensible
answer. Note that the README's Windows advice ("Windows Subsystem for Linux") understates what CI
actually proves, which is a native MinGW build.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- CPU Independent

`CPU Independent` reflects what this package actually is: pure Python plus Fortran compiled from
source on the user's own machine, with no architecture-specific code, no binary wheels and no
intrinsics. `x86-64` records the architecture the project is known to be exercised on.

**Considered and not selected: `Apple Silicon arm64`.** The macOS CI job targets `macos-latest`,
which GitHub mapped to an arm64 runner image at this extraction — but the workflow pins no image,
so what that label resolved to on any past run is not evidence this repository can produce.
`CPU Independent` already covers architecture-agnostic source builds, which is the honest claim.
Recorded so a later refresh does not rediscover the runner-image argument and mistake it for proof.

### 22. Related Phenomena (OPTIONAL)
Not found — correctly empty.

The Phenomena vocabulary offers seven values in total: Coronal Heating, Coronal Mass Ejections,
Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission. All seven are solar or
geospace disturbance phenomena. This software models molecular and aerosol absorption, scattering,
transmittance and radiance in Earth's neutral atmosphere and supports none of them. The vocabulary is
closed — a phenomenon with no row would belong in Keywords, not here — so an empty value is the
correct outcome rather than a gap.

### 23. Development Status (RECOMMENDED)
- **Inactive**

HSSI held no development-status value for this entry before this refresh. The vocabulary's definition
of the recorded value is: "The project has reached a stable, usable state but is no longer being
actively developed; support/maintenance will be provided as time allows."

Both halves are satisfied. *Stable and usable*: v3.1.0 is released on PyPI and Zenodo, CI covers three
operating systems and four Python versions, and the package installs and runs. *No longer actively
developed*: the most recent commit on the default branch is `5b8d387` "simplify/modernize", dated
2024-12-18; the most recent release is 2023-02-19; and five issues and three pull requests stand
open. (GitHub's single `open_issues_count` of 8 sums the two and should not be read as eight
issues.)

The two neighbouring values were checked against their own definitions and rejected:
- **Active** ("being actively developed") is contradicted by the commit record. An earlier extraction
  proposed `Active` on the strength of a recent `date_updated` reported by an automated tool; that
  figure is GitHub's `updated_at`, which advances on stars, watches and metadata edits and is not a
  measure of development. The commit and release dates are.
- **Unsupported** ("the author(s) have ceased all work on it. A new maintainer may be desired")
  requires evidence of cessation that does not exist: the repository is not archived, carries no
  deprecation notice, and the author continues to publish releases of other projects.

Considered and rejected as a mapping source: `pyproject.toml`'s classifier
`"Development Status :: 4 - Beta"`. That is PyPI's maturity scale, a different axis from
repostatus.org's activity scale; reading "Beta" across would suggest `WIP`, which is wrong for a
project with a stable public release.

### 24. Documentation (RECOMMENDED)
- **URL:** https://github.com/space-physics/lowtran/wiki

The project wiki is a genuine, separate documentation resource: three pages ("Home",
"Local meteorological measurements", "Solar irradiance at LWIR") explaining what LOWTRAN 7 is and
documenting, card by card, how the model's input parameters are set for the horizontal-path and
solar-irradiance scenarios. The README does not link it, so this field is what makes the wiki
discoverable from this entry at all.

**A known mismatch, accepted as the cost of this value.** The field asks for "the documentation and
installation instructions"; the wiki contains no installation instructions — those are in README.md,
under "Install". The alternative value would be the repository URL itself, which the field explicitly
permits ("If this is the same as the access URL, then enter that link here"), at the cost of
duplicating Field 3 and dropping the entry's only link to the wiki. The wiki is kept, because
Field 3 already puts the README one click away for any reader, whereas nothing else in the entry
surfaces the wiki.

Note for anyone re-deriving this: a repository wiki is a *separate* git repository
(`<repo>.wiki.git`) and is invisible from the code revision pinned in this file's header; its
contents cannot be checked out from the source tree. The wiki's own internal links use the
project's former `scivision/lowtran` name and, at this extraction, still reached the current
repository by redirect.

### 25. Funder (OPTIONAL)
Not found.

No funding statement exists in any available source: there is no acknowledgements section anywhere in
the repository, no funding file, no reference publication whose acknowledgements could be read (see
Field 14), and neither Zenodo record carries a grant.

Considered and rejected: the U.S. Air Force Geophysics Laboratory, which produced the vendored
LOWTRAN 7 model in 1988 and whose contact address survives in the vendored source
(`L.W ABREU  ,AFGL/OPE,HANSCOM AFB,MASS 01731`). AFGL funded and produced the *original model*, three
decades before this repository existed; it did not fund this software, and recording it would
misattribute the wrapper's sponsorship.

### 26. Award Title (OPTIONAL)
Not found — same evidence as Field 25. There is no award, grant number or contract identifier
anywhere in the repository, the Zenodo records or the package metadata.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://ui.adsabs.harvard.edu/abs/1988ugls.rept.....K/abstract

**Kneizys, F. X.; Shettle, E. P.; Abreu, L. W.; Chetwynd, J. H.; Anderson, G. P.; Gallery, W. O.;
Selby, J. E. A.; Clough, S. A. (1988).** *Users Guide to LOWTRAN 7.* Interim scientific report, Air
Force Geophysics Laboratory. ADS bibcode `1988ugls.rept.....K`. The report is AFGL-TR-88-0177, also
issued as Environmental Research Papers, No. 1010, dated 16 August 1988, Air Force Geophysics
Laboratory, Hanscom AFB, Massachusetts; its cover carries the same eight authors.

HSSI held no related-publication value for this entry before this refresh. This document is the one
publication the software's own author prioritises: the README's "Notes" section opens by naming
LOWTRAN7 and linking
"[User manual](http://www.dtic.mil/dtic/tr/fulltext/u2/a206773.pdf)", then instructs the reader to
"Refer to this to understand what parameters are set to default." `src/lowtran/__init__.py` repeats
the same pointer in its module docstring. The wrapper's parameter names (`itype`, `iemsct`, `im`,
`ird1`, `wmol`) are the manual's card fields, and both `src/lowtran/scenarios.py` and the wiki cite
its page numbers directly. A user of this software cannot configure it without that document.

**Why the ADS abstract page rather than the DTIC link the README carries.** The field accepts a
permanent link for a publication with no DOI, and names an ADS abstract page as the preferred form.
The ADS record is preferred on permanence, and it resolves the work unambiguously — it carries
the same eight author names as the `AUTHORS` block in `src/lowtran/fortran/lowtran7.f` and as the
users-manual entry in the vendored reference list in `archive/TAPE1`,
"(1988) LOWTRAN 7 COMPUTER CODE : USER'S MANUAL AFGL-TR-88-XXXX" — and it does not depend on DTIC's
availability. That vendored list leaves the report number as a literal placeholder; the report
number recorded above resolves it, and confirms that the README's DTIC link, the ADS record and the
vendored entry all name one document. The DTIC URLs are an access problem rather than a missing
document: as observed at this extraction, `www.dtic.mil` presented a certificate chain that does not
validate against a standard trust store, and `apps.dtic.mil` returned a scheduled-maintenance page.
The report remains retrievable from an Internet Archive capture of the DTIC PDF even when DTIC's own
hosts are not reachable. It has no DOI; ADS records none.

Considered and rejected: the many papers that *use* LOWTRAN 7 (an ADS title search for "LOWTRAN 7"
returns validation and comparison studies from 1989–1992, among others). They cite the 1988 Fortran
model, not this Python packaging of it, and listing them would tell a reader nothing about this
software.

### 28. Related Datasets (OPTIONAL)
Not found.

No published dataset is associated with this software. The data-bearing files in the tree are the
test references `test/testfort_trans.asc` and `test/testfort_solarrad.asc` — 53 lines each: a row
count, a header, then 51 wavelength/value pairs the CTest driver compares computed output against —
and the vendored inputs in `archive/`, which are the 1994 distribution's card decks and filter
tables. None of them is published or citable. Creator-keyed Zenodo searches under both identities
the author deposits with (`Hirsch, Michael` and `scivision`), read to the last page of results,
return no dataset associated with this software.

### 29. Related Software (OPTIONAL)
- https://docs.xarray.dev/
- https://www.mathworks.com/products/matlab.html
- https://web.archive.org/web/20220804013629/https://www1.ncdc.noaa.gov/pub/data/software/lowtran/

**xarray** is retained on cited evidence, not on dependency presence. README line 12 states
"`xarray.Dataset` high-performance, simple N-D array data is passed out, with appropriate metadata" —
the labelled dataset is this software's documented output contract, constructed in
`src/lowtran/base.py` with named variables (`transmission`, `radiance`, `irradiance`, `pathscatter`)
and coordinates (`time`, `wavelength_nm`, `angle_deg`), consumed by the plotting module, accepted
back by `horizrad()` as an input, and converted for MATLAB callers by `+lowtran/private/xarray2mat.m`.
That is a specific documented exchange, which is what the Tier B rule requires.

**MATLAB** is retained on the cross-language bridge described under Field 13: the shipped `+lowtran`
package, `RunLowtran.m`, `buildfile.m`, and a CMake test that runs `runtests('lowtran')`. The README
devotes a section to it: "Matlab users can seamlessly access Python modules, as demonstrated in
[RunLowtran.m](./RunLowtran.m)."

**The origin of the vendored Fortran** is the third entry. The README's "Reference" section cites
"* Original 1994 Lowtran7 [Code](http://www1.ncdc.noaa.gov/pub/data/software/lowtran/)", and that
relationship is real and specific: the repository's `archive/` directory holds twelve files from
that distribution — `lowtran7.2`, `.3`, `.7.f`, `.8`, `.9`, `.10.f`, `.11`, `.12`, `.13.f`, `.14`,
`.15`, `.16` — which correspond to entries in that NOAA directory listing one for one by number
rather than by identical filename. The three carrying `.f` are the Fortran sources, two of them the
`LOWFIL` and `LOWSCAN` programs that the same section names. But **the original URL is dead**: at this
extraction it redirected into NOAA's NCEI domain, where the entire `/pub/data/software/` subtree had
been removed in the NCDC-to-NCEI migration while the parent `/pub/` and `/pub/data/` paths still
served. The value recorded above is the Internet Archive's 2022-08-04 capture of that directory,
which still lists all sixteen original files with their 1994-04-14 timestamps.

The Wayback capture is the recorded value because it preserves the provenance while sending a reader
to the real 1994 distribution listing rather than to an error page. The evidence above that the
original URL is dead, and why it died, is kept for a specific reason: it is what stops a later
refresh restoring that URL as the citation of record. Two alternatives were considered and were not
determinative. *Keeping the original NOAA URL* has the historical claim — it is the URL the README
actually prints, and the address the model's own distribution was cited by — but HSSI renders a
related-software entry as a clickable link labelled by its raw URL, so a reader would be sent to a
dead page with nothing to explain why. *Dropping the entry* would lose the provenance link entirely;
the `archive/` directory in the repository still preserves the files themselves, so nothing would be
technically lost, but the connection between this package and the 1994 code would stop being visible
in the catalogue.

**Tier A removals, applied as policy rather than taste.** `https://numpy.org/` and
`https://dateutil.readthedocs.io/` were stored on this entry before this refresh, which drops both. The
field guidance names both packages explicitly in its exclusion list, "Never list these (Tier A), no
exceptions", and extends that exclusion to this field, where the generic scientific-Python stack is
excluded too: "numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests,
python-dateutil, pytest, tqdm, PyYAML, click, setuptools and their peers are not related software,
because listing them says nothing that isn't equally true of most of the ecosystem." Both are genuine
dependencies of this package (`dependencies = ["numpy", "xarray", "python-dateutil"]`); neither
distinguishes it. This is a rule about the field, not a judgement about the packages, and a later
refresh should not restore them from the dependency list.

**Considered and not determinative: MODTRAN.** The relationship is real, and it is kept on the record
here so a later refresh sees that it was weighed rather than missed. The project's own wiki opens
with "LOWTRAN7 is a 1992 program that underlies the proprietary MODTRAN program." — the clearest
"performs similar tasks" relation the project itself documents, and exactly the kind of
distinguishing entry the field describes. It is nevertheless not recorded, because no HSSI entry for
MODTRAN was found to point at and the only remaining target is its vendor page
(`http://modtran.spectral.com/`), which, as observed at this extraction, served only over plain
HTTP — its HTTPS endpoint did not complete a connection. Sending a reader from the catalogue to a
bare plain-HTTP commercial vendor page is a poor destination, and that cost outweighs recording a
relation the wiki already states in one sentence.

Also considered and rejected: `matplotlib` and `pandas` (generic infrastructure, Tier A by the same
rule as numpy — `pandas.read_csv` and `matplotlib.pyplot` are used but characterise nothing);
`seaborn` (an optional cosmetic import inside `example/ScatterRadiance.py`, wrapped in
`try`/`except ImportError`); `f2py` and CMake (build tooling, not related software); the other
`space-physics` packages in the catalogue (no code path, import, document or example connects this
repository to any of them — the shared GitHub organisation is not a relation).

### 30. Interoperable Software (OPTIONAL)
- https://www.mathworks.com/products/matlab.html
- https://docs.xarray.dev/

**MATLAB** was already recorded here before this refresh and is correct: `+lowtran/transmission.m`
calls `T = py.lowtran.transmittance(py.dict(p));`, `+lowtran/private/xarray2mat.m` converts the
returned dataset into MATLAB arrays, `+lowtran/TestLowtran.m` asserts a numerical result through that
path, and the root `CMakeLists.txt` `matlab` option registers a test that executes
`runtests('lowtran')`. That is a demonstrated, tested cross-language exchange, not a claim about
sharing a runtime.

**xarray** is recorded in this refresh on the same evidence cited in Field 29 — the README documents
`xarray.Dataset` as the interchange format the public API passes out, which is precisely the exchange
the Tier B rule asks for, as distinct from internal use. Listing a package in both fields is
deliberate and already this entry's pattern for MATLAB: Field 29 records it as a characterising
dependency, Field 30 records the demonstrated exchange.

No other package qualifies. Neither of the blanket justifications the guidance rejects — ecosystem
membership, or PyHC membership implying interoperation — applies here, and nothing in the repository
exchanges data with another domain tool.

**Catalogue relations, checked in both directions.** No other HSSI entry names this repository (under
its current name or its former `scivision/lowtran` and `scienceopen/lowtran` spellings) in its related
or interoperable software, and a concept sweep of the catalogue for radiative-transfer, atmospheric
transmission and absorption software surfaced no peer entry to relate this one to. Recorded as
negative research so a later refresh need not repeat the sweep from scratch; it should of course be
redone if the catalogue grows a peer.

### 31. Related Instruments (OPTIONAL)
Not found — correctly empty, and earned rather than assumed.

This software is instrument-agnostic by construction: it computes atmospheric transmittance and
radiance for a path geometry, and the package exposes no instrument response, no calibration, no
instrument-specific format and no instrument-specific parser. (The vendored 1994 distribution in
`archive/` does contain the original `LOWFIL` filter and `LOWSCAN` spectral-scanning programs, but
the README records that neither was wired up, and no filter or scanning function exists in the
Python or MATLAB code.)

The tracked tree at this revision was swept with a word-boundary pattern over every file, vendored
sources and `archive/` included (`git grep -P`, case-insensitive, `\b(GOES|SDO|AIA|MODIS|VIIRS|
AVHRR|Landsat|Sentinel|THEMIS|DMSP|ISS|Hubble|Terra|Aqua|SUVI|MSIS|IRI|HITRAN|MODTRAN|FASCODE|AFGL|
AFRL|satellite|spacecraft|telescope|radiometer|sounder|spectrometer|camera|imager|all.?sky|
photometer|lidar|radar|sonde)\b`, written on one line in use), and the three wiki pages were swept
with the same terms. Note that `git grep -E` must not be used for this: it treats `\b` as a literal
`b` and returns a silent, confident zero. The pattern above does return hits on this tree, which is
the control proving that where it finds nothing, nothing is there.

What the sweep found, read hit by hit: in the vendored code and `archive/`, AFGL technical-report
citations, the AFGL mailing address, FASCODE cross-references, and false positives worth knowing
about before re-running it — the apparent `GOES` matches are the English word "goes" in phrases like
"THE PATH GOES THROUGH", and the apparent `ISS` match is a Fortran variable in
`COMMON /CNTRL/ KMAX,M,IKMAX,NL,ML,IKLO,ISS,IMULT`. Not one hit is a supported instrument. The wiki
returns exactly two hits, and neither is an instrument either: `Local-meteorological-measurements.md`
has "set V1, V2, DV for our camera frequency range and desired resolution", a generic sentence about
choosing a spectral range, and `Home.md` has "LOWTRAN7 is a 1992 program that underlies the
proprietary MODTRAN program." — which names a program, not an instrument, so it is out of scope for
this field; Field 29 records why it is not listed as related software either. That MODTRAN hit
exists only in the wiki: the pattern finds no `MODTRAN` anywhere in the tracked source tree at this
revision.

**Considered and rejected: Poker Flat.** The one instrument-adjacent mention in first-party code is a
comment in `test/lowtran_driver.f90`: "for our cameras typically magnetic inclination of E-layer
ionosphere, e.g. angle is about 12.5 at Poker Flat Research Range". That explains how the author
happens to choose a default zenith angle for his own auroral cameras; it does not make the software
designed to support any instrument there. The relevance gate excludes exactly this — a
"commonly used with" mention in an otherwise agnostic tool — and a user searching HSSI for a Poker
Flat instrument would not expect a radiative-transfer model back.

### 32. Related Observatories (OPTIONAL)
Not found — correctly empty, for the same reason and from the same sweep as Field 31.

The controlled vocabulary was searched across three columns — row `name`, row `abbreviation`, and the
SPASE `identifier` path — for every concept the repository raises. LOWTRAN, MODTRAN and AFGL return
no rows at all. Poker Flat does return rows, including the observatory
`Poker Flat Geophysical Observatory` (`https://spase-metadata.org/SMWG/Observatory/Ground/Poker.Flat`),
so this is a deliberate rejection of an existing, resolvable row on relevance grounds — see Field 31 —
not a failure to resolve one. Nothing is recorded here, and nothing should be: a bare name with no
SPASE identifier would create a new identifier-less vocabulary row, which is never an acceptable
outcome.

### 33. Logo (OPTIONAL)
- **URL:** https://raw.githubusercontent.com/space-physics/lowtran/5b8d38714b204eaa12595f5f15e2babec1dbdfb5/gfx/whyskyisblue.png

Verified by fetch: the URL returns PNG image bytes (124025 bytes), and the fetched bytes hash
identically (SHA-256 `01ab768345a680081f4e04f8169d6163c3fe56899e145c306dbe9f3a8d40fa63`) to
`gfx/whyskyisblue.png` at the pinned revision, so the pin is exact and the URL is not a Git-LFS
pointer. The URL is 117 characters, well within the stored column's limit.

The URL is pinned to a 40-character commit SHA rather than a branch. That matters concretely here:
the PyHC registry's own `logo:` entry for this project is the branch form
`https://raw.githubusercontent.com/space-physics/lowtran/master/gfx/whyskyisblue.png`, which names a
branch this repository has since renamed to `main`. As observed at this extraction that form still
resolved, but only through GitHub's compatibility redirect. The pinned form does not depend on that
redirect.

**The logo is kept, and the evidence on both sides is recorded here.** What prevailed: **the project
itself presents this exact image as its logo** — it is the value of the `logo:` field in the PyHC
registry entry for LOWTRAN. That is the guidance's own reason to keep such an image rather than
reject or swap it. Considered and not determinative: looked at, the image is not a wordmark or a
brand mark — it is a two-panel matplotlib figure, transmittance and single-scatter path radiance
against wavelength for three zenith angles, which is the output of `example/ScatterRadiance.py`,
shown in the README's gallery under "sun-to-observer scattered radiance (why the sky is blue)".
Nothing in the repository is a designed logo; `gfx/lowtran.png` is likewise a sample plot. Clearing
Field 33 for a documented omission was therefore weighed and not selected, and substituting a
different image is not the right response either: there is no better candidate in the tree, and this
is the image the project itself has chosen.
