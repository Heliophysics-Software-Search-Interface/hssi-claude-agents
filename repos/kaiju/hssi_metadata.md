# HSSI Metadata Extraction Results

**Repository:** https://github.com/JHUAPL/kaiju
**Extraction Date:** 2026-06-01

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.16818620

*Source: CITATION.cff (Zenodo concept DOI). Confirmed via DataCite/Zenodo APIs — title "MAGE: Multiscale Atmosphere Geospace Environment Model", publisher Zenodo, resource type Software, IsSupplementTo https://github.com/JHUAPL/kaiju/tree/MAGE_1.25.1. Versioned DOIs also exist (e.g., 10.5281/zenodo.16818621); this is the all-versions concept DOI.*

### 3. Code Repository (MANDATORY)
https://github.com/JHUAPL/kaiju

*Source: git remote origin and CITATION.cff repository-code.*

### 4. Software Functionality (MANDATORY)
- Models and Simulations
- Models and Simulations:First Principles
- Models and Simulations:MHD
- Models and Simulations:Physics-Based
- Models and Simulations:Data Guided
- Models and Simulations:Forecasting
- Models and Simulations:Empirical
- Coordinate Transforms
- Coordinate Transforms:Magnetospheric
- Coordinate Transforms:Heliospheric
- Coordinate Transforms:Ionospheric
- Data Processing and Analysis
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Processing
- Servers and Environments
- Servers and Environments:High Performance Computing
- Servers and Environments:Software or Environment Container

*Source: Manual examination of src/ (213 Fortran F90 files), CMakeLists.txt, docs/, and containers/. Kaiju is the C++/Fortran simulation code for the Multiscale Atmosphere-Geospace Environment (MAGE) model and GAMERA-helio. Core capabilities:*
- *GAMERA (src/gamera): a three-dimensional finite-volume MHD solver for non-orthogonal curvilinear geometries (Zhang et al. 2019) — Models and Simulations:MHD, First Principles, Physics-Based. Applied to global magnetosphere and the inner heliosphere/solar wind.*
- *RAIJU/RCM (src/raiju): full rewrite of the Rice Convection Model, an inner-magnetosphere ring-current/plasma model (physics-based bounce-averaged drift kinetics).*
- *REMIX (src/remix): ionospheric electrodynamics module (mixsolver, mixconductance) coupling magnetosphere to ionosphere; couples to TIEGCM ionosphere-thermosphere (empirical/physics-based ionosphere-thermosphere model — Models and Simulations:Empirical for the TIEGCM/EUV climatology components).*
- *Dragon King (src/dragonking): energetic precipitation model.*
- *CHIMP (src/chimp): test-particle pushing, field-line tracing, and ground/space magnetic-perturbation (dB) calculation — Data Processing and Analysis:Field-line Tracing, Processing, Analysis (drivers tracex, pushx, psdx, calcdbx).*
- *VOLTRON (src/voltron): the coupling framework (dyncoupling, modelInterfaces) that couples MHD, inner magnetosphere, and ionosphere — multi-model coupled simulation; boundary/initial conditions can be data-driven (earthcmi IC, GAMERA-helio driven by WSA coronal maps) — Models and Simulations:Data Guided, Forecasting (space-weather predictive use; available for runs at NASA CCMC).*
- *Coordinate transforms: the magnetosphere/ionosphere/heliosphere grids and couplers require transforms among GSM/SM/GEO/MAG (Magnetospheric), heliospheric/inner-heliosphere frames (Heliospheric), and magnetic-coordinate/MLT ionospheric grids in REMIX (Ionospheric).*
- *HPC: OpenMP (ENABLE_OMP default ON) and MPI (ENABLE_MPI, gamera_mpix/voltron_mpix/kaitoy_mpix drivers) parallelization; build guides for NASA Pleiades/Aitken and NCAR Derecho HPC systems — Servers and Environments:High Performance Computing. Docker/Singularity definitions (containers/Dockerfile, containers/gamera.def) — Software or Environment Container.*

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Atmosphere
- Interplanetary Space
- Solar Environment
- Planetary Magnetospheres

*Source: MAGE models the coupled geospace system — global magnetosphere (Earth Magnetosphere), the ionosphere-thermosphere via REMIX/TIEGCM (Earth Atmosphere), and is driven by the upstream solar wind. GAMERA-helio simulates the inner heliosphere / solar wind from the Sun to ~1 AU (Solar Environment, Interplanetary Space). README/docs state the software also simulates "planetary magnetospheres" (Planetary Magnetospheres).*

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

