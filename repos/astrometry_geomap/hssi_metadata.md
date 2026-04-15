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
  - Data Processing and Analysis:Calibration
  - Data Processing and Analysis:Data Reduction
  - Data Processing and Analysis:Image Processing
  - Data Processing and Analysis:File Format Conversion
  - Data Visualization:2D Graphics
  - Data Visualization:Line Plots

- **Rationale:**
  - **Coordinate Transforms:** Converts RA/Dec (celestial coordinates) to Az/El (local horizon coordinates) using observer location and time
  - **Calibration:** Performs plate scaling and calibration of star field images using Astrometry.net
  - **Data Reduction:** Averages multi-frame image stacks to improve signal-to-noise ratio (AverageImageStack.py)
  - **Image Processing:** Processes FITS astronomical images (both grayscale and color), handles WCS coordinate systems
  - **File Format Conversion:** Converts FITS to netCDF format for output
  - **2D Graphics:** Creates geographic projections, overlays star positions and altitude contours on images
  - **Line Plots:** Generates plots of azimuth/elevation and RA/Dec data

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
- **Value:** astrometry_azel
- **Alternative Names:** AstrometryAzEl (PyHC), astrometry_geomap (current repository name)
- **Source:** Package name from pyproject.toml; PyPI package name is "astrometry-azel"

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
- **Version Number:** v1.3.0 (latest release on Zenodo); v1.4.0 (current development version)
- **Version Date:** 2021-02-10 (for v1.3.0)
- **Version Description:** python >= 3.7, to keep up with NEP29 stack, src/ layout
- **Version PID:** https://doi.org/10.5281/zenodo.4527817 (for v1.3.0)

- **Note:** Latest Zenodo release is v1.3.0 from 2021-02-10. Current development version in repository is v1.4.0 (from __init__.py) but not yet released on Zenodo.

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
- **Value:** Not found
- **Note:** Software processes user-provided FITS images and uses downloaded star catalog index files (2MASS, Tycho), but doesn't directly interface with standard data sources like CDAWeb, HAPI, etc.

### 18. Input File Formats (RECOMMENDED)
- **Values:**
  - FITS

- **Source:** Code analysis shows FITS is the primary input format (astropy.io.fits); also mentions JPEG, TIFF, PNG for initial image inputs before FITS conversion

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - netCDF3/4
  - FITS

- **Source:** Code analysis shows netCDF4 output (via xarray and netcdf4 dependencies); also outputs FITS files with WCS coordinates; PNG plots are generated

### 20. Operating System (RECOMMENDED)
- **Values:**
  - Linux
  - Mac

- **Source:** CI configuration tests on ubuntu-latest; macOS support mentioned in CI but currently disabled. pyproject.toml classifies as "Operating System :: OS Independent" but Astrometry.net dependency limits practical OS support

### 21. CPU Architecture (RECOMMENDED)
- **Value:** CPU Independent
- **Note:** Pure Python code with standard dependencies should work on any architecture supporting Python 3.9+

### 22. Related Phenomena (OPTIONAL)
- **Values:**
  - Aurora
  - Airglow

- **Note:** These are the primary atmospheric phenomena this software is designed to study, though these specific terms may not be in the controlled vocabulary

### 23. Development Status (RECOMMENDED)
- **Value:** Active
- **Source:** Repository shows recent commits (last updated 2025-03-27 per SoMEF), multiple releases, active maintenance

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
  - Astrometry.net (https://github.com/dstndstn/astrometry.net)
  - AstroPy (astropy, listed as dependency)
  - starscale (https://github.com/scivision/starscale) - mentioned in README as related for source extraction/photometry

- **Note:** Astrometry.net is the critical dependency that underlies this software's core functionality

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - numpy
  - astropy
  - xarray
  - netcdf4
  - python-dateutil

- **Source:** These are the core dependencies from pyproject.toml that the software is designed to work with

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
- Repository shows active development (2025-03-27 last update)
- 10 releases total spanning 2016-2021
- CI configured for Python 3.9 and 3.12
- 12 stargazers, 3 forks on GitHub
