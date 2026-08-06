# HSSI Metadata Extraction Results

**HSSI Software ID:** cf802366-d886-45a5-bd49-2566521a4bbe
**Repository:** https://github.com/rmcgranaghan/Helio-KNOW
**Source Revision:** 31ef4240a251a10ccf8d6ff4db994fa6e0ebe366
**Extraction Date:** 2026-08-04
**Validation Date:** 2026-08-05
**Validation Status:** PASS

---

**Scope note — read this before the evidence below.** Helio-KNOW is not a single installable package. It is a monorepo holding four distinct kinds of artifact, each with its own authorship, language, and maturity:

- `data-models/` — the HelioKNOW suite of SKOS/OWL ontologies (`hk_core.ttl`, `hk_phenomenon.ttl`, `hk_region.ttl`, `hk_model.ttl`, `hk_instruments.ttl`), a region-based taxonomy contributed to the Unified Astronomy Thesaurus, and the Center for HelioAnalytics (CfHA) community ontology. These are the project's flagship deliverable and the most substantial machine-readable content in the repository (`hk_instruments.ttl` alone is ~95,000 lines).
- `tools/` — six independent tool directories, almost entirely Jupyter notebooks: SSCWeb ephemeris/availability scraping, DMSP SSJ CDF reading and plotting, machine-learning analysis of auroral particle precipitation, NASA ADS literature harvesting and citation-network analysis, NLP over heliophysics texts, and glossary/phenomena vocabulary harmonization.
- `data-pipelines/` — one notebook that semantically lifts CDAWeb observational data toward the knowledge graph.
- `interfaces/` — a Java/RDF4J knowledge-graph server (WAR) and a Plotly data-availability dashboard notebook.

Two consequences shape every field below. First, the tools are **research notebooks, not a distributable library**: many carry hard-coded absolute paths under `/Users/ryanmcgranaghan/...` or `/Users/ryanmc/...`, and several sections are explicit placeholders (`# FORTHCOMING...`). Functionality claims below therefore cite the notebook and cell that implements a capability, and deliberately exclude capabilities that exist only as TODO items. Second, the ontologies' **subject coverage is much broader than the tools' subject coverage** — the region taxonomy spans the solar interior through the magnetotail while the tools work almost entirely on the auroral high-latitude ionosphere. Field 5 (Related Region) records both and labels which is which, because a reader who assumes one scope will misread the other.

A third point of orientation: a repository whose core product is *knowledge representation* maps awkwardly onto the HSSI Software Functionality taxonomy, which has no category for ontologies, controlled vocabularies, or semantic modelling. Field 4 explains how that gap was handled, so a future agent does not read the absence of a "semantics" category as an extraction miss.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Not derivable from the repository. The submitter is the person making the submission rather than a property of the software, and no file, commit, or documentation in the repository designates one.

### 2. Persistent Identifier (RECOMMENDED)
**Not found.**

Negative research, so a future agent does not repeat it: there is no `CITATION.cff`, `codemeta.json`, `.zenodo.json`, or `CITATION` file — and `git log --all --diff-filter=A` confirms none has ever existed on any branch. `README.md` carries no DOI badge and no citation section. A repository-wide regex sweep for `10.\d{4,9}/...` returned only third-party DOIs: reference citations in notebook markdown, ADS/OpenAlex query results captured in notebook output, and DOI strings inside the harvested vocabulary data files (`tools/ADS_enrichment/data/*`). None is a persistent identifier for this software. There is no Zenodo–GitHub integration, and the project has never cut a release for Zenodo to mint against (see Field 12).

Concretely: no concept DOI and no other persistent identifier exists for this software, so this field is correctly empty. One can exist only once the project mints it — through a Zenodo release, or a DOI registered directly with a provider — and neither has happened.

### 3. Code Repository (MANDATORY)
`https://github.com/rmcgranaghan/Helio-KNOW`

Confirmed two ways: it is the `origin` remote of the pinned clone (`https://github.com/rmcgranaghan/Helio-KNOW.git`), and the GitHub API's `full_name` is `rmcgranaghan/Helio-KNOW`. The repository is public, not archived, not disabled, and its default branch is `main`. The URL resolves with no redirect to a renamed or transferred repository.

### 4. Software Functionality (MANDATORY)

**Coordinate Transforms**
**Coordinate Transforms: Ionospheric**
**Coordinate Transforms: Magnetospheric**
**Data Processing and Analysis**
**Data Processing and Analysis: Analysis**
**Data Processing and Analysis: Data Access and Retrieval**
**Data Processing and Analysis: Data Reduction**
**Data Processing and Analysis: Energy Spectra**
**Data Processing and Analysis: File Format Conversion**
**Data Processing and Analysis: ML/AI**
**Data Processing and Analysis: Processing**
**Data Processing and Analysis: Spectrogram**
**Data Processing and Analysis: Time Series Analysis**
**Data Visualization**
**Data Visualization: 2D Graphics**
**Data Visualization: 3D Graphics**
**Data Visualization: Line Plots**
**Data Visualization: ML/AI**
**Data Visualization: Orbit Plots**
**Data Visualization: Spectrogram**
**Data Visualization: Web-Based**
**Models and Simulations**
**Models and Simulations: Data Guided**
**Models and Simulations: Empirical**
**Models and Simulations: Field-line Tracing**
**Models and Simulations: ML/AI**
**Servers and Environments**
**Servers and Environments: Data servers processing and handling**

Every subcategory listed appears together with its parent top-level category, which the hierarchical `Parent: Child` function-category list requires.

This field was previously recorded as the single category `Models and Simulations`. That value is **justified but severely under-specified**, and the list above supersedes it.

*Why `Models and Simulations` is justified.* Three distinct pieces of model machinery are actually invoked, not merely catalogued:
- `tools/tools_for_SSCWeb/SSCWeb_Scraper.ipynb` constructs `BFieldModel(external=Tsyganenko89cBFieldModel())` and passes it into every `DataRequest`, so each ephemeris record is produced in the Tsyganenko 1989c empirical external field.
- `tools/ML/DMSP_CDFfile_analysis.ipynb` instantiates `ovation_prime.FluxEstimator('diff', energy_or_number='energy')` and calls `get_flux_for_time(...)` to generate OVATION Prime auroral flux fields on an MLAT/MLT grid.
- The same notebook loads trained Keras/TensorFlow neural networks and a LightGBM model from `.h5`/pickle artifacts and evaluates them to predict auroral electron energy flux.

*Why that was the only value previously recorded, and why it is wrong.* The repository's dominant activity — knowledge representation, vocabulary harmonization, literature network analysis, data retrieval, and visualization — is absent from that single category entirely. `data-models/hk_model.ttl` compounds the confusion: it is a SKOS vocabulary of roughly 90 named heliophysics models (BATSRUS-family MHD codes, IRI, IGRF, MSIS, WSA, PFSS, ENLIL, TIEGCM, SAMI3, RAM-SCB…), each with `owl:versionInfo` and a landing page. A reader skimming that file could conclude the repository *implements* MHD or first-principles models. **It does not.** `hk_model.ttl` describes models; no solver, no PDE integrator, and no MHD code exists anywhere in the repository. `Models and Simulations: MHD`, `: First Principles`, `: Physics-Based`, and `: Theory` were therefore all considered and rejected — this is the single most likely misclassification for this repository and is recorded here so it is not reintroduced.

Evidence for each selected value:

- **Coordinate Transforms** / **: Magnetospheric** — `SSCWeb_Scraper.ipynb` requests `CoordinateOptions(CoordinateSystem.GEO, ...)` and `CoordinateOptions(CoordinateSystem.GM, ...)` for latitude, longitude, and local time, then writes both geographic and geomagnetic coordinates into the per-spacecraft ephemeris CSVs. The notebook writes a provenance `README_1987.txt` that documents both frames verbatim from the SSCWeb users' guide, which confirms the multi-frame output is an intended user-facing product rather than an incidental request parameter. The IMF components read in `tools/ML/DMSP_CDFfile_analysis.ipynb` (`BY_GSM`, `BZ_GSM`) and in `community/storymaps/dataExploration.ipynb` (`bx_gsm`, `by_gsm`, `bz_gsm`) are handled in GSM.
- **Coordinate Transforms: Ionospheric** — AACGM magnetic coordinates and magnetic local time are the working frame throughout the DMSP work: `tools/DMSP_SSJ_tools/DMSP_SSJ_utils.ipynb` extracts `SC_AACGM_LAT`, `SC_AACGM_LON`, `SC_AACGM_LTIME` and converts MLT to a polar angle (`df_plot_NH['SC_AACGM_LTIME'] / 24. * (2*np.pi) - np.pi/2`); `DMSP_CDFfile_analysis.ipynb` builds `sin_mlt_grid`/`cos_mlt_grid` features from MLT; `SSCWeb_Scraper.ipynb` requests north and south `BFieldTraceOptions` footpoint latitudes and longitudes, i.e. maps each spacecraft to its ionospheric footpoint; and `community/storymaps/dataExploration.ipynb` documents an AACGM equal-area grid together with the MLT-to-AACGM-longitude shift needed to interpret it.
- **Data Processing and Analysis: Data Access and Retrieval** — four independent remote-retrieval paths: `cdasws.CdasWs` calls `get_variable_names` and `get_data` against CDAWeb (`data-pipelines/particle_precipitation_data_pipeline_experiment_v1.ipynb`); `sscws.SscWs` calls `get_observatories` and `get_locations` against SSCWeb (both `tools/tools_for_SSCWeb/` notebooks); `geospacepy.omnireader.omni_interval` retrieves OMNI 5-minute and hourly solar-wind and index data (`DMSP_CDFfile_analysis.ipynb`); and `tools/LitNetworkBuilder/LitNetworkBuilder_harvester.py` plus `tools/ADS_enrichment/doADS_API_Query.{py,ipynb}` page through the NASA ADS `search/query` API with bearer-token authentication. `tools/ADS_enrichment/openAlex_explorer.ipynb` queries OpenAlex, and `tools/NLP/web_scraper_PDFs.ipynb` harvests PDFs from a conference programme page.
- **Data Processing and Analysis: File Format Conversion** — `dmsp_ssj_cdf_to_dataframe()` and `DMSP_SSJ_CDF_to_DataFrame()` read CDF via `spacepy.pycdf` and emit pandas DataFrames and CSV files. On the semantic side, `tools/glossary_harmonization/phenomena_harmonization.ipynb` and `compile_terms_definitions.ipynb` ingest JSON glossaries, CSV hierarchies, XLSX term lists, and RDF/Turtle (GEMET `.rdf`, SWEET `.ttl`, UAT) and emit unified CSV; `tools/ADS_enrichment/generate_uat_leaf_nodes.ipynb` parses `uat.ttl` and writes `uat_leaf_terms.csv`; `tools/AutOntologyTool/CfHA_Parsing_Heliophysics_data.ipynb` serializes an rdflib graph to OWL.
- **Data Processing and Analysis: ML/AI** — supervised regression of auroral electron energy flux: Keras/TensorFlow neural networks (`KerasRegressor`, `EarlyStopping`, `ModelCheckpoint`, `load_model` with a custom objective) and LightGBM, with a pickled input-feature scaler, evaluated across a 70-feature input vector (`DMSP_CDFfile_analysis.ipynb`). Unsupervised and NLP machine learning appears in `tools/AutOntologyTool/CfHA_Parsing_Heliophysics_data.ipynb`: TF-IDF vectorization, Word2Vec via gensim, `sklearn.cluster` agglomerative and k-means clustering, t-SNE via `sklearn.manifold`, and a spaCy NER model trained on a heliophysics corpus with train/test evaluation against the untrained baseline.
- **Data Processing and Analysis: Time Series Analysis** — datetime-indexed DataFrames throughout; `pd.to_datetime` indexing, time-range subsetting, a `nearest()` helper for nearest-timestamp matching between DMSP and solar-wind series, `pd.date_range(..., freq="5min")` prediction grids, and `resample('5T').pad()` with `ffill()` to bring hourly F10.7 onto the 5-minute cadence (`DMSP_CDFfile_analysis.ipynb`). `tools/NLP/lit_database_growth_calculator.ipynb` computes compound literature-growth projections.
- **Data Processing and Analysis: Energy Spectra** — `CHANNEL_ENERGIES` is read from each SSJ CDF and used to label and axis-scale the per-channel differential energy flux, and `ELE_DIFF_ENERGY_FLUX`/`_STD` are expanded into one column per channel energy so flux-versus-energy can be worked with directly (`DMSP_SSJ_utils.ipynb`, `exploreSSJ_notebook.ipynb`, `DMSP_CDFfile_analysis.ipynb`). `ELE_AVG_ENERGY` and `ELE_TOTAL_ENERGY_FLUX` are the integrated spectral quantities.
- **Data Processing and Analysis: Spectrogram** — `exploreSSJ_notebook.ipynb` assembles the time–energy representation before rendering it: it selects the differential-flux columns, transposes to `[n_energy × n_time]`, replaces zeros with NaN, and builds `np.meshgrid(plot_dts, channel_energies)`. `particle_precipitation_data_pipeline_experiment_v1.ipynb` does the equivalent with `np.ma.masked_where` on zeros and NaNs before a log-normed `pcolormesh`. This is the borderline case between processing and visualization; both are listed because array construction and rendering are separate, identifiable steps here.
- **Data Processing and Analysis: Data Reduction** — high-latitude subsetting (`df = df[df['SC_AACGM_LAT'] >= np.abs(45)]`, `df_f17_reduced[df_f17_reduced['SC_AACGM_LAT'] > 45.]`), hemisphere splitting into `df_plot_NH`/`df_plot_SH`, temporal downsampling of the OMNI hourly series onto a 5-minute grid, and a coarse-versus-fine grid switch (`grid_res = 'fine' | 'coarse'`) that trades resolution for volume.
- **Data Processing and Analysis: Analysis** — derived scientific quantities and statistics rather than plain transformation: the Newell coupling function (`NewellCF_calc(vsw, Bz, By)`) and the Borovsky coupling parameter (`omnireader.borovsky`) computed from solar-wind inputs; graph centrality and degree statistics over citation networks (`LitNetworkBuilder_networkBuilder.py` writes a `NetworkMetrics/` directory); TF-IDF term importance; and the coverage/gap analysis in `phenomena_harmonization.ipynb` that cross-references HelioKNOW phenomena against a dozen external glossaries and emits `phenomena_helioknow_coverage.csv` and `phenomena_gaps_not_in_helioknow.csv`.
- **Data Processing and Analysis: Processing** — `data-pipelines/` is a pipeline directory by design ("Scripts and systems for transforming and visualizing heliophysics data (e.g., 'semantically lifting' datasets into a given data schema/model, instantiating knowledge graphs)"), and the multi-stage glossary harmonization notebook is a pipeline in the ordinary sense: parse TTL, load each glossary, normalize terms, flag candidates, cross-reference, unify, export.
- **Data Visualization: 2D Graphics** — `plt.contourf` with `ticker.LogLocator`, `ax.pcolormesh` with `LogNorm`, polar `ax.scatter` maps in MLT/colatitude with custom radial and circumferential tick labelling, and `matplotlib.patches`/`PatchCollection` wedge rendering of an equal-area AACGM grid (`dataExploration.ipynb`).
- **Data Visualization: Line Plots** — `plt.plot` of SymH and of the IMF `bx`/`by`/`bz` components against time (`DMSP_CDFfile_analysis.ipynb`, `dataExploration.ipynb`).
- **Data Visualization: Spectrogram** — the log-scaled energy-versus-time flux images described above, rendered with `contourf` and `pcolormesh` and a log y-axis in eV.
- **Data Visualization: 3D Graphics** and **: Orbit Plots** — `tools/tools_for_SSCWeb/SscWsExample.ipynb` imports `mpl_toolkits.mplot3d.Axes3D`, opens a `projection='3d'` axis, and plots `coords['X'], coords['Y'], coords['Z']` titled `<Id> Orbit (<CoordinateSystem>)`. This is a spacecraft trajectory rendered in three dimensions, which is precisely both categories.
- **Data Visualization: Web-Based** — `interfaces/data_availability_dashboard/Helio-KNOW_data_availability_dashboard.ipynb` builds an interactive Plotly figure (`plotly.express.scatter` plus `plotly.graph_objects`, `template='plotly_white'`, hover data, continuous colour axis) over a melted platform × date availability table; `tools/NLP/text_explorer.ipynb` also uses `plotly.graph_objects`. Separately, `interfaces/User_Interface_with_Interactive_Knowledge_Graph/` is a browser-facing interactive knowledge-graph explorer whose README describes the React frontend it was built to serve.
- **Data Visualization: ML/AI** — `DMSP_CDFfile_analysis.ipynb` plots the three model prediction series (`predictions-NN MAE`, `predictions-NN DRMAE`, `predictions-LGBM`) against the DMSP observations in a shared multi-panel figure with auroral-boundary annotation. Selected specifically for model-output-versus-observation display, not for generic plotting.
- **Models and Simulations: Empirical** — Tsyganenko 1989c external field and OVATION Prime, both empirical/statistical models, as cited above.
- **Models and Simulations: Field-line Tracing** — four `BFieldTraceOptions` entries request north and south hemisphere footpoint latitude and longitude in GEO and GM, traced through the Tsyganenko field. Listed under Models and Simulations rather than under `Data Processing and Analysis: Field-line Tracing` because the tracing is performed in a *model* field, which is the distinction the two categories draw; the data-processing variant was considered and rejected on that basis.
- **Models and Simulations: ML/AI** — the loaded neural-network and LightGBM models act as surrogate models of auroral particle precipitation, predicting flux on an MLAT/MLT grid; the notebook's own framing is comparison of these against OVATION Prime.
- **Models and Simulations: Data Guided** — the model inputs are observational: OMNI solar-wind velocity, IMF `BX_GSE`/`BY_GSM`/`BZ_GSM`, flow speed, dynamic pressure, AE/AL/AU, SymH, PC index, F10.7 and Kp, plus the derived Newell and Borovsky coupling functions, all assembled into the input feature vector.
- **Servers and Environments** / **: Data servers processing and handling** — `interfaces/User_Interface_with_Interactive_Knowledge_Graph/KnowledgeGraphServer/` is a Maven WAR (`<packaging>war</packaging>`, `maven-war-plugin`) containing `@WebServlet("/kgServlet/*")` and a people servlet. `RemoteRepository.java` opens an RDF4J `RemoteRepositoryManager` against an Ontotext GraphDB instance, prepares SPARQL `TupleQuery` and `Update` operations over the CfHA ontology namespace, and the servlet serializes results to JSON with Jackson. That is a data server that processes and hands back graph data.

