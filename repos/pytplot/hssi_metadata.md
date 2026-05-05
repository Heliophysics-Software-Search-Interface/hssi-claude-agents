# HSSI Metadata Extraction Results

**Repository:** https://github.com/MAVENSDC/pytplot
**Extraction Date:** 2025-12-02

**Important Note:** PyTplot is being integrated into PySPEDAS starting in PySPEDAS 2.0, after which it will no longer be maintained as a separate package. The `matplotlib-backend` branch (last updated 2025-07-25) represents an alternative plotting backend using Matplotlib.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.3601517
- **Source:** Zenodo concept DOI (found in README badge and DataCite API)

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/MAVENSDC/pytplot
- **Source:** Repository URL

### 4. Software Functionality (MANDATORY)
**Selected Values:**
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Spectrogram
- Data Visualization:Web-Based
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Time Series Analysis

**Justification:** PyTplot is primarily a data visualization package that creates interactive 2D plots of time series data, with support for line plots and spectrograms. It exports to web-based HTML (via Bokeh) and PNG formats. It also provides data processing capabilities including time series analysis (interpolation, resampling, power spectra), data manipulation (add, subtract, multiply, divide operations via tplot_math), data access from CDF and NetCDF files, and export to ASCII format.

**Sources:**
- README: "plots time series data" with "interactive tools"
- PyHC registry: "Based on IDL tplot, plots and manipulates time series data"
- Code analysis: cdf_to_tplot, netcdf_to_tplot, tplot_ascii exporters
- tplot_math module: resample, tinterp, pwr_spec, degap functions
- Dependencies: bokeh (web-based plotting), matplotlib (alternative backend), pyqtgraph (Qt plotting)

### 5. Related Region (MANDATORY)
**Selected Values:**
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space
- Solar Environment

**Justification:** PyTplot is designed for heliophysics and space physics research across multiple regions. It was developed by the MAVEN Science Data Center for Mars/interplanetary data, and the PyHC registry explicitly lists keywords "solar", "magnetosphere", and "ionosphere_thermosphere_mesosphere" (Earth Atmosphere). The package is used for analyzing data from missions spanning all these regions.

**Sources:**
- PyHC keywords: ["solar","magnetosphere","ionosphere_thermosphere_mesosphere","general"]
- MAVEN SDC affiliation (interplanetary/Mars mission)
- General-purpose tplot tool used across heliophysics domains

### 6. Authors (MANDATORY)

#### Author 1:
- **Authors:** MAVEN SDC
- **Author Identifier:** Not found
- **Affiliation > Organization:** Laboratory for Atmospheric and Space Physics
- **Affiliation Identifier:** Not found

#### Author 2:
- **Authors:** Bryan Harter
- **Author Identifier:** Not found
- **Affiliation > Organization:** Laboratory for Atmospheric and Space Physics
- **Affiliation Identifier:** Not found

#### Author 3:
- **Authors:** Elysia Lucas
- **Author Identifier:** Not found
- **Affiliation:** Not found

#### Author 4:
- **Authors:** supervised
- **Author Identifier:** Not found
- **Affiliation > Organization:** UCLA Institute of Geophysics and Planetary Physics
- **Affiliation Identifier:** Not found

#### Author 5:
- **Authors:** jibarnum
- **Author Identifier:** Not found
- **Affiliation:** Not found

#### Author 6:
- **Authors:** Nick H
- **Author Identifier:** Not found
- **Affiliation:** Not found

#### Author 7:
- **Authors:** nikos15
- **Author Identifier:** Not found
- **Affiliation:** Not found

#### Author 8:
- **Authors:** Takanobu Amano
- **Author Identifier:** Not found
- **Affiliation > Organization:** The University of Tokyo
- **Affiliation Identifier:** Not found

#### Author 9:
- **Authors:** X. N. Chu
- **Author Identifier:** Not found
- **Affiliation > Organization:** LASP
- **Affiliation Identifier:** Not found

**Source:** DataCite API metadata for DOI 10.5281/zenodo.3601517

**Note:** Author names from GitHub commits are often usernames rather than full names. ORCIDs were not found in the repository metadata.

### 7. Software Name (MANDATORY)
- **Value:** PyTplot
- **Source:** Repository name, setup.cfg metadata, and PyHC registry

### 8. Description (MANDATORY)
- **Value:** PyTplot is a Python package that replicates the functionality of IDL's tplot libraries for plotting and manipulating time series data. It creates interactive visualizations with user tools such as zooming and panning, and can export plots as standalone HTML files (retaining interactivity via Bokeh) or static PNG images. PyTplot can be used in Python scripts, IPython, or Jupyter notebooks. The package provides comprehensive support for time series analysis operations including interpolation, resampling, power spectra calculation, and mathematical operations on time series variables.
- **Sources:**
  - README.md: "aims to mimic the functionality of the IDL 'tplot' libraries"
  - PyHC registry: "Based on IDL tplot, plots and manipulates time series data"
  - DataCite API: "A python version of the IDL tplot libraries"
  - Analysis of tplot_math module functionality

