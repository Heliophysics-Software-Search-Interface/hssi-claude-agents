# HSSI Metadata Extraction Results

**HSSI Software ID:** d0dcf8b7-d032-481b-b80e-dea683cc1fa4
**Repository:** https://github.com/AndrewAnnex/SpiceyPy
**Source Revision:** 388c219808f5b0dc9ec10acee2ca1b3cbe3c6e47
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-10-29
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Not part of the stored software record; placeholder is expected for a refresh.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.593914

This is the Zenodo **concept** DOI
(`conceptdoi` / `conceptrecid` 593914 on the Zenodo records for v8.2.0 and v8.3.0) and it is listed in
`CITATION.cff` under `identifiers` with description "Zenodo archive". The v8.3.0 version deposit
(`10.5281/zenodo.23304845`, the Field 12 Version PID) carries `IsVersionOf 10.5281/zenodo.593914` at
DataCite. On 2026-10-29 the concept presented that newest deposit: DataCite gave the concept's `version`
as `v8.3.0` and its title as "AndrewAnnex/SpiceyPy: SpiceyPy 8.3.0", matching the newest tag `v8.3.0`.

### 3. Code Repository (MANDATORY)
https://github.com/AndrewAnnex/SpiceyPy

Confirmed by `pyproject.toml` `[project.urls]` (Homepage / Repository /
Source), `CITATION.cff` `repository-code`, the PyHC community registry `code` field, and the live
GitHub API (not archived, default branch `main`; on 2026-10-29 the last commit on `main` was
`fb98550`, dated 2026-10-25).

### 4. Software Functionality (RECOMMENDED)

The previous value contained only the bare parent `Coordinate Transforms`; the comprehensive set
below replaces it. All 12 values match the live `FunctionCategory` vocabulary with the exact
parent→child pairings shown.

- **Coordinate Transforms**
- **Coordinate Transforms > Mission-Specific**
  Spacecraft- and instrument-fixed reference frames are the toolkit's signature capability:
  `pxform`, `sxform`, `pxfrm2`, `xfmsta` transform between any furnished frames; `ckgp`/`ckgpav`/
  `ckfrot`/`ckfxfm` return spacecraft/instrument pointing from C-kernels; `getfov` returns instrument
  field-of-view geometry from instrument kernels; `namfrm`/`frmnam`/`cidfrm`/`cnmfrm`/`ccifrm` resolve
  frame–body associations. The `software-functionality` skill maps `spiceypy` to this value directly.
- **Coordinate Transforms > Planetary**
  Body-fixed planetary frames via PCK (`IAU_MARS`, `IAU_EARTH`, `ITRF93` — all documented in
  `docs/frames.rst`, `docs/pck.rst`, `docs/binary_pck.rst`), plus a full set of planetary coordinate
  conversions: `reclat`/`latrec`, `recgeo`/`georec` (geodetic), `recpgr`/`pgrrec` (planetographic),
  `recsph`/`sphrec`, `reccyl`/`cylrec`, `recrad`/`radrec`, `srfrec`, and the Jacobians
  `drdgeo`/`dgeodr`/`drdpgr`/`dpgrdr`.
- **Coordinate Transforms > Heliospheric**
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
- **Coordinate Transforms > Magnetospheric**
  `docs/frames.rst` documents `GSE` and `GSM` as SPICE parameterized two-vector dynamic frames,
  including a complete worked GSE frame-kernel definition (appendix "Frame Definition Examples") and
  explicit examples `spkezr(moon, et, "GSE", "NONE", "EARTH")` and `sxform("GSE", "J2000", et)`.
- **Data Processing and Analysis**
  Reads and writes the SPICE ancillary-data kernel family and queries the kernel pool: `furnsh`,
  `unload`, `kclear`, `ktotal`, `kdata`, `kinfo`, `getfat`; `bodvrd`/`bodvcd` and
  `gcpool`/`gdpool`/`gipool`/`stpool` for pool variables; DAF/DAS-level readers (`dafopr`, `dafbfs`,
  `dafgda`, `dasopr`, `dasrfr`); DSK topography readers (`dskd02`, `dski02`, `dskv02`, `dskp02`,
  `dskgd`, `dskobj`, `dsksrf`); and SQL-like queries over Event Kernels (`ekfind`, `ekgc`, `ekgd`,
  `ekgi`, `ekpsel`, `ekntab`, `ektnam`).
- **Data Processing and Analysis > Analysis**
  Derived-geometry science calculations: the full geometry-finder family (`gfoclt`, `gfdist`, `gfsep`,
  `gfrfov`, `gftfov`, `gfpa`, `gfposc`, `gfsubc`, `gfsntc`, `gfilum`, `gfevnt`, `gfudb`, `gfuds`) for
  occultation/distance/angular-separation/FOV/illumination event searches; surface intercepts and
  sub-points (`sincpt`, `subpnt`, `subslr`, `srfxpt`, `latsrf`); illumination angles (`ilumin`,
  `illumf`, `illumg`); limb and terminator point sets (`limbpt`, `termpt`, `edlimb`); phase angle
  (`phaseq`), target separation (`trgsep`), local solar time (`et2lst`), sub-solar planetocentric
  longitude (`lspcn`, `subsol`); and interval/window set algebra over event results (`wnunid`,
  `wnintd`, `wndifd`, `wnfild`, `wnfltd`, `wnexpd`, `wncond`, `wnsumd`).
- **Models and Simulations**
  Provides physical/geometric models rather than only data reduction — see the two children.
