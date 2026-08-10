# HSSI Metadata Extraction Results

**HSSI Software ID:** c5b93d11-92e0-46cd-8616-427edce159d2
**Repository:** https://github.com/rjolitz/mavenpy
**Source Revision:** fb05d5202815a6713224de8ab33e98de22852e4c
**Extraction Date:** 2026-08-07
**Validation Date:** 2026-08-10
**Validation Status:** PASS

---

**Scope note — read this before weighing the evidence below.** MavenPy is not distributed through any
package index, carries no DOI, has no release history, and has no documentation site. Every value in
this dossier therefore rests on the repository's own source, its two reStructuredText documents
(`README.rst`, `UPDATE.rst`), the GitHub repository record, and external authority records (the ORCID
registry, the Research Organization Registry, the SPASE registry). Where a field is empty, that is
usually because the corresponding artifact does not exist rather than because it was not looked for;
those cases are recorded as documented omissions with the negative research that supports them.

A second point that changes how the code evidence should be read: **MavenPy supports different MAVEN
instruments at different depths.** Some instruments have the full chain (remote discovery → download →
local path resolution → file reader → science analysis); others have only retrieval and file-path
construction. `mavenpy/load.py` states the boundary in its own comment — it registers read functions
for EUV, MAG, SWIA, SWEA and SEP and notes it "Will NOT work for NGIMS, IUVS, and ROSE" (NGIMS has its
own dedicated reader in `mavenpy/ngims.py`). The support tiers are spelled out under Field 31, because
they are what justifies each instrument association.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The identity of the original submitter of the live HSSI record is not exposed by the metadata this
dossier was reconciled against, so no name is asserted here.

---

### 2. Persistent Identifier (RECOMMENDED)

**Not found.**

Negative research, so a future agent does not repeat it:

- There is no `CITATION.cff`, no `codemeta.json`, no `.zenodo.json` and no `AUTHORS` file in the
  repository at the pinned revision.
- `README.rst` contains no badges of any kind and no DOI.
- A Zenodo record search for `mavenpy` returns zero hits; a DataCite DOI search for `mavenpy` returns
  zero results. No concept DOI and no version DOI exist for this software.
- The GitHub repository has no releases and no tags, so no Zenodo–GitHub archival workflow has ever
  been triggered.

**PyPI name collision — a durable trap.** `https://pypi.org/project/mavenpy/` exists but is a
completely unrelated project: "Wrapper for calling Maven from Python" by Gabriel Konat
(`github.com/Gohla/mavenpy`, Apache 2.0, versions 0.1.0–0.1.5 released 2016–2021). It concerns the
Apache Maven Java build tool and has nothing to do with the MAVEN spacecraft. `rjolitz/mavenpy` is
**not** distributed on PyPI, and `setup.py` deliberately prevents it — lines 22–26 intersect
`sys.argv` with `frozenset(["register", "upload"])` and raise `ValueError` if either appears. **Do not
cite PyPI as a source for any MavenPy field**, and do not treat the PyPI project's version numbers,
license, author or release dates as evidence about this software.

---

### 3. Code Repository (MANDATORY)

`https://github.com/rjolitz/mavenpy`

