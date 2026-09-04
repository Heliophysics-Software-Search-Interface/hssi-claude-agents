# HSSI Metadata Extraction Results

**HSSI Software ID:** b26b964d-c772-4fe5-893e-74bd9148806a
**Repository:** https://github.com/space-physics/iri90
**Source Revision:** f5c6c898dc4ccb1c26ae086385f8e47f08ba2915
**Extraction Date:** 2026-09-02
**Validation Date:** 2026-09-03
**Validation Status:** PASS

---

## Scope note — read the evidence as final, not provisional

**The GitHub repository is archived.** The GitHub API reports `archived: true`, `fork: false`, default
branch `main`, and a last push of 2021-10-11. An archived GitHub repository is read-only: it accepts
no issues and no pull requests. The pinned revision above is therefore the software's final state,
not a snapshot of a moving target. Two consequences run through the whole dossier:

- There will be no future release, so "current" values here are terminal rather than provisional. A
  later refresh should expect the repository side of this record to be stable and should treat any
  apparent change as suspicious.
- Judgements that would normally be deferred ("this may change") can be settled now.

A second framing point applies throughout: **the repository vendors a large body of third-party
Fortran.** In broad terms, evidence found under `src/` and `reference/` describes the *underlying IRI
model*, while evidence in `iri90/`, `README.md`, `setup.cfg`, `setup.py` and the two example scripts
describes *this Python package*. Several fields below turn on that distinction, and conflating the two
is the most likely way to get this entry wrong.

The split is real but it is not clean, and a future agent should not treat it as a rule.
`.gitattributes` at the pin marks the two directories wholesale with `src/* linguist-vendored` and
`reference/* linguist-vendored`, yet `src/` also contains `src/iri90_driver.f90`, which is Hirsch's
own file — first added 2019-10-07 in commit `8e261445cddc5bbe29daef17f17523cfbdd25e64`
("no preprocessor, add meson"), over a year after the bulk vendored import. So the marking is
directory-level evidence of *predominant* provenance, not a per-file authorship attestation.

Nor can version control repair the gap, and this is worth stating because it is the next check anyone
would reach for: the first-add author of all 15 Fortran sources at the pin is Hirsch, vendored files
included, because he is the one who imported them. Commit authorship cannot separate vendored from
first-party material in this repository. Per-file content comparison can, and does — see Field 29's
byte-level match between `reference/original_iri90.f` and the live upstream file.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Source:** Placeholder. This is the catalogue convention for a record whose submitter is supplied at
submission time rather than extracted from the repository.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.1186962

**Source:** Zenodo concept DOI (`conceptrecid` 1186962). Field 2's definition names exactly this form
as the preferred one — "the concept DOI for all versions" — and adds that entering a concept DOI is
what enables automatic population of metadata from that DOI.

**Why the concept DOI rather than the version DOI.** The deposit has exactly one version record,
`10.5281/zenodo.1186963`, titled `scivision/pyiri90: altitude and time profiles`, version `v1.1.0`,
published 2018-03-02, whose sole creator is `Michael Hirsch, Ph.D.` (affiliation null). Querying the
concept with `all_versions=true` returns that one version and nothing else, which is why both DOIs
resolve to the same landing page as of this refresh. The version DOI was considered and rejected on two
grounds: it pins v1.1.0 while the version this record carries is v1.1.1 (Field 12), and Field 2
prefers the concept form precisely so that the identifier survives further releases. The concept DOI
remains correct even though, for this archived project, no further release will happen.

**How the deposit was tied to this software.** The deposit's `related_identifiers` carries
`isSupplementTo` pointing at `https://github.com/scivision/pyiri90/tree/v1.1.0`. The GitHub API
answers "Moved Permanently" for both `scivision/pyiri90` and `scivision/iri90`, and both redirect to
`space-physics/iri90` — the repository in Field 3. The deposit is this software under its two former
names.

**Negative research — do not re-hunt for a second DOI.** Zenodo free-text searches for `iri90` and
for `pyiri90`, and creator-keyed searches on `Michael Hirsch, Ph.D.` and on `Hirsch, Michael`,
surfaced no other deposit for this software. The free-text `iri90` search also returns unrelated
`glowpython` records, which is the control showing the query was genuinely matching rather than
silently returning nothing. Searching by repository name alone would not have been sufficient
evidence on its own, since a manually created deposit need not carry the repository name; the
creator-keyed searches are what make the negative result meaningful.

**Prior state.** HSSI held no persistent identifier for this software before this refresh, and the
preceding dossier recorded "Not found". That was an extraction gap, not a considered judgement — the
deposit predates the earlier extraction by years.

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/iri90

**Source:** The repository itself; also `setup.cfg`'s `url` at the pin, and the PyHC registry's
`code:` field for the `IRI-90` entry.

**Repository history worth knowing.** The project has lived at three GitHub paths:
`scivision/pyiri90` → `scivision/iri90` → `space-physics/iri90`. Both older paths still redirect to
the current one, which is how the Zenodo deposit (Field 2) and the PyPI `home_page` (Field 12) — both
of which name older paths — were tied to this record. `space-physics/iri90` is the current and final
location; see Field 23 for why this history does *not* make the record `Moved`.

### 4. Software Functionality (RECOMMENDED)
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Models and Simulations
- Models and Simulations: Empirical

**Written in fully-qualified `Parent: Child` form deliberately.** Some child names in this vocabulary
sit under more than one parent — `Analysis` is a child of both `Data Processing and Analysis` and
`Mission-related`, and `Processing` likewise — so a bare child name is ambiguous and a future agent
must not shorten these. Every child listed here has its parent listed alongside it, so the selection
has no structural gap.

**Evidence per value.**

- *Models and Simulations* / *Models and Simulations: Empirical* — IRI-90 is an empirical
  climatology. The model is driven entirely by tabulated coefficients: 24 CCIR/URSI ASCII coefficient
  files ship under `iri90/data/`, and the Fortran interpolates them for the requested date, time and
  location. Nothing is solved from first principles.
- *Data Processing and Analysis* / *Data Processing and Analysis: Analysis* — `runiri()` in
  `iri90/__init__.py` does real post-processing on the Fortran output rather than returning it raw: it
  converts the model's ion percentages into number densities by multiplying by the electron density
  and dividing by 100, and masks non-positive values to NaN because the Fortran signals "undefined"
  with a negative number. `timeprofile()` assembles repeated model evaluations into a
  time × altitude × species cube.
- *Data Visualization* / *Data Visualization: Line Plots* — `iri90/plots.py` provides `plotalt()` and
  `plottime()`. `plotalt()` draws density-vs-altitude curves on a log x-axis and temperature-vs-altitude
  curves on a linked panel; `plottime()` draws density-vs-time curves and overlays sunrise/sunset
  fiducials. Both are user-facing entry points, invoked by the two shipped example scripts.
- *Data Visualization: 2D Graphics* — this is the broader static-two-dimensional-figure category that
  the shipped multi-panel altitude-profile figure falls under; `.github/demoiri.png` is that figure.
  Of the two visualization children, `Line Plots` carries the more precise evidence, and this value is
  retained as the more general companion rather than on separate distinct evidence. Recorded here at
  its true weight so a later agent neither over-reads it nor removes it as unsupported.

**Categories examined against the full 83-row vocabulary and deliberately not selected.** Each of
these has a plausible-looking hook, which is why the reasons are recorded rather than left implicit:

- *Models and Simulations: Physics-Based*, *: First Principles*, *: Theory*, *: MHD* — all rejected
  for the same reason: the model is a fit to observations distributed as coefficient tables, not a
  solved physical system. Selecting any of these would misdescribe what a user gets.
- *Models and Simulations: Forecasting* — rejected. The model returns monthly mean values for
  magnetically quiet conditions. It does not predict a future state, and a visitor filtering HSSI for
  forecasting tools would be poorly served by a climatology.
- *Coordinate Transforms: Ionospheric* — rejected, and this is the closest call. The vendored Fortran
  does contain magnetic-dip/modified-dip machinery internally, and the underlying subroutine accepts a
  `JMAG` flag selecting geodetic or geomagnetic input coordinates. But the Python wrapper hardcodes
  `jmag = 0  # coordinates are: 0:geographic 1: magnetic` and its only coordinate manipulation is
  wrapping longitude with `glon % 360.0`. No coordinate transform is exposed through the public API,
  so under the "provides to users" test this does not apply. A future agent reading the Fortran alone
  could easily reach the opposite conclusion; the wrapper is what determines the answer.
