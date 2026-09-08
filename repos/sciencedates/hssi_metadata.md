# HSSI Metadata Extraction Results

**HSSI Software ID:** c47c5638-d426-4868-ae04-bc993ab0c2e1
**Repository:** https://github.com/geospace-code/sciencedates
**Source Revision:** 8cfe3540b77dba4083e42aa91bb32942e1e26a04
**Extraction Date:** 2026-09-07
**Validation Date:** 2026-09-08
**Validation Status:** PASS

---

Scope note. All repository evidence below is read at the pinned revision
`8cfe3540b77dba4083e42aa91bb32942e1e26a04`, which is also the commit the `v1.5.1` tag points at.
That tree contains 28 tracked files. ScienceDates is a small, single-author date/time conversion
library: its installable Python package is a handful of modules of conversion functions plus two
helpers, and the repository additionally carries one-file Julia, MATLAB and Fortran examples of the
same day-of-year idea. Several fields below therefore turn on a question of *breadth* — whether the
metadata should describe the installable package or the whole tracked tree, and whether a generic
time utility should carry heliophysics domain facets at all. Both questions are settled here and the
answers differ by field: Field 13 describes the whole tracked tree, because all four languages ship
real code a searcher could use, while Fields 4, 5, 29 and 30 confine the metadata to what the
software itself does, which leaves Field 5 evidenced-empty. The reasoning for each is recorded under
that field.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The placeholder form is the catalogue-wide convention for this campaign and is not a gap to be
filled by inference. No submitter identity is recorded in the repository, the DOI record, or the
PyHC registry entry, and none is invented here.

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.598255

This is the Zenodo **concept** DOI, which always resolves to the newest deposited version. It is the
correct Field 2 value because Field 2 identifies the software as a work rather than one release; the
release-specific DOI `https://doi.org/10.5281/zenodo.5808426` belongs in Field 12 (Version PID) and
is recorded there. The `README.md` badge at the pin points at
`https://zenodo.org/badge/latestdoi/81351748`, a redirect service rather than a citable identifier,
so it is not used as the Field 2 value.

The Zenodo deposit is a GitHub-integration deposit, not a manual upload: its `related_identifiers`
consist of a single `isSupplementTo` relation to
`https://github.com/geospace-code/sciencedates/tree/v1.5.1`. That is the signature of the automated
release hook, which matters below because it explains why several Zenodo fields are machine-derived
and unreliable (see Fields 6 and 15).

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/geospace-code/sciencedates

Corroborated from three independent directions: `setup.cfg` at the pin declares
`url = https://github.com/geospace-code/sciencedates`; the PyPI project metadata gives the same
string as its `home_page`; and the PyHC registry entry's `code:` field is the same URL. The
repository is not archived and its default branch is `main`.

Note on the `scivision/` vs `geospace-code/` forms: two of the badges in `README.md` at the pin
still point at `https://github.com/scivision/sciencedates/...`, which is the project's older owner
path. GitHub redirects that path, but the canonical repository name is `geospace-code/sciencedates`
and that is the form declared in `setup.cfg` and on PyPI. A future refresh should not "correct"
Field 3 to the `scivision` form on the strength of those badges.

### 4. Software Functionality (RECOMMENDED)
- **Selected Values:**
  - Data Processing and Analysis
  - Data Processing and Analysis: Time Series Analysis

HSSI held four values for this entry before this refresh: the two above, plus `Data Visualization`
and `Data Visualization: Line Plots`. The visualization pair was removed in this refresh. The
factual basis for what was kept and what was dropped is set out below.

What the package actually exposes. `src/sciencedates/__init__.py` at the pin exports exactly:
`datetime2utsec`, `datetime2yeardec`, `yeardec2datetime`, `datetime2yeardoy`, `yeardoy2datetime`,
`date2doy`, `datetime2gtd`, `find_nearest`, `randomdate`, plus `forceutc` imported inside a
`try`/`except ImportError` block (so timezone support degrades gracefully when `pytz` is absent).
Every one of these converts between representations of an instant, or searches an array for the
value nearest a target. None of them reads a file, fits a model, or draws anything.

Why the visualization pair was removed. The only visualization-adjacent code in the tree is
`src/sciencedates/ticks.py`, whose two functions are `tickfix` and `timeticks`. `tickfix` applies
matplotlib locators and a `DateFormatter` to an axis object handed to it; `timeticks` returns a pair
of matplotlib locators chosen from the span of a `timedelta`. Neither creates a figure, an axis, or
a line. Three facts bound how much weight this module can carry: it is **not** imported by
`src/sciencedates/__init__.py`, so it is not part of the package's public surface; no test module
exercises it (the three test files at the pin are `test_conv.py`, `test_msis.py` and `test_time.py`,
and none imports `ticks`); and `README.md` at the pin never mentions it.

`Data Visualization` and `Data Visualization: Line Plots` were therefore both dropped. The module is
unexported, untested and undocumented, and even taken at face value it restyles the time axis of a
plot someone else made rather than producing one — ScienceDates never generates a line plot, which
is exactly what the `Line Plots` row denotes. The decision was made from the searcher's point of
view: someone filtering HSSI for line-plot software would not be glad to be handed a date library.
Two weaker options were considered and rejected — keeping both rows on the grounds that `ticks.py`
is real, tracked and shipped inside the installed package, and keeping the bare `Data Visualization`
parent while dropping the child so as to acknowledge that a plotting helper exists without claiming
line-plot output. Neither survives the same searcher test, because the package produces no visual
output at all.

Considered and rejected:
- **Coordinate Transforms** and all six of its subcategories. `datetime2gtd` computes a solar local
  time from a geodetic longitude (`stl[i, ...] = utsec[i] / 3600.0 + glon / 15.0` in
  `src/sciencedates/doy.py`), which is a *time* quantity derived arithmetically from a longitude,
  not a transformation between reference frames. No frame name — GSE, GSM, SM, GEO, MAG, AACGM,
  heliographic, helioprojective, Carrington — appears anywhere in the tree.
- **Models and Simulations: Empirical.** ScienceDates prepares inputs *for* empirical models
  (see Fields 29/30) but implements no model itself; there is no atmosphere, field or flux
  calculation in any tracked file.
