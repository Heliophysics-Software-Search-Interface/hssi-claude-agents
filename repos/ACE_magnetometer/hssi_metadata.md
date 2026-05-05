# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/ACE_magnetometer
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found - No DOI found in repository files (CITATION.cff, README.md, .zenodo.json, or codemeta.json)

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/ACE_magnetometer

**Source:** PyHC unevaluated registry, GitHub API, setup.cfg

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Processing
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots

**Source:** Manual code analysis - The software downloads ACE satellite magnetometer data from an FTP archive, loads 16-second averaged magnetic field measurements, and creates multi-panel line plots of magnetic field components (Br, Bt, Bn, Bx, By, Bz, Btotal, dBrms) in both Python and MATLAB workflows.

### 5. Related Region (MANDATORY)
- Interplanetary Space

**Source:** README.md, source code, and mission context - The package downloads and plots ACE magnetometer data from the ACE archive. ACE measures the interplanetary magnetic field from the L1 region, so the directly supported science region is Interplanetary Space.

### 6. Authors (MANDATORY)
- **Authors:** Michael Hirsch
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** setup.cfg (line 4), PyHC unevaluated registry (contact: Michael Hirsch)

### 7. Software Name (MANDATORY)
ACEmag

**Source:** PyHC unevaluated registry (official software name: ACEmag), setup.cfg (package name: ace_magnetometer), GitHub repository name (ACE_magnetometer), SoMEF

**Note:** The package is named "ace_magnetometer" in the Python package metadata and "ACE_magnetometer" in the GitHub repository, but the authoritative software name for HSSI entry purposes is the PyHC registry name "ACEmag".

### 8. Description (MANDATORY)
ACE_magnetometer provides Python and MATLAB tools for working with 16-second ACE satellite magnetometer data. The Python workflow downloads and loads ACE archive files, while the MATLAB workflow reads local ACE HDF files and plots IMF components including Br, Bt, Bn, Bx, By, Bz, Btotal, and dBrms.

**Source:** setup.cfg (line 6), README.md, ace_magnetometer/__init__.py, PlotACE.py, matlab/PlotACE.m

**Extended Description:** This Python package provides tools to download, load, and plot magnetometer data from the ACE (Advanced Composition Explorer) satellite. The software automatically retrieves 16-second averaged magnetic field data from the ACE mission's FTP server and provides visualization capabilities for analyzing the interplanetary magnetic field (IMF) components including Br, Bt, Bn, Bx, By, Bz, total field magnitude (Btotal), and RMS fluctuations (dBrms).

### 9. Concise Description (OPTIONAL)
Python and MATLAB tools to retrieve, load, and plot 16-second ACE magnetometer data from the ACE archive.

**Source:** Derived from README.md, setup.cfg, and the implemented Python and MATLAB workflows.

### 10. Publication Date (RECOMMENDED)
2017-03-14

**Source:** Git history - First commit date, SoMEF (date_created: 2017-03-14T21:03:44Z)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Inferred from repository hosting platform (no DOI exists, so GitHub is the publisher)

### 12. Version (RECOMMENDED)
- **Version Number:** v0.9.0
- **Version Date:** 2018-07-25
- **Version Description:** Uses zip files with ascii data inside
- **Version PID:** Not found

**Source:** setup.cfg (version: 0.9.0), Git tags (v0.9.0 tag dated 2018-07-24 22:52:35 -0400), SoMEF releases data, GitHub release notes

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- MATLAB

**Source:** setup.cfg (Programming Language :: Python :: 3.6, 3.7, 3.8 on lines 16-18), SoMEF programming_languages, matlab/PlotACE.m, matlab/loadACEhdf.m

### 14. Reference Publication (RECOMMENDED)
Not found - No reference publication DOI found in repository files

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html

**Source:** LICENSE.txt (MIT License, Copyright (c) 2017 Michael Hirsch, Ph.D.), SoMEF (spdx_id: MIT)

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- ace
- geoscience
- magnetometer
- python
- satellite-magnetometer
- IMF
- magnetic field
- geospace

**Source:** SoMEF (ace, geoscience, magnetometer, python, satellite-magnetometer from GitHub topics), setup.cfg (IMF, magnetic field, geospace)

### 17. Data Sources (OPTIONAL)
- FTP/FTPS Directories
- Observatory/Mission-specific

**Source:** Manual code analysis - Downloads ACE mission data from ftp://mussel.srl.caltech.edu/pub/ace/browse/MAG16sec/ (ace_magnetometer/__init__.py line 12), which is both an FTP source and an observatory-specific archive.

