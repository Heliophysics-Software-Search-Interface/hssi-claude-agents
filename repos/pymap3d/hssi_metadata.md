# HSSI Metadata Extraction Results

**Repository:** https://github.com/geospace-code/pymap3d
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.595430
- **Source:** DataCite API (concept DOI for all versions)

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/geospace-code/pymap3d
- **Source:** SoMEF and repository metadata
- **Note:** Repository was previously at https://github.com/scivision/pymap3d (redirects to current location)

### 4. Software Functionality (MANDATORY)
- **Coordinate Transforms**
- **Coordinate Transforms:Heliospheric**
- **Coordinate Transforms:Ionospheric**
- **Coordinate Transforms:Magnetospheric**
- **Data Processing and Analysis**
- **Data Processing and Analysis:Analysis**

**Source:** Manual examination of README.md and function list. PyMap3D provides coordinate conversions between multiple systems (geodetic, ECEF, ECI, ENU, NED, AER, spherical, geocentric) used extensively in heliophysics research. Primary functionality is coordinate transformation for ionospheric, magnetospheric, and heliospheric applications.

### 5. Related Region (MANDATORY)
- **Earth Atmosphere**
- **Earth Magnetosphere**
- **Interplanetary Space**

**Source:** PyHC registry classification ("ionosphere_thermosphere_mesosphere") and analysis of coordinate systems supported (ECI for interplanetary, geodetic/ENU for Earth regions). The software supports coordinate transformations commonly used across these physical regions.

### 6. Authors (MANDATORY)

#### Author 1
- **Name:** Michael Hirsch, Ph.D.
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation:** SciVision, Inc.
- **Affiliation Identifier:** Not found
- **Source:** DataCite API, LICENSE file, CITATION.cff, git commit history (primary contributor with 750+ commits)

#### Author 2
- **Name:** Ryan Pavlick
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Affiliation Identifier:** Not found
- **Source:** DataCite API, git contributors

#### Author 3
- **Name:** cchuravy
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Affiliation Identifier:** Not found
- **Source:** DataCite API

#### Author 4
- **Name:** Samuel Marks
- **Author Identifier:** Not found
- **Affiliation:** @offscale @stereostream
- **Affiliation Identifier:** Not found
- **Source:** DataCite API

#### Author 5
- **Name:** Philippe Rivière
- **Author Identifier:** Not found
- **Affiliation:** Visionscarto.net
- **Affiliation Identifier:** Not found
- **Source:** DataCite API

#### Author 6
- **Name:** Felipe Geremia Nievinski
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Affiliation Identifier:** Not found
- **Source:** LICENSE file (copyright holder)

#### Author 7
- **Name:** Michael Kleder
- **Author Identifier:** Not found
- **Affiliation:** Not found
- **Affiliation Identifier:** Not found
- **Source:** LICENSE file (copyright holder)

**Note:** CITATION.cff lists "SciVision" as the author name with ORCID 0000-0002-1637-6526. Based on git commit history and other metadata sources, this ORCID belongs to Michael Hirsch, Ph.D., and SciVision, Inc. is his organization.

### 7. Software Name (MANDATORY)
- **Name:** PyMap3D
- **Source:** SoMEF, CITATION.cff, README.md

### 8. Description (MANDATORY)
Pure Python (no prerequisites beyond Python itself) 3-D geographic coordinate conversions and geodesy. Function syntax is roughly similar to Matlab Mapping Toolbox. PyMap3D is intended for non-interactive use on massively parallel (HPC) and embedded systems. The package provides coordinate transformations between multiple systems including geodetic, ECEF (Earth-Centered Earth-Fixed), ECI (Earth-Centered Inertial), ENU (East-North-Up), NED (North-East-Down), AER (Azimuth-Elevation-Range), and spherical coordinates. Numpy and AstroPy are optional dependencies; the library can operate with pure Python for most transforms, making it suitable for embedded systems and streaming data applications.

**Source:** README.md, pyproject.toml

