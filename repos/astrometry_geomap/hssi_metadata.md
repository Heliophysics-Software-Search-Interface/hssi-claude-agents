# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/astrometry_geomap (formerly astrometry_azel)
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.595450
- **Source:** Concept DOI from Zenodo, represents all versions of the software

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/space-physics/astrometry_geomap
- **Note:** Repository was renamed from astrometry_azel to astrometry_geomap; PyHC registry still uses old URL https://github.com/space-physics/astrometry_azel which redirects to current location

### 4. Software Functionality (MANDATORY)
- **Values:**
  - Coordinate Transforms
  - Data Processing and Analysis
  - Data Processing and Analysis:Data Access and Retrieval
  - Data Processing and Analysis:Calibration
  - Data Processing and Analysis:Data Reduction
  - Data Processing and Analysis:Image Processing
  - Data Processing and Analysis:File Format Conversion
  - Data Visualization
  - Data Visualization:2D Graphics

- **Rationale:**
  - **Coordinate Transforms:** Converts RA/Dec (celestial coordinates) to Az/El (local horizon coordinates) using observer location and time
  - **Data Access and Retrieval:** Includes a user-facing downloader for Astrometry.net star catalog index files from HTTP directories
  - **Calibration:** Performs plate scaling and calibration of star field images using Astrometry.net
  - **Data Reduction:** Averages multi-frame image stacks to improve signal-to-noise ratio (AverageImageStack.py)
  - **Image Processing:** Processes FITS astronomical images (both grayscale and color), handles WCS coordinate systems
  - **File Format Conversion:** Converts FITS to netCDF format for output
  - **2D Graphics:** Creates geographic projections, overlays star positions and altitude contours on images

### 5. Related Region (MANDATORY)
- **Value:** Earth Atmosphere

- **Rationale:**
  - Software is specifically designed for auroral and airglow imaging (as stated in README and PyHC description)
  - Auroral and airglow emissions occur in Earth's upper atmosphere/ionosphere, typically around 100 km altitude (explicitly mentioned in code comments)
  - PyHC keywords categorize this as "ionosphere_thermosphere_mesosphere"
  - Used for ground-based all-sky camera observations of atmospheric phenomena

### 6. Authors (MANDATORY)
- **Authors:** Michael Hirsch
  - **Author Identifier:** Not found
  - **Affiliation:** Not found

- **Note:** Author name from DataCite API and PyHC contact. No ORCID or affiliation information available in repository metadata.

### 7. Software Name (MANDATORY)
- **Value:** AstrometryAzEl
- **Alternative Names:** astrometry_azel (package and PyPI name), astrometry_geomap (current repository name)
- **Source:** PyHC registry name (authoritative software name), pyproject.toml package name, and current repository name

### 8. Description (MANDATORY)
- **Value:** Register images to geographic maps using the astrometry.net program. This software performs plate scale calibration of star imagery to enable use of multiple auroral and airglow cameras together. It converts FITS images to azimuth/elevation coordinates using Astrometry.net, with applications in aeronomy for studying aurora and airglow emissions. The software assumes emissions occur at a specified altitude (typically ~100 km for auroral observations) and projects images onto geographic coordinates.

- **Sources:** Combined from pyproject.toml description, PyHC description, and README analysis

### 9. Concise Description (OPTIONAL)
- **Value:** Plate scale and calibrate star imagery to azimuth/elevation coordinates for auroral and airglow camera observations using Astrometry.net.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2016-02-13
- **Source:** Date of first git commit (2016-02-13 22:28:18 -0500)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

- **Source:** DataCite API and Zenodo metadata

### 12. Version (RECOMMENDED)
- **Version Number:** v1.3.0
- **Version Date:** 2021-02-10
- **Version Description:** python >= 3.7, to keep up with NEP29 stack, src/ layout
- **Version PID:** https://doi.org/10.5281/zenodo.4527817

- **Note:** The current repository declares development version v1.4.0 in `src/astrometry_azel/__init__.py`, but that unreleased development state does not have a Zenodo version DOI and is not used for this version record.

### 13. Programming Language (RECOMMENDED)
- **Values:**
  - Python 3.x
  - MATLAB

- **Source:** SoMEF analysis shows Python (40,201 bytes) and MATLAB (2,514 bytes); pyproject.toml requires Python >= 3.9

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found
- **Note:** No reference publication DOI found in repository metadata

### 15. License (RECOMMENDED)
- **License:** ISC License
- **License URI:** https://spdx.org/licenses/ISC.html

- **Source:** LICENSE.txt file contains ISC License text; SoMEF confirmed with spdx_id "ISC"

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Values:**
  - astrometry
  - plate-scale
  - astronomy
  - aurora
  - astropy
  - citizen-science
  - ionosphere_thermosphere_mesosphere (PyHC classification)

- **Sources:** pyproject.toml, GitHub topics (from SoMEF), PyHC keywords

### 17. Data Sources (OPTIONAL)
- **Value:** HTTP/HTTPS Directories
- **Note:** The repository includes a downloader for Astrometry.net star catalog index files (2MASS and Tycho) from HTTP directories.

