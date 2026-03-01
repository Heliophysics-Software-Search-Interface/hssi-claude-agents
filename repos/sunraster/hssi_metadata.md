# HSSI Metadata Extraction Results

**Repository:** https://github.com/sunpy/sunraster
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Not found** - sunraster does not have its own DOI. The Zenodo badge in the README links to the main SunPy package DOI (10.5281/zenodo.591887), not sunraster specifically.

### 3. Code Repository (MANDATORY)
https://github.com/sunpy/sunraster

### 4. Software Functionality (MANDATORY)
Based on code analysis, documentation, and repository examination, sunraster supports the following functionalities:

- **Data Processing and Analysis**
- **Data Processing and Analysis:Data Access and Retrieval**
- **Data Processing and Analysis:Data Reduction**
- **Data Processing and Analysis:Spectrogram**
- **Data Processing and Analysis:Analysis**
- **Data Visualization**
- **Data Visualization:Spectrogram**
- **Mission-related:Analysis**
- **Mission-related:Instrumentation**

**Source:** Code analysis shows sunraster reads and analyzes spectrogram data from solar instruments, particularly SPICE. The package provides SpectrogramCube and SpectrogramSequence classes for data manipulation and analysis.

### 5. Related Region (MANDATORY)
- **Solar Environment**

**Source:** PyHC registry classification and package description ("solar physics", "solar mission"). The package is specifically designed for solar spectrographic data analysis.

### 6. Authors (MANDATORY)

**Primary Author:**
- **Authors:** The SunPy Community
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Contact:**
- Nabil Freij (from PyHC registry)
- Email: sunpy@googlegroups.com (from pyproject.toml)

**Note:** As a community-developed package under the SunPy umbrella, sunraster has numerous contributors. The main SunPy package has 200+ contributors listed in its Zenodo record, but sunraster-specific contributor information is not easily extractable without examining detailed git history.

### 7. Software Name (MANDATORY)
sunraster

### 8. Description (MANDATORY)
sunraster is an open-source Python library that provides the tools to read in and analyze spectrogram data. It is a SunPy-affiliated package which provides tools to analyze data from spectral data from any solar mission. The package supports reading and analyzing spectroscopic data, particularly from the SPICE instrument on Solar Orbiter, and provides data structures (SpectrogramCube, SpectrogramSequence, RasterSequence) for manipulating multi-dimensional spectral datasets with coordinate information.

**Source:** PyHC registry, SoMEF output, README.rst, and pyproject.toml

### 9. Concise Description (OPTIONAL)
A Python library for reading and analyzing solar spectrogram data from various missions, with built-in support for SPICE.

### 10. Publication Date (RECOMMENDED)
**2017-02-27** (repository creation date)

**Source:** SoMEF output from GitHub API

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Note:** sunraster does not have a Zenodo DOI, so it is not published through Zenodo.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.7.0
- **Version Date:** 2025-10-16
- **Version Description:** Increased minimum Python to 3.12, NumPy to 1.26.0, Astropy to 6.1.0, and sunpy to 7.0.0. Updated to use ndcube 2.3.0 minimum with removal of older metadata handling methods.
- **Version PID:** Not found

**Source:** Git tags, CHANGELOG.rst, SoMEF releases

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** (specifically requires Python >= 3.12 as of v0.7.0)

**Source:** SoMEF output, pyproject.toml

### 14. Reference Publication (RECOMMENDED)
**Not found** - No JOSS paper or other reference publication DOI found in repository files or metadata.

