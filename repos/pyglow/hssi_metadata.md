# HSSI Metadata Extraction Results

**Repository:** https://github.com/timduly4/pyglow
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** Not found

**Notes:** No DOI found in repository files (no CITATION.cff, no DOI badges in README, no Zenodo integration detected).

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/timduly4/pyglow

**Source:** Repository URL, SoMEF extraction, PyHC registry

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Field-line Tracing
- Models and Simulations:Empirical
- Models and Simulations:Field-line Tracing

**Notes:**
- **Coordinate Transforms:** Package includes coordinate conversion functionality (coord.py, location_time.py with LLA-to-ECEF, ECEF-to-LLA, VEN-to-ECEF transformations)
- **Data Access and Retrieval:** Provides access to geophysical indices (AP, Kp, F10.7, DST, AE) via automatic downloading and updating (update_indices() function)
- **Field-line Tracing:** Geomagnetic field-line tracing using IGRF model (Line() function traces along magnetic field lines, pyglow.py:530-553)
- **Empirical Models:** Wraps multiple empirical climatological models:
  - HWM (Horizontal Wind Model) versions 1993, 2007, 2014 - provides horizontal wind velocities
  - IGRF (International Geomagnetic Reference Field) versions 11, 12 - provides magnetic field vectors
  - IRI (International Reference Ionosphere) versions 2012, 2016 - provides electron density, ion density, temperatures
  - MSIS (Mass Spectrometer and Incoherent Scatter Radar) 2000 - provides neutral density, composition, temperature
- **Airglow Emission Calculations:** Computes 630.0-nm and 777.4-nm airglow volume emission rates (run_airglow() method, pyglow.py:308-387)

**Source:** Analysis of README.md, source code (pyglow.py, hwm.py, igrf.py, iri.py, msis.py, coord.py), __init__.py public API, and example files

### 5. Related Region (MANDATORY)
**Value:** Earth Atmosphere

**Notes:** Specifically focused on the ionosphere, thermosphere, and mesosphere regions of Earth's atmosphere. The models wrapped by pyglow (HWM, IGRF, IRI, MSIS) are all upper atmosphere models operating in the 85-1000+ km altitude range.

**Source:** README.md description, PyHC registry keywords ("ionosphere_thermosphere_mesosphere"), example files showing altitude ranges

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Timothy M. Duly (Timothy Duly)
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Notes:**
- Primary author identified from setup.py (author='Timothy M. Duly', author_email='timduly4@gmail.com')
- PyHC registry lists contact as "Timothy Duly"
- SoMEF found email: timduly4@gmail.com
- No ORCID or institutional affiliation found in repository
- Copyright notice in LICENSE shows "Copyright (c) 2016 Timothy Duly"

**Source:** setup.py:144-145, License.md:3, PyHC registry, SoMEF output

### 7. Software Name (MANDATORY)
**Value:** pyglow

**Source:** Repository name, setup.py:142, README.md, PyHC registry, SoMEF output

### 8. Description (MANDATORY)
**Value:** pyglow is a Python module that wraps several upper atmosphere climatological models written in FORTRAN, such as the Horizontal Wind Model (HWM), the International Geomagnetic Reference Field (IGRF), the International Reference Ionosphere (IRI), and the Mass Spectrometer and Incoherent Scatter Radar (MSIS). It includes HWM 1993/2007/2014, IGRF 11/12, IRI 2012/2016, and MSIS 2000. pyglow offers access to these models and geophysical indices (AP, Kp, F10.7, DST, AE) in a convenient, high-level object-oriented interface within Python.

**Source:** README.md lines 11-31, GitHub API description (via SoMEF), PyHC registry

### 9. Concise Description (OPTIONAL)
**Value:** Upper atmosphere climatological models in Python

**Source:** GitHub repository description (via SoMEF output)

### 10. Publication Date (RECOMMENDED)
**Value:** 2013-08-09

**Notes:** Date the repository was created on GitHub

**Source:** SoMEF output (date_created field from GitHub API)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Notes:** No DOI found, so the repository is hosted on GitHub without formal publication through a service like Zenodo.

**Source:** Code repository location

### 12. Version (RECOMMENDED)
- **Version Number:** Not found
- **Version Date:** 2025-12-01
- **Version Description:** Not found
- **Version PID:** Not found

**Notes:**
- Repository has no git tags for versioning
- No version information found in setup.py or __init__.py
- Last update date from GitHub API: 2025-12-01T22:19:37Z
- README.md (line 63) mentions the package is "far behind on maintenance" as of April 2023

**Source:** Git tag check (no tags found), SoMEF output (date_updated field)

### 13. Programming Language (RECOMMENDED)
**Values:**
- Fortran77
- Fortran90
- Python 3.x

