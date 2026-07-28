# HSSI Metadata Extraction Results

**HSSI Software ID:** 37a18000-2d1f-41db-afe6-6545f817bcb7
**Repository:** https://github.com/punch-mission/punchbowl
**Source Revision:** 527b32adf325ab23367925516117df67f4bf717f
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-07-28
**Validation Status:** PASS
**Applied to HSSI:** 2026-07-28 — the approved update to `http://localhost/api/data/software/37a18000-2d1f-41db-afe6-6545f817bcb7/` returned **HTTP 200** (16 fields updated) and was roundtrip-verified. Two shared-`Person` renames and one duplicate-ROR affiliation, none of which the API can express, were then applied by an approved, guarded direct database correction and verified. See "Roundtrip verification" below.

**Seed:** Live HSSI record fetched from `GET http://localhost/api/view/software/37a18000-2d1f-41db-afe6-6545f817bcb7/` (saved at `/tmp/punchbowl_hssi_current.json`). No prior canonical `hssi_metadata.md` existed. Every field below was pre-populated from that record first, then gap-filled / corrected from the repository at revision `527b32ad`, PyPI, Zenodo/DataCite, ORCID, ROR, SPASE, and the PyHC registries.

**Change legend:** `UNCHANGED` = seeded HSSI value kept verbatim · `NEW` = field/value not present in HSSI · `REPLACED` = seeded value superseded by evidence (justified below and in the Proposed removals/replacements section) · `REMOVAL-PROPOSED` = seeded value deliberately withheld (none in this extraction).

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Status: N/A (not exposed by the HSSI view API).*

---

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.14029123

*Status: UNCHANGED. Source: existing HSSI record; confirmed as the Zenodo **concept** DOI — `https://zenodo.org/api/records/21640289` reports `"conceptdoi": "10.5281/zenodo.14029123"`. Also carried in `CITATION.cff` (`doi: 10.5281/zenodo.14029123`) and the `README.md` DOI badge (line 3).*

---

### 3. Code Repository (MANDATORY)
https://github.com/punch-mission/punchbowl

*Status: UNCHANGED. Source: existing HSSI record; confirmed by `git remote -v` (`origin https://github.com/punch-mission/punchbowl.git`), `CITATION.cff` `url:`, `pyproject.toml` `[project.urls] Repository`, and Zenodo `metadata.custom["code:codeRepository"]`.*

---

### 4. Software Functionality (MANDATORY)
*Status: NEW (HSSI record carries **no** software functionality values — this entire field is an addition). Every subcategory below is listed together with its required parent category. Classification performed with the `software-functionality` skill against revision `527b32ad`.*

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
  - *Evidence:* PUNCH is a polarimeter and punchbowl resolves optical (Stokes-like) polarization as a primary function — `punchbowl/data/wcs.py:36` registers custom Stokes symbols `pB`/`B` via `astropy.coordinates.custom_stokes_symbol_mapping`; `punchbowl/level2/polarization.py:37` `solpolpy.resolve(data_collection, outsys)`; `punchbowl/level3/polarization.py` `convert_polarization`; `punchbowl/level3/stellar.py` `polarize_solar_to_celestial` / `polarize_celestial_to_solar`; the quasi-Stokes B/pB/pB′ and M,Z,P tri-polarizer systems are described in `docs/data/data_overview.rst`. **Note for validator:** this is *optical/Thomson-scattering* polarimetry (Stokes parameters of light), not plasma-wave polarization; included because the subcategory is defined by "Stokes parameters / polarization ellipse". Flagged for reviewer judgement.
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
- Solar Environment — *Status: UNCHANGED (from existing HSSI record). Evidence: `docs/intro.rst` — PUNCH studies "how the mass and energy of the Sun's corona become the solar wind"; the L1–L3 products are coronal/heliospheric brightness images; NFI is a coronagraph observing the inner corona.*
- Interplanetary Space — *Status: NEW. Evidence: `docs/data/access.rst`, "Data Projections" — "The PUNCH WFI instruments extend their field of view out to around 45-degrees from the Sun, creating a meshed virtual observatory extending to a diameter of nearly 180 solar radii"; `docs/intro.rst` — PUNCH images "the entire inner solar system"; `punchbowl/level3/velocity.py` `track_velocity` derives solar-wind flow across that heliospheric field of view (L3 "VAM" product, `docs/data/data_overview.rst`).*

*Considered and rejected:* `Earth Atmosphere` — `punchbowl/level2/bright_structure.py` detects "high-altitude aurora" transients, but only to **flag them as artifacts** in the quality mask, not to support atmospheric science. `Earth Magnetosphere` / `Planetary Magnetospheres` — no supporting functionality (the GSE/GEI transforms in `level0.py` are spacecraft-ephemeris bookkeeping only).

---

