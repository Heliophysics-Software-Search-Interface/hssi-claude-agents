# HSSI Metadata Extraction Results

**Repository:** https://github.com/geospace-code/georinex
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Concept DOI:** https://doi.org/10.5281/zenodo.595473
- **Source:** DataCite API, Zenodo API

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/geospace-code/georinex
- **Source:** GitHub repository, DataCite API

### 4. Software Functionality (MANDATORY)
- **Coordinate Transforms** - Exposes `keplerian2ecef` and uses optional geodetic coordinate conversions for receiver and satellite location workflows
- **Data Processing and Analysis**
- **Data Processing and Analysis:File Format Conversion** - Converts RINEX 2/3/4 to NetCDF4/HDF5 formats for efficient storage and processing
- **Data Processing and Analysis:Data Reduction** - Supports filtering by time interval, satellite, and measurement type
- **Data Processing and Analysis:Processing** - Processes GNSS/GPS data with xarray Dataset for efficient analysis
- **Data Visualization**
- **Data Visualization:2D Graphics** - Plotting capabilities for RINEX data visualization
- **Data Visualization:Line Plots** - Time series visualization of GPS/GNSS observations
- **Data Visualization:Orbit Plots** - Plots satellite and receiver positions on geographic maps
- **Source:** README.md, `src/georinex/base.py`, `src/georinex/plots.py`, `src/georinex/plots_geo.py`, `src/georinex/keplerian.py`

### 5. Related Region (MANDATORY)
- **Earth Atmosphere** - Primary application for ionospheric and atmospheric studies using GNSS data; PyHC keywords indicate ionosphere_thermosphere_mesosphere research
- **Source:** PyHC registry keywords (ionosphere_thermosphere_mesosphere), RINEX application domain for atmospheric research

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Michael Hirsch
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Note:** Normalized from the `scivision` creator handle using LICENSE copyright and git history

**Author 2:**
- **Name:** Nikolay Mayorov
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 3:**
- **Name:** Joakim Strandberg
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 4:**
- **Name:** Martin Valgur
- **Author Identifier:** Not found
- **Affiliation:** Milrem Robotics

**Author 5:**
- **Name:** Snehil Saluja
- **Author Identifier:** Not found
- **Affiliation:** IIT Kanpur

**Author 6:**
- **Name:** Daniel Estévez
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 7:**
- **Name:** Elias Kunnas
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 8:**
- **Name:** Frédéric Meynadier
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 9:**
- **Name:** Volker Mayer
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Note:** Normalized from the `VOMAY` GitHub handle; GitHub PR #53 shows "Volker Mayer added 3 commits" for that contributor

**Author 10:**
- **Name:** Derek Knowles
- **Author Identifier:** Not found
- **Affiliation:** Not found

- **Source:** DataCite API, Zenodo API, GitHub PR #53, GitHub PR #69
- **Note:** Creator list follows the Zenodo concept/version DOI creators, with GitHub-handle creators normalized to personal names where primary public evidence was available. The remaining `izzydrewlynn` creator handle appears in DOI metadata and git history but is not mapped here because no primary source located in this workflow ties it to a personal name.

### 7. Software Name (MANDATORY)
- **Software Name:** GEOrinex
- **Package Name:** georinex
- **Source:** PyHC registry name is authoritative for HSSI; repository and package use `georinex`, and README title uses `GeoRinex`

### 8. Description (MANDATORY)
RINEX 2, RINEX 3, RINEX 4, and SP3 reader with batch conversion to NetCDF4 / HDF5 in Python or Matlab. GEOrinex reads plain, compressed, and Hatanaka-compressed GNSS navigation and observation files into xarray datasets for filtering, plotting, and offline analysis, and can write converted NetCDF4 outputs for faster reuse on large datasets.

- **Source:** README.md, SoMEF extraction

### 9. Concise Description (OPTIONAL)
Python RINEX 2/3/4 and SP3 reader with batch conversion to NetCDF4/HDF5 for GNSS processing, plotting, and scalable offline analysis of large local datasets.

- **Source:** Derived from GitHub description and README

### 10. Publication Date (RECOMMENDED)
- **Date:** 2015-04-21
- **Source:** Git repository first commit date
- **Note:** This is the date of initial software creation

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Zenodo API, DataCite API

### 12. Version (RECOMMENDED)

**Current Version:**
- **Version Number:** v1.16.2
- **Version Date:** 2023-11-15
- **Version Description:** Fixed numerous bugs, including xarray API update. Requires Python 3.8+ as Python 3.7 library support and wheel availability is dwindling.
- **Version PID:** https://doi.org/10.5281/zenodo.10130117
- **Source:** DataCite API, GitHub releases, git tags, `src/georinex/__init__.py`

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** - Primary language (144,698 bytes)
- **MATLAB** - Secondary support (1,268 bytes)
- **Source:** GitHub API (via SoMEF), `pyproject.toml` (`requires-python = \">=3.10\"`), `ReadRinex.m`

