# HSSI Metadata Extraction Results

**Repository:** https://github.com/lanl/RAM-SCB
**Extraction Date:** 2026-06-04

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.6977287
- Concept DOI (all versions). Source: README DOI badge + DataCite API.

### 3. Code Repository (MANDATORY)
https://github.com/lanl/RAM-SCB
- Source: git remote.

### 4. Software Functionality (MANDATORY)
- Models and Simulations
- Models and Simulations:First Principles
- Models and Simulations:Physics-Based
- Models and Simulations:Empirical
- Models and Simulations:MHD
- Models and Simulations:Field-line Tracing
- Models and Simulations:Forecasting
- Models and Simulations:Data Guided
- Coordinate Transforms
- Coordinate Transforms:Magnetospheric
- Coordinate Transforms:Ionospheric
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Pitch Angle Distributions
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Processing
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:3D Graphics
- Data Visualization:Movies
- Data Visualization:Line Plots
- Servers and Environments
- Servers and Environments:High Performance Computing
- Servers and Environments:Software or Environment Container

Justification (grounded in repository contents):
- First Principles / Physics-Based: RAM solves the bounce-averaged kinetic
  (Boltzmann) equation for the ring current distribution function for H+, He+,
  O+ ions (and optionally electrons); SCB solves the 3-D force balance
  J x B = grad.P from fundamental physics (src/ModRamRun.f90, ModScbRun.f90,
  ModScbEquation.f90, ModScbCompute.f90).
- Empirical: srcExternal contains empirical field models (Tsyganenko T89/T96/
  T02/TS04/TS07, IGRF/DGRF, Weimer w05/w2k, Geopack) and empirical neutral
  atmosphere / ionosphere models (MSIS, NRLMSISE-00, IRI); empirical
  plasmasphere models (Carpenter/Gallagher in ModRamPlasmasphere.f90).
- MHD: two-way coupling to the BATS-R-US global MHD code as the Inner
  Magnetosphere (IM) component of the SWMF (srcInterface/IM_wrapper.f90,
  ModRamCouple.f90, doc/Tex/RAM_SCB_swmf.tex).
- Field-line Tracing: SCB magnetic field configuration is built by tracing/
  integrating field lines through the 3-D domain; field-line tracing also used
  for coupling and visualization seed lines (Scripts/viz).
- Forecasting / Data Guided: documented as a research and operations tool for
  space-weather forecasting (README; Jordanova et al. 2023); driven by
  observational indices (Kp, F10.7, AE) and flux/field boundary conditions
  (ModRamIndices.f90, ModRamBoundary.f90; Real-of-Record RoR workflow,
  Dockerfile.RoR, launch_run.py).
- Coordinate Transforms (Magnetospheric/Ionospheric): SM/GSM/GEO handling and
  equator-to-ionosphere mapping for the self-consistent electric field /
  ionosphere module (ModRamSce.f90, geo2mag.f90 in srcGlow, Geopack-2008).
- Pitch Angle Distributions: distribution function is resolved in pitch angle;
  pitch-angle diffusion from wave-particle interactions (EMIC, chorus) in
  ModRamWPI.f90.
- Data Visualization (2D/3D/Movies): Scripts/viz generates VTK files and
  ParaView/pvpython images and movies; Scripts/summaryPlots.py.
- Data Visualization (Line Plots): Scripts/summaryPlots.py plotDst() produces
  Dst time-series quick-look line plots (log.add_dst_quicklook).
- Data Access and Retrieval: Scripts/updateRamIndices.py and
  Scripts/provisionalIndices.py retrieve Kp/F10.7 indices over FTP (GFZ Potsdam,
  NRCan) and HTTP (NOAA SWPC, spaceweather.gc.ca) via ftplib/urllib.
- File Format Conversion: Scripts/viz/convertRAMrestart.py reads NetCDF4 restart
  files and writes VTK (.vtp/.vtu) for visualization.
- Processing: post-processing utilities ship with the model (Scripts/CatLog.py
  merges SWMF-format log files; Scripts/summaryPlots.py post-processes output).
- HPC: MPI (mpi.f90, ModRamMpi.f90) + OpenMP build options (Config.pl); CI runs
  with openmpi.
- Software or Environment Container: Dockerfile and Dockerfile.RoR provided.

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Atmosphere
Justification: Core science region is the terrestrial inner magnetosphere
(ring current, plasmasphere, radiation belt context). The model also couples to
the upper atmosphere/ionosphere via the GLOW airglow/auroral electron-transport
module and the self-consistent electric-field/ionosphere (SCE) module, and uses
neutral-atmosphere/ionosphere models (MSIS, IRI), giving Earth Atmosphere
relevance.