Carried over unchanged from the existing HSSI record and independently confirmed: it is the local
clone's `origin` remote, the URL `README.rst` tells users to clone
(``git clone https://github.com/rjolitz/mavenpy.git``), and the GitHub API returns it as
`full_name: rjolitz/mavenpy` with default branch `main`, created 2024-07-15, last pushed 2026-04-02,
not archived.

**Rejected alternative — the stale Bitbucket URL.** `setup.py` line 56 declares
`url="https://bitbucket.org/rdjolitz/mavenpy"`. This predates the project's move to GitHub: the very
first commit is titled "Initial commit (from Bitbucket repo)". The packaging metadata was simply never
updated. The GitHub URL is authoritative for this field; the Bitbucket URL is recorded here only so a
future agent who encounters it in `setup.py` recognizes it as stale rather than as a competing value
to reconcile.

---

### 4. Software Functionality (MANDATORY)

Every subcategory listed has its parent top-level category listed alongside it, as the taxonomy
requires.

**Coordinate Transforms**
- Coordinate Transforms
- Coordinate Transforms: Mission-Specific
- Coordinate Transforms: Planetary

**Data Processing and Analysis**
- Data Processing and Analysis
- Data Processing and Analysis: 3D Particle Distribution Processing
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Pitch Angle Distributions
- Data Processing and Analysis: Plasma Moments
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis

**Data Visualization**
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: Orbit Plots
- Data Visualization: Spectrogram

**Mission-related**
- Mission-related
- Mission-related: Analysis
- Mission-related: Calibration
- Mission-related: Monitoring

**Models and Simulations**
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Forward-Fitting
- Models and Simulations: Instrument Response

The existing HSSI record carried two of these — `Data Processing and Analysis` and
`Data Processing and Analysis: Data Access and Retrieval`. Both are retained; the rest are additions
supported by the evidence below. Nothing previously recorded was dropped.

**Evidence for each selection:**

| Value | Evidence in the pinned source |
|---|---|
| Coordinate Transforms | `mavenpy/coordinates.py` and `mavenpy/spice.py` expose frame and coordinate conversion as public functions users call directly; `README.rst` demonstrates one in its "Running" section. |
| Coordinate Transforms: Mission-Specific | `spice.pxform(time_UTC, v_x, v_y, v_z, initial_frame, final_frame)` and `spice.bpl_to_bmso(...)` rotate vectors between the MAVEN payload frame and MAVEN_MSO using loaded SPICE kernels; `spice.quaternion_rotation`, `spice.MAVEN_position(t_i, frame="MAVEN_MSO")` and `spice.currently_loaded_kernels()` complete the frame machinery. `mavenpy/sep_anc.py` maps SEP sensor look directions to NAIF instrument frame IDs (`SEP_fov_NAIF_ID`) and computes sensor pointing in MSO (`sep_mso_look_dir`). This is spacecraft- and instrument-frame work, which is what "Mission-Specific" denotes. |
| Coordinate Transforms: Planetary | `mavenpy/coordinates.py` converts Cartesian ↔ spherical ↔ Mars geographic latitude/longitude/altitude with the Mars radius as the default reference (`cartesian_to_geographic(x, y, z, re=3389.0, rp=3389.0)`, `rlatlon_to_geographic`, `rlatlon_to_cartesian`, `cartesian_to_spherical_vector`); `spice.local_solar_time` and `spice.mars_sun_distance` are Mars-centric. |
| Data Processing and Analysis | The package's core purpose: reading MAVEN files into common Python structures and operating on them. |
| Data Processing and Analysis: 3D Particle Distribution Processing | `mavenpy/moment_3d.py` operates on full 3D velocity distributions — `jacobian(phi_deg, dphi_deg, theta_deg, dtheta_deg, ...)` builds the solid-angle/energy volume element, and `n`, `nflux`, `v`, `M`, `p`, `T` integrate `diff_en_flux_eVcm2eVsters` over energy, theta and phi. SWIA coarse/fine 3D and SWEA `svy3d`/`arc3d` datasets are the inputs. |
| Data Processing and Analysis: Analysis | `mavenpy/units.py` derives physical quantities from data — `alfven_speed`, `sound_speed`, `dynamic_pressure`, `energy`/`scalar_velocity` conversions, `lorentz_factor_from_velocity`. `mavenpy/mars_shape_conics.py` classifies spacecraft position into solar wind / magnetic pileup / shadow regions (`solar_wind_indices`, `pileup_indices`, `region_index`, `region_separation`). `mavenpy/swea_topo.py` implements the SWEA magnetic-topology matrix. `scripts/find_sw_coverage.py` computes solar-wind coverage statistics per Carrington rotation. |
| Data Processing and Analysis: Calibration | `mavenpy/sep_calib.py` implements the SEP raw-counts calibration chain: `raw_to_fto` (raw bins → front/thick/open coincidence classes via `map_to_bins` with map identifiers), `fto_to_calibrated`, `norm_flux_factor(sensor_num, look_direction, particle_name, mapnum=9)` and `unit_conversion(data, data_name, data_unit, ...)`. `mavenpy/sep.py` calls this chain (`from .sep_calib import raw_to_fto, fto_to_calibrated`) and `tests/verify_sep_read_calib.py` exercises it. |
| Data Processing and Analysis: Data Access and Retrieval | `mavenpy/retrieve.py` is a complete HTTP archive client: `sdc_retrieve` drives the download, `html_retrieve` + BeautifulSoup parse remote HTML directory indexes, `newest_file_from_html_index` and `extract_date_modified` pick the newest version/revision, `remote_file_updated` compares remote and local timestamps, `download_file` streams to disk. `mavenpy/file_path.py` (`local_file_names`, `most_recent_version`) and `mavenpy/specification.py` (`path`, `filename`, `remote_base_directory`, `check_if_dataset_on_remote`) construct the mirrored directory tree and versioned filenames. |
| Data Processing and Analysis: Data Reduction | `mavenpy/ngims.py` `resample(ngims_csn_dat, orbit_nums=None, altitude_bins=None, ...)` and `orbit_average(resampled_ngims, orbit_range)` bin and average NGIMS densities; `helper.rolling_sum(time_s, data, dt, skip=None)` accumulates counts over a moving window; SEP Level-1 exposes `01hr`/`32sec`/`5min` cadence products and MAG exposes `full`/`1sec`/`30sec`. |
| Data Processing and Analysis: Energy Spectra | Energy-resolved spectra are a first-class data structure throughout: `helper.invert_energy_axis`, `helper.format_energy_as_string`, `sep.read_cal`/`cal_FOV_field_names`, `swia.process` (coarse/fine/`onboardsvyspec` differential energy flux), `swea.read` (`svyspec`), `euv.read` (Level-3 FISM-fitted spectra), and `moment_1d.trapezoidal_dE`/`moment_N_T` which integrate over the energy axis. |
| Data Processing and Analysis: Pitch Angle Distributions | `mavenpy/sep.py` `read_pad(filename, field_names=None, particle="", include_unit=True)` reads SEP Level-3 pitch angle distributions; `specification.py` declares SWEA `svypad` and `arcpad` datasets and `UPDATE.rst` documents the commands to download them. |
| Data Processing and Analysis: Plasma Moments | `mavenpy/moment_1d.py` `moment_N_T(...)` derives density and temperature from 1D energy spectra; `mavenpy/moment_3d.py` `n`, `v`, `p`, `T`, `M` and the dispatching `moment(desired_moments, time_unix, energy_eV, ...)` compute density, bulk velocity, pressure tensor and temperature from 3D distributions. `moment_3d.H_alpha_moments` separates proton and alpha moments and its docstring records its origin: "Adaptation of mvn_swia_protonalphamoms_minf.pro". |
| Data Processing and Analysis: Processing | `mavenpy/read.py` (`read_cdf`, `read_sav`, `read_tplot`, `parse_tplot_plot_parameters`, `reformat_sav`, `flatten_rec`, `check_convert_byte_str_arr`) and `mavenpy/load.py` `load_data` normalize heterogeneous archive files into one dictionary structure and concatenate multi-day data along the time axis. `helper.process_data_dict` applies quality masks and unit attachment. |
| Data Processing and Analysis: Time Series Analysis | `load.load_data` identifies the time axis of each file and appends successive days along it; `helper` provides `dt_range`, `daterange`, `find_closest_index_dt`, `subset_window`, `continuous_index_interval`, `UNX_to_UTC`/`UTC_to_UNX`; `specification.in_datagap` and `specification.during_safemode` mask known MAVEN data gaps and the five recorded safe-mode intervals. |
| Data Visualization | `mavenpy/plot_tools.py` plus four plotting scripts (`scripts/plot_MAVEN_orbit.py`, `scripts/plot_sep.py`, `scripts/plot_euv.py`, `scripts/tohban.py`) and the three demo scripts (`demo_mag.py`, `demo_solarwind.py`, `demo_ephemeris.py`), all matplotlib-based. The other two files in `scripts/` are not plotting tools and import no matplotlib: `find_sw_coverage.py` is an analysis script and `update.py` is a download driver. |
| Data Visualization: 2D Graphics | `scripts/plot_MAVEN_orbit.py` renders a Mars crustal magnetic field map with `ax_r.contourf(lon, lat, br, ...)`; `plot_tools.add_colorbar_outside` and `plot_tools.patch_gap` support 2D `pcolormesh` panels across the scripts. |
| Data Visualization: Line Plots | Time series line panels in `demo_mag.py`, `demo_solarwind.py`, `demo_ephemeris.py`, `scripts/plot_euv.py` and `scripts/plot_sep.py`; `plot_tools.format_xaxis(ax, start_date, end_date)` and `plot_tools.legend_sidetext` are shared line-plot helpers. |
| Data Visualization: Mission-Specific | `scripts/tohban.py` reproduces the MAVEN Particles and Fields daily summary display: it downloads `mvn_ql_pfp_{yyyy}{mm}{dd}.tplot` quicklook files from the Berkeley SSL server and rebuilds the panels with MAVEN-specific axis labels hard-coded per tplot variable (`mvn_sep1f_ion_eflux`, `mvn_sta_c0_e`, `mvn_sta_c6_m`, `mvn_swis_en_eflux`, `mvn_swe_etspec`, `mvn_lpw_iv`, `mvn_mag_bamp_1sec`, `burst_flag`). These plot types exist only for MAVEN's instrument suite. |
| Data Visualization: Orbit Plots | `scripts/plot_MAVEN_orbit.py` plots the spacecraft trajectory against the Mars disc and the bow shock / magnetic pileup boundary conics; `anc.add_orbit_axis(ax, data_directory=None, ephemeris=None, ...)` adds an orbit-number axis to any time series plot; `anc.segment_orbit` and `anc.sort_segments_by_day` split trajectories into orbit segments. |
| Data Visualization: Spectrogram | Energy–time dynamic spectra are drawn with `pcolormesh` under a log norm in `scripts/plot_sep.py`, `scripts/plot_euv.py`, `scripts/tohban.py`, `demo_solarwind.py` and `tests/verify_sep_read_calib.py`; `plot_tools.patch_gap` exists specifically so `pcolormesh` does not draw spurious polygons across data gaps in these panels. |
| Mission-related | MavenPy is not a general-purpose tool that happens to accept MAVEN files — it is built around one mission. `specification.py` encodes MAVEN's Mars orbit insertion date, its five safe-mode intervals, its per-instrument level/dataset/format matrix and its three archive layouts; `spice.py` encodes MAVEN's kernel naming and directory conventions. |
| Mission-related: Analysis | The package's science routines are written against MAVEN instrument data products specifically, and many are ported from named MAVEN SPEDAS IDL routines (`mag.read` docstring: "based on the MAG SIS document and the MAVEN SPEDAS routine 'mvn_mag_load.pro'"; `mars_shape_conics.py`: "Conic section fits based on maven_orbit_tplot.pro"; `spice.py`: "based on spice_file_source.pro"). |
| Mission-related: Calibration | The SEP calibration chain in `sep_calib.py` is the mission instrument's own calibration, reimplemented — sensor/telescope/detector coincidence maps, per-look-direction normalization factors and unit conversion for a specific MAVEN instrument. Listed under both parents because the capability is simultaneously general data calibration and mission-instrument calibration. |
| Mission-related: Monitoring | "Tohban" is the MAVEN Particles and Fields daily duty-scientist role; `scripts/tohban.py` is named for it and regenerates that shift's instrument summary display from the mission's daily quicklook files. The strongest evidence is that the mission itself publishes the product under that name: lines 15–17 fetch `mvn_ql_pfp_{yyyy}{mm}{dd}.tplot` from `sprg_url = "http://sprg.ssl.berkeley.edu/data"` (line 15) under `tplot_dir = ("maven", "anc", "tohban", "{yyyy}", "{mm}")` (line 17) — a server directory literally named `tohban`. The residual objection is recorded rather than dismissed: MavenPy is an individual researcher's package, not a formal ground-system component, so a reviewer could read this as consuming a monitoring product rather than performing monitoring. It is included because the script's whole purpose is to reproduce the mission's routine daily instrument monitoring display. |
| Models and Simulations | Two model families are implemented in-package (empirical boundary models and forward-fitted distribution models) alongside instrument field-of-view geometry modeling. |
| Models and Simulations: Empirical | `mavenpy/mars_shape_conics.py` implements published empirical conic-section models of the Martian bow shock (`bow_shock(reference='Trotignonetal2006')`) and magnetic pileup boundary (`MPB(reference="Trotignonetal2006_twoconics")`), parameterized by offset, semi-latus rectum and eccentricity. These are empirical fits to observations, used to classify where the spacecraft is. |
| Models and Simulations: Forward-Fitting | `mavenpy/moment_1d.py` builds analytic distribution models (`maxwell_boltzmann_nflux`, `maxwell_boltzmann_eflux`, `kappa_nflux`, the `maxwell_boltzmann_function` class) and fits them to observed spectra with `scipy.optimize.curve_fit` in `curve_fitted_N_T(energy_eV, d_energy_eV, diff_en_flux_eVcm2eVsters, mass_eVkm2s2, sc_potential_V=None, plot_fits=None)`, recovering density and temperature. That is a forward model plus parameter optimization. |
| Models and Simulations: Instrument Response | `mavenpy/sep_anc.py` models the SEP sensors' geometric response: `get_fov_pixels(sep_sensor, sep_look_direction, pixel_width_deg=1.5)` tessellates each sensor's field of view, `fov_target_angle` computes the angle from a look direction to a target, and `fraction_Mars_in_FOV(sensor, look_direction, time_utc, ...)` computes what fraction of each sensor's field of view Mars occludes at a given time. |

**Considered and rejected, with reasons — so these are not re-litigated:**

- **Data Processing and Analysis: Spectrogram** — rejected. The package assembles and plots energy–time
  dynamic spectra, but it computes no time–frequency transform: there is no FFT, STFT or wavelet
  anywhere in the source. The energy binning arrives already applied from the archive. The *display*
  of these spectra is captured by `Data Visualization: Spectrogram`, and the energy-axis work is
  captured by `Data Processing and Analysis: Energy Spectra`. Note that LPW `wspecact`/`wspecpas`
  wave-spectra datasets are declared for download in `specification.py` but have no reader, so they do
  not change this conclusion.
- **Data Processing and Analysis: Wavelet Analysis**, **Wave Polarization Analysis** — rejected; no
  such code exists.
- **Data Processing and Analysis: File Format Conversion** — rejected, on a narrower premise than it
  might first appear. The package reads CDF, IDL `.sav`, `.tplot`, CSV and STS files into a common
  in-memory dictionary, and it does write one data file — the plain-text solar-wind coverage table
  recorded in Field 19. But that table holds a *derived* list of interval boundaries, not the input
  data re-encoded, and nothing in the package re-emits an archive file in a format different from the
  one it arrived in. Reading many formats into memory, and writing a derived summary, is not format
  conversion.
- **Data Processing and Analysis: Image Processing** — rejected. IUVS imaging files are downloaded but
  never opened (see Field 18); no image-processing routines exist.
- **Data Processing and Analysis: Packet Decommutation** — rejected. Raw Particles and Fields Level-0
  `.dat` telemetry files are downloadable (`formats["pfp"]`), but nothing in the package parses them;
  there is no packet-level code.
- **Data Processing and Analysis: ML/AI** — rejected; no machine-learning code or dependency.
- **Data Processing and Analysis: 2D Slices** and **Data Visualization: 2D Slices** — rejected, and the
  contrary evidence together with the reason it fails is worth recording, because the surface reading
  is tempting. `moment_3d.H_alpha_moments(..., debug_plots=False)` will, when the flag is set, draw
  3×3 panels of theta/phi cuts through a 3D distribution, and `tests/rebin_swif.py` plots theta–phi
  field-of-view slices at fixed energy. What settles it is that the `debug_plots` branch is not
  parameterized at all: `moment_3d.py` lines 550–568 hard-code the sample times twice over —
  `time_indices = [13870, 14010, 14250]` is immediately overwritten by
  `time_indices = [7431, 7670, 7807]` on the next line, with no way for a caller to supply either.
  That is leftover developer debug code against one particular dataset, not a slicing capability
  offered to users.
- **Data Visualization: 3D Graphics** — rejected. `scripts/plot_MAVEN_orbit.py` draws 2D projections of
  the orbit; there is no `mplot3d`, `Axes3D`, `projection='3d'`, VTK, Mayavi or PyVista use anywhere.
- **Data Visualization: Movies** — rejected; no `matplotlib.animation` or frame-export code.
- **Data Visualization: Web-Based** — rejected; no Plotly, Bokeh or Dash.
- **Data Visualization: Hodograms**, **Spacecraft Formation Plots** — rejected. MAVEN is a single
  spacecraft, and no component-versus-component field plots exist.
- **Coordinate Transforms: Magnetospheric** — rejected. That subcategory denotes the Earth
  magnetospheric frames (GSE, GSM, SM, GEO, MAG). MavenPy's frames are Mars-centric (MAVEN_MSO, Mars
  geographic, payload) and are covered by `Planetary` and `Mission-Specific`.
- **Coordinate Transforms: Heliospheric**, **Solar**, **Ionospheric** — rejected; no HCI/HAE/HEE/RTN,
  Carrington/Stonyhurst/helioprojective, or AACGM/apex/magnetic-local-time conversions exist.
  `spice.mars_sun_distance` returns a scalar distance, not a heliospheric frame conversion.
- **Mission-related: Distribution/Access** — rejected. MavenPy is a *client* of the mission archives,
  not a distribution system. Its archive-access capability is recorded as
  `Data Processing and Analysis: Data Access and Retrieval`, and the archives themselves are recorded
  in Field 17.
- **Mission-related: Ingest**, **Archive**, **Operations**, **Orchestration**, **Science Data
  Processing**, **Instrumentation**, **System Testing**, **Inventory**, **Infrastructure as Code** —
  rejected. MavenPy is not part of the MAVEN ground segment and performs none of these roles.
- **Models and Simulations: MHD**, **First Principles**, **Physics-Based**, **Theory**, **Data
  Guided**, **Forecasting**, **Mission-Specific**, **Observatory/Instrument Models**, **Field-line
  Tracing**, **ML/AI** — rejected. There is no simulation code, no field solver, no field-line
  integrator and no forecasting output. `Models and Simulations: Instrument Response` is the correct
  and narrower home for the SEP field-of-view geometry work, in preference to the broader
  `Observatory/Instrument Models`.
- **Servers and Environments** and all its subcategories — rejected. There is no Dockerfile, no server,
  no MPI or parallel-computing code and no deployment configuration in the repository.

---

### 5. Related Region (MANDATORY)

- Planetary Magnetospheres
- Mars Magnetosphere
- Solar Wind
- Interplanetary Space

`Planetary Magnetospheres` is carried over from the existing HSSI record and retained. `Mars
Magnetosphere` is added because the live `Region` vocabulary offers it and it is strictly more
specific and more searchable for a Mars-only package; the broader value is kept alongside it rather
than replaced, so no previously recorded association is lost.

`Solar Wind` reflects a genuine, implemented capability rather than a topical association:
`mars_shape_conics.solar_wind_indices(x, y, z, reference='Trotignonetal2006', ...)` classifies which
samples lie upstream of the Martian bow shock, `scripts/find_sw_coverage.py` computes solar-wind
coverage per Carrington rotation from that classification, `demo_solarwind.py` is one of the three
top-level demonstrations, and SWIA `onboardsvymom` solar-wind moments are a supported product.

