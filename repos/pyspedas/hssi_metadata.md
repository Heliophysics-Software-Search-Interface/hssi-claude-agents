# HSSI Metadata Extraction Results

**Repository:** https://github.com/spedas/pyspedas
**Extraction Date:** 2026-04-24

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.17634923
- Source: Concept DOI (all versions) from CITATION.cff and pyproject.toml `[project.urls]` Concept_DOI; confirmed via DataCite API.

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/spedas/pyspedas
- Source: Repository URL confirmed via PyHC core registry, DataCite, CITATION.cff (swh identifier), and pyproject.toml.

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Coordinate Transforms:Mission-Specific
- Coordinate Transforms:Planetary
- Data Processing and Analysis
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:3D Particle Distribution Processing
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Curlometer
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Field-line Tracing
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Linear Gradient Estimation
- Data Processing and Analysis:Magnetic Null Finding
- Data Processing and Analysis:Pitch Angle Distributions
- Data Processing and Analysis:Plasma Moments
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:Wave Polarization Analysis
- Data Processing and Analysis:Wavelet Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:2D Slices
- Data Visualization:3D Graphics
- Data Visualization:Hodograms
- Data Visualization:Line Plots
- Data Visualization:Mission-Specific
- Data Visualization:Orbit Plots
- Data Visualization:Spacecraft Formation Plots
- Data Visualization:Spectrogram
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Field-line Tracing
- Models and Simulations:Physics-Based
- Source: Determined from source code analysis. Coordinate transforms cover GSE/GSM/SM/GEO/MAG/GEI/J2000 (cotrans_tools/cotrans_lib.py), MLT (sm2mlt), and mission-specific frames (mms_qcotrans for BCS/DBCS/DMPA/SMPA/DSL/SSL/ECI; mms_cotrans_lmn). Data Processing covers wavelet/wavpol (analysis/wavelet*.py, twavpol.py), magnetic null finding (find_magnetic_nulls.py), linear gradient estimation (lingradest.py), curlometer (mms.curlometer), particle moments (particles/moments/), pitch angle distributions (mms_feeps_pad, mms_eis_pad), 2D slices of distributions (spd_slice2d/), energy spectra (mms_part_getspec, energy spectrum routines), field-line tracing (geopack/ttrace2endpoint, trace_to_event), spectrograms (pwr_spec, dpwrspc), time series (tplot_math/), filtering (time_domain_filter), data reduction (avg_data, reduce_tres, rebin), calibration (elfin epd cal, mms scm cal), file format conversion (cdf_to_tplot, netcdf_to_tplot, tplot_ascii), data access (CDAWeb, HAPI, SPDF, ISTP, mission-specific load routines), interpolation (interpol, tinterpol, tinterp). Visualization covers line plots, spectrograms, hodograms, 2D/3D plots (tplotxy, tplotxy3), orbit plots (mms_orbit_plot), formation plots (mms_tetrahedron_qf), 2D slice plots (slice2d_plot, slice1d_plot). Models include Tsyganenko T89/T96/T01/TS04 (geopack/), IGRF empirical magnetic field model, neutral sheet models, magnetopause/bow shock models (mpause_2, mpause_t96, bshock_2), L-shell calculation.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Magnetosphere
- Interplanetary Space
- Planetary Magnetospheres
- Solar Environment
- Source: PySPEDAS supports data from missions across all major heliophysics regions. Earth Atmosphere: ground magnetometers (GMAG, MICA, IUGONET), aurora research, ionospheric observations (DE2, FAST, C/NOFS, Akebono, ICON). Earth Magnetosphere: THEMIS, MMS, Cluster, Polar, RBSP/Van Allen Probes, Geotail, IMAGE, Equator-S, Geopack/Tsyganenko magnetospheric field models. Interplanetary Space: ACE, Wind, DSCOVR, Ulysses, OMNI, STEREO, solar wind data. Planetary Magnetospheres: MAVEN (Mars). Solar Environment: Parker Solar Probe (PSP), Solar Orbiter (SOLO), SOHO, STEREO solar observations.