**Notes:**
- Primary language is Python 3 for the interface
- Wraps FORTRAN models (Fortran 77/90) via f2py
- Language statistics from GitHub: Fortran (405,001 bytes), Python (109,604 bytes), Makefile (9,515 bytes), Dockerfile (608 bytes)
- README troubleshooting section notes incompatibility with Python 3.10, recommending Python 3.8

**Source:** SoMEF output (programming_languages from GitHub API), setup.py (uses f2py and fortran compilation flags), README.md:60

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Notes:** No reference publication, JOSS paper, or preferred citation found in repository.

**Source:** Searched for CITATION files, DOI references, and publication mentions in README

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT

**Notes:** Full license text available in License.md file. Copyright (c) 2016 Timothy Duly.

**Source:** License.md, SoMEF output (license field with SPDX ID "MIT"), GitHub API

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- ionosphere_thermosphere_mesosphere
- specific
- upper atmosphere
- climatological models
- geophysical indices
- HWM
- IGRF
- IRI
- MSIS
- airglow

**Notes:**
- First two keywords from PyHC registry
- Additional keywords derived from README description and model names
- "specific" in PyHC context indicates mission/instrument-specific or model-specific software

**Source:** PyHC registry keywords, README.md, model documentation

### 17. Data Sources (OPTIONAL)
**Values:**
- Other

**Notes:** pyglow downloads geophysical indices from various sources as part of its update_indices() functionality, but the specific data source websites are embedded in the code rather than being a standard data source like CDAWeb or HAPI.

**Source:** README.md:162-180, indice_maintenance.py

### 18. Input File Formats (RECOMMENDED)
**Values:**
- ascii

**Notes:** The geophysical indices are stored as ASCII data files (in kpap/, dst/, ae/ directories). The wrapped FORTRAN models also use ASCII data files (.dat, .asc, .for extensions).

**Source:** Directory analysis (kpap/, dst/, ae/ folders), setup.py data_files listing

### 19. Output File Formats (RECOMMENDED)
**Value:** Not found

**Notes:** pyglow primarily provides data through Python objects (Point class) rather than writing output files. Users can export results using standard Python file I/O, but no specific output format is enforced by the package.

**Source:** Example files showing in-memory data access, no file writing functionality in main code

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac

**Notes:**
- README installation instructions reference Linux commands (apt-get)
- macOS specifically mentioned in README:128 for installation path
- Requires gfortran compiler which is readily available on Linux/Mac
- No explicit Windows support mentioned, though Windows may work with appropriate Fortran compiler
- Docker support available for cross-platform compatibility

**Source:** README.md:37 (Linux apt-get), README.md:128 (macOS path example), README.md:143-154 (Docker), setup.py compilation requirements

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Notes:** Python/Fortran code should run on standard CPU architectures. No GPU or HPC-specific requirements mentioned.

**Source:** Code analysis

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found

**Notes:** While the package models upper atmosphere phenomena (ionospheric density, winds, magnetic fields), specific phenomena are not explicitly listed in the repository documentation. The models provide general climatological conditions rather than focusing on specific phenomena like auroras or geomagnetic storms.

**Source:** README.md and model documentation review

### 23. Development Status (RECOMMENDED)
**Value:** Inactive

**Notes:**
- PyHC registry rates software_maturity as "Good" but community and documentation as "Requires improvement"
- README.md:59-63 includes troubleshooting note dated April 2023 stating "pyglow is far behind on maintenance" and "A solution to Issue #139 is sorely needed"
- Last commit: 2025-12-01 (recent), but maintenance issues noted
- Most appropriate status is "Inactive" - reached stable usable state but no longer actively developed, support provided as time allows

**Source:** PyHC registry quality ratings, README.md:59-63, git log

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/timduly4/pyglow/wiki

**Notes:** Documentation is available on the GitHub wiki. PyHC registry rates documentation as "Requires improvement".

**Source:** README.md:193 link, SoMEF output (documentation field), PyHC registry documentation rating

### 25. Funder (OPTIONAL)
**Value:** Not found

**Notes:** No funding information found in repository.

**Source:** Searched README, setup.py, and repository files

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Notes:** No grant or award information found in repository.

**Source:** Searched README, setup.py, and repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found

**Notes:** No related publications found in repository.

**Source:** Searched README and repository files

### 28. Related Datasets (OPTIONAL)
**Values:**
- Geophysical indices datasets (Kp, AP, F10.7, DST, AE)

**Notes:** While specific dataset DOIs are not provided, the package relies on and provides access to standard geophysical indices datasets. The update_indices() function downloads these from authoritative sources.

**Source:** README.md:162-180, geophysical_indices.py

