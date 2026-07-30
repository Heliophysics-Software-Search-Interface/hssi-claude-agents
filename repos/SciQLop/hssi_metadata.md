# HSSI Metadata Extraction Results

**HSSI Software ID:** 1b5fd49d-9131-46ee-b56a-70efbb1effe5
**Repository:** https://github.com/SciQLop/SciQLop
**Source Revision:** e964ab02b7df13977f4d0e1a7291327a872b0b0a (committed 2026-07-26T23:49:27+02:00, branch `main`)
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-07-29
**Validation Status:** PASS

**Seeds used:** live HSSI record for `1b5fd49d-9131-46ee-b56a-70efbb1effe5` (authoritative for current published state) and the previous canonical `hssi_metadata.md` dated 2025-10-09. Live HSSI wins scalar conflicts; still-supported file-only additions are retained; every replacement is explained inline with its evidence.

**Release scope note (applies to Fields 4, 12, 13, 17–19, 29, 30):** the latest authoritative release is **v0.12.0** (2026-05-17). Capability fields are derived from the code as it exists **at tag `v0.12.0`**, not from unreleased `main` (`pyproject.toml` at HEAD is `0.13.0.dev0`). Every source path cited below as v0.12.0 evidence was confirmed present at that tag. Post-v0.12.0 `main`-only capabilities that were deliberately **excluded** are listed under Field 4 so they can be picked up at the next release.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Note:** Not part of the stored record; supplied at submission/update time.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.7379012

**Source:** Existing HSSI record; re-confirmed against DataCite for `10.5281/zenodo.7379012`, which is the Zenodo **concept** DOI (all versions) and now reports `version: v0.12.0` and `IsSupplementTo https://github.com/SciQLop/SciQLop/tree/v0.12.0`.

**Unchanged from live HSSI.**

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/SciQLop/SciQLop

**Source:** Existing HSSI record; matches the git remote of the local checkout, `pyproject.toml` `[project.urls] homepage`, the Zenodo v0.12.0 record's `code:codeRepository`, and CITATION.cff `url`.

**Unchanged from live HSSI.**

### 4. Software Functionality (MANDATORY)
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
- Data Visualization: Line Plots
- Data Visualization: Orbit Plots
- Data Visualization: Spectrogram

**Change vs live HSSI:** live has 9 values; **3 added** — `Data Processing and Analysis: Data Reduction`, `Data Processing and Analysis: Processing`, `Data Processing and Analysis: Spectrogram`. Nothing removed. The additions are all driven by the `SciQLop.user_api.dsp` signal-processing facade, which **first shipped in v0.12.0** (first commit 2026-04-18; the earliest tag containing it is `v0.12.0`) and therefore did not exist when the record was originally created.

**Change vs the 2025-10-09 canonical file:** that file listed `Data Visualization:Interactive`, which is **not in the controlled vocabulary** — removed. It also listed `Data Visualization:Web-Based`, removed as unsupported (see exclusions below).

**Per-value evidence (every path confirmed present at tag `v0.12.0`):**
- **Data Processing and Analysis: Data Access and Retrieval** — `SciQLop/plugins/speasy_provider/speasy_provider.py` builds the Products tree from the whole `speasy.inventories.tree` (nodes explicitly recognized in `build_product_tree`: `amda`, `ssc`, `cda`/`cdaweb`, `csa`, `archive`, `uiowaephtool`) and fetches through `spz.get_data` on scroll/zoom; the `%plot` magic and the product search overlay let users retrieve any product by fuzzy name.
- **Data Processing and Analysis: Time Series Analysis** — the application's core object is the multivariate time-series panel; `dsp.split_segments` performs gap detection/segmentation, `dsp.rolling_mean` / `dsp.rolling_std` gap-aware rolling statistics, `dsp.resample` uniform-grid resampling. Tutorial `SciQLop/examples/tutorials/SciQLop/14-SciQLopDSP.ipynb` §3 builds a live mean±std envelope.
- **Data Processing and Analysis: Spectrogram** — `dsp.spectrogram(data, col=, window_size=, overlap=, window=)` computes per-segment STFT and returns 2-D `(N_time, N_freq)` `SpeasyVariable`s; `dsp.fft` returns per-segment `(freqs, magnitude)`. Tutorial 14 §4 "Live spectrogram with tunable FFT parameters". Kernels come from `SciQLopPlots.dsp` via `SciQLop/user_api/dsp/_arrays.py`; tests `tests/test_dsp_arrays.py`, `tests/test_dsp_speasy.py`.
- **Data Processing and Analysis: Processing** — filter chain `dsp.filtfilt`, `dsp.sosfiltfilt`, `dsp.fir_filter`, `dsp.iir_sos`, plus `dsp.interpolate_nan`; virtual products recompute on pan/zoom, making these live processing pipelines (tutorial 14 §1 wraps a SciPy Butterworth design in a `%%vp` cell with a cutoff knob).
- **Data Processing and Analysis: Data Reduction** — `dsp.reduce(data, op)` (sum/mean/norm over columns), `dsp.reduce_axes(data, shape, axes, op=)` (arbitrary-axis reduction inside multi-component rows), `dsp.resample`, rolling statistics; `Histogram2D` / `panel.histogram2d(x, y)` bins scatter data into an `x_bins × y_bins` grid.
- **Data Processing and Analysis: Analysis** — virtual products compute derived physical quantities from retrieved data (README example: |B| from `bx, by, bz`), and the annotation-layer system lets a user callable analyse a graph's data and return `Marker` / `Span` / `HLine` results (`SciQLop/user_api/layers/`, seven modules present at the tag). The catalog system supports event labelling for statistical multi-mission studies.
- **Data Visualization: Line Plots** — `TimeSeriesPlot.plot()` / `XYPlot.plot()` line and scatter graphs, multi-component vectors, and a secondary `y2` axis (`SciQLop/user_api/plot/_plots.py:24,210,233,249`); test `tests/test_plot_scatter_hline.py`.
- **Data Visualization: Spectrogram** — `ColorMap` rendering of spectrogram-type products; `data_serie_type()` auto-detects `ParameterType.Spectrogram` from the ISTP `DISPLAY_TYPE` attribute; log color scales via `PlotHints`. README panel example plots `mms1_dis_energyspectr_omni_brst`.
- **Data Visualization: 2D Graphics** — colormap rasters, `Histogram2D` density grids, `XYPlot`, graphic primitives (`Pixmap`, `Ellipse`, `Text`, `CurvedLine`, `HorizontalLine`) and in-canvas `Overlay`, and catalog events rendered as color-coded vertical spans (continuous or categorical matplotlib colormaps).
- **Data Visualization: Orbit Plots** — *live HSSI value, retained.* Supporting evidence: SSCWeb and `UiowaEphTool` ephemeris products are surfaced as `['x','y','z']` position components (`get_components`, `data_serie_type` in `speasy_provider.py`) with a runtime coordinate-frame selector, and `ProjectionPlot` (`SciQLopNDProjectionPlot`) renders them as parametric curves — i.e. trajectory/orbit projections.
- **Data Processing and Analysis** / **Data Visualization** — required parents, both present.

**Recorded decision — `Coordinate Transforms` (and `Coordinate Transforms: Magnetospheric`) excluded.** v0.12.0 does expose a user-facing coordinate-frame control: `SpeasyPlugin.get_knobs` synthesizes a `ChoiceKnob("coordinate_system")` for SSC products, and the release notes advertise switching frames without re-issuing the plot. But the transform itself is performed **server-side by SSCWeb** — SciQLop only forwards `coordinate_system` into `spz.get_data` — so there is **zero transform mathematics in the package** at v0.12.0. Excluded as a pass-through, not a capability. **Revisit trigger:** `SciQLop/components/agents/tools/orbits.py` (first committed 2026-07-02, absent at v0.12.0) fetches ephemerides and 3×3 frame-transform matrices from the CDPP 3DView REST API, so `Coordinate Transforms` and `Coordinate Transforms: Mission-Specific` must be re-decided at v0.13.0.

