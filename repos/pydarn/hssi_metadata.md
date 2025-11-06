# HSSI Metadata Extraction Results

**Repository:** https://github.com/SuperDARN/pydarn
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Source:** To be provided by submitter

---

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.3727269

**Source:** README.md badge, DataCite API, Zenodo API
**Note:** This is the concept DOI covering all versions of pyDARN

---

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/SuperDARN/pydarn

**Source:** DataCite API, Zenodo API, SoMEF, PyHC registry

---

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Spectrogram

**Source:** Code analysis of pydarn package structure, documentation
**Analysis:**
- **Coordinate Transforms**: pyDARN includes extensive coordinate transformation capabilities (coordinates.py, geo.py)
  - AACGM (Altitude Adjusted Corrected Geomagnetic) coordinates for ionospheric studies
  - Geographic to geomagnetic coordinate conversions
  - Magnetic Local Time (MLT) conversions
  - Beam/gate to geographic/geomagnetic location mapping
- **Data Access and Retrieval**: SuperDARNRead class for reading SuperDARN data files (superdarn_io.py)
- **Data Processing**: Range estimations (range_estimations.py), virtual heights (virtual_heights.py), filters (Boxcar filter in filters.py), elevation recalculation
- **Data Analysis**: Statistical power plots, ACF (Auto-Correlation Function) analysis, IQ data analysis, time series analysis
- **2D Graphics**: Fan plots (fan.py), Grid plots (grid.py), Convection maps (maps.py), Range-time plots (rtp.py)
- **Line Plots**: Time series plotting (TimeSeriesParams)
- **Spectrogram**: ACF plots showing spectral/correlation data (acf.py)
- **Data Reduction**: Boxcar filtering for smoothing data before visualization

---

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere
- Earth Magnetosphere

**Source:** Scientific context analysis, PyHC keywords, documentation
**Analysis:** SuperDARN (Super Dual Auroral Radar Network) is an international network of HF radars designed to study the ionosphere and magnetosphere. The ionosphere is part of Earth's upper atmosphere, and SuperDARN specifically studies ionosphere-magnetosphere coupling, plasma convection, and auroral phenomena. PyDARN keywords include "ionosphere_thermosphere_mesosphere" from PyHC registry.

---

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** SuperDARN Data Visualization Working Group
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Author 2:**
- **Name:** C. J. Martin
- **Author Identifier:** https://orcid.org/0000-0002-8278-9783
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: Not found

**Author 3:**
- **Name:** R. A. Rohel
- **Author Identifier:** https://orcid.org/0000-0003-2208-1553
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: Not found

**Author 4:**
- **Name:** D. D. Billett
- **Author Identifier:** https://orcid.org/0000-0002-8905-8609
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: Not found

**Author 5:**
- **Name:** P. Pitzer
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: Not found

**Author 6:**
- **Name:** D. Galeshuck
- **Author Identifier:** https://orcid.org/0000-0003-3985-4225
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: Not found

**Author 7:**
- **Name:** B. S. R. Kunduri
- **Author Identifier:** https://orcid.org/0000-0002-7406-7641
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: Not found

**Author 8:**
- **Name:** K. Khanal
- **Author Identifier:** https://orcid.org/0000-0003-3927-7501
- **Affiliation:**
  - Organization: University of Alabama
  - Affiliation Identifier: Not found

**Author 9:**
- **Name:** A. Hiyadutuje
- **Author Identifier:** https://orcid.org/0000-0002-3391-8737
- **Affiliation:**
  - Organization: SANSA
  - Affiliation Identifier: Not found

**Author 10:**
- **Name:** S. Chakraborty
- **Author Identifier:** https://orcid.org/0000-0001-6792-0037
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: Not found

**Author 11:**
- **Name:** M. Detwiller
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: Not found

**Author 12:**
- **Name:** M. T. Schmidt
- **Author Identifier:** https://orcid.org/0000-0002-3265-977X
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: Not found

**Source:** DataCite API, Zenodo API

---

### 7. Software Name (MANDATORY)
**Value:** pyDARN

**Source:** GitHub repository name, setup.cfg, SoMEF, PyHC registry

---

### 8. Description (MANDATORY)
**Value:** Python data visualization library for the Super Dual Auroral Radar Network (SuperDARN). pyDARN provides comprehensive tools for reading, analyzing, and visualizing SuperDARN radar data, including range-time parameter plots, fan plots, grid plots, convection maps, ACF plots, and time-series visualizations. The package supports coordinate transformations between geographic, geomagnetic, and magnetic local time systems, and includes utilities for data filtering, range estimation, and virtual height calculations. pyDARN enables researchers to study ionosphere-magnetosphere coupling, plasma convection, and space weather phenomena using data from the international SuperDARN radar network.

**Source:** README.md, setup.cfg description, SoMEF, scientific context analysis
**Note:** First 150-200 characters: "Python data visualization library for the Super Dual Auroral Radar Network (SuperDARN). pyDARN provides comprehensive tools for reading, analyzing, and visualizing SuperDARN radar data, including range-time parameter plots, fan plots, grid plots, convection maps, ACF plots, and time-series visualizations."

