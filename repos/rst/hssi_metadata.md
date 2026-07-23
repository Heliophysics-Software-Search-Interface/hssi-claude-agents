# HSSI Metadata Extraction Results

**Repository:** https://github.com/SuperDARN/rst
**Extraction Date:** 2026-06-03

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.801458
- Note: Concept DOI (all versions), from README badge and docs/index.md. Resolves via DataCite/Zenodo to "SuperDARN Radar Software Toolkit (RST)".

### 3. Code Repository (MANDATORY)
https://github.com/SuperDARN/rst
- Note: From git remote and mkdocs.yml (repo_url).

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Processing
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Data Reduction
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Spectrogram
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Forward-Fitting
- Servers and Environments
- Servers and Environments:Data servers processing and handling

- Notes / evidence:
  - **Coordinate Transforms (Ionospheric / Magnetospheric):** Implements the Altitude-Adjusted Corrected Geomagnetic (AACGM and AACGM_v2) coordinate system, Magnetic Local Time (MLT/MLT_v2), the International Geomagnetic Reference Field (IGRF/IGRF_v2), geomagnetic/geographic field-line mapping, and SGP4/astronomical algorithms (astalg). Libraries: `codebase/analysis/src.lib/{aacgm,aacgm_v2,mlt,mlt_v2,igrf,igrf_v2,geopack,astalg}`; about.md explicitly lists AACGM, IGRF, SGP4 and "a set of coordinate transform functions". v5.1 release notes add AACGM_v2 + IGRF coefficients and eccentric dipole coordinates for TS18 models.
  - **Data Processing and Analysis (Analysis / Processing):** Core SuperDARN pipeline — autocorrelation function (ACF) fitting from RAWACF to FITACF using multiple fitting algorithms (FITACF 2.5/3.0, LMFIT/LMFIT_v2, FITEX), gridding (FITACF -> GRID), and spherical-harmonic convection map fitting (FITACF/GRID -> MAP). Libraries under `codebase/superdarn/src.lib/tk/{acf,acfex,fitacf*,lmfit*,fitex*,grid,gtable,cnvmap,shf}` and binaries `make_fit`, `make_grid`, `map_fit`, `map_grd`.
  - **File Format Conversion:** Extensive `reformat/` tools convert between SuperDARN binary DMAP formats and legacy/ASCII (e.g., `rawacftodat`, `dattorawacf`, `fitacftofit`, `fittofitacf`, `fittoascii`, `grdmaptogrid`, `gridtogrdmap`, `maptocnvmap`, `cnvmaptomap`, `oldsndtosnd`, `map_ascii`).
  - **Data Reduction:** Despecking (`fit_speck_removal`), filtering (`fitfilter`, `grid_filter`, `map_filter`), trimming/combining tools (`trim_*`, `combine_grid`, `merge_grid`).
  - **Data Visualization (2D Graphics / Line Plots / Spectrogram):** Plotting binaries produce PostScript/PPM imagery — `field_plot`, `fov_plot`, `grid_plot`, `map_plot` (convection maps), `vec_plot`, `hmb_plot`, `pc_plot`, `time_plot` (range-time / range-time-intensity plots), `iqplot`. Range-time intensity plots and dynamic spectra map to the Spectrogram subcategory. Libraries: `codebase/general/src.lib/{grplotlib,contour,raster}`, `binplotlib`.
  - **Models and Simulations (Empirical):** Empirical statistical convection models — TS18, TS18-Kp, CS10, PSR10 (`cnvmodel`, `map_addmodel`, `solve_model`), plus Christmas Valley virtual height model. Also a data simulator library (`sim_data`, `make_sim`, `sim_real`).
  - **Models and Simulations (Forward-Fitting):** Parameter optimization against model functions — `map_fit` performs spherical-harmonic fitting of observed line-of-sight velocities constrained by a statistical convection model (`map_fit.doc.xml`: "Perform the Spherical Harmonic Fitting on a convection map file"); `lmfit`/`lmfit_v2` (`codebase/superdarn/src.lib/tk/lmfit_v2.0`, `lmfit.1.0`) fit a model (single-component Lorentzian/exponential-decay) ACF to the observed ACF via the Levenberg-Marquardt algorithm (`make_fit.md`). Matches the HSSI Forward-Fitting definition (synthetic/model data + parameter optimization).
  - **Servers and Environments (Data servers):** Real-time TCP/IP FITACF server/client tools (`fitacfserver`, `fitacfclient`, `fitacfclientgui`, `fitacfclientscan`, `rtfittofitacf`) for streaming/serving processed radar data; supporting `codebase/base/src.lib/tcpip`.
  - NOT included: Data Access and Retrieval — README/docs/data.md explicitly state "RST does not provide an interface for downloading data."

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Atmosphere

