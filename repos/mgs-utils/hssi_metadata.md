# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/mgs-radio
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.595431
**Source:** DataCite API, Zenodo concept DOI
**Note:** This is the concept DOI that represents all versions of the software

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/mgs-radio
**Source:** SoMEF, PyHC registry, setup.cfg
**Note:** Repository was previously at https://github.com/scivision/mgs-utils but has been moved to the space-physics organization

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Processing
- Data Visualization:2D Graphics
- Data Visualization:Spectrogram
- Mission-related:Analysis
- Mission-related:Science Data Processing

**Source:** Code analysis, README
**Reasoning:**
- **Data Access and Retrieval:** Reads Mars Global Surveyor radio occultation data files (.sri, .lbl, .srt formats)
- **File Format Conversion:** Converts binary data to structured xarray DataArray format
- **Processing:** Applies scaling factors, byte order conversion (big-endian to native), and array reshaping to raw binary data
- **2D Graphics:** Creates 2D visualizations using matplotlib pcolormesh
- **Spectrogram:** Displays frequency vs time plots of radio occultation data
- **Mission-related Analysis:** Specifically designed for Mars Global Surveyor mission data analysis
- **Mission-related Science Data Processing:** Processes Mars Global Surveyor radio science data for scientific analysis

### 5. Related Region (MANDATORY)
**Value:** Planetary Magnetospheres
**Source:** PyHC registry keywords ("planetary"), scientific context
**Reasoning:** Mars Global Surveyor radio occultation data is used to study Mars' atmosphere and ionosphere, which falls under planetary studies. While Mars lacks a strong global magnetosphere, it has localized magnetic fields and an ionosphere that are studied through radio occultation experiments.

### 6. Authors (MANDATORY)
**Author 1:**
- **Authors:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** SciVision, Inc.
  - **Affiliation Identifier:** Not found

**Source:** DataCite API, setup.cfg, Zenodo API
**Note:** Only one author identified across all metadata sources

### 7. Software Name (MANDATORY)
**Value:** mgsradio
**Source:** setup.cfg (package name), PyHC registry lists it as "MGSutils"
**Note:** The package name is "mgsradio" but it's known as "MGSutils" in PyHC registry and was originally "mgs-utils". Current repository name is "mgs-radio"

### 8. Description (MANDATORY)
**Value:** Mars Global Surveyor radio occultation experiment read and plot. This software provides utilities for reading MGS radio occultation data files in .sri, .lbl, and .srt formats and creating visualizations of the occultation data. The .sri data is big-endian int16 in Fortran order. The software supports reading high-level occultation data and plotting frequency vs time spectrograms to analyze Mars atmospheric properties derived from radio occultation experiments.

**Source:** setup.cfg, README.md, DataCite API, code analysis
**Note:** Combined description from multiple sources to provide comprehensive detail

### 9. Concise Description (OPTIONAL)
**Value:** Mars Global Surveyor radio occultation data reader and plotter for analyzing Mars atmospheric properties from radio occultation experiments.

**Source:** Synthesized from setup.cfg and README.md

### 10. Publication Date (RECOMMENDED)
**Value:** 2014-09-15
**Source:** Git history (first commit date), SoMEF
**Note:** This is the date of the first commit to the repository, predating the first release by several years

### 11. Publisher (RECOMMENDED)
**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)
**Latest Version:**
- **Version Number:** 1.1.0
- **Version Date:** 2020-05-04
- **Version Description:** Rename, refactor
- **Version PID:** Not found (DOI only exists for v1.0.1)

**Previous Versions:**

**Version v1.0.1:**
- **Version Number:** v1.0.1
- **Version Date:** 2017-04-24
- **Version Description:** Not found
- **Version PID:** https://doi.org/10.5281/zenodo.556924

**Version v1.0.0:**
- **Version Number:** v1.0.0
- **Version Date:** 2017-04-23
- **Version Description:** Not found
- **Version PID:** Not found

**Source:** setup.cfg (v1.1.0), SoMEF releases, git tags, Zenodo API

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x
- MATLAB

**Source:** SoMEF, setup.cfg (Python >= 3.6), repository file analysis
**Note:** Primary language is Python 3.x; MATLAB code also present in matlab/ directory

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found
**Source:** No CITATION.cff file, no reference publication mentioned in README or metadata

### 15. License (RECOMMENDED)
**License:**
- **License:** Apache License 2.0
- **License URI:** http://www.apache.org/licenses/LICENSE-2.0

**Source:** LICENSE.txt, SoMEF (SPDX: Apache-2.0), setup.cfg

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- mars
- mars-global-surveyor
- radio-occultation
- planetary
- Mars global surveyor
- radio occultation

**Source:** SoMEF (GitHub topics), setup.cfg, PyHC registry
**Note:** Slight variations in capitalization and hyphenation across sources

### 17. Data Sources (OPTIONAL)
**Value:** Observatory/Mission-specific
**Source:** Code analysis, README
**Note:** Reads Mars Global Surveyor mission-specific data from PDS Geosciences Node archives

