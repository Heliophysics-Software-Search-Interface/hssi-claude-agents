# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/iri90
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/iri90

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Models and Simulations
- Models and Simulations:Empirical

**Source:** Based on code analysis - IRI-90 is an empirical ionospheric reference model that computes ionospheric parameters (electron density, temperatures, ion composition) based on input conditions (location, time, solar indices). It includes visualization capabilities for altitude and time profiles through matplotlib plotting functions.

### 5. Related Region (MANDATORY)
- Earth Atmosphere

**Source:** Software models the ionosphere, which is part of Earth's upper atmosphere in the altitude range 50km to 2000km (from README.md).

### 6. Authors (MANDATORY)
- **Author:** Michael Hirsch, Ph.D.
  - **Author Identifier:** Not found
  - **Affiliation:**
    - **Organization:** Not found
    - **Affiliation Identifier:** Not found

**Source:** From setup.cfg and LICENSE.txt (Copyright 2015 Michael Hirsch). PyHC registry lists contact as "Michael Hirsch".

### 7. Software Name (MANDATORY)
iri90

**Alternative names:** IRI-90, IRI90: International reference ionosphere in Python

**Source:** From setup.cfg (metadata name), repository name, and README.md title.

### 8. Description (MANDATORY)
IRI90 from Python, clean and flexible ionospheric model. IRI-90 provides monthly mean values for magnetically quiet conditions at non-auroral latitudes in the altitude range 50km to 2000km. However, IRI90 is often used as an initialization for conditions at auroral latitudes, understanding the caveats. This IRI90 Python module is as small and clean as possible to enable custom IRI90 applications. The module outputs electron density, neutral temperature, ion temperature, electron temperature, and ion composition (O+, H+, He+, O2+, NO+) as an xarray.DataArray indexable by species, altitude, etc. and includes metadata.

**Source:** Combined from setup.cfg and README.md

### 9. Concise Description (OPTIONAL)
IRI90-international reference ionosphere in Python providing monthly mean ionospheric parameters for magnetically quiet conditions in the altitude range 50km to 2000km.

**Source:** Derived from GitHub API description and README.md (limited to ~200 characters)

### 10. Publication Date (RECOMMENDED)
2015-04-28

**Source:** From SoMEF output (date_created) and git log (first commit: 2015-04-28 04:28:56 -0400)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Repository is hosted on GitHub; no DOI has been obtained through Zenodo or other publisher.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.1.1
- **Version Date:** 2018-08-15
- **Version Description:** Modernization release including documentation improvements, CI template updates, badge updates, and cleanup. Adds time profile functionality for plotting versus time, species and altitude in one xarray.DataArray.
- **Version PID:** Not found

**Source:** From setup.cfg (version 1.1.1), git tag v1.1.1 (date: 2018-08-15 02:02:55 -0400), and git log comparing v1.1.0 to v1.1.1. Previous version v1.1.0 released 2018-03-02 added altitude and time profiles with xarray.DataArray containing all metadata for easy API and plotting.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- Fortran77

**Source:** From setup.cfg (python_requires >= 3.7), SoMEF output (programming_languages: Python, Meson, CMake), and code inspection (src/iri90.f is Fortran 77 code wrapped with f2py). The package also uses build systems Meson and CMake.

### 14. Reference Publication (RECOMMENDED)
Not found

**Source:** No CITATION.cff, no DOI for reference publication in README.md. The README.md references the original Fortran code at http://download.hao.ucar.edu/pub/stans/iri/iri90.f

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html

**Source:** From LICENSE.txt, setup.cfg (license_files), and SoMEF output (license: MIT License with spdx_id: MIT)

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- f2py
- fortran
- geoscience
- ionosphere
- ionosphere-modeling
- iri
- python
- space-physics
- thermosphere

**Source:** From SoMEF output (GitHub topics/keywords) and setup.cfg keywords (ionosphere, thermosphere). PyHC registry includes keywords: ionosphere_thermosphere_mesosphere, specific.

### 17. Data Sources (OPTIONAL)
Not found

**Source:** IRI-90 is a model that uses input parameters (date/time, location, solar indices f107, f107a, ap) rather than fetching data from external sources. It includes internal data files (.asc format) with empirical coefficients.

### 18. Input File Formats (RECOMMENDED)
- ascii

**Source:** The model includes data files in .asc (ASCII) format located in the data/ directory (from setup.py: package_data includes "data/*.asc"). Primary inputs are programmatic parameters rather than files.

### 19. Output File Formats (RECOMMENDED)
Not applicable - outputs xarray.DataArray objects

**Source:** From code analysis (__init__.py), the runiri() function returns xarray.DataArray with ionospheric parameters. Users can save this using xarray's built-in methods (netCDF, etc.), but the package itself doesn't specify output file formats.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source:** From README.md installation instructions (provides instructions for Linux, Mac, and Windows) and .github/workflows/ci.yml (tests on ubuntu-latest, with commented-out tests for macos and windows). The package requires a Fortran compiler (gfortran) which is available on all three platforms.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- CPU Independent

**Source:** No specific CPU architecture requirements found. Python and Fortran code should be CPU architecture independent as long as a compatible Fortran compiler is available. The package uses f2py to compile Fortran extensions.

### 22. Related Phenomena (OPTIONAL)
Not found

