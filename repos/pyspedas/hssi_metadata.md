# HSSI Metadata Extraction Results

**HSSI Software ID:** 82f57fc4-357f-49d3-af4b-e8bfb0a35210
**Repository:** https://github.com/spedas/pyspedas
**Source Revision:** bbfdd632a0eb42953a8c83a489c140b13c508927
**Extraction Date:** 2026-08-11
**Validation Date:** 2026-08-20
**Validation Status:** PASS
> **Scope note.** PySPEDAS is a multi-mission framework: the `pyspedas/projects/` tree carries 37
> per-project subpackages, and the analysis, coordinate-transform, particle, geopack and plotting
> capabilities are shared across all of them. Several fields below (notably Software Functionality,
> Related Region, Related Instruments and Related Observatories) are therefore best read as the union
> of what those projects need, not as a description of one instrument or one mission.
>
> Two of those fields use different granularity on purpose, and each says so in its own note.
> Related Observatories associates at mission or network level, so the breadth of what PySPEDAS can
> load is discoverable in one place. Related Instruments is narrower: it lists only the instruments
> for which PySPEDAS carries dedicated processing code, at the per-spacecraft granularity SPASE
> requires. An instrument's absence from Field 31 therefore says nothing about whether PySPEDAS
> supports it — Field 32 is where support is recorded.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.17634923
- Source: Concept DOI (all versions), declared in `pyproject.toml` `[project.urls] Concept_DOI` and in
  `CITATION.cff` (`doi:`). Confirmed against DataCite, which resolves it with `version: 2.1.4`,
  publisher Zenodo, and an `IsVersionOf` link from the current versioned DOI.

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/spedas/pyspedas
- Source: `pyproject.toml` `[project.urls] Homepage` and `Source_Code`; Zenodo's
  `code:codeRepository` custom field on the 2.1.4 record; the PyHC core registry `code` field. All
  three agree, and the URL resolves.

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Ionospheric
- Coordinate Transforms: Magnetospheric
- Coordinate Transforms: Mission-Specific
- Coordinate Transforms: Planetary
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: 3D Particle Distribution Processing
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Curlometer
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Linear Gradient Estimation
- Data Processing and Analysis: Magnetic Null Finding
- Data Processing and Analysis: Pitch Angle Distributions
- Data Processing and Analysis: Plasma Moments
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Wave Polarization Analysis
- Data Processing and Analysis: Wavelet Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Hodograms
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: Orbit Plots
- Data Visualization: Spacecraft Formation Plots
- Data Visualization: Spectrogram
- Mission-related
- Mission-related: Analysis
- Mission-related: Calibration
- Mission-related: Science Data Processing
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing
- Models and Simulations: Physics-Based

**Evidence for the values carried from the stored HSSI record.** Coordinate transforms: the core
`cotrans` engine converts among GSE, GSM, SM, GEI, GEO, MAG and J2000
(`pyspedas/cotrans_tools/cotrans.py`, `cotrans_lib.py`); `sm2mlt.py` yields magnetic local time
(ionospheric); `gsm2lmn.py` / `lmn_matrix_make.py` / `minvar*.py` / `fac_matrix_make.py` give
boundary-normal, minimum-variance and field-aligned frames (magnetospheric); THEMIS
`cotrans/dsl2gse.py`, `ssl2dsl.py` and MMS `mms_qcotrans` handle spacecraft-fixed spinning and
despun frames (mission-specific); THEMIS `cotrans/gse2sse.py` and `sse2sel.py` transform to
selenocentric solar-ecliptic and selenographic frames for ARTEMIS (planetary). Data processing:
`analysis/wavelet*.py`, `wav_data.py` and `wave_signif.py` (wavelet); `analysis/twavpol.py` (wave
polarization); `analysis/find_magnetic_nulls.py` (magnetic null finding); `analysis/lingradest.py`
(linear gradient estimation); `mms.curlometer` (curlometer); `particles/moments/` (plasma moments);
`mms_feeps_pad`, `mms_eis_pad`, `erg` MEP-e PAD routines (pitch-angle distributions);
`particles/spd_slice2d/` (2-D slices of distributions); `particles/spd_part_products/spd_pgs_make_e_spec.py`
and `mms_part_getspec` (energy spectra); `geopack/ttrace2endpoint.py` and `trace_to_event.py`
(field-line tracing); `tplot_tools/tplot_math/pwr_spec.py`, `dpwrspc.py`, `tdpwrspc.py`
(spectrogram); `tplot_tools/tplot_math/` plus `analysis/tinterpol.py`, `time_domain_filter.py`,
`deriv_data.py` (time-series analysis); `analysis/avg_data.py`, `rebin.py`, `reduce_tres.py` (data
reduction); `tplot_tools/importers/` and `tplot_tools/exporters/` (file-format conversion); the
per-project `load()` routines plus `cdagui_tools/`, `hapi_tools/`, `vires/`, `mth5/` (data access
and retrieval). Visualization: `tplot_tools/MPLPlotter/lineplot.py`, `specplot.py`, `tplotxy.py`,
`tplotxy3.py`, `mms_orbit_plot.py`, `mms_tetrahedron_qf`, `spd_slice2d/slice2d_plot.py` and
`slice1d_plot.py`.
Models: Tsyganenko T89/T96/T01/TS04 and IGRF in `pyspedas/geopack/` (empirical);
`analysis/neutral_sheet.py` (eight neutral-sheet models: SM, THEMIS/Hammond, AEN, DEN, Fairfield,
den_fairfield, Lopez, TAG14), `utilities/mpause_2.py`, `mpause_t96.py`, `utilities/bshock_2.py`
(physics-based magnetopause and bow-shock geometry); `geopack/calculate_lshell.py`.

**Evidence for the values that the stored record did not carry.**

- `Models and Simulations: Data Guided` — the Tsyganenko models are not run on fixed parameters.
  `geopack/get_tsy_params.py` interpolates observed Dst, GSM IMF, solar-wind ion density and proton
  velocity tplot variables into the T89/T96/T01/TS04 driving-parameter vector, and
  `geopack/get_w_params.py` downloads the TS05 W1–W6 driving variables. `geopack/kp2iopt.py`
  converts the observed Kp index into the T89 `iopt` input. That is a model driven by observations,
  which is exactly what this subcategory denotes.
- `Mission-related`, `Mission-related: Analysis`, `Mission-related: Calibration`,
  `Mission-related: Science Data Processing` — PySPEDAS is not only a general analysis library; it
  carries mission ground-segment processing inherited from IDL SPEDAS, and it is funded by mission
  grants (Zenodo funding metadata lists THEMIS NAS5-02099 and MMS NNG04EB99C, alongside SPEDAS
  Community Support NNG17PZ01C). Concretely: `projects/themis/state_tools/spinmodel/` implements the
  THEMIS spin model with eclipse spin-phase corrections (`eclipse_spinmodel_corrections_vector.py`,
  `..._tensor.py`), while the sibling `state_tools/apply_spinaxis_corrections.py` applies spin-axis
  attitude corrections — the step that turns raw spin-phase telemetry into despun science
  coordinates (science data processing). `projects/elfin/epd/calibration_l1.py` and
  `calibration_l2.py` implement the ELFIN
  EPD calibration chain and read mission calibration tables shipped inside the wheel
  (`pyproject.toml` `package-data` ships `el*_epde_cal_data.txt`);
  `projects/mms/feeps_tools/mms_feeps_flat_field_corrections.py`,
  `mms_feeps_correct_energies.py` and `mms_feeps_remove_sun.py` apply FEEPS instrument corrections
  using shipped sun-contamination sector masks (`feeps_tools/sun/*.csv`) — calibration. An earlier
  revision of this record also cited `projects/mms/scm_tools/` as applying MMS SCM calibration; that
  is not supported by the code and has been dropped. `scm_tools/` contains no calibration code — its
  only substantive files are `scm.py`, a load routine that labels the output coordinate system
  according to data level, and `mms_scm_set_metadata.py`, which sets plot metadata, alongside an
  empty `__init__.py`. The two chains named above carry the calibration values on their own.
  `mms_orbit_plot.py`, `mec_ascii/mms_get_tetrahedron_qf.py`, `mms_events.py`,
  `plots/mms_overview_plot.py` and `projects/themis/ground/ask.py` are mission analysis products
  rather than generic utilities.

**Considered and not selected.** Recording these so a later refresh does not re-propose them without
new evidence.

- `Coordinate Transforms: Heliospheric` and `Coordinate Transforms: Solar` — PySPEDAS *loads* data
  that is already expressed in RTN (PSP `mag_RTN*`, Solar Orbiter `rtn-normal`, STEREO `coord='RTN'`),
  but a full-text search finds no transform to or from RTN, HCI, HAE, HEE, Carrington, Stonyhurst or
  helioprojective coordinates. `cotrans.py` documents its supported set as exactly
  `gse, gsm, sm, gei, geo, mag, j2000`. Reading data in a heliospheric frame is not transforming to
  one.
- `Data Processing and Analysis: Image Processing` — PySPEDAS loads image-bearing products (THEMIS
  all-sky keograms and full images via `themis/ground/ask.py`, IMAGE FUV/EUV, Polar UVI/VIS/PIXIE,
  TWINS imager, ERG/ISEE OMTI all-sky imagers) and renders SECS/EICS vector and contour maps, but it
  implements no image-processing algorithms — no deconvolution, mosaicking, feature detection or
  `scikit-image` use. The loading belongs under Data Access and Retrieval, and the map rendering
  under Data Visualization: 2D Graphics.
- `Data Processing and Analysis: Packet Decommutation` and `Mission-related: Packet Decommutation` —
  no CCSDS or raw-telemetry parsing exists anywhere in the tree; a search for L0 handling in
  `projects/mms/` finds none. PySPEDAS begins at L1/L2 science products. (An earlier revision of this
  record cited "MMS L0 packet binaries" as a justification under Input File Formats; that claim is
  not supported by the code and has been dropped.)
- `Data Visualization: 3D Graphics` — a previously submitted value, corrected here on evidence.
  PySPEDAS renders no three-dimensional graphics: there is no `Axes3D`, `mplot3d`,
  `projection='3d'`, `plot_surface`, `scatter3D`, `plot3D`, `voxels` or `quiver3` use in any
  tracked file at the pinned revision, and no vtk, mayavi or pyvista dependency. The routine
  whose name most invites the assumption, `pyspedas/tplot_tools/MPLPlotter/tplotxy3.py`, documents
  itself at line 303 as plotting "one or more 3d tplot variables, by projecting them onto the three
  coordinate axes planes in a single figure" — three 2-D panels of a 3-vector, which
  `Data Visualization: 2D Graphics` and `Data Visualization: Line Plots` already cover, not a 3-D
  rendering. Removing this value orphans no subcategory: the parent `Data Visualization` is still
  recorded and is still carried by the eight visualization subcategories that remain.
- `Data Visualization: Movies` — no `matplotlib.animation`, `imageio` or ffmpeg use.
- `Data Visualization: Web-Based` — the only GUI is `cdagui_tools/cdagui.py`, a desktop tkinter
  window. The bokeh backend that older PyTplot-based releases carried is gone; no bokeh, plotly or
  dash import remains.
- `Data Processing and Analysis: Data Assimilation`, `Data Processing and Analysis: ML/AI`,
  `Models and Simulations: MHD`, `First Principles`, `Forecasting`, `Forward-Fitting`, `Theory`,
  `Instrument Response`, `Observatory/Instrument Models`, `ML/AI`, `Mission-Specific` — none of these
  have implementations. In particular there is no forward instrument-response model; the FEEPS and
  SCM routines apply measured corrections to real data rather than simulating a response.
- `Mission-related: Distribution/Access` — PySPEDAS authenticates to and queries the MMS SDC
  (`mms_login_lasp.py`, `mms_load_data.py`, `mec_ascii/mms_get_state_data.py`) but is a *client* of
  those services, not a distribution system. That capability is already covered by
  `Data Processing and Analysis: Data Access and Retrieval`.
- `Servers and Environments` and all its children — PySPEDAS ships no server, container or HPC
  orchestration.
- `Mission-related: Processing` — considered as the more generic sibling of
  `Mission-related: Science Data Processing`; the specific value is the better fit for THEMIS
  spin-model and calibration processing, so only the specific one is recorded.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Inner Magnetosphere
- Earth Ionosphere
- Earth Magnetosheath
- Earth Magnetosphere
- Earth Magnetotail
- Earth Outer Magnetosphere
- Earth Thermosphere
- Interplanetary Space
- Mars Magnetosphere
- Planetary Magnetospheres
- Solar Environment
- Solar Wind

**Why fourteen regions rather than the coarser five.** The five previously stored values (Earth
Atmosphere, Earth Magnetosphere, Interplanetary Space, Planetary Magnetospheres, Solar Environment)
are the keys of the TTL-export mapping in the HSSI codebase, not the selectable vocabulary. The
selectable vocabulary offers 24 values (as of 2026-08-11), and the guidance is to prefer the most
specific applicable region. The five are retained because they remain true at the coarse level; the
nine additions below each rest on repository evidence, and none of the five was replaced.

- **Earth Ionosphere** — `geopack/ttrace2endpoint.py` traces field lines to the northern and southern
  ionosphere and `tplot_tools/MPLPlotter/tplot_map.py` maps those footpoints;
  `cotrans_tools/sm2mlt.py` produces magnetic local time; `projects/secs/` loads and plots
  equivalent ionospheric currents (`read_data_files.py` reads the already-derived Jx/Jy columns out
  of the downloaded EICS/SECS files; PySPEDAS performs no spherical-elementary-current inversion of
  its own);
  `projects/cnofs/` (CINDI, PLP, VEFI), `projects/de2/` (RPA, IDM, Langmuir probe),
  `projects/swarm/`, `projects/kompsat/`, `projects/mica/` and the THEMIS/ERG ground magnetometer
  and riometer chains are ionospheric datasets.
- **Earth Thermosphere** — `projects/de2/load.py` exposes `nacs` (Neutral Atmosphere Composition
  Spectrometer) and `wats` (Wind and Temperature Spectrometer), which measure the neutral
  thermosphere directly; C/NOFS and Swarm sample thermospheric ion drift and density.
- **Earth Auroral Subregion** — `projects/themis/ground/ask.py` loads THEMIS all-sky keograms and
  full-sky auroral images; `projects/polar/uvi.py`, `vis.py` and `pixie.py` are auroral imagers;
  `projects/image/fuv.py` is the IMAGE far-ultraviolet auroral imager; `projects/fast/` covers the
  auroral acceleration region; `projects/elfin/epd/` measures auroral-zone electron precipitation;
  `projects/akebono/` and `projects/barrel/` sample auroral-latitude precipitation.
- **Earth Inner Magnetosphere** — `projects/rbsp/` (HOPE, MagEIS, REPT, RPS, RBSPICE, EMFISIS),
  `projects/erg/satellite/erg/` (Arase, an inner-magnetosphere mission), `projects/csswe/reptile.py`,
  `projects/barrel/` (radiation-belt electron losses), `projects/twins/imager.py` (ring-current
  energetic neutral atoms), `projects/image/euv.py` (plasmasphere) and `projects/polar/cammice.py`,
  `ceppad.py`; `geopack/calculate_lshell.py` computes L-shell by tracing to the equator with IGRF.