**Other values considered and excluded (audit trail):**
- **Data Visualization: Web-Based** — the 2025-10-09 file claimed it. `SciQLop/core/web_channel_page.py` (QWebEngineView + QWebChannel + Jinja2) backs only the welcome page and the plugin App Store — application chrome, not data visualization. All science plots are native Qt widgets. No plotly/bokeh/dash surface exists.
- **Data Visualization: 3D Graphics** — `SciQLopNDProjectionPlot` projects N-dimensional data onto a 2-D parametric curve; there is no 3-D renderer.
- **Data Visualization: Movies** — no animation or video export anywhere in the package.
- **Data Visualization: Hodograms** — `XYPlot` can plot one field component against another, but no hodogram feature is provided or documented.
- **Data Processing and Analysis: Energy Spectra**, **: 3D Particle Distribution Processing**, **: Plasma Moments**, **: Pitch Angle Distributions** — SciQLop displays energy-flux spectrograms and can reduce arbitrary axes of multi-component products, but implements no energy-spectrum, distribution-function, moment or pitch-angle computation.
- **Mission-related** (any subcategory) — SciQLop is not part of any mission ground segment or pipeline.
- **Servers and Environments** (any subcategory) — SciQLop manages a per-workspace `uv` virtual environment and launches an embedded JupyterLab server, but these are internal runtime mechanics of a desktop application, not infrastructure software offered to others.
- **Data Processing and Analysis: ML/AI** — `machine-learning` is a longstanding GitHub topic and the catalog system is explicitly useful for building labelled training sets, but v0.12.0 implements no ML. (The v0.12.0 Agent Chat is an LLM *assistant* over the app, not machine learning applied to the science data. Unreleased `main` adds `model2vec`/`huggingface_hub` embedding-based product search — revisit at the next release.)

**Format note:** the payload form is `"Parent: Child"` **with a space after the colon** — this is what the API stores and returns, and it is what the live record shows. The `hssi-field-definitions` form documentation writes the same values without the space; both forms parse identically because the API normalizes whitespace around the colon, so the with-space form above is canonical for payloads (`.claude/skills/submission-payload/SKILL.md:200,287`). Note also that the combined string is never itself a vocabulary row: `/api/models/FunctionCategory/rows/all/` holds 83 **bare** parent and child names (`Data Visualization`, `2D Graphics`, `Analysis`, …), and the API resolves `Parent: Child` by walking the parent → child graph. Each parent must therefore also be listed as its own entry, as it is above.

### 5. Related Region (MANDATORY)
**Values:**
- Earth Magnetosphere
- Interplanetary Space
- Planetary Magnetospheres

**Source:** Existing HSSI record — all three retained, and all three confirmed present in `/api/models/Region/rows/all/`.

**Change vs the 2025-10-09 canonical file:** that file had only two values; `Planetary Magnetospheres` is a live-HSSI value the file was missing, and it is well supported — the AMDA/CDPP inventories SciQLop surfaces cover planetary missions, and the developers' own EPSC-DPS 2025 abstract is titled "SciQLop & Speasy: Open-Source Tools for Unified Planetary and Heliospheric Data Analysis" (Field 27).

**Considered and not added:** `Solar Environment` (in the vocabulary, but SciQLop targets *in-situ* plasma measurements and has no solar imaging or remote-sensing functionality) and `Earth Atmosphere` (no atmospheric or ionospheric functionality).

### 6. Authors (MANDATORY)
Union of live HSSI, the 2025-10-09 canonical file, CITATION.cff at `v0.12.0`, and the Zenodo/DataCite v0.12.0 record. **No author is dropped.** Matched by ORCID first, then normalized name.

**Author 1:**
- **Name:** Alexis Jeandet
- **Author Identifier:** https://orcid.org/0000-0003-2892-6924
- **Affiliation:** Laboratory of Plasma Physics (LPP/CNRS)
- **Affiliation Identifier:** https://ror.org/05c95bg36

