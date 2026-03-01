# HSSI Metadata Extraction Results

**Repository:** https://github.com/dpq/python-magnetosphere
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found - No DOI located in repository files, README, or automated extraction.

### 3. Code Repository (MANDATORY)
https://github.com/dpq/python-magnetosphere

**Note:** Original repository was hosted at http://python-magnetosphere.googlecode.com (now defunct, migrated to GitHub).

### 4. Software Functionality (MANDATORY)
Based on analysis of the IGRF, CXFORM, and rigidity modules:

- Coordinate Transforms
- Coordinate Transforms:Heliospheric
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Field-line Tracing

**Details:**
- **IGRF module**: Implements the International Geomagnetic Reference Field (IGRF) v.11 empirical model for calculating Earth's magnetic field properties, L-shell values, and performing field-line tracing.
- **CXFORM module**: Provides coordinate transformations between multiple coordinate systems including magnetospheric (GSE, GSM, SM, MAG), heliospheric (HEE, HAE, HEEQ, GSEQ, RTN), and geocentric (GEI, J2000, GEO) systems.
- **Rigidity module**: Calculates cosmic ray cutoff rigidity (geomagnetic cutoff) at various altitudes, determining the minimum particle momentum required for cosmic rays to penetrate Earth's magnetosphere at a given location (Epoch 2010.0).

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space

**Rationale:** The software supports magnetospheric coordinate systems (GSE, GSM, SM), calculates L-shell parameters for Earth's magnetosphere, models Earth's magnetic field from the surface through the atmosphere, and includes heliospheric coordinate transformations for interplanetary space applications.

### 6. Authors (MANDATORY)

#### Author 1:
- **Authors:** David Parunakian
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Skobeltsyn Institute of Nuclear Physics of the Moscow State University
  - **Affiliation Identifier:** Not found

**Source:** README file states "The wrapper has been written by David Parunakian, Skobeltsyn Institute of Nuclear Physics of the Moscow State University."

**Note:** The underlying CXFORM library was originally written by Ed Santiago (LANL) and modified/maintained by Ryan Boller (NASA/GSFC). The IGRF model itself is developed by IAGA (International Association of Geomagnetism and Aeronomy) Working Group.

### 7. Software Name (MANDATORY)
Magnetosphere (also known as python-magnetosphere)

**Source:** Package name from setup.py is "Magnetosphere"; repository name is "python-magnetosphere".

### 8. Description (MANDATORY)
The magnetosphere package is a collection of useful libraries for Earth and Space scientists, providing three main modules. The igrf module offers methods based on the International Geomagnetic Reference Field (IGRF) version 11, including functions to calculate the geomagnetic dipole moment, L-shell and geomagnetic field intensity, Earth's magnetic field vector components, and the smallest magnetic field strength on a field line through field-line tracing. The cxform module provides coordinate transformation capabilities, allowing users to transform Cartesian coordinates between various coordinate systems commonly used in space physics, including geocentric (GEI, J2000, GEO, MAG), magnetospheric (GSE, GSM, SM), and heliospheric (HEE, HAE, HEEQ, GSEQ, RTN) coordinate systems. The rigidity module calculates cosmic ray cutoff rigidity at various altitudes, determining the minimum particle momentum required for cosmic rays to penetrate Earth's magnetosphere at a given location. The IGRF wrapper and rigidity module were developed by David Parunakian at the Skobeltsyn Institute of Nuclear Physics, while the coordinate transformation functionality is based on CXFORM, an IDL/C library originally written by Ed Santiago at LANL and maintained by Ryan Boller at NASA/GSFC.

### 9. Concise Description (OPTIONAL)
Python package providing IGRF magnetic field calculations, cosmic ray cutoff rigidity analysis, and coordinate transformations for space physics applications.

### 10. Publication Date (RECOMMENDED)
2009-12-29

**Source:** First git commit date. Note that the GitHub repository was created later (2015-03-13) when migrated from Google Code.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Note:** Originally published on Google Code before migration to GitHub.