`Interplanetary Space` covers the solar energetic particle and solar EUV irradiance measurements made
at Mars's heliocentric distance — SEP Level-1 through Level-3 products with a dedicated reader and
calibration chain, and EUV Level-3 FISM-fitted solar spectra.

**Vocabulary gap worth recording.** A substantial part of what MavenPy supports is Martian
upper-atmosphere and ionosphere science — NGIMS neutral and ion densities, LPW electron density and
temperature, IUVS airglow and coronal observations. The live `Region` vocabulary's 24 rows contain
Earth-specific atmospheric and ionospheric regions (`Earth Atmosphere`, `Earth Ionosphere`, `Earth
Thermosphere`, `Earth Lower and Middle Atmosphere`) but **no** Mars or general planetary
atmosphere/ionosphere/thermosphere value. Selecting an `Earth *` row for Mars data would be wrong.
That is why this field stops at the four values above rather than covering the atmospheric side of the
package: the vocabulary has no correct row for it, not because the capability was overlooked.

**Rejected:** `Solar Environment` — the EUV Level-3 product is a solar irradiance spectrum, but
MavenPy neither models nor analyzes the solar atmosphere; it reads an already-fitted irradiance time
series. `Earth Magnetosphere` and every other `Earth *` row — no Earth data is supported.
`Heliosheath`, `Jupiter/Saturn/Neptune/Uranus Magnetosphere` — no.

---

### 6. Authors (MANDATORY)

**Author:** Rebecca Jolitz
- **Author Identifier:** https://orcid.org/0000-0001-6360-0140
- **Affiliation:**
  - Organization: Space Sciences Laboratory, University of California, Berkeley — https://ror.org/048400679

**This corrects a placeholder, and is not a removal of anyone.** The stored HSSI author was a single
author record with `given_name=''`, `family_name='rjolitz'`, no identifier and no affiliation — that
is the GitHub account name of the same human, captured as a bare string. The union rule for authors is satisfied: the author set still
has exactly one member and no one is dropped; the member's identity is filled in.

**Evidence that one author is the complete and correct set:**

- `git log` over the pinned history returns 111 commits, every one authored by
  `Rebecca Jolitz <rjolitz@berkeley.edu>`. There are no other committers and no co-author trailers.
- `setup.py` line 47 declares `author="Rebecca Jolitz"` with no `author_email` and no maintainer.
- `LICENSE` line 1 reads `Copyright (c) 2022, Rebecca Jolitz`.
- There is no `CITATION.cff`, no `AUTHORS`, no `CONTRIBUTORS`, no `codemeta.json` and no `.zenodo.json`
  that could name additional authors.
- `README.rst` thanks "the original authors of those routines" in the Berkeley SSL SPEDAS IDL
  distribution but names none of them, and thanking upstream authors is not co-authorship. That
  relationship is recorded in Field 29 instead, where it belongs.

**Evidence that this is the right ORCID.** An ORCID registry search on the family name Jolitz returns
three people; only `0000-0001-6360-0140` is a Rebecca Jolitz, and her affiliations are University of
California, Berkeley and University of Colorado Boulder. Her public works list is unambiguously the
same researcher: "Energy Input of EUV, Solar Wind, and SEPs at Mars: MAVEN Observations During Solar
Minimum" (10.1029/2022JA030884), "Test Particle Model Predictions of SEP Electron Transport and
Precipitation at Mars" (10.1029/2021JA029132), "First observations of atmospheric sputtering at Mars"
(10.1126/sciadv.adt1538), and further MAVEN and Martian-atmosphere papers. The `@berkeley.edu` commit
address corroborates the Berkeley affiliation.

**Evidence for the affiliation, and why there is exactly one.** Her public ORCID record contains a
single employment summary: department "Space Sciences Laboratory", role "Postdoc", organization
"University of California, Berkeley", Berkeley US, disambiguated to ROR `https://ror.org/01an7q238`.
That is one employer plus a department name, not two employments — so it is recorded as one
affiliation. The department is preferred over the bare parent organization because it is the unit
ORCID actually names, because it is the institution whose SPEDAS IDL routines MavenPy is derived from
and whose SPRG server the package mirrors, and because it is itself a registered organization: ROR
`https://ror.org/048400679` carries the names SSL / Space Sciences Lab / Space Sciences Laboratory /
UCB SSL, confirming it is the Berkeley unit.

**The recorded name is fixed by the shared organization row, not freely chosen.** HSSI already holds
an organization with ROR `https://ror.org/048400679` under the name
`Space Sciences Laboratory, University of California, Berkeley`. Organizations resolve by identifier
first, and a supplied name is only written when the existing name is empty — so submitting the
shorter form `Space Sciences Laboratory` would bind to that same row and the shorter name would be
silently discarded. This dossier therefore records the existing row's name exactly. A future agent
who prefers different wording needs to change the organization row itself, not this record. The name
also happens to satisfy the acronym-expansion rule on its own, spelling out both "Space Sciences
Laboratory" and the parent university rather than "SSL" or "UC Berkeley".

*Rejected alternative — listing two affiliations.* Recording `Space Sciences Laboratory` and
`University of California, Berkeley` as separate affiliation entries was considered. It is wrong on
two counts: ORCID documents one employment rather than two, and the existing organization row's name
already spells out the parent university, so a second entry would be redundant rather than additive.

**How this correction lands, and the durable constraint it leaves behind.** The `rjolitz` placeholder
is not relabelled — author records are matched by `identifier` first, and supplying the ORCID
`https://orcid.org/0000-0001-6360-0140` **creates a correctly identified author record and repoints
this software at it**. The placeholder is left behind unreferenced by MavenPy, which is the accepted
outcome rather than a fault to clean up: at the time of this correction it was referenced by no other
software record, and no author record carried this ORCID beforehand, so nothing else was affected and
no duplicate was created.

**The constraint that outlives this correction: the `rjolitz` placeholder can never be carried in an
authors payload for this record.** Author names are normalized on the way in, and a blank given name
is rejected outright — the failure fires whenever a blank-named author appears in the submitted set,
and it rejects the entire authors field, not just the offending entry. The placeholder has a blank
given name. So any future edit to MavenPy's authors must send the **complete corrected author set**;
full replacement is the only expressible operation. There is no way to add a second author while
leaving the placeholder in place, and an agent that tries an incremental append including the
placeholder will see the whole field refused.

---

### 7. Software Name (MANDATORY)

`MavenPy`

Carried over unchanged from the existing HSSI record. This is a deliberate decision to preserve the
submitter's editorial choice, not an absence of alternatives — the repository actually spells the name
three different ways at the pinned revision:

- `README.rst` title block: `MAVENPy`
- `setup.py` `name=` and the GitHub repository name: `mavenpy`
- `LICENSE` third clause: "the MAVENPY project"

None of these is more authoritative than the others, and `MavenPy` is a reasonable rendering that
matches none of them exactly but reads correctly. Changing a submitted name to a different
capitalization of the same word would be a stylistic substitution with no factual basis, so the stored
value stands.

---

### 8. Description (MANDATORY)

This description replaces an earlier stored value that was an autofill artifact rather than authored
prose. The replacement and the reason for it are below; the superseded text is recorded verbatim after
it. The blockquote's line breaks are presentational only — it is hard-wrapped for readability, and the
actual value is the unwrapped paragraphs and list items, with each wrapped continuation rejoined to its
preceding line by a single space.

> MavenPy is a Python package for downloading, reading, and analyzing data from NASA's Mars Atmosphere
> and Volatile EvolutioN (MAVEN) mission. It retrieves MAVEN data files from the mission's public and
> team archives, mirrors the remote directory trees locally, resolves local file paths and versions,
> and loads the files into common Python data structures. Routines are present for the following data
> products:
>
> - SPICE: kernel download from NAIF, loading via SpiceyPy, and MAVEN position, attitude and
>   coordinate-frame transforms
> - Ephemeris: spacecraft ephemeris (from Berkeley SSL SPRG) and orbit ephemeris (from SPICE)
> - EUV: Level-3 FISM-fitted spectra, Level-2 bands
> - MAG: Level-2 and Level-1 magnetic fields (all cadences, all file formats)
> - NGIMS: Level-2 neutral and ion densities (Level-3 is disrecommended)
> - SEP: Level-1 (raw counts), Level-2 (counts and processed spectra), Level-3 (pitch angle
>   distributions) and ancillary data
> - SWEA: Level-2 (spectra, pitch angle distributions, 3D distributions), Level-3 (spacecraft
>   potential, topology)
> - SWIA: Level-2 angle-averaged and differential spectra and moments (coarse, fine and onboard survey
>   modes)
> - LPW, STATIC, IUVS, ACC, ROSE and raw Particles and Fields Level-0: file retrieval and path
>   resolution
>
> It also provides plasma moment calculations from 1D and 3D particle distributions, SEP calibration
> from raw counts to physical units, empirical Mars bow shock and magnetic pileup boundary models,
> solar wind interval identification, and plotting utilities for time series, energy-time spectrograms
> and MAVEN orbit geometry. Command-line scripts are included for updating a local MAVEN data archive,
> for computing solar-wind coverage statistics, and for producing SEP, EUV, orbit and daily quicklook
> summary plots.
>
> MavenPy is heavily based on IDL programs in the Berkeley SSL tplot SPEDAS distribution that read and
> analyze MAVEN spacecraft data. The original authors of those routines are thanked, and the source
> IDL program is referenced where a routine is derived from one. The package requires Python 3.11 or
> above and is still in development.

**Superseded value, recorded so the change is auditable:**

```
Python routines to download, look up, access and manipulate MAVEN spacecraft data.
Routines to import and download MAVEN data.
Python routines to download, read, and interact with MAVEN spacecraft data. Routines are present for following data products:
    - Spice: Downloading from NAIF, loading via SpiceyPy
    - ephemeris: spacecraft ephemeris (from SSL SPRG) and orbit ephemeris (from Spice) 
    - EUV: Level-3 FISM-fitted spectra, Level-2 bands
    - MAG: Level-2 and 1 magnetic fields (all cadences) (all file formats)
    - NGIMS: Level-2 neutral and ion densities (Level-3 disrecommended)
    - SEP: Level-1 (raw counts), Level-2 (counts and processed spectra), Level-3 (ancillary data, PADs)
    - SWEA: Level-2 (spectra, PAD, 3d), Level-3 (spacecraft potential, topology)
    - SWIA: Level-2 (coarse/fine/onboardsvyspec) angle-averaged spectra (CDF), Level-2 (coarse/fine/onboardsvyspec) differential spectra (CDF), Level-2 moments (CDF). 
This is a package heavily based on IDL programs in the Berkeley SSL tplot SPEDAS distribution that read and analyze MAVEN spacecraft data. We thank the original authors of those routines, and have thanked them and referenced the source IDL program where derived.
```

**Why this is a correction of an artifact rather than a stylistic rewrite.** The stored text is not
authored prose — it is three sources concatenated by an autofill step, and each source is still
individually identifiable at the pinned revision:

1. Line 1 is the GitHub repository's one-line description field, returned by the GitHub API as
   "Python routines to download, look up, access and manipulate MAVEN spacecraft data."
2. Line 2 is `setup.py` line 48: `description="Routines to import and download MAVEN data."`
3. Everything from line 3 onward is `README.rst` lines 5–13 followed directly by line 17 — the
   per-instrument product list and the SPEDAS attribution paragraph. Lines 14 and 16 (both blank)
   and, consequentially, line 15 (`Depends on Python3.11 and above.`) are **absent** from the stored
   text: the concatenation dropped the package's stated Python requirement. The stored text also
   carries a trailing space after `Level-2 moments (CDF).` that `README.rst` line 13 does not have,
   and did not have at any of the three commits that have touched that file (`093ee28`, `7b94199`,
   `607c507`) — so the space was introduced by the concatenation rather than copied from source.

