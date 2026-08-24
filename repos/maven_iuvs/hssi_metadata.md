# HSSI Metadata Extraction Results

**HSSI Software ID:** e2ca7d39-4fae-4ced-9dc2-b2593241b407
**Repository:** https://github.com/lasp/maven_iuvs
**Source Revision:** 1759ab562d379f177a61ed85aed26542b2b82894
**Extraction Date:** 2026-08-06
**Validation Date:** 2026-08-23
**Validation Status:** PASS

---

**Scope note — how to read the evidence in this file.** `maven_iuvs` is an instrument-team working
repository, not a released package. It has no tags, no GitHub releases, no PyPI distribution, no
DOI, no LICENSE file, no CITATION.cff, no codemeta.json, no `.zenodo.json` and no CI configuration
(`.github/` contains only `pull_request_template.md`). Consequently almost every field below is
derived from the source tree itself — module and function-level code reading — rather than from
packaging metadata, a DOI record, or a registry entry. Where a field is empty, the note records what
was searched so a future agent does not repeat the search. Several routines also assume resources
that are not in this repository (local IUVS data holdings, SPICE kernels, and the IUVS team's IDL
pipeline), which is why some capabilities are attested by the code that drives them rather than by
runnable examples.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This record already exists in HSSI; the submitter fields belong to the original submission and are
not part of the metadata this file describes.

### 2. Persistent Identifier (RECOMMENDED)
Not found.

Negative research: the repository contains no CITATION.cff, no codemeta.json, no `.zenodo.json`, no
DOI badge in `README.md`, and no DOI string anywhere in the tracked `.py`/`.md`/`.in` files. A
DataCite query for `"maven_iuvs"` returned zero records. GitHub reports no releases for
`lasp/maven_iuvs`, so there is no GitHub-Zenodo archive to mint a concept DOI from, and the package
is not on PyPI (both `maven_iuvs` and `maven-iuvs` return HTTP 404). Nothing to record; this field
should remain empty until the team archives a release.

Rejected candidate: `https://doi.org/10.5281/zenodo.593914` is already stored on this record as
Interoperable Software (Field 30) and is SpiceyPy's concept DOI, not this software's. It must never
migrate into this field.

### 3. Code Repository (MANDATORY)
https://github.com/lasp/maven_iuvs

Carried over from the existing HSSI record and re-confirmed: the local clone's `origin` remote is
this URL, `setup.py` declares the same `url`, and the URL returns HTTP 200. Default branch is
`master`; the repository has no other branches. Source revision for this extraction is
`1759ab562d379f177a61ed85aed26542b2b82894` (committed 2026-06-22).

### 4. Software Functionality (MANDATORY)

- Coordinate Transforms
- Coordinate Transforms: Magnetospheric
- Coordinate Transforms: Mission-Specific
- Coordinate Transforms: Planetary
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 3D Graphics
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: Orbit Plots
- Mission-related
- Mission-related: Analysis
- Mission-related: Archive
- Mission-related: Calibration
- Mission-related: Instrument Response
- Mission-related: Inventory
- Mission-related: Monitoring
- Mission-related: Orchestration
- Mission-related: Processing
- Mission-related: Science Data Processing
- Models and Simulations
- Models and Simulations: Forward-Fitting
- Models and Simulations: Instrument Response
- Models and Simulations: Physics-Based

The record previously carried only `Data Processing and Analysis` and
`Data Processing and Analysis: Data Access and Retrieval`. Both are retained; the rest are recorded
because the roughly 15,600 lines of Python in this repository implement substantially more than data
retrieval.

Evidence for each value, keyed to source:

- **Coordinate Transforms / Coordinate Transforms: Planetary** — `geometry.py` computes IAU_MARS
  surface intercepts and sub-points (`spice.sincpt`, `spice.subpnt`, `spice.subslr`,
  `spice.recsph`), converts longitude/latitude to IAU_MARS vectors (`transform_lonlat_to_iau_vec`),
  and derives per-pixel solar zenith, emission, zenith, phase and local-time angles
  (`get_pixel_corner_sza`, `get_pixel_corner_local_time`, `get_pixel_corner_emission_angle`,
  `get_pixel_corner_zenith_angle`, `get_pixel_corner_phase_angle`). `graphics.py` builds cartopy
  `RotatedPole`, `NearsidePerspective` and `Orthographic` projections of the Martian disk
  (`rotated_transform`, `highres_NearsidePerspective`, `highres_Orthographic`, `latlon_meshgrid`,
  `latlon_grid`). These are user-facing: the README advertises "Standardized projections of IUVS
  data."
- **Coordinate Transforms: Mission-Specific** — `geometry.get_pixel_vec_mso` rotates pixel vectors
  from `IAU_MARS` into the spacecraft-specific `MAVEN_MSO` frame via `spice.pxform`;
  `geometry.beta_flip` determines instrument/spacecraft attitude by comparing the instrument x-axis
  to the spacecraft velocity in an inertial frame; `geometry.obs_in_orbit_plane` flags integrations
  where the Articulated Payload Platform is out of the orbit plane; `spice.py` loads MAVEN CK, SPK
  and SCLK kernels (`load_sc_ck`, `load_sc_spk`, `load_sc_sclk`, `load_iuvs_spice`).
- **Coordinate Transforms: Magnetospheric** — `geometry.get_pixel_vec_mso` transforms pixel vectors
  into `MAVEN_MSO` (Mars-Solar-Orbital) at `geometry.py:837`. MSO is the Mars analogue of Earth's GSE
  frame — Sun-pointing X, Z normal to the planet's orbital plane — and this taxonomy assigns
  GSE-family frames to `Magnetospheric`; MSO is also the conventional frame for Mars magnetospheric
  and plasma science, and Field 5 records `Mars Magnetosphere` as a served region, so a searcher
  combining that region with a magnetospheric-coordinate requirement should find this record.
  Recorded with an explicit caveat so the placement is not over-read: this package performs no
  magnetic-field analysis, and its MSO transform serves remote-sensing viewing geometry rather than
  magnetospheric physics. `Coordinate Transforms: Planetary` remains the primary and more precise
  placement; `Magnetospheric` classifies the *frame family*, not a capability claim. The alternative
  — filing MSO under `Mission-Specific` alone, on the grounds that `MAVEN_MSO` is defined in MAVEN's
  own SPICE frame kernel — was rejected because the frame is Mars-relative and solar-oriented rather
  than spacecraft-attitude-relative; `Mission-Specific` is carried instead by the attitude and
  kernel-handling evidence in the bullet above.
- **Data Processing and Analysis: Data Access and Retrieval** — `download.sync_data` rsyncs IUVS
  L1A/L1B data and SPICE kernels from the IUVS team virtual machine; `download.sync_euvm_l2b` and
  `download.sync_integrated_reports` authenticate to and download from the MAVEN Science Data Center
  team site; `download.sync_sdc` drives both. `search.find_files`, `search.get_apoapse_files` and
  `search.get_latest_files` query local holdings by orbit, segment, channel and version.
- **Data Processing and Analysis: Calibration** — `instrument.calculate_calibration_curve` produces
  a DN/kR spectral calibration curve from the effective area table
  (`ancillary/iuvs_effective_area.h5`); `instrument.mcp_dn_to_volt` and `instrument.mcp_volt_to_gain`
  implement the microchannel plate gain curve; `instrument.convert_spectrum_DN_to_photoevents` and
  `instrument.DN_to_PE_conversion_factor` convert DN to photoevents; `integration.get_lya_flatfield`
  applies a stellar-derived Lyman-alpha flat field; `echelle.get_conversion_factors` and
  `echelle.convert_to_physical_units` convert fitted quantities into kR/nm for calibration versions
  v13/v14/v15.
- **Data Processing and Analysis: Data Reduction** — `echelle.subtract_darks`,
  `echelle.get_dark_frames`, `echelle.coadd_lights`, `echelle.find_bad_light_frames`,
  `echelle.find_bad_dark_frames`, `echelle.get_corrupt_frames`; `binning.py` handles spatial and
  spectral bin edges, pixel-to-bin mapping and padding of missing bins (`get_bin_edges`,
  `pix_to_bin`, `get_npix_per_bin`, `pad_data_with_missing_bins`).
- **Data Processing and Analysis: Image Processing** — `echelle.remove_cosmic_rays` (median/MAD
  outlier rejection over frames), `echelle.remove_hot_pixels` (sliding-window significance test via
  `vectorized_window_Fsig`), `echelle.clean_data`, `graphics.sharpen_image` (unsharp masking),
  `graphics.resize_data` (`skimage.transform.resize`), `graphics.get_flatfield`,
  `graphics.altitude_mask`.
- **Data Processing and Analysis: File Format Conversion** — `echelle.convert_l1a_to_l1c` takes an
  L1A FITS file through to an L1C product; `scipy.io.idl.readsav` converts IDL save files (EUVM L2B,
  `lsf_new.idl`, the Mayyasi light/dark key `.sav`) into Python structures; fitted arrays and
  parameters are written to CSV (`echelle.prep_output_and_writeout`, `np.savetxt`,
  `DataFrame.to_csv`); file indexes are serialized to `.npy`.
- **Data Processing and Analysis: Analysis / Processing** — both catch-alls apply and are kept
  deliberately. `Analysis` covers the scientific work: `statistics.multiple_linear_regression`
  (template fitting via `sklearn.linear_model.LinearRegression`), `statistics.integrate_intensity`,
  `statistics.chisquared` (correlated-Gaussian reduced chi-squared),
  `echelle.get_countrate_diagnostics`, `echelle.get_lya_countrates`, `geometry.get_mean_mrh`.
  `Processing` covers the pipeline-step transforms themselves (`echelle.clean_data`,
  `echelle.get_spectrum`, `echelle.add_in_quadrature`, `instrument.ran_DN_uncertainty`).
- **Data Visualization: 2D Graphics** — `graphics/line_fit_plot.detector_image` and `plot_detector`
  (pcolormesh detector images), `graphics.bin_centers_2d` and `bin_pixels_2d` (map binning of IUVS
  pixels), `graphics.latlon_grid`, `geometry.highres_swath_geometry` (rendered swath with twilight
  shading over a Mars surface map), plus purpose-built colormaps for NO, CO2+, CO and H emissions
  (`NO_colormap`, `CO2p_colormap`, `CO_colormap`, `H_colormap`, `rainbow_colormap`).
