# HSSI Metadata Extraction Results

**HSSI Software ID:** 6adc2c82-61b3-41b4-89ca-62862bfe9b9f
**Repository:** https://github.com/SciQLop/speasy
**Source Revision:** 7a6281ff044a28a660a71f81e49581fe71baefe4 (2026-07-22 09:22:42 +0200, branch `main`)
**Extraction Date:** 2026-07-24
**Validation Date:** 2026-11-02
**Validation Status:** PASS

**Seeds this record was built from:**
1. **The existing HSSI record for Speasy** — the authoritative baseline for scalar and editorial fields.
2. **Prior canonical `hssi_metadata.md`** — extraction dated 2025-10-09, based on v1.6.1. Source of file-only additions carried forward where the current repo still supports them.

**Release v1.9.1:** Sections brought forward to the v1.9.1 release (2026-10-06) name the revision their new evidence was read at. Capabilities were read at the `v1.9.1` tag commit `bb0ab30525ef33e5d22ad63a68e4afea14b4f8c0` (short `bb0ab30`), an ancestor of `main`. Development activity, and capabilities that `main` has but v1.9.1 does not ship, were read at `main` head `b76618e8914f8cd4c0ec5310340ea262d32009dc` (short `b76618e8`, 2026-10-28). Evidence cited without a revision, or at `7a6281ff`, was read at the Source Revision above.

