# HSSI Metadata Extraction Results

**HSSI Software ID:** b914ff2b-105b-49de-8cca-fd079ec6188a
**Repository:** https://github.com/space-physics/AEindex
**Source Revision:** bcb6ac4aa2c1691d12dbf23ac4f9c9f7eb002c8c
**Extraction Date:** 2026-08-29
**Validation Date:** 2026-08-31
**Validation Status:** PASS

---

## Scope note — read this before weighing any evidence below

`AEindex` is a very small, archived package: one Python module (`aeindex/__init__.py`, two functions),
one command-line script (`plotAE.py`), and packaging files. It has no reference publication, no test
suite, no documentation site, and no data-retrieval code. Several fields below are therefore
"Not found" as a *researched conclusion*, not as an unexamined gap, and the reasoning for each
emptiness is recorded so a future refresh does not have to re-derive it.

**The repository is not a complete record of this software's published artifacts.** A registered
Zenodo DOI pair exists for it (Field 2), deposited in 2017 and never advertised anywhere in the
repository: no revision of `README.md` or `README.rst` anywhere in the history carries a DOI badge or
names Zenodo, and there is no `CITATION.cff`, `.zenodo.json` or `codemeta.json` at any point. So a
question of the form "does this software have an X?" must be put to the archive as well as to the
repository, and put using the software's *descriptive* name rather than its repository name. An
earlier revision of this dossier concluded from repository-keyed evidence alone that no DOI existed;
Field 2 records that error, its cause, and the search that does find the deposit.

Two properties of this repository's packaging metadata distort naive extraction and must be kept in
mind for Fields 5, 12, 16, 20, 21 and 23:

1. **`setup.cfg` is a copy-paste of another package's `setup.cfg`.** It entered the repository at
   commit `8b04386` (2018-09-23, message "template") still reading `name = lowtran`
   (`git show 8b04386:setup.cfg`). The name was corrected to `aeindex` eight months later at
   `88629b6` (2019-05-28); several other inherited values were never corrected.
2. **Consequently, some `setup.cfg` values describe `lowtran`, not this software.** Each field below
   that could be read off `setup.cfg` states whether the value is inherited boilerplate or
   independently confirmed.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The bracketed placeholder is the standing convention for this field in these dossiers; the real
submitter identity is supplied at submission time and is not repository-derived metadata.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.789099

**Corrected 2026-08-31. This field previously read "Not found."** That was wrong: a registered Zenodo
DOI pair for this software has existed since 2017. HSSI held no persistent identifier for this
software before this refresh. The superseded reasoning and the reason it failed are both recorded
below, because the failure mode is general and will recur if it is not named.

**Why the concept DOI.** `10.5281/zenodo.789099` is the Zenodo *concept* DOI — the software-level
identifier. Zenodo's own record says so outright, reporting `conceptdoi: 10.5281/zenodo.789099` and
`conceptrecid: 789099`, and DataCite corroborates through the reciprocal pair: `789099` carries
`HasVersion` to `10.5281/zenodo.376875`, and `376875` carries `IsVersionOf` back to `789099`. Field 2
takes the software-level identifier and the version-specific DOI belongs to Field 12 — the settled
convention across this cohort, applied the same way for DASCutils, the Digital Meridian Spectrometer,
AstrometryAzEl and ApexPy — so `376875` is recorded there, not here. There is one version record under
the concept, so the concept DOI presently resolves to `376875`; that is the concept relation working
as intended, not a sign that the two DOIs are interchangeable.

**What the deposit is.** Title "Auroral Electrojet Tools"; publisher Zenodo; Issued 2017-03-13;
`resourceTypeGeneral: Software`; creator "Hirsch, Michael" with affiliation "Boston University";
keyword `auroral electrojet`; member of the Zenodo `spacephysics` community; description "This program
loads and plots Auroral Electrojet data of specified parameters from the original ASCII data tables."
Both DOI records carry the same values for all of these. The creator affiliation independently
corroborates the Boston University affiliation already recorded in Field 6; it does not change it.

**That this deposit is this software.** The identity does not rest on the title resembling the
software's subject. The deposit's single artifact, `AE-index-plot-1.0.tar.gz`, unpacks to six files —
`.gitignore`, `LICENSE`, `README.rst`, `aeindex/__init__.py`, `plotAE.py`, `setup.py` — each
byte-identical to the corresponding blob at this repository's `v1.0` tag, commit `67ddc628` of
2017-03-13, and the two file sets are the same set in both directions: the tag tree holds nothing the
tarball lacks and the tarball holds nothing the tag tree lacks. Timing corroborates the artifact
match: the GitHub release `v1.0` was published 2017-03-13T06:11:06Z and the Zenodo record was created
2017-03-13T06:15:58Z, about five minutes later.

**The deposit is a manual upload, not a GitHub–Zenodo integration deposit — and that does not weaken
it.** Neither DOI record carries `IsSupplementTo`, a GitHub `/tree/<tag>` relation, or any GitHub
reference at all; Zenodo reports no related identifiers for the record; and the description is
hand-written prose rather than release notes. The archive's own shape says the same. Its root
directory is named `AE-index-plot-1.0`, after the repository's then-name `scivision/AE-index-plot`
(Field 3), whereas the tagged `setup.py` declares `name='AEindex_plot'` and no version at all; and the
tarball contains neither `PKG-INFO` nor an `*.egg-info` directory, which a setuptools sdist would. It
is a hand-rolled archive of the tagged working tree.

An era-matched control shows this is a real distinction and not a limitation of what Zenodo recorded
in 2017. The same author's integration deposits from the same period do carry the signature:
`10.5281/zenodo.162066` (DASCutils, Issued 2016-10-19) has `IsSupplementTo` pointing at
`https://github.com/scienceopen/dascutils/tree/v1.0`, and `10.5281/zenodo.167565` (Meridian
Spectrometer Reader, Issued 2016-11-20) has `IsSupplementTo` pointing at
`https://github.com/scienceopen/meridian-spectrometer-reader/tree/v1.0`. This deposit has none of it.
What follows is only that the DOI was minted by hand: the artifact identity above ties the deposit to
this software independently of any declared repository link, so the DOI is no less this software's for
having been uploaded manually.

**Why the previous "Not found" was reached, and the lesson that stops it recurring.** The four checks
recorded in the superseded version of this field were accurately executed, and their results still
hold on re-run — `https://zenodo.org/api/records?q=AEindex` still returns the same two unrelated
records (`10.5281/zenodo.4718561`, a soft-proton-intensity prediction dataset; `10.5281/zenodo.17494514`,
a brain-activity/geomagnetic sleep study); the exact-string search for `"space-physics/AEindex"` still
returns zero; `https://api.datacite.org/dois?query=%22AEindex%22` still returns a total of 0. None of
them could ever have found this deposit, because **every one of them keyed on the string `AEindex` or
on the repository path, and the deposit's metadata contains neither.** Inspecting the full Zenodo
record confirms it: the tokens `AEindex`, `aeindex`, `space-physics`, `github` and `scivision` appear
nowhere in it. The one repository-derived string anywhere in the deposit is `AE-index`, inside the
artifact filename, and Zenodo does not index filename text — a quoted search for `"AE-index-plot"`
returns zero records.

So those four checks were not four independent confirmations. They shared a single point of failure,
and **a set of checks that share one failure mode is one check.** The README-badge check is that same
failure in another guise: it asked the repository whether it advertised a DOI. The repository does not,
at any revision — but that is a fact about this author's badging practice for this repository, not
about whether a deposit exists.

