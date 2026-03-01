# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/NEXRAD
**Extraction Date:** 2025-12-04

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.1402628
**Source:** Zenodo API (concept DOI for all versions)

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/NEXRAD
**Source:** DataCite API, GitHub
**Note:** Repository was previously named "NEXRADutils" but was renamed to "NEXRAD"

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization:2D Graphics
- Data Visualization:Line Plots

**Source:** Manual code analysis
**Analysis:** The software downloads NEXRAD composite reflectivity PNG images from the Iowa State University archive, loads and processes them with geospatial coordinates from WLD world files, performs coordinate transformations from pixel coordinates to WGS84 latitude/longitude, creates georeferenced map visualizations using Cartopy, and generates keograms (time-longitude/time-latitude plots) for time series analysis.

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere

**Source:** PyHC registry, manual analysis
**Analysis:** NEXRAD (Next-Generation Radar) is a weather radar network that measures atmospheric reflectivity. The software is used to study ionospheric perturbations caused by atmospheric phenomena. PyHC registry lists keywords "ionosphere_thermosphere_mesosphere,general".

### 6. Authors (MANDATORY)
**Author 1:**
- **Authors:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** setup.cfg, LICENSE file, DataCite API

### 7. Software Name (MANDATORY)
**Value:** NEXRAD-quickplot
**Alternate Names:** NEXRADutils (former repository name), NEXRAD
**Source:** setup.cfg (name field), PyHC registry, README

### 8. Description (MANDATORY)
**Value:** Easy Python download and plot NEXRAD N0Q composite reflectivity. Uses RGB high resolution PNG images of North America. The software downloads NEXRAD composite reflectivity data showing weather radar returns and creates georeferenced visualizations on maps using Cartopy. It supports downloading data from the Iowa State archive with parallel downloads, loading images with WGS84 coordinates from .wld files, plotting on geographic maps with state boundaries and coastlines, and creating keograms (time-series plots along latitude or longitude cuts). RGB data scaling covers -32 dBZ to 90 dBZ in 0.5 dBZ increments. These are reduced fidelity RGB images suitable for overview analysis; contact authors for high-fidelity science data.

**Source:** README.md, setup.cfg, DataCite API

### 9. Concise Description (OPTIONAL)
**Value:** Download and plot NEXRAD composite reflectivity PNGs by date/time for ionospheric perturbation studies

**Source:** DataCite API, PyHC description

### 10. Publication Date (RECOMMENDED)
**Value:** 2018-02-12
**Source:** Git history (first commit), SoMEF (date_created: 2018-02-12T22:25:05Z)

### 11. Publisher (RECOMMENDED)
**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API
**Note:** ROR identifier not available for Zenodo; using website URL instead

### 12. Version (RECOMMENDED)
**Latest Version:**
- **Version Number:** v1.0.0
- **Version Date:** 2021-04-27
- **Version Description:** src/ layout - Reorganized code into src/ directory structure
- **Version PID:** https://doi.org/10.5281/zenodo.4722449

**Source:** Git tags, Zenodo API, GitHub releases, SoMEF

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** setup.cfg (python_requires >= 3.7), SoMEF, GitHub API

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found
**Note:** No reference publication or JOSS paper found in repository

### 15. License (RECOMMENDED)
**License:**
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

**Source:** LICENSE file, setup.cfg, SoMEF, GitHub API

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- nexrad
- weather radar
- reflectivity
- ionosphere_thermosphere_mesosphere
- atmospheric science
- weather

**Source:** GitHub topics (nexrad, reflectivity, weather-radar), setup.cfg classifiers (Topic :: Scientific/Engineering :: Atmospheric Science), PyHC registry keywords

### 17. Data Sources (OPTIONAL)
**Values:**
- HTTP/HTTPS Directories
- Other

**Source:** Manual code analysis
**Note:** Downloads from Iowa State University NEXRAD archive at https://mesonet.agron.iastate.edu/archive/data/

### 18. Input File Formats (RECOMMENDED)
**Values:**
- Other (PNG with WLD world files)

**Source:** Manual code analysis
**Note:** Uses PNG images for NEXRAD reflectivity data and WLD (ESRI World File) for geospatial coordinates in EPSG:4326 (WGS84)

### 19. Output File Formats (RECOMMENDED)
**Values:**
- Other (PNG plots)

**Source:** Manual code analysis
**Note:** Outputs georeferenced map plots and keograms as PNG images

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows
- OS Independent

**Source:** setup.cfg (Operating System :: OS Independent), GitHub Actions CI (ubuntu-latest tested), code analysis (Windows-specific filename handling present)

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- CPU Independent

**Source:** Python-only codebase with OS-independent packages

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found
**Note:** NEXRAD measures atmospheric phenomena (precipitation, storms) but specific heliophysics phenomena controlled vocabulary terms not identified

### 23. Development Status (RECOMMENDED)
**Value:** Active
**Source:** setup.cfg classifier (Development Status :: 5 - Production/Stable), recent commits visible through 2023

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/NEXRAD
**Source:** Repository README
**Note:** Documentation is primarily in the README.md file; no separate documentation site found

### 25. Funder (OPTIONAL)
**Value:** Not found
**Note:** No funding information found in repository or DataCite metadata

