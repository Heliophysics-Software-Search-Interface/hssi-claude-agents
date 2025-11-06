# HSSI Metadata Extraction Results

**Repository:** https://github.com/CosmicStudioSoftware/OMMBV
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.1299374
**Source:** User-provided; this is the concept DOI for all versions

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/CosmicStudioSoftware/OMMBV
**Source:** DataCite API, SoMEF, PyHC registry

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:Field-line Tracing
- Models and Simulations:Field-line Tracing

**Source:** Manual analysis of README, documentation, and code. The software provides:
1. Orthogonal vector basis calculations for geomagnetic fields (coordinate transforms)
2. Field-line tracing using IGRF (both processing and simulation capability)
3. Ion drift and electric field mapping along field lines (ionospheric and magnetospheric coordinate systems)
4. Coordinate and vector transformations (ECEF, geodetic, geographic)

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere
- Earth Magnetosphere

**Source:** Manual analysis of README. Software is explicitly designed for:
- Ionosphere and thermosphere (Earth Atmosphere) - mentions E-region at 120 km, neutral atmosphere coupling
- Magnetosphere (Earth Magnetosphere) - explicitly mentioned for plasma mapping and electric field calculations
- Used by ICON mission, COSMIC-2 constellation, and C/NOFS satellite (all Earth-focused missions)

### 6. Authors (MANDATORY)

#### Author 1
- **Name:** Russell Stoneback
- **Author Identifier:** https://orcid.org/0000-0001-7216-4336
- **Affiliation:**
  - **Organization:** Cosmic Studio
  - **Affiliation Identifier:** Not found

#### Author 2
- **Name:** Jeff Klenzing
- **Author Identifier:** https://orcid.org/0000-0001-8321-6074
- **Affiliation:**
  - **Organization:** Goddard Space Flight Center
  - **Affiliation Identifier:** Not found

#### Author 3
- **Name:** Gayatri Iyer
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** DataCite API and Zenodo API

### 7. Software Name (MANDATORY)
**Value:** OMMBV
**Full Name:** Orthogonal Multipole Magnetic Basis Vectors (OMMBV)
**Source:** GitHub repository name, PyHC registry, DataCite, SoMEF

### 8. Description (MANDATORY)
**Value:** The motion of plasma in the ionosphere is the result of forcing from neutral winds, electric fields, as well as the orientation of those fields and forces relative to the background magnetic field. OMMBV (Orthogonal Multipole Magnetic Basis Vectors) calculates directions (unit vectors) based upon the geomagnetic field that are optimized for understanding the movement of plasma, the mapping of electric fields, and coupling with the neutral atmosphere. This system is the first to remain orthogonal for multipole magnetic fields as well as when including a geodetic reference surface (Earth). OMMBV also includes methods for scaling ion drifts and electric fields at one location to any other location along the same field line, typically to either the magnetic footpoint or to the magnetic equator. The software is used by NASA's ICON Explorer Mission, NOAA/NSPO COSMIC-2 constellation, and is being incorporated into C/NOFS satellite analysis routines.

**Source:** GitHub README and SoMEF description extraction

### 9. Concise Description (OPTIONAL)
**Value:** Orthogonal vector basis and field-line mapping for multipole magnetic fields, optimized for ionospheric plasma dynamics and electric field calculations.

**Source:** Created from pyproject.toml description

### 10. Publication Date (RECOMMENDED)
**Value:** 2018-06-21
**Source:** SoMEF (date_created from GitHub API)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/03cpe7c52

**Source:** DataCite API (Zenodo is the publisher for the DOI)

### 12. Version (RECOMMENDED)

#### Latest Version (v1.1.0)
- **Version Number:** v1.1.0
- **Version Date:** 2025-04-07
- **Version Description:** Switched away from distutils to Meson for build system; Updated coupling to coveralls; Updated package version for security issue in sphinx; Updated online unit testing; Updated to IGRF14; Updated documentation; Updated unit tests to latest standards
- **Version PID:** https://doi.org/10.5281/zenodo.15170693

**Source:** DataCite API, Zenodo API, GitHub releases (from SoMEF)

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x
- Fortran 2003
- Fortran 2008

**Source:** SoMEF (GitHub language statistics: Python 231,550 bytes, Fortran 63,461 bytes), pyproject.toml (supports Python 3.9-3.12)

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Source:** No reference publication DOI found in DataCite, Zenodo, README, or other sources

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause

**Source:** DataCite API, Zenodo API, SoMEF, GitHub

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- Magnetosphere
- Ionosphere
- Thermosphere
- Heliophysics
- Magnetic Field
- Electric Field
- vector-basis
- geomagnetic-field
- magnetic-fields
- field-line-tracing
- meridional
- zonal
- field-aligned
- satellite
- electric-field-mapping
- ion-drift-mapping
- multipole
- electrodynamics
- plasma
- coordinate-transformation

**Source:** Zenodo API, pyproject.toml, GitHub topics (from SoMEF)

### 17. Data Sources (OPTIONAL)
**Value:** Not found