### 9. Concise Description (OPTIONAL)
- **Value:** Python implementation of IDL tplot libraries for interactive time series visualization and analysis in heliophysics research.
- **Source:** Synthesized from README and repository description

### 10. Publication Date (RECOMMENDED)
- **Value:** 2020-01-08
- **Source:** DataCite API "created" field (first version release date)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API and Zenodo DOI

### 12. Version (RECOMMENDED)
- **Version Number:** v1.7.28
- **Version Date:** 2021-09-15
- **Version Description:** Bumping version to get metadata updates into PyPI
- **Version PID:** https://doi.org/10.5281/zenodo.5510606
- **Sources:**
  - Setup.cfg (version number)
  - DataCite API (date and description)
  - Zenodo API (version DOI)

**Note:** This is the latest version found in Zenodo. The master branch in the repository may have newer unreleased versions. The matplotlib-backend branch was last updated 2025-07-25.

### 13. Programming Language (RECOMMENDED)
**Selected Values:**
- Python 3.x

**Source:**
- setup.cfg: "Programming Language :: Python :: 3.7", "python_requires = >= 3.6"
- Repository is entirely Python-based

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found
- **Note:** No reference publication (e.g., JOSS paper) was found in the repository, README, or DataCite metadata.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT
- **Sources:**
  - LICENSE file: "MIT License, Copyright (c) 2018 MAVEN SDC"
  - setup.cfg: license_file = LICENSE
  - DataCite API: "Open Access"

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- tplot
- maven
- lasp
- IDL
- spedas
- solar
- magnetosphere
- ionosphere_thermosphere_mesosphere
- time series
- data visualization
- heliophysics
- space physics
- bokeh
- interactive plotting

**Sources:**
- setup.cfg keywords
- PyHC registry keywords
- Inferred from package functionality and domain

### 17. Data Sources (OPTIONAL)
**Selected Values:**
- Other

**Note:** PyTplot reads data from local CDF and NetCDF files. It does not directly connect to data services like CDAWeb or HAPI, but is often used in conjunction with data retrieval packages like PySPEDAS that fetch data from various sources.

**Source:** Code analysis (cdf_to_tplot.py, netcdf_to_tplot.py)

### 18. Input File Formats (RECOMMENDED)
**Selected Values:**
- CDF
- netCDF3/4
- Other

**Justification:** The package includes explicit importers for CDF (via cdflib dependency) and NetCDF files. Additional formats may be supported through xarray and pandas integration.

**Sources:**
- pytplot/importers/cdf_to_tplot.py
- pytplot/importers/netcdf_to_tplot.py
- Dependencies: cdflib, xarray
- Test files: test_cdf_to_tplot.py, test_netcdf_to_tplot.py

### 19. Output File Formats (RECOMMENDED)
**Selected Values:**
- ascii
- Other

**Justification:** PyTplot can export data to ASCII format and plots to HTML (via Bokeh) and PNG (via Qt/Matplotlib backends).

**Sources:**
- pytplot/exporters/tplot_ascii.py
- README: "exported as standalone HTML files" or "static PNG files"
- Dependencies: bokeh (HTML export), matplotlib/pyqtgraph (image export)

### 20. Operating System (RECOMMENDED)
**Selected Values:**
- Operating System Independent

**Source:** setup.cfg classifier: "Operating System :: OS Independent"

### 21. CPU Architecture (RECOMMENDED)
**Selected Values:**
- CPU Independent

**Note:** As a pure Python package with standard numerical libraries, PyTplot should run on any architecture supported by its dependencies (numpy, scipy, etc.).

**Source:** Inferred from Python-only implementation and dependencies

### 22. Related Phenomena (OPTIONAL)
- **Value:** Not found
- **Note:** The package is domain-agnostic for plotting time series data. Specific phenomena would depend on the datasets being analyzed.

### 23. Development Status (RECOMMENDED)
- **Value:** Active
- **Justification:** The matplotlib-backend branch was updated recently (2025-07-25), indicating active development. However, note that the project is transitioning into PySPEDAS 2.0 and may be deprecated as a standalone package in the future.
- **Sources:**
  - PyHC registry: software_maturity = "Good"
  - setup.cfg: "Development Status :: 5 - Production/Stable"
  - Git activity: Recent commits on matplotlib-backend branch
  - User note: "PyTplot is being folded into PySPEDAS starting in PySPEDAS 2.0"

### 24. Documentation (RECOMMENDED)
- **Value:** https://pytplot.readthedocs.io/en/latest/
- **Sources:**
  - README.md: "Full Documentation here: https://pytplot.readthedocs.io/en/latest/"
  - PyHC registry docs field
  - setup.cfg URL field

### 25. Funder (OPTIONAL)
- **Value:** Not found
- **Note:** No funder information was found in the repository metadata, README, or DataCite API.

### 26. Award Title (OPTIONAL)
- **Value:** Not found
- **Note:** No award information was found in the repository metadata.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Value:** Not found
- **Note:** No related publications were found in the DataCite metadata or repository.

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found
- **Note:** PyTplot is a general-purpose tool that can work with any time series dataset in supported formats. No specific dataset DOIs are associated with the software itself.