**Note:** The CHANGELOG mentions a "sunraster JOSS paper" PR (#231) in version 0.5.0, but no published JOSS paper DOI was found.

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://opensource.org/licenses/BSD-2-Clause (or https://api.github.com/licenses/bsd-2-clause)

**Source:** LICENSE.rst, SoMEF output, GitHub API

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
Based on multiple sources:

**From PyHC registry:**
- solar
- data_container
- spectra
- plotting
- general
- fits

**From SoMEF/GitHub topics:**
- astronomy
- astropy
- iris
- python
- solar
- solar-physics
- spice
- sunpy
- sunrise

**Combined unique keywords:** astronomy, astropy, data_container, fits, general, iris, plotting, python, solar, solar-physics, spectra, spice, sunpy, sunrise

### 17. Data Sources (OPTIONAL)
- **Observatory/Mission-specific** (SPICE instrument, Solar Orbiter)

**Note:** Previously supported IRIS before v0.4.0 (removed; users should use irispy-lmsal instead)

### 18. Input File Formats (RECOMMENDED)
- **FITS**

**Source:** Code analysis shows read_spice_l2_fits function in instr/spice.py

### 19. Output File Formats (RECOMMENDED)
**Not explicitly found** in documentation or code. Likely supports standard Python/scientific computing formats through its dependencies (astropy, ndcube), but not definitively documented.

### 20. Operating System (RECOMMENDED)
- **OS Independent** (Python package)

**Inferred:** As a pure Python package with cross-platform dependencies, it should work on Linux, Mac, and Windows.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Inferred:** Pure Python package with no architecture-specific requirements evident.

### 22. Related Phenomena (OPTIONAL)
**Not found** - No specific solar phenomena keywords identified in metadata.

**Note:** As a data analysis tool rather than a phenomena-specific tool, this field may not apply.

### 23. Development Status (RECOMMENDED)
- **Active**

**Source:** PyHC registry shows "Good" software maturity rating. Recent commits (November 2025) and releases (October 2025) indicate active development.

### 24. Documentation (RECOMMENDED)
https://docs.sunpy.org/projects/sunraster

**Source:** PyHC registry, pyproject.toml, README.rst

### 25. Funder (OPTIONAL)
**Not found** - No funder information in repository metadata.

**Note:** As part of the SunPy ecosystem, may share SunPy's funding sources (NumFOCUS), but not explicitly stated for sunraster.

### 26. Award Title (OPTIONAL)
**Not found**

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Not found** - No related publications identified in repository metadata.

### 28. Related Datasets (OPTIONAL)
**Not found** - No specific datasets identified, though the package is designed to work with SPICE Level 2 FITS files.

### 29. Related Software (OPTIONAL)
Based on dependencies and documentation:

**Key Dependencies:**
- **sunpy** (>= 7.0) - https://github.com/sunpy/sunpy (concept DOI: 10.5281/zenodo.591887)
- **ndcube** (>= 2.3.2) - https://github.com/sunpy/ndcube - Core data structure dependency
- **astropy** (>= 6.1.0) - https://www.astropy.org
- **numpy** (>= 1.26.0) - https://numpy.org

**Related packages mentioned:**
- **irispy-lmsal** - Recommended replacement for IRIS support (removed in v0.4.0)

### 30. Interoperable Software (OPTIONAL)
Based on the SunPy ecosystem and dependencies:

- **sunpy** - Parent package, demonstrated interoperability
- **ndcube** - Core dependency, full interoperability
- **astropy** - Core dependency, full interoperability

### 31. Related Instruments (OPTIONAL)

**Primary:**
- **Instrument Name:** SPICE (Spectral Imaging of the Coronal Environment)
- **Instrument Identifier:** Not found
- **Mission:** Solar Orbiter (ESA)
- **Note:** Full reader implementation in instr/spice.py

**Previously supported (removed in v0.4.0):**
- **Instrument Name:** IRIS (Interface Region Imaging Spectrograph)
- **Note:** Support removed; users directed to irispy-lmsal

**Keywords suggest possible support for:**
- SUNRISE mission instruments

### 32. Related Observatories (OPTIONAL)

**Primary:**
- **Observatory Name:** Solar Orbiter
- **Note:** Primary mission for SPICE instrument

**Previously:**
- **Observatory Name:** IRIS (satellite)

**Mentioned in keywords:**
- **Observatory Name:** SUNRISE

### 33. Logo (OPTIONAL)
**Not found** - sunraster does not have its own logo. It uses SunPy branding as an affiliated package.

---

## Metadata Quality Notes

### Completeness
- **MANDATORY fields:** 6/7 completed (missing submitter info, which is expected)
- **RECOMMENDED fields:** 10/14 completed
- **OPTIONAL fields:** 4/19 completed

### Key Gaps
1. **No DOI** - Package does not have its own persistent identifier
2. **No Reference Publication** - JOSS paper mentioned but not found
3. **Limited author information** - Community package with no individual authors listed
4. **Output file formats** - Not documented
5. **Funder information** - Not specified
6. **Related publications/datasets** - None identified

### Reliability Assessment

**High confidence (verified from multiple sources):**
- Software name, description, repository URL
- License (BSD 2-Clause)
- Programming language (Python)
- Documentation URL
- Current version and release date
- Software functionality
- Input file formats (FITS)
- Related instruments (SPICE, Solar Orbiter)
- Development status (Active)

**Medium confidence (from single authoritative source):**
- PyHC classification keywords
- Operating system (inferred)
- Interoperable software

**Low confidence/Not found:**
- DOI
- Individual authors/contributors
- Funder information
- Output file formats
- Reference publication
- Related publications

### Data Sources Used
1. **PyHC Registry** (heliophysicsPy.github.io) - community registry entry
2. **SoMEF** (Software Metadata Extraction Framework) - automated extraction
3. **Repository files:** README.rst, LICENSE.rst, pyproject.toml, CHANGELOG.rst
4. **Git metadata:** tags, release dates
5. **Code analysis:** sunraster/__init__.py, spectrogram.py, instr/spice.py
6. **GitHub API:** (via SoMEF) for release information and topics

---

## Verification Notes

This metadata has been extracted through a systematic process:
1. ✅ Automated API queries attempted (no sunraster-specific DOI found)
2. ✅ SoMEF extraction completed
3. ✅ PyHC registry checked (found in community packages)
4. ✅ Repository files examined
5. ✅ Code analyzed for functionality and file format support
6. ✅ Git history examined for version information

**Extraction methodology:** Combined automated extraction (SoMEF, APIs, PyHC registry) with manual verification through repository file examination and code analysis.

**Last updated:** 2025-12-02
