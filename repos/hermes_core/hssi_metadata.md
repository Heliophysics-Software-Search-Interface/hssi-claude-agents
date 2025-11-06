# HSSI Metadata Extraction Results

**Repository:** https://github.com/HERMES-SOC/hermes_core
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Concept DOI:** https://doi.org/10.5281/zenodo.10257715
- **Source:** Provided by user; confirmed via DataCite API
- **Note:** This is the concept DOI for all versions

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/HERMES-SOC/hermes_core
- **Source:** Repository URL, SoMEF, PyHC registry

### 4. Software Functionality (MANDATORY)
Based on comprehensive code analysis, documentation review, and the software's purpose as a data processing and analysis package for the HERMES mission, the following functionalities apply:

- **Data Processing and Analysis**
- **Data Processing and Analysis:Calibration**
- **Data Processing and Analysis:Data Access and Retrieval**
- **Data Processing and Analysis:Processing**
- **Data Processing and Analysis:Spectrogram**
- **Data Processing and Analysis:Time Series Analysis**
- **Data Visualization**
- **Data Visualization:Line Plots**
- **Data Visualization:Spectrogram**
- **Mission-related**
- **Mission-related:Calibration**
- **Mission-related:Processing**
- **Mission-related:Science Data Processing**

**Sources:**
- Code analysis of HermesData class (data container, time series processing, spectra handling)
- README description: "loading, calibrating, plotting, validating, and saving of measurement data through Common Data Format (CDF) files"
- DataCite description: "loading, calibrating, plotting, validating, and saving of measurement data"
- PyHC keywords: "data_container", "time", "plotting", "spectra", "data_analysis"

### 5. Related Region (MANDATORY)
- **Solar Environment** - HERMES observes solar particles and solar wind directly from the Sun
- **Interplanetary Space** - HERMES operates in cislunar space and observes the solar wind
- **Earth Magnetosphere** - HERMES spends time in Earth's magnetotail studying magnetospheric phenomena

**Sources:**
- NASA Science web search results about HERMES mission
- Mission description: "observe solar particles and the solar wind" from lunar orbit
- Operates in cislunar space (Earth-Moon system)
- Spends time both inside Earth's magnetosphere and in interplanetary space

### 6. Authors (MANDATORY)

**Primary Authors (from pyproject.toml):**

1. **Steven Christe**
   - Email: steven.d.christe@nasa.gov
   - ORCID: https://orcid.org/0000-0001-6127-795X
   - Affiliation: NASA Goddard Space Flight Center, Greenbelt, MD, United States

2. **Damian Barrous Dumme**
   - Email: damianbarrous@gmail.com
   - ORCID: https://orcid.org/0009-0006-2684-0675
   - Affiliation: Community Coordinated Modeling Center, NASA GSFC, Navteca, Greenbelt, MD, United States

3. **Andrew Robbertz**
   - Email: a.robbertz@gmail.com
   - ORCID: https://orcid.org/0009-0008-6857-0882
   - Affiliation: General Dynamics Mission Systems Fairfax, VA, United States

**Additional Authors (from DataCite/Zenodo):**

4. **Amy Rager**
   - ORCID: https://orcid.org/0000-0001-7088-1059
   - Affiliation: General Dynamics Mission Systems Fairfax, VA, United States

5. **Daniel Skeberdis**
   - Affiliation: a.i. solutions, Inc., Lanham, MD, United States

6. **Steve Kreisler**
   - Affiliation: Columbus Technologies and Services, Greenbelt, MD, United States

7. **Tony Mercer**
   - Affiliation: Space science laboratory, Berkeley, CA, United States

8. **William R. Paterson**
   - Affiliation: NASA Goddard Space Flight Center, Greenbelt, MD, United States

**Sources:** pyproject.toml, DataCite API, Zenodo API, PyHC registry

### 7. Software Name (MANDATORY)
- **Name:** hermes_core
- **Full Name:** HERMES Core
- **Long Name:** Heliophysics Environmental and Radiation Measurement Experiment Suite (HERMES) Core Package
- **Source:** Repository name, PyHC registry, DataCite metadata

### 8. Description (MANDATORY)
A central Python package for common functionality across all HERMES instruments. The HERMES core package contains Python interfaces for the loading, calibrating, plotting, validating, and saving of measurement data through Common Data Format (CDF) files. Additional packages are created for HERMES instruments to provide specific calibration and processing functionality. The abstraction of intricate, high heritage, data formats, such as CDF files, in Python enables easier analysis and opens doors for greater participation in heliophysics science.

**Sources:** README.rst, DataCite API, Zenodo API, PyHC registry, SoMEF

### 9. Concise Description (OPTIONAL)
A Python package to support the HERMES instrument packages, providing common functionality for loading, calibrating, plotting, validating, and saving measurement data through CDF files.

**Source:** pyproject.toml, SoMEF

