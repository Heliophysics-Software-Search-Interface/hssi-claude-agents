# HSSI Metadata Extraction Results

**HSSI Software ID:** cf629d4b-a92c-4f53-9e6b-79248dc99489
**Repository:** https://github.com/GFZ/SWVO
**Source Revision:** 1d958871ad9cf431cc3290d413a297f32229270e
**Extraction Date:** 2026-11-03
**Validation Date:** 2026-11-03
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

1. **The pinned revision is six commits after the 1.2.9 release.** `git log 1.2.9..1d95887` holds four
   automated pre-commit dependency bumps (`b8342fe`, `a6f8c8e`, `813689f`, `1d95887`), one functional fix
   (`e1201f8`, "fix solar wind variable handling when combining solar wind from multiple sources",
   touching `swvo/io/solar_wind/read_solar_wind_from_multiple_models.py` and `swvo/io/utils.py`) and a
   docs commit (`268bf6d`, adding `docs/presentation.rst`, which embeds the project's PyHC telecon
   slides). Every capability cited below is already present at the `1.2.9` tag; nothing in the record
   depends on unreleased code.

2. **The repository history predates the public project.** The first commit (`f817da5`, 2021-02-05,
   Ruggero Vasile) belongs to an internal GFZ GitLab project whose package was called `data_management`
   (the removed `.gitlab-ci.yml` and the `data_management/` tree are visible in commit `13025e7`,
   2025-08-21, "change name to SWVO"). The GitHub repository was created 2025-06-25 and the first public
   release is 1.0.0 on 2025-08-22. The earlier name was never published: there is no `data-management` or
   `data_management` project on PyPI and no GitHub repository under either name in the GFZ organization.
   This matters for Fields 2, 6 and 10.

3. **How the readers work.** Each reader class (one per index and source) fetches from a remote service
   in `download_and_process`, writes cleaned daily or monthly CSV files into a user-chosen data directory,
   and `read()` returns pandas DataFrames built from those files. The `read_*_from_multiple_models`
   functions stitch several readers together by priority (historical measurements up to a cutoff time,
   forecasts after it) onto one regular time grid. A second group of readers — `KpEnsemble`,
   `HpEnsemble`, `SWSWIFTEnsemble`, `PlasmaspherePredictionReader`, `PlasmasphereCombinedInputsReader` —
   fetches nothing: they read local forecast files from the PAGER project's operational forecast systems. This
   governs Fields 4, 17, 18 and 19.

4. **`swvo.io.RBMDataSet` is shipped but deprecated.** Its package docstring
   (`swvo/io/RBMDataSet/__init__.py:7-11`) reads "This subpackage is deprecated. RBM dataset handling now
   lives in `el_paso <https://github.com/GFZ/EL_PASO>`_. It is kept here only for backward compatibility
   and will not receive new features." The class docstring (`swvo/io/RBMDataSet/RBMDataSet.py:61-65`)
   reads "RBM dataset handling has moved to `el_paso <https://github.com/GFZ/EL_PASO>`_. This class is kept
   here only for backward compatibility and will not receive new features." (Both quotations join the
   source's wrapped lines.)
   The README never mentions it. Capabilities that only this subpackage provides (reading `.mat` and
   `.pickle` RBM files, binning satellite data onto a model grid, its matplotlib debug figures) are
   therefore not credited to SWVO in Fields 4, 18 and 19; they are the sister package's (Field 29).

5. **The name.** The project's PyHC talk slides (linked from `docs/presentation.rst`, hosted at
   `https://sahiljhawar.in/swvo-pyhc/`) title the package "SWVO: Solar Wind Virtual Observatory" with the
   subtitle "Unified access to space weather data and geomagnetic indices in Python". No file in the
   repository spells out the acronym.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** Shawn Polson
- **Submitter Email:** shawn.polson@lasp.colorado.edu

Supplied by the submitting curator (rule 4). The addresses in the source tree are author and
maintainer contacts, never the submitter (rule 2): `jhawar@gfz.de` and `bhaas@gfz.de` in
`CITATION.cff:18,21` and in the PyHC registry `contact:`, and the GFZ section mailbox `sec15@gfz.de` in
`pyproject.toml:12`.

### 2. Persistent Identifier (RECOMMENDED)
Not found

SWVO has no software DOI. The no-DOI proof:

- **Project files.** No `.zenodo.json`, no `codemeta.json`, no DOI badge in `README.md`, and
  `CITATION.cff` carries no `doi` or `identifiers`. A case-insensitive search of the tracked tree for
  `doi|zenodo` (excluding `uv.lock`) finds only the reference DOIs of the five SuperMAG substorm-onset
  catalogues (`swvo/io/substorms/catalogs.py:38-78`, `docs/supermag_substorms.rst:263-271`) and of the
  SuperMAG electrojet-index paper (`docs/supermag_indices.rst:170`) — papers about data products the
  software reads, not identifiers of the software.
- **Title and subject search.** DataCite `titles.title:SWVO` and the free-text query `"GFZ/SWVO"` return
  only **SWVO Test Data** (concept `10.5281/zenodo.22983305`, version `10.5281/zenodo.22983306`, Zenodo,
  issued 2026-09-26, creators Jhawar and Haas, `IsSupplementTo https://github.com/GFZ/SWVO`). Its
  `resourceTypeGeneral` is `Dataset`, so Field 2 rule 1 excludes it; it is the test-suite fixture set
  and is weighed (and excluded) under Field 28.
- **Old name.** `https://github.com/GFZ/data_management` and `https://github.com/GFZ/data-management`
  do not exist; PyPI has no project under either spelling; the Zenodo query `"data_management" AND GFZ`
  returns nothing.
- **Creator-keyed Zenodo search** (`metadata.creators.person_or_org.name:` and
  `…identifiers.identifier:`): `"Jhawar, Sahil"` → BibQuest (an unrelated tool) and SWVO Test Data;
  `"Sahil Jhawar"` → reuseify and GFZ/EL_PASO; `"Haas, Bernhard"` and Haas's ORCID → radiation-belt
  datasets and figures, EL-PASO Test Data, SWVO Test Data and PINE2025 (a plasmasphere-model software
  deposit, not SWVO); `"Vasile, Ruggero"` → a 2022 VTEC
  neural-network code deposit; `"Bianco, Stefano"` → that same deposit, PINE2025 and records of other
  people. None is a deposit of SWVO's code. Positive control: SWVO Test Data is returned by both the
  title route and the creator route; negative control: a nonsense creator name returns zero.

With no Zenodo DOI identifying the software, Field 11 falls to the repository host.

### 3. Code Repository (MANDATORY)
https://github.com/GFZ/SWVO

The clone's `origin` remote, the GitHub API (`full_name` `GFZ/SWVO`, `html_url`
`https://github.com/GFZ/SWVO`, not archived, not a fork), `pyproject.toml:56` (`Homepage`),
`CITATION.cff:13` (`repository-code`) and the PyHC registry `code:` all agree (rule 7). GitHub also
serves the lower-case path `https://github.com/GFZ/swvo` as the same repository; the canonical
`full_name` spelling is recorded.

### 4. Software Functionality (RECOMMENDED — treated as critical)
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Analysis
- Coordinate Transforms
- Models and Simulations
- Models and Simulations: Forecasting

Every value is a FunctionCategory row, written `Parent: Child`; the parent of each child is listed.
Evidence, value by value:

- **Data Access and Retrieval.** Downloading is the package's core service: every network-backed reader
  implements `download_and_process` (abstract in `swvo/io/base.py`, `BaseIO`) and most `read()` methods
  take `download=True`. Endpoints reached: OMNIWeb (`swvo/io/omni/omni_high_res.py:54`), the SPDF
  low-resolution OMNI directory (`swvo/io/omni/omni_low_res.py:52`), the GFZ Kp/Hp JSON API and nowcast
  file (`swvo/io/kp/niemegk.py:50-52`, `swvo/io/hp/gfz.py:55`), the WDC Kyoto HAPI server
  (`swvo/io/dst/wdc.py:48`), NOAA SWPC text products (`swvo/io/kp/swpc.py:52`, `swvo/io/f10_7/swpc.py:44`),
  the BGS and SIDC Kp forecasts (`swvo/io/kp/bgs.py:50`, `swvo/io/kp/sidc.py:50`), SuperMAG
  (`swvo/io/sme/supermag.py:61`, `swvo/io/substorms/supermag.py:63`), ACE real-time files
  (`swvo/io/solar_wind/ace.py:51`), the NCEI space-weather portal for DSCOVR and WSA-Enlil
  (`swvo/io/solar_wind/dscovr.py:50`, `swvo/io/solar_wind/enlil.py:129`) and IMAP I-ALiRT
  (`swvo/io/solar_wind/imap.py:70`).
- **Processing.** Raw downloads are turned into one standard schema per quantity: fill-value sentinels
  replaced by NaN (`DSCOVR._replace_invalid_values`), records regridded onto complete one-minute ranges
  (`swvo/io/solar_wind/dscovr.py:378-386`), ENLIL netCDF runs extracted from NCEI tar archives and reduced
  to an Earth time series (`swvo/io/solar_wind/enlil.py:431-615`), and the `read_*_from_multiple_models`
  functions (`swvo/io/{kp,dst,hp,f10_7,solar_wind}/read_*_from_multiple_models.py`) merge historical and
  forecast sources by priority onto one grid, labelling each row with its source model.
