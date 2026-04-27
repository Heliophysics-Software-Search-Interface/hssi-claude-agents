# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/maidenhead
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Concept DOI:** https://doi.org/10.5281/zenodo.3229069
- **Source:** DataCite API, Zenodo API

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/space-physics/maidenhead
- **Source:** DataCite API, Zenodo API, PyHC registry

### 4. Software Functionality (MANDATORY)
- **Coordinate Transforms**

**Rationale:** This software provides user-facing coordinate conversions between the Maidenhead grid locator system and WGS84 latitude/longitude coordinates. The public API exposes functions for converting latitude/longitude to Maidenhead locators, converting Maidenhead locators back to latitude/longitude, and representing a Maidenhead grid square as GeoJSON geometry.

### 5. Related Region (MANDATORY)
- **Earth Atmosphere**

**Rationale:** According to PyHC metadata, this package has keywords "ionosphere_thermosphere_mesosphere" and is used for crowdsourced ground-based observations. The Maidenhead coordinate system is primarily used for Earth-based location hashing, particularly relevant to ionosphere and thermosphere observations.

### 6. Authors (MANDATORY)
Authors identified from Zenodo metadata and git history:

1. **Michael Hirsch**
   - Author Identifier: Not found
   - Affiliation: Not found

2. **Kirill Erofeev**
   - Author Identifier: Not found
   - Affiliation: Not found

3. **Andre Pastore**
   - Author Identifier: Not found
   - Affiliation: Bond

4. **powermik**
   - Author Identifier: Not found
   - Affiliation: Not found

5. **Cédric DELAYRE**
   - Author Identifier: Not found
   - Affiliation: Not found

6. **Hilary Jendrasiak**
   - Author Identifier: Not found
   - Affiliation: Not found

7. **Sybrand Strauss**
   - Author Identifier: Not found
   - Affiliation: Not found

8. **flashbanger**
   - Author Identifier: Not found
   - Affiliation: Not found

9. **Henri Kuiper**
   - Author Identifier: Not found
   - Affiliation: Not found

**Primary Contact:** Michael Hirsch (from PyHC registry)
**Source:** Zenodo API, DataCite API, PyHC registry, git history

### 7. Software Name (MANDATORY)
- **Name:** Maidenhead
- **Full Title:** Maidenhead <-> Lat/Lon
- **Source:** PyHC registry, DataCite API, SoMEF, pyproject.toml

### 8. Description (MANDATORY)
Python Maidenhead <--> WGS84 coordinate conversions. This package provides a simple, yet effective location hashing algorithm. Maidenhead provides up to six levels of precision, from world-scale grid cells to approximately 1 m precision, according to the README. The software converts between Maidenhead grid locator strings and WGS84 latitude/longitude coordinates, and can also output GeoJSON geometry. It is particularly useful for amateur radio applications and crowdsourced observations in geospace research.

**Source:** DataCite API, README.md, PyHC registry

### 9. Concise Description (OPTIONAL)
Python Maidenhead <--> WGS84 coordinate conversions, useful for crowdsourced observations.

**Source:** PyHC registry, DataCite API (modified for brevity)

### 10. Publication Date (RECOMMENDED)
- **Date:** 2013-03-05
- **Source:** Git history (first commit); GitHub repository creation date from SoMEF is 2018-05-08

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)
- **Version Number:** v1.8.0
- **Version Date:** 2025-05-25
- **Version Description:** Python >= 3.9. Correct and extended precision
- **Version PID:** https://doi.org/10.5281/zenodo.15509872
- **Source:** Git tags, Zenodo API, SoMEF releases, __init__.py

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (specifically Python >= 3.9 as of v1.8.0)
- **Source:** pyproject.toml, SoMEF, GitHub API

### 14. Reference Publication (RECOMMENDED)
- Not found

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT
- **SPDX Identifier:** MIT
- **Source:** DataCite API, Zenodo API, SoMEF, LICENSE.txt

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- amateur-radio
- geolocation
- maidenhead
- location
- ionosphere_thermosphere_mesosphere
- coordinate conversion
- WGS84
- grid locator

**Source:** SoMEF (GitHub API topics), pyproject.toml, PyHC registry

### 17. Data Sources (OPTIONAL)
- Not applicable (this is a coordinate conversion tool, not a data access tool)

### 18. Input File Formats (RECOMMENDED)
- Not applicable (accepts coordinate values as function parameters, not file inputs)

### 19. Output File Formats (RECOMMENDED)
- **JSON** (geoJSON output capability)
- **Source:** Code analysis (to_geoJSONObject function)

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**
- **Source:** pyproject.toml classifiers, pure Python implementation

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**
- **Source:** Pure Python implementation with no compiled extensions

### 22. Related Phenomena (OPTIONAL)
- Not found (coordinate transformation tool, not phenomena-specific)

### 23. Development Status (RECOMMENDED)
- **Active** (based on recent commits and releases)
- **Maturity:** Production/Stable
- **Source:** pyproject.toml (Development Status :: 5 - Production/Stable), recent git activity (latest release 2025-05-25)

### 24. Documentation (RECOMMENDED)
- **README.md in repository:** https://github.com/space-physics/maidenhead/blob/main/README.md
- No separate documentation site found
- **Source:** Repository examination

### 25. Funder (OPTIONAL)
- Not found

### 26. Award Title (OPTIONAL)
- Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Not found

### 28. Related Datasets (OPTIONAL)
- Not found

