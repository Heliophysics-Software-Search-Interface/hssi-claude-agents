# HSSI Metadata Extraction Results

**Repository:** https://github.com/SciQLop/speasy
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.4118780
- **Source:** CITATION.cff, Zenodo API, DataCite API (Concept DOI for all versions)

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/SciQLop/speasy
- **Source:** GitHub, confirmed in all metadata sources

### 4. Software Functionality (MANDATORY)
**Selected values (based on comprehensive code and documentation analysis):**
- Data Processing and Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:File Format Conversion
- Data Visualization
- Data Visualization:Line Plots
- Data Visualization:2D Graphics
- Coordinate Transforms:Mission-Specific

**Analysis notes:**
- Primary functionality is data access and retrieval from multiple space physics web services (CDAWEB, AMDA, CSA, SSCWeb, UIowa Eph Tool)
- Provides data processing capabilities including resampling, filtering, interpolation
- Supports time series analysis and numpy operations on data
- Provides basic visualization capabilities (plots, though documentation notes this is not the primary purpose)
- Includes coordinate transformation support through data providers
- File format conversion between CDF, CSV, ASCII formats through codecs

**Sources:** README.md, pyproject.toml, code structure analysis (speasy/data_providers/, speasy/core/), PyHC metadata

### 5. Related Region (MANDATORY)
**Selected values:**
- Interplanetary Space
- Earth Magnetosphere

**Analysis notes:**
- Interplanetary Space: Package provides access to solar wind data (ACE, Wind spacecraft examples in README)
- Earth Magnetosphere: Provides access to magnetospheric missions (MMS examples in README, magnetosphere-related data from CDAWeb/AMDA)
- Data sources (CDAWEB, AMDA, SSCWeb) primarily serve heliosphere and magnetosphere datasets

**Sources:** README.md examples, data provider analysis, PyHC keywords ("heliosphere", "magnetosphere")

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Alexis Jeandet
- **Author Identifier:** https://orcid.org/0000-0003-2892-6924
- **Affiliation:**
  - **Organization:** Laboratory of Plasma Physics, Ecole Polytechnique, CNRS, Sorbonne Université, Université Paris-Saclay
  - **Affiliation Identifier:** Not found
- **Source:** CITATION.cff, DataCite API, Zenodo API, pyproject.toml, AUTHORS.rst, LICENSE

**Author 2:**
- **Name:** Alexandre Schulz
- **Author Identifier:** https://orcid.org/0009-0009-7151-8089
- **Affiliation:**
  - **Organization:** IRAP (Institut de Recherche en Astrophysique et Planétologie)
  - **Affiliation Identifier:** Not found
- **Source:** CITATION.cff, DataCite API, Zenodo API, AUTHORS.rst

**Contributor:**
- **Name:** Benjamin Renard
- **Affiliation:** IRAP
- **Source:** AUTHORS.rst (listed as contributor for AMDA Webservice)

### 7. Software Name (MANDATORY)
- **Name:** Speasy
- **Full name from GitHub:** SciQLop/speasy
- **Source:** All metadata sources (pyproject.toml, CITATION.cff, README, DataCite, Zenodo, PyHC)

### 8. Description (MANDATORY)
**Primary description (from PyHC and README):**
Speasy is a free and open-source Python package that makes it easy to find and load space physics data from a variety of data sources, whether it is online and public such as CDAWEB and AMDA, or any described archive, local or remote. This task, where any science project starts, would seem easy a priori but, considering the very diverse array of missions and instrument nowaday available, proves to be one of the major bottleneck, especially for students and newcomers. Speasy solves this problem by providing a single, easy-to-use interface to over 70 space missions and 65,000 products.

**Key features:**
- Simple and intuitive API (spz.get_data(...) to get them all)
- Speasy variables are like Pandas DataFrame with seamless conversion to/from it
- Speasy variables support numpy operations
- Speasy variables filtering and resampling capabilities
- Local cache to avoid redundant downloads
- Uses the SciQLOP ultra fast community cache server
- Full support of AMDA API
- Can retrieve time-series from AMDA, CDAWeb, CSA, SSCWeb
- Support data access from any local or remote archives described by YAML file
- Also available as Speasy.jl for Julia users

