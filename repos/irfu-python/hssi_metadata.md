# HSSI Metadata Extraction Results

**HSSI Software ID:** bdd706f0-b987-446b-b650-78d9d86f00b2
**Repository:** https://github.com/louis-richard/irfu-python
**Source Revision:** 40505b6a6e69c6c6ade8ff57062fbb21f23734b8
**Extraction Date:** 2026-07-26
**Validation Date:** 2026-07-27
**Validation Status:** PASS — full 33-field validation (1 ERROR, 9 WARNINGS, 15 SUGGESTIONS, 25 PASSED); the ERROR and every actionable finding resolved; all 9 user decisions incorporated and the changed fields re-checked against the live controlled vocabularies.
**Applied to HSSI:** 2026-07-27 — `PATCH http://localhost/api/data/software/bdd706f0-b987-446b-b650-78d9d86f00b2/` returned HTTP 200 `status: ok` with 16 `fieldsUpdated`. Every changed field was roundtrip-verified against the view API and, for the fields the view API hides or reshapes, against the database. The 16 untouched fields were confirmed byte-identical to the pre-PATCH baseline. Fields 2–33 of this file match the live HSSI record.

**Extraction mode:** SEEDED. Baseline = union of (a) live HSSI record `GET http://localhost/api/view/software/bdd706f0-b987-446b-b650-78d9d86f00b2/` and (b) the prior canonical `hssi_metadata.md` (extracted 2025-10-09). Live HSSI is authoritative for scalar conflicts unless authoritative current evidence shows the live value is stale/incorrect; every such override is called out explicitly under its field. Multi-valued fields are set unions.

**Source revision context:** `master` HEAD `40505b6a6e69c6c6ade8ff57062fbb21f23734b8` (2026-02-27, "Bump version 2.4.20 -> 2.4.21") is also the `v2.4.21` tag commit; verified against `GET https://api.github.com/repos/louis-richard/irfu-python/branches/master`. (`pushed_at` on the repo is later only because of the unreleased `devel` branch.)

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]
- **Note:** Not exposed by the HSSI view API; unchanged from the prior canonical file. Placeholder.

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.10678694
- **Note:** Unchanged. Zenodo **concept** DOI (all versions). Confirmed live on 2026-07-26 via `GET https://api.datacite.org/dois/10.5281/zenodo.10678694`. From existing HSSI record + prior canonical file + DataCite.

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/louis-richard/irfu-python
- **Note:** Unchanged. Confirmed HTTP 200; matches `pyproject.toml [project.urls] source`, `CITATION.cff repository-code`, Zenodo `code:codeRepository`, and the PyHC registry `code` field.

### 4. Software Functionality (MANDATORY)