### 18. Input File Formats (RECOMMENDED)
- **Values:**
  - FITS
  - HDF5
  - Other

- **Source:** Code analysis shows support for FITS and HDF5 inputs, plus additional image-stack inputs handled outside the controlled list (for example TIFF, GIF, PNG, and MATLAB `.mat` files).

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - netCDF3/4
  - FITS
  - Other

- **Source:** Code analysis shows netCDF4 output, FITS output, and generated PNG plots/products.

### 20. Operating System (RECOMMENDED)
- **Values:**
  - Linux

- **Source:** CI validates Linux on ubuntu-latest. The package metadata says OS Independent, but the Astrometry.net dependency chain is only tested here on Linux.

### 21. CPU Architecture (RECOMMENDED)
- **Value:** CPU Independent
- **Note:** Pure Python code with standard dependencies should work on any architecture supporting Python 3.9+

### 22. Related Phenomena (OPTIONAL)
- **Values:**
  - Aurora
  - Airglow

- **Note:** These are the primary atmospheric phenomena this software is designed to study, though these specific terms may not be in the controlled vocabulary

### 23. Development Status (RECOMMENDED)
- **Value:** Inactive
- **Source:** The local repository snapshot is stable but not under clearly ongoing active maintenance: the latest upstream commit is 2024-02-05 and the latest tagged release is v1.3.0 from 2021-02-10.

### 24. Documentation (RECOMMENDED)
- **Value:** https://github.com/space-physics/astrometry_geomap
- **Note:** No separate documentation site found; README.md in repository serves as primary documentation

### 25. Funder (OPTIONAL)
- **Value:** Not found
- **Source:** No funding information in DataCite API or repository

### 26. Award Title (OPTIONAL)
- **Value:** Not found
- **Source:** No award information in DataCite API or repository

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Value:** Not found
- **Note:** README references an article on Astrometry.net robustness (Schindler et al. 2016) and a tips/techniques article, but no DOIs for publications specifically about this software

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found
- **Note:** Software uses 2MASS and Tycho star catalogs but these are reference catalogs, not datasets the software analyzes

### 29. Related Software (OPTIONAL)
- **Values:**
  - https://github.com/dstndstn/astrometry.net
  - https://github.com/astropy/astropy
  - https://github.com/scivision/starscale

- **Note:** Astrometry.net is the critical dependency that underlies this software's core functionality, and `starscale` is referenced in the README as related software for source extraction and photometry.

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - https://github.com/numpy/numpy
  - https://github.com/astropy/astropy
  - https://github.com/pydata/xarray
  - https://github.com/Unidata/netcdf4-python
  - https://github.com/dateutil/dateutil

- **Source:** These are core Python packages from `pyproject.toml` that the software interoperates with directly.

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** Digital All Sky Cameras (general category)
- **Instrument Identifier:** Not found

- **Note:** README mentions this is used for all-sky cameras, Digital All Sky Camera (DASC) at Poker Flat Research Range (referenced via related DASCutils package by same author), and citizen science DSLR cameras. No specific instrument identifiers available.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Not found (general-purpose tool)
- **Note:** Software is designed to work with imagery from any ground-based observatory or citizen science camera, not tied to a specific mission or observatory

### 33. Logo (OPTIONAL)
- **Value:** Not found
- **Note:** No logo file found in repository

---

## Metadata Agreement (MANDATORY)

By submitting this form, you acknowledge and agree that any metadata you provide is submitted voluntarily and becomes part of the public domain. You waive all rights, claims, and interests to the submitted metadata, and grant unrestricted use, reproduction, modification, and distribution rights to the receiving party or its designees.

---

## Extraction Notes

### Repository Naming
The repository was renamed from "astrometry_azel" to "astrometry_geomap" at some point, causing some inconsistency in metadata:
- PyHC registry uses: https://github.com/space-physics/astrometry_azel (redirects to astrometry_geomap)
- Package name remains: astrometry_azel
- PyPI package: astrometry-azel
- Current repository: astrometry_geomap
- Zenodo titles refer to: astrometry_azel

### Metadata Source Priority
1. **PyHC metadata** - Used for classification (ionosphere_thermosphere_mesosphere) and description enhancement
2. **Repository files** - Primary source for license, dependencies, version
3. **Zenodo/DataCite APIs** - Used for DOI information and publication metadata
4. **SoMEF** - Supplementary metadata, but note repository name confusion

### Key Dependencies
The software critically depends on:
- Astrometry.net (external C program, not Python package)
- Star catalog index files (2MASS, Tycho - must be downloaded separately)
- Standard scientific Python stack (numpy, astropy, xarray)

### Development Status Details
- Latest Zenodo release: v1.3.0 (2021-02-10)
- Current development version: v1.4.0
- Latest upstream commit in the local refreshed repository: 2024-02-05
- 10 releases total spanning 2016-2021
- CI configured for Python 3.9 and 3.12
- 12 stargazers, 3 forks on GitHub
