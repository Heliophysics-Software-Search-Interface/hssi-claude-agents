# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/gima-magnetometer
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** Not found
**Note:** No DOI found in repository files (CITATION.cff, README.md, or other metadata files)

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/gima-magnetometer
**Source:** Repository URL

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots

**Analysis:** The software reads local UAF Geophysical Institute GIMA magnetometer netCDF4 files, processes and filters magnetometer time series data by time windows, concatenates multiple hourly data files, and generates 2D line plots showing the three magnetic field components (horizontal, declination, and vertical).

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere
- Earth Magnetosphere

**Analysis:** Ground-based magnetometer data is used to study ionospheric and magnetospheric processes. The GIMA network monitors geomagnetic variations related to ionospheric currents (auroral electrojet) and magnetospheric disturbances. PyHC classification indicates "ionosphere_thermosphere_mesosphere" usage.

### 6. Authors (MANDATORY)
**Author 1:**
- **Name:** Michael Hirsch
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** setup.cfg author field and copyright notice in source code

### 7. Software Name (MANDATORY)
**Value:** GIMAmag
**Package Name:** gima_magnetometer
**Source:** PyHC registry name is authoritative for HSSI; repository name is `gima-magnetometer`

### 8. Description (MANDATORY)
**Value:** UAF Geophysical Institute magnetometer network data read and plot. This software package provides tools for reading, processing, and visualizing magnetometer data from the University of Alaska Fairbanks Geophysical Institute Magnetometer Array (GIMA) network. The software reads netCDF4 format data files containing magnetic field measurements, allows time-based filtering and extraction, concatenates multiple hourly data files, and generates time series plots of the three magnetic field components (horizontal, declination, and vertical). The package is designed to support analysis of geomagnetic variations related to ionospheric currents and magnetospheric processes observed by the ground-based GIMA magnetometer network in Alaska.
**Source:** README.md, setup.cfg description field, code analysis

### 9. Concise Description (OPTIONAL)
**Value:** UAF Geophysical Institute magnetometer network data read and plot
**Source:** README.md and setup.cfg

### 10. Publication Date (RECOMMENDED)
**Value:** 2017-01-19
**Source:** SoMEF GitHub API date_created (first commit: 2017-01-18 22:05:48 -0500)

### 11. Publisher (RECOMMENDED)
**Value:**
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Note:** No DOI obtained; code is hosted on GitHub

### 12. Version (RECOMMENDED)
- **Version Number:** 0.6.2
- **Version Date:** 2018-07-08
- **Version Description:** modernize, pep8, mypy
- **Version PID:** Not found
**Source:** setup.cfg, git history for the commit introducing version 0.6.2

### 13. Programming Language (RECOMMENDED)
**Value:** Python 3.x
**Source:** setup.cfg (requires Python >= 3.6), SoMEF GitHub API programming_languages

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found
**Note:** No reference publication or citation information found in repository

### 15. License (RECOMMENDED)
**Value:**
- **License:** Apache License 2.0
- **License URI:** https://www.apache.org/licenses/LICENSE-2.0

**Note:** LICENSE.txt file contains Apache License 2.0, but setup.cfg indicates "License :: OSI Approved :: MIT License" - there is a discrepancy. The actual LICENSE.txt file is Apache 2.0, which should be considered authoritative.
**Source:** LICENSE.txt file and SoMEF GitHub API license data

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- magnetometer
- geomagnetic
- geophysics
- geoscience

**Source:** setup.cfg keywords field and SoMEF GitHub API topics

### 17. Data Sources (OPTIONAL)
**Values:**
- HTTP/HTTPS Directories
- Observatory/Mission-specific
**Note:** Data comes from the UAF Geophysical Institute GIMA archive at https://www.gi.alaska.edu/monitors/magnetometer/archive

### 18. Input File Formats (RECOMMENDED)
**Value:** netCDF3/4
**Source:** Code analysis - uses netCDF4 library to read .nc files (see __init__.py lines 17, 58)

