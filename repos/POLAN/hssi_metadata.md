# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/POLAN
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found

**Note:** No DOI was found in repository files, README, or other metadata sources.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/POLAN

**Source:** GitHub API via SoMEF

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Processing
- Models and Simulations
- Models and Simulations:Empirical

**Source:** Manual analysis of README and code purpose. POLAN performs polynomial analysis to calculate real-height profiles from sweep-frequency ionogram data (virtual height measurements from ionosondes). This involves processing and reducing ionospheric sounding data to estimate true ionospheric height profiles. The software also implements empirical models including Chapman layer peak fitting and ionospheric valley modeling between E and F layers.

### 5. Related Region (MANDATORY)
- Earth Atmosphere

**Source:** Manual analysis. The ionosphere is a region of Earth's upper atmosphere (approximately 60-1000 km altitude). The software processes ionosonde data which measures the Earth's ionosphere.

### 6. Authors (MANDATORY)

**Author 1:**
- **Authors:** J. E. Titheridge
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** University of Auckland (historical, based on README.1ST contact information)
  - **Affiliation Identifier:** https://ror.org/03b94tp07

**Author 2 (Package Maintainer):**
- **Authors:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** README.1ST lists J.E. Titheridge as original author (1980s-1990s); LICENSE file shows "Copyright (c) 2017 Michael Hirsch, Ph.D." who modernized the code for contemporary systems; PyHC registry lists Michael Hirsch as contact.

### 7. Software Name (MANDATORY)
POLAN

**Source:** GitHub repository name, SoMEF extraction, PyHC registry

### 8. Description (MANDATORY)
POLAN is a classic Fortran program used to calculate real-height profiles from chirp ionosonde data from the ionosphere. The software performs polynomial analysis (POLynomial ANalysis) on sweep-frequency ionograms to determine the true height distribution of ionospheric electron density from virtual height measurements. Originally developed by J.E. Titheridge in the 1980s and documented in UAG-93 report, the code has been updated to compile on modern PCs. The program supports multiple analysis modes including overlapping polynomials and single-polynomial fits, handles both ordinary and extraordinary ray data, and includes sophisticated modeling of ionospheric valleys and Chapman layer peaks.

**Source:** Synthesized from README.md, README.1ST, GitHub description, and PyHC registry

### 9. Concise Description (OPTIONAL)
Titheridge's POLAN for estimating true ionosphere height from ionosonde measurements using polynomial analysis of sweep-frequency ionogram data.

**Source:** Derived from GitHub API description and README

### 10. Publication Date (RECOMMENDED)
2017-03-07

**Source:** First commit date from git history; corresponds to when the modernized version was first published on GitHub

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Repository is hosted on GitHub with no DOI/Zenodo integration found

### 12. Version (RECOMMENDED)
- **Version Number:** Not found
- **Version Date:** Not found
- **Version Description:** Not found
- **Version PID:** Not found

**Note:** No version tags found in git repository; no releases on GitHub; package does not appear to use semantic versioning

### 13. Programming Language (RECOMMENDED)
- Fortran77
- Fortran90
- Python 3.x

**Source:** SoMEF extraction and repository analysis. Primary language is Fortran (110,118 bytes) with Python wrapper/build code (2,029 bytes) and CMake build system (605 bytes). The Fortran code uses legacy syntax (-std=legacy flag in setup.py) indicating Fortran 77 compatibility.

### 14. Reference Publication (RECOMMENDED)
Not found

**Note:** The README.1ST references several publications by J.E. Titheridge describing the POLAN method and the UAG-93 report "Ionogram analysis with the generalised program POLAN", but none of these have DOIs. Key methodological reference: Titheridge, J.E. (1988). "The real height analysis of ionograms: A generalised formulation", Radio Science 23(5), 831-849.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT

**Source:** LICENSE file and SoMEF extraction (SPDX ID: MIT)

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- ionosphere
- ionogram
- ionosonde
- real-height analysis
- polynomial analysis
- ionospheric sounding
- electron density
- sweep-frequency

**Source:** SoMEF extraction ("ionosphere"), PyHC registry ("ionosphere_thermosphere_mesosphere"), and keywords derived from software description and functionality

### 17. Data Sources (OPTIONAL)
- Other

