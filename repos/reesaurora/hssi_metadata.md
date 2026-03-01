# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/reesaurora
**Extraction Date:** 2025-12-04

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Concept DOI:** https://doi.org/10.5281/zenodo.595438
**Source:** Zenodo API
**Note:** This is the concept DOI for all versions of the software

### 3. Code Repository (MANDATORY)
**Repository URL:** https://github.com/space-physics/reesaurora
**Source:** PyHC registry, SoMEF, setup.cfg

### 4. Software Functionality (MANDATORY)
**Values:**
- Models and Simulations
- Models and Simulations:Physics-Based
- Data Processing and Analysis
- Data Processing and Analysis:Analysis

**Source:** Manual analysis of code and documentation
**Rationale:** This software is a physics-based model of auroral electron precipitation and ionization processes in Earth's ionosphere. It calculates excitation rates and ionization profiles based on the Rees-Sergienko-Ivanov model. It also performs analysis of atmospheric data using the MSISE-00 model.

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere

**Source:** Manual analysis, PyHC keywords, setup.cfg
**Rationale:** The software models auroral phenomena occurring in Earth's upper atmosphere, specifically the ionosphere and thermosphere regions (altitudes 80-700 km). The model is designed for auroral latitudes (>45° latitude).

### 6. Authors (MANDATORY)

#### Author 1:
- **Authors:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** SciVision, Inc.
  - **Affiliation Identifier:** Not found

**Source:** DataCite API, setup.cfg
**Note:** Author email (scivision@users.noreply.github.com) is available but appears to be a GitHub no-reply address

### 7. Software Name (MANDATORY)
**Name:** reesaurora
**Full Title:** Rees-Sergienko-Ivanov Auroral model
**Source:** PyHC registry, setup.cfg, README.md, SoMEF

### 8. Description (MANDATORY)
**Description:** Rees-Sergienko-Ivanov model of excitation rates, relevant to auroral optical emissions. This physics-based model simulates auroral electron precipitation and ionization processes in Earth's ionosphere. The model is designed for electron energies in the range of 100-10,000 eV and uses the MSISE-00 atmospheric model to generate O, O₂, and N₂ densities. It calculates the ionization profiles and volume emission rates as a function of altitude resulting from primary electron precipitation on the neutral atmospheric background. The model is based on work by Gustavsson and Brandström (AIDA_TOOLS) and implements the approach described in Sergienko and Ivanov (1993).

**Source:** Combination of DataCite API, README.md, setup.cfg, and code analysis

### 9. Concise Description (OPTIONAL)
**Concise Description:** Rees-Sergienko-Ivanov model of auroral excitation rates and ionization profiles for electron precipitation in Earth's ionosphere (100-10,000 eV range).

**Source:** Synthesized from multiple sources

### 10. Publication Date (RECOMMENDED)
**Date:** 2015-06-02
**Source:** Git history (first commit), SoMEF
**Note:** This is the date of initial code creation/publication

### 11. Publisher (RECOMMENDED)

#### Publisher:
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

#### Version Information:
- **Version Number:** v1.0.5
- **Version Date:** 2018-07-30
- **Version Description:** Update selftest, cleanup prereqs. Includes Pep8 compliance, additional self-tests, mypy type checking, and updated MSIS API.
- **Version PID:** https://doi.org/10.5281/zenodo.1323860

**Source:** DataCite API, Zenodo API, SoMEF, setup.cfg, git history
**Note:** Version description synthesized from release notes for v1.0.4 and v1.0.5

### 13. Programming Language (RECOMMENDED)
**Languages:**
- Python 3.x

**Additional Languages (minor components):**
- MATLAB

**Source:** SoMEF, setup.cfg, CI workflow
**Note:** Requires Python >= 3.7. The software primarily uses Python with some MATLAB compatibility code.

### 14. Reference Publication (RECOMMENDED)
**Reference Publication:** Not found
**Note:** The software is based on scientific papers (Rees 1989, Sergienko and Ivanov 1993, Wedlund et al 2013) but no specific DOI for a software paper was found.

### 15. License (RECOMMENDED)

#### License:
- **License:** Apache License 2.0
- **License URI:** https://www.apache.org/licenses/LICENSE-2.0

**Source:** SoMEF (GitHub API), LICENSE.txt file

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Keywords:**
- ionosphere
- aurora
- atmospheric science
- ionosphere_thermosphere_mesosphere
- auroral optical emissions
- electron precipitation
- excitation rates
- physics-based model

**Source:** setup.cfg, PyHC registry, README.md, SoMEF

### 17. Data Sources (OPTIONAL)
**Data Sources:** Not applicable
**Note:** This is a model/simulation tool that generates data rather than retrieving it from external sources. It uses the embedded MSISE-00 atmospheric model for atmospheric density inputs.

### 18. Input File Formats (RECOMMENDED)
**Formats:**
- HDF5

**Source:** Code analysis
**Note:** The software reads HDF5 files containing Sergienko-Ivanov model parameters (data/SergienkoIvanov.h5)

### 19. Output File Formats (RECOMMENDED)
**Formats:**
- HDF5

**Source:** Code analysis (ReesSergienkoIvanov.py:62)
**Note:** Outputs eigenprofile production data in HDF5 format via the writeeigen function from gridaurora package

### 20. Operating System (RECOMMENDED)
**Operating Systems:**
- Linux
- Mac
- Windows
- OS Independent

**Source:** CI workflow (.github/workflows/ci.yml), setup.cfg
**Note:** Tested on ubuntu-latest, macos-latest, and windows-latest in CI. Requires a Fortran compiler (e.g., gfortran).

