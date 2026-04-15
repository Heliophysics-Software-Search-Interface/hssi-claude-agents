# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/msise00
**Extraction Date:** 2025-12-04

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.595393
- **Note:** This is the concept DOI (for all versions) from Zenodo

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/space-physics/msise00
- **Source:** DataCite API, Zenodo API, SoMEF, PyHC registry

### 4. Software Functionality (MANDATORY)
- **Values:**
  - Models and Simulations
  - Models and Simulations:Empirical
  - Data Visualization
  - Data Visualization:Line Plots
  - Data Visualization:2D Graphics
  - Data Visualization:Movies
- **Note:** MSISE-00 is an empirical atmospheric model (NRL Mass Spectrometer and Incoherent Scatter radar Extended model) that provides temperature and density data. It includes plotting and visualization capabilities, including time animations (movies) as shown in the demo.

### 5. Related Region (MANDATORY)
- **Values:**
  - Earth Atmosphere
- **Note:** Valid from altitude z = 0..1000 km, covers troposphere through thermosphere

### 6. Authors (MANDATORY)

#### Author 1:
- **Name:** scivision
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** SciVision, Inc.
  - **Affiliation Identifier:** Not found
- **Source:** DataCite API, Zenodo API, LICENSE.txt (Copyright holder)

#### Author 2:
- **Name:** Daniel Kastinen
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Institutet för rymdfysik
  - **Affiliation Identifier:** Not found
- **Source:** DataCite API, Zenodo API

#### Primary Contact:
- **Name:** Michael Hirsch
- **Note:** Listed as contact in PyHC registry

### 7. Software Name (MANDATORY)
- **Name:** msise00
- **Full Title:** MSISE-00 in Python and Matlab
- **Alternate Name:** MSISE-00
- **Source:** GitHub repository name, README, PyHC registry, pyproject.toml

### 8. Description (MANDATORY)
- **Description:** NRL MSISE-00 atmospheric model-- in Python and Matlab. Python API for Fortran MSISE-00 neutral atmosphere model. The MSISE-00 model provides atmospheric temperature and density from ground to thermospheric heights. Valid from altitude z = 0..1000 km. Outputs include temperature (Kelvin), density (particles per cubic meter), and mass density (kilograms per cubic meter).
- **Source:** DataCite API, README.md, pyproject.toml, PyHC registry

### 9. Concise Description (OPTIONAL)
- **Concise Description:** NRL MSISE-00 atmospheric model-- in Python and Matlab
- **Source:** DataCite API, GitHub description

### 10. Publication Date (RECOMMENDED)
- **Date:** 2015-03-27
- **Source:** SoMEF (GitHub repository creation date)
- **Note:** First commit/creation date of the repository

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API

### 12. Version (RECOMMENDED)

#### Latest Version (v1.11.1):
- **Version Number:** v1.11.1
- **Version Date:** 2024-12-19
- **Version Description:** Python bugfix for Python 3.9
- **Version PID:** https://doi.org/10.5281/zenodo.14532758
- **Source:** DataCite API, Zenodo API, GitHub releases

#### Previous Notable Version (v1.10.1):
- **Version Number:** v1.10.1
- **Version Date:** 2021-10-11
- **Version Description:** Matlab tests, enhance build. Improve build for Python and Matlab, fix/add Matlab tests and examples
- **Source:** SoMEF (GitHub releases)

### 13. Programming Language (RECOMMENDED)
- **Languages:**
  - Fortran (primary implementation language - 368,365 bytes)
  - Python 3.x (Python wrapper - 25,179 bytes)
  - MATLAB (10,184 bytes)
  - CMake
- **Source:** SoMEF (GitHub API), pyproject.toml (requires Python >=3.9)

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.1029/2002JA009430
- **Citation:** Picone, J. M., et al. (2002), NRLMSISE‐00 empirical model of the atmosphere: Statistical comparisons and scientific issues, Journal of Geophysical Research: Space Physics, 107(A12).
- **Note:** Referenced in README as "1200+ citations 2002 paper"
- **Original Fortran Code:** https://ccmc.gsfc.nasa.gov/pub/modelweb/atmospheric/msis/

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT
- **SPDX Identifier:** MIT
- **Source:** DataCite API, SoMEF, LICENSE.txt, pyproject.toml

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Keywords:**
  - build-on-run
  - msis
  - atmosphere
  - geospace
  - ionosphere_thermosphere_mesosphere (from PyHC)
  - specific (from PyHC)
- **Source:** SoMEF (GitHub topics), pyproject.toml, PyHC registry

### 17. Data Sources (OPTIONAL)
- **Values:** Not found
- **Note:** The model uses geomagnetic indices (Ap and F10.7) which are obtained via the geomagindices package, but specific data sources are not explicitly listed

### 18. Input File Formats (RECOMMENDED)
- **Formats:**
  - Not applicable (uses programmatic inputs rather than files)
- **Note:** Model takes programmatic inputs (time, altitude, latitude, longitude, geomagnetic indices) rather than reading from data files

### 19. Output File Formats (RECOMMENDED)
- **Formats:**
  - netCDF3/4 (via xarray.Dataset)
  - HDF5 (NetCDF4 output is HDF5 compatible, as mentioned in README)
