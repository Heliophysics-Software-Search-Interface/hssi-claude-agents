# HSSI Metadata Extraction Results

**Repository:** https://github.com/swxsoc/swxsoc
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.15546486
- **Source:** Zenodo concept DOI (all versions)

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/swxsoc/swxsoc
- **Source:** GitHub repository

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Processing
- Data Visualization
- Data Visualization:Line Plots
- Mission-related
- Mission-related:Analysis
- Mission-related:Processing

**Source:** Code analysis - package provides SWXData container class for time series data processing, CDF file I/O, data visualization (plot methods), and mission-specific tools for SWxSOC/HERMES instruments.

### 5. Related Region (MANDATORY)
- Solar Environment
- Interplanetary Space

**Source:** Package description indicates space weather data processing, and HERMES keyword indicates solar observations. Space weather originates from solar environment and propagates through interplanetary space.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Steven Christe
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** NASA Goddard Space Flight Center
  - **Affiliation Identifier:** Not found

**Author 2:**
- **Name:** Damian Barrous Dumme
- **Email:** damianbarrous@gmail.com
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Navteca
  - **Affiliation Identifier:** Not found

**Author 3:**
- **Name:** Andrew Robbertz
- **Email:** a.robbertz@gmail.com
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** pyproject.toml, DataCite API, and Zenodo API

### 7. Software Name (MANDATORY)
- **Name:** swxsoc
- **Source:** Repository name, PyHC registry, pyproject.toml

### 8. Description (MANDATORY)
A Python package to support the SWxSOC instrument packages. This package provides core functionality for all SWxSOC Mission Packages, including pipeline and analysis tools for space weather data processing. The package provides a generic object (SWXData) for loading, storing, and manipulating space weather time series data with support for ISTP-compliant CDF files.

**Source:** Combined from pyproject.toml description, GitHub API description, PyHC registry, and code documentation

### 9. Concise Description (OPTIONAL)
Core functionality package for SWxSOC mission providing data processing and analysis tools for space weather instruments.

**Source:** Derived from descriptions

### 10. Publication Date (RECOMMENDED)
- **Date:** 2024-11-27
- **Source:** Git tag for version 0.1.0 (first release)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API

### 12. Version (RECOMMENDED)

**Latest Version:**
- **Version Number:** 0.2.2
- **Version Date:** 2025-06-07
- **Version Description:** Update Parfive Requirement - Updated parfive dependency version
- **Version PID:** https://doi.org/10.5281/zenodo.15615510

**Source:** Git tags, Zenodo API, GitHub release notes

### 13. Programming Language (RECOMMENDED)
- Python 3.x

**Note:** Package requires Python >= 3.9 and is tested on Python 3.9, 3.10, 3.11, 3.12, and 3.13

**Source:** pyproject.toml, GitHub workflows, SoMEF

### 14. Reference Publication (RECOMMENDED)
- **DOI:** Not found

**Note:** No reference publication found in repository

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** http://www.apache.org/licenses/LICENSE-2.0

**Note:** The repository license file (licenses/LICENSE.md) contains Apache License 2.0. However, Zenodo DOI metadata indicates cc-by-4.0 license for the archived versions. The code license is Apache 2.0.

**Source:** Repository licenses/LICENSE.md file, DataCite API (shows cc-by-4.0 for Zenodo deposit)

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- swxsoc
- nasa mission
- space weather
- general
- data_container
- cdf
- data_analysis
- hermes

**Source:** pyproject.toml keywords field and PyHC registry

### 17. Data Sources (OPTIONAL)
- Other

**Note:** Package provides data retrieval functionality (SWXSOCClient, Grafana API integration mentioned in release notes) but specific data sources not clearly documented. Package supports S3/cloud storage via boto3 dependency.

**Source:** Code analysis, pyproject.toml dependencies

### 18. Input File Formats (RECOMMENDED)
- CDF
- ISTP-Compliant

**Source:** Code analysis - CDFHandler class in util/io.py reads CDF files, SWXSchema enforces ISTP compliance

### 19. Output File Formats (RECOMMENDED)
- CDF
- ISTP-Compliant

**Source:** Code analysis - CDFHandler class in util/io.py writes CDF files, SWXSchema enforces ISTP compliance

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source:** GitHub workflows testing.yml shows testing on ubuntu-latest, macos-latest, and windows-latest

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Note:** Python package with no architecture-specific requirements