The result opens with three consecutive sentences that all say "Python routines to download … MAVEN
data", which is what a reader sees in the 150–200 character preview. Field 8 asks for a description
"written with proper capitalization, grammar, and punctuation"; a concatenation of three overlapping
source strings does not meet that bar, and no human chose that wording.

The replacement is deliberately conservative about *content*: it keeps the complete
per-instrument product list, keeps the level and dataset detail, and keeps the SPEDAS attribution
paragraph in full, because those are the substantive things the original submitter conveyed. What it
changes is (a) removing the two duplicated opening sentences, (b) expanding acronyms and shorthand on
first use ("PAD" → "pitch angle distributions", "3d" → "3D distributions", "Spice" → "SPICE"), (c)
adding the capabilities the stored text omits entirely — plasma moments, SEP calibration, the
empirical Mars boundary models, solar-wind interval identification, plotting, and the command-line
scripts, all of which are major parts of the package and none of which the README paragraph mentions —
and (d) restoring the Python 3.11 requirement that the concatenation dropped (`README.rst` line 15)
and adding the in-development status the README gives on line 23.

Two smaller factual corrections are folded in and are worth calling out: the stored text lists only
the instruments with readers, so a reader would not learn that LPW, STATIC, IUVS, ACC, ROSE and raw
Particles and Fields Level-0 are also retrievable (`mavenpy/specification.py` declares levels,
datasets, extensions and sources for all of them and `UPDATE.rst` documents LPW and IUVS download
commands); and "Spice: Downloading from NAIF, loading via SpiceyPy" understates `mavenpy/spice.py`,
which at 1190 lines is the largest module in the package and provides position, attitude and frame
transforms, not only kernel management.

A third correction is inherited from the README rather than introduced by the concatenation: the
stored text reads "SEP: … Level-3 (ancillary data, PADs)", which folds ancillary data into Level-3.
`mavenpy/specification.py` lines 148–156 separate them — `formats["sep"]["level"]` is
`("l1", "l2", "l3", "anc")`, with `"l3": "pad"` and a distinct `"anc"` level whose extensions are
`("sav", "cdf")`. Ancillary data is its own level, not a Level-3 product, so the replacement reads
"Level-3 (pitch angle distributions) and ancillary data". The README's own wording is what introduced
the conflation, so a future agent comparing the two will find the README and this record disagreeing
on purpose.

The command-line sentence likewise names `scripts/find_sw_coverage.py` (574 lines;
`n_carrington_days = 27.2753` at line 15, `make_Carrington_sw_pass_ranges` at line 470), which the
stored text omits entirely and which is the script that produces the solar-wind coverage table
recorded in Field 19.

**Why replacing a submitted, subjective field was the right call here.** The general rule is to
preserve a submitter's wording rather than substitute a stylistic preference. This case is the
exception the rule allows for: the superseded text was not anyone's wording. It was three source
strings mechanically joined, with the first two saying the same thing as the third, and it silently
dropped a requirement the README states. The narrower fix — leaving the stored text alone and letting
the Field 9 concise description mask the duplicated opening in the preview — was considered and
rejected, because it would have left the duplication, the dropped Python requirement and the missing
capabilities in the description a reader actually opens.

---

### 9. Concise Description (OPTIONAL)

`Python package to download, read and analyze MAVEN spacecraft data: SPICE ephemeris, MAG, EUV, SEP, SWEA, SWIA, NGIMS and more, with plasma moments, calibration and plotting tools.`

180 characters, within the 200-character limit.

This field was previously empty, which meant the site fell back to previewing the first ~200
characters of the description — and under the superseded description those characters were the
duplicated opening sentences described in Field 8. Filling this field fixes the preview independently
of the description itself, which is the main reason it is populated rather than left to the fallback.

The wording is drawn from the repository's own vocabulary: the instrument list is the set with
dedicated reader modules plus SPICE, and "plasma moments, calibration and plotting" names the three
analysis capabilities (`moment_1d.py`/`moment_3d.py`, `sep_calib.py`, `plot_tools.py` and the scripts)
that the existing description omits.

---

### 10. Publication Date (RECOMMENDED)

`2024-07-15`

Carried over unchanged and independently confirmed twice: the GitHub API reports
`created_at: 2024-07-15T17:25:19Z`, and the first commit in the pinned history — `093ee28`, titled
"Initial commit (from Bitbucket repo)" — is dated 2024-07-15.

Note for interpretation: this is the date the code became public *on GitHub*. The commit title and the
`setup.py` Bitbucket URL show the project existed earlier on Bitbucket, and `LICENSE` is dated 2022.
No earlier public-availability date is recoverable, since the Bitbucket repository is not reachable
and its history was squashed into the single initial GitHub commit. 2024-07-15 remains the correct and
defensible value for first public broadcast at the current location.

---

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Newly filled; stored as null in HSSI. This follows Field 11's own instruction: "If no DOI has been
obtained, indicate the repository host, such as GitHub or GitLab." No DOI exists (Field 2), and GitHub
is where the software is published.

**Rejected alternatives.** Zenodo — rejected, because the form directs Zenodo only "for software where
a DOI has been obtained through Zenodo", and no Zenodo record exists. University of California,
Berkeley — rejected; it is the author's institution (Field 6), not the publisher of the code, and
nothing in the repository presents it as an institutional release. Bitbucket — rejected as the stale
former host (see Field 3).

This value is an application of the form's instruction rather than a fact stated anywhere in the
repository. It is recorded on that basis and not on repository evidence, which is the honest standing
of the claim: GitHub is where the software is published, and the form names the repository host as the
correct entry when no DOI exists.

---

### 12. Version (RECOMMENDED)

- **Version Number:** `0.0.0`
- **Version Date:** Not found
- **Version Description:** Not found
- **Version PID:** Not found

**This is the field with the weakest evidence in this dossier, and the reasoning matters more than the
value.** The complete evidence:

- `mavenpy/about.py` contains exactly one line: `__version__ = '0.0.0'`.
- `git log --follow -- mavenpy/about.py` returns exactly one commit: `093ee28`, 2024-07-15, "Initial
  commit (from Bitbucket repo)". The version string has never been changed across the 111 commits of
  the repository's public history, the most recent of which is dated 2026-04-01.
- `setup.py` reads that file (`exec(open("mavenpy/about.py").read())`) and passes it as the package
  version, so an installed copy reports `0.0.0` from `mavenpy.__version__` and from packaging metadata.
- The repository has zero git tags. The GitHub releases and tags endpoints both return empty arrays.
- `setup.py` classifies the package `"Development Status :: 3 - Alpha"`.
- `README.rst` line 23 states "This package is still in development."
- The package is not on PyPI (see Field 2), so no index version history exists either.

**Why `0.0.0` rather than leaving the field empty.** `0.0.0` is not invented — it is the version the
software declares about itself and the version a user's environment will report. It is also
informative in exactly the way a reader needs: it says, unambiguously, that this package has never cut
a numbered release. The stored HSSI value is an empty placeholder version row (number, release date,
description and version identifier all blank) that the site renders as "MavenPy - ", which
communicates nothing at all. Recording the declared version is a strict improvement over that.

**The counter-argument, and why `0.0.0` was chosen over it anyway.** A version of `0.0.0` that has
never been incremented is a scaffolding default rather than a release identifier, and publishing it
next to the software name risks reading as though a 0.0.0 release occurred. Leaving Field 12 entirely
empty was the defensible alternative and was weighed seriously. `0.0.0` was chosen because it is not
invented — it is what the repository declares and what an installed copy reports — and because it
carries the more useful signal of the two: an empty field says nothing, whereas `0.0.0` alongside
Field 23's `WIP` says correctly that this package has never cut a numbered release. The empty
placeholder it replaces communicated neither.

**Rejected alternatives.** Using the commit SHA `fb05d5202815a6713224de8ab33e98de22852e4c` as the
version number — rejected; a revision identifier is not a version, and it already appears in this
file's provenance header where it belongs. Deriving a version from the most recent commit date —
rejected as fabrication. Taking any version from the unrelated PyPI `mavenpy` project (0.1.0–0.1.5) —
rejected; see the collision warning in Field 2.

**Version Date is deliberately left empty even though a date is available.** 2024-07-15 is when
`0.0.0` was first committed, but recording it as a release date would assert a release event that
never happened. Version Description and Version PID are empty because there is no changelog, no
release notes file and no DOI.

---

### 13. Programming Language (RECOMMENDED)

`Python 3.x`

Carried over unchanged and confirmed: every source file in the repository is Python, the GitHub API
reports `language: Python`, `README.rst` line 15 states "Depends on Python3.11 and above", and there
are no compiled extensions, no `ext_modules` in `setup.py`, and no C, Fortran or Cython sources.

`Python 2.x` is not applicable (the stated floor is 3.11). `IDL` was considered and rejected: MavenPy
is a *port of* IDL SPEDAS routines and its docstrings name the `.pro` files they derive from, but the
repository contains no IDL source and executes no IDL. `file_path.get_IDL_data_dir` merely reads
SPEDAS's `ROOT_DATA_DIR` environment variable, optionally by parsing an IDL startup file as text, so a
user can share one data directory between IDL SPEDAS and MavenPy — that is interoperability with an
IDL installation, not IDL code, and it is recorded under Field 30.

---

### 14. Reference Publication (RECOMMENDED)

**Not found.**

Negative research: there is no JOSS paper, no software paper and no "how to cite" section anywhere in
the repository. `README.rst` contains no citation guidance. There is no `CITATION.cff`. DataCite and
Zenodo searches for `mavenpy` return nothing.

The author's own MAVEN publications (recorded in her ORCID profile, cited under Field 6) were
considered and rejected for this field: none of them is a paper *about* MavenPy, and nothing in the
repository designates any publication as its preferred citation. Asserting one would be inference
about the author's intent, not metadata.

---

### 15. License (RECOMMENDED)

- **License:** `BSD 3-Clause "New" or "Revised" License`
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

Carried over unchanged from the existing HSSI record and confirmed against the repository. The
`LICENSE` file (24 lines) is the standard three-clause BSD text — the third clause is present at lines
11–12: "Neither the name of the MAVENPY project nor the names of its contributors may be used to
endorse or promote products…". GitHub's license detection independently reports
`spdx_id: BSD-3-Clause`.

The value is written in the canonical form of the name rather than an abbreviation or an SPDX
identifier, which matters because HSSI's licence names are matched literally and the list carries
near-duplicate legacy spellings. Note that `setup.py` declares only `license="BSD"` and the classifier
`"License :: OSI Approved :: BSD License"`, neither of which distinguishes 2-clause from 3-clause; the
`LICENSE` file text is what settles it, and `BSD 2-Clause "Simplified" License` is therefore rejected.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- mag
- maven
- nasa
- sep
- swea
- swia
- euv
- ephemeris
- iuvs
- lpw
- mars
- ngims
- plasma
- python
- solar wind
- space physics
- spedas
- spice

The first six are the existing HSSI keywords (stored lower-case, rendered title-case by the site) and
are retained unchanged. They are exactly `setup.py` line 55:
`keywords=["maven", "nasa", "swia", "sep", "mag", "swea"]`.

The twelve additions and why each is justified:

- `mars` — the single most conspicuous gap. Nothing in the existing keyword set says Mars, even though
  every data product, coordinate system and boundary model in the package is Martian.
- `euv`, `iuvs`, `lpw`, `ngims` — completes the instrument set already begun by `mag`, `sep`, `swea`
  and `swia`, so every instrument the package supports is searchable by acronym. All four are declared
  in `mavenpy/specification.py`; EUV and NGIMS additionally have dedicated reader modules.
- `spice`, `ephemeris` — `mavenpy/spice.py` is the largest module in the package and
  `mavenpy/anc.py` is dedicated to spacecraft and orbit ephemeris; neither capability was findable.
