# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/AEindex
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found

**Note:** No DOI found in repository files (no CITATION.cff, .zenodo.json, or codemeta.json files present). No DOI badges found in README.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/AEindex

**Source:** GitHub repository URL

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization:2D Graphics
- Data Visualization:Line Plots

**Source:** Analyzed from code examination. The software reads auroral electrojet index data from ASCII files, performs analysis and processing of time series data, and creates line plots for visualization.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere

**Source:** Determined from software description and functionality. The Auroral Electrojet (AE) index measures geomagnetic activity in the ionosphere and magnetosphere. The keywords in setup.cfg include "mesosphere", "thermosphere", "ionosphere", and "aurora", which primarily relate to Earth Atmosphere, while the geomagnetic activity and auroral electrojet phenomena involve both the ionosphere (Earth Atmosphere) and magnetosphere (Earth Magnetosphere). The "geomagnetic" keyword from SoMEF also supports magnetospheric relevance.

### 6. Authors (MANDATORY)

**Author 1:**
- **Authors:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** From setup.cfg (author field). Author email found: scivision@users.noreply.github.com

**Note:** PyHC registry lists contact as "Michael Hirsch" but does not provide ORCID or affiliation information.

### 7. Software Name (MANDATORY)
AEindex (package name: aeindex)

**Source:** Repository name, PyHC registry ("Auroral Electrojet"), SoMEF, and setup.cfg (name field)

### 8. Description (MANDATORY)
Auroral Electrojet AE-index read and plot. This software loads and plots auroral electrojet indices (AE, AU, AL, AO) from data files obtained from the AE-index data web interface at Kyoto University. The data is provided in WDC-like format as ASCII data tables.

**Source:** Combined from README.md, setup.cfg description ("Load and Plot auroral electroject indices"), PyHC description, and SoMEF

### 9. Concise Description (OPTIONAL)
Auroral Electrojet AE-index read and plot.

**Source:** PyHC description and SoMEF (GitHub API description)

### 10. Publication Date (RECOMMENDED)
2017-02-23

**Source:** Git repository creation date (first commit: 2017-02-23 17:47:14 -0500)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** No DOI found, so publisher is the repository host (GitHub)

### 12. Version (RECOMMENDED)

**Latest Version:**
- **Version Number:** v2.4.0
- **Version Date:** Not found (no git tag for v2.4.0)
- **Version Description:** Not found
- **Version PID:** Not found

**Source:** Version 2.4.0 from setup.cfg. Only one git tag exists (v1.0 from 2017-03-13), but setup.cfg shows current version as 2.4.0.

**Note:** There is a discrepancy between the git tags (only v1.0 exists) and the version in setup.cfg (2.4.0). The latest tag is v1.0 from 2017-03-13.

**Tag v1.0:**
- **Version Number:** v1.0
- **Version Date:** 2017-03-13
- **Version Description:** Initial (from SoMEF release data)
- **Version PID:** Not found

### 13. Programming Language (RECOMMENDED)
- Python 3.x

**Source:** setup.cfg lists Python 3.6, 3.7, 3.8, 3.9; SoMEF detected Python; file extensions confirm Python codebase

### 14. Reference Publication (RECOMMENDED)
Not found

**Note:** No CITATION.cff file, no DOI for a reference publication found in README or other files

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** https://spdx.org/licenses/Apache-2.0.html

**Source:** LICENSE.txt file contains full Apache 2.0 license text; SoMEF confirmed via GitHub API; SPDX ID: Apache-2.0

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- ae-index
- aurora
- auroral electrojet
- geomagnetic
- ionosphere
- ionosphere_thermosphere_mesosphere
- mesosphere
- thermosphere

**Source:** Combined from multiple sources:
- SoMEF (GitHub API topics): ae-index, aurora, geomagnetic, ionosphere
- setup.cfg: mesosphere, thermosphere, ionosphere, aurora
- PyHC keywords: ionosphere_thermosphere_mesosphere

### 17. Data Sources (OPTIONAL)
- Other

