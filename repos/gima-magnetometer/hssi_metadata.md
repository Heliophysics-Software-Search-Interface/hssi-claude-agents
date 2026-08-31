# HSSI Metadata Extraction Results

**Software Name:** GIMAmag
**HSSI Software ID:** a81dc380-707e-4d2a-8995-ffe2454026ea
**Repository:** https://github.com/space-physics/gima-magnetometer
**Source Revision:** 040503a3d7055787cf0b363beb94c92b6d6469b6
**Extraction Date:** 2026-08-30
**Validation Date:** 2026-08-31
**Validation Status:** PASS

---

## Scope notes — read these before trusting any repository-derived value

Two properties of this repository change how its evidence must be read.

### 1. The `v1.0` tag sits on an orphan lineage. Never use `git log --all` here.

`git rev-parse v1.0` resolves to `83e11f62249e233bcf77f3d8c521e48022b27d56` (a lightweight tag,
dated 2017-03-13, subject `scale`). That commit shares **no common ancestor** with the pinned
revision: `git merge-base v1.0^{commit} 040503a3d7055787cf0b363beb94c92b6d6469b6` prints nothing and
exits non-zero. The tag's 13-commit lineage duplicates the subjects and dates of `main`'s first 13
commits under different SHAs — the residue of a history rewrite. `main`'s counterpart of `scale` is
`2dfcedf7`.

Consequence: any agent that reads this repository's history with `git log --all` or `git tag` alone
will read a parallel, superseded lineage and reach confidently wrong conclusions about versions and
dates. Use `git rev-list <pin>` / `git log <pin>` so that only the pinned ancestry is considered.
Everything in this dossier that is drawn from history was derived that way.

The tag also never corresponded to a "1.0" of the package: `git show 83e11f62:setup.py` declares
`version = '0.6'`. `v1.0` was a release label that did not match the packaging version at any point
in either lineage. This matters directly for Fields 2 and 12.

### 2. The upstream GitHub repository is archived.

The repository is archived (read-only), so it accepts no issues, pull requests or commits. The last
commit on the pinned ancestry is the pin itself, `040503a3` (2022-08-11, `Update README.md`). The
code itself stopped moving well before that, and two distinct dates mark it. The last commit to
touch a Python file path at all is `9a40e155` (2020-07-02, `src layout`) — but that is a pure
rename, moving `gimamag/__init__.py`, `gimamag/plots.py` and `tests/test_all.py` into the `src/`
layout without changing a line of any of them. The last commit to modify the content of a Python
file is `51bb911c` (2020-02-19, `meta`), which added the fifteen-line Apache 2.0 header block to
`gimamag/__init__.py` in the same commit that replaced the licence text (Field 15). Everything on
the ancestry after that is packaging, CI, documentation and file relocation. The archived state, not
these dates, is the decisive evidence for Field 23; the dates show how long the code had already
been finished when the door was closed. Together they are the reason several "would a maintainer fix
this?" questions below are answered "no, and they cannot".

### The governing principle used throughout

Every judgment call below was decided from the perspective of a person using the HSSI website: *if
someone on the page for this region / observatory / phenomenon / package clicked "show related
software", would they be glad to find GIMAmag, or would they find it out of place?* Arguments that a
site visitor never sees — internal consistency, symmetry between fields, tidiness — are not reasons
and were not used.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The placeholder is the catalogue convention for a record not submitted by its maintainer; it is not
a defect.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.376876

The software does have a DOI, and this dossier records it for the first time — the prior extraction
concluded "No DOI found in repository files", which is true of the repository (no `CITATION.cff`, no
DOI badge in `README.md`, no `codemeta.json`, no `.zenodo.json` at the pin) but not true of the
software. The deposit was found by searching Zenodo for the repository name rather than by reading
the repository.

**Why this is certainly the same software, not a same-named deposit.** The Zenodo record is titled
"GIMA Magnetometer tools", is typed as Software, was issued 2017-03-13, credits "Hirsch, Michael",
and its sole file is `gima-magnetometer-1.0.tar.gz` — a GitHub release archive of this repository's
`v1.0` tag. Unpacking that archive gives the same seven-path tree as `git ls-tree -r v1.0`
(`.gitignore`, `LICENSE`, `LoadGIMA.py`, `README.rst`, `gimamag/__init__.py`, `gimamag/plots.py`,
`setup.py`), and its `setup.py` and `gimamag/__init__.py` are byte-identical to the tagged blobs.
The deposit also sits in Zenodo's `spacephysics` community, the community behind the
`space-physics` GitHub organisation. The archived artefact is genuinely this repository's GitHub
`v1.0` release tarball.

**The deposit was made by hand, not by the GitHub–Zenodo integration.** The distinction matters
because the integration story is the natural assumption and it is wrong here. An integration-produced
deposit records the release it was built from: Zenodo stores a related identifier relating the record
`isSupplementTo` a GitHub `/tree/<tag>` URL. Record 376876 stores no such relation — its only related
identifier is an `IsPartOf` pointing at the `spacephysics` community — and DataCite's `version` field
for the DOI is null. That absence is not an artefact of 2017-era Zenodo practice: the same author's
contemporaneous integration deposits do carry the linkage — `10.5281/zenodo.162066`
("All-sky Camera utilities in Python") relates `isSupplementTo`
`https://github.com/scienceopen/dascutils/tree/v1.0`, and `10.5281/zenodo.167565`
("Meridian Spectrometer Reader") relates to
`https://github.com/scienceopen/meridian-spectrometer-reader/tree/v1.0`. A later refresh should
expect to find the same gap here, and should not restore the integration claim on the strength of
the tarball alone.

The release timeline corroborates a manual upload. GitHub's release record for `v1.0` gives a
publication time of `2017-03-13T06:12:48Z`, and the Zenodo record was created at
`2017-03-13T06:17:15Z` — four minutes and twenty-seven seconds later. That interval fits a person
publishing a release, fetching its archive and depositing it, which is also why the deposited file is
the real release tarball even though no automation produced the record.

That release was published by the GitHub account `meresmclr`, whose profile carries `name`
"Michael Hirsch" and `company` "Boston University" — matching the creator and affiliation on the DOI
record (Field 6). This is a different account from `scivision`, which authored the pinned commit and
supplies `setup.cfg`'s `author_email = scivision@users.noreply.github.com`. The matching profile name
and company are the evidence that both accounts belong to Hirsch; the identification does not rest on
an assumption that two logins touching one repository must be the same person.

