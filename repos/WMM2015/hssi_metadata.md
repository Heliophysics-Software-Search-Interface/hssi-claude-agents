# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/WMM2015
**Extraction Date:** 2025-12-04

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found

**Note:** No DOI found in repository files (README, CITATION.cff, codemeta.json, .zenodo.json). The package does not appear to have a registered DOI.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/WMM2015

**Source:** Repository URL, confirmed in setup.cfg

### 4. Software Functionality (MANDATORY)
- Models and Simulations:Empirical
- Data Visualization:2D Graphics

**Source:** Code analysis (src/wmm2015/base.py, src/wmm2015/plots.py)
**Details:**
- WMM2015 is an empirical geomagnetic model that computes Earth's magnetic field components (north, east, down, total intensity, declination, and inclination) at specified geographic locations
- Takes geographic coordinates (latitude, longitude, altitude) and time as input to calculate magnetic field values
- Provides 2D contour visualization of magnetic declination and inclination

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere

**Source:** PyHC registry metadata and scientific domain knowledge
**Details:** WMM2015 models the Earth's geomagnetic field and is commonly used for ionosphere/thermosphere/mesosphere studies

### 6. Authors (MANDATORY)
- **Authors:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** setup.cfg metadata

### 7. Software Name (MANDATORY)
WMM2015

**Source:** Repository name, setup.cfg, README.md, SoMEF extraction

### 8. Description (MANDATORY)
WMM2015 World Magnetic Model...in simple, object-oriented Python. WMM2015 is a Python wrapper for the World Magnetic Model 2015, providing a simple interface to compute geomagnetic field components (north, east, down, total intensity, declination, and inclination) at specified geographic coordinates and altitudes. The package uses a build-on-run technique, compiling the C library on first use. Tested on Linux, Mac and Windows. Most C compilers work.

**Source:** README.md, setup.cfg, SoMEF extraction

### 9. Concise Description (OPTIONAL)
WMM2015 geomagnetic model with simple object-oriented Python interface

**Source:** setup.cfg description field

### 10. Publication Date (RECOMMENDED)
2018-05-23

**Source:** Git repository creation date (first commit)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Repository hosting platform

### 12. Version (RECOMMENDED)
- **Version Number:** 1.1.1
- **Version Date:** 2021-02-11
- **Version Description:** cleanup, CMake >= 3.10, better feedback, Numpy 1.20 types. Changes include: cmake >= 3.10, pep517 compliance, improved documentation, cmake template updates
- **Version PID:** Not found

**Source:** Git tags, GitHub releases via SoMEF, setup.cfg

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- C

**Source:** setup.cfg (Python >= 3.7), GitHub API via SoMEF (C, Python, CMake, Meson)

### 14. Reference Publication (RECOMMENDED)
Not found

**Note:** No reference publication DOI found. References in README point to NOAA WMM2015 data maps, not a publication.

### 15. License (RECOMMENDED)
- **License:** Public Domain (U.S. Government Work)
- **License URI:** https://www.ngdc.noaa.gov/geomag/WMM/license.shtml

**Source:** LICENSE.txt
**Details:** The WMM source code is in the public domain and not licensed or under copyright. As required by 17 U.S.C. 403, the U.S. Government material is not subject to copyright protection.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- geomagnetic
- build-on-run
- ionosphere_thermosphere_mesosphere (from PyHC)
- specific (from PyHC)

**Source:** setup.cfg, GitHub topics via SoMEF, PyHC registry

### 17. Data Sources (OPTIONAL)
Not found

**Note:** The software uses built-in WMM2015 coefficient data files, not external data sources

### 18. Input File Formats (RECOMMENDED)
Not applicable

**Note:** Software uses internal coefficient data; takes numerical inputs (lat, lon, altitude, year) programmatically

### 19. Output File Formats (RECOMMENDED)
Not applicable

