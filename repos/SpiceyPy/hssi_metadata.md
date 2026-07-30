# HSSI Metadata Extraction Results

**HSSI Software ID:** d0dcf8b7-d032-481b-b80e-dea683cc1fa4
**Repository:** https://github.com/AndrewAnnex/SpiceyPy
**Source Revision:** 388c219808f5b0dc9ec10acee2ca1b3cbe3c6e47
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-07-30
**Validation Status:** PASS

**Extraction mode:** Seeded refresh from the live HSSI record retrieved 2026-07-29. No prior
`hssi_metadata.md` existed for this entry. Every controlled-list value below was confirmed against
the live HSSI vocabulary.

**Provenance legend used in the notes below:**
- `[HSSI]` — carried over from the existing live HSSI record (submitted value, preserved)
- `[NEW]` — field was empty on HSSI; filled from repository/authoritative evidence
- `[CHANGED]` — an existing HSSI value replaced or extended; every one carries its evidence

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Not part of the stored software record; placeholder is expected for a refresh.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.593914

`[HSSI]` Unchanged. Confirmed independently: this is the Zenodo **concept** DOI
(`conceptdoi` / `conceptrecid` 593914 on the Zenodo record for v8.2.0) and it is listed in
`CITATION.cff` under `identifiers` with description "Zenodo archive".

### 3. Code Repository (MANDATORY)
https://github.com/AndrewAnnex/SpiceyPy

`[HSSI]` Unchanged. Confirmed against `pyproject.toml` `[project.urls]` (Homepage / Repository /
Source), `CITATION.cff` `repository-code`, the PyHC community registry `code` field, and the live
GitHub API (not archived, default branch `main`, last push 2026-07-26).

### 4. Software Functionality (MANDATORY)

`[CHANGED]` HSSI currently stores only the bare parent `Coordinate Transforms`. Expanded to a
comprehensive set below. All 12 values were confirmed to exist in the live `FunctionCategory`
vocabulary (83 rows) with the exact parent→child pairings shown; no existing value is removed.

- **Coordinate Transforms** `[HSSI]`
- **Coordinate Transforms > Mission-Specific** `[NEW]`
  Spacecraft- and instrument-fixed reference frames are the toolkit's signature capability:
  `pxform`, `sxform`, `pxfrm2`, `xfmsta` transform between any furnished frames; `ckgp`/`ckgpav`/
  `ckfrot`/`ckfxfm` return spacecraft/instrument pointing from C-kernels; `getfov` returns instrument
  field-of-view geometry from instrument kernels; `namfrm`/`frmnam`/`cidfrm`/`cnmfrm`/`ccifrm` resolve
  frame–body associations. The `software-functionality` skill maps `spiceypy` to this value directly.
- **Coordinate Transforms > Planetary** `[NEW]`
  Body-fixed planetary frames via PCK (`IAU_MARS`, `IAU_EARTH`, `ITRF93` — all documented in
  `docs/frames.rst`, `docs/pck.rst`, `docs/binary_pck.rst`), plus a full set of planetary coordinate
  conversions: `reclat`/`latrec`, `recgeo`/`georec` (geodetic), `recpgr`/`pgrrec` (planetographic),
  `recsph`/`sphrec`, `reccyl`/`cylrec`, `recrad`/`radrec`, `srfrec`, and the Jacobians
  `drdgeo`/`dgeodr`/`drdpgr`/`dpgrdr`.
- **Coordinate Transforms > Heliospheric** `[NEW]`
  Heliocentric ecliptic state computation is documented and worked end-to-end:
  `docs/insitu_sensing.rst` (lines 515–540) computes an interplanetary spacecraft's state **relative to
  the Sun** in the `ECLIPJ2000` ecliptic frame — `spkezr(target, et, "ECLIPJ2000", "NONE", "SUN")` —
  which is the heliocentric-aries-ecliptic (HAE) quantity in substance, and `docs/pyodide.rst` line 128
  shows the same `spkpos(..., "ECLIPJ2000", ...)` pattern. Any heliospheric frame distributed as a NAIF
  frame kernel is usable through the same `pxform`/`sxform`/`spkezr` calls once furnished.
  Consistent with the record's existing `Interplanetary Space` region.
  *Basis for retention, recorded because it is weaker than the sibling children:* SpiceyPy names **no**
  heliospheric coordinate system
  from the controlled definition of this subcategory (HCI, HAE, HEE, Carrington, Stonyhurst, RTN) —
  verified absent from `docs/*.rst` and `src/spiceypy/*.py`. `ECLIPJ2000` is a *generic* inertial
  ecliptic frame that becomes heliocentric only by choosing `SUN` as observer, and the supporting
  example is NAIF tutorial-lesson material. Contrast `> Magnetospheric`, where `GSE`/`GSM` are named
  and defined outright in `docs/frames.rst`. Retention rests on an in-substance rather than a by-name
  reading: the capability is genuinely present, and the completeness goal favors recording it. The
  earlier `IAU_SUN` justification has been withdrawn — it contradicted this file's own exclusion note
  that `IAU_SUN` is a body-fixed planetary-style frame already covered by `> Planetary`.
- **Coordinate Transforms > Magnetospheric** `[NEW]`
  `docs/frames.rst` documents `GSE` and `GSM` as SPICE parameterized two-vector dynamic frames,
  including a complete worked GSE frame-kernel definition (appendix "Frame Definition Examples") and
  explicit examples `spkezr(moon, et, "GSE", "NONE", "EARTH")` and `sxform("GSE", "J2000", et)`.
