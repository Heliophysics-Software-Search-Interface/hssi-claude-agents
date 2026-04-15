# HSSI Metadata Extraction Results

**Repository:** https://github.com/geospace-code/sciencedates
**Extraction Date:** 2025-12-04

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.598255
- **Source:** Concept DOI from Zenodo (covers all versions)

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/geospace-code/sciencedates
- **Source:** DataCite API and repository analysis

### 4. Software Functionality (MANDATORY)
- **Selected Values:**
  - Data Processing and Analysis
  - Data Processing and Analysis:Time Series Analysis
- **Source:** Analysis of code functionality - the library performs date/time conversions used in scientific applications, including datetime to year/day-of-year conversions, decimal year conversions, UTC seconds conversions, and local solar time calculations
- **Note:** This is a utility library for time/date conversions commonly needed in heliophysics data processing

### 5. Related Region (MANDATORY)
- **Selected Values:**
  - Solar Environment
  - Earth Magnetosphere
  - Earth Atmosphere
- **Source:** PyHC registry keywords (solar, magnetosphere, ionosphere_thermosphere_mesosphere)

### 6. Authors (MANDATORY)
- **Author 1:**
  - **Authors:** Michael Hirsch, Ph.D.
  - **Author Identifier:** Not found
  - **Affiliation:** Not found
- **Source:** setup.cfg, LICENSE.txt, DataCite API (note: DataCite only lists first name "Michael" with empty surname)

### 7. Software Name (MANDATORY)
- **Software Name:** sciencedates
- **Source:** setup.cfg, DataCite API, GitHub repository name

### 8. Description (MANDATORY)
- **Description:** Date & time conversions used in the sciences. The assumption is that datetimes are timezone-naive, as this is required in Numpy and other scientific libraries for numpy.datetime64. This library provides conversions between datetime objects and various scientific time formats including year/day-of-year (yyyyddd), decimal year, UTC seconds, and local solar time. It supports Python, with additional examples provided for Julia, Matlab/GNU Octave, and Fortran.
- **Source:** Combined from README.md, setup.cfg, and DataCite API

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Date conversions used in the sciences.
- **Source:** DataCite API description field (exactly 42 characters)

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2017-02-08
- **Source:** SoMEF (date_created from GitHub API)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API and Zenodo metadata

### 12. Version (RECOMMENDED)
- **Version Number:** v1.5.1
- **Version Date:** 2021-12-29
- **Version Description:** Python >= 3.7, update type anno
- **Version PID:** https://doi.org/10.5281/zenodo.5808426
- **Source:** DataCite API, Zenodo API, setup.cfg, GitHub releases, git tag

### 13. Programming Language (RECOMMENDED)
- **Selected Values:**
  - Python 3.x
  - Julia
  - Fortran77
  - MATLAB
- **Source:** SoMEF (programming_languages from GitHub API), repository file analysis (src/, julia/, fortran/, matlab/ directories), setup.cfg (Python >= 3.7)

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication:** Not found
- **Note:** No publication DOI found in repository files

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://api.github.com/licenses/mit
- **Source:** LICENSE.txt, SoMEF (GitHub API), SPDX ID: MIT

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Keywords:**
  - time
  - calendar
  - date-conversion
  - fortran
  - geoscience
  - julia
  - matlab
  - python
  - solar
  - magnetosphere
  - ionosphere_thermosphere_mesosphere
- **Source:** setup.cfg, SoMEF (GitHub topics), PyHC registry

### 17. Data Sources (OPTIONAL)
- **Data Sources:** Not found
- **Note:** This is a utility library for date/time conversions, not designed to read from specific data sources

### 18. Input File Formats (RECOMMENDED)
- **Input File Formats:** Not applicable
- **Note:** Library works with datetime objects and numeric formats, not file I/O

### 19. Output File Formats (RECOMMENDED)
- **Output File Formats:** Not applicable
- **Note:** Library works with datetime objects and numeric formats, not file I/O

### 20. Operating System (RECOMMENDED)
- **Selected Values:**
  - Operating System Independent
  - Linux
  - Mac
  - Windows
- **Source:** setup.cfg (OS Independent), CI configuration shows testing on ubuntu-latest, windows-latest, macos-latest

### 21. CPU Architecture (RECOMMENDED)
- **Selected Values:**
  - CPU Independent
- **Source:** Inferred from Operating System Independent classification and pure Python implementation

### 22. Related Phenomena (OPTIONAL)
- **Related Phenomena:** Not found
- **Note:** As a general-purpose date/time conversion utility, not specific to particular phenomena

