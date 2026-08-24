# HSSI Metadata Extraction Results

**HSSI Software ID:** a53ebbd1-0f08-4bf6-aeaa-90067a3b1312
**Repository:** https://github.com/rilma/pyIRI2016
**Source Revision:** 1a47c6018aae8be93349fb2487c1911e95c1f99f
**Extraction Date:** 2026-07-26
**Validation Date:** 2026-08-24
**Validation Status:** PASS
**Applied to HSSI:** 2026-07-27 — `PATCH http://localhost/api/data/software/a53ebbd1-0f08-4bf6-aeaa-90067a3b1312/` returned HTTP 200 updating 16 fields; every changed field and every omitted field was roundtrip-verified against `GET /api/view/software/<uid>/`. Field 22 (`Geomagnetic Storms`) was additionally applied and roundtrip-verified 2026-08-24. Fields 2–33 below reflect the live, verified state.

**Seeded from:** live HSSI record (`GET http://localhost/api/view/software/a53ebbd1-0f08-4bf6-aeaa-90067a3b1312/`) + prior canonical `hssi_metadata.md` (extracted 2025-12-03, validated 2026-04-24), then verified against the repository at HEAD (`main`, commit dated 2026-02-21).

**Provenance legend used in this file:**
- `[HSSI]` — value currently published in the live HSSI record
- `[FILE]` — value carried over from the prior canonical `hssi_metadata.md`
- `[REPO]` — value derived/confirmed from the repository at the source revision
- `[API]` — value from Zenodo / DataCite / GitHub / ROR / PyHC / Crossref

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.240895
- **Status:** UNCHANGED — live HSSI, prior file, and re-verified Zenodo/DataCite metadata all agree.
- **Source:** `[HSSI]` `[FILE]` `[API]` README.md Zenodo DOI badge (line 1); Zenodo API record 240895; DataCite `10.5281/zenodo.240895`
- **Note:** Re-confirmed 2026-07-26. This is the version-specific DOI for the archived v1.1.0 release. Zenodo record 240895 has `conceptrecid: "591270"` but `conceptdoi: ""` (empty) — this is a legacy 2017 record that predates Zenodo concept DOIs, so **no concept DOI exists**. `https://doi.org/10.5281/zenodo.591270` is therefore not usable. There is no DOI for v1.2.0 (the v1.2.0 GitHub release was not archived to Zenodo).

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/rilma/pyIRI2016
- **Status:** UNCHANGED
- **Source:** `[HSSI]` `[FILE]` `[REPO]` `[API]` git remote `origin`; GitHub API `full_name: rilma/pyIRI2016`; SoMEF `code_repository` (confidence 1); Zenodo related identifier `https://github.com/rilma/pyIRI2016/tree/v1.1.0`
- **Note:** Repository is live, not archived, not a fork, default branch `main`, 21 stars / 12 forks as of 2026-07-26.

### 4. Software Functionality (MANDATORY)

**Proposed value (13 entries — union of live HSSI + prior file + fresh repository evidence):**

- **Coordinate Transforms** `[FILE]`
- **Coordinate Transforms:Ionospheric** `[FILE]`
- **Data Processing and Analysis** `[FILE]`
- **Data Processing and Analysis:Analysis** `[FILE]`
- **Data Processing and Analysis:Data Access and Retrieval** `[FILE]`
- **Data Processing and Analysis:Processing** `[FILE]`
- **Data Visualization** `[FILE]`
- **Data Visualization:2D Graphics** `[FILE]`
- **Data Visualization:Line Plots** `[FILE]`
- **Models and Simulations** `[HSSI]` `[FILE]`
- **Models and Simulations:Empirical** `[HSSI]` `[FILE]`
- **Models and Simulations:Field-line Tracing** — **NEW**
- **Models and Simulations:Physics-Based** — **NEW**

**Parent-category check:** every subcategory has its parent present — `Coordinate Transforms` ✓, `Data Processing and Analysis` ✓, `Data Visualization` ✓, `Models and Simulations` ✓. No orphaned subcategories.

**Per-value justification:**

| Value | Evidence |
|---|---|
| Models and Simulations | pyIRI2016 wraps and runs the IRI-2016 model; the entire package exists to evaluate a model. `pyiri2016/__init__.py` `IRI2016.IRI()`, `IRI2016Profile`. |
| Models and Simulations:Empirical | IRI is the canonical empirical/climatological ionosphere model: CCIR and URSI foF2/M(3000)F2 coefficient maps (`data/ccir/ccir11-22.asc`, `data/ursi/ursi11-22.asc`), statistical Te/Ti profiles, `data/mcsat/*.dat`. `pyproject.toml` topic `Scientific/Engineering :: Atmospheric Science`. |
| Models and Simulations:Physics-Based — **NEW** | `source/iriflip.for` is the FLIP/IDC photochemical ion-density model (`CHEMION` plus `CN2D, CNO, CN4S, CN2PLS, CNOP, CO2P, COP4S, COP2D, COP2P, CNPLS, CN2A, CN2P, CNOPV` production/loss and `RATS` reaction rates) — first-principles ion photochemistry, not a statistical fit. It is **enabled by default** by this wrapper: `pyiri2016/__init__.py` line 45 sets `jf[6-1] = 0`, selecting the "Ni - RBV-10 & TTS-03" option, i.e. the iriflip photochemical ion densities. `source/cira.for` (NRLMSIS-00 neutral atmosphere) and `source/iridreg.for` (Friedrich & Torkar 2001 FIRI D-region) are further physics-based components exposed via `firisubl`. |
| Models and Simulations:Field-line Tracing — **NEW** | `pyiri2016/iri2016prof2D.py` `IRI2016_2DProf.LatVsFL()` (line 140) traces geomagnetic field lines over a range of apex heights via `pyapex.ApexFL().getFL(date=…, dlon=…, dlat=…, hateq=h, mlatRange=…, mlatSTP=…)` (line 189) and evaluates IRI at every point along each traced line through `irisubgl` (line 233); `PlotLatVsFL()` / `PlotLatVsFLFIRI()` render the result. `source/igrf.for` additionally contains the field-line integrators `SHELLG` (line 161), `STOER` (398), `FELDG` (445) and the footprint routine `FTPRNT` (1602). *Caveat: the trace itself is delegated to the optional `pyapex` dependency; `LatVsFL()` raises `ImportError` if it is absent (line 153).* |
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

**Change summary:** live HSSI has only `Models and Simulations` + `Models and Simulations: Empirical`. This proposal **adds 11 values and removes none**.

**Whitespace note for the validator/updater:** the live HSSI record stores the string `"Models and Simulations: Empirical"` (space after the colon). The HSSI form's allowed-value list uses `Models and Simulations:Empirical` (no space). This file uses the allowed-list form. **These are the same value** — do not treat this as a removal + addition.