- **Models and Simulations > Physics-Based**
  Two-body/conic orbital propagation and element conversion (`prop2b`, `conics`, `oscelt`, `oscltx`);
  light-time and stellar-aberration corrected states (`spkltc`, `spkaps`, `spkapo`, `stelab`,
  `ltime`, and the `abcorr` model set documented in `docs/abcorr.rst`); triaxial-ellipsoid body shape
  models (`surfpt`, `surfnm`, `nearpt`, `dnearp`, `npedln`, `edlimb`, `inedpl`, `saelgv`); PCK-based
  body orientation models (`tipbod`, `tisbod`); and time-system models (`unitim`, `deltet`, `sce2c`,
  `sct2e`, `scs2e`, `sce2s`).
- **Models and Simulations > Observatory/Instrument Models**
  Instrument-kernel field-of-view models exposed to users: `getfov` returns an instrument's FOV shape,
  boresight and boundary vectors; `fovray`/`fovtrg` test whether a ray or target lies within a modeled
  FOV; `gfrfov`/`gftfov` search for FOV entry/exit intervals. `docs/remote_sensing.rst` documents FK/IK
  frame and instrument-FOV definitions as the model inputs.
- **Mission-related**
  SPICE is NASA/NAIF's ancillary-data system for space missions, and SpiceyPy is the Python interface
  to it: spacecraft ephemeris and attitude (SPK/CK), spacecraft-clock correlation (SCLK: `sce2c`,
  `sct2e`, `scs2e`, `sce2s`), instrument alignment (FK/IK), and kernel *writers* used by mission
  pipelines to produce ancillary products (`spkopn`/`spkw02`–`spkw20`, `ckopn`/`ckw01`–`ckw05`,
  `pckopn`/`pckw02`, `dskopn`/`dskw02`/`dskmi2`, `ekopn`/`ekops`/`ekifld`/`ekffld`/`ekacli`).
- **Mission-related > Observatory/Instrument Models**
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
  (Cassini position plot) uses `matplotlib` in *documentation example* code only. The docs example
  gallery added on `main` after v8.3.0 (`docs/examples/plot_*.py`, read at `fb98550`) also draws its
  figures with `matplotlib` in documentation code (the Mars 2020 rover traverse and the Santa Monica
  eclipse pages); gallery pages are not the library's capability (Field 4 rule 4).
- `Servers and Environments > Software or Environment Container` — Pyodide/WebAssembly wheels are a
  build target, not a container or server product.
- `Models and Simulations > Mission-Specific` / `> Theory` — SpiceyPy is deliberately
  mission-agnostic, and the analytic two-body work is already covered by `> Physics-Based`.

### 5. Related Region (RECOMMENDED)

The previous value contained only `Interplanetary Space`. It is retained and extended using the curated
PyHC registry classification (highest-priority source per the metadata-priority order). Every value
matches the live `Region` vocabulary.

- **Interplanetary Space** — SPICE's core domain: interplanetary spacecraft trajectory,
  pointing and observation geometry.
- **Solar Environment** — PyHC community registry lists keyword `solar` for SpiceyPy;
  `IAU_SUN`/heliocentric frames and solar-direction geometry (`soldir`, `subsol`, `lspcn`) are
  documented capabilities.
- **Earth Magnetosphere** — PyHC keyword `magnetosphere`; `docs/frames.rst` documents the
  geocentric solar-ecliptic (`GSE`) and geocentric solar-magnetospheric (`GSM`) frames with worked
  examples.
- **Earth Ionosphere** — PyHC keyword `ionosphere_thermosphere_mesosphere`; SpiceyPy provides
  the geometry (position, pointing, geodetic/ITRF93 coordinates, local solar time) used with
  ionospheric-mission data.
- **Earth Thermosphere** — same PyHC `ionosphere_thermosphere_mesosphere` evidence and the
  same geometry basis.

**Considered and excluded:** `Planetary Magnetospheres` and the per-planet magnetosphere rows
(`Mars Magnetosphere`, `Jupiter Magnetosphere`, …) — SpiceyPy supports planetary *body* geometry, not
magnetospheric science specifically, and the vocabulary has no general "planetary bodies/surfaces"
row. `Heliosheath`, `Solar Wind`, `Corona`, `Chromosphere`, `Photosphere`, `Solar Interior` — no
supporting evidence in the repository.

### 6. Authors (MANDATORY)

**Canonical roster: 22 authors.** The union of the 21 people HSSI listed before the v8.3.0 refresh
(2026-10-29), `.zenodo.json` (22 creators at `fb98550`), the DataCite creators of the v8.3.0 deposit (21,
matched by ORCID), and `CITATION.cff` (15 authors, a subset) is exactly these 22 people; Anton Soloviev
(22) entered `.zenodo.json` after the v8.3.0 release (see below). Matched by ORCID first, then normalized name. Affiliations record the complete shared HSSI organization set
for each person, reconciled against the `CITATION.cff` and `.zenodo.json` affiliations.

| # | Name (HSSI stored form) | Identifier (ORCID) | Affiliation |
|---|---|---|---|
| 1 | Andrew Annex | https://orcid.org/0000-0002-0253-2313 | Johns Hopkins University (https://ror.org/00za53h95) |
| 2 | K.-Michael Aye | https://orcid.org/0000-0002-4088-1928 | Laboratory for Atmospheric and Space Physics (https://ror.org/01fcjzv38) |
| 3 | Kristin L. Berry | https://orcid.org/0000-0001-9757-9706 | USGS Astrogeology Science Center (https://ror.org/02623eb90) — see typo note below |
| 4 | Brian T. Carcich | https://orcid.org/0000-0001-9211-6526 | Latchmoor Services, LLC |
| 5 | Helge Eichhorn | https://orcid.org/0000-0003-0303-5199 | Planetary Transportation Systems GmbH |
| 6 | Johan Lauritz Freiherr von Forstner | https://orcid.org/0000-0002-1390-4776 | Institute of Experimental and Applied Physics, University of Kiel; Paradox Cat GmbH |
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
| 20 | Marcel Stefko | https://orcid.org/0000-0002-7736-2611 | ETH Zurich (https://ror.org/05a28rw58) |
| 21 | Miguel de Val-Borro | https://orcid.org/0000-0002-0455-9384 | Planetary Science Institute (https://ror.org/05vvg9554) |
| 22 | Anton Soloviev | Not found | Not found |