**Source:** No specific data sources mentioned as inputs to the software

### 18. Input File Formats (RECOMMENDED)
**Value:** Not found

**Source:** Software primarily performs calculations based on IGRF model and user-provided coordinates; does not appear to read specific file formats

### 19. Output File Formats (RECOMMENDED)
**Value:** Not found

**Source:** Returns calculated values (vectors, scalars) rather than writing to specific file formats; may output via Python data structures

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- OS Independent

**Source:** pyproject.toml classifiers specify POSIX/Linux and MacOS. GitHub Actions CI tests on multiple platforms (from SoMEF).

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Source:** No specific CPU architecture requirements mentioned; pure Python/Fortran code should be CPU independent

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Not found (HSSI-specific phenomena not identified in source materials)

**Source:** No specific phenomena from controlled vocabularies identified

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** PyHC registry rates software maturity as "Good"; latest release in April 2025; continuous development evident from commit history and release notes

### 24. Documentation (RECOMMENDED)
**Value:** https://ommbv.readthedocs.io

**Source:** PyHC registry, SoMEF, README badges

### 25. Funder (OPTIONAL)

#### Funder 1
- **Organization:** Cosmic Studio
- **Funder Identifier:** Not found

#### Funder 2
- **Organization:** Naval Research Laboratory
- **Funder Identifier:** Not found

#### Funder 3
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

#### Funder 4
- **Organization:** National Oceanic and Atmospheric Administration
- **Funder Identifier:** https://ror.org/02z5nhe81

#### Funder 5
- **Organization:** National Science Foundation
- **Funder Identifier:** https://ror.org/021nxhr62

**Source:** README.md funding acknowledgments

### 26. Award Title (OPTIONAL)

#### Award 1
- **Award Title:** Not found
- **Award Number:** N00173-19-1-G016
- **Source:** README.md (Naval Research Laboratory grant)

#### Award 2
- **Award Title:** Not found
- **Award Number:** 80NSSC18K1203
- **Source:** README.md (NASA grant)

#### Award 3
- **Award Title:** Not found
- **Award Number:** NNG12FA45C
- **Source:** README.md (NASA grant for previous versions)

#### Award 4
- **Award Title:** Not found
- **Award Number:** AGS-1033112
- **Source:** README.md (NOAA/NSF grant for previous versions)

#### Award 5
- **Award Title:** Not found
- **Award Number:** 1651393
- **Source:** README.md (NSF grant for previous versions)

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found

**Source:** No related publications found in DataCite, Zenodo, or README

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Source:** No specific datasets mentioned

### 29. Related Software (OPTIONAL)
**Values:**
- pysat (dependency, from requirements.txt)
- apexpy (similar functionality for apex coordinates)

**Source:** requirements.txt, manual analysis of related packages in the PyHC ecosystem

### 30. Interoperable Software (OPTIONAL)
**Values:**
- pysat

**Source:** README mentions OMMBV is used with pysat for satellite data analysis; requirements.txt lists pysat as dependency

### 31. Related Instruments (OPTIONAL)
**Values:**
- Not found (specific instrument identifiers not provided)

**Note:** Software is used by ICON, COSMIC-2, and C/NOFS missions, but specific instrument DOIs not available

**Source:** README mentions mission usage but no formal instrument identifiers

### 32. Related Observatories (OPTIONAL)

#### Observatory 1
- **Observatory Name:** ICON (Ionospheric Connection Explorer)

#### Observatory 2
- **Observatory Name:** COSMIC-2

#### Observatory 3
- **Observatory Name:** C/NOFS (Communications/Navigation Outage Forecasting System)

**Source:** README.md explicitly mentions use by these missions/observatories

### 33. Logo (OPTIONAL)
**Value:** https://raw.githubusercontent.com/CosmicStudioSoftware/OMMBV/main/docs/images/logo_high_res.png

**Source:** SoMEF, PyHC registry, README

---

## Metadata Source Summary

**Data Collection Methods Used:**
1. ✅ DataCite API (DOI: 10.5281/zenodo.1299374)
2. ✅ Zenodo API (Record ID: 15170693 - latest version)
3. ✅ PyHC Package Registry (projects.yml - community packages)
4. ✅ SoMEF (Software Metadata Extraction Framework)
5. ✅ Manual repository examination (README, pyproject.toml, LICENSE, etc.)

**Metadata Quality Assessment:**
- **Excellent coverage:** Basic information (authors, repository, version, license)
- **Good coverage:** Development status, documentation, keywords, programming languages
- **Limited coverage:** File formats (software doesn't use traditional I/O), phenomena terms, related publications
- **PyHC Status:** Package is listed in PyHC community registry with "Good" ratings across all quality metrics

**Notes:**
- This software has exceptional metadata quality due to active maintenance, good documentation, and PyHC registry inclusion
- Concept DOI (10.5281/zenodo.1299374) covers all versions; latest version DOI is 10.5281/zenodo.15170693
- Software is production-ready (Development Status: 5 - Production/Stable)
- Active development with most recent release in April 2025