**Source:** Package metadata and testing configuration

### 22. Related Phenomena (OPTIONAL)
- Not found

**Note:** No specific phenomena keywords found in standard vocabularies. Package is general-purpose for space weather data.

### 23. Development Status (RECOMMENDED)
- **Status:** Active

**Source:** PyHC registry shows "Good" ratings across all categories, recent commits (last updated 2025-09-15 per SoMEF), and active releases. Repository status is Active based on ongoing development and maintenance.

### 24. Documentation (RECOMMENDED)
- **URL:** https://swxsoc.readthedocs.io/en/latest/
- **Alternative URL:** https://swxsoc.readthedocs.io/

**Source:** pyproject.toml, PyHC registry, SoMEF, README.rst

### 25. Funder (OPTIONAL)
- Not found

**Note:** No funding information found in repository or DOI metadata

### 26. Award Title (OPTIONAL)
- Not found

**Note:** No award information found in repository or DOI metadata

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Not found

**Note:** No publications found that cite or describe this software

### 28. Related Datasets (OPTIONAL)
- Not found

**Note:** No specific dataset DOIs referenced in repository

### 29. Related Software (OPTIONAL)

**Dependencies (from pyproject.toml):**
- sammi-cdf (>=0.1.2) - Share Attribute and Metadata Management Interface for CDF files
- astropy (>=5.3.3)
- numpy (>=1.18.0)
- sunpy[all] (>=5.0.1)
- spacepy (>=0.5.0)
- ndcube (>=2.2.0)
- parfive (>=2.1.0)
- pyyaml (>=5.3.1)
- boto3 (>=1.35.26)

**Note:** Major dependencies include sunpy ecosystem packages. Package template based on OpenAstronomy/SunPy Project templates.

**Source:** pyproject.toml dependencies, README.rst acknowledgements

### 30. Interoperable Software (OPTIONAL)
- sunpy - https://github.com/sunpy/sunpy (dependency and interoperable)
- ndcube - https://github.com/sunpy/ndcube (dependency and interoperable)
- astropy - https://github.com/astropy/astropy (dependency and interoperable)

**Source:** Package dependencies indicate interoperability with SunPy ecosystem

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** HERMES

**Note:** PyHC keywords include "hermes", and package description mentions SWxSOC instrument packages. HERMES (Heliophysics Environmental and Radiation Measurement Experiment Suite) is a NASA mission.

**Source:** PyHC registry keywords, package descriptions

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** HERMES
- **Observatory Name:** SWxSOC (Space Weather Science Operation Center)

**Source:** Package name (swxsoc), descriptions, and PyHC keywords

### 33. Logo (OPTIONAL)
- **URL:** https://raw.githubusercontent.com/swxsoc/swxsoc/fbbc26e70863f8acc4df53dee4876a40b5cca154/docs/logo/swxsoc_logo.png

**Source:** PyHC registry

---

## Additional Notes

### Metadata Quality Sources (Priority Order)
1. **PyHC Registry** - Manually curated community metadata (highest priority for certain fields)
2. **Repository Files** - pyproject.toml, README.rst, LICENSE files
3. **Zenodo/DataCite APIs** - Official DOI metadata
4. **SoMEF** - Automated extraction from repository
5. **Code Analysis** - Direct examination of source code

### Key Findings
- Package is part of the Python in Heliophysics Community (PyHC) with "Good" ratings across all quality metrics
- Active development with regular releases (0.1.0 to 0.2.2 between Nov 2024 and Jun 2025)
- Strong integration with SunPy ecosystem
- Mission-specific for SWxSOC/HERMES instruments
- Follows ISTP compliance standards for space physics data
- Comprehensive testing across multiple Python versions and operating systems

### Items Requiring User Input
- Submitter name and email
- ORCIDs for authors (if available)
- ROR identifiers for affiliations (if available)
- Funding information (if applicable)
- Award information (if applicable)
- Reference publication (if one exists or is planned)

### Potential Improvements to Repository
- Add CITATION.cff file with author ORCIDs
- Add funding acknowledgments if applicable
- Consider adding a reference publication DOI when available
- Clarify license discrepancy between repository (Apache 2.0) and Zenodo deposits (CC-BY-4.0)