### 6. Authors (MANDATORY)
*Status: union of the 10 existing HSSI authors + all 15 `CITATION.cff` authors, matched by ORCID. No author dropped. 5 authors are NEW to punchbowl; 2 (Attié, Kovac) had REPLACED name spellings that were **applied by approved direct database correction on 2026-07-28** and are now live; 1 (Van Kooten) had already been corrected directly in the shared database by a concurrent worker. Two names (Murphy, Badman) are recorded in the fuller live HSSI form rather than the shorter `CITATION.cff` form, per reviewer decisions A and B — `Person` is a shared entity with no per-entry name override. **Every name below now matches live HSSI exactly.** Order follows `CITATION.cff` (the maintainers' authoritative ordering). Affiliations are the identity-aware union of the HSSI affiliations (resolved from the HSSI Organization table at `http://localhost/api/models/Organization/rows/all/`) and repository/ORCID evidence.*

1. **J. Marcus Hughes** — UNCHANGED
   - Identifier: https://orcid.org/0000-0003-3410-7650
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: existing HSSI record; `CITATION.cff` lines 4-6; `pyproject.toml` `authors` (`marcus.hughes@swri.org`), also listed as sole `maintainers` entry.*
2. **Sam Van Kooten** (givenName `Sam`, familyName `Van Kooten`) — UNCHANGED relative to the current live HSSI record
   - Identifier: https://orcid.org/0000-0002-4472-8517
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: live HSSI `Person` row `5543956f-39bf-41cf-8fe6-4ab41d39ee7b` (fresh snapshot `/tmp/punchbowl_hssi_live2.json`, re-fetched 2026-07-28). **Name-variant provenance:** punchbowl's own sources give the variant **"Samuel J. Van Kooten"** — `CITATION.cff` lines 8-10 (`family-names: "Van Kooten"`, `given-names: "Samuel J."`), Zenodo/DataCite creator `Van Kooten, Samuel J.`, and `pyproject.toml` (`{ name = "Samuel J. Van Kooten" }`, `samuel.vankooten@swri.org`). Both forms are correct. HSSI's shared `Person` row now holds **"Sam Van Kooten"** following a user-approved **direct database correction on 2026-07-28 by the concurrent regularizePSF worker** (issue #57), which changed `given_name` "Sam Van" → "Sam" and `family_name` "Kooten" → "Van Kooten" — this already fixed the surname mis-split that this file originally flagged. `Person` is a **shared entity** across ndcube, punchbowl, regularizePSF and SunPy, and HSSI provides **no per-entry given-name override**: the API matches on identifier and refuses to overwrite a non-blank name, so submitting "Samuel J." would silently no-op and leave this file permanently out of sync with the database. The canonical file therefore records `Sam` / `Van Kooten` to match the shared row. ORCID and the Southwest Research Institute affiliation are unchanged.*
3. **Jasmine Kobayashi** — NEW
   - Identifier: https://orcid.org/0000-0001-9098-7790
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: `CITATION.cff` lines 12-14; `pyproject.toml` (`jasmine.kobayashi@swri.org`); ORCID employment record confirms Southwest Research Institute (ROR https://ror.org/03tghng59).*
4. **Courtney Peck** — NEW
   - Identifier: https://orcid.org/0000-0002-7586-4220
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: `CITATION.cff` lines 16-18; `pyproject.toml` (`courtney.peck@swri.org`). **Note:** her ORCID record currently lists Laboratory for Atmospheric and Space Physics (https://ror.org/01fcjzv38) and Cooperative Institute for Research in Environmental Sciences (https://ror.org/00bdqav06) as employments; the repository's own contact e-mail domain was preferred as the affiliation for this contribution. Flagged for reviewer confirmation.*
5. **Craig DeForest** — UNCHANGED
   - Identifier: https://orcid.org/0000-0002-7164-2786
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: existing HSSI record; `CITATION.cff` lines 20-22; `pyproject.toml` (`craig.deforest@swri.org`).*
6. **Chris Lowder** — UNCHANGED
   - Identifier: https://orcid.org/0000-0001-8318-8229
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: existing HSSI record; `CITATION.cff` lines 24-26; `pyproject.toml` (`chris.lowder@swri.org`).*
7. **Matthew West** — UNCHANGED
   - Identifier: https://orcid.org/0000-0002-0631-2393
   - Affiliation: European Space Research and Technology Centre — https://ror.org/03h3jqn23
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Source: existing HSSI record (both affiliations preserved); `CITATION.cff` lines 28-30 gives "West, Matthew J." — the middle initial is a stylistic difference only, so the seeded HSSI display name is kept.*
8. **Nicholas A. Murphy** — NEW to punchbowl
   - Identifier: https://orcid.org/0000-0001-6628-8033
   - Affiliation: Smithsonian Astrophysical Observatory — https://ror.org/04mh52z70
   - Affiliation: Center for Astrophysics, Harvard & Smithsonian — https://ror.org/03c3r2d17
   - Affiliation: Smithsonian Institution — https://ror.org/01pp8nd67
   - *Source: `CITATION.cff` lines 32-34, which give the short form "Murphy, Nick". The shared HSSI Person row `9bf176e1`-adjacent entry for ORCID 0000-0001-6628-8033 holds the fuller **`Nicholas A.` / `Murphy`**, and `Person` is a shared entity with no per-entry name override, so the fuller live form is recorded here (reviewer decision A, 2026-07-28). All three affiliations pre-existed on the shared row and were accumulated across other software entries; each resolves to a distinct ROR, so there is no duplication. ROR for SAO resolved via `https://api.ror.org/v2/organizations?query=Smithsonian Astrophysical Observatory`.*
9. **Raphael Attié** — REPLACED (HSSI stored the unaccented "Attie"; **corrected in the database 2026-07-28**)
   - Identifier: https://orcid.org/0000-0003-4312-6298
   - Affiliation: George Mason University — https://ror.org/02jqj7156
   - Affiliation: Goddard Space Flight Center — https://ror.org/0171mag52
   - *Source: `CITATION.cff` lines 36-38 (`family-names: "Attié"`); Zenodo/DataCite creator `Attié, Raphael`. Both existing HSSI affiliations preserved. The HSSI API cannot rename a `Person`, so this was applied by an approved, guarded direct database correction to shared Person row `40c2afb0-dfef-4be8-9ac7-12a046cb71c6`; verified live.*
10. **Samuel T. Badman** — NEW to punchbowl
    - Identifier: https://orcid.org/0000-0002-6145-436X
    - Affiliation: Center for Astrophysics, Harvard & Smithsonian — https://ror.org/03c3r2d17
    - *Source: `CITATION.cff` lines 40-42, which give the short form "Badman, Samuel". The shared HSSI Person row `9bf176e1-07ac-4e04-9cdc-ac37826c473d` holds the fuller **`Samuel T.` / `Badman`**, and `Person` is shared with no per-entry override, so the fuller live form is recorded here (reviewer decision B, 2026-07-28). Affiliation is the single pre-existing row `7706c349-0f19-4b70-b292-4a3f7859a2ba`; a duplicate-ROR affiliation briefly introduced by this refresh's PATCH was removed by an approved, guarded direct database correction on 2026-07-28.*
11. **Sarah Kovac** — REPLACED (HSSI stored the misspelling "Kovak"; **corrected in the database 2026-07-28**)
    - Identifier: https://orcid.org/0000-0003-1714-5970
    - Affiliation: NCAR High Altitude Observatory — https://ror.org/03773p874
    - *Source: `CITATION.cff` lines 44-46 (`family-names: "Kovac"`); Zenodo/DataCite creator `Kovac, Sarah`; `pyproject.toml` `{ name = "Sarah Kovac" }`. Existing HSSI affiliation preserved. The HSSI API cannot rename a `Person`, so this was applied by an approved, guarded direct database correction to shared Person row `24cb65e7-be66-4f5b-a668-09dedf5717d2`; verified live.*
12. **Joseph Plowman** — NEW
    - Identifier: https://orcid.org/0000-0001-7016-7226
    - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
    - *Source: `CITATION.cff` lines 48-50; `pyproject.toml` (`joseph.plowman@swri.org`). His ORCID record lists no employment, so the repository e-mail domain is the affiliation evidence.*
13. **Ritesh Patel** — UNCHANGED
    - Identifier: https://orcid.org/0000-0001-8504-2725
    - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
    - *Source: existing HSSI record; `CITATION.cff` lines 52-54; `pyproject.toml` (`ritesh.patel@swri.org`).*
14. **Derek Lamb** — UNCHANGED
    - Identifier: https://orcid.org/0000-0002-6061-6443
    - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
    - *Source: existing HSSI record; `CITATION.cff` lines 56-58; `pyproject.toml` (`derek.lamb@swri.org`).*
15. **Daniel Seaton** — UNCHANGED
    - Identifier: https://orcid.org/0000-0002-0494-2025
    - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
    - *Source: existing HSSI record; `CITATION.cff` lines 60-62; `pyproject.toml` (`daniel.seaton@swri.org`).*

*Platform limitation, now resolved: the HSSI API silently no-ops `Person` renames, so items 9 (Attié) and 11 (Kovac) could not be corrected by PATCH. Both were applied on 2026-07-28 by an approved, guarded direct database correction and verified live. Item 2 (Van Kooten) had already been fixed the same way earlier that day. Every name in this field now matches the shared database rows exactly.*

---

### 7. Software Name (MANDATORY)
punchbowl

*Status: UNCHANGED. Source: existing HSSI record; `CITATION.cff` `title: "punchbowl"`; `pyproject.toml` `name = "punchbowl"`; Zenodo record title `punchbowl`; PyPI project `punchbowl`.*

---

### 8. Description (MANDATORY)
punchbowl contains the science processing calibration code for use with data from the Polarimeter to UNify the Corona and Heliosphere (PUNCH) mission. It provides the primary software modules in use by the mission processing pipeline for calibrating data, also available directly to science community users. The repository also contains software tools for handling PUNCH data, along with example notebooks. Since version 0.0.23 it has also incorporated the former punchpipe package as the punchbowl.auto subpackage, which supplies the Science Operations Center automation layer: telemetry ingest and Level 0 generation, Prefect-based flow scheduling and orchestration, a processing file database, and a monitoring dashboard.

*Status: REPLACED — additive only. The submitter's three original sentences are preserved **verbatim**; one sentence was appended because the seeded description is now materially incomplete. Evidence for the addition: `CHANGELOG.rst` line 221, "Moves punchpipe into punchbowl auto subpackage. (#771)"; `docs/automation/index.rst` — "This section is about what we used to call 'punchpipe.' It's how the SOC automates file generation on their servers."; `pyproject.toml` `[project.scripts] punchpipe = "punchbowl.auto.cli:main"`; the `punchbowl/auto/` tree (control, flows, monitor); `https://api.github.com/repos/punch-mission/punchpipe` reports `"archived": true`.*

---

### 9. Concise Description (OPTIONAL)
Science calibration code and data handling tools for the PUNCH mission

*Status: UNCHANGED (66 characters). Source: existing HSSI record. Preserved as submitter editorial wording; it remains accurate.*

---

### 10. Publication Date (RECOMMENDED)
2024-11-01

*Status: UNCHANGED. Source: existing HSSI record; corroborated by the earliest PyPI upload for the project, `punchbowl-0.0.0` at `2024-11-01T14:45:44.134455Z` (`https://pypi.org/pypi/punchbowl/json`), which coincides with the first Zenodo deposit under concept DOI 10.5281/zenodo.14029123.*

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Status: UNCHANGED. Source: existing HSSI record; DataCite `attributes.publisher = "Zenodo"` for 10.5281/zenodo.14029123.*

---

### 12. Version (RECOMMENDED)
- **Version Number:** 0.0.24
- **Version Date:** 2026-07-28
- **Version PID:** https://doi.org/10.5281/zenodo.21640289
- **Version Description:** Reworks Level 2 mosaic assembly so polarized inputs are co-aligned before conversion to the MZP-solar system; substantially speeds up Level 1 alignment and runs reprojection and starfield generation at 32 bits to cut memory use; caps whole-pipeline memory and the number of concurrent flows; adds per-server configuration, host-scoped control flows and a "run-on" deployment option; writes spacecraft position and velocity into FITS headers in additional Earth-centric frames via the new GCRS-aware `PUNCHCube.celestial_wcs`; introduces the `PUNCHCube` NDCube subclass carrying a secondary celestial WCS; sets up QuickPUNCH for new clear-derived product types; allows interpolation between starfield models; removes the unused quadprog F-corona approach; plus numerous polarization, metadata, scheduling and Fido-client fixes.

*Status: REPLACED. HSSI currently holds `punchbowl - 0.0.19`. **Verified 0.0.24 is the current latest release** (issue #57's note about 0.0.23 is stale):*
- *`git for-each-ref refs/tags` → tag `0.0.24` dated 2026-07-28 (next-newest `0.0.23` dated 2026-04-01); `0.0.24` is reachable from the extracted revision `527b32ad`.*
- *PyPI: `https://pypi.org/pypi/punchbowl/json` reports `info.version = "0.0.24"`, `punchbowl-0.0.24.tar.gz` uploaded `2026-07-28T08:37:33.933467Z` (24 releases total).*
- *Zenodo: record `21640289` — `"version": "0.0.24"`, `"publication_date": "2026-07-28"`, `"doi": "10.5281/zenodo.21640289"`, `"conceptdoi": "10.5281/zenodo.14029123"`; DataCite relatedIdentifier `IsSupplementTo https://github.com/punch-mission/punchbowl/tree/0.0.24`.*
- *`CITATION.cff`: `version: 0.0.24`, `date-released: 2026-07-28`.*
- *Version Description summarised from `CHANGELOG.rst`, section "0.0.24 (2026-07-28)".*

---

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Status: UNCHANGED. Source: existing HSSI record; `pyproject.toml` `requires-python = ">=3.11,<3.15"`; `.github/workflows/ci.yaml` test matrix `["3.11", "3.12", "3.13", "3.14"]`. **Note:** SoMEF also reports "Shell" for the repository (a handful of helper scripts such as `scripts/L3_PAM_CAM_filecounts.sh`); not added, because the form asks only for "the most important languages" and Shell is incidental here.*

---

### 14. Reference Publication (RECOMMENDED)
Not found

*Status: N/A. `CITATION.cff` contains no `preferred-citation`; the maintainers' stated citation is the software DOI itself ("If you use this software, please cite it as below.", `CITATION.cff` line 2). Closest candidate, recorded under Related Publications instead: Hughes et al. (2023), "Interoperability of PUNCH software in the Python ecosystem", https://doi.org/10.5281/zenodo.8412310, whose abstract explicitly describes punchbowl as "the core PUNCH pipeline package". Flagged for reviewer decision.*

---

### 15. License (RECOMMENDED)
- **License:** GNU Lesser General Public License v3.0 only
- **License URI:** https://spdx.org/licenses/LGPL-3.0-only.html

*Status: License UNCHANGED; License URI NEW (absent from the HSSI record). Source: existing HSSI record; `LICENSE` — "Copyright (c) 2024 PUNCH Science Operations Center … may be used, modified, and distributed under the terms of the GNU Lesser General Public License v3 (LGPL-v3)"; `pyproject.toml` `license = { file = "LICENSE" }`. SPDX short identifier `LGPL-3.0-only`. **Note:** the Zenodo deposit records `cc-by-4.0` (a Zenodo default); the repository `LICENSE` file is authoritative and the existing HSSI value is correct.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
*Status: 8 existing keywords preserved (UNCHANGED) + 13 NEW. Terms marked (in HSSI vocabulary) already exist in `http://localhost/api/models/Keyword/rows/all/`; the two marked (new term) would create new vocabulary rows — the field explicitly allows custom entries.*

Existing (preserved):
- Calibration — *existing HSSI record; `pyproject.toml` `keywords`.*
- Image — *existing HSSI record; GitHub repo topic `image` (SoMEF `keywords`).*
- Nasa — *existing HSSI record; `pyproject.toml` `keywords`; GitHub topic `nasa`.*
- Nasa Data — *existing HSSI record; GitHub topic `nasa-data`.*
- Punch — *existing HSSI record; `pyproject.toml` `keywords`; GitHub topic `punch`.*
- Science — *existing HSSI record; `pyproject.toml` `keywords`.*
- Solar Physics — *existing HSSI record; `pyproject.toml` `keywords`; GitHub topic `solar-physics`.*
- Solar Wind — *existing HSSI record; GitHub topic `solar-wind`.*

New:
- astrometry (in HSSI vocabulary) — *`punchbowl/level1/alignment.py` uses the `astrometry` (astrometry.net) solver and a Gaia catalog to solve image pointing (`astrometry_net_initial_solve`, `solve_pointing`, `download_gaia_data`).*
- ccsds (in HSSI vocabulary) — *`punchbowl/auto/flows/level0.py` decommutates CCSDS packets with `ccsdspy`.*
- corona (in HSSI vocabulary) — *`docs/intro.rst`; L3 products are coronal brightness images.*
- coronagraph (in HSSI vocabulary) — *NFI is PUNCH's coronagraph; `docs/data/access.rst`, `punchbowl/level1/vignette.py` `generate_vignetting_calibration_nfi`.*
- heliosphere (in HSSI vocabulary) — *"Polarimeter to UNify the Corona and Heliosphere"; WFI field of view spans ~180 solar radii (`docs/data/access.rst`).*
- image processing (in HSSI vocabulary) — *`punchbowl/level1/despike.py`, `destreak.py`, `deficient_pixel.py`, `level2/resample.py`.*
- photometry (new term) — *`punchbowl/level1/quartic_fit.py` `photometric_calibration`; products are "floating-point values in mean-solar-brightness units" (`docs/data/data_overview.rst`, Level 1).*
- point spread function (in HSSI vocabulary) — *`punchbowl/level1/psf.py` with `regularizepsf.ArrayPSFTransform`.*
- polarimetry (new term) — *PUNCH is a polarimeter; `punchbowl/level2/polarization.py`, `level3/polarization.py`, and the B/pB/pB′ and M,Z,P systems in `docs/data/data_overview.rst`.*
- solar imaging (in HSSI vocabulary) — *`docs/data/data_overview.rst`: "PUNCH is an imaging mission and most data from the mission are images."*
- space weather (in HSSI vocabulary) — *`docs/data/data_overview.rst`, Level Q: "intended to be useful for space weather forecasting … produced for NOAA's space weather forecasting infrastructure".*
- telemetry (in HSSI vocabulary) — *`punchbowl/auto/flows/level0.py` ingests spacecraft TLM files (`TLMFiles`, `PacketHistory`).*
- thomson scattering (in HSSI vocabulary) — *`examples/PUNCH-InSitu-Connection.py`: "assuming the pixel intensity can be associated with the Thomson sphere"; PUNCH images Thomson-scattered light.*

*Considered and rejected:* `python` and `fits` — the field is for "science keywords … not supported by other metadata fields", and these duplicate Field 13 and Fields 18/19.

---

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific — *Status: UNCHANGED. Source: existing HSSI record; `punchbowl/data/fido/client.py` `PUNCHClient` is a PUNCH-specific client reading the SDAC PUNCH tree; `punchbowl/auto/flows/level0.py` ingests PUNCH spacecraft telemetry directly. Cross-listed with Fields 31/32 as instructed.*
- The Virtual Solar Observatory — *Status: UNCHANGED. Source: existing HSSI record; `docs/data/access.rst` — "stored and accessible through the Solar Data Analysis Center (SDAC) - a portal for hosting through tools such as the Virtual Solar Observatory (VSO). From here PUNCH data products can be queried and requested for download"; `examples/querying_data.py` — "how to query PUNCH data from the SDAC / VSO using Python tools".*
- HTTP/HTTPS Directories — *Status: NEW. Source: `punchbowl/data/fido/client.py:22-23` — `fits_rootdir = "https://umbra.nascom.nasa.gov/punch"`, `jp2_rootdir = "https://umbra.nascom.nasa.gov/punch/L"`, scraped with `sunpy.net.scraper.Scraper` over a dated directory `pattern`; `docs/data/access.rst` documents the equivalent `wget -r -l1 --no-parent … https://umbra.nascom.nasa.gov/punch/3/CAM/2025/09/21/`; `punchbowl/data/sample.py:19` downloads sample files from `https://data.boulder.swri.edu/lowder/PUNCH/sample/`.*

*Considered and rejected:* `S3/Cloud-aware` — `punchbowl/auto/flows/levelq.py:602-609` uploads QuickPUNCH products **to** a NOAA S3 bucket, but this field is defined as "the data **input** source the software supports" and punchbowl never reads from S3. Flagged for reviewer awareness.

---

### 18. Input File Formats (RECOMMENDED)
- FITS — *Status: UNCHANGED. Source: existing HSSI record; `punchbowl/data/punch_io.py:395` `load_ndcube_from_fits`, `load_many_cubes`; `docs/data/access.rst`, "Reading Data".*
- csv — *Status: NEW. Source: `punchbowl/data/meta.py:42` `pd.read_csv(path, na_filter=False)` loads the omniheader/level metadata templates; `punchbowl/level1/alignment.py:153,168` `load_gaia_catalog(... "gaia_catalog.csv")`; `punchbowl/auto/cli.py:273` and `punchbowl/auto/flows/level0.py:1290` `pd.read_csv`; `scripts/auto/prepare_packet_definition_csv_files.py`.*
- JSON — *Status: NEW. Source: `json.load` used in 8 places, including pipeline/quicklook configuration and cached state (`punchbowl/auto/control/util.py`, `punchbowl/auto/flows/level0.py`).*
- Other — *Status: NEW. Covers: raw CCSDS telemetry (TLM) packet files (`punchbowl/auto/flows/level0.py`, `ccsdspy.utils.split_by_apid`); JPEG2000-compressed image packets decoded with `pylibjpeg.decode` (line 624); Excel packet-definition workbooks (`pd.read_excel`, line 198); NumPy `.npy` square-root decode tables (`punchbowl/level1/sqrt.py:71-105`); YAML pipeline configuration (`punchbowl/auto/control/util.py` `load_pipeline_configuration`).*

*Considered and rejected:* `HDF5` — `h5py>=3.15` is declared in the `super_user` extra but is never imported anywhere in `punchbowl/`. `CDF`, `netCDF3/4`, `IDL.sav`, `Zarr`, `ISTP-Compliant`, `ascii` — no supporting code.

---

### 19. Output File Formats (RECOMMENDED)
- FITS — *Status: UNCHANGED. Source: existing HSSI record; `punchbowl/data/punch_io.py:285` `write_ndcube_to_fits` (RICE-compressed, with uncertainty HDU and provenance BinTable — `_make_provenance_hdu`, `_pack_uncertainty`); `docs/data/access.rst`.*
- csv — *Status: NEW. Source: `punchbowl/auto/cli.py:350` `result_df.to_csv(output_file_soc, index=False)`; `punchbowl/auto/flows/level0.py:1296` `new_table.to_csv(df_path, index=False)`; `punchbowl/level1/alignment.py:57` writes the Gaia catalog with `.to_csv(out_path)`.*
- JSON — *Status: NEW. Source: `json.dump` used in 33 places (flow state, cache and dashboard artefacts across `punchbowl/auto/`).*
- Other — *Status: NEW. Covers: JPEG2000 quicklooks (`punchbowl/data/punch_io.py:105` `write_ndcube_to_quicklook` via `glymur.Jp2k`, with an XML metadata box from `_generate_jp2_xmlbox`); MP4 animations (`write_quicklook_to_mp4`, line 242; `punchbowl/data/visualize.py:135` `animate_punch`); NumPy `.npz`/`.npy` (`punchbowl/limits.py:164` `np.savez`, `punchbowl/level1/sqrt.py:95,105` `np.save`); `.sha` checksum sidecars (`punchbowl/data/punch_io.py:40` `write_file_hash`).*

---

### 20. Operating System (RECOMMENDED)
- Linux — *Status: UNCHANGED. Source: existing HSSI record; `.github/workflows/ci.yaml` runs the full test matrix on `runs-on: ubuntu-latest`; the PUNCH SOC servers referenced throughout `punchbowl/auto/` are Linux hosts.*
- Mac — *Status: UNCHANGED. Source: existing HSSI record; `README.md` lines 30, 36 give macOS activation instructions (`source .venv/bin/activate` on Mac/Linux); HSSI CPU architecture already records Apple Silicon arm64.*

*Considered and rejected:* `Windows` — `README.md` lines 30 and 36 do mention `.venv\Scripts\activate` on Windows, but that is boilerplate venv text; CI never exercises Windows, and the `super_user` extra pulls in `astrometry` (astrometry.net bindings, used by `punchbowl/level1/alignment.py:320`) and `sep`, which do not build on Windows. Recorded here as a candidate rather than a value so a reviewer can decide.

---

### 21. CPU Architecture (RECOMMENDED)
- x86-64 — *Status: UNCHANGED. Source: existing HSSI record; CI runs on `ubuntu-latest` (x86-64 runners).*
- Apple Silicon arm64 — *Status: UNCHANGED. Source: existing HSSI record; pure-Python/wheel-based install documented for Mac in `README.md`.*
- GPU — *Status: UNCHANGED, and independently confirmed. Source: `punchbowl/level3/motion_filter.py:7-10,96-110` optionally imports `cupy` and runs the hourglass motion filter on GPU (`use_gpu` parameter, "Whether to use GPU for processing (default is True)"), falling back to CPU when cupy is unavailable; `punchbowl/data/punch_io.py:263` mentions a codec "For GPU acceleration".*

*Considered and rejected:* `HPC or HEC` — the pipeline scales across SOC servers with a Dask `LocalCluster` and numba threading, but there is no HPC-centre scheduler integration (no MPI, no Slurm/PBS job scripts).

---

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections — *Status: UNCHANGED. Source: existing HSSI record; `docs/data/access.rst` — PAM files make it "the product of choice for studies of CMEs, shocks, the solar wind, etc."*
- Solar Corona — *Status: UNCHANGED. Source: existing HSSI record; `docs/intro.rst`; L3 products are "intended to be usable directly as coronal and solar-wind images" (`docs/data/data_overview.rst`).*
- Solar Wind — *Status: UNCHANGED. Source: existing HSSI record; `punchbowl/level3/velocity.py` `track_velocity` produces the L3 VAM "derived solar-wind motion" product.*

*Considered and rejected:* an "F-corona" / zodiacal-light term would be well evidenced (`punchbowl/level3/f_corona_model.py`, `docs/pipeline/level3/f_corona.rst`), but the HSSI Phenomena vocabulary currently holds only 7 rows (`http://localhost/api/models/Phenomena/rows/all/`: Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission) and adding it would create a new controlled-vocabulary row. Flagged for reviewer decision rather than added unilaterally.

---

### 23. Development Status (RECOMMENDED)
Active

*Status: NEW (the HSSI record has no development status). Source: 24 tagged releases with the newest, `0.0.24`, cut on the extraction date 2026-07-28; commit `527b32ad` dated 2026-07-28; `CHANGELOG.rst` 0.0.24 alone references PRs up to #1075; the code is in operational use generating the PUNCH mission's public data products. Per repostatus.org, "Active: reached stable, usable state and being actively developed". **Note:** `README.md` lines 9-11 caution that "This package is still being heavily edited as calibration algorithms are improved. Stability is not promised until v1", and `pyproject.toml` classifies it `Development Status :: 4 - Beta`; "WIP" was rejected because that term requires "no stable, usable public release yet", which is contradicted by 24 PyPI releases in production use.*

---

### 24. Documentation (RECOMMENDED)
https://punchbowl.readthedocs.io/en/latest/

*Status: UNCHANGED. Source: existing HSSI record; `README.md:7`; `pyproject.toml` `[project.urls] Documentation`; `.readthedocs.yaml`. URL verified live (HTTP 200 on 2026-07-28).*

---

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

*Status: UNCHANGED. Source: existing HSSI record (already fully expanded, no acronym). Corroborated by `docs/intro.rst` — "PUNCH is a NASA Small Explorer (SMEX) mission". The repository contains no funding-acknowledgement file and the Zenodo/DataCite records carry an empty `fundingReferences` list, so no additional funder could be evidenced.*

---

### 26. Award Title (OPTIONAL)
- **Award Title:** Polarimeter to UNify the Corona and Heliosphere (PUNCH)
- **Award Number:** 80GSFC18C0014

*Status: **Both values are ALREADY PRESENT IN HSSI — neither is a proposed change, and neither belongs in the removals/replacements table.** Award Title UNCHANGED (source: existing HSSI record; mission name confirmed in `docs/intro.rst` and `punchbowl/data/fido/client.py` — `a.Source: [("PUNCH", "Polarimeter to UNify the Corona and Heliosphere")]`).*

*Award Number `80GSFC18C0014` is **recorded, not introduced**. It was previously written as "Not found" because the software view API does not render it — the same situation as the Field 15 License URI, where the value exists in the database but `GET /api/view/software/<uid>/` omits it. Verified on 2026-07-28 against `http://localhost/api/models/Award/rows/all/`: row `03ab3ee8-fbc6-4a4e-a2da-da87a6c2d5ab` has `name: "Polarimeter to UNify the Corona and Heliosphere (PUNCH)"` and `identifier: "80GSFC18C0014"`. It is the **only** one of the 38 Award rows carrying either that name or that identifier, and punchbowl's live record shows exactly that award title (`"award": ["Polarimeter to UNify the Corona and Heliosphere (PUNCH)"]`), so punchbowl is already linked to it.*

***External corroboration — partial, and honestly qualified.** The number could not be tied to the PUNCH award by any punchbowl-side source: the repository contains no funding-acknowledgement file, and DataCite reports an empty `fundingReferences` list for the punchbowl DOIs. A targeted web search did, however, establish that `80GSFC18C0014` is a **real NASA contract number**: NASA NTRS record `20220017302` ("The Coronal Veil", Malanushenko, Cheung, **DeForest**, Klimchuk & Rempel) lists `CONTRACT_GRANT: 80GSFC18C0014`, and C. E. DeForest is both a punchbowl author and the PUNCH principal investigator at Southwest Research Institute. That corroborates the number's existence and its association with DeForest/SwRI solar work, but **not** that it is specifically the PUNCH SMEX award; a second search against SwRI/PUNCH mission pages returned no acknowledgement text containing it. The value is therefore recorded as a **pre-existing HSSI value we are surfacing, not introducing or endorsing**.*

*Do not patch this field: the backend discards a submitted award `name` when the submitted `identifier` matches an existing row, so the award title is fixed regardless of what is sent, and both values already match the database.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
*Status: all NEW (the HSSI record has no related publications). Only DOIs actually cited by the project are listed.*

- https://doi.org/10.5281/zenodo.8412310 — Hughes, J. M., DeForest, C., Kovac, S., Lowder, C., Patel, R., Seaton, D., & West, M. J. (2023). *Interoperability of PUNCH software in the Python ecosystem*. Zenodo. — *Evidence: the DataCite abstract names this software directly: "regularizePSF corrects variable point spread functions, and solpolpy resolves solar polarization to a standard frame. These packages are used in the core PUNCH pipeline package - punchbowl." Authored by the punchbowl author team. Also a candidate Reference Publication (Field 14).*
- https://doi.org/10.3847/1538-4357/ac43b6 — DeForest, C. E., Seaton, D. B., & West, M. J. (2022). *Three-polarizer Treatment of Linear Polarization in Coronagraphs and Heliospheric Imagers*. The Astrophysical Journal. — *Evidence: cited in `docs/data/data_overview.rst:18` as the definition of the B/pB/pB′ and M,Z,P polarization systems that `punchbowl/level2/polarization.py` and `punchbowl/level3/polarization.py` implement.*
- https://doi.org/10.1023/B:SOLA.0000021743.24248.b0 — DeForest, C. E. (2004). *On Re-sampling of Solar Images*. Solar Physics. — *Evidence: cited in `docs/pipeline/level2/image_resample.rst:11` as the algorithm behind the adaptive reprojection used by `punchbowl/level2/resample.py` `reproject_cube`.*

---

### 28. Related Datasets (OPTIONAL)
*Status: the **complete set of 43** Solar Data Analysis Center PUNCH dataset DOIs is now listed — the 4 seeded HSSI DOIs (UNCHANGED) plus 39 additions (NEW), per the reviewer's explicit decision to maximise comprehensiveness. Enumerated on 2026-07-28 by paging the DataCite API (`https://api.datacite.org/dois?prefix=10.48322&query=titles.title:PUNCH&page[size]=100`), which reported `meta.total = 43`; 43 unique DOIs were collected. **No DOI suffix was pattern-generated** — every one comes from the API response. Each was independently verified twice: `GET https://api.datacite.org/dois/<doi>` returned HTTP 200 with a title matching verbatim (43/43), and `https://doi.org/<doi>` resolved HTTP 200 (43/43), redirecting to the corresponding `https://spase-metadata.org/NASA/NumericalData/PUNCH/...` record. Titles below are reproduced **verbatim from DataCite**, including the registry's own typos ("puls 60", the double space in "Level 3  Low-noise").*

**Collection DOIs — seeded, UNCHANGED (4)**
- https://doi.org/10.48322/5k49-bh56 — PUNCH NFI-WFI Level 0 Science images — *existing HSSI record; DataCite publisher "Solar Data Analysis Center", 2025.*
- https://doi.org/10.48322/enbf-rh75 — PUNCH NFI-WFI Level 1 Science images — *existing HSSI record; DataCite verified.*
- https://doi.org/10.48322/stqs-j385 — PUNCH NFI-WFI Level 2 Science Dataset — *existing HSSI record; DataCite verified.*
- https://doi.org/10.48322/nnv7-bn21 — PUNCH NFI-WFI Level 3 Science Dataset — *existing HSSI record; DataCite verified.*

**Level 2 science products — NEW (2)**
- https://doi.org/10.48322/z829-zy89 — PUNCH Level2 Polarized Mosaics (Trefoil) Data — *product code PTM, produced by `punchbowl/level2/flow.py` `level2_core_flow` (`docs/data/data_overview.rst`, Level 2).*
- https://doi.org/10.48322/sv88-z093 — PUNCH Level2 Clear Mosaics (Trefoil) Data — *product code CTM, same flow.*

**Level 3 science products — NEW (6)**
- https://doi.org/10.48322/f6tk-sm20 — PUNCH Level 3 Polarized Mosaic Data in the MZP system — *product code PTM/L3, `punchbowl/level3/flow.py` `level3_core_flow`.*
- https://doi.org/10.48322/kxpb-q477 — PUNCH Level 3 Clear Mosaic Data — *product code CTM/L3, same flow.*
- https://doi.org/10.48322/5gmz-ka58 — PUNCH Level 3  Low-noise Polarized Mosaic Data in the MZP system — *product code PAM, `punchbowl/level3/low_noise.py` `create_low_noise_task`; `docs/data/access.rst` calls PAM a recommended starting product.*
- https://doi.org/10.48322/bbrw-k528 — PUNCH Level 3 Clear Low-Noise Mosaic Data — *product code CAM, same module; the other recommended starting product.*
- https://doi.org/10.48322/dcpx-4r68 — PUNCH Level 3 Polarized Mosaic F-corona Model in the MZP system — *generated by `punchbowl/level3/f_corona_model.py` `construct_f_corona_model`.*
- https://doi.org/10.48322/dy2y-je98 — PUNCH Level 3 Clear Mosaic F-corona Model — *same module.*

**Level 0 per-spacecraft, per-polarization-state products — NEW (15)**
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

**Level 1 per-spacecraft, per-polarization-state products — NEW (16)**
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

*Note on completeness (supersedes the earlier "deliberately omitted" note):* the per-spacecraft, per-polarization Level 0 and Level 1 children are listed here **alongside** their `PUNCH NFI-WFI Level 0/1 Science images` collection DOIs by explicit reviewer decision — the collections are retained because they are the seeded HSSI values and must not be dropped, and the children are added because punchbowl produces and reads each one individually. The counts are asymmetric because that is what SDAC has registered: Level 0 has 15 children (NFI has only clear, minus-60 and zero states registered — there is no Level 0 NFI plus-60 DOI in DataCite) while Level 1 has 16. 4 + 2 + 6 + 15 + 16 = **43**, matching DataCite's reported total exactly.

---

### 29. Related Software (OPTIONAL)
*Status: 1 existing value preserved (UNCHANGED) + 5 NEW. Relevance gate applied before any DOI lookup.*

- https://doi.org/10.5281/zenodo.17873783 — **punchpipe** — *Status: UNCHANGED (preserved). **Gate: PASSES.** This DOI resolves (via `https://api.datacite.org/dois/10.5281/zenodo.17873783`) to the Zenodo concept record for `punch-mission/punchpipe`, "Pipeline automation for PUNCH mission" (latest version 0.0.14). It is punchbowl's direct predecessor/companion, not generic infrastructure: `CHANGELOG.rst:221` records "Moves punchpipe into punchbowl auto subpackage. (#771)", `pyproject.toml` still ships the console script `punchpipe = "punchbowl.auto.cli:main"`, `docs/automation/index.rst` says "This section is about what we used to call 'punchpipe'", and `https://api.github.com/repos/punch-mission/punchpipe` reports `"archived": true` (last push 2026-02-13). Field 29 explicitly covers predecessors and companions, so it is retained unchanged.*
- https://doi.org/10.5281/zenodo.10076326 — **solpolpy** — *Status: NEW. Gate: PASSES (domain-specific companion, PUNCH-team solar polarization resolver). Evidence: `punchbowl/level2/polarization.py:3,37`, `punchbowl/level3/polarization.py:6`, `punchbowl/level3/stellar.py:21-22`; `README.md` line 68 instructs contributors to set up pre-commit "in the punchbowl, solpolpy, and/or regularizepsf repositories". Concept DOI from `punch-mission/solpolpy` `CITATION.cff`.*
- https://doi.org/10.5281/zenodo.7392170 — **regularizepsf** — *Status: NEW. Gate: PASSES (domain-specific companion, PUNCH-team variable-PSF package, PyHC community package). Evidence: `punchbowl/level1/psf.py`, `punchbowl/level1/alignment.py:18`, `punchbowl/auto/control/cache_layer/psf.py:3` (`from regularizepsf import ArrayPSFTransform`); `README.md` line 68. Concept DOI from `punch-mission/regularizepsf` `CITATION.cff`.*
- https://github.com/punch-mission/simpunch — **simpunch** — *Status: NEW. Gate: PASSES (companion PUNCH data simulator by the same team). Evidence: `punchbowl/auto/flows/simulate.py:11` `from simpunch.flow import generate_flow`; `pyproject.toml` `[dependency-groups] pipe` and `[tool.uv.sources] simpunch = { path = "../simpunch", editable = true }`; `scripts/auto/generate_batch_of_simpunch.py`. No DOI published, so the repository URL is used as the form permits.*
- https://github.com/svank/remove_starfield — **remove_starfield** — *Status: NEW. Gate: PASSES (domain-specific dependency written by punchbowl co-author Samuel Van Kooten, specifically for heliospheric-imager starfield removal). Evidence: `punchbowl/level3/stellar.py:8,15-16,295,317`. No DOI published; repository URL used.*
- https://github.com/ccsdspy/ccsdspy — **CCSDSPy** — *Status: NEW. Gate: PASSES as a **domain-specific dependency** (spacecraft CCSDS packet reader; a PyHC community package per `_data/projects.yml`) whose presence characterises punchbowl as a mission telemetry-ingest pipeline. Evidence: `punchbowl/auto/flows/level0.py:16,24-25,229,274`. Concept DOI 10.5281/zenodo.7819990 also exists; the repository URL is given as the primary link. Deliberately **not** listed under Field 30 — punchbowl passes it packet definitions and receives arrays, which is ordinary library use rather than a peer-tool exchange.*

---

### 30. Interoperable Software (OPTIONAL)
*Status: 1 existing value preserved (UNCHANGED) + 6 NEW. Every entry names the specific adapter, subclass, or documented exchange that satisfies the gate.*

- https://doi.org/10.5281/zenodo.17873783 — **punchpipe** — *Status: UNCHANGED (preserved). **Gate: PASSES.** Identified above as `punch-mission/punchpipe`. Demonstrated exchange: punchpipe was built to import and drive punchbowl's core flows as the SOC orchestration layer, and that code now lives inside punchbowl as `punchbowl/auto/` while retaining the `punchpipe` entry point (`pyproject.toml [project.scripts]`). It is a heliophysics mission-pipeline peer tool, not generic infrastructure, so there is no authoritative evidence that it fails the gate and it is preserved. **Reviewer note:** because punchpipe is now archived and merged in, "interoperability" is arguably historical; retained per the preserve-by-default rule, flagged so a curator can decide.*
- https://doi.org/10.5281/zenodo.10076326 — **solpolpy** — *Status: NEW. Gate: PASSES — shared data-model exchange. `punchbowl/data/punch_io.py:563` `remix_collection` builds an `ndcube.NDCollection` "primarily used for solpolpy", which `punchbowl/level2/polarization.py:37` hands to `solpolpy.resolve(data_collection, outsys)` and reads back as resolved cubes; `punchbowl/level3/stellar.py:22` additionally consumes `solpolpy.util.solnorth_from_wcs`. Version provenance is even recorded in the output metadata (`punchbowl/auto/control/processor.py:118-119`, `result.meta['SPPYVRSN'] = solpolpy.__version__`).*
- https://doi.org/10.5281/zenodo.7392170 — **regularizepsf** — *Status: NEW. Gate: PASSES — object exchange through a documented API. `punchbowl/level1/psf.py` `build_psf_transform` constructs `regularizepsf` PSF models from PUNCH images and `correct_psf` applies `ArrayPSFTransform` objects loaded by `punchbowl/auto/control/cache_layer/psf.py`; output provenance records `result.meta['RPSFVRSN']`-style version stamping in `punchbowl/auto/control/processor.py:122`.*
- https://github.com/svank/remove_starfield — **remove_starfield** — *Status: NEW. Gate: PASSES — plugin/extension relationship. `punchbowl/level3/stellar.py:132` defines `class PUNCHImageProcessor(ImageProcessor)`, implementing remove_starfield's extension interface, plus `class LoggingProgressIndicator` (line 220) "implementing remove_starfield's interface for progress indications"; punchbowl then calls `remove_starfield.build_starfield_estimate(...)` (lines 295, 317) with `BlockMasker`/`GaussianReducer` and subtracts the returned `Starfield`. Version stamped at `punchbowl/auto/control/processor.py:126-127`.*
- https://github.com/punch-mission/simpunch — **simpunch** — *Status: NEW. Gate: PASSES — bidirectional companion exchange. `punchbowl/auto/flows/simulate.py:11,129` calls `simpunch.flow.generate_flow` from inside a punchbowl Prefect flow; simpunch emits synthetic PUNCH FITS products that are then fed straight back through punchbowl's own L0→L3 flows (`scripts/auto/clear_files_for_pending_simpunch_flows.py`, `generate_batch_of_simpunch.py`).*
- https://github.com/sunpy/sunpy — **SunPy** — *Status: NEW. Gate: PASSES (Tier-B-style, with cited evidence) — plugin/extension relationship with a named domain tool. `punchbowl/data/fido/client.py:19` registers `class PUNCHClient(GenericClient)` with sunpy's Fido, and `punchbowl/data/fido/attrs.py` registers a `punch` attrs module (`_attrs_module` returns `("punch", "punchbowl.data.fido.attrs")`), so `Fido.search(a.Time(...), a.punch.ProductCode.ca, a.Level.three, ...)` works after `import punchbowl` — demonstrated in `examples/querying_data.py` ("Note that this import is needed to register PUNCH fido tools"). PUNCH products additionally load directly as `sunpy.map.Map` (`examples/PUNCH-InSitu-Connection.py`), and `docs/intro.rst` states the pipeline and query tools are built on "the SunPy and Astropy software libraries".*
- https://github.com/sunpy/ndcube — **ndcube** — *Status: NEW. Gate: PASSES (Tier-B-style, with cited evidence) — shared data model as the documented interchange format. `punchbowl/data/punchcube.py:13` defines `class PUNCHCube(NDCube)`; the public loader `punchbowl/data/punch_io.py:395` `load_ndcube_from_fits` returns it and `write_ndcube_to_fits` consumes it; `punchbowl/data/punch_io.py:27` uses `ndcube.NDCollection` as the interchange container; and `docs/data/access.rst`, "Reading Data", documents to users that "These data can also be bundled together as an NDCube object … using some of the bundled IO tools within punchbowl", with a `load_ndcube_from_fits` example.*

- https://doi.org/10.5281/zenodo.4670728 — **Astropy** — *Status: NEW. Gate: PASSES (Tier B, with cited evidence) — punchbowl extends astropy's own APIs rather than merely consuming them, meeting the same bar already accepted for `ndcube` and `SunPy`. `punchbowl/data/wcs.py:460` defines `class GCRSWCS(WCS)`, subclassing `astropy.wcs.WCS` so that a PUNCH WCS "accepts and returns GCRS SkyCoords" — the same subclassing justification used for `PUNCHCube(NDCube)`, and this object is exposed to users as `PUNCHCube.celestial_wcs` (CHANGELOG 0.0.24, PR #964). `punchbowl/data/wcs.py:36` calls `custom_stokes_symbol_mapping({10: StokesSymbol("pB", "polarized brightness"), 11: StokesSymbol("B", "total brightness")})` (imported from `astropy.coordinates`, lines 15-25) to register PUNCH's `pB`/`B` symbols into astropy's own polarization-frame API — a documented astropy extension point, not passive dependency use. `docs/intro.rst:38` states "The pipeline and tools for querying / loading PUNCH data use the Python language, along with the SunPy and Astropy software libraries." Identifier is the **Concept DOI** declared authoritatively in astropy's own `CITATION.cff` (`identifiers: - type: doi, description: Concept DOI, value: "10.5281/zenodo.4670728"`), chosen the same way as solpolpy and regularizepsf; verified to resolve HTTP 200 (redirects to `https://zenodo.org/records/21262391`; `https://api.datacite.org/dois/10.5281/zenodo.4670728` returns HTTP 200, title "Astropy", publisher Zenodo). Added to Field 30 only — **not** to Field 29 — per the reviewer's decision.*

*Considered and rejected — Tier A generic infrastructure (would be equally at home in a web app, finance model, or biology pipeline):* numpy, scipy, pandas, matplotlib, plotly, dash / dash-bootstrap-components, requests, python-dateutil, PyYAML, click, tqdm, setuptools, pytest (+ plugins), ruff/pre-commit/codespell, sqlalchemy / pymysql, fastapi, gunicorn, psutil, networkx, numexpr, threadpoolctl, coolname, freezegun, hypothesis, xlrd, lxml, toml, numpy-quaternion.
*Considered and rejected — domain-adjacent but no demonstrated peer exchange:* `reproject`, `photutils`, `sep`, `astrometry`, `lmfit`, `scikit-image`, `scikit-learn`, `numba`, `cupy`, `glymur`, `pylibjpeg`, `prefect` / `prefect-dask` / `prefect-sqlalchemy`, `dask`, `jupyter`.
*Considered and rejected — declared but unused:* `sunkit-image` and `h5py` appear in `pyproject.toml` but are never imported anywhere under `punchbowl/`.

---

### 31. Related Instruments (OPTIONAL)
*Status: all NEW (the HSSI record has no related instruments). Resolved against the HSSI controlled vocabulary at `http://localhost/api/models/InstrumentObservatory/rows/all/` (7,648 rows), filtered locally to `type: 1`. Every identifier below was additionally verified to resolve (HTTP 200) at spase-metadata.org. No bare names are emitted.*

- **Narrow Field Imager**
  - Instrument Identifier: https://spase-metadata.org/NASA/Instrument/PUNCH/NFI
  - *Ladder step 1 (exactly one row after `.html` normalisation). The vocabulary contains both `.../PUNCH/NFI` (name "Narrow Field Imager", abbreviation "NFI") and its `.html` twin `.../PUNCH/NFI.html` (name "Narrow Field Imager (NFI)"); per the normalisation rule these are one resource and the bare identifier/name is used. Repository evidence: `punchbowl/cli.py` `create_calibration` — "For WFIs, use 1, 2, or 3. For NFI, use 4"; `punchbowl/level1/vignette.py:242` `generate_vignetting_calibration_nfi`; `punchbowl/data/fido/client.py` registers `a.Instrument: ("NFI-4", "Narrow Field Imager")`; `punchbowl/auto/control/cache_layer/nfi_l1.py`; `docs/data/data_overview.rst` ("NFI is assigned the number 4").*
- **Wide Field Imager** (PUNCH spacecraft 1)
  - Instrument Identifier: https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/1
- **Wide Field Imager** (PUNCH spacecraft 2)
  - Instrument Identifier: https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/2
- **Wide Field Imager** (PUNCH spacecraft 3)
  - Instrument Identifier: https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/3
  - *The three WFI rows share the identical vocabulary name "Wide Field Imager" (abbreviation "WFI") and are distinguished only by their SPASE identifiers. This is **ladder step 2**, not an ambiguity: the repository supplies concrete evidence selecting all three. `docs/data/data_overview.rst` — "WFI1, WFI2, and WFI3 are assigned the numbers 1-3"; `punchbowl/cli.py` — "For WFIs, use 1, 2, or 3"; `punchbowl/data/fido/client.py` registers `("WFI-1", "Wide Field Imager 1")`, `("WFI-2", "Wide Field Imager 2")`, `("WFI-3", "Wide Field Imager 3")`; `punchbowl/level1/vignette.py:157` `generate_vignetting_calibration_wfi`; `punchbowl/level1/dynamic_stray_light.py` builds per-WFI stray-light models; CHANGELOG 0.0.24 PR #979 fixes labelling of "WFI-3" in `plot_punch`. **Submitter note:** because the three names are byte-identical, the SPASE identifier must be the de-duplication key on submission — do not submit these by name.*

*Considered and rejected (audit trail):* `WISPR Inner/Outer Telescope` — the substring search matched `Parker Solar Probe … Wide-field Imager for Solar Probe, WISPR …` rows, but punchbowl only mentions "wispr" once (`punchbowl/level1/alignment.py:88`, in a comment about a distortion-model technique) and reads no WISPR data. `SOHO/LASCO` and `STEREO/COR2` (`punchbowl/level1/stray_light.py:869-870`) and `STEREO` (`punchbowl/level2/bright_structure.py:38`) are prose about algorithmic heritage only. Gaia — `punchbowl/level1/alignment.py` reads a Gaia star catalog as an astrometric reference, but punchbowl processes no Gaia data products and a user searching for Gaia software would not expect punchbowl; there is also no Gaia row in the `type: 1` vocabulary.

---

### 32. Related Observatories (OPTIONAL)
*Status: all NEW (the HSSI record has no related observatories). Resolved against `http://localhost/api/models/InstrumentObservatory/rows/all/`, `type: 2`. All identifiers verified to resolve (HTTP 200).*

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

**No hard blockers:** every instrument and observatory resolved to exactly one SPASE row (or, for WFI, to three rows each individually evidenced). Nothing required a `NEEDS MANUAL RESOLUTION` marking, and no name is emitted without a `https://spase-metadata.org/` identifier.

---

### 33. Logo (OPTIONAL)
https://punch.space.swri.edu/images/punch-logo_240w.png

*Status: UNCHANGED. Source: existing HSSI record. Verified live on 2026-07-28 (HTTP 200, `image/png`). The repository also ships `docs/_static/logo.png`, but that is not a stable public URL, so the seeded value is kept. **Note:** SoMEF proposed `https://contrib.rocks/image?repo=punch-mission/punchbowl`, which is the contributors-avatar mosaic from `README.md:74`, not a logo — rejected.*

---

## Proposed removals / replacements

Nothing is proposed for **removal**. Every value present in the seeded HSSI record appears above. The following are **replacements**, each with the authoritative evidence that supersedes the seeded value.

| # | Field | Existing HSSI value | Proposed value | Evidence |
|---|-------|--------------------|----------------|----------|
| 1 | 12 Version | `punchbowl - 0.0.19` | `0.0.24`, released 2026-07-28, version DOI https://doi.org/10.5281/zenodo.21640289 | Git tag `0.0.24` (2026-07-28, reachable from `527b32ad`); PyPI `info.version = "0.0.24"`, sdist uploaded `2026-07-28T08:37:33Z`; Zenodo record 21640289 `"version": "0.0.24"`; `CITATION.cff` `version: 0.0.24`, `date-released: 2026-07-28`. Purely stale — 5 releases behind. |
| 2 | 8 Description | 3-sentence description ending "…along with example notebooks." | Same 3 sentences **verbatim**, plus one appended sentence covering the absorbed `punchbowl.auto` SOC automation layer | `CHANGELOG.rst:221` "Moves punchpipe into punchbowl auto subpackage. (#771)"; `docs/automation/index.rst`; `pyproject.toml [project.scripts] punchpipe = "punchbowl.auto.cli:main"`; the `punchbowl/auto/` tree; `punch-mission/punchpipe` archived per the GitHub API. Materially incomplete, not a stylistic rewrite — the submitter's wording is untouched. |
| ~~3~~ | 6 Authors | ~~Person `Sam Van` `Kooten`~~ → now `Sam` `Van Kooten` in the live database (ORCID 0000-0002-4472-8517) | **NO CHANGE PROPOSED — withdrawn 2026-07-28** | The surname mis-split this row targeted was **already fixed** by a user-approved direct database correction to the shared `website_person` row `5543956f-39bf-41cf-8fe6-4ab41d39ee7b`, applied on 2026-07-28 by the concurrent **regularizePSF** worker (issue #57): `given_name` "Sam Van" → "Sam", `family_name` "Kooten" → "Van Kooten". Re-fetching `GET /api/view/software/37a18000-2d1f-41db-afe6-6545f817bcb7/` and diffing against the original snapshot shows those two lines as the **only** difference (author count still 10, affiliation and ordering intact). Field 6 has been aligned to the database value `Sam` / `Van Kooten` rather than proposing the `CITATION.cff` variant "Samuel J.", because `Person` is shared across packages and HSSI cannot express a per-entry given name. **Nothing to patch.** |
| 4 | 6 Authors | Person `Sarah Kovak` (ORCID 0000-0003-1714-5970) | `Sarah Kovac`, same ORCID — **APPLIED 2026-07-28** | `CITATION.cff` line 44 `family-names: "Kovac"`; Zenodo/DataCite creator `Kovac, Sarah`; `pyproject.toml` `{ name = "Sarah Kovac" }`. Simple misspelling. The PATCH attempt no-opped as predicted; applied instead by approved guarded direct database correction to shared Person row `24cb65e7-be66-4f5b-a668-09dedf5717d2`, then verified live in both punchbowl and solpolpy. |
| 5 | 6 Authors | Person `Raphael Attie` (ORCID 0000-0003-4312-6298) | `Raphael Attié`, same ORCID — **APPLIED 2026-07-28** | `CITATION.cff` line 36 `family-names: "Attié"`; Zenodo/DataCite creator `Attié, Raphael`. Missing diacritic. The PATCH attempt no-opped as predicted; applied instead by approved guarded direct database correction to shared Person row `40c2afb0-dfef-4be8-9ac7-12a046cb71c6`, then verified live in both punchbowl and SunPy. |

**Outcome for rows 3-5:** all three are resolved. The HSSI API silently no-ops `Person` renames (a PATCH reports success but the row is unchanged), which is exactly what happened when rows 4 and 5 were sent. Row 3 was withdrawn because a concurrent worker had already fixed it directly; rows 4 and 5 were applied on 2026-07-28 by an approved, guarded direct database transaction and roundtrip-verified. Matching ORCIDs meant no duplicate author rows were ever at risk.

## Open questions for the reviewer — RESOLVED

All 8 items raised at extraction were reviewed by the user on 2026-07-28. The decision trail is preserved below; each item records the original question and the resolution actually applied to this file.

1. **Field 30 / punchpipe.** *Question:* punchpipe is archived and merged into `punchbowl.auto`; keep it in Field 30 (Interoperable Software) as well as Field 29, or Field 29 only? — **RESOLVED: keep punchpipe in BOTH Fields 29 and 30.** No change made; https://doi.org/10.5281/zenodo.17873783 remains in both fields, UNCHANGED.
2. **Field 30 / astropy.** *Question:* astropy was excluded under the Tier B "cited evidence" rule despite the `GCRSWCS(WCS)` subclass and the `custom_stokes_symbol_mapping` registration; add it? — **RESOLVED: ADD astropy to Field 30 only, NOT to Field 29.** Applied: https://doi.org/10.5281/zenodo.4670728 (astropy's own `CITATION.cff` Concept DOI, verified HTTP 200) is now an accepted Field 30 entry marked `Status: NEW`, and it has been removed from that field's "domain-adjacent but no demonstrated peer exchange" rejected list so the two no longer contradict each other. Field 29 is untouched.
3. **Field 22 / F-corona.** *Question:* add a custom "F-corona" phenomenon, absent from HSSI's 7-row Phenomena vocabulary? — **RESOLVED: do NOT add.** No change made; Field 22 remains Coronal Mass Ejections, Solar Corona, Solar Wind.
4. **Field 20 / Windows.** *Question:* `README.md` gives Windows venv activation instructions, but CI is Linux-only and the `super_user` extra pulls in POSIX-only `astrometry`/`sep`; add Windows? — **RESOLVED: do NOT add Windows.** No change made; Field 20 remains Linux, Mac.
5. **Field 6 / Courtney Peck's affiliation.** *Question:* repository e-mail says `@swri.org`, but her ORCID currently lists Laboratory for Atmospheric and Space Physics and Cooperative Institute for Research in Environmental Sciences. — **RESOLVED: keep Southwest Research Institute.** No change made; the ORCID discrepancy is noted under Field 6 but deliberately not applied.
6. **Field 14 / Reference Publication.** *Question:* promote https://doi.org/10.5281/zenodo.8412310 ("Interoperability of PUNCH software in the Python ecosystem") from Related Publications to Reference Publication? — **RESOLVED: no.** No change made; Field 14 stays "Not found" and the DOI remains under Field 27.
7. **Field 28 / dataset breadth.** *Question:* only 8 of the 39 non-seeded SDAC PUNCH dataset DOIs were added; add the remaining 31 per-spacecraft, per-polarization L0/L1 children? — **RESOLVED: add ALL of them — maximum comprehensiveness.** Applied: the DataCite query was re-run with paging on 2026-07-28 and reported `meta.total = 43`, matching the earlier count; all 43 DOIs are now listed in Field 28 (4 seeded UNCHANGED + 39 NEW), every one enumerated from the API rather than pattern-generated, and every one verified HTTP 200 both at `api.datacite.org` and at `doi.org`. The previous "deliberately omitted" note has been replaced by a completeness note.
8. **PyHC.** *Question / finding:* punchbowl is **not** registered in any PyHC list — all three registry files (`projects_core.yml` 7 entries, `projects.yml` 57, `projects_unevaluated.yml` 29) were fetched and parsed in full on 2026-07-28 with no punchbowl entry; two of its companions (regularizePSF, CCSDSPy) are PyHC community packages. — **RESOLVED: informational only, no action.** No PyHC-curated metadata was available to override other sources, and none was invented.

**Additional validator findings resolved by the user as NO-ACTION (recorded for the trail; no field changed):** do not add Jeffrey Hedlund to Field 6 Authors; do not rename the "NCAR High Altitude Observatory" organization; Field 15 License stays "GNU Lesser General Public License v3.0 only". The only validator-driven text change applied was the Field 10 citation correction described below.

**Validator W3 — Field 10 / Field 12 citation correction (applied):** the Field 10 evidence note previously attributed the earliest PyPI upload, `2024-11-01T14:45:44.134455Z`, to `punchbowl-0.0.4`. That timestamp belongs to `punchbowl-0.0.0.tar.gz`; `punchbowl-0.0.4.tar.gz` was uploaded `2024-11-13T17:55:38.815434Z` (both re-verified against `https://pypi.org/pypi/punchbowl/json`). The cited version string is now `punchbowl-0.0.0`. **The Field 10 value (2024-11-01) and the Field 12 value (0.0.24 / 2026-07-28 / https://doi.org/10.5281/zenodo.21640289) are correct and were not changed** — this was a citation-text fix only.

### Baseline drift and later decisions (2026-07-28, after the first validation pass)

**Baseline-drift event.** While this extraction was in review, the shared HSSI database changed underneath it. A concurrent **regularizePSF** worker (also issue #57) applied a user-approved **direct database correction** to the shared `website_person` row `5543956f-39bf-41cf-8fe6-4ab41d39ee7b` (ORCID https://orcid.org/0000-0002-4472-8517): `given_name` "Sam Van" → "Sam" and `family_name` "Kooten" → "Van Kooten". A direct DB edit was required because `Person` is a shared entity across ndcube, punchbowl, regularizePSF and SunPy, and the HSSI API cannot rename a Person — it matches on identifier and refuses to overwrite a non-blank name. The drift was confirmed by re-fetching `GET http://localhost/api/view/software/37a18000-2d1f-41db-afe6-6545f817bcb7/` and diffing against the original seed: exactly **two** lines differ (`authors[3].givenName`, `authors[3].familyName`); author count is still 10 and the Southwest Research Institute affiliation and ordering are unchanged. **The live reference snapshot is now `/tmp/punchbowl_hssi_live2.json`, superseding `/tmp/punchbowl_hssi_current.json`.**

9. **Field 6 / Van Kooten's given name.** *Question:* the file recorded the `CITATION.cff` variant `Samuel J.` / `Van Kooten`, but the shared HSSI Person row now reads `Sam` / `Van Kooten`. — **RESOLVED: record `Sam` / `Van Kooten` to match the shared database row.** Applied: the Field 6 entry now reads `Sam` / `Van Kooten` with ORCID and the SwRI affiliation untouched, and carries a note that both name forms are correct, that HSSI's row was corrected directly by the regularizePSF worker on 2026-07-28, and that HSSI has no per-entry given-name override (so sending "Samuel J." would silently no-op and leave the file permanently out of sync). The Field 6 status line now counts 2 proposed name replacements rather than 3, and the platform-limitation note no longer lists item 2. **Replacements table row 3 has been struck through and marked "NO CHANGE PROPOSED — withdrawn"**, recording who fixed it and when; the table no longer claims a replacement we are not making. Rows 4 (Kovak→Kovac) and 5 (Attie→Attié) are unaffected and remain proposed.

10. **Field 26 / Award Number.** *Question:* Field 26 said "Not found", but the value exists in HSSI. — **RESOLVED: record `80GSFC18C0014` as an already-present HSSI value, not as a proposed change.** Applied: verified on 2026-07-28 that `http://localhost/api/models/Award/rows/all/` row `03ab3ee8-fbc6-4a4e-a2da-da87a6c2d5ab` holds `name: "Polarimeter to UNify the Corona and Heliosphere (PUNCH)"` / `identifier: "80GSFC18C0014"`, uniquely among 38 rows, and that punchbowl's live record already carries that award title. It is **not** added to the removals/replacements table and **must not be patched** — the backend discards a submitted award `name` when the `identifier` matches an existing row. **Correction to the brief given for this edit:** the instruction stated that external corroboration had failed, but a targeted search here *did* find one — NASA NTRS record `20220017302` ("The Coronal Veil", Malanushenko, Cheung, DeForest, Klimchuk & Rempel) lists `CONTRACT_GRANT: 80GSFC18C0014`, and DeForest is a punchbowl author and the PUNCH PI at SwRI. That confirms the number is a real NASA contract associated with DeForest/SwRI, but **not** that it is specifically the PUNCH SMEX award, and no punchbowl-side source (repository, DataCite `fundingReferences`) mentions it. Field 26 records this partial, qualified corroboration rather than either "not found" or an unqualified endorsement.

---

## Roundtrip verification (2026-07-28)

`PATCH http://localhost/api/data/software/37a18000-2d1f-41db-afe6-6545f817bcb7/` — **HTTP 200**. Response `fieldsUpdated` listed 16 fields: `authors`, `data_sources`, `description`, `development_status`, `input_formats`, `interoperable_software`, `keywords`, `output_formats`, `related_datasets`, `related_instruments`, `related_observatories`, `related_publications`, `related_region`, `related_software`, `software_functionality`, `version`.

Sent body md5 `6a106baa70231d63780b5152d54b3147` (16 keys, 15 authors, no `award`). The baseline was re-fetched and confirmed byte-identical to the approved plan's baseline immediately before sending.

### Verified landed

| Check | Result |
|---|---|
| Omitted fields (16) untouched | **PASS** — 0 of 16 changed |
| `softwareFunctionality` | **PASS** — 50 sent / 50 live |
| `relatedDatasets` | **PASS** — 43 / 43 |
| `keywords` | **PASS** — 21 / 21 (render title-cased; `photometry`, `polarimetry` rows created) |
| `interoperableSoftware` | **PASS** — 8 / 8 |
| `relatedSoftware` | **PASS** — 6 / 6 |
| `relatedRegion`, `dataSources`, `inputFormats`, `outputFormats`, `relatedPublications` | **PASS** — exact set match |
| `description` | **PASS** — byte-exact |
| `developmentStatus` | **PASS** — `Active` |
| `version` | **PASS** — `punchbowl - 0.0.24` |
| Authors | **PASS** — 10 → 15, **0 dropped**, 0 missing, 0 unexpected |
| Affiliations of the 10 pre-existing authors | **PASS** — all counts unchanged |
| Fields 31/32 | **PASS** — 4/4 and 5/5 **distinct** rows, SPASE identifier sets exactly equal to sent, all `https://spase-metadata.org/` |

The three byte-identical "Wide Field Imager" names bound to three distinct rows as designed — `…/WFI/1` → `2cd25d1e-ef8f-4a9e-af81-b9ac8b881efe`, `…/WFI/2` → `01f55e2d-c320-4ab2-99e6-43869e6a8c0a`, `…/WFI/3` → `288c9a7a-17fa-4b2a-800c-1f159991ae88`; NFI → `41005ef5-3095-468e-bd96-afbb896cdc35`. Identifier keying worked; no collapse.

### Shared-record corrections applied by approved direct database edit (2026-07-28)

Three defects could not be expressed through the API. `_get_or_create_person()` only fills **blank** names on an ORCID match, so name corrections silently no-op; and `_get_or_create_org()` resolves by identifier with `.first()` and then calls `affiliation.add(...)`, which attaches a second row when two Organization rows share one ROR. All three were corrected in a single guarded transaction against the active `postgres` database on container `website_db`, under explicit approval, with full backups taken first.

| Shared row | Before | After | Also affects |
|---|---|---|---|
| Person `40c2afb0-dfef-4be8-9ac7-12a046cb71c6` (ORCID 0000-0003-4312-6298) | `Raphael Attie` | **`Raphael Attié`** | SunPy |
| Person `24cb65e7-be66-4f5b-a668-09dedf5717d2` (ORCID 0000-0003-1714-5970) | `Sarah Kovak` | **`Sarah Kovac`** | solpolpy |
| Person-affiliation through-row `3074` (Samuel T. Badman) | 2 affiliations, both ROR `03c3r2d17` | **1 affiliation** (row `2474`, `7706c349…`) | PySPEDAS, SunPy |

The duplicate affiliation was introduced by this refresh's PATCH and had been predicted before it was sent. The two name defects were pre-existing.

Verification after the transaction: total `Person` count unchanged at 861; total affiliations 527 → 526; both Organization rows for ROR `03c3r2d17` still present and unmodified (reference counts 1 and 9); Katharine Reeves's affiliation row `2795` intact; 7 authorship rows across the three people unchanged. All four affected software views (`punchbowl`, `SunPy`, `solpolpy`, `PySPEDAS`) were diffed pre/post and showed **only** the three intended changes — no unrelated difference anywhere. punchbowl retained all 15 authors with no non-author field altered.

Two further no-ops were left uncorrected **by decision**, because the live HSSI forms are the fuller and better ones and are now recorded in Field 6: `Nicholas A. Murphy` (CITATION.cff says "Nick") and `Samuel T. Badman` (CITATION.cff says "Samuel"). Van Kooten (0000-0002-4472-8517) needed no change — the shared row had already been corrected directly on 2026-07-28 by the regularizePSF worker.

Nicholas A. Murphy carries three affiliations (SAO, CfA, Smithsonian Institution) — all **distinct** RORs accumulated across software entries, not a duplication.

**Related catalog defect, deliberately NOT included in the approved transaction:** a second Person row `e241cbf2-b3b5-4359-bb36-181988b2de34`, also named `Raphael Attie`, exists with **no ORCID** and is fully orphaned (0 authorships, 0 affiliations, 0 curator rows, 0 submitter rows). It is not user-visible. It was deleted on 2026-07-28 under separate explicit approval by a guarded single-row transaction (`Person` count 861 → 860; the ORCID-bearing `Raphael Attié` row and all its relationships verified intact; punchbowl and SunPy views showed zero difference afterwards).

### Values recorded in this file that HSSI does not render

- Field 15 License URI `https://spdx.org/licenses/LGPL-3.0-only.html` — already on the shared `License` row; not patched.
- Field 26 Award Number `80GSFC18C0014` — already on Award row `03ab3ee8-fbc6-4a4e-a2da-da87a6c2d5ab` and already linked; not patched.

---

## Final state

All Fields 2–33 in this file match live HSSI as of 2026-07-28, verified by roundtrip after the API update and again after the approved shared-record database corrections. No value present in the original submitted record was dropped.

Nothing remains open. The orphaned, ORCID-less duplicate `Raphael Attie` Person row `e241cbf2-b3b5-4359-bb36-181988b2de34` was deleted on 2026-07-28 under separate explicit approval by a guarded single-row transaction: total `Person` count 861 → 860, no other row touched, and the ORCID-bearing `Raphael Attié` row `40c2afb0-dfef-4be8-9ac7-12a046cb71c6` verified intact with its 2 authorships and 2 affiliations. The punchbowl and SunPy views were re-diffed afterwards and showed **zero** differences, confirming the orphan had never been user-visible.