- **Data Processing and Analysis** `[NEW]`
  Reads and writes the SPICE ancillary-data kernel family and queries the kernel pool: `furnsh`,
  `unload`, `kclear`, `ktotal`, `kdata`, `kinfo`, `getfat`; `bodvrd`/`bodvcd` and
  `gcpool`/`gdpool`/`gipool`/`stpool` for pool variables; DAF/DAS-level readers (`dafopr`, `dafbfs`,
  `dafgda`, `dasopr`, `dasrfr`); DSK topography readers (`dskd02`, `dski02`, `dskv02`, `dskp02`,
  `dskgd`, `dskobj`, `dsksrf`); and SQL-like queries over Event Kernels (`ekfind`, `ekgc`, `ekgd`,
  `ekgi`, `ekpsel`, `ekntab`, `ektnam`).
- **Data Processing and Analysis > Analysis** `[NEW]`
  Derived-geometry science calculations: the full geometry-finder family (`gfoclt`, `gfdist`, `gfsep`,
  `gfrfov`, `gftfov`, `gfpa`, `gfposc`, `gfsubc`, `gfsntc`, `gfilum`, `gfevnt`, `gfudb`, `gfuds`) for
  occultation/distance/angular-separation/FOV/illumination event searches; surface intercepts and
  sub-points (`sincpt`, `subpnt`, `subslr`, `srfxpt`, `latsrf`); illumination angles (`ilumin`,
  `illumf`, `illumg`); limb and terminator point sets (`limbpt`, `termpt`, `edlimb`); phase angle
  (`phaseq`), target separation (`trgsep`), local solar time (`et2lst`), sub-solar planetocentric
  longitude (`lspcn`, `subsol`); and interval/window set algebra over event results (`wnunid`,
  `wnintd`, `wndifd`, `wnfild`, `wnfltd`, `wnexpd`, `wncond`, `wnsumd`).
- **Models and Simulations** `[NEW]`
  Provides physical/geometric models rather than only data reduction — see the two children.
- **Models and Simulations > Physics-Based** `[NEW]`
  Two-body/conic orbital propagation and element conversion (`prop2b`, `conics`, `oscelt`, `oscltx`);
  light-time and stellar-aberration corrected states (`spkltc`, `spkaps`, `spkapo`, `stelab`,
  `ltime`, and the `abcorr` model set documented in `docs/abcorr.rst`); triaxial-ellipsoid body shape
  models (`surfpt`, `surfnm`, `nearpt`, `dnearp`, `npedln`, `edlimb`, `inedpl`, `saelgv`); PCK-based
  body orientation models (`tipbod`, `tisbod`); and time-system models (`unitim`, `deltet`, `sce2c`,
  `sct2e`, `scs2e`, `sce2s`).
- **Models and Simulations > Observatory/Instrument Models** `[NEW]`
  Instrument-kernel field-of-view models exposed to users: `getfov` returns an instrument's FOV shape,
  boresight and boundary vectors; `fovray`/`fovtrg` test whether a ray or target lies within a modeled
  FOV; `gfrfov`/`gftfov` search for FOV entry/exit intervals. `docs/remote_sensing.rst` documents FK/IK
  frame and instrument-FOV definitions as the model inputs.
- **Mission-related** `[NEW]`
  SPICE is NASA/NAIF's ancillary-data system for space missions, and SpiceyPy is the Python interface
  to it: spacecraft ephemeris and attitude (SPK/CK), spacecraft-clock correlation (SCLK: `sce2c`,
  `sct2e`, `scs2e`, `sce2s`), instrument alignment (FK/IK), and kernel *writers* used by mission
  pipelines to produce ancillary products (`spkopn`/`spkw02`–`spkw20`, `ckopn`/`ckw01`–`ckw05`,
  `pckopn`/`pckw02`, `dskopn`/`dskw02`/`dskmi2`, `ekopn`/`ekops`/`ekifld`/`ekffld`/`ekacli`).
- **Mission-related > Observatory/Instrument Models** `[NEW]`
  Same FOV/alignment/pointing model surface as above, in its mission-infrastructure role: instrument
  and structure frames come from mission FK/IK kernels and pointing from mission CKs.

**Considered and deliberately excluded (audit trail):**
- `Coordinate Transforms > Ionospheric` / `> Solar` — no AACGM/MLT/apex support, and no
  Carrington/Stonyhurst/helioprojective transform is implemented or documented in this repo.
  (`IAU_SUN` alone is a body-fixed planetary-style frame, already covered by `> Planetary`.)
- `Data Processing and Analysis > Data Access and Retrieval` — the public API reads *local* kernel
  files; there is no remote-archive client. `src/spiceypy/tests/gettestkernels.py` downloads kernels
  over HTTPS but is test fixture infrastructure, not a user-facing retrieval capability.
- `Data Processing and Analysis > File Format Conversion` — the CSPICE transfer-format converters
  (`dafb2t`/`daft2b`/`dasb2t`/`dast2b`) are **not** wrapped (verified absent from the 650 public
  functions in `src/spiceypy/spiceypy.py`).
- `Data Processing and Analysis > Time Series Analysis` — SPICE time conversion and interval windows
  are not time-series signal analysis.
- All `Data Visualization` values — the package contains no plotting code. `docs/exampleone.rst`
  (Cassini position plot) uses `matplotlib` in *documentation example* code only.
- `Servers and Environments > Software or Environment Container` — Pyodide/WebAssembly wheels are a
  build target, not a container or server product.
- `Models and Simulations > Mission-Specific` / `> Theory` — SpiceyPy is deliberately
  mission-agnostic, and the analytic two-body work is already covered by `> Physics-Based`.

### 5. Related Region (MANDATORY)

