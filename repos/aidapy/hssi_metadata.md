# HSSI Metadata Extraction Results

**HSSI Software ID:** b5742bb7-4c8e-45cd-9429-65cb75f32795
**Repository:** https://gitlab.com/aidaspace/aidapy
**Source Revision:** d023f091a9cdf07fb48f232b654a4e15913b668c
**Extraction Date:** 2026-08-27
**Validation Date:** 2026-08-27
**Validation Status:** PASS

---

**Scope note — read this before using the evidence below.** Repository claims in this file are pinned
to the source revision above — the final commit on `master` at
`https://gitlab.com/aidaspace/aidapy` (2021-09-14, commit message "version 0.1.0") — except where a
claim is explicitly about the project's branches or its GitLab activity record, as in the rest of this
note and in Field 23. The project had 22 remote branches when this record was compiled (2026-08-27),
several of which carry substantial later work (`notebooks_merge_dev` through 2022-03-03, `WP4_update`
through 2022-02-08, `develop` through 2022-02-23) that was **not merged into `master`**.
Capabilities that exist only on those branches — notably a `wave_identification` module,
a parallel toolbox, an iRODS example, a VAE use case and mutual-information methods — are therefore
*not* part of the software this record describes, and are recorded below as documented absences so a
future agent does not credit AIDApy with them from a branch listing or a documentation page built
from a branch.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Note:** The submitter identifies the person entering the metadata, not an author of the software.
Placeholders here are the catalogue convention for a record maintained on the software's behalf.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** Not found

**Evidence of absence.** The repository at the pinned revision contains no `CITATION.cff`,
`codemeta.json`, `.zenodo.json`, `AUTHORS` or `CONTRIBUTORS` file, and `README.rst` carries no DOI
badge — its badge block advertises only licence, GitLab pipeline, PyPI, Codecov, Pylint, Sphinx and a
"Maintained?" shield. Negative research against the two registries most likely to hold a software DOI
returned nothing: a Zenodo record search for `aidapy` returns zero hits, and a DataCite DOI search
for `aidapy` returns `meta.total = 0`. AIDApy is distributed through PyPI only, and PyPI does not
mint DOIs.

This is a genuine gap in the software's own metadata rather than a gap in this record. If the
maintainers ever archive a release to Zenodo, the concept DOI belongs here and the version DOI in
Field 12.

### 3. Code Repository (MANDATORY)
**Value:** https://gitlab.com/aidaspace/aidapy

**Source.** The canonical repository, confirmed as the project's `web_url` by GitLab's project API for
`aidaspace/aidapy` and stated in `README.rst` ("The sources are located on **GitLab**"). This is a
GitLab project, not GitHub — GitHub API routes do not resolve for it, and release/tag facts in this
file come from `https://gitlab.com/api/v4/projects/aidaspace%2Faidapy/...`.

The same URL is what the external literature points readers to: the Acknowledgments footnotes of
Breuillard et al. (2020), `https://doi.org/10.3389/fspas.2020.00055`, resolve "aidapy" to
`https://gitlab.com/aidaspace/aidapy`.

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Coordinate Transforms: Magnetospheric
- Coordinate Transforms: Mission-Specific
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: 3D Particle Distribution Processing
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Curlometer
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: ML/AI
- Data Processing and Analysis: Pitch Angle Distributions
- Data Processing and Analysis: Plasma Moments
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Wavelet Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: ML/AI
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Forecasting
- Models and Simulations: ML/AI
- Models and Simulations: Theory

**Why these values.** AIDApy's four documented subpackages (`README.rst`: "Mission tool, Event search
tool, Velocity distribution function tool, Machine learning tool") span data retrieval, in-situ plasma
analysis, velocity-space processing, plotting and machine-learning modelling. Each value below is tied
to a specific artifact at the pinned revision.

*Coordinate Transforms* (with `Magnetospheric` and `Mission-Specific`). `aidapy/aidaxr/vdf.py`
builds and applies rotation matrices between four frames: Earth-Centred Inertial and Geocentric Solar
Ecliptic (`_init_rotations_matrices` sets `R_eci_to_gse` / `R_gse_to_eci` from MMS attitude
quaternions), the MMS **DBCS** instrument frame (`R_eci_to_dbcs`, from
`sc_att` = `mms${probe}_mec_quat_eci_to_${frame}` with `'frame':'dbcs'`), and a magnetic-field-aligned
frame (`_init_R_b_to_dbcs`). GSE is the user-selectable coordinate system across the whole Mission
tool (`'coords': 'gse'`), which supports `Magnetospheric`; DBCS is an MMS-specific spacecraft frame,
which supports `Mission-Specific`. The transforms are user-facing: `aidapy.tools.vdf_utils` exports
`spher2cart`, `cart2spher`, `cyl2cart`, `cart2cyl`, `R_2vect`, `Rx`, `Ry`, `Rz` as module-level
functions, and the `frame` keyword of the `vdf` accessor's `interpolate()` selects the target frame
(the 0.0.4 changelog entry documents the `'B_electron'` frame as a user-selectable value).
`Coordinate Transforms: Heliospheric`, `: Ionospheric`, `: Planetary` and `: Solar` were considered
and rejected — no heliospheric, ionospheric, planetary or solar coordinate system appears at the
pinned revision.

*Data Processing and Analysis.*
- `Data Access and Retrieval` — `aidapy.load_data` and `aidapy.aidafunc.get_mission_info` download and
  load OMNI, MMS and Cluster products; `aidapy/data/mission/modified_cluster.py` issues requests to
  the Cluster Science Archive (`csa_url = 'https://csa.esac.esa.int/csa/aio/product-action?'`).
- `Analysis` — the `statistics` accessor (`sfunc` structure functions, `mean`, `std`, `psd`,
  `autocorr`), the `xevents` accessor (`increm` increments and kurtosis, `pvi` Partial Variance of
  Increments, `threshold`), `aidapy/aidaxr/epsilon.py`'s `epsilon()` non-Maxwellianity parameter, and
  `aidapy/aidaxr/hankel.py`'s spectral Hankel decomposition, described in
  `doc/source/energetic_particles.rst` as "a refined analysis, based on the spectral Hankel
  decomposition, in order to detect high energy particles and the process of entropy cascade in the
  velocity space".
- `Time Series Analysis` — the `statistics` accessor operates on xarray time series with rolling
  windows; `doc/source/extreme_events.rst` documents `autocorr` as computing the autocorrelation
  scale, "the scale at which the autocorrelation function decays to a value *1/e*", which "represents
  in turbulence the typical energy containg scale".
- `ML/AI` — `aidapy/ml/` provides UNet segmentation (`models/unet.py`), LSTM (`models/lstm.py`), a
  deep CNN (`models/dcnn.py`), a multilayer perceptron (`models/multilayer_perceptron.py`), K-means
  (`models/kmeans.py`), hyper-parameter optimisation (`hpo_optuna.py`) and pruning/quantisation
  (`optimizations/`); `aidapy/external/unsupmr/` adds K-means and DBSCAN clustering of plasma
  simulation data.
- `3D Particle Distribution Processing` — `aidapy/aidaxr/vdf.py` interpolates measured 3D velocity
  distribution functions onto spherical or Cartesian grids-of-interest
  (`_interpolate_spher_mms`, `_transform_grid`), and `aidapy/tools/vdf_utils.py` provides the grid and
  rotation machinery.
- `Plasma Moments` — `aidapy/aidaxr/epsilon.py` computes density and velocity moments
  (`compute_rho_vv`) and temperature (`compute_temp`) by integrating a distribution function, with
  `integrate_mms_th_phi` performing the angular integration of MMS distributions.
- `Energy Spectra` — the Mission tool exposes `i_omniflux` ("Ion omnidirectional energy spectrum") and
  `i_energy` ("Ion energy channels table") in `aidapy/data/mission/mission_settings/mms.json`, and the
  Hankel routines decompose 1D VDFs in energy/velocity space.
- `Curlometer` — `aidapy/aidaxr/process.py` implements `j_curl()` and `curl_b(b1, b2, b3, b4, r1, r2,
  r3, r4)`; `doc/source/mission.rst` lists `j_curl` as a Level-3 product, "Current density calculated
  from the Curlometer method", for MMS and Cluster.
- `Image Processing` — `aidapy/ml/data/coronalholes.py` reads image files with `cv2.imread` and
  applies `albumentations` resize/flip transforms; `aidapy/ml/data/ch_unsuper.py` prepares "contoured
  image for KMeans Processing"; the UNet produces segmentation masks.
- `Pitch Angle Distributions` — `aidapy/tools/vdf_plot.py`'s `spher_time()` averages the interpolated
  distribution over velocity bins into `pad` and titles the result "Spherical coordinate system,
  scaled pitch-angle distribution"; `profiles_1d()` extracts parallel, anti-parallel and perpendicular
  profiles.
- `2D Slices` — the 0.0.4 changelog entry documents "New plots for VDF: xy_plane(): cut in
  (v_perp_1, v_perp_2) plane" and `spher_gyro()` giving "a cut through the (v_perp, v_perp)-plane, and
  four sectors of (v_para, v_perp) to diagnose gyrotropy" — 2D cross-sections extracted from the
  interpolated 3D velocity-space volume.
- `Spectrogram` and `Wavelet Analysis` — `statistics.psdwt()` "Returns the wavelet transform of a
  timeseries" using `scipy.signal.cwt`, producing an xarray with dims `(time, scale)`. That is both a
  wavelet analysis and a time-frequency array, so both values apply.
- `Processing` — the accessor named `process` provides unit conversion (`convert`), timestamp
  reindexing/resampling (`reindex_ds_timestamps`), and the derived L3 quantities `plasma_beta` and
  `elev_angle`.

*Data Visualization.*
- `2D Graphics` — `aidapy/tools/vdf_plot.py` renders distributions with `contourf`/`pcolormesh` plus
  overlaid `contour` levels.
- `Line Plots` — `graphical.peek()` on the `graphical` accessor;
  `aidapy/aidafunc/event_search.py:plot_dataset()` line-plots each data variable and shades the
  detected event intervals; `aidapy/ml/visualization/dst_vis.py` plots Dst truth against prediction.
- `2D Slices` — the `xy_plane` and gyrotropy-sector views above are rendered, not merely computed.
- `ML/AI` — `aidapy/ml/visualization/visualizer.py` writes the model graph, losses, metrics and
  validation images to TensorBoard via `SummaryWriter`; `aidapy/ml/callbacks/grids/` builds image
  grids for segmentation and forecasting outputs; `README.rst` lists "Visualization and logging of the
  training/validation procedure" as a package feature.
- `Mission-Specific` — the VDF plotting suite is built around MMS FPI distribution geometry
  (`_interpolate_spher_mms`, `integrate_mms_th_phi`, `aidapy/aidaxr/tests/test_vdf_mms.py`), producing
  views specific to that mission's data type rather than generic 2D plots. This is a judgement call,
  settled in favour of the value: the plots are general in form, but their input geometry and their
  tests are MMS-specific, so a user looking for MMS distribution plotting should reach AIDApy through
  this value.

*Models and Simulations.*
- `ML/AI` and `Forecasting` — the Dst-index use cases train LSTM, MLP and DCNN regressors to predict
  Dst at a forecast horizon; `dst_vis.py` titles its figure `'Forecasting horizon t+{}h'`, and
  `examples/05_omni_regressor_lstm/config_omni_web.yml` configures the training run.
- `Data Guided` — those models are driven by observational input: the same config downloads OMNI
  features `['DST', 'F', 'BZ_GSM', 'N', 'V']` over `['2001-01-13 23:00:00', '2016-01-01 00:00:00']`.
- `Theory` — `aidapy/aidaxr/epsilon.py` generates analytic distributions from first principles:
  `compute_synth_maxw_1D/2D/3D` and `comp_Kdistr`, documented in
  `doc/source/energetic_particles.rst` as calculating "the Maxwell-Boltzmann distribution for given
  density, mean velocity and temperature" and the kappa distribution. These synthetic distributions
  are what `epsilon()` compares measurements against. The value is settled on that evidence. The
  narrower reading — that this subcategory covers simulation rather than analytical calculation — was
  considered and not adopted: `Theory` is the taxonomy's own term for analytical and theoretical
  calculation, and closed-form Maxwellian and kappa distributions generated from given moments are
  exactly that.

**Considered and rejected.**
- **`Mission-related` and all its subcategories.** `aidapy/tools/sitl_parsing.py` parses MMS
  Scientist-In-The-Loop reports into region labels, and Breuillard et al. (2020) footnote 3 points at
  an AIDA notebook for SITL region classification. That is post-hoc science analysis of a published
  operations product, not participation in the MMS ground system, so the taxonomy's distinction puts
  it under `Data Processing and Analysis`. AIDApy is not a mission ground-segment tool.
- **`Data Processing and Analysis: File Format Conversion`.** AIDApy reads CDF files into in-memory
  xarray objects; it does not convert one file format into another on disk. The previous version of
  this record justified the value with "setup.py classifiers mention file format conversion" — that is
  factually wrong. `setup.py` lists `Topic :: Scientific/Engineering :: Information Analysis` and four
  sibling topics; no classifier mentions file-format conversion. (Separately, the keyword is spelled
  `classifier=` rather than `classifiers=` in `setup.py`, so setuptools ignores the block entirely and
  PyPI reports `classifiers = []` for both published releases — the classifier list is not evidence for
  any field.)
- **`Data Processing and Analysis: Data Assimilation`.** `doc/source/getting_started.rst` describes
  AIDApy as using "modern techniques including data assimilation, machine learning (ML), artificial
  intelligence (AI), and advanced statistical models". No assimilation algorithm is implemented at the
  pinned revision; the sentence is a statement of project ambition. Do not re-derive this value from
  that page.
- **`Data Processing and Analysis: Wave Polarization Analysis`.** A `wave_identification` module and
  its documentation exist only on the unmerged `WP4_update` branch (commits dated 2021-12 to 2022-02),
  after the pinned revision. Not part of this release.
- **`Data Processing and Analysis: Linear Gradient Estimation`.** The reciprocal-vector gradient
  machinery exists only inside `curl_b` as the curlometer implementation; there is no separate
  gradient-estimation API, and `Curlometer` already carries it.
