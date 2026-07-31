# HSSI Metadata Extraction Results

**HSSI Software ID:** fa126d2b-ea85-4237-8abd-367c1b1e4e92
**Repository:** https://github.com/SWxTREC/enlilviz
**Source Revision:** 842da22c011d4c0e4deafc6524810646ed4dcf97
**Extraction Date:** 2026-07-30
**Validation Date:** 2026-07-31
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source: Not stored on the HSSI record; supplied at submission/update time.*

### 2. Persistent Identifier (RECOMMENDED)
Not found

*Source: Confirmed absent. No CITATION.cff, codemeta.json, .zenodo.json, or DOI badge exists in the repository. DataCite `?query=enlilviz` returns 0 results; Zenodo `?q=enlilviz` returns 0 hits; SoMEF found no `identifier`. The project has no Zenodo/GitHub release integration.*

### 3. Code Repository (MANDATORY)
https://github.com/SWxTREC/enlilviz

*Source: Already recorded in HSSI. Confirmed by git remote, `pyproject.toml` `[project.urls] repository`, and the GitHub API (repository live, not archived, default branch `main`).*

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Data Visualization: Movies

*Source: Every value is grounded in code at revision 842da22, and every subcategory has its parent listed. `Data Visualization` was already recorded in HSSI.*

Per-value evidence:
- **Data Visualization** — `enlilviz/plotting/` is the package's headline capability.
- **Data Visualization: 2D Slices** — `LatitudeSlice`, `LongitudeSlice`, `RadialSlice` in `enlilviz/plotting/plots.py` render the model's longitude/latitude/radial cut-planes.
- **Data Visualization: 2D Graphics** — those classes draw `ax.pcolormesh` meshes on polar and Mollweide projections with a custom `ENLIL_CMAP` and `Colorbar` class.
- **Data Visualization: Line Plots** — `TimeSeries` draws `ax.plot(times, data)` traces of modeled density/velocity at Earth, STEREO-A, and STEREO-B.
- **Data Visualization: Movies** — `ForecasterPlot` and `_BasePlot` implement `__iter__`/`__next__` over the run's time steps with `save()` writing `enlil_{time}.png` frames; README documents this as "iterate through the entire time series to make a movie".
- **Data Processing and Analysis** — `enlilviz/io.py` reads and conditions netCDF model output into an analysis-ready data model.
- **Data Processing and Analysis: Calibration** — `_calibrate_variable()` reverses Enlil's packed-integer storage using the file's `cal_min`/`cal_range` attributes and per-variable `*_min`/`*_max` attributes ("All variables whose names begin with 'uncalibrated' are calibrated with the following formula (linear transform)").
- **Data Processing and Analysis: Processing** — `_transform_variable()` and `_transform_dimensions()` convert to physical units (m -> AU, m/s -> km/s, T -> nT, kg/m3 -> N/cm3), rename Enlil's terse variables to descriptive names, and reassign dimensions/coordinates; `_unstack_fieldline()` flattens the forward/backward field-line traces.
- **Data Processing and Analysis: 2D Slices** — `Enlil.get_slice(var, slice_plane, time)` extracts named 2D cut-planes with nearest-time selection; `_calibrate_variable` processes the twelve `dd/vv/pp/cc {12,13,23}_3d` slice variables.
- **Data Processing and Analysis: Analysis** — the package derives physical quantities from the raw model file rather than passing values through: `_calibrate_variable()` reconstructs real values from Enlil's packed-integer storage, and `_transform_variable()`/`_transform_dimensions()` convert them into physical units (AU, km/s, N/cm3, nT, degrees north). Those derived quantities are what the `Enlil`/`Evolution` accessor API (`times`, `r`, `lat`, `lon`, `get_satellite_position`, `get_satellite_data`, `get_slice`) returns.

