# HSSI Metadata Extraction Results

**Repository:** https://github.com/peijin94/LOFAR-Sun-tools
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.48550/arXiv.2205.00065
**Source:** User-provided DOI for the associated publication (arXiv preprint)
**Note:** This DOI is for a related publication, not the software itself. No software-specific DOI (e.g., Zenodo) was found in the repository.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/peijin94/LOFAR-Sun-tools
**Source:** PyHC registry, SoMEF, setup.py

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Spectrogram
- Mission-related:Analysis
- Mission-related:Calibration
- Mission-related:Processing

**Source:** Manual code analysis of three main modules:
- **lofarSun.BF** (Beamformed data): Dynamic spectrum processing, RFI flagging using feature matching (CPU/GPU), beamformed data visualization, time series analysis
- **lofarSun.IM** (Interferometric imaging): Radio interferometry image processing, coordinate transformation (RA/DEC to solar coordinates), calibration with A-team sources, 2D Gaussian fitting, image analysis
- **lofarSun.cli** (Command-line tools): Data inspection utilities, FITS/HDF5 file conversion, measurement set utilities, WSClean command generation

### 5. Related Region (MANDATORY)
**Value:** Solar Environment
**Source:** Package description from PyHC ("LOFAR solar and spaceweather data processing"), paper.md ("solar radio imaging spectroscopy"), and code analysis (solar coordinate transformations, solar position calculations)

### 6. Authors (MANDATORY)

**Primary Authors from paper.md:**

**Author 1:**
- **Author Name:** Peijin Zhang
- **Author Identifier:** Not found (paper.md contains placeholder ORCID: 0000-0000-0000-0000)
- **Affiliations:**
  - **Organization:** Center for Solar-Terrestrial Research, New Jersey Institute of Technology
  - **Affiliation Identifier:** Not found
  - **Organization:** Cooperative Programs for the Advancement of Earth System Science, University Corporation for Atmospheric Research
  - **Affiliation Identifier:** Not found

**Additional Authors from arXiv paper (DOI 10.48550/arXiv.2205.00065):**

**Author 2:**
- **Author Name:** Pietro Zucca
- **Author Identifier:** Not found
- **Affiliation:** Not found in DOI metadata

**Author 3:**
- **Author Name:** Kamen Kozarev
- **Author Identifier:** Not found
- **Affiliation:** Not found in DOI metadata

**Author 4:**
- **Author Name:** Eoin Carley
- **Author Identifier:** Not found
- **Affiliation:** Not found in DOI metadata

**Author 5:**
- **Author Name:** ChuanBing Wang
- **Author Identifier:** Not found
- **Affiliation:** Not found in DOI metadata

**Author 6:**
- **Author Name:** Thomas Franzen
- **Author Identifier:** Not found
- **Affiliation:** Not found in DOI metadata

**Author 7:**
- **Author Name:** Bartosz Dabrowski
- **Author Identifier:** Not found
- **Affiliation:** Not found in DOI metadata

**Author 8:**
- **Author Name:** Andrzej Krankowski
- **Author Identifier:** Not found
- **Affiliation:** Not found in DOI metadata

**Author 9:**
- **Author Name:** Jasmina Magdalenic
- **Author Identifier:** Not found
- **Affiliation:** Not found in DOI metadata

**Author 10:**
- **Author Name:** Christian Vocks
- **Author Identifier:** Not found
- **Affiliation:** Not found in DOI metadata

**Contributor Organization:**
- **Organization:** LOFAR SSWKSP (LOFAR Solar and Space Weather Key Science Project)
- **Affiliation:** ASTRON – The Netherlands Institute for Radio Astronomy

**Note:** The arXiv paper lists 10 authors for the scientific publication. The software repository identifies Peijin Zhang as the primary developer (setup.py, LICENSE, PyHC contact). The other authors likely contributed to the scientific use cases and validation.

### 7. Software Name (MANDATORY)
**Value:** lofarSun (package name) / LOFAR Sun Tools (full name)
**Source:** setup.py (package name: "lofarSun"), README.md (repository title: "LOFAR Sun Tools"), SoMEF, PyHC

