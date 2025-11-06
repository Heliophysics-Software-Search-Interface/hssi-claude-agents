# HSSI Metadata Extraction Results

**Repository:** https://github.com/JouleCai/geospacelab
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.5377318

**Source:** CITATION.cff, Zenodo API
**Note:** This is the concept DOI for all versions of the software.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/JouleCai/geospacelab

**Source:** CITATION.cff, DataCite API, SoMEF

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Orbit Plots
- Data Visualization:Spectrogram

**Source:** README.md feature list, built-in data sources table, PyHC keywords
**Analysis:** GeospaceLAB provides comprehensive data management, visualization, and analysis capabilities for space physics. Key functionalities include:
- Coordinate transformations between GEO and AACGM/APEX systems
- Data access from multiple sources (CDAWeb, Madrigal, etc.)
- Time series analysis with automatic time tick adjustment
- 2D visualization including polar maps, satellite tracks, and spectrograms
- Data processing through DataHub/Dataset/Variable architecture

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space

**Source:** README.md built-in data sources, PyHC keywords
**Analysis:**
- **Earth Atmosphere:** Ionospheric/thermospheric data (EISCAT ISR, GNSS TEC maps, GITM model, SWARM)
- **Earth Magnetosphere:** Magnetospheric phenomena (SWARM, AMPERE FAC, SuperDARN convection, DMSP, geomagnetic indices)
- **Interplanetary Space:** Solar wind and IMF data (OMNI dataset)

### 6. Authors (MANDATORY)

#### Author 1
- **Authors:** Lei Cai
- **Author Identifier:** https://orcid.org/0000-0003-0127-7303
- **Affiliation:**
  - **Organization:** University of Oulu (inferred from email lei.cai@oulu.fi)
  - **Affiliation Identifier:** Not found

**Source:** CITATION.cff, DataCite API, setup.py

### 7. Software Name (MANDATORY)
**Value:** GeospaceLAB

**Source:** CITATION.cff, DataCite API, SoMEF, PyHC

### 8. Description (MANDATORY)
**Value:** GeospaceLAB provides a framework of data access, analysis, and visualization for researchers in space physics and space weather. It features a class-based data manager (DataHub, Dataset, Variable), extendable architecture for adding new data sources, comprehensive visualization tools for time series and map projections (including polar views with AACGM coordinates), space coordinate system transformations, and built-in support for numerous data sources including CDAWeb/OMNI, Madrigal/EISCAT, DMSP/SSUSI, ESA SWARM, AMPERE, SuperDARN, and various geomagnetic indices.

**Source:** README.md, PyHC, DataCite API

### 9. Concise Description (OPTIONAL)
**Value:** A Python framework for managing and visualizing data in space physics, with built-in support for numerous data sources including EISCAT, DMSP, SWARM, OMNI, and geomagnetic indices.

**Source:** Derived from README.md and PyHC description

### 10. Publication Date (RECOMMENDED)
**Value:** 2021-03-13

**Source:** SoMEF (GitHub API - repository creation date)
**Note:** This is the date the repository was created. The first release was on 2021-09-02.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/04aj4c181 (Zenodo ROR)

**Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

#### Latest Version (v0.11.0)
- **Version Number:** v0.11.0
- **Version Date:** 2025-06-13
- **Version Description:** Fix the memory leak in Dashboard and Panel objects.
- **Version PID:** https://doi.org/10.5281/zenodo.15656924

**Source:** DataCite API, Zenodo API, SoMEF (GitHub releases)

#### Version in CITATION.cff
- **Version Number:** v0.5.10
- **Version Date:** 2023-02-15
- **Version Description:** Add SuperMAG indices dataset. Bugs fixed.

**Note:** The CITATION.cff file has not been updated to reflect the latest release.

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** SoMEF (GitHub API shows 2,077,173 bytes of Python code), setup.py (Python >=3.7, with classifiers for 3.7-3.11)
**Note:** Also contains Jupyter Notebooks (392,637 bytes) for examples.

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.3389/fspas.2022.1023163

**Source:** README.md (Citation section)
**Full Citation:** Cai L, Aikio A, Kullen A, Deng Y, Zhang Y, Zhang S-R, Virtanen I and Vanhamäki H (2022), GeospaceLAB: Python package for managing and visualizing data in space physics. Front. Astron. Space Sci. 9:1023163.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause

**Source:** LICENSE file, DataCite API, SoMEF
**SPDX Identifier:** BSD-3-Clause

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- analysis
- data analysis
- data access
- data retrieval
- data container
- dmsp
- eiscat
- geospace
- heliophysics
- ionosphere
- ionosphere thermosphere mesosphere
- madrigal
- magnetosphere
- omni
- plotting
- python
- space
- space physics
- space weather
- spaceweather
- swarm
- visualization

**Source:** SoMEF (GitHub topics), setup.py keywords, PyHC keywords

### 17. Data Sources (OPTIONAL)
**Values:**
- CDAWeb
- das2 (Not found)
- FTP/FTPS Directories (Not found)
- HAPI (Not found)
- HTTP/HTTPS Directories (mentioned for data downloads)
- Observatory/Mission-specific (EISCAT, DMSP, SWARM, etc.)
- OMNIWeb (via CDAWeb/OMNI)
- Other (Madrigal, JHUAPL/AMPERE, SuperDARN, WDC, GFZ, TUDelft, UTA/GITM)
- S3/Cloud-aware (Not found)
- SSCWeb (Not found)
- TAP (Not found)
- The Virtual Solar Observatory (Not found)
- VirES (Not found)

**Source:** README.md built-in data sources table
**Note:** GeospaceLAB supports extensive data sources primarily through Madrigal and CDAWeb interfaces.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- ascii
- CDF
- csv (Not found)
- FITS (Not found)
- HDF5
- IDL.sav
- ISTP-Compliant (via CDF files)
- JSON (Not found)
- netCDF3/4
- Other (IAGA2002-ASCII, EISCAT-hdf5, Madrigal-hdf5, binary)
- Zarr (Not found)

**Source:** README.md built-in data sources table (File Format column)

### 19. Output File Formats (RECOMMENDED)
**Values:**
- Not explicitly documented

**Note:** The software primarily focuses on data loading and visualization. Output formats for saved figures (PNG, etc.) are mentioned in examples but data export formats are not explicitly documented.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux (Ubuntu 20.04 mentioned)
- Mac (MacOS Big Sur mentioned)
- Operating System Independent (Python-based)

**Source:** README.md installation section
**Note:** The package is Python-based and should work on any platform supporting Python >=3.7, though Ubuntu 20.04 and MacOS Big Sur are specifically mentioned as tested platforms.

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Source:** Inferred from Python package nature
**Note:** As a pure Python package (with some Cython and Fortran dependencies), it should work on standard CPU architectures.

### 22. Related Phenomena (OPTIONAL)
**Values:**
- auroral emissions
- field-aligned currents
- geomagnetic indices
- ionospheric convection
- ionospheric density
- ionospheric electric fields
- neutral atmosphere
- solar wind

**Source:** Inferred from built-in data sources and README description
**Note:** Specific phenomena covered include aurora (DMSP/SSUSI), field-aligned currents (AMPERE), ionospheric plasma parameters (EISCAT), and solar wind parameters (OMNI).

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** SoMEF (last update 2025-08-14), setup.py (Development Status :: 4 - Beta), PyHC (software_maturity: Good)
**Note:** The project is actively developed with the most recent release (v0.11.0) on 2025-06-13.

### 24. Documentation (RECOMMENDED)
**Value:** https://geospacelab.readthedocs.io/en/latest/

**Source:** README.md, SoMEF, PyHC
**Note:** Also includes GitHub wiki at https://github.com/JouleCai/geospacelab/wiki

### 25. Funder (OPTIONAL)
**Value:** Not found

**Source:** Checked DataCite API, Zenodo API, README.md

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Source:** Checked DataCite API, Zenodo API, README.md

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** https://doi.org/10.1029/2020JA028808

**Source:** README.md (Example 4 section)
**Full Citation:** Cai et al., JGR, 2021, "DMSP observations of the HiLDA aurora"
**Note:** This publication uses GeospaceLAB as demonstrated in Example 4.

### 28. Related Datasets (OPTIONAL)
**Values:**
- CDAWeb/OMNI (solar wind and IMF data)
- CDAWeb/DMSP/SSUSI EDR_AUR (aurora emission data)
- Madrigal/EISCAT (ionospheric radar data)
- Madrigal/GNSS TECMAP (ionospheric TEC maps)
- Madrigal/DMSP satellites (various instruments)
- ESA SWARM mission data
- WDC geomagnetic indices (Dst, AE, ASY/SYM)
- GFZ indices (Kp/Ap, Hp, SN, F107)
- JHUAPL/AMPERE (field-aligned currents)
- SuperDARN (ionospheric convection maps)