- **Earth Outer Magnetosphere** — `projects/themis/`, `projects/cluster/`, `projects/mms/`,
  `projects/geotail/`, `projects/polar/` and `projects/equator_s/` operate largely outside
  geosynchronous orbit, and `utilities/mpause_2.py` (Fairfield) and `mpause_t96.py` model the
  magnetopause boundary.
- **Earth Magnetotail** — `analysis/neutral_sheet.py` implements eight neutral-sheet models whose
  only purpose is locating the tail current sheet; ARTEMIS (`projects/themis/`, lunar orbit) samples
  the deep tail; Geotail is a dedicated tail mission.
- **Earth Magnetosheath** — `utilities/bshock_2.py` models the bow-shock surface and the magnetopause
  models above bound the other side of the sheath, so the sheath is the region that the pair of
  boundary models delimits; MMS, Cluster and THEMIS magnetosheath crossings are the standard use of
  those routines.
- **Solar Wind** — `projects/omni/omni_solarwind_load.py` and `projects/omni/load.py` load the OMNI
  solar-wind record, which also drives the Tsyganenko parameter derivation; ACE (SWEPAM, SWICS),
  Wind (SWE, 3DP), DSCOVR, STEREO PLASTIC, PSP SWEAP, Solar Orbiter SWA and Ulysses SWOOPS are all
  solar-wind plasma instruments with dedicated load routines.
- **Mars Magnetosphere** — `projects/maven/` loads MAG, STATIC, SWIA, SWEA, SEP, LPW, NGIMS, EUV and
  IUVS data, i.e. the induced Martian magnetosphere and its ionosphere.

**Considered and not selected.**

- **Corona**, **Chromosphere**, **Photosphere**, **Solar Interior** — PySPEDAS has no solar imaging
  or magnetogram support at all. Its SOHO module loads only CELIAS, COSTEP and ERNE (in-situ plasma
  and energetic particles) plus orbit data, and its STEREO module loads MAG, PLASTIC, SWEA, STE,
  SEPT, HET, LET, SIT and WAVES — no LASCO, no SECCHI, no EUV imager. Parker Solar Probe does fly
  through the corona, but PySPEDAS provides no corona-specific analysis; `Solar Environment` already
  covers the near-Sun in-situ missions.
- **Earth Lower and Middle Atmosphere** — BARREL balloons fly in the stratosphere, but their science
  target is magnetospheric electron precipitation, not the neutral middle atmosphere; no module
  models or analyses lower/middle atmospheric quantities.
- **Jupiter**, **Saturn**, **Uranus**, **Neptune Magnetosphere** — the Ulysses module loads that
  mission's heliospheric in-situ datasets, which happen to span its Jupiter flyby, but there is no
  outer-planet-specific functionality, coordinate system or model.
- **Heliosheath** — no Voyager or IBEX support. Voyager appears in this repository only as a CDAWeb
  GUI tutorial example (`docs/source/cdaweb.rst`, `cdagui_tools/tests/test_cdagui.py`), which is a
  demonstration of the generic CDAWeb browser rather than mission support.

### 6. Authors (MANDATORY)
1. **Vassilis Angelopoulos** | ORCID: https://orcid.org/0000-0001-7024-1561 | University of California, Los Angeles
2. **Bryan Harter** | ORCID: https://orcid.org/0000-0002-3908-9001 | Laboratory for Atmospheric and Space Physics
3. **Eric Grimes** | ORCID: https://orcid.org/0000-0001-5756-8789 | Adnet Systems (United States)
4. **Cindy Russell** | University of California, Los Angeles
5. **Jiashu Wu** | University of California, Los Angeles
6. **Jim Lewis** | ORCID: https://orcid.org/0009-0005-4191-5906 | Space Sciences Laboratory, University of California, Berkeley; University of California, Berkeley
7. **Alexander Drozdov** | ORCID: https://orcid.org/0000-0002-5334-2026 | University of California, Los Angeles
8. **Nick Hatzigeorgiu** | Space Sciences Laboratory, University of California, Berkeley; University of California, Berkeley
9. **James McTiernan** | ORCID: https://orcid.org/0000-0002-3038-176X | Space Sciences Laboratory, University of California, Berkeley; University of California, Berkeley
10. **Daniel Carpenter** | University of California, Los Angeles
11. **Julie Barnum** | ORCID: https://orcid.org/0000-0001-8755-0694 | Laboratory for Atmospheric and Space Physics

> **`family-names: GithubUser` is this project's own upstream convention, not an HSSI defect.** Seven
> entries in `CITATION.cff` (lines 50, 63, 68, 86, 93, 110, 112) use the literal family name
> `GithubUser` with the contributor's handle as the given name. HSSI reproduced that verbatim. Each
> of the seven is resolved individually below against a platform-native attribution standard —
> a GitHub noreply address encoding the account, or GitHub's commit API returning the account's login and
> ID. The outcomes differ per entry and are recorded on each: three resolved to a real person (13, 19,
> 34), two to an exact handle labelled `(GitHub)` (25, 28), one to `(Username)` because no account exists
> (35), and one to a mononym because the stored string was a display name rather than a handle (17). The
> upstream strings are preserved in those notes; a future refresh reading `CITATION.cff` must not
> reintroduce `GithubUser` as a family name.
12. **Ayris Narock** | ORCID: https://orcid.org/0000-0001-6746-7455 | Adnet Systems (United States)
13. **Zijin Zhang**
    - *Identity:* an earlier revision of this file recorded given "Beforerr", family "GithubUser". The git author is
      `Beforerr <58776897+Beforerr@users.noreply.github.com>`, and GitHub account ID 58776897 is login
      `Beforerr`, whose **profile publishes the name "Zijin Zhang"**. A real identity is proven, so the
      record is canonicalized to the person rather than labelled as a handle. **No identifier recorded:**
      thirteen ORCID records exist for this name; `0000-0002-9968-067X` (University of California, Los
      Angeles + USTC) is the only plausible one for a PySPEDAS contributor, but institutional similarity
      is not proof, so it was left unassigned.
14. **Marc Pulupa** | ORCID: https://orcid.org/0000-0002-1573-7457 | University of California, Berkeley
15. **Xiangning Chu** | ORCID: https://orcid.org/0000-0003-4109-0770 | University of Colorado Boulder
16. **Brent Smith** | Johns Hopkins University Applied Physics Laboratory
17. **Tiger** *(stored as an empty given name with family name `Tiger`)*
    - *Identity:* the `GithubUser` family name this project's roster uses is factually wrong here. GitHub's
      commit API attributes commit `c9accb2834003df8eadcde33dd3e5fbbd232a23d` to account `tiger2017`
      (ID 11709762) — so the stored string "Tiger" is **not** the handle, it is that account's own profile
      display name. This is therefore a mononym, preserved without any platform label. The mononym is
      held in the family-name field, matching how every other incomplete personal name in the catalogue is
      stored and keeping the invariant that no record has an empty family name.
18. **Austin Norris** | University of California, Los Angeles
19. **Kiril Bourakov**
    - *Identity:* an earlier revision of this file recorded given "Kiril B", family "GithubUser". GitHub's commit API
      attributes commit `713c9a605dcf0e692f8b9bb51e9a6269ae808f80` to account **`KirilBourakov`
      (ID 86131959)**, whose profile publishes the name **"Kiril Bourakov"**; that account has eight
      commits in this repository. A real identity is proven, so the record is canonicalized to the person.
      "Kiril B" was a given name plus a surname initial, not a username. **No identifier recorded:** an
      ORCID surname search for "Bourakov" returns zero records.
20. **Samuel T. Badman** | ORCID: https://orcid.org/0000-0002-6145-436X | Center for Astrophysics Harvard & Smithsonian
21. **Anansa Keaton-Ashanti** | The University of Texas at Austin
22. **Tomo Hori** | Nagoya University
23. **Takanobu Amano** | ORCID: https://orcid.org/0000-0002-2140-6961
24. **Warren Rexroad** | University of California, Berkeley
25. **krvidal (GitHub)** *(stored as givenName `krvidal`, familyName `(GitHub)`)*
    - *Identity:* a proven platform handle with no published human name. The git author is
      `krvidal <92814757+krvidal@users.noreply.github.com>`, whose noreply address encodes account ID
      92814757 and login `krvidal`. The upstream `GithubUser` family name is replaced by the platform
      label `(GitHub)`; **no human name is asserted.**
26. **Shuji Onosawa**
27. **Luke Powell** | Southwest Research Institute
28. **ThiGli (GitHub)** *(stored as givenName `ThiGli`, familyName `(GitHub)`)*
    - *Identity:* a proven platform handle. GitHub's commit API attributes commit
      `d95f877d1c3acb05fd86f3f475d1b61962e8e3fe` to account **`ThiGli` (ID 98546855)**. Note the
      **capitalization correction**: the exact login is `ThiGli`, not the lower-case `thigli` this roster
      uses. Handle capitalization is preserved verbatim. **No human name is asserted** — the account
      publishes none, though the commit address `t.glissmann@protonmail.com` is consistent with the
      login.
29. **Mykhaylo Shumko** | ORCID: https://orcid.org/0000-0002-0437-7521 | Johns Hopkins University Applied Physics Laboratory
30. **Qusai Al Shidi** | ORCID: https://orcid.org/0000-0003-0426-038X | West Virginia University
31. **Alex Antunes** | ORCID: https://orcid.org/0000-0002-3098-2602 | Johns Hopkins University Applied
    Physics Laboratory; Project Calliope
    - *Identity:* an earlier revision of this file recorded "Sandy Antunes" with the Project Calliope affiliation and no
      identifier. ORCID `0000-0002-3098-2602` resolves to "Alex Antunes" at JHU/APL, and that person
      commits as `Sandy Antunes <sandy.antunes@jhuapl.edu>`. **This project's own `CITATION.cff` is part
      of the proof**: it lists `Antunes, Sandy` with affiliation "Johns Hopkins University Applied Physics
      Laboratory" — the ORCID's employment. The name alone would not have sufficed; that ORCID record
      publishes no "Sandy" alias, so a refresh must not read that as a contradiction. The Project
      Calliope affiliation this project supplies is retained on his record alongside JHU/APL.
