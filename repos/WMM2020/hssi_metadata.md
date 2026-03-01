# HSSI Metadata Extraction Results

**Repository:** https://github.com/space-physics/WMM2020
**Extraction Date:** 2025-12-04

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/WMM2020

### 4. Software Functionality (MANDATORY)
- Models and Simulations:Empirical
- Data Visualization:2D Graphics
- Data Processing and Analysis:Analysis

**Source:** The World Magnetic Model (WMM2020) is an empirical model of Earth's magnetic field. The software computes magnetic field components (north, east, down, total intensity, declination, inclination) at specified geographic coordinates. It includes visualization capabilities for creating contour plots of magnetic declination and inclination.

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Atmosphere

**Source:** WMM models Earth's magnetic field, which is fundamental to the magnetosphere. The magnetic field also affects the ionosphere (part of Earth's atmosphere). PyHC registry categorizes this as "ionosphere_thermosphere_mesosphere".

### 6. Authors (MANDATORY)
- **Authors:** Michael Hirsch, Ph.D.
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Source:** From setup.cfg author field and PyHC registry contact field.

### 7. Software Name (MANDATORY)
WMM2020

**Source:** PyHC registry, SoMEF, README.md, and setup.cfg all confirm this name (case-insensitive variations: wmm2020).

### 8. Description (MANDATORY)
WMM2020 World Magnetic Model in simple, object-oriented Python. This Python package provides a wrapper for the World Magnetic Model 2020, which is used to compute Earth's magnetic field components including declination, inclination, and total field intensity at any point on or above Earth's surface. The software is tested on Linux, Mac and Windows with most C compilers. It uses a build-on-run technique where the C code is compiled on first use. The package provides functions for single-point calculations, grid calculations, and arbitrary path transects through the magnetic field model, with visualization capabilities for creating contour maps of magnetic parameters.

**Source:** Combined from README.md, SoMEF description, and setup.cfg description.

### 9. Concise Description (OPTIONAL)
WMM2020 geomagnetic model in Python - computes Earth's magnetic field components with simple object-oriented interface.

**Source:** Adapted from SoMEF and setup.cfg descriptions.

### 10. Publication Date (RECOMMENDED)
2020-06-10

**Source:** From SoMEF date_created and git repository creation date.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Repository is hosted on GitHub without DOI/Zenodo integration.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.1.1
- **Version Date:** 2020-11-17
- **Version Description:** Allow CMake >= 3.10; bugfix to prevent rebuilding on each import; enhance build and add single point calculation and tests
- **Version PID:** Not found

**Source:** From setup.cfg (version 1.1.1), SoMEF releases, and git tags. Combined release notes from v1.1.1 and v1.1.0.

### 13. Programming Language (RECOMMENDED)
- C
- Python 3.x

**Source:** From SoMEF programming_languages (C and Python are the primary languages; CMake, Meson, and Makefile are build tools). Setup.cfg specifies Python >= 3.7.

### 14. Reference Publication (RECOMMENDED)
Not found

**Source:** No JOSS paper or similar publication found in repository.

### 15. License (RECOMMENDED)
- **License:** Public Domain
- **License URI:** https://www.ngdc.noaa.gov/geomag/WMM/license.shtml

**Source:** From LICENSE.txt - "The WMM source code is in the public domain and not licensed or under copyright." The original WMM code from NOAA/NGDC is public domain.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- geomagnetic
- build-on-run
- ionosphere_thermosphere_mesosphere
- World Magnetic Model
- magnetic field
- declination
- inclination

**Source:** From setup.cfg keywords, SoMEF keywords, and PyHC registry keywords.

### 17. Data Sources (OPTIONAL)
Not found

**Source:** The software uses the WMM coefficient file (WMM.COF) which is embedded in the package, but does not retrieve data from external sources.

### 18. Input File Formats (RECOMMENDED)
Not applicable

**Source:** The software primarily accepts numeric inputs (latitude, longitude, altitude, year) rather than data files. The WMM coefficient file is internal to the package.

### 19. Output File Formats (RECOMMENDED)
Not found

