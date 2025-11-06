# HSSI Metadata Extraction Results

**Repository:** https://github.com/aburrell/ocbpy
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.1179230
- **Source:** Provided by user; confirmed in DataCite API and repository README badge

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/aburrell/ocbpy
- **Source:** Provided by user; confirmed in all sources

### 4. Software Functionality (MANDATORY)
- **Values:**
  - Coordinate Transforms
  - Coordinate Transforms:Ionospheric
  - Coordinate Transforms:Magnetospheric
  - Data Processing and Analysis
  - Data Processing and Analysis:Data Access and Retrieval
- **Source:** Analysis of README, code structure, and package description. The software converts between AACGM magnetic coordinates and adaptive polar boundary coordinate systems (OCB/EAB), which is a specific type of ionospheric/magnetospheric coordinate transformation. It also processes boundary data from multiple sources (IMAGE, AMPERE, DMSP).

### 5. Related Region (MANDATORY)
- **Values:**
  - Earth Atmosphere
  - Earth Magnetosphere
- **Source:** Analysis of software purpose. The software operates at the interface between the magnetosphere and ionosphere, dealing with the open-closed field line boundary (magnetosphere) and polar cap/auroral oval regions (upper atmosphere/ionosphere).

### 6. Authors (MANDATORY)
- **Author 1:**
  - **Name:** Angeline G. Burrell
  - **Author Identifier:** https://orcid.org/0000-0001-8875-9326
  - **Affiliation:**
    - **Organization:** Naval Research Laboratory
    - **Affiliation Identifier:** Not found
  - **Source:** DataCite API
- **Author 2:**
  - **Name:** Gareth Chisham
  - **Author Identifier:** https://orcid.org/0000-0003-1151-5934
  - **Affiliation:**
    - **Organization:** British Antarctic Survey
    - **Affiliation Identifier:** Not found
  - **Source:** DataCite API
- **Author 3:**
  - **Name:** Jone Reistad
  - **Author Identifier:** https://orcid.org/0000-0003-3509-5479
  - **Affiliation:**
    - **Organization:** Birkeland Centre for Space Science
    - **Affiliation Identifier:** Not found
  - **Source:** DataCite API

### 7. Software Name (MANDATORY)
- **Value:** OCBpy
- **Source:** PyHC registry, GitHub API, pyproject.toml

### 8. Description (MANDATORY)
- **Value:** OCBpy is a Python module that converts between AACGM coordinates and a magnetic coordinate system that adjusts latitude and local time relative to the Open Closed field line Boundary (OCB), Equatorial Auroral Boundary (EAB), or both. This is particulary useful for statistical studies of the poles, where gridding relative to a fixed magnetic coordinate system would cause averaging of different physical regions, such as auroral and polar cap measurements. The coordinate system methodology is described in Chisham (2017). Boundaries must be obtained from observations or models for this coordinate transformation. Several boundary data sets are included within this package, including northern hemisphere boundaries from the IMAGE satellite, northern and southern hemisphere OCBs from AMPERE, and single-point boundary locations from DMSP.
- **Source:** Combined from README.md and PyHC registry

### 9. Concise Description (OPTIONAL)
- **Value:** A Python module that converts between AACGM coordinates and an adjustable magnetic coordinate system based on the location of the polar cap boundary.
- **Source:** PyHC registry description

### 10. Publication Date (RECOMMENDED)
- **Value:** 2018-02-19
- **Source:** SoMEF date_created from GitHub API (first release date)

### 11. Publisher (RECOMMENDED)
- **Publisher:**
  - **Organization:** Zenodo
  - **Publisher Identifier:** https://zenodo.org
  - **Source:** DataCite API

### 12. Version (RECOMMENDED)
- **Version Number:** 0.6.0
- **Version Date:** 2025-08-11
- **Version Description:** This release introduces the ability to define boundaries based on a mathematical model. The Starkov (1994) model is added to practically enable this new ability. Also: Added more AMPERE boundaries (2022-2024); Added a to_dict method to the boundary classes; Adapted the code to use the newest version of zenodo_get.
- **Version PID:** https://doi.org/10.5281/zenodo.16802585
- **Source:** DataCite API, GitHub releases, git tag date

### 13. Programming Language (RECOMMENDED)
- **Values:**
  - Python 3.x
- **Source:** GitHub API, pyproject.toml specifies Python 3.10-3.13

### 14. Reference Publication (RECOMMENDED)
- **Value:** https://doi.org/10.1002/2016JA023235
- **Source:** README.md (Chisham, G. (2017), A new methodology for the development of high‐latitude ionospheric climatologies and empirical models, Journal of Geophysical Research: Space Physics)

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause
- **Source:** GitHub API and LICENSE file. Note: DataCite API incorrectly lists "BSD 1-Clause" but the actual LICENSE file in the repository is BSD 3-Clause.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Values:**
  - magnetic coordinates
  - coordinate-transformation
  - coordinate-systems
  - space
  - space-physics
  - ionosphere
  - magnetosphere
  - coordinates
  - field-line boundary
  - auroral oval
  - polar cap
  - pysat
  - atmosphere
  - thermosphere
  - heliosphere
  - observations
  - models
  - satellites
  - analysis
  - Conversion
  - Coordinate Conversion
  - Converting
  - Magnetic Field
  - Space Physics
  - Heliophysics
