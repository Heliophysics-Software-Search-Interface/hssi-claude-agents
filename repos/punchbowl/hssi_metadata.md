# HSSI Metadata Extraction Results

**HSSI Software ID:** 37a18000-2d1f-41db-afe6-6545f817bcb7
**Repository:** https://github.com/punch-mission/punchbowl
**Source Revision:** 527b32adf325ab23367925516117df67f4bf717f
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Submitter information is not published in the HSSI software view, so there is no recorded value to carry forward; the actual submitter supplies it.*

---

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.14029123

*Source: existing HSSI record; confirmed as the Zenodo **concept** DOI — `https://zenodo.org/api/records/21640289` reports `"conceptdoi": "10.5281/zenodo.14029123"`. Also carried in `CITATION.cff` (`doi: 10.5281/zenodo.14029123`) and the `README.md` DOI badge (line 3).*

---

### 3. Code Repository (MANDATORY)
https://github.com/punch-mission/punchbowl

*Source: existing HSSI record; confirmed by `git remote -v` (`origin https://github.com/punch-mission/punchbowl.git`), `CITATION.cff` `url:`, `pyproject.toml` `[project.urls] Repository`, and Zenodo `metadata.custom["code:codeRepository"]`.*

---

### 4. Software Functionality (MANDATORY)
*The existing HSSI record carried no software functionality values, so this entire classification is derived from the repository. Every subcategory below is listed together with its required parent category.*

**Coordinate Transforms**
- Coordinate Transforms
  - *Evidence:* `punchbowl/data/wcs.py` is a dedicated WCS/frame-conversion module (`calculate_helio_wcs_from_celestial`, `calculate_celestial_wcs_from_helio`, `hpc_to_gcrs`, `compute_hp_to_eq_rotation_angle`, `celestial_north_from_wcs`, `class GCRSWCS(WCS)`); every PUNCH product carries both a helioprojective and a celestial WCS (`docs/data/access.rst`, "Data Projections").
- Coordinate Transforms:Solar
  - *Evidence:* `punchbowl/data/wcs.py` imports `sunpy.coordinates.frames` and converts between helioprojective and celestial frames; `get_p_angle()` computes the solar P angle; `punchbowl/auto/flows/level0.py:524` transforms to `HeliographicCarrington`; `punchbowl/data/meta.py:21` uses `sunpy.coordinates.sun._sun_north_angle_to_z`.
- Coordinate Transforms:Heliospheric
  - *Evidence:* `punchbowl/auto/flows/level0.py:520-521` — `gcrs.transform_to(HeliocentricInertial(...))` (HCI) and `HeliocentricEarthEcliptic(...)` (HEE); `punchbowl/data/meta.py:1008-1011` places Sun/Moon/Earth into HEE for the FITS headers.
