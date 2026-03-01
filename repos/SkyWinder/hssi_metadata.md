# HSSI Metadata Extraction Results

**Repository:** https://github.com/PolarMesosphericClouds/SkyWinder
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** Not found
**Note:** No DOI found in repository files (CITATION.cff, README, codemeta.json, .zenodo.json)

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/PolarMesosphericClouds/SkyWinder
**Source:** GitHub repository URL

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Processing
- Data Visualization:2D Graphics
- Mission-related:Instrumentation
- Mission-related:Operations
- Mission-related:Monitoring
- Mission-related:Analysis

**Source:** Code analysis, README description, and PyHC registry
**Notes:**
- SkyWinder provides modular distributed flight control including telemetry and subsystem coordination for running mobile aeronomy experiments (balloon-borne payloads, airplanes, sounding rockets, suborbital reusable launch vehicles)
- Includes camera control and housekeeping system monitoring
- Provides preliminary image processing (hot pixel correction, format conversion, image analysis)
- Ground station equipment for telemetry reception and commanding
- Image viewing and data visualization capabilities

### 5. Related Region (MANDATORY)
**Value:** Earth Atmosphere
**Source:** README description and PyHC keywords
**Notes:** Software is designed for mid- and upper-atmosphere science instrumentation including aurora, cloud (specifically Polar Mesospheric Clouds), and airglow imagers. The package was adapted from the PMC-Turbo balloon-borne experiment.

### 6. Authors (MANDATORY)
**Author 1:**
- **Name:** Carl Bjorn Kjellstrand
- **Email:** bkjell@gmail.com
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** setup.py and PyHC community registry

### 7. Software Name (MANDATORY)
**Value:** SkyWinder
**Source:** Repository name, README, setup.py, PyHC registry, and SoMEF

### 8. Description (MANDATORY)
**Value:** SkyWinder is an open-source Python package useful for instrument control, telemetry, and image analysis. It is adapted from software that successfully managed flight control, telemetry, preliminary image analysis, and data visualization for a balloon-borne mission and it has broad uses for mid- and upper-atmosphere science instrumentation including aurora, cloud, and airglow imagers. SkyWinder will save future aeronomy experiments significant time and money, and lowers the barrier to entry in analyzing data hosted in public available repositories.

Our software consists of two distinct parts: the flight and analysis modules. The SkyWinder flight package includes modular distributed flight control including telemetry and subsystem coordination for running mobile aeronomy experiments such as balloon-borne payloads, airplanes, sounding rockets, and suborbital reusable launch vehicles (sRLVs), as well as isolated semi-autonomous ground instruments. The SkyWinder analysis software provides functionality more broadly useful in neutral upper atmosphere dynamics, such as pointing reconstruction, image projection, preliminary image processing, and various image analysis techniques.

**Source:** README.md and SoMEF output

### 9. Concise Description (OPTIONAL)
**Value:** An open-source Python package for instrument control, telemetry, and image analysis for mid- and upper-atmosphere science instrumentation including aurora, cloud, and airglow imagers.
**Source:** Derived from README.md (first 200 characters approximate)

### 10. Publication Date (RECOMMENDED)
**Value:** 2022-02-06
**Source:** Git repository creation date (first commit)

### 11. Publisher (RECOMMENDED)
**Publisher:**
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Repository hosted on GitHub, no Zenodo DOI found

### 12. Version (RECOMMENDED)
**Version Number:** v0.0.4
**Version Date:** 2022-09-08
**Version Description:** Not found (no CHANGELOG.md or release notes available)
**Version PID:** Not found

**Source:** Git tags
**Note:** Repository has tags v0.0.4 (most recent, 2022-09-08) and v0.0.3 (2022-09-08). The setup.py file lists version 0.0.3.

### 13. Programming Language (RECOMMENDED)
**Value:** Python 3.x
**Source:** setup.py (requires Python >=3.6), GitHub API, CI/CD workflows (testing with Python 3.9)

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found
**Source:** No CITATION.cff or reference publication found in repository

### 15. License (RECOMMENDED)
**License:** BSD 3-Clause "New" or "Revised" License
**License URI:** https://opensource.org/licenses/BSD-3-Clause
**Source:** LICENSE.md file, setup.py, SoMEF output

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- ionosphere_thermosphere_mesosphere
- geospace
- planetary
- instrumentation
- image
- image processing
- telemetry
- flight control
- balloon-borne
- aeronomy
- aurora
- airglow
- polar mesospheric clouds
- PMC
- upper atmosphere

**Source:** PyHC community registry, README content, and code analysis

