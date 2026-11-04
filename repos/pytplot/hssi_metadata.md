# HSSI Metadata Extraction Results

**HSSI Software ID:** b703fe9b-09b0-4f65-9388-527f7ab6a588
**Repository:** https://github.com/MAVENSDC/PyTplot
**Source Revision:** 2cd7b27b0c911850f4d8d71b613248e0d2dd9ec9
**Extraction Date:** 2026-11-03
**Validation Date:** 2026-11-03
**Validation Status:** PASS

---

## Scope note — read this before the field notes

**This entry records PyTplot's newest release line, `pytplot-mpl-temp` 2.2.79** (Field 12), and
**unqualified citations are at the Source Revision**, `2cd7b27`: the head of the branch
`matplotlib-backend` (2025-07-25) and the commit 2.2.79 was built from. That commit's `setup.cfg`
declares `name = pytplot-mpl-temp`, `version = 2.2.79`, and the `pytplot/` tree of the 2.2.79 sdist on
PyPI is byte-identical to the commit's `pytplot/` tree. The release line was never merged into the
default branch, so the repository's default branch lags it.

**Context: the default branch.** `master` (pinned for reference at
`f7fb3042898a52f8289b9d8c60ffae38949cad04`, last commit 2023-04-18) carries the older `pytplot`
distribution, 0.1 (2016-10-11) to 1.7.28 (2021-09-15), which plots through Qt/pyqtgraph and Bokeh. The
two lines share history up to the merge base `9a4fc7c` (2022-07-15); `matplotlib-backend` then holds 812
further commits. Passages that cite the 1.x line say `master` or `f7fb304`. The default-branch README
(`pip install pytplot`), the Read the Docs "latest" build, the Zenodo concept DOI and the PyHC registry
entry all present the 1.x line; the branch README presents this one: "This is the modified (matplotlib)
version of the pytplot package. This version is used in the pyspedas project, which is a python rewrite
of the IDL SPEDAS software." (`README.md:8`). Issue #159 ("Planning for pytplot 2.0", opened 2021-10-28
by GitHub account `ericthewizard`) proposed this matplotlib backend as "pytplot 2.0"; it was released
instead under the separate distribution name, imports as `pytplot`, and keeps `author = MAVEN SDC` and
`url = https://github.com/MAVENSDC/pytplot` in its `setup.cfg`.

**Both lines are now superseded by PySPEDAS.** PySPEDAS's README (`spedas/pyspedas` at
`1a019705da713355d828b8ab0081e82e82192edc`, "PyTplot" section) states: "Previous releases of PySPEDAS
depended on the external pytplot or pytplot-mpl-temp Python packages. Starting with PySPEDAS 2.0, these
external packages are no longer required -- their functionality is now included directly in PySPEDAS."
PySPEDAS 1.7.28 required `pytplot-mpl-temp>=2.2.78`. PySPEDAS 2.0.5 (2025-11-07) is the first PySPEDAS
2.0 release that is not a pre-release (2.0.2a1 and 2.0.4a1 preceded it), and it and every later
release declare no dependency on either distribution.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** Shawn Polson
- **Submitter Email:** shawn.polson@lasp.colorado.edu

Supplied by the user for this new submission (rule 4). HSSI holds a Person row `Shawn` / `Polson`
carrying ORCID https://orcid.org/0000-0003-0619-5745; the submitter's person is sent under exactly that
given/family split so it binds that row rather than minting a duplicate.

The addresses found in the source — `mavensdc@lasp.colorado.edu` (`setup.cfg` `author_email`),
`jwl@ssl.berkeley.edu` (the branch README's contact, Jim Lewis) and `harter@lasp.colorado.edu` (Bryan
Harter, named in both READMEs) — are correspondence context only and never this field's value (rule 2).

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.3601517

- **What it is.** The Zenodo concept ("all versions") DOI of the project's own GitHub-integration
  deposits. DataCite registers it as `resourceTypeGeneral: Software`, publisher Zenodo, with
  `IsSupplementTo https://github.com/MAVENSDC/PyTplot/tree/v1.7.28` and sixteen `HasVersion` children
  (v1.5.0 of 2020-01-08 through v1.7.28 of 2021-09-15). Rule 5 fires: concept DOI of a software
  deposit of this software, identified by the `IsSupplementTo` tree link to this repository.
- **Known cost: the concept presents an older version than Field 12.** Deposits stopped at v1.7.28
  while releases continued as `pytplot-mpl-temp` 2.x, which was never deposited. The concept resolves to
  the newest deposit, v1.7.28 (version DOI 10.5281/zenodo.5510606), titled "MAVENSDC/PyTplot: Bumping
  version to get metadata updates into PyPI", so the "Software" citation HSSI generates carries that
  title and version beside Field 12's 2.2.79. Rule 5 keeps the DOI regardless.
- **Source in the project's own files.** The DOI badge `https://zenodo.org/badge/latestdoi/68843190`
  (`README.md:2` on both branches) redirects to the version DOI 10.5281/zenodo.5510606; rule 3 maps a
  latest-version badge to its concept, which is this DOI. There is no `CITATION.cff`, `codemeta.json` or
  `.zenodo.json` on either branch.
- **No second concept DOI.** A free-text Zenodo search for `pytplot` and creator-keyed searches for
  `Harter, Bryan`, `Bryan Harter` and `MAVEN SDC` return this concept as the only PyTplot deposit (the
  creator searches also return the team's other deposits — cdflib, PyDIVIDE, posters and
  presentations — none of them PyTplot).
- The earlier (2025) extraction recorded the same concept DOI.

### 3. Code Repository (MANDATORY)
https://github.com/MAVENSDC/PyTplot

- Rule 7: the canonical base URL spelled as the GitHub API's `full_name` (`MAVENSDC/PyTplot`); the
  repository is not a fork, not archived, and answers without a redirect. Both release lines live in
  this one repository; the recorded line is on its `matplotlib-backend` branch, and a branch page URL is
  never the value.
- **Considered and not adopted: `https://github.com/MAVENSDC/pytplot`** (lower-case), the form in both
  branches' `setup.cfg` `url` and `meta.yaml`, the PyPI `home_page`/`project_urls`, the PyHC registry
  `code:` and the clone's git remote. GitHub serves both spellings of the same repository without a
  redirect; the `full_name` form is recorded because it is the canonical spelling and because three
  catalogue entries link to PyTplot under exactly this string in their Interoperable Software (PySPEDAS,
  SPEDAS and Helio-Lite), so those relations bind to this entry.
- `https://github.com/MAVENSDC/pyptlot` in `meta.yaml` `dev_url` is a typo and is not a repository.

### 4. Software Functionality (RECOMMENDED — treated as critical)
- Data Visualization
- Data Visualization: Line Plots
- Data Visualization: Spectrogram
- Data Visualization: 2D Slices
- Data Processing and Analysis
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Processing
- Data Processing and Analysis: File Format Conversion

Evidence at the Source Revision, by value:

- **Line Plots** — `pytplot.tplot()` hands every call without `qt=`/`bokeh=` to the matplotlib plotter
  (`pytplot/tplot.py:155`); `pytplot/MPLPlotter/lineplot.py` draws line panels, with error bars when a
  variable carries `dy` (lines 54–56), stacked on a common time axis.
- **Visualization: Spectrogram** — `pytplot/MPLPlotter/specplot.py` (`pcolormesh`, line 690), plus the
  interactive slice window that plots the spectrum under the cursor (`tplot(..., slice=True)`,
  `MPLPlotter/tplot.py:841-845`).
- **Visualization: 2D Slices** — for a variable with more than two dimensions, the public option
  `spec_slices_to_use` (`options.py:144-146`, handled at `:591-601`) picks an index along each extra
  dimension, and the plotter draws that two-dimensional slice as a spectrogram:
  `MPLPlotter/tplot.py:329-331` calls `tplot_utilities.reduce_spec_dataset`
  (`tplot_utilities.py:666-696`, `da.isel({dim: value})`). Exercised in
  `tests/test_docstring_examples.py:38`.
- **Time Series Analysis** — `pytplot/tplot_math/`: `tinterp`, `interp_nan`, `degap`, `makegap`,
  `deflag`, `tdeflag`, `clean_spikes`, `derive`, `subtract_average`, `subtract_median`, `time_clip`,
  `clip`, `crop`; documented on the branch's "Math Routines" page.