**Source:** README.md built-in data sources table
**Note:** These are the primary datasets that GeospaceLAB is designed to work with.

### 29. Related Software (OPTIONAL)
**Values:**
- aacgmv2 (https://github.com/aburrell/aacgmv2) - AACGM coordinate transformations
- apexpy (https://github.com/aburrell/apexpy) - Apex coordinate system
- cartopy - Map projections
- cdflib (https://github.com/MAVENSDC/cdflib) - CDF file reading
- geopack (https://github.com/tsssss/geopack) - Tsyganenko models
- madrigalweb - Madrigal database access
- sscws - SSC web services

**Source:** README.md dependencies section, setup.py install_requires
**Note:** These are key dependencies that GeospaceLAB builds upon.

### 30. Interoperable Software (OPTIONAL)
**Value:** Not explicitly documented

**Note:** While the software uses many dependencies, specific interoperability demonstrations with other PyHC packages are not explicitly documented.

### 31. Related Instruments (OPTIONAL)
**Values:**
- EISCAT (European Incoherent Scatter Scientific Association radars)
- DMSP/SSUSI (Defense Meteorological Satellite Program / Special Sensor Ultraviolet Spectrographic Imager)
- DMSP/SSM (Special Sensor Magnetometer)
- DMSP/SSIES (Special Sensor for Ions, Electrons, and Scintillation)
- DMSP/SSJ (Special Sensor J)
- ESA SWARM/EFI (Electric Field Instrument)
- AMPERE (Active Magnetosphere and Planetary Electrodynamics Response Experiment)
- SuperDARN (Super Dual Auroral Radar Network)
- GNSS (Global Navigation Satellite System) receivers
- Millstone Hill ISR (Incoherent Scatter Radar)
- Poker Flat ISR

**Source:** README.md built-in data sources table

### 32. Related Observatories (OPTIONAL)
**Values:**
- DMSP (Defense Meteorological Satellite Program)
- ESA SWARM mission
- EISCAT Scientific Association
- GOCE (Gravity Field and Steady-State Ocean Circulation Explorer)
- GRACE (Gravity Recovery and Climate Experiment)
- CHAMP (CHAllenging Minisatellite Payload)

**Source:** README.md built-in data sources table

### 33. Logo (OPTIONAL)
**Value:** https://github.com/JouleCai/geospacelab/blob/master/docs/images/logo_v1_landscape_accent_colors.png

**Source:** README.md, PyHC, SoMEF

---

## Metadata Sources Summary

This metadata extraction utilized the following sources in priority order:

1. **PyHC Community Registry** - Manually curated metadata (highest priority)
2. **DataCite API** - Official DOI metadata for concept DOI 10.5281/zenodo.5377318
3. **Zenodo API** - Version-specific metadata for latest release
4. **SoMEF (Software Metadata Extraction Framework)** - Automated repository analysis
5. **Manual Repository Examination:**
   - CITATION.cff
   - README.md
   - LICENSE
   - setup.py
   - Git repository metadata

## Verification Notes

- All URLs have been verified to be properly formatted
- DOIs are correctly formatted (https://doi.org/10.XXXX/XXXXX)
- Author ORCID is properly formatted
- Dates are in YYYY-MM-DD format
- Software Functionality was determined through comprehensive analysis of:
  - README.md feature descriptions
  - Built-in data sources table
  - PyHC keywords
  - Code examples
- Related Region was determined based on:
  - Data sources and their scientific domains
  - PyHC keywords (ionosphere_thermosphere_mesosphere, magnetosphere, geospace)
  - Supported instruments and observatories

## Notes

- **CITATION.cff outdated:** The CITATION.cff file references v0.5.10 (2023-02-15) but the latest release is v0.11.0 (2025-06-13)
- **PyHC Package:** GeospaceLAB is registered in the Python in Heliophysics Community (PyHC) as a community package with "Good" ratings across all quality metrics
- **Active Development:** The package is actively maintained with 16 releases from 2021-2025
- **Comprehensive Data Support:** Built-in support for 20+ data sources covering ionosphere, magnetosphere, and solar wind
- **Author Affiliation:** Author email (lei.cai@oulu.fi) indicates affiliation with University of Oulu, Finland
