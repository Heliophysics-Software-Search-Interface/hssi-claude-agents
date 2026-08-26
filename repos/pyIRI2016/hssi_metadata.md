# HSSI Metadata Extraction Results

**HSSI Software ID:** a53ebbd1-0f08-4bf6-aeaa-90067a3b1312
**Repository:** https://github.com/rilma/pyIRI2016
**Source Revision:** 1a47c6018aae8be93349fb2487c1911e95c1f99f
**Extraction Date:** 2026-07-26
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.240895
- **Source:** README.md Zenodo DOI badge (line 1); Zenodo API record 240895; DataCite `10.5281/zenodo.240895`.
- **Note:** This is the version-specific DOI for the archived v1.1.0 release. Zenodo record 240895 has `conceptrecid: "591270"` but an empty `conceptdoi`; this legacy 2017 record predates Zenodo concept DOIs, so **no concept DOI exists**. `https://doi.org/10.5281/zenodo.591270` is therefore not usable. There is no DOI for v1.2.0 because that GitHub release was not archived to Zenodo.

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/rilma/pyIRI2016
- **Source:** git remote `origin`; GitHub API `full_name: rilma/pyIRI2016`; SoMEF `code_repository` (confidence 1); Zenodo related identifier `https://github.com/rilma/pyIRI2016/tree/v1.1.0`.

### 4. Software Functionality (MANDATORY)

**Values:**

- **Coordinate Transforms**
- **Coordinate Transforms:Ionospheric**
- **Data Processing and Analysis**
- **Data Processing and Analysis:Analysis**
- **Data Processing and Analysis:Data Access and Retrieval**
- **Data Processing and Analysis:Processing**
- **Data Visualization**
- **Data Visualization:2D Graphics**
- **Data Visualization:Line Plots**
- **Models and Simulations**
- **Models and Simulations:Empirical**
- **Models and Simulations:Field-line Tracing**
- **Models and Simulations:Physics-Based**

**Parent-category check:** every subcategory has its parent present — `Coordinate Transforms` ✓, `Data Processing and Analysis` ✓, `Data Visualization` ✓, `Models and Simulations` ✓. No orphaned subcategories.

**Per-value justification:**

| Value | Evidence |
|---|---|
| Models and Simulations | pyIRI2016 wraps and runs the IRI-2016 model; the entire package exists to evaluate a model. `pyiri2016/__init__.py` `IRI2016.IRI()`, `IRI2016Profile`. |
| Models and Simulations:Empirical | IRI is the canonical empirical/climatological ionosphere model: CCIR and URSI foF2/M(3000)F2 coefficient maps (`data/ccir/ccir11-22.asc`, `data/ursi/ursi11-22.asc`), statistical Te/Ti profiles, `data/mcsat/*.dat`. `pyproject.toml` topic `Scientific/Engineering :: Atmospheric Science`. |
| Models and Simulations:Physics-Based | `source/iriflip.for` is the FLIP/IDC photochemical ion-density model (`CHEMION` plus `CN2D, CNO, CN4S, CN2PLS, CNOP, CO2P, COP4S, COP2D, COP2P, CNPLS, CN2A, CN2P, CNOPV` production/loss and `RATS` reaction rates) — first-principles ion photochemistry, not a statistical fit. It is **enabled by default** by this wrapper: `pyiri2016/__init__.py` line 45 sets `jf[6-1] = 0`, selecting the "Ni - RBV-10 & TTS-03" option, i.e. the iriflip photochemical ion densities. `source/cira.for` (NRLMSIS-00 neutral atmosphere) and `source/iridreg.for` (Friedrich & Torkar 2001 FIRI D-region) are further physics-based components exposed via `firisubl`. |
| Models and Simulations:Field-line Tracing | `pyiri2016/iri2016prof2D.py` `IRI2016_2DProf.LatVsFL()` (line 140) traces geomagnetic field lines over a range of apex heights via `pyapex.ApexFL().getFL(date=…, dlon=…, dlat=…, hateq=h, mlatRange=…, mlatSTP=…)` (line 189) and evaluates IRI at every point along each traced line through `irisubgl` (line 233); `PlotLatVsFL()` / `PlotLatVsFLFIRI()` render the result. `source/igrf.for` additionally contains the field-line integrators `SHELLG` (line 161), `STOER` (398), `FELDG` (445) and the footprint routine `FTPRNT` (1602). *Caveat: the trace itself is delegated to the optional `pyapex` dependency; `LatVsFL()` raises `ImportError` if it is absent (line 153).* |
| Coordinate Transforms | User-facing geographic↔geomagnetic handling: `jmag` argument (`0: geographic; 1: geomagnetic`) is a public parameter of both `IRI2016.IRI()` (`pyiri2016/__init__.py` line 134) and `IRI2016Profile.__init__` (line 237). |
| Coordinate Transforms:Ionospheric | `source/igrf.for` implements the ionospheric/geomagnetic coordinate machinery, and the following routines are all **verified reachable** from the Python API: `GEODIP` (line 872), called unconditionally at `source/irisub.for:840`; `igrf_dip` (line 99), returning dip, modip and `ymodip`, reachable via the default `jf(18)=1` at `irisub.for:844`; `fmodip`, reachable via `EXTERNAL FMODIP`/`REGFA1` at `irisub.for:394,1264`; and the magnetic-local-time routine `CLCMLT` (line 3931), called unconditionally at `irisub.for:879` to compute `XMLT`. These alone are sufficient to justify this value. `LatVsFL()` returns quasi-dipole/Apex coordinates to the user in `self.qdcoordl` (line 200); `LatVsLon()` returns the dip angle in `data2D['dip']` (line 123) and contours it on the maps. *Not cited as evidence (unreachable):* `GEOCGM01` (line 933) is called only from `irisub.for:1235` behind `if(jf(33))`, and `Switches()` in `pyiri2016/__init__.py:73` hardcodes `jf[33-1] = 0` with no public override — so `GEOCGM01`, and `FTPRNT`, `GEOLOW`, `MLTUT` (1485) and most `CORGEO`/`GEOCOR` call sites reachable only through it, are dead code in this wrapper. |
| Data Processing and Analysis | The package post-processes raw Fortran output arrays into physical quantities and Python dictionaries before returning them. |
| Data Processing and Analysis:Analysis | Derived scientific quantities: total electron content via `source/iritec.for` (`IRIT13`, `IONCORR`, `IRI_TEC`, driven by `h_tec_max` at `pyiri2016/__init__.py` line 137); critical frequency foF2 computed from NmF2 as `9.0 * NmF2**0.5 * 1e-6` (`iri2016prof2D.py` lines 483, 563, 637); MUF map workflow `Plot2DMUF()` (line 558); ion densities converted from percent to m⁻³ (`__init__.py` lines 184-191); 2-D spatial interpolation of foF2/hmF2/B0 with `scipy.interpolate.interp2d` in `IntLatVsLon()` (line 626). |
| Data Processing and Analysis:Processing | Data-conditioning pipeline: `_RmZeros()` and `_RmNeg()` replace zero/negative fill values with NaN (`__init__.py` lines 210-224), `numpy.ma.masked_where` NaN masking (`iri2016prof2D.py` line 336), array slicing/reshaping, log₁₀ scaling. |
| Data Processing and Analysis:Data Access and Retrieval | `pyiri2016/api/update.py` `retrieve(url, filename, directory)` downloads and safely un-tars remote archives; `settings/settings.py` defines the endpoints `https://irimodel.org/IRI-2016` (`00_iri.tar` Fortran source + IGRF coefficients), `https://irimodel.org/COMMON_FILES` (`00_ccir-ursi.tar`), and `https://chain-new.chain-project.net/echaim_downloads` (`apf107.dat`, `ig_rz.dat`). Covered by `tests/test_api.py`. |
| Data Visualization | `pyiri2016/iri2016prof2D.py` plus `examples/*.py` and `scripts/*.py` build and save matplotlib figures. |
| Data Visualization:2D Graphics | `Plot2D()` `pcolor` height-vs-time panels for Ne/Te/Ti (line 435-455); `mpl_toolkits.basemap.Basemap` world maps with coastlines, countries, parallels and meridians plus dip-angle contours (lines 460-492, `MapPColor`, `MapPColorInt`); `contourf` panels in `PlotLatVsFL()`, `PlotLatVsFLFIRI()`, `PlotFIRI2D()`. |
| Data Visualization:Line Plots | `examples/iri1DExample01.py`, `iri1DExample01b.py`, `iri1DExample02.py`, `iri1DExample08.py` — `pn.plot()` of Ne/Ti/Te vs altitude, NmF2/NmF1/NmE and hmF2/hmF1/hmE vs hour, ion densities vs altitude, with log axes and legends. |

