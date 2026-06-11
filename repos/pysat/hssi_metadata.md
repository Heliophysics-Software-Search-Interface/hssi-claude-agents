# HSSI Metadata Extraction Results

**Repository:** https://github.com/pysat/pysat
**Extraction Date:** 2026-05-06

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.1199703
- **Role:** Software concept DOI
- **Source:** `pysat/citation.txt`; source file DOI headers; Zenodo and DataCite records for the pysat software concept DOI.
- **Note:** The README Zenodo badge currently resolves to the latest version DOI, https://doi.org/10.5281/zenodo.15059161. The concept DOI is used here for the persistent identifier.

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/pysat/pysat
- **Source:** User-provided URL; git remote origin; `pyproject.toml` project URLs.

### 4. Software Functionality (MANDATORY)
- **Coordinate Transforms**
- **Data Processing and Analysis**
- **Data Processing and Analysis:Analysis**
- **Data Processing and Analysis:Data Access and Retrieval**
- **Data Processing and Analysis:File Format Conversion**
- **Data Processing and Analysis:Processing**
- **Data Processing and Analysis:Time Series Analysis**

**Rationale:** pysat provides a framework for downloading, loading, cleaning, managing, processing, and analyzing scientific instrument data. Its public `Instrument`, `Constellation`, `Files`, `Meta`, and `Orbits` APIs support data access workflows, file discovery, local and remote file management, time-indexed loading, orbit/day/file iteration, custom processing functions, and multi-instrument analysis. The `pysat.utils.io` public API reads and writes netCDF3/4 files, including pysat metadata handling, and the `Instrument.to_netcdf4` method exports loaded data. The public coordinate utilities include longitude range adjustment, solar local time calculation, and common coordinate-grid helpers, but no more specific HSSI coordinate-transform subcategory is asserted.

**Source:** `README.md`; `docs/introduction.rst`; `docs/api.rst`; `docs/tutorial/tutorial_iteration.rst`; `docs/tutorial/tutorial_orbit.rst`; `docs/tutorial/tutorial_files.rst`; `pysat/_instrument.py`; `pysat/_constellation.py`; `pysat/_files.py`; `pysat/_orbits.py`; `pysat/utils/io.py`; `pysat/utils/coords.py`.

### 5. Related Region (MANDATORY)
- **Earth Atmosphere**
- **Earth Magnetosphere**
- **Interplanetary Space**
- **Solar Environment**

**Rationale:** pysat is a heliophysics and space-physics data-analysis framework. Repository keywords include ionosphere, atmosphere, thermosphere, magnetosphere, heliosphere, space, and satellites. Documentation and tutorials describe use with in situ satellite measurements, observational and modeled space science measurements, DMSP ionospheric data, C/NOFS data, ACE real-time solar-wind data, and ecosystem packages for NASA, Madrigal, space-weather, and model data.

**Source:** `pyproject.toml` keywords; `README.md`; `docs/introduction.rst`; `docs/ecosystem.rst`; `docs/tutorial/tutorial_basics.rst`; `docs/tutorial/tutorial_constellation.rst`; PyHC core registry exact match.

### 6. Authors (MANDATORY)

#### Author 1:
- **Author Name:** Russell Stoneback
- **Author Identifier:** https://orcid.org/0000-0001-7216-4336
- **Affiliation - Organization:** Cosmic Studio
- **Affiliation - Identifier:** Not found

#### Author 2:
- **Author Name:** Jeff Klenzing
- **Author Identifier:** https://orcid.org/0000-0001-8321-6074
- **Affiliation - Organization:** Goddard Space Flight Center
- **Affiliation - Identifier:** Not found

#### Author 3:
- **Author Name:** Angeline G. Burrell
- **Author Identifier:** https://orcid.org/0000-0001-8875-9326
- **Affiliation - Organization:** U.S. Naval Research Laboratory
- **Affiliation - Identifier:** Not found

#### Author 4:
- **Author Name:** Asher Pembroke
- **Author Identifier:** Not found
- **Affiliation - Organization:** Predictive Science
- **Affiliation - Identifier:** Not found

#### Author 5:
- **Author Name:** Carey Spence
- **Author Identifier:** https://orcid.org/0000-0001-8340-5625
- **Affiliation - Organization:** The University of Texas at Dallas
- **Affiliation - Identifier:** Not found