Considered and rejected, with reasons — recorded so these are not re-proposed:

- **`Models and Simulations: MHD` / `: First Principles` / `: Physics-Based` / `: Theory`** — no solver or numerical integrator exists. `hk_model.ttl` is a vocabulary *about* such models. See the discussion above.
- **`Models and Simulations: Forecasting`** — the ML models are evaluated retrospectively against DMSP observations for a known event (17 March 2015); nothing in the repository produces a forecast or nowcast product.
- **`Mission-related`** and all its children — Helio-KNOW is not part of any mission ground system, does not ingest telemetry, and performs no mission operations, calibration, or science data production. It consumes already-processed public archive products.
- **`Data Processing and Analysis: Calibration`** — the DMSP SSJ data read are already-calibrated Level-2 differential and total energy flux in physical units; no calibration is applied.
- **`Data Processing and Analysis: Image Processing`** — `matplotlib` image rendering is not scientific image processing; there is no `scikit-image`, no deconvolution, no feature detection on image arrays.
- **`Data Processing and Analysis: Data Assimilation`** — the ML models ingest observations as features; no assimilation scheme, filter, or analysis-increment machinery is present. `hk_model.ttl` catalogues assimilative models (AMIE, DREAM, BRAVDA), which is again vocabulary, not implementation.
- **`Data Processing and Analysis: Pitch Angle Distributions` / `: Plasma Moments` / `: 3D Particle Distribution Processing`** — the SSJ product read is already reduced to integrated and channel-resolved flux; no distribution-function arrays, moment integration, or pitch-angle machinery appears.
- **`Data Visualization: Movies`** — no `matplotlib.animation`, no frame export, no video writer.
- **`Data Visualization: 2D Slices` / `Data Processing and Analysis: 2D Slices`** — no 3D volumes are sliced; the "2D" products are maps and spectrograms, not cross-sections.
- **`Servers and Environments: Software or Environment Container`** — no Dockerfile or Singularity definition has ever existed in the repository. `environments.yml` and `tools/AutOntologyTool/environment.yml` are conda environment specifications, which are dependency manifests rather than containers. (`jupyterhub.sqlite` and `jupyterhub_cookie_secret` are committed at the repository root, but they are stray runtime artifacts of a JupyterHub session, not a deliberate deployment definition.)
- **`Servers and Environments: High Performance Computing`** — no MPI, no job scripts, no parallel framework.
- **`Servers and Environments: Distribution/Access`** — genuinely arguable, since the knowledge-graph servlet does distribute graph data over HTTP. It was left off because `Data servers processing and handling` already carries that capability for the same single component, and listing both would double-count one servlet.
- **`Coordinate Transforms: Mission-Specific`** — no SPICE, no kernels, no instrument pointing or attitude handling.
- **`Coordinate Transforms: Solar` / `: Heliospheric` / `: Planetary`** — the region taxonomy names solar and interplanetary regions, but no code converts between solar, heliospheric, or planetary frames.

**A gap in the taxonomy worth recording.** The repository's primary output — ontologies, SKOS taxonomies, controlled-vocabulary harmonization, SPARQL competency questions, and RDF knowledge-graph construction — has no corresponding category anywhere in the 83-value `FunctionCategory` vocabulary. That work is represented here only indirectly, through `File Format Conversion` (glossaries and TTL in, unified CSV and OWL out), `Processing` and `Analysis` (the harmonization pipeline and its coverage analysis), and `Servers and Environments: Data servers processing and handling` (the graph server). A future agent should not read the absence of a semantics or knowledge-representation category as an extraction oversight, and should not stretch an unrelated category to cover it.

### 5. Related Region (MANDATORY)

**Earth Ionosphere**
**Earth Auroral Subregion**
**Earth Thermosphere**
**Earth Magnetosphere**
**Earth Magnetotail**
**Earth Inner Magnetosphere**
**Earth Outer Magnetosphere**
**Earth Magnetosheath**
**Earth Atmosphere**
**Earth Lower and Middle Atmosphere**
**Solar Wind**
**Interplanetary Space**
**Chromosphere**
**Corona**
**Photosphere**
**Solar Interior**
**Solar Environment**

Every value here is grounded in the repository — either in code the tools execute, or in the project's own published region taxonomy.

As flagged in the scope note, the evidence splits into two tiers, and the split matters for anyone judging whether the list is too broad.

*Tier 1 — regions the tools operate on directly:*

- **Earth Ionosphere** — DMSP SSJ measures precipitating electrons and ions at 850 km; the working coordinate frame is AACGM magnetic latitude and magnetic local time; `hk_region.ttl` defines `Ionosphere` with narrower `D Region`, `E Region`, `F Region`; `hk_phenomenon.ttl` carries Ionospheric Conductivity, Ionospheric Electron/Ion Density, Pedersen and Hall Conductivity and Currents, Tongue Of Ionization, Storm-Enhanced Density, Polar Cap Patch.
- **Earth Auroral Subregion** — the SSJ CDFs' `AURORAL_REGION` and `AURORAL_BOUNDARY_FOM` variables are decoded and plotted with the labels "no bndry / eq of AO / in AO / pol of AO"; OVATION Prime is called for the diffuse, monoenergetic, and wave (broadband) auroral flux types; `hk_region.ttl` defines `Auroral Oval`, `Auroral Region`, `Equatorward Boundary`, `Poleward Boundary`, `Subauroral`; `hk_phenomenon.ttl` carries Diffuse, Monoenergetic, Broadband, Proton, Pulsating and Throat Aurora, Quiet Arc, Polar Cap Arc, PBI, PMAF, SAID, SAPS, STEVE.
- **Earth Thermosphere** — the Poynting-flux work in `community/storymaps/dataExploration.ipynb` is explicitly framed against thermospheric density enhancements (its reference is Billett et al. 2021, "The Relationship Between Large Scale Thermospheric Density Enhancements and the Spatial Distribution of Poynting Flux"); `hk_region.ttl` defines `Thermosphere`; `hk_phenomenon.ttl` carries Thermospheric Composition, Density, State, Temperature, Wind, O/N2 Ratio, Joule Heating, Ion Drag.
- **Earth Magnetosphere** — the README's own subject is "the solar wind-magnetosphere-ionosphere (SWMI) system"; magnetosphere–ionosphere coupling is the stated science focus; GM coordinates and Tsyganenko field-line traces are computed for every ephemeris record; `hk_core.ttl` declares `hk:MagnetosphericPhysics` as a discipline; `hk_phenomenon.ttl` carries Magnetospheric State and Magnetospheric Mass Weighting.
- **Solar Wind** — OMNI solar-wind velocity, IMF components, flow speed and dynamic pressure drive the ML models; `hk_phenomenon.ttl` carries Solar Wind, Solar Wind Shock, and Interplanetary Magnetic Field.

*Tier 2 — regions the HelioKNOW region taxonomy and phenomena ontology define, which are the project's flagship deliverable and were contributed upstream to the Unified Astronomy Thesaurus:*

- **Earth Magnetotail** — `hk_region.ttl`: `Magnetotail`, `Magnetotail Current Sheet`, `Magnetotail Kink`, `Lobes`; `hk_phenomenon.ttl`: Tail Reconnection, Near-Earth Reconnection, Substorm Current Wedge.
- **Earth Inner Magnetosphere** — `hk_region.ttl`: `Inner Magnetosphere`, `Plasmasphere`, `Ring Current`, `Symmetric Ring Current`, `Inner Radiation Belt`, `Region 1`, `Region 2`.
- **Earth Outer Magnetosphere** — `hk_region.ttl`: `Outer Radiation Belt`, `Warm Plasma Cloak`, `Cusp`, `Lobes`, `Wake`.
- **Earth Magnetosheath** — `hk_region.ttl`: `Magnetosheath`, `Bowshock`, `Magnetopause`, `Dipole Standoff`; `hk_phenomenon.ttl`: Foreshock, Sheath, Magnetopause Current, Dayside Reconnection.
- **Earth Atmosphere** — `hk_region.ttl` defines `Atmosphere` and `Upper Atmosphere` as the containers for `Exosphere`, `Thermosphere`, `Mesosphere`, `Stratosphere`. Retained alongside the two more specific atmospheric values because `Exosphere` falls under neither of them.
- **Earth Lower and Middle Atmosphere** — `hk_region.ttl`: `Ground and Lower Atmosphere`, `Ground`, `Stratosphere`, `Mesosphere`, `Polar Vortex`.
- **Interplanetary Space** — `hk_region.ttl`: `Interplanetary space`, `Heliosphere`, `Near Planet Space`; `hk_core.ttl` declares `hk:InterplanetaryPhysics` as a discipline.
- **Chromosphere** — `hk_region.ttl`: `Chromosphere`; `data-models/hk_cq.rq` records a competency-question result placing Coronal Mass Ejection in `hkr:Chromosphere`; `tools/ADS_enrichment/active_solar_chromosphere_20220519.tsv` is a curated ADS result set for the active solar chromosphere.
- **Corona** — `hk_region.ttl`: `Corona`, `Solar Atmosphere`; `hk_cq.rq` places CME in `hkr:Corona`; `hk_phenomenon.ttl`: Streamer, Flux Rope; `hk_model.ttl` catalogues PFSS, WSA, MAS/CORHEL, and NLFFF coronal models.
- **Photosphere** — `hk_region.ttl`: `Photosphere`; `hk_cq.rq` places CME in `hkr:Photosphere`.
- **Solar Interior** — `hk_region.ttl`: `Solar Interior`, `Solar Convective Zone`, `Solar Radiative Zone`.
- **Solar Environment** — the broad solar container matching the taxonomy's whole solar branch and `tools/ADS_enrichment/data/UAT_Solar-related-concepts.csv`.

Considered and rejected:

- **`Heliosheath`** — no region concept in `hk_region.ttl` corresponds to it. `hk_phenomenon.ttl` has `Termination Shock`, which bounds the heliosheath, and `hk_region.ttl` has generic `Heliosphere` and `Pause` concepts, but nothing names the heliosheath and no tool touches outer-heliosphere data.
- **`Jupiter Magnetosphere`, `Mars Magnetosphere`, `Saturn Magnetosphere`, `Uranus Magnetosphere`, `Neptune Magnetosphere`** — a case-insensitive search of `hk_region.ttl`, `hk_phenomenon.ttl`, `hk_core.ttl`, and `hk_model.ttl` finds zero occurrences of Jupiter, Mars, Saturn, Uranus, or Neptune. No planet is named anywhere in the data models.
- **`Planetary Magnetospheres`** — the taxonomy's only non-Earth planetary concepts are the generic `Near Planet Space` and `Unmagnetized Bodies` (plus the `Induced Magnetic Fields` phenomenon). An unmagnetized body has, by definition, no magnetosphere, so these do not support the value. Recorded because "the taxonomy covers planets generically" is a tempting but incorrect basis for selecting it.

**On the breadth of this selection.** This is a broad selection, and the full set is the settled value: every value maps to a named concept in the project's own published region taxonomy, which is the project's flagship deliverable, so recall is the right trade here. A narrower reading — restricting the field to the five Tier 1 regions the tools operate on directly — was considered and rejected, because it would represent the notebooks' scope as though it were the repository's scope and would erase the region taxonomy from this field entirely. The Tier 1 / Tier 2 split above is retained as evidence structure, not as an offer to trim: it records which regions rest on executed code and which rest on the taxonomy, so a later reader can weigh the two kinds of evidence without re-deriving either.

### 6. Authors (MANDATORY)

Seven authors. Each is attested by the repository itself — commit authorship, an in-file byline, or a per-directory README naming the contributor — and identified further, where the evidence allows, against ORCID, ROR, Crossref, and OpenAlex. The list deliberately includes single-commit contributors: in a monorepo of independently contributed tools, one commit can be an entire component.

**1. Edwin Henneken**
- Identifier: `https://orcid.org/0000-0003-4264-2450`
- Affiliation: Center for Astrophysics Harvard & Smithsonian — `https://ror.org/03c3r2d17`

Both the identifier and the affiliation are established from ORCID: the record's sole employment is "Center for Astrophysics Harvard & Smithsonian", department "High Energy Astrophysics", role "IT Specialist", disambiguated by ROR to `https://ror.org/03c3r2d17`; the GitHub account `ehenneken` (Edwin Henneken) independently gives company "Smithsonian Astrophysical Observatory" and a bio identifying him as IT Specialist for the SAO/NASA Astrophysics Data System at the Harvard-Smithsonian Center for Astrophysics. His contribution is commit `055d2c7` (2022-09-12, "ADS curated synonyms"), which is consistent with the ADS role. The full institutional name is used rather than the acronym, and matches the ROR record's primary name exactly.

**2. Ryan McGranaghan**
- Identifier: `https://orcid.org/0000-0002-9605-0007`
- Affiliation: Jet Propulsion Laboratory — `https://ror.org/027k65916`

Established from ORCID and from the repository's commit history: ORCID 0000-0002-9605-0007 resolves to Ryan McGranaghan with a single current employment at Jet Propulsion Laboratory (ROR `https://ror.org/027k65916`, from 2023-01, no end date). He is the repository owner and principal author, with 127 of the 170 commits across three author identities (`Ryan McGranaghan <34279613+rmcgranaghan@users.noreply.github.com>`, `rmcgranaghan <ryan.mcgranaghan@colorado.edu>`, `rmcgranaghan <ryan.mcgranaghan@gmail.com>`).

Two further affiliations are attested but deliberately **not recorded**, kept here so a future agent knows they were evaluated:
- *Atmospheric and Space Technology Research Associates* (`https://ror.org/04jzxg282`) — the institution named against his ECIP award in the repository's own `data/ECIP_awards_2020.pdf` ("Ryan McGranaghan/Atmospheric & Space Technology Research Associates"), i.e. his affiliation when Helio-KNOW was funded and started in 2021. Not recorded because the Jet Propulsion Laboratory value is his current affiliation and is corroborated by ORCID; adding a historical second affiliation is a curatorial choice, not a correction.
- *Goddard Space Flight Center* (`https://ror.org/0171mag52`) — OpenAlex records both GSFC and JPL as his affiliations on the 2023 CfHA paper (raw strings "NASA Goddard Space Flight Center, Greenbelt, MD, USA" and "NASA Jet Propulsion Laboratory, California Institute of Technology, Pasadena, CA, USA"). Not recorded for the same reason.

**3. Megan Powers**
- Identifier: Not found
- Affiliation: Not found

**Established by commit and in-tool evidence.** She is the author of the AutOntology tool, a complete subdirectory of the repository: commits `66afbef` (2022-11-25, "Adding AutOntology tool") and `c4a75b9` (2023-01-31, "Modified the AutOntology tool to contain a dependencies yaml, as well as guides for training data and language models"), both as `Megan Powers <meganpowers@Megans-MBP.home>`. Her authorship is corroborated inside the tool: `tools/AutOntologyTool/README.md` uses `/Users/meganpowers/Desktop/HeliophysicsDatasetCleaned.txt` as its worked example path, its title is the name of her own repository, and all 37 of its figures are served from `github.com/meganpowers1/SemanticNaturalLanguageProcessingforKnowledgeGraphsCreation`.

She is absent from the GitHub contributors list because her commit email (`meganpowers@Megans-MBP.home`, a local machine hostname) is not linked to a GitHub account — which is exactly why an extraction based on the GitHub contributors API alone would miss her. Recorded so this omission is not repeated.

No identifier could be established. An ORCID search for given name "Megan" and family name "Powers" returns four records (0000-0003-1899-6291, 0000-0002-6450-9995, 0000-0001-6672-400X at University of Washington, and 0000-0003-4191-4493 for Megan Sandoval-Powers), none of which shows ontology, semantic-web, or heliophysics work; an OpenAlex search for her together with ontology/NLP/knowledge-graph terms returns nothing relevant. There is a *lead* but not proof: the AutOntology README is written in consistent British English ("utilises", "visualise", "serialised", "organisational"), matching the Birmingham City University group that co-authored the CfHA paper with McGranaghan. That is suggestive only and was deliberately not acted on. Do not guess an ORCID for her.

**4. Omar Shalaby**
- Identifier: Not found
- Affiliation: Not found

**Corrected name.** This author was previously recorded as the bare GitHub handle `oms9`, carrying no given name at all — a handle standing in for a person's name. That value was incorrect; the author is Omar Shalaby, and the name is recorded correctly here. His identity is established from the source files themselves: `tools/LitNetworkBuilder/LitNetworkBuilder_networkBuilder.py` opens with `#HelioKnow - Omar Shalaby` and `tools/LitNetworkBuilder/LitNetworkBuilder_paperMatch.py` with `#Omar Shalaby - 7/22/22`. Those files entered the repository in commit `dc90521` (2022-12-11, "Adding LitNetworkBuilder") authored by `oms9 <oms9@njit.edu>`, and `tools/README-tools.md` links the tool's upstream home at `github.com/oms9/LitNetworkBuilder`, whose GitHub description is "2022 NASA Summer Internship - HelioKnow Utilities". The chain from handle to person is therefore complete.

No identifier has ever been established for him, and none should be invented: the GitHub profile `oms9` exposes no name, company, or email. An ORCID search for "Omar Shalaby" returns three records — 0000-0001-8504-5352 (Texas A&M College of Medicine, University of Houston), 0009-0001-9331-0782 (American University of Science and Technology, and others), and 0009-0007-0757-8162 (Adnet Systems) — and **none is at the New Jersey Institute of Technology**, which his commit email `oms9@njit.edu` indicates. The Adnet Systems record is superficially tempting because Adnet is a NASA contractor, but nothing links it to this person, so it was rejected. Do not assign any of these three ORCIDs without new evidence.

**5. Alex Shifrin**
- Identifier: `https://orcid.org/0009-0000-8635-3314`
- Affiliation: Not found

**Corrected name; identifier unchanged.** This author was previously recorded as the bare GitHub handle `shurgithub` with no given name — again a handle standing in for a person's name — although the correct ORCID was already attached. The name is recorded correctly here, and the ORCID it always carried is retained: ORCID 0009-0000-8635-3314 resolves to given name "Alex", family name "Shifrin". Three independent links tie that ORCID to this repository: `data-models/hk_core.ttl` line 22 declares `dcterms:contributor <https://orcid.org/0009-0000-8635-3314>` on the HelioKNOW core ontology; commit `124a937` (2025-06-20) is authored by `shifrin@gmail.com`; and every other commit from the same GitHub account (`35734521+shurgithub`) touches the same ontology files. He is the second-largest contributor (36 commits) and the principal author of the HelioKNOW ontology suite — `hk_core.ttl`, `hk_phenomenon.ttl`, `hk_region.ttl`, `hk_model.ttl`, the `hk_instruments.ttl` updates, and `hk_cq.rq`.

*Affiliation candidate, evaluated and not recorded:* the ORCID record's only employment entry is "Siemens Energy", with no start or end date, no department, no role, and no ROR or Ringgold disambiguation. It was **not recorded**, because nothing in the repository corroborates it and the undated entry cannot be tied to the period of his contributions (2025–2026). Recorded rather than silently dropped so a future agent knows the candidate exists and why it was rejected; new evidence dating the employment to his contribution period would be grounds to revisit it.

**6. Brandon Whitehead**
- Identifier: `https://orcid.org/0000-0002-0337-8610`
- Affiliation: Manaaki Whenua – Landcare Research — `https://ror.org/02p9cyn66`

The ORCID above is an established and verified identifier for this author: it is registered to given name "brandon", family name "whitehead", and the ORCID record itself is the source of the affiliation below. The identity chain: the git author is `brandonw <brandonnodnarb@gmail.com>` (commit `71c8576`, 2022-09-14, "added text block for string comparison"), and GitHub attributes that single commit to the account `semantic-nomad`, whose profile name is "brandon whitehead" and whose company is `@manaakiwhenua`. ORCID 0000-0002-0337-8610 records a current employment at "Manaaki Whenua - Landcare Research" as Environmental Data Scientist since 2020-01-22, which spans the 2022 commit date; the account handle `semantic-nomad` is itself consistent with a semantic-web practitioner contributing to an ontology project.