**Note:** Data comes from the AE-index data web interface at Kyoto University (http://wdc.kugi.kyoto-u.ac.jp/aeasy/index.html). Data is downloaded manually and provided as local ASCII files in WDC-like format.

### 18. Input File Formats (RECOMMENDED)
- ascii

**Source:** README.md indicates data is obtained as "ASCII data tables" in "WDC-like format". Code analysis shows reading from fixed-width format files.

### 19. Output File Formats (RECOMMENDED)
- Other (plotting output - display only)

**Source:** Code analysis shows the software primarily produces matplotlib plots for display. No evidence of file output functionality in the code.

### 20. Operating System (RECOMMENDED)
- Operating System Independent

**Source:** setup.cfg classifiers include "Operating System :: OS Independent"

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Source:** Pure Python implementation with standard libraries (numpy, pandas, matplotlib), no architecture-specific requirements

### 22. Related Phenomena (OPTIONAL)
Not found in standard controlled vocabularies

**Note:** The software deals with auroral electrojet phenomena, which relates to geomagnetic activity and auroral processes, but specific controlled vocabulary terms were not available in the provided list.

### 23. Development Status (RECOMMENDED)
- Active

**Source:** setup.cfg classifiers include "Development Status :: 4 - Beta", indicating active development. Latest commit was 2022-08-11, suggesting the project may be less active now but has reached a usable state.

**Note:** SoMEF did not detect a specific repostatus.org badge. Based on commit history (last commit in 2022) and Beta status, it appears to be in an "Inactive" or "Active" state depending on interpretation.

### 24. Documentation (RECOMMENDED)
Not found

**Note:** No separate documentation URL found. README.md contains basic installation and usage instructions but no link to external documentation. No docs/ folder in repository. No readthedocs configuration found.

### 25. Funder (OPTIONAL)
Not found

### 26. Award Title (OPTIONAL)
Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

**Note:** README includes a link to a paper about the physical meaning of the AE index (http://onlinelibrary.wiley.com/doi/10.1029/2004EO190010/abstract), but this is a background reference, not a publication about this specific software.

### 28. Related Datasets (OPTIONAL)
Not found

**Note:** The software uses data from the AE-index data web interface (http://wdc.kugi.kyoto-u.ac.jp/aeasy/index.html), but no DOI or formal dataset citation is available.

### 29. Related Software (OPTIONAL)
Not found

**Note:** No dependencies on other scientific software packages beyond standard libraries (numpy, pandas, matplotlib, python-dateutil, seaborn)

### 30. Interoperable Software (OPTIONAL)
Not found

**Note:** No evidence of demonstrated interoperability with other heliophysics software packages

### 31. Related Instruments (OPTIONAL)
Not found

**Note:** The AE index is derived from a network of magnetometer stations, but no specific instrument identifiers are provided in the repository.

### 32. Related Observatories (OPTIONAL)
Not found

**Note:** The AE index data comes from a global network of magnetometer stations coordinated by the World Data Center for Geomagnetism at Kyoto University, but no specific observatory identifiers are provided.

### 33. Logo (OPTIONAL)
Not found

**Note:** No logo file or logo URL found in repository

---

## PyHC Package Information

This package is listed in the PyHC (Python in Heliophysics Community) **Unevaluated Packages** registry:

- **PyHC Name:** Auroral Electrojet
- **PyHC Description:** Auroral Electrojet AE-index read and plot.
- **PyHC Contact:** Michael Hirsch
- **PyHC Keywords:** ionosphere_thermosphere_mesosphere, specific
- **PyHC Quality Ratings:** Not available (unevaluated package)

**Source:** https://github.com/heliophysicsPy/heliophysicsPy.github.io/blob/main/_data/projects_unevaluated.yml

---

## Additional Notes

### Data Source Details
The software reads AE index data from the World Data Center for Geomagnetism at Kyoto University. According to the README:
- Data URL: http://wdc.kugi.kyoto-u.ac.jp/aeasy/index.html
- Data format: "AE output" in "WDC-like format" as ASCII data tables
- Format specification: http://wdc.kugi.kyoto-u.ac.jp/aeasy/format/aeformat.html
- Physical meaning: http://onlinelibrary.wiley.com/doi/10.1029/2004EO190010/abstract

### Software Dependencies
Required packages (from setup.cfg):
- python-dateutil
- numpy
- pandas

Optional packages for plotting:
- matplotlib
- seaborn

Testing/development packages:
- pytest
- flake8
- mypy

### Installation
According to README.md:
```bash
pip install -e .
```

### Usage Example
According to plotAE.py and README.md:
```bash
plotAE.py data/WWW_aeasy00007552.dat -t 2013-05-01T07:00 2013-05-01T11:00
```

### GitHub Repository Metadata
- **Owner:** space-physics (organization)
- **Stargazers:** 3
- **Forks:** 1
- **Created:** 2017-02-23
- **Last Updated:** 2024-01-22 (per SoMEF GitHub API data)
- **Issue Tracker:** https://api.github.com/repos/space-physics/AEindex/issues

**Source:** SoMEF output from GitHub API

---

## Metadata Extraction Summary

### Sources Used
1. ✅ DataCite API - Not applicable (no DOI found)
2. ✅ Zenodo API - Not applicable (no Zenodo DOI found)
3. ✅ SoMEF - Completed successfully
4. ✅ PyHC Registry - Package found in unevaluated packages list
5. ✅ Manual Repository Examination - Completed

### Completeness
- **MANDATORY fields:** 6/6 completed (Submitter is user-provided)
- **RECOMMENDED fields:** 10/12 completed (Documentation and Funder not found)
- **OPTIONAL fields:** 2/15 completed (Keywords and Data Sources found)

### Confidence Level
- **High confidence:** Repository URL, Software Name, Description, Authors, License, Programming Language, Version, Operating System, Keywords
- **Medium confidence:** Software Functionality, Related Region (inferred from description and keywords)
- **Low confidence:** None

### Missing Critical Information
- No DOI or persistent identifier
- No separate documentation beyond README
- No formal citation file (CITATION.cff)
- Limited author information (no ORCID, no affiliation)
- No version tags in git beyond v1.0 (despite setup.cfg showing v2.4.0)
- No reference publication
- No related publications or datasets
