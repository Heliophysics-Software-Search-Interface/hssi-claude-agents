# HSSI Metadata Extraction Results

**Repository:** https://github.com/sunpy/sunpy
**Extraction Date:** 2025-10-01

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Concept DOI:** https://doi.org/10.5281/zenodo.591887
- **Note:** This is the concept DOI for all versions of sunpy from Zenodo

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/sunpy/sunpy
- **Source:** Repository URL

### 4. Software Functionality (MANDATORY)
Based on comprehensive analysis of the codebase, documentation, and PyHC metadata, sunpy provides the following functionalities:

- **Coordinate Transforms**
- **Coordinate Transforms:Solar**
- **Coordinate Transforms:Heliospheric**
- **Data Processing and Analysis**
- **Data Processing and Analysis:Data Access and Retrieval**
- **Data Processing and Analysis:Analysis**
- **Data Processing and Analysis:Calibration**
- **Data Processing and Analysis:File Format Conversion**
- **Data Processing and Analysis:Image Processing**
- **Data Processing and Analysis:Time Series Analysis**
- **Data Processing and Analysis:Spectrogram**
- **Data Visualization**
- **Data Visualization:2D Graphics**
- **Data Visualization:Line Plots**
- **Data Visualization:Spectrogram**
- **Data Visualization:Movies**

**Note:** Functionality determined from:
- Module structure (coordinates, timeseries, map, visualization with animator submodule, net, io, image modules)
- PyHC keywords: 2D_graphics, coordinates, data_analysis, data_retrieval, fido, fits, heliosphere, image_processing, line_plots, netcdf, plotting, power_spectra, solar, time
- Documentation and repository examination
- Differential rotation calculations in physics module

### 5. Related Region (MANDATORY)
- **Solar Environment** (primary focus - solar physics data and phenomena)
- **Interplanetary Space** (heliosphere support based on PyHC keywords)

**Note:** Determined from package description "Python for Solar Physics", PyHC keywords "solar" and "heliosphere", and the solar-focused data sources supported (SDO, SOHO, GOES, etc.)

### 6. Authors (MANDATORY)

**Primary Author/Community:**
- **Authors:** The SunPy Community
- **Author Identifier:** Not available
- **Affiliation:**
  - **Organization:** Not specified
  - **Affiliation Identifier:** Not available

**Key Individual Authors** (from Zenodo v7.0.2 and CITATION.cff):

1. **Authors:** Stuart J. Mumford
   - **Author Identifier:** https://orcid.org/0000-0003-4217-4642
   - **Affiliation:**
     - **Organization:** Aperio Software Ltd.
     - **Affiliation Identifier:** Not available

2. **Authors:** Nabil Freij
   - **Author Identifier:** https://orcid.org/0000-0002-6253-082X
   - **Affiliation:**
     - **Organization:** SETI Institute & Lockheed Martin Solar and Astrophysics Laboratory
     - **Affiliation Identifier:** Not available

3. **Authors:** David Stansby
   - **Author Identifier:** https://orcid.org/0000-0002-1365-1908
   - **Affiliation:**
     - **Organization:** University College London
     - **Affiliation Identifier:** https://ror.org/02jx3x895

4. **Authors:** Steven Christe
   - **Author Identifier:** https://orcid.org/0000-0001-6127-795X
   - **Affiliation:**
     - **Organization:** NASA Goddard Space Flight Center
     - **Affiliation Identifier:** https://ror.org/0171mag52

5. **Authors:** Albert Y. Shih
   - **Author Identifier:** https://orcid.org/0000-0001-6874-2594
   - **Affiliation:**
     - **Organization:** NASA Goddard Space Flight Center
     - **Affiliation Identifier:** https://ror.org/0171mag52

6. **Authors:** Jack Ireland
   - **Author Identifier:** https://orcid.org/0000-0002-2019-8881
   - **Affiliation:**
     - **Organization:** NASA Goddard Space Flight Center
     - **Affiliation Identifier:** https://ror.org/0171mag52