Note two details that could trip up a later reconciliation. First, the ORCID employment carries a RINGGOLD disambiguation (`2243`), not a ROR, so the ROR was resolved separately: a ROR v2 query for "Manaaki Whenua Landcare Research" returns `https://ror.org/02p9cyn66` as the only exact-name match (ROR's fuzzy full-text search returns many loose hits for these terms; this is the one genuine name match, and it is independently corroborated by a direct ID lookup and by the RINGGOLD-to-name match on the ORCID employment itself), primary name "Manaaki Whenua – Landcare Research". That name uses an **en dash (U+2013)**, not a hyphen — the ROR primary name is reproduced verbatim here. Second, his ORCID also lists a Ronin Institute fellowship from 2025-11 and a prior CABI post ending 2019-12; Manaaki Whenua is the one that covers the contribution date and matches his GitHub company.

**7. Swapnali Yadav**
- Identifier: Not found
- Affiliation: Birmingham City University — `https://ror.org/00t67pt25`

She contributed `interfaces/User_Interface_with_Interactive_Knowledge_Graph/` in commit `42d004a` (2022-09-30) as `SwapnaliY16 <yadavswapnali.1995@gmail.com>`, and `interfaces/README-interfaces.md` names her explicitly: "The code in this directory was contributed by Swapnali Yadav (@SwapnaliY16)", adding that the interface is documented in "Swapnali's Masters Degree final presentation".

The affiliation comes from the peer-reviewed paper describing exactly that work — McGranaghan, Young, Powers, Yadav & Vakaj (2023), `10.1016/j.acags.2023.100142`, the CfHA community knowledge graph paper cited in this repository's own `data-models/README-data-models.md`. OpenAlex resolves her authorship affiliation on that paper to Birmingham City University (raw string "Birmingham City University, B47 XG, United Kingdom"), as it does for co-authors Cameron Powers and Edlira Vakaj. Since the contributed code *is* the frontend for that paper's knowledge graph and was her Masters work, Birmingham City University is the affiliation for this contribution. ROR `https://ror.org/00t67pt25` is the sole match for "Birmingham City University".

No identifier: an ORCID search for given name "Swapnali", family name "Yadav" returns **zero** records, and neither Crossref nor OpenAlex carries an ORCID for her on the 2023 paper. Her GitHub profile lists a current company of "Natural History Museum" in London, which postdates and is unrelated to this contribution and was therefore rejected as an affiliation.

### 7. Software Name (MANDATORY)
`Helio-KNOW`

Confirmed three ways: the `README.md` H1 heading is `# Helio-KNOW`; the GitHub API `name` field is `Helio-KNOW`; and SoMEF independently extracted both `name` and `full_title` as `Helio-KNOW`. The expansion "Heliophysics KNOWledge Network" appears throughout the README, with the deliberate internal capitalization that gives the short name its form, but `Helio-KNOW` is the name as listed on the repository and is what the project calls itself.

### 8. Description (MANDATORY)

> This repository is home to the Heliophysics KNOWledge Network (Helio-KNOW) development and community: the collection of software and systems for improved information representation in Heliophysics, and the commons for the community to use and collaborate through them. Helio-KNOW brings knowledge graph approaches to the solar wind-magnetosphere-ionosphere (SWMI) system, focusing on magnetosphere-ionosphere coupling and creating the tools with which coupling phenomena and space weather risks can be studied. The repository provides four kinds of resource. First, data models: the HelioKNOW suite of SKOS/OWL ontologies covering core concepts, phenomena, regions, models and instruments; a region-based taxonomy contributed to the Unified Astronomy Thesaurus; and the Center for HelioAnalytics community ontology. Second, tools: utilities for retrieving DMSP and FAST spacecraft ephemeris and data availability from NASA's Satellite Situation Center; reading, converting and plotting DMSP SSJ precipitating electron and ion CDF data; machine-learning analysis and prediction of auroral particle precipitation; harvesting and citation-network analysis of the heliophysics literature from NASA ADS; natural language processing of heliophysics texts; and harmonizing heliophysics glossaries and phenomena vocabularies across SPASE, the Unified Astronomy Thesaurus, AGU, GCMD, SWEET and GEMET. Third, data pipelines for semantically lifting observational datasets into the knowledge graph. Fourth, interfaces: a Java/RDF4J knowledge-graph server and an interactive data-availability dashboard. The tools are research notebooks rather than an installable package, and several carry hard-coded local paths. This repo's issue tracker also serves as a general-purpose discussion forum, and one goal of Helio-KNOW is to bring together the research community around intelligent knowledge infrastructure and welcome all to contribute to the conversation and development.

**This supersedes the previously stored description**, which was a verbatim excerpt of the README's opening paragraph:

> This repository is home to the Heliophysics KNOWledge Network (Helio-KNOW) development and community. This repo's issue tracker also serves as a general-purpose discussion forum. Learn more details about the project below. One goal of Helio-KNOW is to bring together the research community around intelligent knowledge infrastructure and welcome all to contribute to the conversation and development.

The default is to respect a submitter's wording, and that excerpt was superseded only because it is **materially incomplete rather than merely differently phrased**: it never states what the software does. A reader deciding whether Helio-KNOW is useful to their work learned from it only that a repository exists and that its issue tracker doubles as a forum. Field 8 asks specifically for "what the software does, why to use it, assumptions it makes".

There was also a concrete defect: the sentence "Learn more details about the project below" is a README cross-reference that has no referent once the paragraph is lifted into a metadata record, and it displaced the space where the actual capability summary should have been.

The replacement is constructed to preserve editorial intent rather than override it. It opens with the superseded text's first clause and closes with its final sentence, both essentially verbatim; the added middle is drawn from the repository's own words — the GitHub repository description and README ("the collection of software and systems for improved information representation in Heliophysics, and the commons for the community to use and collaborate through them", "brings knowledge graph approaches ... focusing on magnetosphere-ionosphere coupling and creating the tools for which coupling phenomena and space weather risks can be studied") and the per-directory READMEs, which are the maintainers' own descriptions of each component. The closing sentence about notebooks and hard-coded paths is included because Field 8 explicitly asks for assumptions, and this is the assumption most likely to surprise a prospective user.

The first 200 characters preview as: "This repository is home to the Heliophysics KNOWledge Network (Helio-KNOW) development and community: the collection of software and systems for improved information representation in Heliophysics, and…" — which is a usable preview on its own, though Field 9 supplies a better one regardless.

### 9. Concise Description (OPTIONAL)
`Software and systems for improved information representation in Heliophysics`

This is the best available concise description and needs no improvement: it is simultaneously the GitHub repository's own `description` field, the README's definitional sentence ("The Heliophysics KNOWledge Network (Helio-KNOW) is the collection of software and systems for improved information representation in Heliophysics"), and the highest-confidence `description` result SoMEF returned. At 76 characters it is well inside the 200-character limit.

### 10. Publication Date (RECOMMENDED)
`2021-03-01`

**This replaces the previously recorded value `2025-11-05`.**

Field 10 is "Date of first broadcast/publication ... Used for the initial version of the software." The repository became public — which is this software's publication event, there being no DOI or package release — on 2021-03-01: the GitHub API reports `created_at: 2021-03-01T13:42:03Z`, SoMEF independently extracted `date_created: 2021-03-01T13:42:03Z`, and the first two commits (`Initial commit` and `Added details of Helio-KNOW project`) are both dated 2021-03-01. Three independent sources agree.

The previously recorded `2025-11-05` cannot be the software's publication date: it postdates the repository's creation by four and a half years and falls in the middle of a period of continuous development (there are commits in 2021, 2022, 2023, 2024, 2025 and 2026, with 51 in 2025 alone), so it corresponds to no publication event in the project's history. It is most consistent with the date the metadata record itself was created rather than with anything in the software's history. Because this corrects a previously recorded value rather than filling a gap, the three-source agreement above is what carries it; `2025-11-05` is superseded and should not be reinstated without evidence of a publication event on that date.

### 11. Publisher (RECOMMENDED)
- **Organization:** `GitHub`
- **Publisher Identifier:** `https://github.com`

Field 11's rule is explicit: "If no DOI has been obtained, indicate the repository host, such as GitHub or GitLab." No DOI exists (Field 2), and the repository is hosted on GitHub, so GitHub is the publisher.

A ROR was sought and does not exist: a ROR v2 query for "GitHub" returns no items, which is expected since ROR indexes research organizations rather than commercial hosting providers. Field 11 permits a URL in that case ("or URL otherwise (e.g., https://zenodo.org)"), so `https://github.com` is used. "GitHub" is left unexpanded because it is a proper company name, not an acronym.

### 12. Version (RECOMMENDED)
- **Version Number:** Not found
- **Version Date:** Not found
- **Version Description:** Not found
- **Version PID:** Not found

**The project has never released or tagged a version.** This is deliberate negative research, because two plausible-looking strings in this repository are traps.

What was checked, all negative:
- `git tag` on the pinned clone with all remote refs fetched: no tags at all.
- GitHub API `/releases`: empty array. GitHub API `/tags`: empty array.
- No `CITATION.cff`, `codemeta.json`, or `.zenodo.json` — and `git log --all --diff-filter=A` confirms none ever existed.
- No Python packaging metadata: no `setup.py`, `pyproject.toml`, `setup.cfg`, `package.json`, `DESCRIPTION`, or `Project.toml`, and none in history. The repository is not installable, so there is no package version to read.
- No `CHANGELOG.md`.
- No DOI, hence no version DOI (Field 2).
- Branches are `main` plus one feature branch (`add-models`) and seven `shurgithub-patch-*` branches; none encodes a release.

Two strings that must **not** be recorded as this software's version:

1. **`0.0.1-SNAPSHOT`** — SoMEF reports this as `version`. It is the Maven default placeholder in `interfaces/User_Interface_with_Interactive_Knowledge_Graph/KnowledgeGraphServer/pom.xml`, the version of one Java sub-component, and the `-SNAPSHOT` suffix means "not released" by definition. Recorded explicitly because any future SoMEF-driven pass will surface it again.
2. **Per-artifact ontology versions** — `hk_region-v3.1.ttl` and `hk_region-v3.0.ttl` version the region taxonomy file, `heliodata_region_taxonomy-v2.0.ttl` versions its predecessor, and `CfHA_Ontology_V_4.2.owl` versions a third-party ontology that is merely redistributed here. `data-models/hk_model.ttl` additionally carries dozens of `owl:versionInfo` values ("1", "2016", "cdbm_201510", "v20190904", …) which are the versions of the *external models it catalogues*, not of anything in this repository. None of these is the software's version. `data-models/README-data-models.md` makes the intent clear: "Latest region-based taxonomy always **hk_region.ttl**" — the project versions individual semantic artifacts and keeps an unversioned "latest" pointer, rather than versioning the software.

This field is therefore correctly empty. If the project ever cuts a release, this is the field to revisit first.

### 13. Programming Language (RECOMMENDED)
**Other**
**Python 3.x**
**Java**

GitHub's language statistics for the repository are Jupyter Notebook 27,424,070 bytes, Python 35,754 bytes, Java 17,263 bytes, and SoMEF returns the same three. Since `Jupyter Notebook` is not an available value in this field and notebooks here contain Python, the notebook bytes count toward Python.

- **Python 3.x** — `environments.yml` pins `python=3.9`; `tools/AutOntologyTool/environment.yml` pins `python>=3.0` with Python-3-only dependency versions (spacy 3.4.0, rdflib 6.2.0, scikit_learn 1.2.1); all 26 notebooks and 4 `.py` files are Python 3. One legacy exception is worth noting rather than acting on: `tools/ADS_enrichment/doADS_API_Query.py` imports `urllib2`, which is Python 2 only, while its notebook counterpart `doADS_API_Query.ipynb` imports `urllib3` and `urllib.parse`. That single stale script does not make `Python 2.x` a language of the software, and it was rejected on that basis.
- **Java** — `interfaces/.../KnowledgeGraphServer/` contains five `.java` sources and a Maven `pom.xml` whose `maven-compiler-plugin` sets `<release>13</release>`, with RDF4J 3.6.0, GraphDB 9.11.2, `javax.servlet-api` 3.1.0 and Jackson dependencies.
- **Other** — included deliberately. The repository's largest and most consequential machine-readable artifacts are not in any listed language: 12 Turtle files (including the ~95,000-line `hk_instruments.ttl`), 4 OWL ontologies, 5 RDF/XML files, and a SPARQL query file (`hk_cq.rq`). `Other` is the only available value that represents them, and omitting it would erase the project's flagship deliverable from this field.

**`Javascript` was considered and rejected**, and the reason is worth recording because the repository looks at first glance as though it should have it. `interfaces/User_Interface_with_Interactive_Knowledge_Graph/README.md` describes a React frontend, and commit `42d004a` is titled "Commit for (1) Frontend code in knowledge-graph-user-interface (2) Backend code in KnowledgeGraphServer". But `git ls-tree -r 42d004a` shows that path was committed as mode `160000` — a gitlink — with no `.gitmodules` entry, so the frontend source was never actually stored in this repository, and the path is absent from the tree at the pinned revision. A history-wide search for `.js`, `.jsx`, `.ts`, and `.tsx` files across all branches returns nothing. There is no JavaScript here.

### 14. Reference Publication (RECOMMENDED)
**Not found.**

No publication describes this software. What was checked:
- No JOSS paper, and no `paper.md`/`paper.bib` in the repository or its history.
- `README.md` has no citation section. Its only "More information" pointer is a NASA NSPIRES PDF of ECIP 2020 award abstracts (link still live), which is a funding abstract, not a publication, and carries no DOI.
- Crossref searches for a Helio-KNOW software or project paper returned only adjacent work by the same author: `10.1002/essoar.10503724.1` (the CHESS Open Knowledge Network preprint, a different project), `10.1051/swsc/2021037` (a topical-issue editorial), and general Complexity Heliophysics essays. None describes this software.
- One unverifiable candidate exists and is recorded so it is not re-hunted from scratch: an essay titled "The NASA Heliophysics KNOWledge Network (Helio-KNOW) project (an essay for the Space Data Knowledge Commons)" at `https://knowledgestructure.pubpub.org/pub/helio-know`. The page sits behind Cloudflare and refuses automated retrieval, so its authorship, date, and whether it carries a DOI could not be confirmed from a primary source. It was therefore not recorded as a value. If a human can open that page and it has a DOI, it is the strongest reference-publication candidate that exists.

Publications that describe *components* of the repository rather than the software as a whole are recorded in Field 27, which is the correct home for them.

### 15. License (RECOMMENDED)
- **License:** `GNU General Public License v3.0 or later`
- **License URI:** `https://spdx.org/licenses/GPL-3.0-or-later.html`

The License URI above is the SPDX page for the selected license's identifier, `GPL-3.0-or-later`, which is why it takes this form rather than another SPDX page for the same license family. The repository's `LICENSE` is the verbatim GNU General Public License Version 3 text (29 June 2007), and the GitHub API license object reports `key: gpl-3.0`, `spdx_id: GPL-3.0`.

One nuance, since it will recur on any future check: the repository declares plain GPLv3 with no per-file "or any later version" notice, so `GPL-3.0-only` would be the more precise SPDX identifier for it. `GNU General Public License v3.0 or later` is nonetheless the correct available choice for a GPLv3 project, and selecting it is not drift.

**Durable note on a differing per-artifact license.** `data-models/hk_core.ttl` line 23 declares `dcterms:license <https://creativecommons.org/licenses/by-sa/4.0/>` on the HelioKNOW core ontology — CC BY-SA 4.0, not GPL-3.0. The License field takes a single value and the repository-level `LICENSE` governs the work as a whole, so the GPLv3 value remains correct; but anyone reusing the ontologies specifically should be aware they carry their own license declaration. Recorded so a future agent does not read the CC BY-SA declaration as evidence that the recorded license is wrong.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

`heliophysics`, `space weather`, `knowledge graph`, `knowledge network`, `ontology`, `semantic web`, `knowledge representation`, `linked data`, `taxonomy`, `interoperability`, `metadata`, `spase`, `unified astronomy thesaurus`, `glossary harmonization`, `natural language processing`, `machine learning`, `open science`, `python`, `magnetosphere-ionosphere coupling`, `magnetosphere`, `ionosphere`, `thermosphere`, `aurora`, `particle precipitation`, `electron precipitation`, `poynting flux`, `solar wind`, `dmsp`

All 28 are given in normalized lowercase, one term per entry, which is the recorded form.

Keywords are an open field rather than a controlled list, so these are free terms. Each is deliberately spelled in its conventional community form rather than as an ad-hoc variant, so that one concept is not expressed two different ways.

Evidence, grouped:
- *Semantic and knowledge-infrastructure terms* (`knowledge graph`, `knowledge network`, `ontology`, `semantic web`, `knowledge representation`, `linked data`, `taxonomy`, `interoperability`, `metadata`) — the README's central argument is to "Embrace a more natural structure for the data: a knowledge graph (KG)" and to grow it "into a _Knowledge Network_"; `data-models/` holds the SKOS/OWL ontologies; `community/Knowledge_Modeling_Curriculum/Glossary.md` defines "ontology" and "knowledge base" as its first two entries; `CONTRIBUTING.md` has a whole section on "Relate to Other Knowledge Organization Systems" discussing `rdfs:seeAlso`, SKOS mapping, and `owl:sameAs` alignment.
- `spase` — `hk_instruments.ttl` binds the `spase:` prefix and contains 2,899 `spase:Instrument` and 1,798 `spase:Observatory` instances; `tools/ADS_enrichment/data/spase-2.5.0-draft.json` is the SPASE dictionary; `CONTRIBUTING.md` records "We started by uplifting existing Madrigal and SPASE Instrument data into RDF."
- `unified astronomy thesaurus` — `tools/ADS_enrichment/uat.ttl`, `uat_leaf_terms.csv`, `data/UAT.csv`, `data/UAT.json`, `data/UAT_Heliophysics.csv`, `data/helio-vocamp-uat-ext-shared.{owl,ttl}`; `CONTRIBUTING.md`: "In Fall 2025 we contributed 173 concepts in a full taxonomy ... to establish a new version of the astronomy thesaurus."
- `glossary harmonization` — the entire `tools/glossary_harmonization/` directory, whose `phenomena_harmonization.ipynb` unifies HelioKNOW phenomena against HELIO Ontology, HEK, NASA CCMC, SWEET, SPASE, the NASA Heliophysics Vocabulary, ESA, UAT, AGU, GCMD and GEMET.
- `natural language processing`, `machine learning` — `tools/NLP/`, `tools/ML/`, `tools/AutOntologyTool/` (spaCy NER, TF-IDF, Word2Vec, clustering) and the Keras/TensorFlow/LightGBM precipitation models.
- `open science` — `CONTRIBUTING.md` adapts the Pangeo open-science community's guidelines; `CODE-OF-CONDUCT.md` adopts the Contributor Covenant and the ESIP Community Participation Guidelines; `tools/README-tools.md` and the README frame the repository as a commons "to produce open, reproducible, and scalable Heliophysics science".
- *Science terms* (`magnetosphere-ionosphere coupling`, `magnetosphere`, `ionosphere`, `thermosphere`, `aurora`, `particle precipitation`, `electron precipitation`, `poynting flux`, `solar wind`, `dmsp`) — evidenced in Fields 4, 5 and 31/32 above. `poynting flux` and `particle precipitation` in particular are the two quantities the README names as the "sensors" of information flow in the SWMI system, and both are `hk_phenomenon.ttl` concepts.

**Why several central phenomena appear here rather than in Field 22.** `Related Phenomena` is a closed seven-value list with no applicable controlled value for particle precipitation, Poynting flux, aurora, substorms, Joule heating, or reconnection — the phenomena this repository is actually about. Field 22's own guidance directs such terms to Keywords, which is why they are here. See Field 22.

`coordinates` was considered — AACGM/GEO/GM handling is real (Field 4) — but was left off because Field 4's two Coordinate Transforms values already carry that capability and the keyword adds no discovery value beyond them.

### 17. Data Sources (OPTIONAL)

**CDAWeb**
**SSCWeb**
**OMNIWeb**
**Observatory/Mission-specific**
**Madrigal**
**HTTP/HTTPS Directories**
**Other**

- **CDAWeb** — `data-pipelines/particle_precipitation_data_pipeline_experiment_v1.ipynb` imports `from cdasws import CdasWs, TimeInterval`, instantiates `cdas = CdasWs()`, and calls `cdas.get_variable_names('DMSP-F16_SSJ_PRECIPITATING-ELECTRONS-IONS')` and `cdas.get_data(...)` over a `TimeInterval`. Its header markdown links the CDAWeb dataset notes pages for both DMSP-F16 SSJ and FAST ESA.
- **SSCWeb** — both `tools/tools_for_SSCWeb/` notebooks import `from sscws.sscws import SscWs`, instantiate `ssc = SscWs()`, and call `get_observatories()` and `get_locations()`; `SSCWeb_Scraper.ipynb` states its purpose as generating "a DB of data availability for the followign missions: DMSP, FAST" and `tools/README-tools.md` describes the directory as "Tools for accessing data from NASA's Satellite Situation Center (SSC)".
- **OMNIWeb** — `tools/ML/DMSP_CDFfile_analysis.ipynb` does `from geospacepy import omnireader` and builds `omnireader.omni_interval(t_start, t_end, '5min', cdf_or_txt='txt')` and an `'hourly'` interval, reading `BX_GSE`, `BY_GSM`, `BZ_GSM`, `AE_INDEX`, `AL_INDEX`, `AU_INDEX`, `SYM_H`, `flow_speed`, `Pressure`, `Vx`, `PC_N_INDEX`, `F10_INDEX` and `KP` — the OMNI merged solar-wind and index dataset.
- **Observatory/Mission-specific** — required by Field 17's own instruction to cross-list with Field 32 whenever a specific mission's data is read. The DMSP SSJ CDF files are read directly off disk, and `exploreSSJ_notebook.ipynb`'s docstring names their origin: "reads data from CDF files created by NCEI (https://www.ngdc.noaa.gov/)". The filename convention `dmsp-f16_ssj_precipitating-electrons-ions_YYYYMMDD_v1.1.x.cdf` is the NOAA/NCEI DMSP SSJ product convention, and `DMSP_SSJ_CDF_to_DataFrame(sat, yr, mn, dy, ...)` builds paths from it. The Poynting-flux HDF5 file read by `community/storymaps/dataExploration.ipynb` is likewise a mission-specific product supplied by its author.
- **Madrigal** — a judgment call, recorded as such. No code retrieves measurements from Madrigal. What the repository does is ingest Madrigal's *instrument catalogue* as source data for the knowledge graph: `data-models/hk_instruments.ttl` binds `@prefix madrigal: <http://cedar.openmadrigal.org/>`, declares `madrigal:` a `skos:ConceptScheme` with `schema:about <http://cedar.openmadrigal.org/docs/name/wt_dataOrg.html>`, models Madrigal's data model (Instrument, InstrumentType, Site, Experiment, ExperimentFile, ExperimentFileParameter, each with definitions quoted from Madrigal's documentation), and instantiates 227 `madrigal:Instrument` and 10 `madrigal:Site` individuals with `skos:exactMatch` links to SPASE. `CONTRIBUTING.md` confirms the intent: "We started by uplifting existing Madrigal and SPASE Instrument data into RDF." Selected because Madrigal genuinely is a data input the software consumes; recorded as metadata-catalogue ingest rather than measurement retrieval so the basis is not mistaken later.
- **HTTP/HTTPS Directories** — `tools/NLP/web_scraper_PDFs.ipynb` fetches a conference programme page, parses it with BeautifulSoup, selects `a[href$='.pdf']`, and downloads every linked PDF, i.e. harvests a web-served document directory. `tools/ADS_enrichment/compile_vocabs.ipynb` and `compile_DB_existingVocabularies.ipynb` use `urllib.request` to retrieve vocabulary files over HTTPS, and `phenomena_harmonization.ipynb` parses SWEET modules directly from `http://sweetontology.net/<module>` URIs.
- **Other** — covers three real sources with no applicable controlled value: the **NASA ADS** API (`tools/LitNetworkBuilder/LitNetworkBuilder_harvester.py` and `tools/ADS_enrichment/doADS_API_Query.{py,ipynb}` page through `https://api.adsabs.harvard.edu/v1/search/query` with a bearer token), **OpenAlex** (`tools/ADS_enrichment/openAlex_explorer.ipynb`), and the community vocabulary sources aggregated by the harmonization pipeline (UAT, AGU index terms, GCMD science keywords, GEMET, SWEET, NASA Heliophysics Vocabulary).

Considered and rejected: **HAPI**, **das2**, **VirES**, **TAP**, **AMDA**, **GFZ**, **WDC**, **S3/Cloud-aware**, and **The Virtual Solar Observatory.** — no client, URL, or reference to any of these appears anywhere in the repository.

### 18. Input File Formats (RECOMMENDED)

**CDF**
**csv**
**JSON**
**HDF5**
**ascii**
**Other**

- **CDF** — `spacepy.pycdf.CDF(...)` opens DMSP SSJ files in `tools/DMSP_SSJ_tools/DMSP_SSJ_utils.ipynb`, `tools/DMSP_SSJ_tools/exploreSSJ_notebook.ipynb`, and `tools/ML/DMSP_CDFfile_analysis.ipynb`; `community/storymaps/dataExploration.ipynb` reads SSJ CDFs via `%run DMSP_SSJ_utils.ipynb`.
- **csv** — `pd.read_csv` in seven notebooks, plus `csv.DictReader` over the GCMD science-keywords CSV in `phenomena_harmonization.ipynb`. Roughly 31 CSV files are checked into `tools/*/data/`.
- **JSON** — `json.load` in twelve files: the ADS harvester's cached paper JSON, `interfaces/data_availability_dashboard/helioKNOW_metadata.json`, the SPASE dictionary and glossary JSON sources, GCMD CMR JSON, and UAT definitions JSON.
- **HDF5** — `community/storymaps/dataExploration.ipynb` opens the SuperDARN/AMPERE-derived Poynting flux product with `h5py.File(pf_filename, "r")` and walks its `Grid/`, `Data/` and `Time/` groups.
- **ascii** — plain-text term and synonym lists are read directly: `tools/ADS_enrichment/data/AGU_index_terms_Helio.txt`, `AGU_index_terms_Helio_synonyms.txt`, `ads_simple_synonyms*.txt`, `ads_multi_synonyms*.txt`, `ads_OpenAlex_synonyms_updated_v*.txt`; `tools/LitNetworkBuilder/LitNetworkBuilder_paperMatch.py` reads `LitNetworkBuilder_matchKeys.txt`; `DMSP_CDFfile_analysis.ipynb` reads `inputfeature_labels.txt`.
- **Other** — the formats with no applicable controlled value, which are the ones that matter most here: Turtle (`rdflib` `graph.parse(..., format='turtle')` over `hk_core.ttl` and `hk_phenomenon.ttl`; SWEET `.ttl`; `uat.ttl`), OWL (`CfHA_Ontology_V_4.2.owl`, `helio-vocamp-uat-ext-shared.owl`), RDF/XML (`gemet-backbone.rdf`, `gemet-definitions.rdf`, `gemet-skoscore.rdf`, `gemet.rdf`, `sweetAll.rdf`), XLSX (`pd.read_excel` over `agu-index-terms.xlsx`, `NASA Heliophysics Vocabulary.xlsx`, `SMD_and_manual_synthesized_terms.xlsx`, `AGU-index-terms-synonyms-workingList.xlsx`), TSV (`active_solar_chromosphere_20220519.tsv`), and PDF (Apache Tika `parser.from_file(...)` over the ECIP award abstracts and the Heliophysics Decadal Survey in `tools/NLP/text_explorer.ipynb` and `tools/ADS_enrichment/heliophysicsAcronymGenerator.ipynb`).

**`netCDF3/4` was considered and rejected.** `tools/DMSP_SSJ_tools/exploreSSJ_notebook.ipynb` contains `# ds = xr.open_dataset(os.path.join(directory,file)) # with xarray (doesn't work with .cdf)` — a commented-out line whose own comment records that it failed. No netCDF file is read anywhere. Recorded because a grep for `open_dataset` will hit this line again. **`FITS`** — no `astropy.io.fits`, no `.fits` file, nothing. **`IDL.sav`**, **`Zarr`**, **`ISTP-Compliant`** — no evidence; note in particular that although the DMSP SSJ CDFs are in practice ISTP-compliant, the code reads them with generic `pycdf` variable access and implements nothing ISTP-specific, so the value would misrepresent the software.

### 19. Output File Formats (RECOMMENDED)

**csv**
**JSON**
**ascii**
**Other**

- **csv** — twelve files write CSV. The most consequential are `SSCWeb_Scraper.ipynb`, which writes one ephemeris CSV per spacecraft per day into a `YYYY/YYYYMMDD/<scid>/` tree; `exploreSSJ_notebook.ipynb`'s `DMSP_SSJ_CDF_to_DataFrame`, which converts each SSJ CDF to a CSV subset; `DMSP_CDFfile_analysis.ipynb`, which writes `y_loop_predictions_save--f17--March17_2015.csv`; and `phenomena_harmonization.ipynb`, which writes `phenomena_longform.csv`, `phenomena_unified.csv`, `phenomena_helioknow_coverage.csv` and `phenomena_gaps_not_in_helioknow.csv` with `quoting=csv.QUOTE_ALL`.
- **JSON** — `interfaces/data_availability_dashboard/Helio-KNOW_metadataFileCreator.ipynb` writes `helioKNOW_metadata.json` via `json.dumps`; all three `LitNetworkBuilder_*.py` scripts write JSON caches and statistics. The Java `KGServlet` also serializes SPARQL results to JSON with Jackson and writes them to the HTTP response.
- **ascii** — `SSCWeb_Scraper.ipynb` writes a provenance text file (`f = open(os.path.join(save_directory,'README_1987.txt'), "w")`) recording the generation timestamp and the definitions of the GEO and GM coordinate systems.
- **Other** — OWL/RDF serialization, which is the repository's signature output: `tools/AutOntologyTool/CfHA_Parsing_Heliophysics_data.ipynb` builds an rdflib `Graph` with its own namespace, adds the extracted triples and labels, and serializes to an OWL file (the README's final stage: "the graph was serialised to an OWL file"). The `data-models/*.ttl` artifacts are themselves the maintained Turtle output of this work.

**`CDF` and `HDF5` were considered and rejected as outputs** — both are read but never written; the CDF path is deliberately one-way (CDF in, DataFrame and CSV out). `FITS`, `IDL.sav`, `netCDF3/4`, `Zarr`, `ISTP-Compliant` — no evidence.

### 20. Operating System (RECOMMENDED)

**Linux**
**Mac**
**Windows**

This value is **inferred, not tested**, and the inference is stated plainly because there is no authoritative source. There is no CI configuration of any kind: `.github/` contains only `ISSUE_TEMPLATE/bug_report.md` and `ISSUE_TEMPLATE/feature_request.md`, with no `workflows/` directory, no `.travis.yml`, and no tox or nox configuration; and there is no installation documentation anywhere in the repository. The basis is therefore the dependency stack: `environments.yml` and `tools/AutOntologyTool/environment.yml` pin only pure-Python or wheel-distributed packages (numpy, pandas, matplotlib, IPython, nbconvert, jupyter, tika, nltk, rdflib, spacy, gensim, networkx, scikit-learn, scipy, beautifulsoup4, tqdm, requests), all of which are available on Linux, macOS, and Windows; and the Java component targets JVM release 13, which is cross-platform. Development is evidenced on macOS from the hard-coded `/Users/ryanmcgranaghan/...` and `/Users/ryanmc/...` paths and the commit author string `meganpowers@Megans-MBP.home`.

**`Operating System Independent` was considered and rejected**, for two concrete reasons. First, `spacepy.pycdf` — the only way the DMSP SSJ CDFs are read — requires the NASA CDF C library to be installed separately, and that library is a platform-specific binary; no truly OS-independent install path is demonstrated. Second, the notebooks contain hard-coded POSIX absolute paths that will not resolve on Windows without edits. Naming the three platforms is the more honest claim than asserting independence.

`Solaris`, `MobilePlatform`, `Other` — no evidence. (Note that the cross-platform choice is spelled out in full as `Operating System Independent`; `OS Independent` is not an available value.)

### 21. CPU Architecture (RECOMMENDED)
**CPU Independent**

Nothing in the repository is architecture-dependent: there is no compiled C, C++, Fortran, or Cython source, no build system producing native binaries, and no architecture-specific wheels or conditional dependencies. The only compiled artifacts checked in are five Java `.class` files under `KnowledgeGraphServer/target/classes/com/nasa/`, and JVM bytecode is architecture-independent by construction. The Python side is interpreted, with all native dependencies supplied as portable wheels.

**`GPU` was considered and rejected.** `tools/ML/DMSP_CDFfile_analysis.ipynb` imports TensorFlow and Keras, which can use a GPU, but the notebook only calls `load_model(...)` on pre-trained `.h5` artifacts and runs inference; there is no CUDA code, no device placement, no `tf.config` device selection, and no statement anywhere that a GPU is required or supported. Importing a framework that is GPU-capable is not the same as requiring or supporting GPU execution.

`x86-64` and `Apple Silicon arm64` were also considered. Both would be *true* — development plainly happened on macOS, and everything runs on x86-64 — but neither is a *requirement*, and listing specific architectures would wrongly imply others are excluded. `Sun (SPARC)`, `Linux aarch64 or arm64`, `ppc64le`, `HPC or HEC`, `Other` — no evidence.

### 22. Related Phenomena (OPTIONAL)

**Coronal Mass Ejections**
**Geomagnetic Storms**
**Solar Flares**
**Solar Wind**
**X-ray emission**

Five of the seven values in the closed `Phenomena` list — the whole of what this vocabulary can express about this software, for the reason set out at the end of this field.

- **Coronal Mass Ejections** — `hk_phenomenon.ttl` defines `Coronal Mass Ejection` as a phenomenon concept, and `data-models/hk_cq.rq` records competency-question output placing it in the Chromosphere, Corona and Photosphere regions. `hk_model.ttl` catalogues CME-related models (DBM, KINCAT, CORHEL with CMEs, MLSO K-Cor CMEs).
- **Geomagnetic Storms** — `hk_phenomenon.ttl` defines `Geomagnetic Storm`; the working use case across `tools/ML/DMSP_CDFfile_analysis.ipynb` and `community/storymaps/dataExploration.ipynb` is the 17 March 2015 St. Patrick's Day storm ("This is a data exploration script using the March 17, 2015 storm as a use case"), with a 2013-03-17 event as a secondary check; SymH and AE/AL/AU storm indices are read from OMNI. This is the strongest of the five.
- **Solar Flares** — `hk_phenomenon.ttl` defines `Flare`; `hk_model.ttl` catalogues numerous flare-forecasting models (A-EFFort, ASAP, AMOS, ASSA, DAFFS, SIDC Flare Forecasting, MAG4, Solar Particle System Flare Forecast).
- **Solar Wind** — `hk_phenomenon.ttl` defines `Solar Wind`, `Solar Wind Shock` and `Interplanetary Magnetic Field`; OMNI solar-wind parameters drive the ML models (Field 4).
- **X-ray emission** — `hk_phenomenon.ttl` defines `Solar X-ray Radiation`.

**`Coronal Heating` and `Solar Corona` were considered and rejected.** A case-insensitive search across `hk_phenomenon.ttl`, `hk_region.ttl`, `hk_core.ttl` and `hk_model.ttl` finds no coronal-heating concept at all. The corona *is* represented in this repository, but as a **region** in `hk_region.ttl`, not as a phenomenon — and it is already recorded that way in Field 5. Selecting `Solar Corona` here would duplicate that with a worse fit. (Note also that `Coronal Holes` is not an available value here, despite older documentation that treats it as though it were.)

**Why this field understates the software, and where the rest went.** The phenomena this repository is genuinely built around are almost entirely absent from the closed 7-value vocabulary. `hk_phenomenon.ttl` maintains roughly 120 phenomenon concepts, and the ones central to Helio-KNOW's stated science focus — Particle Precipitation, Poynting Flux, Joule Heating, Substorm, Diffuse/Monoenergetic/Broadband/Proton/Pulsating Aurora, Auroral Electrojet, Dayside and Tail Reconnection, Ion Outflow, Field-Aligned Currents (Region 1 / Region 2), Ionospheric Conductivity, SAPS, SAID, STEVE, Storm-Enhanced Density, Polar Cap Patch, Tongue Of Ionization, Wave-Particle Interaction — have **no applicable controlled value**. Field 22's own guidance covers this case: a phenomenon the software supports that has no applicable controlled value belongs in Keywords (Field 16, the open vocabulary), not here. Accordingly `particle precipitation`, `electron precipitation`, `poynting flux`, `aurora` and `magnetosphere-ionosphere coupling` are recorded in Field 16. The five values above are the complete correct answer for this field; the apparent mismatch between them and the software's actual subject is a vocabulary limitation, not an extraction gap.

### 23. Development Status (RECOMMENDED)
**Active**

Evidence for continuing active development: commits in every year of the project's life, with 45 in 2021, 45 in 2022, 10 in 2023, 3 in 2024, 51 in 2025, and 16 in 2026 — the 2025 total being the highest of any year. The most recent commit is `31ef424` on 2026-07-20 ("harmonization with phenomena update"), roughly two weeks before this extraction; the GitHub API reports `pushed_at: 2026-07-20T14:10:18Z`, `archived: false`, `disabled: false`, with 17 open issues. Recent work is substantive rather than housekeeping: a new `hk_model.ttl` and BFO alignment in early 2026, then five commits between March and July 2026 building out the glossary and phenomena harmonization pipeline, explicitly "for IHDEA". The project also has demonstrable external adoption — `CONTRIBUTING.md` records that "In Fall 2025 we contributed 173 concepts in a full taxonomy that were co-identified with the Heliophysics community and harmonized in cooperation with the UAT steering committee to establish a new version of the astronomy thesaurus", and `data-models/README-data-models.md` notes the region taxonomy "is used by the helio.data website".

**`WIP` was seriously considered and was the genuine alternative.** repostatus.org defines WIP as "Initial development is in progress, but there has not yet been a stable, usable release suitable for the public", and several facts point that way: there has never been a release or tag (Field 12); `CONTRIBUTING.md` calls the ontology suite "the first official draft of HelioKNOW" and lists substantial gaps ("the notion of temporality is absent from the model"); `interfaces/README-interfaces.md` marks the data-availability dashboard "(currently only in exploration stage)"; the FAST branch of the data pipeline is `# FORTHCOMING...`; and the notebooks are not installable or path-portable.

`Active` was chosen because the criterion that separates the two is whether a usable public release exists, and the ontologies are exactly that: published, versioned, externally consumed artifacts (accepted into the UAT, in use on helio.data) that a user can fetch and apply today. The tools are immature; the flagship deliverable is not. Given five years of unbroken development and the highest commit year being the most recent full one, `Active` describes the project better than `WIP`.

`WIP` is therefore recorded as considered and rejected, not as an open alternative. The reasoning that decided it is the one above: the criterion separating the two values is whether a usable public release exists, and weighting "no release has ever been cut" above "the ontologies are published, versioned, and in external use" would describe the immature tools while ignoring the flagship deliverable. Both cases are preserved so that a future refresh can re-examine the choice against new evidence — a first tagged release, or a lapse in commit activity — rather than re-deriving it from scratch.

### 24. Documentation (RECOMMENDED)
`https://github.com/rmcgranaghan/Helio-KNOW/wiki`

The wiki is the project's own designated resources location — `README.md` states "there is a [Wiki page](https://github.com/rmcgranaghan/Helio-KNOW/wiki) for this repo where resources and updates are posted" — and SoMEF independently identified it (`documentation`, format `wiki`). It resolves and has real content across four pages: Home, Activities, Links-to-bring-together-Heliophysics-Tools, and Publications.

Two honest caveats. First, **the repository has no installation instructions anywhere**, so no URL can fully satisfy Field 8's "documentation and installation instructions". The closest thing to install guidance is the header comment in `environments.yml` (`# run: conda env create --file environment.yml`, which itself names the file incorrectly) and the "Prerequisites: 1. pip install sscws" cells in the two SSCWeb notebooks. Second, the substantive per-component documentation is the README set inside the repository — `README.md` plus `tools/README-tools.md`, `data-models/README-data-models.md`, `data-pipelines/README-data-pipelines.md`, `interfaces/README-interfaces.md`, `community/README-community.md`, `data/README-data.md`, `tools/ADS_enrichment/README.md`, `tools/AutOntologyTool/README.md` (an unusually complete 37-figure walkthrough), and `interfaces/User_Interface_with_Interactive_Knowledge_Graph/README.md`.

The repository root URL was considered as an alternative but rejected because it duplicates Field 3 exactly, whereas the wiki adds a distinct resource the maintainer explicitly points readers to. There is no Read the Docs site: no `.readthedocs.yml`, no `docs/` directory, and no Sphinx configuration have ever existed.

### 25. Funder (OPTIONAL)

**1. National Aeronautics and Space Administration** — `https://ror.org/027ka1x80`

`README.md` states the project is "funded through the NASA Heliophysics Early Career Investigator Program (ECIP)". Corroborated by the repository's own `data/ECIP_awards_2020.pdf`, whose cover page identifies it as "Early Career Investigator Program / Abstracts of Selected Proposals / (NNH20ZDA001N-ECIP)" and which contains McGranaghan's selected Helio-KNOW abstract. The acronym is expanded per Field 25's instruction ("Avoid acronyms"); the full name is the ROR record's primary name for `https://ror.org/027ka1x80`.

**2. Heliophysics Digital Resource Library** — `https://ror.org/00d1g0h88`

`tools/ADS_enrichment/README.md` states: "It is funded by the NASA Heliophysics Digital Resource Library (HDRL) and in-part supported by the NASA ADS team and the [NASA Center for HelioAnalytics]". HDRL has its own ROR record (`https://ror.org/00d1g0h88`, type "government", located in Greenbelt, a child of NASA's Heliophysics Science Division and parent of the Space Physics Data Facility and Solar Data Analysis Center), so it can be named precisely rather than folded into NASA. Listed separately because it funds a distinct body of work in this repository — the ADS enrichment and vocabulary effort in `tools/ADS_enrichment/` — rather than the ECIP-funded core.

**Considered and not selected — Earth Science Information Partners** (`https://ror.org/03q5xa910`). `tools/ADS_enrichment/README.md` notes that a description of glossary harmonization "was created as part of an Earth Science Informatics Partners (ESIP) Funding Friday grant in Summer 2021". The wording attributes the grant to an explanatory document hosted on Google Drive rather than to code in this repository, and the `tools/glossary_harmonization/` work is a later continuation rather than the funded deliverable. Evaluated and **not recorded** on that basis. Recorded rather than dropped so a future agent knows the candidate exists and why the lineage was judged insufficient; documentary evidence tying the Funding Friday grant to code in this repository would be grounds to revisit it. (Separately, `CODE-OF-CONDUCT.md` adopts the ESIP Community Participation Guidelines, which is a governance borrowing, not funding.)

**Considered and rejected — NASA Center for HelioAnalytics and the NASA ADS team.** The same README sentence describes these as providing support "in-part", and `interfaces/README-interfaces.md` describes the CfHA graph as the target of the contributed interface. Both are collaborators and users, not funders, and Field 25 is specifically "a person or organization that supports (sponsors) something through some kind of financial contribution."

### 26. Award Title (OPTIONAL)
- **Award Title:** `Understanding the high-latitude geospace system to the point of prediction: The Heliophysics KNOWledge Network (Helio-KNOW)`
- **Award Number:** `80NSSC21K0622`

**The award title comes from a primary source inside the repository.** `data/ECIP_awards_2020.pdf` — NASA's official "Early Career Investigator Program / Abstracts of Selected Proposals (NNH20ZDA001N-ECIP)", which records that "54 proposals were received ... On December 3, 2020, 15 proposals were selected for funding" — contains the entry:

> Ryan McGranaghan/Atmospheric & Space Technology Research Associates
> Understanding the high-latitude geospace system to the point of prediction: The
> Heliophysics KNOWledge Network (Helio-KNOW)

The title is transcribed with line breaks removed. It is 123 characters, just inside the 128-character maximum an award title accepts — a limit the submission form does not document — so any future rewording of this title must be re-measured against it.

That the abstract is the right one is confirmed by content, not just by name: the abstract's opening paragraph is reproduced nearly verbatim as the "Description" section of the repository's `README.md` (the SWMI complexity paragraph and the "new and possibly disruptive data analytic approach" sentence), and the README's own "More information" link points to the NSPIRES copy of this very PDF with the instruction to look "under 'Ryan McGranaghan'".

**The award number is not stated in the repository** and was established externally; the chain is recorded so it can be audited or corrected rather than re-derived.
- Crossref's structured funder metadata for `10.1016/j.acags.2023.100142` — McGranaghan, Young, Powers, Yadav & Vakaj (2023), the paper describing the CfHA ontology that is distributed in this repository — lists funder "National Aeronautics and Space Administration" with award `80NSSC21K0622`.
- Crossref's funder metadata for `10.1051/swsc/2021037` (McGranaghan et al. 2021) lists the same NASA award `80NSSC21K0622`, and that paper's acknowledgment identifies it specifically as a NASA Early Career Investigator Program grant supporting his work.
- The ECIP PDF establishes that McGranaghan has exactly one ECIP award, made in the December 2020 selection, and that its title is the Helio-KNOW proposal.

Note what was checked and did **not** confirm it: the ASTRA press release announcing the award ("ASTRA Researcher Wins Prestigious NASA Grant", 2021-03-10) names the programme and the 15-awardee selection but gives no grant number. `NNH20ZDA001N-ECIP`, which does appear in the repository, is the ROSES-2020 **solicitation** identifier, not an award number, and was rejected for this field on that basis.

**A caveat that travels with this value.** The award number rests on external publication metadata rather than on anything in the repository. Two independent Crossref records corroborate it, which is why it is recorded, but it is not attested in a primary grant record; anyone with access to one should confirm it rather than assume it is authoritative.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**1. `https://doi.org/10.1016/j.acags.2023.100142`**
McGranaghan, R. M., Young, E., Powers, C., Yadav, S., & Vakaj, E. (2023). The cultural-social nucleus of an open community: A multi-level community knowledge graph and NASA application. *Applied Computing and Geosciences*.

The strongest entry, because the repository cites it itself: `data-models/README-data-models.md` introduces the CfHA Ontology and then gives this exact citation as the paper in which it is "described". The ontology is distributed here twice (`data-models/CfHA_Ontology_V_4.2.owl` and `interfaces/User_Interface_with_Interactive_Knowledge_Graph/latest_updated_ontology_file/CfHA_Ontology_V_4.2.owl`, alongside `CFHA V 4.1.owl`), and the contributed interface is the frontend for the knowledge graph the paper describes. Two of its five authors (McGranaghan, Yadav) are authors of this software.

**2. `https://doi.org/10.1029/2020SW002684`**
McGranaghan, R. M., Ziegler, J., Bloch, T., Hatch, S., Camporeale, E., & Lynch, K. (2021). Toward a Next Generation Particle Precipitation Model: Mesoscale Prediction Through Machine Learning (a Case Study and Framework for Progress). *Space Weather*.

This is the science behind `tools/ML/DMSP_CDFfile_analysis.ipynb`. The correspondence is exact rather than thematic: the notebook reads DMSP F16/F17/F18 SSJ precipitating-electron CDFs, assembles OMNI solar-wind drivers plus the Newell and Borovsky coupling functions into a 70-feature input vector, evaluates trained neural-network and LightGBM models of auroral electron energy flux on an MLAT/MLT grid, and compares them against OVATION Prime — which is the method of this paper. It is also the first entry on the project wiki's own Publications page, so it is developer-prioritized in the sense Field 27 asks for.

**3. `https://doi.org/10.1029/2009JA014326`**
Newell, P. T., Sotirelis, T., & Wing, S. (2009). Diffuse, monoenergetic, and broadband aurora: The global precipitation budget. *Journal of Geophysical Research: Space Physics*.

Included because the software uses this paper's results directly, not merely cites them. `data-pipelines/particle_precipitation_data_pipeline_experiment_v1.ipynb` names it as the specification for the pipeline's classification step ("Identify the four main types of particle precipitation in the data segment ... Ryan will code the identification from Newell et al., [2009]"), and `tools/ML/DMSP_CDFfile_analysis.ipynb` already implements two things from it: `NewellCF_calc(vsw, Bz, By)`, the Newell solar-wind coupling function, and the `auroral_flux_types = ['diff','mono','wave']` categories that drive the OVATION Prime estimator — which are this paper's diffuse, monoenergetic, and broadband classes.

Considered and not selected, with reasons:
- **`https://doi.org/10.1051/swsc/2021037`** (McGranaghan et al. 2021, "Space Weather research in the Digital Age and across the full data lifecycle: Introduction to the Topical Issue") — listed on the project wiki and the source of the award number in Field 26, but it is a topical-issue editorial that neither describes, cites, nor uses this software.
- **The remaining nine entries on the project wiki's Publications page** — Ziegler & McGranaghan 2021 (arXiv:2111.14998), Ringuette et al. 2022 (`10.1016/j.asr.2022.05.012`), Upendran et al. 2022 (`10.1029/2022SW003045`), Haines & McGranaghan 2021 (`10.1029/2020SW002624`), Nishimura et al. 2021 (`10.1002/9781119815617.ch3`), McGranaghan et al. 2021 (Space Data Knowledge Commons essay), Thomas et al. (research-infrastructure workshop report), McGranaghan et al. 2020 (`10.5281/zenodo.4031888`), and McGranaghan et al. 2020 (`10.5281/zenodo.4048814`). These are the principal author's broader research programme rather than publications tied to code in this repository, and listing all twelve would dilute the field to the point of carrying no signal. Recorded here in full so a future agent can promote any of them deliberately rather than rediscover the list.
- **`https://doi.org/10.1029/2021JA029205`** (Billett et al. 2021) — genuinely related, but it describes a *dataset* the software reads, so it belongs in Field 28 and is recorded there.

### 28. Related Datasets (OPTIONAL)

**1. `https://doi.org/10.48322/1rnz-f067`**
Redmon, R. J., & Kilcommons, L. M. (2023). *DMSP F16 Special Sensor J, SESS/SSJ5, Precipitating Electrons and Ions Observed at 850 km, 1 s Data* [Data set]. Space Physics Data Facility.

The dataset the pipeline reads. `data-pipelines/particle_precipitation_data_pipeline_experiment_v1.ipynb` sets `DMSP_dataset = 'DMSP-F16_SSJ_PRECIPITATING-ELECTRONS-IONS'` and retrieves it through `cdasws`; the notebook's captured output includes the dataset's own attributes, among them `DOI: ['https://doi.org/10.48322/1rnz-f067']` and `spase_DatasetResourceID: ['spase://NASA/NumericalData/DMSP_5D-3/F16/S...']`. Verified against DataCite: publisher "Space Physics Data Facility", `resourceTypeGeneral: Dataset`, resolving to `https://spase-metadata.org/NASA/NumericalData/DMSP_5D-3/F16/SESS/SSJ5/PT1S`. That landing URL independently corroborates the Field 31 instrument resolution to `SMWG/Instrument/DMSP_5D-3/F16/SESS/SSJ5`.

**2. `https://doi.org/10.5281/zenodo.4281122`**
McGranaghan, R. M., Bloch, T., Ziegler, J., Hatch, S., Camporeale, E., Owens, M., Lynch, K., & Gjerloev, J. (2020). *DMSP Particle Precipitation AI-ready Data* [Data set]. Zenodo.

The training data behind the machine-learning models in `tools/ML/DMSP_CDFfile_analysis.ipynb`. The Zenodo record's own description states that the dataset "accompanies the manuscript 'Next generation particle precipitation: Mesoscale prediction through machine learning ...' ... and used to produce new machine learning models of particle precipitation from the magnetosphere to the ionosphere" — i.e. the models the notebook loads and evaluates. It is also cited on the project wiki's Publications page, which is where the version DOI recorded here comes from; the all-versions concept DOI is `https://doi.org/10.5281/zenodo.4281121`. The version DOI is the value recorded here because it is what the wiki cites; the concept DOI is the more durable identifier across future versions of the dataset.

**3. `https://doi.org/10.1029/2021JA029205`**
Billett, D. D., Perry, G. W., Clausen, L. B. N., Archer, W. E., McWilliams, K. A., Haaland, S., et al. (2021). The Relationship Between Large Scale Thermospheric Density Enhancements and the Spatial Distribution of Poynting Flux. *Journal of Geophysical Research: Space Physics*.

Recorded here rather than in Field 27 because Field 28 explicitly accepts "the publication that described the dataset" when the dataset has no DOI of its own. `community/storymaps/dataExploration.ipynb` reads a SuperDARN/AMPERE-derived Poynting flux product (`20150317_sd_amp_pf.h5`, `20100101_sd_amp_pf.h5`) and gives this citation as its reference, followed by a "Description of the data from Danielle Billett" documenting the file's quality flags, the 3D `[n_lats × n_lon × n_times]` Poynting flux array, the equal-area AACGM grid above 50° latitude, the MLT-to-longitude shift variable, and the OMNI GSM IMF data included with it. The dataset itself has no DOI, so its describing publication stands in for it.

### 29. Related Software (OPTIONAL)

**1. `https://github.com/oms9/LitNetworkBuilder`**
The upstream home of the LitNetworkBuilder tool vendored into `tools/LitNetworkBuilder/`. `tools/README-tools.md` links it explicitly for the network-graph stage: "creating a network graph and generating some graph statistics, [more info and demo notebook here!]". Its GitHub description is "2022 NASA Summer Internship - HelioKnow Utilities", so it is unambiguously this project's companion repository, authored by the same person (Omar Shalaby, Field 6) and holding the demo notebook that this repository's copy lacks. It is licensed Apache-2.0, unlike this repository's GPL-3.0, which is worth knowing for anyone reusing that tool.

**2. `https://github.com/meganpowers1/SemanticNaturalLanguageProcessingforKnowledgeGraphsCreation`**
The project `tools/AutOntologyTool/` came from. `tools/AutOntologyTool/README.md`'s heading is literally `# SemanticNaturalLanguageProcessingforKnowledgeGraphsCreation`, and every one of its 37 walkthrough figures is served from `github.com/meganpowers1/SemanticNaturalLanguageProcessingforKnowledgeGraphsCreation/blob/main/AutOntFigures/...`. This is the predecessor repository for a whole component of this software, which is exactly what Field 29 asks for ("software this work was forked from should also be included").

**3. `https://pypi.org/project/sscws/`**
NASA's Satellite Situation Center Web Service client library. A domain-specific dependency that characterizes the software rather than a generic one: without it, the entire `tools/tools_for_SSCWeb/` capability and the platform-availability database behind `interfaces/data_availability_dashboard/` do not exist. Both notebooks link this exact URL themselves ("This notebook uses [sscws](https://pypi.org/project/sscws/)") and list "pip install sscws" as their prerequisite. PyPI is the canonical link because the package has no public code repository (its only project URL is the API documentation at `berniegsfc.github.io/sscws/REST/`).

**4. `https://pypi.org/project/cdasws/`**
NASA's Coordinated Data Analysis System (CDAWeb) Web Service client library, the sole data-access mechanism in `data-pipelines/particle_precipitation_data_pipeline_experiment_v1.ipynb`, which names it in its own install note (`pip install -U xarray cdflib cdasws`). Same reasoning and same absence of a public repository as `sscws`.

**5. `https://github.com/lkilcommons/geospacepy-lite`**
The library providing `omnireader`, used in `tools/ML/DMSP_CDFfile_analysis.ipynb` as `from geospacepy import omnireader` to build OMNI 5-minute and hourly intervals and to compute the Borovsky coupling parameter. A heliophysics-specific dependency, not general infrastructure, and the only route by which the ML models get their solar-wind drivers.

Considered and rejected — recorded so these are not proposed later:
- **rdflib, spacy, nltk, gensim, networkx, scikit-learn, TensorFlow/Keras, LightGBM, BeautifulSoup, Apache Tika, joblib, colorcet, toolz** — all fail the Field 30 test that governs both fields: each would be equally at home in a web app, a finance model, or a biology pipeline. rdflib in particular is tempting given how central RDF is here, but it is general-purpose semantic-web infrastructure used across every domain, not a heliophysics peer tool.
- **Eclipse RDF4J and Ontotext GraphDB** — the same reasoning. A triplestore and its Java API are domain-neutral infrastructure; that they appear in `pom.xml` says nothing distinguishing about heliophysics software.
- **numpy, pandas, matplotlib, plotly, scipy, requests, tqdm, h5py, jupyter** — Tier A generic scientific-Python and tooling stack; being a dependency is not a relationship worth recording.
- **The Unified Astronomy Thesaurus (`github.com/astrothesaurus/UAT`), SWEET, GEMET, GCMD, and SPASE** — all genuinely central to this repository (`CONTRIBUTING.md` devotes a section to UAT alignment, and 173 concepts were contributed upstream), but they are *vocabularies and metadata standards*, not software. Field 29 is a software field. Their role is captured in Fields 16, 17 and 27 instead. This is the most likely mistaken addition to this field and is recorded for that reason.
- **`time_hist2`** — imported by `tools/ML/DMSP_CDFfile_analysis.ipynb` but not present in the repository and not published anywhere findable; a private local module, so there is no URL to record. Worth knowing as a reproducibility gap in that notebook.

### 30. Interoperable Software (OPTIONAL)

**1. `https://github.com/spacepy/spacepy`**
Specific documented exchange, in two places. `data-pipelines/particle_precipitation_data_pipeline_experiment_v1.ipynb` branches on the object type returned by `cdasws.get_data` and handles SpacePy's data model as one of two supported interchange formats:

> `if 'spacepy' in str(type(data)):` → `print(DMSP_var[0], '=', data[DMSP_var[0]]); print(data[DMSP_var[0]].attrs)` — with the comment `# see https://spacepy.github.io/datamodel.html`

That is deliberate handling of another package's documented data model, not incidental internal use. Separately, `tools/DMSP_SSJ_tools/DMSP_SSJ_utils.ipynb`, `exploreSSJ_notebook.ipynb`, and `tools/ML/DMSP_CDFfile_analysis.ipynb` all use `spacepy.pycdf.CDF` objects as the input side of a documented CDF → pandas DataFrame → CSV conversion, iterating SpacePy CDF variables and reading their `.attrs` metadata. SpacePy is a heliophysics peer tool, not infrastructure, so it clears the Tier B bar with cited evidence.

**2. `https://github.com/lkilcommons/OvationPyme`**
`tools/ML/DMSP_CDFfile_analysis.ipynb` does not merely depend on OvationPyme, it exchanges data with it in both directions. It constructs `estimator = ovation_prime.FluxEstimator('diff', energy_or_number='energy')`, calls `get_flux_for_time(datetime(2010,1,1,0,0,0), hemi='N', return_dF=False, combine_hemispheres=True)`, and then consumes OvationPyme's own grid as its prediction grid:

> `mlat_grid = (mlat_grid_ovation).copy(); mlt_grid = mlt_grid_ovation.copy(); mlt_grid[mlt_grid < 0] = 24 + mlt_grid[mlt_grid < 0]`

so this software's ML output is produced on OVATION Prime's coordinate grid and compared against OVATION Prime's flux field, with the notebook's `numFluxThreshold = 5.0e7` commented as a "Value pulled from OvationPyme". It also imports `ovation_utilities`. A shared grid plus a directly comparable output quantity is a demonstrated exchange between peer heliophysics tools.

Considered and rejected:
- **xarray** — Tier B, and the bar is not met. The pipeline notebook's `else` branch does read `data.data_vars[...]` when `cdasws` returns an `xarray.Dataset`, and the install note is `pip install -U xarray cdflib cdasws`, but this is handling whatever type a dependency happens to hand back rather than an exchange this software offers. Nothing in the public surface produces or accepts xarray objects, and the one attempt to use xarray directly is commented out with its own failure noted (`# ds = xr.open_dataset(...) # with xarray (doesn't work with .cdf)`).
- **cdflib** — appears only inside a pip-install comment and a doc-link comment (`# see https://github.com/MAVENSDC/cdflib`); no code imports it.
- **h5py** — used to read one third-party HDF5 file; generic I/O plumbing, Tier A treatment.
- **Jupyter** — the notebooks run in it, which is true of a large share of scientific Python and distinguishes nothing.
- **"Part of the scientific Python ecosystem"** and **"a heliophysics project, so it interoperates with heliophysics packages"** — never sufficient on their own, and neither is claimed here.

### 31. Related Instruments (OPTIONAL)

Three instruments. Each is recorded with its canonical SPASE name and its identifier in the `https://spase-metadata.org/` namespace, because an instrument name is not unique across the SPASE catalogue and the identifier is what pins the entry to a single resource.

| Instrument Name | Instrument Identifier |
|---|---|
| `DMSP/F16, SESS Special Sensor Precipitating Electron and Ion Spectrometer 5, SESS/SSJ5` | `https://spase-metadata.org/SMWG/Instrument/DMSP_5D-3/F16/SESS/SSJ5` |
| `DMSP/F17, SESS Special Sensor Precipitating Electron and Ion Spectrometer 5, SESS/SSJ5` | `https://spase-metadata.org/SMWG/Instrument/DMSP_5D-3/F17/SESS/SSJ5` |
| `DMSP/F18, SESS Special Sensor Precipitating Electron and Ion Spectrometer 5, SESS/SSJ5` | `https://spase-metadata.org/SMWG/Instrument/DMSP_5D-3/F18/SESS/SSJ5` |

**Why these three, and why exactly three.** The repository reads DMSP SSJ precipitating electron and ion data as a primary function, and the spacecraft are named explicitly rather than inferred — this is an explicit supported-platform list, which is the standard of concrete evidence required before listing more than one entry:
- `tools/ML/DMSP_CDFfile_analysis.ipynb`: `filenames = ['dmsp-f16_ssj_precipitating-electrons-ions_20150317_v1.1.3.cdf', 'dmsp-f17_ssj_...', 'dmsp-f18_ssj_...']`, each loaded into `df_f16`, `df_f17`, `df_f18`.
- `tools/DMSP_SSJ_tools/DMSP_SSJ_utils.ipynb`: the same three filenames in its worked example, plus an F16 single-file usage script.
- `data-pipelines/particle_precipitation_data_pipeline_experiment_v1.ipynb`: retrieves the CDAWeb dataset `DMSP-F16_SSJ_PRECIPITATING-ELECTRONS-IONS`, whose DataCite landing URL is `https://spase-metadata.org/NASA/NumericalData/DMSP_5D-3/F16/SESS/SSJ5/PT1S` — an independent confirmation that F16's SSJ5 identifier path is the right one.
- `community/storymaps/dataExploration.ipynb`: reads `dmsp-f17_ssj_precipitating-electrons-ions_20150317_v1.1.3.cdf`.

What the software does with them is squarely "designed to support": it parses the instrument's CDF variables by name (`ELE_DIFF_ENERGY_FLUX`, `ELE_TOTAL_ENERGY_FLUX`, `ELE_AVG_ENERGY`, `CHANNEL_ENERGIES`, `AURORAL_REGION`, `AURORAL_BOUNDARY_FOM`, `ORBIT_INDEX`), decodes the auroral-region flag values to their documented meanings, plots the differential flux spectrogram and the total flux in polar magnetic coordinates, and trains and evaluates models against the measurements. Someone working with DMSP SSJ data would reach for this.

Considered and rejected, each with its reason so the work is not repeated:

- **F19 and S20 SSJ5** (`.../DMSP_5D-3/F19/SESS/SSJ5`, `.../DMSP_5D-3/S20/SESS/SSJ5`) — both are catalogued in SPASE, but no artifact in the repository references either spacecraft's SSJ data. Adding them would be inference, not evidence.
- **F15 SSJ4** (`.../DMSP_5D-3/F15/SEM/SSJ4`) and **5D-2 SSJ4** (`.../DMSP_5D-2/SSJ4`) — both are catalogued in SPASE and `dmspf15` is in the platform list, but that list drives *ephemeris* retrieval only (Field 32); no code reads F15 or 5D-2 SSJ4 science data. The NOAA/NCEI `dmsp-fXX_ssj_precipitating-electrons-ions` product the code parses covers F16–F18.
- **SSUSI** (catalogued in SPASE for F16–S20) and **SSIES** (`.../DMSP_5D-2/SSIES`) — `community/storymaps/dataExploration.ipynb` has `#### SSUSI` and `#### SSIES` headings, but the cells beneath them contain only empty placeholder paths (`ssusi_filename = os.path.join('/Users/ryanmcgranaghan/Documents/DMSP_SSUSIdata','')`), and the notebook's own TODO records "SSUSI status: ... None" and "SSIES status: Do NOT have the March 17, 2015 data yet". Planned, not implemented.
- **FAST instruments** — `.../SMWG/Instrument/FAST/ESA` ("Electro-Static Analyzers", abbreviation `ESA`) matches the CDAWeb dataset `FA_ESA_L2_EES` referenced in the data pipeline's header markdown, but the FAST section of that notebook is entirely `# FORTHCOMING...` with only comment stubs. `FAST/EFLP`, `FAST/TEAMS`, `FAST/MAG` are not referenced at all. FAST *is* supported at the observatory level (Field 32) through the ephemeris tooling, so the mission is not lost — only the instrument-level claim is withheld.
- **Ephemeris "instrument" entries** — SPASE catalogues instrument-level ephemeris resources such as `DMSP_5D3-F16 Ephemeris`, `DMSP_5D2-F09 Ephemeris`, and `FAST Ephemeris`, which superficially match what `SSCWeb_Scraper.ipynb` produces. Rejected because the notebook does not read those catalogued ephemeris *data products*; it requests locations from the SSCWeb service, which propagates orbits itself. The association belongs at the observatory level, and that is where it is recorded.
- **SuperDARN and AMPERE** — both are catalogued in SPASE (`SMWG/Observatory/SuperDARN`, `SMWG/Instrument/SuperDARN/Radars`, `SMWG/Observatory/AMPERE`, plus IUGONET per-radar entries), and `community/storymaps/dataExploration.ipynb` does read a product derived from both (`20150317_sd_amp_pf.h5`, where `sd` is SuperDARN and `amp` is AMPERE). Rejected because the software reads a *third-party derived Poynting flux product* in its author's own custom HDF5 layout, not SuperDARN or AMPERE data in any native format or convention. It implements nothing specific to either facility. Recorded because the filename makes this look like instrument support at first glance.
- **THEMIS ASI** — appears only as a TODO wish ("Include one THEMIS ASI image plotted on a polar plot with DMSP data"). No implementation.
- **The 2,899 `spase:Instrument` and 227 `madrigal:Instrument` individuals in `data-models/hk_instruments.ttl`** — the single most important rejection in this field, because the temptation to expand it is large and the expansion would be wrong. `CONTRIBUTING.md` explains what that file is: "We started by uplifting existing Madrigal and SPASE Instrument data into RDF." It is an instrument *catalogue* lifted into a knowledge graph, so that a user can reason over instrument types, locations (9,348 `geo:Feature` and 3,116 `schema:GeoCoordinates` nodes) and cross-vocabulary `skos:exactMatch` links. Cataloguing an instrument is not being designed to support it: nobody working with, say, the Syowa East HF radar's data would reach for Helio-KNOW to process it, and listing thousands of instruments would make the field meaningless. Fields 16 and 17 record the SPASE and Madrigal relationship instead, which is the accurate representation.

### 32. Related Observatories (OPTIONAL)

Thirteen observatories, each recorded with its canonical SPASE name and identifier.

| Observatory Name | Observatory Identifier |
|---|---|
| `Defense Meteorological Satellite Program` | `https://spase-metadata.org/SMWG/Observatory/DMSP` |
| `DMSP_5D-2/F08` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-2/F08` |
| `DMSP_5D-2/F09` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-2/F09` |
| `DMSP_5D-2/F10` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-2/F10` |
| `DMSP_5D-2/F11` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-2/F11` |
| `DMSP_5D-2/F12` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-2/F12` |
| `DMSP_5D-2/F13` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-2/F13` |
| `DMSP_5D-2/F14` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-2/F14` |
| `Defense Meteorological Satellite Program, DMSP-F15` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-3/F15` |
| `Defense Meteorological Satellite Program, DMSP-F16` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-3/F16` |
| `Defense Meteorological Satellite Program, DMSP-F17` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-3/F17` |
| `Defense Meteorological Satellite Program, DMSP-F18` | `https://spase-metadata.org/SMWG/Observatory/DMSP_5D-3/F18` |
| `Fast Auroral Snapshot` | `https://spase-metadata.org/SMWG/Observatory/FAST` |

Note that SPASE's canonical names are stylistically inconsistent between the two spacecraft blocks: the 5D-2 spacecraft carry the terse forms `DMSP_5D-2/F08`… while the 5D-3 spacecraft carry the long form `Defense Meteorological Satellite Program, DMSP-F16`. Each name is recorded exactly as SPASE gives it rather than normalized to a common style.

**The evidence is an explicit supported-platform enumeration**, stated three times in the repository:
1. `interfaces/data_availability_dashboard/helioKNOW_metadata.json` is a one-line manifest of the platforms the project handles: `{"platforms": ["dmspf06", "dmspf07", "dmspf08", "dmspf09", "dmspf10", "dmspf11", "dmspf12", "dmspf13", "dmspf14", "dmspf15", "dmspf16", "dmspf17", "dmspf18", "fast"]}`.
2. `interfaces/data_availability_dashboard/Helio-KNOW_metadataFileCreator.ipynb` is the notebook that writes it, with the same fourteen entries listed literally.
3. `tools/tools_for_SSCWeb/SSCWeb_Scraper.ipynb` constructs the same set programmatically — `sc_ids = ['dmspf' + str(d).zfill(2) for d in range(6,19)]` then `sc_ids = sc_ids + ['fast']` — and states its purpose as generating "a DB of data availability for the followign missions: DMSP, FAST".

For each of these platforms the software actually does something: it builds a `SatelliteSpecification`, requests locations with GEO and GM coordinates, space-region flags and north/south magnetic footpoints, writes a per-spacecraft-per-day ephemeris CSV, and then `Helio-KNOW_data_availability_dashboard.ipynb` reads that tree back — using the manifest's platform list as its DataFrame columns and branching per platform on the DMSP versus FAST filename convention — to render an interactive availability chart. F16, F17 and F18 are additionally supported at the science-data level (Field 31).

**Two inclusion decisions worth recording.**

*The program-level DMSP entry is included deliberately.* `dmspf06` and `dmspf07` are in the supported-platform list but have **no** SPASE records of their own: nothing in SPASE covers `5D-1`, `/F06` or `/F07`, so the DMSP Block 5D-1 spacecraft are simply not catalogued there. Rather than let two supported platforms vanish, `SMWG/Observatory/DMSP` ("Defense Meteorological Satellite Program") is recorded alongside the eleven specific spacecraft: it covers the program as a whole, including F06 and F07. This is the same spirit as falling back from a missing instrument to its platform — a missing record should not silently drop a real association. It does mean the program entry and its members are both listed, which is redundant but harmless.

*The F19 and S20 spacecraft are excluded.* Both are catalogued in SPASE (`SMWG/Observatory/DMSP_5D-3/F19` and `.../S20`), but neither appears in the platform list nor anywhere else in the repository.

**Considered and rejected:** `SMWG/Observatory/ISS` ("International Space Station"). `tools/tools_for_SSCWeb/SscWsExample.ipynb` calls `ssc.get_locations(['iss'], ['2020-01-01T00:00:00Z', '2020-01-01T01:00:00Z'])` and plots the result in 3D — but that notebook is, by its own first line, an "sscws Example Jupyter Notebook" that "demonstrates using the sscws to access satellite location and (modeled) magnetic field information", and the ISS is its illustrative subject. This is a tutorial name-drop, which the relevance gate excludes explicitly. Nothing in the project's actual platform list includes the ISS. Also rejected: `SMWG/Observatory/SuperDARN` and `SMWG/Observatory/AMPERE`, for the reason given in Field 31.

**On the breadth of this selection.** Thirteen observatory entries is broad, and the full set is the settled value. A coherent tighter alternative was considered and rejected: the program-level `SMWG/Observatory/DMSP`, the three spacecraft whose science data is actually read (F16, F17, F18), and `SMWG/Observatory/FAST` — five entries. The full thirteen stands because the platform enumeration is explicit in three places in the repository and the ephemeris and availability capability is genuinely implemented for every one of them, which is the "designed to support" standard this field applies. The distinction that the five-entry alternative was reaching for is preserved above instead: F08–F15 receive ephemeris and availability handling only, never science-data processing, while F16–F18 are additionally supported at the science-data level and are recorded that way in Field 31.

### 33. Logo (OPTIONAL)
**Not found.**

The repository contains six images in `data/images/`, and all six were examined: `KnowledgeGraphExample.png`, `HeliophysicsLandscapeVisual.png`, `HeliophysicsKnowledgeNetwork.png` and `HelioKNOW_singleslide.png` are the four explanatory figures embedded in `README.md`; `MI Coupling Phenomena Conceptual Model_2023.png` and `MI Coupling Tools Draft Concept Map February 2022.png` are concept maps not referenced by any README. None is a logo — they are diagrams, a project summary slide, and concept maps. `tools/AutOntologyTool/AutOntology_OnePager.png` and the 34 `AutOntFigures/Step*.png` files belong to that tool's walkthrough. `data/README-data.md` describes the directory's purpose as holding "data that are used by the Github repository (e.g., images for display on the front page)", with no mention of a logo.

Also checked and negative: `README.md` has no logo or badge images of any kind; the GitHub API reports no `organization` avatar applicable to the software; and the project is not in any PyHC registry, so PyHC's curated `logo` field — the usual fallback source for this field — is unavailable (see below).

---

## Additional Findings

### PyHC registry: not a member

**Helio-KNOW appears in none of the three PyHC registry files** — `projects_core.yml`, `projects.yml`, `projects_unevaluated.yml` — by name, by description, or by repository URL: no entry's `code` field points at `rmcgranaghan/Helio-KNOW`.

This is expected rather than a problem — the registries list installable Python packages, and Helio-KNOW is a monorepo of ontologies and research notebooks with no package (Field 12) — but it is recorded because PyHC metadata is the highest-priority source when it exists and would otherwise supply curated values for logo, documentation, keywords, and contact. None of those is available for this software, so every value in this file is derived from the repository, its DOI-bearing references, or authoritative external registries (ORCID, ROR, Crossref, DataCite, GitHub).

Two PyHC packages are worth noting as adjacent rather than related: `SpacePy` (core) is recorded in Field 30, and `CDFlib` was rejected there for lack of evidence.