### 6. Authors (MANDATORY)
1. **Vassilis Angelopoulos** | ORCID: https://orcid.org/0000-0001-7024-1561 | UCLA Division of Physical Sciences
2. **Bryan Harter** | ORCID: https://orcid.org/0000-0002-3908-9001 | Laboratory for Atmospheric and Space Physics
3. **Eric Grimes** | ORCID: https://orcid.org/0000-0001-5756-8789 | Adnet Systems (United States)
4. **Cindy Russell**
5. **Jiashu Wu** | University of California, Los Angeles
6. **Jim Lewis** | ORCID: https://orcid.org/0009-0005-4191-5906 | University of California, Berkeley
7. **Alexander Drozdov** | ORCID: https://orcid.org/0000-0002-5334-2026 | University of California, Los Angeles
8. **Nick Hatzigeorgiu** | University of California, Los Angeles
9. **James McTiernan** | ORCID: https://orcid.org/0000-0002-3038-176X | University of California, Berkeley
10. **Daniel Carpenter** | University of California, Los Angeles
11. **Julie Barnum** | ORCID: https://orcid.org/0000-0001-8755-0694 | Laboratory for Atmospheric and Space Physics
12. **Ayris Narock** | ORCID: https://orcid.org/0000-0001-6746-7455 | Adnet Systems (United States)
13. **Beforerr** (GitHub user)
14. **Marc Pulupa** | ORCID: https://orcid.org/0000-0002-1573-7457 | University of California, Berkeley
15. **Xiangning Chu** | ORCID: https://orcid.org/0000-0003-4109-0770 | University of Colorado Boulder
16. **Brent Smith** | Johns Hopkins University Applied Physics Laboratory
17. **Tiger** (GitHub user)
18. **Austin Norris** | University of California, Los Angeles
19. **Kiril B** (GitHub user)
20. **Samuel Badman** | ORCID: https://orcid.org/0000-0002-6145-436X | Center for Astrophysics | Harvard & Smithsonian
21. **Anansa Keaton-Ashanti** | The University of Texas at Austin
22. **Tomo Hori** | Nagoya University
23. **Takanobu Amano** | ORCID: https://orcid.org/0000-0002-2140-6961
24. **Warren Rexroad** | University of California, Berkeley
25. **krvidal** (GitHub user)
26. **Shuji Onosawa**
27. **Luke Powell** | Southwest Research Institute
28. **thigli** (GitHub user)
29. **Mykhaylo Shumko** | ORCID: https://orcid.org/0000-0002-0437-7521
30. **Qusai Al Shidi** | ORCID: https://orcid.org/0000-0003-0426-038X | West Virginia University
31. **Sandy Antunes** | Johns Hopkins University Applied Physics Laboratory
32. **Sean A. Q. Young** | Johns Hopkins University Applied Physics Laboratory
33. **Tien 'Vo**
34. **donglai96** (GitHub user)
35. **rale8469** (GitHub user)
36. **Benjamin Short** | ORCID: https://orcid.org/0000-0003-3945-6577
37. **Elysia Lucas** | Laboratory for Atmospheric and Space Physics
- Source: CITATION.cff (authoritative author list with affiliations and ORCIDs); cross-checked with Zenodo and DataCite metadata.

### 7. Software Name (MANDATORY)
- **Name:** PySPEDAS
- **Full Name:** PySPEDAS (Space Physics Environment Data Analysis System in Python)
- Source: pyproject.toml `name = "pyspedas"`, README.md, CITATION.cff title, PyHC registry, Zenodo title.