- *Data Processing and Analysis: Time Series Analysis* — rejected. `timeprofile()` *generates* a time
  series by evaluating the model repeatedly; it performs no temporal analysis of one.
- *Data Processing and Analysis: Data Access and Retrieval* — rejected. The package reads only the
  coefficient files it bundles. It fetches nothing remote. See also Field 17.

### 5. Related Region (RECOMMENDED)
- Earth Atmosphere
- Earth Ionosphere
- Earth Thermosphere

**The Region vocabulary is flat.** Its 24 rows have no working parent/child relationships, so a coarse
value never implies a fine one and a fine value never implies a coarse one. Two consequences a future
agent must respect: each of the three values below needs, and has, its own independent evidence; and
no argument of the form "Earth Atmosphere already encompasses the ionosphere" or "the ionosphere
implies the thermosphere" is valid here. Such an argument is itself a defect, not a simplification.

- **Earth Ionosphere** — the model's subject. `README.md`'s heading is
  `# IRI90: International reference ionosphere in Python`, the model's outputs are ionospheric
  (electron density, ion and electron temperatures, ion composition), and `ionosphere` is both a
  GitHub topic and a `setup.cfg` keyword.
- **Earth Thermosphere** — evidenced independently. `src/iri90.f` computes neutral temperature via a
  routine documented as using the `C   MSIS-86/CIRA 1986 Neutral Thermosphere Model. The subroutines`,
  and `Tn` is one of the nine quantities the public API returns. `thermosphere` is also a `setup.cfg`
  keyword and a stored HSSI keyword (Field 16).
- **Earth Atmosphere** — retained on its own footing. The model's documented range spans 50 km to
  2000 km, which is an atmospheric-envelope claim rather than a purely ionospheric one, and the coarse
  row is not made redundant by the two finer rows in a flat vocabulary.

**The field doc's instruction that drove the expansion.** Field 5 directs a chooser to prefer the
`most specific applicable region (e.g. `Earth Ionosphere` over `Earth Atmosphere`) rather than`
defaulting to the older five-value list. The record previously carried only `Earth Atmosphere`, which
was the correct choice against the vocabulary as it then stood; the two specific rows became available
when the vocabulary grew to its present 24.

**Rejected candidate — `Earth Auroral Subregion`.** There is a real case for it, and it is recorded so
the next refresh does not mistake its absence for an oversight. In favour: `README.md` states that
IRI90 `is often used as an initialization for conditions at` auroral latitudes, `understanding the
caveats`; both shipped examples default to 65°N (`AltitudeProfile.py` `default=(65, -147.5)`,
`TimeProfile.py` `default=(65, -148)`); and the repository's own demo figure is titled for
`(65, -147.5)`. Against it, decisively: the model's stated validity is *non-auroral* latitudes. A
visitor filtering HSSI for auroral-region software would be handed a model that documents itself as
invalid there — which is worse than not returning it. The catalogue deliberately declines to mirror
the README on this point.

**Rejected candidate — `Earth Lower and Middle Atmosphere`.** Also a real hook: the model's stated
floor of 50 km lies in the mesosphere, so the bottom of its range overlaps the middle atmosphere.
Rejected because everything the repository actually exercises sits at or above 85 km —
`AltitudeProfile.py` defaults `--alt` to `default=(85, 500, 1.0)`, `TimeProfile.py` to
`default=(120, 180, 20)`, and `iri90/tests/test_all.py` uses `altkm = np.arange(90, 500, 5)`. The
mesospheric overlap is the unexercised bottom of a range spanning nearly 2000 km, and the model's
subject is the ionosphere. Someone filtering for lower- and middle-atmosphere software would not
expect an ionospheric climatology back.

### 6. Authors (MANDATORY)
- **Author:** Michael Hirsch
  - **Author Identifier:** https://orcid.org/0000-0002-1637-6526
  - **Affiliation:**
    - **Organization:** Boston University
      - **Affiliation Identifier:** https://ror.org/05qwgg493
    - **Organization:** Scivision, Inc.
      - **Affiliation Identifier:** Not found

**Source:** `setup.cfg` at the pin declares `author = Michael Hirsch, Ph.D.`; `LICENSE.txt` carries
`Copyright (c) 2015 Michael Hirsch`; the Zenodo deposit's sole creator is `Michael Hirsch, Ph.D.`; the
PyHC registry lists `contact: Michael Hirsch`. The name is recorded without the credential suffix, the
catalogue's convention for personal names. `https://ror.org/05qwgg493` resolves to Boston University.
`Scivision, Inc.` carries no organizational identifier. This is negative research rather than an
unchecked gap, and it is recorded so the wrong identifier is not attached later: a ROR search for
"Scivision" returns a single organization, `https://ror.org/011qev639` — "SciVision Biotech Inc.
(Taiwan)" — which is an unrelated company. That ROR must not be used here.

**Stan Solomon was considered as an author and rejected.** This is among the most likely
re-proposals a future agent could make, because his name is prominent in the source tree, so the
reasoning is recorded in full and strongest evidence first.

**1. Direct, per-file provenance — the decisive evidence.** `reference/original_iri90.f` at the pin is
identical to the file the live upstream source at `http://download.hao.ucar.edu/pub/stans/iri/iri90.f`
serves as of this refresh, once trailing whitespace is stripped from both (both 2979 lines; 828 raw
differing lines, every one trailing-whitespace only). That is a verifiable byte-level fact
establishing that the model code originates outside this project, independent of any marking or
metadata claim.
`src/iri90.f` is a modernised derivative of that same file.

**2. What the in-code credits actually say.** A case-insensitive search for `solomon` across the tree
at the pin returns eight lines. Five credit Stan Solomon: `reference/original_iri90.f:3`,
`src/iri90.f:3` and `src/iri90_solomon.f:6` each read
`C Adapted 7/93 from 10/91 version of IRIS12 by Stan Solomon.`, and
`reference/original_iri90.f:1015` and `src/iri90_solomon.f:1030` each read
`C Subroutine DFP, Stan Solomon, 3/92, splices filename to directory`. Read them for what they claim:
they credit him as the origin of the *adapted model*, not as a developer of this Python package.

**3. Two of those eight lines are a different Solomon, and must not be counted with the rest.**
`src/iriflip.for:1765` reads `C---- Calculate hv + NO ion. freq. from Lyman-a (Brasseur & Solomon)`
and `src/iriflip.for:1769` reads
`C---- LY_a=2.5E11 (Lean), sigi(NO)=2.0E-18 (Brasseur & Solomon page 329)`. "Brasseur & Solomon" is a
page-numbered citation to the aeronomy textbook by Guy Brasseur and Susan Solomon — a literature
reference to a different person, and not an authorship claim of any kind. A sentence of the form
"eight Solomon references, all crediting Stan Solomon" would be wrong on both halves.

**4. The one first-party mention.** `iri90/__init__.py:65` reads
`    JF = np.array((1, 1, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1), bool)  # Solomon 1993 version of IRI`. It sits
in the Python package itself, outside the vendored directories, so it is accounted for explicitly
rather than swept under a directory rule: the comment names *which variant of the model* the
option-flag array selects. That is model provenance, not a developer credit.

**5. Corroborating, stated with its limit.** The author marks `src/*` and `reference/*`
`linguist-vendored` in `.gitattributes`. That is directory-level evidence of predominant provenance
and nothing more — the same rule also covers `src/iri90_driver.f90`, which Hirsch wrote himself. It
must not be presented as a per-file attestation, and it is not what carries this argument.

**6. The software-metadata sources for the package name only Hirsch** — `LICENSE.txt`,
`setup.cfg`'s `author`, the Zenodo deposit's sole creator, and the PyHC registry contact. Commit
authorship adds nothing either way here: Hirsch is the committing author of the whole tree, vendored
files included, because he imported them.

The upstream provenance is not lost by this decision: it is carried by the Field 29 link to the HAO
source file and by this rationale.

### 7. Software Name (MANDATORY)
IRI-90

**Source:** The PyHC registry entry, whose `name:` is exactly `IRI-90`. This is the curated form and
is authoritative for this workflow.

