# HSSI Metadata Extraction Results

**HSSI Software ID:** c9f100c2-e502-4a61-94d5-87ae0f4d3646
**Repository:** https://github.com/jgieseler/solarmach
**Source Revision:** dbafa3b06e021c651df7ed41dc31649b441c8909
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-08-26
**Validation Status:** PASS
---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** To be filled by actual submitter
- **Submitter Email:** To be filled by actual submitter
- **Source:** Submitter information is intentionally deferred to the person who performs the submission.

### 2. Persistent Identifier (RECOMMENDED)
- **Persistent Identifier:** https://doi.org/10.5281/zenodo.7016783
- **Source:** Preserved from the existing HSSI record and confirmed as the Zenodo concept DOI by the Zenodo and DataCite APIs.

### 3. Code Repository (MANDATORY)
- **Code Repository:** https://github.com/jgieseler/solarmach
- **Source:** Preserved from the existing HSSI record and confirmed by `CITATION.cff`, `pyproject.toml`, and the GitHub repository.

### 4. Software Functionality (MANDATORY)
- **Values:**
  - Coordinate Transforms
  - Coordinate Transforms:Heliospheric
  - Coordinate Transforms:Solar
  - Data Processing and Analysis
  - Data Processing and Analysis:Analysis
  - Data Processing and Analysis:Data Access and Retrieval
  - Data Processing and Analysis:Data Reduction
  - Data Processing and Analysis:Field-line Tracing
  - Data Processing and Analysis:Image Processing
  - Data Processing and Analysis:Processing
  - Data Visualization
  - Data Visualization:2D Graphics
  - Data Visualization:3D Graphics
  - Data Visualization:Line Plots
  - Data Visualization:Movies
  - Data Visualization:Orbit Plots
  - Data Visualization:Web-Based
  - Models and Simulations
  - Models and Simulations:Data Guided
  - Models and Simulations:Empirical
  - Models and Simulations:Field-line Tracing
  - Models and Simulations:Physics-Based
- **Source:** Repository code and the documented example notebook. Public APIs transform Carrington and Stonyhurst heliographic coordinates; retrieve ephemerides, solar-wind measurements, and GONG maps; process solar magnetogram maps; calculate Parker-spiral and PFSS magnetic connections; reduce measurements to hourly means; trace field lines; and produce tabular, 2D, interactive 3D, HTML, and animated-GIF outputs. Every selected subcategory includes its required parent category.

### 5. Related Region (MANDATORY)
- **Values:**
  - Interplanetary Space
  - Solar Environment
  - Corona
  - Photosphere
  - Solar Wind
- **Source:** Interplanetary Space and Solar Environment are preserved from the existing HSSI record and confirmed by the repository's heliospheric Parker-spiral and solar-coronal PFSS functionality.
- **Evidence, Corona:** The documented PFSS extension explicitly "connects the heliospheric magnetic field (HMF) to the solar corona" (`examples/example.ipynb:58640`).
- **Evidence, Photosphere:** `plot_pfss` tracks an open field line to the photosphere (`solarmach/__init__.py:1227`), `trace_field_line` documents the same endpoint (`solarmach/pfss_utilities.py:303-306`), and the user-facing results table labels its output as a magnetic footpoint at the photosphere (`solarmach/__init__.py:1822`).
- **Evidence, Solar Wind:** `get_sw_speed` retrieves measured solar-wind bulk speed (`solarmach/__init__.py:93`), which parameterizes the Parker-spiral model (`solarmach/__init__.py:428-431,669,675`). Solar Wind therefore describes a medium that the software measures and models, not merely one crossed by a connectivity line.

