# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/themisasi
**Extraction Date:** 2025-12-04

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Concept DOI:** https://doi.org/10.5281/zenodo.595411
- **Source:** DataCite API and Zenodo API

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/space-physics/themisasi
- **Source:** DataCite API, GitHub

### 4. Software Functionality (MANDATORY)
- **Selected Functionalities:**
  - Coordinate Transforms
  - Data Processing and Analysis:Data Access and Retrieval
  - Data Processing and Analysis:Data Reduction
  - Data Processing and Analysis:File Format Conversion
  - Data Processing and Analysis:Image Processing
  - Data Processing and Analysis:Processing
  - Data Visualization:2D Graphics
  - Data Visualization:Line Plots
  - Data Visualization:Movies
- **Source:** Manual analysis of code and documentation. The software downloads, reads, calibrates, and visualizes THEMIS ASI ground-based aurora imager data. It performs coordinate transformations (az/el to RA/Dec), processes 256x256 images with calibration data, plots time series, and plays back video sequences.

### 5. Related Region (MANDATORY)
- **Selected Regions:**
  - Earth Atmosphere
  - Earth Magnetosphere
- **Source:** PyHC registry keywords ("magnetosphere", "ionosphere_thermosphere_mesosphere"). THEMIS ASI observes aurora in the ionosphere/thermosphere (Earth Atmosphere) as part of the THEMIS mission studying the magnetosphere (Earth Magnetosphere).

### 6. Authors (MANDATORY)
- **Author 1:**
  - **Name:** Michael Hirsch
  - **Author Identifier:** Not found
  - **Affiliation:**
    - **Organization:** Not found
    - **Affiliation Identifier:** Not found
- **Source:** DataCite API, PyHC registry. Note: Only one author listed in available metadata sources.

### 7. Software Name (MANDATORY)
- **Name:** themisasi
- **Full Title:** THEMIS GBO ASI Reader
- **Source:** DataCite API, SoMEF, README

### 8. Description (MANDATORY)
- **Description:** Read & plot 256x256 "high resolution" THEMIS ASI ground-based imager data from Python. THEMIS ASI data are collected with the original 2002 design, using Starlight-Xpress Lodestar MX716 cameras with monochrome Sony ICX249AL imaging chips. A subregion from full-size 752 x 582 pixels (512 x 512 pixels) are 2x2 binned to 256 x 256 pixels and retrieved over USB 1.1 for disk storage. This package also reads the THEMIS ASI star registered plate scale, giving azimuth and elevation for each pixel. The software supports downloading data concurrently using asyncio, loading calibration data with azimuth/elevation information, coordinate conversion to RA/Dec, video playback, and plotting pixel time series.
- **Source:** Combination of DataCite API, README, and PyHC registry

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Reads and plots THEMIS ASI video data of aurora, including calibration for azimuth/elevation and coordinate transformations.
- **Source:** Derived from pyproject.toml

### 10. Publication Date (RECOMMENDED)
- **Date:** 2015-02-11
- **Source:** SoMEF (GitHub API date_created), git history (first commit)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/03cpe7c52
- **Source:** DataCite API

### 12. Version (RECOMMENDED)
- **Version Number:** v1.2.0
- **Version Date:** 2021-04-27
- **Version Description:** Update for newer numpy.datetime64
- **Version PID:** https://doi.org/10.5281/zenodo.4722490
- **Source:** DataCite API, Zenodo API, SoMEF releases, git tags

**Additional Version History:**
- **v1.1.0** (2020-07-17): src/ layout, entry_points, add examples. Modernizing package layout.
- **v1.0.0** (2019-06-17): asyncio downloading, base url is a parameter, parametrize tests
- **v0.8.4** (2018-12-31): Improved project structure, put projections into own file
- **v0.8.3.1** (2018-09-14): Bugfix: not autofinding cal files
- **v0.8.3** (2018-09-14): Fix corner cases, auto-download cal files
- **v0.8.2** (2018-09-05): Autoload most recent prior cal file if available
- **v0.8.1** (2018-08-29): SpacePy=>CDFlib, robust time handling
- **v0.7.2** (2018-07-10): Robustify, add pixel time series plot function
- **v0.7.1** (2018-07-09): Modernization (pep8, mypy, setup.cfg)
- **v0.7.0** (2018-06-21): Initial release

### 13. Programming Language (RECOMMENDED)
- **Languages:**
  - Python 3.x (requires Python >= 3.10)
  - MATLAB
  - IDL
- **Source:** SoMEF (GitHub API programming_languages), pyproject.toml (Python version requirement)

### 14. Reference Publication (RECOMMENDED)
- **DOI:** Not found
- **Note:** README references descriptive articles about THEMIS GBO ASI:
  - Mende 2008 SSR: http://www.igpp.ucla.edu/public/THEMIS/SCI/Pubs/2008_Refereed/mende_ssr_onlinefirst.pdf
  - Jackel 2014: http://eprints.lancs.ac.uk/68180/4/gi_3_71_2014.pdf (color instrument based on THEMIS)

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html
- **Source:** SoMEF (GitHub API), LICENSE.txt file

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Keywords:**
  - all-sky-imager
  - all-sky-camera
  - aurora
  - geoscience
  - python
  - themis
  - xarray
  - magnetosphere
  - ionosphere_thermosphere_mesosphere
- **Source:** SoMEF (GitHub topics), pyproject.toml, PyHC registry

