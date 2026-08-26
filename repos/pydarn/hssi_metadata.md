# HSSI Metadata Extraction Results

**HSSI Software ID:** dab7d824-81ec-49ba-911a-b3d081469a84
**Repository:** https://github.com/SuperDARN/pydarn
**Source Revision:** 203ad0450906b8825b00dccf7b0126cd0fa5b955 (branch `main`, committed 2026-06-23)
**Relation to release tag:** this revision is **one commit after** tag `v4.3`, which points to `ae20850c6a812165e31989b245583d2e7f29a7f0`. The single intervening commit (`203ad04`, "update DOI link") is a **documentation-only change** adding the v4.3 DOI badge; it touches no package code, so `203ad04` and the tagged release are functionally identical for metadata purposes. `203ad04` is retained as the extraction revision.
**Extraction Date:** 2026-07-24
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Note:** Submitter contact is submission-only information and is not part of the public software metadata recorded in this dossier.

---

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.3727269

**Source:** From existing HSSI record; confirmed by README.md DOI badge, `docs/user/citing.md`, `pydarn/utils/citations.py` (`pydarn2023 = 'DVWG, 2023, 10.5281/zenodo.3727269'`), and the DataCite/Zenodo APIs.
**Rationale:** This is the Zenodo concept DOI covering all versions (`conceptdoi` / `conceptrecid` 3727269).

---

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/SuperDARN/pydarn

**Source:** From existing HSSI record; confirmed by Zenodo `metadata.custom["code:codeRepository"]`, PyHC community registry `code` field, and the local git remote.
**Note:** The default branch on GitHub is `develop`; `main` and `develop` were at the same source revision when this evidence was recorded. The repository root URL is the stable software-level value.

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
- **Coordinate Transforms:Magnetospheric** — retained by settled user decision on 2026-07-24. The supporting transformations are AACGM/MLT rather than explicit GSM/GSE/SM frames: a repository-wide search for those named magnetospheric frames returns no hits. Retention rests on AACGM's magnetic-field-line tracing (Shepherd 2014, doi:10.1002/2014JA020264), its role in expressing magnetosphere-ionosphere coupling, and `pydarn/plotting/maps.py` evaluating convection potentials and fitted velocities at the ionospheric footprint of magnetospheric convection. The narrower `Coordinate Transforms:Ionospheric` value is also listed, and this caveat prevents the broader classification from being mistaken for an explicit GSM/GSE/SM transform.
- **Data Processing and Analysis** (parent) — see subcategories.
- **Data Processing and Analysis:Analysis** — `pydarn/plotting/power.py::plot_pwr0_statistic` (statistical analysis of lag-0 power with user-supplied statistical methods); `pydarn/plotting/maps.py::calculated_true_velocities`, `calculated_fitted_velocities`, `calculate_potentials`, `calculate_potentials_pos` (derivation of physical quantities); `docs/user/vels_and_potentials.md`.
- **Data Processing and Analysis:Calibration** — `pydarn/utils/recalculate_elevation.py::recalculate_elevation(dmap_data, tdiff, interferometer_offset=...)` recomputes interferometer elevation angles from raw phase (`phi0`) using a corrected `tdiff` calibration constant and array geometry; ported from RST `elevation_v2.c` and citing Shepherd (2017). Applying an instrument calibration parameter converts measured phase into a corrected physical quantity.
- **Data Processing and Analysis:Data Access and Retrieval** — rests **solely** on genuine remote retrieval from a remote archive: `pydarn/utils/superdarn_radars.py::get_hdw_files()` (public, re-exported in `pydarn/__init__.py`) and `read_hdw_file(update=True)` download and unpack the SuperDARN hardware descriptor archive over HTTPS via `urllib.request` from `https://github.com/SuperDARN/hdw/archive/main.zip`. **Scope caveat:** this retrieves radar **hardware descriptor files**, not science data — `docs/user/superdarn_data.md` states explicitly that "pyDARN does not provide an interface for downloading data" and directs users to the SuperDARN mirrors. The package's local file-reading API (`read_fitacf`, `read_rawacf`, etc.) is deliberately **not** cited as evidence here, so this value is not read as a claim that pyDARN downloads science data.
- **Data Processing and Analysis:Data Reduction** — `pydarn/utils/filters.py::Boxcar` (3x3x3 median/threshold filter over beam-gate-time to suppress noise; `docs/user/filters.md`); `pydarn/utils/detrend.py::Detrend.detrend_running_mean` (running-mean smoothing).
- **Data Processing and Analysis:File Format Conversion** — `pydarn/io/superdarn_io.py::read_borealis` wraps `pydarnio.BorealisConvert` to convert Borealis RAWACF/BFIQ HDF5 files into the SuperDARN DMAP data structure (it writes an intermediate `dmap_file.rawacf` and returns `converter.sdarn_dict`); documented under `docs/user/io.md` § "Converting Borealis Files". `pydarn/utils/conversions.py::dmap2dict` converts DMAP records to plain dictionaries. *Caveat:* the converted product is returned in memory; the intermediate DMAP file is deleted.
- **Data Processing and Analysis:Processing** — general pipeline operations: `pydarn/utils/scan.py::build_scan/find_records_by_scan/find_records_by_datetime`, `pydarn/utils/range_estimations.py` (`gate2slant`, `gate2halfslant`, `gate2timeofflight`, `gate2groundscatter`, `gate2gs_bristow`), `pydarn/utils/plotting.py` (`find_record`, `check_data_type`, `time2datetime`, embargo handling), `Boxcar.run_filter` with multiprocessing.
- **Data Processing and Analysis:Time Series Analysis** — `pydarn/plotting/rtp.py::plot_time_series`, `pydarn/plotting/maps.py::plot_time_series`, `pydarn/plotting/iq.py::plot_time_series`, `pydarn/utils/plotting.py::TimeSeriesParams`; `pydarn/utils/detrend.py` (`detrend_savgol` using `scipy.signal.savgol_filter`, `detrend_running_mean`, `detrend_fitacf`) detrends FITACF parameter time series (new in v4.3).
- **Data Visualization** (parent) — the entire `pydarn/plotting/` subpackage (~7,200 lines) built on matplotlib/cartopy.
- **Data Visualization:2D Graphics** — `fan.py::plot_fan/plot_fan_input/plot_fov`, `grid.py::plot_grid`, `maps.py::plot_mapdata/plot_potential_contours/plot_heppner_maynard_boundary`, `rtp.py::plot_range_time/plot_coord_time` (`pcolormesh` range-time and coordinate-time images), `projections.py` polar/geographic/geomagnetic axes, `color_maps.py` custom colour maps.
- **Data Visualization:Line Plots** — `rtp.py::plot_time_series`, `acf.py::plot_acfs` / `plot_acf_param` (real/imaginary, power and phase versus lag), `iq.py::plot_iq_sequence/plot_iq_record/plot_iq_overview`, `power.py::plot_pwr0_statistic`.
- **Data Visualization:Mission-Specific** — the plot types are SuperDARN-specific data products: range-time-parameter (RTI) summary plots, radar field-of-view plots driven by the SuperDARN hardware database, convection (map-potential) plots with cross-polar-cap potential, Heppner-Maynard boundary and IMF dial, gridded-vector GRID plots, ACF/XCF lag plots, and Borealis/IQDAT I/Q sequence plots.
- **Models and Simulations** (parent) — see subcategories.
- **Models and Simulations:Data Guided** — `pydarn/plotting/maps.py` reconstructs and evaluates the SuperDARN map-potential model: `calculate_potentials`/`calculate_potentials_pos` evaluate the spherical-harmonic solution (associated Legendre expansion via `scipy.special.assoc_legendre_p_all`) from the fit coefficients (`N+2`) on an arbitrary magnetic lat/lon grid, and `calculated_fitted_velocities`/`calculated_true_velocities` derive convection velocities from the electric field of that fitted potential. Documented as a first-class user capability in `docs/user/vels_and_potentials.md`. This is a model driven by and fitted to observational line-of-sight velocities.
- **Models and Simulations:Empirical** — `pydarn/utils/virtual_heights.py` implements user-selectable empirical virtual height models (`VHModels.CHISHAM` — Chisham et al. 2008 "A new empirical virtual height model", doi:10.5194/angeo-26-823-2008 — and `VHModels.STANDARD`); `pydarn/utils/range_estimations.py::gate2gs_bristow` implements the Bristow et al. (1994) ground-scatter mapped-range model and `gate2groundscatter` the Thomas & Shepherd (2022) variant; `pydarn/utils/terminator.py` implements a solar-position/terminator model (Meeus astronomical algorithms).