### 6. Authors (MANDATORY)
1. Vania K. Jordanova
   - Identifier: https://orcid.org/0000-0003-0475-8743
   - Affiliation: Los Alamos National Laboratory
   - Affiliation Identifier: https://ror.org/01e41cf67
2. Miles A. Engel
   - Identifier: https://orcid.org/0000-0003-4248-9636
   - Affiliation: Los Alamos National Laboratory
   - Affiliation Identifier: https://ror.org/01e41cf67
3. Steven K. Morley
   - Identifier: https://orcid.org/0000-0001-8520-0199
   - Affiliation: Los Alamos National Laboratory
   - Affiliation Identifier: https://ror.org/01e41cf67
4. Daniel T. Welling
   - Identifier: https://orcid.org/0000-0002-0590-1022
   - Affiliation: University of Michigan
   - Affiliation Identifier: https://ror.org/00jmfr291
5. Yiqun Yu
   - Identifier: https://orcid.org/0000-0002-1013-6505
   - Affiliation: Beihang University
   - Affiliation Identifier: https://ror.org/00wk2mp56
6. Kateryna Yakymenko
   - Identifier: https://orcid.org/0000-0002-7663-8006
   - Affiliation: Los Alamos National Laboratory
   - Affiliation Identifier: https://ror.org/01e41cf67
7. Rehana Mahfuz
   - Identifier: https://orcid.org/0000-0002-9974-1137
   - Affiliation: Not found
8. Humberto C. Godinez
   - Identifier: https://orcid.org/0000-0001-7138-3481
   - Affiliation: Los Alamos National Laboratory
   - Affiliation Identifier: https://ror.org/01e41cf67
9. Louis Vernon
   - Identifier: Not found
   - Affiliation: Not found
10. Cristoph Junghans
    - Identifier: Not found
    - Affiliation: Not found
- Source: CITATION.cff and DataCite API (concept DOI). Author names "Louis
  Vernon" and "Cristoph Junghans" have no affiliation/ORCID in CITATION.cff;
  both are LANL staff but affiliation is not stated in the repo, so left as
  Not found.

### 7. Software Name (MANDATORY)
RAM-SCB
- Full name: Ring current Atmosphere interactions Model with Self-Consistent
  magnetic field (B). Source: README.md, CITATION.cff title.

### 8. Description (MANDATORY)
RAM-SCB (Ring current Atmosphere interactions Model with Self-Consistent
magnetic field) is a coupled model of the terrestrial inner magnetosphere that
combines a kinetic model of ring current plasma with a three-dimensional
force-balanced model of the magnetic field. The kinetic component (RAM) solves
the bounce-averaged kinetic equation to yield the distribution function as a
function of azimuth, radial distance, energy, and pitch angle for three ion
species (H+, He+, O+) and, optionally, electrons. The three-dimensional
force-balanced magnetic field component (SCB) balances the J x B force against
the divergence of the general pressure tensor to compute the magnetic field
configuration within its domain. The two codes run in tandem: RAM supplies the
anisotropic plasma pressure to SCB, and SCB returns the self-consistent
magnetic field through which the RAM plasma is advected. RAM-SCB includes a
range of additional physics and output products, including wave-particle
interactions (EMIC and chorus pitch-angle diffusion), plasmasphere models
(e.g., Carpenter/Gallagher), a self-consistent electric-field/ionosphere
coupling module, coupled airglow/auroral electron transport via the GLOW
model, and empirical field, neutral-atmosphere, and ionosphere models
(Tsyganenko, IGRF, Weimer, MSIS/NRLMSISE-00, IRI). It can run standalone or as
the Inner Magnetosphere (IM) component of the Space Weather Modeling Framework
(SWMF), two-way coupled to the BATS-R-US global MHD model. RAM-SCB has matured
from a research-grade code into a highly configurable research and space-weather
operations tool. Source: README.md, doc/, src/.

### 9. Concise Description (OPTIONAL)
Coupled kinetic ring current and self-consistent 3-D magnetic field model of
Earth's inner magnetosphere, used for research and space-weather forecasting.

### 10. Publication Date (RECOMMENDED)
2018-11-02
- Date of the first released/published version (v2.1.0) on Zenodo.
  Source: DataCite (version DOI 10.5281/zenodo.6977288).

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- Source: DataCite API. (Software is released via the GitHub-Zenodo workflow.)