### 26. Award Title (OPTIONAL)
**Value:** Not found
**Note:** No award information found in repository or DataCite metadata

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found
**Note:** No related publications found in repository or DataCite metadata

### 28. Related Datasets (OPTIONAL)
**Value:** NEXRAD composite reflectivity data from Iowa State University Mesonet
**Source:** README.md and code
**URL:** https://mesonet.agron.iastate.edu/docs/nexrad_composites/
**Note:** No DOI available; data source is an ongoing operational archive

### 29. Related Software (OPTIONAL)
**Values:**
- xarray (data structure dependency)
- Cartopy (mapping dependency)
- imageio (image I/O dependency)

**Source:** setup.cfg install_requires
**Note:** Key dependencies for core functionality; no DOIs found for these dependencies

### 30. Interoperable Software (OPTIONAL)
**Value:** xarray
**Source:** Code analysis
**Note:** Uses xarray.DataArray as primary data structure, enabling interoperability with xarray-compatible packages

### 31. Related Instruments (OPTIONAL)
**Instrument 1:**
- **Instrument Name:** NEXRAD (Next-Generation Radar)
- **Instrument Identifier:** Not found

**Source:** Software name and functionality
**Note:** NEXRAD is a network of weather radars operated by NOAA, the U.S. Air Force, and the FAA

### 32. Related Observatories (OPTIONAL)
**Observatory 1:**
- **Observatory Name:** NEXRAD Network

**Source:** Software functionality
**Note:** National network of Doppler weather radars across the United States

### 33. Logo (OPTIONAL)
**Value:** Not found
**Note:** No logo found in repository

---

## PyHC Package Information

**PyHC Status:** Unevaluated
**PyHC Name:** NEXRADutils
**PyHC Description:** Download/Plot NEXRAD compositive reflectivity by date/time, for ionospheric perturbations
**PyHC Keywords:** ionosphere_thermosphere_mesosphere, general
**PyHC Contact:** Michael Hirsch

**Source:** PyHC unevaluated packages registry (https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_unevaluated.yml)

**Note:** Repository URL in PyHC registry (https://github.com/space-physics/NEXRADutils) redirects to current repository name (https://github.com/space-physics/NEXRAD)

---

## Additional Technical Details

### Dependencies
**Core Dependencies:**
- python-dateutil
- numpy
- imageio >= 2.3
- xarray
- requests

**Optional Dependencies (for plotting):**
- cartopy
- matplotlib
- seaborn
- scikit-image

**Source:** setup.cfg

### Installation
```bash
python -m pip install -e .
```
**Source:** README.md

### Command Line Tools
1. `download-nexrad` - Parallel download of NEXRAD data by date range
2. `plot-nexrad` - Plot NEXRAD reflectivity data on maps or as keograms

**Source:** Manual code analysis

### Testing
- Uses pytest for testing
- Includes flake8 for linting
- Includes mypy for type checking
- GitHub Actions CI on Linux

**Source:** setup.cfg, .github/workflows/ci.yml

---

## Data Format Details

### NEXRAD N0Q Reflectivity Scale
- Black: No Data
- Range: -32 dBZ to 90 dBZ
- Increment: 0.5 dBZ
- Format: RGB PNG images (12200 x 5400 pixels at full resolution)
- Coordinates: EPSG:4326 (WGS84) latitude/longitude
- Coverage: North America

**Source:** README.md, code analysis

### WLD World File Format
Contains 6 lines defining the pixel-to-coordinate transform:
1. Pixel size in x direction (0.005)
2. Rotation of row (typically 0.0)
3. Rotation of column (typically 0.0)
4. Pixel size in y direction (-0.005)
5. X coordinate of upper left pixel center (longitude: -126.0)
6. Y coordinate of upper left pixel center (latitude: 50.0)

**Source:** README.md

---

## Version History

Available versions from GitHub releases and Zenodo:
- v1.0.0 (2021-04-27): src/ layout
- v0.6.8 (2018-08-23): rename modules for convenience
- v0.6.7 (2018-08-17): Improve downsampling, imageio>=2.3
- v0.6.6 (2018-08-17): modularize, document
- v0.6.5 (2018-07-26): Robustness improvements
- v0.6.4 (2018-07-08): Code quality: flake8, mypy typing
- v0.6.3 (2018-06-19): Add N0Q scale to plots
- v0.6.2 (2018-06-11): optional subplots, ticks
- v0.6.1 (2018-06-05): Windows compatibility
- v0.6.0 (2018-06-05): Initial release

**Source:** SoMEF, GitHub releases

---

## Metadata Extraction Summary

**Automated Extraction Methods Used:**
- ✅ DataCite API
- ✅ Zenodo API
- ✅ SoMEF
- ✅ PyHC Registry

**Manual Examination Completed:**
- ✅ README.md
- ✅ LICENSE
- ✅ setup.cfg, setup.py, pyproject.toml
- ✅ Source code files
- ✅ GitHub Actions CI configuration
- ✅ Git history and tags

**Key Strengths of Metadata:**
- Well-documented code repository
- Clear licensing (MIT)
- Version control with semantic versioning
- DOI available through Zenodo
- Listed in PyHC registry
- Active development status

**Metadata Gaps:**
- No author ORCID or affiliation
- No author email (uses GitHub noreply address)
- No reference publication
- No funding information
- No dedicated documentation site
- No logo
