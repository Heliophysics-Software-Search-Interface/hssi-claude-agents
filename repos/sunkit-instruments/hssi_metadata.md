# HSSI Metadata Extraction Results

**Repository:** https://github.com/sunpy/sunkit-instruments
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.6578605
**Source:** Concept DOI from Zenodo (covers all versions)

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/sunpy/sunkit-instruments
**Source:** Repository URL

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: File Format Conversion
- Data Visualization: Line Plots
- Mission-related: Instrumentation
- Mission-related: Instrument Response

**Source:** Code analysis of repository structure. The package provides:
- GOES-XRS: Temperature and emission measure calculations, flare event retrieval, flux/flare class conversions
- Fermi/GBM: Detector sun angle calculations and plotting
- PROBA2/LYRA: Time series data processing with LYTAF event removal
- RHESSI: Image cube to map sequence extraction
- SUVI: FITS/NetCDF file reading, despiking, response functions
- Response module: Temperature and wavelength response function calculations for instrument channels

### 5. Related Region (MANDATORY)
**Value:** Solar Environment
**Source:** Code analysis and PyHC registry. All instruments (GOES-XRS, Fermi/GBM, LYRA, RHESSI, SUVI) observe the Sun and solar phenomena.

### 6. Authors (MANDATORY)
**Values:**
1. **DanRyanIrish** (Dan Ryan)
2. **Stuart Mumford**
   - Affiliation: Aperio Software
3. **Nabil Freij**
   - Affiliation: SETI Institute & LMSAL
4. **aringlis** (Andrew Inglis)
5. **Drew Leonard**
6. **Steven Christe**
   - Affiliation: NASA Goddard Space Flight Center
7. **vn-ki**
8. **Albert Y. Shih**
9. **Silvan Laube**
10. **Brigitta Sipőcz**
    - Affiliation: Caltech/IPAC
11. **Keith Hughitt**
    - Affiliation: National Institutes of Health
12. **Asish Panda**
    - Affiliation: International Institute of Information Technology Bhubaneswar
13. **Jack Ireland**
14. **David Pérez-Suárez**
    - Affiliation: UCL-ARC
15. **Larry Manley**
16. **David Stansby**
    - Affiliation: UCL
17. **Yash Jain**
18. **Alex-Ian-Hamilton**
19. **derdon**
20. **Will Barnes**
    - Affiliation: American University
21. **Nitin Choudhary**
    - Affiliation: @kossiitkgp
22. **Daniel Williams**
    - Affiliation: University of Glasgow
23. **Laura Hayes**
24. **Samuel Bennett**
    - Affiliation: University of Sheffield
25. **Michael Charlton**
26. **Pritish Chakraborty**
27. **Carlos Molina**
    - Affiliation: @SUGUS-GNULinux
28. **Rishabh Sharma**

**Primary Contact (from pyproject.toml):** The SunPy Community (sunpy@googlegroups.com)

**Source:** DataCite API, Zenodo API

**Note:** Author ORCID identifiers were not found in the available metadata sources (DataCite, repository files).

### 7. Software Name (MANDATORY)
**Value:** sunkit-instruments
**Source:** GitHub API, pyproject.toml, PyHC registry

### 8. Description (MANDATORY)
**Value:** sunkit-instruments is a SunPy-affiliated package for solar instrument-specific tools. Its purpose is not to be a repository for all tools for all instruments. Instead it is intended to perform three main roles: (1) Hold instrument tools that are so few they do not warrant their own package; (2) Hold tools for instruments with no instrument team or the instrument team does not currently support solar applications; (3) Act as an incubator for instrument-specific tools that can evolve into a separate instrument package, backed by an instrument team. The package currently provides tools for GOES-XRS, Fermi/GBM, PROBA2/LYRA, RHESSI, and GOES/SUVI instruments, including data processing, calibration, instrument response calculations, and visualization capabilities.

**Source:** README.rst, PyHC registry, code analysis

### 9. Concise Description (OPTIONAL)
**Value:** A SunPy-affiliated package providing analysis and calibration tools for multiple solar observing instruments including GOES-XRS, Fermi/GBM, PROBA2/LYRA, RHESSI, and SUVI.

**Source:** Synthesized from README.rst

### 10. Publication Date (RECOMMENDED)
**Value:** 2020-04-02
**Source:** SoMEF (GitHub API repository creation date)

### 11. Publisher (RECOMMENDED)
**Values:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)
**Version Number:** v0.6.2
**Version Date:** 2025-07-09
**Version Description:** Bug fixes including: Updating the maximum supported GOES satellite to GOES 19 for temperature and emission measure calculation; Updated GOES event list to account for change in the HEK results from sunpy 7.0.
**Version PID:** https://doi.org/10.5281/zenodo.15852260

**Source:** DataCite API, Zenodo API, CHANGELOG.rst, git tags

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** SoMEF (GitHub API), pyproject.toml (requires-python >= 3.12)

**Note:** The package requires Python 3.12 or higher as of version 0.6.2.

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found
**Source:** No reference publication DOI found in DataCite API, README, or CITATION files.

### 15. License (RECOMMENDED)
**Values:**
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause

**Source:** DataCite API, Zenodo API, LICENSE.rst, pyproject.toml

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- solar
- specific
- instrumentation
- GOES
- Fermi
- LYRA
- RHESSI
- SUVI
- instrument response
- temperature response
- wavelength response
- flare detection
- calibration

**Source:** PyHC registry, code analysis, README