- Note: SuperDARN HF radars observe the high-latitude ionosphere/thermosphere and map ionospheric convection, which is the footprint of magnetospheric electric fields. about.md notes use with ITM (ionosphere-thermosphere-mesosphere) data sets and spacecraft (Polar, TIMED, ACE) and ground magnetometers. "Earth Atmosphere" covers the ionosphere/thermosphere; "Earth Magnetosphere" covers the convection/coupling science. (Interplanetary Space considered via IMF inputs to convection models but the software's core region is ionosphere/magnetosphere; left out to avoid over-classification.)

### 6. Authors (MANDATORY)
Primary credited author/organization (from .zenodo.json, AUTHORS.md, DataCite v5.1 DOI 10.5281/zenodo.4435150):

1. **SuperDARN Data Analysis Working Group** (organizational author/maintainer)
2. **Thomas, E.G.** — ORCID https://orcid.org/0000-0001-8036-8793 — Dartmouth College (ROR https://ror.org/049s0rh22)
3. **Burrell, A.G.** — ORCID https://orcid.org/0000-0001-8875-9326 — United States Naval Research Laboratory (ROR https://ror.org/04a9s4445)
4. **Ponomarenko, P.V.** — ORCID https://orcid.org/0000-0001-8407-0193 — University of Saskatchewan (ROR https://ror.org/010hz4p62)
5. **Bland, E.C.** — ORCID https://orcid.org/0000-0002-0252-0400 — The University Centre in Svalbard (ROR https://ror.org/05d7e2443)
6. **Sterne, K.T.** — ORCID https://orcid.org/0000-0002-1076-0009 — Virginia Polytechnic Institute and State University (ROR https://ror.org/0113b0661)
7. **Rohel, R.A.** — ORCID https://orcid.org/0000-0003-2208-1553 — University of Saskatchewan (ROR https://ror.org/010hz4p62)
8. **Shepherd, S.G.** — ORCID https://orcid.org/0000-0003-1992-4118 — Dartmouth College (ROR https://ror.org/049s0rh22)
9. **Billett, D.D.** — ORCID https://orcid.org/0000-0002-8905-8609 — University of Saskatchewan (ROR https://ror.org/010hz4p62)
10. **Schmidt, M.T.** — ORCID https://orcid.org/0000-0002-3265-977X — University of Saskatchewan (ROR https://ror.org/010hz4p62)
11. **Walach, M.-T.** — ORCID https://orcid.org/0000-0002-9352-0659 — Lancaster University (ROR https://ror.org/026a3xj54)

- Notes: Author list and ORCIDs/affiliations from `.zenodo.json` and the v5.1 DataCite record. Surname for author 9 spelled **"Billett"** (two t's) per `AUTHORS.md` (the human-curated source) and the resolving ORCID 0000-0002-8905-8609; the `.zenodo.json` spelling "Billet" (one t) is a typo and was not used. AUTHORS.md additionally credits the original JHUAPL authors (R.J. Barnes and K.B. Baker as main authors of the original codebase, adapted from RADOPS) and many additional DAWG contributors (D. Andre, R.A. Greenwald, C. Hanuise, N. Mattin, K. Oksavik, J.M. Ruohoniemi, J.P. Villain, S. Wing, A. Grocott, K. Kotyk, A.S. Reimer, A.J. Ribeiro, C.L. Waters, E.D.P. Cousins, I. Coco, and others). "Virginia Tech" expanded to "Virginia Polytechnic Institute and State University"; "Naval Research Laboratory" expanded to "United States Naval Research Laboratory".

### 7. Software Name (MANDATORY)
SuperDARN Radar Software Toolkit (RST)
- Note: From README ("Radar Software Toolkit"), .zenodo.json, and DataCite title.

### 8. Description (MANDATORY)
The Radar Software Toolkit (RST) is the official open-source data-analysis package for the Super Dual Auroral Radar Network (SuperDARN), an international network of HF coherent-scatter radars that observe ionospheric plasma convection at high latitudes. RST provides a complete command-line processing pipeline that converts raw radar data into scientific products: fitting autocorrelation functions to produce line-of-sight velocity, spectral width, and power (RAWACF -> FITACF, using the FITACF 2.x/3.0, LMFIT, and FITEX algorithms), combining fitted data into gridded velocity maps (FITACF -> GRID), and fitting global high-latitude ionospheric convection patterns with spherical-harmonic expansions constrained by statistical convection models such as TS18, TS18-Kp, CS10, and PSR10 (GRID -> MAP). It includes implementations of the Altitude-Adjusted Corrected Geomagnetic (AACGM/AACGM_v2) coordinate system, Magnetic Local Time (MLT), the International Geomagnetic Reference Field (IGRF), SGP4, and a suite of coordinate-transform functions. RST also provides visualization binaries that generate field-of-view, range-time, field, grid, and convection-map plots; tools for converting among SuperDARN data formats; a real-time TCP/IP FITACF server/client; and a data simulator. Originally developed at the Johns Hopkins University Applied Physics Laboratory and now maintained collaboratively by the SuperDARN Data Analysis Working Group (DAWG), it is written in ANSI C with Interactive Data Language (IDL) components and runs on Linux and macOS.
- Note: Synthesized from README.md, docs/about.md, docs/index.md, mkdocs.yml navigation, AUTHORS.md, and codebase structure.

### 9. Concise Description (OPTIONAL)
Official open-source toolkit for processing, modelling, and visualizing SuperDARN HF radar data of high-latitude ionospheric convection; converts raw data to fitted velocities, grids, and convection maps.
- Note: 199 characters.

### 10. Publication Date (RECOMMENDED)
2017-05-31
- Note: Date of the earliest version published on Zenodo under the concept DOI (v4.0, DOI 10.5281/zenodo.801459, dateType "Issued"). The software itself predates this (JHUAPL origin), but 2017-05-31 is the first DataCite/Zenodo publication record.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- Note: From DataCite (`attributes.publisher` = "Zenodo") for the RST DOI records.

### 12. Version (RECOMMENDED)
- **Version Number:** v5.1
- **Version Date:** 2025-05-02
- **Version Description:** Key updates include addition of AACGM_v2 and IGRF coefficients supporting mapping until ~2030; new eccentric-dipole coordinate derivation for the TS18 and TS18-Kp convection models; new tools `find_elvstat` (realistic elevation-angle measurement counts) and `oldsndtosnd` (legacy binary sounding -> DMAP); addition of slant-range (srng) parameter to grid and map files; updated `grid_filter` (range-based filtering); `fitacfclientgui` viewing improvements; and extensive new/updated radar information (Iceland East/West, Longjing, Siziwanqi, Hejing, Hokkaido East, SANAE, Hankasalmi, etc.).
- **Version PID:** https://doi.org/10.5281/zenodo.4435150
- Note: Version number from `.rst.version` (5.1), git tag v5.1, and DataCite version record. Version-specific DOI 10.5281/zenodo.4435150 (issued 2025-05-02). Description from the v5.1 Zenodo/DataCite abstract.

### 13. Programming Language (RECOMMENDED)
- C
- IDL
- Note: about.md states RST is "written using a combination of ANSI C and the Interactive Data Language (IDL)". Source counts: ~887 .c files, ~336 .h files, ~79 .pro (IDL) files, ~16 .dlm (IDL DLM). No Fortran sources present. "C" chosen over "C++" (ANSI C).

### 14. Reference Publication (RECOMMENDED)
Not found
- Note: No JOSS or peer-reviewed software paper is cited in README/CITATION. README directs citation to the Zenodo DOI. (Underlying methods are documented in journal papers, e.g., the TS18 convection-model paper by Thomas & Shepherd 2018, but no single canonical software reference publication is declared in the repo.)

### 15. License (RECOMMENDED)
- **License:** GNU General Public License v3.0 only
- **License URI:** https://www.gnu.org/licenses/gpl-3.0-standalone.html
- Note: LICENSE file is GPL v3 (29 June 2007); docs/index.md states "licensed under GPL v3.0"; DataCite rightsList confirms "GNU General Public License v3.0 only".

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- SuperDARN
- HF radar
- ionosphere
- ionospheric convection
- space physics
- space weather
- AACGM
- geomagnetic coordinates
- IGRF
- magnetosphere
- coordinates
- Note: Derived from README, docs/about.md, and codebase scope. No explicit keyword/topic list in repo metadata.

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific
- Note: Operates on SuperDARN radar data files. RST does not download data itself (docs/user_guide/data.md); data are obtained externally from SuperDARN data mirrors (SuperDARN Canada/Globus, BAS) and FRDR.

### 18. Input File Formats (RECOMMENDED)
- Other
- CDF
- ascii
- Note: Primary inputs are SuperDARN-specific binary DMAP formats (RAWACF, DAT, IQDAT, FITACF/FIT, CFIT, GRID, MAP, SND) — represented as "Other". Reads NASA CDF (CI installs the NASA CDF library; `codebase/analysis/src.lib/cdf/rcdf`). ASCII inputs supported by some reformat tools.

### 19. Output File Formats (RECOMMENDED)
- Other
- ascii
- CDF
- netCDF3/4
- Note: Outputs SuperDARN DMAP binary formats (FITACF, GRID, MAP, etc.) -> "Other"; ASCII output via `fittoascii`, `map_ascii`, `extract_*`; CDF output via the `dmaptocdf` binary (`codebase/general/src.bin/dmap/dmaptocdf.1.9`) and netCDF output via the `dmaptoncdf` binary (`codebase/general/src.bin/dmap/dmaptoncdf.1.11`, requires `libnetcdf`); plotting binaries also produce PostScript/PPM image output (graphics, not in the HSSI data-format list).

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Note: README provides Linux and macOS installation guides (Windows "yet to be implemented"). CI (.github/workflows/main.yml) tests ubuntu-latest and macos-latest.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64
- Note: Inferred — CI runs on x86-64 Linux and macOS runners; macOS support implies Apple Silicon arm64. No explicit architecture statement in repo; this is an inference.

### 22. Related Phenomena (OPTIONAL)
- Ionospheric convection
- Note: Custom term. The controlled-vocabulary list (Coronal Heating, Coronal Holes, CMEs, Solar Corona, Solar Flares, X-ray emission) is solar-focused and none apply to SuperDARN; the field allows custom entries. Software supports study of high-latitude ionospheric plasma convection, field-aligned currents, and magnetosphere-ionosphere coupling.

### 23. Development Status (RECOMMENDED)
Active
- Note: Tagged stable releases (v5.1 in 2025, v5.1.1 in Dec 2025), active GitHub issues/PRs and CI, ongoing DAWG maintenance.

### 24. Documentation (RECOMMENDED)
https://radar-software-toolkit-rst.readthedocs.io/en/latest/
- Note: From README. Secondary API documentation at https://superdarn.github.io/rst/ . ReadTheDocs configured via .readthedocs.yaml + mkdocs.yml.

### 25. Funder (OPTIONAL)
Not found
- Note: No funder declared in repo metadata or .zenodo.json. SuperDARN is funded by national agencies of Australia, Canada, China, France, Italy, Japan, Norway, South Africa, the United Kingdom, and the United States (per the README data acknowledgement), but no specific funder/grant is attributed to the RST software itself.

### 26. Award Title (OPTIONAL)
Not found
- Note: No award/grant identifiers present in the repository.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2022RS007449 — FitACF 3.0 noise-estimation method
- https://doi.org/10.5194/angeo-24-115-2006 — FitACF 2.0 algorithm
- https://doi.org/10.1002/2017RS006450 — LMFit 2.0 algorithm
- https://doi.org/10.1002/rds.20031 — LMFit 1 / FitEX algorithm
- Note: DOIs for the ACF-fitting algorithms implemented in RST, hyperlinked in `docs/user_guide/make_fit.md`. Additional calibration-related DOIs appear in `tables/superdarn/tdiff/` (e.g., 10.1002/2016RS006089, 10.1029/2018rs006638, 10.1029/2017rs006492, 10.1029/2024RS007957) and may be added if desired.

### 28. Related Datasets (OPTIONAL)
- SuperDARN raw data collection (FRDR): https://www.frdr-dfdr.ca/repo/collection/superdarn
- Note: From README; SuperDARN rawacf/dat data published on FRDR (CC BY-NC 4.0). No DOI declared in repo.

### 29. Related Software (OPTIONAL)
- pyDARN: https://github.com/SuperDARN/pydarn
- Note: pyDARN is the SuperDARN Python data visualization library (DOI 10.5281/zenodo... ; PyHC community package) and is the Python-side companion to RST. RST was historically adapted from RADOPS (RADar OPerating System) at JHUAPL per AUTHORS.md.

### 30. Interoperable Software (OPTIONAL)
Not found
- Note: No interoperability explicitly declared. RST requires the NASA CDF library and IDL (for IDL components) but these are dependencies rather than declared interoperable packages.

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** SuperDARN HF radars (Super Dual Auroral Radar Network coherent-scatter HF radars)
- Note: RST is purpose-built for SuperDARN HF coherent-scatter radars. about.md also references compatibility with Polar, TIMED, and ACE spacecraft data, ground-based magnetometers, and incoherent scatter radars.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** SuperDARN (Super Dual Auroral Radar Network)
- Note: The international SuperDARN radar network; RST is its official analysis toolkit.

### 33. Logo (OPTIONAL)
Not found
- Note: No software logo file or logo URL found in the repository.