### 10. Publication Date (RECOMMENDED)
- **Date:** 2022-03-17 (repository creation date)
- **First Release Date:** 2022-10-05 (v0.1.0)
- **Source:** GitHub API via SoMEF, CHANGELOG.rst

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

**Latest Tagged Version:**
- **Version Number:** v0.2.0
- **Version Date:** 2023-03-22 (publication date) / 2023-01-05 (tag date)
- **Version Description:** This release includes improvements tested in the second dataflow test. Uses fstrings instead of the format syntax, adds a log message on import to show the version number of the package, documentation content and styling improvements, switches from using setup.py to pyproject.toml for package, and bug fixes for supporting pathlib's Path objects and a permissions bug to the devcontainer.
- **Version PID:** https://doi.org/10.5281/zenodo.10257716

**Previous Version:**
- **Version Number:** v0.1.0
- **Version Date:** 2022-10-05
- **Version Description:** This version release was tested in the first HERMES Ground System data flow test. Includes first draft of python packaging including sphinx documentation based on the sunpy package template, first draft of the documentation including coding standards for the HERMES ecosystem, automated testing and coverage using GitHub actions, logging support, configuration support, and utilities parsing compliant filenames for level 0 binary files and creating and parsing higher level filenames.

**Sources:** CHANGELOG.rst, GitHub releases (via SoMEF), git tags, Zenodo API

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (specifically Python 3.9, 3.10, 3.11, 3.12, 3.13 are tested)
- **Source:** pyproject.toml (requires-python >= 3.9), GitHub workflows, SoMEF, PyHC registry

### 14. Reference Publication (RECOMMENDED)
- **Not found** - No reference publication DOI exists yet
- **Note:** CITATION.rst states "A paper citation does not yet exist."
- **Source:** CITATION.rst

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** http://www.apache.org/licenses/LICENSE-2.0
- **Source:** licenses/LICENSE.md, pyproject.toml, PyHC registry, DataCite API

**Additional Information:**
- The README.rst also mentions that "This project constitutes a work of the United States Government and is not subject to domestic copyright protection under 17 USC § 105" and includes a CC0 1.0 Universal public domain dedication.
- **CC0 License URI:** https://creativecommons.org/publicdomain/zero/1.0/

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- hermes
- nasa mission
- space weather
- nasa
- data_container
- time
- plotting
- spectra
- cdf
- data_analysis
- heliophysics
- calibration
- validation

**Sources:** pyproject.toml, SoMEF, PyHC registry, DataCite description

### 17. Data Sources (OPTIONAL)
- **Observatory/Mission-specific** (HERMES mission instruments)
- **Note:** Designed specifically for HERMES mission data from instruments EEA, NEMISIS, MERIT, and SPANI
- **Source:** Code analysis (instrument names in config), DataCite description

### 18. Input File Formats (RECOMMENDED)
- **CDF** (Common Data Format) - Primary input format
- **Source:** Code analysis, documentation references to reading CDF files, schema files reference ISTP-compliant CDF

### 19. Output File Formats (RECOMMENDED)
- **CDF** (Common Data Format) - Primary output format
- **ISTP-Compliant** CDF files specifically
- **Source:** Code analysis (HermesData class has methods for saving to CDF), schema for CDF validation, documentation

### 20. Operating System (RECOMMENDED)
- **Linux** (ubuntu-latest tested in CI)
- **Mac** (macos-latest tested in CI)
- **Windows** (windows-latest tested in CI)
- **Operating System Independent** (Python-based, should work on any OS with Python 3.9+)
- **Source:** .github/workflows/testing.yml

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** (Pure Python package with no platform-specific compiled code)
- **Note:** May depend on compiled dependencies (astropy, numpy, spacepy) but those handle architecture independence
- **Source:** Code analysis, package structure

### 22. Related Phenomena (OPTIONAL)
Based on HERMES mission objectives:
- **Solar Flares** (monitoring solar activity)
- **Coronal Mass Ejections** (space weather observations)
- **Solar wind** (primary observation target)
- **Note:** These are inferred from the mission's focus on space weather and solar particle observation
- **Source:** Web search about HERMES mission objectives, space weather focus

### 23. Development Status (RECOMMENDED)
- **Active** - The repository is actively developed with recent commits, ongoing testing, and support
- **PyHC Status:**
  - Community: Partially met
  - Documentation: Good
  - Testing: Good
  - Software Maturity: Partially met
  - Python3: Good
  - License: Good
- **Source:** GitHub repository activity (last updated 2025-03-12 per SoMEF), PyHC registry quality ratings, active CI/CD

### 24. Documentation (RECOMMENDED)
- **Primary:** https://hermes-core.readthedocs.io/en/latest/
- **Alternative URL:** https://hermes_core.readthedocs.io/
- **Wiki:** https://github.com/HERMES-SOC/hermes_core/wiki
- **Source:** README.rst, SoMEF, PyHC registry

