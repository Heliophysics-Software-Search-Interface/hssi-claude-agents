# HSSI Metadata Extraction Results

**Repository:** https://github.com/rilma/pyIRI2016
**Extraction Date:** 2025-12-03

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.240895
- **Source:** DataCite API, Zenodo badge in README.md
- **Note:** This is the DOI for version v1.1.0. The concept DOI was not found in the Zenodo API response.

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/rilma/pyIRI2016
- **Source:** DataCite API, SoMEF, manual examination

### 4. Software Functionality (MANDATORY)
- **Coordinate Transforms**
- **Coordinate Transforms:Ionospheric**
- **Models and Simulations**
- **Models and Simulations:Empirical**
- **Models and Simulations:Physics-Based**
- **Data Processing and Analysis**
- **Data Processing and Analysis:Analysis**

**Rationale:** pyIRI2016 is a Python wrapper for the International Reference Ionosphere (IRI) 2016 model, which is an empirical, physics-based model of the Earth's ionosphere. The software computes electron density (Ne), electron temperature (Te), ion temperature (Ti), and ion densities (O+, H+, N+, He+, O2+, NO+, cluster ions). It provides various profile types (height, latitude, longitude, time) for analysis purposes. The underlying code includes coordinate transformations between geographic and geomagnetic (Corrected Geomagnetic - CGM) coordinate systems, which are essential for ionospheric research.

**Source:** Manual code examination of pyiri2016/__init__.py, README.md, setup.py, and source/igrf.for (contains GEODIP subroutine for geographic-geomagnetic coordinate conversions)

### 5. Related Region (MANDATORY)
- **Earth Atmosphere**

**Rationale:** The IRI2016 model specifically models the ionosphere, which is part of Earth's upper atmosphere (approximately 60-1000 km altitude). The software is designed for ionospheric research.

**Source:** Software description, model domain knowledge

### 6. Authors (MANDATORY)

#### Author 1:
- **Author Name:** Ronald Ilma
- **Author Identifier:** Not found
- **Affiliation - Organization:** Cornell University
- **Affiliation - Identifier:** https://ror.org/05bnh6r87
- **Source:** DataCite API, Zenodo API, LICENSE.md (Copyright 2017 Ronald Ilma)

#### Author 2:
- **Author Name:** Ronald R. Ilma Campana
- **Author Identifier:** Not found
- **Affiliation - Organization:** Not found
- **Affiliation - Identifier:** Not found
- **Source:** SoMEF (from pyproject.toml)
- **Note:** This appears to be the same person as Author 1, with full name in pyproject.toml

#### Author 3:
- **Author Name:** Michael Hirsch
- **Author Identifier:** Not found
- **Affiliation - Organization:** Not found
- **Affiliation - Identifier:** Not found
- **Source:** setup.py (listed as co-author)
- **Note:** Listed as "Michael Hirsch, Ph.D." in setup.py

### 7. Software Name (MANDATORY)
- **Name:** pyIRI2016
- **Source:** DataCite API, Zenodo API, SoMEF, repository name, README.md

### 8. Description (MANDATORY)
- **Description:** Python wrapper for the International Reference Ionosphere (IRI) 2016 model. The IRI2016 model provides empirical predictions of ionospheric parameters including electron density (Ne), electron temperature (Te), ion temperature (Ti), and ion densities for various species (O+, H+, N+, He+, O2+, NO+, cluster ions). The software supports various profile types including height profiles, latitudinal profiles, longitudinal profiles, and time profiles. It enables users to compute ionospheric parameters as a function of location, time, altitude, and solar/geomagnetic conditions.
- **Source:** README.md, DataCite API, code examination

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Python wrapper for the International Reference Ionosphere (IRI) 2016 model.
- **Source:** DataCite API, Zenodo API description

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2017-01-12
- **Source:** DataCite API (date issued), Zenodo API, git tag date for v1.1.0

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite API, Zenodo API

### 12. Version (RECOMMENDED)

#### Version v1.1.0 (DOI version):
- **Version Number:** v1.1.0
- **Version Date:** 2017-01-12
- **Version Description:** Release with License and DOI number.
- **Version PID:** https://doi.org/10.5281/zenodo.240895
- **Source:** DataCite API, Zenodo API, git tag, SoMEF (release information)

#### Note on version discrepancy:
The setup.py file shows version '1.2.2', while the DOI and git tag reference v1.1.0. The pyproject.toml shows version "0.1.0". The repository appears to have been updated after the DOI was minted for v1.1.0, but no subsequent releases were tagged or assigned DOIs.

### 13. Programming Language (RECOMMENDED)
- **Python** (primary language for wrapper)
- **Python 3.x** (requires Python >=3.8.6,<3.11 per pyproject.toml; >=2.7 per setup.py)
- **Fortran** (for the underlying IRI2016 model code)

**Source:** SoMEF (GitHub API shows Fortran: 2363231 bytes, Python: 40413 bytes), setup.py (uses f2py), pyproject.toml, README.md

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication DOI:** Not found
- **Note:** No reference publication DOI found in repository files, README, CITATION files, or metadata sources.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://api.github.com/licenses/mit
- **SPDX ID:** MIT
- **Source:** SoMEF (GitHub API), LICENSE.md file, setup.py

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

**Source:** SoMEF (GitHub topics), manual extraction from description and README.md

### 17. Data Sources (OPTIONAL)
- **Other** (uses internal data files)

**Note:** The software includes data files in subdirectories (ccir, igrf, index, mcsat, ursi) which are part of the IRI model distribution. These are reference data files, not external data sources.

**Source:** setup.py (iriDataFiles), repository structure examination

### 18. Input File Formats (RECOMMENDED)
- **ascii** (uses .asc and .dat files for model coefficients)