- `solar wind` — matches the implemented solar-wind interval identification and `demo_solarwind.py`.
- `plasma`, `space physics` — the science domain.
- `python` — the implementation language, consistent with existing usage of this keyword.
- `spedas` — MavenPy is derived from the Berkeley SSL SPEDAS IDL distribution and reads SPEDAS
  `.tplot` files; a user searching for SPEDAS-related tooling should find it.

Of these, `mars`, `euv`, `iuvs`, `spice`, `ephemeris`, `solar wind`, `plasma`, `space physics`,
`python` and `spedas` already exist as rows in the live Keyword vocabulary and are reused rather than
duplicated. `ngims` and `lpw` do not yet exist and would be created; Keywords is the one open
vocabulary in the form, so that is expected rather than an error, and the two acronyms follow the
lower-case convention of the existing instrument keywords.

**Rejected keywords, with reasons.** `static` — the MAVEN instrument acronym is an ordinary English
adjective and a common programming term, so as a free-text keyword it would attract unrelated matches;
the instrument association is carried precisely by Field 31 instead. `tplot` — an implementation
detail of the file format read, not a science keyword. `magnetometer` — redundant with `mag`.
`planetary science` — true but too broad to add discrimination beyond `mars`, and the region
associations in Field 5 already carry it. `pfp`, `acc`, `rose` — retrieval-only instruments whose
acronyms are ambiguous outside the mission (see Field 31 for their treatment).

---

### 17. Data Sources (OPTIONAL)

- HTTP/HTTPS Directories
- Observatory/Mission-specific

Both are additions to a previously empty field.

**`HTTP/HTTPS Directories`** is precisely what `mavenpy/retrieve.py` implements. It does not use a
query API — it fetches remote directory index pages over HTTP(S), parses them with BeautifulSoup
(`html_retrieve`, `newest_file_from_html_index`, `extract_date_modified`), matches filenames against
version/revision regular expressions built by `specification.filename`, compares remote modification
times to local files (`remote_file_updated`), and streams the chosen files down (`download_file`).
`specification.remote_base_directory` builds the per-source root path, and `UPDATE.rst` documents the
`--no_mirror` flag that controls whether the remote tree layout is reproduced locally.

**`Observatory/Mission-specific`** is required by Field 17's own instruction — every source MavenPy
supports is a MAVEN mission archive, and the corresponding observatory is recorded in Field 32. The
sources actually reachable in code are the three in `specification.remote_options`
(`"lasp_sdc_team"`, `"lasp_sdc_public"`, `"ssl_sprg"`) — the LASP MAVEN Science Data Center team and
public areas and the Berkeley SSL SPRG MAVEN tree — plus the NAIF SPICE archive
(`spice.py`: `naif_url = "https://naif.jpl.nasa.gov/pub/naif"`). Team-area access takes credentials;
`scripts/update.py` exposes `--username` and `--password` for it.

**A trap in the repository worth recording.** `data_info.yaml` at the repository root lists five
archive URLs, including `PDS_PLASMA: https://pds-ppi.igpp.ucla.edu/...` and
`PDS_ATMOSPHERE: https://atmos.nmsu.edu/PDS/data/PDS4/MAVEN`. **No Python file in the repository reads
`data_info.yaml`**, there is no YAML parser among the dependencies, and
`specification.remote_base_directory` contains the commented-out branch
`# elif source == "pds": # Not handled at this time.` — with `remote_options` excluding PDS, passing a
PDS source raises `IOError`. `data_info.yaml` is a legacy reference document, not live configuration,
and the PDS archives are **not** supported data sources. A future agent reading only that file could
easily conclude otherwise.

**Rejected values.** `FTP/FTPS Directories` — no FTP code or URL anywhere. `CDAWeb`, `HAPI`, `AMDA`,
`das2`, `SSCWeb`, `OMNIWeb`, `VirES`, `TAP`, `Madrigal`, `WDC`, `GFZ`,
`The Virtual Solar Observatory.`, `S3/Cloud-aware` — none is referenced in the source. `Other` — not
needed; the two selected values fully describe the access pattern and the archive class.

---

### 18. Input File Formats (RECOMMENDED)

- CDF
- IDL.sav
- csv
- ascii
- Other

All are additions to a previously empty field.

| Format | Evidence |
|---|---|
| CDF | `read.read_cdf(cdf_file_path, field_names='', lib='cdflib', show_info=False)` reads NASA CDF through either `cdflib` (default) or `spacepy.pycdf`, selected by the `lib` argument. CDF is the declared extension for SWIA Level-2, SWEA Level-2, SEP Level-2, EUV Level-2/3, LPW Level-2 and STATIC Level-2 in `specification.py`. |
| IDL.sav | `read.read_sav(sav_file_path, field_names='', struct_name='', ...)` uses `scipy.io.readsav`, with `reformat_sav`, `flatten_rec` and `check_convert_byte_str_arr` to normalize IDL record structures and byte strings. This covers both plain `.sav` files (SEP Level-1/Level-3, SWEA Level-3, MAG `.sav`, monthly ephemeris) and `.tplot` files — `read.read_tplot`'s docstring states a `.tplot` file "is an IDL sav file that contains a list of tplot variables", and it is read with the same `readsav` call. |
| csv | `ngims.read` parses NGIMS Level-2 comma-separated files with `np.loadtxt(filename, delimiter=',', skiprows=1, dtype=dtype_i)`; `specification.py` declares `formats["ngi"]["ext"] = "csv"`. |
| ascii | MAG's preferred format is a plain-text `.sts` table — `mag.read_sts(filename, method='loadtxt')` and `mag.parse_sts` parse it, and `mag.read`'s docstring states "Unlike other MAVEN instruments, MAGs preferred data format is an ASCII text file postpended with '.sts'". `anc.read_orb` reads NAIF `.orb` orbit files, described in its docstring as "plain text with two header rows"; SPICE text kernels (leap-second, frame, text PCK) are also plain text. |
| Other | SPICE binary kernels. `mavenpy/spice.py` discovers, downloads and furnishes SPK trajectory kernels, CK attitude kernels, spacecraft-clock and frame kernels through `spiceypy`, and MavenPy's position and frame-transform capability is built entirely on them (`load_kernels`, `MAVEN_kernels`, `spk_file_names`, `ck_file_names`, `MAVEN_position`, `pxform`). The `FileFormat` vocabulary has no SPICE row, so `Other` is the only way to record a format that the package genuinely reads and that is central to what it does. |

**`FITS` was considered and rejected**, and the reason should stop it being re-proposed. IUVS files are
`.fits.gz` (`specification.py`: `formats["iuv"]["ext"] = "fits.gz"`) and `UPDATE.rst` documents an
IUVS download command, so FITS filenames are constructed and FITS files land on disk. But **nothing in
the package opens them**: there is no `astropy`, no `fitsio` and no FITS reader in the dependency list
or the source, and `load.py`'s own comment states its loader "Will NOT work for NGIMS, IUVS, and
ROSE". Field 18 says "Only formats actually supported should be indicated", and downloading a file
without being able to read it is not input support. The IUVS *instrument* association is still
recorded in Field 31, because retrieval and path resolution are real support for that instrument —
the two judgements are independent.

