# HSSI Metadata Extraction Results

**HSSI Software ID:** 6adc2c82-61b3-41b4-89ca-62862bfe9b9f
**Repository:** https://github.com/SciQLop/speasy
**Source Revision:** 7a6281ff044a28a660a71f81e49581fe71baefe4 (2026-07-22 09:22:42 +0200, branch `main`)
**Extraction Date:** 2026-07-24
**Validation Date:** 2026-08-21
**Validation Status:** PASS

**Seeds this record was built from:**
1. **The existing HSSI record for Speasy** — the authoritative baseline for scalar and editorial fields.
2. **Prior canonical `hssi_metadata.md`** — extraction dated 2025-10-09, based on v1.6.1. Source of file-only additions carried forward where the current repo still supports them.

**Release-state caveat used throughout:** the repository's `main` branch at the extraction revision contains capabilities that are **not in the v1.7.1 release** (2025-12-18). Values whose sole or primary evidence is post-release code are tagged `[main-branch, unreleased as of v1.7.1]`. Verified post-release-only: `speasy/core/hapi/` HAPI server client, HAPI **binary** codec, ISTP **netCDF** codec, and the `cdpp3dview` data provider. Verified already released in v1.7.1: HAPI **CSV** codec, ISTP CDF codec, CSA-over-TAP, bundled `cda.yaml` archive definitions, UiowaEphTool, SSCWeb coordinate systems, signal filtering/resampling, line + colormap plotting, WASM/Pyodide support. The tagged, unreleased-on-`main` values are recorded rather than withheld, because this record's Code Repository (Field 3) points at the repository itself and its default branch is `main` — `main` is therefore the software state this metadata describes. The tags exist so a later reader can tell which capabilities a user of the v1.7.1 release will not yet find.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

HSSI does not expose the original submitter through the view API. The Speasy wording in HSSI (name, description, concise description) is treated as intentional submitted editorial content and is preserved verbatim.

---

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** `https://doi.org/10.5281/zenodo.4118780`

**Source:** From existing HSSI record. Re-verified against the Zenodo API (`records/17978034` -> `"conceptdoi": "10.5281/zenodo.4118780"`), the DataCite API, and `CITATION.cff`/README badge. This is the correct concept (all-versions) DOI.

---

### 3. Code Repository (MANDATORY)
- **Value:** `https://github.com/SciQLop/speasy`

**Source:** From existing HSSI record. Re-verified: repo is live, not archived, default branch `main`, last push 2026-07-22 (GitHub API). Also matches `CITATION.cff` `url:`, `pyproject.toml` `[project.urls] homepage`, and Zenodo `metadata.custom["code:codeRepository"]`.

---

### 4. Software Functionality (MANDATORY)

**Values — 16 total:**

*Formatting note:* HSSI stores/displays these with a space after the colon (e.g. `Data Processing and Analysis: Analysis`). Below they are written in the canonical form from the HSSI field definitions (no space). This is a display/storage normalization, **not** a value change — none of these values should be diffed on the colon-space.

**From the existing HSSI record — 10:**
1. `Coordinate Transforms:Mission-Specific`
2. `Data Processing and Analysis`
3. `Data Processing and Analysis:Analysis`
4. `Data Processing and Analysis:Data Access and Retrieval`
5. `Data Processing and Analysis:File Format Conversion`
6. `Data Processing and Analysis:Processing`
7. `Data Processing and Analysis:Time Series Analysis`
8. `Data Visualization`
9. `Data Visualization:2D Graphics`
10. `Data Visualization:Line Plots`

**From repository evidence — 6:**

11. `Coordinate Transforms`
    **Reason: REQUIRED PARENT — missing in live HSSI.** HSSI has `Coordinate Transforms: Mission-Specific` without its parent category. Every subcategory must have its parent listed.

12. `Coordinate Transforms:Magnetospheric`
    Evidence (released): `speasy/data_providers/ssc/__init__.py` exposes `coordinate_system=` on `get_data`/`_get_orbit` and injects it into the SSCWeb REST path; `docs/user/sscweb/sscweb.rst` documents the user-selectable set **geo, gm, gse, gsm, sm, geitod, geij2000** (default `gse`). Also `tests/test_cdpp3dview.py::test_get_data_on_frames` parameterizes over `GSE`, `GSM`, `SM`, `IAU_EARTH` `[main-branch, unreleased as of v1.7.1 for the 3DView provider]`. The released SSCWeb evidence above is sufficient on its own, so this value is release-backed.

13. `Coordinate Transforms:Heliospheric`
    Evidence: `tests/test_cdpp3dview.py` parameterizes `coordinate_frame` over `HEE`, `HEEQ`, `HCI`, `IAU_SUN`, `ECLIPJ2000`, `J2000` `[main-branch, unreleased as of v1.7.1 for the 3DView provider]`; released support comes from `speasy/data_providers/uiowa_eph_tool/__init__.py`, whose `__SUN_COORDINATES__ = {"Ecliptic", "Equatorial"}` provides Sun-origin heliocentric ecliptic/equatorial trajectories.

14. `Coordinate Transforms:Planetary`
    Evidence (released): `uiowa_eph_tool` hardcodes `__PLANET_COORDINATES__` (Geographic/Ecliptic/Equatorial), `__SATURN_COORDINATES__` (adds **KSM**), and `__SATELLITE_COORDINATES__` (adds **Co-rotational**) for Venus, Earth, Jupiter, Saturn, Io, Europa, Ganymede, Callisto, Titan, Enceladus and 14 other moons. Reinforced by 3DView body-fixed frames `IAU_JUPITER`, `IAU_MARS`, `IAU_SATURN`, `CPHIO`/`EPHIO`/`GPHIO`/`IPHIO` `[main-branch]`.

15. `Data Processing and Analysis:Data Reduction`
    Evidence (released): `speasy/signal/resampling/__init__.py` — `resample(var, new_dt)`, `interpolate(ref, var)`, `generate_time_vector`; `speasy/signal/filtering/__init__.py` — `apply_sos_filter`, `sosfiltfilt` (SciPy IIR); `SpeasyVariable.sanitized(drop_fill_values=..., drop_out_of_range_values=..., drop_nan_and_inf=...)`, `replace_fillval_by_nan()`, `clamp_with_nan()`. `tests/test_resampling.py`, `tests/test_filtering.py`; documented at `docs/user/scipy.rst` and the README "Resampling" example.

16. `Data Visualization:Spectrogram`
    Evidence (released): `speasy/plotting/__init__.py` defines `PlotType.SPECTRO` and `_infer_plot_type()` auto-selects `colormap()` when `meta["DISPLAY_TYPE"] == "spectrogram"`; `speasy/plotting/mpl_backend/__init__.py::colormap` renders `pcolormesh` with `LogNorm` + colorbar. `docs/examples/CDAWeb.ipynb` calls `mms1_dis_energyspectr_omni_fast.plot["matplotlib"].colormap(cmap='viridis')`; `docs/examples/CompleteDemo.ipynb` has a "CSA spectrogram example"; `tests/test_speasy_variable.py` builds `DISPLAY_TYPE: "spectrogram"` variables and asserts they are plottable; `tests/test_amda_parameter.py::test_parameter_colormap_lot`.

**Note — considered and deliberately NOT added:**
- `Data Processing and Analysis:Spectrogram` — Speasy performs no FFT/STFT/wavelet computation; it retrieves pre-computed spectrogram products. Only the *display* side applies.
- `Data Processing and Analysis:Energy Spectra` — energy-spectra products (`mms1_des_energyspectr_omni_fast`, `PSP_ISOIS-EPILO_L2-PE/Electron_Counts_ChanE`, `STA_L1_HET/Proton_Flux`) are retrieved and their energy axes/bins handled, but no spectra are computed.
- `Data Processing and Analysis:Plasma Moments` — FPI/CIS moment products are retrieved, not computed.
- `Data Processing and Analysis:3D Particle Distribution Processing` — `docs/examples/alfvenic.ipynb` retrieves PAS VDF data, but the distribution math is user NumPy code in the notebook, not Speasy API.
- `Data Visualization:3D Graphics` / `Data Visualization:Orbit Plots` — `docs/examples/SSCWeb.ipynb` builds 3D orbit figures with raw `ax.plot_surface`/`ax.plot`; Speasy's own plotting API offers only `line()` and `colormap()`.
- `Mission-related:*` (incl. `:Inventory`, `:Distribution/Access`) — Speasy builds mission inventories (`DataProvider.build_inventory/update_inventory`), but it is general-purpose community software, not part of any mission's ground system or pipeline.
- `Servers and Environments:*` — Speasy is a *client* of the SciQLOP proxy/cache server (`speasy/core/proxy/`), not a server; no Dockerfile or container definition in the repo.
- `Coordinate Transforms:Solar` — no solar-disk coordinates (no Carrington/Stonyhurst/helioprojective); `HEEQ`/`IAU_SUN` are covered under Heliospheric.
- `Coordinate Transforms:Ionospheric`, `Data Processing and Analysis:Calibration`, `ML/AI`, `Models and Simulations:*` — no supporting code.

**Caveat on Coordinate Transforms (for the validator):** Speasy does not implement the transform math itself — it exposes the target coordinate system/frame as a user-facing request parameter and the web service returns data in that frame. Per the `software-functionality` skill ("if the user can access or benefit from the transform, even indirectly, err on the side of inclusion"), these are user-facing coordinate-transformation capabilities.

---

### 5. Related Region (MANDATORY)

**Values — 3:**
1. `Earth Magnetosphere`
2. `Interplanetary Space`
3. `Planetary Magnetospheres`

**Source:** From existing HSSI record. Re-verified against the current repo: Earth Magnetosphere (MMS, Cluster, THEMIS, Arase, Wind/ACE upstream of the bow shock, SSCWeb GSE/GSM/SM trajectories); Interplanetary Space (ACE/Wind/OMNI solar wind, Solar Orbiter, PSP, STEREO); Planetary Magnetospheres (MAVEN STATIC at Mars, Juno JEDI at Jupiter, UiowaEphTool Jupiter/Saturn/moon frames, IMPEx common provider in `speasy/core/impex/`).

