# HSSI Metadata Extraction Results

**Repository:** https://github.com/JHUAPL/kaipy
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Concept DOI:** https://doi.org/10.5281/zenodo.15801040

**Source:** User-provided and confirmed via Zenodo API

### 3. Code Repository (MANDATORY)
**Repository URL:** https://github.com/JHUAPL/kaipy

**Source:** User-provided, DataCite API, SoMEF

### 4. Software Functionality (MANDATORY)
**Selected Values:**
- Data Processing and Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Field-line Tracing
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Movies
- Models and Simulations
- Models and Simulations:Physics-Based
- Models and Simulations:MHD
- Models and Simulations:Field-line Tracing

**Source:** Manual examination of repository structure, scripts (setup.py showing scripts for data access via CDAWeb/HAPI, satellite comparison tools, visualization scripts for 2D plots and movies, post-processing tools, field-line tracing genXLine script), PyHC keywords (2D_graphics, plotting, data_analysis), and description indicating it's for "analysis and visualization of simulation results" from MHD models like MAGE and GAMERA.

**Justification:**
- Data access functionality evident from dependencies (cdasws, pyspedas, gfz-api-client, supermag-api) and scripts
- Analysis tools for satellite data comparison (helioSatComp, msphSatComp, rbspSCcomp, supermag_analysis)
- Extensive visualization capabilities with 2D plotting scripts (*pic scripts), movie generation (*Vid, heliomovie scripts)
- Post-processing tools for MHD simulation outputs (embiggen*, genXDMF, genXLine for field-line tracing)
- Supports physics-based MHD models (MAGE, GAMERA, RCM as documented)

### 5. Related Region (MANDATORY)
**Selected Values:**
- Earth Magnetosphere
- Interplanetary Space

**Source:** Manual examination of code structure (RCM - Ring Current Model, GAMERA magnetosphere model, solar wind modules), README description mentioning "planetary magnetospheres and the solar wind", PyHC keywords ("geospace"), and satellite comparison scripts for magnetospheric missions (RBSP/Van Allen Probes).

**Justification:**
- Primary focus on Earth's magnetosphere (RCM, GAMERA models, RBSP comparison tools, magnetosphere-specific modules)
- Solar wind and heliospheric environments (solarWind module, gamhelio module, helio* scripts)
- Software explicitly designed for MAGE model which simulates magnetosphere-ionosphere-thermosphere coupling

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Michael Wiltberger
- **Affiliation:** National Center for Atmospheric Research (NCAR)
- **Source:** DataCite API, PyHC registry (contact), setup.py author_email

**Author 2:**
- **Name:** Eric Winter
- **Affiliation:** Johns Hopkins University Applied Physics Laboratory
- **Source:** DataCite API, pyproject.toml

**Author 3:**
- **Name:** Nikhil Rao
- **Affiliation:** Not found
- **Source:** DataCite API

**Author 4:**
- **Name:** Anthony Sciola
- **Affiliation:** Not found
- **Source:** DataCite API

**Author 5:**
- **Name:** vmerkin
- **Affiliation:** Not found
- **Source:** DataCite API

**Author 6:**
- **Name:** Jeff
- **Affiliation:** Not found
- **Source:** DataCite API

**Author 7:**
- **Name:** phamkh
- **Affiliation:** Not found
- **Source:** DataCite API

**Author 8:**
- **Name:** atmichael18
- **Affiliation:** Not found
- **Source:** DataCite API

**Author 9:**
- **Name:** Shanshan Bao
- **Affiliation:** Rice University
- **Source:** DataCite API

**Author 10:**
- **Name:** ksorat
- **Affiliation:** Not found
- **Source:** DataCite API

**Author 11:**
- **Name:** Andrew McCubbin
- **Affiliation:** Johns Hopkins University Applied Physics Laboratory (JHU APL)
- **Source:** DataCite API

**Author 12:**
- **Name:** Darren De Zeeuw
- **Affiliation:** NASA Goddard Space Flight Center (NASA GSFC)
- **Source:** DataCite API

**Note:** Several author names appear to be GitHub usernames. ORCIDs not found in available metadata.

### 7. Software Name (MANDATORY)
**Name:** kaipy

**Source:** DataCite API, SoMEF, PyHC registry, setup.py

### 8. Description (MANDATORY)
**Description:** Kaipy is a Python package for analysis and visualization of simulation results from a scientific software package Kaiju. Kaiju includes the Multiscale Atmosphere-Geospace Environment (MAGE) model developed by the NASA DRIVE Center for Geospace Storms as well as other scientific software for simulation of heliospheric environments such as planetary magnetospheres and the solar wind.

**Source:** DataCite API, Zenodo API, SoMEF, PyHC registry, README.md

### 9. Concise Description (OPTIONAL)
**Concise Description:** Python package for analysis and visualization of Kaiju simulation results (MAGE model and other heliospheric environment models).

**Source:** Derived from full description

### 10. Publication Date (RECOMMENDED)
**Date:** 2025-09-30

**Source:** DataCite API (publication date for version 1.1.3)

