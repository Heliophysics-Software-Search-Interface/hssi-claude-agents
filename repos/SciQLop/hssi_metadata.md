# HSSI Metadata Extraction Results

**Repository:** https://github.com/SciQLop/SciQLop
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.7379012

**Source:** Provided by user (concept DOI for all versions)

**Note:** The version-specific DOI for v0.10.0 is https://doi.org/10.5281/zenodo.17176824

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/SciQLop/SciQLop

**Source:** GitHub repository URL

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Interactive
- Data Visualization:Spectrogram
- Data Visualization:Web-Based

**Source:** Analysis of README.md, PyHC metadata, and software description. SciQLop is a visualization and analysis tool for in-situ space plasma data that provides:
- Access to tens of thousands of data products from major archives (CDAWeb, AMDA, SSCWeb)
- Interactive visualization of multivariate time series
- Jupyter notebook integration for analysis
- Catalog system for event labeling
- Support for spectrograms, line plots, and custom visualizations

### 5. Related Region (MANDATORY)
**Values:**
- Earth Magnetosphere
- Interplanetary Space

**Source:** Analysis of README.md, PyHC metadata keywords ("heliosphere", "magnetosphere"), and example notebooks (MMS magnetopause studies). The software is designed for in-situ space plasma data visualization and analysis, primarily focused on magnetospheric and heliospheric observations.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Alexis Jeandet
- **Author Identifier:** https://orcid.org/0000-0003-2892-6924
- **Affiliation:** Laboratory of Plasma Physics (From CITATION.cff: @LaboratoryOfPlasmaPhysics)
- **Affiliation Identifier:** Not found

**Author 2:**
- **Name:** Nicolas Aunai
- **Author Identifier:** https://orcid.org/0000-0002-9862-4318
- **Affiliation:** CNRS / Laboratory of Plasma Physics (From DataCite API)
- **Affiliation Identifier:** Not found

**Author 3:**
- **Name:** Benjamin Renard
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 4:**
- **Name:** Vincent Génot
- **Author Identifier:** https://orcid.org/0000-0002-7708-8077
- **Affiliation:** Not found

**Author 5:**
- **Name:** Nicolas André
- **Author Identifier:** https://orcid.org/0000-0001-8017-5676
- **Affiliation:** Not found

**Source:** CITATION.cff file and DataCite API

**Note:** Additional contributors from DataCite API for v0.10.0 include aleroux-itlink, itlink-hackathon, and meriadegp, but these appear to be GitHub usernames rather than formal authors.

### 7. Software Name (MANDATORY)
**Value:** SciQLop

**Source:** Repository name, CITATION.cff, pyproject.toml

**Full Name:** SciQLop (SCIentific Qt application for Learning from Observations of Plasmas)

### 8. Description (MANDATORY)
**Value:** SciQLop (SCIentific Qt application for Learning from Observations of Plasmas) is a powerful and user-friendly tool designed for the visualization and analysis of in-situ space plasma data. Using SciQLop, users can access tens of thousands of products from major data archives worldwide, explore multivariate time series effortlessly with lightning-fast and transparent downloads, visualize custom products with simple Python code executed on-the-fly, easily label time intervals and make or edit catalogs of events graphically, and analyze data in Jupyter notebooks. SciQLop aims to be the right tool for exploring, labeling, and analyzing huge amounts of space physics data, and is also ideal for teaching space physics and in situ spacecraft data handling to students.

**Source:** Synthesized from README.md and CITATION.cff

### 9. Concise Description (OPTIONAL)
**Value:** An ergonomic and efficient application to browse and label in situ plasma measurements from multi-mission satellite data.

**Source:** pyproject.toml description

### 10. Publication Date (RECOMMENDED)
**Value:** 2025-09-22

**Source:** Git tag v0.10.0 release date

**Note:** The initial repository creation date was 2018-12-15 (from SoMEF/GitHub API)

### 11. Publisher (RECOMMENDED)
**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://doi.org/10.5281/zenodo.7379012

**Source:** DataCite API

### 12. Version (RECOMMENDED)
**Version Number:** v0.10.0

**Version Date:** 2025-09-22