### 29. Related Software (OPTIONAL)
**Values:**
- HWM (Horizontal Wind Model) - FORTRAN models wrapped by pyglow
- IGRF (International Geomagnetic Reference Field) - FORTRAN models wrapped by pyglow
- IRI (International Reference Ionosphere) - FORTRAN models wrapped by pyglow
- MSIS (NRLMSISE-00) - FORTRAN model wrapped by pyglow

**Notes:** These are the upstream FORTRAN models that pyglow wraps to provide Python access. pyglow is essentially a Python interface to these existing models.

**Source:** README.md:13-22, setup.py model list

### 30. Interoperable Software (OPTIONAL)
**Values:**
- numpy
- python-dateutil
- matplotlib (used in examples)

**Notes:** Listed dependencies from requirements.txt. Package integrates with standard scientific Python ecosystem.

**Source:** requirements.txt, examples/

### 31. Related Instruments (OPTIONAL)
**Value:** Not found

**Notes:** This is a general-purpose modeling package not specific to any particular instrument.

**Source:** Package analysis

### 32. Related Observatories (OPTIONAL)
**Value:** Not found

**Notes:** This is a general-purpose modeling package not specific to any particular mission or observatory.

**Source:** Package analysis

### 33. Logo (OPTIONAL)
**Value:** https://raw.githubusercontent.com/timduly4/pyglow/master/logo.png

**Notes:** Logo shows airglow image from ISS. Also available via PyHC registry with alternate camo.githubusercontent.com URL.

**Source:** README.md:5, PyHC registry, SoMEF output

---

## Metadata Sources Summary

**Automated Extraction:**
1. **SoMEF:** Provided software name, description, license, repository URL, programming languages, dates, logo, documentation URL, requirements, and GitHub statistics
2. **PyHC Registry:** Confirmed package listing, provided contact name, keywords, quality ratings, and logo URL
3. **No DOI found:** DataCite and Zenodo API queries were not applicable

**Manual Extraction:**
1. **README.md:** Software description, model versions, geophysical indices, installation requirements, documentation link, development status notes
2. **setup.py:** Author name, author email, package name, repository URL, model list, dependencies
3. **License.md:** License type, copyright holder, copyright year
4. **Source code analysis:** Software functionality (coordinate transforms, data access, empirical models), related region (upper atmosphere)
5. **Example files:** Usage patterns, altitude ranges, functionality demonstration
6. **Git history:** Creation date, recent activity, lack of version tags

---

## Verification Notes

**Completeness Check:**
- ✅ All 33 form fields addressed
- ✅ All MANDATORY fields have values
- ✅ Most RECOMMENDED fields have values
- ⚠️ Some OPTIONAL fields marked as "Not found" where data was not available

**Accuracy Check:**
- ✅ All URLs verified as valid GitHub links
- ✅ Author information confirmed across multiple sources
- ✅ Software functionality verified through code analysis
- ✅ Related region confirmed through PyHC keywords and model descriptions
- ✅ License SPDX ID confirmed
- ⚠️ No version number available (package lacks formal versioning)
- ⚠️ No DOI or formal publication

**Exhaustiveness Check:**
- ✅ Software Functionality: Identified coordinate transforms, data access/retrieval, and empirical models
- ✅ Related Region: Confirmed Earth Atmosphere (ionosphere/thermosphere/mesosphere)
- ✅ Programming Languages: All major languages identified (Python, Fortran77, Fortran90)
- ✅ Keywords: Comprehensive list from PyHC and model names
- ⚠️ Author affiliation unknown (no institutional information in repository)

**Priority Metadata Status:**
- ✅ MANDATORY fields: All complete
- ⚠️ RECOMMENDED fields: Missing version number, version PID, reference publication, author identifier, author affiliation
- ℹ️ OPTIONAL fields: Many not found, which is acceptable

---

## Extraction Challenges

1. **No formal versioning:** Repository lacks git tags or version numbers in code
2. **No DOI:** Package has not been published to Zenodo or similar DOI-issuing service
3. **Limited author information:** No ORCID or institutional affiliation provided
4. **No citation file:** No CITATION.cff or similar citation guidance
5. **Maintenance concerns:** README notes package is "far behind on maintenance" as of April 2023
6. **Documentation limitations:** PyHC registry notes documentation "Requires improvement"

---

## Recommendations for Package Maintainers

If the package maintainers wish to improve metadata for HSSI submission:

1. **Add versioning:** Use git tags to mark releases
2. **Obtain a DOI:** Publish to Zenodo to get a persistent identifier
3. **Create CITATION.cff:** Provide clear citation guidance
4. **Add author ORCIDs:** Include author identifiers in repository
5. **Document affiliations:** Add institutional affiliations for authors
6. **Improve documentation:** Address documentation gaps noted by PyHC
7. **Add reference publication:** Consider publishing a software paper (e.g., JOSS)
8. **Update README:** Add DOI badge, citation information, and version information