### 12. Version (RECOMMENDED)
- **Version Number:** 0.11
- **Version Date:** Not found (no git tags or release dates available; last commit was 2011-02-08)
- **Version Description:** Not found
- **Version PID:** Not found

**Source:** Version number from setup.py

### 13. Programming Language (RECOMMENDED)
- C
- Python 2.x

**Source:** GitHub API reports C (184,515 bytes) and Python (793 bytes). The package uses Python 2 syntax based on setup.py structure and code inspection. Primary implementation is in C with Python bindings.

**Note:** The package was developed for Python 2 and may require updates for Python 3 compatibility.

### 14. Reference Publication (RECOMMENDED)
Not found

### 15. License (RECOMMENDED)
- **License:** GNU General Public License v3.0
- **License URI:** https://www.gnu.org/licenses/gpl-3.0.html

**Source:** LICENSE file in repository and GitHub API (SPDX ID: GPL-3.0)

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- magnetosphere
- IGRF
- coordinate transformations
- geomagnetic field
- L-shell
- field-line tracing
- space physics
- Earth magnetic field
- heliophysics
- cosmic ray
- cutoff rigidity
- geomagnetic cutoff

**Source:** Derived from package description and functionality analysis.

### 17. Data Sources (OPTIONAL)
Not applicable - This software does not retrieve data from external sources; it performs calculations and transformations.

### 18. Input File Formats (RECOMMENDED)
Not applicable - The software operates on numerical input parameters (coordinates, dates, altitudes) rather than file-based input. IGRF coefficients are read from data files installed with the package.

**Note:** IGRF coefficient files are included with the package and installed to /usr/local/lib/igrf/.

### 19. Output File Formats (RECOMMENDED)
Not applicable - The software returns numerical results (tuples, arrays) directly to the calling Python code rather than writing to files.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows
- Solaris

**Source:** README states CXFORM "has been tested under SunOS v5.7, Microsoft Windows 2000/XP, Mac OS X 10.3 & 10.4, and Linux 2.4.20-28.9. It has previously been tested under Solaris 2.6 and DEC OSF/1 V4.0."

**Note:** Requires C compiler and f2c library for building from source.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- CPU Independent

**Source:** Based on operating system support and lack of architecture-specific code. The README mentions "Updated Mac compiler flags to compile 32- and 64-bit versions on Intel- and PPC-based CPUs."

### 22. Related Phenomena (OPTIONAL)
Not applicable - The software is a tool for coordinate transformations and field calculations rather than being specific to particular phenomena.

### 23. Development Status (RECOMMENDED)
Inactive

**Rationale:** The repository reached a stable, usable state (version 0.11) but is no longer actively developed. Last commit was in 2011 (2011-02-08), though the repository has only 8 total commits. The software appears functional but has not been updated in over 14 years. Support would be provided as time allows by the original author if contacted.

**Note:** Despite the inactive development status, the GitHub repository shows a recent update date (2025-02-24), likely due to repository activity (stars, forks) rather than code changes.

### 24. Documentation (RECOMMENDED)
https://github.com/dpq/python-magnetosphere/blob/master/README

**Note:** Documentation is limited to the README file. More comprehensive documentation for the underlying CXFORM library is available at http://nssdcftp.gsfc.nasa.gov/selected_software/coordinate_transform/

### 25. Funder (OPTIONAL)
Not found

### 26. Award Title (OPTIONAL)
Not found

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

**Note:** The README references the following publications as the basis for the CXFORM coordinate transformations:
- Mike Hapgood's introduction to coordinate transformations: http://sspg1.bnsc.rl.ac.uk/Share/Coordinates/ct_home.htm
- Markus Fraenz' "Heliospheric Coordinate Systems": http://www.space-plasma.qmul.ac.uk/heliocoords/
- Christopher Russell's "Geophysical Coordinate Transformations": http://www-ssc.igpp.ucla.edu/personnel/russell/papers/gct1.html/

### 28. Related Datasets (OPTIONAL)
Not found

