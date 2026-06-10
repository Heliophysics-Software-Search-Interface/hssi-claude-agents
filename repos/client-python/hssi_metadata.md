# HSSI Metadata Extraction Results

**Repository:** https://github.com/hapi-server/client-python
**Extraction Date:** 2025-10-01
**HSSI Sync:** 2026-06-09 — reconciled with the live HSSI record after a local metadata update. Field values below reflect what is in HSSI (software UUID `f6e3429d-e80e-4cf6-889e-44af1e93f87d`).

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.5553155
- **Source:** Found in .zenodo.json file (concept DOI)

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/hapi-server/client-python
- **Source:** Repository URL

### 4. Software Functionality (MANDATORY)
Based on comprehensive analysis of the code, documentation, and PyHC metadata, the following functionalities apply:

- **Data Processing and Analysis** - Parent category
- **Data Processing and Analysis:Data Access and Retrieval** - Primary functionality: retrieves time series data from HAPI servers
- **Data Processing and Analysis:Processing** - Parses binary/CSV HAPI responses into NumPy structured arrays; provides time-format conversion (hapitime2datetime, datetime2hapitime), chunked/parallel requests, caching, and data trimming/concatenation

**Analysis:** The HAPI client is a Python interface for accessing time series data from Heliophysics Application Programmer's Interface (HAPI) servers. It retrieves data from various heliophysics data sources (CDAWeb, OMNI, and other HAPI-compliant servers). Visualization (line plots, spectrograms) is provided by the separate optional `hapiplot` package and is not part of `hapiclient` itself — the hapiclient public API (`__init__.py`) exports only data retrieval and time-conversion functions.

### 5. Related Region (MANDATORY)
Based on analysis of typical HAPI server data and the README examples, plus the regions already curated in the HSSI record:

- **Earth Atmosphere** - retained from the existing HSSI record
- **Earth Magnetosphere** - OMNI data example in README includes magnetospheric data
- **Interplanetary Space** - HAPI servers provide solar wind and interplanetary data
- **Planetary Magnetospheres** - retained from the existing HSSI record
- **Solar Environment** - HAPI servers provide solar data

**Analysis:** The HAPI client is a general-purpose data access tool that can retrieve data from any HAPI-compliant server, so a broad set of regions applies. The extraction originally identified three regions (Earth Magnetosphere, Interplanetary Space, Solar Environment); the HSSI record additionally includes Earth Atmosphere and Planetary Magnetospheres, which were kept during reconciliation. The actual regions depend on which HAPI servers and datasets the user accesses.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Robert S. Weigel
- **Author Identifier:** https://orcid.org/0000-0002-9521-5228
- **Affiliation - Organization:** George Mason University
- **Affiliation Identifier:** https://ror.org/02jqj7156
- **Source:** ORCID (canonical name), LICENSE.txt (R.S. Weigel), DataCite API, .zenodo.json, setup.py
- **Note:** setup.py, .zenodo.json list informal "Bob Weigel"; CITATION.cff has family-names and given-names reversed. Canonical form from ORCID used.

**Author 2:**
- **Name:** Hari Narayana Batta
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Source:** DataCite API, Zenodo API

**Author 3:**
- **Name:** Jeremy Faden
- **Author Identifier:** https://orcid.org/0000-0003-2397-488X
- **Affiliation - Organization:** Cottage Systems; University of Iowa
- **Source:** Existing HSSI record (ORCID + affiliations carried from the maintainer submission and kept during reconciliation); DataCite/Zenodo API for name

**Author 4:**
- **Name:** Jon Vandegriff
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Source:** DataCite API, Zenodo API (handle "jvandegriff"); full name supplied by submitter

### 7. Software Name (MANDATORY)
- **Value:** HAPI Client
- **Alternative Names:** hapiclient, hapi-server/client-python
- **Source:** PyHC registry (authoritative display name: HAPI Client); setup.py package identifier is `hapiclient`

### 8. Description (MANDATORY)
- **Value:** A Python client for the Heliophysics Application Programmer's Interface (HAPI). This package provides functions to access time series data from HAPI-compliant servers, which serve data from various heliophysics missions and instruments. The client handles data retrieval, caching, and provides utilities for time format conversions. An optional hapiplot package provides basic visualization capabilities including line plots and spectrograms. The HAPI data model is intentionally minimal and follows the HAPI metadata specification closely.
- **Source:** Synthesized from README.md, setup.py, DataCite API, PyHC registry, and code analysis