`[CHANGED]` HSSI currently stores only `Interplanetary Space`. Kept, and extended using the curated
PyHC registry classification (highest-priority source per the metadata-priority order). All values
confirmed against the live `Region` vocabulary (24 rows).

- **Interplanetary Space** `[HSSI]` — SPICE's core domain: interplanetary spacecraft trajectory,
  pointing and observation geometry.
- **Solar Environment** `[NEW]` — PyHC community registry lists keyword `solar` for SpiceyPy;
  `IAU_SUN`/heliocentric frames and solar-direction geometry (`soldir`, `subsol`, `lspcn`) are
  documented capabilities.
- **Earth Magnetosphere** `[NEW]` — PyHC keyword `magnetosphere`; `docs/frames.rst` documents the
  geocentric solar-ecliptic (`GSE`) and geocentric solar-magnetospheric (`GSM`) frames with worked
  examples.
- **Earth Ionosphere** `[NEW]` — PyHC keyword `ionosphere_thermosphere_mesosphere`; SpiceyPy provides
  the geometry (position, pointing, geodetic/ITRF93 coordinates, local solar time) used with
  ionospheric-mission data.
- **Earth Thermosphere** `[NEW]` — same PyHC `ionosphere_thermosphere_mesosphere` evidence and the
  same geometry basis.

**Considered and excluded:** `Planetary Magnetospheres` and the per-planet magnetosphere rows
(`Mars Magnetosphere`, `Jupiter Magnetosphere`, …) — SpiceyPy supports planetary *body* geometry, not
magnetospheric science specifically, and the vocabulary has no general "planetary bodies/surfaces"
row. `Heliosheath`, `Solar Wind`, `Corona`, `Chromosphere`, `Photosphere`, `Solar Interior` — no
supporting evidence in the repository.

### 6. Authors (MANDATORY)

`[HSSI]` **Identity-aware union — all 21 existing HSSI authors retained, none dropped, none added.**
The union of HSSI's 21 people, `.zenodo.json` (21 creators), the DataCite concept-DOI creators
(21, matched by ORCID), and `CITATION.cff` (15 authors, a subset) is exactly these 21 people. Matched
by ORCID first, then normalized name. Affiliations are the union of the HSSI-stored organization and
the `CITATION.cff` / `.zenodo.json` affiliation for each matched author (no author gains or loses an
affiliation relative to HSSI).