Notes on this field:
- All 22 are people; there is no organization author, so no ROR is used as an author identifier.
- **Previous affiliation name corrected.** The shared organization previously read
  **"USGS Astrogeology Science Centerlogy"**, a typo originating in `.zenodo.json` and propagated
  through DataCite. The corrected **"USGS Astrogeology Science Center"** matches `CITATION.cff`
  (lines 37 and 66); its existing ROR `https://ror.org/02623eb90` resolves to "Astrogeology Science
  Center". Kristin L. Berry and Jesse A. Mapel retain their existing affiliations to this
  organization.

**Johan Lauritz Freiherr von Forstner — both affiliations, and why.** The Kiel institute is supported
by this software's `CITATION.cff`; Paradox Cat GmbH is shared-record context rather than evidence from
SpiceyPy. ORCID `0000-0002-1390-4776` gives Paradox Cat as his current employer, and `solarmach`
independently credits the same person with that affiliation. The catalogue therefore retains both
organizations on the shared person record; neither is discarded in favour of the other.

- Non-actionable stylistic naming variants were intentionally **not** changed: `CITATION.cff` writes
  "Andrew M. Annex" where the shared HSSI record uses "Andrew Annex". The Johan Lauritz Freiherr von Forstner form
  above follows the shared, ORCID-bearing HSSI person record. `pyproject.toml` lower-cases the surname
  ("Andrew M. annex") and is not authoritative for name form.
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

**Anton Soloviev — added in the v8.3.0 refresh (2026-10-29; rule 8).** Commit `373782e` (pull request #582, 2026-10-21, after
the v8.3.0 release) added `{"name": "Anton Soloviev"}` to the `.zenodo.json` creators (read at `fb98550`).
`.zenodo.json` is one of the project's own author sources, so he is an attested author although the v8.3.0
Zenodo deposit predates the change: a deposit's creator list is a snapshot.
- *Identity and name.* The commit that added him (`373782e`) and a later commit by the same account
  (`a676028`) are git-authored as "Anthony", and the commit API attributes both to the GitHub account
  `antonsoo`. The name and its split (`Anton` /
  `Soloviev`) follow the project's spelling in `.zenodo.json` (rule 12), not the account's display name.
- *No ORCID* (rule 14). A fielded ORCID search for given name Anton and family name Soloviev returns two
  records, and neither links to him: `0009-0001-5273-7106` (Saratov State University employment, no works,
  no researcher URLs) and `0009-0001-3407-7220` (two clinical neurology papers on transthyretin
  amyloidosis). The spellings Solovev and Solovyev are other surnames; a control search for Andrew Annex
  returns his ORCID alone.
- *No affiliation.* `.zenodo.json` gives none, and the company named on his GitHub profile is not a source
  rule 21 accepts.

**Committers not added (rule 5).** Apart from Andrew Annex, Anton Soloviev and dependabot, the commits in
`388c219..fb98550` are by Mark Mentovai (`8209dea`, long kernel paths in the test meta-kernel) and Sammy
Dabbas (`1e387fd`, the `py.typed` marker); neither appears in any author source.

### 7. Software Name (MANDATORY)
SpiceyPy

Matches the repository name, `README.rst` title, the PyHC registry `name`, and
`CITATION.cff` title "SpiceyPy: a Pythonic Wrapper for the SPICE Toolkit". Editorial intent preserved.

### 8. Description (MANDATORY)
SpiceyPy is a python wrapper for the SPICE Toolkit. SPICE is an essential tool for scientists and engineers alike in the planetary science field for Solar System Geometry. Please visit the NAIF website for more details about SPICE.

IMPORTANT: The code is provided "as is", use at your own risk. However, the NAIF now distributes python "lessons" that use SpiceyPy as the python to spice interface.

This is a faithful transcription of `README.rst` "Introduction" (lines 32–36), so it is both the
submitted wording and the repository's own wording.

### 9. Concise Description (OPTIONAL)
SpiceyPy is a python wrapper for the SPICE Toolkit. SPICE is an essential tool for scientists and engineers alike in the planetary science field for Solar System Geometry.

The text is 171 characters, within the 200-character limit.

### 10. Publication Date (RECOMMENDED)
2016-03-27

HSSI previously stored **2025-10-27**, which is the release date of tag `v8.0.0`
(`git log -1 v8.0.0` → 2025-10-27) — i.e. a version date, not a first-publication date. Field 10 is
defined as "Date of first broadcast/publication … Used for the initial version of the software."
Evidence for 2016-03-27: the first PyPI distribution of `spiceypy` is 1.0.0, uploaded
2016-03-27T20:21:04Z (PyPI JSON API `releases`), and tag `v1.0.0` is dated 2016-03-27 (the earlier
pre-release tag `v0.7.0` points at a 2016-03-26 commit and was never published to PyPI). Leaving 2025-10-27 in place would be
additionally misleading now that Version (Field 12) records later releases. The prior value
is recorded here so the replacement remains auditable.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Correct per the Field 11 guidance (DOI obtained through the GitHub–Zenodo
workflow) and confirmed by DataCite `publisher: "Zenodo"` for the concept DOI.

### 12. Version (RECOMMENDED)
- **Version Number:** v8.3.0
- **Version Date:** 2026-10-11
- **Version Description:** exactly the text in the block below: three `###` section headings, each item
  line beginning with a space and `- `, single newlines within a section and one blank line between
  sections.

