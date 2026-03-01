# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/dascasi
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.595465

**Source:** Zenodo API (concept DOI for all versions)

**Note:** This is the concept DOI that represents all versions of the software. The DOI for the specific version v2.3.0 is https://doi.org/10.5281/zenodo.6419126. An older citation DOI (https://doi.org/10.5281/zenodo.3471731) was found in the CITATION file but appears to be superseded.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/dascasi

**Source:** Repository URL from DataCite API, confirmed in SoMEF output

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Data Processing and Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Image Processing
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Movies

**Source:** Manual analysis of README.md, source code, and PyHC metadata

**Analysis:** The software provides the following functionalities:
1. **Data Access and Retrieval** - Downloads DASC camera data from FTP servers
2. **Image Processing** - Reads, processes, and analyzes all-sky camera FITS images, including handling corrupted files from 2013 RAID array failure
3. **Calibration** - Spatial registration using azimuth/elevation plate scale calibration data
4. **Coordinate Transforms** - Azimuth/elevation transformations, map projections to geographic grids at specified altitudes
5. **File Format Conversion** - Converts FITS image stacks to HDF5 format with lossless compression
6. **Visualization** - Creates 2D plots, azimuth/elevation plots, projected images, time-series movies

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere

**Source:** PyHC metadata (keywords include "ionosphere_thermosphere_mesosphere"), README analysis

**Analysis:** The software is designed for Digital All-Sky Camera data used in auroral and airglow analysis. These phenomena occur in Earth's upper atmosphere, specifically the ionosphere-thermosphere-mesosphere region. The cameras observe atmospheric optical emissions from aurora and airglow.

### 6. Authors (MANDATORY)

**Author 1:**
- **Authors:** Michael Hirsch
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found (Note: Associated with U. Alaska Geophysical Institute based on software description, but no formal affiliation listed in metadata)
  - **Affiliation Identifier:** Not found

**Source:** PyHC registry (contact: Michael Hirsch), DataCite API lists "Michael" but with malformed name structure

**Author 2:**
- **Authors:** Samuel
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** DataCite API (surname appears to be missing in the metadata)

**Author 3:**
- **Authors:** Sebastijan Mrak
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** DataCite API, contributors.md (credited for mapping projection contributions)

**Note:** Author names from DataCite appear incomplete or malformed. The primary maintainer/contact is Michael Hirsch based on PyHC registry and repository ownership. Samuel's full name could not be determined from available metadata.

### 7. Software Name (MANDATORY)
**Value:** dascasi

**Alternate Names:**
- DASCutils (PyHC registry name)
- space-physics/dascasi (GitHub repository name)

**Source:** SoMEF (package name from pyproject.toml), PyHC registry

**Note:** The formal Python package name is "dascasi". The PyHC registry refers to it as "DASCutils". DataCite lists the title as "space-physics/dascasi: use python -m" which appears to be a release-specific title.

### 8. Description (MANDATORY)
**Value:** Digital All Sky Camera utilities for the University of Alaska Geophysical Institute cameras. This software provides utilities for plotting, saving, and analyzing data from the Poker Flat Research Range Digital All Sky Camera and other locations. It reads FITS format all-sky camera images, performs spatial calibration using azimuth/elevation plate scale data, supports map projection to specified altitudes for auroral and airglow analysis, converts FITS image stacks to HDF5 format with lossless compression, and creates visualizations including movies and projected images. The software handles corrupted FITS files from the 2013 RAID array failure and supports multi-wavelength image analysis for scientific studies of aurora and airglow phenomena.

**Source:** Synthesized from README.md, DataCite description, PyHC description, and SoMEF output

### 9. Concise Description (OPTIONAL)
**Value:** Digital All Sky Camera utilities for U. Alaska Geophysical Institute cameras, supporting image reading, calibration, projection, format conversion, and visualization.

**Source:** Derived from DataCite abstract (199 characters)

### 10. Publication Date (RECOMMENDED)
**Value:** 2016-02-03

**Source:** SoMEF (date_created from GitHub API), confirmed by git log first commit date