**Source:** setup.py shows data files: ccir/*.asc, igrf/*.dat, index/*.dat, mcsat/*.dat, ursi/*.asc

### 19. Output File Formats (RECOMMENDED)
- Not found

**Note:** The software returns data as Python dictionaries/arrays. Output file generation is not explicitly implemented in the core package, though users could save outputs using standard Python methods.

### 20. Operating System (RECOMMENDED)
- **Operating System Independent** (or OS Independent)

**Rationale:** Python package with compiled Fortran extensions via f2py should work on any platform with appropriate compilers. The README shows Docker support, suggesting cross-platform capability.

**Source:** Inference from Python/f2py architecture, Docker support in README.md

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Rationale:** Python with f2py-compiled Fortran should compile on standard CPU architectures where compilers are available.

**Source:** Inference from software architecture

### 22. Related Phenomena (OPTIONAL)
- Not found in controlled vocabularies

**Note:** While the software models ionospheric phenomena, no specific controlled vocabulary terms were found in the available metadata.

### 23. Development Status (RECOMMENDED)
- **Inactive**

**Rationale:** The repository shows the last tagged release was in 2017 (v1.1.0). While the main branch was updated more recently (SoMEF shows date_updated: 2025-05-21T20:55:24Z), there have been no new releases or active development indicators. The package reached a stable, usable state but appears to no longer be actively developed.

**Source:** Git history, SoMEF date information, release history

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/rilma/pyIRI2016/blob/main/README.md

**Note:** Documentation consists primarily of the README.md with examples. No dedicated documentation site (e.g., ReadTheDocs) was found.

**Source:** Repository examination, SoMEF

### 25. Funder (OPTIONAL)
- Not found

**Source:** DataCite API (no fundingReferences), manual examination of repository files

### 26. Award Title (OPTIONAL)
- Not found

**Source:** DataCite API (no fundingReferences), manual examination of repository files

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Not found

**Source:** DataCite API, repository examination (no CITATION.cff or papers/ directory)

### 28. Related Datasets (OPTIONAL)
- Not found

**Source:** DataCite API, repository examination

### 29. Related Software (OPTIONAL)

#### Related Software 1:
- **Name/Repository:** TimeUtilities
- **URL:** https://github.com/rilma/TimeUtilities
- **Relationship:** Required dependency
- **Source:** README.md, setup.py dependency_links

#### Related Software 2:
- **Name/Repository:** IRI-2016 (alternative implementation)
- **URL:** https://github.com/space-physics/iri2016
- **Relationship:** Similar package - different Python wrapper for IRI2016
- **Source:** PyHC unevaluated registry, manual knowledge

**Note:** While this package is not formally related, there exists another Python package for IRI2016 by Michael Hirsch (who is listed as a co-author of pyIRI2016).

### 30. Interoperable Software (OPTIONAL)
- Not found

**Source:** Repository examination, no explicit interoperability statements

### 31. Related Instruments (OPTIONAL)
- Not found

**Note:** IRI is a model, not instrument-specific, though it can be used with data from various ionospheric instruments (ionosondes, ISRs, etc.).

### 32. Related Observatories (OPTIONAL)
- Not found

**Note:** The IRI model is a general ionospheric model not tied to specific observatories, though it incorporates data from various ground-based and satellite observations.

### 33. Logo (OPTIONAL)
- Not found

**Source:** SoMEF, repository examination

---

## Metadata Quality Notes

### PyHC Package Status
- **PyHC Registry:** Not found in PyHC core, community, or unevaluated packages
- **Note:** A different IRI2016 package (https://github.com/space-physics/iri2016) appears in the PyHC unevaluated registry

### Completeness Assessment
- **MANDATORY fields:** All filled or marked for user completion
- **RECOMMENDED fields:** Most filled; missing Reference Publication, complete version history
- **OPTIONAL fields:** Partially filled where information available

### Data Quality Issues
1. **Version Inconsistency:** Three different version numbers found (v1.1.0 in git tag, 1.2.2 in setup.py, 0.1.0 in pyproject.toml)
2. **Author Name Variation:** Ronald Ilma vs. Ronald R. Ilma Campana may be same person
3. **Concept DOI:** Not found in Zenodo API response (field was empty)
4. **Limited Documentation:** No comprehensive documentation site, only README with examples

### Verification Status
- DataCite API: ✓ Verified
- Zenodo API: ✓ Verified
- SoMEF: ✓ Completed
- PyHC Registry: ✓ Checked (not found)
- Repository Examination: ✓ Completed
- Code Analysis: ✓ Completed

---

## Extraction Methodology

This metadata was extracted using the following cascade:

1. **DataCite API** (https://api.datacite.org/dois/10.5281/zenodo.240895)
2. **Zenodo API** (https://zenodo.org/api/records/240895)
3. **SoMEF** (Software Metadata Extraction Framework v0.9.11)
4. **PyHC Registry Check** (all three registry files examined)
5. **Manual Repository Examination**:
   - README.md
   - LICENSE.md
   - pyproject.toml
   - setup.py
   - pyiri2016/__init__.py
   - Git history and tags
   - Repository structure

---

## Recommended Actions for Submitter

1. **Create CITATION.cff** file with complete author information including ORCIDs
2. **Resolve version numbering** inconsistencies across setup.py, pyproject.toml, and git tags
3. **Consider creating formal documentation** using ReadTheDocs or similar
4. **Add concept DOI** to repository if available from Zenodo
5. **Tag newer versions** if updates beyond v1.1.0 should be released
6. **Consider publishing reference paper** describing the wrapper implementation
7. **Clarify development status** - update README if package is actively maintained or add archive notice if not

---

**End of Metadata Extraction**