Considered and excluded:
- **Data Processing and Analysis: Time Series Analysis** — extraction at satellite locations is plain indexed retrieval, not analysis. `get_satellite_data()` is a bare accessor (`self.ds.loc[{'satellite': satellite}][varname]`) and `_BasePlot.set_time()` is a single `sel(..., method='nearest')` index pick. The package performs none of this subcategory's indicators: a search of the whole package for temporal filtering, resampling, smoothing, trend, autocorrelation, or time-axis statistics returns nothing (the only `np.diff` is `_interp_grid` in `plots.py`, a pcolormesh grid-edge helper operating on spatial mesh coordinates). Plotting a time series is captured by `Data Visualization: Line Plots`.
- **Models and Simulations / …: MHD / …: Forecasting** — enlilviz does not solve or run anything. It visualizes output produced by the separate Enlil MHD code. `ForecasterPlot` reproduces a forecast office's figure layout; it does not forecast.
- **Data Processing and Analysis: Field-line Tracing** — `read_enlil2d` ingests and unstacks Enlil-computed field-line variables (`fld_step`, `*_FLD_*`, `_unstack_fieldline`) but performs no tracing/integration itself.
- **Coordinate Transforms (any)** — `_transform_dimensions()` converts colatitude-radians to degrees-north and metres to AU within one heliocentric spherical frame. That is unit/convention normalization, not a transform between named coordinate systems, and it is a private function.
- **Data Visualization: Orbit Plots** — satellite markers show instantaneous positions as context on the model field; no trajectory or orbital path is rendered.
- **Data Visualization: 3D Graphics / Web-Based / Spectrogram / Mission-Specific** — output is static 2D matplotlib only. (3D and web-based Enlil viewing is the sibling project `h3lioviz-server`, see Field 29.)
- **Data Processing and Analysis: Data Access and Retrieval** — no network client; `xr.load_dataset(filename)` takes a local path.
- **Data Processing and Analysis: File Format Conversion** — reads netCDF into memory; does not write a converted data file.

### 5. Related Region (MANDATORY)
- Solar Environment
- Solar Wind
- Interplanetary Space

*Source: `Solar Environment` was already recorded in HSSI. `Solar Wind` and `Interplanetary Space` are supported by Enlil being a solar wind model and the package being described throughout as "Enlil solar wind visualizations"; the plotted domain runs from the model inner boundary to ~1.7 AU (`RMIN, RMAX = 0, 1.8`; `r = np.linspace(0.101, 1.698, ...)` in `load_example`), i.e. the inner heliosphere between the Sun and beyond Earth orbit.*

