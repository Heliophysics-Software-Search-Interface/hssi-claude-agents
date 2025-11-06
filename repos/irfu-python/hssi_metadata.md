# HSSI Metadata Extraction Results

**Repository:** https://github.com/louis-richard/irfu-python
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.10678694
- **Note:** This is the concept DOI for all versions (from DataCite API and user input)

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/louis-richard/irfu-python
- **Note:** From DataCite API, Zenodo API, and PyHC registry

### 4. Software Functionality (MANDATORY)
**Selected based on code analysis, documentation review, and PyHC metadata:**

- Coordinate Transforms
- Coordinate Transforms:Magnetospheric
- Coordinate Transforms:Mission-Specific
- Data Processing and Analysis
- Data Processing and Analysis:3D Particle Distribution Processing
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Curlometer
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Linear Gradient Estimation
- Data Processing and Analysis:Pitch Angle Distributions
- Data Processing and Analysis:Plasma Moments
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:Wave Polarization Analysis
- Data Processing and Analysis:Wavelet Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Orbit Plots
- Data Visualization:Spectrogram
- Mission-related
- Mission-related:Analysis
- Mission-related:Distribution/Access

**Note:** Based on extensive code analysis showing modules for:
- MMS mission-specific routines (particle distributions, pitch angles, energy spectra)
- MAVEN mission support
- Solar Orbiter support
- General plasma analysis routines (coordinate transforms, moments, spectrograms)
- 4-spacecraft analysis techniques (curlometer, gradient estimation)
- Wave analysis (polarization, wavelets)
- Data retrieval from multiple sources (local, SDC, AWS S3)

### 5. Related Region (MANDATORY)
- **Earth Magnetosphere** - Primary focus on MMS mission data which studies Earth's magnetosphere
- **Interplanetary Space** - Solar wind analysis, Solar Orbiter support, OMNI data access
- **Planetary Magnetospheres** - MAVEN mission support for Mars magnetosphere studies

**Note:** From PyHC keywords (heliosphere, magnetosphere, planetary) and mission support (MMS, MAVEN, Solar Orbiter)

### 6. Authors (MANDATORY)

#### Author 1
- **Name:** Louis Richard
- **Author Identifier:** https://orcid.org/0000-0003-3446-7322
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11
- **Affiliation:**
  - **Organization:** Uppsala University
  - **Affiliation Identifier:** https://ror.org/048a87296

#### Author 2
- **Name:** Yuri V. Khotyaintsev
- **Author Identifier:** https://orcid.org/0000-0001-5550-3113
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Author 3
- **Name:** Andris Vaivads
- **Author Identifier:** https://orcid.org/0000-0003-1654-841X
- **Affiliation:**
  - **Organization:** Ventspils University of Applied Sciences
  - **Affiliation Identifier:** https://ror.org/03sc6wx59
- **Affiliation:**
  - **Organization:** KTH Royal Institute of Technology
  - **Affiliation Identifier:** https://ror.org/026vcq606

#### Author 4
- **Name:** Daniel B. Graham
- **Author Identifier:** https://orcid.org/0000-0002-1046-746X
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Author 5
- **Name:** Cecilia Norgren
- **Author Identifier:** https://orcid.org/0000-0002-6561-2337
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Author 6
- **Name:** Andreas Johlander
- **Author Identifier:** https://orcid.org/0000-0001-7714-1870
- **Affiliation:**
  - **Organization:** Swedish Defence Research Agency
  - **Affiliation Identifier:** https://ror.org/0470cgs30

**Note:** All authors from DataCite API and CITATION.cff with complete ORCID and ROR identifiers

### 7. Software Name (MANDATORY)
- **Value:** Python RymdFysik Utilities (PyRFU)
- **Note:** From DataCite API. Also known as "pyrfu" (package name). Full formal name from Zenodo metadata.

### 8. Description (MANDATORY)
**Value:** PyRFU is a free and open-source Python package for advanced analysis of in-situ space plasma data. It provides routines to work with space data, particularly with Magnetospheric Multiscale (MMS) mission data, as well as MAVEN and Solar Orbiter missions. The package includes general plasma physics routines for coordinate transformations, particle distribution analysis, plasma moments calculations, wave analysis (including polarization and wavelets), multi-spacecraft techniques (curlometer, gradient estimation), and comprehensive data visualization capabilities. PyRFU is based on the IRFU-MATLAB library and supports data retrieval from multiple sources including local files, MMS Science Data Center, MAVEN Science Data Center, and cloud storage (AWS S3).

**Note:** Compiled from DataCite API description, README.rst, PyHC description, and detailed code analysis

### 9. Concise Description (OPTIONAL)
**Value:** A Python package for advanced analysis of in-situ space plasma data, particularly for MMS, MAVEN, and Solar Orbiter missions, with comprehensive tools for particle distributions, waves, and plasma physics.