**The search that does find it**, recorded so the next refresh uses it: query Zenodo or DataCite on the
software's *descriptive* name, independently of any repository naming. A Zenodo search for
`"Auroral Electrojet"` — the software name this record already stores in Field 7 — returns this deposit
among its hits, and a DataCite query for `titles.title:"Auroral Electrojet Tools"` returns exactly the
two DOIs recorded here. This record's own Field 7 value would have found what its Field 2 checks could
not.

**Durable evidence that survives the correction.** The following was gathered for the superseded
conclusion, remains true, and is kept because it still answers real questions:

- **Repository history.** Exactly 19 distinct file paths appear anywhere on the pinned history:
  `.coveragerc`, `.flake8`, `.gitattributes`, `.github/CODE_OF_CONDUCT.md`, `.github/FUNDING.yml`,
  `.gitignore`, `.travis.yml`, `CODE_OF_CONDUCT.md`, `LICENSE`, `LICENSE.txt`, `README.md`,
  `README.rst`, `aeindex/__init__.py`, `mypy.ini`, `plotAE.py`, `pyproject.toml`, `pytest.ini`,
  `setup.cfg`, `setup.py`. There is no `CITATION.cff`, `.zenodo.json`, or `codemeta.json` at any
  point. A caution for anyone re-deriving this list: `.github/CODE_OF_CONDUCT.md` entered by a
  rename (`R100` from `CODE_OF_CONDUCT.md` at commit `1c1016c`) and so is invisible to an
  additions-only listing, which undercounts by one.
- **README badges.** The pinned `README.md` carries one badge, a Travis CI build badge pointing at
  `https://travis-ci.com/space-physics/AEindex` (the `.travis.yml` it referred to was deleted at the
  pinned commit itself, so the badge is dead). There is no DOI badge — not at the pinned revision, and
  not in the `v1.0` `README.rst` either. By contrast, the same author's `lowtran` carries a Zenodo DOI
  badge in its PyPI long description, so the difference in badging practice between his repositories is
  real; what it is not, as above, is evidence about whether a deposit exists.
- **No GitHub–Zenodo archive of this repository exists.** The zero result for `"space-physics/AEindex"`
  remains sound for that narrower question: the integration signature is absent, which is independently
  what the manual-upload analysis above concludes. What it cannot establish is the broader claim that
  no DOI exists.

**A trap the deposit sets for other fields.** Both DOI records declare the licence `cc-by-4.0`. That is
not this software's licence at any point in its history: the `v1.0` tree the deposit archives carries
the GNU Affero General Public License v3, and the pinned revision carries Apache-2.0 (Field 15).
**Do not re-derive Field 15 from the DOI record** — a DOI-autofill path that copies Zenodo's
declaration verbatim would introduce a licence this software has never carried. The deposit's
publication date of 2017-03-13 sets a related trap for Field 10, addressed in the note there.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/AEindex

The repository is archived upstream and read-only (`archived: true` from
`https://api.github.com/repos/space-physics/AEindex`), but it remains publicly readable and is the
authoritative location for the source. Its earlier locations, read off the `url` value in every
`setup.py`/`setup.cfg` revision on the pinned history, were `https://github.com/scienceopen/AE-index-plot`
(2017-02-26), then `https://github.com/scivision/AE-index-plot` (2017-03-13), then
`https://github.com/scivision/AEindex` (2018-09-23). Each of those three was followed on 2026-08-29 and
redirects to `https://github.com/space-physics/AEindex` with HTTP 200, so none should be recorded in
preference to it; the current value first appears in `setup.cfg` at commit `88629b6` (2019-05-28).

A fourth `url` value precedes all of these and is **not** an earlier location of this repository. The
first packaging commit, `a5daffc` (2017-02-23) — not the repository's root commit, which is `5d4bbd02`
"Initial commit" seven minutes earlier and adds only `.gitignore`, `LICENSE` and `README.md` — declares
`url='https://github.com/scienceopen/weaksig-plot'` — a different, unrelated project by the same
author, which today redirects to `https://github.com/space-physics/weaksig-plot`. It was replaced with
`AE-index-plot` three days later at `925fcf6` (2017-02-26). It is recorded here so a future agent
mining the git history does not mistake it for a prior home of this software: it is a copy-paste
artifact in the initial packaging file, of a piece with the `setup.cfg` inheritance described under
Fields 5 and 12.

### 4. Software Functionality (RECOMMENDED — treated as critical)
- Data Processing and Analysis
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: Line Plots

Grounded in the whole of the package's user-facing API, which is two functions in
`aeindex/__init__.py`:

- `readae(fn: Path, tlim: Sequence[datetime] = None) -> pandas.DataFrame` parses the Kyoto WDC-like
  fixed-width AE table with `pandas.read_fwf`, using an explicit column-boundary list, then
  restructures each hourly record into 60 one-minute rows indexed by timestamp, for each of the four
  indices `AE`, `AU`, `AL`, `AO`. That restructuring-plus-parsing is *Processing*; the construction of
  a minute-cadence datetime index and the `tlim` time-window filter are *Time Series Analysis*.
- `plotae(dat: pandas.DataFrame, tlim)` creates a matplotlib figure, calls `dat.plot(ax=ax)`, and sets
  axis labels, title and x-limits. `dat.plot()` on a datetime-indexed frame draws one line per column,
  so this is *Line Plots*, and the parent *Data Visualization*.

Both subcategories carry their parent, as the taxonomy requires.

**Considered and rejected**, with reasons — an earlier revision of this dossier asserted the first
three, so they are recorded here to stop them being reintroduced:

- *Data Processing and Analysis: Data Access and Retrieval* — the package retrieves nothing. A
  case-insensitive search of every `.py`, `.cfg` and `.toml` file in the pinned tree for `http`,
  `urllib`, `requests`, `download`, `ftp`, `savefig`, `to_csv`, `write` and `open(` yields exactly one
  hit: the `url = https://github.com/space-physics/AEindex` line in `setup.cfg`. `readae` takes a local
  `Path`; the user downloads the file by hand from the Kyoto web form.
- *Data Processing and Analysis: Analysis* — no derived physical quantity, statistic, or fit is
  computed. The values plotted are the index values as published.
- *Data Visualization: 2D Graphics* — that subcategory means contour/heatmap/image output; this
  package draws lines only.
- *Data Processing and Analysis: File Format Conversion* — nothing is written to disk, so no format
  conversion occurs; the WDC-like table is parsed into an in-memory DataFrame and that is the end of it.
- *Data Processing and Analysis: Data Reduction* — the `tlim` filter is a user-specified time-window
  subset, not volume reduction, averaging, binning or noise filtering.

### 5. Related Region (RECOMMENDED — treated as critical)
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Magnetosphere

As stored on 2026-08-29, before this refresh, HSSI held `Earth Atmosphere` and `Earth Magnetosphere`.
The Region vocabulary has since grown to 24 rows (confirmed against
`/api/models/Region/rows/all/` on 2026-08-29), and it is **flat** — every row is a top-level value,
no row implies any other, and "region X encompasses region Y" is therefore not an argument for or
against any value. The field definitions direct: "Prefer the most specific applicable region (e.g.
`Earth Ionosphere` over `Earth Atmosphere`)."

Each candidate, accepted or rejected on the physics plus repository evidence:

- **`Earth Auroral Subregion`.** The auroral electrojets are the intense horizontal currents
  that flow *within and below the auroral oval*; the AE index exists to quantify exactly that. The
  twelve contributing Kyoto observatories are sited to ring the auroral zone. This is the single most
  specific true statement of where this software's subject matter lives.
