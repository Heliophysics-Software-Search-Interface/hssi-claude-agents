# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/NCAR-GLOW
**Extraction Date:** 2025-12-03
**DOI:** https://doi.org/10.5281/zenodo.3344536

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.3344536
**Source:** DataCite API - Concept DOI for all versions
**Note:** This is the concept DOI that points to the latest version. The latest version-specific DOI is https://doi.org/10.5281/zenodo.8309940

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/NCAR-GLOW
**Source:** DataCite API, SoMEF, PyHC registry

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Visualization
- Data Visualization:Line Plots
- Models and Simulations
- Models and Simulations:Physics-Based
- Models and Simulations:First Principles

**Source:** Manual analysis of README, package description, and example code
**Justification:** GLOW is a physics-based, first-principles model that simulates auroral and airglow phenomena in the Earth's atmosphere. It computes number densities of neutrals, ions, and electrons; Pedersen and Hall currents; volume emission rates vs. wavelength and altitude; and precipitating flux vs. energy. The package includes plotting functionality (ncarglow.plots module) for visualizing altitude profiles, precipitation, volume emission rates, densities, and temperatures. This constitutes modeling/simulation, data analysis, and data visualization functionality.

### 5. Related Region (MANDATORY)
**Value:** Earth Atmosphere
**Source:** PyHC keywords ("ionosphere_thermosphere_mesosphere"), package keywords, and manual analysis
**Justification:** GLOW models the ionosphere, thermosphere, and mesosphere regions of Earth's atmosphere, specifically for aurora and airglow phenomena.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** scivision (Michael Hirsch)
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 2:**
- **Name:** Stan Solomon
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** DataCite API, Zenodo API, PyHC contact field
**Note:** The DataCite API lists "Scivision" and "Solomon, Stan" as creators. The PyHC registry lists "Michael Hirsch" as the contact. "Scivision" appears to be Michael Hirsch's GitHub username. ORCIDs were not found in the repository or metadata sources.

### 7. Software Name (MANDATORY)
**Value:** GLOW (or NCAR-GLOW)
**Source:** PyHC registry, SoMEF, README
**Note:** The Python package name is "ncarglow" but the software is referred to as "GLOW" in documentation. The full expanded name is "GLobal airglOW Model" (per README).

### 8. Description (MANDATORY)
**Value:** The GLobal airglOW Model (GLOW) is a physics-based model for simulating auroral and airglow phenomena in Earth's ionosphere and thermosphere. GLOW computes number densities of neutrals, ions and electrons; Pedersen and Hall currents; volume emission rates versus wavelength and altitude; and precipitating flux versus energy. This implementation provides Python, Matlab, and Fortran interfaces to NCAR GLOW version 0.981, with the Python interface being the recommended approach. The model uses first-principles physics to simulate the effects of auroral precipitation on the upper atmosphere.

**Source:** Compiled from README, PyHC registry, SoMEF, and DataCite descriptions

### 9. Concise Description (OPTIONAL)
**Value:** NCAR GLOW 0.981 aurora/airglow model for Earth's ionosphere and thermosphere, accessible from Python, Matlab, and Fortran.
**Source:** Adapted from PyHC registry description and README

### 10. Publication Date (RECOMMENDED)
**Value:** 2018-12-20
**Source:** SoMEF (date_created from GitHub API)
**Note:** This is the date the repository was created. The first commit was on 2017-01-06, but the GitHub repository was created in 2018.

### 11. Publisher (RECOMMENDED)

**Organization:** Zenodo
**Publisher Identifier:** https://zenodo.org

**Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

**Version Number:** v1.4.0
**Version Date:** 2023-09-01
**Version Description:** Require Python >= 3.9; fixed geomagindices package for current Pandas versions. This GLOW implementation remains as an almost zero modification to the original source code. The Matlab/Python interface uses a command line interface to GLOW, running GLOW as a separate process to avoid thread-safety issues.
**Version PID:** https://doi.org/10.5281/zenodo.8309940

**Source:** DataCite API, Zenodo API, SoMEF (releases), pyproject.toml

### 13. Programming Language (RECOMMENDED)
**Values:**
- Fortran77
- Fortran90
- Python 3.x
- MATLAB

**Source:** SoMEF (GitHub API language statistics), pyproject.toml (requires Python >=3.9), CI configuration
**Note:** Primary implementation is in Fortran (435,994 bytes), with Python (14,376 bytes) and MATLAB (12,742 bytes) interfaces. The package also uses CMake and Meson build systems.

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found
**Source:** Checked README, repository files, and all metadata sources
**Note:** No reference publication DOI or citation was found in the repository. Users should check with the original NCAR GLOW model for potential reference papers.

### 15. License (RECOMMENDED)

**License:** Apache License 2.0
**License URI:** https://www.apache.org/licenses/LICENSE-2.0

**Source:** SoMEF (GitHub API), LICENSE.txt file
**Note:** Full license text is available in LICENSE.txt

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- thermosphere
- ionosphere
- aurora
- airglow

**Source:** pyproject.toml keywords field, PyHC keywords, SoMEF
**Note:** PyHC registry includes "ionosphere_thermosphere_mesosphere" as a domain keyword.