**Note:** Condensed version under 200 characters

### 10. Publication Date (RECOMMENDED)
- **Value:** 2024-02-19
- **Note:** From DataCite API (publication date of version 2.4.12 associated with the concept DOI)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/04t3en479 (Note: Based on Zenodo being the publisher)

**Note:** From DataCite API

### 12. Version (RECOMMENDED)

#### Version Number
- **Value:** v2.4.12
- **Note:** This is the version associated with the concept DOI 10.5281/zenodo.10678694

#### Version Date
- **Value:** 2024-02-15
- **Note:** From git tag date for v2.4.12

#### Version Description
- **Value:** This version includes updates to requirements for PyHC Docker environment compatibility, addition of custom PyRFU plotting styles, improvements to particle distribution background removal, fixes for new CDF attributes structure, and updates to MAVEN data download functionality with new file tree organization.
- **Note:** From GitHub release notes for v2.4.12

#### Version PID
- **Value:** https://doi.org/10.5281/zenodo.10678695
- **Note:** Version-specific DOI from Zenodo API

### 13. Programming Language (RECOMMENDED)
- **Value:** Python 3.x
- **Specific versions supported:** Python 3.10, Python 3.11, Python 3.12
- **Note:** From pyproject.toml classifiers and Zenodo API

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found
- **Note:** No reference publication DOI found in DataCite API, CITATION.cff, or README. The software itself should be cited using its DOI.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT
- **Note:** From DataCite API, Zenodo API, SoMEF, and LICENSE.txt file

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values from multiple sources:**

**From PyHC registry:**
- heliosphere
- magnetosphere
- planetary
- plasma physics (plasma_physics)
- coordinates
- data retrieval (data_retrieval)
- line plots (line_plots)
- multidimensional
- orbit
- plotting
- power spectra (power_spectra)
- spectra
- time
- data access (data_access)
- data analysis (data_analysis)
- instrumentation
- theory

**From SoMEF/GitHub:**
- python3
- space physics (space-physics)

**Mission-specific:**
- MMS
- MAVEN
- OMNI
- Solar Orbiter (solo)

**Note:** Comprehensive keywords from PyHC metadata (manually curated) and GitHub topics

### 17. Data Sources (OPTIONAL)
- **Observatory/Mission-specific** - MMS Science Data Center, MAVEN Science Data Center
- **OMNIWeb** - Supported via get_omni_data function
- **S3/Cloud-aware** - AWS S3 bucket support for HelioCloud
- **HTTP/HTTPS Directories** - Direct data download from SDC

**Note:** From code analysis (download_data, db_init modules), pyproject.toml dependencies (boto3, botocore), and PyHC keywords (remote, web_service)

### 18. Input File Formats (RECOMMENDED)
- **CDF** - NASA Common Data Format (primary format)

**Note:** From code analysis (uses cdflib and pycdfpp libraries), pyproject.toml dependencies, and PyHC keywords

### 19. Output File Formats (RECOMMENDED)
- **CDF** - NASA Common Data Format

**Note:** Software can write CDF files based on the CDF library dependencies

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**

**Note:** From pyproject.toml classifiers listing Unix, macOS (MacOS X), and Microsoft Windows

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Note:** Python package with no specific CPU architecture requirements; pyproject.toml doesn't specify architecture constraints

### 22. Related Phenomena (OPTIONAL)
**Note:** Not found in repository documentation. This would require domain expertise to determine which specific phenomena the software is designed to study.

### 23. Development Status (RECOMMENDED)
- **Value:** Active
- **Note:** From Zenodo API metadata (developmentStatus: "active") and recent commit activity (last updated 2025-09-22 per SoMEF)

### 24. Documentation (RECOMMENDED)
- **Value:** https://pyrfu.readthedocs.io/en/latest/
- **Note:** From pyproject.toml, CITATION.cff, PyHC registry, and SoMEF

### 25. Funder (OPTIONAL)

#### Funder 1
- **Organization:** Swedish National Space Board
- **Funder Identifier:** https://ror.org/04t512h04

**Note:** From DataCite API funding references

### 26. Award Title (OPTIONAL)

#### Award 1
- **Award Title:** Plasma Jet Fronts: Energy Conversion and Particle Acceleration
- **Award Number:** 139/18

**Note:** From DataCite API funding references

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Value:** Not found
- **Note:** No related publications found in DataCite API relatedIdentifiers, README, or documentation

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found
- **Note:** No dataset DOIs found in DataCite API relatedIdentifiers

### 29. Related Software (OPTIONAL)

**From pyproject.toml dependencies (important related software):**
- cdflib - Python CDF reader/writer
- pycdfpp - Fast C++ CDF library with Python bindings
- geopack - Python version of geopack and Tsyganenko models
- xarray - Multi-dimensional labeled arrays
- matplotlib - Plotting library
- scipy - Scientific computing library
- numpy - Numerical computing library
- pandas - Data analysis library
- numba - JIT compiler for Python

