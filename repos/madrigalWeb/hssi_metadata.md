# HSSI Metadata Extraction Results

**Repository:** https://github.com/MITHaystack/madrigalWeb
**Extraction Date:** 2025-12-04

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**DOI:** Not found

**Note:** No DOI found in repository files (CITATION.cff, README.md, or other common locations). Package is available on PyPI but does not appear to have a Zenodo DOI or other persistent identifier.

---

### 3. Code Repository (MANDATORY)
**Repository URL:** https://github.com/MITHaystack/madrigalWeb

**Source:** CITATION.cff, PyHC registry, SoMEF

---

### 4. Software Functionality (MANDATORY)

Based on comprehensive analysis of the code, documentation, and repository:

- **Data Processing and Analysis:Data Access and Retrieval** (primary functionality)
- **Data Processing and Analysis:Data Reduction**
- **Data Processing and Analysis:File Format Conversion**

**Source:** Code analysis of madrigalWeb.py, globalDownload.py, and globalIsprint.py. The software is a remote API client for accessing Madrigal databases with the following capabilities:
- Remote data access from any Madrigal server via web services
- Data retrieval with filtering by date, instrument, experiment, and parameters
- Parameter selection (choose specific parameters from available data)
- Data filtering (apply numeric filters and range constraints to parameters)
- File format conversion (ascii, HDF5, netCDF4)

---

### 5. Related Region (MANDATORY)

- **Earth Atmosphere** (primary)
- **Earth Magnetosphere**

**Source:** PyHC registry keywords ("ionosphere_thermosphere_mesosphere"), package description, and domain knowledge of Madrigal databases. Madrigal is primarily used for ionospheric and upper atmospheric radar data, with some magnetospheric applications.

---

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** William Rideout
- **Author Identifier:** https://orcid.org/0000-0002-1591-4855
- **Affiliation:**
  - **Organization:** MIT Haystack Observatory
  - **Affiliation Identifier:** Not found

**Author 2:**
- **Name:** Katherine Cariglia
- **Email:** cariglia@mit.edu
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** MIT Haystack Observatory
  - **Affiliation Identifier:** Not found

**Source:** CITATION.cff, pyproject.toml

---

### 7. Software Name (MANDATORY)
**Name:** madrigalWeb

**Source:** CITATION.cff, pyproject.toml, PyHC registry, SoMEF

---

### 8. Description (MANDATORY)

madrigalWeb is a pure python module to access data from any Madrigal database. For documentation and examples go to any Madrigal site such as http://cedar.openmadrigal.org

The easiest way to use the Madrigal python remote data access API is to simply let the web interface write the script you need for you. Just choose the Access data pull-down menu and choose Create a command to download multiple exps. Then follow the instructions, and you will have the command you need to download whatever you want from Madrigal. Be sure to select python as the language you want to create the command with. You can choose to download files as they are in Madrigal in either column-delimited ascii, Hdf5, or netCDF4 formats, or you can choose the parameters yourself (including derived parameters), and optionally include filters on the data you get back.

This web interface will generate python commands using one of the following two Python scripts: globalDownload.py and globalIsprint.py. Use globalDownload.py if you want data as it is in Madrigal. Use globalIsprint.py to choose parameters and/or filters. These two scripts are documented below, for those who do not want to use the web interface to generate the needed arguments.

**Source:** CITATION.cff abstract, README.md

---

### 9. Concise Description (OPTIONAL)
**Concise Description:** Python Madrigal Remote API - Access data from any Madrigal database with support for multiple file formats and parameter filtering.

**Source:** Derived from pyproject.toml description and CITATION.cff

---

### 10. Publication Date (RECOMMENDED)
**Publication Date:** 2024-09-19

**Source:** Git repository creation date (2024-09-19 16:37:31 -0400), SoMEF date_created (2024-09-19T20:37:31Z)

**Note:** This appears to be the date the GitHub repository was created. The software itself (madrigalWeb) has existed longer but was migrated to GitHub at this date.

---

### 11. Publisher (RECOMMENDED)