### 9. Concise Description (OPTIONAL)
- **Value:** Python client for accessing time series data from HAPI servers, providing data retrieval and basic plotting capabilities for heliophysics data.
- **Source:** Synthesized from multiple sources

### 10. Publication Date (RECOMMENDED)
- **Value:** 2021-10-06
- **Source:** HSSI record (Zenodo concept DOI publication date). The extraction originally proposed 2017-06-02 (GitHub date_created via SoMEF); the HSSI DOI-based date was kept during reconciliation.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/01ggx4157
- **Source:** DataCite API, Zenodo API; ROR lookup (api.ror.org)

### 12. Version (RECOMMENDED)

**Latest Release Version (current HSSI value):**
- **Version Number:** v0.2.9
- **Version Date:** 2026-06-08
- **Version Description:** Not found in repository
- **Version PID:** https://doi.org/10.5281/zenodo.20598746
- **Source:** GitHub release v0.2.9 (published 2026-06-08); Zenodo version DOI 10.5281/zenodo.20598746

**Earlier release (extraction-time):**
- **Version Number:** v0.2.6 (2024-05-11) — superseded by v0.2.9

**Note:** v0.2.9 was released 2026-06-08 and registered on Zenodo; this is the value set in HSSI during the local update.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** - Primary language (111,259 bytes)
- **Python 2.x** - Also supported: setup.py has Py2 dependency branch, `hapiclient/__init__.py` includes `sys.version_info[0] < 3` compatibility block, tox.ini envlist includes `py27`
- **Source:** SoMEF, GitHub API, PyHC registry, direct inspection of setup.py/__init__.py/tox.ini

### 14. Reference Publication (OPTIONAL)
- **Value:** https://doi.org/10.1029/2021JA029534
- **Source:** Kept from the existing HSSI record (the extraction found no reference publication in the repository).

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html
- **SPDX ID:** BSD-3-Clause
- **Source:** LICENSE.txt, SoMEF, GitHub API, SPDX

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
From PyHC registry and analysis:
- data_retrieval
- line_plots
- plotting
- spectra
- heliophysics
- time series
- HAPI

**Source:** PyHC registry, analysis of functionality

### 17. Data Sources (OPTIONAL)
- **CDAWeb** - Explicitly mentioned in README example
- **HAPI** - Primary data source type
- **OMNIWeb** - Accessible through CDAWeb HAPI endpoint
- **Observatory/Mission-specific** - HAPI servers can be mission-specific

**Source:** README.md, HAPI specification
**Note:** See http://hapi-server.org/servers/ for full list of HAPI servers

### 18. Input File Formats (RECOMMENDED)
The HAPI client doesn't read local files directly; it retrieves data from HAPI servers via HTTP:
- **Not applicable** - Data is retrieved from servers, not read from files

### 19. Output File Formats (RECOMMENDED)
Data returned as:
- **Python data structures** - Numpy arrays and Python dictionaries
- **Not applicable for traditional file formats** - The package returns in-memory data structures

**Note:** Users can convert the returned data to formats like CSV, HDF5, or CDF using other libraries

### 20. Operating System (RECOMMENDED)
- **Operating System Independent** - Pure Python package, works on any OS with Python
- **Source:** Package structure analysis (no OS-specific dependencies)

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** - Pure Python with numpy, no architecture-specific code
- **Source:** Package analysis

### 22. Related Phenomena (OPTIONAL)
- **Not found** - No specific phenomena listed
- **Note:** As a general data access client, it can access data related to many phenomena depending on the HAPI server queried

### 23. Development Status (RECOMMENDED)
- **Active** - Repository shows recent activity (last update: 2025-05-29 per SoMEF)
- **Source:** SoMEF (date_updated), PyHC registry (all quality ratings: Good)

### 24. Documentation (RECOMMENDED)
- **Value:** https://github.com/hapi-server/client-python/blob/master/README.md
- **Additional:**
  - Demo Jupyter Notebook: https://colab.research.google.com/github/hapi-server/client-python-notebooks/blob/master/hapi_demo.ipynb
  - Example script: https://github.com/hapi-server/client-python/blob/master/hapi_demo.py
- **Source:** PyHC registry, README.md

### 25. Funder (OPTIONAL)
- **Value:** Not found
- **Note:** No funding information found in repository files or DOI metadata