**Note:** Major dependencies that this software builds upon and demonstrates interoperability with

### 30. Interoperable Software (OPTIONAL)

**From PyHC registry and dependencies:**
- xarray - Data container interoperability
- matplotlib - Visualization interoperability
- cdflib / pycdfpp - CDF file format compatibility

**Note:** Software packages that pyrfu has demonstrated interoperability with based on its design and PyHC membership

### 31. Related Instruments (OPTIONAL)

**From code analysis and PyHC keywords:**
- MMS (Magnetospheric Multiscale mission instruments)
  - FGM (Fluxgate Magnetometer)
  - EDP (Electric Double Probes)
  - FPI (Fast Plasma Investigation)
  - HPCA (Hot Plasma Composition Analyzer)
  - EIS (Energetic Ion Spectrometer)
  - FEEPS (Fly's Eye Energetic Particle Sensor)
- MAVEN (Mars Atmosphere and Volatile Evolution mission instruments)
- Solar Orbiter instruments

**Note:** From extensive MMS-specific code modules and MAVEN/Solar Orbiter support modules

### 32. Related Observatories (OPTIONAL)

**From code analysis, documentation, and PyHC keywords:**
- MMS (Magnetospheric Multiscale)
- MAVEN (Mars Atmosphere and Volatile Evolution)
- Solar Orbiter

**Note:** Primary missions supported based on dedicated code modules (pyrfu.mms, pyrfu.maven, solo routines)

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/louis-richard/irfu-python/master/docs/_static/logo-pyrfu.png
- **Note:** From PyHC registry

---

## Metadata Sources Summary

### Primary Sources (in priority order):
1. **PyHC Registry** (projects.yml) - Manually curated, highly reliable
2. **DataCite API** (10.5281/zenodo.10678694) - Official DOI metadata
3. **Zenodo API** (record 10678695) - Publisher metadata
4. **Repository Files:**
   - CITATION.cff - Author and citation information
   - README.rst - Description and documentation links
   - pyproject.toml - Package metadata, dependencies, classifiers
   - LICENSE.txt - License information
5. **SoMEF** - Automated repository metadata extraction
6. **Manual Code Analysis** - Functionality determined by examining:
   - Module structure (pyrfu/mms/, pyrfu/maven/, pyrfu/pyrf/, etc.)
   - Function names and purposes
   - Documentation structure
   - Examples in docs/examples/

### Extraction Methodology:
- All automated tools (DataCite, Zenodo, SoMEF, PyHC) were successfully queried
- Repository was thoroughly examined including code structure, documentation, and configuration files
- Git history analyzed for version information
- Software Functionality field required deep code analysis to identify all capabilities
- Related Region determined from mission support and scientific domain

### Confidence Assessment:
- **High Confidence:** Basic Information fields (Authors, DOI, Repository, Name, License, Publisher)
- **High Confidence:** Programming Language, Operating System, Documentation, Development Status
- **Medium-High Confidence:** Software Functionality (exhaustive code analysis performed)
- **Medium-High Confidence:** Related Region (based on mission support)
- **Medium Confidence:** File Formats (based on library dependencies)
- **Low Confidence:** Related Phenomena (would benefit from author input)

---

## Notes for Submitter

1. **Submitter Information (Field 1):** Please fill in your name and email address
2. **Related Phenomena (Field 22):** Consider adding specific phenomena the software is designed to study (e.g., magnetic reconnection, shock waves, plasma turbulence)
3. **Related Publications (Field 27):** If there are publications that use or cite this software, please add their DOIs
4. **Related Datasets (Field 28):** If there are specific datasets this software is designed to work with, please add their DOIs or citations
5. **Current Version:** Note that the repository's current version is v2.4.17 (as of extraction date), but the concept DOI metadata reflects v2.4.12. You may want to update the Zenodo deposit to include newer versions.
6. **Instrument Identifiers (Field 31):** Consider adding DOIs or persistent identifiers for the specific instruments if available
7. **Observatory Identifiers (Field 32):** Consider adding persistent identifiers for the missions if available

---

## Verification Checklist

- [x] All 33 form fields addressed
- [x] All MANDATORY fields have values
- [x] All RECOMMENDED fields have values (except Reference Publication - none exists)
- [x] Software Functionality exhaustively analyzed
- [x] Related Region comprehensively determined
- [x] All author ORCIDs verified from DataCite API
- [x] All ROR identifiers included where available
- [x] DOIs properly formatted (https://doi.org/...)
- [x] Dates in YYYY-MM-DD format
- [x] URLs verified from source files
- [x] Metadata traceable to sources
- [x] PyHC metadata prioritized (most reliable)
- [x] Multiple verification sources for key fields

**Extraction completed successfully with high confidence in all major fields.**