### 17. Data Sources (OPTIONAL)
**Value:** Not found
**Source:** Manual examination of code and documentation
**Note:** GLOW appears to be a model that generates data rather than consuming external data sources. It may use geomagnetic indices (via the geomagindices dependency) but no specific data sources like CDAWeb or HAPI are mentioned.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- Other (binary scratch disk files for Matlab interface)
- Other (NetCDF for TIEGCM I/O in MPI version)

**Source:** README mentions binary files for Matlab interface and NetCDF for TIEGCM I/O
**Note:** The Python interface uses direct API calls rather than file I/O.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- Other (xarray.Dataset in Python)
- Other (binary scratch disk files for Matlab interface)
- netCDF3/4 (for TIEGCM I/O in MPI version)

**Source:** README documentation
**Note:** Primary Python output is an xarray.Dataset object.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- OS Independent

**Source:** CI workflow (.github/workflows/ci.yml) tests on ubuntu-latest and macos-latest; pyproject.toml classifies as "Operating System :: OS Independent"
**Note:** A Fortran compiler is required on any platform.

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- x86-64
- CPU Independent

**Source:** Inferred from OS support and lack of architecture-specific code
**Note:** Should work on any architecture with a Fortran compiler, though primarily tested on x86-64.

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Not explicitly categorized using HSSI controlled vocabulary

**Source:** Manual analysis
**Note:** The software models auroral and airglow phenomena, which are related to geomagnetic activity and solar-terrestrial interactions, but these specific phenomena are not in the provided HSSI controlled vocabulary list.

### 23. Development Status (RECOMMENDED)
**Value:** Active
**Source:** SoMEF (date_updated: 2025-10-23), GitHub activity
**Note:** The software reached a stable, usable state and is being actively developed. Latest update was in October 2025.

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/NCAR-GLOW/blob/main/README.md
**Source:** Repository README
**Note:** Documentation is primarily in the README file. No separate documentation site was found.

### 25. Funder (OPTIONAL)
**Value:** Not found
**Source:** Checked DataCite API, Zenodo API, and repository files
**Note:** No funding information was found in the available metadata.

### 26. Award Title (OPTIONAL)
**Value:** Not found
**Source:** Checked DataCite API, Zenodo API, and repository files
**Note:** No award information was found in the available metadata.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found
**Source:** Checked DataCite API relatedIdentifiers and repository
**Note:** No related publications were listed in the available metadata.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found
**Source:** Checked DataCite API relatedIdentifiers
**Note:** No related datasets were listed in the DOI metadata.

### 29. Related Software (OPTIONAL)
**Values:**
- numpy (dependency)
- xarray (dependency)
- geomagindices (dependency, version >=1.5.0)

**Source:** pyproject.toml dependencies
**Note:** These are the primary Python dependencies. The software also uses MSIS and other atmospheric models internally.

### 30. Interoperable Software (OPTIONAL)
**Value:** Not found
**Source:** Manual examination
**Note:** While the software has dependencies, no explicit interoperability with other heliophysics packages was documented.

### 31. Related Instruments (OPTIONAL)
**Value:** Not applicable / Not found
**Source:** Manual examination
**Note:** GLOW is a model rather than instrument-specific analysis software. It can be used to interpret data from various auroral observation instruments but is not tied to a specific instrument.

### 32. Related Observatories (OPTIONAL)
**Value:** Not applicable / Not found
**Source:** Manual examination
**Note:** GLOW is a general-purpose model not tied to a specific observatory or mission.

### 33. Logo (OPTIONAL)
**Value:** https://www2.hao.ucar.edu/sites/default/files/resize/images/ICON-GOLD_2016/IonosphereHorizon-Banner-980x232.jpg
**Source:** PyHC registry
**Note:** This logo URL is from the PyHC registry entry.

---

## Additional Notes

### Metadata Sources Priority
The metadata in this file was compiled using the following priority order:
1. PyHC registry (manually curated, most authoritative for this package)
2. DataCite/Zenodo APIs (official DOI metadata)
3. SoMEF (automated extraction from repository)
4. Manual examination of repository files

### Version History
According to the GitHub releases and Zenodo records, the software has had multiple versions:
- v1.4.0 (2023-09-01) - Latest, modernize and cleanup
- v1.3.0 (2021-05-25) - Updated interfaces, tests, examples
- v1.1.3 (2019-09-27) - Added examples and simulation mods
- v1.1.2 (2019-07-30) - Meson subproject support
- v1.1.1 (2019-07-19) - Build system version checks
- v1.1.0 (2019-07-19) - Bug fixes for Python output reading

### Quality Ratings from PyHC
While GLOW is in the "unevaluated" PyHC registry, the package appears to be well-maintained based on:
- Recent updates (2025-10-23)
- Active CI/CD with testing on multiple platforms
- Clear documentation in README
- Apache 2.0 open-source license
- Support for multiple programming languages

### Scientific Context
GLOW (GLobal airglOW Model) is an atmospheric model originally developed at NCAR (National Center for Atmospheric Research). It simulates the effects of auroral particle precipitation on the ionosphere and thermosphere, computing various physical quantities including:
- Number densities of neutral species, ions, and electrons
- Pedersen and Hall conductivities and currents
- Volume emission rates as a function of wavelength and altitude
- Energy deposition profiles
- Heating rates

This implementation maintains the original NCAR GLOW 0.981 Fortran code with minimal modifications while providing modern interfaces for Python and Matlab users.