**Source:** The software returns xarray.Dataset or dict objects in Python. No explicit file output functionality documented, though users could save results using standard Python methods.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source:** From README.md "Tested on Linux, Mac and Windows" and CI/CD configuration testing on ubuntu-latest, macos-latest, and windows-latest.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- CPU Independent

**Source:** Python code with C extensions; CI/CD uses standard GitHub runners (x86-64). The C code should be portable to other architectures but not explicitly tested.

### 22. Related Phenomena (OPTIONAL)
Not found

**Source:** No specific phenomena keywords found in repository. The software models geomagnetic field in general rather than specific phenomena.

### 23. Development Status (RECOMMENDED)
Active

**Source:** From setup.cfg: "Development Status :: 5 - Production/Stable" indicates the software has reached a stable, usable state. The repository shows recent updates (date_updated: 2025-06-11) indicating active maintenance.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/WMM2020

**Source:** No separate documentation site found. README.md in the repository serves as primary documentation with installation and usage instructions.

### 25. Funder (OPTIONAL)
Not found

**Source:** No funding information in repository.

### 26. Award Title (OPTIONAL)
Not found

**Source:** No award information in repository.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

**Source:** No publications citing or describing this specific Python implementation found in repository. The README references NOAA/NGDC technical documentation:
- WMM2020 inclination map: https://www.ngdc.noaa.gov/geomag/WMM/data/WMM2020/WMM2020_I_MERC.pdf
- WMM2020 declination map: https://www.ngdc.noaa.gov/geomag/WMM/data/WMM2020/WMM2020_D_MERC.pdf

### 28. Related Datasets (OPTIONAL)
Not found

**Source:** The software embeds the WMM coefficient file internally rather than using external datasets.

### 29. Related Software (OPTIONAL)
- https://github.com/space-physics/WMM2015

**Source:** From README.md - "WMM2015 is also available" with link to predecessor version.

### 30. Interoperable Software (OPTIONAL)
- xarray
- numpy

**Source:** From setup.cfg install_requires and code imports. These are dependencies that the software interoperates with.

### 31. Related Instruments (OPTIONAL)
Not found

**Source:** WMM is a model rather than instrument-specific software, though it may be used to calibrate magnetometers.

### 32. Related Observatories (OPTIONAL)
Not found

**Source:** No specific observatory affiliations found, though WMM is developed by NOAA/NGDC.

### 33. Logo (OPTIONAL)
Not found

**Source:** No logo URL found in repository or PyHC registry entry.

---

## Additional Notes

### Data Collection Summary

**Automated Extraction:**
1. **DOI Search:** No DOI found (confirmed by user)
2. **SoMEF:** Successfully extracted metadata including repository info, programming languages, releases, keywords, and descriptions
3. **PyHC Registry:** Found in unevaluated packages list with name, description, contact, and keywords

**Manual Examination:**
- README.md: Software description, installation, usage, operating system compatibility
- setup.cfg: Author, version, dependencies, development status, Python version requirements
- LICENSE.txt: Public domain status
- .github/workflows/ci.yml: Operating system testing (Linux, Mac, Windows)
- Git history: Version dates and release information
- Source code analysis: Software functionality (empirical model, visualization, analysis)

### Metadata Source Priority

Following the recommended priority order:
1. **PyHC metadata** (manually curated): Used for keywords, contact, general description
2. **Manual examination** (setup.cfg, LICENSE, README): Used for author, version, license, OS compatibility
3. **SoMEF** (automated): Used for repository metadata, programming languages, dates
4. **Git analysis**: Used for version dates and release chronology

### Completeness Assessment

**Mandatory fields completed:** 6/7 (missing only Submitter, which requires actual submitter input)

**Recommended fields completed:** 9/14
- Found: Code Repository, Version, Programming Language, License, Operating System, CPU Architecture, Development Status, Documentation, Input File Formats
- Not found: Persistent Identifier, Publication Date (inferred from git), Publisher (inferred), Reference Publication, Output File Formats

**Optional fields completed:** 3/11
- Found: Keywords, Related Software, Interoperable Software
- Not found: Concise Description (created from available info), Data Sources, Related Phenomena, Funder, Award Title, Related Publications, Related Datasets, Related Instruments, Related Observatories, Logo

---

## Verification Pass Results

**Date:** 2025-12-04

### Correctness Verification