- Coordinate Transforms:Magnetospheric
  - *Evidence:* `punchbowl/auto/flows/level0.py:525-526` — `gcrs.transform_to(GeocentricSolarEcliptic(...))` (GSE) and `GeocentricEarthEquatorial(...)` (GEI); these Earth-centric spacecraft position/velocity vectors are written into the delivered L0 FITS headers (CHANGELOG.rst 0.0.24, PR #964: "Spacecraft positions and velocities are included in FITS headers in several new Earth-centric frames"), so the transform is user-facing.
- Coordinate Transforms:Mission-Specific
  - *Evidence:* per-spacecraft PUNCH instrument frames and distortion models — `punchbowl/level1/alignment.py` (`build_distortion_model`, `solve_pointing`, `filter_distortion_table`), `punchbowl/data/wcs.py` (`load_trefoil_wcs`, `load_quickpunch_mosaic_wcs`, `load_quickpunch_nfi_wcs`), and the PUNCH-specific Stokes symbol mapping `PUNCH_STOKES_MAPPING` in `punchbowl/data/wcs.py:36`.

**Data Processing and Analysis**
- Data Processing and Analysis
- Data Processing and Analysis:Calibration
  - *Evidence:* the package's stated purpose — "`punchbowl` is the science calibration code for the PUNCH mission" (`README.md:5`); `punchbowl/level1/` implements vignetting (`vignette.py`), photometric quartic calibration (`quartic_fit.py`, `photometric_calibration`), PSF correction (`psf.py`), stray light removal (`stray_light.py`, `dynamic_stray_light.py`); `punchbowl/cli.py` `create_calibration()` generates calibration products.
- Data Processing and Analysis:Image Processing
  - *Evidence:* `punchbowl/level1/despike.py`, `destreak.py`, `deficient_pixel.py`, `psf.py`; `punchbowl/level2/resample.py` (`reproject_cube`); `punchbowl/level2/bright_structure.py` (ZSPIKE voting algorithm); `punchbowl/levelq/pca.py`; `punchbowl/level3/stellar.py`; `skimage` imported in 4 modules.
- Data Processing and Analysis:Processing
  - *Evidence:* the L0→L1→L2→L3 and Level-Q segment structure (`docs/intro.rst`, "Where does `punchbowl` fit in?"), realized as `punchbowl/level1/flow.py`, `level2/flow.py`, `level3/flow.py`, `levelq/flow.py`.
- Data Processing and Analysis:Analysis
  - *Evidence:* `punchbowl/level3/velocity.py` derives solar-wind flow (`track_velocity`, `calculate_cross_correlation`, `process_corr`, producing the L3 "VAM" wind-flow product per `docs/data/data_overview.rst`); `punchbowl/level3/f_corona_model.py`; `punchbowl/limits.py` outlier statistics.
- Data Processing and Analysis:Data Access and Retrieval
  - *Evidence:* `punchbowl/data/fido/client.py` defines `PUNCHClient(GenericClient)` — "Fido client for fetching PUNCH data from the SDAC" — with registered attrs in `punchbowl/data/fido/attrs.py`; `punchbowl/data/sample.py` (`download_all`, `_download_sample_data`) fetches sample data; `examples/querying_data.py` demonstrates `Fido.search(...)`/`Fido.fetch(...)`.
- Data Processing and Analysis:Data Reduction
  - *Evidence:* "`punchbowl` is the data reduction pipeline code for the PUNCH mission" (`docs/intro.rst`); `punchbowl/level3/low_noise.py` (`create_low_noise_task`) averages 32 minutes of acquisitions into the PAM/CAM low-noise products (`docs/data/data_overview.rst`, Level 3).
- Data Processing and Analysis:File Format Conversion
  - *Evidence:* raw CCSDS telemetry → FITS ("Raw to *Level 0*: converts raw satellite data to FITS images", `docs/intro.rst`; `punchbowl/auto/flows/level0.py`); FITS → JPEG2000 quicklook (`punchbowl/data/punch_io.py:105` `write_ndcube_to_quicklook`, `glymur.Jp2k`); JPEG2000 → MP4 (`punchbowl/data/punch_io.py:242` `write_quicklook_to_mp4`).
- Data Processing and Analysis:Packet Decommutation
  - *Evidence:* `punchbowl/auto/flows/level0.py:16,24-25` imports `ccsdspy`, `PacketArray`, `PacketField`, `converters`, `split_by_apid`; lines 229/274 build `ccsdspy.FixedLength(fields)` / `ccsdspy.VariableLength(fields)` decommutators; packet definitions loaded from spreadsheets (`pd.read_excel`, line 198) and `scripts/auto/prepare_packet_definition_csv_files.py`.
- Data Processing and Analysis:Time Series Analysis
  - *Evidence:* `punchbowl/level3/f_corona_model.py` (`construct_f_corona_model` fits a background across a time-ordered file series); `punchbowl/level1/dynamic_stray_light.py` (phase/time-window pairing, `make_phases`, `collect_pairs_by_phase`); `punchbowl/level2/bright_structure.py` ZSPIKE *temporal* despiking; `punchbowl/level3/velocity.py:194` `accumulate_cross_correlation_across_frames`; `punchbowl/level3/motion_filter.py` FFT-in-time hourglass velocity filter.
- Data Processing and Analysis:Wave Polarization Analysis
  - *Evidence:* PUNCH is a polarimeter and punchbowl resolves optical (Stokes-like) polarization as a primary function — `punchbowl/data/wcs.py:36` registers custom Stokes symbols `pB`/`B` via `astropy.coordinates.custom_stokes_symbol_mapping`; `punchbowl/level2/polarization.py:37` `solpolpy.resolve(data_collection, outsys)`; `punchbowl/level3/polarization.py` `convert_polarization`; `punchbowl/level3/stellar.py` `polarize_solar_to_celestial` / `polarize_celestial_to_solar`; the quasi-Stokes B/pB/pB′ and M,Z,P tri-polarizer systems are described in `docs/data/data_overview.rst`. **Scope note:** this is *optical/Thomson-scattering* polarimetry (Stokes parameters of light), not plasma-wave polarization. It is included because the subcategory is defined by "Stokes parameters / polarization ellipse", which punchbowl resolves directly as a primary function.
- Data Processing and Analysis:ML/AI
  - *Evidence:* `punchbowl/levelq/pca.py:14` `from sklearn.decomposition import PCA`; `run_pca_filtering` (line 173) fits/transforms/inverse-transforms an unsupervised PCA model to remove background structure from QuickPUNCH images.

**Data Visualization**
- Data Visualization
- Data Visualization:2D Graphics
  - *Evidence:* `punchbowl/data/visualize.py` — `plot_punch` (line 194, `ax.imshow`), `_cmap_punch` custom PUNCH colormap, `radial_filter`, `generate_mzp_to_rgb_map` (line 66); `examples/plotting_data.py`, `examples/create_rgb_map.py`.
- Data Visualization:Movies
  - *Evidence:* `punchbowl/data/visualize.py:135` `animate_punch` ("Create an animation from a sequence of PUNCH data", writes `.mp4`); `punchbowl/data/punch_io.py:242` `write_quicklook_to_mp4`; `punchbowl/auto/flows/visualize.py` schedules daily movies (CHANGELOG 0.0.24, PR #978 "daily movie quicklook scheduling").
- Data Visualization:Line Plots
  - *Evidence:* `punchbowl/limits.py:77` `plt.plot(self.xs, self.ys, ...)` for outlier-limit curves; `punchbowl/level3/velocity.py:434,439` `ax.plot(thetas, signal, "k-")`; `punchbowl/level1/stray_light.py:105-109` skew-Gaussian fit diagnostic plots.
- Data Visualization:Mission-Specific
  - *Evidence:* PUNCH-specific rendering — `plot_punch` labels the WFI/NFI satellites (CHANGELOG 0.0.24, PRs #960/#979), `generate_mzp_to_rgb_map` renders the PUNCH M/Z/P polarization triplet as RGB, `write_ndcube_to_quicklook` produces the mission's JPEG2000 quicklooks with PUNCH XML metadata boxes (`punchbowl/data/punch_io.py:92` `_generate_jp2_xmlbox`).
- Data Visualization:Web-Based
  - *Evidence:* `punchbowl/auto/monitor/app.py` builds a `Dash` application ("PUNCHPipe dashboard", `dash_bootstrap_components`, served via `gunicorn`); `punchbowl/auto/monitor/pages/files.py` renders interactive `plotly.express` figures with live filtering/auto-refresh.

**Mission-related**
- Mission-related
- Mission-related:Science Data Processing
  - *Evidence:* punchbowl is the PUNCH mission's science processing pipeline — "It provides the primary software modules in use by the mission processing pipeline" (HSSI description); `docs/pipeline/` documents every science segment.
- Mission-related:Processing
  - *Evidence:* `punchbowl/auto/flows/level1.py`, `level2.py`, `level3.py`, `levelq.py` run the operational per-level processing flows at the SOC.
- Mission-related:Calibration
  - *Evidence:* `punchbowl/cli.py` `punchbowl create <level> <code> <spacecraft> ...` generates mission calibration products; `scripts/auto/add_real_calibration_to_db.py`, `add_synthetic_psf_to_db.py`, `add_synthetic_vignetting_to_db.py`, `add_synthetic_quartic_to_db.py`.
- Mission-related:Ingest
  - *Evidence:* `punchbowl/auto/flows/level0.py` ingests spacecraft TLM files (`TLMFiles`, `PacketHistory`, `split_by_apid`) into the SOC database and writes L0 FITS.
- Mission-related:Packet Decommutation
  - *Evidence:* as for Data Processing and Analysis:Packet Decommutation — `punchbowl/auto/flows/level0.py` with `ccsdspy`.
- Mission-related:Orchestration
  - *Evidence:* `punchbowl/auto/control/scheduler.py`, `launcher.py`, `processor.py`, `cluster.py`; Prefect `@flow`/`@task` decorators throughout `punchbowl/auto/flows/`; `docs/automation/index.rst` ("This section is about what we used to call 'punchpipe.' It's how the SOC automates file generation on their servers.").
- Mission-related:Monitoring
  - *Evidence:* `punchbowl/auto/monitor/` Dash dashboard; `punchbowl/auto/control/health.py`; `punchbowl/auto/control/cache_nanny.py`; CHANGELOG 0.0.24 PR #839 "Adds host tracking to the health stats".
- Mission-related:Operations
  - *Evidence:* `docs/automation/control/index.rst` and `states.rst` document SOC operational states; `punchbowl/auto/cli.py` exposes the `punchpipe` operations CLI; `scripts/auto/` contains ~24 SOC operations scripts (`productionify.py`, `reprocess_px.py`, `start_watchdog.py`, `reset_db.py`).
- Mission-related:Inventory
  - *Evidence:* `punchbowl/auto/control/db.py` defines the `File`/`Flow` inventory tables; `scripts/auto/get_bad_image_table.py`, `scan_for_duplicates_and_delete.py`, `sync_db_to_files.py`.
- Mission-related:Archive
  - *Evidence:* `punchbowl/auto/control/cleaner.py` manages retention of FITS/JP2 products in the SOC store; `scripts/auto/import_export.py`, `set_file_date.py`, `upgrade_L0_to_v0e.py` / `upgrade_L0_to_v0h.py` manage archived-product versions.
- Mission-related:Distribution/Access
  - *Evidence:* `punchbowl/data/fido/client.py` serves PUNCH data to users from the SDAC; `punchbowl/auto/flows/levelq.py:602` `levelq_upload_core_flow(... bucket_name, aws_profile="noaa-prod")` pushes QuickPUNCH products to NOAA's S3 bucket ("They're produced for NOAA's space weather forecasting infrastructure", `docs/data/data_overview.rst`).
- Mission-related:Instrument Response
  - *Evidence:* PSF transform construction/application (`punchbowl/level1/psf.py` `build_psf_transform`, `generate_projected_psf`, `regularizepsf.ArrayPSFTransform`), vignetting functions (`punchbowl/level1/vignette.py` `generate_vignetting_calibration_wfi` / `_nfi`), quartic photometric response (`punchbowl/level1/quartic_fit.py`), stray-light response maps (`punchbowl/level1/stray_light.py`).
- Mission-related:Observatory/Instrument Models
  - *Evidence:* per-spacecraft instrument models — `load_spacecraft_def` (`punchbowl/data/meta.py`), instrument masks and per-instrument distortion models (`punchbowl/level1/alignment.py` `build_distortion_model`), and separate WFI/NFI calibration generators in `punchbowl/level1/vignette.py`.
- Mission-related:Analysis
  - *Evidence:* mission-level derived-science products generated in operations — `punchbowl/auto/flows/velocity.py` and `punchbowl/level3/velocity.py` produce the L3 VAM solar-wind flow product.
- Mission-related:System Testing
  - *Evidence:* `punchbowl/auto/flows/simulate.py` drives `simpunch.flow.generate_flow` to push synthetic PUNCH data end-to-end through the operational flows; `scripts/auto/generate_batch_of_simpunch.py`; `pyproject.toml` `[tool.pytest.ini_options] markers = ["prefect_test: a test that integrates with Prefect", "regression: a regression test, likely slow"]`.

**Models and Simulations**
- Models and Simulations
- Models and Simulations:Instrument Response
  - *Evidence:* `punchbowl/level1/psf.py` builds and projects PSF models; `punchbowl/level1/initial_uncertainty.py` models detector noise (`dn_to_photons`, `compute_noise`, `compute_uncertainty`); `punchbowl/level1/sqrt.py` models square-root-encoding noise (`noise_pdf`, `mean_b_offset`, `generate_decode_sqrt_table`).
- Models and Simulations:Observatory/Instrument Models
  - *Evidence:* `punchbowl/level1/vignette.py` `generate_vignetting_calibration_wfi/nfi` synthesize per-instrument vignetting models; `scripts/auto/add_synthetic_psf_to_db.py` / `add_synthetic_vignetting_to_db.py` / `add_synthetic_quartic_to_db.py`.
- Models and Simulations:Empirical
  - *Evidence:* `punchbowl/level3/f_corona_model.py` `construct_f_corona_model` builds the F-corona background empirically from the observations; `punchbowl/level3/stellar.py` `generate_starfield_background` builds a starfield model from the data; `punchbowl/level1/stray_light.py` fits skew-Gaussian stray-light models to observed pixel distributions.
- Models and Simulations:Data Guided
  - *Evidence:* every model above is driven entirely by observed PUNCH frames (`construct_f_corona_model(filenames, ...)`, `construct_dynamic_stray_light_model(filepaths, reference_time, ...)`, `build_psf_transform(image_paths, ...)`), i.e. observation-derived rather than prescribed.
- Models and Simulations:Forward-Fitting
  - *Evidence:* `lmfit` `Parameters`/residual minimisation in `punchbowl/level1/alignment_parallel.py:74` `_residual` and `punchbowl/level1/stray_light.py:136` `_resid_skew` / `fit_skew`; `punchbowl/level1/alignment.py` `solve_pointing` iteratively forward-projects a Gaia catalog and minimises star-position residuals; `punchbowl/level1/quartic_fit.py` fits quartic photometric coefficients.
- Models and Simulations:Mission-Specific
  - *Evidence:* all of the above models are PUNCH-specific (WFI/NFI PSFs, PUNCH trefoil-mosaic F-corona, PUNCH stray-light phases); `punchbowl/auto/flows/simulate.py` generates PUNCH-specific synthetic observations via `simpunch`.

**Servers and Environments**
- Servers and Environments
- Servers and Environments:Data servers processing and handling
  - *Evidence:* `punchbowl/auto/control/db.py` + `prefect_sqlalchemy.SqlAlchemyConnector` back the SOC file database (MariaDB/MySQL — `README.md` testing section, `pymysql` in the `pipe` dependency group); `punchbowl/auto/control/launcher.py` / `processor.py` are long-running server processes; `gunicorn` serves the dashboard.
- Servers and Environments:High Performance Computing
  - *Evidence:* `punchbowl/auto/cluster.py` starts and dynamically scales a `dask.distributed.LocalCluster`; `punchbowl/util.py:109,159,200` `@numba.njit(parallel=True)` with `numba.prange`; `multiprocessing` / `concurrent.futures.ProcessPoolExecutor` used across `punchbowl/data/punch_io.py`, `level1/stray_light.py`, `levelq/pca.py`; `threadpoolctl`/`limit_threads` helpers (CHANGELOG 0.0.24, PR #970); whole-pipeline memory capping (PR #867).
- Servers and Environments:Infrastructure as Code
  - *Evidence:* `punchbowl/auto/control/util.py` `load_pipeline_configuration` drives which flows deploy on which hosts from a declarative config file — CHANGELOG 0.0.24: "Allow duplicating control flows by host…", "Allows deploying flows only on certain machines using 'run-on' option", "The config file can now contain per-server values" (PRs #839, #867); `docs/automation/control/configuration.rst`; `punchbowl/auto/cluster.py` re-reads the config to scale workers.

*Considered and rejected (audit trail):*
- `Data Visualization:3D Graphics` / `Data Visualization:Orbit Plots` — `examples/PUNCH-InSitu-Connection.py` does plot PSP/Solar Orbiter trajectories in 3D, but with plain `matplotlib`/`sunpy.coordinates.get_horizons_coord`, not with any punchbowl API. Not a punchbowl capability.
- `Models and Simulations:Forecasting` — QuickPUNCH products are *delivered to* NOAA forecasters (`docs/data/data_overview.rst`), but punchbowl produces no forecast.
- `Data Processing and Analysis:2D Slices` / `Data Visualization:2D Slices` — polarization-layer selection from an (npol, y, x) cube is not cross-sectioning a 3D volume.
- `Servers and Environments:Software or Environment Container` — Docker/Podman appear only as a way to obtain a MariaDB image for tests (`README.md`, Testing); no container is shipped.
- `Data Processing and Analysis:Field-line Tracing`, `Spectrogram`, `Wavelet Analysis`, `Energy Spectra`, `Plasma Moments`, `Pitch Angle Distributions`, `Curlometer`, `Magnetic Null Finding`, `Linear Gradient Estimation`, `3D Particle Distribution Processing`, `Data Assimilation` — no supporting code.
- `Models and Simulations:MHD` / `First Principles` / `Theory` / `ML/AI` — no solver or physics-first model; the only ML is the PCA classified above.
- `Coordinate Transforms:Ionospheric` / `:Planetary` — no such frames used.

---

### 5. Related Region (MANDATORY)
- Solar Environment — *From the existing HSSI record. Evidence: `docs/intro.rst` — PUNCH studies "how the mass and energy of the Sun's corona become the solar wind"; the L1–L3 products are coronal/heliospheric brightness images; NFI is a coronagraph observing the inner corona.*
- Interplanetary Space — *Evidence: `docs/data/access.rst`, "Data Projections" — "The PUNCH WFI instruments extend their field of view out to around 45-degrees from the Sun, creating a meshed virtual observatory extending to a diameter of nearly 180 solar radii"; `docs/intro.rst` — PUNCH images "the entire inner solar system"; `punchbowl/level3/velocity.py` `track_velocity` derives solar-wind flow across that heliospheric field of view (L3 "VAM" product, `docs/data/data_overview.rst`).*
- Corona — *Evidence: the data overview identifies the corona as a direct imaging target and says the Level 3 products are usable as coronal images (`docs/data/data_overview.rst:4,70`); the Level 3 flow-tracking documentation explicitly computes outflow velocities in the solar corona (`docs/pipeline/level3/velocity.rst:4`).*
- Solar Wind — *Evidence: PUNCH is designed to study how coronal mass and energy become the solar wind (`docs/intro.rst:6-7`), and its Level 3 products are directly usable as solar-wind images (`docs/data/data_overview.rst:70`), including the implemented VAM derived solar-wind-motion product.*

*Considered and rejected:* `Earth Atmosphere` — `punchbowl/level2/bright_structure.py` detects "high-altitude aurora" transients, but only to **flag them as artifacts** in the quality mask, not to support atmospheric science. `Earth Magnetosphere` / `Planetary Magnetospheres` — no supporting functionality (the GSE/GEI transforms in `level0.py` are spacecraft-ephemeris bookkeeping only).

---

### 6. Authors (MANDATORY)
*This list is the identity-aware union of the authors already held in HSSI and all 15 `CITATION.cff` authors, matched by ORCID; no author was dropped. Two spellings HSSI had stored were wrong — "Attie" for Attié and "Kovak" for Kovac — and were corrected in the shared author records. Two names (Murphy, Badman) are recorded in the fuller live HSSI form rather than the shorter `CITATION.cff` form, per reviewer decisions A and B — `Person` is a shared entity with no per-entry name override. Order follows `CITATION.cff` (the maintainers' authoritative ordering). Affiliations are the identity-aware union of the HSSI affiliations (resolved from the HSSI Organization table) and repository/ORCID evidence.*

1. **J. Marcus Hughes**
   - Identifier: https://orcid.org/0000-0003-3410-7650
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: existing HSSI record; `CITATION.cff` lines 4-6; `pyproject.toml` `authors` (`marcus.hughes@swri.org`), also listed as sole `maintainers` entry.*
2. **Sam Van Kooten** (givenName `Sam`, familyName `Van Kooten`)
   - Identifier: https://orcid.org/0000-0002-4472-8517
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: the live HSSI `Person` row for ORCID 0000-0002-4472-8517, which holds **`Sam` / `Van Kooten`**. punchbowl's own sources give the variant **`Samuel J.` / `Van Kooten`** — `CITATION.cff` lines 8-10, Zenodo/DataCite creator `Van Kooten, Samuel J.`, and `pyproject.toml` (`samuel.vankooten@swri.org`). Both forms are correct. `Person` is a **shared entity** across ndcube, punchbowl, regularizePSF and SunPy, and HSSI provides **no per-entry given-name override** — the API matches on identifier and refuses to overwrite a non-blank name — so this file follows the shared live identity. ORCID and the Southwest Research Institute affiliation are unchanged.*
3. **Jasmine Kobayashi**
   - Identifier: https://orcid.org/0000-0001-9098-7790
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: `CITATION.cff` lines 12-14; `pyproject.toml` (`jasmine.kobayashi@swri.org`); ORCID employment record confirms Southwest Research Institute (ROR https://ror.org/03tghng59).*
4. **Courtney Peck**
   - Identifier: https://orcid.org/0000-0002-7586-4220
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: `CITATION.cff` lines 16-18; `pyproject.toml` (`courtney.peck@swri.org`). **Note:** her ORCID record currently lists Laboratory for Atmospheric and Space Physics (https://ror.org/01fcjzv38) and Cooperative Institute for Research in Environmental Sciences (https://ror.org/00bdqav06) as employments; the repository's own contact e-mail domain was preferred as the affiliation for this contribution. Southwest Research Institute stands as the recorded affiliation; the ORCID discrepancy is noted here deliberately and not applied.*
5. **Craig DeForest**
   - Identifier: https://orcid.org/0000-0002-7164-2786
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: existing HSSI record; `CITATION.cff` lines 20-22; `pyproject.toml` (`craig.deforest@swri.org`).*
6. **Chris Lowder**
   - Identifier: https://orcid.org/0000-0001-8318-8229
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: existing HSSI record; `CITATION.cff` lines 24-26; `pyproject.toml` (`chris.lowder@swri.org`).*
7. **Matthew West**
   - Identifier: https://orcid.org/0000-0002-0631-2393
   - Affiliation: European Space Research and Technology Centre — https://ror.org/03h3jqn23
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: existing HSSI record (both affiliations preserved); `CITATION.cff` lines 28-30 gives "West, Matthew J." — the middle initial is a stylistic difference only, so the seeded HSSI display name is kept.*
8. **Nicholas A. Murphy**
   - Identifier: https://orcid.org/0000-0001-6628-8033
   - Affiliation: Smithsonian Astrophysical Observatory — https://ror.org/04mh52z70
   - Affiliation: Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17
   - Affiliation: Smithsonian Institution — https://ror.org/01pp8nd67
   - *Source: `CITATION.cff` lines 32-34, which give the short form "Murphy, Nick". The shared HSSI Person record for ORCID 0000-0001-6628-8033 holds the fuller **`Nicholas A.` / `Murphy`**, and `Person` is a shared entity with no per-entry name override, so the fuller live form is recorded here (reviewer decision A, 2026-07-28). All three affiliations pre-existed on the shared row and were accumulated across other software entries; each resolves to a distinct ROR, so there is no duplication. ROR for SAO resolved via `https://api.ror.org/v2/organizations?query=Smithsonian Astrophysical Observatory`.*
9. **Raphael Attié**
   - Identifier: https://orcid.org/0000-0003-4312-6298
   - Affiliation: George Mason University — https://ror.org/02jqj7156
   - Affiliation: Goddard Space Flight Center — https://ror.org/0171mag52
   - *Source: `CITATION.cff` lines 36-38 (`family-names: "Attié"`); Zenodo/DataCite creator `Attié, Raphael`. Both existing HSSI affiliations are preserved. The earlier HSSI spelling "Attie" was incorrect; the repository and Zenodo evidence support the accented family name recorded here.*
10. **Samuel T. Badman**
    - Identifier: https://orcid.org/0000-0002-6145-436X
    - Affiliation: Center for Astrophysics Harvard & Smithsonian — https://ror.org/03c3r2d17
    - *Source: `CITATION.cff` lines 40-42, which give the short form "Badman, Samuel". The shared HSSI Person row holds the fuller **`Samuel T.` / `Badman`**, and `Person` is shared with no per-entry override, so the fuller live form is recorded here. Affiliation name follows the ROR canonical display name for `03c3r2d17`.*
11. **Sarah Kovac**
    - Identifier: https://orcid.org/0000-0003-1714-5970
    - Affiliation: NSF NCAR High Altitude Observatory — https://ror.org/03773p874
   - *Source: `CITATION.cff` lines 44-46 (`family-names: "Kovac"`); Zenodo/DataCite creator `Kovac, Sarah`; `pyproject.toml` `{ name = "Sarah Kovac" }`. The existing HSSI affiliation is preserved. The earlier HSSI spelling "Kovak" was incorrect; all repository and publication evidence supports `Kovac`.*
12. **Joseph Plowman**
    - Identifier: https://orcid.org/0000-0001-7016-7226
    - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
    - *Source: `CITATION.cff` lines 48-50; `pyproject.toml` (`joseph.plowman@swri.org`). His ORCID record lists no employment, so the repository e-mail domain is the affiliation evidence.*
13. **Ritesh Patel**
    - Identifier: https://orcid.org/0000-0001-8504-2725
    - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
    - *Source: existing HSSI record; `CITATION.cff` lines 52-54; `pyproject.toml` (`ritesh.patel@swri.org`).*
14. **Derek Lamb**
    - Identifier: https://orcid.org/0000-0002-6061-6443
    - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
    - *Source: existing HSSI record; `CITATION.cff` lines 56-58; `pyproject.toml` (`derek.lamb@swri.org`).*
15. **Daniel Seaton**
    - Identifier: https://orcid.org/0000-0002-0494-2025
    - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
    - *Source: existing HSSI record; `CITATION.cff` lines 60-62; `pyproject.toml` (`daniel.seaton@swri.org`).*

*Shared-author identity constraint: HSSI author identities are shared across software entries and keyed by ORCID, with no per-entry name override. This dossier therefore records the settled shared forms for Van Kooten, Attié, Kovac, Murphy, and Badman, while preserving the repository variants and correction evidence above so future refreshes do not reintroduce the earlier spellings.*

---

### 7. Software Name (MANDATORY)
punchbowl

*Source: existing HSSI record; `CITATION.cff` `title: "punchbowl"`; `pyproject.toml` `name = "punchbowl"`; Zenodo record title `punchbowl`; PyPI project `punchbowl`.*

---

### 8. Description (MANDATORY)
punchbowl contains the science processing calibration code for use with data from the Polarimeter to UNify the Corona and Heliosphere (PUNCH) mission. It provides the primary software modules in use by the mission processing pipeline for calibrating data, also available directly to science community users. The repository also contains software tools for handling PUNCH data, along with example notebooks. Since version 0.0.23 it has also incorporated the former punchpipe package as the punchbowl.auto subpackage, which supplies the Science Operations Center automation layer: telemetry ingest and Level 0 generation, Prefect-based flow scheduling and orchestration, a processing file database, and a monitoring dashboard.

*The submitter's three original sentences are preserved **verbatim**; a fourth sentence is appended because those three alone leave the description materially incomplete — an addition, not a stylistic rewrite of the submitter's wording. Evidence for the addition: `CHANGELOG.rst` line 221, "Moves punchpipe into punchbowl auto subpackage. (#771)"; `docs/automation/index.rst` — "This section is about what we used to call 'punchpipe.' It's how the SOC automates file generation on their servers."; `pyproject.toml` `[project.scripts] punchpipe = "punchbowl.auto.cli:main"`; the `punchbowl/auto/` tree (control, flows, monitor); `https://api.github.com/repos/punch-mission/punchpipe` reports `"archived": true`.*

---

### 9. Concise Description (OPTIONAL)
Science calibration code and data handling tools for the PUNCH mission

*Source: existing HSSI record (66 characters). Preserved as submitter editorial wording; it remains accurate.*

---

### 10. Publication Date (RECOMMENDED)
2024-11-01

*Source: existing HSSI record; corroborated by the earliest PyPI upload for the project, `punchbowl-0.0.0` at `2024-11-01T14:45:44.134455Z` (`https://pypi.org/pypi/punchbowl/json`), which coincides with the first Zenodo deposit under concept DOI 10.5281/zenodo.14029123. That earliest timestamp belongs to `punchbowl-0.0.0`, not to `punchbowl-0.0.4` (uploaded `2024-11-13T17:55:38.815434Z`), which an earlier version of this note cited in error; the 2024-11-01 publication date itself is unaffected.*

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Source: existing HSSI record; DataCite `attributes.publisher = "Zenodo"` for 10.5281/zenodo.14029123.*

---

### 12. Version (RECOMMENDED)
- **Version Number:** 0.0.24
- **Version Date:** 2026-07-28
- **Version PID:** https://doi.org/10.5281/zenodo.21640289
- **Version Description:** Reworks Level 2 mosaic assembly so polarized inputs are co-aligned before conversion to the MZP-solar system; substantially speeds up Level 1 alignment and runs reprojection and starfield generation at 32 bits to cut memory use; caps whole-pipeline memory and the number of concurrent flows; adds per-server configuration, host-scoped control flows and a "run-on" deployment option; writes spacecraft position and velocity into FITS headers in additional Earth-centric frames via the new GCRS-aware `PUNCHCube.celestial_wcs`; introduces the `PUNCHCube` NDCube subclass carrying a secondary celestial WCS; sets up QuickPUNCH for new clear-derived product types; allows interpolation between starfield models; removes the unused quadprog F-corona approach; plus numerous polarization, metadata, scheduling and Fido-client fixes.

*The record previously carried `punchbowl - 0.0.19`, five releases stale. 0.0.24 is the current latest release:*
- *`git for-each-ref refs/tags` → tag `0.0.24` dated 2026-07-28 (next-newest `0.0.23` dated 2026-04-01); `0.0.24` is reachable from the extracted revision `527b32ad`.*
- *PyPI: `https://pypi.org/pypi/punchbowl/json` reports `info.version = "0.0.24"`, `punchbowl-0.0.24.tar.gz` uploaded `2026-07-28T08:37:33.933467Z` (24 releases total).*
- *Zenodo: record `21640289` — `"version": "0.0.24"`, `"publication_date": "2026-07-28"`, `"doi": "10.5281/zenodo.21640289"`, `"conceptdoi": "10.5281/zenodo.14029123"`; DataCite relatedIdentifier `IsSupplementTo https://github.com/punch-mission/punchbowl/tree/0.0.24`.*
- *`CITATION.cff`: `version: 0.0.24`, `date-released: 2026-07-28`.*
- *Version Description summarised from `CHANGELOG.rst`, section "0.0.24 (2026-07-28)".*

---

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source: existing HSSI record; `pyproject.toml` `requires-python = ">=3.11,<3.15"`; `.github/workflows/ci.yaml` test matrix `["3.11", "3.12", "3.13", "3.14"]`. **Note:** SoMEF also reports "Shell" for the repository (a handful of helper scripts such as `scripts/L3_PAM_CAM_filecounts.sh`); not added, because the form asks only for "the most important languages" and Shell is incidental here.*

---

### 14. Reference Publication (RECOMMENDED)
Not found

*`CITATION.cff` contains no `preferred-citation`; the maintainers' stated citation is the software DOI itself ("If you use this software, please cite it as below.", `CITATION.cff` line 2). The closest candidate — Hughes et al. (2023), "Interoperability of PUNCH software in the Python ecosystem", https://doi.org/10.5281/zenodo.8412310, whose abstract explicitly describes punchbowl as "the core PUNCH pipeline package" — was considered and deliberately not promoted to this field, because the maintainers name no reference publication of their own; it is recorded under Related Publications (Field 27) instead.*

---

### 15. License (RECOMMENDED)
- **License:** GNU Lesser General Public License v3.0 only
- **License URI:** https://spdx.org/licenses/LGPL-3.0-only.html

*Source: existing HSSI record; `LICENSE` — "Copyright (c) 2024 PUNCH Science Operations Center … may be used, modified, and distributed under the terms of the GNU Lesser General Public License v3 (LGPL-v3)"; `pyproject.toml` `license = { file = "LICENSE" }`. SPDX short identifier `LGPL-3.0-only`; the License URI is held on the shared HSSI `License` row, which the software view does not display. **Note:** the Zenodo deposit records `cc-by-4.0` (a Zenodo default); the repository `LICENSE` file is authoritative and the existing HSSI value is correct.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

Carried over from the existing HSSI record:
- Calibration — *existing HSSI record; `pyproject.toml` `keywords`.*
- Image — *existing HSSI record; GitHub repo topic `image` (SoMEF `keywords`).*
- Nasa — *existing HSSI record; `pyproject.toml` `keywords`; GitHub topic `nasa`.*
- Nasa Data — *existing HSSI record; GitHub topic `nasa-data`.*
- Punch — *existing HSSI record; `pyproject.toml` `keywords`; GitHub topic `punch`.*
- Science — *existing HSSI record; `pyproject.toml` `keywords`.*
- Solar Physics — *existing HSSI record; `pyproject.toml` `keywords`; GitHub topic `solar-physics`.*
- Solar Wind — *existing HSSI record; GitHub topic `solar-wind`.*

From repository evidence:
- astrometry (in HSSI vocabulary) — *`punchbowl/level1/alignment.py` uses the `astrometry` (astrometry.net) solver and a Gaia catalog to solve image pointing (`astrometry_net_initial_solve`, `solve_pointing`, `download_gaia_data`).*
- ccsds (in HSSI vocabulary) — *`punchbowl/auto/flows/level0.py` decommutates CCSDS packets with `ccsdspy`.*
- corona (in HSSI vocabulary) — *`docs/intro.rst`; L3 products are coronal brightness images.*
- coronagraph (in HSSI vocabulary) — *NFI is PUNCH's coronagraph; `docs/data/access.rst`, `punchbowl/level1/vignette.py` `generate_vignetting_calibration_nfi`.*
- heliosphere (in HSSI vocabulary) — *"Polarimeter to UNify the Corona and Heliosphere"; WFI field of view spans ~180 solar radii (`docs/data/access.rst`).*
- image processing (in HSSI vocabulary) — *`punchbowl/level1/despike.py`, `destreak.py`, `deficient_pixel.py`, `level2/resample.py`.*
- photometry — *`punchbowl/level1/quartic_fit.py` `photometric_calibration`; products are "floating-point values in mean-solar-brightness units" (`docs/data/data_overview.rst`, Level 1).*
- point spread function (in HSSI vocabulary) — *`punchbowl/level1/psf.py` with `regularizepsf.ArrayPSFTransform`.*
- polarimetry — *PUNCH is a polarimeter; `punchbowl/level2/polarization.py`, `level3/polarization.py`, and the B/pB/pB′ and M,Z,P systems in `docs/data/data_overview.rst`.*
- solar imaging (in HSSI vocabulary) — *`docs/data/data_overview.rst`: "PUNCH is an imaging mission and most data from the mission are images."*
- space weather (in HSSI vocabulary) — *`docs/data/data_overview.rst`, Level Q: "intended to be useful for space weather forecasting … produced for NOAA's space weather forecasting infrastructure".*
- telemetry (in HSSI vocabulary) — *`punchbowl/auto/flows/level0.py` ingests spacecraft TLM files (`TLMFiles`, `PacketHistory`).*
- thomson scattering (in HSSI vocabulary) — *`examples/PUNCH-InSitu-Connection.py`: "assuming the pixel intensity can be associated with the Thomson sphere"; PUNCH images Thomson-scattered light.*

*Considered and rejected:* `python` and `fits` — the field is for "science keywords … not supported by other metadata fields", and these duplicate Field 13 and Fields 18/19.

---

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific — *Source: existing HSSI record; `punchbowl/data/fido/client.py` `PUNCHClient` is a PUNCH-specific client reading the SDAC PUNCH tree; `punchbowl/auto/flows/level0.py` ingests PUNCH spacecraft telemetry directly. Cross-listed with Fields 31/32 as instructed.*
- The Virtual Solar Observatory. — *Source: existing HSSI record; `docs/data/access.rst` — "stored and accessible through the Solar Data Analysis Center (SDAC) - a portal for hosting through tools such as the Virtual Solar Observatory (VSO). From here PUNCH data products can be queried and requested for download"; `examples/querying_data.py` — "how to query PUNCH data from the SDAC / VSO using Python tools". The trailing period is part of the controlled value, not sentence punctuation: the stored `DataInput` vocabulary row is named `The Virtual Solar Observatory.`, and the bare form without it matches no row.*
- HTTP/HTTPS Directories — *Source: `punchbowl/data/fido/client.py:22-23` — `fits_rootdir = "https://umbra.nascom.nasa.gov/punch"`, `jp2_rootdir = "https://umbra.nascom.nasa.gov/punch/L"`, scraped with `sunpy.net.scraper.Scraper` over a dated directory `pattern`; `docs/data/access.rst` documents the equivalent `wget -r -l1 --no-parent … https://umbra.nascom.nasa.gov/punch/3/CAM/2025/09/21/`; `punchbowl/data/sample.py:19` downloads sample files from `https://data.boulder.swri.edu/lowder/PUNCH/sample/`.*

*Considered and rejected:* `S3/Cloud-aware` — `punchbowl/auto/flows/levelq.py:602-609` uploads QuickPUNCH products **to** a NOAA S3 bucket, but this field is defined as "the data **input** source the software supports" and punchbowl never reads from S3.

---

### 18. Input File Formats (RECOMMENDED)
- FITS — *Source: existing HSSI record; `punchbowl/data/punch_io.py:395` `load_ndcube_from_fits`, `load_many_cubes`; `docs/data/access.rst`, "Reading Data".*
- csv — *Source: `punchbowl/data/meta.py:42` `pd.read_csv(path, na_filter=False)` loads the omniheader/level metadata templates; `punchbowl/level1/alignment.py:153,168` `load_gaia_catalog(... "gaia_catalog.csv")`; `punchbowl/auto/cli.py:273` and `punchbowl/auto/flows/level0.py:1290` `pd.read_csv`; `scripts/auto/prepare_packet_definition_csv_files.py`.*
- JSON — *Source: `json.load` used in 8 places, including pipeline/quicklook configuration and cached state (`punchbowl/auto/control/util.py`, `punchbowl/auto/flows/level0.py`).*
- Other — *Covers: raw CCSDS telemetry (TLM) packet files (`punchbowl/auto/flows/level0.py`, `ccsdspy.utils.split_by_apid`); JPEG2000-compressed image packets decoded with `pylibjpeg.decode` (line 624); Excel packet-definition workbooks (`pd.read_excel`, line 198); NumPy `.npy` square-root decode tables (`punchbowl/level1/sqrt.py:71-105`); YAML pipeline configuration (`punchbowl/auto/control/util.py` `load_pipeline_configuration`).*

*Considered and rejected:* `HDF5` — `h5py>=3.15` is declared in the `super_user` extra but is never imported anywhere in `punchbowl/`. `CDF`, `netCDF3/4`, `IDL.sav`, `Zarr`, `ISTP-Compliant`, `ascii` — no supporting code.

---

### 19. Output File Formats (RECOMMENDED)
- FITS — *Source: existing HSSI record; `punchbowl/data/punch_io.py:285` `write_ndcube_to_fits` (RICE-compressed, with uncertainty HDU and provenance BinTable — `_make_provenance_hdu`, `_pack_uncertainty`); `docs/data/access.rst`.*
- csv — *Source: `punchbowl/auto/cli.py:350` `result_df.to_csv(output_file_soc, index=False)`; `punchbowl/auto/flows/level0.py:1296` `new_table.to_csv(df_path, index=False)`; `punchbowl/level1/alignment.py:57` writes the Gaia catalog with `.to_csv(out_path)`.*
- JSON — *Source: `json.dump` used in 33 places (flow state, cache and dashboard artefacts across `punchbowl/auto/`).*
- Other — *Covers: JPEG2000 quicklooks (`punchbowl/data/punch_io.py:105` `write_ndcube_to_quicklook` via `glymur.Jp2k`, with an XML metadata box from `_generate_jp2_xmlbox`); MP4 animations (`write_quicklook_to_mp4`, line 242; `punchbowl/data/visualize.py:135` `animate_punch`); NumPy `.npz`/`.npy` (`punchbowl/limits.py:164` `np.savez`, `punchbowl/level1/sqrt.py:95,105` `np.save`); `.sha` checksum sidecars (`punchbowl/data/punch_io.py:40` `write_file_hash`).*

---

### 20. Operating System (RECOMMENDED)
- Linux — *Source: existing HSSI record; `.github/workflows/ci.yaml` runs the full test matrix on `runs-on: ubuntu-latest`; the PUNCH SOC servers referenced throughout `punchbowl/auto/` are Linux hosts.*
- Mac — *Source: existing HSSI record; `README.md` lines 30, 36 give macOS activation instructions (`source .venv/bin/activate` on Mac/Linux); HSSI CPU architecture already records Apple Silicon arm64.*

*Considered and rejected:* `Windows` — `README.md` lines 30 and 36 do mention `.venv\Scripts\activate` on Windows, but that is boilerplate venv text; CI never exercises Windows, and the `super_user` extra pulls in `astrometry` (astrometry.net bindings, used by `punchbowl/level1/alignment.py:320`) and `sep`, which do not build on Windows. Windows is therefore deliberately not recorded as a supported operating system.

---

### 21. CPU Architecture (RECOMMENDED)
- x86-64 — *Source: existing HSSI record; CI runs on `ubuntu-latest` (x86-64 runners).*
- Apple Silicon arm64 — *Source: existing HSSI record; pure-Python/wheel-based install documented for Mac in `README.md`.*
- GPU — *Carried over from the existing HSSI record and independently confirmed. Source: `punchbowl/level3/motion_filter.py:7-10,96-110` optionally imports `cupy` and runs the hourglass motion filter on GPU (`use_gpu` parameter, "Whether to use GPU for processing (default is True)"), falling back to CPU when cupy is unavailable; `punchbowl/data/punch_io.py:263` mentions a codec "For GPU acceleration".*

*Considered and rejected:* `HPC or HEC` — the pipeline scales across SOC servers with a Dask `LocalCluster` and numba threading, but there is no HPC-centre scheduler integration (no MPI, no Slurm/PBS job scripts).

---

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections — *Source: existing HSSI record; `docs/data/access.rst` — PAM files make it "the product of choice for studies of CMEs, shocks, the solar wind, etc."*
- Solar Corona — *Source: existing HSSI record; `docs/intro.rst`; L3 products are "intended to be usable directly as coronal and solar-wind images" (`docs/data/data_overview.rst`).*
- Solar Wind — *Source: existing HSSI record; `punchbowl/level3/velocity.py` `track_velocity` produces the L3 VAM "derived solar-wind motion" product.*

*Considered and rejected:* an "F-corona" / zodiacal-light term would be well evidenced (`punchbowl/level3/f_corona_model.py`, `docs/pipeline/level3/f_corona.rst`), but the HSSI Phenomena vocabulary holds only Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind and X-ray emission, none of which expresses it, and adding it would create a new controlled-vocabulary row. It was considered and deliberately not added, so this field carries only the three vocabulary terms above.

---

### 23. Development Status (RECOMMENDED)
Active

*The HSSI record carried no development status. Source: 24 tagged releases with the newest, `0.0.24`, cut on 2026-07-28; commit `527b32ad` dated 2026-07-28; `CHANGELOG.rst` 0.0.24 alone references PRs up to #1075; the code is in operational use generating the PUNCH mission's public data products. Per repostatus.org, "Active: reached stable, usable state and being actively developed". **Note:** `README.md` lines 9-11 caution that "This package is still being heavily edited as calibration algorithms are improved. Stability is not promised until v1", and `pyproject.toml` classifies it `Development Status :: 4 - Beta`; "WIP" was rejected because that term requires "no stable, usable public release yet", which is contradicted by 24 PyPI releases in production use.*

---

### 24. Documentation (RECOMMENDED)
https://punchbowl.readthedocs.io/en/latest/

*Source: existing HSSI record; `README.md:7`; `pyproject.toml` `[project.urls] Documentation`; `.readthedocs.yaml`. URL verified live (HTTP 200 on 2026-07-28).*

---

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

*Source: existing HSSI record (already fully expanded, no acronym). Corroborated by `docs/intro.rst` — "PUNCH is a NASA Small Explorer (SMEX) mission". The repository contains no funding-acknowledgement file and the Zenodo/DataCite records carry an empty `fundingReferences` list, so no additional funder could be evidenced.*

---

### 26. Award Title (OPTIONAL)
- **Award Title:** Polarimeter to UNify the Corona and Heliosphere (PUNCH)
- **Award Number:** 80GSFC18C0014

*Award Title source: existing HSSI record; the mission name is confirmed in `docs/intro.rst` and `punchbowl/data/fido/client.py` — `a.Source: [("PUNCH", "Polarimeter to UNify the Corona and Heliosphere")]`.*

*Award Number `80GSFC18C0014` was previously recorded here as "Not found" because the HSSI software view does not render award numbers. The existing HSSI association pairs that number with the PUNCH award title, so the value is retained rather than discarded.*

***External corroboration — partial, and honestly qualified.** The number could not be tied to the PUNCH award by any punchbowl-side source: the repository contains no funding-acknowledgement file, and DataCite reports an empty `fundingReferences` list for the punchbowl DOIs. A targeted web search did, however, establish that `80GSFC18C0014` is a **real NASA contract number**: NASA NTRS record `20220017302` ("The Coronal Veil", Malanushenko, Cheung, **DeForest**, Klimchuk & Rempel) lists `CONTRACT_GRANT: 80GSFC18C0014`, and C. E. DeForest is both a punchbowl author and the PUNCH principal investigator at Southwest Research Institute. That corroborates the number's existence and its association with DeForest/SwRI solar work, but **not** that it is specifically the PUNCH SMEX award; a second search against SwRI/PUNCH mission pages returned no acknowledgement text containing it. The value is therefore recorded as a **pre-existing HSSI value we are surfacing, not introducing or endorsing**.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
*The HSSI record carried no related publications. Only DOIs actually cited by the project are listed.*

- https://doi.org/10.5281/zenodo.8412310 — Hughes, J. M., DeForest, C., Kovac, S., Lowder, C., Patel, R., Seaton, D., & West, M. J. (2023). *Interoperability of PUNCH software in the Python ecosystem*. Zenodo. — *Evidence: the DataCite abstract names this software directly: "regularizePSF corrects variable point spread functions, and solpolpy resolves solar polarization to a standard frame. These packages are used in the core PUNCH pipeline package - punchbowl." Authored by the punchbowl author team. Also a candidate Reference Publication (Field 14).*
- https://doi.org/10.3847/1538-4357/ac43b6 — DeForest, C. E., Seaton, D. B., & West, M. J. (2022). *Three-polarizer Treatment of Linear Polarization in Coronagraphs and Heliospheric Imagers*. The Astrophysical Journal. — *Evidence: cited in `docs/data/data_overview.rst:18` as the definition of the B/pB/pB′ and M,Z,P polarization systems that `punchbowl/level2/polarization.py` and `punchbowl/level3/polarization.py` implement.*
- https://doi.org/10.1023/B:SOLA.0000021743.24248.b0 — DeForest, C. E. (2004). *On Re-sampling of Solar Images*. Solar Physics. — *Evidence: cited in `docs/pipeline/level2/image_resample.rst:11` as the algorithm behind the adaptive reprojection used by `punchbowl/level2/resample.py` `reproject_cube`.*

---

### 28. Related Datasets (OPTIONAL)
*This field lists the **complete set of 43** Solar Data Analysis Center PUNCH dataset DOIs: the four collection DOIs plus 39 product DOIs. They were enumerated from the DataCite query `https://api.datacite.org/dois?prefix=10.48322&query=titles.title:PUNCH&page[size]=100`; no DOI suffix was pattern-generated. Titles below are reproduced **verbatim from DataCite**, including the registry's own typos ("puls 60", the double space in "Level 3  Low-noise").*

**Collection DOIs already held in HSSI (4)**
- https://doi.org/10.48322/5k49-bh56 — PUNCH NFI-WFI Level 0 Science images — *existing HSSI record; DataCite publisher "Solar Data Analysis Center", 2025.*
- https://doi.org/10.48322/enbf-rh75 — PUNCH NFI-WFI Level 1 Science images — *existing HSSI record; DataCite verified.*
- https://doi.org/10.48322/stqs-j385 — PUNCH NFI-WFI Level 2 Science Dataset — *existing HSSI record; DataCite verified.*
- https://doi.org/10.48322/nnv7-bn21 — PUNCH NFI-WFI Level 3 Science Dataset — *existing HSSI record; DataCite verified.*

**Level 2 science products (2)**
- https://doi.org/10.48322/z829-zy89 — PUNCH Level2 Polarized Mosaics (Trefoil) Data — *product code PTM, produced by `punchbowl/level2/flow.py` `level2_core_flow` (`docs/data/data_overview.rst`, Level 2).*
- https://doi.org/10.48322/sv88-z093 — PUNCH Level2 Clear Mosaics (Trefoil) Data — *product code CTM, same flow.*

**Level 3 science products (6)**
- https://doi.org/10.48322/f6tk-sm20 — PUNCH Level 3 Polarized Mosaic Data in the MZP system — *product code PTM/L3, `punchbowl/level3/flow.py` `level3_core_flow`.*
- https://doi.org/10.48322/kxpb-q477 — PUNCH Level 3 Clear Mosaic Data — *product code CTM/L3, same flow.*
- https://doi.org/10.48322/5gmz-ka58 — PUNCH Level 3  Low-noise Polarized Mosaic Data in the MZP system — *product code PAM, `punchbowl/level3/low_noise.py` `create_low_noise_task`; `docs/data/access.rst` calls PAM a recommended starting product.*
- https://doi.org/10.48322/bbrw-k528 — PUNCH Level 3 Clear Low-Noise Mosaic Data — *product code CAM, same module; the other recommended starting product.*
- https://doi.org/10.48322/dcpx-4r68 — PUNCH Level 3 Polarized Mosaic F-corona Model in the MZP system — *generated by `punchbowl/level3/f_corona_model.py` `construct_f_corona_model`.*
- https://doi.org/10.48322/dy2y-je98 — PUNCH Level 3 Clear Mosaic F-corona Model — *same module.*

**Level 0 per-spacecraft, per-polarization-state products (15)**
*Evidence: `punchbowl/auto/flows/level0.py` decommutates each spacecraft's CCSDS telemetry and writes exactly these products; `docs/data/data_overview.rst`, Level 0 — "Polarized images have the codes \"PMn\", \"PZn\", and \"PPn\" where \"n\" is the spacecraft number … Clear images (taken with no polarizer in the beam) have the codes \"CRn\"."*
- https://doi.org/10.48322/rdxc-x144 — PUNCH NFI Level 0 Science images in the clear polarization state
- https://doi.org/10.48322/d23m-1943 — PUNCH NFI Level 0 Science images in the minus 60 degree polarization state
- https://doi.org/10.48322/snkc-vw59 — PUNCH NFI Level 0 Science images in the zero degree polarization state
- https://doi.org/10.48322/fkmt-dc86 — PUNCH WFI1 Level 0 Science images in the clear polarization state
- https://doi.org/10.48322/rw5m-qm29 — PUNCH WFI1 Level 0 Science images in the minus 60 degree polarization state
- https://doi.org/10.48322/4bf8-rn78 — PUNCH WFI1 Level 0 Science images in the puls 60 degree polarization state
- https://doi.org/10.48322/qjbk-w851 — PUNCH WFI1 Level 0 Science images in the zero degree polarization state
- https://doi.org/10.48322/mm0r-tp04 — PUNCH WFI2 Level 0 Science images in the clear polarization state
- https://doi.org/10.48322/gztn-bp08 — PUNCH WFI2 Level 0 Science images in the minus 60 degree polarization state
- https://doi.org/10.48322/553p-pm90 — PUNCH WFI2 Level 0 Science images in the puls 60 degree polarization state
- https://doi.org/10.48322/mxc0-0t72 — PUNCH WFI2 Level 0 Science images in the zero degree polarization state
- https://doi.org/10.48322/wwep-rq13 — PUNCH WFI3 Level 0 Science images in the clear polarization state
- https://doi.org/10.48322/337y-yr97 — PUNCH WFI3 Level 0 Science images in the minus 60 degree polarization state
- https://doi.org/10.48322/1psr-xf64 — PUNCH WFI3 Level 0 Science images in the puls 60 degree polarization state
- https://doi.org/10.48322/d9d6-yy72 — PUNCH WFI3 Level 0 Science images in the zero degree polarization state

**Level 1 per-spacecraft, per-polarization-state products (16)**
*Evidence: `punchbowl/level1/flow.py` (`level1_early_core_flow`, `level1_middle_core_flow`, `level1_late_core_flow`) produces the calibrated per-spacecraft L1 images; `docs/data/data_overview.rst`, Level 1 — "photometrically calibrated, conditioned data from the PUNCH cameras, maintained as separate data files from each spacecraft … with the same product codes" as Level 0.*
- https://doi.org/10.48322/q3ap-jw02 — PUNCH NFI Level 1 Science images in the clear polarization state
- https://doi.org/10.48322/7xqq-en92 — PUNCH NFI Level 1 Science images in the minus 60 degree polarization state
- https://doi.org/10.48322/8d1c-z963 — PUNCH NFI Level 1 Science images in the plus 60 degree polarization state
- https://doi.org/10.48322/j7f6-3891 — PUNCH NFI Level 1 Science images in the zero degree polarization state
- https://doi.org/10.48322/0sh7-0305 — PUNCH WFI1 Level 1 Science images in the clear polarization state
- https://doi.org/10.48322/pb0y-sk87 — PUNCH WFI1 Level 1 Science images in the minus 60 degree polarization state
- https://doi.org/10.48322/29d8-ex57 — PUNCH WFI1 Level 1 Science images in the puls 60 degree polarization state
- https://doi.org/10.48322/g2n0-2615 — PUNCH WFI1 Level 1 Science images in the zero degree polarization state
- https://doi.org/10.48322/s1h4-8b87 — PUNCH WFI2 Level 1 Science images in the clear polarization state
- https://doi.org/10.48322/13yg-5s75 — PUNCH WFI2 Level 1 Science images in the minus 60 degree polarization state
- https://doi.org/10.48322/smdy-e012 — PUNCH WFI2 Level 1 Science images in the puls 60 degree polarization state
- https://doi.org/10.48322/ba0t-hb24 — PUNCH WFI2 Level 1 Science images in the zero degree polarization state
- https://doi.org/10.48322/ssj7-kw56 — PUNCH WFI3 Level 1 Science images in the clear polarization state
- https://doi.org/10.48322/q2pz-tr06 — PUNCH WFI3 Level 1 Science images in the minus 60 degree polarization state
- https://doi.org/10.48322/n8x9-5v15 — PUNCH WFI3 Level 1 Science images in the puls 60 degree polarization state
- https://doi.org/10.48322/2gry-kg12 — PUNCH WFI3 Level 1 Science images in the zero degree polarization state

*Completeness rationale:* the per-spacecraft, per-polarization Level 0 and Level 1 children are listed **alongside** their `PUNCH NFI-WFI Level 0/1 Science images` collection DOIs. The collections remain useful aggregate identifiers, while punchbowl produces and reads each child individually. The counts are asymmetric because that is what SDAC has registered: Level 0 has 15 children (NFI has only clear, minus-60 and zero states registered — there is no Level 0 NFI plus-60 DOI in DataCite) while Level 1 has 16. Together with the four collection, two Level 2, and six Level 3 DOIs, these make the 43 DataCite-registered PUNCH datasets.

---

### 29. Related Software (OPTIONAL)

- https://doi.org/10.5281/zenodo.17873783 — **punchpipe** — *This DOI is the Zenodo concept record for `punch-mission/punchpipe`, "Pipeline automation for PUNCH mission". It is punchbowl's direct predecessor/companion, not generic infrastructure: `CHANGELOG.rst:221` records "Moves punchpipe into punchbowl auto subpackage. (#771)", `pyproject.toml` still ships the console script `punchpipe = "punchbowl.auto.cli:main"`, and `docs/automation/index.rst` says "This section is about what we used to call 'punchpipe'".*
- https://doi.org/10.5281/zenodo.10076326 — **solpolpy** — *Domain-specific PUNCH companion and solar-polarization resolver. Evidence: `punchbowl/level2/polarization.py:3,37`, `punchbowl/level3/polarization.py:6`, `punchbowl/level3/stellar.py:21-22`; `README.md` line 68 instructs contributors to set up pre-commit "in the punchbowl, solpolpy, and/or regularizepsf repositories". Concept DOI from `punch-mission/solpolpy` `CITATION.cff`.*
- https://doi.org/10.5281/zenodo.7392170 — **regularizepsf** — *Domain-specific PUNCH companion and variable-PSF package. Evidence: `punchbowl/level1/psf.py`, `punchbowl/level1/alignment.py:18`, `punchbowl/auto/control/cache_layer/psf.py:3` (`from regularizepsf import ArrayPSFTransform`); `README.md` line 68. Concept DOI from `punch-mission/regularizepsf` `CITATION.cff`.*
- https://github.com/punch-mission/simpunch — **simpunch** — *Companion PUNCH data simulator by the same team. Evidence: `punchbowl/auto/flows/simulate.py:11` `from simpunch.flow import generate_flow`; `pyproject.toml` `[dependency-groups] pipe` and `[tool.uv.sources] simpunch = { path = "../simpunch", editable = true }`; `scripts/auto/generate_batch_of_simpunch.py`.*
- https://github.com/svank/remove_starfield — **remove_starfield** — *Domain-specific dependency written by punchbowl co-author Samuel Van Kooten for heliospheric-imager starfield removal. Evidence: `punchbowl/level3/stellar.py:8,15-16,295,317`.*
- https://github.com/ccsdspy/ccsdspy — **CCSDSPy** — *Domain-specific spacecraft CCSDS packet reader whose presence characterises punchbowl as a mission telemetry-ingest pipeline. Evidence: `punchbowl/auto/flows/level0.py:16,24-25,229,274`. It is deliberately not listed under Field 30: punchbowl passes it packet definitions and receives arrays, which is ordinary library use rather than a peer-tool exchange.*

---

### 30. Interoperable Software (OPTIONAL)

- https://doi.org/10.5281/zenodo.17873783 — **punchpipe** — *Punchpipe was built to import and drive punchbowl's core flows as the SOC orchestration layer, and that code now lives inside punchbowl as `punchbowl/auto/` while retaining the `punchpipe` entry point (`pyproject.toml [project.scripts]`). Because punchpipe is now archived and merged in, the interoperability is partly historical; it remains in both Field 29 and Field 30 as punchbowl's direct predecessor and an evidenced exchange.*
- https://doi.org/10.5281/zenodo.10076326 — **solpolpy** — *Shared data-model exchange. `punchbowl/data/punch_io.py:563` `remix_collection` builds an `ndcube.NDCollection` "primarily used for solpolpy", which `punchbowl/level2/polarization.py:37` hands to `solpolpy.resolve(data_collection, outsys)` and reads back as resolved cubes; `punchbowl/level3/stellar.py:22` additionally consumes `solpolpy.util.solnorth_from_wcs`. Version provenance is recorded in the output metadata (`punchbowl/auto/control/processor.py:118-119`, `result.meta['SPPYVRSN'] = solpolpy.__version__`).*
- https://doi.org/10.5281/zenodo.7392170 — **regularizepsf** — *Object exchange through a documented API. `punchbowl/level1/psf.py` `build_psf_transform` constructs `regularizepsf` PSF models from PUNCH images and `correct_psf` applies `ArrayPSFTransform` objects loaded by `punchbowl/auto/control/cache_layer/psf.py`; output provenance records the regularizepsf version in `punchbowl/auto/control/processor.py:122`.*
- https://github.com/svank/remove_starfield — **remove_starfield** — *Plugin/extension relationship. `punchbowl/level3/stellar.py:132` defines `class PUNCHImageProcessor(ImageProcessor)`, implementing remove_starfield's extension interface, plus `class LoggingProgressIndicator` (line 220); punchbowl then calls `remove_starfield.build_starfield_estimate(...)` (lines 295, 317) with `BlockMasker`/`GaussianReducer` and subtracts the returned `Starfield`.*
- https://github.com/punch-mission/simpunch — **simpunch** — *Bidirectional companion exchange. `punchbowl/auto/flows/simulate.py:11,129` calls `simpunch.flow.generate_flow` from inside a punchbowl Prefect flow; simpunch emits synthetic PUNCH FITS products that are then fed straight back through punchbowl's own L0→L3 flows (`scripts/auto/clear_files_for_pending_simpunch_flows.py`, `generate_batch_of_simpunch.py`).*
- https://github.com/sunpy/sunpy — **SunPy** — *Plugin/extension relationship with a named domain tool. `punchbowl/data/fido/client.py:19` registers `class PUNCHClient(GenericClient)` with sunpy's Fido, and `punchbowl/data/fido/attrs.py` registers a `punch` attrs module, so `Fido.search(a.Time(...), a.punch.ProductCode.ca, a.Level.three, ...)` works after `import punchbowl` — demonstrated in `examples/querying_data.py`. PUNCH products additionally load directly as `sunpy.map.Map` (`examples/PUNCH-InSitu-Connection.py`), and `docs/intro.rst` states the pipeline and query tools are built on "the SunPy and Astropy software libraries".*
- https://github.com/sunpy/ndcube — **ndcube** — *Shared data model as the documented interchange format. `punchbowl/data/punchcube.py:13` defines `class PUNCHCube(NDCube)`; the public loader `punchbowl/data/punch_io.py:395` `load_ndcube_from_fits` returns it and `write_ndcube_to_fits` consumes it; `punchbowl/data/punch_io.py:27` uses `ndcube.NDCollection` as the interchange container; and `docs/data/access.rst` documents NDCube as a supported user-facing data container.*

- https://doi.org/10.5281/zenodo.4670728 — **Astropy** — *Punchbowl extends Astropy's APIs rather than merely consuming them. `punchbowl/data/wcs.py:460` defines `class GCRSWCS(WCS)`, subclassing `astropy.wcs.WCS` so that a PUNCH WCS accepts and returns GCRS SkyCoords, and this object is exposed as `PUNCHCube.celestial_wcs` (CHANGELOG 0.0.24, PR #964). `punchbowl/data/wcs.py:36` registers PUNCH's `pB`/`B` symbols through Astropy's polarization-frame extension API. The identifier is the concept DOI declared in Astropy's `CITATION.cff`. Astropy belongs in Field 30 for this evidenced exchange, but not in Field 29.*

*Considered and rejected — Tier A generic infrastructure (would be equally at home in a web app, finance model, or biology pipeline):* numpy, scipy, pandas, matplotlib, plotly, dash / dash-bootstrap-components, requests, python-dateutil, PyYAML, click, tqdm, setuptools, pytest (+ plugins), ruff/pre-commit/codespell, sqlalchemy / pymysql, fastapi, gunicorn, psutil, networkx, numexpr, threadpoolctl, coolname, freezegun, hypothesis, xlrd, lxml, toml, numpy-quaternion.
*Considered and rejected — domain-adjacent but no demonstrated peer exchange:* `reproject`, `photutils`, `sep`, `astrometry`, `lmfit`, `scikit-image`, `scikit-learn`, `numba`, `cupy`, `glymur`, `pylibjpeg`, `prefect` / `prefect-dask` / `prefect-sqlalchemy`, `dask`, `jupyter`.
*Considered and rejected — declared but unused:* `sunkit-image` and `h5py` appear in `pyproject.toml` but are never imported anywhere under `punchbowl/`.

---

### 31. Related Instruments (OPTIONAL)
*The HSSI record carried no related instruments. Every value below is resolved against the HSSI `InstrumentObservatory` controlled vocabulary (`type: 1`, instruments), and every identifier was additionally verified to resolve (HTTP 200) at spase-metadata.org. No bare names are emitted.*

- **Narrow Field Imager**
  - Instrument Identifier: https://spase-metadata.org/NASA/Instrument/PUNCH/NFI
  - *Ladder step 1 (exactly one row after `.html` normalisation). The vocabulary contains both `.../PUNCH/NFI` (name "Narrow Field Imager", abbreviation "NFI") and its `.html` twin `.../PUNCH/NFI.html` (name "Narrow Field Imager (NFI)"); per the normalisation rule these are one resource and the bare identifier/name is used. Repository evidence: `punchbowl/cli.py` `create_calibration` — "For WFIs, use 1, 2, or 3. For NFI, use 4"; `punchbowl/level1/vignette.py:242` `generate_vignetting_calibration_nfi`; `punchbowl/data/fido/client.py` registers `a.Instrument: ("NFI-4", "Narrow Field Imager")`; `punchbowl/auto/control/cache_layer/nfi_l1.py`; `docs/data/data_overview.rst` ("NFI is assigned the number 4").*
- **Wide Field Imager** (PUNCH spacecraft 1)
  - Instrument Identifier: https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/1
- **Wide Field Imager** (PUNCH spacecraft 2)
  - Instrument Identifier: https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/2
- **Wide Field Imager** (PUNCH spacecraft 3)
  - Instrument Identifier: https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/3
  - *The three WFI rows share the identical vocabulary name "Wide Field Imager" (abbreviation "WFI") and are distinguished by their SPASE identifiers. This is **ladder step 2**, not an ambiguity: the repository supplies concrete evidence selecting all three. `docs/data/data_overview.rst` — "WFI1, WFI2, and WFI3 are assigned the numbers 1-3"; `punchbowl/cli.py` — "For WFIs, use 1, 2, or 3"; `punchbowl/data/fido/client.py` registers `("WFI-1", "Wide Field Imager 1")`, `("WFI-2", "Wide Field Imager 2")`, `("WFI-3", "Wide Field Imager 3")`; `punchbowl/level1/vignette.py:157` `generate_vignetting_calibration_wfi`; `punchbowl/level1/dynamic_stray_light.py` builds per-WFI stray-light models; CHANGELOG 0.0.24 PR #979 fixes labelling of "WFI-3" in `plot_punch`.*

*Considered and rejected (audit trail):* `WISPR Inner/Outer Telescope` — the substring search matched `Parker Solar Probe … Wide-field Imager for Solar Probe, WISPR …` rows, but punchbowl only mentions "wispr" once (`punchbowl/level1/alignment.py:88`, in a comment about a distortion-model technique) and reads no WISPR data. `SOHO/LASCO` and `STEREO/COR2` (`punchbowl/level1/stray_light.py:869-870`) and `STEREO` (`punchbowl/level2/bright_structure.py:38`) are prose about algorithmic heritage only. Gaia — `punchbowl/level1/alignment.py` reads a Gaia star catalog as an astrometric reference, but punchbowl processes no Gaia data products and a user searching for Gaia software would not expect punchbowl; there is also no Gaia row in the `type: 1` vocabulary.

---

### 32. Related Observatories (OPTIONAL)
*The HSSI record carried no related observatories. Every value below is resolved against the HSSI `InstrumentObservatory` controlled vocabulary (`type: 2`, observatories). All identifiers verified to resolve (HTTP 200).*

- **PUNCH Mission**
  - Observatory Identifier: https://spase-metadata.org/NASA/Observatory/PUNCH
  - *Ladder step 1 after `.html` normalisation: the vocabulary holds `.../Observatory/PUNCH` (name "PUNCH Mission") and its `.html` twin `.../Observatory/PUNCH.html` (name "Polarimeter to Unify the Corona and Heliosphere (PUNCH)"); the bare row is used, with its `name` copied verbatim. Evidence: punchbowl **is** the PUNCH mission pipeline — `README.md:5`, `docs/intro.rst`, `punchbowl/data/fido/client.py` `a.Source: [("PUNCH", "Polarimeter to UNify the Corona and Heliosphere")]`, `a.Provider: [("SwRI", "Southwest Research Institute")]`.*
- **PUNCH-NFI**
  - Observatory Identifier: https://spase-metadata.org/NASA/Observatory/PUNCH/NFI
- **PUNCH-WFI-1**
  - Observatory Identifier: https://spase-metadata.org/NASA/Observatory/PUNCH/WFI/1
- **PUNCH-WFI-2**
  - Observatory Identifier: https://spase-metadata.org/NASA/Observatory/PUNCH/WFI/2
- **PUNCH-WFI-3**
  - Observatory Identifier: https://spase-metadata.org/NASA/Observatory/PUNCH/WFI/3
  - *Each PUNCH observatory row is a distinct spacecraft with a unique name and identifier (ladder step 1 for each). punchbowl processes all four spacecraft individually and by name: `punchbowl/cli.py create <level> <code> <spacecraft> …`; `docs/data/data_overview.rst` — "Level 0 files have two-letter codes with a spacecraft number appended. WFI1, WFI2, and WFI3 are assigned the numbers 1-3, and NFI is assigned the number 4"; `punchbowl/data/meta.py` `load_spacecraft_def`; CHANGELOG 0.0.24 PR #952 — "L1_early can be configured to exclude observatories or polarizations"; the Fido client registers each as a queryable instrument value.*

*Considered and rejected (audit trail):* Parker Solar Probe and Solar Orbiter — mentioned only in the documentation example `examples/PUNCH-InSitu-Connection.py`, which overplots their JPL Horizons trajectories on a PUNCH image using `sunpy.coordinates.get_horizons_coord`; punchbowl reads no PSP or Solar Orbiter data (an explicit tutorial/demo exclusion). SOHO / STEREO — heritage prose only, see Field 31. The Solar Data Analysis Center / `umbra.nascom.nasa.gov` and the Virtual Solar Observatory are **archives**, correctly recorded under Field 17 (Data Sources), not here.

---

### 33. Logo (OPTIONAL)
https://punch.space.swri.edu/images/punch-logo_240w.png

*Source: existing HSSI record. Verified live on 2026-07-28 (HTTP 200, `image/png`). The repository also ships `docs/_static/logo.png`, but that is not a stable public URL, so the seeded value is kept. **Note:** SoMEF proposed `https://contrib.rocks/image?repo=punch-mission/punchbowl`, which is the contributors-avatar mosaic from `README.md:74`, not a logo — rejected.*

---

## Cross-cutting negative research

Recorded so a later refresh does not repeat the work:

- **PyHC registry — punchbowl is not a registered package.** All three registry files
  (`projects_core.yml`, `projects.yml`, `projects_unevaluated.yml`) were read in full and none
  contains a punchbowl entry, so no PyHC-curated keywords, logo or description were available to
  weigh against the other sources. Two of its companions, regularizePSF and CCSDSPy, *are* PyHC
  community packages, so the absence is specific to punchbowl rather than to the PUNCH software
  family, and it is not a quality signal.