- **Data Processing and Analysis: File Format Conversion.** The package performs no file I/O at all
  (see Fields 18/19), so the "formats" it converts between are in-memory time representations, which
  is not what this subcategory means.

Why `Data Processing and Analysis: Time Series Analysis` is the subcategory kept. Everything the
package does concerns time-ordered data, and `find_nearest` is in practice used to locate the
nearest sample time in an array (its docstring lists `datetime` among the searchable types). The
tension is acknowledged rather than hidden: the taxonomy's sense of this subcategory is *analysis*
of time-ordered data — temporal filtering, trend analysis, autocorrelation — and ScienceDates
performs none of those; it converts one timestamp at a time. It was kept anyway because it is the
available value that carries the most accurate discriminating signal about what the data is.

The alternatives, each rejected for a stated reason:
- `Data Processing and Analysis: Processing` **instead**. The taxonomy describes it as general data
  processing, pipeline steps and transforms, which is what representation conversion is. Rejected as
  vaguer: it loses the accurate signal that the data in question is temporal.
- `Data Processing and Analysis: Analysis`. This is a real row under this parent, and it describes
  derived physical quantities and scientific calculations — `datetime2gtd` does derive a local solar
  time. Rejected because most of the package is plain representation conversion rather than
  calculation, so the row would characterise a minority of the code.
- Listing `Processing` alongside `Time Series Analysis`. The two are not mutually exclusive and
  capture different true things, but `Processing` adds little discriminating power to a search.
- Keeping only the bare parent `Data Processing and Analysis`. Rejected as discarding a true and
  useful signal.

Note on the vocabulary, for a future agent: two distinct FunctionCategory rows are named `Analysis`,
one under `Data Processing and Analysis` and one under `Mission-related`. That is why every value in
this field is written in the fully-qualified `Parent: Child` form, and why any future change must be
written that way too. The functionality vocabulary rows carry empty definitions, so the category
wording quoted above comes from the classification guide's category tables rather than from the
vocabulary itself.

### 5. Related Region (RECOMMENDED)
- **Related Region:** Not found

**Field 5 was cleared in this refresh. The `Not found` marker above means deliberately emptied, not
never-populated.** HSSI held three regions for this entry before this refresh — `Solar Environment`,
`Earth Magnetosphere` and `Earth Atmosphere` — and all three were removed. Their sole provenance was
the PyHC registry: the entry in `_data/projects_unevaluated.yml` of
`heliophysicsPy/heliophysicsPy.github.io` reads

```yaml
- name: ScienceDates
  code: https://github.com/geospace-code/sciencedates
  description: Date / time conversions used in the sciences.
  contact: Michael Hirsch
  keywords: ["solar","magnetosphere","ionosphere_thermosphere_mesosphere","specific"]
```

and the three regions are a one-to-one transcription of the first three of those four facets
(`solar` to Solar Environment, `magnetosphere` to Earth Magnetosphere,
`ionosphere_thermosphere_mesosphere` to Earth Atmosphere). No repository artifact at the pin
independently supports any of them: nothing in the tracked tree names a region, an altitude range,
or a plasma domain.

The Region vocabulary is **flat** — every row is top-level, with no parent/child links — so
`Earth Atmosphere` does not imply and is not implied by `Earth Ionosphere`, `Earth Thermosphere`, or
`Earth Lower and Middle Atmosphere`, all of which are separate rows. Any argument of the form "the
coarse value already encompasses the fine one" is unsound here.

The counterweight, stated honestly: `datetime2gtd` is not a generic utility. It exists to produce
the specific time arguments that Fortran empirical upper-atmosphere models expect, and two
heliophysics packages consume it (see Fields 29/30). So there is a real, if indirect, tie to the
ionosphere/thermosphere. That tie was weighed and judged insufficient to assert a region for
software that does not model one: it is a connection to models other packages run, not a property of
what ScienceDates operates on.

Why the field was cleared. Nothing in the software is region-specific — its entire public API takes
a time and returns a time — so a regional search that returned this package would be a false
positive for the searcher. Field 5 is RECOMMENDED rather than mandatory, and an evidenced-empty
Region is a legitimate outcome, which is what this is: the regions were examined against the source
and found to have no basis in it, not left unexamined.

Alternatives considered and rejected:
- *Keep all three.* PyHC is the most carefully curated source available for this package,
  a human chose those facets deliberately, and removing them discards curation we did not do.
  Rejected because PyHC's facets classify the package's *user community*, not what the software
  operates on; the same three would be true of any utility used by heliophysicists.
- *Reduce to the ionosphere/thermosphere group only* — some combination of `Earth Ionosphere`,
  `Earth Thermosphere` and `Earth Lower and Middle Atmosphere`, or retaining `Earth Atmosphere`,
  while dropping `Solar Environment` and `Earth Magnetosphere`. This is the one regional tie with
  repository-side evidence: `datetime2gtd` and `src/sciencedates/tests/test_msis.py` exist for
  upper-atmosphere models, whereas `solar` and `magnetosphere` have no counterpart anywhere in the
  tree. Rejected because it still asserts a region for software that does not model one, and the
  finer rows overstate the specificity of a day-of-year calculation.

A future refresh should not re-add these regions from the PyHC entry: the registry facets were read,
understood, and deliberately not carried into this field. The same three facets are retained as
keywords, and Field 16 records why the two fields diverge despite the shared origin.

### 6. Authors (MANDATORY)
- **Author 1:**
  - **Author Name:** Michael Hirsch
  - **Author Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliations:**
    - Boston University — https://ror.org/05qwgg493
    - Scivision, Inc. — no identifier

ScienceDates has exactly one author. Listing every commit author string reachable from the pin
(`git log --format='%an <%ae>' <pin> | sort | uniq -c`) returns six distinct forms across 84
commits, all of them the same person and all but one sharing a single address:

```
  59 Michael Hirsch, Ph.D <scivision@users.noreply.github.com>
  14 scivision <scivision@users.noreply.github.com>
   5 Michael Hirsch <scivision@users.noreply.github.com>
   4 irs4 <scivision@users.noreply.github.com>
   1 scivision <scivision@noreply.users.gitlab.com>
   1 Michael <10931741+scivision@users.noreply.github.com>
```