### 6. Authors (MANDATORY)
- **Author:** Jan Gieseler
  - **Author Identifier:** https://orcid.org/0000-0003-1848-7067
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Author:** Nina Dresing
  - **Author Identifier:** https://orcid.org/0000-0003-3903-4649
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Author:** Johan Lauritz Freiherr von Forstner
  (given name `Johan Lauritz`, family name `Freiherr von Forstner`)
  - **Author Identifier:** https://orcid.org/0000-0002-1390-4776
  - **Affiliation:** Institute of Experimental and Applied Physics, University of Kiel
  - **Affiliation Identifier:** Not found
  - **Affiliation:** Paradox Cat GmbH
  - **Affiliation Identifier:** Not found

**Name split and identifier.** An earlier revision of this file gave the given name
"Johan L. Freiherr von", family "Forstner", with no identifier — a split that put the nobiliary particle
chain "Freiherr von" in the given name. ORCID `0000-0002-1390-4776`, the author's own self-curated
record, gives `given-names` = "Johan Lauritz" and `family-name` = "Freiherr von Forstner", and its
**current** employment is "Paradox Cat, Machine Learning Engineer" — the very affiliation this entry
already stored, which is what identifies the two HSSI rows as one person rather than a name coincidence.
Both affiliations are retained: this author's record carries the union of the institutions any source
attributes to him, and an affiliation is never dropped in favour of a newer one.
- **Author:** Christian Palmroos
  - **Author Identifier:** https://orcid.org/0000-0002-7778-5454
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Author:** Seve Nyberg
  - **Author Identifier:** https://orcid.org/0000-0003-2672-5491
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Author:** Rami Vainio
  - **Author Identifier:** https://orcid.org/0000-0002-3298-2067
  - **Affiliation:** University of Turku
  - **Affiliation Identifier:** https://ror.org/05vghhr25
- **Source:** Identity-aware union of the existing HSSI authors with the API-representable current software authors in `CITATION.cff`, `.zenodo.json`, and the Zenodo v0.5.3 record. The University of Turku ROR was confirmed through the live HSSI organization record and the ROR API. The public ORCID record confirms that https://orcid.org/0000-0003-2672-5491 belongs to Seve Nyberg. No ROR match was found for Paradox Cat GmbH. The one-token username-style release creator `drazerd` is authoritative source credit but is not emitted as an HSSI author because the schema requires non-empty given and family names and no non-invented split is available.

### 7. Software Name (MANDATORY)
- **Software Name:** solarmach
- **Source:** Preserved from the existing HSSI record and confirmed by the repository, PyPI, Zenodo, and PyHC registry.

### 8. Description (MANDATORY)
- **Description:** solarmach is the Python package for Solar-MACH, a multi-spacecraft heliospheric configuration and magnetic-connectivity tool. It obtains spacecraft ephemerides from JPL Horizons, can retrieve measured solar-wind speeds for selected missions through Speasy, computes Parker-spiral backmapping in Carrington or Stonyhurst coordinates, and produces tabular, 2D polar, interactive 3D, and optional PFSS field-line results driven by GONG maps. When a measured solar-wind speed cannot be obtained, it uses a configurable default value.
- **Source:** Materially expanded from the short existing HSSI description using the README, public API docstrings, source code, and example notebook. The submitted wording and identity as the Solar-MACH Python package are preserved.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Python package of the multi-spacecraft longitudinal configuration plotter Solar-MACH
- **Source:** Preserved verbatim from the existing HSSI record and confirmed by the current Zenodo record.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2022-03-14
- **Source:** GitHub API repository creation date. This replaces the existing HSSI value `2025-01-29`, which is the v0.5.0 release date rather than the software's initial publication; the first PyPI release followed on 2022-03-17.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** Preserved from the existing HSSI record and confirmed by the concept and version DOI metadata.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.5.3
- **Version Date:** 2026-03-27
- **Version Description:** Fixes GONG-map path selection in PFSS analysis, PFSS plotting and reference-coordinate edge cases, and PFSS table value typing; adds SOLAR-1 to the supported-spacecraft list; and refactors the GitHub Actions setup.
- **Version PID:** https://doi.org/10.5281/zenodo.19257728
- **Source:** Current GitHub release, PyPI 0.5.3 release files, Zenodo record 19257728, DataCite, and `CITATION.cff`. These authoritative current sources replace the stale existing HSSI version `solarmach - v0.5.0`. The DOI written in the current `CITATION.cff` (`10.5281/zenodo.16882017`) resolves to v0.5.1, so the latest Zenodo version DOI is used here instead.