- **`Earth Ionosphere`.** The electrojet is an ionospheric Hall/Pedersen current sheet at
  roughly 100–130 km. The `ionosphere` keyword in `setup.cfg` is one of the two keywords added
  deliberately for this package rather than inherited (see the boilerplate analysis below), and
  `ionosphere` is also a GitHub repository topic on the upstream repo.
- **`Earth Magnetosphere` — retained; it was already stored.** The auroral electrojets are the
  ionospheric closure path of the Region 1/Region 2 field-aligned current system, so the index is a
  standard measure of magnetosphere–ionosphere coupling. `geomagnetic` is likewise a GitHub topic on
  the repository.
- **`Earth Atmosphere` — removed.** True only in the loose sense that the ionosphere is part of the
  atmosphere; the field definitions explicitly prefer the specific term. Because the vocabulary is
  flat, keeping it alongside `Earth Ionosphere` would not have been logically wrong, merely
  uninformative — which is why it was dropped in favour of the specific term rather than defended.
- **`Earth Thermosphere` — not added; the closest call on this field.** In favour: the electrojet
  current sheet is altitude-co-located with the lower thermosphere, and AE is routinely used as a
  driver/proxy in thermospheric Joule-heating and density studies. Against: AE is a measure of an
  ionospheric *current*, not of any thermospheric state variable, and this package neither models nor
  derives a thermospheric quantity. Critically, the `thermosphere` keyword in `setup.cfg` is **not**
  evidence here — it is inherited boilerplate (below). Adding it for driver-index discoverability
  would be a defensible judgement; it was not added because the exclusion turns on what the software
  supports science functionality *for*, not on any claim that the physics is unrelated.
- **`Earth Lower and Middle Atmosphere` — rejected, firmly.** That region ends below the electrojet
  altitude. Its only apparent support is the `mesosphere` keyword, and that keyword is inherited
  boilerplate traceable to lowtran's own keyword list (below).
- **`Earth Magnetotail` — rejected.** AE is the canonical *substorm* index and substorm onset is a
  magnetotail process, so the causal link is real; but the index is a ground magnetic measurement of
  ionospheric currents and the software makes no tail measurement or inference.
- **`Earth Inner Magnetosphere` — rejected.** The inner-magnetosphere/ring-current index is Dst or
  SYM-H, not AE. Kyoto WDC publishes both; this software reads only the AE family.
- Two further terrestrial rows were checked and rejected: **`Earth Magnetosheath`** (the shocked
  solar-wind layer outside the magnetopause, which the electrojet system does not reach) and
  **`Earth Outer Magnetosphere`** (rejected for the same reason as `Earth Magnetotail` — a causal
  driver region, not a region this software measures or models). The remaining rows in the 24-value
  vocabulary are solar, heliospheric, or non-terrestrial-planetary and are inapplicable on their face.

**The keyword-boilerplate finding, which decides two of the rejections.** `setup.cfg` lists
`mesosphere, thermosphere, ionosphere, aurora`. That block did not exist in this project before the
2018-09-23 template commit — the immediately preceding `setup.py` (`git show 8b04386^:setup.py`)
declares no keywords at all. The template commit's `setup.cfg` read `name = lowtran`, and the real
`lowtran` 2.4.0 sdist on PyPI
(`https://files.pythonhosted.org/packages/db/00/a76204de792d97eef7622c3e70f829eb970a4e601669fa423888a0ecfccb/lowtran-2.4.0.tar.gz`)
contains a `setup.cfg` whose keywords are `mesosphere, stratosphere, thermosphere` — lowtran being an
atmospheric absorption/transmission model for which those are apt. So `mesosphere` and `thermosphere`
arrived in this package by copy-paste from an atmospheric radiative-transfer code, while `ionosphere`
and `aurora` were added on purpose for this one (and `stratosphere` was dropped). A previously
plausible-sounding argument — that this keyword block is a shared template across the author's
repositories, making it weak evidence generally — is **false and should not be repeated**: the
three sibling packages checked carry distinct, apt keyword lists (`space-physics/ACE_magnetometer`:
`IMF, magnetic field, geospace`; `space-physics/reesaurora`: `ionosphere, aurora`;
`space-physics/gima-magnetometer`: `magnetometer, geomagnetic`). The correct statement is narrower and
stronger: *these two specific keywords are traceable to lowtran's own keyword list.*

### 6. Authors (MANDATORY)

**Author 1:**
- **Author:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493
- **Affiliation 2:**
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found

These values are the ones HSSI already held as stored on 2026-08-29, and the identity evidence below
confirms them rather than revising them. The ORCID must not be re-sent and the author entry must not
be restructured: the stored Person row already carries that identifier, and re-supplying an identifier
for an already-identified stored author risks creating a duplicate Person row rather than updating the
existing one.

Identity evidence, recorded so a future agent can defend the entry without re-deriving it:

- **Sole contributor.** `https://api.github.com/repos/space-physics/AEindex/contributors` returns
  exactly one contributor, `scivision`, GitHub id 10931741, with 16 contributions — matching the 16
  commits reachable from the pinned revision. `git shortlog -sne bcb6ac4aa2c1691d12dbf23ac4f9c9f7eb002c8c`
  attributes all 16 to four author strings that are the same person under GitHub noreply addresses:
  `Michael Hirsch, Ph.D <scivision@users.noreply.github.com>` (10),
  `scivision <scivision@users.noreply.github.com>` (4),
  `Michael Hirsch <10931741+scivision@users.noreply.github.com>` (1), and
  `scivision <10931741+scivision@users.noreply.github.com>` (1). The numeric prefix `10931741+` in two
  of those addresses is the GitHub account id, which ties the commits to account `scivision` directly
  rather than by name resemblance. `setup.cfg` gives `author = Michael Hirsch, Ph.D.` and
  `author_email = scivision@users.noreply.github.com`.
- **ORCID → person.** `https://pub.orcid.org/v3.0/0000-0002-1637-6526/person` gives given name
  `Michael`, family name `Hirsch`. `.../employments` gives one employment: Boston University,
  department `ECE`, role `Research Scientist`, start 2018-08, no end date.
- **ORCID → GitHub account.** The JOSS paper for PyMap3D, `10.21105/joss.00580`
  (`https://joss.theoj.org/papers/10.21105/joss.00580.json`), lists author Michael Hirsch with ORCID
  `0000-0002-1637-6526`, affiliation string `Boston University ECE Dept., SciVision, Inc.`, and
  `software_repository: https://github.com/scivision/pymap3d`. That single record independently
  corroborates the ORCID, both stored affiliations, and the link to the `scivision` GitHub account.
- **The Boston University ROR is correct.** `https://api.ror.org/v2/organizations/05qwgg493` returns
  display name `Boston University`, located in Boston. Note that the ORCID employment record
  disambiguates Boston University by RINGGOLD id 1846, not by ROR, so the ROR was resolved
  independently and does not come from ORCID.
- **Scivision, Inc. has no ROR, and this is a researched negative, not a gap.** A ROR search for
  "Scivision" (`https://api.ror.org/v2/organizations?query=Scivision`) returns exactly one
  organization, `SciVision Biotech Inc. (Taiwan)`, `https://ror.org/011qev639`, in Kaohsiung — an
  unrelated biotechnology company. Michael Hirsch's SciVision, Inc. is a US consultancy with no ROR
  record. **Do not attach `https://ror.org/011qev639` to this author.**

No other author is warranted. The PyHC registry names `Michael Hirsch` as the sole contact
(`https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_unevaluated.yml`).
There is no `AUTHORS`, `CONTRIBUTORS`, `CITATION.cff` or `.zenodo.json` file at any point on the
pinned history.

### 7. Software Name (MANDATORY)
Auroral Electrojet