```text
### Added
 - Python 3.15 support: cp315 wheel builds, CI test matrix, and PyPI classifier
 - PEP 561 `py.typed` marker and `Typing :: Typed` classifier so type checkers use spiceypy's annotations
 - Top-level cyice functions now accept NumPy scalars and 0-d arrays (numeric and string) and dispatch them to the scalar `_s` implementations

### Changed
 - Refined type hints throughout spiceypy, callbacks, and support types for smoother mypy usage

### Fixed
 - String-input cyice `_v` functions (str2et_v, utc2et_v, scencd_v, scs2e_v) segfaulted on 0-d or multi-dimensional arrays; they now raise ValueError
 - cyice functions rejected `np.str_` and `bytes` for string arguments with a TypeError due to Cython 3 exact-type checks
 - Missing commas in cyice `__all__` that merged "azlcpo_v"/"azlrec" and "reset"/"rpd"
 - ekgc return type annotation had the tuple element order wrong
```

- **Version PID:** https://doi.org/10.5281/zenodo.23304845

**Why v8.3.0** (rule 3; read at `fb9855023083371735c0423ae30cfa0db46f7d4f`, the head of `main`, and at the
tag). The tag `v8.3.0` names `b27a33dd55395e8d212f77dfb4969953808a61da`, which lies on `main`'s own lineage
(`git merge-base --is-ancestor v8.3.0 fb98550` holds), and `v8.2.0` is its ancestor. Its GitHub release,
"SpiceyPy 8.3.0", is neither a draft nor a pre-release; PyPI's JSON API lists 8.3.0 with an sdist and
wheels for CPython 3.10–3.15, none yanked; and `__version__` in `src/spiceypy/__init__.py` reads `8.3.0` at
the tag (the package version is dynamic, scraped from that string). No later tag, GitHub release or PyPI
upload existed on 2026-10-29. The number keeps the `v` of the tags and of the superseded value; PyPI and
the release name write it bare.

**Version Date** (rule 7). The GitHub release was published 2026-10-11T20:49:50Z. The tagged commit is
dated 2026-10-11T13:14:55-07:00 (20:14:55Z), the first PyPI file was uploaded 2026-10-11T21:20:23Z, the
Zenodo deposit's `publication_date` and DataCite's `Issued` date are 2026-10-11, and `CHANGELOG.md` heads
the section `## [8.3.0] - 2026-10-11`.

**Version Description** (rules 13–15). The release name says no more than the tag, so the text comes from
the release body, which matches the `CHANGELOG.md` `[8.3.0]` section. Kept whole: the items on supported
Python versions, type-checker support, cyice input handling and four fixes a user could hit. Dropped whole
as build, CI, packaging or documentation housekeeping (rule 14): "mypy type checking CI job and `typecheck`
dependency group", "Zero-argument ctypes functions now declare empty argtypes rather than None", "Updated
to cibuildwheel v4.3.1 for the final CPython 3.15.0 release", the Pyodide/wasm build-configuration item,
"Docs updated to PyScript 2026.7.3 (Pyodide 314.0.3)", "Various CI action pin updates" and "Various typos
in docstrings and docs". The body's `## [8.3.0] - 2026-10-11` heading, which repeats the number and date,
and each kept item's trailing pull-request references (`(#575)` and the like) are dropped (rule 15); the
items' own words and the leading space before each `-` are kept, with the body's CRLF line endings written
as LF.

**Version PID** (rule 17). `10.5281/zenodo.23304845` is v8.3.0's GitHub-integration deposit: its Zenodo
`version` and DataCite `version` are `v8.3.0`, its title is "AndrewAnnex/SpiceyPy: SpiceyPy 8.3.0", it
carries `IsSupplementTo https://github.com/AndrewAnnex/SpiceyPy/tree/v8.3.0` and
`IsVersionOf 10.5281/zenodo.593914`, the concept's `HasVersion` list includes it, and the DOI resolves.

**Previous values.** HSSI held v8.2.0 (released 2026-07-24, Version PID
`https://doi.org/10.5281/zenodo.21540077`) until the v8.3.0 refresh (2026-10-29), and v8.0.0 before that; each was superseded
by a newer release (rule 3). The v8.2.0 description was a condensed summary of that release's changelog
section; it belongs to that release and is not carried onto v8.3.0 (rule 10). **Stored form is the bare
`v8.3.0`**: the view API renders it as `SpiceyPy - v8.3.0`, and that rendered prefix must never be written
back.

**After v8.3.0.** `CHANGELOG.md` at `fb98550` opens an `## [Unreleased]` section: cyice built and shipped
in the Pyodide/WebAssembly wheel, the start of a docs example gallery, and cyice fixes (error checks,
double-precision returns, integer dtypes). That code is unreleased and is not recorded here (rule 2); a
later update should look for the release that ships it.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x**
- **C**

The final field value is exactly these two values; both match the live `ProgrammingLanguage` vocabulary.
Read at `fb98550`.
- `Python 3.x` — the language users write. The package is Python-only at the API level;
  `requires-python = ">=3.10"`, the classifiers name Python 3.10–3.15, and the v8.3.0 wheels cover
  CPython 3.10–3.15.
- `C` — the science core. SpiceyPy exists to bind the NAIF **C** SPICE toolkit:
  `src/spiceypy/utils/libspicehelper.py` marshals to the C ABI via `ctypes`; `CMakeLists.txt` builds
  CSPICE from source ("CSPICE is ~2200 C files") via `FetchContent` of `cspice-cmake-spiceypy`, and the
  wheels ship the compiled library. A third-party C library the package compiles and calls to do its
  science lists C (rule 4).