### 26. Award Title (OPTIONAL)
- **Value:** Not found
- **Note:** No award information found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Value:** Not found
- **Note:** No publications citing or describing this software were found in the repository

### 28. Related Datasets (OPTIONAL)
- **Value:** Not specific datasets
- **Note:** The client can access any dataset from HAPI-compliant servers. See http://hapi-server.org/servers/ for available datasets

### 29. Related Software (OPTIONAL)
- **hapiplot** - Optional plotting package for HAPI data
  - Repository: https://github.com/hapi-server/plot-python
  - Relationship: Companion visualization package
- **Source:** README.md

### 30. Interoperable Software (OPTIONAL)
- **hapiplot** - Companion visualization package for HAPI data
  - Repository: https://github.com/hapi-server/plot-python
- **Note:** numpy/pandas/isodate are runtime dependencies rather than interoperable software, so only hapiplot is recorded here (and in HSSI).

### 31. Related Instruments (OPTIONAL)
- **Value:** Not specific instruments
- **Note:** The client can access data from any instrument whose data is served via a HAPI server

### 32. Related Observatories (OPTIONAL)
Examples from README and HAPI server listings:
- **OMNI** - Solar wind data (via CDAWeb HAPI)
- **CDAWeb** - NASA's space physics data facility
- **Note:** Many other observatories serve data via HAPI. See http://hapi-server.org/servers/

### 33. Logo (OPTIONAL)
- **Value:** https://hapi-server.org/logos/HAPI-large.png
- **Source:** HAPI server project logo (hapi-server.org), set per user request. (Earlier value was the PyHC-registry SVG `https://raw.githubusercontent.com/hapi-server/hapi-server.github.io/master/logos/HAPI.svg`.)

---

## Summary of Metadata Sources

### Source Priority and Verification
Metadata was extracted using the following sources (in priority order):

1. **PyHC Registry (Core Packages)** - ✓ Found
   - Manually curated, highest trustworthiness
   - Provided: logo, documentation URL, keywords, quality ratings, contact

2. **DataCite/Zenodo APIs** - ✓ Found (DOI: 10.5281/zenodo.5553155)
   - Official DOI metadata
   - Provided: authors, affiliations, publication date, version info, concept DOI

3. **SoMEF** - ✓ Completed
   - Automated repository analysis
   - Provided: programming languages, license, dates, releases

4. **Manual Repository Examination** - ✓ Completed
   - Direct file inspection
   - Provided: ORCID for main author, current version, dependencies

### Critical MANDATORY Fields Status
- ✅ **Submitter** - To be filled by user
- ✅ **Code Repository** - https://github.com/hapi-server/client-python
- ✅ **Software Functionality** - Data Processing and Analysis (+ Data Access and Retrieval, Processing)
- ✅ **Related Region** - Earth Atmosphere, Earth Magnetosphere, Interplanetary Space, Planetary Magnetospheres, Solar Environment
- ✅ **Authors** - 4 authors identified with ORCID for primary author
- ✅ **Software Name** - HAPI Client
- ✅ **Description** - Comprehensive description provided

### PyHC Package Information
**Package Found:** Yes, in Core Packages
**Quality Ratings:** All "Good"
- Community: Good
- Documentation: Good
- Testing: Good
- Software Maturity: Good
- Python 3: Good
- License: Good

---

## Notes and Recommendations

1. **Version:** As of the 2026-06-09 HSSI sync, the current release is v0.2.9 (2026-06-08), registered on Zenodo (10.5281/zenodo.20598746). (At extraction time the newest DOI was v0.2.1 while the repo had v0.2.6.)

2. **Related Regions:** The HSSI record carries five regions (Earth Atmosphere, Earth Magnetosphere, Interplanetary Space, Planetary Magnetospheres, Solar Environment). The extraction proposed three; the two additional regions were retained from the existing HSSI record during reconciliation.

3. **Software Functionality:** The primary functionality is data access/retrieval plus response parsing/processing. Plotting is NOT part of this package — it is provided by the separate optional `hapiplot` package (https://github.com/hapi-server/plot-python).

4. **Reference Publication:** No primary publication found. Authors may want to consider publishing in JOSS or similar venue.

5. **ORCID Coverage:** Only the primary author (Robert S. Weigel) has an ORCID identified. Other contributors may benefit from having their ORCIDs linked.

6. **Documentation Quality:** Excellent documentation with README, Jupyter notebooks, and example scripts. Hosted on Google Colab for easy access.
