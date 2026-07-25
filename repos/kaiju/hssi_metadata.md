# HSSI Metadata Extraction Results

**HSSI Software ID:** aebd4757-08dc-4ca0-be33-aa85171de59d
**Repository:** https://github.com/JHUAPL/kaiju
**Source Revision:** 9e19bfc61a63206e7e74340b5dbf0b7537afa8a7
**Extraction Date:** 2026-07-24
**Validation Date:** 2026-07-24
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.16818620

*Source: Seeded from existing HSSI record and confirmed by CITATION.cff line 6, DataCite concept DOI metadata, and Zenodo concept record. This is the all-versions concept DOI; the latest version DOI is recorded in Field 12.*

### 3. Code Repository (MANDATORY)
https://github.com/JHUAPL/kaiju

*Source: Seeded from existing HSSI record and confirmed by git remote origin, CITATION.cff line 7, and docs/source/building/index.rst lines 27-32.*

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms:Heliospheric
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:3D Particle Distribution Processing
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Plasma Moments
- Data Processing and Analysis:Processing
- Models and Simulations
- Models and Simulations:Data Guided
- Models and Simulations:Empirical
- Models and Simulations:First Principles
- Models and Simulations:Forecasting
- Models and Simulations:MHD
- Models and Simulations:Physics-Based
- Servers and Environments
- Servers and Environments:High Performance Computing
- Servers and Environments:Software or Environment Container

*Source: Seeded HSSI record had only Models and Simulations; repository evidence supports a fuller set. README.md lines 5-25 identify MAGE, GAMERA-helio, GAMERA, RAIJU, Dragon King, REMIX, and TIEGCM. CMakeLists.txt lines 122-274 builds CHIMP, GAMERA, Dragon King, REMIX, RAIJU, VOLTRON, GAMERA-helio, and MPI variants. Coordinate transforms are supported by src/base/kai2geo.F90 and src/base/defs/mixdefs.F90 for SM/GEO/GSM/APEX transforms and by src/chimp/gridloc.F90 for LFM and heliospheric spherical coordinates. Data access/retrieval and file conversion are supported by docs/source/running/geoGRQuickStart.rst lines 76-107 and scripts/makeitso/makeitso.py lines 848-855 for CDAWeb solar-wind retrieval and HDF5 conversion; docs/source/running/helioQuickStart.rst lines 54-87 and scripts/makeitso-gamhelio/makeitso-gamhelio.py lines 227-256 support WSA FITS input. Field-line tracing and analysis tools are built in CMakeLists.txt lines 130-143 and documented in docs/source/tools. 2D slice extraction is documented in docs/source/tools/slice.rst, and particle distribution/PSD processing is implemented in src/chimp/psdio.F90. RAIJU moments and precipitation outputs are in src/raiju/raijuIO.F90. Container and HPC support are documented in docs/source/building/index.rst lines 17-48 and containers/containerization.md lines 95-168, 220-228. Standalone visualization, mission-operations support, and observatory/instrument model categories were considered but not selected because visualization is delegated to companion Kaipy/quicklook workflows, CCMC/HPC packaging does not make the software mission-specific, and WSA/TIEGCM coupling does not establish instrument or observatory model support.*

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space
- Planetary Magnetospheres
- Solar Environment

*Source: Seeded from existing HSSI record and enriched with Interplanetary Space. README.md lines 5-25 and docs/source/index.rst lines 4-11 describe geospace, inner heliosphere, planetary magnetospheres, solar wind, ionosphere, and thermosphere support.*

### 6. Authors (MANDATORY)
- **Author:** Slava Merkin
  - **Author Identifier:** https://orcid.org/0000-0003-4344-5424
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Harry Arnold
  - **Author Identifier:** https://orcid.org/0000-0002-0449-1498
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Shanshan Bao
  - **Author Identifier:** https://orcid.org/0000-0002-5209-3988
  - **Affiliation:**
    - **Organization:** Rice University
      - **Affiliation Identifier:** https://ror.org/008zs3103
- **Author:** Jeffery Garretson
  - **Author Identifier:** https://orcid.org/0000-0003-3805-9860
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Dong Lin
  - **Author Identifier:** https://orcid.org/0000-0003-2894-6677
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
- **Author:** John Lyon
  - **Author Identifier:** https://orcid.org/0000-0002-5759-9849
  - **Affiliation:**
    - **Organization:** Gamera Consulting