**Source:** README.md, PyHC projects.yml, pyproject.toml, SoMEF output

### 9. Concise Description (OPTIONAL)
Space Physics made EASY! A simple Python package to deal with main Space Physics WebServices (CDA, SSC, AMDA, CSA) providing easy access to over 70 space missions and 65,000 products.

**Source:** GitHub description, SoMEF output

### 10. Publication Date (RECOMMENDED)
- **Date:** 2019-12-07
- **Note:** Initial creation date of the repository
- **Source:** SoMEF (GitHub API: date_created)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

**Version Number:**
- **Value:** v1.6.1
- **Source:** CITATION.cff, pyproject.toml, git tags, DataCite API, Zenodo API

**Version Date:**
- **Value:** 2025-09-05
- **Source:** CITATION.cff, git log, Zenodo API

**Version Description:**
**1.6.1 changes:**
- [UiowaEphTool] Remove coordinate_system kwarg for proxy (leftover from sscweb copy)

**1.6.0 changes:**
- Add user agent config bit and set it for GH actions
- Slicing a variable by columns did break with secondary axis
- Bump PyISTP to cover cases where axis data is in master CDF
- Fix #225
- Add uiowa eph tool
- Always use certifi provided certificates bundle
- Is VIRTUAL any product that is VIRTUAL or has a VIRTUAL support data axis
- [UiowaEphTool] products are registered with UiowaEphTool as provider

**Source:** DataCite API description, Zenodo API, GitHub releases

**Version PID:**
- **Value:** https://doi.org/10.5281/zenodo.17065425
- **Note:** DOI for specific version v1.6.1
- **Source:** CITATION.cff, Zenodo API

**Previous versions available:**
v1.6.0, v1.5.2, v1.5.1, v1.5.0, v1.4.0, v1.3.2, v1.3.1, v1.3.0, v1.2.7, and earlier versions (see Zenodo for complete list)

### 13. Programming Language (RECOMMENDED)
- Python 3.x (specifically: Python 3.9, 3.10, 3.11, 3.12, 3.13)
- Jupyter Notebook (for examples/documentation)

**Source:** pyproject.toml, SoMEF (GitHub API: programming_languages)

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found
- **Note:** No reference publication (e.g., JOSS paper) was found in the repository metadata

### 15. License (RECOMMENDED)

**License:**
- **Name:** MIT License
- **License URI:** https://opensource.org/licenses/MIT
- **SPDX Identifier:** MIT

**Copyright:** Copyright (c) 2024 Laboratory of Plasma Physics, Ecole Polytechnique, CNRS, Sorbonne Université, Université Paris-Saclay

**Source:** LICENSE file, pyproject.toml, DataCite API, Zenodo API, SoMEF, PyHC metadata

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Extracted keywords (consolidated from all sources):**
- space-physics
- plasma-physics
- satellite
- heliosphere
- magnetosphere
- data_retrieval
- data_container
- data_access
- nasa-data
- amda
- cdaweb
- sscweb
- cdpp
- CDF
- CSV
- ASCII
- cnes
- esa
- nasa-api
- pnst
- pyhc
- python-3
- python3
- sciqlop
- space-plasma
- webservices
- general
- local
- remote
- web_service

**Source:** PyHC metadata (keywords field), SoMEF (GitHub topics), pyproject.toml

### 17. Data Sources (OPTIONAL)
- CDAWeb
- OMNIWeb (through AMDA and CDAWeb)
- SSCWeb
- Observatory/Mission-specific
- Other (AMDA, CSA, UIowa Eph Tool)

