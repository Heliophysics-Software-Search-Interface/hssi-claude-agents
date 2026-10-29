# HSSI Metadata Extraction Results

**HSSI Software ID:** 1b5fd49d-9131-46ee-b56a-70efbb1effe5
**Repository:** https://github.com/SciQLop/SciQLop
**Source Revision:** e964ab02b7df13977f4d0e1a7291327a872b0b0a (committed 2026-07-26T23:49:27+02:00, branch `main`)
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-10-29
**Validation Status:** PASS

**Seeds used:** live HSSI record for `1b5fd49d-9131-46ee-b56a-70efbb1effe5` (authoritative for current published state) and the previous canonical `hssi_metadata.md` dated 2025-10-09. Live HSSI wins scalar conflicts; still-supported file-only additions are retained; every replacement is explained inline with its evidence.

**Sources, in priority order:** live HSSI record (authoritative for current published state) → PyHC community registry → Zenodo/DataCite for the version DOIs (v0.12.0 at extraction, v0.14.1 at the release update) and the concept DOI → repository primary sources, read at tag `v0.12.0` and the Source Revision for the extraction and at tag `v0.14.1` and `main` head `b6702c70` for the release update (CITATION.cff, `pyproject.toml`, `CHANGELOG.md`, README, `COPYING`, source code, tests, bundled tutorials, CI workflows) → GitHub API (releases, tags, languages, topics) → ORCID public API (author employments) → ROR API (organization identifiers) → HSSI controlled vocabularies (`FunctionCategory`, `Region`, `ProgrammingLanguage`, `FileFormat`, `DataInput`, `Phenomena`, `RepoStatus`, `License`, `InstrumentObservatory`) → Crossref (publication DOIs). The `somef_output.json`, `datacite.json`, `zenodo.json` and `pyhc_community.yml` files sitting in the working tree are stale caches of those upstream sources and are history rather than evidence; the live sources above govern where they differ.

