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
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Data Processing and Analysis
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:Analysis
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:First Principles
- Models and Simulations:Physics-Based
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:2D Slices
- Data Visualization:Line Plots
- Servers and Environments
- Servers and Environments:High Performance Computing
- Data Processing and Analysis:Processing

**Note:** PyGemini is the PyHC registry name for the Gemini3D/GEMINI software stack. The repository implements a three-dimensional ionospheric fluid-electrodynamic model, uses empirical ionospheric/atmospheric components such as Fang, GLOW, MSIS, and HWM, exposes geographic/geomagnetic and dipole coordinate utilities, supports HDF5 simulation data loading/processing, includes 2D and slice plotting examples, and is built for MPI/HPC execution.

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
**Value:** PyGemini

**Full Name:** GEMINI (Geospace Environment Model of Ion-Neutral Interactions)

**Note:** PyGemini is the authoritative PyHC/HSSI registry name for this entry. The repository, README, CITATION.cff, codemeta.json, and Zenodo records use Gemini3D or GEMINI as alternate names.

### 8. Description (MANDATORY)
**Value:** PyGemini is the PyHC registry name for the Gemini3D/GEMINI software stack, a three-dimensional ionospheric fluid-electrodynamic model written primarily in object-oriented Fortran 2008. GEMINI is used for studies of auroral effects on the terrestrial ionosphere, natural hazard effects on the space environment, and ionospheric fluid instabilities that affect radio propagation. The model uses generalized orthogonal curvilinear coordinates, has been tested with dipole and Cartesian coordinates, supports MPI/HPC execution, and includes Python/MATLAB-facing workflows for running simulations and loading, plotting, and analyzing HDF5 output.

**Note:** Compiled from README.md, docs/Readme_output.md, docs/Readme_magcalc.md, CITATION.cff, codemeta.json, and the PyHC registry name.

### 9. Concise Description (OPTIONAL)
**Value:** PyHC entry for the Gemini3D ionospheric fluid-electrodynamic model and scripting workflows for simulations, HDF5 output, plotting, and analysis.

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

**Note:** Latest tagged/Zenodo release from git tags and Zenodo API. The concept DOI is 10.5281/zenodo.3647579, while the version-specific DOI is 10.5281/zenodo.10475267. The refreshed main branch declares a development project version of 2.0.0 in CMakeLists.txt, but no newer release tag or version DOI is present.

### 13. Programming Language (RECOMMENDED)
**Values:**
- Fortran 2008
- C
- C++
- Python 3.x

**Note:** Primary code is Fortran 2008+ (README and source tree). The repository also contains C/C++ interface and utility code, and Python is used for scripting, tests, plotting, and analysis workflows described in the documentation.

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
- ionospheric fluid electrodynamics
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
- Other

**Note:** From docs/Readme_input.md and docs/Readme_magcalc.md. Primary scientific input is HDF5; text configuration is provided through config.nml/config.ini; raw binary .dat field-point files are also supported for magcalc and are represented as Other.

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
- Auroral emissions
- Ionospheric disturbances
- Ionospheric instabilities
- Natural hazard effects on the space environment
- Space weather events

**Note:** Based on README.md use cases for auroras, natural hazard effects on the space environment, and ionospheric fluid instabilities affecting radio propagation.

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Note:** From codemeta.json (developmentStatus: "active") and recent upstream activity. The copied repository was fast-forwarded to origin/main at commit a0ae56fe from 2026-04-22; the latest release tag remains v1.7.0 from 2024-01-09.

### 24. Documentation (RECOMMENDED)
**Value:** https://gemini3d.github.io/gemini3d/

**Note:** Public generated documentation page. Additional durable documentation is in the repository docs/ directory at https://github.com/gemini3d/gemini3d/tree/main/docs.

### 25. Funder (OPTIONAL)

**Funder 1:**
- **Organization:** National Science Foundation
- **Funder Identifier:** Not found

**Funder 2:**
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** Not found

**Funder 3:**
- **Organization:** Defense Advanced Research Projects Agency
- **Funder Identifier:** Not found

**Note:** Funder names expanded from codemeta.json. Specific funder identifiers are not provided in available repository metadata.

### 26. Award Title (OPTIONAL)

**Award 1:**
- **Award Title:** NASA Heliophysics Data Environment Enhancements
- **Award Number:** NNH19ZDA001N-HDEE grant 80NSSC20K0176

**Note:** From README.md, this NASA HDEE grant funded development of h5fortran and PyGemini components.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values:**
- https://doi.org/10.1029/2012JA017637
- https://doi.org/10.1002/2013GL058018
- https://doi.org/10.1002/2013JA019583
- https://doi.org/10.1002/2015JA021116
- https://doi.org/10.1002/2015GL066806
- https://doi.org/10.1002/2015JA021790
- https://doi.org/10.1002/2014JA020860
- https://doi.org/10.1002/2015JA021536
- https://doi.org/10.1002/2016JA023159
- https://doi.org/10.1002/2016RS006182
- https://doi.org/10.1029/2018JA025721
- https://doi.org/10.1029/2018GL081569
- https://doi.org/10.1029/2018GL081886
- https://doi.org/10.1029/2019GL082576
- https://doi.org/10.1029/2019JA027200
- https://doi.org/10.1029/2019JA027734
- https://doi.org/10.1029/2008JA013384
- https://doi.org/10.1029/2010GL045406
- https://doi.org/10.1029/2011JA016649

**Note:** Related model-use and method publications found in docs/Readme_references.md and inline source references. Field 14 remains Not found because the repository does not identify one preferred software-reference publication separate from the software DOI.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Note:** The software uses standard atmospheric models (MSIS, HWM) but no specific dataset DOIs were provided.

### 29. Related Software (OPTIONAL)

**Software 1:** https://github.com/gemini3d/mat_gemini (MATLAB scripts for Gemini)

**Software 2:** https://github.com/gemini3d/GEMINI-examples (Example simulations)

**Software 3:** https://github.com/gemini3d/GEMINI-docs (Mathematical formulation documentation)

**Software 4:** https://github.com/geospace-code/h5fortran (HDF5 Fortran library, dependency)

**Software 5:** https://github.com/gemini3d/glow (GLOW dependency used by the build)

**Software 6:** https://github.com/gemini3d/hwm14 (HWM14 dependency used by the build)

**Software 7:** https://github.com/gemini3d/msis (MSIS dependency used by the build)

**Software 8:** https://mumps-solver.org/ (MUMPS sparse solver dependency)

**Note:** From README.md and CMake configuration. These are companion repositories and key model/numerical dependencies.

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://github.com/gemini3d/pygemini
- https://github.com/gemini3d/mat_gemini
- https://github.com/HDFGroup/hdf5
- https://github.com/geospace-code/h5fortran
- https://www.mcs.anl.gov/research/projects/mpi/
- https://netlib.org/lapack/
- https://www.netlib.org/scalapack/
- https://mumps-solver.org/

**Note:** Interoperable companion front ends and important runtime/numerical libraries documented in README.md and CMake configuration.

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
- Date updated: 2025-12-01 in the original SoMEF output; current Codex copy was refreshed to origin/main commit a0ae56fe dated 2026-04-22
- License: Apache-2.0
- Keywords: aurora, ionosphere
- Description excerpts from README

### PyHC Registry (Unevaluated)
- Entry name: PyGemini
- Description: Python frontend for Gemini3D ionospheric kinetic + fluid dynamics models
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