### 8. Description (MANDATORY)
**Value:** lofarSun is a Python toolset for solar radio imaging spectroscopy data processing from the Low Frequency Array (LOFAR) telescope. The package provides comprehensive tools for processing LOFAR solar observations, including beamformed data (dynamic spectra), interferometric imaging, and data analysis. It includes three main modules: (1) lofarSun.BF for dynamic spectrum processing with RFI flagging using feature matching methods available on both CPU and GPU; (2) lofarSun.IM for interferometric imaging post-processing, including calibration with A-team sources, coordinate transformations, and 2D Gaussian source fitting; and (3) lofarSun.cli for command-line utilities for data inspection and conversion. The tools are designed to be modular and flexible, enabling high-quality radio observations of the Sun at frequencies below 240 MHz for studying, monitoring, and forecasting solar activity and space weather.

**Source:** Combined from PyHC description, paper.md, README.md, and code analysis

### 9. Concise Description (OPTIONAL)
**Value:** Python tools for LOFAR solar radio imaging spectroscopy data processing, including beamformed data analysis, interferometric imaging, and RFI flagging.

**Source:** Condensed from main description

### 10. Publication Date (RECOMMENDED)
**Value:** 2019-06-07
**Source:** SoMEF (GitHub repository creation date)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Repository hosting platform (no Zenodo DOI found)

### 12. Version (RECOMMENDED)
- **Version Number:** 0.3.33
- **Version Date:** 2025-04-08 (last repository update)
- **Version Description:** Not found (no CHANGELOG.md or release notes found)
- **Version PID:** Not found (no version-specific DOI found)

**Source:** setup.py (version number), SoMEF (date_updated)

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** setup.py (classifiers specify Python 3.9), SoMEF (primary language: Python), GitHub language statistics

**Note:** Repository also contains Jupyter Notebook (1,049,340 bytes - largest by size, used for demonstrations), Common Workflow Language (36,128 bytes), Shell scripts (9,773 bytes), TeX (9,055 bytes), and JavaScript (1,217 bytes), but Python is the primary programming language for the package itself.

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.3847/1538-4357/ac6b37

**Source:** DataCite API for arXiv DOI (relatedIdentifiers with relationType "IsVersionOf")

**Note:** The arXiv preprint (10.48550/arXiv.2205.00065) is a version of this ApJ publication titled "Imaging of the Quiet Sun in the Frequency Range of 20-80 MHz". This publication describes scientific results using the lofarSun tools.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html

**Source:** LICENSE file, setup.py, SoMEF, GitHub API

**Full license text found in:** /repos/LOFAR-Sun-tools/LICENSE

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- LOFAR
- Solar
- radio
- Solar and Stellar Astrophysics
- Space Physics
- radio interferometry
- astronomy
- solar physics

**Source:** setup.py (LOFAR, Solar, radio), DataCite API/arXiv (Solar and Stellar Astrophysics, Space Physics), paper.md tags (radio interferometry, astronomy, solar physics), SoMEF (lofar, solar), GitHub topics (lofar, solar)

### 17. Data Sources (OPTIONAL)
**Value:** Observatory/Mission-specific (LOFAR)

**Source:** The software is specifically designed for LOFAR (Low Frequency Array) telescope data

### 18. Input File Formats (RECOMMENDED)
**Values:**
- HDF5
- FITS
- IDL.sav (IDL save files)
- Other (Measurement Sets - radio interferometry standard format)

**Source:** Code analysis
- lofarSun/BF/BFdata.py: load_sav_xy(), load_sav_radec() for IDL .sav files; load_fits() for FITS
- lofarSun/IM/IMdata.py: load_fits() for FITS files
- lofarSun/cli/h5_to_fits_spec.py: compress_h5() for HDF5 files
- Documentation and code references to Measurement Sets (.ms files)

### 19. Output File Formats (RECOMMENDED)
**Values:**
- FITS
- HDF5

**Source:** Code analysis
- lofarSun/BF/BFdata.py: write_fits(), write_fits_full() methods for FITS output
- lofarSun/cli/h5_to_fits_spec.py: conversion from HDF5 to FITS

### 20. Operating System (RECOMMENDED)
**Value:** OS Independent (Linux preferred for HPC workflows)

**Source:** Python package with standard dependencies suggests OS independence. Documentation and shell scripts (utils/IM/slurmScripts/) indicate Linux is commonly used for processing workflows, particularly on HPC systems.

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- CPU Independent
- GPU (optional, for RFI flagging)