**Note:** Repository creation date from SoMEF: 2025-06-11

### 11. Publisher (RECOMMENDED)
**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

**Version Number:** 1.1.3

**Version Date:** 2025-09-30

**Version Description:** Enable rotation of the colorbar for GAMERA slice plots. New contributor: @darrendezeeuw made their first contribution.

**Version PID:** https://doi.org/10.5281/zenodo.17236774

**Source:** DataCite API, Zenodo API, SoMEF, setup.py, pyproject.toml

**Note:** The concept DOI (10.5281/zenodo.15801040) represents all versions, while the version PID represents the specific 1.1.3 release.

### 13. Programming Language (RECOMMENDED)
**Languages:**
- Python 3.x

**Source:** SoMEF (GitHub API shows Python as primary language with 1,371,975 bytes), setup.py (requires Python >=3.9,<3.13), PyHC registry

**Note:** Repository also contains Jupyter Notebook (11,869 bytes) and Shell scripts (8,120 bytes) but Python is the primary language.

### 14. Reference Publication (RECOMMENDED)
**Reference Publication:** Not found

**Source:** Searched DataCite API relatedIdentifiers, Zenodo API, README.md, and repository - no reference publication found.

### 15. License (RECOMMENDED)
**License:**
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause

**Source:** DataCite API, Zenodo API, SoMEF, LICENSE.md

**Note:** License file shows copyright holders: Johns Hopkins University Applied Physics Laboratory, US National Science Foundation National Center for Atmospheric Research, and Rice University (all 2023).

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Keywords:**
- CGS (from pyproject.toml)
- MAGE (from pyproject.toml)
- KAIJU (from pyproject.toml)
- geospace (from PyHC)
- 2D_graphics (from PyHC)
- plotting (from PyHC)
- hdf5 (from PyHC)
- local (from PyHC)
- data_analysis (from PyHC)
- specific (from PyHC)
- magnetosphere
- solar wind
- heliosphere
- simulation

**Source:** pyproject.toml, PyHC registry, manual analysis of software domain

### 17. Data Sources (OPTIONAL)
**Data Sources:**
- CDAWeb
- HAPI
- Observatory/Mission-specific

**Source:** Dependencies in requirements.txt (cdasws for CDAWeb/HAPI access, pyspedas for mission data, gfz-api-client, supermag-api for magnetometer data)

### 18. Input File Formats (RECOMMENDED)
**Formats:**
- HDF5
- CDF
- ascii
- Other

**Source:** Dependencies (h5py for HDF5, cdasws/pyspedas/spacepy for CDF), setup.py package_data showing various .txt and .dat files, script names suggesting multiple input formats

### 19. Output File Formats (RECOMMENDED)
**Formats:**
- HDF5
- Other (XDMF for visualization)

**Source:** Dependencies (h5py), scripts (genXDMF, slimh5 for HDF5 output, XDMF generation for ParaView visualization)

### 20. Operating System (RECOMMENDED)
**Operating Systems:**
- OS Independent

**Source:** Pure Python package with no OS-specific dependencies. setup.py classifiers don't specify OS restrictions. Package should work on any platform supporting Python 3.9-3.12.

**Note:** Some dependencies (cartopy, spacepy) may have OS-specific installation requirements, but kaipy itself is OS-independent.

### 21. CPU Architecture (RECOMMENDED)
**CPU Architecture:**
- CPU Independent

**Source:** Pure Python package with no architecture-specific requirements

### 22. Related Phenomena (OPTIONAL)
**Phenomena:**
- Not explicitly specified in available metadata

**Source:** While the software relates to magnetospheric and solar wind phenomena, specific controlled vocabulary terms were not found in the codebase or documentation.

### 23. Development Status (RECOMMENDED)
**Status:** Active

**Source:** SoMEF repository status, PyHC quality rating (software_maturity: Good), recent release (v1.1.3 on 2025-09-30), active commits (last updated 2025-09-30 per SoMEF)

**Note:** PyHC evaluates this package with "Good" software maturity, indicating stable, usable state with active development.

### 24. Documentation (RECOMMENDED)
**Documentation URL:** https://kaipy-docs.readthedocs.io/en/latest/

**Source:** README.md, SoMEF, PyHC registry

**Note:** Documentation is hosted on Read the Docs with Sphinx-based documentation (evident from sphinx-rtd-theme dependency).

### 25. Funder (OPTIONAL)
**Funders:** Not found

**Source:** Searched DataCite API fundingReferences and Zenodo API - no funders listed

**Note:** The software is developed by NASA DRIVE Center for Geospace Storms, but specific funding information not provided in metadata.

### 26. Award Title (OPTIONAL)
**Awards:** Not found

**Source:** Searched DataCite API fundingReferences and Zenodo API - no award information found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Publications:** Not found

**Source:** Searched DataCite API relatedIdentifiers for publications - none found

### 28. Related Datasets (OPTIONAL)
**Datasets:** Not found

**Source:** Searched DataCite API relatedIdentifiers - no datasets found