### 14. Reference Publication (RECOMMENDED)
- **DOI:** Not found
- **Note:** CITATION file references a Zenodo DOI (https://doi.org/10.5281/zenodo.3401498) which appears to be a version DOI, not a separate publication

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html
- **SPDX ID:** MIT
- **Source:** LICENSE.txt, GitHub API

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- gnss
- gps
- rinex
- sp3
- HDF5
- NetCDF4
- ionosphere_thermosphere_mesosphere (from PyHC)

- **Source:** GitHub repository topics, pyproject.toml, PyHC registry, SoMEF

### 17. Data Sources (OPTIONAL)
- Not found
- **Note:** GEOrinex reads local files and in-memory text streams; the README's UNAVCO URLs are example download locations rather than supported remote-access backends
- **Source:** README.md, `src/georinex/base.py`, `src/georinex/rio.py`

### 18. Input File Formats (RECOMMENDED)
- **ascii** - Plain ASCII RINEX files
- **netCDF3/4** - Can read previously converted `.nc` datasets
- **Other** - Compressed formats (.gz, .Z, .bz2, .zip), Hatanaka compressed RINEX (.crx)
- **Source:** README.md, `src/georinex/base.py`, code analysis

### 19. Output File Formats (RECOMMENDED)
- **netCDF3/4** - Primary output format
- **Source:** README.md, `src/georinex/base.py`, `src/georinex/sp3.py`

### 20. Operating System (RECOMMENDED)
- **Linux** - Tested in CI (ubuntu-latest)
- **Mac** - Tested in CI (macos-latest)
- **Windows** - Tested in CI (windows-latest)
- **Operating System Independent** - Declared in package classifiers and designed for cross-platform use
- **Source:** .github/workflows/ci.yml, README mentions cross-platform install

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** - Pure Python implementation works on any architecture
- **Source:** Python-based implementation, cross-platform nature

### 22. Related Phenomena (OPTIONAL)
- Not found
- **Note:** Could potentially include ionospheric phenomena, but not explicitly stated

### 23. Development Status (RECOMMENDED)
- **Active** - Reached stable, usable state and being actively developed
- **Source:** Recent commit (2025-03-09), released tag v1.16.2, PyHC unevaluated registry

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/geospace-code/georinex
- **Note:** Documentation is primarily in the README; no separate documentation site found
- **Source:** Repository structure, no .readthedocs.yml or docs hosting detected

### 25. Funder (OPTIONAL)
- Not found
- **Source:** No funding information in DataCite API or repository files

### 26. Award Title (OPTIONAL)
- Not found
- **Source:** No award information found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Not found
- **Source:** No related publications in DataCite API relatedIdentifiers

### 28. Related Datasets (OPTIONAL)
- Not found
- **Note:** While the software processes UNAVCO and other RINEX datasets, no specific dataset DOIs are referenced

### 29. Related Software (OPTIONAL)
- https://github.com/pydata/xarray
- https://github.com/numpy/numpy
- https://github.com/valgur/hatanaka
- https://github.com/vapier/ncompress
- https://github.com/Unidata/netcdf4-python
- https://github.com/scivision/pymap3d
- **Source:** `pyproject.toml` dependencies, README.md mentions

### 30. Interoperable Software (OPTIONAL)
- https://github.com/pydata/xarray
- https://github.com/pandas-dev/pandas
- https://github.com/matplotlib/matplotlib
- https://github.com/SciTools/cartopy
- **Source:** `pyproject.toml`, README.md

### 31. Related Instruments (OPTIONAL)
- Not found
- **Note:** Software is instrument-agnostic, processing standard RINEX format from any GNSS receiver

### 32. Related Observatories (OPTIONAL)
- Not found
- **Note:** The package is general-purpose across GNSS networks; README references to UNAVCO are data-source examples rather than an observatory-specific software target

### 33. Logo (OPTIONAL)
- Not found
- **Source:** No logo URL found in repository or SoMEF output

---

## Additional Notes

### PyHC Package Information
- **Status:** Unevaluated PyHC package
- **PyHC Contact:** Michael Hirsch
- **PyHC Description:** Python RINEX 2/3 NAV/OBS reader with speed and simplicity, handling most RINEX formats.
- **PyHC Keywords:** ionosphere_thermosphere_mesosphere, specific

### GitHub Statistics
- **Stars:** 260
- **Forks:** 97
- **Source:** SoMEF/GitHub API

### Test Coverage
- **Test Framework:** pytest
- **Number of Tests:** 158 (as of README)
- **Source:** README.md

### Version History
- **Total Versions:** 48 versions on Zenodo
- **First Release:** v0.5.0 (2017-05-30, DOI: 10.5281/zenodo.569328)
- **Latest Release:** v1.16.2 (2023-11-15, DOI: 10.5281/zenodo.10130117)
- **Source:** DataCite API relatedIdentifiers

---

## Metadata Extraction Summary

**Automated Sources Used:**
- ✅ DataCite API
- ✅ Zenodo API
- ✅ SoMEF
- ✅ PyHC Registry (unevaluated packages)

**Manual Sources Examined:**
- ✅ README.md
- ✅ LICENSE.txt
- ✅ CITATION
- ✅ pyproject.toml
- ✅ .github/workflows/ci.yml
- ✅ Git history and tags

**Completeness:**
- All 33 HSSI form fields addressed
- 6 MANDATORY fields: ✅ Complete
- RECOMMENDED fields: Mostly complete
- Domain-specific fields (Software Functionality, Related Region): Analyzed based on RINEX/GNSS domain knowledge