**Alternative forms encountered, and why they were not used.** `iri90` is the package and PyPI
distribution name (lower-case, no separator) — a distribution identifier rather than a display name.
`IRI90` is the form used inside `README.md` and the code comments. `IRI90: International reference
ionosphere in Python` is the README's H1 heading — a title line, not a name. The hyphenated `IRI-90`
matches how the international model is written in the literature and is the form a searcher is most
likely to type.

### 8. Description (MANDATORY)
IRI-90 from Python, clean and flexible ionospheric model. IRI-90 provides monthly mean values for magnetically quiet conditions at non-auroral latitudes in the altitude range 50km to 2000km. However, IRI-90 is often used as an initialization for conditions at auroral latitudes, understanding the caveats. This IRI-90 Python module is as small and clean as possible to enable custom IRI-90 applications. The module outputs electron density, neutral temperature, ion temperature, electron temperature, and ion composition (O+, H+, He+, O2+, NO+) as an xarray.DataArray indexable by species, altitude, etc. and includes metadata.

**Source and its exact relationship to the repository.** This is an *adapted* composite of `setup.cfg`
and `README.md`, not a quotation of either, and a future agent comparing it to the sources should
expect the following deliberate normalizations rather than treat them as drift:

- The opening sentence follows `setup.cfg`'s
  `description = IRI90 from Python, clean and flexible ionospheric model.` with `IRI90` normalized to
  the Field 7 name form `IRI-90`.
- The second and third sentences follow `README.md`'s opening blockquote and the sentence beneath it,
  with the README's markdown emphasis removed, its line wrapping joined, and `IRI90` again normalized.
- The fourth sentence follows the README's usage line with `your custom IRI90 applications` reduced to
  `custom IRI-90 applications`.
- The species list is the nine quantities the API actually returns, which
  `iri90/__init__.py` declares as
  `simout = ["ne", "Tn", "Ti", "Te", "nO+", "nH+", "nHe+", "nO2+", "nNO+"]`.
- The closing clause follows the README's statement that
  `` `iono` is an xarray.DataArray indexable by species, altitude, etc. and includes metadata. ``

The wording is the existing curated description and is retained as editorial intent. It is accurate
against the pin and no factual correction was warranted.

### 9. Concise Description (OPTIONAL)
IRI-90 is an international reference ionosphere model in Python providing monthly mean ionospheric parameters from 50km to 2000km altitude.

**Source:** Derived from the GitHub repository description
(`IRI90-international reference ionosphere in Python`) and the README's stated altitude range, held
to roughly 200 characters. Retained as editorial intent; it is accurate against the pin.

### 10. Publication Date (RECOMMENDED)
2015-04-28

**Source:** The first commit on the pinned lineage, `61ac00b1bbbc89ed6b8f55e67c0804536657fe47`,
authored 2015-04-28 04:28:56 -0400. Independently corroborated by the GitHub API's repository
`created_at` of 2015-04-28T08:28:56Z — the same instant expressed in UTC.

**Method note that matters for this repository.** The date was derived by walking the pinned revision
(`git log <pin> --reverse`), never `git log --all`. Repositories in this family can carry tags on
pre-rewrite orphan lineages, so an all-refs walk can surface commits that are not ancestors of the pin
and produce a "correction" that is wrong. Both tags in this repository were confirmed to be genuine
ancestors of the pin with `git merge-base --is-ancestor` rather than assumed.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source and rule applied.** Field 11 states: `For software where a DOI has been obtained through
Zenodo (e.g., GitHub-Zenodo workflow), Zenodo is the correct entry. If no DOI has been obtained,
indicate the repository host, such as GitHub or GitLab.` A DOI was obtained through Zenodo (Field 2),
so Zenodo is the entry.

**Two independent fingerprints that the deposit came from the GitHub–Zenodo integration**, rather than
being a manual upload that merely happens to be about this software:

1. The deposit's `related_identifiers` carries `isSupplementTo` pointing at a `tree/v1.1.0` URL under
   the repository. That relation and URL shape is what the integration writes; a manual deposit has no
   reason to contain it.
2. The deposit is a mechanical copy of a GitHub release. Its title, `scivision/pyiri90: altitude and
   time profiles`, is `<owner>/<repo>: <release name>` — and the GitHub release on tag `v1.1.0` is
   indeed named `altitude and time profiles`. Its description is that release's body: the release body
   reads "Improving robustness and versatility of IRI90 interface, while maintaining simplicity." and
   "xarray.DataArray contains all the metadata for easy API and plotting, etc.", and the Zenodo
   description is exactly those two sentences wrapped in HTML paragraphs.

**Previous value and why it was wrong.** The record previously named GitHub, and the preceding dossier
justified it with the premise that no DOI had been obtained through Zenodo or any other publisher.
That premise was false — the deposit predates that extraction — so the value failed the second half of
Field 11's rule rather than the first. Recording the falsified premise, not just the changed value,
is the point: the error was an unfound DOI, not a misreading of the publisher rule.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.1.1
- **Version Date:** 2018-08-15
- **Version Description:** Modernization release including documentation improvements, CI template updates, badge updates, and cleanup. No detailed v1.1.1 release notes are provided in the GitHub release.
- **Version PID:** Not found

**Source.** Tag `v1.1.1` is `776b0190cd19f2a2015f76c92094016eff16986a`, committed 2018-08-15
02:02:55 -0400, and is an ancestor of the pin (confirmed with `git merge-base --is-ancestor`, not
assumed). `setup.cfg` at the pin declares `version = 1.1.1`. The GitHub release on that tag is named
`modernization` and its body is empty, which is precisely why the description above characterizes the
release rather than quoting notes: there are none to quote. The repository carries two tags, `v1.1.0`
(2018-03-02) and `v1.1.1`, matching its two GitHub releases.

**A GitHub release carries two separately authored fields, `name` and `body`, and both were checked.**
The distinction is load-bearing rather than pedantic, because the attribution argument below depends
on it: the description's opening word traces to the release *name*, which is `modernization`, while
the *body* is empty. An agent that fetches only `body` sees nothing and would wrongly conclude the
description is unattributable. That is a demonstrated failure mode, not a hypothetical.

**The stored description was tested for misattribution and is sound — do not re-investigate it.** A
characterization with no release notes behind it invites the suspicion that it was inherited from the
previous release. It was not: `v1.1.0`'s release body is about entirely different content —
robustness, versatility and `xarray.DataArray`, quoted in full under Field 11 — so the description
reproduces nothing from it. Every element of the first sentence instead maps to a commit subject
inside the release range `v1.1.0..v1.1.1`: "Modernization" to the release name `modernization` and to
a `modernize` commit; "documentation improvements" to four `doc [ci skip]` commits; "CI template
updates" to `CI tempalte` (the typo is in the original commit subject) and the AppVeyor work
(`init appveyor`, two `Update .appveyor.yml`); "badge updates" to `badges` and `badge`; "cleanup" to
`cleanup [ci skip]` and `cleanup`. The description is therefore synthesized from the release's own
commit subjects, not inherited from another release — a sound stored value rather than a defect.

**Test that against the release range, not the range that follows it.** `v1.1.0..v1.1.1` is 23
commits and is the correct range here; `v1.1.1..<pin>` is the 19 commits discussed next, which run
from the tag to the archived final state. The four `doc [ci skip]` commits, the `badges` and `badge`
commits, the AppVeyor commits and `modernize` occur only in the release range and not once in the
later one, so running the attribution test against the later range produces a false negative. Note
the one term that would not reveal the mistake: `cleanup` occurs in both ranges, so testing on it
alone succeeds against either and proves nothing.

**The pin is 19 commits later than the release tag** (`git rev-list --count v1.1.1..<pin>`), so the
archived final state of the repository post-dates its last release. This is *not* a
"version declared but never released" case: `setup.cfg` at the pin still declares 1.1.1, so no
unreleased bump happened. The 19 commits are build-system and CI work — among other things, the
meson build, the root `CMakeLists.txt`, `src/iri90_driver.f90` and the GitHub Actions workflow all
arrive after the tag, and the Travis/AppVeyor configs are moved into `archive/`.