### 18. Input File Formats (RECOMMENDED)
- ascii
- Other

**Source:** Manual code analysis - The Python workflow reads ASCII text files from within ZIP archives (ace_magnetometer/__init__.py lines 59-62, using pd.read_csv with whitespace separator). The MATLAB workflow reads ACE `.HDF` files with hdfinfo/hdfread (matlab/PlotACE.m, matlab/loadACEhdf.m), so `Other` is included for that mission-specific HDF input path.

### 19. Output File Formats (RECOMMENDED)
Not found - The software produces interactive matplotlib plots displayed to screen, not saved to file by default

**Note:** While the software could save plots in various formats supported by matplotlib (PNG, PDF, SVG, etc.), there is no explicit output file generation in the codebase.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows
- Operating System Independent

**Source:** setup.cfg (Operating System :: OS Independent on line 15), CI workflow (.github/workflows/ci.yml tests on ubuntu-latest, windows-latest, and macos-latest)

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Source:** Inferred - Python package with no compiled extensions or architecture-specific requirements

### 22. Related Phenomena (OPTIONAL)
Not found - No specific phenomena keywords found in repository

**Note:** The software measures the Interplanetary Magnetic Field (IMF), which is related to solar wind phenomena and space weather, but specific phenomena are not explicitly listed.

### 23. Development Status (RECOMMENDED)
- Inactive

**Source:** setup.cfg (Development Status :: 5 - Production/Stable on line 12), git history (latest upstream commit on main: 2021-04-27), SoMEF date_updated (2023-01-27)

**Note:** The package appears stable and usable, but the available repository evidence does not show ongoing active development.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/ACE_magnetometer/blob/main/README.md

**Source:** README.md in repository - No separate documentation site exists; documentation is in the README

### 25. Funder (OPTIONAL)
Not found - No funding information in repository files

### 26. Award Title (OPTIONAL)
Not found - No award information in repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found - No related publications found in repository files

### 28. Related Datasets (OPTIONAL)
Not found - No related dataset DOIs found in repository files

**Note:** The software works with ACE magnetometer data from the ACE mission archive, but no specific dataset DOI is referenced.

### 29. Related Software (OPTIONAL)
Not found - No related software with repository links or persistent identifiers is documented in the repository metadata

### 30. Interoperable Software (OPTIONAL)
Not found - No explicit interoperability with other software packages documented

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** ACE Magnetometer (MAG)
- **Instrument Identifier:** Not found

**Source:** Manual analysis - The software is specifically designed for the Magnetometer (MAG) instrument on the ACE spacecraft

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** ACE (Advanced Composition Explorer)

**Source:** Manual analysis - The software is designed for data from the ACE satellite mission

**Mission Details:** ACE is a NASA space exploration mission positioned at the L1 Lagrange point (approximately 1.5 million km from Earth toward the Sun) to observe solar wind and cosmic rays. The mission was launched in 1997 and continues to provide real-time space weather data.

### 33. Logo (OPTIONAL)
Not found - No official software logo was found in the repository or linked metadata

---

## Metadata Sources Summary

This metadata was extracted from the following sources:

1. **PyHC Unevaluated Registry** - Package listing with basic metadata
2. **SoMEF (Software Metadata Extraction Framework)** - Automated extraction from GitHub repository
3. **Repository Files:**
   - setup.cfg - Package metadata and configuration
   - setup.py - Build configuration
   - LICENSE.txt - License information
   - README.md - Project description and usage
   - pyproject.toml - Build system requirements
4. **Source Code Analysis:**
   - ace_magnetometer/__init__.py - Main package implementation
   - DownloadACE.py - Download script
   - PlotACE.py - Plotting script
5. **GitHub Repository:**
   - .github/workflows/ci.yml - CI/CD configuration showing OS support
   - Git history - Version and date information
   - GitHub API data via SoMEF

---

## Notes

- **No DOI:** This package does not have a DOI. Consider creating one through Zenodo for better citability.
- **Limited Documentation:** Documentation is minimal and contained only in README. Consider creating comprehensive documentation using ReadTheDocs or similar.
- **No CITATION.cff:** Consider adding a CITATION.cff file to specify how the software should be cited.
- **Author Information Incomplete:** No ORCID or affiliation information available for the author.
- **Development status:** The package appears stable, but the available repository evidence does not indicate ongoing active development.