| # | Name (HSSI stored form) | Identifier (ORCID) | Affiliation |
|---|---|---|---|
| 1 | Andrew Annex | https://orcid.org/0000-0002-0253-2313 | Johns Hopkins University (https://ror.org/00za53h95) |
| 2 | K.-Michael Aye | https://orcid.org/0000-0002-4088-1928 | Laboratory for Atmospheric and Space Physics (https://ror.org/01fcjzv38) |
| 3 | Kristin L. Berry | https://orcid.org/0000-0001-9757-9706 | USGS Astrogeology Science Center (https://ror.org/02623eb90) — see typo note below |
| 4 | Brian T. Carcich | https://orcid.org/0000-0001-9211-6526 | Latchmoor Services, LLC |
| 5 | Helge Eichhorn | https://orcid.org/0000-0003-0303-5199 | Planetary Transportation Systems GmbH |
| 6 | Johan Freiherr von Forstner | https://orcid.org/0000-0002-1390-4776 | Institute of Experimental and Applied Physics, University of Kiel |
| 7 | Lars Hinüber | https://orcid.org/0009-0004-7121-1021 | Not found |
| 8 | Chris Jeppesen | Not found | Laboratory for Atmospheric and Space Physics (https://ror.org/01fcjzv38) |
| 9 | Shankar Kulumani | https://orcid.org/0000-0002-7822-0471 | Collins Aerospace |
| 10 | Jesse A. Mapel | https://orcid.org/0000-0001-5756-0373 | USGS Astrogeology Science Center (https://ror.org/02623eb90) — see typo note below |
| 11 | Jean-Luc Margot | https://orcid.org/0000-0001-9798-1797 | University of California, Los Angeles (https://ror.org/046rm7j60) |
| 12 | Jonathan McAuliffe | Not found | DLR Gesellschaft für Raumfahrtanwendungen (GfR) mbH |
| 13 | Gavin Medley | https://orcid.org/0000-0002-3520-9715 | Laboratory for Atmospheric and Space Physics (https://ror.org/01fcjzv38); University of Colorado Boulder (https://ror.org/02ttsq026) |
| 14 | Shin-ya Murakami | https://orcid.org/0000-0002-7137-4849 | GFD Dennou Club |
| 15 | Kyle Niemeyer | https://orcid.org/0000-0003-4425-7097 | Oregon State University (https://ror.org/00ysfqy60) |
| 16 | Ben Pearson | Not found | Not found |
| 17 | Jorge Diaz del Rio | Not found | ODC Space |
| 18 | Alfonso Sánchez Rodríguez | https://orcid.org/0000-0003-1889-6696 | Not found |
| 19 | Benoît Seignovert | https://orcid.org/0000-0001-6533-275X | Jet Propulsion Laboratory (https://ror.org/027k65916) |
| 20 | Marcel Stefko | https://orcid.org/0000-0002-7736-2611 | ETH Zurich |
| 21 | Miguel de Val-Borro | https://orcid.org/0000-0002-0455-9384 | Planetary Science Institute |

Notes on this field:
- All 21 are people; there is no organization author, so no ROR is used as an author identifier.
- **Affiliation-name correction completed 2026-07-30.** The shared organization previously read
  **"USGS Astrogeology Science Centerlogy"**, a typo originating in `.zenodo.json` and propagated
  through DataCite. The corrected **"USGS Astrogeology Science Center"** matches `CITATION.cff`
  (lines 37 and 66); its existing ROR `https://ror.org/02623eb90` resolves to "Astrogeology Science
  Center". Kristin L. Berry and Jesse A. Mapel retain their existing affiliations to this
  organization.
- Non-actionable stylistic naming variants were intentionally **not** changed: `CITATION.cff` writes
  "Andrew M. Annex" where HSSI
  stores "Andrew Annex", and "Johan Lauritz Freiherr von Forstner" where HSSI stores "Johan Freiherr
  von Forstner". `pyproject.toml` lower-cases the surname ("Andrew M. annex") and is not authoritative
  for name form.
- **Andrew Annex's affiliation is point-in-time, not current.**
  All three static sources agree
  on Johns Hopkins University (HSSI, `CITATION.cff` line 10, `.zenodo.json`), and that is the value
  recorded above. His ORCID employment record, however, shows JHU ("Ph.D. Candidate") **ended
  2022-01-31**, a Caltech postdoc ended 2024-01-12, and his current open employment since 2024-01-29 is
  **SETI Institute** ("Senior Science Systems Engineer", Mountain View) — which already exists as an
  HSSI Organization row with ROR `https://ror.org/02dxgk712`. Author affiliation in a citation context
  is normally the affiliation at time of contribution, which is what the project's own citation files
  assert, so Johns Hopkins University is retained.
- Gavin Medley's ORCID and his second affiliation come from the existing HSSI record; `.zenodo.json`
  lists him without an ORCID, so the HSSI value is the richer one and is preserved.

### 7. Software Name (MANDATORY)
SpiceyPy

`[HSSI]` Unchanged. Matches the repository name, `README.rst` title, the PyHC registry `name`, and
`CITATION.cff` title "SpiceyPy: a Pythonic Wrapper for the SPICE Toolkit". Editorial intent preserved.

### 8. Description (MANDATORY)
SpiceyPy is a python wrapper for the SPICE Toolkit. SPICE is an essential tool for scientists and engineers alike in the planetary science field for Solar System Geometry. Please visit the NAIF website for more details about SPICE.

IMPORTANT: The code is provided "as is", use at your own risk. However, the NAIF now distributes python "lessons" that use SpiceyPy as the python to spice interface.

`[HSSI]` Unchanged. This is a faithful transcription of `README.rst` "Introduction" (lines 32–36),
so it is both the submitted wording and the repository's own wording. No stylistic rewrite applied.

### 9. Concise Description (OPTIONAL)
SpiceyPy is a python wrapper for the SPICE Toolkit. SPICE is an essential tool for scientists and engineers alike in the planetary science field for Solar System Geometry.

`[HSSI]` Unchanged (171 characters, within the 200-character limit).

### 10. Publication Date (RECOMMENDED)
2016-03-27

`[CHANGED]` HSSI previously stored **2025-10-27**, which is the release date of tag `v8.0.0`
(`git log -1 v8.0.0` → 2025-10-27) — i.e. a version date, not a first-publication date. Field 10 is
defined as "Date of first broadcast/publication … Used for the initial version of the software."
Evidence for 2016-03-27: the first PyPI distribution of `spiceypy` is 1.0.0, uploaded
2016-03-27T20:21:04Z (PyPI JSON API `releases`), and tag `v1.0.0` is dated 2016-03-27 (the earlier
pre-release tag `v0.7.0` points at a 2016-03-26 commit and was never published to PyPI). Leaving 2025-10-27 in place would be
additionally misleading now that Version (Field 12) advances to v8.2.0 (2026-07-24). The prior value
is recorded here so the replacement remains auditable.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

`[HSSI]` Unchanged. Correct per the Field 11 guidance (DOI obtained through the GitHub–Zenodo
workflow) and confirmed by DataCite `publisher: "Zenodo"` for the concept DOI.

### 12. Version (RECOMMENDED)
- **Version Number:** v8.2.0
- **Version Date:** 2026-07-24
- **Version Description:** Restored Python 3.10 wheel builds and corrected the PyPI classifier; faster wheel builds that compile CSPICE once per cibuildwheel job; CSPICE cached from a hash-verified mirror; documentation updated to the Pyodide 314.0.0 kernel; `cspice_flavor` now read via `c_int.in_dll`. Fixes: `spkaps` `accobs` corrected to a 3-vector (backwards compatible via truncation), `dskb02` vertex-bounds return shape corrected, `ctypes` argtype misspellings on `dafrs`, `gfilum`, `polyds`, `vnormg` and `vnorm` that silently disabled argument marshalling, erroneous double-byref calls, and a missing comma in `__all__` that merged "exceptions" and "stypes" and broke those imports.
- **Version PID:** https://doi.org/10.5281/zenodo.21540077

`[CHANGED]` HSSI stores `v8.0.0`. Superseded by objectively newer authoritative evidence: git tag
`v8.2.0` (tag commit `c8b6da4f1370ba7b5cf9ad06829143f7fc055f2a`, 2026-07-24), `CHANGELOG.md`
`## [8.2.0] - 2026-07-24`, PyPI `spiceypy` 8.2.0 uploaded 2026-07-24T21:37:59Z, and the Zenodo
record for that release (`10.5281/zenodo.21540077`, `version: v8.2.0`,
`publication_date: 2026-07-24`) whose `conceptdoi` is the Field 2 value.
**Stored form is the bare `v8.2.0`** — the view API renders it as `SpiceyPy - v8.2.0`; that rendered
prefix must never be written back. Version description condensed from the `CHANGELOG.md` 8.2.0
section.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x** `[HSSI]`
- **C** `[NEW]`
- **Other** `[HSSI]`

`Java` was **REMOVED** on 2026-07-30 and is deliberately absent from the list
above. The final field value is exactly the three values shown.

`[CHANGED]` All values confirmed against the live `ProgrammingLanguage` vocabulary (19 rows).
- `Python 3.x` — the package is Python-only at the API level; `requires-python = ">=3.10"`, wheels for
  CPython 3.10–3.14.
- `C` added: SpiceyPy exists to bind the NAIF **C** SPICE toolkit. `src/spiceypy/utils/libspicehelper.py`
  marshals to the C ABI via `ctypes`; `CMakeLists.txt` builds CSPICE from source ("CSPICE is ~2200 C
  files") via `FetchContent` of `cspice-cmake-spiceypy`; `src/spiceypy/cyice/cyice.pyx` compiles to C.
- `Other` — covers Cython (GitHub linguist: 337 KB, the second-largest language) and CMake, neither of
  which has a vocabulary row.
- **Java — removed.** No evidence supports it: the GitHub languages API returns
  `{Python, Cython, CMake, TeX}` only, and the *entire* git history contains **zero** `.java` files
  (`git log --all --name-only | grep -ci '\.java$'` → 0). The likely origin is an early commit message
  (`ab0890a`, seven minutes after the initial commit), which notes that the early file structure "was
  intended to replicate classes seen in JSPICE (Java wrapper for SPICE)" — an inspiration, not an
  implementation language.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.21105/joss.02050

`[NEW]` Empty on HSSI. Annex et al., "SpiceyPy: a Pythonic Wrapper for the SPICE Toolkit", *Journal of
Open Source Software*, 5(46), 2050. Authoritative: `CITATION.cff` `preferred-citation` with
`doi: 10.21105/joss.02050`, the README "Citing SpiceyPy" section, the JOSS badge in `README.rst`, and
the `joss/` directory in the repository.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

`[NEW]` Empty on HSSI. Evidence: `LICENSE` ("The MIT License (MIT)", Copyright (c) [2015-2024]
[Andrew Annex]), `pyproject.toml` `license = "MIT"` with `license-files = ["LICENSE"]`,
`CITATION.cff` `license: MIT`, `.zenodo.json` `"license": "MIT"`, GitHub API license
`"MIT License"`, and DataCite `rightsList` (`rightsIdentifier: mit`, SPDX scheme). `MIT License` is
the canonical live `License` row and the URI is that row's stored URL.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

`[CHANGED]` Set-union: all 13 existing HSSI keywords retained (stored lower-case; the view renders
Title Case), plus 6 additions that reuse **existing** live `Keyword` rows (585 rows) rather than
minting near-duplicates.

Existing `[HSSI]`: `cspice`, `ephemeris`, `geometry`, `hacktoberfest`, `jpl`, `naif`, `nasa`,
`navigation`, `python`, `space`, `spice`, `spiceypy`, `toolkit`

Added `[NEW]`: `planetary science`, `coordinate transformations`, `time`, `orbit`, `wrapper`, `pyhc`

Evidence for the additions — `planetary science`: README/description "essential tool … in the
planetary science field"; `coordinate transformations`: the frame/coordinate conversion API (Field 4);
`time`: SPICE time-system conversion (`str2et`, `et2utc`, `timout`, `unitim`, SCLK family);
`orbit`: ephemeris/orbital-element API (`spkezr`, `oscelt`, `conics`, `prop2b`); `wrapper`:
`README.rst` line 4 "SpiceyPy is a Python wrapper for the NAIF C SPICE Toolkit"; `pyhc`: SpiceyPy is
a listed PyHC **community** package (`_data/projects.yml`). `hacktoberfest` is preserved even though
it is no longer among the repository's GitHub topics — set-union never drops an existing entry.
Current GitHub topics (`ephemeris`, `nasa`, `navigation`, `python`, `space`, `spice`, `toolkit`) and
`pyproject.toml` keywords (`spiceypy`, `spice`, `cspice`, `naif`, `jpl`, `space`, `geometry`,
`ephemeris`) are all already covered.

### 17. Data Sources (OPTIONAL)
Not found — intentionally left empty.

`[NEW]` (still empty) SpiceyPy's public API reads SPICE kernels from the **local filesystem**
(`furnsh` takes a path); it implements no archive client, no HTTP/FTP retrieval, and no
observatory-specific data source. `src/spiceypy/tests/gettestkernels.py` downloads test kernels from
`https://naif.jpl.nasa.gov/pub/naif/…`, but that is test-fixture infrastructure, not a user-facing
data source. `Other` and `HTTP/HTTPS Directories` were considered and dropped for that reason; and
`Observatory/Mission-specific` is inapplicable because Field 17 requires naming the observatory in
Field 32, which is (correctly) empty for this mission-agnostic toolkit. A documented empty value is
the correct outcome here.

### 18. Input File Formats (RECOMMENDED)
- **ascii** `[NEW]`
- **Other** `[NEW]`

`[NEW]` Both empty on HSSI; both confirmed in the live `FileFormat` vocabulary (11 rows).
- `ascii` — SPICE **text** kernels are plain text and are read directly: meta-kernels/furnsh files,
  LSK (leapseconds), FK (frames), IK (instruments), text SCLK and text PCK. Wrapped readers:
  `furnsh`, `ldpool`, `lmpool`, `rdtext`, `getfat`.
- `Other` — SPICE **binary** kernels have no vocabulary row: SPK, binary PCK, CK, DSK, EK/DBK, and the
  underlying DAF/DAS containers. Wrapped readers: `spkobj`/`spkcov`, `ckobj`/`ckcov`, `pckfrm`/`pckcov`,
  `dskobj`/`dsksrf`/`dskd02`/`dski02`, `dafopr`/`dafgda`, `dasopr`/`dasrfr`, `ekopr`.

### 19. Output File Formats (RECOMMENDED)
- **ascii** `[NEW]`
- **Other** `[NEW]`

`[NEW]` Both empty on HSSI.
- `ascii` — text file creation and writing is wrapped: `txtopn` (open a new text file) and `writln`
  (write a line of text).
- `Other` — SpiceyPy wraps the SPICE kernel **writers**, which produce binary kernels:
  `spkopn`/`spkcls` with `spkw01`–`spkw20`, `ckopn`/`ckcls` with `ckw01`–`ckw05`,
  `pckopn`/`pckw02`/`pckcls`, `dskopn`/`dskw02`/`dskmi2`/`dskcls`, and the EK writers
  `ekopn`/`ekops`/`ekifld`/`ekffld`/`ekacli`.

### 20. Operating System (RECOMMENDED)
- **Linux** `[NEW]`
- **Mac** `[NEW]`
- **Windows** `[NEW]`
- **Other** `[NEW]`

`[NEW]` Empty on HSSI. All four confirmed in the live `OperatingSystem` vocabulary (7 rows).
`README.rst` "Known Working Environments": "SpiceyPy is compatible with modern Linux, Mac, and Windows
environments … OS: OS X, Linux, Windows, FreeBSD". `pyproject.toml` classifiers cover
`MacOS :: MacOS X`, `POSIX :: Linux`, `Microsoft :: Windows` and `POSIX :: BSD :: FreeBSD`.
`.github/workflows/ci-build.yml` tests on `ubuntu-latest`, `ubuntu-22.04-arm`, `macos-15`,
`macos-15-intel` and `windows-latest`. `Other` covers **FreeBSD** (classifier, README) and the
**Pyodide/WebAssembly browser** target (CHANGELOG 8.1.2 "Python 3.14 Pyodide/WebAssembly (wasm32)
wheels"), neither of which has a vocabulary row.
`Operating System Independent` was rejected: the package ships compiled, platform-specific wheels.

### 21. CPU Architecture (RECOMMENDED)
- **x86-64** `[NEW]`
- **Apple Silicon arm64** `[NEW]`
- **Linux aarch64 or arm64** `[NEW]`
- **Other** `[NEW]`

`[NEW]` Empty on HSSI. All four confirmed in the live `CpuArchitecture` vocabulary (9 rows).
`README.rst`: "CPU: x64, arm" and "ARM support for Linux-aarch64 & osx-arm64". The publish workflow
sets `CIBW_ARCHS_MACOS=arm64` / `x86_64` and `CIBW_ARCHS_LINUX=aarch64`; CI matrix includes
`ubuntu-22.04-arm` (Linux arm64), `macos-15` (Apple Silicon), `macos-15-intel` and `windows-latest`
(x86-64); `pyproject.toml` `[tool.cibuildwheel] skip` excludes 32-bit builds.
`Other` covers the `wasm32` Pyodide/Emscripten target (`CIBW_ARCHS: "wasm32"` in `ci-build.yml`),
which has no vocabulary row.

### 22. Related Phenomena (OPTIONAL)
Not found — intentionally left empty.

`[NEW]` (still empty) The live `Phenomena` vocabulary has 7 rows (Coronal Heating, Coronal Mass
Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission). SpiceyPy is a
geometry/ancillary-data toolkit and supports none of these phenomena as a science function; the
vocabulary is closed, so an unsupported term cannot be added. Documented empty value.

### 23. Development Status (RECOMMENDED)
Active

`[NEW]` Empty on HSSI. Confirmed in the live `RepoStatus` vocabulary (8 rows). Evidence:
`pyproject.toml` classifier `Development Status :: 5 - Production/Stable`; four releases in the last
four months (8.1.0 2026-04-04, 8.1.1 and 8.1.2 2026-06-14, 8.2.0 2026-07-24); GitHub API
`archived: false`, `disabled: false`, last push 2026-07-26; a scheduled weekly CI cron; and a funded
active development effort (the Cyice PDART work). Matches the repostatus.org definition of `Active`
("reached a stable, usable state and is being actively developed").

### 24. Documentation (RECOMMENDED)
https://spiceypy.readthedocs.io

`[HSSI]` Unchanged. Confirmed by `pyproject.toml` `"Documentation"`, `CITATION.cff` `url`,
`.readthedocs.yaml`, the PyHC registry `docs` field, and the README documentation section. The URL
resolves (README also links the equivalent `http://spiceypy.readthedocs.org` form). Installation
instructions live at `docs/installation.rst` under the same site, satisfying the field's
"documentation and installation instructions" requirement.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

`[NEW]` Empty on HSSI. Evidence: `README.rst` "Acknowledgements" — "Supported in part through NASA
PDART23 80NSSC25K7040 FY24-FY27"; and `docs/cyice.rst` — "A recent NASA PDART grant award
(80NSSC25K7040) has funded work to significantly enhance SpiceyPy". The acronym is expanded per the
Field 25 instruction, and the name/ROR match the existing HSSI `Organization` row
identified by `https://ror.org/027ka1x80`.

### 26. Award Title (OPTIONAL)
- **Award Title:** Improving SpiceyPy: the Python SPICE interface
- **Award Number:** 80NSSC25K7040

`[NEW]` Empty on HSSI. The **award number** is authoritative and directly stated in the repository
(`README.rst` Acknowledgements; `docs/cyice.rst`), which also names the program (NASA PDART, 2023
call — "PDART23", period FY24–FY27). No live `Award` row exists for `80NSSC25K7040` (checked all 50
rows), so this creates a new award entry.
The **title** is not stated in the repository. It is taken from the NASA ADS record for the matching
PDART-2023 proposal by A. M. Annex, bibcode `2023pdar.prop...37A`, titled "Improving SpiceyPy: the
Python SPICE interface." The author, program and cycle all align with the repository's
"PDART23 … FY24-FY27", and independent third-party reporting describes Annex as PI of "NASA ROSES
PDART23 #37 'Improving SpiceyPy: the Python SPICE interface,' project funding spans FY24-FY27" —
corroborating the title↔grant-number linkage from a second source. The title is retained as the
best-supported match to the repository's award number and program evidence.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

`[NEW]` Empty on HSSI. Four publications the project itself prioritizes, all distinct from the Field 14
reference publication.

1. https://doi.org/10.1016/0032-0633(95)00107-7
   Acton, C. H., Jr. (1996). Ancillary data services of NASA's Navigation and Ancillary Information
   Facility. *Planetary and Space Science*, 44(1), 65–70.
   *Source:* `CITATION.cff` `references[0]` — the SPICE toolkit citation the project asks users to cite
   alongside SpiceyPy.
2. https://doi.org/10.1016/j.pss.2017.02.013
   Acton, C., Bachman, N., Semenov, B., & Wright, E. (2017). A look towards the future in the handling
   of space science mission geometry. *Planetary and Space Science*, 150, 9–12.
   *Source:* `CITATION.cff` `references[1]`.
3. Annex, A. M. (2017). *SpiceyPy usage statistics abstract* [Conference abstract]. Lunar and Planetary
   Institute Contribution 1986, 7081. https://ui.adsabs.harvard.edu/abs/2017LPICo1986.7081A/abstract
   *Source:* `README.rst` "Citing SpiceyPy" — explicitly requested for citing SpiceyPy usage
   statistics. No DOI available, so recorded as a citation with a permanent link per the Field 27
   instruction.
4. Annex, A. M. (2019). *SpiceyPy usage statistics abstract* [Conference abstract]. Lunar and Planetary
   Institute Contribution 2151, 7043. https://ui.adsabs.harvard.edu/abs/2019LPICo2151.7043A/abstract
   *Source:* `README.rst` "Citing SpiceyPy". No DOI available.

### 28. Related Datasets (OPTIONAL)
Not found.

`[NEW]` (still empty) SpiceyPy operates on SPICE kernels, which are per-mission ancillary data
products archived at NAIF/PDS, but the repository identifies no specific dataset and no dataset DOI.
The toolkit is deliberately dataset-agnostic. Documented empty value.

### 29. Related Software (OPTIONAL)

`[NEW]` Empty on HSSI. Two entries pass the relevance gate.

1. **NAIF CSPICE Toolkit** — https://naif.jpl.nasa.gov/naif/toolkit_C.html
   *Evidence:* the defining relationship — SpiceyPy is a wrapper around this specific
   domain library. `README.rst` line 4 ("a Python wrapper for the NAIF C SPICE Toolkit, written using
   ctypes and Cython"), `pyproject.toml` description, `src/spiceypy/utils/libspicehelper.py` (loads and
   binds `libcspice`), `CMakeLists.txt` (builds/links CSPICE), and `tkvrsn("TOOLKIT")` returning
   `CSPICE_N0067`. A domain-specific dependency in the strongest sense.
2. **cspice-cmake-spiceypy** — https://github.com/AndrewAnnex/cspice-cmake-spiceypy
   *Evidence:* a companion package maintained by the same author specifically to build CSPICE for
   SpiceyPy. `CMakeLists.txt` `FetchContent_Declare(cspice GIT_REPOSITORY
   https://github.com/AndrewAnnex/cspice-cmake-spiceypy.git)`; `pyproject.toml` and CI comments
   describe the pinned ref and the shared-library naming contract between the two projects.

**Considered and excluded (audit trail):**
- `numpy` — Tier A generic infrastructure (the sole runtime dependency; `requires_dist:
  ["numpy>=1.23.5"]`). Excluded from Fields 29 and 30 alike.
- `cython`, `scikit-build-core`, `cmake`, `pytest`, `pytest-benchmark`, `pandas`, `coverage`, `black`,
  `twine`, `build`, `cibuildwheel`, `delvewheel`, `sphinx` and the doc/CI toolchain — build, test and
  packaging infrastructure; equally at home in a web app or a finance model. Tier A treatment.
- `spiceminer` (https://github.com/DaRasch/spiceminer) — README Acknowledgements: "DaRasch wrote
  spiceminer, which I looked at to get SpiceCells working". A genuine same-purpose predecessor
  influence, but the acknowledgement is a one-line historical credit rather than a maintained
  relationship, and the project is long unmaintained. It stays in this audit trail and is not
  asserted.
- `Icy` (IDL) and `Mice` (MATLAB), NAIF's official sibling wrappers — genuinely similar-purpose
  software, but the repository never references them (the docs reference NAIF's C and IDL *toolkit
  documentation*, not the Icy wrapper), so there is no in-repo evidence to cite.
- `JSPICE` — named only in a 2014 early commit message (`ab0890a`) as structural inspiration; no URL,
  no durable relationship.
- `Pyodide` / `PyScript` — generic runtime/browser infrastructure, not a heliophysics peer tool.

### 30. Interoperable Software (OPTIONAL)
Not found — intentionally left empty.

`[NEW]` (still empty) No package meets the demonstrated-exchange bar for this field. SpiceyPy exposes
no adapter/converter API to another domain tool, defines no shared or convertible data model with a
peer package, ships no plugin/extension relationship, and provides no cross-language bridge to a named
domain tool. Its only runtime dependency is `numpy` (Tier A — being a dependency is not
interoperability). The `cyice` submodule shares the CSPICE kernel pool with the ctypes wrappers, but
that is *intra*-package, not interoperability with other software. CSPICE itself is the wrapped
library and is recorded in Field 29. The `docs/pyodide.rst` PyScript examples demonstrate running in a
browser runtime, which is infrastructure, not a peer-tool exchange. A documented empty value is the
correct outcome.

### 31. Related Instruments (OPTIONAL)
None — no entries. Documented omission (SPASE ladder rule 5).

`[NEW]` (still empty) **Determination: SpiceyPy is instrument-agnostic by design and supports no
specific instrument.** It provides generic geometry, time and reference-frame services for *whatever*
kernels the user furnishes; every instrument-specific fact (FOV shape, boresight, alignment) lives in
the mission's own IK/FK kernels, not in this software. It reads no instrument-specific data format,
implements no instrument-specific convention, and is not an instrument-team tool. A user searching HSSI
for a particular instrument would not expect SpiceyPy back.

Instrument-adjacent mentions found and correctly excluded at the relevance gate, all of them
**tutorial/demo material** — the `docs/` tree carries NAIF's "Lessons" verbatim
(`docs/lessonindex.rst`: "Here listed are the various SPICE lessons provided by the NAIF translated to
use python code examples"): the Cassini framing camera in `docs/remote_sensing.rst` ("Remote Sensing
Hands-On Lesson, using CASSINI"), Mars Express in `docs/event_finding.rst`, and Voyager, Galileo and
Mars Global Surveyor instrument/pointing examples in `docs/ck.rst`. The Field 31 gate explicitly
excludes tutorial/demo name-drops and instrument-agnostic tools.
Per the ladder, no name is emitted without an `https://spase-metadata.org/` identifier, and nothing is
invented; the correct outcome here is a documented omission because the entries
fail the *relevance* gate rather than being related-but-unresolvable.

### 32. Related Observatories (OPTIONAL)
None — no entries. Documented omission (SPASE ladder rule 5).

`[NEW]` (still empty) **Determination: SpiceyPy is mission/observatory-agnostic.** Same reasoning as
Field 31 — mission identity is supplied entirely by the user's kernels (SPK/CK/SCLK), not by the
software. SpiceyPy implements no mission's data conventions, is not a mission-team tool, and accesses
no mission archive. The mission names in the repository (Cassini, Mars Express, Voyager, Galileo,
Mars Global Surveyor, and the Saturn-barycenter Cassini position example in `docs/exampleone.rst`) all
occur inside NAIF's translated tutorial lessons or documentation examples, which the Field 32 gate
excludes as "tutorial/demo name-drops" and "platforms you *could* support". Consistent with Field 17
being empty (no observatory-specific data source) — the two fields agree.
No related entity reaches the resolution ladder. Should a future release add mission-specific
support, those entries should be resolved against the then-current SPASE-backed HSSI vocabulary.

### 33. Logo (OPTIONAL)
Not found.

`[NEW]` (still empty) No logo exists. The repository's only image is
`docs/images/exampleoneplot_min.png` (a plot from the Cassini position example, not a logo); the
README uses only shields.io status badges; the PyHC community-registry entry for SpiceyPy has no
`logo` field (unlike several other PyHC entries); and `docs/conf.py` sets no Sphinx logo. The GitHub
owner avatar is a personal account image, not a software logo, so it is not used.

---

## Summary of changes relative to the live HSSI record

**Newly filled (were empty):** Reference Publication (14), License (15), Input File Formats (18),
Output File Formats (19), Operating System (20), CPU Architecture (21), Development Status (23),
Funder (25), Award (26), Related Publications (27), Related Software (29).

**Enriched (existing values kept, new ones added):** Software Functionality (4) — 1 value → 12;
Related Region (5) — 1 value → 5; Keywords (16) — 13 → 19; Version (12) — v8.0.0 → v8.2.0 with date,
description and version DOI added.

**Corrected (a submitted value replaced or removed on authoritative evidence):**
Publication Date (10) — 2025-10-27 → 2016-03-27; Programming Language (13) — `Java` removed and `C`
added, leaving `Python 3.x`, `C`, `Other`.

**Unchanged (submitted values respected):** Persistent Identifier (2), Code Repository (3),
Authors (6, all 21 retained), Software Name (7), Description (8), Concise Description (9),
Publisher (11), Documentation (24).

**Documented empty (correct outcome, not a gap):** Data Sources (17), Related Phenomena (22),
Related Datasets (28), Interoperable Software (30), Related Instruments (31),
Related Observatories (32), Logo (33).

## Notes on non-obvious values

- Publication Date is the first PyPI publication date, not the date of the previously stored release.
- Programming Language excludes unsupported `Java` and includes the wrapped C toolkit.
- The ADS-derived PDART title is the best-supported match to award `80NSSC25K7040`.
- `Coordinate Transforms > Heliospheric` is retained on demonstrated heliocentric ecliptic capability.
- Andrew Annex retains the citation-time Johns Hopkins University affiliation rather than his current
  employment.
- `spiceminer` remains excluded because its historical acknowledgement does not establish a current
  software relationship.

## Final HSSI state (2026-07-30)

Fields 2–33 match the final live record. Field 12 is stored as bare `v8.2.0`; the `SpiceyPy -`
prefix is presentation only. The corrected shared USGS organization name applies to Kristin L. Berry
and Jesse A. Mapel without changing either affiliation relationship.