**Considered and not selected — `Solar Environment`:** Speasy's dynamic inventory reaches solar-mission datasets through CDAWeb/AMDA, `docs/examples/*.ipynb` and `tests/test_cdpp3dview.py` reference SOHO/SDO/STEREO, and the developers' own EPSC-DPS 2025 abstract frames the tool as serving "planetary and heliospheric" data. However the repository contains **no solar-atmosphere-specific support**, and the inner-heliosphere in-situ data (PSP/SOLO/STEREO SEP and magnetic field) is already covered by Interplanetary Space. The region is therefore omitted, per "prefer evidence over speculation"; it would become correct only if the repository gained solar-atmosphere-specific support, which it does not have at the source revision above.

**Note — `Earth Atmosphere` considered and dropped:** no ionosphere/thermosphere-specific products, models, or tests in the repo.

---

### 6. Authors (MANDATORY)

**Values — 6 authors.** This is the single largest correction in this refresh: live HSSI has 2 authors, while the repository's current `CITATION.cff`, the Zenodo v1.7.1 record, and the DataCite concept-DOI record all list **6**. Matched by ORCID first, then normalized name; affiliations unioned per matched author. No author present in any source has been dropped.

**Author 1 — Alexis Jeandet**
- **Name:** Alexis Jeandet
- **Author Identifier:** `https://orcid.org/0000-0003-2892-6924`
- **Affiliation:**
  - **Organization:** Laboratoire de Physique des Plasmas
  - **Affiliation Identifier:** `https://ror.org/05c95bg36`
- **Source:** From existing HSSI record. Re-verified: `CITATION.cff`, `pyproject.toml` `authors`/`maintainers`, `AUTHORS.rst` (Development Lead), Zenodo + DataCite creators, and the author's ORCID record (current employment "Laboratoire de Physique des Plasmas", ROR `05c95bg36`, since 2008 — an exact ROR match to the existing HSSI affiliation).

**Author 2 — Alexandre Schulz**
- **Name:** Alexandre Schulz
- **Author Identifier:** `https://orcid.org/0009-0009-7151-8089`
- **Affiliation:**
  - **Organization:** Institut de Recherche en Astrophysique et Planétologie
  - **Affiliation Identifier:** `https://ror.org/05hm2ja81`
- **Source:** Author from the existing HSSI record, whose shared Person record carries the same IRAP affiliation recorded above (`https://ror.org/05hm2ja81`) — HSSI holds affiliations on a Person shared across software records rather than per record. That value is independently supported for Speasy: it was carried forward from the prior `hssi_metadata.md` and is backed by `AUTHORS.rst` (`alexandre.schulz@irap.omp.eu`). The full expanded name and ROR match the organization already held in HSSI for Institut de Recherche en Astrophysique et Planétologie (`https://ror.org/05hm2ja81`), so no new organization is created.
- *Note:* the author's ORCID lists a different current employment (Université Sorbonne Paris Nord, ROR `0199hds37`, since 2022). The repo-stated IRAP affiliation is the one relevant to his Speasy contribution (the AMDA web service), and it is the affiliation recorded above. His other ORCID-listed employment, Université Sorbonne Paris Nord, is not recorded: it is not stated anywhere in the repository and is not tied to his Speasy contribution.

**Author 3 — Nicolas Aunai**
- **Name:** Nicolas Aunai
- **Author Identifier:** `https://orcid.org/0000-0002-9862-4318`
- **Affiliation:**
  - **Organization:** Laboratoire de Physique des Plasmas
  - **Affiliation Identifier:** `https://ror.org/05c95bg36`
- **Source:** `CITATION.cff` (3rd author), Zenodo v1.7.1 creators, DataCite concept-DOI creators. Affiliation from the author's ORCID record: current employment "Laboratoire de Physique des Plasmas / CNRS" (since 2014) — matched by institution to the **existing** HSSI organization row for LPP (ROR `05c95bg36`).
- **Affiliation, and the add-only constraint that governs it.** The LPP affiliation recorded above is the affiliation Nicolas Aunai holds, on the ROR-backed organization row (`https://ror.org/05c95bg36`), and it is the only LPP organization he is associated with. A durable platform constraint governs any future change here: an affiliation can only ever be **added** to a person through the metadata update path — it can never be replaced or removed there — so recording an affiliation for an institution the person already carries under a differently-named organization row leaves a permanent duplicate that no later metadata update can undo. That constraint is why this value was once withheld: a second, identifierless organization row denoted the same laboratory, and recording the ROR-backed row while that duplicate stood would have left him permanently showing two affiliations for one institution. Those identifierless rows no longer exist and the laboratory is represented by the single ROR-backed row above, so the constraint no longer stands against this value — but it still binds a future agent, who must resolve any name variant of this laboratory to `https://ror.org/05c95bg36`, and check for an existing same-institution affiliation, rather than adding a second organization for it.

**Author 4 — Benjamin Renard**
- **Name:** Benjamin Renard
- **Author Identifier:** `https://orcid.org/0000-0003-1847-7627`
- **Affiliation:**
  - **Organization:** Institut de Recherche en Astrophysique et Planétologie
  - **Affiliation Identifier:** `https://ror.org/05hm2ja81`
- **Source:** The identifier recorded above is the value the live shared HSSI Person record carries — HSSI holds identifiers and affiliations on a Person shared across software records rather than per record, so it reaches Speasy from that shared Person and **not** from Speasy's own metadata, which names him as an author but supplies no ORCID for him (`CITATION.cff`, Zenodo and DataCite all omit it). It is nonetheless independently verified as his: ORCID `0000-0003-1847-7627` carries the record name "Benjamin Renard" and a single open-ended employment at Institut de Recherche en Astrophysique et Planétologie, Toulouse, FR, disambiguated by ROR `https://ror.org/05hm2ja81` — the same ROR as the affiliation recorded above, which ORCID therefore independently corroborates. Repository and DOI evidence for his authorship and IRAP association: `CITATION.cff` (4th author), Zenodo v1.7.1 creators, DataCite creators, `AUTHORS.rst` (Contributors -> AMDA Webservice, `benjamin.renard@irap.omp.eu`). Also a Speasy committer (`@brenard-irap` in `HISTORY.rst` for 1.5.0/1.5.2) and co-author of the EPSC-DPS 2025 Speasy abstract. The affiliation matches the existing HSSI IRAP organization row.

**Author 5 — Vincent Génot**
- **Name:** Vincent Génot
- **Author Identifier:** `https://orcid.org/0000-0002-7708-8077`
- **Affiliation:**
  - **Organization:** Institut de Recherche en Astrophysique et Planétologie
  - **Affiliation Identifier:** `https://ror.org/05hm2ja81`
- **Source:** `CITATION.cff` (5th author), Zenodo v1.7.1 creators, DataCite creators; co-author of the EPSC-DPS 2025 Speasy abstract.
- **Affiliation — what supports it, and what does not.** The IRAP affiliation above is the value the live shared HSSI Person record carries; HSSI holds affiliations on a Person shared across software records rather than per record, so it reaches Speasy from that shared Person. **It is recorded because the shared HSSI Person record carries it, not because Speasy's repository establishes it.** The independent evidence stays thin and must remain visible as such: his ORCID record's `employments` group is empty, so ORCID establishes nothing about his affiliation; the repository states no affiliation for him; and although he is the lead author of the AMDA reference paper (`10.1016/j.pss.2021.105214`), Crossref returns no affiliation strings for it. Nothing consulted ties IRAP to the time of his Speasy contribution, and this entry should not be read as asserting that it does. The organization resolves by ROR `https://ror.org/05hm2ja81` to the IRAP row already held in HSSI, so no new organization is created.

**Author 6 — Nicolas André**
- **Name:** Nicolas André
- **Author Identifier:** `https://orcid.org/0000-0001-8017-5676`
- **Affiliation 1:**
  - **Organization:** Institut de Recherche en Astrophysique et Planétologie
  - **Affiliation Identifier:** `https://ror.org/05hm2ja81`
- **Affiliation 2:**
  - **Organization:** Institut Supérieur de l'Aéronautique et de l'Espace
  - **Affiliation Identifier:** `https://ror.org/04gyj6s21`
- **Source:** `CITATION.cff` (6th author), Zenodo v1.7.1 creators, DataCite creators; co-author of the EPSC-DPS 2025 Speasy abstract.
- **Affiliations — what supports them, and what does not.** Both affiliations above are values the live shared HSSI Person record carries; HSSI holds affiliations on a Person shared across software records rather than per record, so they reach Speasy from that shared Person. **Neither is stated anywhere in Speasy's repository**, which is silent on his affiliation, so neither is asserted here as a contribution-time affiliation. ORCID corroborates the two unevenly:
  - **Institut Supérieur de l'Aéronautique et de l'Espace** is directly corroborated: his ORCID record carries an employment at "Institut Supérieur de l'Aéronautique et de l'Espace (ISAE-SUPAERO)", Toulouse, disambiguated by ROR `https://ror.org/04gyj6s21` — the same identifier recorded above.
  - **Institut de Recherche en Astrophysique et Planétologie** is supported by the *department and city* of his other ORCID employment, which gives the organization name as "Conseil National de la Recherche Scientifique" but sets `department` to `Institut de Recherche en Astrophysique et Planétologie` and the city to Toulouse. **The trap in that entry, recorded so a later reader does not fall into it:** ORCID disambiguates it with Funder Registry ID `10.13039/501100007175`, which resolves to the **Lebanese** *Conseil* National de la Recherche Scientifique (CNRS-L), **not** the French *Centre* National de la Recherche Scientifique. That identifier is mis-selected upstream, and anyone following it alone lands on the wrong organization in the wrong country; the department and city are the reliable part of the entry, and they identify IRAP. The organization resolves by ROR `https://ror.org/05hm2ja81` to the IRAP row already held in HSSI, so no new organization is created.

**Note:** the ORCID display names are lowercased in some records (`nicolas aunai`, `nicolas andre`). The properly-cased, accented forms from `CITATION.cff` are used above.

---

### 7. Software Name (MANDATORY)
- **Value:** `Speasy`

**Source:** From existing HSSI record. Matches `CITATION.cff` `title:`, `pyproject.toml` `name = 'speasy'`, Zenodo/DataCite title, and the PyHC registry entry (`name: Speasy`). Submitted capitalization preserved.

---

### 8. Description (MANDATORY)
Submitted editorial wording, preserved verbatim:

> Speasy is a free and open-source Python package that makes it easy to find and load space physics data from a variety of data sources, whether it is online and public such as CDAWEB and AMDA, or any described archive, local or remote. This task, where any science project starts, would seem easy a priori but, considering the very diverse array of missions and instrument nowaday available, proves to be one of the major bottleneck, especially for students and newcomers. Speasy solves this problem by providing a single, easy-to-use interface to over 70 space missions and 65,000 products.