---

### 9. Concise Description (OPTIONAL)
**Value:** Python visualization and analysis library for SuperDARN radar data, providing plotting tools, coordinate transformations, and data processing for ionospheric and magnetospheric research.

**Source:** Condensed from full description

---

### 10. Publication Date (RECOMMENDED)
**Value:** 2020-03-25

**Source:** DataCite API (first version release date), SoMEF (date_created: 2018-04-27T20:23:07Z for repository, first release: 2020-03-25)
**Note:** This is the publication date of the first official release (v1.0.0) on Zenodo

---

### 11. Publisher (RECOMMENDED)

**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/03cpe7c52 (Zenodo ROR ID)

**Source:** DataCite API, Zenodo API

---

### 12. Version (RECOMMENDED)

**Latest Version (v4.1.2):**
- **Version Number:** v4.1.2
- **Version Date:** 2025-05-16
- **Version Description:** This patch release fixes a bug with installation from PyPI that affected v4.1.1, and updates ownership of ADE, ADW, KOD, KSR, MCM, and SPS radars to Penn State University.
- **Version PID:** https://doi.org/10.5281/zenodo.15441879

**Source:** DataCite API, Zenodo API, SoMEF releases, git tags

---

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** SoMEF (GitHub API), setup.cfg (python_requires = >=3.8), README.md
**Note:** Specifically supports Python 3.8, 3.9, 3.10, 3.11 according to setup.cfg classifiers

---

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.3389/fspas.2022.1022690

**Source:** README.md
**Note:** Shi, X., Schmidt, M., Martin, C. J., Billett, D. D., Bland, E., Tholley, F. H., Frissell, N. A., Khanal, K., Coyle, S., Chakraborty, S., Detwiller, M., Kunduri, B., & McWilliams, K. (2022). pyDARN: A Python software for visualizing SuperDARN radar data. Frontiers in Astronomy and Space Sciences.

---

### 15. License (RECOMMENDED)

**License:**
- **License:** GNU Lesser General Public License v3.0 only
- **License URI:** https://www.gnu.org/licenses/lgpl-3.0-standalone.html

**Source:** DataCite API (SPDX identifier: lgpl-3.0), LICENSE file, SoMEF
**Note:** SPDX identifier: LGPL-3.0-only

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- ionosphere_thermosphere_mesosphere
- data_analysis
- general
- superdarn
- plots
- superdarn-data
- visualization
- radar
- space physics
- magnetosphere

**Source:** PyHC registry, GitHub topics (SoMEF), scientific context
**Note:** PyHC provides curated keywords: ionosphere_thermosphere_mesosphere, general, data_analysis, superdarn

---

### 17. Data Sources (OPTIONAL)
**Values:**
- Observatory/Mission-specific

**Source:** Code analysis, documentation
**Note:** pyDARN reads SuperDARN-specific data formats (DMAP files, Borealis HDF5 files). See SuperDARN data access documentation at https://pydarn.readthedocs.io/en/main/user/superdarn_data/

---

### 18. Input File Formats (RECOMMENDED)
**Values:**
- HDF5
- Other

**Source:** Code analysis (superdarn_io.py), documentation
**Note:** Supports SuperDARN DMAP format (binary format specific to SuperDARN) and Borealis HDF5 format. DMAP is a custom binary format not in the standard list, hence "Other" is also selected.

---

### 19. Output File Formats (RECOMMENDED)
**Value:** Not found