This is the name the PyHC registry publishes for this package
(`- name: Auroral Electrojet` with `code: https://github.com/space-physics/AEindex` in
`_data/projects_unevaluated.yml`), and it is the name HSSI already held on 2026-08-29. PyHC is a
manually
curated registry and takes priority over repository-derived strings.

**Considered and rejected: `AEindex`.** That is the repository name, and `aeindex` is the Python
package/import name (`setup.cfg` `name = aeindex`; `aeindex/__init__.py`). It is rejected because the
curated registry name is more informative to a heliophysics reader searching HSSI, because it is the
value a prior submitter deliberately chose, and because `AEindex` remains discoverable through the
Code Repository URL and the `ae-index` keyword. Two further historical names appear in old packaging
metadata and are wrong for any purpose today: `AEindex_plot` (the distribution name in `setup.py`
before 2018-09-23) and `AE-index-plot` (the original repository name).

### 8. Description (MANDATORY)
Auroral Electrojet AE-index read and plot. This software loads and plots auroral electrojet indices
(AE, AU, AL, AO) from data files obtained from the AE-index data web interface at Kyoto University.
The data is provided in WDC-like format as ASCII data tables.

Carried over from the existing HSSI record. Each factual claim in it was re-checked against
the pinned source and holds: the four indices `AE`, `AU`, `AL`, `AO` are exactly the columns
`readae` builds (`pandas.DataFrame(columns=['AE', 'AU', 'AL', 'AO'])`); the README names the
"[AE-index data web interface](http://wdc.kugi.kyoto-u.ac.jp/aeasy/index.html)" as the data source and
specifies "'AE output' in 'WDC-like format' as [ASCII data tables]". It is not reworded: this is a
prior submitter's deliberate phrasing and it is accurate.

### 9. Concise Description (OPTIONAL)
Auroral Electrojet AE-index read and plot.

Carried over from the existing HSSI record. This exact sentence is the upstream GitHub repository description (the
`description` field of `https://api.github.com/repos/space-physics/AEindex`), the first content line
of `README.md`, and the PyHC registry `description`. Three independent sources agree on it, so there
is no better candidate.

### 10. Publication Date (RECOMMENDED)
2017-02-23

Carried over from the existing HSSI record. The repository was created 2017-02-23T22:47:13Z (GitHub API `created_at`) and
the first commit, `5d4bbd02fff9d0bdd42bc546484fe432533162df` "Initial commit", is dated
2017-02-23 17:47:14 -0500, i.e. 22:47:14Z — the same date in UTC and in the author's local time, so the
value is not sensitive to timezone interpretation.

**Considered and not selected: the Zenodo deposit's Issued date, 2017-03-13.** The DOI recorded in
Field 2 was published on that date, and now that Field 11 names Zenodo as the publisher a reader will
reasonably ask why this field does not follow it. The field asks for the date of first
broadcast/publication, and this software was first published — publicly readable at its repository —
on 2017-02-23, eighteen days before it was deposited. The deposit date is not lost: it is the release
date of `v1.0`, recorded in Field 12 alongside that version's DOI. The recorded value is therefore left
unchanged. The alternative reading — that the field's "used for the initial version of the software"
points at the first tagged release rather than at first publication — is noted here so that a future
agent weighs it deliberately rather than discovering the eighteen-day gap and closing it silently in
one direction or the other.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Corrected 2026-08-31.** This field previously read `GitHub` / `https://github.com`, on the rationale
that "with no DOI (Field 2), the publisher is the repository host" and that "Zenodo would be the answer
only if a GitHub-Zenodo archive existed." Both halves of that rationale fail. A DOI does exist
(Field 2), so the field's no-DOI branch — "If no DOI has been obtained, indicate the repository host" —
no longer applies; and the field's positive rule is *a DOI obtained through Zenodo*, with the
GitHub–Zenodo workflow named as an example of how that comes about ("e.g., GitHub-Zenodo workflow")
rather than as a condition on it. DataCite reports `publisher: "Zenodo"` for both the concept and the
version DOI. HSSI held `GitHub` in this field before this refresh.

**This entry reaches the cohort rule by a different route than its siblings.** DASCutils, the Digital
Meridian Spectrometer, AstrometryAzEl and ApexPy all record Zenodo here because their DOIs were minted
through the GitHub–Zenodo release integration. This software's DOI was uploaded to Zenodo by hand, with
no integration and no repository link in the deposit at all (the evidence is in Field 2). The route
differs; the publisher does not. Zenodo published the deposit that carries the DOI either way — which
is precisely why the example in the field's rule must not be read as the rule itself.

**From the searcher's side this is also the only non-confusing option.** The record shows a resolving
Zenodo DOI in Field 2; "Publisher: GitHub" displayed beside it would invite a reader to conclude that
one of the two must be wrong.