- **Time Series Analysis.** Temporal operations on the index and solar-wind series that users switch on
  through documented keywords: spline interpolation of short gaps (`do_interpolation=True`,
  `UnivariateSpline` at `swvo/io/solar_wind/read_solar_wind_from_multiple_models.py:780`) and the
  solar-wind propagation in `swvo/io/utils.py:240` (`sw_mag_propagation`), which time-shifts L1 data to
  the bow shock using a Gaussian-smoothed (`scipy.ndimage.gaussian_filter1d`) travel time and is exposed
  as `propagation=True` on the ACE, DSCOVR, IMAP, MIDL and SWIFT readers.
- **Data Reduction.** Ensemble forecasts are reduced to one series by mean or median
  (`reduce_ensemble="mean"|"median"`, `swvo/io/solar_wind/read_solar_wind_from_multiple_models.py:914-916`;
  the Kp and Hp combiners do the same), and IMAP I-ALiRT MAG and SWAPI records are averaged to
  one-minute values (`swvo/io/solar_wind/imap.py:400-401`).
- **Analysis.** Derived physical quantities the user receives: solar-wind dynamic pressure `pdyn`
  computed from density and speed (`swvo/io/solar_wind/ace.py:490`, `dscovr.py:388`, `enlil.py:615`) and
  the bow-shock propagation above.
- **Coordinate Transforms (parent only, rule 11).** The ENLIL reader converts the model's Earth-position
  magnetic field from HEEQ (Heliographic Stonyhurst) spherical components to GSM Cartesian components
  with `sunpy.coordinates` (`SWENLIL._transform_b_to_gsm`, `swvo/io/solar_wind/enlil.py:619-676`), and the
  user receives the converted `bx_gsm`/`by_gsm`/`bz_gsm` columns — rule 3's "converted output the user
  receives". No child fits: the conversion crosses from a heliospheric frame into a magnetospheric one
  for a single model's field vector, so neither `Coordinate Transforms: Heliospheric` ("Between
  heliospheric coordinate systems") nor `Coordinate Transforms: Magnetospheric` ("Between magnetospheric
  coordinate systems") describes it. The conversion is a private step (`_transform_b_to_gsm`) applied
  only to WSA-Enlil output, so SWVO offers no transform a searcher filtering on either child could apply
  to their own data; `Magnetospheric` was considered on the ground that the output columns are GSM, and
  declined for that reason. `Coordinate Transforms: Solar` is rejected too — no solar-disk coordinates
  are handled. The DSCOVR reader's mapping of the portal's `bx_gse`/`by_gse`/`bz_gse` parameters into
  SWVO's `bx_gsm`/`by_gsm`/`bz_gsm` columns (`swvo/io/solar_wind/dscovr.py:54-59`) is a column rename
  with no rotation and is not counted as a transform.
- **Models and Simulations: Forecasting** (with its parent). The package's combined product is a
  prediction series: the `read_*_from_multiple_models` functions take measurements up to a cutoff that
  stands for "now" (`historical_data_cutoff_time`) and forecasts after it, and part of that prediction
  is SWVO's own. With `recurrence=True`, `read_kp_from_multiple_models` gives every Kp step still
  missing, future steps beyond the forecast providers' reach included, the value observed one solar
  rotation (27 days) earlier by the historical readers and labels it `<source>_recurrence`
  (`_recursive_fill_27d_historical`, `swvo/io/kp/read_kp_from_multiple_models.py:67-72,135-143,379-428`):
  the 27-day recurrence (persistence) prediction of geomagnetic activity. `fill_average` then closes any
  remaining forecast tail with climatological values (Kp 4; ten-year solar-wind averages,
  `AVERAGE_VALUES_TO_FILL` in `swvo/io/solar_wind/__init__.py`). Both are documented keywords whose output
  reaches the user (rule 3). The forecasts SWVO reads from SWPC, BGS, SIDC, the PAGER ensembles and
  WSA-Enlil are those systems' capability, not SWVO's (rule 5); the value rests on the recurrence
  prediction. A searcher filtering on Forecasting finds a tool that assembles gapless forecast-horizon
  Kp and solar-wind driver series, which the project's slides present as its main use ("Measurements up
  to now, then a forecast model takes over, as one continuous series").

Considered and rejected:

- **Data Processing and Analysis: File Format Conversion.** The CSV files `download_and_process` writes
  are the readers' own processed cache, read back by `read()`; SWVO offers no conversion a user selects,
  and Field 19 excludes the same writes (its rule 2). In-memory parsing of JSON, text and netCDF is not
  conversion (Field 4 trap).
- **Data Processing and Analysis: Data Assimilation.** The only "assimilation" strings are plot titles
  ("Assimilation input") inside the deprecated `swvo/io/RBMDataSet/bin_and_interpolate_to_model_grid.py`
  debug-figure helpers; no assimilation algorithm exists.
- **Calibration, Image Processing, ML/AI, Spectrogram, Energy Spectra, Pitch Angle Distributions,
  Plasma Moments, Wave/Wavelet analysis, 3D distributions, 2D Slices, Curlometer, Linear Gradient
  Estimation, Magnetic Null Finding, Field-line Tracing, Packet Decommutation** — no code for any of
  them. The machine-learning forecast systems the project's slides name (KpML, PINE) run elsewhere;
  SWVO only reads forecast output files (rule 5).
- **Data Visualization (and every child).** No module outside the deprecated `RBMDataSet` imports
  matplotlib or draws anything; the only figure code is `plot_debug_figures*` in
  `swvo/io/RBMDataSet/bin_and_interpolate_to_model_grid.py:400-635`, a debug aid in the deprecated
  subpackage (scope note 4). `matplotlib` in the dependency list is not a feature (rule 2).
- **Models and Simulations: Empirical, Data Guided, Physics-Based and the other children.** The
  recurrence and average fills copy a past observation or a fixed climatological constant: they fit no
  relation and represent no physical system, so `Empirical` and `Data Guided` would overstate them. The
  bow-shock propagation (`sw_mag_propagation`, `swvo/io/utils.py:240-292`) divides a fixed distance
  (`distance = 1.5e6`, km) by the measured speed: a ballistic time shift, carried under Analysis, not a
  `Physics-Based` model. No MHD solver, first-principles, forward-fitting, instrument-response,
  observatory-model, ML/AI or theory code exists in SWVO (`SWMIDL`'s `method="mhd"` only selects MIDL's own
  propagation, a wrapped-library capability under rule 5).
- **Mission-related (and every child).** SWVO is a third-party reader of finished real-time and archived
  products (ACE RTSW, DSCOVR, IMAP I-ALiRT, OMNI); it is part of no mission's ground system (rule 8).
- **Servers and Environments: Software or Environment Container.** The repository holds an Apptainer
  definition (`swvo.def`) and a workflow (`.github/workflows/apptainer.yml`) that publishes the image to
  `oras://ghcr.io/gfz/swvo` (the workflow tags each image with the package version). It packages SWVO
  itself together with `download_daily_files.py`, and neither the README nor the docs mention it; a
  searcher filtering for container or environment software would find a data-reader library with an
  undocumented image, so the value is not recorded. The rest of `Servers and Environments` has no
  evidence (no server, HPC or infrastructure code).
- **Capabilities of the deprecated `RBMDataSet`** (binning and interpolating satellite flux and phase
  space density onto a model grid, orbit identification, trajectory linearisation) are not credited
  (scope note 4).

### 5. Related Region (RECOMMENDED — treated as critical)
- Interplanetary Space
- Solar Wind
- Earth Magnetosphere
- Earth Inner Magnetosphere
- Earth Atmosphere
- Earth Ionosphere
- Earth Auroral Subregion
- Solar Environment

Each fine row carries its own evidence (rule 4) and brings its coarse row (rule 5):

- **Solar Wind** (+ **Interplanetary Space**): the solar-wind readers process L1 plasma and magnetic
  field measurements from ACE, DSCOVR and IMAP, the OMNI bow-shock-shifted record, MIDL, and the SWIFT
  and WSA-Enlil solar-wind forecasts (`swvo/io/solar_wind/`), and propagate L1 data to the bow shock.
- **Earth Inner Magnetosphere** (+ **Earth Magnetosphere**): the Dst readers, documented as measuring
  "the intensity of the Earth's ring current" (`README.md`, Dst bullet), the SYM-H reader
  (`swvo/io/symh/omni.py`), and the plasmasphere-density readers, whose `PlasmasphereDensityCube` holds
  electron density on an L × MLT grid (`swvo/io/plasmasphere/read_plasmasphere.py`). The Kp and Hp30/Hp60
  readers handle planetary geomagnetic-activity indices of magnetospheric current systems, which the
  coarse row also covers.