- **Data Visualization: 3D Graphics** — `graphics/maven_orbit_image.py` renders a textured Mars
  sphere and the MAVEN orbit in 3D using `mayavi.mlab` and `tvtk` (`TexturedSphereSource`,
  `mlab.plot3d`, offscreen screenshot capture).
- **Data Visualization: Line Plots** — `graphics/echelle_graphics.plot_line_fit`,
  `example_fit_plot`, `plot_line_fit_comparison`, `plot_background_in_no_spectrum_region`;
  `graphics.make_sza_plot`, `make_alt_plot`, `make_tangent_lat_lon_plot`.
- **Data Visualization: Mission-Specific** — `graphics/echelle_graphics.run_quicklooks`,
  `quicklook_figure_skeleton` and `make_one_quicklook` build the IUVS echelle quicklook figure
  layout (thumbnail grid of detector frames plus geometry, solar-zenith-angle and altitude panels)
  that exists only for this instrument's data; `graphics/line_fit_plot.LineFitPlot` composes the
  IUVS detector-plus-line-fit figure.
- **Data Visualization: Orbit Plots** — `maven_orbit_image.maven_orbit_image` and
  `maven_orbit_summary` draw the MAVEN spacecraft trajectory (with view-from-periapsis and
  view-from-orbit-normal options); `graphics.mars_orbit_path`, `graphics.mars_orbit_path_position`
  and `graphics.plot_solar_longitude` draw Mars's orbit about the Sun.
- **Mission-related** and its subcategories — this package is an instrument-team tool, not a
  general-purpose reader that happens to open MAVEN files, which is what distinguishes it from
  "Data Processing and Analysis" alone:
  - *Science Data Processing* / *Processing*: `echelle.convert_l1a_to_l1c` is the L1A-to-L1C science
    product pipeline, and `RUN_ECHELLE_v15_PIPELINE.py` is its production driver.
  - *Calibration*: the calibration-version machinery (`calibration="v13"|"v14"|"v15"`,
    `echelle.get_binning_df`, `echelle.load_lsf`) is mission calibration bookkeeping, distinct from
    the physics of the DN-to-kR conversion.
  - *Instrument Response*: `instrument.py` encodes the IUVS instrument model — slit width and
    field-of-regard, port separation, detector pixel size, focal length, MUV/FUV dispersion, slit
    pixel extents, echelle Lyman-alpha slit indices, LSF unit — together with the effective-area
    table and MCP gain curve; `integration.get_lsf`, `get_lsf_from_bins` and `get_lsf_interp` supply
    the line-spread function for a given binning.
  - *Archive*: `pds.verify_pds_completion` checks that every planned L1C FITS file and its XML label
    is present for a numbered PDS delivery; `pds.make_pds_csv` and `pds.get_pds_dates` slice the
    master light/dark key to a delivery's date window; `reprocessing.compare_PDS_with_reprocess`
    reconciles a reprocessing run against the PDS file list.
  - *Inventory*: `echelle.get_dir_metadata`, `update_metadata_file` and `update_index` build and
    incrementally extend a metadata index of the local mission archive; the master light/dark key
    CSVs in `ancillary/` plus `find_files_missing_in_key`, `add_new_files_to_light_dark_key`,
    `update_filenames_in_light_dark_key` and `make_light_and_dark_pair_CSV` maintain the
    observation-pairing inventory; `find_files_missing_geometry` and `find_files_with_geometry`
    track geometry coverage.
  - *Monitoring*: `echelle.weekly_echelle_report` reports on observations taken in the last N weeks,
    `identify_rogue_observations` flags segments with lights but no darks (or missing data),
    `report_orbits_with_observations` summarizes coverage, and `run_quicklooks` generates the figures
    used to assess incoming observations.
  - *Orchestration*: `RUN_ECHELLE_v15_PIPELINE.py` runs a `multiprocessing` worker pool over
    observations, with a dedicated IDL-writer process fed by a command queue, per-observation
    logging, thread-based pipe monitoring (`pipe_processer`, `message_watcher`) and result
    aggregation under a lock; `RUN_ECHELLE_v15_PIPELINE_SERIAL.py` is the serial variant.
  - *Analysis*: the mission-specific science analysis of IUVS observations (H and D brightness
    retrieval, D/H-relevant faint-emission fitting) that the pipeline exists to produce.
- **Models and Simulations: Forward-Fitting** — `echelle.lineshape_model` builds a synthetic
  spectrum (H and D Lyman-alpha lines plus a linear/quadratic background, optionally an
  interplanetary hydrogen component), `echelle.loglikelihood` and `negloglikelihood` score it
  against the data with a correlated-Gaussian likelihood, and `echelle.fit_flat_data` and
  `fit_H_and_D` optimize the parameters with `dynesty` nested sampling or a least-squares fitter;
  `line_fit_initial_guess` supplies priors. This is a textbook forward model plus parameter
  optimization.
- **Models and Simulations: Instrument Response** — the forward model is convolved with the IUVS
  line-spread function through `CLSF_from_LSF` and `interpolate_CLSF`, using the v13/v14/v15 LSFs in
  `ancillary/`; `integration.fit_line` performs the same LSF-convolved fit for arbitrary emission
  lines in L1B files.
- **Models and Simulations: Physics-Based** — `echelle.predict_IPH_linecenter` computes the expected
  interplanetary-hydrogen line center from first principles: it constructs the IPH flow vector in
  ECLIPJ2000 from published upwind direction and speed, obtains Mars's velocity from SPICE
  ephemerides, projects the relative velocity onto the instrument line of sight, and converts to a
  Doppler wavelength shift. `time.Ls` and `Ls_to_et`, and `graphics.terminator`, are further
  physical-geometry calculations.

Considered and rejected, with reasons (recorded so a future agent does not re-propose them):

- **Data Processing and Analysis: Energy Spectra** — this taxonomy entry is oriented to particle
  energy spectra (energy channels, flux versus energy). `maven_iuvs` produces photon brightness
  versus wavelength from a UV spectrograph. Mapping UV spectroscopy onto a particle-spectra category
  would mislead searchers; the spectral work is already carried by `Analysis`, `Processing`,
  `Calibration` and the two `Instrument Response` entries.
- **Data Processing and Analysis: Spectrogram** and **Data Visualization: Spectrogram** — a sweep of
  the package source for `fft`, `wavelet`, `stft`, `periodogram`, `spectrogram` and `welch` returned
  nothing, so there is no time-frequency transform to classify. The detector images are
  spatial-by-spectral arrays, not dynamic spectra.
- **Data Processing and Analysis: Time Series Analysis** — the temporal operations present
  (interpolating EUVM Lyman-alpha to an observation time in `search.get_solar_lyman_alpha`, weekly
  aggregation in `weekly_echelle_report`, apsis finding via `spice.gfdist` in
  `geometry.find_maven_apsis`) are ancillary lookups and scheduling, not a user-facing time-series
  analysis capability. The package's analysis axes are spectral and spatial.
- **Data Visualization: Movies** — searched for `animation`, `FuncAnimation`, `imageio`, `ffmpeg`,
  `gif` and `mp4` across all modules; nothing matched. Figures are written with `plt.savefig` only.
- **Data Visualization: Web-Based**, **2D Slices**, **Hodograms**, **Spacecraft Formation Plots**,
  **ML/AI** — no plotly/bokeh/dash, no volumetric slicing, no field-component hodograms,
  single-spacecraft mission, no machine-learning plots.
- **Mission-related: Distribution/Access** — the package is a *client* of the IUVS virtual machine
  and the MAVEN SDC, not part of the mission's distribution system. The retrieval capability is
  already recorded under `Data Processing and Analysis: Data Access and Retrieval`.
- **Mission-related: Ingest**, **Instrumentation**, **Operations**, **Packet Decommutation**,
  **System Testing**, **Infrastructure as Code**, **ML/AI** — no telemetry ingest or packet parsing,
  no instrument commanding, no spacecraft operations function
  (`download.sync_integrated_reports` merely downloads the MAVEN integrated-report text files; it
  does not perform operations), and `tests/test_science_week.py` is a single unit test of the
  `ScienceWeek` class rather than a system-testing capability.
- **Mission-related: Observatory/Instrument Models** and
  **Models and Simulations: Observatory/Instrument Models** — the instrument-model content
  (`instrument.py`, LSF, effective area, gain curve) is already, and more precisely, captured by the
  two `Instrument Response` entries; adding these would duplicate the same evidence under a vaguer
  label.
- **Models and Simulations: Empirical**, **First Principles**, **MHD**, **Forecasting**,
  **Data Guided**, **Theory**, **Mission-Specific**, **Field-line Tracing** — the package contains
  no empirical climatology, no PDE or MHD solver, no forecast product, no assimilation, no
  field-line tracer. `Physics-Based` and `Forward-Fitting` are the accurate placements.
- **Servers and Environments** and all its subcategories — no server, no Dockerfile or container
  definition, no MPI or job-scheduler integration, no infrastructure-as-code. The `multiprocessing`
  pool in `RUN_ECHELLE_v15_PIPELINE.py` is single-machine parallelism, which is not
  high-performance computing in this taxonomy's sense.

### 5. Related Region (MANDATORY)
- Planetary Magnetospheres
- Mars Magnetosphere
- Interplanetary Space

`Planetary Magnetospheres` is carried over from the existing HSSI record and retained.
`Mars Magnetosphere` is recorded because the `Region` vocabulary contains a Mars-specific row and the
guidance is to prefer the most specific applicable region over a broad one. Essentially all of this
package's science capability targets Mars, so leaving only the generic planetary row understates it.
`Interplanetary Space` is recorded on concrete evidence rather than proximity — the echelle fitting
code models and fits an interplanetary hydrogen component as a first-class feature
(`constants.IPH_wv_spread`, `IPH_minw`, `IPH_maxw`, derived from Quemerais 2006 temperatures;
`echelle.check_whether_IPH_fittable`, `predict_IPH_linecenter`, the `fit_IPH_component` branch of
`lineshape_model`, and the IPH brightness and line-center entries in the fit-parameter
dictionaries).