**PyPI corroboration and identity.** PyPI carries `iri90` 1.1.1 as its sole release, an sdist uploaded
2018-08-15T06:04:10Z — roughly a minute after the tag (02:02:55 -0400 = 06:02:55Z) and about
forty-five seconds after the GitHub release (06:03:25Z). Identity was closed through the distribution's
`home_page`, `https://github.com/scivision/iri90`, which redirects to the repository. `pyiri90`,
`iri-90` and `iri_90` are all absent from PyPI. Only the JSON/Simple API is authoritative for that
kind of negative check — the HTML project page answers 200 even for names that do not exist.

**Packaging drifted between the tag and the pin**, which explains an apparent inconsistency a future
agent will otherwise trip over. At the tag, `setup.cfg` declared `python_requires = >= 3.6`, and its
licence key was the singular `license_file = LICENSE`, with its value inline on the same line; at the
pin it declares `python_requires = >= 3.7`, and its licence key has become the plural
`license_files`, written as a key on its own line with `LICENSE.txt` indented beneath it. PyPI still
advertises `>= 3.6` because the sdist was built from the tag.
Field 13's `Python 3.x` covers both, so nothing needs reconciling in the metadata.

**Version PID is empty deliberately — do not "fill the gap".** The only Zenodo version record is for
v1.1.0 (Field 2), and the version recorded here is v1.1.1. Attaching `10.5281/zenodo.1186963` to a
v1.1.1 row would assert a DOI for a release that has none. Because the repository is archived, no
v1.1.1 deposit will ever appear; this field is permanently and correctly empty.

### 13. Programming Language (RECOMMENDED)
- Fortran77
- Fortran90
- Fortran 2003
- Fortran 2008
- Python 3.x

**The criterion: this field records each language edition for which a construct introduced by that
edition is present in the code — not the minimum standard any file requires.** Every inclusion and
exclusion below follows from that single rule, and a future refresh should apply it rather than
invent a fresh basis. It is also why the list is longer than a conformance summary would be: no file
here *requires* Fortran 2008 as a minimum, and none requires Fortran77 specifically either. The
CMake and Meson builds reach for the GNU legacy flag rather than any numbered standard —
`add_compile_options(-std=legacy)` at `CMakeLists.txt:6` under a GNU-compiler guard and
`old = '-std=legacy'` at `meson.build:6` for `gcc` (Field 21 records the flags) — because
`src/iri90.f`, the single source of the Python extension, conforms to no numbered edition at all. A
reader who takes this field as a conformance claim will object that the build passes `-std=legacy`;
it is not that claim.

Each value, with the construct that admits it:

- **Fortran77** — fixed source form throughout the vendored library (eleven `.for` files under
  `src/`), including DO terminations so old that Fortran 2018 *deleted* them: `src/irisub.for:368`
  opens `do 7397 kk=1,nummax` and `:369` terminates it on the labelled statement
  `7397    OUTF(KI,kk)=-1.`, which gfortran 14.1.0 reports at `-std=f2018` as
  "Fortran 2018 deleted feature: Shared DO termination label 7397".
- **Fortran90** — attribute-form type declarations with `INTENT` at `src/irisub.for:329-330`
  (`Real,intent(inout):: OARR(100)` and `Real,intent(out)  :: OUTF(20,1000)`) and the parenthesised
  length form `CHARACTER(12)  FILNAM` at `:325`; plus the block `DO WHILE (TABM(MON).GT.IDAY)` at
  `src/iridreg.for:129`, closed by `END DO` at `:131`. Both files are compiled into the Fortran
  library (`src/CMakeLists.txt:1`, `src/meson.build:1`), and both are accepted at `-std=f95` with
  exit 0 and no errors, so their content needs nothing later than F90. `-std=f95` does emit
  obsolescent-feature warnings against `src/irisub.for` for its F77-era DO terminations — the same
  mixture of eras this field records as separate dialects.
- **Fortran 2003** — `use, intrinsic:: iso_fortran_env, only: error_unit, output_unit` at
  `src/iri90.f:161`, and deferred-length `character(:), allocatable :: datadir` at
  `src/iri90_driver.f90:16`. That free-form driver is the one source in the tree that genuinely
  requires F2003 as a minimum.
- **Fortran 2008** — the single bare `error stop` at `src/iri90.f:435`, deliberate per the author's
  comment at `:434`: `! must be "error stop" so Travis-CI tests, etc. fail when this fails.`
- **Python 3.x** — `python_requires = >= 3.7` at `setup.cfg:22` (`>= 3.6` at the release tag); the
  package under `iri90/` is Python 3 throughout, with type annotations.

**`Fortran 2023` is excluded** by the same criterion: it is the next vocabulary rung above
`Fortran 2008`, and no construct in the tree reaches it. `do concurrent`, `submodule`, `contiguous`,
coarray syntax, `findloc` and `newunit` are all absent, and the `G0` occurrences in the vendored code
are a variable and a statement function rather than the F2008 `g0` edit descriptor. That negative
research is what bounds this list at the top.

**`Fortran 2018` is excluded** twice over: it has no row in this vocabulary (the Fortran rungs are
`Fortran77`, `Fortran90`, `Fortran 2003`, `Fortran 2008` and `Fortran 2023`), so it is not selectable
at all; and the only F2018-related signal in the tree is a feature F2018 deleted, which is F77-era
content rather than F2018 content.

**Two falsified justifications, retired here — do not restore either.** (1) "The highest standard
required" was wrong in both directions: nothing in this tree requires Fortran 2008, and the framing
would drop F90 constructs that are plainly present. (2) "`Fortran 2003` already covers everything
`Fortran90` would" rested on `src/iri90_driver.f90` being the only F90-era source; the two vendored
fixed-form files above disprove it. `Fortran90`'s standing was the last open question in this field,
and the criterion settles it: the constructs are present, so the value is recorded. Before this
refresh the HSSI record carried only `Fortran77` and `Python 3.x`, so the later dialects are
additions here rather than corrections.

One trap, because it would otherwise inflate the Fortran 2008 evidence from one construct to seven:
compiling `src/iri90.f` under a numbered standard also emits six
`Error: Fortran 2008: Pointer procedure assignment` diagnostics between lines 1795 and 1805, but
those lines are ordinary array assignments whose arrays are declared with the nonstandard `REAL*8` at
`src/iri90.f:1791` — gfortran discards that declaration and re-reads the assignments as pointer
function results; substituting the standard `DOUBLE PRECISION` makes them vanish.

The list is re-derivable with one invocation per file: `gfortran -std=<edition> -c` over the Fortran
sources under `src/` at each rung, with `-std=f95`'s outright rejection of `src/iri90.f` as the
control that a clean pass elsewhere is a real result rather than an inert check.

**Rejected: Meson and CMake as "languages."** An earlier automated extraction reported them among
this project's languages; they are build systems, absent from the controlled vocabulary, and are
noted only so the suggestion is not revived.

### 14. Reference Publication (OPTIONAL)
Not found

**Source — negative research, deliberately recorded.** There is no `CITATION.cff`, `codemeta.json` or
`.zenodo.json` anywhere in the tree at the pin, and `README.md`'s References section contains a single
link, to the upstream Fortran source. Literature searches through ADS/SciX found no publication
describing *this Python package*: `full:"pyiri90"`, `full:"github.com/space-physics/iri90"`,
`full:"scivision/pyiri90"` and `author:"Hirsch, M" full:"IRI90"` each returned nothing. Those queries
were controlled against a deliberately invalid credential, which was rejected outright rather than
answering with an empty result set — so the zero hits are genuine absence rather than a query failing
silently.

**The trap this field sets.** IRI-90 has a substantial literature, and a future agent searching for
"IRI-90" will find plenty. Those papers describe the *international model*, not this Python wrapper of
Stan Solomon's 1993 adaptation of it. Recording one of them here would attribute someone else's work
to this software entry. The empty value is a considered outcome, not a gap.

### 15. License (RECOMMENDED)
MIT License

**Source:** `LICENSE.txt` at the pin opens `The MIT License (MIT)` and carries
`Copyright (c) 2015 Michael Hirsch`; `setup.cfg` points at it via `license_files`; GitHub reports SPDX
`MIT`. `MIT License` is the exact spelling of the vocabulary row, which matters because the value is
resolved by exact (case-insensitive) name match with no alias table.

**Zenodo's licence field disagrees, and the repository wins.** The Zenodo deposit records the licence
as `other-open`, not MIT. DOI-derived metadata is convenient but it reproduces whatever the depositor
selected, including mistakes, so it must not override the repository's own `LICENSE.txt`. This is
worth remembering for any future refresh that autofills from the DOI: the licence, the version date
and the publication date are exactly the fields where that autofill goes wrong.