**Source:** From existing HSSI record. Still factually current: the README and `docs/index.rst` at the extraction revision continue to claim "over 70 space missions and 65,000 products", and the PyHC registry description is the same opening sentence. **No rewording proposed** — the description is submitted editorial content and is preserved verbatim.

**Correction to an earlier source note:** the grammar artifacts "nowaday" and "one of the major bottleneck" are **not** inherited from the current upstream text. They are legacy phrasing specific to the previously submitted HSSI description. The upstream README was grammatically corrected in commit `6caade95bbc325a99e29ccca04d8a2740d6add8c` ("Pick readme improvments from @nicolasaunai", 2023-10-30) and now reads "...considering the diverse array of missions and instruments available nowadays, it proves to be one of the major bottlenecks..." (`README.md:18-24`, `docs/index.rst:66-69`). The PyHC registry description reproduces only the first sentence and never contained the "bottleneck" clause at all.

**Considered and not selected:** replacing the submitted description with the current, grammatically corrected upstream README wording. The submitted value is factually accurate, so this was a question of editorial currency rather than a correctness fix, and the submitted wording is kept verbatim. A future agent should not re-propose the swap on grammar grounds alone.

---

### 9. Concise Description (OPTIONAL)
Submitted editorial wording, preserved verbatim:

> Space Physics made easy! A simple Python package to deal with main Space Physics WebServices (CDA, SSC, AMDA, CSA) providing easy access to over 70 space missions and 65,000 products.

**Source:** From existing HSSI record (183 characters — within the 200-character limit). The prior `hssi_metadata.md` had "made EASY!" (matching the README H1 "Space Physics made EASY"); live HSSI is authoritative for this scalar editorial field, so the submitted lowercase "easy!" is kept. Not a proposed change.

---

### 10. Publication Date (RECOMMENDED)
- **Value:** `2019-12-07`

**Source:** From existing HSSI record. Re-verified: GitHub API `created_at = 2019-12-07T14:24:03Z`.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** `Zenodo`
- **Publisher Identifier:** `https://zenodo.org`

**Source:** From existing HSSI record. Correct per the HSSI field guidance (DOI obtained via the GitHub-Zenodo workflow); DataCite `attributes.publisher = "Zenodo"`.

---

### 12. Version (RECOMMENDED)

Live HSSI holds `v1.6.1` (released 2025-09-05). Two releases have shipped since; all four subfields are refreshed.

| Subfield | Live HSSI (stale) | Proposed |
|---|---|---|
| Version Number | `v1.6.1` | `v1.7.1` |
| Version Date | `2025-09-05` | `2025-12-18` |
| Version PID | `https://doi.org/10.5281/zenodo.17065425` | `https://doi.org/10.5281/zenodo.17978034` |
| Version Description | 1.6.1 + 1.6.0 changelog | 1.7.1 + 1.7.0 changelog (below) |

- **Version Number:** `v1.7.1`
  Reason: v1.6.1 is two releases stale. Evidence: `VERSION` file = `1.7.1`; `pyproject.toml` `version = "1.7.1"`; `speasy/__init__.py` `__version__ = '1.7.1'`; `CITATION.cff` `version: 1.7.1`; newest git tag `v1.7.1`; DataCite concept DOI `attributes.version = "v1.7.1"`; Zenodo latest version `v1.7.1`.
  *HSSI display convention:* the live version entry is stored as `Speasy - v1.6.1`, so the refreshed entry becomes `Speasy - v1.7.1`.

- **Version Date:** `2025-12-18`
  Evidence: GitHub Releases API `v1.7.1 published_at = 2025-12-18T14:05:16Z`; Zenodo record 17978034 `metadata.publication_date = "2025-12-18"` and `created = 2025-12-18T14:05:35Z`; DataCite `dates[] Issued = 2025-12-18`; `CITATION.cff` `date-released: 2025-12-18`; git tag `v1.7.1` dated 2025-12-18.
  **Discrepancy found and resolved:** `HISTORY.rst` heads the section `1.7.1 (2025-12-25)`. That date is contradicted by four independent authoritative sources (GitHub release, Zenodo, DataCite, `CITATION.cff`) plus the git tag date, and is treated as a changelog typo. **`2025-12-18` is used.**

- **Version PID:** `https://doi.org/10.5281/zenodo.17978034`
  Reason: the superseded value is the v1.6.1 version DOI. Resolved from the concept DOI as instructed: `GET https://zenodo.org/api/records/4118780` resolves to the latest version, record **17978034**, with `"doi": "10.5281/zenodo.17978034"`, `"conceptdoi": "10.5281/zenodo.4118780"`, `"metadata.version": "v1.7.1"`. Independently confirmed by `CITATION.cff` `doi: 10.5281/zenodo.17978034`. **The v1.6.1 DOI `10.5281/zenodo.17065425` is NOT reused.**

- **Version Description:** formatted to match the style of the existing HSSI entry (version header, then `- <change> by @<author> in #<PR>`), covering both releases published since HSSI was last updated:

```
1.7.1
- Bump actions/checkout from 5 to 6 by @dependabot in #251
- Bump github/codeql-action from 2 to 4 by @dependabot in #252
- Bump codecov/codecov-action from 4 to 5 by @dependabot in #253
- Lazily use threading.get_native_id by @martinRenou in #255
- Use HTTPS everywhere possible (HTTP is rejected within WASM) by @jeandet in #256
- Adds a function to drop all cache entries for a specific cached function by @jeandet in #257
- Make Speasy init a bit more robust by @jeandet in #259
- Is server up wasm by @jeandet in #258
- Replace deprecated datetime utcxxx functions by xxx(tz=utc) by @jeandet in #261
- Fix Speasy crash when provider is disabled on the proxy by @jeandet in #262
1.7.0
- More cache control by @jeandet in #238
- Disable CDPP Themis archive since the connection is not that reliable by @jeandet in #239
- Increase proxy request timeout from 1 minute (default) to 5 minutes by @jeandet in #240
- Ensure identical requests deduplication on AMDA by @jeandet in #241
- Cache file timerange maping for direct archive modules by @jeandet in #243
- Fixes broken doctests (repr) by @jeandet in #242
- Actions update by @jeandet in #244
- Update contributing guidelines by @jeandet in #249
- Cleanup and coverage by @jeandet in #245
- add support for http proxies by @jeandet in #247
- Unlike the documentation says socks does not only return ProxyError by @jeandet in #250
```

**Source:** `HISTORY.rst`, GitHub Releases API, Zenodo record 17978034 description, DataCite `descriptions[0]`.

**Newer versions since v1.7.1:** none. `main` is at `7a6281ff` (2026-07-22) with substantial unreleased work (see the release-state caveat in the header); no v1.8.0 tag or Zenodo record exists.

---

### 13. Programming Language (RECOMMENDED)
- **Value:** `Python 3.x`