Zenodo has no ROR that would serve as a better identifier — a ROR v2 query for "Zenodo" returns zero
results — so `https://zenodo.org` is the URL fallback the field allows ("ROR identifier when available
or URL otherwise"). Do not substitute CERN's ROR: CERN operates Zenodo but is not the publisher named
in the DOI metadata.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.0
- **Version Date:** 2017-03-13
- **Version Description:** Initial
- **Version PID:** https://doi.org/10.5281/zenodo.376875

This field was the substantive problem with this entry. As stored on 2026-08-29, before this refresh,
HSSI held version `v2.4.0` with no release date and no version PID. **`2.4.0` is a different package's
version number and was never a release of this software.** The provenance chain is established and is
recorded here in full so that no future agent has to re-derive it, and so that nobody reintroduces
`2.4.0` from `setup.cfg`:

1. `setup.cfg` did not exist in this repository before commit `8b04386` (2018-09-23, message
   "template"). At that commit it reads:
   `name = lowtran`, `version = 2.4.0`, `author = Michael Hirsch, Ph.D.`,
   `description = Load and Plot auroral electroject indices`, `url = https://github.com/scivision/AEindex`.
   The name and version are lowtran's; the description and URL are AEindex's — a partially edited
   copy-paste.
2. The name was corrected to `aeindex` eight months later at `88629b6` (2019-05-28, "CI template").
   **The version was never corrected.** All four `setup.cfg` revisions on the pinned history —
   `8b04386` (2018-09-23), `88629b6` (2019-05-28), `9042318` (2019-11-22), `bb7cdd1` (2020-02-19) —
   read `version = 2.4.0`.
3. `lowtran` 2.4.0 is a real release by the same author: `https://pypi.org/pypi/lowtran/json` lists
   `lowtran-2.4.0.tar.gz` uploaded 2018-08-13T22:56:22Z, roughly six weeks before the template commit.
   The `setup.cfg` inside that sdist is recognisably the source of the copied block: same
   `[metadata]` key order, `version = 2.4.0`, `author = Michael Hirsch, Ph.D.`, the keyword list
   discussed under Field 5, and a classifier block of which AEindex's is the same list minus
   `License :: OSI Approved :: MIT License` and `Programming Language :: Fortran` and with later
   Python versions appended.
4. **This software was never published to PyPI under any name it has used.** Both the JSON API and the
   Simple API return 404 for `aeindex`, `AEindex`, `aeindex-plot`, `AEindex_plot`, `aeindex_plot` and
   `ae-index-plot` (checked 2026-08-29). Those two endpoints are the authoritative absence test; the
   HTML project page is not, because it can return 200 behind a bot gate even for a package that does
   not exist. So there is no PyPI release history that could rehabilitate `2.4.0`.

**The one genuine release marker.** The repository has exactly one git tag, `v1.0`, at commit
`67ddc6287000950784c3f960b3f791311044ebe7`, dated 2017-03-13 02:10:45 -0400. There is a matching
GitHub Release: `https://api.github.com/repos/space-physics/AEindex/releases` returns exactly one
release, tag `v1.0`, name `Initial`, `published_at` 2017-03-13T06:11:06Z, with an empty body. Tag date
and release date agree once the -0400 offset is applied. The recorded Version Description `Initial` is
the release's own published title, character for character; the release has no release notes to draw a
longer summary from.

**A property of the upstream history that will otherwise confuse a future reader.** The commit the
`v1.0` tag points at is **not an ancestor of the pinned revision**: `git merge-base 67ddc628
bcb6ac4aa2c1691d12dbf23ac4f9c9f7eb002c8c` returns nothing at all, because the two commits sit on
lineages with different root commits (`b4153646` for the tag, `5d4bbd02` "Initial commit" for the
pinned branch). The upstream repository's history was evidently rewritten at some point and the tag
was left pointing at the pre-rewrite lineage; both are still present in the repository's object set
and `git ls-remote --tags https://github.com/space-physics/AEindex` returns
`67ddc6287000950784c3f960b3f791311044ebe7 refs/tags/v1.0` from the live remote, so this is a property
of the upstream repository and not of any local clone. **This does not weaken the v1.0 evidence** —
the tag and the GitHub Release are real, dated, author-published facts about this software regardless
of branch ancestry. It does mean `git log` on the current `master` will never show the tagged commit,
and it reinforces the caveat below that v1.0 does not describe the archived HEAD.

**Why `v1.0` rather than an empty version.** `v1.0` records a true, dated, author-published release of
this software, and it is what the repository's own Releases panel shows. Its weakness is that v1.0
predates most of the code's evolution (packaging modernised 2018–2020, `.travis.yml` removed 2022), so
it does not describe the archived HEAD. Clearing the version entirely was the alternative and was
rejected: it is defensible on the grounds that no release corresponds to the archived state of the
code, and that recording a 2017 version alongside a 2022 last-push date could mislead, but it discards
a true fact in order to avoid a partial one.

**The Version PID, recorded 2026-08-31.** This sub-field previously read `Not found`, justified by
Field 2's superseded conclusion that no DOI existed for any version; that justification fell with
Field 2's correction. `https://doi.org/10.5281/zenodo.376875` is the version-specific Zenodo DOI paired
with the concept DOI recorded in Field 2, carrying `IsVersionOf` back to `10.5281/zenodo.789099`. It
belongs here rather than in Field 2 under the cohort convention, and it is the right version DOI for
*this* version row on direct evidence rather than by elimination: the deposit's artifact
`AE-index-plot-1.0.tar.gz` unpacks to a file set byte-identical to the `v1.0` tag tree (the full
identity argument is in Field 2), its Issued date is 2017-03-13, and the Zenodo record was created
about five minutes after the GitHub `v1.0` release was published. Version number, version date and
version PID recorded here therefore all describe one and the same release. The PID inherits the same
limitation as the number — it archives the 2017 release, not the archived HEAD — and that is a reason
to read the three sub-fields together, not a reason to doubt any of them. HSSI held no version PID for
this software before this refresh.

**One thing not to expect here.** Neither Zenodo nor DataCite declares a `version` string for this
deposit; both report it as null. Where a sibling record in this cohort does declare one and can be
matched on that string — DASCutils's `v3.0.0`, AstrometryAzEl's `v1.4.1` — the pairing of this DOI to
`v1.0` rests on artifact identity and timing instead. That is stronger evidence, not weaker — but an agent
looking for a declared version string will not find one, and must not read its absence as a mismatch.

`v2.4.0` must not return under any reading: it is not a version of this software and it carries no
date.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

Carried over from the existing HSSI record, and independently confirmed rather than merely read off the inherited
classifier block. `setup.cfg` declares `python_requires = >= 3.6` and classifiers for Python 3.6, 3.7,
3.8 and 3.9. The code itself is Python 3 only: `aeindex/__init__.py` uses PEP 484 type annotations on
both function signatures (`fn: Path`, `tlim: Sequence[datetime] = None`, `-> pandas.DataFrame`) and
`pathlib`. There is no compiled or non-Python source anywhere in the tree.

### 14. Reference Publication (OPTIONAL)
Not found

There is no paper describing this software. No `CITATION.cff` exists at any point in the history, the
README carries no citation section, and this author's JOSS papers are for other packages (PyMap3D,
`10.21105/joss.00580`), not for AEindex. Note the Eos article linked from the README is *about the AE
index*, not about this software — see Field 27 for why it is not recorded there either.

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** https://spdx.org/licenses/Apache-2.0.html

As stored on 2026-08-29, before this refresh, HSSI held no license value for this entry; recording it
fills a real and repository-evidenced gap. `LICENSE.txt` in the pinned tree is the Apache License, Version 2.0 —
176 lines, opening "Apache License / Version 2.0, January 2004 / http://www.apache.org/licenses/".
GitHub's own license detection agrees: `https://api.github.com/repos/space-physics/AEindex` reports
`license.spdx_id: Apache-2.0`. `Apache License 2.0` is the exact row name in the HSSI License
vocabulary (confirmed against `/api/models/License/rows/all/` on 2026-08-29, 11 rows on this target).

Two details a future reader should know rather than rediscover:

- **The file omits the Apache appendix entirely.** It ends at "END OF TERMS AND CONDITIONS"; the
  "APPENDIX: How to apply the Apache License to your work" boilerplate, and with it the
  `Copyright [yyyy] [name of copyright owner]` line, is not present at all — this is not a case of a
  placeholder left unfilled. The license grant itself is complete and unambiguous, so this does not
  affect the recorded value.
- **The project was relicensed.** The initial commit (2017-02-23) added a `LICENSE` file containing
  the GNU Affero General Public License v3, and the pre-2018 `setup.py` carried the classifier
  `License :: OSI Approved :: GNU Affero License`. At commit `bb7cdd1` (2020-02-19, "meta") the AGPL
  `LICENSE` was deleted and the Apache-2.0 `LICENSE.txt` added in the same commit; `LICENSE.txt` has
  not been modified since. **The AGPL is historical and must not be recorded** — the pinned revision,
  and every revision since 2020-02-19, is Apache-2.0.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- ae-index
- aurora
- auroral electrojet
- geomagnetic
- ionosphere
- ionosphere_thermosphere_mesosphere
- mesosphere
- thermosphere

Carried over from the existing HSSI record (HSSI title-cases keywords for display, so the
same eight appear rendered as `Ae-Index`, `Auroral Electrojet`, and so on). Their sources:
`ae-index`, `aurora`, `geomagnetic` and `ionosphere` are the four GitHub repository topics
(`topics` in `https://api.github.com/repos/space-physics/AEindex`); `mesosphere`, `thermosphere`,
`ionosphere` and `aurora` are the `setup.cfg` keywords; `ionosphere_thermosphere_mesosphere` is the
PyHC registry classification tag; `auroral electrojet` is the subject itself, present in the software
name and description.

**Caveat worth carrying forward:** `mesosphere` — and, for evidentiary purposes, `thermosphere` — are
traceable to `lowtran`'s keyword list via the copy-pasted `setup.cfg` (the full chain is under
Field 5). They are retained here because Keywords is an open, low-cost discovery vocabulary and
because PyHC's own `ionosphere_thermosphere_mesosphere` tag independently groups this package with
ITM software. But **they must not be cited as supporting evidence** for Fields 5 or 22.