**Note:** This is the initial publication/creation date of the repository. The concept DOI publication year is 2022, which corresponds to when the Zenodo integration was established.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API, Zenodo metadata

### 12. Version (RECOMMENDED)

**Version Number:** v2.3.0

**Version Date:** 2022-04-06

**Version Description:** Use python -m

**Version PID:** https://doi.org/10.5281/zenodo.6419126

**Source:** DataCite API, Zenodo API, SoMEF releases, git tags

**Note:** This is the latest version with a DOI. The actual current code version in the repository is 3.0.0 (from __init__.py), but this version does not appear to have a corresponding DOI release on Zenodo. Previous versions include v2.2.1, v2.2.0, v2.1.0, v2.0.3, v2.0.2, v2.0.1, v2.0.0, and earlier versions back to v1.0 (2016-10-19).

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** SoMEF (programming_languages from GitHub API), pyproject.toml (requires-python = ">=3.7"), CI configuration (tests Python 3.7 and 3.11)

**Note:** Primary language is Python. Repository also contains minor amounts of Jupyter Notebook (2,038 bytes) and Shell scripts (497 bytes) according to GitHub language statistics.

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Source:** No reference publication DOI found in DataCite relatedIdentifiers, README, or CITATION file

**Note:** The software has DOIs for the code itself but no associated journal publication (e.g., JOSS paper) was found.

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** https://www.apache.org/licenses/LICENSE-2.0

**Source:** SoMEF (spdx_id: Apache-2.0), LICENSE.txt file in repository

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- all-sky-camera
- aurora
- camera
- ionosphere
- thermosphere
- mesosphere
- atmospheric science
- airglow
- FITS
- image processing
- calibration

**Source:** GitHub topics (via SoMEF), pyproject.toml, PyHC keywords (ionosphere_thermosphere_mesosphere), README analysis

### 17. Data Sources (OPTIONAL)
**Values:**
- FTP/FTPS Directories

**Source:** README.md mentions downloading from FTP server at ftp://optics.gi.alaska.edu/

**Note:** The software downloads calibration data and raw DASC FITS files from University of Alaska Geophysical Institute FTP servers.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- FITS
- HDF5

**Source:** README.md, io.py source code analysis

**Note:** Primary input format is FITS (Flexible Image Transport System) for raw camera images. The software also supports reading previously converted HDF5 files.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- HDF5

**Source:** README.md (save_hdf5 function), hdf5.py module

**Note:** The software saves processed image stacks to HDF5 format with lossless compression. Visualization outputs (plots, movies) are also generated but file formats for these are not explicitly specified in the documentation.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Source:** .github/workflows/ci.yml (tests on ubuntu-latest, macos-latest, windows-latest), pyproject.toml (Operating System :: OS Independent)

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- CPU Independent

**Source:** Inferred from Python implementation and CI testing on standard architectures

**Note:** As a pure Python package with standard dependencies, it should run on any CPU architecture that supports Python 3.7+.

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Not found in controlled vocabulary

**Potential Values (not in HSSI list):**
- Aurora (auroral emissions)
- Airglow

**Source:** README.md and pyproject.toml keywords mention "aurora" and README discusses "auroral and airglow analysis"

**Note:** The primary phenomena studied with this software are aurora and airglow, but these specific terms do not appear to be in the HSSI Related Phenomena controlled vocabulary shown in the form documentation.

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** SoMEF (date_updated: 2023-03-20 shows recent activity), git history shows commits through 2023, CI workflow actively maintained

**Note:** The repository shows signs of active maintenance with updates in 2023, though the last Zenodo release was in 2022. Based on repostatus.org definitions, this qualifies as "Active" - reached stable, usable state and being actively developed.

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/dascasi

**Source:** Repository serves as primary documentation location; no separate documentation site found

**Note:** Documentation is provided through the README.md file in the repository. No separate ReadTheDocs or dedicated documentation website was identified. Usage examples are provided in the README and in the scripts/ directory.

### 25. Funder (OPTIONAL)
**Value:** Not found

