# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/WMM2020
**Extraction Date:** 2026-03-10

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found -- no DOI, Zenodo integration, CITATION.cff, or codemeta.json file found in the repository.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/WMM2020

### 4. Software Functionality (MANDATORY)
- Models and Simulations
- Models and Simulations:Empirical
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Visualization
- Data Visualization:2D Graphics

**Source notes:** The software is a Python wrapper around the NOAA/NCEI World Magnetic Model 2020 (WMM2020), which is an empirical spherical-harmonic model of Earth's main magnetic field. The core functionality computes geomagnetic field elements (declination, inclination, total intensity, north/east/down components) at any geographic location and time using pre-computed Gauss coefficients (WMM.COF). The `plots.py` module provides 2D contour plots of magnetic declination and inclination over geographic coordinates using matplotlib.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere

**Source notes:** The World Magnetic Model describes Earth's main magnetic field generated in the core, which extends through the atmosphere and magnetosphere. The PyHC keyword "ionosphere_thermosphere_mesosphere" confirms applicability to Earth's upper atmosphere. The model is used for navigation, compass calibration, and geomagnetic research spanning from the surface through the atmosphere. The magnetosphere is included because the model describes Earth's core-generated magnetic field which structures the magnetosphere.

### 6. Authors (MANDATORY)
- **Author 1:**
  - **Name:** Michael Hirsch, Ph.D.
  - **Author Identifier:** https://orcid.org/0000-0001-6183-6256
  - **Affiliation:** SciVision, Inc.
- **Author 2:**
  - **Name:** Aaron Nielsen
  - **Author Identifier:** Not found
  - **Affiliation:** Not found
- **Author 3:**
  - **Name:** Andrey Korzh
  - **Author Identifier:** Not found
  - **Affiliation:** Not found
- **Author 4:**
  - **Name:** Antoine T
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

**Source notes:** Michael Hirsch from setup.cfg (24 commits, primary author). Aaron Nielsen (2 commits: transect function, error checking), Andrey Korzh (1 commit: build optimization), Antoine T (1 commit: wmm_point feature) identified from git shortlog as substantive contributors.

### 7. Software Name (MANDATORY)
wmm2020

**Source notes:** From setup.cfg `name` field and PyPI package name. Also listed as "WMM2020" in PyHC registry.

### 8. Description (MANDATORY)
WMM2020 is a Python wrapper providing a simple, object-oriented interface to the World Magnetic Model 2020 (WMM2020), the standard geomagnetic reference model produced by NOAA's National Centers for Environmental Information (NCEI) and the British Geological Survey (BGS). Given geographic latitude, longitude, altitude, and decimal year as inputs, the software computes the geomagnetic field elements: magnetic declination, inclination, total field intensity, and the north, east, and downward components of the magnetic field vector. The underlying WMM2020 C source code from NOAA is compiled automatically on first use via CMake. The package supports gridded computations over latitude/longitude arrays (returning xarray Datasets) as well as single-point lookups, and includes visualization of declination and inclination contour maps. WMM2020 is tested on Linux, macOS, and Windows. The model is valid for the epoch 2020.0 to 2025.0.

**Source notes:** Synthesized from README.md, setup.cfg description, PyHC description, NOAA documentation, and code analysis.

### 9. Concise Description (OPTIONAL)
Python interface to the World Magnetic Model 2020 (WMM2020) for computing geomagnetic field declination, inclination, and intensity at any location and time.

### 10. Publication Date (RECOMMENDED)
2020-06-10

**Source notes:** From git tag v1.0.0 creation date (first tagged release).

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source notes:** No DOI/Zenodo integration found. The software is published via GitHub and PyPI.

### 12. Version (RECOMMENDED)
- **Version Number:** 1.1.1
- **Version Date:** 2020-11-17
- **Version Description:** Not found -- no CHANGELOG or release notes
- **Version PID:** Not found -- no version-specific DOI

**Source notes:** Version from setup.cfg. Git tags confirm versions v1.0.0, v1.1.0, and v1.1.1.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- C

**Source notes:** Python wrapper (setup.cfg requires Python >= 3.7) with underlying C source code (GeomagnetismLibrary.c, wmm_point_sub.c). Build system uses CMake or Meson.