**Source:** `[REPO]` README.md; pyproject.toml; CMakeLists.txt; generate_f2py.py; pyiri2016/__init__.py; pyiri2016/iri2016prof2D.py; pyiri2016/api/update.py; settings/settings.py; source/igrf.for; source/iritec.for; source/iriflip.for; source/iridreg.for; source/cira.for; source/iriweb.pyf; examples/*.py; scripts/*.py; tests/*.py

### 5. Related Region (MANDATORY)
- **Earth Atmosphere**
- **Status:** UNCHANGED — live HSSI and prior file agree; re-verified.
- **Rationale:** The International Reference Ionosphere models Earth's ionosphere (roughly 50-2000 km), which is part of the upper atmosphere. `pyproject.toml` classifier `Topic :: Scientific/Engineering :: Atmospheric Science`. The bundled `source/cira.for` (NRLMSIS-00) additionally returns thermospheric neutral densities (O, O₂, N₂, He, H, N, Ar) to the user through `LatVsFL()` — still Earth Atmosphere.
- **Considered and excluded:** *Earth Magnetosphere* — although `igrf.for` computes IGRF field, L-shell and corrected geomagnetic coordinates, and `LatVsFL()` follows field lines, the modelled domain and all output quantities are ionospheric/thermospheric, not magnetospheric plasma. Listing it would over-broaden search results. **RESOLVED 2026-07-27 — user confirmed the exclusion** (decision 12); `Earth Atmosphere` alone is final.
- **Source:** `[HSSI]` `[FILE]` `[REPO]` README.md; pyproject.toml; package API and examples

### 6. Authors (MANDATORY)

#### Author 1:
- **Author Name:** Ronald Ilma
- **Author Identifier:** Not found
- **Affiliation - Organization:** Cornell University
- **Affiliation - Identifier:** https://ror.org/05bnh6r87
- **Status:** name REVERTED to the live HSSI form (prior file had `Ronald R. Ilma Campana`); affiliation UNCHANGED.
- **Source:** `[HSSI]` (givenName `Ronald` / familyName `Ilma`); `[API]` Zenodo record 240895 creator `Ronald Ilma`, affiliation `Cornell University`; DataCite creator `Ilma, Ronald` (`nameType: Personal`); `[REPO]` LICENSE.md `Copyright (c) 2017 Ronald Ilma`; git author identity `Ronald Ilma <rri5@cornell.edu>`
- **Reason for reverting to `Ronald Ilma`:** three of four authoritative author sources (live HSSI, Zenodo/DataCite, LICENSE.md) use `Ronald Ilma`. Only `pyproject.toml` uses the fuller `Ronald R. Ilma Campana`. Per the reconciliation rule, live HSSI wins a scalar conflict absent evidence that it is wrong — and here the repository's own LICENSE and git identity corroborate live HSSI rather than contradict it. Practical consideration: the HSSI PATCH API silently no-ops `Person` renames, so a rename would not take effect anyway.
- **Documented alternative (NOT proposed):** `Ronald R. Ilma Campana` — `pyproject.toml` line 5 (`authors = [{name = "Ronald R. Ilma Campana", email = "ronald.ilmacampana@example.com"}]`), also picked up by SoMEF at confidence 1. Note the email in `pyproject.toml` is the placeholder `@example.com`. Retained here so nothing is lost; user may elect the longer form.
- **ORCID:** searched `pub.orcid.org` for `family-name:Ilma` (67 hits) and `family-name:"Ilma Campana"` (0 hits) on 2026-07-26 — no matching record. Zenodo/DataCite `nameIdentifiers` is empty. Genuinely Not found.
- **Affiliation cross-check:** live HSSI affiliation object `bf476440-fe83-4a21-bc16-faa3c7c2365a` resolves to `Cornell University` / `https://ror.org/05bnh6r87`, matching the prior file and the ROR API lookup exactly. No change needed. Name is already fully expanded (no acronym).

**RESOLVED 2026-07-27 — possible second author considered and DECLINED (decision 2); not added:**
**Michael Hirsch** (GitHub `scivision`) is a major contributor to this repository with 29 commits, and is a named creator on the derivative Zenodo record `10.5281/zenodo.591802`. *Methodology note:* by raw `git shortlog -sn --all` he is third of eight identities with 29 of 169 commits = **17.2%**, but that ranking is an artifact of the author's own name being split across four unmerged identities (`Ronald I` 56, `Ronald Ilma` 32, `Ronald I.` 20, `rilma` 18). GitHub's deduplicated contributor API collapses those into the single account `rilma` and reports `scivision` at 29 of 116 = **25.0%, second overall**. Either way his share is substantial — the earlier "~13%, third" figure was wrong under both methodologies and understated him. However he appears in **no** author list for *this* repository: not in `pyproject.toml`, not in `LICENSE.md`, not in Zenodo record 240895, not in live HSSI, and there is no `CITATION.cff` / `codemeta.json` / `AUTHORS` file. Adding him would be a new authorship claim resting on git history alone, so it is flagged rather than asserted. **No existing author is being dropped by this decision.**

### 7. Software Name (MANDATORY) — RESOLVED 2026-07-27

- **Proposed value:** `pyIRI2016`
- **Former live HSSI value (REPLACED 2026-07-27):** `pyIRI2016: Official release of the IRI2016 wrapper in Python`
- **Former canonical-file value (REPLACED 2026-07-27):** `IRI-2016`

**Evidence for `pyIRI2016`:**
1. `[REPO]` README.md line 6 — the document's H1 title is exactly `# pyIRI2016`.
2. `[API]` GitHub API `name: "pyIRI2016"`.
3. `[API]` SoMEF `name` = `pyIRI2016` (confidence 1, GitHub_API) **and** `full_title` = `pyIRI2016` (confidence 1, regular_expression over README.md) — two independent techniques agree.
4. `[REPO]` Python distribution/import name is `pyiri2016` (`pyproject.toml` `name = "pyiri2016"`; `pip install pyiri2016`; package dir `pyiri2016/`) — the same name, lowercased for PyPI.
5. Field 7's own instruction is "The name of the software package **as listed on the code repository**."

**Evidence that the live HSSI value is release-title pollution (this is confirmed, not suspected):**
- The GitHub release for tag `v1.1.0` is titled verbatim **"Official release of the IRI2016 wrapper in Python"** (GitHub releases API, published 2017-01-12T15:26:14Z).
- Zenodo record 240895 `metadata.title` is **"rilma/pyIRI2016: Official release of the IRI2016 wrapper in Python"** — the standard GitHub→Zenodo `owner/repo: <release title>` concatenation. DataCite `titles[0].title` is identical.
- The live HSSI name is that Zenodo/DataCite title with the `rilma/` owner prefix stripped. It is a **release title**, not a software name, and it also embeds a specific version's marketing text into a version-independent field.

**Evidence that the prior canonical-file value `IRI-2016` is a mis-attribution (new finding this run):**
- The prior file sourced `IRI-2016` from "PyHC registry / Google sheet". I read all three PyHC registry YAML files in full on 2026-07-26. The **only** entry named `IRI-2016` is in `projects_unevaluated.yml` and its `code` field is **`https://github.com/space-physics/iri2016`**, `contact: Michael Hirsch`, `description: International Reference Ionosphere 2016 from Python and Matlab`, `logo: https://iri.gsfc.nasa.gov/images/red_band-179.jpg`.
- That is a **different repository** from this HSSI entry's `codeRepositoryUrl` (`https://github.com/rilma/pyIRI2016`). The PyHC name `IRI-2016` therefore belongs to a *different software package* and must not be applied here. There is **no** PyHC entry for `rilma/pyIRI2016`.
- Consequence: the PyHC logo `https://iri.gsfc.nasa.gov/images/red_band-179.jpg` must likewise **not** be used for Field 33 of this entry (see Field 33).

**Recommendation:** set Field 7 to **`pyIRI2016`**. Both the live HSSI value and the prior file value are demonstrably wrong for different reasons, so this is one of the few places where replacing a submitted value is strongly justified. *Presented as a decision because it replaces a submitted value.* **CONFIRMED by the user 2026-07-27 (decision 1).**

**Alternatives, if the user prefers:**
- `pyiri2016` — the exact PyPI/import spelling (loses the repository's capitalization).
- Keep `pyIRI2016: Official release of the IRI2016 wrapper in Python` — not recommended; provably a v1.1.0 release title.
- `IRI-2016` — not recommended; provably belongs to `space-physics/iri2016`.

### 8. Description (MANDATORY)
- **Proposed Description:**

  Python wrapper for the International Reference Ionosphere (IRI) 2016 model. The package computes empirical ionospheric parameters including electron density, electron temperature, ion temperature, ion densities, NmF2, hmF2, B0, and total electron content as functions of location, time, altitude, and solar/geomagnetic conditions. It supports height, latitude, longitude, local-time, and 2D profile workflows, can evaluate the model along traced geomagnetic field lines, includes helpers for retrieving IRI-related source, coefficient and index files, and provides example plotting workflows for line plots and 2D maps. The IRI-2016 Fortran source is bundled and bound to Python with f2py through a CMake / scikit-build-core build; the package requires Python 3.11 or newer.

- **Live HSSI value:** `Python wrapper for the International Reference Ionosphere (IRI) 2016 model.` (one sentence, from the 2017 Zenodo abstract)
- **Prior canonical-file value:** the same text as proposed above, minus "and total electron content", "can evaluate the model along traced geomagnetic field lines", "and index", and the final build/Python-version sentence.
- **Status:** ENRICHED. **This is not a conflict** — the proposed description begins with the live HSSI sentence *verbatim* and then adds detail. Nothing published is contradicted or removed.
- **Reason for superseding the live value:** Field 8 asks for a description "sufficiently detailed to provide the potential user with information to determine if the software is useful to their work". The single published sentence does not state what the software computes, what workflows it offers, or what it requires. The additions are each directly evidenced (see below). Editorial wording from the prior extraction is preserved verbatim; only material facts were added.
- **Evidence for the additions:** TEC — `source/iritec.for` (`IRI_TEC`) and the `h_tec_max` parameter (`pyiri2016/__init__.py` line 137). Field lines — `IRI2016_2DProf.LatVsFL()` (`iri2016prof2D.py` line 140). Index files — `settings/settings.py` `INDICES_FILES = ["apf107.dat", "ig_rz.dat"]`. Build/Python — `CMakeLists.txt` (`find_package(Python 3.11 EXACT …)`), `pyproject.toml` (`requires-python = ">=3.11"`, `build-backend = "scikit_build_core.build"`), `generate_f2py.py`.
- **Source:** `[HSSI]` `[FILE]` `[REPO]` README.md; pyproject.toml; CMakeLists.txt; pyiri2016/__init__.py; pyiri2016/iri2016prof2D.py; pyiri2016/api/update.py; settings/settings.py; source/iritec.for; examples/README.md

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Python wrapper for the International Reference Ionosphere (IRI) 2016 model.
- **Status:** UNCHANGED — keeping the live HSSI value (75 characters, within the 200-character limit).
- **Reason:** the prior canonical file used the stylistic variant `Python wrapper for the International Reference Ionosphere 2016 empirical ionospheric model.` The difference is phrasing, not fact, so the published value is preserved per the editorial-intent rule. It also now reads as the exact first sentence of the Field 8 description, which is precisely what a preview should be.
- **Documented alternative (NOT proposed):** `Python wrapper for the International Reference Ionosphere 2016 empirical ionospheric model.` `[FILE]` — slightly more informative ("empirical"). Available if the user prefers it.
- **Source:** `[HSSI]` `[FILE]` `[API]` Zenodo API record 240895 description; README.md line 10

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2017-01-12
- **Status:** UNCHANGED — live HSSI, prior file, Zenodo and DataCite all agree; re-verified.
- **Source:** `[HSSI]` `[FILE]` `[API]` Zenodo record 240895 `publication_date: "2017-01-12"`; DataCite `dates[] {dateType: "Issued", date: "2017-01-12"}`; GitHub release `v1.1.0` published `2017-01-12T15:26:14Z`; git tag `v1.1.0`
- **Note:** This is the first *published* release. The repository itself was created 2016-11-01 (GitHub `created_at`); Field 10 asks for date of first publication, so 2017-01-12 is correct.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Status:** UNCHANGED — re-verified against the Zenodo API as requested.
- **Source:** `[HSSI]` `[FILE]` `[API]` DataCite `attributes.publisher = "Zenodo"`; Zenodo API record 240895 (the record is hosted on zenodo.org); Field 11 guidance ("For software where a DOI has been obtained through Zenodo … Zenodo is the correct entry")
- **Note:** Field 11 prefers a ROR "when available … or URL otherwise". The live value `https://zenodo.org` is an acceptable URL identifier and matches the existing HSSI `Organization` row; no change proposed, to avoid gratuitous churn on a shared organization record.

### 12. Version (RECOMMENDED)

**Former live HSSI value (REPLACED 2026-07-27):** the view rendered a single string `pyIRI2016: Official release of the IRI2016 wrapper in Python - v1.1.0`. See the correction below — the stored row's `number` was a clean `v1.1.0`; the prefix was inherited from the polluted `softwareName` via `SoftwareVersion.__str__`. The row's real defects were a stale number and a wrong release date. It now renders as `pyIRI2016 - v1.2.0`.

#### Version v1.2.0 (current — proposed primary):
- **Version Number:** v1.2.0
- **Version Date:** 2026-02-21
- **Version Description:** Upgrade to Python 3.11. Adds a fallback `TimeUtilities` implementation in `pyiri2016/__init__.py` for when the `timeutil` package is unavailable, and declares `timeutil` explicitly as a git dependency; fixes `NameError: name 'TimeUtilities' is not defined`; removes obsolete Poetry-era build files, the Meson alternative build, the deprecated `.travis.yml` CI config, and build artifacts.
- **Version PID:** Not found — the v1.2.0 GitHub release was not archived to Zenodo.
- **Source:** `[REPO]` `[API]` `[FILE]` GitHub release `v1.2.0` "Upgrade to Python 3.11", published 2026-02-21T07:17:13Z; git tag `v1.2.0`; `pyproject.toml` `version = "1.2.0"`; `CHANGELOG.md` `## [1.2.0] - 2026-02-21`; `QUICKSTART.md` "What's New in v1.2.0"; SoMEF `version` = `1.2.0` (confidence 1)

#### Version v1.1.0 (archived DOI release — retained):
- **Version Number:** v1.1.0
- **Version Date:** 2017-01-12
- **Version Description:** First official release of the IRI2016 Python wrapper: `pyiri2016.IRI2016` class API, retrieval of Fortran/coefficient/index files, setuptools installation, unit test, Docker image for f2py, CHANGELOG, comprehensive README, Travis CI. Archived on Zenodo.
- **Version PID:** https://doi.org/10.5281/zenodo.240895
- **Source:** `[FILE]` `[API]` Zenodo record 240895 (`version: "v1.1.0"`); DataCite `version: "v1.1.0"`; git tag `v1.1.0`; GitHub release; `CHANGELOG.md` `## [1.1.0] - 2017-01-12`

**Release inventory (confirmed complete):** `git tag -l` returns exactly `v1.1.0` and `v1.2.0`; the GitHub releases API returns exactly two non-draft, non-prerelease entries. There are no other versions.

**APPLIED 2026-07-27 — only v1.2.0 is on HSSI.** The version row was replaced, not supplemented.

*Correction to this file's earlier rationale:* the previously recorded justification claimed the live HSSI version string `pyIRI2016: Official release of the IRI2016 wrapper in Python - v1.1.0` was itself polluted. It was not. The **stored** `SoftwareVersion` row (`00b9a7a9-…`) held a clean `number` of `v1.1.0`; the polluted string was only the *rendered* view, because `SoftwareVersion.__str__` is `f"{software} - {number}"` and therefore inherited the bad `softwareName`. Fixing Field 7 resolved the display on its own — after the patch the version renders as `pyIRI2016 - v1.2.0`. The row's genuine defects were a **stale number** (v1.1.0, two releases behind) and a **wrong release date** (`2023-04-25`, whereas the real v1.1.0 date is 2017-01-12).

**API limitation (user-accepted):** the update API's `version` key takes a single object and `software.version.set([...])` replaces the whole M2M, so a record cannot hold two versions through PATCH. The user chose the latest release. v1.1.0 is retained above as documentation only. Its DOI is **not** lost from the record — `https://doi.org/10.5281/zenodo.240895` remains published as Field 2 `persistentIdentifier`, which was deliberately omitted from the patch and is unchanged. Restoring v1.1.0 as a second version row would require the CSV / DB path. The old version row remains in the database, detached and orphaned by `.set()`.

**Unreleased work at HEAD (informational, not a version):** `CHANGELOG.md` has a substantial `## [Unreleased]` section (CMake/scikit-build-core build system, `plotting` extras, ruff/mypy/pre-commit, headless plotting, coverage CI). Much of this is already present in the v1.2.0 tree; it has not been cut as a release, so it is not listed as a version.

### 13. Programming Language (RECOMMENDED)

**Proposed value:**
- **Python 3.x**
- **Fortran77**
- **Fortran90**

**Live HSSI value:** `Fortran90`, `Java`, `Other`, `Python 3.x`, `Typescript`
**Prior canonical-file value:** `Python 3.x`, `Fortran77`

**Per-value evidence:**

| Value | Evidence | Verdict |
|---|---|---|
| Python 3.x | `pyproject.toml` `requires-python = ">=3.11"` and classifiers for 3.10/3.11/3.12; `CMakeLists.txt` `find_package(Python 3.11 EXACT …)`; CI matrix `python-version: ["3.11"]`; 16 tracked `.py` files; GitHub languages `Python: 49,541 bytes` | KEEP (in HSSI and file) |
| Fortran77 | All ten `source/*.for` files are **fixed-form** source: `c`/`C` comment markers in column 1, continuation characters in column 6 (`grep -c "^     [^ ]" source/irifun.for` → 3,525 lines), `Cf2py` directives in column 1. `gfortran` compiles `.for` as fixed form. GitHub languages `Fortran: 2,363,225 bytes` (94% of the repo). | KEEP (file-only enrichment; **add** to HSSI) |
| Fortran90 | The same fixed-form files use Fortran-90 language features: attribute declarations `real, intent(in) ::` / `real*8, intent(out) ::` / `real, external ::` (`iriflip.for` 61 occurrences, `igrf.for` 12, `iriwebg.for` 7, `irisubg.for` 4, `irisub.for` 2, `iritec.for` 1) and `end do` block terminators (108 in `irifun.for`). Live HSSI already asserts Fortran90. | KEEP (in HSSI; independently corroborated) |

**Fortran77 + Fortran90 rationale:** the source is genuinely a hybrid — F77 *fixed source form* carrying F90 *language features*. Both entries are individually true, so the set union is kept rather than choosing one and dropping the other. This resolves the HSSI-vs-file disagreement without discarding either supported value.

**PROPOSED REMOVALS (explicit — all three are currently published):**

| Removal | Justification |
|---|---|
| **`Java`** | Zero evidence anywhere. `git ls-files` extension census: `.dat` 30, `.asc` 24, `.py` 16, `.for` 10, `.png` 6, `.md` 5, `.pyf` 3, `.json` 3, `.txt` 2, plus one each of `.yml`, `.yaml`, `.toml`, `.sh`, `.gif`, `.f`, `.c`, `Makefile`, `Dockerfile`, `.gitignore`. `git rev-list --all --objects \| grep -iE '\.(java\|ts\|tsx\|jsx\|js)$'` across **all** branches returns nothing. GitHub languages API lists no Java. No JVM tooling, no build file, no import. |
| **`Typescript`** | Same evidence — no `.ts`/`.tsx` in any branch, no `package.json`, no `tsconfig.json`, no npm/node tooling. The only Node reference in the entire repo is `.devcontainer/devcontainer.json` `"NODE_VERSION": "none"` and the correspondingly disabled `.devcontainer/Dockerfile` line `RUN if [ "${NODE_VERSION}" != "none" ]; …` — i.e. Node is explicitly **turned off**. `.vscode/extensions.json` recommends only `vscode-icons-team.vscode-icons` and `ms-python.python`. |
| **`Other`** | Every language present in the repository is now identified by name. GitHub languages: Fortran, Python, C, CMake, Makefile, Dockerfile, Shell. CMake/Makefile/Dockerfile/Shell are build tooling, not "languages most important for the software", and none appears in the allowed-value list; `Other` adds no information once Python 3.x / Fortran77 / Fortran90 are present. **Alternative reading considered:** `Other` could have been retained to stand for CMake + Makefile + Shell + Dockerfile. **RESOLVED 2026-07-27 — user chose removal (decision 5).** |

**RESOLVED 2026-07-27 — should `C` be added? User decided NO (decision 4).** GitHub reports `C: 25,883 bytes`, `CMakeLists.txt` declares `project(pyiri2016 LANGUAGES C Fortran)`, and `source/iriwebmodule.c` is committed and compiled into the shipped extension. **However** its header reads `This file is auto-generated with f2py (version:2.2.6). … Do not edit this file directly` — it is machine-generated glue (as is `source/iriweb-f2pywrappers.f`), not authored source. Adding a language nobody wrote would be a mild version of the same pollution being removed here, so `C` is **not** proposed, and the user confirmed that call.

**Source:** `[REPO]` `[API]` pyproject.toml; CMakeLists.txt; generate_f2py.py; source/*.for; source/iriwebmodule.c; .github/workflows/smoke.yml; .devcontainer/*; .vscode/extensions.json; `git ls-files`; `git rev-list --all --objects`; GitHub languages API; SoMEF `programming_languages`

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication DOI:** Not found
- **Status:** UNCHANGED (both live HSSI and prior file are empty/not found).
- **Note:** Re-searched at HEAD. There is no `CITATION.cff`, no `codemeta.json`, no `.zenodo.json`, no "How to cite" section, and no JOSS/software paper. Zenodo record 240895 has no `IsDescribedBy` related identifier. The scientific DOIs embedded in the bundled IRI Fortran comments describe the underlying IRI model, not this Python wrapper, so they do not belong in Field 14. The IRI-2016 model paper is proposed under Field 27 instead (see below).
- **Source:** `[REPO]` `[API]` full repository search; Zenodo API 240895 `relatedIdentifiers`; DataCite `relatedIdentifiers`

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html
- **SPDX ID:** MIT
- **Status:** ENRICHMENT — live HSSI has **no** license recorded; this is a file-only value, re-verified at HEAD.
- **Source:** `[FILE]` `[REPO]` `[API]` `LICENSE.md` (`MIT License / Copyright (c) 2017 Ronald Ilma`, full MIT text); `pyproject.toml` `license = {text = "MIT"}` and classifier `License :: OSI Approved :: MIT License`; GitHub API `license: {key: "mit", spdx_id: "MIT"}`; README badge `License: MIT`; SoMEF `license` (confidence 1, `spdx_id: MIT`)
- **Note on a conflicting source:** Zenodo record 240895 carries `license: {id: "other-open"}`. That is stale 2017 metadata; the repository's own `LICENSE.md`, `pyproject.toml`, GitHub's license detector and SoMEF all agree on MIT. Repository evidence is preferred.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Proposed value (union; live HSSI forms preserved verbatim to avoid duplicate rows):**

*Published on HSSI — retained exactly as stored (KEEP, no case churn):*
- Atmospheric Modelling
- F2Py
- Fortran
- Ionosphere
- Ionosphere Modeling
- Python
- Standard

*File-only enrichments (re-verified against the repository):*
- electron density — `IRI()` returns `iri["ne"]`; `outf(1,*)`
- electron temperature — `iri["te"]`
- ion temperature — `iri["ti"]`
- IRI — the model acronym used throughout
- International Reference Ionosphere — README.md line 10
- empirical model — CCIR/URSI coefficient maps
- ionospheric physics — domain term

*New this run (fresh repository evidence):*
- total electron content — `source/iritec.for` (`IRIT13`, `IONCORR`, `IRI_TEC`); `h_tec_max` parameter
- NmF2 — returned in `iriadd["NmF2"]`, plotted in `iri1DExample08.py`
- hmF2 — returned in `iriadd["hmF2"]`
- IGRF — `source/igrf.for`; `data/igrf/dgrf1945…igrf2015s.dat`; optional `pyigrf` integration
- thermosphere — `source/cira.for` (NRLMSIS-00) neutral densities O, O₂, N₂, He, H, N, Ar exposed via `LatVsFL()`

*Dropped by user decision 2026-07-27 (build tooling, not science keywords — never submitted to HSSI, so this removes nothing published):*
- ~~CMake~~
- ~~scikit-build-core~~

**Note on the seven published keywords:** the prior canonical file also listed `atmospheric-modelling`, `f2py`, `fortran`, `ionosphere`, `ionosphere-modeling`, `python`, `standard` — these are the raw GitHub repository topics, i.e. lowercase/hyphenated **variants of the same seven concepts** already published in HSSI in Title Case. They have been normalised into the published forms rather than listed twice, so HSSI does not acquire duplicate keyword rows. No concept is lost.

**Note on Field 16 scope:** Field 16 asks for "general science keywords … (e.g., from the AGU Index List or the UAT)". `CMake` and `scikit-build-core` do not meet that description. They were surfaced rather than silently dropped because they appeared in the prior canonical file; the user elected to drop them on 2026-07-27. They were never published to HSSI, so this is a change to the canonical file only, not a removal from the live record.

**Final keyword count:** 7 published (retained verbatim) + 12 enrichments = **19 values**.

**Source:** `[HSSI]` `[FILE]` `[REPO]` `[API]` GitHub repository topics (`atmospheric-modelling, f2py, fortran, ionosphere, ionosphere-modeling, python, standard`, also returned by SoMEF `keywords` at confidence 1); README.md; pyproject.toml; source/iritec.for; source/igrf.for; source/cira.for; CHANGELOG.md

### 17. Data Sources (OPTIONAL)
- **HTTP/HTTPS Directories**
- **Other** — bundled IRI coefficient and index files shipped inside the package

**Status:** ENRICHMENT — live HSSI has no data sources recorded; both values are file-only and were re-verified at HEAD.

**Evidence:** `settings/settings.py` defines three HTTPS endpoints — `FORTRAN_CODE_URL = "https://irimodel.org/IRI-2016"` (`00_iri.tar`), `COMMON_FILES_URL = "https://irimodel.org/COMMON_FILES"` (`00_ccir-ursi.tar`), `INDICES_URL = "https://chain-new.chain-project.net/echaim_downloads"` (`apf107.dat`, `ig_rz.dat`). `pyiri2016/api/update.py` `retrieve()` fetches them with `wget.download` and safely extracts tarballs; exercised by `tests/test_api.py`. The package additionally ships 54 data files locally (`data/ccir` 12, `data/ursi` 12, `data/mcsat` 12, `data/igrf` 16, `data/index` 2 — confirmed by `find data -type f | wc -l` → 54, installed to `pyiri2016/data/…` by `CMakeLists.txt`) which the Fortran reads via the `dirdata` argument — hence `Other`.

**Considered and excluded:** `Observatory/Mission-specific` — the `chain-new.chain-project.net` host (Canadian High Arctic Ionospheric Network) is used **only** as a mirror for the generic IRI solar/magnetic index files `apf107.dat` and `ig_rz.dat`. The software does not read any CHAIN instrument data, so this is a plain HTTPS directory, not observatory-specific access (see also Fields 31/32).

**Source:** `[FILE]` `[REPO]` settings/settings.py; pyiri2016/api/update.py; tests/test_api.py; CMakeLists.txt; data/*

### 18. Input File Formats (RECOMMENDED)
- **ascii**

**Status:** ENRICHMENT — live HSSI has no input formats recorded.

**Evidence:** all bundled model inputs are plain-text: `data/ccir/ccir11-22.asc` and `data/ursi/ursi11-22.asc` (CCIR/URSI foF2 and M(3000)F2 coefficient maps), `data/igrf/dgrf1945-2010.dat` + `igrf2015.dat` + `igrf2015s.dat` (IGRF/DGRF spherical-harmonic coefficients), `data/index/apf107.dat` and `ig_rz.dat` (magnetic and solar indices), `data/mcsat/mcsat11-22.dat`. They are read by the Fortran through the `dirdata` path argument (`read_ig_rz`, `readapf107`, `GETSHC` in `igrf.for`).

**Considered and excluded:** `Other` for the `.tar` archives retrieved by `api/update.py` — tar is a transport container around the same ascii files, not a science data format.

**Source:** `[FILE]` `[REPO]` data/ccir; data/igrf; data/index; data/mcsat; data/ursi; source/irifun.for; source/igrf.for; settings/settings.py

### 19. Output File Formats (RECOMMENDED)
- **Other** — PNG raster figures produced by the plotting and example workflows

**Status:** ENRICHMENT — live HSSI has no output formats recorded.

**Evidence:** the core model API returns Python dictionaries and NumPy arrays in memory rather than writing science-data files (`IRI2016.IRI()` returns `iri, iriadd`; `IRI2016Profile` exposes `self.a`, `self.b`). The only files the package writes are PNG figures: `iri2016prof2D.py` `Plot2D()`, `PlotFIRI2D()`, `PlotLatVsFL()`, `PlotLatVsFLFIRI()`, `Plot2DMUF()` all call `savefig(str(filepath), dpi=100, bbox_inches="tight")` into `figures/` with UUID-suffixed names; `examples/iri1DExample01.py`, `iri1DExample01b.py`, `iri1DExample02.py`, `iri1DExample08.py` do the same.

**Considered and excluded:** `ascii` — the `verbose=True` paths in `HeiProfile()`, `LatProfile()`, `LonProfile()`, `HrProfile()` print formatted tables to **stdout**, not to a file. `source/iritest.for` writes text output but is not part of the f2py interface (`generate_f2py.py` exposes only `iriwebg`, `irisubgl`, `firisubl`).

**Source:** `[FILE]` `[REPO]` pyiri2016/iri2016prof2D.py; examples/*.py; scripts/*.py; generate_f2py.py

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**

**Status:** ENRICHMENT — live HSSI has no operating system recorded.

**Rationale:** pure-Python front end (3.11+) over a Fortran extension built with CMake ≥3.15 + scikit-build-core, a deliberately cross-platform toolchain. README.md: "modern CMake-based build system with scikit-build-core for **cross-platform** compilation"; QUICKSTART.md: "CMake 3.15+ for cross-platform compilation" and "Reproducible across platforms". Requirements are only Python 3.11, NumPy ≥2.0, CMake, Ninja and a Fortran compiler (gfortran) — all available on Linux, macOS and Windows. No OS-specific code paths, no platform-conditional dependencies in `pyproject.toml`.

**Caveat recorded for the validator:** CI verifies **Linux only** (`.github/workflows/smoke.yml` — all three jobs `runs-on: ubuntu-latest`, installing `gfortran cmake ninja-build` via `apt-get`), and the devcontainer is Debian bullseye. macOS and Windows are claimed by the documentation but not tested. If the user prefers evidence-only, `Linux` alone would be the conservative choice; `Operating System Independent` is kept as the prior file's assessment and matches the project's own stated intent.

**Source:** `[FILE]` `[REPO]` README.md; QUICKSTART.md; pyproject.toml; CMakeLists.txt; Makefile; .github/workflows/smoke.yml; .devcontainer/Dockerfile

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Status:** ENRICHMENT — live HSSI has no CPU architecture recorded.

**Rationale:** Python + NumPy + compiled Fortran/C extension code with no SIMD intrinsics, no assembly, no GPU code, no MPI, and no architecture-conditional build logic. `CMakeLists.txt` sets only `target_compile_options(iriweb PRIVATE -w)` (warning suppression) and `cmake.build-type = "Release"`; nothing pins an ISA. Builds wherever gfortran and CPython exist. `.devcontainer/devcontainer.json` explicitly notes, on its `VARIANT` build argument, "Use -bullseye variants on local on arm64/Apple Silicon", indicating arm64 is anticipated.

**Source:** `[FILE]` `[REPO]` pyproject.toml; CMakeLists.txt; .devcontainer/devcontainer.json; .devcontainer/Dockerfile; repository source files

### 22. Related Phenomena (OPTIONAL)
- **Geomagnetic Storms**

**Status:** CHANGED 2026-08-24 (was empty; live HSSI was empty before this addition — ENRICHMENT to HSSI).

**Note:** an earlier version of this note called the controlled vocabulary "entirely solar" and enumerated a stale six-value documentation list (which included a `Coronal Holes` phantom that has never been a row, and omitted the vocabulary's two geospace rows, `Geomagnetic Storms` and `Solar Wind`). That description was wrong: the vocabulary is not entirely solar, and `Geomagnetic Storms` applies directly to this terrestrial ionospheric model.

**USER DECISION 2026-08-24 — `Geomagnetic Storms` (a controlled row) ADDED.** The reachability audit below had already established the science: the foF2 and foE ionospheric-storm models (`jf[26-1]`, `jf[35-1]`) are both switched on, and ionospheric storms are the ionospheric signature of geomagnetic storms. The value was previously excluded only because the stale documentation list hid the row. This is consistent with, not a reversal of, the 2026-07-27 decision below: that decision declined free-text terms and directed "stick to the HSSI controlled vocabulary" — which is exactly what selecting this controlled row does.

**USER DECISION 2026-07-27 — custom terms considered and DECLINED. Stick to the HSSI controlled vocabulary.** No custom free-text phenomena will be added. The candidate analysis below is retained purely as an audit trail so a future extraction does not silently rediscover and re-propose these terms as free text; "equatorial F-region vertical drift" still has no controlled row and stays out.

**Candidate custom terms (the field does allow custom entries) — DECLINED, not proposed.** Only phenomena that this wrapper actually computes were considered, following a reachability audit of `pyiri2016/__init__.py` `Switches()`:

*Genuinely active and user-visible:*
- **ionospheric storms** — `jf[26-1]` (foF2 storm model) and `jf[35-1]` (foE storm model), both switched **on** in the `year >= 1958` branch at `__init__.py` lines 124-125.
- **equatorial F-region vertical drift** — `jf[21-1]` "ion drift computed", enabled by default and surfaced to the user as `V_y` in `examples/iri1DExample08.py`.

*Latent model capability, NOT computed by this wrapper (do not list):*
- **spread F** — `jf[28-1]` is hardcoded to `0` at `__init__.py` line 67.
- **auroral boundary** — `jf[33-1]` is hardcoded to `0` at `__init__.py` line 73.

Neither `IRI2016.IRI()`, `IRI2016Profile.__init__`, nor any path in `iri2016prof2D.py` exposes a mechanism to override an individual `jf` switch — the only conditional block (`IRI()` lines 114-126) touches solely `jf[17,25,26,27,32,35]`. So spread F and auroral boundary describe dormant Fortran capability, not behaviour of this package, and were dropped from the candidate list on evidence grounds before the user decision was taken.

Injecting custom free-text terms into a controlled vocabulary is a curation decision, and the user declined it: neither remaining live candidate (ionospheric storms, equatorial vertical drift) is submitted **as free text**. The ionospheric-storm science is instead represented by the controlled row `Geomagnetic Storms` (added 2026-08-24, above); equatorial vertical drift has no controlled row and remains unrepresented.

**Source:** `[FILE]` `[REPO]` pyiri2016/__init__.py `Switches()`; examples/iri1DExample08.py

### 23. Development Status (RECOMMENDED)
- **Active**

**Status:** UNCHANGED value, re-derived at HEAD (live HSSI has no development status — this is an ENRICHMENT to HSSI).

**Rationale (re-derived 2026-07-26):** the project has reached a stable, usable state and is still being developed. Evidence: stable release `v1.2.0` published 2026-02-21; `pyproject.toml` classifier `Development Status :: 5 - Production/Stable`; a modern maintained toolchain (CMake + scikit-build-core, NumPy ≥2.0, ruff, mypy, pre-commit, pytest+coverage, Codecov) added recently; a three-job GitHub Actions CI pipeline; a substantial `## [Unreleased]` section in `CHANGELOG.md` showing work in progress; repository not archived, not disabled; 3 open issues.

**Datapoint recorded for transparency:** last code push was 2026-02-21 (GitHub `pushed_at`), i.e. ~5 months before this extraction; `updated_at` is 2026-07-07 (metadata-level activity). This is still comfortably within "Active" under repostatus.org, but if the user applies a stricter recency bar, `Inactive` would be the alternative. `Active` is retained.

**Source:** `[FILE]` `[REPO]` `[API]` GitHub release v1.2.0; git tag v1.2.0; GitHub repository metadata (`archived: false`, `pushed_at`, `open_issues_count`); CHANGELOG.md; pyproject.toml; .github/workflows/smoke.yml

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/rilma/pyIRI2016

**Status:** UNCHANGED value, re-verified (live HSSI has no documentation URL — ENRICHMENT to HSSI).

**Note:** there is no separate documentation site. GitHub API reports `has_pages: false` and an empty `homepage`; there is no `docs/` directory, no `.readthedocs.yml`, and no Sphinx/MkDocs configuration. Documentation lives in the repository: `README.md` (install, quick start, test targets, example gallery, build-system reference), `QUICKSTART.md` (detailed build/test/troubleshooting guide), `examples/README.md` (how to run the 1D and 2D examples), and `CHANGELOG.md`. The repository root URL is therefore the correct single entry point, per Field 24's "If this is the same as the access URL, then enter that link here."

**Considered:** `https://github.com/rilma/pyIRI2016/blob/main/QUICKSTART.md` is the most detailed installation document, but it is reachable from the README and is narrower than the field's intent. The GitHub wiki (`has_wiki: true`, `/wiki` returns HTTP 200 via redirect) has no substantive content and was not used.

**Source:** `[FILE]` `[REPO]` `[API]` README.md; QUICKSTART.md; examples/README.md; GitHub API repository metadata

### 25. Funder (OPTIONAL)
- **Not found**
- **Status:** UNCHANGED
- **Note:** re-searched at HEAD. Zenodo record 240895 and DataCite both have empty `fundingReferences`. No acknowledgement, funding statement, grant number or sponsor appears in README.md, QUICKSTART.md, CHANGELOG.md, LICENSE.md, `pyproject.toml`, or the bundled Fortran headers (which credit model authors, not funders). The author's Cornell University affiliation is an affiliation (Field 6), not a funder.
- **Source:** `[FILE]` `[REPO]` `[API]` Zenodo API record 240895; DataCite; full repository search

### 26. Award Title (OPTIONAL)
- **Not found**
- **Status:** UNCHANGED
- **Source:** `[FILE]` `[REPO]` `[API]` Zenodo API record 240895 (`fundingReferences` empty); full repository search

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- **Not found**

**Status:** UNCHANGED (live HSSI empty; prior canonical file "Not found"). No change proposed to HSSI.

**USER DECISION 2026-07-27 — candidate publication considered and DECLINED.** The extraction initially proposed Bilitza, D., Altadill, D., Truhlik, V., Shubin, V., Galkin, I., Reinisch, B., & Huang, X. (2017), *International Reference Ionosphere 2016: From ionospheric climate to real-time weather predictions*, Space Weather, 15(2), 418-429, `https://doi.org/10.1002/2016SW001593`. The DOI is genuine (resolved via the Crossref API 2026-07-26 — *Space Weather*, issued 2017-02; note `10.1002/2017SW001593` is **not** valid, the correct year segment is 2016).

**Why it was declined:** two reservations, both decisive.
1. *Not cited in the repository.* The citation appears nowhere in the repo; it was inferred from the software's subject and its `irimodel.org` links.
2. *Fits neither field's definition.* Field 27 wants publications that "describe, cite, or use the software". This paper describes the underlying IRI-2016 **model**, not `rilma/pyIRI2016`, and neither cites nor uses this repository — its 2017-02 publication essentially coincides with, rather than follows, the wrapper's 2017-01-12 v1.1.0 release. Field 14 was ruled out on exactly the same reasoning, so the paper satisfies the literal definition of *neither* field.

Recording an inferred, uncited citation would assert a relationship the evidence does not support, so Field 27 remains empty. Retained here as an audit trail so the candidate is not silently rediscovered and re-proposed by a future extraction.

**Source:** `[FILE]` `[REPO]` `[API]` full repository search; README.md; settings/settings.py; Crossref API

### 28. Related Datasets (OPTIONAL)
- **Not found**
- **Status:** UNCHANGED
- **Note:** the package ships genuine datasets (CCIR and URSI ionospheric coefficient maps, IGRF/DGRF 1945-2015 spherical-harmonic coefficients, `apf107.dat` / `ig_rz.dat` solar and magnetic indices, `mcsat*.dat`), but none of them has a DOI or an APA-citable dataset landing page. They are distributed as bare files from `irimodel.org` and `chain-new.chain-project.net`. Recorded under Field 17 (Data Sources) and Field 18 (Input File Formats) instead.
- **Source:** `[FILE]` `[REPO]` `[API]` data/*; settings/settings.py; Zenodo API record 240895 `relatedIdentifiers`

### 29. Related Software (OPTIONAL)

#### Related Software 1: Time Utilities (`timeutil`)
- **URL:** https://github.com/rilma/TimeUtilities
- **Relationship:** Companion package by the same author; required runtime dependency.
- **Specific evidence:** README.md line 21 — "This also installs [Time Utilities](https://github.com/rilma/TimeUtilities)"; `pyproject.toml` dependency `timeutil @ git+https://github.com/rilma/TimeUtilities.git`; `pyiri2016/__init__.py` lines 8-21 import `TimeUtilities` and ship a **fallback re-implementation** of `ToHMS()` for when it is unavailable; `iri2016prof2D.py` lines 40-44 and line 179 (`TimeUtilities().CalcDOY(...)`).
- **Status:** UNCHANGED (`[FILE]`).
- **Note on the relevance gate — USER DECISION 2026-07-27: KEEP.** This was a genuine judgment call and the user resolved it in favour of retaining the entry. *For inclusion:* Field 29 explicitly welcomes companion packages; this one is by the same author, is named outright in the README, is declared as a git dependency, and is important enough that pyIRI2016 ships a vendored fallback re-implementation of it. *Against inclusion:* the functions actually exchanged are `ToHMS()` (decimal hours → H:M:S) and `CalcDOY()` (day-of-year) — plain calendar arithmetic with no heliophysics-domain content. Applied honestly, the Fields 29/30 gate question ("would this be equally at home in a web app, a finance model, or a biology pipeline?") answers *yes*, which is the same reasoning used to exclude the Tier A infrastructure list below. *Resolution:* the user weighed both readings and elected to keep the entry, on the strength of the companion-package relationship (same author, README-named, declared dependency, vendored fallback) rather than the nature of the functions exchanged. The tension is recorded here rather than resolved silently.

#### Related Software 2: IRI-2016 (space-physics / iri2016)
- **Submitted identifier:** https://doi.org/10.5281/zenodo.591802 — **this is the value on HSSI**
- **Same package, alternate identifier (deliberately NOT submitted):** https://github.com/space-physics/iri2016
- **Relationship:** Independent Python (and MATLAB) wrapper for the same IRI-2016 model — *performs similar tasks* — and a **descendant of this repository**.
- **Specific evidence:** the DOI `10.5281/zenodo.591802` is the Zenodo **concept DOI** for `scivision/pyIRI2016` (DataCite title "scivision/pyIRI2016 v1.2.1_1"; abstract "International Reference Ionosphere 2016 for Python"; creators "Ronald, I." and "Michael Hirsch, Ph.D." / SciVision, Inc.; `IsSupplementTo https://github.com/scivision/pyIRI2016/tree/v1.2.1_1`; latest version record 556843). `scivision/pyIRI2016` no longer exists under that name — `https://api.github.com/repos/scivision/pyIRI2016` returns **HTTP 301** (`Location: .../repositories/123071113`), a rename redirect, not a 404 — and the line continues as `space-physics/iri2016` ("International Reference Ionosphere 2016 from Python and Matlab"), which is the package PyHC registers under the name `IRI-2016` in `projects_unevaluated.yml`. Michael Hirsch (`scivision`) is a major contributor to *this* repository with 29 commits (25.0% and second overall by GitHub's deduplicated contributor stats; 17.2% by raw `git shortlog`), confirming the shared lineage.
- **Status:** the DOI is **RELOCATED from live HSSI Field 30** to Field 29 (see the removal note below); the repository URL is `[FILE]`.
- **USER DECISION 2026-07-27 — DOI only, GitHub URL not submitted.** `relatedSoftware` is a flat list of URLs, so the two identifiers for this one package cannot be merged into a single row; submitting both would list the same software twice. The user chose the DOI as the more durable identifier: it is persistent, it already survived the `scivision` → `space-physics` rename that broke the GitHub URL, and it is the value already published on HSSI (so keeping it preserves existing data rather than dropping it).
- **Display note:** the DOI's RelatedItem row (`55ad8364-…`) has `name = "UNKNOWN"` in the database and the API cannot rename it. This does **not** affect users — `RelatedItem.to_user_str()` returns the identifier and `RelatedItem.__str__()` falls back to the identifier when the name is `UNKNOWN`. Verified on the rendered page: 0 occurrences of `UNKNOWN`, 3 of the DOI. Raised and closed as hssi-website#58; ~294 of 295 RelatedItem rows share this placeholder-name condition, so it is systemic and cosmetic, not specific to this entry.

#### Related Software 3: IRI-2016 Fortran model (upstream)
- **URL:** https://irimodel.org/
- **Relationship:** The upstream Fortran model that this package wraps and redistributes.
- **Specific evidence:** README.md line 10 links `http://irimodel.org/`; `settings/settings.py` `FORTRAN_CODE_URL = "https://irimodel.org/IRI-2016"` with `00_iri.tar`, and `COMMON_FILES_URL = "https://irimodel.org/COMMON_FILES"` with `00_ccir-ursi.tar`; `pyiri2016/api/update.py` `retrieve()` downloads and extracts them; the ten `source/*.for` files are that distribution verbatim, including their original version headers.
- **Status:** **NEW** this run. Per Field 29's "If no public repository, enter link where users can find more information", `https://irimodel.org/` is the canonical distribution page (verified HTTP 200 on 2026-07-26; the site returns 406 to unbranded user agents but serves normally to browsers).
- **Note:** this is arguably the single most distinguishing related-software entry for this package.

**PROPOSED REMOVAL from Field 30 → RELOCATION to Field 29 (explicit; this is a published value):**
`https://doi.org/10.5281/zenodo.591802` is currently HSSI's only `interoperableSoftware` value. Resolved this run: it is the Zenodo concept DOI of `scivision/pyIRI2016` — a **fork/derivative** of this repository, now `space-physics/iri2016`. There is no adapter, converter, shared data model, plugin relationship or documented exchange between `rilma/pyIRI2016` and that package; they are two independent wrappers of the same Fortran model and would in fact compete for the same import namespace. It therefore **fails the Field 30 gate** but is a textbook **Field 29** entry ("software that performs similar tasks", "software this work was forked from" / forked into). **The value is preserved, not discarded** — it moves fields.

**Considered and EXCLUDED from both Field 29 and Field 30 (Tier A generic infrastructure — audit trail):**
`numpy`, `scipy`, `matplotlib`, `seaborn`, `basemap` / `basemap-data` (mapping — the peer of the explicitly Tier-A `cartopy`), `beautifulsoup4`, `wget`, `simple-settings`, `pytest`, `pytest-cov`, `coverage`, `parameterized`, `pre-commit`, `ruff`, `mypy`, `cmake`, `ninja`, `scikit-build-core`, `setuptools`. Each fails the "would this be equally at home in a web app, a finance model, or a biology pipeline?" test; listing any of them would say nothing specific about pyIRI2016.

**Source:** `[FILE]` `[HSSI]` `[REPO]` `[API]` README.md; pyproject.toml; pyiri2016/__init__.py; pyiri2016/iri2016prof2D.py; settings/settings.py; DataCite `10.5281/zenodo.591802`; Zenodo record 556843; GitHub API; PyHC `projects_unevaluated.yml`

### 30. Interoperable Software (OPTIONAL)

#### Interoperable Software 1: pyApex
- **URL:** https://github.com/rilma/pyApex
- **Relationship:** Demonstrated data exchange — pyApex's traced field-line geometry is consumed directly by pyIRI2016.
- **Specific evidence (not a dependency claim):** `pyiri2016/iri2016prof2D.py` `LatVsFL()` calls `gc, qc = pyapex.ApexFL().getFL(date=date2, dlon=dlon, dlat=dlat, hateq=h, mlatRange=mlatlim, mlatSTP=mlatstp)` at line 189, then feeds the returned geographic coordinate arrays into IRI via `irisubgl(jf, jmag, year, mmdd, hour2, curr_coordl[ind[0], :], DataFolder)` at line 233, and surfaces pyApex's quasi-dipole coordinates to the user as `self.qdcoordl` (line 200). The import is guarded (`try: import pyapex / except ModuleNotFoundError: pyapex = None`, lines 26-29) with an explicit `ImportError("pyapex is required for LatVsFL(). Install it with: pip install pyapex")` at line 153 — an optional, deliberate integration rather than a hard dependency. API match verified upstream: `class ApexFL` at `pyapex/__init__.py` line 37 and `def getFL(...)` at line 47 in `rilma/pyApex`.
- **Status:** **NEW** this run.
- **Install caveat for the user:** the CHANGELOG and the runtime error message both say `pip install pyapex`, but the PyPI project named `pyapex` is an unrelated package ("Create interactive html charts", `nicodemus-opon/pyapex`). The correct package is `https://github.com/rilma/pyApex`, which is what the code's API actually matches. Recording the repository URL avoids propagating that ambiguity.

#### Interoperable Software 2: pyIGRF
- **URL:** https://github.com/rilma/pyIGRF
- **Relationship:** Demonstrated data exchange — pyIGRF's IGRF field output is substituted into pyIRI2016's own output arrays.
- **Specific evidence:** `pyiri2016/iri2016prof2D.py` `getIGRF()` calls `bn, be, bd, xl, icode = GetIGRF(lat, lon, alt, year)` at line 294 and yields the derived horizontal component `bh`; `LatVsFL()` line 256-258 then writes that result into `self.babs` **in place of** the model's internal `outf[19, :]` when `IGRF=True`. Import guarded at lines 31-34 (`from pyigrf.pyigrf import GetIGRF`) with `ImportError("pyigrf is required for IGRF calculations. …")` at line 289. API match verified upstream: `def GetIGRF(xlat=-11.95, xlon=283.13, height=0., year=2004.75)` at `pyigrf/pyigrf.py` line 8 in `rilma/pyIGRF` — signature and argument order match the call site exactly.
- **Status:** **NEW** this run.
- **Install caveat:** the PyPI project `pyigrf` is `zzyztyy/pyIGRF` (IGRF-14), a different package whose API does not match this call. The repository URL is recorded for that reason.

**PROPOSED REMOVAL (explicit — currently the only published value in this field):** `https://doi.org/10.5281/zenodo.591802`. Resolved, relocated to Field 29, justification in full under Field 29 above. **Not discarded.**

**Considered and EXCLUDED:** the entire Tier A list under Field 29 applies here unchanged. Also excluded: `timeutil`/TimeUtilities — although imported, the exchange is one-way consumption of a generic `ToHMS`/`CalcDOY` helper (and pyIRI2016 ships a fallback re-implementation of it), which is dependency use, not peer-tool interoperation; it is recorded in Field 29 as a companion package instead. No blanket "part of the scientific Python ecosystem" claim is made anywhere in this field.

**Source:** `[REPO]` `[API]` pyiri2016/iri2016prof2D.py lines 26-44, 140-264, 286-299; CHANGELOG.md `[Unreleased] > Changed`; `rilma/pyApex` `pyapex/__init__.py`; `rilma/pyIGRF` `pyigrf/pyigrf.py`; GitHub API; PyPI API

### 31. Related Instruments (OPTIONAL)
- **Not found**
- **Status:** UNCHANGED (live HSSI empty; prior file "Not found").

**Relevance-gate reasoning:** pyIRI2016 is an **instrument-agnostic** global empirical model. It reads no instrument's data products, implements no instrument-specific format or convention, is not an instrument-team tool, and does not calibrate or process any instrument's measurements. A user searching HSSI for a specific instrument would not expect this package back. No SPASE vocabulary resolution was required because nothing passes the gate.

**Considered and EXCLUDED (audit trail):**
- `AEROS`, `ISIS`, `AE-C`, `AE-E`, `Atmosphere Explorer`, `Jicamarca`, `Arecibo`, `digisonde`/`ionosonde`, `COSMIC`, `MGS` — these appear **only inside the bundled IRI Fortran comment headers** (`source/*.for`), documenting the historical measurement campaigns from which the IRI empirical coefficients were *derived decades ago*. The software neither reads nor supports data from any of them. The single Python-side mention, `pyiri2016/__init__.py` line 62 (`jf[23-1] = 0  #  23  Te_tops (Aeros,ISIS)  Te_topside (TBT-2011)`), is a switch label for which statistical topside-Te parameterisation to use — a model option, not instrument support.
- **CCIR / URSI coefficient maps** — derived from a global ionosonde network, but distributed as generic coefficient files with no instrument identity; recorded under Fields 17/18 instead.

**Source:** `[FILE]` `[REPO]` source/*.for; pyiri2016/__init__.py; full repository grep for instrument names

### 32. Related Observatories (OPTIONAL)
- **Not found**
- **Status:** UNCHANGED (live HSSI empty; prior file "Not found").

**Relevance-gate reasoning:** the software is **observatory/mission-agnostic**. It is a global climatological model valid at any geographic location; it supports no mission's data conventions and is not a mission-team tool.

**Considered and EXCLUDED (audit trail):**
- **CHAIN (Canadian High Arctic Ionospheric Network)** — `settings/settings.py` `INDICES_URL = "https://chain-new.chain-project.net/echaim_downloads"`. This host is used purely as a **mirror for the generic IRI index files** `apf107.dat` (magnetic indices) and `ig_rz.dat` (solar indices). No CHAIN instrument or observatory data is read. Per the Field 32 guidance this is a generic data source → recorded under Field 17 as `HTTP/HTTPS Directories`, and `Observatory/Mission-specific` was deliberately **not** selected there.
- **irimodel.org** — the model distribution site, not an observatory. Recorded under Fields 17 and 29.
- The historical missions named in the bundled Fortran headers (AEROS, ISIS, Atmosphere Explorer) — excluded for the same reason as Field 31.

**Source:** `[FILE]` `[REPO]` settings/settings.py; pyiri2016/api/update.py; source/*.for

### 33. Logo (OPTIONAL)
- **Not found**
- **Status:** UNCHANGED
- **Note:** no logo asset or logo URL exists in the repository. SoMEF returned no `logo` key. GitHub reports no social-preview/homepage asset.
- **IMPORTANT — do NOT use `https://iri.gsfc.nasa.gov/images/red_band-179.jpg`.** That logo belongs to the PyHC `IRI-2016` entry, whose `code` field is `https://github.com/space-physics/iri2016` — a **different package** (see Field 7). Applying it here would compound the same mis-attribution that produced the prior file's incorrect software name.
- **Also not a logo:** `figures/iri2DExample02.gif`, displayed as a banner at README.md line 8, is an example model-output animation, not a project logo.
- **Source:** `[FILE]` `[REPO]` `[API]` repository examination; SoMEF output; PyHC `projects_unevaluated.yml`

---

## Metadata Quality Notes

### Summary of changes APPLIED to the live HSSI record (2026-07-27)

All changes below were approved by the user and applied in a single PATCH (HTTP 200, 16 fields), then roundtrip-verified. Fields omitted from the patch were confirmed unchanged.

**Replacements of published values (each requires user approval):**
1. **Field 7 Software Name** — `pyIRI2016: Official release of the IRI2016 wrapper in Python` → `pyIRI2016`. Release-title pollution, confirmed against the GitHub releases API and Zenodo/DataCite titles.
2. **Field 12 Version** — `pyIRI2016: Official release of the IRI2016 wrapper in Python - v1.1.0` → structured `v1.2.0` (2026-02-21) + `v1.1.0` (2017-01-12, DOI `10.5281/zenodo.240895`). Same pollution, plus two releases stale.
3. **Field 8 Description** — one sentence → expanded (strictly additive; begins with the published sentence verbatim).

**Proposed removals (each requires user approval):**
1. **Field 13** — `Java` (zero evidence in any branch).
2. **Field 13** — `Typescript` (zero evidence in any branch; Node explicitly disabled in the devcontainer).
3. **Field 13** — `Other` (every present language is now named; alternative reading offered).
4. **Field 30** — `https://doi.org/10.5281/zenodo.591802` — **relocated to Field 29**, not discarded.

**Enrichments (fields currently empty on HSSI):** Software Functionality (+11 values), License, Keywords (+12), Data Sources, Input File Formats, Output File Formats, Operating System, CPU Architecture, Development Status, Documentation, Related Software (3 entries), Interoperable Software (2 entries), Version date/description/PID.

**Deliberately left empty (user decision 2026-07-27):** Related Publications (the inferred Bilitza et al. 2017 model paper was declined as uncited and definitionally ill-fitting). Related Phenomena was also left empty at that decision, but only because a stale documentation list hid the vocabulary's geospace rows; the controlled row `Geomagnetic Storms` was added 2026-08-24 (see Field 22) — the ban on custom free-text terms stands.

**Confirmed unchanged:** Persistent Identifier, Code Repository, Related Region, Author (name reverted to the live HSSI form), Author affiliation, Concise Description, Publication Date, Publisher.

### User decisions — all resolved 2026-07-27

No open questions remain. All twelve were put to the user and answered.

| # | Field | Question | Decision |
|---|---|---|---|
| 1 | 7 | `pyIRI2016` over the polluted HSSI value and the mis-attributed `IRI-2016`? | **`pyIRI2016`** — both prior values disproven |
| 2 | 6 | Add Michael Hirsch (`scivision`, 29 commits) as a second author? | **No** — no source credits him as an author of *this* repository; commit history alone is too weak a basis |
| 3 | 6 | `Ronald Ilma` or `Ronald R. Ilma Campana`? | **`Ronald Ilma`** — live HSSI, Zenodo/DataCite and LICENSE.md agree; only `pyproject.toml` differs (with a placeholder email). The HSSI API also silently no-ops Person renames |
| 4 | 13 | Add `C` for the auto-generated `source/iriwebmodule.c`? | **No** — f2py-generated glue, header reads "Do not edit this file directly" |
| 5 | 13 | Retain `Other` for build tooling? | **Remove** — every language actually present is now named |
| 6 | 16 | Drop `CMake` / `scikit-build-core` keywords? | **Drop** — build tooling, not science keywords; never published to HSSI |
| 7 | 20 | `Operating System Independent` or `Linux` only? | **Operating System Independent** — documented cross-platform design intent; Linux-only CI recorded as a caveat |
| 8 | 22 | Add custom phenomena terms? | **No — stick to the HSSI controlled vocabulary.** Free-text terms declined; see Field 22 for the declined candidates. (Field 22 was empty at this decision only because a stale documentation list hid the geospace rows; the controlled row `Geomagnetic Storms` was added by user decision 2026-08-24 — consistent with this ruling, not a reversal) |
| 9 | 27 | Confirm the inferred Bilitza et al. (2017) IRI-2016 paper? | **No — do not include.** Uncited in the repo and fits neither Field 14's nor Field 27's definition; Field 27 stays empty |
| 10 | 9 | Keep the published concise description? | **Keep** — it is exactly the first sentence of Field 8, which is what a preview should be |
| 11 | 29 | Keep `TimeUtilities`? | **Keep** — companion package by the same author, README-named, declared dependency, vendored fallback |
| 12 | 5 | Add `Earth Magnetosphere` alongside `Earth Atmosphere`? | **No** — field lines are traced, but every output quantity is ionospheric/thermospheric |

### Naming history (corrects the prior file's note)
The prior canonical file recorded "Official HSSI Software Name: IRI-2016 … Field 7 intentionally uses the PyHC/HSSI software-sheet name." **That note is retracted.** A full read of all three PyHC registry YAML files on 2026-07-26 shows the only `IRI-2016` entry has `code: https://github.com/space-physics/iri2016` — a different repository from this HSSI entry. There is no PyHC entry for `rilma/pyIRI2016`. The repository's own name is `pyIRI2016`.

### Verification status
- **Live HSSI:** `GET http://localhost/api/view/software/a53ebbd1-0f08-4bf6-aeaa-90067a3b1312/` fetched twice, byte-identical; affiliation organization `bf476440-…` resolved via `/api/models/Organization/rows/all/`
- **Zenodo API:** record 240895 verified (DOI, title, publication date, creator, license, no concept DOI); record 556843/591802 resolved for the Field 30 investigation
- **DataCite API:** `10.5281/zenodo.240895` and `10.5281/zenodo.591802` verified
- **GitHub API:** repository metadata, languages (Fortran/Python/C/CMake/Makefile/Dockerfile/Shell — **no Java, no TypeScript**), releases (exactly v1.1.0 and v1.2.0), topics, contributors
- **SoMEF:** run at `-t 0.7` against `https://github.com/rilma/pyIRI2016` — corroborates name `pyIRI2016` (two techniques, confidence 1), version 1.2.0, MIT license, keywords, languages
- **PyHC registries:** all three YAML files read in full — no entry for `rilma/pyIRI2016`; the `IRI-2016` entry belongs to `space-physics/iri2016`
- **ROR API:** Cornell University → `https://ror.org/05bnh6r87` confirmed
- **ORCID API:** no record found for Ronald Ilma / Ilma Campana
- **Crossref API:** IRI-2016 model paper DOI corrected to `10.1002/2016SW001593`
- **Repository:** examined at commit `1a47c6018aae8be93349fb2487c1911e95c1f99f` (`main`) — public API, Fortran sources and f2py interface, build system, data files, examples, scripts, tests, CI, devcontainer; `git rev-list --all` searched for Java/TypeScript artifacts across every branch

### Completeness assessment
- **MANDATORY fields:** all populated (Submitter is the expected placeholder)
- **RECOMMENDED fields:** all populated except Reference Publication (genuinely absent — no software paper) and the v1.2.0 Version PID (genuinely absent — not archived to Zenodo)
- **OPTIONAL fields:** populated wherever evidence exists; Related Phenomena carries `Geomagnetic Storms` (added 2026-08-24); Related Datasets, Funder, Award Title, Related Instruments, Related Observatories and Logo are `Not found` with documented reasoning

---

**End of Metadata Extraction**