7. **Authors:** Will Barnes
   - **Author Identifier:** https://orcid.org/0000-0001-9642-6089
   - **Affiliation:**
     - **Organization:** Department of Physics, American University & NASA Goddard Space Flight Center
     - **Affiliation Identifier:** Not available

8. **Authors:** Laura Hayes
   - **Author Identifier:** https://orcid.org/0000-0002-6835-2390
   - **Affiliation:**
     - **Organization:** Dublin Institute for Advanced Studies
     - **Affiliation Identifier:** https://ror.org/02w89n821

9. **Authors:** David Pérez-Suárez
   - **Author Identifier:** https://orcid.org/0000-0003-0784-6909
   - **Affiliation:**
     - **Organization:** University College London
     - **Affiliation Identifier:** https://ror.org/02jx3x895

10. **Authors:** Daniel F. Ryan
    - **Author Identifier:** https://orcid.org/0000-0001-8661-3825
    - **Affiliation:**
      - **Organization:** University College London, Mullard Space Science Laboratory
      - **Affiliation Identifier:** https://ror.org/02jx3x895

**Note:** Over 200 additional contributors listed in Zenodo metadata. The above represents the lead authors from the CITATION.cff file and the first 10 authors from the Zenodo record.

### 7. Software Name (MANDATORY)
- **Name:** sunpy
- **Full Name:** SunPy - Python for Solar Physics
- **Source:** PyHC registry, GitHub repository, Zenodo

### 8. Description (MANDATORY)
sunpy is a Python software package that provides fundamental tools for accessing, loading and interacting with solar physics data in Python. It includes an interface for searching and downloading data from multiple data providers, data containers for image and time series data, commonly used solar coordinate frames and associated transformations, as well as other functionality needed for solar data analysis.

**Source:** README.rst and Zenodo metadata

### 9. Concise Description (OPTIONAL)
SunPy core package: Python for Solar Physics

**Source:** pyproject.toml

### 10. Publication Date (RECOMMENDED)
- **Date:** 2011-08-06
- **Source:** Repository creation date from SoMEF/GitHub API

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/03cpe7c52

**Note:** sunpy releases are published through GitHub-Zenodo integration

### 12. Version (RECOMMENDED)

**Latest Stable Version:**
- **Version Number:** v7.0.2
- **Version Date:** 2025-09-20
- **Version Description:** Bug fix release including fixes for warnings, documentation improvements, and parsing issues
- **Version PID:** https://doi.org/10.5281/zenodo.17162925

**Source:** Zenodo API and git tags

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (primary - requires Python >=3.11)
- **C** (for performance-critical components)

**Note:** Also includes small amounts of IDL, Xonsh, and Shell scripts for specific purposes

**Source:** GitHub API via SoMEF, pyproject.toml

### 14. Reference Publication (OPTIONAL)
- **DOI:** https://doi.org/10.3847/1538-4357/ab4f7a
- **Title:** The SunPy Project: Open Source Development and Status of the Version 1.0 Core Package
- **URL:** https://iopscience.iop.org/article/10.3847/1538-4357/ab4f7a

**Source:** CITATION.cff

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://spdx.org/licenses/BSD-2-Clause.html
- **SPDX ID:** BSD-2-Clause

**Source:** LICENSE.rst, GitHub API, pyproject.toml

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
From multiple sources (PyHC, GitHub topics, pyproject.toml):

- solar physics
- solar
- sun
- astronomy
- astropy
- python
- heliosphere
- science
- wcs
- coordinates
- 2D graphics
- cdaweb
- data analysis
- data retrieval
- fermi
- fido
- fits
- goes
- image processing
- lasco
- line plots
- netcdf
- plotting
- power spectra
- soho
- time
- hacktoberfest

**Source:** PyHC registry, GitHub topics, pyproject.toml, SoMEF

### 17. Data Sources (OPTIONAL)
Based on the net module structure and documentation:

- **CDAWeb** (cdaweb module)
- **The Virtual Solar Observatory** (vso module)
- **Observatory/Mission-specific** (JSOC for SDO data)
- **Other** (HEK, HELIO, web scrapers for various archives)

**Note:** sunpy's Fido interface provides unified access to multiple data providers including VSO, JSOC, CDAWeb, and many web-based archives