**Caveats a future refresh must not lose:**

- **It is a version DOI, not a concept DOI.** Field 2 prefers a concept ("all versions") DOI, but
  none exists here: the record's `conceptdoi` is empty, and the parent record's would-be DOI
  `10.5281/zenodo.789071` is not a registered handle. `10.5281/zenodo.376876` is the only persistent
  identifier this software has, so it is the correct entry despite not being a concept DOI.
- **It archives the 2017 `v1.0` snapshot only**, which is a state of the *orphan* lineage described
  in the scope note. That snapshot's own `setup.py` declares `version = '0.6'`. The DOI therefore
  does **not** identify the current 0.6.2 code and must not be copied into Field 12's Version PID
  (see Field 12).
- **Its own descriptive metadata contradicts itself and the repository.** Zenodo/DataCite record the
  rights as `cc-by-4.0` ("Creative Commons Attribution 4.0 International") while the `LICENSE` file
  *inside the archived tarball* is the 674-line GNU GPL v3. That is a Zenodo-side default, not a
  statement by the author, and it must not be used for Field 15. Its title, "GIMA Magnetometer
  tools", must not be used for Field 7.

The DataCite record confirms `publisher = "Zenodo"` and `publicationYear = 2017` with
`{"date": "2017-03-13", "dateType": "Issued"}`; those feed Fields 11 and 10 respectively (see
there).

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/gima-magnetometer

The repository root URL, matching `setup.cfg`'s `url = https://github.com/space-physics/gima-magnetometer`
and the PyHC registry's `code:` entry. It resolves, and remains the right value even though the
repository is archived: archiving makes a repository read-only, not unavailable, and this is still
where the human-readable source lives. The repository is not a fork and has no parent repository.

### 4. Software Functionality (RECOMMENDED)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots

**What the software actually does**, from the pinned source. `src/gimamag/__init__.py` exposes two
reading functions. `readgimafile` opens one GIMA hourly netCDF file
(`    with nc.Dataset(fn, 'r') as f:`), recovers the file's calendar date from its *filename*
(`# %% date from filename -- only way`, then
`    d0 = datetime.strptime(fn.stem[-13:-3], '%Y_%m_%d')`), decodes the archive's decimal-hour time
convention into datetimes (`            hour = int(h)` /
`            second = (h-hour)*3600`), optionally restricts the record to a caller-supplied time
window, and assembles the three geomagnetic components into a labelled array with
`coords={'dir': ['Bh', 'Bd', 'Bz'],`. `readgima` is the
`    Helper function to concatenate hourly file data`, joining successive hours with
`            Bs = xr.concat([Bs, B], dim='time')`. `src/gimamag/plots.py` contains one function,
`def plotmag(B: xr.DataArray):`, which builds `    fg, axs = subplots(3, 1, sharex=True)` and draws
one component per panel via `        B.sel(dir=d).plot(ax=a)`, labelling
`        a.set_ylabel(f'{d.item()} [nT]')` and `    axs[-1].set_xlabel('time [UTC]')`. `LoadGIMA.py`
wraps both in a command-line entry point described as
`        description='reading UAF Geophysical Institute GIMA magnetometer data')`.

That maps cleanly onto the six values above: format-specific decoding and component assembly are
`Processing`; the time-window selection, hourly concatenation and time-indexed result are
`Time Series Analysis`; the three-panel figure is `Line Plots`. Parents are listed alongside their
subcategories as the taxonomy requires.

**Categories examined and rejected** — recorded so a later refresh does not re-propose them:

- **`Coordinate Transforms` and all six of its subcategories.** Magnetometer software often converts
  between geomagnetic (H, D, Z) and geographic (X, Y, Z) components, and the bundled data file even
  carries the attributes that would enable it — `Source_GMag_model` reads
  `Altitude Adjusted Corrected Geomagnetic Coordinates`, and `Magnetic_decl_Coord_accuracy` reads
  `Zero Decimal places.  Gross magnetic rotation for converting data between geomagnetic (H,D,Z) and geographic (X,Y,Z) components.`
  GIMAmag reads none of those attributes and performs no such conversion; it returns the three
  components exactly as stored. `Ionospheric` in particular would be wrong, and the fixture's own
  wording makes that rejection stronger rather than weaker. The bundled
  `src/gimamag/tests/poker_2017_11_16_10.nc` names its coordinate model only by the expansion quoted
  above, held in the `Source_GMag_model` attribute; the acronym `AACGM` appears in no tracked file at
  the pin, and the expansion appears in no tracked file other than that fixture. The model name is
  inert metadata that the software never reads, and there is no coordinate-transform code anywhere in
  the package for it to drive.
- **`Data Processing and Analysis: Data Access and Retrieval`.** GIMAmag has no retrieval capability
  whatsoever. A sweep of every tracked text file at the pin for `requests`, `urllib`, `urlopen`,
  `wget`, `curl`, `ftp` and `download` finds only the `.gitignore` entry `downloads/`, the two
  documentation links to the GIMA archive, and the repository/licence URLs — no network code. The
  user downloads files by hand; the software reads local paths. (This is also why Field 17's
  `HTTP/HTTPS Directories` must not be read as implying retrieval — see Field 17.)
- **`Data Processing and Analysis: Analysis`.** The author's own `setup.cfg` description says
  `description = Plotting and analysis of UAF GIMA Magnetometer data`, and this catch-all is easy to
  add on that word alone. But the package computes no derived physical quantity and performs no
  statistical operation — it converts a time base, stacks three stored variables, and plots them.
  Someone browsing this category for statistical or derived-quantity tooling would find a file
  reader out of place.
- **`Data Processing and Analysis: Data Reduction`.** The `-t/--tlim` window
  (`    p.add_argument('-t', '--tlim', help='time window to zoom plot in on', nargs=2)`) selects a
  sub-interval; it does not average, bin, downsample or denoise, which is what this category
  describes.
- **`Data Processing and Analysis: Calibration`.** The archive files already carry physical units
  (`hcomp.units` is `nano-tesla`); GIMAmag applies no calibration of its own.
- **`Data Processing and Analysis: File Format Conversion`.** Nothing is written. Reading netCDF into
  an in-memory object is not a format conversion, and Field 19 is correspondingly empty.
- **`Mission-related` and its subcategories.** GIMA is a ground observatory array, not a mission, and
  GIMAmag is not part of anyone's ground system or processing pipeline.