- **`Other` — removed in the v8.3.0 refresh (2026-10-29).** HSSI held `Other` until then, recorded for Cython (GitHub
  linguist's second-largest language) and CMake, neither of which has a vocabulary row. Rule 7 excludes
  both: `Other` is never a stand-in for a build system (CMake), nor for glue code such as a single Cython
  bridge between two counted languages. The Cython here is exactly that bridge: the cyice submodule, one
  `src/spiceypy/cyice/cyice.pyx` with its `cyice.pxd`, which `docs/cyice.rst` describes as Cython-based
  "wrapper functions to CSPICE within SpiceyPy". The layer is large: `cyice.pyx` is 319,115 bytes and
  `cyice.pxd` 27,186 bytes, together the 346,301 bytes GitHub's linguist reports as Cython, and it has its
  own tests, benchmarks and docs page. Size does not change what it is. Rule 4's clause for a supported
  front end in a second language does not fire either: users call cyice from Python
  (`from spiceypy import cyice`), and the Cython is a binding layer over CSPICE's C API, not a language a
  user writes to use the software. No other tracked file is in a language rule 4 admits:
  the rest of the tree is Python, reStructuredText, JSON, YAML, Markdown, TOML and plain text, one PNG
  image, `CITATION.cff`, the `py.typed` marker, docs tooling (`docs/mini-coi.js`,
  `docs/_static/css/pyscript_editor.css`, `docs/make.bat`, `docs/Makefile`) and the JOSS paper's
  bibliography (`joss/paper.bib`, which linguist counts as TeX). `Other` should not be restored unless a
  language without a row enters the package.
- **Java — removed earlier.** No evidence supports it: the GitHub languages API returns
  `{Python, Cython, CMake, TeX}` only, and the *entire* git history contains **zero** `.java` files
  (`git log --all --name-only | grep -ci '\.java$'` → 0). The likely origin is an early commit message
  (`ab0890a`, seven minutes after the initial commit), which notes that the early file structure "was
  intended to replicate classes seen in JSPICE (Java wrapper for SPICE)" — an inspiration, not an
  implementation language.

### 14. Reference Publication (OPTIONAL)
https://doi.org/10.21105/joss.02050

Annex et al., "SpiceyPy: a Pythonic Wrapper for the SPICE Toolkit", *Journal of
Open Source Software*, 5(46), 2050. Authoritative: `CITATION.cff` `preferred-citation` with
`doi: 10.21105/joss.02050`, the README "Citing SpiceyPy" section, the JOSS badge in `README.rst`, and
the `joss/` directory in the repository.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

Evidence: `LICENSE` ("The MIT License (MIT)", Copyright (c) [2015-2024]
[Andrew Annex]), `pyproject.toml` `license = "MIT"` with `license-files = ["LICENSE"]`,
`CITATION.cff` `license: MIT`, `.zenodo.json` `"license": "MIT"`, GitHub API license
`"MIT License"`, and DataCite `rightsList` (`rightsIdentifier: mit`, SPDX scheme). `MIT License` is
the canonical live `License` row and the URI is that row's stored URL.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

The keyword set retains the 13 established HSSI terms (stored lower-case; the view renders Title
Case) and adds six distinct terms that reuse existing HSSI vocabulary entries.

Retained: `cspice`, `ephemeris`, `geometry`, `hacktoberfest`, `jpl`, `naif`, `nasa`,
`navigation`, `python`, `space`, `spice`, `spiceypy`, `toolkit`

Additional values: `planetary science`, `coordinate transformations`, `time`, `orbit`, `wrapper`, `pyhc package`

Evidence for the additions — `planetary science`: README/description "essential tool … in the
planetary science field"; `coordinate transformations`: the frame/coordinate conversion API (Field 4);
`time`: SPICE time-system conversion (`str2et`, `et2utc`, `timout`, `unitim`, SCLK family);
`orbit`: ephemeris/orbital-element API (`spkezr`, `oscelt`, `conics`, `prop2b`); `wrapper`:
`README.rst` line 4 "SpiceyPy is a Python wrapper for the NAIF C SPICE Toolkit"; `pyhc package`: SpiceyPy is a listed PyHC **community** package (`_data/projects.yml`), and `pyhc package` is HSSI's catalogue-wide marker for official PyHC packages. It replaced the ad hoc `pyhc` keyword this record used to carry; `pyhc` should not be restored. `hacktoberfest` is preserved even though
it is no longer among the repository's GitHub topics — set-union never drops an existing entry.
Current GitHub topics (`ephemeris`, `nasa`, `navigation`, `python`, `space`, `spice`, `toolkit`) and
`pyproject.toml` keywords (`spiceypy`, `spice`, `cspice`, `naif`, `jpl`, `space`, `geometry`,
`ephemeris`) are all already covered.

### 17. Data Sources (OPTIONAL)
Not found — intentionally left empty.

SpiceyPy's public API reads SPICE kernels from the **local filesystem**
(`furnsh` takes a path); it implements no archive client, no HTTP/FTP retrieval, and no
observatory-specific data source. `src/spiceypy/tests/gettestkernels.py` downloads test kernels from
`https://naif.jpl.nasa.gov/pub/naif/…`, but that is test-fixture infrastructure, not a user-facing
data source. `Other` and `HTTP/HTTPS Directories` were considered and dropped for that reason; and
`Observatory/Mission-specific` is inapplicable because Field 17 requires naming the observatory in
Field 32, which is (correctly) empty for this mission-agnostic toolkit. A documented empty value is
the correct outcome here.

### 18. Input File Formats (RECOMMENDED)
- **ascii**
- **Other**
Both names match the live `FileFormat` vocabulary.
- `ascii` — SPICE **text** kernels are plain text and are read directly: meta-kernels/furnsh files,
  LSK (leapseconds), FK (frames), IK (instruments), text SCLK and text PCK. Wrapped readers:
  `furnsh`, `ldpool`, `lmpool`, `rdtext`, `getfat`.
- `Other` — SPICE **binary** kernels have no vocabulary row: SPK, binary PCK, CK, DSK, EK/DBK, and the
  underlying DAF/DAS containers. Wrapped readers: `spkobj`/`spkcov`, `ckobj`/`ckcov`, `pckfrm`/`pckcov`,
  `dskobj`/`dsksrf`/`dskd02`/`dski02`, `dafopr`/`dafgda`, `dasopr`/`dasrfr`, `ekopr`.

### 19. Output File Formats (RECOMMENDED)
- **ascii**
- **Other**
Both formats are directly supported by the writer API.
- `ascii` — text file creation and writing is wrapped: `txtopn` (open a new text file) and `writln`
  (write a line of text).
- `Other` — SpiceyPy wraps the SPICE kernel **writers**, which produce binary kernels:
  `spkopn`/`spkcls` with `spkw01`–`spkw20`, `ckopn`/`ckcls` with `ckw01`–`ckw05`,
  `pckopn`/`pckw02`/`pckcls`, `dskopn`/`dskw02`/`dskmi2`/`dskcls`, and the EK writers
  `ekopn`/`ekops`/`ekifld`/`ekffld`/`ekacli`.

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**
- **Other**
All four names match the live `OperatingSystem` vocabulary.
`README.rst` "Known Working Environments": "SpiceyPy is compatible with modern Linux, Mac, and Windows
environments … OS: OS X, Linux, Windows, FreeBSD". `pyproject.toml` classifiers cover
`MacOS :: MacOS X`, `POSIX :: Linux`, `Microsoft :: Windows` and `POSIX :: BSD :: FreeBSD`.
`.github/workflows/ci-build.yml` tests on `ubuntu-latest`, `ubuntu-22.04-arm`, `macos-15`,
`macos-15-intel` and `windows-latest`. `Other` covers **FreeBSD** (classifier, README) and the
**Pyodide/WebAssembly browser** target (CHANGELOG 8.1.2 "Python 3.14 Pyodide/WebAssembly (wasm32)
wheels"), neither of which has a vocabulary row.
`Operating System Independent` was rejected: the package ships compiled, platform-specific wheels.

### 21. CPU Architecture (RECOMMENDED)
- **x86-64**
- **Apple Silicon arm64**
- **Linux aarch64 or arm64**
- **Other**
All four names match the live `CpuArchitecture` vocabulary.
`README.rst`: "CPU: x64, arm" and "ARM support for Linux-aarch64 & osx-arm64". The publish workflow
sets `CIBW_ARCHS_MACOS=arm64` / `x86_64` and `CIBW_ARCHS_LINUX=aarch64`; CI matrix includes
`ubuntu-22.04-arm` (Linux arm64), `macos-15` (Apple Silicon), `macos-15-intel` and `windows-latest`
(x86-64); `pyproject.toml` `[tool.cibuildwheel] skip` excludes 32-bit builds.
`Other` covers the `wasm32` Pyodide/Emscripten target (`CIBW_ARCHS: "wasm32"` in `ci-build.yml`),
which has no vocabulary row.

### 22. Related Phenomena (OPTIONAL)
Not found — intentionally left empty.

The available HSSI phenomena are Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar
Corona, Solar Flares, Solar Wind, and X-ray emission. SpiceyPy is a
geometry/ancillary-data toolkit and supports none of these phenomena as a science function; the
vocabulary is closed, so an unsupported term cannot be added. Documented empty value.

### 23. Development Status (RECOMMENDED)
Active

The value matches the live `RepoStatus` vocabulary. Rules 1–4 do not fire: nothing points to a new
location, the repository is not archived (GitHub API `archived: false`, `disabled: false`), and the README
carries no repostatus.org badge or status statement. Rule 6 (recency, for software that reached a stable,
usable state) gives `Active`. The dated anchors, read on 2026-10-29: the last commit on `main` is
`fb9855023083371735c0423ae30cfa0db46f7d4f`, dated 2026-10-25, and the latest release is v8.3.0
(2026-10-11). Stable releases go back to 1.0.0 (2016); the `pyproject.toml` classifier
`Development Status :: 5 - Production/Stable`, a weekly scheduled CI run (`.github/workflows/ci-build.yml`,
cron `0 4 * * 0`) and the funded Cyice work (Fields 25–26) corroborate. Matches the repostatus.org
definition of `Active` ("reached a stable, usable state and is being actively developed").

### 24. Documentation (RECOMMENDED)
https://spiceypy.readthedocs.io

Confirmed by `pyproject.toml` `"Documentation"`, `CITATION.cff` `url`,
`.readthedocs.yaml`, the PyHC registry `docs` field, and the README documentation section. The URL
resolves (README also links the equivalent `http://spiceypy.readthedocs.org` form). Installation
instructions live at `docs/installation.rst` under the same site, satisfying the field's
"documentation and installation instructions" requirement.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

Evidence: `README.rst` "Acknowledgements" — "Supported in part through NASA
PDART23 80NSSC25K7040 FY24-FY27"; and `docs/cyice.rst` — "A recent NASA PDART grant award
(80NSSC25K7040) has funded work to significantly enhance SpiceyPy". The acronym is expanded per the
Field 25 instruction, and the name/ROR match the existing HSSI `Organization` row
identified by `https://ror.org/027ka1x80`.

### 26. Award Title (OPTIONAL)
- **Award Title:** Improving SpiceyPy: the Python SPICE interface
- **Award Number:** 80NSSC25K7040

The **award number** is authoritative and directly stated in the repository
(`README.rst` Acknowledgements; `docs/cyice.rst`), which also names the program (NASA PDART, 2023
call — "PDART23", period FY24–FY27).
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

Two publications: the SPICE toolkit papers the project asks every user to cite alongside SpiceyPy, both
distinct from the Field 14 reference publication. Project files read at `fb98550`; literature searched on
2026-10-29, all years.

1. https://doi.org/10.1016/0032-0633(95)00107-7
   Acton, C. H., Jr. (1996). Ancillary data services of NASA's Navigation and Ancillary Information
   Facility. *Planetary and Space Science*, 44(1), 65–70.
   *Source:* `CITATION.cff` `references[0]` — the SPICE toolkit citation the project asks users to cite
   alongside SpiceyPy (README "Citing SpiceyPy": "please cite SpiceyPy and the SPICE toolkit").
2. https://doi.org/10.1016/j.pss.2017.02.013
   Acton, C., Bachman, N., Semenov, B., & Wright, E. (2018). A look towards the future in the handling
   of space science mission geometry. *Planetary and Space Science*, 150, 9–12.
   *Source:* `CITATION.cff` `references[1]`, which dates it February 2017; Crossref gives the volume's
   January 2018 issue date.

Both qualify under rule 4 (papers the project's citation guidance asks for) and are kept as incumbents
under rule 7.

**Removed in the v8.3.0 refresh (2026-10-29): two meeting abstracts.** HSSI held two further entries,
stored as their ADS abstract URLs (`https://ui.adsabs.harvard.edu/abs/<bibcode>/abstract`), until then; the
user confirmed their removal on 2026-10-29 (rules 1 and 7).
- `2017LPICo1986.7081A` — Annex, A. (2017). SpiceyPy, a Python
  Wrapper for SPICE. Third Planetary Data Workshop and The Planetary Geologic Mappers Annual Meeting,
  LPI Contribution No. 1986, abstract 7081.
- `2019LPICo2151.7043A` — Annex, A. M. (2019). SpiceyPy, a
  Complete Pythonic Interface for Spice. 4th Planetary Data Workshop, LPI Contribution No. 2151,
  abstract 7043.

Both are two-page abstracts in the workshops' LPI abstract volumes, and the 2019 text calls itself one
("This abstract serves as a status update on the project"); ADS indexes the abstracts in the LPI Contribution
volumes as `inproceedings`, so the record type does not distinguish them from papers. The README asks readers who
cite SpiceyPy usage statistics to cite "my 2017 and or 2019 abstracts", but a meeting abstract is never an
eligible publication, even one the project asks for. No poster or paper from either workshop is deposited
(a Zenodo search keyed on Annex's ORCID and on his name finds none), so nothing replaces them. They should
not be restored. The dossier formerly described both as "SpiceyPy usage statistics" abstracts, after the
README's reason for citing them; the titles above are the records' own.

**Weighed and not listed.**
- `2023LPICo2991.7004A` — Annex, A. M. (2023). The Status of
  SpiceyPy in 2023. 6th Planetary Data Workshop, LPI Contribution No. 2991, abstract 7004. A one-page
  meeting abstract (rule 1), with no deposited poster or paper.
- `10.5281/zenodo.11114005` — Annex, A. (2024). SpiceyPy: an open source exemplar in PSD.
  A seven-slide lightning-talk deck (title; what SpiceyPy is; a JOSS citation request; missions and
  agencies using it; two slides of lessons for SMD; links): about 400 words of bullet points, with no
  results or explanatory prose. The user judged on 2026-10-29 that it fails the standalone test for slide
  decks, so it is not an eligible publication (rule 1).
- `10.5281/zenodo.11117756` — Annex, A. (2024). PlanetaryPy: a Python community for
  Planetary Science. A presentation about the PlanetaryPy community, not about this software.
- `10.1029/2018JA025877` — Burrell, A. G., et al. (2018). Snakes on a Spaceship—An Overview
  of Python in Heliophysics. *Journal of Geophysical Research: Space Physics* (`2018JGRA..12310384B`).
  Annex is one of its ten authors, and the JOSS paper cites it as background. SpiceyPy appears in its
  package table (Table 1), in its own short appendix subsection (A.5.1 of the arXiv version, 1901.00143)
  among 27 package descriptions, and in the HelioPy description (A.1.4), which says HelioPy builds on it.
  Its subject is Python in heliophysics as a whole, not this software, so rule 3 does not add it, nor is
  Python in heliophysics a platform SpiceyPy serves (it serves SPICE users); the paper's own results and
  software are not built with SpiceyPy, so rule 5 does not add it either, whoever wrote it.
- `2023pdar.prop...37A`, Annex's 2023 PDART proposal "Improving SpiceyPy: the Python SPICE interface" (the
  Field 26 title source), is a funding proposal record, not a publication; the ASCL entry
  (`2019ascl.soft03016A`) and the Zenodo version deposits are software records (Fields 2 and 12).

**Method and model papers (rule 4): none beyond the two Acton papers.** Rule 4 is applied to the list as a
whole, by its usefulness to a reader of this record. The method and model references in the docs'
reference lists, the code's docstrings and the wrapped CSPICE routines each attach to one component of
the wrapped toolkit:
- the *Literature_References* of the CSPICE N0067 routines SpiceyPy wraps (the CSPICE source the build
  fetches through `cspice-cmake-spiceypy`, pinned by SHA-256), of which 49 out of 626 cite anything: the
  SGP4 papers behind `evsgp4`, `getelm` and `spkw10` (Hoots and Roehrich, Spacetrack Report #3; Hoots,
  Spacetrack Report #6; Hoots, Schumacher and Glover 2004; Vallado et al. 2006, which the `evsgp4`
  docstring also names), Lieske 1979 behind `b1900` and `b1950`, and three JPL memoranda by Owen (one with
  Vaughan);
- the NAIF Required Reading reproduced in the docs: `docs/frames.rst` (Lieske 1977 and 1979; Standish
  1982 and two Standish JPL memoranda; Bass and Cesarone, a JPL document) and `docs/pck.rst` (Duxbury
  1979; the IAU/IAG working group reports on cartographic coordinates and rotational elements of 2000,
  2006 and 2009).

With the two Acton papers that makes 13 papers in published form (journal articles, one conference
paper and the two Spacetrack technical reports), or 19 counting the six internal JPL memoranda and
documents; the split is by publication form. The other references in those lists are generic mathematics,
numerical-methods, almanac and textbook references (Thomas and Finney, Numerical Recipes, the CRC tables,
Rivlin, Apostol, Conte and de Boor, the ANSI C standard, Bate, Mueller and White, Danby, Taff, the
Explanatory Supplement, the Astronomical Almanacs, Jespersen and Fitz-Randolph) and three further items:
Woo's "Fast Ray-Box Intersection" (a generic graphics algorithm, behind `dskx02`), the ADCOM/DO Form 12
element-set transmission format (behind `getelm`) and a Wikipedia page on Chebyshev polynomials (behind
`chbigr`). None of these count. Each method or model paper beyond the two Acton papers documents
one routine or subsystem and is incidental to SpiceyPy as a whole; listed together they would bury the
papers about SpiceyPy, so none is listed. Only the two Acton papers, which the project asks every user to
cite, stay. A later refresh should not propose the per-routine or Required Reading references.

**Third-party uses (rule 5): none, because SpiceyPy is widely used.** On 2026-10-29 ADS found SpiceyPy in
the full text of 173 records (110 refereed) and in the acknowledgements of 53 (51 refereed), and the
Field 14 JOSS paper had 132 citations in ADS and 134 in Semantic Scholar. A list of users would tell a
searcher nothing about the software, so none is added. That includes the early uses the JOSS paper itself
cites (`joss/paper.bib`: Behar et al. 2016 and 2017, Porter et al. 2018, Zangari 2018, Attree et al. 2019,
two theses and other projects), which are third-party uses, not method papers. DataCite records no `IsCitedBy` relation on the
concept DOI.

**Search** (2026-10-29, all years): the README and `docs/citation.rst` citation guidance, `CITATION.cff`
`references`, the docs' reference lists and the code's docstrings; ADS by title, abstract, full text and
acknowledgements; Zenodo keyed on Annex's ORCID and name variants; DataCite relations on the concept DOI;
Semantic Scholar. Nonsense-token controls returned nothing, and a comparable package name (`sunpy`)
returned full-text hits.

### 28. Related Datasets (OPTIONAL)
Not found.

SpiceyPy operates on SPICE kernels, which are per-mission ancillary data
products archived at NAIF/PDS, but the repository identifies no specific dataset and no dataset DOI.
The toolkit is deliberately dataset-agnostic. Documented empty value.

### 29. Related Software (OPTIONAL)

Two entries pass the relevance gate.

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

No package meets the demonstrated-exchange bar for this field. SpiceyPy exposes
no adapter/converter API to another domain tool, defines no shared or convertible data model with a
peer package, ships no plugin/extension relationship, and provides no cross-language bridge to a named
domain tool. Its only runtime dependency is `numpy` (Tier A — being a dependency is not
interoperability). The `cyice` submodule shares the CSPICE kernel pool with the ctypes wrappers, but
that is *intra*-package, not interoperability with other software. CSPICE itself is the wrapped
library and is recorded in Field 29. The `docs/pyodide.rst` PyScript examples demonstrate running in a
browser runtime, which is infrastructure, not a peer-tool exchange. The docs example gallery added on
`main` after v8.3.0 (read at `fb98550`) runs in a browser environment that also installs astropy, scipy
and sympy; its scratchpad page shows `spice.str2et(Time("2019-06-10", scale="utc").isot)`, which hands an
astropy time to SpiceyPy as an ISO-8601 string. A string any time library can produce is not a
package-specific exchange (Tier B, rule 4), so astropy is not listed. A documented empty value is the
correct outcome.

### 31. Related Instruments (OPTIONAL)
None — no entries. Documented omission (SPASE ladder rule 5).

**Determination: SpiceyPy is instrument-agnostic by design and supports no
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
Mars Global Surveyor instrument/pointing examples in `docs/ck.rst`. The docs example gallery added on
`main` after v8.3.0 (read at `fb98550`) adds a page plotting the Mars 2020 Perseverance rover's drive from
mission kernels (`docs/examples/plot_m20_three_forks.py`), another demonstration of the generic
`spkpos`/`reclat` path. The Field 31 gate explicitly excludes tutorial/demo name-drops, gallery pages
and instrument-agnostic tools.
Per the ladder, no name is emitted without an `https://spase-metadata.org/` identifier, and nothing is
invented; the correct outcome here is a documented omission because the entries
fail the *relevance* gate rather than being related-but-unresolvable.

### 32. Related Observatories (OPTIONAL)
None — no entries. Documented omission (SPASE ladder rule 5).

**Determination: SpiceyPy is mission/observatory-agnostic.** Same reasoning as
Field 31 — mission identity is supplied entirely by the user's kernels (SPK/CK/SCLK), not by the
software. SpiceyPy implements no mission's data conventions, is not a mission-team tool, and accesses
no mission archive. The mission names in the repository (Cassini, Mars Express, Voyager, Galileo,
Mars Global Surveyor, the Saturn-barycenter Cassini position example in `docs/exampleone.rst`, and Mars
2020 in the docs example gallery added after v8.3.0, read at `fb98550`) all occur inside NAIF's translated
tutorial lessons or documentation examples, which the Field 31/32 relevance gate excludes as tutorial,
demo and gallery name-drops and as platforms the software *could* support. Consistent with Field 17
being empty (no observatory-specific data source) — the two fields agree.
No related entity reaches the resolution ladder. Should a future release add mission-specific
support, those entries should be resolved against the then-current SPASE-backed HSSI vocabulary.

### 33. Logo (OPTIONAL)
Not found.

No logo exists. The repository's only image is
`docs/images/exampleoneplot_min.png` (a plot from the Cassini position example, not a logo); the
README uses only shields.io status badges; the PyHC community-registry entry for SpiceyPy has no
`logo` field (unlike several other PyHC entries); and `docs/conf.py` sets no Sphinx logo. The GitHub
owner avatar is a personal account image, not a software logo, so it is not used.