An important caveat for a future agent: the vocabulary has no row for a planetary *atmosphere*,
*thermosphere*, *exosphere* or *corona* outside Earth. IUVS is an atmospheric remote-sensing
instrument, so the regions this software actually serves — the Martian upper atmosphere, exosphere
and hydrogen corona — are not directly expressible. `Mars Magnetosphere` is the closest available
Mars row and is retained on that basis; the atmospheric science content is carried in Keywords
(Field 16) instead.

Considered and rejected: `Solar Environment` and `Solar Wind` — the package retrieves EUVM solar
Lyman-alpha irradiance (`search.get_solar_lyman_alpha`) purely as a normalization input to Martian
observations; solar physics is not a science target of this software. `Earth`-prefixed rows do not
apply. `Corona` is a solar-corona row in this vocabulary and would be misread if used for the
Martian hydrogen corona.

### 6. Authors (MANDATORY)

Six authors, reconciled as the union of the five authors previously stored in HSSI, the author
string in `setup.py`, and the repository's commit history. No stored author is dropped.

1. **Zachariah Milby**
   - Author Identifier: https://orcid.org/0000-0001-5683-0095
   - Affiliation: Laboratory for Atmospheric and Space Physics — https://ror.org/01fcjzv38
   - Affiliation: University of Colorado Boulder — https://ror.org/02ttsq026
2. **Kyle Connour**
   - Author Identifier: https://orcid.org/0000-0003-0858-2511
   - Affiliation: Laboratory for Atmospheric and Space Physics — https://ror.org/01fcjzv38
   - Affiliation: University of Colorado Boulder — https://ror.org/02ttsq026
3. **Mike Chaffin**
   - Author Identifier: https://orcid.org/0000-0002-1939-4797
   - Affiliation: Laboratory for Atmospheric and Space Physics — https://ror.org/01fcjzv38
   - Affiliation: University of Colorado Boulder — https://ror.org/02ttsq026
4. **Eryn Cangi**
   - Author Identifier: https://orcid.org/0000-0002-8548-4088
   - Affiliation: Laboratory for Atmospheric and Space Physics — https://ror.org/01fcjzv38
   - Affiliation: University of Colorado Boulder — https://ror.org/02ttsq026
5. **Kei Masunaga**
   - Author Identifier: https://orcid.org/0000-0001-9704-6993
   - Affiliation: Laboratory for Atmospheric and Space Physics — https://ror.org/01fcjzv38
   - Affiliation: University of Colorado Boulder — https://ror.org/02ttsq026
6. **Josh Elliott**
   - Author Identifier: https://orcid.org/0000-0002-7209-008X
   - Affiliation: Laboratory for Atmospheric and Space Physics — https://ror.org/01fcjzv38
   - Affiliation: University of Colorado Boulder — https://ror.org/02ttsq026

**Ordering.** The order follows `setup.py`'s author string —
`'Zachariah Milby, Kyle Connour, Mike Chaffin, Eryn Cangi, and the IUVS team'` — with the two
authors HSSI holds but `setup.py` does not name (Masunaga, Elliott) appended. That string is the
only explicit credit statement the project makes about itself.

**What was previously stored, and why each author record reads as it does.**

- Eryn Cangi's stored record was already complete and correct (ORCID plus both affiliations with
  RORs) and is unchanged here. She is by a wide margin the most active contributor: 435 commits, 418
  under `emcangi@protonmail.com` and 17 under her GitHub no-reply address, a total the GitHub
  contributors API independently reports for `emcangi`.
- Mike Chaffin's stored record had both affiliations but no identifier. ORCID `0000-0002-1939-4797`
  is recorded: that record is named "MICHAEL CHAFFIN", lists University of Colorado Boulder
  employment, and carried 76 works at extraction time, dominated by Mars/MAVEN topics (Martian
  proton aurora, Mars thermosphere composition, water escape). A second ORCID, `0009-0007-7342-2668`
  ("Michael S Chaffin"), was examined and rejected: it carried no employment entries and no works,
  so it cannot be tied to this person's scholarly identity. His GitHub account is `planetarymike`
  (profile name "Mike Chaffin", company "LASP, University of Colorado"), which authored 109 of the
  commits here.
- Josh Elliott's stored record had neither identifier nor affiliation. ORCID `0000-0002-7209-008X`
  (Joshua Elliott) is recorded on converging evidence: that record lists "Software Engineer III /
  Professional Research Assistant" at the Laboratory for Atmospheric and Space Physics from
  2016-04-25 to 2023-10-06 — a window that contains all of his commits here — followed by the Jet
  Propulsion Laboratory; and its earlier NEON Airborne Observation Platform employment and Cassini
  UVIS and SORCE/SOLSTICE works line up with the public repositories on his GitHub account
  `spacemanjosh` (`NEON-AOP-H5toENVI`, `pyuvis`, `sorce-occultations`). His two commits are the
  repository's root commit `2a1b844` and `2c675e5` ("Create README.md"), both on 2019-04-08 — that
  is, he created the repository, which is why its GitHub creation timestamp and its root commit
  timestamp coincide (see Field 10). He is at JPL now; the LASP/CU Boulder affiliation recorded here
  is the one contemporaneous with his contributions to this software.