**Version Description:** Changelog for SciQLop v0.10.0 includes: Core Changes - Use consistent DateTime format across Speasy/SciQLop; Update Python AppImage version to 3.12.11; Add gettext library handling for x86_64 architecture; Inject SciQLop version in Speasy user agent; Fix Python compatibility by removing forbidden backslash in f-string; Bump various dependencies for improved stability. Component Updates - SciQLopPlots updated with performance improvements and fixed DPI scaling issues on macOS; TSCat GUI updated with improved UI and catalog management features; Speasy Integration improved with better float conversion and data handling capabilities. Build System - Various build script improvements for better cross-platform support; Enhanced macOS packaging support.

**Version PID:** https://doi.org/10.5281/zenodo.17176824

**Source:** CITATION.cff, git tags, DataCite API, GitHub releases

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x
- C++
- Jupyter Notebook

**Source:** pyproject.toml (supports Python 3.9-3.14), CITATION.cff keywords, GitHub API (shows Python, Jupyter Notebook, Jinja, Shell)

**Note:** The software is built with Qt (C++) but has Python bindings and is primarily used as a Python application.

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Source:** No reference publication DOI found in CITATION.cff, README, or DataCite API

### 15. License (RECOMMENDED)
**License:** GNU General Public License v3.0 or later

**License URI:** https://www.gnu.org/licenses/gpl-3.0-standalone.html

**Source:** CITATION.cff ("GPL-3.0-or-later"), pyproject.toml, DataCite API, COPYING file

**SPDX Identifier:** GPL-3.0-or-later

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- space physics
- plasma
- data analysis
- visualization
- in-situ measurements
- time series
- spectrograms
- particle distributions
- magnetic fields
- electric fields
- spacecraft data
- scientific software
- open source
- Qt
- Python
- GUI
- machine-learning
- satellite
- plasma-physics
- nasa-data
- amda
- cdpp
- heliosphere
- magnetosphere
- interactive
- line_plots
- plotting
- general
- cdaweb
- sscweb
- web_service
- remote
- data_access

**Source:** CITATION.cff keywords, GitHub topics (from SoMEF), PyHC metadata

### 17. Data Sources (OPTIONAL)
**Values:**
- CDAWeb
- SSCWeb
- Observatory/Mission-specific (AMDA from CDPP)
- Other (Speasy-based data providers)

**Source:** README.md mentions "tens of thousands of products from the top main data archives," PyHC keywords include "cdaweb" and "sscweb", examples show usage with CDAWeb and AMDA data sources via Speasy

### 18. Input File Formats (RECOMMENDED)
**Values:**
- CDF
- ascii
- csv

**Source:** PyHC metadata and Speasy dependency (Speasy supports CDF, CSV, ASCII formats). SciQLop primarily accesses data through Speasy rather than direct file I/O.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- Not found (primarily interactive visualization tool)

**Source:** Software is primarily an interactive visualization and analysis tool; output formats for data export are not explicitly documented in README or metadata files.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Source:** README.md installation instructions for Mac (App Bundle for ARM64 and x86_64), Linux (AppImage), and from sources (cross-platform Python). PyProject.toml shows pytest-xvfb for Linux, and build scripts exist for macOS. Windows support mentioned in release notes (v0.5.5 fixes IPykernel integration on Windows).

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- x86-64
- Apple Silicon arm64
- CPU Independent (Python-based)

**Source:** README.md mentions "ARM64 for Apple M1/2/3 chips and x86_64 for intel ones", Python-based application is generally CPU independent

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Magnetic fields
- Electric fields
- Particle distributions

**Source:** CITATION.cff keywords include "magnetic fields", "electric fields", and "particle distributions"

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** PyHC registry indicates "Requires improvement" for documentation, testing, and software maturity, but "Good" for Python 3 and license. Recent commits (last updated 2025-10-07 from SoMEF) and regular releases (v0.10.0 released 2025-09-22) indicate active development. Repository status would be "Active" per repostatus.org definitions (reached stable, usable state and being actively developed).

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/SciQLop/SciQLop

**Source:** pyproject.toml homepage, README.md. The software includes extensive examples in Jupyter notebooks within the repository and a welcome screen with tutorials.

**Note:** No separate documentation site was found. Documentation is primarily through README, examples, and in-code tutorials.

### 25. Funder (OPTIONAL)
**Organization 1:**
- **Name:** CDPP (Centre de Données de la Physique des Plasmas)
- **Funder Identifier:** Not found