**Considered and deliberately EXCLUDED (audit trail):**

| Candidate | Why excluded |
|---|---|
| Coordinate Transforms:Magnetospheric | `source/igrf.for` does contain the Tsyganenko-style GEO↔MAG↔SM↔GSM stack (`GEOMAG` 3820, `MAGSM` 3860, `SMGSM` 3896, `RECALC` 3373, `SPHCAR` 3751, `BSPCAR` 3793). Excluded on **output-frame** grounds rather than pure unreachability, which is the precise argument: `GEOMAG`, `RECALC` and `SPHCAR` *do* execute on every call — `irisub.for:840` calls `GEODIP` unconditionally, and `GEODIP` (`igrf.for:872-911`) calls `SPHCAR` (897,899) and `GEOMAG` (898), which calls `RECALC` (3845). But their only product is a **geomagnetic-dipole** conversion (`MLAT`/`MLONG`, surfaced as `OARR(25-27,49,50)` → dip / dip-lat / modip / geomagnetic lat / geomagnetic lon, exposed as `data2D['dip']`) — an Ionospheric-class result, never an SM or GSM magnetospheric frame. The genuinely unreachable routines are `MAGSM`, `SMGSM` and `BSPCAR`, which are the only ones that would produce a magnetospheric frame: `generate_f2py.py` restricts the f2py build to `only: iriwebg irisubgl firisubl :` and `source/iriweb.pyf` exposes exactly those three subroutines. No magnetospheric coordinate ever reaches a Python user. |
| Data Processing and Analysis:2D Slices / Data Visualization:2D Slices | `HeightVsTime()` and `LatVsLon()` evaluate the model on a 2-D grid; they do not slice a pre-existing 3-D data volume. |
| Data Processing and Analysis:Time Series Analysis | `HrProfile()` / `HeightVsTime()` *generate* diurnal series; no temporal filtering, autocorrelation, trend or spectral analysis exists. |
| Data Visualization:Movies | `figures/iri2DExample02.gif` is a pre-rendered banner asset committed to the repo; grep for `animation`, `FuncAnimation`, `imageio`, `ffmpeg` across all `*.py` returns nothing. No animation code exists at HEAD. |
| Servers and Environments:Software or Environment Container | `.devcontainer/Dockerfile` is a VS Code developer container (`mcr.microsoft.com/vscode/devcontainers/python`), not a distributed runtime artifact of the software. CHANGELOG v1.1.0 "Python + Fortran in a Docker image for f2py" refers to the same developer convenience. |
| Data Processing and Analysis:File Format Conversion | `api/update.py` untars archives; that is decompression, not scientific format conversion. |
| Models and Simulations:Forecasting | IRI is a **climatological/empirical** model driven by monthly-median coefficient maps and historical solar/magnetic indices (`apf107.dat`, `ig_rz.dat`); it assimilates no real-time observations and produces no forecast product. The `jf(26)`/`jf(35)` storm models perturb the climatology from past indices rather than predicting forward. Noted explicitly because the Field 27 model paper's title ("…to real-time weather predictions") describes an aspiration of the wider IRI programme, not a capability of this wrapper. |