32. **Sean A. Q. Young** | Johns Hopkins University Applied Physics Laboratory
33. **Tien Vo** | ORCID: https://orcid.org/0000-0002-8335-1441 | Laboratory for Atmospheric and Space
    Physics (https://ror.org/01fcjzv38)
    - *Identity:* an earlier revision of this file carried a stray leading apostrophe in the family name
      (`'Vo`). **The
      apostrophe is this project's own upstream typo, and it is still live:** `CITATION.cff` line 108
      reads `family-names: '''Vo'`, whose YAML single-quote escaping yields `'Vo`. This repository's git
      history has the correct form, `Tien Vo <tienrvo@gmail.com>`. ORCID `0000-0002-8335-1441` resolves to
      "Tien Vo", now a postdoctoral scholar at UCLA and previously a graduate research assistant at LASP,
      CU Boulder, which is the affiliation recorded for the same person as PlasmaPy's author 139. A
      future refresh reading `CITATION.cff` must not restore the apostrophe. Note PlasmaPy separately
      lists **Anthony Vo**, a different person.
34. **Donglai Ma**
    - *Identity:* an earlier revision of this file recorded given "donglai96", family "GithubUser". GitHub's commit API
      attributes commit `bcff2ef5a231744635b84b87f06e122e30efcbc9` to account **`donglai96`
      (ID 29682557)**, whose profile publishes the name **"Donglai Ma"** and the company UCLA; the commit
      address `donglaima96@gmail.com` reconciles login and name. A real identity is proven, so the record
      is canonicalized to the person. **No identifier recorded:** six ORCID records exist for this name
      and none publishes an institution, so none could be matched.
35. **rale8469 (Username)** *(stored as givenName `rale8469`, familyName `(Username)`)*
    - *Identity:* a proven username whose platform cannot be established, so the platform-specific
      label is **not** used. GitHub's commit API attributes commit
      `31c47718cba9c8d574a983adf94e163d7415dadd` to **no account** (`author: null`), and no
      `github.com/rale8469` exists — so this roster's `GithubUser` classification is factually
      unsupported and must not be carried forward. The string is nonetheless certainly a username: the git
      address is `rale8469@macl63.lasp.colorado.edu`, a LASP machine-local address whose local part is the
      handle itself, and this project's own `CITATION.cff` classifies it as a user handle. Hence
      `(Username)` rather than `(GitHub)`.
36. **Benjamin Short** | ORCID: https://orcid.org/0000-0003-3945-6577
37. **Elysia Lucas** | Laboratory for Atmospheric and Space Physics

- **Roster completeness.** `CITATION.cff` at the pinned revision lists exactly these 37 people in
  this order, so no contributor has been added upstream since the roster was last reconciled and
  nobody needs to be added or removed. Affiliation strings above are the organization names HSSI
  actually stores (resolved from the affiliation records referenced by the software entry), not the
  raw `CITATION.cff` strings; the two differ in punctuation for several organizations, for example
  `Center for Astrophysics Harvard & Smithsonian` (stored) versus
  `Center for Astrophysics | Harvard & Smithsonian` (`CITATION.cff`).
- **The upstream `GithubUser` convention is resolved, not copied.** Seven `CITATION.cff` entries use
  that placeholder, but each has been evaluated independently. The author entries and identity notes
  above preserve the upstream strings while recording the evidence-backed result: a proven person,
  a platform handle, an unassigned username, or a mononym. A later refresh must not restore the
  literal `GithubUser` family name merely because it reappears in `CITATION.cff`.
- **Divergences between `CITATION.cff` and the stored affiliations, deliberately not applied.**
  `CITATION.cff` gives Nick Hatzigeorgiu's affiliation as University of California, Los Angeles,
  whereas the stored record has Space Sciences Laboratory, University of California, Berkeley plus
  University of California, Berkeley; it gives Sandy Antunes as Johns Hopkins University Applied
  Physics Laboratory, while the shared stored record carries both that organization and Project
  Calliope; it lists no affiliation for
  Mykhaylo Shumko, whereas the stored record has Johns Hopkins University Applied Physics
  Laboratory; it likewise lists no affiliation for Cindy Russell, whereas the stored record gives
  her the same University of California, Los Angeles organization that Angelopoulos, Wu, Drozdov,
  Carpenter and Norris carry; and it gives Samuel Badman's given name as `Samuel` rather than the
  stored `Samuel T.`. Two further divergences belong in the same list: `CITATION.cff` gives Vassilis
  Angelopoulos's affiliation as UCLA Division of Physical Sciences, whereas the stored record has
  University of California, Los Angeles; and it gives Jim Lewis and James McTiernan only University
  of California, Berkeley, whereas the stored record additionally carries Space Sciences Laboratory,
  University of California, Berkeley for each of them. These were reconciled deliberately when the
  roster was reconciled: the stored values were preserved rather than overwritten by `CITATION.cff`.
  They are recorded here so a future refresh recognises them as known, settled divergences rather
  than fresh drift.
- **Durable platform limitation.** An author *name* correction is not expressible through a routine
  metadata update: the update path silently no-ops a rename of an existing person record, it cannot
  *replace* an existing affiliation (adding one that matches by ROR is idempotent, so additions do
  work), and it rejects the entire authors field if any stored given name is blank. Person records
  are also shared across software entries, so changing one here could affect other entries that
  reference it. Any name repair therefore has to happen at the data layer with the other references
  checked first, and should not be re-proposed as part of an ordinary metadata refresh.

### 7. Software Name (MANDATORY)
- **Name:** PySPEDAS
- **Full Name:** PySPEDAS (Space Physics Environment Data Analysis System in Python)
- Source: `README.md` heading, `CITATION.cff` `title`, DataCite/Zenodo title for both the concept and
  the 2.1.4 DOI. The PyPI distribution name is the lower-case `pyspedas` (`pyproject.toml`
  `name`) and the PyHC core registry spells it `pySPEDAS`; the mixed-case `PySPEDAS` used in the
  README, the citation file and the DOI records is the form recorded here, and it is the stored
  value. The parenthetical long form is retained as context, not as the stored name.

### 8. Description (MANDATORY)
- **Description:** The Python-based Space Physics Environment Data Analysis Software (PySPEDAS)
  framework supports multi-mission, multi-instrument retrieval, analysis, and visualization of
  heliophysics time series data. PySPEDAS provides a unified Python interface, modeled on the IDL
  SPEDAS toolkit, for loading data from more than 35 space- and ground-based heliophysics projects.
  It includes coordinate transformations; particle distribution analysis; wavelet and wave
  polarization analysis; magnetic field modeling and field-line tracing; multi-spacecraft analysis;
  neutral sheet, magnetopause, and bow shock models; the embedded PyTplot framework for time-series
  management and plotting; and access to CDAWeb, HAPI, SPDF, ISTP, mission-specific, and cloud data
  sources.
- Source and re-verification at 2.1.4: the opening sentence is the upstream abstract used verbatim in
  `README.md`, `CITATION.cff` and the Zenodo/DataCite description. The "more than 35" claim still
  holds — `pyspedas/projects/` contains 37 project subpackages at the pinned revision (the README's
  "Projects Supported" list names 33 of them; BARREL, ELFIN, KOMPSAT and the NOAA/GFZ Kp loader are
  present in the package but absent from that list). "The embedded PyTplot framework" matches the
  README's PyTplot section, which records that from PySPEDAS 2.0 the external `pytplot` /
  `pytplot-mpl-temp` packages are no longer required because their functionality now lives in
  `pyspedas/tplot_tools/`. No wording change is warranted for this release.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Python framework for multi-mission heliophysics data retrieval, analysis,
  and visualization, with coordinate transforms, field models, and particle-distribution tools.
- Source: condensed from the full description and `pyproject.toml`'s one-line `description`. 167
  characters, within the 200-character limit. Still accurate for 2.1.4; retained unchanged because
  the wording is a settled editorial choice, not a value in need of refresh.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2016-10-11
- Source: the repository's first commit, `9bb0757e66fba434a09335833fe278e302d5fe62`, "Turning project
  into pypi package", dated 2016-10-11. Deliberately *not* taken from DataCite or `CITATION.cff`:
  the DOI record's `Issued` date tracks the most recent Zenodo deposit (currently 2026-08-05) and
  `CITATION.cff`'s `date-released` (2025-11-07) describes a later software release, neither of which
  is the date of first publication of this software.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- Source: DataCite `publisher` for both the concept DOI and the 2.1.4 versioned DOI. Zenodo is the
  correct entry because the DOIs were minted through the GitHub–Zenodo workflow.

### 12. Version (RECOMMENDED)
- **Version Number:** 2.1.4
- **Version Date:** 2026-08-06
- **Version Description:** PySPEDAS 2.1.4 supersedes 2.1.2 and rolls up the intervening 2.1.3
  release. From 2.1.3: customizable basemap plotting with ionospheric footpoint traces and station
  field-of-view overlays (`tplot_map`), more efficient MMS SDC burst-interval queries, improved
  handling of input and output coordinate systems and units in the field-line tracing routines, and a
  `quiet` flag to suppress progress messages in the coordinate-transform routines. New in 2.1.4: an
  option for load routines to apply THEMIS eclipse spin-model corrections; general-purpose TAI/Unix
  time converters with the MMS TAI wrappers rewired through them; reworked and cached MMS fast-survey
  and burst-segment queries; retry handling for HTTP 429 responses from the MAVEN and MMS SDC
  servers; a keyword to disable MAVEN KP file downloads; a fix to HPCA multiply-charged (He++) flux
  conversion; correct propagation of spectrogram pseudovariable options such as ytitle and zlog;
  support for dividing a time series by a scalar; preservation of `store_data` input dictionaries;
  and an initial pre-commit configuration.
- **Version PID:** https://doi.org/10.5281/zenodo.21812086
- Source: git tag `v2.1.4` at commit `8eb4272ad4d586e6ea84404c671d45810b421334`; `pyproject.toml`
  `version = "2.1.4"` and `[project.urls] Versioned_DOI`; the GitHub release notes for `v2.1.3` and
  `v2.1.4`; and `git log v2.1.2..v2.1.4`. The intervening release `v2.1.3` is commit
  `66c874565da0626c4377a20d549e9d07dba3382b`, whose GitHub release was published 2026-06-25.
- **How the version date was chosen, and the two dates that disagree with it.** 2026-08-06 is the
  date of the release commit itself (`8eb4272a`, authored and committed 2026-08-06 09:23:54 −0700),
  which is also the day the GitHub release object was created (2026-08-06T16:23:54Z). Two other
  candidate dates exist and were rejected: GitHub reports `published_at` 2026-08-07T21:26:15Z, which
  is when the release became publicly visible rather than when it was cut, a day later than the
  release commit; and Zenodo/DataCite record an `Issued` / `publication_date` of
  2026-08-05, which is *earlier* than the release commit and earlier than the Zenodo record's own
  creation timestamp (2026-08-07T23:33:50Z) and is therefore not supported by any repository
  artifact. Zenodo's deposit metadata is known to reproduce upstream errors verbatim, so the
  repository-derived date is preferred. The same reasoning was applied to the previous stored version
  (2.1.2, dated 2026-06-08), where the release commit and the GitHub release date happened to agree.
- **Stored form versus displayed form.** The value stored for the version number is the bare string
  `2.1.4`. The read API renders it with the software name prefixed, as `PySPEDAS - 2.1.4`; that
  prefix is a display transform and must never be written back into the version field.
- **Known side effect of changing this field.** Replacing the version replaces the underlying version
  record rather than editing it, leaving the previous one unreferenced. This has been reviewed and
  accepted as normal platform behaviour; no cleanup should be proposed for it.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- Source: `pyproject.toml` `requires-python = ">=3.10"` and the classifiers for Python 3.10 through
  3.14; `README.md` "Python 3.10+ is required"; Zenodo's `code:programmingLanguage` custom field
  ("Python"). The codebase is pure Python — no compiled extension is built, and `build-system`
  requires only setuptools and wheel. IDL was considered and rejected: PySPEDAS is *modeled on* IDL
  SPEDAS and interoperates with it, but contains no IDL source.

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.3389/fspas.2022.1020815
- Title: "The Space Physics Environment Data Analysis System in Python" (Angelopoulos et al.,
  *Frontiers in Astronomy and Space Sciences*, 2023).
- Source: the `IsDescribedBy` related identifier on both the concept DOI and the 2.1.4 versioned DOI
  in DataCite, and the `isDescribedBy` relation in the Zenodo record.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT
- Source: `LICENSE.txt` contains the MIT text; `pyproject.toml` declares `license = "MIT"`;
  `CITATION.cff` declares `license: [mit]`; DataCite's `rightsList` carries
  `MIT License` with SPDX identifier `mit`. The URI recorded here is the one the HSSI licence entry
  itself carries (`https://spdx.org/licenses/MIT`); note that DataCite instead publishes
  `https://opensource.org/licenses/MIT` for the same licence, and that the DOI record additionally
  asserts "Copyright (C) 2026, Regents of the University of California (unless otherwise noted in
  source code)", which is a copyright statement rather than a second licence.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- ace
- ae index
- arase
- artemis
- astrophysics
- aurora
- cdaweb
- cdf
- cluster
- coordinate transformations
- data
- data analysis
- data retrieval
- data visualization
- erg
- esa
- geomagnetic index
- geopack
- geophysics
- goes
- ground magnetometer
- hapi
- heliophysics
- heliosphere
- hso
- IDL SPEDAS
- igrf
- ionosphere
- istp
- jaxa
- kp index
- magnetic field models
- magnetosphere
- magnetotelluric
- maven
- mms
- nasa
- netcdf
- noaa
- omniweb
- particle moments
- pitch angle distributions
- plasma
- poes
- python
- python package
- pytplot
- rbsp
- remote sensing
- satellite data
- science research
- scientific computing
- solar physics
- solar wind
- space
- space physics
- space science
- space weather
- spectrograms
- spedas
- themis
- time series analysis
- tools
- tsyganenko
- van allen probes
- wavelet analysis
- wave polarization

- **Form of the values.** These are the stored keyword strings, which are lower-case except for the
  one legacy entry `IDL SPEDAS`. The web view renders them in Title Case (`Ace`, `Idl Spedas`, …);
  that is a display transform. Comparisons against any other source must be done on the
  case-normalized string, or the same keyword will look like drift.
- **Coverage.** Every keyword declared in `pyproject.toml` at 2.1.4 (50 terms) is present here after
  case normalization; the release added no new package keyword relative to the stored set. The
  remainder are capability and data-service terms added when the record was enriched
  (`cdaweb`, `coordinate transformations`, `hapi`, `heliosphere`, `IDL SPEDAS`, `particle moments`,
  `pitch angle distributions`, `plasma`, `python`, `pytplot`, `science research`, `solar wind`,
  `space`, `spectrograms`, `wavelet analysis`, `wave polarization`, `ground magnetometer`).
- **Deliberately omitted.** Thirty terms in the `CITATION.cff` keyword list are absent from the set
  above. Eighteen name a mission or a data product: DSCOVR, EQUATOR-S, FAST, GEOTAIL, IMAGE,
  KOMPSAT, MICA, POLAR, PSP, SOLO, WIND, Akebono, BARREL, ELFIN, ICON and Kyoto Dst, together with
  `Parker Solar Probe` and `Solar Orbiter`, which are the long forms of the PSP and SOLO
  abbreviations already in that list. The other twelve are `plotting`, `line plots`,
  `spectrogram plots`, `particles`, `moments`, `fields`, `coordinates`, `data access`,
  `magnetic field modeling`, `geomagnetic`, `GMAG` and `IUGONET`. Mission names belong in Related
  Observatories, where they are recorded with SPASE identifiers, and all but the last of those
  twelve are near-synonyms of terms already present, which would create near-duplicate rows in an
  open vocabulary that never rejects a value; `IUGONET` is a data-network label whose exclusion is
  reasoned out as a documented omission under Related Observatories. This trimming is a settled
  decision, not an omission to repair.

### 17. Data Sources (OPTIONAL)
- CDAWeb
- FTP/FTPS Directories
- GFZ
- HAPI
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- OMNIWeb
- Other
- S3/Cloud-aware
- VirES
- WDC

- Source for the values carried forward: `cdagui_tools/` wraps `cdasws` for CDAWeb;
  `hapi_tools/hapi.py` wraps `hapiclient`; `projects/omni/` loads the OMNI record; `vires/load.py`
  uses `viresclient` against `https://vires.services/ows`; `utilities/download.py` and
  `download_ftp.py` implement HTTP(S) and FTP retrieval; `utilities/download.py`'s `is_fsspec_uri`
  plus the `s3fs`/`aioboto3`/`fsspec` dependencies and the README "Cloud Repositories" section give
  S3/cloud-aware access.
- **How the servers divide between `Observatory/Mission-specific` and `Other`.** Each named server
  belongs to exactly one of the two values: a service is either run by the mission or observatory
  whose data it serves, or it is a general multi-mission archive. It is never counted as both.
  - `Observatory/Mission-specific` — the mission- and observatory-run servers that many
    `projects/<name>/load.py` routines target instead of a general archive: the MMS Science Data
    Center at LASP (`projects/mms/mms_load_data.py`, `mms_events.py`), the MAVEN SDC at LASP
    (`projects/maven/download_files_utilities.py`), the Berkeley SSL THEMIS server
    (`projects/themis/config.py` sets `remote_data_dir` to `https://themis.ssl.berkeley.edu/data/themis/`,
    and `projects/themis/ground/gmag.py` queries `themis.ssl.berkeley.edu/gmag/gmag_json.php` for the
    ground magnetometer station list), the UCLA SECS server (`projects/secs/config.py`,
    `http://vmo.igpp.ucla.edu/data1/SECS/`), the University of New Hampshire MICA server
    (`projects/mica/config.py`, `http://mirl.unh.edu/ULF/cdf/`) and the ISEE/Nagoya ERG Science
    Center endpoint behind the ERG modules (`projects/erg/config.py`,
    `https://ergsc.isee.nagoya-u.ac.jp/data/ergsc/`). Worth recording so it is not misread later:
    `projects/themis/config.py` also carries a UCLA THEMIS mirror
    (`https://themis-data.igpp.ucla.edu/`) and an SPDF path, but both are commented out — the active
    THEMIS server is Berkeley's, and UCLA's role here is SECS, not THEMIS.
  - `Other` — the general, multi-mission services with no row of their own: the SPDF file tree, used
    as the default or fallback archive by many project modules; NOAA's NCEI archive
    (`projects/goes/config.py`, `projects/poes/config.py`); and EarthScope's FDSN service
    (`pyspedas/mth5/load_fdsn.py`, `client="EARTHSCOPE"`).
- **Evidence for `GFZ` and `WDC`.** `GFZ` — `projects/noaa/noaa_load_kp.py` takes a `gfz` keyword
  and switches to the GFZ (Helmholtz Centre Potsdam) archive via `CONFIG['gfz_remote_data_dir']`,
  and it does so automatically for years from 2018 onward;
  `projects/kyoto/load_geomagnetic_indices.py` lists `"gfz"` among its selectable sources.
  `WDC` — `projects/kyoto/load_dst.py` and `load_ae.py` download the Dst and AE indices directly
  from the World Data Center for Geomagnetism, Kyoto at `https://wdc.kugi.kyoto-u.ac.jp/`.
- **Considered and not selected.** `SSCWeb` — `projects/themis/state_tools/ssc.py` and `ssc_pre.py`
  are documented as loading "THEMIS current/past orbit data from CDAWeb/SSCWeb", but the path they
  build is the CDAWeb file tree (`https://cdaweb.gsfc.nasa.gov/pub/data/themis/thc/ssc/`) and there
  is no SSCWeb web-service client in the dependency set, so `CDAWeb` already covers it.
  `Madrigal`, `AMDA` and `TAP` — no references anywhere in the tree. `das2` — the only occurrences are the University of Iowa HAPI
  endpoint `http://planet.physics.uiowa.edu/das/das2Server/hapi`, printed in an error message in
  `hapi_tools/hapi.py` and listed among the known HAPI servers in `docs/source/hapi.rst`; PySPEDAS
  reaches that server over HAPI, not over the das2 protocol.
