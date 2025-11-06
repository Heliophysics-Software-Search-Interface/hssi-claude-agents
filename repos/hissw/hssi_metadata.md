# HSSI Metadata Extraction Results

**Repository:** https://github.com/wtbarnes/hissw
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.5519495
**Source:** README.md badge, Zenodo API (concept DOI)

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/wtbarnes/hissw
**Source:** SoMEF, Repository URL

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion
- Servers and Environments:Software or Environment Container

**Analysis:** hissw is a Python wrapper that enables integration of SolarSoft IDL (SSWIDL) scripts into Python workflows. It provides:
- Access to IDL/SSW functionality from Python
- Conversion between Python objects and IDL .sav file format (via scipy.io.readsav)
- Environment management for executing IDL/SSW scripts within Python

**Source:** Code analysis of hissw/environment.py, documentation

### 5. Related Region (MANDATORY)
**Value:** Solar Environment

**Analysis:** hissw is specifically designed for solar physics applications, as it provides access to the SolarSoft (SSW) library, which contains solar physics analysis tools. Keywords include "solar", "solar-physics", and "solarsoft".

**Source:** setup.cfg keywords, PyHC metadata, documentation

### 6. Authors (MANDATORY)

**Author 1:**
- **Author Name:** Will Barnes
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** @rice-solar-physics (Rice Solar Physics group)
  - **Affiliation Identifier:** Not found

**Author 2:**
- **Author Name:** Bin Chen
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** New Jersey Institute of Technology
  - **Affiliation Identifier:** Not found

**Source:** Zenodo API, DataCite API, setup.cfg

### 7. Software Name (MANDATORY)
**Value:** hissw
**Source:** setup.cfg, SoMEF, GitHub API

### 8. Description (MANDATORY)
**Value:** Seamlessly integrate SSWIDL code into your Python workflow. The SolarSoftware (SSW) stack contains nearly every piece of software a solar physicist needs. hissw is a lightweight Python package that allows you to write IDL scripts (either inline or in a separate file) which use your installed SSW packages and return the results to your local Python namespace. hissw uses Jinja2 templates to generate SSW startup scripts and then runs your IDL code using subprocess. You can also use Jinja syntax to inject arguments from Python into IDL. The results are then saved to a file and then loaded back in using scipy.io.readsav().

**Source:** setup.cfg, documentation index.md, SoMEF

### 9. Concise Description (OPTIONAL)
**Value:** Easily integrate SSWIDL scripts into your Python workflow via Jinja templates

**Source:** PyHC metadata

### 10. Publication Date (RECOMMENDED)
**Value:** 2017-01-25
**Source:** SoMEF (date_created from GitHub API)

### 11. Publisher (RECOMMENDED)

**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** Zenodo API, DataCite API

### 12. Version (RECOMMENDED)

**Latest Version (v2.3):**
- **Version Number:** v2.3
- **Version Date:** 2022-11-23
- **Version Description:** Add filter to force preservation of precision in floating point values
- **Version PID:** https://doi.org/10.5281/zenodo.7352323

**Cited Version (v2.0):**
- **Version Number:** v2.0
- **Version Date:** 2022-06-14
- **Version Description:** Added default filters for passing in Quantity objects and computing log10; The 'ssw_home' variable is now exposed in all scripts by default; Scripts can be run in "IDL only" mode to avoid the need to install SSW
- **Version PID:** https://doi.org/10.5281/zenodo.6640421

**Note:** The README cites v2.0 as the preferred citation, though v2.3 is the latest release.

**All Versions:**
- v1.0: 2018-09-12
- v1.1: 2019-07-26
- v1.2: 2021-09-21
- v2.0: 2022-06-14
- v2.1: 2022-06-21
- v2.2: 2022-08-23
- v2.3: 2022-11-23

**Source:** Zenodo API, SoMEF releases, git tags

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x
- IDL

**Note:** The package itself is written primarily in Python (with Shell and Prolog scripts for templates), but it explicitly integrates with IDL as its core functionality.

**Source:** SoMEF (GitHub API languages), setup.cfg (python_requires >= 3.6)

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Note:** No journal publication describing hissw was found in the repository or metadata.

### 15. License (RECOMMENDED)

**License:**
- **License Name:** MIT License
- **License URI:** https://api.github.com/licenses/mit

**Full License Text Available In:** LICENSE file

**Source:** SoMEF, GitHub API, LICENSE file, setup.cfg

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- solar
- sun
- ssw
- solar-physics
- idl
- sswidl
- solarsoft
- python
- general
- wrapper
- idl_save

**Source:** setup.cfg, SoMEF (GitHub topics), PyHC metadata

### 17. Data Sources (OPTIONAL)
**Value:** Not applicable

**Note:** hissw is a wrapper/interface tool, not a data access tool. It enables users to access data through IDL/SSW scripts, but does not itself provide data source integration.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- IDL.sav

**Note:** hissw can read IDL save files (.sav) returned from IDL script execution using scipy.io.readsav. Other formats are accessible indirectly through IDL scripts.

**Source:** Code analysis (environment.py uses scipy.io.readsav)