### 19. Output File Formats (RECOMMENDED)
**Value:** Not found
**Note:** Software generates interactive matplotlib visualizations but does not write output files

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Source:** CI configuration (.github/workflows/ci.yml) tests on ubuntu-latest, macos-latest, windows-latest

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent
**Note:** Pure Python package with no CPU-specific requirements

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found
**Note:** Could potentially include auroral phenomena, but not explicitly documented

### 23. Development Status (RECOMMENDED)
**Value:** Inactive
**Note:** setup.cfg classifiers indicate "Development Status :: 4 - Beta"; last code commit was 2022-08-11 (over 3 years ago). Repository has reached a stable, usable state but is no longer actively developed.
**Source:** setup.cfg classifiers and git commit history

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/gima-magnetometer#readme
**Note:** Installation and usage documentation are in the repository README.
**Source:** README.md

### 25. Funder (OPTIONAL)
**Value:** Not found

### 26. Award Title (OPTIONAL)
**Value:** Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

### 29. Related Software (OPTIONAL)
**Values:**
- https://github.com/pydata/xarray
- https://github.com/Unidata/netcdf4-python
- https://github.com/matplotlib/matplotlib
- https://github.com/mwaskom/seaborn

**Source:** setup.cfg install_requires and extras_require

### 30. Interoperable Software (OPTIONAL)
**Value:** Not found
**Note:** Uses standard scientific Python packages but no explicit interoperability documentation

### 31. Related Instruments (OPTIONAL)
**Value:**
- **Instrument Name:** GIMA (Geophysical Institute Magnetometer Array)
- **Instrument Identifier:** Not found

**Note:** The software is specifically designed for the UAF Geophysical Institute magnetometer network

### 32. Related Observatories (OPTIONAL)
**Value:**
- **Observatory Name:** UAF Geophysical Institute / GIMA

**Note:** University of Alaska Fairbanks Geophysical Institute operates the GIMA magnetometer network

### 33. Logo (OPTIONAL)
**Value:** Not found

---

## Additional Notes

### PyHC Package Status
This package is listed in the PyHC (Python in Heliophysics Community) **Unevaluated** registry.

**PyHC Metadata:**
- **Name:** GIMAmag
- **Code:** https://github.com/space-physics/gima-magnetometer
- **Description:** UAF Geophysical Institute magnetometer network data read and plot
- **Contact:** Michael Hirsch
- **Keywords:** ionosphere_thermosphere_mesosphere, specific

**Source:** https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_unevaluated.yml (lines 45-49)

### Data Source Information
GIMA data archive: https://www.gi.alaska.edu/monitors/magnetometer/archive

### License Discrepancy
**Important:** There is a discrepancy between the LICENSE.txt file (Apache License 2.0) and the setup.cfg classifier (MIT License). The LICENSE.txt file should be considered authoritative, but this should be clarified with the author.

### Repository Activity
- **Created:** 2017-01-19
- **Last Code Commit:** 2022-08-11
- **Last Repository Update:** 2023-01-27 (per SoMEF GitHub API - likely metadata update)
- **Stars:** 1
- **Forks:** 1
- **Release v1.0:** 2017-03-13 (initial release)
- **Current Version:** 0.6.2 (introduced in commit `87953c1`; latest git tag is `v1.0`)

---

## Metadata Sources Summary

1. **Repository files examined:**
   - README.md
   - setup.cfg
   - setup.py
   - pyproject.toml
   - LICENSE.txt
   - .github/workflows/ci.yml
   - src/gimamag/__init__.py
   - src/gimamag/plots.py
   - LoadGIMA.py

2. **SoMEF output:** somef_output.json (automated extraction from repository)

3. **PyHC registry:** projects_unevaluated.yml (package is listed as unevaluated PyHC package)

4. **Git history:** Commit and tag analysis for dates and versions

5. **Code analysis:** Examined source code to determine functionality, file formats, and dependencies
