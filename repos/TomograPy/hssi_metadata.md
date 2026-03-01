# HSSI Metadata Extraction Results

**Repository:** https://github.com/nbarbey/TomograPy
**Extraction Date:** 2025-12-02

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found

**Note:** No DOI was found in CITATION.cff, README, codemeta.json, or .zenodo.json files.

### 3. Code Repository (MANDATORY)
https://github.com/nbarbey/TomograPy

**Source:** GitHub repository URL

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Data Reduction
- Data Visualization
- Models and Simulations:Forward-Fitting
- Models and Simulations:Theory
- Mission-related:Analysis

**Note:** TomograPy implements solar tomography algorithms, specifically:
- Solar Rotational Tomography (SRT)
- Smooth Temporal Solar Rotational Tomography (STSRT)
- Thomson scattering model for white-light coronagraph data
- Fast Siddon algorithm for ray tracing
- Processes data from SOHO and STEREO missions
- Reconstructs 3-dimensional maps of the solar corona from 2D extreme-ultraviolet and coronagraph images

### 5. Related Region (MANDATORY)
- Solar Environment

**Note:** TomograPy is specifically designed for solar corona tomography and reconstruction.

### 6. Authors (MANDATORY)

**Primary Author:**
- **Authors:** Nicolas Barbey
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Commissariat à l'Énergie Atomique (CEA)
  - **Affiliation Identifier:** Not found

**Note:** Two email addresses found for Nicolas Barbey: nicolas.barbey@cea.fr (in setup.py) and nicolas.a.barbey@gmail.com (in AUTHOR file).

**Additional Contributors (Testing):**
- **Authors:** Chloé Guennou
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Institut d'Astrophysique Spatiale, Université Paris-Sud
  - **Affiliation Identifier:** Not found

- **Authors:** Frédéric Auchère
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Institut d'Astrophysique Spatiale, Université Paris-Sud
  - **Affiliation Identifier:** Not found

**Source:** AUTHOR file in repository

### 7. Software Name (MANDATORY)
TomograPy

**Source:** Repository name, setup.py, and SoMEF output

### 8. Description (MANDATORY)
TomograPy is a fast parallelized tomography projector and backprojector for solar physics applications. It implements the Siddon algorithm with OpenMP parallelization for efficient ray tracing. For solar astrophysics, TomograPy enables tomographic reconstructions of the solar corona by processing data from spacecraft such as SOHO and STEREO. The software can take Extreme-Ultraviolet (EUV) and white-light coronagraph data and output 3-dimensional maps of the corona. The package includes modules for solar rotational tomography (SRT), smooth temporal solar rotational tomography (STSRT), Thomson scattering models, data simulation, phantom generation, and visualization tools.

**Source:** Compiled from README.rst, setup.py, and tomograpy/__init__.py

### 9. Concise Description (OPTIONAL)
Fast parallelized tomography for solar coronal reconstructions using the Siddon algorithm.

**Source:** Derived from README and package documentation

### 10. Publication Date (RECOMMENDED)
2010-07-27

**Source:** First commit date from Git repository history

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Note:** Software is hosted on GitHub without a DOI publisher like Zenodo.

### 12. Version (RECOMMENDED)
- **Version Number:** 0.3.1
- **Version Date:** Not found (no git tags or release dates available)
- **Version Description:** Not found
- **Version PID:** Not found

**Note:** Version 0.3.1 found in setup.py; version 0.3.0 in __init__.py. No official releases or git tags found. The repository has a notice that a new version is being developed as "solartom" at https://github.com/jmbhughes/solartom.

### 13. Programming Language (RECOMMENDED)
- Python 2.x
- C

**Note:** PyHC registry indicates "Requires improvement" for Python 3 compatibility. The package uses Python with C extensions for performance (OpenMP parallelization).

**Source:** SoMEF output, setup.py, and PyHC registry

### 14. Reference Publication (RECOMMENDED)
Not found

**Note:** No reference publication DOI found in repository files.

### 15. License (RECOMMENDED)
- **License:** CeCILL-B Free Software License Agreement
- **License URI:** Not found (license text included in repository as LICENSE file)

**Note:** CeCILL-B is a French free software license similar to BSD, compatible with international and European law. The license allows broad freedom to modify and redistribute the software with a strong obligation to give proper attribution.

**Source:** LICENSE file in repository

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- solar
- tomography
- corona
- EUV
- extreme ultraviolet
- coronagraph
- SOHO
- STEREO
- Siddon algorithm
- rotational tomography
- Thomson scattering
- image reconstruction
- inverse problems

**Source:** Derived from README, PyHC registry, and code documentation

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific

**Note:** Specifically designed for SOHO and STEREO spacecraft data. The README mentions that data needs to be pre-processed using SolarSoft (http://www.lmsal.com/solarsoft/).

**Source:** README.rst

### 18. Input File Formats (RECOMMENDED)
- FITS

**Note:** The package uses pyfits and fitsarray libraries, indicating FITS file format support for input data. Examples reference SECCHI FITS data files.

**Source:** setup.py requirements and example files

### 19. Output File Formats (RECOMMENDED)
- FITS

**Note:** Based on the use of fitsarray package for handling output data cubes.

**Source:** Inferred from dependencies in setup.py

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- OS Independent

**Note:** Python package with C extensions requiring OpenMP. Likely works on Unix-like systems. No explicit OS restrictions documented.

**Source:** Inferred from code structure and dependencies

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- CPU Independent

**Note:** Uses OpenMP for parallelization, which is CPU-architecture independent. C extensions are compiled during installation.

**Source:** setup.py compilation flags

### 22. Related Phenomena (OPTIONAL)
- Solar Corona
- Coronal Heating

**Note:** The software reconstructs the solar corona structure.

**Source:** Derived from package purpose and documentation

### 23. Development Status (RECOMMENDED)
Unsupported

**Note:** PyHC registry indicates "Partially met" for software maturity with "Requires improvement" for community, documentation, testing, and Python 3 compatibility. The README contains a prominent notice that "A new version of this repo is being developed as solartom (https://github.com/jmbhughes/solartom)". The most recent commits are from 2025, but the project appears to be superseded by the newer solartom implementation. This suggests the software reached a usable state but the original authors have moved development to a successor project.

**Source:** PyHC registry and README notice

### 24. Documentation (RECOMMENDED)
http://nbarbey.github.io/TomograPy

**Note:** According to PyHC registry entry, though SoMEF notes that documentation is embedded in the code as docstrings. The README states: "The documentation for TomograPy is embedded into the code as docstrings. To get started, take a look at tomograpy/__init__.py or in IPython, just do: `import tomograpy; tomograpy?`"

**Source:** PyHC registry and README.rst

### 25. Funder (OPTIONAL)
Not found

**Note:** No funding information found in repository.

### 26. Award Title (OPTIONAL)
Not found

**Note:** No award information found in repository.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- Siddon, R. L. (1985). Fast calculation of the exact radiological path for a three-dimensional CT array. Medical Physics, 12(2), 252-255. http://adsabs.harvard.edu/abs/1985MedPh..12..252S

**Note:** This is the original publication describing the Siddon algorithm that forms the core of TomograPy. Cited in tomograpy/__init__.py documentation.

**Source:** Package documentation

### 28. Related Datasets (OPTIONAL)
Not found

**Note:** No specific dataset DOIs mentioned. Software processes SOHO and STEREO mission data that must be obtained separately and pre-processed with SolarSoft.

### 29. Related Software (OPTIONAL)
- https://github.com/jmbhughes/solartom

**Note:** The successor project that is actively being developed. The README explicitly states "A new version of this repo is being developed as solartom".

**Source:** README.rst prominent notice

### 30. Interoperable Software (OPTIONAL)
Not found

**Note:** Software requires several dependencies (numpy, scipy, pyfits, fitsarray, lo) but no specific interoperability claims found.

### 31. Related Instruments (OPTIONAL)

**Instrument 1:**
- **Instrument Name:** SECCHI (Sun Earth Connection Coronal and Heliospheric Investigation)
- **Instrument Identifier:** Not found

**Instrument 2:**
- **Instrument Name:** SOHO (Solar and Heliospheric Observatory)
- **Instrument Identifier:** Not found

**Note:** README explicitly mentions SOHO and STEREO spacecraft data. SECCHI is the instrument suite on STEREO. Examples include test_siddon_secchi.py and test_siddon_cor1.py (COR1 is a SECCHI coronagraph).

**Source:** README.rst and example file names

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** SOHO (Solar and Heliospheric Observatory)

**Observatory 2:**
- **Observatory Name:** STEREO (Solar Terrestrial Relations Observatory)

**Note:** These are the primary missions for which TomograPy processes data.

**Source:** README.rst

### 33. Logo (OPTIONAL)
Not found

**Note:** No logo found in repository.

---

## Metadata Sources Summary

This metadata was extracted using the following methods:

1. **SoMEF (Software Metadata Extraction Framework):** Automated extraction of repository metadata including description, programming languages, authors, and dates.

2. **PyHC (Python in Heliophysics Community) Registry:** TomograPy is listed in the PyHC community registry (projects.yml) with manually curated metadata including quality ratings and keywords.

3. **Manual Repository Examination:** Direct reading of key files including:
   - README.rst (software description, usage, requirements)
   - setup.py (version, author contact, dependencies, description)
   - LICENSE (CeCILL-B license text)
   - AUTHOR (author names and test contributors)
   - tomograpy/__init__.py (package documentation and version)
   - tomograpy/models.py (implementation details)
   - Git history (first commit date, development activity)

4. **Code Analysis:** Examination of example files and source code to understand software functionality and supported data formats.

## Notes and Observations

1. **Successor Project:** The README prominently notes that development has moved to "solartom" (https://github.com/jmbhughes/solartom), which should be considered the active continuation of this project.

2. **Python 3 Compatibility:** PyHC registry indicates "Requires improvement" for Python 3 compatibility, suggesting the software may primarily support Python 2.x.

3. **Missing DOI:** The software lacks a persistent identifier (DOI), which would improve citability and long-term accessibility.

4. **Data Pre-processing Required:** Users must pre-process SOHO/STEREO data using SolarSoft IDL libraries before using TomograPy.

5. **Limited Public Documentation:** Documentation is primarily embedded as docstrings rather than comprehensive external documentation.

6. **License Compatibility:** The CeCILL-B license is compatible with international open-source standards and similar to BSD-style licenses.

7. **Active Maintenance Status:** While recent commits exist (as of 2025), the project appears to be in maintenance mode with development focus shifted to the solartom successor.
