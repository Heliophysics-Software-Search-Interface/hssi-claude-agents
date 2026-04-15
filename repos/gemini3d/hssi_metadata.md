# HSSI Metadata Extraction Results

**Repository:** https://github.com/gemini3d/gemini3d
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.3647579

**Note:** This is the concept DOI for all versions. Found in DataCite API and confirmed in README badge.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/gemini3d/gemini3d

**Note:** From GitHub API and repository analysis.

### 4. Software Functionality (MANDATORY)
**Values:**
- Models and Simulations
- Models and Simulations:MHD
- Models and Simulations:Physics-Based
- Models and Simulations:First Principles
- Data Visualization:2D Graphics
- Data Visualization:3D Graphics
- Data Processing and Analysis:Processing

**Note:** Gemini3D is a three-dimensional ionospheric fluid-electrodynamic model that solves MHD equations. It includes visualization capabilities for 2D and 3D outputs, and processes simulation data. The model uses first-principles physics to simulate ionospheric dynamics.

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere
- Earth Magnetosphere

**Note:** The software models the ionosphere (part of Earth's atmosphere) and its interaction with the magnetosphere. The ionosphere-thermosphere-mesosphere coupling is a primary focus, as indicated by PyHC registry keywords.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Matthew Zettergren
- **Author Identifier:** https://orcid.org/0000-0002-9837-059X
- **Affiliation:** Not found in available metadata

**Author 2:**
- **Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation:** Not found in available metadata

**Note:** Authors extracted from CITATION.cff, codemeta.json, and DataCite API.

### 7. Software Name (MANDATORY)
**Value:** Gemini3D

**Full Name:** GEMINI (Geospace Environment Model of Ion-Neutral Interactions)

**Note:** From repository name, README, and all metadata sources.

### 8. Description (MANDATORY)
**Value:** The GEMINI model (Geospace Environment Model of Ion-Neutral Interactions) is a three-dimensional ionospheric fluid-electrodynamic model written in object-oriented Fortran (2008+ standard). GEMINI is used for various scientific studies including: effects of auroras on the terrestrial ionosphere, natural hazard effects on the space environment, and effects of ionospheric fluid instabilities on radio propagation. The model uses generalized orthogonal curvilinear coordinates and has been tested with dipole and Cartesian coordinates. It solves the coupled ionospheric fluid and electrodynamic equations to simulate plasma dynamics in the ionosphere-thermosphere system.

**Note:** Compiled from README.md and codemeta.json descriptions.

### 9. Concise Description (OPTIONAL)
**Value:** Three-dimensional ionospheric fluid-electrodynamic model for simulating auroral effects, natural hazards, and ionospheric instabilities on radio propagation.

**Note:** Condensed version of main description (under 200 characters).

### 10. Publication Date (RECOMMENDED)
**Value:** 2018-08-31

**Note:** From git history (first commit date) and SoMEF extraction.

### 11. Publisher (RECOMMENDED)

**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Note:** Software is published via Zenodo DOI system (GitHub-Zenodo workflow).

### 12. Version (RECOMMENDED)

**Version Number:** v1.7.0

**Version Date:** 2024-01-09

**Version Description:** Working release wrapping up late 2022 and all 2023 changes, before implementing Git Submodules in Gemini3D. CI passes: Linux (GCC 9,10,11,12,13, Intel oneAPI 2024.0), macOS (GCC 13).

**Version PID:** https://doi.org/10.5281/zenodo.10475267

**Note:** Latest version from git tags and Zenodo API. The concept DOI is 10.5281/zenodo.3647579, while the version-specific DOI is 10.5281/zenodo.10475267.

### 13. Programming Language (RECOMMENDED)
**Values:**
- Fortran 2008
- Python 3.x

**Note:** Primary code is in Fortran 2008+ (from README and codemeta.json), with Python frontend for scripting, plotting, and analysis.

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Note:** No reference publication DOI found in CITATION.cff, README, or other metadata sources. The software itself has DOIs, but no separate publication describing it was identified.

### 15. License (RECOMMENDED)

**License:** Apache License 2.0

**License URI:** https://spdx.org/licenses/Apache-2.0

**Note:** From LICENSE file, GitHub API, SoMEF, and codemeta.json.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- ionosphere
- aurora
- ionosphere_thermosphere_mesosphere
- magnetosphere
- fluid dynamics
- electrodynamics
- space physics
- space weather
- MHD
- plasma physics
- geospace

**Note:** From GitHub topics (aurora, ionosphere), codemeta.json, PyHC registry, and domain analysis of the software.

### 17. Data Sources (OPTIONAL)
**Values:**
- Other

**Note:** The model can ingest neutral atmospheric data from other models/datasets (e.g., MSIS, HWM for neutral atmosphere). It also accepts precipitation and electric field boundary conditions from external sources. No specific standard data sources like CDAWeb or HAPI were identified.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- HDF5
- ascii

**Note:** From documentation (Readme_input.md). Primary format is HDF5, with support for raw binary (.dat) files which are ASCII-like.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- HDF5

**Note:** From documentation (Readme_output.md). The file format for Gemini output is HDF5.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Note:** Explicitly stated in README.md: "Operating system support includes: Linux, MacOS, and Windows."

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- x86-64
- Apple Silicon arm64
- Linux aarch64 or arm64
- ppc64le
- HPC or HEC

**Note:** From README.md: "CPU arch support includes: Intel, AMD, ARM, IBM POWER, Cray and more." The software runs on HPC clusters and is optimized for parallel execution.

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Not found in standard controlled vocabularies

**Suggested values based on software purpose:**
- Auroral emissions
- Ionospheric disturbances
- Geomagnetic storms
- Space weather events

**Note:** While the software models auroras and ionospheric phenomena, specific controlled vocabulary terms were not found in the available metadata.

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Note:** From codemeta.json (developmentStatus: "active"). The repository shows recent activity (last updated 2025-12-01 per SoMEF) and active development.

### 24. Documentation (RECOMMENDED)
**Value:** https://gemini3d.github.io/gemini3d/

**Note:** Main documentation page. Inline source code documentation is at https://gemini3d.github.io/gemini/. Additional documentation in docs/ directory of repository.

### 25. Funder (OPTIONAL)

**Funder 1:**
- **Organization:** NSF
- **Funder Identifier:** Not found

**Funder 2:**
- **Organization:** NASA
- **Funder Identifier:** Not found

**Funder 3:**
- **Organization:** DARPA
- **Funder Identifier:** Not found

**Note:** From codemeta.json. Specific grant identifiers not provided in available metadata.

### 26. Award Title (OPTIONAL)

**Award 1:**
- **Award Title:** Not found
- **Award Number:** NNH19ZDA001N-HDEE grant 80NSSC20K0176

**Note:** From README.md, this NASA HDEE grant funded development of h5fortran and PyGemini components. Full award title not provided.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found

**Note:** No specific publications citing or describing the software were found in the repository metadata.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Note:** The software uses standard atmospheric models (MSIS, HWM) but no specific dataset DOIs were provided.

### 29. Related Software (OPTIONAL)

**Software 1:** https://github.com/gemini3d/mat_gemini (MATLAB scripts for Gemini)

**Software 2:** https://github.com/gemini3d/GEMINI-examples (Example simulations)

**Software 3:** https://github.com/gemini3d/GEMINI-docs (Mathematical formulation documentation)

**Software 4:** https://github.com/geospace-code/h5fortran (HDF5 Fortran library, dependency)

**Note:** From README.md. These are companion repositories and key dependencies.

### 30. Interoperable Software (OPTIONAL)
**Value:** Not found

**Note:** While the software depends on standard numerical libraries (LAPACK, ScaLAPACK, MUMPS, HDF5), no specific DOIs for interoperable software packages were identified.

### 31. Related Instruments (OPTIONAL)
**Value:** Not found

**Note:** The software is a modeling tool and not tied to specific instruments, though it can simulate observations from various ionospheric instruments.

### 32. Related Observatories (OPTIONAL)
**Value:** Not found

**Note:** The software is a general modeling tool not specific to particular observatories, though users may configure it for specific observatory locations.

### 33. Logo (OPTIONAL)
**Value:** Not found

**Note:** No logo file or URL found in repository metadata or PyHC registry.

---

## Metadata Sources Summary

### DataCite API (10.5281/zenodo.3647579)
- Software name: Gemini3D
- Authors with ORCIDs
- Publisher: Zenodo
- Version: v1.7.0
- License: Creative Commons Attribution 4.0 International (note: this is for the Zenodo deposit; the code itself is Apache 2.0)
- Description (brief version)
- Related repository URL

### Zenodo API (10475267)
- Version-specific DOI: 10.5281/zenodo.10475267
- Concept DOI: 10.5281/zenodo.3647579
- Publication date: 2024-01-09
- Creators with ORCIDs
- Version information

### SoMEF
- Repository: https://github.com/gemini3d/gemini3d
- Date created: 2018-08-31
- Date updated: 2025-12-01
- License: Apache-2.0
- Keywords: aurora, ionosphere
- Description excerpts from README

### PyHC Registry (Unevaluated)
- Entry name: PyGemini
- Description: Python frontend for Gemini3D ionospheric kintic + fluid dynamics models
- Repository: https://github.com/gemini3d/gemini3d
- Contact: Michael Hirsch
- Keywords: ionosphere_thermosphere_mesosphere, specific

### Repository Files
- **README.md:** Comprehensive description, platform support, use cases
- **CITATION.cff:** Authors with ORCIDs, DOI
- **LICENSE:** Apache License 2.0 full text
- **codemeta.json:** Structured metadata including funders (NSF, NASA, DARPA), keywords, development status
- **Git history:** Version tags, dates, first commit date
- **Documentation:** Detailed usage, input/output formats, capabilities

### Manual Analysis
- Source code structure revealing functionality categories
- Documentation analysis for input/output formats
- README analysis for operating systems and CPU architectures
- Scientific domain expertise applied to determine Related Region and Software Functionality

---

## Notes on Completeness

### Fields with High Confidence
All mandatory and most recommended fields have been populated with data from multiple authoritative sources.

### Fields Requiring User Input
- Submitter information (by design)
- Award titles (partial information available)
- ROR identifiers for funders and affiliations

### Fields Not Found
- Reference publication (no JOSS or similar paper identified)
- Logo
- Specific related publications, datasets, instruments, or observatories
- Complete award information

### Special Notes
1. The concept DOI (10.5281/zenodo.3647579) points to all versions, while 10.5281/zenodo.10475267 is the latest specific version (v1.7.0)
2. The license on Zenodo deposits is CC-BY-4.0, but the source code license is Apache-2.0
3. Software is in PyHC unevaluated registry, indicating it's recognized by the heliophysics Python community but may not meet all PyHC standards yet
4. The software has both a Fortran computational core and a Python frontend (PyGemini)
