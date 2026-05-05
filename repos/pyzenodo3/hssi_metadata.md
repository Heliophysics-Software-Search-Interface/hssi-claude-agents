# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/pyzenodo3
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.3239431
- **Source:** DataCite API, Zenodo API. This is the concept DOI for all versions.

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/space-physics/pyzenodo3
- **Source:** DataCite API, SoMEF, PyHC registry

### 4. Software Functionality (MANDATORY)
- **Data Processing and Analysis**
- **Data Processing and Analysis:Data Access and Retrieval**
- **Source:** Manual analysis of repository code and documentation. PyZenodo is a Python wrapper for the Zenodo REST API that enables searching/retrieving Zenodo records and uploading files and metadata to Zenodo.

### 5. Related Region (MANDATORY)
- **Earth Atmosphere**
- **Earth Magnetosphere**
- **Solar Environment**
- **Source:** PyHC registry keywords (ionosphere_thermosphere_mesosphere, magnetosphere, solar). PyZenodo is a general Zenodo API client; these regions reflect the PyHC registry classification rather than region-specific algorithms in the code.

### 6. Authors (MANDATORY)

#### Author 1
- **Authors:** Michael Hirsch
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found
- **Source:** DataCite API, setup.cfg

#### Author 2
- **Authors:** Tom Klaver
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found
- **Source:** setup.cfg

**Note:** GitHub username "kasbah" mentioned in release notes as contributor but not listed as primary author.

### 7. Software Name (MANDATORY)
- **Software Name:** PyZenodo
- **Source:** PyHC registry authoritative name and README.md title. Package and repository identifiers use `pyzenodo3`.

### 8. Description (MANDATORY)
- **Description:** PyZenodo, distributed as the `pyzenodo3` Python package, is a pure Python wrapper for the Zenodo REST API. It provides a Python 3 interface for interacting with Zenodo records, including functionality to search Zenodo by query, GitHub repository, or DOI; retrieve record/version metadata; prepare Zenodo metadata from `.ini` files; and upload files to Zenodo depositions. The package includes a `--use-sandbox` flag to avoid cluttering Zenodo with test uploads during development. PyZenodo is useful for researchers who need to programmatically deposit datasets or inspect Zenodo records as part of their data management workflows.
- **Source:** Compiled from README.md, DataCite API, SoMEF, and PyHC registry

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Pure Python wrapper for the Zenodo REST API that enables programmatic record search, metadata retrieval, and file upload.
- **Source:** Derived from README.md and package description

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2018-06-25
- **Source:** SoMEF (date_created from GitHub API)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

#### Latest Published Release (1.0.2)
- **Version Number:** 1.0.2
- **Version Date:** 2020-04-28
- **Version Description:** Added `upload_zenodo.py --use-sandbox` flag to avoid cluttering Zenodo with test uploads (thanks to @kasbah). Moved package to src/ layout.
- **Version PID:** https://doi.org/10.5281/zenodo.3772154
- **Source:** DataCite API, Zenodo API, GitHub Releases, PyPI

**Repository note:** `setup.cfg` declares version 1.1.0 on the main branch, but no GitHub, PyPI, or Zenodo release or DOI was found for 1.1.0.

**Other Available Versions:**
- v1.0.1 (2019-11-11): Modernized packaging, moved CI to Github actions, fixed issue #1
- v1.0.0 (2019-06-05): Initial release
- v0.3.1, v0.3.0, v0.1.1 (2018-06-26): Early versions

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (requires Python >= 3.6)
- **Source:** SoMEF, setup.cfg

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication:** Not found
- **Note:** No JOSS paper or similar publication describing the software was found.

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** https://www.apache.org/licenses/LICENSE-2.0
- **Source:** SoMEF (SPDX ID: Apache-2.0), LICENSE.txt file

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- json
- zenodo
- open data
- ionosphere_thermosphere_mesosphere
- magnetosphere
- solar
- **Source:** SoMEF (GitHub topics), setup.cfg, PyHC registry

### 17. Data Sources (OPTIONAL)
- **Other** (Zenodo repository)
- **Source:** Manual analysis - the software accesses Zenodo as a data source

### 18. Input File Formats (RECOMMENDED)
- **Other** (.ini metadata files for uploads; arbitrary payload files are passed through to Zenodo rather than parsed as scientific data files)
- **Source:** Manual analysis of README.md and code

