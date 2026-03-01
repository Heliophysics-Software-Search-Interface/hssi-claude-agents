# HSSI Metadata Extraction Results

**Repository:** https://github.com/PyGSDR/PyGS
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found - No DOI badge or CITATION.cff file containing DOI in repository

### 3. Code Repository (MANDATORY)
https://github.com/PyGSDR/PyGS

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Models and Simulations:Data Guided

**Source:** Based on README.md and documentation analysis. The software performs flux rope detection and reconstruction using Grad-Shafranov techniques, including 2D cross-section visualization, time series analysis, field configuration characterization, and data retrieval from CDAWeb.

### 5. Related Region (MANDATORY)
- Interplanetary Space
- Solar Environment

**Source:** Inferred from software purpose and supported spacecraft missions (PSP, Solar Orbiter, Ulysses, ACE, WIND), which all measure heliospheric and solar wind phenomena.

### 6. Authors (MANDATORY)

**Author 1:**
- **Authors:** Yu Chen
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** University of Alabama in Huntsville (inferred from email domain)
  - **Affiliation Identifier:** Not found

**Author 2:**
- **Authors:** Qiang Hu
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** University of Alabama in Huntsville (inferred from email domain)
  - **Affiliation Identifier:** Not found

**Author 3:**
- **Authors:** Jinlei Zheng
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** From setup.py author field and LICENSE copyright notice. PyHC registry lists "Yu Chen and Qiang Hu" as contacts.

### 7. Software Name (MANDATORY)
PyGS

**Source:** From repository name, setup.py, README.md, and PyHC registry

### 8. Description (MANDATORY)
This package consists of two key products to serve as a set of comprehensive tools for the investigation of magnetic flux ropes (FRs) in space plasmas based on in-situ spacecraft measurements. The Grad-Shafranov (GS)-based detection (GSD) automatedly identifies flux ropes and outputs their parameters to support statistical analysis, relying on the generalized version of the GS equation. It is applicable to FRs with a broad definition including both static and dynamic structures, and works with PSP, Solar Orbiter, Ulysses, ACE, and WIND spacecraft datasets. The Grad-Shafranov (GS) type reconstruction (GSR) visualizes and characterizes the 2D magnetic field configuration from 1D time-series data, confirms the flux rope detection results, and derives flux rope parameters such as the poloidal and toroidal magnetic fluxes, the relative helicity, and average twist.

**Source:** Compiled from README.md Introduction section

### 9. Concise Description (OPTIONAL)
Magnetic flux rope detection and reconstruction based on the extended Grad-Shafranov equation for in-situ spacecraft measurements.

**Source:** From GitHub repository description

### 10. Publication Date (RECOMMENDED)
2023-05-12

**Source:** From first git commit date

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** No DOI was obtained through Zenodo; code is hosted on GitHub

### 12. Version (RECOMMENDED)
- **Version Number:** 1.0.0
- **Version Date:** Not found (no git tags available)
- **Version Description:** Not found
- **Version PID:** Not found - No DOI for this version

**Source:** From setup.py and README.md installation instructions mentioning "PyGS-1.0.0.tar.gz"

### 13. Programming Language (RECOMMENDED)
- Python 3.x

**Source:** From setup.py (python_requires='>=3'), setup.py classifiers, and PyHC registry

### 14. Reference Publication (RECOMMENDED)
Multiple publications should be cited depending on usage:

**For GSD (Grad-Shafranov Detection):**
- https://doi.org/10.3847/2041-8213/aaa3d7 (Zheng and Hu 2018)
- https://doi.org/10.3847/1538-4365/aae57d (Hu et al. 2018)
- https://doi.org/10.3847/1538-4357/ac3487 (Chen and Hu 2022)

**For GSR (Grad-Shafranov Reconstruction):**
- https://doi.org/10.1029/96GL03573 (Sonnerup & Guo 1996)
- https://doi.org/10.1029/1999JA900002 (Hau & Sonnerup 1999)
- https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2001JA000293 (Hu & Sonnerup 2002)
- https://doi.org/10.3847/1538-4357/ac3487 (Chen and Hu 2022)

**Source:** From README.md "Citations and References" section

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

**Source:** From LICENSE file and setup.py classifier, confirmed by GitHub API and SoMEF

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
heliosphere, 2D_graphics, interactive, csv, cdaweb, data_analysis, ace, psp, ulysses, wind, solo, magnetic flux ropes, grad-shafranov, space plasmas, spacecraft measurements, solar orbiter, in-situ measurements, flux rope detection, flux rope reconstruction

**Source:** From PyHC registry keywords and README.md content analysis

### 17. Data Sources (OPTIONAL)
- CDAWeb

**Source:** From README.md dependencies (ai.cdas package) and PyHC registry keywords

### 18. Input File Formats (RECOMMENDED)
- CDF

**Source:** Inferred from CDAWeb data access (ai.cdas package) and SpacePy dependency, which commonly works with CDF files. Also from PyHC registry keywords.

### 19. Output File Formats (RECOMMENDED)
- csv

**Source:** From README.md stating GSD produces "a csv file including flux rope parameters" and PyHC registry keywords

### 20. Operating System (RECOMMENDED)
- Operating System Independent

