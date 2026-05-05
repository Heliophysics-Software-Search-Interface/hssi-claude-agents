# HSSI Metadata Extraction Results

**Repository:** https://github.com/rilma/pyIRI2016
**Extraction Date:** 2025-12-03
**Validation Update:** 2026-04-24

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.240895
- **Source:** README.md Zenodo DOI badge; Zenodo API record 240895
- **Note:** Version-specific DOI for the archived v1.1.0 software release. The Zenodo API record has conceptrecid 591270 but no populated concept DOI.

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/rilma/pyIRI2016
- **Source:** git remote origin; GitHub repository metadata; Zenodo related identifier

### 4. Software Functionality (MANDATORY)
- **Coordinate Transforms**
- **Coordinate Transforms:Ionospheric**
- **Models and Simulations**
- **Models and Simulations:Empirical**
- **Data Processing and Analysis**
- **Data Processing and Analysis:Analysis**
- **Data Processing and Analysis:Data Access and Retrieval**
- **Data Processing and Analysis:Processing**
- **Data Visualization**
- **Data Visualization:2D Graphics**
- **Data Visualization:Line Plots**

**Rationale:** IRI-2016 is a Python wrapper for the International Reference Ionosphere 2016 empirical ionospheric model. The public API computes ionospheric parameters including electron density, electron temperature, ion temperature, ion densities, NmF2, hmF2, and B0 for height, latitude, longitude, local-time, and 2D profile modes. The package includes retrieval helpers for IRI source/data files, optional ionospheric field-line and IGRF-related calculations, and plotting/example code that generates line plots and 2D pcolor/contour graphics.