- **Earth Ionosphere** and **Earth Auroral Subregion** (+ **Earth Atmosphere**): the SuperMAG SME/SML/SMU
  indices "describe the auroral electrojet" (`README.md`; `swvo/io/sme/supermag.py`), an ionospheric
  current in the auroral zone, and the substorm-onset catalogues locate onsets at the auroral station
  contributing to SML or at the auroral brightening seen in IMAGE-FUV and Polar UVI images
  (`swvo/io/substorms/catalogs.py:29-78`).
- **Solar Environment** (coarse alone, rule 6): the F10.7 readers handle "a daily measure of solar
  activity", the project describing its scope as "solar and geomagnetic indices" (`README.md`). No finer
  solar row is evidenced: the 10.7 cm flux originates in the upper chromosphere and corona, but SWVO
  treats it purely as an activity index and handles nothing about where it is emitted, so `Corona` and
  `Chromosphere` are not recorded.

Rejected: **Earth Magnetotail** — substorms originate in the tail, but SWVO reads onset lists derived
from ground SML and auroral images and handles no tail data; **Earth Magnetosheath** — the bow-shock
propagation is a time shift, not magnetosheath physics; **Earth Thermosphere** and **Earth Lower and
Middle Atmosphere** — Kp, Hp and F10.7 drive thermosphere models downstream, which is not this software's
physics (rule 4 trap); **Earth Outer Magnetosphere**, **Heliosheath**, the **solar interior/photosphere**
rows and every **planetary** row — no evidence. The PyHC registry's facet tags (`heliosphere`,
`magnetosphere`, `solar`, `ionosphere_thermosphere_mesosphere`) were not used as evidence (rule 3); each
row above rests on code.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Bernhard Haas
- **Author Identifier:** https://orcid.org/0000-0003-0379-7281
- **Affiliation:**
  - **Organization:** GFZ Helmholtz Centre for Geosciences
  - **Affiliation Identifier:** https://ror.org/04z8jg394

**Author 2:**
- **Name:** Sahil Jhawar
- **Author Identifier:** https://orcid.org/0000-0002-0003-0571
- **Affiliation:**
  - **Organization:** GFZ Helmholtz Centre for Geosciences
  - **Affiliation Identifier:** https://ror.org/04z8jg394

**Author 3:**
- **Name:** Stefano Bianco
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** GFZ Helmholtz Centre for Geosciences
  - **Affiliation Identifier:** https://ror.org/04z8jg394

**Author 4:**
- **Name:** Ruggero Vasile
- **Author Identifier:** https://orcid.org/0000-0003-3640-3517
- **Affiliation:**
  - **Organization:** GFZ Helmholtz Centre for Geosciences
  - **Affiliation Identifier:** https://ror.org/04z8jg394

**Who is an author (rules 8 and 5–6).** Three project sources name exactly these four people in this
order: `CITATION.cff:15-25` (given/family split for each), `AUTHORS.md` and `pyproject.toml:12` (one
combined name string). `docs/conf.py:19` names the first two. There is no DOI deposit of the software, so
there is no Zenodo creator list. Not authors:

- **Simon Mischel** and **Matyas Szabo-Roberts** appear only as REUSE `SPDX-FileContributor` headers
  (Mischel on `README.md`, several `docs/` pages, `swvo/io/__init__.py` and the OMNI index readers;
  Szabo-Roberts on `README.md`). That is a per-file contributor heading the project keeps separate from
  its author list (rule 6); Mischel's commits date from 2026-07/08 and Szabo-Roberts's (`matszabo`) from
  2022-11/12.
- **Committers absent from every attestation** (rule 5): Dmitrii Gurev, Parvathy S, Alexander Y.
  Drozdov, a shared `PAGER user` and `root` machine account, and the dependabot, Copilot and Claude bots.

**Order.** `CITATION.cff` order, which `AUTHORS.md` and `pyproject.toml` repeat.

**Names (rule 12).** Each given/family split is `CITATION.cff`'s, and each ORCID record writes the same
split. Before SWVO's submission the catalogue held no Person row under any of the four names and none
carrying any of the three ORCIDs.

**Identifiers (rules 14 and 16).** ORCID fielded searches (`given-names:<G> AND family-name:<F>`) with a
positive control (`Yuri Shprits`, one GFZ record) gave:

- **Haas — `0000-0003-0379-7281` recorded.** Two records carry the name. This one's researcher URL is the
  GFZ staff page `https://www.gfz-potsdam.de/staff/bernhard.haas`, matching his `bhaas@gfz.de` commit
  address, and its works are radiation-belt and plasmasphere papers (EL-PASO, PINE, VERB-3D); Zenodo
  creator records for EL-PASO Test Data and the May 2024 radiation-belt dropout dataset carry the same
  ORCID. Rejected: `0000-0003-0229-9117`, a University of Plymouth School of Health Professions record
  whose one work is a Parkinson's-disease study.
- **Jhawar — `0000-0002-0003-0571` recorded.** The only record with the name; employment at GFZ,
  department "Space Physics and Space Weather" (student assistant 2024–2025, research scientist /
  scientific programmer from 2026, ROR `04z8jg394`), matching his `jhawar@gfz.de` commit address; works
  include the 2026 EGU abstract on validating data-assimilative plasmasphere, ring-current and
  radiation-belt simulations.