**Final value (39 entries — set union of live HSSI (25) + prior canonical file (26) + 13 newly evidenced values; every child's parent category is present):**

- Coordinate Transforms
- Coordinate Transforms:Magnetospheric
- Coordinate Transforms:Mission-Specific
- Data Processing and Analysis
- Data Processing and Analysis:2D Slices
- Data Processing and Analysis:3D Particle Distribution Processing
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Curlometer
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:Energy Spectra
- Data Processing and Analysis:Linear Gradient Estimation
- Data Processing and Analysis:Pitch Angle Distributions
- Data Processing and Analysis:Plasma Moments
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Spectrogram
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:Wave Polarization Analysis
- Data Processing and Analysis:Wavelet Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:2D Slices
- Data Visualization:3D Graphics
- Data Visualization:Hodograms
- Data Visualization:Line Plots
- Data Visualization:Orbit Plots
- Data Visualization:Spacecraft Formation Plots
- Data Visualization:Spectrogram
- Mission-related
- Mission-related:Analysis
- Mission-related:Calibration
- Mission-related:Distribution/Access
- Models and Simulations
- Models and Simulations:Empirical
- Models and Simulations:Field-line Tracing
- Models and Simulations:Instrument Response
- Models and Simulations:Physics-Based
- Models and Simulations:Theory

**Note (provenance):** All 25 live-HSSI values are retained. The `Parent:Child` values are written here without a space after the colon, matching the `hssi-field-definitions` allowed-value list; live HSSI and the `submission-payload`/`update-payload` skills use the equivalent `Parent: Child` form with a space. **The two forms are the same value** — the graph-list parser strips surrounding whitespace — so this is purely presentational (validation finding S7). A diff must NOT treat the 25 retained values as changed on colon spacing alone; the real delta for Field 4 is the 14 additions listed below, not 39 replacements.

**File-only value restored (1):** `Data Processing and Analysis:Wavelet Analysis` is present in the prior canonical file but **absent from live HSSI**. It is retained under the union rule because the evidence is unambiguous: `pyrfu/pyrf/wavelet.py` implements a continuous wavelet transform (Morlet), `pyrfu/pyrf/compress_cwt.py` compresses CWT output, and `pyrfu/pyrf/ebsp.py` performs wavelet-based E/B spectral analysis — all three are exported in `pyrfu/pyrf/__init__.py` `__all__`. The live record's other 25 values are a subset of the canonical file's 26.

The following **13 values are new**, each with code evidence at revision `40505b6a`:

| New value | Evidence (revision 40505b6a) |
|---|---|
| `Data Processing and Analysis:2D Slices` | `pyrfu/mms/vdf_projection.py` ("Compute the projection of the velocity distribution onto a specified plane"), `pyrfu/mms/reduce.py` ("Reduces (integrates) 3D distribution to 1D (line) or 2D (plane)"), `pyrfu/mms/vdf_reduce.py` |
| `Data Processing and Analysis:Data Reduction` | `pyrfu/mms/reduce.py`, `pyrfu/mms/psd_rebin.py`, `pyrfu/mms/eis_spin_avg.py`, `pyrfu/mms/feeps_spin_avg.py`, `pyrfu/mms/hpca_spin_sum.py`, `pyrfu/pyrf/mean_bins.py`, `pyrfu/pyrf/median_bins.py`, `pyrfu/pyrf/waverage.py`, `pyrfu/pyrf/movmean.py` |
| `Data Visualization:2D Slices` | `pyrfu/plot/plot_projection.py`, `pyrfu/plot/plot_reduced_2d.py` (both exported in `pyrfu/plot/__init__.py`) |
| `Data Visualization:3D Graphics` | `pyrfu/plot/plot_surf.py` (`axis.plot_surface(...)`), `pyrfu/plot/mms_pl_config.py` (`fig.add_subplot(..., projection="3d")`) |
| `Data Visualization:Hodograms` | `pyrfu/pyrf/mva_gui.py` — interactive minimum-variance GUI whose panels are explicitly "Min/Max hodogram", "Interm/Max hodogram", "B3/B1 hodogram", "B2/B1 hodogram"; exported as `mva_gui` in `pyrfu/pyrf/__init__.py` `__all__` |
| `Data Visualization:Spacecraft Formation Plots` | `pyrfu/plot/mms_pl_config.py` — "Plot spacecraft configuration with three 2d plots of the position in Re and one 3d plot of the relative position of the spacecraft" |
| `Mission-related:Calibration` | MMS-instrument-specific calibration/correction routines: `pyrfu/mms/feeps_flat_field_corrections.py`, `feeps_correct_energies.py`, `feeps_remove_sun.py`, `feeps_remove_sunlit_sectors.py`, `feeps_remove_bad_data.py`, `eis_proton_correction.py`, `correct_edp_probe_timing.py`, `remove_edist_background.py`, `remove_idist_background.py`, `remove_imoms_background.py` |
| `Models and Simulations` (parent) | Required parent for the four children below |
| `Models and Simulations:Empirical` | `pyrfu/models/igrf.py` (IGRF-13 empirical geomagnetic field, coefficients in `igrf13coeffs.csv`), `pyrfu/pyrf/magnetosphere.py` (Shue+1998 magnetopause and bow-shock models), `pyrfu/models/magnetopause_normal.py`, `pyrfu/models/ion_anisotropy_thresh.py` |
| `Models and Simulations:Field-line Tracing` | `pyrfu/plot/plot_magnetosphere.py` calls `geopack.trace(...)` twice to trace model field lines (`_add_field_lines`) |
| `Models and Simulations:Instrument Response` | `pyrfu/lp/` — `LangmuirProbe` class plus `photo_current.py` (per-surface-material photoemission current densities) and `thermal_current.py` model Langmuir-probe/spacecraft-potential instrument response; `pyrfu/mms/make_model_vdf.py`, `make_model_kappa.py` synthesize instrument-frame model distributions |
| `Models and Simulations:Physics-Based` | `pyrfu/dispersion/one_fluid_dispersion.py`, `pyrfu/mms/make_model_kappa.py`, `pyrfu/mms/make_model_vdf.py`, `pyrfu/lp/thermal_current.py` |
| `Models and Simulations:Theory` | `pyrfu/dispersion/disp_surf_calc.py` + `one_fluid_dispersion.py` (analytic plasma dispersion-relation solvers; `docs/examples/02_dispersion/`); corroborated by the PyHC registry keyword `theory` |

**Note (considered and rejected):** `Data Processing and Analysis:File Format Conversion` — `psd2def`/`psd2dpf`/`def2psd`/`dpf2psd` convert particle *units*, not file formats. `Data Processing and Analysis:Image Processing`, `:ML/AI`, `:Packet Decommutation`, `:Data Assimilation`, `:Magnetic Null Finding`, `:Field-line Tracing` — no implementation found. `Data Visualization:Movies`/`:Web-Based` — no `matplotlib.animation`, `plotly` or `bokeh` usage. `Servers and Environments*` — no container, server, or HPC/MPI code in the repository. `Coordinate Transforms:Heliospheric`/`:Planetary`/`:Solar` — `pyrfu/pyrf/cotrans.py` supports only geocentric systems (`geo/gei/gse/gsm/sm/mag` plus `dipoledirectiongse`); the Solar Orbiter and MAVEN modules perform no coordinate transforms.

### 5. Related Region (MANDATORY)
- **Earth Magnetosphere**
- **Interplanetary Space**
- **Planetary Magnetospheres**

**Note:** Unchanged (identical in live HSSI and the prior canonical file). Re-verified: Earth Magnetosphere — the whole `pyrfu/mms/` package (91 modules) plus `pyrf/magnetosphere.py`, `models/magnetopause_normal.py`, `models/igrf.py`, `pyrf/l_shell.py`; Interplanetary Space — `pyrf/get_omni_data.py` (solar-wind/IMF), `pyrf/shock_normal.py`, `shock_parameters.py`, `docs/examples/01_mms/example_mms_ipshocks.ipynb`, `example_mms_walen_test.ipynb`, and `pyrfu/solo/` (Solar Orbiter RPW in the inner heliosphere); Planetary Magnetospheres — `pyrfu/maven/` (Mars). `Solar Environment` and `Earth Atmosphere` deliberately not selected: nothing in the package works with solar-disk/coronal or neutral-atmosphere data.

### 6. Authors (MANDATORY)

Six person authors, matched by ORCID across live HSSI, the prior canonical file, `CITATION.cff`, DataCite and Zenodo — all three sources agree. Affiliations are the identity-aware union (matched by ROR); the live HSSI affiliation UUIDs were resolved via `GET http://localhost/api/models/Organization/rows/all/` and are identical to the prior canonical file's organizations.

#### Author 1
- **Name:** Louis Richard
- **Author Identifier:** https://orcid.org/0000-0003-3446-7322
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11
- **Affiliation:**
  - **Organization:** Uppsala University
  - **Affiliation Identifier:** https://ror.org/048a87296

#### Author 2
- **Name:** Yuri V. Khotyaintsev
- **Author Identifier:** https://orcid.org/0000-0001-5550-3113
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Author 3
- **Name:** Andris Vaivads
- **Author Identifier:** https://orcid.org/0000-0003-1654-841X
- **Affiliation:**
  - **Organization:** KTH Royal Institute of Technology
  - **Affiliation Identifier:** https://ror.org/026vcq606
- **Affiliation:**
  - **Organization:** Ventspils University of Applied Sciences
  - **Affiliation Identifier:** https://ror.org/03sc6wx59

#### Author 4
- **Name:** Daniel B. Graham
- **Author Identifier:** https://orcid.org/0000-0002-1046-746X
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Author 5
- **Name:** Cecilia Norgren
- **Author Identifier:** https://orcid.org/0000-0002-6561-2337
- **Affiliation:**
  - **Organization:** Swedish Institute of Space Physics
  - **Affiliation Identifier:** https://ror.org/043kppn11

#### Author 6
- **Name:** Andreas Johlander
- **Author Identifier:** https://orcid.org/0000-0001-7714-1870
- **Affiliation:**
  - **Organization:** Swedish Defence Research Agency
  - **Affiliation Identifier:** https://ror.org/0470cgs30

#### Candidate additional author (organization) — NEEDS USER DECISION, do not submit without approval
- **Name:** PyRFU team
- **Author Identifier:** Not found (no ROR)
- **Affiliation:** Not found
- **Note:** `CITATION.cff` at revision `40505b6a` lists a **seventh, organization-style author** as its *first* entry: a bare `- name: "PyRFU team"` with no `given-names`/`family-names`, which is the CFF convention for an entity author. It is absent from live HSSI, from the prior canonical file, and from both the DataCite and Zenodo creator lists (which contain only the six people). A ROR lookup (`https://api.ror.org/organizations?query=PyRFU+team`) finds no institution — "PyRFU team" is a project team, not a registered organization, so there is no identifier to attach and HSSI would have no way to infer org-ness. Recorded here so the finding is not lost; recommend **not** adding it unless the maintainer confirms, since an identifier-less group author adds little and DataCite/Zenodo (the citation of record) omit it.

**Note (author-name provenance):** Live HSSI splits names into `givenName`/`familyName`; the display forms above match the prior canonical file and DataCite exactly. No renames are proposed. `CITATION.cff` uses the shorter given names "Yuri" and "Daniel"; DataCite/Zenodo/live HSSI use "Yuri V." and "Daniel B." — the fuller DataCite/live forms are kept.

### 7. Software Name (MANDATORY)
- **Value:** PyRFU
- **Note:** **Live HSSI value preserved deliberately.** The prior canonical file said `Python RymdFysik Utilities (PyRFU)`; that is the DataCite/Zenodo *record title* ("Python RymdFysik Utilities (PyRFU): An Open-Source Python Package for Advanced In-Situ Space Plasma Analysis"), not the name the software goes by. Repository evidence supports the short form: `pyproject.toml name = "pyrfu"`, `CITATION.cff title: "pyrfu"`, the README heading `pyRFU`, and the PyHC registry entry `name: PyRFU`. Field 7 asks for "the name of the software package as listed on the code repository". Discrepancy noted rather than silently renamed; **no change proposed**.

### 8. Description (MANDATORY)
**Value:**
PyRFU is a free and open-source Python package for advanced analysis of in-situ space plasma data. It provides routines to work with space data, particularly with Magnetospheric Multiscale (MMS) mission data, as well as MAVEN and Solar Orbiter missions. The package includes general plasma physics routines for coordinate transformations, particle distribution analysis, plasma moments calculations, wave analysis (including polarization and wavelets), multi-spacecraft techniques (curlometer, gradient estimation), and comprehensive data visualization capabilities. PyRFU is based on the IRFU-MATLAB library and supports data retrieval from multiple sources including local files, MMS Science Data Center, MAVEN Science Data Center, and cloud storage (AWS S3). The package additionally provides analytic plasma dispersion-relation solvers, Langmuir-probe and spacecraft-potential current models, and empirical field and boundary models including IGRF-13 and the Shue et al. (1998) magnetopause and bow shock.

- **Note:** **The live HSSI text is preserved verbatim and unaltered**; a single sentence has been **appended** by user decision (2026-07-27), per validation finding S14. Every claim in the original was re-verified at revision `40505b6a`, and no existing wording was edited, reordered, or removed — the original editorial intent is intact.
- **Evidence for the appended sentence:** it covers three of PyRFU's six subpackages that the original text omitted entirely. Dispersion-relation solvers — `pyrfu/dispersion/one_fluid_dispersion.py` and `disp_surf_calc.py` (`optimize.fsolve` on analytic dispersion relations), with two example notebooks in `docs/examples/02_dispersion/`. Langmuir-probe / spacecraft-potential current models — `pyrfu/lp/` (`LangmuirProbe` class, `photo_current.py`, `thermal_current.py`, all exported in `pyrfu/lp/__init__.py` `__all__`), plus `pyrfu/mms/scpot2ne.py`. Empirical field and boundary models — `pyrfu/models/igrf.py` (IGRF-13, coefficients in `igrf13coeffs.csv`), `pyrfu/pyrf/magnetosphere.py` (`model="mp_shue1998"` and bow shock), `pyrfu/models/magnetopause_normal.py`. Validation identified this as the largest single completeness gain available in a mandatory field.

### 9. Concise Description (OPTIONAL)
- **Value:** PyRFU is a free and open-source Python package for advanced analysis of in-situ space plasma data.
- **Length:** 98 characters (within the 200-character limit)
- **Note:** **Live HSSI value preserved.** It is also the exact `description` string in the PyHC community registry (the most trustworthy curated source), so it is doubly supported. The prior canonical file had a different, longer 197-character sentence ("A Python package for advanced analysis of in-situ space plasma data, particularly for MMS, MAVEN, and Solar Orbiter missions, with comprehensive tools for particle distributions, waves, and plasma physics."); that is a stylistic alternative only and is **not** proposed as a replacement.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2020-11-27
- **Note:** **OVERRIDES live HSSI's `2024-02-19` by user decision (2026-07-27), per validation finding W6.** Field 10 is defined as "date of first broadcast/publication … used for the initial version of the software". PyRFU's genuine first public release was **2020-11-27** — PyPI `pyrfu` 1.8.3, `upload_time_iso_8601 = 2020-11-27T09:59:36.830283Z`, the earliest of 100 releases. The prior value `2024-02-19` is the DataCite `dates[] dateType="Issued"` for concept DOI `10.5281/zenodo.10678694`, i.e. the date the Zenodo deposit (capturing v2.4.12) was published — a DOI-record date, not the software's first publication, and an artifact of how HSSI's DOI-driven autofill populates this field. Corroborating: `LICENSE.txt` reads "Copyright (c) 2020"; `pyrfu/__init__.py` reads `Copyright 2020-2026`. The prior canonical file also carried the stale `2024-02-19`.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Note:** **Live HSSI value preserved** (HSSI Organization row `ee990b81-8115-4ab4-8a7f-68a4d0bb345d`, `name: "Zenodo"`, `identifier: "https://zenodo.org"`). DataCite `publisher` = "Zenodo". The prior canonical file used the ROR `https://ror.org/04t3en479` instead; Field 11 permits "ROR identifier when available or URL otherwise (e.g., https://zenodo.org)", and the live value matches the field definition's own example and the existing HSSI organization row, so **no change is proposed** (changing it would risk duplicating the Zenodo organization).

### 12. Version (RECOMMENDED)

#### Version Number
- **Value:** v2.4.21
- **Note:** **OVERRIDES live HSSI, which is stale.** Live HSSI returns `version: ["PyRFU - v2.4.12"]` (i.e. stored version number `v2.4.12`, rendered by the view API as `<softwareName> - <versionNumber>`). Evidence that v2.4.21 is current as of 2026-07-26: (1) `pyproject.toml` at revision `40505b6a` has `version = "2.4.21"` and `[tool.bumpver] current_version = "2.4.21"`; (2) git tag `v2.4.21` points at `40505b6a`, and it is the newest of 19 tags (`git for-each-ref --sort=-creatordate`); (3) `GET https://api.github.com/repos/louis-richard/irfu-python/branches/master` → `40505b6a…`, so the tag is HEAD of the default branch; (4) PyPI `pyrfu` `info.version = "2.4.21"`, uploaded `2026-02-27T17:03:52Z`, the latest of 100 releases; (5) GitHub release `v2.4.21` published `2026-02-27T17:03:34Z`. The prior canonical file also said `v2.4.12` and is equally stale.

#### Version Date
- **Value:** 2026-02-27
- **Note:** **OVERRIDES the prior canonical file's `2024-02-15`** (which was the `v2.4.12` tag date); live HSSI returns no separate version date. Evidence: git tag `v2.4.21` creator date `2026-02-27`; commit `40505b6a` committed `2026-02-27T16:52:06Z`; GitHub release published `2026-02-27T17:03:34Z`; PyPI upload `2026-02-27T17:03:52Z`. All four agree.

#### Version Description
- **Value:** Version 2.4.21 adds new features and bug fixes across the generic and MMS subpackages. New features: `pyrfu.pyrf.filt` now supports tensors; `pyrfu.pyrf.pid_4sc` adds error propagation; `pyrfu.mms.tokenize` adds keys for loading FPI-DIS moment errors and FPI-DES temperature errors; and `pyrfu.mms.fk_power_spectrum_4sc` now also returns the mean and standard deviation of the wave vector and frequency. Bug fixes: `pyrfu.pyrf.calc_dt` corrects time-precision handling, and `pyrfu.pyrf.int_sph_dist` corrects index handling at bin edges.
- **Note:** **OVERRIDES the prior canonical file** (which described v2.4.12). Composed from the official GitHub release notes for tag `v2.4.21` (`GET https://api.github.com/repos/louis-richard/irfu-python/releases`), cross-checked against the 66 commits in `git log v2.4.20..v2.4.21` (e.g. "enable handling tensors", "simplify pid_4sc and add error propagation", "add keys for FPI-DIS moments errors and FPI-DES temperature errors", "add output of mean and standard deviation of the wave vector and frequency", "fix calculation of the sampling frequency to avoid loosing precision", "fix indexing in searchsorted").

#### Version PID
- **Value:** Not found
- **Note:** **This is a deliberate correction — the prior canonical file's `https://doi.org/10.5281/zenodo.10678695` must NOT be carried forward as the PID of v2.4.21.** Verified on 2026-07-26: `GET https://api.datacite.org/dois/10.5281/zenodo.10678694` (concept DOI) still reports `version: "2.4.12"`, `dates: [{date: "2024-02-19", dateType: "Issued"}]`, and exactly **one** `relatedIdentifiers` entry — `{relationType: "HasVersion", relatedIdentifier: "10.5281/zenodo.10678695"}`. `GET https://zenodo.org/api/records/10678695` reports `metadata.version = "2.4.12"` and `publication_date = "2024-02-19"`. (An earlier draft of this note also cited `relations.version[0].is_last = true`; that citation is withdrawn per validation finding S9 — the field comes back as an empty list on re-query. The conclusion is unaffected and independently confirmed: `GET https://zenodo.org/api/records?q=pyrfu` returns exactly one record, 10678695 at version 2.4.12.) Zenodo archiving stopped at v2.4.12, so **no version-specific DOI exists for v2.4.21**. `CITATION.cff` still pins `doi: 10.5281/zenodo.10678695` and the README DOI badge still points at it, but both refer to the v2.4.12 deposit. Recommend telling the maintainer to re-enable the GitHub–Zenodo integration; until then this sub-field is legitimately empty. (Live HSSI returns no version PID, so this is not an override of a live value.)

### 13. Programming Language (RECOMMENDED)
- **Value:** Python 3.x
- **Note:** Unchanged (live HSSI + prior canonical file). Only `Python 3.x` is an allowed value; the specific supported minor versions are 3.10–3.14 (`pyproject.toml requires-python = ">=3.10,<3.15"` and classifiers `Programming Language :: Python :: 3.10` through `3.14`, plus `3 :: Only`). This is broader than the prior canonical file's note (3.10–3.12) — v2.4.18 "Enable compatibility with python 3.13 and 3.14". GitHub reports `language: Python`; SoMEF reports Python only (1,012,181 bytes).

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found
- **Note:** No paper describes PyRFU. Confirmed by: no `IsDescribedBy` / `IsSupplementTo` publication in the concept DOI's `relatedIdentifiers`; `CITATION.cff` has no `preferred-citation` and points only at the software DOI; the README "Acknowledgement" section asks users to cite the repository URL, not a paper ("Data analysis was performed using the pyrfu analysis package available at https://github.com/louis-richard/irfu-python"); no JOSS or other software paper found by web search. Live HSSI is also empty here, so this remains legitimately unfilled.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://opensource.org/licenses/MIT
- **Note:** **NEWLY FILLED** — live HSSI returns no license. Four independent sources agree: (1) `LICENSE.txt` at revision `40505b6a` begins "MIT License / Copyright (c) 2020 L. RICHARD"; (2) DataCite `rightsList` = `{rights: "MIT License", rightsUri: "https://opensource.org/licenses/MIT", rightsIdentifier: "mit", rightsIdentifierScheme: "SPDX", schemeUri: "https://spdx.org/licenses/"}`; (3) `pyproject.toml` `license = { file = "LICENSE.txt" }` plus classifier `License :: OSI Approved :: MIT License`; (4) GitHub API `license = {key: "mit", name: "MIT License", spdx_id: "MIT"}`. "MIT License" is the exact SPDX title and an allowed Field 15 option. README also states "It is distributed under the open-source MIT license." Matches the prior canonical file.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Final value (44 keywords — set union of the 22 live-HSSI keywords + 15 newly evidenced controlled-vocabulary terms + `data analysis` restored per validation W2 + 6 added by user decision per validation S4).** All 44 exist as rows in the HSSI `Keyword` vocabulary (re-verified 2026-07-27 against `GET http://localhost/api/models/Keyword/rows/all/`). Recorded in the vocabulary's stored form — note `Langmuir probes` carries a capital L in the vocabulary and is recorded that way; `GET /api/view/software/<uid>/` renders keywords Title Case for display (e.g. stored `mms` is shown as `Mms`), so the apparent case difference from the live JSON is presentational only.

**Added by user decision 2026-07-27 (validation S4), each in-vocabulary and repo-evidenced:** `Langmuir probes` (the whole `pyrfu/lp/` subpackage — `LangmuirProbe`, `photo_current.py`, `thermal_current.py`) · `igrf13` (`pyrfu/models/igrf.py` + bundled `igrf13coeffs.csv`) · `shue` (`pyrfu/pyrf/magnetosphere.py` `model="mp_shue1998"`) · `l shell` (`pyrfu/pyrf/l_shell.py`, exported) · `istp` (the ISTP attribute dependence documented in Field 18) · `energetic particles` (EIS + FEEPS, 28 modules).

**Not created (user decision):** `magnetic reconnection` and `turbulence` are strongly evidenced but are **not** rows in the vocabulary (confirmed absent from all 536 rows), and creating new vocabulary rows was declined for this record.

- calibration
- cdf
- coordinate transformations
- coordinates
- data access
- data analysis
- data retrieval
- data visualization
- energetic particles
- heliosphere
- igrf13
- in situ measurements
- instrumentation
- istp
- l shell
- Langmuir probes
- line plots
- magnetosphere
- maven
- mms
- multidimensional
- omni
- orbit
- pitch angle distributions
- planetary
- plasma parameters
- plasma physics
- plotting
- power spectra
- python 3
- shock waves
- shue
- solar orbiter
- solar wind
- space physics
- space plasma
- spectra
- spectrograms
- theory
- time
- time series
- velocity distribution functions
- wave polarization
- wavelet analysis

**Retained from live HSSI (22):**
coordinates · data access · data retrieval · heliosphere · instrumentation · line plots · magnetosphere · maven · mms · multidimensional · omni · orbit · planetary · plasma physics · plotting · power spectra · python 3 · solar orbiter · space physics · spectra · theory · time

*(Origin: the PyHC registry keyword list for PyRFU — `heliosphere, magnetosphere, planetary, plasma_physics, coordinates, data_retrieval, line_plots, multidimensional, orbit, plotting, power_spectra, spectra, time, general, local, remote, web_service, data_access, data_analysis, instrumentation, theory, maven, mms, omni, solo` — plus the GitHub topics `python3`, `space-physics`. Re-fetched 2026-07-26 and unchanged. Note that the live HSSI set drops PyHC's `data analysis` … see below.)*

**Newly added (15), each in-vocabulary and repo-evidenced:**

| Keyword | Evidence |
|---|---|
| in situ measurements | README/PyHC/description core framing: "advanced analysis of **in-situ** space plasma data" |
| space plasma | Same; `Topic :: Scientific/Engineering :: Physics` classifier; whole package scope |
| solar wind | `pyrfu/pyrf/get_omni_data.py` (OMNI solar-wind/IMF retrieval), `shock_normal.py`, `shock_parameters.py`, `docs/examples/01_mms/example_mms_ipshocks.ipynb`, `example_mms_walen_test.ipynb` |
| cdf | Primary input format; `pyrfu/pyrf/read_cdf.py`, `pyrfu/mms/get_ts.py`, `get_dist.py`, `get_variable.py` (pycdfpp), `pyrfu/pyrf/cdfepoch2datetime64.py` (cdflib) |
| calibration | `pyrfu/mms/feeps_flat_field_corrections.py`, `feeps_correct_energies.py`, `eis_proton_correction.py`, `correct_edp_probe_timing.py`, `remove_edist_background.py` |
| coordinate transformations | `pyrfu/pyrf/cotrans.py`, `gse2gsm.py`, `convert_fac.py`, `new_xyz.py`, `eb_nrf.py`, `pyrfu/mms/dsl2gse.py`, `dsl2gsm.py` |
| wavelet analysis | `pyrfu/pyrf/wavelet.py`, `compress_cwt.py`, `ebsp.py` |
| wave polarization | `pyrfu/pyrf/wavepolarize_means.py`, `ebsp.py`, `docs/examples/01_mms/example_mms_polarizationanalysis.ipynb` |
| pitch angle distributions | `pyrfu/mms/get_pitch_angle_dist.py`, `feeps_pad.py`, `feeps_pad_spinavg.py`, `eis_pad.py`, `hpca_pad.py`, `docs/examples/01_mms/example_mms_particle_pad.ipynb` |
| velocity distribution functions | `pyrfu/mms/vdf_omni.py`, `vdf_projection.py`, `vdf_reduce.py`, `vdf_elim.py`, `vdf_to_e64.py`, `make_model_vdf.py`, `pyrfu/pyrf/ts_skymap.py`, `average_vdf.py` |
| shock waves | `pyrfu/pyrf/shock_normal.py`, `shock_parameters.py`, `shock_models_parameters.json`, `pyrfu/pyrf/magnetosphere.py` (bow shock), `example_mms_ipshocks.ipynb` |
| time series | `pyrfu/pyrf/ts_scalar.py`, `ts_vec_xyz.py`, `ts_tensor_xyz.py`, `ts_spectr.py`, `ts_append.py`, `resample.py`, `filt.py`, `time_clip.py`, `autocorr.py` |
| plasma parameters | `pyrfu/pyrf/plasma_calc.py`, `iplasma_calc.py`, `plasma_beta.py`, `pres_anis.py`, `dynamic_press.py` |
| spectrograms | `pyrfu/plot/plot_spectr.py`, `pyrfu/pyrf/ts_spectr.py`, `wave_fft.py`, `psd.py`, `pyrfu/mms/spectr_to_dataset.py`, `feeps_sector_spec.py`, `eis_omni.py` |
| data visualization | Entire `pyrfu/plot/` subpackage (21 modules, 22 exported names) |

**Candidate new vocabulary terms (NOT in the HSSI Keyword vocabulary) — flagged for user decision, would create new rows:**
- `magnetic reconnection` — strongly evidenced: `docs/examples/01_mms/example_mms_edr_signatures.ipynb` (electron diffusion region), `example_mms_walen_test.ipynb`, `pyrfu/pyrf/match_phibe_dir.py`, `match_phibe_v.py`, `pyrfu/mms/calculate_epsilon.py`, `docs/examples/01_mms/example_mms_ohmslaw.ipynb`
- `turbulence` — evidenced: `pyrfu/pyrf/pvi.py`, `pvi_4sc.py` (partial variance of increments), `struct_func.py`, `increments.py`

**`data analysis` — RESTORED (validation finding W2).** PyHC also lists `data_analysis`, `general`, `local`, `remote`, `web_service`, and `solo` for PyRFU. `solo` is already covered by live HSSI's `solar orbiter`; `general`, `local`, `remote`, `web_service` are PyHC infrastructure tags rather than science keywords and remain excluded. `data analysis` is an exact row in the HSSI `Keyword` vocabulary (verified) and appears in both the PyHC curated registry (top source-priority tier) and the prior canonical file. The extraction pass originally omitted it on the inference that "the live record's curator appears to have dropped it deliberately"; validation correctly identified that as an inference rather than evidence, and as a violation of this file's own set-union rule for multi-valued fields. It is therefore included in the final 44.

### 17. Data Sources (OPTIONAL)
- **HTTP/HTTPS Directories**
- **Observatory/Mission-specific**
- **OMNIWeb**
- **S3/Cloud-aware**

**Note:** Unchanged (live HSSI = prior canonical file). All four re-verified at revision `40505b6a`:
- **OMNIWeb** — `pyrfu/pyrf/get_omni_data.py` builds `https://omniweb.gsfc.nasa.gov/cgi/nx1.cgi?activity=retrieve&spacecraft=omni2|omni_min…` and reads the response with `urllib.request.urlopen`.
- **Observatory/Mission-specific** — MMS Science Data Center (`pyrfu/mms/list_files_sdc.py`, `download_data.py`, `download_ancillary.py`, `list_files_ancillary_sdc.py`) and MAVEN SDC (`pyrfu/maven/download_data.py`, `LASP_PUBL = "https://lasp.colorado.edu/maven/sdc/public/files/api/v1/"`). Per Field 17's instruction, the corresponding missions are cross-listed in Field 32.
- **S3/Cloud-aware** — `pyrfu/mms/list_files_aws.py` uses `boto3.resource("s3")` with a configurable bucket/prefix (`pyrfu/mms/config.json` `"aws"` key); `boto3>=1.35.0` and `botocore>=1.35.0` are hard dependencies; `mms.get_data(..., source="aws")`.
- **HTTP/HTTPS Directories** — the SDC/OMNIWeb retrievals above plus `pyrfu/mms/load_brst_segments.py`, which fetches over plain **HTTP** (`URL = "http://www.spedas.org/mms/mms_brst_intervals.sav"` — an earlier draft said HTTPS; corrected per validation finding S10, which does not affect the value).

**Considered and rejected:** `CDAWeb`, `HAPI`, `das2`, `SSCWeb`, `TAP`, `VirES`, `The Virtual Solar Observatory`, `FTP/FTPS Directories` — no client code for any of these. Solar Orbiter data are read from a **local** directory tree only (`pyrfu/solo/db_init.py`, `config.json` `local_data_dir`), with no remote fetch, so Solar Orbiter adds no new data-source value.

### 18. Input File Formats (RECOMMENDED)
- **CDF**
- **IDL.sav** *(new — added in validation, finding E1)*
- **ISTP-Compliant** *(new)*
- **ascii** *(new)*

*(`csv` was proposed during extraction and **dropped by user decision**, 2026-07-27, per validation finding W7 — see below.)*

**`IDL.sav` — ADDED (validation ERROR E1).** The extraction pass wrongly rejected this format on the claim that `scipy.io.readsav` is not a dependency. It is: `pyrfu/mms/load_brst_segments.py` line 11 is `from scipy.io import readsav`, line 26 sets `URL = "http://www.spedas.org/mms/mms_brst_intervals.sav"`, and line 71 calls `intervals = readsav(file_path)`. `scipy>=1.14.0` is a hard dependency (`pyproject.toml`, `requirements.txt`), and `load_brst_segments` is a **public exported** function (`pyrfu/mms/__init__.py` line 71 import, line 173 in `__all__`). It downloads and parses the externally-hosted MMS burst-segment IDL SAVE file to return burst-mode intervals — an externally-sourced science-support input read through a documented public API, which is exactly what Field 18 covers. `IDL.sav` is an exact row in the live `FileFormat` vocabulary (verified 2026-07-27 via `GET http://localhost/api/models/FileFormat/rows/all/`).

**Note:** `CDF` retained from live HSSI (primary format — `pyrfu/pyrf/read_cdf.py`, `pyrfu/mms/get_ts.py`/`get_dist.py`/`get_variable.py` via `pycdfpp.load`, `pyrfu/solo/read_tnr.py` and `read_lfr_density.py` matching `solo_L2_rpw-tnr-surv_*.cdf` / `solo_L3_rpw-bia-density*_*.cdf`; dependencies `cdflib>=1.3.0`, `pycdfpp>=0.7.0`). Three **newly added** values, all repo-evidenced:
- **ISTP-Compliant** — `pyrfu/mms/get_ts.py` reads and depends on ISTP metadata attributes: `file[cdf_name].attributes["DEPEND_0"]`, an assertion that `"DEPEND_0" in var_attrs and "epoch" in var_attrs["DEPEND_0"].lower()`, plus handling of `DEPEND_1`/`REPRESENTATION_1`; `pyrfu/mms/eis_ang_ang.py` writes `FILLVAL`, `VALIDMIN` ISTP attributes. The package relies on the ISTP convention, not merely on raw CDF.
- **ascii** — `pyrfu/pyrf/get_omni_data.py` parses the plain-text OMNIWeb response; `pyrfu/mms/load_ancillary.py` reads whitespace-delimited MMS ancillary (ephemeris/attitude) products with `pd.read_csv(file, sep=r"\s+", header=None, skiprows=…)` driven by `pyrfu/mms/ancillary.json` column definitions.
- **`csv` — DROPPED by user decision (validation W7).** It was proposed on the basis of `pyrfu/models/igrf.py` `pd.read_csv(path)` for the bundled `igrf13coeffs.csv` and `pyrfu/mms/read_feeps_sector_masks_csv.py` for the FEEPS sector masks. But both read paths resolve their file from `os.path.dirname(os.path.abspath(__file__))` and read only tables bundled inside the installed package — `read_feeps_sector_masks_csv(tint)` takes a time interval, not a user-supplied path. That is the *same* "internal lookup table" category used below to reject `JSON`, so listing `csv` while rejecting `JSON` was internally inconsistent. Resolved by dropping `csv`, which restores consistency and removes a proposed addition rather than a submitted value. `ascii` is unaffected: it is genuinely external (OMNIWeb responses and downloaded MMS ancillary products).

**Considered and rejected:** `JSON` — JSON is read only for package-internal configuration/lookup tables (`pyrfu/{mms,maven,solo}/config.json`, `ancillary.json`, `mms_keys.json`, `feeps_bad_data.json`, `shock_models_parameters.json`) and for the MAVEN SDC's file-listing API response, never as a science-data input format (but see the `csv` inconsistency above). `HDF5`, `netCDF3/4`, `FITS`, `Zarr` — no reader present (`h5py`, `netCDF4`, `astropy` are not dependencies). **Correction:** an earlier version of this note also rejected `IDL.sav` on the false claim that `scipy.io.readsav` is absent; it is present and used, and `IDL.sav` is now listed as a value above.

### 19. Output File Formats (RECOMMENDED)
- *(none — `CDF` removed by user decision, 2026-07-27, per validation finding W1)*

**USER DECISION APPLIED:** `CDF` has been **removed**, emptying this field. Live HSSI carries `CDF`, so this is a deliberate removal of a submitted value, approved explicitly.

**Note (evidence for the removal):** A full search of the package found **no CDF-writing API** (no `cdfwrite`/`CDFWriter`/`pycdfpp` write calls, no `to_netcdf`, `to_csv`, `to_json`, `to_zarr`, `to_hdf`, `np.save`, or `savemat` anywhere in `pyrfu/`). The only files the package writes are downloaded mission CDFs copied into the local data store (`pyrfu/mms/download_data.py` → `copyfileobj` into a temp file then `copy(ftmp.name, out_file)`; `pyrfu/maven/download_data.py`; `pyrfu/mms/download_ancillary.py`; `pyrfu/mms/load_brst_segments.py`). In-memory results are returned as `xarray` objects, not written to disk. So "CDF output" is true only in the sense that PyRFU materialises `.cdf` files locally when downloading. Validation independently repeated the write-path search over all 250 modules and confirmed the same result (finding W1): every `pycdfpp` call is `pycdfpp.load`, `cdflib` is imported only for `cdfepoch` time conversion, and the only non-config writes are binary downloads of mission files. The prior canonical file's note ("Software can write CDF files based on the CDF library dependencies") was an inference this analysis does not support. Field 19's instruction is "only formats actually supported should be indicated" for **generated** files; caching a downloaded mission `.cdf` is not generating CDF output, and accepting that reading would make every downloader in HSSI claim CDF output.

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**

**Note:** Unchanged (live HSSI = prior canonical file). Re-verified from two sources at revision `40505b6a`: `pyproject.toml` classifiers `Operating System :: Unix`, `:: MacOS`, `:: MacOS :: MacOS X`, `:: Microsoft`, `:: Microsoft :: MS-DOS`, `:: Microsoft :: Windows`; and `.github/workflows/tests.yml` which runs the test suite on a matrix of `os: [ macos-latest, windows-latest, ubuntu-latest ]` (a v2.4.21-era commit is literally "fix job matrix switching to windows-latest"). `Solaris`/`MobilePlatform` not claimed; `OS Independent`/`Operating System Independent` not used since the three concrete platforms are CI-verified.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

**Note:** Unchanged (live HSSI = prior canonical file). Pure-Python package; `pyproject.toml` declares no architecture constraint and no compiled extensions are built (`build-backend = "setuptools.build_meta"`, `requires = ["setuptools>=42", "wheel==0.38.1"]`). `numba>=0.63.0` provides JIT acceleration but is architecture-portable, and the binary wheels of `pycdfpp`/`numpy` cover the common architectures. No `GPU`/`HPC or HEC` code (no CUDA, `mpi4py`, or job scripts).

### 22. Related Phenomena (OPTIONAL)
- **Solar Wind**

**Note:** **NEWLY FILLED** — live HSSI returns nothing and the prior canonical file said "Not found". `Solar Wind` is an exact row in the live HSSI phenomena vocabulary (`GET http://localhost/api/models/Phenomena/rows/all/` → `Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`, `X-ray emission`). Evidence that PyRFU supports solar-wind science: `pyrfu/pyrf/get_omni_data.py` retrieves OMNI solar-wind plasma and IMF parameters; `pyrfu/pyrf/magnetosphere.py` drives the Shue+1998 magnetopause and bow-shock models from solar-wind dynamic pressure and IMF `Bz`; `pyrfu/pyrf/shock_normal.py`, `shock_parameters.py` and `shock_models_parameters.json` compute interplanetary/bow-shock normals and upstream parameters; `docs/examples/01_mms/example_mms_ipshocks.ipynb` and `example_mms_walen_test.ipynb` are solar-wind analyses.

**Considered and rejected:** the other controlled values. `Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`, `Solar Flares`, `X-ray emission` — PyRFU is an in-situ plasma package with no solar imaging, coronal, or remote-sensing functionality. (`Coronal Holes` was listed here previously but is **not** a row in the live vocabulary; the `hssi-field-definitions` list is stale on that point.)

**`Geomagnetic Storms` — PENDING USER DECISION (validation W3).** The extraction pass rejected it on the claim that there is "no storm indices, storm-phase logic, or Dst/Kp handling anywhere in the package." **That claim is false** and is retracted here: `pyrfu/pyrf/get_omni_data.py` explicitly maps OMNI column indices for `dst`, `ae`, `al`, `au`, `kp` and `pc` (plus `ssn`, `f10.7`) for both the hourly and 1-minute OMNI databases, and `get_omni_data` is exported in `pyrfu/pyrf/__init__.py` `__all__`. The substantive recommendation is still **no** — retrieving a geomagnetic index is not science functionality *for* storms, and there is no storm-phase, superposed-epoch, or Dst-modelling code — but the decision now rests on that narrower argument rather than on a false factual premise. `Geomagnetic Storms` is confirmed in-vocabulary. The package's most characteristic phenomena (**magnetic reconnection**, **plasma turbulence**, **plasma waves/instabilities**) have **no rows in the phenomena vocabulary**; they are proposed instead as Field 16 keywords (see the candidate new terms there) rather than as invented phenomena rows.

### 23. Development Status (RECOMMENDED)
- **Value:** Active
- **Note:** **NEWLY FILLED** — live HSSI returns no development status. Evidence: (1) Zenodo record 10678695 `metadata.custom["code:developmentStatus"] = {id: "active", title: {en: "Active"}}` — the maintainer's own declaration; (2) sustained release cadence through the extraction date — tags v2.4.18 (2026-01-22), v2.4.19 (2026-01-31), v2.4.20 (2026-02-07), v2.4.21 (2026-02-27), with 66 commits in `v2.4.20..v2.4.21` alone, and further work on `devel` (repo `pushed_at = 2026-04-22T14:30:55Z`); (3) GitHub API `archived: false`; (4) four active CI workflows (`tests.yml`, `pylint.yml`, `codeql.yml`, `publish-to-pypi.yml`) plus pre-commit; (5) PyHC rates `software_maturity: Good` and `documentation: Good`. This matches repostatus.org "Active" — "reached a stable, usable state and being actively developed". Matches the prior canonical file.
- **Conflicting signal, deliberately not followed:** `pyproject.toml` still carries the classifier `Development Status :: 2 - Pre-Alpha`, and individual modules carry `__status__ = "Prototype"`. Both are stale boilerplate that contradicts a 100-release PyPI history, an explicit maintainer-set Zenodo status of "active", and PyHC's maturity rating; `Pre-Alpha` also has no HSSI equivalent (the nearest, `WIP`, means "no stable, usable public release yet", which is plainly false here).

### 24. Documentation (RECOMMENDED)
- **Value:** https://pyrfu.readthedocs.io/en/latest/
- **Note:** Unchanged. Confirmed HTTP 200 on 2026-07-26. Four agreeing sources: `pyproject.toml [project.urls] documentation`, the PyHC registry `docs` field, README ("Full documentation can be found on pyrfu.readthedocs.io"), and SoMEF. Includes installation instructions at `https://pyrfu.readthedocs.io/en/latest/installation.html` (`docs/installation.rst`) and a worked example gallery (`docs/examples/`). `.readthedocs.yaml` is present at the repository root.

### 25. Funder (OPTIONAL)

#### Funder 1
- **Organization:** Swedish National Space Agency
- **Funder Identifier:** https://ror.org/04t512h04

**Note:** **NEWLY FILLED** — live HSSI returns no funder. From DataCite `fundingReferences` on the concept DOI: `{funderName: "Swedish National Space Board", funderIdentifier: "04t512h04", funderIdentifierType: "ROR", awardTitle: "Plasma Jet Fronts: Energy Conversion and Particle Acceleration", awardNumber: "139/18"}`. Matches the prior canonical file. Name is already fully spelled out (no acronym to expand).
**Naming decision — RESOLVED by user decision 2026-07-27 (validation finding S8): the organization row is renamed to the current official name.** ROR `04t512h04`'s `ror_display` is **"Swedish National Space Agency"**; "Swedish National Space Board" is recorded there only as an *alias*, alongside `SNSA` (acronym) and `Rymdstyrelsen` (alias) — the agency was renamed. Verified 2026-07-27 via `GET https://api.ror.org/v2/organizations/04t512h04`.

The HSSI Organization row `14b7348c-636f-4142-b5ed-eea92095ad44` carries ROR `https://ror.org/04t512h04` and was named "Swedish National Space Board". Because the HSSI API cannot rename organizations (a PATCH would create a near-duplicate rather than rename), this is corrected as a guarded, backed-up DB-level `UPDATE` on the live database, executed **before** the PyRFU PATCH so that Field 25 binds to the existing row instead of creating a second organization. Isolation was established first: the row had **zero** inbound references in the live database (0 `website_software_funder`, 0 `website_person_affiliation`, 0 `publisher_id`), and no row named "Swedish National Space Agency" existed, so the rename affects no other record. PyRFU's funder link will be the row's first reference.

### 26. Award Title (OPTIONAL)

#### Award 1
- **Award Title:** Plasma Jet Fronts: Energy Conversion and Particle Acceleration
- **Award Number:** 139/18

**Note:** **NEWLY FILLED** — live HSSI returns no award. Verbatim from DataCite `fundingReferences[0].awardTitle` / `.awardNumber` on concept DOI 10.5281/zenodo.10678694 (re-fetched 2026-07-26). Matches the prior canonical file.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2021JA029152
- https://doi.org/10.1029/2022JA030430
- https://doi.org/10.1029/2022GL101693
- https://doi.org/10.1103/PhysRevLett.131.115201
- https://doi.org/10.1103/PhysRevLett.132.105201
- https://doi.org/10.1103/PhysRevLett.134.215201

**Note:** **All six retained verbatim from the existing HSSI record.** The prior canonical file said "Not found" — that is the stale value and it is **overridden by live HSSI**, which wins here. These DOIs appear nowhere in the repository, nowhere in the concept DOI's `relatedIdentifiers`, and nowhere in the PyHC entry, so they were supplied by the original submitter/curator (plausibly the maintainer, since three are Physical Review Letters papers from the IRF/MMS reconnection-and-turbulence literature and the v2.4.20 release notes cite "Kamaletdinov+2021, PRL" for a bundled example). **All six were machine-verified in validation (finding S5)** — not through DataCite, which does not index them, but through **Crossref** (`GET https://api.crossref.org/works/{doi}`), and every one is first-authored by Louis Richard, PyRFU's principal author: "Observations of Short-Period Ion-Scale Current Sheet Flapping" (JGR 2021, `10.1029/2021JA029152`); "Proton and Helium Ion Acceleration at Magnetotail Plasma Jets" (JGR 2022, `10.1029/2022JA030430`); "Are Dipolarization Fronts a Typical Feature of Magnetotail Plasma Jet Fronts?" (GRL 2022, `10.1029/2022GL101693`); "Fast Ion Isotropization by Current Sheet Scattering in Magnetic Reconnection Jet" (PRL 2023); "Turbulence in Magnetic Reconnection Jets from Injection to Sub-Ion Scales" (PRL 2024); "Electron Heating by Parallel Electric Fields in Magnetotail Reconnection" (PRL 2025). This materially strengthens the case that the maintainer supplied them, and removes the earlier caveat that they "could not be machine-verified." No additions: no publication DOIs were found anywhere in `README.rst`, `CITATION.cff`, `docs/`, or the notebook examples (the only DOI-like string in `docs/` is `10.1007/s11214-014-0057-3` inside a pasted MMS FGM CDF global-attribute dump in `quick-overview.ipynb` — that is the FGM instrument paper embedded in sample data, not a PyRFU-related publication, and it is not listed). Validation additionally surveyed the source tree, which the extraction pass had not: `pyrfu/**/*.py` docstrings carry roughly 20 further DOIs (e.g. `pyrf/c_4_j.py` → `10.1029/2001JA005088`, `models/magnetopause_normal.py` → Shue 1997/1998, `mms/remove_edist_background.py` → `10.1002/2017JA024518`). These are deliberately **not** added: they are algorithm-provenance citations for the methods each function implements, whereas Field 27 is for publications that describe, cite, or use the software itself.

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found
- **Note:** Unchanged (live HSSI empty; prior canonical file "Not found"). The concept DOI has no `relatedIdentifiers` with `resourceTypeGeneral = "Dataset"` (its only related identifier is the `HasVersion` link to 10678695). The repository names data *products* extensively (MMS FGM/FPI/HPCA/EIS/FEEPS/EDP/MEC L2 keys in `pyrfu/mms/get_data.py`, `solo_L2_rpw-tnr-surv`, `solo_L3_rpw-bia-density`) but never cites dataset DOIs or `hpde.io` identifiers for them, so listing any would be fabrication. If the user wants this field populated, the natural candidates are the SPDF/`hpde.io` NumericalData records for the MMS and Solar Orbiter RPW products the package reads — that requires a deliberate curation decision, not extraction.

### 29. Related Software (OPTIONAL)

**Retained from live HSSI (2):**
- **https://doi.org/10.5281/zenodo.1481144** — cdflib. Domain-specific heliophysics dependency (`cdflib>=1.3.0`); PyRFU's public time-conversion API is built on it: `pyrfu/pyrf/cdfepoch2datetime64.py`, `datetime642ttns.py`, `ttns2datetime64.py` all `from cdflib import cdfepoch`, and all three are exported in `pyrfu/pyrf/__init__.py` `__all__`. DataCite confirms the DOI resolves to "MAVENSDC/cdflib" (Software, Zenodo).
- **https://doi.org/10.5281/zenodo.15110786** — geopack. Domain-specific heliophysics dependency (`geopack>=1.0.10`); `pyrfu/plot/plot_magnetosphere.py` imports `from geopack import geopack` and calls `geopack.recalc()` and `geopack.trace()` to draw traced model field lines. DataCite confirms "tsssss/geopack: v1.0.12" (Software, Zenodo).

**Newly added (2):**
- **https://doi.org/10.5281/zenodo.11550090** — IRFU-Matlab (Zenodo concept DOI; DataCite title "IRFU-Matlab", `IsSupplementTo https://github.com/irfu/irfu-matlab`, creators Khotyaintsev, Nilsson, Johansson, Vaivads, Graham, Karlsson — overlapping PyRFU's own author list). **This is the single most distinguishing related-software link and it was missing.** PyRFU is explicitly the Python re-implementation of it: `README.rst` — "The Python package `pyrfu` is a software based on the IRFU-MATLAB library to work with space data" and "This software was developed by Louis RICHARD (louisr@irfu.se) based on the IRFU-MATLAB library"; the live HSSI description itself says "PyRFU is based on the IRFU-MATLAB library". Field 29 explicitly covers "software this work was forked from" / predecessors. Repository `https://github.com/irfu/irfu-matlab` confirmed HTTP 200.
- **https://doi.org/10.5281/zenodo.6391115** — pycdfpp. Domain-specific heliophysics dependency (`pycdfpp>=0.7.0`) and PyRFU's *primary* CDF reader: `pyrfu/pyrf/read_cdf.py`, `pyrfu/mms/get_ts.py`, `get_dist.py`, `get_variable.py`, `pyrfu/mms/remove_edist_background.py`, `pyrfu/solo/read_tnr.py`, `read_lfr_density.py` all use `pycdfpp.load`. **DOI corrected in validation (finding W4):** the extraction pass used the repository URL `https://github.com/SciQLop/CDFpp` on the claim that no DOI exists. A concept DOI does exist — the Zenodo search missed it because the deposit is titled by the C++ repository name `CDFpp`, not the PyPI name `pycdfpp`. Verified 2026-07-27: `GET https://zenodo.org/api/records/20813467` ("SciQLop/CDFpp: v0.11.0") reports `conceptdoi: 10.5281/zenodo.6391115` and `conceptrecid: 6391115`; `https://doi.org/10.5281/zenodo.6391115` resolves HTTP 200 and DataCite confirms `resourceTypeGeneral: Software`. Field 29 instructs "Ideally, enter the DOI for the software code. Otherwise, link to code repository," so the concept DOI supersedes the URL.

**Considered and REJECTED (audit trail).** Generic scientific-Python / infrastructure dependencies, excluded under the Field 29/30 relevance gate because the entry would be equally true of most Python packages and says nothing about PyRFU: `numpy>=2.0,<2.4`, `scipy>=1.14.0`, `pandas>=2.2.3`, `matplotlib>=3.9.0`, `requests>=2.32.0`, `python-dateutil>=2.9.0`, `tqdm>=4.66.0`, `numba>=0.63.0` (JIT compiler — generic infrastructure), `boto3`/`botocore` (AWS SDK — generic I/O plumbing), `keyring`/`keyrings.alt` (credential storage), `setuptools`/`wheel` (packaging), and the optional dev/test/docs extras (`pytest`, `pytest-cov`, `ddt`, `black`, `flake8`, `isort`, `pylint`, `mypy`, `pre-commit`, `sphinx` and its plugins, `nbsphinx`, `numpydoc`, `pydata-sphinx-theme`). Also rejected: `xarray` **here**, because it belongs in Field 30 where the demonstrated data-model exchange is documented (see below); and Cluster/THEMIS/Cassini tooling — those names appear in `pyrfu/lp/photo_current.py` only as spacecraft-surface *material* presets (`surface_materials = ["cluster", "themis", "cassini", "aluminium", …]`) and in `pyrfu/plot/pl_tx.py` only as a color-scheme option, which is not a software relationship.

### 30. Interoperable Software (OPTIONAL)

**Newly added (1):**
- **https://doi.org/10.5281/zenodo.598201** — xarray (DataCite: "xarray", Software, Zenodo).
  **Cited evidence of a demonstrated data-model exchange (Tier B bar):** `xarray` is not merely a dependency — `xarray.DataArray`/`xarray.Dataset` *is* PyRFU's documented public interchange format, so a user's PyRFU results are directly consumable by, and constructible from, any other xarray-based tool.
  - Public constructors that **return** xarray objects: `pyrfu.pyrf.ts_scalar`, `ts_vec_xyz`, `ts_tensor_xyz`, `ts_spectr`, `ts_skymap`, `ts_time`, `ts_append` (all in `pyrfu/pyrf/__init__.py` `__all__`).
  - Public readers that **return** xarray objects: `pyrfu.pyrf.read_cdf` (`import xarray as xr`; "Construct xarray DataArray" → returns a dict of `xr.DataArray`), `pyrfu.mms.get_data` (signature annotated `-> Union[DataArray, Dataset]`), `pyrfu.mms.get_ts`, `get_dist`, `get_variable`, `pyrfu.solo.read_tnr`, `read_lfr_density`, `pyrfu.mms.load_ancillary` (`data_frame.to_xarray()`), `pyrfu.mms.spectr_to_dataset`.
  - Public functions that **accept** xarray objects as their documented input type — e.g. `pyrfu/pyrf/cotrans.py` asserts `isinstance(inp, xr.DataArray)`; `pyrfu/mms/reduce.py` and `vdf_projection.py` document `vdf : xarray.Dataset`; `pyrfu/pyrf/wave_fft.py` documents `inp : xarray.DataArray`.
  This is exactly the "public API returns/accepts `xarray.Dataset` as its documented interchange format" case the field definition admits, not "uses xarray internally".

**Considered and REJECTED (audit trail):**
- **cdflib, pycdfpp** — Tier B; they are used to *read* files, which is dependency use rather than a peer-tool exchange. Recorded in Field 29 as domain-specific dependencies instead.
- **IRFU-Matlab** — a predecessor/re-implementation relationship with no data bridge, converter, or shared model between the two codebases (PyRFU cannot read irfu-matlab output and there is no MATLAB interface). Belongs in Field 29, and is listed there.
- **matplotlib** — Tier A, no exceptions. PyRFU's plot functions take a caller-supplied `matplotlib` axis, but "uses matplotlib for all plotting" is the field definition's own worked ❌ example.
- **numpy, scipy, pandas, requests, tqdm, python-dateutil, numba, boto3/botocore, keyring, pytest, setuptools** — Tier A / generic infrastructure by the "equally at home in a web app, a finance model, or a biology pipeline" test.
- **geopack** — a model library PyRFU calls internally for field-line tracing, not a tool a user would combine with PyRFU via a shared data model. Field 29 only.
- **Jupyter** — Tier B; the docs ship notebook examples (`nbsphinx`, `docs/examples/*.ipynb`), but shipping notebooks is not a documented package-to-package exchange.
- **PyHC ecosystem / "standard scientific Python ecosystem" blanket claims** — explicitly never sufficient. PyRFU's PyHC membership is recorded via Field 16 keywords and Field 24, not as an interoperability claim; no PySPEDAS/pytplot/SunPy/SpacePy/HAPI adapter, converter, or import path exists anywhere in `pyrfu/`.
- **The prior canonical file's Field 30 entries** (`xarray`, `matplotlib`, `cdflib`/`pycdfpp`, justified as "based on its design and PyHC membership") are therefore **not** carried over wholesale: only `xarray` survives the gate, and it now carries specific cited evidence instead of an ecosystem claim.

### 31. Related Instruments (OPTIONAL)

**RESOLVED BY USER DECISION 2026-07-27 (validation finding W5): all four per-spacecraft SPASE rows are accepted for each of the ten supported MMS instruments, and `MMS ASPOC` is dropped.** Final value = **41 entries**. Every identifier below was confirmed to exist in the live `InstrumentObservatory` vocabulary on 2026-07-27, and each `name` is copied verbatim from its matched row.

Rationale for the granularity: PyRFU supports all four MMS observatories equally (`mms_id` ∈ {1,2,3,4} throughout `pyrfu/mms/`, plus the explicit 4-spacecraft routines `c_4_j`, `c_4_grad`, `c_4_k`, `c_4_v`, `avg_4sc`, `pvi_4sc`, `pid_4sc`, `eis_skymap_combine_sc`, `feeps_avg_4sc`, `fk_power_spectrum_4sc`). The SMWG vocabulary has no constellation-level row for these instruments, so recording one spacecraft's identifier would state something false. Accepting all four is the only option that encodes no false claim.

**Known display consequence (accepted deliberately):** the view API returns instrument *names*, and nine of the ten instruments carry an identical name across all four of their per-spacecraft rows (only ADP is numbered). PyRFU's page will therefore show e.g. `MMS FEEPS` four times. This is an upstream defect in the vocabulary — four distinct rows sharing one display name — not an error in PyRFU's metadata, and it should be reported as such rather than worked around by encoding a single arbitrary spacecraft. Note also that no other software record in the database currently references any per-spacecraft MMS row, so there is no established precedent either way; the nearest analogue is OCBpy, which enumerates DMSP F16/F17/F18 separately (those rows have distinct names).

- **MMS FIELDS/FGM** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/FGM`
- **MMS FIELDS/FGM** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/FGM`
- **MMS FIELDS/FGM** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/FGM`
- **MMS FIELDS/FGM** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/FGM`
- **MMS FIELDS/SCM** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/SCM`
- **MMS FIELDS/SCM** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/SCM`
- **MMS FIELDS/SCM** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/SCM`
- **MMS FIELDS/SCM** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/SCM`
- **MMS FIELDS/SDP** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/SDP`
- **MMS FIELDS/SDP** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/SDP`
- **MMS FIELDS/SDP** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/SDP`
- **MMS FIELDS/SDP** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/SDP`
- **MMS 1 FIELDS Suite, Axial Double Probe** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/ADP`
- **MMS 2 FIELDS Suite, Axial Double Probe** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/ADP`
- **MMS 3 FIELDS Suite, Axial Double Probe** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/ADP`
- **MMS 4 FIELDS Suite, Axial Double Probe** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/ADP`
- **MMS FPI/DES** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DES`
- **MMS FPI/DES** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DES`
- **MMS FPI/DES** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DES`
- **MMS FPI/DES** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DES`
- **MMS FPI/DIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DIS`
- **MMS FPI/DIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DIS`
- **MMS FPI/DIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DIS`
- **MMS FPI/DIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DIS`
- **MMS HPCA** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/HotPlasmaCompositionAnalyzer`
- **MMS HPCA** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/HotPlasmaCompositionAnalyzer`
- **MMS HPCA** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/HotPlasmaCompositionAnalyzer`
- **MMS HPCA** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/HotPlasmaCompositionAnalyzer`
- **MMS EIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/EnergeticParticleDetector/EIS`
- **MMS EIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/EnergeticParticleDetector/EIS`
- **MMS EIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/EnergeticParticleDetector/EIS`
- **MMS EIS** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/EnergeticParticleDetector/EIS`
- **MMS FEEPS** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/EnergeticParticleDetector/FEEPS`
- **MMS FEEPS** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/EnergeticParticleDetector/FEEPS`
- **MMS FEEPS** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/EnergeticParticleDetector/FEEPS`
- **MMS FEEPS** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/EnergeticParticleDetector/FEEPS`
- **MMS Positions** — `https://spase-metadata.org/SMWG/Instrument/MMS/1/Ephemeris`
- **MMS Positions** — `https://spase-metadata.org/SMWG/Instrument/MMS/2/Ephemeris`
- **MMS Positions** — `https://spase-metadata.org/SMWG/Instrument/MMS/3/Ephemeris`
- **MMS Positions** — `https://spase-metadata.org/SMWG/Instrument/MMS/4/Ephemeris`
- **Plasma Wave Investigation** — `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/RPW`

**`MMS ASPOC` — DROPPED by user decision.** Its only support is the data key `aspoc` in `pyrfu/mms/mms_keys.json`; there is no ASPOC-specific reader, calibration, or processing anywhere in the package, making it the weakest of the eleven candidates.

**Solar Orbiter RPW entry (retained, unchanged):**
- **Instrument Name:** Plasma Wave Investigation
- **Instrument Identifier:** https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/RPW
- **Evidence (designed-to-support):** `pyrfu/solo/read_tnr.py` and `pyrfu/solo/read_lfr_density.py` are RPW-specific readers — they match the RPW product filename patterns `solo_L2_rpw-tnr-surv.*_YYYYMMDD_Vnn.cdf` and `solo_L3_rpw-bia-density.*_YYYYMMDD_Vnn.cdf`, walk RPW's `L2/thr/` and `L3/lfr_density/` directory trees, and implement RPW-specific science processing (TNR band/sweep reconstruction from `tnr_band_freq`/`tnr_band`/`sweep_num`, `-1e31` fill handling for BIA density). Both are exported from `pyrfu/solo/__init__.py`.
- **Resolution note:** exactly one type-1 row in the controlled vocabulary corresponds to Solar Orbiter's Radio and Plasma Waves instrument (matched via the identifier path segment `Solar_Orbiter/RPW`, since the repo only ever writes "rpw"/"TNR"/"LFR"). Canonical `name` copied verbatim. Two vocabulary rows share the name "Plasma Wave Investigation" (the other is `.../Galileo/PWS`), which is why the SPASE identifier is supplied — it is the de-duplication key and removes the collision.

**Per-instrument evidence (RESOLVED — all four spacecraft rows accepted for each instrument below; see the enumerated 41-entry list above, which is the submittable value):**

| Instrument (canonical vocab `name`) | Candidate SPASE identifiers | Repository evidence at 40505b6a |
|---|---|---|
| MMS FIELDS/FGM | `https://spase-metadata.org/SMWG/Instrument/MMS/{1,2,3,4}/FIELDS/FGM` | `pyrfu/mms/get_data.py` FGM keys (`b_gse_fgm_srvy_l2`, `b_gsm_fgm_brst_l2`, `b_bcs/dmpa_…`), `pyrfu/mms/mms_keys.json` `fgm`/`afg`/`dfg`/`fsm`, `dsl2gse.py`, `dsl2gsm.py` |
| MMS FIELDS/SCM | `.../SMWG/Instrument/MMS/{1,2,3,4}/FIELDS/SCM` | `get_data.py` `SCM: b_gse_scm_brst_l2`; `mms_keys.json` `scm`; `whistler_b2e.py`, `lh_wave_analysis.py` |
| MMS FIELDS/SDP **and** MMS *n* FIELDS Suite, Axial Double Probe | `.../SMWG/Instrument/MMS/{1,2,3,4}/FIELDS/SDP` and `.../FIELDS/ADP` (EDP = SDP + ADP; a per-spacecraft `Electric field Double Probe` row also exists at `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MMS{1,2,3,4}/EDP`) | `get_data.py` EDP keys (`e_gse_edp_brst_l2`, `e_dsl_edp_*`, `hmfe_dsl_edp_brst_l2`, `v_edp_*`, `phase_edp_*`, `sdev12/34_edp_*`), `correct_edp_probe_timing.py`, `scpot2ne.py`, `probe_align_times.py`, `mms_keys.json` `edp` |
| MMS FPI/DES | `.../SMWG/Instrument/MMS/{1,2,3,4}/FastPlasmaInstrument/DES` | `get_data.py` FPI electron keys, `get_dist.py`, `psd_moments.py`, `remove_edist_background.py`, `vdf_*`, `docs/examples/01_mms/example_mms_electron_psd.ipynb`, `example_mms_reduced_electron_dist.ipynb` |
| MMS FPI/DIS | `.../SMWG/Instrument/MMS/{1,2,3,4}/FastPlasmaInstrument/DIS` | `get_data.py` FPI ion keys, `remove_idist_background.py`, `remove_imoms_background.py`, `example_mms_reduced_ion_dist.ipynb`, `example_mms_reduced_ion_dist_para.ipynb` |
| MMS HPCA | `.../SMWG/Instrument/MMS/{1,2,3,4}/HotPlasmaCompositionAnalyzer` | `get_hpca_dist.py`, `hpca_calc_anodes.py`, `hpca_energies.py`, `hpca_pad.py`, `hpca_spin_sum.py`, `get_data.py` HPCA keys, `docs/examples/01_mms/example_mms_hpca.ipynb` |
| MMS EIS | `.../SMWG/Instrument/MMS/{1,2,3,4}/EnergeticParticleDetector/EIS` | 12 dedicated modules: `eis_ang_ang.py`, `eis_combine_proton_pad.py`, `eis_combine_proton_skymap.py`, `eis_combine_proton_spec.py`, `eis_moments.py`, `eis_omni.py`, `eis_pad.py`, `eis_pad_combine_sc.py`, `eis_pad_spinavg.py`, `eis_proton_correction.py`, `eis_skymap.py`, `eis_skymap_combine_sc.py`, `eis_spec_combine_sc.py`, `eis_spin_avg.py`, `get_eis_allt.py`; `docs/examples/01_mms/example_mms_eis.ipynb` |
| MMS FEEPS | `.../SMWG/Instrument/MMS/{1,2,3,4}/EnergeticParticleDetector/FEEPS` | 16 dedicated modules: `feeps_active_eyes.py`, `feeps_avg_4sc.py`, `feeps_bad_data.json`, `feeps_correct_energies.py`, `feeps_corrections.py`, `feeps_energy_table.py`, `feeps_flat_field_corrections.py`, `feeps_omni.py`, `feeps_pad.py`, `feeps_pad_spinavg.py`, `feeps_pitch_angles.py`, `feeps_remove_bad_data.py`, `feeps_remove_sun.py`, `feeps_remove_sunlit_sectors.py`, `feeps_sector_spec.py`, `feeps_spin_avg.py`, `feeps_split_integral_ch.py`, `get_feeps_alleyes.py`, `get_feeps_omni.py`, `read_feeps_sector_masks_csv.py`; `example_mms_feeps.ipynb`, `example_mms_feeps_electrons_4sc.ipynb` |
| MMS Positions | `.../SMWG/Instrument/MMS/{1,2,3,4}/Ephemeris` | MEC support: `get_data.py` `MEC: r_gse_mec_srvy_l2, r_gsm_mec_srvy_l2, r_gse_mec_brst_l2, r_gsm_mec_brst_l2, v_gse/gsm_mec_*`; `mms_keys.json` `mec`; `pyrfu/plot/add_position.py`, `mms_pl_config.py`; ancillary DEFATT/DEFEPH via `load_ancillary.py` |
| ~~MMS ASPOC~~ **(DROPPED)** | ~~`.../SMWG/Instrument/MMS/{1,2,3,4}/InstrumentControl/ASPOC`~~ | `pyrfu/mms/mms_keys.json` key `aspoc` only — data-key support with no ASPOC-specific processing. Weakest of the eleven candidates; **excluded by user decision 2026-07-27** and not part of the 41-entry value |

**Considered and REJECTED (audit trail):**
- **All MAVEN instruments** (ACC, EUV, IUVS, KP, LPW, MAG, NGIMS, PFP, SEP, STATIC, SWEA, SWIA — each has SPASE rows). `pyrfu/maven/` contains only `db_init.py`, `config.json` and `download_data.py`; the latter is a **generic archive downloader** that passes an instrument acronym straight through to the LASP SDC query string (`url = f"{url}instrument={var['inst']}"`, docstring "inst: instrument acronym (acc, euv, iuv, kp, lpw, mag, ngi, pfp, sep, sta, swe, swi)"). There is no MAVEN instrument-specific reader, calibration, or processing anywhere in the package — support is at the *mission archive* level, so MAVEN is listed in Field 32 (with `Observatory/Mission-specific` in Field 17) and no MAVEN instrument is listed here.
- **MMS AFG, DFG, FSM** — genuinely supported data keys (`mms_keys.json` `afg`, `dfg`, `fsm`; `get_data.py` `b_*_afg_srvy_l2pre`, `b_*_dfg_srvy_l2pre`) but the controlled vocabulary has **no rows** for them (only the merged `MMS FIELDS/FGM`); their support is already represented by the FGM entry above.
- **MMS DSP, EDI** — SPASE rows exist (`.../FIELDS/DSP`, `.../FIELDS/EDI`) but PyRFU has no DSP or EDI keys or routines.
- **Cluster, THEMIS, Cassini instruments** — appear only as Langmuir-probe *surface-material* presets in `pyrfu/lp/photo_current.py` (`surface_materials = ["cluster", "themis", "cassini", "aluminium", "aquadag", "gold", "graphite", "solar cells", "1eV", "TiN", "elgiloy"]`) and as a plot color scheme in `pyrfu/plot/pl_tx.py` (`colors: {'cluster', 'mms'}`). No data are read for any of them.
- **Other Solar Orbiter instruments** (EPD, EUI, Metis, PHI, SPICE, STIX, SoloHI, Ephemeris) — SPASE rows exist, but `pyrfu/solo/` reads RPW products only.
- **Generic multi-mission plumbing** — CDF/ISTP support → Field 18 (Input File Formats); OMNIWeb → Field 17 (Data Sources); the AWS S3 HelioCloud bucket → Field 17. None of these are instrument-specific and none are listed here.

**Note:** live HSSI returns no `relatedInstruments`, so nothing was dropped from the seed; the prior canonical file's freeform text (`MMS (… FGM, EDP, FPI, HPCA, EIS, FEEPS)`, `MAVEN (… instruments)`, `Solar Orbiter instruments`) is fully superseded by the vocabulary-resolved table above.

### 32. Related Observatories (OPTIONAL)

#### Observatory 1
- **Observatory Name:** Magnetospheric Multiscale
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MMS
- **Note:** Retained from live HSSI (which already stores exactly this `name`); the SPASE identifier is **newly added** as the reliable de-duplication key. Designed-to-support evidence: `pyrfu/mms/` is 91 modules — the largest subpackage — covering MMS data retrieval (SDC/AWS/local), instrument-specific calibration, moments, PADs, spectra, VDF reduction and 4-spacecraft techniques; README's quickstart is an MMS workflow. Resolution: six type-2 rows match "Magnetospheric Multiscale"; the `SMWG/...` namespace is the tie-breaker over the five `CNES/Observatory/CDPP-AMDA|CDPP-Archive/...` mirrors, and the per-spacecraft `SMWG/Observatory/MMS/{1..4}` rows are correctly *not* used since PyRFU supports the constellation.

#### Observatory 2
- **Observatory Name:** Solar Orbiter
- **Observatory Identifier:** https://spase-metadata.org/ESA/Observatory/SolarOrbiter
- **Note:** Retained from live HSSI (same `name`); SPASE identifier **newly added**. Designed-to-support evidence: `pyrfu/solo/` (`db_init.py`, `config.json`, `read_tnr.py`, `read_lfr_density.py`) reads Solar Orbiter RPW L2/L3 products with mission-specific filename and directory conventions. Resolution: two type-2 rows are named "Solar Orbiter" — `ESA/Observatory/SolarOrbiter` and `CNES/Observatory/CDPP-AMDA/SolO`. The agency-canonical ESA row is chosen (the `hssi-field-definitions` guidance names `ESA/Observatory/SolarOrbiter` as the correct resolution for Solar Orbiter, and the CDPP-AMDA row is a third-party archive mirror). Because the explicit identifier is supplied, the shared name cannot bind ambiguously; the alternate candidate is recorded here for transparency.

#### Observatory 3 — NEWLY ADDED / RESTORED
- **Observatory Name:** Mars Atmosphere and Volatile EvolutioN
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MAVEN
- **Note:** **Absent from live HSSI; present in the prior canonical file as "MAVEN".** Restored under the union rule, with the controlled-vocabulary spelling and identifier. Designed-to-support evidence at revision `40505b6a`: `pyrfu/maven/` exists as a first-class subpackage — `download_data.py` targets the MAVEN Science Data Center directly (`LASP_PUBL = "https://lasp.colorado.edu/maven/sdc/public/files/api/v1/"`), builds MAVEN `search/science/fn_metadata/file_info` queries by instrument/level/date, downloads via `search/science/fn_metadata/download`, and lays files out in a MAVEN-specific local tree; `db_init.py` + `config.json` manage the MAVEN data directory (`/Volumes/maven`); the live HSSI **description** already says "as well as MAVEN and Solar Orbiter missions" and "MAVEN Science Data Center"; live HSSI keyword `Maven` is already present, as is PyHC's `maven` keyword; and Field 5 already carries `Planetary Magnetospheres`, which only MAVEN justifies. Its absence from `relatedObservatories` while the description, keywords, and region all reference it is a straightforward gap. Resolution: two type-2 rows match; `SMWG/Observatory/MAVEN` (canonical name "Mars Atmosphere and Volatile EvolutioN", note the capital N) wins over `CNES/Observatory/CDPP-AMDA/MAVEN` by the SMWG tie-breaker. Name copied verbatim from the matched row.

**Considered and REJECTED (audit trail):** Cluster / THEMIS / Cassini / Galileo — see Field 31's rejection note (surface-material presets and a plot color scheme only). Per-spacecraft rows `SMWG/Observatory/MMS/{1,2,3,4}` — PyRFU supports the whole constellation, so the constellation-level row is the right granularity. CDAWeb / OMNIWeb — multi-mission archives, recorded in Field 17 (Data Sources) as the field definitions direct, not as observatories.

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/louis-richard/irfu-python/master/docs/_static/logo-pyrfu.png
- **Note:** Unchanged (live HSSI = prior canonical file = PyHC registry `logo`). Re-verified 2026-07-26: HTTP 200, and `docs/_static/logo-pyrfu.png` exists at revision `40505b6a` on the default branch, which is `master` (confirmed via the GitHub API), so the raw URL is stable. An SVG version also exists at `docs/_static/logo-pyrfu.svg` if a vector asset is ever preferred.

---

## Change Summary

### Changed vs. live HSSI (overrides — each justified in-field)
| Field | Live HSSI | New value | Why |
|---|---|---|---|
| 12 Version Number | `v2.4.12` (rendered "PyRFU - v2.4.12") | `v2.4.21` | Stale. `pyproject.toml`, tag `v2.4.21` = `master` HEAD, PyPI 2.4.21, GitHub release — all agree |
| 4 Software Functionality | 25 values | 39 values | Set union: +1 restored from the canonical file (`DPA:Wavelet Analysis`) and +13 newly evidenced (see table); child/parent completeness maintained |
| 16 Keywords | 22 | 44 | Set union + 15 in-vocabulary repo-evidenced additions + `data analysis` restored (W2) + 6 added by user decision (S4) |
| 18 Input File Formats | `CDF` | `CDF`, `IDL.sav`, `ISTP-Compliant`, `ascii` | ISTP attribute dependence in `get_ts.py`; OMNIWeb/ancillary ASCII; `scipy.io.readsav` burst-segment reader (E1). `csv` dropped by user decision (W7) |
| 19 Output File Formats | `CDF` | *(empty)* | No CDF-writing API exists anywhere in the package; removed by user decision (W1) |
| 10 Publication Date | `2024-02-19` | `2020-11-27` | DOI-record date replaced by the true first release (PyPI 1.8.3); user decision (W6) |
| 31 Related Instruments | *(empty)* | 41 entries | All four per-spacecraft SPASE rows for each of ten MMS instruments + Solar Orbiter RPW; `MMS ASPOC` excluded; user decision (W5) |
| 29 Related Software | 2 DOIs | 4 entries | Added IRFU-Matlab (predecessor — biggest gap) and pycdfpp (primary CDF reader, cited by concept DOI `10.5281/zenodo.6391115` per W4) |
| 32 Related Observatories | 2 entries | 3 entries | **Added MAVEN** (`pyrfu/maven/` + description + keyword already reference it). Correction: the two existing rows already carried the correct SPASE identifiers (`SMWG/Observatory/MMS`, `ESA/Observatory/SolarOrbiter`) — an earlier draft described these as "newly added", which overstated it. Sending them is still correct and binds to the same rows; the genuine delta is MAVEN alone |

### Newly filled (live HSSI returned nothing)
Field 15 License · Field 22 Related Phenomena · Field 23 Development Status · Field 25 Funder · Field 26 Award Title/Number · Field 30 Interoperable Software · Field 31 Related Instruments (41 entries) · Field 12 Version Date / Version Description

### Changed vs. the prior canonical file (2025-10-09)
- Field 27 Related Publications: `Not found` → the 6 live-HSSI DOIs (live HSSI wins; the file was stale)
- Field 7 Software Name: `Python RymdFysik Utilities (PyRFU)` → `PyRFU` (live HSSI + repository evidence)
- Field 9 Concise Description: replaced by the live HSSI / PyHC sentence
- Field 11 Publisher Identifier: `https://ror.org/04t3en479` → `https://zenodo.org` (live HSSI + field-definition example + existing HSSI org row)
- Field 12: `v2.4.12` / `2024-02-15` / v2.4.12 notes / version DOI `…10678695` → `v2.4.21` / `2026-02-27` / v2.4.21 release notes / **Version PID: Not found**
- Field 13 note: supported Python versions 3.10–3.12 → 3.10–3.14
- Fields 29 & 30: dependency dumps (numpy, scipy, pandas, matplotlib, xarray, numba, …) replaced by relevance-gated entries with cited evidence
- Fields 31 & 32: freeform instrument/observatory text replaced by SPASE-resolved values
- Field 22: `Not found` → `Solar Wind`

### Could not be determined
- **Version PID for v2.4.21** — verified not to exist (Zenodo archiving stopped at v2.4.12; concept DOI has a single `HasVersion`). Explicitly *not* back-filled with the v2.4.12 DOI.
- **Reference Publication (14)** — no paper describes PyRFU.
- **Related Datasets (28)** — no dataset DOIs cited anywhere; would require curation, not extraction.
- **Related Instruments for MMS (31)** — *(resolved during validation, no longer outstanding)* each instrument maps to four per-spacecraft SPASE rows; the user decided on 2026-07-27 to accept all four for each of the ten supported instruments, giving the 41-entry value.
- **ORCID/ROR for the `PyRFU team` CITATION.cff organization author** — no ROR exists; flagged for a user decision.
- **Provenance of the 6 Related Publications DOIs** — not machine-verifiable (Crossref, not DataCite-indexed) and absent from the repository; retained as submitted.

### Validation pass (2026-07-27)

Independent full validation returned **1 ERROR, 9 WARNINGS, 15 SUGGESTIONS, 25 PASSED**. Applied in this file without needing a user decision:

- **E1** — added `IDL.sav` to Field 18 and retracted the false "`scipy.io.readsav` is not a dependency" claim.
- **W2** — restored `data analysis` to Field 16 (now 38 keywords).
- **W4** — replaced pycdfpp's repository URL with its verified concept DOI `10.5281/zenodo.6391115`.
- **W8** — Field 16's final value is now an enumerated bulleted list rather than middot-delimited prose.
- **W3, S9, S10** — retracted three factually wrong evidence citations (the `Geomagnetic Storms` rejection premise, the Zenodo `is_last` citation, and HTTPS-vs-HTTP in Field 17). None changed a value.
- **S5** — recorded Crossref verification of all six Field 27 DOIs (all first-authored by Louis Richard) and the deliberate exclusion of ~20 algorithm-provenance DOIs in the source tree.
- **S7** — clarified that `Parent:Child` vs `Parent: Child` is presentational, so the update plan must not manufacture a 39-value diff for Field 4.

Validation confirmed as correct, with no change required: the provenance header; every controlled-vocabulary value across all list fields; Field 4's parent coverage (zero orphaned children) and all 14 additions; the entire version block including the absence of a v2.4.21 DOI; all six authors, ORCIDs and ROR affiliations (each binding to an existing HSSI Organization row, so no duplicates); Field 30's `xarray` entry and every Tier A rejection; and all three Field 32 observatories including the MAVEN restoration.

### User decisions — ALL RESOLVED 2026-07-27

| # | Field | Decision | Applied |
|---|---|---|---|
| 1 | 19 Output Formats | **Remove `CDF`** — field becomes empty (W1) | ✅ |
| 2 | 31 Related Instruments | **Accept all four per-spacecraft rows** for each of the ten instruments; **drop `MMS ASPOC`**. 41 entries (W5) | ✅ |
| 3 | 18 Input Formats | **Drop `csv`** for consistency with the `JSON` rejection (W7) | ✅ |
| 4 | 10 Publication Date | **Use `2020-11-27`** (true first PyPI release) over the DOI-record date `2024-02-19` (W6) | ✅ |
| 5 | 6 Authors | **Do not add** the `PyRFU team` CITATION.cff organization author (W9) | ✅ (no change) |
| 6 | 8 Description | **Extend** — append one sentence covering dispersion solvers, Langmuir-probe models, and empirical field/boundary models, **leaving the original text untouched** (S14) | ✅ |
| 7 | 16 Keywords | **Add the six in-vocabulary terms**; **do not create** the new rows `magnetic reconnection` / `turbulence` (S4) | ✅ |
| 8 | 4 Functionality | **No** borderline additions — `Data Visualization:Mission-Specific` and `Models and Simulations:Forward-Fitting` both declined (S1, S2) | ✅ (no change) |
| 9 | 25 Funder | **Rename the organization row** "Swedish National Space Board" → "Swedish National Space Agency" to match the current ROR display name (S8). DB-level change; the HSSI API cannot rename organizations | ✅ applied to the live DB 2026-07-27 (`UPDATE 1`; 287 orgs unchanged, no duplicate; API serves the new name) |

Field 4 remains at 39 values, Field 16 at 44 keywords, Field 18 at 4 values, Field 19 empty, Field 31 at 41 entries.

### PATCH applied and verified — 2026-07-27

`PATCH http://localhost/api/data/software/bdd706f0-b987-446b-b650-78d9d86f00b2/` → HTTP 200, `status: ok`, 16 `fieldsUpdated`: `award, description, development_status, funder, input_formats, interoperable_software, keywords, license, output_formats, publication_date, related_instruments, related_observatories, related_phenomena, related_software, software_functionality, version`.

**Roundtrip verification — all pass.** Via the view API: description 761→1009 chars matching the patch byte-for-byte; `publicationDate = 2020-11-27`; version renders `PyRFU - v2.4.21`; `inputFormats = [CDF, IDL.sav, ISTP-Compliant, ascii]`; `outputFormats` absent (cleared); `relatedPhenomena = [Solar Wind]`; 39 functionality values matching the patch after colon normalization; 44 keywords matching case-insensitively with zero missing and zero extra; 4 related software; `interoperableSoftware = [xarray]`; 3 observatories including MAVEN; 41 instruments. Via the database (fields the view API hides or reshapes): the version row is `number=v2.4.21`, `release_date=2026-02-27`, `version_pid=NULL`, with the v2.4.12 row unlinked as designed; `license = MIT License`; `development_status = Active` (repostatus row `29d7a7e6…`); `funder = Swedish National Space Agency` bound to the pre-renamed row with the organization count still 287 and exactly one such row, so no duplicate was created; the award row reuses the existing `139/18`; all 41 instrument identifiers and all 3 observatory identifiers match the patch exactly; author count unchanged at 6.

**Untouched fields confirmed intact** — Fields 2, 3, 5, 6, 7, 9, 11, 13, 14, 17, 20, 21, 24, 27, 28 and 33 were compared byte-for-byte against the pre-PATCH baseline and are unchanged.

**Known consequence, accepted:** the v2.4.12 version row carried `version_pid = https://doi.org/10.5281/zenodo.10678695`. The serializer creates a new version row rather than editing the existing one, so that DOI left the record along with the superseded version. This is correct — the DOI belongs to v2.4.12, and no Zenodo DOI exists for v2.4.21 — but it was a stored value, recorded here for traceability.

### Upstream items to relay to the maintainer (no HSSI action)
- Zenodo archiving stopped at v2.4.12; `CITATION.cff` and the README DOI badge still point at the v2.4.12 deposit, nine releases behind. Re-enabling the GitHub–Zenodo integration would restore version DOIs.
- `pyproject.toml` still carries `Development Status :: 2 - Pre-Alpha` and 250 modules carry `__status__ = "Prototype"`, contradicting a 100-release history (S13).
- Two code contributors — Apostolos Kolokotronis (6 modules) and Atlas Silverhult (`pyrf/mva_gui.py`) — carry `__author__` tags but appear in no citation source, including `CITATION.cff` (S12).