**`ISTP-Compliant` was considered and rejected.** The MAVEN Level-2 CDFs served by the LASP Science
Data Center do broadly follow ISTP conventions, but `read.read_cdf` is a generic reader: it enumerates
`cdf_info().zVariables` (or the caller's `field_names`) and pulls each variable, with a special case
only for a variable literally named `epoch`. It does not consult `DEPEND_0`, `CATDESC`, `LABLAXIS` or
any other ISTP attribute, so the package does not implement or depend on the convention.

**Rejected:** `HDF5`, `netCDF3/4`, `JSON`, `Zarr` — no reader, no dependency, no reference in the
source.

**Formats retrieved but not read, recorded so the distinction is not lost:** IUVS `.fits.gz` (above);
ACC Level-3 and ROSE Level-2/3 `.tab` PDS tables (`formats["acc"]["ext"] = "tab"`,
`formats["rse"]["ext"] = "tab"` — declared for retrieval, with no reader anywhere and `load.py`
explicitly excluding ROSE); and raw Particles and Fields Level-0 `.dat` telemetry
(`formats["pfp"]["ext"] = "dat"` — no parser exists).

---

### 19. Output File Formats (RECOMMENDED)

`ascii`

An addition to a previously empty field.

Three candidate outputs were examined; only the third is a file MavenPy itself writes as a product.
The first two are recorded here as the negative research, because both are easy to mistake for output
support in either direction.

1. **Byte-for-byte copies of remote archive files — written, but not a product of this software.**
   `retrieve.download_file(file_url, local_filename, ...)` streams the remote response to disk
   unchanged. The local file is in whatever format the archive served; the package neither chose nor
   produced that format, so it says nothing about what MavenPy can emit.
2. **Figures — not written at all.** Plots are rendered with matplotlib by the scripts and demos, but
   the one `savefig` call in the repository (`scripts/plot_sep.py` line 594) is commented out, so
   figure export is left entirely to the user's own matplotlib session. No image file is produced by
   the package.
3. **A solar-wind coverage table — this is the output format.** `scripts/find_sw_coverage.py` line 356
   defines `make_sw_coverage_file(save_dir, filename, sw_entry_utc, sw_exit_utc)`, which opens a file
   with a bare builtin `open(..., "w")`, writes the header line
   `Enter SW (YYYY-MM-DD HH:mm), Exit SW (YYYY-MM-DD HH:mm)` and then one line per interval carrying
   the solar-wind entry and exit times. It is user-facing and documented: the `--make_file` flag is
   registered at lines 513–518 with the help text "Make a file containing all the entry/exit times of
   s/c in solar wind." and acted on at lines 566–574, writing
   `maven_sw_coverage_{YYYYMMDD}to{YYYYMMDD}.dat` into the data directory. It is an interchange
   product rather than a debug dump: `read_sw_coverage_file` (line 368) parses the file back, and
   `make_sw_pass_ranges` (line 386) and `make_Carrington_sw_pass_ranges` (line 470) consume it.

**`ascii` rather than `csv` — a close call, stated honestly.** Structurally the file is CSV-shaped,
and that should not be understated: line 358 is
`header = "Enter SW (YYYY-MM-DD HH:mm), Exit SW (YYYY-MM-DD HH:mm)\n"`, a two-column comma-separated
column header, and each body row is a two-field `", ".join(...)`. A CSV reader would parse it.

`ascii` is chosen on three pieces of evidence about what the *author* treated the format as, rather
than about what a parser could do with it. First, the extension the code itself constructs is `.dat`
(`maven_sw_coverage_{YYYYMMDD}to{YYYYMMDD}.dat`, lines 566–574), not `.csv`. Second, the package's own
reader does not use a CSV parser: `read_sw_coverage_file` line 375 does a plain
`entry_i, exit_i = line.split(", ")` and strips the newline by hand; neither the `csv` module nor a
dataframe reader appears anywhere in the package. Third and most telling, the author demonstrably had a
comma-delimited parsing idiom already in hand and chose not to use it here: `mavenpy/ngims.py` line 203
reads genuine NGIMS CSV input with `np.loadtxt(filename, delimiter=',', skiprows=1, dtype=dtype_i)`
(and that input *is* recorded as `csv` in Field 18). The contrast between how he reads NGIMS CSV and
how he reads his own coverage file is the clearest statement available that he did not regard the
latter as a CSV interchange contract. It is a plain-text table that one function writes and one
function reads back, and `ascii` describes that without over-claiming.

*Live rejected alternative — `csv`.* Field 19 accepts multiple values, so `csv` could be recorded
alongside `ascii` rather than instead of it, and a reviewer who weighs the file's structure more
heavily than the author's chosen extension and hand-rolled reader could reasonably do so. That is a
defensible reading of the same evidence, not an error. It is left off here because the two signals
that reflect authorial intent both point away from CSV, and because `ascii` is true of the file under
either reading. `Other` is rejected in either case, since a listed row fits.

Rejected for want of any writer: `CDF`, `csv` (above), `FITS`, `HDF5`, `IDL.sav`, `ISTP-Compliant`,
`JSON`, `netCDF3/4`, `Zarr`. The read side of the package (`read.py`, `load.py`) has no writing
counterpart — data read from archives is returned as Python dictionaries of NumPy arrays for
in-session use and is not written back out.

**Negative-research search terms — a complete re-check of this field must cover all of these:** the
library-level serialization helpers (`savetxt`, `to_csv`, `np.save`, `pickle.dump`, `json.dump`,
`csv.writer`, `tofile`, CDF and `sav` writing) **and, critically, the plain builtins** — `.write(`,
`.writelines(`, and `open()` in every write mode and quote style (`"w"`, `'w'`, `'wb'`, `'a'`, `'x'`).
The builtins are what matter here: `make_sw_coverage_file` uses a bare `open` plus `fh.write`, so a
search restricted to serialization helpers misses it entirely and wrongly concludes the package writes
no data at all.

Run exhaustively over the pinned revision, that search returns exactly three writing sites, and all
three are accounted for above: `scripts/find_sw_coverage.py` lines 361 and 365 (the coverage table),
`mavenpy/retrieve.py` lines 799 and 803 (`open(temp_filename, 'wb')` and the chunked download write —
the byte-for-byte archive copy), and `mavenpy/retrieve.py` line 851, which is a `sys.stdout.write`
progress spinner and not a file at all.

---

### 20. Operating System (RECOMMENDED)

- Linux
- Mac

Both are additions to a previously empty field. This is the most weakly evidenced field in the
dossier after Field 12, and the reasoning below is deliberately explicit about which of the two values
rests on what.

What the repository actually establishes:

- There is no continuous-integration configuration at all — no `.github/workflows`, no `.travis.yml`,
  no `tox.ini` — so no operating system is *tested*.
- `setup.py` declares no `Operating System ::` classifier, and `README.rst` names no platform. Its only
  environment statement is "Depends on Python3.11 and above".
- The code contains no operating-system **branching**: `sys.platform`, `platform.system()` and
  `os.name` do not appear anywhere in the source, and there are no drive letters. Relative paths are
  built with `os.path` and URLs with `posixpath` (the correct choice for URLs, not a POSIX filesystem
  assumption).
- It does, however, carry **six live, uncommented hard-coded absolute macOS paths**, which is direct
  rather than circumstantial evidence of the development environment: `demo_mag.py` line 15
  (`/Users/rjolitz/DataFiles/data`); `scripts/plot_MAVEN_orbit.py` line 335
  (`/Users/rjolitz/DataFiles/from_others/Morschhauser_spc_dlat0.25_delon0.25_dalt5.sav`, reached
  whenever `--plot_b` is passed); `tests/verify_sep_read_calib.py` lines 208 and 209;
  `tests/sep_arc_v_svy.py` line 11; and `tests/rebin_swif.py` line 114. Two further `/Users/rjolitz/`
  paths are commented out, at `scripts/plot_sep.py` line 594 and `mavenpy/spice.py` line 81. These
  paths make `Mac` the best-evidenced value of the two.
- The remaining fingerprints are weaker and are recorded as such: the package mirrors the Berkeley SSL
  SPRG unix data tree and reads SPEDAS's `ROOT_DATA_DIR` convention. `#!/usr/bin/env python3` is not
  evidence here — it appears on exactly two trivial stubs (`main.py` and `mavenpy/main.py`) and on
  none of the six `scripts/` entry points.

`Mac` is directly evidenced by the developer paths above. `Linux` is the weaker of the two: it rests
on the unix data-tree conventions the package mirrors and on its dependencies being routinely
installed there, not on anything the repository states or tests. Together they record where the
package is evidently developed and used, not a tested support matrix.

**Rejected, with reasons.** `Windows` — left off rather than asserted. The repository neither claims
nor excludes it, and the concrete risk is the `spacepy` dependency: `mavenpy/read.py` line 11 imports
`from spacepy import pycdf` at module top level with no guard and no fallback, so any environment
where SpacePy will not install cannot import the package's reader module at all. A maintainer
statement, or a successful Windows install, would be enough to add this value.
`Operating System Independent` — rejected for the same reason plus a stronger one: it is a positive
claim of universal installability that nothing in the repository tests or asserts. `Solaris`,
`MobilePlatform`, `Other` — no basis.

---

### 21. CPU Architecture (RECOMMENDED)

`CPU Independent`

An addition to a previously empty field.

This is a statement about what **MavenPy itself** requires, and on that question the repository is
conclusive rather than silent: the package is pure Python. `setup.py` declares no `ext_modules`, there
are no C, Cython, Fortran or assembly sources in the tree, no build step beyond
`python -m pip install -e .`, and `setup.cfg` marks the wheel `universal = 1`. Nothing in the source
depends on word size, endianness or instruction set.

Caveat recorded for accuracy: the architectures a user can *actually* install on are determined by
MavenPy's ten declared dependencies (`setup.py` lines 9–20: `numpy`, `python-dateutil`, `spacepy`,
`cdflib>=1.3.3`, `scipy`, `matplotlib`, `spiceypy`, `requests`, `bs4`, `html5lib`), several of which
ship compiled wheels for a finite set of platforms. The repository pins no
architecture and says nothing about this, so `x86-64` and `Apple Silicon arm64` were considered and
rejected as inferences about the dependency closure rather than facts about this software.

---

### 22. Related Phenomena (OPTIONAL)

`Solar Wind`

An addition to a previously empty field.

Justified by implemented capability, not topic: `mars_shape_conics.solar_wind_indices` classifies
which spacecraft positions are in the undisturbed solar wind upstream of the Martian bow shock,
`scripts/find_sw_coverage.py` builds solar-wind coverage statistics from that classification over
Carrington rotations, `demo_solarwind.py` is one of three top-level demonstrations and is the one
`README.rst` tells new users to run to verify their install, and SWIA `onboardsvymom` solar-wind
moments are a supported product with a dedicated reader.

**Rejected, with reasons.** `Solar Flares` — EUV FISM-fitted irradiance and SEP fluxes will contain
flare signatures, but the package has no flare detection, identification or analysis code.
`Coronal Mass Ejections` — same reasoning; no CME-specific functionality, and MAVEN's CME science is
done with the general-purpose products MavenPy reads rather than with anything CME-aware in the
package. `Geomagnetic Storms`, `Coronal Heating`, `Solar Corona`, `X-ray emission` — not applicable.

**Vocabulary gap, recorded so the emptiness beyond `Solar Wind` is understood as correct.** The
phenomena MavenPy most directly supports — Martian atmospheric escape and sputtering, solar energetic
particle precipitation into the Martian atmosphere, proton aurora, crustal-field magnetic topology,
and ionospheric response at Mars — have **no rows** in the seven-value `Phenomena` vocabulary, which
is entirely Earth- and Sun-focused. Field 22 is a closed list and rejects unknown values, so those
phenomena are not recorded here. Where they are searchable at all, it is through the open Keywords
vocabulary (Field 16) and the region and instrument associations.

---

### 23. Development Status (RECOMMENDED)

`WIP`

An addition to a field that previously held no value.

repostatus.org defines WIP as "Initial development in progress; no stable, usable public release yet",
and every independent signal in the repository agrees:

- `README.rst` line 23 states, in the section a new user reads to install it: "This package is still
  in development."
- `setup.py` classifies it `"Development Status :: 3 - Alpha"`.
- The declared version is `0.0.0` and has never been incremented (Field 12).
- There are no git tags and no GitHub releases — no release has ever been cut.
- The package is not published to any index, and `setup.py` actively blocks PyPI registration and
  upload.
- Installation is by `git clone` plus `python -m pip install -e .`, the editable-install workflow of a
  package that is not distributed.

**`Active` was the serious alternative and is rejected.** It requires that the software has "reached
stable, usable state and being actively developed". Development is unquestionably active — 111 commits
with the most recent dated 2026-04-01, roughly 21 months after the initial commit — and that half of
the definition is met. The other half is contradicted by the repository's own words: the README and
the alpha classifier both deny a stable, usable public release. When repostatus terms conflict this
way, the release-maturity half is the discriminating one, since `WIP` exists precisely to describe
work that is active but pre-release.

**Also rejected.** `Concept` — far too weak for roughly 16,000 lines of working code with a functional
command-line interface, demos and tests. `Inactive`, `Abandoned`, `Suspended`, `Unsupported` — all
contradicted by commit activity through 2026-04-01. `Moved` — the move from Bitbucket to GitHub is
complete and the GitHub repository *is* the authoritative location, so this status would describe the
wrong direction.

---

### 24. Documentation (RECOMMENDED)

`https://github.com/rjolitz/mavenpy/blob/main/README.rst`

An addition; the stored value is empty.

There is no documentation site to point at, and that is established rather than assumed: the
repository has no `docs/` directory, no `.readthedocs.yml` or `conf.py`, no Sphinx configuration; the
GitHub API reports `has_pages: false` and an empty `homepage`; and no documentation URL appears in
`README.rst` or `setup.py`. Documentation lives entirely in two reStructuredText files at the
repository root.

`README.rst` is the right target of the two: it carries the installation instructions (the
"Development" section — clone, then `python -m pip install -e .`, then run `demo_solarwind.py` to
verify), the supported-data-product list, and worked "Running" examples for retrieval, file-path
resolution, loading and coordinate rotation. Field 24 asks for the "documentation link including
installation instructions", which is exactly this file.

The companion document is `https://github.com/rjolitz/mavenpy/blob/main/UPDATE.rst`, a per-instrument
reference of concrete `scripts/update.py` command lines for downloading SPICE kernels, EUV, SWIA,
SWEA, IUVS, LPW, SEP, MAG and NGIMS data. Field 24 accepts a single URL, so it is named here rather
than recorded as a value.

**Rejected alternatives.** The bare repository URL `https://github.com/rjolitz/mavenpy` — permitted by
the form ("If this is the same as the access URL, then enter that link here") but it would duplicate
Field 3 exactly and add no information; the direct README link at least identifies which document is
the documentation. `https://github.com/rjolitz/mavenpy#readme` — equivalent and branch-independent,
and a reasonable substitute if the `blob/main` path is judged too fragile. The residual risk in the
chosen value is that it embeds the branch name `main`, which is the current default branch; if the
default branch is ever renamed this link needs updating.

---

### 25. Funder (OPTIONAL)

**Not found.**

Negative research, recorded so it is not repeated: a case-insensitive search across every Python,
reStructuredText, configuration and YAML file in the repository for `fund`, `grant`, `award`,
`acknowledg`, and the NASA grant-number prefixes `NNX` and `80NSSC` returns **no matches**. There is
no funding statement, no acknowledgments section, no grant number and no sponsor logo anywhere at the
pinned revision. `README.rst` has no acknowledgments section beyond its thanks to the SPEDAS IDL
authors, which credits prior work rather than funding.

Inferring a funder from the author's institutional affiliation or from MAVEN mission funding would be
fabrication and is deliberately not done.

---

### 26. Award Title (OPTIONAL)

**Not found.** No award title and no award number exists in the repository — same negative research as
Field 25.

**A stored placeholder association was cleared, and the scope of that matters.** The record
previously carried one award entry whose name, identifier and funder were all empty — an artifact of the original submission rather than a value, since the
repository contains no funding or award strings at all.

The correction is a *detachment*, not a deletion. That empty award row is shared with other software
records, so clearing this field removes only MavenPy's association with it; the row itself persists for
those other records. No row is deleted and none needs to be — the defect being fixed is that MavenPy
pointed at an information-free placeholder, and pointing at nothing is the accurate state. A future
agent should not read this note as licence to delete the row, and should not expect the row to have
disappeared.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Not found.**