**Source:** From existing HSSI record. Re-verified; set-union with repo evidence yields no new value:
- `pyproject.toml` at HEAD: `requires-python = ">=3.10"` with classifiers for Python **3.10, 3.11, 3.12, 3.13, 3.14** (the repo's `CLAUDE.md` claim of ">=3.10" is confirmed).
- **Change since the prior extraction:** at the v1.7.1 release the floor was still `>=3.9` (classifiers 3.9-3.14); the bump to `>=3.10` and removal of the 3.9 classifier are post-release `main`-branch changes. The prior `hssi_metadata.md` listing of "3.9, 3.10, 3.11, 3.12, 3.13" is superseded by 3.10-3.14 — this affects only the note, not the field value.
- GitHub language breakdown: Python 659,690 B; Jupyter Notebook 20,204 B; Makefile 2,486 B. `Jupyter Notebook` is **not** an allowed HSSI value and the notebooks are documentation examples, so nothing is added. `Julia` is deliberately not added — `Speasy.jl` is a separate repository (Fields 29/30), not code in this one.

---

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found

**Source / reasoning:** No paper describing Speasy is designated by the project as its preferred citation. `CITATION.cff` has no `preferred-citation` block and points users at the software DOI (`message: "If you use this software, please cite it as below."` + `doi: 10.5281/zenodo.17978034`); the README's only DOI badge is the Zenodo concept DOI; the Zenodo and DataCite records carry no `IsDescribedBy` relation. There is no JOSS paper.

**Closest available item (recorded under Field 27 instead):** the developer-authored conference abstract *"SciQLop & Speasy: Open-Source Tools for Unified Planetary and Heliospheric Data Analysis"*, `https://doi.org/10.5194/epsc-dps2025-1422` (EPSC-DPS 2025, Crossref type `posted-content`). A conference abstract is not treated as a Reference Publication here. Promoting it to Field 14 was weighed and rejected: it is a meeting abstract rather than a paper describing the software, and the project designates no reference publication of its own. Field 14 therefore stays empty, and the abstract stays in Field 27.

---

### 15. License (RECOMMENDED)
- **License:** `MIT License`
- **License URI:** `https://spdx.org/licenses/MIT`

**Source:** Carried forward from the prior `hssi_metadata.md` and fully re-verified against the current repo and authoritative APIs:
- `LICENSE` — "MIT License / Copyright (c) 2024 Laboratory of Plasma Physics, Ecole Polytechnique, CNRS, Sorbonne Université, Université Paris-Saclay".
- `pyproject.toml` — `license = { file = "LICENSE" }` and classifier `License :: OSI Approved :: MIT License`.
- DataCite `rightsList[0]` — `{"rights": "MIT License", "rightsUri": "https://opensource.org/licenses/MIT", "rightsIdentifier": "mit", "rightsIdentifierScheme": "SPDX"}` (the License URI above is copied verbatim from here).
- Zenodo record 17978034 — `metadata.license.id = "mit-license"`. GitHub API — `license.spdx_id = "MIT"`. PyHC registry — license rating "Good".
- Historical check: `HISTORY.rst` 1.5.0 records "Switch to MIT license and drop last python 3.8 references", so MIT has been the license since v1.5.0 (2025-02-25) and is correct for both v1.6.1 and v1.7.1.

**SPDX identifier:** `MIT`. **Copyright holder:** Laboratory of Plasma Physics, Ecole Polytechnique, CNRS, Sorbonne Université, Université Paris-Saclay.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**From the existing HSSI record — 18, shown here in the capitalisation HSSI's view renders rather than the lowercase it stores:**
`Amda`, `Cdaweb`, `Cdf`, `Cdpp`, `Cnes`, `Esa`, `Nasa Api`, `Nasa Data`, `Plasma Physics`, `Pnst`, `Pyhc`, `Python 3`, `Satellite`, `Sciqlop`, `Space Physics`, `Space Plasma`, `Sscweb`, `Webservices`

**From PyHC curated keywords and fresh repo evidence — 11 (set-union):**

| Keyword | Evidence |
|---|---|
| `heliosphere` | PyHC registry `keywords` (curated, highest-trust source); README / `docs/index.rst` framing |
| `magnetosphere` | PyHC registry `keywords` (curated) |
| `data access` | PyHC `data_access`; `speasy.get_data` is the package's central API |
| `data retrieval` | PyHC `data_retrieval` |
| `csv` | PyHC `csv`; HAPI CSV codec (`bundled_codecs/hapi/csv/`), AMDA and UiowaEphTool CSV parsing — consistent with `Cdf` already being a keyword |
| `ascii` | PyHC `ascii`; ASCII/CSV parsing paths |
| `csa` | Dedicated CSA provider (`speasy/data_providers/csa/`), `docs/user/csa/csa.rst` — fills the gap beside the existing `Amda` / `Cdaweb` / `Sscweb` keywords |
| `ephemeris` | Three trajectory/ephemeris providers: SSCWeb, UiowaEphTool (`Trajectories.*`), CDPP 3DView; `uiowa_eph_tool.parse_trajectory` |
| `time series` | `SpeasyVariable` is a time-series container; `docs/user/scipy.rst`; README "Can retrieve time-series from AMDA, CDAWeb, CSA, SSCWeb" |
| `hapi` | `speasy/core/hapi/` client (capabilities / catalog / info / data) `[main-branch, unreleased as of v1.7.1]` plus the released HAPI CSV codec; `tests/test_hapi.py`, `tests/test_hapi_codecs.py` |
| `netcdf` | ISTP netCDF codec `speasy/core/codecs/bundled_codecs/istp/netcdf.py`, `tests/test_netcdf_codec.py` `[main-branch, unreleased as of v1.7.1]` |

**Note — considered and dropped:** `general`, `local`, `remote`, `web_service` (PyHC keywords, but too generic to function as science keywords; `Webservices` already covers the last), `python3` / `python-3` (duplicates of the existing `Python 3`), `data_container` (implementation detail), `wasm` / `pyodide` (runtime platform, not a science keyword), and the GitHub topics already represented by existing values (`amda`, `cdaweb`, `cnes`, `esa`, `nasa-api`, `plasma-physics`, `pnst`, `pyhc`, `sciqlop`, `space-physics`, `space-plasma`, `sscweb`).

*Casing note:* HSSI stores keywords in lowercase and title-cases them for display, so the Title-Case forms listed above are the rendered spelling, not the stored one. New values are written lowercase in their natural form.

---

### 17. Data Sources (OPTIONAL)

**From the existing HSSI record — 6:**
1. `AMDA` *(a custom value already in the HSSI vocabulary for this record, not one of the form's standard options)*
2. `CDAWeb`
3. `Observatory/Mission-specific`
4. `OMNIWeb`
5. `Other`
6. `SSCWeb`

**From repository evidence — 3:**

7. `TAP` — **released in v1.7.1.** `speasy/data_providers/csa/__init__.py` imports `from astroquery.utils.tap.core import TapPlus` (line 9) and builds the entire CSA inventory over IVOA TAP through `CSA = TapPlus(url=tapurl)` (line 108). Verified present at tag `v1.7.1`.

8. `HTTP/HTTPS Directories` — **released.** `speasy/core/any_files.py::list_files` scrapes `href="..."` entries out of remote directory index pages (`_HREF_REGEX`), with `os.listdir` for local paths; the Direct Archive module (`speasy/core/direct_archive_downloader/`, `speasy/data_providers/generic_archive/`) resolves `url_pattern` + `use_file_list` against HTTP(S) archive trees. Documented at `docs/user/direct_archive/direct_archive.rst`; exercised by `tests/test_direct_archive_downloader.py` and `tests/test_file_access.py`.

9. `HAPI` — **partially released**; the server client is `[main-branch, unreleased as of v1.7.1]`. `speasy/core/hapi/{client,provider,parser,exceptions}.py` implements a full HAPI client (`capabilities`, `catalog`, `about`, `info`, `data` endpoints with HAPI status-code handling for codes 1201/1400-1499/1500+), tested against live servers in `tests/test_hapi.py` (AMDA `https://amda.irap.omp.eu/service`, CDAWeb, and `hapi-server.org/servers/TestData3.3`). The HAPI **CSV** codec has shipped since v1.5.0 ("Basic HAPI CSV codec", `HISTORY.rst`) and the HAPI **binary** codec is on `main`. Scope caveat: the HAPI client is not yet wired into `get_data`/the dynamic inventory — `request_dispatch.py` registers only amda, cda, csa, ssc, archive, uiowaephtool, cdpp3dview.

**Note — considered and dropped:** `FTP/FTPS Directories` (no FTP support anywhere — `any_files.py` and `http.py` are HTTP(S)-only, and there are zero `ftp://` occurrences in the tree), `S3/Cloud-aware` (no boto3/fsspec, no `s3://`), `das2`, `The Virtual Solar Observatory`, `VirES` (no code or references). CSA, CDPP 3DView, the University of Iowa Cassini Ephemeris Tool, and YAML-described local/remote archives remain covered by the existing `Other`.

---

### 18. Input File Formats (RECOMMENDED)

**From the existing HSSI record — 4:** `ascii`, `CDF`, `csv`, `Other`

**From repository evidence — 2:**

5. `ISTP-Compliant` — **released.** Speasy's CDF reading is explicitly an ISTP layer: at tag `v1.7.1` the file is `speasy/core/codecs/bundled_codecs/istp_cdf.py`; on `main` a post-release directory reorganization moved it to `speasy/core/codecs/bundled_codecs/istp/cdf.py` (class `IstpCdf` in both) loads through `pyistp` and honours ISTP metadata (`DEPEND_n`, `VAR_TYPE`, `FILLVAL`, `VALIDMIN`/`VALIDMAX`, `LABL_PTR_n`, `*_PTR` attributes, and master/skeleton CDFs with a 7-day cache retention). `speasy/core/cdf/inventory_extractor.py` extracts inventories from ISTP master CDFs; `speasy/data_providers/cda/_inventory_builder/_cdf_masters_parser.py` parses CDAWeb ISTP masters; `docs/user/csa/csa.rst` states the CSA integration handles "both the webservice API and ISTP CDF file formats".

6. `netCDF3/4` — `[main-branch, unreleased as of v1.7.1]`. `speasy/core/codecs/bundled_codecs/istp/netcdf.py` (class `IstpNetCDF`) declares `supported_extensions = ["nc", "nc4"]` and `supported_mimetypes = ["application/x-netcdf", "application/netcdf"]`, and implements `load_variables` / `load_variable` / `list_variables`. Registered in `bundled_codecs/__init__.py` behind an optional `import netCDF4` (skipped on WASM, which has no netCDF4 wheel). Tested by `tests/test_netcdf_codec.py`, including a real CDAWeb-derived fixture `tests/resources/ac_h2s_mfi_cdaweb.nc`.

**Note — considered and dropped:** `JSON` — `speasy.core.inventory.indexes.to_json`/`from_json` and the HAPI/CSA JSON payloads are inventory-metadata and wire-protocol handling, not science-data file I/O (inventories are persisted through the disk cache, not JSON files). `HDF5` — reached only indirectly as netCDF4's container; there is no `h5py` dependency and no HDF5 API. `FITS`, `IDL.sav`, `Zarr` — no support. The existing `Other` continues to cover HAPI CSV/binary and the YAML archive-description files (`speasy/data/archive/*.yaml`).

---

### 19. Output File Formats (RECOMMENDED)

**From the existing HSSI record — 3:** `ascii`, `CDF`, `csv`

**From repository evidence — 3:**

4. `ISTP-Compliant` — **released.** `IstpCdf.save_variables` writes ISTP-structured CDFs via `pycdfpp` (at tag `v1.7.1`: `bundled_codecs/istp_cdf.py`; on `main`: `bundled_codecs/istp/cdf.py` after the post-release reorg): `_write_axis` / `_write_variable` emit `DEPEND_n` links, convert `datetime64[ns]` axes to `CDF_TIME_TT2000`, materialise `*_PTR` attributes as real variables, and support gzip variable compression. `tests/test_codecs.py` covers the round trip.

5. `netCDF3/4` — `[main-branch, unreleased as of v1.7.1]`. `istp/netcdf.py::save_variables` (line 129) implements writing; `tests/test_netcdf_codec.py` exercises write-then-read.

6. `Other` — HAPI **binary** output via `bundled_codecs/hapi/binary/writer.py::save_hapi_binary` (registered as codec `hapi/binary`) `[main-branch, unreleased as of v1.7.1]`, plus HAPI CSV output via `save_hapi_csv` (released — at tag `v1.7.1`: `bundled_codecs/hapi_csv/writer.py`; on `main`: `bundled_codecs/hapi/csv/writer.py` after the post-release reorg). Mirrors the `Other` already present in Input File Formats.

**Note:** every Speasy codec implements the same `CodecInterface` contract with `save_variables(variables, file=None)` returning a buffer when `file is None`, so each listed output format is genuinely writable rather than read-only.

---

### 20. Operating System (RECOMMENDED)

**From the existing HSSI record — 4:** `Linux`, `Mac`, `Operating System Independent`, `Windows`

**From repository evidence — 1:**

5. `Other` — WebAssembly / Pyodide in-browser runtime. **Released in v1.7.1** (verified: `speasy/core/platform.py` and `.github/workflows/wasm_tests.yml` both exist at the tag). Evidence: `speasy/core/platform.py::is_running_on_wasm()` (tests `platform.system() == "emscripten"`), WASM-specific branches in `speasy/core/http.py`, `core/cache/_function_cache.py`, `core/cache/_providers_caches.py`, `core/cache/_request_locker.py`; `pyproject.toml` gates `pysciqlop-cache` on `sys_platform != "emscripten"`; a dedicated CI workflow builds a wheel, loads a custom Pyodide 0.29.0 distribution with `pycdfpp` preinstalled, and runs `tests/test_wasm.py` in Chrome via `pytest-pyodide`, asserting `spz.core.platform.is_running_on_wasm()` and performing real `spz.get_data` calls (`amda/c1_b_gsm`, `amda/ace-imf-all`, `cdaweb/THA_L2_FGM/tha_fgl_gsm`, `sscweb/moon`). Two of the v1.7.1 changelog entries are WASM-driven.

**Source for those four:** From existing HSSI record; re-verified against `.github/workflows/tests.yml`, whose matrix is `os: [macos-latest, windows-latest, ubuntu-latest]` x `python-version: [3.10, 3.11, 3.12, 3.13, 3.14]`.

**Note:** `OS Independent` (the HSSI vocabulary's near-duplicate of `Operating System Independent`) is deliberately **not** added — the record already carries `Operating System Independent`, and adding both would create a duplicate. `MobilePlatform` and `Solaris` are unevidenced.

---

### 21. CPU Architecture (RECOMMENDED)
- **Value:** `CPU Independent`

**Source:** From existing HSSI record. Re-verified: Speasy is pure Python (built with `flit_core.buildapi`, no compiled extensions, no `platform_machine` environment markers). CI additionally demonstrates execution on x86-64 (ubuntu-latest, windows-latest), Apple Silicon arm64 (macos-latest), and WebAssembly (Pyodide). Those specific values are deliberately **not** added: `CPU Independent` already subsumes them, and enumerating them would add redundancy without search value. All binary-wheel dependencies (`numpy`, `scipy`, `pandas`, `matplotlib`, `pycdfpp`, `netCDF4`) publish wheels for these platforms.

---

### 22. Related Phenomena (OPTIONAL)
- **Value:** `Solar Wind`

**Reasoning:** an earlier source note for this field enumerated a stale list taken from the static form-fields reference. The live controlled vocabulary for Related Phenomena is: **Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission** — it contains no "Coronal Holes", and it does contain "Geomagnetic Storms" and "Solar Wind", which the stale list omitted.

Re-assessed against that live list: Speasy is deliberately phenomenon-agnostic — a data access layer plus a time-series container. There is no solar-feature code, no event detection, and no phenomenon-specific algorithm anywhere under `speasy/`. `Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`, `Solar Flares` and `X-ray emission` therefore have no repository support and remain excluded.

**`Solar Wind` is recorded, on a completeness argument.** The arguments weighed both ways were: in favor, Speasy's flagship documented products are solar-wind measurements (ACE/SWE, Wind/SWE, and the entire OMNI solar-wind dataset are among its headline examples, and `Interplanetary Space` is already an accepted Related Region), so an HSSI user searching "Solar Wind" arguably should find Speasy. Against: Speasy *transports* upstream solar-wind data rather than providing solar-wind science functionality — by that standard the value would be equally true of any generic CDAWeb/AMDA client and carries no distinguishing information about this software. The completeness argument prevailed: the field would otherwise be empty, `Solar Wind` is an exact controlled-vocabulary value, and discoverability for solar-wind data access is a genuine user benefit.

**`Geomagnetic Storms`** — excluded. Speasy ships no storm indices as a distinguishing capability and no storm-phase logic; the Kp/Dst-style products reachable through AMDA/OMNI are again pure upstream transport.

**Note — considered and dropped (custom entries are permitted for this field, so these were weighed explicitly):** the AMDA shared catalogs and timetables reachable through Speasy include event lists such as `Catalogs.SharedCatalogs.MARS.MEXShockCrossings` and `TimeTables.SharedTimeTables.EARTH.Event_list_tail_hall_reconnection_SC1` (used in `tests/test_amda_catalog.py` and `tests/test_amda_timetable.py`), which would suggest **custom** entries like "bow shock crossings" or "magnetic reconnection" (distinct from the official `Solar Wind` vocabulary row adopted above). These are **upstream data products that Speasy transports**, not science functionality Speasy provides for a phenomenon — the same entries would be equally true of any generic AMDA client, so they carry no information about this software. The `docs/examples/alfvenic.ipynb` "Alfvénic slow solar wind" topic is likewise an example notebook, not a capability.

---

### 23. Development Status (RECOMMENDED)
- **Value:** `Active`

**Source:** Carried forward from the prior `hssi_metadata.md` and re-verified against the current repo. Per repostatus.org, "Active" = has reached a stable, usable state and is being actively developed:
- `pyproject.toml` classifier `Development Status :: 5 - Production/Stable`.
- Release cadence: v1.5.0 (2025-02-25), v1.5.1 (2025-02-25), v1.5.2 (2025-06-03), v1.6.0 and v1.6.1 (2025-09-05), v1.7.0 (2025-11-25), v1.7.1 (2025-12-18).
- Ongoing development after the last release: `main` at `7a6281ff`, dated **2026-07-22**, carrying substantial new work (HAPI client, netCDF codec, CDPP 3DView provider, uv/Python-3.10 modernisation); GitHub `pushed_at = 2026-07-22T07:25:10Z`; 53 open issues; Dependabot active (three dependency bumps in v1.7.1 alone).
- Maintained CI (3 operating systems x 5 Python versions, plus a separate WASM job, plus scheduled Monday/Wednesday runs) and maintained ReadTheDocs documentation.
- PyHC registry ratings: software_maturity **Good**, testing **Good**, documentation **Good**, python3 **Good**, license **Good** (community: Partially met).
- GitHub `archived = false`.

Not `Inactive` or `Unsupported` (development is ongoing), not `WIP` (there are stable public releases on PyPI), not `Moved` (the repository URL is current).

---

### 24. Documentation (RECOMMENDED)
- **Value:** `https://speasy.readthedocs.io/en/stable/`

**Source:** From existing HSSI record — submitted value preserved. The URL resolves, and serves the project's stable documentation. The README's "Documentation and examples" section links to exactly this `/en/stable/` URL, and `.readthedocs.yaml` is present in the repo root. The PyHC registry lists the unversioned `https://speasy.readthedocs.io/`, and the prior `hssi_metadata.md` also used the unversioned form; the submitted `/en/stable/` form is more precise and is kept. The examples gallery `https://speasy.readthedocs.io/en/latest/examples/index.html` also resolves but is not added, since Field 24 takes a single URL.

---

### 25. Funder (OPTIONAL)
- **Organization:** `CDPP (Centre de Données de la Physique des Plasmas)`
- **Funder Identifier:** `https://cdpp.irap.omp.eu/`

**Source:** From existing HSSI record. Re-verified against the README "Credits" section: "The development of Speasy is supported by the CDPP (http://www.cdpp.eu/)."

**Notes:**
- **No ROR exists for CDPP.** The ROR v2 API returns 0 results for the exact phrase "Centre de Données de la Physique des Plasmas", and broader CDPP-related queries return only unrelated plasma-physics institutes. The existing non-ROR URL identifier is therefore the best available value and is kept unchanged.
- Per the acronym-expansion guidance the preferred organization form would be the expanded `Centre de Données de la Physique des Plasmas` without the leading acronym. This is a **cosmetic** difference from the submitted value and is **not** proposed as a change.
- Zenodo and DataCite `fundingReferences` are both empty, so no additional funder can be substantiated. CNES appears only as a GitHub topic/keyword (CDPP is CNES/CNRS-operated) and is **not** asserted as a funder.

---

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

**Reasoning:** No award or grant information exists in any source. DataCite `fundingReferences = []`; the Zenodo record carries no grants; and the repository (README Credits, `AUTHORS.rst`, `HISTORY.rst`, `docs/`) names CDPP as a supporter without any award title or number. Deliberately not fabricated.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Values — 1.** Entry 1 below is the recorded value. Entry 2 is a documented omission, kept here with the evidence and the reason it is excluded.

1. `https://doi.org/10.5194/epsc-dps2025-1422`
   *Jeandet, A., Renard, B., Aunai, N., Ghisalberti, A., Génot, V., André, N., & Bouchemit, M. (2025). SciQLop & Speasy: Open-Source Tools for Unified Planetary and Heliospheric Data Analysis. Europlanet Science Congress-DPS Joint Meeting 2025. https://doi.org/10.5194/epsc-dps2025-1422*
   **Evidence:** a **developer-authored publication that describes Speasy**. The author list matches `CITATION.cff` (Jeandet, Renard, Aunai, Génot, André), and the abstract states that "SciQLop … and its data engine Speasy address this challenge by enabling seamless access, visualization, and correlation of datasets from multiple servers and archives (e.g., AMDA, CDAWeb, CSA)". Verified via the Crossref API (type `posted-content`, published 2025-07-09). Recorded here rather than in Field 14 because it is a conference abstract rather than a designated reference publication.

2. `https://doi.org/10.1051/0004-6361/202141095`
   *Louarn, P., Fedorov, A., Prech, L., Owen, C. J., et al. (2021). Multiscale views of an Alfvénic slow solar wind: 3D velocity distribution functions observed by the Proton-Alpha Sensor of Solar Orbiter. Astronomy & Astrophysics. https://doi.org/10.1051/0004-6361/202141095*
   **Evidence:** the developers ship an example-gallery notebook, `docs/examples/alfvenic.ipynb`, whose title and opening cell cite this paper by DOI and whose analysis it reproduces using Speasy (`amda/solo_b_rtn_hr`, `pas_l2_omni`). Verified via Crossref.
   **Omitted, and why:** this paper does not itself describe or cite Speasy — it is the science result that a documented Speasy example reproduces. Field 27 is read strictly as "publications that describe, cite, or use the software", and this paper meets none of the three. It is deliberately not one of this field's values, and is retained here as documented evidence so that a future agent does not re-propose it.

**Note — considered and dropped:** the AMDA reference papers `https://doi.org/10.1016/j.pss.2021.105214` (Génot et al. 2021, *Automated Multi-Dataset Analysis (AMDA)*) and `https://doi.org/10.1007/978-90-481-3499-1_16` (Jacquey et al. 2009) describe an upstream **data service** that Speasy consumes, not Speasy itself; they belong on AMDA's own record. The Zenodo and DataCite records for Speasy contain no publication-type `relatedIdentifiers` — only `IsSupplementTo` the GitHub tag plus 20+ `HasVersion` sibling-release DOIs, which are versions, not publications.

---

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found

**Reasoning:** Speasy exposes **65,000+ products across 70+ missions** through inventories built dynamically at runtime from AMDA, CDAWeb, CSA, SSCWeb, CDPP 3DView and UiowaEphTool. There is no bounded, meaningful dataset list to record, and no dataset DOIs appear in any Speasy metadata source (the Zenodo/DataCite `relatedIdentifiers` contain no `Dataset` entries).

**Concrete enrichment opportunity deliberately left for a human** (not performed, to avoid recording unverified identifiers): `speasy/data/archive/cda.yaml` ships exactly 14 hard-coded dataset definitions that could each be resolved to an `hpde.io` dataset identifier — `erg_lepe_l3_pa`, `erg_pwe_hfa_l3_1min`, `mms{1,2,3,4}_fgm_srvy_l2`, `mms{1,2,3,4}_fpi_brst_l2_des_moms`, and `mms{1,2,3,4}_fpi_fast_l2_des_moms`. Every one would need its `hpde.io` URL individually verified before submission.

---

### 29. Related Software (OPTIONAL)

**Values — 5.** Every entry below passed the Field 29/30 relevance gate; the gate reasoning is given per entry, and every rejection is recorded in the Note for audit purposes.

1. `https://doi.org/10.5281/zenodo.7379012` — **SciQLop** (Zenodo concept DOI; repo `https://github.com/SciQLop/SciQLop`)
   **Gate: PASSES — companion application.** The README's second paragraph is "Don't want to write code? See our graphical interface SciQLop", and the developers' own EPSC-DPS 2025 abstract describes Speasy as SciQLop's "data engine". `plan/REVIEW.md` also documents the shared community proxy server. Distinguishing and specific to Speasy, not generic.

2. `https://github.com/SciQLop/Speasy.jl` — **Speasy.jl**
   **Gate: PASSES — cross-language wrapper of this exact package.** Advertised in the README main-features list ("Also available as Speasy.jl for Julia users") and in `docs/index.rst`; introduced by `HISTORY.rst` 1.5.0 ("docs: mention julia wrapper"). No Zenodo DOI was found, so the repository URL is used as the form permits.

3. `https://github.com/SciQLop/PyISTP` — **PyISTP**
   **Gate: PASSES — domain-specific important dependency.** `pyproject.toml` pins `pyistp>=0.8.2`, and it is the ISTP-compliance engine behind both codecs (`bundled_codecs/istp/cdf.py`, `istp/netcdf.py`, `istp/__init__.py`), inventory extraction (`core/cdf/inventory_extractor.py`), the CDAWeb master-CDF parser, and the generic archive provider. A heliophysics-specific library whose presence characterises the software; `HISTORY.rst` tracks PyISTP version bumps as user-visible changes (e.g. 1.6.0 "Bump PyISTP to cover cases where axis data is in master CDF").

4. `https://doi.org/10.5281/zenodo.6391115` — **pycdfpp / CDFpp** (Zenodo concept DOI; repo `https://github.com/SciQLop/CDFpp`)
   **Gate: PASSES — domain-specific dependency (heliophysics CDF-format library).** Imported directly in `bundled_codecs/istp/cdf.py` and `core/cdf/inventory_extractor.py` for reading and writing CDF, including `CDF_TIME_TT2000` conversion and gzip variable compression; the WASM CI job uses a custom-built Pyodide distribution specifically to preinstall `pycdfpp`. Also identified in the PyHC context as related CDF software by the same author.

5. `https://github.com/astropy/astroquery` — **astroquery**
   **Gate: PASSES — domain-specific important dependency, not generic infrastructure.** It is not arrays, dataframes, plotting or HTTP plumbing: `speasy/data_providers/csa/__init__.py` imports `astroquery.utils.tap.core.TapPlus` and builds the **entire** CSA (Cluster / Double Star) inventory over the IVOA TAP protocol. `request_dispatch.py::init_csa` even disables the whole CSA provider when `HTTP_PROXY` is set, citing astroquery issue #3228 — an astroquery limitation directly shapes Speasy's user-facing behaviour. Verified present at tag `v1.7.1`.

**Note — considered and REJECTED (audit trail):**
- **Tier A, always excluded — being a dependency is not relatedness:** `numpy`, `scipy`, `pandas`, `matplotlib`, `requests`, `python-dateutil`, `tqdm`, `PyYAML`, `packaging`, `urllib3`, `certifi`, `appdirs`, `humanize`, `pysocks`, `pytest`, `pytest-cov`, `ddt`, `flit_core`. Every one of these would read identically for an arbitrary Python package.
- **`pysciqlop-cache`** — a same-authors library, but it is a **cache**: it passes the "would this be equally at home in a web app, a finance model, or a biology pipeline?" test, so it is generic infrastructure despite the shared origin. Excluded from both Fields 29 and 30.
- **`diskcache`, `pyzstd`, `netCDF4`, `watchdog`, `IPython`, sphinx/docs toolchain** — generic infrastructure or build/test tooling. `netCDF4` is Tier B and is used only *internally* to implement the netCDF codec, which is explicitly insufficient.
- **AMDA, CDAWeb, CSA, SSCWeb, CDPP 3DView, University of Iowa Cassini Ephemeris Tool** — these are **web services / data sources**, not installable software; they are recorded in Field 17 and Fields 31/32 instead.
- **`hapiclient`, `hapiplot`, `pysat`, `pySPEDAS`, `sunpy`, `cdasws`** — plausible "performs similar tasks" peers, but **the repository references none of them**, so listing them would be speculation. `plan/BACKLOG.md` lists an unimplemented "PySPEDAS interface" wish (GH #235) — an unbuilt plan is not a relationship.
- **Blanket ecosystem claims** ("part of the scientific Python ecosystem", "a PyHC member, therefore interoperable with PyHC packages") were not used anywhere as justification.

---

### 30. Interoperable Software (OPTIONAL)

**Values — 3.** This field is gated on a *demonstrated exchange*, not on dependency presence; the specific evidence is named for each entry.

1. `https://doi.org/10.5281/zenodo.7379012` — **SciQLop** (repo `https://github.com/SciQLop/SciQLop`)
   **Demonstrated exchange:** SciQLop is a peer application that runs *on top of* Speasy. The developers' EPSC-DPS 2025 abstract states "SciQLop, powered by Speasy, streamlines access to heterogeneous datasets"; the README directs non-programmers to SciQLop as the GUI over the same data engine; and both share the SciQLOP community proxy/cache server (`speasy/core/proxy/`, `CDPP3DVIEW_MIN_PROXY_VERSION`, and the README uptime badge for `sciqlop.lpp.polytechnique.fr/cache`). A host/plugin relationship between two domain tools, not a runtime coincidence.

2. `https://github.com/SciQLop/Speasy.jl` — **Speasy.jl**
   **Demonstrated exchange:** an explicit **cross-language bridge** — a Julia wrapper that calls this package and surfaces `SpeasyVariable` data to Julia users. Advertised in the README feature list and in `docs/index.rst`.

3. `https://github.com/astropy/astropy` — **astropy** *(Tier B — admitted only with cited evidence, which exists here)*
   **Demonstrated exchange via a documented public adapter API, not internal use:** `SpeasyVariable.to_astropy_table() -> astropy.table.Table` (`speasy/products/variable.py`, line 578) is a documented public conversion, constructing the table with per-column units through `astropy.table.Table.from_pandas(df, units=umap, index=True)`. `SpeasyVariable.unit_applied(unit=None)` returns a variable whose values are `astropy.units.Quantity` objects (docstring: "values converted to astropy.units.Quantity according to given or found unit"). `docs/examples/SSCWeb.ipynb` imports `astropy.units` and combines it with Speasy output. This is a genuine data-model exchange and clears the Tier B bar.

**Note — considered and REJECTED:**
- **`pandas`** — Tier A, no exceptions, even though `to_dataframe()` / `from_dataframe()` exist and the README advertises DataFrame-like behaviour. The rule is explicit and absolute.
- **`numpy`** — Tier A, even though `SpeasyVariable` implements `__array_function__` / `__array_ufunc__` and supports NumPy operations (`docs/user/numpy.rst`). "Interoperates with numpy" is true of nearly every HSSI package and distinguishes nothing.
- **`matplotlib`** — Tier A; "uses matplotlib for all plotting" is the worked counter-example in the field definition.
- **`netCDF4`, `xarray`** — `netCDF4` is used internally to implement a codec (insufficient per Tier B); `xarray` is not used at all.
- **`Jupyter` / `IPython`** — Tier B bar not met: `_repr_pretty_` rich display, notebook examples, and MyBinder/Colab badges are documentation and display-protocol conveniences, equally true of most packages.
- **`Pyodide`** — a runtime/platform (recorded under Field 20 `Other`), not a peer domain tool.
- **`PyISTP`, `pycdfpp`, `astroquery`** — genuine domain dependencies, so they are recorded under Field 29; they are libraries Speasy *calls*, not peer tools it exchanges data with, and are therefore not duplicated here.

---

### 31. Related Instruments (OPTIONAL)

**Values — 19.** Every entry is resolved to exactly one SPASE row and recorded with that row's canonical `name` copied verbatim plus its SPASE `identifier` (the reliable de-duplication key on submission). Entries are drawn from HSSI's SPASE-backed instrument vocabulary (its `type = 1` rows); where an identifier exists in both a bare and an `.html` form, the two are treated as one resource and the bare identifier is used.

**Relevance gate applied.** Each instrument listed is one for which the package ships **instrument-specific support** — either hard-coded dataset definitions in `speasy/data/archive/cda.yaml` (per-instrument master CDF URL, filename regex, split rule and cadence) or a README/`docs` worked example backed by regression tests that retrieve that instrument's data. The resulting set is exactly the prior canonical file's list minus one entry that is no longer supported (see the Note).

**ACE — 1**

| # | Instrument Name (verbatim) | Instrument Identifier | Evidence |
|---|---|---|---|
| 1 | `ACE Magnetic Field Instrument` | `https://spase-metadata.org/SMWG/Instrument/ACE/MAG` | README quickstart `spz.get_data('amda/imf', ...)` and `amda_tree.Parameters.ACE.MFI.ace_imf_all.imf`; `tests/test_cdaweb.py` uses `tree.cda.ACE.MAG.AC_H2_MFI.BGSEc`; `tests/test_amda_parameter.py` uses `ACE.MFI.ace_imf_all.{imf, imf_gsm, imf_mag}` and `ACE.MFI.ace_mag_real.imf_real_gse`. Unique exact-name match. |

**Wind — 2**

| # | Instrument Name (verbatim) | Instrument Identifier | Evidence |
|---|---|---|---|
| 2 | `Wind Magnetic Field Investigation` | `https://spase-metadata.org/SMWG/Instrument/Wind/MFI` | README multi-product example `tree.cda.Wind.WIND.MFI.WI_H2_MFI.BGSE`; also in `docs/index.rst`. Two same-named rows exist (SMWG + CNES/CDPP-AMDA); resolved to SMWG per the tie-breaker, and recording the identifier removes the ambiguity. |
| 3 | `Wind Solar Wind Experiment` | `https://spase-metadata.org/SMWG/Instrument/Wind/SWE` | README multi-product example `tree.amda.Parameters.Wind.SWE.wnd_swe_kp.{wnd_swe_vth, wnd_swe_pdyn, wnd_swe_n}`; also in `docs/index.rst`. Unique exact-name match (abbreviation `SWE`). |

**MMS — 16 (4 spacecraft x 4 instruments)**

SPASE models MMS instruments **per spacecraft**, so each instrument yields four rows that share one canonical name. Speasy supports all four observatories (`cda.yaml` ships `mms1`-`mms4` definitions), so all four are listed; the identifiers disambiguate them.

| # | Instrument Name (verbatim) | Instrument Identifier |
|---|---|---|
| 4 | `MMS FIELDS/FGM` | `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/FGM` |
| 5 | `MMS FIELDS/FGM` | `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/FGM` |
| 6 | `MMS FIELDS/FGM` | `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/FGM` |
| 7 | `MMS FIELDS/FGM` | `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/FGM` |
| 8 | `MMS FPI/DES` | `https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DES` |
| 9 | `MMS FPI/DES` | `https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DES` |
| 10 | `MMS FPI/DES` | `https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DES` |
| 11 | `MMS FPI/DES` | `https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DES` |
| 12 | `MMS FPI/DIS` | `https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DIS` |
| 13 | `MMS FPI/DIS` | `https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DIS` |
| 14 | `MMS FPI/DIS` | `https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DIS` |
| 15 | `MMS FPI/DIS` | `https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DIS` |
| 16 | `MMS FIELDS/SCM` | `https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/SCM` |
| 17 | `MMS FIELDS/SCM` | `https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/SCM` |
| 18 | `MMS FIELDS/SCM` | `https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/SCM` |
| 19 | `MMS FIELDS/SCM` | `https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/SCM` |

**MMS evidence (all released in v1.7.1):**
- **FGM:** `speasy/data/archive/cda.yaml` ships `mms{1..4}_fgm_srvy_l2` with the FGM master CDF, `url_pattern`, `split_rule: regular` and `use_file_list: true` — i.e. hard-coded knowledge of FGM L2 survey file naming, versioning and cadence. README example `MMS1_FGM_SRVY_L2.mms1_fgm_b_gse_srvy_l2_clean`; tests `archive/cda/MMS/MMS1/FGM/SRVY/...`, `cda/MMS2_FGM_SRVY_L2/...`, `tree.cda.MMS.MMS1.FGM.MMS1_FGM_SRVY_L2....`
- **FPI/DES:** `cda.yaml` ships `mms{1..4}_fpi_brst_l2_des_moms` and `mms{1..4}_fpi_fast_l2_des_moms` (with `fname_regex`, `split_frequency: monthly`, `split_rule: random`). README examples `MMS1_FPI_FAST_L2_DES_MOMS.{mms1_des_bulkv_gse_fast, mms1_des_temppara_fast, mms1_des_tempperp_fast, mms1_des_energyspectr_omni_fast}`; tests `archive/cda/MMS/MMS1/FPI/{BURST,FAST}/MOMS/...`; AMDA `MMS.MMS1.FPI.fast_mode.mms1_fpi_desmoms.mms1_des_omni` and `MMS3...mms3_des_tpara`.
- **FPI/DIS:** README example `MMS1_FPI_FAST_L2_DIS_MOMS.mms1_dis_energyspectr_omni_fast`; `docs/examples/CDAWeb.ipynb` renders `mms1_dis_energyspectr_omni_fast` as a spectrogram; the README resampling example uses `mms1_dis_tempperp_fast` / `mms1_dis_temppara_fast`; AMDA `mms1_fpi_dismoms.mms1_dis_omni`.
- **SCM:** README example `MMS1_SCM_SRVY_L2_SCSRVY.mms1_scm_acb_gse_scsrvy_srvy_l2`; test product `cdaweb/MMS2_SCM_SRVY_L2_SCSRVY/mms2_scm_acb_gse_scsrvy_srvy_l2`.

**Two genuinely supported instruments are deliberately omitted, because the SPASE vocabulary has no row for either:**
- **Arase/ERG LEPE** (Low-Energy Particle experiments - Electron analyzer) — `cda.yaml` ships `erg_lepe_l3_pa` with the ERG LEPE L3 pitch-angle master CDF and URL pattern.
- **Arase/ERG PWE/HFA** (Plasma Wave Experiment - High Frequency Analyzer) — `cda.yaml` ships `erg_pwe_hfa_l3_1min`; exercised by `tests/test_direct_archive_downloader.py`, `tests/test_direct_archive_inventory.py`, `tests/test_codecs.py`, and `tree.archive.cda.Arase_ERG.PWE.HFA.erg_pwe_hfa_l3_1min.ne_mgf`.

  The vocabulary contains the **observatory** row `SMWG/Observatory/ARASE` (added under Field 32) but **zero Arase/ERG instrument rows**. Recording these as bare names would create new identifierless, non-SPASE instrument rows in HSSI's controlled vocabulary, so they are omitted instead. The omission is documented rather than silent: both are genuinely supported, and both should be revisited if Arase/ERG instrument rows appear in a later upstream vocabulary refresh.

**Note — considered and dropped (relevance gate), with reasons:**
- **`ACE Solar Wind Electron Proton Alpha Monitor` (SWEPAM)** — present in the prior `hssi_metadata.md` as "ACE/SWE", but **the current repository provides no evidence for it**: no README or docs example and no test references it (only ACE MFI and ACE Ephemeris appear). Per the seeding rule, file-only additions are carried forward *only where the repository still supports them*, so this one is **dropped**. Recorded here so the removal is visible rather than silent. (Note it is absent from live HSSI too, so no existing HSSI value is being removed.)
- **Single-fixture instruments** — each appears exactly once, as an incidental regression-test fixture for a *generic* feature rather than as instrument-specific support: MMS FEEPS (`cda/MMS1_FEEPS_SRVY_L2_ELECTRON/...`), Cluster FGM and CIS-HIA (`tree.csa.Cluster.Cluster_1.CIS_HIA1....`, `tree.cda.Cluster.C1.FGM_SPIN....`), Cluster EFW (`csa/C1_CP_EFW_L3_P/...`), Solar Orbiter SWA-PAS (`tree.cda.Solar_Orbiter.SOLO.SWA_PAS....`), PSP IS-IS/EPI-Lo (`cda/PSP_ISOIS-EPILO_L2-PE/...`), STEREO HET (`cda/STA_L1_HET/Proton_Flux`, added purely as the fix for GH #223), THEMIS ESA/FGM/SCM, MAVEN STATIC, Juno JEDI, Equator-S MAM, Wind 3DP, ACE Ephemeris.
- **Values belonging to other fields:** generic multi-instrument file formats (CDF / netCDF / ISTP) -> Fields 18/19; multi-mission archives (CDAWeb, AMDA, CSA, SSCWeb) -> Field 17.

---

### 32. Related Observatories (OPTIONAL)

**16 values.** Each resolves to exactly one SPASE row (`type = 2`), with the canonical `name` copied verbatim.

**From the existing HSSI record — 9.** The exact SPASE row each one corresponds to is identified below, and each was re-verified as still supported by the repository at the extraction revision.

| # | Observatory Name (verbatim) | Observatory Identifier | Still-supported evidence |
|---|---|---|---|
| 1 | `Advanced Composition Explorer` | `https://spase-metadata.org/SMWG/Observatory/ACE` | README quickstart (`amda/imf`), `tree.cda.ACE.MAG`, `ssc.Trajectories.ace` |
| 2 | `Cluster` | `https://spase-metadata.org/SMWG/Observatory/Cluster` | CSA provider + `docs/user/csa/csa.rst`; `amda/c1_b_gsm`, `csa/C1_CP_EFW_L3_P/...`, `tree.cda.Cluster.C1.FGM_SPIN` |
| 3 | `International Solar Polar Mission` | `https://spase-metadata.org/SMWG/Observatory/Ulysses` | `uiowa_eph_tool` hard-codes `"Ulysses": "ulys"` in the Sun/Earth/Jupiter/Saturn observer tables; named in `docs/user/data_providers.rst` and `docs/user/Uiowa_eph_tool/uiowa_eph_tool.rst` |
| 4 | `ISTP/Wind` | `https://spase-metadata.org/SMWG/Observatory/Wind` | README and `docs/index.rst` examples (`WI_H2_MFI.BGSE`, `wnd_swe_*`, `ssc.Trajectories.wind`), `cda/WI_SFSP_3DP/FLUX` |
| 5 | `Magnetospheric Multiscale` | `https://spase-metadata.org/SMWG/Observatory/MMS` | `cda.yaml` ships 12 MMS1-4 dataset definitions; README multi-panel example; extensive tests |
| 6 | `Mars Atmosphere and Volatile EvolutioN` | `https://spase-metadata.org/SMWG/Observatory/MAVEN` | `tree.amda.Parameters.MAVEN.STATIC.mavpds_sta_c6.mav_sta_c6_energy` (`tests/test_amda_parameter.py`); named in the developers' EPSC-DPS 2025 abstract |
| 7 | `OMNI` | `https://spase-metadata.org/SMWG/Observatory/OMNI` | OMNI products in `tests/test_amda.py`, `test_amda_parameter.py`, `test_codecs.py`, `test_direct_archive_downloader.py`; `OMNIWeb` also present in Field 17 |
| 8 | `Parker Solar Probe` | `https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe` | `cda/PSP_ISOIS-EPILO_L2-PE/Electron_Counts_ChanE` (`tests/test_cdaweb.py`); PSP products in AMDA tests |
| 9 | `Solar Orbiter` | `https://spase-metadata.org/ESA/Observatory/SolarOrbiter` | `docs/index.rst` SSCWeb example (`Trajectories.solarorbiter`); `tree.cda.Solar_Orbiter.SOLO.SWA_PAS.SOLO_L2_SWA_PAS_GRND_MOM`; `docs/examples/{solo_epd,alfvenic}.ipynb`; direct-archive and file-access tests |

*Resolution notes for those nine:* `Cluster`, `International Solar Polar Mission`, `OMNI` and `Parker Solar Probe` each have 2-3 same-named rows in the vocabulary; the SMWG-namespace tie-breaker selects exactly the row already bound in HSSI. `Solar Orbiter` has no SMWG row — the bound row is `ESA/Observatory/SolarOrbiter`, matching the documented expectation. Recording the identifiers makes all nine unambiguous on submission.

**From repository evidence — 7:**

| # | Observatory Name (verbatim) | Observatory Identifier | Evidence (all released in v1.7.1) |
|---|---|---|---|
| 10 | `Time History of Events and Macroscale Interactions during Substorms` | `https://spase-metadata.org/SMWG/Observatory/THEMIS` | The broadest test coverage of any addition — THEMIS products are retrieved in **five** test files: `tests/test_amda_parameter.py` (`amda.Parameters.THEMIS.THEMIS_A.ESA.tha_peim_all.tha_n_peim`), `tests/test_speasy.py` (`THEMIS.THEMIS_A.FGM.tha_fgm_s.tha_bs_gsm`), `tests/test_speasy_variable.py` (`cda.THEMIS.THC.L2.THC_L2_ESA.thc_peif_t3`), `tests/test_cdaweb.py` and `tests/test_wasm.py` (`cdaweb/THA_L2_FGM/tha_fgl_gsm`). `tests/test_direct_archive_downloader.py` additionally uses real `themis.ssl.berkeley.edu/data/themis/thb/l2/...` URL patterns and master CDFs as its archive fixtures. The package also ships `speasy/data/archive/themis_cdpp.yaml.example`, `docs/user/direct_archive/direct_archive.rst` is built around THEMIS, and `docs/examples/SSCWeb.ipynb` fetches `Trajectories.themisb`. The canonical SMWG name is the long form. |
| 11 | `Exploration of energization and Radiation in Geospace` | `https://spase-metadata.org/SMWG/Observatory/ARASE` | The strongest evidence class available: `speasy/data/archive/cda.yaml` — shipped inside the package — hard-codes Arase/ERG dataset definitions (`erg_lepe_l3_pa`, `erg_pwe_hfa_l3_1min`) with master CDFs, URL patterns and split rules under `inventory_path: cda/Arase_ERG/...`; verified present at tag `v1.7.1`. Exercised by `tests/test_direct_archive_downloader.py`, `test_direct_archive_inventory.py`, `test_codecs.py`, `test_cdaweb.py` and `test_amda_parameter.py`. (The `.html` duplicate row was normalised; the bare row's name is used.) |
| 12 | `Cassini Orbiter` | `https://spase-metadata.org/SMWG/Observatory/Cassini` | `speasy/data_providers/uiowa_eph_tool/__init__.py` hard-codes `"Cassini": "cass"` in every observer table (Sun, Venus, Earth, Jupiter, Saturn and all moon origins); `docs/user/data_providers.rst` and `docs/user/Uiowa_eph_tool/uiowa_eph_tool.rst` name the provider "University of Iowa **Cassini** Ephemeris Tool ... provides trajectories for Cassini, Ulysses, Voyager 1, and Voyager 2"; `tests/test_uiowa_eph_tool.py` and `tests/test_speasy.py` retrieve `Trajectories.{Callisto.Co_rotational, Saturn_baricentric.KSM, Sun.Ecliptic}.Cassini`; also in `tests/test_cdpp3dview.py`. |
| 13 | `Voyager 1 & 2` | `https://spase-metadata.org/SMWG/Observatory/Voyager` | `uiowa_eph_tool` hard-codes `"Voyager 1": "voy1"` and `"Voyager 2": "voy2"` in the Sun, Earth, Jupiter, Saturn, Jupiter-satellite and satellite-satellite observer tables; both are named in `docs/user/data_providers.rst` and the UiowaEphTool doc page. The single mission-level SPASE row is used deliberately (unique exact name). The per-spacecraft alternatives `SMWG/Observatory/Voyager1` and `.../Voyager2` were weighed and rejected: both are canonically named "Mariner Jupiter/Saturn A" and "... B", so recording them would file the mission under names that appear nowhere in Speasy or its documentation. |
| 14 | `Galileo Orbiter-Probe` | `https://spase-metadata.org/SMWG/Observatory/Galileo` | `uiowa_eph_tool` hard-codes `"Galileo": "gali"` in the Sun, Venus, Earth, Jupiter and Jupiter-satellite observer tables; `tests/test_uiowa_eph_tool.py` retrieves `Trajectories.Io.Geographic.Galileo`; also in `tests/test_cdpp3dview.py`. Unique exact-name match. |
| 15 | `Double Star Mission` | `https://spase-metadata.org/SMWG/Observatory/DoubleStar` | `docs/user/csa/csa.rst`: "The Cluster Science Archive (CSA) provides access to all science and support data from the ongoing Cluster (2000-present) and **Double Star (2004-2008)** missions. Its integration into Speasy makes it easy to get any public data from the CSA, handling both the webservice API and ISTP CDF file formats." Repeated in `docs/user/data_providers.rst` ("CSA - Cluster and Double Star mission data") and `docs/examples/CompleteDemo.ipynb`. A documented statement of which missions a shipped provider covers. Three candidate rows exist; the **mission-level** row (unique exact name "Double Star Mission") is used rather than the per-spacecraft `DoubleStar1`/`DoubleStar2` rows, which are both named "Double Star". |
| 16 | `Juno Orbiter` | `https://spase-metadata.org/SMWG/Observatory/Juno` | **Moderate confidence — two independent sources.** (a) `tests/test_amda.py::test_get_templated_parameter` retrieves the Juno JEDI product `jedi_i90_flux` and asserts the templated result `jedi_i90_flux_4` — Juno data is the fixture for Speasy's AMDA templated-parameter feature; (b) the developers' own EPSC-DPS 2025 abstract names Juno as a driving mission ("The surge of planetary and heliospheric data from missions like MAVEN, Juno, and Solar Orbiter..."). Also present in `docs/examples/{alfvenic, CompleteDemo, CDAWeb, Cdpp3dView}.ipynb`. Unique exact-name match (the alternative row is `CNES/Observatory/CDPP-AMDA/Juno`, named just "Juno"). **This is the weakest-evidenced entry in the field**, and it is kept deliberately: two independent sources clear the designed-to-support gate, though by a narrower margin than any other entry here. |

**Note — considered and dropped (relevance gate), with reasons:**
- **Appear only inside auto-generated inventory dumps in example notebooks** — `docs/examples/Cdpp3dView.ipynb` and `SSCWeb.ipynb` print whole trajectory catalogues, which name dozens of bodies: Geotail, Polar, IMP-8, Interball, Van Allen Probes/RBSP, Rosetta, SDO, SOHO, Venus Express, Mars Express, Dimorphos/Didymos, Halley, 67P, and many moons. A catalogue listing is not designed-to-support.
- **Single incidental regression-test fixtures** — STEREO (`cda/STA_L1_HET/Proton_Flux`, added as the fix for GH #223), BepiColombo (one `"bepicolombo"` case in `tests/test_sscweb.py`), Equator-S (`tree.cda.Equator_S.EQ.MAM....`), and Moon (`sscweb/moon` — not an observatory at all).
- **Multi-mission archives** routed to Field 17 instead: CDAWeb, AMDA, CSA, SSCWeb, CDPP 3DView, OMNIWeb.
- **Consistency check:** THEMIS and Arase are added while STEREO/BepiColombo/Equator-S are not, because the former have shipped package data and/or broad multi-file test coverage while the latter appear exactly once as fixtures for generic features. Juno is included on the strength of two independent sources (a feature test plus a developer statement), and is the weakest-evidenced entry in the field.

---

### 33. Logo (OPTIONAL)
- **Value:** `https://raw.githubusercontent.com/SciQLop/speasy/8f06d06f1e9c6e6013668c887c5c2546079b9b90/logo/logo_speasy_400dpi.png`

**Source:** From existing HSSI record — the submitted *asset* is preserved, recorded as a commit-pinned raw URL. The URL serves the logo file itself. The submitted value and the PyHC registry `logo` field both reference the same file on the `main` branch; the registry is authoritative about which asset is the logo, not about the URL string, and a branch reference breaks silently on any upstream rename, move or deletion, so the commit is pinned instead. The repository also contains `logo/logo_speasy.svg` (which also resolves, and is used in the README and docs headers), but Field 33 takes a single URL and the submitted PNG is kept.

---

## Metadata Agreement

By submitting this metadata, you acknowledge and agree that any metadata you provide is submitted voluntarily and becomes part of the public domain. You waive all rights, claims, and interests to the submitted metadata, and grant unrestricted use, reproduction, modification, and distribution rights to the receiving party or its designees.

---

## Could not verify
- **Contribution-time affiliations for Vincent Génot and Nicolas André.** Both now carry recorded affiliations (Field 6), taken from their shared HSSI Person records. What remains unverifiable is the tie to Speasy itself: the repository states no affiliation for either, Génot's ORCID `employments` group is empty, and Crossref returns no affiliation strings for the AMDA reference paper he leads. André's ISAE-SUPAERO is ROR-corroborated by ORCID and his IRAP association is supported by the department and city of his other ORCID employment, but neither appears in Speasy's own metadata.
- **An ORCID for Benjamin Renard in Speasy's own metadata** — `CITATION.cff`, Zenodo and DataCite still carry none. The identifier recorded in Field 6 comes from the shared HSSI Person record and is independently verified against ORCID itself, not from the repository.
- **A ROR for CDPP** — the ROR v2 API returns no match for "Centre de Données de la Physique des Plasmas".
- **DOIs for Speasy.jl and PyISTP** — no Zenodo records found; repository URLs are used instead, which the form permits.
- **`hpde.io` dataset identifiers** for the 14 bundled `cda.yaml` datasets (Field 28) — not resolved, so Field 28 stays "Not found" rather than risking unverified identifiers.
- **Two stale artifacts inside the repo, left as-is:** `HISTORY.rst` dates 1.7.1 as `2025-12-25`, contradicted by GitHub Releases, Zenodo, DataCite, `CITATION.cff` and the git tag (all 2025-12-18); and `plan/BACKLOG.md` still lists "HAPI client" and "NetCDF codec" as open P2 items although both are implemented and tested on `main` — the backlog is stale, not the code.

---

**End of HSSI Metadata Extraction**