**Release state — what a value may rest on.** A value rests on what the newest release ships, not on unreleased code on `main` (the maintainer's rule for release updates, applied to this record on 2026-10-29 as to SciQLop and irispy). The record was first written the other way: at the Source Revision `main` held capabilities that the v1.7.1 release (2025-12-18) lacked — the `speasy/core/hapi/` HAPI server client, the HAPI binary codec, the ISTP netCDF codec and the `cdpp3dview` data provider — and the values resting on them carried the tag `[main-branch, unreleased as of v1.7.1]`. All four shipped in v1.8.0 (2026-08-31) and are present at `bb0ab30`, so those values are release-backed and each tag has been replaced by the release that shipped the capability. Capabilities `main` has gained since v1.9.1 — a `hapi` provider serving the whole official HAPI server registry, FTP access for direct archives, and a `speasy` command-line tool — support no value; they are recorded under the fields they bear on (Fields 4, 16, 17, 18 and 19) as notes for the next release update. Already released in v1.7.1, and unaffected: the HAPI **CSV** codec, the ISTP CDF codec, CSA-over-TAP, the bundled `cda.yaml` archive definitions, UiowaEphTool, SSCWeb coordinate systems, signal filtering/resampling, line + colormap plotting, WASM/Pyodide support.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

HSSI does not expose the original submitter through the view API. The Speasy wording in HSSI (name, description, concise description) is treated as intentional submitted editorial content and is preserved verbatim.

---

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** `https://doi.org/10.5281/zenodo.4118780`

**Source:** From existing HSSI record. Re-verified against the Zenodo API (`records/17978034` -> `"conceptdoi": "10.5281/zenodo.4118780"`), the DataCite API, and `CITATION.cff`/README badge. This is the correct concept (all-versions) DOI. Re-checked for v1.9.1 (2026-10-29): the v1.9.1 deposit `records/23186600` carries the same `conceptdoi`, DataCite's concept record presents `version` `v1.9.1`, and the README badge at `bb0ab30` still points at `10.5281/zenodo.4118780`. The `doi:` in `CITATION.cff` is a version DOI (Field 12), not this value.

---

### 3. Code Repository (MANDATORY)
- **Value:** `https://github.com/SciQLop/speasy`

**Source:** From existing HSSI record. Re-verified: repo is live, not archived, default branch `main`, last push 2026-07-22 (GitHub API). Also matches `CITATION.cff` `url:`, `pyproject.toml` `[project.urls] homepage`, and Zenodo `metadata.custom["code:codeRepository"]`. Re-verified 2026-10-29: live, not archived, default branch `main`, last push 2026-10-28.

---

### 4. Software Functionality (RECOMMENDED)

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
    **Reason: REQUIRED PARENT.** HSSI held `Coordinate Transforms: Mission-Specific` without its parent category until an earlier refresh added the parent. Every subcategory must have its parent listed.

12. `Coordinate Transforms:Magnetospheric`
    Evidence (released): `speasy/data_providers/ssc/__init__.py` exposes `coordinate_system=` on `get_data`/`_get_orbit` and injects it into the SSCWeb REST path; `docs/user/sscweb/sscweb.rst` documents the user-selectable set **geo, gm, gse, gsm, sm, geitod, geij2000** (default `gse`). Also `tests/test_cdpp3dview.py::test_get_data_on_frames` parameterizes over `GSE`, `GSM`, `SM`, `IAU_EARTH` (the 3DView provider, released in v1.8.0). The SSCWeb evidence above, released before v1.7.1, is sufficient on its own.

13. `Coordinate Transforms:Heliospheric`
    Evidence: `tests/test_cdpp3dview.py` parameterizes `coordinate_frame` over `HEE`, `HEEQ`, `HCI`, `IAU_SUN`, `ECLIPJ2000`, `J2000` (the 3DView provider, released in v1.8.0); support released before v1.7.1 comes from `speasy/data_providers/uiowa_eph_tool/__init__.py`, whose `__SUN_COORDINATES__ = {"Ecliptic", "Equatorial"}` provides Sun-origin heliocentric ecliptic/equatorial trajectories.

14. `Coordinate Transforms:Planetary`
    Evidence (released): `uiowa_eph_tool` hardcodes `__PLANET_COORDINATES__` (Geographic/Ecliptic/Equatorial), `__SATURN_COORDINATES__` (adds **KSM**), and `__SATELLITE_COORDINATES__` (adds **Co-rotational**) for Venus, Earth, Jupiter, Saturn, Io, Europa, Ganymede, Callisto, Titan, Enceladus and 14 other moons. Reinforced by 3DView body-fixed frames `IAU_JUPITER`, `IAU_MARS`, `IAU_SATURN`, `CPHIO`/`EPHIO`/`GPHIO`/`IPHIO` (released in v1.8.0).

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

**Caveat on Coordinate Transforms:** Speasy does not implement the transform math itself — it exposes the target coordinate system/frame as a user-facing request parameter and the web service returns data in that frame. Per the `software-functionality` skill ("if the user can access or benefit from the transform, even indirectly, err on the side of inclusion"), these are user-facing coordinate-transformation capabilities.

**Checked against v1.9.1 (`bb0ab30`).** The capabilities the 1.8.x and 1.9.x releases add fall under rows already listed, and the code named above as evidence for every stored row is still present:
- the 3DView provider (`speasy/data_providers/cdpp3dview/`), shipped in v1.8.0 and enabled by default since then (`HISTORY.rst` 1.8.0, pull request #349; the default `disabled_providers` is empty, and its docs page says it is enabled by default as of speasy 1.8, although the provider list in `docs/user/data_providers.rst` still calls it disabled), whose `get_data` takes a user-selected `coordinate_frame` (or `coordinate_system`) → the Coordinate Transforms rows already listed;
- the HAPI client `speasy.core.hapi.HapiProvider` (`capabilities`, `catalog`, `about`, `info`, `data`; v1.8.0), AMDA private parameters under `spz.inventories.tree.amda.PrivateParameters` (v1.8.3, `speasy/core/impex/__init__.py`) and direct file access to CDAWeb's netCDF datasets (v1.8.0, `speasy/data_providers/cda/_direct_archive.py`) → `Data Processing and Analysis:Data Access and Retrieval`;
- colormaps of CDAWeb `map_image`/`map_movie` products over their latitude/longitude grids, log scales and axis labels taken from ISTP attributes (`speasy/plotting/istp_hints.py`) and fill values masked before plotting (`speasy/plotting/__init__.py`) → `Data Visualization:2D Graphics`, `:Spectrogram` and `:Line Plots`;
- the v1.9.1 fixes to `clamp_with_nan()` and `sanitized()` → `Data Processing and Analysis:Data Reduction`.

`Data Visualization:Movies` was considered for the `map_movie` display type and rejected: `colormap()` draws a single time step (its `time_index` argument) and writes no animation.

*Note for the next release update:* `main` at `b76618e8` (2026-10-28) adds a `speasy` command-line tool (`speasy/cli/`, from commit `b87cb5b`, 2026-10-16): `get` with `--output` to a `.cdf`, `.csv` or `.nc` file, `cache warm`, `archive validate`, `providers`, `config`, and `quicklook`, which renders a SciQLop plot template as one image per time window. None of it is in v1.9.1, and it would fall under rows already listed (`Data Processing and Analysis:File Format Conversion`, `:Data Access and Retrieval`, `Data Visualization:Line Plots`).

---

### 5. Related Region (RECOMMENDED)

**Values — 3:**
1. `Earth Magnetosphere`
2. `Interplanetary Space`
3. `Planetary Magnetospheres`

**Source:** From existing HSSI record. Re-verified against the current repo: Earth Magnetosphere (MMS, Cluster, THEMIS, Arase, Wind/ACE upstream of the bow shock, SSCWeb GSE/GSM/SM trajectories); Interplanetary Space (ACE/Wind/OMNI solar wind, Solar Orbiter, PSP, STEREO); Planetary Magnetospheres (MAVEN STATIC at Mars, Juno JEDI at Jupiter, UiowaEphTool Jupiter/Saturn/moon frames, IMPEx common provider in `speasy/core/impex/`).

**Considered and not selected — `Solar Environment`:** Speasy's dynamic inventory reaches solar-mission datasets through CDAWeb/AMDA, `docs/examples/*.ipynb` and `tests/test_cdpp3dview.py` reference SOHO/SDO/STEREO, and the developers' own EPSC-DPS 2025 abstract frames the tool as serving "planetary and heliospheric" data. However the repository contains **no solar-atmosphere-specific support**, and the inner-heliosphere in-situ data (PSP/SOLO/STEREO SEP and magnetic field) is already covered by Interplanetary Space. The region is therefore omitted, per "prefer evidence over speculation"; it would become correct only if the repository gained solar-atmosphere-specific support, which it does not have at the source revision above.

**Note — `Earth Atmosphere` considered and dropped:** no ionosphere/thermosphere-specific products, models, or tests in the repo.

**Checked against v1.9.1 (`bb0ab30`).** The 1.8.x and 1.9.x releases add no region-specific code: the 3DView provider, the HAPI client and the plotting changes behave the same whatever region the data describe, so the three rows stand, and `Solar Environment` and `Earth Atmosphere` stay unselected for the reasons above. On `main` (`b76618e8`, not in v1.9.1) the `hapi` provider reaches every server of the official HAPI registry, LISIRD, Helioviewer, INTERMAGNET and VirES for Swarm among them; that is generic access to whatever those servers hold, not region-specific support (rules 3 and 7), so it would not change this field either.

---

### 6. Authors (MANDATORY)

**Values — 6 authors.** HSSI held 2 authors until an earlier refresh added the other four, the largest correction that refresh made: the repository's `CITATION.cff`, the Zenodo v1.7.1 record, and the DataCite concept-DOI record all list **6**. Matched by ORCID first, then normalized name; affiliations unioned per matched author. No author present in any source has been dropped.

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

**Checked against v1.9.1 (`bb0ab30`).** The author sources are unchanged: `CITATION.cff` changed only its `version`, `doi` and `date-released`; `AUTHORS.rst` and the `pyproject.toml` `authors`/`maintainers` are as before; and the Zenodo v1.9.1 deposit (`10.5281/zenodo.23186600`) lists the same six creators and no contributors. Two people who committed to the 1.8 and 1.9 releases are not authors, because no author source names them (rule 5): Richard Hitier (`@RichardHitier`, 146 commits between v1.7.1 and v1.9.1, who wrote the 3DView provider, the HAPI codecs and client, and the netCDF codec) and `@Beforerr` (three commits, fixes in 1.9.0 and 1.9.1). Commit volume is not authorship; a later refresh adds either one if `CITATION.cff`, `AUTHORS.rst` or a Zenodo deposit comes to credit them.

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

**Re-checked at v1.9.1 (`bb0ab30`):** the README lead and `docs/index.rst` still claim "over 70 space missions and 65,000 products", and the description names no capability the code lacks, so it is kept (rule 6).

---

### 9. Concise Description (OPTIONAL)
Submitted editorial wording, preserved verbatim:

> Space Physics made easy! A simple Python package to deal with main Space Physics WebServices (CDA, SSC, AMDA, CSA) providing easy access to over 70 space missions and 65,000 products.

**Source:** From existing HSSI record (183 characters — within the 200-character limit). The prior `hssi_metadata.md` had "made EASY!" (matching the README H1 "Space Physics made EASY"); live HSSI is authoritative for this scalar editorial field, so the submitted lowercase "easy!" is kept. Not a proposed change. Re-checked at v1.9.1 (`bb0ab30`): every claim is still supported, and the `pyproject.toml` `description` still reads "A simple Python package to deal with main Space Physics WebServices (CDA, CSA, AMDA and SSC)."

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

- **Version Number:** `v1.9.1`
- **Version Date:** `2026-10-06`
- **Version PID:** `https://doi.org/10.5281/zenodo.23186600`
- **Version Description:**

```markdown
### Bug fixes

* `SpeasyVariable.clamp_with_nan()` works on multi-component variables (e.g. `amda/imf`) instead of
  raising `IndexError`, and clamps each value on its own. A per-component `VALIDMIN`/`VALIDMAX` is
  applied per column, and an explicit `valid_min=0` or `valid_max=0` is no longer ignored.
* `SpeasyVariable.sanitized()` no longer ignores an explicit `valid_min=0` or `valid_max=0`, accepts
  per-component bounds as arrays, and filters with a single bound when only `VALIDMIN` or `VALIDMAX` is set.
```

**Version Number** (rule 3). HSSI held `v1.7.1` (2025-12-18, PID `10.5281/zenodo.17978034`) until this update, and `v1.6.1` before that; each was superseded by a newer release. Nine releases followed v1.7.1: v1.8.0 (2026-08-31), v1.8.1 to v1.8.6 (2026-09-02 to 2026-10-01), v1.9.0 (2026-10-03) and v1.9.1 (2026-10-06). Each has a `v`-prefixed tag on `main`'s own lineage (`git merge-base --is-ancestor <tag> b76618e8` holds for all nine), a GitHub release that is neither a draft nor a pre-release, and a PyPI wheel and sdist that are not yanked. `v1.9.1` is the newest: its tag points at `bb0ab30`, where `CITATION.cff` has `version: 1.9.1`, and on 2026-10-29 GitHub's newest release and PyPI's `info.version` were both 1.9.1. The tags `v1.10.0.dev0` (2026-10-04) and `v1.9.2.dev0` (2026-10-06) open development cycles: they are PEP 440 pre-releases with no GitHub release and no PyPI upload, and never count (rule 2). Since v1.8.0 the version is derived from git tags (`uv-dynamic-versioning`); the `VERSION` file and the static `pyproject.toml` `version` are gone, so the tag is the version's only source in the tree. The `v` prefix follows the form this entry already used and the tag's own form; PyPI writes `1.9.1`.

**Version Date** (rule 7). The GitHub release `v1.9.1` was published 2026-10-06T11:13:59Z. The tagged commit (2026-10-06 10:44:36 +0200), the PyPI upload (2026-10-06T11:14:20Z), the Zenodo deposit (created 2026-10-06T11:14:08Z), `CITATION.cff` `date-released: 2026-10-06` and the `HISTORY.rst` heading `1.9.1 (2026-10-06)` all agree.

**Version PID** (rule 17). `10.5281/zenodo.23186600` is the v1.9.1 GitHub-integration deposit: its Zenodo `metadata.version` and DataCite `version` are `v1.9.1`, it carries `IsSupplementTo https://github.com/SciQLop/speasy/tree/v1.9.1` and `IsVersionOf 10.5281/zenodo.4118780`, and the DOI resolves. **Trap:** `CITATION.cff` at the tag commit `bb0ab30` gives `doi: 10.5281/zenodo.23127741`, which is the **v1.9.0** deposit; the tag was cut before the v1.9.1 deposit existed, and commit `aaae574` (2026-10-06, the `v1.9.2.dev0` tag commit) corrected the file to `10.5281/zenodo.23186600`. The v1.9.0 DOI is never this release's PID.

**Version Description** (rules 10 and 13–16). Derived afresh for v1.9.1; the v1.7.1 and v1.7.0 changelog HSSI held is not carried over. The GitHub release name is only the tag (`v1.9.1`), so the text comes from the release body, which `HISTORY.rst` (`1.9.1 (2026-10-06)`) and the Zenodo deposit's description repeat. The body's curated `### Bug fixes` section is kept verbatim, line breaks included. Its two trailing auto-generated pull-request items are trimmed whole: "A zero-lifetime cache entry is expired immediately" (pull request #397) fixed a strict comparison that made a cache test flaky on Windows CI (commit `25c6bb1`), test housekeeping no user meets (rule 14), and "Fix clamp_with_nan on multi-component variables" (pull request #396) restates the first bullet.

**Earlier discrepancy, kept for the record:** `HISTORY.rst` heads the v1.7.1 section `1.7.1 (2025-12-25)`, contradicted by the GitHub release, Zenodo, DataCite, `CITATION.cff` and the tag (all 2025-12-18); the v1.7.1 row used 2025-12-18.

---

### 13. Programming Language (RECOMMENDED)
- **Value:** `Python 3.x`

**Source:** From existing HSSI record. Re-verified; set-union with repo evidence yields no new value:
- `pyproject.toml` at HEAD: `requires-python = ">=3.10"` with classifiers for Python **3.10, 3.11, 3.12, 3.13, 3.14** (the repo's `CLAUDE.md` claim of ">=3.10" is confirmed).
- **Change since the prior extraction:** at the v1.7.1 release the floor was still `>=3.9` (classifiers 3.9-3.14); the bump to `>=3.10` and the removal of the 3.9 classifier shipped in v1.8.0 ("Foundation: Python ≥3.10 + UV + dependency-groups", pull request #290). At `bb0ab30` (v1.9.1) `requires-python = ">=3.10"`, the classifiers are 3.10–3.14, and the CI matrix is 3.10–3.14. The prior `hssi_metadata.md` listing of "3.9, 3.10, 3.11, 3.12, 3.13" is superseded by 3.10-3.14 — this affects only the note, not the field value.
- GitHub language breakdown: Python 659,690 B; Jupyter Notebook 20,204 B; Makefile 2,486 B. `Jupyter Notebook` is **not** an allowed HSSI value and the notebooks are documentation examples, so nothing is added. `Julia` is deliberately not added — `Speasy.jl` is a separate repository (Fields 29/30), not code in this one.

---

### 14. Reference Publication (RECOMMENDED)
- **Value:** Not found

**Source / reasoning:** No paper describing Speasy is designated by the project as its preferred citation. `CITATION.cff` has no `preferred-citation` block and points users at the software DOI (`message: "If you use this software, please cite it as below."` + `doi: 10.5281/zenodo.17978034`); the README's only DOI badge is the Zenodo concept DOI; the Zenodo and DataCite records carry no `IsDescribedBy` relation. There is no JOSS paper.

**Closest available items, and why neither is a reference publication:** the developers' EPSC-DPS 2025 abstract *"SciQLop & Speasy: Open-Source Tools for Unified Planetary and Heliospheric Data Analysis"* (`https://doi.org/10.5194/epsc-dps2025-1422`) is a meeting abstract, which is not an eligible publication for Field 14 or Field 27; HSSI listed it in Field 27 until the v1.9.1 update removed it (see Field 27). The developers' DASH 2026 poster *"The SciQLop ecosystem: a layered open-source stack for in-situ heliophysics data"* (`https://doi.org/10.5281/zenodo.23169249`) presents Speasy as one layer of the SciQLop stack and is recorded in Field 27 under rule 3; the project designates neither it nor any paper as the work to cite.

**Re-checked at v1.9.1 (`bb0ab30`):** `CITATION.cff` still has no `preferred-citation` and asks users to cite the software DOI, and the README and `docs/index.rst` cite only the concept DOI. The 2026-10-29 literature search (Field 27) found no paper describing Speasy: ADS `title:"speasy"` returns six Zenodo software records and the EPSC-DPS abstract, and `abs:"speasy"` adds only meeting abstracts. Field 14 therefore stays empty.

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
`Amda`, `Cdaweb`, `Cdf`, `Cdpp`, `Cnes`, `Esa`, `Nasa Api`, `Nasa Data`, `Plasma Physics`, `Pnst`, `Pyhc Package`, `Python 3`, `Satellite`, `Sciqlop`, `Space Physics`, `Space Plasma`, `Sscweb`, `Webservices`

**PyHC membership keyword:** `pyhc package` (stored lower-case, rendered `Pyhc Package`) is HSSI's catalogue-wide marker for official PyHC packages, and Speasy is listed in the PyHC registry (`_data/projects.yml`). It replaced the ad hoc `pyhc` keyword this record used to carry; `pyhc` should not be restored.

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
| `hapi` | `speasy/core/hapi/` client (capabilities / catalog / info / data; released in v1.8.0) plus the HAPI CSV codec (since v1.5.0) and binary codec (v1.8.0); `tests/test_hapi.py`, `tests/test_hapi_codecs.py` |
| `netcdf` | ISTP netCDF codec `speasy/core/codecs/bundled_codecs/istp/netcdf.py`, `tests/test_netcdf_codec.py` (released in v1.8.0) |

**Added for v1.9.1 — 1:**

| Keyword | Evidence |
|---|---|
| `3dview` | The CDPP 3DView geometry service, for which Speasy ships a dedicated provider (`speasy/data_providers/cdpp3dview/`), released in v1.8.0 and enabled by default since then; documented at `docs/user/cdpp3dview/cdpp3dview.rst` and listed in `docs/user/data_providers.rst` at `bb0ab30`. It is the service Speasy is a client for (rule 10), as the stored `amda`, `cdaweb`, `csa` and `sscweb` are, and it restates no other field: 3DView has no Data Sources row and is carried by `Other` in Field 17. No keyword row existed for it in any case, separator or plural variant (`cdpp` is the organization), so the term is minted lower-case (rule 12). |

**Checked against v1.9.1 (`bb0ab30`).** The project-declared keywords are unchanged: the `pyproject.toml` `keywords`, the GitHub topics, and the PyHC registry `keywords` (`_data/projects.yml`) read as described here on 2026-10-29. Considered and not added: `quicklook` and `command line`, for the `speasy` command-line tool only `main` has (an interface, not a domain term, and not in v1.9.1); and the names of HAPI registry servers that `main`'s `hapi` provider reaches (`intermagnet`, `lisird`, `vires`, `das2` and others), which are not in v1.9.1, are generic HAPI access the stored `hapi` already carries, and in the case of `vires` and `das2` would restate Field 17 rows (rule 6).

**Note — considered and dropped:** `general`, `local`, `remote`, `web_service` (PyHC keywords, but too generic to function as science keywords; `Webservices` already covers the last), `python3` / `python-3` (duplicates of the existing `Python 3`), `data_container` (implementation detail), `wasm` / `pyodide` (runtime platform, not a science keyword), and the GitHub topics already represented by existing values (`amda`, `cdaweb`, `cnes`, `esa`, `nasa-api`, `plasma-physics`, `pnst`, `pyhc` (as `pyhc package`), `sciqlop`, `space-physics`, `space-plasma`, `sscweb`).

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

9. `HAPI` — **released.** `speasy/core/hapi/{client,provider,parser,exceptions}.py` implements a full HAPI client (`capabilities`, `catalog`, `about`, `info`, `data` endpoints with HAPI status-code handling for codes 1201/1400-1499/1500+), tested against live servers in `tests/test_hapi.py` (AMDA `https://amda.irap.omp.eu/service`, CDAWeb, and `hapi-server.org/servers/TestData3.3`). The HAPI **CSV** codec has shipped since v1.5.0 ("Basic HAPI CSV codec", `HISTORY.rst`); the HAPI **binary** codec and the server client shipped in v1.8.0 ("Hapi binary codec", pull request #283; "Hapi REST provider", #285). Scope caveat, still true at `bb0ab30` (v1.9.1): the client is a public class, `speasy.core.hapi.HapiProvider`, not a `get_data` provider — `speasy/data_providers/__init__.py` imports only the amda, csa, cda, ssc, generic archive, uiowaephtool and cdpp3dview providers.

**Note — considered and dropped:** `FTP/FTPS Directories` (no FTP support in v1.9.1: at `bb0ab30` `any_files.py` and `http.py` are HTTP(S)-only, and `speasy/` holds no `ftp://` or `ftplib`; see the note below), `S3/Cloud-aware` (no boto3/fsspec, no `s3://`), `das2`, `The Virtual Solar Observatory`, `VirES`, `WDC` (no code in v1.9.1 reaches them; see the note below). CSA, CDPP 3DView, the University of Iowa Cassini Ephemeris Tool, and YAML-described local/remote archives remain covered by the existing `Other`.

**Note for the next release update** (read at `main` `b76618e8`, 2026-10-28; none of this is in v1.9.1, so no value here rests on it):
- `speasy/core/ftp.py` (commit `2d8eca9`, 2026-09-25) lets direct archives and `speasy.core.any_files` read files from FTP servers through an `ftp://` `url_pattern` or `master_file`, with folder listing and the file cache working as for HTTP (the `Unreleased` section of `HISTORY.rst`). Once released, `FTP/FTPS Directories` passes rule 9.
- `speasy/data_providers/hapi/` (commit `0a1ecbd`, 2026-10-13) is a `hapi` provider serving every server of the official HAPI registry from a bundled snapshot, `speasy/data/hapi/abouts.json`, and wires the HAPI client into `get_data` (`hapi/<server>/<dataset id>/<parameter name>`). The snapshot includes VirES for Swarm (`https://vires.services/hapi`), the World Data Centres at Edinburgh (`https://wdcapi.bgs.ac.uk/hapi`) and Kyoto (`https://wdc.kugi.kyoto-u.ac.jp/hapi`), and the das2 server at the University of Iowa (`https://planet.physics.uiowa.edu/das/das2Server/hapi`); `docs/user/hapi/hapi.rst` names VirES for Swarm and the Kyoto WDC and fetches the Kyoto Dst index as its example. Once released, `VirES`, `WDC` and `das2` pass rule 7 (the rows the client reaches), and the registry's other servers (CCMC ISWA, INTERMAGNET, UCalgary SRS, NESDIS, LISIRD, KNMI, Helioviewer) stay under `Other`. CDAWeb, AMDA, CSA and SSCWeb are never queried through it (`NATIVELY_SERVED` in `speasy/core/hapi/registry.py`).

---

### 18. Input File Formats (RECOMMENDED)

**From the existing HSSI record — 4:** `ascii`, `CDF`, `csv`, `Other`

**From repository evidence — 2:**

5. `ISTP-Compliant` — **released.** Speasy's CDF reading is explicitly an ISTP layer: at tag `v1.7.1` the file is `speasy/core/codecs/bundled_codecs/istp_cdf.py`; a directory reorganization released in v1.8.0 moved it to `speasy/core/codecs/bundled_codecs/istp/cdf.py` (class `IstpCdf` in both) loads through `pyistp` and honours ISTP metadata (`DEPEND_n`, `VAR_TYPE`, `FILLVAL`, `VALIDMIN`/`VALIDMAX`, `LABL_PTR_n`, `*_PTR` attributes, and master/skeleton CDFs with a 7-day cache retention). `speasy/core/cdf/inventory_extractor.py` extracts inventories from ISTP master CDFs; `speasy/data_providers/cda/_inventory_builder/_cdf_masters_parser.py` parses CDAWeb ISTP masters; `docs/user/csa/csa.rst` at `7a6281ff` stated that the CSA integration handles "both the webservice API and ISTP CDF file formats"; at `bb0ab30` the page is reworded and says the integration exposes the CSA's public CEF datasets that follow the ISTP conventions, delivered as CDF files.

6. `netCDF3/4` — **released in v1.8.0** ("Add new net_cdf4 codec", pull request #288); v1.8.0 also serves CDAWeb's netCDF datasets by direct file access (pull request #333). `speasy/core/codecs/bundled_codecs/istp/netcdf.py` (class `IstpNetCDF`) declares `supported_extensions = ["nc", "nc4"]` and `supported_mimetypes = ["application/x-netcdf", "application/netcdf"]`, and implements `load_variables` / `load_variable` / `list_variables`. Registered in `bundled_codecs/__init__.py` behind an optional `import netCDF4` (skipped on WASM, which has no netCDF4 wheel). Tested by `tests/test_netcdf_codec.py`, including a real CDAWeb-derived fixture `tests/resources/ac_h2s_mfi_cdaweb.nc`.

**Note — considered and dropped:** `JSON` — `speasy.core.inventory.indexes.to_json`/`from_json` and the HAPI/CSA JSON payloads are inventory-metadata and wire-protocol handling, not science-data file I/O (inventories are persisted through the disk cache, not JSON files). `HDF5` — reached only indirectly as netCDF4's container; there is no `h5py` dependency and no HDF5 API. `FITS`, `IDL.sav`, `Zarr` — no support. The existing `Other` continues to cover HAPI CSV/binary and the YAML archive-description files (`speasy/data/archive/*.yaml`).

*Note for the next release update:* the `speasy quicklook` command on `main` (`b76618e8`, not in v1.9.1) reads SciQLop plot templates written as JSON or YAML (`speasy/plotting/sciqlop_template.py::_read_document`). Once released, a user-supplied JSON template passes rule 4, which would add `JSON`; the YAML form falls under the existing `Other`.

---

### 19. Output File Formats (RECOMMENDED)

**From the existing HSSI record — 3:** `ascii`, `CDF`, `csv`

**From repository evidence — 3:**

4. `ISTP-Compliant` — **released.** `IstpCdf.save_variables` writes ISTP-structured CDFs via `pycdfpp` (at tag `v1.7.1`: `bundled_codecs/istp_cdf.py`; from v1.8.0: `bundled_codecs/istp/cdf.py`): `_write_axis` / `_write_variable` emit `DEPEND_n` links, convert `datetime64[ns]` axes to `CDF_TIME_TT2000`, materialise `*_PTR` attributes as real variables, and support gzip variable compression. `tests/test_codecs.py` covers the round trip.

5. `netCDF3/4` — **released in v1.8.0**. `istp/netcdf.py::save_variables` (line 129) implements writing; `tests/test_netcdf_codec.py` exercises write-then-read.

6. `Other` — HAPI **binary** output via `bundled_codecs/hapi/binary/writer.py::save_hapi_binary` (registered as codec `hapi/binary`; released in v1.8.0), plus HAPI CSV output via `save_hapi_csv` (at tag `v1.7.1`: `bundled_codecs/hapi_csv/writer.py`; from v1.8.0: `bundled_codecs/hapi/csv/writer.py`). Mirrors the `Other` already present in Input File Formats.

**Note:** every Speasy codec implements the same `CodecInterface` contract with `save_variables(variables, file=None)` returning a buffer when `file is None`, so each listed output format is genuinely writable rather than read-only.

*Note for the next release update:* `speasy quicklook` on `main` (`b76618e8`, not in v1.9.1) writes one figure per time window in any format matplotlib writes (`png` by default, `pdf`, `svg`); once released, those images fall under the existing `Other` (rule 7).

---

### 20. Operating System (RECOMMENDED)

**From the existing HSSI record — 4:** `Linux`, `Mac`, `Operating System Independent`, `Windows`

**From repository evidence — 1:**

5. `Other` — WebAssembly / Pyodide in-browser runtime. **Released in v1.7.1** (verified: `speasy/core/platform.py` and `.github/workflows/wasm_tests.yml` both exist at the tag). Evidence: `speasy/core/platform.py::is_running_on_wasm()` (tests `platform.system() == "emscripten"`), WASM-specific branches in `speasy/core/http.py`, `core/cache/_function_cache.py`, `core/cache/_providers_caches.py`, `core/cache/_request_locker.py`; `pyproject.toml` gates `pysciqlop-cache` on `sys_platform != "emscripten"`; a dedicated CI workflow builds a wheel, loads a Pyodide distribution (a custom 0.29.0 build with `pycdfpp` preinstalled at v1.7.1; the stock 314.0.7 distribution at `bb0ab30`), and runs `tests/test_wasm.py` in Chrome via `pytest-pyodide`, asserting `spz.core.platform.is_running_on_wasm()` and performing real `spz.get_data` calls (`amda/c1_b_gsm`, `amda/ace-imf-all`, `cdaweb/THA_L2_FGM/tha_fgl_gsm`, `sscweb/moon`). Two of the v1.7.1 changelog entries are WASM-driven. Since v1.8.5 Speasy needs Pyodide 314 or later on WebAssembly, where micropip installs `pycdfpp` 0.15's wasm wheel from PyPI (`HISTORY.rst` 1.8.5); the WASM test fetches the same four products at `bb0ab30`.

**Source for those four:** From existing HSSI record; re-verified against `.github/workflows/tests.yml`, whose matrix is `os: [macos-latest, windows-latest, ubuntu-latest]` x `python-version: [3.10, 3.11, 3.12, 3.13, 3.14]`, unchanged at `bb0ab30`.

**Note:** `OS Independent` (the HSSI vocabulary's near-duplicate of `Operating System Independent`) is deliberately **not** added — the record already carries `Operating System Independent`, and adding both would create a duplicate. `MobilePlatform` and `Solaris` are unevidenced.

---

### 21. CPU Architecture (RECOMMENDED)
- **Value:** `CPU Independent`

**Source:** From existing HSSI record. Re-verified: Speasy is pure Python (built with `flit_core.buildapi` until v1.8.0 and with `hatchling` since; no compiled extensions, no `platform_machine` environment markers; the v1.9.1 wheel on PyPI is `speasy-1.9.1-py3-none-any.whl`). CI additionally demonstrates execution on x86-64 (ubuntu-latest, windows-latest), Apple Silicon arm64 (macos-latest), and WebAssembly (Pyodide). Those specific values are deliberately **not** added: `CPU Independent` already subsumes them, and enumerating them would add redundancy without search value. All binary-wheel dependencies (`numpy`, `scipy`, `pandas`, `matplotlib`, `pycdfpp`, `netCDF4`) publish wheels for these platforms. `pycdfpp` has been a direct dependency since v1.8.5 (`pycdfpp>=0.15.0`).

---

### 22. Related Phenomena (OPTIONAL)
- **Value:** `Solar Wind`

**Reasoning:** an earlier source note for this field enumerated a stale list taken from the static form-fields reference. The live controlled vocabulary for Related Phenomena is: **Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission** — it contains no "Coronal Holes", and it does contain "Geomagnetic Storms" and "Solar Wind", which the stale list omitted.

Re-assessed against that live list: Speasy is deliberately phenomenon-agnostic — a data access layer plus a time-series container. There is no solar-feature code, no event detection, and no phenomenon-specific algorithm anywhere under `speasy/`. `Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`, `Solar Flares` and `X-ray emission` therefore have no repository support and remain excluded.

**`Solar Wind` is recorded, on a completeness argument.** The arguments weighed both ways were: in favor, Speasy's flagship documented products are solar-wind measurements (ACE/SWE, Wind/SWE, and the entire OMNI solar-wind dataset are among its headline examples, and `Interplanetary Space` is already an accepted Related Region), so an HSSI user searching "Solar Wind" arguably should find Speasy. Against: Speasy *transports* upstream solar-wind data rather than providing solar-wind science functionality — by that standard the value would be equally true of any generic CDAWeb/AMDA client and carries no distinguishing information about this software. The completeness argument prevailed: the field would otherwise be empty, `Solar Wind` is an exact controlled-vocabulary value, and discoverability for solar-wind data access is a genuine user benefit.

**`Geomagnetic Storms`** — excluded. Speasy ships no storm indices as a distinguishing capability and no storm-phase logic; the Kp/Dst-style products reachable through AMDA/OMNI are again pure upstream transport.

**Note — considered and dropped (custom entries are permitted for this field, so these were weighed explicitly):** the AMDA shared catalogs and timetables reachable through Speasy include event lists such as `Catalogs.SharedCatalogs.MARS.MEXShockCrossings` and `TimeTables.SharedTimeTables.EARTH.Event_list_tail_hall_reconnection_SC1` (used in `tests/test_amda_catalog.py` and `tests/test_amda_timetable.py`), which would suggest **custom** entries like "bow shock crossings" or "magnetic reconnection" (distinct from the official `Solar Wind` vocabulary row adopted above). These are **upstream data products that Speasy transports**, not science functionality Speasy provides for a phenomenon — the same entries would be equally true of any generic AMDA client, so they carry no information about this software. The `docs/examples/alfvenic.ipynb` "Alfvénic slow solar wind" topic is likewise an example notebook, not a capability.

**Checked against v1.9.1 (`bb0ab30`):** the 1.8.x and 1.9.x releases add no phenomenon-specific code, so the verdicts above stand. The Kyoto Dst example in the documentation of `main`'s `hapi` provider (not in v1.9.1) retrieves an index, which is transport, not storm analysis (rules 5 and 6).

---

### 23. Development Status (RECOMMENDED)
- **Value:** `Active`

**Source:** Carried forward from the prior `hssi_metadata.md` and re-verified against the current repo. Per repostatus.org, "Active" = has reached a stable, usable state and is being actively developed:
- `pyproject.toml` classifier `Development Status :: 5 - Production/Stable`.
- Release cadence: v1.5.0 (2025-02-25), v1.5.1 (2025-02-25), v1.5.2 (2025-06-03), v1.6.0 and v1.6.1 (2025-09-05), v1.7.0 (2025-11-25), v1.7.1 (2025-12-18), v1.8.0 (2026-08-31), v1.8.1 (2026-09-02), v1.8.2 (2026-09-18), v1.8.3 (2026-09-24), v1.8.4 (2026-09-25), v1.8.5 (2026-09-28), v1.8.6 (2026-10-01), v1.9.0 (2026-10-03), v1.9.1 (2026-10-06).
- Dated anchors, read 2026-10-29: last commit on the default branch `main` `b76618e8`, **2026-10-28**; last release v1.9.1, **2026-10-06**; GitHub `pushed_at = 2026-10-28T20:37:53Z`; `open_issues_count` 60 (GitHub counts open pull requests in it); Dependabot active. At the Source Revision they were `7a6281ff` (2026-07-22), v1.7.1 (2025-12-18) and 53.
- Maintained CI (3 operating systems x 5 Python versions, plus a separate WASM job, plus scheduled Monday/Wednesday runs) and maintained ReadTheDocs documentation.
- PyHC registry ratings: software_maturity **Good**, testing **Good**, documentation **Good**, python3 **Good**, license **Good** (community: Partially met).
- GitHub `archived = false`.

Not `Inactive` or `Unsupported` (development is ongoing), not `WIP` (there are stable public releases on PyPI), not `Moved` (the repository URL is current).

---

### 24. Documentation (RECOMMENDED)
- **Value:** `https://speasy.readthedocs.io/en/stable/`

**Source:** From existing HSSI record — submitted value preserved. The URL resolves, and serves the project's stable documentation. The README's "Documentation and examples" section links to exactly this `/en/stable/` URL, and `.readthedocs.yaml` is present in the repo root. The PyHC registry lists the unversioned `https://speasy.readthedocs.io/`, and the prior `hssi_metadata.md` also used the unversioned form; the submitted `/en/stable/` form is more precise and is kept. The examples gallery `https://speasy.readthedocs.io/en/latest/examples/index.html` also resolves but is not added, since Field 24 takes a single URL. Re-verified 2026-10-29: the URL resolves (HTTP 200) and serves the documentation built from the v1.9.1 commit (its page title carries `+bb0ab30`); the README's "Documentation and examples" section still links it, and the PyHC registry still lists the unversioned `https://speasy.readthedocs.io/`.

---

### 25. Funder (OPTIONAL)
- **Organization:** `CDPP (Centre de Données de la Physique des Plasmas)`
- **Funder Identifier:** `https://cdpp.irap.omp.eu/`

**Source:** From existing HSSI record. Re-verified against the README "Credits" section: "The development of Speasy is supported by the CDPP (http://www.cdpp.eu/)."

**Notes:**
- **No ROR exists for CDPP.** The ROR v2 API returns 0 results for the exact phrase "Centre de Données de la Physique des Plasmas", and broader CDPP-related queries return only unrelated plasma-physics institutes. The existing non-ROR URL identifier is therefore the best available value and is kept unchanged.
- Per the acronym-expansion guidance the preferred organization form would be the expanded `Centre de Données de la Physique des Plasmas` without the leading acronym. This is a **cosmetic** difference from the submitted value and is **not** proposed as a change.
- Zenodo and DataCite `fundingReferences` are both empty, so no additional funder can be substantiated. CNES appears only as a GitHub topic/keyword (CDPP is CNES/CNRS-operated) and is **not** asserted as a funder.
- Re-checked for v1.9.1 (2026-10-29): the Zenodo v1.9.1 deposit and DataCite's concept and v1.9.1 records carry no funding, the README Credits section at `bb0ab30` is unchanged, and the developers' DASH 2026 poster (Field 27) acknowledges no funder.

---

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

**Reasoning:** No award or grant information exists in any source. DataCite `fundingReferences = []`; the Zenodo record carries no grants; and the repository (README Credits, `AUTHORS.rst`, `HISTORY.rst`, `docs/`) names CDPP as a supporter without any award title or number. Deliberately not fabricated. Re-checked for v1.9.1 (2026-10-29): still none in the Zenodo v1.9.1 deposit, DataCite, the README Credits at `bb0ab30`, or the DASH 2026 poster.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Values — 12:** one publication by the developers about the software (rule 3) and eleven papers whose results were built with Speasy and say so (rule 5). Rule 4 adds nothing.

**By the developers, about the software (rule 3):**

1. `https://doi.org/10.5281/zenodo.23169249`
   *Jeandet, A., Aunai, N., Génot, V., Renard, B., Bouchemit, M., & André, N. (2026). The SciQLop ecosystem: a layered open-source stack for in-situ heliophysics data. Poster, Data, Analysis, and Software in Heliophysics (DASH) 2026, Dublin, 5–7 October 2026. Zenodo.*
   **Evidence:** a poster deposited as the poster itself (Zenodo resource type `poster`, with the PDF `poster_DASH2026_jeandet.pdf`), by five of Speasy's six `CITATION.cff` authors. It presents the SciQLop stack layer by layer, and Speasy is one of the layers, with panels of its own: the data-access layer that, in the record's words, "presents AMDA, CDAWeb, SSCWeb, the Cluster Science Archive, CDPP's 3DView geometry service, HAPI servers and local archives behind one API", `SpeasyVariable` as the interface every layer shares, the speasy-proxy server, and the entry points through which a package adds a data source of its own. It also covers SciQLop, the application Speasy serves as data engine, and the stack's other layers (AstraLint, CDFpp, SciQLopPlots, tscat, cocat). Found by the Zenodo creator-keyed search on Alexis Jeandet's name and ORCID.

**Papers whose results were built with Speasy (rule 5):** each paper's own results rest on data retrieved through Speasy, and the paper says so deliberately, in its acknowledgements, its Data Availability statement or its methods. Speasy's citing literature is small (these eleven are the deliberate uses the 2026-10-29 search confirmed and the catalogue maintainer kept), so each still shows a searcher how and where Speasy is used. All eleven were read, in the source each entry names or else in ADS's full-text index.

2. `https://doi.org/10.1029/2022JA030686` — Dahani, S., et al. (2022). The Helicity Sign of Flux Transfer Event Flux Ropes and Its Relationship to the Guide Field and Hall Physics in Magnetic Reconnection at the Magnetopause. *Journal of Geophysical Research: Space Physics*, 127, e2022JA030686. Its acknowledgements credit "tools developped at IRAP by the CDPP", naming AMDA and speasy with its PyPI address.
3. `https://doi.org/10.1029/2022JA030996` — Michotte de Welle, B., et al. (2022). Global Three-Dimensional Draping of Magnetic Field Lines in Earth's Magnetosheath From In-Situ Spacecraft Measurements. *Journal of Geophysical Research: Space Physics*, 127, e2022JA030996. Data Availability statement, read in the HAL author manuscript (`hal-03841364`): "The in-situ data are available by using the Speasy package (https://github.com/SciQLop/speasy). It allows to access the data on the CDAweb database (https://cdaweb.gsfc.nasa.gov) for the THEMIS mission, and AMDA database (http://amda.irap.omp.eu) for Cluster, DoubleStar, and MMS missions."
4. `https://doi.org/10.1103/PhysRevLett.130.205201` — Manzini, D., Sahraoui, F., & Califano, F. (2023). Subion-Scale Turbulence Driven by Magnetic Reconnection. *Physical Review Letters*, 130, 205201. Acknowledgements, as ADS's full-text index gives them for the published article: "The python client Speasy [70] was used for data retrieval." The arXiv version (2208.00855v2), with its own reference numbering, reads "The python client SPEASY [72] was used for data retrieval." The publisher's page was not read.
5. `https://doi.org/10.1029/2023JA032098` — Michotte de Welle, B., et al. (2024). Global Environmental Constraints on Magnetic Reconnection at the Magnetopause From In Situ Measurements. *Journal of Geophysical Research: Space Physics*, 129, e2023JA032098. Data Availability statement, read in the HAL author manuscript (`hal-04780931`): "The in-situ data are available by using the Speasy package Jeandet & Schulz (2023). It allows to access the data on the CDAweb database (https://cdaweb.gsfc.nasa.gov) for the THEMIS mission, and AMDA Budnik (2011) for Cluster, DoubleStar, and MMS missions." Its reference list gives the Speasy record `doi: 10.5281/zenodo.7995732`.
6. `https://doi.org/10.1103/PhysRevLett.132.235201` — Manzini, D., Sahraoui, F., & Califano, F. (2024). Cascade-Dissipation Balance in Astrophysical Plasmas: Insights from the Terrestrial Magnetosheath. *Physical Review Letters*, 132, 235201. ADS indexes no full text for it; it was found because ADS lists it among the papers citing a Speasy Zenodo record, and its arXiv version (arXiv:2312.15365) acknowledges: "The python client SPEASY was used for data retrieval."
7. `https://doi.org/10.1029/2024JA032754` — Dahani, S., et al. (2024). Direct In-Situ Estimates of Energy and Force Balance Associated With Magnetopause Reconnection. *Journal of Geophysical Research: Space Physics*, 129, e2024JA032754. Its acknowledgements credit "tools developed at IRAP by the CDPP", naming AMDA and speasy with its PyPI address.
8. `https://doi.org/10.1051/0004-6361/202554759` — Head, L. A., et al. (2025). Ultraviolet auroral bridge of Jupiter: The effect of the solar wind on the morphology of the polar aurora. *Astronomy & Astrophysics*, 700, A142. Its data section says the data obtained from the CDPP were "accessed using the speasy Python library", citing the Speasy software record, the JEDI data excepted.
9. `https://doi.org/10.3847/1538-4357/ae2601` — Fargette, N., et al. (2026). Fluid and Kinetic Properties of the Near-Sun Heliospheric Current Sheet. *The Astrophysical Journal*, 997, 174. Its acknowledgements credit the AMDA science analysis system and the speasy Python package, giving Speasy's documentation address, as the tools used to visualize data.
10. `https://doi.org/10.1029/2025GL119118` — Michotte de Welle, B., et al. (2026). Statistical Estimate of the Magnetopause Reconnection Rate as a Function of the Interplanetary Magnetic Field Clock Angle. *Geophysical Research Letters*, 53, e2025GL119118. Data Availability statement, as ADS's full-text index gives it: "The in situ data are available by using the Speasy package at Github", followed by the repository address and a citation of the Speasy Zenodo record. The publisher's page was not read.
11. `https://doi.org/10.1029/2025JA034657` — Hadid, L. Z., et al. (2026). Evidence of an Extended Alfvén Wing System at Enceladus: Cassini's Multi-Instrument Observations. *Journal of Geophysical Research: Space Physics*, 131, e2025JA034657. Data Availability statement, read in the HAL author manuscript (`hal-05507022`): "The data analysis has been done using Python and loading the data from Amda was done using Speasy is a free and open‐source Python package (Jeandet & Schulz, 2025)." Its reference list gives the Speasy record `https://doi.org/10.5281/zenodo.15583262`.
12. `https://doi.org/10.48550/arXiv.2610.16602` — Head, L., et al. (2026). An updated view of Jupiter's UV main auroral emission: large-scale analysis of UV and particle data from Juno's first 60 orbits. arXiv preprint arXiv:2610.16602. It uses MAG magnetometer data obtained "via the AMDA repository and associated speasy Python library provided by the CDPP", citing the Speasy software record.

**The three Michotte de Welle et al. papers (3, 5, 10)** are listed under rule 5 by user decision (2026-10-29), on the same test as the others: each paper's results were built with data retrieved through Speasy, and each says so deliberately in its Data Availability statement.

**Rule 4 adds nothing.** At `bb0ab30` the project presents no method or model paper as the basis of the software, and its citation guidance asks only for the software DOI (`CITATION.cff`: "If you use this software, please cite it as below." with the version DOI); the code has no reference blocks, and the only paper DOI in the tree, Louarn et al. (2021) below, is cited by an example notebook, which rule 4 does not count. Qualifying papers: none.

**Removed in the v1.9.1 update — `https://doi.org/10.5194/epsc-dps2025-1422`:** *Jeandet, A., Renard, B., Aunai, N., Ghisalberti, A., Génot, V., André, N., & Bouchemit, M. (2025). SciQLop & Speasy: Open-Source Tools for Unified Planetary and Heliospheric Data Analysis. EPSC-DPS Joint Meeting 2025, EPSC-DPS2025-1422.* HSSI listed it until this update. It is a meeting abstract (Crossref type `posted-content`; ADS `2025epsc.conf.1422J`), not an eligible publication (rule 1), and no poster or paper from that presentation is deposited: the Zenodo creator-keyed search on Alexis Jeandet's name and ORCID finds none from EPSC-DPS 2025. The user confirmed its removal on 2026-10-29. It should not be restored; if a poster or paper from that presentation is deposited later, that deposit is the candidate.

**Documented omission — `https://doi.org/10.1051/0004-6361/202141095`:** *Louarn, P., Fedorov, A., Prech, L., Owen, C. J., et al. (2021). Multiscale views of an Alfvénic slow solar wind: 3D velocity distribution functions observed by the Proton-Alpha Sensor of Solar Orbiter. Astronomy & Astrophysics.* The developers ship an example-gallery notebook, `docs/examples/alfvenic.ipynb`, whose title and opening cell cite this paper by DOI and whose analysis it reproduces using Speasy (`amda/solo_b_rtn_hr`, `pas_l2_omni`). Verified via Crossref. It is not listed: the paper does not itself describe, cite or use Speasy — it is the science result a documented Speasy example reproduces — and a paper cited only by an example is excluded under rule 4. It is retained here so that a future agent does not re-propose it.

**Weighed and not added:**
- `10.1029/2024JA032897`, Fargette, N., et al. (2024), "Statistical Study of Energy Transport and Conversion in Electron Diffusion Regions at Earth's Dayside Magnetopause", *Journal of Geophysical Research: Space Physics*, 129, e2024JA032897. Not listed, by the catalogue maintainer's decision of 2026-10-30 ("drop those two papers"). Its text was never read: the publisher (Wiley) answered automated requests with a human-verification check, which was not cleared, and no repository copy was found (HAL, OpenAlex and Semantic Scholar list none). Rule 5 was first applied to it on ADS evidence alone: a full-text probe restricted to the paper places `speasy` within 5 words of `package` in its body, and ADS lists the paper among those citing a Speasy Zenodo record (controls: the same probe matches papers 3, 5, 10 and 11, whose statements were read, and a nonsense token matches nothing). The deliberate credit rule 5 requires was therefore never confirmed. A later refresh that can read the paper should quote its statement here before weighing it again.
- `10.3847/1538-4357/ae5e62`, Lewis, H. C., et al. (2026), "Parker Solar Probe Observations of a Flux Rope Embedded in a Near-Sun Heliospheric Current Sheet Magnetic Reconnection Exhaust", *The Astrophysical Journal*, 1002, 125. Not listed, by the catalogue maintainer's decision of 2026-10-30 ("drop those two papers"). Its only credit to Speasy is the journal's Software statement, which lists AMDA and Speasy, with Speasy's documentation address, as ADS's full-text index gives it (ADS finds `speasy` in its acknowledgements and not in its body). The dossier's own reading, not a reason the maintainer gave: the statement names Speasy without saying what it was used for, where entries 2 and 7 say "Our analysis made use of" the CDPP tools that include it and entry 9 says the authors "visualize data" with it, so the statement reads as the list of tools that rule 6 describes. Rule 5 was first applied to it on that statement alone.
- Meeting abstracts (rule 1): Génot, V., et al. (2025), "Analyzing planetary and heliophysics plasma data with AMDA: the last 20 years", EPSC-DPS2025-1365 (`10.5194/epsc-dps2025-1365`), which describes AMDA's interfacing with Speasy; and the SciQLop EGU General Assembly abstracts of 2022, 2023, 2024 and 2025 (`10.5194/egusphere-egu22-5774`, `egu23-13581`, `egu24-3515`, `egu25-10101`), which list Speasy among SciQLop's tools.
- The same team's two DASH 2026 talks, deposited as slide decks, weighed in rule order (rules 1, 3, 5 and 6) from a searcher's view:
  - `10.5281/zenodo.23196188`, "Agentic LLM workflows inside SciQLop: data, literature, and the verification practices they require" (18 pages). The catalogue maintainer judged this deck standalone on 2026-10-29, as SciQLop's record notes, so rule 1 does not exclude it. Rule 3 does not fire either, read as for 23150226 below: its subject is SciQLop, not Speasy, and the one platform publication this field admits is the DASH 2026 poster. One of its use cases is built on data gathered through Speasy ("the agent gathered every solar-wind measurement in Speasy: 16 spacecraft, plus OMNI at Earth", then studied how the wind changes with distance), so rule 5 would include it. On 2026-10-29 the catalogue maintainer decided that it is not listed for Speasy, choosing the option "Readable; just not for Speasy". Its DOI did not resolve at doi.org on 2026-10-29 or 2026-10-30 (a 404, with no Handle record), although DataCite lists it as findable and Zenodo shows it on the deposit; the deposit's permanent landing page is `https://zenodo.org/records/23196188`, the form SciQLop's record uses.
  - `10.5281/zenodo.23150226`, "Ground-based and space-based radio spectra in SciQLop: interoperability obstacles from the client side" (16 pages). The catalogue maintainer judged this deck standalone on 2026-10-29, as SciQLop's record notes, so rule 1 does not exclude it; rules 3, 5 and 6 decide it. Rule 3's first clause does not fire: its subject is SciQLop, not Speasy. Nor does its second clause, which admits "one by an author about the platform the software serves": SciQLop, the application Speasy serves as data engine, is that platform, and the one publication about it that this field admits is the developers' DASH 2026 poster (entry 1), which presents the SciQLop stack and gives Speasy panels of its own; this deck has no section on Speasy, and to a searcher looking for Speasy it is a SciQLop talk. The field file does not say whether its "one" caps the count, so this reading is an interpretation, the one the solarmach record also applies (of the platform publications, it admits the one with a section on the software); should the clause come to be read otherwise, this deck is the one to revisit. Rule 5 does not fire either: the deck credits no result to Speasy. Speasy appears as SciQLop's built-in provider for CDAWeb, AMDA, CSA and SSCWeb, as a pending SuperMAG provider (one slide explains that SuperMAG publishes no per-station coverage, so that provider can only advertise a blanket 1975–2100 range for every station), and as an example of glue shared in a library, while the radio burst it shows comes through SciQLop's radio plugin, which builds on sunpy's Fido. Rule 6 fires, so it is not listed.
- `10.5281/zenodo.7261367`, "Space Physics data analysis with Speasy" (Modolo, Génot and Cecconi, 2022): a Zenodo software deposit of two Python scripts (`shock_normal_MVAB.py`, `DeHoffmann_Teller_calculation.py`) accompanying a manuscript, "Space Physics data analysis with AMDA, TOPCAT and 3Dview", submitted to the European Journal of Physics. A software deposit is not a publication (rule 1), and the manuscript was found in neither Crossref nor ADS on 2026-10-29.
- Mentions without deliberate credit for a result (rule 6): Barnum, J., et al. (2023), "Python in Heliophysics Community (PyHC): Current status and future outlook", *Advances in Space Research* (`10.1016/j.asr.2022.10.006`), which names speasy among non-core PyHC projects; Dresing, N., et al. (2026), "Comprehensive solar eruption analyses enabled by the tools of the SOLER project" (arXiv:2608.24458), which lists speasy among the existing packages its tools use; and Poirier, N. A. (2022), PhD thesis (arXiv:2208.11637), whose background text on AMDA says that "a python package speasy has been developed".
- Full-text matches unrelated to the software: arXiv:2507.19002 (an image-generation paper whose notation "s(Peasy" matched) and arXiv:2305.18424.
- Speasy's own Zenodo software records (rule 1).
- The AMDA reference papers `https://doi.org/10.1016/j.pss.2021.105214` (Génot et al. 2021, *Automated Multi-Dataset Analysis (AMDA)*) and `https://doi.org/10.1007/978-90-481-3499-1_16` (Jacquey et al. 2009) describe an upstream **data service** that Speasy consumes, not Speasy itself, and Speasy does not present them as its basis; they belong on AMDA's own record. The Zenodo and DataCite records for Speasy contain no publication-type `relatedIdentifiers` — only `IsSupplementTo` the GitHub tag plus the `HasVersion` sibling-release DOIs, which are versions, not publications.

**Search record (2026-10-29, all years; the first literature search this record documents):** ADS `full:"speasy" OR ack:"speasy" OR abs:"speasy" OR title:"speasy" OR full:"spz.get_data"` returned 29 records, every one weighed above (controls: `full:"qzxvwplmk"` → 0, `full:"pyspedas"` → 171, `full:"sciqlop"` → 16). ADS `citations(title:"speasy" doctype:software)` returned 7, among them paper 6, which full text did not reach. Semantic Scholar's reference lists were read for the AGU papers it exposes; DataCite gives the concept DOI a `citationCount` of 0. Zenodo: the creator-keyed search on `"Jeandet, Alexis"` and on his ORCID returned 9 records each, and free text `speasy` returned 3 (controls: `pyspedas` → 12, a nonsense token → 0). The project's own files at `bb0ab30` were swept for references (rule 4).

---

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found

**Weighed and not added — the 14 datasets defined in `speasy/data/archive/cda.yaml`.** Not listed, by the catalogue maintainer's decision of 2026-10-30, in his words: "I agree those datasets are only examples; drop them". They were first read under rule 3, as loaders written for those datasets; that decision supersedes the reading. The facts weighed: the first four were verified at `bb0ab30`, the last against the live SPDF catalogue, CDAS and AMDA's public tree on 2026-10-30:
- `cda.yaml` is the YAML inventory the generic direct-archive provider loads out of the box (`speasy/data_providers/generic_archive/__init__.py` reads `speasy/data/archive/`). Each entry is a layout descriptor — a master CDF, a file-name pattern under `https://cdaweb.gsfc.nasa.gov/pub/data/`, a split rule and a cadence — not code written for that dataset.
- Eight of the MMS entries (FGM survey and FPI/DES fast moments, MMS1–4) came in commit `bc87314` (2023-11-28), titled "Adds few more archive/cda MMS products as example"; the four FPI/DES burst entries and the two ERG entries are older.
- `docs/user/direct_archive/direct_archive.rst` calls `cda.yaml` "the inventory Speasy loads out of the box — which is why" `spz.inventories.data_tree.archive.cda` "already contains MMS and Arase (ERG) datasets before you add anything", and says of it and `themis_cdpp.yaml.example`: "Both files are also worth reading as real-world examples."
- Twelve of the 14 are three MMS products repeated for the four spacecraft.
- All 12 MMS datasets are also in CDAWeb's catalogue (`https://spdf.gsfc.nasa.gov/pub/catalogs/all.xml`), from which Speasy's CDAWeb provider builds its inventory, and in CDAS. The two ERG Level-3 products are in neither, because CDAWeb serves them only as files, so Speasy's CDAWeb provider does not list them, and AMDA's public observatory tree, read on 2026-10-30, has no Arase/ERG mission; `cda.yaml` is Speasy's only route to them.

On 2026-10-30, after being told that `cda.yaml` is Speasy's only route to the two ERG Level-3 products and that the "as example" commit added 8 of the 12 MMS entries, the catalogue maintainer confirmed the decision.

The 14, with the DOIs found for them, kept so that a later refresh does not resolve them again:

| # | Dataset (`cda.yaml` key) | Dataset | DOI |
|---|---|---|---|
| 1 | `erg_lepe_l3_pa` | ERG (Arase) LEP-e Level-3 pitch angle distribution electron flux | `https://doi.org/10.34515/DATA.ERG-04003` |
| 2 | `erg_pwe_hfa_l3_1min` | ERG (Arase) PWE/HFA Level-3 electron density, 1 min | `https://doi.org/10.34515/DATA.ERG-10001` |
| 3 | `mms1_fgm_srvy_l2` | MMS1 FGM survey Level 2 | `https://doi.org/10.48322/mxbx-r466` |
| 4 | `mms1_fpi_brst_l2_des_moms` | MMS1 FPI/DES burst Level 2 moments | `https://doi.org/10.48322/6172-zw20` |
| 5 | `mms1_fpi_fast_l2_des_moms` | MMS1 FPI/DES fast Level 2 moments | `https://doi.org/10.48322/550t-zy35` |
| 6 | `mms2_fgm_srvy_l2` | MMS2 FGM survey Level 2 | `https://doi.org/10.48322/xz3n-g079` |
| 7 | `mms2_fpi_brst_l2_des_moms` | MMS2 FPI/DES burst Level 2 moments | `https://doi.org/10.48322/tryj-n584` |
| 8 | `mms2_fpi_fast_l2_des_moms` | MMS2 FPI/DES fast Level 2 moments | `https://doi.org/10.48322/cqez-ga35` |
| 9 | `mms3_fgm_srvy_l2` | MMS3 FGM survey Level 2 | `https://doi.org/10.48322/8s4y-en47` |
| 10 | `mms3_fpi_brst_l2_des_moms` | MMS3 FPI/DES burst Level 2 moments | `https://doi.org/10.48322/8ypa-ba28` |
| 11 | `mms3_fpi_fast_l2_des_moms` | MMS3 FPI/DES fast Level 2 moments | `https://doi.org/10.48322/yaqw-7j55` |
| 12 | `mms4_fgm_srvy_l2` | MMS4 FGM survey Level 2 | `https://doi.org/10.48322/50p5-d131` |
| 13 | `mms4_fpi_brst_l2_des_moms` | MMS4 FPI/DES burst Level 2 moments | `https://doi.org/10.48322/20ws-ge68` |
| 14 | `mms4_fpi_fast_l2_des_moms` | MMS4 FPI/DES fast Level 2 moments | `https://doi.org/10.48322/62dq-ym51` |

**How each DOI was resolved.** MMS: from CDAWeb's own dataset descriptions (CDAS REST `https://cdaweb.gsfc.nasa.gov/WS/cdasr/1/dataviews/sp_phys/datasets?idPattern=<id>`, whose `Doi` and `SpaseResourceId` fields name, for example, `MMS1_FGM_SRVY_L2` → `10.48322/mxbx-r466` and `spase://NASA/NumericalData/MMS/1/FIELDS/FGM/Survey/Level2/PT0.125S`). Each of the 12 DOIs resolves, and DataCite gives the matching title and the SPASE landing page. ERG: CDAWeb serves these two Level-3 products as files only — CDAS lists `ERG_LEPE_L2_OMNIFLUX` and three `ERG_PWE_HFA_L2_SPEC_*` datasets, but neither Level-3 product — so their DOIs come from the ERG Science Center's JaLC-registered records. `10.34515/DATA.ERG-04003` is titled "Exploration of energization and Radiation in Geospace (ERG) LEPe Level-3 pitch angle distribution electron flux data", and its landing page points at the `erg/lepe/l3/pa/` directory; `10.34515/DATA.ERG-10001` is the PWE/HFA Level-3 electron density data, whose landing page points at `erg/pwe/hfa/l3`, and the PWE/HFA Level-3 master CDF carries the global attribute `DOI: 10.34515/DATA.ERG-10001` (as does the repository's `tests/resources/erg_pwe_hfa_l3_1min_00000000_v01.skeleton.yaml`). The LEP-e Level-3 master carries no DOI attribute. Both ERG DOIs resolve.

The field was empty before the v1.9.1 update and stays empty; the earlier version of this file had left these 14 unresolved.

**Considered and not added:** the 65,000+ products reachable through the providers' dynamic inventories (generic access, with no code written for any one of them); and `tests/resources/ac_h2s_mfi_cdaweb.nc`, a CDAWeb-derived netCDF fixture for the generic netCDF codec test, which shows the codec works rather than a reader built for that dataset.

---

### 29. Related Software (OPTIONAL)

**Values — 5.** Every entry below passed the Field 29/30 relevance gate; the gate reasoning is given per entry, and every rejection is recorded in the Note for audit purposes.

1. `https://github.com/SciQLop/SciQLop` — **SciQLop** (in HSSI; that entry's stored `code_repository_url`, copied byte for byte — rule 11)
   **Gate: PASSES — companion application.** The README's second paragraph is "Don't want to write code? See our graphical interface SciQLop", and the developers' own EPSC-DPS 2025 abstract describes Speasy as SciQLop's "data engine". `plan/REVIEW.md` also documents the shared community proxy server. Distinguishing and specific to Speasy, not generic.
   **URL:** HSSI held SciQLop's Zenodo concept DOI `https://doi.org/10.5281/zenodo.7379012` here until the v1.9.1 update. Rule 13 replaces a DOI with the repository URL when the target has a public repository, because the site shows the raw URL as link text; the concept DOI is recorded here so the choice can be reversed if HSSI ever renders resolved titles.

2. `https://github.com/SciQLop/Speasy.jl` — **Speasy.jl**
   **Gate: PASSES — cross-language wrapper of this exact package.** Advertised in the README main-features list ("Also available as Speasy.jl for Julia users") and in `docs/index.rst`; introduced by `HISTORY.rst` 1.5.0 ("docs: mention julia wrapper"). No Zenodo DOI was found, so the repository URL is used as the form permits.

3. `https://github.com/SciQLop/PyISTP` — **PyISTP**
   **Gate: PASSES — domain-specific important dependency.** `pyproject.toml` pins `pyistp>=0.8.2`, and it is the ISTP-compliance engine behind both codecs (`bundled_codecs/istp/cdf.py`, `istp/netcdf.py`, `istp/__init__.py`), inventory extraction (`core/cdf/inventory_extractor.py`), the CDAWeb master-CDF parser, and the generic archive provider. A heliophysics-specific library whose presence characterises the software; `HISTORY.rst` tracks PyISTP version bumps as user-visible changes (e.g. 1.6.0 "Bump PyISTP to cover cases where axis data is in master CDF").

4. `https://github.com/SciQLop/CDFpp` — **pycdfpp / CDFpp** (not in HSSI; the upstream repository root — rule 12)
   **Gate: PASSES — domain-specific dependency (heliophysics CDF-format library).** Imported directly in `bundled_codecs/istp/cdf.py`, the one module under `speasy/` that imports `pycdfpp` at the Source Revision and at `bb0ab30` alike, for reading and writing CDF, including `CDF_TIME_TT2000` conversion and gzip variable compression, and a declared dependency since v1.8.5 (`pycdfpp>=0.15.0`; before that it came in only through `pyistp`). On WebAssembly, micropip installs its wasm wheel from PyPI (v1.8.5; at v1.7.1 the WASM CI used a custom-built Pyodide distribution to preinstall it). Also identified in the PyHC context as related CDF software by the same author. An earlier version of this file also named `core/cdf/inventory_extractor.py` as importing it; that module mentions `pycdfpp` only in comments.
   **URL:** HSSI held CDFpp's Zenodo concept DOI `https://doi.org/10.5281/zenodo.6391115` here until the v1.9.1 update; rule 13 replaces it with the repository root, for the reason given under SciQLop, and records the DOI here.

5. `https://github.com/astropy/astroquery` — **astroquery**
   **Gate: PASSES — domain-specific important dependency, not generic infrastructure.** It is not arrays, dataframes, plotting or HTTP plumbing: `speasy/data_providers/csa/__init__.py` imports `astroquery.utils.tap.core.TapPlus` and builds the **entire** CSA (Cluster / Double Star) inventory over the IVOA TAP protocol. `request_dispatch.py::init_csa` even disables the whole CSA provider when `HTTP_PROXY` is set, citing astroquery issue #3228 — an astroquery limitation directly shapes Speasy's user-facing behaviour. Verified present at tag `v1.7.1`.

**Note — considered and REJECTED (audit trail):**
- **Tier A, always excluded — being a dependency is not relatedness:** `numpy`, `scipy`, `pandas`, `matplotlib`, `requests`, `python-dateutil`, `tqdm`, `PyYAML`, `packaging`, `urllib3`, `certifi`, `appdirs`, `humanize`, `pysocks`, `pytest`, `pytest-cov`, `ddt`, `flit_core`. Every one of these would read identically for an arbitrary Python package.
- **`pysciqlop-cache`** — a same-authors library, but it is a **cache**: it passes the "would this be equally at home in a web app, a finance model, or a biology pipeline?" test, so it is generic infrastructure despite the shared origin. Excluded from both Fields 29 and 30.
- **`diskcache`, `pyzstd`, `numcodecs`, `netCDF4`, `watchdog`, `IPython`, sphinx/docs toolchain** — generic infrastructure or build/test tooling. `diskcache` is a runtime dependency again at `bb0ab30`, and `numcodecs` backs the `blosc` extra added in v1.8.3; both are generic storage and compression. `cyclopts`, the command-line parser of `main`'s `speasy` tool (not in v1.9.1), is CLI parsing, generic as well. `netCDF4` is Tier B and is used only *internally* to implement the netCDF codec, which is explicitly insufficient.
- **AMDA, CDAWeb, CSA, SSCWeb, CDPP 3DView, University of Iowa Cassini Ephemeris Tool** — these are **web services / data sources**, not installable software; they are recorded in Field 17 and Fields 31/32 instead.
- **`hapiclient`, `hapiplot`, `pysat`, `pySPEDAS`, `sunpy`, `cdasws`** — plausible "performs similar tasks" peers, but **the repository references none of them**, so listing them would be speculation. `plan/BACKLOG.md` lists an unimplemented "PySPEDAS interface" wish (GH #235) — an unbuilt plan is not a relationship.
- **Blanket ecosystem claims** ("part of the scientific Python ecosystem", "a PyHC member, therefore interoperable with PyHC packages") were not used anywhere as justification.

---

### 30. Interoperable Software (OPTIONAL)

**Values — 5.** This field is gated on a *demonstrated exchange*, not on dependency presence; the specific evidence is named for each entry.

1. `https://github.com/SciQLop/SciQLop` — **SciQLop** (in HSSI; that entry's stored `code_repository_url` — rule 11)
   **Demonstrated exchange:** SciQLop is a peer application that runs *on top of* Speasy. The developers' EPSC-DPS 2025 abstract states "SciQLop, powered by Speasy, streamlines access to heterogeneous datasets"; the README directs non-programmers to SciQLop as the GUI over the same data engine; and both share the SciQLOP community proxy/cache server (`speasy/core/proxy/`, `CDPP3DVIEW_MIN_PROXY_VERSION`, and the README uptime badge for `sciqlop.lpp.polytechnique.fr/cache`). A host/plugin relationship between two domain tools, not a runtime coincidence.
   **URL:** HSSI held SciQLop's concept DOI `https://doi.org/10.5281/zenodo.7379012` here until the v1.9.1 update; it was replaced by the repository URL for the reason given in Field 29.

2. `https://github.com/SciQLop/Speasy.jl` — **Speasy.jl**
   **Demonstrated exchange:** an explicit **cross-language bridge** — a Julia wrapper that calls this package and surfaces `SpeasyVariable` data to Julia users. Advertised in the README feature list and in `docs/index.rst`.

3. `https://github.com/astropy/astropy` — **astropy** *(Tier B — admitted only with cited evidence, which exists here)*
   **Demonstrated exchange via a documented public adapter API, not internal use:** `SpeasyVariable.to_astropy_table() -> astropy.table.Table` (`speasy/products/variable.py`, line 578) is a documented public conversion, constructing the table with per-column units through `astropy.table.Table.from_pandas(df, units=umap, index=True)`. `SpeasyVariable.unit_applied(unit=None)` returns a variable whose values are `astropy.units.Quantity` objects (docstring: "values converted to astropy.units.Quantity according to given or found unit"). `docs/examples/SSCWeb.ipynb` imports `astropy.units` and combines it with Speasy output. This is a genuine data-model exchange and clears the Tier B bar.

4. `https://github.com/SciQLop/speasy_proxy` — **speasy_proxy** (not in HSSI; the upstream repository root)
   **Demonstrated exchange:** the server side of Speasy's community cache, a companion package designed to be used with this one (rule 7). Speasy's proxy client at `bb0ab30` (`speasy/core/proxy/__init__.py`: `query_proxy_version`, `GetInventory`, `GetProduct`, and `load_response`, which decodes a response "according to its Content-Type", including the blosc-compressed format added in v1.8.3) is written against this server's wire format, and `tests/test_proxy.py` keeps a "Copy of speasy-proxy's encoder (speasy_proxy/api/compression.py), the reference for the wire format." The README advertises the "SciQLOP ultra fast community cache server", and `docs/user/configuration.rst` documents pointing Speasy at it. It is Speasy-specific, unlike the generic `pysciqlop-cache` (Field 29). SciQLop's HSSI entry lists the same URL.

5. `https://github.com/jgieseler/solarmach` — **solarmach** (in HSSI; that entry's stored `code_repository_url`)
   **Demonstrated exchange, seen from the other side** (rule 7), found by the inbound sweep (rule 10): solarmach's HSSI entry lists Speasy as interoperable, and its `get_sw_speed` imports Speasy, walks `spz.inventories.data_tree.amda` and `.cda`, calls `spz.get_data(...).replace_fillval_by_nan().to_dataframe()` to obtain measured solar-wind speeds, and catches Speasy's `MissingCredentials` (`solarmach/__init__.py` lines 140–232 at solarmach `cd4d8366`). The Speasy APIs it uses are present at `bb0ab30`. The only other HSSI entry that lists Speasy, SciQLop, is reciprocated above.

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
- **Arase/ERG PWE/HFA** (Plasma Wave Experiment - High Frequency Analyzer) — `cda.yaml` ships `erg_pwe_hfa_l3_1min`; exercised by `tests/test_direct_archive_downloader.py` (which reads `tree.archive.cda.Arase_ERG.PWE.HFA.erg_pwe_hfa_l3_1min.ne_mgf`), `tests/test_direct_archive_inventory.py` and, at `bb0ab30`, `tests/test_inventories.py`. An earlier version of this file also named `tests/test_codecs.py`, which mentions no Arase/ERG product at `7a6281ff` or `bb0ab30`.

  The vocabulary contains the **observatory** row `SMWG/Observatory/ARASE` (added under Field 32) but **zero Arase/ERG instrument rows**. Recording these as bare names would create new identifierless, non-SPASE instrument rows in HSSI's controlled vocabulary, so they are omitted instead. The omission is documented rather than silent: both are genuinely supported, and both should be revisited if Arase/ERG instrument rows appear in a later upstream vocabulary refresh. Re-checked 2026-10-29 against the live vocabulary: still no Arase/ERG instrument row (searched by name, abbreviation, identifier and definition; the only hit is the observatory row), so both stay omitted.

**Note — considered and dropped (relevance gate), with reasons:**
- **`ACE Solar Wind Electron Proton Alpha Monitor` (SWEPAM)** — present in the prior `hssi_metadata.md` as "ACE/SWE", but **the current repository provides no evidence for it**: no README or docs example and no test references it (only ACE MFI and ACE Ephemeris appear). Per the seeding rule, file-only additions are carried forward *only where the repository still supports them*, so this one is **dropped**. Recorded here so the removal is visible rather than silent. (Note it is absent from live HSSI too, so no existing HSSI value is being removed.)
- **Fixture- and example-only instruments** — each appears only as a regression-test fixture or a documentation example for a *generic* feature, never with instrument-specific support: MMS FEEPS (`cda/MMS1_FEEPS_SRVY_L2_ELECTRON/...`), Cluster FGM and CIS-HIA (`tree.csa.Cluster.Cluster_1.CIS_HIA1....`, `tree.cda.Cluster.C1.FGM_SPIN....`), Cluster EFW (`csa/C1_CP_EFW_L3_P/...`), Solar Orbiter SWA-PAS (`tree.cda.Solar_Orbiter.SOLO.SWA_PAS....`), PSP IS-IS/EPI-Lo (`cda/PSP_ISOIS-EPILO_L2-PE/...`), STEREO HET (`cda/STA_L1_HET/Proton_Flux`, added purely as the fix for GH #223), THEMIS ESA/FGM/SCM, MAVEN STATIC, Juno JEDI, Equator-S MAM, Wind 3DP, ACE Ephemeris. Several appear more than once: at `bb0ab30` PSP IS-IS/EPI-Lo's `PSP_ISOIS-EPILO_L2-PE` is the shape example (an energy grid over every time and look-direction cell) in `tests/test_codec_coordinate_grids.py`, `tests/test_plotting_hints.py` and `tests/test_speasy_variable.py` as well as `tests/test_cdaweb.py`; Cluster CIS-HIA is the spectrogram example of `docs/user/plotting.rst`; STEREO HET is also the round-trip sample of `tests/test_hapi_codecs.py`; and THEMIS ESA and Juno JEDI each appear in two test files. Every one exercises generic code.
- **Values belonging to other fields:** generic multi-instrument file formats (CDF / netCDF / ISTP) -> Fields 18/19; multi-mission archives (CDAWeb, AMDA, CSA, SSCWeb) -> Field 17.

**Checked against v1.9.1 (`bb0ab30`):** `cda.yaml` is unchanged, the README examples still use the same MMS, ACE and Wind products, the 1.8.x and 1.9.x releases add no instrument-specific code, and each of the 19 identifiers still resolves to exactly one row of the live vocabulary on 2026-10-29.

**Stored rows kept by the catalogue maintainer's decision of 2026-11-01.** Fields 31 and 32 keep all 19 instrument rows and all 16 observatory rows as stored, by the catalogue maintainer's decision ("C: keep all 35"), although rule 23, which puts stored rows through Stage A on a refresh, would remove those resting only on examples, tests or docstrings. The decision covers Speasy's record only. Stage A as read at `bb0ab30`, kept so that these removals are not re-proposed or taken for an oversight:
- **Rule 6** (a provider or table written for the mission): Cluster and Double Star (the CSA provider, the missions' own archive), and Ulysses, Cassini, Voyager 1 & 2 and Galileo (UiowaEphTool's observer tables).
- **Rule 6 if the shipped `cda.yaml` entries are read as loaders, rule 3 if read as examples:** MMS FGM ×4 and FPI/DES ×4, and the MMS and Arase observatories.
- **Rules 2–3** (an archive-wide client's examples, tests or docstrings): ACE MAG, Wind MFI, Wind SWE, MMS FPI/DIS ×4 and MMS SCM ×4, and the ACE, Wind, MAVEN, OMNI, Parker Solar Probe, Solar Orbiter, THEMIS and Juno observatories. The package code that names some of them decides nothing under rule 4: the CDAWeb provider's `_burst_regex` only sizes requests and cache fragments for MMS FPI and SCM burst products, and `_xml_catalogs_parser.alias_rules` only renames inventory nodes (`AC`→`ACE`, `PSP`→`ParkerSolarProbe`, `mms1`→`MMS1`).

**How Fields 28 and 31/32 read `cda.yaml`.** Field 28 lists none of the 14 datasets defined in `cda.yaml`, by the catalogue maintainer's decision of 2026-10-30 that they are "only examples". The relevance gate of this field and Field 32 counts the same entries as shipped dataset definitions, and so as support for the instruments and missions they cover. Each decision stands for its own field only.

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
| 11 | `Exploration of energization and Radiation in Geospace` | `https://spase-metadata.org/SMWG/Observatory/ARASE` | The strongest evidence class available: `speasy/data/archive/cda.yaml` — shipped inside the package — hard-codes Arase/ERG dataset definitions (`erg_lepe_l3_pa`, `erg_pwe_hfa_l3_1min`) with master CDFs, URL patterns and split rules under `inventory_path: cda/Arase_ERG/...`; verified present at tag `v1.7.1`. Exercised by `tests/test_direct_archive_downloader.py` and `test_direct_archive_inventory.py` (the PWE/HFA Level-3 product), `test_cdaweb.py` (the `ERG_ORB_L2` orbit dataset) and, at `bb0ab30`, `test_inventories.py` (the PWE/HFA master CDF). An earlier version of this file also named `test_codecs.py` and `test_amda_parameter.py`, which mention no Arase/ERG product at `7a6281ff` or `bb0ab30`. (The `.html` duplicate row was normalised; the bare row's name is used.) |
| 12 | `Cassini Orbiter` | `https://spase-metadata.org/SMWG/Observatory/Cassini` | `speasy/data_providers/uiowa_eph_tool/__init__.py` hard-codes `"Cassini": "cass"` in every observer table (Sun, Venus, Earth, Jupiter, Saturn and all moon origins); `docs/user/data_providers.rst` and `docs/user/Uiowa_eph_tool/uiowa_eph_tool.rst` name the provider "University of Iowa **Cassini** Ephemeris Tool ... provides trajectories for Cassini, Ulysses, Voyager 1, and Voyager 2"; `tests/test_uiowa_eph_tool.py` and `tests/test_speasy.py` retrieve `Trajectories.{Callisto.Co_rotational, Saturn_baricentric.KSM, Sun.Ecliptic}.Cassini`; also in `tests/test_cdpp3dview.py`. |
| 13 | `Voyager 1 & 2` | `https://spase-metadata.org/SMWG/Observatory/Voyager` | `uiowa_eph_tool` hard-codes `"Voyager 1": "voy1"` and `"Voyager 2": "voy2"` in the Sun, Earth, Jupiter, Saturn, Jupiter-satellite and satellite-satellite observer tables; both are named in `docs/user/data_providers.rst` and the UiowaEphTool doc page. The single mission-level SPASE row is used deliberately (unique exact name). The per-spacecraft alternatives `SMWG/Observatory/Voyager1` and `.../Voyager2` were weighed and rejected: both are canonically named "Mariner Jupiter/Saturn A" and "... B", so recording them would file the mission under names that appear nowhere in Speasy or its documentation. |
| 14 | `Galileo Orbiter-Probe` | `https://spase-metadata.org/SMWG/Observatory/Galileo` | `uiowa_eph_tool` hard-codes `"Galileo": "gali"` in the Sun, Venus, Earth, Jupiter and Jupiter-satellite observer tables; `tests/test_uiowa_eph_tool.py` retrieves `Trajectories.Io.Geographic.Galileo`; also in `tests/test_cdpp3dview.py`. Unique exact-name match. |
| 15 | `Double Star Mission` | `https://spase-metadata.org/SMWG/Observatory/DoubleStar` | `docs/user/csa/csa.rst` at `7a6281ff`: the Cluster Science Archive "provides access to all science and support data from the ongoing Cluster (2000–present) and Double Star (2004–2008) missions. Its integration into Speasy makes it easy to get any public data from the CSA, handling both the webservice API and ISTP CDF file formats." At `bb0ab30` the page is reworded and still covers "the Cluster (2000–2024) and Double Star (2004–2008) missions". Repeated in `docs/user/data_providers.rst` ("Cluster and Double Star mission data") and `docs/examples/CompleteDemo.ipynb`. A documented statement of which missions a shipped provider covers. Three candidate rows exist; the **mission-level** row (unique exact name "Double Star Mission") is used rather than the per-spacecraft `DoubleStar1`/`DoubleStar2` rows, which are both named "Double Star". |
| 16 | `Juno Orbiter` | `https://spase-metadata.org/SMWG/Observatory/Juno` | **Moderate confidence — two independent sources.** (a) `tests/test_amda.py::test_get_templated_parameter` retrieves the Juno JEDI product `jedi_i90_flux` and asserts the templated result `jedi_i90_flux_4` — Juno data is the fixture for Speasy's AMDA templated-parameter feature; (b) the developers' own EPSC-DPS 2025 abstract names Juno as a driving mission ("The surge of planetary and heliospheric data from missions like MAVEN, Juno, and Solar Orbiter..."). Also present in `docs/examples/{alfvenic, CompleteDemo, CDAWeb, Cdpp3dView}.ipynb`. Unique exact-name match (the alternative row is `CNES/Observatory/CDPP-AMDA/Juno`, named just "Juno"). **This is the weakest-evidenced entry in the field**, and it is kept deliberately: two independent sources clear the designed-to-support gate, though by a narrower margin than any other entry here. |

**Note — considered and dropped (relevance gate), with reasons:**
- **Appear only inside auto-generated inventory dumps in example notebooks** — `docs/examples/Cdpp3dView.ipynb` and `SSCWeb.ipynb` print whole trajectory catalogues, which name dozens of bodies: Geotail, Polar, IMP-8, Interball, Van Allen Probes/RBSP, Rosetta, SDO, SOHO, Venus Express, Mars Express, Dimorphos/Didymos, Halley, 67P, and many moons. A catalogue listing is not designed-to-support.
- **Incidental regression-test fixtures** — STEREO (`cda/STA_L1_HET/Proton_Flux`, added as the fix for GH #223, and also the round-trip sample of `tests/test_hapi_codecs.py`), BepiColombo (one `"bepicolombo"` case in `tests/test_sscweb.py`), Equator-S (`tree.cda.Equator_S.EQ.MAM....`), and Moon (`sscweb/moon` — not an observatory at all).
- **Multi-mission archives** routed to Field 17 instead: CDAWeb, AMDA, CSA, SSCWeb, CDPP 3DView, OMNIWeb.
- **Consistency check:** THEMIS and Arase are added while STEREO/BepiColombo/Equator-S are not, because the former have shipped package data and/or broad multi-file test coverage while the latter appear only as fixtures for generic features. Juno is included on the strength of two independent sources (a feature test plus a developer statement), and is the weakest-evidenced entry in the field.

**Checked against v1.9.1 (`bb0ab30`):** the evidence cited for the 16 rows is present at the tag (`cda.yaml`, the UiowaEphTool observer tables, the README, docs and tests named above), except that `docs/user/csa/csa.rst`, cited for row 15, was reworded at the tag; the new wording still names Double Star (2004–2008) among the missions the CSA covers, and row 15 quotes both. The 1.8.x and 1.9.x releases add no observatory-specific code, and each identifier still resolves to exactly one row on 2026-10-29. The `hapi` provider on `main` (not in v1.9.1) reaches servers such as VirES for Swarm through the HAPI registry; an archive-wide client chosen at run time supports no observatory specifically (Field 31 rule 2).

**All 16 rows kept by the catalogue maintainer's decision of 2026-11-01.** The decision, the Stage A reading of each row, and how this field and Field 28 read `cda.yaml` are recorded under Field 31.

---

### 33. Logo (OPTIONAL)
- **Value:** `https://raw.githubusercontent.com/SciQLop/speasy/8f06d06f1e9c6e6013668c887c5c2546079b9b90/logo/logo_speasy_400dpi.png`

**Source:** From existing HSSI record — the submitted *asset* is preserved, recorded as a commit-pinned raw URL. The URL serves the logo file itself. The submitted value and the PyHC registry `logo` field both reference the same file on the `main` branch; the registry is authoritative about which asset is the logo, not about the URL string, and a branch reference breaks silently on any upstream rename, move or deletion, so the commit is pinned instead. The repository also contains `logo/logo_speasy.svg` (which also resolves, and is used in the README and docs headers), but Field 33 takes a single URL and the submitted PNG is kept. Re-verified 2026-10-29: the pinned URL returns `image/png`, `logo/` is unchanged at `bb0ab30`, and the README header and the PyHC registry `logo:` still present the same mark.

---

## Metadata Agreement

By submitting this metadata, you acknowledge and agree that any metadata you provide is submitted voluntarily and becomes part of the public domain. You waive all rights, claims, and interests to the submitted metadata, and grant unrestricted use, reproduction, modification, and distribution rights to the receiving party or its designees.

---

## Could not verify
- **Contribution-time affiliations for Vincent Génot and Nicolas André.** Both now carry recorded affiliations (Field 6), taken from their shared HSSI Person records. What remains unverifiable is the tie to Speasy itself: the repository states no affiliation for either, Génot's ORCID `employments` group is empty, and Crossref returns no affiliation strings for the AMDA reference paper he leads. André's ISAE-SUPAERO is ROR-corroborated by ORCID and his IRAP association is supported by the department and city of his other ORCID employment, but neither appears in Speasy's own metadata.
- **An ORCID for Benjamin Renard in Speasy's own metadata** — `CITATION.cff`, Zenodo and DataCite still carry none. The identifier recorded in Field 6 comes from the shared HSSI Person record and is independently verified against ORCID itself, not from the repository.
- **A ROR for CDPP** — the ROR v2 API returns no match for "Centre de Données de la Physique des Plasmas".
- **DOIs for Speasy.jl and PyISTP** — no Zenodo records found; repository URLs are used instead, which the form permits.
- **The full text of one weighed Field 27 paper** (Fargette et al. 2024): the publisher answered automated requests with a human-verification check, which was not cleared, and no repository copy was found; it is weighed and not listed (Field 27).
- **Two stale artifacts inside the repo, left as-is:** `HISTORY.rst` dates 1.7.1 as `2025-12-25`, contradicted by GitHub Releases, Zenodo, DataCite, `CITATION.cff` and the git tag (all 2025-12-18); and `plan/BACKLOG.md` still lists "HAPI client" and "NetCDF codec" as open P2 items although both shipped in v1.8.0, and still lists them at `bb0ab30` — the backlog is stale, not the code.

---

**End of HSSI Metadata Extraction**