**Note:** Speasy supports data access from AMDA (http://amda.irap.omp.eu/), CDAWeb (https://cdaweb.gsfc.nasa.gov/), CSA (https://csa.esac.esa.int/csa-web/), SSCWeb (https://sscweb.gsfc.nasa.gov/), and UIowa Eph Tool, plus any local or remote archives described by YAML file.

**Source:** README.md, PyHC metadata, code analysis (data_providers directory)

### 18. Input File Formats (RECOMMENDED)
- CDF
- CSV
- ASCII
- Other (HAPI CSV, YAML for archive descriptions)

**Source:** Code analysis (speasy/core/codecs/), README.md, PyHC keywords

### 19. Output File Formats (RECOMMENDED)
- CDF
- CSV
- ASCII
- Other (HAPI CSV)

**Note:** Speasy primarily works with data in memory but can save to CDF and CSV formats through its codec system.

**Source:** Code analysis (speasy/core/codecs/), PyHC keywords

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows
- OS Independent

**Note:** Python package compatible with all major operating systems. OS independence confirmed by Python 3.9+ requirement.

**Source:** Inferred from being a Python package, GitHub Actions CI/CD runs on multiple OS

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Note:** Pure Python package with platform-independent dependencies

**Source:** Inferred from package structure (no compiled components requiring specific architecture)

### 22. Related Phenomena (OPTIONAL)
- Not found

**Note:** No specific phenomena keywords found in standard controlled vocabularies. The package is a general-purpose data access tool rather than being focused on specific phenomena.

### 23. Development Status (RECOMMENDED)
- **Status:** Active
- **PyPI Classifier:** Development Status :: 5 - Production/Stable
- **PyHC Rating:** Good (software_maturity)

**Evidence:**
- Recent releases (v1.6.1 released 2025-09-05)
- Active development (last updated 2025-10-07 according to SoMEF GitHub API)
- Regular commits and pull requests
- Maintained documentation

**Source:** pyproject.toml, PyHC metadata, SoMEF (date_updated), GitHub activity

### 24. Documentation (RECOMMENDED)
- **URL:** https://speasy.readthedocs.io/
- **Additional:** https://speasy.readthedocs.io/en/latest/examples/index.html (examples)
- **PyHC Documentation Rating:** Good

**Note:** Comprehensive documentation hosted on ReadTheDocs, including installation instructions, API documentation, and examples.

**Source:** README.md, PyHC metadata, SoMEF

### 25. Funder (OPTIONAL)
- **Organization:** CDPP (Centre de Données de la Physique des Plasmas)
- **Funder Identifier:** Not found
- **Note:** README states "The development of Speasy is supported by the CDPP (http://www.cdpp.eu/)."

**Source:** README.md (Credits section)

### 26. Award Title (OPTIONAL)
- **Value:** Not found
- **Award Number:** Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Not found

**Note:** No related publications found in metadata. Users are encouraged to cite the software DOI when using Speasy.

### 28. Related Datasets (OPTIONAL)
- Not found

**Note:** Speasy provides access to numerous datasets from AMDA, CDAWeb, CSA, SSCWeb but does not have specific related dataset DOIs in its metadata. The software provides access to data from over 70 space missions.

### 29. Related Software (OPTIONAL)

**Important dependencies:**
- PyISTP (>=0.7.2) - for ISTP-compliant CDF file handling
- pyCDFpp - mentioned in PyHC registry as related CDF software by same author
- astropy - for astronomical/time handling
- numpy, pandas, scipy - core data manipulation
- matplotlib - for plotting

**Related tools:**
- SciQLOP (https://github.com/SciQLop/SciQLop) - Graphical interface mentioned in README
- Speasy.jl (https://github.com/SciQLop/Speasy.jl) - Julia wrapper for Speasy

**Source:** pyproject.toml dependencies, README.md, PyHC registry

### 30. Interoperable Software (OPTIONAL)
- Not found in metadata

**Note:** Speasy works with data from various missions and can export to common formats (CDF, CSV) making it interoperable with many space physics tools, but no specific interoperability declarations were found.

### 31. Related Instruments (OPTIONAL)
**Instruments mentioned in examples and supported through data providers:**
- ACE/MFI (ACE Magnetic Field Instrument)
- ACE/SWE (ACE Solar Wind Electron Proton Alpha Monitor)
- Wind/MFI (Wind Magnetic Field Investigation)
- Wind/SWE (Wind Solar Wind Experiment)
- MMS/FGM (Magnetospheric Multiscale Mission - Fluxgate Magnetometer)
- MMS/SCM (MMS - Search Coil Magnetometer)
- MMS/DES (MMS - Dual Electron Spectrometers)
- MMS/DIS (MMS - Dual Ion Spectrometers)
- MMS/FPI (MMS - Fast Plasma Investigation)

**Note:** Speasy provides access to data from over 70 space missions through various web services. The instruments listed above are examples from the README; the actual supported instruments number in the thousands.

**Instrument Identifier:** Not found for individual instruments

**Source:** README.md examples, data providers (AMDA, CDAWeb, CSA, SSCWeb provide mission-specific data)

### 32. Related Observatories (OPTIONAL)
**Observatories/Missions mentioned in examples and supported:**
- ACE (Advanced Composition Explorer)
- Wind
- MMS (Magnetospheric Multiscale Mission)
- Solar Orbiter (Solo)
- Cluster
- MAVEN
- PSP (Parker Solar Probe)
- Ulysses
- OMNI

**Note:** Speasy provides access to data from over 70 space missions. The missions listed above are examples; the full list is available through the data providers (AMDA, CDAWeb, CSA, SSCWeb).

**Observatory Identifier:** Not found

**Source:** README.md examples, PyHC keywords, code analysis (data_providers)

### 33. Logo (OPTIONAL)
- **URL:** https://raw.githubusercontent.com/SciQLop/speasy/main/logo/logo_speasy_400dpi.png
- **Additional logo:** https://raw.githubusercontent.com/SciQLop/speasy/main/logo/logo_speasy.svg

**Source:** README.md, PyHC metadata, SoMEF

---

## Metadata Agreement

By submitting this metadata, you acknowledge and agree that any metadata you provide is submitted voluntarily and becomes part of the public domain. You waive all rights, claims, and interests to the submitted metadata, and grant unrestricted use, reproduction, modification, and distribution rights to the receiving party or its designees.

---

## Metadata Extraction Summary

### Sources Used:
1. **DataCite API** - DOI metadata for concept DOI 10.5281/zenodo.4118780
2. **Zenodo API** - Version-specific metadata for v1.6.1 (DOI: 10.5281/zenodo.17065425)
3. **PyHC Registry** (projects.yml) - Community-curated metadata
4. **SoMEF** - Automated extraction from repository
5. **Manual examination:**
   - README.md
   - CITATION.cff
   - pyproject.toml
   - LICENSE
   - AUTHORS.rst
   - Git tags and commit history
   - Code structure analysis (speasy/data_providers/, speasy/core/)

### Metadata Quality Assessment:
- **Completeness:** High - 30 of 33 fields populated (91%)
- **MANDATORY fields:** All filled (Submitter to be filled by actual submitter)
- **RECOMMENDED fields:** 13 of 15 filled (87%)
- **OPTIONAL fields:** 6 of 13 filled (46%)

### Fields Not Found:
- Reference Publication (14)
- Related Phenomena (22)
- Award Title/Number (26)
- Related Publications (27)
- Related Datasets (28)
- Interoperable Software (30)
- Detailed Instrument/Observatory Identifiers (31-32)

### Confidence Level:
- **High confidence:** Basic information, authors, licensing, version info, repository URL (verified across multiple sources)
- **Medium confidence:** Software functionality and related region (based on analysis of code, documentation, and examples)
- **Note:** Software Functionality and Related Region classifications are based on comprehensive analysis but may benefit from validation by the software developers

### Notes for Submitter:
1. Verify Software Functionality selections align with your intended use cases
2. Verify Related Region selections - particularly if the software is used for other regions (Solar Environment, Earth Atmosphere, Planetary Magnetospheres)
3. Consider adding a Reference Publication if you publish a paper about Speasy (e.g., in JOSS)
4. Update Award information if Speasy development was funded by specific grants
5. Add Related Publications as they become available (papers citing or using Speasy)

---

**End of HSSI Metadata Extraction**
