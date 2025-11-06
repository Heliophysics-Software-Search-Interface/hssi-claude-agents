# HSSI Metadata Extraction Results

**Repository:** https://github.com/MihailoMartinovic/SAVIC
**Extraction Date:** 2025-10-21

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.8170235
- **Source:** Concept DOI from Zenodo badge in README and DataCite API

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/MihailoMartinovic/SAVIC
- **Source:** GitHub repository URL, verified via SoMEF and PyHC registry

### 4. Software Functionality (MANDATORY)
- **Data Processing and Analysis:ML/AI** - Uses machine learning algorithms (XGBoost, scikit-learn) to predict plasma instabilities
- **Data Processing and Analysis:Analysis** - Analyzes velocity distribution functions (VDFs) of solar wind plasma particles
- **Models and Simulations:ML/AI** - ML-based prediction of unstable wave modes in plasma
- **Models and Simulations:Forecasting** - Predicts plasma instability characteristics
- **Source:** Repository documentation, PyHC metadata, code dependencies analysis

### 5. Related Region (MANDATORY)
- **Interplanetary Space** - Primary focus on solar wind plasma analysis
- **Solar Environment** - Analyzes solar wind particle distribution functions
- **Source:** PyHC keywords ("heliosphere"), documentation describing solar wind VDF analysis

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Martinović, Mihailo M.
- **Author Identifier:** https://orcid.org/0000-0002-7365-0472
- **Affiliation:**
  - **Organization:** University of Arizona
  - **Affiliation Identifier:** Not found
- **Source:** DataCite API contributors metadata, pyproject.toml

**Author 2:**
- **Name:** Klein, Kristopher G.
- **Author Identifier:** https://orcid.org/0000-0001-6038-1923
- **Affiliation:**
  - **Organization:** University of Arizona
  - **Affiliation Identifier:** Not found
- **Source:** DataCite API contributors metadata (listed as Project Member)

### 7. Software Name (MANDATORY)
- **Name:** SAVIC
- **Full Name:** Stability Analysis Vitalizing Instability Classification
- **Source:** GitHub API, PyHC registry, repository documentation

### 8. Description (MANDATORY)
- **Description:** SAVIC (Stability Analysis Vitalizing Instability Classification) is a Python package for predicting, quantifying and classifying ion-driven plasma instabilities in the solar wind. The software uses Machine Learning algorithms to decrease computational power requirements by several orders of magnitude compared to traditional dispersion solvers, providing instability properties for a given velocity distribution function (VDF) practically instantaneously. SAVIC combines three components: SAVIC-P (predictor of VDF stability), SAVIC-Q (regressors that quantify parameters of the most unstable mode), and SAVIC-C (classifiers that recognize the type of instability predicted for the given VDF). The software makes plasma stability analysis tools accessible to the entire community through a user-friendly environment.
- **Source:** Combined from PyHC description, DataCite description, and repository documentation (01-intro.rst, 01-purpose.rst)

### 9. Concise Description (OPTIONAL)
- **Concise Description:** ML-based Python package for predicting, quantifying and classifying ion-driven plasma instabilities in the solar wind, making stability analysis accessible to the community.
- **Source:** Derived from description (under 200 characters)

### 10. Publication Date (RECOMMENDED)
- **Date:** 2023-01-24
- **Source:** GitHub repository creation date from SoMEF

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API and Zenodo metadata

### 12. Version (RECOMMENDED)

**Version Number:**
- **Value:** v1.2.6
- **Source:** pyproject.toml, Zenodo metadata, GitHub releases

**Version Date:**
- **Value:** 2025-10-17
- **Source:** Git tag date, Zenodo publication date

**Version Description:**
- **Value:** SAVIC - Stability Analysis Vitalizing Instability Classification, Version: 1.2.6, Documentation: https://savic.readthedocs.io/en/latest/, Package: pip install savic
- **Source:** GitHub release notes

**Version PID:**
- **Value:** https://doi.org/10.5281/zenodo.17382178
- **Source:** Zenodo API (latest version DOI)

