# HSSI Metadata Extraction Results

**Repository:** https://github.com/aburrell/apexpy
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Concept DOI:** https://doi.org/10.5281/zenodo.1214206
- **Source:** Zenodo API, .zenodo.json file, README badge

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/aburrell/apexpy
- **Source:** GitHub, DataCite API, PyHC registry

### 4. Software Functionality (MANDATORY)
- **Coordinate Transforms**
- **Coordinate Transforms:Ionospheric**
- **Coordinate Transforms:Magnetospheric**
- **Data Processing and Analysis**
- **Data Processing and Analysis:Analysis**
- **Data Processing and Analysis:Field-line Tracing**
- **Models and Simulations:Empirical**
- **Models and Simulations:Field-line Tracing**

**Notes:** ApexPy performs coordinate transformations between geodetic (WGS84), modified apex, and quasi-dipole coordinate systems. It also calculates magnetic local time (MLT), base vectors, and performs field-line tracing. These are fundamental operations for ionospheric and magnetospheric research.

**Source:** Code analysis, README description, PyHC keywords

### 5. Related Region (MANDATORY)
- **Earth Atmosphere** (specifically the ionosphere/thermosphere/mesosphere)
- **Earth Magnetosphere**

**Notes:** The software works with magnetic apex coordinates and quasi-dipole coordinates, which are coordinate systems specifically designed for ionospheric and magnetospheric studies. The PyHC keywords list "ionosphere_thermosphere_mesosphere" as the primary region.

**Source:** PyHC registry, scientific context from README references

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Christer van der Meeren
- **Author Identifier:** https://orcid.org/0000-0002-8043-0953
- **Affiliation:** Not found

**Author 2:**
- **Name:** Karl M. Laundal
- **Author Identifier:** https://orcid.org/0000-0001-5028-4943
- **Affiliation:** Not found

**Author 3:**
- **Name:** Angeline G. Burrell
- **Author Identifier:** https://orcid.org/0000-0001-8875-9326
- **Affiliation:** Naval Research Laboratory

**Author 4:**
- **Name:** Leslie L. Lamarche
- **Author Identifier:** https://orcid.org/0000-0001-7098-0524
- **Affiliation:** Not found

**Author 5:**
- **Name:** Gregory Starr
- **Author Identifier:** https://orcid.org/0000-0002-3487-3630
- **Affiliation:** Not found

**Author 6:**
- **Name:** Ashton S. Reimer
- **Author Identifier:** https://orcid.org/0000-0002-4621-3453
- **Affiliation:** Not found

**Author 7:**
- **Name:** Achim Morschhauser
- **Author Identifier:** https://orcid.org/0000-0001-7955-4441
- **Affiliation:** GFZ German Research Centre for Geosciences

**Author 8:**
- **Name:** Ingo Michaelis
- **Author Identifier:** https://orcid.org/0000-0001-9741-4063
- **Affiliation:** GFZ German Research Centre for Geosciences

**Author 9:**
- **Name:** Jeff Klenzing
- **Author Identifier:** https://orcid.org/0000-0001-8321-6074
- **Affiliation:** Goddard Space Flight Center

**Source:** DataCite API, Zenodo API, .zenodo.json

### 7. Software Name (MANDATORY)
- **Name:** apexpy
- **Full Name:** aburrell/apexpy: ApexPy

**Source:** GitHub repository, DataCite API, PyHC registry

### 8. Description (MANDATORY)
This is a Python wrapper for the Apex fortran library by Emmert et al. (2010), which allows converting between geodetic, modified apex, and quasi-dipole coordinates as well as getting modified apex and quasi-dipole base vectors (Richmond 1995). The geodetic system used here is WGS84. MLT calculations are also included. The package uses IGRF-14 magnetic field coefficients (1900-2030) and provides tools essential for ionospheric and magnetospheric research. The software is free and open source under the MIT license.

**Source:** README, DataCite API, PyHC registry