### 14. Reference Publication (RECOMMENDED)
Not found -- no CITATION.cff, no reference publication DOI in README or repository files. The underlying WMM2020 model has a NOAA technical report: "The US/UK World Magnetic Model for 2020-2025: Technical Report" (https://repository.library.noaa.gov/view/noaa/24390).

### 15. License (RECOMMENDED)
- **License:** Other
- **License URI:** https://www.ngdc.noaa.gov/geomag/WMM/license.shtml

**Source notes:** The LICENSE.txt states: "The WMM source code is in the public domain and not licensed or under copyright." This is a US Government public domain dedication per 17 U.S.C. 403. This does not correspond to a standard SPDX license; "Other" is the most appropriate selection. The Python wrapper code does not have a separate license declaration.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- geomagnetic
- space weather
- magnetism
- geophysics
- World Magnetic Model
- declination
- inclination
- space physics
- ionosphere
- upper atmosphere

**Source notes:** "geomagnetic" from setup.cfg classifiers keyword. PyHC keywords: "ionosphere_thermosphere_mesosphere", "specific". Additional domain-relevant keywords derived from the software's purpose.

### 17. Data Sources (OPTIONAL)
Not found -- the software does not retrieve data from external sources at runtime. The WMM.COF coefficient file is bundled with the package.

### 18. Input File Formats (RECOMMENDED)
- ascii

**Source notes:** The WMM.COF coefficient file is an ASCII text file containing spherical harmonic Gauss coefficients. The test_input.asc file is also ASCII. The software reads these ASCII coefficient files internally.

### 19. Output File Formats (RECOMMENDED)
Not found -- the software returns in-memory Python objects (xarray.Dataset or dict). It does not write output files directly, though the underlying C wmm_file executable can produce ASCII output files.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source notes:** README states "Tested on Linux, Mac and Windows." CI workflow (.github/workflows/ci.yml) confirms testing on ubuntu-latest, macos-latest, and windows-latest.

### 21. CPU Architecture (RECOMMENDED)
- x86-64

**Source notes:** CI runs on GitHub Actions standard runners which are x86-64. The C code is portable and could likely run on other architectures, but only x86-64 is explicitly tested.

### 22. Related Phenomena (OPTIONAL)
Not found -- the software models the main geomagnetic field, which is not directly one of the listed phenomena (Coronal Heating, Coronal Holes, CMEs, Solar Corona, Solar Flares, X-ray emission).

### 23. Development Status (RECOMMENDED)
Inactive

**Source notes:** setup.cfg classifies the software as "Development Status :: 5 - Production/Stable". The latest version (1.1.1) appears to be the final release with no recent commits. The WMM2020 model itself is valid only through 2025 and has been superseded by WMM2025, suggesting the package has reached end-of-life for its intended purpose. The CI uses outdated actions (actions/checkout@v2, actions/setup-python@v2) and Python 3.7.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/WMM2020

**Source notes:** No separate documentation site found. The README.md serves as the primary documentation with usage examples and installation instructions.

### 25. Funder (OPTIONAL)
Not found -- no funding information in repository.

### 26. Award Title (OPTIONAL)
Not found -- no award information in repository.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Chulliat, A., Brown, W., Alken, P., et al. (2020). The US/UK World Magnetic Model for 2020-2025: Technical Report. NOAA. https://repository.library.noaa.gov/view/noaa/24390

**Source notes:** This is the official WMM2020 technical report from NOAA/NCEI describing the underlying model.

### 28. Related Datasets (OPTIONAL)
Not found

### 29. Related Software (OPTIONAL)
- https://github.com/space-physics/WMM2015 -- WMM2015 Python wrapper by the same author (referenced in README)
- https://github.com/space-physics/igrf -- IGRF model Python wrapper by the same author (same GitHub organization)

**Source notes:** WMM2015 is directly referenced in the README. The space-physics GitHub organization contains related geomagnetic model packages.

### 30. Interoperable Software (OPTIONAL)
Not found -- no explicit interoperability statements. The software depends on numpy and xarray, and its output (xarray.Dataset) is interoperable with the broader scientific Python ecosystem.

### 31. Related Instruments (OPTIONAL)
Not found -- the WMM is a global model not tied to specific instruments, though it is derived from satellite (e.g., Swarm) and ground observatory magnetic measurements.

### 32. Related Observatories (OPTIONAL)
Not found

### 33. Logo (OPTIONAL)
Not found -- no logo file or URL found in repository or PyHC registry.

---

## Extraction Summary

| Field | Status | Source |
|-------|--------|--------|
| 1. Submitter | Placeholder | -- |
| 2. Persistent Identifier | Not found | No DOI in repo |
| 3. Code Repository | Found | Git remote config |
| 4. Software Functionality | Found | Code analysis |
| 5. Related Region | Found | Domain knowledge + PyHC keywords |
| 6. Authors | Found | setup.cfg + web search |
| 7. Software Name | Found | setup.cfg |
| 8. Description | Found | README + setup.cfg + code analysis |
| 9. Concise Description | Found | Synthesized |
| 10. Publication Date | Not found | No clear date |
| 11. Publisher | Found | GitHub |
| 12. Version | Found | setup.cfg + git tags |
| 13. Programming Language | Found | File analysis |
| 14. Reference Publication | Not found | No DOI; NOAA tech report noted |
| 15. License | Found | LICENSE.txt |
| 16. Keywords | Found | setup.cfg + PyHC + domain knowledge |
| 17. Data Sources | Not found | N/A for this package |
| 18. Input File Formats | Found | Code analysis (WMM.COF) |
| 19. Output File Formats | Not found | In-memory only |
| 20. Operating System | Found | README + CI config |
| 21. CPU Architecture | Found | CI config |
| 22. Related Phenomena | Not found | Not applicable |
| 23. Development Status | Found | setup.cfg + analysis |
| 24. Documentation | Found | README serves as docs |
| 25. Funder | Not found | No info |
| 26. Award Title | Not found | No info |
| 27. Related Publications | Found | NOAA tech report |
| 28. Related Datasets | Not found | No info |
| 29. Related Software | Found | README + GitHub org |
| 30. Interoperable Software | Not found | No explicit info |
| 31. Related Instruments | Not found | Not applicable |
| 32. Related Observatories | Not found | Not applicable |
| 33. Logo | Not found | No logo |

**PyHC Status:** Listed in unevaluated packages registry
**SoMEF:** Not run (Bash tool unavailable during extraction)
**DataCite/Zenodo:** Not applicable (no DOI found)