### 13. Programming Language (RECOMMENDED)
- **Values:**
  - Python 3.x
- **Source:** Preserved from the existing HSSI record and confirmed by `pyproject.toml`, PyPI classifiers, and GitHub language metadata. The current project requires Python 3.11 or newer.

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication:** https://doi.org/10.3389/fspas.2022.1058810
- **Source:** Preferred citation in `CITATION.cff`, README, and documentation.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://opensource.org/licenses/BSD-3-Clause
- **Source:** `pyproject.toml`, `LICENSE.rst`, Zenodo, and DataCite. SoMEF's file-text classifier suggested BSD-2-Clause, but the repository declares `BSD-3-Clause` and the license text includes the third non-endorsement clause, so BSD-3-Clause is authoritative.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Values:**
  - ESA
  - coordinates
  - GONG
  - heliophysics
  - heliosphere
  - magnetic connectivity
  - multi-spacecraft
  - Parker spiral
  - PFSS
  - solar
  - solar wind
  - space physics
  - space weather
- **Source:** Identity-aware union of the existing HSSI keywords with current GitHub topics, PyHC community-registry keywords, README terminology, and public API concepts. Existing `Esa` is normalized to the authoritative acronym `ESA`.

### 17. Data Sources (OPTIONAL)
- **Values:**
  - CDAWeb
  - AMDA
  - Observatory/Mission-specific
  - Other
- **Other Data Sources:** AMDA through Speasy, JPL Horizons, and GONG synoptic-map access through SunPy Fido.
- **Source:** `get_sw_speed`, `SolarMACH.__init__`, and `get_gong_map` in the source. `solarmach/__init__.py:133` binds the Speasy AMDA inventory, lines 138-142 select AMDA parameter paths for multiple missions, and line 169 dispatches those datasets to `spz.get_data`, so AMDA is a direct data backend. Observatory/Mission-specific is selected because the package directly retrieves named mission/instrument data products; those relationships are resolved in Fields 31–32. Other remains supported by JPL Horizons and GONG access through SunPy Fido.

### 18. Input File Formats (RECOMMENDED)
- **Values:**
  - FITS
  - Other
- **Other Input File Formats:** Python pickle files containing cached PFSS solutions.
- **Source:** `pfss_utilities.py` loads GONG/HMI FITS maps and can load cached pickled PFSS outputs.

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - Other
- **Other Output File Formats:** PNG, PDF, HTML, animated GIF, and Python pickle.
- **Source:** Plot methods, PFSS cache code, and the documented example notebook. DataFrames and Plotly figure objects are also returned in memory but are not claimed as file formats.

### 20. Operating System (RECOMMENDED)
- **Values:**
  - Operating System Independent
- **Source:** Exact live HSSI controlled value, normalized from the `Operating System :: OS Independent` classifier in `pyproject.toml` and PyPI.

### 21. CPU Architecture (RECOMMENDED)
- **Values:**
  - CPU Independent
- **Source:** The current PyPI release publishes a `py3-none-any` wheel and the repository contains no architecture-specific compiled code.

### 22. Related Phenomena (OPTIONAL)
- **Values:**
  - Solar Corona
  - Solar Wind
- **Source:** Solar Corona and Solar Wind are exact live HSSI controlled values supported by the package's PFSS and solar-wind functionality. Interplanetary Magnetic Field and Parker Spiral are scientifically supported by the directly implemented and documented backmapping, but are omitted because they are absent from the live Phenomena vocabulary.