- **Author:** Andrew McCubbin
  - **Author Identifier:** https://orcid.org/0000-0002-6222-3627
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Adam Michael
  - **Author Identifier:** https://orcid.org/0000-0003-2227-1242
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Kevin Pham
  - **Author Identifier:** https://orcid.org/0000-0001-5031-5519
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
- **Author:** Elena Provornikova
  - **Author Identifier:** https://orcid.org/0000-0001-8875-7478
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Nikhil Rao
  - **Author Identifier:** https://orcid.org/0000-0003-2639-9892
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
- **Author:** Anthony Sciola
  - **Author Identifier:** https://orcid.org/0000-0002-9752-9618
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Kareem Sorathia
  - **Author Identifier:** https://orcid.org/0000-0002-6011-5470
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Frank Toffoletto
  - **Author Identifier:** https://orcid.org/0000-0001-7789-2615
  - **Affiliation:**
    - **Organization:** Rice University
      - **Affiliation Identifier:** https://ror.org/008zs3103
- **Author:** Aleksandr Ukhorskiy
  - **Author Identifier:** https://orcid.org/0000-0002-3326-4024
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Wenbin Wang
  - **Author Identifier:** https://orcid.org/0000-0002-6287-4542
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
- **Author:** Michael Wiltberger
  - **Author Identifier:** https://orcid.org/0000-0002-4844-3148
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44
- **Author:** Eric Winter
  - **Author Identifier:** https://orcid.org/0000-0001-5226-2107
  - **Affiliation:**
    - **Organization:** Johns Hopkins University Applied Physics Laboratory
      - **Affiliation Identifier:** https://ror.org/029pp9z10
- **Author:** Haonan Wu
  - **Author Identifier:** https://orcid.org/0000-0002-3272-8106
  - **Affiliation:**
    - **Organization:** NSF National Center for Atmospheric Research
      - **Affiliation Identifier:** https://ror.org/05cvfcr44

*Source: Live HSSI record contained only three incomplete author entries. Replaced with the complete DOI/CITATION.cff creator set from CITATION.cff lines 10-86 and DataCite/Zenodo metadata. The CITATION.cff/Zenodo spelling "Haonon Wu" conflicts with the ORCID public record for https://orcid.org/0000-0002-3272-8106, which gives "Haonan Wu"; the ORCID-backed spelling is used. ROR identifiers resolved through the ROR API for JHU/APL, NSF NCAR, and Rice University. No ROR found for Gamera Consulting.*

### 7. Software Name (MANDATORY)
Kaiju

*Source: Seeded from existing HSSI record and confirmed by README.md line 1 and repository name. CITATION.cff line 3 titles the DOI record as MAGE because MAGE is a primary application within Kaiju.*

### 8. Description (MANDATORY)
Kaiju software includes the Multiscale Atmosphere-Geospace Environment (MAGE) model developed by the Center for Geospace Storms (CGS) as well as other scientific software for simulation of heliospheric environments such as planetary magnetospheres and the solar wind. Currently supported applications include MAGE (version 1.25) and GAMERA-helio, the geospace and inner heliosphere applications of the Kaiju software. MAGE 1.25 includes the GAMERA global magnetosphere model, RAIJU inner-magnetosphere model, Dragon King energetic-precipitation model, REMIX ionospheric electrodynamics module, and TIEGCM ionosphere-thermosphere coupling. Kaiju also includes CHIMP analysis tools for field-line tracing, test-particle calculations, slices, and ground/space magnetic perturbation calculations. The software is primarily modern Fortran with Python run-preparation tooling, uses HDF5 and related input conversion workflows, and is built for serial and MPI/OpenMP high-performance computing runs. Users are encouraged to use the companion Kaipy package for analysis and visualization of Kaiju simulations.

*Source: Seeded HSSI description, streamlined without changing factual scope; confirmed by README.md lines 5-53, CMakeLists.txt lines 122-274, docs/source/building/index.rst lines 17-48, and docs/source/running/geoGRQuickStart.rst lines 76-131.*

### 9. Concise Description (OPTIONAL)
HPC space-physics modeling framework for MAGE coupled geospace simulations and GAMERA-helio inner-heliosphere simulations, built around the GAMERA MHD solver.

*Source: Derived from README.md lines 5-25 and docs/source/index.rst lines 4-11.*

### 10. Publication Date (RECOMMENDED)
2025-12-12

*Source: DataCite issued date and Zenodo publication date for DOI 10.5281/zenodo.16818620 / 10.5281/zenodo.17915213. This supersedes the older HSSI value 2025-06-16.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Source: DataCite/Zenodo metadata for DOI 10.5281/zenodo.16818620.*

### 12. Version (RECOMMENDED)
- **Version Number:** MAGE_1.25.1
- **Version Date:** 2025-12-12
- **Version Description:** First official open-source release of the Kaiju software; adds CONE geometry type and improves OpenMP thread-safety.
- **Version PID:** https://doi.org/10.5281/zenodo.17915213