**Considered and not selected: `substorm`.** The AE index is canonically a substorm-activity index and
the term would improve discoverability, particularly since the Related Phenomena vocabulary has no
substorm row (Field 22). It is not added because the word appears nowhere in the repository, the
README, the packaging metadata, the GitHub topics, or the PyHC entry, and keywords in these dossiers
are kept evidence-backed. Adding it on domain grounds alone would be a defensible curatorial
judgement rather than a correction; the omission recorded here is deliberate, not an oversight.

### 17. Data Sources (OPTIONAL)
- WDC

As stored on 2026-08-29, before this refresh, HSSI held `HTTP/HTTPS Directories`. That value is not
supported by the code: **this package performs no retrieval of any kind.** `readae` accepts a local
`fn: Path` and hands it straight to `pandas.read_fwf`; `plotAE.py` passes an argparse-supplied
filename. The exhaustive search described under Field 4 — every `.py`, `.cfg` and `.toml` file in the
pinned tree, for `http`, `urllib`, `requests`, `download`, `ftp` and related tokens — finds only the
repository URL in `setup.cfg`. The README instructs the user to obtain the file by hand from the Kyoto
"AE-index data web interface", which is an interactive request form, not an HTTP directory listing, so
even the manual workflow does not match the superseded term.

`WDC` is a row in the live DataInput vocabulary (confirmed against `/api/models/DataInput/rows/all/`
on 2026-08-29, 17 rows on this target; the field's documented traps note that `WDC` carries an empty
`identifier`, which is expected for that row and not a defect). It is the accurate description of the
data input source this software is built for: the AE, AU, AL and AO indices published by the World
Data Center for Geomagnetism, Kyoto, in their WDC-like fixed-width ASCII format, whose column layout
`readae`'s hard-coded boundary list reproduces.

**Alternatives considered and rejected.** Keeping `HTTP/HTTPS Directories` alongside `WDC` would have
left an unsupported claim of HTTP retrieval in the record. Pairing `WDC` with `Other` adds nothing.
`Observatory/Mission-specific` was rejected because the WDC AE product is a derived global index
synthesised from twelve observatories, so it is a multi-observatory archive product rather than a
single observatory's data (this is the same reasoning that keeps Fields 31/32 empty).

### 18. Input File Formats (RECOMMENDED)
- ascii

Carried over from the existing HSSI record. `readae` calls `pandas.read_fwf`, the fixed-width ASCII reader, on the Kyoto
"WDC-like format" table; the README describes the input as "[ASCII data tables]" and links the format
specification at `http://wdc.kugi.kyoto-u.ac.jp/aeasy/format/aeformat.html` (reachable over HTTPS,
verified 2026-08-29). `ascii` is the exact row name in the live FileFormat vocabulary (confirmed
2026-08-29). No other format is read: there is no CDF, netCDF, HDF5, FITS, JSON or CSV path in the code.

### 19. Output File Formats (RECOMMENDED)
Not found

Correctly empty, and this is an evidenced conclusion rather than a gap. `plotae` builds a matplotlib
figure and returns nothing; `plotAE.py` ends with `show()`, which renders interactively. There is no
`savefig`, no `to_csv`, no file-writing call, and no `open(` for writing anywhere in the pinned tree
(same exhaustive search as Field 4). The package produces an on-screen figure and an in-memory
`pandas.DataFrame`, neither of which is a file format.

### 20. Operating System (RECOMMENDED)
- Operating System Independent

Carried over from the existing HSSI record. `setup.cfg` declares `Operating System :: OS Independent`, but because that
classifier block is part of the inherited lowtran template it is corroborated independently rather
than relied on: the package is pure Python with no compiled extension, no platform-conditional code,
no shell invocation, and it uses `pathlib` for path handling. The now-deleted `.travis.yml` ran only
`flake8` and `mypy`, so CI configuration offers no additional platform evidence either way.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Carried over from the existing HSSI record. Pure Python with no compiled extension modules, no architecture-specific
intrinsics, and no GPU or MPI code. Its runtime dependencies (`python-dateutil`, `numpy`, `pandas`,
plus optional `matplotlib` and `seaborn`) impose no architecture constraint that this package adds
to; nothing in its own code is architecture-sensitive.

This conclusion rests on the code, not on `setup.cfg`, and deliberately so: the dependency block is
itself partly inherited from the lowtran template described in the scope note. lowtran 2.4.0's own
sdist `setup.cfg` declares `install_requires = python-dateutil, numpy, xarray` and the same
`plot = matplotlib, seaborn` extra, so AEindex's list is that block with `pandas` substituted for
`xarray`. The substitution is apt — `readae` genuinely returns a `pandas.DataFrame` — but the point
for this field is that no packaging declaration was relied on: there is no CPU or architecture
classifier in `setup.cfg` at all, and the recorded value follows from reading the two source files.

### 22. Related Phenomena (OPTIONAL)
Not found

As stored on 2026-08-29, before this refresh, HSSI held no phenomena for this entry, and the field is
deliberately left empty. The Phenomena vocabulary has since gained `Geomagnetic Storms`, which was
absent from the stale value list this
dossier's predecessor consulted; the live vocabulary is 7 flat rows — `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`,
`X-ray emission` — confirmed against `/api/models/Phenomena/rows/all/` on 2026-08-29. That enumeration
is the substantive reason this field is correctly empty rather than unexamined: **the phenomenon this
software actually serves — auroral/substorm activity — has no row.** Five of the seven rows are solar
or coronal and are inapplicable on their face; `Solar Wind` is a driver of the electrojet but is not
what the AE index measures.

That leaves `Geomagnetic Storms` as the only candidate, and it was rejected:

- AE is a measure of auroral-zone electrojet intensity, driven predominantly by substorms. The
  canonical storm indices are Dst and SYM-H, which the Kyoto WDC publishes separately and which this
  software does not read.
- There is a specific, well-known physical reason AE is a poor storm metric: during large storms the
  auroral oval expands equatorward of the twelve fixed AE observatories, so the electrojet's peak
  moves off the station chain and AE systematically underestimates activity. Recording
  `Geomagnetic Storms` would therefore assert support for exactly the regime where the index is least
  trustworthy.
- The README's own explanatory link is Kamide & Rostoker (2004), "What is the physical meaning of the
  AE index?" (`https://doi.org/10.1029/2004EO190010`) — a paper devoted to the interpretive limits of
  the index. The author's chosen framing is about what AE means, not about storm analysis.

**The argument on the other side, recorded so it is not re-litigated:** AE is routinely plotted
alongside Dst in storm studies, and adding `Geomagnetic Storms` for discoverability rather than leaving
the field empty would be a legitimate curatorial call. It was not taken, for the three reasons above.
What must not happen is inventing a substorm or auroral-activity term: the vocabulary is closed and any
unknown value is rejected outright. The substorm framing is instead served by Keywords (Field 16),
where `aurora`, `auroral electrojet` and `geomagnetic` already appear.

### 23. Development Status (RECOMMENDED)
- Unsupported

As stored on 2026-08-29, before this refresh, HSSI held no development status. The live RepoStatus
vocabulary is 8 rows (confirmed against `/api/models/RepoStatus/rows/all/` on 2026-08-29) carrying the
repostatus.org definitions. Six are excluded immediately: `Active` (no development since 2022-08-11);
`WIP`, `Suspended` and `Abandoned`, whose definitions all begin from "there has not yet been a stable,
usable release", whereas this package is complete and works; `Concept`, defined as minimal or no
implementation, or a repository intended only as a limited example, demo or proof-of-concept, which a
working installable package with a console script is not; and `Moved` (nothing succeeded it — see
below). The real choice was between two:

- **`Inactive`** — "The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows."
- **`Unsupported`** — "The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired."