**Source:** paper.md mentions "RFI flagging uses a feature matching based method available both on CPU and GPU". setup.py lists torch as a dependency, which supports GPU acceleration.

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Solar Corona
- Solar Flares (likely, given radio observations)
- Coronal Heating (possibly, given quiet Sun observations in reference paper)

**Source:** Reference publication title "Imaging of the Quiet Sun in the Frequency Range of 20-80 MHz" indicates coronal observations. Solar radio observations typically study solar flares and coronal phenomena.

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:**
- setup.py classifiers: "Development Status :: 4 - Beta"
- SoMEF: last updated 2025-04-08
- PyHC quality ratings: Software maturity "Partially met", indicating active but not fully mature

**Note:** According to repostatus.org definitions, this would map to "Active - The project has reached a stable, usable state and is being actively developed"

### 24. Documentation (RECOMMENDED)
**Value:** https://lofar-sun-tools.readthedocs.io/en/latest/

**Source:** README.md, PyHC registry, SoMEF, paper.md

**Note:** PyHC rates documentation as "Good"

### 25. Funder (OPTIONAL)
**Values:** Multiple funders acknowledged in paper.md

**Organizations (partial list from acknowledgments):**
- CNRS-INSU (France)
- Observatoire de Paris (France)
- Universite d'Orleans (France)
- BMBF (Germany)
- MIWF-NRW (Germany)
- MPG (Germany)
- Science Foundation Ireland (SFI)
- Department of Business, Enterprise and Innovation (DBEI), Ireland
- NWO (The Netherlands)
- Science and Technology Facilities Council (STFC), UK
- Ministry of Science and Higher Education (Poland)
- Istituto Nazionale di Astrofisica (INAF), Italy

**Funder Identifiers:** Not found

**Note:** These funders support LOFAR infrastructure and operations. Specific grant information for software development not found in repository.

### 26. Award Title (OPTIONAL)
**Award Title:** Not found
**Award Number:** Not found

**Note:** Acknowledgments mention ST/P000096/1 supporting LOFAR-UK compute facility, but no specific software development awards identified

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Publication 1:**
**Value:** https://doi.org/10.48550/arXiv.2205.00065
**Source:** User-provided; arXiv preprint describing quiet Sun observations using LOFAR

**Publication 2:**
**Value:** https://doi.org/10.3847/1538-4357/ac6b37
**Source:** DataCite API (published version of the arXiv preprint in The Astrophysical Journal)

**Note:** These publications demonstrate scientific applications of the lofarSun tools. Additional references in paper.md include citations for LOFAR telescope description and data processing methods but are not listed here as they are background references rather than publications using/describing this software.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Note:** README.md mentions test data available at https://pjzhang.cc/static/demo_data.7z but this is demonstration data rather than a citable dataset. No DOI or formal dataset citation found.

### 29. Related Software (OPTIONAL)

**Software Dependencies (from setup.py):**
- **SunPy** - Python for Solar Physics (PyHC Core package)
  - Repository: https://github.com/sunpy/sunpy
  - Description: Used for solar coordinate transformations and solar position calculations
- **Astropy** - Core astronomy package
  - Repository: https://github.com/astropy/astropy
- **python-casacore** - Python bindings for CASA core libraries
  - Used for Measurement Set (radio interferometry data) access

**External Processing Tools (mentioned in paper.md and code):**
- **WSClean** - 2D FFT and deconvolution for radio imaging
  - Reference: Offringa et al. 2014
  - URL: https://gitlab.com/aroffringa/wsclean
- **LINC Pipeline** - LOFAR preprocessing pipeline
  - Reference: de Gasperin et al. 2019

**Source:** setup.py (install_requires), code analysis (imports and CLI tools), paper.md