### 9. Concise Description (OPTIONAL)
A Python wrapper for converting between geodetic, modified apex, and quasi-dipole coordinates, with magnetic local time calculations.

**Source:** Derived from full description

### 10. Publication Date (RECOMMENDED)
- **Date:** 2015-11-18
- **Source:** GitHub API (repository creation date), SoMEF

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

**Latest Version:**
- **Version Number:** v2.1.0
- **Version Date:** 2025-01-07
- **Version Description:** This is a major release that updates the magnetic coefficients to IGRF-14. It also updates the code to be compliant with Numpy 2.0, Python 3.12, and changes made to datetime. A bug that made the command line executable unavailable was fixed.
- **Version PID:** https://doi.org/10.5281/zenodo.14610316

**Previous Versions:** v2.0.2 (2024-11-12), v2.0.1 (2023-04-11), v2.0.0 (2022-12-09), v1.1.0 (2021-03-05), 1.0.3 (2018-04-06), v1.0.2 (2018-02-28)

**Source:** DataCite API, Zenodo API, GitHub releases, git tags, SoMEF

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (specifically Python 3.9, 3.10, 3.11, 3.12)
- **Fortran 2003** / **Fortran90** (underlying computational library)
- **C** (build components)

**Source:** GitHub API (language statistics), pyproject.toml classifiers, GitHub Actions CI configuration

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.1029/2010JA015326
- **Citation:** Emmert, J. T., A. D. Richmond, and D. P. Drob (2010), A computationally compact representation of Magnetic-Apex and Quasi-Dipole coordinates with smooth base vectors, J. Geophys. Res., 115(A8), A08322, doi:10.1029/2010JA015326.
- **Additional Reference:** Richmond, A. D. (1995), Ionospheric Electrodynamics Using Magnetic Apex Coordinates, Journal of geomagnetism and geoelectricity, 47(2), 191–212, doi:10.5636/jgg.47.191.

**Source:** README, .zenodo.json references, Zenodo notes field

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT
- **SPDX Identifier:** MIT

**Source:** LICENSE file, DataCite API, GitHub API, SoMEF, pyproject.toml

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- apex
- modified apex
- quasi-dipole
- quasi dipole
- coordinates
- magnetic coordinates
- mlt
- magnetic local time
- conversion
- converting
- Magnetic Apex Coordinates
- Quasi Dipole Coordinates
- MLT
- Magnetic Local Time
- Conversion
- Coordinate Conversion
- Converting
- Ionosphere
- Magnetic Field
- Space Physics
- Heliophysics
- ionosphere_thermosphere_mesosphere (PyHC keyword)

**Source:** pyproject.toml, .zenodo.json, Zenodo API, DataCite API, PyHC registry

### 17. Data Sources (OPTIONAL)
Not found - The software uses internal data files (apexsh.dat, igrf14coeffs.txt) for magnetic field coefficients rather than external data sources.

**Source:** Code analysis

### 18. Input File Formats (RECOMMENDED)
Not applicable - The software primarily accepts numerical coordinate inputs (latitude, longitude, altitude) programmatically rather than reading data files. It does use internal coefficient files in custom formats.

**Source:** Code analysis, documentation

### 19. Output File Formats (RECOMMENDED)
Not applicable - The software primarily returns numerical coordinate outputs programmatically rather than writing to files.

**Source:** Code analysis, documentation

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**

**Source:** GitHub Actions CI configuration (.github/workflows/main.yml), pyproject.toml classifiers

### 21. CPU Architecture (RECOMMENDED)
- **x86-64** (tested on ubuntu-latest, windows-latest in CI)
- **Apple Silicon arm64** (tested on macos-latest in CI)
- **CPU Independent** (Python code is architecture-independent, though compiled Fortran components are architecture-specific)

**Source:** GitHub Actions CI configuration, general Python/Fortran compilation practices

### 22. Related Phenomena (OPTIONAL)
Not found in structured form. The software is used for studying ionospheric and magnetospheric phenomena but specific phenomena are not enumerated.