**The evidence.** `https://api.github.com/repos/space-physics/AEindex` reports `archived: true`. The
last push was 2022-08-11T13:37:11Z, and the pinned revision is that push — commit `bcb6ac4`,
"Delete .travis.yml", which removed the project's CI rather than adding anything.

**Why `Unsupported` and not `Inactive`.** Archiving a GitHub repository makes it read-only: it can accept no
issue, no pull request, and no commit until someone deliberately unarchives it. That falsifies
`Inactive`'s defining clause — "support/maintenance will be provided as time allows" — because the
platform makes even as-time-allows maintenance impossible in place. Archiving is not passive drift; it
is the author's explicit, deliberate act of declaring work finished, which is precisely
`Unsupported`'s "the author(s) have ceased all work on it."

**The counter-argument, recorded so it is not re-litigated:** nothing in the repository says a new
maintainer is desired, and `Unsupported` may read as a stronger disclaimer than intended for a small
utility that simply has nothing left to do. `Inactive` is the softer reading, and it was weighed and
set aside for the reason above: archiving is a deliberate act, not passive drift. Note that this
choice is specific to this repository's archived state and does not follow from what was chosen for
any other entry.

**Do not cite `Development Status :: 4 - Beta` as evidence here.** That `setup.cfg` classifier is part
of the inherited lowtran template: this project's own pre-2018 `setup.py` declared
`Development Status :: 3 - Alpha`, and the "4 - Beta" value arrived with the `name = lowtran` template
commit. An earlier revision of this dossier reasoned from it; it says nothing about AEindex.

**`Moved` was considered and rejected.** The author maintains `space-physics/geomagindices`, which is
active, but it reads Ap, F10.7 and Kp — not AE — so it is not a successor to this package. Nothing in
this repository points to a replacement.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/AEindex

Carried over from the existing HSSI record. `README.md` is the project's documentation: it contains the install instruction
(`pip install -e .`), a one-line description of `plotAE.py`, the data-source and format links, and the
Kamide & Rostoker background link. The invocation example is in `plotAE.py`'s module docstring
(`./plotAE.py data/WWW_aeasy00007552.dat -t 2013-05-01T07:00 2013-05-01T11:00`). There is no separate
documentation site: `has_pages` is false and `homepage` is an empty string in the GitHub API response,
there is no `docs/` directory or Read the Docs configuration at any point in the history, and the PyHC
registry entry carries no `docs:` key (the registry does record one where a docs site exists: the
`MSISE-00` entry in this same `projects_unevaluated.yml`, also contributed by this author, carries
`docs: https://ccmc.gsfc.nasa.gov/modelweb/models/nrlmsise00.php`). Pointing this field at the repository is the field's own documented
fallback when the documentation URL is the access URL.

### 25. Funder (OPTIONAL)
Not found

Correctly empty. There is no funding statement in the README, no acknowledgements section, and no
reference publication whose Acknowledgments or Data Availability Statement could be read (Field 14) —
which is normally the best source for this field. The single funding-related artifact on the
pinned history is `.github/FUNDING.yml`, present from `bb7cdd1` (2020-02-19) until `cdcec38`
(2021-03-22, "Delete .github directory"). Below its one comment line it declared exactly two
platforms:

```
# These are supported funding model platforms

github: [scivision]
ko_fi: scivision
```

Those are personal donation platform handles, not a research funder, and they were removed a year and
a half before the pinned revision. **This is not a funder and should not be recorded as one.**

### 26. Award Title (OPTIONAL)
Not found

Correctly empty, for the same reason as Field 25: no award number, grant identifier, or acknowledgement
appears anywhere in the repository, and there is no publication to read one from.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

Correctly empty, and this is a researched negative rather than an unexamined field.

**No publication cites this software.** An ADS/SciX full-text search finds zero papers containing the
string `space-physics/AEindex` or `github.com/space-physics/AEindex`. Two controls validate that
result rather than leaving it as an unfalsifiable zero: a nonsense token returns 0 as expected, and
`full:"geospace-code/pymap3d"` — another repository by the same author — returns 2, proving the query
form does find repository URLs in full text when they are present. (A bare `full:"AEindex"` search
returns hundreds of hits, but those are papers about the AE index itself: the tokenizer folds
"AE-index" onto the same term, so that query measures nothing about this software.)

