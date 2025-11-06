# HSSI Metadata Extraction Results

**Repository:** https://github.com/rstoneback/pysatCDF (redirects to https://github.com/pysat/pysatCDF)
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.1217180
- **Source:** User-provided; verified in README.md badge and DataCite API

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/pysat/pysatCDF
- **Source:** SoMEF GitHub API (repository moved from rstoneback/pysatCDF to pysat/pysatCDF)

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion

**Rationale:** pysatCDF is a Python reader for NASA CDF (Common Data Format) files. It provides data access by loading CDF files into Python and converts CDF format to Python dictionaries and pysat data structures.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space

**Rationale:** Based on PyHC keywords (ionosphere_thermosphere_mesosphere, magnetosphere) and the widespread use of CDF format across space physics missions. CDF is a standard format for satellite data in these regions.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Russell Stoneback
- **Author Identifier:** https://orcid.org/0000-0001-7216-4336
- **Affiliation:** Stoneris

**Author 2:**
- **Name:** Matthew Depew
- **Author Identifier:** Not found
- **Affiliation:** The University of Texas at Dallas

**Author 3:**
- **Name:** Jeffrey Klenzing
- **Author Identifier:** https://orcid.org/0000-0001-8321-6074
- **Affiliation:** Goddard Space Flight Center

**Author 4:**
- **Name:** Gayatri Iyer
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 5:**
- **Name:** Asher Pembroke
- **Author Identifier:** Not found
- **Affiliation:** Predictive Science

**Author 6:**
- **Name:** Greg Starr
- **Author Identifier:** https://orcid.org/0000-0002-3487-3630
- **Affiliation:** The Johns Hopkins Applied Physics Laboratory

**Author 7:**
- **Name:** Ashton Reimer
- **Author Identifier:** https://orcid.org/0000-0002-4621-3453
- **Affiliation:** SRI International

**Source:** DataCite API

### 7. Software Name (MANDATORY)
- **Name:** pysatCDF
- **Source:** DataCite API, SoMEF, PyHC registry

### 8. Description (MANDATORY)
**Description:**
pysatCDF is a self-contained Python reader for NASA's Common Data Format (CDF) files. It uses standard and extended Fortran CDF interfaces to load CDF files into Python. The package provides simple, robust access to CDF data and simplifies adding instruments to pysat. It includes the NASA CDF libraries and supports reading CDF files, accessing variable data and metadata, and exporting data to pysat data and metadata format.

**Source:** Combined from README.md, SoMEF description, and PyHC registry

### 9. Concise Description (OPTIONAL)
**Concise Description:**
Python reader for NASA CDF file format

**Source:** SoMEF GitHub API description

### 10. Publication Date (RECOMMENDED)
- **Date:** 2016-02-15
- **Source:** SoMEF GitHub API (repository creation date)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API

### 12. Version (RECOMMENDED)

**Latest Version:**
- **Version Number:** v0.3.2
- **Version Date:** 2022-05-12
- **Version Description:** Compatible with pysat v3.0+. Added pull request templates and other GitHub project documentation. Switched Windows installation instructions to favor installing WSL. Improved builds for newer compilers. Replaces uninterpretable characters with '*' so data loading may continue. Adopted latest pysat development standards. Shifted from TravisCI to GitHub Actions for online testing. Adopted setup.cfg. Improved PEP8 compliance.
- **Version PID:** https://doi.org/10.5281/zenodo.6544438

**Source:** DataCite API, CHANGELOG.md, Git tags

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- C
- Fortran77

**Source:** SoMEF GitHub API shows primary languages are C (6.1 MB), Fortran (204 KB), and Python (40 KB). Setup.py shows Python is the interface language with Fortran77/C for CDF library. The Fortran code uses fixed-form format (.f extension) and is compiled with `--std=legacy` flag (setup.py:194).

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication:** Not found
- **Note:** No reference publication DOI found in DataCite metadata or repository files

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://api.github.com/licenses/bsd-3-clause
- **SPDX ID:** BSD-3-Clause
- **Source:** SoMEF, LICENSE file

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- cdf
- nasa-cdf
- python
- python-reader
- ionosphere_thermosphere_mesosphere (from PyHC)
- magnetosphere (from PyHC)