**Source:** Code analysis
**Note:** pyDARN is primarily a visualization library. Output is typically in the form of matplotlib figures (PNG, PDF, SVG, etc. via matplotlib's save functions), but the library itself does not explicitly specify output file format support.

---

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows
- OS Independent

**Source:** Installation documentation, SoMEF (continuous integration configurations suggest cross-platform testing)
**Note:** Python package installable via pip on all major operating systems. Installation guide mentions Ubuntu, OpenSuse, Fedora, OSX, and Windows.

---

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Source:** Installation requirements analysis
**Note:** Pure Python implementation with standard scientific computing dependencies (NumPy, matplotlib). No architecture-specific compilation requirements.

---

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Not found in standard list

**Source:** N/A
**Note:** pyDARN studies phenomena such as plasma convection, auroral electrojets, ionospheric irregularities, and space weather effects, but these are not in the current HSSI controlled vocabulary for Related Phenomena.

---

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** PyHC registry (software_maturity: Good), SoMEF (date_updated: 2025-10-01T21:17:05Z), GitHub activity
**Note:** The software has reached a stable, usable state (v4.x releases) and is being actively developed with recent updates and releases.

---

### 24. Documentation (RECOMMENDED)
**Value:** https://pydarn.readthedocs.io/en/main/

**Source:** README.md, setup.cfg, SoMEF, PyHC registry

---

### 25. Funder (OPTIONAL)
**Value:** Not found

**Source:** DataCite API shows no funding references
**Note:** No funding information found in DataCite metadata, README, or documentation

---

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Source:** DataCite API shows no funding references
**Note:** No award information found in DataCite metadata, README, or documentation

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** https://doi.org/10.3389/fspas.2022.1022690

**Source:** README.md
**Note:** This is also listed as the Reference Publication. Additional publications citing pyDARN would need to be identified through literature search.

---

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Source:** N/A
**Note:** pyDARN works with SuperDARN radar data, but specific dataset DOIs are not provided in the repository or documentation. SuperDARN data access information is available at https://pydarn.readthedocs.io/en/main/user/superdarn_data/

---

### 29. Related Software (OPTIONAL)
**Values:**
- pydarnio (dependency, handles I/O operations)
- aacgmv2 (dependency, coordinate transformations)
- cartopy (dependency, geographic plotting)

**Source:** setup.cfg dependencies, code analysis
**Note:** Key dependencies:
- pydarnio >= 1.3.0 - SuperDARN data I/O library
- aacgmv2 - AACGM coordinate transformation library
- cartopy >= 0.22.0 - Geographic mapping library
- matplotlib >= 3.7.0 - Plotting library
- numpy - Numerical computing
- scipy < 1.15.0 - Scientific computing
- pyyaml - YAML parsing

---

### 30. Interoperable Software (OPTIONAL)
**Value:** Not found

**Source:** N/A
**Note:** While pyDARN has dependencies, explicit interoperability demonstrations with other PyHC packages are not documented in the repository.

---

### 31. Related Instruments (OPTIONAL)
**Value:** SuperDARN radars (international network of HF coherent scatter radars)

**Source:** Software name, description, scientific context
**Note:** pyDARN is designed specifically for the SuperDARN radar network, which consists of 35+ radars worldwide. Individual radar identifiers are managed in the code (superdarn_radars.py, RadarID enum), but no persistent instrument identifiers (DOIs) are available.

---

### 32. Related Observatories (OPTIONAL)
**Value:** SuperDARN (Super Dual Auroral Radar Network)

**Source:** Software name, description, documentation
**Note:** SuperDARN is an international scientific collaboration operating a network of high-frequency radars for studying the upper atmosphere and ionosphere.

---

### 33. Logo (OPTIONAL)
**Value:** https://raw.githubusercontent.com/SuperDARN/pydarn/master/docs/imgs/pydarn_logo.png

**Source:** README.md, SoMEF, PyHC registry

---

## Extraction Metadata

### Automated Extraction Methods Used:
1. ✅ DataCite API queried successfully
2. ✅ Zenodo API queried successfully
3. ✅ SoMEF executed successfully
4. ✅ PyHC registry checked (found in projects.yml)

### Manual Examination Completed:
- ✅ README.md
- ✅ LICENSE file
- ✅ setup.cfg
- ✅ pyproject.toml
- ✅ version.py
- ✅ Package structure analysis
- ✅ Code analysis for functionality
- ✅ Git tags for version information
- ✅ Documentation structure

### Data Source Priority (in order of trustworthiness):
1. PyHC registry (manually curated)
2. DataCite/Zenodo APIs (official DOI metadata)
3. Repository files (LICENSE, setup.cfg, README.md)
4. SoMEF (automated extraction)
5. Code analysis

### Confidence Assessment:
- **High confidence fields:** Software Name, Code Repository, Description, Authors, License, Version, Programming Language, Documentation, DOI
- **Medium confidence fields:** Software Functionality, Related Region, Keywords, Operating System
- **Low confidence/Not found:** Funder, Award Title, Related Datasets, Interoperable Software, Related Phenomena

---

## Notes

1. **Version discrepancy:** The repository's current code shows version 4.1.1 in version.py, but the latest Zenodo release is v4.1.2 (released 2025-05-16). This is expected as the Zenodo release happens after tagging but before updating the development branch.

2. **PyHC Package:** pyDARN is a recognized PyHC (Python in Heliophysics Community) package with "Good" ratings for community, documentation, software maturity, python3, and license. Testing is rated "Partially met."

3. **SuperDARN Context:** The Super Dual Auroral Radar Network (SuperDARN) is an international collaboration of HF radar systems designed to study geospace phenomena, particularly in the polar regions. pyDARN serves as the primary Python visualization toolkit for this community.

4. **Software Maturity:** Active development with regular releases. The v4.x series indicates a mature, stable API. Recent updates show ongoing maintenance and feature development.

5. **Comprehensive Functionality:** pyDARN provides end-to-end workflow support for SuperDARN data: reading data files, coordinate transformations, data processing/filtering, and multiple visualization types (range-time, fan, grid, maps, ACF, IQ, power, time-series).

6. **Documentation Quality:** Extensive ReadTheDocs documentation with user guides, installation instructions, API reference, and tutorials. Jupyter notebook with examples available on Zenodo.