**Considered and rejected: the Eos article linked from the README.** `README.md` links "[physical
meaning of the AE index](http://onlinelibrary.wiley.com/doi/10.1029/2004EO190010/abstract)", which is
Y. Kamide and G. Rostoker, "What is the physical meaning of the AE index?", *Eos, Transactions
American Geophysical Union*, published 2004-05-11 (`https://doi.org/10.1029/2004EO190010`, verified
via the Crossref work record). It does not belong in this field: it was published thirteen years
before this software existed, so it cannot describe, cite, or use it. It is background reading about
the index the software parses. It is recorded here so its recurring appearance in the README does not
prompt a future agent to add it.

### 28. Related Datasets (OPTIONAL)
https://wdc.kugi.kyoto-u.ac.jp/aeasy/index.html

Carried over from the existing HSSI record. This is the World Data Center for Geomagnetism, Kyoto "AE-index data web
interface" — the service from which a user obtains the file that `readae` parses, and the only data
source the README names. The link resolves with HTTP 200 over HTTPS as of 2026-08-29 (the README's
own link is the `http://` form; the stored `https://` form is the correct one to keep).

No DOI exists for the Kyoto AE product, so the field's documented fallback applies: the dataset's
permanent landing page. Its full citation, for anyone who needs the prose form: World Data Center for
Geomagnetism, Kyoto. *AE-index data web interface.* https://wdc.kugi.kyoto-u.ac.jp/aeasy/index.html

The companion format specification, `https://wdc.kugi.kyoto-u.ac.jp/aeasy/format/aeformat.html` (also
200 as of 2026-08-29), was considered and **not** added: it documents the file layout rather than being
a dataset, and adding it would dilute the field.

### 29. Related Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.17634923 — PySPEDAS
- https://doi.org/10.5281/zenodo.3986138 — pysatSpaceWeather
- https://doi.org/10.5281/zenodo.2604784 — geomagindices

As stored on 2026-08-29, before this refresh, HSSI held no related software. The dependency list is not
a source of candidates here: `setup.cfg` requires `python-dateutil`, `numpy` and `pandas`, with
`matplotlib` and `seaborn` in the `plot` extra and `pytest`/`flake8`/`mypy` in dev extras. Every one of
those is the generic scientific-Python or tooling stack, which the field's own rule excludes by name —
listing them would say nothing that is not equally true of most packages in the Python ecosystem.

Three candidates pass the relevance gate on the strength of a specific, cited artifact:

- **PySPEDAS** — `https://doi.org/10.5281/zenodo.17634923`. This is the strongest match: PySPEDAS
  reads **the same data product from the same provider**. Its `pyspedas/projects/kyoto/load_ae.py`
  downloads and parses Kyoto AE, AL, AO, AU and AX values, and the module's own README states "The
  routines in this module can be used to load AE index data (AE, AL, AO, AU, AX) from the World Data
  Center for Geomagnetism, Kyoto, Japan", citing the example page
  `https://wdc.kugi.kyoto-u.ac.jp/ae_provisional/201210/ae121001.for.request`. The two packages
  perform the same task under different assumptions — PySPEDAS fetches over HTTP and emits tplot
  variables inside a large multi-mission framework; AEindex reads a hand-downloaded file and emits a
  `pandas.DataFrame` — which is exactly the contrast Field 29 exists to record. The concept DOI is the
  one PySPEDAS's own `CITATION.cff` declares (`doi: 10.5281/zenodo.17634923`).
- **pysatSpaceWeather** — `https://doi.org/10.5281/zenodo.3986138`. Ships three dedicated instrument
  modules, `sw_ae.py`, `sw_al.py` and `sw_au.py`, whose docstrings read "Supports the auroral
  electrojet AE values" (respectively AL, AU). Same indices, different provenance: its only tag is
  `'lasp'`, documented as "Predicted AE from real-time ACE or DSCOVR provided by LASP" — modelled
  real-time predictions rather than the Kyoto WDC's observatory-derived tables. That difference in
  assumptions is what makes it informative alongside this package. The concept DOI is stated in
  `sw_ae.py`'s own header comment.
- **geomagindices** — `https://doi.org/10.5281/zenodo.2604784`. The same author's and the same
  `space-physics` organisation's geomagnetic-index reader: "Geomagnetic indices downloader and parser,
  returns Ap, F10.7 (unsmoothed and smoothed) and Kp", output type `pandas.DataFrame`. It is the
  closest sibling in shape — index parser to DataFrame, with an example plot — but it covers different
  indices, and unlike this package it downloads. It is also still maintained (last push 2024-12-26,
  not archived), which is directly useful context for a reader arriving at an archived package.

**Why all three, and not fewer.** Recording PySPEDAS and pysatSpaceWeather only — on the view that a
different-indices sibling is not "similar tasks" — was considered and rejected: geomagindices is the
closest sibling in shape, and its still-maintained status is directly useful context for a reader who
arrives at an archived package. Leaving the field empty was the weakest option: three genuinely
distinguishing domain packages exist and the reader learns something real from each.

**Considered and rejected, with reasons** — recorded so these are not re-proposed:

- `space-physics/gima-magnetometer` ("UAF Geophysical Institute magnetometer network data read and
  plot", also archived) — it reads raw magnetometer network data, not a derived global index. The
  resemblance to this package is a shared authoring template, not a shared task.
- `space-physics/ACE_magnetometer` (GitHub description "Load and Plot ACE satelite magnetometer data",
  the misspelling being upstream's; also archived) —
  same objection, and its measurements are interplanetary rather than ground-based. It is also close
  to Auroral Electrojet in the PyHC unevaluated list, two entries above it under the registry name
  `ACEmag` and separated from it by `AstrometryAzEl`, which makes it easy to reach for by proximity;
  proximity is not evidence.
- `sciencedates` — a former dependency in the pre-2018 `setup.py`. It was removed before the pinned
  revision and is absent from `setup.cfg`; it is also a general date/time utility, not a domain tool.
  A future agent mining the git history should not resurrect it.
- `numpy`, `pandas`, `python-dateutil`, `matplotlib`, `seaborn`, `pytest`, `flake8`, `mypy` — generic
  infrastructure, excluded by the field's own rule.

All three recorded URLs are 38–39 characters, well inside the 128-character limit that applies to
these entries.

### 30. Interoperable Software (OPTIONAL)
Not found

Correctly empty. This field requires a *demonstrated exchange* — a shared or converted data model, an
adapter API, a plugin relationship, or a documented cross-tool bridge — and this package has none. It
exposes two functions; `readae` returns a bare `pandas.DataFrame` and `plotae` draws a matplotlib
figure. There is no converter, no `to_*`/`from_*` adapter, no plugin hook, no documented integration,
and no test or example demonstrating use with another domain package (the repository has no tests at
all, despite carrying a `pytest.ini` and a `tests` extra).

`pandas` and `matplotlib` do not qualify: being a dependency is not interoperability, and both are
named exclusions. The three Field 29 entries are *similar-purpose* tools, not interoperating ones —
nothing converts between AEindex's DataFrame and PySPEDAS tplot variables or pysat Instrument objects.
PyHC membership is likewise not a qualifying justification on its own.

### 31. Related Instruments (OPTIONAL)
Not found — documented omission, not a gap

### 32. Related Observatories (OPTIONAL)
Not found — documented omission, not a gap

Fields 31 and 32 share one piece of reasoning, recorded in full because the natural instinct on
encountering an auroral-electrojet package is to attach the AE observatory chain, and because the
relevant vocabulary rows genuinely exist — a future agent will find them and needs to know why they
were nonetheless not used.

**The rows exist.** The HSSI InstrumentObservatory vocabulary was checked against
`/api/models/InstrumentObservatory/rows/all/` on 2026-08-29: 7,602 rows, of which 0 fail the
`https://spase-metadata.org/` identifier guard, so the vocabulary was fully SPASE-backed at that date.
All twelve canonical Kyoto AE observatories resolve as type-2 rows under
`https://spase-metadata.org/IUGONET/Observatory/WDC_Kyoto/WDC/<code>` — Abisko (ABK), Dixon (DIK),
Cape Chelyuskin (CCS), Tixie Bay (TIK), Cape Wellen (CWE), Barrow (BRW), College (CMO), Yellowknife
(YKC), Fort Churchill (FCC), Poste-De-La-Baleine (PBQ), Narsarsuaq (NAQ) and Leirvogur (LRV) — and each
has a matching type-1 "Magnetometers at …" instrument row under
`https://spase-metadata.org/IUGONET/Instrument/WDC_Kyoto/WDC/<code>/Magnetometer`. There is also an
archive-level observatory row, `World Data Center Ground Observatories` =
`https://spase-metadata.org/SMWG/Observatory/WDC`, and a related
`World Data Center Ground Data Master Catalog` = `https://spase-metadata.org/SMWG/Observatory/Ground/WDC`.

**None of them passes the relevance gate.** The gate is "designed to support": the software must read,
parse, calibrate, process, or model that specific instrument's or observatory's data. This package
reads the **derived global index product** — a single number per minute per index, synthesised by
Kyoto from the twelve stations — and never touches any station's magnetometer data. Consistently with
that, the repository names no station: not in `README.md`, not in `aeindex/__init__.py`, not in
`plotAE.py`, not in the packaging metadata. Recording twelve observatories would return this package
to a user searching for, say, `observatory:"Barrow Geomagnetic Observatory"`, who would find nothing
here that helps them work with Barrow's data. Recording the twelve magnetometers would be worse: the
software cannot read a magnetometer file at all.

The archive-level `World Data Center Ground Observatories` row is also rejected, and for a reason the
field definitions state directly: a generic, multi-observatory data source belongs in **Data Sources**,
not in Fields 31/32. That is precisely where it is recorded — Field 17's `WDC` value.

This is a **documented omission, which the resolution ladder treats as a correct outcome**, not an
unresolved item. There is nothing ambiguous here to escalate: no candidate was rejected for being hard
to resolve, and no name is recorded without an identifier.

### 33. Logo (OPTIONAL)
Not found

Correctly empty, and evidenced twice over:

- **No image appears anywhere on the pinned history.** The complete list of 19 paths appearing on
  the pinned history is enumerated under Field 2; none of them is an image file, and there is no
  `docs/`, `assets/` or `img/` directory at any point.
- **The PyHC registry entry has no logo.** The `Auroral Electrojet` block in
  `_data/projects_unevaluated.yml` contains only `name`, `code`, `description`, `contact` and
  `keywords`. That the omission is meaningful rather than a registry-wide limitation is shown by the
  very next entry in the same file, `DASCutils`, which does carry
  `logo: https://i.ibb.co/JKLF4FB/logo.jpg`.

No logo is recorded. Any future proposal would have to be a commit-pinned raw URL, verified by fetch to
return an `image/*` content type with a plausible byte count (a raw GitHub URL can return HTTP 200 with
`text/plain` when it is serving a Git LFS pointer rather than an image), never a branch reference or a
`blob/` page URL, and at most 200 characters. An evidenced absence is preferable to a fragile link.