### 18. Input File Formats (RECOMMENDED)
**Values:**
- Other

**Source:** Code analysis
**Note:** The software reads mission-specific file formats (.sri, .lbl, .srt) which are not in the standard list. These are:
- .sri: binary data files (big-endian int16, Fortran order)
- .lbl: label/metadata files (parsed as CSV with '=' separator)
- .srt: time information files

### 19. Output File Formats (RECOMMENDED)
**Value:** Not found
**Source:** Code analysis shows the software creates visualizations but does not appear to export data in specific file formats (only displays plots)

### 20. Operating System (RECOMMENDED)
**Values:**
- Operating System Independent
- Linux

**Source:** setup.cfg declares "Operating System :: OS Independent", CI testing on Linux (ubuntu-latest)
**Note:** As a pure Python package, it should work on all major operating systems (Linux, Mac, Windows)

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent
**Source:** Pure Python implementation with no architecture-specific dependencies

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found
**Source:** No specific phenomena keywords found in metadata; general radio occultation science applicable

### 23. Development Status (RECOMMENDED)
**Value:** Active
**Source:** setup.cfg classifiers (Development Status :: 4 - Beta), recent updates
**Note:** setup.cfg indicates "Beta" status, which corresponds to "Active" in HSSI terminology. Last update was 2023-11-01 according to SoMEF.

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/mgs-radio#readme
**Source:** Repository README
**Note:** No separate documentation site found; documentation is in README.md with installation and usage examples. Data source links are provided to PDS Geosciences Node.

### 25. Funder (OPTIONAL)
**Value:** Not found
**Source:** No funding information in DataCite API, README, or other metadata sources

### 26. Award Title (OPTIONAL)
**Value:** Not found
**Source:** No award information found in any metadata sources

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found
**Source:** No related publications found in DataCite relatedIdentifiers or README

### 28. Related Datasets (OPTIONAL)
**Values:**
- http://pds-geosciences.wustl.edu/missions/mgs/rsdata.html (MGS Radio Science Data archive)
- http://pds-geosciences.wustl.edu/mgs/mgs-m-rss-5-sdp-v1/mors_1038/index/cumindex.tab (Cumulative file index)
- http://pds-geosciences.wustl.edu/mgs/mgs-m-rss-5-sdp-v1/mors_1014/ (Example data)

**Source:** README.md
**Note:** These are the data sources mentioned in the README for finding MGS radio occultation data files

### 29. Related Software (OPTIONAL)
**Dependencies:**
- python-dateutil
- numpy
- pandas
- xarray
- matplotlib (implied by plotting code)
- seaborn (used in example script)

**Source:** setup.cfg (install_requires), code analysis
**Note:** These are required dependencies, not necessarily related software packages. No DOIs available for dependencies.

### 30. Interoperable Software (OPTIONAL)
**Value:** Not found
**Source:** No explicit interoperability statements in documentation or metadata

### 31. Related Instruments (OPTIONAL)
**Value:**
- **Instrument Name:** MGS Radio Science Subsystem
- **Instrument Identifier:** Not found

**Source:** README.md, scientific context
**Note:** The software is designed to work with data from the Mars Global Surveyor Radio Science Subsystem used for radio occultation experiments

### 32. Related Observatories (OPTIONAL)
**Value:**
- **Observatory Name:** Mars Global Surveyor

**Source:** README.md, software name and description across all sources
**Note:** Mars Global Surveyor (MGS) was a NASA spacecraft mission to Mars (1996-2006)

### 33. Logo (OPTIONAL)
**Value:** Not found
**Source:** No logo found in repository or PyHC registry

---

## Summary of Metadata Sources

This metadata extraction utilized the following sources in priority order:

1. **PyHC Registry (Unevaluated)** - Manually curated metadata confirmed package is listed
2. **DataCite API** - DOI metadata for concept DOI (10.5281/zenodo.595431)
3. **Zenodo API** - Version-specific metadata
4. **SoMEF** - Automated extraction from repository
5. **Manual Repository Examination** - README.md, LICENSE.txt, setup.cfg, pyproject.toml, code analysis
6. **Git History** - Version dates, publication date

---

## Notes

- **Repository Migration:** The repository was originally hosted at scivision/mgs-utils and has been moved to space-physics/mgs-radio. The DataCite/Zenodo DOI metadata still references the old URL.
- **Naming Inconsistency:** The software is known by multiple names: "mgsradio" (package name), "MGSutils" (PyHC), "mgs-utils" (old repo), "mgs-radio" (current repo)
- **Limited DOI Coverage:** Only version v1.0.1 has a version-specific DOI. The latest version (v1.1.0) does not have a DOI registered.
- **Minimal Documentation:** No dedicated documentation site; all documentation is in README.md
- **Pure Python:** The software is primarily Python-based with some MATLAB utilities included
- **Mission-Specific:** Highly specialized for Mars Global Surveyor radio occultation data formats