### 17. Data Sources (OPTIONAL)
- **Data Sources:**
  - HTTP/HTTPS Directories (THEMIS data repository at http://themis.ssl.berkeley.edu/data/themis/thg/l1/asi/)
  - Observatory/Mission-specific (THEMIS mission data)
- **Source:** README documentation, code examination

### 18. Input File Formats (RECOMMENDED)
- **Formats:**
  - CDF
  - IDL.sav
  - HDF5
  - netCDF3/4
- **Source:** Code analysis (src/themisasi/io.py imports and file handling)

### 19. Output File Formats (RECOMMENDED)
- **Formats:**
  - ascii (PNG images for video frames)
  - netCDF3/4 (via xarray output capabilities)
  - HDF5 (via xarray output capabilities)
- **Source:** README mentions PNG output for video frames; xarray Dataset output supports netCDF and HDF5

### 20. Operating System (RECOMMENDED)
- **Operating Systems:**
  - Linux
  - Mac
  - Windows
- **Source:** CI configuration (.github/workflows/ci.yml) tests on ubuntu-latest, windows-latest, macos-latest; pyproject.toml states "Operating System :: OS Independent"

### 21. CPU Architecture (RECOMMENDED)
- **Architecture:**
  - x86-64
  - Apple Silicon arm64 (inferred from macOS support)
  - CPU Independent
- **Source:** Inferred from OS support and Python package nature

### 22. Related Phenomena (OPTIONAL)
- **Phenomena:**
  - Aurora
  - Auroral emissions (visible wavelength, particularly 557.7 nm based on spectral response data)
- **Source:** README, package description, keywords

### 23. Development Status (RECOMMENDED)
- **Status:** Active
- **Source:** SoMEF, pyproject.toml classifier "Development Status :: 5 - Production/Stable", recent commit activity (last updated 2025-03-02 according to SoMEF)

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/space-physics/themisasi/blob/main/README.md
- **Source:** Repository README file (no separate documentation site found)

### 25. Funder (OPTIONAL)
- **Funder:** Not found
- **Funder Identifier:** Not found

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Publications:**
  - Not found as DOIs
  - Referenced articles (non-DOI):
    - Mende 2008 SSR: http://www.igpp.ucla.edu/public/THEMIS/SCI/Pubs/2008_Refereed/mende_ssr_onlinefirst.pdf
    - Jackel 2014: http://eprints.lancs.ac.uk/68180/4/gi_3_71_2014.pdf
- **Source:** README

### 28. Related Datasets (OPTIONAL)
- **Datasets:**
  - THEMIS GBO ASI data repository: http://themis.ssl.berkeley.edu/data/themis/thg/l1/asi/
  - THEMIS plate scale/calibration data: http://themis.ssl.berkeley.edu/themisdata/thg/l2/asi/cal/
  - Alternate plate scale data: http://data.phys.ucalgary.ca/sort_by_project/THEMIS/asi/skymaps/new_style/
- **Source:** README resources section

### 29. Related Software (OPTIONAL)
- **Software:**
  - pymap3d: https://github.com/geospace-code/pymap3d (for coordinate conversion)
  - dascutils (Digital All Sky Camera utilities - optional dependency)
  - histutils (optional dependency for field-of-view functionality)
- **Source:** README, pyproject.toml optional dependencies

### 30. Interoperable Software (OPTIONAL)
- **Software:**
  - xarray (core dependency - data structure)
  - pymap3d (coordinate conversions)
- **Source:** Documentation shows integration with these packages

### 31. Related Instruments (OPTIONAL)
- **Instruments:**
  - **Instrument Name:** THEMIS All-Sky Imagers (ASI)
  - **Instrument Identifier:** Not found
  - **Details:** Starlight-Xpress Lodestar MX716 cameras with monochrome Sony ICX249AL imaging chips, 256x256 pixel resolution after binning
- **Source:** README technical description

### 32. Related Observatories (OPTIONAL)
- **Observatories:**
  - **Observatory Name:** THEMIS (Time History of Events and Macroscale Interactions during Substorms)
  - **Observatory Details:** THEMIS GBO (Ground-Based Observatory) network with stations including Gakona (gako), Fort Yukon (fykn), and others shown in station map
- **Source:** README, package name and description

### 33. Logo (OPTIONAL)
- **Logo URL:** https://i.ibb.co/Jyx1nNd/thm-gbo-logo.jpg
- **Source:** PyHC unevaluated registry

---

## Metadata Sources Summary

1. **DataCite API** (10.5281/zenodo.595411): Provided DOI, title, description, author, publisher, version, publication date, related identifiers
2. **Zenodo API** (record 4722490): Provided concept DOI, version DOI, creation/modification dates, license
3. **SoMEF**: Provided comprehensive metadata including GitHub statistics, programming languages, releases, keywords, dependencies
4. **PyHC Unevaluated Registry**: Provided logo, keywords for related regions (magnetosphere, ionosphere_thermosphere_mesosphere), contact information
5. **Manual Repository Examination**:
   - README.md: Description, usage, installation, related articles, resources, technical details
   - LICENSE.txt: License text confirmation
   - pyproject.toml: Python version requirement, dependencies, classifiers, keywords
   - .github/workflows/ci.yml: Operating system support
   - src/themisasi/io.py: Input file format support
   - Git history: First commit date, version tags

---

## Notes

- The package is part of the PyHC unevaluated registry, indicating it serves the heliophysics Python community
- THEMIS ASI data uses CDF format with calibration files in either CDF or IDL .sav format
- The software emphasizes concurrent downloading capabilities using asyncio for efficient data retrieval
- Calibration data provides azimuth and elevation mapping for each pixel, critical for multi-camera analyses
- The package uses xarray.Dataset as its primary data structure, following geoscience best practices
- Development is active with regular updates and comprehensive CI testing across multiple platforms
- Author Michael Hirsch maintains multiple space physics Python packages in the PyHC ecosystem
