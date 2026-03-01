# HSSI Metadata Extraction Results

**Repository:** https://gitlab.com/aidaspace/aidapy
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** Not found

**Note:** No DOI was found in the repository files (CITATION.cff, README, or other standard locations).

### 3. Code Repository (MANDATORY)
**Value:** https://gitlab.com/aidaspace/aidapy

**Source:** Repository URL

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Analysis
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:ML/AI
- Data Processing and Analysis:3D Particle Distribution Processing
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Plasma Moments
- Data Processing and Analysis:Curlometer
- Data Processing and Analysis:Image Processing
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Spectrogram
- Models and Simulations
- Models and Simulations:ML/AI
- Models and Simulations:Data Guided
- Models and Simulations:Forecasting

**Source:** Analysis of README, CHANGELOG, examples directory structure, and package modules:
- **aidapy.aidafunc**: Data retrieval from missions (OMNI, MMS, Cluster), event search
- **aidapy.aidaxr**: Statistical analysis, velocity distribution functions (VDFs), curlometer technique for multi-spacecraft current density calculations, plasma beta calculations, event detection
- **aidapy.ml**: Machine learning models (UNet, LSTM, MLP, GMM) for coronal hole detection, DST index forecasting, particle distribution analysis
- **Examples**: Coronal hole detection (04_coronal_holes), DST forecasting (02_omni_regressor, 05_omni_regressor_lstm), GMM for reconnection analysis (03_gmm), VDF analysis (01_missions)

### 5. Related Region (MANDATORY)
**Values:**
- Earth Magnetosphere
- Interplanetary Space
- Solar Environment

**Source:** Analysis of supported missions and use cases:
- **Earth Magnetosphere**: MMS (Magnetospheric Multiscale) and Cluster mission data support
- **Interplanetary Space**: OMNI solar wind data, heliospheric mission data
- **Solar Environment**: Coronal hole detection from SDO (Solar Dynamics Observatory) images

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Romain Dupuis
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Author 2:**
- **Name:** Jorge Amaya
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Author 3:**
- **Name:** Giovanni Lapenta
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** PyHC community registry. Additional contact information in setup.py lists "AIDA Consortium" as author with email coordinator.aida@kuleuven.be.

### 7. Software Name (MANDATORY)
**Value:** AIDApy

**Source:** README.rst, setup.py, SoMEF

### 8. Description (MANDATORY)
**Value:** The Python package `aidapy` centralizes and simplifies access to spacecraft data from heliospheric missions, space physics simulations, advanced statistical tools, and Machine Learning/Deep Learning algorithms and applications. It provides a simple mechanism for downloading multi-dimensional time-series from various sources and analyzing them by extracting different meaningful statistics. The package includes four main sub-packages: Mission tool, Event search tool, Velocity distribution function tool, and Machine learning tool. It features easy data download from heliophysics missions, xarray data structures for statistical analysis, sophisticated event identification, multiple heliophysics use-cases ready to use, simple interface based on configuration files, easy mechanism to add custom metrics and datasets, visualization and logging of training/validation procedures, and optimization techniques such as Hyper-Parameter Optimization (HPO) and pruning.

**Source:** Consolidated from README.rst and SoMEF description field

### 9. Concise Description (OPTIONAL)
**Value:** AI package for heliophysics providing machine learning and statistical methods for spacecraft data analysis

**Source:** setup.py and PyHC registry

### 10. Publication Date (RECOMMENDED)
**Value:** 2020-06-24

**Source:** CHANGELOG.rst indicates v0.0.2 (first release) on 2020-06-24

### 11. Publisher (RECOMMENDED)
- **Organization:** GitLab
- **Publisher Identifier:** https://gitlab.com

**Source:** Code repository is hosted on GitLab, no DOI publisher found

### 12. Version (RECOMMENDED)