*Considered and excluded: `Corona` (Enlil's inner boundary sits above the corona; enlilviz does not read WSA coronal output), `Earth Magnetosphere` (the model domain is the solar wind, not the magnetosphere).*

### 6. Authors (MANDATORY)
**Author 1: Greg Lucas**
- **Author Identifier:** https://orcid.org/0000-0003-1331-1863
- **Affiliations** (all five already recorded in HSSI for this author; none dropped, none added):
  - Laboratory for Atmospheric and Space Physics — https://ror.org/01fcjzv38
  - National Aeronautics and Space Administration — https://ror.org/027ka1x80
  - Sandia National Laboratories — https://ror.org/01apwpt12
  - United States Geological Survey — https://ror.org/035a68863
  - University of Colorado Boulder — https://ror.org/02ttsq026

*Source: Author and all five affiliations already recorded in HSSI, corroborated by `AUTHORS.rst` ("Development Lead: Greg Lucas <greg.lucas@lasp.colorado.edu>"), `pyproject.toml` `authors`, `enlilviz/__init__.py` `__author__`/`__email__`, PyHC `contact: Greg Lucas`, and SoMEF. ORCID 0000-0003-1331-1863 independently confirms four of the five affiliations as employments: Laboratory for Atmospheric and Space Physics (2019-04 -> present), USGS/Geomagnetism (2017-05 -> 2019-04), University of Colorado Boulder/Aerospace Engineering Sciences (2012-2017), Sandia National Laboratories (2009-2013). NASA is not among his ORCID employments but was already recorded for this author in HSSI from other software, and is retained.*

*Considered and not added: "Space Weather Technology Research and Education Center" (ROR-less). The repository is hosted under the SWxTREC GitHub organization, but that is project provenance, not a personal affiliation, and it appears in neither ORCID nor any repository file. Not added without evidence for the person. No other contributors exist — `AUTHORS.rst` says "Contributors: None yet."*

### 7. Software Name (MANDATORY)
enlilviz

*Source: Already recorded in HSSI. Confirmed by `pyproject.toml` `name`, PyPI package name, README title, and PyHC registry. The all-lowercase form is the project's own consistent styling.*

### 8. Description (MANDATORY)
A Python toolkit for Enlil solar wind visualizations. enlilviz reads post-processed output from the Enlil solar wind magnetohydrodynamic code — the 2D `suball` netCDF files and the per-object `evo` time-evolution files produced by runs such as NOAA's operational WSA-Enlil — into xarray-backed `Enlil` and `Evolution` objects, calibrating the packed model variables and converting them to physical units (AU, km/s, N/cm3, nT). On top of that data model it provides matplotlib plot classes for longitude, latitude, and radial 2D slices of density, velocity, and magnetic polarity, and for time series of the modeled solar wind at the Earth, STEREO-A, and STEREO-B locations. A pre-arranged `ForecasterPlot` figure reproduces the layout used by space weather forecasting offices, and the plot classes are iterable over a run's time steps so an entire model run can be rendered frame by frame into a movie.

**Correction.** The previous HSSI description was two concatenated one-liners:

> `A Python toolkit for Enlil solar wind visualizations.\nA Python package for visualizing output from the Enlil code.`

Line 1 is the GitHub repository description and the PyHC registry description; line 2 is `pyproject.toml`'s `description`. They are near-duplicates of each other and, together, say only that the package visualizes Enlil output — materially incomplete against Field 8's requirement that the description let a user judge whether the software is useful to their work (it omits the reader API, the xarray data model, the calibration/unit handling, the slice and time-series plot types, the forecaster figure, and the movie workflow).

The current text preserves that first sentence verbatim as its opening and expands from primary sources (`README.rst`, `enlilviz/io.py`, `enlilviz/enlil.py`, `enlilviz/plotting/`, `docs/examples.rst`, `HISTORY.rst`). The redundant second sentence was folded in rather than kept as a separate line; it is the only prior wording removed, and it is quoted above so the removal stays visible.

### 9. Concise Description (OPTIONAL)
A Python toolkit for reading Enlil solar wind model output into xarray and plotting 2D slices, satellite time series, and the pre-arranged forecast-office figure, frame by frame as a movie.

*Source: 189 characters, within the 200-character limit. Composed from README.rst and the plotting API.*

### 10. Publication Date (RECOMMENDED)
2020-02-14

*Source: Already recorded in HSSI. Corroborated by the GitHub API `created_at = 2020-02-14T22:30:17Z` (also SoMEF `date_created`). Documented alternative: the first public release was PyPI 0.0.1 on 2020-02-17 (`HISTORY.rst`: "0.0.1 (2020-02-17) — First release on PyPI"). The existing value is defensible as the date the repository was published, so it stands rather than being replaced over a 3-day judgment call.*

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

*Source: Field 11 instructs that when no DOI has been obtained the repository host is the correct entry; no DOI exists (Field 2). GitHub is already an established publisher organization in HSSI under the identifier `https://github.com`.*

### 12. Version (RECOMMENDED)
- **Version Number:** 0.2.0
- **Version Date:** 2022-11-27
- **Version Description:** Fixes handling of missing data variables in the more recent `suball` files that NOAA produces, so runs whose output omits some variables load without error.
- **Version PID:** Not found — no DOI is minted for any release.

*Source: Version number `0.2.0` was already recorded in HSSI and is confirmed still current: `pyproject.toml version = "0.2.0"`, `enlilviz/__init__.py __version__ = '0.2.0'`, newest git tag `v0.2.0`, only GitHub release `v0.2.0`, newest PyPI release 0.2.0, and `origin/main` HEAD is 842da22 — there is no newer release.*

**Correction — Version Date: 2025-03-28 → 2022-11-27.** The prior date is not a release date for this project: 0.2.0 shipped in November 2022 and nothing has been released since, so 2025-03-28 was a submission-time artifact. Authoritative evidence for 2022-11-27: `HISTORY.rst` heading "0.2.0 (2022-11-27)"; release commit 842da22 dated 2022-11-27 20:35:23 -0700. (The corresponding UTC instants are GitHub release published 2022-11-28T03:36:14Z and PyPI upload 2022-11-28T03:37:34Z; the project's own changelog dates the release 2022-11-27, so that is used.)

*Version Description is taken from `HISTORY.rst` 0.2.0 ("Fix handling of missing data variables from more recent suball files that NOAA uses.") and the GitHub release notes for `REL: v0.2.0` (PR #14 "FIX: Skip variables that aren't present in the dataset").*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source: Already recorded in HSSI and confirmed. `requires-python = ">=3.8"`, classifiers for Python 3.8-3.11, CI matrix 3.8/3.9/3.10/3.11, GitHub `language = Python`. No other implementation language (the repo's only non-Python files are a Makefile and Sphinx config, which do not meet Field 13's "most important languages" bar).*

### 14. Reference Publication (RECOMMENDED)
Not found

*Source: No paper describes enlilviz. No CITATION.cff, no "how to cite" section in README.rst or the documentation, no JOSS submission, no BibTeX (SoMEF's citation extractor found none), and DataCite/Zenodo return no records for the package.*

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

*Source: `LICENSE` is the MIT text, "Copyright (c) 2020, Regents of the University of Colorado"; `pyproject.toml` `license = {file = "LICENSE"}` plus classifier `License :: OSI Approved :: MIT License`; GitHub API `license.spdx_id = MIT`; SoMEF agrees. `MIT License` is HSSI's canonical name for this license, and `https://spdx.org/licenses/MIT` its canonical URI.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- enlil
- visualization
- heliosphere
- magnetohydrodynamics
- solar wind
- space weather
- WSA
- xarray

*Source: `enlil` and `visualization` were already recorded in HSSI and correspond to `pyproject.toml keywords = ["Enlil", "Visualization"]`. HSSI stores keywords lowercase. The six others: `heliosphere` (PyHC registry keyword for enlilviz), `magnetohydrodynamics` (Enlil is a 3D MHD heliospheric code), `solar wind` (the package's stated subject), `space weather` (`ForecasterPlot` reproduces the space weather forecast office figure per `docs/examples.rst`), `WSA` (the supported input is WSA-Enlil output — `wsa_enlil.latest.suball.nc`, and `ForecasterPlot._model_info()` reads the `wsa_version` file attribute), `xarray` (the public data model, see Field 30).*

*Considered and not added: `python` (covered by Field 13), `netcdf` (covered by Field 18), `coronal mass ejections` (covered by Field 22), `plotting` (redundant with `visualization`), `specific` (a PyHC registry keyword for enlilviz, but not a meaningful standalone search term — it carries no subject content).*

### 17. Data Sources (OPTIONAL)
- Other

*Source: enlilviz has no networked data-source client: both readers call `xr.load_dataset(filename)` on a local path (`read_enlil2d('wsa_enlil.latest.suball.nc')`, `read_evo('evo.earth.nc')`), and there is no HTTP/FTP/S3/HAPI/CDAWeb code anywhere in the package. Its input source — locally held post-processed WSA-Enlil model output files, such as those NOAA produces (`HISTORY.rst`: "more recent suball files that NOAA uses") — is not among the listed sources, and Field 17 instructs "If a source is not listed, select 'Other'."*

*Considered and excluded: `Observatory/Mission-specific` — the input is model output, not observatory data (see Fields 31-32).*

### 18. Input File Formats (RECOMMENDED)
- netCDF3/4

*Source: `enlilviz/io.py` docstring "Input routines for reading Enlil netcdf files"; `read_enlil2d` and `read_evo` both call `xr.load_dataset()` on `.nc` files; `netcdf4` is a hard runtime dependency in `pyproject.toml`. No other input format is supported.*

### 19. Output File Formats (RECOMMENDED)
- Other

*Source: The only files enlilviz writes are matplotlib figures: `ForecasterPlot.save(filename=None)` defaults to `"enlil_{time}.png"` via `self.fig.savefig(filename)`. PNG (and the other raster/vector formats matplotlib accepts through a user-supplied extension) has no dedicated HSSI file-format value, so `Other` is the correct selection. The package writes no data files.*

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

*Source: `.github/workflows/tests.yml` runs the full test suite on `os: [windows-latest, ubuntu-latest, macos-latest]` across Python 3.8-3.11. Pure-Python install via `pip install enlilviz`; `docs/installation.rst` imposes no platform restriction. Listing the three CI-verified platforms rather than `Operating System Independent`, since those are what is actually tested.*

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

*Source: enlilviz is pure Python — no compiled extensions, no build step beyond `setuptools`, no `[tool.setuptools.ext-modules]`, no architecture-specific code paths, and a `py3-none-any` wheel on PyPI. Architecture support is therefore inherited entirely from numpy/matplotlib/netcdf4 wheels rather than constrained by this package.*

### 22. Related Phenomena (OPTIONAL)
- Solar Wind
- Coronal Mass Ejections

Per-value evidence:
- **Solar Wind** — the package's subject: it plots modeled solar wind density, radial velocity, and magnetic polarity throughout the inner heliosphere and as time series at satellite locations.
- **Coronal Mass Ejections** — first-class support for Enlil's CME/cloud-tracer field: `_variables = {..., 'DP_CME': 'cme', ...}` and `_variables_evo = {..., 'DP': 'cme', ...}` in `enlilviz/io.py`, the `cc12_3d`/`cc13_3d`/`cc23_3d` slice variables calibrated and labelled "cloud parameter" in `_calibrate_variable`, and `cme` in the example dataset's variable set. WSA-Enlil+Cone runs exist principally to propagate CMEs.

*Considered and excluded: `Geomagnetic Storms` — enlilviz computes no geomagnetic index or ground response; the model domain ends in the solar wind.*

### 23. Development Status (RECOMMENDED)
Inactive

*Source: The package reached a stable, usable, documented public state — three PyPI releases (0.0.1 2020-02-17, 0.1.0 2020-04-27, 0.2.0 2022-11-28), published Read the Docs documentation, a passing three-OS CI matrix — but there has been no development since 2022-11-27: `origin/main` HEAD is still 842da22 (2022-11-27), GitHub `pushed_at = 2022-11-28T03:36:13Z`, and 4 issues remain open. That matches repostatus.org "Inactive" (stable and usable, no longer actively developed).*

*Conflicting evidence, flagged rather than followed: `pyproject.toml` carries `Development Status :: 2 - Pre-Alpha`. That classifier is unchanged cookiecutter boilerplate — it was still Pre-Alpha at the 0.2.0 release — and mapping it to repostatus `WIP` would be factually wrong, since WIP means "no stable, usable public release yet" and enlilviz has three. `Unsupported` was also considered and rejected: the authors have made no statement of ceasing work or seeking a new maintainer.*

### 24. Documentation (RECOMMENDED)
https://enlilviz.readthedocs.io

*Source: Already recorded in HSSI. Byte-identical to `pyproject.toml` `[project.urls] documentation`; README and SoMEF agree. PyHC lists the trailing-slash variant `https://enlilviz.readthedocs.io/`; not adopted, as the recorded form matches the project's own declaration.*

### 25. Funder (OPTIONAL)
Not found

*Source: No evidence found. There is no funding or acknowledgement statement anywhere in the repository (README.rst, docs/, AUTHORS.rst, CONTRIBUTING.rst, LICENSE, pyproject.toml), no DOI record to carry `fundingReferences`, and no paper. The LICENSE copyright holder is the "Regents of the University of Colorado" and the repository sits under the SWxTREC (Space Weather Technology Research and Education Center) GitHub organization, but a copyright holder and a hosting organization are not funders and no sponsoring agency or award is named. Recorded as Not found rather than inferred.*

### 26. Award Title (OPTIONAL)
Not found

*Source: No grant or award is named anywhere in the repository or in any external record for this package. Follows directly from Field 25.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

*Source: No publication in the repository, documentation, or PyHC entry describes, cites, or uses enlilviz, and DataCite/Zenodo hold no records referencing it. The Enlil model's own literature (e.g. Odstrcil 2003) describes the model, not this software, so it does not belong here.*

### 28. Related Datasets (OPTIONAL)
Not found

*Source: enlilviz consumes WSA-Enlil model output files rather than a published dataset, and no DOI-bearing or formally citable dataset for that output could be identified. NOAA/SWPC's WSA-Enlil Solar Wind Prediction is distributed as an operational product page (https://www.swpc.noaa.gov/products/wsa-enlil-solar-wind-prediction), not an archived dataset with a persistent identifier, so it is not recorded here as a related dataset.*

### 29. Related Software (OPTIONAL)
- **Enlil** — https://ccmc.gsfc.nasa.gov/models/ENLIL~2.8f/
- **h3lioviz-server** — https://github.com/SWxTREC/h3lioviz-server

*Source (Enlil): The 3D MHD heliospheric code (Dusan Odstrcil) whose output enlilviz exists solely to read and plot — the single most distinguishing related entity for this package, and the software a reader most needs to know about to understand what enlilviz is for. It is closed-source with no code repository and no software DOI, so per Field 29's instruction ("If no public repository, enter link where users can find more information") the value is the CCMC model page. It passes the distinguishing test unambiguously: the relationship is specific to this package and would be absurd to assert of most software.*

*Source (h3lioviz-server): A same-organization companion that performs the analogous task for the same data: its README describes "a ParaView visualization server for 3D heliospheric output from codes such as Enlil and Euhforia", and its pre-processing script `scripts/process_output.py` ingests the same SWPC WSA-Enlil netCDF run directories (documented run-id regex `^.*wsa_enlil_\d{5}\.\d*\.dbqs0`, with `netcdf4`/`xarray` in `scripts/requirements.txt`). Its `pvw/server/` contains the direct analogues of enlilviz's modules — `slice.py`, `satellite.py`, `assets/cmap-WSA-Enlil.json`. This is exactly Field 29's "performs similar tasks but does not necessarily link together": h3lioviz-server does not depend on enlilviz (`pvw/requirements.txt` is `flask`, `boto3`), so it is a similar-purpose/companion tool, not interoperable software. Listing it is distinguishing — it tells a reader enlilviz is the 2D matplotlib toolkit while h3lioviz is the 3D interactive web/ParaView route for the same output.*

*Considered and excluded:*
- ***Kamodo*** *(https://github.com/nasa/Kamodo) — the PyHC registry lists `enlil` among Kamodo's keywords, which would make it a similar-purpose reader of Enlil output. Dropped because the claim could not be verified: no Enlil reader exists anywhere in the `nasa/Kamodo` tree on `main`, `master`, or `develop`, and no `nasa/Kamodo-ccmc` repository exists. Not listed on unverified evidence.*
- ***numpy, matplotlib, netcdf4, setuptools, pytest*** — generic scientific-Python/tooling stack; Tier A exclusion applies to Field 29 as well as Field 30.*

### 30. Interoperable Software (OPTIONAL)
- **xarray** — https://github.com/pydata/xarray

*Source: Tier B inclusion with cited evidence of a documented exchange, not mere dependency presence: xarray is enlilviz's public interchange format. `Enlil.ds` and `Evolution.ds` are public attributes holding an `xarray.Dataset`; `get_slice()`, `get_satellite_data()`, and `get_satellite_position()` all declare `Returns: xarray.DataArray` in their docstrings; the README's first documented feature is "Read in Enlil data files into an xarray dataset for analysis"; the `Enlil`/`Evolution` constructors accept a user-supplied `xarray.Dataset` ("Parameters: ds : xarray.Dataset"); and `docs/conf.py` wires `intersphinx_mapping` to the xarray documentation so the returned types are cross-linked. A user can therefore take enlilviz output straight into any xarray-based workflow, and can hand an xarray Dataset back in.*

*Considered and excluded: **numpy**, **matplotlib** — Tier A, never listed; being a dependency is not interoperability. **netCDF4** — Tier B, but it is present only as xarray's file engine, with no exchange exposed in enlilviz's public API, docs, examples, or tests, so it does not qualify. **h3lioviz-server** — reads the same source files independently; there is no exchange between the two packages, so it belongs in Field 29 (above), not here.*

### 31. Related Instruments (OPTIONAL)
None — documented omission.

*Source: enlilviz is an instrument-agnostic tool: it reads and plots output from a numerical MHD model, never instrument data. No instrument name, instrument data format, calibration table, or instrument-specific parser appears anywhere in the package. There is no candidate instrument to resolve, so the field is correctly left empty.*

### 32. Related Observatories (OPTIONAL)
None — documented omission.

*Source: Correctly empty after explicit consideration.*

*Considered and excluded: **Earth, STEREO-A, and STEREO-B**. These appear in `enlilviz/io.py` as `_satellites = ['Earth', 'STEREO_A', 'STEREO_B']` and drive `TimeSeries` plots and position markers. They are **Enlil's output-sampling locations**, not data sources: enlilviz reads no STEREO telemetry, no STEREO instrument products, and no STEREO-specific format — the plotted density/velocity values are model results interpolated to those bodies' positions. The relevance gate therefore fails on both sanity checks: a user searching HSSI for `observatory:"STEREO"` would not want a model-output plotter back, and a scientist working with STEREO data would not reach for enlilviz.*

*Also considered and excluded: **NOAA / NOAA Space Weather Prediction Center**, the source of the operational WSA-Enlil runs enlilviz reads (`HISTORY.rst`). SWPC is a forecasting centre running a model, not an observatory, and the input is model output rather than observatory data — this belongs to Field 17, where it is reflected as `Other`.*

### 33. Logo (OPTIONAL)
Not found

*Source: No logo exists — no image files in the repository (`MANIFEST.in` reserves `docs/*.jpg|png|gif` but none are committed), no logo in the README (its only images are PyPI/Travis/Read the Docs status badges), no `logo:` key in the PyHC registry entry for enlilviz, and SoMEF extracted no `logo`.*