### 23. Development Status (RECOMMENDED)
- **Development Status:** Active
- **Source:** Repository status badge explicitly declares Active; the repository has a 2026 release and current 2026 development activity.

### 24. Documentation (RECOMMENDED)
- **Documentation:** https://solarmach.readthedocs.io
- **Source:** Preserved from the existing HSSI record and confirmed by the README, documentation configuration, and PyHC registry.

### 25. Funder (OPTIONAL)
- **Organization:** European Commission
- **Funder Identifier:** https://ror.org/00k4n6c32
- **Source:** Preserved from the existing HSSI record and confirmed by the live HSSI organization record, Zenodo/DataCite funding metadata, README acknowledgements, and CORDIS project records. The repository says "European Union"; the existing HSSI/Zenodo identity `European Commission` is retained as the funding organization.

### 26. Award Title (OPTIONAL)
- **Award Title:** Solar EneRgetic ParticlE aNalysis plaTform for the INner hEliosphere (SERPENTINE)
  - **Award Number:** 101004159
- **Award Title:** The Energetic Solar Eruptions: Data and Analysis Tools (SOLER)
  - **Award Number:** 101134999
- **Source:** The existing HSSI award and Zenodo/DataCite metadata provide SERPENTINE; the README adds both grant numbers, and the European Commission CORDIS record supports SOLER. The SOLER label is reconciled to the existing shared HSSI Award record matched by identifier `101134999`.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Value:** Not found
- **Source:** The repository prioritizes the Solar-MACH paper already recorded in Field 14; it is not duplicated here.

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found
- **Source:** The source names dynamic CDAWeb/AMDA instrument variables, JPL Horizons ephemerides, and GONG maps, but the repository does not curate a dataset DOI or a preferred permanent dataset citation. Their data services and controlled instrument/observatory relationships are recorded in Fields 17 and 31–32.

### 29. Related Software (OPTIONAL)
- **Values:**
  - https://github.com/jgieseler/Solar-MACH
  - https://github.com/dstansby/pfsspy
- **Source:** The README identifies the first as the corresponding Streamlit web application. GitHub release v0.4.0 documents `pfsspy` as the former PFSS backend replaced by `sunkit-magex`, making it a distinguishing predecessor rather than a generic dependency.
- **Note:** Generic scientific-Python and tooling dependencies were considered and omitted under the HSSI relevance gate; dependency presence alone does not make them related software.

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - https://github.com/sunpy/sunpy
  - https://github.com/sunpy/sunkit-magex
  - https://github.com/SciQLop/speasy
  - https://github.com/astropy/astropy
- **Source:** Specific repository evidence demonstrates exchange rather than mere co-installation: public APIs consume and return SunPy coordinate/Map objects and use SunPy Fido; PFSS methods exchange `sunkit-magex` PFSS input/output and field-line objects; `get_sw_speed` consumes Speasy data containers and converts their measurements to DataFrames; and public backmapping/coordinate APIs accept and return Astropy `SkyCoord` and `Quantity` objects.
- **Note:** NumPy, SciPy, pandas, Matplotlib, Plotly, imageio, CMasher, orjson, Jinja2, lxml, parfive, threadpoolctl, tqdm, zeep, and packaging/testing dependencies were considered and omitted because they are generic infrastructure, not high-level demonstrated heliophysics interoperability. Pandas is omitted even though a DataFrame is exposed because it is a Tier-A generic dependency under the HSSI policy.

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** ACE Solar Wind Electron, Proton and Alpha Monitor
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ACE/SWEPAM
- **Instrument Name:** Charge, Element, and Isotope Analysis System
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SOHO/CELIAS
- **Instrument Name:** PSP SWEAP
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/SWEAP/SPC
- **Instrument Name:** Proton-Alpha Sensor
  - **Instrument Identifier:** https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/PAS