### 19. Output File Formats (RECOMMENDED)
- **JSON** (API responses)
- **Other** (metadata JSON files generated from `.ini` upload metadata)
- **Source:** Manual analysis of code (`base.py` returns JSON API responses; `upload.py` writes JSON metadata files)

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**
- **OS Independent** (Pure Python implementation)
- **Source:** CI/CD configuration (.github/workflows/ci.yml shows testing on ubuntu-latest, macos-latest, windows-latest), setup.cfg classifiers

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** (Pure Python, no compiled extensions)
- **Source:** Manual analysis - pure Python package with no compiled dependencies

### 22. Related Phenomena (OPTIONAL)
- Not found
- **Note:** This is a general data access tool, not specific to particular heliophysics phenomena.

### 23. Development Status (RECOMMENDED)
- **Inactive**
- **Source:**
  - GitHub default branch `main` points to commit `09bdb3f9f0ac9961f74220a21ca6d4fd666e198a`, dated 2021-04-27
  - Latest GitHub, PyPI, and Zenodo release is 1.0.2 from 2020-04-28
  - setup.cfg classifiers indicate "Development Status :: 4 - Beta"
  - Repository is not archived or disabled, so Inactive is more appropriate than Abandoned or Unsupported

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/space-physics/pyzenodo3
- **Source:** README.md serves as primary documentation. No separate documentation site found (no ReadTheDocs or similar).

### 25. Funder (OPTIONAL)
- Not found
- **Source:** No funding information in DataCite API, repository files, or documentation

### 26. Award Title (OPTIONAL)
- Not found
- **Source:** No award information found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Not found
- **Source:** No publications citing or describing this software were found in the repository or APIs

### 28. Related Datasets (OPTIONAL)
- Not applicable - This tool provides access to any dataset hosted on Zenodo
- **Source:** Manual analysis

### 29. Related Software (OPTIONAL)
- https://github.com/zenodo/zenodo (Zenodo platform wrapped by this client)
- https://github.com/psf/requests (Python dependency)
- https://www.crummy.com/software/BeautifulSoup/ (Beautiful Soup / beautifulsoup4 Python dependency)
- **Source:** setup.cfg dependencies and README.md usage description

### 30. Interoperable Software (OPTIONAL)
- Not found
- **Note:** As a Zenodo API client, it can retrieve data that may be used with various analysis packages, but no specific interoperability is documented.

### 31. Related Instruments (OPTIONAL)
- Not applicable
- **Source:** This is a general data access tool, not instrument-specific

### 32. Related Observatories (OPTIONAL)
- Not applicable
- **Source:** This is a general data access tool, not observatory-specific

### 33. Logo (OPTIONAL)
- Not found
- **Source:** No logo found in repository or PyHC registry

---

## Additional Notes

### PyHC Package Status
- **PyHC Status:** Unevaluated
- **PyHC Name:** PyZenodo
- **PyHC Contact:** Michael Hirsch
- **Source:** PyHC unevaluated packages registry

### Alternative Citations
The CITATION file in the repository points to an older version DOI:
- **CITATION file DOI:** https://doi.org/10.5281/zenodo.3537730
- **Concept DOI:** https://doi.org/10.5281/zenodo.3239431 (recommended for citing all versions)
- **Latest version DOI:** https://doi.org/10.5281/zenodo.3772154 (v1.0.2)

### Package Identifiers
- **PyPI Package Name:** pyzenodo3
- **GitHub Repository:** space-physics/pyzenodo3
- **GitHub Owner:** space-physics
- **Zenodo Badge:** [![DOI](https://zenodo.org/badge/138543765.svg)](https://zenodo.org/badge/latestdoi/138543765)

### Contact Information
- **Primary Contact:** Michael Hirsch
- **Email:** scivision@users.noreply.github.com (from setup.cfg)
- **GitHub:** scivision (author username from releases)

### Repository Statistics (from SoMEF)
- **Stars:** 40
- **Forks:** 5
- **Issue Tracker:** https://api.github.com/repos/space-physics/pyzenodo3/issues

### Installation
```sh
pip install pyzenodo3
```

Or for latest development version:
```sh
git clone https://github.com/space-physics/pyzenodo3
pip install -e pyzenodo3
```
