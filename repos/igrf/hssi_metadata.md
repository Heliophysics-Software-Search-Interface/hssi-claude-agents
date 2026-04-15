# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/igrf
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.1184871
- **Note:** This is the concept DOI for all versions (from Zenodo badge in README)

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/space-physics/igrf
- **Source:** Repository URL, verified via DataCite and SoMEF

### 4. Software Functionality (MANDATORY)
Based on comprehensive repository analysis, the following functionalities apply:
- **Models and Simulations** - Primary functionality
- **Models and Simulations:Empirical** - IGRF is an empirical geomagnetic field model
- **Models and Simulations:Physics-Based** - Based on spherical harmonic analysis
- **Coordinate Transforms** - Handles geographic coordinate transformations
- **Data Visualization** - Creates magnetic field visualizations
- **Data Visualization:2D Graphics** - Generates contour and pcolor plots
- **Data Processing and Analysis** - Provides geomagnetic field calculations
- **Data Processing and Analysis:Analysis** - Analyzes magnetic field at various locations

**Source:** Repository code examination (base.py, plots.py), README description

### 5. Related Region (MANDATORY)
- **Earth Magnetosphere** - Primary region; IGRF models Earth's internal magnetic field
- **Earth Atmosphere** - Secondary region; used for ionosphere/thermosphere/mesosphere research (confirmed by PyHC categorization)

**Source:** PyHC registry keywords ("ionosphere_thermosphere_mesosphere"), software description and purpose

### 6. Authors (MANDATORY)
- **Author Name:** Michael Hirsch
- **Author Identifier:** Not found in repository
- **Affiliation:**
  - **Organization:** Scivision, Inc. (from LICENSE.txt copyright notice)
  - **Affiliation Identifier:** Not found

**Source:** PyHC registry contact field, LICENSE.txt

**Note:** The DataCite API only listed "Michael" without surname; the full name "Michael Hirsch" was found in the PyHC registry as the contact person.

### 7. Software Name (MANDATORY)
- **Name:** igrf
- **Full Title:** IGRF 13 in Python (from README)
- **Alternative Name:** IGRF-13 (from PyHC registry)

**Source:** pyproject.toml, SoMEF, README.md, PyHC registry

### 8. Description (MANDATORY)
International Geomagnetic Reference Field: IGRF13 in object-oriented Python or Matlab. IGRF13, IGRF12, IGRF11 models with simple object-oriented Python interface. The software provides calculations of Earth's main magnetic field components (north, east, down, total intensity) as well as magnetic inclination and declination at specified geographic coordinates and altitudes. It uses a Fortran backend with Python and Matlab interfaces, and outputs results as xarray Datasets for easy integration with other geoscience tools.

**Source:** Combined from README.md, pyproject.toml, and repository code analysis

### 9. Concise Description (OPTIONAL)
International Geomagnetic Reference Field (IGRF13) model with object-oriented Python and Matlab interfaces for calculating Earth's magnetic field components.

**Source:** Condensed from description

### 10. Publication Date (RECOMMENDED)
- **Date:** 2015-03-29
- **Source:** Repository creation date from GitHub API via SoMEF, confirmed by first git commit

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API, Zenodo DOI

### 12. Version (RECOMMENDED)
**Latest Version (v13.0.2):**
- **Version Number:** v13.0.2
- **Version Date:** 2021-10-11
- **Version Description:** Use Matlab test unit class. Attempt to make CMake build more robust from Python.
- **Version PID:** https://doi.org/10.5281/zenodo.5560949

**Source:** DataCite API, Zenodo API, Git tags, SoMEF releases, __init__.py

**Additional Version Information:**
- v13.0.1 (2021-10-11): Update syntax for xarray
- v13.0.0 (2020-08-24): Update to use IGRF13 model
- Multiple earlier versions available (v1.3.6, v1.3.5, v1.3.4, v1.3.2, v1.3.1, v1.3.0, v1.2.1, v1.2.0)

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** - Primary interface (requires Python >= 3.9 based on pyproject.toml)
- **Fortran** - Backend computational engine (Fortran code for IGRF calculations)
- **MATLAB** - Alternative interface provided

**Source:** GitHub API via SoMEF, pyproject.toml, CI configuration, README.md

### 14. Reference Publication (RECOMMENDED)
Not found

**Note:** The README references the original IGRF Fortran code sources but no specific publication describing this Python implementation.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://api.github.com/licenses/mit
- **SPDX ID:** MIT

**Source:** GitHub API via SoMEF, LICENSE.txt

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
From multiple sources:
- fortran
- geomagnetic
- igrf
- igrf12
- igrf13
- matlab
- matlab-python-interface
- python
- ionosphere_thermosphere_mesosphere (from PyHC)
- specific (from PyHC)

**Source:** GitHub topics via SoMEF, pyproject.toml, PyHC registry

### 17. Data Sources (OPTIONAL)
Not applicable - This is a model/calculation tool that generates magnetic field values from the IGRF model coefficients, not a data retrieval tool.

### 18. Input File Formats (RECOMMENDED)
Not applicable - The software uses embedded coefficient files (IGRF12.COF, WMM2015.COF) and takes parameters directly via function calls rather than input files.