Those counts sum to 84, which is the full commit count reachable from the pin
(`git rev-list <pin> | wc -l` returns 84). Five of the six forms are GitHub or GitLab noreply
addresses for the `scivision` account; the sixth is the numeric-prefix GitHub noreply form
`10931741+scivision@users.noreply.github.com`, which is genuinely present here on exactly one
commit. `setup.cfg` at the pin gives `author = Michael Hirsch, Ph.D.` and
`author_email = scivision@users.noreply.github.com`, and `LICENSE.txt` at the pin reads
`Copyright (c) 2017 Michael Hirsch, Ph.D.`. The `Ph.D.` suffix is a credential, not part of the
name, so the recorded author name drops it. `irs4` is a legacy username of the same person, not a
second contributor.

The ORCID resolves to given name `Michael`, family name `Hirsch`, and is the identifier already
carried by this author's stored record. No change is needed for it — it is noted here as context so
that a future refresh does not attempt to "add" an identifier that is already present, which for an
already-stored identifier-less author would mint a duplicate record rather than update the existing
one.

Why Zenodo is not the authority for the author name. The v1.5.1 deposit's creator block is
`[{"name": "Michael", "affiliation": null}]` — a first name with no surname and no affiliation. That
is an artifact of the automated GitHub-release integration reading a display name, not a curated
statement of authorship, and it is why the repository files and ORCID are preferred over the DOI
record for this field.

Negative research on the second affiliation. `Scivision, Inc.` is this author's own consultancy and
is stored without an identifier. A ROR query for `Scivision` returns exactly one organization,
`https://ror.org/011qev639`, whose display name is `SciVision Biotech Inc. (Taiwan)` — a Taiwanese
biotechnology company, unrelated to this author. **That ROR must not be attached to this
affiliation.** Recorded so a future agent does not re-propose it on a name match.

### 7. Software Name (MANDATORY)
- **Software Name:** ScienceDates

The camel-case display form comes from the PyHC registry entry's `name: ScienceDates`, which is a
human-curated presentation name. The lowercase `sciencedates` appearing in `setup.cfg`
(`name = sciencedates`), in the repository path, and on PyPI is the package/distribution identifier,
not a display name. Keeping the curated display form is deliberate; a future refresh should not
"correct" it to the lowercase distribution name.

### 8. Description (MANDATORY)
- **Description:** Date & time conversions used in the sciences. The assumption is that datetimes are timezone-naive, as this is required in Numpy and other scientific libraries for numpy.datetime64. This library provides conversions between datetime objects and various scientific time formats including year/day-of-year (yyyyddd), decimal year, UTC seconds, and local solar time. It supports Python, with additional examples provided for Julia, Matlab/GNU Octave, and Fortran.

The first two sentences are a lightly de-marked rendering of the opening of `README.md` at the pin,
which reads `Date & time conversions used in the sciences.` followed by a sentence stating that the
assumption is that datetimes are timezone-naive, as this is required in Numpy *et al* for
`numpy.datetime64`. The remaining sentences summarise the exported API and the additional-language
examples, and both claims check out against the tree: the exported functions cover year/day-of-year
(`datetime2yeardoy`, `yeardoy2datetime`, `date2doy`), decimal year (`datetime2yeardec`,
`yeardec2datetime`), UTC seconds (`datetime2utsec`), and local solar time (`datetime2gtd`); and
`julia/`, `matlab/` and `fortran/` each contain example scripts, which `README.md` describes as
"examples" in three separate sections.

This wording is a prior submitter's editorial construction and is preserved. It is accurate and
readable; the alternative of substituting the one-line upstream description is available as Field 9
and is already used there.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** Date conversions used in the sciences.

This is the project's own one-line self-description, identical in two independent places:
`setup.cfg` at the pin declares `description = Date conversions used in the sciences.`, and the
GitHub repository description is the same string. It is 38 characters long.

Correction to a prior claim. An earlier version of this dossier described this string as "exactly 42
characters". That is wrong: measured, its length is 38. The number is recorded here only because a
stale count invites a future agent to "fix" the string to match it.

Alternative considered and not selected: the PyHC registry's description,
`Date / time conversions used in the sciences.`, which differs by the inserted `/ time`. The
project's own `setup.cfg` and GitHub description are the more authoritative statement of how the
project describes itself in one line, and PyHC's variant appears to be a curator's light rewording.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2017-02-08

The GitHub repository's creation timestamp is `2017-02-08T16:42:17Z`. This is the earliest
defensible public date for the work, and it is corroborated by the copyright year in `LICENSE.txt`
at the pin, which is 2017. The Zenodo deposit's publication date (2021-12-29) describes the v1.5.1
release, not the software's first appearance, and is recorded in Field 12 where it belongs.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

The persistent identifier in Field 2 is a Zenodo DOI, and the deposits are made through Zenodo's
GitHub release integration, so Zenodo is the publisher of record for the archived artifact. PyPI
distributes the package but is a package index rather than the DOI-registering publisher, so it is
not the Field 11 value.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.5.1
- **Version Date:** 2021-12-29
- **Version Description:** Python >= 3.7, update type anno
- **Version PID:** https://doi.org/10.5281/zenodo.5808426

`v1.5.1` is the newest tag in the repository and the only tag pointing at the pinned commit
(`git tag --points-at <pin>` returns `v1.5.1`). Every component above is corroborated: the GitHub
release `v1.5.1` has the name `Python >= 3.7, update type anno`, an empty body, and a publication
timestamp of `2021-12-29T04:56:01Z`; the Zenodo record 5808426 has version `v1.5.1`, publication
date `2021-12-29`, and the title `geospace-code/sciencedates: Python >= 3.7, update type anno`.

The version description is the release's title line, which is all the upstream release provides —
the release body is empty, so there is no fuller changelog text available to record. This is not an
omission that a future refresh can repair from the release itself.

**Durable context: v1.5.1 never reached PyPI.** The PyPI project's newest release is `1.5.0`,
uploaded `2020-05-20T03:55:40`, and its release list ends there. So the newest tagged,
GitHub-released and Zenodo-deposited version is one release ahead of anything installable from PyPI.
A future refresh should not read the PyPI version as evidence that HSSI's stored version is stale,
and should not "correct" Field 12 down to 1.5.0.