- **`Data Processing and Analysis: Data Reduction`.** `reindex_ds_timestamps(sample_freq)` aligns
  products onto a common cadence and `vdf.py:_time_average` averages distributions over time, but
  neither is presented as a data-volume-reduction capability. Rejected to avoid over-classification.
  The opposite reading — that resampling and time-averaging are data reduction — is available on the
  same evidence and was not taken; this value is settled as rejected.
- **`Data Processing and Analysis: Calibration`.** AIDApy consumes Level-2 calibrated products
  (`_l2` CDF keys throughout `mission_settings/mms.json`) and performs no calibration.
- **`Data Visualization: Spectrogram`.** `psd` and `psdwt` return xarray objects for the user to plot;
  no spectrogram-rendering routine ships at the pinned revision. `spher_time()` renders time against
  pitch angle, which is not a time–frequency spectrogram. This value was claimed by the previous
  version of this record and is removed as unsupported.
- **`Data Visualization: Web-Based`.** `plotly` is declared as a dependency only — `setup.py`'s `ml`
  extra and `requirements.txt`'s `plotly==4.13.0` — and is imported nowhere in the package.
- **`Data Visualization: 3D Graphics`, `: Movies`, `: Hodograms`, `: Orbit Plots`,
  `: Spacecraft Formation Plots`.** No `mplot3d`, `Axes3D`, `mayavi`, `vtk`, `pyvista`,
  `matplotlib.animation` or `FuncAnimation` usage exists in the package; spacecraft position is loaded
  as a product (`sc_pos`) and used in event-search criteria but never plotted as a trajectory or
  formation.
- **`Models and Simulations: Empirical`, `: First Principles`, `: MHD`, `: Physics-Based`,
  `: Forward-Fitting`.** AIDApy analyses particle-in-cell simulation output (the double Harris sheet
  case in `examples/03_gmm/`) but runs no simulation of its own, and `epsilon()` compares a measured
  distribution against a synthetic Maxwellian carrying the same moments — there is no parameter
  optimisation, so `Forward-Fitting` does not apply.
- **`Servers and Environments` and all its subcategories.** `mpi4py` is imported only by
  `examples/03_gmm/reconnection_harris/mpi_script.py`, an example script, and is not declared in
  `install_requires` or any extra; the repository contains no Dockerfile, Singularity definition or
  deployment manifest.

**What this refresh replaced.** Until this refresh the stored record carried three values — the
bare top-level `Data Processing and Analysis`, `Data Visualization` and `Models and Simulations`,
with no subcategory under any of them. All three are retained. The other 26 values were added by this
refresh: 23 subcategories under those three existing parents (14 under Data Processing and Analysis,
5 under Data Visualization, 4 under Models and Simulations), plus a `Coordinate Transforms`
top-level branch, with two subcategories, that the record did not carry at all.

### 5. Related Region (MANDATORY)
**Values:**
- Corona
- Earth Magnetosheath
- Earth Magnetosphere
- Earth Magnetotail
- Earth Outer Magnetosphere
- Interplanetary Space
- Solar Environment
- Solar Wind

**How each was decided.** The Region vocabulary is flat — no row is a parent or child of any other —
so each value is judged on its own evidence and a coarse value never implies a fine one.

- **Earth Magnetosphere** — the Mission tool serves MMS and Cluster in-situ magnetospheric data;
  `aidapy/tools/sitl_parsing.py` emits a `MAGNETOSPHERE` label as one of the ten classes in its
  `generate_location_dict()` classifier (the module also has a second, five-class
  `generate_event_dict()` classifier, and `read_and_transform(file_name, category=...)` selects
  between them).
- **Earth Magnetotail** — `event_search(settings='df')` searches for dipolarization fronts with an
  explicit tail-location criterion, `(np.all(sc_pos_x <= -5 * 6378)) & (np.all(np.abs(sc_pos_y) <= 15
  * 6378))` in `aidapy/aidafunc/event_search.py:_settings_df`, i.e. X <= -5 Earth radii and |Y| <= 15
  Earth radii; `doc/source/event_search.rst` works the same criterion through as its illustrative
  example, "to ensure that one spacecraft from a fleet is in the Earth's magnetotail". `sitl_parsing`
  carries a dedicated `MAGNETOTAIL` class whose terms include bursty bulk flows and dipolarization
  fronts, and its event classifier adds `DIPOLARIZATION_FRONT`, `BURSTY_BULK_FLOW`, `PLASMA_JET`,
  `FLUX_ROPES` and `PLASMA_FLOWS`, all magnetotail phenomena.
  Externally corroborated: Alqeeq et al. (2022), `https://doi.org/10.5194/egusphere-egu22-9532`,
  state that "Criteria for selecting DF using an AIDApy routine are based on difference of maximum and
  minimum values computed with a 306 s sliding window" for dipolarization fronts "near the Earth's
  magnetotail equator".
- **Earth Magnetosheath** — `sitl_parsing` carries a dedicated `MAGNETOSHEATH` class built from 28
  literal spelling variants plus six abbreviation expansions, making it a first-class output category
  of that module.
- **Earth Outer Magnetosphere** — `sitl_parsing` carries dedicated `MAGNETOPAUSE`, `BOUNDARY_LAYER`
  (including `LLBL`) and `PSBL` (including `lobe` and `Mantle`) classes, and
  `event_search(settings='edr')` targets electron diffusion regions, the reconnection sites found at
  the magnetopause and in the tail current sheet.
- **Interplanetary Space** — the OMNI mission module retrieves near-Earth interplanetary field and
  plasma parameters (`aidapy/data/mission/mission_settings/omni.json` includes `IMF`, `BX_GSE`, `V`,
  `N`, `T`, `Pressure`, `Mach_num`).