**Source:** No funding information found in DataCite fundingReferences, README, or repository metadata

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Source:** No award information found in available metadata sources

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found

**Source:** No related publications found in DataCite relatedIdentifiers or README

**Note:** No papers citing or describing this software were found in the available metadata.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Source:** No related datasets with DOIs found in metadata

**Note:** The software works with DASC camera data from UAF Geophysical Institute, but no specific dataset DOIs were identified. Data is available via FTP at ftp://optics.gi.alaska.edu/

### 29. Related Software (OPTIONAL)

**Value 1:** pymap3d

**Source:** Listed in dependencies (pyproject.toml)

**Note:** PyMap3D provides 3D coordinate conversions used for geographic transformations. No DOI found; repository at https://github.com/geospace-code/pymap3d

**Value 2:** xarray

**Source:** Listed in dependencies, core data structure used

**Note:** Xarray provides labeled multi-dimensional arrays. No specific DOI for the software itself.

**Value 3:** astropy

**Source:** Listed in dependencies, used for FITS file I/O

**Note:** Astropy is used for reading FITS files. While Astropy has publications, the software dependency is on the package itself.

**Value 4:** themisasi

**Source:** Listed in optional dependencies (pyproject.toml)

**Note:** THEMIS All-Sky Imager utilities, related software for similar camera systems. Repository: https://github.com/space-physics/themisasi

### 30. Interoperable Software (OPTIONAL)
**Value:** Not found

**Source:** No explicit interoperability claims found beyond standard Python package dependencies

**Note:** The software uses standard Python scientific stack (numpy, scipy, xarray) which enables broad interoperability, but no specific demonstrated interoperability with other heliophysics packages was documented.

### 31. Related Instruments (OPTIONAL)

**Instrument 1:**
- **Instrument Name:** DASC (Digital All-Sky Camera)
- **Instrument Identifier:** Not found

**Source:** README.md, software description

**Note:** Software is specifically designed for DASC cameras at Poker Flat Research Range and other University of Alaska Geophysical Institute locations.

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** Poker Flat Research Range

**Source:** README.md, PyHC description

**Note:** Primary observatory location mentioned for DASC cameras

**Observatory 2:**
- **Observatory Name:** University of Alaska Geophysical Institute

**Source:** Software description, FTP data source

**Note:** Operates the DASC camera network

### 33. Logo (OPTIONAL)
**Value:** https://i.ibb.co/JKLF4FB/logo.jpg

**Source:** PyHC registry metadata

---

## Summary of Metadata Sources

This metadata extraction utilized the following sources in priority order:

1. **PyHC Registry** (projects_unevaluated.yml) - Manually curated, most reliable for core metadata
2. **Zenodo API** - Official DOI metadata, concept DOI and version information
3. **DataCite API** - DOI metadata (some author name issues identified)
4. **SoMEF** - Automated extraction from repository
5. **Manual Repository Examination** - README.md, pyproject.toml, LICENSE.txt, CI configuration, source code

## Verification Notes

- **DOI Verification:** Concept DOI (10.5281/zenodo.595465) verified via both DataCite and Zenodo APIs
- **Repository URL:** Verified accessible at https://github.com/space-physics/dascasi
- **License:** Apache-2.0 confirmed via LICENSE.txt file and SPDX identifier
- **Operating Systems:** Verified via CI configuration testing on Linux, macOS, and Windows
- **Software Functionality:** Comprehensively analyzed through README and source code examination
- **Related Region:** Confirmed through PyHC keywords and scientific context (aurora/airglow in ionosphere-thermosphere)

## Known Limitations

1. **Author Information Incomplete:** Full names and ORCIDs not available for all authors (particularly "Samuel")
2. **No Reference Publication:** No peer-reviewed publication describing the software
3. **Version DOI Gap:** Current code version (3.0.0) does not have a corresponding Zenodo DOI
4. **Affiliation Information Missing:** No formal institutional affiliations listed for authors
5. **Phenomena Vocabulary Mismatch:** Aurora and airglow are key phenomena but may not be in HSSI controlled vocabulary