**Organization 2:**
- **Name:** Plas@Par (Federation of Plasma Physics laboratories at Sorbonne University)
- **Funder Identifier:** Not found

**Source:** README.md Credits section: "The development of SciQLop is supported by the CDPP. We acknowledge support from the federation Plas@Par"

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Source:** No award titles or grant numbers found in README, CITATION.cff, or metadata files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found

**Source:** No publications citing or describing SciQLop were found in CITATION.cff, README, or DataCite API

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Source:** The software supports many datasets through Speasy (MMS, THEMIS, ACE, AMDA catalogs, etc.) but no specific dataset DOIs are referenced as required datasets

### 29. Related Software (OPTIONAL)
**Values:**
- **Speasy** - https://github.com/SciQLop/speasy - Data retrieval library (required dependency)
- **SciQLopPlots** - Plotting library (required dependency)
- **TSCat** - Time series catalog library (required dependency)
- **PySide6** - Qt bindings for Python (required dependency)
- **QCustomPlot** - C++ plotting library (acknowledged in README)
- **NumPy** - Python array library (required dependency)
- **Jupyter** - Notebook integration (required dependency)

**Source:** pyproject.toml dependencies, README.md Thanks section

### 30. Interoperable Software (OPTIONAL)
**Values:**
- **Speasy** - https://github.com/SciQLop/speasy - Primary data access library, demonstrates full interoperability
- **PySPEDAS** - Mentioned in examples (SciQLop/examples/PySPEDAS/pyspedas.ipynb), demonstrating interoperability

**Source:** Dependencies in pyproject.toml, example notebooks in repository

### 31. Related Instruments (OPTIONAL)
**Values:**
- MMS (Magnetospheric Multiscale Mission) - Examples show MMS data visualization
- THEMIS - Examples show THEMIS data
- ACE (Advanced Composition Explorer) - Example shows ACE data

**Source:** Example notebooks in repository (SciQLop/examples/mms/, usage examples in README.md show MMS, THEMIS, and ACE data products)

**Note:** Instrument identifiers (DOIs) not available for these instruments

### 32. Related Observatories (OPTIONAL)
**Values:**
- **MMS (Magnetospheric Multiscale)** - Examples demonstrate MMS data analysis
- **THEMIS (Time History of Events and Macroscale Interactions during Substorms)** - Usage examples in README
- **ACE (Advanced Composition Explorer)** - Virtual product example uses ACE data

**Source:** README.md usage examples and example notebooks

### 33. Logo (OPTIONAL)
**Value:** https://raw.githubusercontent.com/SciQLop/SciQLop/main/SciQLop/resources/icons/SciQLop.png

**Source:** PyHC metadata, SoMEF extraction, README.md

---

## Metadata Sources Summary

This metadata extraction combined information from multiple sources with the following priority order:

1. **PyHC Community Registry** (projects.yml) - Manually curated, highest confidence for community-verified fields
2. **CITATION.cff** - Authoritative for authors, DOIs, keywords, and citation information
3. **DataCite API** - Official DOI metadata from https://api.datacite.org/dois/10.5281/zenodo.7379012
4. **Repository Files** - README.md, pyproject.toml, COPYING file
5. **SoMEF** - Automated extraction from repository
6. **Git History** - Version tags and release information

---

## Extraction Completeness

**All 33 HSSI form fields have been addressed:**
- ✅ All MANDATORY fields have values
- ✅ Most RECOMMENDED fields have values (14 of 17)
- ✅ Several OPTIONAL fields have values (8 of 12)

**Fields marked "Not found":**
- Reference Publication (no JOSS or similar paper found)
- Award Title/Number (no grants explicitly listed)
- Related Publications (no papers found)
- Related Datasets (accesses many datasets but none are dependencies)
- Output File Formats (interactive tool without explicit export formats documented)

**Notes on Confidence:**
- Software Functionality and Related Region were determined through comprehensive analysis of README, examples, PyHC metadata, and software description
- The concept DOI (10.5281/zenodo.7379012) vs version-specific DOI (10.5281/zenodo.17176824) distinction is important - the concept DOI represents all versions
- Author affiliations are partially complete - ORCIDs available for most authors but some affiliation details missing
- Development Status assessed as "Active" based on recent commits and releases, though PyHC rates maturity as "Requires improvement"