*Source: git tag MAGE_1.25.1 at revision 9e19bfc61a63206e7e74340b5dbf0b7537afa8a7, DataCite version field "MAGE_1.25.1", Zenodo record 17915213, and CITATION.cff lines 4-6. The release date uses the Zenodo/DataCite publication date; CITATION.cff date-released is 2025-12-01.*

### 13. Programming Language (RECOMMENDED)
- Fortran90
- Fortran 2008
- Python 3.x
- Other

*Source: GitHub/SoMEF language scan and local extension counts show 215 .F90 files and 27 Python files. CMakeLists.txt line 2 declares Fortran and C, but line 3 states C was added for HDF5 build issues rather than code content, and no .c source files were found. Fortran 2008 is supported by the MPI F08 requirement in cmake/compilers.cmake lines 18-37. Python 3.x is used for run-preparation scripts and documentation tooling; Other covers shell, CMake, Dockerfile, and PBS/job templates.*

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.3847/1538-4365/ab3a4c

*Source: README.md lines 76-80 asks users to cite the GAMERA MHD algorithm paper, the foundational solver for Kaiju/MAGE/GAMERA-helio.*

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

*Source: Seeded from existing HSSI record and confirmed by README.md lines 136-139, CITATION.cff line 8, GitHub/SoMEF license metadata, and LICENSE.md lines 6-19.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- space weather
- MAGE
- geospace modeling
- Kaiju
- GAMERA
- GAMERA-helio
- magnetohydrodynamics
- MHD
- magnetosphere
- ionosphere
- thermosphere
- heliosphere
- solar wind
- planetary magnetospheres
- RAIJU
- REMIX
- TIEGCM
- Dragon King
- CHIMP
- field-line tracing
- high performance computing
- CDAWeb
- HDF5
- WSA
- coronal mass ejections

*Source: DataCite/CITATION.cff keywords plus README.md lines 5-25, 33-53, 67-133; docs/source/running/geoGRQuickStart.rst lines 76-131; docs/source/running/helioQuickStart.rst lines 54-94.*

### 17. Data Sources (OPTIONAL)
- CDAWeb
- Other

*Source: docs/source/running/geoGRQuickStart.rst lines 76-107 and scripts/makeitso/makeitso.py lines 848-855 fetch solar-wind/f10.7 data through CDAWeb. GAMERA-helio uses WSA FITS boundary-condition files (docs/source/running/helioQuickStart.rst lines 54-87), represented as Other/model-derived source data. Observatory/Mission-specific was considered but not selected because the repository does not establish one specific mission or observatory as a supported target.*

### 18. Input File Formats (RECOMMENDED)
- ascii
- CDF
- FITS
- HDF5
- JSON
- netCDF3/4
- Other

*Source: docs/source/running/geoGRQuickStart.rst lines 51-78 and 96-107 require CDF support for CDAWeb-derived solar-wind retrieval and produce HDF5 boundary files; docs/source/running/helioQuickStart.rst lines 54-94 uses WSA FITS input and produces HDF5/XML/JSON run files. scripts/makeitso/makeitso.py and scripts/makeitso-gamhelio/makeitso-gamhelio.py read/write JSON and convert INI to XML. TIEGCM coupling requires netCDF data/modules per docs/source/building/buildAitken_GTR.rst lines 28 and 149-152. Plain text/ascii is used for config/tables and generated OMNI text inputs; Other covers XML/INI/PBS run-control files.*

### 19. Output File Formats (RECOMMENDED)
- ascii
- HDF5
- JSON
- Other

*Source: src/base/ioH5.F90 and module-specific IO files write HDF5 outputs; docs/source/running/geoGRQuickStart.rst lines 121-155 and docs/source/running/helioQuickStart.rst lines 89-115 list generated HDF5, JSON, XML, PBS, PNG, and log files. JSON is included for run-option records. Other covers XML/PBS/log products; PNG quicklook plots are not an allowed HSSI format value.*

### 20. Operating System (RECOMMENDED)
- Linux
- Mac

*Source: docs/source/building/index.rst lines 8-48 emphasizes supercomputer/Linux builds and serial single-machine builds; .readthedocs.yaml lines 3-20 uses Ubuntu; cmake/compilers.cmake lines 165-167 explicitly handles Apple Silicon/macOS. No Windows build is documented.*

### 21. CPU Architecture (RECOMMENDED)
- Apple Silicon arm64
- HPC or HEC
- x86-64

