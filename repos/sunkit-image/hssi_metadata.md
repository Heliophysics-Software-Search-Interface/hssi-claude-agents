# HSSI Metadata Extraction Results

**Repository:** https://github.com/sunpy/sunkit-image
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**DOI:** https://doi.org/10.5281/zenodo.5715430
**Source:** Concept DOI from Zenodo (provided by user)

### 3. Code Repository (MANDATORY)
**URL:** https://github.com/sunpy/sunkit-image
**Source:** Repository URL

### 4. Software Functionality (MANDATORY)
**Selected Categories:**
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:Wavelet Analysis
- Data Visualization:2D Graphics

**Source:** Analysis of repository modules and documentation. The package provides:
- Image processing algorithms (MGN, radial filters, enhancement)
- Feature detection (swirl detection via ASDA, sunspot tracking via STARA, granule segmentation)
- Structure tracing (loop tracing)
- Time series analysis (cross-correlation, time lag computation)
- Wavelet analysis (WOW - Wavelets Optimized Whitening)
- Visualization capabilities (2D plotting in examples)

### 5. Related Region (MANDATORY)
**Selected Category:** Solar Environment

**Source:** Package description states it is "a toolbox for solar physics image processing" and all functionality is specific to solar observations.

### 6. Authors (MANDATORY)

**From DataCite/Zenodo (v0.6.1):**

1. **Nabil Freij**
   - Affiliation: SETI Institute & LMSAL (@LM-SAL)

2. **Jack Ireland**
   - Affiliation: Not provided in DataCite

3. **Stuart Mumford**
   - Affiliation: Aperio Software

4. **Will Barnes**
   - Affiliation: American University

5. **David Stansby**
   - Affiliation: UCL

6. **Vatsalya Chaubey**
   - Affiliation: Not provided in DataCite

7. **Jayraj Dulange**
   - Affiliation: Not provided in DataCite

8. **Dr. Gilly**
   - Affiliation: Southwest Research Institute

9. **Laura Hayes**
   - Affiliation: Not provided in DataCite

10. **Ghaithq**
    - Affiliation: Not provided in DataCite

11. **Abinash Mahapatra**
    - Affiliation: Not provided in DataCite

12. **Leah Zuckerman**
    - Affiliation: Not provided in DataCite

13. **Saksham Alok**
    - Affiliation: Not provided in DataCite

14. **frederic-auchere**
    - Affiliation: Not provided in DataCite

15. **Jeffrey Aaron Paul**
    - Affiliation: Not provided in DataCite

16. **Matt Wentzel-Long**
    - Affiliation: Not provided in DataCite

17. **P. L. Lim**
    - Affiliation: Space Telescope Science Institute

18. **Samuel Bennett**
    - Affiliation: University of Sheffield

19. **bberkeyU**
    - Affiliation: Not provided in DataCite

20. **Michael Kirk**
    - Affiliation: NASA/GSFC

**Note:** Authors listed above are from the v0.6.1 Zenodo release. The pyproject.toml lists "The SunPy Community" as the primary author contact.

**Source:** DataCite API, Zenodo API, pyproject.toml

### 7. Software Name (MANDATORY)
**Name:** sunkit-image

**Source:** Repository name, pyproject.toml, SoMEF, PyHC registry

### 8. Description (MANDATORY)
**Description:** sunkit-image is an open-source toolbox for solar physics image processing. It is an experimental library for solar physics specific image processing routines. The package contains image processing algorithms that have been published in the literature, including Multi-scale Gaussian Normalization (MGN), radial gradient filters (FNRGF, NRGF, RHEF), Automated Swirl Detection Algorithm (ASDA), Sunspot Tracking And Recognition Algorithm (STARA), granule segmentation, loop/structure tracing, image coalignment routines, time lag cross-correlation analysis, and Wavelets Optimized Whitening (WOW).

**Source:** README.rst, GitHub description, SoMEF, analysis of modules

### 9. Concise Description (OPTIONAL)
**Concise Description:** A image processing toolbox for Solar Physics

**Source:** pyproject.toml, GitHub API

### 10. Publication Date (RECOMMENDED)
**Date:** 2017-11-01

**Source:** SoMEF (date_created from GitHub API)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API

### 12. Version (RECOMMENDED)

**Latest Version (v0.6.1):**
- **Version Number:** v0.6.1
- **Version Date:** 2025-02-20
- **Version Description:** Breaking changes: Removed "inplace" method for radial.rhef; Changed default rank method for radial.rhef from 'numpy' to 'scipy'. New features: Added "none" method to radial.rhef to allow bypassing the radial filter. Bug fixes: Fixed NaN handling in radial.rhef.
- **Version PID:** https://doi.org/10.5281/zenodo.15619797

**Source:** Git tags, CHANGELOG.rst, Zenodo API

### 13. Programming Language (RECOMMENDED)
**Languages:**
- Python 3.x

**Source:** pyproject.toml (requires Python >=3.12), SoMEF, PyHC registry

### 14. Reference Publication (RECOMMENDED)
**Reference Publication:** Not found

**Source:** No reference publication DOI found in DataCite relatedIdentifiers, CITATION.cff file not present

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://opensource.org/licenses/BSD-2-Clause
- **SPDX Identifier:** BSD-2-Clause

**Source:** DataCite API, SoMEF, LICENSE.rst file, pyproject.toml

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Keywords:**
- solar physics
- solar
- science
- image analysis
- data_analysis