**Previous Versions:**
- v1.2.5 (2025-10-15) - DOI: 10.5281/zenodo.17344665
- v1.2.2 (2025-10-13)
- v1.2.0 (2025-10-13)
- v1.1.0 (2024-01-29) - DOI: 10.5281/zenodo.10581356
- v1.0.2 (2023-07-20) - DOI: 10.5281/zenodo.8170236

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** - Primary language (requires Python >=3.7)
- **Jupyter Notebook** - For tutorials and examples
- **Source:** pyproject.toml, SoMEF GitHub API analysis, repository structure

### 14. Reference Publication (RECOMMENDED)
- **DOI:** Not found
- **Note:** No reference publication DOI found in repository. Documentation mentions articles (via tutorial.article_path function) but specific DOIs not provided in accessible metadata.
- **Source:** Searched in DataCite relatedIdentifiers, README, documentation

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html
- **Source:** source/LICENSE file, pyproject.toml classifiers
- **Note:** DataCite lists CC-BY-4.0 for the Zenodo deposit, but the software code itself is MIT licensed

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **heliosphere** (from PyHC)
- **plasma_physics** (from PyHC)
- **multidimensional** (from PyHC)
- **solar wind** (inferred from documentation)
- **machine learning** (from functionality analysis)
- **instability classification** (from software name/purpose)
- **velocity distribution function** (from documentation)
- **plasma instabilities** (from description)
- **Source:** PyHC metadata, documentation analysis, software functionality

### 17. Data Sources (OPTIONAL)
- **Other** - Software generates predictions from VDF data; specific data sources depend on user input
- **Note:** SAVIC is primarily an analysis tool that operates on velocity distribution function data provided by the user
- **Source:** Documentation and code analysis

### 18. Input File Formats (RECOMMENDED)
- **HDF5** - Primary data format (uses "tables" package, PyHC keyword)
- **csv** - Likely supported for data input
- **Source:** PyHC keywords, dependencies (pytables/tables>=3.8.0), tutorial examples

### 19. Output File Formats (RECOMMENDED)
- **HDF5** - Primary output format
- **csv** - Likely supported for results output
- **Source:** Inferred from input formats and common Python data analysis practices

### 20. Operating System (RECOMMENDED)
- **Operating System Independent** - Python package installable via pip
- **Linux** - Supported
- **Mac** - Supported
- **Windows** - Likely supported (OS Independent Python package)
- **Source:** pyproject.toml classifiers ("Operating System :: OS Independent")

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent** - Pure Python package with standard dependencies
- **Source:** Package structure analysis (Python-only implementation)

### 22. Related Phenomena (OPTIONAL)
- **Solar Wind** (custom entry - primary phenomenon studied)
- **Note:** No exact matches in provided controlled vocabulary list for specific plasma phenomena
- **Source:** Documentation describing solar wind VDF analysis

### 23. Development Status (RECOMMENDED)
- **Active** - Reached stable, usable state and being actively developed
- **Source:** Recent releases (v1.2.6 on 2025-10-17), PyHC quality ratings showing "Good" or "Partially met", active maintenance

### 24. Documentation (RECOMMENDED)
- **URL:** https://savic.readthedocs.io/en/latest/
- **Source:** README, PyHC metadata, SoMEF, pyproject.toml, Zenodo description

### 25. Funder (OPTIONAL)
- **Not found**
- **Source:** DataCite API shows no fundingReferences

### 26. Award Title (OPTIONAL)
- **Not found**
- **Source:** DataCite API shows no fundingReferences

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Not found in accessible metadata**
- **Note:** Documentation mentions articles available via tutorial.article_path() function, but specific citations not accessible without running the code
- **Source:** Searched DataCite relatedIdentifiers, README, documentation files

### 28. Related Datasets (OPTIONAL)
- **Not found**
- **Note:** Software includes example dataset (SAVIC_Examples.h5) but no published dataset DOI found
- **Source:** Repository search, DataCite API