- **Solar Wind** — `sitl_parsing` carries a dedicated `SOLAR_WIND` class (including "interplanetary
  shock" and IMF terms), and the OMNI product set is a solar-wind parameter set. This is a separate
  flat row from `Interplanetary Space` and both apply on their own evidence.
- **Corona** — `examples/04_coronal_holes/README.rst` is titled "Coronal Holes segmentation in SDO
  images" and ships six configuration files plus a trained checkpoint
  (`aidapy/ml/models/tests/CH/model_best.pt`) for a UNet that segments coronal holes; `README.rst`
  advertises "the automatically detection of coronal holes in SDO images" as a headline use case.
  Coronal holes are structures of the solar corona, so the specific `Corona` row applies, not only the
  broad `Solar Environment` row.
- **Solar Environment** — retained from the stored record on the same coronal-hole evidence; it is the
  broad solar row and, because the vocabulary is flat, it must be listed explicitly rather than
  inferred from `Corona`.

**Considered and rejected.**
- **Earth Inner Magnetosphere** — `sitl_parsing`'s `MAGNETOSPHERE` class folds in inner-magnetosphere
  terms (`plasmapause`, `Radiation belt`, `plasmasphere`, `EMIC`, `Microinjections`) as synonyms of a
  single generic label. No AIDApy analysis targets the inner magnetosphere as such, and a user
  searching for inner-magnetosphere software would not be well served. Rejected on the strength of the
  evidence, not on principle — if a future release adds an inner-magnetosphere product or criterion,
  revisit.
- **Chromosphere, Photosphere, Solar Interior** — the coronal-hole imagery is coronal; no
  chromospheric, photospheric or helioseismic capability exists.
- **Earth Atmosphere, Earth Lower and Middle Atmosphere, Earth Thermosphere, Earth Ionosphere,
  Earth Auroral Subregion** — no atmospheric, ionospheric or auroral data product, model or example.
- **Heliosheath** — no outer-heliosphere capability.
- **Jupiter / Mars / Neptune / Saturn / Uranus Magnetosphere and Planetary Magnetospheres** — the
  three supported missions are all Earth-orbiting or near-Earth.
- **Bow shock and foreshock have no Region row.** `sitl_parsing` emits dedicated `BOW_SHOCK` and
  `FORESHOCK` classes, and `doc/source/event_search.rst` names "particle acceleration sites at shocks"
  among the processes the Event Search tool handles. Those regions are upstream of the magnetosphere,
  and the Region vocabulary — 24 rows when this record was compiled — has no term for either, so the
  capability is deliberately recorded here as an omission rather than forced into
  `Earth Magnetosheath` or `Interplanetary Space`.

### 6. Authors (MANDATORY)

Author order below is alphabetical by family name and carries no significance; it does not correspond
to HSSI's stored ordering.

**Author 1:**
- **Name:** Jorge Amaya
- **Author Identifier:** https://orcid.org/0000-0003-1320-8428
- **Affiliation:**
  - **Organization:** KU Leuven
  - **Affiliation Identifier:** https://ror.org/05f950310

**Author 2:**
- **Name:** Etienne Behar
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Not found
  - **Affiliation Identifier:** Not found

**Author 3:**
- **Name:** Hugo Breuillard
- **Author Identifier:** https://orcid.org/0000-0003-4187-7303
- **Affiliation:**
  - **Organization:** Laboratoire de Physique des Plasmas
  - **Affiliation Identifier:** https://ror.org/05c95bg36

**Author 4:**
- **Name:** Romain Dupuis
- **Author Identifier:** https://orcid.org/0000-0002-7976-1034
- **Affiliation:**
  - **Organization:** KU Leuven
  - **Affiliation Identifier:** https://ror.org/05f950310

**Author 5:**
- **Name:** Sofoklis Katakis
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Irida Labs
  - **Affiliation Identifier:** https://ror.org/02hcnd264

**Author 6:**
- **Name:** Giovanni Lapenta
- **Author Identifier:** https://orcid.org/0000-0002-3123-4024
- **Affiliation:**
  - **Organization:** KU Leuven
  - **Affiliation Identifier:** https://ror.org/05f950310

**Author 7:**
- **Name:** Jannis Teunissen
- **Author Identifier:** https://orcid.org/0000-0003-0811-5091
- **Affiliation:**
  - **Organization:** Centrum Wiskunde & Informatica
  - **Affiliation Identifier:** https://ror.org/00x7ekv49

**Where the list comes from.** The repository's own package-level author declaration is
`doc/source/conf.py` at the pinned revision:

> `author = 'Jorge Amaya, Etienne Behar, Hugo Breuillard, Romain Dupuis,' \`
> `         ' Sofoklis Katakis, Jannis Teunissen'`

with the identical six names in the adjacent `copyright = '2019, ...'` line. Until this refresh the
stored record carried three names — Jorge Amaya, Romain Dupuis, Giovanni Lapenta — which are the
value of the `contact:` key in the PyHC registry entry (`_data/projects.yml`, the community list:
`contact: Romain Dupuis, Jorge Amaya, Giovanni Lapenta`). Those are the package's *contacts*, and the
overlap with the author list is partial. Giovanni Lapenta is not in `conf.py`'s author list but is
kept: he is the AIDA project's principal investigator, appears as a commit author
(`giovanni.lapenta@kuleuven.be`), and was already among the three names published for this software.
The value above is therefore the union of the two sources, which drops nobody.

**Identifier resolution.** Each ORCID was matched by name and then corroborated against the record's
own works or employments, because same-name ORCID collisions are common:
- Jorge Amaya `0000-0003-1320-8428` — employment "Katholieke Universiteit Leuven", department
  Mathematics, 2018–2022 (the AIDA period), now European Space Agency; works include "Unsupervised
  classification of simulated magnetospheric regions".
- Hugo Breuillard `0000-0003-4187-7303` — works include "Automatic Classification of Plasma Regions in
  Near-Earth Space with Supervised Machine Learning" (the paper whose Acknowledgments cite AIDApy) and
  "A statistical study of dipolarization fronts observed by MMS", within a large MMS/Cluster
  magnetosheath corpus. The only employment on the record is BRGM, a later move; his affiliation here
  is taken from the 2020 paper instead (see below).
- Romain Dupuis `0000-0002-7976-1034` — works include "Characterizing Magnetic Reconnection Regions
  Using Gaussian Mixture Models on Particle Velocity Distributions", the paper the `examples/03_gmm`
  use case implements; employment "Katholieke Universiteit Leuven - Campus Arenberg", department
  "Centre for mathematical Plasma-Astrophysics", 2019–2020. A second "Romain Dupuis"
  (`0000-0001-9451-1132`, materials science) exists and is a different person.
- Giovanni Lapenta `0000-0002-3123-4024` — KU Leuven employment from 2007, with an MMS and
  particle-in-cell publication record.
- Jannis Teunissen `0000-0003-0811-5091` — the only ORCID record a search on the name returns;
  employments are Centrum Wiskunde & Informatica, department Multiscale Dynamics, from 2018, and KU
  Leuven CmPA 2016–2019, the
  latter overlapping the AIDA project at its host institute. His published works are streamer-discharge
  plasma physics rather than heliophysics, so the linkage rests on the institutional overlap plus the
  in-repo attribution `Author: Jannis Teunissen` in `aidapy/ml/models/RegressorMlp.py` and the commit
  identity `Jannis Teunissen <jannis@teunissen.net>`. CWI is recorded as the affiliation because it
  spans the whole development period; the KU Leuven CmPA post is the AIDA-side link and is noted here
  rather than added as a second affiliation, to keep one affiliation per author.

**Affiliation sources.** The JSON-LD block of Breuillard et al. (2020) at
`https://www.frontiersin.org/journals/astronomy-and-space-sciences/articles/10.3389/fspas.2020.00055/full`
gives per-author affiliations contemporaneous with the AIDA work: Hugo Breuillard -> "Laboratoire de
Physique des Plasmas (LPP), France"; Romain Dupuis, Jorge Amaya and Giovanni Lapenta -> "Center for
Mathematical Plasma Astrophysics (CmPA), KU Leuven, Belgium". Breuillard's commit addresses in this
repository (`breuillard@lab-lpp.local`, `hbreuill@lpce.lan`) independently point to LPP. RORs were
resolved through `https://api.ror.org/v2/organizations`: KU Leuven `https://ror.org/05f950310`,
Laboratoire de Physique des Plasmas `https://ror.org/05c95bg36`, Centrum Wiskunde & Informatica
`https://ror.org/00x7ekv49`, Irida Labs `https://ror.org/02hcnd264`. Sofoklis Katakis has no ORCID
record; his affiliation is taken from the commit address `katakis@iridalabs.gr`, the company's own
domain. ROR's display name for that organization is "Irida Labs (Greece)" — the country suffix is a
ROR disambiguation artifact, so the institutional name is recorded without it and the ROR carries the
precise identity.

**The recorded affiliation name for Breuillard, and the name forms behind it.**
`Laboratoire de Physique des Plasmas` is the authoritative name for ROR `https://ror.org/05c95bg36`.
That ROR record (`https://api.ror.org/v2/organizations/05c95bg36`) carries it as the `ror_display`
name, also typed `label` and tagged French; `Laboratory of Plasma Physics` is an English **alias** on
the same record, `LPP` and `LPTP` are acronyms, and `UMR 7648` is a further alias. The record locates
the laboratory in Palaiseau, France, gives its website as `https://www.lpp.polytechnique.fr`, and
lists its parents as the Centre National de la Recherche Scientifique (and CNRS Ingénierie), École
Polytechnique, Sorbonne Université, Université Paris-Saclay and Observatoire de Paris. That parent set
is what the literature spells out for this laboratory: Crossref's record for
`https://doi.org/10.1029/2020JA028040` — the Behar, Sahraoui & Berčič paper discussed below and in
Field 27 — affiliates its two LPP authors to Laboratoire de Physique des Plasmas together with
CNRS-École Polytechnique, CNRS-Sorbonne Université, Université Paris-Saclay and Observatoire de
Paris-Meudon at Palaiseau. (Crossref's string spells the word "Unversité" there; that is a typo in the
deposited metadata, not a variant institutional name.) The Frontiers paper's own string quoted above,
"Laboratoire de Physique des Plasmas (LPP), France", agrees on the French name and appends the
acronym, which this field's expand-acronyms instruction drops.

This field records `Laboratoire de Physique des Plasmas`, which is also the name, abbreviation `LPP`
and website `https://www.lpp.polytechnique.fr` that the ROR-identified organization row was corrected
to carry when this record was refreshed. That correction had to be made directly against the database
for the reason set out below, so it does not travel with a submitted field value: an HSSI instance
that has not received it will still show the earlier English-alias form, and correcting it there is a
database change, not something this field can express.

**The name this replaced, recorded so it is not reintroduced.** The same ROR-identified organization
was stored as `Laboratory of Plasma Physics (LPP/CNRS)` — the English alias from the ROR record, plus
a `(LPP/CNRS)` parenthetical matching none of the name forms enumerated above — with its
`abbreviation` and `website` columns empty even though ROR supplies both. The disagreement between
that spelling and the ROR form was examined against the evidence above and settled in favour of the
ROR name; it is not a variant to restore. This record makes no claim about how the earlier label came
to be.

**Why the correction could not be a field value.** Organization resolution matches on the identifier
and fills only a *blank* name, so a row whose name already differs keeps its stored label however the
name is spelled in submitted metadata. The name, abbreviation and website could therefore only be
corrected directly against the database, which is where the recorded values came from — this field
can state the correct name but cannot install it.

The laboratory's own site could not be used to corroborate any of this:
`https://www.lpp.polytechnique.fr` refuses automated requests. The recorded name therefore rests on
ROR and Crossref, which agree.

Etienne Behar has no confirmable identifier, and two candidate ORCID records were examined rather than
one. `0000-0003-0177-510X` is the record Crossref attaches to the "E. Behar" of
`https://doi.org/10.1029/2020JA028040`, an LPP-affiliated author — which would, if it held, supply both
an identifier and a contemporaneous institution. `0009-0009-5843-901X`, "Etienne Behar Berčič", is the
only hit for a search on the name itself. **Both records carry zero works and zero employments**, so
neither corroborates anything: the first rests on a first-initial match inside a third-party metadata
record, the second on a name string alone, and an ORCID with no works and no employments cannot confirm
an identity even when the name matches exactly. Asserting either would be an identity claim the
evidence does not support, so the identifier stays unrecorded — do not resolve a person on a
first-initial match. His affiliation is unrecorded for the same reason: nothing in the repository gives
him an institution, and reading LPP into it would inherit the very inference the first ORCID candidate
failed to establish. His only in-repo traces are `Contributors: Etienne Behar` in
`aidapy/aidaxr/graphical.py` and the commit address `etienne.behar@gmail.com`.

**Considered and not recorded.**
- **AIDA Consortium as an organization author.** `setup.py` declares
  `author="AIDA Consortium"` with `author_email="coordinator.aida@kuleuven.be"`, and
  `LICENSE.txt` reads "Copyright (c) 2019 AIDA Consortium". An H2020 project consortium is not a
  ROR-registered organization, and a ROR search for "AIDA Consortium" returns only unrelated bodies
  (an American Indian development association, a French agroecology unit, a Japanese press
  manufacturer, an imaging-diagnostics data hub). Recording an organization author with no ROR would
  give HSSI no way to identify it, so the seven named people are recorded instead and the consortium
  attribution is documented here.
- **Brecht Laperre** — author of `aidapy/ml/models/lstm.py` ("author: Brecht Laperre / contributor:
  Romain Dupuis / e-mail: brecht.laperre@kuleuven.be") and `aidapy/ml/metrics/dtw_m_e.py`
  ("@author: Brecht Laperre"), i.e. of both the Dst LSTM and the dynamic-time-warping metric. He also
  presented AIDApy publicly ("Pitfalls in the prediction of the Dst index using ANN", Machine Learning
  in Heliophysics 2019: "We will give an introduction to the AIDApy python package and the AIDAdb
  database that contain the ANN models that we studied"; that abstract's ADS permanent link is the
  fifth value in Field 27).
- **Leonidas Liakopoulos** — co-credited with Sofoklis Katakis in the module docstrings of
  `aidapy/ml/builders/builders.py`, `cli.py`, `engine.py`, `engine_unspr.py`, `factory.py` and
  `hpo_optuna.py`, which is most of the ML framework's scaffolding, and is a substantial commit author.
- **Seven further commit authors with no authorship claim anywhere in the package.** A
  `git shortlog -sne` at the pinned revision, with the duplicate identities of the recorded authors
  collapsed, leaves Sara Jamal (49 commits), Mariangela Viviani (24, across the `mviviani@live.it`
  identity and her full-name one), `xristos klaridopoulos` (13), Domenico Trotta (7), Alessandro Retino
  (4), `francescofinelli94` (2) and Andong Hu (1). Three are visible in the surrounding record: Sara
  Jamal is first author of the AGU 2021 abstract that describes AIDApy (Field 27), Alessandro Retino is
  a co-author of Breuillard et al. (2020) (also Field 27), and Andong Hu's `cwi.nl` commit address
  places him at Jannis Teunissen's institute. None of the seven appears in `doc/source/conf.py`'s
  author line, in the `copyright` line beside it, in any module docstring's author or contributor tag,
  in the PyHC registry's `contact:` value, or in `setup.py`. Two are known only by a bare login
  (`xristos klaridopoulos`, `francescofinelli94`), which is not a resolvable person identity in any
  case; do not expand a login into a presumed real name.

**The governing principle: declared authorship, not commit volume.** Field 6 records the people the
software declares as its authors — `doc/source/conf.py`'s author line, unioned with the PyHC
registry's `contact:` value — and no one else. That criterion is settled, and it is why Brecht
Laperre, Leonidas Liakopoulos and the seven further commit authors above are documented here rather
than recorded as authors: none of them appears in either of those two declarations. Laperre's and
Liakopoulos's credits are module-docstring author tags, which name who wrote a file rather than whom
the package declares as its authors. A commit count cannot stand in for the criterion either, because
the two orderings disagree sharply. Liakopoulos has 51 commits at the pinned revision — more than
three of the declared authors, Jannis Teunissen (40), Jorge Amaya (24) and Giovanni Lapenta (2) — and
is still not declared; Sara Jamal's 49 would likewise outrank Amaya; and Brecht Laperre's single
commit would badly understate the two modules whose docstrings credit him. Volume measures who touched
the code, not whom the project credits. Every contributor in this subsection is therefore documented
rather than added, so that a future agent does not read the absence as an oversight and re-derive an
author list from a `shortlog`.

**Durable limitation — how HSSI resolves a person, and what that means for these ORCIDs.** Person
resolution branches on whether an identifier is supplied. **With** an identifier, HSSI matches on the
identifier alone and does not fall back to the name: supplying an ORCID for an author already stored
*without* one does not enrich that stored row, it creates a second person row and leaves the original
behind. **Without** an identifier, resolution matches on the exact, case-sensitive given and family
name and reuses the existing row. Affiliations are added to whichever row was matched, so submitting
an author with no identifier still attaches the affiliation to the row that already exists. Two
further constraints sit alongside that: the whole authors field is rejected if any stored given name
is blank, and an existing affiliation cannot be replaced (adding one whose ROR already matches is
idempotent).

**The settled consequence for AIDApy.** All five ORCIDs recorded above were applied to their authors'
person rows when this record was refreshed, two of them through submitted metadata and three directly
against the database. As with the affiliation name above, the three database-applied identifiers do
not travel with a submitted field value: an HSSI instance that has not received that correction will
still hold those three authors without identifiers, and putting them right there is a database change
rather than anything this field can carry. Those three —
`https://orcid.org/0000-0003-1320-8428` (Amaya), `https://orcid.org/0000-0002-7976-1034` (Dupuis) and
`https://orcid.org/0000-0002-3123-4024` (Lapenta) — belong to the three authors the record already
carried before this refresh, and were applied directly against the database rather than as submitted
field values. The mechanism above is the reason: because those three rows existed with no identifier,
an ORCID accompanying them in submitted metadata would have created a second person row and left the
original behind, so the KU Leuven affiliation recorded above would have attached to the duplicate
instead of to the row this software points at. Correcting the existing rows instead put each author's
identifier and affiliation on the person this software is actually associated with.

Breuillard's and Teunissen's ORCIDs were not exposed to that hazard, because both are authors this
record added rather than rows already associated with this software; Behar carries no identifier at
all, and Katakis carries an affiliation ROR and no ORCID. Identifier-only matching can still create a
duplicate of a same-named person stored elsewhere in HSSI without that ORCID; what it cannot do is
displace an association this record already holds.

The general rule behind the choice, and the reason it is recorded here rather than treated as a
one-off: orphaning a shared row — a Person or an Organization, which other software records may
reference — is not an acceptable price for an enrichment. `SoftwareVersion` is the exception the
project has explicitly accepted: replacing a version orphans the row it replaces, and that has been
judged acceptable HSSI behaviour (Field 12).

### 7. Software Name (MANDATORY)
**Value:** AIDApy

**Source.** `README.rst`'s document title is `AIDApy`, and `doc/source/index.rst` reads "Welcome to
AIDApy's documentation!". The distribution name is lower-case `aidapy` on PyPI and in
`setup.py` (`name="aidapy"`), and the PyHC registry entry uses `name: aidapy`; the mixed-case
`AIDApy` is the project's own presentation form, and is the form the record already carried before
this refresh. Retained unchanged — the lower-case packaging name is a distribution identifier, not a
rename.

### 8. Description (MANDATORY)
**Value:** The Python package aidapy centralizes and simplifies access to spacecraft data from heliospheric missions, space physics simulations, advanced statistical tools, and Machine Learning/Deep Learning algorithms and applications. It provides a simple mechanism for downloading multi-dimensional time-series from various sources and analyzing them by extracting different meaningful statistics. The package includes four main sub-packages: Mission tool, Event search tool, Velocity distribution function tool, and Machine learning tool. It features easy data download from heliophysics missions, xarray data structures for statistical analysis, sophisticated event identification, multiple heliophysics use-cases ready to use, simple interface based on configuration files, easy mechanism to add custom metrics and datasets, visualization and logging of training/validation procedures, and optimization techniques such as Hyper-Parameter Optimization (HPO) and pruning.

**Source.** Carried over unchanged from the published HSSI record. It is a faithful consolidation of
`README.rst`'s opening bullets, its four-subpackage list and its eight-item feature list. It is kept
as written: the text is accurate against the pinned revision, and a stylistic alternative is not a
reason to overwrite a curated description.

### 9. Concise Description (OPTIONAL)
**Value:** AI package for heliophysics providing machine learning and statistical methods for spacecraft data analysis

**Source.** Carried over unchanged from the published HSSI record. It combines `setup.py`'s
`description="AI package for heliophysics"` with the PyHC registry description, "A Python package to
provide machine learning and statistical methods to heliophysics data". 107 characters, within the
200-character limit. Retained as curated wording.

### 10. Publication Date (RECOMMENDED)
**Value:** 2020-06-24

**Source.** The date of first public release, corroborated three ways: `CHANGELOG.rst` heads its
oldest entry "AIDApy 0.0.2 (2020-06-24)" and calls it "the first release of *aidapy*"; the annotated
git tag `v0.0.2` is dated 2020-06-24 with the message "The first release of aidapy. Add 0.0.2
changelog"; and PyPI's JSON API records both `0.0.2` distribution files uploaded
2020-06-24T13:23:49Z and 2020-06-24T13:24:15Z.

**Trap.** GitLab's releases API reports `released_at` of 2020-09-23T06:48:17Z for `v0.0.2` — later
than `v0.0.4`'s git tag date. Both GitLab *release objects* were created on 2020-09-23, retroactively
for 0.0.2. That timestamp records when someone filled in the release page, not when the software was
first published, and must not be used for this field.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitLab
- **Publisher Identifier:** https://gitlab.com

**Source.** No DOI has been obtained (Field 2), so the field takes the repository host. The project is
hosted on GitLab.com under the `aidaspace` group. Retained unchanged. PyPI was considered as an
alternative publisher, since that is where the distributions live; the field's own instruction is to
"indicate the repository host" when no DOI exists, so GitLab is the correct entry and PyPI's role is
recorded in Field 12 instead.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.0.4
- **Version Date:** 2020-09-23
- **Version Description:** Second release of aidapy. New features include an additional B-field aligned reference frame for VDF analysis with the ion bulk flow set to zero and the electron bulk velocity in the (v_x, v_z)-plane (keyword 'B_electron'), new VDF plot methods xy_plane() and spher_gyro(), electron heat flux (e_heatq) added to the MMS mission, increased test coverage for xevents, statistics, event_search, the L3 MMS products e_beta/i_beta/j_curl and vdf_utils, and fixes for a duplicated-index spacecraft position problem and an argument bug in aidaxr.vdf.
- **Version PID:** Not found

**Why v0.0.4 and not 0.1.0 — the two candidates, and why one is not a release.**

This software has a genuinely ambiguous version at the pinned revision, and the distinction is worth
stating precisely so it is not silently re-decided later.

*The candidate that was rejected: 0.1.0.* `aidapy/__init__.py` at the pinned revision ends with
`__version__ = '0.1.0'`, and `setup.py` derives the packaged version from exactly that line
(`version=get_version(os.path.join('aidapy', '__init__.py'))`, which scans for the `__version__`
assignment). So a distribution built from `master` today would declare itself 0.1.0. The pinned
commit's own message is "version 0.1.0". Against that: `CHANGELOG.rst` has no 0.1.0 entry — its newest
section is "AIDApy 0.0.4 (2020-09-23)"; the repository has exactly two tags, `v0.0.2` and `v0.0.4`,
and the pinned commit is untagged; GitLab's releases endpoint lists exactly two releases, `v0.0.2` and
`v0.0.4`; and PyPI's JSON API reports `info.version = 0.0.4` with release keys `0.0.2` and `0.0.4`
only. 0.1.0 was never tagged, never released and never published. It is an unreleased trunk version
bump, and an unreleased version bump is not a release.

*The value recorded: v0.0.4.* It is simultaneously the newest git tag (dated 2020-09-23T07:50:37Z),
the newest GitLab release, and the newest PyPI distribution (files uploaded 2020-09-23T07:52:25Z and
07:52:58Z). The version date is the tag/release/upload date they agree on.

*A note on PyPI as a source.* PyPI's HTML project page returns HTTP 200 behind a bot gate even for
package names that do not exist, so a rendered page is never proof that a version was published. The
statements above rest on the JSON API (`https://pypi.org/pypi/aidapy/json`), which enumerates the
actual release files.

*Version-string form.* The git tag and the GitLab release `tag_name` are both `v0.0.4`; `CHANGELOG.rst`
and PyPI write it as `0.0.4` without the prefix. `v0.0.4` is recorded because it matches the tag and
release names. The rendered view is not a way to check what is stored — it shows a name-prefixed
transform ("AIDApy - v0.0.4") rather than the stored string — so the stored `SoftwareVersion` row
should be read directly before any change to this field is made.

*Version PID.* None exists; see Field 2 for the negative research.

*The superseded release.* Version 0.0.2 (2020-06-24) was the first release: OMNI/Cluster/MMS data
access wrapping HelioPy, the `aidaxr` xarray extensions with statistics, VDF, curlometer, plasma beta
and extreme-event methods, MLP and Gaussian-mixture ML classes, and the `aidafunc` high-level
retrieval, event-search and configuration helpers. Its date is Field 10. `CHANGELOG.rst` also carries
a section "AIDApy 0.0.3 (2020-09-22)" whose entire body reads "No version 0.0.3" — 0.0.3 was skipped,
and it is not a missing release.

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source.** `setup.py` declares `python_requires='>=3.5'`; `README.rst`'s installation instructions
create `conda create -n aidapy python=3.6`; `.gitlab-ci.yml` runs each of its active jobs on the
`python:3.7` image (one further job, pinned to `python:3.6`, is commented out);
`.readthedocs.yml` pins `python: version: 3.7`; the PyHC registry rates the package "Good" for
`python3`. Retained unchanged.

**Considered and rejected.** No compiled sources exist in the tree — no `.c`, `.cpp`, `.f`, `.f90` or
`.pyx` files, and `setup.py`'s `ext_modules=cythonize(extensions)` line is commented out with the note
"Uncommend to wrap C/C++/Fortran codes". Two artifacts could mislead a future agent: the test fixture
`aidapy/aidaxr/tests/data/pvi_output_f90.dat` is reference output *from* a Fortran implementation used
to validate `pvi`, not Fortran source shipped here; and `doc/source/event_search.rst` records that the
Event Search subpackage "is based on Matlab routines available at LPP and further developed", which
describes the algorithms' provenance, not a MATLAB component in this package.

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Why this field is empty.** No publication describes AIDApy as software. There is no software paper,
no JOSS submission, no `CITATION.cff`, and no "How to cite" section anywhere in `README.rst` or the
Sphinx documentation. A full-text search of the astronomical literature for the package name
(`full:"AIDApy"` against `https://api.adsabs.harvard.edu/v1/search/query`) returned twelve documents
on 2026-08-27, none of which is a software paper for it; the closest is a conference abstract with no
DOI (Jamal, Amaya & Lapenta, AGU Fall Meeting 2021, "Making ML applications more accessible to the
space community: Progress overview of the AIDA Horizon 2020 project", whose abstract states that "The
novelty provided by the AIDA project lies in the development of the Python-based AIDApy" and that "The
current work aims to present the functionalities developed within the Python-based AIDApy package").

**Why that abstract is not this field's value, and where it is recorded instead.** Not because it
lacks a DOI. The same abstract *is* a recorded value in Field 27, through its ADS permanent link
`https://ui.adsabs.harvard.edu/abs/2021AGUFMSH35H..05J/abstract` (bibcode `2021AGUFMSH35H..05J`;
Jamal, Sara; Amaya, Jorge; Lapenta, Giovanni; *AGU Fall Meeting Abstracts*, 2021; no DOI) — so a
missing DOI is not what disqualifies a publication reference, and the shape such a value has to take
is set out once in Field 28. The abstract is excluded from *this* field on substance: it is a
conference-talk abstract reporting a project's progress, not a publication describing the software,
and it cannot serve as AIDApy's citable paper. This field stays empty because no such paper exists,
not because that abstract was unusable.

**Considered and rejected: arXiv 1910.10012 / `https://doi.org/10.3847/1538-4357/ab5524`.** This is the
only publication the repository itself links to, in two places:
`examples/03_gmm/reconnection_harris/mpi_script.py` line 5, "See also AIDA paper:
https://arxiv.org/abs/1910.10012", and the opening markdown cell of
`examples/03_gmm/reconnection_harris/gmm.ipynb`, "Details can be found in the following paper:
https://arxiv.org/abs/1910.10012." It is Dupuis, Goldman, Newman, Amaya & Lapenta, "Characterizing
Magnetic Reconnection Regions Using Gaussian Mixture Models on Particle Velocity Distributions",
*The Astrophysical Journal* 889(1):22 (2020-01-20). The previous version of this record described it
as "the AIDA paper", which is how `mpi_script.py` labels it but not what it is: it is the method paper
for the Gaussian-mixture reconnection technique that one AIDApy example demonstrates, written by three
of AIDApy's authors. It never mentions AIDApy — the package name appears in neither its abstract nor
its indexed full text. Citing it would tell a user how to cite that method, not how to cite this
software. It is recorded in Field 27 instead, where it belongs.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

**Source.** `LICENSE.txt` at the pinned revision carries the MIT licence text — the "Permission is
hereby granted, free of charge, to any person obtaining a copy of this software" grant, the
"above copyright notice and this permission notice shall be included" condition, and the
warranty disclaimer `THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND` — under
"Copyright (c) 2019 AIDA Consortium". (The quotation marks around `AS IS` are straight ASCII in
`LICENSE.txt`, not typographic quotes.)
Corroborated by `setup.py` (`license='MIT'`), `setup.cfg` (`license_files = LICENSE.txt`), PyPI's
metadata (`license = MIT` for both published releases), `README.rst`'s MIT badge and its prose "It is
distributed under the open-source MIT license", and the PyHC registry's "Good" licence rating. The
name and URI are copied from the matched controlled-vocabulary row so they resolve exactly.

**This field held no value in HSSI until this refresh**, which was a real gap rather than a curation
decision: `LICENSE.txt` carries the MIT text under a 2019 copyright, and `setup.py` and `README.rst`
name MIT as well.

**Two traps in `README.rst` that must not change this value.**
1. Its "Licenses" section hyperlinks the word MIT to a GPL-3.0 URL:
   "distributed under the `MIT <https://www.gnu.org/licenses/gpl-3.0>`__ license". The link target is
   simply wrong; every other statement about *this software's* licence in the repository, including
   the licence file itself, says MIT. (The Creative Commons statement in the same section is trap 2
   below; it governs the AIDAdb data collections, not AIDApy.) Do not read GPL-3.0 from it.
2. The same section adds a Creative Commons statement: "This software (AIDApy) and the database of the
   AIDA project (AIDAdb) are distributed under the MIT license. The data collections included in the
   AIDAdb are distributed under the Creative Commons `CC BT 4.0` license", and `README.rst` carries a
   CC BY 4.0 badge alongside the MIT one. `Creative Commons Attribution 4.0 International` is a row in
   the licence vocabulary, so this is a live temptation — but it governs the AIDAdb *data collections*,
   a separate product of the AIDA project, not this software. Rejected for that reason.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- artificial intelligence
- cluster
- coronal holes
- data analysis
- deep learning
- dst index
- event detection
- heliosphere
- machine learning
- magnetic reconnection
- magnetosphere
- mms
- omni
- pytorch
- space physics
- space weather
- spacecraft data
- statistical analysis
- turbulence
- velocity distribution functions
- xarray

**Source of the retained values.** The first eighteen (all but `magnetic reconnection`,
`space weather` and `turbulence`) are carried over from the published HSSI record, which drew on the
PyHC registry's `keywords: [machine_learning, heliosphere, data_analysis]`, `README.rst` and the
example set. They are recorded here in the lower-case form the vocabulary rows actually use; the
title-cased rendering visible on the site ("Machine Learning", "Mms", "Dst Index") is a display
transform, not the stored value. The previous version of this record listed `machine_learning` and
`data_analysis` with underscores, which is PyHC's spelling, not HSSI's — the matching rows are
`machine learning` and `data analysis`.

**Added by this refresh, and why each carries information not already in another field.**
- `magnetic reconnection` — the single most pervasive science theme in the package and the one with no
  home elsewhere. `event_search(settings='edr')` detects electron diffusion regions;
  `examples/03_gmm/` characterises reconnection regions with Gaussian mixture models;
  `aidapy/external/unsupmr/` ("unsupervised magnetic reconnection") clusters simulation data into
  reconnection regions; `doc/source/event_search.rst` names "magnetic reconnection electron and ion
  diffusion regions and separatrices" first among the processes handled. The Phenomena vocabulary
  (Field 22) has no reconnection term, so this keyword is where the capability becomes findable.
- `space weather` — the Dst-index forecasting use cases are space-weather prediction;
  `doc/source/getting_started.rst` states the aim of showing "how it can make space weather
  forecasts". No other field expresses this.
- `turbulence` — `doc/source/extreme_events.rst` frames the `xevents` module around turbulence
  ("intermittency measurements", "a newly developed technique known as Partial Variance of
  Increments", "tested here on direct numerical simulations of turbulence, by using the virtual
  spacecraft technique"), and `statistics.autocorr`'s documentation refers to "the typical energy
  containg scale" in turbulence. **This term had no existing row in the keyword vocabulary when this
  record was compiled, so it is a minted row rather than a reused one.** Keywords is the one field
  whose vocabulary is open — a missing value is created rather than rejected — so that is permitted.
  It is noted because minting rows is how near-duplicates accumulate; the vocabulary was searched for
  a near-duplicate of `turbulence` to reuse on 2026-08-27 and held none.

**Considered and rejected.** `magnetotail`, `magnetosheath` and `solar wind` all have existing rows and
are all well evidenced, but Fields 5 and 22 already carry them as regions and phenomena, and this field
is for keywords "not supported by other metadata fields". `python` duplicates Field 13; `omniweb`
duplicates Field 17 and the existing `omni` keyword; `clustering` and `neural networks` add nothing to
`machine learning` and `deep learning`; `plasma` and `time series` are too generic to aid a search.
`curlometer`, `dipolarization fronts`, `electron diffusion region`, `pitch angle distribution` and
`gaussian mixture model` are all specific and all absent from the vocabulary; each was left out to
avoid minting five further rows for terms the functionality and region fields already surface.

### 17. Data Sources (OPTIONAL)
**Values:**
- Observatory/Mission-specific
- OMNIWeb

**Source.** `Observatory/Mission-specific` is retained: AIDApy retrieves MMS and Cluster data from
those missions' own archives, and `aidapy/data/mission/modified_cluster.py` targets the ESA Cluster
Science Archive directly (`csa_url = 'https://csa.esac.esa.int/csa/aio/product-action?'`, with a
`DELIVERY_FORMAT: 'CDF'` request dictionary and the CSA cookie described in its module docstring). The
corresponding missions are listed in Field 32, as this field's instruction requires.

`OMNIWeb` was added by this refresh. `doc/source/mission.rst` states "Missions that can be selected
currently are: OMNIWeb, MMS, Cluster"; `aidapy/data/mission/omni.py`'s docstring is "This module
serves as data manager for Omniweb" and its `_download_ts` calls `omni.h0_mrg1hr` for the OMNI2
hourly merged product; `aidapy/ml/data/aidapy_omniweb.py` is "Dataloader to download from the omni
web" and is selected by name in the Dst configurations (`train_datasets: [Aidapy_OmniWeb]`).

**Considered and rejected.** `CDAWeb` and `HTTP/HTTPS Directories` describe how HelioPy transports the
OMNI2 product beneath AIDApy, not a source AIDApy itself declares or targets; AIDApy names OMNIWeb
throughout. `FTP/FTPS Directories`, `HAPI`, `AMDA`, `SSCWeb`, `The Virtual Solar Observatory.`,
`das2`, `TAP`, `VirES`, `Madrigal`, `GFZ`, `WDC` and `S3/Cloud-aware` have no corresponding client,
URL or configuration anywhere in the package. The coronal-hole training images are downloaded by the
user from an OSF project by hand (see Field 28) and then read from a local directory
(`datamode: 'memory'`, `data_path: '../Coronal_Holes/CoronalHoles'`), so they are not a programmatic
data source; `Other` was considered for them and rejected as uninformative.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- ascii
- CDF
- csv
- HDF5
- netCDF3/4
- Other

**Source.** The first five are retained from the published record, each verified against the pinned
revision; `Other` was added by this refresh.
- **CDF** — `aidapy/data/mission/modified_cluster.py` sets `extension = '.cdf'`, requests
  `DELIVERY_FORMAT: 'CDF'` from the Cluster Science Archive and reads the files through `cdf_info()`;
  every product entry in `mission_settings/mms.json` and `cluster.json` is keyed on a CDF variable
  name under `cdf_key`.
- **ascii** — `aidapy/aidaxr/tests/` reads plain-text fixtures (`increm_input_f3.dat`,
  `pvi_input_f3_50pts.dat`, `vdf_T1_v0_nv32.dat`); `aidapy/tools/sitl_parsing.py` parses MMS SITL
  report text files (`aidapy/tools/tests/data/2017-07-31_072433.txt`);
  `doc/source/event_search.rst` describes the Event Search output as "ASCII files with header
  information".
- **csv** — `aidapy/external/unsupmr/ingester.py` and `km_utils_2d.py` read tabular data with
  `pandas.read_csv`.
- **HDF5** — `aidapy/external/unsupmr/scripts/example_script.py` opens the in-package fixture
  `sample_data.h5` via `h5py.File`; `examples/03_gmm/reconnection_harris/` reads simulation output
  with `h5py`.
- **netCDF3/4** — the weakest of the five carried over, retained with its basis stated plainly:
  `h5netcdf` is a hard dependency in `setup.py`'s `install_requires`, and its only purpose is netCDF
  reading and writing through xarray, which is AIDApy's documented data container. No AIDApy code path
  at the pinned revision calls `xarray.open_dataset` or `to_netcdf`; the capability is inherited from
  the data model and the declared dependency rather than exercised in the package.
- **Other** — the vocabulary's only home for image input, and it is recorded because the coronal-hole
  use case is entirely image-driven. `aidapy/ml/data/coronalholes.py` sets
  `self.ext = ('.jpg', '.jpg')` and loads with `cv2.imread`; `ch_unsuper.py` reads the same files; and
  the UNet configurations take `input_nc: 3`, three-channel RGB. The file-format vocabulary has no
  image row and no near-miss row to reuse, so the choice is between `Other` and silence. `Other`
  carries no information by itself, which is why an earlier pass left it out; it is recorded because
  silence is the stronger misstatement — a list of tabular, text and CDF formats alone reads as a claim
  that AIDApy consumes no images at all, which is false for one of its two headline use cases.

**Considered and rejected.**
- **FITS** — a trap worth naming. `doc/source/mission.rst` and `event_search.rst` both say the time
  input may be "an astropy.Time object allowing to handle multiple time format such as GPS, ISOT, or
  FITS". That is astropy's *time-string* format named FITS, not the FITS file format. AIDApy reads no
  FITS file.
- **JSON** — `aidapy/data/mission/mission_settings/*.json` are package-internal product catalogues
  read by `base_mission.py`, and the ML configurations are YAML. Neither is user data input.
- **A JPEG- or image-specific row.** There is none. The vocabulary's rows, when this record was
  compiled, were `ascii`, `CDF`, `csv`, `FITS`, `HDF5`, `IDL.sav`, `ISTP-Compliant`, `JSON`,
  `netCDF3/4`, `Zarr` and `Other` — tabular, binary-scientific and text formats, with no row for a
  consumer raster format. (`FITS` is image-capable, but it is an astronomical container AIDApy does
  not read; see the FITS trap above.) The image input above can therefore only be carried by `Other`,
  as it now is. Recorded so that a future agent does not search for an image row that does not
  exist.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- ascii
- csv
- HDF5
- Other

**Source.** The first three are retained from the published record; `Other` was added by this
refresh.
- **ascii** — `aidapy/aidafunc/event_search.py:_write_events` writes `events_list.txt` with a header
  and one line per event interval, which `doc/source/event_search.rst` describes as the subpackage's
  ASCII output; `aidapy/external/unsupmr/ar_utils_2d.py` writes `structures_thickness.log`.
- **csv** — `aidapy/external/unsupmr/ingester.py` writes with `dataframe.to_csv`;
  `aidapy/ml/data/common/utils.py` writes reformatted data with `to_csv`.
- **HDF5** — `examples/03_gmm/reconnection_harris/mpi_script.py` writes its results with
  `h5py.File(file_output, 'w')`, and `doc/source/mission.rst` documents the inherited HelioPy option
  to "convert all downloaded data to a hdf store, enabling much faster file reading after the initial
  load".
- **Other** — covering two classes of output the vocabulary cannot name. Figures:
  `matplotlib.savefig` writes PNG and EPS throughout `aidapy/ml/visualization/dst_vis.py`,
  `aidapy/external/unsupmr/plot_utils_2d.py` and the ML save callbacks, and rendered figures are the
  visible product of everything in Field 4's Data Visualization branch. Model artifacts: `torch.save`
  writes PyTorch `.pt` checkpoints in `aidapy/ml/models/model.py`, and one such checkpoint
  (`aidapy/ml/models/tests/CH/model_best.pt`) ships inside the package. As in Field 18, `Other` is
  uninformative on its own and is recorded because the alternative — ascii, csv and HDF5 alone —
  implies a package that writes neither figures nor trained models, which is the opposite of what a
  machine-learning toolkit does.

**Considered and rejected.** `netCDF3/4` is recorded as an input format on the strength of the
`h5netcdf` dependency but not as an output, because nothing in the package writes one.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Windows

**Source.** `README.rst` states exactly this, in the installation section: "The package aidapy has
been tested for Linux (Ubuntu 16.04 / 18.04) and Windows 10." Retained unchanged.

**Considered and rejected.** `Mac` is not claimed anywhere, and `.gitlab-ci.yml` runs only on
`python:3.7` Linux container images, so there is no automated evidence for it either.
`Operating System Independent` was rejected because the project made a specific tested-platform claim
rather than a portability claim, and because a Windows-10-plus-two-Ubuntu-LTS statement is narrower
than platform independence. Note also that `OS Independent` is not a value in this vocabulary — the
cross-platform term is `Operating System Independent`, spelled out.

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- CPU Independent
- GPU

**Source.** Retained unchanged. `CPU Independent` — pure Python with no compiled extension in the tree
(see Field 13). `GPU` — genuine CUDA support: `aidapy/ml/engine.py` sets
`self.device = torch.device('cpu' if not self.cfg.getUseGPU() else 'cuda')`, the same construction
appears in `hpo_optuna.py` and `loss/loss.py`, `builders/builders.py` reads `cfg.getUseGPU()` in four
of its nine `build_*` functions (`build_dataloader`, `build_loss`, `build_metrics` and `build_model`;
`build_visualizer`, `build_logger`, `build_postprocess`, `build_optimizer` and `build_callbacks` do
not), `data/data.py` toggles `pin_memory` on it, and the shipped configurations expose it as
a user setting (`system: use_gpu: false` in `examples/04_coronal_holes/config_coronal_holes.yml`,
`use_gpu: true` in `examples/05_omni_regressor_lstm/config_omni_web.yml`).

**Considered and rejected.** `HPC or HEC` — `mpi4py` appears only in
`examples/03_gmm/reconnection_harris/mpi_script.py` and is declared in neither `install_requires` nor
any extra; the notebook instructs the user to run that script outside the notebook across several
cores, which is an example's requirement, not the package's. (A "parallel gpu feature" and a parallel
toolbox were added on the `develop`/`WP4_update` branches in late 2021 and early 2022, after the
pinned revision, and are not part of this release.) `x86-64`, `Apple Silicon arm64`,
`Linux aarch64 or arm64`, `ppc64le` and `Sun (SPARC)` are never claimed and are subsumed by
`CPU Independent`.

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Geomagnetic Storms
- Solar Corona
- Solar Wind

**Source of the retained values.**
- **Solar Wind** — the OMNI product set is a solar-wind parameter set
  (`mission_settings/omni.json` includes `V`, `N`, `T`, `Beta`, `Mach_num`, `Pressure` and the IMF
  components), and `aidapy/tools/sitl_parsing.py` emits a dedicated `SOLAR_WIND` classification.
- **Geomagnetic Storms** — Dst-index forecasting is the package's space-weather use case:
  `mission_settings/omni.json` exposes `DST`, `KP`, `AE`, `AL_INDEX`, `AU_INDEX` and `AP_INDEX`;
  `examples/05_omni_regressor_lstm/config_omni_web.yml` trains on `features: ['DST', 'F', 'BZ_GSM',
  'N', 'V']`; and `aidapy/ml/visualization/dst_vis.py` provides `plot_set_of_storms()` writing to
  `figures/notebook_storms`, i.e. storm-interval evaluation is a first-class output. This value was
  added to the record on 2026-08-24 on exactly that DST-forecasting evidence and is confirmed here.

**Added by this refresh.**
- **Solar Corona** — the coronal-hole segmentation use case is solar-corona science:
  `examples/04_coronal_holes/README.rst`, six shipped configurations, the `CoronalHoles` dataloader,
  and a trained UNet checkpoint at `aidapy/ml/models/tests/CH/model_best.pt`. The value is settled as
  recorded, with the objection to it stated so that it is not relitigated: `Solar Corona` reads more
  like a region than a phenomenon, and Field 5's `Corona` row already carries the regional aspect. It
  is recorded anyway because, of the seven terms in this vocabulary, it is the closest available
  phenomenon under which coronal-hole work becomes findable, and a search for solar-corona software
  should return this package.

**`Coronal Holes` is not a value in this vocabulary and must not be re-proposed.** The controlled list
held seven terms when this record was compiled (2026-08-27) — `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`,
`X-ray emission` — and `Coronal Holes` is not one of them. It appeared in the submission form's own
documented value list in error until that list was audited against the live vocabulary on 2026-07-29;
submitting it now would be rejected. It was removed from this record on
2026-08-24 for that reason. The coronal-hole science is real and is carried by the `coronal holes`
keyword in Field 16, the `Corona` and `Solar Environment` rows in Field 5, and now `Solar Corona`
here.

**Other terms considered and rejected.**
- **Coronal Mass Ejections** — `doc/source/extreme_events.rst` claims the `xevents` module "will lead
  to the identification of large amounts of structures such as magnetic reconnection events, coronal
  mass ejections, shocks, fluid-like vortices, discontinuities, as well as large amplitude waves".
  That is a forward-looking statement about a class of structures a generic PVI threshold detector may
  surface; no CME-specific criterion, catalogue or example exists. Rejected, with the quotation
  recorded so a future agent recognises the sentence rather than treating it as new evidence.
- **Coronal Heating, Solar Flares, X-ray emission** — no corresponding functionality.
- **Magnetic reconnection has no row here.** It is arguably the package's central science theme
  (Field 16 sets out the evidence), and the vocabulary enumerated above simply has no term for it.
  This is the reason the `magnetic reconnection` keyword was added to Field 16, and the reason this
  field looks thinner than the software's reconnection focus would suggest.
- **Nor do the other phenomena the software actually classifies.** `sitl_parsing.py`'s event
  classifier emits `DIPOLARIZATION_FRONT`, `BURSTY_BULK_FLOW`, `PLASMA_JET`, `FLUX_ROPES` and
  `PLASMA_FLOWS`, and `event_search` ships presets for dipolarization fronts and electron diffusion
  regions. None of the five has a Phenomena row, and turbulence — the framing of the whole `xevents`
  module — has none either. The regions in Field 5 and the keywords in Field 16 are where those
  capabilities are findable; this field cannot express them.

### 23. Development Status (RECOMMENDED)
**Value:** Inactive

**Why Inactive.** The repostatus.org definition attached to this row is "The project has reached a
stable, usable state but is no longer being actively developed; support/maintenance will be provided
as time allows." Both halves hold:

*Reached a stable, usable state.* Two versioned releases were tagged, released on GitLab and published
to PyPI (Field 12); `CHANGELOG.rst` documents both; Sphinx documentation is published at
`https://aidapy.readthedocs.io`; a GitLab CI pipeline runs Pylint with a score gate and a coverage
job; and the package is registered in the PyHC community list.

*No longer actively developed.* The last release was 2020-09-23. `master`'s final commit is the pinned
revision, 2021-09-14. Development continued on branches for a further five and a half months and then
stopped: GitLab reports the project's `last_activity_at` as 2022-03-03T14:42:01Z, and the most
recently updated branch tip (`notebooks_merge_dev`) is 2022-03-03T16:41:53+02:00. No merge request has
been opened or updated since 2021-09-14 (the newest, `!44` "merge develop into master", was merged
that day).

**Rejected candidates, each with its reason.**
- **WIP** and **Abandoned** — both definitions require that "there has not yet been a stable, usable
  release". AIDApy published two. The previous version of this record chose `WIP` on the reasoning that
  a 0.0.x version number implies early development; that conflates a version-numbering convention with
  the absence of a release, and is corrected here.
- **Suspended** — also requires no stable release, and additionally asserts that the authors "intend on
  resuming work", which nothing published claims.
- **Concept** — requires minimal or no implementation. AIDApy is a documented, tested, released package.
- **Active** — contradicted by the activity record above: no release for nearly six years, no trunk
  commit for nearly five, no repository activity of any kind for over four.
- **Unsupported** — the closest rival. It asserts that "the author(s) have ceased all work on it. A new
  maintainer may be desired." That is a statement of maintainer intent, and the project has not
  published it: there is no end-of-life notice or maintainer-wanted note anywhere in the repository,
  the GitLab project is still public and browsable, and `README.rst` still carries a
  "Maintained?: yes" shield. `Inactive` is the strongest status the published evidence supports
  without inventing an intent. (GitLab's unauthenticated project response does not expose the
  `archived` flag at all, so archival status is not usable evidence either way here.)
- **Moved** — no successor location is announced. When this record was compiled the `aidaspace`
  GitLab group held only `aidapy`, `heliopy_multid` and `notebooks_aida`.

**Caveat for a future refresh.** This is a 2026 judgement about a repository whose trunk last moved in
2021 and whose last activity of any kind was 2022-03-03. The H2020 AIDA project that funded it has
ended and the project website is gone: `http://aida-space.eu/AIDApy_AIDAdb`, the URL that Arró,
Califano & Lapenta (2020), `https://doi.org/10.1051/0004-6361/202038696`, give for accessing the AIDA
database, no longer responds. If a maintainer ever declares end-of-life or asks for a new maintainer,
`Unsupported` becomes the correct value; if someone resumes releases, `Active`.

**This field held no value in HSSI until this refresh**, which was a real gap rather than a curation
decision.

### 24. Documentation (RECOMMENDED)
**Value:** https://aidapy.readthedocs.io

**Source.** `README.rst` — "Full documentation can be found `here <https://aidapy.readthedocs.io>`_";
the same URL is the PyHC registry's `docs:` value. `.readthedocs.yml` configures the build from
`doc/source/`. The URL resolves — it redirects to `https://aidapy.readthedocs.io/en/latest/`, which
serves the built documentation. Retained unchanged.

**Caveat.** The `latest` build tracks the repository's default branch, so the published documentation
can describe modules that the pinned revision does not contain. The `doc/source/*.rst` files at the
pinned revision are the authority for what this release documents.

### 25. Funder (OPTIONAL)

**Funder 1:**
- **Organization:** European Commission
- **Funder Identifier:** https://ror.org/00k4n6c32

**Source.** `README.rst` lines 49–50 at the pinned revision:

> The ``aidapy`` package is part of the project AIDA (Artificial Intelligence Data Analysis) in Heliophysics funded from
> the European  Unions  Horizon  2020  research  and  innovation  programme under grant agreement No 776262.

(The doubled spaces and the missing apostrophe in "Unions" are as written in the source.)
Independently corroborated twice: Crossref's funding block for
`https://doi.org/10.3847/1538-4357/ab5524` records funder "European Union Horizon 2020" with award
`776262`; and the ADS abstract of Jamal, Amaya & Lapenta (AGU 2021) closes "[This project has received
funding from the European Unions Horizon 2020 research and innovation programme under grant agreement
No 776262 (AIDA)]".

**Why the recorded name is not the label it replaced.** Until this refresh the record carried the
organization as `European Commission - Horizon 2020` with an empty identifier. Horizon 2020 is the
European Union's funding *programme*, not an organization; the funding body is the European
Commission, which `https://api.ror.org/v2/organizations` resolves to `https://ror.org/00k4n6c32`
(display name "European Commission", aliases including "EC", located in Belgium). This field asks for
one organization per entry with acronyms expanded, so the programme name belongs to the award context
in Field 26 rather than inside the funder's name, and the ROR makes the organization
machine-identifiable where that identifier-less label did not.

**Why this needed no rename.** Two organization rows exist for this funder: one named
`European Commission` carrying the ROR `https://ror.org/00k4n6c32`, and a separate, identifier-less
row named `European Commission - Horizon 2020`, which was the label this software's funding had been
stored under. The settled outcome was to associate the ROR-identified row — exactly the value recorded
above — rather than to rename anything, and that is the row this record points at. A rename would not
have worked in any case: organization resolution matches on the identifier and fills only a *blank*
name, so an existing row whose name differs keeps its stored label. Because the ROR-identified row
already carried the right name, supplying the ROR was sufficient.

A related constraint worth knowing before a later refresh: the funder-to-award association renders on
the software's detail page but is not writable through any API path, so keeping the award linkage
intact alongside a funder change is a database-level matter.

**Considered and rejected.** Crossref's funder block for the same ApJ paper also lists "Office of
Science US Department of Energy", award `DE-AC02-05CH1123`. That award supports the paper's US
co-authors (Goldman and Newman, University of Colorado), not this software; Crossref flattens all
funding tiers into one list, and only the funding of *this software* belongs here. Recorded so a later
refresh does not reintroduce it from Crossref. KU Leuven, which hosted the work and whose address is
the package's contact (`coordinator.aida@kuleuven.be`), is an author affiliation rather than a funder.

### 26. Award Title (OPTIONAL)

**Award 1:**
- **Award Title:** AIDA (Artificial Intelligence Data Analysis) in Heliophysics
- **Award Number:** 776262

**Source.** The title is taken from `README.rst`'s own naming of the project — "the project AIDA
(Artificial Intelligence Data Analysis) in Heliophysics" — and the number from the same sentence,
"under grant agreement No 776262" (quoted in full in Field 25). The number is confirmed independently
by Crossref and by the AGU 2021 abstract cited there. Retained unchanged from the published record.

**Length check.** The award title is 60 characters, comfortably inside the undocumented 128-character
cap on the award name column that causes a database-level failure rather than a validation error. The
award number is 6 characters. No length risk in this field.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values:**
- https://doi.org/10.3847/1538-4357/ab5524
- https://doi.org/10.3389/fspas.2020.00055
- https://doi.org/10.1029/2023JA031738
- https://ui.adsabs.harvard.edu/abs/2021AGUFMSH35H..05J/abstract
- https://ui.adsabs.harvard.edu/abs/2019mlhp.confQ..46L/abstract

**Why each qualifies.**
1. **`10.3847/1538-4357/ab5524`** — Dupuis, Goldman, Newman, Amaya & Lapenta, "Characterizing Magnetic
   Reconnection Regions Using Gaussian Mixture Models on Particle Velocity Distributions", *ApJ*
   889(1):22 (2020). It is the sole DOI-or-arXiv reference anywhere in the repository at the pinned
   revision, cited twice (`examples/03_gmm/reconnection_harris/mpi_script.py` line 5 and the first
   markdown cell of `gmm.ipynb`), and the `examples/03_gmm` use case implements its method. Field 14 explains why it is
   a related publication rather than the reference publication.
2. **`10.3389/fspas.2020.00055`** — Breuillard, Dupuis, Retino, Le Contel, Amaya & Lapenta, "Automatic
   Classification of Plasma Regions in Near-Earth Space With Supervised Machine Learning: Application
   to Magnetospheric Multi Scale 2016–2019 Observations", *Frontiers in Astronomy and Space Sciences*
   7 (2020). Its Acknowledgments cite the package by name — "Data were retrieved using HELIOPY v0.5.3
   (Stansby et al., 2020) and processed using aidapy [footnote 4]" with footnote 4 resolving to
   `https://gitlab.com/aidaspace/aidapy` — and its Data section describes the use: "We start with
   loading the raw MMS magnetic field and plasma moments data from FGM and FPI instruments for the
   2016–2019 period using the aidapy package". Its Discussion states an intent to integrate the
   resulting model into AIDApy. There is a further concrete tie: `requirements.txt` at the pinned
   revision installs HelioPy from `github.com/hbreuill/heliopy`, the fork maintained by that paper's
   first author.
3. **`10.1029/2023JA031738`** — Alqeeq et al., "Two Classes of Equatorial Magnetotail Dipolarization
   Fronts Observed by Magnetospheric Multiscale", *JGR Space Physics* 128 (2023). A full-text probe
   confirms the package name appears in this article (`full:"AIDApy" bibcode:2023JGRA..12831738A`
   returns it, against a nonsense-token control that returns nothing). Its precursor EGU abstract,
   `https://doi.org/10.5194/egusphere-egu22-9532`, spells the use out: "Criteria for selecting DF
   using an AIDApy routine are based on difference of maximum and minimum values computed with a 306 s
   sliding window" — the 306-second window is literally the `"time_window": 306` default in
   `aidapy/aidafunc/event_search.py:_settings_df`. The peer-reviewed article is listed rather than the
   abstract; the abstract is recorded here because it is the clearer statement of how AIDApy was used.
4. **`https://ui.adsabs.harvard.edu/abs/2021AGUFMSH35H..05J/abstract`** — Jamal, S., Amaya, J., &
   Lapenta, G. (2021). *Making ML applications more accessible to the space community: Progress
   overview of the AIDA Horizon 2020 project* [Conference abstract SH35H-05]. AGU Fall Meeting 2021.
   Of everything the literature search surfaced, this is the item that comes closest to *describing*
   AIDApy rather than using it: its abstract states that "The novelty provided by the AIDA project
   lies in the development of the Python-based AIDApy" and that "The current work aims to present the
   functionalities developed within the Python-based AIDApy package". Its inclusion is settled:
   bibcode `2021AGUFMSH35H..05J` has no DOI, this field accepts any permanent link, and the ADS
   abstract page is therefore the value. To re-verify this value later: the ADS web interface answers
   automated requests with an HTTP 405 and a WAF captcha rather than the page, so a 405 there is
   bot-blocking and not link rot; the bibcode and its metadata are confirmable through
   `api.adsabs.harvard.edu`, which serves an anonymous bootstrap token. The three Lapenta
   project-overview abstracts, below, do not do as much: they name AIDApy without saying how it was
   used.
   **Recorded as the bare ADS permanent link, with the APA citation confined to this rationale** —
   not a stylistic choice but the field's storage shape, set out once in Field 28. Any later attempt
   to enrich this entry with the citation, the title or the author list will fail for that reason: the
   link is the only part of the reference the field can hold, and the rest has to live here.
5. **`https://ui.adsabs.harvard.edu/abs/2019mlhp.confQ..46L/abstract`** — Laperre, B. (2019).
   *Pitfalls in the prediction of the Dst index using ANN* [Conference abstract]. Machine Learning in
   Heliophysics 2019. Sole-authored; no DOI; recorded as the ADS permanent link on the same storage
   grounds as item 4. It qualifies because the abstract states a direct relationship between the
   publication's subject matter and this software's shipped contents: "We will give an introduction to
   the AIDApy python package and the AIDAdb database that contain the ANN models that we studied.
   These models can be use in conjunction with OMNI datasets to reproduce our results" (the
   misspelling is the source's). The models in question are the ones this package distributes — the
   LSTM Dst forecasting stack in `aidapy/ml/models/lstm.py`, whose module docstring names Laperre as
   its author (see Field 6), driven by the OMNI access documented in Field 17 — so the abstract
   describes the software's own capability rather than merely citing the project. The same abstract
   independently repeats the Horizon 2020 grant number recorded in Fields 25 and 26 ("grant agreement
   No 776262 (AIDA, www.aida-space.eu)"), which corroborates that funding attribution from outside the
   repository.

   An earlier reading of this record excluded it on the grounds that "We will give an introduction to"
   announces a workshop talk rather than reporting completed work. That reading was not adopted: the
   same sentence also asserts what the package contains, which is a statement of relationship to the
   software and is what this field's test asks for. Recorded so the exclusion is not re-proposed from
   the phrasing of the first clause alone.

**Considered and rejected.**
- **`10.1051/0004-6361/202038696`** (Arró, Califano & Lapenta 2020, *A&A* 642:A45). This looks like a
  hit because the string "AIDApy" appears in its Data Availability Statement — but as part of a URL:
  "The simulation dataset (UNIPI e-rec) is available at Cineca on the AIDA-DB. Details to access the
  meta-information and the link to the raw data are available at
  http://aida-space.eu/AIDApy_AIDAdb." That is a page on the AIDA project website about the AIDAdb
  database, not a use of this software. (The URL no longer resolves; see Field 23.)
- **The three remaining DOI-less items among the twelve full-text matches** (the dated search is
  recorded in Field 14). Five of those twelve matches carry no DOI. Two of them, the Jamal and Laperre
  abstracts, are recorded above; the other three are excluded on content, not on the absence of a DOI
  — each has an ADS permanent link that could have carried a value, and the reason not to use it is
  the same substantive-relationship test applied to the passing mentions below. All three are Lapenta
  project-overview abstracts: `2019shin.confE..44L` (SHINE 2019), `2020AGUFMNG005..04L` (AGU 2020) and
  `2022cosp...44..869L` (COSPAR 2022). The package name is present in the full text with no
  accompanying statement of how it was used.

  Recorded so that the inclusion of two DOI-less abstracts is not later read as licence to add the
  rest: what separates them is a statement of relationship to the software, not the venue type.
- **Passing mentions and downstream citations.** `10.1109/TPS.2023.3268170` (2022 Review of
  Data-Driven Plasma Science) names AIDApy inside a very large survey; `10.3847/1538-4357/abd24b`
  (Sisti et al. 2021), `10.1029/2020JA028040` (Behar et al. 2020) and the works citing the ApJ and
  Frontiers papers cite the *methods*, not the package. Citation contexts were used to separate
  substantive use from a bibliography entry; among the items considered, the five recorded above are
  the ones that show the software being used, credited, or described.
- **`10.3389/fspas.2020.00039`** (Laperre, Amaya & Lapenta 2020, "Dynamic Time Warping as a New
  Evaluation for Dst Forecast with Machine Learning"). Tempting, because AIDApy ships
  `aidapy/ml/metrics/dtw.py` and `dtw_m_e.py` implementing exactly that metric, the latter authored by
  Brecht Laperre. But a full-text probe restricted to that author returns only his 2019 conference
  abstract, not this paper: the article does not mention AIDApy, and the modules cite no publication.
  Rejected on the evidence, and recorded so the apparent connection is not mistaken for a citation.

### 28. Related Datasets (OPTIONAL)
**Values:**
- https://osf.io/48jyb/

**Source.** `examples/04_coronal_holes/README.rst` instructs the user to obtain the training data:
"Available data are `here <https://osf.io/48jyb/files/>`_. There are 3 choices, which contains
different amount of images to inference on: 1) **CoronalHoles.zip**: 300 images 2)
**CoronalHoles_test.zip**: 28 images 3) **Coronal_Holes_unsupervised_case**". The OSF API confirms the
project is public, titled "AIDA_CoronalHoles", described as "Coronal Holes Image Segmentation
Dataset", category `data`, created 2020-09-30 and last modified 2021-09-10. This is the dataset the
shipped coronal-hole configurations and the included UNet checkpoint were built on, so the software
supports functionality for it directly.

**No DOI exists for it.** OSF's identifiers endpoint returns no registered DOI for the project, and it
carries no licence. The value recorded is therefore the permanent project link. In APA form the
citation would be: AIDA Consortium. (2020). *AIDA_CoronalHoles: Coronal Holes Image Segmentation
Dataset* [Data set]. Open Science Framework. https://osf.io/48jyb/ — kept here in prose rather than
in the value, because the field itself can hold only the URL.

**The storage shape of a related item — the constraint that governs every related-item field (27,
28, 29 and 30) alike, stated here once.** Related publications, datasets and software are stored as
URL-shaped related items. The submitted value must be a real URL: free text is rejected by URL
validation, so a citation string is not an option. The URL is stored as both the item's identifier
and its display name, which caps it at 128 characters. A DOI URL is preferred and any permanent link
is acceptable — an ADS abstract page for a publication with no DOI (Field 27), an OSF project link
for a dataset with none (this field), a repository URL for software (Fields 29 and 30). Full
citations therefore belong in this file's prose and never in the field. Every related-item value
recorded in this record sits well inside the cap; the longest are the two 62-character ADS links in
Field 27.

**Considered and rejected.** `examples/03_gmm/reconnection_harris/mpi_script.py` and `gmm.ipynb` point
to a second OSF location for the double Harris sheet simulation data,
`https://osf.io/sh89u/?view_only=4e4fd8f513a34ebebdcca1747a505581`. That is an anonymous view-only
link: the OSF API returns "Authentication credentials were not provided" for node `sh89u`, so the
project is not public and cannot be cited as a persistent dataset reference. Recorded so a future
agent does not add an unresolvable link. The MMS, Cluster and OMNI datasets AIDApy reads are
identified through Fields 31 and 32 rather than listed here as individual data products.

### 29. Related Software (OPTIONAL)
**Values:**
- HelioPy — https://github.com/heliopython/heliopy
- heliopy-multid — https://gitlab.com/aidaspace/heliopy_multid
- SunPy — https://github.com/sunpy/sunpy

**Why each passes the relevance gate.**
- **HelioPy** is the package AIDApy's Mission tool wraps, and part of AIDApy is derived from it. The
  0.0.2 changelog entry reads "``aidapy.data.mission``: wrap *heliopy* to provide data from 3
  different missions (OMNI, cluster, and MMS) in *xarray* format";
  `doc/source/mission.rst` says the subpackage "is based on routines mainly adopted from HelioPy
  (https://heliopy.readthedocs.io/en/stable/) and SunPy packages ... and further developed", and
  "Because the core of the downloading process is based on the HelioPy package, we chose to borrow its
  file handling system"; and `aidapy/data/mission/modified_cluster.py` announces itself as a "Slight
  modification of the cluster method from HelioPy". That is a domain-specific dependency *and* a
  code-provenance relationship — exactly what this field is for.
- **heliopy-multid** is a companion package from the same project, purpose-built for AIDApy. Its PyPI
  metadata gives the summary "Extension to heliopy to retrieve multi-dimensional heliopheric data",
  author "AIDA Consortium" and homepage `https://gitlab.com/aidaspace/heliopy_multid`, and it lives in
  the same `aidaspace` GitLab group. AIDApy's mission modules import it directly
  (`import heliopy_multid.data.mms as mms` in `mms.py`, `heliopy_multid.data.cluster` in `cluster.py`,
  `heliopy_multid.data.util.convert_units_to_str` in `omni.py`), and the 0.0.2 changelog records
  "*heliopy_multid* is now a dependency".
- **SunPy** is a declared heliophysics dependency named in the documentation as a source of adopted
  routines (quoted above), and its data model is a documented intermediate in AIDApy's Mission
  pipeline: `aidapy/data/mission/base_mission.py`'s abstract `_download_ts` is documented as
  "Abstract method to download sunpy timeseries from heliopy", `mms.py` documents its `data` attribute
  as "dict of sunpy timeseries object", and `modified_cluster.py` documents a return type of
  `sunpy.timeseries.TimeSeries`. It is also a similar-purpose heliophysics data-access package, which
  is the field's core case.

**Excluded, with the reason.** The previous version of this record listed xarray, PyTorch,
scikit-learn, Optuna and Albumentations here. All five are generic infrastructure: they would be
equally at home in a web application, a finance model or a biology pipeline, and listing them says
nothing that is not equally true of most of the ecosystem. They are removed. Applying the same test to
every declared dependency at the pinned revision:

- *Generic scientific-Python and tooling stack, excluded outright* — from `setup.py`'s
  `install_requires`: `numpy`, `matplotlib`, `requests`, `more_itertools`, `chardet<4.0`,
  `bottleneck`, `h5netcdf`, and `extension` (a name that appears to be a packaging mistake — the PyPI
  project of that name is unrelated to anything AIDApy imports). From `requirements.txt`: `scipy`,
  `pandas`, `ConfigUpdater`, `coverage`, `pytest`, `Sphinx`, `sphinx_rtd_theme`. From the `ml` extra:
  `torch`, `torchvision`, `optuna`, `plotly`, `sklearn`, `h5py`, `joblib`, `tensorboard`,
  `albumentations`, plus `skorch` from `requirements.txt`. From the `vdf_cub` extra: `tricubic`. From
  `tests_require` and the `doc` extra, both development-only: `pylint`, `pytest-cov`, `ipython`,
  `ipykernel`, `nbsphinx` and `sphinxcontrib-apidoc`. Also `opencv` (imported as `cv2` by the
  coronal-hole and K-means modules but not declared at all).
- *`cdflib`* — declared in `install_requires` and used by `modified_cluster.py` to read Cluster CDFs.
  Closer to the domain than the stack above, but it is a file-format reader: reading CDF files is I/O
  plumbing, not a relationship that characterises this software, and the format itself is recorded in
  Field 18.
- *`astropy`* — a real API-boundary relationship rather than a similar-purpose tool, so it is recorded
  in Field 30 instead.
- *The LPP MATLAB routines* — `doc/source/event_search.rst` states the Event Search subpackage "is
  based on Matlab routines available at LPP and further developed". This is a genuine
  code-provenance relationship, but those routines have no public repository, DOI or landing page to
  link to, and MATLAB the product is not what the provenance refers to. Documented here instead of
  listed.
- *`notebooks_aida`* (`https://gitlab.com/aidaspace/notebooks_aida`, "Examples of using aidapy and
  scripts related to AIDA papers", cited as footnote 3 by Breuillard et al. 2020) — a companion
  *notebook collection* rather than software. Considered and left out; if HSSI later wants to surface
  worked examples, this is where they live.

### 30. Interoperable Software (OPTIONAL)
**Values:**
- xarray — https://github.com/pydata/xarray
- HelioPy — https://github.com/heliopython/heliopy
- heliopy-multid — https://gitlab.com/aidaspace/heliopy_multid
- astropy — https://github.com/astropy/astropy

**The specific exchange demonstrated in each case.** This field is not the dependency list; each entry
below names the artifact that shows a real exchange.

- **xarray** — the strongest case available, and an extension relationship rather than a dependency.
  AIDApy's entire user-facing analysis API is implemented as registered xarray accessors:
  `@xr.register_dataarray_accessor('statistics')` and `@xr.register_dataset_accessor('statistics')` in
  `aidapy/aidaxr/statistics.py`, plus `'graphical'` (`graphical.py`), `'process'` (`process.py`),
  `'vdf'` (`vdf.py`) and `'xevents'` (`xevents.py`). `load_data` returns an `xarray.Dataset`, which
  `doc/source/mission.rst` documents at length as the Mission subpackage's output and the interchange
  between subpackages — "The main output of the subpackage are xarray to be further used by other
  subpackages of the AIDApy package" — and `README.rst` states that AIDApy "inherits many features from
  high-level data structures such as xarray, and improves them by adding new ones". A user's own xarray
  objects gain AIDApy's methods, and AIDApy's outputs are ordinary xarray objects consumable by any
  xarray-based tool.
- **HelioPy** — bidirectional. AIDApy writes into HelioPy's own configuration file:
  `aidapy/aidafunc/set_load_config.py` imports `heliopy.util.config.get_config_file` and updates
  `download_dir` and `cluster_cookie` in `heliopyrc`. In the other direction,
  `aidapy/data/mission/modified_cluster.py` imports `from heliopy import config` and
  `from heliopy.data import util` and converts downloaded CDFs through `util.cdf2xr(...)`. Each side
  reads and configures the other.
- **heliopy-multid** — a companion package designed to be used with AIDApy (same consortium, released
  alongside it) supplying the multi-dimensional MMS and Cluster downloaders AIDApy's mission classes
  call directly, with unit conversion flowing back through
  `heliopy_multid.data.util.convert_units_to_str`. Listed in Field 29 as a companion and here for the
  functional exchange.
- **astropy** — an exchange at the public API boundary, not internal use. `load_data` and
  `event_search` accept `astropy.time.Time` objects as documented alternatives to
  `datetime.datetime`: `doc/source/mission.rst` says the time may be "an astropy.Time object allowing
  to handle multiple time format such as GPS, ISOT, or FITS", `aidapy/aidafunc/load_data.py` raises a
  `TypeError` naming both accepted types, and `base_mission.py` normalises inputs through
  `_to_astropy_time`. Separately, the user-facing `process.convert(dim, new_unit)` resolves its
  argument with `astropy.units.Unit`, so astropy unit strings drive a public method. This is the
  narrowest of the four entries — the evidence is type acceptance at the API boundary rather than a
  data-product round trip — and it is settled as included on exactly that evidence: a documented
  public signature that accepts an astropy type, and a public method that resolves astropy unit
  strings, are exchanges at the API boundary, which is what this field requires of a
  foundational-but-domain-adjacent package. Dependency presence alone would not have been enough.

**Excluded, with the reason.** SunPy is in Field 29 rather than here: there is no `import sunpy`
anywhere at the pinned revision, and its `TimeSeries` appears as an intermediate object produced by
HelioPy and consumed internally, documented in docstrings rather than offered as a user-facing
interchange. Everything in Field 29's exclusion list is excluded here too, on the same test — being a
dependency is not interoperability, and a claim that would read identically for an arbitrary Python
package carries no information. Two justifications were specifically avoided: "part of the standard
scientific Python ecosystem", and "a PyHC community package, so it interoperates with PyHC packages" —
neither is a demonstrated interoperation with any particular package.

### 31. Related Instruments (OPTIONAL)

Every entry resolves to a SPASE identifier from HSSI's controlled instrument/observatory vocabulary.
A name without an identifier is not recorded under any circumstances: there is no free-type path, and
an identifierless entry either binds to an arbitrary same-name row or creates a new identifierless
one.

**The evidence base.** `aidapy/data/mission/mission_settings/mms.json` and `cluster.json` are the
product catalogues that drive the MMS and Cluster downloads, and every one of their product entries
names the instrument it comes from in an `"instr"` key (22 entries and 8 respectively at the pinned
revision). The third catalogue, `omni.json`, names no instrument at all — each of its three entries
carries `"instr": "low"` — which fits OMNI being a derived multi-mission product rather than an
observatory with instruments; Field 32 sets out why it is not listed there.
`doc/source/mission.rst` establishes the spacecraft range: "Probes that can
be selected are probe1, probe2, probe3 and probe4 for MMS and Cluster and probe1 for OMNIWeb", and the
CDF keys are templated per probe (`mms${probe}_fgm_b_${coords}_${mode}_l2`,
`B_vec_xyz_${coords}__C${probe}_CP_FGM_${mode}`). The curlometer requires all four spacecraft
simultaneously. Instrument rows in the vocabulary exist only per spacecraft, so a genuinely
four-spacecraft capability resolves to four rows. External corroboration for the MMS instruments:
Breuillard et al. (2020) describe "loading the raw MMS magnetic field and plasma moments data from FGM
and FPI instruments ... using the aidapy package".

**MMS Fluxgate Magnetometer** — from `"dc_mag"` with `"instr": "fgm"`, the package's primary product
(the default `data_types` of both the MMS and Cluster managers, and the input to the curlometer, the
event search and the VDF reference frames).
- Name: `MMS FIELDS/FGM` — https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/FGM
- Name: `MMS FIELDS/FGM` — https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/FGM
- Name: `MMS FIELDS/FGM` — https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/FGM
- Name: `MMS FIELDS/FGM` — https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/FGM

**MMS Fast Plasma Investigation, ion sensor** — from the ten `"instr": "fpi"` products with a
`"dis-"` product string: ion density, bulk velocity, parallel and perpendicular temperature,
pressure and temperature tensors, heat flux, omnidirectional energy spectrum, energy channel table,
and the 3D ion distribution that the whole VDF subpackage operates on.
- Name: `MMS FPI/DIS` — https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DIS
- Name: `MMS FPI/DIS` — https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DIS
- Name: `MMS FPI/DIS` — https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DIS
- Name: `MMS FPI/DIS` — https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DIS

**MMS Fast Plasma Investigation, electron sensor** — from the seven `"des-"` products: electron
density, bulk velocity, parallel and perpendicular temperature, temperature tensor, the 3D electron
distribution, and the electron heat flux (`e_heatq`) added in release 0.0.4.
- Name: `MMS FPI/DES` — https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DES
- Name: `MMS FPI/DES` — https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DES
- Name: `MMS FPI/DES` — https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DES
- Name: `MMS FPI/DES` — https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DES

**MMS Electric field Double Probe** — from `"dc_elec"` with `"instr": "edp"`, reading
`mms${probe}_edp_dce_${coords}_${mode}_l2`, the Level-2 DC electric field.
- Name: `Electric field Double Probe` — https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MMS1/EDP
- Name: `Electric field Double Probe` — https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MMS2/EDP
- Name: `Electric field Double Probe` — https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MMS3/EDP
- Name: `Electric field Double Probe` — https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MMS4/EDP

These four were, when this record was compiled, the vocabulary's only rows for the EDP instrument as
such; they come from the CNES CDPP-AMDA namespace rather than SMWG. A non-SMWG match is still a
correct resolution when it is the only row for the entity. The SMWG namespace instead carries EDP's
two sensor pairs separately — `MMS FIELDS/SDP` (`.../SMWG/Instrument/MMS/n/FIELDS/SDP`) and
`MMS n FIELDS Suite, Axial Double Probe` (`.../SMWG/Instrument/MMS/n/FIELDS/ADP`). Those were considered
and not used: the repository names the combined `edp` instrument and its `dce` product, not one
sensor pair, and attributing the product to SDP or ADP individually would be an inference the
repository does not support.

**MMS Active Spacecraft Potential Control** — from `"i_aspoc"` with `"instr": "aspoc"`, reading
`mms${probe}_aspoc_ionc`, described in `mission_settings/mms.json` as "Spacecraft potential control
ion current" and in `doc/source/mission.rst` as "ASPOC instrument ion current".
- Name: `MMS ASPOC` — https://spase-metadata.org/SMWG/Instrument/MMS/1/InstrumentControl/ASPOC
- Name: `MMS ASPOC` — https://spase-metadata.org/SMWG/Instrument/MMS/2/InstrumentControl/ASPOC
- Name: `MMS ASPOC` — https://spase-metadata.org/SMWG/Instrument/MMS/3/InstrumentControl/ASPOC
- Name: `MMS ASPOC` — https://spase-metadata.org/SMWG/Instrument/MMS/4/InstrumentControl/ASPOC

**MMS ephemeris and attitude** — from `"sc_pos"` and `"sc_att"`, both with `"instr": "mec"`, reading
`mms${probe}_mec_r_${coords}` and `mms${probe}_mec_quat_eci_to_${frame}`. Spacecraft position drives
the magnetotail location criterion in `_settings_df`, and the attitude quaternions are what
`aidapy/aidaxr/vdf.py` builds all of its reference-frame rotations from.
- Name: `MMS Positions` — https://spase-metadata.org/SMWG/Instrument/MMS/1/Ephemeris
- Name: `MMS Positions` — https://spase-metadata.org/SMWG/Instrument/MMS/2/Ephemeris
- Name: `MMS Positions` — https://spase-metadata.org/SMWG/Instrument/MMS/3/Ephemeris
- Name: `MMS Positions` — https://spase-metadata.org/SMWG/Instrument/MMS/4/Ephemeris

No row in the vocabulary carried "MEC" or "Magnetic Ephemeris" in its name or identifier when this
record was compiled, so MMS's MEC instrument has no dedicated record; the per-spacecraft `Ephemeris`
rows are the ephemeris and attitude records the `mec` products correspond to. This is a defensible
mapping rather than a name match, and it is settled in favour of keeping the four rows. The
alternative — dropping them and letting the MMS observatory association in Field 32 carry the
ephemeris products — was considered and not taken: the `mec` products are loaded per probe,
spacecraft position drives the magnetotail criterion in `_settings_df` and the attitude quaternions
drive the VDF reference-frame rotations, so a user searching at instrument level for MMS ephemeris
and attitude should find AIDApy.

**Cluster Fluxgate Magnetometer** — from `cluster.json`'s `"dc_mag"` and `"sc_pos"`, both with
`"instr": "fgm"`, reading `B_vec_xyz_${coords}__C${probe}_CP_FGM_${mode}` and
`sc_pos_xyz_gse__C${probe}_CP_FGM_${mode}`. The four SMWG rows are named by flight model rather than
by number (Rumba = Cluster 1, Salsa = 2, Samba = 3, Tango = 4).
- Name: `Fluxgate Magnetometer` — https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/FGM
- Name: `Fluxgate Magnetometer` — https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/FGM
- Name: `Fluxgate Magnetometer` — https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/FGM
- Name: `Fluxgate Magnetometer` — https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/FGM

**Cluster Ion Spectrometry** — from `cluster.json`'s six `"instr": "cis"` products (ion density, bulk
velocity, total/parallel/perpendicular temperature and the 3D ion distribution).
- Name: `Cluster Ion Spectrometry` — https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/CIS
- Name: `Cluster Ion Spectrometry` — https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/CIS
- Name: `Cluster Ion Spectrometry` — https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/CIS
- Name: `Cluster Ion Spectrometry` — https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/CIS

A finer alternative was considered and not used. The repository's CDF keys name the CIS **HIA**
sub-sensor specifically (`CP_CIS-HIA_ONBOARD_MOMENTS`, `CP_CIS-HIA_HS_MAG_IONS_PF`), and the
vocabulary carried two HIA-specific rows when this record was compiled, both named
`Cluster Ion Spectrometry : Hot Ion Analyser`, at
`https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Cluster1/CIS-HIA` and
`https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Cluster3/CIS-HIA` — for Cluster 1 and Cluster 3
only. Choosing those would be more precise about the sensor but would silently narrow the association
to two spacecraft, whereas the repository templates all four probes and `doc/source/mission.rst`
documents probe1 through probe4. The four SMWG `Cluster Ion Spectrometry` rows are therefore the
settled choice: they are the canonical instrument records covering the documented probe range. The HIA
rows are recorded here as the rejected alternative, so that a future agent recognises the coarser
choice as deliberate rather than as a refinement that was missed.

**Correction to the previously recorded values.** The previous version of this record listed "MMS
(Magnetospheric Multiscale Mission)", "Cluster" and "SDO/AIA (Solar Dynamics Observatory /
Atmospheric Imaging Assembly)" here, each with "Instrument Identifier: Not found". The first two are
missions, not instruments, and belong in Field 32; all three lacked identifiers and so were not
submittable. The instrument-level values above are re-derived from the product catalogues that
actually name instruments.

**Considered and rejected: SDO/AIA at instrument level.** `README.rst` and
`examples/04_coronal_holes/README.rst` refer only to "SDO images"; nothing in the repository names AIA,
a data level or a FITS product. The one wavelength-like string anywhere in it is a local input
directory path, `'../DATA/images_channel_2014/193'`, in `config_coronal_holes_unspr.yml` and in
`aidapy/ml/tests/test_dataload.py` — a folder the user populates, named after an AIA channel but not
read as one by any code path, since the loader takes whatever images the directory holds.
`aidapy/ml/data/coronalholes.py` reads three-channel JPEG
files from a local directory, and the training set is distributed as image archives (Field 28). There is
no instrument-specific parser or convention to point at, so no instrument row is recorded. The
observatory-level association was considered too, and rejected on the same evidence; Field 32 sets out
why. Do not add an AIA row without new evidence naming the instrument.

**Considered and rejected: other MMS and Cluster instruments.** The vocabulary carries rows for MMS
EIS, FEEPS, HPCA, EDI, SCM and DSP, and for Cluster ASPOC, EFW, DWP and CIS-CODIF among others. None
appears in either product catalogue at the pinned revision, and AIDApy provides no loader for them.

**Considered and rejected: Wind and Parker Solar Probe.** `doc/source/extreme_events.rst` states that
the `xevents` analysis "has been tested here on direct numerical simulations of turbulence, by using
the virtual spacecraft technique (WP5), and to satellite data such as Wind, Magnetospheric Multiscale
(**MMS**) mission, and Parker Solar Probe." The `xevents` module is mission-agnostic — it operates on
any xarray time series — and AIDApy's Mission tool provides no Wind or PSP loader. "Tested on" is
precisely the kind of mention this field excludes. Recorded so the sentence is not later read as
support for those missions.

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** Magnetospheric Multiscale
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MMS

**Observatory 2:**
- **Observatory Name:** Cluster
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Cluster

**Why each is designed-to-support.**
- **Magnetospheric Multiscale** — already stored, and the mission AIDApy supports most deeply: a
  22-product catalogue in `mission_settings/mms.json`, a dedicated data manager
  (`aidapy/data/mission/mms.py`), MMS-specific VDF interpolation and reference-frame machinery, both
  event-search presets (`_settings_df` and `_settings_edr` set `"mission": "mms"`), an MMS SITL report
  parser (`aidapy/tools/sitl_parsing.py`), and MMS-specific tests
  (`aidapy/tests/test_vdf_mms.py`, `aidapy/aidaxr/tests/test_vdf_mms.py`).
- **Cluster** — added by this refresh. `aidapy/data/mission/cluster.py` and `modified_cluster.py`
  implement a dedicated manager that downloads from the Cluster Science Archive;
  `mission_settings/cluster.json` is an eight-product catalogue; `doc/source/mission.rst` lists
  Cluster among the three selectable missions and gives it Level-3 `j_curl`, `i_beta`, `e_beta` and
  `mag_elev_angle` products; and `set_load_config(cluster_cookie=...)` exists specifically to
  configure Cluster archive access.

**Considered and rejected: Solar Dynamics Observatory**
(`https://spase-metadata.org/SMWG/Observatory/SDO`). The case for it is real and was weighed, not
overlooked. `README.rst` advertises "the automatically detection of coronal holes in SDO images" as one
of two headline use cases; `examples/04_coronal_holes/README.rst` is titled "Coronal Holes segmentation
in SDO images"; and the repository ships six configurations plus a trained UNet checkpoint for that use
case. It is rejected because it fails this field's designed-to-support test.
`aidapy/ml/data/coronalholes.py` reads generic three-channel JPEG files from a local directory the user
populates by hand from an OSF archive (Field 28). There is no SDO data-access path, no FITS reader, and
no instrument or data-level convention anywhere in the package; the only wavelength-like string in it
is the user-supplied directory path recorded in Field 31 — nothing in the loader
would behave differently if the images had come from another source, or from no telescope at all. SDO
is the provenance of the training data, not an observatory the software is built to serve. Field 31
reached the same conclusion at instrument level when it rejected SDO/AIA, and keeping the observatory
while rejecting the instrument would have been the inconsistent outcome. The coronal-hole science stays
findable through the `coronal holes` keyword (Field 16), the `Corona` and `Solar Environment` rows
(Field 5), the `Solar Corona` phenomenon (Field 22), the OSF dataset (Field 28), and the
image-processing and ML values in Field 4. Do not re-add the observatory without evidence of an
SDO-specific code path.

**Resolution notes.** Each name is copied verbatim from the matched row. Both resolved to a single SMWG
row for the entity: `SMWG/Observatory/MMS` (abbreviation "MMS") and `SMWG/Observatory/Cluster`. The
vocabulary also holds per-spacecraft
rows — `SMWG/Observatory/MMS/1` through `/4`, and `SMWG/Observatory/Cluster-Rumba` through
`-Tango` — and duplicate CNES CDPP-AMDA and CDPP-Archive entries for the same missions. The
per-spacecraft rows are different entities, not duplicates, and the mission-level row is the right
granularity here because AIDApy supports each mission as a whole across all four probes; the CNES
rows are alternative catalogue entries for the same entity, resolved in favour of SMWG. Note that the
rendered site value for Magnetospheric Multiscale appears as "Magnetospheric Multiscale (MMS)", which
is the row's name and abbreviation composed for display, not the stored name.

**Considered and rejected: OMNI / OMNIWeb as an observatory.** OMNI is a derived, multi-mission
near-Earth solar-wind dataset rather than an observatory or mission, and the form's own instruction
routes a multi-mission data source to Field 17, where `OMNIWeb` is now recorded. Listing it here would
associate AIDApy with an entity SPASE does not model as an observatory.

### 33. Logo (OPTIONAL)
**Value:** https://gitlab.com/aidaspace/aidapy/-/raw/d023f091a9cdf07fb48f232b654a4e15913b668c/doc/source/fig/logo_AIDA.png

**Source.** `doc/source/conf.py` line 142 sets `html_logo = 'fig/logo_AIDA.png'`, so this image is the
logo AIDApy's own published Sphinx documentation displays. `doc/source/fig/` also holds
`logo_aida_small.png` and `favicon_aida.png` (the latter set as `html_favicon`).

**Fetch-verified.** The URL serves `content-type: image/png` with `content-length: 108360`, and the
bytes are a genuine PNG: 3189 x 3189, 8-bit RGBA, non-interlaced. This check matters because a raw
repository URL can resolve successfully while serving `text/plain` — a pointer file rather than image
bytes — which is a common way a logo URL looks valid and renders as nothing. That is not the case
here.

**Why the URL is pinned to a commit.** GitLab's `/-/raw/master/...` form also serves the image today,
but it follows the default branch and would change or break if the file moved. The commit-pinned form
above is immutable, which is what a "permanent place" means for this field. It is 111 characters,
within the 200-character limit that URL columns impose at the database level.

**Caveat.** This is the AIDA *project* logo, not a logo drawn for AIDApy specifically — the filename,
the AIDA-branded favicon beside it, and the shared `logo_aida_small.png` all indicate project
branding. It is nevertheless the image the software's own documentation presents as its logo, which is
what this field asks for. No AIDApy-specific logo exists in the repository at the pinned revision, and
the PyHC registry entry has no `logo:` key. The value is settled as recorded: the project logo that
the software's own documentation displays is a better answer to this field than an empty value, and
the caveat is kept here so that the provenance of the image is not mistaken.

**This field held no value in HSSI until this refresh.**

---

## Metadata Agreement (MANDATORY)
**Status:** To be agreed to by the actual submitter.

---

## Cross-cutting notes worth keeping

**The repository cannot be installed from `requirements.txt` as written.** Its last line is
`git+git://github.com/hbreuill/heliopy@0074817#egg=heliopy` — a personal fork of HelioPy pinned to a
commit, fetched over the `git://` protocol that GitHub disabled in 2022. `setup.py` meanwhile requires
upstream `heliopy>=0.12.0`. The two declarations disagree about which HelioPy is needed, and the fork
is probably the operative one: `modified_cluster.py` calls `heliopy.data.util.cdf2xr`, which is not
part of upstream HelioPy's public API. This does not change any field value, but it explains why the
package's dependency story looks inconsistent and should not be "corrected" by assuming upstream
HelioPy suffices.

**Two example use cases import a module the package does not contain.**
`examples/03_gmm/reconnection_harris/mpi_script.py` does
`from aidapy.ml.gmm import leggi_h5, clustering`, and `gmm.ipynb` depends on its output. No
`aidapy/ml/gmm.py` exists at the pinned revision. The 0.0.2 changelog records that `aidapy.ml`
provided "basic classes providing multi layer perceptrons and GMM for particle distribution analysis",
so the GMM code was present in the first release and was refactored away by the time of this revision;
the surviving clustering capability lives in `aidapy/external/unsupmr/` (K-means and DBSCAN) and
`aidapy/ml/models/kmeans.py`. The Gaussian-mixture functionality is therefore claimed by the examples
and the changelog but not present in the shipped package — relevant to any future reading of Field 4.

**The repository contains a hard-coded credential.** `aidapy/data/mission/cluster.py`,
`modified_cluster.py` and `.gitlab-ci.yml` each embed the same literal Cluster Science Archive cookie.
Recorded only so that a future agent recognises it as a checked-in secret rather than a configuration
value worth extracting into metadata; `set_load_config(cluster_cookie=...)` is the intended mechanism.

**PyHC registration.** AIDApy is in PyHC's **community** list, `_data/projects.yml` in
`heliophysicsPy/heliophysicsPy.github.io` — not `projects_core.yml` and not
`projects_unevaluated.yml`. Its curated entry supplies `code`, `docs`, `description`, `contact`,
`keywords: [machine_learning, heliosphere, data_analysis]`, and quality ratings of "Good" for licence
and Python 3 and "Partially met" for community, documentation, testing and software maturity. The
"Partially met" software-maturity rating was the previous version of this record's stated basis for a
`WIP` development status; Field 23 explains why that inference does not hold.