**Publisher:**
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Repository hosting platform. Note: The package is also published to PyPI (https://pypi.org/project/madrigalWeb/)

---

### 12. Version (RECOMMENDED)

**Version Information:**
- **Version Number:** 3.3.5
- **Version Date:** Not found
- **Version Description:** Not found
- **Version PID:** Not found

**Source:** pyproject.toml, SoMEF

**Note:** No git tags found in repository. No CHANGELOG or release notes found. Version information only available from pyproject.toml.

---

### 13. Programming Language (RECOMMENDED)

- **Python 3.x**

**Source:** pyproject.toml (requires-python = ">=3.3"), CITATION.cff keywords, SoMEF, GitHub repository statistics

---

### 14. Reference Publication (RECOMMENDED)
**Reference Publication:** Not found

**Note:** No reference publication DOI found in CITATION.cff or README.md

---

### 15. License (RECOMMENDED)

**License:**
- **License Name:** MIT License
- **License URI:** https://api.github.com/licenses/mit

**Source:** CITATION.cff, license.txt, pyproject.toml, SoMEF

**Note:** Full license text available in license.txt. Copyright 2024 Massachusetts Institute of Technology.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- python
- database
- geospace
- API
- ionosphere_thermosphere_mesosphere
- general

**Source:** CITATION.cff keywords, PyHC registry

---

### 17. Data Sources (OPTIONAL)

- **Observatory/Mission-specific** (Madrigal databases)

**Source:** Code analysis and documentation. The software connects to any Madrigal database server, which are observatory/mission-specific distributed databases.

---

### 18. Input File Formats (RECOMMENDED)

Not applicable - this is a data access API that retrieves data from remote Madrigal servers via web services, not from local files.

---

### 19. Output File Formats (RECOMMENDED)

- **ascii**
- **HDF5**
- **netCDF3/4**

**Source:** Code analysis of madrigalWeb.py (lines 586-632), globalDownload.py documentation. The software can download/export data in these formats.

---

### 20. Operating System (RECOMMENDED)

- **Operating System Independent**
- **Linux** (verified via CI/CD)

**Source:** GitHub Actions workflow (python-publish.yml uses ubuntu-latest), pyproject.toml classifiers ("Operating System :: OS Independent"), globalDownload.py documentation states "It runs on either unix or windows"

---

### 21. CPU Architecture (RECOMMENDED)

- **CPU Independent**

**Source:** Pure Python implementation with no compiled dependencies (only requires 'packaging' package), runs on any platform supporting Python 3.3+

---

### 22. Related Phenomena (OPTIONAL)

Not found

**Note:** No specific phenomena keywords found in repository metadata. Madrigal databases contain various ionospheric and atmospheric phenomena data, but specific phenomena are not listed in the package metadata.

---

### 23. Development Status (RECOMMENDED)

**Status:** Active

**Source:** Inference based on recent development activity and lack of deprecation notices. The repository was created in September 2024, indicating recent migration/setup. Current version 3.3.5 suggests mature, actively maintained software.

**Note:** No explicit repostatus.org badge found in repository.

---

### 24. Documentation (RECOMMENDED)

**Documentation URL:** http://cedar.openmadrigal.org

**Source:** CITATION.cff url field, setup.py, README.md

**Note:** Documentation is available at any Madrigal site. The main reference site is cedar.openmadrigal.org. The repository README and inline documentation provide usage examples.

---

### 25. Funder (OPTIONAL)

Not found

**Note:** No funder information found in CITATION.cff, README.md, or other repository files.

---

### 26. Award Title (OPTIONAL)

Not found

**Note:** No award information found in repository files.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

Not found

**Note:** No publications found in CITATION.cff or README.md

---

### 28. Related Datasets (OPTIONAL)

Not found

**Note:** While the software accesses Madrigal databases which contain numerous datasets, no specific dataset DOIs or citations are provided in the repository metadata.

---

### 29. Related Software (OPTIONAL)

**Related Software:**
- **pysat** - Management and analysis tool for satellite and radar data (has madrigal keyword in PyHC registry)

**Source:** PyHC core registry. pysat includes madrigal data access functionality and is listed as a related/complementary tool.

---

### 30. Interoperable Software (OPTIONAL)

Not found

**Note:** No explicit interoperability statements found in repository documentation.

---

### 31. Related Instruments (OPTIONAL)

Not applicable - this software accesses data from any instrument whose data is stored in a Madrigal database. The specific instruments are not enumerated in the software metadata.

**Note:** Madrigal databases contain data from numerous radar and optical instruments worldwide. The getAllInstruments() method in the code can retrieve the list of instruments from a given Madrigal server.

---

### 32. Related Observatories (OPTIONAL)

Not applicable - this software accesses data from any observatory whose data is stored in a Madrigal database. Specific observatories are not enumerated in the software metadata.

**Note:** Madrigal is a distributed database system used by multiple observatories and facilities worldwide. The software can access any Madrigal site.

---

### 33. Logo (OPTIONAL)

Not found

**Note:** No logo found in repository or PyHC registry entry.

---

## Metadata Sources Summary

**Primary Sources:**
1. **CITATION.cff** - Authors with ORCID, title, abstract, keywords, license, repository URL
2. **pyproject.toml** - Version, authors, description, Python requirements, dependencies
3. **PyHC unevaluated registry** - Package classification, domain keywords
4. **SoMEF output** - Automated metadata extraction
5. **Code analysis** - File formats, functionality, data sources
6. **Repository files** - License (license.txt), README (README.md)

**Metadata Quality Notes:**
- No DOI or persistent identifier available
- No version history or release dates in git tags
- No CHANGELOG or detailed version descriptions
- Limited documentation in repository (references external Madrigal sites)
- Recent GitHub repository creation (Sept 2024) but software is more mature
- PyHC unevaluated status - not yet fully reviewed by PyHC standards

---

## Verification Notes

**Verified Information:**
- ✓ Authors confirmed across multiple sources (CITATION.cff, pyproject.toml)
- ✓ License confirmed (MIT) with full text in license.txt
- ✓ Repository URL verified and accessible
- ✓ Version number (3.3.5) confirmed in pyproject.toml
- ✓ Programming language (Python 3.x) confirmed
- ✓ File formats (ascii, HDF5, netCDF4) verified in code
- ✓ Software functionality verified through code analysis

**Information Requiring User Verification:**
- Development Status (inferred as "Active" but no explicit badge)
- Related Region classification (based on domain knowledge of Madrigal)
- Software Functionality categories (based on code analysis)

**Missing Information:**
- Persistent Identifier (DOI)
- Reference Publication
- Version release dates and descriptions
- Funder and Award information
- Related Publications
- Explicit Related Instruments/Observatories enumeration
- Logo
