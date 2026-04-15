# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/digital-meridian-spectrometer
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Concept DOI:** https://doi.org/10.5281/zenodo.596378
- **Note:** This is the concept DOI for all versions, found in Zenodo API response

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/space-physics/digital-meridian-spectrometer
- **Note:** Repository was previously at https://github.com/scivision/digital-meridian-spectrometer and has been moved/redirected

### 4. Software Functionality (MANDATORY)
Based on comprehensive analysis of code, documentation, and functionality:

- **Data Processing and Analysis**
- **Data Processing and Analysis:Data Access and Retrieval** - Loads data from remote FTP sources (Poker Flat Research Range)
- **Data Processing and Analysis:File Format Conversion** - Supports both NetCDF3 (.PF) and NetCDF4 (.NC) formats
- **Data Processing and Analysis:Processing** - Processes spectral intensity data with filter factors and calibration
- **Data Processing and Analysis:Time Series Analysis** - Time-indexed spectral data analysis with temporal filtering
- **Data Visualization**
- **Data Visualization:2D Graphics** - Creates pcolormesh visualizations of spectral data
- **Data Visualization:Line Plots** - Plots spectral data vs elevation angle
- **Data Visualization:Spectrogram** - Creates time-elevation-intensity spectrograms for multiple wavelengths

**Analysis rationale:** The software loads spectral data from the Digital Meridian Spectrometer, processes it (applying filter factors, handling multiple file formats), and creates comprehensive visualizations including spectrograms and 2D plots. It performs time series analysis with temporal filtering capabilities.

### 5. Related Region (MANDATORY)
- **Earth Atmosphere** - The Digital Meridian Spectrometer measures atmospheric emissions including auroral phenomena
- **Earth Magnetosphere** - Auroral emissions are a magnetospheric phenomenon; measurements at Poker Flat Research Range (high latitude) capture magnetosphere-ionosphere coupling

**Analysis rationale:** Located at Poker Flat Research Range, Alaska (65°N), the instrument measures auroral emissions (N₂⁺, H-beta, [OI], [NI]) which occur in the thermosphere/ionosphere due to magnetospheric particle precipitation. Keywords include "aurora" and "ionosphere_thermosphere_mesosphere".

### 6. Authors (MANDATORY)

#### Author 1:
- **Author Name:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found in DataCite/Zenodo metadata
- **Affiliation:**
  - **Organization:** SciVision, Inc.
  - **Affiliation Identifier:** Not found

**Note:** DataCite API listed "Ph.D." as given name and "Michael Hirsch" as family name (appears to be parsing error). PyHC registry lists "Michael Hirsch" as contact for this package.

### 7. Software Name (MANDATORY)
- **Software Name:** Digital Meridian Spectrometer
- **Package Name:** dmsp
- **Note:** Full title from README; package name "dmsp" used in PyPI and code

### 8. Description (MANDATORY)
Load and plot UAF Geophysical Institute Digital Meridian Spectrometer data from Poker Flat Research Range. The software handles spectral data from a ground-based meridian scanning photometer that measures auroral emissions at multiple wavelengths (427.8 nm N₂⁺, 486.1 nm H-beta, 520.0 nm [NI], 557.7 nm [OI], 630.0 nm [OI], 670.0 nm N₂). It supports both historical NetCDF3 format (.PF files from 1983-2010) and current NetCDF4 format (.NC files from 2011-present). The software provides data loading functions that return xarray.Dataset objects with time-elevation-intensity arrays, along with visualization capabilities including spectrograms and line plots. The library includes both Python and MATLAB interfaces.

### 9. Concise Description (OPTIONAL)
Load and plot UAF Geophysical Institute Digital Meridian Spectrometer data from Poker Flat Research Range, supporting NetCDF3/4 formats with auroral spectral measurements.

### 10. Publication Date (RECOMMENDED)
- **Initial Publication Date:** 2015-10-26
- **Note:** From git log --reverse, first commit date