### 29. Related Software (OPTIONAL)
- **numpy** - Key dependency for numerical operations
- **pandas** - Data manipulation
- **pytables (tables)** - HDF5 file handling
- **xgboost** - Machine learning framework
- **scikit-learn** - Machine learning library
- **wget** - Data downloading
- **urllib3** - URL handling
- **Source:** pyproject.toml dependencies, SoMEF requirements analysis
- **Note:** These are dependencies rather than similar software packages

### 30. Interoperable Software (OPTIONAL)
- **Not found**
- **Note:** No explicit interoperability claims found in documentation
- **Source:** Repository documentation search

### 31. Related Instruments (OPTIONAL)
- **Not found**
- **Note:** SAVIC is a general-purpose plasma instability analysis tool, not instrument-specific
- **Source:** Documentation analysis - software works with VDF data from any source

### 32. Related Observatories (OPTIONAL)
- **Not found**
- **Note:** Software is not mission-specific; it can analyze VDF data from any solar wind mission
- **Source:** Documentation describes general VDF analysis, no specific mission mentioned

### 33. Logo (OPTIONAL)
- **Not found**
- **Note:** No logo file found in repository
- **Source:** Repository file search, PyHC metadata (no logo field)

---

## Metadata Sources Summary

**Priority order applied (per CLAUDE.md guidelines):**
1. **PyHC metadata** - Used for description enhancement, keywords, documentation URL
2. **DataCite/Zenodo APIs** - Used for DOIs, authors with ORCIDs, publisher, dates, version info
3. **SoMEF** - Used for repository metadata, creation date, programming languages
4. **Manual examination** - Used for detailed description, functionality analysis, license verification

**Automated extraction methods completed:**
- ✅ DataCite API (https://doi.org/10.5281/zenodo.8170235)
- ✅ Zenodo API (record 17382178 - latest version)
- ✅ SoMEF (GitHub repository analysis)
- ✅ PyHC registry (projects.yml - package found and analyzed)

**Manual examination completed:**
- ✅ README.md
- ✅ pyproject.toml
- ✅ LICENSE file
- ✅ Documentation files (docs/01-intro.rst, docs/01-purpose.rst, docs/03-functions-tutorial.rst)
- ✅ Git history and tags
- ✅ Source code structure
- ✅ Repository file structure

**MANDATORY fields status:**
- ✅ Code Repository
- ✅ Software Functionality (4 categories identified)
- ✅ Related Region (2 regions identified)
- ✅ Authors (2 authors with ORCIDs)
- ✅ Software Name
- ✅ Description

**RECOMMENDED fields status:**
- ✅ Persistent Identifier
- ✅ Publisher
- ✅ Version (all sub-fields)
- ✅ Programming Language
- ✅ License
- ✅ Input File Formats
- ✅ Output File Formats
- ✅ Operating System
- ✅ CPU Architecture
- ✅ Development Status
- ✅ Documentation
- ⚠️ Reference Publication (not found)

---

## Notes

1. **License discrepancy:** The Zenodo DOI uses CC-BY-4.0 for the deposit metadata, but the actual source code is MIT licensed (as stated in source/LICENSE and pyproject.toml). For the software itself, MIT License is correct.

2. **Author information:** DataCite lists "MihailoMartinovic" as a creator and two contributors (Martinović and Klein) with full details. The contributors appear to be the actual authors, with Martinović as the primary author and Klein as a project member.

3. **Software Functionality:** Based on comprehensive analysis, SAVIC primarily performs:
   - ML/AI-based prediction and classification (primary function)
   - Plasma VDF analysis
   - Instability forecasting
   - Data processing with machine learning

4. **Related Region:** Focuses on interplanetary space (solar wind) with connections to solar environment.

5. **Publication Date:** Using repository creation date (2023-01-24) as the initial publication date, though first DOI version was released 2023-07-20.

6. **Development Status:** Active development evidenced by recent releases (October 2025) and regular updates.

7. **PyHC Package:** SAVIC is a PyHC community package with "Good" ratings for documentation, testing, python3, and license; "Partially met" for community and software_maturity.
