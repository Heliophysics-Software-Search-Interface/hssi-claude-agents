# HSSI Metadata Extraction Results

**Repository:** https://github.com/HinodeXRT/xrtpy
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.13157913
- **Source:** Zenodo API (concept DOI for all versions)
- **Note:** This is the concept DOI. The version-specific DOI for v0.4.1 is https://doi.org/10.5281/zenodo.13157914

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/HinodeXRT/xrtpy
- **Source:** DataCite API, Zenodo API, repository

### 4. Software Functionality (MANDATORY)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Image Processing
- Data Visualization
- Data Visualization:2D Graphics
- Mission-related
- Mission-related:Analysis
- Mission-related:Calibration
- Mission-related:Instrument Response
- Mission-related:Instrumentation

**Source:** Manual analysis of JOSS paper, documentation, and repository
**Rationale:** XRTpy provides comprehensive analysis tools for Hinode/XRT data including:
- Object-oriented representation of instrument configuration
- Effective area calculations (calibration)
- Temperature response computation (instrument response)
- Light leak subtraction (image processing)
- Image sharpening via deconvolution (image processing)
- Estimation of electron temperature (analysis)
- Emission measure derivation (analysis)
- Visualization of temperature responses and filter ratios (2D graphics)

### 5. Related Region (MANDATORY)
- **Value:** Solar Environment
- **Source:** Manual analysis
- **Rationale:** XRTpy analyzes observations from the X-Ray Telescope (XRT) aboard Hinode, which observes the solar corona (photosphere to upper corona, temperatures from <1 MK to >10 MK)

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Joy Velasquez
- **Author Identifier:** https://orcid.org/0009-0005-4804-0946
- **Affiliation 1:**
  - **Organization:** Center for Astrophysics Harvard & Smithsonian
  - **Affiliation Identifier:** https://ror.org/03c3r2d17
- **Affiliation 2:**
  - **Organization:** Smithsonian Astrophysical Observatory
  - **Affiliation Identifier:** https://ror.org/04mh52z70
- **Affiliation 3:**
  - **Organization:** Smithsonian Institution
  - **Affiliation Identifier:** https://ror.org/01pp8nd67
- **Source:** DataCite API

**Author 2:**
- **Name:** Katharine Reeves
- **Author Identifier:** https://orcid.org/0000-0002-6903-6832
- **Affiliation 1:**
  - **Organization:** Smithsonian Institution
  - **Affiliation Identifier:** https://ror.org/01pp8nd67
- **Affiliation 2:**
  - **Organization:** Harvard-Smithsonian Center for Astrophysics
  - **Affiliation Identifier:** Not found (Note: Different naming than in DataCite)
- **Affiliation 3:**
  - **Organization:** Smithsonian Astrophysical Observatory
  - **Affiliation Identifier:** https://ror.org/04mh52z70
- **Source:** DataCite API

**Author 3:**
- **Name:** Nicholas Murphy
- **Author Identifier:** https://orcid.org/0000-0001-6628-8033
- **Affiliation 1:**
  - **Organization:** Center for Astrophysics Harvard & Smithsonian
  - **Affiliation Identifier:** https://ror.org/03c3r2d17
- **Affiliation 2:**
  - **Organization:** Smithsonian Astrophysical Observatory
  - **Affiliation Identifier:** https://ror.org/04mh52z70
- **Affiliation 3:**
  - **Organization:** Smithsonian Institution
  - **Affiliation Identifier:** https://ror.org/01pp8nd67
- **Source:** DataCite API

**Author 4:**
- **Name:** Jonathan Slavin
- **Author Identifier:** https://orcid.org/0000-0002-7597-6935
- **Affiliation:**
  - **Organization:** Center for Astrophysics Harvard & Smithsonian
  - **Affiliation Identifier:** https://ror.org/03c3r2d17
- **Source:** DataCite API

**Author 5:**
- **Name:** Mark Weber
- **Author Identifier:** https://orcid.org/0000-0001-7098-7064
- **Affiliation 1:**
  - **Organization:** Center for Astrophysics Harvard & Smithsonian
  - **Affiliation Identifier:** https://ror.org/03c3r2d17
- **Affiliation 2:**
  - **Organization:** Smithsonian Astrophysical Observatory
  - **Affiliation Identifier:** https://ror.org/04mh52z70
- **Affiliation 3:**
  - **Organization:** Smithsonian Institution
  - **Affiliation Identifier:** https://ror.org/01pp8nd67
- **Source:** DataCite API