### 29. Related Software (OPTIONAL)

**Related Software:**
1. **PySPEDAS** - https://github.com/spedas/pyspedas
   - Note: PyTplot is being integrated into PySPEDAS 2.0. PySPEDAS uses PyTplot for visualization.

2. **cdflib** - https://github.com/MAVENSDC/cdflib
   - Note: Dependency for reading CDF files. Developed by the same team (MAVENSDC).

3. **IDL tplot** - (Commercial software, no DOI)
   - Note: PyTplot is designed to replicate IDL tplot functionality in Python.

**Sources:**
- setup.cfg dependencies
- README mentions IDL tplot as inspiration
- User note about PySPEDAS integration
- PyHC registry (cdflib is also a PyHC package)

### 30. Interoperable Software (OPTIONAL)

**Interoperable Software:**
1. **PySPEDAS** - https://github.com/spedas/pyspedas
   - Note: PySPEDAS uses PyTplot for data visualization and they work together seamlessly.

2. **pysat** - https://github.com/pysat/pysat
   - Note: Both are PyHC packages commonly used together in heliophysics workflows.

**Sources:**
- PyHC ecosystem (both are PyHC community packages)
- setup.cfg keywords include "spedas"
- Common usage patterns in heliophysics community

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** Not found (general-purpose tool)
- **Note:** PyTplot is a general-purpose visualization tool not tied to specific instruments. However, it is heavily used with MAVEN mission data given its origin at the MAVEN SDC.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** MAVEN (Mars Atmosphere and Volatile EvolutioN)
- **Note:** PyTplot was developed by the MAVEN Science Data Center and is commonly used for MAVEN data, though it is a general-purpose tool.
- **Source:** Repository ownership (MAVENSDC), author affiliations, and setup.cfg keywords

### 33. Logo (OPTIONAL)
- **Value:** https://avatars3.githubusercontent.com/u/22352442?s=460&v=4
- **Source:** PyHC registry logo field
- **Note:** This is the MAVENSDC GitHub organization avatar

---

## Metadata Sources Summary

1. **DataCite API** (`https://api.datacite.org/dois/10.5281/zenodo.3601517`):
   - Authors and affiliations
   - Title, description, publication date
   - Publisher, license
   - Version information
   - Related identifiers

2. **Zenodo** (DOI badge in README):
   - Concept DOI: 10.5281/zenodo.3601517
   - Version DOI: 10.5281/zenodo.5510606

3. **PyHC Community Registry** (`projects.yml`):
   - Documentation URL
   - Description
   - Keywords (domain-specific)
   - Quality ratings
   - Logo
   - Contact information

4. **Repository Files**:
   - **setup.cfg**: Version, author, email, keywords, dependencies, Python version, classifiers
   - **LICENSE**: MIT License, copyright holder
   - **README.md**: Description, features, documentation links, contact
   - **Git history**: Version tags, recent activity
   - **Source code**: File format support (CDF, NetCDF, ASCII), functionality analysis

5. **SoMEF Output**:
   - Limited success due to errors during header extraction
   - Confirmed programming language and basic metadata

---

## Verification Notes

### Completeness
- ✅ All 33 HSSI form fields have been addressed
- ✅ Mandatory fields all have values
- ✅ Most recommended fields have values
- ⚠️ Some optional fields lack data (funders, awards, phenomena, instruments)

### Correctness
- ✅ DOI verified via Zenodo badge and DataCite API
- ✅ Repository URL confirmed
- ✅ License verified in LICENSE file
- ✅ Programming language confirmed in setup.cfg
- ✅ Version information cross-checked between setup.cfg and Zenodo
- ✅ Documentation URL verified as accessible

### Exhaustiveness
- ✅ Software Functionality: Comprehensively analyzed through code inspection, README, and dependencies
  - Primary: Data visualization (2D, line plots, spectrograms, web-based)
  - Secondary: Data processing (time series analysis, format conversion, data access)
- ✅ Related Region: All four relevant regions identified based on PyHC keywords and domain knowledge
  - Earth Atmosphere (ionosphere/thermosphere/mesosphere)
  - Earth Magnetosphere
  - Interplanetary Space (MAVEN mission context)
  - Solar Environment
- ✅ Authors: All 9 authors from Zenodo metadata included
- ✅ Keywords: Comprehensive list from multiple sources

### Special Considerations
- **Deprecation Notice**: PyTplot is being integrated into PySPEDAS 2.0, which should be noted in any submission
- **matplotlib-backend Branch**: Alternative plotting backend exists, last updated 2025-07-25
- **PyHC Status**: Community package with "Good" ratings for most categories, "Requires improvement" for community engagement
- **Missing ORCIDs**: No ORCID identifiers found for any authors
- **Missing Funder/Award Info**: No funding acknowledgments found in standard locations

---

## Extraction Timestamp
**Generated:** 2025-12-02
**Extractor:** HSSI Metadata Extractor (AI Agent)
**Repository Commit:** master branch (as of clone date)
**Alternative Branch Examined:** matplotlib-backend (last commit 2025-07-25)