- **Instrument Name:** Plasma and Supra-Thermal Ion Composition
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-A/PLASTIC
- **Instrument Name:** Plasma and Supra-Thermal Ion Composition
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-B/PLASTIC
- **Instrument Name:** Wind Solar Wind Experiment
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/Wind/SWE
- **Instrument Name:** HMI
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/HMI
- **Source:** Exact mission/instrument paths in `get_sw_speed` select ACE/SWEPAM, SOHO/CELIAS Proton Monitor, PSP/SWEAP-SPC, Solar Orbiter/SWA-PAS, STEREO-A and STEREO-B/PLASTIC, and Wind/SWE. The `get_pfss_hmimap` implementation directly supports SDO/HMI magnetograms. Duplicate CNES/SMWG representations were normalized to the preferred non-`.html` SMWG rows except where the exact AMDA inventory path selects the CNES Solar Orbiter/PAS row.
- **Note:** No GONG station-level instrument is emitted. The generic `attrs.Instrument("GONG")` query provides no evidence selecting any station among the six station-specific SPASE rows; the uniquely resolved Global Oscillation Network Group observatory remains recorded in Field 32.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Advanced Composition Explorer
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ACE
- **Observatory Name:** BepiColombo Spacecraft
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/BepiColombo
- **Observatory Name:** Mercury Planetary Orbiter
  - **Observatory Identifier:** https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/BepiColombo/MPO
- **Observatory Name:** Cassini Orbiter
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Cassini
- **Observatory Name:** JUpiter ICy moons Explorer
  - **Observatory Identifier:** https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/Juice
- **Observatory Name:** Juno Orbiter
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Juno
- **Observatory Name:** Mars Express
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MarsExpress
- **Observatory Name:** Mars Atmosphere and Volatile EvolutioN
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MAVEN
- **Observatory Name:** Mercury Surface, Space Environment, Geochemistry and Ranging
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MESSENGER
- **Observatory Name:** Parker Solar Probe
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe
- **Observatory Name:** 1972-012A
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Pioneer10
- **Observatory Name:** 1973-019A
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Pioneer11
- **Observatory Name:** Rosetta Comet Rendezvous
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Rosetta
- **Observatory Name:** Solar and Heliospheric Observatory
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SOHO
- **Observatory Name:** Solar Orbiter
  - **Observatory Identifier:** https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SolO
- **Observatory Name:** Solar Terrestrial Relations Observatory A
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-A
- **Observatory Name:** Solar Terrestrial Relations Observatory B
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-B
- **Observatory Name:** International Solar Polar Mission
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Ulysses
- **Observatory Name:** Mariner Jupiter/Saturn A
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Voyager1
- **Observatory Name:** Mariner Jupiter/Saturn B
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Voyager2
- **Observatory Name:** ISTP/Wind
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Wind
- **Observatory Name:** Global Oscillation Network Group
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/GONG
- **Observatory Name:** Solar Dynamics Observatory
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SDO
- **Source:** The repository's concrete `body_dict` supported-spacecraft list, mission-specific solar-wind dataset paths, GONG map retrieval, and HMI helper. The matched controlled-list row names are copied verbatim. SMWG rows are preferred over duplicate provider-specific representations except where an evidenced resource has only a CNES row or the exact AMDA `SolarOrbiter.SWAPAS` path selects the CNES Solar Orbiter row. Both BepiColombo and its explicitly aliased MPO spacecraft are included because the repository evidence names both.
- **Note:** Europa Clipper, Psyche, and SOLAR-1/SWFO-L1 are explicitly supported by the source but have no defensible observatory row in the live SPASE-backed vocabulary; they are omitted rather than emitted as identifierless names. Planets and Lagrange points are also omitted because they are bodies/locations rather than observatories.

### 33. Logo (OPTIONAL)
- **Logo:** Not found
- **Source:** No durable software-logo URL was found in the existing HSSI record, current repository metadata, PyHC registry, or SoMEF output. The repository's `examples/solarmach.png` is a generated example plot, not a software logo.
