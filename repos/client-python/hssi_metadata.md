# HSSI Metadata Extraction Results

**Repository:** https://github.com/hapi-server/client-python
**Extraction Date:** 2025-10-01

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

- **Data Processing and Analysis:Data Access and Retrieval** - Primary functionality: retrieves time series data from HAPI servers
- **Data Visualization:Line Plots** - From PyHC keywords and hapiplot integration
- **Data Visualization:Spectrogram** - From PyHC keywords and hapiplot capabilities

**Analysis:** The HAPI client is a Python interface for accessing time series data from Heliophysics Application Programmer's Interface (HAPI) servers. It retrieves data from various heliophysics data sources (CDAWeb, OMNI, and other HAPI-compliant servers) and provides basic plotting capabilities through the optional hapiplot package.

### 5. Related Region (MANDATORY)
Based on analysis of typical HAPI server data and the README examples:

- **Earth Magnetosphere** - OMNI data example in README includes magnetospheric data
- **Interplanetary Space** - HAPI servers provide solar wind and interplanetary data
- **Solar Environment** - HAPI servers provide solar data

**Analysis:** The HAPI client is a general-purpose data access tool that can retrieve data from any HAPI-compliant server. Since HAPI servers provide data across multiple heliophysics regions, and the example in the README uses OMNI data (which spans solar wind, magnetosphere, and interplanetary space), all three regions are appropriate. Note that this is a client library, so the actual regions depend on which HAPI servers and datasets the user accesses.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Bob Weigel (full name: Robert S. Weigel)
- **Author Identifier:** https://orcid.org/0000-0002-9521-5228
- **Affiliation - Organization:** George Mason University
- **Affiliation Identifier:** Not found
- **Source:** DataCite API (primary), .zenodo.json, setup.py
- **Note:** CITATION.cff has family-names and given-names reversed

**Author 2:**
- **Name:** Hari Narayana Batta
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Source:** DataCite API, Zenodo API

**Author 3:**
- **Name:** Jeremy Faden
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Source:** DataCite API, Zenodo API

**Author 4:**
- **Name:** jvandegriff
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Source:** DataCite API, Zenodo API

### 7. Software Name (MANDATORY)
- **Value:** hapiclient
- **Alternative Names:** HAPI Client, hapi-server/client-python
- **Source:** setup.py (package name: hapiclient), PyHC registry (display name: HAPI Client)

### 8. Description (MANDATORY)
- **Value:** A Python client for the Heliophysics Application Programmer's Interface (HAPI). This package provides functions to access time series data from HAPI-compliant servers, which serve data from various heliophysics missions and instruments. The client handles data retrieval, caching, and provides utilities for time format conversions. An optional hapiplot package provides basic visualization capabilities including line plots and spectrograms. The HAPI data model is intentionally minimal and follows the HAPI metadata specification closely.
- **Source:** Synthesized from README.md, setup.py, DataCite API, PyHC registry, and code analysis

### 9. Concise Description (OPTIONAL)
- **Value:** Python client for accessing time series data from HAPI servers, providing data retrieval and basic plotting capabilities for heliophysics data.
- **Source:** Synthesized from multiple sources

### 10. Publication Date (RECOMMENDED)
- **Value:** 2017-06-02
- **Source:** SoMEF (date_created from GitHub API)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

**Latest Release Version:**
- **Version Number:** v0.2.6
- **Version Date:** 2024-05-11
- **Version Description:** Not found in repository
- **Version PID:** Not found (no specific DOI for v0.2.6)
- **Source:** Git tags

**Version from Zenodo DOI:**
- **Version Number:** v0.2.1
- **Version Date:** 2021-10-06
- **Version Description:** Not found
- **Version PID:** https://doi.org/10.5281/zenodo.5553156
- **Source:** Zenodo API, DataCite API

**Current Development Version:**
- **Version Number:** v0.2.7b1
- **Source:** setup.py (in development, not yet released)

**Note:** The latest GitHub release is v0.2.6 (2024-05-11), but the most recent DOI is for v0.2.1 (2021-10-06). The package appears to be actively maintained with newer versions not yet registered with Zenodo.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** - Primary language (111,259 bytes)
- **Source:** SoMEF, GitHub API, PyHC registry

### 14. Reference Publication (OPTIONAL)
- **Value:** Not found
- **Note:** No JOSS paper or primary reference publication was found in the repository

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://api.github.com/licenses/bsd-3-clause
- **SPDX ID:** BSD-3-Clause
- **Source:** LICENSE.txt, SoMEF, GitHub API

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
- **OS Independent** - Pure Python package, works on any OS with Python
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
From setup.py dependencies and README:
- **numpy** - Data arrays
- **pandas** - Data manipulation
- **isodate** - Time format handling
- **hapiplot** - Visualization (optional)

### 31. Related Instruments (OPTIONAL)
- **Value:** Not specific instruments
- **Note:** The client can access data from any instrument whose data is served via a HAPI server

### 32. Related Observatories (OPTIONAL)
Examples from README and HAPI server listings:
- **OMNI** - Solar wind data (via CDAWeb HAPI)
- **CDAWeb** - NASA's space physics data facility
- **Note:** Many other observatories serve data via HAPI. See http://hapi-server.org/servers/

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/hapi-server/hapi-server.github.io/master/logos/HAPI.svg
- **Source:** PyHC registry

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
- ✅ **Software Functionality** - Data Access and Retrieval, Line Plots, Spectrogram
- ✅ **Related Region** - Earth Magnetosphere, Interplanetary Space, Solar Environment
- ✅ **Authors** - 4 authors identified with ORCID for primary author
- ✅ **Software Name** - hapiclient
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

1. **Version Discrepancy:** The latest Zenodo DOI is for v0.2.1 (2021), but the repository has v0.2.6 (2024) and development v0.2.7b1. Recommend updating Zenodo with recent releases.

2. **Related Regions:** The three regions selected (Earth Magnetosphere, Interplanetary Space, Solar Environment) represent the most common data types accessed via HAPI servers. Additional regions could be added if needed.

3. **Software Functionality:** The primary functionality is data access/retrieval. Plotting is a secondary feature provided by the optional hapiplot package.

4. **Reference Publication:** No primary publication found. Authors may want to consider publishing in JOSS or similar venue.

5. **ORCID Coverage:** Only the primary author (Bob Weigel) has an ORCID identified. Other contributors may benefit from having their ORCIDs linked.

6. **Documentation Quality:** Excellent documentation with README, Jupyter notebooks, and example scripts. Hosted on Google Colab for easy access.