The repository designates no publications. Two categories were considered and rejected, and both
rejections are worth keeping because both are plausible things a later agent might propose:

1. **The author's MAVEN papers.** Rebecca Jolitz's ORCID profile lists a substantial MAVEN
   bibliography, and some of that work plausibly used this code. But no paper in it states that it
   used MavenPy, and the repository designates none of them. Selecting some subset would be a guess
   about which analyses used the package.
2. **The papers the code implements.** `mars_shape_conics.py` implements the Trotignon et al. (2006)
   bow shock and magnetic pileup boundary conic fits, `mag.read`'s docstring cites the MAVEN MAG
   Software Interface Specification document, and several routines name the SPEDAS `.pro` files they
   were ported from. These are sources MavenPy *uses*; Field 27 is for publications that "describe,
   cite, or use the software" — the relationship runs the wrong way.

---

### 28. Related Datasets (OPTIONAL)

**Not found.**

MavenPy supports a large number of MAVEN data products — `mavenpy/specification.py` enumerates levels,
dataset names, file extensions and archive sources for thirteen instrument keys — but the repository
provides **no dataset DOI and no `hpde.io` or PDS dataset identifier** for any of them. Field 28 asks
for a DOI or a full formal citation, and constructing either from instrument and level names alone
would be inventing identifiers rather than recording them.

The association these datasets represent is not lost: it is carried by the instrument and observatory
records in Fields 31 and 32, which resolve to persistent SPASE identifiers, and by the
`Observatory/Mission-specific` data source in Field 17. Should authoritative dataset identifiers
become available, this field is where they belong.

---

### 29. Related Software (OPTIONAL)

- `https://doi.org/10.5281/zenodo.15022990` — Space Physics Environment Data Analysis System (SPEDAS)
- `https://github.com/spedas/pyspedas` — PySPEDAS
- `https://github.com/AndrewAnnex/SpiceyPy` — SpiceyPy
- `https://github.com/spacepy/spacepy` — SpacePy
- `https://github.com/MAVENSDC/cdflib` — cdflib

**SPEDAS is carried over from the existing HSSI record and is strongly supported.** The stored related
item has the placeholder label `UNKNOWN` — an artifact of how the record was created, and one that is
not user-visible — but its identifier resolves to Zenodo record 15022990, SPEDAS v6.0 (concept DOI
`10.5281/zenodo.14919975`, MIT, Angelopoulos et al.). The relationship it encodes is exactly what
Field 29 is for: a predecessor the software is derived from. `README.rst` line 17 states MavenPy "is a
package heavily based on IDL programs in the Berkeley SSL tplot SPEDAS distribution that read and
analyze MAVEN spacecraft data", and individual modules name the specific routines they were ported
from — `mag.read` ("based on … the MAVEN SPEDAS routine 'mvn_mag_load.pro'"), `mars_shape_conics.py`
("Conic section fits based on maven_orbit_tplot.pro"), `spice.py` ("based on spice_file_source.pro"),
`moment_3d.H_alpha_moments` ("Adaptation of mvn_swia_protonalphamoms_minf.pro").
`file_path.get_IDL_data_dir` even reads SPEDAS's `ROOT_DATA_DIR` so the two can share a data directory.

*A considered alternative, not applied:* the stored identifier is SPEDAS's **version** DOI (v6.0). The
**concept** DOI `https://doi.org/10.5281/zenodo.14919975` is more durable, since it always resolves to
the latest version. Switching would be a marginal improvement to a correct submitted value, so the
submitted version DOI stands and the concept DOI is recorded here so the choice does not get churned
in a later pass. If a maintainer prefers the concept DOI, this note is the justification.

**PySPEDAS is here as a similar-purpose peer, on external evidence only.** Field 29 covers "software
that performs similar tasks", and PySPEDAS is the closest functional peer MavenPy has: it ships a
dedicated `pyspedas/projects/maven` subpackage with per-instrument loaders — `mag.py`, `euv.py`,
`lpw.py`, `iuv.py`, `sep.py`, `swea.py`, `swia.py`, `sta.py`, `ngi.py`, `rse.py` and `kp.py` — plus a
`download_files_utilities.py` that fetches from the same public and credentialed MAVEN Science Data
Center archives MavenPy targets — by a different access route, which is worth naming so a future agent
comparing URL roots does not conclude the overlap claim is wrong. MavenPy composes
`https://lasp.colorado.edu` (`mavenpy/retrieve.py` line 242) with the path roots
`("maven", "sdc", "team")` and `("maven", "sdc", "public")` (`mavenpy/specification.py` lines 327–330,
selected from `remote_options` at line 25) and then browses HTML directory indexes; PySPEDAS queries
the same Science Data Center through its REST search API at
`…/maven/sdc/service/files/api/v1/search/…`. Different route, same two sides of the same archive.
The instrument coverage is close to identical to MavenPy's, ROSE included. Both are Python tools for
retrieving and reading MAVEN instrument data, so a user evaluating one has a real interest in knowing
about the other. (Module names are cited rather than a file count, because PySPEDAS is an external
repository this record does not pin: a count would drift, whereas these per-instrument modules are its
stable public shape.)

State the limits of this association plainly, because they matter for how it should be maintained:
**there is no in-repo evidence connecting MavenPy and PySPEDAS.** PySPEDAS is not a dependency, is not
imported, and is not mentioned in `README.rst`, `UPDATE.rst`, `setup.py` or any docstring. MavenPy's
documented lineage is the *IDL* SPEDAS distribution, not its Python successor. This entry is therefore
a similar-purpose association inferred from what the two packages do, not a dependency claim and not an
interoperability claim — which is why it is deliberately **not** listed in Field 30.

**The three remaining additions are domain-specific dependencies that characterize the software** —
the test Field 29 sets for "important software dependencies", as opposed to merely present ones:

- **SpiceyPy** — the Python binding to NASA NAIF's SPICE toolkit. `mavenpy/spice.py` (1190 lines, the
  largest module in the package) is built entirely on it, and everything MavenPy knows about spacecraft
  position, attitude and coordinate frames flows through it. A package that ships a module this size
  around SPICE is characterized by that dependency.
- **SpacePy** — a heliophysics library, and a hard install requirement. `read.py` imports
  `from spacepy import pycdf` and `read_cdf(..., lib='spacepy')` selects it as one of two CDF backends;
  `tests/test_pycdf_v_cdflib.py` exists specifically to compare the two.
- **cdflib** — the default CDF backend (`read_cdf(..., lib='cdflib')`), pinned at `>=1.3.3` in
  `setup.py` for a specific reason recorded in `read.py`: "NaTs fixed as of 2025/01/15 in cdflib
  1.3.3." A version floor set to pick up a named upstream bug fix in epoch handling is evidence of a
  real, load-bearing relationship rather than an incidental import.

**Excluded, and why — this is the audit trail for the dependencies that did not make it.** `setup.py`
lists ten install requirements. `numpy`, `scipy`, `matplotlib`, `requests`, `python-dateutil`, `bs4`
(BeautifulSoup) and `html5lib` are all excluded from both Field 29 and Field 30. Each is generic
infrastructure — arrays, numerics, plotting, HTTP, date parsing, HTML parsing — and each would be
equally at home in a web application, a finance model or a biology pipeline. Listing them would say
nothing that is not equally true of most of the Python ecosystem. Note that being rejected here does
not relocate them to Field 30; the correct destination for all seven is neither field.

---

### 30. Interoperable Software (OPTIONAL)

- `https://doi.org/10.5281/zenodo.15022990` — Space Physics Environment Data Analysis System (SPEDAS)

An addition; the stored value is empty.

**This entry records a different relationship from the SPEDAS entry in Field 29, and both are
intentional.** Field 29 records that MavenPy is *derived from* SPEDAS. This field records that the two
*exchange data at runtime*, which is a separate, independently evidenced fact:

- `read.read_tplot(tplot_file_path, return_plot_parameters=True, verbose=None)` reads IDL SPEDAS
  `.tplot` save files, extracting the `dq` variable structure **and** the per-variable plot parameters,
  so the IDL figure can be reproduced in Python. `read.parse_tplot_plot_parameters` is a 137-line
  function dedicated to interpreting SPEDAS's plot-limit structures.
- `scripts/tohban.py` uses this in earnest: it downloads `mvn_ql_pfp_{yyyy}{mm}{dd}.tplot` quicklook
  files produced by the SPEDAS-based MAVEN pipeline from the Berkeley SSL server and rebuilds the
  panels in matplotlib.
- `specification.py` declares `.tplot` as a supported extension for EUV Level-0 and STATIC Level-3.
- `file_path.get_IDL_data_dir` resolves SPEDAS's `ROOT_DATA_DIR` — from the environment or by parsing
  an IDL startup file — so a single local archive can be shared between an IDL SPEDAS installation and
  MavenPy without duplicating downloads.

That is output from one tool imported into the other, plus a shared on-disk data layout: a
cross-language bridge to a named domain tool, which is the paradigm case Field 30 describes. It is
recorded with the same identifier the record already uses for SPEDAS, so the two fields resolve to one
software entity.

**Rejected, with reasons.**

- **PyTplot** — a natural-looking proposal that is wrong here, and worth recording so it is not made.
  MavenPy reads `.tplot` *files* with its own `scipy.io.readsav`-based parser; it does not import
  PyTplot, does not create or consume PyTplot/tplot variables in memory, and PyTplot appears nowhere in
  its dependencies. There is no exchange with that package.
- **PySPEDAS** — deliberately excluded *from this field* while being listed in Field 29. It is a
  genuine similar-purpose peer, but no exchange exists: MavenPy does not import it, produce data it
  consumes, or consume data it produces, and it appears in no dependency list or docstring. MavenPy's
  documented SPEDAS relationship is with the IDL distribution, which is what `README.rst` and the
  module docstrings name. Similar purpose is a Field 29 relationship; Field 30 needs a demonstrated
  exchange.
- **cdflib** and **SpacePy** — genuinely interchangeable CDF backends within MavenPy, which is real
  evidence, but the relationship is one of dependency and characterization rather than peer-tool
  exchange, so they are recorded in Field 29 and not duplicated here.
- **numpy, scipy, matplotlib, requests, python-dateutil, bs4, html5lib** — generic infrastructure;
  excluded for the reasons given under Field 29. "Runs in the same environment without errors" is a
  caveat on real interoperability, not a test that sharing a Python runtime satisfies.

---

### 31. Related Instruments (OPTIONAL)

Every entry below carries a `https://spase-metadata.org/` identifier, and each name is copied from its
matched vocabulary row. The stored value is empty, so all ten are additions.

| Instrument name (as in the vocabulary) | SPASE identifier |
|---|---|
| MAVEN Magnetometer, MAG, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/MAG |
| MAVEN Solar Energetic Particle, SEP, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/SEP |
| MAVEN Solar Wind Electron Analyzer, SWEA, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/SWEA |
| MAVEN Solar Wind Ion Analyzer, SWIA, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/SWIA |
| MAVEN Langmuir Probe and Waves, LPW, Extreme Ultraviolet Monitor, EUV, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/LPW/EUV |
| MAVEN Neutral Gas and Ion Mass Spectrometer, NGIMS, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/NGIMS |
| MAVEN Spacecraft Ephemeris Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/Ephemeris |
| MAVEN Langmuir Probe and Waves, LPW, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/LPW |
| MAVEN SupraThermal And Thermal Ion Composition, STATIC, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/STATIC |
| MAVEN Imaging Ultraviolet Spectrograph, IUVS, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/IUVS |

**Support tiers — the evidence behind each association.** Not every instrument is supported to the same
depth, and recording which is which is the point of this section.

*Full support (remote discovery, download, local path resolution, dedicated reader, and analysis):*

