# HSSI Metadata Extraction Results

**HSSI Software ID:** 37a18000-2d1f-41db-afe6-6545f817bcb7
**Repository:** https://github.com/punch-mission/punchbowl
**Source Revision:** 527b32adf325ab23367925516117df67f4bf717f
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-10-29
**Validation Status:** PASS

*Unqualified line citations are at the header's Source Revision `527b32a`; passages that name `d2d44328` cite that revision.*

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

### 4. Software Functionality (RECOMMENDED)
*Before the 2026-07-28 extraction the HSSI record carried no software functionality values, so this entire classification is derived from the repository. Every subcategory below is listed together with its required parent category.*

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
  - *Evidence:* the package's stated purpose — "`punchbowl` is the science calibration code for the PUNCH mission" (`README.md:5`); `punchbowl/level1/` implements vignetting (`vignette.py`), photometric quartic calibration (`quartic_fit.py`, `photometric_calibration`), PSF correction (`psf.py`), stray light removal (`stray_light.py`, `dynamic_stray_light.py`); `punchbowl/cli.py` `create_calibration()` generates calibration products. Release 0.0.25 added dynamic stray-light correction for NFI ("Add code for nfi dynamic stray light processing.", `CHANGELOG.rst` 0.0.25): `punchbowl/level1/nfi_dynamic_stray_light.py:181` `remove_nfi_stray_light`, which the Level 1 flow calls (`punchbowl/level1/flow.py:373`), builds forward matrices for the sky, per-pixel instrument and stray-light components (`punchbowl/level1/nfi_modules/fwdmats.py:39` `generate_nfi_forward_matrices`) and inverts them (`punchbowl/level1/nfi_modules/reconstruct.py:8` `reconstruct_nfi_straylight`), read at `d2d44328`.
- Data Processing and Analysis:Image Processing
  - *Evidence:* `punchbowl/level1/despike.py`, `destreak.py`, `deficient_pixel.py`, `psf.py`; `punchbowl/level2/resample.py` (`reproject_cube`); `punchbowl/level2/bright_structure.py` (ZSPIKE voting algorithm); `punchbowl/level3/stellar.py`; the NFI PCA background filter `punchbowl/level2/nfi_pca.py:38` `pca_filter`, which inpaints planets, the Moon and saturated pixels before fitting (`skimage.restoration.inpaint_biharmonic`, line 510) and replaced `punchbowl/levelq/pca.py` in release 0.0.25 (read at `d2d44328`); `skimage` is imported in 4 modules at `527b32a` and in 5 at `d2d44328`.
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
  - *Evidence:* PUNCH is a polarimeter and punchbowl resolves optical (Stokes-like) polarization as a primary function — `punchbowl/data/wcs.py:36` registers custom Stokes symbols `pB`/`B` via `astropy.coordinates.custom_stokes_symbol_mapping`; `punchbowl/level2/polarization.py:37` `solpolpy.resolve(data_collection, outsys)`; `punchbowl/level3/polarization.py` `convert_polarization`; `punchbowl/level3/stellar.py` `polarize_solar_to_celestial` / `polarize_celestial_to_solar`; the quasi-Stokes B/pB/pB′ and M,Z,P tri-polarizer systems are described in `docs/data/data_overview.rst`. **Scope note:** this is *optical/Thomson-scattering* polarimetry (Stokes parameters of light), not plasma-wave polarization. It is included because the field file lists this subcategory's indicators as "Stokes parameters, polarization ellipse, wave analysis methods", and punchbowl resolves Stokes parameters directly as a primary function.
- Data Processing and Analysis:ML/AI
  - *Evidence (read at `d2d44328`):* `punchbowl/level2/nfi_pca.py:19` `from sklearn.decomposition import PCA`. `pca_filter` (line 38) fits unsupervised PCA components to a batch of NFI images, generates a dynamic stray-light model for each image from those components and subtracts it (its docstring, steps 5-6); `find_outliers_with_pca` (line 557) uses a PCA fit to exclude out-of-distribution frames first. QuickPUNCH reuses the fitted components through `punchbowl/levelq/quickpunch_pca.py:26` `quickpunch_pca_filter`. Release 0.0.25 introduced this science-pipeline PCA ("Added re-vamped NFI PCA filtering, to be used in the science pipeline", `CHANGELOG.rst` 0.0.25) and removed `punchbowl/levelq/pca.py`, whose `run_pca_filtering` (line 173 at `527b32a`, importing PCA at line 14) this value cited until then; the capability stayed and widened from QuickPUNCH to the NFI science products.

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
  - *Evidence:* `lmfit` `Parameters`/residual minimisation in `punchbowl/level1/alignment_parallel.py:74` `_residual` and `punchbowl/level1/stray_light.py:136` `_resid_skew` / `fit_skew`; `punchbowl/level1/alignment.py` `solve_pointing` iteratively forward-projects a Gaia catalog and minimises star-position residuals; `punchbowl/level1/quartic_fit.py` fits quartic photometric coefficients. Since release 0.0.25 the NFI stray-light correction is a forward-fitting inversion too: `punchbowl/level1/nfi_modules/solver.py:66` `sparse_nonlinear_map_solver` minimises chi-squared plus regularisation over the NFI forward model and "Uses the log mapping and iteration from Plowman & Caspi 2020 to ensure positivity of solutions" (line 93), read at `d2d44328`.
- Models and Simulations:Mission-Specific
  - *Evidence:* all of the above models are PUNCH-specific (WFI/NFI PSFs, PUNCH trefoil-mosaic F-corona, PUNCH stray-light phases); `punchbowl/auto/flows/simulate.py` generates PUNCH-specific synthetic observations via `simpunch`.

**Servers and Environments**
- Servers and Environments
- Servers and Environments:Data servers processing and handling
  - *Evidence:* `punchbowl/auto/control/db.py` + `prefect_sqlalchemy.SqlAlchemyConnector` back the SOC file database (MariaDB/MySQL — `README.md` testing section, `pymysql` in the `pipe` dependency group); `punchbowl/auto/control/launcher.py` / `processor.py` are long-running server processes; `gunicorn` serves the dashboard.