- **Trap worth remembering.** The Virtual Solar Observatory entry in this vocabulary ends with a
  full stop (`The Virtual Solar Observatory.`). It is not selected here — PySPEDAS has no VSO client
  — but any future addition must copy the trailing period or it will not match.

### 18. Input File Formats (RECOMMENDED)
- ascii
- CDF
- csv
- HDF5
- IDL.sav
- ISTP-Compliant
- JSON
- netCDF3/4
- Other

- Source: `tplot_tools/importers/cdf_to_tplot.py` (CDF, with ISTP metadata conventions honoured
  throughout — `get_support_data`, `VAR_TYPE`, `varformat`); `netcdf_to_tplot.py` (netCDF3/4,
  including mission-specific workarounds for ICON's non-standard unit strings and POES/MetOp epoch
  descriptions); `sts_to_tplot.py` (MAVEN STS ASCII); `tplot_restore.py` (IDL `.sav` tplot save files
  via `scipy.io.readsav`, plus Python pickle for PySPEDAS-written saves);
  `projects/mms/mms_login_lasp.py` reads IDL SPEDAS's `~/mms_auth_info.sav` credential cache, and
  2.1.4 added loading of `.sav` files carrying early-mission MMS fast-survey intervals;
  `projects/akebono/load_csv_file.py` and the FEEPS sun-contamination sector masks
  (`projects/mms/feeps_tools/sun/*.csv`) are CSV; the ELFIN EPD calibration tables
  (`el*_epde_cal_data.txt`), the Kyoto index pages and the MMS ancillary/attitude/ephemeris products
  under `projects/mms/mec_ascii/` are ASCII; JSON is parsed from service responses in
  `mms_load_data.py`, `mec_ascii/mms_get_state_data.py`, `mms_get_tetrahedron_qf.py`,
  `projects/kompsat/esa_hapi_data.py` and `projects/themis/ground/gmag.py`; HDF5 arrives through the
  optional `mth5` extra, which builds and then reads an MTH5 `.h5` file in
  `pyspedas/mth5/load_fdsn.py`. `Other` covers the formats with no row of their own: MAVEN STS,
  MTH5's magnetotelluric HDF5 schema, PySPEDAS pickle saves, and the plain-text calibration and
  parameter tables.
- **`FITS` was previously submitted and has been removed as incorrect.** PySPEDAS reads no FITS
  files. At the pinned revision there is no FITS reader, no `astropy.io.fits` import and no code
  path that opens a FITS file; searching every tracked file for "fits" case-insensitively returns
  only the words "spin fits", the Wind `3dp_emfits_e0` datatype name, and a `*.fits` line in
  `.gitignore` (`.gitignore:10`). `astropy` is a dependency, but its ten
  non-test imports are `astropy.units` in `tplot_tools/get_data.py` and `astropy.coordinates`
  spherical/Cartesian conversion helpers in nine files under `particles/spd_part_products/` and
  `projects/erg/`. This is a relevance correction, not a vocabulary miss: `FITS` does exist as a row
  in the live `FileFormat` vocabulary, so a future refresh that finds the value available should not
  read its absence here as a resolution failure.
- **Considered and not selected.** `Zarr` — no Zarr use; the cloud support streams CDF and netCDF
  objects through `fsspec`/`s3fs` rather than a chunked array store. (The only textual matches for
  "zarr" anywhere in the source tree are the local variables `bzarr` and `bzarra` in
  `cotrans_tools/gsm2lmn.py`, plus one incidental binary match inside the screenshot
  `docs/source/_static/vscode_createenv.png`. The qualifier "textual" is doing real work in that
  sentence: without it the claim would be false, and a binary grep hit inside a screenshot is not a
  Zarr reference.)

### 19. Output File Formats (RECOMMENDED)
- ascii
- csv
- Other

- Source: `tplot_tools/exporters/tplot_ascii.py` converts a tplot variable to a pandas frame and
  writes CSV (its docstring states that no other file format is supported, and it writes spectral bin
  metadata to a companion `_v` file); `tplot_tools/exporters/tplot_save.py` writes a Python pickle;
  `tplot_tools/MPLPlotter/save_plot.py` and `projects/secs/makeplots.py` emit matplotlib raster and
  vector figures (PNG, PDF, SVG, JPEG). `ascii` and `csv` cover the tabular export, and `Other`
  covers the figure formats and the pickle save file.
- **Considered and not selected.** `HDF5` as an *output* — `pyspedas/mth5/load_fdsn.py` does cause an
  MTH5 `.h5` file to be created in the local data directory, but that file is produced by the `mth5`
  library as a download cache on the way to building tplot variables, not by a PySPEDAS "save my
  data as HDF5" capability. It is recorded as an input format only.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows
- Source: `README.md` states plainly that "PySPEDAS supports Windows, macOS and Linux" and gives
  activation instructions for each; `pyproject.toml` carries the classifier
  `Operating System :: OS Independent`; the package is pure Python with no platform-specific code.
- **Considered and not selected.** `Operating System Independent` — that value exists in the
  vocabulary and would match the setuptools classifier, but the three named platforms are the ones
  the project actually documents and supports, and they are more informative to a user. Note also
  that continuous integration currently exercises Linux only: every workflow in `.github/workflows/`
  runs on `ubuntu-latest`, and the macOS and Windows matrix entries in `quick_tests.yml` are
  commented out. `OS Independent` (without the words spelled out) is not a value in this vocabulary
  and must never be emitted.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent
- Source: pure-Python package with no compiled extension and no architecture-specific classifier or
  build step in `pyproject.toml`; its numerical work is delegated to NumPy and SciPy, which supply
  their own per-architecture wheels. No narrower value (x86-64, Apple Silicon arm64, …) is asserted
  by the project.

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections
- Geomagnetic Storms
- Solar Flares
- Solar Wind
- X-ray emission

- Source for the four carried forward: solar-wind plasma and field data are a core product of the
  ACE, Wind, DSCOVR, OMNI, PSP, Solar Orbiter, STEREO and Ulysses modules; geomagnetic storms are
  addressed through the Dst, AE and Kp index loaders (`projects/kyoto/`, `projects/noaa/`) and the
  storm-time Tsyganenko models; interplanetary CME signatures and flare-associated particle events
  are what the solar-wind monitors and the energetic-particle instruments (ACE EPAM/SIS/CRIS, STEREO
  HET/LET/SEPT, SOHO ERNE/COSTEP, Solar Orbiter EPD) measure.
- **Evidence for `X-ray emission`.** `projects/goes/load.py` supports the `xrs` instrument
  across GOES 8–19, including the `gxrs-l2-irrad`, `xrsf-l2-flx1s` and `xrsf-l2-avg1m` solar X-ray
  irradiance products that define the standard flare classification; `projects/barrel/` loads the
  BARREL fast, medium and slow X-ray spectra (`fspc.py`, `mspc.py`, `sspc.py`) from
  bremsstrahlung produced by precipitating electrons; and `projects/polar/pixie.py` loads the Polar
  X-ray imager.
- **Considered and not selected.** `Solar Corona` and `Coronal Heating` — PySPEDAS has no coronal
  imaging or coronal-analysis capability (see the Corona discussion under Related Region). This
  vocabulary is closed and rejects unknown values, so phenomena that PySPEDAS supports but that have
  no row here — substorms, radiation-belt dynamics, magnetic reconnection, plasma waves — would have
  to be represented through Keywords instead, which is the only open vocabulary in the form.

### 23. Development Status (RECOMMENDED)
- **Status:** Active
- Source: the repostatus.org "Active" badge in `README.md`; `pyproject.toml` classifier
  `Development Status :: 5 - Production/Stable`; Zenodo's `code:developmentStatus` of "active"; 97
  commits and two tagged releases (2.1.3 and 2.1.4) between the previously recorded version and the
  `v2.1.4` tag; the PyHC core registry rates community, documentation, testing, software
  maturity, Python 3 support and license all "Good".

### 24. Documentation (RECOMMENDED)
- **URL:** https://pyspedas.readthedocs.io
- Source: `pyproject.toml` `[project.urls] Documentation`, `README.md` "Documentation" section, and
  the PyHC core registry `docs` field — all three give this URL. The presence of `.readthedocs.yaml`
  additionally confirms the project builds its Sphinx documentation on Read the Docs, but that file
  is a build configuration only (`version: 2`, `build.os`, `sphinx.configuration`, `python.install`)
  and carries no project documentation URL of its own; it is not evidence for this value.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80
- Source: all three funding references on the concept and versioned DOIs name
  `National Aeronautics and Space Administration` (Crossref Funder ID 10.13039/100000104), and
  Zenodo's grant records carry the ROR-prefixed internal identifiers `027ka1x80::…`. The name is
  recorded in full rather than as the acronym NASA, per the organization-naming rule.

### 26. Award Title (OPTIONAL)
1. **Award Title:** MMS
   - **Award Number:** NNG04EB99C
2. **Award Title:** SPEDAS Community Support
   - **Award Number:** NNG17PZ01C
3. **Award Title:** THEMIS
   - **Award Number:** NAS5-02099
- Source: the `fundingReferences` on both the concept DOI and the 2.1.4 versioned DOI, and Zenodo's
  `grants` block, which agree exactly. All three titles are short, well within the 128-character
  limit that award titles are subject to.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found. The Angelopoulos et al. (2023) *Frontiers* paper is the reference publication and is
recorded in Field 14; it is the only publication either DOI record relates to
(`IsDescribedBy`). The repository's `README.md` and documentation cite no further publications as
developer priorities, and the DOI records carry no other publication-type related identifier.

### 28. Related Datasets (OPTIONAL)
Not found. PySPEDAS retrieves a very large number of heliophysics datasets at run time, but it
neither bundles any dataset nor names specific dataset DOIs as citations. The DOI records carry no
`Dataset` related identifier. The missions whose data it retrieves are captured in Field 32 instead,
which is the field designed for that relationship.

### 29. Related Software (OPTIONAL)
- https://github.com/hapi-server/client-python — hapiclient, the HAPI server client that
  `pyspedas/hapi_tools/hapi.py` wraps
- https://github.com/spedas/bleeding_edge — IDL SPEDAS, the parent project PySPEDAS is a Python
  reimplementation of
- https://doi.org/10.5281/zenodo.14919975 — the DOI for that same IDL SPEDAS software (DataCite
  resolves it as "SPEDAS (Space Physics Environment Data Analysis System)", version 6.1, IDL,
  by Angelopoulos, Lewis, McTiernan, Grimes, Russell, Drozdov, Cruce, Hatzigeorgiu, Wu, Larson,
  McFadden and Flores). It reached this record through the `IsSupplementedBy` relation on the
  PySPEDAS DOI. Recording both this DOI and the `bleeding_edge` repository URL means IDL SPEDAS is
  represented twice, once in each of the two forms the field accepts; that is worth knowing before
  anyone treats one of them as an unexplained extra entry.
- https://github.com/spedas/pyspedas_examples — the companion example and notebook repository, linked
  from `README.md`
- https://github.com/spedas/mms-examples — MMS-specific example notebooks, linked from `README.md`
- https://github.com/spedas/themis-examples — THEMIS-specific example notebooks, linked from
  `README.md`

- **What was deliberately trimmed and why.** `cdflib`, `geopack` and SpacePy were removed from this
  field when it was last curated, on the grounds that they are routine dependencies rather than
  software that distinguishes PySPEDAS. That decision stands.
- **Considered and not added.** `cdasws`, `viresclient` and `mth5` are domain-specific client
  libraries with the same standing as `hapiclient`, which is listed. They are not added, to keep this
  field focused on the parent project, the companion example repositories and the one data-access
  client whose capability PySPEDAS advertises as a headline feature with its own module and
  documentation page (`pyspedas/hapi_tools/`, `docs/source/hapi.rst`). A future curator who wants
  symmetry here has the facts; the asymmetry is intentional, not an oversight.
- **Excluded on principle.** NumPy, SciPy, pandas, matplotlib, requests and the rest of the generic
  scientific-Python stack are not related software: their presence says nothing about PySPEDAS that
  is not equally true of most of the ecosystem.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/MAVENSDC/PyTplot — PyTplot. PySPEDAS 2.0 vendored PyTplot's functionality into
  `pyspedas/tplot_tools/`; 35 files under `pyspedas/` still carry a MAVENSDC PyTplot provenance
  header (among them `tplot_restore.py`, `tplot_save.py`, `tplot_ascii.py` and
  `convert_tplotxarray_to_pandas_dataframe.py`), so this is a wholesale vendoring rather than an
  incidental borrowing. The two share the tplot variable data model and the
  `tplot_save`/`tplot_restore` save-file format, so variables and saved sessions pass between them.
- https://github.com/spedas/bleeding_edge — IDL SPEDAS. This is a cross-language bridge to a named
  domain tool, which the field's criteria treat as qualifying interoperability, and the evidence is
  specific rather than generic: `tplot_tools/importers/tplot_restore.py` reads IDL `.tplot` save
  files written by IDL SPEDAS's `tplot_save` routine (dispatching on the `.tplot` suffix to
  `scipy.io.readsav`); `projects/mms/mms_login_lasp.py` reads, via `scipy.io.readsav`, the same
  `~/mms_auth_info.sav` MMS credential cache that IDL SPEDAS writes (PySPEDAS's own cache is a
  Python pickle); 2.1.4 added reading of IDL `.sav` files carrying MMS fast-survey intervals;
  `README.md` states that the `SPEDAS_DATA_DIR` local data directory "will also be used by IDL (if
  you're running a recent copy of the bleeding edge)"; and `utilities/libs.py` reimplements IDL
  SPEDAS's `libs` routine-search command. IDL SPEDAS is also listed in Field 29 as the parent
  project; listing it here as well records the distinct fact that the two tools exchange data.
- https://github.com/pydata/xarray — xarray. The exchange is a documented public API rather than
  internal use, which is what the field's Tier-B bar requires: `pyspedas/tplot_tools/get_data.py:12`
  declares `def get_data(name, xarray=False, …)` and returns the underlying xarray object when the
  flag is set, `get_data.py:194` gives the same option on the `get()` wrapper, and
  `pyspedas/tplot_tools/store_data.py:209` documents the store path accepting an xarray `DataArray`
  as its time input. A caller can therefore hand PySPEDAS an xarray object and take one back.

- **Why xarray is listed after previously being trimmed.** An earlier curation removed xarray from
  this field along with a group of generic dependencies. That grouping was wrong for xarray
  specifically: the `xarray=True` option is part of the public signature of the two functions users
  call to retrieve data, so the relationship is an advertised interchange format and not merely an
  internal array container. The earlier decision is reversed on that evidence. The rest of that
  trim stands.