### 17. Data Sources (OPTIONAL)
**Values:**
- Observatory/Mission-specific

**Source:** Code analysis. The package retrieves GOES flare events via HEK (Heliophysics Event Knowledgebase) and Fermi spacecraft data.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- FITS
- netCDF3/4
- HDF5

**Source:** Code analysis. The package reads FITS files (RHESSI, SUVI), NetCDF files (SUVI), and HDF5 files (SUVI).

### 19. Output File Formats (RECOMMENDED)
**Values:**
- Not found (primarily returns processed data structures in memory)

**Source:** Code analysis. The package primarily works with in-memory data structures (SunPy Maps, TimeSeries, xarray DataArrays) rather than writing output files.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows
- Operating System Independent

**Source:** Inferred from Python package structure and pyproject.toml. Python packages are generally OS-independent unless they have compiled extensions.

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- CPU Independent

**Source:** Inferred from Python package. No architecture-specific compiled components detected.

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Solar Flares
- X-ray emission
- Coronal Heating

**Source:** Code analysis. The package includes GOES flare class conversions, X-ray flux analysis, and temperature/emission measure calculations relevant to coronal heating studies.

### 23. Development Status (RECOMMENDED)
**Value:** Active
**Source:** PyHC registry (software_maturity: Good), SoMEF (last updated 2025-10-08), recent releases

### 24. Documentation (RECOMMENDED)
**Value:** https://docs.sunpy.org/projects/sunkit-instruments
**Source:** pyproject.toml, PyHC registry, SoMEF

### 25. Funder (OPTIONAL)
**Value:** Not found
**Source:** No funding information in DataCite API or repository files

### 26. Award Title (OPTIONAL)
**Value:** Not found
**Source:** No award information in DataCite API or repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found
**Source:** No related publications found in DataCite API relatedIdentifiers

### 28. Related Datasets (OPTIONAL)
**Value:** Not found
**Source:** No related datasets found in DataCite API

### 29. Related Software (OPTIONAL)
**Values:**
- **sunpy** (https://github.com/sunpy/sunpy) - Primary dependency, provides core solar physics data structures
- **astropy** - Astronomy data structures and units
- **xarray** - Multi-dimensional labeled arrays
- **numpy** - Numerical computing
- **scipy** - Scientific computing
- **matplotlib** - Visualization
- **pandas** - Data analysis
- **h5py** - HDF5 file I/O

**Source:** pyproject.toml dependencies, SoMEF requirements

### 30. Interoperable Software (OPTIONAL)
**Values:**
- **sunpy** (https://github.com/sunpy/sunpy) - Designed as a SunPy-affiliated package, fully interoperable
- **ndcube** - Works with multi-dimensional coordinate-aware data
- **aiapy** - Example of instrument-specific package mentioned in README

**Source:** README.rst, pyproject.toml, PyHC ecosystem knowledge

### 31. Related Instruments (OPTIONAL)
**Values:**
1. **GOES X-Ray Sensor (XRS)** - Geostationary Operational Environmental Satellite X-ray Sensor (GOES 8-19)
2. **Fermi Gamma-ray Burst Monitor (GBM)** - Fermi spacecraft
3. **PROBA2/LYRA** - Large Yield Radiometer on PROBA2
4. **RHESSI** - Reuven Ramaty High Energy Solar Spectroscopic Imager
5. **SUVI** - Solar Ultraviolet Imager on GOES-R series (GOES 16-19)

**Source:** Code structure analysis (module names: goes_xrs/, fermi/, lyra/, rhessi/, suvi/)

### 32. Related Observatories (OPTIONAL)
**Values:**
1. **GOES (Geostationary Operational Environmental Satellite)** - GOES 8-19
2. **Fermi Gamma-ray Space Telescope**
3. **PROBA2 (Project for On-Board Autonomy 2)**
4. **RHESSI (Reuven Ramaty High Energy Solar Spectroscopic Imager)**

**Source:** Code analysis and instrument documentation

### 33. Logo (OPTIONAL)
**Value:** Not found
**Source:** No logo URL found in PyHC registry, repository, or Zenodo

---

## Additional Notes

### PyHC Package Status
This package is listed in the PyHC (Python in Heliophysics Community) community registry with the following quality ratings:
- **Community:** Partially met
- **Documentation:** Partially met
- **Testing:** Good
- **Software Maturity:** Good
- **Python 3:** Good
- **License:** Good

### Version History
The package has had 8 major releases from v0.1.0 (2020-09-30) to v0.6.2 (2025-07-09), showing active ongoing development.

### Key Dependencies
The package is part of the SunPy ecosystem and requires:
- sunpy >= 7.0.0 (with map, net, timeseries, and visualization extras)
- Python >= 3.12
- Standard scientific Python stack (numpy, scipy, matplotlib, pandas, astropy, xarray, h5py)

### Supported Instruments Details
1. **GOES-XRS:** Temperature and emission measure calculations using CHIANTI atomic database, flare event retrieval from HEK, flux/flare class conversions
2. **Fermi/GBM:** Detector sun angle calculations and visualization
3. **PROBA2/LYRA:** Time series processing with LYTAF (LYRA Timeline Annotation File) event filtering
4. **RHESSI:** Image cube to map sequence extraction for 4D datacubes
5. **SUVI:** FITS/NetCDF reading, L1b despiking, response function calculations, supports all GOES-R series flight models (FM1-FM4, GOES 16-19)

### Response Function Framework
The package includes a general framework for computing instrument response functions (wavelength and temperature response) that can be extended to additional instruments.