**Source:** sunpy/net/ module structure

### 18. Input File Formats (RECOMMENDED)
- **FITS** (primary format for solar images and data)
- **CDF** (for time series data)
- **HDF5** (via h5netcdf)
- **netCDF3/4** (for time series)
- **JPEG 2000** (JP2 - for compressed solar images)
- **ascii** (various text formats)
- **ASDF** (Advanced Scientific Data Format)
- **Other** (ANA - legacy IDL format, GENX)

**Source:** sunpy/io/ module structure, optional dependencies in pyproject.toml

### 19. Output File Formats (RECOMMENDED)
- **FITS** (primary output format)
- **CDF** (time series export)
- **HDF5**
- **netCDF3/4**
- **JPEG 2000** (JP2)
- **ascii**
- **ASDF**
- **Other** (PNG, JPEG, SVG via matplotlib for visualization)

**Source:** sunpy/io/ module structure, visualization capabilities

### 20. Operating System (RECOMMENDED)
- **OS Independent** (pure Python with platform-independent dependencies)
- **Linux** (tested via CI)
- **Mac** (tested via CI)
- **Windows** (supported)

**Source:** pyproject.toml classifier "Operating System :: OS Independent", CI configuration

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** (Python bytecode, no architecture-specific code)
- **x86-64** (most common deployment)
- **Apple Silicon arm64** (supported on macOS)

**Source:** Cross-platform Python package, no CPU-specific requirements

### 22. Related Phenomena (OPTIONAL)
Based on solar physics focus:

- **Solar Flares**
- **Coronal Mass Ejections**
- **Solar Corona**
- **Coronal Heating**
- **Coronal Holes**
- **X-ray emission**

**Note:** sunpy provides tools for analyzing these phenomena through data access, coordinate transforms, and visualization capabilities. Specific support includes HEK event search for flares, CMEs, and other solar phenomena.

**Source:** Heliophysics domain knowledge, HEK module capabilities

### 23. Development Status (RECOMMENDED)
- **Active**

**Note:** Package is actively maintained with recent releases (v7.0.2 in September 2025), continuous integration, and ongoing development. PyHC quality ratings are all "Good" for community, documentation, testing, software maturity, python3, and license.

**Source:** PyHC registry, git activity, repostatus.org badge in README

### 24. Documentation (RECOMMENDED)
- **URL:** https://docs.sunpy.org/
- **Source:** PyHC registry, pyproject.toml, README.rst

### 25. Funder (OPTIONAL)
Not found in repository metadata or Zenodo records.

**Note:** While not explicitly documented in the examined sources, sunpy has likely received funding from various sources throughout its history. Check the documentation or contact the development team for comprehensive funding information.

### 26. Award Title (OPTIONAL)
Not found in repository metadata or Zenodo records.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Primary Reference:**
- The SunPy Project: Open Source Development and Status of the Version 1.0 Core Package
- DOI: https://doi.org/10.3847/1538-4357/ab4f7a

**Note:** Additional publications citing or using sunpy would need to be obtained from the scientific literature or the sunpy website. The package has been widely cited in solar physics research.

### 28. Related Datasets (OPTIONAL)
sunpy provides access to numerous solar physics datasets through its Fido interface, including:

- SDO/AIA, HMI (via JSOC)
- SOHO/EIT, LASCO, MDI
- GOES X-ray data
- STEREO/SECCHI
- Hinode data
- IRIS data
- Many others via VSO and web archives

**Note:** Rather than being tied to specific datasets, sunpy is a tool for accessing and analyzing many different solar physics datasets.

**Source:** Data client modules in sunpy/net/, PyHC keywords

### 29. Related Software (OPTIONAL)
Based on dependencies and the broader ecosystem:

- **Astropy** - https://github.com/astropy/astropy (core dependency)
- **NumPy** - https://github.com/numpy/numpy (core dependency)
- **Matplotlib** - https://github.com/matplotlib/matplotlib (visualization dependency)
- **SciPy** - https://github.com/scipy/scipy (image and analysis dependency)
- **pandas** - https://github.com/pandas-dev/pandas (timeseries dependency)

