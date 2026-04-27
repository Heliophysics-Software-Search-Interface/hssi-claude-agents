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
- **Data Visualization** - Creates magnetic field visualizations
- **Data Visualization:2D Graphics** - Generates contour and pcolor plots
- **Data Processing and Analysis** - Provides geomagnetic field calculations
- **Data Processing and Analysis:Analysis** - Analyzes magnetic field at various locations

**Source:** Repository code examination (base.py, __main__.py, plots.py), README description

### 5. Related Region (MANDATORY)
- **Earth Atmosphere** - Used for ionosphere/thermosphere/mesosphere research (confirmed by PyHC categorization and pyproject.toml Atmospheric Science classifier)

**Source:** PyHC registry keywords ("ionosphere_thermosphere_mesosphere"), pyproject.toml classifier, software description and purpose

### 6. Authors (MANDATORY)
- **Author Name:** Michael Hirsch
- **Author Identifier:** Not found in repository
- **Affiliation:**
  - **Organization:** Scivision, Inc. (from LICENSE.txt copyright notice)
  - **Affiliation Identifier:** Not found

**Source:** PyHC registry contact field, LICENSE.txt

**Note:** The DataCite API only listed "Michael" without surname; the full name "Michael Hirsch" was found in the PyHC registry as the contact person.

### 7. Software Name (MANDATORY)
- **Name:** IGRF-13
- **Full Title:** IGRF 13 in Python (from README)
- **Package Name:** igrf (from pyproject.toml)

**Source:** pyproject.toml, SoMEF, README.md, PyHC registry

### 8. Description (MANDATORY)
International Geomagnetic Reference Field: IGRF13 in object-oriented Python or Matlab. The current public Python API and build path target IGRF13; IGRF11 and IGRF12 source files are retained in the repository but are not exposed by the current driver. The software provides calculations of Earth's main magnetic field components (north, east, down, total intensity) as well as magnetic inclination and declination at specified geographic coordinates and altitudes. It uses a Fortran backend with Python and Matlab interfaces, and outputs results as xarray Datasets for easy integration with other geoscience tools. The included IGRF13 synthesis routine is valid through 2025.0, with reduced-accuracy warnings for later dates.

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
- **Fortran90** - Backend computational engine includes the current IGRF13 driver in Fortran 90 format
- **Fortran77** - Backend also includes fixed-form Fortran source files for IGRF model calculations
- **MATLAB** - Alternative interface provided

**Source:** GitHub API via SoMEF, pyproject.toml, CI configuration, README.md, src/igrf/fortran files

### 14. Reference Publication (RECOMMENDED)
Not found

**Note:** The README references the original IGRF Fortran code sources but no specific publication describing this Python implementation.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html
- **SPDX ID:** MIT

**Source:** LICENSE.txt

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
Not applicable - The current IGRF13 driver takes parameters directly via function calls or CLI arguments rather than user-supplied input files. IGRF13 coefficients are embedded in the Fortran source used by the current build path.

**Note:** Users provide datetime, latitude, longitude, and altitude as function parameters.

### 19. Output File Formats (RECOMMENDED)
Not applicable for file output. The software returns xarray.Dataset objects in memory, which users can subsequently save in various formats supported by xarray (netCDF, Zarr, etc.).

**Source:** Code examination (base.py)

### 20. Operating System (RECOMMENDED)
- **Operating System Independent** - Declared in pyproject.toml classifier
- **Linux** - Installation documented in README and tested on ubuntu-24.04 in CI
- **Mac** - Installation documented in README and tested on macos-latest in CI
- **Windows** - Installation documented in README; build code includes Windows-specific MinGW handling

**Source:** pyproject.toml classifier, CI configuration (.github/workflows/ci.yml), base.py code (Windows-specific logic), README installation instructions

**Note:** Requires a Fortran compiler (gfortran) on all platforms.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** - Python/Fortran source has no architecture-specific code; requires a compatible Python runtime, CMake, and Fortran compiler

**Source:** Repository source layout, pyproject.toml, README build requirements

### 22. Related Phenomena (OPTIONAL)
Not found in repository metadata.

**Potential values based on usage:** The software could be relevant to phenomena affected by Earth's magnetic field, but no specific phenomena are explicitly mentioned in the repository.

### 23. Development Status (RECOMMENDED)
- **Inactive** - Package has reached a stable, usable state but does not show recent active release development

**Source:** Last upstream commit on main is 2024-08-23; latest release is v13.0.2 from 2021-10-11; pyproject.toml classifier is "Development Status :: 5 - Production/Stable"

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
- **Publication DOI:** https://doi.org/10.1186/s40623-020-01288-x
- **Title:** International Geomagnetic Reference Field: the thirteenth generation

**Note:** This publication describes the IGRF13 scientific model, not this specific Python/MATLAB wrapper. The README references the original IGRF Fortran code sources from NOAA/NGDC.

### 28. Related Datasets (OPTIONAL)
Not found

**Note:** The software uses IGRF model coefficients but these are embedded in the package, not referenced as external datasets.

### 29. Related Software (OPTIONAL)
**Dependencies:**
- **xarray:** https://github.com/pydata/xarray - For dataset output format
- **NumPy:** https://github.com/numpy/numpy - For numerical operations
- **Matplotlib:** https://github.com/matplotlib/matplotlib - For optional visualization
- **CMake:** https://github.com/Kitware/CMake - Build system used to compile the Fortran backend

**Source:** pyproject.toml dependencies, SoMEF requirements

**Reference sources for IGRF model:**
- IGRF13 Fortran code: http://www.ngdc.noaa.gov/IAGA/vmod/igrf13.f
- IGRF12 Fortran code: http://www.ngdc.noaa.gov/IAGA/vmod/igrf12.f
- IGRF11 Fortran code: http://www.ngdc.noaa.gov/IAGA/vmod/igrf11.f

### 30. Interoperable Software (OPTIONAL)
- **xarray:** https://docs.xarray.dev/ - Python API returns `xarray.Dataset` objects
- **MATLAB:** https://www.mathworks.com/products/matlab.html - Repository includes a MATLAB interface that calls the Python package

**Source:** README example, base.py return types, +igrf/igrf.m

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
- Uses modern Python packaging standards (pyproject.toml) and includes CI configuration
- The author "Michael Hirsch" is associated with the "space-physics" GitHub organization and maintains numerous other space physics Python packages
- Download statistics from PyPI show active usage (per README badge)