**The `v` prefix is deliberate and unchanged.** `v1.5.1` matches the git tag exactly, matches the
GitHub release tag name, and matches Zenodo's own version field — three independent external
records, including the DOI record that this field's own Version PID points at. The unprefixed
alternative `1.5.1` was considered and rejected: `setup.cfg` at the pin declares `version = 1.5.1`
without the prefix, which is the version the software reports about itself, and PyPI's release
identifiers are likewise unprefixed, so the leading `v` can be read as a git tagging convention
rather than part of the version number. That reading loses to the three concurring external records.
A future refresh should not strip the `v` on the strength of `setup.cfg` alone.

### 13. Programming Language (RECOMMENDED)
- **Selected Values:**
  - Fortran90
  - Julia
  - MATLAB
  - Python 3.x

All four values were already stored for this entry before this refresh, and all four are retained.
What the tracked tree actually contains at the pin:

| Language | Files | Role |
|---|---|---|
| Python | the modules under `src/sciencedates/`, three test modules under `src/sciencedates/tests/`, plus top-level `date2doy.py`, `findnearest.py`, `randomdate.py` | the installable package declared in `setup.cfg` |
| Fortran | `fortran/doy.f90` | one standalone program; `README.md` says Fortran examples are provided |
| Julia | `julia/date2doy.jl`, `julia/randomdate.jl` | two standalone scripts; `README.md` says Julia examples are provided |
| MATLAB | `matlab/date2doy.m` | one function, built on `datevec`/`datenum`, also valid GNU Octave; `README.md` says Matlab / GNU Octave examples are provided |

`setup.cfg` declares `python_requires = >= 3.7` and the classifier
`Programming Language :: Python :: 3`, which fixes `Python 3.x` (not `Python 2.x`) as the Python row.

**The criterion, chosen deliberately: every language present in the tracked tree.** The value
follows from it, so a future refresh that wants to change this field should argue about the
criterion first. The repository genuinely ships working code in all four languages, and a user
searching HSSI for Julia or MATLAB code in this domain would find something real here. The argument
against was weighed and accepted as a cost: three of the four are single-file demonstrations that
`README.md` itself calls "examples" rather than deliverables; nothing installs them, and no CI runs
them — `.github/workflows/ci.yml` at the pin triggers only on pushes touching `**.py` and runs
`flake8`, `mypy` and `pytest`.

The competing criterion — *the language the installable package is written in*, which yields
`Python 3.x` alone — was rejected. `setup.cfg` packages only `src/`, so installing the distribution
delivers Python and nothing else, and on that view the other three directories are documentation by
example. It loses because it discards true information about the repository's contents and would
remove three values a searcher can act on.

**Which Fortran row, and why `Fortran90` understates by exactly one construct.** The vocabulary
offers `Fortran77`, `Fortran90`, `Fortran 2003`, `Fortran 2008` and `Fortran 2023`. **There is no
`Fortran95` row.** `fortran/doy.f90` is free-form and uses `implicit none`, `contains`,
`integer, intent(in)`, a `result()` clause and `modulo()` — all Fortran 90 — but its function is
declared `elemental integer function yyyyddd2yyddd(y4d3) result(yyddd)`, and `elemental` was
introduced in Fortran 95. The file is therefore strictly one construct newer than the nearest
available row. `Fortran90` is recorded as the closest row that does not claim features the file
lacks, accepting that it understates by that single construct; `Fortran 2003` was rejected as
overstating, because the file uses nothing introduced in that edition.

**A compiler cannot arbitrate this, and a future agent should not try.** `fortran/doy.f90` does
not compile at *any* standard: it assigns to an undeclared `doy2` and then reads `doy`
(`doy2 = modulo(y4d3, 1000)` followed by `year4 = (y4d3 - doy) / 1000`), which is a genuine typo
under `implicit none`. Compiling it with `gfortran` at `-std=f95`, `-std=f2003`, `-std=f2008` and
`-std=legacy` fails identically in all four cases at line 21 with
`Error: Symbol 'doy2' at (1) has no IMPLICIT type; did you mean 'doy'?`. The edition must
therefore be read off the language constructs, not from a compiler ladder.

### 14. Reference Publication (RECOMMENDED)
- **Reference Publication:** Not found

Evidenced absence, from four directions at the pin. There is no `CITATION.cff`, no `codemeta.json`
and no `.zenodo.json` in the tracked tree — the whole tree is 28 files and none of them is a
citation metadata file. `README.md` contains no paper citation: its only links are a Zenodo badge,
an LGTM code-quality badge, a GitHub Actions badge, a PyPI download-stats badge, and the
Datetime-Fortran pointer discussed in Field 29. The Zenodo record's related identifiers contain a
single entry, the `isSupplementTo` link to the GitHub tag tree, with no publication relation of any
kind. And `setup.cfg` carries no citation or publication field.

This is a small single-author utility library with no accompanying paper. The correct value is
empty, and a future refresh should not expect to find one.

### 15. License (RECOMMENDED)
- **License:** MIT License

HSSI held no licence value for this entry before this refresh. The evidence is unambiguous and
threefold: `LICENSE.txt` at the pin opens with the line `MIT License`, followed by
`Copyright (c) 2017 Michael Hirsch, Ph.D.` and the standard MIT permission text; `setup.cfg`
declares `license_files = LICENSE.txt`; and GitHub's own licence detection reports the SPDX
identifier `MIT`. The licence vocabulary contains a row named exactly `MIT License`, whose url is
`https://spdx.org/licenses/MIT`.

**Zenodo disagrees and is wrong.** The v1.5.1 deposit records its licence as `other-open`. That is a
known failure mode of the automated GitHub-release integration, which did not resolve the repository
licence and fell back to a generic value. The repository's own `LICENSE.txt` governs. A future
refresh should not adopt `Other` on the strength of the DOI record.

**Do not record a per-software licence URI.** An earlier version of this dossier carried a "License
URI" of `https://spdx.org/licenses/MIT.html`. There is no per-software licence URI to record: the
licence is a reference to a single shared vocabulary row that carries its own url. That row's url is
`https://spdx.org/licenses/MIT`, without the `.html` suffix, so the earlier string did not match the
shared row either. The only storable value for this field is the row name, `MIT License`.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Keywords:**
  - calendar
  - date-conversion
  - fortran
  - geoscience
  - ionosphere_thermosphere_mesosphere
  - julia
  - magnetosphere
  - matlab
  - python
  - solar
  - time

