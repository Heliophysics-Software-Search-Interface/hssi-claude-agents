# HSSI Metadata Extraction Results

**Repository:** https://github.com/sunpy/pyflct
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found - No DOI exists for this software package

**Note:** No CITATION.cff, .zenodo.json, or DOI badges found in repository

### 3. Code Repository (MANDATORY)
https://github.com/sunpy/pyflct

**Source:** GitHub repository URL

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics

**Source:** Analysis of code functionality. The software performs Fourier Local Correlation Tracking (FLCT) to analyze sequences of images (particularly magnetograms) to determine velocity flow fields between successive observations. It processes image data to track movements and generates 2D visualizations of flow fields.

### 5. Related Region (MANDATORY)
- Solar Environment

**Source:** Documentation and reference papers indicate this software is used for analyzing solar photosphere magnetograms and tracking magnetic field evolution on the Sun's surface.

### 6. Authors (MANDATORY)

**Author 1:**
- **Authors:** The SunPy Developers
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** setup.cfg metadata

**Note:** Author email (sunpy@googlegroups.com) is a mailing list. Primary maintainer contact is Nabil Freij (from PyHC registry).

### 7. Software Name (MANDATORY)
pyflct

**Source:** Repository name, setup.cfg, PyHC registry

### 8. Description (MANDATORY)
pyflct is a Python wrapper that allows users to perform Fourier Local Correlation Tracking (FLCT). The C-based implementation of the FLCT algorithm is developed by George H. Fisher and Brian T. Welsch. FLCT is used to estimate horizontal flow velocities on the Sun's surface by analyzing sequences of magnetic field images (magnetograms) taken at closely spaced time intervals. The software tracks magnetic field evolution at the photosphere, horizontal plasma motions, and active region dynamics. The derived flow velocities contribute to electric field inversions in the solar photosphere, data-driven simulations of solar corona behavior, studies of magnetic flux transport and emergence, and space weather forecasting models.

**Source:** README.rst, documentation, PyHC registry, and analysis of reference papers

### 9. Concise Description (OPTIONAL)
A Python wrapper for Fourier Local Correlation Tracking to estimate flow velocities from sequences of solar magnetogram images.

**Source:** Condensed from full description

### 10. Publication Date (RECOMMENDED)
2020-04-02

**Source:** GitHub API (repository creation date from SoMEF output)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Since no DOI exists, the repository host is the publisher

### 12. Version (RECOMMENDED)

**Current Version:**
- **Version Number:** v0.3.1
- **Version Date:** 2024-07-31
- **Version Description:** Bug fixes to resolve builds on conda-forge
- **Version PID:** Not found

**Source:** Git tags, CHANGELOG.rst

**Note:** Previous versions include v0.3.0 (2024-07-23), v0.2.4 (2023-11-27), v0.2.3 (2022-05-24), v0.2.2 (2021-04-01), v0.2.1 (2020-05-08), v0.2.0 (2020-05-08), v0.1.0 (2020-05-01)

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- C
- Cython

**Source:** SoMEF output (GitHub API language statistics), setup.cfg indicates Python >=3.10 required

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.3847/1538-4365/ab8303

**Citation:** Fisher et al., ApJS 248, 1, (2020)

**Source:** Documentation (docs/index.rst) lists this as the most recent reference paper for the FLCT algorithm

**Note:** Additional reference papers:
- Welsch et al., ApJ 610, 1148, (2004): https://doi.org/10.1086/421767
- Fisher & Welsch, PASP 383, 373, (2008): https://arxiv.org/abs/0712.4289

### 15. License (RECOMMENDED)
- **License:** GNU Lesser General Public License v2.1 or later (LGPLv2+)
- **License URI:** https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html

**Source:** setup.cfg, LICENSE.rst, SoMEF output, README.rst

**Note:** License file is available at LICENSE.rst in repository

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- solar
- wrapper
- data_analysis
- FLCT
- Fourier Local Correlation Tracking
- magnetogram
- photosphere
- velocity tracking
- flow field
- image processing

**Source:** PyHC registry keywords (solar, wrapper, specific, data_analysis) supplemented with domain-specific terms from documentation and analysis

### 17. Data Sources (OPTIONAL)
Observatory/Mission-specific

**Source:** Inferred from documentation - FLCT is commonly used with solar magnetogram data from missions like SDO/HMI, but the software itself is mission-agnostic and can work with any appropriately formatted image sequence data

### 18. Input File Formats (RECOMMENDED)
- Other (binary .dat files)

**Source:** Code analysis (pyflct/utils.py) shows functions read_2_images and read_3_images that read binary .dat files. The software also accepts numpy arrays as direct input.

**Note:** The .dat format is specific to the FLCT C library. Python users typically work with numpy arrays which can be loaded from various formats (FITS, etc.) before passing to pyflct.

### 19. Output File Formats (RECOMMENDED)
- Other (binary .dat files)

**Source:** Code analysis (pyflct/utils.py) shows functions write_2_images and write_3_images that write binary .dat files. The software outputs numpy arrays which can be saved in any standard format.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source:** setup.cfg classifiers, README.rst installation instructions