### 17. Data Sources (OPTIONAL)
**Value:** Not applicable / Not found
**Source:** Code analysis suggests the package works with locally acquired data from instruments rather than accessing external data sources

### 18. Input File Formats (RECOMMENDED)
**Values:**
- Other (blosc compressed format)
- ascii

**Source:** Code analysis (skywinder/camera/image_processing/blosc_file.py, skywinder/utils/file_reading.py)

### 19. Output File Formats (RECOMMENDED)
**Values:**
- JPEG
- Other (blosc compressed format)

**Source:** Code analysis (skywinder/camera/image_processing/jpeg.py, skywinder/utils/blosc_to_jpeg.py)

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac

**Source:**
- CI/CD workflows test on ubuntu-latest
- README installation instructions mention macOS and Linux
- setup.py lists "Operating System :: OS Independent" but practical usage appears to be Unix-like systems

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent
**Source:** Python-based package with no specific architecture requirements evident in the code

### 22. Related Phenomena (OPTIONAL)
**Values:** Not found in controlled vocabulary, but relevant phenomena include:
- Polar Mesospheric Clouds (PMCs)
- Aurora
- Airglow

**Source:** README.md description

### 23. Development Status (RECOMMENDED)
**Value:** Inactive
**Source:**
- Most recent commit: 2022-09-28
- PyHC registry quality ratings: software_maturity="Good", but documentation="Requires improvement"
- Repository appears to have reached a stable state but is not actively developed (last activity over 2 years ago)

### 24. Documentation (RECOMMENDED)
**Value:** Not found
**Source:** No dedicated documentation site found. No docs/ directory or ReadTheDocs configuration. PyHC registry notes "Requires improvement" for documentation.

### 25. Funder (OPTIONAL)
**Funder:**
- **Organization:** NASA
- **Funder Identifier:** https://ror.org/027ka1x80

**Source:** README.md acknowledgments section states "SkyWinder was developed from the software that ran on the PMC-Turbo balloon borne experiment, which was supported by NASA."

**Funder 2:**
- **Organization:** Python in Heliophysics Community (PyHC)
- **Funder Identifier:** Not found

**Source:** README.md acknowledgments section states "Development of SkyWinder was supported by the Python in Heliophysics Community (PyHC)."

### 26. Award Title (OPTIONAL)
**Value:** Not found
**Source:** No specific grant or award numbers mentioned in repository

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found
**Source:** No publications found citing or describing SkyWinder

### 28. Related Datasets (OPTIONAL)
**Value:** Not found
**Source:** No specific datasets mentioned in repository

### 29. Related Software (OPTIONAL)
**Values:** Dependencies from requirements.txt include:
- numpy (scientific computing)
- Pillow (image processing)
- aiohttp (async HTTP)
- Pyro4 (distributed computing framework)
- pyserial (serial communication)
- pymodbus (Modbus protocol)
- blosc (compression library)

**Source:** requirements.txt and setup.py

### 30. Interoperable Software (OPTIONAL)
**Value:** Not found
**Source:** No explicit interoperability claims or demonstrations found

### 31. Related Instruments (OPTIONAL)
**Values:**
- PMC-Turbo (balloon-borne Polar Mesospheric Cloud imaging instrument)

**Source:** README.md states the software was adapted from PMC-Turbo balloon-borne experiment
**Note:** The software is designed to be broadly applicable to various upper atmosphere imaging instruments, not specific to one instrument

### 32. Related Observatories (OPTIONAL)
**Value:** Not found
**Source:** Software is designed for mobile platforms (balloons, aircraft, rockets) rather than fixed observatories

### 33. Logo (OPTIONAL)
**Value:** Not found
**Source:** No logo file found in repository

---

## Metadata Agreement (MANDATORY)
This metadata was extracted automatically and will need to be reviewed and agreed to by the actual submitter.

---

## Summary of Sources

1. **PyHC Community Registry** - Package is listed with quality ratings and keywords
2. **GitHub Repository** - Code structure, README, LICENSE, setup.py
3. **SoMEF** - Automated metadata extraction (license, programming language, dates)
4. **Git History** - Version tags, commit dates
5. **Code Analysis** - Package structure, file formats, functionality

---

## Notes

- **No DOI found** - Package would benefit from obtaining a Zenodo DOI
- **Limited documentation** - PyHC registry notes documentation requires improvement
- **Development appears inactive** - Last commit over 2 years ago (Sept 2022)
- **Broad applicability** - While developed for PMC-Turbo, designed for general upper atmosphere instrumentation
- **Two-part architecture** - Flight package (instrument control, telemetry) + Analysis package (image processing, visualization)
