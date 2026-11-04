# HSSI Metadata Extraction Results

**HSSI Software ID:** 85fefaab-71cb-461b-bce8-04493730eb7d
**Repository:** https://github.com/erdoganfurkan/HelioAI
**Source Revision:** e45edbb62162a2de2aa024e003755a1b9d252cd4
**Extraction Date:** 2026-11-03
**Validation Date:** 2026-11-03
**Validation Status:** PASS

---

**Scope note.** The pinned revision is the tip of `main` on 2026-10-15, two commits after the `v0.4.0` release tag (`95f93bc`): `c944947` ("fix(mcp): one workspace per stdio process, whatever the protocol era") and its merge `e45edbb`. That change touches only `helioai/mcp_server.py` and `tests/test_mcp_server.py`, so every value below reads the same at `v0.4.0` and at the pin; `CITATION.cff` and the `[0.4.0]` section of `CHANGELOG.md` are byte-identical at both. The PyHC registry entry cited throughout is the `HelioAI` entry of `_data/projects.yml` (the community list) at heliophysicsPy/heliophysicsPy.github.io commit `b1e3c973eebe77486b9530bf06667b8a0fb2be3e`. The project's whole git history is the work of one person under three commit identities (`Furkan <furkan.erdogan@akkodis.com>`, 2026-05-31 to 2026-08-28; `Furkan <furkan.erdogan.pro@gmail.com>`, from 2026-08-28; and the GitHub account `erdoganfurkan`, noreply id 78423357); the GitHub contributors API lists that account alone.

HelioAI is an LLM-driven agent: most user-facing analysis happens in a Python sandbox (`run_python`) where the language model writes code. This dossier credits the software only with what its own distributed code ships — the registered tools in `helioai/tools/setup.py`, the eleven recipes in `helioai/data/recipes/`, the sandbox helpers in `helioai/tools/sandbox_helpers.py`, the interfaces under `helioai/interfaces/`, and the skill templates in `helioai/core/skills/` — never with what an LLM could in principle write in the sandbox.

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** Shawn Polson
- **Submitter Email:** shawn.polson@lasp.colorado.edu

**Source:** Supplied by the user for this submission (Field 1 rule 4). The name is written as the catalogue's existing Person row for this submitter stores it (`Shawn` / `Polson`, carrying ORCID `https://orcid.org/0000-0003-0619-5745`), so the submitter binds that row rather than minting a new one.

**Note:** The addresses found in the software's sources — `furkan.erdogan.pro@gmail.com` (`CITATION.cff`, `pyproject.toml`) and `furkan.erdogan@akkodis.com` (early commits) — belong to the author and are correspondence context only, never this field (rule 2).

### 2. Persistent Identifier (RECOMMENDED)
Not found

**Why empty (rule 8, with the no-DOI proof run 2026-11-03):** HelioAI has no DOI of its own.
- **The project's own files carry none.** `CITATION.cff` has no `doi` or `identifiers`; there is no `.zenodo.json` and no `codemeta.json`; the README badges are CI, codecov, PyPI, PyHC, License and Python, with no DOI badge; the README's "How to cite" block is a `@software` BibTeX entry giving `url` and `version` but no DOI. Every `zenodo` or `10.5281` string in the pinned tree (a case-insensitive sweep of the whole tree) is another work's DOI: PHEP 3 (`10.5281/zenodo.17794207`, the PyHC support-policy document cited in `CHANGELOG.md`, `CONTRIBUTING.md`, `docs/installation.md` and `docs/dev/dependencies.md`); the IPShocks database (`10.5281/zenodo.19730292`, cited in `examples/00_quickstart.ipynb` as an independent comparison value); and, inside the test fixture `tests/fixtures/tool_results/list_catalogs.json`, the DOIs that AMDA's own catalogue descriptions give for their event lists (`10.5281/zenodo.6240624`, the Martian bow-shock crossing lists, and `10.5281/zenodo.6343989`). The tree's other `doi` strings are method and dataset citations in recipe headers, docs and code strings. Automated extraction (SoMEF) finds no identifier either.
- **Title and subject search.** Zenodo `title:HelioAI`, `HelioAI`, `"helioai agent"` and `"heliophysics" AND "agent" AND "natural-language"` each returned 0. DataCite `titles.title:HelioAI` returned 0, and `titles.title:"heliophysics data discovery and analysis"` (the `CITATION.cff` title) returned 0. DataCite free-text `HelioAI` returned two records, both "Connecting the Dots: A Machine Learning Ready Dataset for Ionospheric Forecasting Models" (`10.5281/zenodo.18343832`, `.18343833`) — a dataset unrelated to this software. Positive control: `title:solarmach` returned 2 at Zenodo and 30 at DataCite.
- **Former names.** The repository has been named HelioAI since its first commits (the README at `321dced`, 2026-06-02, is titled `# HelioAI`); the GitHub API's `full_name` is `erdoganfurkan/HelioAI` and GitHub serves the URL without a redirect. Free-text `"erdoganfurkan/HelioAI"` returned 0. The distribution name differs (`helioai-agent`, because PyPI rejected `helioai` as confusable with `helloai`, per `CHANGELOG.md` `[0.2.0]`); the quoted search `"helioai agent"` returned 0.
- **Creator-keyed search.** Zenodo `metadata.creators.person_or_org.name:` with `"Erdogan, Furkan"`, `"Furkan Erdogan"` and `"erdoganfurkan"` each returned 0. DataCite `creators.name:"Erdogan, Furkan"` returned three records by other people of that name (radiation-shielding work at Virginia Commonwealth University, and a cosmology preprint). Positive control: `metadata.creators.person_or_org.name:"Polson, Shawn"` returned 31.

**Re-check at the next refresh:** a GitHub–Zenodo integration deposit or a software paper would supply a concept DOI; Field 11 would then move from GitHub to Zenodo (Field 2 coupling).

### 3. Code Repository (MANDATORY)
https://github.com/erdoganfurkan/HelioAI

**Source:** Rule 7 (canonical base URL). The clone's `origin` remote, the GitHub API (`full_name` `erdoganfurkan/HelioAI`, `html_url` identical, `fork: false`, `archived: false`), `pyproject.toml` `[project.urls] Repository`, `CITATION.cff` `repository-code`, `mkdocs.yml` `repo_url` and the PyHC registry `code:` all give this URL. Written without `.git` or a trailing slash, in the letter case GitHub's API returns.

### 4. Software Functionality (RECOMMENDED)
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Pitch Angle Distributions
- Data Processing and Analysis: Processing
- Data Processing and Analysis: ML/AI
- Data Visualization
- Data Visualization: Line Plots
- Data Visualization: Hodograms
- Data Visualization: Web-Based
- Coordinate Transforms
- Coordinate Transforms: Magnetospheric
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Physics-Based
- Servers and Environments
- Servers and Environments: Data servers processing and handling
- Servers and Environments: Software or Environment Container

Each child is listed beside its bare parent (rule 10), parents first within each family.

