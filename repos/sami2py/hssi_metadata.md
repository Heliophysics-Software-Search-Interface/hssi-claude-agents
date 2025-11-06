# HSSI Metadata Extraction Results

**Repository:** https://github.com/sami2py/sami2py
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.2875799
**Source:** DataCite API (concept DOI for all versions)

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/sami2py/sami2py
**Source:** Repository URL, confirmed in DataCite and SoMEF

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion
- Data Visualization
- Data Visualization:Line Plots
- Models and Simulations
- Models and Simulations:Physics-Based
- Models and Simulations:Theory

**Source:** Manual analysis of README and documentation. SAMI2 is a physics-based ionospheric model that solves chemical and dynamical evolution equations. Sami2py provides functionality to run the model, process outputs, archive data, load/retrieve archived data, convert output to netCDF format, and visualize results through line plots.

### 5. Related Region (MANDATORY)
**Value:** Earth Atmosphere
**Source:** PyHC keywords (ionosphere_thermosphere_mesosphere) and README description indicating ionospheric modeling

### 6. Authors (MANDATORY)

**Author 1:**
- **Author Name:** Jeff Klenzing
- **Author Identifier:** https://orcid.org/0000-0001-8321-6074
- **Affiliation:**
  - **Organization:** Goddard Space Flight Center
  - **Affiliation Identifier:** Not found

**Author 2:**
- **Author Name:** Jonathon M. Smith
- **Author Identifier:** https://orcid.org/0000-0002-8191-4765
- **Affiliation:**
  - **Organization:** Catholic University of America, Goddard Space Flight Center
  - **Affiliation Identifier:** Not found

**Author 3:**
- **Author Name:** Angeline G. Burrell
- **Author Identifier:** https://orcid.org/0000-0001-8875-9326
- **Affiliation:**
  - **Organization:** U.S. Naval Research Laboratory
  - **Affiliation Identifier:** Not found

**Author 4:**
- **Author Name:** Reika Kitano
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** American University
  - **Affiliation Identifier:** Not found

**Author 5:**
- **Author Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** Not found

**Author 6:**
- **Author Name:** zzyztyy
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** DataCite API

### 7. Software Name (MANDATORY)
**Value:** sami2py
**Source:** DataCite API, GitHub repository, setup.cfg

### 8. Description (MANDATORY)
**Value:** Sami2py is a python module that runs the SAMI2 model, archives the output, and loads the resulting modeled values. SAMI2 is a model developed by the Naval Research Laboratory to simulate the motions of plasma in a 2D ionospheric environment along a dipole magnetic field. SAMI2 solves for the chemical and dynamical evolution of seven ion species in this environment (H+, He+, N+, O+, N2+, NO+, and O2+). The implementation used here includes several added options to the original release of SAMI2, including the ability to scale the neutral atmosphere in which the ions form through direct modification of the exospheric neutral temperature for extreme solar minimum conditions, and the ability to input custom ExB drifts as a Fourier series.

**Source:** README.rst, enhanced from DataCite API description

### 9. Concise Description (OPTIONAL)
**Value:** Python wrapper to run, read, and plot the SAMI2 ionospheric model

**Source:** SoMEF (GitHub API description)

### 10. Publication Date (RECOMMENDED)
**Value:** 2022-11-03
**Source:** Zenodo API (publication date for latest version v0.3.0)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API

### 12. Version (RECOMMENDED)

**Version Number:** v0.3.0
**Version Date:** 2022-11-03
**Version Description:** Updates code standards and improves testing / os support. Maintenance includes implementation of flake8-docstring and hacking packages to lint code, update of docstring standards, updated NEP 29 compliance in CI tests, addition of CI tests for Mac Os X, fixed a bug in Windows CI environment in usage of mingw-64, deprecated camel case keys in run_model, removed deprecated plotting functions (moved to sami2py_vis), improved discussion of fortran compiler requirements in docs, and removed deprecated pytest functions.
**Version PID:** https://doi.org/10.5281/zenodo.7277517

**Source:** Zenodo API, Git tags, CHANGELOG.md

### 13. Programming Language (RECOMMENDED)
**Values:**
- Fortran77
- Fortran90
- Python 3.x

**Source:** SoMEF (GitHub API languages - Fortran is the primary language for the model itself, Python is the wrapper), setup.cfg (Python 3.7, 3.8, 3.9 listed)

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.1029/2000JA000035

**Note:** This is the foundational SAMI2 model paper by Huba, J.D., G. Joyce, and J.A. Fedder (2000), "Sami2 is Another Model of the Ionosphere (SAMI2): A new low‐latitude ionosphere model," J. Geophys. Res., 105, Pages 23035-23053.