### 23. Development Status (RECOMMENDED)
- **Development Status:** Active
- **Source:** setup.cfg classifier "Development Status :: 5 - Production/Stable", recent repository activity (last updated 2025-04-17 per SoMEF)

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/geospace-code/sciencedates
- **Source:** No separate documentation site found; README.md in repository serves as documentation

### 25. Funder (OPTIONAL)
- **Funder:** Not found
- **Note:** No funding information in DataCite metadata or repository files

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Note:** No award information in DataCite metadata or repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Related Publications:** Not found
- **Note:** No publications found in DataCite relatedIdentifiers

### 28. Related Datasets (OPTIONAL)
- **Related Datasets:** Not found
- **Note:** No datasets found in DataCite relatedIdentifiers

### 29. Related Software (OPTIONAL)
- **Related Software:**
  - numpy (dependency)
  - python-dateutil (dependency)
- **Source:** setup.cfg install_requires
- **Note:** These are required dependencies listed in the package metadata

### 30. Interoperable Software (OPTIONAL)
- **Interoperable Software:**
  - numpy
  - pytz (optional)
  - xarray (optional)
  - matplotlib (optional)
- **Source:** setup.cfg (install_requires and extras_require)

### 31. Related Instruments (OPTIONAL)
- **Related Instruments:** Not found
- **Note:** General-purpose utility library not specific to particular instruments

### 32. Related Observatories (OPTIONAL)
- **Related Observatories:** Not found
- **Note:** General-purpose utility library not specific to particular observatories/missions

### 33. Logo (OPTIONAL)
- **Logo:** Not found
- **Note:** No logo found in repository or PyHC registry

---

## Metadata Sources Summary

This metadata was extracted using the following sources in order of priority:

1. **PyHC Registry (Unevaluated):** Package found in projects_unevaluated.yml with keywords: solar, magnetosphere, ionosphere_thermosphere_mesosphere, specific
2. **DataCite API:** Queried https://api.datacite.org/dois/10.5281/zenodo.598255
3. **Zenodo API:** Queried https://zenodo.org/api/records/5808426
4. **SoMEF:** Automated metadata extraction from repository (somef_output.json)
5. **Manual Repository Examination:**
   - README.md
   - LICENSE.txt
   - setup.cfg (primary source for package metadata)
   - setup.py
   - pyproject.toml
   - .github/workflows/ci.yml
   - Source code analysis (src/sciencedates/)
   - Git tags and release history

---

## Verification Notes

### Correctness
- All URLs verified to be accessible
- DOI formatted correctly and resolves properly
- Author name extracted from multiple sources (setup.cfg, LICENSE.txt)
- Version date verified from git tag (2021-12-29 for v1.5.1)

### Software Functionality Analysis
The software provides the following date/time conversion capabilities:
- `datetime2yeardoy()` - Convert datetime to year/day-of-year format (yyyyddd)
- `yeardoy2datetime()` - Convert year/day-of-year to datetime
- `datetime2yeardec()` - Convert datetime to decimal year
- `yeardec2datetime()` - Convert decimal year to datetime
- `datetime2utsec()` - Convert datetime to UTC seconds since midnight
- `datetime2gtd()` - Convert datetime to day-of-year, UTC seconds, and local solar time
- `date2doy()` - Extract day of year from date
- Additional utilities: `find_nearest()`, `randomdate()`, `forceutc()`

These functions are classified as "Data Processing and Analysis:Time Series Analysis" because they process temporal data.

### Related Region Analysis
Based on PyHC registry keywords and the general applicability of time conversion utilities in heliophysics:
- **Solar Environment**: Used for solar observations and data processing
- **Earth Magnetosphere**: Used for magnetospheric data analysis
- **Earth Atmosphere**: Used for ionosphere/thermosphere/mesosphere research

### Completeness
- All 33 form fields have been addressed
- MANDATORY fields all have values
- Most RECOMMENDED fields have values (except Reference Publication, Funder, Award Title)
- Multi-language support documented (Python, Julia, Fortran, MATLAB)

---

## Final Notes

**PyHC Package Status:** This package is listed in the PyHC unevaluated registry, indicating it is a recognized tool in the heliophysics Python community but has not yet undergone full PyHC standards evaluation.

**Primary Contact:** Michael Hirsch (per PyHC registry)

**GitHub Statistics (from SoMEF):**
- Stars: 6
- Forks: 4
- Last updated: 2025-04-17

**Dependencies:**
- Required: numpy, python-dateutil
- Optional: pytz (timezone support), xarray and matplotlib (plotting), pytest (testing), flake8 and mypy (linting)