**No licence URI is recorded, and none can be.** The preceding dossier carried a second sub-field
labelled "License URI", holding `https://spdx.org/licenses/MIT.html`, as though it were a storable
value. There is
no per-software licence URI in HSSI: a software record points at a shared licence row, and the URL
lives on that shared row rather than on the software. Field 15's only storable value is the licence
name. The URI line is therefore not restored here — recording it would hand the next refresh a value
it would try to submit and fail on. `LICENSE.txt` remains perfectly good *evidence* for the choice;
it is just not a second value.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- f2py
- fortran
- geoscience
- ionosphere
- ionosphere-modeling
- iri
- python
- space-physics
- thermosphere

**Source:** These nine are the repository's own vocabulary. The first eight are exactly the GitHub
repository topics; `thermosphere` comes from `setup.cfg`, whose `keywords` block lists `ionosphere`
and `thermosphere`. They are recorded in the repository's lower-case hyphenated style.

**The PyHC registry's two additional tags were considered and not added.** The registry entry carries
`keywords: ["ionosphere_thermosphere_mesosphere","specific"]`. This is not the usual case of an
unsupported inherited domain tag — `ionosphere_thermosphere_mesosphere` is *truthful* here, since this
genuinely is an ionosphere/thermosphere model. They were still not added, for two reasons that a
future agent should weigh rather than re-derive: `specific` carries no meaning to a searcher and would
match nothing anyone would type; and the underscored registry-internal form would sit oddly in a list
that otherwise uses the repository's hyphenated topic style, without adding a term the existing
`ionosphere` and `thermosphere` keywords do not already cover. Recorded so the omission is not later
mistaken for an oversight.

### 17. Data Sources (OPTIONAL)
Not found

**Source — correctly empty, checked against the whole 17-row vocabulary.** That vocabulary lists data
archives and access protocols: `AMDA`, `CDAWeb`, `das2`, `FTP/FTPS Directories`, `GFZ`, `HAPI`,
`HTTP/HTTPS Directories`, `Madrigal`, `Observatory/Mission-specific`, `OMNIWeb`, `Other`,
`S3/Cloud-aware`, `SSCWeb`, `TAP`, `The Virtual Solar Observatory.`, `VirES`, `WDC`. This software
fetches from none of them. It takes scalar inputs — date and time, latitude and longitude, a solar
index — and reads only the coefficient files it bundles: 24 CCIR/URSI `.asc` files under
`iri90/data/`, which the wrapper points the Fortran at by passing its own package directory. A further
19 `.dat` files under `src/data/` (IGRF coefficients and an `apf107` index table) serve the standalone
Fortran library rather than the Python path. Bundled coefficient tables are not a data source in this
field's sense; they are part of the model.

### 18. Input File Formats (RECOMMENDED)
- ascii

**Source:** The coefficient files the model reads are ASCII. `iri90/data/` holds 24 `.asc` files
(twelve CCIR and twelve URSI, one per month each); `src/data/` holds 19 `.dat` files for the Fortran
library. The upstream `00readme.txt` marks each of these coefficient files `(ASCII)`. The wrapper
does not offer the user a file-input path — the primary inputs are programmatic parameters — so
`ascii` describes what the model loads rather than a user-supplied file format. That is the accurate
reading of a single-value field here and no other vocabulary row applies.

### 19. Output File Formats (RECOMMENDED)
Not found

**Source — correctly empty, checked against the whole 11-row vocabulary** (`ascii`, `CDF`, `csv`,
`FITS`, `HDF5`, `IDL.sav`, `ISTP-Compliant`, `JSON`, `netCDF3/4`, `Other`, `Zarr`). The package writes
no files. `runiri()` and `timeprofile()` return an in-memory `xarray.DataArray`, and the plotting
functions build matplotlib figures and hand them back without saving. The one thing that writes to a
stream is the standalone Fortran driver `src/iri90_driver.f90`, which prints a numeric table to
standard output — that is console output, not a file format, and it is outside the Python package.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source:** `README.md` gives a Fortran-compiler install path for each of the three. Its Install
section lists a Linux bullet invoking `apt install gfortran`, a Mac bullet invoking
`brew install gcc`, and a Windows bullet linking out to a mingw setup guide and writing a
`pydistutils.cfg` from PowerShell.

**Documented-supported, not continuously tested — record this caveat.** At the pin,
`.github/workflows/ci.yml` defines one active job, `linux`, running on `ubuntu-latest`. The `macos`
and `windows` jobs are present in the file but entirely commented out (`# macos:` and `# windows:`).
Because the repository is archived, they will never be re-enabled. The three values are therefore
right — the maintainer documents all three platforms and the package has no platform-specific code
beyond needing a Fortran compiler — but a future agent should know that only Linux was ever verified
by CI, and should not read the three values as three tested platforms.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Source:** Nothing in the tree targets an architecture. There is no SIMD intrinsic, no assembly, no
architecture-conditional build logic, and no architecture-specific compiler flag; the only explicit
compiler flags anywhere in the build files are `-std=legacy` for GNU Fortran and `-w` for the f2py
extension build. Portability is
bounded by the availability of a Fortran compiler, not by the CPU, which is exactly what
`CPU Independent` means.

### 22. Related Phenomena (OPTIONAL)
Not found

**Source — correctly empty, and the whole vocabulary is the reason.** The field offers seven values:
`Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`,
`Solar Wind`, `X-ray emission`. Six are solar or heliospheric and have no bearing on an ionospheric
climatology. The seventh, `Geomagnetic Storms`, is the one a future agent might reach for — and it is
specifically wrong here: the model supplies values *for magnetically quiet conditions*, which is the
opposite of the storm-time case. Selecting it would actively mislead a visitor filtering for
storm-related software.

**Corroborating API fact.** `runiri()` accepts an `ap` geomagnetic-activity index in its signature,
which could suggest storm-time capability. It does not have any: `ap` never reaches the Fortran. The
wrapper's parameter handling is set out in full in the closing section "A precise API limitation
worth carrying forward"; `ap` is carried only as metadata on the returned array.

### 23. Development Status (RECOMMENDED)
Unsupported

**Source and the decisive fact.** The GitHub repository is archived. An archived repository is
read-only: it accepts neither issues nor pull requests. Work on it has ceased, and there is a stable,
usable release (v1.1.1 on PyPI, plus the Zenodo deposit). The `Unsupported` row's stored definition
matches that state exactly: "The project has reached a stable, usable state but the author(s) have
ceased all work on it. A new maintainer may be desired."

**Why each alternative fails.** The RepoStatus vocabulary carries definitions, and they decide this:

- **`Inactive`** — "The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows." Rejected because archiving
  *forecloses* the support channel that definition promises. The repository cannot accept an issue or
  a pull request at all, so "as time allows" is not merely unlikely — it is impossible.
- **`Moved`** — "The project has been moved to a new location, and the version at that location should
  be considered authoritative." Rejected on a real but insufficient hook: the project *did* move,
  twice (`scivision/pyiri90` → `scivision/iri90` → `space-physics/iri90`). But `space-physics/iri90`
  **is** the authoritative current location; there is no newer location for a visitor to be sent to.
  `Moved` describes a signpost, and this repository is the destination.
- **`Abandoned`**, **`Suspended`**, **`WIP`**, **`Concept`** — all four describe a project that has
  not yet produced a stable, usable release, with `Concept` covering minimal or no implementation at
  all. Each is falsified by `iri90` 1.1.1 on PyPI and the Zenodo deposit.
- **`Active`** — falsified by the archive flag and by a last push of 2021-10-11.

**Previous value, and why it was wrong.** The record carried no development status, and the preceding
dossier proposed `Inactive`, citing `setup.cfg`'s `Development Status :: 4 - Beta`. That reasoning
does not hold: the trove classifier is a PyPI convention describing a package's *maturity*, not its
repository status, and "Beta" does not correspond to `Inactive` under any reading of either
vocabulary. The evidence simply did not support the value it was offered for. A future agent should
not re-derive repository status from trove classifiers.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/iri90