**Note:** POLAN processes ionosonde data from chirp ionosondes. These are ground-based instruments, not specifically listed data sources like CDAWeb or HAPI servers. Data is typically provided as input files rather than fetched from a specific server.

### 18. Input File Formats (RECOMMENDED)
- ascii

**Source:** Code analysis shows program reads ASCII text files (.dat format) with frequency and height data. Example files in examples/in.dat and examples/in.asc confirm ASCII format.

### 19. Output File Formats (RECOMMENDED)
- ascii

**Source:** Code analysis (polrun.f line 33) shows output written to 'out.dat' file in ASCII format. Example output files (out.dat, POLOUT.396) are ASCII text.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source:** CI configuration shows testing on Linux (ubuntu-latest). Fortran code is generally portable across platforms. The original README.1ST mentions compilation on IBM PC (DOS/Windows). Modern CMake build system supports cross-platform compilation.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Source:** Fortran code does not require specific CPU architecture; standard numerical computation

### 22. Related Phenomena (OPTIONAL)
Not found

**Note:** The software analyzes ionospheric structure but is a general-purpose ionogram analysis tool not specifically tied to particular phenomena like solar flares or CMEs.

### 23. Development Status (RECOMMENDED)
- Inactive

**Source:** Repository last updated 2024-06-24 (per SoMEF); has reached stable, usable state as a mature tool (originally from 1980s-1990s); appears to be maintained but not actively developed with new features. Code has not had recent commits focused on new functionality.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/POLAN/blob/main/README.1ST

**Source:** Primary documentation is in README.1ST file which contains detailed usage instructions. Full documentation available in UAG-93 report referenced at http://www.sws.bom.gov.au/IPSHosted/INAG/uag_93/uag_93.html (link reported as down in README)

### 25. Funder (OPTIONAL)
Not found

### 26. Award Title (OPTIONAL)
Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found - No DOIs available for related publications

**Note:** Several publications describe the POLAN methodology but lack DOIs:
- Titheridge, J.E. (1988). "The real height analysis of ionograms: A generalised formulation", Radio Science 23(5), 831-849.
- Titheridge, J.E. (1985). "Ionogram analysis: Least squares fitting of a Chapman-layer peak", Radio Sci., 20(2), 247-256.
- Titheridge, J.E. (1986). "Starting models for the real height analysis of ionograms", J. Atmos. Terr. Phys., 48(5), 435-446.
- Titheridge, J.E. (1982). "The stability of ionogram analysis techniques", J. Atmos. Terr. Phys., 44(8), 657-669.

### 28. Related Datasets (OPTIONAL)
Not found

**Note:** POLAN is a general analysis tool that can process ionosonde data from various instruments; no specific dataset DOIs are tied to the software

### 29. Related Software (OPTIONAL)
Not found

**Note:** The README mentions SPOLAN (a simplified version of POLAN) but this is included as source code within the same historical distribution, not a separate software package. No other related software dependencies or similar tools are identified.

### 30. Interoperable Software (OPTIONAL)
Not found

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** Ionosonde (general class of instruments)
- **Instrument Identifier:** Not found

**Note:** POLAN is designed to work with ionosonde data (sweep-frequency ionospheric sounders), particularly chirp ionosondes, but is not specific to a particular instrument or mission.

### 32. Related Observatories (OPTIONAL)
Not found

**Note:** POLAN is a general-purpose analysis tool not tied to specific observatories, though it could process data from any ionosonde installation

### 33. Logo (OPTIONAL)
Not found

---

## Metadata Sources Summary

This metadata was extracted using the following methods:

1. **SoMEF Analysis:** Automated extraction from repository (somef_output.json)
2. **PyHC Registry:** Found in projects_unevaluated.yml
3. **Manual Repository Examination:**
   - README.md and README.1ST
   - LICENSE file
   - setup.py and pyproject.toml
   - Source code analysis (src/*.f files)
   - GitHub CI configuration (.github/workflows/ci_unix.yml)
   - Git history
   - Example files (examples/ directory)

**Key Findings:**
- No DOI or persistent identifier exists for this software
- Original author (J.E. Titheridge) developed in 1980s-1990s; modernized by Michael Hirsch in 2017
- Classic ionospheric analysis tool with extensive documentation in UAG-93 report
- Primarily Fortran code with Python build infrastructure
- Listed in PyHC unevaluated packages registry
- Active in ionospheric research community but code development appears inactive