#### Author 6:
- **Author Name:** Jonathon M. Smith
- **Author Identifier:** https://orcid.org/0000-0002-8191-4765
- **Affiliation 1 - Organization:** Catholic University of America
- **Affiliation 1 - Identifier:** https://ror.org/047yk3s18
- **Affiliation 2 - Organization:** Goddard Space Flight Center
- **Affiliation 2 - Identifier:** https://ror.org/0171mag52

#### Author 7:
- **Author Name:** Matthew Depew
- **Author Identifier:** Not found
- **Affiliation - Organization:** The University of Texas at Dallas
- **Affiliation - Identifier:** Not found

#### Author 8:
- **Author Name:** Aadarsh Govada
- **Author Identifier:** https://orcid.org/0009-0004-7873-5899
- **Affiliation 1 - Organization:** Universities Space Research Association
- **Affiliation 1 - Identifier:** https://ror.org/043pgqy52
- **Affiliation 2 - Organization:** Goddard Space Flight Center
- **Affiliation 2 - Identifier:** https://ror.org/0171mag52

#### Author 9:
- **Author Name:** Ryan Fuller
- **Author Identifier:** Not found
- **Affiliation - Organization:** The University of Texas at Dallas
- **Affiliation - Identifier:** Not found

#### Author 10:
- **Author Name:** Teresa Esman
- **Author Identifier:** https://orcid.org/0000-0003-0382-6281
- **Affiliation - Organization:** Goddard Space Flight Center
- **Affiliation - Identifier:** https://ror.org/0171mag52

#### Author 11:
- **Author Name:** Veronica Von Bose
- **Author Identifier:** Not found
- **Affiliation - Organization:** The University of Texas at Dallas
- **Affiliation - Identifier:** Not found

#### Author 12:
- **Author Name:** Nathaniel Hargrave
- **Author Identifier:** Not found
- **Affiliation - Organization:** The University of Texas at Dallas
- **Affiliation - Identifier:** Not found

#### Author 13:
- **Author Name:** Gayatri Iyer
- **Author Identifier:** Not found
- **Affiliation - Organization:** The University of Texas at Dallas
- **Affiliation - Identifier:** Not found

#### Author 14:
- **Author Name:** Silvio Leite
- **Author Identifier:** https://orcid.org/0000-0003-1707-7963
- **Affiliation - Organization:** Olist
- **Affiliation - Identifier:** Not found

**Source:** `.zenodo.json` creators; Zenodo/DataCite creators for the v3.2.2 software record; author ORCID and contributor profiles; CEDAR 2023 presentation; ROR records; corroborated by `pyproject.toml` package author summary and git shortlog.

### 7. Software Name (MANDATORY)
- **Name:** pysat
- **Full Title:** pysat: Python Satellite Data Analysis Toolkit
- **Source:** `pyproject.toml`; `README.md`; PyHC core registry exact match.

### 8. Description (MANDATORY)
- **Description:** pysat, the Python Satellite Data Analysis Toolkit, is a Python package and framework for science data management and analysis across disparate space-science data platforms. It provides a consistent `Instrument` interface for finding, downloading, loading, cleaning, managing, processing, and analyzing time-indexed scientific measurements, with support for pandas and xarray data structures, metadata handling, orbit/day/file iteration, and custom processing functions. The core package supplies reusable I/O, metadata, file-management, orbit, constellation, and coordinate utility APIs, while the broader pysat ecosystem provides plug-ins for public scientific datasets and analysis workflows, including NASA, Madrigal, CDAAC, model, mission, and space-weather packages.
- **Source:** `README.md`; `docs/introduction.rst`; `docs/ecosystem.rst`; `docs/api.rst`; `pyproject.toml`; PyHC core registry.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Python framework for downloading, loading, managing, processing, and analyzing satellite and space-science data across instrument plug-ins.
- **Source:** Synthesized from `README.md`, `pyproject.toml`, and PyHC core registry description.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2015-04-18
- **Source:** Earliest git tag, `v0.1.2.3`, dated 2015-04-18.
- **Note:** GitHub reports the repository was created on 2015-04-05; this field uses the first tagged software release date.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** DataCite and Zenodo records for https://doi.org/10.5281/zenodo.1199703.