**Source:** `README.md` at the repository URL is the documentation. There is no `docs/` directory, no
`.rst` file, no ReadTheDocs configuration and no documentation site anywhere in the tree at the pin;
the GitHub repository's `homepage` field is unset. Beyond the README, the usable documentation is the
two example scripts (`AltitudeProfile.py`, `TimeProfile.py`) and the docstrings in `iri90/plots.py`.

**Negative research on the wiki — do not chase it.** GitHub reports `has_wiki: true` for this
repository, which is a default that says nothing about whether a wiki exists. It does not: cloning
`https://github.com/space-physics/iri90.wiki.git` returns "Repository not found". A wiki is a separate
git repository and is not reachable from the code pin, so no Field 12 or Field 24 claim can rest on
wiki content here.

### 25. Funder (OPTIONAL)
Not found

**Source — negative research.** No award, grant number or funding acknowledgement appears anywhere in
the tree at the pin, including the vendored Fortran. Institution names do appear there — `src/igrf.for`
credits contributors at NASA/GSFC, NSF, DMI and IZMIRAN, and `00readme.txt` gives a NASA contact
address for the upstream IRI project — but those are author affiliations and contact details for the
*upstream model*, not funders of this software. A future agent should not read them as Field 25
candidates. The only funding-adjacent file the repository
ever had is `.github/FUNDING.yml`, added 2019-10-07 and deleted 2021-04-27 in a commit titled
"Delete FUNDING.yml". Its two entries, under the GitHub template's comment header, were a GitHub
Sponsors account and a Ko-fi account, both for `scivision`. That is personal sponsorship, not grant
funding, and it names no funding organization. There is also no publication for this package
(Field 14) whose acknowledgements could be consulted — the usual fallback route for this field is
unavailable here, not merely unexplored.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

**Source:** Same negative research as Field 25. No award title or number exists to record, and there
is no publication whose acknowledgements could supply one.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

**Source:** The same ADS/SciX searches described under Field 14, with the same invalid-credential
control confirming the queries were live. No publication describing or citing this Python package was
found. `README.md`'s References section links only the upstream Fortran source, which is recorded
under Field 29 as software rather than as a publication.

**The same caution as Field 14 applies.** Papers about IRI-90 the international model are abundant and
are not related publications *of this software*.

### 28. Related Datasets (OPTIONAL)
Not found

**Source:** The package bundles empirical coefficient tables (Fields 17 and 18) but these are model
internals distributed with the code, not a separately identified dataset. No dataset DOI or external
dataset reference appears anywhere in the tree at the pin.

### 29. Related Software (OPTIONAL)
- http://download.hao.ucar.edu/pub/stans/iri/iri90.f
- https://github.com/space-physics/iri2016
- https://github.com/rilma/pyIRI2016
- https://github.com/space-physics/NCAR-GLOW

**`http://download.hao.ucar.edu/pub/stans/iri/iri90.f`** — a reasoned keep, not retention by default.
This is the live upstream provenance of the vendored Fortran, and Field 29 explicitly covers
"software this work was forked from". The evidentiary link is exact: `reference/original_iri90.f` at
the pin is identical to the file this URL serves as of this refresh, once trailing whitespace is
stripped from both. Both are 2979 lines; the raw files differ on 828 lines, and every one of those
differences is trailing whitespace only. It is the only entry here that is a source file rather than
a software project, and it earns its place because a visitor who wants to know where the model code
came from is served precisely by this link. `README.md` cites it in its References section as
`[Fortran Code](http://download.hao.ucar.edu/pub/stans/iri/iri90.f)`.

*Rejected: re-scheming it to `https://`.* The server 301-redirects `http://` to `https://`, and the
stored value is rendered to visitors as the link text, so the change is arguable. It was declined
because the stored form is exactly the URL the README cites, the link resolves either way, and
re-scheming would drop and re-attach the stored relation for a difference no visitor experiences.
Invisible tidiness is not a reason to change a stored value; recorded so the next refresh does not
reopen it.

**`https://github.com/space-physics/iri2016`** — the author's own Python and Matlab wrapper for the
newer IRI-2016 generation of the same international model. This is Field 29's paradigm case: a
peer tool for a different model generation, which tells a reader something real about the scope of
this one. State its evidentiary standing honestly: **the repository never mentions it.** A
case-insensitive search for `iri2016` across the tree at the pin returns zero matches. The relation
rests entirely on it being a same-author peer IRI wrapper, not on in-repo evidence.

**`https://github.com/rilma/pyIRI2016`** — an independent Python wrapper for IRI-2016 by a different
author (owner `rilma`, described upstream as a Python wrapper of the International Reference
Ionosphere 2016). It matches Field 29's own worked example almost word for word: "two software that
model the upper atmosphere of Earth but using different assumptions". Its evidentiary standing is
identical to that of the `iri2016` entry the record already carried — the repository does not mention
it either — which is why admitting one while excluding the other would have been indefensible.

**`https://github.com/space-physics/NCAR-GLOW`** — a companion package, and the only one of the three
software-project entries here with direct in-repo evidence (the fourth entry, the HAO source file, is
cited in `README.md` and so has its own). State that evidence at its true weight: a case-insensitive search for `glow`
across the whole tree at the pin returns **exactly one** line, `src/iri90_solomon.f:3`, reading
`C Special-purpose version of IRI90 for use with the GLOW model.`, with line 4 reading
`C This is not the original IRI90.` One documented line is the entire in-repo case, and it sits in a
file that **no build system compiles**. That claim rests on reading the whole build graph, not on a
name search: `meson.build`, `src/meson.build`, `CMakeLists.txt`, `src/CMakeLists.txt`, `setup.cfg` and
`pyproject.toml` name no source by wildcard, so every compile target in them is listed explicitly —
`setup.cfg`'s `packages = find:` discovers Python packages, not compile targets; the only
glob-shaped constructs anywhere in the build and packaging surface are the two data-file patterns
in `setup.py`, `iridata = glob(join("data", "*.asc"))` and `package_data={"pyiri90": ["data/*.asc"]}`,
neither of which can match a Fortran source; and there is no `Makefile` or other build entry point at
the pin. A name-grep alone would not have settled this, because a glob would compile the file without
ever naming it.

Do not read that as unusual, and do not write it as though the file were singled out. Carrying unbuilt
vendored material is this repository's normal state: taking the union of every explicit source list
against the tree, 10 of the 15 Fortran sources at the pin are compiled by at least one build system
and 5 are compiled by none — `reference/original_iri90.f`, `src/iri90_solomon.f`, `src/irifp3.for`,
`src/iriorbit.for` and `src/iriorbitmax.for`. The GLOW file's evidentiary value is that this repository
ships and documents a GLOW-purposed IRI90 variant, not that GLOW is built or exercised here.

That one line is nevertheless strictly more than the `iri2016` entry has, which has zero matches
anywhere in the tree and is retained purely as a same-author peer. Excluding GLOW while
keeping `iri2016` would have put the rejection bar above the acceptance bar. Both numbers are recorded
so a future agent can re-derive the reasoning rather than inherit a verdict.

**Removed — `https://numpy.org/` and `https://matplotlib.org`.** These were removed because the rule
applied, not as a curatorial preference a later reviewer might reverse. Field 30's Tier A clause reads:
"Never list these (Tier A), no exceptions: numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly,
bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click, setuptools, and the rest of the generic
scientific-Python/tooling stack", and Field 29 extends the same exclusion, adding that a package
rejected from Field 30 is not thereby a Field 29 entry. Both package names appear in that list. numpy is
a genuine hard dependency (f2py, which builds the extension, is part of it) and matplotlib is the
`plot` extra — but being a dependency is not what this field records, and an entry that would read the
same for most Python packages carries no information.

**Considered and rejected — `python-dateutil`, `pytest`, `flake8`, `mypy`, `setuptools`, `wheel`.**
The example scripts import `dateutil.parser`; `setup.cfg`'s `tests` extra lists `pytest`, `flake8` and
`mypy`; `pyproject.toml` requires `setuptools`, `wheel` and `numpy` to build. All are generic tooling
under the same rule.

**Considered and rejected — `ephem` (PyEphem).** Worth recording explicitly, because it is the one
dependency here that looks domain-adjacent and a future agent reading `iri90/plots.py` will encounter
`import ephem`. Three reasons it does not belong: it is a *soft, optional* import guarded by
`try`/`except ImportError`, and is not declared in `setup.cfg` at all — not in `install_requires` and
not in either extra; its sole use is decorative, drawing sunrise and sunset fiducial lines on the time
profile plot; and it is a general astronomical-ephemeris library rather than a heliophysics tool, so
it is not the domain-specific dependency Field 29 asks for. It would be equally at home in an
amateur-astronomy or a scheduling application.