- **Source:** Combined from DataCite API, SoMEF (GitHub topics), and pyproject.toml

### 17. Data Sources (OPTIONAL)
- **Values:**
  - Observatory/Mission-specific
  - Other
- **Source:** Analysis of README and instruments module. The software supports SuperMAG, SuperDARN Vorticity, and pysat instruments. Boundary data comes from IMAGE, AMPERE, and DMSP missions.

### 18. Input File Formats (RECOMMENDED)
- **Values:**
  - ascii
  - Other
- **Source:** Analysis of code structure. The software reads custom OCB boundary files and various mission-specific formats through pysat.

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - Not found
- **Note:** The software appears to primarily return transformed coordinates programmatically rather than writing output files.

### 20. Operating System (RECOMMENDED)
- **Values:**
  - Linux
  - Mac
  - Windows
- **Source:** CI workflow file (.github/workflows/main.yml) tests on ubuntu-latest, macos-latest, and windows-latest; pyproject.toml classifiers confirm Unix, POSIX, Linux, MacOS X, and Microsoft Windows

### 21. CPU Architecture (RECOMMENDED)
- **Values:**
  - CPU Independent
- **Source:** Python package with no specific CPU architecture requirements

### 22. Related Phenomena (OPTIONAL)
- **Values:**
  - Not found in standard vocabularies
- **Note:** The software deals with polar cap boundaries, auroral oval, and open-closed field line boundaries, but these specific phenomena are not in the provided controlled vocabulary list.

### 23. Development Status (RECOMMENDED)
- **Value:** Active
- **Source:** PyHC registry shows all quality metrics as "Good"; pyproject.toml classifier indicates "Development Status :: 5 - Production/Stable"; recent commits and releases (v0.6.0 released 2025-08-11)

### 24. Documentation (RECOMMENDED)
- **Value:** https://ocbpy.readthedocs.io/en/latest/
- **Source:** PyHC registry, pyproject.toml, README.md

### 25. Funder (OPTIONAL)
- **Value:** Not found
- **Source:** No funding information in DataCite API or repository files

### 26. Award Title (OPTIONAL)
- **Value:** Not found
- **Source:** No award information in DataCite API or repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Value:** https://doi.org/10.5194/angeo-38-481-2020
- **Note:** Burrell, A. G. et al. (2020): AMPERE Polar Cap Boundaries, Ann. Geophys., 38, 481-490
- **Source:** README.md

### 28. Related Datasets (OPTIONAL)
- **Values:**
  - IMAGE Auroral Boundary data: https://www.bas.ac.uk/project/image-auroral-boundary-data/
  - DMSP SSJ Boundaries: https://doi.org/10.5281/zenodo.3373812
- **Source:** README.md

### 29. Related Software (OPTIONAL)
- **Values:**
  - aacgmv2 (required dependency)
  - pysat (optional dependency for instrument support)
- **Source:** README.md dependencies section, pyproject.toml

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - pysat: https://github.com/pysat/pysat
- **Source:** The software includes pysat instrument integration modules and is designed to work within the pysat ecosystem

### 31. Related Instruments (OPTIONAL)
- **Values:**
  - IMAGE FUV
  - DMSP SSJ
  - AMPERE
  - SuperMAG
  - SuperDARN
- **Source:** README.md and analysis of instruments module

### 32. Related Observatories (OPTIONAL)
- **Values:**
  - IMAGE
  - DMSP
- **Source:** README.md

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/aburrell/ocbpy/main/docs/figures/ocbpy_logo.gif
- **Source:** PyHC registry, README.md, SoMEF output

---

## Metadata Source Priority

The following sources were used in priority order:
1. **PyHC Community Registry** - Manually curated, most trustworthy for this package
2. **DataCite API** - Official DOI metadata
3. **Repository files** (README.md, pyproject.toml, LICENSE) - Direct from source
4. **GitHub API / SoMEF** - Automated extraction
5. **Manual code analysis** - For functionality and technical details

---

## Notes

- The DOI 10.5281/zenodo.1179230 is the concept DOI representing all versions
- The latest version (0.6.0) has DOI 10.5281/zenodo.16802585
- The software is a well-maintained PyHC community package with "Good" ratings across all quality metrics
- Primary author/maintainer: Angeline G. Burrell (angeline.g.burrell.civ@us.navy.mil)
- The software specifically addresses the challenge of creating statistics in polar regions by using an adaptive coordinate system that adjusts based on actual boundary locations rather than fixed magnetic coordinates
- CI/CD testing confirms cross-platform compatibility (Linux, macOS, Windows) for Python 3.10-3.13