- **`Models and Simulations`, `Servers and Environments` and their subcategories.** Nothing in the
  package models, simulates, serves or containerises anything.

**One value is imprecise but was deliberately left in place: `Data Visualization: 2D Graphics`.**
The only plotting code produces stacked one-dimensional line panels, so `Line Plots` is the exact
value and `2D Graphics` is normally understood as the contour/heatmap/image family — there is no
contour, image, mesh or map rendering anywhere in the pinned tree. It was kept because the claim it
makes is presentational rather than scientific: the figure genuinely is a static two-dimensional
graphic, the category carries no definition in the vocabulary to appeal to, and a visitor browsing
"2D Graphics" who finds a time-series plotting tool is at worst unsurprised. Contrast Field 5's
`Earth Atmosphere`, which was removed: that value made a substantive and false claim about which
physical region the software serves. The difference in treatment is a difference in the strength of
the claim, not a difference in standard.

### 5. Related Region (RECOMMENDED)
**Values:**
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Magnetosphere

The vocabulary is flat: every row is top-level, with no parent/child relationships populated. A
coarse value therefore never implies a fine one and a fine value never implies a coarse one, so each
row has to earn its place on its own. "X encompasses Y" is not an argument here.

**`Earth Auroral Subregion`** — the strongest and most specific value, and it rests on primary
evidence inside the repository rather than on domain assumption. The bundled data file
`src/gimamag/tests/poker_2017_11_16_10.nc` carries `Source_Location` =
`Poker Flat Research Range, AK`, `Source_Latitude` = `65.118669` and, decisively,
`Source_GMagLatitude` = `65.4523` — a corrected-geomagnetic latitude squarely inside the auroral
oval. The array is sited to observe the auroral zone, and someone browsing for auroral-region
software would expect a reader for auroral-zone ground magnetometer data to be there.

**`Earth Ionosphere`** — a ground magnetometer at auroral latitudes records, above all, the ground
magnetic signature of ionospheric current systems. This is what the existing HSSI description
already asserts ("geomagnetic variations related to ionospheric currents"), and it is corroborated
externally by the PyHC registry, which tags GIMAmag
`keywords: ["ionosphere_thermosphere_mesosphere","specific"]`. A visitor browsing ionospheric
software would be glad to find it.

**`Earth Magnetosphere`** — retained. Auroral-zone ground magnetometer records are the standard
ground-based proxy for magnetospheric substorm and storm activity, which is precisely why this array
is embedded in a magnetospheric mission's ground network: SPASE's `SMWG/Observatory/THEMIS/Ground/GIMA`
record states "The Alaska Geophysical Institute Magnetometer Array (GIMA) is part of the THEMIS Ground based observatory network."
A visitor browsing magnetospheric software would expect ground magnetometer readers to appear.

**`Earth Atmosphere` was removed.** It was one of the two values previously held. The removal is not
a re-styling: the value asserts that the software supports science for the neutral-atmosphere region,
and it does not. Every quantity GIMAmag surfaces is a component of the geomagnetic field in
nano-tesla (`hcomp.long_name` = `H-component, geomagnetic field`, and likewise for `dcomp` and
`zcomp`); nothing about neutral composition, density, temperature or winds is read, derived or
plotted. The vocabulary offers a distinct `Earth Lower and Middle Atmosphere` row, so `Earth
Atmosphere` reads as the general neutral-atmosphere facet, and a visitor browsing it for atmospheric
science tooling would find a magnetometer file reader misplaced. Notably, the reason originally given
for choosing `Earth Atmosphere` was ionospheric currents and the auroral electrojet — exactly what
`Earth Ionosphere` and `Earth Auroral Subregion` now express directly. The prior reasoning is
preserved; only the row that carried it changes.

**Regions considered and rejected:**

- **`Earth Thermosphere`** — the auroral electrojet does flow at E-region/lower-thermospheric
  altitude, and PyHC's single lumped `ionosphere_thermosphere_mesosphere` tag touches it. But that
  tag is one coarse registry bucket and cannot select among I, T and M; the current system is
  conventionally labelled ionospheric; and GIMAmag yields nothing about neutral thermospheric state.
  A visitor browsing thermospheric software (densities, winds, composition) would not expect this.
- **`Earth Inner Magnetosphere`** — the ring current is indexed by mid- and low-latitude
  magnetometers. GIMA is a high-latitude auroral array whose signal is electrojet-dominated. A
  visitor browsing inner-magnetosphere software (ring current, radiation belts, plasmasphere) would
  find it out of place.
- **`Earth Magnetotail`** — reaching it requires mapping the substorm current wedge from the ground
  to the tail. That is an inference about the physics the data are used to study, not a region the
  software supports; the general `Earth Magnetosphere` value already carries the substorm
  association honestly.
- **`Earth Lower and Middle Atmosphere`** — same objection as `Earth Atmosphere`, more so.

### 6. Authors (MANDATORY)
**Author 1:**
- **Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:** Boston University — https://ror.org/05qwgg493
- **Affiliation 2:** Scivision, Inc.

Sole author. `setup.cfg` records `author = Michael Hirsch, Ph.D.` with
`author_email = scivision@users.noreply.github.com`; `src/gimamag/__init__.py` opens
`Copyright 2020 Michael Hirsch, Ph.D.`; the PyHC registry gives `contact: Michael Hirsch`; and the
Zenodo/DataCite deposit credits `Hirsch, Michael`. The ORCID resolves to Michael Hirsch.

The **Boston University** affiliation is independently corroborated by the DOI record, whose creator
entry carries `"affiliation": ["Boston University"]` — Hirsch's affiliation at the time of the 2017
deposit. Its ROR resolves. **Scivision, Inc.** is his own company, matching the
`scivision@users.noreply.github.com` author address and the `scivision` GitHub account that authored
the pinned commit. It carries no identifier, and correctly so: a ROR search for "Scivision" returns
a single unrelated organisation (a Taiwanese company at `scivision.com.tw`), so there is no ROR to
attach. A future refresh should not re-run that search hoping for a different answer.

**Parked observation, not a task for this record.** The organisation is stored as `Scivision, Inc.`
while DataCite and Zenodo render Hirsch's company as `SciVision, Inc.` in other deposits. The
capitalisation question is shared across every record that references this organisation and is being
handled separately; it is deliberately not addressed here and must not block anything about GIMAmag.

### 7. Software Name (MANDATORY)
**Value:** GIMAmag