**Note:** Users provide datetime, latitude, longitude, and altitude as function parameters.

### 19. Output File Formats (RECOMMENDED)
Not applicable for file output. The software returns xarray.Dataset objects in memory, which users can subsequently save in various formats supported by xarray (netCDF, Zarr, etc.).

**Source:** Code examination (base.py)

### 20. Operating System (RECOMMENDED)
- **Linux** - Tested on ubuntu-24.04 in CI
- **Mac** - Tested on macos-latest in CI
- **Windows** - Supported (code includes Windows-specific handling for MinGW Makefiles)

**Source:** CI configuration (.github/workflows/ci.yml), base.py code (Windows-specific logic), README installation instructions

**Note:** Requires a Fortran compiler (gfortran) on all platforms.

### 21. CPU Architecture (RECOMMENDED)
- **x86-64** - Primary architecture based on CI testing
- **CPU Independent** - Python/Fortran code should be portable to other architectures with appropriate Fortran compiler

**Source:** Inferred from CI configuration and programming languages

### 22. Related Phenomena (OPTIONAL)
Not found in repository metadata.

**Potential values based on usage:** The software could be relevant to phenomena affected by Earth's magnetic field, but no specific phenomena are explicitly mentioned in the repository.

### 23. Development Status (RECOMMENDED)
- **Active** - Package has reached stable, usable state and is being actively developed

**Source:** Recent commit activity (last commit 2024-08-23), pyproject.toml classifier "Development Status :: 5 - Production/Stable", active release history

### 24. Documentation (RECOMMENDED)
- **URL:** https://github.com/space-physics/igrf

**Note:** Documentation is embedded in the README.md file at the repository URL. No separate documentation site was found.

**Source:** Repository examination, no ReadTheDocs or similar configuration found

### 25. Funder (OPTIONAL)
Not found

**Source:** No funding information in DataCite API or repository

### 26. Award Title (OPTIONAL)
Not found

**Source:** No award information in DataCite API or repository

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

**Note:** No related publications found in DataCite API or repository. The README references the original IGRF Fortran code sources from NOAA/NGDC.

### 28. Related Datasets (OPTIONAL)
Not found

**Note:** The software uses IGRF model coefficients but these are embedded in the package, not referenced as external datasets.

### 29. Related Software (OPTIONAL)
**Dependencies:**
- **xarray** - For dataset output format
- **numpy** - For numerical operations
- **matplotlib** - For visualization (optional)

**Source:** pyproject.toml dependencies, SoMEF requirements

**Reference sources for IGRF model:**
- IGRF13 Fortran code: http://www.ngdc.noaa.gov/IAGA/vmod/igrf13.f
- IGRF12 Fortran code: http://www.ngdc.noaa.gov/IAGA/vmod/igrf12.f
- IGRF11 Fortran code: http://www.ngdc.noaa.gov/IAGA/vmod/igrf11.f

### 30. Interoperable Software (OPTIONAL)
Not found

**Note:** While the software uses xarray for data output (suggesting compatibility with the xarray ecosystem), no specific interoperability claims are made in the repository.

### 31. Related Instruments (OPTIONAL)
Not applicable

**Note:** IGRF is a general geomagnetic field model, not specific to any particular instrument.

### 32. Related Observatories (OPTIONAL)
Not applicable

**Note:** IGRF is a general geomagnetic field model based on global data, not specific to any particular observatory.

### 33. Logo (OPTIONAL)
- **URL:** https://www.ngdc.noaa.gov/IAGA/vmod/img/vmod_header.gif

**Source:** PyHC registry logo field

---

## Metadata Sources Summary

This metadata extraction combined information from:

1. **DataCite API** - DOI metadata, basic bibliographic information
2. **Zenodo API** - Version-specific information, concept DOI
3. **PyHC Unevaluated Registry** - Package name, contact, logo, keywords, description
4. **SoMEF** - Automated extraction from repository (languages, releases, keywords, license)
5. **Repository Files:**
   - README.md - Description, usage, installation, references
   - pyproject.toml - Package metadata, dependencies, classifiers
   - LICENSE.txt - License text, copyright holder
   - src/igrf/__init__.py - Version number
   - src/igrf/base.py - Core functionality analysis
   - src/igrf/plots.py - Visualization capabilities
   - .github/workflows/ci.yml - OS support, testing configuration
6. **Git Repository Analysis:**
   - Tags - Version history
   - Commit history - Development timeline and activity

---

## Notes

- This package is listed in the PyHC (Python in Heliophysics Community) unevaluated registry
- The software provides Python and Matlab interfaces to IGRF geomagnetic field models (versions 11, 12, and 13)
- Requires compilation of Fortran code using CMake and a Fortran compiler (gfortran)
- Uses modern Python packaging standards (pyproject.toml) and maintains active CI/CD
- The author "Michael Hirsch" is associated with the "space-physics" GitHub organization and maintains numerous other space physics Python packages
- Download statistics from PyPI show active usage (per README badge)
- The software has 73 stars and 29 forks on GitHub, indicating community interest and adoption