### 12. Version (RECOMMENDED)
- **Version Number:** v2.2.0
- **Version Date:** 2023-05-19
- **Version Description:** Builds on the v2.1 series by updating and fixing bugs
  in the plasmasphere models, modernizing the CatLog log-merging script,
  updating documentation, and modernizing/updating index-retrieval scripts and
  the RamIndices data files. Source: DataCite abstract for this release.
- **Version PID:** https://doi.org/10.5281/zenodo.7951034
- Note: This is the latest tagged release in the repo (git tags end at v2.2.0).
  The prompt references a later commit (8508522, 2024-09-20) on main that is
  past the v2.2.0 tag; no newer tagged release/DOI was found.

### 13. Programming Language (RECOMMENDED)
- Fortran90
- Fortran77
- C
- C++
- Python 3.x
- Source: code analysis. Majority of src/, srcInterface/, srcGlow/ is free-form
  Fortran (.f90); legacy fixed-form Fortran77 (.f/.for) in srcExternal/ and
  srcGlow/ (e.g., Tsyganenko, IGRF, MSIS, IRI, GLOW); RamGSL.c is C; C++ wrappers
  in share/Library/src/linear_solver_wrapper_c.cpp (README requires a C++
  compiler, g++); Config.pl build script is Perl (not an allowed HSSI value);
  supporting/launch/visualization scripts (launch_run.py, Scripts/) are Python 3.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1029/2018JA026260
- Engel et al. (2019), "Improved simulations of the inner magnetosphere during
  high geomagnetic activity with the RAM-SCB model," JGR Space Physics.
  Identified as the preferred citation in CITATION.cff.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause License (Triad National Security/LANL variant with
  U.S. Government rights clause)
- **License URI:** https://github.com/lanl/RAM-SCB/blob/master/LICENSE.txt
- Note: LICENSE.txt is a 3-clause BSD-style license with an added DOE/NNSA
  government-rights paragraph; it is not an exact SPDX match. Release approved
  as open source under LA-CC-16-077 (README). GLOW and other external libraries
  carry their own licenses (srcGlow/Glowlicense.txt: Open Source Academic
  Research License).

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- ring current
- inner magnetosphere
- magnetosphere
- space weather
- kinetic model
- plasma
- self-consistent magnetic field
- plasmasphere
- wave-particle interactions
- radiation belts
- swmf
- magnetohydrodynamics
- space physics
- heliophysics
- Source: README, source modules, coupling docs. (No subjects in DataCite;
  no repository topics extracted.)

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific
- FTP/FTPS Directories
- HTTP/HTTPS Directories
- Other
- Note: The model is driven by geomagnetic/solar indices (Kp, F10.7, AE) and
  by plasma/field boundary conditions. Index-retrieval scripts fetch indices
  over FTP (ftp.gfz-potsdam.de, ftp.seismo.nrcan.gc.ca via ftplib) and HTTP
  (spaceweather.gc.ca, NOAA SWPC via urllib) in Scripts/updateRamIndices.py and
  Scripts/provisionalIndices.py; the Real-of-Record (RoR) workflow uses GEO
  satellite flux boundaries (makeGEOboundary.py). No CDAWeb/HAPI/SSCWeb/VSO
  client found in-repo.

### 18. Input File Formats (RECOMMENDED)
- ascii
- netCDF3/4
- Other
- Source: ModRamIO.f90 / ModRamNCDF.f90 read NetCDF (e.g., initialization.nc,
  flux boundary, restart files via netcdf module). Many inputs are ascii/text
  (.txt, .dat, .asc) under input/ (RamIndices.txt, AEindex.txt, IGRF/DGRF .dat,
  CCIR .asc, diffusion-coefficient .dat). PARAM.in configuration files are
  custom plain-text ("Other").

### 19. Output File Formats (RECOMMENDED)
- netCDF3/4
- ascii
- Other
- Source: RAM flux written as NetCDF output, plus hourly ASCII logs and
  diagnostic outputs (ModRamIO.f90, ModRamNCDF.f90). Visualization scripts
  (Scripts/viz) convert NetCDF restart files to VTK XML (.vtp/.vtu) and PNG
  images ("Other").

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Note: README/docs target Linux ("or similar"); CI runs on Ubuntu 20.04
  (.github/workflows/ramscb-ci.yml); Docker image based on ubuntu:20.04.
  macOS is supported via the same gfortran/gcc/g++ + GSL + NetCDF-Fortran
  toolchain (Unix-like). Windows not indicated.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- HPC or HEC
- Note: Built/tested on x86-64 (Ubuntu CI, Docker). MPI + OpenMP parallelism
  targets HPC clusters. No explicit arm64/Apple Silicon testing found.