- Servers and Environments:High Performance Computing
  - *Evidence:* `punchbowl/auto/cluster.py` starts and dynamically scales a `dask.distributed.LocalCluster`; `punchbowl/util.py:109,159,200` `@numba.njit(parallel=True)` with `numba.prange`; `multiprocessing` / `concurrent.futures.ProcessPoolExecutor` used across `punchbowl/data/punch_io.py`, `level1/stray_light.py` and `level2/nfi_pca.py` (read at `d2d44328`; `levelq/pca.py` until release 0.0.25); `threadpoolctl`/`limit_threads` helpers (CHANGELOG 0.0.24, PR #970); whole-pipeline memory capping (PR #867).
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
- *Release 0.0.25 and `main` to `d2d44328`.* The whole vocabulary was walked again against the code at `d2d44328`. The release's NFI stray-light inversion, NFI PCA filtering, colormap module (`punchbowl/data/color.py`) and daily quicklook flow (`punchbowl/auto/flows/quicklook.py`) support values already listed and add none. `Mission-related: ML/AI` and `Mission-related: Infrastructure as Code` would restate `Data Processing and Analysis: ML/AI` and `Servers and Environments: Infrastructure as Code` (rule 9). `Models and Simulations: Physics-Based` was rejected for the stray-light forward model, which models the instrument rather than a physical system and is carried by the two Instrument Response values. Case-insensitive sweeps of `punchbowl/` (tests excluded) for `wavelet`, `spectrogram`, `mplot3d`, `assimilat`, `hodogram`, `mhd` and `field.?line` matched nothing, while `forward.?model|forward matri` matched the new NFI modules; the tree holds no Dockerfile or other container definition.

---

### 5. Related Region (RECOMMENDED)
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

*Release 0.0.25's GitHub notes list @Rokkaan5 under "New Contributors" for pull request #1012, the NFI stray-light code. That account commits as Jasmine Kobayashi (`Jasmine Kobayashi <70308626+Rokkaan5@users.noreply.github.com>` in `git log 527b32a..d2d44328`), author 3 above, so it adds no author. The declared author lists did not change: `CITATION.cff` and the `pyproject.toml` `authors` are identical at `527b32a` and `d2d44328`, and the 0.0.25 Zenodo deposit (https://doi.org/10.5281/zenodo.23421836) lists the same 15 creators, in the `CITATION.cff` order.*

---

### 7. Software Name (MANDATORY)
punchbowl

*Source: existing HSSI record; `CITATION.cff` `title: "punchbowl"`; `pyproject.toml` `name = "punchbowl"`; Zenodo record title `punchbowl`; PyPI project `punchbowl`.*

---

### 8. Description (MANDATORY)
punchbowl contains the science processing calibration code for use with data from the Polarimeter to UNify the Corona and Heliosphere (PUNCH) mission. It provides the primary software modules in use by the mission processing pipeline for calibrating data, also available directly to science community users. The repository also contains software tools for handling PUNCH data, along with example notebooks. Since version 0.0.21 it has also incorporated the former punchpipe package as the punchbowl.auto subpackage, which supplies the Science Operations Center automation layer: telemetry ingest and Level 0 generation, Prefect-based flow scheduling and orchestration, a processing file database, and a monitoring dashboard.

*The submitter's three original sentences are preserved **verbatim**; a fourth sentence is appended because those three alone leave the description materially incomplete — an addition, not a stylistic rewrite of the submitter's wording. Evidence for the addition: `CHANGELOG.rst` line 221, "Moves punchpipe into punchbowl auto subpackage. (#771)"; `docs/automation/index.rst` — "This section is about what we used to call 'punchpipe.' It's how the SOC automates file generation on their servers."; `pyproject.toml` `[project.scripts] punchpipe = "punchbowl.auto.cli:main"`; the `punchbowl/auto/` tree (control, flows, monitor); `https://api.github.com/repos/punch-mission/punchpipe` reports `"archived": true`. HSSI held the sentence as "Since version 0.0.23 it has also incorporated…" from the 2026-07-28 refresh until the 0.0.25 release update, and that version number was wrong: at `527b32a`, `CHANGELOG.rst` line 221 sits in the section "0.0.21 (2026-02-20)" (lines 204–285); the merge of pull request #771 (`b49d833d`) is in the `0.0.21` tag and not in `0.0.20`; and `punchbowl/auto/` is absent at the `0.0.20` tag and present, with 58 files, at `0.0.21`. Only the number was corrected, since the rest of the sentence is accurate; a later refresh should not restore 0.0.23.*

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
- **Version Number:** 0.0.25
- **Version Date:** 2026-10-16
- **Version PID:** https://doi.org/10.5281/zenodo.23421836
- **Version Description:** exactly the text in the block below: a lead sentence, one blank line, then 30 lines each beginning `- `, joined by single newlines.

```text
Data version 0m candidate version.

- Add code for nfi dynamic stray light processing.
- Updates solar wind flow tracking modules to work with PUNCH data for initial activation.
- Implements daily quicklook movies and images.
- Improves starfield model generation and subtraction. A median background subtraction that is no longer needed was removed. This should improve capturing the Milky Way into the starfield models. This also allows for a single starfield model subtraction.
- For science images, use the timestamp of the image to set to polarization state of the image. Previously the PFW packet was used even if it was stale, producing erroneously-labelled images. The PFWSTAT header value now reads -1 if the PFW packet is stale.
- Added utilities to calculate a sliding-window percentile or run z-filtering in parallel.
- Flows can write output files in parallel, define more complex file relationships, and allow expected output files to not be produced.
- Added re-vamped NFI PCA filtering, to be used in the science pipeline
- Add scheduling layer for L2 PCA flow
- Add a L3 NFI flow to subtract the F corona and produce mosaic-frame intermediaries
- Include NFI images in CTM scheduling and production
- Include NFI images in CAM scheduling and production
- Add NFI QuickPUNCH flow
- Allow level 2 to skip including image based on configurable accepted phases.
- Change F-corona percentile from 3 to 2%.
- Fixed outlier flagging for L2+ products.
- Added the helioviewer tag to the JPEG2000 quicklook files. This will allow the image scaling of PUNCH data in Helioviewer to be correct.
- Fixes file writing to use operational config image scaling parameters.
- Corrects a bug with starfield model subtraction where the RA-axis cdelt was being accidentally sign flipped twice.
- Fix logic to avoid attempting regeneration of CAM/PAMs when some input files are severely delayed.
- Disable NFI statis stray light processing in the construct_stray_light_scheduler_flow
- Fix DSATVAL calculation to set NFI DSATVAL to 1254, but keep WFI DSATVAL at 1023.
- Add robots=off to wget command as part of recent umbra.nascom.nasa.gov permissions updates.
- We were previously clipping all negative values to 0. This led to negative values becoming transparent in JHelioviewer. This fixes that clipping bug by clipping to 1 instead.
- Improve starfield blur by reprojecting directly to the image frame instead of intermediate union WCS.
- Avoid crash in L0 flow if there aren't any replay needs
- Work around [astropy bug #20441](https://github.com/astropy/astropy/issues/20441), ensure that all WCS keywords including distortion keywords are written for both the helio and celestial WCS in level1 files.
- Avoid fall through for backprocessing if the children files list is empty.
- Flips RA coordinate cdelt in starfield model generation.
- Renamed L3_VAM to level3_VAM so it'll be found properly at deployment.
```

*Why 0.0.25 is the current release (rule 3):* `0.0.25` is a lightweight tag on commit `88bdea640f52ead17f86a798b16cdea974edd4ea` ("Merge pull request #1273 from punch-mission/release-0.0.25") on `main`; it is an ancestor of `d2d44328`, and `0.0.24` (`e83d02b3`) is an ancestor of it. GitHub release `0.0.25` is neither a draft nor a pre-release, and PyPI's JSON API lists `punchbowl-0.0.25.tar.gz`, not yanked, with `info.version` `0.0.25`; none of the 25 PyPI releases is yanked or a pre-release. The version is dynamic (`pyproject.toml` `dynamic = ["version"]`), so the tag is what declares it. The number is written without a `v`, as the tag, the release name and PyPI write it and as 0.0.24 was stored.

*Version date (rule 7):* the GitHub release was published 2026-10-16T15:43:14Z; the tagged commit is dated 2026-10-16T09:42:46−06:00 (15:42:46Z); PyPI's sdist was uploaded 2026-10-16T15:43:45Z; and the Zenodo deposit's `publication_date` and DataCite `Issued` are 2026-10-16. All agree.

*Version description (rules 10, 13–16):* the release name is the bare tag, and the release body is GitHub's auto-generated "What's Changed" list of 66 pull-request titles with contributor credits, so the text comes from the project's own `CHANGELOG.rst` section "0.0.25 (2026-10-16)", which is identical at the tag and at `d2d44328`. Its lead line and 30 of its 45 items are kept verbatim; each item's trailing pull-request link is dropped and one item wrapped across two source lines is joined. Dropped whole: "Sets up QuickPUNCH to run on new product types from clears." (#1019) and "Fix holes in L2 images after changing reprojection to run at 32 bits." (#1053, merged as `a41635b9` on 2026-07-21), which merged before the `0.0.24` tag and already stand in the 0.0.24 section, so they would carry the previous release's notes onto this one (rule 10); "Starfield model generation now logs progress messages in Prefect." (#1028, logging, and likewise already in the 0.0.24 section); "Better error reporting in import_export.py" and "productionify.py supports running to generate jp2s and/or .sha files without changing the version string" (operations scripts under `scripts/auto/`, outside the package); "FITS files output is buffered to speed hash file generation." (an internal write-path optimisation); "Change jpegls decoding package from pylibjpeg to imagecodecs." and "Pin versions of packages in the pyproject.toml." (dependency changes); and the section's three Documentation and four Internal Changes items (rule 14). The section headings "New Features" and "Bug Fixes" are not carried, because the reStructuredText underlines would render as markdown headings under "Release Notes"; every kept item reads on its own. "statis" in the NFI stray-light item is the project's spelling and is kept. Each of the 30 kept items either merged after the `0.0.24` tag or had its changelog fragment added after it, and none appears in the 0.0.24 section.

*Version PID (rule 17):* `10.5281/zenodo.23421836` is this release's GitHub-integration deposit. DataCite gives it `version` `0.0.25`, `IsSupplementTo https://github.com/punch-mission/punchbowl/tree/0.0.25` and `IsVersionOf 10.5281/zenodo.14029123`, and the concept's `HasVersion` list includes it. The DOI resolves.

*Superseded values.* HSSI held 0.0.24 (release date 2026-07-28, version PID https://doi.org/10.5281/zenodo.21640289) until the 0.0.25 release update. That release was correctly dated and its PID was its own deposit, but its stored description was a summary composed from the 0.0.24 changelog section rather than the section's own items, which rule 15 does not allow; nothing of it carries onto 0.0.25 (rule 10). Before the 2026-07-28 extraction HSSI held 0.0.19, five releases stale (the view API renders it `punchbowl - 0.0.19`; the prefix is a display transform).

*Release-history notes.*
- `CITATION.cff` still declares `version: 0.0.24` and `date-released: 2026-07-28`, both at the `0.0.25` tag and at `d2d44328`. The file was not updated for the release, so it is stale rather than evidence against 0.0.25.
- `main` carries 115 commits after the tag, up to `d2d44328` (2026-10-27), and towncrier fragments under `changelog/` that no release has rendered yet (among them `1195.feature.rst`, colormap registration; `1254.feature.rst`, sample data from SDAC; `1274.feature.rst`, MZP variance propagation; `1284.feature.rst`, faster Level 1 alignment). That code is unreleased (rule 2); the Read the Docs build of `main` calls itself `0.0.26.dev115`. A later release update should look for 0.0.26.

---

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source: existing HSSI record; `pyproject.toml` `requires-python = ">=3.12,<3.15"` and the `.github/workflows/ci.yaml` test matrix `["3.12", "3.13", "3.14"]`, read at `d2d44328`; release 0.0.25 raised the floor from Python 3.11 (`>=3.11,<3.15` and a matrix starting at `"3.11"` at `527b32a`), and PyPI gives 0.0.25 `requires_python` `<3.15,>=3.12`. **Note:** SoMEF also reports "Shell" for the repository (a handful of helper scripts such as `scripts/L3_PAM_CAM_filecounts.sh`); not added, because the form asks only for "the most important languages" and Shell is incidental here.*

---

### 14. Reference Publication (OPTIONAL)
Not found

*`CITATION.cff` contains no `preferred-citation`; the maintainers' stated citation is the software DOI itself ("If you use this software, please cite it as below.", `CITATION.cff` line 2). The closest candidate — Hughes et al. (2023), "Interoperability of PUNCH software in the Python ecosystem", https://doi.org/10.5281/zenodo.8412310, whose abstract explicitly describes punchbowl as "the core PUNCH pipeline package" — was considered and not promoted to this field: the maintainers name no reference publication of their own, and the record is a Zenodo Presentation, an 8-slide deck, which rule 2 keeps out of this field. It has since been removed from Related Publications as well (Field 27, *Superseded entry*). The developers' DASH 2023 and 2025 decks about punchbowl itself (Field 27) are slide decks too, and rule 2 excludes them here on the same ground. The PUNCH mission paper (DeForest et al. 2026, https://doi.org/10.1007/s11207-026-02608-2, Field 27) never names punchbowl, so it is not this software's paper either: rule 6 needs a paper that names the software or presents its code. It defers its account of the Science Operations Center to "Hughes, M., one, two, three: 2025, The Science Operations Center (SOC) for the Polarimeter to UNify the Corona and Heliosphere (PUNCH) mission. Solar Physics in work."; on 2026-10-29 ADS held no such article, only meeting abstracts by Hughes on the SOC. When that paper is published, a later update should test it under rule 6 as the paper describing punchbowl.*

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
- stray light (new row; no live row in any case, separator or plural variant) — *a signature technique: Level 1 removes static and dynamic stray light (`punchbowl/level1/stray_light.py`, `dynamic_stray_light.py`; its own pipeline page, `docs/pipeline/level1/stray_light.rst`), and release 0.0.25 added the NFI dynamic stray-light inversion `punchbowl/level1/nfi_dynamic_stray_light.py:181` `remove_nfi_stray_light`. Read at `d2d44328`.*
- f-corona (new row) — *punchbowl builds and subtracts F-corona models (`punchbowl/level3/f_corona_model.py` `construct_f_corona_model`; `docs/pipeline/level3/f_corona.rst`, "F-Corona Removal"), which SDAC registers as datasets (Field 28). Per-observatory models already existed at 0.0.24; release 0.0.25 extended F-corona modelling to NFI, with the `level3_NFI_*` flows in `punchbowl/auto/flows/level3.py` (lines 514 and 539; pull request #1226), observatory `N` in `punchbowl/auto/flows/fcorona.py` (line 25), and PCA-based F-corona models (commit `54780b92`). Written with the project's hyphen ("The F-corona - light emitted from scatted dust within the solar system - must be removed", `docs/pipeline/level3/f_corona.rst`), lower-case. Read at `d2d44328`.*
- starfield (new row) — *punchbowl generates and subtracts starfield models (`punchbowl/level3/stellar.py:253` `generate_starfield_background`; line 282 writes the PSM and CSM products; `docs/pipeline/level3/starfield.rst`), which SDAC registers as datasets (Field 28); release 0.0.25 reworked their generation and subtraction (pull requests #1134, #1145, #1180). Read at `d2d44328`.*

*Considered and rejected:* `python` and `fits` — the field is for "science keywords … not supported by other metadata fields", and these duplicate Field 13 and Fields 18/19. `principal component analysis` — the NFI PCA filter is how punchbowl removes NFI's variable stray light, which `stray light` now carries, and as a technique keyword it would mostly restate the Field 4 `Data Processing and Analysis: ML/AI` value (rule 6). `helioviewer` and `jpeg2000` would restate Field 30 and Field 19. The project's declared keywords did not change in release 0.0.25: the `pyproject.toml` `keywords` and `CITATION.cff` are identical at `527b32a` and `d2d44328`, and the repository topics were still `image`, `nasa`, `nasa-data`, `punch`, `solar-physics` and `solar-wind` on 2026-10-29. punchbowl is not a PyHC package (see *Cross-cutting negative research*), so the `pyhc package` marker does not apply.

---

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific — *Source: existing HSSI record; `punchbowl/data/fido/client.py` `PUNCHClient` is a PUNCH-specific client reading the SDAC PUNCH tree; `punchbowl/auto/flows/level0.py` ingests PUNCH spacecraft telemetry directly. Cross-listed with Fields 31/32 as instructed.*
- The Virtual Solar Observatory. — *Source: existing HSSI record; `docs/data/access.rst` — "stored and accessible through the Solar Data Analysis Center (SDAC) - a portal for hosting through tools such as the Virtual Solar Observatory (VSO). From here PUNCH data products can be queried and requested for download"; `examples/querying_data.py` — "how to query PUNCH data from the SDAC / VSO using Python tools". The trailing period is part of the controlled value, not sentence punctuation: the stored `DataInput` vocabulary row is named `The Virtual Solar Observatory.`, and the bare form without it matches no row.*
- HTTP/HTTPS Directories — *Source: `punchbowl/data/fido/client.py:22-23` — `fits_rootdir = "https://umbra.nascom.nasa.gov/punch"`, `jp2_rootdir = "https://umbra.nascom.nasa.gov/punch/L"`, scraped with `sunpy.net.scraper.Scraper` over a dated directory `pattern`; `docs/data/access.rst` documents the equivalent `wget -r -l1 --no-parent … https://umbra.nascom.nasa.gov/punch/3/CAM/2025/09/21/`; `punchbowl/data/sample.py` downloads its sample files over HTTPS: at `527b32a` from `https://data.boulder.swri.edu/lowder/PUNCH/sample/` (line 19), and at `d2d44328`, after a change on `main` that no release had shipped by 2026-10-29 (`changelog/1254.feature.rst`), from their SDAC locations under `https://umbra.nascom.nasa.gov/punch/` (line 18), falling back to `https://github.com/punch-mission/punch-sample-data/raw/main/` (line 19). Release 0.0.25 added `-e robots=off` to the documented `wget` example after permission changes on `umbra.nascom.nasa.gov`.*

*Considered and rejected:* `S3/Cloud-aware` — `punchbowl/auto/flows/levelq.py:602-609` uploads QuickPUNCH products **to** a NOAA S3 bucket, but this field is defined as "[t]he data **input** source the software supports" (emphasis added) and punchbowl never reads from S3.

---

### 18. Input File Formats (RECOMMENDED)
- FITS — *Source: existing HSSI record; `punchbowl/data/punch_io.py:395` `load_ndcube_from_fits`, `load_many_cubes`; `docs/data/access.rst`, "Reading Data".*
- csv — *Source: `punchbowl/data/meta.py:42` `pd.read_csv(path, na_filter=False)` loads the omniheader/level metadata templates; `punchbowl/level1/alignment.py:153,168` `load_gaia_catalog(... "gaia_catalog.csv")`; `punchbowl/auto/cli.py:273` and `punchbowl/auto/flows/level0.py:1290` `pd.read_csv`; `scripts/auto/prepare_packet_definition_csv_files.py`.*
- JSON — *Source: `json.load` used in 8 places, including pipeline/quicklook configuration and cached state (`punchbowl/auto/control/util.py`, `punchbowl/auto/flows/level0.py`).*
- Other — *Covers: raw CCSDS telemetry (TLM) packet files (`punchbowl/auto/flows/level0.py`, `ccsdspy.utils.split_by_apid`); JPEG-LS-compressed image packets, decoded with `imagecodecs` `jpegls_decode` since release 0.0.25 (line 633 at `d2d44328`; `pylibjpeg.decode`, line 624, at `527b32a`). The release notes call the decoder a "jpegls decoding package", so these packets are JPEG-LS, not the JPEG2000 an earlier version of this note named; Excel packet-definition workbooks (`pd.read_excel`, line 198); NumPy `.npy` square-root decode tables (`punchbowl/level1/sqrt.py:71-105`); YAML pipeline configuration (`punchbowl/auto/control/util.py` `load_pipeline_configuration`).*

*Considered and rejected:* `HDF5` — `h5py>=3.15` is declared in the `super_user` extra but is never imported anywhere in `punchbowl/`. `CDF`, `netCDF3/4`, `IDL.sav`, `Zarr`, `ISTP-Compliant`, `ascii` — no supporting code.

---

### 19. Output File Formats (RECOMMENDED)
- FITS — *Source: existing HSSI record; `punchbowl/data/punch_io.py:285` `write_ndcube_to_fits` (RICE-compressed, with uncertainty HDU and provenance BinTable — `_make_provenance_hdu`, `_pack_uncertainty`); `docs/data/access.rst`.*
- csv — *Source: `punchbowl/auto/cli.py:350` `result_df.to_csv(output_file_soc, index=False)`; `punchbowl/auto/flows/level0.py:1296` `new_table.to_csv(df_path, index=False)`; `punchbowl/level1/alignment.py:57` writes the Gaia catalog with `.to_csv(out_path)`.*
- JSON — *Source: `json.dump` used in 33 places (flow state, cache and dashboard artefacts across `punchbowl/auto/`).*
- Other — *Covers: JPEG2000 quicklooks (`punchbowl/data/punch_io.py:105` `write_ndcube_to_quicklook` via `glymur.Jp2k`, with an XML metadata box from `_generate_jp2_xmlbox`); MP4 animations (`write_quicklook_to_mp4`, line 242; `punchbowl/data/visualize.py:135` `animate_punch`); NumPy `.npz`/`.npy` (`punchbowl/limits.py:164` `np.savez`, `punchbowl/level1/sqrt.py:95,105` `np.save`); `.sha256` checksum sidecars (`punchbowl/data/punch_io.py:43` `write_file_hash`, suffix at line 51, read at `d2d44328`; the suffix was `.sha` at `527b32a`, line 47); and, since release 0.0.25, JPEG daily quicklook images beside the MP4 daily movies (`punchbowl/auto/flows/quicklook.py:217-225`). Release 0.0.25 also adds a Helioviewer element to each JPEG2000 quicklook's XML metadata box (`punchbowl/data/punch_io.py:76` `_create_meta_for_helioviewer`; see Field 30). No live FileFormat row names JPEG, JPEG2000, MP4 or NumPy formats, so `Other` carries them.*

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

*Before the 2026-07-28 extraction the HSSI record carried no development status. Source: 25 tagged releases, the newest, `0.0.25`, published 2026-10-16, and 25 PyPI releases; the last commit on `main`, `d2d44328`, is dated 2026-10-27; GitHub reported the repository not archived on 2026-10-29; and the code is in operational use generating the PUNCH mission's public data products. (At the extraction revision `527b32ad` there were 24 releases, the newest `0.0.24` of 2026-07-28.)*

*Decision (fields/23).* Rules 1–3 do not fire: nothing points to a new location, GitHub reported the repository not archived on 2026-10-29, and the README carries no repostatus.org badge. Rule 4 asks which term's full definition an explicit project status statement matches. The README's caution (`README.md` lines 9-11, unchanged at `d2d44328`) reads "This package is still being heavily edited as calibration algorithms are improved. Stability is not promised until v1." Its first sentence matches the second half of `Active`, "The project has reached a stable, usable state and is being actively developed."; its second withholds a stability promise for future versions, which no RepoStatus definition addresses. It does not match `WIP`, "Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.", because it claims neither initial development nor the absence of a public release, and the same README directs users to one: "Install with `pip install punchbowl` to get the released version." With 25 releases on PyPI and the code producing the mission's public data products, a stable, usable release suitable for the public exists. Rule 4 therefore gives no term but `Active`, rule 5 does not fire, and rule 6 gives `Active`: the last commit on `main` (2026-10-27) was under six months old when this was decided on 2026-10-29. `pyproject.toml`'s `Development Status :: 4 - Beta`, also unchanged at `d2d44328`, is a Trove packaging classifier rather than a RepoStatus term; it corroborates that releases exist and is not mapped onto a row. If the project replaces the caution with a statement that matches `WIP` or another term, rule 4 decides on that statement.

---

### 24. Documentation (RECOMMENDED)
https://punchbowl.readthedocs.io/en/latest/

*Source: existing HSSI record; `README.md:7`; `pyproject.toml` `[project.urls] Documentation`; `.readthedocs.yaml`. URL verified live on 2026-07-28 and again on 2026-10-29, when the page title read "Welcome to punchbowl’s documentation!" for a build of `main` (`punchbowl 0.0.26.dev115 documentation`); `.readthedocs.yaml` is still present at `d2d44328`.*

---

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

*Source: existing HSSI record (already fully expanded, no acronym). Corroborated by `docs/intro.rst` — "PUNCH is a NASA Small Explorer (SMEX) mission". The repository contains no funding-acknowledgement file and the Zenodo/DataCite records carry an empty `fundingReferences` list, so no additional funder could be evidenced. The PUNCH mission paper (DeForest et al. 2026, Field 27) gives the mission's own attribution — "PUNCH is a heliophysics mission to study the corona, solar wind, and space weather as an integrated system, and is part of NASA’s Explorers program" — and the PUNCH contract (Field 26) is NASA's, which corroborates this funder for the program whose product punchbowl is (rule 8). The same paper's acknowledgements also credit the National Science Foundation's cooperative agreement for NCAR and NASA's IMAP mission, each for named individual authors; both are person-level support (rule 3) and are not recorded.*

---

### 26. Award Title (OPTIONAL)
- **Award Title:** Polarimeter to UNify the Corona and Heliosphere (PUNCH)
- **Award Number:** 80GSFC18C0014
- **Award Funder:** National Aeronautics and Space Administration — https://ror.org/027ka1x80 (as Field 25 records it; HSSI's award record already names this funder)

*Award Title source: existing HSSI record; the mission name is confirmed in `docs/intro.rst` and `punchbowl/data/fido/client.py` — `a.Source: [("PUNCH", "Polarimeter to UNify the Corona and Heliosphere")]`.*

*Award Number `80GSFC18C0014` was previously recorded here as "Not found" because the HSSI software view does not render award numbers. The existing HSSI association pairs that number with the PUNCH award title, so the value is retained rather than discarded.*

***Corroboration (2026-10-29).** USAspending's contract record for `80GSFC18C0014` (`spending_by_award`, contract types A–D) is NASA's award to Southwest Research Institute, running 2017-11-22 to 2027-12-02 with an award amount of $143,551,156.57; its description opens "UNDER THIS CONTRACT, THE CONTRACTOR WILL PROVIDE THE PERSONNEL,  MATERIALS, EQUIPMENT, AND FACILITIES NECESSARY TO PRODUCE THE POLARIMETER TO UNIFY THE CORONA HELIOSPHERE (PUNCH) PHASE A CONCEPT STUDY", the stage at which the contract began. The number is therefore the PUNCH mission contract, which funds the program whose product punchbowl is (rule 1). The PUNCH mission paper (DeForest et al. 2026, Field 27) prints the mission's acknowledgement as "Contract 80GSFC14C0014", in its Section 6 data-use statement and in its Acknowledgements; USAspending returns nothing for `80GSFC14C0014` in any award-type group (contracts, indefinite-delivery vehicles, grants, direct payments, loans and other), as it returns nothing for a nonsense control, while `80GSFC18C0014` resolves to the PUNCH contract. In ADS full text the `80GSFC14C0014` string recurs in five PUNCH-related records of 2026 (2026SoPh..301...16D, 2026SoPh..301...33G, 2026SoPh..301..112L, 2026arXiv260728506D and 2026arXiv260723043D), while `80GSFC18C0014` appears in seven, including the earlier PUNCH papers 2022ApJ...927...98D and 2023AJ....165..204H; a nonsense award string returns none. The paper's number is therefore the team's recurring 2026 acknowledgement string; it is not an award USAspending holds, and the stored number stands (rule 14); a later refresh should not "correct" it to the paper's form. Before this check the number could be tied only to DeForest's SwRI solar work, through NASA NTRS record `20220017302` ("The Coronal Veil", Malanushenko, Cheung, **DeForest**, Klimchuk & Rempel, `CONTRACT_GRANT: 80GSFC18C0014`), and was recorded as a pre-existing HSSI value that could not be confirmed as the PUNCH award.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
*Before the 2026-07-28 extraction the HSSI record carried no related publications. The entries are publications the project itself cites for its methods (rule 4) and the developers' own publications about the software or about the mission it serves (rule 3).*

- https://doi.org/10.1023/B:SOLA.0000021743.24248.b0 — DeForest, C. E. (2004). *On Re-sampling of Solar Images*. Solar Physics. — *Evidence: cited in `docs/pipeline/level2/image_resample.rst:11` as the algorithm behind the adaptive reprojection used by `punchbowl/level2/resample.py` `reproject_cube`.*
- https://doi.org/10.3847/1538-4357/ac43b6 — DeForest, C. E., Seaton, D. B., & West, M. J. (2022). *Three-polarizer Treatment of Linear Polarization in Coronagraphs and Heliospheric Imagers*. The Astrophysical Journal. — *Evidence: cited in `docs/data/data_overview.rst:18` as the definition of the B/pB/pB′ and M,Z,P polarization systems that `punchbowl/level2/polarization.py` and `punchbowl/level3/polarization.py` implement.*
- https://doi.org/10.3847/1538-4357/abc260 — Plowman, J., & Caspi, A. (2020). *A Fast, Simple, Robust Algorithm for Coronal Temperature Reconstruction*. The Astrophysical Journal, 905(1), 17. — *Evidence (rule 4): the solver behind the NFI dynamic stray-light correction that release 0.0.25 added names this paper as its method. `punchbowl/level1/nfi_modules/solver.py:12-14` describes "the general linear operator for chi squared plus regularization with nonlinear mapping as outlined in Plowman & Caspi 2020", and line 93 says the solver "Uses the log mapping and iteration from Plowman & Caspi 2020 to ensure positivity of solutions" (read at `d2d44328`). The solver names only "Plowman & Caspi 2020", with no title or DOI; an ADS author search for Plowman and Caspi over 2018–2021 returns one article, 2020ApJ...905...17P (this paper), beside two ASCL software records and a meeting abstract, so the reference is unambiguous. Title, venue and authors from Crossref; Joseph Plowman is also a punchbowl author (Field 6).*
- https://doi.org/10.1007/s11207-026-02608-2 — DeForest, C. E., Gibson, S. E., Killough, R., et al. (2026). *Polarimeter to Unify the Corona and Heliosphere (PUNCH)*. Solar Physics, 301, 16; arXiv:2509.15131. — *Evidence (rule 3, a developers' publication about the platform the software serves): the PUNCH mission paper, whose 78 authors include the punchbowl authors DeForest (its first author and the mission's principal investigator), Seaton, Hughes, Attié, Lamb, Lowder, Patel and West. It never names punchbowl: ADS `full:"punchbowl"` on bibcode `2026SoPh..301...16D` returns nothing, while `full:"Thomson"` on the same bibcode matches. Its Section 6, "Data products and Ground Pipeline", summarises the Science Operations Center processing that punchbowl implements: Level 0 files unpacked from the downlinked CCSDS packet stream; the Level 0 to Level 1 steps, including square-root decoding, destreaking, stray-light removal and PSF regularization; Level 2 mosaics merged across spacecraft; Level 3 subtraction of the F-corona and stellar backgrounds; and the QuickLook and QuickPUNCH products. Its data-use statement gives the acknowledgement the mission asks users to make (see Field 26 for its contract number, which differs from the PUNCH contract's). Title, venue and authors from Crossref.*
- https://doi.org/10.3847/2515-5172/ad0b0d — Patel, R., Seaton, D. B., Caspi, A., Kovac, S. A., et al. (2023). *A Chromatic Treatment of Linear Polarization in the Solar Corona at the 2023 Total Solar Eclipse*. Research Notes of the AAS, 7(11), 241. — *Evidence (rule 4): the project's documentation gallery names it, beside DeForest et al. (2022) above, as the formalism its RGB maps follow: "These data are mapped to MZP triplets, which are then mapped to RGB components based on the formalism presented in DeForest et al. (2022) and Patel et al. (2023)." (`examples/create_rgb_map.py:7`, read at `d2d44328`; the example's docstring names the same two papers at `527b32a` and at the `0.0.25` tag). At `d2d44328` the example demonstrates `punchbowl/data/visualize.py:114` `generate_tbpb_to_rgb_map`, which entered `main` after the `0.0.25` tag (commit `809bf110`, 2026-10-08); at the tag it demonstrates `generate_mzp_to_rgb_map` (line 66 there, line 53 at `d2d44328`). Neither function's own docstring cites the papers; the example's does. The paper converts polarized eclipse observations to −60°, 0° and +60° (MZP) polarization channels and renders them as the R, G and B colour channels; its authors include the punchbowl authors Patel, Seaton, Kovac, DeForest and West. A Research Note of the AAS is editor-moderated rather than refereed, a kind the field's list of eligible publication types does not name; the catalogue's maintainer ruled on 2026-10-29 that a published, DOI-registered RNAAS note is an eligible publication. Title, venue and authors from Crossref.*

*Superseded entry.* HSSI listed https://doi.org/10.5281/zenodo.8412310 — Hughes, J. M., DeForest, C., Kovac, S., Lowder, C., Patel, R., Seaton, D., & West, M. J. (2023), "Interoperability of PUNCH software in the Python ecosystem" — from the 2026-07-28 refresh until the 0.0.25 release update. It is a Zenodo Presentation (DataCite `resourceType` `Presentation`): its one version, https://doi.org/10.5281/zenodo.8412311, holds a single 8-slide PowerPoint file, `hughes_marcus_dash_punch.pptx`, from the DASH 2023 conference, with about 410 words of headings and short bullets, one slide that only points to a live demo, and no results. Its DataCite abstract names punchbowl as "the core PUNCH pipeline package", but the deck is about the interoperability of PUNCH software in general, chiefly regularizePSF and solpolpy. The field admits a slide deck only as a substantial standalone document, and the catalogue's maintainer confirmed on 2026-10-29 that this one is not, so it was removed (rules 1 and 7). A later refresh should not restore it.

*Literature search, 2026-10-29 (the first this section records; the extraction was on 2026-07-28).* ADS/SciX `full:"punchbowl"`, alone and combined with `PUNCH`, `corona`, `heliosphere` or `sunpy`; `ack:"punchbowl"`; `full:"zenodo.14029123"`; and `full:"punch-mission/punchbowl"`, with `full:"qzxwvplk"` returning 0 and `full:"regularizepsf"` returning four records as controls; ADS title and author searches for PUNCH Science Operations Center, pipeline and mission papers; DataCite, where the concept DOI has a `citationCount` of 0 and no `IsCitedBy` relation; and Semantic Scholar, which does not index the concept DOI. Most `full:"punchbowl"` hits are the Punchbowl fault of the San Andreas system and other namesakes, and no third-party paper credits the software. Weighed and not added:
- meeting abstracts (rule 1): 2021AGUFMSH55A1824H, 2024AGUFMSH23B2943H, 2025AAS...24612603H, 2025AAS...24612604L, 2025AGUFMSH11E2095H and 2026SPD....5710402V, all by punchbowl authors on the SOC, its data products or their use;
- the instrument papers for NFI (Colaninno et al. 2025, https://doi.org/10.1007/s11207-025-02506-z) and WFI (Laurent et al. 2026, https://doi.org/10.1007/s11207-026-02706-1), which describe hardware whose data punchbowl processes rather than the software or the mission as a whole;
- "PUNCH Mission Planning and Operations" (Lamb et al., a DASH 2025 Zenodo presentation, https://doi.org/10.5281/zenodo.17382378), which is about mission planning, not this software;
- "Ladling Data from the Heliosphere with punchbowl" (Lowder et al., a DASH 2025 Zenodo presentation, https://doi.org/10.5281/zenodo.17382249, version https://doi.org/10.5281/zenodo.17382250, deposited as PowerPoint, PDF and Keynote files): a 15-slide deck of about 500 words with no speaker notes, 2 of whose slides carry no text (a first-light movie and a screenshot of the GitHub repository). Its finished Level 0 to Level 3 data-flow diagram can be followed without the talk, but the rest is headings and bullet fragments with no results, and it shows punchbowl as it stood at 0.0.19 (the screenshot reads "0.0.19 Latest"), with punchpipe still a separate package, before punchpipe was merged into punchbowl. Its PDF expands the animation builds into 27 pages, so a page count overstates its length. The catalogue's maintainer weighed it on 2026-10-29, including as a replacement for the 2023 deck above, and listed neither: it does not read as a substantial standalone document;
- "punchbowl - A Data Processing Pipeline from a Four-Satellite Constellation Observatory" (Lowder et al., a DASH 2023 Zenodo presentation, https://doi.org/10.5281/zenodo.8412194, version https://doi.org/10.5281/zenodo.8412195): one 11-slide PowerPoint file of about 370 words of headings and short bullets, written before launch ("Will be open sourced post-launch"). It is about punchbowl, but as a deck of headings and images it does not read as a standalone document, and the catalogue's maintainer did not add it (2026-10-29);
- two papers the mission paper cites as in preparation, both for Solar Physics: Hughes et al., "The Science Operations Center (SOC) for the Polarimeter to UNify the Corona and Heliosphere (PUNCH) mission", and Seaton et al., "Punch data for space weather forecasting". ADS held neither on 2026-10-29. A later update should look for both; the first is about punchbowl itself (rule 3, and see Field 14).

---

### 28. Related Datasets (OPTIONAL)
*This field lists the **complete set of 53** Solar Data Analysis Center PUNCH dataset DOIs that DataCite held on 2026-10-29: the four collection DOIs plus 49 product DOIs. They were enumerated from the DataCite query `https://api.datacite.org/dois?prefix=10.48322&query=titles.title:PUNCH&page[size]=100`, which returned 43 on 2026-07-28; the ten registered on 2026-08-19 and 2026-09-18 are grouped last. No DOI suffix was pattern-generated. Titles below are reproduced **verbatim from DataCite**, including the registry's own typos ("puls 60", the double space in "Level 3  Low-noise") and its mixed "Level 3" and "Level-3".*

**Collection DOIs already held in HSSI (4)**
- https://doi.org/10.48322/5k49-bh56 — PUNCH NFI-WFI Level 0 Science images — *existing HSSI record; DataCite publisher "Solar Data Analysis Center", 2025.*
- https://doi.org/10.48322/enbf-rh75 — PUNCH NFI-WFI Level 1 Science images — *existing HSSI record; DataCite verified.*
- https://doi.org/10.48322/stqs-j385 — PUNCH NFI-WFI Level 2 Science Dataset — *existing HSSI record; DataCite verified.*
- https://doi.org/10.48322/nnv7-bn21 — PUNCH NFI-WFI Level 3 Science Dataset — *existing HSSI record; DataCite verified.*

**Level 2 science products (2)**
- https://doi.org/10.48322/z829-zy89 — PUNCH Level2 Polarized Mosaics (Trefoil) Data — *product code PTM, produced by `punchbowl/level2/flow.py` `level2_core_flow` (`docs/data/data_overview.rst`, Level 2).*
- https://doi.org/10.48322/sv88-z093 — PUNCH Level2 Clear Mosaics (Trefoil) Data — *product code CTM, same flow.*

**Level 3 science products (6)**
- https://doi.org/10.48322/f6tk-sm20 — PUNCH Level 3 Polarized Mosaic Data in the MZP system — *product code PIM, the polarized mosaics with F-corona subtraction, without starfield subtraction and still in the MZP system (`docs/data/data_codes.rst`; the DOI's SPASE ID ends `Level3/PIM/PT4M`), written by `punchbowl/level3/flow.py:184` (`new_type = "PIM" if polarized else "CIM"`), read at `d2d44328`. An earlier version of this note gave PTM, the code of the final K-corona mosaics, which SDAC registered separately as https://doi.org/10.48322/0zsb-2c44 (below).*
- https://doi.org/10.48322/kxpb-q477 — PUNCH Level 3 Clear Mosaic Data — *product code CIM, the clear counterpart (SPASE ID ending `Level3/CIM/PT8M`), same line; an earlier version of this note gave CTM, the code of https://doi.org/10.48322/z3s9-1x36 (below).*
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

**Level 3 models and K-corona mosaics registered after 2026-07-28 (10)**
*Evidence (read at `d2d44328`): each is a product punchbowl writes (rule 5) and reads back through `punchbowl/data/punch_io.py` `load_ndcube_from_fits` (rule 3). Product codes from `docs/data/data_codes.rst` and each DOI's SPASE ID.*
- https://doi.org/10.48322/pe4q-mm17 — PUNCH Level 3 WFI-1 Polarized F-Corona Model
- https://doi.org/10.48322/pkmm-5p92 — PUNCH Level 3 WFI-2 Polarized F-Corona Model
- https://doi.org/10.48322/eeqw-x739 — PUNCH Level 3 WFI-3 Polarized F-Corona Model — *codes PF1–PF3, written by `punchbowl/level3/f_corona_model.py:155` (`NormalizedMetadata.load_template("PF" + obscode, "3")`) and taken as F-corona inputs by the Level 3 flow (`punchbowl/level3/flow.py:151-155`); DataCite records each as referencing the mosaic model https://doi.org/10.48322/dcpx-4r68.*
- https://doi.org/10.48322/3dne-5k54 — PUNCH Level-3 WFI-1 Unpolarized F-Corona Model
- https://doi.org/10.48322/mz36-vv57 — PUNCH Level-3 WFI-2 Unpolarized F-Corona Model
- https://doi.org/10.48322/b5xe-vw91 — PUNCH Level-3 WFI-3 Unpolarized F-Corona Model — *codes CF1–CF3, same module, line 159.*
- https://doi.org/10.48322/mdwg-ap12 — PUNCH Level 3 Polarized Mosaic Starfield Model
- https://doi.org/10.48322/kb0b-dw04 — PUNCH Level 3 Clear Mosaic Starfield Model — *codes PSM and CSM, written by `punchbowl/level3/stellar.py:282` (`NormalizedMetadata.load_template("PSM" if is_polarized else "CSM", "3")`).*
- https://doi.org/10.48322/0zsb-2c44 — PUNCH Level 3 Polarized K-Corona Mosaic Data
- https://doi.org/10.48322/z3s9-1x36 — PUNCH Level 3 Clear K-Corona Mosaic Data — *codes PTM and CTM at Level 3, the background-subtracted K-corona mosaics, written by `punchbowl/level3/flow.py:314` (`NormalizedMetadata.load_template("PTM" if is_polarized else "CTM", "3")`).*

*Completeness rationale:* the per-spacecraft, per-polarization Level 0 and Level 1 children are listed **alongside** their `PUNCH NFI-WFI Level 0/1 Science images` collection DOIs. The collections remain useful aggregate identifiers, while punchbowl produces and reads each child individually. The counts are asymmetric because that is what SDAC has registered: Level 0 has 15 children (NFI has only clear, minus-60 and zero states registered — there is no Level 0 NFI plus-60 DOI in DataCite) while Level 1 has 16. Together with the four collection, two Level 2 and sixteen Level 3 DOIs, these make the 53 PUNCH datasets DataCite held on 2026-10-29.

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

- https://github.com/Helioviewer-Project/helioviewer.org — **Helioviewer** — *Output imported into a named domain tool (rule 7). `punchbowl/data/punch_io.py:76` `_create_meta_for_helioviewer` ("Generate a helioviewer XML Tree so JPEG2000 files render properly.") builds a `<helioviewer>` element carrying `HV_ROTATION`, `HV_COMMENT` and `HV_SUPPORTED`, which `_generate_jp2_xmlbox` (line 107) appends to the XML metadata box (line 116) that `write_ndcube_to_quicklook` writes into every JPEG2000 quicklook (line 257), and `punchbowl/data/tests/test_punch_io.py:106-123` checks that a written file carries it. Release 0.0.25 added the box: "Added the helioviewer tag to the JPEG2000 quicklook files. This will allow the image scaling of PUNCH data in Helioviewer to be correct." (`CHANGELOG.rst` 0.0.25, pull request #1109). `docs/data/access.rst:39-40`: "PUNCH data are also accessible using the Helioviewer tool, where it can be quickly visualized and stitched together with other observations for context." Read at `d2d44328`. Helioviewer has no HSSI entry; the URL is the upstream repository root of the Helioviewer Project's web application ("Main web application for solar data visualization"), the form SolarSoft's HSSI entry already uses for Helioviewer.*
- https://github.com/Helioviewer-Project/JHelioviewer-SWHV — **JHelioviewer** — *Output tailored for a named domain tool (rule 7). The quicklook writer makes greyscale images because "JHelioviewer wants greyscale images" (`punchbowl/data/punch_io.py:213`); release 0.0.25 clips them at 1 rather than 0 because zero-clipping "led to negative values becoming transparent in JHelioviewer" (`CHANGELOG.rst` 0.0.25, pull request #1159); and an earlier data version "shifts a few keys for JHelioviewer compatibility" (`docs/data/data_versions.rst:62`, pull request #903). Read at `d2d44328`. JHelioviewer has no HSSI entry. The URL is the repository the JHelioviewer site (https://www.jhelioviewer.org/) links to; the older `https://github.com/Helioviewer-Project/JHelioviewer` is archived, last pushed 2020-11-24, and was passed over.*

*Considered and rejected — Tier A generic infrastructure (would be equally at home in a web app, finance model, or biology pipeline):* numpy, scipy, pandas, matplotlib, plotly, dash / dash-bootstrap-components, requests, python-dateutil, PyYAML, click, tqdm, setuptools, pytest (+ plugins), ruff/pre-commit/codespell, sqlalchemy / pymysql, fastapi, gunicorn, psutil, networkx, numexpr, threadpoolctl, coolname, freezegun, hypothesis, xlrd, lxml, toml, numpy-quaternion.
*Considered and rejected — domain-adjacent but no demonstrated peer exchange:* `reproject`, `photutils`, `sep`, `astrometry`, `lmfit`, `scikit-image`, `scikit-learn`, `numba`, `cupy`, `glymur`, `pylibjpeg` (a dependency until release 0.0.25, when `imagecodecs`, a generic codec library excluded under rule 2, replaced it for JPEG-LS decoding), `prefect` / `prefect-dask` / `prefect-sqlalchemy`, `dask`, `jupyter`.
*Considered and rejected — declared but unused:* `sunkit-image` and `h5py` appear in `pyproject.toml` but are never imported anywhere under `punchbowl/`.

---

### 31. Related Instruments (OPTIONAL)
*Before the 2026-07-28 extraction the HSSI record carried no related instruments. Every value below is resolved against the HSSI `InstrumentObservatory` controlled vocabulary (`type: 1`, instruments), and every identifier was additionally verified to resolve at spase-metadata.org. No bare names are emitted.*

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
*Before the 2026-07-28 extraction the HSSI record carried no related observatories. Every value below is resolved against the HSSI `InstrumentObservatory` controlled vocabulary (`type: 2`, observatories). All identifiers verified to resolve.*

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

*Source: existing HSSI record. Verified live on 2026-07-28 (HTTP 200, `image/png`) and again on 2026-10-29 (HTTP 200, `image/png`, a 240 × 316 PNG with SHA-256 `a102e3766bcdd8784da4758e204c58854ce26e6385ff36ddaa14b60ad2a99bfa`). The repository also ships `docs/_static/logo.png`, but that is not a stable public URL, so the seeded value is kept. **Note:** SoMEF proposed `https://contrib.rocks/image?repo=punch-mission/punchbowl`, which is the contributors-avatar mosaic from `README.md:74`, not a logo — rejected.*

---

## Cross-cutting negative research

Recorded so a later refresh does not repeat the work:

- **PyHC registry — punchbowl is not a registered package.** All three registry files
  (`projects_core.yml`, `projects.yml`, `projects_unevaluated.yml`) were read in full and none
  contains a punchbowl entry, so no PyHC-curated keywords, logo or description were available to
  weigh against the other sources. Two of its companions, regularizePSF and CCSDSPy, *are* PyHC
  community packages, so the absence is specific to punchbowl rather than to the PUNCH software
  family, and it is not a quality signal. Re-checked on 2026-10-29 at registry commit
  `f7b0421b08c2cbc614a8d68372b42428d3a53cb2`: still no punchbowl entry in any of the three files, while
  regularizePSF and CCSDSPy still match in `projects.yml`.