✓ **URLs verified:**
- Repository URL (https://github.com/space-physics/WMM2020): Accessible (HTTP 200)
- Related software URL (https://github.com/space-physics/WMM2015): Accessible (HTTP 200)

⚠️ **URLs with issues:**
- NOAA WMM2020 inclination map (https://www.ngdc.noaa.gov/geomag/WMM/data/WMM2020/WMM2020_I_MERC.pdf): Returns 404
- NOAA WMM2020 declination map (https://www.ngdc.noaa.gov/geomag/WMM/data/WMM2020/WMM2020_D_MERC.pdf): Returns 404

**Note:** The NOAA PDF map URLs referenced in the README are no longer accessible. These resources may have been moved or removed as the WMM2020 model expired on December 31, 2024, and WMM2025 was released on December 17, 2024. Alternative resources are available at:
- Main WMM page: https://www.ngdc.noaa.gov/geomag/WMM/calculators.shtml
- ArcGIS WMM2020 map: https://oceans-esrioceans.hub.arcgis.com/datasets/noaa::magnetic-declination-from-world-magnetic-model-wmm2020

✓ **Dates:** All dates formatted correctly (YYYY-MM-DD format)

✓ **Author names:** Formatted properly (Given name, initials if any, surname)

✓ **License:** Verified as public domain per LICENSE.txt

### Verifiability Assessment

All metadata can be traced back to verifiable sources:
- ✓ Repository metadata: GitHub API and repository contents
- ✓ Author information: setup.cfg and PyHC registry
- ✓ Version information: Git tags, setup.cfg, and SoMEF releases
- ✓ Programming languages: SoMEF and repository file analysis
- ✓ Operating systems: README.md and CI/CD configuration
- ✓ License: LICENSE.txt file in repository
- ✓ Keywords: setup.cfg, SoMEF, and PyHC registry

### Exhaustiveness Review

**Software Functionality:**
✓ Thoroughly analyzed. The three selected categories (Models and Simulations:Empirical, Data Visualization:2D Graphics, Data Processing and Analysis:Analysis) accurately represent the software's capabilities:
- Empirical model of Earth's magnetic field
- Visualization with contour plots
- Analysis of magnetic field components

**Related Region:**
✓ Both applicable regions identified:
- Earth Magnetosphere (primary - models Earth's magnetic field)
- Earth Atmosphere (secondary - magnetic field affects ionosphere)

**Authors:**
✓ Primary author identified (Michael Hirsch, Ph.D.)
⚠️ **Note:** Git history shows additional contributors (Aaron Nielsen with 2 commits, Andrey Korzh with 1 commit, Antoine T with 1 commit), but the official package metadata (setup.cfg) only lists Michael Hirsch as the author. Following standard practice of using official package metadata for authorship.

**Keywords:**
✓ Comprehensive keywords captured from multiple sources (setup.cfg, SoMEF, PyHC registry)

**Programming Languages:**
✓ Primary languages identified (C and Python). Build tools (CMake, Meson, Makefile) were noted but not included as programming languages per field definition.

### Completeness Check

**All 33 form fields addressed:** ✓
- Mandatory fields: 6/7 completed (Submitter requires actual submitter input)
- Recommended fields: 9/14 completed
- Optional fields: 10/12 addressed (8 marked "Not found", 2 populated)

**Multi-entry fields:**
- ✓ Authors: Listed (only 1 found in official metadata)
- ✓ Keywords: Multiple keywords from various sources
- ✓ Software Functionality: All applicable functionalities identified
- ✓ Related Region: All applicable regions identified
- ✓ Programming Languages: All significant languages listed
- ✓ Operating System: All tested systems listed

### Final Verification Checklist

- [x] All automated extraction methods attempted
- [x] Repository thoroughly examined manually
- [x] All 33 form fields addressed
- [x] MANDATORY fields have values (except Submitter)
- [x] Software Functionality exhaustively analyzed
- [x] Related Region exhaustively analyzed
- [x] Second verification pass completed
- [x] Metadata sources are verifiable
- [x] Format matches required structure
- [x] URLs validated (noted broken URLs in Related Publications section)

**Status:** Metadata extraction complete and verified. Ready for submission (after submitter information is added).