*Source: CITATION.cff (19 authors with ORCIDs and affiliations). ROR identifiers resolved via ROR v2 API: Johns Hopkins University Applied Physics Laboratory (029pp9z10), NSF National Center for Atmospheric Research (05cvfcr44), Rice University (008zs3103). "Gamera Consulting" has no ROR record found. Affiliation acronyms in source were already expanded full names; no acronym expansion needed.*

### 7. Software Name (MANDATORY)
Kaiju

*Source: README.md ("Project Kaiju"), repository name. The Kaiju software contains the MAGE (Multiscale Atmosphere-Geospace Environment) model and GAMERA-helio; the Zenodo/CITATION.cff title is "MAGE: Multiscale Atmosphere Geospace Environment Model". Kaiju is the encompassing software package/framework name; MAGE is its flagship application.*

### 8. Description (MANDATORY)
Kaiju is a space-physics modeling framework developed primarily at the Johns Hopkins University Applied Physics Laboratory by the Center for Geospace Storms (CGS), a NASA DRIVE Science Center, together with the NSF National Center for Atmospheric Research and Rice University. It contains the Multiscale Atmosphere-Geospace Environment (MAGE) model for the coupled geospace system and the GAMERA-helio application for the inner heliosphere and solar wind. The core numerical engine is GAMERA, a three-dimensional finite-volume magnetohydrodynamic (MHD) solver designed for non-orthogonal curvilinear geometries with high-order reconstruction and low numerical diffusion. MAGE couples GAMERA's global magnetosphere simulation with RAIJU (a modern full rewrite of the Rice Convection Model for the inner magnetosphere ring current and plasma), the REMIX ionospheric electrodynamics solver, the Dragon King energetic-precipitation model, and the TIEGCM ionosphere-thermosphere model, all orchestrated through the VOLTRON coupling framework. GAMERA-helio applies the same MHD core to time-dependent simulations of the inner heliosphere and coronal mass ejection propagation, driven by solar coronal magnetic field maps (e.g., WSA). The CHIMP toolset provides test-particle tracing, field-line tracing, and ground/space magnetic-perturbation (delta-B) calculations from the simulation output. Kaiju is written predominantly in modern Fortran (with C), parallelized with OpenMP and MPI for high-performance and supercomputing platforms (e.g., NASA Pleiades/Aitken, NCAR Derecho), reads and writes HDF5 data, and is distributed with Docker/Singularity container definitions. Previous MAGE versions (0.75, 1.0) and GAMERA-helio are also available for community runs through the NASA Community Coordinated Modeling Center (CCMC). The companion Python package kaipy is recommended for analysis and visualization of Kaiju output.

*Source: README.md, docs/source/index.rst, CMakeLists.txt, src/ module structure, containers/, and CGS/MAGE web pages.*

### 9. Concise Description (OPTIONAL)
A Fortran/C HPC space-physics modeling framework containing the MAGE coupled magnetosphere-ionosphere-thermosphere model and GAMERA-helio inner-heliosphere model, built on the GAMERA 3D finite-volume MHD solver.

### 10. Publication Date (RECOMMENDED)
2025-12-12

*Source: Zenodo/DataCite issued date for the concept DOI 10.5281/zenodo.16818620 (2025-12-12), the initial open-source public release. CITATION.cff date-released is 2025-12-01.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Source: DataCite/Zenodo metadata for DOI 10.5281/zenodo.16818620 (publisher: Zenodo).*

### 12. Version (RECOMMENDED)
- **Version Number:** 1.25.1
- **Version Date:** 2025-12-01
- **Version Description:** Initial open-source launch of the kaiju software. Introduces a "CONE" geometry type and improves thread-safety for OpenMP parallel processing. (MAGE version 1.25; master branch under active development.)
- **Version PID:** https://doi.org/10.5281/zenodo.17915213

*Source: CITATION.cff (version 1.25.1, date-released 2025-12-01), git tag MAGE_1.25.1, Zenodo record. The versioned DOI for MAGE_1.25.1 is 10.5281/zenodo.17915213 (DataCite confirms version "MAGE_1.25.1", issued 2025-12-12); the all-versions concept DOI (10.5281/zenodo.16818620) is recorded under Field 2.*

### 13. Programming Language (RECOMMENDED)
- Fortran90
- Fortran 2008