- **Considered and not selected.** PlasmaPy, SpacePy, Astropy, cdflib, geopack, hapiclient, NumPy,
  pandas, SciPy and matplotlib were removed from this field when it was last curated, as generic
  dependencies or loosely-related projects, and that decision stands. PlasmaPy and SpacePy are each
  demonstrated only by a notebook hosted in the separate `spedas/mms-examples` repository ("Plasma
  calculations with PlasmaPy", "Quaternion transformations with SpacePy"), linked from `README.md`;
  that was judged too loose a relationship, and no new evidence has appeared.

### 31. Related Instruments (OPTIONAL)

Sixty-five instrument rows are recorded. They are a deliberately bounded subset, chosen by one rule:

> **An instrument is listed when PySPEDAS carries dedicated processing code for its data —
> calibration, plasma moments, energy spectra, pitch-angle distributions, distribution
> reconstruction or slicing, spin- and attitude-correction, or instrument-specific artifact
> corrections. An instrument is not listed when PySPEDAS merely has a load call for it.**

**Instruments outside that boundary are still supported by PySPEDAS, and their support is recorded
at mission level in Field 32.** This list is not a statement that the unlisted instruments are
unsupported. PySPEDAS loads data from far more instruments than are listed here: the 37 projects
under `pyspedas/projects/` between them cover the instrument suites of dozens of missions and ground
networks, and those missions and networks are either recorded in Related Observatories or their
absence is documented there. The instrument field records the narrower fact that PySPEDAS
does instrument-specific science processing for these particular instruments — which is what a user
searching HSSI for a specific instrument is looking for, and what an enumeration of every load
routine would have drowned out.

SPASE namespaces instruments beneath their spacecraft, so a single instrument maps to one row per
spacecraft; it also namespaces a suite above its sub-instruments, so one suite can map to several
rows on a single spacecraft. Expansions of either kind are made only where a concrete repository
artifact names what is being expanded. For a per-spacecraft expansion that artifact is an explicit
probe list, a validated probe set, a per-spacecraft calibration table, or a routine that requires a
fixed number of spacecraft. For a sub-instrument expansion within one spacecraft — the three Parker
Solar Probe FIELDS rows below are that case — it is an explicit variable-name list that picks out
those sub-instruments and nothing else in the suite (`projects/psp/filter.py:105-108`). Where the
repository does not name them, no expansion is made.

**Duplicate display names are expected in this table and are not errors.** Each MMS instrument
recorded here carries one name across all four probes (four rows each named `MMS FEEPS`, `MMS EIS`,
`MMS FPI/DES`, `MMS FPI/DIS`, `MMS HPCA` and `MMS FIELDS/FGM`); both ELFIN EPD rows are named
`The Electron Losses and Fields Investigation`, both RBSPICE rows `RBSP RBSPICE`, all four
Cluster CIS rows `Cluster Ion Spectrometry`, and all three Parker Solar Probe rows `PSP FIELDS`.
The identifier is what distinguishes and links them.
Among the rows recorded here, THEMIS is the exception: its names embed the probe letter. Several names also carry
irregular internal spacing upstream (`THEMIS-A:  Solid State Telescope` has two spaces after the
colon, `THEMIS-A: Search Coil Magnetometer` has one); the names below are copied byte-verbatim from
the vocabulary and must stay that way.

| Instrument | SPASE row name (verbatim) | SPASE identifier | Repository evidence |
|---|---|---|---|
| MMS FEEPS, MMS1 | MMS FEEPS | https://spase-metadata.org/SMWG/Instrument/MMS/1/EnergeticParticleDetector/FEEPS | `feeps_tools/` flat-field, energy-table and sun-contamination corrections plus PADs and spin averaging; probe list at `feeps_tools/feeps.py:56` |
| MMS EIS, MMS1 | MMS EIS | https://spase-metadata.org/SMWG/Instrument/MMS/1/EnergeticParticleDetector/EIS | `eis_tools/` omni spectra, PADs, spin averaging and cross-spacecraft spectrum combination; probe list at `eis_tools/eis.py:26` |
| MMS FPI (DES), MMS1 | MMS FPI/DES | https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DES | `fpi_tools/mms_get_fpi_dist.py`, `mms_load_fpi_calc_pad.py`, `particles/mms_part_des_photoelectrons.py`; `des-*` datatypes at `fpi_tools/fpi.py:40`, probe list at `fpi.py:27` |
| MMS FPI (DIS), MMS1 | MMS FPI/DIS | https://spase-metadata.org/SMWG/Instrument/MMS/1/FastPlasmaInstrument/DIS | `fpi_tools/mms_get_fpi_dist.py`, `mms_pad_fpi.py`, `mms_fpi_split_tensor.py`; `dis-*` datatypes at `fpi_tools/fpi.py:40`, probe list at `fpi.py:27` |
| MMS HPCA, MMS1 | MMS HPCA | https://spase-metadata.org/SMWG/Instrument/MMS/1/HotPlasmaCompositionAnalyzer | `hpca_tools/mms_get_hpca_dist.py`, `mms_hpca_calc_anodes.py`, `mms_hpca_spin_sum.py`; probe list at `hpca_tools/hpca.py:33` |
| MMS FGM, MMS1 | MMS FIELDS/FGM | https://spase-metadata.org/SMWG/Instrument/MMS/1/FIELDS/FGM | `fgm_tools/mms_curl.py` (four-spacecraft curlometer, enforced at `mms_curl.py:47`) and `mms_lingradest.py:18`; probe list at `fgm_tools/fgm.py:29` |
| MMS FEEPS, MMS2 | MMS FEEPS | https://spase-metadata.org/SMWG/Instrument/MMS/2/EnergeticParticleDetector/FEEPS | `feeps_tools/` flat-field, energy-table and sun-contamination corrections plus PADs and spin averaging; probe list at `feeps_tools/feeps.py:56` |
| MMS EIS, MMS2 | MMS EIS | https://spase-metadata.org/SMWG/Instrument/MMS/2/EnergeticParticleDetector/EIS | `eis_tools/` omni spectra, PADs, spin averaging and cross-spacecraft spectrum combination; probe list at `eis_tools/eis.py:26` |
| MMS FPI (DES), MMS2 | MMS FPI/DES | https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DES | `fpi_tools/mms_get_fpi_dist.py`, `mms_load_fpi_calc_pad.py`, `particles/mms_part_des_photoelectrons.py`; `des-*` datatypes at `fpi_tools/fpi.py:40`, probe list at `fpi.py:27` |
| MMS FPI (DIS), MMS2 | MMS FPI/DIS | https://spase-metadata.org/SMWG/Instrument/MMS/2/FastPlasmaInstrument/DIS | `fpi_tools/mms_get_fpi_dist.py`, `mms_pad_fpi.py`, `mms_fpi_split_tensor.py`; `dis-*` datatypes at `fpi_tools/fpi.py:40`, probe list at `fpi.py:27` |
| MMS HPCA, MMS2 | MMS HPCA | https://spase-metadata.org/SMWG/Instrument/MMS/2/HotPlasmaCompositionAnalyzer | `hpca_tools/mms_get_hpca_dist.py`, `mms_hpca_calc_anodes.py`, `mms_hpca_spin_sum.py`; probe list at `hpca_tools/hpca.py:33` |
| MMS FGM, MMS2 | MMS FIELDS/FGM | https://spase-metadata.org/SMWG/Instrument/MMS/2/FIELDS/FGM | `fgm_tools/mms_curl.py` (four-spacecraft curlometer, enforced at `mms_curl.py:47`) and `mms_lingradest.py:18`; probe list at `fgm_tools/fgm.py:29` |
| MMS FEEPS, MMS3 | MMS FEEPS | https://spase-metadata.org/SMWG/Instrument/MMS/3/EnergeticParticleDetector/FEEPS | `feeps_tools/` flat-field, energy-table and sun-contamination corrections plus PADs and spin averaging; probe list at `feeps_tools/feeps.py:56` |
| MMS EIS, MMS3 | MMS EIS | https://spase-metadata.org/SMWG/Instrument/MMS/3/EnergeticParticleDetector/EIS | `eis_tools/` omni spectra, PADs, spin averaging and cross-spacecraft spectrum combination; probe list at `eis_tools/eis.py:26` |
| MMS FPI (DES), MMS3 | MMS FPI/DES | https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DES | `fpi_tools/mms_get_fpi_dist.py`, `mms_load_fpi_calc_pad.py`, `particles/mms_part_des_photoelectrons.py`; `des-*` datatypes at `fpi_tools/fpi.py:40`, probe list at `fpi.py:27` |
| MMS FPI (DIS), MMS3 | MMS FPI/DIS | https://spase-metadata.org/SMWG/Instrument/MMS/3/FastPlasmaInstrument/DIS | `fpi_tools/mms_get_fpi_dist.py`, `mms_pad_fpi.py`, `mms_fpi_split_tensor.py`; `dis-*` datatypes at `fpi_tools/fpi.py:40`, probe list at `fpi.py:27` |
| MMS HPCA, MMS3 | MMS HPCA | https://spase-metadata.org/SMWG/Instrument/MMS/3/HotPlasmaCompositionAnalyzer | `hpca_tools/mms_get_hpca_dist.py`, `mms_hpca_calc_anodes.py`, `mms_hpca_spin_sum.py`; probe list at `hpca_tools/hpca.py:33` |
| MMS FGM, MMS3 | MMS FIELDS/FGM | https://spase-metadata.org/SMWG/Instrument/MMS/3/FIELDS/FGM | `fgm_tools/mms_curl.py` (four-spacecraft curlometer, enforced at `mms_curl.py:47`) and `mms_lingradest.py:18`; probe list at `fgm_tools/fgm.py:29` |
| MMS FEEPS, MMS4 | MMS FEEPS | https://spase-metadata.org/SMWG/Instrument/MMS/4/EnergeticParticleDetector/FEEPS | `feeps_tools/` flat-field, energy-table and sun-contamination corrections plus PADs and spin averaging; probe list at `feeps_tools/feeps.py:56` |
| MMS EIS, MMS4 | MMS EIS | https://spase-metadata.org/SMWG/Instrument/MMS/4/EnergeticParticleDetector/EIS | `eis_tools/` omni spectra, PADs, spin averaging and cross-spacecraft spectrum combination; probe list at `eis_tools/eis.py:26` |
| MMS FPI (DES), MMS4 | MMS FPI/DES | https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DES | `fpi_tools/mms_get_fpi_dist.py`, `mms_load_fpi_calc_pad.py`, `particles/mms_part_des_photoelectrons.py`; `des-*` datatypes at `fpi_tools/fpi.py:40`, probe list at `fpi.py:27` |
| MMS FPI (DIS), MMS4 | MMS FPI/DIS | https://spase-metadata.org/SMWG/Instrument/MMS/4/FastPlasmaInstrument/DIS | `fpi_tools/mms_get_fpi_dist.py`, `mms_pad_fpi.py`, `mms_fpi_split_tensor.py`; `dis-*` datatypes at `fpi_tools/fpi.py:40`, probe list at `fpi.py:27` |
| MMS HPCA, MMS4 | MMS HPCA | https://spase-metadata.org/SMWG/Instrument/MMS/4/HotPlasmaCompositionAnalyzer | `hpca_tools/mms_get_hpca_dist.py`, `mms_hpca_calc_anodes.py`, `mms_hpca_spin_sum.py`; probe list at `hpca_tools/hpca.py:33` |
| MMS FGM, MMS4 | MMS FIELDS/FGM | https://spase-metadata.org/SMWG/Instrument/MMS/4/FIELDS/FGM | `fgm_tools/mms_curl.py` (four-spacecraft curlometer, enforced at `mms_curl.py:47`) and `mms_lingradest.py:18`; probe list at `fgm_tools/fgm.py:29` |
| THEMIS FGM, probe a | THEMIS-A Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/A/FGM | `spacecraft/fields/fgm.py:131` applies eclipse spin-model corrections, choosing spin-fit or waveform corrections per variable; `spacecraft/fields/fit.py:129` `cal_fit()` calibrates the onboard B spin fits |
| THEMIS EFI, probe a | THEMIS-A Electric Field Instrument | https://spase-metadata.org/SMWG/Instrument/THEMIS/A/EFI | `spacecraft/fields/efi.py:156` applies eclipse spin-model corrections with EFI-specific variable selection; `fit.py:129` `cal_fit()` applies boom-shortening and Ex offsets to the onboard E spin fits |
| THEMIS ESA, probe a | THEMIS-A Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/A/ESA | `spacecraft/particles/esa.py:108` applies vector and tensor eclipse corrections; `analysis/scpot2dens.py:106` and `scpot2dens_nishimura.py:8` derive density from ESA `peer`/`peir` quantities |
| THEMIS SST, probe a | THEMIS-A:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/A/SST | `spacecraft/particles/sst.py:132` applies vector and tensor eclipse corrections to L2 SST moments |
| THEMIS SCM, probe a | THEMIS-A: Search Coil Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/A/SCM | `spacecraft/fields/scm.py:109` applies waveform eclipse corrections, skipping `btotal` |
| THEMIS MOM, probe a | THEMIS-A:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature. | https://spase-metadata.org/SMWG/Instrument/THEMIS/A/MOM | `spacecraft/particles/mom.py:114` applies vector and tensor eclipse corrections to the onboard ESA+SST moments |
| THEMIS FGM, probe b | THEMIS-B Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/B/FGM | `spacecraft/fields/fgm.py:131` applies eclipse spin-model corrections, choosing spin-fit or waveform corrections per variable; `spacecraft/fields/fit.py:129` `cal_fit()` calibrates the onboard B spin fits |
| THEMIS EFI, probe b | THEMIS-B Electric Field Instrument | https://spase-metadata.org/SMWG/Instrument/THEMIS/B/EFI | `spacecraft/fields/efi.py:156` applies eclipse spin-model corrections with EFI-specific variable selection; `fit.py:129` `cal_fit()` applies boom-shortening and Ex offsets to the onboard E spin fits |
| THEMIS ESA, probe b | THEMIS-B Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/B/ESA | `spacecraft/particles/esa.py:108` applies vector and tensor eclipse corrections; `analysis/scpot2dens.py:106` and `scpot2dens_nishimura.py:8` derive density from ESA `peer`/`peir` quantities |
| THEMIS SST, probe b | THEMIS-B:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/B/SST | `spacecraft/particles/sst.py:132` applies vector and tensor eclipse corrections to L2 SST moments |
| THEMIS SCM, probe b | THEMIS-B: Search Coil Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/B/SCM | `spacecraft/fields/scm.py:109` applies waveform eclipse corrections, skipping `btotal` |
| THEMIS MOM, probe b | THEMIS-B:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature. | https://spase-metadata.org/SMWG/Instrument/THEMIS/B/MOM | `spacecraft/particles/mom.py:114` applies vector and tensor eclipse corrections to the onboard ESA+SST moments |
| THEMIS FGM, probe c | THEMIS-C Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/C/FGM | `spacecraft/fields/fgm.py:131` applies eclipse spin-model corrections, choosing spin-fit or waveform corrections per variable; `spacecraft/fields/fit.py:129` `cal_fit()` calibrates the onboard B spin fits |
| THEMIS EFI, probe c | THEMIS-C Electric Field Instrument | https://spase-metadata.org/SMWG/Instrument/THEMIS/C/EFI | `spacecraft/fields/efi.py:156` applies eclipse spin-model corrections with EFI-specific variable selection; `fit.py:129` `cal_fit()` applies boom-shortening and Ex offsets to the onboard E spin fits |
| THEMIS ESA, probe c | THEMIS-C Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/C/ESA | `spacecraft/particles/esa.py:108` applies vector and tensor eclipse corrections; `analysis/scpot2dens.py:106` and `scpot2dens_nishimura.py:8` derive density from ESA `peer`/`peir` quantities |
| THEMIS SST, probe c | THEMIS-C:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/C/SST | `spacecraft/particles/sst.py:132` applies vector and tensor eclipse corrections to L2 SST moments |
| THEMIS SCM, probe c | THEMIS-C: Search Coil Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/C/SCM | `spacecraft/fields/scm.py:109` applies waveform eclipse corrections, skipping `btotal` |
| THEMIS MOM, probe c | THEMIS-C:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature. | https://spase-metadata.org/SMWG/Instrument/THEMIS/C/MOM | `spacecraft/particles/mom.py:114` applies vector and tensor eclipse corrections to the onboard ESA+SST moments |
| THEMIS FGM, probe d | THEMIS-D Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/D/FGM | `spacecraft/fields/fgm.py:131` applies eclipse spin-model corrections, choosing spin-fit or waveform corrections per variable; `spacecraft/fields/fit.py:129` `cal_fit()` calibrates the onboard B spin fits |
| THEMIS EFI, probe d | THEMIS-D Electric Field Instrument | https://spase-metadata.org/SMWG/Instrument/THEMIS/D/EFI | `spacecraft/fields/efi.py:156` applies eclipse spin-model corrections with EFI-specific variable selection; `fit.py:129` `cal_fit()` applies boom-shortening and Ex offsets to the onboard E spin fits |
| THEMIS ESA, probe d | THEMIS-D Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/D/ESA | `spacecraft/particles/esa.py:108` applies vector and tensor eclipse corrections; `analysis/scpot2dens.py:106` and `scpot2dens_nishimura.py:8` derive density from ESA `peer`/`peir` quantities |
| THEMIS SST, probe d | THEMIS-D:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/D/SST | `spacecraft/particles/sst.py:132` applies vector and tensor eclipse corrections to L2 SST moments |
| THEMIS SCM, probe d | THEMIS-D: Search Coil Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/D/SCM | `spacecraft/fields/scm.py:109` applies waveform eclipse corrections, skipping `btotal` |
| THEMIS MOM, probe d | THEMIS-D:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature. | https://spase-metadata.org/SMWG/Instrument/THEMIS/D/MOM | `spacecraft/particles/mom.py:114` applies vector and tensor eclipse corrections to the onboard ESA+SST moments |
| THEMIS FGM, probe e | THEMIS-E Fluxgate Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/E/FGM | `spacecraft/fields/fgm.py:131` applies eclipse spin-model corrections, choosing spin-fit or waveform corrections per variable; `spacecraft/fields/fit.py:129` `cal_fit()` calibrates the onboard B spin fits |
| THEMIS EFI, probe e | THEMIS-E Electric Field Instrument | https://spase-metadata.org/SMWG/Instrument/THEMIS/E/EFI | `spacecraft/fields/efi.py:156` applies eclipse spin-model corrections with EFI-specific variable selection; `fit.py:129` `cal_fit()` applies boom-shortening and Ex offsets to the onboard E spin fits |
| THEMIS ESA, probe e | THEMIS-E Electrostatic Analyzers | https://spase-metadata.org/SMWG/Instrument/THEMIS/E/ESA | `spacecraft/particles/esa.py:108` applies vector and tensor eclipse corrections; `analysis/scpot2dens.py:106` and `scpot2dens_nishimura.py:8` derive density from ESA `peer`/`peir` quantities |
| THEMIS SST, probe e | THEMIS-E:  Solid State Telescope | https://spase-metadata.org/SMWG/Instrument/THEMIS/E/SST | `spacecraft/particles/sst.py:132` applies vector and tensor eclipse corrections to L2 SST moments |
| THEMIS SCM, probe e | THEMIS-E: Search Coil Magnetometer | https://spase-metadata.org/SMWG/Instrument/THEMIS/E/SCM | `spacecraft/fields/scm.py:109` applies waveform eclipse corrections, skipping `btotal` |
| THEMIS MOM, probe e | THEMIS-E:  On Board moments:  ESA and SST Electron/Ion moments density, flux, velocity, pressure and temperature. | https://spase-metadata.org/SMWG/Instrument/THEMIS/E/MOM | `spacecraft/particles/mom.py:114` applies vector and tensor eclipse corrections to the onboard ESA+SST moments |
| ELFIN EPD, ELFIN-A | The Electron Losses and Fields Investigation | https://spase-metadata.org/NASA/Instrument/ELFIN/A/EPD | `projects/elfin/epd/calibration_l1.py` and `calibration_l2.py`; the per-spacecraft table is selected at `calibration_l1.py:176` and both `ela_`/`elb_epde_cal_data.txt` ship in the wheel (`pyproject.toml:120`) |
| ELFIN EPD, ELFIN-B | The Electron Losses and Fields Investigation | https://spase-metadata.org/NASA/Instrument/ELFIN/B/EPD | `projects/elfin/epd/calibration_l1.py` and `calibration_l2.py`; the per-spacecraft table is selected at `calibration_l1.py:176` and both `ela_`/`elb_epde_cal_data.txt` ship in the wheel (`pyproject.toml:120`) |
| RBSPICE, Van Allen Probe A | RBSP RBSPICE | https://spase-metadata.org/SMWG/Instrument/RBSP/A/RBSPICE | `projects/rbsp/rbspice_lib/` omni spectra, spin averages and PADs, invoked from `rbspice.py:118`; probe set `['a','b']` at `rbspice.py:94` |
| RBSPICE, Van Allen Probe B | RBSP RBSPICE | https://spase-metadata.org/SMWG/Instrument/RBSP/B/RBSPICE | `projects/rbsp/rbspice_lib/` omni spectra, spin averages and PADs, invoked from `rbspice.py:118`; probe set `['a','b']` at `rbspice.py:94` |
| Cluster CIS, Rumba | Cluster Ion Spectrometry | https://spase-metadata.org/SMWG/Instrument/Cluster-Rumba/CIS | `projects/cluster/particle_tools/cluster_get_codif_dist.py` and `cluster_get_hia_dist.py` reconstruct CODIF and HIA distributions; per-species datatypes at `cis.py:42`, probe set at `cis.py:35` |
| Cluster CIS, Salsa | Cluster Ion Spectrometry | https://spase-metadata.org/SMWG/Instrument/Cluster-Salsa/CIS | `projects/cluster/particle_tools/cluster_get_codif_dist.py` and `cluster_get_hia_dist.py` reconstruct CODIF and HIA distributions; per-species datatypes at `cis.py:42`, probe set at `cis.py:35` |
| Cluster CIS, Samba | Cluster Ion Spectrometry | https://spase-metadata.org/SMWG/Instrument/Cluster-Samba/CIS | `projects/cluster/particle_tools/cluster_get_codif_dist.py` and `cluster_get_hia_dist.py` reconstruct CODIF and HIA distributions; per-species datatypes at `cis.py:42`, probe set at `cis.py:35` |
| Cluster CIS, Tango | Cluster Ion Spectrometry | https://spase-metadata.org/SMWG/Instrument/Cluster-Tango/CIS | `projects/cluster/particle_tools/cluster_get_codif_dist.py` and `cluster_get_hia_dist.py` reconstruct CODIF and HIA distributions; per-species datatypes at `cis.py:42`, probe set at `cis.py:35` |
| PSP FIELDS MAG | PSP FIELDS | https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/MAG | `projects/psp/filter.py` applies the FIELDS data-quality-flag artifact filter, exported at `psp/__init__.py:8` and exercised by `projects/psp/tests/test_psp.py`; `filter.py:105-108` restricts it to `fld_l2_mag_RTN` and `fld_l2_mag_SC` variables |
| PSP FIELDS RFS/LFR | PSP FIELDS | https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/RFS/LFR | `projects/psp/filter.py` as above; `filter.py:105-108` restricts it to `rfs_lfr` variables |
| PSP FIELDS RFS/HFR | PSP FIELDS | https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/RFS/HFR | `projects/psp/filter.py` as above; `filter.py:105-108` restricts it to `rfs_hfr` variables, and `test_psp.py` `test_l3_filtering` filters `psp_fld_l3_rfs_hfr_auto_averages_ch0_V1V2` |

**Evidence, by instrument group.**

- **MMS, probes 1–4.** The probe set is stated in the docstring of each instrument's loader in the
  form `list of probes, valid values for MMS probes are ['1','2','3','4']`
  (`feeps_tools/feeps.py:56`, `eis_tools/eis.py:26`, `fpi_tools/fpi.py:27`, `hpca_tools/hpca.py:33`,
  `fgm_tools/fgm.py:29`), and `fgm_tools/mms_curl.py:47` refuses field or position lists that are
  not exactly four elements, so the four-spacecraft expansion is read from the repository rather
  than assumed. FEEPS has the deepest chain: flat-field corrections, energy-table corrections,
  removal of sun-contaminated sectors using shipped masks (`feeps_tools/sun/*.csv`), bad-data
  removal, integral-channel splitting, pitch-angle and gyrophase distributions, spin averaging, and
  a per-probe active-eye table (`mms_feeps_active_eyes.py`). EIS adds omni-directional spectra,
  PADs, spin averaging and `mms_eis_spec_combine_sc.py`, which merges the omni spectra across
  spacecraft. FPI is split by SPASE into DES and DIS rows, and PySPEDAS processes both: `fpi.py:40`
  names the `des-*` and `dis-*` datatypes, `mms_get_fpi_dist.py` reconstructs the distributions,
  `mms_load_fpi_calc_pad.py` and `mms_pad_fpi.py` compute PADs, and
  `particles/mms_part_des_photoelectrons.py` applies the DES photoelectron model — DES-specific, and
  the reason the DES row is not merely a mirror of DIS. HPCA has distribution reconstruction, anode
  field-of-view sums and averages, energy tables, spin summing and `mms_pgs_split_hpca.py`; release
  2.1.4 fixed its multiply-charged He++ flux conversion. FGM carries the curlometer and the linear
  gradient estimator (`mms_lingradest.py:18` names `mms1_b_gse` … `mms4_b_gse`), plus flag removal
  and data splitting.
- **THEMIS, probes a–e.** `common/check_args.py:26` fixes the valid probe set as
  `{'a', 'b', 'c', 'd', 'e'}`, which is the artifact that licenses the five-way expansion. Each of
  the six listed instruments has its own eclipse spin-model correction logic, applied to that
  instrument's L2 variables with instrument-specific variable selection — SCM corrects waveforms and
  skips `btotal`; FGM distinguishes spin-fit from waveform corrections; ESA, SST and MOM route
  tensor quantities (`mftens`, `ptens`) to the tensor correction and vector quantities to the vector
  one. This is spin/attitude handling of a specific instrument's data, not a shared utility applied
  uniformly. `fields/fit.py:129` `cal_fit()` adds a genuine calibration chain — per-probe
  calibration tables, rotation vectors, boom-shortening factors, an Ex offset and a Bzoffset read
  from `th?_fgmcal.txt` — applied to the onboard spin fits of the FGM B field and the EFI E field,
  which is why it is cited as evidence for those two rows rather than as an instrument of its own
  (SPASE has no THEMIS FIT row). ESA carries additional processing of its own:
  `analysis/scpot2dens.py` and `scpot2dens_nishimura.py` derive electron density from ESA
  spacecraft potential, thermal velocity and density variables (`peer_sc_pot`, `peer_avgtemp`,
  `peer_vthermal`, `peer_density`, `peir_density`) using McFadden's and Nishimura's empirical
  relations, per probe.
- **ELFIN A and B.** `projects/elfin/epd/calibration_l1.py` and `calibration_l2.py` implement the
  EPD calibration chain, and `calibration_l1.py:176` selects the calibration table by spacecraft as
  `el{probe}_epde_cal_data.txt`. Both `ela_epde_cal_data.txt` and `elb_epde_cal_data.txt` are
  present in the package and shipped in the wheel (`pyproject.toml:120`), which is the artifact that
  names both spacecraft. `epd/postprocessing.py` builds the calibrated L1 and L2 products.
- **Van Allen Probes A and B.** `rbspice.py:94` fixes the probe set as `['a', 'b']`, and
  `rbspice.py:118` onward invokes `rbspice_lib/rbsp_rbspice_omni.py` and
  `rbsp_rbspice_spin_avg.py`, with `rbsp_rbspice_pad.py` and `rbsp_rbspice_pad_spinavg.py` available
  for pitch-angle distributions.
- **Cluster 1–4.** `projects/cluster/particle_tools/cluster_get_codif_dist.py` and
  `cluster_get_hia_dist.py` reconstruct distributions from the two CIS sensors, CODIF (per species:
  H+, He+, O+) and HIA; `cis.py:42` exposes the corresponding `psd_*` and `def_*` datatypes and
  `cis.py:35` fixes the probe set as `'1','2','3','4'`. The four CIS rows are namespaced by
  spacecraft name (Rumba, Salsa, Samba, Tango) rather than by number. No per-spacecraft
  number-to-name mapping was needed to select them: the repository supports all four probes, so the
  set of supported spacecraft is the complete set of four rows.
- **Parker Solar Probe FIELDS: MAG, RFS/LFR and RFS/HFR.** `projects/psp/filter.py` is a 333-line
  data-quality-flag artifact filter written specifically for PSP FIELDS. It is part of the public
  API (`psp/__init__.py:8` re-exports it as `filter_fields`) and is exercised by
  `projects/psp/tests/test_psp.py`, including `test_l3_filtering`. Its docstring enumerates the
  FIELDS quality-flag table — antenna bias sweep, PSP thruster firing, SCM calibration, MAG rolls,
  the FIELDS MAG calibration sequence, SWEAP SPC electron mode, the solar limb sensor test,
  off-umbra pointing, high-frequency noise affecting the RFS and TDS receivers, and antennas driven
  towards the FIELDS power-supply rails — and applies them as a bitmask with keep-versus-reject
  semantics, writing new flag-tagged tplot variables. The three-row expansion is read from the
  repository rather than assumed: `filter.py:105-108` reduces the input to variables matching
  `fld_l2_mag_RTN`, `fld_l2_mag_SC`, `rfs_lfr` and `rfs_hfr`, which names the FIELDS magnetometer
  and the two Radio Frequency Spectrometer receivers and nothing else in the suite. All three rows
  carry the display name `PSP FIELDS`, which is expected here for the same reason it is expected for
  MMS and Cluster: the identifier distinguishes them.
  **The suite-level row was considered and not selected.**
  `https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS` exists, is of instrument type
  and is also named `PSP FIELDS`; it would have been the coarser choice. The repository's explicit
  variable list picks out three sub-instruments, so the three sub-instrument rows are the accurate
  association and the suite row would over-claim. The suite's other rows — `DFB`, `SCM`,
  `FIELDS2/TDS` and `V1` through `V5` — are likewise not recorded, because `filter.py` does not name
  their variables. `test_psp.py` does call `filter_fields` on DFB variables
  (`psp_fld_l2_dfb_dc_spec_dV12hg`, `psp_fld_l2_dfb_ac_xspec_power_ch1_SCMdlfhg`), but those calls
  fall through the same line-105 filter and return without creating anything, so they are not
  evidence that DFB data is processed.
  This entry sits on the same side of the boundary as `mms/fgm_tools/mms_fgm_remove_flags.py`, which
  is already cited as processing evidence for the four MMS FGM rows. Both are instrument-specific
  artifact removal driven by the instrument's own quality flags, and the PSP module is the more
  substantial of the two: a ten-flag bitmask table with keep-versus-reject semantics, against a
  single `flags != 0.0` cut applied to four B-field variables.

**Instruments PySPEDAS processes that could not be recorded here.** These are resolution outcomes,
not relevance judgements — the software genuinely processes this data.

- **ERG/Arase MEP-e, MEP-i, LEP-e, LEP-i, HEP and XEP.** This is the largest gap. PySPEDAS carries a
  full particle package for these instruments in
  `projects/erg/satellite/erg/particle/` — `erg_*_get_dist.py` distribution reconstruction,
  `erg_*_part_products.py` spectra and moments, `erg_pgs_do_fac.py` field-aligned coordinates,
  `erg_convert_flux_units.py`, and instrument-specific pointing geometry in
  `get_mepe_az_dir_in_sga.py`, `get_mepe_flux_angle_in_sga.py`, `get_mepi_flux_angle_in_sga.py` and
  `get_lepi_flux_angle_in_sga.py`. The vocabulary contains no ERG or Arase instrument row of any
  kind: the mission appears in the vocabulary only as observatory rows, one of which is already
  recorded in Field 32. The mission-level association therefore stands in for the instrument-level
  one, and a future agent
  should re-check the vocabulary rather than assume this gap is permanent.
- **MMS MEC.** `cotrans/mms_qcotrans.py` and `mms_cotrans_qtransformer.py` rotate vectors using the
  MEC quaternions `mms{probe}_mec_quat_eci_to_{coord}`, `mms_cotrans_lmn.py` builds the
  boundary-normal frame from `mms{probe}_mec_r_gsm`, and `mec_ascii/` parses the MMS ancillary
  attitude and ephemeris products and computes the tetrahedron quality factor. No vocabulary row is
  named MEC. The nearest candidate is the per-probe `SMWG/Instrument/MMS/<n>/Ephemeris` row named
  `MMS Positions`, which denotes spacecraft position rather than the MEC product; selecting it would
  be an inference rather than a match, so the MMS observatory association in Field 32 carries this
  instead.
- **Ephemeris, state and probe-status rows generally.** The same reasoning applies to
  `SMWG/Instrument/THEMIS/<p>/Ephemeris` (`THEMIS-A Probe Status` and its siblings),
  `SMWG/Instrument/RBSP/<p>/Ephemeris` (`RBSP Positions`), the Cluster `Ephemeris` rows and the
  ELFIN `Ephemeris` rows. PySPEDAS does real processing of mission state data — the THEMIS spin
  model in `themis/state_tools/spinmodel/` and the spin-axis attitude corrections in
  `state_tools/apply_spinaxis_corrections.py` are substantial — but these rows describe spacecraft
  position and status rather than a science instrument, and that processing is already the reason
  each THEMIS science instrument above is listed. Treating them uniformly keeps the boundary
  legible.
- **THEMIS FIT and GMOM.** Both have dedicated processing (`fields/fit.py` `cal_fit()`;
  `particles/gmom.py` eclipse corrections for the ground-computed moments) and neither has a
  vocabulary row. Their evidence is folded into the FGM, EFI and MOM rows, whose data they process.
- **ISEE VLF/ELF receivers (ERG ground).** A ground instrument that does pass the boundary:
  `erg/ground/vlf/isee_vlf.py` applies a genuine gain calibration when its documented `cal_gain`
  keyword is set (`isee_vlf.py:82`). Lines 190–225 read `amplitude_cal_vlf_ch1` and
  `amplitude_cal_vlf_ch2` from the CDF, interpolate them onto `freq_vlf`, divide by the resulting
  gain curves, and re-store the ch1 and ch2 variables. Calibration is the first item in the
  boundary rule above, so this instrument is inside it. It is omitted for a resolution reason
  instead: the vocabulary has no parent ISEE VLF instrument row, only fifteen per-station antenna
  rows under `IUGONET/Instrument/ISEE/VLF_ELF/<STATION>/…`, and the module's seven site codes
  (`ath`, `gak`, `hus`, `ist`, `kap`, `mam`, `nai` at `isee_vlf.py:101`) do not map cleanly onto
  them. `ath`, `gak`, `hus`, `kap` and `nai` match a `VLF_ELF_crs` row by station code. `ist` and
  `mam` match no row by code: their plausible candidates are `ITK` ("VLF/ELF crossed loop antenna at
  Istok") and `KMH` ("VLF/ELF valley antenna at Maenohama, Kagoshima, Japan."), each of which has to
  be inferred from the row's prose description rather than read off the code, which is the kind of
  inference this record does not make. Recording five of the seven would misstate the module's
  coverage, so this follows the same station-level scale decision already recorded in Field 32 for
  the ERG/ISEE ground networks as a whole. If per-station granularity is ever adopted for ground
  networks, the five code-matched rows are the defensible starting set, and `ist` and `mam` need the
  station identification confirmed upstream before they can be bound.
  One nearby module that looks similar and is not: `erg/ground/geomag/gmag_isee_induction.py` reads
  the ISEE induction magnetometers' `sensitivity` and `phase_difference` tables when
  `frequency_dependent=True`, but it returns that structure to the caller rather than applying it,
  so it is a calibration-table reader and stays outside the boundary.

**Instruments considered and deliberately not recorded, because they fall outside the boundary.**
Each of these is loaded by PySPEDAS and is covered at mission level in Field 32; recording the
reasoning so a later refresh does not re-propose them without new evidence.

- **MMS SCM, EDP, EDI, ASPOC, DSP and FSM.** Each has a loader plus, in most cases, a
  `*_set_metadata.py` that assigns plot labels and colours. `scm_tools/scm.py` additionally labels
  the output coordinate system by data level. Assigning metadata is not processing.
- **THEMIS FBK, FFT and ESD.** Load routines with no post-load processing; unlike their eight
  siblings under `spacecraft/` (FGM, EFI, FIT, SCM, ESA, GMOM, MOM and SST, the modules that call
  `apply_eclipse_corrections`), none of these three applies eclipse corrections.
- **RBSP EFW, EMFISIS, HOPE, MagEIS, REPT, RPS and MagEphem.** Each `return load(...)` directly.
  RBSPICE is the only Van Allen Probes instrument with a processing library.
- **Cluster ASPOC, DWP, EDI, EFW, FGM, PEACE, RAPID, STAFF, WBD and WHISPER.** Load routines only;
  CIS is the only Cluster instrument with distribution code.
- **NOAA POES and MetOp SEM-2.** `projects/poes/sem.py` is a six-line loader alias, and
  `projects/poes/load.py` assembles archive paths generically. SEM-2 rows do exist in the
  vocabulary — `SMWG/Instrument/NOAA/<15–19>/SEM-2` and `SMWG/Instrument/MetOp/<A,B>/SEM-2`, the
  latter pair both correctly named `Space Environmental Monitor-2` even though the `MetOp/B`
  observatory row is not — so this is a boundary exclusion, not a resolution failure.
- **MAVEN IUVS.** `projects/maven/read_iuvs_file.py` is a substantial bespoke parser for the IUVS
  key-parameter blocks, and rows exist (`SMWG/Instrument/MAVEN/IUVS`, with an `.html` twin). It is
  excluded because a bespoke format reader is still a load path, however long, rather than
  scientific processing of the measurement. The same reasoning excludes
  `projects/akebono/rdm_postprocessing.py`, which parses a fixed-column RDM text file and assigns
  plot labels.
- **THEMIS ground all-sky imagers and ground magnetometers.** `themis/ground/ask.py` and `gmag.py`
  are load routines — `ask.py` is a single `def ask()`, and `gmag.py` is a loader plus station-list
  helpers — and PySPEDAS does no keogram construction, calibration or image processing on that data.
  Because no THEMIS ground instrument passes the boundary, the CARISMA ambiguity that affects the
  ground networks in Field 32 does not arise here. This is a statement about the THEMIS ground tree
  only, not about ground instruments generally — the ISEE VLF/ELF receivers above do pass the
  boundary and are omitted for a different reason.
- **SuperDARN radars (ERG ground).** `erg/ground/radar/superdarn/sd_fit.py` is substantial — about
  910 lines — and it does more than call `load()`: `get_pixel_cntr()` derives radar-cell centre
  coordinates from the corner table shipped in the data file, using the spherical averaging in
  `get_sphcntr.py` (`astropy.coordinates.cartesian_to_spherical`), and the routine then splits the
  per-beam variables, separates ionospheric from ground-scatter echoes, clips at ±9000, converts
  fill values to NaN and reassigns scan numbers. On balance this is judged to fall outside the
  boundary and is deliberately not recorded, so that a later refresh does not re-open it without new
  evidence. The reasoning: the boundary is drawn around transformations of the measured quantity —
  calibration, moments, spectra, pitch-angle distributions, distribution reconstruction or slicing,
  spin and attitude correction, instrument-specific artifact correction — and `sd_fit.py` performs
  none of those on the Doppler velocities themselves. Its geolocation output is derived positional
  metadata; its three "components" are slices of an array dimension the CDF already carries
  (`sd_fit.py:454` onward indexes `[:, :, 0]`, `[:, :, 1]`, `[:, :, 2]`), not a computed rotation;
  and its ionospheric/ground-scatter separation is a different operation from the artifact removal
  that puts PSP FIELDS and MMS FGM inside the boundary. Those two discard instrument-flagged bad
  data: `psp/filter.py` and `mms/fgm_tools/mms_fgm_remove_flags.py` each overwrite the flagged
  samples with NaN and leave the surviving measurements as the product. `sd_fit.py` instead keeps
  the measurements and partitions them by physical scatter type, testing the `echo_flag` variable
  the data file supplies (`sd_fit.py:520,523`) to write complementary `*_iscat_` and `*_gscat_`
  variables plus a combined `*_bothscat_`. PySPEDAS does encode that flag's meaning, so the
  distinction is not that one side carries flag semantics and the other does not; it is that
  sorting valid data into physical categories labels the measurement rather than correcting it.
  An unambiguous row exists should that judgement ever be revisited on new evidence: the name
  `SuperDARN Radars` matches exactly one instrument-type row, `https://spase-metadata.org/SMWG/Instrument/SuperDARN/Radars`. SuperDARN's
  support is in any case already recorded at network level in Field 32.
- **Placeholder post-processing hooks are not evidence of processing.** `soho/celias_postprocessing.py`,
  `costep_postprocessing.py` and `erne_postprocessing.py`, and `akebono/pws_postprocessing.py`, all
  contain a docstring reading "Placeholder for … post-processing" and return their input unchanged.
  A file named `*_postprocessing.py` must be opened before it is counted.

**Identifier form.** All 65 identifiers above are `https://spase-metadata.org/` identifiers of
instrument type, each in the bare form rather than an `.html` twin. That is a property of the rows
used here, not a guarantee about the vocabulary: a row that fails any of those three tests indicates
upstream drift or a row wrongly created by a submission, and must be reported rather than used.

**Why this field was previously empty, and why that is superseded.** The prior revision left Field 31
empty on granularity grounds, arguing that instrument-comprehensive support would multiply out to
several hundred entries and that a partial list would falsely imply the unlisted instruments were
unsupported. The first half of that argument was sound and is answered by the processing-code
boundary above, which is a principled cut rather than a sample; the second half is answered by
stating the boundary explicitly here and in Field 32. An earlier revision still gave a different
reason — that none of 156 extracted instrument labels matched a 27-entry HSSI instrument vocabulary.
That reason was already obsolete when it was removed: the instrument vocabulary is far larger than
that, and it is keyed on SPASE identifiers.

### 32. Related Observatories (OPTIONAL)

Forty-two observatories are recorded, in the three tables below. Every entry carries a SPASE
identifier; none is free-typed. Every value already stored is retained — this is a union, and
nothing is removed.

**Currently recorded (30).** Names are copied exactly as stored.

| Name | SPASE identifier |
|---|---|
| Acceleration, Reconnection, Turbulence, Electrodynamics of the Moon’s Interaction with the Sun | https://spase-metadata.org/SMWG/Observatory/ARTEMIS |
| Advanced Composition Explorer | https://spase-metadata.org/SMWG/Observatory/ACE |
| AKEBONO | https://spase-metadata.org/SMWG/Observatory/Akebono |
| Balloon Array for Radiation-belt Relativistic Electron Losses | https://spase-metadata.org/SMWG/Observatory/BARREL |
| Cluster | https://spase-metadata.org/SMWG/Observatory/Cluster |
| Communication/Navigation Outage Forecasting System | https://spase-metadata.org/SMWG/Observatory/CNOFS |
| Deep Space Climate Observatory, DSCOVR | https://spase-metadata.org/SMWG/Observatory/DSCOVR |
| Electron Losses and Fields Investigation A, CubeSat | https://spase-metadata.org/SMWG/Observatory/ELFIN/A |
| Electron Losses and Fields Investigation B, CubeSat | https://spase-metadata.org/SMWG/Observatory/ELFIN/B |
| Exploration of energization and Radiation in Geospace (ERG), now known as Arase | https://spase-metadata.org/SMWG/Observatory/ARASE.html |
| Fast Auroral Snapshot | https://spase-metadata.org/SMWG/Observatory/FAST |
| Geomagnetic Tail Lab | https://spase-metadata.org/SMWG/Observatory/Geotail |
| Geostationary Operational Environmental Satellites | https://spase-metadata.org/SMWG/Observatory/GOES |
| Imager for Magnetopause-to-Aurora Global Exploration | https://spase-metadata.org/SMWG/Observatory/IMAGE |
| International Solar Polar Mission | https://spase-metadata.org/SMWG/Observatory/Ulysses |
| Ionospheric Connection | https://spase-metadata.org/SMWG/Observatory/ICON |
| ISTP/Wind | https://spase-metadata.org/SMWG/Observatory/Wind |
| KOMPSAT | https://spase-metadata.org/SMWG/Observatory/KOMPSAT1.html |
| Magnetosphere-Ionosphere Coupling in the Alfvén resonator (MICA) mission | https://spase-metadata.org/SMWG/Observatory/MICA.html |
| Magnetospheric Multiscale | https://spase-metadata.org/SMWG/Observatory/MMS |
| Mars Atmosphere and Volatile EvolutioN | https://spase-metadata.org/SMWG/Observatory/MAVEN |
| Parker Solar Probe | https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe |
| Polar-orbiting Operational Environmental Satellite (POES) | https://spase-metadata.org/SMWG/Observatory/POES.html |
| Solar and Heliospheric Observatory | https://spase-metadata.org/SMWG/Observatory/SOHO |
| Solar Orbiter | https://spase-metadata.org/ESA/Observatory/SolarOrbiter |
| Solar-Terrestrial Relations Observatory | https://spase-metadata.org/SMWG/Observatory/STEREO |
| SuperMAG | https://spase-metadata.org/SMWG/Observatory/SuperMAG |
| Swarm | https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SWARM.html |
| Time History of Events and Macroscale Interactions during Substorms | https://spase-metadata.org/SMWG/Observatory/THEMIS |
| Van Allen Probes | https://spase-metadata.org/SMWG/Observatory/RBSP |

Notes on the stored set:

- Each of these corresponds to a `pyspedas/projects/<name>/` subpackage except ARTEMIS, SuperMAG and
  ICON, which rest on a documented capability instead and are covered here and in the next note.
  ARTEMIS is the lunar-orbit portion of THEMIS served by `projects/themis/` and its
  `gse2sse`/`sse2sel` transforms, and SuperMAG ground magnetometer data is retrieved through the
  HAPI client (`hapi_tools/tests/test_hapi_supermag.py` exercises it).
- ICON is supported through the generic CDAWeb path rather than a dedicated module, but with
  ICON-specific handling: `tplot_tools/importers/netcdf_to_tplot.py` carries explicit workarounds for
  ICON's non-standard units strings and its string fill values.
- ELFIN correctly appears as two entries because the vocabulary has no mission-level ELFIN row, only
  the per-spacecraft A and B rows. That is not inconsistent with the mission-level granularity used
  elsewhere; it is the only option the vocabulary offers.
- Five entries use an identifier ending in `.html` that has a bare twin naming the same resource:
  `ARASE.html` / `ARASE` ("Exploration of energization and Radiation in Geospace"),
  `KOMPSAT1.html` / `KOMPSAT1` ("Korean Multi-Purpose Satellite"), `MICA.html` / `MICA`,
  `POES.html` / `POES`, and `CDPP-AMDA/SWARM.html` / `CDPP-AMDA/SWARM` ("Swarm : ESA mission"). The
  convention is to prefer the bare form, so these are duplicates worth consolidating in the
  vocabulary itself. The five `.html` identifiers are nevertheless the ones recorded here, because
  swapping them for their twins would mean removing settled associations to gain nothing
  functionally.
- Swarm resolves through a CNES/AMDA row rather than an SMWG one because no `SMWG/Observatory/Swarm`
  row exists. A single non-SMWG match is a correct outcome.

**Recorded from repository evidence, with no prior stored association (10).** Each names a
capability in the repository, and each resolves to exactly one appropriate row. Nine are `pyspedas/projects/<name>/`
subpackages; SuperDARN is not — it is a ground-radar module inside the ERG project
(`projects/erg/ground/radar/superdarn/`).

| Name (verbatim from the vocabulary) | SPASE identifier | Repository evidence |
|---|---|---|
| Colorado Student Space Weather Experiment | https://spase-metadata.org/SMWG/Observatory/CubeSat/CSSWE | `pyspedas/projects/csswe/` with the `reptile.py` REPTile load routine |
| Dynamics Explorer-B | https://spase-metadata.org/SMWG/Observatory/DynamicsExplorer2 | `pyspedas/projects/de2/load.py`, instruments `mag`, `nacs`, `rpa`, `idm`, `wats`, `vefi`, `lang` |
| ISTP/Equator-S | https://spase-metadata.org/SMWG/Observatory/Equator-S | `pyspedas/projects/equator_s/` |
| LANL Spacecraft Series | https://spase-metadata.org/SMWG/Observatory/LANL | `pyspedas/projects/lanl/` with `mpa.py` and `spa.py` |
| OMNI | https://spase-metadata.org/SMWG/Observatory/OMNI | `pyspedas/projects/omni/load.py` and `omni_solarwind_load.py`; also the automatic driver source for the Tsyganenko models |
| Polar | https://spase-metadata.org/SMWG/Observatory/POLAR | `pyspedas/projects/polar/` with eleven instrument routines plus orbit data |
| Spherical Elementary Current Systems | https://spase-metadata.org/SMWG/Observatory/SECS | `pyspedas/projects/secs/` (EICS/SECS load, read and plot) |
| ST5 Mission | https://spase-metadata.org/SMWG/Observatory/ST5 | `pyspedas/projects/st5/mag.py` |
| SuperDARN | https://spase-metadata.org/SMWG/Observatory/SuperDARN | `pyspedas/projects/erg/ground/radar/superdarn/sd_fit.py` |
| Two Wide-angle Imaging Neutral Atom Spectrometers | https://spase-metadata.org/SMWG/Observatory/TWINS | `pyspedas/projects/twins/` (`imager.py`, `lad.py`, `ephemeris.py`) |

Resolution notes for those ten:

- **Dynamics Explorer-B** was chosen over the sibling rows `Dynamics Explorer` (the programme) and
  `Dynamics Explorer-A`: the module is DE-2, and DE-2 is the spacecraft the `DynamicsExplorer2`
  identifier denotes.
- **Polar** matches exactly one row by name; the similarly-named `Polar Plasma Laboratory`
  (`CNES/Observatory/CDPP-AMDA/POLAR`) is a different row with a different name and was not selected.
- **OMNI** has two same-named rows, `SMWG/Observatory/OMNI` and `CNES/Observatory/CDPP-AMDA/OMNI`;
  the SMWG row is preferred, which is the documented tie-breaker for same-name duplicates. OMNI is
  listed here even though `OMNIWeb` already appears under Data Sources, because the two are different
  things: OMNIWeb is the service, and the SPASE OMNI row is the virtual observatory whose merged
  record PySPEDAS has a dedicated module for and depends on to drive its magnetic field models.
- **ST5 Mission** and **Two Wide-angle Imaging Neutral Atom Spectrometers** were chosen at mission
  level even though per-spacecraft rows exist and the repository names the individual spacecraft
  (`st5/mag.py` accepts probes `094`, `224`, `155`; `twins/load.py` accepts probes `1` and `2`). The
  three ST5 rows are named by international designator (`2006-008A`, `2006-008B`, `2006-008C`), which
  is opaque to a reader, and expanding either mission to per-spacecraft rows would be inconsistent
  with the mission-level treatment this record uses for GOES, Cluster, THEMIS and Van Allen Probes,
  all of which also have per-spacecraft rows available.
- **LANL Spacecraft Series** was chosen over the per-satellite rows for a stronger reason than
  consistency: `projects/lanl/load.py` maps its probe keys to satellites 89, 90, 91, 94, 97, 01a and
  02a, and the vocabulary's per-satellite rows for those are internally contradictory — `LANL-97`
  points at `/LANL/97A` while `LANL-97A` points at `/LANL/1997`, and `LANL01A` and `LANL-01A`
  likewise disagree. The series row is unambiguous. Note also that the similarly-named
  `IGPPLANL` rows are a *ground magnetometer chain*, unrelated to the LANL geosynchronous spacecraft
  this module loads, and must not be substituted for them.
- **SuperDARN** is recorded at network level. `sd_fit.py` ships an explicit `valid_sites` list, but
  the vocabulary offers a clean network observatory row plus only three IUGONET station
  *observatory* rows (Hokkaido East, Hokkaido West, King Salmon), so station-level expansion would
  be both incomplete and disproportionate. SuperDARN rows of instrument type also exist — the
  per-station IUGONET HF radar rows, including two SENSU Syowa rows under NIPR, and
  `SMWG/Instrument/SuperDARN/Radars` — but this field records observatories, and the network row is
  the right granularity for a module that loads any of the network's sites.

**MetOp (2).** PySPEDAS supports the MetOp spacecraft through its POES module:
`projects/poes/load.py` documents `metop1` and `metop2` among its probe values alongside the NOAA
POES spacecraft, `projects/poes/tests/test_poes.py` loads both and asserts that the retrieved files'
`Source_name` global attribute reads `MetOp1` and `MetOp2`, and `projects/poes/config.py` points at
NCEI's `poes-metop-space-environment-monitor` archive. Both MetOp rows the vocabulary offers are
recorded, so that support is discoverable rather than silently dropped.

| Name (verbatim from the vocabulary) | SPASE identifier |
|---|---|
| MetOp-A | https://spase-metadata.org/SMWG/Observatory/MetOp/A |
| MetOp-A | https://spase-metadata.org/SMWG/Observatory/MetOp/B |

- **The duplicated name is correct here, and must not be "fixed".** These are two distinct
  spacecraft under two distinct, correct identifiers, and the identifier — not the display name — is
  what links the record. The `MetOp/B` row nevertheless carries the name `MetOp-A`, and that is an
  upstream SPASE defect that HSSI mirrors faithfully rather than an import error: fetching
  `https://spase-metadata.org/SMWG/Observatory/MetOp/B.json` returns
  `ResourceID: spase://SMWG/Observatory/MetOp/B` together with `ResourceName: MetOp-A`. Copying the
  name verbatim is therefore the correct behaviour, and the two identically-labelled entries are
  expected. The repair belongs upstream in SPASE, not in this record.
- **Why the record does not distinguish MetOp-A from MetOp-B by number.** The repository names MetOp
  spacecraft numerically and never states the letter correspondence. Besides `metop1` and `metop2`,
  the NCEI L1B tests in `projects/poes/tests/test_poes.py` exercise `probe=['metop03']` and
  `probe=['metop3']`, and `projects/poes/load.py` does not validate probe strings at all — the L1B
  path is assembled generically from a regex digit match as `prb_name + num.zfill(2)`, so any
  `metopN` is accepted. Recording both rows sidesteps a number-to-letter mapping that the repository
  does not supply.
- **Durable negative research: there is no MetOp-C.** No row in the vocabulary is named MetOp-C, and
  no third row exists under `SMWG/Observatory/MetOp/`, so the `metop3`/`metop03` probes exercised in
  the POES tests have no candidate row at all. That is a gap in the vocabulary, not an omission in
  this record.

**Documented omissions.** These are things PySPEDAS touches that were considered and deliberately not
recorded here; the reasoning is kept so the same candidates are not re-proposed.

- **World Data Center for Geomagnetism, Kyoto** — `projects/kyoto/load_dst.py`, `load_ae.py` and
  `load_geomagnetic_indices.py` download the Dst and AE indices from
  `https://wdc.kugi.kyoto-u.ac.jp/`. These are derived global indices rather than one observatory's
  measurements, and the vocabulary carries no WDC-Kyoto parent row — only several hundred
  station-level rows under `IUGONET/Observatory/WDC_Kyoto/WDC/<code>` (523 as of
  2026-08-11), none of which PySPEDAS names. The
  relationship is captured instead by selecting `WDC` in Data Sources (Field 17). One caveat for
  anyone re-checking that figure: counting the whole `IUGONET/Observatory/WDC_Kyoto/` prefix instead
  of the `/WDC/` sub-prefix returns five additional rows, but they sit under
  `IUGONET/Observatory/WDC_Kyoto/Micro-barometic.observation/` (spelled that way upstream) and are
  barometric and infrasound sensor sites, not geomagnetic stations.
- **NOAA/GFZ planetary indices (`projects/noaa/`)** — `noaa_load_kp.py` retrieves the Kp index and
  the series published alongside it (ap, Kp_Sum, ap_Mean, Cp, C9, Sunspot_Number, F10.7) from NOAA
  and, for years from 2018 onward, from GFZ Potsdam. The reasoning is
  the same as for the Kyoto indices: these are derived global indices rather than one observatory's
  measurements, and the relationship is captured by the `GFZ` value in Data Sources (Field 17)
  rather than by an observatory association. With this omission recorded, each of the 37
  `pyspedas/projects/` subpackages maps either to an observatory recorded above or to a documented
  omission in this list.
- **Ground magnetometer partner networks reached through the THEMIS archive** —
  `projects/themis/ground/gmag.py` ships convenience station lists grouped by network (THEMIS GBO,
  TGO, DTU, University of Alaska, MACCS, USGS, Athabasca, THEMIS EPO, Falcon, McMAC, NRCan, STEP,
  FMI, AARI, CARISMA, and the USGS/EarthScope variometer sites), but every one of them is fetched
  from the THEMIS ground-based observatory tree (`thg/l2/...`) on the THEMIS data server. The
  THEMIS association already recorded covers that. The site lists name more than 200 station codes in total, so
  expanding to station level would swamp the record, and one of the candidate network rows cannot be resolved anyway: CARISMA has two
  distinct SMWG rows with the same name, `SMWG/Observatory/Ground/CARISMA` and
  `SMWG/Observatory/CARISMA`, with nothing to choose between them.
- **ERG/ISEE ground-network stations** — `projects/erg/ground/` loads the ISEE fluxgate and induction
  magnetometers, the MM210 chain, MAGDAS, the OMTI all-sky imagers, the ISEE riometers and the ISEE
  VLF receivers. The vocabulary has no parent row for any of these networks, only per-station rows
  under `IUGONET/Observatory/ISEE/...` and `IUGONET/Observatory/ICSWSE/MAGDAS/...`; recording them
  would mean adding well over a hundred station entries. Recorded here so the absence is understood
  as a scale decision rather than an oversight.
- **INTERMAGNET** — an earlier revision of this record listed INTERMAGNET among the observatories
  PySPEDAS supports. That is not correct: the only occurrences in the repository are in the
  acknowledgement text reproduced by the Kyoto Dst loader and its README. A row does exist
  (`https://spase-metadata.org/SMWG/Observatory/Ground/INTERMAGNET`), so this is a relevance
  exclusion, not a resolution failure.
- **IUGONET** — likewise previously listed. The current source tree contains no reference to IUGONET
  at all; the term reaches the project only through a `CITATION.cff` keyword. The ERG ground datasets
  are IUGONET-registered, but PySPEDAS retrieves them from ISEE/Nagoya endpoints, and no
  IUGONET-level observatory row exists.
- **EarthScope magnetotelluric network (`pyspedas/mth5/`)** — `load_fdsn.py` builds an MTH5 file from
  the EarthScope FDSN service (`client="EARTHSCOPE"`, formerly IRIS). No observatory row exists for
  the EarthScope/IRIS seismological and magnetotelluric network. A serious trap to avoid: the
  vocabulary *does* contain a row at `https://spase-metadata.org/SMWG/Observatory/IRIS` named
  `Interface Region Imaging Spectrograph`, which is NASA's solar mission and has nothing to do with
  this data source. It must never be used here. Note that searching the observatory rows for the
  name or abbreviation `IRIS` finds nothing — that row's name is the spelled-out form and its
  abbreviation field is empty — so a future agent who searches by the short name and comes up empty
  should not conclude that this caveat is stale.
- **Voyager** — appears only as the worked example in the CDAWeb browser tutorial
  (`docs/source/cdaweb.rst` and `cdagui_tools/tests/test_cdagui.py`). A tutorial name-drop of the
  generic CDAWeb interface is not mission support.
- **Individual GOES, NOAA POES, Cluster, MMS, THEMIS and Van Allen Probes spacecraft** — per-satellite
  observatory rows exist for all of these, but this field associates at mission level, so they are
  not expanded. Field 31 does use per-spacecraft granularity, because SPASE namespaces science
  instruments beneath their spacecraft rather than at mission level; the two fields differ on
  purpose, and neither is drifting from the other. (The one mission-level row under
  `SMWG/Instrument/Cluster/` is `JSOC`, the Cluster Joint Science Operations Centre, which is an
  operations centre carried as an instrument-type row rather than a science instrument, and is not
  a mission-level alternative to the four CIS rows in Field 31.)

### 33. Logo (OPTIONAL)
Not found. The repository contains no logo image: the images in `docs/source/_static/` are example plots and
IDE screenshots, `docs/source/conf.py` sets neither `html_logo` nor a favicon, and there is no
project image at the repository root. The PyHC core registry entry for pySPEDAS has no `logo` field,
even though the registry schema supports one and other core entries populate it. The wider SPEDAS project maintains a site at
`https://spedas.org/wiki/`, but no stable, publicly-addressable logo image URL was found there.
Re-checked at the pinned revision; nothing has been added.