**Author 6:**
- **Name:** Will Barnes
- **Author Identifier:** https://orcid.org/0000-0001-9642-6089
- **Affiliation 1:**
  - **Organization:** American University
  - **Affiliation Identifier:** https://ror.org/052w4zt36
- **Affiliation 2:**
  - **Organization:** Goddard Space Flight Center
  - **Affiliation Identifier:** https://ror.org/0171mag52
- **Source:** DataCite API

**Additional Authors from pyproject.toml:**
- Nabil Freij (email: nabil.freij@gmail.com)
- Stuart Mumford
- **Note:** These authors are listed in pyproject.toml but not in the Zenodo metadata

### 7. Software Name (MANDATORY)
- **Value:** XRTpy: A Hinode X-Ray Telescope Python Package
- **Source:** DataCite API, Zenodo API, JOSS paper
- **Short form:** xrtpy (package name)

### 8. Description (MANDATORY)
- **Value:** The XRTpy Python package is a specialized tool developed for the analysis of observations made by the X-Ray Telescope (XRT) aboard the Hinode spacecraft. Hinode is a joint mission involving space agencies from Japan, the United States, and Europe, launched with the primary aim of providing multi-wavelength data from the photosphere to the upper corona, enabling continuous observations of the Sun. XRTpy offers a comprehensive range of functionalities, including object-oriented representation of instrument configuration, effective area calculations, temperature response computation, light leak subtraction, image sharpening, estimation of electron temperature, and emission measure derivation. These capabilities empower researchers to explore and analyze XRT data comprehensively, contributing to a deeper understanding of solar phenomena.
- **Source:** DataCite API, Zenodo API

### 9. Concise Description (OPTIONAL)
- **Value:** A Python package for analyzing data from the X-Ray Telescope (XRT) on the Hinode spacecraft.
- **Source:** pyproject.toml
- **Character count:** 108 characters

### 10. Publication Date (RECOMMENDED)
- **Value:** 2024-08-08
- **Source:** DataCite API, Zenodo API
- **Note:** This is the publication date for version 0.4.1

### 11. Publisher (RECOMMENDED)
- **Publisher:**
  - **Organization:** Zenodo
  - **Publisher Identifier:** https://zenodo.org (URL form; ROR not available in metadata)
- **Source:** DataCite API

### 12. Version (RECOMMENDED)

**Latest Stable Version:**
- **Version Number:** v0.5.0
- **Version Date:** 2025-04-08
- **Version Description:** This update brings improvements to both the code and documentation, including a new tutorial for accessing and visualizing Hinode/XRT observations, improved internal testing, cleaned up older files, expanded documentation with Code of Conduct, and upgrades to data models and package dependencies.
- **Version PID:** Not found (no DOI for v0.5.0)
- **Source:** Git tags, GitHub releases (from SoMEF)

**Version in Zenodo DOI:**
- **Version Number:** version 0.4.1
- **Version Date:** 2024-08-08
- **Version Description:** This release includes modifications and updates for the Journal of Open Source Software (JOSS) submission, including updated references in bibliography, final review and corrections to manuscript, and version number increment.
- **Version PID:** https://doi.org/10.5281/zenodo.13157914
- **Source:** DataCite API, Zenodo API, GitHub releases

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Specific versions supported (from pyproject.toml):**
- Python 3.11
- Python 3.12
- Python 3.13

**Additional languages (minor, from SoMEF):**
- TeX (documentation)
- IDL (legacy scripts for comparison)

**Source:** Zenodo API, SoMEF, pyproject.toml

### 14. Reference Publication (RECOMMENDED)
- **Value:** https://doi.org/10.21105/joss.06396
- **Citation:** Velasquez, Joy; Reeves, Katharine; Murphy, Nicholas; Slavin, Jonathan; Weber, Mark; Barnes, Will. (2024). XRTpy: A Hinode X-Ray Telescope Python Package. Journal of Open Source Software, 9(100), 6396.
- **Source:** Web search, README.md
- **Note:** Published August 9, 2024

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://opensource.org/licenses/BSD-2-Clause
- **Source:** DataCite API (SPDX identifier: BSD-2-Clause), LICENSE file, SoMEF

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- Solar Physics
- Hinode Spacecraft
- Python
- Heliophysics
- open source software
- X-Ray Telescope (XRT)
- Hinode
- x-ray
- XRT
- solar
- data_analysis

**Sources:**
- DataCite API (first 6 keywords)
- pyproject.toml (Hinode, Solar Physics, x-ray, XRT)
- PyHC registry (solar, specific, data_analysis, hinode)
- SoMEF