### 8. Description (MANDATORY)
- **Description:** The Python-based Space Physics Environment Data Analysis Software (PySPEDAS) framework supports multi-mission, multi-instrument retrieval, analysis, and visualization of heliophysics time series data. PySPEDAS provides a unified Python interface (modeled on the IDL SPEDAS toolkit) for loading data from over 35 space- and ground-based heliophysics projects (including ACE, Akebono, Arase/ERG, Cluster, CSSWE, C/NOFS, DSCOVR, DE2, Equator-S, FAST, Geotail, GOES, IMAGE, MAVEN, MICA, MMS, OMNI, POES, Polar, Parker Solar Probe, SOHO, Solar Orbiter, STEREO, ST5, SECS, Swarm, THEMIS/ARTEMIS, TWINS, Ulysses, Van Allen Probes/RBSP, Wind, and ground magnetometer networks). It bundles tools for coordinate transformations (GSE, GSM, SM, GEO, MAG, LMN, FAC, etc.), particle distribution analysis (moments, 2D slices, pitch angle distributions, energy spectra), wavelet and wave polarization analysis, magnetic field modeling (Tsyganenko T89/T96/T01/TS04, IGRF) and field-line tracing, multi-spacecraft analysis (curlometer, linear gradients, magnetic null finding), neutral sheet/magnetopause/bow shock models, the embedded PyTplot framework for time-series management and plotting (line plots, spectrograms, orbit plots, hodograms, 3D and projection plots), and CDAWeb / HAPI / SPDF / ISTP data servers, plus cloud (S3) repository support.
- Source: README.md, CITATION.cff abstract, docs/source/index.rst, codebase analysis.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Python framework for multi-mission, multi-instrument retrieval, analysis, and visualization of heliophysics time-series data, with built-in tools for coordinate transformations, magnetic field modeling, and particle distribution analysis.
- Source: Derived from pyproject.toml description and README.md.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2016-10-11
- Source: First commit date from repository history (`git log --reverse --format='%H %cs %s'`); DataCite/CITATION.cff dates describe later DOI/software-release records rather than the original repository publication.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- Source: DataCite API publisher field for concept DOI 10.5281/zenodo.17634923.

### 12. Version (RECOMMENDED)
- **Version Number:** v2.1.0
- **Version Date:** 2026-02-23
- **Version Description:** PySPEDAS 2.1.0 introduces tplotxy3 (three-orthogonal-plane spacecraft trajectory plots) with options to overlay magnetopause, bow shock, and neutral sheet models; adds plotting of multiple field-line traces; refactors plot saving to a separate routine; includes accuracy fixes to gse2sse coordinate transform; adds neutral_sheet to top-level imports; and improves legend layout in Jupyter notebooks. Continues PySPEDAS 2.x series in which the previously external pytplot/pytplot-mpl-temp packages are bundled directly.
- **Version PID:** https://doi.org/10.5281/zenodo.18718385
- Source: Git tag `v2.1.0`, pyproject.toml version, git log of recent commits, Zenodo versioned-DOI metadata, pyproject.toml `Versioned_DOI` URL.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- Source: pyproject.toml `requires-python = ">=3.10"`, classifiers (Python 3.10–3.14), README installation instructions; codebase is pure Python.

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.3389/fspas.2022.1020815
- Title: "The Space Physics Environment Data Analysis System in Python" (Frontiers in Astronomy and Space Sciences, 2023; Angelopoulos et al.)
- Source: Zenodo `relatedIdentifiers` (relation: isDescribedBy), confirmed via DataCite API.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT
- Source: LICENSE.txt (MIT text), pyproject.toml `license = "MIT"`, CITATION.cff `license: mit`, DataCite/Zenodo metadata.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- heliophysics
- space physics
- space weather
- magnetosphere
- ionosphere
- heliosphere
- solar wind
- aurora
- ground magnetometer
- coordinate transformations
- magnetic field modeling
- Tsyganenko
- IGRF
- geopack
- particle moments
- plasma
- pitch angle distributions
- spectrograms
- wave polarization
- wavelet analysis
- time series analysis
- data access
- CDF
- HAPI
- CDAWeb
- ISTP
- ACE
- Akebono
- Arase
- ERG
- BARREL
- Cluster
- CSSWE
- C/NOFS
- DSCOVR
- DE2
- ELFIN
- Equator-S
- FAST
- Geotail
- GOES
- IMAGE
- ICON
- KOMPSAT
- Kyoto Dst
- LANL
- MAVEN
- MICA
- MMS
- OMNI
- POES
- Polar
- Parker Solar Probe
- PSP
- SOHO
- Solar Orbiter
- SOLO
- STEREO
- ST5
- SECS
- Swarm
- THEMIS
- ARTEMIS
- TWINS
- Ulysses
- Van Allen Probes
- RBSP
- Wind
- pytplot
- IDL SPEDAS
- Source: Combined from CITATION.cff keywords, pyproject.toml keywords, PyHC core registry keywords, and Zenodo subjects.