### 25. Funder (OPTIONAL)
- **Not found** - No funder information in repository or DOI metadata
- **Note:** As a NASA mission, likely funded by NASA but not explicitly stated in available metadata
- **Source:** DataCite API (empty fundingReferences)

### 26. Award Title (OPTIONAL)
- **Not found** - No award information available
- **Source:** DataCite API (empty fundingReferences)

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Not found** - No related publications identified
- **Source:** DataCite API

### 28. Related Datasets (OPTIONAL)
- **Not found** - No related datasets identified in metadata
- **Note:** The software is designed to work with HERMES mission data, but specific dataset DOIs are not referenced
- **Source:** DataCite API

### 29. Related Software (OPTIONAL)

**Dependencies (from pyproject.toml):**
- **swxsoc** - https://github.com/swxsoc/swxsoc (parent package, hermes_core extends swxsoc.swxdata.SWXData)
- **sunpy** >= 5.0.1 - https://github.com/sunpy/sunpy (solar physics library, DOI: 10.5281/zenodo.591887)
- **astropy** >= 5.3.3 - https://github.com/astropy/astropy
- **numpy** >= 1.18.0
- **spacepy** >= 0.5.0
- **ndcube** >= 2.2.0 - https://github.com/sunpy/ndcube
- **pyyaml** >= 5.3.1

**Acknowledged in README:**
- **OpenAstronomy community** - https://openastronomy.org (package template)
- **SunPy Project** - https://sunpy.org/ (package template)

**Sources:** pyproject.toml, README.rst, code imports

### 30. Interoperable Software (OPTIONAL)
Based on PyHC registry membership and dependencies:
- **swxsoc** - https://github.com/swxsoc/swxsoc - Direct integration, hermes_core extends swxsoc
- **sunpy** - https://github.com/sunpy/sunpy - Uses SunPy ecosystem packages
- **ndcube** - https://github.com/sunpy/ndcube - For spectral data handling
- **astropy** - https://github.com/astropy/astropy - Core astronomy library
- **spacepy** - https://github.com/spacepy/spacepy - Space science library

**Note:** As a PyHC community package, designed to work within the Python in Heliophysics Community ecosystem

**Sources:** pyproject.toml dependencies, PyHC registry membership, code analysis

### 31. Related Instruments (OPTIONAL)
Based on HERMES mission configuration:
- **EEA** (Electron Electrostatic Analyzer)
- **NEMISIS**
- **MERIT**
- **SPANI**

**Note:** These are the HERMES mission instruments that this software supports
**Source:** Code analysis (hermes_core/timedata.py line 116, instrument names in config)

### 32. Related Observatories (OPTIONAL)
- **HERMES** (Heliophysics Environmental and Radiation Measurement Experiment Suite)
- **Gateway** (NASA's Lunar Gateway where HERMES will be installed)
- **Note:** HERMES is a payload on NASA's Gateway outpost in lunar orbit
- **Source:** Web search about HERMES mission, software is mission-specific

### 33. Logo (OPTIONAL)
- **Logo URL:** https://raw.githubusercontent.com/HERMES-SOC/hermes_core/main/docs/logo/hermes_logo.png
- **Source:** PyHC registry

---

## Metadata Extraction Summary

### Data Sources Used:
1. **DataCite API** - DOI 10.5281/zenodo.10257715 (concept DOI)
2. **Zenodo API** - Record 10257716 (specific version)
3. **SoMEF** - Automated repository analysis
4. **PyHC Registry** - Found in community packages list
5. **Manual Repository Examination:**
   - README.rst
   - pyproject.toml
   - LICENSE.md
   - CHANGELOG.rst
   - GitHub workflows
   - Source code analysis (hermes_core package)
6. **Web Search** - HERMES mission information from NASA Science

### Metadata Completeness:
- **Mandatory Fields:** 6/6 completed (Submitter to be filled by user)
- **Recommended Fields:** 16/18 completed (87.5%)
  - Missing: Reference Publication (none exists yet), Funder (not documented)
- **Optional Fields:** 8/9 completed (88.9%)
  - Missing: Award information

### High-Confidence Metadata:
- Software name, description, and functionality
- Authors with ORCIDs and affiliations
- Repository URL and DOI
- Programming language (Python 3.9+)
- License (Apache 2.0)
- Operating systems (Linux, Mac, Windows)
- File formats (CDF input/output)
- Documentation URL
- Related software dependencies
- Related region (Solar Environment, Interplanetary Space, Earth Magnetosphere)

### Notes:
- The software is in active development (v0.2.0 released 2023-03-22)
- Part of the Python in Heliophysics Community (PyHC)
- Mission-specific for HERMES payload on NASA's Gateway
- Primary function is CDF data processing and validation for space weather observations
- No reference publication yet, but CITATION.rst indicates one may be forthcoming