### 17. Data Sources (OPTIONAL)
- **Value:** Observatory/Mission-specific
- **Source:** Manual analysis
- **Note:** XRTpy analyzes data from the Hinode/XRT instrument specifically. Data access methods are not explicitly documented in the metadata, but the package works with XRT FITS files.

### 18. Input File Formats (RECOMMENDED)
- **Value:** FITS
- **Source:** Manual analysis (JOSS paper mentions SunPy Map object for handling Hinode/XRT image data, which uses FITS format)
- **Note:** XRTpy builds on the SunPy framework and uses the Map object for handling XRT image data, which typically uses FITS format

### 19. Output File Formats (RECOMMENDED)
- **Value:** Not found
- **Note:** Output formats not explicitly documented in available metadata

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows
- OS Independent

**Source:** CI workflow configuration (.github/workflows/ci.yml shows testing on ubuntu-latest, macos-latest, windows-latest), pyproject.toml classifiers
**Note:** Package is OS Independent per classifiers, with active CI testing on all three major platforms

### 21. CPU Architecture (RECOMMENDED)
- **Value:** CPU Independent
- **Source:** Inferred from Python package nature
- **Note:** As a pure Python package with standard scientific dependencies, should work on any architecture that supports Python 3.11+

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Solar Corona
- Solar Flares
- Coronal Heating

**Source:** Manual analysis of JOSS paper and documentation
**Rationale:** XRTpy analyzes X-ray observations of the solar corona, including temperature diagnostics and emission measure calculations relevant to studying coronal heating and solar flares

### 23. Development Status (RECOMMENDED)
- **Value:** Active
- **Source:** Zenodo API
- **Supporting evidence:** Recent releases (v0.5.0 in April 2025, v0.5.1-pre in July 2025), active development on GitHub

### 24. Documentation (RECOMMENDED)
- **Value:** https://xrtpy.readthedocs.io
- **Source:** pyproject.toml, SoMEF, PyHC registry
- **Additional documentation:**
  - Installation guide: https://xrtpy.readthedocs.io/en/latest/install.html
  - Contributing guide: https://xrtpy.readthedocs.io/en/latest/contributing.html
  - Changelog: https://xrtpy.readthedocs.io/en/stable/changelog/index.html

### 25. Funder (OPTIONAL)
- **Funder:**
  - **Organization:** National Aeronautics and Space Administration (NASA)
  - **Funder Identifier:** https://ror.org/027ka1x80
- **Source:** README.md, JOSS paper
- **Award:** NASA contract NNM07AB07C to the Smithsonian Astrophysical Observatory

**Additional Funder (from JOSS acknowledgements):**
- **Organization:** National Science Foundation (NSF)
- **Funder Identifier:** https://ror.org/021nxhr62
- **Award:** NSF CSSI award 1931388 (for N.A.M.)

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found (contract number NNM07AB07C provided but not award title)
- **Award Number:** NNM07AB07C
- **Source:** README.md, JOSS paper

**Additional Award:**
- **Award Title:** Not found
- **Award Number:** 1931388
- **Source:** JOSS paper acknowledgements
- **Recipient:** Nicholas A. Murphy

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Note:** These are publications that describe XRT instrument and methods, not publications citing XRTpy

**Key publications from JOSS paper bibliography:**
1. Golub et al. (2007) - The X-Ray Telescope (XRT) for the Hinode Mission. Solar Physics, 243(1), 63-86. https://doi.org/10.1007/s11207-007-0182-1
2. Kosugi et al. (2007) - The Hinode (Solar-B) Mission: An Overview. Solar Physics, 243(1), 3-17. https://doi.org/10.1007/s11207-007-9014-6
3. Narukage et al. (2011) - Coronal-Temperature-Diagnostic Capability of the Hinode/X-Ray Telescope. Solar Physics, 269(1), 169-236. https://doi.org/10.1007/s11207-010-9685-2
4. Narukage et al. (2014) - Coronal-Temperature-Diagnostic Capability of the Hinode/X-Ray Telescope Based on Self-consistent Calibration. II. Solar Physics, 289(3), 1029-1042. https://doi.org/10.1007/s11207-013-0368-7

**Source:** JOSS paper bibliography (paper.bib)

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found
- **Note:** XRTpy analyzes Hinode/XRT data, but specific dataset DOIs are not provided in the metadata. Users would access XRT data through standard solar physics data archives.

### 29. Related Software (RECOMMENDED)