### 17. Data Sources (OPTIONAL)
- CDAWeb
- FTP/FTPS Directories
- HAPI
- HTTP/HTTPS Directories
- OMNIWeb
- Observatory/Mission-specific
- Other
- S3/Cloud-aware
- VirES
- Source: Codebase analysis (cdagui_tools/, hapi_tools/, mth5/, vires/, projects/*/load.py); README "Cloud Repositories" section; .github/workflows/full_coverage.yml shows CDAWeb, HAPI, SPDF, MMS-SDC, LASP, IRIS, mission-specific, HTTP/HTTPS, and S3/cloud-aware data sources.

### 18. Input File Formats (RECOMMENDED)
- CDF
- netCDF3/4
- HDF5
- IDL.sav
- ascii
- JSON
- Other
- Source: pyproject.toml dependencies (cdflib, netCDF4, h5py via spacepy); tplot_tools/importers/ (cdf_to_tplot.py, netcdf_to_tplot.py, sts_to_tplot.py for STS ascii, tplot_restore.py reads IDL `.sav` tplot save files via scipy.io.readsav); HDF5 input via the optional `mth5` extra; JSON config files; "Other" covers proprietary formats: STS (Space Time Series ASCII), MMS L0 packet binaries, MTH5 (HDF5-based magnetotelluric), pickled tplot save files, calibration/parameter text tables.

### 19. Output File Formats (RECOMMENDED)
- ascii
- csv
- Other
- Source: tplot_tools/exporters/ (tplot_ascii.py writes CSV via pandas.to_csv with default `.csv` extension; tplot_save.py writes Python pickle); MPLPlotter/save_plot.py produces image outputs (PNG/PDF/SVG via matplotlib backend). "Other" covers matplotlib figure formats (PNG, PDF, SVG, EPS) and pickled tplot save files.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows
- Source: README.md ("PySPEDAS supports Windows, macOS and Linux"); pyproject.toml classifier `Operating System :: OS Independent`; CI workflows test on `ubuntu-latest`; cross-platform compatibility documented in pyspedas/projects/mms/README.md.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent
- Source: Pure-Python package with NumPy/SciPy native dependencies; pyproject.toml classifies the package as operating-system independent and does not declare a CPU-architecture-specific requirement.

### 22. Related Phenomena (OPTIONAL)
- Solar Wind
- Coronal Mass Ejections
- Solar Flares
- Magnetic Reconnection
- Magnetospheric Substorms
- Geomagnetic Storms
- Auroral Phenomena
- Radiation Belts
- Ring Current
- Magnetopause
- Bow Shock
- Neutral Sheet / Plasma Sheet
- Field-Aligned Currents
- ULF/ELF/VLF waves
- Energetic Particle Events
- Source: Mission scope (THEMIS substorms, MMS reconnection, RBSP radiation belts, MAVEN Mars solar-wind interaction, ACE/Wind solar wind / CME monitoring, GOES/Kyoto Dst geomagnetic storm tracking, ground magnetometers / aurora). Built-in models for magnetopause, bow shock, neutral sheet. Wave polarization analysis (twavpol) supports ULF/ELF/VLF wave studies.

### 23. Development Status (RECOMMENDED)
- **Status:** Active
- Source: README.md repostatus badge ("Project Status: Active – The project has reached a stable, usable state and is being actively developed"); pyproject.toml classifier `Development Status :: 5 - Production/Stable`; recent commits (2026-02-23 v2.1.0 release); PyHC registry quality ratings all "Good".

### 24. Documentation (RECOMMENDED)
- **URL:** https://pyspedas.readthedocs.io
- Source: README.md, pyproject.toml `[project.urls]` Documentation, .readthedocs.yaml, PyHC registry docs field.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration (NASA)
- **Funder Identifier:** https://ror.org/027ka1x80
- Source: Zenodo grants metadata (THEMIS NAS5-02099, SPEDAS Community Support NNG17PZ01C, MMS NNG04EB99C — all NASA-funded).

### 26. Award Title (OPTIONAL)
1. **Award Title:** THEMIS
   - **Award Number:** NAS5-02099
2. **Award Title:** SPEDAS Community Support
   - **Award Number:** NNG17PZ01C
3. **Award Title:** MMS
   - **Award Number:** NNG04EB99C
- Source: Zenodo grants/funding metadata.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found — the primary reference (Angelopoulos et al., 2023) is captured in Field 14, and no additional non-reference publications are cited as priorities by the developers in the repository or Zenodo metadata.

### 28. Related Datasets (OPTIONAL)
Not found — PySPEDAS accesses many heliophysics datasets at runtime but does not bundle or formally cite specific datasets.

### 29. Related Software (OPTIONAL)
- https://github.com/spedas/pyspedas_examples — pyspedas_examples (companion examples and Jupyter notebooks)
- https://github.com/spedas/mms-examples — MMS PySPEDAS examples
- https://github.com/spedas/themis-examples — THEMIS PySPEDAS examples
- https://github.com/spedas/bleeding_edge — IDL SPEDAS (parent project, IDL-based predecessor)
- https://github.com/MAVENSDC/cdflib — cdflib (CDF file I/O dependency)
- https://github.com/spacepy/spacepy — SpacePy (CDF/coordinates/quaternion dependency)
- https://github.com/tsssss/geopack — geopack (Tsyganenko/IGRF magnetic field model implementation)
- https://github.com/hapi-server/client-python — hapiclient (HAPI server data retrieval)
- https://doi.org/10.5281/zenodo.14919975 — supplementary software dataset (related via Zenodo `isSupplementedBy`)
- Source: pyproject.toml dependencies, README.md "Additional Information" links, Zenodo related identifiers.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/MAVENSDC/cdflib — cdflib
- https://github.com/spacepy/spacepy — SpacePy
- https://github.com/tsssss/geopack — geopack
- https://github.com/hapi-server/client-python — hapiclient
- https://github.com/astropy/astropy — Astropy (core dependency)
- https://github.com/PlasmaPy/PlasmaPy — PlasmaPy (used in PySPEDAS analysis examples)
- https://github.com/spedas/bleeding_edge — IDL SPEDAS (compatible coordinate frames, file conventions, save-file restore)
- https://github.com/numpy/numpy — NumPy
- https://github.com/scipy/scipy — SciPy
- https://github.com/matplotlib/matplotlib — matplotlib
- https://github.com/pydata/xarray — xarray (tplot variables backed by xarray DataArrays)
- https://github.com/pandas-dev/pandas — pandas
- Source: pyproject.toml `dependencies`, README "Examples" section (PlasmaPy notebook, SpacePy quaternion notebook), `convert_tplotxarray_to_pandas_dataframe` interoperability function.

### 31. Related Instruments (OPTIONAL)
- ACE: MAG, SWEPAM, EPAM, SIS, CRIS, ULEIS, SEPICA, SWICS
- Akebono: PWS, RDM, ORB
- Arase/ERG: MGF, MEP-e, MEP-i, LEP-e, LEP-i, HEP, XEP, PWE (HFA/OFA/EFD/WFC), Orbit
- BARREL: SSPC
- Cluster: FGM, EFW, STAFF, WBD, WHISPER, EDI, PEACE, CIS, RAPID, ASPOC, DWP
- CSSWE: REPTile
- C/NOFS: VEFI, CINDI, PLP
- DSCOVR: MAG, FC, ATT
- DE2: FPI, IDM, LANG, MAG, NACS, RPA, VEFI, WATS
- ELFIN: EPD, FGM, MRMa
- Equator-S: EDI, EPI, ICI, MAM, PCD, SFD
- FAST: ACF, DCF, ESA, TEAMS
- Geotail: CPI, EFD, EPIC, LEP, MGF, PWI
- GOES: FGM, MAG
- IMAGE: HENA, LENA, MENA, RPI, EUV, FUV
- KOMPSAT: MAG, particle detectors
- MAVEN: MAG, SWEA, SWIA, STA, SEP, EUV, LPW
- MMS: FGM, SCM, FSM, EDI, EDP, FPI (DIS/DES), HPCA, EIS, FEEPS, ASPOC, DSP, MEC
- MICA: induction magnetometers
- POES: SEM
- Polar: CAMMICE, CEPPAD, EFI, HYDRA, MFE, PWI, TIDE, TIMAS
- Parker Solar Probe (PSP): FIELDS, SWEAP (SPC, SPAN-i, SPAN-e), ISOIS (EPI-Lo, EPI-Hi)
- Solar Orbiter (SOLO): MAG, SWA, RPW, EPD
- SOHO: CELIAS, COSTEP, ERNE
- STEREO: MAG, PLASTIC
- THEMIS/ARTEMIS: FGM, EFI, ESA, SST, SCM, MOM, GMOM, GMAG, State
- TWINS: LAD (Lyman Alpha Detector), Ephemeris
- Ulysses: VHM, EPAC, GRB, HISCALE, SWICS, SWOOPS
- Van Allen Probes (RBSP): EFW, EMFISIS, HOPE, MagEIS, RBSPICE, REPT, RPS
- Wind: MFI, SWE, 3DP, WAVES, SMS
- ST5: MAG
- Swarm: MAG (and VirES products)
- Source: docs/source/_static/ instrument plot images and pyspedas/projects/<mission>/ load routines / README files.

### 32. Related Observatories (OPTIONAL)
- ACE (Advanced Composition Explorer)
- Akebono
- Arase / ERG (Exploration of energization and Radiation in Geospace)
- BARREL (Balloon Array for RBSP Relativistic Electron Losses)
- Cluster
- CSSWE (Colorado Student Space Weather Experiment)
- C/NOFS (Communications/Navigation Outage Forecasting System)
- DSCOVR (Deep Space Climate Observatory)
- DE2 (Dynamics Explorer 2)
- ELFIN (Electron Losses and Fields Investigation)
- Equator-S
- FAST (Fast Auroral Snapshot Explorer)
- Geotail
- GOES (Geostationary Operational Environmental Satellite)
- IMAGE (Imager for Magnetopause-to-Aurora Global Exploration)
- ICON (Ionospheric Connection Explorer)
- KOMPSAT
- LANL (Los Alamos National Laboratory geosynchronous satellites)
- MAVEN (Mars Atmosphere and Volatile Evolution)
- MICA (Magnetic Induction Coil Array)
- MMS (Magnetospheric Multiscale)
- POES (Polar Orbiting Environmental Satellites)
- Polar
- Parker Solar Probe (PSP)
- Solar Orbiter (SOLO)
- SOHO (Solar and Heliospheric Observatory)
- STEREO (Solar Terrestrial Relations Observatory)
- ST5 (Space Technology 5)
- SECS (Spherical Elementary Currents — derived ground product)
- Swarm
- THEMIS / ARTEMIS
- TWINS (Two Wide-Angle Imaging Neutral-Atom Spectrometers)
- Ulysses
- Van Allen Probes (RBSP)
- Wind
- Kyoto WDC (ground geomagnetic indices)
- INTERMAGNET, IUGONET, SuperMAG, GMAG networks (ground magnetometer arrays)
- Source: README.md "Projects Supported", pyspedas/projects/ subdirectories, pyspedas/projects/mms/README.md, ground network references in CITATION.cff keywords.

### 33. Logo (OPTIONAL)
Not found — repository contains no dedicated PySPEDAS logo image; PyHC core registry entry does not provide a logo URL. The SPEDAS project hosts branding at http://spedas.org/wiki/ but no canonical logo image URL was identified.
