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
- **URL:** https://github.com/geospace-code/georinex
- **Source:** GitHub repository, DataCite API

### 4. Software Functionality (MANDATORY)
- **Data Processing and Analysis:Data Access and Retrieval** - Reads RINEX observation and navigation files from various sources
- **Data Processing and Analysis:File Format Conversion** - Converts RINEX 2/3/4 to NetCDF4/HDF5 formats for efficient storage and processing
- **Data Processing and Analysis:Data Reduction** - Supports filtering by time interval, satellite, and measurement type
- **Data Processing and Analysis:Processing** - Processes GNSS/GPS data with xarray Dataset for efficient analysis
- **Data Processing and Analysis:Time Series Analysis** - Handles time-series GNSS observations and navigation data
- **Data Visualization:2D Graphics** - Plotting capabilities for RINEX data visualization
- **Data Visualization:Line Plots** - Time series visualization of GPS/GNSS observations
- **Source:** README.md, code analysis, package description, pyproject.toml

### 5. Related Region (MANDATORY)
- **Earth Atmosphere** - Primary application for ionospheric and atmospheric studies using GNSS data; PyHC keywords indicate ionosphere_thermosphere_mesosphere research
- **Source:** PyHC registry keywords (ionosphere_thermosphere_mesosphere), RINEX application domain for atmospheric research

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** scivision (Michael Hirsch)
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Note:** Identified as Michael Hirsch from LICENSE copyright and PyHC contact

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
- **Name:** fmeynadier
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 9:**
- **Name:** VOMAY
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 10:**
- **Name:** Derek Knowles
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 11:**
- **Name:** izzydrewlynn
- **Author Identifier:** Not found
- **Affiliation:** Not found

- **Source:** DataCite API, Zenodo API
- **Note:** Primary contact is Michael Hirsch based on PyHC registry and LICENSE file copyright

### 7. Software Name (MANDATORY)
- **Name:** GeoRinex
- **Source:** README.md, GitHub repository name (georinex), DataCite API

### 8. Description (MANDATORY)
RINEX 4, RINEX 3 and RINEX 2 reader and batch conversion to NetCDF4 / HDF5 in Python or Matlab. Batch converts NAV and OBS GPS RINEX (including Hatanaka compressed OBS) data into xarray.Dataset for easy use in analysis and plotting. This gives remarkable speed vs. legacy iterative methods, and allows for HPC / out-of-core operations on massive amounts of GNSS data. GeoRinex has over 125 unit tests driven by Pytest. Pure compiled language RINEX processors such as within Fortran NAPEOS give perhaps 2x faster performance than this Python program, but the initial goal was to be for one-time offline conversion of ASCII (and compressed ASCII) RINEX to HDF5/NetCDF4, where ease of cross-platform install and correctness are primary goals.

- **Source:** README.md, SoMEF extraction

### 9. Concise Description (OPTIONAL)
Python RINEX 2/3/4 NAV/OBS/SP3 reader with batch conversion to HDF5/NetCDF4, offering C-like speed for GNSS data processing and analysis.

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
- **Source:** Zenodo API, GitHub releases, git tags

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** - Primary language (144,698 bytes)
- **MATLAB** - Secondary support (1,268 bytes)
- **Source:** GitHub API (via SoMEF), pyproject.toml (requires Python >=3.10)

### 14. Reference Publication (RECOMMENDED)
- **DOI:** Not found
- **Note:** CITATION file references a Zenodo DOI (https://doi.org/10.5281/zenodo.3401498) which appears to be a version DOI, not a separate publication

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://api.github.com/licenses/mit
- **SPDX ID:** MIT
- **Source:** LICENSE.txt, GitHub API, DataCite API

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
- **FTP/FTPS Directories** - UNAVCO RINEX data repositories
- **HTTP/HTTPS Directories** - Various RINEX data sources
- **Source:** README.md mentions UNAVCO FTP sites and other data sources

### 18. Input File Formats (RECOMMENDED)
- **ascii** - Plain ASCII RINEX files
- **Other** - Compressed formats (.gz, .Z, .bz2, .zip), Hatanaka compressed RINEX (.crx)
- **Source:** README.md, code analysis

### 19. Output File Formats (RECOMMENDED)
- **netCDF3/4** - Primary output format
- **HDF5** - NetCDF4 is a subset of HDF5
- **Source:** README.md, package description

### 20. Operating System (RECOMMENDED)
- **Linux** - Tested in CI (ubuntu-latest)
- **Mac** - Tested in CI (macos-latest)
- **Windows** - Tested in CI (windows-latest)
- **Source:** .github/workflows/ci.yml, README mentions cross-platform install

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** - Pure Python implementation works on any architecture
- **Source:** Python-based implementation, cross-platform nature

### 22. Related Phenomena (OPTIONAL)
- Not found
- **Note:** Could potentially include ionospheric phenomena, but not explicitly stated

### 23. Development Status (RECOMMENDED)
- **Active** - Reached stable, usable state and being actively developed
- **Source:** Recent commit (2025-12-03), multiple recent releases, PyHC unevaluated registry

### 24. Documentation (RECOMMENDED)
- **URL:** https://github.com/geospace-code/georinex/blob/main/README.md
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
- **xarray** - Core dependency for data structures
- **numpy** - Numerical processing
- **hatanaka** - Hatanaka CRINEX decompression (https://github.com/valgur/hatanaka)
- **PyMap3d** - Coordinate conversions (https://github.com/scivision/pymap3d)
- **Source:** pyproject.toml dependencies, README.md mentions

### 30. Interoperable Software (OPTIONAL)
- **xarray** - Direct integration as primary data structure
- **Pandas** - Can convert to Pandas DataFrames
- **matplotlib** - Optional plotting dependency
- **cartopy** - Optional geospatial plotting
- **Source:** pyproject.toml, README.md

### 31. Related Instruments (OPTIONAL)
- Not found
- **Note:** Software is instrument-agnostic, processing standard RINEX format from any GNSS receiver

### 32. Related Observatories (OPTIONAL)
- **UNAVCO** - Major data source mentioned in README
- **Note:** Software works with data from any GNSS observatory/network that produces RINEX files
- **Source:** README.md extensive references to UNAVCO data repositories

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