**Source:** README.rst citation section

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

**Source:** SoMEF (GitHub API), License.md file

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- ionosphere
- ionosphere-modeling
- python
- ionosphere_thermosphere_mesosphere
- SAMI2

**Source:** SoMEF (GitHub topics), PyHC metadata, setup.cfg

### 17. Data Sources (OPTIONAL)
**Value:** Not found

**Note:** SAMI2py is a model that generates data rather than consuming external data sources. It uses internal neutral atmosphere and geophysical models.

### 18. Input File Formats (RECOMMENDED)
**Value:** ascii

**Note:** The model accepts text-based input files for configuration (namelist files, ExB drift coefficients). Source: Manual examination of setup.py and CHANGELOG.md

### 19. Output File Formats (RECOMMENDED)
**Values:**
- netCDF3/4
- Other (binary unformatted Fortran output)

**Source:** CHANGELOG.md mentions netCDF export capability added in v0.2.2, and unformatted binary files are the native SAMI2 output format

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Source:** CI workflows (.github/workflows/main.yml tests on ubuntu-latest, macos-latest, windows-latest), setup.cfg classifiers

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Note:** Python/Fortran code can run on standard CPU architectures. No specific architecture requirements found.

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found

**Note:** While the software models ionospheric plasma dynamics, specific phenomena classifications were not explicitly listed in the repository.

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** Repository shows recent activity (last updated 2025-05-21 per SoMEF), active maintenance, and PyHC status of "Partially met" for software maturity indicates ongoing development

### 24. Documentation (RECOMMENDED)
**Value:** https://sami2py.readthedocs.io

**Source:** PyHC metadata, README.rst, SoMEF

### 25. Funder (OPTIONAL)
**Value:** Not found

**Note:** No funding information found in DataCite API or repository files

### 26. Award Title (OPTIONAL)
**Value:** Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Publication 1:** https://doi.org/10.1029/2010GL043671
Emmert, J.T., J.L. Lean, and J.M. Picone (2010), "Record‐low thermospheric density during the 2008 solar minimum," Geophys. Res. Lett., 37.

**Publication 2:** https://doi.org/10.5194/angeo-31-2147-2013
Klenzing, J., A. G. Burrell, R. A. Heelis, J. D. Huba, R. Pfaff, and F. Simões (2013), "Exploring the role of ionospheric drivers during the extreme solar minimum of 2008," Ann. Geophys., 31, 2147-2156.

**Source:** README.rst references section

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Note:** SAMI2py generates modeled data rather than analyzing existing datasets

### 29. Related Software (OPTIONAL)
**Values:**
- numpy (dependency)
- pandas (dependency)
- scipy (dependency)
- xarray (dependency)
- netCDF4 (dependency)

**Note:** These are key dependencies listed in requirements.txt

**Source:** requirements.txt, setup.cfg

### 30. Interoperable Software (OPTIONAL)
**Value:** sami2py_vis (companion visualization package)

**Note:** CHANGELOG.md indicates plotting functions were moved to sami2py_vis package, suggesting interoperability

**Source:** CHANGELOG.md

### 31. Related Instruments (OPTIONAL)
**Value:** Not found

**Note:** SAMI2py is a model/simulation tool, not designed for specific instrument data

### 32. Related Observatories (OPTIONAL)
**Value:** Not found

**Note:** While SAMI2py models the ionosphere and could be used to support various missions, no specific observatories are explicitly listed as targets

### 33. Logo (OPTIONAL)
**Value:** Not found

**Note:** No logo URL found in PyHC metadata or repository

---

## Summary of Sources

This metadata extraction utilized the following sources in priority order:

1. **PyHC Community Registry** - Most reliable, manually curated metadata
2. **DataCite API** - Official DOI metadata for authors, affiliations, citations
3. **Zenodo API** - Version-specific metadata, publication dates
4. **SoMEF** - Automated extraction from repository (programming languages, keywords, dates)
5. **Manual Repository Examination** - README.rst, License.md, setup.cfg, CHANGELOG.md, CI workflows

## Notes

- **Contact Information:** Primary contact is Jeff Klenzing (jeffrey.klenzing@nasa.gov per setup.cfg)
- **Code of Conduct:** Present (CODE_OF_CONDUCT.md follows Contributor Covenant v1.4)
- **Contributing Guidelines:** Present (CONTRIBUTING.md)
- **Fortran Compiler Required:** The software requires GFortran or compatible Fortran compiler for installation
- **Citation Requirement:** Authors request citation of both the original SAMI2 paper (Huba et al. 2000) and the software package DOI
- **Acknowledgment Text:** "This work uses the SAMI2 ionosphere model written and developed by the Naval Research Laboratory."