### 9. Concise Description (OPTIONAL)
Pure Python 3-D geographic coordinate conversions and geodesy for geospace applications, with optional Numpy/AstroPy support for enhanced accuracy.

**Source:** Synthesized from README.md and pyproject.toml

### 10. Publication Date (RECOMMENDED)
- **Date:** 2014-08-03
- **Source:** SoMEF (repository creation date from GitHub API)

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API, Zenodo integration

### 12. Version (RECOMMENDED)

#### Latest Version (v3.2.0)
- **Version Number:** v3.2.0
- **Version Date:** 2025-07-08
- **Version Description:** Added enu2ecefv support and downrange-crossrange-above coordinate conversions. Includes nvector module addition and improvements to ECI coordinate handling.
- **Version PID:** Not found - Zenodo DOI only available for v1.8.1

**Source:** Git tags, GitHub releases via SoMEF

#### Most Recent Zenodo Version (v1.8.1)
- **Version Number:** v1.8.1
- **Version Date:** 2019-06-30
- **Version Description:** Put ellipsoid in own file, put examples in own dir, test python setup.py install as well as python setup.py develop
- **Version PID:** https://doi.org/10.5281/zenodo.3262738

**Source:** Zenodo API, DataCite API

**Note:** The latest code version (v3.2.0) does not have a corresponding Zenodo DOI. The concept DOI (10.5281/zenodo.595430) covers all versions.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (primary - requires Python >= 3.9 as of v3.2.0)
- **MATLAB** (small amount - 682 bytes)

**Source:** SoMEF (GitHub API language statistics), pyproject.toml

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.21105/joss.00580
- **Source:** CITATION.cff, README.md badge, SoMEF

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://spdx.org/licenses/BSD-2-Clause.html
- **SPDX ID:** BSD-2-Clause
- **Source:** SoMEF (GitHub API), LICENSE file

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- coordinate-conversion
- coordinate-transformation
- geodesy
- ionosphere_thermosphere_mesosphere (PyHC classification)

**Source:** SoMEF (GitHub topics), pyproject.toml, PyHC registry

### 17. Data Sources (OPTIONAL)
Not found - PyMap3D is a computational library for coordinate transformations, not a data access library.

### 18. Input File Formats (RECOMMENDED)
Not applicable - PyMap3D operates on coordinate values (scalars or arrays) rather than file formats.

**Note:** The library accepts Python numeric types, Numpy arrays, Pandas DataFrames, and Xarray objects as input.

### 19. Output File Formats (RECOMMENDED)
Not applicable - PyMap3D returns coordinate values (scalars or arrays) rather than writing to files.

**Note:** Output types match input types (scalar for scalar, array for array).

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**

**Source:** pyproject.toml classifier "Operating System :: OS Independent", SoMEF GitHub Actions CI testing on Linux, macOS, and Windows

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Source:** Pure Python implementation with no CPU-specific dependencies

### 22. Related Phenomena (OPTIONAL)
Not found - No specific phenomena listed in available metadata sources.

**Note:** The software is used for coordinate transformations relevant to various heliophysics phenomena but does not target specific phenomena.

### 23. Development Status (RECOMMENDED)
- **Active**

**Source:** SoMEF (date_updated: 2025-12-01), pyproject.toml classifier "Development Status :: 5 - Production/Stable", active releases through 2025

### 24. Documentation (RECOMMENDED)
- **URL:** https://geospace-code.github.io/pymap3d/
- **Source:** README.md

### 25. Funder (OPTIONAL)
Not found

### 26. Award Title (OPTIONAL)
Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

#### Publication 1
- **DOI:** https://doi.org/10.1029/2019GL084473
- **Source:** DataCite API (relatedIdentifiers with relationType: IsCitedBy)

#### Publication 2
- **DOI:** https://doi.org/10.1111/mice.12493
- **Source:** DataCite API (relatedIdentifiers with relationType: IsCitedBy)