**Key dependencies:**
1. SunPy (https://github.com/sunpy/sunpy) - Core dependency for solar physics data analysis
   - DOI: https://doi.org/10.3847/1538-4357/ab4f7a (Version 1.0 paper)
2. astropy (>=6)
3. matplotlib (>=3.7)
4. numpy (>=1.24)
5. scikit-image (>=0.21)
6. scipy (>=1.11.1)

**Interoperable packages mentioned in JOSS paper:**
1. aiapy - https://github.com/LM-SAL/aiapy
   - DOI: https://doi.org/10.21105/joss.02801
   - Description: For SDO/AIA observations
2. EISPAC - https://eispac.readthedocs.io
   - DOI: https://doi.org/10.21105/joss.04914
   - Description: For Hinode-EIS data analysis
3. irispy-lmsal - https://github.com/LM-SAL/irispy-lmsal
   - Description: For IRIS observations

**Source:** pyproject.toml dependencies, JOSS paper

### 30. Interoperable Software (RECOMMENDED)
**Values:**
1. SunPy - https://github.com/sunpy/sunpy
   - XRTpy builds on SunPy framework and uses SunPy Map objects
2. aiapy - https://github.com/LM-SAL/aiapy
   - DOI: https://doi.org/10.21105/joss.02801
3. EISPAC - https://eispac.readthedocs.io
   - DOI: https://doi.org/10.21105/joss.04914
4. irispy-lmsal - https://github.com/LM-SAL/irispy-lmsal

**Source:** JOSS paper explicitly mentions interoperability collaboration with these packages
**Note:** JOSS paper states "interoperability with other packages is a work in progress"

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** X-Ray Telescope (XRT)
- **Instrument Identifier:** Not found
- **Source:** Software name, description
- **Observatory:** Hinode spacecraft

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Hinode
- **Source:** Software name, description, JOSS paper
- **Note:** Hinode is a joint mission involving JAXA (Japan), NASA (United States), and STFC/ESA (Europe), launched to provide multi-wavelength observations of the Sun

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/HinodeXRT/xrtpy/main/docs/_static/images/XRTpy_logo.png
- **Source:** SoMEF, README.md, PyHC registry
- **Alternate location:** Listed in PyHC registry as well

---

## Additional Notes

### Data Collection Summary
- **Automated extraction:** Successfully extracted metadata from DataCite API, Zenodo API, SoMEF, and PyHC registry
- **Manual verification:** Examined README.md, LICENSE, pyproject.toml, JOSS paper, CI workflows
- **Web search:** Used to find JOSS publication DOI

### PyHC Package Status
- **Status:** XRTpy is a PyHC community package (listed in projects.yml)
- **Quality ratings:**
  - Community: Partially met
  - Documentation: Partially met
  - Testing: Partially met
  - Software maturity: Partially met
  - Python 3: Good
  - License: Good

### Key Contacts
- **Primary contact:** Joy Velasquez
- **General contact email:** XRTpy@cfa.harvard.edu
- **Issue tracker:** https://github.com/HinodeXRT/xrtpy/issues

### Version History Notes
- First public release: v0.1.0 (September 26, 2022)
- Repository created: January 5, 2021
- Latest stable: v0.5.0 (April 8, 2025)
- Latest pre-release: v0.5.1-pre (July 15, 2025)
- JOSS submission version: v0.4.1 (August 8, 2024)

### Missing Metadata
The following fields could not be populated:
- Output file formats (not documented)
- Related datasets (no specific dataset DOIs provided)
- Instrument identifier (no persistent ID for XRT found)
- Some award titles (only contract/award numbers provided)

---

## Metadata Priority Assessment

**MANDATORY fields:** ✅ All complete (pending submitter information)
- Submitter: User to fill
- Code Repository: ✅
- Software Functionality: ✅
- Related Region: ✅
- Authors: ✅
- Software Name: ✅
- Description: ✅

**RECOMMENDED fields:** ✅ Mostly complete
- Persistent Identifier: ✅
- Publication Date: ✅
- Publisher: ✅
- Version: ✅
- Programming Language: ✅
- Reference Publication: ✅
- License: ✅
- Input File Formats: ✅
- Operating System: ✅
- CPU Architecture: ✅
- Development Status: ✅
- Documentation: ✅
- Related Software: ✅
- Interoperable Software: ✅
- Output File Formats: ❌ (not found)

**OPTIONAL fields:** Partially complete
- Keywords: ✅
- Data Sources: ✅
- Related Phenomena: ✅
- Funder: ✅
- Award Title: Partial
- Related Publications: ✅
- Related Datasets: ❌
- Related Instruments: ✅
- Related Observatories: ✅
- Logo: ✅
- Concise Description: ✅

---

**Metadata extraction completed: 2025-10-09**
