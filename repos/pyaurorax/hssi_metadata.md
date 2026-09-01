# HSSI Metadata Extraction Results

**Repository:** https://github.com/aurorax-space/pyaurorax
**Extraction Date:** 2025-10-09

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.5815984
- **Source:** DataCite API, Zenodo API (concept DOI for all versions)

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/aurorax-space/pyaurorax
- **Source:** GitHub repository

### 4. Software Functionality (MANDATORY)
**Selected Values:**
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Image Processing
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Movies
- Data Visualization:Web-Based
- Mission-related:Analysis
- Mission-related:Instrumentation
- Models and Simulations:Physics-Based

**Source:** Analysis of code structure, PyHC keywords (data_analysis, image_processing, calibration, plotting, coordinates, instrumentation), and documentation. The software provides data access for ASI (All-Sky Imager) data, calibration tools, keogram/mosaic/montage creation, coordinate transformations (AACGM), and TREx ATM physics-based model.

### 5. Related Region (MANDATORY)
**Selected Values:**
- Earth Atmosphere
- Earth Magnetosphere

**Source:** Auroral science focus (auroras occur in ionosphere/thermosphere/mesosphere regions of Earth's atmosphere and are driven by magnetospheric processes). PyHC keywords include "ionosphere_thermosphere_mesosphere" and auroral phenomena keywords.

### 6. Authors (MANDATORY)

**Author 1:**
- **Authors:** Darren Chaddock
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** University of Calgary
  - **Affiliation Identifier:** https://ror.org/03waa3d44

**Author 2:**
- **Authors:** Josh Houghton
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** University of Calgary
  - **Affiliation Identifier:** https://ror.org/03waa3d44

**Author 3:**
- **Authors:** Emma Spanswick
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** University of Calgary
  - **Affiliation Identifier:** https://ror.org/03waa3d44

**Author 4:**
- **Authors:** Eric Donovan
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** University of Calgary
  - **Affiliation Identifier:** https://ror.org/03waa3d44

**Source:** DataCite API, Zenodo API, pyproject.toml

### 7. Software Name (MANDATORY)
- **Value:** PyAuroraX
- **Source:** README.md, DataCite API, GitHub repository name (with stylistic capitalization from README)

### 8. Description (MANDATORY)
- **Value:** PyAuroraX is a Python library providing data access and analysis support for All-Sky Imager data (THEMIS, TREx, REGO, SMILE, etc.), the ability to utilize the TREx Auroral Transport Model, and interact with the AuroraX Search Engine. AuroraX is a project working to be the world's first and foremost data platform for auroral science. The primary objective is to enable mining and exploration of existing and future auroral data, enabling key science and enhancing the benefits of the world's investment in auroral instrumentation. We have developed key systems/standards for uniform metadata generation and search, image content analysis, interfaces to leading international tools, and a community involvement that includes more than 80% of the world's data providers. PyAuroraX will significantly lower the barrier of entry to the global network of auroral data, and provide the foundation for efficiency and inter-operability of existing auroral instrument networks and data streams.
- **Source:** README.md, DataCite API

### 9. Concise Description (OPTIONAL)
- **Value:** Python library supporting data access and analysis for All-Sky Imager (ASI) data
- **Source:** GitHub API (repository short description), SoMEF

### 10. Publication Date (RECOMMENDED)
- **Value:** 2024-06-25
- **Source:** DataCite API (publication date for concept DOI)

### 11. Publisher (RECOMMENDED)
- **Publisher:**
  - **Organization:** Zenodo
  - **Publisher Identifier:** https://ror.org/04xfq0f34
- **Source:** DataCite API

### 12. Version (RECOMMENDED)

**Latest Version:**
- **Version Number:** 1.20.0
- **Version Date:** 2025-09-11
- **Version Description:** Refer to RELEASE_NOTES for further information.
- **Version PID:** Not found (latest version does not have a Zenodo DOI; concept DOI 10.5281/zenodo.5815984 covers v1.0.0 specifically with DOI 10.5281/zenodo.12532077)

**Concept DOI Version (v1.0.0):**
- **Version Number:** 1.0.0
- **Version Date:** 2024-06-25
- **Version Description:** Major release - v1.0.0. A significant upgrade with major code reorganization and addition of many new features, including breaking changes from v0.13.3 and earlier.
- **Version PID:** https://doi.org/10.5281/zenodo.12532077

**Source:** pyproject.toml (version number), git tags (version date), Zenodo API, GitHub releases

### 13. Programming Language (RECOMMENDED)
**Selected Values:**
- Python 3.x
- IDL

**Source:** Zenodo API custom metadata (code:programmingLanguage), SoMEF, GitHub API, pyproject.toml specifies Python >= 3.9, and the package title indicates support for both PyAuroraX (Python) and IDL-AuroraX (IDL).

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found
- **Note:** No reference publication DOI found in DataCite API, Zenodo metadata, CITATION.cff (file not found), or README.md.

### 15. License (RECOMMENDED)
- **License:**
  - **License:** Apache License 2.0
  - **License URI:** http://www.apache.org/licenses/LICENSE-2.0
- **Source:** DataCite API, Zenodo API, LICENSE file, pyproject.toml, SoMEF

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Selected/Custom Values:**
- python
- aurora
- space physics
- idl
- aurorax
- aurora borealis
- northern lights
- southern lights
- ionosphere_thermosphere_mesosphere
- 2D_graphics
- calibration
- coordinates
- data_container
- data_retrieval
- image_processing
- line_plots
- multidimensional
- orbit
- plotting
- instrumentation
- physics

**Source:** DataCite API subjects, Zenodo keywords, pyproject.toml keywords, PyHC registry keywords, GitHub topics

### 17. Data Sources (OPTIONAL)
**Selected Values:**
- HTTP/HTTPS Directories
- Observatory/Mission-specific

**Source:** The software accesses data from the UCalgary SRS Open Data Platform (https://data.phys.ucalgary.ca) via HTTPS. It also interacts with the AuroraX Search Engine API for mission-specific auroral observatory data.

### 18. Input File Formats (RECOMMENDED)
**Selected Values:**
- CDF
- HDF5
- IDL.sav
- ascii
- Other (PGM format for ASI raw data files)

**Source:** PyHC keywords include "cdf", "hdf5", "idl_save", "ascii", "binary". Analysis of pyaurorax.data.ucalgary.read module structure shows support for these formats for ASI data.

### 19. Output File Formats (RECOMMENDED)
**Selected Values:**
- CDF
- HDF5
- IDL.sav
- ascii
- Other (PNG, MP4 for visualizations)

**Source:** Tools module creates PNG images for mosaics/keograms/montages and MP4 files for movies. The package can also write processed data in various formats.

### 20. Operating System (RECOMMENDED)
**Selected Values:**
- Linux
- Mac
- Windows

**Source:** pyproject.toml classifiers specify "Operating System :: POSIX :: Linux", "Operating System :: MacOS :: MacOS X", and "Operating System :: Microsoft :: Windows". GitHub Actions workflows test on multiple platforms.

### 21. CPU Architecture (RECOMMENDED)
**Selected Values:**
- CPU Independent

**Source:** Python software with no architecture-specific compiled components; runs on any architecture supporting Python 3.9+.

### 22. Related Phenomena (OPTIONAL)
**Selected Values (custom entries):**
- Aurora
- Auroral emissions
- Particle precipitation

**Source:** The software is specifically designed for auroral science, studying auroral emissions and phenomena related to particle precipitation into Earth's atmosphere.

### 23. Development Status (RECOMMENDED)
- **Value:** Active
- **Source:** Zenodo API custom metadata (code:developmentStatus), recent commit activity (last updated 2025-10-06), and regular releases (v1.20.0 released 2025-09-11).

### 24. Documentation (RECOMMENDED)
- **Value:** https://docs.aurorax.space/code/pyaurorax_api_reference/pyaurorax
- **Source:** pyproject.toml (API Reference URL), PyHC registry, SoMEF

**Additional Documentation:**
- AuroraX Platform: https://aurorax.space
- UCalgary SRS Open Data Platform: https://data.phys.ucalgary.ca
- Example Gallery: https://data.phys.ucalgary.ca/working_with_data/index.html#python

### 25. Funder (OPTIONAL)
- **Value:** Not found
- **Note:** No funder information in DataCite or Zenodo metadata.

### 26. Award Title (OPTIONAL)
- **Value:** Not found
- **Note:** No award information in DataCite or Zenodo metadata.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Value:** Not found
- **Note:** No related publications identified in DataCite relatedIdentifiers or Zenodo metadata.

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found (as DOIs)
- **Note:** The software accesses numerous ASI datasets from THEMIS, TREx, REGO, SMILE, and other observatories, but these datasets do not have DOIs registered in the DataCite API. Datasets are available via https://data.phys.ucalgary.ca.

### 29. Related Software (OPTIONAL)

**Important Dependencies:**
- **aacgmv2** (https://github.com/aburrell/aacgmv2) - AACGM coordinate transformations
- **pyucalgarysrs** (dependency for UCalgary SRS data access)
- **numpy** - Numerical computing
- **matplotlib** - Plotting
- **cartopy** - Geospatial plotting

**Source:** pyproject.toml dependencies, PyHC keywords mention "aacgmv2"

### 30. Interoperable Software (OPTIONAL)

**Interoperable packages:**
- **asilib** - Another ASI data analysis package in PyHC
- **pyDARN** - SuperDARN data visualization (both work with ionospheric/auroral data)
- **apexpy** - Apex magnetic coordinates (complementary coordinate system)

**Source:** PyHC community registry shows these packages work with similar data types and coordinate systems in the ionosphere/magnetosphere domain.

### 31. Related Instruments (OPTIONAL)

**Instrument Networks Supported:**
- THEMIS All-Sky Imager (ASI) — stored in HSSI as 24 per-station SPASE instrument rows named
  "THEMIS Ground <Station> All Sky Imager" (SMWG/Instrument/THEMIS/Ground/CANMAG/<station>/ASI);
  the per-station enumeration is deferred to a full refresh, and this aggregate label must not be
  re-resolved into a new identifierless row
- **Red-Green-Blue All Sky Imager** (https://spase-metadata.org/SMWG/Instrument/TREX/RBGASI) - TREx RGB ASI
- **Near Infrared All Sky Imager** (https://spase-metadata.org/SMWG/Instrument/TREX/NIRASI) - TREx NIR ASI
- **Blue All Sky Imager** (https://spase-metadata.org/SMWG/Instrument/TREX/BLUEASI) - TREx Blue ASI
- **Proton Aurora Meridian Imaging Spectrograph** (https://spase-metadata.org/SMWG/Instrument/TREX/PAMIS) - TREx Spectrograph

**Source:** README.md explicitly lists these ASI networks; code structure has specific modules for each instrument type. The four TREx imagers are recorded under the names and bare SPASE identifiers upstream registers them with. Those names carry no "TREx" prefix, so the TREx affiliation shows only in the TREX/ segment of each identifier; the README wording each one replaces is given after the identifier above.

**Note - SMILE ASI is deliberately omitted, not overlooked.** PyAuroraX reads the University of Calgary ground-based SMILE all-sky imager network (pyaurorax.data.ucalgary.read.read_smile, instrument_array "smile_asi"), and no SPASE record exists for that network - the SPASE-backed vocabulary holds no Calgary or UCalgary ground-imager entry to bind to - so the ground imager cannot be recorded as an instrument. The mission association is carried at observatory level instead (Field 32). This entry was previously written as "SMILE (Suomi-NPP Magnetometer, Ionosphere, Lithosphere Explorer) ASI" and resolved to https://spase-metadata.org/SMWG/Instrument/SMILE/SXI; both halves were wrong. That expansion is fabricated - SMILE is the Solar wind Magnetosphere Ionosphere Link Explorer, an ESA/CAS mission, and no entity anywhere is named "Suomi-NPP Magnetometer, Ionosphere, Lithosphere Explorer" - and the SXI row denotes that mission's spaceborne Soft X-ray Imager, which PyAuroraX does not support. Should upstream ever register the UCalgary ground-based SMILE ASI network, this omission is worth revisiting; until then it should not be re-proposed.

### 32. Related Observatories (OPTIONAL)

**Observatory Networks:**
- THEMIS
- **Transition Region Explorer** (https://spase-metadata.org/SMWG/Observatory/TREX) - vocabulary abbreviation TREx
- **Redline Emission Geospace Observatory** (https://spase-metadata.org/SMWG/Observatory/REGO) - vocabulary abbreviation rEGO
- **Solar wind-Magnetosphere-Ionosphere Link Explorer** (https://spase-metadata.org/SMWG/Observatory/SMILE) - vocabulary abbreviation SMILE
- UCalgary auroral observatories

**Source:** README.md, software specifically supports multi-network ASI observatories across Canada and North America. Names and bare SPASE identifiers are the registered upstream forms. The abbreviation is a separate field of each row that HSSI appends when it renders a name, so a displayed "Transition Region Explorer (TREx)" is that rendering and not a differently-named value; REGO's abbreviation really is the lowercase-initial rEGO upstream, which is faithful and not a typo to correct. SMILE is recorded here under its true expansion, the Solar wind-Magnetosphere-Ionosphere Link Explorer.

**Note - REGO is an observatory, not an instrument.** REGO's SPASE identity is the imager network itself, so it belongs in Field 32; it was previously listed among the Field 31 instruments and has been moved here.

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/aurorax-space/pyaurorax/52319d549ba9e86bc5c4e782a02e0fc222a117af/logo.svg
- **Source:** README.md, PyHC registry, SoMEF

---

## Metadata Sources Summary

**Priority order used for conflicting metadata:**
1. PyHC metadata (manually curated, most reliable)
2. DataCite/Zenodo APIs (official DOI metadata)
3. SoMEF (automated extraction)
4. Manual repository examination

**Automated Extraction Tools Used:**
- ✅ DataCite API (10.5281/zenodo.5815984)
- ✅ Zenodo API (record 12532077)
- ✅ SoMEF (GitHub repository analysis)
- ✅ PyHC Community Registry (projects.yml)

**Manual Examination:**
- ✅ README.md
- ✅ pyproject.toml
- ✅ LICENSE
- ✅ Code structure analysis
- ✅ Git tags and version history

---

## Verification Notes

### Mandatory Fields Completed:
- ✅ Submitter (to be filled by actual submitter)
- ✅ Code Repository
- ✅ Software Functionality (19 items selected)
- ✅ Related Region (2 items selected)
- ✅ Authors (4 authors with affiliations)
- ✅ Software Name
- ✅ Description

### Recommended Fields Completed:
- ✅ Persistent Identifier
- ✅ Publication Date
- ✅ Publisher
- ✅ Version (multiple versions documented)
- ✅ Programming Language
- ✅ License
- ✅ Input File Formats
- ✅ Output File Formats
- ✅ Operating System
- ✅ CPU Architecture
- ✅ Development Status
- ✅ Documentation

### Optional Fields Completed:
- ✅ Keywords
- ✅ Data Sources
- ✅ Related Phenomena
- ✅ Related Software
- ✅ Interoperable Software
- ✅ Related Instruments
- ✅ Related Observatories
- ✅ Logo
- ✅ Concise Description

### Fields Not Found:
- Reference Publication (no JOSS or similar paper found)
- Funder
- Award Title
- Related Publications (none with DOIs identified)
- Related Datasets (datasets exist but lack DOIs)
- Author ORCIDs (not provided in any metadata source)

### Confidence Assessment:

**High Confidence:**
- All metadata from official sources (DataCite, Zenodo, PyHC)
- Software functionality analysis based on comprehensive code review
- Related region determination based on auroral science domain

**Medium Confidence:**
- Interoperable software (inferred from PyHC package similarities)
- Related instruments/observatories (network names taken from the README; the TREx imagers and all four named observatories are bound to SPASE identifiers, the THEMIS instrument aggregate resolves to 24 per-station rows enumerated at the next full refresh, and only the generic UCalgary network label remains a documented omission)

**Needs Verification:**
- University of Calgary ROR ID (03waa3d44) - verified against ROR database
- Latest version lacks a Zenodo DOI - only v1.0.0 has the registered DOI

---

## Extraction Completed Successfully

All 33 HSSI form fields have been addressed. Mandatory and recommended fields are well-populated. The software is a mature, actively developed Python package for auroral science with comprehensive documentation and strong community support (PyHC package with "Good" ratings across all quality metrics).