**Considered and rejected (audit trail):**
- **Data Visualization:Spectrogram** and **Data Processing and Analysis:Spectrogram** — present in the prior canonical file (justified there by "ACF plots showing spectral/correlation data"). **Removed.** `pydarn/plotting/acf.py` plots the autocorrelation function real/imaginary components, power and phase against *lag* for a single range gate; there is no FFT, STFT, wavelet, periodogram or any other time-frequency transform anywhere in the package (grep for `fft|welch|periodogram|spectrogram` across `pydarn/` returns no computational hits; the only "spectral" matches are the SuperDARN *spectral width* parameter `w_l`, which is a scalar fit parameter, not a spectrum). Not supported by the code.
- **Data Visualization:Movies / 3D Graphics / Web-Based / Orbit Plots** — no `matplotlib.animation`, `mplot3d`, `Axes3D`, `plotly`, `bokeh` or orbit code anywhere in the package.
- **Data Processing and Analysis:Image Processing** — the `Boxcar` filter is a geophysical median filter over (beam, gate, time), not scientific image processing; no `scikit-image`.
- **Mission-related (top level and subcategories)** — pyDARN is a community analysis/visualization library, not part of a mission ground system or data-production pipeline (SuperDARN's production processing chain is RST). Mission specificity is captured by `Data Visualization:Mission-Specific`, Field 31 and Field 32 instead.
- **Models and Simulations:Observatory/Instrument Models** — the radar field-of-view computation is geolocation geometry from hardware descriptor files, not instrument-response simulation or synthetic observation generation.
- **Coordinate Transforms:Solar** — `terminator.py` computes solar declination/subsolar position for nightshade overlays; it does not convert between solar coordinate systems (Carrington/Stonyhurst/helioprojective).

---

### 5. Related Region (MANDATORY)
**Values:**
- Earth Atmosphere
- Earth Magnetosphere
- Earth Ionosphere
- Earth Auroral Subregion

**Source:** Earth Atmosphere and Earth Magnetosphere are retained from the existing HSSI record and re-verified against the science content of the package; the finer regions are supported by the repository evidence below.
**Analysis:** SuperDARN is a network of HF coherent-scatter radars measuring ionospheric plasma irregularities in Earth's upper atmosphere (E and F regions; virtual height models in `virtual_heights.py` explicitly map returns into the E and F regions). Its principal science product — the high-latitude convection pattern reconstructed in `pydarn/plotting/maps.py` — is the ionospheric footprint of magnetospheric convection, so the software directly supports Earth Magnetosphere science (cross-polar-cap potential, Heppner-Maynard boundary, IMF-driven convection). PyHC keyword `ionosphere_thermosphere_mesosphere` agrees.
**Evidence, Earth Ionosphere:** The virtual-height implementation explicitly determines the ionospheric region for each gate (`pydarn/utils/virtual_heights.py:44`) and documents SuperDARN backscatter mapping into the E and F regions (`pydarn/utils/virtual_heights.py:63-70`).
**Evidence, Earth Auroral Subregion:** The package identifies itself as the visualization library for the Super Dual Auroral Radar Network (`README.md:8`), plots the Heppner-Maynard boundary of the auroral convection zone (`pydarn/plotting/maps.py:902-910`), and exposes cross-polar-cap potential in its map products (`docs/user/map.md:95-97,166`). The network also includes mid-latitude radars, so this value complements rather than replaces the broader regions.
**Considered and rejected:** *Interplanetary Space* — `maps.py::plot_imf_dial` displays the IMF By/Bz clock angle recorded in the map file, but this is a contextual annotation of solar-wind driving conditions, not science functionality for the interplanetary medium. *Planetary Magnetospheres* / *Solar Environment* — no support.

---

### 6. Authors (MANDATORY)

**Author-set rationale:** the 18 authors are the identity-aware union of earlier HSSI/canonical authors, `.zenodo.json` and DataCite creators, and in-repository module authorship. Wanner, Kucharyshen, Sylvestre, and Sterne appear in the v4.3 creator list; Hiyadutuje, Khanal, Chakraborty, and Pitzer remain because earlier authoritative sources credit them; Danno Peters and Francis Tholley are named in package copyright headers. Preston Pitzer's ORCID supports expanding the former initial `P.`. ORCID and ROR evidence also correct the former `Galeshuck` spelling to `Galeschuk` and expand `SANSA` to `South African National Space Agency`; the details below preserve why those current forms supersede the earlier ones.

**Author 1:**
- **Name:** SuperDARN Data Visualization Working Group
- **Author Identifier:** Not found
- **Affiliation:** Not found

**Source:** From existing HSSI record; also `setup.cfg` `author =`, `.zenodo.json` first creator, DataCite creator 1, PyHC `contact`.
**Note:** This is an **organization** author (a working group). A ROR lookup (`https://api.ror.org/v2/organizations?query=SuperDARN`) returns no result, so no organization identifier can be supplied. DataCite records it with `nameType: "Personal"`, which explains the historical given/family split; the rendered name is correct and remains unchanged.

**Author 2:**
- **Name:** Daniel D. Billett
- **Author Identifier:** https://orcid.org/0000-0002-8905-8609
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** `.zenodo.json` ("Billett, D.D.", ORCID, University of Saskatchewan), DataCite, and University of Saskatchewan ROR `https://ror.org/010x8gc63`.

**Author 3:**
- **Name:** Shibaji Chakraborty
- **Author Identifier:** https://orcid.org/0000-0001-6792-0037
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: https://ror.org/02smfhw86

**Source:** Earlier HSSI/canonical authorship and the Frontiers 2022 reference publication. This author is retained even though no longer listed in `.zenodo.json`/DataCite at v4.3. Virginia Tech ROR: `https://ror.org/02smfhw86`.

**Author 4:**
- **Name:** M. Detwiller
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** From existing HSSI record; confirmed by `.zenodo.json` ("Detwiller, M.", no ORCID) and DataCite.
**Alternative considered and excluded:** git history shows `mardet987 <marci.detwiller@usask.ca>`, so the given name may be "Marci." This inference is not strong enough to override the authoritative citation file's initial: no ORCID or citation-file confirmation was found, and changing the identity key could create a duplicate author.

**Author 5:**
- **Name:** Draven Galeschuk
- **Author Identifier:** https://orcid.org/0000-0003-3985-4225
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source and correction history:** ORCID `https://orcid.org/0000-0003-3985-4225` gives the name **Draven Galeschuk**, and git history independently uses `Draven Galeschuk <doreban@gmail.com>`. The earlier `Galeshuck` spelling in HSSI, `.zenodo.json`, and DataCite was a propagated transcription error. ORCID is the person's self-curated identity record and supports the corrected surname recorded here; the given name and University of Saskatchewan affiliation remain unchanged.

**Author 6:**
- **Name:** Alicreance Hiyadutuje
- **Author Identifier:** https://orcid.org/0000-0002-3391-8737
- **Affiliation:**
  - Organization: South African National Space Agency
  - Affiliation Identifier: https://ror.org/02epph894

**Source and correction history:** This author is retained because earlier authoritative sources credit her, even though v4.3 `.zenodo.json`/DataCite no longer list her. ROR `https://ror.org/02epph894` identifies the **South African National Space Agency** and lists `SANSA` as its acronym, so the full organization name recorded here supersedes the earlier acronym-only form.

**Author 7:**
- **Name:** Krishna Khanal
- **Author Identifier:** https://orcid.org/0000-0003-3927-7501
- **Affiliation:**
  - Organization: University of Alabama
  - Affiliation Identifier: https://ror.org/03xrrjk67

**Source:** Earlier HSSI/canonical authorship; retained even though no longer listed in `.zenodo.json`/DataCite at v4.3. ORCID `0000-0003-3927-7501` confirms "Krishna Khanal"; University of Alabama ROR `https://ror.org/03xrrjk67` confirms the affiliation.

**Author 8:**
- **Name:** K. Kucharyshen
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** `.zenodo.json` at v4.3 and the DataCite record for the concept DOI ("Kucharyshen, K.", University of Saskatchewan, no ORCID).
**Alternative considered and excluded:** git history contains `KieranKuch <137737969+KieranKuch@users.noreply.github.com>`, suggesting the given name "Kieran." No ORCID or citation-file confirmation was found, so the authoritative `.zenodo.json` initial is retained rather than an inference.

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

**Source:** Named as an author in the `pydarn/utils/superdarn_radars.py` copyright header, with substantive feature commits in git history. Affiliation from the committer email `Danno.Peters@usask.ca` (git authors `Danno Peters` / `DannoPeters`), giving University of Saskatchewan and its ROR `https://ror.org/010x8gc63`.
**Author Identifier: Not found.** An ORCID search for `family-name:Peters AND given-names:Danno` returned **0 results**, so no ORCID can be attached.
**Note:** Although absent from `.zenodo.json` and DataCite, in-repository module authorship is primary evidence of authorship.

**Author 12:**
- **Name:** Preston Pitzer
- **Author Identifier:** https://orcid.org/0009-0007-0655-1347
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: https://ror.org/02smfhw86

**Source and correction history:** ORCID `https://orcid.org/0009-0007-0655-1347` returns given-names **"Preston"**, family-name **"Pitzer"**, with Virginia Tech employment starting 2023-05. The git author `PrestonXPitzer <prestonpitzer20@vt.edu>` and `pydarn/__init__.py` credit "2023-06-20 PXP" corroborate the identification. This evidence supports expanding the earlier bare initial `P.` and attaching the ORCID.
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

**Source:** `.zenodo.json` at v4.3 and DataCite ("Sterne, K.T.", ORCID 0000-0002-1076-0009, Virginia Tech). Given name "Kevin" from the ORCID public API; middle initial "T." from `.zenodo.json`. Also present in git history as `Kevin Sterne <kevintyler@vt.edu>`.

**Author 16:**
- **Name:** R. Sylvestre
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Saskatchewan
  - Affiliation Identifier: https://ror.org/010x8gc63

**Source:** `.zenodo.json` at v4.3 and DataCite ("Sylvestre, R.", University of Saskatchewan, no ORCID).
**Alternative considered and excluded:** git history shows `RileySylvestre <nil625@usask.ca>`, suggesting the given name "Riley." No ORCID or citation-file confirmation was found, so the authoritative initial is retained.

**Author 17:**
- **Name:** Francis Tholley
- **Author Identifier:** Not found
- **Affiliation:**
  - Organization: University of Scranton
  - Affiliation Identifier: https://ror.org/05xwb6v37

**Source:** Named as module author in the `pydarn/utils/virtual_heights.py` copyright header, which also supplies the University of Scranton affiliation; 25 commits between April and September 2021; and a named co-author — "Tholley, F. H." — of the Field 14 reference publication. Also credited in `pydarn/plotting/rtp.py` and `virtual_heights.py`; University of Scranton ROR `https://ror.org/05xwb6v37`.
**Author Identifier: Not found — deliberately withheld.** ORCID lists 11 people with the family name Tholley; the single "Francis Tholley" record (`0009-0007-9521-0981`) is **entirely empty** — no employments, no educations, no works — so it cannot be confirmed as this person and **is not attached**. Attaching an unverified ORCID would be worse than omitting the identifier.
**Note:** Particularly significant because `virtual_heights.py` is the module cited in Field 4 as evidence for `Models and Simulations:Empirical`. Although absent from `.zenodo.json` and DataCite, the module authorship is direct primary evidence.

**Author 18:**
- **Name:** Tristen D. Wanner
- **Author Identifier:** https://orcid.org/0009-0007-0616-5796
- **Affiliation:**
  - Organization: Virginia Tech
  - Affiliation Identifier: https://ror.org/02smfhw86

**Source:** `.zenodo.json` at v4.3 and DataCite ("Wanner, T.D.", ORCID 0009-0007-0616-5796, Virginia Tech). Given name "Tristen" from the ORCID public API; middle initial "D." from `.zenodo.json`. Also present in git history as `Wtristen <wanner.tristen@gmail.com>`.

**Affiliation ROR evidence:** University of Saskatchewan `https://ror.org/010x8gc63`, Virginia Tech `https://ror.org/02smfhw86`, University of Alabama `https://ror.org/03xrrjk67`, University of Scranton `https://ror.org/05xwb6v37`, and South African National Space Agency `https://ror.org/02epph894` all resolve through the ROR v2 API.

---

### 7. Software Name (MANDATORY)
**Value:** pyDARN

**Source:** From existing HSSI record; confirmed by PyHC registry (`name: pyDARN`), DataCite title ("SuperDARN/pydarn: pyDARN v4.3"), README.md, and documentation site title.
**Rationale:** The PyPI/import name is lowercase `pydarn` (`setup.cfg` `name = pydarn`); the project's own branding, used throughout the documentation and release titles, is "pyDARN," so that editorial form is preserved.

---

### 8. Description (MANDATORY)
**Value:** Python data visualization library for the Super Dual Auroral Radar Network (SuperDARN). pyDARN provides comprehensive tools for reading, analyzing, and visualizing SuperDARN radar data, including range-time parameter plots, coordinate-time plots, fan plots, field-of-view plots, grid plots, convection maps, ACF plots, IQ plots, statistical power plots, and time-series visualizations. The package supports coordinate transformations between geographic, geomagnetic, and magnetic local time systems, and includes utilities for data filtering, detrending, elevation angle recalculation, range estimation, and virtual height calculations. pyDARN enables researchers to study ionosphere-magnetosphere coupling, plasma convection, and space weather phenomena using data from the international SuperDARN radar network.

**Source and revision history:** The earlier HSSI description was preserved except that its plot-type and utility enumerations had become materially incomplete. The current wording adds only the following repository-evidenced capabilities:
- "coordinate-time plots" — `pydarn/plotting/rtp.py::plot_coord_time`, `docs/user/coord_time.md`
- "field-of-view plots" — `pydarn/plotting/fan.py::plot_fov`, `docs/user/fov.md`
- "IQ plots" — `pydarn/plotting/iq.py` (`plot_iq_sequence`, `plot_iq_record`, `plot_iq_overview`), `docs/user/iq.md`
- "statistical power plots" — `pydarn/plotting/power.py::plot_pwr0_statistic`, `docs/user/power.md`
- "detrending" — `pydarn/utils/detrend.py` (new in v4.3; listed in the v4.3 release notes)
- "elevation angle recalculation" — `pydarn/utils/recalculate_elevation.py`

**Previous description:** "Python data visualization library for the Super Dual Auroral Radar Network (SuperDARN). pyDARN provides comprehensive tools for reading, analyzing, and visualizing SuperDARN radar data, including range-time parameter plots, fan plots, grid plots, convection maps, ACF plots, and time-series visualizations. The package supports coordinate transformations between geographic, geomagnetic, and magnetic local time systems, and includes utilities for data filtering, range estimation, and virtual height calculations. pyDARN enables researchers to study ionosphere-magnetosphere coupling, plasma convection, and space weather phenomena using data from the international SuperDARN radar network." It is retained here to document the precise historical baseline and why the current additions were made.

---

### 9. Concise Description (OPTIONAL)
**Value:** Python data visualization library for the Super Dual Auroral Radar Network.

**Source:** From existing HSSI record; identical to the PyHC registry `description` and to the one-line summary in README.md.
**Rationale:** This 74-character description is the project's own wording and is within the 200-character limit. A longer alternative in an earlier dossier was rejected in favor of the authoritative project wording.

---

### 10. Publication Date (RECOMMENDED)
**Value:** 2020-03-25

**Source:** From existing HSSI record; independently verified via DataCite for the first release DOI `10.5281/zenodo.3727270` ("SuperDARN/pydarn: pyDARN v1.0.0 release", version `v1.0.0`, `dates: [{date: 2020-03-25, dateType: Issued}]`).

---

### 11. Publisher (RECOMMENDED)

**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source:** DataCite `attributes.publisher = "Zenodo"`.
**Correction history:** An earlier dossier recorded the Publisher Identifier `https://ror.org/03cpe7c52`, but that ROR resolves to the **Allen Institute**, not Zenodo. A ROR v2 query for "Zenodo" returns no result, so Zenodo has no ROR; `https://zenodo.org` is the correct fallback under the field definition ("ROR identifier when available or URL otherwise").

---

### 12. Version (RECOMMENDED)

**Latest Version:**
- **Version Number:** v4.3
- **Version Date:** 2026-06-23
- **Version Description:** This minor release updates the SciPy version restriction and the associated code, and adds true velocity calculation in convection map plots, a FITACF data detrending algorithm, an option to snap a plot to the field of view of a given radar, and options to plot only ground scatter or only ionospheric scatter in fan and range-time plots. It also fixes plot_center for fields of view that did not correctly use magnetic longitude, and fixes updating of hardware (HDW) files on Windows.
- **Version PID:** https://doi.org/10.5281/zenodo.20820577

**Source:** git tag `v4.3` at `203ad04` (tagged 2026-06-23); `pydarn/version.py` (`__version__='4.3'`); GitHub release `v4.3` ("pyDARN v4.3", published 2026-06-23T21:28:32Z) release notes; Zenodo record 20820577 (`version: v4.3`, `publication_date: 2026-06-23`, `conceptdoi: 10.5281/zenodo.3727269`); DataCite for the concept DOI resolves to "SuperDARN/pydarn: pyDARN v4.3"; `docs/user/citing.md` lists "Release 4.3 ... 10.5281/zenodo.20820577".
**Previous version and update rationale:** HSSI formerly held v4.1.2 (2025-05-16, DOI 10.5281/zenodo.15441879), and issue #57 later identified v4.2 (DOI 10.5281/zenodo.17943702). Version 4.2 has itself been superseded by v4.3, so v4.3 is recorded. The version description renders the complete GitHub/Zenodo release-notes list as prose. README.md's in-repository changelog omits three of the seven v4.3 notes (snap-to-FOV, scatter-selection options, and the `plot_center` magnetic-longitude fix), so the GitHub release and Zenodo/DataCite abstract are the authoritative complete sources.

---

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

**Source:** From existing HSSI record; confirmed by `setup.cfg` (`python_requires = >=3.8`; classifiers for Python 3.8, 3.9, 3.10, 3.11 and **3.12**), `pyproject.toml` (setuptools build backend), and the fact that the repository is pure Python.
**Note:** The supported-version range grew to include the Python 3.12 classifier after the earlier dossier recorded 3.8–3.11, but this does not change the controlled `Python` value. `.readthedocs.yaml` builds with Python 3.11.

---

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.3389/fspas.2022.1022690

**Source:** From existing HSSI record; confirmed by README.md ("our [publication]") and `docs/user/citing.md`.
**Citation:** Shi, X., Schmidt, M., Martin, C. J., Billett, D. D., Bland, E., Tholley, F. H., Frissell, N. A., Khanal, K., Coyle, S., Chakraborty, S., Detwiller, M., Kunduri, B., & McWilliams, K. (2022). pyDARN: A Python software for visualizing SuperDARN radar data. *Frontiers in Astronomy and Space Sciences*, 9, 1022690.

---

### 15. License (RECOMMENDED)

**License:**
- **License:** GNU Lesser General Public License v3.0 only
- **License URI:** https://www.gnu.org/licenses/lgpl-3.0-standalone.html

**Source:** From existing HSSI record; confirmed by DataCite `rightsList` (`rights: "GNU Lesser General Public License v3.0 only"`, `rightsUri: "https://www.gnu.org/licenses/lgpl-3.0-standalone.html"`, `rightsIdentifier: "lgpl-3.0"`, SPDX scheme), the repository `LICENSE` file, `setup.cfg` (`license_files = LICENSE`; classifier "License :: OSI Approved :: GNU Lesser General Public License v3 (LGPLv3)"), Zenodo `metadata.license.id = "lgpl-3.0"`, and per-module copyright headers throughout `pydarn/`.
**SPDX identifier:** `LGPL-3.0-only`.

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

**Source:** Identity-aware union of earlier HSSI/canonical keywords and the PyHC registry, normalized to one spelling per concept. Keywords are an open vocabulary; the values below are chosen deliberately rather than generated mechanically.

**Mapping and provenance:**
- **Earlier HSSI forms retained:** `ionosphere`, `ionosphere thermosphere mesosphere`, `magnetosphere`, `plotting`, `radar`, `space physics`, `superdarn`, `superdarn data`, `visualization`.
- **Normalized alternatives:** `plots` → `plotting`; `superdarn-data` → `superdarn data`; `ionosphere_thermosphere_mesosphere` → `ionosphere thermosphere mesosphere`; `data_analysis` → `data analysis`. `general` is also a PyHC-curated keyword for pyDARN.
- **Repository-evidenced terms:**
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

**Source:** pyDARN reads SuperDARN-specific data products (IQDAT, RAWACF, FITACF, GRID/GRD, MAP, SND in DMAP format, plus Borealis RAWACF/BFIQ HDF5). This is consistent with Field 32 (Related Observatories: SuperDARN), as the field guidance requires.
**Considered and rejected (audit trail):** *HTTP/HTTPS Directories* — `pydarn/utils/superdarn_radars.py::get_hdw_files()` does retrieve `https://github.com/SuperDARN/hdw/archive/main.zip` over HTTPS via `urllib.request`, but that retrieves **radar hardware descriptor files**, not science data. `docs/user/superdarn_data.md` states outright: "pyDARN does not provide an interface for downloading data" and directs users to the SuperDARN Canada (Globus), BAS and NSSC mirrors for data acquisition. Claiming an HTTP data source would mislead a user searching HSSI on that facet. *FTP/FTPS Directories*, *CDAWeb*, *HAPI*, *S3/Cloud-aware* — no support anywhere in the code.

---

### 18. Input File Formats (RECOMMENDED)
**Values:**
- HDF5
- Other

**Source and rationale:** `pydarn/io/superdarn_io.py::read_borealis` reads Borealis RAWACF/BFIQ files, which are HDF5, via `pydarnio.BorealisConvert`; `docs/user/io.md` under "Converting Borealis Files" discusses the `hdf5` libraries. `Other` covers DMAP (Data Map), the SuperDARN community's self-describing binary format, which is not on the controlled list: `docs/user/io.md` describes DMAP and its IQDAT, RAWACF, FITACF, GRID/GRD, MAP and SND file types, with transparent `.bz2` decompression. Hardware descriptor files (`pydarn/utils/hdw`, read by `read_hdw_file`) are plain text and also fall under `Other`.

---

### 19. Output File Formats (RECOMMENDED)
**Value:** Not found

**Source:** Code analysis at v4.3.
**Rationale:** pyDARN is a visualization and analysis library that returns matplotlib figures/axes and Python data structures. A repository-wide search for write operations (`savefig`, `to_csv`, `.write`, `open(...,'w')`) finds no data-file writing in `pydarn/`; the only file writes are `get_hdw_files()` unpacking downloaded hardware text files and the transient `dmap_file.rawacf` created and immediately deleted inside `read_borealis`. Users save figures through matplotlib themselves (PNG/PDF/SVG), which are not values in the controlled list, so this field is empty.

---

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Operating System Independent
- Windows

**Source:** From existing HSSI record; confirmed by `docs/user/install.md`, whose installation matrix has columns for **Ubuntu | OpenSuse | Fedora | OSX | Windows**, and by the v4.3 release note "Bug Fix: Updating HDW files on Windows fixed" (evidence of active Windows support). `.github/workflows/ruff.yml` runs on `ubuntu-latest`. Pure-Python package installable with `pip install pydarn`.
**Alternative considered and excluded:** `OS Independent` is not added because `Operating System Independent` is synonymous; carrying both would create a redundant duplicate.

---

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

**Source:** From existing HSSI record; re-verified. Pure Python with no compiled extensions in this repository (`pyproject.toml` build-backend `setuptools.build_meta`, no C/Fortran sources, no `ext_modules`). Architecture support is inherited from the wheels of the dependencies (numpy, scipy, matplotlib, cartopy, aacgmv2).
**Rationale:** Specific architectures (x86-64, Apple Silicon arm64, aarch64) are all subsumed by `CPU Independent`.

---

### 22. Related Phenomena (OPTIONAL)
**Values:**
- Geomagnetic Storms

**Source and selection rationale:** `pydarn/plotting/maps.py` visualizes and computes geomagnetic-activity diagnostics — cross-polar-cap potential (`pot.drop`, `add_map_info`), the Heppner-Maynard boundary (`plot_heppner_maynard_boundary`), IMF By/Bz driving conditions (`plot_imf_dial`), and the full high-latitude convection pattern (`calculate_potentials`, `plot_potential_contours`). The relationship is through the ionospheric convection response rather than direct measurement of storm indices, but the settled 2026-07-24 decision includes `Geomagnetic Storms` as the closest controlled phenomenon for this SuperDARN science.
**Considered and rejected:** *Solar Wind* — `plot_imf_dial` merely annotates a convection map with the IMF clock angle recorded in the map file; pyDARN provides no solar-wind science functionality. All solar phenomena (Coronal Heating, CMEs, Solar Corona, Solar Flares, X-ray emission) — not applicable.

---

### 23. Development Status (RECOMMENDED)
**Value:** Active

**Source:** `setup.cfg` classifier `Development Status :: 5 - Production/Stable`; sustained release cadence (v4.1.2 in 2025-05, v4.2, v4.3 tagged 2026-06-23); HEAD commit dated 2026-06-23 with 2026-dated modification entries inside the source (e.g. `rtp.py`: "2026-04-20 Carley Martin added options for remove_iono_scatter and remove_ground_scatter"); five active feature/fix branches on the remote; PyHC registry rates `software_maturity: Good` and `community: Good`. Matches repostatus.org "Active" — reached a stable, usable state and being actively developed.
---

### 24. Documentation (RECOMMENDED)
**Value:** https://pydarn.readthedocs.io/en/main/

**Source:** README.md ("pyDARN's documentation can be found here"), the PyHC registry `docs` field, `mkdocs.yml`, and `.readthedocs.yaml` all identify this documentation site.
**Note:** The site includes the installation guide at `https://pydarn.readthedocs.io/en/main/user/install/`, satisfying the "including installation instructions" requirement. (`setup.cfg` `url =` still points at the `/en/latest/` alias; the `/en/main/` form used by the README and PyHC is the canonical one.)

---

### 25. Funder (OPTIONAL)
**Value:** Not found

**Source:** DataCite `attributes.fundingReferences` is an empty array for the concept DOI; no funding statement in README.md, `setup.cfg`, `.zenodo.json`, or the documentation.
**Rationale:** `docs/user/citing.md` records that SuperDARN *data* is "funded by national scientific funding agencies of Australia, Canada, China, France, Italy, Japan, Norway, South Africa, United Kingdom and the United States of America," but that is an acknowledgement for the radar network's observations, not a funder of this software, so no value is recorded here.

---

### 26. Award Title (OPTIONAL)
**Value:** Not found

**Source:** DataCite `attributes.fundingReferences` empty; no award number or grant title anywhere in the repository or DOI metadata.

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
**Rationale:** These are the algorithm/method publications the developers explicitly prioritize: `pydarn.Citations.print_citations()` prints them with the instruction "If using pyDARN produced plots in publications please be aware of the following citations that may have been used to produce your plot and should be included in your publication". Each is implemented in the code:
- **10.1029/93JA01470** — Bristow, W. A., Greenwald, R. A., & Samson, J. C. (1994). Ground scatter mapped range; implemented in `pydarn/utils/range_estimations.py::gate2gs_bristow`.
- **10.5194/angeo-26-823-2008** — Chisham, G., Yeoman, T. K., & Sofko, G. J. (2008). Empirical virtual height model; implemented in `pydarn/utils/virtual_heights.py::chisham` and `standard_virtual_height`.
- **10.1002/2014JA020264** — Shepherd, S. G. (2014). AACGM-v2 definition; the coordinate system used by `pydarn.Coords.AACGM` via `aacgmv2`.
- **10.1002/2017RS006348** — Shepherd, S. G. (2017). Elevation angle determination for SuperDARN HF radar layouts; implemented in `pydarn/utils/recalculate_elevation.py` (header: "Modified from the RST elevation_v2.c code").
- **10.1029/2022RS007429** — Thomas, E. G., & Shepherd, S. G. (2022). Virtual height characteristics of ionospheric and ground scatter; implemented in `pydarn/utils/range_estimations.py::gate2groundscatter`.

**Additional candidates considered and excluded:** Greenwald et al. (1995) https://doi.org/10.1007/BF00751350; Chisham et al. (2007) https://doi.org/10.1007/s10712-007-9017-8; and Nishitani et al. (2019) https://doi.org/10.1186/s40645-019-0270-5 describe the SuperDARN network and its data rather than this software. The example Jupyter notebook accompanying the reference publication, https://zenodo.org/record/7005203, is noted by the README as potentially out of date and is also excluded.

---

### 28. Related Datasets (OPTIONAL)
**Value:** https://www.frdr-dfdr.ca/repo/collection/superdarn

**Citation form (human reference only; not the stored value):** SuperDARN RAWACF data collection [Data set]. Federated Research Data Repository (FRDR). https://www.frdr-dfdr.ca/repo/collection/superdarn

**Source:** `docs/user/superdarn_data.md`, under a heading titled literally `## RAWACF Data`: "Raw data with DOI's can be accessed on [FRDR](https://www.frdr-dfdr.ca/repo/collection/superdarn). These data are published once all gaps are checked and PIs are happy with the collection for each year and no data is under embargo."
**Identifier rationale:** The bare collection URL covers all years and is used because the collection landing page exposes no collection-level DOI. The APA-style citation is retained above for human reference.

**Independently verified evidence for the relationship (2026-07-24):**
- The FRDR SuperDARN collection is the year-by-year archived **RAWACF/DAT** corpus (1996–2023), authored by "Super Dual Auroral Radar Network" — precisely the data product pyDARN is built to read. The repository's link to it sits under a heading titled literally `## RAWACF Data`.
- pyDARN exposes `read_rawacf` as top-level public API (`pydarn/__init__.py:27`), and `pydarn/plotting/power.py:28` and `pydarn/plotting/acf.py:41` are documented as plotting "SuperDARN RAWACF data".
- **The relationship is reciprocal and machine-readable.** The FRDR dataset *SuperDARN 2023 RAWACF* (`https://doi.org/10.20383/103.01307`) lists in its own **Related Identifiers**: "This dataset is supplemented by `https://doi.org/10.5281/zenodo.15441879`" — pyDARN v4.1.2 — alongside `https://doi.org/10.5281/zenodo.4435150` (RST) and `https://github.com/SuperDARN/hdw`. The archive itself therefore asserts the link back to this software.
- The individual **annual** datasets do carry real DOIs (e.g. `10.20383/103.01307`), even though the collection page does not. The collection URL was chosen deliberately as the non-arbitrary pointer covering all years rather than singling out one year. **Optional future enrichment:** add the per-year dataset DOIs alongside (or instead of) the collection URL.
**Also considered:** the SuperDARN hardware descriptor repository https://github.com/SuperDARN/hdw (a git submodule at `pydarn/utils/hdw` and the target of `get_hdw_files()`) — it is radar configuration metadata rather than a science dataset and has no DOI, so it is not recorded as a value.

---

### 29. Related Software (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.801458
- https://doi.org/10.5281/zenodo.4009470
- https://doi.org/10.5281/zenodo.1212694
- https://github.com/vtsuperdarn/davitpy

**Source and per-entry relevance justification:**
- **`10.5281/zenodo.801458` — SuperDARN Radar Software Toolkit (RST).** The SuperDARN community's C-based radar software toolkit is the peer/counterpart toolkit that produces the FITACF, GRID, MAP and SND products pyDARN visualizes. The documentation references RST (`docs/user/io.md` links to its DMap-format documentation; `docs/user/vels_and_potentials.md` links to its map-file reference for the fit parameters pyDARN evaluates), and `pydarn/utils/recalculate_elevation.py` is a port of RST's `elevation_v2.c`. DataCite title: "SuperDARN Radar Software Toolkit (RST) 5.1.1".
- **`10.5281/zenodo.4009470` — pyDARNio.** The SuperDARN-specific I/O library is maintained by the same working group; `setup.cfg` pins `pydarnio>=2.0.0` and `pydarn/__init__.py` re-exports its readers directly into pyDARN's public namespace. It is a domain-specific, characterizing dependency and companion package rather than generic infrastructure. It is also cited by `pydarn.Citations` (`pydarnio2023`). DataCite title: "SuperDARN/pyDARNio: pyDARNio v2.0".
- **`10.5281/zenodo.1212694` — aacgmv2.** The AACGM-v2 heliophysics coordinate library is a domain-specific dependency that characterizes what pyDARN does: `pydarn/utils/coordinates.py` imports `aacgmv2`, and `Coords.AACGM`/`AACGM_MLT` are built on it. It is cited by `pydarn.Citations` (`burrell2023`). The concept DOI is used here (DataCite title "aburrell/aacgmv2: Version 2.7.1"); `citations.py` cites the version-specific `10.5281/zenodo.7621545`.
- **`https://github.com/vtsuperdarn/davitpy` — DaViTPy.** The predecessor Virginia Tech SuperDARN Python toolkit from which pyDARN's plotting was derived. Direct repository evidence: `pydarn/plotting/rtp.py` says "This code is improvement based on rti.py in the DaVitpy library" and links the source; `pydarn/plotting/acf.py` says "This code is based on acf.py in the DaVitpy library"; colormap-derivation comments also appear at `rtp.py:391` and `rtp.py:1847`. Field 29 explicitly covers software from which a work was forked. No DOI was found, so the repository URL is used.

**Considered and rejected (Tier A generic infrastructure — being a dependency is not relatedness):** `numpy`, `scipy`, `matplotlib`, `cartopy`, `pyyaml` (all of `setup.cfg` `install_requires` except `pydarnio` and `aacgmv2`). Each would be equally at home in a web app, a finance model or a biology pipeline; listing them would say nothing that isn't true of most of the ecosystem. `cartopy` is mapping infrastructure and is rejected on the same basis despite being cited in `citations.py`. `setuptools` (build backend) likewise.

---

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.4009470
- https://github.com/SuperDARNCanada/borealis

**Source and per-entry demonstrated-exchange evidence:**
- **`10.5281/zenodo.4009470` — pyDARNio.** `pydarn/__init__.py` re-exports pyDARNio's readers (`from pydarnio import read_iqdat, read_rawacf, read_fitacf, read_grid, read_map, read_snd, read_dmap`) as pyDARN's own public API; the two packages share a data model (lists of DMAP record dictionaries) that flows unchanged from pyDARNio's readers into every pyDARN plotting entry point; `pydarn/io/superdarn_io.py` calls the `pydarnio.BorealisConvert` adapter; `pydarn/utils/conversions.py::dmap2dict` converts pyDARNio's DMAP structures to plain dictionaries. `docs/user/io.md` closes by directing users to pyDARNio for further reading/writing needs. This demonstrates exchange beyond a mere dependency.
- **`https://github.com/SuperDARNCanada/borealis` — Borealis.** `pydarn.read_borealis(filename, slice_id=...)` is a purpose-built converter that ingests files produced by the Borealis SuperDARN radar operating system (RAWACF and BFIQ HDF5) and returns them in pyDARN's SDARN data model, with explicit handling of Borealis slice IDs and files produced before Borealis v0.5. This is documented in `docs/user/io.md` under "Converting Borealis Files". Output of one tool is imported into the other through a named adapter API, meeting the Field 30 bar. No DOI was located, so the repository URL is used.

**Considered and rejected:**
- **Tier A, always excluded:** `numpy`, `scipy`, `matplotlib`, `cartopy`, `pyyaml`. Being a dependency is not interoperability.
- **`aacgmv2`** — recorded in Field 29 as a characterizing domain dependency, but **not** here: pyDARN calls into it as a library; there is no bidirectional exchange, adapter, shared data model, or plugin relationship.
- **RST (`10.5281/zenodo.801458`)** — RST's FITACF/GRID/MAP output is pyDARN's input, a real cross-language exchange with a named domain tool documented in `docs/user/io.md` and `docs/user/vels_and_potentials.md`. It is deliberately retained in Field 29 and not duplicated here.
- **Blanket claims not used:** "part of the standard scientific Python ecosystem" and "a PyHC member, so it interoperates with PyHC packages" were explicitly *not* relied upon.

---

### 31. Related Instruments (OPTIONAL)

**Instrument 1:**
- **Instrument Name:** SuperDARN Radars
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SuperDARN/Radars

**Source:** The HSSI controlled vocabulary has one instrument entry named "SuperDARN Radars," with the SPASE identifier above and no `.html` duplicate. The canonical name is copied verbatim.
**Rationale:** pyDARN is purpose-built for SuperDARN HF radar data. It embeds the complete hardware description of every SuperDARN radar (`pydarn/utils/superdarn_radars.py`, with `RadarID`, `SuperDARNRadars`, `read_hdw_file`, `get_hdw_files` and the `pydarn/utils/hdw` submodule), computes each radar's beam/range-gate geolocation and field of view from those hardware parameters, implements SuperDARN-specific data formats and control-program identifiers (`superdarn_cpid.py`), and reads and plots every SuperDARN data product. A user searching HSSI for SuperDARN radar software would expect this package.
**Previous value and correction:** The prior canonical file used the free-text string "SuperDARN radars (international network of HF coherent scatter radars)," which would not bind to the controlled vocabulary. The resolved canonical name and SPASE identifier replace it.
**Deliberately not expanded:** the vocabulary also contains individual IUGONET instrument rows (SuperDARN Hokkaido East/West HF radar, SuperDARN King Salmon HF radar, SENSU SuperDARN Syowa East/South HF radar). pyDARN supports all 35+ network radars equally through its hardware database, so listing four arbitrary members would misrepresent the coverage; the umbrella "SuperDARN Radars" row is the correct single entry.

---

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** SuperDARN
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SuperDARN

**Source:** The HSSI controlled vocabulary has one observatory entry named "SuperDARN," with the SPASE identifier above and no `.html` duplicate. The canonical name is copied verbatim.
**Rationale:** The software exists to read, process and visualize the SuperDARN network's data products; this is consistent with Field 17 (`Observatory/Mission-specific`). The previously bare "SuperDARN" name is supplemented with its SPASE identifier so the relationship binds deterministically rather than relying on name lookup alone.
**Deliberately not expanded:** the IUGONET observatory rows for individual sites (SuperDARN Hokkaido East/West, King Salmon) are members of the same network, not separate targets of this software.

---

### 33. Logo (OPTIONAL)
**Value:** https://raw.githubusercontent.com/SuperDARN/pydarn/main/docs/imgs/pydarn_logo.png

**Source:** Repository file `docs/imgs/pydarn_logo.png` on the `main` branch; the URL serves the repository's PNG logo and matches the image formerly served through the stale ref path.
**Previous URL and correction:** HSSI, README.md (first line) and the PyHC `projects.yml` `logo` field had all pointed at `.../pydarn/**master**/docs/imgs/pydarn_logo.png`. No `master` ref exists on the remote, so that URL resolves only through GitHub's legacy default-branch alias, which survived the `master` to `main`/`develop` rename and is not a guaranteed-stable contract. The value is therefore repointed at the **branch** form `main`, which is a real ref on the remote and currently identical to `develop`.
**Why the branch form rather than a tag:** the tag-pinned `.../v4.3/docs/imgs/pydarn_logo.png` would freeze the logo at v4.3 and require an update at every release; the `main` branch form survives future releases.
**Upstream follow-up (outside HSSI's control):** PyHC's `projects.yml` still carries the stale `master` URL, and so does the repository's own README.md. Worth reporting upstream, but it does not block this correction.

---