Four names are in play and it is worth recording which is which so the next refresh does not churn
this field: the repository is `gima-magnetometer`, the distribution is
`name = gima_magnetometer` in `setup.cfg`, the import package is `gimamag`, and the Zenodo deposit
is titled "GIMA Magnetometer tools". `GIMAmag` is the name under which the PyHC registry lists the
project (`- name: GIMAmag`), it matches the import package's spelling, and it is the form a person
would recognise. It is kept unchanged.

### 8. Description (MANDATORY)
**Value:**
UAF Geophysical Institute magnetometer network data read and plot. This software package provides tools for reading, processing, and visualizing magnetometer data from the University of Alaska Fairbanks Geophysical Institute Magnetometer Array (GIMA) network. The software reads netCDF4 format data files containing magnetic field measurements, allows time-based filtering and extraction, concatenates multiple hourly data files, and generates time series plots of the three magnetic field components (horizontal, declination, and vertical). The package is designed to support analysis of geomagnetic variations related to ionospheric currents and magnetospheric processes observed by the ground-based GIMA magnetometer network in Alaska.

Kept unchanged. Every factual claim in it was re-checked against the pinned source and the bundled
data file and holds: the first sentence is the repository's own one-line summary; the format is
indeed netCDF4 (the fixture's magic bytes are HDF5 and its `file_format` is `NETCDF4`); the
time-window selection, hourly concatenation and three-panel plot are all as described.

One wording note, recorded so it is not mistaken for an error later: the second component is called
"declination" here, following the standard HDZ naming of geomagnetic components, even though in this
archive `dcomp` is an eastward field component in nano-tesla (`dcomp.notes` = `Positive values are East`)
rather than an angle. That is the conventional usage and was left alone.

### 9. Concise Description (OPTIONAL)
**Value:** UAF Geophysical Institute magnetometer network data read and plot

Kept unchanged. This exact string is the repository's README summary line, the GitHub repository
description, and the PyHC registry's `description:` for the project — three independent sources
agreeing verbatim. Note that `setup.cfg` carries a different one-liner,
`description = Plotting and analysis of UAF GIMA Magnetometer data`; the README/PyHC form was
preferred because it is the one the project actually publishes.

### 10. Publication Date (RECOMMENDED)
**Value:** 2017-01-19

The field asks for the date of first publication of the initial version. The repository became
public with its initial commit `ddfd14fd`, authored `2017-01-18 22:05:48 -0500` — that is
`2017-01-19T03:05:48Z`, and GitHub's own `created_at` for the repository is exactly that instant.
So 2017-01-19 is the UTC date the software first appeared publicly. Kept unchanged.

**The alternative was considered and not selected.** The Zenodo/DataCite record carries
`{"date": "2017-03-13", "dateType": "Issued"}`. That is when the first archival release was issued,
nearly two months after the code was first published, and it belongs to the orphan `v1.0` lineage.
It is recorded under Field 2 as evidence about the DOI rather than substituted here.

### 11. Publisher (RECOMMENDED)
**Value:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Changed from GitHub. The field's rule turns on the DOI alone: "For software where a DOI has been
obtained through Zenodo (e.g., GitHub-Zenodo workflow), Zenodo is the correct entry. If no DOI has
been obtained, indicate the repository host, such as GitHub or GitLab." The GitHub–Zenodo workflow is
a parenthetical example of how such a DOI is commonly obtained, not a condition attached to it; the
condition is simply that a DOI was obtained through Zenodo. Field 2 records one,
`https://doi.org/10.5281/zenodo.376876`, and DataCite's own record for that DOI independently states
`publisher = "Zenodo"`.

The route the deposit took does not bear on this. Field 2 establishes that record 376876 was uploaded
manually rather than produced by the GitHub–Zenodo integration, which gives it a different shape from
the integration-produced deposits a reviewer sees more often — it carries no `isSupplementTo` link
back to a GitHub release. A later refresh that notices that difference should not reopen this field:
the rule asks whether a DOI was obtained through Zenodo, and it was.

GitHub was the right answer while the record held no DOI; it is superseded by the DOI, not corrected
for style. **These two fields move together**: were a future refresh ever to withdraw the DOI in
Field 2, this field would revert with it to Organization `GitHub`, identifier `https://github.com`.

### 12. Version (RECOMMENDED)
- **Version Number:** 0.6.2
- **Version Date:** 2018-07-08
- **Version Description:** modernize, pep8, mypy
- **Version PID:** Not found

Kept unchanged, and confirmed against the declared-version history along the pinned ancestry only
(`git rev-list <pin> -- setup.py setup.cfg`), which is strictly monotonic and ends where the record
already sits:

| declared version | first commit declaring it | date |
|---|---|---|
| `0.5` | `ac6d923e` | 2017-02-08 |
| `0.6` | `74d4eaf8` | 2017-02-14 |
| `0.6.1` | `e5231061` | 2018-05-08 |
| `0.6.2` | `87953c14` (`modernize, pep8, mypy`) | 2018-07-08 |

`setup.cfg` at the pin declares `version = 0.6.2`, unchanged through the five subsequent commits
that touched it. The version date and description are the date and subject of the commit that
introduced 0.6.2.

**Do not "upgrade" this to 1.0.** The only tag in the repository is `v1.0`, and a naive
latest-tag-wins reading would replace a correct value with a wrong one twice over: the tag is on the
orphan lineage (scope note 1), and the code it labels declares `version = '0.6'`, so 1.0 was never
the packaging version on either lineage.

**Version PID is deliberately empty although the software has a DOI.**
`https://doi.org/10.5281/zenodo.376876` archives the `v1.0` snapshot, whose `setup.py` declares
`0.6`. It is not a persistent identifier for version 0.6.2 and putting it here would assert a false
correspondence. There is no DOI for 0.6.2, and the repository being archived means none will be
minted.

### 13. Programming Language (RECOMMENDED)
**Value:** Python 3.x

`setup.cfg` sets `python_requires = >= 3.6` and classifies the project for Python 3 only; the CI
workflow installs `        python-version: '3.x'`. Pure Python — the pinned tree contains no
compiled sources. Kept unchanged.

### 14. Reference Publication (RECOMMENDED)
**Value:** Not found

There is no paper describing this software. The repository contains no `CITATION.cff`, no citation
section in `README.md`, and no reference to a publication anywhere at the pin. A full-text
literature search corroborates this rather than merely failing to find it: searching for the exact
string `GIMAmag` returns nothing, and searching for the exact repository path
`space-physics/gima-magnetometer` also returns nothing — while the same index does return papers
containing `github.com/space-physics`, proving that it indexes URLs from this GitHub organisation in
full text and that the absence is real. A search for a package name that does exist returns hundreds
of hits, and a nonsense control returns none, so the query form is sound.

One trap for a future refresh: searching for the *hyphenated* repository name as a phrase returns
about seventeen unrelated papers. Those are a tokenisation artefact — the index splits on the hyphen
and matches "GIMA" and "magnetometer" independently, so the hits are papers about the observatory
array, not about this software. None of them describes, cites or uses GIMAmag.

### 15. License (RECOMMENDED)
**Value:**
- **License:** Apache License 2.0
- **License URI:** https://spdx.org/licenses/Apache-2.0

Newly recorded; the record previously held no license at all. **The licence history here is a
three-way story and the repository still contains a contradiction at the pin**, so the reasoning is
set out in full to stop a later refresh from reopening it.

1. `LICENSE` was added at the initial commit `ddfd14fd` (2017-01-18) as the 674-line **GNU GPL v3**.
2. `0f416698` (2019-10-08, `ci=>actions`) renamed it to `LICENSE.txt` with the content unchanged
   (git detects the rename at 100% similarity), and introduced `license_files =` / `  LICENSE.txt`
   in `setup.cfg`.
3. `51bb911c` (2020-02-19, `meta`) **replaced that text with the full 176-line Apache License 2.0**,
   and in the same commit added the Apache 2.0 header block to `gimamag/__init__.py` — which at the
   pin still opens `Copyright 2020 Michael Hirsch, Ph.D.` followed by
   `Licensed under the Apache License, Version 2.0 (the "License");`.

**MIT was considered and rejected.** `setup.cfg` at the pin still carries the classifier
`  License :: OSI Approved :: MIT License`, and that line has sat there unchanged since the very
first packaging commit `ac6d923e` (2017-02-08). It is a stale classifier, not a licence grant, and
the evidence that it is stale is unusually direct: commit `51bb911c` — the commit that swapped the
licence text to Apache 2.0 — edited that very classifiers block (adding the Python 3.8 and 3.9
lines) and left the MIT line untouched. A classifier that survived the licence change untouched is
an oversight, not a decision. It also contradicted the GPL v3 file for the three years before that.
The authoritative artefacts are the licence file itself, which `setup.cfg` points at through
`license_files`, and the source header — and both say Apache 2.0. GitHub's own licence detection for
the repository independently reports `Apache-2.0`.

**CC-BY-4.0 was also considered and rejected.** The Zenodo/DataCite deposit records the rights as
`cc-by-4.0`. That is a Zenodo-side value attached to a 2017 snapshot whose bundled `LICENSE` file is
GPL v3 — it disagrees with the very archive it describes, so it carries no weight. This is the
specific reason not to let DOI-driven autofill populate this field.

**GNU General Public License v3.0 or later was considered and rejected**: it is the *historical*
licence (2017-01 to 2020-02) and would be correct only for a record pinned before `51bb911c`. The
pin is well after it.

The URI recorded is the one the `Apache License 2.0` vocabulary row itself carries; it is a property
of that row rather than a per-record value. The licence text's own canonical address, as printed in
the source header, is `http://www.apache.org/licenses/LICENSE-2.0`.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- geomagnetic
- geophysics
- geoscience
- magnetometer
- ground magnetometer
- auroral electrojet

The first four are unchanged and fully evidenced: `setup.cfg` declares `keywords =` /
`  magnetometer` / `  geomagnetic`, and the GitHub repository carries the topics `geophysics`,
`geoscience` and `magnetometer`. (These are stored in lower case; the site renders them
capitalised.)

**`ground magnetometer` is added.** It is the precise instrument class — the bundled file's
`Instrument` attribute is `NAROD Fluxgate Magnetometer`, sited at
`Poker Flat Research Range, AK` — and it distinguishes this software from spacecraft magnetometer
tooling, which the bare `magnetometer` keyword does not. It reuses an existing keyword rather than
minting a near-duplicate, and a visitor searching for ground magnetometer software would want this
package back.

**`auroral electrojet` is added.** This is an inference from what the data are, not a phrase that
appears in the repository, and it is flagged as such: the array's corrected-geomagnetic latitude of
`65.4523` puts it under the auroral oval, where the electrojet dominates the horizontal-component
record that this software reads and plots. It also gives Field 22's coarser `Geomagnetic Storms`
value the specificity the closed phenomena vocabulary cannot express (see Field 22). It likewise
reuses an existing keyword row.

**Considered and not added:** a geographic keyword such as `alaska`. The vocabulary carries no such
row, so adding one would mint a permanent new row for little discovery value; the place is already
carried by the description, the observatory association and the software name.

**`poker-flat-research-range` was also considered and rejected**, even though the vocabulary does
carry that row, so nothing new would have had to be minted. Poker Flat is the software's
demonstration station, not a station it is bound to: it is simply where the bundled fixture and all
four `LoadGIMA.py` example invocations happen to come from, and the reader takes any station's files
without branching on station (see Field 31). Tagging the one demonstration station would tell a
visitor that this is a Poker-Flat-specific tool, which is false of an array-wide reader. That is the
mirror image of the asymmetry Field 31 rejects, where recording the seven "University of Alaska
Network" station rows would have connected the software to seven stations while omitting the very
one it demonstrates. Both distortions come from the same mistake — letting the vocabulary's
incidental coverage decide what the software is about — and both are rejected on that ground. The
array-level association a visitor actually needs is already carried by Field 32's observatory entry,
and the place by the description and the software name.

### 17. Data Sources (OPTIONAL)
**Values:**
- HTTP/HTTPS Directories
- Observatory/Mission-specific

Kept unchanged. `Observatory/Mission-specific` is the primary value and is exactly what the field
intends: the data are the GIMA array's own hourly files, and the field's guidance is to pair that
selection with naming the observatory in Field 32, which this record does. `HTTP/HTTPS Directories`
describes how those files are distributed — `README.md` points users at
`GIMA data [download](https://www.gi.alaska.edu/monitors/magnetometer/archive)`, a plain web archive
directory rather than a standard service such as CDAWeb, HAPI or Madrigal.

**One nuance that must travel with this field:** the value records where the supported data come
from, **not** a retrieval capability. GIMAmag downloads nothing (see Field 4's rejection of
`Data Access and Retrieval`); the user fetches files from that archive by hand and passes local
paths. A future agent should not read `HTTP/HTTPS Directories` here as evidence for a data-access
functionality.

Also worth knowing: `LoadGIMA.py`'s docstring still points at the older archive address
`http://www.gi.alaska.edu/magnetometer/archive`, which is now dead; the README's
`/monitors/magnetometer/archive` form is the live one. The repository is archived, so that stale
in-source link will not be fixed upstream.

### 18. Input File Formats (RECOMMENDED)
**Value:** netCDF3/4

Kept unchanged, and verified directly rather than inferred: the module does
`import netCDF4 as nc` and reads through `    with nc.Dataset(fn, 'r') as f:`, and the bundled
fixture `src/gimamag/tests/poker_2017_11_16_10.nc` begins with the HDF5 magic bytes and reports
`file_format` `NETCDF4`. This is the only format the software can read, which is also why it cannot
consume the THEMIS ground-magnetometer CDF products discussed under Field 28.

### 19. Output File Formats (RECOMMENDED)
**Value:** Not found

Correctly empty rather than unexamined. The package writes no files: a sweep of every tracked text
file at the pin for `savefig`, `to_netcdf` and `write` finds no writer of any kind. `LoadGIMA.py`
ends by calling `show()` to display an interactive figure, and `plotmag` returns nothing. There is
no output format to declare.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

Kept unchanged. The CI workflow at the pin runs the lint-and-test job with `    runs-on: ubuntu-latest`
and an integration job over `        os: [windows-latest, macos-latest]`, each installing the package
and running `    - run: pytest`. All three platforms are therefore demonstrated, not assumed.

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

Kept unchanged. Pure Python with no compiled extensions of its own and no architecture-specific code
or configuration at the pin.

### 22. Related Phenomena (OPTIONAL)
**Value:** Geomagnetic Storms

Newly recorded; the record previously held nothing here. This is a closed vocabulary offering only
Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind
and X-ray emission — six of which are solar or heliospheric and plainly inapplicable to a ground
magnetometer reader.

`Geomagnetic Storms` applies because the ground geomagnetic-field variation that this software reads
and plots *is* the measurement by which geomagnetic storms and substorms are observed: the record it
surfaces is the H, D and Z components in nano-tesla at an auroral-zone station. A visitor browsing
geomagnetic-storm software and finding a reader for auroral-zone ground magnetometer data would be
served, not surprised.

**This is a domain judgement, not a repository quotation** — the word "storm" appears nowhere in the
pinned tree, and that was verified by sweeping every tracked text file for `storm`, `substorm`,
`aurora` and `electrojet`, which returns nothing. It is recorded here so the basis is transparent.

**The more precise phenomena have no rows.** Substorms and the auroral electrojet — which are what an
auroral-zone magnetometer chain actually records most of the time — are absent from this closed
vocabulary and cannot be entered here; the vocabulary rejects anything without a row. Per the field's
own guidance they belong in Keywords instead, which is why `auroral electrojet` was added under
Field 16. A future refresh should re-check whether rows for them have appeared before concluding
that `Geomagnetic Storms` is still the closest available term.

### 23. Development Status (RECOMMENDED)
**Value:** Unsupported

Newly recorded; the record previously held nothing here. The decisive fact is that **the upstream
GitHub repository is archived** — the author has put it in a read-only state that accepts no issues,
pull requests or commits. The software itself reached a stable, working state: it has a tagged
release and a DOI deposit, a passing three-platform CI workflow, and a real test with a bundled data
fixture.

Measured against the repostatus.org definitions the vocabulary uses:

- **`Unsupported`** — "The project has reached a stable, usable state but the author(s) have ceased
  all work on it. A new maintainer may be desired." The first sentence matches exactly. The second,
  wanting a new maintainer, is not something the author states anywhere — but no term in the
  vocabulary expresses "finished and closed" more accurately, and stable-state-plus-ceased-work is
  the substance a site visitor needs.
- **`Inactive`** — "The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows." Rejected on that final clause.
  Archiving makes support structurally impossible, not merely slow: a user cannot open an issue.
  Telling a visitor that support is provided as time allows would set an expectation the repository
  cannot meet. This is a change from the previous extraction's proposal of `Inactive`, which was made
  from the commit dates alone without weighing the archived state.
- **`Abandoned`** — "Initial development has started, but there has not yet been a stable, usable
  release; the project has been abandoned and the author(s) do not intend on continuing development."
  Fails on its opening condition, which is binding: there was a stable, usable release — a tagged
  release and an archived deposit — and the package works. The clause about ceasing development with
  no intent to continue does fit this project, which is precisely why the release condition has to be
  read as the discriminator.
- **`Moved`** was rejected: nothing indicates a successor project, and the repository is not a fork
  and has no parent.
- **`Suspended`** — "Initial development has started, but there has not yet been a stable, usable
  release; work has been stopped for the time being but the author(s) intend on resuming work."
  Rejected twice over: there was a stable release, and archiving is the opposite of intending to
  resume.

The packaging classifier `  Development Status :: 4 - Beta` in `setup.cfg` was noted and not used.
It describes maturity, not activity; it was `3 - Alpha` from 2017-02-08 until `9a40e155`
(2020-07-02) raised it to `4 - Beta`, and it has been frozen ever since — including through the
project's closure. It cannot distinguish among the terms above.

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/gima-magnetometer#readme

Kept unchanged and it resolves. This is genuinely the whole of the documentation: there is no
`docs/` directory, no Read the Docs configuration and no project site at the pin. `README.md`
carries the install step (`    pip install -e .`) and the invocation
(`python LoadGIMA.py myfile.nc`), and the four worked examples live in `LoadGIMA.py`'s own
docstring.

### 25. Funder (OPTIONAL)
**Value:** Not found

No funder is acknowledged anywhere at the pin — there is no acknowledgements section, no funding
statement, and no paper to carry one (Field 14). The one funding-adjacent artefact in the project's
history is not a research funder: `.github/FUNDING.yml` existed from `0f416698` (2019-10-08) until
`c3b8cf41` (2021-03-22, `cleanup`) removed it, and it listed only the personal donation platforms
`github: [scivision]` and `ko_fi: scivision`. It is absent at the pin, and it would not belong in
this field in any case. Recorded so a future agent does not resurrect it as a funder.

### 26. Award Title (OPTIONAL)
**Value:** Not found

No award or grant number appears anywhere at the pin, and with no funder (Field 25) and no
publication (Field 14) there is no acknowledgements section or data-availability statement that
could supply one.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** Not found

No publication cites or uses this software. The negative research supporting this is set out under
Field 14 — including the positive and negative controls that show the searches were sound and the
tokenisation trap that makes a hyphenated-name search look like seventeen false hits. Independently,
the citation graph holds no record at all for `10.5281/zenodo.376876`, so the DOI has no tracked
citations either.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

The data GIMAmag reads are the GIMA array's hourly netCDF files, distributed from the University of
Alaska's web archive at `https://www.gi.alaska.edu/monitors/magnetometer/archive`. That is a plain
directory listing: there is no dataset DOI and no persistent dataset landing page for it, so there
is no URL that could be entered here. (The observatory itself does have a persistent record — that
is Field 32's SPASE identifier, which is an observatory, not a dataset.)

**The obvious near-miss was rejected.** The THEMIS ground-based observatory programme publishes
ground-magnetometer datasets that include GIMA stations, and those do have persistent records. They
are a *different product*: THEMIS-processed CDF, which GIMAmag cannot read — it reads netCDF only,
through `nc.Dataset` (Field 18). Listing them would tell a visitor this software works with data it
cannot open.

### 29. Related Software (OPTIONAL)
**Value:** Not found

**This field was emptied.** It previously listed four packages — matplotlib, seaborn, xarray and
netcdf4-python — which together are simply the project's dependency list read off `setup.cfg`. None
of them is distinguishing: an entry that would read identically for a large fraction of the Python
ecosystem tells a visitor nothing about *this* software, and that is the test this field applies. An
evidenced removal is as legitimate an outcome as an addition.

Taking them individually, and applying the same bar to each:

- **matplotlib** and **seaborn** are excluded outright as generic plotting infrastructure — they
  would be equally at home in a web application or a finance model. Both are additionally only
  optional extras here, not requirements: `setup.cfg` puts them under `plot =` in
  `[options.extras_require]`, and `LoadGIMA.py` imports seaborn inside a `try` block purely to set
  figure styling.
- **netcdf4-python** is a conditional case that fails its condition. It qualifies only on a specific
  documented exchange, and there is none: it appears solely inside `readgimafile`'s body as the file
  reader (`    with nc.Dataset(fn, 'r') as f:`) and in no public signature. What it contributes to
  the record — that the software reads netCDF — is already stated precisely by Field 18, where a
  visitor filtering by input format will actually find it.
- **xarray** is a conditional case that *passes*, but belongs in Field 30 rather than here, because
  the relationship is a demonstrated data exchange rather than similarity or a domain-specific
  dependency. See Field 30.
- **numpy** and **python-dateutil**, the remaining two entries in `install_requires`, are generic
  infrastructure and were never listed.

Nothing else qualifies. The repository is not a fork and has no parent repository, so there is no
predecessor to record; it names no companion package and no comparable tool. A similar-purpose
magnetometer package could legitimately live here, but the repository offers no evidence connecting
GIMAmag to one, and inventing a comparison would be worse than leaving the field empty.

### 30. Interoperable Software (OPTIONAL)
**Value:** https://github.com/pydata/xarray

Newly recorded; the field was previously empty. xarray is a conditional inclusion that has to be
earned by a specific documented exchange, and here it is earned by the package's public interface
rather than by its dependency list:

- `readgimafile` is declared
  `def readgimafile(fn: Path,` / `                 tlim: List[Union[str, datetime]] = None) -> xr.DataArray:`
  — an annotated xarray return type on a public function;
- `readgima`, the top-level entry point, returns the result of
  `            Bs = xr.concat([Bs, B], dim='time')`;
- the plotting entry point declares `def plotmag(B: xr.DataArray):`, so an xarray object is also the
  package's public *input* type.

The package writes no files (Field 19), so an `xarray.DataArray` is the *only* way data leaves
GIMAmag. That makes the interchange type a real and useful fact about the software: a visitor
evaluating it learns that its output drops straight into any xarray-based pipeline without
conversion. This is a claim that is specific and checkable, not one that would read the same for an
arbitrary package.

**How this differs from netcdf4-python**, which was rejected — the distinction is the reason the
rejection bar and the acceptance bar are the same one. xarray appears in the public signatures on
both the input and the output side; netCDF4 appears only inside a function body. That is an
asymmetry in the evidence, not in the standard applied.

**Rejected in this field:** matplotlib, seaborn, numpy and python-dateutil, for the reasons given
under Field 29. "Part of the scientific Python ecosystem" and "a PyHC-listed package, so it
interoperates with PyHC packages" were both available as arguments and are both insufficient on
their own; neither was used.

### 31. Related Instruments (OPTIONAL)
**Value:** Not found — documented omission

**This is a deliberate omission after resolving the candidates, not an unexamined gap.** The
array-level association that this software actually supports is carried by Field 32; no
instrument-level row can carry it correctly.

The software is designed to support the GIMA array's *file format*, not any particular station's
magnetometer. `readgimafile` is entirely station-agnostic: it derives the date from the filename
(`    d0 = datetime.strptime(fn.stem[-13:-3], '%Y_%m_%d')`) and then reads a fixed set of variable
names — `hcomp`, `dcomp` and `zcomp` — which the bundled Poker Flat fixture carries. Nothing in the
code branches on station. Because that fixture is the only station file in the repository, the
uniformity of those variable names across the rest of the archive is an inference from the format
the array publishes rather than something the pinned tree demonstrates; the station-agnostic
conclusion does not rest on it, since the reader requests those names unconditionally.

Poker Flat is the only GIMA station named anywhere in the repository — a sweep of every tracked text
file at the pin for station names finds it in six `poker_*.nc` filenames across the four example
invocations in `LoadGIMA.py`'s docstring and in the bundled fixture's filename, and it appears again
inside that fixture's own `Source_Location` attribute. No other station is mentioned, and THEMIS is
mentioned nowhere at all.

Three families of candidate instrument rows were examined and each was rejected for a reason a
future refresh should not have to rediscover:

- **The two THEMIS ground-based-observatory GIMA magnetometers**,
  `https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/GIMA/ARCT/MAG` and
  `.../GIMA/BETT/MAG` (both named "THEMIS GBO University of Alaska Geophysical Institute Magnetometer Array",
  abbreviated `GIMA`). Rejected on two counts. They are station-specific to Arctic Village and
  Bettles — "The magnetometer is at the THEMIS/ARCT station." — and the repository names neither, so
  nothing selects them; and they describe instruments as deployed within THEMIS's ground network,
  whose data products are not what GIMAmag reads. Recording them would tell a visitor this software
  supports two specific stations, which is false of an array-wide reader.
- **`https://spase-metadata.org/SMWG/Instrument/Ground/Poker.Flat/Magnetometer`**
  ("Poker.Flat Magnetometer"). This is the tempting one, since Poker Flat is the station the software
  demonstrates and its data are bundled in the repository. Rejected because the association would be
  an inference and would mislead. The row is defined as
  "Magnetometer located at the station with the IAGA identifier POK", which does not attribute it to
  the University of Alaska array — and pointedly, Poker Flat is *absent* from the set of rows that
  SPASE does attribute to that array (the "University of Alaska Network" instrument rows cover
  Bettles, Eagle, Gakona, Homer, Kaktovik, Kenai and Trapper Creek). The bundled file's own
  `Instrument` is a `NAROD Fluxgate Magnetometer` operated as part of
  `GIMA - Geophysical Institute Magnetometer Array`, so binding GIMAmag to a row SPASE has not
  connected to GIMA would assert a link the evidence does not support. Separately, Poker Flat's role
  in this repository is as the test and example station, which is the kind of demonstration mention
  the relevance gate excludes.
- **The seven "University of Alaska Network" per-station magnetometer rows** (`SMWG/Instrument/Ground/{Bettles,Eagle,Gakona,Homer,Kaktovik,Kenai,Trapper.Creek}/Magnetometer`).
  These genuinely are the array's station magnetometers, and the software can read all of their
  files. Rejected because listing them would give a visitor a lopsided and misleading picture: it
  would connect GIMAmag to seven stations while omitting Poker Flat — the one station the software
  actually demonstrates — purely because SPASE has no University-of-Alaska-network row for it. That
  asymmetry is an artefact of the vocabulary's coverage, not a property of the software. The
  observatory-level row covers all of them at once and does so accurately.

The array's own instrument model, the `NAROD Fluxgate Magnetometer` named in the data file, has no
row in the vocabulary at all and is in any case a hardware model name rather than a deployed
instrument.

The correct outcome is therefore the observatory association alone. A visitor searching for software
that supports the GIMA array finds this record through Field 32; no visitor is misled into thinking
it is a station-specific tool.

### 32. Related Observatories (OPTIONAL)
**Value:**
- **Observatory Name:** GIMA
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Ground/GIMA

The value is unchanged; what is new here is that the dossier now records the SPASE identifier
alongside it, which is what makes the entry reliably resolvable rather than a bare name.

This row is the right one and the match is exact. Its definition describes the Geophysical Institute
of the University of Alaska operating "magnetometer sites at locations across Alaska and Western Canada."
— which is precisely the array whose hourly files GIMAmag parses. The bundled data file confirms the
identification from the other direction: its `Experiment` attribute reads
`GIMA - Geophysical Institute Magnetometer Array`, its `Source` reads
`Geophysical Institute Magnetometer Array`, its `Title` reads
`Geophysical Institute, UAF, Magnetometer`, and its `Investigator` is
`Dr. Donald Hampton, Geophyiscal Institute, University of Alaska Fairbanks` (the misspelling is in
the file).

The software also implements a convention specific to this archive, which is what makes it
designed-to-support rather than merely compatible: the files' `time` variable is documented in its
own `units` attribute as `Decimal days, i.e. 2000 Dec. 31 12:24:00=366.51667` while the file's global
attributes say `Start and End times are in decimal hours` and `Time_units` is `Decimal Hours UTC`.
GIMAmag resolves that contradiction the way the archive actually writes the data — as decimal hours
offset from a date recovered from the filename. Software that did not know this archive would decode
the time base wrongly.

**The alternative observatory row was considered and rejected.**
`https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/GIMA`, named
"NASA THEMIS Ground Stations in Alaska", describes the same physical array under a second SPASE
hierarchy: "The Alaska Geophysical Institute Magnetometer Array (GIMA) is part of the THEMIS Ground based observatory network."
Because both rows denote one entity, exactly one should be selected. The `Ground/GIMA` row was chosen
because it is the array in its own right, which is what GIMAmag supports — the software reads the
University of Alaska archive's netCDF files and never touches THEMIS products, and the repository
does not mention THEMIS anywhere. A visitor arriving from a THEMIS-framed page would find a tool that
cannot read the data they have; a visitor arriving from the GIMA array page finds exactly the reader
they want.

### 33. Logo (OPTIONAL)
**Value:** Not found

Correctly empty, on evidence rather than for want of looking. The pinned tree contains sixteen
tracked files and none is an image; sweeping the whole pinned history for `.png`, `.jpg`, `.jpeg`,
`.gif`, `.svg`, `.ico` and `.webp` paths returns nothing, so no image has ever been committed to
this repository. The PyHC registry entry for GIMAmag carries no `logo:` key either — notable because
the neighbouring entry in that same file does, so the absence is a real gap rather than a registry
that omits logos generally. The project has no site or documentation build that might host one.

There is nothing to link to, and no branch-ref or `blob/` URL should be invented to fill the field.

---

## Cross-cutting notes for a future refresh

**The record is not, and will not become, PyPI-distributed.** `README.md` instructs
`    pip install -e .` from a checkout, and the distribution name `gima_magnetometer`, the
hyphenated form and the import name `gimamag` all return "not found" from PyPI's JSON API. (Only the
JSON or Simple API settles this; the HTML project page returns 200 even for packages that do not
exist.) There is therefore no PyPI release history to date versions from, which is why Field 12
rests on the declared version in `setup.cfg`.

**PyHC listing.** GIMAmag appears in the PyHC registry's *unevaluated* list — `_data/projects_unevaluated.yml`
in `heliophysicsPy/heliophysicsPy.github.io` — and in neither the core nor the community list. Its
entry is:

```yaml
- name: GIMAmag
  code: https://github.com/space-physics/gima-magnetometer
  description: UAF Geophysical Institute magnetometer network data read and plot
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","specific"]
```

That is the source for the software name (Field 7), corroborates the concise description (Field 9)
and the author contact (Field 6), and supplies the ITM domain tag weighed under Field 5. A future
refresh should re-check which of the three registry files the entry sits in, since packages move
between them.

**Nothing upstream will change.** With the repository archived, the stale MIT classifier (Field 15),
the dead archive link in `LoadGIMA.py`'s docstring (Field 17), and the absent PyPI release are all
permanent. None of them should be re-investigated as open questions; they are settled facts about a
closed project.
