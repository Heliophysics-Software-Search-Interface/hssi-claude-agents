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
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization:2D Graphics
- Data Visualization:Line Plots

**Source:** Manual code analysis - The software downloads ACE satellite magnetometer data from FTP, processes 16-second averaged magnetic field measurements, and creates time series plots of multiple magnetic field components (Br, Bt, Bn, Bx, By, Bz, Btotal, dBrms).

### 5. Related Region (MANDATORY)
- Interplanetary Space
- Earth Magnetosphere

**Source:** Domain knowledge - ACE satellite is positioned at the L1 Lagrange point between Earth and Sun, primarily observing the Interplanetary Magnetic Field (IMF) in interplanetary space. This IMF data is commonly used for Earth magnetosphere studies, as solar wind conditions measured at L1 affect the magnetosphere.

### 6. Authors (MANDATORY)
- **Authors:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** setup.cfg (line 4), PyHC unevaluated registry (contact: Michael Hirsch)

### 7. Software Name (MANDATORY)
ace_magnetometer

**Source:** setup.cfg (line 2), PyHC unevaluated registry (name: ACEmag), SoMEF (name: ACE_magnetometer)

**Note:** The package is named "ace_magnetometer" in the Python package metadata, "ACEmag" in the PyHC registry, and "ACE_magnetometer" as the GitHub repository name.

### 8. Description (MANDATORY)
Load and Plot ACE satellite magnetometer data

**Source:** setup.cfg (line 6), README.md (line 10), PyHC unevaluated registry, SoMEF

**Extended Description:** This Python package provides tools to download, load, and plot magnetometer data from the ACE (Advanced Composition Explorer) satellite. The software automatically retrieves 16-second averaged magnetic field data from the ACE mission's FTP server and provides visualization capabilities for analyzing the interplanetary magnetic field (IMF) components including Br, Bt, Bn, Bx, By, Bz, total field magnitude (Btotal), and RMS fluctuations (dBrms).

### 9. Concise Description (OPTIONAL)
Load and Plot ACE satellite magnetometer data

**Source:** README.md, setup.cfg - The existing description is already concise (under 200 characters).

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

**Source:** setup.cfg (Programming Language :: Python :: 3.6, 3.7, 3.8 on lines 16-18), SoMEF programming_languages

**Note:** Also contains MATLAB code (2564 bytes) according to SoMEF, but Python is the primary language (4018 bytes).

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
- magnetosphere
- ionosphere_thermosphere_mesosphere

**Source:** SoMEF (ace, geoscience, magnetometer, python, satellite-magnetometer from GitHub topics), setup.cfg (IMF, magnetic field, geospace), PyHC unevaluated registry (magnetosphere, ionosphere_thermosphere_mesosphere, specific)

### 17. Data Sources (OPTIONAL)
- FTP/FTPS Directories

**Source:** Manual code analysis - Downloads data from ftp://mussel.srl.caltech.edu/pub/ace/browse/MAG16sec/ (ace_magnetometer/__init__.py line 12)

### 18. Input File Formats (RECOMMENDED)
- ascii

**Source:** Manual code analysis - The software reads ASCII text files from within ZIP archives (ace_magnetometer/__init__.py lines 59-62, using pd.read_csv with whitespace separator)

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
- Active

**Source:** setup.cfg (Development Status :: 5 - Production/Stable on line 12), GitHub activity (last updated 2023-01-27 according to SoMEF)

**Note:** While the last update was in January 2023, the package is marked as "Production/Stable" in its classifiers, suggesting it reached a stable, usable state.

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
Not found - No related software explicitly referenced in repository

**Dependencies (from setup.cfg):**
- pandas
- numpy
- python-dateutil
- matplotlib (for plotting)
- seaborn (for plotting)

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
https://raw.githubusercontent.com/space-physics/ace_magnetometer/main/tests/timeplot.png

**Source:** SoMEF images - This is an example plot image, not an official logo. No official software logo was found.

**Note:** This is an example visualization output, not a dedicated logo for the software package.

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
- **Active but not recently updated:** The package is marked as Production/Stable but hasn't been updated since January 2023. This may indicate it has reached a stable state rather than being abandoned.