### 21. CPU Architecture (RECOMMENDED)
**Architecture:** CPU Independent
**Source:** Inference from OS Independent designation and lack of specific architecture requirements

### 22. Related Phenomena (OPTIONAL)
**Phenomena:** Not found in controlled vocabulary
**Note:** The software relates to auroral phenomena including auroral optical emissions and ionospheric ionization, but these specific terms were not found in the standard controlled vocabulary.

### 23. Development Status (RECOMMENDED)
**Status:** Active
**Source:** Inference from setup.cfg (Development Status :: 4 - Beta) and recent repository activity (last updated 2023-01-27)
**Note:** While classified as "Beta" in setup.cfg, the repository shows continued maintenance and the software has reached a stable, usable state.

### 24. Documentation (RECOMMENDED)
**Documentation URL:** https://github.com/space-physics/reesaurora/blob/main/README.md
**Source:** Repository examination
**Note:** Primary documentation is in the README.md file. No separate documentation website was found.

### 25. Funder (OPTIONAL)
**Funder:** Not found
**Note:** No funding information found in repository files, DataCite metadata, or Zenodo record

### 26. Award Title (OPTIONAL)
**Award Title:** Not found
**Award Number:** Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Related Publications:**
No DOIs found, but the following papers are referenced in the code as the scientific basis:

- Rees, M. H. (1989) - Physics and Chemistry of the Upper Atmosphere
- Sergienko, T., and Ivanov, V. E. (1993) "A new approach to calculate the excitation of atmospheric gases by auroral electron impact" Annales Geophysicae
- Wedlund et al. (2013) "Electron Energy Spectra and Auroral Arcs" Journal of Geophysical Research

**Source:** Code comments in ReesSergienkoIvanov.py and __init__.py

### 28. Related Datasets (OPTIONAL)
**Related Datasets:** Not found
**Note:** The software generates its own data and uses the MSISE-00 atmospheric model, but no specific dataset DOIs were identified.

### 29. Related Software (OPTIONAL)
**Related Software:**

1. **msise00** - MSIS atmospheric model (required dependency)
   - Repository: https://github.com/space-physics/msise00
   - Note: Used to generate atmospheric densities (O, O₂, N₂)

2. **gridaurora** - Aurora grid utilities (required dependency)
   - Note: Provides altitude grid generation and data output functions

3. **AIDA_TOOLS** - Original implementation
   - Repository: https://github.com/scivision/AIDA-tools
   - Note: This software is inspired by/based upon the AIDA_TOOLS package by Gustavsson and Brandström

**Source:** setup.cfg dependencies, README.md

### 30. Interoperable Software (OPTIONAL)
**Interoperable Software:**
- numpy
- scipy
- xarray
- matplotlib
- seaborn

**Source:** setup.cfg install_requires and extras_require
**Note:** These are standard scientific Python packages that the software uses and demonstrates interoperability with

### 31. Related Instruments (OPTIONAL)
**Instruments:** Not found
**Note:** While the software models auroral phenomena that could be observed by various instruments, no specific instruments are mentioned in the documentation

### 32. Related Observatories (OPTIONAL)
**Observatories:** Not found
**Note:** The software is a general-purpose model not specifically designed for a particular observatory or mission

### 33. Logo (OPTIONAL)
**Logo URL:** Not found

---

## PyHC Package Information

**PyHC Status:** Unevaluated
**PyHC Package Name:** ReesAurora
**PyHC Contact:** Michael Hirsch
**PyHC Keywords:** ionosphere_thermosphere_mesosphere, specific

**Source:** PyHC unevaluated packages registry (projects_unevaluated.yml)

---

## Additional Technical Information

### Dependencies:
**Required:**
- python-dateutil
- numpy
- scipy
- xarray
- msise00
- gridaurora

**Optional (for plotting):**
- matplotlib
- seaborn

**Build Requirements:**
- Fortran compiler (e.g., gfortran)
- setuptools
- wheel

### Installation:
```bash
pip install -e .
```
Requires a Fortran compiler to build.

### Energy Range:
Model is designed for electron energies of 100-10,000 eV

### Altitude Range:
Operates on altitudes from ~80 km to 700 km (electron source assumed at 700 km)

### Geographic Scope:
Intended for auroral latitudes (|latitude| > 45°)

---

## Metadata Sources Summary

1. **DataCite API** (10.5281/zenodo.595438): Basic metadata, author, publisher, dates
2. **Zenodo API** (record 1323860): Concept DOI, version DOI, license information
3. **SoMEF** (automated repository analysis): Programming languages, keywords, repository structure
4. **PyHC Unevaluated Registry**: Package name, contact, classification keywords
5. **Manual Repository Examination**:
   - README.md: Full title, description, usage information
   - setup.cfg: Detailed metadata including version, author, dependencies, classifiers
   - LICENSE.txt: License text (Apache 2.0)
   - .github/workflows/ci.yml: Operating system support
   - Source code: File formats, functionality analysis
   - Git history: Creation date, version dates

---

## Notes

- The repository was originally under the scivision organization but has moved to space-physics organization
- Both URLs redirect appropriately: https://github.com/scivision/reesaurora → https://github.com/space-physics/reesaurora
- The software implements a parameter-fit model from the early 1990s era, optimized for computational efficiency on older hardware
- Modern physics-based models are more advanced, but this model remains useful for quick calculations in the 100-10,000 eV range
- Author contact email uses GitHub's no-reply address; real contact information not publicly available