**Source:** README.md; pyproject.toml; pyiri2016/__init__.py; pyiri2016/iri2016prof2D.py; pyiri2016/api/update.py; examples/*.py; scripts/*.py; settings/settings.py; source/igrf.for

### 5. Related Region (MANDATORY)
- **Earth Atmosphere**

**Rationale:** The International Reference Ionosphere models the ionosphere, which is part of Earth's upper atmosphere.

**Source:** README.md; pyproject.toml topic classifier; package API and examples

### 6. Authors (MANDATORY)

#### Author 1:
- **Author Name:** Ronald R. Ilma Campana
- **Author Identifier:** Not found
- **Affiliation - Organization:** Cornell University
- **Affiliation - Identifier:** https://ror.org/05bnh6r87
- **Source:** pyproject.toml author field; Zenodo creator "Ronald Ilma" with Cornell University affiliation; LICENSE.md copyright holder
- **Note:** Zenodo and the license use the shorter name "Ronald Ilma"; pyproject.toml gives the fuller current package-author form.

### 7. Software Name (MANDATORY)
- **Name:** IRI-2016
- **Source:** PyHC registry / Google sheet official software name supplied for this validation workflow
- **Note:** The repository, Python package, and README use the alternate name pyIRI2016.

### 8. Description (MANDATORY)
- **Description:** Python wrapper for the International Reference Ionosphere (IRI) 2016 model. The package computes empirical ionospheric parameters including electron density, electron temperature, ion temperature, ion densities, NmF2, hmF2, and B0 as functions of location, time, altitude, and solar/geomagnetic conditions. It supports height, latitude, longitude, local-time, and 2D profile workflows, includes helpers for retrieving IRI-related source and coefficient files, and provides example plotting workflows for line plots and 2D maps.
- **Source:** README.md; pyproject.toml; pyiri2016/__init__.py; pyiri2016/iri2016prof2D.py; pyiri2016/api/update.py; examples/README.md

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Python wrapper for the International Reference Ionosphere 2016 empirical ionospheric model.
- **Source:** README.md; pyproject.toml; Zenodo API record 240895

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2017-01-12
- **Source:** Zenodo API record 240895 publication_date; v1.1.0 git tag date

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Zenodo API record 240895

### 12. Version (RECOMMENDED)

#### Version v1.2.0 (current repository release):
- **Version Number:** v1.2.0
- **Version Date:** 2026-02-21
- **Version Description:** Upgrade to Python 3.11; adds TimeUtilities fallback and explicit timeutil dependency; removes obsolete Poetry/Meson/legacy build artifacts.
- **Version PID:** Not found
- **Source:** GitHub release v1.2.0; git tag v1.2.0; pyproject.toml version 1.2.0; CHANGELOG.md

#### Version v1.1.0 (archived DOI release):
- **Version Number:** v1.1.0
- **Version Date:** 2017-01-12
- **Version Description:** Official release of the IRI2016 wrapper in Python, archived on Zenodo.
- **Version PID:** https://doi.org/10.5281/zenodo.240895
- **Source:** Zenodo API record 240895; README.md DOI badge; git tag v1.1.0; CHANGELOG.md

#### Version note:
The current repository version and latest GitHub release are v1.2.0, while the available Zenodo DOI is for v1.1.0. No DOI for v1.2.0 was found.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x**
- **Fortran77**

**Source:** pyproject.toml requires Python >=3.11; source/*.for contains Fortran source; CMakeLists.txt builds a Fortran extension through f2py/scikit-build-core.

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication DOI:** Not found
- **Note:** No software reference publication DOI was found in README.md, pyproject.toml, repository citation files, or Zenodo metadata. Scientific DOIs appear in bundled IRI/Fortran source comments but do not describe this Python wrapper as a software publication.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html
- **SPDX ID:** MIT
- **Source:** LICENSE.md; pyproject.toml; GitHub repository license metadata

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- atmospheric-modelling
- f2py
- fortran
- ionosphere
- ionosphere-modeling
- python
- standard
- electron density
- electron temperature
- ion temperature
- IRI
- International Reference Ionosphere
- empirical model
- ionospheric physics
- CMake
- scikit-build-core

**Source:** GitHub repository topics; README.md; pyproject.toml; CHANGELOG.md

### 17. Data Sources (OPTIONAL)
- **HTTP/HTTPS Directories**
- **Other** (bundled IRI coefficient and index files)

**Note:** The package includes IRI coefficient/index data files and has a retrieval helper for remote IRI/Common Files/index archives.

**Source:** data/ccir; data/igrf; data/index; data/mcsat; data/ursi; pyiri2016/api/update.py; settings/settings.py; CHANGELOG.md

### 18. Input File Formats (RECOMMENDED)
- **ascii**

**Source:** Bundled .asc and .dat IRI coefficient/index files in data/ccir, data/igrf, data/index, data/mcsat, and data/ursi.

### 19. Output File Formats (RECOMMENDED)
- **Other** (PNG figures from plotting/example workflows)

**Note:** The core model API returns Python dictionaries and NumPy arrays rather than writing science-data files. Plotting and example workflows save PNG graphics.

**Source:** examples/*.py; scripts/*.py; pyiri2016/iri2016prof2D.py

### 20. Operating System (RECOMMENDED)
- **Operating System Independent**

**Rationale:** The package is a Python 3.11+ project with a CMake/scikit-build-core build and compiled Fortran extension. It should be portable to systems with Python 3.11, NumPy, CMake, and a Fortran compiler.

**Source:** README.md; QUICKSTART.md; pyproject.toml; CMakeLists.txt; Makefile

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Rationale:** The software uses Python, NumPy, and compiled Fortran/C extension code without GPU-specific or architecture-specific requirements.

**Source:** pyproject.toml; CMakeLists.txt; repository source files

### 22. Related Phenomena (OPTIONAL)
- Not found in controlled vocabularies

**Note:** The software models ionospheric quantities such as electron density, electron/ion temperature, ion composition, NmF2, hmF2, B0, and total electron content, but no controlled related-phenomena term was identified in the available HSSI guidance.

### 23. Development Status (RECOMMENDED)
- **Active**

**Rationale:** The repository has a stable package release v1.2.0 dated 2026-02-21, current pyproject metadata, modernized CMake/scikit-build-core build configuration, updated CI, and recent changelog entries. As of validation on 2026-04-24, the latest release and push were recent.

**Source:** GitHub release v1.2.0; git tag v1.2.0; GitHub repository metadata; CHANGELOG.md; pyproject.toml

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/rilma/pyIRI2016

**Note:** Documentation is provided through README.md, QUICKSTART.md, and examples/README.md in the repository. No separate documentation site was found.

**Source:** README.md; QUICKSTART.md; examples/README.md

### 25. Funder (OPTIONAL)
- Not found

**Source:** Zenodo API record 240895; repository files

### 26. Award Title (OPTIONAL)
- Not found

**Source:** Zenodo API record 240895; repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Not found

**Source:** Repository search; README.md; pyproject.toml; Zenodo API record 240895

### 28. Related Datasets (OPTIONAL)
- Not found

**Source:** Repository search; Zenodo API record 240895

### 29. Related Software (OPTIONAL)

#### Related Software 1:
- **Name/Repository:** TimeUtilities
- **URL:** https://github.com/rilma/TimeUtilities
- **Relationship:** Required dependency
- **Source:** README.md; pyproject.toml; CHANGELOG.md

#### Related Software 2:
- **Name/Repository:** space-physics/iri2016
- **URL:** https://github.com/space-physics/iri2016
- **Relationship:** Alternative Python implementation/wrapper for the IRI model
- **Source:** PyHC registry / Google sheet context supplied for this validation workflow

### 30. Interoperable Software (OPTIONAL)
- Not found

**Source:** Repository examination; no explicit interoperability statement found

### 31. Related Instruments (OPTIONAL)
- Not found

**Note:** IRI-2016 is a general ionospheric model and is not tied to a specific instrument.

### 32. Related Observatories (OPTIONAL)
- Not found

**Note:** IRI-2016 is a general ionospheric model and is not tied to a specific observatory.

### 33. Logo (OPTIONAL)
- Not found

**Source:** Repository examination; no logo asset or URL found

---

## Metadata Quality Notes

### PyHC/HSSI Naming
- **Official HSSI Software Name:** IRI-2016
- **Repository/package alternate name:** pyIRI2016
- **Note:** Field 7 intentionally uses the PyHC/HSSI software-sheet name rather than the repository or import-package name.

### Completeness Assessment
- **MANDATORY fields:** All filled or marked for user completion
- **RECOMMENDED fields:** Filled where evidence was available; Reference Publication and v1.2.0 DOI remain not found
- **OPTIONAL fields:** Filled where evidence was available

### Verification Status
- Zenodo API: Verified for DOI and v1.1.0 archival metadata
- GitHub API: Verified for repository metadata and latest v1.2.0 release
- Repository Examination: Completed against refreshed main branch
- Code Analysis: Completed for public API, retrieval helper, build system, examples, and plotting workflows

---

**End of Metadata Extraction**