**Source:** SoMEF GitHub API topics, PyHC registry

### 17. Data Sources (OPTIONAL)
- Not found
- **Note:** pysatCDF reads local CDF files; it does not connect to specific data sources

### 18. Input File Formats (RECOMMENDED)
- CDF (Common Data Format)

**Source:** README.md, package description

### 19. Output File Formats (RECOMMENDED)
- Python dictionaries (in-memory)
- pysat format (Python objects)

**Source:** README.md example code showing cdf.data dictionaries and cdf.to_pysat() export

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows (via Windows Subsystem for Linux)

**Source:** README.md states "tested on Mac OS X and Ubuntu 15.04" and "Support is included for building on windows via Windows Subsystem for Linux." GitHub Actions workflow shows testing on ubuntu-latest.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- CPU Independent

**Source:** Inferred from supported operating systems and lack of architecture-specific requirements in documentation

### 22. Related Phenomena (OPTIONAL)
- Not found
- **Note:** As a general-purpose CDF reader, this software doesn't target specific phenomena

### 23. Development Status (RECOMMENDED)
- **Status:** Active
- **Source:** PyHC registry shows "Good" for software_maturity. Repository shows recent activity (last updated 2025-07-16 per SoMEF).

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** Not found
- **Note:** No dedicated documentation site found. README.md provides basic usage examples. PyHC registry shows "Requires improvement" for documentation quality.

### 25. Funder (OPTIONAL)
- Not found
- **Source:** No funding information in DataCite metadata

### 26. Award Title (OPTIONAL)
- Not found
- **Source:** No award information in DataCite metadata

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Not found
- **Source:** No related publications found in DataCite metadata

### 28. Related Datasets (OPTIONAL)
- Not found
- **Source:** No related datasets found in DataCite metadata

### 29. Related Software (OPTIONAL)
- **pysat:** https://github.com/pysat/pysat
  - **Relationship:** pysatCDF is designed to work with pysat for loading instrument data
  - **Source:** README.md, requirements.txt (pysat>=3.0)

### 30. Interoperable Software (OPTIONAL)
- **pysat:** https://github.com/pysat/pysat
  - **Source:** Requirements.txt shows pysat>=3.0 as a dependency; designed for integration

### 31. Related Instruments (OPTIONAL)
- Not found
- **Note:** As a general CDF reader, it supports data from any instrument that uses CDF format rather than specific instruments

### 32. Related Observatories (OPTIONAL)
- Not found
- **Note:** As a general CDF reader, it supports data from any mission that uses CDF format rather than specific observatories

### 33. Logo (OPTIONAL)
- **Logo URL:** https://raw.githubusercontent.com/pysat/pysatCDF/main/docs/images/logo.png
- **Source:** SoMEF regular expression extraction, PyHC registry

---

## Metadata Sources Summary

1. **DataCite API** (https://doi.org/10.5281/zenodo.1217180): Authors with ORCIDs, affiliations, titles, publication date, publisher, version, license, descriptions
2. **SoMEF** (GitHub repository analysis): Repository URL, programming languages, keywords, creation/update dates, license details, logo
3. **PyHC Registry** (projects.yml): Keywords (ionosphere_thermosphere_mesosphere, magnetosphere), development status, contact information
4. **Manual Repository Examination:**
   - README.md: Description, usage examples, installation instructions, operating system support
   - LICENSE: Full BSD-3-Clause license text
   - CHANGELOG.md: Version history and descriptions
   - setup.py: Programming language details, build information
   - .github/workflows/main.yml: CI/CD testing on ubuntu-latest with Python 3.8-3.10
   - Git tags: Version numbers and dates

---

## Notes

- The repository has moved from rstoneback/pysatCDF to pysat/pysatCDF (organization ownership)
- The concept DOI (10.5281/zenodo.1217180) represents all versions
- The latest version DOI is 10.5281/zenodo.6544438 (v0.3.2)
- pysatCDF is listed in the PyHC community packages registry with "Good" ratings for community, testing, software_maturity, python3, and license, but "Requires improvement" for documentation
- The package includes the NASA CDF library (v3.6.3) for self-contained operation
- Primary contact from PyHC: Russell Stoneback