**Note:** The package uses IGRF coefficient files, which can be obtained from ftp://nssdcftp.gsfc.nasa.gov/models/geomagnetic/igrf/fortran_code/

### 29. Related Software (OPTIONAL)
- **GEOPACK** - SSCWeb's coordinate transformation software (mentioned for comparison/validation)
- **SpacePy** - Python package for space science that includes similar IGRF and coordinate transformation functionality
- **IGRF** - The official IGRF model software (Fortran): http://www.ngdc.noaa.gov/IAGA/vmod/igrf.html

**Note:** The CXFORM test results indicate "within 1% of the results of SSCWeb's calculations (based on GEOPACK), and in many cases are within 0.01%."

### 30. Interoperable Software (OPTIONAL)
Not found - No explicit interoperability testing documented.

### 31. Related Instruments (OPTIONAL)
Not applicable - This is a general-purpose library for coordinate transformations and magnetic field modeling, not specific to any particular instrument.

### 32. Related Observatories (OPTIONAL)
Not applicable - This is a general-purpose library not tied to specific missions or observatories, though it can be used with data from any mission requiring coordinate transformations or magnetic field calculations.

### 33. Logo (OPTIONAL)
Not found

---

## Metadata Sources Summary

### Automated Extraction Results:

1. **DOI/DataCite API:** Not applicable (no DOI found)
2. **Zenodo API:** Not applicable (no Zenodo DOI found)
3. **SoMEF:** Successfully extracted metadata including:
   - Code repository URL
   - License (GPL-3.0)
   - Description
   - Programming languages (C, Python)
   - Package name (Magnetosphere)
   - Author email (dp@xientific.info)
   - Date created: 2015-03-13 (GitHub repo creation)
   - Date updated: 2025-02-24 (recent activity)

4. **PyHC Registry:** Not found - This package is not listed in PyHC core, community, or unevaluated registries.

### Manual Extraction Results:

- **README:** Comprehensive description of two modules (igrf, cxform), usage examples, coordinate systems supported, IGRF functionality, installation instructions, authors, affiliations, version history (Note: rigidity module not documented in README)
- **setup.py:** Package name, version (0.11), author name, author email, description, module structure including three modules (igrf, cxform, rigidity)
- **LICENSE:** Confirmed GNU GPL v3.0
- **Git history:** First commit (2009-12-29), last commit (2011-02-08), 8 total commits, no tags
- **Code analysis:** Three main modules (igrf, cxform, rigidity) implemented primarily in C with Python bindings. Rigidity module calculates cosmic ray cutoff rigidity.

---

## Notes for Submitter

1. **DOI Recommendation:** Consider creating a DOI through Zenodo to make this software more citable and discoverable.

2. **Python 3 Compatibility:** The package appears to be written for Python 2. Consider updating for Python 3 compatibility to maintain usability.

3. **Development Status:** The package has not been updated since 2011. Consider whether active maintenance will resume or if the status should remain as "Inactive."

4. **Documentation:** The current documentation is limited to the README. Consider creating more comprehensive documentation (e.g., ReadTheDocs) with API references and examples.

5. **IGRF Version:** The package uses IGRF version 11 from 2010. The current version is IGRF-13 (released 2019). Consider updating to the latest IGRF coefficients.

6. **Contact Information:** Confirm that dp@xientific.info and rumith@srd.sinp.msu.ru are still valid contact addresses.

7. **Testing:** No test suite was found in the repository. Consider adding automated tests.

8. **PyHC Consideration:** If active development resumes and the package is updated for Python 3, consider submitting to the PyHC registry.

---

## Extraction Completeness

- ✅ All automated extraction methods attempted (DataCite, Zenodo, SoMEF, PyHC)
- ✅ Repository thoroughly examined manually
- ✅ All 33 form fields addressed (value provided or "Not found")
- ✅ MANDATORY fields have values
- ✅ Software Functionality comprehensively analyzed (8 categories identified)
- ✅ Related Region comprehensively analyzed (3 regions identified)
- ✅ Metadata sources are verifiable and documented
- ✅ Format matches required structure