All eleven values were already stored for this entry before this refresh, in lowercase, and all
eleven are retained. (The public rendering title-cases keywords for display; the stored form is the
lowercase one listed above.) Every one traces to a specific upstream source, and the three sources
account for all eleven with none left over:

| Source | Keywords contributed |
|---|---|
| `setup.cfg` at the pin, `keywords =` block | `time`, `calendar` |
| GitHub repository topics | `date-conversion`, `fortran`, `geoscience`, `julia`, `matlab`, `python` |
| PyHC registry entry `keywords:` | `solar`, `magnetosphere`, `ionosphere_thermosphere_mesosphere` |

The PyHC facet `specific` is the fourth entry in that registry list and was deliberately not
recorded: it is a PyHC-internal classification marker meaning the package is narrowly scoped, not a
subject keyword, and it would be meaningless as a search term in HSSI. That omission is correct and
should not be reversed.

Keywords are the one open vocabulary in HSSI — unrecognised values are created rather than
rejected — so nothing here is constrained by an existing row list.

**Why the three PyHC facet keywords are kept even though Field 5 was cleared.** `solar`,
`magnetosphere` and `ionosphere_thermosphere_mesosphere` have no counterpart anywhere in the tracked
tree, and they are the same PyHC assertions that were removed from Field 5. Keeping them here is
deliberate and is not in tension with that removal: keywords are a free-text discovery aid with a
much lower evidential bar than a controlled Region facet. A heliophysicist searching the keyword
`magnetosphere` who finds a time library used in magnetospheric work has not been misled in the way
a Region facet would mislead, and the keywords record durably that PyHC curators judged this package
relevant to those three areas.

This is the point in the dossier most likely to look like an inconsistency and be "fixed", so it is
stated plainly: the different outcomes for Fields 5 and 16 are the intended consequence of the two
fields having different evidential bars, not an oversight. Two alternatives were considered and
rejected — dropping all three facets for surface consistency with Field 5, and dropping only `solar`
and `magnetosphere` while keeping `ionosphere_thermosphere_mesosphere`, the one facet with
repository-side support via `datetime2gtd` and `src/sciencedates/tests/test_msis.py`. Both trade a
harmless discovery aid for a symmetry the two vocabularies do not require.

The eight non-PyHC keywords were never in question: they come from the project's own `setup.cfg` and
its GitHub topics.

### 17. Data Sources (OPTIONAL)
- **Data Sources:** Not found

ScienceDates retrieves nothing. No tracked file at the pin imports `requests`, `urllib`, `ftplib`,
`http`, or any archive client, and no URL to a data service appears in any source file. The package
operates entirely on values passed to it by the caller. Empty is the correct value here, not an
unexamined gap.

### 18. Input File Formats (RECOMMENDED)
- **Input File Formats:** Not found

The package performs **no file I/O whatsoever**. No tracked Python file at the pin calls `open()`,
and none imports `h5py`, `netCDF4`, `cdflib`, `astropy.io`, `json`, `csv`, or `pathlib` for reading.
Its inputs are Python objects: `datetime.datetime`, `datetime.date`, `numpy.datetime64`, ISO-8601
strings parsed via `dateutil.parser.parse`, and plain integers and floats.

Considered and rejected: the docstring of `find_nearest` in `src/sciencedates/findnearest.py`
describes its first argument as an array of type `float, int, datetime, h5py.Dataset` within which
to search. That mention of `h5py.Dataset` is a note about which array-like objects the function
tolerates — `h5py` is imported nowhere in the tree and is not a declared dependency in `setup.cfg`.
It is not evidence of HDF5 support and must not be recorded as an input format.

### 19. Output File Formats (RECOMMENDED)
- **Output File Formats:** Not found

Same evidence as Field 18. Every exported function returns in-memory Python or NumPy values; nothing
is written to disk anywhere in the package.

### 20. Operating System (RECOMMENDED)
- **Selected Values:**
  - Linux
  - Mac
  - Operating System Independent
  - Windows

Both the general claim and the three specific platforms are supported by evidence. `setup.cfg` at
the pin carries the classifier `Operating System :: OS Independent`, which is the basis for
`Operating System Independent`. The three named platforms rest on CI rather than on assertion:
`.github/workflows/ci.yml` at the pin defines a `linux` job running on `ubuntu-latest`, and an
`integration` job whose matrix is `[windows-latest, macos-latest]`, each installing the package and
running `pytest`. All three platforms are therefore actually exercised, not merely claimed.

Listing both the general and the specific values is intentional: the specific rows make the package
findable in platform-filtered searches, while the general row records the author's own portability
claim.

### 21. CPU Architecture (RECOMMENDED)
- **Selected Values:**
  - CPU Independent

The package is pure Python with no compiled extension, no architecture-specific code path, and no
build step beyond `setuptools` — `pyproject.toml` at the pin requires only `setuptools` and `wheel`,
and `setup.py` is a three-line shim calling `setup()`. Its declared dependencies, `numpy` and
`python-dateutil`, ship wheels across architectures. Nothing in the tree constrains the CPU.

The Fortran example in `fortran/doy.f90` does not change this: it is not built, not installed, and
not part of the distribution.

### 22. Related Phenomena (OPTIONAL)
- **Related Phenomena:** Not found