- **Processing: Spectrogram** — `pwr_spec`, `dpwrspc`/`tdpwrspc` ("Compute power spectra for a tplot
  variable", the dynamic power spectrum) and `pwrspc`/`tpwrspc` compute time–frequency or frequency
  arrays and store them as new tplot variables (arrays, not only figures; rule 9 admits both twins).
- **Data Reduction** — `avg_res_data` averages onto a coarser time resolution (`coarsen(...).mean()`)
  and `tsmooth`/`smooth` apply a boxcar average.
- **Processing** — arithmetic and restructuring routines: `add`, `subtract`, `multiply`, `divide`,
  `add_across`, `join_vec`, `split_vec`, `spec_mult`, vector `tdotp`, `tcrossp` and `tnormalize`, and
  the `tkm2re` unit conversion.
- **File Format Conversion** — readers for CDF (`importers/cdf_to_tplot.py`), netCDF
  (`netcdf_to_tplot.py`), MAVEN STS text files (`sts_to_tplot.py`) and IDL tplot save files
  (`tplot_restore.py`), and writers that hand the data on in another format: `tplot_ascii` writes CSV
  (imported as `from pytplot.exporters.tplot_ascii import tplot_ascii`, not re-exported at the package
  top level; the changelog calls it "the tplot_ascii tool", `docs/source/introduction.rst:86`) and
  `tplot_save` writes a Python pickle.

**Considered and not selected.**
- **`Data Visualization: Web-Based`** — this release has no Bokeh output: `tplot(..., bokeh=True)` only
  logs "This version of pytplot no longer supports Bokeh plotting." (`pytplot/tplot.py:201`); there is
  no `HTMLPlotter` package and no bokeh dependency.
- **`Data Visualization: 2D Graphics`, `Orbit Plots`, `3D Graphics`** — the map and altitude plots
  (`QtPlotter/TVarFigureMap.py`, `TVarFigureAlt.py`) and the Mars position windows
  (`AncillaryPlots/position_mars_2d.py`, `position_mars_3d.py`) are still in the tree but no public call
  reaches them (rule 3): `pytplot/__init__.py:15` sets `using_graphics = False` unconditionally, so
  `QtPlotter` is never imported; `tplot(..., qt=True)` prints "Qt was not successfully imported…" and
  returns (lines 178–180) unless `save_file` is given, and then calls the unimported Qt code; the Mars
  windows need `tplot_utilities.get_available_qt_window`, whose window lists exist only when graphics
  are on; and pyqtgraph is not a dependency. The spectrogram's pcolormesh image is carried by
  `Spectrogram`. These three values, like `Web-Based`, held for the 1.x line at `f7fb304`, where Bokeh
  wrote interactive HTML and notebook output and the Qt plots and Mars windows were live (Field 12).
- **`Data Processing and Analysis: 2D Slices`** — the slice extraction exists only to draw the slice;
  `reduce_spec_dataset` is an undocumented helper, and the user receives a figure, not an array
  (rules 3 and 9).
- `Data Processing and Analysis: Data Access and Retrieval` — PyTplot downloads nothing. The only
  network call in the package is `tplot_utilities.compare_versions()`, which asks PyPI for the `pytplot`
  distribution's version list. Every reader takes a local file the user names. Rule 8's example says a
  package that *reads* MMS data is this row, but the classification reference defines the row as
  "Downloading or querying data from remote archives", and the row exists for searchers looking for
  software that fetches data for them. A reader of local files in one mission's format does not fetch
  anything. Its reading is carried by `File Format Conversion` here, and by Fields 17, 18 and 32. The
  earlier (2025) extraction's value is rejected.
- `Data Processing and Analysis: Analysis` — no routine derives a physical quantity; vector dot and cross
  products, normalization and unit conversion are generic operations, carried by `Processing`.
- `Data Processing and Analysis: Energy Spectra` — the power-spectrum routines are frequency spectra;
  particle energy spectra are displayed, not computed.
- `Data Visualization: Mission-Specific`, Hodograms, Movies, Spacecraft Formation Plots, ML/AI — no
  such plot types.
- `Coordinate Transforms` (all children) — no frame transforms; `tkm2re` converts units only.
- `Mission-related` (all children) — an analysis and plotting library, not part of a mission's ground
  system or archive-production chain (rule 8); its reader for the MAVEN mission's STS files reads
  finished data files and is carried by Fields 17, 18 and 32. `Models and Simulations` and `Servers and
  Environments` — none.

### 5. Related Region (RECOMMENDED — treated as critical)
Not found

Evidenced empty. PyTplot stores, manipulates and plots whatever time series the user loads, and behaves
identically whatever physical region the data describe; no module computes, models or analyses the
physics of any region (rules 2 and 4).

- **MAVEN STS reader.** `sts_to_tplot` reads a text format its docstring attributes to the MAVEN mission
  (Field 32) by loading whatever columns the file's label declares; it does nothing with Mars physics.
  A region row is not a planet or mission filter (rule 4), so `Mars Magnetosphere` and `Planetary
  Magnetospheres` were considered and rejected.
- **Mars position windows** (unreachable in this release, Field 4) only ever drew where a spacecraft
  *is* relative to Mars — where the instrument sits, not where the physics happens (rule 4).
- `tkm2re` converts between kilometres and Earth radii; a unit is not region physics.
- **Registry facets.** The PyHC registry tags PyTplot `solar`, `magnetosphere`,
  `ionosphere_thermosphere_mesosphere` and `general`. Rule 3 makes these non-evidence. The earlier
  (2025) extraction's `Earth Atmosphere`, `Earth Magnetosphere`, `Interplanetary Space` and
  `Solar Environment` rested on those tags and on the MAVEN SDC's mission context; all four are rejected.
- **Test fixtures and examples** (MAVEN EUV and SWEA, MMS FPI and THEMIS SCM CDF files, MMS `.tplot`
  files, a GOES-15 XRS netCDF file) exercise the generic readers and plotting; they are not scope.

All 24 live Region rows were walked; none applies.

### 6. Authors (MANDATORY)

1. **MAVEN SDC** | Identifier: none (no ROR) | Affiliation: Laboratory for Atmospheric and Space
   Physics (https://ror.org/01fcjzv38)
2. **Bryan Harter** | https://orcid.org/0000-0002-3908-9001 | Laboratory for Atmospheric and Space
   Physics (https://ror.org/01fcjzv38)
3. **Elysia Lucas** | https://orcid.org/0009-0000-0784-8571 — **the new submission names her by given
   and family name only, with no identifier; the ORCID reaches her Person row through an update that
   selects that row (see below)** | Affiliation: none asserted
4. **Eric Grimes** | https://orcid.org/0000-0001-5756-8789 | Affiliation: none added (see below)
5. **Julie Barnum** | https://orcid.org/0000-0001-8755-0694 | Laboratory for Atmospheric and Space
   Physics (https://ror.org/01fcjzv38)
6. **Nick Hatzigeorgiu** | Identifier: none | Affiliation: none asserted
7. **Takanobu Amano** | https://orcid.org/0000-0002-2140-6961 | The University of Tokyo
   (https://ror.org/057zh3y96)
8. **Xiangning Chu** | https://orcid.org/0000-0003-4109-0770 | Laboratory for Atmospheric and Space
   Physics (https://ror.org/01fcjzv38)

**Attestation.** The author list is the creator list of the project's own Zenodo deposits (rule 8).
Every one of the sixteen deposits lists a subset of the same nine creator strings; from v1.7.16 on all
nine appear, in this order: `MAVEN SDC` (LASP), `Bryan Harter` (LASP), `Elysia Lucas`, `supervised`
(UCLA Institute of Geophysics and Planetary Physics), `jibarnum`, `Nick H`, `nikos15`,
`Takanobu Amano` (The University of Tokyo), `X. N. Chu` (LASP). The nine strings resolve to seven
people and one organization, in that order; the two Hatzigeorgiu accounts are merged at the position of
the first. `setup.cfg` (`author = MAVEN SDC`, on both branches) and the LICENSE ("Copyright (c) 2018
MAVEN SDC") attest the organization. The eight person creators map one-to-one onto the GitHub accounts
that had committed to the default branch by the last deposit (`bryan-harter`, `esalvolucas`,
`ericthewizard`, `jibarnum`, `nickssl`, `nikos15`, `amanotk`, `xnchu`).

**The recorded release line adds no author source.** `pytplot-mpl-temp` has no Zenodo deposit, no
`CITATION.cff` and no AUTHORS file, and its `setup.cfg` keeps `author = MAVEN SDC`. Its README names Jim
Lewis as the contact ("If you have any suggestions or notice any problems, don't hesitate to contact Jim
Lewis", `README.md:60`) and says "The original version of pytplot was developed by Bryan Harter"
(line 62). A correspondence contact is not an author (rule 4), and the line's committers —
`jameswilburlewis` / `Jim Lewis` above all, with `Alexander Drozdov (Sasha)`, `clrussell90404`,
`jwu` / `Jiashu Wu`, `Marc Pulupa`, `shuji-onosawa`, `Beforerr` and `Jim McTiernan` (git author names
as they appear) — are named as authors by no PyTplot source (rule 5). Several of them are credited as
PySPEDAS authors, which is where that code now lives. On `master`, `Jim McTiernan` (`jimm02`) and
`rale8469` are likewise committers only.

**Identity resolution of the handle-like creator strings.**
- **`supervised` → Eric Grimes.** GitHub's commit API attributes commits git-authored
  `supervised <egrimes@igpp.ucla.edu>` (e.g. `9a4fc7c`) to account `ericthewizard` (id 4745136), and
  attributes commits git-authored `Eric Grimes <egrimes@igpp.ucla.edu>` in this same repository
  (e.g. `0fa9bd7` on `matplotlib-backend`) to the same account. The Zenodo affiliation, "UCLA Institute
  of Geophysics and Planetary Physics", matches that `igpp.ucla.edu` address, and `ericthewizard` is the
  only contributor account not otherwise mapped. The GitHub account whose login is `supervised` (id
  152027414) was created on 2023-11-25, years after these deposits, and is a different person; it is not
  this creator. (The CDFlib dossier left the same Zenodo string unresolved because cdflib's own history
  has no `supervised` commit; this repository supplies that evidence.)
- **`jibarnum` → Julie Barnum.** The commit API attributes commits git-authored
  `Julie Barnum <julieirene17@gmail.com>` (e.g. `heliophysicsPy/standards` `99e07c2`) to account
  `jibarnum` (id 23218684), the same account and address as this repository's `jibarnum` commits.
- **`Nick H` and `nikos15` → one author, Nick Hatzigeorgiu.** The two Zenodo creators are two GitHub
  accounts of one person. `Nick H` is the profile display name of account `nickssl` (id 34072991);
  `nikos15` (id 15306172) is a login with no display name.
  - In this repository, `nickssl`'s commits are git-authored `nickssl <nikos@berkeley.edu>` and
    `Nikos H <nikos@berkeley.edu>` (e.g. `046f970`), and `nikos15`'s as
    `nikos15 <nick.hatzigeorgiu@gmail.com>` (e.g. `1cf872e`).
  - In `spedas/pyspedas`, the commit API attributes a commit git-authored
    `Nikos H <nick.hatzigeorgiu@gmail.com>` (`5c10085`) to `nikos15`, so both accounts write the same
    git name.
  - The project's own changelog names him: "Thanks to Nick Hatzigeorgiu for finding / solving the bug"
    (`pytplot/version.txt:72` at `f7fb304`, 1.6.5), and PySPEDAS's `CITATION.cff` (at `1a019705`) lists
    `Hatzigeorgiu, Nick` (University of California, Los Angeles).
  - No commit is git-authored under the full name "Nick Hatzigeorgiu", so Field 6 rule 2's literal test
    for asserting a personal name from a handle is not met. The name rests on the changelog credit, the
    commit address and the shared git name, and he is recorded by name as one author bound to the
    Person row HSSI holds for him; that was the user's decision. Two handle authors, `Nick H` and
    `nikos15` / `(GitHub)`, were weighed and rejected: they would list one person twice beside his
    existing named row.
- `Elysia Lucas`, `Takanobu Amano` and `X. N. Chu` are profile names of accounts `esalvolucas`,
  `amanotk` and `xnchu`; the commit API ties commits git-authored `Elysia Lucas`, `Takanobu Amano` and
  `Xiangning Chu`/`X. N. Chu` to them.

**Binding to existing Person rows (new submission).** HSSI held all seven people as Person rows serving other
entries (PySPEDAS, SPEDAS, CDFlib) before this submission, so none needs to be minted for PyTplot.
- Bryan Harter, Eric Grimes, Julie Barnum, Takanobu Amano and Xiangning Chu: rows carrying exactly the
  ORCIDs above, so sending the ORCID binds each row and keeps its stored name (Xiangning Chu, not the
  Zenodo string "X. N. Chu").
- Nick Hatzigeorgiu and Elysia Lucas: each had an identifier-less row, the only row with its split
  (Elysia Lucas's row takes her ORCID through the update described below; Nick Hatzigeorgiu's stays
  identifier-less). A new submission cannot select a row by id, so each is named without an identifier
  under the row's exact stored split (`Nick`/`Hatzigeorgiu`, `Elysia`/`Lucas`), which binds it
  (rule 16).
- MAVEN SDC: no existing row; split for a new author as `MAVEN` / `SDC` (rule 27, the project's own
  spelling). A ROR v2 search for "MAVEN Science Data Center" returns only unrelated data centres and a
  search for "MAVEN" returns nothing (the same query set returns LASP as `https://ror.org/01fcjzv38`), so
  the organization has no ROR; without one HSSI stores and renders it as a person-shaped author. The
  project writes "MAVEN SDC" throughout, so the acronym is kept as the name.

**Elysia Lucas's ORCID.**
- `0009-0000-0784-8571` passes rule 14. The record's employment is the University of Colorado Boulder
  (CIRES, Data Analyst), which matches her `elysia.lucas@lasp.colorado.edu` commit address (LASP is a
  University of Colorado Boulder institute). Its one work is in the same field: the 2026 preprint "GOES-R
  Series X-Ray Sensor (XRS): 2. On-orbit measurements and calibrations"
  (https://doi.org/10.22541/essoar.177092672.25576917/v1), added by her as "Elysia S. Lucas". Its other
  name, "Elysia Salvo Lucas", spells out her GitHub login `esalvolucas`. PySPEDAS's `CITATION.cff` lists
  `Lucas, Elysia` (LASP).
- `0009-0006-3139-2133` (ETH Zurich, Imperial College London) is a different person.
- **How the identifier reaches the catalogue (rules 16 and 15).** Before this entry was submitted, the
  catalogue already held a Person row `Elysia` / `Lucas`, the only row with that exact split, carrying no
  identifier and crediting her on PySPEDAS. It is the same person: PySPEDAS's `CITATION.cff` credits
  `Lucas, Elysia` (LASP), the institution of her PyTplot commit address. A new submission cannot select
  a Person row by `personId`, and an ORCID that no row carried would have created a second Person for
  her. So the submission binds the existing row by its exact given and family names, with no
  identifier, and the ORCID is attached by an update that selects that row by `personId`. After both
  writes the one Person row carries the ORCID on this entry and on PySPEDAS alike, which is correct for
  the same person.

**Other ORCID linkage (rule 14).**
- Bryan Harter `0000-0002-3908-9001`: the record's one work is "The Space Physics Environment Data
  Analysis System (SPEDAS)", and PySPEDAS's `CITATION.cff` carries this ORCID beside "Harter, Bryan"
  (LASP). **Rejected: `0000-0002-3148-121X`** ("BRYAN HARTER", University of Colorado Boulder, no works,
  no other linkage) — a same-name, same-institution record with nothing tying it to this work.
- Eric Grimes `0000-0001-5756-8789`, Julie Barnum `0000-0001-8755-0694` (LASP employment from 2018-06;
  works include the PyHC status paper) and Takanobu Amano `0000-0002-2140-6961`: each is carried beside
  the name in PySPEDAS's `CITATION.cff`. Fielded name searches return only these records for Barnum and
  Amano; for Grimes they also return `0009-0000-9732-4703` ("Eric Grimes Grimes", no employment, no
  works), which has no linkage and is not used.
- Xiangning Chu `0000-0003-4109-0770`: the record lists open-ended employment since January 2018 as a
  Research Associate at the Laboratory for Atmospheric and Space Physics, University of Colorado Boulder,
  and its works include "The Space Physics Environment Data Analysis System in Python".
- Nick Hatzigeorgiu — a fielded ORCID search on family name `Hatzigeorgiu` returns no record (the same
  query form returns Julie Barnum's record).

**Affiliations.**
- MAVEN SDC, Bryan Harter, Xiangning Chu: LASP, from the Zenodo creator affiliations ("LASP" expanded to
  the ROR display name); Chu's ORCID employment confirms LASP is current.
- Julie Barnum: LASP from her ORCID employment, which covers the period of her PyTplot commits (2019).
- Takanobu Amano: The University of Tokyo, from the Zenodo creator affiliation, and current (his GitHub
  profile, commit address `amano@eps.s.u-tokyo.ac.jp` and homepage "Takanobu Amano @ U-Tokyo"). HSSI held
  no Organization row for it before this submission; the ROR-keyed row takes ROR's display name.
- Eric Grimes: the Zenodo affiliation "UCLA Institute of Geophysics and Planetary Physics" was true when
  the deposits were made, but his ORCID records Adnet Systems from 2023-08 and his Person row also serves
  PySPEDAS and SPEDAS, so rule 19 keeps the years-stale UCLA affiliation off. (The department would in
  any case have been recorded as University of California, Los Angeles, rule 23.)
- Elysia Lucas and Nick Hatzigeorgiu: PyTplot's own sources give none; nothing is asserted.

**Superseded value.** The earlier (2025) extraction copied DataCite's parse of the creators verbatim
("supervised", "jibarnum", "Nick H", "nikos15", "X. N. Chu", nine entries); the resolutions above
replace it.

### 7. Software Name (MANDATORY)
PyTplot

Rule 8: the project's own sources disagree among themselves — the docs title "PyTplot's Documentation"
(`docs/source/index.rst`, both branches), the GitHub repository name `PyTplot` and the Read the Docs
project name write `PyTplot`; the README prose writes "Pytplot"; the branch README's heading is
"pytplot - matplotlib version"; the distribution names are `pytplot` and `pytplot-mpl-temp` and the import
name is `pytplot` — so the curated PyHC registry `name: PyTplot` (`_data/projects.yml`) decides.
Considered and not used: `pytplot` (import and 1.x distribution name), `Pytplot` (README prose),
`pytplot-mpl-temp` (the recorded release's distribution name; its "-temp" marks it as a stand-in for
the project's name, and an edition suffix is never appended, rule 6), "pytplot - matplotlib version" (a
README heading), and the Zenodo title "MAVENSDC/PyTplot: Bumping version to get metadata updates into
PyPI" (a generated locator plus release title, rule 1).

### 8. Description (MANDATORY)
**Value:**

> Pytplot is a python package which aims to mimic the functionality of the IDL "tplot" libraries for analysis and visualization of heliophysics time series data.
>
> This is the modified (matplotlib) version of the pytplot package. This version is used in the pyspedas project, which is a python rewrite of the IDL SPEDAS software.
>
> Pytplot can be used in python scripts, or interactively through IPython and the Jupyter notebook.
>
> Data is read into pytplot by using the "store_data" command. Each dataset is assigned a unique name by the user.
>
> The data is stored in a "tplot variable" class. The tplot variables contain all the information required to create a plot of the dataset. The details of the plot, such as axis titles, types, line colors, etc, can be changed through other functions in pytplot.

(The `> ` markers are dossier formatting; the value is the five paragraphs, each on one line.)

- **Source (rule 7).** No `CITATION.cff` exists. The value is the Source Revision's README, verbatim:
  the lead paragraphs (`README.md:6`, `:8`, `:10`) and, because the lead says little about how the
  package is used, the two whole paragraphs of its "How It Works" section (`:15`, `:17`) in the
  project's order. The README's installation and contact sections are not used. The source's double
  spaces after full stops are normalized to single spaces; nothing else is changed.
- **Claims tested against the code at the Source Revision.** matplotlib plotting
  (`pytplot/MPLPlotter/`, the default `tplot()` path), notebook and script use (`plt.show()`), PySPEDAS's
  use of this line (PySPEDAS 1.7.28 required `pytplot-mpl-temp>=2.2.78`), `store_data` and the tplot
  variable with per-variable plot options (`options`) all hold.
- **Not used.** The docs introduction (`docs/source/introduction.rst:9-11`, the same text as on the 1.x
  line) says "It can plot using either Qt via pytqtgraph, or using HTML files via Bokeh", which this
  release does not do (Field 4); rule 2 keeps that claim out, and its "What does it do?" list adds
  nothing the README lead and the structured fields do not carry. `setup.cfg` `description` ("A python
  version of IDL tplot libraries") is too thin.
- **Superseded values.** The earlier (2025) extraction's composed text ("…provides comprehensive support
  for time series analysis operations including interpolation, resampling, power spectra calculation…")
  was not written by the project; rule 7 forbids composed prose. The 1.x line's README and docs
  introduction are not the source either: their Bokeh HTML and Qt claims do not hold for 2.2.79.

### 9. Concise Description (OPTIONAL)
Based on IDL tplot, plots and manipulates time series data

58 characters. The PyHC registry `description:` for PyTplot (`_data/projects.yml`, the community list),
used verbatim. It is the first source in rule 6's order, and it names what the software does.

- **Why the field is filled.** The user decided that every new entry carries both a concise
  description and a description. Not taken: rule 6's empty outcome. That outcome would have left the
  field empty because Field 8's opening sentence (159 characters) already works as a preview.
- **Rule 2.** Every claim holds for the recorded 2.2.79 line. It is modelled on IDL tplot (the README:
  "aims to mimic the functionality of the IDL "tplot" libraries"). It plots time series through the
  matplotlib plotter. It manipulates them with the `tplot_math` routines (Field 4). The sentence names no
  plotting backend, so the 1.x line's Bokeh and Qt plotting is not implied.
- Rules 1, 3 and 4 do not fire: the sentence is no autofill text, is under 200 characters and has no
  spelling or grammar error.
- **Considered and not used.** The recorded line's package `description` (`setup.cfg` of
  `pytplot-mpl-temp`), "A python version of IDL tplot libraries", and the GitHub description, "A python
  version of the IDL tplot libraries". Both say only what the software imitates, not what it does, and
  rule 6 prefers the candidate that names what distinguishes the software. The README has no separate
  one-line tagline; its first sentence is Field 8's opening.
- The earlier (2025) extraction's composed sentence is superseded.

### 10. Publication Date (RECOMMENDED)
2016-10-11

Rule 4, anchor (a): the first PyPI upload of PyTplot (distribution `pytplot`, version 0.1,
`2016-10-11T22:25:25Z`; that release's metadata gives author MAVEN SDC and
`home_page http://github.com/MAVENSDC/Pytplot`). Rule 2's lineage clause applies: the recorded
`pytplot-mpl-temp` line grew out of the same repository history (merge base `9a4fc7c`), so the earlier
distribution's first public date is this software's publication date; `pytplot-mpl-temp` 2.0.0
(2022-01-26) is a later release, not a first one.

- Considered: anchor (b), 2016-09-21 — the repository's `created_at`, the same day as its root commit
  `90e2366` ("Initial Commit"). A first release exists, so rule 4 prefers it.
- Rejected: the earlier (2025) extraction's 2020-01-08, the DataCite `created` date of the first Zenodo
  deposit, made after the software had been public for over three years (rule 1).

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Rule 1: Field 2 is a Zenodo DOI, and DataCite's `publisher` for it is "Zenodo". Zenodo has no ROR; CERN's
ROR identifies the operator and is not a substitute. The catalogue's Organization row `Zenodo` carries the
identifier `https://zenodo.org`, so this binds it. PyPI and the `mavensdc` Anaconda channel are
distribution channels, never the publisher (rule 6).

### 12. Version (RECOMMENDED)
- **Version Number:** 2.2.79
- **Version Date:** 2025-07-25
- **Version Description:** Not found
- **Version PID:** Not found

**The release line recorded is `pytplot-mpl-temp`, the newest one** (the user's decision; see the
rubric gap below).
- **Number.** 2.2.79 is the newest upload of `pytplot-mpl-temp` (wheel and sdist, neither yanked nor a
  pre-release), built from the Source Revision (scope note). The line runs from 2.0.0 (2022-01-26)
  through 2.2.79 in 146 releases, continuing the version series after `pytplot` 1.7.28, and has no git
  tags and no GitHub releases.
- **Date.** With no tag and no release object, the release event is the PyPI upload (rule 7): wheel
  `2025-07-25T23:02:30Z`, sdist `23:02:48Z`, the same UTC day as the commit that set 2.2.79
  (`2025-07-25T22:58:04Z`).
- **Description.** There is no release title or body, and the project's changelog
  (`pytplot/version.txt`, mirrored in `docs/source/introduction.rst`) stops at 1.7.22. Commit subjects are
  never a release description (rule 15), so the field is empty (rule 16).
- **PID.** No Zenodo deposit exists for any `pytplot-mpl-temp` release; the newest deposit is v1.7.28
  (rule 18).

**Considered and not chosen: the `pytplot` distribution's 1.7.28.** Its values would be 1.7.28, dated
2021-09-15 (GitHub release `published_at` 2021-09-15T19:35:41Z, PyPI 19:39:16Z), with an empty description
(its release title "Bumping version to get metadata updates into PyPI" is a packaging chore, rule 14)
and PID https://doi.org/10.5281/zenodo.5510606. It is the newest release of the distribution the
default branch, its README (`pip install pytplot`), the Read the Docs "latest" build, the Zenodo concept
and the PyHC registry present, and `master` has 47 unreleased commits after its tag. It was not chosen
because the entry records the newest release line, which is `pytplot-mpl-temp`.

**Rubric gap.** Rule 3 counts "a PyPI upload of the project's package … built from any branch", and the
preamble says a PyPI upload of "the project's own package" needs no lineage check. No written rule
decides whether a second distribution name, built from a non-default branch and imported under the same
package name, is "the project's own package"; the "One entry, two packages" clause addresses separately
packaged components with independent version histories, which this is not.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

Rules 4 and 5: a pure-Python package (`python_requires = >= 3.9`, classifier
`Programming Language :: Python :: 3`; the wheel is `py3-none-any`, and the package tree holds no
compiled sources). `Python 2.x` is not targeted. The TypeScript embedded in the 1.x line's Bokeh custom
models does not exist in this release (no `HTMLPlotter`); the default branch's development-container
Dockerfiles are build tooling.

### 14. Reference Publication (OPTIONAL)
Not found

Evidenced empty. The project gives no citation guidance: no `CITATION.cff`, no README or docs "Citing"
section on either branch; the only scholarly pointer is the Zenodo DOI badge (a software DOI, rule 1).

- **Grimes et al. (2022), "The Space Physics Environment Data Analysis System in Python", Frontiers in
  Astronomy and Space Sciences, https://doi.org/10.3389/fspas.2022.1020815** — written by PyTplot
  developers (Grimes, Harter, Hatzigeorgiu, Chu among the authors) and describing PyTplot in its
  Section 2.1 ("Tplot"), but its subject is PySPEDAS, the package PyTplot feeds. Rule 5 fires; it is
  recorded in Field 27 instead (Field 27 rule 3).
- AGU Fall Meeting abstracts by Harter (2017, 2018, 2019) and Grimes (2018), and the 2017 Planetary Data
  Workshop abstract by DeWolfe et al., describe PyTplot but are meeting abstracts (rule 2); no poster or
  paper of them is deposited on Zenodo.
- Angelopoulos et al. (2019, Space Science Reviews, SPEDAS) mentions pytplot variables only in a
  future-plans paragraph and is about SPEDAS.

### 15. License (RECOMMENDED)
- **License:** MIT License

Rule 3: `LICENSE` at the Source Revision is the MIT text ("Copyright (c) 2018 MAVEN SDC"), identical to
the default branch's; GitHub detects `MIT`; the README says "Released under the MIT license."; `meta.yaml`
says `license: "MIT"`. The live row name is `MIT License`. Not used: the Zenodo deposits' licence id
`other-open` and DataCite's "Open Access" rights string, which are placeholders (rule 7). `setup.cfg`
sets only `license_file`, so PyPI shows no licence; that is a packaging gap, not a licensing fact.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- tplot
- maven
- lasp
- spedas
- power spectra
- pyhc package

- **Project-declared (rule 9):** `setup.cfg` `keywords` are `tplot`, `maven`, `lasp`, `IDL`, `spedas`
  (the same on both branches). `maven`, `lasp` and `spedas` bind existing rows; `tplot` has no row (the
  nearest, `pytplot`, is this software's name, a different term) and is minted lower-case (rule 12).
  `maven` is supported by the MAVEN STS reader (`importers/sts_to_tplot.py`, Field 32) and the MAVEN test
  fixtures; `spedas` by the IDL-tplot save-file reader, the `spedas` colour bar and the PySPEDAS
  docstring examples.
- **Excluded: `IDL`** — rule 4: PyTplot contains no IDL code, and its IDL-adjacent facts already sit in
  Field 18 (`IDL.sav`) and Fields 29/30 (SPEDAS).
- **Domain term (rule 10):** `power spectra` (existing row) — `pwr_spec`, `pwrspc`, `tpwrspc`, `dpwrspc`
  and `tdpwrspc` compute power spectra of a time series.
- **PyHC marker (rule 15):** PyTplot is listed in `_data/projects.yml`, so `pyhc package` is added.
- **Rejected:** the registry tags `solar`, `magnetosphere`, `ionosphere_thermosphere_mesosphere`
  (rule 3; the software works in no particular domain, see Field 5) and `general` (rule 2); `time series`,
  `spectrograms`, `data visualization` (rule 6, carried by Field 4); `matplotlib`, `xarray`, `pytplot`
  (rule 7 dependencies, and the software's own name). The earlier (2025) extraction's list of fourteen
  terms (among them `IDL`, the registry tags, `heliophysics`, `space physics`, `bokeh` and `interactive
  plotting`) is superseded.

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific

Rule 8: `importers/sts_to_tplot.py`, exported at the package top level (`pytplot/__init__.py:158`), reads
the MAVEN mission's STS data files. Its docstrings say "The .sts file format is a text file format used
by the MAVEN mission." (lines 27 and 116), and its example loads MAVEN magnetometer Level 2 files
(`/maven/data/sci/mag/l2/2015/01/mvn_mag_l2_2015002ss1s_20150102_v01_r01.sts`, line 122). The
observatory is named in Field 32 (Field 32 rule 6).

- No other row applies. A sweep of `pytplot/` at the Source Revision for `urlopen`, `urlretrieve`,
  `requests.`, `ftplib` and `http(s)://` finds only documentation URLs in comments and docstrings and
  `tplot_utilities.compare_versions()`, which reads the `pytplot` distribution's release list from PyPI
  (rule 5: the package's own material). PyTplot reaches no archive, service or directory: every reader
  takes a local file the user supplies, and loading mission data from archives is what PySPEDAS does for
  this package (Field 30).
- The earlier (2025) extraction's `Other` is rejected.

### 18. Input File Formats (RECOMMENDED)
- CDF
- ISTP-Compliant
- netCDF3/4
- IDL.sav
- ascii
- Other

- **CDF** — `importers/cdf_to_tplot.py` via `cdflib`.
- **ISTP-Compliant** — the same reader is built on the ISTP conventions: "In general, the files should
  be ISTP compliant for this importer to work" (`cdf_to_tplot.py:27-28`), with `VAR_TYPE`, `DEPEND_0`
  and fill-value handling.
- **netCDF3/4** — `importers/netcdf_to_tplot.py` via `netCDF4.Dataset` (`netCDF4` is a declared
  dependency of this release).
- **IDL.sav** — `importers/tplot_restore.py` reads IDL `.tplot` save files with `scipy.io.readsav`:
  "This function is compatible with the IDL tplot_save routine" (line 22); `tests/test_tplot_restore.py`
  restores four MMS `.tplot` files.
- **ascii** — `importers/sts_to_tplot.py` reads STS (`.sts`) files, the text format its docstring
  attributes to the MAVEN mission: an `OBJECT … END_OBJECT` label followed by a whitespace-delimited
  ASCII data table whose columns the label names (`TIME_YEAR`, `TIME_DOY`, …). That is what the `ascii`
  row means; `Other` is not added for it, since it would name nothing distinct from `ascii`.
- **Other** — Python pickle save files, read back by `tplot_restore` from `tplot_save`. They are
  user-requested saves of data and plot options that a later session (or PySPEDAS) restores, not
  internal bookkeeping (rule 4).
- The test fixtures only confirm the readers. The earlier (2025) extraction's list (CDF, netCDF3/4,
  Other) is extended.

### 19. Output File Formats (RECOMMENDED)
- csv
- Other

- **csv** — `tplot_ascii` (`from pytplot.exporters.tplot_ascii import tplot_ascii`; "the tplot_ascii
  tool" in the changelog, `docs/source/introduction.rst:86`) writes a variable with
  `pandas.DataFrame.to_csv` (comma-separated, default extension `.csv`), plus a `_v` companion file of
  spectrogram bins. `ascii` is not added: the writer has no delimiter option and produces CSV only
  (Field 18 rule 7); the earlier (2025) extraction's `ascii` is superseded.
- **Other** — matplotlib figures written by `tplot(..., save_png=, save_eps=, save_svg=, save_pdf=,
  save_jpeg=)` (`MPLPlotter/tplot.py:819-839`, `plt.savefig`), and Python pickle save files
  (`tplot_save`). The 1.x line's Bokeh HTML output does not exist in this release.

### 20. Operating System (RECOMMENDED)
- Operating System Independent
- Linux

Rule 3: pure Python with no compiled extension (a `py3-none-any` wheel); `setup.cfg` classifier
`Operating System :: OS Independent` (the HSSI row is `Operating System Independent`). **Linux** — the
branch's CI workflows (`.github/workflows/unittest.yaml` and the two build workflows) run the test suite
`runs-on: ubuntu-latest`; GitHub no longer retains their run history.

- **Considered and not selected: `Mac` and `Windows`.** Their evidence belongs to the 1.x line: the
  conda packages the project's CI published for `osx-64`, `win-64` and `win-32` on its `mavensdc` channel
  are of the `pytplot` distribution (through 1.7.28); no conda package of `pytplot-mpl-temp` exists
  there, and the branch's publishing steps run only on tags, which this line never made. The Windows
  workaround in `pytplot/__init__.py:56-58` sits inside the Qt block this release never executes, and
  the "Windows bug fix" release titles are 1.7.13's and 1.7.14's. Rule 7: no OS by inference.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Rule 3: pure interpreted code with no architecture-specific dependency built by the project; the
2.2.79 wheel is `py3-none-any`.

### 22. Related Phenomena (OPTIONAL)
Not found

Evidenced empty. All seven rows were examined. PyTplot is a general time-series manipulation and
plotting technique (rules 3 and 4): no code detects, models or computes diagnostics of Coronal Heating,
Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind or X-ray emission.
The GOES XRS test fixture is a format example, not X-ray processing.

### 23. Development Status (RECOMMENDED)
Moved

- **Rule 1.** The recorded release line was folded into PySPEDAS 2.0. The pointer is the PySPEDAS
  README statement in the scope note, written by this line's own maintainers: Jim Lewis, the contact in
  this line's README, is PySPEDAS's contact in the PyHC registry, and as `jameswilburlewis` he committed
  this line's version bumps, among them 2.2.79 (`2cd7b27`). That
  statement is the project's own account of where its functionality now lives, so it is read as coming
  from the project. PySPEDAS 2.0.5 (2025-11-07) was the first PySPEDAS 2.0 release that was not a
  pre-release, and it declared no pytplot dependency. The authoritative continuation is PySPEDAS (Field
  29). The status was settled by the user's decision.
- **Considered and not selected.**
  - `Inactive`: rule 6 measured literally on the repository's default branch, `master`, whose last commit
    is `f7fb304` on 2023-04-18. It would tell a user that support continues "as time allows" for a line
    its maintainers have replaced.
  - `Active`: rule 6 measured on the recorded line's branch, whose last commit (2025-07-25) falls in the
    six-to-24-month band, with no stored value. That band assumes "a quiet stretch under two years is not
    evidence that development has stopped", and here the stop is stated.
- **Dated anchors for a later refresh.** `matplotlib-backend` last commit 2025-07-25 (`2cd7b27`, the
  2.2.79 build); `pytplot-mpl-temp` 2.2.79 on 2025-07-25; `pytplot` 1.7.28 on 2021-09-15; `master` last
  commit 2023-04-18. The repository is not archived and carries no repostatus badge.
- The trove classifier "Development Status :: 5 - Production/Stable" corroborates only that a stable
  release exists. The earlier (2025) extraction's `Active` is superseded.
- **Rubric gaps.**
  - Rule 6 and its trap measure "the default branch" and do not say what to measure when the recorded
    release line lives on a non-default branch.
  - Rule 1 does not say whether a successor's README, written by the same maintainers, counts as the
    pointer coming "from the project".

### 24. Documentation (RECOMMENDED)
https://pytplot.readthedocs.io/en/matplotlib-backend/

Rule 3: the project's own Sphinx documentation for this release line on Read the Docs. The branch
carries the Read the Docs configuration (`.readthedocs.yaml`, building `docs/source/conf.py`), and the
Read the Docs project `pytplot` (connected to `https://github.com/MAVENSDC/PyTplot.git`) serves an active
`matplotlib-backend` version built from this branch, documenting this line's API (its "Math Routines"
page covers `clean_spikes`, the dynamic power spectrum, vector products, `tkm2re` and smoothing; its
"Plotting" page covers interactive time selection). The URL is that version's landing page and answers
directly with no redirect.

- **Considered and not used: `https://pytplot.readthedocs.io/en/latest/`**, the README link on `master`
  and the PyHC registry `docs:`. It is built from `master` (revision `f7fb3042`) and documents the 1.x
  line's Bokeh and Qt plotting, so it does not document this package as released (rule 3).
- **Caveat.** The `matplotlib-backend` version's newest successful build is of `f8f7299` (2025-06-13);
  Read the Docs builds of later commits, including `2cd7b27`, failed, so the pages lag 2.2.79 by about
  six weeks. The branch README itself links no documentation.
- **Rubric gap.** Rule 6 prefers a site's default version (`/en/latest/`, `/en/stable/`) over other
  versions, and rule 3 requires the page to document this package. Neither says which applies when the
  default version documents a different release line from the one the entry records and a per-branch
  version documents the recorded one. Rule 3 decided it here.

### 25. Funder (OPTIONAL)
Not found

No source attributes funding to PyTplot or to the MAVEN SDC's work on it. Swept: every tracked text
file at `f7fb304` except the generated example assets (`docs/source/_images/*.html`,
`docs/pytplot_tutorial.html`, the tutorial notebook) — a case-insensitive word-initial search for nasa,
grant, funded, funding, award, sponsor and acknowledg finds only "granted" in the MIT licence text
(positive control: "Laboratory for Atmospheric" matches `README.md`); the Source Revision's README,
`setup.cfg` and docs (no match); and the Zenodo/DataCite records (no `grants`, no `fundingReferences`).

- **Rejected: NASA contracts NNG17PZ01C, NNG04EB99C and NAS5-02099.** They are named in the Funding
  section of Grimes et al. (2022), which reads "The core SPEDAS team acknowledges support from NASA
  contract NNG17PZ01C (for SPEDAS community support) to UCLA …". They fund SPEDAS community support, MMS
  SPEDAS plug-in development and THEMIS TDAS/SPEDAS infrastructure at UCLA, UCB and BU, and no sentence
  attributes them to PyTplot (rule 4).
- **Rejected:** Harter's 2020 HDEE proposal record "Integrating the python XArray library and the CDF
  file format" concerns cdflib. The MAVEN mission, the MAVEN SDC and LASP are named as the software's
  origin, never as a source of funding (rule 7).

### 26. Award Title (OPTIONAL)
Not found

No award is attributed to PyTplot by any qualifying source; see Field 25 for the sweep and the rejected
SPEDAS contracts.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.3389/fspas.2022.1020815
- https://doi.org/10.1029/2022GL100652
- https://doi.org/10.1029/2023JA031621
- https://doi.org/10.1029/2025GL118895

- **Grimes et al. (2022), "The Space Physics Environment Data Analysis System in Python", Frontiers in
  Astronomy and Space Sciences** — rule 3, a paper by PyTplot's developers about the platform PyTplot
  serves. It covers PySPEDAS; its Section 2.1 ("Tplot") describes PyTplot as the implementation of the
  tplot data model — its importers (CDF, netCDF, STS, IDL sav), routines (`store_data`, `get_data`,
  `tplot`, `options`, `crop`, `avg_res_data`) and plotting backends (Bokeh, Qt and matplotlib) — and its
  author-contribution statement says "BH contributed to the development of cdflib, PyTplot, as well as
  the MAVEN plug-in." Heuer et al. (2025), below, cite it for the pyTplot libraries. Not Field 14 (see
  there).
- **Heuer et al. (2022), "Calculating the Electron Diffusion Region Aspect Ratio With Magnetic Field
  Gradients", GRL** — rule 5, a statement naming the software for the paper's data processing:
  "Routines from the pySPEDAS and pyTplot libraries used to process the MMS data analyzed in this paper
  (Grimes et al., 2019) …" (the passage as ADS's full-text index shows it).
- **Krämer et al. (2023), "Waves in Magnetosheath Jets—Classification and the Search for Generation
  Mechanisms Using MMS Burst Mode Data", JGR Space Physics** — rule 5: its Data Availability Statement
  says "Data analysis was performed using the pyspedas package …, the pytplot package available at
  https://github.com/MAVENSDC/PyTplot, and the IRFU-Matlab analysis package".
- **Heuer et al. (2025), "Investigating the Dependence of Normalized Reconnection Rate on Upstream Plasma
  Parameters", GRL** — rule 5: "Routines used to process the MMS data analyzed in this paper are from the
  pySPEDAS and pyTplot libraries (Grimes et al., 2022)."
- **How Krämer et al. (2023) differs from the two Capannolo papers (weighed below).** Krämer's
  statement names three domain analysis packages — pyspedas, pytplot and IRFU-Matlab — each with its own
  repository URL, as the tools the paper's data analysis was performed with. The Capannolo statements name
  pytplot only as one entry in a parenthetical list of general Python libraries (numpy, pandas,
  matplotlib, xarray, tslearn, scikit-learn), which is a dependency list (rule 6).
- **The widely-used limit does not apply.** Rule 5 adds no use papers for widely used software such as
  Astropy or SunPy. PyTplot's citing literature is small — an ADS full-text search for "pytplot" returns
  only the papers and abstracts named in this section, plus the project's own Zenodo deposit — so each substantive use still tells a searcher
  where and how the package is used.

**Weighed and not added (rule 6, or ineligible under rule 1).**
- Capannolo et al. (2025), "Statistical Properties of Solar Wind Parameters Driving Relativistic
  Electron Precipitation", JGR Space Physics, https://doi.org/10.1029/2025JA034548. Its Data
  Availability Statement reads "We used PySPEDAS (Grimes et al., 2022) to load OMNI data (1-min
  resolution, level HRO2; Papitashvili & King, 2020) and other Python routines for analysis and plotting
  (numpy, pandas, matplotlib, xarray, pytplot, tslearn, scikitlearn)." Nothing else in the paper names
  pytplot.
- Capannolo et al. (2026), "Solar Wind Drivers of Relativistic Electron Precipitation: A Comparison
  Between Coronal Mass Ejections and High-Speed Streams", JGR Space Physics,
  https://doi.org/10.1029/2026JA035528. Its Availability Statement reads "We used PySPEDAS (Grimes, 2022)
  to load OMNI data (1-min resolution, level HRO2; Papitashvili & King, 2020) and other Python routines
  for analysis and plotting (numpy, pandas, matplotlib, xarray, pytplot, tslearn, scikit-learn)." Nothing
  else in the paper names pytplot.
- Both Capannolo papers name pytplot only inside a list of Python libraries. That is a rule 6 mention
  (a list of tools or dependencies), not a rule 5 credit of the package for the paper's results; the
  user decided these two cases.
- Barnum et al. (2023), "Python in Heliophysics Community (PyHC): Current status and future outlook",
  Advances in Space Research — lists PyTplot among PyHC packages.
- Ringuette et al. (2023), "The DIARieS ecosystem…", Advances in Space Research — proposes "offering
  pyTplot as a widget-based application" as future work.
- Fung et al. (2023), "SPASE metadata as a building block of a heliophysics science-enabling framework",
  Advances in Space Research — a metadata-framework paper whose body names pytplot. Its full text was
  not available to check the passage, and nothing in the paper's subject suggests results built with
  PyTplot.
- Angelopoulos et al. (2019), "The Space Physics Environment Data Analysis System (SPEDAS)", Space
  Science Reviews — names pytplot variables in a future-plans paragraph.
- AGU abstracts 2017AGUFMIN33A0105H, 2018AGUFMIN11B0621H, 2019AGUFMSH41C3312H (Harter),
  2018AGUFMIN11B0629G (Grimes), and 2017LPICo1986.7079D (DeWolfe et al.) — meeting abstracts, never
  eligible; no deposited poster or paper exists for them.
- 2020hdee.prop...14H (Harter) — a proposal record about cdflib.

### 28. Related Datasets (OPTIONAL)
Not found

Evidenced empty. PyTplot's readers target formats, and its one mission-specific reader targets a
mission's file format rather than a dataset. It ships only a sample `.tplot` file for its examples
(`pytplot/sampledata/test_data.tplot`) and produced no data release.

- **Considered and not used: MAVEN magnetometer data.**
  - `sts_to_tplot` reads any STS file whose label declares its columns. The only dataset it names is in
    its docstring example (MAVEN MAG Level 2 sun-state 1-second `.sts` files), so the reader is not
    "built to read" one dataset (rule 3).
  - The DOI DataCite registers for MAVEN MAG Level 2 sun-state 1-second data,
    https://doi.org/10.48322/b9da-ph25 ("MAVEN Magnetometer (MAG) Magnetic Field and Orbital Position,
    Sun-State and Payload Coordinates, Level 2 (L2), 1 s Data", publisher Space Physics Data Facility),
    identifies the SPDF dataset, not the PDS `.sts` release the example names.
- **Considered and excluded:** the datasets of the test fixtures (`tests/testfiles/`).
  - They are MAVEN EUV Level 2 bands, MAVEN SWEA Level 2 survey spectra, MMS FPI burst moments, THEMIS-A
    Level 1 search-coil, GOES-15 XRS 2-second, and MMS FPI variables saved as `.tplot` files.
  - They exercise the generic CDF, netCDF and tplot-save readers, and no reader is written for any of
    them (rule 3).

### 29. Related Software (OPTIONAL)
- https://spedas.org/downloads
- https://github.com/spedas/pyspedas

- **SPEDAS (IDL) — `https://spedas.org/downloads`**, the code repository URL the SPEDAS catalogue entry
  stores (rule 11). PyTplot is a reimplementation of the IDL tplot library, which SPEDAS distributes
  (`idl/general/tplot/` in `spedas/bleeding_edge` at `0e909ceb47274c09f9fb8ac5b87df4a368274684`): the
  README says it "aims to mimic the functionality of the IDL "tplot" libraries" (`README.md:6`) and the
  docs say its helper functions "were basically mapped one-to-one from IDL routines"
  (`docs/source/helper_functions.rst:4`). Rule 9, predecessor and equivalent named by the project.
  Passed over (rule 13): SPEDAS's concept DOI https://doi.org/10.5281/zenodo.14919975 and the GitHub
  mirror `https://github.com/spedas/bleeding_edge`.
- **PySPEDAS — `https://github.com/spedas/pyspedas`**, the PySPEDAS entry's stored URL.
  - It is the companion this release line was built for: "This version is used in the pyspedas project
    … Since this version is designed to be used with pyspedas, you can also install it by installing
    pyspedas" (`README.md:8`, `:33`), and the README links PySPEDAS under "Additional Information".
  - It is also the successor that now carries this line's functionality and the location `Moved` points
    to (Field 23). The statement comes from PySPEDAS's developers, who maintained this line (rule 4).
  - Passed over: concept DOI https://doi.org/10.5281/zenodo.17634923.
- Both also appear in Field 30, on independent grounds (an exchange of tplot variables and save files).
- **Considered and excluded:**
  - cdflib: the CDF reader's dependency. A file format read through a library is Field 18, and "same
    organisation" is a blanket justification.
  - pysat: the earlier (2025) extraction listed it because both are PyHC packages, a blanket
    justification.
  - matplotlib, xarray, netCDF4: plain dependencies (Tier A/B).
  - The earlier extraction's IDL tplot entry ("Commercial software, no DOI") is recorded here as SPEDAS.
  - PyDIVIDE (`https://github.com/MAVENSDC/Pydivide`) as a code origin: at `f7fb304`, the
    `sts_to_tplot.py` header points to it. That header is gone at the Source Revision, and one copied
    file is not a distinguishing origin. See also Field 30.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/spedas/pyspedas
- https://spedas.org/downloads
- https://github.com/pydata/xarray

- **PySPEDAS** — the field's own worked example (exchanges tplot variables).
  - PySPEDAS's core load routines "load the data files into PyTplot variables" (Grimes et al. 2022,
    Section 2.2, "Load routines"), and PySPEDAS 1.7.28 declared `pytplot-mpl-temp>=2.2.78`.
  - This release's docstring examples call its routines through the `pyspedas` namespace (e.g.
    `pytplot/tplot_names.py`), and its docs build installs PySPEDAS (`docs/requirements.txt`).
  - The two share the `tplot_save`/`tplot_restore` save format. PySPEDAS's own record lists PyTplot in its
    Interoperable Software too.
- **SPEDAS (IDL)** — `tplot_restore` reads the `.tplot` files IDL SPEDAS's `tplot_save` writes
  (`importers/tplot_restore.py:22`, `readsav`), a cross-language bridge to a named domain tool; from the
  other side, SPEDAS's Python validation tests import `pytplot` (`store_data`, `tplot_rename`), as the
  SPEDAS record documents. Stored-URL form as in Field 29.
- **xarray — `https://github.com/pydata/xarray`** (Tier B, admitted under rule 4).
  - The documented interchange type is the DataArray: `"Tplot variable" is really just a fancy name for
    an Xarray DataArrray object` (`docs/source/tplot_variables.rst:20`, the source's spelling). The page
    introduces this as "good information to know" for using tplot variables in other libraries.
  - `get_data(name, xarray=False, ...)` returns the DataArray when asked (`pytplot/get_data.py:12`).
  - Passed over: concept DOI https://doi.org/10.5281/zenodo.598201.
- **Considered and excluded: PyDIVIDE — `https://github.com/MAVENSDC/Pydivide`** ("A plotting tool for
  MAVEN in-situ key parameter data"; concept DOI https://doi.org/10.5281/zenodo.3601515). It is an
  exchange partner of the 1.x line, not of this release.
  - It declares `install_requires=['pytplot', 'pyspedas']`: the `pytplot` distribution, which installs
    the same import package as `pytplot-mpl-temp`.
  - `pydivide/plot.py` builds tplot variables and links them to MAVEN altitude and MSO position variables
    for PyTplot's Qt altitude and Mars-position plots, which 2.2.79 cannot draw (Field 4).
  - Checked at `MAVENSDC/Pydivide` `4aaf932138f1dfc2f4db2e90369a9f6e8bde10b0`, last pushed 2020. For the
    1.x line it would qualify under rule 7, as an exchange seen from the other side.
- **Considered and excluded:**
  - Helio-Lite, which lists PyTplot in its own Interoperable Software. From PyTplot's side there is no
    exchange: Helio-Lite is a deployment environment that installs PyTplot and ships a demonstration
    notebook of PyTplot itself (`examples/PyHC/pytplot_demo.ipynb`). The exchange its record cites is
    between PySPEDAS and PyTplot.
  - pysat (from the earlier extraction): a blanket "PyHC" justification.
  - cdflib, netCDF4, scipy: formats read through a library (Field 18).
  - matplotlib, numpy, pandas: Tier A.
  - MavenPy (in the catalogue) does not use PyTplot.

### 31. Related Instruments (OPTIONAL)
Not found

Evidenced empty.
- **MAVEN magnetometer — row `https://spase-metadata.org/SMWG/Instrument/MAVEN/MAG` ("MAVEN
  Magnetometer, MAG, Instrument") — considered and not used.**
  - The STS reader passes rule 1 because it parses a format the project attributes to a mission. Its
    target is stated at the platform level: "The .sts file format is a text file format used by the
    MAVEN mission." (`importers/sts_to_tplot.py:27`, `:116`).
  - The magnetometer is named only by the docstring's example file paths (line 122). Docstring example
    values are not support (rule 3), and a single example is not expanded into an instrument row
    (rule 7). The mission is recorded in Field 32.
- **MAVEN SWEA and MAVEN EUV** — real files of their Level 2 products are test fixtures for the generic
  CDF reader (rule 3). Rows `https://spase-metadata.org/SMWG/Instrument/MAVEN/SWEA` ("MAVEN Solar Wind
  Electron Analyzer, SWEA, Instrument") and `…/SMWG/Instrument/MAVEN/LPW/EUV` exist and are not used.
- **GOES-15 XRS, MMS FPI, THEMIS SCM** — further test fixtures (`…/SMWG/Instrument/GOES/15/XRS` not
  used).

Sweep: the production InstrumentObservatory vocabulary (every row SPASE-identified, no `.html` orphans
at the time of the sweep) was searched on `name`, `abbreviation`, `identifier` and `definition` for
`MAVEN`, `SWEA`, `EUV`, `MAVEN/MAG`, `MAVEN Magnetometer`, `Mars Atmosphere and Volatile` and `GOES/15`
(positive controls: the rows named here; `MAVEN/MAG` also finds the CNES/CDPP-AMDA twin "Fluxgate
magnetometer"), with a nonsense token returning 0.

### 32. Related Observatories (OPTIONAL)

| Observatory name (as in the vocabulary) | SPASE identifier |
|---|---|
| Mars Atmosphere and Volatile EvolutioN | https://spase-metadata.org/SMWG/Observatory/MAVEN |

- **Evidence.** The software parses a format specific to the MAVEN mission as its means of reading that
  mission's data (Field 31 rule 6, applied through Field 32).
  - `pytplot.sts_to_tplot` is exported at the package top level (`pytplot/__init__.py:158`).
  - Its docstrings state "The .sts file format is a text file format used by the MAVEN mission."
    (`importers/sts_to_tplot.py:27`, `:116`).
  - It reads that format's object label and data table into tplot variables.
  - Its documented example loads MAVEN magnetometer Level 2 files (line 122).
- **Level.** The docstring states the target at the mission level, so the observatory row is recorded and
  the instrument row is not (Field 31 rule 7).
- **Row choice.** The row name is copied from the vocabulary byte for byte, with no abbreviation stored on
  the row. The SMWG row is chosen over its CNES/CDPP-AMDA twin, "Mars Atmosphere and Volatile Evolution
  Mission" (`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/MAVEN`), as the authoritative
  registry's row for the same observatory (rule 4).
- **Coupling.** Field 17 carries `Observatory/Mission-specific` for the same reader (rule 6).
- **Not evidence:**
  - The MAVEN SDC origin.
  - The docs' description of the Mars position windows as "specifically ones that are useful for the
    MAVEN spacecraft" (`docs/source/interactivity.rst:6`; that page is no longer in the branch's
    published docs, and the windows are unreachable in this release, Field 4).
  - The MAVEN test fixtures.
- The earlier (2025) extraction recorded MAVEN as a bare name with no SPASE identifier, which is never
  submittable; the row above replaces it.
- **GOES-15** (`…/SMWG/Observatory/GOES/15`), MMS and THEMIS — test fixtures only, not used.

### 33. Logo (OPTIONAL)
https://avatars.githubusercontent.com/u/22352442?v=4

- **Image.** A 265×265 PNG, the "MAVEN Science Data Center" wordmark with Mars and an orbit arc — the
  GitHub avatar of the `MAVENSDC` organization that owns the repository. It is served as `image/png`
  (25,862 bytes) and was viewed.
- **Why it is the logo (rule 2).** The PyHC registry entry for PyTplot (`_data/projects.yml`, matched by
  its `code:` URL) presents this image as PyTplot's logo.
  - The project has no logo of its own on either branch: no image in the README header (only the build
    and DOI badges), and no file named for a logo.
  - `docs/source/conf.py` has no `html_logo`; it sets `html_theme = 'sphinx_rtd_theme'` and no logo
    option.
  - The images under `docs/source/_images/` are example plots (rule 4).
  - The mark belongs to the developing organization, which rule 5 would exclude had the registry not
    presented it.
- **URL form (rule 9).** The asset is not git-hosted, so there is no commit to pin. The value is the
  `avatar_url` the GitHub API reports for the organization.
  - Considered and not used: the registry's own string,
    `https://avatars3.githubusercontent.com/u/22352442?s=460&v=4`. It is the same image, at the same
    size, from a legacy avatar shard host with a sizing parameter (24,913 bytes; byte-identical to the
    same query on the canonical host).
  - It still answers, but the registry's string is never recorded without re-deriving it.
- **Difference from CDFlib.** The CDFlib dossier declined the same avatar because cdflib has moved out of
  the MAVENSDC organization and its registry entry is stale; neither holds for PyTplot, which still lives
  under MAVENSDC.