### 11. Publisher (RECOMMENDED)
- **Publisher:**
  - **Organization:** Zenodo
  - **Publisher Identifier:** https://zenodo.org
- **Note:** DOI obtained through Zenodo (GitHub-Zenodo workflow)

### 12. Version (RECOMMENDED)

#### Latest Version Information:
- **Version Number:** v1.0 (from git tags, current development version 1.0.0 in __init__.py)
- **Version Date:** Not found in git tags for v1.0
- **Version Description:** Not found
- **Version PID:** Not found (no specific DOI for v1.0)

#### Documented Version from Zenodo:
- **Version Number:** v0.6.0
- **Version Date:** 2018-10-10
- **Version Description:** Simplify "load" API like many other of our programs. Create Matlab API and plots.
- **Version PID:** https://doi.org/10.5281/zenodo.1453766

**Note:** Repository appears to have evolved beyond v0.6.0 (current code shows v1.0.0), but v1.0 has not been formally released to Zenodo with a DOI.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** - Primary language (13,378 bytes from GitHub API, ~89%)
- **MATLAB** - Secondary support (1,718 bytes from GitHub API, ~11%, MATLAB interface file dmsp.m)
- **Note:** Requires Python ≥3.8 according to pyproject.toml

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication:** Not found
- **Note:** No CITATION.cff file or published paper reference found in repository or DataCite metadata

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** http://www.apache.org/licenses/LICENSE-2.0
- **SPDX ID:** Apache-2.0
- **Note:** Confirmed from GitHub API, SoMEF, and LICENSE.txt file in repository

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
From multiple sources (GitHub topics, PyHC registry, pyproject.toml):

- aurora
- auroral emissions
- spectrograph
- spectrometer
- geophysical-institute
- poker-flat-research-range
- netcdf
- matlab-python-interface
- python
- ionosphere_thermosphere_mesosphere (from PyHC)

### 17. Data Sources (OPTIONAL)
- **FTP/FTPS Directories** - Primary data source: ftp://optics.gi.alaska.edu/PKR/DMSP/NCDF/ (2011-present)
- **Observatory/Mission-specific** - Poker Flat Research Range Digital Meridian Spectrometer
- **Note:** Historical data (1983-2010) previously available at http://optics.gi.alaska.edu/realtime/data/msp/pkr but link stopped working in late 2018

### 18. Input File Formats (RECOMMENDED)
- **netCDF3/4** - Primary format (.NC files and .PF files)
- **Note:** Software explicitly handles both NetCDF3 (legacy .PF format, 1983-2010) and NetCDF4 (.NC format, 2011-present)

### 19. Output File Formats (RECOMMENDED)
- **Not specified** - Software focuses on data loading and visualization; primary output is xarray.Dataset objects (in-memory)
- **Note:** Plots can be saved in standard matplotlib formats (PNG, PDF, etc.) but no explicit file writing functionality in the API

### 20. Operating System (RECOMMENDED)
- **Linux** - Tested on ubuntu-latest in CI/CD (GitHub Actions)
- **Operating System Independent** - Pure Python implementation should work on any OS with Python support
- **Note:** CI/CD tests on ubuntu-latest with Python 3.8 and 3.12; no OS-specific code detected

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** - Pure Python/NumPy implementation with no architecture-specific code
- **Note:** Should run on any architecture supporting Python and dependencies (x86-64, ARM, etc.)

### 22. Related Phenomena (OPTIONAL)
Detected from spectral analysis in code (plots.py):

- Auroral emissions
- Atmospheric optical emissions
- **Note:** Software measures specific emission lines: N₂⁺ 1N (427.8nm), H-beta (486.1nm), [NI] (520.0nm), N₂ 1P (670.0nm), [OI] (557.7nm, 630.0nm)

### 23. Development Status (RECOMMENDED)
- **Active** - Based on repository status and recent activity
- **Note:** PyHC lists this package in the "unevaluated" category. Recent commit in 2024-03-21 (from SoMEF date_updated). Repository shows active development with CI/CD configured.

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/space-physics/digital-meridian-spectrometer
- **Note:** No separate documentation site found; README.md in repository serves as primary documentation. No readthedocs configuration detected.