### 12. Version (RECOMMENDED)
- **Version Number:** v3.2.2
- **Version Date:** 2025-03-20
- **Version Description:** Bug-fix and maintenance release that includes test data in the source distribution, updates `.gitignore`, updates Zenodo affiliations and references, clarifies the public-release statement, and updates operational tests for Python 3.9 and Ubuntu 22.04.
- **Version PID:** https://doi.org/10.5281/zenodo.15059161
- **Source:** `pyproject.toml`; `setup.cfg`; `CHANGELOG.md`; git tag `v3.2.2`; Zenodo/DataCite v3.2.2 record.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x**

**Source:** `pyproject.toml` requires Python >=3.9 and classifies support for Python 3.9 through 3.12; repository source is Python.

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication DOI:** https://doi.org/10.1029/2018JA025297
- **Citation Context:** Stoneback et al. (2018), "PYSAT: Python Satellite Data Analysis Toolkit," Journal of Geophysical Research: Space Physics.
- **Source:** `README.md`; `.zenodo.json`; `docs/citing.rst`; Crossref DOI metadata.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html
- **SPDX ID:** BSD-3-Clause
- **Source:** `LICENSE`; `pyproject.toml` BSD classifier; GitHub and DataCite license metadata.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- pysat
- Python
- heliophysics
- space physics
- satellite data
- space science
- data analysis
- data retrieval
- data management
- time series
- orbit
- instrument data
- metadata
- netCDF
- observations
- models
- ionosphere
- thermosphere
- atmosphere
- magnetosphere
- heliosphere
- solar wind
- space weather
- plasma
- NASA data
- electric fields
- radar measurements
- CubeSat

**Source:** `pyproject.toml`; `.zenodo.json`; PyHC core registry; `README.md`; documentation tutorials; GitHub repository topics.

### 17. Data Sources (OPTIONAL)
- **Observatory/Mission-specific**
- **Other**

**Note:** The core package provides the data-access framework and instrument interface. Concrete data repositories are usually implemented by instrument modules or ecosystem packages, while documentation demonstrates mission/observatory-specific and user-defined data sources.

**Source:** `README.md`; `docs/ecosystem.rst`; `docs/new_instrument.rst`; `docs/tutorial/tutorial_basics.rst`; `pysat/_instrument.py`.

### 18. Input File Formats (RECOMMENDED)
- **netCDF3/4**
- **csv**
- **Other**

**Note:** pysat directly supports loading netCDF3/4 files through `pysat.utils.io.load_netcdf` and CSV files through `pysat.instruments.methods.general.load_csv_data`. The `Instrument` abstraction also supports plug-in-defined file formats.

**Source:** `pysat/utils/io.py`; `pysat/instruments/methods/general.py`; `docs/tutorial/tutorial_files.rst`; `docs/new_instrument.rst`.

### 19. Output File Formats (RECOMMENDED)
- **netCDF3/4**
- **ISTP-Compliant**

**Note:** pysat writes netCDF3/4 output through `Instrument.to_netcdf4` and `pysat.utils.io.inst_to_netcdf`. The output metadata convention is described as a simplified SPDF ISTP/IACG convention for netCDF.

**Source:** `pysat/_instrument.py`; `pysat/utils/io.py`; `docs/tutorial/tutorial_files.rst`.

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**

**Source:** `pyproject.toml` operating-system classifiers; GitHub Actions workflow testing on Ubuntu, macOS, and Windows.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Rationale:** pysat is a pure Python package with no repository-native compiled extension modules, GPU requirements, MPI requirements, or architecture-specific code paths. Some dependencies may provide native wheels, but no pysat architecture restriction was found.

**Source:** Repository source tree; `pyproject.toml`; CI configuration.

### 22. Related Phenomena (OPTIONAL)
- ionosphere
- thermosphere
- magnetosphere
- heliosphere
- solar wind
- space weather
- satellite observations
- ion drifts
- plasma parameters

**Source:** `pyproject.toml` keywords; `README.md`; `docs/tutorial/tutorial_basics.rst`; `docs/tutorial/tutorial_constellation.rst`; PyHC registry keywords.

### 23. Development Status (RECOMMENDED)
- **Active**

**Rationale:** The project has a stable public release, production/stable package classifier, PyHC "Good" maturity/testing/documentation signals, current documentation, GitHub Actions CI, and the latest repository release/tag v3.2.2 dated 2025-03-20.

**Source:** `pyproject.toml`; `CHANGELOG.md`; git tags and recent commits; PyHC core registry.

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://pysat.readthedocs.io/en/latest/
- **Source:** `pyproject.toml`; `README.md`; `.readthedocs.yml`; PyHC core registry.

### 25. Funder (OPTIONAL)