**Note:** Software accesses various mission datasets (CDAWeb, SuperMAG, GFZ) but no specific dataset DOIs are listed in the metadata.

### 29. Related Software (OPTIONAL)
**Related Software:**
- pyspedas (dependency)
- spacepy (dependency)
- sunpy (dependency)
- astropy (dependency)
- cartopy (dependency)

**Source:** requirements.txt, setup.py dependencies

**Note:** These are important PyHC community packages that kaipy depends on and interoperates with.

### 30. Interoperable Software (OPTIONAL)
**Interoperable Software:**
- pyspedas (https://github.com/spedas/pyspedas)
- spacepy (https://github.com/spacepy/spacepy)
- sunpy (https://github.com/sunpy/sunpy)

**Source:** requirements.txt showing integration with other PyHC packages

**Note:** All three are PyHC core/community packages. Kaipy successfully runs in environments with these packages as demonstrated by its dependency structure.

### 31. Related Instruments (OPTIONAL)
**Instruments:**
- Van Allen Probes (RBSP) - inferred from rbspSCcomp, rbsp_satcomp scripts
- MMS (Magnetospheric Multiscale) - possible based on magnetosphere focus
- THEMIS - possible based on geospace focus

**Source:** Script names in setup.py (rbspSCcomp, rcm_rbsp_satcomp), dependencies (pyspedas which supports these missions)

**Note:** Specific instrument DOIs not available. Instruments inferred from satellite comparison script names.

### 32. Related Observatories (OPTIONAL)
**Observatories:**
- Van Allen Probes (RBSP mission)
- SuperMAG (ground magnetometer network) - from supermag-api dependency

**Source:** Script names, dependencies (supermag-api, supermag_comparison, supermag_analysis scripts)

### 33. Logo (OPTIONAL)
**Logo:** Not found

**Source:** Checked PyHC registry, README.md, repository - no logo URL found

---

## Metadata Sources Summary

This metadata was extracted using the following sources, in order of priority:

1. **PyHC Package Registry** - Manually curated metadata from PyHC community registry (kaipy is listed as a PyHC community package with "Good" ratings for documentation, testing, software maturity, python3 compatibility, and license)

2. **DataCite API** (DOI: 10.5281/zenodo.15801040) - Official DOI metadata including authors, version, license, description, dates

3. **Zenodo API** (Record: 17236774) - Additional version-specific metadata including concept DOI relationship

4. **SoMEF** (Software Metadata Extraction Framework) - Automated extraction from GitHub repository including programming languages, dependencies, dates, repository statistics

5. **Manual Repository Examination** - Direct analysis of:
   - README.md - Description, documentation link, contact info
   - LICENSE.md - Full license text with copyright holders
   - setup.py & pyproject.toml - Package metadata, dependencies, scripts, version, Python requirements
   - Repository structure (kaipy/ modules) - Understanding of functionality
   - Script entry points - Analysis of 40+ command-line tools for understanding capabilities

---

## Verification Notes

### Completeness
- ✓ All 33 HSSI form fields addressed
- ✓ All MANDATORY fields have values
- ✓ Most RECOMMENDED fields have values
- ✓ Software Functionality exhaustively analyzed based on 40+ scripts and module structure
- ✓ Related Region thoroughly analyzed based on models and data sources

### Correctness
- ✓ DOI validated via DataCite and Zenodo APIs
- ✓ Repository URL validated (successfully cloned)
- ✓ Authors extracted from official DOI metadata
- ✓ License confirmed in LICENSE.md file
- ✓ Version and dates match across all sources
- ✓ PyHC membership confirmed in community registry

### Known Limitations
- Several author names appear to be GitHub usernames without full names
- No ORCIDs found for any authors
- No reference publication, related publications, or datasets found
- Funders and awards not specified in metadata
- Related instruments inferred from script names rather than explicit documentation
- Some phenomena could be specified more precisely with domain expert input

### Confidence Level
**High confidence** for: Software name, description, repository URL, DOI, license, version, programming language, development status, documentation URL, PyHC membership

**Medium confidence** for: Software functionality categories (based on code analysis), related regions (based on documented models), related instruments (inferred from scripts)

**Low confidence** for: Complete author affiliations (several missing), related phenomena (not explicitly documented)

---

## Recommended Next Steps

1. **Author Information:** Contact Michael Wiltberger (wiltbemj@ucar.edu) to:
   - Confirm full names for GitHub username authors
   - Obtain ORCID identifiers
   - Verify affiliations

2. **Scientific Context:** Consult with domain expert or review MAGE/Kaiju documentation to:
   - Add specific Related Phenomena terms
   - Confirm all applicable Software Functionality categories
   - Identify any additional Related Instruments or Observatories

3. **Publications:** Check if there are any papers describing MAGE, Kaiju, or kaipy that should be listed as reference or related publications

4. **Funding:** Confirm if NASA DRIVE Center funding should be listed in Funder/Award fields

---

*Metadata extracted by HSSI Metadata Extractor on 2025-10-09*