- **`kconnour` is Kyle Connour.** The stored author record was the bare GitHub username, with no
  given name at all. The GitHub API attributes commit `237f355e` (2019-04-09, titled "Initial
  commit" and the first to add substantive code, though third in the history — see Field 10) to
  account `kconnour`, with commit author `Kyle Connour <Kyle.Connour@colorado.edu>`, and `setup.py`
  names Kyle Connour. ORCID `0000-0003-0858-2511` is recorded: the works listed on that record at
  extraction time were MAVEN/IUVS Mars aerosol and cloud retrievals, co-authored with the LASP IUVS
  team (Michael J. Wolff, Nicholas M. Schneider, Justin Deighan). The ORCID record itself lists no
  employment, so the LASP and CU Boulder affiliations here are inferred from his `colorado.edu`
  commit address and his MAVEN/IUVS co-authorship with that group; they match the affiliations
  already stored for his co-authors.
- **`keimasunaga` is Kei Masunaga.** Same defect in the stored record — bare username, no given
  name. ORCID `0000-0001-9704-6993` is recorded: that record lists "JSPS overseas research
  fellowship postdoc" at University of Colorado Boulder with department "Laboratory for Atmospheric
  and Space Physics", which is the period around his 2021-01-04 commit here, and its works include
  MAVEN observations of Mars (for example C+ 133.5 nm emission mechanisms). Independent
  corroboration from inside the repository: `ancillary/kei_flatfield_polynomial_25Nov2020.npy` is
  the flat-field polynomial the package loads in `integration.get_lya_flatfield`. His current post
  is at Yamagata University (https://ror.org/00xy44n04); the LASP/CU Boulder affiliation recorded
  here is the one contemporaneous with his contribution, consistent with the treatment of the other
  authors.
- **Zachariah Milby was missing from the stored record entirely.** `setup.py` names him first, he
  authored 23 commits (including `cd54ca0`, "Initial updates to structure, documentation", which
  introduced the package's version declaration, and `8c4d45f`, the rename from PyUVS to maven_iuvs),
  and his commit address was `zachariah.milby@lasp.colorado.edu`. ORCID `0000-0001-5683-0095` is
  recorded: of the 16 works listed on that record at extraction time, nine are MAVEN/IUVS Mars
  papers (discrete aurora at Mars from MAVEN/IUVS observations, NO nightglow and Martian mesospheric
  circulation, Mars's twilight cloud band). He is now a planetary-science postdoc at Caltech (GitHub
  `zachariahmilby`); the LASP/CU Boulder affiliation recorded here is the one contemporaneous with
  his contributions.

**Why two of these identities rest on external evidence rather than on what was stored.** The
author records for `kconnour` and `keimasunaga` were bare GitHub usernames with no given name — a
login handle standing in for a person. The human identities and ORCIDs above are what those two
records should say, and the evidence establishing each is set out in the bullets above so the
usernames are not mistaken for names again.

**A durable HSSI constraint worth knowing before any future author change.** The API cannot rename
an existing person record, and it matches people by ORCID. A person whose stored record carries no
ORCID therefore presents no reliable key to match on and no way to correct a wrong stored name, so
an author-identity defect of that kind is not something a routine metadata update can repair. That
is also why an ORCID is recorded for each of the six authors above: the ORCID is what keeps an
author record durably identifiable across later updates.

**Considered and not listed as authors.**

- *Jaden Strommer* appears once in the commit history (`ecda65d`, 2025-06-02, "First Commit to Get
  Rid of Syntax Warning Message"). A single warning-suppression commit does not make someone an
  author of the software, and `setup.py` does not credit them. Recorded here so the name is not
  mistaken for an omission.
- *"the IUVS team"* is the trailing element of `setup.py`'s author string. It was considered as an
  organization author, which HSSI supports via a `ror.org` identifier, and rejected: it is a
  collective courtesy credit rather than a registered organization, and no ROR resolves for it. The
  institutional identity is already captured by the LASP and CU Boulder affiliations on the
  individual authors.

### 7. Software Name (MANDATORY)
maven_iuvs

Carried over from the existing HSSI record and confirmed against `setup.py` (`name='maven_iuvs'`),
the top-level package directory, the repository name and the README heading. The lower-case
underscore form is what the project uses in its own packaging, documentation and repository naming;
it is not normalized to "MAVEN IUVS" or
"MAVEN/IUVS", because those name the mission and instrument, not the package.

Historical note worth keeping for discovery: this package was called **PyUVS** until commit
`8c4d45f` (2020-12-22, "Renamed module from PyUVS to maven_iuvs."). A stale
`include PyUVS/ancillary/*` line survives in `MANIFEST.in`, and `download.py` still names local
variables `pyuvs_path`. PyUVS is therefore a *former name of this same software*, not separate
software, and must not be recorded as Related Software.

### 8. Description (MANDATORY)

> maven_iuvs is a Python library of analysis routines for data from the Imaging Ultraviolet
> Spectrograph (IUVS) aboard NASA's Mars Atmosphere and Volatile EvolutioN (MAVEN) orbiter,
> developed by the IUVS instrument team at the Laboratory for Atmospheric and Space Physics,
> University of Colorado Boulder. It reads and manipulates IUVS level 1A and level 1B FITS files,
> synchronizes data and SPICE kernels from the MAVEN Science Data Center and the IUVS team server,
> and maintains searchable indexes of local mission data holdings. Calibration routines convert raw
> detector counts to physical brightness units using the instrument's effective area, microchannel
> plate gain curve, flat fields and line-spread function, and cleaning routines remove darks, cosmic
> rays, hot pixels and corrupt frames. For echelle observations the package forward-fits the
> hydrogen and deuterium Lyman-alpha lines, optionally including an interplanetary hydrogen
> component, using nested-sampling or least-squares fitters, and drives generation of level 1C data
> products. Geometry routines built on SPICE provide pixel viewing vectors; solar zenith, emission,
> phase and local-time angles; sub-solar and sub-spacecraft points; transforms between the IAU_MARS
> and MAVEN_MSO reference frames; and Mars solar longitude and mission timekeeping utilities.
> Plotting routines produce quicklook figures, detector images, spectral line-fit plots,
> map-projected swaths of the Martian disk, and three-dimensional renderings of Mars and the MAVEN
> orbit. Operational tooling supports pipeline orchestration, weekly observation reports,
> reprocessing comparisons, and the preparation and verification of Planetary Data System
> deliveries. The package assumes access to local IUVS data holdings and SPICE kernels configured
> through a user paths file; some routines additionally require the IUVS team's IDL pipeline.

**This replaces the description that was previously stored.** That value was the README's text,
preserved here in full so nothing is lost and the change remains reversible:

> maven_iuvs is the place where all cool cats and kittens go to contribute Python routines for IUVS
> science. :smiley_cat: :sunglasses:
> It provides:
> * Tools for reading and manipulating IUVS data
> * Standardized projections of IUVS data
> * Integration with spiceyPy
> * ... and much much more
>
> We appreciate contributions from people of all backgrounds. Even if you do not plan to contribute
> code, raising issues of bugs, unexpected behavior, and suggestions for improvement would all be
> valuable.

Why the README text was replaced rather than deferred to as the maintainers' own wording:

- HSSI uses the first 150-200 characters as the search-result preview. The README text's preview
  read "maven_iuvs is the place where all cool cats and kittens go to contribute Python routines for
  IUVS science. :smiley_cat: :sunglasses: It provides: * Tools for reading...", which tells a
  scientist browsing HSSI almost nothing about what the software can do for them.
- `:smiley_cat:` and `:sunglasses:` are GitHub emoji shortcodes. GitHub renders them as pictures;
  HSSI stores and displays them as the literal text shown above.
- The Markdown bullet markers and the ellipsis item "... and much much more" are list markup
  flattened into a paragraph.
- The closing paragraph solicits contributions. That is appropriate in a README and out of place in
  a catalogue description, which the form specifies should tell a potential user "what the software
  does, why to use it, assumptions it makes."
- The form additionally asks for "proper capitalization, grammar, and punctuation."

The replacement preserves the three capabilities the README itself highlights — reading and
manipulating IUVS data, standardized projections, and spiceypy integration — and expands them with
capabilities established by direct code reading (see Field 4). The closing sentence records the
software's operating assumptions, which the form explicitly asks for and the original omits. The
README text above is preserved as the exact value to restore should the maintainers' own voice ever
be preferred to a catalogue description.

### 9. Concise Description (OPTIONAL)
Python analysis library for MAVEN/IUVS ultraviolet spectrograph data: reading, calibration, dark and artifact removal, Lyman-alpha line fitting, SPICE geometry, map projection, and quicklook plots.

197 characters, within the 200-character limit. This field was previously empty, which meant the
search-result preview fell back to the first ~200 characters of the description — the "cool cats and
kittens" sentence discussed in Field 8. A purpose-written concise description fixes that preview
independently of whatever the description in Field 8 says.

### 10. Publication Date (RECOMMENDED)
2019-04-08

Carried over from the existing HSSI record and confirmed: the GitHub API reports
`created_at = 2019-04-08T22:06:09Z` for `lasp/maven_iuvs`, which is also what SoMEF reports as
`date_created`, and the repository's root commit carries exactly that timestamp: `git rev-list
--max-parents=0 HEAD` returns `2a1b844` alone, authored by Josh Elliott at 2019-04-08 16:06:09 -0600.
There is no release or DOI that would supply a better date.

A point of confusion worth disarming, because it is easy to reach the wrong conclusion from a
one-line `git log`: `237f355e` (Kyle Connour, 2019-04-09) is *also* titled "Initial commit" and is
the commit that first added substantive code, but it is the third commit in the history, not the
root.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

This field was empty. The form's instruction is explicit: "For software where a DOI has been
obtained through Zenodo ... Zenodo is the correct entry. If no DOI has been obtained, indicate the
repository host, such as GitHub or GitLab." No DOI exists (Field 2), so the repository host is the
correct entry.

Considered and rejected: **Laboratory for Atmospheric and Space Physics** (or University of Colorado
Boulder) as the institutional publisher. It is the developing institution and is already recorded on
every author's affiliation; the form reserves this field for the publication venue, which absent a
DOI is the repository host. A ROR was searched for GitHub and none exists, so the identifier is the
service URL, which the form permits ("ROR identifier when available ... or URL otherwise").

### 12. Version (RECOMMENDED)
- **Version Number:** 0.1.0
- **Version Date:** Not found
- **Version Description:** Not found
- **Version PID:** Not found

**What was previously stored, and why it was wrong.** The version entry attached to this record was
entirely empty: no number, no release date, no description, no version PID. It conveyed nothing about
the software and left the record looking unversioned.

**A view-layer rendering trap.** HSSI's view layer renders a version through a
`<software> - <number>` template, so the empty entry appeared there as `"maven_iuvs - "`, and the
recorded version appears there as `"maven_iuvs - 0.1.0"`. Those are rendered display strings, **not
stored values** — the stored version number is the bare `0.1.0`. The rendered form must never be read
back as the version.

**How 0.1.0 was chosen.** Every candidate source was checked:

- *Git tags* — none. `git tag` is empty in the clone and the GitHub tags API returns an empty list.
- *GitHub releases* — none; the releases API returns an empty list.
- *PyPI* — not published. Both `https://pypi.org/pypi/maven_iuvs/json` and the hyphenated form
  return HTTP 404.
- *Zenodo / DataCite* — no record; a DataCite query for `"maven_iuvs"` returns zero results, so
  there is no version DOI.
- *CHANGELOG* — the repository has none.
- *In-tree declaration* — `setup.py` line 6 declares `version='0.1.0'`. No module defines
  `__version__`; the other `version`-named identifiers in the source are an rsync version probe in
  `download.py` and IUVS *data* product versions in `echelle.py` and `search.py`. So `setup.py` is
  the authoritative version statement the project makes about itself, and it is what
  `pip install -e .` records, so it is what a user's environment will report.

`0.1.0` is therefore recorded, with the explicit caveat that it is an **untagged in-tree
declaration, not a release**. It was introduced on 2020-12-15 by Zachariah Milby (commit `cd54ca0`,
"Initial updates to structure, documentation") and has never been changed, despite continuous
development through the extraction revision of 2026-06-22.

**Version Date is deliberately left empty.** The only date associable with `0.1.0` is 2020-12-15,
the day the string was first written into `setup.py`. Recording that as a release date would tell an
HSSI user that this software dates from 2020, when in fact more than five years of development
followed without a version bump. Absent a real release there is no honest release date; the
2020-12-15 date is preserved in this note so a future agent has it if a release date is ever
warranted.

**A trap for a future agent.** The strings `v13`, `v14` and `v15` appear throughout `echelle.py`,
`RUN_ECHELLE_v15_PIPELINE.py`, the ancillary LSF files and the master light/dark key filenames.
These are **IUVS data calibration versions**, selected by the `calibration=` keyword and governing
which LSF, binning table and conversion factors are used. They are not software versions and must
not be recorded in this field.

### 13. Programming Language (RECOMMENDED)
Python 3.x

Carried over from the existing HSSI record and confirmed: the GitHub languages API lists Python as
the sole language it detects for this repository, SoMEF likewise reports Python, and `setup.py`
declares `python_requires='>=3.7'`.

Considered and rejected: **IDL**. `echelle.py` opens an `idl` subprocess and compiles/runs
`write_l1c_file_from_python.pro` to write out L1C files, and several ancillary files are IDL save
files (`lsf_new.idl`, `ech_light_dark_fnames_Mayyasi_20230223.sav`, read with
`scipy.io.idl.readsav`). But no IDL *source* is in this repository — the `.idl` file is data despite
its extension, and the `.pro` script lives in the team's separate IDL pipeline directory. This field
asks for "the computer programming languages most important for the software," meaning the
software's own implementation language, which is Python only.

### 14. Reference Publication (RECOMMENDED)
Not found.

There is no publication that describes this software. Searched: the README (no citation section, no
"how to cite"), the absent CITATION.cff, code comments, and DataCite (zero records for
`"maven_iuvs"`).

Candidates examined and rejected, with their DOIs recorded so a future agent need not re-find them:

- **McClintock et al. (2015), "The Imaging Ultraviolet Spectrograph (IUVS) for the MAVEN Mission,"
  Space Science Reviews, https://doi.org/10.1007/s11214-014-0098-7** — the IUVS instrument paper. It
  describes the hardware this software analyses data from, not the software. Listing it here would
  misrepresent it as the software's reference publication.
- **Mayyasi et al. (2023), https://doi.org/10.1029/2022EA002602** — describes the MAVEN echelle data
  reduction pipeline, but the earlier Boston University / IDL implementation, which this Python code
  treats as an *alternative* to compare against (see Field 27). It predates
  `echelle.convert_l1a_to_l1c` and does not describe this package. It is recorded under Related
  Publications instead.

### 15. License (RECOMMENDED)
- **License:** Not found
- **License URI:** Not found

**The current source tree carries no licence grant.** No `LICENSE`, `LICENSE.txt`, `LICENCE`,
`COPYING` or `NOTICE` file is tracked (`git ls-files` matched none); `setup.py` passes no `license=`
argument and no `classifiers`; the README says nothing about licensing; `MANIFEST.in` ships nothing
licence-related; and the GitHub API reports `"license": null` for `lasp/maven_iuvs`. A `git grep` of
the tracked tree for `bsd`, `licen[sc]e` and `copyright` surfaces no licence statement in any source
file — the only text hits are `np.linalg.slogdet(covmat).logabsdet` in `echelle.py` and
`graphics/echelle_graphics.py`, where the letters "bsd" fall inside `logabsdet`.

**But the project was licensed at founding, and the licence was later removed.** This history is the
substance of this field and is recorded so a future agent does not re-derive it, and does not read
the empty value as "licensing was never addressed":

- The repository's root commit `2a1b8449d79106a4cfc35be6af802938cade7cd6` (Josh Elliott, "Initial
  commit", 2019-04-08) contains a complete 29-line `LICENSE` file: a **BSD 3-Clause License**,
  `Copyright (c) 2019, Laboratory for Atmospheric and Space Physics`, with all three standard
  clauses (retain the copyright notice in source, reproduce it in binary distributions, no
  endorsement using the copyright holder's or contributors' names) and the standard
  "AS IS" warranty disclaimer. Retrieve it with `git show 2a1b844:LICENSE`.
- `git log --all --follow -- LICENSE` returns exactly two commits over the repository's whole
  history: `2a1b844`, which added the file, and `cd54ca0`, which deleted it.
- `cd54ca0` is Zachariah Milby's "Initial updates to structure, documentation" (2020-12-15). Its
  diffstat shows `LICENSE | 29 -` among 43 changed files, 19 of which are paths under a new
  `PyUVS/` package directory — some moved there from the repository root, some newly added (a
  further 9 are generated documentation under `doc/html/PyUVS/`). The
  commit message is a one-line summary about structure and documentation with an empty body, and
  **nothing in the commit indicates that removing the licence was deliberate** — no substitute
  licence, no relicensing note, no discussion. It reads as fallout of the restructuring, but that is
  an inference about appearance, not a determination of intent.
  (This is the same commit cited in Fields 6 and 12 as the one that introduced `version='0.1.0'`;
  a week later `8c4d45f` renamed `PyUVS` to `maven_iuvs`.)
- No commit since has restored or replaced it: `git log --all --diff-filter=A -- LICENSE` returns
  only the root commit.

**Why the field is nevertheless left empty.** HSSI describes the software as it stands at the
recorded source revision, and at that revision the distributed tree grants no licence. Asserting
BSD-3-Clause would state a grant that a user cloning the repository today does not actually receive.
Confirming whether LASP considers BSD-3-Clause still operative is a question for the maintainers, not
something this file can settle.

**If that confirmation is obtained, everything needed is here.** The value to record would be the
live `License` row `BSD 3-Clause "New" or "Revised" License` (copied exactly, including the straight
double quotes around `New`), with License URI `https://spdx.org/licenses/BSD-3-Clause.html`, which is
the URI carried by that row.

**Durable upstream follow-up worth reporting to the LASP maintainers.** A licence removed without
replacement is a real reuse blocker, not a cosmetic gap: by default a public repository with no
licence grants no redistribution or modification rights, so downstream users, packagers and archives
have no clear basis to redistribute or build on this code even though a permissive BSD grant was in
place at founding. Restoring `LICENSE` at the repository root would resolve it, and this dossier's
Field 15 value could then be filled from the paragraph above.

Considered and rejected as values: selecting **`Other`** from the controlled vocabulary. `Other`
asserts that a licence exists but is absent from HSSI's list; here the current tree grants none at
all, so `Other` would state something false — and it would also obscure the specific and recoverable
BSD-3-Clause history above. **`Restricted`** was rejected because the repository is publicly readable
and the form reserves that value for software whose access is restricted.
**`BSD 3-Clause "New" or "Revised" License`** was considered and not selected for the reason given
above — it is a historical grant that the current tree does not carry, and recording it would require
the maintainer confirmation this file cannot supply.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- mars
- maven
- iuvs
- ultraviolet
- spectroscopy
- imaging spectroscopy
- spectrograph
- echelle
- lyman alpha
- hydrogen
- deuterium
- aeronomy
- airglow
- corona
- upper atmosphere
- thermosphere
- planetary science
- remote sensing
- calibration
- data reduction
- spice
- geometry
- fits
- python

This field was previously empty. Keywords is the form's one open vocabulary
(`_get_or_create_keyword` mints missing rows), so each term was matched against the existing
`Keyword` rows first, to reuse a shared row rather than mint a near-duplicate. These terms already
existed as rows at extraction time and are reused as-is: `mars`, `maven`, `ultraviolet`,
`spectroscopy`, `imaging spectroscopy`, `spectrograph`, `aeronomy`, `airglow`, `corona`,
`upper atmosphere`, `thermosphere`, `planetary science`, `remote sensing`, `calibration`,
`data reduction`, `spice`, `geometry`, `fits`, `python`. Five terms had no existing row — `iuvs`,
`echelle`, `lyman alpha`, `hydrogen`, `deuterium` — and are recorded as new terms because each is
central to this software and none of the five is a variant spelling of a row that already existed.

Term-by-term basis: `mars`, `maven` and `iuvs` are the target, mission and instrument; `ultraviolet`,
`spectroscopy`, `imaging spectroscopy` and `spectrograph` describe the measurement; `echelle` is the
observing mode that `echelle.py` (4,539 lines, the largest module) exists to process; `lyman alpha`,
`hydrogen` and `deuterium` are the emissions the fitting code retrieves (`fit_H_and_D`,
`constants.D_offset`, `constants.Lya_lab`); `aeronomy`, `airglow`, `upper atmosphere`, `thermosphere`
and `corona` carry the science regions the Region vocabulary cannot express (see Field 5), and are
supported by the NO nightglow, CO2+ and CO emission colormaps in `graphics.py` as well as the
hydrogen-corona focus of the echelle work; `planetary science` and `remote sensing` place the
software; `calibration`, `data reduction`, `spice`, `geometry` and `fits` name its principal
technical capabilities; `python` its implementation.

Considered and rejected: `planetary magnetospheres` (an existing row, but it duplicates Field 5 and
this software is not a magnetospheric tool) and `spiceypy` (an existing row, but the dependency is
already expressed precisely in Field 30).

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific
- HTTP/HTTPS Directories

This field was previously empty.

`Observatory/Mission-specific` is the primary and correct value: all science input comes from
MAVEN-specific holdings — IUVS L1A/L1B FITS and MAVEN SPICE kernels rsynced from the IUVS team
virtual machine (`download.call_rsync`, `download.get_vm_file_list`, `download.sync_data`), and EUVM
L2B files from the MAVEN Science Data Center. Field 17's own instruction ("If observatory-specific,
select 'observatory-specific' and indicate the observatory/mission name in the Related Observatory
field") is satisfied by the MAVEN entry in Field 32.

`HTTP/HTTPS Directories` is supported concretely: `download.sync_euvm_l2b` logs into
`https://lasp.colorado.edu/maven/sdc/team/data/sci/euv/l2b/` with `twill`, enumerates the `.sav`
links in that directory listing, and downloads the most recent one;
`download.sync_integrated_reports` does the same against
`https://lasp.colorado.edu/ops/maven/team/inst_ops.php?content=msa_ir&show_all`.

Considered and rejected: **`FTP/FTPS Directories`** — the bulk transfer is `rsync` over SSH
(`pexpect.spawn` of an `rsync -trvzL` command, with `sysrsync` and `fabric` in the dependency list),
not FTP. **`S3/Cloud-aware`** — `ancillary/MASTER_LIGHT_DARK_KEY_v14_AWS.csv` records AWS-style file
*names* used elsewhere in the team's workflow, but no code in this repository talks to S3 or any
cloud API. **`CDAWeb`, `HAPI`, `SSCWeb`, `OMNIWeb`, `AMDA`, `Madrigal`, `VirES`, `das2`, `TAP`,
`GFZ`, `WDC`, `The Virtual Solar Observatory.`** — no client for any of these exists in the code.
**`Other`** was considered for the rsync-over-SSH transport and dropped as adding no information
beyond `Observatory/Mission-specific`.

### 18. Input File Formats (RECOMMENDED)
- FITS
- IDL.sav
- HDF5
- csv
- ascii
- Other

This field was empty. Evidence per value:

- **FITS** — the core input. `astropy.io.fits.open` is used throughout (`echelle.py`,
  `graphics/echelle_graphics.py`, `integration.py`, the pipeline drivers), and
  `file_classes.IUVSFITS` subclasses `astropy.io.fits.hdu.hdulist.HDUList` to read IUVS L1A/L1B
  `.fits.gz` files, with named extensions `Primary`, `Integration`, `Binning`, `PixelGeometry` and
  `SpacecraftGeometry`.
- **IDL.sav** — `scipy.io.idl.readsav` reads three distinct inputs: the EUVM L2B orbit-averaged save
  file (`search.get_solar_lyman_alpha`), the v14 line-spread function (`echelle.load_lsf`,
  `lsf_new.idl`), and the legacy Mayyasi light/dark filename key
  (`ech_light_dark_fnames_Mayyasi_20230223.sav`).
- **HDF5** — `instrument.calculate_calibration_curve` opens `ancillary/iuvs_effective_area.h5` with
  `h5py.File` to obtain the instrument sensitivity curve.
- **csv** — `pandas.read_csv` reads the master light/dark key files
  (`ancillary/MASTER_LIGHT_DARK_KEY_v13/v14/v14_AWS.csv`), the PDS delivery target lists
  (`pds.verify_pds_completion`), and the light/dark pair lists consumed by the pipeline drivers.
- **ascii** — `astropy.io.ascii.read` parses the PDS file list in
  `reprocessing.compare_PDS_with_reprocess`; `reprocessing.get_all_errors` reads plain-text pipeline
  log files; `download.sync_integrated_reports` retrieves `.txt` integrated reports.
- **Other** — NumPy `.npy` files are a first-class input: the file metadata index
  (`echelle.get_dir_metadata`, `np.load(..., allow_pickle=True)`), the v15 LSF (`lsf_v15.npy`), the
  cruise LSF, the flat-field polynomial, the MUV contamination templates, and the Mars-year boundary
  ephemeris table. JPEG Mars surface maps are also read (`plt.imread` in
  `geometry.highres_swath_geometry`; `tvtk.JPEGReader` in `maven_orbit_image`). Neither `.npy` nor
  JPEG has a row in the `FileFormat` vocabulary, so `Other` is the correct representation.

Considered and rejected: **CDF**, **netCDF3/4**, **JSON**, **Zarr** — no reader for any of them
appears in the code. **ISTP-Compliant** — IUVS FITS files follow the MAVEN/PDS4 conventions, not the
ISTP CDF metadata standard.

### 19. Output File Formats (RECOMMENDED)
- FITS
- csv
- Other

This field was empty. Evidence per value:

- **csv** — the most direct output. `echelle.prep_output_and_writeout` writes brightness and
  line-center, photons-per-second, and all-fits tables to CSV; `convert_l1a_to_l1c` with
  `save_arrays=True` writes per-integration data and fit-parameter CSVs; `pds.make_pds_csv` writes
  the per-delivery key; `echelle.make_light_and_dark_pair_CSV`, `add_new_files_to_light_dark_key` and
  `update_filenames_in_light_dark_key` write and back up the master light/dark key CSVs.
- **FITS** — the pipeline's science product is an L1C `.fits.gz` file. Recorded with an explicit
  nuance: the byte-level write is performed by the IUVS team's IDL routine
  `write_l1c_file_from_python.pro`, which this package starts as a subprocess, compiles and drives
  (`echelle.open_idl_and_compile_writel1c_script`, `command_IDL_and_verify_done`,
  `prep_output_and_writeout`, whose docstring states its return as "an l1c .fits.gz file, written out
  from IDL"). Generating that L1C FITS product is the declared purpose of `convert_l1a_to_l1c` and of
  both pipeline driver scripts, so FITS is a genuine output format of this software even though the
  final serialization is delegated. `pds.verify_pds_completion` then checks those L1C FITS files and
  their XML labels for a PDS delivery.
- **Other** — figures written with `plt.savefig` (quicklooks, line-fit plots, comparison plots) and
  NumPy `.npy` artifacts written with `np.save` (the file metadata index in
  `echelle.update_metadata_file`, the synced filename index in `download.sync_data`, the Mars-year
  boundary table in `time.generate_marsyear_boundaries_file`). Neither PNG/PDF nor `.npy` has a row
  in the `FileFormat` vocabulary.

Considered and rejected: **ascii** — the package writes plain-text log files (`IDLerrors.txt`,
`IDLoutput.txt`, missing-lights logs) and temporary `np.savetxt` file lists for rsync, but these are
operational plumbing rather than a data output format offered to users. **IDL.sav** — IDL save files
are read, never written. **HDF5**, **CDF**, **netCDF3/4**, **JSON**, **Zarr**, **ISTP-Compliant** —
no writer exists.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac

This field was empty. There is no CI matrix, no `classifiers` in `setup.py` and no installation notes
beyond `pip install -e .`, so the values are inferred from hard platform dependencies in the code,
which are unambiguous:

- `download.call_rsync` uses `pexpect.spawn(...)` to drive an interactive `rsync` command and answer
  its SSH password prompt. `pexpect`'s `spawn` class is POSIX-only and is not available on Windows.
- The same function shells out to `rsync` and raises "is rsync installed on your system?" if it is
  absent; `sysrsync` is a declared dependency.
- `echelle.open_idl_and_compile_writel1c_script` launches
  `subprocess.Popen(["stdbuf", "-oL", "-eL", "idl", "-quiet"])`. `stdbuf` is a GNU coreutils utility.
- `make_documentation.py` calls `os.system('rm -r ...')` and `os.system('mv -f ...')`.

**Windows is therefore not listed**, and this is a positive finding rather than an omission: the
data-sync path cannot run there at all. `Linux` and `Mac` are both listed because the science and
plotting paths (FITS reading, calibration, fitting, geometry, plotting) are pure Python over
cross-platform dependencies, and the developers' commit addresses and workflow are LASP
Linux/macOS. One caveat a future agent should know: `stdbuf` is not present on a stock macOS
install, so the IDL-driven L1C writeout step specifically requires GNU coreutils there; the rest of
the package is unaffected.

Considered and rejected: **`Operating System Independent`** — contradicted by the POSIX-only
dependencies above. (Note also that `OS Independent` is not a value in this vocabulary; the
spelled-out form is the only cross-platform row.) **`Solaris`**, **`MobilePlatform`**, **`Other`** —
no evidence.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64

This field was empty. The package itself is pure Python with no compiled extensions of its own, so
the practical constraint comes from its declared dependencies rather than from its own code:
`mayavi>=4.7.2` and `PyQt5>=5.15.2` (VTK/Qt binaries), `jax>0.5.0`, `h5py`, `scipy`, `scikit-image`,
`cartopy`. `x86-64` and `Apple Silicon arm64` are the architectures for which that whole stack is
routinely available as wheels, and they match the LASP development environment.

Considered and rejected: **`CPU Independent`** — attractive because the package contains no compiled
code, but it would overstate installability, since a user cannot run the 3D orbit imagery or the
JAX-accelerated likelihood without architecture-specific binaries. **`Linux aarch64 or arm64`** —
plausible for the science paths but not asserted, because Mayavi/VTK and PyQt5 wheel coverage there
is thin and nothing in the repository demonstrates it. **`GPU`** — `jax` is used for just-in-time
compilation of `lineshape_model` and `(neg)loglikelihood` (commit `e681028`), not for GPU execution;
no CUDA or ROCm code or configuration exists. **`HPC or HEC`** — the `multiprocessing` pool in
`RUN_ECHELLE_v15_PIPELINE.py` is single-machine parallelism, with no MPI or scheduler integration.
**`Sun (SPARC)`**, **`ppc64le`**, **`Other`** — no evidence.

### 22. Related Phenomena (OPTIONAL)
Not found.

This field is empty, and correctly so. `Phenomena` is a **closed** vocabulary, and at this
extraction its rows were the seven values `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and `X-ray emission` — each of
them a solar or geospace phenomenon. This software
supports Martian ultraviolet airglow and nightglow, the hydrogen and deuterium coronae, atmospheric
escape, and interplanetary hydrogen — none of which has a row. The API path rejects unknown values
(`_get_graph_list_item` raises `Unknown value`), so a free-text phenomenon cannot be added here.

The phenomena this software does support are carried in Keywords (Field 16), which is the open
vocabulary the field definition directs such terms to: `airglow`, `corona`, `lyman alpha`,
`hydrogen`, `deuterium`, `aeronomy`.

### 23. Development Status (RECOMMENDED)
Active

This field was empty. `Active` ("Reached stable, usable state and being actively developed") is
supported by sustained recent development: the extraction revision is dated 2026-06-22, with
substantive 2025-2026 work including a new v15 line-spread function, migration from `pkg_resources`
to `importlib_resources`, and the JAX just-in-time transition of the likelihood functions. The
repository carries open issues and forks and merges pull requests; the extraction revision is itself
a merge commit.

Considered and rejected: **`WIP`** — defensible on the literal `version='0.1.0'` and the absence of
any tagged release, but contradicted by seven years of production use generating official MAVEN IUVS
L1C data products delivered to the PDS. The repostatus.org definition of WIP is "no stable, usable
public release yet," and this software demonstrably has a stable, used state; the missing version tag
is a packaging omission, not a maturity signal. **`Inactive`**, **`Unsupported`**, **`Abandoned`**,
**`Suspended`**, **`Moved`** — all contradicted by the commit history.

### 24. Documentation (RECOMMENDED)
https://lasp.github.io/maven_iuvs/

Carried over from the existing HSSI record and re-verified: the URL returns HTTP 200 and serves
pdoc-generated API documentation (generator meta tag "pdoc 0.9.2", title "maven_iuvs API
documentation"). The in-repo `docs/` directory holds the generated HTML that backs this site, and
`make_documentation.py` regenerates it with `pdoc --html`.

A caveat worth recording: this is auto-generated API reference only. There is no narrative user
guide, tutorial or installation documentation beyond the two-sentence `pip install -e .` note in the
README, and the published site is regenerated manually rather than by CI, so it can lag the `master`
branch. SoMEF proposed `https://github.com/lasp/maven_iuvs/tree/master/docs` instead; the rendered
GitHub Pages URL is the better value because it is the human-readable form of the same content.

### 25. Funder (OPTIONAL)
Not found.

Negative research: a sweep of the package source, the README and `setup.py` for `fund`, `grant`,
`award`, `acknowledg`, `sponsor` and the NASA grant-number prefixes `NNX`, `NNH` and `80NSSC`
returned nothing, and there is no DOI record whose `fundingReferences` could supply one.

**Considered and not recorded: the National Aeronautics and Space Administration**
(ROR https://ror.org/027ka1x80). The inference is an obvious one — MAVEN is a NASA Mars Scout
mission, IUVS is a NASA-funded instrument, and this is the IUVS instrument team's analysis software
developed at LASP — but the funding relationship runs to the mission and the instrument, not
demonstrably to this software, and nothing in or about the repository states a funder. The field is
left empty rather than asserting an unevidenced value. The ROR is recorded here so that a future
agent who does find a direct funding statement can fill the field without re-researching the
identifier.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

Negative research: no grant number, contract number, or award title appears anywhere in the
repository, and there is no DOI record to draw one from.

**A placeholder award was previously associated with this record** — an award entry whose title,
identifier and funder were all empty, which surfaced in the rendered view as an award list containing
an empty string. It carried no information about any real award and is not part of this record's
metadata. The field is empty because no award evidence exists, not because an empty placeholder
stands in for one.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2022EA002602
- https://doi.org/10.1002/2016JA023466

This field was empty. Both entries are named directly by the code:

- **Mayyasi et al. (2023), "Upgrades to the MAVEN Echelle Data Reduction Pipeline: New Calibration
  Standard and Improved Faint Emission Detection Algorithm at Lyman-alpha," Earth and Space
  Science.** `echelle.convert_l1a_to_l1c` exposes `do_BU_background_comparison`, documented as
  "whether to include an alternate fit using a background as per Mayyasi+2023," and `fit_flat_data`
  accepts a `BU_bg` array implementing that method (`make_BU_background`,
  `plot_line_fit_comparison`). The repository also ships
  `ancillary/ech_light_dark_fnames_Mayyasi_20230223.sav`, the light/dark filename key from that
  work. This paper describes the predecessor echelle pipeline whose algorithm this software
  implements as a comparison baseline and supersedes.
- **Mayyasi et al. (2017), "IUVS echelle-mode observations of interplanetary hydrogen: Standard for
  calibration and reference for cavity variations between Earth and Mars during MAVEN cruise," JGR
  Space Physics.** `echelle.get_conversion_factors` hard-codes
  `Ph_pers_perkR = 29.8 # Average calibration factor WRT SWAN (Mayyasi+ 2017)`; that paper is the
  source of the SWAN-referenced calibration standard the software applies.

**A caveat about the field's scope, recorded so the choice is understood rather than second-guessed.**
Field 27's narrow "How to fill it" text says "Enter DOIs for all publications the software is cited
in," and neither of these cites this software — the relation runs the other way: the software
implements methods and constants from them. The field's broader "What it is" text ("Publications that
describe, cite, or use the software that the software developer prioritizes") admits them, and they
are the most useful literature pointers HSSI can give a user of this software's data products. They
are recorded on that broader reading; the strict reading would leave the field empty, and that
trade-off was made knowingly.

Considered and rejected: **McClintock et al. (2015), https://doi.org/10.1007/s11214-014-0098-7** —
the IUVS instrument paper. It is the right citation for the *instrument*, which is already linked
through Field 31, and adding it here would blur software-related literature with hardware
literature. The DOI is recorded so this decision does not have to be researched again.

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.17189/1518929
- https://doi.org/10.17189/1518946
- https://doi.org/10.17189/1518964

This field was empty. All three are NASA Planetary Data System bundle DOIs for MAVEN IUVS, confirmed
through DataCite:

- **10.17189/1518929** — "Mars Atmosphere and Volatile Evolution (MAVEN) Imaging Ultraviolet
  Spectrograph (IUVS) Raw-level Data Product Bundle." The PDS description of the Raw bundle is
  "DN/bin + engineering and geometric data," which is the level 1A product this software reads:
  `download.sync_data(level='l1a')`, `user_paths.l1a_dir`, and `echelle.convert_l1a_to_l1c` operate
  directly on it.
- **10.17189/1518946** — "...Calibrated-level Data Product Bundle." The PDS description is
  "Calibrated instrument readouts in kr/nm and ancillary data," i.e. level 1B, which
  `download.sync_data(level='l1b')`, `integration.fit_line`, `graphics.latlon_meshgrid` (documented
  as taking an "Opened level 1B FITS file") and much of `geometry.py` consume.
- **10.17189/1518964** — "...Processed-level Data Product Bundle." The PDS description is "calibrated
  brightness including isolating emission features and spatial binning," which is what
  `echelle.convert_l1a_to_l1c` produces (H and D brightnesses isolated by line fitting, on the binned
  spatial grid) and what `pds.verify_pds_completion` audits before a numbered PDS delivery. This is
  an inference from the bundle description rather than a quoted level mapping — the PDS page names
  the bundles Raw/Calibrated/Processed/Derived without spelling out l1a/l1b/l1c — but the description
  match is close and the software's PDS delivery tooling targets L1C files.

Considered and rejected: the **Derived-level** bundle (10.17189/1518956, "column abundance, density
profiles, and maps") and the **Key Parameter** bundle (10.17189/1518955) — this software neither
reads nor produces those products. The **MAVEN Remote Sensing (IUVS) Data Return Files** collections
(10.17189/1517677, 10.17189/1414188) are instrument housekeeping deliveries, not science data this
package touches.

### 29. Related Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.34140

**`michaelaye/iuvs`** — https://github.com/michaelaye/iuvs, by K.-Michael Aye, DOI
`https://doi.org/10.5281/zenodo.34140`. This field was previously empty, and of everything the
search documented below turned up, this is the one candidate that clears Field 29's gate ("software
that performs similar tasks but does not necessarily link together").

Evidence that it is a similar-purpose tool for the same instrument: its GitHub description is "Maven
IUVS reader and plot utilities" and its README calls it "a data processing and reader library for
data from the Maven IUVS UV spectrometer." Its module layout mirrors this package's concerns
closely — `io.py` (the reader, and its largest module), `calib.py`, `superdark.py` (dark-frame
handling), `scaling.py`, `plotting.py`, `apoapse.py` (an IUVS observing mode), `hk.py`
(housekeeping), `spice.py`, `profile_movie_plotter.py` — alongside an `idl/` directory, `tests/` and
`notebooks/`. It is independently citable: ISC-licensed, one tagged release `v0.1.0-beta`
(2015-11-23), and a Zenodo deposit that resolves from the README's badge.

**Why it is recorded.** It predates this package (created 2014-12-01, versus 2019-04-08 here),
is by a different author, and is not a fork parent — the two share no code — so what it tells an HSSI
reader is precisely the distinguishing fact Field 29 exists to convey: an earlier, independent Python
IUVS reader exists, and `maven_iuvs` is not descended from it. Field 29 carries no recency criterion,
and of the IUVS-specific counterparts this search turned up it is the one with a public repository,
a licence and a DOI — unlike the IUVS team's IDL pipeline below, which had to be omitted for want of
any identifier.

**Its staleness is recorded, and is not a reason to reject it.** `michaelaye/iuvs` is effectively
dead: last pushed 2015-11-23, the same day as its only release, and unmaintained since. That is
stated plainly rather than left implicit, so a future agent understands the entry was chosen
*despite* being abandoned rather than in ignorance of it. The judgement made here is that telling an
HSSI reader an earlier, independent Python IUVS reader exists is worth more than the entry's age
costs; dropping it would empty the field without adding any information in its place.

*Which identifier.* The Zenodo record (`10.5281/zenodo.34140`, "iuvs: First beta release",
K.-Michael Aye, 2015-11-23) carries no concept DOI — it predates Zenodo's concept-DOI mechanism — so
this version DOI is the identifier the project's own README badge resolves to, and it is used here.
The repository URL above is the practical link for a reader who wants the code.

The remainder of the Field 29 search is documented below. The full dependency list in `setup.py` was
evaluated against the same relevance gate — "distinguishing" software: similar-purpose tools, a
predecessor or fork parent, a companion package, or a domain-specific dependency whose presence
characterizes the software.

- **PyUVS is not a separate package.** `MANIFEST.in` still reads `include PyUVS/ancillary/*` and
  `download.py` uses `pyuvs_path` variable names, which look like a predecessor reference. Commit
  `8c4d45f` (2020-12-22) shows otherwise: "Renamed module from PyUVS to maven_iuvs." PyUVS is this
  software's own former name; listing it would be a self-reference.
- **`causaliteaa/PyUVS` on GitHub** ("This is the code I use to make the standard imaging products
  for the MAVEN/IUVS team," created 2024, owner Caroline E.) was examined because its name collides
  with this software's former name. It is not a fork of this repository, nothing in this repository
  references it, and it has no licence or DOI. Recorded so the name collision does not cause a future
  agent to infer a relationship that the evidence does not support.
- **The IUVS team's IDL pipeline** is a genuine companion: `echelle.py` starts `idl` as a subprocess,
  compiles `write_l1c_file_from_python.pro` from `user_paths.idl_pipeline_dir`, and depends on it for
  the final L1C serialization, while `reprocessing.py` compares this software's output against it. It
  cannot be recorded because it has no public repository, DOI or landing page — it lives on the
  team's internal systems, referenced only by a user-configured local path. Among the candidates
  that *cannot* be recorded for want of a public identifier, this is the one with a genuine claim to
  the field; its absence is a limitation of the counterpart's publication status rather than an
  oversight. It does not compete with `michaelaye/iuvs` above, which is recorded precisely because it
  does have a public repository, a licence and a DOI.
- **Rejected as generic infrastructure** (would be equally at home in a web application, a finance
  model or a biology pipeline, so listing them says nothing about this software): `numpy`, `scipy`,
  `pandas`, `matplotlib`, `cartopy`, `scikit-image`, `scikit-learn`, `statsmodels`, `shapely`,
  `h5py`, `tqdm`, `pytz`, `julian`, `idl_colorbars`, `mayavi`, `PyQt5`, `jax`, `dynesty`,
  `importlib_resources`, `pdoc3`, and the transport/automation stack `fabric`, `invoke`, `pexpect`,
  `sysrsync`, `twill`. `dynesty` deserves a specific note because it is astronomy-adjacent: it is a
  general-purpose nested-sampling Bayesian inference library, applicable to any likelihood problem,
  and its presence here characterizes the fitting method rather than the software's domain.
- **`MAVENSDC/Pydivide`** (https://github.com/MAVENSDC/Pydivide, DOI
  `https://doi.org/10.5281/zenodo.3601516`, MIT, developed at LASP, last pushed 2020-08-18) was
  examined and **not selected**. Its IUVS support is real and more substantial than its one-line
  description ("a plotting tool for MAVEN in-situ key parameter data") suggests: `download_files.py`
  exposes an `iuvs=True` download mode, `read.py` reads IUVS Key Parameter files, and `corona.py`,
  `periapse.py` and `occultation.py` are IUVS observing-mode plotting modules. It is nonetheless a
  different kind of tool: it operates on the mission's Key Parameter product through `pytplot`,
  spans MAVEN's instrument suite rather than IUVS specifically, and neither package references the
  other or shares a data model. It is complementary at a higher data level, not a similar-purpose
  tool for the detector-level processing this package performs. Recorded with its resolved DOI so a
  future agent taking a broader reading of Field 29 can promote it without re-researching it.
- **`pyspedas` and `PyRFU`** were considered because both advertise MAVEN support in the PyHC
  registry. Neither appears anywhere in this repository, and both load MAVEN particles-and-fields
  data rather than IUVS imaging spectroscopy, so they are not similar-purpose tools for this
  software.

### 30. Interoperable Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.593914
- https://github.com/astropy/astropy

**SpiceyPy** (`https://doi.org/10.5281/zenodo.593914`, SpiceyPy's Zenodo concept DOI) is carried over
from the existing HSSI record and confirmed as a correct entry. The README lists "Integration with
spiceyPy" as one of three headline capabilities, and the integration is concrete and bidirectional:
`spice.load_iuvs_spice` furnishes MAVEN CK, SPK, SCLK and IUVS kernels into the shared SPICE kernel
pool so that user code and this package share one geometry environment; `geometry.py`, `time.py` and
`graphics.py` exchange SPICE ephemeris times, frames and vectors with `spiceypy` throughout
(`spkezr`, `pxform`, `sincpt`, `subpnt`, `subslr`, `str2et`, `et2datetime`, `gfdist`, `lspcn`); and
`maven_orbit_image` documents "Call maven_iuvs.load_iuvs_spice() before calling this function." The
stored `RelatedItem` row for this entry has the placeholder name `UNKNOWN`; those names are not
user-visible and the DOI is the operative value, so the placeholder is not a reason to touch the
entry.

**Astropy** (`https://github.com/astropy/astropy`) is recorded, and it clears the Tier B "specific
documented exchange" bar rather than being a bare dependency: `file_classes.IUVSFITS` subclasses
`astropy.io.fits.hdu.hdulist.HDUList` and is documented as a "Wrapper around astropy HDUList with
convenience functions for IUVS data," so this package's primary data object *is* an astropy object;
and the public API's documented parameter and return type across `echelle.py`, `geometry.py`,
`binning.py`, `instrument.py` and `integration.py` is "astropy.io.fits instance" — for example
`integration.get_muv_contamination_templates` returns one. Astropy FITS objects are the interchange
currency in both directions, which is the documented-data-model criterion, not "uses astropy
internally." The repository URL is recorded rather than a DOI because Zenodo queries for the astropy
concept DOI did not return a reliable result at extraction time, and Field 30 explicitly permits a
repository link; a future agent may upgrade this to the concept DOI.

Considered and rejected under the Tier A / generic-infrastructure test: `numpy`, `scipy`, `pandas`,
`matplotlib`, `cartopy`, `tqdm`, `h5py`, `PyQt5`, `mayavi`, `jax`, `scikit-image`, `scikit-learn`,
`statsmodels`, `shapely`, `idl_colorbars`, `dynesty`, `fabric`, `invoke`, `pexpect`, `twill`,
`sysrsync`, `julian`, `pytz`, `importlib_resources`, `pdoc3`. Being in `install_requires` is not
interoperability. `h5py` was weighed as Tier B and rejected: it is used only to read one bundled
ancillary file (`iuvs_effective_area.h5`) inside `instrument.calculate_calibration_curve`, with no
HDF5 object crossing the public API.

The IDL bridge described in Field 29 is a genuine cross-language interoperation and is documented
there; it is not listed here because the counterpart pipeline has no public repository or DOI to
point at.

### 31. Related Instruments (OPTIONAL)

1. **MAVEN Imaging Ultraviolet Spectrograph, IUVS, Instrument**
   - Instrument Identifier: https://spase-metadata.org/SMWG/Instrument/MAVEN/IUVS
2. **MAVEN Langmuir Probe and Waves, LPW, Extreme Ultraviolet Monitor, EUV, Instrument**
   - Instrument Identifier: https://spase-metadata.org/SMWG/Instrument/MAVEN/LPW/EUV

Both names are the `InstrumentObservatory` vocabulary's own names for the corresponding instrument
rows, and both identifiers are `https://spase-metadata.org/` SPASE Resource IDs.

**IUVS** is carried over from the existing HSSI record. It is the instrument this software exists
for, so the relevance gate is met trivially.

*Identifier-form note, recorded so it is not rediscovered.* This instrument was previously recorded
as `MAVEN Imaging Ultraviolet Spectrograph (IUVS)` under
`https://spase-metadata.org/SMWG/Instrument/MAVEN/IUVS.html`. The `.html` form is not a registered
SPASE identifier — it was an artifact of a SPASE landing-page URL entering through the submission
path, and no `.html` identifier exists in the maintained upstream registry. The bare identifier
above is the registered, maintained form and is the durable half of the entry; the name is
upstream's own comma-styled display form. The `.html` variant should not be reintroduced.

**MAVEN LPW/EUV (the EUV Monitor, "EUVM")** is recorded. Evidence that the software is designed to
support it, not merely to mention it: `download.sync_euvm_l2b` is a dedicated function that
authenticates to the MAVEN SDC team site and downloads the latest EUVM L2B save file;
`download.get_euvm_l2b_dir` maintains a configured directory for it; `search.get_euvm_l2b_filename`
locates it; and `search.get_solar_lyman_alpha` parses that instrument's data structure
(`mvn_euv_l2_orbit`, its orbit times, Lyman-alpha channel and Mars-Sun distance) and interpolates it
to an IUVS observation time. That is direct, instrument-specific retrieval and parsing.

*Which row, and why.* Two rows in the vocabulary describe the same MAVEN EUV monitor:
`https://spase-metadata.org/SMWG/Instrument/MAVEN/LPW/EUV` (SMWG) and
`https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MAVEN/EUV` (the CNES/CDPP-AMDA catalogue
mirror, named "Extreme UltraViolet Monitor"). This is one entity with two candidate rows, so the SMWG
tie-breaker applies; and the repository's own evidence points the same way, since the data is fetched
from the MAVEN Science Data Center (`lasp.colorado.edu/maven/sdc/team/data/sci/euv/l2b/`), the
mission's NASA-side archive that the SMWG record describes, not from AMDA. On MAVEN the EUV Monitor
is a sensor of the Langmuir Probe and Waves package, which is why the SMWG name and identifier path
read `LPW/EUV`.

*Why a secondary instrument is listed, and how to read the association.* EUVM support here is real
but secondary — the solar Lyman-alpha value is an input used to interpret IUVS observations, and
nobody would choose this package as their EUVM analysis tool. It is recorded because the
"designed to support" test is met by dedicated download and parsing code for that instrument's
specific data product, and because a searcher looking for software that consumes EUVM L2B data should
find this record. The indirectness is stated so the entry is read as a data-input relationship, not
as a claim that this is an EUVM analysis package.

Considered and rejected:

- **SOHO/SWAN** — `echelle.py` cites SWAN twice, as the calibration standard behind the hard-coded
  factor `Ph_pers_perkR = 29.8` and in a docstring about "using SWAN instead of HST." The software
  applies a constant derived from SWAN observations; it never reads SWAN data. That is a literature
  reference, correctly captured by the Mayyasi et al. 2017 DOI in Field 27.
- **Hubble Space Telescope** — mentioned in the same docstring as the alternative calibration
  reference. Same reasoning.
- **Other MAVEN instruments** (NGIMS, SWIA, SWEA, STATIC, SEP, MAG) — a word-boundary sweep of the
  package source found no instrument references for any of them. One near-miss is worth naming so it
  is not re-investigated: `static` does occur in `echelle.py`, but as the `dynesty` sampler's
  `approach="static"` option, not the STATIC instrument. All six have SMWG rows, but this software
  does not touch their data.
- **The Mars surface map images** (`ancillary/marssurface_2.jpg`, `mars_surface_map.jpg`, used as
  textures in `maven_orbit_image` and `geometry.highres_swath_geometry`) carry no attribution in the
  code to a source instrument or mission, so no association can be defended from them.

### 32. Related Observatories (OPTIONAL)

1. **Mars Atmosphere and Volatile EvolutioN**
   - Observatory Identifier: https://spase-metadata.org/SMWG/Observatory/MAVEN

Carried over from the existing HSSI record, and correct: name and identifier match the live
vocabulary row of type 2, the identifier is a SPASE Resource ID, and the entire package is MAVEN
mission software. Field 17 records `Observatory/Mission-specific` as instructed for this pairing.

Considered and rejected: `Mars Atmosphere and Volatile Evolution Mission`
(`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/MAVEN`), the CNES/CDPP-AMDA catalogue mirror
of the same mission. One entity, two rows; the SMWG row already stored is the correct one, and the
two must not both be listed. No other observatory or mission is supported by this software — a
word-boundary sweep of the package source for Mars Express, MEX, TGO, NOMAD, MRO, MARCI, CRISM, EMM,
EMUS, Mars
Global Surveyor, MGS, Viking, Curiosity and MSL returned nothing.

### 33. Logo (OPTIONAL)
Not found.

Negative research: there is no logo image in the repository, no logo in the README, no PyHC registry
entry to supply one (see below), and SoMEF reported none.

One item could mislead a future agent: `Python Logo.pdf` sits at the repository root. It is the
Python language logo, not a logo for this software; nothing in the tracked files references it
(including `make_documentation.py`), so it appears to be a stray commit.

---

## Cross-cutting negative research

**PyHC registry.** All three registry files — `projects_core.yml`, `projects.yml` and
`projects_unevaluated.yml` — were checked in full at extraction time. `maven_iuvs` appears in none of
them, by name, by `code` repository URL, or by description. Absence from PyHC is not a defect; it
simply means no curated PyHC metadata exists for this software, so no PyHC-sourced keywords, logo or
documentation
URL could be applied. Two neighbouring facts worth recording: `pySPEDAS` and `PyRFU` both carry the
`maven` keyword in that registry, and `SpiceyPy` is a PyHC community package — but neither fact
creates a relationship for Fields 29/30 (see those fields).

**SoMEF.** Run against the repository URL at extraction time (v0.9.11, threshold 0.7). It returned
only what is already known from the GitHub API and the README: repository URL, owner `lasp`, creation
and update dates, name, `programming_languages: Python`, the README description excerpts,
`has_build_file: setup.py`, and `documentation: .../tree/master/docs`. It found no licence, no
version, no DOI, no authors and no logo, which independently corroborates the negative findings in
Fields 2, 12, 15 and 33. Its `application_domain: "Semantic web"` classification is wrong and was
discarded; SoMEF's domain classifier is known to be unreliable.

**No DOI-sourced metadata is available.** With no DOI (Field 2), neither DataCite nor Zenodo has
anything to say about this software. That is why the fields a DOI record would normally populate —
persistent identifier, publisher, license, funder, award, version PID — are either derived from other
evidence or recorded as absent.