#### Funder 1:
- **Organization:** The Catholic University of America
- **Funder Identifier:** Not found

#### Funder 2:
- **Organization:** Cosmic Studio
- **Funder Identifier:** Not found

#### Funder 3:
- **Organization:** Defense Advanced Research Projects Agency Defense Sciences Office
- **Funder Identifier:** Not found

#### Funder 4:
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** Not found

#### Funder 5:
- **Organization:** National Oceanic and Atmospheric Administration
- **Funder Identifier:** Not found

#### Funder 6:
- **Organization:** National Science Foundation
- **Funder Identifier:** Not found

#### Funder 7:
- **Organization:** Office of Naval Research
- **Funder Identifier:** Not found

#### Funder 8:
- **Organization:** NOAA Constellation Observing System for Meteorology Ionosphere and Climate (COSMIC-2)
- **Funder Identifier:** Not found

#### Funder 9:
- **Organization:** NASA Ionospheric Connections Explorer (ICON)
- **Funder Identifier:** Not found

#### Funder 10:
- **Organization:** NASA Scintillation Observations and Response of the Ionosphere to Electrodynamics (SORTIE)
- **Funder Identifier:** Not found

#### Funder 11:
- **Organization:** NASA Scintillation Prediction Observations Research Task (SPORT)
- **Funder Identifier:** Not found

#### Funder 12:
- **Organization:** Goddard Space Flight Center
- **Funder Identifier:** https://ror.org/0171mag52

**Note:** The pysat project explicitly states that the listed institutions, missions, and programs provided funding for its development. Mission funders are therefore retained as project-reported funding sources. The Space Precipitation Impacts project is represented under Award Title, while its funding organization is listed here.

**Source:** `ACKNOWLEDGEMENTS.md`; `docs/funding.rst`; ROR.

### 26. Award Title (OPTIONAL)
#### Award 1:
- **Award Title:** Collaborative Research: Inferring High Latitude Convection Patterns Using SuperDARN, DMSP and ACE
- **Award Number:** 1259508

#### Award 2:
- **Award Title:** Collaborative Research: CEDAR--Assimilative Analysis of Low- and Mid-latitude Ionospheric Electrodynamics
- **Award Number:** AGS-1651393

#### Award 3:
- **Award Title:** NASA grant
- **Award Number:** NNX10AT02G

#### Award 4:
- **Award Title:** NASA ROSES-2020 B.5 Living With a Star Science program element
- **Award Number:** NNH20ZDA001N-LWS

#### Award 5:
- **Award Title:** NASA grant
- **Award Number:** 80NSSC18K1203

#### Award 6:
- **Award Title:** NASA Goddard Space Flight Center HSD Support Partnership
- **Award Number:** 80NSSC21M0180

#### Award 7:
- **Award Title:** U.S. Naval Research Laboratory award
- **Award Number:** N00173191G016

#### Award 8:
- **Award Title:** U.S. Naval Research Laboratory award
- **Award Number:** N0017322P0744

#### Award 9:
- **Award Title:** Space Precipitation Impacts (SPI)
- **Award Number:** Not found

**Note:** Awards 3, 5, 7, and 8 appear in the project's acknowledgements as award numbers only, with no public project title (Stoneback et al., 2023 describes the two NRL awards simply as Naval Research Laboratory support, and no NASA NSPIRES/USAspending title was found). They are labeled here by funding agency ("NASA grant", "U.S. Naval Research Laboratory award") to preserve the award numbers without asserting an unverified title.

**Source:** `ACKNOWLEDGEMENTS.md`; `docs/funding.rst`; National Science Foundation award records; NASA NSPIRES; USAspending award record; repository-linked publications and project acknowledgements.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Related Publication DOI:** https://doi.org/10.3389/fspas.2023.1119775
- **Citation Context:** Stoneback et al. (2023), "The pysat ecosystem," Frontiers in Astronomy and Space Science.
- **Source:** `README.md`; `.zenodo.json`; `docs/citing.rst`; Crossref DOI metadata.

### 28. Related Datasets (OPTIONAL)
- Not found

**Source:** Repository DOI search; `.zenodo.json`; README and documentation review; Zenodo/DataCite DOI review.

### 29. Related Software (OPTIONAL)
- Not found

**Source:** Repository and ecosystem review; software packages with demonstrated direct integration are classified under Interoperable Software.

### 30. Interoperable Software (OPTIONAL)