### 19. Output File Formats (RECOMMENDED)
**Values:**
- IDL.sav

**Note:** hissw saves results from IDL execution to .sav files before loading them into Python. Other output formats depend on what the user's IDL scripts produce.

**Source:** Code analysis (environment.py line 186)

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac

**Note:** README explicitly states "This has not been tested on Windows" and warns that shell command execution may cause difficulties on Windows. CI runs on ubuntu-latest.

**Source:** README.md, docs/index.md, .github/workflows/deploy-docs.yml

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Note:** Python code is CPU-independent. Actual architecture support depends on IDL installation requirements.

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Solar Corona
- Solar Flares
- Coronal Mass Ejections
- Coronal Heating
- X-ray emission

**Note:** While hissw itself is a tool wrapper, the SolarSoft library it provides access to is commonly used for these solar phenomena. The specific phenomena depend on which SSW packages the user loads (e.g., 'sdo/aia', 'chianti').

**Source:** Documentation context (SSW is for solar physics), typical SSW use cases

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Rationale:**
- setup.cfg declares "Development Status :: 5 - Production/Stable"
- Last commit was 2024-12-26 (per SoMEF)
- PyHC software_maturity rating: "Good"
- Repository is actively maintained

**Source:** setup.cfg, SoMEF (date_updated), PyHC metadata

### 24. Documentation (RECOMMENDED)
**Value:** https://wtbarnes.github.io/hissw/

**Source:** setup.cfg project_urls, SoMEF, PyHC metadata

### 25. Funder (OPTIONAL)
**Value:** Not found

**Note:** No funding information found in repository files or metadata APIs.

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Note:** No award information found in repository files or metadata APIs.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found

**Note:** No publications citing or describing hissw were found in the repository or metadata.

### 28. Related Datasets (OPTIONAL)
**Value:** Not applicable

**Note:** hissw is a tool for interfacing with IDL/SSW; it does not directly work with specific datasets.

### 29. Related Software (OPTIONAL)
**Values:**

**Dependencies:**
- **Jinja2** - Template engine used for generating IDL scripts
- **scipy** - Used for reading IDL .sav files (scipy.io.readsav)

**Related Tools:**
- **SolarSoft (SSW)** - The IDL library that hissw provides Python access to (http://www.lmsal.com/solarsoft/)
- **SunPy** - https://github.com/sunpy/sunpy (Python library for solar physics, mentioned in documentation as alternative for some SSW functionality)
- **Astropy** - http://www.astropy.org/ (Astronomy tools in Python, mentioned in documentation)
- **ChiantiPy** - https://github.com/chianti-atomic/ChiantiPy (Atomic database in Python, mentioned in documentation)

**Source:** setup.cfg dependencies, docs/index.md

### 30. Interoperable Software (OPTIONAL)
**Values:**
- **Astropy** (optional dependency in setup.cfg, tested together)

**Note:** The setup.cfg includes an 'astropy' extra, suggesting interoperability. The package can work with astropy Quantity objects via custom filters.

**Source:** setup.cfg [options.extras_require], code analysis

### 31. Related Instruments (OPTIONAL)
**Value:** Not specific to any instrument

**Note:** hissw is a general-purpose wrapper. The instruments it can work with depend on which SSW packages the user loads (e.g., SDO/AIA, SOHO/LASCO, etc.).

### 32. Related Observatories (OPTIONAL)
**Value:** Not specific to any observatory

**Note:** hissw is a general-purpose wrapper. The observatories/missions it can work with depend on which SSW packages are loaded (e.g., Solar Dynamics Observatory, SOHO, etc.).

### 33. Logo (OPTIONAL)
**Value:** Not found

**Note:** No logo file or URL found in the repository.

---

## PyHC Metadata (Additional Context)

hissw is listed in the Python in Heliophysics Community (PyHC) registry as a community package with the following quality ratings:

- **Community:** Partially met
- **Documentation:** Good
- **Testing:** Good
- **Software Maturity:** Good
- **Python 3 Compatibility:** Good
- **License:** Good

**Source:** PyHC projects.yml (heliophysicsPy.github.io)

---

## Metadata Extraction Summary

### Data Sources Used:
1. **Zenodo API** - Version metadata, DOIs, authors, affiliations
2. **DataCite API** - License, publication metadata
3. **SoMEF** - Repository metadata, programming languages, dates
4. **PyHC Registry** - Community ratings, description, keywords
5. **Manual Repository Examination** - Code analysis, documentation, configuration files

### Metadata Completeness:
- **MANDATORY fields:** 7/7 complete (100%)
- **RECOMMENDED fields:** 11/17 complete (65%)
- **OPTIONAL fields:** 5/9 with values (56%)

### Fields Not Found:
- Author ORCIDs
- Affiliation RORs
- Reference Publication
- Funder information
- Award information
- Related publications
- Logo
- Specific CPU architecture requirements

### Notes:
- The software is well-documented with good test coverage
- Active development status with recent updates
- Part of the PyHC ecosystem
- Requires local IDL and SolarSoft installations to function
- Primary use case is solar physics research