**Evidence, value by value:**
- **Data Access and Retrieval** — the agent tools `search_parameters` (hybrid MiniLM + BM25 search over HelioAI's own index of speasy products, `helioai/tools/rag.py`), `get_timeseries` (downloads any indexed product through speasy, from AMDA, CDAWeb, the Cluster Science Archive, SSCWeb or CDAWeb's public file tree — Field 17; `helioai/tools/speasy_tools.py`), `list_catalogs` / `get_catalog` / `get_events_timeseries` (AMDA event catalogs and timetables, and every event's data in one call, `helioai/tools/catalog_tools.py`), and HelioAI's own HTTPS loader for the HELIO4CAST ICMECAT CSV (`_fetch_helio4cast_csv`, `urllib.request`). Retrieval through the speasy dependency is user-facing: the user asks and receives the data (rules 2–3); the ICMECAT loader is HelioAI's own network code.
- **Analysis** — the shipped recipes `theta_bn` (shock-normal angle by magnetic coplanarity), `rankine_hugoniot` (compression ratio, shock speed, Mach numbers), `shock_timing_2sc` (two-spacecraft shock timing), `mvab` (minimum variance analysis) and `walen_test` (de Hoffmann–Teller frame and Walén slope), run by the `run_recipe` tool; and the tools `plasma_beta`, `gyrofrequency`, `debye_length`, `alfven_speed`, `inertial_length` (`helioai/tools/plasmapy_tools.py`), which derive plasma parameters.
- **Time Series Analysis** — the `power_spectrum` tool (Welch power spectral density, peak frequency), the `superposed_epoch` recipe (superposed epoch analysis with bootstrap confidence intervals over an event collection), and the `sep_onset_poisson_cusum` recipe (Poisson-CUSUM onset detection on particle intensity series).
- **Pitch Angle Distributions** — the `pitch_angle_dist` recipe computes pitch angles from particle velocity and magnetic field vectors and returns the binned distribution and an anisotropy.
- **Processing** — every download has its fill values replaced by NaN from the dataset's declared `FILLVAL` (`helioai/datastore.py` `fill_mask`/`blank_fill`, applied in `get_timeseries`); the sandbox helper `interp_to` puts series from different cadences on one time base; the `fill_values` recipe ships the same masking logic for scripts outside HelioAI.
- **ML/AI** — the software is an LLM agent that performs the analysis (`helioai/core/agent_loop.py`, sub-agents in `helioai/core/sub_agents.py`, providers in `helioai/core/llm/`), finds parameters by sentence-transformer embeddings (`helioai/indexer.py`, `helioai/tools/rag.py`), and reviews its own figures with a vision model (`helioai/core/vision.py`). Machine learning applied to data analysis is its core mechanism.
- **Line Plots** — the `superposed_epoch` and `sep_onset_poisson_cusum` recipes draw line plots with matplotlib; `run_python` captures every figure as a PNG (and PDF) artifact; the shipped plotting skill (`helioai/core/skills/plotting/SKILL.md`) carries the multi-panel time-series and log-log PSD templates the agent uses.
- **Hodograms** — the same shipped plotting skill names "hodogram" in its `when_to_use` line and carries a "Hodogram template" (§5), which the agent loads when a user asks for one; the helper skill's reconnection workflow uses it to find the minimum-variance direction. The capability is a template the agent follows, not a dedicated plotting function; it is recorded because the template is part of the installed package and yields the hodogram the user asks for (rule 4 excludes only examples that live outside the distributed package).
- **Web-Based** — `helioai serve --web` runs a browser application (`helioai/interfaces/web/app.py`, FastAPI; `static/app.js`) in which a user asks questions in the page and the session's figures are shown there, each downloadable as PNG and PDF. The figures themselves are static matplotlib images, not browser-side interactive plots; the value is recorded because the whole question-to-figure workflow runs in the browser with nothing to code, which is what a user browsing for web-based visualization tools looks for.
- **Coordinate Transforms: Magnetospheric** — the sandbox helper `transform_coords(time, vectors, frm, to)` rotates vectors between GSE, GSM, SM, GEO, MAG and GEI, recomputing the dipole tilt per point through geopack; it is documented to users in the `run_python` tool description and is carried into exported notebooks (`helioai/export.py`). A user-selected transform whose output the user receives qualifies (rule 3).
- **Empirical** — the sandbox helpers `mp_shue1998` (Shue et al. 1998 magnetopause) and `bs_jelinek2012` (Jelinek et al. 2012 bow shock) are, in the module's words, "clean-room implementations from the published papers", returning boundary profiles from solar-wind dynamic pressure and IMF Bz.
- **Physics-Based** — the `pressure_balance` recipe models the subsolar magnetopause standoff from physical equations: it balances the solar wind's dynamic and magnetic pressure against Earth's dipole field (`B_dip(r) = B0 (R_E / r)^3`, epoch-2020 IGRF dipole coefficients) amplified by the Chapman–Ferraro factor (`F_CF = 2.0`), and returns the standoff distance `r_mp_RE` with the pressures behind it.
- **Data servers processing and handling** — HelioAI is also an MCP server (`helioai/mcp_server.py`, console script `helioai-mcp`; `helioai mcp-install` wires it into Claude Code, Claude Desktop or Codex) that serves its data-search, download and analysis tools to other AI clients, and a web server (`helioai serve --web`).
- **Software or Environment Container** — `docker/Dockerfile` and `docker/docker-compose.yml` build and run HelioAI as a container image with bubblewrap installed for sandbox isolation; `docs/installation.md` documents Docker as one of the three install routes, and the `docker` job in `.github/workflows/ci.yml` builds the image and runs `helioai doctor` inside it.

**Considered and not selected:**
- **Data Visualization: Orbit Plots** — the only orbit-style figure the package ships is the `solar_mach` recipe's Parker-spiral connectivity plot, which is drawn entirely by the optional `solarmach` package (`pip install "helioai-agent[solarmach]"`); a capability that exists only after installing a separately distributed package is excluded (rules 5–6). The web UI's example prompt asking for MMS1's position against the Shue magnetopause and Jelinek bow shock is answered by LLM-written sandbox code, not a shipped plotting routine.
- **Data Visualization: 2D Graphics** — the `pitch_angle_dist` recipe's figure is a histogram, not a contour, heat-map or image plot.
- **Data Visualization: Spectrogram / Data Processing and Analysis: Spectrogram / Wavelet Analysis** — `power_spectrum` returns a single power spectrum, not a time–frequency array, and no shipped code computes or draws a spectrogram or a wavelet transform. A sweep of `helioai/` for `spectrogram|wavelet|pcolormesh|imshow` matches only text: the docstring and error message of the sandbox's `magnitude()` helper, which refuses a spectrogram as input (`helioai/tools/sandbox.py`, the message repeated in `helioai/export.py`), and the keyword pattern in `helioai/tools/rag.py` that labels wave and spectrogram products in the index.
- **Data Processing and Analysis: Data Reduction** — `get_timeseries` downsamples to `max_points` only for the preview returned to the language model, and `get_events_timeseries` reports per-event statistics for the same purpose; neither is a reduction product the user requests.
- **Data Processing and Analysis: Plasma Moments, Energy Spectra, 3D Particle Distribution Processing, Curlometer, Linear Gradient Estimation, Wave Polarization Analysis, Field-line Tracing, Magnetic Null Finding, Calibration, Packet Decommutation, File Format Conversion, Image Processing, Data Assimilation, 2D Slices** — no shipped code computes any of these; plasma moments are read from the archives' own moment products.
- **Models and Simulations: Theory / First Principles** — the standoff calculation is a physical-equation model evaluated on measured inputs, carried as Physics-Based; nothing in the package solves the governing equations from first principles or is a standalone theoretical calculation.
- **Models and Simulations: ML/AI, Data Visualization: ML/AI** — the language models drive the analysis; they are not physical models, and no visualization displays model output or feature importance.
- **Coordinate Transforms: Heliospheric / Solar / Ionospheric / Planetary / Mission-Specific** — `transform_coords` covers geocentric frames only; heliographic coordinates appear only inside the optional `solarmach` package.
- **Mission-related (any child)** — HelioAI reads finished archive products of many missions and is part of no mission's ground segment or pipeline (rule 8).
- **Servers and Environments: Distribution/Access** — HelioAI distributes no science-data holdings of its own; its MCP and web servers relay archive search, download and analysis to their own clients, which `Data servers processing and handling` describes.
- **Servers and Environments: High Performance Computing** — no MPI, scheduler or cluster support.

### 5. Related Region (RECOMMENDED)
- Interplanetary Space
- Solar Wind
- Earth Magnetosphere

Written coarse row first, then its fine row.

**Evidence (rule 4 — where the physics the software's own code handles happens):**
- **Solar Wind** — the shipped shock recipes (`theta_bn`, `rankine_hugoniot`, `shock_timing_2sc`, whose reference is Russell et al. 1983, "Multiple spacecraft observations of interplanetary shocks") and the `walen_test` recipe analyse discontinuities and shocks in the solar-wind plasma; `pressure_balance`, `mp_shue1998` and `bs_jelinek2012` take solar-wind density, speed, dynamic pressure and IMF as their inputs; the built-in HELIO4CAST ICMECAT reader is a catalogue of interplanetary CMEs observed in situ in the solar wind. The project's own `CITATION.cff` keywords include "solar wind", and the headline README example is an interplanetary shock in Wind data.
- **Interplanetary Space** — the coarse row containing Solar Wind (rule 5), independently supported by the `sep_onset_poisson_cusum` recipe (solar energetic particle onsets observed in interplanetary space).
- **Earth Magnetosphere** — the `pressure_balance` recipe computes the magnetopause standoff distance, `mp_shue1998` and `bs_jelinek2012` model Earth's magnetopause and bow shock, and `transform_coords` converts between magnetospheric frames; `CITATION.cff` keywords include "magnetosphere". Recorded as the coarse row alone (rule 6): the boundary models locate the magnetosphere's outer boundaries from upstream input, and no shipped code processes data specific to one of its sub-regions.

**Considered and not selected:**
- **Earth Outer Magnetosphere, Earth Magnetosheath** — the magnetopause and bow-shock models place the boundaries of these regions from solar-wind input but compute nothing about the plasma inside them; adding them would make the record look more specific than the code is (rule 6).
- **Earth Magnetotail, Earth Inner Magnetosphere** — substorm and radiation-belt material appears only as AMDA catalogues reached through the generic catalogue tools and as text in the agent's skill prompts; no shipped code handles those regions' physics.
- **Earth Ionosphere, Earth Atmosphere, Planetary Magnetospheres (and each planet), Solar Environment, Corona, Heliosheath** — HelioAI's index labels products from missions in these regions (`_SPACECRAFT_REGION` in `helioai/indexer.py` maps spacecraft to SPASE regions for every archive), but that is archive-wide metadata, the same for every region; the software's own analysis code touches none of them. The `solar_mach` recipe's solar-footpoint connectivity is drawn by the optional `solarmach` package (Field 4).
- **Registry tags not used as evidence (rule 3):** the PyHC registry entry carries `heliosphere` and `magnetosphere` facet tags; the values above rest on the code, not on those tags.

### 6. Authors (MANDATORY)
1. **Furkan Erdogan**
   - **Identifier:** Not found
   - **Affiliation:** Not found

**Source:** `CITATION.cff` (`given-names: Furkan`, `family-names: Erdogan`), `pyproject.toml` `authors` (`Furkan Erdogan`), the README's citation block (`Erdogan, Furkan`) and the PyHC registry `contact:` all name the same single author (rule 8). The name is written as the project writes it, without the diacritic of the Turkish spelling "Erdoğan" (rule 12). Every commit in the history is this person's (see the scope note); no other contributor is attested anywhere, so the list is complete.

**Identifier — rejected candidates (rule 14).** No project source, DOI record or paper carries an ORCID for this author. The fielded ORCID searches `given-names:Furkan AND family-name:Erdogan` (4 records) and `given-names:Furkan AND family-name:Erdoğan` (14 records) were run on 2026-11-03 beside a positive control (`given-names:Shawn AND family-name:Polson`, 2 records, the submitter's among them). None links to this software, to heliophysics, or to the GitHub account:
- `0000-0001-8244-9415` (Furkan Erdogan) — an empty record: no works, no employment, no researcher URLs. A name match alone is not identity linkage.
- `0009-0009-3916-1497` (Furkan Erdogan) — listed by the search index under "Bursa Yuksek Ihtisas Egitim Ve Arastirma Hastanesi" (a training and research hospital in Bursa) and Uludağ University; nothing ties it to this work.
- `0000-0002-2489-2379` (FURKAN ERDOGAN) — Virginia Commonwealth University, Mechanical and Nuclear Engineering; works on radiation shielding and FeCrAl alloys. A different field and person.
- `0000-0002-9269-0541` (FURKAN ERDOĞAN) — one mathematics-education work; `0009-0004-3542-6180` (Furkan Erdoğan) — an empty record; `0009-0004-7432-5438` is "Furkan Mert Erdogan". The other Erdoğan records either carry a different given name (Muhammet, Ebubekir, Ali, Hatice, Muhammed or İbrahim Furkan; Furkan Kürşat) or are listed by the search index under Fırat University, Marmara University and Pfizer (Turkey), the Turkish Ministry of Health, Near East University, or Ondokuz Mayıs University's medical faculty; nothing ties any of them to this work.
The GitHub account `erdoganfurkan` publishes no name, company, website or bio.

**Affiliation — considered and not recorded (rules 20–21).** No project metadata source (`CITATION.cff`, `pyproject.toml`, PyHC registry) and no ORCID employment or paper byline gives an institution. The author's commits from 2026-05-31 to 2026-08-28 use the address `furkan.erdogan@akkodis.com` (Akkodis, an engineering consultancy), while every later commit and every project file uses a personal address; a commit-address domain is not one of the sources rule 21 accepts, and nothing says whether the work was done for that employer. An added affiliation cannot be withdrawn, so none is asserted.

**Person row:** the catalogue held no Person row for this author under either spelling before this submission (checked 2026-11-03), so the entry's author row carries no identifier. A later refresh that finds an ORCID with real identity linkage can add it to that row (rule 15).

### 7. Software Name (MANDATORY)
HelioAI

**Source:** Rule 8 (new value: the name the project uses for itself). The README's header image alt text ("HelioAI — heliophysics agent"), its prose throughout, `mkdocs.yml` `site_name`, the documentation site's page title, the GitHub repository name, the PyHC registry `name:` and the `CITATION.cff` title prefix all write `HelioAI`. Commit `c3d9f6d` ("fix(web): the wordmark reads HelioAI, not Helio AI") settles the spacing.

**Alternatives considered:** `helioai-agent` (the PyPI distribution name, chosen only because PyPI rejected `helioai` as confusable with `helloai`, `CHANGELOG.md` `[0.2.0]`); `helioai` (the import package); "HelioAI: a natural-language agent for heliophysics data discovery and analysis" (the `CITATION.cff` title — a name joined to a description, rejected under rules 1–2); "Helio AI" (the spacing the project corrected).

### 8. Description (MANDATORY)
HelioAI is an AI agent for heliophysics and space plasma physics. It resolves natural-language descriptions to parameter identifiers across more than 70 missions using hybrid semantic and lexical retrieval over the speasy catalogue, downloads the data, runs the analysis in a sandboxed Python environment, and exports the session as a self-contained, re-runnable Jupyter notebook. Derived quantities are computed from cited recipes so that every result carries its method and reference.

**Source:** `CITATION.cff` `abstract` at the pinned revision, verbatim after unfolding the YAML `>-` block (rule 7, first source in order). It says what the software does and why to use it, and its opening sentence stands alone as the card preview (rule 8).

**Every claim was tested against the pinned code:** natural-language resolution to parameter identifiers by hybrid semantic and lexical retrieval (`helioai/tools/rag.py`: MiniLM embeddings plus BM25, fused by reciprocal rank fusion, over the index `helioai/indexer.py` builds from speasy's inventory); "more than 70 missions" is the project's own figure (README "70+ missions", the helper skill's data table); downloading (`get_timeseries`); a sandboxed Python environment (`helioai/tools/sandbox.py`, bubblewrap isolation on Linux and in the Docker image — on macOS and Windows the sandbox falls back to a plain subprocess, which `SECURITY.md` and `docs/installation.md` state; the claim describes a capability present at the pin, so rule 2 does not fire); notebook export (`helioai/export.py`, `helioai export`); cited recipes (each file in `helioai/data/recipes/` carries a `# reference:` header, which the export's "Methods & data acknowledgements" cell collects).

**Alternatives considered:** the README lead ("AI agent for heliophysics and space plasma data analysis." followed by "Ask questions in natural language — HelioAI finds the right parameter across 70+ missions, downloads it, runs the analysis, and produces reproducible plots and notebooks.") says the same at landing-page length; the `CITATION.cff` abstract is the project's declared description and comes first in rule 7's order.

### 9. Concise Description (OPTIONAL)
An AI agent for heliophysics: natural-language parameter discovery across 70+ missions, sandboxed analysis, and reproducible notebook export.

**Source:** the PyHC registry `description:` of the `HelioAI` entry in `_data/projects.yml` (at the registry commit named in the scope note), verbatim — the first source in fields/09's priority order. It is 141 characters after trimming (rule 3) and has no autofill artifact (rule 1) and no error to fix (rule 4). It names what distinguishes the software — its mechanism (natural-language parameter discovery), its reach and its products — where the shorter candidates do not.

**Every claim is supported at the pinned revision (rule 2), as for Field 8:** natural-language parameter discovery is the hybrid semantic and lexical search over HelioAI's index (`helioai/tools/rag.py`); "70+ missions" is the project's own figure (README, the helper skill's data table); sandboxed analysis is `run_python` in `helioai/tools/sandbox.py`, isolated by bubblewrap on Linux and in the Docker image, falling back to a plain subprocess on macOS and Windows (`SECURITY.md`, `docs/installation.md`) — a capability present in the code, not an absent one; reproducible notebook export is `helioai/export.py` (`helioai export`, `%helioai_export`).

**Why a concise description is recorded:** by curatorial decision, every new entry in this submission batch carries both a description and a concise description. That overrides rule 6's empty outcome, which was the alternative not taken: the description's first sentence, "HelioAI is an AI agent for heliophysics and space plasma physics.", stands alone as a preview, so under rule 6 alone this field would have been left empty.

**Other candidates considered:** `pyproject.toml` `description` and the GitHub repository description, "AI agent for heliophysics and space plasma data analysis" (the GitHub form ends with a period), and the README's one-line tagline in bold, "AI agent for heliophysics and space plasma data analysis." These are accurate but come later in rule 6's order, and they drop the mechanism and products that set HelioAI apart.

### 10. Publication Date (RECOMMENDED)
2026-08-14

**Source:** Rule 4, anchor (a): the first public release. `v0.2.0` was published as a GitHub release at 2026-08-14T13:25:48Z and uploaded to PyPI (`helioai_agent-0.2.0-py3-none-any.whl`) at 13:25:57Z the same day; the tag is on the pinned revision's ancestry. `CHANGELOG.md` `[0.2.0]` calls it the "First published release. `0.1.0` was never released to PyPI, so this is the first version anyone can install." No `v0.1.0` tag or GitHub release exists.

**Alternative considered:** anchor (b), the repository's creation (GitHub `created_at` 2026-06-02T12:59:22Z, matching the root commit `4bb87a0` "Initial commit" of the same day). Rule 4 uses the repository date only when no release exists. (One commit, `e0493e7`, carries an author date of 2026-05-31, but it sits on top of the root commit and was committed on 2026-06-02, so the source was not public before that day.)

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Rule 5: there is no DOI (Field 2) and no source names a publishing or distributing institution, so the publisher is the repository host. Rule 6 keeps PyPI out (a distribution channel). GitHub has no ROR; its URL is the identifier (rule 7). The catalogue's existing `GitHub` Organization row carries exactly this identifier, so the value binds it.

### 12. Version (RECOMMENDED)
**Version Number:** 0.4.0

**Version Date:** 2026-10-01

**Version Description:** the six bullets below, verbatim from `CHANGELOG.md` at `v0.4.0` (line breaks as in the file). They are indented by four spaces here only so they do not read as sub-fields of this file; the value itself is the unindented markdown list.

    - **Search finds the product it is asked for** — recall@1 on the HelioBench identifier
      tasks 58.6 → 80.0 % live. Replace the index after upgrading: `helioai index --download`.
    - **The index is downloaded, not built**: `helioai index` fetches the one CI built for the
      release (~125 MB, about a minute) instead of 7 to 10 minutes of local build.
    - **One agent loop** for the lead and its sub-agents; the vetted recipes run as shipped
      (`run_recipe`); one verdict on every answer; a session replays from its journal.
    - **A first run that explains itself.** OpenCode is the default provider; a failure is one
      sentence naming the fix, in the CLI, the web UI and Jupyter; `helioai --version`;
      commands in the interactive prompt; a [troubleshooting page](https://erdoganfurkan.github.io/HelioAI/troubleshooting/).
    - **The web UI** gets the HelioAI logo, a narrow-screen layout, a profile editor, copy and
      export buttons, and a provider selector that knows which keys are set.
    - **A judge can watch, in observation** — off by default.

**Version PID:** Not found

**Release history (read 2026-11-03).** Tags, in creation order, all annotated and all on the pinned revision's ancestry: `v0.2.0` (2026-08-14), `v0.2.1` (2026-08-14), `v0.3.0` (2026-09-21), `v0.4.0` (2026-10-01); each has a GitHub release (none a pre-release) and a matching PyPI upload of `helioai-agent` (none yanked); each tag's `helioai/__init__.py` declares its own number. Nothing newer exists: the pin's `__init__.py` still declares `0.4.0` and the changelog's `[Unreleased]` section is empty.

**Number:** `0.4.0`, as PyPI, `helioai/__init__.py` and `CITATION.cff` write it; the git tag and GitHub release are `v0.4.0`. Both forms are correct (rule 5); a later refresh should not "fix" the prefix.

**Date (rule 7):** the GitHub release `published_at` 2026-10-01T21:02:38Z. Corroborated by the PyPI upload (2026-10-01T21:02:39Z), the tagged commit (`95f93bc`, 2026-10-01T15:39:33+02:00), `CITATION.cff` `date-released: "2026-10-01"` and the changelog heading — all the same day.

**Description (rules 13–16).** The GitHub release `name` is the bare tag, and its body is GitHub's auto-generated "What's Changed" pull-request list, which rule 16 never records. The next source is the changelog entry for the tag: the six bullets of the `### Highlights` subsection of `## [0.4.0] — 2026-10-01`, copied verbatim (line breaks as in the file) from `CHANGELOG.md` at `v0.4.0`. Every bullet reports new or changed user-facing behaviour. The rest of the entry — the paragraph that follows the bullets, "Upgrading from 0.3.0", and the long Fixed, Added, Removed and Changed sections — was trimmed as whole items (rule 15); the Highlights are the project's own summary of the release.

**Version PID:** no Zenodo or other deposit exists for any release (Field 2's searches), so it is empty (rule 18).

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- Javascript

**Python 3.x** — rules 4–5: `requires-python = ">=3.12"`, classifiers `Programming Language :: Python :: 3 :: Only` and 3.12/3.13/3.14, CI on Python 3.12–3.14; the wheel is `py3-none-any`. No compiled extension and no Python 2 target.

**Javascript** — rule 4's "supported front end in a second language that ships with the software and has its own tests or build target counts". The browser front end of the web interface, `helioai/interfaces/web/static/app.js`, is the project's own JavaScript (1,117 lines), ships in the wheel, and has its own JavaScript tests (`tests/web/test_turn_ui.js` and `tests/web/test_session_streams.js`, which drive the real `app.js` against a DOM stub), run by `tests/test_web.py` under Node whenever `node` is installed. A contributor working on the web interface works in JavaScript. Written `Javascript`, the vocabulary's spelling.

**Alternative weighed and not adopted:** reading rule 4's front-end sentence as an extension of "the language a user writes to use it" to second-language programming front ends (its example is a MATLAB package). On that reading `Javascript` would be left out, because HelioAI's users write Python, or nothing, never JavaScript, and a Language-tab user filtering for Javascript finds a Python agent. The record follows the rule's literal text instead: the web interface is a shipped, separately tested front end in a second language.

**Not recorded:** the vendored minified third-party libraries under `helioai/interfaces/web/static/vendor/` (marked, Prism, DOMPurify); HTML and CSS (not languages in the vocabulary); `scripts/record_demo.sh` (shell tooling) and `docker/Dockerfile` (build tooling); the Jupyter notebooks under `examples/` (a file format, Python kernel).

### 14. Reference Publication (OPTIONAL)
Not found

**Why empty (rule 7):** the project's citation guidance (`CITATION.cff`, the README's "How to cite") asks users to cite the software itself — a `type: software` record and a `@software` BibTeX entry with no DOI — plus the data providers and the method references each exported notebook lists; it names no paper about HelioAI (rule 1: a software citation is Fields 2/12). No paper describing HelioAI exists: ADS (anonymous Sci-X bootstrap token) `full:"HelioAI"`, `title:"HelioAI" OR abs:"HelioAI"`, `full:"helioai-agent"` and `full:"erdoganfurkan"` each returned 0 on 2026-11-03, with a positive control (`full:"solarmach"`, 141 records) and a negative control (`full:"xylophonicqwz"`, 0). `author:"Erdogan, Furkan"` returns papers by other people of that name (fracture mechanics, cosmology), none on this software. The arXiv API and Semantic Scholar did not serve as independent checks: arXiv's `all:HelioAI` returned 0 but so did its positive control `all:PlasmaPy`, and Semantic Scholar was rate-limited; ADS indexes arXiv preprints.

**Note:** "HelioBench", named in the release notes, is the project's own benchmark of agent tasks; ADS `full:"HelioBench"` returned 0 on 2026-11-03 (positive control `full:"pyspedas"`, 172), so no publication about it exists to consider.

### 15. License (RECOMMENDED)
MIT License

**Source:** Rule 3. `LICENSE` at the pin is the MIT text, headed "MIT License" with the line "Copyright (c) 2026 erdoganfurkan"; `pyproject.toml` `license = { text = "MIT" }` and the `License :: OSI Approved :: MIT License` classifier, `CITATION.cff` `license: MIT`, PyPI's `license: MIT`, the README badge and GitHub's detected `spdx_id: MIT` all agree. The licence has not changed since the first commit.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- heliophysics
- space physics
- plasma physics
- solar wind
- magnetosphere
- reproducibility
- large language models
- ai agent
- plasma
- mcp
- shock waves
- solar energetic particles
- magnetopause
- pyhc package

**Project-declared terms (rule 9).** `CITATION.cff` `keywords` (heliophysics, space physics, plasma physics, solar wind, magnetosphere, reproducibility, large language models, AI agent) and `pyproject.toml` `keywords` (heliophysics, plasma, space physics, AI agent, MCP). Each is supported by the software (rules 2–4 do not fire): "solar wind" and "magnetosphere" by the shock and boundary code described in Field 5, "reproducibility" by the notebook export, "large language models" and "AI agent" by the agent itself, "MCP" by the MCP server and client (`helioai/mcp_server.py`, `helioai/tools/mcp_client.py` — the Model Context Protocol). `heliophysics`, `space physics`, `plasma physics`, `solar wind`, `magnetosphere`, `reproducibility` and `plasma` are existing rows, bound exactly (the separate `space-physics` and `reproducible` rows are variants not used, rule 11). `large language models`, `ai agent` and `mcp` had no row in any case, separator or plural variant before this submission; they are new rows, written lower-case (rule 12). Note that "MCP" also abbreviates microchannel plate in instrumentation; the term is kept because it is the project's own accurate keyword.

**Domain terms added (rule 10, and Field 22 rule 1 for phenomena without a row):**
- `shock waves` (existing row) — collisionless shock analysis is the headline workflow: the `theta_bn`, `rankine_hugoniot` and `shock_timing_2sc` recipes, and `theta_bn`'s screening of |B| jumps for shock candidates. Interplanetary shocks have no Related Phenomena row. A search for "shock" reaches this row.
- `solar energetic particles` (existing row) — the `sep_onset_poisson_cusum` recipe detects SEP onsets; SEPs have no Related Phenomena row.
- `magnetopause` (existing row) — the `pressure_balance` recipe's magnetopause standoff and the `mp_shue1998` magnetopause model.

**PyHC marker (rule 15).** HelioAI is listed in the PyHC registry's `_data/projects.yml`, so `pyhc package` is recorded (existing row).

**Considered and not added:** `artificial intelligence`, `machine learning`, `natural language processing` (existing rows) — they restate Field 4's ML/AI value and the project-declared `ai agent` / `large language models` (rule 6); `jupyter` (existing row) — Jupyter is carried by Field 30 (rule 6–7); `amda` (existing row) — a Field 17 data source (rule 6); `speasy` — a dependency, carried by Field 29 (rule 7); `catalogs`, `event detection` — generic. **Registry tags not taken:** the PyHC entry's `heliosphere`, `plasma_physics`, `data_retrieval`, `data_access`, `data_analysis`, `plotting` and `cdaweb` are registry facet tags (rule 3); their meanings are already carried by Fields 4, 5, 17 and the project-declared keywords, and the underscore spellings are never minted.

### 17. Data Sources (OPTIONAL)
- AMDA
- CDAWeb
- SSCWeb
- HTTP/HTTPS Directories
- Other

**Evidence:** HelioAI's indexer walks six speasy providers (`_PROVIDER_PREFIXES` in `helioai/indexer.py`: `amda`, `cda`, `csa`, `ssc`, `archive` and `uiowaephtool`). The index snapshot tagged `v0.4.0` on the Hugging Face Hub (Field 28) holds 82,702 products from five of them — `cda` 68,233, `amda` 11,853, `csa` 1,936, `archive` 360 and `ssc` 320, none from `uiowaephtool`. `search_parameters` searches that index (its optional `provider` filter offers `amda`, `cda`, `csa` and `ssc`), `get_timeseries` downloads any product it returns through speasy, and `list_missions` lists every provider speasy exposes. The catalogue tools read AMDA's event catalogues and timetables.
- **AMDA** — AMDA (CDPP) parameters and its shared catalogues/timetables (`list_catalogs`, `get_catalog`, `get_events_timeseries`).
- **CDAWeb** — the `cda` provider (CDAWeb's web services), the bulk of the index.
- **SSCWeb** — the `ssc` provider's spacecraft trajectories are indexed (`_ssc_trajectory_doc` in `helioai/indexer.py`) and downloadable.
- **HTTP/HTTPS Directories** — speasy's `archive` provider reads CDF files directly from CDAWeb's public data tree: its built-in inventory (`speasy/data/archive/cda.yaml` in speasy 1.8.2, the version the `v0.4.0` index was built with) gives each dataset a URL pattern under `https://cdaweb.gsfc.nasa.gov/pub/data/…`, and the provider lists those directories and downloads the files. HelioAI indexes these products (ids `archive/cda/…`, all MMS and Arase datasets in the `v0.4.0` snapshot) and downloads them like any other. Rule 9: data files fetched from a plain multi-mission directory tree, recorded beside the data centre's own row as in the GFZ and WDC case.
- **Other** — two real sources with no row (rule 10): the ESA **Cluster Science Archive** (the `csa` provider), and **HELIO4CAST** (helioforecast.space), from which HelioAI's own code downloads the ICMECAT catalogue (`https://helioforecast.space/static/sync/icmecat/HELIO4CAST_ICMECAT_v23.csv`, `_fetch_helio4cast_csv` in `helioai/tools/catalog_tools.py`).

**Why speasy-mediated sources count here (rule 4).** Retrieval from AMDA, CDAWeb, the Cluster Science Archive, SSCWeb and CDAWeb's file tree runs through speasy, a required dependency that `pip install helioai-agent` installs with the package; no separately distributed plug-in or extra is needed to reach these archives, and HelioAI's own code chooses the providers, indexes their inventories and exposes the downloads as its tools (the README calls speasy "the data access layer powering HelioAI"). Rule 4's exclusion fires only when a source is reached after installing another package.

**Considered and not selected:**
- **HELIO4CAST as HTTP/HTTPS Directories** — its download is one named catalogue file at a fixed URL, not a directory tree (rule 9), so HELIO4CAST is named under `Other` (rules 6, 10); the HTTP/HTTPS Directories value rests on the `archive` provider above.
- **TAP** — how speasy's `csa` provider talks to the Cluster Science Archive is internal to that provider, behind a named archive service; HelioAI exposes no TAP query. (The `archive` provider differs: reading a directory tree is what that provider is, and its products appear to the user under their own `archive/` identifiers.)
- **The `uiowaephtool` provider** (the University of Iowa ephemeris tool) — the indexer walks it, but the `v0.4.0` index holds none of its products, so no HelioAI search returns them, and no HelioAI documentation describes fetching one by a raw identifier. Re-check when a later index carries its products.
- **Observatory/Mission-specific** — HelioAI is archive-wide and mission-agnostic; the user chooses the mission (Fields 31/32 are empty for the same reason).
- **HAPI, das2, OMNIWeb, Madrigal, VirES, GFZ, WDC, The Virtual Solar Observatory., FTP/FTPS Directories, S3/Cloud-aware** — no code reaches them. OMNI products may be indexed through CDAWeb, which is the source recorded.
- **NASA ADS** — the `find_papers` tool queries the ADS literature API; publication search is not a science-data source.
- **The prebuilt index** that `helioai index` fetches from the Hugging Face Hub is the software's own asset (rule 5).

### 18. Input File Formats (RECOMMENDED)
- csv

**Source:** Rule 5: HelioAI's own code reads the HELIO4CAST ICMECAT catalogue file it downloads (`HELIO4CAST_ICMECAT_v23.csv`) with `csv.DictReader` (`_load_helio4cast_catalog` in `helioai/tools/catalog_tools.py`) and turns it into an event catalogue the user queries with `get_catalog('helio4cast/icmecat')`. Scope, so the value is not over-read: HelioAI has no general reader for a user's own CSV files.

**Considered and not selected:**
- **CDF and the archives' other formats** — archive data arrive in memory through speasy; HelioAI's code opens no CDF file and accepts no data file from the user (rule 9).
- **JSON** — local event catalogues saved with `save_catalog` are written and read back by HelioAI itself (rule 4); the JSON manifest and `.jsonl.gz`/`.npy` files of the prebuilt index are the software's own asset; the `mcp-install` client configuration is configuration HelioAI writes, not data it reads.
- The `.env` file (`python-dotenv`) holds provider keys and settings — runtime configuration, not a data format.

### 19. Output File Formats (RECOMMENDED)
- JSON
- Other

**Source:** Rules 6–7.
- **JSON** — the `save_catalog` tool writes a user's detected events as an event catalogue, `<name>.json` (name, description, creation time and events with metadata; `helioai/tools/catalog_tools.py`), a data product the user asks for; the project documents these catalogues as speasy-format files that open in SciQLop (Field 30). The session export also writes JSON: the Jupyter notebook (`.ipynb`, built with `nbformat` by `helioai/export.py` through `helioai export` or `%helioai_export`) is a JSON document, and rule 7 records a format that has its own row as that row.
- **Other** — figures: `run_python` saves every matplotlib figure as PNG and as PDF (`plt.savefig` in `helioai/tools/sandbox.py`), and the web UI offers both for download. The vocabulary has no image row (rule 7).

**Considered and not selected:** the `.npz` arrays in each session's data directory (`helioai/datastore.py`) are the sandbox's internal store, which `load_data()` reads back (rule 3); the exported `code_*.py` scripts are Python source, not a data format; `helioai index --export DIR` writes the index snapshot (`manifest.json`, `.jsonl.gz`, `.npy`) that CI publishes — the software's own search index, not a product for users; `helioai doctor --json` prints a report to standard output, not a file.

### 20. Operating System (RECOMMENDED)
- Operating System Independent
- Linux
- Mac
- Windows

**Source:** Rule 3: pure Python (hatchling build, `py3-none-any` wheel, no compiled extension) with no OS restriction declared, plus each OS the project names: the classifiers `Operating System :: POSIX :: Linux`, `Operating System :: MacOS` and `Operating System :: Microsoft :: Windows`, and CI test jobs on `ubuntu-latest`, `macos-latest` and `windows-latest`.

**Caveat recorded with the values:** the sandbox's real isolation (bubblewrap) exists only on Linux; on macOS and Windows `run_python` falls back to a plain subprocess. `docs/installation.md` says "Linux is recommended.", the `pyproject.toml` comment beside the classifiers reads "The sandbox is only real on Linux (SECURITY.md); the other two run the fallback.", and the Windows CI job is marked experimental ("Windows is reported but not gating."). The software installs and runs on all three, which is what this field asks.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Source:** Rule 3: pure interpreted code; the project builds no compiled extension and publishes no architecture-specific artifact.

**Considered and not selected:** `GPU` — the code selects no device (`git grep` for `cuda|device\s*=|\bgpu\b` in the package finds nothing, while the positive control `SentenceTransformer` matches `indexer.py` and `rag.py`); sentence-transformers or torch might use a GPU on their own, which rule 6 does not count. `HPC or HEC` — no MPI or scheduler support. No arm64 row: the Mac CI runner does not add one (rule 3).

### 22. Related Phenomena (OPTIONAL)
- Solar Wind
- Coronal Mass Ejections

**Evidence (rule 5):**
- **Solar Wind** — the shipped recipes analyse the solar wind's shocks and discontinuities (`theta_bn`, `rankine_hugoniot` and `shock_timing_2sc` for interplanetary shocks, `walen_test` for rotational discontinuities), and the headline workflow is an interplanetary shock in Wind data. Decided independently of Field 5's place row (rule 8).
- **Coronal Mass Ejections** — HelioAI ships a dedicated reader for the HELIO4CAST ICMECAT interplanetary-CME catalogue (`_HELIO4CAST` and `_load_helio4cast_catalog` in `helioai/tools/catalog_tools.py`) so the user can download a parameter across every ICME (`get_events_timeseries`) and composite them (`superposed_epoch`). The inferential step: ICMEs are coronal mass ejections observed in the heliosphere, and this code exists to analyse them as a population.

**Considered and not selected:** `Geomagnetic Storms` — the only storm material is the example notebook `examples/02_stpatrick_storm_2015.ipynb` and a README Jupyter example; no shipped code computes a storm index or a storm-specific effect (rule 6). `Solar Flares` — SEP onset detection concerns energetic particles in interplanetary space, not flares; SEPs go to Keywords. `Solar Corona`, `Coronal Heating`, `X-ray emission` — no code touches them. Shocks and solar energetic particles have no row and are carried as Keywords (rule 1).

### 23. Development Status (RECOMMENDED)
Active

**Source:** Rule 6: the software has reached a stable, usable state (four releases on PyPI since 2026-08-14), and the last commit on the default branch is `e45edbb` at 2026-10-15T12:35:00Z, under six months before this record was prepared (2026-11-03). The last release is `v0.4.0` (2026-10-01). No repostatus.org badge and no status statement exist (rules 3–4); the README's badges carry no status, and the changelog's "While the version stays below 1.0, the public API may change between minor releases." is a versioning note, not a work-in-progress statement. The `Development Status :: 4 - Beta` classifier is a packaging label, not a repostatus term (trap). The repository is not archived.

### 24. Documentation (RECOMMENDED)
https://erdoganfurkan.github.io/HelioAI/

**Source:** Rule 3: the project's own MkDocs Material site, built and deployed to GitHub Pages by `.github/workflows/docs.yml`, named by `CITATION.cff` `url`, `mkdocs.yml` `site_url`, the README's "Documentation" link and table, and the PyHC registry `docs:`. The site's title is "HelioAI", and its Installation page (`/installation/`) carries install instructions for PyPI, source and Docker. Recorded with the trailing slash as the project writes it.

**Note:** `pyproject.toml` declares no `Documentation` URL (only Homepage, Repository and Issues, all the repository), and the GitHub repository's `homepage` is empty; neither offers an alternative. The repository has no wiki (GitHub reports `has_wiki: false`; the documentation site makes a wiki moot under rule 3).

### 25. Funder (OPTIONAL)
Not found

**Why empty (rule 12):** no source attributes funding to HelioAI. A case-insensitive sweep of the pinned tree (excluding `uv.lock`, `tests/` and the compressed data file) for `\bfund|grant\b|award|acknowledg|sponsor|supported by` finds no funding statement. Every match is something else: the "Methods & data acknowledgements" cell of the export and its descriptions (`helioai/export.py`, `README.md`, `CITATION.cff`'s `message`, `docs/index.md`, `docs/quickstart.md`, `docs/guide/export.md`, `docs/guide/recipes.md`, the two example notebooks), the Hugging Face index card's request to acknowledge the archives, `SECURITY.md`'s "acknowledgement within a week", a prompt line in `helioai/core/agent_loop.py` ("Do NOT acknowledge the off-topic request"), and two statistical uses of "supported by" in the `superposed_epoch` recipe. Those matches are also the sweep's positive control. There is no DOI record (Field 2), so no `fundingReferences`; there is no paper about the software (Field 14), so no acknowledgements section to read; `CITATION.cff` and `pyproject.toml` carry no funding keys. The author's employer address in early commits (Field 6) is not a funding statement (rule 6).

### 26. Award Title (OPTIONAL)
Not found

**Why empty (rule 8):** no qualifying source names an award; see Field 25 for the sweep and the sources checked.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

**Why empty, rule by rule:**
- **Rule 3 (the developers' own publication about the software):** none exists — see Field 14's ADS searches and controls.
- **Rule 4 (papers the project presents as the basis of the software).** Each shipped recipe names its method references in a `# reference:` header, and the README asks users to cite "the method references each exported notebook lists". Counting the qualifying ones (generic statistics excluded — Page 1954 CUSUM, Rousseeuw & Croux 1993, Efron 1979 bootstrap — and the Baumjohann & Treumann textbook): Sonnerup & Scheible 1998 (MVA), Chapman & Ferraro 1931, Spreiter et al. 1966, Schield 1969, Alken et al. 2021 and Shue et al. 1998 (pressure balance and magnetopause), Jelinek et al. 2012 (bow shock), Rankine 1870 and Hugoniot 1887, Schwartz 1998 (shock normals and Mach numbers), Colburn & Sonett 1966 (coplanarity), Russell et al. 1983 (shock timing), Huttunen-Heikinmaa et al. 2005 (SEP onset), Chree 1913 (superposed epoch), Walén 1944, Sonnerup et al. 1987, Khrabrov & Sonnerup 1998 and Paschmann & Sonnerup 2008 (Walén test), Gieseler et al. 2023 (Solar-MACH, drawn by the optional `solarmach` package), and Möstl et al. 2017 (the ICMECAT catalogue the code reads). That is some twenty papers, each behind a single recipe or helper, and none of them explains the software's purpose — finding, downloading and analysing data by natural-language request. Listed together they would bury any future paper about HelioAI, so, as for PyRFU, none is listed. The README's request to cite the routines' references counts with the rest and is never the rule-4 exception; no README, docs or citation passage presents any one paper as the foundation of the whole package. The retrieval method's references (MiniLM embeddings, BM25, reciprocal rank fusion) are generic methods and are not counted.
- **Rule 5 (substantive uses):** ADS `full:"HelioAI"` returned 0 (controls in Field 14); the software was first released on 2026-08-14 and has no citing literature yet.
- **Not publications here:** PHEP 3 (`10.5281/zenodo.17794207`) is the PyHC support policy HelioAI follows, not a paper about or used by it; the IPShocks paper (Kilpua et al. 2015) and database are cited in `examples/00_quickstart.ipynb` only as independent comparison values.

**Re-check at the next refresh:** a HelioAI or HelioBench paper by the developer (rule 3), or published studies that credit HelioAI in their acknowledgements or data-availability statements (rule 5).

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.6084/m9.figshare.6356420
- https://huggingface.co/datasets/erdoganfurkan/helioai-speasy-index

**Evidence:**
- **HELIO4CAST Interplanetary Coronal Mass Ejection Catalog (ICMECAT)** — `https://doi.org/10.6084/m9.figshare.6356420` (rule 3: a dataset the software is built to read). HelioAI ships a dedicated loader for it (`_HELIO4CAST`, `_fetch_helio4cast_csv`, `_load_helio4cast_catalog` in `helioai/tools/catalog_tools.py`), exposed as `get_catalog('helio4cast/icmecat')`. DataCite: a Figshare dataset whose creators begin Moestl, Davies, Weiler; this unversioned Figshare DOI is the series-level identifier, presenting "HELIO4CAST Interplanetary Coronal Mass Ejection Catalog v2.3" on 2026-11-03 beside per-version DOIs (`.v22`, `.v23` and `.v24` are titled v2.3, earlier ones v2.2 and older). The code fetches the v2.3 file (`HELIO4CAST_ICMECAT_v23.csv`) from helioforecast.space. The DOI resolves to the Figshare article page, which gates automated fetches; DataCite's record is the reliable check. **Re-check:** when HELIO4CAST releases v2.4 the series DOI will present it while the code still reads v2.3 until the URL in `catalog_tools.py` changes; the entry stays, since it identifies the catalogue the code reads.
- **HelioAI speasy parameter index** — `https://huggingface.co/datasets/erdoganfurkan/helioai-speasy-index` (rule 5: a dataset the software produced). The repository's `Index` workflow (`.github/workflows/index.yml`) builds it with `helioai index --rebuild` at every release tag and publishes it to this Hugging Face dataset (`settings.rag.index_repo` default in `helioai/config.py`; card `.github/hf-index-card.md`): the `v0.4.0` snapshot holds 82,702 product descriptions from AMDA, CDAWeb (through its web services and, for 360 MMS and Arase products, its public file tree), the Cluster Science Archive and SSCWeb, with the measurement type and region HelioAI adds and MiniLM embeddings, MIT-licensed, with a git tag per release. It has no DOI; the Hugging Face dataset page, public and not gated, is its permanent landing page. Recorded because it is a data release made with the software and a reader can reuse it; it is also what `helioai index` downloads.

**Considered and not selected:**
- **Archive datasets reached through speasy** (the 82,702 products of the `v0.4.0` index) and **AMDA's shared catalogues** (Richardson & Cane ICMEs, MMS bow-shock crossings, substorm onsets and others) — HelioAI reads them all through one archive-wide path with no dataset-specific reader, so no subset qualifies under rule 3; the archives are recorded in Field 17.
- **IPShocks database** (`https://doi.org/10.5281/zenodo.19730292`) and the **Harvard-CfA Wind shock database** — cited in `examples/00_quickstart.ipynb` as independent comparison values; the software does not read them (rule 2).
- `helioai/data/judged_products.jsonl.gz` — a classification table shipped inside the package and applied when the index is built (`JUDGED_FILE` in `helioai/indexer.py`), with no DOI or landing page of its own (rule 8).

### 29. Related Software (OPTIONAL)
- https://github.com/SciQLop/speasy
- https://github.com/PlasmaPy/PlasmaPy
- https://github.com/tsssss/geopack

All three are catalogue entries; each URL is copied byte for byte from that entry's stored Code Repository value as read on 2026-11-03 (rule 11). Each target also has a concept DOI — speasy `https://doi.org/10.5281/zenodo.4118780`, PlasmaPy `https://doi.org/10.5281/zenodo.6774349`, geopack `https://doi.org/10.5281/zenodo.15110786` (DataCite shows `HasVersion` on each, no `IsVersionOf`) — passed over because the site shows the raw URL as link text (rule 13).

**Evidence (rule 9, a domain-specific dependency whose presence characterises the software):**
- **speasy** — HelioAI's whole data path: `search_parameters` searches HelioAI's index of speasy's inventory, `get_timeseries` and the catalogue tools download through `spz.get_data`, the HELIO4CAST loader builds speasy `Catalog`/`Event` objects, the sandbox pre-imports speasy as `spz`, and exported notebooks fetch through it. The README's "Related projects" names it "the data access layer powering HelioAI".
- **PlasmaPy** — the plasma-parameter tools (`plasma_beta`, `gyrofrequency`, `debye_length`, `alfven_speed`, `inertial_length` in `helioai/tools/plasmapy_tools.py`) delegate their physics to `plasmapy.formulary`, and the sandbox pre-imports it as `pf`; the README's "Related projects" lists it ("plasma physics calculations").
- **geopack** — `transform_coords`, the source of Field 4's magnetospheric coordinate transforms, delegates every rotation to `geopack.geopack` ("Coordinate transforms wrap geopack (MIT, Tsyganenko models port)", `helioai/tools/sandbox_helpers.py`); a required dependency.

**Considered and not selected:**
- **Generic infrastructure (rule 1, Field 30 rules 1–3):** numpy, scipy, matplotlib, pillow, pyyaml, structlog, python-dotenv, httpx/httpx2, fastapi, uvicorn, chromadb, rank-bm25, sentence-transformers, torch, huggingface-hub, the LLM SDKs (`openai`, `google-genai`), `mcp`, nbformat, ipykernel and ipywidgets — each would be equally at home outside heliophysics; being a dependency is not a relation.
- **astropy** (Tier B) — used for `astropy.units` in the sandbox and by PlasmaPy; no documented package-specific exchange (rule 2).
- **solarmach** — recorded in Field 30, where its documented integration is the ground; it has no separate Field 29 ground (rule 3).
- **SciQLop** — recorded in Field 30: HelioAI's documented catalogue handoff to it is the only relationship, and that relation belongs in Field 30 alone (rule 3; Field 30 rule 9).
- **SunPy** — listed in the docs home page's "It uses" table ("units, time, solar context"), but HelioAI's code imports it nowhere and does not declare it as a dependency; it arrives only inside the optional `solarmach` stack (the `solar_mach` recipe's docstring calls it a "heavy sunpy stack"). Not a domain dependency of this distribution, so rule 9 does not fire.
- **AMDA, CDAWeb, the Cluster Science Archive and SSCWeb** — data services, recorded in Field 17 (rule 5).
- **Claude Code, Claude Desktop, Codex** — general AI coding clients HelioAI can be installed into as an MCP server; generic tools (rule 1). The same holds for the MCP servers HelioAI's own MCP client can consume (`helioai/tools/mcp_client.py`'s configuration examples name an ADS and an alphaXiv server).
- **Similar-purpose tools, predecessors, companions:** the project's README, docs and `CITATION.cff` name no alternative or equivalent software and no predecessor, and GitHub reports the repository is not a fork. The packages they do name are dependencies (README "Related projects": speasy, PlasmaPy and the PyHC community itself; the docs home page's "It uses" table: speasy, PlasmaPy, geopack, Astropy, SunPy) and SciQLop, which `CONTRIBUTING.md` names as the tool HelioAI interoperates with rather than competes with — not a similar-task claim (rule 6); Field 30 carries it.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/jgieseler/solarmach
- https://github.com/SciQLop/SciQLop
- https://github.com/ipython/ipython

**Evidence (rule 7, and rule 4 for the Tier B entry):**
- **solarmach** — a documented integration with a named domain tool: the optional extra `solarmach = ["solarmach>=0.5"]` in `pyproject.toml`, the shipped `solar_mach` recipe, which hands the session's date, observers and solar-wind speeds to solarmach's `SolarMACH`, returns its Parker-spiral connectivity figure and coordinate table to the session (and so to the exported notebook), the installation docs' extras table ("Parker spiral connectivity figures") and the recipes guide, and tests (`tests/recipes/test_shipped_recipes.py` runs it when solarmach is installed; `tests/test_recipes.py` checks the graceful message without it). The URL is the catalogue entry's stored Code Repository value, copied byte for byte (Field 29 rule 11); its concept DOI `https://doi.org/10.5281/zenodo.7016783` was passed over because the site shows the raw URL (Field 29 rule 13).
- **SciQLop** — a documented export-to-import handoff (rule 7: one package's output imported into the other). `save_catalog` writes a user's detected events as a catalogue file (`helioai/tools/catalog_tools.py`; `CatalogsConfig` in `helioai/config.py` describes the directory as "Where user-saved event catalogs are written, in speasy format."), and the project documents that these catalogues open in SciQLop: the docs home page says an event set detected in HelioAI opens directly in SciQLop for visual inspection, `docs/guide/tools.md` that catalogs saved with `save_catalog` "open directly in SciQLop for visual checking", and `CONTRIBUTING.md` assigns interactive visual exploration to SciQLop, adding "HelioAI interoperates with it (catalogs are written in the standard `speasy` format) rather than competing". The URL is the catalogue entry's stored Code Repository value as read on 2026-11-03, copied byte for byte (Field 29 rule 11); its concept DOI `https://doi.org/10.5281/zenodo.7379012` was passed over because the site shows the raw URL (Field 29 rule 13). Not also in Field 29: the handoff is the only relationship (rule 9).
- **IPython / Jupyter** — Jupyter is Tier B, admitted only with "an extension, kernel, widget or rich display written for it". HelioAI ships exactly that: an IPython extension (`%load_ext helioai.interfaces.jupyter_magic`, documented in the README) registering the `%%helioai` cell magic and the `%helioai_session`, `%helioai_provider`, `%helioai_history`, `%helioai_resume`, `%helioai_export` and `%helioai_dev` line magics through `IPython.core.magic`, and rendering parameter cards and catalogue cards as rich HTML, figures as `IPython.display.Image`, and answers as Markdown (`helioai/interfaces/jupyter_magic.py`); the package also declares the `Framework :: Jupyter` classifier. The extension is written against IPython's magic and display API, and Jupyter front ends run Python through the IPython kernel (`ipykernel`, a declared dependency), so the upstream repository recorded is IPython's (`https://github.com/ipython/ipython`; not a catalogue entry as of 2026-11-03; no concept DOI found at Zenodo or DataCite). JupyterLab (`https://github.com/jupyterlab/jupyterlab`, the form SciQLop's record uses because SciQLop embeds JupyterLab) and the classic Notebook were considered and not used: HelioAI's magics are not specific to either front end.

**Considered and not selected:**
- **speasy** — HelioAI builds speasy `Catalog`/`Event` objects and calls speasy for every download, but that is HelioAI using its data layer, recorded in Field 29 under that ground; listing the same URL here as well would show one fact twice (rule 9).
- **PlasmaPy, geopack** — called as libraries; recorded in Field 29.
- **Claude Code, Claude Desktop, Codex (MCP clients)** — `helioai mcp-install` writes their MCP configuration so they can call HelioAI's tools, but they are general-purpose AI coding agents, not heliophysics or science tools (rule 2).
- **Tier A and generic packages** — see Field 29.

### 31. Related Instruments (OPTIONAL)
Not found

**Why empty (Stage A, rule 2):** HelioAI is an archive-wide client: the user names the mission and instrument at run time, and the same search, download and analysis path serves every product of the archives speasy reaches (Field 17). Instruments appear only as examples (the README's Wind magnetic-field session `cda/WI_H0_MFI/B3F1`, ACE in the Jupyter example, MMS FGM in the plotting skill's hodogram template, instrument tables in the parameter-hunter skill) and in archive-wide lookup tables that treat every mission alike (`_SPACECRAFT_REGION` in `helioai/indexer.py`). Listing the examples' instruments would imply a specialisation the software does not have (rules 2–3). Product identifiers of particular instruments do occur in the package (`WI_H1_SWE`, `WI_H0_MFI`, `AC_H2_SWE`, `MMS1_FGM_SRVY_L2` and others), but a sweep finds them only in docstrings, comments and examples that illustrate archive-wide behaviour; no code path is written for one instrument's data.

**Vocabulary sweep (production `InstrumentObservatory`, fetched whole on 2026-11-03, every row's identifier SPASE):** the example instrument resolves cleanly — `Wind Magnetic Field Investigation`, `https://spase-metadata.org/SMWG/Instrument/Wind/MFI` (with a CNES/CDPP-AMDA twin, `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Wind/MFI`) — and is deliberately not used: the decision is relevance, not lookup. Sweeps of `name`, `abbreviation`, `identifier` and `definition` for `HelioAI` and `speasy` return no row; negative control `xylophonic` returns 0; positive control `Wind` among observatories returns `ISTP/Wind` (`https://spase-metadata.org/SMWG/Observatory/Wind`) and its CNES twins.

### 32. Related Observatories (OPTIONAL)
Not found

**Why empty:** the same archive-wide reasoning as Field 31 (Stage A, rule 2, applied with type 2). The README's data-coverage table names example missions per provider (Cluster, MMS, Solar Orbiter, WIND, ACE, Cassini, Helios, STEREO, THEMIS, Van Allen Probes, Parker Solar Probe, Ulysses, Voyager, Double Star, Mars Express) as illustrations of what the archives hold, not as missions the software is built for; the HELIO4CAST ICMECAT reader is a catalogue reader, and the catalogue's own spacecraft are its content, not HelioAI's support. The rows for the headline example's spacecraft — `ISTP/Wind` (`https://spase-metadata.org/SMWG/Observatory/Wind`) and `Advanced Composition Explorer` (`https://spase-metadata.org/SMWG/Observatory/ACE`) — exist and are deliberately not used. Field 17 accordingly carries no `Observatory/Mission-specific` (Field 32 rule 6).

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/erdoganfurkan/HelioAI/e45edbb62162a2de2aa024e003755a1b9d252cd4/docs/assets/logo/helioai-icon.png

**Source:** Rules 2–3 and 7. The project presents two images as its logo, both added in `74ddb21` ("feat: the HelioAI logo, in the README, the docs and the web UI"):
- **`docs/assets/logo/helioai-icon.png`** — the documentation theme's logo option (`mkdocs.yml` `theme.logo: assets/logo/helioai-icon.png`), shown in the documentation site's header. Under rule 3 the docs logo outranks a README header, so it is the value. It is a 180×180 square emblem: a glowing yellow-orange sun inside a blue orbital ring with one small blue sphere on the ring, on a dark rounded square — a mark that reads well beside the name on the detail page and result card.
- **`docs/assets/logo/helioai-logo-light.png`** (530×215), with `helioai-logo-dark.png` for dark mode — the README's header image (`<picture>` at the top of the README) and the docs home page's banner: the wordmark "HelioAI" with the same sun-in-ring device replacing the "o", orbital arcs, and the tagline "HELIOPHYSICS AGENT". Recorded as the alternative; its pinned URL is `https://raw.githubusercontent.com/erdoganfurkan/HelioAI/e45edbb62162a2de2aa024e003755a1b9d252cd4/docs/assets/logo/helioai-logo-light.png` (serves `image/png`, 18,608 bytes).

**Verification (2026-11-03):** the recorded URL serves `image/png` — 8,105 bytes, a 180×180 PNG byte-identical (SHA-256) to the blob tracked at the pinned commit — showing the emblem described above. The path is not Git-LFS-tracked (the repository has no `.gitattributes`). The URL is pinned to the 40-hex source revision (no branch, no `blob/` segment) and is 130 characters long. The README's own image URLs point at `.../main/...`, a branch reference, so they were re-derived to the pinned form (rule 7). The PyHC registry entry has no `logo:` field.

**Not used:** `docs/assets/logo/favicon.png` (32×32 favicon) and `helioai/interfaces/web/static/icon.png` (the web UI's icon); `docs/assets/web-demo.gif`, `docs/assets/demo.gif` and `docs/assets/shock-analysis.png` are demonstration recordings and an example figure, not logos (rule 4).