**Release scope note (applies to Fields 4, 12, 13, 17–19, 29, 30):** the latest authoritative release is **v0.14.1** (2026-10-06); v0.12.0 (2026-05-17) held that place until this update. Capability fields are derived from the code as it exists **at tag `v0.14.1`** (commit `a12a635fadf2c14e78945574c0b5a3b3ead8f337`, on `main`'s own lineage), not from unreleased `main`, which had moved on to `b6702c703f2b5d02d4c0dcade7b935b775edc517` (2026-10-22, declaring `0.14.2.dev0`). Citations labelled `v0.12.0` were confirmed present at that tag, and every file they name, apart from those described below as deleted, is still present at `v0.14.1`; citations labelled `v0.14.1` were read at that tag. Post-v0.14.1 `main`-only capabilities that were deliberately **excluded** are listed under Field 4 so they can be picked up at the next release. The catalogue maintainer confirmed this scope for this record on 2026-10-29: the capability fields describe the release users install, and work that reaches `main` after the tag is taken up when it ships.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Note:** Not part of the stored record; supplied at submission/update time.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.7379012

**Source:** Existing HSSI record; re-confirmed against DataCite for `10.5281/zenodo.7379012`, which is the Zenodo **concept** DOI (all versions). Read on 2026-10-29, it reports `version: v0.14.1` and `IsSupplementTo https://github.com/SciQLop/SciQLop/tree/v0.14.1`, and it resolves to the v0.14.1 deposit `10.5281/zenodo.23193945`. The project now cites it itself: `CITATION.cff` at `v0.14.1` declares `doi: 10.5281/zenodo.7379012`, and the README's DOI badge and its "Citing SciQLop" section name it as the DOI covering all versions.

**Known cost — the concept also collects the launcher's deposits.** The repository's separately versioned native-launcher releases, `launcher-v0.1.0` through `launcher-v0.2.2` (2026-09-02 to 2026-09-29), were deposited into this same concept, each with `IsSupplementTo …/tree/launcher-v<version>` (Field 12 explains the launcher). A concept DOI resolves to its most recently created deposit, so it can land on a launcher deposit whenever a launcher release is newer than the latest SciQLop release. That is not a reason to move or clear the value (Field 2 rule 5).

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/SciQLop/SciQLop

**Source:** Existing HSSI record; matches the git remote of the local checkout, `pyproject.toml` `[project.urls] homepage`, the Zenodo v0.12.0 record's `code:codeRepository`, and CITATION.cff `url`.

### 4. Software Functionality (RECOMMENDED)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Hodograms
- Data Visualization: Line Plots
- Data Visualization: Orbit Plots
- Data Visualization: Spectrogram

**History:** HSSI held 9 values until the earlier refresh added 3 — `Data Processing and Analysis: Data Reduction`, `Data Processing and Analysis: Processing`, `Data Processing and Analysis: Spectrogram`. Nothing was removed. The additions are all driven by the `SciQLop.user_api.dsp` signal-processing facade, which **first shipped in v0.12.0** (first commit 2026-04-18; the earliest tag containing it is `v0.12.0`) and therefore did not exist when the record was originally created.

**Change vs the 2025-10-09 canonical file:** that file listed `Data Visualization:Interactive`, which is **not in the controlled vocabulary** — removed. It also listed `Data Visualization:Web-Based`, removed as unsupported (see exclusions below).

**Re-derived at `v0.14.1` — one value added.** The releases v0.12.1 through v0.14.1 add one value, `Data Visualization: Hodograms` (evidence below); the other capabilities they add fall under values already recorded. At `v0.14.1`: `dsp.background_subtract` (`SciQLop/user_api/dsp/_background.py`, per-channel background removal for spectrograms) is further `Processing` and `Data Processing and Analysis: Spectrogram` evidence; interval timelines (`SciQLop/user_api/plot/_timeline.py`) and step-shaped line graphs are new plot types within the existing `Data Visualization` values; colour-by-scalar curves and projection graphs are `2D Graphics` and `Orbit Plots`; and the `cdpp3dview` trajectory provider added in v0.13.0 (`SciQLop/plugins/speasy_provider/speasy_provider.py`, CDPP 3DView orbits and ephemeris with a frame choice) is further `Data Access and Retrieval` and `Orbit Plots` evidence. A case-insensitive sweep of `SciQLop/` at `v0.14.1`, bundled examples excluded, finds no wavelet, curlometer, polarization, pitch-angle or plasma-moment code, and no data animation or movie export (the package's animations are interface effects, such as `QPropertyAnimation` in `SciQLop/components/plotting/ui/time_range_bar.py`); minimum-variance analysis and pitch-angle spectra appear only in bundled tutorial notebooks, which rule 4 excludes.

**Per-value evidence (for the values recorded before this update, every path was confirmed present at tag `v0.12.0` and is still present at `v0.14.1`; the Hodograms evidence is read at `v0.14.1`):**
- **Data Processing and Analysis: Data Access and Retrieval** — `SciQLop/plugins/speasy_provider/speasy_provider.py` builds the Products tree from the whole `speasy.inventories.tree` (nodes explicitly recognized in `build_product_tree`: `amda`, `ssc`, `cda`/`cdaweb`, `csa`, `archive`, `uiowaephtool`) and fetches through `spz.get_data` on scroll/zoom; the `%plot` magic and the product search overlay let users retrieve any product by fuzzy name.
- **Data Processing and Analysis: Time Series Analysis** — the application's core object is the multivariate time-series panel; `dsp.split_segments` performs gap detection/segmentation, `dsp.rolling_mean` / `dsp.rolling_std` gap-aware rolling statistics, `dsp.resample` uniform-grid resampling. Tutorial `SciQLop/examples/tutorials/SciQLop/14-SciQLopDSP.ipynb` §3 builds a live mean±std envelope.
- **Data Processing and Analysis: Spectrogram** — `dsp.spectrogram(data, col=, window_size=, overlap=, window=)` computes per-segment STFT and returns 2-D `(N_time, N_freq)` `SpeasyVariable`s; `dsp.fft` returns per-segment `(freqs, magnitude)`. Tutorial 14 §4 "Live spectrogram with tunable FFT parameters". Kernels come from `SciQLopPlots.dsp` via `SciQLop/user_api/dsp/_arrays.py`; tests `tests/test_dsp_arrays.py`, `tests/test_dsp_speasy.py`.
- **Data Processing and Analysis: Processing** — filter chain `dsp.filtfilt`, `dsp.sosfiltfilt`, `dsp.fir_filter`, `dsp.iir_sos`, plus `dsp.interpolate_nan`; virtual products recompute on pan/zoom, making these live processing pipelines (tutorial 14 §1 wraps a SciPy Butterworth design in a `%%vp` cell with a cutoff knob).
- **Data Processing and Analysis: Data Reduction** — `dsp.reduce(data, op)` (sum/mean/norm over columns), `dsp.reduce_axes(data, shape, axes, op=)` (arbitrary-axis reduction inside multi-component rows), `dsp.resample`, rolling statistics; `Histogram2D` / `panel.histogram2d(x, y)` bins scatter data into an `x_bins × y_bins` grid.
- **Data Processing and Analysis: Analysis** — virtual products compute derived physical quantities from retrieved data (README example: |B| from `bx, by, bz`), and the annotation-layer system lets a user callable analyse a graph's data and return `Marker` / `Span` / `HLine` results (`SciQLop/user_api/layers/`, seven modules present at the tag). The catalog system supports event labelling for statistical multi-mission studies.
- **Data Visualization: Line Plots** — `TimeSeriesPlot.plot()` / `XYPlot.plot()` line and scatter graphs, multi-component vectors, and a secondary `y2` axis (`SciQLop/user_api/plot/_plots.py:24,210,233,249` at `v0.12.0`); test `tests/test_plot_scatter_hline.py`.
- **Data Visualization: Spectrogram** — `ColorMap` rendering of spectrogram-type products; `data_serie_type()` auto-detects `ParameterType.Spectrogram` from the ISTP `DISPLAY_TYPE` attribute; log color scales via `PlotHints`. README panel example plots `mms1_dis_energyspectr_omni_brst`.
- **Data Visualization: 2D Graphics** — colormap rasters, `Histogram2D` density grids, `XYPlot`, graphic primitives (`Pixmap`, `Ellipse`, `Text`, `CurvedLine`, `HorizontalLine`) and in-canvas `Overlay`, and catalog events rendered as color-coded vertical spans (continuous or categorical matplotlib colormaps).
- **Data Visualization: Hodograms** — read at `v0.14.1`. `PlotPanel.plot_product(product, plot_type=PlotType.Projection)` (`SciQLop/user_api/plot/_panel.py:228`, whose documented plot types are TimeSeries, Projection and XY) draws a vector product's components against one another on the three panes of a `ProjectionPlot`, over the panel's time range; for a magnetic-field product these are the field component-versus-component plots that fields/04 gives as the Hodograms indicator. SciQLop's own `_projection_shaped_callback` (`SciQLop/components/plotting/ui/time_sync_panel.py`) splits a vector product into one buffer per component, covered by `tests/test_projection_product_shape.py` (`test_a_vector_product_is_split_into_one_buffer_per_dimension`), and `panel.plot_data(x, y, plot_type=PlotType.XY)` plots any one component against another. That reshaping first shipped in v0.13.0 (`9c821064`, 2026-08-20); before it, a product plotted as a projection stayed empty. At `v0.14.1` a product with more than three components (a field with its magnitude) and static `(t, (N, 3))` data still drew empty projection panes; `0f4ed5fb` on unreleased `main` fixes both. Rules 1–9 exclude nothing here: the value is a live row, exposed by SciQLop's own public API rather than only by an import, shipped in the package rather than only in examples, and drawn through the same SciQLopPlots rendering on which every `Data Visualization` value here rests; rule 12 then includes it. The earlier refresh excluded the value because no feature named as a hodogram is provided or documented. That remains true, but fields/04 judges the capability against its indicator, plotting field component vs component, rather than against a feature's name, so that exclusion is superseded.
- **Data Visualization: Orbit Plots** — *live HSSI value, retained.* Supporting evidence: SSCWeb and `UiowaEphTool` ephemeris products are surfaced as `['x','y','z']` position components (`get_components`, `data_serie_type` in `speasy_provider.py`) with a runtime coordinate-frame selector, and `ProjectionPlot` (`SciQLopNDProjectionPlot`) renders them as parametric curves — i.e. trajectory/orbit projections.
- **Data Processing and Analysis** / **Data Visualization** — required parents, both present.

**Recorded decision — `Coordinate Transforms` (and `Coordinate Transforms: Magnetospheric`) excluded.** v0.12.0 does expose a user-facing coordinate-frame control: `SpeasyPlugin.get_knobs` synthesizes a `ChoiceKnob("coordinate_system")` for SSC products, and the release notes advertise switching frames without re-issuing the plot. But the transform itself is performed **server-side by SSCWeb** — SciQLop only forwards `coordinate_system` into `spz.get_data` — so there is **zero transform mathematics in the package** at v0.12.0. Excluded as a pass-through, not a capability.

**Re-decided at `v0.14.1` — still excluded (rule 5).** `SciQLop/components/agents/tools/orbits.py` (first committed 2026-07-02) shipped in v0.13.0. Its `fetch_transform` downloads 3×3 frame-rotation matrices from the CDPP 3DView REST API into the kernel namespace for the AI assistant, and the tool's own description in `SciQLop/components/agents/tools/_builder.py` says it does not apply the rotation, leaving the multiplication to code the assistant writes; `fetch_ephemeris` passes the frame to 3DView as a request parameter, so the service computes the converted positions. The new `cdpp3dview` trajectory products take their frame the same way, through a `coordinate_frame` choice forwarded to `spz.get_data` alongside SSC's `coordinate_system`. The frames are the user's choice — SSC offers GSE, GSM, SM, GEO, GM, GEI_TOD and GEI_J_2000 (`speasy_provider.py:77–81` at `v0.14.1`), and 3DView its live frame list, falling back to J2000, ECLIPJ2000, HEE, HEEQ, HCI, GSE, GSM, SM, MAG, GEO, MSO, VSO, JSO and KSO when the service is unreachable (`speasy_provider.py:82–83`) — and the user receives positions already converted to the chosen frame. Nothing in the package applies a rotation at `v0.14.1`: a sweep of its Python for rotation or matrix application (`einsum`, `scipy.spatial.transform`, `matmul`) finds only the transform tool's help text. The conversion is computed by the service SciQLop calls, SSCWeb (through Speasy) or 3DView. **Settled by the catalogue maintainer on 2026-10-29: `Coordinate Transforms` is not recorded.** Field 4's rule 5 governs a wrapper whose frames are converted server-side, because the capability exists only in the service being called, and it is preferred here over rule 3's inclusion of a transform the user selects and whose converted output the user receives. The alternative weighed was the catalogue's precedent for that rule 3 reading: the Speasy and VirES Python client records list `Coordinate Transforms` for frames or coordinates a web service computes and the client exposes as a request parameter. **Revisit trigger for the next release:** on unreleased `main`, `SciQLop/components/scenes/frames.py` (first committed 2026-10-14, absent at `v0.14.1`) applies 3DView rotation matrices locally with SciPy's `Rotation` and `Slerp` to redraw trajectories and boundaries in a scene's frame (`scene_plot.set_frame("GSE")`). When that ships, re-decide `Coordinate Transforms` with its `Magnetospheric`, `Heliospheric` and `Planetary` children.

**Other values considered and excluded (audit trail):**
- **Data Visualization: Web-Based** — the 2025-10-09 file claimed it. `SciQLop/core/web_channel_page.py` (QWebEngineView + QWebChannel + Jinja2) backs only the welcome page and the plugin App Store — application chrome, not data visualization. All science plots are native Qt widgets. No plotly/bokeh/dash surface exists.
- **Data Visualization: 3D Graphics** — `SciQLopNDProjectionPlot` projects N-dimensional data onto a 2-D parametric curve; there is no 3-D renderer.
- **Data Visualization: Movies** — no data animation or video export anywhere in the package; its animations are interface effects.
- **Data Processing and Analysis: Energy Spectra**, **: 3D Particle Distribution Processing**, **: Plasma Moments**, **: Pitch Angle Distributions** — SciQLop displays energy-flux spectrograms and can reduce arbitrary axes of multi-component products, but implements no energy-spectrum, distribution-function, moment or pitch-angle computation.
- **Mission-related** (any subcategory) — SciQLop is not part of any mission ground segment or pipeline.
- **Servers and Environments** (any subcategory) — SciQLop manages a per-workspace `uv` virtual environment and launches an embedded JupyterLab server, but these are internal runtime mechanics of a desktop application, not infrastructure software offered to others. The same holds at `v0.14.1` for the agent layer's MCP-shaped tool server (`SciQLop/components/agents/acp/tool_server.py`), which lets the chosen AI backend act on the user's own live session.
- **Models and Simulations** (any subcategory) — no model at `v0.14.1`. **Revisit trigger for the next release:** unreleased `main` adds a built-in `SciQLop/plugins/planetary_scenes/` plugin whose `models.py` implements empirical boundary models — the Shue 1998 magnetopause and Jelinek 2012 bow shock for Earth, the Vignes 2000 bow shock and magnetic pileup boundary for Mars, and the Winslow 2013 magnetopause and bow shock for Mercury — drawn by `panel.plot_scene(...)`; re-decide `Models and Simulations: Empirical` when it ships. The other unreleased additions on `main` — Compare panels (overlay, difference, ratio and log ratio of panel variants) and headless `sciqlop --batch` runs — fall under values already recorded or under none, and are noted so the next release update reads them.
- **Data Processing and Analysis: ML/AI** — `machine-learning` is a longstanding GitHub topic and the catalog system is explicitly useful for building labelled training sets, but v0.12.0 implements no ML. (The Agent Chat is an LLM *assistant* over the app, not machine learning applied to the science data. Re-decided at `v0.14.1`: the product smart search, shipped in v0.13.0 (`SciQLop/components/smart_search/`), ranks the product inventory with `model2vec` text embeddings alongside full-text ranking; that is machine learning applied to searching product names, not to the measurements, so `ML/AI` stays excluded.)

### 5. Related Region (RECOMMENDED)
**Values:**
- Earth Magnetosphere
- Interplanetary Space
- Planetary Magnetospheres

**Source:** Existing HSSI record — all three retained, and all three are Region vocabulary rows.

**Change vs the 2025-10-09 canonical file:** that file had only two values; `Planetary Magnetospheres` is a live-HSSI value the file was missing, and it is well supported — the AMDA/CDPP inventories SciQLop surfaces cover planetary missions, and the developers' own EPSC-DPS 2025 abstract is titled "SciQLop & Speasy: Open-Source Tools for Unified Planetary and Heliospheric Data Analysis" (a meeting abstract, weighed under Field 27 and not listed there).

**Considered and not added:** `Solar Environment` (in the vocabulary, but SciQLop targets *in-situ* plasma measurements and has no solar imaging or remote-sensing functionality) and `Earth Atmosphere` (no atmospheric or ionospheric functionality).

### 6. Authors (MANDATORY)
Union of live HSSI, the 2025-10-09 canonical file, CITATION.cff at `v0.12.0`, and the Zenodo/DataCite v0.12.0 record. **No author is dropped.** Matched by ORCID first, then normalized name.

**Author 1:**
- **Name:** Alexis Jeandet
- **Author Identifier:** https://orcid.org/0000-0003-2892-6924
- **Affiliation:** Laboratoire de Physique des Plasmas
- **Affiliation Identifier:** https://ror.org/05c95bg36

**Author 2:**
- **Name:** Nicolas Aunai
- **Author Identifier:** https://orcid.org/0000-0002-9862-4318
- **Affiliation:** Laboratoire de Physique des Plasmas
- **Affiliation Identifier:** https://ror.org/05c95bg36

**Author 3:**
- **Name:** Benjamin Renard
- **Author Identifier:** https://orcid.org/0000-0003-1847-7627
- **Affiliation:** Institut de Recherche en Astrophysique et Planétologie
- **Affiliation Identifier:** https://ror.org/05hm2ja81

**Author 4:**
- **Name:** Vincent Génot
- **Author Identifier:** https://orcid.org/0000-0002-7708-8077
- **Affiliation:** Institut de Recherche en Astrophysique et Planétologie
- **Affiliation Identifier:** https://ror.org/05hm2ja81

**Author 5:**
- **Name:** Nicolas André
- **Author Identifier:** https://orcid.org/0000-0001-8017-5676
- **Affiliation 1:** Institut de Recherche en Astrophysique et Planétologie
- **Affiliation Identifier 1:** https://ror.org/05hm2ja81
- **Affiliation 2:** Institut Supérieur de l'Aéronautique et de l'Espace
- **Affiliation Identifier 2:** https://ror.org/04gyj6s21

**Sources and reconciliation:**
- The author list is stable: CITATION.cff at `v0.12.0` still declares exactly these five people in this order, and the **Zenodo v0.12.0 record now derives its creators from CITATION.cff** — the GitHub-handle "creators" that polluted older Zenodo versions (`aleroux-itlink`, `itlink-hackathon`, `meriadegp`) are gone. v0.12.0 added no authors and filled in no affiliations, so affiliations below come from ORCID and from the existing HSSI record.
- **Benjamin Renard's ORCID** (`0000-0003-1847-7627`) comes from the live HSSI record only — it is *not* in CITATION.cff. Retained, and independently corroborated: that ORCID's employment record lists Institut de Recherche en Astrophysique et Planétologie (ROR `https://ror.org/05hm2ja81`), exactly the affiliation live HSSI already stores for him.
- **Alexis Jeandet's** affiliation and ROR are the live HSSI values, confirmed by his ORCID employment record (Laboratoire de Physique des Plasmas, ROR `05c95bg36`). The 2025-10-09 file's `@LaboratoryOfPlasmaPhysics` (a raw DataCite string) is superseded.
- **Nicolas Aunai's affiliation is the ROR-backed `Laboratoire de Physique des Plasmas` / `https://ror.org/05c95bg36`** — the same organization recorded for Jeandet. That name is ROR's own display form; HSSI previously stored the organization as `Laboratory of Plasma Physics (LPP/CNRS)`, an English alias plus an acronym matching no name form on the ROR record, and the row was corrected. The superseded label is noted so it is not reintroduced. Both independent sources for Aunai name that one laboratory (LPP, UMR 7648): his ORCID employment record reads "Laboratoire de Physique des Plasmas / CNRS", and the shared byline of the 2025 abstracts reads "CNRS, Laboratory Of Plasma Physics, Palaiseau CEDEX, France". The ROR-identified name is the correct expression of both.
- **Superseded label, recorded so it is not reintroduced:** an earlier revision of this record carried Aunai's affiliation as the free-text `CNRS / Laboratory of Plasma Physics` with no identifier. It named the same laboratory, but without a ROR it could not be recognized as the same organization as Jeandet's, and an unidentified free-text variant of an organization that already has a ROR-backed record should not be recorded here.
- **Nicolas André — two affiliations, both resolved to RORs.** No affiliation appears in any repository or DOI metadata, and HSSI stored none for him before the earlier refresh, so both come from his ORCID record's two concurrent current employments. The first is recorded as **Institut de Recherche en Astrophysique et Planétologie** (ROR `https://ror.org/05hm2ja81`): the ORCID entry for that post names the organization "Conseil National de la Recherche Scientifique" but gives `department: Institut de Recherche en Astrophysique et Planétologie`, `city: Toulouse`, `country: FR`, `role: Staff Scientist`, from 2009-01-01 with no end date — and IRAP (ROR `05hm2ja81`, UMR 5277) lists `Centre National de la Recherche Scientifique` (ROR `https://ror.org/02feahw73`) among its parents, so "CNRS, department IRAP" *is* IRAP. It is recorded under IRAP rather than under CNRS for a second reason: ORCID disambiguates that employment with Funder Registry ID `10.13039/501100007175`, which resolves to **`Conseil` National de la Recherche Scientifique, located in Lebanon** (CNRS-L) — not the French `Centre` National de la Recherche Scientifique (`10.13039/501100004794`, ROR `https://ror.org/02feahw73`). CNRS-L's registry aliases include the bare "CNRS", which is how it wins ORCID's typeahead; the mismatch is treated as an upstream ORCID data-entry error rather than propagated. The second affiliation is **Institut Supérieur de l'Aéronautique et de l'Espace** (ROR `https://ror.org/04gyj6s21`, from 2024-03), disambiguated by ROR in ORCID itself. Both are corroborated for IRAP by the 2025 abstract bylines cited under Génot below.
- **Vincent Génot — affiliation recorded on the developers' bylines alone.** His ORCID record is **completely empty**: zero entries across employments, educations, memberships and services, so ORCID contributes nothing. No affiliation appears in CITATION.cff, `pyproject.toml`, DataCite or Zenodo either. The sources are the developers' own bylines: the two 2025 conference abstracts he co-authored (weighed under Field 27 and left out there as meeting abstracts), whose printed affiliation 3 — *"Institut de Recherche en Astrophysique et Planétologie, CNRS, CNES, UPS, Toulouse, France"* — is attached to both Génot and André on **both** `EPSC-DPS2025-1422` and `EGU25-10101`, and the developers' DASH 2026 poster (Field 27), which prints Génot at IRAP, Toulouse. That is self-declared and consistent across three venues, but it is weaker evidence than André's, which ORCID corroborates; it is recorded as such. The affiliation resolves to the ROR-backed row already stored in HSSI for Renard, so no new organization is created.

  Calibration on byline evidence, recorded deliberately: those same two abstracts print **Renard** at affiliation 2, *"Akkodis, Toulouse, France"* (the DASH 2026 poster does too), whereas both live HSSI and Renard's own ORCID record place him at IRAP — so a printed byline and a registry can diverge, and Renard's affiliation is accordingly left on its registry-backed value rather than changed to match the abstracts. The divergence does not undercut affiliation 3 for Génot: the string itself is independently corroborated as accurate by ORCID's department field and ROR's parent chain (via André), and for Génot there is no competing registry claim to diverge from — his ORCID is empty rather than contradictory.
- **Not added as authors:** the developers' conference abstracts and DASH 2026 deposits (Field 27) carry additional co-authors — Alexandre Schulz, Gautier Nguyen, Patrick Boettcher, Bayane Michotte de Welle, Myriam Bouchemit, Nicolas Dufourg, Ambre Ghisalberti and, on one DASH slide deck, Lina Hadid. CITATION.cff is the project's own authoritative statement of *software* authorship and lists five people; co-authoring a presentation about the software is not software authorship. Recorded here for the audit trail only.

**API-expressibility note (metadata note, not a value):** *adding* an affiliation is safe and idempotent when the payload's identifier matches an organization row that already exists — which is why the three IRAP and ISAE-SUPAERO affiliations recorded here are expressible as written: Génot's IRAP and André's IRAP both resolve by ROR `https://ror.org/05hm2ja81` to the row already used for Renard, and André's ISAE-SUPAERO resolves to a correctly named, ROR-backed row of its own (the shared organization vocabulary held no ISAE-SUPAERO entry beforehand, checked across several spellings). *Replacing or removing* an affiliation is **not** expressible that way — the software update path only ever adds — and an organization's own name and non-blank identifier cannot be rewritten through it at all. This is durable: any future correction that must **change** an author's affiliation rather than add one, or restate an organization's name or identifier, has to be made against the shared organization records themselves; a software-record update cannot accomplish it.

### 7. Software Name (MANDATORY)
**Value:** SciQLop

**Source:** Existing HSSI record; matches CITATION.cff `title`, `pyproject.toml` `name`, the Zenodo v0.12.0 record title, and the repository name.

Expansion (for reference, not the field value): SCIentific Qt application for Learning from Observations of Plasmas.

### 8. Description (MANDATORY)
**Value:**
SciQLop (SCIentific Qt application for Learning from Observations of Plasmas) is a powerful and user-friendly tool designed for the visualization and analysis of in-situ space plasma data. Using SciQLop, users can access tens of thousands of products from major data archives worldwide, explore multivariate time series effortlessly with lightning-fast and transparent downloads, visualize custom products with simple Python code executed on-the-fly, easily label time intervals and make or edit catalogs of events graphically, and analyze data in Jupyter notebooks. SciQLop aims to be the right tool for exploring, labeling, and analyzing huge amounts of space physics data, and is also ideal for teaching space physics and in situ spacecraft data handling to students. More recent releases add opt-in real-time collaborative catalog editing, a signal-processing toolbox that operates directly on retrieved variables, per-project workspaces with isolated Python environments, and community plugins installable from a built-in App Store. SciQLop ships an agent chat dock with pluggable AI backends — Claude Code, GitHub Copilot, OpenCode, and Albert — installable from the App Store. The assistant has access to dedicated tools: it can plot products, fetch and describe data, run notebook cells, and inspect your workspace, all under your control.

**Source:** the description HSSI held before the earlier refresh (identical to the 2025-10-09 file), **preserved byte-verbatim** up to "...handling to students.", followed by the sentence the earlier refresh appended and, from this update, two sentences quoted verbatim from the README's "AI Assistant" section at `v0.14.1` (joined across their line breaks). Every word before them is unmodified.

**Why the two AI-assistant sentences were added (Field 8 rule 3).** At `v0.14.1` the README's own description of the software ("What Is SciQLop?") lists getting help from an AI assistant among the things SciQLop lets a user do, and gives the assistant a section of its own; the stored text omitted it. Rule 3 adopts the project's text verbatim, so the README's two sentences are appended unaltered and every earlier word is kept. They attribute the language-model backends to plugins installed from the App Store, as rule 8 requires; what SciQLop itself ships is the chat dock and the tools the assistant calls (`SciQLop/components/agents/`, tool definitions in `SciQLop/components/agents/tools/_builder.py`). HSSI held the description without them until this update. Re-checked at `v0.14.1`, every clause of the earlier appended sentence still holds: the collaborative-catalogs plugin still ships `"disabled": true`, and the DSP module, workspaces and App Store are all present.

**Reason for the sentence the earlier refresh appended:** the published description had become materially incomplete for a user deciding whether the software is useful. Every clause is supported by primary evidence at `v0.12.0`:
- *opt-in real-time collaborative catalog editing* — `SciQLop/plugins/collaborative_catalogs/` (`client.py`, `cocat_provider.py`, `room.py`), cocat CRDT over WebSocket, README section "Collaborative Catalog Editing", tests `tests/test_cocat_event_meta.py` and `tests/test_cocat_move_catalog.py`. Described as **opt-in** because `SciQLop/plugins/collaborative_catalogs/plugin.json` ships `"disabled": true` at v0.12.0: the feature is implemented, documented and tested, but off by default.
- *signal-processing toolbox* — `SciQLop.user_api.dsp`, 13 functions with `SpeasyVariable` round-trip semantics, tutorial 14.
- *per-project workspaces with isolated Python environments* — `SciQLop/components/workspaces/`, `.sciqlop` TOML manifests, per-workspace `uv` venv, `docs/workspaces-and-uv.md`.
- *community plugins from a built-in App Store* — `SciQLop/components/appstore/`, live registry at `https://github.com/SciQLop/sciqlop-appstore`, hot-loaded plugins.

### 9. Concise Description (OPTIONAL)
**Value:** An ergonomic and efficient application to browse and label in situ plasma measurements from multi-mission satellite data.

**Source:** Existing HSSI record; still byte-identical to `pyproject.toml` `description` at `v0.12.0` and at `v0.14.1`. The GitHub repository description, read 2026-10-29, is the same sentence preceded by "SciQLop is".

### 10. Publication Date (RECOMMENDED)
**Value:** 2018-12-15

**Source:** Existing HSSI record; corresponds to the GitHub repository creation date (GitHub API `created_at = 2018-12-15T19:33:44Z`, also captured by SoMEF as `date_created`).

**Change vs the 2025-10-09 canonical file:** that file recorded `2025-09-22` (the v0.10.0 release date), which is wrong for this field — Field 10 is the date of *first* publication, used for the initial version. Corrected to the live HSSI value.

**Alternatives considered and rejected:** the first commit in history is 2017-05-16 (pre-dating the public repository) and the first Zenodo deposit is 2022-11-29 (`10.5281/zenodo.7379013`, tag `v0.1.0`). The live value (public repository creation) is the most defensible reading and is retained.

### 11. Publisher (RECOMMENDED)
**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** Existing HSSI record; DataCite/Zenodo confirm `publisher: Zenodo` for the concept DOI and for the v0.12.0 version DOI. Matches Field 11's guidance for GitHub–Zenodo workflows.

**Change vs the 2025-10-09 canonical file:** that file used the concept DOI as the publisher identifier, which is incorrect (the identifier should be the publisher's ROR or URL). Corrected to the live HSSI value.

### 12. Version (RECOMMENDED)
**Version Number:** v0.14.1

**Version Date:** 2026-10-06

**Version Description:** the release notes below. They are recorded indented by four spaces so that their `###` headings do not read as sections of this file; the stored value is the same text without that indentation.

    ### Virtual products

    - `%%vp --debug` now prints a report in the cell output, not only on the debug panel: each input with its shape, unit, columns, NaN share, value range and time span, then the same for the result, then the checks. When the function fails, the report shows the error and its traceback. Before, a failing function printed nothing in the cell.
    - Tracebacks of a failing virtual product show your own code again. The line in your function that raised was hidden whenever SciQLop's code called it, which is always. In a development checkout, frames from installed libraries such as speasy were hidden too.

    ### Catalogs

    - Saving right after adding events now keeps them in their catalog. The Save was committed before the step that puts a new event in its catalog, so after a restart the catalog came back empty and the events sat in "Orphan events". This hit the catalog browser's Save too when pressed right after an import, and could also lose the folder of a catalog created just before saving.
    - `catalogs.persist(path)` writes a catalog to disk from a notebook or an agent, like the catalog browser's Save. Writing events from Python only changed them in memory, and nothing in Python could save them.
    - `panel.catalog_mode` reads and sets a panel's catalog mode (`"view"`, `"jump"` or `"edit"`), like the mode combo and Ctrl+Shift+M.
    - Reading or changing a catalog from a cell right after startup waits for its events to load. `catalogs.get()` returned an empty catalog while they were still loading, and `add_events` or `save` then worked from that empty list, so the catalog showed only the new events.
    - The event editor accepts ratings from 1 to 10, the range the catalog store uses. It stopped at 5, so editing an event rated higher by another tool lowered its rating to 5.

    ### Agent chat

    - Agents are told to ask before acting when a request leaves open a choice that changes the result: the product, the time range, the frame, the exact definition of a quantity, or what to deliver. At most three questions, each with the answer they would pick, so a "yes" is enough. Clear requests go ahead without questions.
    - Agents get skills, published into each workspace's `.claude/skills/` folder, where opencode and Claude Code find them: settling what the user wants before a larger task, finding the right data product, designing and testing virtual products, labeling events in catalogs, troubleshooting empty or slow plots, and writing SciQLop plugins. They load only when a task needs them, so they don't lengthen every session. Agents that don't load skills are pointed at the files from `AGENTS.md`.
    - `sciqlop_set_time_range` accepts ISO-8601 times as well as epoch seconds, like `sciqlop_fetch` and `sciqlop_describe_product`. It failed with "could not convert string to float" on the ISO times agents pass to the other tools.
    - The `AGENTS.md` guidance tells agents how to try a virtual product's maths before writing it: load the inputs with `sciqlop_fetch` from their product-tree paths, compute on them, then run the product once with `--debug`. An agent asked for |V_alpha − V_p| spent about ten tool calls hunting Speasy identifiers instead.

    ### JupyterLab

    - The JupyterLab panel no longer stays blank white until you reload it. If the page fails to load, or loads without Lab starting, it is loaded again on its own (jupyqt 0.6.6). This happened mostly on a busy start, such as the first one after an update.

**Version PID:** https://doi.org/10.5281/zenodo.23193945

**Previous values.** HSSI held v0.12.0 (released 2026-05-17, Version PID `https://doi.org/10.5281/zenodo.20261873`) until this update, and v0.10.0 before that; each was superseded by a newer release (Field 12 rule 3). The v0.12.0 description was a condensed summary of that release's changelog section; it belongs to that release and is not carried onto v0.14.1 (rule 10).

**Why v0.14.1** (read at `main` head `b6702c703f2b5d02d4c0dcade7b935b775edc517` and at the tag). The annotated tag `v0.14.1` points at `a12a635fadf2c14e78945574c0b5a3b3ead8f337`, an ancestor of `main` head (`git merge-base --is-ancestor` holds), whose `pyproject.toml` declares `version = "0.14.1"`. The GitHub release `v0.14.1` was published 2026-10-06T17:19:37Z and is neither a draft nor a pre-release. PyPI's JSON API gives `0.14.1` as `info.version`, with a wheel and an sdist uploaded from 2026-10-06T17:19:56Z, neither yanked, and its `project_urls` homepage is this repository. Zenodo's version deposit `10.5281/zenodo.23193945` carries `metadata.version` `v0.14.1`. The `v` prefix follows the form the entry already used; `pyproject.toml` and PyPI write `0.14.1`.

**Nothing newer had been released on 2026-10-29.** `main` head declares `0.14.2.dev0`, a development version (rule 2), and its `CHANGELOG.md` opens an `## Unreleased` section; no later SciQLop tag, GitHub release or PyPI upload exists. A later update should look for the next release, and read Field 4's revisit triggers then; under this record's release-tag scope (header), work on `main` after the tag enters the capability fields only when it ships.

**Releases between v0.12.0 and v0.14.1**, all superseded by v0.14.1 (rule 3): v0.12.1 (2026-08-05) and v0.12.2 (2026-08-06), two JupyterLab hotfixes tagged on a hotfix line descended from `v0.12.0`; v0.13.0 (2026-09-14) and v0.14.0 (2026-10-05) on `main`; and v0.13.1 (2026-10-01), a one-fix patch tagged on a branch descended from `v0.13.0`. The off-`main` tags share history with the pin (their merge bases with `main` are the `v0.12.0` and `v0.13.0` commits), so they are release-branch releases rather than orphan lineages; each is a GitHub release and a PyPI upload, and v0.14.1 is the newest release of the current series.

**The `launcher-v*` tags are a separate component, not SciQLop releases.** `launcher-v0.1.0` through `launcher-v0.2.2` release the native launcher in `launcher/`, a separate CMake project (`project(sciqlop_launcher VERSION 0.2.2 LANGUAGES CXX)` in `launcher/CMakeLists.txt` at `v0.14.1`). Their GitHub releases carry prebuilt launcher binaries with their SHA-256 checksum files, which the installer build scripts consume through `scripts/launcher.version`, and none is an upload of the `sciqlop` package. Under Field 12's one-entry-two-packages rule the record carries the version of the package the entry's name and repository identify, `sciqlop`; the launcher's history stays here. Their Zenodo deposits share the Field 2 concept (see Field 2).

**Version Date.** 2026-10-06, the UTC day of the release's `published_at` (rule 7). PyPI's upload and the Zenodo deposit fall on the same day, and so does the tag object (2026-10-06T19:19:29+02:00, 17:19:29 UTC).

**Version Description.** The release's GitHub `name` is the bare tag, so the description comes from its body (rule 13), which is byte-identical to the `## v0.14.1 — 2026-10-06` section of `CHANGELOG.md` at the tag. Each item reports new or changed behaviour a user meets, or a bug a user could hit, in virtual products, catalogs, the agent chat or the JupyterLab panel, and all are kept verbatim under their section headings (rules 14–15). The item on the `AGENTS.md` guidance is kept rather than dropped as documentation housekeeping: SciQLop publishes that guidance into each workspace (`SciQLop/components/agents/guidance.py`), and it changes how the in-app agents act. Only the section's title line, `## v0.14.1 — 2026-10-06`, is left out: it repeats the version number and date that the site shows beside the notes.

**Version PID.** `10.5281/zenodo.23193945` is the deposit for exactly this release: its `metadata.version` is `v0.14.1`, its only related identifier is `isSupplementTo https://github.com/SciQLop/SciQLop/tree/v0.14.1`, its publication date is 2026-10-06, and the DOI resolves (rule 17).

**Storage warning:** write the **bare** version number `v0.14.1`. The view API renders the stored value as `SciQLop - <number>`; that prefix is a rendering transform and must never be written back.

**Note:** `CITATION.cff` now agrees with the release. At `v0.12.0` it still declared `version: 0.10.0` and the v0.10.0 version DOI `10.5281/zenodo.17176824`; at `v0.14.1` it declares `version: 0.14.1`, `date-released: 2026-10-06` and the concept DOI `10.5281/zenodo.7379012`.

### 13. Programming Language (RECOMMENDED)
**Value:**
- Python 3.x

**Source:** `Python 3.x` is the existing HSSI value. It is the language users write against SciQLop — the `SciQLop.user_api` package, the IPython magics, virtual products and plugins — and the language of its application and analysis code (Field 13 rules 4 and 5). `pyproject.toml` at `v0.14.1` declares `requires-python = ">=3.13,<3.15"` with Python 3, 3.13 and 3.14 classifiers; v0.14.0 dropped Python 3.11 and 3.12 (at `v0.12.0` the bound was `>=3.11,<3.15`).

**Removed — `Javascript`, which HSSI held until this update.** The earlier refresh added it for `welcome.js` and `appstore.js`, which drive the QWebChannel welcome page and App Store (`SciQLop/core/web_channel_page.py`), on the reading that the field lists every language the software is implemented in, interface chrome included. Field 13's rule 4 records instead the language a user writes to use the software plus any compiled or scripted core that carries the science, and rule 9 holds incumbents to the same test. At `v0.14.1` the repository's own JavaScript is still interface chrome — `SciQLop/components/welcome/resources/welcome.js`, `SciQLop/components/appstore/resources/appstore.js` and the agent chat's `SciQLop/components/agents/resources/web/transcript.js`, beside vendored libraries. No user writes JavaScript to use SciQLop, none of it carries the science, and a visitor filtering the catalogue by JavaScript would not be looking for a Python desktop application. Rule 4's other admission, a supported front end in a second language with its own tests or build target, does not fit either: the scripts run inside the embedded web views of SciQLop's Qt and Python interface and are tested as parts of it (`tests/test_web_channel_page.py`, `tests/test_agent_web_transcript.py`, `tests/test_web_transcript_browser.py`), rather than forming a second front end through which users drive the software. Do not re-add it for web-view chrome.

**Not added — `C++`.** Since v0.13.0 the repository holds a native launcher in C++ under `launcher/`: a separate CMake project (`project(sciqlop_launcher VERSION 0.2.2 LANGUAGES CXX)`, C++20, an FLTK interface and, on macOS, Objective-C++), released separately as `launcher-v*` (Field 12) and consumed by the installer builds as prebuilt binaries. It starts and supervises the SciQLop process — splash screen, restart and workspace-switch rounds, the startup error window — while workspace resolution stays in Python (`launcher/src/launcher.hpp` at `v0.14.1`). It is not a language a user writes against and does not carry the science, so rule 4 does not admit it. It has its own tests and build target (`launcher/tests/`, the CMake option `SCIQLOP_LAUNCHER_BUILD_TESTS`), but it is a separately released component (Field 12) rather than a front end to this package's functionality, so rule 4's supported-front-end admission does not apply either. It replaced `scripts/windows/launcher.c`, the single C file this record cited at `v0.12.0`, which no longer exists at `v0.14.1`. The C++ behind SciQLop's plotting lives in the separate SciQLopPlots and NeoQCP repositories (Field 29).

**Change vs the 2025-10-09 canonical file:** that file added `C++` and `Jupyter Notebook`.
- `Jupyter Notebook` is **not in the controlled vocabulary**, and a notebook is a file format rather than a language — removed.
- `C++` was inferred from a CITATION.cff *keyword*, not from code: this repository then held no C++ (GitHub reported zero C++ bytes) and its only C file was `scripts/windows/launcher.c`. Removed; the launcher C++ added since does not change that verdict (above).

### 14. Reference Publication (OPTIONAL)
**Value:** Not found

**Source:** No reference publication is designated anywhere authoritative — CITATION.cff has no `preferred-citation` (still none at `v0.14.1`), the README's "Citing SciQLop" section, added since `v0.12.0`, asks users to cite the Zenodo concept DOI, which is the software record (Field 2) rather than a paper, and neither the Zenodo nor the DataCite record carries an `IsDescribedBy` relation. The DOI in CITATION.cff points at the software deposit itself, not a paper.

**Note:** the developers' publications about SciQLop — a deposited poster and two slide decks from DASH 2026 — are recorded under Field 27, and their earlier conference abstracts were weighed there and left out as meeting abstracts. None is declared by the project as the preferred citation, so Field 14 is deliberately left empty rather than promoting one.

### 15. License (RECOMMENDED)
**License:** GNU General Public License v3.0 or later

**License URI:** https://www.gnu.org/licenses/gpl-3.0-standalone.html

**SPDX Identifier:** GPL-3.0-or-later

**Source:** the license *name* is the existing HSSI value and is a License vocabulary row. It is corroborated by four independent sources that now all agree: CITATION.cff (`license: "GPL-3.0-or-later"`), the `COPYING` file (GPL version 3), the Zenodo v0.12.0 record (`license.id = gpl-3.0-or-later`), and DataCite for the concept DOI, which returns `rights: "GNU General Public License v3.0 or later"`, `rightsIdentifier: gpl-3.0+` and `rightsUri: https://www.gnu.org/licenses/gpl-3.0-standalone.html` — matching the License URI recorded here exactly. `pyproject.toml` points at `COPYING` and carries the GPLv3 OSI classifier.

**The License URI and SPDX identifier are not software fields.** The API's `license` field is the license **name** only, and there is no software-level URI or SPDX key. Both are attributes of the shared `License` vocabulary row, which already carries `https://spdx.org/licenses/GPL-3.0-or-later.html`; editing that row would change the URI for every GPL-3.0-or-later package in HSSI. The URI and SPDX identifier are retained here as durable provenance, not as pending changes.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values (identity-aware union; stored lowercase, rendered Title Case by HSSI):**
- amda
- c++
- catalogs
- cdaweb
- cdpp
- data access
- data analysis
- electric fields
- gui
- heliophysics
- heliosphere
- in-situ measurements
- interactive
- jupyter
- line plots
- machine learning
- magnetic fields
- magnetosphere
- nasa data
- open source
- particle distributions
- plasma
- plasma physics
- plotting
- pnst
- pyhc package
- pyside6
- python
- qt
- remote
- satellite
- scientific software
- signal processing
- space physics
- spacecraft data
- spectrograms
- sscweb
- time series
- visualization
- web service

**Sources at the earlier refresh:** union of the HSSI record as it then stood (7: amda, cdpp, machine learning, nasa data, plasma physics, pnst, satellite — **all retained**), the 2025-10-09 canonical file (its 26 file-only additions retained), CITATION.cff `keywords` at `v0.12.0`, GitHub repository topics as they then stood (`amda, cdpp, machine-learning, nasa-data, plasma-physics, pnst, satellite`), and the PyHC community registry entry for SciQLop (`heliosphere, magnetosphere, plasma_physics, interactive, line_plots, plotting, general, cdaweb, sscweb, web_service, remote, data_access, data_analysis`).

**Normalization applied (documented, not a drop):** underscore and hyphen variants are folded to the space-separated form so near-duplicates are not created — `plasma_physics`/`plasma-physics` → `plasma physics` (matching the live stored value), `line_plots` → `line plots`, `web_service` → `web service`, `data_access` → `data access`, `data_analysis`/`data analysis` → `data analysis`, `machine-learning` → `machine learning` (live), `nasa-data` → `nasa data` (live).

**Added from v0.12.0 evidence (3):** `catalogs` (the catalog browser, providers, overlays and `catalogs.*` user API are a headline feature), `jupyter` (embedded IPython kernel, JupyterLab server, `%plot`/`%%vp`/`%timerange`/`%install` magics), `signal processing` (the new `SciQLop.user_api.dsp` module).

**Brought forward to `v0.14.1`:**
- **Added (2, project-declared, rule 9):** the repository's GitHub topics, read 2026-10-29, are now `amda, cdpp, heliophysics, jupyter, machine-learning, nasa-data, plasma-physics, pnst, pyside6, python, qt, satellite, space-physics, time-series, visualization` — eight more than the seven listed above. Six of the eight bind keywords this record already carries (`jupyter`, `python`, `qt`, `space physics`, `time series`, `visualization`): the topic spellings `space-physics` and `time-series` are separator variants of the stored rows (rule 11), and a separate `space-physics` row in the vocabulary is not the one to bind. `heliophysics` binds its existing row; `pyside6` has no row in any spelling and is minted lower-case (rule 12). Both are accurate: SciQLop is a heliophysics tool built on PySide6.
- **`pyhc package` (rule 15).** SciQLop is listed in the PyHC registry's `_data/projects.yml`, so the record carries the PyHC package marker. HSSI already held it; this record had not listed it.
- **Removed — `general` (rule 2).** It is the PyHC registry's scope tag, which says nothing about the software to a catalogue visitor; HSSI held it until this update.
- **Unchanged sources:** `pyproject.toml` `keywords` and `CITATION.cff` `keywords` at `v0.14.1` equal those at `v0.12.0`, the Zenodo v0.14.1 deposit's keywords equal the `CITATION.cff` list, and the PyHC entry's keywords are as listed above. No term is added for the capabilities v0.12.1 through v0.14.1 added: each falls under a keyword already recorded or under another field.

**Notes:** `c++` is retained because it is an upstream-declared keyword (CITATION.cff and the Zenodo deposit's keywords, unchanged at `v0.14.1`), but it refers to the C++ engine that lives in the **separate** SciQLopPlots / NeoQCP / CDFpp repositories. The C++ this repository has held since v0.13.0 is the separately released native launcher (Field 13). That is also why `C++` is *not* a Field 13 value.

### 17. Data Sources (OPTIONAL)
**Values:**
- AMDA
- CDAWeb
- HTTP/HTTPS Directories
- Other
- SSCWeb

**Source:** `AMDA`, `CDAWeb`, `SSCWeb` and `Other` are existing HSSI values — retained. All five values above are DataInput vocabulary rows. `SciQLop/plugins/speasy_provider/speasy_provider.py` builds the Products tree from Speasy's full inventory and explicitly recognizes the `amda`, `cda`/`cdaweb`, `ssc`, `csa`, `archive` and `uiowaephtool` provider nodes.

**Removed (1) — `Observatory/Mission-specific`, a value HSSI held until the earlier refresh.** No observatory-specific code path exists anywhere at v0.12.0: `build_product_tree` branches on **provider**, and `get_components` / `data_serie_type` branch on generic ISTP attributes — never on a mission or observatory. The value's own rule requires naming the observatory in Field 32, and Field 32 is empty for exactly the same architectural reason (see Fields 31/32). `AMDA` + `CDAWeb` + `SSCWeb` + `HTTP/HTTPS Directories` + `Other` describes SciQLop's data-source coverage accurately without it.

**Added (1) — `HTTP/HTTPS Directories`.** SciQLop surfaces Speasy's generic `archive` provider node in its Products tree (`build_product_tree` maps an `"archive"` icon for it, and the agent tool help text enumerates providers as "amda, cda, ssc, archive, ..." at `SciQLop/components/agents/tools/_builder.py:184` at `v0.12.0`, line 280 at `v0.14.1`), and Speasy's README states it can "Support data access from any local or remote archives described by YAML file." The evidence reaches SciQLop through Speasy, which is exactly how *every* SciQLop data source works — including the already-published AMDA, CDAWeb and SSCWeb — so this value is supported on the same footing as those.

**Considered and not added:** `FTP/FTPS Directories` (no citation found), `HAPI` (mentioned only hypothetically in an `istp_hints.py` docstring — no HAPI client is used), `OMNIWeb`, `das2`, `TAP`, `The Virtual Solar Observatory.`, `VirES`, `S3/Cloud-aware`, `Madrigal`, `GFZ`, `WDC` (no evidence). The Cluster Science Archive (`csa`) is reachable through Speasy's inventory but, like every other archive, via the generic provider mechanism.

**Re-checked at `v0.14.1` — unchanged.** The provider table in `SciQLop/plugins/speasy_provider/speasy_provider.py` now labels each node it builds: `amda` (AMDA), `cda` (CDAWeb), `csa` (the ESA Cluster Science Archive), `ssc` (SSCWeb), `archive`, `cdpp3dview` (CDPP 3DView orbits and ephemeris, added in v0.13.0 with a coordinate-frame choice) and `uiowaephtool` (the University of Iowa ephemeris tool). `Other` stands for the sources with no vocabulary row: the Cluster Science Archive, CDPP 3DView and the Iowa ephemeris tool. SciQLop's label for the `archive` node reads `Local archive files`; that names the common case and does not withdraw the remote-archive support `HTTP/HTTPS Directories` rests on, so the value stays (rule 12). Sources reached through separately installed plugins, such as the radio plugin's e-CALLISTO, I-LOFAR and RSTN dynamic spectra and the seismic plugin's FDSN networks that the developers presented at DASH 2026 (neither plugin is in `SciQLop/plugins/` at `v0.14.1`), belong to those plugins' records (rule 4).

### 18. Input File Formats (RECOMMENDED)
**Values:**
- ascii
- CDF
- csv
- ISTP-Compliant

**Source:** `ascii`, `CDF` and `csv` are existing HSSI values — retained (SciQLop reads science data through Speasy, whose PyHC entry lists `cdf, csv, ascii`). All four are FileFormat vocabulary rows.

**Added (1) — `ISTP-Compliant`.** Direct in-repo evidence at `v0.12.0`: `SciQLop/core/istp_hints.py` ("ISTP metadata → PlotHints translation ... any provider whose upstream metadata follows the ISTP/CDF convention") reads **nine ISTP attributes** directly out of the variable's metadata mapping to configure axis labels, units, scales, valid ranges, fill values and spectrogram detection — `LABL_PTR_1` (:67), `LABLAXIS` (:75, :97), `FIELDNAM` (:102), `VALIDMIN` (:106), `VALIDMAX` (:107), `DISPLAY_TYPE` (:123), `UNITS` (:126), `SCALETYP` (:127) and `FILLVAL` (:130). A tenth, `DEPEND_1`, is handled indirectly: the caller may attach the DEPEND_1 variable's own ISTP attributes as a `_depend_1` sub-mapping (documented at :116, read at :142), whose `UNITS`, `SCALETYP` and valid range are then used to populate the secondary axis hints for spectrogram plots (:146–148). `data_serie_type()` in the Speasy provider keys spectrogram-vs-scalar-vs-vector classification off the same convention; covered by `tests/test_istp_hints.py`.

**Considered and not added:** `JSON` — the app reads `.ipynb` notebooks and JSON plugin descriptors, and `YAML`/`TOML` for panel templates, settings and `.sciqlop` workspace manifests, but these are application configuration rather than scientific data input.

### 19. Output File Formats (RECOMMENDED)
**Value:** Other

**Source:** HSSI held no value for this field before the earlier refresh filled it, and the 2025-10-09 file recorded "Not found". SciQLop does export, but only to formats outside the controlled list, so `Other` is the correct single value. Evidence at `v0.12.0`: `PlotPanel.save(path)` (`SciQLop/user_api/plot/_panel.py:400`) exports a panel as an image, dispatching on extension across `.png`, `.pdf`, `.jpg`, `.jpeg` and `.bmp`; `PlotPanel.save_template()` (`_panel.py:426`) writes panel layouts as YAML templates.

**`JSON` deliberately not selected.** Panel templates, settings and `.sciqlop` workspace manifests are application configuration, not scientific data — the same rule Field 18 already applies to JSON on the input side. Applying it consistently here leaves `Other` alone.

**Note:** no export to ascii, CDF, csv, FITS, HDF5, IDL.sav, netCDF3/4 or Zarr exists, so no listed format may be claimed.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Source:** Existing HSSI record. Re-confirmed against `.github/workflows/SingleExe.yml`, which builds release artifacts on `ubuntu-latest` (AppImage), `macos-latest` at `v0.14.1` (`macos-14` at `v0.12.0` and at the Source Revision) for the Apple Silicon bundle, `macos-15-intel` (Intel bundle) and `windows-latest` (Inno Setup installer); `.github/workflows/tests.yml` runs the test matrix across operating systems; the README documents a Windows installer, macOS app bundles for both architectures, and a Linux AppImage; the README at `v0.14.1` adds that its Flatpak manifest is not yet published on Flathub.

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- Apple Silicon arm64
- CPU Independent
- x86-64

**Source:** Existing HSSI record — all three retained. macOS bundles are built for both Apple Silicon (`macos-latest` at `v0.14.1`, `macos-14` at `v0.12.0`) and Intel x86-64 (`macos-15-intel`); the README instructs users to "pick the right architecture for your Mac (ARM64 for Apple M1/2/3/4 chips and x86_64 for Intel)"; the from-source Python install is architecture independent.

The 2025-10-09 file wrote `CPU Independent (Python-based)`; the controlled value is the bare `CPU Independent`, the form HSSI stores.

**Considered and not added:** `Linux aarch64 or arm64` — the Linux AppImage is produced only on `ubuntu-latest` (x86-64); no aarch64 Linux artifact is published.

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found — deliberately empty. No phenomenon is recorded.

**Change vs the 2025-10-09 canonical file (removal, documented):** that file listed `Magnetic fields`, `Electric fields` and `Particle distributions`, carried over from CITATION.cff keywords. All three are removed for two independent reasons. First, they are **not in the controlled vocabulary**: `/api/models/Phenomena/rows/all/` has exactly seven rows — Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission — so writing them would have minted three custom entries. Second, they are measured *quantities*, not phenomena. Live HSSI has no `relatedPhenomena`, so nothing published is being dropped; the net effect against HSSI is a no-op.

**`Solar Wind` and `Geomagnetic Storms` considered and not added.** Both are in the vocabulary and both are studied with SciQLop, but the same architectural agnosticism that empties Fields 31/32 applies here: SciQLop implements no phenomenon-specific analysis, detection or model, and selecting two phenomena from the many its users study would be as arbitrary as naming three of the hundreds of missions it can browse.

**Note:** the three removed terms remain correctly carried in **Field 16 Keywords** (`magnetic fields`, `electric fields`, `particle distributions`), which is a free-text field and their proper home.

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** `Active` is a RepoStatus vocabulary row; HSSI has held it since the earlier refresh filled the field, which was empty until then. Re-derived on 2026-10-29 (rule 6): the last commit on `main` is `b6702c70`, dated 2026-10-22; the latest release is v0.14.1, published 2026-10-06; `main` declares `0.14.2.dev0` with an `## Unreleased` CHANGELOG section; the repository is neither archived nor disabled; and the README carries no repostatus.org badge (its badges show the PyPI version, Python versions, license, DOI and test status) and no status statement. This matches repostatus.org **Active** ("reached a stable, usable state and is being actively developed").

**Note:** `pyproject.toml` still carries the `Development Status :: 4 - Beta` trove classifier, and PyHC rates documentation, testing and software maturity as "Requires improvement". Neither contradicts repostatus **Active**, which is about development activity rather than maturity.

### 24. Documentation (RECOMMENDED)
**Value:** https://sciqlop.github.io/

**Source:** the project's own documentation site (Field 24 rule 3). It is the repository's declared GitHub homepage, and the README at `v0.14.1` sends readers to it for the step-by-step tutorials. Read on 2026-10-29, `https://sciqlop.github.io/` answers 200 with no redirect, and the site — its pages dated 2026-10-11, built from the `SciQLop/sciqlop.github.io` repository (last commit 2026-10-15) — holds download and installation instructions; a Tutorials section (basic plotting workflow, catalogs, plot templates, virtual products, batch quick-looks); a User guide with one guide per analysis tool (graphic primitives, annotation layers, the DSP toolbox, 2D histograms); a Reference section (the `SciQLop.user_api` Python API split by topic, and the panel-template format); and a What's New page. The site root is recorded, as the documentation's landing page (rule 6). Its API reference states that it documents v0.13.1 and marks development-branch features with a "Next release" box, so it can trail the newest release; the site is maintained, and that lag is not a reason to prefer the README.

**Superseded — the README.** HSSI held `https://github.com/SciQLop/SciQLop/blob/main/README.md` until this update. It was the best documentation while the project site was stale: read for the earlier refresh, the site was dated 2025-05-16, mirrored an older README, called collaborative catalog co-editing an upcoming feature, and did not cover the App Store, workspaces, the command palette or the DSP module. The site's restructuring into tutorials, a user guide and a reference resolved each of those objections: the DSP toolbox has its own guide, the App Store, workspaces and the command palette are covered, and no "upcoming" co-editing text remains. Rule 3 therefore makes the site the value; the README stays one click away through Field 3.

**Also noted (not field values):** no Read the Docs site exists for SciQLop, and the PyHC registry entry for SciQLop has no `docs` field. In-application documentation is substantial: tutorial notebooks under `SciQLop/examples/tutorials/`, browsable from the welcome page and installed into the user's workspace, and a guided tour on first use; `docs/` holds developer design documents including `docs/qt-lifetime-patterns.md` and `docs/workspaces-and-uv.md`.

### 25. Funder (OPTIONAL)
**Organization 1:**
- **Name:** CDPP (Centre de Données de la Physique des Plasmas)
- **Funder Identifier:** https://cdpp.irap.omp.eu/

**Organization 2:**
- **Name:** Federation of Plasma Physics laboratories at Sorbonne University
- **Funder Identifier:** https://ror.org/02rmk5x23

**Source:** Existing HSSI record for both organizations, supported by the README "Credits" section: "The development of SciQLop is supported by the CDPP. We acknowledge support from the federation Plas@Par."

**Both organizations are kept as stored, deliberately:**

- **Organization 2 is identified by the ROR `https://ror.org/02rmk5x23`.** That ROR record registers its website as `https://www.plasapar.sorbonne-universite.fr` — the same host as the bare project URL this record previously carried as the identifier — and that shared host is what establishes the two as one entity. The ROR is preferred because it is a stable, resolvable organization identifier that can be matched against any other record naming this federation, whereas a project URL can move or lapse. The earlier URL identifier is noted here as history, not as an alternative to re-adopt.
- **The name `Federation of Plasma Physics laboratories at Sorbonne University` is retained** in preference to the ROR record's own display name, `Fédération de recherche PLAS@PAR` (registered aliases `PLAS@PAR` and `Plasmas à Paris`). This is a settled naming choice, not a pending rename: the English name is what the README's credit line supports and what this catalogue uses, while the ROR identifier already carries the canonical French form for anyone who needs it.
- An organization's name or identifier cannot be changed through a software-record update (see the API-expressibility note under Field 6); corrections of that kind are made against the shared organization record itself.

**Considered and not changed:**
- CDPP has **no ROR record** (searched the ROR API for "Centre de Données de la Physique des Plasmas", "Centre de Donnees de Physique des Plasmas" and "CDPP plasma physics data centre"; no match — CDPP is a data centre operated within IRAP/CNES rather than a separately registered organization). Its URL identifier is retained.
- Field 25 says to avoid acronyms, which would argue for renaming organization 1 to plain "Centre de Données de la Physique des Plasmas". The live name already contains the full expansion in parentheses, and renaming a stored Organization is riskier than the cosmetic gain, so it is left alone. Recorded as an optional curation item.

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Source:** No award title or grant number appears in the README, CITATION.cff, `pyproject.toml`, the Zenodo record or the DataCite record (`fundingReferences` is empty). The README credits institutional support, not specific grants.

**Note:** `pnst` (Programme National Soleil-Terre) is a GitHub topic and a retained keyword, but no award title or number is associated with it anywhere in scope.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.23169249 — Jeandet, A., Aunai, N., Génot, V., Renard, B., Bouchemit, M., & André, N. (2026). *The SciQLop ecosystem: a layered open-source stack for in-situ heliophysics data* [Poster]. Data, Analysis, and Software in Heliophysics (DASH) 2026, Dublin. Zenodo.
- https://doi.org/10.5281/zenodo.23150226 — Jeandet, A., Aunai, N., Renard, B., Génot, V., Bouchemit, M., & André, N. (2026). *Ground-based and space-based radio spectra in SciQLop: interoperability obstacles from the client side* [Slides]. DASH 2026, Dublin. Zenodo.
- https://zenodo.org/records/23196188 — Jeandet, A., Hadid, L., Génot, V., Aunai, N., Renard, B., Bouchemit, M., & André, N. (2026). *Agentic LLM workflows inside SciQLop: data, literature, and the verification practices they require* [Slides]. DASH 2026, Dublin. Zenodo. DOI `10.5281/zenodo.23196188`, which did not resolve on 2026-10-29 (below).
- https://doi.org/10.1029/2025JE009617 — Wang, X., Hadid, L. Z., Aizawa, S., Sahraoui, F., Raines, J. M., & Lavraud, B. (2026). *Mercury’s Low‐Latitude Boundary Layer: Identification of Distinct Proton Populations Using MESSENGER Spacecraft Data.* Journal of Geophysical Research: Planets, 131(5), e2025JE009617.
- https://doi.org/10.1029/2025JA034657 — Hadid, L. Z., Chust, T., Wahlund, J.-E., et al. (2026). *Evidence of an Extended Alfvén Wing System at Enceladus: Cassini's Multi‐Instrument Observations.* Journal of Geophysical Research: Space Physics, 131(2), e2025JA034657.

**Settled on 2026-10-29.** HSSI held no value for this field before the earlier refresh filled it with five conference abstracts, and the 2025-10-09 file recorded "Not found". The five entries above replace those abstracts. The titles and authors above come from each publication's Crossref or DataCite record; the site shows only the URL, so the citations are recorded here.

**Removed — five meeting abstracts, which HSSI held until this update (rules 1 and 7; removal confirmed by the catalogue maintainer on 2026-10-29).** A conference or meeting abstract is never an eligible Field 27 publication, even when it describes the software. Each of these is a Copernicus meeting abstract, Crossref type `posted-content`; ADS indexes the four EGU records as `abstract` and the EPSC–DPS record as `inproceedings`. None of their meeting pages links a deposited poster or paper, and the 2022 page embeds a video of the presentation, a talk with no document of its own. Do not re-add them; if a poster or paper from one of these presentations is later deposited, it enters through that deposit. The five, by DOI:
- `10.5194/egusphere-egu22-5774` — Jeandet, A., Aunai, N., Génot, V., Schulz, A., Renard, B., Michotte de Welle, B., & Nguyen, G. (2022). *SciQLop: an open source project for in situ data analysis.* EGU General Assembly 2022. Copernicus GmbH.
- `10.5194/egusphere-egu23-13581` — Jeandet, A., Aunai, N., Génot, V., Boettcher, P., Renard, B., Michotte de Welle, B., André, N., Bouchemit, M., & Dufourg, N. (2023). *SciQLop: a tool suite to facilitate multi-mission data browsing and analysis.* EGU General Assembly 2023. Copernicus GmbH.
- `10.5194/egusphere-egu24-3515` — Jeandet, A., Aunai, N., Renard, B., Génot, V., Boettcher, P., Bouchemit, M., Michotte de Welle, B., Ghisalberti, A., & André, N. (2024). *SciQLop: a tool suite to facilitate multi-mission data browsing and analysis.* EGU General Assembly 2024. Copernicus GmbH.
- `10.5194/egusphere-egu25-10101` — Jeandet, A., Renard, B., Aunai, N., Ghisalberti, A., Génot, V., André, N., & Bouchemit, M. (2025). *SciQLop: A Tool Suite for Multi-Mission High-Resolution In-Situ Data Analysis in the Heliophysics Community.* EGU General Assembly 2025. Copernicus GmbH.
- `10.5194/epsc-dps2025-1422` — Jeandet, A., Renard, B., Aunai, N., Ghisalberti, A., Génot, V., André, N., & Bouchemit, M. (2025). *SciQLop & Speasy: Open-Source Tools for Unified Planetary and Heliospheric Data Analysis.* Europlanet Science Congress – Division for Planetary Sciences Joint Meeting 2025. Copernicus GmbH.

**Added — the developers' deposited poster (rule 3).** `10.5281/zenodo.23169249` is a Zenodo poster record (CC-BY-4.0) from DASH 2026 in Dublin, 5–7 October 2026, by SciQLop's own authors Jeandet, Aunai, Génot, Renard and André, with Bouchemit. Its one-page poster, with a two-page pitch, presents the SciQLop stack: the desktop application and the libraries and services beneath it (SciQLopPlots and NeoQCP, jupyqt, tscat and cocat, speasy-proxy, Speasy, AstraLint, pycdfpp, PyISTP and sciqlop-cache).

**Added — two DASH 2026 slide decks by the developers, judged standalone by the catalogue maintainer on 2026-10-29 (rule 3).** Field 27 admits a slide deck only when it reads as a substantial document a reader can follow without the talk.
- `10.5281/zenodo.23150226`, a 16-page deck of about 1,900 words: how SciQLop serves ground-based radio spectrographs (e-CALLISTO, I-LOFAR, RSTN) and seismic networks through plugins, and SuperMAG magnetometers through a proposed Speasy provider, beside the space archives, and the interoperability obstacles this exposed — missing presentation metadata, metadata carried only in filenames, split files — with full-sentence explanations and figures. Its first slide is headed "Ground-based and space-based data in SciQLop".
- `10.5281/zenodo.23196188`, an 18-page deck of about 2,400 words: lessons from embedding LLM agents in SciQLop — the agent layer and its tools, hard versus soft feedback, a fuzzing campaign on the user API, the product-search episode and science use cases — written in dense sentences that read without the talk. Its first slide is headed "Agents are only as good as their feedback". DataCite marks its DOI findable, but on 2026-10-29 doi.org answered 404 and the Handle system held no record for it, while the deposit's Zenodo landing page resolved; the entry is therefore that permanent landing page. When the DOI resolves, a later update should switch the entry to `https://doi.org/10.5281/zenodo.23196188`.

**Added — two papers whose results were built with SciQLop and that say so deliberately (rule 5).** SciQLop's citing literature is small, so each such use is still news.
- Wang et al. 2026 (JGR Planets): its Acknowledgments thank Alexis Jeandet for developing and maintaining SciQLop and credit it as the visualization and analysis tool that greatly facilitated the work. None of its six authors is a SciQLop author.
- Hadid et al. 2026 (JGR Space Physics): its Data Availability Statement credits SciQLop for the event selection, which was initially done with it, and gives the repository URL (read in the published article's open-access PDF deposited at HAL, `hal-05507022`; ADS's full-text index of the article carries the same repository URL). The paper has 29 authors and is led by L. Z. Hadid of the Laboratoire de Physique des Plasmas, the developers' laboratory, who also co-authored the agentic DASH 2026 deck above; two CITATION.cff authors are among them, Alexis Jeandet (15th) and Nicolas André (17th). It is listed as a third-party use under rule 5, a decision the catalogue maintainer made on 2026-10-29, because a non-developer led the study and the developers are 2 of its 29 authors; the reason rule 5 exists, a stated use of the software in one of the paper's results, holds, and no rule excludes the paper.

**Weighed and not added.**
- Michotte de Welle et al. 2026, Geophysical Research Letters (`10.1029/2025GL119118`), and Michotte de Welle et al. 2022, JGR Space Physics (`10.1029/2022JA030996`): the SciQLop name appears in them only within the address of the Speasy repository, a credit to Speasy (rule 6).
- Génot et al. 2021, Planetary and Space Science (`10.1016/j.pss.2021.105214`), on AMDA: names the SciQLop project in background text (rule 6).
- Koval et al., *ISTP Metadata Guidelines: Current Status and Future Development* (`10.5281/zenodo.23111203`), a presentation Jeandet co-authors: about the ISTP guidelines; it does not name SciQLop.
- Papers that credit Speasy rather than SciQLop belong to Speasy's record, and the Speasy software deposits that ADS lists beside SciQLop are software records (rule 1). The research group's Zenodo datasets are weighed under Field 28.

**Search record (2026-10-29).**
- ADS/SciX, with the anonymous token: `full:"SciQLop"` returned 16 records (the five abstracts, six Speasy software deposits and the five journal papers above); `title:"SciQLop" OR abs:"SciQLop"` returned 11 (the abstracts and the Speasy deposits); `ack:"SciQLop"` returned 1 (Wang et al. 2026). Controls: `full:"qwxzvplk"` returned 0, and `full:"Speasy"` returned 29 and `ack:"Speasy"` 5.
- Zenodo: the creator-keyed search `metadata.creators.person_or_org.name:"Jeandet, Alexis"`, excluding software, returned 6 records (the poster, the two decks, the ISTP presentation and two datasets), and a text search for SciQLop excluding software returned the poster and the two decks; a nonsense creator name returned 0.
- DataCite reports no citations of the concept DOI `10.5281/zenodo.7379012`.
- Semantic Scholar holds no record of the SciQLop software DOIs; ADS full text covers the literature.
- The next update should search from 2026-10-29.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Source:** Empty on HSSI; unchanged. SciQLop is dataset-agnostic — it browses tens of thousands of products from whatever Speasy's inventory exposes and depends on no particular dataset. No dataset DOI is referenced in the repository, CITATION.cff, Zenodo or DataCite metadata.

**Weighed at the v0.14.1 update:** the developers' Zenodo datasets *Automatic detection of the Earth's magnetopause boundary layer from multiple mission data* (`10.5281/zenodo.20312678`) and *MANGO Dataset : Magnetosphere Atlas from Normalized Geospace Observations* (`10.5281/zenodo.19671706`) are science products of the same research group; neither record names SciQLop, so neither is this software's dataset.

### 29. Related Software (OPTIONAL)
**Values:**
- https://github.com/SciQLop/speasy — **Speasy** (the stored Code Repository of Speasy's own HSSI entry, copied byte for byte; Speasy's concept DOI was passed over, below)
- https://github.com/SciQLop/SciQLopPlots — **SciQLopPlots**
- https://github.com/SciQLop/tscat — **tscat**
- https://github.com/SciQLop/tscat_gui — **tscat_gui**
- https://github.com/SciQLop/cocat — **cocat**

**Source:** Speasy is the existing HSSI relation — **retained**; the earlier refresh added the four domain-specific companion packages, each a declared dependency and each documented in the README "SciQLop Ecosystem" table.

**Speasy's URL form (Field 29 rules 11 and 13).** HSSI held the Speasy relation as its concept DOI, `https://doi.org/10.5281/zenodo.4118780` (DataCite: title "Speasy", publisher Zenodo, `IsSupplementTo https://github.com/SciQLop/speasy`), until this update. Speasy has its own HSSI entry, whose stored Code Repository is `https://github.com/SciQLop/speasy`, and an in-catalogue target takes that exact string: the site shows a related item's raw URL as its link text, and a repository URL is legible where a DOI is not. The concept DOI stays on file here so the choice can be reversed if HSSI ever renders resolved titles for related items.

**Per-value evidence:**
- **Speasy** — `pyproject.toml` `speasy[blosc]>=1.8.5` in the `all` extra at `v0.14.1` (`speasy>=1.6.1` at v0.12.0); the entire data layer (`SciQLop/plugins/speasy_provider/`) is a Speasy client. Speasy's own README points back: "Don't want to write code? See our graphical interface SciQLop."
- **SciQLopPlots** — `pyproject.toml` `SciQLopPlots==0.47.1` in the `all` extra at `v0.14.1` (0.24.0 at v0.12.0); provides every plot widget SciQLop wraps (`SciQLopNDProjectionPlot`, `SciQLopHistogram2D`, `SciQLopColorMapBase`) and the DSP kernels behind `SciQLop.user_api.dsp` (`from SciQLopPlots import dsp`). Purpose-built for this application by the same organization.
- **tscat** — heliophysics time-series event/catalog library; the default local catalog store (`SciQLop/plugins/tscat_catalogs/tscat_provider.py`, `orphans.py`), declared as a runtime plugin dependency in `SciQLop/plugins/tscat_catalogs/plugin.json` and in the dev extra, as `tscat>=0.5.1` in both at `v0.14.1`.
- **tscat_gui** — Qt catalog editor reached from SciQLop's catalog browser ("Open in TSCat editor…"); `tscat_gui>=0.7.0`.
- **cocat** — CRDT collaborative-catalog library; `SciQLop/plugins/collaborative_catalogs/` (`client.py`, `cocat_provider.py`, `room.py`) is a cocat client, declaring `cocat>=0.7.0`.

**Considered and excluded — generic infrastructure (Tier A):** numpy, scipy, matplotlib, seaborn, PySide6, shiboken6, PySide6-QtAds, qasync, jinja2, pydantic, keyring, uv, tomli_w, pyyaml, psutil, humanize, platformdirs, pyzstd, PyGitHub, expression, cloudpickle, defusedxml, pypdf, qtconsole, ipywidgets, jupyterlab_widgets, model2vec, huggingface_hub. Each would read identically for an arbitrary Python package. Also generic, weighed at the v0.14.1 update: packaging, ipympl, agent-client-protocol, mcp and uvicorn, and jupyqt — the SciQLop organisation's library for embedding JupyterLab in PySide6 applications, which would serve any Qt application equally.

**Also excluded (with reason):**
- **QCustomPlot** — listed by the 2025-10-09 file. It is a general-purpose Qt plotting library (equally at home in a finance dashboard), acknowledged in the README "Thanks" section but not a SciQLop dependency; `NeoQCP` is the fork actually used, and that sits under SciQLopPlots.
- **PySide6, NumPy, Jupyter** — listed by the 2025-10-09 file as Field 29 dependencies. PySide6 and NumPy are Tier A. Jupyter is a genuine peer-tool integration and has been moved to Field 30, where it belongs.
- **Ecosystem siblings not listed as values because they are not this package's dependencies** (all documented in the README ecosystem table): **NeoQCP** (`https://github.com/SciQLop/NeoQCP`, the QCustomPlot-fork rendering engine used by SciQLopPlots — also generic plotting infrastructure), **CDFpp / PyCDFpp** (`https://github.com/SciQLop/CDFpp`, the fast C++ CDF reader behind Speasy and itself a PyHC package — a transitive dependency only), **SciQLop-cache** (`https://github.com/SciQLop/SciQLop-cache`), **speasy_proxy** (`https://github.com/SciQLop/speasy_proxy`; not a dependency — since v0.13.0 SciQLop exchanges plot configurations with it, which is recorded under Field 30, and the link alone does not also make it a Field 29 value, Field 30 rule 9).
- **PySPEDAS** — the 2025-10-09 file cited `SciQLop/examples/PySPEDAS/pyspedas.ipynb`. That example **no longer exists**: it was deleted upstream on 2026-04-11 ("chore: remove broken PySPEDAS example"). No reference to PySPEDAS or SPEDAS remains in the repository at `e964ab02` or at `v0.12.0`; at `v0.14.1` the name appears only in test fixtures — a product path in `tests/remote/test_registry.py:17` and a missing-dependency message in `tests/test_magics/test_workspace_magic.py:146–149` — with no exchange in the package. PySPEDAS reaches SciQLop users through the separately distributed App Store plugin `sciqlop-pyspedas` ("MMS Particle Spectra (pyspedas)", by Alexis Jeandet, from the `SciQLop/sciqlop-plugins` repository, marked experimental), which belongs to that plugin rather than to this package. Removed from both Fields 29 and 30 on that evidence; the exclusion stands.

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://github.com/SciQLop/speasy — **Speasy**
- https://github.com/SciQLop/tscat — **tscat**
- https://github.com/SciQLop/tscat_gui — **tscat_gui**
- https://github.com/SciQLop/cocat — **cocat**
- https://github.com/jupyterlab/jupyterlab — **JupyterLab / Jupyter**
- https://github.com/SciQLop/speasy_proxy — **speasy_proxy**

**Source:** Speasy is the existing HSSI relation — **retained**, its URL now in the in-catalogue form explained under Field 29 (HSSI held it as the concept DOI `https://doi.org/10.5281/zenodo.4118780` until this update). The earlier refresh added four entries and this update adds speasy_proxy, each with a specific demonstrated exchange rather than mere dependency presence.

**Per-value evidence (the specific exchange; the first five confirmed at `v0.12.0` and still present at `v0.14.1`, speasy_proxy read at `v0.14.1`):**
- **Speasy** — three independent, bidirectional exchanges. (1) SciQLop registers itself as a **Speasy plot backend**: `_register_plot_backend()` in `SciQLop/plugins/speasy_provider/speasy_provider.py` installs `SciQLopBackend` (`SciQLop/user_api/plot/_speasy_backend.py`, with `line()` and `colormap()` entry points) into `speasy.plotting`, so `speasy.plot()` from any notebook can render into SciQLop panels when SciQLop is selected as the backend — `tests/test_speasy_plot_backend.py:9` asserts the default remains `matplotlib`, so this is an available, selectable backend rather than an automatic redirection. (2) The DSP API is defined on Speasy's data model: every `SciQLop.user_api.dsp` function accepts a `speasy.products.SpeasyVariable` and returns a new one with metadata preserved (`SciQLop/user_api/dsp/_speasy.py` `rewrap_time_series`, `rewrap_spectrogram`, `slice_segments`). (3) The catalog API converts both ways: `catalogs.get(path)` returns a `speasy.products.catalog.Catalog` and `catalogs.save(path, data)` accepts one (`SciQLop/user_api/catalogs/_service.py`).
- **tscat** — SciQLop reads and writes tscat catalogs, events, attributes and attribute schemas through its provider (`SciQLop/plugins/tscat_catalogs/tscat_provider.py`, `orphans.py`), including a driver-thread query path for `tscat.get_events()` / `tscat.get_catalogues()`; catalogs created in SciQLop are ordinary tscat catalogs usable by other tscat clients.
- **tscat_gui** — SciQLop hands a live catalog off to the standalone TSCatGUI editor ("Open in TSCat editor…" on the *My Catalogs* row, routed through `CatalogProvider.actions()`); both surfaces operate on the same tscat store.
- **cocat** — the `collaborative_catalogs` plugin joins a cocat room and exchanges CRDT catalog state over WebSocket, so several SciQLop instances co-edit one catalog conflict-free; includes cocat-specific operations such as the `MOVE_CATALOG` attribute mutation and CRDT `set_attributes` write-through. Tests `tests/test_cocat_event_meta.py` and `tests/test_cocat_move_catalog.py`. (The plugin ships `"disabled": true` by default at v0.12.0, so the integration is opt-in — see Field 8.)
- **JupyterLab / Jupyter** — Tier B, admitted on cited evidence rather than dependency presence. SciQLop embeds a full IPython kernel and launches a JupyterLab server bound to it: `SciQLop/components/jupyter/kernel/manager.py:7` at `v0.14.1` (line 1 at `v0.12.0`) is `from jupyqt import EmbeddedJupyter`, and at `v0.12.0` `SciQLop/components/workspaces/backend/workspace_project.py:33,35,148,151` provisioned `jupyqt` and `jupyterlab` into each workspace venv. Since v0.12.2 the venv receives JupyterLab's front end as `jupyterlab-js`, through `jupyqt` → `jupyverse`, and leaves the `jupyterlab` package out deliberately because both ship the same data files (`workspace_project.py:312–316` at `v0.14.1`); the embedded JupyterLab panel itself is unchanged. The exchange is genuinely two-way: notebook cells create and drive SciQLop panels through `SciQLop.user_api`, and SciQLop ships IPython magics (`%plot`, `%%vp`, `%%layer`, `%timerange`, `%install`) plus "Copy Python code" reproducer snippets generated *for* notebooks (`SciQLop/core/snippets/templates/notebook_matplotlib.j2`). README: "analyze your data in Jupyter notebooks side by side with interactive plots".
- **speasy_proxy** — SciQLop converts a plot panel to the Speasy proxy's interactive plot-page configuration and back. `SciQLop/components/plotting/ui/proxy_share.py` (first in v0.13.0) builds a proxy `/plot?config=…` URL from a panel (`proxy_plot_url`, schema v1 of the proxy's plot page, offered from the panel's menu in `SciQLop/components/plotting/ui/time_sync_panel.py`), and `proxy_plot_config_from_text` with `apply_proxy_config` rebuilds a panel from such a URL pasted into the product search overlay; `tests/test_proxy_share.py` covers it. Only Speasy-backed products cross over. speasy_proxy is the SciQLop organisation's caching proxy server for shared Speasy data access; it has no HSSI entry, so its upstream repository root is recorded (Field 29 rule 12), and its concept DOI `10.5281/zenodo.22180324` was passed over for the legible repository URL (Field 29 rule 13).

**Considered and excluded:** every Tier A package listed under Field 29; **matplotlib**, **seaborn** and **scipy** (used internally for colormaps, styling and filter design — no documented exchange of a shared data model, and each would read the same for most packages); **SciQLopPlots** and **NeoQCP** (SciQLop is *built on* them, which is a dependency relationship rather than interoperation between peer tools — SciQLopPlots is recorded in Field 29); **PySPEDAS** (see Field 29 — its example was deleted upstream, and the App Store plugin that brings it is separately distributed); **the AI-assistant backends** (Claude Code, GitHub Copilot, OpenCode, Albert), which arrive as separately installed App Store plugins, and the Agent Client Protocol and MCP that the agent layer speaks — generic AI tooling that would be equally at home in a web app (rule 2).

**Note on HSSI display names:** the live record's RelatedItem entries render as placeholder names (`UNKNOWN` / raw URL). Those placeholders are never user-visible and were disregarded when deciding these values; the DOI or URL is the identity.

### 31. Related Instruments (OPTIONAL)
**Value:** Not found — deliberately empty. No instrument is recorded.

**Change vs the 2025-10-09 canonical file (removal, documented):** that file listed *MMS*, *THEMIS* and *ACE* with the note "instrument identifiers (DOIs) not available". All three are removed. Live HSSI has no `relatedInstruments` at all, so nothing published is being dropped.

**Reason — SciQLop is instrument-agnostic.** It is a general multi-mission browser: `build_product_tree` / `explore_nodes` walk Speasy's *entire* inventory and build the Products tree generically, and `get_components` / `data_serie_type` branch on the **provider** (`amda`, `ssc`, `UiowaEphTool`) and on generic ISTP attributes — never on a mission or instrument.

**What the mission and instrument name mentions actually are, scoped to `v0.12.0`:** a repository-wide search at the tag, excluding `SciQLop/examples/`, returns only — the product-search placeholder text `"Search products (e.g. MMS FGM, ACE MAG B_gsm)…"` (`SciQLop/components/plotting/ui/product_search_overlay.py:67`); agent tool help strings using `amda.Parameters.MMS.MMS1` and `speasy//amda//Parameters//MMS//MMS1` as illustrative inventory paths (`SciQLop/components/agents/tools/_builder.py:184,207`); a workspace-manifest **format docstring** whose example installed-example entry is `name = "MMS"` (`SciQLop/components/workspaces/backend/workspace_manifest.py:18`); and product-path fixtures scattered through `docs/plans/*.md` and `tests/`. There is no instrument-specific parser, calibration, format or code path anywhere at the tag.

Two mentions cited in the previous revision of this file do **not** exist at `v0.12.0` and have been withdrawn: the code comment about MMS's Search Coil Magnetometer arrived after the tag, and the onboarding-tour target pointing at `ACE / MFI / b_gse` is part of the onboarding component, every commit of which post-dates the tag. Their removal strengthens rather than weakens the conclusion — the surviving mentions are even more clearly placeholders, help text, docstrings, design notes and test fixtures.

**Re-swept at `v0.14.1` — unchanged.** The mission and instrument names in the code at the tag, bundled examples excluded, are of the same kinds: the onboarding tour's example product (`SciQLop/components/onboarding/backend/targets.py:9`, ACE MFI `b_gse`) and its prompt text, the product-search placeholder, agent help strings and guidance snippets using MMS product paths, a job-record example name, the workspace-manifest docstring, and the provider's Cluster Science Archive icon. The two mentions withdrawn above as post-v0.12.0 — the MMS Search Coil comment, now `SciQLop/plugins/speasy_provider/speasy_provider.py:297`, and the onboarding ACE target — are present at `v0.14.1` and are of those kinds. The README at `v0.14.1` names MMS, THEMIS/ARTEMIS, Cluster, Solar Orbiter, Parker Solar Probe, Wind and ACE as examples of missions whose data the archives serve; that describes the archives' reach, not mission-specific support.

The 2025-10-09 entries rested entirely on example notebooks and README usage snippets — exactly the demo/name-drop case the relevance gate excludes. Listing three instruments while omitting the hundreds of others equally supported would be arbitrary and would mislead anyone searching HSSI by instrument.

**SPASE resolution work performed anyway, so a future include decision starts from verified rows.** Every candidate below, resolved against the controlled vocabulary, is multi-row **ambiguous**, so even under an "include" decision none could be emitted as a clean value — each would have to be marked `NEEDS MANUAL RESOLUTION`:
- **MMS FGM** — 330 rows match `FGM` / `Fluxgate Magnetometer` (type 1), across dozens of missions. Not resolvable from the acronym.
- **MMS FPI / DIS / DES** — 30 rows match `FPI` / `Fast Plasma`; the MMS-relevant ones alone are four identically-named CDPP-AMDA rows "Fast Plasma Investigation" (`CNES/Instrument/CDPP-AMDA/MMS1..4/FPI`) plus CDPP-Archive rows split per-probe *and* per-sensor ("MMS 1 Fast Plasma Instrument", abbreviations `DIS` and `DES`). Ambiguous.
- **THEMIS ESA** — 16 rows under the rule "type 1 and name or identifier matching a `THEMIS/<probe>/ESA` path or the phrase *Electrostatic Analyzer*"; a broader rule that also accepts the bare abbreviation `ESA` anywhere returns 28, and 10 of those 16 sit on a THEMIS identifier path. Under the narrow rule the THEMIS-relevant matches are five identically-named CDPP-AMDA rows "Dual Full Distribution Electrostatic Analyzers" (`CNES/Instrument/CDPP-AMDA/THEMIS/A..E/ESA`, plus two ARTEMIS probes) alongside SMWG per-probe rows such as `SMWG/Instrument/THEMIS/A/ESA` ("THEMIS-A Electrostatic Analyzers"). Ambiguous under any of the three rules.
- **ACE MFI** — the only two rows matching `MFI` are both **Wind**, not ACE (`SMWG/Instrument/Wind/MFI` and `CNES/Instrument/CDPP-AMDA/Wind/MFI`). ACE's magnetometer is not reachable under the acronym used in the repository, which is itself a caution against acronym-driven matching.

### 32. Related Observatories (OPTIONAL)
**Value:** Not found — deliberately empty. No observatory is recorded.

**Change vs the 2025-10-09 canonical file (removal, documented):** that file listed *MMS*, *THEMIS* and *ACE* with no identifiers. All three are removed, for the same agnosticism reason given under Field 31. Live HSSI has no `relatedObservatories`, so nothing published is being dropped.

**SPASE resolution work performed — every candidate examined, every fallback considered.** Resolved against the same vocabulary, restricted to `type = 2`. No candidate family contains `.html` identifier twins, so no `.html` normalization was needed:
- **MMS — 16 candidate rows.** `SMWG/Observatory/MMS` ("Magnetospheric Multiscale"), `SMWG/Observatory/MMS/1..4` ("MMS-1".."MMS-4"), `CNES/Observatory/CDPP-AMDA/MMS` ("Magnetospheric Multiscale Mission"), `CDPP-AMDA/MMS1..3` ("… Mission #1..#3"), `CDPP-AMDA/MMS4` (name "MMS4"), `CDPP-AMDA/MMS1234` ("… Mission : 4 s/c"), and `CDPP-Archive/MMS` plus `CDPP-Archive/MMS-1..4`. The mission-level `SMWG/Observatory/MMS` was verified resolvable, but it is not the single unambiguous match the vocabulary requires: the **bare name "MMS" belongs to a different row** (`CNES/Observatory/CDPP-Archive/MMS`), so a name-only write would bind to the wrong resource.
- **THEMIS — 61 candidate rows,** under the rule "type 2 and `THEMIS` matched case-insensitively in the row `name` or anywhere in the SPASE identifier path". Those 61 rows carry **61 distinct SPASE identifiers** and contain no `.html` twins, so the vocabulary is unambiguous about how many resources exist. What it is *not* unambiguous about is naming: there are only **55 distinct names**, and three name-collision families account for the gap — five probe rows all named "MIDEX/THEMIS" (`CNES/Observatory/CDPP-AMDA/THEMIS/ThemisA..E`); `SMWG/Observatory/AUTUMN` and `SMWG/Observatory/Ground/AUTUMN`, both named "Athabasca University THEMIS UCLA Magnetometer Network"; and `SMWG/Observatory/Ground/GMAG` and `SMWG/Observatory/THEMIS/Ground`, both named "THEMIS-Associated Ground Magnetometer Stations". 42 of the 61 rows are ground stations or networks (`SMWG/Observatory/THEMIS/Ground/...`, UCLA-EPO / GBO / CANMAG). The spacecraft family is `SMWG/Observatory/THEMIS` ("Time History of Events and Macroscale Interactions during Substorms", verified resolvable) with per-probe children `THEMIS/A..E`. Note that case-insensitive matching is required: `CNES/Observatory/CDPP-AMDA/Themis` uses a mixed-case path segment and spells the mission out in its name rather than using the acronym, so a case-sensitive identifier test silently drops it. It is the **name collisions**, not the row count, that make a bare-name write dangerous here.
- **ACE — 2 candidate rows.** `SMWG/Observatory/ACE` ("Advanced Composition Explorer", verified resolvable) and `CNES/Observatory/CDPP-AMDA/ACE` ("Advanced Composition Explorer, NASA"). Two candidates, so still ambiguous under the resolution ladder.
- **Cluster — 15 candidate rows** (`SMWG/Observatory/Cluster`, `Cluster-Rumba/Salsa/Samba/Tango`, CDPP-AMDA `Cluster1..4`, CDPP-Archive `Cluster` / `Cluster-1..4`). Considered because Speasy's Cluster Science Archive (`csa`) provider node is surfaced in SciQLop's Products tree — but that is generic archive plumbing, not Cluster-specific support, so Cluster fails the relevance gate as well as being ambiguous.
- **Observatory-level fallback considered and rejected.** Where an instrument cannot be resolved, the ladder allows falling back to its SPASE observatory/platform record. That fallback is not used here because the *observatories themselves* fail the relevance gate — SciQLop is not designed to support MMS, THEMIS, ACE or Cluster specifically. Falling back would launder a relevance failure into a resolution success.

**Nothing was omitted merely for being hard to resolve.** Every candidate was resolved as far as the vocabulary allows and then rejected on relevance; the ambiguity findings above are recorded so a future include decision starts from verified data rather than from scratch. Should MMS ever be added — it has the strongest case, since SciQLop ships a dedicated installable MMS example workspace (`SciQLop/examples/mms/` with `example.json`, `index.ipynb`, `DemoMMS_tags-up_meeting.ipynb` and `MMS_dayside_magnetopause.ipynb`, all present at `v0.12.0`), the project's demo screencast is `SciQLop_MMS.gif`, and the README's primary API examples use MMS products — it would have to be hand-bound to one of the 16 rows, most plausibly `Magnetospheric Multiscale` / `https://spase-metadata.org/SMWG/Observatory/MMS`.

### 33. Logo (OPTIONAL)
**Value:** https://raw.githubusercontent.com/SciQLop/SciQLop/f9a0484a61b63def3814309d5af53d839229b16a/SciQLop/resources/icons/SciQLop.png

**Source:** Existing HSSI record. Re-verified on 2026-10-29: the URL serves `image/png`; the file at that path is the same git blob at `v0.14.1` and at `main` head; the README renders it as the project banner; and the PyHC community registry entry for SciQLop designates the same asset as its `logo`.

**Same asset as the original submission, recorded as a commit-pinned raw URL.** The submitted value referenced the `main` branch, which breaks silently on any upstream rename, move or deletion; the URL above pins the commit and serves byte-identical image data. The registry's own `logo` string is still the branch form — it is authoritative about *which* asset is the logo, not about the URL used to reach it.