**Source:** From setup.py classifier: "Operating System :: OS Independent"

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Source:** Inferred from Python-only implementation with no architecture-specific compiled components

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections

**Source:** Flux ropes are commonly associated with CMEs and other solar eruptive phenomena

### 23. Development Status (RECOMMENDED)
- Active

**Source:** PyHC registry lists software_maturity as "Partially met" (indicating active development but not fully mature). Setup.py classifier states "Development Status :: 5 - Stable". Most recent commit from February 2024 indicates ongoing maintenance.

### 24. Documentation (RECOMMENDED)
https://github.com/PyGSDR/PyGS/tree/main/documentation

**Source:** From PyHC registry and repository structure containing documentation/ folder with instruction files

### 25. Funder (OPTIONAL)
- **Organization:** NASA
- **Funder Identifier:** https://ror.org/027ka1x80

**Source:** From README.md Acknowledgements section: "acknowledge the NASA grant 80NSSC23K0256 for funding"

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found (grant number provided but not award title)
- **Award Number:** 80NSSC23K0256

**Source:** From README.md Acknowledgements section

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.3847/2041-8213/aaa3d7 (Zheng and Hu 2018)
- https://doi.org/10.3847/1538-4365/aae57d (Hu et al. 2018)
- https://doi.org/10.3847/1538-4357/ac3487 (Chen and Hu 2022)
- https://doi.org/10.1029/96GL03573 (Sonnerup & Guo 1996)
- https://doi.org/10.1029/1999JA900002 (Hau & Sonnerup 1999)
- https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2001JA000293 (Hu & Sonnerup 2002)
- https://doi.org/10.1186/s40623-018-0802-z (Teh 2018 - cited in README as basis for GS equation)

**Source:** From README.md "Citations and References" section

### 28. Related Datasets (OPTIONAL)
Not found - No specific datasets mentioned, though software works with data from multiple spacecraft missions

### 29. Related Software (OPTIONAL)
https://github.com/AlexJinlei/Magnetic_Flux_Rope_Detection

**Source:** From README.md acknowledgments - PyGS is "Enhanced and streamlined from the original automated GSD" created by Dr. Jinlei Zheng

### 30. Interoperable Software (OPTIONAL)
- SpacePy (https://github.com/spacepy/spacepy)
- ai.cdas

**Source:** From setup.py install_requires - these are key dependencies that PyGS interfaces with

### 31. Related Instruments (OPTIONAL)

**Instrument 1:**
- **Instrument Name:** Parker Solar Probe (PSP) instruments
- **Instrument Identifier:** Not found

**Instrument 2:**
- **Instrument Name:** Solar Orbiter instruments
- **Instrument Identifier:** Not found

**Instrument 3:**
- **Instrument Name:** Ulysses magnetometer
- **Instrument Identifier:** Not found

**Instrument 4:**
- **Instrument Name:** ACE magnetometer and plasma instruments
- **Instrument Identifier:** Not found

**Instrument 5:**
- **Instrument Name:** WIND magnetometer and plasma instruments
- **Instrument Identifier:** Not found

**Source:** From README.md stating software is "Applicable to PSP, Solar Orbiter, Ulysses, ACE, and WIND spacecraft datasets"

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** Parker Solar Probe

**Observatory 2:**
- **Observatory Name:** Solar Orbiter

**Observatory 3:**
- **Observatory Name:** Ulysses

**Observatory 4:**
- **Observatory Name:** ACE (Advanced Composition Explorer)

**Observatory 5:**
- **Observatory Name:** WIND

**Source:** From README.md and PyHC registry keywords

### 33. Logo (OPTIONAL)
https://github.com/PyGSDR/PyGS/blob/main/logo/logo.png

**Source:** From PyHC registry and confirmed by repository structure containing logo/ folder

---

## Summary of Extraction Methods Used

1. **DOI Search:** No DOI found in repository files (CITATION.cff, .zenodo.json, or README badges)
2. **DataCite/Zenodo APIs:** Not applicable (no DOI found)
3. **SoMEF:** Successfully executed and extracted metadata from repository
4. **PyHC Registry:** Found in PyHC community packages registry with quality ratings and additional metadata
5. **Manual Repository Examination:** Examined README.md, LICENSE, setup.py, documentation files, and git history
6. **Code Analysis:** Analyzed repository structure and dependencies

---

## Notes on Metadata Quality

### High Confidence Fields
- Software Name, Code Repository, Description, Authors, License, Programming Language, Version Number, Documentation URL, Funder, Related Publications all confirmed from multiple sources

### Medium Confidence Fields
- Software Functionality and Related Region determined through comprehensive analysis of README and documentation
- Input/Output Formats inferred from dependencies and documentation
- Related Instruments and Observatories listed in README but without formal identifiers

### Missing Data
- No DOI (Persistent Identifier or Version PID)
- No ORCID identifiers for authors
- No ROR identifiers for affiliations
- No formal version release dates (no git tags)
- No version descriptions/changelogs
- Author affiliation organizations inferred from email domains only

### Recommendations
1. Consider creating a Zenodo DOI for the software to obtain a persistent identifier
2. Add CITATION.cff file with complete citation information including ORCIDs
3. Create git tags for version releases with release notes
4. Add a CHANGELOG.md file documenting version history