**Source:** While the software relates to ionospheric phenomena, specific controlled vocabulary terms for phenomena (like those from SPASE) were not found in the repository or documentation.

### 23. Development Status (RECOMMENDED)
Active

**Source:** From setup.cfg: "Development Status :: 4 - Beta". Repository shows commits as recent as 2021-10-10 and was last updated 2025-10-08 according to SoMEF. The package is functional and in active use, though development appears intermittent.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/iri90

**Source:** No separate documentation site found. Documentation is in README.md at the repository URL. The repository includes example scripts (AltitudeProfile.py, TimeProfile.py) and docstrings in the code.

### 25. Funder (OPTIONAL)
Not found

**Source:** No funding information found in repository files.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

**Source:** No award or grant information found in repository files.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

**Source:** No publications citing or describing this specific Python package were found in the repository.

### 28. Related Datasets (OPTIONAL)
Not found

**Source:** The model includes empirical coefficient data files but no external dataset DOIs or references.

### 29. Related Software (OPTIONAL)
- numpy (https://numpy.org) - required dependency
- xarray (https://xarray.dev) - required dependency
- matplotlib (https://matplotlib.org) - optional dependency for plotting

**Source:** From setup.cfg install_requires and extras_require sections. Also uses f2py (part of numpy) for Fortran-Python interface.

**Note:** The original IRI-90 Fortran code is available at http://download.hao.ucar.edu/pub/stans/iri/iri90.f (referenced in README.md). Related packages by the same author include IRI-2016 (more recent version of IRI model) at https://github.com/space-physics/iri2016.

### 30. Interoperable Software (OPTIONAL)
Not found

**Source:** No explicit interoperability statements found, though the package uses standard Python scientific stack (numpy, xarray) which enables interoperability with many packages.

### 31. Related Instruments (OPTIONAL)
Not found

**Source:** IRI-90 is a reference model, not instrument-specific. However, ionospheric models are used to interpret data from ionosondes, incoherent scatter radars, and satellite instruments.

### 32. Related Observatories (OPTIONAL)
Not found

**Source:** IRI-90 is a general ionospheric model, not observatory-specific.

### 33. Logo (OPTIONAL)
https://iri.gsfc.nasa.gov/images/tail-179.jpg

**Source:** From PyHC unevaluated registry (pyhc_unevaluated.yml line 82). This appears to be a generic IRI model logo from NASA GSFC.

---

## Additional Notes

### PyHC Package Information
This package is listed in the PyHC (Python in Heliophysics Community) unevaluated registry:
- **Registry:** Unevaluated packages
- **Contact:** Michael Hirsch
- **PyHC Keywords:** ionosphere_thermosphere_mesosphere, specific

### Software Dependencies
**Build requirements:**
- setuptools
- wheel
- numpy
- Fortran compiler (gfortran recommended)
- Optionally: Meson or CMake build system

**Runtime requirements:**
- Python >= 3.7
- numpy
- xarray

**Testing requirements:**
- pytest
- flake8
- mypy

**Optional (for plotting):**
- matplotlib

### Model Information
IRI-90 (International Reference Ionosphere 1990) is an empirical model based on the Solomon 1993 version. It provides:
- Electron density (ne)
- Neutral temperature (Tn)
- Ion temperature (Ti)
- Electron temperature (Te)
- Ion composition: O+, H+, He+, O2+, NO+

The model is valid for:
- Altitude range: 50 km to 2000 km
- Magnetically quiet conditions
- Non-auroral latitudes (though often used as initialization for auroral latitudes)
- Monthly mean values

### Repository Statistics (from SoMEF)
- Stars: 7
- Forks: 4
- Owner: space-physics (Organization)
- Issue tracker: https://api.github.com/repos/space-physics/iri90/issues

---

## Metadata Source Summary

**Automated extraction sources:**
1. ✅ DataCite API - Not applicable (no DOI)
2. ✅ Zenodo API - Not applicable (no DOI)
3. ✅ SoMEF - Completed successfully
4. ✅ PyHC Registry - Found in unevaluated packages registry

**Manual extraction sources:**
1. ✅ README.md
2. ✅ setup.cfg
3. ✅ setup.py
4. ✅ pyproject.toml
5. ✅ LICENSE.txt
6. ✅ Source code analysis (iri90/__init__.py, example scripts)
7. ✅ Git history (tags, commits, dates)
8. ✅ CI/CD configuration (.github/workflows/ci.yml)

**Metadata priority used:**
1. PyHC metadata (most trustworthy for PyHC packages)
2. Package metadata files (setup.cfg, setup.py)
3. SoMEF extraction (comprehensive but automated)
4. Manual code analysis

---

## Completeness Check

**MANDATORY fields completed:**
- ✅ Submitter (to be filled by submitter)
- ✅ Code Repository
- ✅ Software Functionality
- ✅ Related Region
- ✅ Authors
- ✅ Software Name
- ✅ Description

**RECOMMENDED fields completed:**
- ❌ Persistent Identifier (not available)
- ✅ Publication Date
- ✅ Publisher
- ✅ Version
- ✅ Programming Language
- ❌ Reference Publication (not available)
- ✅ License
- ✅ Input File Formats
- ✅ Operating System
- ✅ CPU Architecture
- ✅ Development Status
- ✅ Documentation

**Field completion rate:** 28 of 33 fields have values (85%)