*Source: docs/source/building/index.rst lines 8-21 and build guides document Aitken/Derecho HPC systems; containers/Dockerfile and containers/gamera.def use Intel oneAPI/x86-64 HPC stacks; .readthedocs.yaml lines 8-13 downloads linux-amd64 git-lfs; cmake/compilers.cmake lines 165-167 handles Apple Silicon arm64.*

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections

*Source: README.md lines 122-133 and GAMERA-helio documentation discuss CME modeling. Other central phenomena such as geomagnetic storms, substorms, aurora, ring current, and solar wind are recorded as keywords because they are not in the current HSSI Related Phenomena controlled list.*

### 23. Development Status (RECOMMENDED)
Active

*Source: README.md lines 27-31 states the master branch is under active development; git HEAD and latest tag MAGE_1.25.1 are dated 2025-12-12; SoMEF/GitHub metadata reports repository update activity.*

### 24. Documentation (RECOMMENDED)
https://kaiju-docs.readthedocs.io/en/latest/

*Source: README.md lines 45-48 and docs/source/index.rst. URL returned HTTP 200 on 2026-07-24. This broad documentation landing page supersedes the narrower seeded HSSI rules-of-road URL.*

### 25. Funder (OPTIONAL)
Not found

*Source: No funder entries are present in DataCite/Zenodo metadata, CITATION.cff, README.md, or repository documentation. README.md identifies CGS and NASA CCMC availability, but does not state a specific funder for the software metadata record.*

### 26. Award Title (OPTIONAL)
Not found

*Source: No grant or award title/number is present in DataCite/Zenodo metadata, CITATION.cff, README.md, or repository documentation.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2020GL088227
- https://doi.org/10.1029/2010JA015461
- https://doi.org/10.1002/9781118704417.ch7
- https://doi.org/10.1029/2023JA031594
- https://doi.org/10.1029/2021JA030071
- https://doi.org/10.3847/1538-4357/ad83b1
- https://doi.org/10.1002/2015JA022200

*Source: README.md lines 82-133 lists component/configuration citation papers for GAMERA magnetosphere, REMIX, TIEGCM, MAGE 0.75, MAGE 1.0, and GAMERA-helio. The GAMERA MHD algorithm DOI is Field 14.*

### 28. Related Datasets (OPTIONAL)
Not found

*Source: No dataset DOI or persistent dataset identifier is present in CITATION.cff, DataCite/Zenodo metadata, README.md, or docs. CCMC run availability is a service/model-run access path, not a specific dataset PID.*

### 29. Related Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.15801040
- https://github.com/NCAR/tiegcm

*Source: README.md lines 52-53 and docs/source/python/index.rst lines 9-17 identify kaipy as the companion package for analysis, visualization, and run-preparation dependencies. docs/source/building/buildAitken_GTR.rst lines 115-180 and docs/source/building/buildDerecho_GTR.rst document TIEGCM source/build coupling.*

### 30. Interoperable Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.15801040
- https://github.com/NCAR/tiegcm

*Source: Kaipy is explicitly recommended for analysis and visualization of Kaiju simulations in README.md lines 50-53 and is required for run-preparation/data workflows in docs/source/python/index.rst lines 9-17; DataCite confirms the Kaipy concept DOI. TIEGCM interoperates through coupled GTR workflows and VOLTRON/REMIX interfaces, with build/run requirements documented in docs/source/building/buildAitken_GTR.rst lines 115-180 and code evidence in src/remix/tgcm.F90 / src/voltron/mpi/gcm_mpi.F90. Generic dependencies such as numpy, h5py, netCDF4, matplotlib, SpacePy, and astropy are intentionally excluded.*

### 31. Related Instruments (OPTIONAL)
Not found

*Source: The software is a model/run framework and preprocessing workflow, not a package designed to support a specific instrument's data. WSA FITS, CDAWeb/OMNI, TIEGCM, and GONG-like magnetogram sources were considered but do not establish a specific instrument-level support target under the HSSI relevance gate.*

### 32. Related Observatories (OPTIONAL)
Not found

*Source: The software supports geospace/heliosphere models and generic data-source workflows, but the repository does not show design support for one specific mission/observatory. OMNI and GONG vocabulary matches were considered; OMNI is a multi-source data product/source and GONG is only an upstream WSA magnetogram source, so neither is listed as a related observatory.*

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/JHUAPL/kaiju/master/docs/source/_static/MAGE_Logo_final_dark-bg_vertical.png

*Source: docs/source/conf.py lines 37-41 sets this image as the documentation logo; file exists at docs/source/_static/MAGE_Logo_final_dark-bg_vertical.png in the source repository.*