**Author 2:**
- **Name:** Nicolas Aunai
- **Author Identifier:** https://orcid.org/0000-0002-9862-4318
- **Affiliation:** CNRS / Laboratory of Plasma Physics
- **Affiliation Identifier:** Not found

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
- **Nicolas Aunai's affiliation is carried at the live stored value** — `CNRS / Laboratory of Plasma Physics`, no identifier — which his ORCID employment record ("Laboratoire de Physique des Plasmas / CNRS") and the shared byline of the 2025 abstracts ("CNRS, Laboratory Of Plasma Physics, Palaiseau CEDEX, France") both support as a correct, if non-canonical, label.
- **Deferred correction (Aunai's affiliation).** The canonical target is `Laboratory of Plasma Physics (LPP/CNRS)` / `https://ror.org/05c95bg36`, the ROR-backed row already used for Jeandet. The correction is **deferred to direct curation of the shared organization records** rather than recorded as a value here, because the update API can add an affiliation but cannot replace or remove one — writing the canonical row would leave Aunai attached to both. The underlying cause is that the shared organization vocabulary holds four rows for this one laboratory: the ROR-backed `Laboratory of Plasma Physics (LPP/CNRS)` plus three identifier-less variants (`CNRS / Laboratory of Plasma Physics`, `Laboratoire de Physique des Plasmas`, `Laboratoire de Physique des Plasmas, Ecole Polytechnique`). Consolidating those four is the real fix and is out of scope for this record.
- **Nicolas André — two affiliations, both resolved to RORs.** No affiliation appears in any repository or DOI metadata, and live HSSI stores none, so both come from his ORCID record's two concurrent current employments. The first is recorded as **Institut de Recherche en Astrophysique et Planétologie** (ROR `https://ror.org/05hm2ja81`): the ORCID entry for that post names the organization "Conseil National de la Recherche Scientifique" but gives `department: Institut de Recherche en Astrophysique et Planétologie`, `city: Toulouse`, `country: FR`, `role: Staff Scientist`, from 2009-01-01 with no end date — and IRAP (ROR `05hm2ja81`, UMR 5277) lists `Centre National de la Recherche Scientifique` (ROR `https://ror.org/02feahw73`) among its parents, so "CNRS, department IRAP" *is* IRAP. It is recorded under IRAP rather than under CNRS for a second reason: ORCID disambiguates that employment with Funder Registry ID `10.13039/501100007175`, which resolves to **`Conseil` National de la Recherche Scientifique, located in Lebanon** (CNRS-L) — not the French `Centre` National de la Recherche Scientifique (`10.13039/501100004794`, ROR `https://ror.org/02feahw73`). CNRS-L's registry aliases include the bare "CNRS", which is how it wins ORCID's typeahead; the mismatch is treated as an upstream ORCID data-entry error rather than propagated. The second affiliation is **Institut Supérieur de l'Aéronautique et de l'Espace** (ROR `https://ror.org/04gyj6s21`, from 2024-03), disambiguated by ROR in ORCID itself. Both are corroborated for IRAP by the 2025 abstract bylines cited under Génot below.
- **Vincent Génot — affiliation now recorded, on abstract evidence alone.** His ORCID record is **completely empty**: zero entries across employments, educations, memberships and services, so ORCID contributes nothing. No affiliation appears in CITATION.cff, `pyproject.toml`, DataCite or Zenodo either. The sole source is the two 2025 conference abstracts he co-authored (Field 27), whose printed affiliation 3 — *"Institut de Recherche en Astrophysique et Planétologie, CNRS, CNES, UPS, Toulouse, France"* — is attached to both Génot and André on **both** `EPSC-DPS2025-1422` and `EGU25-10101`. That is self-declared and consistent across two independent venues, but it is weaker evidence than André's, which ORCID corroborates; it is recorded as such. The affiliation resolves to the ROR-backed row already stored in HSSI for Renard, so no new organization is created.

  Calibration on byline evidence, recorded deliberately: those same two abstracts print **Renard** at affiliation 2, *"Akkodis, Toulouse, France"*, whereas both live HSSI and Renard's own ORCID record place him at IRAP — so a printed byline and a registry can diverge, and Renard's affiliation is accordingly left on its registry-backed value rather than changed to match the abstracts. The divergence does not undercut affiliation 3 for Génot: the string itself is independently corroborated as accurate by ORCID's department field and ROR's parent chain (via André), and for Génot there is no competing registry claim to diverge from — his ORCID is empty rather than contradictory.
- **Not added as authors:** the developer-authored conference abstracts (Field 27) carry additional co-authors — Alexandre Schulz, Gautier Nguyen, Patrick Boettcher, Bayane Michotte de Welle, Myriam Bouchemit, Nicolas Dufourg, Ambre Ghisalberti. CITATION.cff is the project's own authoritative statement of *software* authorship and lists five people; abstract co-authorship is not software authorship. Recorded here for the audit trail only.

**API-expressibility note (metadata note, not a value):** *adding* an affiliation is safe and idempotent when the payload's identifier matches an organization row that already exists — which is why the three additions recorded here are expressible as written: Génot's IRAP and André's IRAP both resolve by ROR `https://ror.org/05hm2ja81` to the row already used for Renard, and André's ISAE-SUPAERO creates one new, correctly named, ROR-backed row (the shared organization vocabulary has no ISAE-SUPAERO entry, checked across several spellings). *Replacing or removing* an affiliation is **not** expressible — the update path only ever adds — which is why the Aunai correction above is deferred to direct curation instead of being written here.

### 7. Software Name (MANDATORY)
**Value:** SciQLop

**Source:** Existing HSSI record; matches CITATION.cff `title`, `pyproject.toml` `name`, the Zenodo v0.12.0 record title, and the repository name.

**Unchanged from live HSSI.** Expansion (for reference, not the field value): SCIentific Qt application for Learning from Observations of Plasmas.

### 8. Description (MANDATORY)
**Value:**
SciQLop (SCIentific Qt application for Learning from Observations of Plasmas) is a powerful and user-friendly tool designed for the visualization and analysis of in-situ space plasma data. Using SciQLop, users can access tens of thousands of products from major data archives worldwide, explore multivariate time series effortlessly with lightning-fast and transparent downloads, visualize custom products with simple Python code executed on-the-fly, easily label time intervals and make or edit catalogs of events graphically, and analyze data in Jupyter notebooks. SciQLop aims to be the right tool for exploring, labeling, and analyzing huge amounts of space physics data, and is also ideal for teaching space physics and in situ spacecraft data handling to students. More recent releases add opt-in real-time collaborative catalog editing, a signal-processing toolbox that operates directly on retrieved variables, per-project workspaces with isolated Python environments, and community plugins installable from a built-in App Store.

**Source:** the live HSSI description (identical to the 2025-10-09 file) **preserved byte-verbatim**, with one sentence appended. The original text ends at "...handling to students."; everything before that point is unmodified.

**Reason for the appended sentence:** the published description had become materially incomplete for a user deciding whether the software is useful. Every clause is supported by primary evidence at `v0.12.0`:
- *opt-in real-time collaborative catalog editing* — `SciQLop/plugins/collaborative_catalogs/` (`client.py`, `cocat_provider.py`, `room.py`), cocat CRDT over WebSocket, README section "Collaborative Catalog Editing", tests `tests/test_cocat_event_meta.py` and `tests/test_cocat_move_catalog.py`. Described as **opt-in** because `SciQLop/plugins/collaborative_catalogs/plugin.json` ships `"disabled": true` at v0.12.0: the feature is implemented, documented and tested, but off by default.
- *signal-processing toolbox* — `SciQLop.user_api.dsp`, 13 functions with `SpeasyVariable` round-trip semantics, tutorial 14.
- *per-project workspaces with isolated Python environments* — `SciQLop/components/workspaces/`, `.sciqlop` TOML manifests, per-workspace `uv` venv, `docs/workspaces-and-uv.md`.
- *community plugins from a built-in App Store* — `SciQLop/components/appstore/`, live registry at `https://github.com/SciQLop/sciqlop-appstore`, hot-loaded plugins.

### 9. Concise Description (OPTIONAL)
**Value:** An ergonomic and efficient application to browse and label in situ plasma measurements from multi-mission satellite data.

**Source:** Existing HSSI record; still byte-identical to `pyproject.toml` `description` at both HEAD and `v0.12.0`, and to the GitHub repository description.

**Unchanged from live HSSI.**

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
**Version Number:** v0.12.0

**Version Date:** 2026-05-17

**Version Description:**
v0.12.0 is a large feature release. Catalogs: per-event metadata is now editable directly in the catalog browser (type-aware editors, multi-row bulk edit, searchable and persisted column visibility, "+ Attribute"), events can be dragged between catalogs (link by default, Shift to move, Ctrl to duplicate), catalogs can be dragged within the browser or onto a plot panel to become an overlay, tscat orphan events are surfaced as a virtual row with a cleanup dialog, and a typed `CatalogProvider.attribute_spec` API lets providers publish per-attribute schemas. New parameterized data products ("knobs"): virtual-product callbacks and Speasy templated parameters expose runtime-tunable arguments (`IntKnob`, `FloatKnob`, `BoolKnob`, `ChoiceKnob`, `StringKnob`, plus widget-bound `TimeRangeKnob`, `ThresholdKnob`, `DatetimeKnob`) edited from an Inspector "Parameters" section. New annotation-layer system: a registered callable returns `Marker` / `Span` / `HLine` annotations drawn on a plot, via the `@register_layer` decorator, the `%%layer` cell magic, `panel.layer(...)`, or drag-and-drop from the product tree. New plot API: a `Histogram2D` plottable with `panel.histogram2d(...)`, an `Overlay` wrapper for in-canvas text, and a `dsp` facade wrapping 13 signal-processing primitives (`filtfilt`, `sosfiltfilt`, `fir_filter`, `iir_sos`, `interpolate_nan`, `rolling_mean`, `rolling_std`, `resample`, `fft`, `spectrogram`, `reduce`, `reduce_axes`, `split_segments`) with `SpeasyVariable` round-trip semantics. Every graph now carries a `GraphContext` envelope enabling "Copy Python code" reproducer snippets, hover tooltips and Inspector context rows; snippet generation moved to Jinja2 templates using a `//`-joined product-path convention. Speasy integration: SSC products publish a runtime coordinate-system choice — the release notes summarize it as GSE/GSM/SM/GEI/GEO/MAG, while the code-verified choice list is GSE, GSM, SM, GEO, GM, GEI_TOD and GEI_J_2000 (`SciQLop/plugins/speasy_provider/speasy_provider.py:356–358`), i.e. no `MAG` entry and an additional `GM` — and each Speasy config section is surfaced in SciQLop's Settings UI so it drives Speasy's runtime configuration directly. Also: a runtime tracer with Chrome/Perfetto capture under Tools › Profiling, version-aware App Store filtering, provider-driven aggregated `PlotHints` with ISTP fallbacks, a faster-painting startup splash, a per-panel crosshair toggle, palette-aware styling arguments on the graphic primitives, and a rewritten bundled tutorial suite. Fixes include offline startup no longer aborting when the workspace dependency sync cannot reach the network, two SIGSEGV plot/panel teardown crash classes (Qt lifetime rules now documented in `docs/qt-lifetime-patterns.md`), macOS window geometry and toolbar-icon sizing, Python 3.14 lazy-annotation introspection, and Windows packaging (paths containing spaces, HiDPI manifest, `SCIQLOP_DIST_DIR`). Dependencies moved to PySide6/shiboken6 6.11.0, PySide6-QtAds 4.5.0.3 and SciQLopPlots 0.24.0.

**Version PID:** https://doi.org/10.5281/zenodo.20261873

**Change vs live HSSI:** live stores `v0.10.0`; **updated to `v0.12.0`.** Evidence — v0.12.0 is the newest non-draft, non-prerelease GitHub release (published 2026-05-17T20:54:17Z), the newest git tag by creation date, and the PyPI `sciqlop` latest release (0.12.0, uploaded 2026-05-17). Eleven releases shipped after v0.10.0: v0.10.1–v0.10.5, v0.11.0–v0.11.4, v0.12.0. The version-specific DOI `10.5281/zenodo.20261873` was resolved from the Zenodo REST API by following the concept record `7379012` to its latest version, whose `metadata.version` is `v0.12.0`, `publication_date` is `2026-05-17`, and whose only related identifier is `IsSupplementTo https://github.com/SciQLop/SciQLop/tree/v0.12.0`. The description is condensed from the repository `CHANGELOG.md` `## v0.12.0 — 2026-05-17` section (the GitHub release body is the same text).

**Storage warning:** write the **bare** version number `v0.12.0`. The live view API renders the stored value as `SciQLop - v0.10.0`; that `<software> - <number>` prefix is a rendering transform and must never be written back.

**Note:** CITATION.cff was **not** updated for v0.12.0 — at tag `v0.12.0` it still declares `version: 0.10.0` and `doi: 10.5281/zenodo.17176824`. Zenodo/DataCite and the git tags are authoritative here; CITATION.cff is stale upstream. (For the record, `10.5281/zenodo.17176824` is the v0.10.0 version DOI, which the 2025-10-09 file correctly captured at the time.)

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x
- Javascript

**Source:** `Python 3.x` is the existing HSSI value, confirmed by `pyproject.toml` (`requires-python = ">=3.11,<3.15"`, Python 3.10–3.14 classifiers) and GitHub language statistics dominated by Python (2.62 MB) and Jupyter notebooks (3.16 MB, i.e. the bundled tutorials and examples).

**Added (1) — `Javascript`.** The package carries real JavaScript in two files — `SciQLop/components/welcome/resources/welcome.js` and `SciQLop/components/appstore/resources/appstore.js` — which drive the QWebChannel welcome page and App Store surfaces (`SciQLop/core/web_channel_page.py`). GitHub reports **60,823 bytes** of JavaScript, but that is a measurement of the **default branch**; at tag `v0.12.0` the two files total **48,071 bytes** (`welcome.js` 36,848 + `appstore.js` 11,223). Both files are present at the tag, so the value holds under either measurement. It is UI chrome rather than science code, but Field 13 asks for the languages the software is *implemented* in, not only those of its science core, so it belongs. Both values are exact rows in `/api/models/ProgrammingLanguage/rows/all/` (19 rows), and the vocabulary's spelling is `Javascript` — capital J, lowercase s, no camel-case — which is the spelling used above.

**Change vs the 2025-10-09 canonical file:** that file added `C++` and `Jupyter Notebook`.
- `Jupyter Notebook` is **not in the controlled vocabulary** — removed.
- `C++` was inferred from a CITATION.cff *keyword*, not from any code. GitHub reports **zero C++ bytes** in this repository; the only C file is `scripts/windows/launcher.c`. The Qt/C++ engine lives in the separate `SciQLopPlots` / `NeoQCP` / `CDFpp` repositories (Field 29). Removed.

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

**Source:** No reference publication is designated anywhere authoritative — CITATION.cff has no `preferred-citation`, the README has no "cite this paper" instruction, and neither the Zenodo nor the DataCite record carries an `IsDescribedBy` relation. The DOI in CITATION.cff points at the software deposit itself, not a paper.

**Note:** five developer-authored conference abstracts describing SciQLop **do** exist and are recorded under Field 27 (Related Publications), which is their correct home. None is declared by the project as the preferred citation, so Field 14 is deliberately left empty rather than promoting one.

### 15. License (RECOMMENDED)
**License:** GNU General Public License v3.0 or later

**License URI:** https://www.gnu.org/licenses/gpl-3.0-standalone.html

**SPDX Identifier:** GPL-3.0-or-later

**Source:** the license *name* is the existing HSSI value and is an exact row in `/api/models/License/rows/all/`. It is corroborated by four independent sources that now all agree: CITATION.cff (`license: "GPL-3.0-or-later"`), the `COPYING` file (GPL version 3), the Zenodo v0.12.0 record (`license.id = gpl-3.0-or-later`), and DataCite for the concept DOI, which returns `rights: "GNU General Public License v3.0 or later"`, `rightsIdentifier: gpl-3.0+` and `rightsUri: https://www.gnu.org/licenses/gpl-3.0-standalone.html` — matching the License URI recorded here exactly. `pyproject.toml` points at `COPYING` and carries the GPLv3 OSI classifier.

**Change vs live HSSI:** **none — the name is unchanged and no write was made.** The License URI and SPDX identifier recorded above are *not* patchable software fields: the API's `license` field is the license **name** only, and there is no software-level URI or SPDX key. Both are attributes of the shared `License` vocabulary row, which already exists and already carries `https://spdx.org/licenses/GPL-3.0-or-later.html`. Editing that row would change the URI for every GPL-3.0-or-later package in HSSI, so no action is taken. The URI and SPDX identifier are retained here as durable provenance, not as pending changes.

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
- general
- gui
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

**Sources:** union of live HSSI (7: amda, cdpp, machine learning, nasa data, plasma physics, pnst, satellite — **all retained**), the 2025-10-09 canonical file (its 26 file-only additions retained), CITATION.cff `keywords` at `v0.12.0`, GitHub repository topics (`amda, cdpp, machine-learning, nasa-data, plasma-physics, pnst, satellite`), and the PyHC community registry entry for SciQLop (`heliosphere, magnetosphere, plasma_physics, interactive, line_plots, plotting, general, cdaweb, sscweb, web_service, remote, data_access, data_analysis`).

**Normalization applied (documented, not a drop):** underscore and hyphen variants are folded to the space-separated form so near-duplicates are not created — `plasma_physics`/`plasma-physics` → `plasma physics` (matching the live stored value), `line_plots` → `line plots`, `web_service` → `web service`, `data_access` → `data access`, `data_analysis`/`data analysis` → `data analysis`, `machine-learning` → `machine learning` (live), `nasa-data` → `nasa data` (live).

**Added from v0.12.0 evidence (3):** `catalogs` (the catalog browser, providers, overlays and `catalogs.*` user API are a headline feature), `jupyter` (embedded IPython kernel, JupyterLab server, `%plot`/`%%vp`/`%timerange`/`%install` magics), `signal processing` (the new `SciQLop.user_api.dsp` module).

**Notes:** `c++` is retained because it is an upstream-declared CITATION.cff keyword, but it refers to the C++ engine that lives in the **separate** SciQLopPlots / NeoQCP / CDFpp repositories, not to code in this repository — GitHub reports zero C++ bytes here and the only C file is `scripts/windows/launcher.c`. That is also why `C++` is *not* a Field 13 value. `general` comes from the PyHC taxonomy and carries little information; it is retained only because it is a supported file-only addition and is safe to drop.

### 17. Data Sources (OPTIONAL)
**Values:**
- AMDA
- CDAWeb
- HTTP/HTTPS Directories
- Other
- SSCWeb

**Source:** `AMDA`, `CDAWeb`, `SSCWeb` and `Other` are existing HSSI values — retained. All five values above are exact rows in `/api/models/DataInput/rows/all/`, re-verified against live after the vocabulary reconciliation that deleted the malformed row `Other - https://xrt.cfa.harvard.edu/level1/`. `SciQLop/plugins/speasy_provider/speasy_provider.py` builds the Products tree from Speasy's full inventory and explicitly recognizes the `amda`, `cda`/`cdaweb`, `ssc`, `csa`, `archive` and `uiowaephtool` provider nodes.

**Removed (1) — `Observatory/Mission-specific`, a live published value.** No observatory-specific code path exists anywhere at v0.12.0: `build_product_tree` branches on **provider**, and `get_components` / `data_serie_type` branch on generic ISTP attributes — never on a mission or observatory. The value's own rule requires naming the observatory in Field 32, and Field 32 is empty for exactly the same architectural reason (see Fields 31/32). `AMDA` + `CDAWeb` + `SSCWeb` + `HTTP/HTTPS Directories` + `Other` describes SciQLop's data-source coverage accurately without it.

**Added (1) — `HTTP/HTTPS Directories`.** SciQLop surfaces Speasy's generic `archive` provider node in its Products tree (`build_product_tree` maps an `"archive"` icon for it, and the agent tool help text enumerates providers as "amda, cda, ssc, archive, …" at `SciQLop/components/agents/tools/_builder.py:184`), and Speasy's README states it can "Support data access from any local or remote archives described by YAML file." The evidence reaches SciQLop through Speasy, which is exactly how *every* SciQLop data source works — including the already-published AMDA, CDAWeb and SSCWeb — so this value is supported on the same footing as those.

**Considered and not added:** `FTP/FTPS Directories` (no citation found), `HAPI` (mentioned only hypothetically in an `istp_hints.py` docstring — no HAPI client is used), `OMNIWeb`, `das2`, `TAP`, `The Virtual Solar Observatory.`, `VirES`, `S3/Cloud-aware`, `Madrigal`, `GFZ`, `WDC` (no evidence). The Cluster Science Archive (`csa`) is reachable through Speasy's inventory but, like every other archive, via the generic provider mechanism.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- ascii
- CDF
- csv
- ISTP-Compliant

**Source:** `ascii`, `CDF` and `csv` are existing HSSI values — retained (SciQLop reads science data through Speasy, whose PyHC entry lists `cdf, csv, ascii`). All four values are exact rows in `/api/models/FileFormat/rows/all/`.

**Added (1) — `ISTP-Compliant`.** Direct in-repo evidence at `v0.12.0`: `SciQLop/core/istp_hints.py` ("ISTP metadata → PlotHints translation ... any provider whose upstream metadata follows the ISTP/CDF convention") reads **nine ISTP attributes** directly out of the variable's metadata mapping to configure axis labels, units, scales, valid ranges, fill values and spectrogram detection — `LABL_PTR_1` (:67), `LABLAXIS` (:75, :97), `FIELDNAM` (:102), `VALIDMIN` (:106), `VALIDMAX` (:107), `DISPLAY_TYPE` (:123), `UNITS` (:126), `SCALETYP` (:127) and `FILLVAL` (:130). A tenth, `DEPEND_1`, is handled indirectly: the caller may attach the DEPEND_1 variable's own ISTP attributes as a `_depend_1` sub-mapping (documented at :116, read at :142), whose `UNITS`, `SCALETYP` and valid range are then used to populate the secondary axis hints for spectrogram plots (:146–148). `data_serie_type()` in the Speasy provider keys spectrogram-vs-scalar-vs-vector classification off the same convention; covered by `tests/test_istp_hints.py`.

**Considered and not added:** `JSON` — the app reads `.ipynb` notebooks and JSON plugin descriptors, and `YAML`/`TOML` for panel templates, settings and `.sciqlop` workspace manifests, but these are application configuration rather than scientific data input.

### 19. Output File Formats (RECOMMENDED)
**Value:** Other

**Source:** New — this field is **empty** on HSSI, and the 2025-10-09 file recorded "Not found". SciQLop does export, but only to formats outside the controlled list, so `Other` is the correct single value. Evidence at `v0.12.0`: `PlotPanel.save(path)` (`SciQLop/user_api/plot/_panel.py:400`) exports a panel as an image, dispatching on extension across `.png`, `.pdf`, `.jpg`, `.jpeg` and `.bmp`; `PlotPanel.save_template()` (`_panel.py:426`) writes panel layouts as YAML templates.

**`JSON` deliberately not selected.** Panel templates, settings and `.sciqlop` workspace manifests are application configuration, not scientific data — the same rule Field 18 already applies to JSON on the input side. Applying it consistently here leaves `Other` alone.

**Note:** no export to ascii, CDF, csv, FITS, HDF5, IDL.sav, netCDF3/4 or Zarr exists, so no listed format may be claimed.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

**Source:** Existing HSSI record. Re-confirmed against `.github/workflows/SingleExe.yml`, which builds release artifacts on `ubuntu-latest` (AppImage), `macos-14` (Apple Silicon bundle), `macos-15-intel` (Intel bundle) and `windows-latest` (Inno Setup installer); `.github/workflows/tests.yml` runs the test matrix across operating systems; the README documents a Windows installer, macOS app bundles for both architectures, and a Linux AppImage (plus a Flatpak manifest for Flathub).

**Unchanged from live HSSI.**

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- Apple Silicon arm64
- CPU Independent
- x86-64

**Source:** Existing HSSI record — all three retained. macOS bundles are built for both Apple Silicon (`macos-14`) and Intel x86-64 (`macos-15-intel`); the README instructs users to "pick the right architecture for your Mac (ARM64 for Apple M1/2/3/4 chips and x86_64 for Intel)"; the from-source Python install is architecture independent.

**Unchanged from live HSSI.** (The 2025-10-09 file wrote `CPU Independent (Python-based)`; the controlled value is the bare `CPU Independent`, which is what live HSSI stores.)

**Considered and not added:** `Linux aarch64 or arm64` — the Linux AppImage is produced only on `ubuntu-latest` (x86-64); no aarch64 Linux artifact is published.

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found — deliberately empty. No phenomenon is recorded.

**Change vs the 2025-10-09 canonical file (removal, documented):** that file listed `Magnetic fields`, `Electric fields` and `Particle distributions`, carried over from CITATION.cff keywords. All three are removed for two independent reasons. First, they are **not in the controlled vocabulary**: `/api/models/Phenomena/rows/all/` has exactly seven rows — Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission — so writing them would have minted three custom entries. Second, they are measured *quantities*, not phenomena. Live HSSI has no `relatedPhenomena`, so nothing published is being dropped; the net effect against HSSI is a no-op.

**`Solar Wind` and `Geomagnetic Storms` considered and not added.** Both are in the vocabulary and both are studied with SciQLop, but the same architectural agnosticism that empties Fields 31/32 applies here: SciQLop implements no phenomenon-specific analysis, detection or model, and selecting two phenomena from the many its users study would be as arbitrary as naming three of the hundreds of missions it can browse.

**Note:** the three removed terms remain correctly carried in **Field 16 Keywords** (`magnetic fields`, `electric fields`, `particle distributions`), which is a free-text field and their proper home.

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** New — this field is **empty** on HSSI. `Active` is an exact row in `/api/models/RepoStatus/rows/all/`. Evidence: HEAD commit dated 2026-07-26 (three days before extraction); eleven releases published since v0.10.0, the most recent being v0.12.0 on 2026-05-17; `pyproject.toml` already bumped to `0.13.0.dev0` with a populated `## v0.13.0` CHANGELOG section; the repository is neither archived nor disabled and runs CI on every push. This matches repostatus.org **Active** ("reached a stable, usable state and is being actively developed").

**Note:** `pyproject.toml` still carries the `Development Status :: 4 - Beta` trove classifier, and PyHC rates documentation, testing and software maturity as "Requires improvement". Neither contradicts repostatus **Active**, which is about development activity rather than maturity.

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/SciQLop/SciQLop/blob/main/README.md

**Source:** Existing HSSI record, retained. The README is the project's most complete and most current documentation: it covers what the software is, the ecosystem, every major feature, per-platform installation instructions, and Python user-API examples.

**Unchanged from live HSSI.** (The 2025-10-09 file used the bare repository URL; the live value is more precise.)

**Alternative recorded for the user:** the repository's declared GitHub homepage is **https://sciqlop.github.io/** — a real, reachable project site with its own installation instructions. It is *not* adopted here because it is stale: the page is dated 2025-05-16 and mirrors an older README. It mentions collaborative catalogs only as an **upcoming** feature ("Upcoming features … catalogs coediting: SciQLop *will* allow users to coedit catalogs"), when that capability has since shipped, and it does not cover the App Store, workspaces, the command palette or the DSP module at all. If the user prefers a non-repository documentation URL, this is the candidate.

**Also noted (not field values):** no Read the Docs site exists for SciQLop, and the PyHC registry entry for SciQLop has no `docs` field. In-application documentation is substantial: 12 SciQLop tutorial notebooks plus 3 Speasy tutorials under `SciQLop/examples/tutorials/`, browsable from the welcome page and installed into the user's workspace; `docs/` holds developer design documents including `docs/qt-lifetime-patterns.md` and `docs/workspaces-and-uv.md`.

### 25. Funder (OPTIONAL)
**Organization 1:**
- **Name:** CDPP (Centre de Données de la Physique des Plasmas)
- **Funder Identifier:** https://cdpp.irap.omp.eu/

**Organization 2:**
- **Name:** Federation of Plasma Physics laboratories at Sorbonne University
- **Funder Identifier:** https://www.plasapar.sorbonne-universite.fr/en

**Source:** Existing HSSI record for both organizations, supported by the README "Credits" section: "The development of SciQLop is supported by the CDPP. We acknowledge support from the federation Plas@Par."

**Change vs live HSSI — none. The value above is the live stored state, deliberately.**

- **Deferred correction (organization 2 identifier).** The correct identifier for this funder is the ROR `https://ror.org/02rmk5x23`: that record lists its website as `https://www.plasapar.sorbonne-universite.fr` — the same host as the stored URL, confirming the same entity. The upgrade is **deferred to direct curation of the shared organization records** and is deliberately *not* recorded as the value here, because the update API cannot express it. `_get_or_create_org` matches on `identifier` first; no organization row carries that ROR, so a payload containing it would `create()` a **second** Plas@Par row rather than upgrading the first. Because `funder` is a full-replacement M2M and SciQLop is the only software referencing the existing row, attempting it would link the new duplicate and leave the original fully orphaned. An organization's non-blank identifier cannot be rewritten through the software update path at all. This is the same limitation that defers Aunai's affiliation in Field 6.
- The **live stored name is kept**; the ROR record's own display name, `Fédération de recherche PLAS@PAR`, is recorded as the alternative if canonical naming is preferred during that curation.

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
- https://doi.org/10.5194/egusphere-egu22-5774 — Jeandet, A., Aunai, N., Génot, V., Schulz, A., Renard, B., Michotte de Welle, B., & Nguyen, G. (2022). *SciQLop: an open source project for in situ data analysis.* EGU General Assembly 2022. Copernicus GmbH.
- https://doi.org/10.5194/egusphere-egu23-13581 — Jeandet, A., Aunai, N., Génot, V., Boettcher, P., Renard, B., Michotte de Welle, B., André, N., Bouchemit, M., & Dufourg, N. (2023). *SciQLop: a tool suite to facilitate multi-mission data browsing and analysis.* EGU General Assembly 2023. Copernicus GmbH.
- https://doi.org/10.5194/egusphere-egu24-3515 — Jeandet, A., Aunai, N., Renard, B., Génot, V., Boettcher, P., Bouchemit, M., Michotte de Welle, B., Ghisalberti, A., & André, N. (2024). *SciQLop: a tool suite to facilitate multi-mission data browsing and analysis.* EGU General Assembly 2024. Copernicus GmbH.
- https://doi.org/10.5194/egusphere-egu25-10101 — Jeandet, A., Renard, B., Aunai, N., Ghisalberti, A., Génot, V., André, N., & Bouchemit, M. (2025). *SciQLop: A Tool Suite for Multi-Mission High-Resolution In-Situ Data Analysis in the Heliophysics Community.* EGU General Assembly 2025. Copernicus GmbH.
- https://doi.org/10.5194/epsc-dps2025-1422 — Jeandet, A., Renard, B., Aunai, N., Ghisalberti, A., Génot, V., André, N., & Bouchemit, M. (2025). *SciQLop & Speasy: Open-Source Tools for Unified Planetary and Heliospheric Data Analysis.* Europlanet Science Congress – Division for Planetary Sciences Joint Meeting 2025. Copernicus GmbH.

**Source:** New — this field is **empty** on HSSI, and the 2025-10-09 file recorded "Not found". All five are author-authored abstracts that *describe* SciQLop, i.e. exactly what Field 27 asks for. Each DOI was verified against the Crossref API — the titles, author lists and dates above are taken from those records — and each resolves. A Crossref title search for "SciQLop" returns exactly these five works, so the list is complete as of this extraction.

**Note:** these are Crossref (Copernicus GmbH) DOIs rather than DataCite DOIs, so HSSI's DataCite lookup widget may not autofill them; an APA-style citation is therefore included alongside each DOI, as Field 27 permits. The EPSC-DPS 2025 abstract is the same work cited as primary evidence for `Planetary Magnetospheres` under Field 5.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Source:** Empty on HSSI; unchanged. SciQLop is dataset-agnostic — it browses tens of thousands of products from whatever Speasy's inventory exposes and depends on no particular dataset. No dataset DOI is referenced in the repository, CITATION.cff, Zenodo or DataCite metadata.

### 29. Related Software (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.4118780 — **Speasy** (concept DOI verified against DataCite: title "Speasy", publisher Zenodo, `IsSupplementTo https://github.com/SciQLop/speasy`)
- https://github.com/SciQLop/SciQLopPlots — **SciQLopPlots**
- https://github.com/SciQLop/tscat — **tscat**
- https://github.com/SciQLop/tscat_gui — **tscat_gui**
- https://github.com/SciQLop/cocat — **cocat**

**Source:** the Speasy DOI is the existing HSSI value — **retained**. Four domain-specific companion packages are added, each a declared dependency and each documented in the README "SciQLop Ecosystem" table.

**Per-value evidence:**
- **Speasy** — `pyproject.toml` `speasy>=1.6.1`; the entire data layer (`SciQLop/plugins/speasy_provider/`) is a Speasy client. Speasy's own README points back: "Don't want to write code? See our graphical interface SciQLop."
- **SciQLopPlots** — `pyproject.toml` `SciQLopPlots==0.32.0` (0.24.0 at v0.12.0); provides every plot widget SciQLop wraps (`SciQLopNDProjectionPlot`, `SciQLopHistogram2D`, `SciQLopColorMapBase`) and the DSP kernels behind `SciQLop.user_api.dsp` (`from SciQLopPlots import dsp`). Purpose-built for this application by the same organization.
- **tscat** — heliophysics time-series event/catalog library; the default local catalog store (`SciQLop/plugins/tscat_catalogs/tscat_provider.py`, `orphans.py`), declared as a runtime plugin dependency in `SciQLop/plugins/tscat_catalogs/plugin.json` and as `tscat>=0.4.0` in the dev extra.
- **tscat_gui** — Qt catalog editor reached from SciQLop's catalog browser ("Open in TSCat editor…"); `tscat_gui>=0.7.0`.
- **cocat** — CRDT collaborative-catalog library; `SciQLop/plugins/collaborative_catalogs/` (`client.py`, `cocat_provider.py`, `room.py`) is a cocat client, declaring `cocat>=0.7.0`.

**Considered and excluded — generic infrastructure (Tier A):** numpy, scipy, matplotlib, seaborn, PySide6, shiboken6, PySide6-QtAds, qasync, jinja2, pydantic, keyring, uv, tomli_w, pyyaml, psutil, humanize, platformdirs, pyzstd, PyGitHub, expression, cloudpickle, defusedxml, pypdf, qtconsole, ipywidgets, jupyterlab_widgets, model2vec, huggingface_hub. Each would read identically for an arbitrary Python package.

**Also excluded (with reason):**
- **QCustomPlot** — listed by the 2025-10-09 file. It is a general-purpose Qt plotting library (equally at home in a finance dashboard), acknowledged in the README "Thanks" section but not a SciQLop dependency; `NeoQCP` is the fork actually used, and that sits under SciQLopPlots.
- **PySide6, NumPy, Jupyter** — listed by the 2025-10-09 file as Field 29 dependencies. PySide6 and NumPy are Tier A. Jupyter is a genuine peer-tool integration and has been moved to Field 30, where it belongs.
- **Ecosystem siblings not listed as values because they are not this package's dependencies** (all documented in the README ecosystem table, all available for the user to promote): **NeoQCP** (`https://github.com/SciQLop/NeoQCP`, the QCustomPlot-fork rendering engine used by SciQLopPlots — also generic plotting infrastructure), **CDFpp / PyCDFpp** (`https://github.com/SciQLop/CDFpp`, the fast C++ CDF reader behind Speasy and itself a PyHC package — a transitive dependency only), **SciQLop-cache** (`https://github.com/SciQLop/SciQLop-cache`), **speasy_proxy** (`https://github.com/SciQLop/speasy_proxy`, configured through Speasy's settings rather than SciQLop's).
- **PySPEDAS** — the 2025-10-09 file cited `SciQLop/examples/PySPEDAS/pyspedas.ipynb`. That example **no longer exists**: it was deleted upstream on 2026-04-11 ("chore: remove broken PySPEDAS example"), and no reference to PySPEDAS or SPEDAS remains anywhere in the repository at HEAD or at `v0.12.0`. Removed from both Fields 29 and 30 on that evidence.

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.4118780 — **Speasy**
- https://github.com/SciQLop/tscat — **tscat**
- https://github.com/SciQLop/tscat_gui — **tscat_gui**
- https://github.com/SciQLop/cocat — **cocat**
- https://github.com/jupyterlab/jupyterlab — **JupyterLab / Jupyter**

**Source:** the Speasy DOI is the existing HSSI value — **retained**. Four entries added, each with a specific demonstrated exchange rather than mere dependency presence.

**Per-value evidence (the specific exchange, all confirmed at `v0.12.0`):**
- **Speasy** — three independent, bidirectional exchanges. (1) SciQLop registers itself as a **Speasy plot backend**: `_register_plot_backend()` in `SciQLop/plugins/speasy_provider/speasy_provider.py` installs `SciQLopBackend` (`SciQLop/user_api/plot/_speasy_backend.py`, with `line()` and `colormap()` entry points) into `speasy.plotting`, so `speasy.plot()` from any notebook can render into SciQLop panels when SciQLop is selected as the backend — `tests/test_speasy_plot_backend.py:9` asserts the default remains `matplotlib`, so this is an available, selectable backend rather than an automatic redirection. (2) The DSP API is defined on Speasy's data model: every `SciQLop.user_api.dsp` function accepts a `speasy.products.SpeasyVariable` and returns a new one with metadata preserved (`SciQLop/user_api/dsp/_speasy.py` `rewrap_time_series`, `rewrap_spectrogram`, `slice_segments`). (3) The catalog API converts both ways: `catalogs.get(path)` returns a `speasy.products.catalog.Catalog` and `catalogs.save(path, data)` accepts one (`SciQLop/user_api/catalogs/_service.py`).
- **tscat** — SciQLop reads and writes tscat catalogs, events, attributes and attribute schemas through its provider (`SciQLop/plugins/tscat_catalogs/tscat_provider.py`, `orphans.py`), including a driver-thread query path for `tscat.get_events()` / `tscat.get_catalogues()`; catalogs created in SciQLop are ordinary tscat catalogs usable by other tscat clients.
- **tscat_gui** — SciQLop hands a live catalog off to the standalone TSCatGUI editor ("Open in TSCat editor…" on the *My Catalogs* row, routed through `CatalogProvider.actions()`); both surfaces operate on the same tscat store.
- **cocat** — the `collaborative_catalogs` plugin joins a cocat room and exchanges CRDT catalog state over WebSocket, so several SciQLop instances co-edit one catalog conflict-free; includes cocat-specific operations such as the `MOVE_CATALOG` attribute mutation and CRDT `set_attributes` write-through. Tests `tests/test_cocat_event_meta.py` and `tests/test_cocat_move_catalog.py`. (The plugin ships `"disabled": true` by default at v0.12.0, so the integration is opt-in — see Field 8.)
- **JupyterLab / Jupyter** — Tier B, admitted on cited evidence rather than dependency presence. SciQLop embeds a full IPython kernel and launches a JupyterLab server bound to it: `SciQLop/components/jupyter/kernel/manager.py:1` is `from jupyqt import EmbeddedJupyter`, and `SciQLop/components/workspaces/backend/workspace_project.py:33,35,148,151` provisions `jupyqt` and `jupyterlab` into each workspace venv as implicit dependencies. The exchange is genuinely two-way: notebook cells create and drive SciQLop panels through `SciQLop.user_api`, and SciQLop ships IPython magics (`%plot`, `%%vp`, `%%layer`, `%timerange`, `%install`) plus "Copy Python code" reproducer snippets generated *for* notebooks (`SciQLop/core/snippets/templates/notebook_matplotlib.j2`). README: "analyze your data in Jupyter notebooks side by side with interactive plots."

**Considered and excluded:** every Tier A package listed under Field 29; **matplotlib**, **seaborn** and **scipy** (used internally for colormaps, styling and filter design — no documented exchange of a shared data model, and each would read the same for most packages); **SciQLopPlots** and **NeoQCP** (SciQLop is *built on* them, which is a dependency relationship rather than interoperation between peer tools — SciQLopPlots is recorded in Field 29); **PySPEDAS** (see Field 29 — its example was deleted upstream).

**Note on HSSI display names:** the live record's RelatedItem entries render as placeholder names (`UNKNOWN` / raw URL). Those placeholders are never user-visible and were disregarded when deciding these values; the DOI or URL is the identity.

### 31. Related Instruments (OPTIONAL)
**Value:** Not found — deliberately empty. No instrument is recorded.

**Change vs the 2025-10-09 canonical file (removal, documented):** that file listed *MMS*, *THEMIS* and *ACE* with the note "instrument identifiers (DOIs) not available". All three are removed. Live HSSI has no `relatedInstruments` at all, so nothing published is being dropped.

**Reason — SciQLop is instrument-agnostic.** It is a general multi-mission browser: `build_product_tree` / `explore_nodes` walk Speasy's *entire* inventory and build the Products tree generically, and `get_components` / `data_serie_type` branch on the **provider** (`amda`, `ssc`, `UiowaEphTool`) and on generic ISTP attributes — never on a mission or instrument.

**What the mission and instrument name mentions actually are, scoped to `v0.12.0`:** a repository-wide search at the tag, excluding `SciQLop/examples/`, returns only — the product-search placeholder text `"Search products (e.g. MMS FGM, ACE MAG B_gsm)…"` (`SciQLop/components/plotting/ui/product_search_overlay.py:67`); agent tool help strings using `amda.Parameters.MMS.MMS1` and `speasy//amda//Parameters//MMS//MMS1` as illustrative inventory paths (`SciQLop/components/agents/tools/_builder.py:184,207`); a workspace-manifest **format docstring** whose example installed-example entry is `name = "MMS"` (`SciQLop/components/workspaces/backend/workspace_manifest.py:18`); and product-path fixtures scattered through `docs/plans/*.md` and `tests/`. There is no instrument-specific parser, calibration, format or code path anywhere at the tag.

Two mentions cited in the previous revision of this file do **not** exist at `v0.12.0` and have been withdrawn: the code comment about MMS's Search Coil Magnetometer arrived after the tag, and the onboarding-tour target pointing at `ACE / MFI / b_gse` is part of the onboarding component, every commit of which post-dates the tag. Their removal strengthens rather than weakens the conclusion — the surviving mentions are even more clearly placeholders, help text, docstrings, design notes and test fixtures.

The 2025-10-09 entries rested entirely on example notebooks and README usage snippets — exactly the demo/name-drop case the relevance gate excludes. Listing three instruments while omitting the hundreds of others equally supported would be arbitrary and would mislead anyone searching HSSI by instrument.

**SPASE resolution work performed anyway, so a future include decision starts from verified rows.** The controlled vocabulary was fetched once (7,648 rows, of which 0 have a non-SPASE identifier) and filtered locally. Every candidate below is multi-row **ambiguous**, so even under an "include" decision none could be emitted as a clean value — each would have to be marked `NEEDS MANUAL RESOLUTION`:
- **MMS FGM** — 330 rows match `FGM` / `Fluxgate Magnetometer` (type 1), across dozens of missions. Not resolvable from the acronym.
- **MMS FPI / DIS / DES** — 30 rows match `FPI` / `Fast Plasma`; the MMS-relevant ones alone are four identically-named CDPP-AMDA rows "Fast Plasma Investigation" (`CNES/Instrument/CDPP-AMDA/MMS1..4/FPI`) plus CDPP-Archive rows split per-probe *and* per-sensor ("MMS 1 Fast Plasma Instrument", abbreviations `DIS` and `DES`). Ambiguous.
- **THEMIS ESA** — 16 rows under the rule "type 1 and name or identifier matching a `THEMIS/<probe>/ESA` path or the phrase *Electrostatic Analyzer*"; a broader rule that also accepts the bare abbreviation `ESA` anywhere returns 28, and 10 of those 16 sit on a THEMIS identifier path. Under the narrow rule the THEMIS-relevant matches are five identically-named CDPP-AMDA rows "Dual Full Distribution Electrostatic Analyzers" (`CNES/Instrument/CDPP-AMDA/THEMIS/A..E/ESA`, plus two ARTEMIS probes) alongside SMWG per-probe rows such as `SMWG/Instrument/THEMIS/A/ESA` ("THEMIS-A Electrostatic Analyzers"). Ambiguous under any of the three rules.
- **ACE MFI** — the only two rows matching `MFI` are both **Wind**, not ACE (`SMWG/Instrument/Wind/MFI` and `CNES/Instrument/CDPP-AMDA/Wind/MFI`). ACE's magnetometer is not reachable under the acronym used in the repository, which is itself a caution against acronym-driven matching.

### 32. Related Observatories (OPTIONAL)
**Value:** Not found — deliberately empty. No observatory is recorded.

**Change vs the 2025-10-09 canonical file (removal, documented):** that file listed *MMS*, *THEMIS* and *ACE* with no identifiers. All three are removed, for the same agnosticism reason given under Field 31. Live HSSI has no `relatedObservatories`, so nothing published is being dropped.

**SPASE resolution work performed — every candidate examined, every fallback considered.** Filtered from the same 7,648-row vocabulary, restricted to `type = 2`. No candidate family contains `.html` identifier twins, so no `.html` normalization was needed:
- **MMS — 16 candidate rows.** `SMWG/Observatory/MMS` ("Magnetospheric Multiscale"), `SMWG/Observatory/MMS/1..4` ("MMS-1".."MMS-4"), `CNES/Observatory/CDPP-AMDA/MMS` ("Magnetospheric Multiscale Mission"), `CDPP-AMDA/MMS1..3` ("… Mission #1..#3"), `CDPP-AMDA/MMS4` (name "MMS4"), `CDPP-AMDA/MMS1234` ("… Mission : 4 s/c"), and `CDPP-Archive/MMS` plus `CDPP-Archive/MMS-1..4`. The mission-level `SMWG/Observatory/MMS` was verified resolvable, but it is not the single unambiguous match the vocabulary requires: the **bare name "MMS" belongs to a different row** (`CNES/Observatory/CDPP-Archive/MMS`), so a name-only write would bind to the wrong resource.
- **THEMIS — 61 candidate rows,** under the rule "type 2 and `THEMIS` matched case-insensitively in the row `name` or anywhere in the SPASE identifier path". Those 61 rows carry **61 distinct SPASE identifiers** and contain no `.html` twins, so the vocabulary is unambiguous about how many resources exist. What it is *not* unambiguous about is naming: there are only **55 distinct names**, and three name-collision families account for the gap — five probe rows all named "MIDEX/THEMIS" (`CNES/Observatory/CDPP-AMDA/THEMIS/ThemisA..E`); `SMWG/Observatory/AUTUMN` and `SMWG/Observatory/Ground/AUTUMN`, both named "Athabasca University THEMIS UCLA Magnetometer Network"; and `SMWG/Observatory/Ground/GMAG` and `SMWG/Observatory/THEMIS/Ground`, both named "THEMIS-Associated Ground Magnetometer Stations". 42 of the 61 rows are ground stations or networks (`SMWG/Observatory/THEMIS/Ground/...`, UCLA-EPO / GBO / CANMAG). The spacecraft family is `SMWG/Observatory/THEMIS` ("Time History of Events and Macroscale Interactions during Substorms", verified resolvable) with per-probe children `THEMIS/A..E`. Note that case-insensitive matching is required: `CNES/Observatory/CDPP-AMDA/Themis` uses a mixed-case path segment and spells the mission out in its name rather than using the acronym, so a case-sensitive identifier test silently drops it. It is the **name collisions**, not the row count, that make a bare-name write dangerous here.
- **ACE — 2 candidate rows.** `SMWG/Observatory/ACE` ("Advanced Composition Explorer", verified resolvable) and `CNES/Observatory/CDPP-AMDA/ACE` ("Advanced Composition Explorer, NASA"). Two candidates, so still ambiguous under the resolution ladder.
- **Cluster — 15 candidate rows** (`SMWG/Observatory/Cluster`, `Cluster-Rumba/Salsa/Samba/Tango`, CDPP-AMDA `Cluster1..4`, CDPP-Archive `Cluster` / `Cluster-1..4`). Considered because Speasy's Cluster Science Archive (`csa`) provider node is surfaced in SciQLop's Products tree — but that is generic archive plumbing, not Cluster-specific support, so Cluster fails the relevance gate as well as being ambiguous.
- **Observatory-level fallback considered and rejected.** Where an instrument cannot be resolved, the ladder allows falling back to its SPASE observatory/platform record. That fallback is not used here because the *observatories themselves* fail the relevance gate — SciQLop is not designed to support MMS, THEMIS, ACE or Cluster specifically. Falling back would launder a relevance failure into a resolution success.

**Nothing was omitted merely for being hard to resolve.** Every candidate was resolved as far as the vocabulary allows and then rejected on relevance; the ambiguity findings above are recorded so a future include decision starts from verified data rather than from scratch. Should MMS ever be added — it has the strongest case, since SciQLop ships a dedicated installable MMS example workspace (`SciQLop/examples/mms/` with `example.json`, `index.ipynb`, `DemoMMS_tags-up_meeting.ipynb` and `MMS_dayside_magnetopause.ipynb`, all present at `v0.12.0`), the project's demo screencast is `SciQLop_MMS.gif`, and the README's primary API examples use MMS products — it would have to be hand-bound to one of the 16 rows, most plausibly `Magnetospheric Multiscale` / `https://spase-metadata.org/SMWG/Observatory/MMS`.

### 33. Logo (OPTIONAL)
**Value:** https://raw.githubusercontent.com/SciQLop/SciQLop/main/SciQLop/resources/icons/SciQLop.png

**Source:** Existing HSSI record. Re-verified: the URL still resolves and serves a PNG image; the file exists at that path in the checkout; the README renders it as the project banner; and the PyHC community registry entry for SciQLop lists the identical URL as its `logo`.

**Unchanged from live HSSI.**

---

## Reconciliation Summary

**Sources, in priority order:** live HSSI record (authoritative for current published state) → PyHC community registry → Zenodo/DataCite for the v0.12.0 version DOI and the concept DOI → repository primary sources at tag `v0.12.0` and at HEAD (CITATION.cff, `pyproject.toml`, `CHANGELOG.md`, README, `COPYING`, source code, tests, bundled tutorials, CI workflows) → GitHub API (releases, tags, languages, topics) → ORCID public API (author employments) → ROR API (organization identifiers) → HSSI controlled vocabularies (`FunctionCategory`, `Region`, `ProgrammingLanguage`, `FileFormat`, `DataInput`, `Phenomena`, `RepoStatus`, `License`, `InstrumentObservatory`) → Crossref (publication DOIs). The stale `somef_output.json`, `datacite.json`, `zenodo.json` and `pyhc_community.yml` artifacts left in the working tree by the 2025-10-09 run were treated as history, not evidence; all APIs were re-queried.

**Changed vs live HSSI — 13 fields, all patched and roundtrip-verified 2026-07-29:**

| Field | Live value | This file | Why |
|---|---|---|---|
| 4 Software Functionality | 9 values | 12 values | +3 (Data Reduction, Processing, Spectrogram); the `dsp` module first shipped in v0.12.0 |
| 6 Authors | 5 authors; Génot and André with no affiliation | same 5 authors; **3 affiliations added** — André ×2 (IRAP, ISAE-SUPAERO), Génot ×1 (IRAP) | ORCID employment record plus two 2025 abstract bylines; purely additive — no author dropped, no affiliation replaced or removed, Aunai carried at his live value |
| 8 Description | ends at "…handling to students." | same text + 1 appended sentence | published text had become materially incomplete; original preserved byte-verbatim |
| 12 Version | `v0.10.0` | `v0.12.0` + date, description, version DOI | v0.12.0 is newest release / tag / PyPI upload; version DOI `10.5281/zenodo.20261873` |
| 13 Programming Language | 1 value | 2 values | +`Javascript` (60,823 bytes in `welcome.js` / `appstore.js`) |
| 16 Keywords | 7 | 38 | live 7 all retained; 26 file-only additions retained and normalized; +3 new |
| 17 Data Sources | 5 values | 5 values | −`Observatory/Mission-specific` (no observatory-specific code path; Field 32 empty), +`HTTP/HTTPS Directories` |
| 18 Input File Formats | 3 | 4 | +`ISTP-Compliant` (`SciQLop/core/istp_hints.py`, 6 ISTP attributes) |
| 19 Output File Formats | empty | `Other` | `PlotPanel.save()` images, `save_template()` YAML — none in the controlled list |
| 23 Development Status | empty | `Active` | HEAD 2026-07-26; 11 releases since v0.10.0; `0.13.0.dev0` in flight |
| 27 Related Publications | empty | 5 DOIs | five Crossref-verified developer-authored abstracts describing SciQLop |
| 29 Related Software | 1 value | 5 values | +SciQLopPlots, tscat, tscat_gui, cocat (domain-specific companions/dependencies) |
| 30 Interoperable Software | 1 value | 5 values | +tscat, tscat_gui, cocat, JupyterLab — each with a specific demonstrated exchange |

**Unchanged vs live HSSI — 12 fields:** 15 License (name already correct), 2 Persistent Identifier, 3 Code Repository, 5 Related Region, 7 Software Name, 9 Concise Description, 10 Publication Date, 11 Publisher, 20 Operating System, 21 CPU Architecture, 24 Documentation, 33 Logo.

**Empty on both sides (no-op) — 6 fields:** 14 Reference Publication, 22 Related Phenomena, 26 Award Title, 28 Related Datasets, 31 Related Instruments, 32 Related Observatories. Field 22 is a no-op against HSSI even though three values were dropped relative to the 2025-10-09 file, because live HSSI never held them.

**Not expressible through the update API — 1 field:** 25 Funder. Live value retained; the ROR upgrade is a deferred correction requiring direct curation of the shared organization record.

**Not part of the stored record — 1 field:** 1 Submitter.

Accounting: 13 changed (patched) + 12 unchanged + 6 no-op + 1 non-patchable (25) + 1 submitter = **33 fields**.

**Applied 2026-07-29** by `PATCH /api/data/software/1b5fd49d-9131-46ee-b56a-70efbb1effe5/` against `http://localhost`, which reported exactly the 13 intended fields updated. Every changed field was roundtrip-verified, every omitted field confirmed byte-intact, and the version confirmed stored bare (the view renders it as `SciQLop - v0.12.0`). Field 6 bound as intended: Génot and André to the existing IRAP organization row, Aunai unchanged, and exactly one new organization row created for ISAE-SUPAERO.

**Nothing is silently removed from live HSSI.** Exactly one live published value is dropped — `Observatory/Mission-specific` from Field 17 — and it is documented above with its reason. No author and no author affiliation is dropped or replaced anywhere: Field 6 is purely additive, and Aunai's affiliation is deliberately carried at its live stored value with the canonical correction recorded as deferred. The only other change that touches an existing live value is Field 25, where Plas@Par's URL identifier is upgraded to its ROR; Field 8 appends to the published description without altering a character of it.

**Corrections to the 2025-10-09 canonical file:** Publication Date `2025-09-22` → `2018-12-15`; Publisher identifier (concept DOI → `https://zenodo.org`); removal of the out-of-vocabulary values `Data Visualization:Interactive`, `Jupyter Notebook`, `CPU Independent (Python-based)`, `Magnetic fields`, `Electric fields` and `Particle distributions`; removal of `C++` from Programming Language and `Data Visualization:Web-Based` from Software Functionality as unsupported; removal of PySPEDAS (its example was deleted upstream); removal of QCustomPlot / PySide6 / NumPy from Related Software as generic infrastructure; removal of the identifier-less MMS / THEMIS / ACE instrument and observatory entries; `Planetary Magnetospheres` added to Related Region (a live value the file lacked).