**Source:** pyproject.toml, SoMEF, PyHC registry (combines "solar", "general", "data_analysis")

### 17. Data Sources (OPTIONAL)
**Data Sources:** Not explicitly specified

**Note:** The software is designed to work with solar imaging data but does not restrict to specific data sources. Examples in the repository use data from missions like SDO/AIA.

### 18. Input File Formats (RECOMMENDED)
**Formats:**
- FITS

**Source:** Analysis of dependencies and code. The package depends on sunpy[map] which primarily works with FITS files for solar images. Examples use FITS format.

### 19. Output File Formats (RECOMMENDED)
**Formats:**
- FITS
- Image formats (PNG, JPEG, etc. via matplotlib)

**Source:** The package can output processed maps (FITS format via sunpy) and visualization outputs via matplotlib.

### 20. Operating System (RECOMMENDED)
**Operating Systems:**
- Linux
- Mac
- Windows

**Source:** CI configuration (.github/workflows/ci.yml) shows testing on linux, windows, and macos. pyproject.toml classifies as "Operating System :: OS Independent"

### 21. CPU Architecture (RECOMMENDED)
**Architecture:** CPU Independent

**Source:** Pure Python package with no architecture-specific compiled code. Uses numpy/scipy which support multiple architectures.

### 22. Related Phenomena (OPTIONAL)
**Phenomena:**
- Solar Corona
- Solar Flares
- Coronal Mass Ejections

**Source:** Inferred from package functionality. The image processing techniques (radial filters, enhancement, loop tracing, swirl detection) are commonly used for studying coronal features, flares, and CMEs.

### 23. Development Status (RECOMMENDED)
**Status:** Active

**Source:** SoMEF repository status, PyHC registry (software_maturity: Good), recent commit activity (last updated 2025-10-07), and pyproject.toml classifies as "Development Status :: 3 - Alpha"

### 24. Documentation (RECOMMENDED)
**URL:** https://docs.sunpy.org/projects/sunkit-image

**Source:** pyproject.toml, PyHC registry, SoMEF

### 25. Funder (OPTIONAL)
**Funder:** Not found

**Source:** No funding information in DataCite fundingReferences

### 26. Award Title (OPTIONAL)
**Award:** Not found

**Source:** No award information available

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Publications:** Not found

**Source:** No related publications found in DataCite relatedIdentifiers

### 28. Related Datasets (OPTIONAL)
**Datasets:** Not found

**Source:** No related datasets found in DataCite relatedIdentifiers

### 29. Related Software (OPTIONAL)
**Software:**
- sunpy (https://github.com/sunpy/sunpy) - Core dependency
- astropy
- numpy
- scipy
- scikit-image
- matplotlib
- watroo (optional dependency for WOW functionality)

**Source:** pyproject.toml dependencies, SoMEF requirements

### 30. Interoperable Software (OPTIONAL)
**Software:**
- sunpy (https://github.com/sunpy/sunpy)
- ndcube
- astropy

**Source:** The package is designed as part of the SunPy ecosystem and works seamlessly with sunpy Map objects, ndcube objects, and astropy utilities.

### 31. Related Instruments (OPTIONAL)
**Instruments:**
- SDO/AIA (Solar Dynamics Observatory / Atmospheric Imaging Assembly)

**Note:** While the package is instrument-agnostic and designed for general solar image processing, the examples and some algorithms (like RHEF) are commonly used with or optimized for SDO/AIA data.

**Source:** Analysis of examples and CHANGELOG.rst references to AIA

### 32. Related Observatories (OPTIONAL)
**Observatories:**
- SDO (Solar Dynamics Observatory)
- Hinode

**Note:** The package is designed for general solar physics image processing but examples and documentation reference SDO and Hinode data.

**Source:** Analysis of examples, documentation, and related packages (XRTpy for Hinode mentioned in SunPy ecosystem)

### 33. Logo (OPTIONAL)
**Logo:** Not found

**Source:** No logo field in PyHC registry or repository

---

## Metadata Sources Summary

1. **DataCite API** - Authors, publisher, license, version, DOI, description
2. **Zenodo API** - Latest version DOI, code repository URL, version metadata
3. **SoMEF** - Description, keywords, license, programming languages, documentation URL, repository metadata
4. **PyHC Registry** - Package name, description, documentation URL, keywords, development status ratings
5. **Repository Files** - pyproject.toml (dependencies, keywords, license, Python version requirements), CHANGELOG.rst (version descriptions), LICENSE.rst (license text), README.rst (description)
6. **Git Repository** - Version tags, release dates
7. **CI Configuration** - Operating system support (Linux, Mac, Windows)
8. **Code Analysis** - Software functionality categories based on module analysis (asda.py, coalignment.py, enhance.py, granule.py, radial.py, stara.py, time_lag.py, trace.py)

---

## Notes

- **MANDATORY fields completed:** Submitter (to be filled by user), Code Repository, Software Functionality, Related Region, Authors, Software Name, Description
- **RECOMMENDED fields completed:** Persistent Identifier, Publication Date, Publisher, Version, Programming Language, License, Input/Output File Formats, Operating System, CPU Architecture, Development Status, Documentation
- **PyHC Package:** Yes - sunkit-image is listed in the PyHC community packages registry
- **SunPy Affiliated Package:** Yes - This is an official SunPy affiliated package, part of the broader SunPy ecosystem