- **Note:** Outputs xarray.Dataset objects which can be written to NetCDF4/HDF5
- **Source:** README.md mentions "Write NetCDF4 output (HDF5 compatible)"

### 20. Operating System (RECOMMENDED)
- **Systems:**
  - Linux
  - Mac
  - Windows
  - OS Independent (Python-based with Fortran compilation)
- **Source:** CI configuration (.github/workflows/ci.yml), pyproject.toml classifier "Operating System :: OS Independent"

### 21. CPU Architecture (RECOMMENDED)
- **Architectures:**
  - x86-64 (tested on ubuntu-latest, macos-latest)
  - CPU Independent (Python with Fortran compilation)
- **Source:** CI workflows test on standard x86-64 architectures

### 22. Related Phenomena (OPTIONAL)
- **Values:** Not found
- **Note:** As an atmospheric model, it relates to neutral atmosphere phenomena but specific phenomena are not tagged in available metadata

### 23. Development Status (RECOMMENDED)
- **Status:** Active
- **Source:** pyproject.toml classifier "Development Status :: 5 - Production/Stable", recent commits (last updated 2025-11-06), active release cycle
- **Note:** Latest release v1.11.1 on 2024-12-19

### 24. Documentation (RECOMMENDED)
- **URL:** https://ccmc.gsfc.nasa.gov/modelweb/models/nrlmsise00.php
- **Source:** PyHC registry
- **Additional Documentation:** README.md in repository provides usage examples and installation instructions

### 25. Funder (OPTIONAL)
- **Values:** Not found
- **Source:** No funding information in DataCite, Zenodo, or repository files

### 26. Award Title (OPTIONAL)
- **Values:** Not found
- **Source:** No award information in DataCite, Zenodo, or repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Publications:** Not found in structured metadata
- **Note:** README references "1200+ citations 2002 paper" but no DOI explicitly provided in machine-readable format

### 28. Related Datasets (OPTIONAL)
- **Datasets:** Not found
- **Note:** Uses geomagnetic indices (Ap, F10.7) from geomagindices package as inputs

### 29. Related Software (OPTIONAL)
- **Software:**
  - geomagindices (>=1.4.0) - dependency for geomagnetic indices
  - xarray - for data container output
  - numpy - core numerical dependency
  - python-dateutil - date/time handling
- **Source:** pyproject.toml dependencies
- **Note:** These are dependencies rather than related/interoperable software

### 30. Interoperable Software (OPTIONAL)
- **Software:** Not found
- **Note:** Can be called from both Python and MATLAB environments, demonstrating cross-language interoperability

### 31. Related Instruments (OPTIONAL)
- **Instruments:** Not found
- **Note:** Model is mission-independent and not tied to specific instruments, though historically informed by mass spectrometer and incoherent scatter radar data

### 32. Related Observatories (OPTIONAL)
- **Observatories:** Not found
- **Note:** Model is mission-independent and provides general atmospheric parameters for any location/time

### 33. Logo (OPTIONAL)
- **URL:** https://raw.githubusercontent.com/space-physics/msise00/main/./src/msise00/tests/msise00_demo.gif
- **Source:** SoMEF (extracted from README)
- **Note:** Animated demonstration of global atmospheric parameters at 200km altitude

---

## Additional Notes

### PyHC Status:
- **Registry:** PyHC Unevaluated Packages
- **Source:** https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_unevaluated.yml (lines 166-171)

### Repository Statistics (from SoMEF):
- **Stars:** 55
- **Forks:** 26
- **Created:** 2015-03-27
- **Last Updated:** 2025-11-06
- **Issue Tracker:** https://api.github.com/repos/space-physics/msise00/issues

### Build System:
- Uses "build-on-run" technique with Meson build system
- Automatically compiles Fortran code on first use
- Requires Fortran compiler (gfortran recommended)

### Dependencies:
- python-dateutil
- numpy
- xarray
- geomagindices>=1.4.0
- setuptools>=61.0.0
- wheel

### Optional Dependencies:
- **Tests:** pytest, netCDF4
- **Plotting:** matplotlib, astropy, pymap3d
- **Linting:** flake8, mypy, types-python-dateutil

### Command Line Interface:
- Available via `msise00` command
- Supports time series, altitude profiles, and spatial grids
- Can output NetCDF4 files

### Cross-Platform Compatibility:
- Python >= 3.9 required
- Tested on Python 3.9 and 3.13
- Works on Linux, macOS, Windows
- Requires Fortran compiler installation

---

## Metadata Sources Summary

1. **DataCite API** (10.5281/zenodo.595393): DOI, basic metadata, authors, license, version, publisher
2. **Zenodo API** (record 14532758): Concept DOI, code repository URL, version details, custom metadata
3. **SoMEF**: Repository statistics, programming languages, releases, dependencies, keywords
4. **PyHC Registry** (unevaluated): Package listing, contact, keywords, documentation URL
5. **Manual Examination:**
   - README.md: Description, usage examples, reference information, units
   - LICENSE.txt: MIT License, copyright holder (SciVision, Inc.)
   - pyproject.toml: Dependencies, classifiers, Python version requirements, package name
   - .github/workflows/ci.yml: Operating systems, testing configuration