**Note:** Software returns xarray.Dataset objects in memory; does not write to specific file formats by default

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source:** README.md, .github/workflows/ci.yml (CI testing on ubuntu-latest, macos-latest, windows-latest)

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- CPU Independent

**Source:** Inferred from Python package compatibility and lack of architecture-specific constraints

### 22. Related Phenomena (OPTIONAL)
Not found

**Note:** While the software models geomagnetic phenomena, specific phenomena terms from controlled vocabularies were not found in repository documentation

### 23. Development Status (RECOMMENDED)
Active

**Source:** setup.cfg (Development Status :: 5 - Production/Stable), recent commit activity

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/wmm2015

**Source:** setup.cfg url field
**Note:** Documentation is primarily in the README.md file in the repository; no separate documentation site found

### 25. Funder (OPTIONAL)
Not found

### 26. Award Title (OPTIONAL)
Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

**Note:** No publications citing or describing the software were found in repository

### 28. Related Datasets (OPTIONAL)
- WMM2015 inclination map: https://www.ngdc.noaa.gov/geomag/WMM/data/WMM2015/WMM2015_I_MERC.pdf
- WMM2015 declination map: https://www.ngdc.noaa.gov/geomag/WMM/data/WMM2015/WMM2015_D_MERC.pdf

**Source:** README.md references section

### 29. Related Software (OPTIONAL)
- WMM2020: https://github.com/space-physics/wmm2020

**Source:** README.md (mentions WMM2020 as related/successor software)

### 30. Interoperable Software (OPTIONAL)
- xarray
- numpy

**Source:** setup.cfg install_requires
**Note:** These are required dependencies that the software interoperates with

### 31. Related Instruments (OPTIONAL)
Not found

**Note:** WMM is a general geomagnetic model not specific to any instrument

### 32. Related Observatories (OPTIONAL)
Not found

**Note:** WMM is a general model not specific to any observatory or mission

### 33. Logo (OPTIONAL)
Not found

---

## PyHC Registry Information

**Registry:** PyHC Unevaluated Packages
**Entry Found:** Yes

**PyHC Metadata:**
- **Name:** WMM2015
- **Code:** https://github.com/space-physics/WMM2015
- **Description:** World Magnetic Model 2015 from Python
- **Contact:** Michael Hirsch
- **Keywords:** ["ionosphere_thermosphere_mesosphere", "specific"]

---

## SoMEF Extraction Summary

**SoMEF Version:** 0.9.11
**Extraction Date:** 2025-12-04

**Key SoMEF Findings:**
- Repository owner: space-physics (Organization)
- Repository created: 2018-05-23T17:34:51Z
- Repository last updated: 2024-10-14T09:02:57Z
- Stargazers: 14
- Forks: 2
- Programming languages detected: C (8,774,915 bytes), Python (8,369 bytes), CMake (974 bytes), Meson (563 bytes)
- Has build files: pyproject.toml, setup.py
- Continuous Integration: GitHub Actions (.github/workflows/ci.yml)
- Application domain (ML classification): Computer Vision (confidence: 0.71) - likely incorrect classification

---

## Metadata Sources Priority

1. **PyHC metadata** - Found in unevaluated packages registry
2. **Repository files** - README.md, setup.cfg, LICENSE.txt
3. **SoMEF extraction** - Automated analysis of repository
4. **Code analysis** - Direct examination of Python source files
5. **Git history** - Commit logs, tags, and releases

---

## Notes

- **DOI Status:** No DOI found; package is not registered with Zenodo or other DOI providers
- **Documentation:** Minimal; primarily README-based
- **Maturity:** Production/Stable status but in PyHC "unevaluated" category
- **WMM Version:** This package implements WMM2015; a newer version (WMM2020) exists as separate package
- **Build System:** Uses "build-on-run" approach - C library compiled on first import
- **Compiler Requirements:** Requires C compiler; Visual Studio (MSVC) not supported