### 30. Interoperable Software (OPTIONAL)
- https://xarray.dev

**Source and the rule applied.** xarray is a Tier B package under Field 30, admissible "only when a
specific exchange is documented in the public API, docs, examples, or tests — never on dependency
presence alone", with the doc's own qualifying example being that the public API returns an xarray
object as its documented interchange format. That is exactly the situation here:

- Both public entry points in `iri90/__init__.py` — `runiri()` and `timeprofile()` — are annotated
  `-> xarray.DataArray`. It is the package's sole return type; there is no alternative plain-array
  path.
- `README.md` states of the return value that
  `` `iono` is an xarray.DataArray indexable by species, altitude, etc. and includes metadata. `` —
  i.e. the documentation presents the xarray object, and the metadata it carries, as the interface a
  user works with.
- The returned object is a genuine interchange carrier rather than an internal convenience: it is
  labelled by named coordinates (`alt_km`, `sim`, and `time` for the time profile) and carries the run
  parameters in `attrs`, so a downstream tool receives a self-describing object.

**This entry was moved here from Field 29, where it had been recorded as a "required dependency".**
That was the wrong field and the wrong justification — dependency presence is explicitly not
sufficient for Field 30 and does not qualify a Tier B package for Field 29 either. The documented
return-type contract is what admits it, and a future agent should keep the justification attached to
the entry rather than to the `install_requires` line.

**Rejected — blanket ecosystem claims.** The preceding dossier's reasoning for leaving this field
empty was that the package "uses standard Python scientific stack (numpy, xarray) which enables
interoperability with many packages". Field 30 names that exact form of argument as never sufficient
on its own, alongside "a PyHC member, so it interoperates with PyHC packages". Neither is used here.

**Rejected — numpy.** Tier A, no exceptions, notwithstanding that f2py builds the extension.

### 31. Related Instruments (OPTIONAL)
Not found

**Source — examined, and correctly empty.** IRI-90 is instrument-agnostic. It takes date, time,
location and a solar index and returns interpolated climatological coefficients; it reads, parses,
calibrates and processes no instrument's data.

**What was searched, and what was found — fitting rows exist and were declined.** The
instrument/observatory vocabulary was searched by concept (ionosonde, digisonde, incoherent scatter,
sounder, GNSS, GPS, riometer, topside, TEC, beacon) and by the facility and satellite names that
appear in the tree. That search did not come back empty, and recording so is the point: rows exist for
the very hardware the vendored comments name, and they were declined on the relevance gate rather than
missed. On the instrument side, the topside sounders behind the ISIS comment quoted below are
catalogued as `https://spase-metadata.org/SMWG/Instrument/ISIS1/SFS`
("ISIS1 Swept-Frequency Sounder"), `https://spase-metadata.org/SMWG/Instrument/ISIS2/SFS`
("ISIS2 Swept-Frequency Sounder") and `https://spase-metadata.org/SMWG/Instrument/ISIS2/FFS`
("ISIS2 Fixed-Frequency Sounder"); and the instrument named at `src/iriflip.for:1313` has a row of
its own, `https://spase-metadata.org/SMWG/Instrument/AE-E/PES` ("Photoelectron Spectrometer"). The
observatory-level rows are named under Field 32.

Two of the names return nothing at all, and a third resolves only to the wrong thing — but the
decision deliberately does not rest on either fact. Searching the vocabulary's names, identifiers and
abbreviations returns nothing for `Arecibo` and nothing for `IK19`, while `Jicamarca` returns three
rows that are a fluxgate magnetometer and a GIRO ionosonde station at that site rather than the radio
observatory the Te comment means. Those gaps are incidental. The field is empty because this software
supports none of the rows that *do* exist.

**Where instrument and facility names do occur, and why none qualifies.** They occur in more places
than one, so do not expect a short list — Jicamarca, Arecibo, ISIS 1 and 2, IK19, AEROS and the
Atmosphere Explorer satellites (AE-C and AE-E by name) are all named, and the vendored
magnetic-field code additionally labels a legacy field model after the POGO satellite series
(`POGO 68/10`, `POGO-75`). What matters is that every one of those occurrences is confined to the
vendored Fortran and tables under `src/` and `reference/`, and records which historical observations
an empirical coefficient set was fitted to, or which legacy model variant is in use. Representative
lines, quoted at the pin:

- `src/irisub.for:1594` — `C Te-MAXIMUM based on JICAMARCA and ARECIBO data`
- `src/irifun.for:5170` — `C    according to the observations by space ionosondes ISIS 1,ISIS 2, and IK19.`
- `src/irisub.for:1627` — `c Te(600km) from AEROS, Spenner and Plugge (1979)`
- `src/irisub.for:1606` — `c ISIS, Brace and Theis`
- `src/iriflip.for:1313` — `C...... the Atmosphere Explorer-E PES fluxes of John Doering (Lee et al.`

Most are Fortran comments. Two are not, and are worth naming so the pattern is not overstated:
`src/irisub.for:703` is an output-label statement, `9033    format('Te: Aeros/AE/ISIS model')`, and
`src/iritest.for:120` is a flag assignment with an inline comment,
`          jf(23)=.false.     ! t=AEROS/ISIS f=TTS Te with PF10.7`. Both still describe which
empirical Te model is in use rather than any data the software reads.

None of these names appears outside `src/` and `reference/`: a case-insensitive search for
`jicamarca`, `arecibo`, `aeros`, `isis`, `ik19`, `ae-c`, `ae-e` and `pogo` across every other tracked
file — `iri90/`, `README.md`, `setup.py`, `setup.cfg`, `pyproject.toml`, `00readme.txt`, the two
example scripts, the build files, the CI workflow and the archived CI configs — returns nothing. So
they belong to the model's fitting history, not to this package's capabilities.

Under Field 31's relevance gate this is precisely the excluded case — the software does not read,
parse, calibrate or process any of those instruments' data. The resolution ladder also names a generic
class label such as `Ionosonde` as an omit-and-document outcome, which covers the ISIS/IK19 comment's
"space ionosondes" phrasing.

**This rejection and the Stan Solomon rejection under Field 6 share one shape**, and seeing that is
what makes both durable. In each, the repository carries a genuine and prominent trace of something
upstream — an adapted model's author there, the observations a coefficient set was fitted to here —
and in each the trace records provenance rather than the relationship the field is asking about.
Provenance is not authorship, and fitting heritage is not designed-to-support. If fitting heritage
counted as support, every empirical model would attach to every observatory in its lineage. A future
agent who finds one of these arguments persuasive should expect to have to accept the other.

**A method warning for whoever re-checks this — the negative is easy to fake.** `git grep -E` does
not implement `\b`. It reads the escape as a literal `b`, which is checkable on this tree:
`git grep -E '\bar'` and `git grep -E 'bar'` return the identical single-file match set
(`src/irifun.for`), while the unanchored `ar` returns 34 files. The system `grep` does honour `\b`, so
sanity-checking a pattern outside git and then running it through `git grep` produces a false
negative. On the search behind this field, the same case-insensitive pattern
`\b(arecibo|jicamarca|isis)\b` matches 0 tracked files under `git grep -E`, 6 under `git grep -P`,
and the same 6 under the system `grep -rE` once it is restricted to tracked files — a directory-wide
system grep in a working checkout counts one file more, because this dossier names those instruments
itself; dropping the anchors makes `git grep -E` match 6 as well. Worse, `git grep -E` exits 1 on
that zero — the ordinary "no matches" code — so a zero meaning "clean" is
indistinguishable from a zero meaning "your anchors were reinterpreted". The remedy is `git grep -P`,
or plain alternation, and always confirming a negative with a positive control. Do not overstate this
into distrusting `\b` itself: it asserts a token boundary, not a delimiter boundary, so `\barray\b`
excludes `myarray` but still matches `np.array`.

**The visitor test settles it.** Someone browsing ISIS 2 in the catalogue and asking for related
software would not expect an ionospheric climatology that never touches ISIS data. Listing these
would degrade that entry, not enrich this one.

### 32. Related Observatories (OPTIONAL)
Not found