Correctly empty rather than unexamined. The phenomena vocabulary consists of `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and
`X-ray emission`. A date and time conversion library models, detects, and processes none of these,
and no tracked file at the pin names any of them. There is no row that could honestly be selected,
so the empty value is the accurate one and a future refresh should not treat it as a gap to fill.

### 23. Development Status (RECOMMENDED)
- **Development Status:** Inactive

HSSI held no development-status value for this entry before this refresh. The evidence is laid out
in full here because the two leading candidate rows genuinely conflict, and because the choice
between them is a judgement a later refresh may be tempted to revisit.

*Signals of a finished, stable project.* `setup.cfg` at the pin carries the classifier
`Development Status :: 5 - Production/Stable`. The package has a long release history — a run of
releases on PyPI ending at `1.5.0`, plus the tagged `v1.5.1` — and its API has been stable across
the most recent of them. There is nothing unfinished about it.

*Signals of dormancy.* The newest commit, the newest tag, the newest GitHub release and the newest
Zenodo deposit all carry the same date, 2021-12-29 — a little under five years before this
extraction. Nothing has been pushed since.

*Signals against declaring it dead.* The repository is **not archived**, and it has **0 open
issues**. Neither is a signal of abandonment; a maintainer who had walked away would typically leave
issues open, and archiving is the explicit act by which this author's other repositories announce
end-of-life. The settled campaign policy that makes `Unsupported` the right row applies to
**archived** repositories, and explicitly does not extend to repositories that are merely quiet but
still open.

The two candidate definitions, quoted from the development-status vocabulary:
- `Inactive` — "The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows."
- `Unsupported` — "The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired."

Both presuppose the stable, usable state, which is satisfied. They differ only on whether the author
has ceased *all* work — a claim about intent that the repository does not directly evidence either
way.

**`Inactive` was chosen** because its definition matches exactly what is observable — stable,
usable, no longer actively developed — without asserting anything about the author's intent, and
because the repository being unarchived and issue-free is consistent with passive maintenance. The
cost is acknowledged: nearly five years of complete silence stretches "support/maintenance will be
provided as time allows".

Rejected, with the reasons that a future refresh should weigh before overturning them:
- `Unsupported`. Five years with no commit, no release and no issue activity is in practice hard to
  distinguish from ceased work. But this row asserts that the author has ceased *all* work, which no
  artifact states, and the settled policy that makes it the right row is keyed to archival — which
  has not happened here.
- `Active`. Supported only by the `Production/Stable` classifier in `setup.cfg`. That classifier is
  the author's claim frozen at the last release and describes release maturity, not current
  development; by the maintenance measure the vocabulary uses, `Active` is plainly false.

The durable point underneath the disagreement: `Production/Stable` is a *maturity* statement frozen
at the last release, while the vocabulary rows describe *maintenance* status. They are not answering
the same question, so the classifier cannot settle this field on its own and must not be used to
promote the entry to `Active`.

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://github.com/geospace-code/sciencedates

`README.md` is the entire documentation, and the repository URL is where a user finds it. There is
no separate documentation site: the tracked tree at the pin has no `docs/` directory, no
ReadTheDocs configuration, no Sphinx `conf.py`, and no documentation URL in `setup.cfg` or in the
GitHub repository metadata.

**There is no wiki either, despite the repository metadata suggesting otherwise.** GitHub reports
this repository as having wikis enabled, but that flag records only that the wiki *feature* is
switched on, not that a wiki exists. A wiki lives in a separate git repository, and this one has
never been created: listing the remote refs of `https://github.com/geospace-code/sciencedates.wiki.git`
exits 128 with `remote: Repository not found.`, whereas the same command against a repository that
does have a wiki (`https://github.com/numpy/numpy.wiki.git`) exits 0 and returns a `HEAD` ref. The
negative is therefore a real absence rather than a broken command. A future refresh should not chase
the enabled-wiki flag as a documentation lead.

Durable defect worth knowing about: the one usage example in `README.md` at the pin is broken. It
calls `sd.datetime2yd(T)`, but no function named `datetime2yd` exists anywhere in the tree — a
fixed-string search for that exact name across the pinned revision matches only that single README
line. The exported function is `datetime2yeardoy`. This changes no metadata value, but it means the
README's example cannot be run as written, and a future agent reading the README should take the
exported names from `src/sciencedates/__init__.py` rather than from the example.

### 25. Funder (OPTIONAL)
- **Funder:** Not found

Evidenced absence. No tracked file at the pin contains an acknowledgements section, a grant number,
or a funding agency name: `README.md` is a short description, install and usage document with no
funding text; `LICENSE.txt` is the unmodified MIT text; `setup.cfg` has no funding field. The Zenodo
record carries no grants or funding block, and there is no accompanying publication (Field 14) whose
acknowledgements could be consulted. This appears to be unfunded personal or consultancy work.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found

Same evidence as Field 25. With no funder identified anywhere, there is no award to record.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **Related Publications:** Not found

The Zenodo record's related identifiers contain exactly one entry — the `isSupplementTo` relation to
`https://github.com/geospace-code/sciencedates/tree/v1.5.1` — which is a source-code relation, not a
publication. No DOI other than the software's own concept and version DOIs appears anywhere in the
tracked tree. This is consistent with Field 14: there is no paper.

### 28. Related Datasets (OPTIONAL)
- **Related Datasets:** Not found

Same evidence as Field 27: the sole related identifier on the Zenodo record is the GitHub tag tree.
The software neither ships nor consumes a dataset — it performs no file I/O at all (Fields 18/19).

### 29. Related Software (OPTIONAL)
- **Related Software:**
  - https://github.com/space-physics/hwm93
  - https://github.com/space-physics/msise00
  - https://github.com/wavebitscientific/datetime-fortran

All three entries above were added in this refresh, and they replaced the field's previous contents
entirely: HSSI held two Field 29 entries before this refresh, `https://github.com/numpy/numpy` and
`https://github.com/dateutil/dateutil`, and both were removed. The evidence and reasoning for both
fields is set out together under Field 30 below, because the two fields' previous entries were
assembled the same way and had to be assessed as one set.

### 30. Interoperable Software (OPTIONAL)
- **Interoperable Software:** Not found

**Field 30 was emptied in this refresh. The `Not found` marker above means deliberately emptied, not
never-populated.** HSSI held four entries here before this refresh — `https://github.com/numpy/numpy`,
`https://github.com/matplotlib/matplotlib`, `https://github.com/stub42/pytz` and
`https://github.com/pydata/xarray` — and all four were removed. Counting the two Field 29 entries,
all six previously stored entries across the two fields were removed.

Both lists had been assembled from the `install_requires` and `extras_require` blocks of
`setup.cfg`, which is precisely the derivation the current field guidance rules out. The analysis
below records the assessment of every one of those six entries against that guidance, and the three
candidates the dependency-derived approach had missed, which now constitute Field 29.

**The two bars being applied**, quoted from the field reference document:

- *Rejection bar (both fields).* Field 30's Tier A list names "numpy, scipy, pandas, matplotlib,
  cartopy, seaborn, plotly, bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click,
  setuptools" among others, and states: "Being a dependency is not interoperability." For any
  package not named there, the test is: "would this package be equally at home in a web app, a
  finance model, or a biology pipeline?" The guidance also closes the relocation escape hatch
  explicitly: "The two gates are one rule — a package rejected from Field 30 is *not* thereby a
  Field 29 entry; it usually belongs in neither." Where a rejected entry goes is "usually
  **nowhere**".
- *Acceptance bar (Field 30).* A demonstrated exchange — shared or converted data models, one
  package's output imported into the other, an adapter API, or a plugin or companion relationship.
  For the Tier B set, which includes `xarray`, qualification requires that "a specific exchange is
  documented in the public API, docs, examples, or tests", and "never on dependency presence alone";
  the guidance's own contrast is that returning `xarray.Dataset` as a documented interchange format
  qualifies whereas "uses xarray internally" does not.
- *Acceptance bar (Field 29).* "Software that performs similar tasks but does not necessarily link
  together", a predecessor or fork parent, a companion, or a **domain-specific** dependency whose
  presence characterises the software.

**Verdict on each previously stored entry.**

| Entry | Sole basis in the pre-refresh record | Assessment |
|---|---|---|
| `https://github.com/numpy/numpy` (in **both** fields) | `install_requires` | Named explicitly on the Tier A line. Its use here is ordinary array handling throughout the modules. Fails the rejection bar in both fields, and the guidance forbids relocating it to Field 29. |
| `https://github.com/dateutil/dateutil` (Field 29) | `install_requires` | `python-dateutil` is named explicitly on the Tier A line. It is used only as `dateutil.parser.parse` for ISO-8601 string input in `dec.py`, `doy.py` and `tz.py`. Fails the rejection bar. |
| `https://github.com/matplotlib/matplotlib` (Field 30) | `extras_require` `plot` | Named explicitly on the Tier A line. Its only consumer is `src/sciencedates/ticks.py`, which is unexported, untested and unmentioned in the README. Fails the rejection bar. |
| `https://github.com/stub42/pytz` (Field 30) | `extras_require` `timezone` | Not named in either tier, so the web-app/finance/biology test applies: a timezone database wrapper is exactly as useful in a web app, a finance model, or a biology pipeline as it is here. It is generic infrastructure and takes Tier A treatment. Its entire use is a single `from pytz import UTC` in `src/sciencedates/tz.py`. Fails the rejection bar. |
| `https://github.com/pydata/xarray` (Field 30) | `extras_require` `plot` | **Tier B — an evidence check, not a policy removal.** The evidence at the pin is thin: xarray appears in exactly one module, `src/sciencedates/ticks.py`, where `timeticks` accepts an `xarray.DataArray` and immediately converts it to a `timedelta`. That module is not imported by `src/sciencedates/__init__.py`, is exercised by none of the three test modules, and is not mentioned in `README.md`. There is no public-API exchange, no documented interchange format, and no example. It fails the Tier B bar on evidence — but were evidence later found (an exported function accepting or returning an xarray object), it would qualify on the merits. |

**The three entries that replaced them.** Each was verified at source.

- **HWM-93** — `https://github.com/space-physics/hwm93` (38 characters). HWM-93 is a Python wrapper
  for the Horizontal Wind Model, and it is built on ScienceDates: line 4 of its `hwm93/__init__.py`
  is `from sciencedates import datetime2gtd`, and line 34 of its `setup.cfg` declares `sciencedates`
  in `install_requires`. This is a genuine relation between two heliophysics packages, not a generic
  dependency. **HWM-93's own catalogue record already listed this repository among its related
  software while ScienceDates carried no entry pointing back**, so recording it here makes the
  association reciprocal rather than creating it from nothing.
- **MSISE-00** — `https://github.com/space-physics/msise00` (40 characters). Evidenced from
  ScienceDates' *own* side at its own pin: `src/sciencedates/tests/test_msis.py` is a whole test
  module whose line 2 reads `tests for time conversions relevant to MSISE00`, and whose tests
  exercise `datetime2gtd` against the time inputs NRLMSISE-00 expects. Historically the relation ran
  both ways — at MSISE-00 commit `afbe588` (2018-07-09) line 13 of its `msise00/__init__.py` was
  `from sciencedates import datetime2gtd` — but that import is absent from MSISE-00's current
  source, which no longer depends on ScienceDates. The present-day evidence is therefore
  one-directional: a ScienceDates test module maintained specifically for MSISE-00 compatibility.
- **Datetime-Fortran** — `https://github.com/wavebitscientific/datetime-fortran` (53 characters).
  `README.md` at the pin tells the reader that for Python-like modern Fortran datetime handling they
  should see Datetime-Fortran, linking that exact URL. That is the author pointing users at a peer
  tool performing similar tasks in the language ScienceDates only demonstrates by example — the
  textbook Field 29 relation. Whether or not it has its own HSSI entry is immaterial here: Field 29
  accepts any repository URL, in-catalogue or not.

**Why HWM-93 and MSISE-00 are domain-specific rather than generic plumbing.** The function they
consume is `datetime2gtd`, defined in `src/sciencedates/doy.py`. It takes a time and a geodetic
longitude and returns a three-tuple of the day of year, the seconds elapsed since UTC midnight, and
the solar local time, the last computed as `utsec[i] / 3600.0 + glon / 15.0`. Those three quantities
are not a general-purpose time representation — they are the time arguments that the Fortran
NRLMSISE-00 `GTD7` routine expects, which is what the `gtd` in the function's name refers to. In
other words, ScienceDates carries a function whose output signature is shaped by a Fortran empirical
upper-atmosphere model's calling convention. That is what distinguishes this relation from "both
packages import numpy".

**Considered and rejected: Helio-Lite** (`https://github.com/indiajacksonphd/Helio-Lite`, itself an
entry in the HSSI catalogue). It does pin ScienceDates: line 246 of its
`libraries_dependencies/requirements.txt` reads `sciencedates==1.5.0`. But that file is a 309-line
frozen environment manifest, and ScienceDates is one line within it. Bulk environment inclusion is
not a demonstrated exchange — the same file would list any package that happened to be in the
environment, and nothing in Helio-Lite's code is documented as exchanging data with ScienceDates. It
fails both bars. This is recorded as considered-and-rejected rather than as an omission, so that a
future agent does not re-propose it on the strength of the pin.