### 29. Related Software (OPTIONAL)
- **Open Location Codes (Plus Codes)** - mentioned in README as alternative
  - URL: https://github.com/google/open-location-code/tree/master/python
- **Source:** README.md

### 30. Interoperable Software (OPTIONAL)
- Not found

### 31. Related Instruments (OPTIONAL)
- Not applicable (general-purpose coordinate conversion tool)

### 32. Related Observatories (OPTIONAL)
- Not applicable (general-purpose coordinate conversion tool)

### 33. Logo (OPTIONAL)
- Not found

---

## Additional Metadata Sources Summary

### DataCite API Results
- DOI: 10.5281/zenodo.3229069
- Title: space-physics/maidenhead: Python >= 3.9. Correct and extended precision
- Description: Python Maidenhead <--> WGS84 coordinate conversions
- Creators: 8 authors (scivision, ErofeevK, Andre Pastore, powermik, Cédric DELAYRE, Hilary Jendrasiak, Sybrand Strauss, flashbanger); git history also identifies Michael Hirsch, Kirill Erofeev, and Henri Kuiper by name
- Publisher: Zenodo
- Publication Year: 2025 (latest version)
- License: MIT License
- Version: v1.8.0
- Related identifier (repository): https://github.com/space-physics/maidenhead/tree/v1.8.0

### Zenodo API Results
- Record ID: 15509872 (latest version)
- Concept Record ID: 3229069
- Concept DOI: 10.5281/zenodo.3229069
- Version DOI: 10.5281/zenodo.15509872
- Code Repository: https://github.com/space-physics/maidenhead
- Publication Date: 2025-05-25
- Version: v1.8.0
- License: mit-license
- Access: Open access

### SoMEF Results
- Name: maidenhead
- Full Name: space-physics/maidenhead
- Description: Python Maidenhead <--> WGS84 coordinate conversions
- Owner: space-physics
- Date Created: 2018-05-08T19:06:16Z
- Date Updated: 2025-11-11T16:26:42Z
- License: MIT License
- Programming Language: Python
- Keywords: amateur-radio, geolocation, maidenhead, location
- Stargazers: 26
- Forks: 13
- Repository Status: Not explicitly provided
- Latest Release: v1.8.0 (2025-05-25)
- Identifier: https://zenodo.org/badge/latestdoi/132653071

### PyHC Registry Results
- **Registry:** Unevaluated packages
- Name: Maidenhead
- Code: https://github.com/space-physics/maidenhead
- Description: Python Maidenhead <--> WGS84 coordinate conversions, useful for crowdsourced observations
- Contact: Michael Hirsch
- Keywords: ["ionosphere_thermosphere_mesosphere","specific"]

### Repository File Analysis
- License: MIT License (Copyright 2018 SciVision, Inc.)
- Package Name: maidenhead
- Description (pyproject.toml): Maidenhead Locator, Lat Lon coordinate convertor
- Keywords (pyproject.toml): location, maidenhead
- Python Version Required: >=3.9
- Development Status: Production/Stable
- Operating System: OS Independent
- Current Version: 1.8.0 (from __init__.py)
- Package Type: Console application / Command-line tool
- Scientific Classification: GIS (Geographic Information System)

### Git Repository Analysis
- Repository created: 2013-03-05 (based on first commit)
- GitHub repository created: 2018-05-08 (from SoMEF)
- Latest version: v1.8.0 (2025-05-25)
- Recent versions: v1.7.0, v1.6.0, v1.5.0, v1.4.1
- CI Platform: GitHub Actions
- Testing: pytest
- Code Quality: flake8, mypy
- Test OS: ubuntu-latest (but OS independent)

---

## Metadata Completeness Assessment

### Mandatory Fields - Complete
✓ Code Repository
✓ Software Functionality
✓ Related Region
✓ Authors
✓ Software Name
✓ Description

### Mandatory Fields - To Be Completed by Submitter
- Submitter Name
- Submitter Email

### Recommended Fields - Complete
✓ Persistent Identifier (Concept DOI)
✓ Publication Date
✓ Publisher
✓ Version (Number, Date, Description, PID)
✓ Programming Language
✓ License
✓ Operating System
✓ CPU Architecture
✓ Development Status
✓ Documentation

### Recommended Fields - Not Found
- Reference Publication
- Input File Formats (N/A)
- Output File Formats (JSON only)

### Optional Fields - Found
✓ Keywords
✓ Concise Description
✓ Related Software

### Optional Fields - Not Found
- Data Sources (N/A)
- Related Phenomena
- Funder
- Award Title
- Related Publications
- Related Datasets
- Interoperable Software
- Related Instruments (N/A)
- Related Observatories (N/A)
- Logo

---

## Notes

1. This software is listed in the PyHC unevaluated packages registry, indicating it is used within the heliophysics Python community.

2. The Maidenhead grid locator system is a geocode system used primarily by amateur radio operators but has applications in scientific crowdsourced observations.

3. The software is actively maintained with the latest release in May 2025, requiring Python >= 3.9.

4. Author names from Zenodo are partly GitHub usernames. The metadata uses real names where git history confirms them (Michael Hirsch, Kirill Erofeev, and Henri Kuiper) and preserves remaining Zenodo creator names where fuller names were not found.

5. The software's primary functionality is coordinate transformation, which is fundamental for geolocation in heliophysics research.

6. No formal reference publication (e.g., JOSS paper) was found for this software.

7. The software has a mature development status (Production/Stable) and is actively used (26 stars, 13 forks on GitHub).