- **Vasile — `0000-0003-3640-3517` recorded.** The only record with the name; employment "Helmholtz
  Centre Potsdam - GFZ German Research Centre for Geosciences", Section 2.8, scientist, 2017–present
  (GRID `grid.23731.34`, GFZ), covering his 2021-02 to 2022-10 commits from `ruggero@gfz-potsdam.de`.
  OpenAlex attaches this ORCID to a GFZ author profile whose topics are ionosphere/magnetosphere
  dynamics, and he co-created the 2022 Zenodo VTEC neural-network code deposit with Stefano Bianco.
  Crossref bylines carry the same ORCID: "Systematic Analysis of Machine Learning and Feature Selection
  Techniques for Prediction of the Kp Index" (2019, https://doi.org/10.1029/2019SW002271, with a GFZ Potsdam
  affiliation) and "Thermosphere and satellite drag" (2023, https://doi.org/10.1016/j.asr.2023.05.011).
- **Bianco — no identifier.** Six ORCID records carry the name; none connects to this person (four have
  no works and no employment; `0000-0001-5434-8676` is a Politecnico di Torino materials scientist;
  `0000-0002-8300-4124` is an INFN particle physicist). The GFZ space-physics Stefano Bianco's OpenAlex
  profile carries no ORCID. A name match alone is not linkage (rule 14), so none is recorded; a later
  refresh should re-check only if a record linked to GFZ appears.

**Affiliations (rule 21).** GFZ Helmholtz Centre for Geosciences (ROR `https://ror.org/04z8jg394`, ROR
display name verbatim, the name the catalogue's Organization row for that ROR carries):

- **Haas and Jhawar:** the project's own Zenodo deposit SWVO Test Data gives both creators the
  affiliation "GFZ Helmholtz Centre for Geosciences"; Jhawar's ORCID employment and Haas's GFZ staff page
  agree, as do their `gfz.de` commit addresses and the GFZ `SPDX-FileCopyrightText` headers across the
  REUSE-compliant tree.
- **Vasile:** ORCID employment at GFZ covering the period of his commits. OpenAlex lists a later
  non-GFZ institution among his last-known affiliations; it is not added (rule 18: an employer joined
  after producing the software).
- **Bianco:** paper bylines covering his 2021-02 to 2025-09 commit period give GFZ: "A Kp-Driven Machine
  Learning Model Predicting the Ultraviolet Emission Auroral Oval" (2025,
  https://doi.org/10.1029/2024JH000543) and his 2023 and 2024 EGU abstracts on solar-wind forecasting.
  His commit addresses are `bianco@gfz-potsdam.de`.

### 7. Software Name (MANDATORY)
SWVO

The project writes `SWVO` as its name: `CITATION.cff:8` (`title: SWVO`), the PyHC registry
(`_data/projects.yml` at heliophysicsPy/heliophysicsPy.github.io `b1e3c97`, `name: "SWVO"`), the
GitHub repository name, the Apptainer label `Description SWVO` (`swvo.def`) and the test-data deposit
title "SWVO Test Data". Alternatives considered:

- `SWVO @ GFZ` — the README H1 (`README.md:11`), which appends the host institution; the registry and
  `CITATION.cff` write the bare name, and the registry decides among the project's own forms (rule 8).
- `swvo` — the distribution, import and Sphinx `project =` name (`pyproject.toml:10`,
  `docs/conf.py:17`), a conventional lower-case slug (rule 4).
- `Solar Wind Virtual Observatory` — the expansion on the project's talk slides (scope note 5); no
  repository source or registry uses it as the name.
- `data_management` — the pre-2025 internal package name, never published (scope note 2).

### 8. Description (MANDATORY)
The value is the text between the fences, exactly as written (the fences are not part of it):

```markdown
Tools for downloading and reading space-weather data and geomagnetic indices.

This package provides tools to read, process, and analyze several key solar and geomagnetic indices. For each index, the available data sources and the corresponding reader classes are listed below:

- **Kp Index**:
  A global geomagnetic activity index with a 3-hour cadence, ranging from 0 (quiet) to 9 (extremely disturbed). Used to assess geomagnetic storm conditions.
  - **Sources & Classes:**
    - OMNI: `KpOMNI`
    - SWPC: `KpSWPC`
    - Niemegk: `KpNiemegk` (alias: `KpGFZ`)
    - Ensemble: `KpEnsemble`
    - BGS: `KpBGS`
    - SIDC: `KpSIDC`
    - Combined: `read_kp_from_multiple_models`

- **Dst Index**:
  The Disturbance Storm Time (Dst) index measures the intensity of the Earth's ring current, related to geomagnetic storms. Provided hourly and is negative during storm conditions.
  - **Sources & Classes:**
    - OMNI: `DSTOMNI`
    - WDC: `DSTWDC`
    - Combined: `read_dst_from_multiple_models`

- **Hp Index**:
  The Hp30 and Hp60 indices are high-cadence (30-minute and 60-minute) geomagnetic indices provided by GFZ, used for detailed geomagnetic activity studies.
  - **Sources & Classes:**
    - GFZ: `HpGFZ`
    - Ensemble: `HpEnsemble`
    - Combined: `read_hp_from_multiple_models`

- **F10.7 Index**:
  The F10.7 solar radio flux index is a daily measure of solar activity (flux density at 10.7 cm), a standard proxy for solar EUV emissions.
  - **Sources & Classes:**
    - OMNI: `F107OMNI`
    - SWPC: `F107SWPC`
    - Combined: `read_f107_from_multiple_models`

- **SuperMAG electrojet indices**:
  SME, SML, and SMU describe the auroral electrojet using the SuperMAG ground-magnetometer network at one-minute cadence. Access requires a valid SuperMAG account.
  - **Sources & Classes:**
    - SuperMAG: `SMESuperMAG`

- **Substorm-onset events**:
  Sparse onset catalogues identified from SuperMAG SML or auroral images. The available techniques are Newell, Forsyth/SOPHIE, Ohtani, Frey, and Liou.
  - **Sources & Classes:**
    - SuperMAG: `SubstormsSuperMAG`

- **Solar Wind Parameters**:
  Access to solar wind data (speed, density, magnetic field components) from various spacecraft. Essential for solar-terrestrial interaction studies.
  - **Sources & Classes:**
    - ACE: `SWACE`
    - DSCOVR: `DSCOVR`
    - IMAP: `SWIMAP`
    - OMNI: `SWOMNI`
    - SWIFT: `SWSWIFTEnsemble`
    - ENLIL: `SWENLIL_BKG` (ambient background runs), `SWENLIL_CME` (CME simulation runs)
    - MIDL: `SWMIDL` (merged L1 record from ACE, DSCOVR, WIND and SOHO)
    - Combined: `read_solar_wind_from_multiple_models`

- **Plasmasphere Density Predictions**:
  Reader utilities for PAGER plasmasphere density grids and model combined inputs.
  - **Sources & Classes:**
    - Density predictions: `PlasmaspherePredictionReader`
    - Combined inputs: `PlasmasphereCombinedInputsReader`
    - Density cube container: `PlasmasphereDensityCube`

Each index can be accessed via these dedicated reader classes, which handle downloading and read methods.
```

**Sources (rule 7).** The first paragraph is the `CITATION.cff:9` `abstract` verbatim (also
`pyproject.toml:14` `description`, the PyPI summary, the GitHub description and the PyHC registry
`description:`). One sentence is too thin to say what the package covers, so the README's "Space Weather
Data Overview" section (`README.md:44-107`) follows unaltered and in order, with two edits: the section
heading is dropped, and the README's final pointer sentence ("See the code in `swvo/io` or API
documentation for details on each index's implementation.") is dropped as navigation. The source lists
are kept because they name the services and spacecraft a searcher types (SWPC, Niemegk, BGS, SIDC, WDC,
ACE, DSCOVR, IMAP, SWIFT, ENLIL, MIDL) and the class names make each list item actionable. One typo is
corrected (rule 5): the README's `BSG: KpBGS` (`README.md:53`) is written `BGS: KpBGS` — the class is
`KpBGS`, which reads the British Geological Survey forecast (`swvo/io/kp/bgs.py:50`).

**Claims checked against the pinned code (rule 2).** Every class named exists and is exported from its
subpackage's `__init__.py`; `KpGFZ` is an alias of `KpNiemegk` (`swvo/io/kp/__init__.py`); the SuperMAG
account requirement is the `username` argument of `SMESuperMAG` (`swvo/io/sme/supermag.py:44-46`); the
five substorm techniques are the five catalogues in `swvo/io/substorms/catalogs.py`. The page is read as
markdown; the result-card preview is the first sentence, which carries no markup.

**Considered and not used.** The README "Introduction" paragraph ("This package provides a set of tools
for managing solar data in Python. It includes functionalities for reading, writing, and processing data
from various sources.", `README.md:22`) — the `CITATION.cff` abstract states the scope more accurately
(the package is mostly geomagnetic indices and solar wind, not "solar data"), and "writing" would imply
an output-file capability Field 19 does not record. The talk-slide subtitle "Unified access to space
weather data and geomagnetic indices in Python" is a near-duplicate of the abstract.

### 9. Concise Description (OPTIONAL)
Tools for downloading and reading space-weather data and geomagnetic indices.

The PyHC registry's `description:` for SWVO (`_data/projects.yml` at
heliophysicsPy/heliophysicsPy.github.io `b1e3c97`), the first source in rule 6's order. The project's
other one-line summaries are byte-identical to it: `pyproject.toml:14` `description` (also the PyPI
summary), the `CITATION.cff:9` `abstract` and the GitHub repository description. It is 77 characters with
no markup, within the 200-character limit (rule 3). Every claim in it is backed by the pinned code, as
for Field 8 (rule 2), and it has no spelling or grammar error (rule 4).

Shawn Polson decided that every new entry in this submission batch carries a concise description as
well as a description. That decision overrides rule 6's empty outcome, which is the alternative not
taken. Under rule 6 alone the field would stay empty, because the description's opening sentence is this
same text and already serves as the card preview. The value therefore repeats Field 8's first sentence,
by design.

### 10. Publication Date (RECOMMENDED)
2025-08-22

The first public release: GitHub release `1.0.0` published 2025-08-22T09:49:36Z, and the PyPI upload of
`swvo` 1.0.0 at 2025-08-22T09:50:10Z (rule 4, anchor a). Alternatives considered: the GitHub repository's
`created_at` (2025-06-25) does not satisfy anchor (b), because the first commit on the pin's ancestry is
2021-02-05 — the history was developed on GFZ's internal GitLab and pushed later; the 2021-02-05 first
commit is not a publication date, since the code under its earlier name `data_management` was never
publicly released (scope note 2).

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

No DOI identifies the software (Field 2), so rule 5 gives the repository host: the catalogue's `GitHub`
Organization row (identifier `https://github.com`). GFZ is the copyright holder
(`reuseify.toml`, every SPDX header) and the repository lives in the GFZ GitHub organization, but nothing
names GFZ as the software's publisher or distributor (rule 3 needs such a statement; a copyright holder
is not the publisher). PyPI is a distribution channel, never the publisher (rule 6).

### 12. Version (RECOMMENDED)
- **Version Number:** 1.2.9
- **Version Date:** 2026-10-16
- **Version Description:**
  - Fetch historical Kp from the GFZ API in KpNiemegk
  - Use HAPI for WDC Dst, add start_of_next_month helper
  - set default midl target to 14
- **Version PID:** Not found

**Number.** The newest release: tag `1.2.9` (an ancestor of the pin), GitHub release named `v1.2.9`,
PyPI `swvo` 1.2.9 (wheel `swvo-1.2.9-py3-none-any.whl` and sdist, neither yanked), and the declared
version at the tag (`swvo/__init__.py`, `pyproject.toml:103`). Recorded without the `v`, as the tag, PyPI
and package metadata write it. Release history: 1.0.0, 1.1.0, 1.2.0–1.2.9, with pre-releases 1.2.2rc0–rc2
and 1.2.7rc0–rc1 that never count (rule 2); one tag is spelled `v1.2.6` while every other is bare.

**Date.** GitHub release `published_at` 2026-10-16T14:37:30Z; the PyPI upload (14:37:52Z) and the tagged
commit (2026-10-16 16:36 +02:00) fall on the same UTC day.

**Description.** The release body's items (rules 13–15), trimmed whole and with the trailing
"by @sahiljhawar in https://github.com/GFZ/SWVO/pull/N" credits dropped. Kept: the three changes in data
access and default behaviour — Kp history now from the GFZ web service, Dst from WDC Kyoto's HAPI server,
and the default MIDL propagation target of 14 Earth radii (`target` is the distance along the Sun–Earth
line at which MIDL returns propagated solar wind, `swvo/io/solar_wind/midl.py:82-97`). Dropped: "Use
hugging face to store test data" (test housekeeping) and the "Full Changelog" compare link (a pointer).

**PID.** No Zenodo or other deposit of SWVO's code exists (Field 2), so no version DOI exists.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

A pure-Python package (rule 4): the tracked tree holds 100 `.py` files and no compiled source;
`requires-python = ">=3.11"` (`pyproject.toml:16`) with classifiers for Python 3.11–3.14
(`pyproject.toml:20-24`), and CI tests 3.11–3.14 (`.github/workflows/tests.yml`). Excluded: the one shell
script `download_data_for_tests.sh` (test-data tooling, rule 4); the Apptainer definition and YAML
workflows (build tooling); the Jupyter notebook `docs/examples/solar_wind_example.ipynb` (a Python kernel
document, not a language). GitHub's language statistics (Python, Shell) agree once the test script is set
aside. No Python 2 targeting anywhere (rule 5).

### 14. Reference Publication (OPTIONAL)
Not found

No paper describes SWVO (rule 7). `CITATION.cff` has no `preferred-citation` and asks users to cite the
software itself; the README and docs have no citing section and no JOSS badge. Literature search: ADS
full text for `"SWVO"` returns only unrelated records that use the string, `"GFZ/SWVO"` and
`"swvo.readthedocs"` return nothing (control: `"EL_PASO" OR "EL-PASO"` finds the 2026 COSPAR EL-PASO
abstract; a nonsense token returns zero); OpenAlex and Crossref title searches find only the SWVO Test
Data deposit. The project's own talk slides (2026-10-26 PyHC telecon) and the authors' 2026 EGU abstract
on data-assimilative plasmasphere/ring-current/radiation-belt validation are a talk and a meeting
abstract, never this field (rule 2).

### 15. License (RECOMMENDED)
Apache License 2.0

The licence file is `LICENSES/Apache-2.0.txt` (REUSE layout; first lines "Apache License / Version 2.0,
January 2004"), `pyproject.toml:17-18` declares `license = "Apache-2.0"` and that licence file, every
tracked source carries `SPDX-License-Identifier: Apache-2.0`, `CITATION.cff:12` says `Apache-2.0`, and
PyPI's `license_expression` is `Apache-2.0` (rules 1 and 3). The file was added 2025-06-25 (`56a5b8a`,
"add licenses to all the code files") and has not changed. GitHub's API reports no licence because there
is no LICENSE file at the repository root, only under `LICENSES/` — a detection gap, not a licensing fact.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- pyhc package
- space weather
- geomagnetic index
- kp index
- dst index
- hp30
- hp60
- sym-h
- f10.7
- auroral electrojet
- substorm onset
- plasmasphere
- enlil

The project declares no keywords (none in `pyproject.toml` or `CITATION.cff`, no GitHub topics).

- **`pyhc package`** — rule 15: SWVO is listed in the PyHC registry (`_data/projects.yml`, entry
  `name: "SWVO"`, at `b1e3c97`).
- **Domain terms a searcher would type (rule 10)**, each evidenced in the code or the project's text:
  `space weather` (the project's own framing, `CITATION.cff` abstract; the description writes it
  hyphenated, so a search for the unhyphenated phrase needs the keyword); `geomagnetic index` (the
  project's "geomagnetic indices", matched to the singular row the catalogue already had rather than a
  new plural, rule 11); `kp index`, `dst index`, `f10.7` and `auroral electrojet` (the Kp, Dst, F10.7 and
  SuperMAG electrojet readers); `enlil` (the WSA-Enlil readers, `swvo/io/solar_wind/enlil.py`; no other
  field carries the model's name). Each matched a keyword row the catalogue already had.
- **New terms (rule 12)**, lower-case; before SWVO's submission none had a keyword row in any case,
  separator or plural variant:
  `hp30` and `hp60` (GFZ's Hp30/Hp60 indices, `swvo/io/hp/`), `sym-h` (`swvo/io/symh/omni.py`,
  `SymhOMNI`), `substorm onset` (`swvo/io/substorms/`, the SuperMAG onset catalogues; a search for
  "substorm" also reaches it) and `plasmasphere` (`swvo/io/plasmasphere/`).

Not added. From the PyHC registry entry's keyword list: `general` (scope tag, rule 2);
`heliosphere`, `magnetosphere`, `solar`, `ionosphere_thermosphere_mesosphere`, `plasma_physics` (registry
domain tags; the domains SWVO does touch are carried by Field 5, and plasma physics is not what it does —
rules 3 and 6); `data_access`, `data_retrieval` (Field 4); `csv`, `netcdf`, `ascii` (Field 18);
`coordinates` (Field 4); `time`, `remote`, `local`, `web_service`, `reference_data` (registry facet
vocabulary that tells a searcher nothing about SWVO, rules 3 and 7); `ace`, `dscovr`, `omni` (Fields 31,
32 and 17). Also declined: `solar wind` and `geomagnetic storms` (Fields 5 and 22), `supermag` (Field 32),
`kyoto dst` and `omniweb` (Field 17), and `space weather forecasting` / `geomagnetic forecasting` —
Field 4's `Models and Simulations: Forecasting` carries that capability (rule 6).

### 17. Data Sources (OPTIONAL)
- GFZ
- WDC
- HAPI
- OMNIWeb
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- Other

Every row is reached by code in the distribution (rule 2):

- **GFZ** — the GFZ Kp/Hp web service `https://kp.gfz.de/app/json/` (definitive Kp history in
  `KpNiemegk`, Hp30/Hp60 in `HpGFZ`) and the Niemegk Kp nowcast file under
  `https://kp.gfz.de/fileadmin/files_for_gfz_cms/` (`swvo/io/kp/niemegk.py:50-53`, `swvo/io/hp/gfz.py:55`).
- **WDC** and **HAPI** — `DSTWDC` queries the World Data Center for Geomagnetism, Kyoto through its HAPI
  server (`https://wdc.kugi.kyoto-u.ac.jp/hapi/`, `info?id=hour_dst` and `data?id=hour_dst&format=csv`,
  `swvo/io/dst/wdc.py:48-50,127,142`). Both rows apply: WDC is the service, HAPI the access protocol the
  client speaks (rule 7).
- **OMNIWeb** — `OMNIHighRes` (and `SWOMNI`, `SymhOMNI`) post requests to the OMNIWeb CGI
  `https://omniweb.gsfc.nasa.gov/cgi/nx1.cgi` (`swvo/io/omni/omni_high_res.py:54,586-593`).
- **HTTP/HTTPS Directories** — plain directory trees whose files the code builds paths under and
  downloads: SPDF's `https://spdf.gsfc.nasa.gov/pub/data/omni/low_res_omni/` (`omni2_<year>.dat`,
  `swvo/io/omni/omni_low_res.py:52,131`), NOAA SWPC's `https://services.swpc.noaa.gov/text/`
  (`3-day-forecast.txt`, `daily-solar-indices.txt`) and the GFZ nowcast file directory (rule 9).
- **Observatory/Mission-specific** — readers of one mission's or network's own products: ACE real-time
  MAG and SWEPAM files (`https://sohoftp.nascom.nasa.gov/sdb/goes/ace/daily/`), DSCOVR PlasMag 1-minute
  data from the NCEI space-weather portal values API, IMAP I-ALiRT MAG and SWAPI data
  (`https://ialirt.imap-mission.com/space-weather`), and the SuperMAG indices and substorm services
  (`swvo/io/sme/supermag.py:61`, `swvo/io/substorms/supermag.py:63`). The observatories and instruments
  are named in Fields 31/32 (rule 8); IMAP had no SPASE row when this record was prepared, which does not
  undo this value (Field 32 rule 6).
- **Other** — real sources with no row (rule 10): the British Geological Survey Kp forecast
  (`https://geomag.bgs.ac.uk/cgi-bin/solar`, `swvo/io/kp/bgs.py:50`), the SIDC/ESA space-situational
  awareness Kp forecast API (`https://ssa.sidc.be/prod/API/index.php`, `swvo/io/kp/sidc.py:50`), and the
  NOAA NCEI space-weather portal files API for WSA-Enlil model runs
  (`https://www.ncei.noaa.gov/cloud-access/space-weather-portal/api/v1/files`,
  `swvo/io/solar_wind/enlil.py:129`).

Not counted: **MIDL** — `SWMIDL` delegates the download to the `csem-midl` client library
(`midl_client.load`, `swvo/io/solar_wind/midl.py:239`), so the MIDL server is that library's retrieval
routine, not SWVO's (rule 4); the relation is recorded in Field 30. The **PAGER forecast readers**
(Kp/Hp ensembles, SWIFT, plasmasphere) read local files the user supplies (rule 11). No FTP access exists
anywhere (every endpoint is `https://`). `CDAWeb`, `AMDA`, `das2`, `Madrigal`, `SSCWeb`, `TAP`, `VirES`,
`S3/Cloud-aware` and `The Virtual Solar Observatory.` — no client for any of them.

### 18. Input File Formats (RECOMMENDED)
- ascii
- csv
- JSON
- netCDF3/4

Each format is read by a reader in the installed package (rule 5):

- **ascii** — whitespace-delimited text tables: the ACE real-time `*_ace_mag_1m.txt` and
  `*_ace_swepam_1m.txt` files (`pd.read_csv(..., sep=r"\s+")`, `swvo/io/solar_wind/ace.py:408-415,467`),
  SPDF's `omni2_<year>.dat` (`swvo/io/omni/omni_low_res.py:205`), SWPC's `daily-solar-indices.txt`
  (`swvo/io/f10_7/swpc.py:186-192`) and `3-day-forecast.txt`, and the GFZ `Kp_ap_nowcast.txt`
  (`swvo/io/kp/niemegk.py:372`).
- **csv** — the PAGER forecast files the user supplies: Kp and Hp ensemble members
  (`swvo/io/kp/ensemble.py:143`, `swvo/io/hp/ensemble.py:143`) and the plasmasphere prediction and
  combined-input files (`swvo/io/plasmasphere/read_plasmasphere.py:229`,
  `read_plasmasphere_combined_inputs.py:85-89`).
- **JSON** — SWIFT ensemble files the user supplies (`gsm_*.json`, `json.load`,
  `swvo/io/solar_wind/swift.py:164,204-205`), and downloaded JSON saved and parsed from the DSCOVR portal
  (`swvo/io/solar_wind/dscovr.py:356-357`), the GFZ Hp API (`swvo/io/hp/gfz.py:321`) and the SIDC API
  (`swvo/io/kp/sidc.py:303`).
- **netCDF3/4** — WSA-Enlil run files extracted from NCEI tar archives and opened with
  `xarray.open_dataset` (`swvo/io/solar_wind/enlil.py:451-452,574`).

Excluded: the processed CSV files each reader writes and reads back (its own cache, rule 4 — `csv` is
recorded on the PAGER files' evidence, not on this); the BGS forecast page, saved as `kp.html` and
scraped with BeautifulSoup (`swvo/io/kp/bgs.py:100,303`) — a web page, not a data file format a user
holds; MATLAB `.mat` and Python `.pickle` RBM files, read only by the deprecated `RBMDataSet` (scope note
4); the WDC HAPI CSV and the IMAP and SuperMAG JSON responses, which are parsed in memory and never form
a file. `CDF`, `FITS`, `HDF5`, `IDL.sav`, `ISTP-Compliant` and `Zarr` — no reader.

### 19. Output File Formats (RECOMMENDED)
Not found

Evidenced empty (rule 9). The public API returns pandas DataFrames (lists of them for ensembles) and a
`PlasmasphereDensityCube` container; the save format is the caller's choice (rule 5). The write paths
in the package, found by searching for `to_csv|to_netcdf|json.dump|.write(|savefig` and read one by one:
the daily and monthly CSV files every `download_and_process` writes (`swvo/io/solar_wind/ace.py:351`,
`swvo/io/omni/omni_high_res.py:223`, and the other readers) persist processed inputs that `read()` loads
back, which is Field 18 evidence, not an output product (rule 2); the raw downloads written to temporary
directories (`f.write(response.content)`, `json.dump` in `swvo/io/hp/gfz.py:183`) and the log files of
`swvo/logger.py` are bookkeeping (rule 3). The only figure code is in the deprecated `RBMDataSet`
(scope note 4). A positive control on the same scope — the read-side search — matches the readers listed
in Field 18.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac

The project names its supported systems itself: `Operating System :: POSIX`, `Operating System :: Unix`
and `Operating System :: MacOS` (`pyproject.toml:25-27`), unchanged since the file was added
(`05a8893`, 2025-06-25). CI runs on `ubuntu-latest` (`.github/workflows/tests.yml`) and the published
Apptainer image is Debian-based (`swvo.def`, `From: astral/uv:python3.12-bookworm-slim`), which gives
`Linux`; the MacOS classifier gives `Mac`. `Operating System Independent` is not recorded: although the
package is pure Python, the project deliberately lists specific systems instead of `OS Independent`, and
that choice is a declared scope rather than an absence of restriction (rule 3 applies to packages that
declare none). `Windows` is not recorded: no classifier, document or CI job names it (rule 7).

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Pure Python with no compiled extension and no architecture-specific dependency built by the project; the
only wheel is `py3-none-any` (rule 3). No GPU or cluster code (rules 6–7).

### 22. Related Phenomena (OPTIONAL)
- Geomagnetic Storms
- Solar Wind
- Coronal Mass Ejections

Kept under rule 5:

- **Geomagnetic Storms.** The package exists to deliver and process the storm diagnostics — Dst and
  SYM-H (ring-current intensity), Kp and Hp30/Hp60 — and the README says so: Kp is "Used to assess
  geomagnetic storm conditions" and Dst is "related to geomagnetic storms … negative during storm
  conditions". The inferential step: processing a phenomenon's defining measurements is primary-function
  support. These indices are SWVO's products, not parameters of another model, so rule 6 does not fire.
- **Solar Wind.** The solar-wind readers process the phenomenon's defining measurements (plasma speed,
  density, temperature and magnetic field from ACE, DSCOVR, IMAP and OMNI), derive dynamic pressure and
  propagate the flow to the bow shock. Decided separately from Field 5's `Solar Wind` row (rule 8).
- **Coronal Mass Ejections.** SWVO has a dedicated reader for NOAA SWPC's WSA-Enlil CME simulation runs
  (`SWENLIL_CME`, `swvo/io/solar_wind/enlil.py:754-815`), which the README lists as "CME simulation
  runs". It finds each day's CME runs (zero, one or several, each at its own run time), extracts each
  run's modelled solar wind at Earth, converts its field to GSM and returns one DataFrame per CME run;
  `read_solar_wind_from_multiple_models` lets the latest CME run carry the forecast once SWIFT runs out,
  and makes the CME runs the ensemble when SWIFT supplies none. The inferential step: processing
  simulations of CMEs arriving at Earth, through code written for CME runs, is primary-function
  support for the phenomenon (rule 5). Rule 2 does not fire: the link is SWVO's own CME-specific code,
  not the reach of a wrapped library. The modelling itself is WSA-Enlil's; SWVO is the reader.

Rejected: **Solar Flares**, **X-ray emission**, **Coronal Heating**, **Solar Corona** — no code; F10.7 is
a radio index treated as a generic activity proxy, not X-ray or coronal analysis (rules 4 and 6).
Substorms have no row (their keyword is in Field 16).

### 23. Development Status (RECOMMENDED)
Active

No successor pointer, archive flag, repostatus badge or status statement (rules 1–4). The software has
stable releases on PyPI (1.0.0 through 1.2.9). The last commit on the default branch `main` is
`1d95887` dated 2026-10-30, and the latest release 1.2.9 is dated 2026-10-16 — both within six months
of the 2026-11-03 extraction (rule 6).

### 24. Documentation (RECOMMENDED)
https://swvo.readthedocs.io/en/latest/

The project's own Sphinx site (rule 3), named in `pyproject.toml:57` (`Documentation`), `CITATION.cff:14`
(`url`), the README's Read the Docs badge, the GitHub repository `homepage`, PyPI's `project_urls` and the
PyHC registry `docs:`, and built from `.readthedocs.yaml` and `docs/conf.py` in the pinned tree. It
serves this package's documentation (page title "Welcome to swvo documentation! — swvo 1.2.9
documentation") and carries
the README's installation section plus the API reference, the solar-wind example notebook, the
changelog and pages on OMNI variables, SuperMAG indices and substorm catalogues. `/en/latest/` is the
landing form the project itself uses (rule 6). No wiki exists: the wiki repository
`https://github.com/GFZ/SWVO.wiki.git` does not exist (the API's `has_wiki: false` alone would prove
nothing).

### 25. Funder (OPTIONAL)
Not found

No source attributes funding to SWVO or to a project whose product SWVO is (rule 12). The sweep: the
tracked tree (excluding `uv.lock` and the licence text) searched case-insensitively with PCRE word
boundaries for `fund`, `grant`, `award`, `sponsor`, `horizon`, `acknowledg`, `DFG`, `ERC`, `BMBF`,
`DLR`, `Helmholtz Association`, `H2020` and `grant agreement` finds only the data-use
acknowledgement guidance in `docs/omni_variables.rst:235-243`, `docs/supermag_indices.rst:161-170` and
`docs/supermag_substorms.rst:241-271` (how to acknowledge OMNI and SuperMAG data) and an unrelated
`read_with_horizon` method (`swvo/io/hp/ensemble.py:209`); positive control: `SuperMAG` matches in all
three docs pages. `CITATION.cff` has no funding block, there is no software DOI record, no paper
describes SWVO (Field 14), and the project's talk slides end with contacts and the repository link, not an
acknowledgement. Rejected candidates and their actual roles:

- **GFZ Helmholtz Centre for Geosciences** — the authors' employer and the copyright holder
  (`reuseify.toml`); an employer is not a funder of the software (rule 6).
- **The PAGER project** (`spacepager.eu`) — produces the SWIFT, Kp/Hp ensemble and plasmasphere forecasts
  that SWVO's local-file readers consume; its funding pays for an input (rule 5).
- **NASA (SPDF/OMNI), NOAA (SWPC, NCEI), SuperMAG, WDC Kyoto, BGS, SIDC** — operators of the data services
  SWVO reads; input funding (rule 5).

### 26. Award Title (OPTIONAL)
Not found

No qualifying source names an award (rule 8); the sweep and rejected candidates are those of Field 25.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

No developers' publication about SWVO exists (Field 14), and the project names no paper as the basis of
its code (rule 4). Weighed:

- **The SuperMAG catalogue and index papers** — Newell and Gjerloev (2011,
  https://doi.org/10.1029/2011JA016779), Forsyth et al. (2015, https://doi.org/10.1002/2015JA021343),
  Ohtani and Gjerloev (2020, https://doi.org/10.1029/2020JA027902), Frey et al. (2004,
  https://doi.org/10.1029/2004JA010607), Liou (2010, https://doi.org/10.1029/2010JA015578) and the SME/SML/SMU
  index paper (https://doi.org/10.1029/2011JA016936). The docs and `swvo/io/substorms/catalogs.py` cite
  them as the references SuperMAG asks users of each *data product* to cite; SWVO implements none of
  these methods, it downloads their results. They are data citations, not the basis of the software, so
  rule 4 does not admit them and they are mentions under rule 6.
- **Meeting abstracts** — the 2026 EGU abstract "Validation of Data-assimilative Plasmasphere, Ring
  Current, and Radiation Belts Simulations Powered by the Open-Source Data Processing …"
  (https://doi.org/10.5194/egusphere-egu26-6291, listed among Jhawar's ORCID works) and the 2026 COSPAR
  EL-PASO abstract (ADS `2026cosp...46.3292H`) are never eligible (rule 1).
- **The PyHC telecon slides** (2026-10-26, `https://sahiljhawar.in/swvo-pyhc/`, embedded by
  `docs/presentation.rst`) — a single-page slide app on a personal domain with no DOI and no permanent
  landing page (rule 1); its slides are headings, short bullets and code snippets.
- **The EL-PASO preprint** — Haas, Drozdov and Jhawar, "EL-PASO: An Open-Source Python Library for
  Processing and Standardizing Particle Measurements Taken in Space", ESS Open Archive: v1
  https://doi.org/10.22541/essoar.15002644/v1 (posted 2026-05-02) and v2
  https://doi.org/10.22541/essoar.15002644/v2 (12 August 2026); Haas's ORCID lists both versions.
  Weighed under rule 5 because EL-PASO's code is built on SWVO (Field 30). The v2 full text never names
  SWVO: its Open Research section credits the Van Allen Probes RBSP-ECT data, OMNIWeb, EL-PASO and IRBEM;
  its Acknowledgments credit RBSP-ECT, IRBEM and the funders of that work; and its methods attribute the
  solar-wind parameters to "the OMNI database, which is used in this work to retrieve solar wind
  parameters at the bow shock". The v1 landing page's abstract and data-availability statement do not
  name SWVO either. Rule 5 needs the paper itself to credit the software, so it is not added; recorded so
  a later refresh does not reopen it.

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.48322/1shr-ht18
- https://doi.org/10.48322/45bb-8792
- https://doi.org/10.48322/gbpg-5r77
- https://doi.org/10.5880/Kp.0001
- https://doi.org/10.5880/Hpo.0003
- https://doi.org/10.17593/14515-74000
- https://doi.org/10.7289/v51z42f7
- https://doi.org/10.7289/v5445jgh
- https://sohoftp.nascom.nasa.gov/sdb/goes/ace/daily/
- https://services.swpc.noaa.gov/text/
- https://supermag.jhuapl.edu/indices/
- https://supermag.jhuapl.edu/products/
- https://csem.engin.umich.edu/MIDL/

Every dataset SWVO has a dedicated reader for (rule 3), each mapped to its reader:

| Entry | Dataset | Reader(s) |
|---|---|---|
| `10.48322/1shr-ht18` | OMNI Hourly Data Set (NASA SPDF; its SPASE record lists `https://spdf.gsfc.nasa.gov/pub/data/omni/low_res_omni/`, the exact directory the code reads) | `OMNILowRes`, `KpOMNI`, `DSTOMNI`, `F107OMNI` |
| `10.48322/45bb-8792` | OMNI 1-min Data Set (High Resolution OMNI, Version 1; its SPASE record lists the OMNIWeb high-resolution service the code queries with `spacecraft=omni_min`) | `OMNIHighRes` (cadence 1), `SWOMNI`, `SymhOMNI` |
| `10.48322/gbpg-5r77` | OMNI 5-min Data Set (Version 1; `spacecraft=omni_5min`) | `OMNIHighRes` (cadence 5) |
| `10.5880/Kp.0001` | Geomagnetic Kp index (GFZ Data Services) | `KpNiemegk` / `KpGFZ` |
| `10.5880/Hpo.0003` | Geomagnetic Hpo index (V3.0) (GFZ Data Services) — Hp30 and Hp60 | `HpGFZ`, `Hp30GFZ`, `Hp60GFZ` |
| `10.17593/14515-74000` | Dst Index (WDC for Geomagnetism, Kyoto; HAPI dataset `hour_dst`) | `DSTWDC` |
| `10.7289/v51z42f7` | Deep Space Climate Observatory (DSCOVR) (NOAA NCEI; PlasMag magnetometer and Faraday cup) | `DSCOVR` |
| `10.7289/v5445jgh` | Wang-Sheeley-Arge (WSA)-Enlil Solar Wind Prediction (NOAA NCEI) | `SWENLIL_BKG`, `SWENLIL_CME` |
| `sohoftp…/ace/daily/` | ACE real-time 1-minute MAG and SWEPAM daily files (no DOI; the public HTTPS archive root the code reads) | `SWACE` |
| `services.swpc.noaa.gov/text/` | NOAA SWPC text products `3-day-forecast.txt` (Kp forecast) and `daily-solar-indices.txt` (F10.7) (no DOI; archive root the code reads) | `KpSWPC`, `F107SWPC` |
| `supermag.jhuapl.edu/indices/` | SuperMAG SME/SML/SMU electrojet indices (no DOI; the data centre's indices page, which the docs link) | `SMESuperMAG` |
| `supermag.jhuapl.edu/products/` | SuperMAG substorm-onset lists (Newell, SOPHIE, Ohtani, Frey, Liou) (no DOI; the data centre's products page, which the docs link) | `SubstormsSuperMAG` |
| `csem.engin.umich.edu/MIDL/` | MIDL, Merged Interplanetary Data from L1 (University of Michigan CSEM; no dataset DOI) | `SWMIDL` |

Rule 6: the Hpo index is published as linked release DOIs (`Hpo.0001` → `.0002` → `.0003`, joined by
`IsNewVersionOf`/`IsPreviousVersionOf`) with no series DOI, so the newest release, V3.0, is recorded; a
later refresh moves it forward if GFZ publishes a newer one. The Kp index has a single DOI. The OMNI,
Kp, Hpo and Dst DOIs resolved to their landing pages on 2026-11-03; the two NOAA NCEI DOIs are registered at DataCite
(publisher NOAA National Centers for Environmental Information), whose records describe DSCOVR's PlasMag
suite and the SWPC WSA-Enlil prediction archive.

Considered and excluded:

- **SWVO Test Data** (https://doi.org/10.5281/zenodo.22983305; the Hugging Face copy `spsw/SWVO-Test-Data`
  that `download_data_for_tests.sh` fetches) — the test suite's fixture archive, not a data product SWVO
  is built to read for users nor a data release made with it (rules 3–5).
- **OMNI High Resolution Version 2** (`10.48322/mj0k-fq60`, `10.48322/hkaw-ff03`) — the Version 2 SPASE
  records list CDAWeb and SPDF `hro2_*` access, while OMNIWeb's high-resolution service, which SWVO
  queries, is listed on the Version 1 records (rule 2).
- **SuperMAG Lower Index Onsets List** (`10.48322/v3c2-4a19`, McPherron) — a different onset catalogue
  that SWVO does not read (rule 2).
- **Hpo V1 and V2** (`10.5880/Hpo.0001`, `.0002`) — superseded releases (rule 6).
- **NOAA WSA-Enlil on the AWS Registry of Open Data** (`10.60489/roda.zs4psu`) — another distribution of
  the Enlil runs; SWVO reads NCEI's.
- **IMAP I-ALiRT real-time data** — no DOI and no landing page; the only URL is the JSON API endpoint
  `https://ialirt.imap-mission.com/space-weather`, a query interface (rule 8 and *Form of each entry*).
- **SIDC and BGS Kp forecasts** — reachable only as an API query and a CGI form (rule 8).
- **PAGER forecast products** (Kp/Hp ensembles, SWIFT, plasmasphere) — read from local files; no
  published dataset or DOI found (DataCite searches for PAGER and SWIFT datasets return nothing relevant).

### 29. Related Software (OPTIONAL)
- https://github.com/GFZ/EL_PASO

**EL_PASO — a sister implementation split out of this repository (rule 9).** SWVO's own deprecation
notices say that RBM dataset handling now lives in, and has moved to, EL_PASO (quoted in scope note 4:
`swvo/io/RBMDataSet/__init__.py:7-11`, `swvo/io/RBMDataSet/RBMDataSet.py:61-65`), and EL_PASO carries the
successor code (its `el_paso/dataset/` module and the same `create_RBSP_line_data` script SWVO still
ships as `swvo/io/RBMDataSet/scripts/create_RBSP_line_data.py`). EL_PASO's package metadata names
Bernhard Haas, SWVO's first-listed author, as its author. The upstream repository root is recorded (rule
12a): EL_PASO had no HSSI entry when SWVO was submitted. Its Zenodo concept DOI,
`10.5281/zenodo.20760790`, was passed over because the site shows the raw URL as link text (rule 13).

Considered and excluded: **sunpy** and **astropy** — used inside one reader for one frame conversion
(`swvo/io/solar_wind/enlil.py:20-28`); they do not characterise SWVO (rules 1–2; astropy is Tier B with
no exchange);
**xarray**, **netCDF4**, **mat73**, **scipy**, **numpy**, **pandas**, **matplotlib**, **requests**,
**beautifulsoup4**, **wget**, **tqdm**, **rich**, **richpool**, **icecream**, **distance**,
**python-dateutil** — Tier A or generic infrastructure (rule 1); **csem-midl** — a single-service client
library, whose relation is the exchange recorded in Field 30 (rules 3 and 5); **reuseify** — Sahil
Jhawar's REUSE-compliance tool, a development dependency; similar-purpose PyHC tools — the project names
no alternatives (rule 9); GFZ's downstream forecast systems named on the project's slides (KpML, PINE,
radiation-belt and ring-current forecasts) — no public code of theirs imports SWVO (a GitHub code
search on 2026-11-03 for `import swvo` and `from swvo` outside this repository found, apart from unrelated string
matches such as `swvox`, only EL_PASO and the PyHC environment's import test).

### 30. Interoperable Software (OPTIONAL)
- https://github.com/GFZ/EL_PASO
- https://github.com/connordimarco/CSEM-MIDL

- **EL_PASO — the consumer side (rule 7).** EL_PASO declares `swvo>=1.2.7rc0` as a dependency and its
  `el_paso/load_indices_solar_wind_parameters.py` imports `swvo.io` and builds its geomagnetic-index and
  solar-wind inputs from SWVO's output: Kp through `swvo_io.kp.read_kp_from_multiple_models` with
  `KpOMNI` and `KpNiemegk`, Dst through `swvo_io.dst.DSTOMNI`, and solar wind through
  `swvo_io.solar_wind.SWOMNI`. This ground is independent of Field 29's (the split-out RBM code), so the
  package is listed in both fields (rule 9).
- **CSEM-MIDL (`csem-midl`) — an adapter around a named domain tool (rule 7).** `SWMIDL` calls the official
  MIDL client `midl.load` and adapts the `xarray` dataset it returns to SWVO's solar-wind schema
  (`swvo/io/solar_wind/midl.py:36-38,239,345`), and `csem-midl>=1.1.2` is a declared dependency
  (`pyproject.toml`). The repository is the one PyPI's `project_urls` name. Its Zenodo concept DOI,
  `10.5281/zenodo.19739785`, was passed over because the site shows the raw URL (Field 29 rule 13).

Excluded: the **PyHC environment** (`heliophysicsPy/pyhc-docker-environment`) — it only imports `swvo` in
an import test, which is shared-environment membership, not an exchange (rule 3); the Tier A and generic
dependencies listed under Field 29 (rules 1–2); **xarray** — SWVO's public API returns pandas DataFrames
and uses xarray only internally (rule 4).

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** ACE Magnetic Field Instrument
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ACE/MAG
- **Instrument Name:** ACE Solar Wind Electron, Proton and Alpha Monitor
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ACE/SWEPAM
- **Instrument Name:** DSCOVR PlasMag Fluxgate Magnetometer
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/DSCOVR/PlasMag/FluxgateMagnetometer
- **Instrument Name:** DSCOVR PlasMag Faraday Cup
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/DSCOVR/PlasMag/FaradayCup

Names are the matched rows' `name` values, quoted from the vocabulary; each identifier resolves to
exactly one row (rule 17). Designed-to-support evidence (rule 6): `SWACE` parses the ACE real-time
`*_ace_mag_1m.txt` and `*_ace_swepam_1m.txt` files separately (`_process_mag_file`,
`_process_swepam_file`, `swvo/io/solar_wind/ace.py:52-53,380-494`); `DSCOVR` reads the NCEI portal's
`m1m_dscovr.*` (magnetometer) and `f1m_dscovr.*` (Faraday cup) parameters
(`swvo/io/solar_wind/dscovr.py:54-66,390-396`). Both instruments and their platforms are genuinely
supported (Field 31 rule 7), so Field 32 carries the observatories too. The SMWG rows were chosen over
their CNES/CDPP-AMDA twins by the SMWG tie-breaker (rule 15): `…/CNES/Instrument/CDPP-AMDA/ACE/MAG`
("Magnetic Field Instrument"), `…/CDPP-AMDA/ACE/SWEPAM`, `…/CDPP-AMDA/DSCOVR/MAG` ("Fluxgate
Magnetometer") and `…/CDPP-AMDA/DSCOVR/FC` ("PlasmaProbe").

Note: **IMAP MAG and SWAPI** (read by `SWIMAP` from the I-ALiRT API, `swvo/io/solar_wind/imap.py:47-48`)
are genuinely supported but omitted (rule 21): the vocabulary held no row for either instrument or for
the IMAP observatory when this record was prepared (2026-11-03), so no substitution is possible (rule
20). Sweep: the name, abbreviation, identifier and definition columns for the token `IMAP`, for
"Interstellar Mapping", `SWAPI` and `I-ALiRT`; the only `IMAP` hits are Interball spacecraft rows
(`IMAP-3` magnetometers on Interball-2 and Interball-Auroral, an Interball-1 ion instrument). Controls:
`SUVI` returns the four GOES SUVI rows; a nonsense token returns none. A later refresh should re-check
once IMAP enters the vocabulary.

Note: **SuperMAG Magnetometers** (`…/SMWG/Instrument/SuperMAG/Magnetometers`) — SWVO reads the network's
derived indices and event lists, not magnetometer data, so the network is recorded at the observatory
level only (rule 7). **IMAGE FUV** (`…/SMWG/Instrument/IMAGE/FUV`) and **Polar UVI** — the Frey and Liou
onset lists were derived from their images, but SWVO reads the SuperMAG-hosted lists and no IMAGE or
Polar data product (rule 3). **Wind** and **SOHO** instruments — reached only through the merged MIDL
product, read via `csem-midl` (rule 5).

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Advanced Composition Explorer
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ACE
- **Observatory Name:** Deep Space Climate Observatory, DSCOVR
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/DSCOVR
- **Observatory Name:** SuperMAG
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SuperMAG

Names quoted from the rows; one row per identifier. **ACE** and **DSCOVR**: the `SWACE` and `DSCOVR`
readers read each spacecraft's real-time solar-wind products as a whole (Field 32 rule 1); the CNES twins
`…/CNES/Observatory/CDPP-AMDA/ACE` ("Advanced Composition Explorer, NASA") and
`…/CNES/Observatory/CDPP-AMDA/DSCOVR` ("Deep Space Climate Observatory") are the same observatories and
were not recorded (rule 4). **SuperMAG**: a ground-magnetometer network ("a collaboration of more than 200
ground geomagnetic observatories coordinated by JHU/APL", its row definition) whose own services SWVO
queries for the SME/SML/SMU indices and the substorm-onset lists (`swvo/io/sme/supermag.py:61`,
`swvo/io/substorms/supermag.py:63`) — a ground network is a platform (rule 1). Field 17 carries
`Observatory/Mission-specific` for all three (rule 6).

Note: **IMAP** had no observatory row (sweep in Field 31) and is omitted (Field 31 rule 21).
**Dominion Radio Astrophysical Observatory** (`…/SMWG/Observatory/DRAO`) — F10.7 is DRAO's measurement,
but SWVO reads it from SWPC and OMNI as a generic activity index and never touches DRAO's archive (rule
2). **Niemegk** (`…/SMWG/Observatory/WDC/Niemegk`, `…/SMWG/Observatory/Ground/Niemegk`,
`…/SMWG/Observatory/IAGA/Niemegk`, `…/IUGONET/Observatory/WDC_Kyoto/WDC/NGK`) — `KpNiemegk` is named for
GFZ's Kp service at Niemegk and reads the planetary Kp index, not the observatory's magnetometer data
(rule 3). **IMAGE** (`…/SMWG/Observatory/IMAGE`) and **Polar** — see Field 31. **OMNI** is a multi-source
data product carried by Field 17, not an observatory (Field 31 rule 1).

### 33. Logo (OPTIONAL)
Not found

A documented omission (rule 6). Every source checked: the tracked tree contains no image file (no
`.png`, `.jpg`, `.jpeg`, `.svg`, `.gif`, `.ico` or `.webp`, and no file named for a logo); `docs/conf.py`
sets no `html_logo` and passes no logo to the `pydata_sphinx_theme` (`docs/conf.py:98-101`), and the
`_static` directory it references is not tracked; the README's only images are six status badges; the
PyHC registry entry has no `logo:`; the rendered documentation shows only those README badges.
