# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/scanning-doppler-interferometer
**Extraction Date:** 2025-12-04

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/scanning-doppler-interferometer

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Processing
- Data Visualization:Line Plots

**Source:** Analysis of source code in scanning_doppler_interferometer/ directory. The software reads Scanning Doppler Interferometer data files (ASCII and IDL .sav formats), parses wind measurements, and creates line plots of wind speeds over time.

### 5. Related Region (MANDATORY)
- Earth Atmosphere

**Source:** PyHC registry keywords indicate "ionosphere_thermosphere_mesosphere". The data file shows measurements at 557.7 nm wavelength (characteristic of airglow emissions from the ionosphere/thermosphere region) from Poker Flat Research Range, Alaska.

### 6. Authors (MANDATORY)
- **Authors:** Michael Hirsch, Ph.D.
- **Author Email:** scivision@users.noreply.github.com
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** setup.cfg file (author and author_email) and LICENSE.txt file (copyright 2014-2020)

### 7. Software Name (MANDATORY)
Scanning Doppler Interferometer

**Source:** PyHC registry entry and README.md title

### 8. Description (MANDATORY)
Get, Parse, Plot: Scanning Doppler Interferometer data from PI Mark Conde's instruments. This software package loads and plots scanning Doppler interferometer data, particularly focused on atmospheric wind measurements. The package supports reading both ASCII text files and IDL .sav files containing wind data (zonal, meridional, and vertical components with associated uncertainties) from Scanning Doppler Interferometer observations. The data is aligned geographically at the station location and includes time series measurements of wind speeds in meters per second.

**Source:** README.md, PyHC registry, setup.cfg, and analysis of source code and example data files

### 9. Concise Description (OPTIONAL)
Load and plot scanning Doppler interferometer data from PI Mark Conde's instruments, with focus on atmospheric wind measurements.

### 10. Publication Date (RECOMMENDED)
2018-03-16

**Source:** First commit date from git history (SoMEF also extracted date_created: 2018-03-16T16:20:36Z from GitHub API)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** No DOI found, so repository host is the publisher

### 12. Version (RECOMMENDED)
- **Version Number:** 0.7.0
- **Version Date:** Not found (no git tags available)
- **Version Description:** Not found
- **Version PID:** Not found

**Source:** setup.cfg metadata

### 13. Programming Language (RECOMMENDED)
- Python 3.x

**Source:** setup.cfg specifies Python >= 3.6 (versions 3.6-3.9 listed in classifiers). SoMEF confirms Python from GitHub API.

### 14. Reference Publication (RECOMMENDED)
Not found

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://opensource.org/licenses/BSD-2-Clause

**Source:** LICENSE.txt file and SoMEF extraction from GitHub API (SPDX ID: BSD-2-Clause)

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
winds, interferometry, ionosphere

**Source:** setup.cfg (winds, interferometry) and SoMEF GitHub API extraction (interferometry, ionosphere)

### 17. Data Sources (OPTIONAL)
Observatory/Mission-specific

**Source:** The software is designed specifically for PI Mark Conde's Scanning Doppler Interferometer instruments

### 18. Input File Formats (RECOMMENDED)
- ascii
- IDL.sav

**Source:** Analysis of source code in base.py shows support for both ASCII text files (txt2dat function) and IDL .sav files (plotsav function using scipy.io.readsav)

### 19. Output File Formats (RECOMMENDED)
Not found

**Source:** Software primarily visualizes data rather than writing output files

### 20. Operating System (RECOMMENDED)
- Operating System Independent

**Source:** setup.cfg classifier "Operating System :: OS Independent"

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Source:** Python package with no architecture-specific dependencies

### 22. Related Phenomena (OPTIONAL)
Not found

**Source:** No specific phenomena mentioned in repository documentation

### 23. Development Status (RECOMMENDED)
Inactive

**Source:** setup.cfg classifier indicates "Development Status :: 4 - Beta". Last commit was 2022-08-11, and last update from GitHub API was 2023-01-27 (likely a metadata update). No releases or git tags found.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/scanning-doppler-interferometer

**Source:** No separate documentation site found. README.md provides basic usage instructions. Repository URL serves as documentation location.

### 25. Funder (OPTIONAL)
Not found

### 26. Award Title (OPTIONAL)
Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

### 28. Related Datasets (OPTIONAL)
Not found

**Note:** Example data file included in repository from Poker Flat Research Range (PKR_2017_061_date_03_02_sky_5577_nz0115.txt) but this is sample data, not a published dataset with a DOI.

### 29. Related Software (OPTIONAL)
Not found

**Note:** The package has dependencies on standard scientific Python libraries (pandas, matplotlib, scipy, python-dateutil) but these are not listed as they are general-purpose libraries rather than heliophysics-specific related software.

### 30. Interoperable Software (OPTIONAL)
Not found

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** Scanning Doppler Interferometer (Mark Conde's instruments)
- **Instrument Identifier:** Not found

**Source:** README.md and software description refer to "PI Mark Conde's instruments." Example data shows measurements from Poker Flat Research Range.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Poker Flat Research Range

**Source:** Example data file header shows "Site: Poker Flat Research Range" at coordinates 65.1192°N, 147.4303°W

### 33. Logo (OPTIONAL)
Not found

---

## Summary of Metadata Sources

1. **PyHC Registry (Unevaluated):** Package name, description, contact, keywords
2. **SoMEF Analysis:** Repository metadata, dates, license, programming language
3. **setup.cfg:** Package name, version, author, description, keywords, development status, Python versions
4. **LICENSE.txt:** License type, copyright holder, date range
5. **Source Code Analysis:** Software functionality, supported file formats
6. **Example Data Files:** Related observatory, instrument details, measurement types
7. **Git History:** Publication date, development activity
8. **README.md:** Software name, basic description, usage instructions

---

## Notes

- **No DOI Found:** This package does not have a persistent identifier (DOI). No CITATION.cff, .zenodo.json, or DOI badges found in repository.
- **No Git Tags:** No version tags found in git repository, though setup.cfg indicates version 0.7.0.
- **Development Status:** The repository shows limited recent activity (last commit 2022-08-11), indicating an inactive or minimally maintained project.
- **PyHC Status:** Listed in PyHC unevaluated packages, indicating it has been identified as a heliophysics Python package but has not undergone full PyHC standards evaluation.
- **Instrument-Specific:** This is a specialized package designed for a specific instrument operated by PI Mark Conde.