### 30. Interoperable Software (OPTIONAL)
**Value:** SunPy (https://github.com/sunpy/sunpy)

**Source:** Code analysis shows lofarSun.IM.IMdata.make_map() creates sunpy.map.Map objects, demonstrating interoperability with the SunPy ecosystem. SunPy is a PyHC Core package.

### 31. Related Instruments (OPTIONAL)

**Instrument 1:**
- **Instrument Name:** LOFAR (Low Frequency Array)
- **Instrument Identifier:** Not found

**Note:** The software is specifically designed for LOFAR telescope data. LOFAR operates at frequencies 10-240 MHz with stations primarily in the Netherlands and across Europe.

**Source:** Package name, description, and all documentation

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** LOFAR (Low Frequency Array)

**Note:** LOFAR is both an observatory and an instrument network. Primary location in the Netherlands with international stations.

**Source:** Package name, description, paper.md acknowledgments, code (IMdata.py specifies LOFAR location: lat=52.905329712°, lon=6.867996528°)

### 33. Logo (OPTIONAL)
**Value:** https://lofar-sun-tools.readthedocs.io/en/latest/_static/logo0.png

**Source:** PyHC registry

---

## PyHC Package Information

This package is listed in the **PyHC Community Packages** registry.

**PyHC Quality Ratings:**
- Community: Partially met
- Documentation: Good
- Testing: Requires improvement
- Software Maturity: Partially met
- Python 3: Good
- License: Good

**Source:** https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects.yml

---

## Additional Notes

### Metadata Extraction Sources Summary

1. **DataCite API** (DOI 10.48550/arXiv.2205.00065): Provided author information, publication metadata, license, keywords, and related publication DOI
2. **PyHC Registry** (Community Packages): Provided package name, description, documentation URL, logo, contact, and quality ratings
3. **SoMEF** (Repository Analysis): Provided repository metadata, languages, dates, license, keywords, file formats
4. **Manual Repository Examination:**
   - setup.py: Package name, version, dependencies, classifiers, author email
   - paper.md: Detailed authors with affiliations, software description, acknowledgments
   - LICENSE: Full MIT license text
   - README.md: Basic description and documentation link
   - Code analysis (lofarSun/BF/, lofarSun/IM/, lofarSun/cli/): Software functionality, file formats, interoperability

### Fields Requiring Additional Information from Submitter

- **Submitter Name and Email** (Field 1): Required from actual submitter
- **Persistent Identifier for Software** (Field 2): Consider creating a Zenodo DOI for the software repository
- **Author ORCIDs** (Field 6): Peijin Zhang's ORCID was not found (placeholder in paper.md); ORCIDs for co-authors not available
- **Author Affiliations with ROR IDs** (Field 6): ROR identifiers not found for institutions
- **Version Description** (Field 12): No changelog found; recommend adding CHANGELOG.md
- **Funder ROR IDs** (Field 25): Could be added if needed
- **Award Numbers** (Field 26): Specific grants for software development unclear

### Recommendations

1. **Create a Zenodo DOI** for the software repository to provide a citable, persistent identifier distinct from publication DOIs
2. **Add CITATION.cff file** with complete author information including ORCIDs and affiliations
3. **Create CHANGELOG.md** to document version history and changes
4. **Add version tags** in git to track releases
5. **Consider adding .zenodo.json** to improve Zenodo metadata if creating a DOI
6. **Document test data** with proper citation if it should be referenced as a dataset

### Related Region Analysis

The software is classified as **Solar Environment** based on:
- Observations of the Sun's corona and quiet Sun
- Solar radio emission studies
- Solar coordinate system transformations (helioprojective coordinates)
- Solar position angle and rotation calculations
- Focus on solar physics and space weather

While space weather applications might extend to **Interplanetary Space**, the primary scientific focus and data processing is for **Solar Environment**.

### Software Functionality Analysis

The software provides comprehensive data processing capabilities:

**Data Processing and Analysis:**
- Calibration with A-team sources (calibrator observations)
- RFI (Radio Frequency Interference) flagging using feature matching
- Image processing (rotation, shifting, Gaussian filtering)
- Spectral analysis (dynamic spectra, spectrograms)
- Time series analysis
- File format conversion (HDF5, FITS, IDL .sav, Measurement Sets)
- Data access and retrieval utilities

**Data Visualization:**
- 2D imaging with customizable colormaps
- Line plots and spectrograms
- Beam shape visualization
- Contour plots for FWHM analysis

**Mission-related:**
- LOFAR-specific data processing workflows
- Beamformed data processing
- Interferometric imaging calibration and processing
- Integration with LOFAR pipelines (LINC)
- Observatory-specific coordinate transformations

---

## Verification Notes

All metadata has been extracted from verifiable sources:
- API responses saved to /tmp/ directory
- Repository files directly examined
- Code analyzed for functionality classification
- Cross-referenced multiple sources for accuracy (PyHC, SoMEF, repository files, DOI metadata)

**Confidence Level:** High for most fields. Medium confidence for fields requiring domain expertise (Related Phenomena) or where multiple interpretations are possible.
