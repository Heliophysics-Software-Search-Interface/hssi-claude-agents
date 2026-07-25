# HSSI Metadata Extraction Results

**HSSI Software ID:** dab7d824-81ec-49ba-911a-b3d081469a84
**Repository:** https://github.com/SuperDARN/pydarn
**Source Revision:** 203ad0450906b8825b00dccf7b0126cd0fa5b955 (branch `main`, committed 2026-06-23)
**Relation to release tag:** this revision is **one commit after** tag `v4.3`, which points to `ae20850c6a812165e31989b245583d2e7f29a7f0`. The single intervening commit (`203ad04`, "update DOI link") is a **documentation-only change** adding the v4.3 DOI badge; it touches no package code, so `203ad04` and the tagged release are functionally identical for metadata purposes. `203ad04` is retained as the extraction revision.
**Extraction Date:** 2026-07-24
**Validation Date:** 2026-07-24
**Validation Status:** PASS

**Applied to HSSI:** 2026-07-25 — `PATCH http://localhost/api/data/software/dab7d824-81ec-49ba-911a-b3d081469a84/` returned HTTP 200 updating 14 fields (`authors`, `description`, `development_status`, `input_formats`, `interoperable_software`, `keywords`, `logo`, `related_datasets`, `related_instruments`, `related_phenomena`, `related_publications`, `related_software`, `software_functionality`, `version`). All 14 were roundtrip-verified against live HSSI with **0 discrepancies**; 6 new Person rows were created, **0** new Organization rows, and no existing value was dropped. Approved patch body SHA-256 `a0300ae8f241b3d0220c07af980976166792960475f80f9c08f94d405aa3aa58`.

**Two API-inexpressible corrections applied separately, 2026-07-25 (direct database edits, both user-approved):** `Person` row `a36dc72f…` `Galeshuck` → `Galeschuk`, and `Organization` row `06e0a335…` `SANSA` → `South African National Space Agency` + ROR `https://ror.org/02epph894`. Both were verified isolated to pyDARN beforehand and left the Person and Organization row counts unchanged (850 → 850, 285 → 285), i.e. in-place renames with no duplicate rows. Both are reflected in this file's Field 6 values, so it matches live HSSI exactly. They will reach the seed CSVs automatically via `export_db_csv()` on the campaign's next export — **no manual CSV edit is required**, and any hand-edit would be overwritten by that export.

**One open cleanup item:** Person row `0fd7b2c4…` (`P. Pitzer`, no ORCID) was orphaned by the approved substitution onto ORCID row `110061a1…`. It is now referenced by zero software, zero submitters and no curator. Deleting it is optional tidy-up and has **not** been done.

**Extraction mode:** Full metadata refresh, seeded from (a) live HSSI record `GET http://localhost/api/view/software/dab7d824-81ec-49ba-911a-b3d081469a84/` (local mirror of the 2026-07-23 production backup) and (b) the prior canonical `hssi_metadata.md` (extraction date 2025-10-09). Every seeded value was re-verified against the repository at the revision above and against primary DOI/registry sources.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Source:** To be provided by submitter (not stored in the HSSI view API).

---

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.3727269

**Source:** From existing HSSI record; confirmed by README.md DOI badge, `docs/user/citing.md`, `pydarn/utils/citations.py` (`pydarn2023 = 'DVWG, 2023, 10.5281/zenodo.3727269'`), and the DataCite/Zenodo APIs.
**Note:** Zenodo concept DOI covering all versions (`conceptdoi` / `conceptrecid` 3727269). Unchanged from live HSSI.

---

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/SuperDARN/pydarn

**Source:** From existing HSSI record; confirmed by Zenodo `metadata.custom["code:codeRepository"]`, PyHC community registry `code` field, and the local git remote.
**Note:** Unchanged. Default branch on GitHub is `develop`; `main` and `develop` are currently at the same commit (`203ad04`). The repository root URL is correct and stable.

---

### 4. Software Functionality (MANDATORY)
**Values:**
- Coordinate Transforms
- Coordinate Transforms:Ionospheric
- Coordinate Transforms:Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Calibration
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:File Format Conversion
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Mission-Specific
- Models and Simulations
- Models and Simulations:Data Guided
- Models and Simulations:Empirical

**Source:** Code analysis of the `pydarn` package at v4.3 (`203ad04`), plus `docs/user/*.md` tutorials and `pydarn/__init__.py` public API surface.

**Parent-category check:** every subcategory listed above has its parent listed (Coordinate Transforms, Data Processing and Analysis, Data Visualization, Models and Simulations). Verified.

**Per-value evidence:**
- **Coordinate Transforms** (parent) — `pydarn/utils/coordinates.py`, `pydarn/utils/geo.py`, `pydarn/utils/general_utils.py`; exposed publicly as `pydarn.Coords`, `pydarn.geocentric_coordinates`, `pydarn.calculate_azimuth`.
- **Coordinate Transforms:Ionospheric** — `Coords.AACGM` and `Coords.AACGM_MLT` in `coordinates.py` call `aacgmv2.get_aacgm_coord()` and `aacgmv2.convert_mlt()`; `convert2MLT()` computes magnetic local time. `docs/user/coordinates.md`. AACGM/MLT are the canonical ionospheric coordinate systems.
- **Coordinate Transforms:Magnetospheric** — geographic (GEO) to geomagnetic conversions used to build magnetic-coordinate axes and to map coastlines into magnetic coordinates (`pydarn/plotting/projections.py::convert_geo_coastline_to_mag`, `axis_geomagnetic`, `axis_geomagnetic_polar`); `pydarn/utils/geo.py` provides geodetic/geocentric, global/local spherical and Cartesian frame conversions. Carried over from the existing HSSI record. **>>> CHALLENGED — RESOLVED: RETAINED by explicit user decision, 2026-07-24 (see note below). <<<**

**>>> DISPUTED VALUE — `Coordinate Transforms:Magnetospheric` — DISPOSITION: RESOLVED 2026-07-24 — RETAINED by explicit user decision <<<**
- **Validator's challenge:** the supporting evidence is entirely AACGM/MLT, which is the *Ionospheric* subcategory; a repository-wide grep for the magnetospheric reference frames named in the taxonomy (GSM, GSE, SM) returns **zero** hits, so the value may be an over-classification.
- **Counter-argument for retention:** AACGM is a magnetic-**field-line-traced** coordinate system (Shepherd 2014, doi:10.1002/2014JA020264, cited by `pydarn.Citations`), i.e. it maps ionospheric locations along geomagnetic field lines and is the standard frame for expressing magnetosphere-ionosphere coupling; `pydarn/plotting/maps.py` evaluates convection potentials and fitted velocities that *are* the ionospheric footprint of magnetospheric convection; and this record independently lists **Earth Magnetosphere** under Field 5 (Related Region), which the Validator did not challenge.
- **Why it was not removed unilaterally:** the value is present in the **live HSSI record**, so deleting it is a destructive change to published metadata. Per the seeding rules, proposed removals stay visible rather than being silently applied.
- **RESOLUTION (2026-07-24):** the user was presented with the challenge and the counter-argument and **explicitly decided to retain the value**. It is therefore a settled, non-disputed member of Field 4 and is **not** part of any proposed removal. No further action.
- **Data Processing and Analysis** (parent) — see subcategories.
- **Data Processing and Analysis:Analysis** — `pydarn/plotting/power.py::plot_pwr0_statistic` (statistical analysis of lag-0 power with user-supplied statistical methods); `pydarn/plotting/maps.py::calculated_true_velocities`, `calculated_fitted_velocities`, `calculate_potentials`, `calculate_potentials_pos` (derivation of physical quantities); `docs/user/vels_and_potentials.md`.
- **Data Processing and Analysis:Calibration** — `pydarn/utils/recalculate_elevation.py::recalculate_elevation(dmap_data, tdiff, interferometer_offset=...)` recomputes interferometer elevation angles from raw phase (`phi0`) using a corrected `tdiff` calibration constant and array geometry; ported from RST `elevation_v2.c` and citing Shepherd (2017). Applying an instrument calibration parameter to convert measured phase into a corrected physical quantity. **NEW this extraction.**
- **Data Processing and Analysis:Data Access and Retrieval** — rests **solely** on genuine remote retrieval from a remote archive: `pydarn/utils/superdarn_radars.py::get_hdw_files()` (public, re-exported in `pydarn/__init__.py`) and `read_hdw_file(update=True)` download and unpack the SuperDARN hardware descriptor archive over HTTPS via `urllib.request` from `https://github.com/SuperDARN/hdw/archive/main.zip`. **Scope caveat:** this retrieves radar **hardware descriptor files**, not science data — `docs/user/superdarn_data.md` states explicitly that "pyDARN does not provide an interface for downloading data" and directs users to the SuperDARN mirrors. The package's local file-reading API (`read_fitacf`, `read_rawacf`, etc.) is deliberately **not** cited as evidence here, so this value is not read as a claim that pyDARN downloads science data.
- **Data Processing and Analysis:Data Reduction** — `pydarn/utils/filters.py::Boxcar` (3x3x3 median/threshold filter over beam-gate-time to suppress noise; `docs/user/filters.md`); `pydarn/utils/detrend.py::Detrend.detrend_running_mean` (running-mean smoothing).
- **Data Processing and Analysis:File Format Conversion** — `pydarn/io/superdarn_io.py::read_borealis` wraps `pydarnio.BorealisConvert` to convert Borealis RAWACF/BFIQ HDF5 files into the SuperDARN DMAP data structure (it writes an intermediate `dmap_file.rawacf` and returns `converter.sdarn_dict`); documented under `docs/user/io.md` § "Converting Borealis Files". `pydarn/utils/conversions.py::dmap2dict` converts DMAP records to plain dictionaries. **NEW this extraction.** *Caveat:* the converted product is returned in memory; the intermediate DMAP file is deleted.
- **Data Processing and Analysis:Processing** — general pipeline operations: `pydarn/utils/scan.py::build_scan/find_records_by_scan/find_records_by_datetime`, `pydarn/utils/range_estimations.py` (`gate2slant`, `gate2halfslant`, `gate2timeofflight`, `gate2groundscatter`, `gate2gs_bristow`), `pydarn/utils/plotting.py` (`find_record`, `check_data_type`, `time2datetime`, embargo handling), `Boxcar.run_filter` with multiprocessing. **NEW this extraction.**
- **Data Processing and Analysis:Time Series Analysis** — `pydarn/plotting/rtp.py::plot_time_series`, `pydarn/plotting/maps.py::plot_time_series`, `pydarn/plotting/iq.py::plot_time_series`, `pydarn/utils/plotting.py::TimeSeriesParams`; `pydarn/utils/detrend.py` (`detrend_savgol` using `scipy.signal.savgol_filter`, `detrend_running_mean`, `detrend_fitacf`) detrends FITACF parameter time series (new in v4.3).
- **Data Visualization** (parent) — the entire `pydarn/plotting/` subpackage (~7,200 lines) built on matplotlib/cartopy.
- **Data Visualization:2D Graphics** — `fan.py::plot_fan/plot_fan_input/plot_fov`, `grid.py::plot_grid`, `maps.py::plot_mapdata/plot_potential_contours/plot_heppner_maynard_boundary`, `rtp.py::plot_range_time/plot_coord_time` (`pcolormesh` range-time and coordinate-time images), `projections.py` polar/geographic/geomagnetic axes, `color_maps.py` custom colour maps.
- **Data Visualization:Line Plots** — `rtp.py::plot_time_series`, `acf.py::plot_acfs` / `plot_acf_param` (real/imaginary, power and phase versus lag), `iq.py::plot_iq_sequence/plot_iq_record/plot_iq_overview`, `power.py::plot_pwr0_statistic`.
- **Data Visualization:Mission-Specific** — the plot types are SuperDARN-specific data products: range-time-parameter (RTI) summary plots, radar field-of-view plots driven by the SuperDARN hardware database, convection (map-potential) plots with cross-polar-cap potential, Heppner-Maynard boundary and IMF dial, gridded-vector GRID plots, ACF/XCF lag plots, and Borealis/IQDAT I/Q sequence plots. Carried over from the existing HSSI record; still fully supported.
- **Models and Simulations** (parent) — see subcategories. **NEW this extraction.**
- **Models and Simulations:Data Guided** — `pydarn/plotting/maps.py` reconstructs and evaluates the SuperDARN map-potential model: `calculate_potentials`/`calculate_potentials_pos` evaluate the spherical-harmonic solution (associated Legendre expansion via `scipy.special.assoc_legendre_p_all`) from the fit coefficients (`N+2`) on an arbitrary magnetic lat/lon grid, and `calculated_fitted_velocities`/`calculated_true_velocities` derive convection velocities from the electric field of that fitted potential. Documented as a first-class user capability in `docs/user/vels_and_potentials.md`. This is a model driven by (and fitted to) observational line-of-sight velocities. **NEW this extraction.**
- **Models and Simulations:Empirical** — `pydarn/utils/virtual_heights.py` implements user-selectable empirical virtual height models (`VHModels.CHISHAM` — Chisham et al. 2008 "A new empirical virtual height model", doi:10.5194/angeo-26-823-2008 — and `VHModels.STANDARD`); `pydarn/utils/range_estimations.py::gate2gs_bristow` implements the Bristow et al. (1994) ground-scatter mapped-range model and `gate2groundscatter` the Thomas & Shepherd (2022) variant; `pydarn/utils/terminator.py` implements a solar-position/terminator model (Meeus astronomical algorithms). **NEW this extraction.**