#### Publication 3
- **URL:** https://lib.ugent.be/fulltxt/RUG01/002/785/834/RUG01-002785834_2019_0001_AC.pdf
- **Source:** DataCite API (relatedIdentifiers with relationType: IsCitedBy)

#### Publication 4
- **Handle:** 11250/2566894
- **Source:** DataCite API (relatedIdentifiers with relationType: IsCitedBy)

#### Publication 5
- **URL:** http://id.nii.ac.jp/1342/00001621
- **Source:** DataCite API (relatedIdentifiers with relationType: IsCitedBy)

### 28. Related Datasets (OPTIONAL)
Not found

### 29. Related Software (OPTIONAL)

#### Software 1
- **Name:** matmap3d (Matlab/GNU Octave version)
- **URL:** https://github.com/geospace-code/matmap3d
- **Source:** README.md (Similar toolboxes section)

#### Software 2
- **Name:** maptran3d (Fortran version)
- **URL:** https://github.com/geospace-code/maptran3d
- **Source:** README.md (Similar toolboxes section)

#### Software 3
- **Name:** map_3d (Rust version)
- **URL:** https://github.com/gberrante/map_3d
- **Source:** README.md (Similar toolboxes section)

#### Software 4
- **Name:** cppmap3d (C++ version)
- **URL:** https://github.com/ClancyWalters/cppmap3d
- **Source:** README.md (Similar toolboxes section)

#### Software 5
- **Name:** PyProj
- **URL:** https://github.com/jswhit/pyproj
- **Source:** README.md (comparison/notes section)

#### Software 6
- **Name:** AstroPy
- **Description:** Optional dependency for high-accuracy ECI transformations
- **Source:** README.md, pyproject.toml

#### Software 7
- **Name:** Numpy
- **Description:** Optional dependency for array operations
- **Source:** README.md, pyproject.toml

### 30. Interoperable Software (OPTIONAL)

#### Software 1
- **Name:** Numpy
- **Description:** Tested with Numpy arrays
- **Source:** README.md, pyproject.toml, test suite

#### Software 2
- **Name:** Pandas
- **Description:** Tested with Pandas DataFrames
- **Source:** README.md ("added several tests so that Pandas and Xarray are functioning")

#### Software 3
- **Name:** Xarray
- **Description:** Tested with Xarray objects
- **Source:** README.md, pyproject.toml optional dependencies

#### Software 4
- **Name:** AstroPy
- **Description:** Used for high-accuracy astronomical conversions when available
- **Source:** README.md, pyproject.toml

### 31. Related Instruments (OPTIONAL)
Not found - PyMap3D is a general-purpose coordinate conversion library, not instrument-specific.

### 32. Related Observatories (OPTIONAL)
Not found - PyMap3D is a general-purpose coordinate conversion library, not mission-specific.

**Note:** However, it is used by various heliophysics missions requiring coordinate transformations.

### 33. Logo (OPTIONAL)
Not found

---

## Metadata Sources Summary

**Primary Sources:**
- DataCite API (10.5281/zenodo.595430)
- Zenodo API (record 3262738)
- SoMEF output from repository analysis
- PyHC unevaluated registry
- Repository files: README.md, CITATION.cff, LICENSE, pyproject.toml
- Git repository metadata (tags, release history)

**Metadata Quality Notes:**
- Concept DOI exists and is well-documented
- Reference publication available (JOSS)
- Active development with recent releases
- Listed in PyHC unevaluated registry
- Comprehensive documentation available
- Author information limited (mostly GitHub usernames, few ORCIDs)
- No recent Zenodo DOI for latest versions (last DOI is from 2019)
- No funder information found
- Limited structured metadata beyond basic fields

**Recommendations for Improvement:**
1. Create Zenodo DOIs for recent versions (v2.x - v3.x)
2. Add ORCID identifiers for all authors in CITATION.cff
3. Add funder information if applicable
4. Consider adding ROR identifiers for institutional affiliations
5. Add more structured keywords from controlled vocabularies (AGU, UAT)