**Latest Version (v0.0.4):**
- **Version Number:** 0.0.4
- **Version Date:** 2020-09-23
- **Version Description:** Second release of aidapy. New features include B-field aligned reference frames for VDF analysis, new VDF plotting methods (xy_plane, spher_gyro), electron heat flux support for MMS mission, expanded test coverage, and bug fixes for spacecraft position handling.
- **Version PID:** Not found

**Previous Version (v0.0.2):**
- **Version Number:** 0.0.2
- **Version Date:** 2020-06-24
- **Version Description:** First release of aidapy featuring data access from OMNI/Cluster/MMS missions, xarray extensions with statistical methods and VDF analysis, ML tools (MLP, GMM), event search functionality, and comprehensive documentation.
- **Version PID:** Not found

**Source:** CHANGELOG.rst, git tags, SoMEF releases

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** setup.py (python_requires='>=3.5'), README mentions Python 3.6, PyHC registry indicates "Good" Python3 support

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Note:** An arXiv paper is mentioned in one example file (https://arxiv.org/abs/1910.10012 - AIDA paper) but no formal reference publication DOI was found in standard locations.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT

**Source:** setup.py, LICENSE.txt, SoMEF, PyHC registry

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- machine_learning
- heliosphere
- data_analysis
- artificial intelligence
- space physics
- magnetosphere
- spacecraft data
- MMS
- Cluster
- OMNI
- velocity distribution functions
- statistical analysis
- deep learning
- coronal holes
- DST index
- event detection
- xarray
- pytorch

**Source:** PyHC registry, README.rst, setup.py classifiers, examples, and inferred from functionality

### 17. Data Sources (OPTIONAL)
**Values:**
- Observatory/Mission-specific

**Source:** README and package documentation indicate support for:
- MMS (Magnetospheric Multiscale) mission
- Cluster mission
- OMNI solar wind database
- SDO (Solar Dynamics Observatory) for coronal hole detection
- Uses heliopy for data access

### 18. Input File Formats (RECOMMENDED)
**Values:**
- CDF
- HDF5
- netCDF3/4
- ascii
- csv

**Source:**
- Dependencies in setup.py include: cdflib, h5netcdf, h5py (in ml extras)
- Requirements.txt includes: h5py, xarray (supports netCDF)
- setup.py classifiers mention file format conversion

### 19. Output File Formats (RECOMMENDED)
**Values:**
- HDF5
- ascii
- csv

**Source:** Inferred from dependencies (h5py, joblib) and typical scientific Python workflows; xarray supports multiple output formats

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Windows

**Source:** README.rst explicitly states "The package aidapy has been tested for Linux (Ubuntu 16.04 / 18.04) and Windows 10"

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- CPU Independent
- GPU

**Source:**
- Python package is generally CPU independent
- ML functionality (PyTorch in requirements) supports GPU acceleration

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Coronal Holes
- Solar Wind

**Source:**
- Coronal hole detection is a major use case (examples/04_coronal_holes)
- Solar wind data analysis through OMNI database support
- DST index forecasting related to geomagnetic storms

### 23. Development Status (RECOMMENDED)
**Value:** WIP

**Note:** While SoMEF could not determine repository status with high confidence, the last release (v0.0.4) was in September 2020. The software reached usable state but appears to be in early development with version 0.0.x. Based on typical software lifecycle, this appears to be "Work in Progress" though it could also be considered "Active" or "Inactive" depending on recent commit activity.

**Source:** Git tags, version numbers (0.0.x series), PyHC registry shows "Partially met" for software maturity

### 24. Documentation (RECOMMENDED)
**Value:** https://aidapy.readthedocs.io

**Source:** README.rst, setup.py, PyHC registry, SoMEF

### 25. Funder (OPTIONAL)

**Funder 1:**
- **Organization:** European Commission - Horizon 2020
- **Funder Identifier:** Not found (but likely https://ror.org/00k4n6c32 for European Commission)

**Source:** README.rst states: "The `aidapy` package is part of the project AIDA (Artificial Intelligence Data Analysis) in Heliophysics funded from the European Unions Horizon 2020 research and innovation programme under grant agreement No 776262."

### 26. Award Title (OPTIONAL)

**Award 1:**
- **Award Title:** AIDA (Artificial Intelligence Data Analysis) in Heliophysics
- **Award Number:** 776262

**Source:** README.rst

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values:**
- Not found

**Note:** An arXiv paper (https://arxiv.org/abs/1910.10012) is mentioned in example code but not formally listed as a related publication.

### 28. Related Datasets (OPTIONAL)
**Values:**
- Not found

**Note:** The software accesses MMS, Cluster, and OMNI datasets, but specific dataset DOIs were not found in the repository.

### 29. Related Software (OPTIONAL)
**Values:**
- HelioPy (https://github.com/heliopython/heliopy) - Dependency
- heliopy-multid - Dependency
- SunPy (https://github.com/sunpy/sunpy) - Dependency for solar data
- xarray - Core data structure dependency
- PyTorch - For machine learning functionality
- scikit-learn - For machine learning functionality
- Optuna - For hyperparameter optimization
- Albumentations - For image augmentation

**Source:** setup.py install_requires and extras_require, requirements.txt

### 30. Interoperable Software (OPTIONAL)
**Values:**
- HelioPy
- SunPy
- xarray

**Source:** Package design indicates direct interoperability with HelioPy (wraps it), SunPy (listed as dependency), and xarray (extends it). README states it "inherits many features from high-level data structures such as xarray."

### 31. Related Instruments (OPTIONAL)

**Instrument 1:**
- **Instrument Name:** MMS (Magnetospheric Multiscale Mission)
- **Instrument Identifier:** Not found

**Instrument 2:**
- **Instrument Name:** Cluster
- **Instrument Identifier:** Not found

**Instrument 3:**
- **Instrument Name:** SDO/AIA (Solar Dynamics Observatory / Atmospheric Imaging Assembly)
- **Instrument Identifier:** Not found

**Source:** README, examples, CHANGELOG indicate support for MMS, Cluster, and SDO data

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** MMS (Magnetospheric Multiscale)

**Observatory 2:**
- **Observatory Name:** Cluster

**Observatory 3:**
- **Observatory Name:** SDO (Solar Dynamics Observatory)

**Source:** Mission data support documented in README and examples

### 33. Logo (OPTIONAL)
**Value:** Not found

**Note:** No logo file or URL was found in the repository or PyHC registry entry.

---

## Metadata Agreement (MANDATORY)
**Status:** To be agreed to by actual submitter

---

## Extraction Notes

### Data Collection Methods Used:
1. **SoMEF Analysis**: Successfully extracted repository metadata including releases, authors, description, license, installation instructions, and usage examples
2. **PyHC Registry Check**: Found aidapy in PyHC community packages with additional curated metadata
3. **Repository File Analysis**: Examined README.rst, setup.py, CHANGELOG.rst, LICENSE.txt, package structure
4. **Code Structure Analysis**: Analyzed package modules (aidafunc, aidaxr, ml, tools) and examples directory
5. **Git History**: Checked tags and version information

### No DOI Found:
No persistent identifier (DOI) was discovered in standard locations (CITATION.cff, .zenodo.json, README badges, codemeta.json). This limits automated metadata extraction via DataCite/Zenodo APIs.

### Key Strengths:
- Comprehensive README with clear installation and usage instructions
- Well-documented examples covering major use cases
- Active PyHC community package
- Clear licensing (MIT)
- Good test coverage noted in CHANGELOG

### Metadata Gaps:
- No DOI or persistent identifier
- No CITATION.cff file with author ORCIDs and affiliations
- No formal reference publication listed
- Author affiliations not specified in repository
- No logo provided
- Limited version metadata (only 2 releases documented)

### Recommended Improvements for Future Submissions:
1. Create CITATION.cff file with complete author information including ORCIDs and affiliations
2. Register a Zenodo DOI for the software
3. Include reference publication DOI if available
4. Add logo to repository and PyHC registry
5. Consider creating releases for newer versions if development continues