**Why all six previously stored entries were removed.** Each failed the rejection bar on the
analysis above: every one was a bare dependency listing drawn from the generic scientific-Python
stack, and being a dependency is not interoperability. `xarray` was the one genuine evidence
question rather than a policy removal, and it failed the Tier B check because its only consumer is
`src/sciencedates/ticks.py`, which is unexported, untested and undocumented. Two alternatives were
considered and rejected: keeping `xarray` alone, on the view that `ticks.py` is shipped code and its
`DataArray` handling is a real if minor accommodation of another package's data model (rejected
because the Tier B bar asks for a documented *public* exchange, which `ticks.py` cannot supply); and
keeping some subset of the Tier A entries, for which no argument from the guidance exists — recorded
here only so the option is visibly foreclosed rather than silently so. A future refresh should not
restore any of the six from `setup.cfg`: a package rejected from Field 30 does not thereby become a
Field 29 entry, and the usual correct destination for such a package is neither field.

One durable mechanical note about that removal: `numpy` occupied the **same** related-item record in
both fields, so it appeared twice in the pre-refresh record but is a single entity. Removing it from
one field does not remove it from the other.

**Why HWM-93 and MSISE-00 are recorded in Field 29 rather than Field 30.** From ScienceDates' side
these are *dependents*: they consume `datetime2gtd`, which is a characterising domain relation
rather than an interoperation this package advertises. The placement is also symmetric with how
HWM-93's own catalogue record already files ScienceDates. Field 30 was considered on the ground that
HWM-93 importing ScienceDates' output is a demonstrated exchange in the guidance's own sense, and
listing both fields was considered because the relation genuinely has both characters; the latter
was rejected because duplicating one entity across both fields is precisely what produced the
`numpy` situation described above. On MSISE-00 specifically, the present-day evidence is
one-directional — a ScienceDates test module maintained for it — because MSISE-00 dropped its
`sciencedates` import years ago; a maintained compatibility test module was judged sufficient to
assert a current relation.

**Why Datetime-Fortran is recorded in Field 29.** `README.md` at the pin explicitly recommends it as
the modern-Fortran counterpart, which is the definition of similar-task software. The
counter-argument was weighed: it is a Fortran library, whereas ScienceDates' Fortran content is a
single example file, so the "similar tasks" claim rests on the example directory rather than on the
installable package. The author's own pointer at a peer tool was judged the stronger evidence.

Convention followed for all three entries: another HSSI entry is named by that entry's own stored
code repository URL, because the page renders a related item's raw URL as its link text. That is why
these are recorded as `https://github.com/space-physics/hwm93` and
`https://github.com/space-physics/msise00` rather than as display names or DOIs. Whether or not
Datetime-Fortran has its own HSSI entry is immaterial — Field 29 accepts any repository URL,
in-catalogue or not — and while it has none, its entry renders as a plain external URL. All three
URLs are well within the 128-character limit that applies when a new related-item record is
created: they are 38, 40 and 53 characters.

### 31. Related Instruments (OPTIONAL)
- **Related Instruments:** Not found

Evidenced absence, and the search is recorded here so that it need not be guessed at again. A
case-insensitive PCRE search (`git grep -P -in`) over every tracked file at the pin for the pattern

```
msis|radar|observator|satellite|magnetomet|instrument|dmsp|themis|eiscat|arecibo
```

returns exactly one match in the entire repository (shown here without the revision prefix that
`git grep` prepends to each line):

```
src/sciencedates/tests/test_msis.py:2:tests for time conversions relevant to MSISE00
```

That match is the substring `MSIS` inside `MSISE00`, which is the NRLMSISE-00 **empirical
atmospheric model** — not an instrument and not an observatory. It belongs in Fields 29/30 as a
software relation, where it is discussed, and nowhere here.

A kind-widened second pass over the same tree, again case-insensitive PCRE, for

```
spacecraft|mission|telescope|sounder|ionosonde|lidar|imager|photometer|interferomet|antenna|payload|orbiter|probe
```

returns only two lines, both in `LICENSE.txt` (lines 5 and 12), where the alternative `mission`
matches inside the words `Permission` and `permission` of the standard MIT text. There is no
instrument or observatory reference of any kind in this repository.

Use `git grep -P` rather than `-E` for patterns like these: `-E` handles `\b` incorrectly and can
return a silent empty result that looks like a genuine negative.

Confirming from the vocabulary side: a case-insensitive substring search of the
instrument/observatory vocabulary for `MSIS` returns no rows, and for `sciencedates` no rows, while
the control term `geospace` does return rows — so the searches themselves work and the negatives are
real. Every row in that vocabulary carries a `https://spase-metadata.org/` identifier, with none
failing that guard.

ScienceDates is instrument- and observatory-agnostic. Empty is the correct outcome, not a gap.

### 32. Related Observatories (OPTIONAL)
- **Related Observatories:** Not found

Same searches and same result as Field 31 — the two patterns above cover observatory, mission and
platform vocabulary as well as instrument vocabulary, and neither produced a single genuine hit. No
observatory, mission or spacecraft is named anywhere in the tracked tree.

### 33. Logo (OPTIONAL)
- **Logo:** Not found

Listing every tracked path at the pin (`git ls-tree -r --name-only <pin>`) and matching against
`\.(png|jpg|jpeg|svg|gif|ico|webp)$` returns nothing: there is no image file of any kind in the
repository. `README.md` at the pin embeds four images, and all four are external status badges — a
Zenodo DOI badge, an LGTM code-quality badge, a GitHub Actions build badge, and a PyPI
download-count badge. A build-status or DOI badge is not a logo and must not be recorded as one.

The PyHC registry entry for ScienceDates has no `logo:` key. Neighbouring entries in the same
registry file do carry one — the THEMISasi entry a few lines below it, for instance — so the key's
absence here is a real absence specific to this package, not a registry-wide omission.

A documented absence is the correct outcome. No logo should be invented for this entry.