### 25. Funder (OPTIONAL)
- **Funder:** Not found
- **Note:** No funding information in DataCite metadata or repository

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found
- **Note:** No grant/award information found in any metadata source

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Related Publications:** Not found
- **Note:** No related publications in DataCite metadata or repository

### 28. Related Datasets (OPTIONAL)
- **Related Datasets:** The UAF Geophysical Institute Poker Flat Digital Meridian Spectrometer data archive
  - FTP: ftp://optics.gi.alaska.edu/PKR/DMSP/
  - Historical: 1983-present
- **Note:** No formal DOI for the dataset itself

### 29. Related Software (OPTIONAL)
Dependencies from pyproject.toml:

- netCDF4 - For reading NetCDF files
- xarray - For data container/manipulation
- numpy - For numerical operations
- python-dateutil - For date/time parsing
- matplotlib (implied from plots.py) - For visualization

**Note:** No DOIs found for related software; these are standard scientific Python packages

### 30. Interoperable Software (OPTIONAL)
- **xarray** - Returns xarray.Dataset objects, making it interoperable with the xarray ecosystem
- **MATLAB** - Provides MATLAB interface (dmsp.m) for MATLAB users
- **Note:** Software designed to integrate with broader scientific Python ecosystem

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** Digital Meridian Spectrometer (also called Meridian Scanning Photometer)
- **Instrument Identifier:** Not found
- **Location:** Poker Flat Research Range, UAF Geophysical Institute, Alaska
- **Note:** Ground-based optical instrument measuring auroral emissions along the magnetic meridian

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Poker Flat Research Range (PFRR)
- **Alternative:** UAF Geophysical Institute
- **Note:** Poker Flat Research Range is a major high-latitude research facility operated by the University of Alaska Fairbanks Geophysical Institute

### 33. Logo (OPTIONAL)
- **Logo URL:** Not found
- **Note:** No logo file found in repository; PyHC registry entry does not include logo

---

## Metadata Sources Summary

1. **DataCite API** (DOI: 10.5281/zenodo.596378): Software name, description, authors, publisher, publication date, version, license, repository URL
2. **Zenodo API** (Record: 1453766): Concept DOI, version-specific DOI, detailed version information
3. **SoMEF**: Keywords, programming languages, repository statistics, descriptions, license confirmation, dates
4. **PyHC Registry** (unevaluated packages): Package entry confirmed, contact information, keywords (ionosphere_thermosphere_mesosphere)
5. **Manual Repository Examination**:
   - README.md: Data sources, usage examples, installation instructions
   - pyproject.toml: Dependencies, package metadata, Python version requirements
   - LICENSE.txt: License confirmation (Apache 2.0)
   - Source code (io.py, plots.py): File format support, functionality analysis, spectral wavelengths
   - .github/workflows/ci.yml: OS support, Python version testing
   - Git history: Initial commit date, version tags

---

## Notes on Metadata Quality

### High Confidence Fields:
- Code repository, software name, description, programming languages, license, keywords, input formats, operating systems, development status

### Medium Confidence Fields:
- Authors (single author confirmed from multiple sources, but no ORCID found)
- Version information (v0.6.0 well-documented, but current v1.0 not formally released)
- Software functionality (comprehensive analysis performed)
- Related region (based on scientific understanding of auroral measurements)

### Missing/Unknown Fields:
- Submitter information (to be filled by actual submitter)
- Author ORCID, affiliation ROR
- Reference publication
- Funding information
- Output file formats (software focuses on visualization, not file output)
- Logo
- Related publication/dataset DOIs
- Formal documentation site

### Metadata Priorities Applied:
PyHC metadata (manually curated) was prioritized for contact information and keywords. DataCite/Zenodo APIs provided authoritative DOI-related metadata. SoMEF provided supplementary confirmation and GitHub-specific details. Manual repository examination was critical for understanding file format support, functionality, and scientific context.