#### Interoperable Software 1:
- **Name/Repository:** pysatNASA
- **URL:** https://github.com/pysat/pysatNASA
- **Relationship:** Provides pysat `Instrument` and `Constellation` modules for NASA instruments and missions.

#### Interoperable Software 2:
- **Name/Repository:** pysatMadrigal
- **URL:** https://github.com/pysat/pysatMadrigal
- **Relationship:** Provides instrument modules that register with and run through pysat for Madrigal data access.

#### Interoperable Software 3:
- **Name/Repository:** pysatCDAAC
- **URL:** https://github.com/pysat/pysatCDAAC
- **Relationship:** Provides pysat `Instrument` and `Constellation` modules for COSMIC data products from CDAAC.

#### Interoperable Software 4:
- **Name/Repository:** pysatModels
- **URL:** https://github.com/pysat/pysatModels
- **Relationship:** Provides a pysat interface and instrument modules for model outputs, analysis, and model-data comparisons.

#### Interoperable Software 5:
- **Name/Repository:** pysatSpaceWeather
- **URL:** https://github.com/pysat/pysatSpaceWeather
- **Relationship:** Provides registered pysat instruments and analysis routines for real-time and historical space-weather products and indices.

#### Interoperable Software 6:
- **Name/Repository:** pysatCDF
- **URL:** https://github.com/pysat/pysatCDF
- **Relationship:** Reads NASA CDF files and exports their data and metadata directly into pysat format through `to_pysat()`.

**Source:** `README.md`; `docs/ecosystem.rst`; instrument and analysis documentation; tutorial integration examples; `ecosystem.txt`; pysatCDF repository and README.

### 31. Related Instruments (OPTIONAL)
- Not found

**Note:** Intentionally left empty. The instruments previously listed (C/NOFS VEFI DC magnetometer, DMSP IVM, and the four ACE real-time instruments EPAM/MAG/SIS/SWEPAM) were tutorial and demo examples drawn from ecosystem plug-in packages (pysatNASA, pysatMadrigal, pysatSpaceWeather), not instruments the core pysat framework is designed to support. The four ACE entries were a single realtime-constellation example expanding to four sub-instruments. Per HSSI Field 31 ("the instrument the software is designed to support"), an instrument-agnostic framework supports none specifically; instrument associations belong to the ecosystem packages' own records.

**Source:** `docs/examples/example_orbit.rst`; `docs/tutorial/tutorial_basics.rst`; `docs/tutorial/tutorial_constellation.rst`; `docs/ecosystem.rst`.

### 32. Related Observatories (OPTIONAL)
- Not found

**Note:** Intentionally left empty. The observatories previously listed (C/NOFS, DMSP, ACE, Dynamics Explorer 2, ICON, COSMIC, SuperDARN, Jicamarca Radio Observatory) were tutorial examples or illustrative name-drops — SuperDARN, JRO, and COSMIC trace to a single example sentence in `docs/new_instrument.rst` listing platforms one could write a module for. None is a mission/observatory the core framework is designed to support (HSSI Field 32). ICON's only deeper link is that pysat's netCDF output conventions derive from ICON file standards, which is already captured under Output File Formats (ISTP-Compliant) rather than as a supported observatory.

**Source:** `docs/examples/example_orbit.rst`; `docs/tutorial/tutorial_basics.rst`; `docs/tutorial/tutorial_constellation.rst`; `docs/new_instrument.rst`; `docs/ecosystem.rst`.

### 33. Logo (OPTIONAL)
- **Logo URL:** https://raw.githubusercontent.com/pysat/pysat/main/docs/images/logo.png
- **Source:** `README.md`; `docs/conf.py`; PyHC core registry.

---

## Extraction Notes

- **PyHC Status:** Exact match in PyHC core registry (`projects_core.yml`) by repository URL and package name.
- **SoMEF:** Raw output collected in `somef_output.json`; used only as corroborating evidence.
- **DOI Roles:** https://doi.org/10.5281/zenodo.1199703 is the software concept DOI; https://doi.org/10.5281/zenodo.15059161 is the v3.2.2 software version DOI; https://doi.org/10.1029/2018JA025297 is the reference publication DOI; https://doi.org/10.3389/fspas.2023.1119775 is a related publication DOI.
- **Citation caveat:** `pysat/citation.txt` still mentions v3.1, but the current package metadata, git tag, changelog, Zenodo, and DataCite records all identify v3.2.2 as the latest release.