*Source: src/ contains 213 .F90 (free-form modern Fortran) source files; cmake/compilers.cmake requires MPI with `MPI_Fortran_HAVE_F08_MODULE` and references Fortran 2008 features, so both Fortran90 and Fortran 2008 apply. Note: `project(Kaiju Fortran C)` in CMakeLists.txt declares C only as a toolchain workaround for recent HDF5 ("Adding C to project to deal w/ issues w/ most recent HDF") — there are no `.c` source files in the repository, so C is not listed as a programming language. Build scripts use shell/csh; ancillary run-setup scripts use Python. The companion analysis package kaipy (separate repository) is Python.*

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.3847/1538-4365/ab3a4c

*Zhang, B., Sorathia, K.A., Lyon, J.G., Merkin, V.G., Garretson, J.S. and Wiltberger, M., 2019. GAMERA: A three-dimensional finite-volume MHD solver for non-orthogonal curvilinear geometries. The Astrophysical Journal Supplement Series, 244(1), p.20. This is the foundational paper for the GAMERA MHD core, the primary algorithm of the Kaiju/MAGE software, and the citation requested in README.md "How to cite this work". (Component/configuration-specific references — Sorathia et al. 2020/2023, Merkin & Lyon 2010, Pham et al. 2022, Provornikova et al. 2024, Merkin et al. 2016 — are listed under Related Publications.)*

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

*Source: LICENSE.md and CITATION.cff (BSD-3-Clause). Copyright held by Johns Hopkins University Applied Physics Laboratory, US NSF National Center for Atmospheric Research, John G. Lyon, and Rice University. Confirmed via DataCite rightsList (SPDX bsd-3-clause).*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- space weather
- MAGE
- geospace modeling
- magnetohydrodynamics
- MHD
- magnetosphere
- ionosphere
- thermosphere
- inner heliosphere
- solar wind
- GAMERA
- magnetosphere-ionosphere coupling
- ring current
- numerical simulation
- high performance computing
- geomagnetic storms
- substorms
- aurora

*Source: CITATION.cff/Zenodo keywords ("space weather", "MAGE", "geospace modeling") plus keywords derived from README/docs scientific content. Geomagnetic storms, substorms, and aurora were moved here from Field 22 Related Phenomena as they are not in that field's controlled vocabulary.*

### 17. Data Sources (OPTIONAL)
- Other
- Observatory/Mission-specific

*Source: MAGE/GAMERA are driven by solar wind / IMF upstream boundary conditions (observed near-Earth solar wind, e.g., OMNI) and GAMERA-helio is driven by solar coronal magnetic field model maps (WSA derived from synoptic magnetograms); the simulation itself produces model output. Inputs include both model-derived (WSA/coronal model) and observatory/mission-specific (solar wind monitor) data.*

### 18. Input File Formats (RECOMMENDED)
- HDF5
- netCDF3/4
- ascii
- Other

*Source: HDF5 is the primary grid/state I/O format (cmake/compilers.cmake requires HDF5 Fortran/Fortran_HL; src/gamera/gioH5.F90, src/remix/mixio.F90). TIEGCM coupling uses netCDF (netCDF3/4). Some inputs/run setup use plain-text/ascii (.txt). Configuration/run-definition inputs use XML and JSON, captured as "Other" (neither is in the standard allowed list). Note: CDF was removed as a direct Kaiju input format — a search of all 213 .F90 source files found no CDF library calls; CDF time-series solar-wind input is handled upstream by the kaipy `cda2wind` preprocessor (a separate package), with the Fortran code reading the resulting HDF5.*

### 19. Output File Formats (RECOMMENDED)
- HDF5

*Source: Simulation state and results are written to HDF5 (gioH5.F90, mixio.F90, voltio.F90, chmpio.F90); compiler/git-hash provenance is embedded in H5 files. CDF was removed as a Kaiju output format — no CDF library calls exist in the 213 .F90 source files; CDF time-series products (e.g., dB/CHIMP) are generated downstream by the kaipy Python package (separate), not by the Fortran simulation.*

### 20. Operating System (RECOMMENDED)
- Linux
- Mac

*Source: Build guides (docs/source/building, docs/source/misc/build_guides) cover Ubuntu 20.04, CentOS Stream 9, macOS, and HPC systems (NASA Pleiades/Aitken, NCAR Derecho); .readthedocs.yaml uses ubuntu-22.04; containers/Dockerfile uses Intel oneAPI on Ubuntu 22.04. Targets Unix-like HPC environments; no Windows build documented.*

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64
- HPC or HEC

*Source: Container/build environments target x86-64 (Intel oneAPI HPC toolkit, x86-64 HPC clusters; git-lfs amd64 in .readthedocs.yaml). Apple Silicon arm64 is explicitly handled in cmake/compilers.cmake (`if (CMAKE_HOST_SYSTEM_PROCESSOR MATCHES arm64)` "#Apple silicon"). HPC or HEC applies given build guides for NASA Pleiades/Aitken and NCAR Derecho HPC systems. Compiler support includes Intel and GNU Fortran.*

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections

*Source: GAMERA-helio models CME propagation in the inner heliosphere — Coronal Mass Ejections is the only term in the HSSI controlled vocabulary that applies. Other phenomena central to MAGE (Geomagnetic Storms, Substorms, Aurora) are not in the controlled vocabulary and have been moved to Field 16 Keywords; Ring Current and Solar Wind were already in Keywords.*

### 23. Development Status (RECOMMENDED)
Active

*Source: README states the master branch (v1.25) is "bleeding-edge code that is under active development"; most recent commit 2025-12-12, tag MAGE_1.25.1, with team noting forthcoming publications for RAIJU, Dragon King, and MAGE 1.25.*

### 24. Documentation (RECOMMENDED)
https://kaiju-docs.readthedocs.io/en/latest/

*Source: README.md and .readthedocs.yaml (Sphinx docs at docs/source/conf.py).*

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
  - **Funder Identifier:** https://ror.org/027ka1x80

*Source: The software is developed by the Center for Geospace Storms (CGS), a NASA DRIVE Science Center funded by the National Aeronautics and Space Administration (NASA began funding CGS in April 2020; Phase II extension granted). Per CGS/JHUAPL and NASA Heliophysics DRIVE Science Center pages. No specific award number is stated in the repository. ROR for NASA: 027ka1x80.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Center for Geospace Storms (DRIVE Science Center)
  - **Award Number:** Not found

*Source: CGS is a NASA DRIVE (Diversity, Realize, Integrate, Venture, Educate) Science Center. The specific grant/award number is not stated in the repository, CITATION.cff, or LICENSE; submitter should add the NASA cooperative-agreement number if known.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2020GL088227 *(Sorathia et al. 2020 — GAMERA global magnetosphere; ballooning-interchange instability and auroral beads)*
- https://doi.org/10.1029/2010JA015461 *(Merkin & Lyon 2010 — REMIX low-latitude ionospheric boundary condition)*
- https://doi.org/10.1002/9781118704417.ch7 *(Qian et al. 2014 — NCAR TIE-GCM)*
- https://doi.org/10.1029/2023JA031594 *(Sorathia et al. 2023 — MAGE 0.75 multiscale magnetosphere-ionosphere coupling)*
- https://doi.org/10.1029/2021JA030071 *(Pham et al. 2022 — MAGE 1.0 thermospheric density perturbations)*
- https://doi.org/10.3847/1538-4357/ad83b1 *(Provornikova et al. 2024 — GAMERA-helio MHD modeling of a geoeffective ICME)*
- https://doi.org/10.1002/2015JA022200 *(Merkin et al. 2016 — GAMERA-helio time-dependent inner-heliosphere MHD simulations)*

*Source: README.md "How to cite this work" — component- and configuration-specific references for the Kaiju/MAGE software.*

### 28. Related Datasets (OPTIONAL)
Not found

*Source: No dataset DOIs are published in the repository. (MAGE/GAMERA-helio runs are also available on request via the NASA CCMC, but no specific dataset PID is provided.)*

### 29. Related Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.17914543 *(kaipy — companion Python package for analysis and visualization of Kaiju simulation output; recommended in README)*

*Source: README.md "Analysis" section and src/voltron/modelInterfaces (TIEGCM coupling). kaipy is in the PyHC community registry.*

### 30. Interoperable Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.17914543 *(kaipy reads and post-processes Kaiju HDF5/CDF output)*
- https://www.hao.ucar.edu/modeling/tgcm/tie.php

*Source: README.md and src/remix/tgcm.F90, src/voltron/modelInterfaces. MAGE 1.0+ provides two-way coupling with TIEGCM (NCAR Thermosphere-Ionosphere-Electrodynamics General Circulation Model), coupled within MAGE via the VOLTRON framework; kaipy interoperates with Kaiju output files.*

### 31. Related Instruments (OPTIONAL)
Not found

*Source: No specific instrument is associated with the model in the repository.*

### 32. Related Observatories (OPTIONAL)
Not found

*Source: No specific observatory is asserted in the software. (GAMERA-helio coronal boundary maps are typically derived from ground-based synoptic magnetograms, e.g., GONG/ADAPT, but no specific observatory is named as a software dependency.)*

### 33. Logo (OPTIONAL)
Not found

*Source: No logo image file identified in the repository root or docs/_static. (containers/screenshot.png is a documentation screenshot, not a logo.)*