**Source:** Scientific context suggests usage for auroral, ionospheric current, and magnetic field studies

### 23. Development Status (RECOMMENDED)
- **Active**

**Notes:** The software shows consistent development activity with the latest release in January 2025. PyHC ratings show all categories as "Good," indicating active maintenance. The pyproject.toml classifies it as "Development Status :: 5 - Production/Stable".

**Source:** GitHub commit activity, release history, PyHC quality ratings, pyproject.toml classifiers

### 24. Documentation (RECOMMENDED)
- **URL:** https://apexpy.readthedocs.io/en/latest/
- **Installation Guide:** https://apexpy.readthedocs.io/en/latest/installation.html

**Source:** README, pyproject.toml, PyHC registry, SoMEF

### 25. Funder (OPTIONAL)
Not found

**Source:** DataCite API returned no funding references

### 26. Award Title (OPTIONAL)
Not found

**Source:** DataCite API returned no funding references

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found beyond the reference publication

**Source:** DataCite API

### 28. Related Datasets (OPTIONAL)
Not found

**Source:** DataCite API, code analysis

### 29. Related Software (RECOMMENDED)
- **AACGMV2** (https://github.com/aburrell/aacgmv2) - Another coordinate transformation package by the same maintainer, for AACGM coordinates
- **SpacePy** - PyHC core package that includes coordinate transformations and magnetic field models
- **pysat** - PyHC core package with coordinate transformation capabilities

**Notes:** These packages provide complementary or alternative coordinate transformation capabilities for space physics research.

**Source:** PyHC registry (packages by same author/maintainer), scientific domain knowledge

### 30. Interoperable Software (OPTIONAL)
- **NumPy** - Core dependency, fully interoperable
- **pysat** - Listed in PyHC core packages with coordinate functionality
- **SpacePy** - Listed in PyHC core packages with coordinate functionality

**Notes:** As a PyHC community package, apexpy is designed to interoperate with the PyHC ecosystem.

**Source:** pyproject.toml dependencies, PyHC ecosystem

### 31. Related Instruments (OPTIONAL)
Not found - The software is instrument-agnostic, providing coordinate transformations applicable to data from any ionospheric or magnetospheric instrument.

**Source:** Code analysis, documentation

### 32. Related Observatories (OPTIONAL)
Not found - The software is observatory-agnostic, providing coordinate transformations applicable to any location-based observations.

**Source:** Code analysis, documentation

### 33. Logo (OPTIONAL)
- **URL:** https://github.com/aburrell/apexpy/blob/main/docs/apexpy.png?raw=true

**Notes:** Yellow magnetic field lines surrounding the Earth's surface, which is blue

**Source:** README.rst, repository docs folder

---

## Metadata Extraction Summary

### Sources Used:
1. **DataCite API** - DOI metadata for version 2.1.0 (concept DOI)
2. **Zenodo API** - Detailed version metadata, keywords, authors with ORCIDs
3. **SoMEF** - Repository analysis for programming languages, dates, releases
4. **PyHC Registry** - Community package metadata, quality ratings, contact information
5. **Manual Repository Examination:**
   - README.rst - Description, usage examples, references
   - LICENSE - MIT license confirmation
   - pyproject.toml - Package metadata, dependencies, classifiers
   - .zenodo.json - Author information, keywords, license, references
   - .github/workflows/main.yml - OS and Python version support
   - apexpy/apex.py - Code functionality analysis
   - Git history - Version information

### Metadata Completeness:
- **MANDATORY fields:** All filled ✓
- **RECOMMENDED fields:** 11 of 11 filled ✓
- **OPTIONAL fields:** 5 of 11 filled

### Notes:
- The software is well-documented with comprehensive metadata available through multiple sources
- PyHC community package status indicates high quality and community trust
- All authors have ORCIDs, facilitating proper attribution
- Active development with recent major release (January 2025)
- Strong testing infrastructure across multiple OS platforms
- Clear licensing (MIT) and citation requirements