**Note:** Windows support is officially through Conda only. Linux and Mac support installation via pip with pre-compiled binary wheels.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64

**Source:** Inferred from pyproject.toml cibuildwheel configuration showing manylinux_2_28 for Linux and macOS builds with MACOSX_DEPLOYMENT_TARGET="12.0" (which supports both Intel and Apple Silicon)

### 22. Related Phenomena (OPTIONAL)
- Solar Flares
- Coronal Mass Ejections
- Solar Corona

**Source:** Inferred from description and reference papers - FLCT is used to track magnetic field evolution which is relevant to understanding solar flares, CMEs, and coronal dynamics

### 23. Development Status (RECOMMENDED)
Active

**Source:** setup.cfg classifier "Development Status :: 5 - Production/Stable" and recent commit activity (last updated 2025-10-06 per SoMEF)

### 24. Documentation (RECOMMENDED)
https://pyflct.readthedocs.io/en/latest/

**Source:** README.rst, SoMEF output, setup.cfg url field (https://docs.sunpy.org/projects/pyflct/)

**Note:** Documentation is hosted on Read the Docs

### 25. Funder (OPTIONAL)
Not found

**Source:** No funding information in repository files

### 26. Award Title (OPTIONAL)
Not found

**Source:** No award information in repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Welsch et al., ApJ 610, 1148, (2004): https://doi.org/10.1086/421767
- Fisher & Welsch, PASP 383, 373, (2008): https://arxiv.org/abs/0712.4289

**Source:** Documentation (docs/index.rst)

**Note:** These are additional reference papers for the FLCT algorithm beyond the main reference publication listed in field 14

### 28. Related Datasets (OPTIONAL)
Not found

**Source:** No specific datasets mentioned in repository

**Note:** The software is designed to work with solar magnetogram data, but no specific dataset DOIs are provided

### 29. Related Software (OPTIONAL)
- SunPy: https://github.com/sunpy/sunpy
- NDCube: https://github.com/sunpy/ndcube
- Another version of pyflct: https://github.com/PyDL/pyflct

**Source:** README.rst indicates this is part of the SunPy ecosystem (powered by SunPy badge), uses SunPy-related tooling (sunpy-sphinx-theme), and documentation mentions an alternative pyflct implementation

**Note:** This package is affiliated with the SunPy project and follows SunPy development guidelines

### 30. Interoperable Software (OPTIONAL)
- SunPy: https://github.com/sunpy/sunpy
- NumPy: https://numpy.org
- Matplotlib: https://matplotlib.org

**Source:** Dependencies listed in setup.cfg and examples show integration with numpy (required dependency) and matplotlib (used in examples for visualization)

### 31. Related Instruments (OPTIONAL)
Not found

**Source:** The software is instrument-agnostic and can work with any image sequence data

**Note:** Commonly used with solar magnetograph instruments like SDO/HMI, but not limited to any specific instrument

### 32. Related Observatories (OPTIONAL)
Not found

**Source:** The software is mission-agnostic

**Note:** Commonly used with Solar Dynamics Observatory (SDO) data and other solar observatories, but not limited to any specific mission

### 33. Logo (OPTIONAL)
Not found

**Source:** No logo file found in repository

---

## Metadata Sources Summary

**Automated Extraction:**
1. **SoMEF:** Successfully extracted repository metadata, programming languages, license information, dates, and documentation links
2. **PyHC Registry:** Found entry in community packages registry with keywords and quality ratings
3. **DataCite/Zenodo APIs:** Not applicable - no DOI exists for this package

**Manual Extraction:**
1. **Repository Files:** README.rst, setup.cfg, setup.py, pyproject.toml, CHANGELOG.rst, LICENSE.rst
2. **Code Analysis:** pyflct/__init__.py, pyflct/flct.py, pyflct/utils.py, examples/
3. **Documentation:** docs/index.rst, installation instructions
4. **Git History:** Tags for version information
5. **External References:** Analysis of reference publication (Fisher et al. 2020) for understanding software applications

---

## Notes

1. **No DOI Available:** This package does not have a persistent identifier (DOI). Consider registering with Zenodo through GitHub integration to obtain a concept DOI and version-specific DOIs for better citation and discovery.

2. **PyHC Affiliation:** This package is listed in the PyHC (Python in Heliophysics Community) community packages registry with "Good" ratings for documentation, testing, software maturity, Python 3 support, and license. The community rating is "Partially met."

3. **SunPy Affiliation:** This is an affiliated package of the SunPy project and follows SunPy development practices. It is maintained by The SunPy Developers with Nabil Freij as the primary contact.

4. **Active Development:** The package is in active development with the latest release (v0.3.1) from July 2024. Python 3.10+ is required.

5. **C Extension:** The core FLCT algorithm is implemented in C (by George H. Fisher and Brian T. Welsch), with this package providing a Python wrapper via Cython for ease of use in Python workflows.

6. **File Format Specificity:** The native .dat file format is specific to the original FLCT C implementation. Most Python users will work with numpy arrays loaded from standard solar physics file formats (like FITS) and can use pyflct without directly handling .dat files.

7. **Operating System Support:** Cross-platform with pre-built wheels for Linux and macOS (pip installable), and Conda support for Windows.