**Considered and rejected (audit trail):**
- **Data Visualization:Spectrogram** and **Data Processing and Analysis:Spectrogram** — present in the prior canonical file (justified there by "ACF plots showing spectral/correlation data"). **Removed.** `pydarn/plotting/acf.py` plots the autocorrelation function real/imaginary components, power and phase against *lag* for a single range gate; there is no FFT, STFT, wavelet, periodogram or any other time-frequency transform anywhere in the package (grep for `fft|welch|periodogram|spectrogram` across `pydarn/` returns no computational hits; the only "spectral" matches are the SuperDARN *spectral width* parameter `w_l`, which is a scalar fit parameter, not a spectrum). Not supported by the code.
- **Data Visualization:Movies / 3D Graphics / Web-Based / Orbit Plots** — no `matplotlib.animation`, `mplot3d`, `Axes3D`, `plotly`, `bokeh` or orbit code anywhere in the package.
- **Data Processing and Analysis:Image Processing** — the `Boxcar` filter is a geophysical median filter over (beam, gate, time), not scientific image processing; no `scikit-image`.
- **Mission-related (top level and subcategories)** — pyDARN is a community analysis/visualization library, not part of a mission ground system or data-production pipeline (SuperDARN's production processing chain is RST). Mission specificity is captured by `Data Visualization:Mission-Specific`, Field 31 and Field 32 instead.
- **Models and Simulations:Observatory/Instrument Models** — the radar field-of-view computation is geolocation geometry from hardware descriptor files, not instrument-response simulation or synthetic observation generation.
- **Coordinate Transforms:Solar** — `terminator.py` computes solar declination/subsolar position for nightshade overlays; it does not convert between solar coordinate systems (Carrington/Stonyhurst/helioprojective).

**Comparison:** live HSSI has 10 values; the prior canonical file had 12. This extraction has 18 (superset of both, minus the unsupported Spectrogram value from the prior file).

---

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere
- Earth Magnetosphere

**Source:** From existing HSSI record; re-verified against the science content of the package.
**Analysis:** SuperDARN is a network of HF coherent-scatter radars measuring ionospheric plasma irregularities in Earth's upper atmosphere (E and F regions; virtual height models in `virtual_heights.py` explicitly map returns into the E and F regions). Its principal science product — the high-latitude convection pattern reconstructed in `pydarn/plotting/maps.py` — is the ionospheric footprint of magnetospheric convection, so the software directly supports Earth Magnetosphere science (cross-polar-cap potential, Heppner-Maynard boundary, IMF-driven convection). PyHC keyword `ionosphere_thermosphere_mesosphere` agrees. Unchanged from live HSSI.
**Considered and rejected:** *Interplanetary Space* — `maps.py::plot_imf_dial` displays the IMF By/Bz clock angle recorded in the map file, but this is a contextual annotation of solar-wind driving conditions, not science functionality for the interplanetary medium. *Planetary Magnetospheres* / *Solar Environment* — no support.

---

### 6. Authors (MANDATORY)

**Reconciliation note:** the author list is the **union** of live HSSI (12 authors), the prior canonical file (12 authors), `.zenodo.json` at v4.3 (12 creators), the DataCite record for the concept DOI (12 creators), and in-repo module authorship (copyright headers and git history). The v4.3 `.zenodo.json`/DataCite creator list **added** Wanner, Kucharyshen, Sylvestre and Sterne and **dropped** Hiyadutuje, Khanal, Chakraborty and Pitzer relative to earlier releases; per the union rule the four dropped contributors are retained (they contributed to the software and are present in live HSSI) and the four new ones are added. Two further authors — **Danno Peters** and **Francis Tholley** — are named in package copyright headers but appear in *no* citation source; they were added on validator findings [W3] and [W2]. Result: **18 authors**. Given/family splits and affiliations for pre-existing authors are preserved exactly as stored in live HSSI to avoid creating duplicate author records, with **one evidence-backed exception** applied on a validator finding: the given name `P.` → `Preston` with a newly attached ORCID (Author 12, [W5]). Two further evidence-backed corrections — the family name `Galeshuck` → `Galeschuk` (Author 5, [W4]) and the affiliation acronym `SANSA` → `South African National Space Agency` (Author 6) — were **identified but deliberately not applied** (user decision, 2026-07-24): neither is expressible through the HSSI Update API, so both are deferred to the seed-CSV workflow and this file mirrors what HSSI actually holds. The full evidence for each is retained under its author.

**Author 1:**
- **Name:** SuperDARN Data Visualization Working Group
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** From existing HSSI record; also `setup.cfg` `author =`, `.zenodo.json` first creator, DataCite creator 1, PyHC `contact`.
**Note:** This is an **organization** author (a working group). A ROR lookup (`https://api.ror.org/v2/organizations?query=SuperDARN`) returns **0 results**, so no organization identifier can be supplied. Live HSSI stores this entry with `givenName = "SuperDARN Data Visualization Working"` and `familyName = "Group"` (an artefact of DataCite recording it with `nameType: "Personal"`). The rendered name is correct either way, so the split is **left unchanged** to avoid creating a duplicate author record; flagged here for the curator's awareness.

**Author 2:**
- **Name:** Daniel D. Billett
- **Author Identifier:** https://orcid.org/0000-0002-8905-8609
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** From existing HSSI record (given/family split preserved); confirmed by `.zenodo.json` ("Billett, D.D.", ORCID, University of Saskatchewan) and DataCite. ROR from the live HSSI Organization row `fa54b15f-9620-4e57-b8d8-9c8cac5d69a5`.

**Author 3:**
- **Name:** Shibaji Chakraborty
- **Author Identifier:** https://orcid.org/0000-0001-6792-0037
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: https://ror.org/02smfhw86

**Source:** From existing HSSI record. **Retained by the union rule** — no longer listed in `.zenodo.json`/DataCite at v4.3, but present in live HSSI and credited on the reference publication (Frontiers 2022). ROR from live HSSI Organization row `f32614d5-4fce-4412-8564-a3a2febf5ece`.

**Author 4:**
- **Name:** M. Detwiller
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** From existing HSSI record; confirmed by `.zenodo.json` ("Detwiller, M.", no ORCID) and DataCite.
**Note (candidate improvement, not applied):** git history shows `mardet987 <marci.detwiller@usask.ca>`, i.e. the given name is likely "Marci". Not applied because changing the given name would change the author-identity key and could create a duplicate record; the authoritative citation file uses the initial.

**Author 5:**
- **Name:** Draven Galeschuk
- **Author Identifier:** https://orcid.org/0000-0003-3985-4225
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** Live HSSI record, with the surname corrected directly in the database on 2026-07-25 (see below). Given name, ORCID and affiliation are unchanged from the original HSSI record.
**Note — CORRECTION APPLIED 2026-07-25 via direct database edit: the previously stored surname `Galeshuck` was a transcription error; the correct spelling is `Galeschuk`.**
- **Evidence for the correct spelling:** `https://pub.orcid.org/v3.0/0000-0003-3985-4225/person` — the ORCID **already attached to this author in live HSSI** — returns given-names **"Draven"** and family-name **"Galeschuk"**. The given name matches live HSSI exactly, confirming this is the same person and that the stored surname is wrong. The misspelling "Galeshuck" is carried by **live HSSI, `.zenodo.json` and DataCite alike**, so it propagated from the Zenodo deposit into every downstream record; git history independently uses the correct form (`Draven Galeschuk <doreban@gmail.com>`). The ORCID registry is the person's own authoritative self-description and outranks the deposit metadata.
- **Why it could not be patched:** `SubmissionSerializer._get_or_create_person` (`django/website/models/serializers/submission.py:176`) matches an author by `identifier` first and then fills only **blank** names (`if not person.family_name: person.family_name = family_name`). Person row `a36dc72f-09af-464d-ab07-dfb907c778c1` already had a non-blank `family_name`, so a PATCH carrying "Galeschuk" was **silently ignored**; sending the corrected name *without* the ORCID would instead have created a duplicate Person row. The approved PATCH therefore deliberately carried the old spelling so no rejected write was attempted.
- **How it was applied instead (2026-07-25):** direct edit of `Person` row `a36dc72f-09af-464d-ab07-dfb907c778c1` in the local HSSI database (`family_name` only, via `save(update_fields=["family_name"])`), after asserting the row's ORCID matched and that it is referenced by **pyDARN only**. Person row count unchanged (850 → 850), confirming an in-place rename rather than a new row. Verified live: `GET /api/view/software/dab7d824-.../` now returns `Draven Galeschuk` with the same ORCID and affiliation. Because the campaign's seed CSVs are regenerated from this database by `export_db_csv()`, the correction will flow into `person.csv` automatically on the next export — no manual CSV edit is needed or wanted (a hand-edit would be overwritten by that export).

**Author 6:**
- **Name:** Alicreance Hiyadutuje
- **Author Identifier:** https://orcid.org/0000-0002-3391-8737
- **Affiliation:**
  - Organization: South African National Space Agency
  - Affiliation Identifier: https://ror.org/02epph894

**Source:** Live HSSI Organization row `06e0a335-8a81-4f48-b837-488e4564ff19`, renamed and given its ROR directly in the database on 2026-07-25 (see below). **Author retained by the union rule** — no longer listed in `.zenodo.json`/DataCite at v4.3.
**Note — ACRONYM EXPANSION APPLIED 2026-07-25 via direct database edit.**
- **The correct expansion is known:** "SANSA" is the **South African National Space Agency**, ROR `https://ror.org/02epph894` (confirmed via the ROR v2 API, whose record for that ROR lists "SANSA" as its acronym). Per the "expand acronyms" rule this fuller form would be preferred.
- **Why it could not be patched:** no Organization row matched that ROR and none matched that name, so `SubmissionSerializer._get_or_create_org` would have **created a second organization row**; and author affiliations are only ever `add()`ed (`django/website/models/serializers/submission.py:449`) and never removed. The author would have ended up affiliated with **both** "SANSA" and "South African National Space Agency". The approved PATCH therefore deliberately carried `{"name": "SANSA"}` with no identifier, so the existing row was reused and no duplicate created.
- **How it was applied instead (2026-07-25):** direct edit of `Organization` row `06e0a335-8a81-4f48-b837-488e4564ff19` in the local HSSI database (`name` and `identifier`), after asserting the row is not referenced by any award, is not a publisher or funder of any software, is affiliated with **Hiyadutuje only** (who authors pyDARN only), and that no existing Organization already carried the name or the ROR — so this is a clean rename, not a merge. Organization row count unchanged (285 → 285). Verified live: the affiliation still resolves to the same row id, now named "South African National Space Agency" with ROR `https://ror.org/02epph894`. As with the surname correction, `export_db_csv()` will carry this into `organization.csv` automatically on the campaign's next export.

**Author 7:**
- **Name:** Krishna Khanal
- **Author Identifier:** https://orcid.org/0000-0003-3927-7501
- **Affiliation:**
  - Organization: University of Alabama
  - Affiliation Identifier: https://ror.org/03xrrjk67

**Source:** From existing HSSI record. **Retained by the union rule** — no longer listed in `.zenodo.json`/DataCite at v4.3. Given/family names confirmed against ORCID 0000-0003-3927-7501 ("Krishna Khanal"). ROR from live HSSI Organization row `19ecb440-d144-4669-bc8d-8a3c6ebf4fad`.

**Author 8:**
- **Name:** K. Kucharyshen
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** **NEW** — `.zenodo.json` at v4.3 and the DataCite record for the concept DOI ("Kucharyshen, K.", University of Saskatchewan, no ORCID).
**Note (candidate improvement, not applied):** git history contains `KieranKuch <137737969+KieranKuch@users.noreply.github.com>`, suggesting the given name "Kieran". Not applied — no ORCID or citation-file confirmation, so the authoritative `.zenodo.json` initial is used rather than an inference.

**Author 9:**
- **Name:** Bharat S.R. Kunduri
- **Author Identifier:** https://orcid.org/0000-0002-7406-7641
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: https://ror.org/02smfhw86

**Source:** From existing HSSI record; confirmed by `.zenodo.json` ("Kunduri, B.S.R.", Virginia Tech, ORCID) and DataCite.

**Author 10:**
- **Name:** Carley J. Martin
- **Author Identifier:** https://orcid.org/0000-0002-8278-9783
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** From existing HSSI record; confirmed by `.zenodo.json` ("Martin, C.J.") and DataCite. Primary maintainer per recent commit history.

**Author 11:**
- **Name:** Danno Peters
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** **NEW — added on validator finding [W3].** Named as an Author in the `pydarn/utils/superdarn_radars.py` copyright header, with substantive feature commits in the git history. Affiliation from the committer email `Danno.Peters@usask.ca` (git authors `Danno Peters` / `DannoPeters`), giving University of Saskatchewan and its ROR `https://ror.org/010x8gc63`.
**Author Identifier: Not found.** An ORCID search for `family-name:Peters AND given-names:Danno` returned **0 results**, so no ORCID can be attached.
**Note:** Not present in live HSSI, `.zenodo.json` or DataCite — added because in-repo module authorship is primary evidence of authorship, and the union rule adds rather than replaces.

**Author 12:**
- **Name:** Preston Pitzer
- **Author Identifier:** https://orcid.org/0009-0007-0655-1347
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: https://ror.org/02smfhw86

**Source:** From existing HSSI record (affiliation); **given name expanded and ORCID added** on validator finding [W5].
**Note — CHANGE APPLIED vs. live HSSI, which stores the given name as the bare initial "P." and no author identifier.** `https://pub.orcid.org/v3.0/0009-0007-0655-1347` returns given-names **"Preston"**, family-name **"Pitzer"**, with employment **Virginia Tech, Research Assistant, start 2023-05**. Three independent signals corroborate the identification: the ORCID employment matches the Virginia Tech affiliation already stored in live HSSI; the git commit author is `PrestonXPitzer <prestonpitzer20@vt.edu>` (a `vt.edu` address); and `pydarn/__init__.py` credits "2023-06-20 PXP - added TimeSeriesParams to the __init__ file", whose date falls inside the ORCID employment period and whose initials match. Because a verified ORCID is now attached, author identity is keyed on the ORCID rather than on the name string, so expanding the given name is safe.
**Retained by the union rule** — no longer listed in `.zenodo.json`/DataCite at v4.3.

**Author 13:**
- **Name:** Remington A. Rohel
- **Author Identifier:** https://orcid.org/0000-0003-2208-1553
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** From existing HSSI record; confirmed by `.zenodo.json` ("Rohel, R.A.") and DataCite.

**Author 14:**
- **Name:** Marina T. Schmidt
- **Author Identifier:** https://orcid.org/0000-0002-3265-977X
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** From existing HSSI record; confirmed by `.zenodo.json` ("Schmidt, M.T."), DataCite, and copyright headers throughout `pydarn/`.

**Author 15:**
- **Name:** Kevin T. Sterne
- **Author Identifier:** https://orcid.org/0000-0002-1076-0009
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: https://ror.org/02smfhw86

**Source:** **NEW** — `.zenodo.json` at v4.3 and DataCite ("Sterne, K.T.", ORCID 0000-0002-1076-0009, Virginia Tech). Given name "Kevin" resolved from the ORCID public API (`https://pub.orcid.org/v3.0/0000-0002-1076-0009/person`); middle initial "T." from `.zenodo.json`. Also present in git history as `Kevin Sterne <kevintyler@vt.edu>`.

**Author 16:**
- **Name:** R. Sylvestre
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** **NEW** — `.zenodo.json` at v4.3 and DataCite ("Sylvestre, R.", University of Saskatchewan, no ORCID).
**Note (candidate improvement, not applied):** git history shows `RileySylvestre <nil625@usask.ca>`, suggesting the given name "Riley". Not applied — no ORCID or citation-file confirmation.

**Author 17:**
- **Name:** Francis Tholley
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Scranton
  - Affiliation Identifier: https://ror.org/05xwb6v37

**Source:** **NEW — added on validator finding [W2].** Named as module author in the `pydarn/utils/virtual_heights.py` copyright header ("(C) Copyright 2021 University of Scranton / Author(s): Francis Tholley"), which also supplies the affiliation; 25 commits between April and September 2021 (git author `Francis Tholley <francis.tholley@scranton.edu>`); and a named co-author — "Tholley, F. H." — of the Field 14 reference publication, Shi et al. (2022). Also credited in the `pydarn/plotting/rtp.py` modification log ("2021-05-12 Francis Tholley added gate2grounscatter to range-time plots") and in `virtual_heights.py` ("2021-09-15 Francis Tholley moved the chisham and standard virtual height models to separate file"). ROR for the University of Scranton resolved via the ROR v2 API.
**Author Identifier: Not found — deliberately withheld.** ORCID lists 11 people with the family name Tholley; the single "Francis Tholley" record (`0009-0007-9521-0981`) is **entirely empty** — no employments, no educations, no works — so it cannot be confirmed as this person and **is not attached**. Attaching an unverified ORCID would be worse than omitting the identifier.
**Note:** Particularly significant because `virtual_heights.py` is the module cited in Field 4 as the evidence for `Models and Simulations:Empirical`. Not present in live HSSI, `.zenodo.json` or DataCite.

**Author 18:**
- **Name:** Tristen D. Wanner
- **Author Identifier:** https://orcid.org/0009-0007-0616-5796
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: https://ror.org/02smfhw86

**Source:** **NEW** — `.zenodo.json` at v4.3 and DataCite ("Wanner, T.D.", ORCID 0009-0007-0616-5796, Virginia Tech). Given name "Tristen" resolved from the ORCID public API; middle initial "D." from `.zenodo.json`. Also present in git history as `Wtristen <wanner.tristen@gmail.com>`.

**Affiliation ROR verification:** University of Saskatchewan `https://ror.org/010x8gc63`, Virginia Tech `https://ror.org/02smfhw86`, University of Alabama `https://ror.org/03xrrjk67` (all three already stored on the live HSSI Organization rows and re-confirmed via the ROR v2 API); University of Scranton `https://ror.org/05xwb6v37` (newly resolved; new **for this record**, introduced with Author 17 — but the Organization row already exists in HSSI as `8ed44163-4384-4622-af9b-458efbdc52ed`, so it is reused rather than created). The South African National Space Agency ROR `https://ror.org/02epph894` was also resolved and verified, but is **not applied** — see Author 6.

---

### 7. Software Name (MANDATORY)
**Value:** pyDARN

**Source:** From existing HSSI record; confirmed by PyHC registry (`name: pyDARN`), DataCite title ("SuperDARN/pydarn: pyDARN v4.3"), README.md, and documentation site title.
**Note:** Unchanged. The PyPI/import name is lowercase `pydarn` (`setup.cfg` `name = pydarn`); the project's own branding, used throughout the docs and release titles, is "pyDARN". Editorial choice preserved.

---

### 8. Description (MANDATORY)
**Value:** Python data visualization library for the Super Dual Auroral Radar Network (SuperDARN). pyDARN provides comprehensive tools for reading, analyzing, and visualizing SuperDARN radar data, including range-time parameter plots, coordinate-time plots, fan plots, field-of-view plots, grid plots, convection maps, ACF plots, IQ plots, statistical power plots, and time-series visualizations. The package supports coordinate transformations between geographic, geomagnetic, and magnetic local time systems, and includes utilities for data filtering, detrending, elevation angle recalculation, range estimation, and virtual height calculations. pyDARN enables researchers to study ionosphere-magnetosphere coupling, plasma convection, and space weather phenomena using data from the international SuperDARN radar network.

**Source:** From existing HSSI record, minimally extended against the code at v4.3.
**Note — proposed change, wording otherwise preserved verbatim:** the seeded description enumerates plot types and utilities, and both enumerations had become materially incomplete. Only the two lists were extended; sentence structure, voice and every other word are unchanged. Additions and their evidence:
- "coordinate-time plots" — `pydarn/plotting/rtp.py::plot_coord_time`, `docs/user/coord_time.md`
- "field-of-view plots" — `pydarn/plotting/fan.py::plot_fov`, `docs/user/fov.md`
- "IQ plots" — `pydarn/plotting/iq.py` (`plot_iq_sequence`, `plot_iq_record`, `plot_iq_overview`), `docs/user/iq.md`
- "statistical power plots" — `pydarn/plotting/power.py::plot_pwr0_statistic`, `docs/user/power.md`
- "detrending" — `pydarn/utils/detrend.py` (new in v4.3; listed in the v4.3 release notes)
- "elevation angle recalculation" — `pydarn/utils/recalculate_elevation.py`

**Original live HSSI value (for reversion if the curator prefers no change):** "Python data visualization library for the Super Dual Auroral Radar Network (SuperDARN). pyDARN provides comprehensive tools for reading, analyzing, and visualizing SuperDARN radar data, including range-time parameter plots, fan plots, grid plots, convection maps, ACF plots, and time-series visualizations. The package supports coordinate transformations between geographic, geomagnetic, and magnetic local time systems, and includes utilities for data filtering, range estimation, and virtual height calculations. pyDARN enables researchers to study ionosphere-magnetosphere coupling, plasma convection, and space weather phenomena using data from the international SuperDARN radar network."

---

### 9. Concise Description (OPTIONAL)
**Value:** Python data visualization library for the Super Dual Auroral Radar Network.

**Source:** From existing HSSI record; identical to the PyHC registry `description` and to the one-line summary in README.md.
**Note:** Unchanged (74 characters, within the 200-character limit). The prior canonical file proposed a longer alternative; the seeded value is the project's own wording and is preserved.

---

### 10. Publication Date (RECOMMENDED)
**Value:** 2020-03-25

**Source:** From existing HSSI record; independently verified via DataCite for the first release DOI `10.5281/zenodo.3727270` ("SuperDARN/pydarn: pyDARN v1.0.0 release", version `v1.0.0`, `dates: [{date: 2020-03-25, dateType: Issued}]`).
**Note:** Unchanged.

---

### 11. Publisher (RECOMMENDED)

**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** From existing HSSI record (Organization row `ee990b81-8115-4ab4-8a7f-68a4d0bb345d`); confirmed by DataCite `attributes.publisher = "Zenodo"`.
**Note — correction to the prior canonical file:** that file recorded a Publisher Identifier of `https://ror.org/03cpe7c52`. That ROR resolves to the **Allen Institute**, not Zenodo, and a ROR v2 query for "Zenodo" returns **0 results** — Zenodo has no ROR. The live HSSI value `https://zenodo.org` is correct and is what the field definition prescribes as the fallback ("ROR identifier when available or URL otherwise"). Kept unchanged; the erroneous ROR is dropped.

---

### 12. Version (RECOMMENDED)

**Latest Version:**
- **Version Number:** v4.3
- **Version Date:** 2026-06-23
- **Version Description:** This minor release updates the SciPy version restriction and the associated code, and adds true velocity calculation in convection map plots, a FITACF data detrending algorithm, an option to snap a plot to the field of view of a given radar, and options to plot only ground scatter or only ionospheric scatter in fan and range-time plots. It also fixes plot_center for fields of view that did not correctly use magnetic longitude, and fixes updating of hardware (HDW) files on Windows.
- **Version PID:** https://doi.org/10.5281/zenodo.20820577

**Source:** git tag `v4.3` at `203ad04` (tagged 2026-06-23); `pydarn/version.py` (`__version__='4.3'`); GitHub release `v4.3` ("pyDARN v4.3", published 2026-06-23T21:28:32Z) release notes; Zenodo record 20820577 (`version: v4.3`, `publication_date: 2026-06-23`, `conceptdoi: 10.5281/zenodo.3727269`); DataCite for the concept DOI resolves to "SuperDARN/pydarn: pyDARN v4.3"; `docs/user/citing.md` lists "Release 4.3 ... 10.5281/zenodo.20820577".
**Note — changed vs. live HSSI, which holds v4.1.2 (2025-05-16, DOI 10.5281/zenodo.15441879).** Issue #57 flagged v4.2 (DOI 10.5281/zenodo.17943702) as newer; **v4.2 has itself been superseded by v4.3**, so v4.3 is recorded. The version description is the GitHub/Zenodo release-notes list rendered as prose to match the style of the stored v4.1.2 description; the verbatim release-notes bullets are: "Updated SciPy restriction and changes associated / NEW: True velocity in map plots / NEW: FITACF data detrending algorithm / NEW: Snap to a FOV of a given radar option / NEW: Option to plot only groundscatter or only ionospheric scatter in fan and RT plots / Bug Fix: Bug fix in plot_center for FOV that didn't appropriately use the magnetic longitude / Bug Fix: Updating HDW files on Windows fixed". (README.md's in-repo changelog lists only 4 of these 7 bullets — it **omits three**: "NEW: Snap to a FOV of a given radar option", "NEW: Option to plot only groundscatter or only ionospheric scatter in fan and RT plots", and the `plot_center` magnetic-longitude bug fix. The GitHub release and the Zenodo/DataCite abstract are the complete and authoritative list.)

---

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** From existing HSSI record; confirmed by `setup.cfg` (`python_requires = >=3.8`; classifiers for Python 3.8, 3.9, 3.10, 3.11 and **3.12**), `pyproject.toml` (setuptools build backend), and the fact that the repository is pure Python.
**Note:** Value unchanged. The supported-version range has grown since the prior extraction (3.12 classifier added; the prior canonical file recorded 3.8–3.11), but this does not change the controlled value. `.readthedocs.yaml` builds with Python 3.11.

---

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.3389/fspas.2022.1022690

**Source:** From existing HSSI record; confirmed by README.md ("our [publication]") and `docs/user/citing.md`.
**Note:** Unchanged. Shi, X., Schmidt, M., Martin, C. J., Billett, D. D., Bland, E., Tholley, F. H., Frissell, N. A., Khanal, K., Coyle, S., Chakraborty, S., Detwiller, M., Kunduri, B., & McWilliams, K. (2022). pyDARN: A Python software for visualizing SuperDARN radar data. *Frontiers in Astronomy and Space Sciences*, 9, 1022690.

---

### 15. License (RECOMMENDED)

**License:**
- **License:** GNU Lesser General Public License v3.0 only
- **License URI:** https://www.gnu.org/licenses/lgpl-3.0-standalone.html

**Source:** From existing HSSI record; confirmed by DataCite `rightsList` (`rights: "GNU Lesser General Public License v3.0 only"`, `rightsUri: "https://www.gnu.org/licenses/lgpl-3.0-standalone.html"`, `rightsIdentifier: "lgpl-3.0"`, SPDX scheme), the repository `LICENSE` file, `setup.cfg` (`license_files = LICENSE`; classifier "License :: OSI Approved :: GNU Lesser General Public License v3 (LGPLv3)"), Zenodo `metadata.license.id = "lgpl-3.0"`, and per-module copyright headers throughout `pydarn/`.
**Note:** Unchanged. SPDX identifier `LGPL-3.0-only`.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- aacgm
- aurora
- data analysis
- electric field
- general
- ionosphere
- ionosphere thermosphere mesosphere
- magnetosphere
- mlt
- plotting
- radar
- space physics
- space weather
- superdarn
- superdarn data
- visualization

**Source:** Set-union of live HSSI (9 terms), the prior canonical file, and the PyHC registry, all mapped onto HSSI's controlled `Keyword` vocabulary (508 rows, fetched from `/api/models/Keyword/rows/all/`). Every value above is an existing row in that vocabulary — no free-text terms were invented.

**Mapping and provenance:**
- **Kept from live HSSI (9):** `ionosphere`, `ionosphere thermosphere mesosphere`, `magnetosphere`, `plotting`, `radar`, `space physics`, `superdarn`, `superdarn data`, `visualization`. (The live view API renders these in Title Case — "Ionosphere", "Superdarn Data" — but the stored vocabulary rows are lowercase, as listed here.)
- **From the prior canonical file, normalized to the vocabulary:** `plots` → existing `plotting`; `superdarn-data` → existing `superdarn data`; `ionosphere_thermosphere_mesosphere` → existing `ionosphere thermosphere mesosphere` (the vocabulary contains **both** the underscore and the spaced form; the spaced form is the one already attached to this record, so the underscore duplicate is deliberately not added); `data_analysis` → `data analysis` (**added**); `general` → `general` (**added**). Both of these are PyHC-curated keywords for pyDARN.
- **Newly added, repo-evidenced (5):**
  - `aacgm` — `pydarn.Coords.AACGM` / `Coords.AACGM_MLT`, `aacgmv2` dependency in `setup.cfg`, `docs/user/coordinates.md`.
  - `mlt` — `pydarn/utils/coordinates.py::convert2MLT` / `aacgm_MLT_coordinates`, MLT tick labelling in `projections.py::mlt_ticklabels`.
  - `aurora` — SuperDARN is the Super Dual **Auroral** Radar Network; the package's convection and fan plots are used for auroral-zone science.
  - `electric field` — `pydarn/plotting/maps.py` derives convection velocities from the electric field of the fitted electrostatic potential (`calculated_fitted_velocities`, `calculate_potentials`); `docs/user/vels_and_potentials.md`.
  - `space weather` — already asserted by the record's own description ("space weather phenomena"); supported by the cross-polar-cap-potential and IMF diagnostics in `maps.py`.
**Considered and rejected:** `data visualization` and `3D visualization` (near-duplicate of the existing `visualization` / not supported); `python` and `python package` (true but generic — carries no distinguishing information); `polar` (ambiguous with the Polar mission); `coordinate transformation` variants (already fully captured by Field 4 and by `aacgm`/`mlt`).

---

### 17. Data Sources (OPTIONAL)
**Values:**
- Observatory/Mission-specific

**Source:** From existing HSSI record; re-verified. pyDARN reads SuperDARN-specific data products (IQDAT, RAWACF, FITACF, GRID/GRD, MAP, SND in DMAP format, plus Borealis RAWACF/BFIQ HDF5). Cross-listed with Field 32 (Related Observatories: SuperDARN), as the field guidance requires.
**Note:** Unchanged.
**Considered and rejected (audit trail):** *HTTP/HTTPS Directories* — `pydarn/utils/superdarn_radars.py::get_hdw_files()` does retrieve `https://github.com/SuperDARN/hdw/archive/main.zip` over HTTPS via `urllib.request`, but that retrieves **radar hardware descriptor files**, not science data. `docs/user/superdarn_data.md` states outright: "pyDARN does not provide an interface for downloading data" and directs users to the SuperDARN Canada (Globus), BAS and NSSC mirrors for data acquisition. Claiming an HTTP data source would mislead a user searching HSSI on that facet. *FTP/FTPS Directories*, *CDAWeb*, *HAPI*, *S3/Cloud-aware* — no support anywhere in the code.

---

### 18. Input File Formats (RECOMMENDED)
**Values:**
- HDF5
- Other

**Source:** Set-union of live HSSI (`Other` only) and the prior canonical file (`HDF5`, `Other`); both verified against the code.
**Note — changed vs. live HSSI: `HDF5` added.** Evidence: `pydarn/io/superdarn_io.py::read_borealis` reads Borealis RAWACF/BFIQ files, which are HDF5, via `pydarnio.BorealisConvert`; `docs/user/io.md` § "Converting Borealis Files" warns "There may be some issues with using `hdf5` libraries on a Windows machine". `Other` covers DMAP (Data Map), the SuperDARN community's self-describing binary format, which is not on the controlled list — `docs/user/io.md`: "Data Map (DMap) is a binary self-describing format that was developed by the SuperDARN community", supporting IQDAT, RAWACF, FITACF, GRID/GRD, MAP and SND file types, with transparent `.bz2` decompression. Hardware descriptor files (`pydarn/utils/hdw`, read by `read_hdw_file`) are plain text and also fall under `Other`.

---

### 19. Output File Formats (RECOMMENDED)
**Value:** Not found

**Source:** Code analysis at v4.3.
**Note:** Unchanged (live HSSI stores no output formats). pyDARN is a visualization and analysis library: it returns matplotlib figures/axes and Python data structures. A repository-wide search for write operations (`savefig`, `to_csv`, `.write`, `open(...,'w')`) finds **no** data-file writing in `pydarn/`; the only file writes are `get_hdw_files()` unpacking downloaded hardware text files and the transient `dmap_file.rawacf` created and immediately deleted inside `read_borealis`. Users save figures through matplotlib themselves (PNG/PDF/SVG), which are not values in the controlled list.

---

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Operating System Independent
- Windows

**Source:** From existing HSSI record; confirmed by `docs/user/install.md`, whose installation matrix has columns for **Ubuntu | OpenSuse | Fedora | OSX | Windows**, and by the v4.3 release note "Bug Fix: Updating HDW files on Windows fixed" (evidence of active Windows support). `.github/workflows/ruff.yml` runs on `ubuntu-latest`. Pure-Python package installable with `pip install pydarn`.
**Note:** Unchanged. `OS Independent` is **not** added even though the controlled list contains it, because live HSSI already carries the synonymous `Operating System Independent` and adding both would create a redundant duplicate.

---

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Source:** From existing HSSI record; re-verified. Pure Python with no compiled extensions in this repository (`pyproject.toml` build-backend `setuptools.build_meta`, no C/Fortran sources, no `ext_modules`). Architecture support is inherited from the wheels of the dependencies (numpy, scipy, matplotlib, cartopy, aacgmv2).
**Note:** Unchanged. Specific architectures (x86-64, Apple Silicon arm64, aarch64) are all subsumed by `CPU Independent`.

---

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Geomagnetic Storms

**Source:** HSSI controlled `Phenomena` vocabulary (`/api/models/Phenomena/rows/all/` — 7 rows: Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission).
**Note — NEW; live HSSI stores no related phenomena, and the prior canonical file recorded "Not found in standard list" on the basis of an older, solar-only vocabulary that did not include `Geomagnetic Storms`.** Evidence for the claim: `pydarn/plotting/maps.py` visualizes and computes the standard geomagnetic-activity diagnostics — the cross-polar-cap potential (`pot.drop`, `add_map_info`), the Heppner-Maynard boundary (`plot_heppner_maynard_boundary`), the IMF By/Bz driving conditions (`plot_imf_dial`) and the full high-latitude convection pattern (`calculate_potentials`, `plot_potential_contours`) — which are the primary observables used to characterize geomagnetic storms and substorms with SuperDARN.
**Flagged as a judgment call** for the validator/curator: the link is via the ionospheric convection response rather than a direct measurement of storm indices, so this value can reasonably be struck.
**Considered and rejected:** *Solar Wind* — `plot_imf_dial` merely annotates a convection map with the IMF clock angle recorded in the map file; pyDARN provides no solar-wind science functionality. All solar phenomena (Coronal Heating, CMEs, Solar Corona, Solar Flares, X-ray emission) — not applicable.

---

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** `setup.cfg` classifier `Development Status :: 5 - Production/Stable`; sustained release cadence (v4.1.2 in 2025-05, v4.2, v4.3 tagged 2026-06-23); HEAD commit dated 2026-06-23 with 2026-dated modification entries inside the source (e.g. `rtp.py`: "2026-04-20 Carley Martin added options for remove_iono_scatter and remove_ground_scatter"); five active feature/fix branches on the remote; PyHC registry rates `software_maturity: Good` and `community: Good`. Matches repostatus.org "Active" — reached a stable, usable state and being actively developed.
**Note — NEW: live HSSI has no `developmentStatus` value at all.** The prior canonical file recorded "Active"; retained and re-verified.

---

### 24. Documentation (RECOMMENDED)
**Value:** https://pydarn.readthedocs.io/en/main/

**Source:** From existing HSSI record; confirmed by README.md ("pyDARN's documentation can be found here"), the PyHC registry `docs` field, `mkdocs.yml`, and `.readthedocs.yaml`. URL re-checked on 2026-07-24: **HTTP 200**.
**Note:** Unchanged. Includes the installation guide at `https://pydarn.readthedocs.io/en/main/user/install/`, satisfying the "including installation instructions" requirement. (`setup.cfg` `url =` still points at the `/en/latest/` alias; the `/en/main/` form stored in HSSI and used by the README and PyHC is the canonical one.)

---

### 25. Funder (OPTIONAL)
**Value:** Not found

**Source:** DataCite `attributes.fundingReferences` is an empty array for the concept DOI; no funding statement in README.md, `setup.cfg`, `.zenodo.json`, or the documentation.
**Note:** Unchanged. `docs/user/citing.md` records that SuperDARN *data* is "funded by national scientific funding agencies of Australia, Canada, China, France, Italy, Japan, Norway, South Africa, United Kingdom and the United States of America", but that is an acknowledgement for the radar network's observations, not a funder of this software, so it is deliberately not recorded here.

---

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Source:** DataCite `attributes.fundingReferences` empty; no award number or grant title anywhere in the repository or DOI metadata.
**Note:** Unchanged.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values:**
- https://doi.org/10.1029/93JA01470
- https://doi.org/10.5194/angeo-26-823-2008
- https://doi.org/10.1002/2014JA020264
- https://doi.org/10.1002/2017RS006348
- https://doi.org/10.1029/2022RS007429

**Source:** `pydarn/utils/citations.py` (the `Citations` class, exposed publicly as `pydarn.Citations`) and `docs/user/citing.md`.
**Note — NEW; live HSSI stores no related publications (the prior canonical file listed only the reference publication, which is recorded separately in Field 14).** These are the algorithm/method publications the developers explicitly prioritize: `pydarn.Citations.print_citations()` prints them with the instruction "If using pyDARN produced plots in publications please be aware of the following citations that may have been used to produce your plot and should be included in your publication". Each is implemented in the code:
- **10.1029/93JA01470** — Bristow, W. A., Greenwald, R. A., & Samson, J. C. (1994). Ground scatter mapped range; implemented in `pydarn/utils/range_estimations.py::gate2gs_bristow`.
- **10.5194/angeo-26-823-2008** — Chisham, G., Yeoman, T. K., & Sofko, G. J. (2008). Empirical virtual height model; implemented in `pydarn/utils/virtual_heights.py::chisham` and `standard_virtual_height`.
- **10.1002/2014JA020264** — Shepherd, S. G. (2014). AACGM-v2 definition; the coordinate system used by `pydarn.Coords.AACGM` via `aacgmv2`.
- **10.1002/2017RS006348** — Shepherd, S. G. (2017). Elevation angle determination for SuperDARN HF radar layouts; implemented in `pydarn/utils/recalculate_elevation.py` (header: "Modified from the RST elevation_v2.c code").
- **10.1029/2022RS007429** — Thomas, E. G., & Shepherd, S. G. (2022). Virtual height characteristics of ionospheric and ground scatter; implemented in `pydarn/utils/range_estimations.py::gate2groundscatter`.

**Additional candidates considered but not included as values** (they describe the SuperDARN network and its data rather than this software; `docs/user/citing.md` recommends them under "How to cite the SuperDARN Community"): Greenwald et al. (1995) https://doi.org/10.1007/BF00751350; Chisham et al. (2007) https://doi.org/10.1007/s10712-007-9017-8; Nishitani et al. (2019) https://doi.org/10.1186/s40645-019-0270-5. Also considered: the example Jupyter notebook accompanying the reference publication, https://zenodo.org/record/7005203 (README notes "This notebook may be out of date"). Recorded here so the curator can promote any of them if desired.

---

### 28. Related Datasets (OPTIONAL)
**Value:** https://www.frdr-dfdr.ca/repo/collection/superdarn

**Citation form (human reference only; not the stored value):** SuperDARN RAWACF data collection [Data set]. Federated Research Data Repository (FRDR). https://www.frdr-dfdr.ca/repo/collection/superdarn

**Source:** `docs/user/superdarn_data.md`, under a heading titled literally `## RAWACF Data`: "Raw data with DOI's can be accessed on [FRDR](https://www.frdr-dfdr.ca/repo/collection/superdarn). These data are published once all gaps are checked and PIs are happy with the collection for each year and no data is under embargo."
**Note — NEW; live HSSI and the prior canonical file both stored nothing here.** The value is recorded as the **bare collection URL** because HSSI stores Related Datasets as URLs: `SubmissionSerializer._get_or_create_related` runs every entry through `_validate_url`, so a prose citation is rejected with HTTP 400. The APA-style citation is kept directly above for human reference only. (Recorded as the collection URL rather than a DOI because the collection landing page exposes **no collection-level DOI** — checked 2026-07-24.)

**Independently verified evidence for the relationship (2026-07-24):**
- The FRDR SuperDARN collection is the year-by-year archived **RAWACF/DAT** corpus (1996–2023), authored by "Super Dual Auroral Radar Network" — precisely the data product pyDARN is built to read. The repository's link to it sits under a heading titled literally `## RAWACF Data`.
- pyDARN exposes `read_rawacf` as top-level public API (`pydarn/__init__.py:27`), and `pydarn/plotting/power.py:28` and `pydarn/plotting/acf.py:41` are documented as plotting "SuperDARN RAWACF data".
- **The relationship is reciprocal and machine-readable.** The FRDR dataset *SuperDARN 2023 RAWACF* (`https://doi.org/10.20383/103.01307`) lists in its own **Related Identifiers**: "This dataset is supplemented by `https://doi.org/10.5281/zenodo.15441879`" — **that is pyDARN v4.1.2**, the exact version currently stored in HSSI — alongside `https://doi.org/10.5281/zenodo.4435150` (RST) and `https://github.com/SuperDARN/hdw`. The archive itself therefore asserts the link back to this software; this is far stronger than a one-way documentation mention.
- The individual **annual** datasets do carry real DOIs (e.g. `10.20383/103.01307`), even though the collection page does not. The collection URL was chosen deliberately as the non-arbitrary pointer covering all years rather than singling out one year. **Optional future enrichment:** add the per-year dataset DOIs alongside (or instead of) the collection URL.
**Also considered:** the SuperDARN hardware descriptor repository https://github.com/SuperDARN/hdw (a git submodule at `pydarn/utils/hdw` and the target of `get_hdw_files()`) — it is radar configuration metadata rather than a science dataset and has no DOI, so it is not recorded as a value.

---

### 29. Related Software (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.801458
- https://doi.org/10.5281/zenodo.4009470
- https://doi.org/10.5281/zenodo.1212694
- https://github.com/vtsuperdarn/davitpy

**Source and per-entry relevance justification** (relevance gate applied *before* identifier lookup):
- **`10.5281/zenodo.801458` — SuperDARN Radar Software Toolkit (RST).** *Carried over from live HSSI, retained.* The SuperDARN community's C-based radar software toolkit: the peer/counterpart toolkit that produces the FITACF, GRID, MAP and SND products pyDARN visualizes. Referenced from the documentation (`docs/user/io.md` links to the RST docs for the DMap format; `docs/user/vels_and_potentials.md` links to the RST map-file reference for the fit parameters pyDARN evaluates), and `pydarn/utils/recalculate_elevation.py` is a port of RST's `elevation_v2.c`. DataCite title verified: "SuperDARN Radar Software Toolkit (RST) 5.1.1".
- **`10.5281/zenodo.4009470` — pyDARNio.** **NEW.** The SuperDARN-specific I/O library maintained by the same working group; `setup.cfg` pins `pydarnio>=2.0.0` and `pydarn/__init__.py` re-exports its readers directly into pyDARN's public namespace. A domain-specific, characterizing dependency and companion package — not generic infrastructure. Also cited by `pydarn.Citations` (`pydarnio2023`). DataCite title verified: "SuperDARN/pyDARNio: pyDARNio v2.0".
- **`10.5281/zenodo.1212694` — aacgmv2.** **NEW.** The AACGM-v2 heliophysics coordinate library; a domain-specific dependency that characterizes what pyDARN does (`pydarn/utils/coordinates.py` imports `aacgmv2` and `Coords.AACGM`/`AACGM_MLT` are built on it) and is cited by `pydarn.Citations` (`burrell2023`). Concept DOI used (DataCite title "aburrell/aacgmv2: Version 2.7.1"); `citations.py` cites the version-specific `10.5281/zenodo.7621545`.
- **`https://github.com/vtsuperdarn/davitpy` — DaViTPy.** **NEW.** The predecessor Virginia Tech SuperDARN Python toolkit that pyDARN's plotting was derived from. Direct in-repo evidence: `pydarn/plotting/rtp.py` header — "This code is improvement based on rti.py in the DaVitpy library / https://github.com/vtsuperdarn/davitpy/blob/master/davitpy"; `pydarn/plotting/acf.py` header — "This code is based on acf.py in the DaVitpy library"; plus colormap-derivation comments at `rtp.py:391` and `rtp.py:1847`. Field 29 explicitly covers "software this work was forked from". No DOI found; repository URL used as the field permits.

**Considered and rejected (Tier A generic infrastructure — being a dependency is not relatedness):** `numpy`, `scipy`, `matplotlib`, `cartopy`, `pyyaml` (all of `setup.cfg` `install_requires` except `pydarnio` and `aacgmv2`). Each would be equally at home in a web app, a finance model or a biology pipeline; listing them would say nothing that isn't true of most of the ecosystem. `cartopy` is mapping infrastructure and is rejected on the same basis despite being cited in `citations.py`. `setuptools` (build backend) likewise.

---

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.4009470
- https://github.com/SuperDARNCanada/borealis

**Source and per-entry demonstrated-exchange evidence:**
- **`10.5281/zenodo.4009470` — pyDARNio.** **NEW.** Genuine demonstrated exchange, not mere dependency: `pydarn/__init__.py` re-exports pyDARNio's readers (`from pydarnio import read_iqdat, read_rawacf, read_fitacf, read_grid, read_map, read_snd, read_dmap`) as pyDARN's own public API; the two packages share a data model (lists of DMAP record dictionaries) that flows unchanged from pyDARNio's readers into every pyDARN plotting entry point; `pydarn/io/superdarn_io.py` calls the `pydarnio.BorealisConvert` adapter; `pydarn/utils/conversions.py::dmap2dict` converts pyDARNio's DMAP structures to plain dictionaries. `docs/user/io.md` closes by directing users to pyDARNio for further reading/writing needs. Companion package by the same working group.
- **`https://github.com/SuperDARNCanada/borealis` — Borealis.** **NEW.** Cross-tool adapter: `pydarn.read_borealis(filename, slice_id=...)` is a purpose-built converter that ingests files produced by the Borealis SuperDARN radar operating system (RAWACF and BFIQ HDF5) and returns them in pyDARN's SDARN data model, with explicit handling of Borealis slice IDs and of files produced before Borealis v0.5. Documented in `docs/user/io.md` § "Converting Borealis Files". Output of one tool imported into the other via a named adapter API — exactly the Field 30 bar. No DOI located; repository URL used as the field permits.

**Considered and rejected:**
- **Tier A, always excluded:** `numpy`, `scipy`, `matplotlib`, `cartopy`, `pyyaml`. Being a dependency is not interoperability.
- **`aacgmv2`** — recorded in Field 29 as a characterizing domain dependency, but **not** here: pyDARN calls into it as a library; there is no bidirectional exchange, adapter, shared data model, or plugin relationship.
- **RST (`10.5281/zenodo.801458`)** — an arguable Field 30 entry (RST's FITACF/GRID/MAP output is pyDARN's input, a real cross-language exchange with a named domain tool, documented in `docs/user/io.md` and `docs/user/vels_and_potentials.md`). **Not duplicated here** because it is already carried in Field 29 on the live record. Flagged for the curator in case promotion to Field 30 is preferred.
- **Blanket claims not used:** "part of the standard scientific Python ecosystem" and "a PyHC member, so it interoperates with PyHC packages" were explicitly *not* relied upon.

---

### 31. Related Instruments (OPTIONAL)

**Instrument 1:**
- **Instrument Name:** SuperDARN Radars
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SuperDARN/Radars

**Source:** Resolved against HSSI's controlled vocabulary at `/api/models/InstrumentObservatory/rows/all/` (7,648 rows; fetched to file and filtered locally). Filtering on `type == 1` (instrument) yields exactly **one** row matching "SuperDARN Radars" (row id `f5c62429-9d44-4ff0-ae61-1186005f1335`), with no `.html` duplicate. Name copied verbatim. The identical row set is returned by production `https://hssi.hsdcloud.org` and by the local target, so the resolution is instance-independent.
**Relevance gate — passes ("designed to support"):** pyDARN is purpose-built for SuperDARN HF radar data. It embeds the complete hardware description of every SuperDARN radar (`pydarn/utils/superdarn_radars.py`, 687 lines, with `RadarID`, `SuperDARNRadars`, `read_hdw_file`, `get_hdw_files` and the `pydarn/utils/hdw` submodule), computes each radar's beam/range-gate geolocation and field of view from those hardware parameters, implements SuperDARN-specific data formats and control-program identifiers (`superdarn_cpid.py`), and reads/plots every SuperDARN data product. A user searching HSSI for SuperDARN radar software would certainly expect this package back.
**Note — NEW; live HSSI stores no related instruments.** The prior canonical file had the free-text string "SuperDARN radars (international network of HF coherent scatter radars)", which would not have matched the controlled vocabulary; it is replaced with the resolved canonical name plus SPASE identifier.
**Deliberately not expanded:** the vocabulary also contains individual IUGONET instrument rows (SuperDARN Hokkaido East/West HF radar, SuperDARN King Salmon HF radar, SENSU SuperDARN Syowa East/South HF radar). pyDARN supports all 35+ network radars equally through its hardware database, so listing four arbitrary members would misrepresent the coverage; the umbrella "SuperDARN Radars" row is the correct single entry.

---

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** SuperDARN
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SuperDARN

**Source:** Resolved against `/api/models/InstrumentObservatory/rows/all/`. Filtering on `type == 2` (observatory) yields exactly **one** row named "SuperDARN" (row id `26339745-8c88-4046-a7ba-8197c9c51614`, SMWG namespace, no `.html` duplicate). Name copied verbatim.
**Relevance gate — passes:** the software exists to read, process and visualize the SuperDARN network's data products; cross-listed with Field 17 (`Observatory/Mission-specific`) as the field guidance requires.
**Note — value unchanged from live HSSI (which stores the bare name "SuperDARN"); the SPASE identifier is now supplied** so the entry binds deterministically instead of relying on a name lookup.
**Deliberately not expanded:** the IUGONET observatory rows for individual sites (SuperDARN Hokkaido East/West, King Salmon) are members of the same network, not separate targets of this software.

---

### 33. Logo (OPTIONAL)
**Value:** https://raw.githubusercontent.com/SuperDARN/pydarn/main/docs/imgs/pydarn_logo.png

**Source:** Repository file `docs/imgs/pydarn_logo.png` on the `main` branch; verified 2026-07-24 to return **HTTP 200, `image/png`, 24,081 bytes** — byte-identical to the file served by the previously stored URL.
**Note — changed vs. live HSSI (stale ref path corrected).** Live HSSI, README.md (first line) and the PyHC `projects.yml` `logo` field all point at `.../pydarn/**master**/docs/imgs/pydarn_logo.png`. **No `master` ref exists on the remote** — `git ls-remote` lists only `develop`, `main` and four topic branches — so that URL resolves solely through GitHub's legacy default-branch alias, which survived the `master` → `main`/`develop` rename and is not a guaranteed-stable contract. The value is therefore repointed at the **branch** form `main`, which is a real ref on the remote and currently identical to `develop`.
**Why the branch form rather than a tag:** the tag-pinned `.../v4.3/docs/imgs/pydarn_logo.png` also returns HTTP 200, but would freeze the logo at v4.3 and require an update at every release; the `main` branch form survives future releases.
**Upstream follow-up (outside HSSI's control):** PyHC's `projects.yml` still carries the stale `master` URL, and so does the repository's own README.md. Worth reporting upstream, but it does not block this correction.

---

## Extraction Summary

### Sources consulted
1. **Live HSSI record** — `GET http://localhost/api/view/software/dab7d824-81ec-49ba-911a-b3d081469a84/` (seed / authoritative baseline)
2. **Prior canonical `hssi_metadata.md`** — extraction dated 2025-10-09 (seed)
3. **DataCite API** — concept DOI `10.5281/zenodo.3727269`, plus `10.5281/zenodo.3727270` (v1.0.0), `10.5281/zenodo.20820577` (v4.3), `10.5281/zenodo.801458` (RST), `10.5281/zenodo.4009470` (pyDARNio), `10.5281/zenodo.1212694` and `10.5281/zenodo.7621545` (aacgmv2)
4. **Zenodo API** — record 20820577 (v4.3) and concept record 3727269
5. **GitHub API** — release `v4.3` notes and publication timestamp
6. **PyHC registry** — all three YAML files read in full; pyDARN found in `projects.yml` (community packages)
7. **ORCID public API** — full given names for Wanner (0009-0007-0616-5796), Sterne (0000-0002-1076-0009), Khanal (0000-0003-3927-7501); family-name correction for Galeschuk (0000-0003-3985-4225); given name + Virginia Tech employment for Preston Pitzer (0009-0007-0655-1347). **Negative results, recorded so they are not re-litigated:** no confirmable ORCID for Francis Tholley (the sole matching record, 0009-0007-9521-0981, is entirely empty), none for Danno Peters (0 search results), and none for Detwiller, Kucharyshen or Sylvestre
8. **ROR v2 API** — University of Saskatchewan, Virginia Tech, South African National Space Agency, University of Alabama, University of Scranton; negative results for "Zenodo" and "SuperDARN"
9. **HSSI controlled vocabularies** — `InstrumentObservatory` (7,648 rows), `Keyword` (508 rows), `Phenomena` (7 rows), `Organization` (285 rows)
10. **Repository at `203ad04`** — `README.md`, `LICENSE`, `setup.cfg`, `pyproject.toml`, `.zenodo.json`, `.readthedocs.yaml`, `.gitmodules`, `mkdocs.yml`, `.github/workflows/`, all 34 modules under `pydarn/`, all 20 pages under `docs/user/`, `test/`, git tags and full author history

**Not present in this repository:** `CITATION.cff`, `codemeta.json`, `AUTHORS`, `CONTRIBUTORS`, `CHANGELOG.md` (the changelog lives in `README.md` and in GitHub release notes).
**SoMEF:** not run for this refresh — the fields SoMEF supplies (name, description, version, license, keywords, documentation, logo, dates) were all obtained from higher-priority sources (live HSSI, PyHC, DataCite/Zenodo, GitHub API, and direct repository inspection), per the metadata priority order.

### Fields changed relative to live HSSI
| Field | Change |
|---|---|
| 4. Software Functionality | 10 → 18 values (added Calibration, Data Access and Retrieval, Data Reduction, File Format Conversion, Processing, Models and Simulations + Data Guided + Empirical) |
| 6. Authors | 12 → **18** (added Sterne, Sylvestre, Wanner, Kucharyshen from `.zenodo.json` v4.3; **Peters** and **Tholley** from package copyright headers). Given name `P.` → **`Preston`** Pitzer, with ORCID `0009-0007-0655-1347` newly attached. Affiliations otherwise unchanged; University of Scranton (`https://ror.org/05xwb6v37`) is new for this record but already exists as an HSSI Organization row. **Identified but not applied, deferred to the seed-CSV workflow:** `Galeshuck` → `Galeschuk` and Hiyadutuje's `SANSA` → `South African National Space Agency` (see Authors 5 and 6) |
| 8. Description | Two enumerations extended (coordinate-time, field-of-view, IQ and statistical power plots; detrending, elevation angle recalculation); all other wording preserved verbatim |
| 12. Version | v4.1.2 → **v4.3**; date 2025-05-16 → 2026-06-23; new description; PID → https://doi.org/10.5281/zenodo.20820577 |
| 16. Keywords | 9 → 16 (added aacgm, aurora, data analysis, electric field, general, mlt, space weather) |
| 18. Input File Formats | `Other` → `HDF5`, `Other` |
| 22. Related Phenomena | (empty) → `Geomagnetic Storms` |
| 23. Development Status | (empty) → `Active` |
| 27. Related Publications | (empty) → 5 method-paper DOIs |
| 28. Related Datasets | (empty) → `https://www.frdr-dfdr.ca/repo/collection/superdarn` (the FRDR SuperDARN RAWACF collection) |
| 29. Related Software | 1 → 4 (added pyDARNio, aacgmv2, DaViTPy) |
| 30. Interoperable Software | (empty) → pyDARNio, Borealis |
| 31. Related Instruments | (empty) → SuperDARN Radars + SPASE identifier |
| 32. Related Observatories | `SuperDARN` (bare name) → same name + SPASE identifier |
| 33. Logo | `.../pydarn/`**`master`**`/docs/imgs/pydarn_logo.png` → `.../pydarn/`**`main`**`/docs/imgs/pydarn_logo.png` (no `master` ref exists on the remote; the old URL survives only via GitHub's legacy default-branch alias) |

**Unchanged from live HSSI:** Fields 2, 3, 5, 7, 9, 10, 11, 13, 14, 15, 17, 19, 20, 21, 24, 25, 26.

### Fields changed relative to the prior canonical file
- **4** — removed the unsupported `Data Visualization:Spectrogram`; restored `Data Visualization:Mission-Specific`; added Calibration, File Format Conversion, Processing and the three Models and Simulations values.
- **6** — 12 → **18** authors; affiliation RORs added throughout; names otherwise aligned to live HSSI's stored given/family splits, except the one **applied** ORCID-verified correction (Preston Pitzer). The equally ORCID-verified Galeschuk correction is fully documented but **not applied** — see Author 5.
- **11** — dropped the incorrect Zenodo ROR `https://ror.org/03cpe7c52` (that ROR is the Allen Institute; Zenodo has no ROR).
- **12** — v4.1.2 → v4.3.
- **13** — Python classifier range now includes 3.12 (value unchanged).
- **16** — normalized to HSSI's controlled `Keyword` vocabulary; 7 terms added.
- **20** — `OS Independent` replaced by live HSSI's `Operating System Independent` (no duplicate).
- **22** — "Not found in standard list" → `Geomagnetic Storms` (the live vocabulary now contains it).
- **33** — logo repointed from the nonexistent `master` ref to the `main` branch (the prior canonical file also carried the `master` URL).
- **27, 28, 29, 30, 31, 32** — populated/expanded as described above; free-text instrument and observatory strings replaced with resolved SPASE names and identifiers; the dependency list in Field 29 replaced with relevance-gated entries carrying DOIs/URLs.

### Unresolved / flagged for the validator and curator
1. **Description change (Field 8)** — a factual completeness fix to an otherwise preserved editorial value. The original text is recorded verbatim under that field for one-step reversion.
2. **Hiyadutuje's affiliation (Field 6) — CLOSED 2026-07-25: expansion applied by direct database edit.** The PATCH deliberately carried `SANSA` (unpatchable: no Organization row matched that ROR or name, so the API would have created a second row, and affiliations are only ever added, never removed). After the PATCH landed, org row `06e0a335…` was renamed in place to "South African National Space Agency" with ROR `https://ror.org/02epph894`, having first verified it is affiliated with Hiyadutuje only and is not a funder or publisher anywhere. Organization count unchanged at 285. Full record under Author 6.
3. **Organization author split (Field 6, Author 1)** — live HSSI stores "SuperDARN Data Visualization Working Group" as `givenName` + `familyName`. Left unchanged deliberately; there is no ROR for the working group, so no organization identifier can be supplied.
4. **Full given names still not applied** for Detwiller (likely "Marci"), Kucharyshen (likely "Kieran") and Sylvestre (likely "Riley") — inferred from git history only, with no ORCID or citation-file confirmation, and applying them would change author-identity keys. (Pitzer has been **removed from this list**: his ORCID `0009-0007-0655-1347` is verified, so the given name "Preston" is now applied and identity is keyed on the ORCID rather than the name string.)
5. **Surname spelling — CLOSED 2026-07-25: corrected to `Galeschuk` by direct database edit.** The ORCID registry entry for `0000-0003-3985-4225` (the ORCID already stored in live HSSI for this author) gives family-name "Galeschuk", matching git history; "Galeshuck" in live HSSI, `.zenodo.json` and DataCite was a transcription error propagated from the Zenodo deposit. The PATCH deliberately carried the old spelling (unpatchable: the API matches by ORCID then fills only blank names, so it would have been silently ignored). After the PATCH landed, person row `a36dc72f…` was renamed in place, having first verified it is referenced by pyDARN only. Person count unchanged at 850. Full record under Author 5.
6. **Two authors added with no author identifier** — Danno Peters and Francis Tholley. Both are named in package copyright headers; neither could be matched to a confirmable ORCID (Tholley's only candidate record is empty; Peters returns no search results). They will be created as name-only author records.
7. **`Coordinate Transforms:Magnetospheric` (Field 4) — RESOLVED 2026-07-24: RETAINED by explicit user decision.** The Validator argued the evidence is entirely AACGM/MLT (i.e. Ionospheric) and that a repo-wide grep for GSM/GSE/SM returns zero hits. The counter-argument (AACGM is a field-line-traced frame; `maps.py` convection potentials are the ionospheric footprint of magnetospheric convection; Field 5 independently lists Earth Magnetosphere) was presented alongside it, and the user chose to keep the value. It is **not** part of any proposed removal. Full record under Field 4.
8. **Related Phenomena `Geomagnetic Storms` (Field 22) — RESOLVED 2026-07-24: INCLUDED by explicit user decision.** The live Phenomena vocabulary has only 7 rows, six of them solar (Coronal Heating, Coronal Mass Ejections, Solar Corona, Solar Flares, Solar Wind, X-ray emission); `Geomagnetic Storms` is the only geospace term available and is the best fit for SuperDARN convection science (`maps.py` computes cross polar cap potential and the Heppner-Maynard boundary). `Solar Wind` was considered and rejected — the IMF dial is a plot annotation, not a solar-wind analysis capability. Fills a currently empty field; non-destructive.
9. **Related Datasets (Field 28) — RESOLVED 2026-07-24: INCLUDED by explicit user decision, recorded as the bare collection URL `https://www.frdr-dfdr.ca/repo/collection/superdarn`.** HSSI stores Related Datasets as URLs (`_get_or_create_related` → `_validate_url`), so the APA-style citation could not be the stored value and is kept alongside it for human reference. The relationship was then **independently verified and is stronger than a one-way documentation mention**: the FRDR dataset *SuperDARN 2023 RAWACF* (`https://doi.org/10.20383/103.01307`) lists in its own Related Identifiers "This dataset is supplemented by `https://doi.org/10.5281/zenodo.15441879`" — pyDARN v4.1.2, the exact version HSSI currently stores — so the archive asserts the link back to this software. The collection page carries **no collection-level DOI**, but the individual annual datasets do; the collection URL was chosen as the non-arbitrary pointer covering all years. **Optional future enrichment:** add the per-year dataset DOIs. Fills a previously empty field; non-destructive.
10. **RST placement (Fields 29/30)** — kept in Field 29 as seeded; it also satisfies the Field 30 exchange test. Curator may prefer to add it to Field 30.
11. **Logo (Field 33) — RESOLVED; change applied.** The URL is repointed from the nonexistent `master` ref to the `main` branch. Remaining follow-up is upstream and outside HSSI's control: PyHC's `projects.yml` and the repository's own README.md both still carry the stale `master` URL.