- **MAG** — `mavenpy/mag.py` (344 lines): `read` dispatches on extension across `.sts`, `.sav` and
  `.cdf`, with `read_sts`/`parse_sts`, `parse_sav`, `read_b_cdf`/`parse_b_cdf` and `doy_to_utc`.
  `specification.py` encodes the full MAG resolution and coordinate matrices (`mag_avail_res`,
  `mag_avail_coords`, `mag_coordinate_mapping`) for Level-1 and Level-2 across payload, planetocentric
  and Mars-solar-orbital frames. `README.rst`'s worked example is a MAG retrieve-load-rotate workflow.
  `tests/test_mag.py` (295 lines) benchmarks the readers.
- **SEP** — `mavenpy/sep.py` (782 lines: `read`, `read_raw`, `read_cal`, `read_anci`, `read_pad`,
  `uncertainty`), `mavenpy/sep_calib.py` (646 lines, the raw→FTO→calibrated chain) and
  `mavenpy/sep_anc.py` (303 lines, sensor field-of-view geometry). `scripts/plot_sep.py` is a
  dedicated plotting tool and `README.rst` gives its command line as the first example.
- **SWEA** — `mavenpy/swea.py` (`read` for `svyspec`/`svypad`/`arcpad`/`svy3d`/`arc3d`, `read_scpot`)
  and `mavenpy/swea_topo.py` (Level-3 magnetic topology, `swe_topo_matrix`,
  `read_swea_l3_swia_regid`, `read_swea_l3_topo_parameters`).
- **SWIA** — `mavenpy/swia.py` (`read`, `process`, and `uncompress` for the onboard-compressed 3D
  distributions), feeding the moment calculations in `moment_1d.py` and `moment_3d.py`.
  `tests/test_swia.py` and `tests/rebin_swif.py` exercise it.
- **EUV** (the LPW Extreme Ultraviolet Monitor) — `mavenpy/euv.py` reads Level-2 bands and Level-3
  FISM-fitted spectra from CDF and `.tplot`; `scripts/plot_euv.py` is a dedicated plotting tool.
  Mapped to the SPASE `LPW/EUV` row because SPASE models the MAVEN EUV monitor as a component of LPW,
  which is also how the mission describes it.
- **NGIMS** — `mavenpy/ngims.py` (394 lines: `read`, `select`, `resample`, `orbit_average`,
  `filename_to_datatype`, `tstring_to_dt`), with `tests/test_ngims.py`. Note this instrument is one
  `load.py` excludes from its generic loader while still having a full dedicated reader.
- **Spacecraft Ephemeris** — `mavenpy/anc.py` (698 lines) reads monthly spacecraft ephemeris `.sav`
  files and NAIF `.orb` orbit files (`read_spacecraft_ephemeris`, `read_orbit_ephemeris`, `read_orb`,
  `orbit_num`, `segment_orbit`, `add_orbit_axis`), and `mavenpy/spice.py` computes positions from SPK
  kernels. SPASE models MAVEN ephemeris as an instrument resource, and MavenPy supports it at the same
  depth as any instrument.

*Retrieval and path-resolution support (no reader):*

- **LPW** — `specification.py` declares Level-2 (`lpiv`, `lpnt`, `mrgscpot`, `wn`, `we12` and the
  wave/spectra products) and Level-0b datasets with their archive sources; `UPDATE.rst` documents three
  concrete LPW download commands (density and temperatures, IV curve, passive spectra). MavenPy is the
  tool that fetches and organizes these files, which is real designed-to-support behaviour even though
  it does not parse them.
- **STATIC** — one of the most detailed instrument specifications in the file: the fourteen application
  identifiers in `sta_appids`, the six calibrated identifiers in `sta_calib_ids`, the `iv1`–`iv4`
  calibration levels, and the Level-3 density/temperature short-name mapping and filename template
  (`sta_l3_name`, `sta_iv_name`). `scripts/tohban.py` additionally labels STATIC C0 energy and C6 mass
  panels when replaying quicklook files.
- **IUVS** — an extensive specification covering levels `l1b`/`l1c`/`l2`, the corona/disk/echelle/limb/
  occultation datasets, far- and mid-ultraviolet and echelle imaging modes, and the orbit-segment
  vocabulary (`apoapse`, `periapse`, `inlimb`, `outlimb`, `incorona`, and the rest), plus dedicated
  filename templates. `UPDATE.rst` documents an IUVS download command and records the operational
  advice that "The level 2 files are generally filled with NaNs, so best to download the L1cs."

**IUVS — how the two candidate rows were resolved.** The vocabulary contains two rows for this one
instrument: `https://spase-metadata.org/SMWG/Instrument/MAVEN/IUVS` named "MAVEN Imaging Ultraviolet
Spectrograph, IUVS, Instrument", and `https://spase-metadata.org/SMWG/Instrument/MAVEN/IUVS.html`
named "MAVEN Imaging Ultraviolet Spectrograph (IUVS)". This is the known bare-versus-`.html`
duplication of a single SPASE resource, not two distinct entities, so it is not an ambiguity requiring
manual resolution. The bare identifier is selected, per the rule that the two forms are one resource
and the non-`.html` row is preferred. Two further points support it independently: the bare row's name
follows the "MAVEN <long name>, <abbreviation>, Instrument" pattern shared by the other MAVEN SMWG
instrument rows used here, and choosing it keeps every MAVEN instrument in this record within one
naming family.

**The CNES/CDPP-AMDA rows were considered and rejected.** A parallel family exists under
`https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MAVEN/` with rows for EUV ("Extreme UltraViolet
Monitor"), MAG ("Fluxgate magnetometer"), LPW, NGIMS, SEP, SWEA, SWIA, STATIC, Ephemeris ("MAVEN
Orbit") and a crustal-field model set ("MAVEN : Mars crustal magnetic field analytical models"). All
were rejected for three converging reasons: they are the AMDA data service's own descriptions of MAVEN
parameters rather than the mission's canonical instrument records, so `SMWG` wins the tie-break;
MavenPy does not use AMDA as a data source (its remotes are the LASP Science Data Center public and
team areas, the Berkeley SSL SPRG tree and NAIF, per Field 17); and the SMWG family already covers
every instrument MavenPy supports, so mixing families would split single entities across two
identifiers and defeat de-duplication. The crustal-field "Models" row is additionally not an instrument
at all.

**Documented omissions — three instruments MavenPy supports that have no SPASE resource.** These are
omissions, not oversights, and the check behind them was direct:

- **ACC (Accelerometer)** — `specification.py` declares `formats["acc"]` with Level-3 `.tab` files,
  the `pro-acc-p(.*)` dataset pattern and the Berkeley SSL SPRG source, and `file_per_orbit` includes
  `"acc"`. `https://spase-metadata.org/SMWG/Instrument/MAVEN/ACC` returns HTTP 404, as does
  `.../MAVEN/Accelerometer`. No row exists in the vocabulary. The instrument-to-observatory fallback is
  not applied, because the MAVEN observatory is already recorded in Field 32 and adding it again would
  be a no-op.
- **ROSE / RSE (Radio Occultation Science Experiment)** — `formats["rse"]` declares Level-2
  (`dlf`, `fup`, `sky`) and Level-3 (`edp`) `.tab` products from the LASP Science Data Center.
  `https://spase-metadata.org/SMWG/Instrument/MAVEN/ROSE` and `.../MAVEN/RSE` both return HTTP 404.
- **PFP (Particles and Fields Package, raw Level-0)** — `formats["pfp"]` declares Level-0 `.dat`
  telemetry (`all`, `arc`, `svy`) from SSL SPRG and the LASP team area.
  `https://spase-metadata.org/SMWG/Instrument/MAVEN/PFP` returns HTTP 404. Independently of the missing
  resource, PFP is an instrument *package* rather than a single instrument, and its constituent
  instruments — SWEA, SWIA, STATIC, SEP, MAG and LPW — are each already listed above, so the science
  association is not lost.

A note on why these three are recorded as omissions rather than dropped silently: the SPASE registry
directory `https://spase-metadata.org/SMWG/Instrument/MAVEN/` resolves for exactly `Ephemeris`, `IUVS`,
`LPW`, `LPW/EUV`, `MAG`, `NGIMS`, `SEP`, `STATIC`, `SWEA` and `SWIA`. If the registry later gains ACC,
ROSE or PFP resources, these three become straightforward additions and this note is the evidence that
they belong.

**Relevance gate — what was excluded.** No instrument outside the MAVEN payload is listed. MavenPy
downloads SPICE kernels from NAIF for planetary bodies and for MAVEN, but a kernel archive is not an
instrument. The `plot_MAVEN_orbit.py` crustal-field map is drawn from a locally supplied `.sav` file
rather than from a named instrument's data product.

---

### 32. Related Observatories (OPTIONAL)

| Observatory name (as in the vocabulary) | SPASE identifier |
|---|---|
| Mars Atmosphere and Volatile EvolutioN | https://spase-metadata.org/SMWG/Observatory/MAVEN |

Carried over unchanged from the existing HSSI record, and independently re-confirmed as the correct
canonical row: observatory type, SMWG family, bare identifier with no `.html` variant. The name is
copied from the row as stored.

The association could hardly be better supported — the entire package is a MAVEN mission data client,
from the Mars orbit insertion date and safe-mode intervals encoded in `specification.py` to the
mission-specific archive layouts, the `MAVEN_MSO` frame, and the `mvn_*` filename conventions
throughout.

**Rejected duplicate.** `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/MAVEN`, named "Mars
Atmosphere and Volatile Evolution Mission", is the same mission under the AMDA data service's family.
`SMWG` is preferred as the canonical family among same-entity duplicates, consistent with the
instrument choices in Field 31, and MavenPy does not use AMDA as a data source.

**No other observatory is listed**, and that is deliberate: MavenPy reads no other mission's data. The
NAIF SPICE archive it downloads from is a kernel repository, not an observatory, and the generic
archive access it performs is recorded in Field 17.

---

### 33. Logo (OPTIONAL)

**Not found.**

Negative research: there is no image file of any kind in the repository (the full file listing at the
pinned revision contains only Python sources, `README.rst`, `UPDATE.rst`, `LICENSE`, `data_info.yaml`,
`setup.py`, `setup.cfg`, `.gitignore` and an empty `test.txt`). `README.rst` embeds no image directive
and carries no badges. The GitHub repository has no social preview or organization avatar of its own —
it is a personal-account repository. MavenPy is not registered in any of the three PyHC project
registries, so no curated logo URL is available from there either.

---

## Cross-cutting notes

**PyHC registry status.** All three PyHC registry files — core, community and unevaluated — were read
in full and checked by project name, repository URL and description. MavenPy appears in none of them,
so no curated PyHC metadata (logo, documentation URL, curated keywords, maturity ratings) is available
to supplement this record. Absence from PyHC is not a defect; it simply means the community-curated
source that improves many HSSI records does not apply here.

**Four registry entries mention MAVEN and none of them is this software.** Two are confusable with it
because of where they are hosted: `CDFlib` and `PyTplot`, both in the community list, live under the
`MAVENSDC` GitHub organization, but they are LASP Science Data Center products rather than
MAVEN-specific analysis tools. Two more carry `maven` as a curated keyword: `pySPEDAS` in the core list
and `PyRFU` in the community list. (The entries are named rather than cited by line number, because the
registry files are live external documents this record does not pin and their line numbers drift.)

Of the four, pySPEDAS is the similar-purpose *peer* and is recorded as such in Field 29. cdflib also
appears in Field 29, but as a characterizing dependency rather than a peer — a different relationship,
not a lesser one. PyRFU lists `maven` among many mission keywords yet is a general multi-mission
analysis package rather than a MAVEN-focused loader, and PyTplot is a time-series plotting library;
neither name appears anywhere in MavenPy's source or documentation, and neither is recorded in this
dossier.