**Source:** The same examination as Field 31. The software targets no platform, mission or facility.
The facilities and satellites the tree names — Jicamarca, Arecibo, ISIS 1 and 2, IK19, AEROS, the
Atmosphere Explorer satellites, and the POGO series carried in a legacy field-model label — appear
only in the vendored comments and tables catalogued under Field 31, which is not a
designed-to-support relationship. No observatory-level substitution applies either, because there is
no supported instrument for which a platform row could stand in.

**Fitting rows exist, and this field is empty by decision rather than by absence.** The vocabulary
carries observatory rows for the satellites those comments name:
`https://spase-metadata.org/SMWG/Observatory/Aeros-A` ("Aeros A") for the first AEROS satellite, the
vocabulary carrying no AEROS-B row; `https://spase-metadata.org/SMWG/Observatory/AE`
("Atmosphere Explorer") for the programme, with
`https://spase-metadata.org/SMWG/Observatory/AE-C`,
`https://spase-metadata.org/SMWG/Observatory/AE-D` and
`https://spase-metadata.org/SMWG/Observatory/AE-E` for the C, D and E spacecraft and
`https://spase-metadata.org/SMWG/Observatory/Explorer32` for Atmosphere Explorer-B, whose identifier
does not follow the `AE-` pattern the others do; and
`https://spase-metadata.org/SMWG/Observatory/ISIS1`,
`https://spase-metadata.org/SMWG/Observatory/ISIS2`, plus the programme-level
`https://spase-metadata.org/SMWG/Observatory/ISIS`, all three carried under the name
"International Sats for Ionosph Studies". Of the satellites named in those coefficient-provenance
comments, only `IK19` has no row at all.

Each of those rows was declined. Selecting any would assert that this software is designed to support
that mission, and it is not: a climatology fitted decades ago to ISIS and AEROS observations cannot
ingest those missions' data, and exposes no path by which a user could feed it any. Recording the
rows by identifier is what converts this field from "no fitting row was found" into "fitting rows were
found and deliberately not used" — the distinction that stops a future agent concluding nobody
checked. It is the same distinction drawn under Field 31 and, for authorship, under Field 6.

### 33. Logo (OPTIONAL)
https://spdf.gsfc.nasa.gov/research/IRI/website/doc/images/tail-179.jpg

**What this image actually is.** Fetched and inspected: `image/jpeg`, 179 × 119, 15,318 bytes. It is a
NASA Space Shuttle photograph of aurora over Earth's limb — decoration from the SPDF IRI *project*
website, not a mark this repository ever published. That is stated plainly so a future agent does not
"discover" it and reopen the question.

**Why it is kept anyway.** The PyHC registry entry for `IRI-90` presents it as this project's logo, in
its `logo:` field. Field 33's guidance names exactly that — whether the project itself presents the
image as its logo — as good reason to keep such a value even when it is not a conventional wordmark.
The guidance also states that an asset not hosted in a git repository is "a perfectly good Field 33
value"; there is no commit to pin, so the URL is recorded as-is and verified reachable.

**On the URL form.** The registry lists `https://iri.gsfc.nasa.gov/images/tail-179.jpg`. That URL
redirects to the value stored here and serves a byte-identical image (verified by fetching both and
comparing). The resolved form is stored because it is the more stable of the two — it does not depend
on a redirect continuing to exist.

**Alternatives considered and rejected.**

- *Clearing the field as a documented omission.* Rejected: a documented omission is a legitimate
  outcome in general, but not when the project's own registry entry supplies an image.
- *Substituting the repository's own `.github/demoiri.png`.* Reachable commit-pinned at
  `https://raw.githubusercontent.com/space-physics/iri90/f5c6c898dc4ccb1c26ae086385f8e47f08ba2915/.github/demoiri.png`
  (`image/png`, 1040 × 646), and it is the image the README displays. It was rejected on inspection:
  it is an example altitude-profile plot the software produces — nine labelled density and temperature
  curves against altitude, titled with the run parameters — which the same Field 33 guidance names as
  not-a-logo. Swapping one non-logo for another gains the visitor nothing, and it would trade a
  curated registry choice for an auto-generated figure.

This choice is settled. It should not be re-raised absent new evidence, such as the project publishing
an actual mark — which, the repository being archived, will not happen there.

---

## Repository shape at the pin (context for future refreshes)

83 tracked files. No `CITATION.cff`, `codemeta.json`, `.zenodo.json`, `AUTHORS` or `CONTRIBUTORS`
file — which is why Fields 6, 14 and 27 rest on `setup.cfg`, `LICENSE.txt`, the Zenodo deposit and the
PyHC registry rather than on a machine-readable citation file. No `docs/` directory and no `Makefile`.
The Python package is `iri90/` (`__init__.py`, `plots.py`, `tests/test_all.py`, and 24 `.asc`
coefficient files under `data/`). Two example scripts sit at the repository root
(`AltitudeProfile.py`, `TimeProfile.py`) and one test file exists (`iri90/tests/test_all.py`). The
vendored Fortran is under `src/` (11 `.for`, `iri90.f`, `iri90_solomon.f`, `iri90_driver.f90`, and 19
`.dat` data files) and `reference/` (the pristine upstream `original_iri90.f`).

**Two stale fragments in `setup.py`**, noted because they look like evidence and are not. It computes
`iridata = glob(join("data", "*.asc"))` and never uses the result — and the glob would match nothing
anyway, since the `.asc` files live under `iri90/data/`, not `data/`. And its packaging line reads
`setup(ext_modules=ext, package_data={"pyiri90": ["data/*.asc"]})`, naming `pyiri90` while the actual
package directory is `iri90/` — a leftover from the pre-rename package name, and a second concrete
in-repo trace of the `scivision/pyiri90` → `space-physics/iri90` rename that explains why the Zenodo
deposit (Field 2) sits under the old name. Neither affects any field value or library use; both are
recorded so a future agent does not read `pyiri90` in `setup.py` as evidence of a second package.

**Scale of the modernization**, for anyone weighing how much of `src/iri90.f` is Hirsch's work versus
upstream's. Method-independent facts: `src/iri90.f` is 3008 lines and contains, *within that file*,
one `iso_fortran_env` reference and one `error stop` statement — the F2003 and F2008 bases recorded
under Field 13; `reference/original_iri90.f` is 2979 lines and contains neither; and
`reference/original_iri90.f` is identical to the live upstream HAO file once trailing whitespace is
stripped from both. (Tree-wide, `iso_fortran_env` appears in two files, while `error stop` is confined
to `src/iri90.f` — see Field 13. The per-file scope of the 3008-line sentence is load-bearing for
`iso_fortran_env`; dropping it makes the sentence false.) Qualitatively,
`src/iri90.f` is a substantially modernised derivative of that file rather than a lightly edited copy.
Line-level change counts between the two are method-dependent and must not be quoted bare. The one
invocation-stable figure is `git diff --stat`, which reports 1067 insertions and 1038 deletions at the
pin. A plain `diff` changed-line count is *not* stable on these two files — it varies with how the
comparison is invoked, so no such count is recorded here and none should be added. Any figure cited
later must name the method that produced it, and `git diff --stat` is the method to use.

## A precise API limitation worth carrying forward

`runiri()`'s signature is
`time: datetime, altkm: np.ndarray, glatlon: tuple, f107: float, f107a: float, ap: int`, but **two of
those parameters never reach the Fortran.** The call site passes, in order, `JF`, `jmag`, `glat`,
`glon % 360.0`, `-f107`, `monthday`, `hourfrac`, `altkm` and `datadir`. `f107a` and `ap` appear only in
the returned array's `attrs`, as metadata. Only `f107` influences the result, and it is passed
negated — which the Fortran documents as the intended calling convention, since the subroutine's
solar-activity argument is described as
`C         RZ12 (-COV)   12-MONTHS-RUNNING MEAN OF SOLAR SUNSPOT NUMBER` with the continuation
`(OR EQUIVALENT F10.7 SOLAR RADIO FLUX AS` a negative number.

This is a real limitation of the wrapper rather than a reading error, and it is durable: the
repository is archived, so it will not be fixed. It also corroborates two field decisions above — the
absence of `Geomagnetic Storms` from Field 22 (the geomagnetic-activity input is inert) and the
model's characterization as a quiet-time climatology in Fields 8 and 9.