**Source:** README.md; pyproject.toml; CMakeLists.txt; generate_f2py.py; pyiri2016/__init__.py; pyiri2016/iri2016prof2D.py; pyiri2016/api/update.py; settings/settings.py; source/igrf.for; source/iritec.for; source/iriflip.for; source/iridreg.for; source/cira.for; source/iriweb.pyf; examples/*.py; scripts/*.py; tests/*.py

### 5. Related Region (MANDATORY)
- **Earth Atmosphere**
- **Earth Ionosphere**
- **Earth Thermosphere**
- **Rationale, Earth Atmosphere:** The International Reference Ionosphere models Earth's ionosphere (roughly 50-2000 km), which is part of the upper atmosphere. `pyproject.toml` classifies the package under `Topic :: Scientific/Engineering :: Atmospheric Science`.
- **Rationale, Earth Ionosphere:** The package identifies itself as a wrapper for the International Reference Ionosphere (`README.md:10`), and its public return dictionary consists of ionospheric electron density, temperatures, FIRI density, and ion composition (`pyiri2016/__init__.py:192-203`).
- **Rationale, Earth Thermosphere:** `LatVsFL()` exposes NRLMSIS-00 neutral temperature and the He, O, N₂, O₂, Ar, H, and N neutral composition (`pyiri2016/iri2016prof2D.py:239,248-254`); the bundled model labels those outputs as neutral-atmosphere densities and temperatures (`source/irisub.for:286,1933-1944`).
- **Considered and excluded:** *Earth Magnetosphere* — although `igrf.for` computes IGRF field, L-shell and corrected geomagnetic coordinates, and `LatVsFL()` follows field lines, the modelled domain and all output quantities are ionospheric/thermospheric, not magnetospheric plasma. Listing it would over-broaden search results. The 2026-07-27 decision 12 confirming this exclusion also governs the finer Earth Inner Magnetosphere, Earth Outer Magnetosphere, Earth Magnetotail, and Earth Magnetosheath rows: none describes a user-visible magnetospheric-plasma output. Earth Auroral Subregion is independently excluded because the wrapper hard-codes the auroral-boundary model off (`pyiri2016/__init__.py:73`). Earth Ionosphere and Earth Thermosphere transcribe the same settled rationale into the finer region rows now available; they do not reverse decision 12.
- **Source:** README.md; pyproject.toml; pyiri2016/__init__.py; pyiri2016/iri2016prof2D.py; source/irisub.for; package examples

### 6. Authors (MANDATORY)

#### Author 1:
- **Author Name:** Ronald Ilma
- **Author Identifier:** Not found
- **Affiliation - Organization:** Cornell University
- **Affiliation - Identifier:** https://ror.org/05bnh6r87
- **Source:** Zenodo record 240895 creator `Ronald Ilma`, affiliation `Cornell University`; DataCite creator `Ilma, Ronald` (`nameType: Personal`); LICENSE.md `Copyright (c) 2017 Ronald Ilma`; git author identity `Ronald Ilma <rri5@cornell.edu>`.
- **Name rationale:** Zenodo/DataCite, LICENSE.md, and the git identity use `Ronald Ilma`. Only `pyproject.toml` uses the fuller `Ronald R. Ilma Campana`, with the placeholder email `@example.com`. The settled form is therefore `Ronald Ilma`; the longer form remains documented as a rejected alternative rather than an open choice.
- **ORCID:** searched `pub.orcid.org` for `family-name:Ilma` (67 hits) and `family-name:"Ilma Campana"` (0 hits) on 2026-07-26 — no matching record. Zenodo/DataCite `nameIdentifiers` is empty. Genuinely Not found.
- **Affiliation cross-check:** the ROR API identifies Cornell University as `https://ror.org/05bnh6r87`. The name is already fully expanded.

**Considered and declined as a second author (decision 2, 2026-07-27):**
**Michael Hirsch** (GitHub `scivision`) is a major contributor to this repository with 29 commits, and is a named creator on the derivative Zenodo record `10.5281/zenodo.591802`. *Methodology note:* by raw `git shortlog -sn --all` he is third of eight identities with 29 of 169 commits = **17.2%**, but that ranking is an artifact of the author's own name being split across four unmerged identities (`Ronald I` 56, `Ronald Ilma` 32, `Ronald I.` 20, `rilma` 18). GitHub's deduplicated contributor API collapses those into the single account `rilma` and reports `scivision` at 29 of 116 = **25.0%, second overall**. Either way his share is substantial. However he appears in **no** author list for *this* repository: not in `pyproject.toml`, not in `LICENSE.md`, not in Zenodo record 240895, and there is no `CITATION.cff` / `codemeta.json` / `AUTHORS` file. Adding him would be a new authorship claim resting on git history alone, so he is not listed as an author.

### 7. Software Name (MANDATORY)

- **Software Name:** `pyIRI2016`
- **Previous incorrect HSSI value:** `pyIRI2016: Official release of the IRI2016 wrapper in Python`
- **Previous incorrect canonical-file value:** `IRI-2016`

**Evidence for `pyIRI2016`:**
1. README.md line 6 — the document's H1 title is exactly `# pyIRI2016`.
2. GitHub API `name: "pyIRI2016"`.
3. SoMEF `name` = `pyIRI2016` (confidence 1, GitHub_API) **and** `full_title` = `pyIRI2016` (confidence 1, regular_expression over README.md) — two independent techniques agree.
4. Python distribution/import name is `pyiri2016` (`pyproject.toml` `name = "pyiri2016"`; `pip install pyiri2016`; package dir `pyiri2016/`) — the same name, lowercased for PyPI.
5. Field 7's own instruction is "The name of the software package **as listed on the code repository**."

**Why the previous HSSI value was incorrect:**
- The GitHub release for tag `v1.1.0` is titled verbatim **"Official release of the IRI2016 wrapper in Python"** (GitHub releases API, published 2017-01-12T15:26:14Z).
- Zenodo record 240895 `metadata.title` is **"rilma/pyIRI2016: Official release of the IRI2016 wrapper in Python"** — the standard GitHub→Zenodo `owner/repo: <release title>` concatenation. DataCite `titles[0].title` is identical.
- The live HSSI name is that Zenodo/DataCite title with the `rilma/` owner prefix stripped. It is a **release title**, not a software name, and it also embeds a specific version's marketing text into a version-independent field.

**Why the previous canonical-file value was incorrect:**
- The prior file sourced `IRI-2016` from "PyHC registry / Google sheet". I read all three PyHC registry YAML files in full on 2026-07-26. The **only** entry named `IRI-2016` is in `projects_unevaluated.yml` and its `code` field is **`https://github.com/space-physics/iri2016`**, `contact: Michael Hirsch`, `description: International Reference Ionosphere 2016 from Python and Matlab`, `logo: https://iri.gsfc.nasa.gov/images/red_band-179.jpg`.
- That is a **different repository** from this HSSI entry's `codeRepositoryUrl` (`https://github.com/rilma/pyIRI2016`). The PyHC name `IRI-2016` therefore belongs to a *different software package* and must not be applied here. There is **no** PyHC entry for `rilma/pyIRI2016`.
- Consequence: the PyHC logo `https://iri.gsfc.nasa.gov/images/red_band-179.jpg` must likewise **not** be used for Field 33 of this entry (see Field 33).

The settled 2026-07-27 decision uses **`pyIRI2016`**. The lowercase `pyiri2016` is the PyPI/import spelling but loses the repository's capitalization; the two previous values remain excluded for the evidence above.

### 8. Description (MANDATORY)
- **Description:**

  Python wrapper for the International Reference Ionosphere (IRI) 2016 model. The package computes empirical ionospheric parameters including electron density, electron temperature, ion temperature, ion densities, NmF2, hmF2, B0, and total electron content as functions of location, time, altitude, and solar/geomagnetic conditions. It supports height, latitude, longitude, local-time, and 2D profile workflows, can evaluate the model along traced geomagnetic field lines, includes helpers for retrieving IRI-related source, coefficient and index files, and provides example plotting workflows for line plots and 2D maps. The IRI-2016 Fortran source is bundled and bound to Python with f2py through a CMake / scikit-build-core build; the package requires Python 3.11 or newer.

- **Previous description:** `Python wrapper for the International Reference Ionosphere (IRI) 2016 model.` (the 2017 Zenodo abstract). The current description preserves that sentence verbatim and adds the computations, workflows, and requirements necessary to characterize the software accurately.
- **Evidence for the additions:** TEC — `source/iritec.for` (`IRI_TEC`) and the `h_tec_max` parameter (`pyiri2016/__init__.py` line 137). Field lines — `IRI2016_2DProf.LatVsFL()` (`iri2016prof2D.py` line 140). Index files — `settings/settings.py` `INDICES_FILES = ["apf107.dat", "ig_rz.dat"]`. Build/Python — `CMakeLists.txt` (`find_package(Python 3.11 EXACT …)`), `pyproject.toml` (`requires-python = ">=3.11"`, `build-backend = "scikit_build_core.build"`), `generate_f2py.py`.
- **Source:** README.md; pyproject.toml; CMakeLists.txt; pyiri2016/__init__.py; pyiri2016/iri2016prof2D.py; pyiri2016/api/update.py; settings/settings.py; source/iritec.for; examples/README.md

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Python wrapper for the International Reference Ionosphere (IRI) 2016 model.
- **Reason:** the alternative `Python wrapper for the International Reference Ionosphere 2016 empirical ionospheric model.` is slightly more informative but only stylistically different. The selected value is preserved because it is the exact first sentence of Field 8 and therefore works as its preview.
- **Source:** Zenodo API record 240895 description; README.md line 10

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2017-01-12
- **Source:** Zenodo record 240895 `publication_date: "2017-01-12"`; DataCite `dates[] {dateType: "Issued", date: "2017-01-12"}`; GitHub release `v1.1.0` published `2017-01-12T15:26:14Z`; git tag `v1.1.0`.
- **Note:** This is the first *published* release. The repository itself was created 2016-11-01 (GitHub `created_at`); Field 10 asks for date of first publication, so 2017-01-12 is correct.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite `attributes.publisher = "Zenodo"`; Zenodo API record 240895; Field 11 guidance ("For software where a DOI has been obtained through Zenodo … Zenodo is the correct entry").
- **Note:** Field 11 prefers a ROR "when available … or URL otherwise". Zenodo has no ROR, so `https://zenodo.org` is the appropriate identifier.

### 12. Version (RECOMMENDED)

#### Version v1.2.0 (current):
- **Version Number:** v1.2.0
- **Version Date:** 2026-02-21
- **Version Description:** Upgrade to Python 3.11. Adds a fallback `TimeUtilities` implementation in `pyiri2016/__init__.py` for when the `timeutil` package is unavailable, and declares `timeutil` explicitly as a git dependency; fixes `NameError: name 'TimeUtilities' is not defined`; removes obsolete Poetry-era build files, the Meson alternative build, the deprecated `.travis.yml` CI config, and build artifacts.
- **Version PID:** Not found — the v1.2.0 GitHub release was not archived to Zenodo.
- **Source:** GitHub release `v1.2.0` "Upgrade to Python 3.11", published 2026-02-21T07:17:13Z; git tag `v1.2.0`; `pyproject.toml` `version = "1.2.0"`; `CHANGELOG.md` `## [1.2.0] - 2026-02-21`; `QUICKSTART.md` "What's New in v1.2.0"; SoMEF `version` = `1.2.0` (confidence 1).

#### Version v1.1.0 (archived DOI release — retained):
- **Version Number:** v1.1.0
- **Version Date:** 2017-01-12
- **Version Description:** First official release of the IRI2016 Python wrapper: `pyiri2016.IRI2016` class API, retrieval of Fortran/coefficient/index files, setuptools installation, unit test, Docker image for f2py, CHANGELOG, comprehensive README, Travis CI. Archived on Zenodo.
- **Version PID:** https://doi.org/10.5281/zenodo.240895
- **Source:** Zenodo record 240895 (`version: "v1.1.0"`); DataCite `version: "v1.1.0"`; git tag `v1.1.0`; GitHub release; `CHANGELOG.md` `## [1.1.0] - 2017-01-12`.

**Release inventory and selection rationale:** `git tag -l` and the GitHub Releases API expose exactly v1.1.0 and v1.2.0. Field 12 records the current release v1.2.0; v1.1.0 is retained above as historical release evidence because its DOI is also the persistent identifier in Field 2. The earlier v1.1.0 date `2023-04-25` was incorrect; Zenodo, DataCite, the tag, and the changelog all establish `2017-01-12`.

**Unreleased work at HEAD (informational, not a version):** `CHANGELOG.md` has a substantial `## [Unreleased]` section (CMake/scikit-build-core build system, `plotting` extras, ruff/mypy/pre-commit, headless plotting, coverage CI). Much of this is already present in the v1.2.0 tree; it has not been cut as a release, so it is not listed as a version.

### 13. Programming Language (RECOMMENDED)

**Values:**
- **Python 3.x**
- **Fortran77**
- **Fortran90**

**Live HSSI value:** `Fortran90`, `Java`, `Other`, `Python 3.x`, `Typescript`
**Prior canonical-file value:** `Python 3.x`, `Fortran77`

**Per-value evidence:**

| Value | Evidence |
|---|---|
| Python 3.x | `pyproject.toml` `requires-python = ">=3.11"` and classifiers for 3.10/3.11/3.12; `CMakeLists.txt` `find_package(Python 3.11 EXACT …)`; CI matrix `python-version: ["3.11"]`; 16 tracked `.py` files; GitHub languages `Python: 49,541 bytes`. |
| Fortran77 | All ten `source/*.for` files are **fixed-form** source: `c`/`C` comment markers in column 1, continuation characters in column 6 (`grep -c "^     [^ ]" source/irifun.for` → 3,525 lines), `Cf2py` directives in column 1. `gfortran` compiles `.for` as fixed form. GitHub languages `Fortran: 2,363,225 bytes` (94% of the repo). |
| Fortran90 | The same fixed-form files use Fortran-90 language features: attribute declarations `real, intent(in) ::` / `real*8, intent(out) ::` / `real, external ::` (`iriflip.for` 61 occurrences, `igrf.for` 12, `iriwebg.for` 7, `irisubg.for` 4, `irisub.for` 2, `iritec.for` 1) and `end do` block terminators (108 in `irifun.for`). |

**Fortran77 + Fortran90 rationale:** the source is genuinely a hybrid — F77 *fixed source form* carrying F90 *language features*. Both entries are individually true, so the set union is kept rather than choosing one and dropping the other. This resolves the HSSI-vs-file disagreement without discarding either supported value.

**Previous values considered and excluded:**

| Removal | Justification |
|---|---|
| **`Java`** | Zero evidence anywhere. `git ls-files` extension census: `.dat` 30, `.asc` 24, `.py` 16, `.for` 10, `.png` 6, `.md` 5, `.pyf` 3, `.json` 3, `.txt` 2, plus one each of `.yml`, `.yaml`, `.toml`, `.sh`, `.gif`, `.f`, `.c`, `Makefile`, `Dockerfile`, `.gitignore`. `git rev-list --all --objects \| grep -iE '\.(java\|ts\|tsx\|jsx\|js)$'` across **all** branches returns nothing. GitHub languages API lists no Java. No JVM tooling, no build file, no import. |
| **`Typescript`** | Same evidence — no `.ts`/`.tsx` in any branch, no `package.json`, no `tsconfig.json`, no npm/node tooling. The only Node reference in the entire repo is `.devcontainer/devcontainer.json` `"NODE_VERSION": "none"` and the correspondingly disabled `.devcontainer/Dockerfile` line `RUN if [ "${NODE_VERSION}" != "none" ]; …` — i.e. Node is explicitly **turned off**. `.vscode/extensions.json` recommends only `vscode-icons-team.vscode-icons` and `ms-python.python`. |
| **`Other`** | Every language present in the repository is now identified by name. GitHub languages: Fortran, Python, C, CMake, Makefile, Dockerfile, Shell. CMake/Makefile/Dockerfile/Shell are build tooling, not "languages most important for the software", and none appears in the allowed-value list; `Other` adds no information once Python 3.x / Fortran77 / Fortran90 are present. The 2026-07-27 decision 5 therefore excludes it. |

**C considered and excluded (decision 4, 2026-07-27):** GitHub reports `C: 25,883 bytes`, `CMakeLists.txt` declares `project(pyiri2016 LANGUAGES C Fortran)`, and `source/iriwebmodule.c` is committed and compiled into the shipped extension. Its header reads `This file is auto-generated with f2py (version:2.2.6). … Do not edit this file directly`; it is machine-generated glue, not authored source, so C is not listed.

**Source:** pyproject.toml; CMakeLists.txt; generate_f2py.py; source/*.for; source/iriwebmodule.c; .github/workflows/smoke.yml; .devcontainer/*; .vscode/extensions.json; `git ls-files`; `git rev-list --all --objects`; GitHub languages API; SoMEF `programming_languages`

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication DOI:** Not found
- **Note:** There is no `CITATION.cff`, `codemeta.json`, `.zenodo.json`, "How to cite" section, or JOSS/software paper. Zenodo record 240895 has no `IsDescribedBy` related identifier. The scientific DOIs embedded in the bundled IRI Fortran comments describe the underlying IRI model, not this Python wrapper, so they do not belong in Field 14.
- **Source:** Full repository search; Zenodo API 240895 `relatedIdentifiers`; DataCite `relatedIdentifiers`.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html
- **SPDX ID:** MIT
- **Source:** `LICENSE.md` (`MIT License / Copyright (c) 2017 Ronald Ilma`, full MIT text); `pyproject.toml` `license = {text = "MIT"}` and classifier `License :: OSI Approved :: MIT License`; GitHub API `license: {key: "mit", spdx_id: "MIT"}`; README badge `License: MIT`; SoMEF `license` (confidence 1, `spdx_id: MIT`).
- **Note on a conflicting source:** Zenodo record 240895 carries `license: {id: "other-open"}`. That is stale 2017 metadata; the repository's own `LICENSE.md`, `pyproject.toml`, GitHub's license detector and SoMEF all agree on MIT. Repository evidence is preferred.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values:**

- Atmospheric Modelling
- F2Py
- Fortran
- Ionosphere
- Ionosphere Modeling
- Python
- Standard

- electron density — `IRI()` returns `iri["ne"]`; `outf(1,*)`
- electron temperature — `iri["te"]`
- ion temperature — `iri["ti"]`
- IRI — the model acronym used throughout
- International Reference Ionosphere — README.md line 10
- empirical model — CCIR/URSI coefficient maps
- ionospheric physics — domain term

- total electron content — `source/iritec.for` (`IRIT13`, `IONCORR`, `IRI_TEC`); `h_tec_max` parameter
- NmF2 — returned in `iriadd["NmF2"]`, plotted in `iri1DExample08.py`
- hmF2 — returned in `iriadd["hmF2"]`
- IGRF — `source/igrf.for`; `data/igrf/dgrf1945…igrf2015s.dat`; optional `pyigrf` integration
- thermosphere — `source/cira.for` (NRLMSIS-00) neutral densities O, O₂, N₂, He, H, N, Ar exposed via `LatVsFL()`

*Considered and excluded by decision 6 (2026-07-27):* `CMake` and `scikit-build-core` are build tooling, not science keywords.

**Note on the seven published keywords:** the prior canonical file also listed `atmospheric-modelling`, `f2py`, `fortran`, `ionosphere`, `ionosphere-modeling`, `python`, `standard` — these are the raw GitHub repository topics, i.e. lowercase/hyphenated **variants of the same seven concepts** already published in HSSI in Title Case. They have been normalised into the published forms rather than listed twice, so HSSI does not acquire duplicate keyword rows. No concept is lost.

**Source:** GitHub repository topics (`atmospheric-modelling, f2py, fortran, ionosphere, ionosphere-modeling, python, standard`, also returned by SoMEF `keywords` at confidence 1); README.md; pyproject.toml; source/iritec.for; source/igrf.for; source/cira.for; CHANGELOG.md

### 17. Data Sources (OPTIONAL)
- **HTTP/HTTPS Directories**
- **Other** — bundled IRI coefficient and index files shipped inside the package

**Evidence:** `settings/settings.py` defines three HTTPS endpoints — `FORTRAN_CODE_URL = "https://irimodel.org/IRI-2016"` (`00_iri.tar`), `COMMON_FILES_URL = "https://irimodel.org/COMMON_FILES"` (`00_ccir-ursi.tar`), `INDICES_URL = "https://chain-new.chain-project.net/echaim_downloads"` (`apf107.dat`, `ig_rz.dat`). `pyiri2016/api/update.py` `retrieve()` fetches them with `wget.download` and safely extracts tarballs; exercised by `tests/test_api.py`. The package additionally ships 54 data files locally (`data/ccir` 12, `data/ursi` 12, `data/mcsat` 12, `data/igrf` 16, `data/index` 2 — confirmed by `find data -type f | wc -l` → 54, installed to `pyiri2016/data/…` by `CMakeLists.txt`) which the Fortran reads via the `dirdata` argument — hence `Other`.

**Considered and excluded:** `Observatory/Mission-specific` — the `chain-new.chain-project.net` host (Canadian High Arctic Ionospheric Network) is used **only** as a mirror for the generic IRI solar/magnetic index files `apf107.dat` and `ig_rz.dat`. The software does not read any CHAIN instrument data, so this is a plain HTTPS directory, not observatory-specific access (see also Fields 31/32).

**Source:** settings/settings.py; pyiri2016/api/update.py; tests/test_api.py; CMakeLists.txt; data/*

### 18. Input File Formats (RECOMMENDED)
- **ascii**

**Evidence:** all bundled model inputs are plain-text: `data/ccir/ccir11-22.asc` and `data/ursi/ursi11-22.asc` (CCIR/URSI foF2 and M(3000)F2 coefficient maps), `data/igrf/dgrf1945-2010.dat` + `igrf2015.dat` + `igrf2015s.dat` (IGRF/DGRF spherical-harmonic coefficients), `data/index/apf107.dat` and `ig_rz.dat` (magnetic and solar indices), `data/mcsat/mcsat11-22.dat`. They are read by the Fortran through the `dirdata` path argument (`read_ig_rz`, `readapf107`, `GETSHC` in `igrf.for`).

**Considered and excluded:** `Other` for the `.tar` archives retrieved by `api/update.py` — tar is a transport container around the same ascii files, not a science data format.

**Source:** data/ccir; data/igrf; data/index; data/mcsat; data/ursi; source/irifun.for; source/igrf.for; settings/settings.py

### 19. Output File Formats (RECOMMENDED)
- **Other** — PNG raster figures produced by the plotting and example workflows

**Evidence:** the core model API returns Python dictionaries and NumPy arrays in memory rather than writing science-data files (`IRI2016.IRI()` returns `iri, iriadd`; `IRI2016Profile` exposes `self.a`, `self.b`). The only files the package writes are PNG figures: `iri2016prof2D.py` `Plot2D()`, `PlotFIRI2D()`, `PlotLatVsFL()`, `PlotLatVsFLFIRI()`, `Plot2DMUF()` all call `savefig(str(filepath), dpi=100, bbox_inches="tight")` into `figures/` with UUID-suffixed names; `examples/iri1DExample01.py`, `iri1DExample01b.py`, `iri1DExample02.py`, `iri1DExample08.py` do the same.

**Considered and excluded:** `ascii` — the `verbose=True` paths in `HeiProfile()`, `LatProfile()`, `LonProfile()`, `HrProfile()` print formatted tables to **stdout**, not to a file. `source/iritest.for` writes text output but is not part of the f2py interface (`generate_f2py.py` exposes only `iriwebg`, `irisubgl`, `firisubl`).

**Source:** pyiri2016/iri2016prof2D.py; examples/*.py; scripts/*.py; generate_f2py.py

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**

**Rationale:** pure-Python front end (3.11+) over a Fortran extension built with CMake ≥3.15 + scikit-build-core, a deliberately cross-platform toolchain. README.md: "modern CMake-based build system with scikit-build-core for **cross-platform** compilation"; QUICKSTART.md: "CMake 3.15+ for cross-platform compilation" and "Reproducible across platforms". Requirements are only Python 3.11, NumPy ≥2.0, CMake, Ninja and a Fortran compiler (gfortran) — all available on Linux, macOS and Windows. No OS-specific code paths, no platform-conditional dependencies in `pyproject.toml`.

**Caveat:** CI verifies **Linux only** (`.github/workflows/smoke.yml` — all three jobs `runs-on: ubuntu-latest`, installing `gfortran cmake ninja-build` via `apt-get`), and the devcontainer is Debian bullseye. The selected `Operating System Independent` value rests on the project's explicit cross-platform design and documentation; macOS and Windows are not independently tested by CI.

**Source:** README.md; QUICKSTART.md; pyproject.toml; CMakeLists.txt; Makefile; .github/workflows/smoke.yml; .devcontainer/Dockerfile

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Rationale:** Python + NumPy + compiled Fortran/C extension code with no SIMD intrinsics, no assembly, no GPU code, no MPI, and no architecture-conditional build logic. `CMakeLists.txt` sets only `target_compile_options(iriweb PRIVATE -w)` (warning suppression) and `cmake.build-type = "Release"`; nothing pins an ISA. Builds wherever gfortran and CPython exist. `.devcontainer/devcontainer.json` explicitly notes, on its `VARIANT` build argument, "Use -bullseye variants on local on arm64/Apple Silicon", indicating arm64 is anticipated.

**Source:** pyproject.toml; CMakeLists.txt; .devcontainer/devcontainer.json; .devcontainer/Dockerfile; repository source files

### 22. Related Phenomena (OPTIONAL)
- **Geomagnetic Storms**

**Note:** an earlier version of this note called the controlled vocabulary "entirely solar" and enumerated a stale six-value documentation list (which included a `Coronal Holes` phantom that has never been a row, and omitted the vocabulary's two geospace rows, `Geomagnetic Storms` and `Solar Wind`). That description was wrong: the vocabulary is not entirely solar, and `Geomagnetic Storms` applies directly to this terrestrial ionospheric model.

**Selection rationale:** The foF2 and foE ionospheric-storm models (`jf[26-1]`, `jf[35-1]`) are both switched on, and ionospheric storms are an ionospheric signature of geomagnetic storms. `Geomagnetic Storms` was previously excluded only because the stale documentation list hid the row. Its selection on 2026-08-24 is consistent with decision 8 from 2026-07-27 to use only the controlled Phenomena vocabulary.

**Other phenomena considered and excluded:** Only phenomena that this wrapper actually computes were considered, following a reachability audit of `pyiri2016/__init__.py` `Switches()`:

*Genuinely active and user-visible:*
- **ionospheric storms** — `jf[26-1]` (foF2 storm model) and `jf[35-1]` (foE storm model), both switched **on** in the `year >= 1958` branch at `__init__.py` lines 124-125.
- **equatorial F-region vertical drift** — `jf[21-1]` "ion drift computed", enabled by default and surfaced to the user as `V_y` in `examples/iri1DExample08.py`.

*Latent model capability, NOT computed by this wrapper (do not list):*
- **spread F** — `jf[28-1]` is hardcoded to `0` at `__init__.py` line 67.
- **auroral boundary** — `jf[33-1]` is hardcoded to `0` at `__init__.py` line 73.

Neither `IRI2016.IRI()`, `IRI2016Profile.__init__`, nor any path in `iri2016prof2D.py` exposes a mechanism to override an individual `jf` switch — the only conditional block (`IRI()` lines 114-126) touches solely `jf[17,25,26,27,32,35]`. So spread F and auroral boundary describe dormant Fortran capability, not behaviour of this package, and were dropped from the candidate list on evidence grounds before the user decision was taken.

The ionospheric-storm science is represented by the controlled row `Geomagnetic Storms`; equatorial vertical drift has no controlled row and remains unrepresented.

**Source:** pyiri2016/__init__.py `Switches()`; examples/iri1DExample08.py

### 23. Development Status (RECOMMENDED)
- **Active**

**Rationale:** the project has reached a stable, usable state and is still being developed. Evidence: stable release `v1.2.0` published 2026-02-21; `pyproject.toml` classifier `Development Status :: 5 - Production/Stable`; a modern maintained toolchain (CMake + scikit-build-core, NumPy ≥2.0, ruff, mypy, pre-commit, pytest+coverage, Codecov); a three-job GitHub Actions CI pipeline; a substantial `## [Unreleased]` section in `CHANGELOG.md`; and a repository that is neither archived nor disabled.

**Recency caveat:** the last code push was 2026-02-21 (GitHub `pushed_at`), about five months before extraction; `updated_at` was 2026-07-07. Together with the stable release and ongoing unreleased work, this supports `Active` under repostatus.org.

**Source:** GitHub release v1.2.0; git tag v1.2.0; GitHub repository metadata (`archived: false`, `pushed_at`, `open_issues_count`); CHANGELOG.md; pyproject.toml; .github/workflows/smoke.yml

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/rilma/pyIRI2016

**Note:** there is no separate documentation site. GitHub API reports `has_pages: false` and an empty `homepage`; there is no `docs/` directory, no `.readthedocs.yml`, and no Sphinx/MkDocs configuration. Documentation lives in the repository: `README.md` (install, quick start, test targets, example gallery, build-system reference), `QUICKSTART.md` (detailed build/test/troubleshooting guide), `examples/README.md` (how to run the 1D and 2D examples), and `CHANGELOG.md`. The repository root URL is therefore the correct single entry point, per Field 24's "If this is the same as the access URL, then enter that link here."

**Considered:** `https://github.com/rilma/pyIRI2016/blob/main/QUICKSTART.md` is the most detailed installation document, but it is reachable from the README and is narrower than the field's intent. The GitHub wiki (`has_wiki: true`, `/wiki` returns HTTP 200 via redirect) has no substantive content and was not used.

**Source:** README.md; QUICKSTART.md; examples/README.md; GitHub API repository metadata

### 25. Funder (OPTIONAL)
- **Not found**
- **Note:** Zenodo record 240895 and DataCite both have empty `fundingReferences`. No acknowledgement, funding statement, grant number or sponsor appears in README.md, QUICKSTART.md, CHANGELOG.md, LICENSE.md, `pyproject.toml`, or the bundled Fortran headers (which credit model authors, not funders). The author's Cornell University affiliation is an affiliation (Field 6), not a funder.
- **Source:** Zenodo API record 240895; DataCite; full repository search

### 26. Award Title (OPTIONAL)
- **Not found**
- **Source:** Zenodo API record 240895 (`fundingReferences` empty); full repository search

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- **Not found**

**Candidate publication considered and declined (decision 9, 2026-07-27):** Bilitza, D., Altadill, D., Truhlik, V., Shubin, V., Galkin, I., Reinisch, B., & Huang, X. (2017), *International Reference Ionosphere 2016: From ionospheric climate to real-time weather predictions*, Space Weather, 15(2), 418-429, `https://doi.org/10.1002/2016SW001593`. The DOI is genuine; note that `10.1002/2017SW001593` is not valid.

**Why it was declined:** two reservations, both decisive.
1. *Not cited in the repository.* The citation appears nowhere in the repo; it was inferred from the software's subject and its `irimodel.org` links.
2. *Fits neither field's definition.* Field 27 wants publications that "describe, cite, or use the software". This paper describes the underlying IRI-2016 **model**, not `rilma/pyIRI2016`, and neither cites nor uses this repository — its 2017-02 publication essentially coincides with, rather than follows, the wrapper's 2017-01-12 v1.1.0 release. Field 14 was ruled out on exactly the same reasoning, so the paper satisfies the literal definition of *neither* field.

Recording an inferred, uncited citation would assert a relationship the evidence does not support, so Field 27 remains empty. Retained here as an audit trail so the candidate is not silently rediscovered and re-proposed by a future extraction.

**Source:** Full repository search; README.md; settings/settings.py; Crossref API

### 28. Related Datasets (OPTIONAL)
- **Not found**
- **Note:** the package ships genuine datasets (CCIR and URSI ionospheric coefficient maps, IGRF/DGRF 1945-2015 spherical-harmonic coefficients, `apf107.dat` / `ig_rz.dat` solar and magnetic indices, `mcsat*.dat`), but none of them has a DOI or an APA-citable dataset landing page. They are distributed as bare files from `irimodel.org` and `chain-new.chain-project.net`. Recorded under Field 17 (Data Sources) and Field 18 (Input File Formats) instead.
- **Source:** data/*; settings/settings.py; Zenodo API record 240895 `relatedIdentifiers`

### 29. Related Software (OPTIONAL)

#### Related Software 1: Time Utilities (`timeutil`)
- **URL:** https://github.com/rilma/TimeUtilities
- **Relationship:** Companion package by the same author; required runtime dependency.
- **Specific evidence:** README.md line 21 — "This also installs [Time Utilities](https://github.com/rilma/TimeUtilities)"; `pyproject.toml` dependency `timeutil @ git+https://github.com/rilma/TimeUtilities.git`; `pyiri2016/__init__.py` lines 8-21 import `TimeUtilities` and ship a **fallback re-implementation** of `ToHMS()` for when it is unavailable; `iri2016prof2D.py` lines 40-44 and line 179 (`TimeUtilities().CalcDOY(...)`).
- **Selection rationale (decision 11, 2026-07-27):** Field 29 includes companion packages, and Time Utilities is by the same author, named in the README, declared as a dependency, and important enough that pyIRI2016 ships a fallback re-implementation. Its `ToHMS()` and `CalcDOY()` functions are generic calendar arithmetic, which would normally fail the relevance gate, but the settled decision retains it for the unusually direct companion-package relationship. This tension is recorded so the choice is not silently reversed.

#### Related Software 2: IRI-2016 (space-physics / iri2016)
- **Identifier:** https://doi.org/10.5281/zenodo.591802
- **Same package, alternate identifier (not separately listed):** https://github.com/space-physics/iri2016
- **Relationship:** Independent Python (and MATLAB) wrapper for the same IRI-2016 model — *performs similar tasks* — and a **descendant of this repository**.
- **Specific evidence:** the DOI `10.5281/zenodo.591802` is the Zenodo **concept DOI** for `scivision/pyIRI2016` (DataCite title "scivision/pyIRI2016 v1.2.1_1"; abstract "International Reference Ionosphere 2016 for Python"; creators "Ronald, I." and "Michael Hirsch, Ph.D." / SciVision, Inc.; `IsSupplementTo https://github.com/scivision/pyIRI2016/tree/v1.2.1_1`; latest version record 556843). `scivision/pyIRI2016` no longer exists under that name — `https://api.github.com/repos/scivision/pyIRI2016` returns **HTTP 301** (`Location: .../repositories/123071113`), a rename redirect, not a 404 — and the line continues as `space-physics/iri2016` ("International Reference Ionosphere 2016 from Python and Matlab"), which is the package PyHC registers under the name `IRI-2016` in `projects_unevaluated.yml`. Michael Hirsch (`scivision`) is a major contributor to *this* repository with 29 commits (25.0% and second overall by GitHub's deduplicated contributor stats; 17.2% by raw `git shortlog`), confirming the shared lineage.
- **Identifier rationale (decision 2026-07-27):** the DOI and GitHub URL identify the same package, so listing both would duplicate it. The DOI is the more durable identifier because it survived the `scivision` → `space-physics` rename. This software belongs in Field 29 as a similar-purpose descendant, rather than Field 30: there is no adapter, converter, shared data model, plugin relationship, or documented exchange between the two independent wrappers.

#### Related Software 3: IRI-2016 Fortran model (upstream)
- **URL:** https://irimodel.org/
- **Relationship:** The upstream Fortran model that this package wraps and redistributes.
- **Specific evidence:** README.md line 10 links `http://irimodel.org/`; `settings/settings.py` `FORTRAN_CODE_URL = "https://irimodel.org/IRI-2016"` with `00_iri.tar`, and `COMMON_FILES_URL = "https://irimodel.org/COMMON_FILES"` with `00_ccir-ursi.tar`; `pyiri2016/api/update.py` `retrieve()` downloads and extracts them; the ten `source/*.for` files are that distribution verbatim, including their original version headers.
- **Identifier rationale:** Per Field 29's "If no public repository, enter link where users can find more information", `https://irimodel.org/` is the canonical distribution page. The site may return 406 to unbranded user agents but serves normally to browsers.
- **Note:** this is arguably the single most distinguishing related-software entry for this package.

**Considered and EXCLUDED from both Field 29 and Field 30 (Tier A generic infrastructure — audit trail):**
`numpy`, `scipy`, `matplotlib`, `seaborn`, `basemap` / `basemap-data` (mapping — the peer of the explicitly Tier-A `cartopy`), `beautifulsoup4`, `wget`, `simple-settings`, `pytest`, `pytest-cov`, `coverage`, `parameterized`, `pre-commit`, `ruff`, `mypy`, `cmake`, `ninja`, `scikit-build-core`, `setuptools`. Each fails the "would this be equally at home in a web app, a finance model, or a biology pipeline?" test; listing any of them would say nothing specific about pyIRI2016.

**Source:** README.md; pyproject.toml; pyiri2016/__init__.py; pyiri2016/iri2016prof2D.py; settings/settings.py; DataCite `10.5281/zenodo.591802`; Zenodo record 556843; GitHub API; PyHC `projects_unevaluated.yml`

### 30. Interoperable Software (OPTIONAL)

#### Interoperable Software 1: pyApex
- **URL:** https://github.com/rilma/pyApex
- **Relationship:** Demonstrated data exchange — pyApex's traced field-line geometry is consumed directly by pyIRI2016.
- **Specific evidence (not a dependency claim):** `pyiri2016/iri2016prof2D.py` `LatVsFL()` calls `gc, qc = pyapex.ApexFL().getFL(date=date2, dlon=dlon, dlat=dlat, hateq=h, mlatRange=mlatlim, mlatSTP=mlatstp)` at line 189, then feeds the returned geographic coordinate arrays into IRI via `irisubgl(jf, jmag, year, mmdd, hour2, curr_coordl[ind[0], :], DataFolder)` at line 233, and surfaces pyApex's quasi-dipole coordinates to the user as `self.qdcoordl` (line 200). The import is guarded (`try: import pyapex / except ModuleNotFoundError: pyapex = None`, lines 26-29) with an explicit `ImportError("pyapex is required for LatVsFL(). Install it with: pip install pyapex")` at line 153 — an optional, deliberate integration rather than a hard dependency. API match verified upstream: `class ApexFL` at `pyapex/__init__.py` line 37 and `def getFL(...)` at line 47 in `rilma/pyApex`.
- **Install caveat for the user:** the CHANGELOG and the runtime error message both say `pip install pyapex`, but the PyPI project named `pyapex` is an unrelated package ("Create interactive html charts", `nicodemus-opon/pyapex`). The correct package is `https://github.com/rilma/pyApex`, which is what the code's API actually matches. Recording the repository URL avoids propagating that ambiguity.

#### Interoperable Software 2: pyIGRF
- **URL:** https://github.com/rilma/pyIGRF
- **Relationship:** Demonstrated data exchange — pyIGRF's IGRF field output is substituted into pyIRI2016's own output arrays.
- **Specific evidence:** `pyiri2016/iri2016prof2D.py` `getIGRF()` calls `bn, be, bd, xl, icode = GetIGRF(lat, lon, alt, year)` at line 294 and yields the derived horizontal component `bh`; `LatVsFL()` line 256-258 then writes that result into `self.babs` **in place of** the model's internal `outf[19, :]` when `IGRF=True`. Import guarded at lines 31-34 (`from pyigrf.pyigrf import GetIGRF`) with `ImportError("pyigrf is required for IGRF calculations. …")` at line 289. API match verified upstream: `def GetIGRF(xlat=-11.95, xlon=283.13, height=0., year=2004.75)` at `pyigrf/pyigrf.py` line 8 in `rilma/pyIGRF` — signature and argument order match the call site exactly.
- **Install caveat:** the PyPI project `pyigrf` is `zzyztyy/pyIGRF` (IGRF-14), a different package whose API does not match this call. The repository URL is recorded for that reason.

**Previously misclassified here:** `https://doi.org/10.5281/zenodo.591802` identifies the similar-purpose descendant recorded in Field 29. It is excluded from Field 30 because the repositories have no demonstrated exchange.

**Considered and EXCLUDED:** the entire Tier A list under Field 29 applies here unchanged. Also excluded: `timeutil`/TimeUtilities — although imported, the exchange is one-way consumption of a generic `ToHMS`/`CalcDOY` helper (and pyIRI2016 ships a fallback re-implementation of it), which is dependency use, not peer-tool interoperation; it is recorded in Field 29 as a companion package instead. No blanket "part of the scientific Python ecosystem" claim is made anywhere in this field.

**Source:** pyiri2016/iri2016prof2D.py lines 26-44, 140-264, 286-299; CHANGELOG.md `[Unreleased] > Changed`; `rilma/pyApex` `pyapex/__init__.py`; `rilma/pyIGRF` `pyigrf/pyigrf.py`; GitHub API; PyPI API

### 31. Related Instruments (OPTIONAL)
- **Not found**

**Relevance-gate reasoning:** pyIRI2016 is an **instrument-agnostic** global empirical model. It reads no instrument's data products, implements no instrument-specific format or convention, is not an instrument-team tool, and does not calibrate or process any instrument's measurements. A user searching HSSI for a specific instrument would not expect this package back. No SPASE vocabulary resolution was required because nothing passes the gate.

**Considered and EXCLUDED (audit trail):**
- `AEROS`, `ISIS`, `AE-C`, `AE-E`, `Atmosphere Explorer`, `Jicamarca`, `Arecibo`, `digisonde`/`ionosonde`, `COSMIC`, `MGS` — these appear **only inside the bundled IRI Fortran comment headers** (`source/*.for`), documenting the historical measurement campaigns from which the IRI empirical coefficients were *derived decades ago*. The software neither reads nor supports data from any of them. The single Python-side mention, `pyiri2016/__init__.py` line 62 (`jf[23-1] = 0  #  23  Te_tops (Aeros,ISIS)  Te_topside (TBT-2011)`), is a switch label for which statistical topside-Te parameterisation to use — a model option, not instrument support.
- **CCIR / URSI coefficient maps** — derived from a global ionosonde network, but distributed as generic coefficient files with no instrument identity; recorded under Fields 17/18 instead.

**Source:** source/*.for; pyiri2016/__init__.py; full repository grep for instrument names

### 32. Related Observatories (OPTIONAL)
- **Not found**

**Relevance-gate reasoning:** the software is **observatory/mission-agnostic**. It is a global climatological model valid at any geographic location; it supports no mission's data conventions and is not a mission-team tool.

**Considered and EXCLUDED (audit trail):**
- **CHAIN (Canadian High Arctic Ionospheric Network)** — `settings/settings.py` `INDICES_URL = "https://chain-new.chain-project.net/echaim_downloads"`. This host is used purely as a **mirror for the generic IRI index files** `apf107.dat` (magnetic indices) and `ig_rz.dat` (solar indices). No CHAIN instrument or observatory data is read. Per the Field 32 guidance this is a generic data source → recorded under Field 17 as `HTTP/HTTPS Directories`, and `Observatory/Mission-specific` was deliberately **not** selected there.
- **irimodel.org** — the model distribution site, not an observatory. Recorded under Fields 17 and 29.
- The historical missions named in the bundled Fortran headers (AEROS, ISIS, Atmosphere Explorer) — excluded for the same reason as Field 31.

**Source:** settings/settings.py; pyiri2016/api/update.py; source/*.for

### 33. Logo (OPTIONAL)
- **Not found**
- **Note:** no logo asset or logo URL exists in the repository. SoMEF returned no `logo` key. GitHub reports no social-preview/homepage asset.
- **IMPORTANT — do NOT use `https://iri.gsfc.nasa.gov/images/red_band-179.jpg`.** That logo belongs to the PyHC `IRI-2016` entry, whose `code` field is `https://github.com/space-physics/iri2016` — a **different package** (see Field 7). Applying it here would compound the same mis-attribution that produced the prior file's incorrect software name.
- **Also not a logo:** `figures/iri2DExample02.gif`, displayed as a banner at README.md line 8, is an example model-output animation, not a project logo.
- **Source:** repository examination; SoMEF output; PyHC `projects_unevaluated.yml`