**Note:** These are key dependencies. For a complete list of affiliated and interoperable packages, see the SunPy Project's affiliated packages list.

**Source:** pyproject.toml dependencies

### 30. Interoperable Software (OPTIONAL)
Based on PyHC ecosystem and documented interoperability:

- **Astropy** - https://github.com/astropy/astropy
- **pysat** - https://github.com/pysat/pysat (PyHC core package)
- **SpacePy** - https://github.com/spacepy/spacepy (PyHC core package)
- **PlasmaPy** - https://github.com/PlasmaPy/PlasmaPy (PyHC core package)
- **pySPEDAS** - https://github.com/spedas/pyspedas (PyHC core package)
- **Kamodo** - https://github.com/nasa/Kamodo (PyHC core package)

**Note:** As a PyHC core package, sunpy is designed to work within the Python in Heliophysics ecosystem and maintains interoperability with other PyHC packages.

**Source:** PyHC core packages list

### 31. Related Instruments (OPTIONAL)
Based on data sources supported and module structure:

sunpy supports data from numerous solar physics instruments including:

- **SDO/AIA** (Atmospheric Imaging Assembly)
- **SDO/HMI** (Helioseismic and Magnetic Imager)
- **SOHO/EIT** (Extreme ultraviolet Imaging Telescope)
- **SOHO/LASCO** (Large Angle and Spectrometric Coronagraph)
- **SOHO/MDI** (Michelson Doppler Imager)
- **GOES** (Geostationary Operational Environmental Satellite - X-ray sensors)
- **STEREO/SECCHI** (Sun Earth Connection Coronal and Heliospheric Investigation)
- **Hinode** instruments
- **IRIS** (Interface Region Imaging Spectrograph)
- **RHESSI** (Reuven Ramaty High Energy Solar Spectroscopic Imager)
- **Fermi** (Gamma-ray Space Telescope - for solar flares)
- **SUIT** (Solar Ultraviolet Imaging Telescope)
- **PUNCH** (Polarimeter to Unify the Corona and Heliosphere)

**Note:** Many more instruments are supported through the VSO interface and dedicated map sources.

**Source:** PyHC keywords (fermi, goes, lasco, soho), map sources, data clients, SUIT and PUNCH map support mentioned in SoMEF release notes

### 32. Related Observatories (OPTIONAL)
- **Solar Dynamics Observatory (SDO)**
- **Solar and Heliospheric Observatory (SOHO)**
- **GOES** series
- **STEREO** (Solar Terrestrial Relations Observatory)
- **Hinode**
- **IRIS** (Interface Region Imaging Spectrograph)

**Note:** sunpy supports data from many solar observatories through various data access interfaces.

**Source:** Data client modules, PyHC keywords, documentation

### 33. Logo (OPTIONAL)
- **URL:** https://raw.githubusercontent.com/sunpy/sunpy-logo/master/generated/sunpy_icon.png

**Source:** PyHC registry

---

## Metadata Sources Summary

This metadata was extracted using the following methods (in order of priority when conflicts occur):

1. **PyHC Registry** (manually curated) - projects_core.yml
2. **Zenodo API** - Concept DOI 10.5281/zenodo.591887, Version DOI 10.5281/zenodo.17162925
3. **SoMEF** (Software Metadata Extraction Framework) - Automated extraction from repository
4. **Manual Repository Examination**:
   - CITATION.cff
   - README.rst
   - pyproject.toml
   - LICENSE.rst
   - Git tags and commit history
   - Module structure analysis (sunpy/net/, sunpy/coordinates/, sunpy/io/, etc.)

All extracted metadata has been verified against multiple sources where possible to ensure accuracy.

---

## Notes

- sunpy is a **PyHC core package** with "Good" ratings across all quality metrics
- The package has over 200 contributors and is actively maintained
- Version 7.0.2 is the latest stable release as of September 2025
- The software is mature, well-documented, and widely used in the solar physics community
- Contact: Stuart Mumford (per PyHC registry), community email: sunpy@googlegroups.com