### 22. Related Phenomena (OPTIONAL)
- geomagnetic storms
- substorms
- ring current
- radiation belts
- EMIC waves
- chorus waves
- plasmasphere dynamics
- aurora
- Note: None of these match the controlled-vocabulary list in the field
  definitions (which is solar-focused). Provided as custom entries grounded in
  README, ModRamWPI.f90 (EMIC/chorus), ModRamPlasmasphere.f90, srcGlow (aurora),
  and the cited publications.

### 23. Development Status (RECOMMENDED)
Active
- Reached a stable, usable state with tagged releases (v2.1.0–v2.2.0), DOIs,
  CI, and continued commits on main (latest 2024-09-20). Source: git history,
  CI workflow, repostatus criteria.

### 24. Documentation (RECOMMENDED)
https://github.com/lanl/RAM-SCB/blob/master/doc/RAM_SCB.pdf
- The RAM-SCB manual (installation, configuration, usage, scripts, SWMF
  coupling, testing, visualization) is in doc/RAM_SCB.pdf, built from
  doc/Tex/. No separate hosted (Read the Docs) site found.

### 25. Funder (OPTIONAL)
1. **Organization:** United States Department of Energy
   - **Funder Identifier:** https://ror.org/01bj3aw27
2. **Organization:** National Nuclear Security Administration
   - **Funder Identifier:** https://ror.org/03sk1we31
- Note: No fundingReferences in DataCite. The DOE/NNSA attribution comes from
  LICENSE.txt (U.S. Government contract 89233218CNA000001 operating LANL via
  Triad National Security, LLC) and is institutional/operational support rather
  than a stated research grant. Specific research grants are not listed in the
  repository.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** 89233218CNA000001 (DOE contract operating LANL; from
  LICENSE.txt). Note: this is the LANL operating contract, not a research award
  title; no research grant title/number is stated in the repo.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1016/j.asr.2022.08.077 — Jordanova et al. (2023), The
  RAM-SCB model and its applications to advance space weather forecasting, Adv.
  Space Res., 72, 5596-5606.
- https://doi.org/10.1029/2018JA026260 — Engel et al. (2019), Improved
  simulations of the inner magnetosphere during high geomagnetic activity with
  the RAM-SCB model, JGR Space Physics, 124, 4233-4248. (Also the reference
  publication.)
- https://doi.org/10.1029/2010JA015671 — Jordanova, Zaharia & Welling (2010),
  Comparative study of ring current development using empirical, dipolar, and
  self-consistent magnetic field simulations, JGR.
- https://doi.org/10.1029/2010JA015642 — Welling, Jordanova, Zaharia, Glocer &
  Toth (2011), The effects of dynamic ionospheric outflow on the ring current,
  JGR.
- https://doi.org/10.1029/2006JA011644 — Jordanova et al. (2006), Kinetic
  simulations of ring current evolution during the GEM challenge events, JGR.
- Source: README "Attribution" section.

### 28. Related Datasets (OPTIONAL)
Not found
- No dataset DOIs referenced in the repository.

### 29. Related Software (OPTIONAL)
- https://github.com/SWMFsoftware/BATSRUS — BATS-R-US global MHD model (coupled
  partner via SWMF).
- Space Weather Modeling Framework (SWMF) — RAM-SCB serves as the IM component
  (https://github.com/SWMFsoftware/SWMF).
- GLOW (GLobal airglOW model), Stan Solomon / HAO-NCAR — bundled in srcGlow/
  (https://github.com/NCAR/GLOW).
- spacepy — required by the visualization scripts
  (https://github.com/spacepy/spacepy).
- Note: Repository URLs given where confidently known; exact upstream repos for
  SWMF/BATS-R-US should be confirmed (SWMFsoftware org hosts canonical copies).

### 30. Interoperable Software (OPTIONAL)
- BATS-R-US / SWMF — demonstrated two-way coupling (RAM-SCB runs as the SWMF IM
  component; srcInterface/IM_wrapper.f90, doc/Tex/RAM_SCB_swmf.tex).
- ParaView (pvpython) — used to render VTK output from Scripts/viz.

### 31. Related Instruments (OPTIONAL)
Not found
- The model supports virtual/"flown" satellites (ModRamSats.f90) but is not
  tied to a specific physical instrument.

### 32. Related Observatories (OPTIONAL)
Not found
- No specific mission/observatory is the target of the software. (Geosynchronous
  particle flux boundary conditions are used in the RoR workflow, but no named
  observatory is required.)

### 33. Logo (OPTIONAL)
Not found
- No logo file or logo URL found in the repository.
