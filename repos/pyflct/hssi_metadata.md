# HSSI Metadata Extraction Results

**HSSI Software ID:** d5abf164-694c-4a24-8528-7395a7a01326
**Repository:** https://github.com/sunpy/pyflct
**Source Revision:** 250028870f1eee77c2cf0093916634c8a8e64558
**Extraction Date:** 2026-09-09
**Validation Date:** 2026-09-11
**Validation Status:** PASS

---

**Scope note — read the evidence in two halves.** pyflct is a thin Python/Cython wrapper around a
vendored C library, and its tracked tree is almost entirely free of solar-physics vocabulary. A
case-insensitive, unanchored `git grep -c -i` over the whole tracked tree at the pinned revision
returns 0 files for `photosphere`, `chromosphere`, `corona`, `flare`, `CME` and `space weather`;
`magnetogram` matches one line (a comment at `cextern/flctsubs.c:2703`), and `solar` matches one
line (inside a URL in `pyflct/flct.py`). Controls in the same sweep, in that same unanchored
case-insensitive form: `flct` 29 files (positive), `xylophone` 0 (negative). Anchoring changes only
the positive control — word-anchored, `(?<![0-9A-Za-z])flct(?![0-9A-Za-z])`, `flct` is 16 files —
while every zero above holds under every variant. Consequently the *code* evidence settles what the
software does mechanically (Fields 4, 13, 18–21), while the *domain* fields (5, 8, 16, 22, 27) rest
on the reference papers named in `docs/index.rst` and on the upstream FLCT project — never on
repository prose. Any later refresh that greps the repository for domain terms and finds nothing has
not discovered new evidence; it has re-run this sweep.

A second structural fact governs several fields: the whole of pyflct's code arrived in this
repository in a single squashed commit, `43a6bd0` (2020-04-04), whose subject is
`Add code to make it a real package (#1)` and whose body reads
`Moved everything from sunkit-image to here.` The authorship, and the project lineage, therefore live
in sunkit-image's history rather than in this repository's — see Fields 6 and 29.

---

## Section 1: Basic Information

### 1. Submitter

- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Not submitted metadata about the software; the submitting person is supplied at submission time.

### 2. Persistent Identifier (RECOMMENDED)

- **Value:** Not found

pyflct has no DOI. This is an evidenced negative, not an unchecked blank, and the method is recorded
so a later refresh does not repeat it.

At the pinned revision there is no `CITATION.cff`, no `.zenodo.json`, no `codemeta.json`, no DOI badge
in `README.rst`, and no GitHub–Zenodo release integration. A case-insensitive `git grep -i -- doi`
over the whole tracked tree returns six lines in three files, and not one of them is a DOI. Four are
the word
"doing" inside the vendored C library — `cextern/flctsubs.c` lines 338 (`doing the
cross-correlation`), 1133 (`doing nothing`), 1881 (`for doing byteswaps`) and 2833 (`doing LCT on
f1merc and f2merc`). One is `not doing this` in `docs/install.rst:63`. The remaining line, and the
only occurrence of `doi` as a token rather than as a substring of "doing", is the linkcheck regular
expression `r"https://doi.org/\d+"` at `docs/conf.py:36`, which exists so Sphinx's link checker
skips DOI URLs appearing in documentation prose; it asserts nothing about this package.

A DOI search must not key on the repository name alone, because a manually deposited record need not
contain it. Six DataCite queries were run on 2026-09-09 against the Zenodo client, all of the form
`https://api.datacite.org/dois?client-id=cern.zenodo&query=<q>&page[size]=1` (note `client-id` is a
parameter, not a query term): `titles.title:pyflct`; free text `pyflct`; free text `"sunpy/pyflct"`;
`relatedIdentifiers.relatedIdentifier:"https://github.com/sunpy/pyflct/tree/v0.3.1"`;
`titles.title:"Fourier Local Correlation Tracking"`; and
`creators.name:Freij AND titles.title:flct`. Every one returned 0. Four positive controls run in the
same sitting with the identical URL shape returned non-zero — `creators.name:Freij` 363, free text
`"sunpy/sunkit-image"` 10, the tree-URL form for `sunkit-image/tree/v0.7.0` 2, and
`titles.title:msise00 AND creators.name:scivision` 3 — so the zeros are real absences rather than a
broken query form.

Consequence for Field 11: with no DOI, the publisher is the repository host rather than Zenodo.

### 3. Code Repository (MANDATORY)

- **Value:** https://github.com/sunpy/pyflct

The project's canonical repository, and the URL the PyHC registry records as its `code` entry. Also
the base of the pinned revision this dossier was reconciled against.

### 4. Software Functionality (RECOMMENDED)

- **Selected Values:**
  - Data Processing and Analysis
  - Data Processing and Analysis: Analysis
  - Data Processing and Analysis: Image Processing

**The bar applied, in both directions.** A category is selected when a documented, user-callable
capability of the installed package matches the category's criteria wording. It is rejected when the
only match rests on a dependency, on user code in the example gallery, or on a paraphrase looser than
the criteria. Every value is written `Parent: Child`, because thirteen child names recur under more
than one parent and a bare child would bind to an arbitrary row.

The package's entire public surface is small enough to enumerate: `pyflct/__init__.py` declares
`__all__` as `["flct", "__version__"]` — one callable plus the version string — and
`pyflct/utils.py` declares `__all__` as `read_2_images`, `read_3_images`, `write_2_images`,
`write_3_images`, `column_row_of_two`, `column_row_of_three`. `flct(image1, image2, deltat, deltas,
sigma, ...)` returns three numpy arrays.

- **Data Processing and Analysis** — the parent of both selected children, and independently correct:
  the package reads, transforms and analyses scientific arrays.
- **Data Processing and Analysis: Image Processing** — the criteria call for scientific processing of
  2D image data. `flct`'s own docstring opens `Performs Fourier Local Correlation Tracking by calling
  the FLCT C library.`, its parameters are two 2D images, and the operations are exactly image
  processing: Gaussian windowing (`Sub-images are weighted by Gaussian of width `sigma`.`), an
  optional low-pass filter (`Apply a low-pass filter to the sub-images, with a Gaussian of a
  characteristic wavenumber`), and an intensity threshold. This is the single most defensible value in
  the field.
- **Data Processing and Analysis: Analysis** — the criteria cover derived physical quantities and
  scientific calculations beyond basic processing. `flct` does not return processed images; it returns
  a velocity field in physical units: the docstring states that velocity is computed in units of the
  pixel side length `deltas` divided by the time separation `deltat`. Producing a derived physical
  quantity from observations is analysis, and the skill's own guidance names omission of this
  catch-all as a common under-classification.

**Rejected, each under the same bar:**

- **Data Visualization** and **Data Visualization: 2D Graphics** — *rejected; `Data Visualization` was
  the previously recorded value and has been removed.* The package exposes no plotting
  entry point. `matplotlib` appears in four files at the pin — the `docs` extra in `setup.cfg`,
  `docs/conf.py`, `.rtd-environment.yml`, and `examples/running_flct.py` — and in none of them is it
  imported by the installed package. In the gallery example it is the *user* who builds the figure
  (`ax2.quiver(U, V, vel_x, vel_y, scale=20)`); pyflct supplies only the arrays. The classification
  rule that a package importing a plotting library is not thereby a visualization package applies here
  in its strongest form, since pyflct does not even import it. Read from the searcher's side, a user
  filtering HSSI on Data Visualization and landing on a library with no plotting API has been
  mis-served.
- **Data Processing and Analysis: Time Series Analysis** — *rejected.* Proposed by the 2025-12-02
  extraction. `flct` takes exactly two images and a scalar `deltat`; there is no time axis, no series,
  no temporal filtering, autocorrelation or trend analysis anywhere in the API. An image *pair* with a
  separation is not time-ordered data in the sense the criteria describe. A user who applies pyflct
  repeatedly across a sequence is doing time-series work with pyflct as one step, which is not the
  same claim.
- **Data Processing and Analysis: File Format Conversion** — *rejected.* The read/write utilities
  consume and produce the same binary `.dat` format, so nothing is converted between formats. The
  `column_row_of_*` helpers change memory ordering (column-major to row-major), not file format.
- **Data Processing and Analysis: Processing** — *rejected.* Its criteria describe pipeline steps and
  transformation chains, which pyflct is not; and what it would cover here is already carried, more
  specifically and more usefully to a searcher, by Image Processing.
- **Data Processing and Analysis: Data Access and Retrieval** — *rejected.* The package retrieves
  nothing remotely; input arrives as in-memory arrays or a local file path.
- **Models and Simulations** and its children — *rejected.* FLCT infers flows from observations; it
  does not model or simulate a physical system, and it produces no synthetic data.
- **Coordinate Transforms** and its children — *rejected.* The `pc` / `latmin` / `latmax` options
  handle Plate Carrée-projected input inside the correlation, which is a projection-aware calculation,
  not a user-facing conversion between coordinate systems.

### 5. Related Region (RECOMMENDED)

- **Selected Values:**
  - Photosphere
  - Solar Environment

The `Region` vocabulary is **flat**: every row is a top-level value. `Photosphere`, `Chromosphere`,
`Corona`, `Solar Interior` and `Solar Environment` are separate, independent rows. A coarse value
never implies a fine one and a fine value never implies its coarse relative, so "Solar Environment
encompasses the photosphere" is not an argument for or against either — each row must be earned on
its own.

Per the scope note, the repository itself supplies no regional evidence at all; it comes from the
papers `docs/index.rst` names as references for the algorithm.

- **Photosphere** — earned directly. Welsch et al. 2004, the first reference listed, is titled
  `ILCT: Recovering Photospheric Velocities from Magnetograms by Combining the Induction Equation with
  Local Correlation Tracking`, and Fisher et al. 2020 (`The PDFI_SS Electric Field Inversion
  Software`) inverts electric fields at the photosphere from the same class of measurement. This is
  the region FLCT's input data is measured in and where its output velocities live. It was not
  previously recorded; the vocabulary's flatness is why it had to be added explicitly rather than
  being implied by the coarser value.
- **Solar Environment** — retained. It is the correct coarse home for a tool whose entire documented
  purpose is solar, and it keeps the entry visible to searchers browsing at that granularity.

**Rejected:**

- **Corona** — the recorded description notes that FLCT-derived velocities feed `data-driven
  simulations of solar corona behavior`. That is a downstream *consumer* of the output, two steps
  removed; the software's own functionality operates on photospheric image pairs. Selecting Corona
  would return pyflct to a searcher looking for coronal science tools, which it is not.
- **Chromosphere**, **Solar Interior** — no reference paper or documentation associates the technique
  with either as implemented here.
- **Solar Wind**, **Interplanetary Space**, the Earth and planetary rows — nothing in any source
  connects the software to them.

### 6. Authors (MANDATORY)

- **Selected Values:**
  - The SunPy Developers — no author identifier, no affiliation

**The author is recorded as the collective the package itself declares: `The SunPy Developers`, with
no identifier.** The alternatives below were weighed against the upstream-history evidence and
rejected; they are kept on file so a later refresh does not re-propose them as though they were new.

*The evidence.* `setup.cfg` declares `author = The SunPy Developers` with
`author_email = sunpy@googlegroups.com` (a mailing list), and `README.rst` states
`This project is Copyright (c) The SunPy Developers and licensed under the terms of the LGPL-2.1
license.` So the collective is what the package itself declares. The PyHC registry gives the contact
as `SunPy Steering Committee`. There is no `CITATION.cff`, no `.zenodo.json` and no Zenodo creators
list, so there is no third source to reconcile against.

Actual authorship, however, is not visible in this repository's history, because the code arrived in
one squashed commit. `git shortlog -sne` at the pin lists only four authors — `pre-commit-ci[bot]` 43,
Nabil Freij 28, `dependabot[bot]` 4, Stuart Mumford 3 — and Mumford's three are
`initial render of the package template` (2020-04-02), `Set up CI with Azure Pipelines` (2020-05-02)
and `Add scheduled job to azure pipelines` (2020-10-12), i.e. packaging scaffolding rather than the
wrapper. Freij's `43a6bd0` (2020-04-04) is the import: `Moved everything from sunkit-image to here.`

Following that pointer upstream settles it. In sunkit-image, the FLCT subpackage was created by
**Vatsalya Chaubey** in commit `cc6be6a`, `Flct (#36)`, dated 2019-11-30 — a 50-file commit that adds
`sunkit_image/flct/flct.py` (293 lines), `sunkit_image/flct/utils.py` (243),
`sunkit_image/flct/src/pyflct.pyx` (162), `sunkit_image/flct/src/sunkit.c`, the vendored
`flctsubs.c`/`.h`, the test suite, the two gallery examples and the very
`docs/logo/sunpy_icon_128x128.png` file discussed under Field 33. That is substantially the whole of
pyflct as it stands at the pin. Nabil Freij is recorded as a co-author on that PR and is the author of
almost every subsequent human change here, but not of every change: across the 76 commits from the
import to the pin, `git log --format='%an' 43a6bd0..<pin>` counts Nabil Freij 27, `pre-commit-ci[bot]`
43, `dependabot[bot]` 4 and Stuart Mumford 2 — Mumford's two being the Azure Pipelines commits listed
above. Conor MacBride co-authored one infrastructure commit
(`Migrate to pyproject (#46)`, 2023-01-24).

*Why the collective was kept, and what each alternative would have cost a site visitor.*

- **The recorded value — `The SunPy Developers`.** It is exactly what the package declares, it matches
  how the project asks to be credited, and it singles nobody out unfairly (including the many
  non-commit contributors that a git-derived list would miss). The accepted cost is that the author
  carries no ORCID or ROR, so the entry contributes nothing to HSSI's author graph and a visitor
  cannot reach a person or a project page from it; and an identifier-less collective label aggregates
  only with rows carrying the same spelling, so identical credit does not reliably aggregate. That is
  not a hypothetical here: when this was checked on 2026-09-09, variant spellings of this same
  collective were already present among the catalogue's person rows — among them a `SunPy` /
  `Community` row carrying the sunpy CITATION.cff URL as its identifier, alongside this entry's own
  `The SunPy` / `Developers`. Whether that particular divergence still stands is not something this
  entry can keep current, and nothing about pyflct alone fixes it; it is a catalogue-level naming
  question. The durable cost of the recorded value is that pyflct's credit is contingent on spelling,
  and that cost was accepted with the divergence in view rather than overlooked.
- **Rejected — replacing the collective with the humans who wrote and maintain the code.** On the
  evidence above that list would be Vatsalya Chaubey (original author of the wrapper), Nabil Freij
  (imported it, and sole substantive maintainer since), and — if scaffolding counts — Stuart J.
  Mumford. It would have bought real, linkable credit and a place in the author graph, since two of
  those already have ORCID-bearing rows in the catalogue (Freij
  `https://orcid.org/0000-0002-6253-082X`, Mumford `https://orcid.org/0000-0003-4217-4642`). It was
  rejected because it contradicts the package's own declared author, and because it can under-credit:
  a single squashed import commit is a poor census of who contributed. Note also that this option's
  obvious short form — "the two humans in this repo's git log" — is *wrong*: it would credit Mumford's
  CI scaffolding while omitting the person who actually wrote the wrapper.
- **Rejected — keeping the collective and adding the individuals alongside it.** It would have
  preserved the project's declared credit while making the entry linkable, but it mixes an
  organisation-style label with people in one list, and the collective still has no identifier.
- **Rejected — crediting George H. Fisher and Brian T. Welsch.** They authored the FLCT algorithm and
  the C library pyflct vendors — `docs/index.rst` says `The C-based implementation of the FLCT
  algorithm is developed by George H. Fisher and Brian T. Welsch`, and `cextern/COPYRIGHT` carries
  `Copyright (C) 2007-2019, Regents of the University of California`. But they are the authors of the
  wrapped library, not of this package, and the copyright holder there is an institution. Their
  contribution is already represented where it belongs, in the publications under Field 27. Recording
  them as authors of pyflct would misattribute the wrapper.

*Two constraints that would bear on any later reconsideration.* First, an identifier for Vatsalya
Chaubey should not be invented: an ORCID fielded search on 2026-09-09
(`given-names:Vatsalya AND family-name:Chaubey`, with the control `given-names:Zzqqxx AND
family-name:Chaubey` returning 0) yields exactly one record, `https://orcid.org/0000-0001-5707-8018`,
but that record lists no employment or education and its single work is on application-layer coding
for data recovery — telecommunications, not solar physics. There is no corroboration that it is the
same person, so no ORCID is recorded for this author and a later refresh should not attach that one
without new evidence. Second, an author change must be made by sending the intended author list, not
by editing the existing entry in place: a metadata update cannot rename a stored person, and supplying
an identifier for an author whose stored row has none creates a second row rather than annotating the
first. Any departure from the recorded collective therefore needs its author list stated explicitly.

### 7. Software Name (MANDATORY)

- **Value:** pyflct

The distribution name in `setup.cfg` (`name = pyflct`), the repository name, the PyPI project name,
and the name the PyHC registry uses. Lower-case throughout every source; the title in `README.rst`
reads `pyflct: A Python wrapper for Fourier Local Correlation Tracking.`, so the lower-case form is
the project's own styling and not a normalisation artifact.

### 8. Description (MANDATORY)

- **Value:**

pyflct is a Python wrapper that allows users to perform Fourier Local Correlation Tracking (FLCT). The C-based implementation of the FLCT algorithm is developed by George H. Fisher and Brian T. Welsch. FLCT is used to estimate horizontal flow velocities on the Sun's surface by analyzing sequences of magnetic field images (magnetograms) taken at closely spaced time intervals. The software tracks magnetic field evolution at the photosphere, horizontal plasma motions, and active region dynamics. The derived flow velocities contribute to electric field inversions in the solar photosphere, data-driven simulations of solar corona behavior, studies of magnetic flux transport and emergence, and space weather forecasting models.

Retained unchanged. Every factual claim in it checks out against a primary source: the wrapper framing
and the attribution to Fisher and Welsch are `docs/index.rst`'s own wording; the photospheric
application and the electric-field-inversion use are the subject matter of the two papers that
document the algorithm (Welsch et al. 2004 recovers photospheric velocities from magnetograms; Fisher
et al. 2020 is the PDFI_SS electric field inversion software, which consumes such velocities). The
downstream uses named in the last sentence are the reasons the technique exists, and they give a
prospective user the context the form asks for.

**Considered and not selected:** adding a sentence stating the concrete interface — that a user passes
two 2D arrays and a time separation and receives `vx`, `vy` and a mask array — which is arguably the
most decision-relevant fact for someone judging whether the package fits their work, and which the
current text never states. It was not selected because the recorded description is sound, is the
project's and submitter's own framing, and the interface detail is one click away in the API reference;
rewriting a MANDATORY field for an improvement a reader would find marginal is churn. Recorded here so
a later refresh can weigh it rather than rediscover it.

### 9. Concise Description (OPTIONAL)

- **Value:** A Python wrapper for Fourier Local Correlation Tracking to estimate flow velocities from sequences of solar magnetogram images.

Retained unchanged. It is 127 characters, inside the field's 200-character limit and within the
150–200 character preview band the form describes. It is a slight expansion of the project's own
one-liner — `setup.cfg` has `description = A Python wrapper for Fourier Local Correlation Tracking.`,
identical to the GitHub repository description and to the PyHC registry's
`description: "A Python wrapper for Fourier Local Correlation Tracking"` — with the scientific purpose
appended, which is what makes it more useful as a preview than the bare package summary.

### 10. Publication Date (RECOMMENDED)

- **Value:** 2020-04-02

The date of the repository's first commit, `cc832b1` (`initial render of the package template`,
Stuart Mumford), which coincides with GitHub's `created_at` for the repository,
`2020-04-02T14:03:51Z`. The form asks for the date of first publication, used for the initial version.

Note the alternative that was not chosen: the first *release*, tag `v0.1`, is dated 2020-05-04, and
the first PyPI upload of `0.1` follows it. Repository creation is the earlier and more stable anchor
for "first broadcast/publication", and it is what the record already holds; the release dates are
carried by Field 12 instead.

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

The form directs that when no DOI has been obtained the publisher is the repository host, and Zenodo
is correct only for a DOI obtained through the GitHub–Zenodo workflow. Field 2 establishes that no DOI
exists, so GitHub is the right answer and Zenodo would be wrong. A ROR is not used here because the
identifier for a commercial code host is its URL.

### 12. Version (RECOMMENDED)

- **Version Number:** v0.3.1
- **Version Date:** 2024-07-31
- **Version Description:** (empty)
- **Version PID:** Not found

v0.3.1 is the latest release and the current one at the pin. Corroborated four ways: the git tag
`v0.3.1` on commit `3e617cc` dated 2024-07-31; the GitHub release for that tag, published
`2024-07-31T21:17:10Z`; the PyPI upload of `0.3.1` at `2024-07-31T21:23:34Z`; and the top section of
`CHANGELOG.rst`, headed `0.3.1 (2024-07-31)`. No version-level DOI exists — Field 2 establishes there
is no DOI of any kind.

**The full tag history, because the previously recorded list was wrong.** The nine tags in this
repository, with the commit date of each tagged commit, are: `v0.1` 2020-05-04, `v0.2` 2020-05-08,
`v0.2.1` 2020-05-08, `v0.2.2` 2021-04-01, `v0.2.2.post` 2021-05-15, `v0.2.3` 2022-05-24, `v0.2.4`
2023-11-27, `v0.3.0` 2024-07-23, `v0.3.1` 2024-07-31. The 2025-12-02 extraction's "previous versions"
note is superseded and must not be carried forward, but its error is narrower than invention, and the
narrower statement is the useful one. The two strings it lists as tags, `v0.2.0` and `v0.1.0`, are
indeed not tags — the tags are `v0.2` and `v0.1` — but they are real `CHANGELOG.rst` section headings
(`0.2.0 (2020-05-08)` and `0.1.0 (2020-05-01)`), and that file is where it took both the numbers and
most of the dates. Its dates are therefore changelog dates presented as tag dates: `0.1.0 (2020-05-01)`
against the `v0.1` tag's 2020-05-04. The list is not purely changelog-derived either — it gives 0.2.2
the tag date 2021-04-01 rather than the changelog heading — and it omits `v0.2.2.post`, which has a tag
but no changelog section at all. A later reader chasing `v0.2.0` or `v0.1.0` should look in
`CHANGELOG.rst`, not in `git tag`. Two further facts worth keeping: PyPI
holds seven releases (`0.1`, `0.2.1`, `0.2.2`, `0.2.2.post0`, `0.2.3`, `0.3.0`, `0.3.1`), so tags
`v0.2` and `v0.2.4` were never uploaded there; and `CHANGELOG.rst` heads its 0.2.2 section
`0.2.2 (2020-05-01)` while the `v0.2.2` tag sits on a 2021-04-01 commit, so the changelog dates are
not a reliable substitute for tag dates.

**The version description is deliberately left empty.** Two authored texts exist for this release and
neither was adopted: v0.3.1 is a build fix with no user-visible functional change, so a description
adds little for a visitor, and an empty field asserts nothing a source does not say.

The two texts, recorded so a later refresh can weigh them rather than rediscover them:

- **The changelog text, `Tried to fix builds on conda-forge.`** — the project's own release note, at
  the top of `CHANGELOG.rst` under `Bugfixes`, and what the maintainers chose to publish for this
  version. Its hedged wording is theirs.
- **The GitHub release body.** The release `name` is only `v0.3.1`; the authored content sits in the
  body, whose substantive line reads `* Fix issues with builds on conda-forge (hopefully) by
  @nabobalis in https://github.com/sunpy/pyflct/pull/80`. It carries an author handle and a PR URL
  that would need trimming before use.

If the field is ever filled, the 2025-12-02 extraction's `Bug fixes to resolve builds on conda-forge`
is not the text to use: it is a paraphrase matching neither source, and it silently drops the hedge
both authored texts contain.

### 13. Programming Language (RECOMMENDED)

- **Selected Values:**
  - C
  - Python 3.x

**The recorded value follows the criterion the form states — the languages most important for the
software — rather than a census of the tree.** Nothing here turns on what is in the tree; the
extension census at the pin is unambiguous. It turns on what this field is *for*, and the competing
reading was considered and rejected.

*What is in the tree.* Across 58 tracked files: `.py` 16, `.pyx` 1 (`pyflct/flct.pyx`, the Cython
bridge), `.c` 2 (`cextern/flctsubs.c`, the vendored FLCT library, and `pyflct/sunkit.c`) with 2 `.h`.
There are no `.pro`, `.f*`, `.m` or `.jl` files. `setup.cfg` requires `python_requires = >=3.10` and
lists `cython` under `setup_requires`, so Python 2.x is excluded and Cython is a real build-time
component rather than an incidental file.

*The criterion applied.* The form describes the field as `The computer programming languages most
important for the software.` and instructs `Select the most important languages (e.g., Python,
Fortran, C). This is not meant to be an exhaustive list.` Under that criterion the answer is **C and
Python 3.x**: the scientific work is C, the interface a user writes against is Python, and the single
`.pyx` file is glue between them. The entry is then honest about what a user reads and writes.

*Rejected — cataloguing every language present in the tracked tree.* Under that reading Cython would
have to be represented, and there is **no `Cython` row** in the 19-row vocabulary, so it could only be
recorded as `Other`, giving C, Python 3.x, Other. Its one real merit is completeness for someone who
needs to know a Cython toolchain is involved when building from source — a real concern here, since
source installation additionally requires a C compiler and the FFTW library. It was rejected because
`Other` would sit next to two specific languages and tell a searcher nothing on its own, and it is
unfilterable in any useful sense; the toolchain warning belongs in installation documentation rather
than in this field. Separately, the 2025-12-02 extraction proposed a literal `Cython` value, which is
unwritable — that spelling does not exist in the vocabulary and would be rejected.

### 14. Reference Publication (OPTIONAL)

- **Value:** Not found

**This field is empty by decision, because no publication describes pyflct.** The algorithm papers
stay in Field 27, where a plain list makes no claim that any of them is *the* publication for this
software. The reasoning spans both fields; it is written out here and cross-referenced from Field 27.

*The candidates, with titles confirmed from Crossref on 2026-09-09.*

- `https://doi.org/10.1086/421767` — Welsch et al., `ILCT: Recovering Photospheric Velocities from
  Magnetograms by Combining the Induction Equation with Local Correlation Tracking`, The
  Astrophysical Journal, 2004-08. Recorded in Field 27.
- `https://arxiv.org/abs/0712.4289` — Fisher & Welsch, `FLCT: A Fast, Efficient Method for Performing
  Local Correlation Tracking` (PASP Conf. Ser. 383, 373, 2008). Recorded in Field 27; it has no DOI,
  so the arXiv abstract page is the permanent link.
- `https://doi.org/10.3847/1538-4365/ab8303` — Fisher et al., `The PDFI_SS Electric Field Inversion
  Software`, ApJS, 2020-04-24. Not recorded anywhere. The 2025-12-02 extraction proposed it for this
  field.
- `https://doi.org/10.1007/s11207-015-0659-2` — `Analysing the Effects of Apodizing Windows on Local
  Correlation Tracking Using Nirvana Simulations of Convection`, Solar Physics, 2015-02-11. Listed in
  `docs/index.rst` under `Other references you might find useful are:`, not among the algorithm
  references.

*The decisive distinction.* `docs/index.rst` introduces the first three with
`The following papers are references for the FLCT algorithm:` — references for the **algorithm**, not
papers describing this software. No paper describes pyflct: there is no JOSS paper, no software note,
and none of the four predates or discusses the Python wrapper. Fisher et al. 2020 in particular
describes PDFI_SS, a separate electric-field inversion package that *consumes* FLCT-style velocities;
`cextern/COPYRIGHT` asks users to cite it because it documents updates to the C library's methods, not
because it documents pyflct. So the strict reading of this field — the DOI for the publication
describing the software — is satisfied by nothing.

*How the fields render, since that is what the visitor experiences, and why it settles the question.*
A Field 2 DOI would drive a "Cite Me" block typed as software — not available here, as pyflct has no
DOI. A Field 14 value renders as a distinct, labelled "Reference Publication" block, which is a
stronger claim than a list entry: it says *this* paper is the publication for this software. Field 27
renders as a plain list of related publications, which makes no such claim. That asymmetry is why the
empty field is correct rather than a gap.

*The alternatives, both rejected.*

- **Putting Fisher et al. 2020 in Field 14.** It is the most recent and most complete description of
  the algorithm and the C library pyflct wraps, and one of the two papers the vendored COPYRIGHT asks
  citers to cite. Rejected because the page would then render a labelled reference-publication block
  asserting that this paper describes pyflct, which it does not — it describes PDFI_SS.
- **Putting Fisher & Welsch 2008 in Field 14 instead.** It is the paper that actually introduces the
  FLCT method the package implements, and its title names FLCT. Rejected for the same category error,
  and it is an arXiv link rather than a DOI.

The accepted cost of the empty field is that the page carries no "Reference Publication" block at all,
so a visitor looking for "what do I cite" gets a list rather than a preferred citation, even though
`cextern/COPYRIGHT` states a clear preference (`the authors would appreciate a citation to these
papers`, meaning Welsch & Fisher 2008 and Fisher et al. 2019/2020).

**The Springer apodizing-windows paper is deliberately not added to Field 27.** `docs/index.rst`
places `https://doi.org/10.1007/s11207-015-0659-2` under `Other references you might find useful are:`,
alongside the link to the independent PyDL wrapper. The case for it is real: it is a methods study of
apodizing windows in local correlation tracking, useful to someone choosing pyflct's `sigma`, and it
is a documented project recommendation. It was rejected because it is explicitly *not* one of the
algorithm references, it does not cite or describe pyflct, and adding it would dilute a list whose two
entries are the algorithm's defining papers.

### 15. License (RECOMMENDED)

- **Value:** Other

**The licence itself is not in doubt.** pyflct is LGPL-2.1-or-later, evidenced five independent ways:
`setup.cfg` carries `license = LGPLv2+` and the classifier
`License :: OSI Approved :: GNU Lesser General Public License v2 or later (LGPLv2+)`; `README.rst`
states `This project is Copyright (c) The SunPy Developers and licensed under the terms of the
LGPL-2.1 license.`; `LICENSE.rst` is the FSF text headed `GNU LESSER GENERAL PUBLIC LICENSE` /
`Version 2.1, February 1999`; GitHub's API reports `spdx_id` `LGPL-2.1`; and PyPI's `info.license`
reads `LGPLv2+`. The vendored library agrees: `docs/index.rst` carries a note that the FLCT C source
is licensed under the GNU Lesser General Public License, version 2.1, and points the reader at
`cextern/COPYRIGHT`, which states the same and adds `Copyright (C) 2007-2019, Regents of the
University of California`.

**Relicensing history — durable, because reading the first commit alone gives the wrong answer.** The
initial commit `cc832b1` (2020-04-02) shipped GPL v3-or-later: `LICENSE.rst` opened
`Copyright (C) 2020, The SunPy Developers` above 708 lines of GPL-3 text, and `setup.cfg` read
`license = GNU GPL v3+`. On 2020-05-08, commit `cede8e2` (tagged `v0.2`) relicensed to
`license = LGPL-2.1`, and `262f116` the same day settled on the `LGPLv2+` spelling still in place at
the pin. The `LICENSE.rst` committed that day was git's own copy of the LGPL-2.1 text, preamble
included; `348b25f` (2022-05-24) replaced it with the clean 458-line FSF text. The relicensing plainly
aligns pyflct with the LGPL-2.1 FLCT library it vendors. This matters because
`GNU General Public License v3.0 or later` **is** a live vocabulary row: an agent reading only the
initial commit would find a perfectly writable value that is factually wrong today. It must not be
"corrected" backwards.

**`Other` is recorded, because no vocabulary row names LGPL-2.1.** The list has 11 rows and none of
them is this licence. `Other` is accurate in the narrow sense that the licence is not in the list, and
it is the only candidate that carries no misleading URL — that row's `url` is empty. Its accepted cost
is that it tells a visitor nothing on its own and is indistinguishable from a licence nobody bothered
to determine; the evidence above is on file precisely so that a reader who reaches this dossier learns
what the licence actually is. It was chosen over:

- **Leaving the field empty**, which is how the record previously stood. Nothing false would be
  asserted, but a visitor filtering by licence would never see pyflct at all, and the entry would look
  as if its licence were unknown when it is thoroughly documented. `Other` at least keeps the entry in
  the facet and says the licence was determined and is unlisted.
- **`GNU Library or ‘Lesser’ General Public Licenses (LGPL version 2)`**, the nearest row by name.
  Rejected because its stored `url` is `https://spdx.org/licenses/LGPL-2.0`, i.e. SPDX **LGPL-2.0** —
  a different licence from LGPL-2.1. Because licence is a foreign key to a shared row, selecting it
  would publish that row's URL on pyflct's page and point a visitor at the wrong licence text. (Note
  the row name uses typographic quotes around `‘Lesser’`; were it ever used, it would have to be
  copied character-for-character.)
- **Requesting a new `GNU Lesser General Public License v2.1 or later` row.** This is the only route
  that ends with the record being exactly right, and it remains open. It is a change to a vocabulary
  shared by every entry in the catalogue, so it is not ours to make unilaterally; it would need to go
  to whoever maintains the licence list. `Other` is the correct interim value, and should give way to
  the new row if one is ever created.

**On the form's "License URI" sub-field:** do not treat it as a per-software value here. The stored
licence is a foreign key to a shared licence row, and the URL belongs to that row — there is no
per-software licence URI to fill in. The 2025-12-02 extraction recorded
`https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html` as a License URI; that URL is correct *about
the licence* but is not a storable field value, and it should not be carried forward as if it were.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- **Selected Values:**
  - data analysis
  - flct
  - flow field
  - fourier local correlation tracking
  - image processing
  - magnetogram
  - photosphere
  - solar
  - velocity tracking
  - wrapper

All ten are retained; none is unsupported. Keyword rows are stored lower-case and rendered title-cased
on the page, so the list above is the stored form — the rendered `Flct` and `Data Analysis` are display
transforms, not the values.

Provenance and support, term by term: `solar`, `wrapper` and `data analysis` come from the PyHC
registry entry, whose `keywords` are `["solar", "wrapper", "specific", "data_analysis"]` (the stored
`data analysis` is the space-separated normalisation of PyHC's `data_analysis`). `flct` and
`fourier local correlation tracking` are the software's name and the expansion used throughout the
documentation. `image processing`, `flow field` and `velocity tracking` describe what `flct` does and
returns. `magnetogram` and `photosphere` are the domain of the reference papers rather than of the
repository text — per the scope note, `magnetogram` appears once in the tree (a comment in the
vendored C source) and `photosphere` not at all — but they are the terms a solar physicist would
search on to find this tool, which is what this field is for.

**Deliberately not added:** PyHC's fourth keyword, `specific`. It is a PyHC taxonomy tag meaningful
only inside that registry's own faceting; as a standalone HSSI keyword it says nothing.

**Considered and not added:** `optical flow`, which already exists as a keyword row and would place
pyflct alongside other flow-estimation tools for a searcher. It was not added because no source read
for this dossier — not the repository at the pin, not the PyHC entry, not the papers named in
`docs/index.rst` — uses the term for FLCT; adding it would be an inference dressed as a keyword. A
later refresh with a citable source may add it.

GitHub topics are not a source here: the repository's `topics` array is empty (checked 2026-09-09).

### 17. Data Sources (OPTIONAL)

- **Value:** Not found

**The field is deliberately empty: pyflct supports no data source.** The previously recorded
`Observatory/Mission-specific` was removed because it asserts a specificity the package does not have
and could not be completed as the form requires.

*The facts.* pyflct accesses no data source whatsoever. There is no network code, no archive client,
no download helper; `install_requires` is `numpy, packaging`. The user supplies two numpy arrays, or a
local `.dat` file path to `read_2_images`/`read_3_images`. Nothing in the package knows which
observatory produced the pixels.

*Why the previous value could not stand.* The form's instruction for Field 17 reads: `Select all data
input sources the software supports. If a source is not listed, select 'Other'. If observatory-specific,
select 'observatory-specific' and indicate the observatory/mission name in the Related Observatory
field.` Field 32 is empty here, and Fields 31/32 establish that it is correctly empty — the software is
instrument- and mission-agnostic. Selecting `Observatory/Mission-specific` while naming no observatory
left the record internally inconsistent by the form's own rule. Weighed from the searcher's side,
someone filtering on that value is looking for software that handles a particular mission's data
products; pyflct will not help them. That is the decisive argument.

*The alternatives, both rejected.*

- **Keeping `Observatory/Mission-specific`.** In practice FLCT is applied to observatory magnetogram
  sequences, so a solar physicist filtering on it would not be badly served. Rejected for the reason
  above: the claim asserts a specificity the package lacks and cannot be completed with an observatory.
- **Recording `Other`.** The form says to select `Other` when the source is not listed, and pyflct's
  actual input path — in-memory arrays and local FLCT `.dat` files — is not listed. Rejected because
  `Other` on this field conveys almost nothing to a searcher and slightly overstates the case: "local
  files the user already has" is arguably not a data *source* at all. (The same value is recorded on
  Field 15 for a different reason: there the licence is determined and merely unlisted, and `Other`
  keeps the entry in a facet it otherwise vanishes from. Here there is nothing to be unlisted.)

The accepted cost is that the entry appears in no data-source facet. That is the right outcome for a
package that genuinely supports none; an evidenced empty is a legitimate value here.

### 18. Input File Formats (RECOMMENDED)

- **Selected Values:**
  - Other

Retained. The library's only file input is the binary `.dat` format of the original FLCT C code, read
by `read_2_images` and `read_3_images`, whose docstrings describe reading two or three arrays of the
same size from a `dat` file. That format has no vocabulary row and is not a general interchange
format, so `Other` is exactly right.
The gallery example states the rationale plainly: the original FLCT C code uses `dat` files for input
and output, and these functions exist so that work stays compatible with the existing C
implementation.

**Explicitly not `csv`, and this needs to be recorded because the tree invites the mistake.**
`pyflct/data/test/` contains five `.csv` files and an `IDL.txt`. They are regression fixtures, not a
supported format: `pyflct/tests/test_flct.py` loads them with `np.genfromtxt(filepath1, delimiter=",")`, a numpy call in
the test suite, and no function in `pyflct` or `pyflct.utils` reads CSV. A later agent doing an
extension census will see the five `.csv` files; they are not evidence of CSV support.

Also not recorded: `FITS`. Users typically load solar images from FITS before calling `flct`, but they
do so with other software; pyflct neither imports a FITS reader nor mentions the format.

### 19. Output File Formats (RECOMMENDED)

- **Selected Values:**
  - Other

Retained, for the mirror-image reason. The only file output is the same binary `.dat` format, written
by `write_2_images` and `write_3_images`. Everything else the package produces is returned in memory
as numpy arrays, which the user may then save in whatever format their own tooling supports — that is
not a format pyflct supports.

### 20. Operating System (RECOMMENDED)

- **Selected Values:**
  - Linux
  - Mac
  - Windows

All three retained. `setup.cfg` classifies `Operating System :: MacOS`, `Operating System :: POSIX ::
Linux` and `Operating System :: Microsoft :: Windows`. Linux and macOS ship pre-compiled wheels on
PyPI (`README.rst`: `This will install the pre-compiled binary wheels for these two platforms.`).
Windows is supported through conda rather than pip — `README.rst` says
`We only officially support Windows through Conda.` and `docs/install.rst` gives
`$ conda install -c conda-forge pyflct` — and is corroborated by 47 `win-64` artifacts in the
conda-forge channel for this package (counted 2026-09-09 from the anaconda.org file listing, 193 files
total across `linux-64` 76, `osx-64` 70, `win-64` 47).

**A dated CI failure is not a reason to unseat Windows.** On the most recent workflow run on `main`
at the pin (2026-06-01) the `conda-windows` job concluded in failure, as did `conda-mac` — which
despite its name declares `runs-on: windows-latest`, so it is a second Windows job rather than a
macOS one (see the CI record below) — and, on the macOS side, the arm64 job. That is a 2026 CI state
observed on 2026-09-09, against a package last released in 2024; the distributed conda-forge
artifacts and the documented install path are the better evidence of what a user can install today,
and they are unambiguous for all three platforms.

**The retained CI record in full, because Fields 20, 21 and 23 all lean on it and it is easy to
misread.** GitHub retains 14 runs of `ci.yml`, this repository's only test workflow, spanning
2025-10-01 to 2026-07-06; that figure is from the workflow-scoped run listing for `ci.yml`, whereas the
repository-wide run listing reports 27, the difference being Dependabot's own update workflow. v0.3.1
was released on 2024-07-31, so no run from that release's era survives: CI evidence about the version a
user installs today is **unverified by this route, not absent**, and a later refresh must not read its
absence as a finding. Eleven of the 14 runs expanded the tox matrix; the other three, from 2026-07-01
and 2026-07-06, skipped or cancelled the downstream jobs. Across those eleven:

- `failing_mac_arm / py312 (macos-latest)` — Apple Silicon — **failed in all eleven**, and it really
  ran. In the 2026-06-01 run on `main` it was picked up by a live runner and completed checkout, the
  Homebrew FFTW install and Python 3.12 setup successfully before failing at the `tox -e py312` step.
- `tests / py311 (macos-12)` — Intel macOS — was **cancelled in all eleven**: never failed, never
  succeeded. In that same 2026-06-01 run it sat with no runner assigned for exactly 24 hours,
  `2026-06-01T14:24:26Z` to `2026-06-02T14:24:27Z`. That is the signature of a runner label nothing can
  claim, not a test result — GitHub's `macos-12` image became fully unsupported on 2024-12-03, and
  `ci.yml` still pins `runs-on: macos-12` for that environment at the pin.
- `conda-mac` **carries no macOS information whatsoever**, despite its name and the comment above it
  about checking that the package can be `installed and run on a Mac` without brew: at the pin the job
  declares `runs-on: windows-latest`. Its tallies match `conda-windows` exactly (11 failures, 1
  cancelled, 2 skipped across the 14 runs) because it is the same platform. A later reader must not
  count those failures as macOS evidence, in either direction.
- For contrast, `conda-linux` succeeded in all eleven.

`Operating System Independent` was considered and rejected: the package contains a compiled C
extension and requires a platform-specific FFTW build, so it is emphatically not OS-independent.

**`Mac` stands, and it is read together with Field 21's x86-64-only architecture list.** Linux and
Windows were never in doubt; Mac was, because the *kind* of support behind it has changed and this
field cannot express the difference on its own. The two fields carry the qualification jointly: macOS,
on x86-64 only.

*The facts.* Mac support is **artifact-only**. conda-forge ships 70 `osx-64` files and PyPI ships 23
macOS wheels across the seven releases — 17 `macosx_10_9_x86_64` and 6 `macosx_12_0_x86_64`, of which
three are in 0.3.1, one per supported Python (all counted 2026-09-09) — and `setup.cfg` carries the
`Operating System :: MacOS` classifier. Set against that, the CI record above contains **no macOS job
that concluded `success` in any retained run**: the Intel job is cancelled for a retired runner label
and never executes, the arm64 job executes and fails, and `conda-mac` is a Windows job. And every one
of those artifacts is Intel — `osx-64` and `macosx_*_x86_64` throughout, no `osx-arm64` anywhere —
while the Mac a visitor buys today is Apple Silicon, where the only tested outcome on record is failure
and where `docs/install.rst`'s Homebrew prefix is the wrong one (Field 21's fifth signal). Rosetta 2
would run an Intel wheel under an Intel Python build, but no source claims that, and it is not what a
visitor filtering on `Mac` is asking.

*Why this reading was chosen.* Keeping `Mac` here while Field 21 lists only `x86-64` makes the two
fields accurate when read together, and keeps the catalogue from dropping a platform the project
actively publishes for: a visitor on an Intel Mac or in an x86-64 conda environment is correctly
served. The accepted cost is that it depends on the visitor reading both fields — `Mac` on its own
still over-promises on a current Apple Silicon Mac.

*The alternatives, both rejected.*

- **Keeping `Mac` and also keeping `Apple Silicon arm64` in Field 21.** This would leave `Mac`
  unqualified. Rejected on Field 21's own evidence, set out in the next section: a tested, named,
  reproducible arm64 failure and no arm64 artifact published anywhere.
- **Dropping `Mac` from Field 20 as well as `Apple Silicon arm64` from Field 21.** The record would
  then assert only what is tested green, namely Linux plus Windows via conda. Rejected as too strict:
  it contradicts the project's own classifier and discards 70 published `osx-64` files and 23 macOS
  wheels, so a visitor who genuinely can install pyflct on a Mac would never find it. Absence of a
  green test is not evidence of failure — exactly the distinction Field 21 draws between the cancelled
  Intel job and the failing arm64 one.

### 21. CPU Architecture (RECOMMENDED)

- **Selected Values:**
  - x86-64

**`Apple Silicon arm64` is removed.** This is not a judgement call between defensible readings; four
independent lines of evidence point the same way, and none points the other. The form's criterion is
`Select all CPU architectures the software can successfully be installed and executed on` — evidence of
*success* is what it asks for, and for arm64 there is none.

1. The project deliberately does not build arm64 wheels. In `.github/workflows/ci.yml` the three arm64
   wheel targets are commented out — `#- cp310-macosx_arm64`, `#- cp311-macosx_arm64`,
   `#- cp312-macosx_arm64` — while their `macosx_x86_64` and `manylinux_x86_64` siblings are live. A
   `# Linux Arm` entry in the same file carries `# TODO: Workout how to add`.
2. No arm64 artifact has ever been published to PyPI. Across all 79 distribution files in the seven
   PyPI releases, filename matches for `arm64` or `aarch64` number 0; the positive control `x86_64`
   matches 60 (counted 2026-09-09 from the PyPI JSON API). Release 0.3.1 ships six wheels, all
   `macosx_12_0_x86_64` or `manylinux_2_28_x86_64`, plus an sdist.
3. conda-forge has no arm64 build either: of the 193 files listed on 2026-09-09, the subdirs are
   `linux-64`, `osx-64` and `win-64` only — no `osx-arm64`, no `linux-aarch64`.
4. Most tellingly, the project's own arm64 test job is *named for its failure*. `ci.yml` defines a job
   `failing_mac_arm:` whose only environment is `- macos: py312` on `runs-on: macos-latest` (an arm64
   runner) under the comment `# Mac Arm`. It concluded in failure in every one of the eleven retained
   CI runs that expanded the tox matrix, 2025-10-01 through 2026-07-06 — the record is set out under
   Field 20 — and it fails after really building, reaching the `tox -e py312` step with checkout,
   Homebrew FFTW and Python 3.12 setup all successful. A tested, named, reproducible failure is
   stronger evidence than an absent build.

**Cancelled and failed are not the same evidence, and the difference is what this field turns on.**
The Intel-macOS job (`tests / py311 (macos-12)`) is *cancelled* in every retained run because GitHub
retired the `macos-12` runner image; that is a fact about GitHub's hosted fleet and says nothing at all
about whether pyflct works on an Intel Mac. The arm64 job is *failed* in every retained run, having
actually executed on a live arm64 runner. Only the second is evidence about the software. So the
removal of `Apple Silicon arm64` rests on a tested failure, while the retention of `x86-64` rests on
published artifacts — points 2 and 3 above — rather than on a green test, because the retained record
contains no green macOS test of either architecture. A later refresh should not read the cancelled
Intel job as though it were a failure, nor read the absence of a green x86-64 macOS test as a reason to
unseat `x86-64`.

A fifth, smaller signal points the same way: the Mac source-install instructions in `docs/install.rst`
set `export LDFLAGS="-L/usr/local/lib"` and the matching `CFLAGS`, which is the Intel Homebrew prefix;
Apple Silicon Homebrew installs under `/opt/homebrew`, so the documented recipe does not work
unmodified on an arm64 Mac.

The counter-argument, stated so it is not re-litigated: a determined user could probably compile from
source on Apple Silicon after installing FFTW and fixing the paths. That is a claim about what might
work, not evidence that it does, and the project's own arm64 job says otherwise at the pin. If a later
refresh finds a green arm64 job, a published `osx-arm64` artifact, or a documented successful build,
the value should come back.

`x86-64` is retained on evidence 2 and 3 above (60 `x86_64` distribution files; `linux-64`, `osx-64`
and `win-64` conda builds are all x86-64). `Linux aarch64 or arm64` was considered and rejected — the
`# TODO: Workout how to add` comment is an unimplemented intention. `CPU Independent` is wrong for a
package with a compiled extension. `GPU`, `HPC or HEC`, `ppc64le` and `Sun (SPARC)` have no support of
any kind.

### 22. Related Phenomena (OPTIONAL)

- **Value:** Not found

**The field is deliberately empty: pyflct supports a technique, not a phenomenon.** The seven-row
vocabulary is flat, so this was a straight question about one value with no hierarchy to fall back on,
and the previously recorded `Solar Flares` was removed.

*The evidence against it.* No phenomenon term appears anywhere in the tracked tree: the sweep in the
scope note returns 0 files for `flare`, 0 for `CME`, 0 for `corona`. Neither the recorded description
nor the concise description mentions flares — the description names electric-field inversions,
data-driven coronal simulations, flux transport and space weather forecasting, but not flares. The
software computes a velocity field from two images; the connection to any phenomenon runs through
downstream consumers of that output, at least two steps away.

*The case that was made for it, and why it did not carry.* The reason photospheric flow measurement
matters scientifically is the build-up and release of magnetic energy in the corona, which is what the
algorithm papers are about: Welsch et al. 2004 recovers photospheric velocities to constrain energy
and helicity flux, and Fisher et al. 2020's PDFI_SS inversions exist to drive models of eruptive
events. A solar physicist filtering on `Solar Flares` for tools that support flare research would not
be astonished to find a flow-tracking wrapper. That was judged insufficient: it is a value no source
states directly, and none of the seven rows (`Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`, `X-ray emission`) names what the
software actually addresses. An evidenced empty is a legitimate outcome for this field, at the
accepted cost that the entry appears in no phenomenon facet.

*Also rejected — keeping `Solar Flares` and adding `Coronal Mass Ejections`*, as the 2025-12-02
extraction proposed (it also proposed `Solar Corona`). If the downstream-use argument is accepted at
all, CMEs have as good a claim as flares, since eruption modelling is the canonical use of PDFI_SS
electric fields. The argument was not accepted, so neither belongs.

The one position that was never defensible is keeping `Solar Flares` alone on the grounds that flares
are somehow better evidenced than CMEs — the evidence is identical for both, and that asymmetry was an
artifact of the earlier extraction rather than a finding.

### 23. Development Status (RECOMMENDED)

- **Value:** Inactive

The controlled term is `Inactive`, whose vocabulary definition reads: `The project has reached a
stable, usable state but is no longer being actively developed; support/maintenance will be provided
as time allows.` Every clause of that fits.

*Reached a stable, usable state.* v0.3.1 is released on PyPI and conda-forge, the documentation builds,
and the test suite is complete. This eliminates `Concept`, `WIP`, `Abandoned` and `Suspended`, all four
of whose definitions turn on there not yet being a stable, usable release.

*No longer actively developed.* The last commit by a human is `3e617cc`, dated 2024-07-31 — the v0.3.1
tag commit itself. Every one of the six commits between that tag and the pin is a bot
(`pre-commit-ci[bot]` four, `dependabot[bot]` two), the newest being the pinned commit on 2026-06-01.
That is two years and one month with no human change as of 2026-09-09.

*Support as time allows, rather than ceased.* The repository is not archived and not disabled
(`archived: false`, `disabled: false`, checked 2026-09-09), it carries 8 open issues, and its
automated dependency and lint updates are still landing. That distinguishes it from `Unsupported`,
defined as `The project has reached a stable, usable state but the author(s) have ceased all work on
it. A new maintainer may be desired.` — nothing anywhere states that work has ceased or that a
maintainer is wanted. `Moved` is excluded: the project has not relocated. `Active` is excluded by the
two-year gap in human commits.

**Two pieces of evidence the 2025-12-02 extraction used are not evidence for this field, and should
not be reused.** First, `setup.cfg`'s `Development Status :: 5 - Production/Stable` is a PyPI trove
*maturity* classifier — it describes how finished the software is, not whether the repository is being
developed, and a mature package that stopped receiving changes carries exactly that classifier.
Second, that extraction's other stated evidence was `last updated 2025-10-06 per SoMEF`. The date is
real, but the change it dates is `f9c14bc`, a `pre-commit-ci[bot]` pre-commit autoupdate — a
last-touched timestamp records the most recent push of any kind, bot pushes included, and is not a
measure of development activity. That the misreading is structural rather than a one-off is clear from
the same trap being set today by GitHub's `pushed_at` (`2026-07-06T21:06:12Z` here), which is likewise
a bot push. A maturity classifier and a bot-driven timestamp together produced the earlier `Active`,
which the commit record contradicts.

### 24. Documentation (RECOMMENDED)

- **Value:** https://pyflct.readthedocs.io/en/latest/

Retained, and it is better than the URL the package declares about itself.

Tested 2026-09-09: `https://pyflct.readthedocs.io/en/latest/` answers 200 with no redirect. The bare
`https://pyflct.readthedocs.io` — the value GitHub carries as the repository homepage and the value
the PyHC registry gives as `docs` — answers 200 after one redirect to the same page, so the stored
form is the redirect-free canonical one.

**The divergence worth recording:** the package's own declared documentation URL is dead. `setup.cfg`
has `url = https://docs.sunpy.org/projects/pyflct/`, and PyPI's only project URL is that same
`Homepage`; fetched 2026-09-09 it returns 404 with no redirect. So the most authoritative-looking
source — the package's own metadata — points at a page that does not exist, while the stored HSSI
value works. A later refresh reading `setup.cfg` will find that URL and may be tempted to "correct"
the record to it; do not. Re-test both before changing anything, since the sunpy documentation site is
not ours and its behaviour may change.

### 25. Funder (OPTIONAL)

- **Value:** Not found

Evidenced absent, not merely unfound. There is no funding information anywhere in this repository.

The sweep, so it need not be repeated: `git grep -c -i -- <term>` over the whole tracked tree at the
pin returns 0 files for `fund`, `funding`, `award`, `acknowledg`, `NASA` and `sponsor`. Two terms match
and neither is a funder. `grant` matches two lines, both inside the LGPL text in `LICENSE.rst`
(`nothing else grants you permission to modify or` and `restrictions on the recipients' exercise of the
rights granted herein.`). `NSF` matches seven lines across four files, every one a substring of an
ordinary word — `transferring` in the LGPL text, and `transfer`, `transform` or `transformations` in
`cextern/flctsubs.c`, `pyflct/sunkit.c` and `pyflct/flct.py`. Every matched line was read.

There is also no publication route to a funder for *this software*: pyflct has no paper of its own
(Field 14), and the acknowledgements of the algorithm papers fund the FLCT and PDFI_SS work at
Berkeley, not the Python wrapper. Attributing those awards to pyflct would misstate what was funded.

### 26. Award Title (OPTIONAL)

- **Value:** Not found

Follows directly from Field 25 — no funder is evidenced, so no award is. The same sweep covers both
(`award` matches 0 files).

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- **Selected Values:**
  - https://doi.org/10.1086/421767
  - https://arxiv.org/abs/0712.4289

Both retained. `docs/index.rst` introduces them with `The following papers are references for the FLCT
algorithm:`, so they are the project's own designated references, and together they define the method
the package implements: Welsch et al. 2004, `ILCT: Recovering Photospheric Velocities from Magnetograms
by Combining the Induction Equation with Local Correlation Tracking` (The Astrophysical Journal,
2004-08), and Fisher & Welsch 2008, `FLCT: A Fast, Efficient Method for Performing Local Correlation
Tracking` (PASP Conf. Ser. 383, 373). The 2008 paper has no DOI, so its arXiv abstract page is the
correct permanent link, exactly as the form prescribes for a DOI-less publication. `cextern/COPYRIGHT`
independently asks users of the C library to cite Welsch & Fisher (2008).

Two further candidates were weighed for this field and both were declined; the reasoning is written
out under Field 14 so it stays in one place. Fisher et al. 2020
(`https://doi.org/10.3847/1538-4365/ab8303`), the third of the algorithm references, is not recorded
here and was not moved into Field 14 either. The Springer apodizing-windows paper
(`https://doi.org/10.1007/s11207-015-0659-2`), which `docs/index.rst` lists separately under
`Other references you might find useful are:`, is not recorded here because it is explicitly not one
of the algorithm references and neither cites nor describes pyflct.

### 28. Related Datasets (OPTIONAL)

- **Value:** Not found

Examined, not assumed. The package ships no dataset and depends on none. The files under
`pyflct/data/test/` are small regression fixtures — `pyflct/data/README.rst` describes the directory
as holding data files shipped with the package's source distribution and intended only for relatively
small files — and they exist to pin numerical output, not to be analysed.

The tree's external references to `dat` data live in two different docstrings, and they are easy to
conflate. `flct`'s own docstring carries the note
`In the references there are some dat files which can be used to test the FLCT code.`, pointing the
reader at `pyflct.read_2_images` and `pyflct.read_3_images` as the way to read them; it gives no
location for those files, and the only URL anywhere in that docstring is the FLCT C user manual PDF on
`solarmuri.ssl.berkeley.edu`, cited in the limitations warning. The link to the FLCT project's own site,
`http://cgem.ssl.berkeley.edu/cgi-bin/cgem/FLCT/dir?ci=tip`, is in the `read_2_images` and
`read_3_images` docstrings instead, where it is cited as the source of the IDL IO routines rather than
as a place to obtain data. Either way what is pointed at is test input for the C code on a project web
page: no DOI, no landing page of the kind this field takes. Nothing else in the documentation names a
dataset, a mission data product, or an archive holding.

### 29. Related Software (OPTIONAL)

- **Selected Values:**
  - https://github.com/sunpy/sunkit-image
  - https://github.com/PyDL/pyflct

**One bar, applied in both directions.** An entry belongs here if it *distinguishes* pyflct — a
similar-purpose tool, the project this work came from, a companion, or a domain-specific dependency
whose presence characterises the software. An entry does not belong if the same sentence would be true
of an arbitrary package, or if the relationship is organisational rather than between the software.
The form states the same test both ways: `Important software dependencies and software this work was
forked from should also be included.` and `if the entry would be equally true of most Python packages,
it carries no information and does not belong.`

Where an entry names another catalogued item, its exact stored repository URL is used, because the page
renders a related item's raw URL as its link text.

**`https://github.com/sunpy/sunkit-image` — added.** pyflct's code was extracted from sunkit-image,
and both repositories document the move. In this repository, the single commit that brought in the
entire package — `43a6bd0`, 2020-04-04, which added `pyflct/flct.py`, `pyflct/flct.pyx`,
`pyflct/utils.py`, `pyflct/sunkit.c`, the vendored `cextern/` sources, the tests and both gallery
examples — has the body `Moved everything from sunkit-image to here.` On the same day, sunkit-image's
commit `1b4339e`, `removed flct (#47)`, states `moved flct to https://github.com/sunpy/pyflct` and
deletes the changelog fragment that had announced the addition of a `sunkit_image.flct` subpackage for
applying Fourier Local Correlation Tracking between two images. The FLCT subpackage had lived there
since 2019-11-30 (`cc6be6a`, `Flct (#36)`). This is precisely the predecessor relationship the field
asks for, it is evidenced in both directions and dated, and it tells a reader something true and
non-obvious about pyflct: it is a spun-out subpackage, not an independent project. (Verified against
GitHub on 2026-09-09; the sunkit-image evidence is in that project's git history rather than its
current released changelog, where the fragment no longer appears.)

**`https://github.com/PyDL/pyflct` — retained.** `docs/index.rst` links it under
`Other references you might find useful are:` with the label `Another version of pyflct`. It is an
independent Python wrapper for the same FLCT C library — GitHub describes it as
`Python wrapper for FLCT in C and IDL`, it is not a fork (`fork: false`), it was created 2017-12-07,
i.e. before this project, its primary language is C and it is GPL-2.0 licensed (all checked
2026-09-09). "Software that performs similar tasks but does not necessarily link together" is the
field's own definition and this is a textbook instance: a user choosing between the two is exactly the
reader this field serves.

**`https://github.com/sunpy/ndcube` — removed.** There is no relationship of any kind. `ndcube` has 0
matches in the entire tracked tree at the pin, case-insensitively: it is not a dependency, not
imported, not mentioned in the documentation, not in the intersphinx mapping. Nothing supports it and
nothing is lost by removing it.

**`https://github.com/sunpy/sunpy` — removed.** This is the harder call, so the argument is spelled
out. sunpy appears on 46 lines across 9 files at the pin, measured with a case-insensitive, unanchored
`git grep -i -- sunpy` over the whole tracked tree; word-anchored with `\b` it is 42 lines across the
same 9 files, the four-line difference being underscore-adjacent forms (`SUNPY_CONFIGDIR` and
`sunpy_sphinx_theme` in `docs/conf.py`, and two `pyflct/_sunpy_init*` coverage-omit patterns in
`setup.cfg`). Every one of those lines is project governance, packaging or documentation
infrastructure: the "Powered by SunPy" README badge, the `#sunpy:matrix.org`
chat link, links to the SunPy Developer's Guide, contributing guide and Code of Conduct,
`author = The SunPy Developers`, `author_email = sunpy@googlegroups.com`,
`url = https://docs.sunpy.org/projects/pyflct/`, the `sunpy-sphinx-theme` docs extra with
`html_theme = "sunpy"`, an intersphinx mapping, `known_astropy = astropy, asdf, sunpy` in the isort
configuration, `tox.ini` pulling sunpy's test package pins, and PR-URL templates. **There is no import
of sunpy anywhere in the package and sunpy is not a dependency** — `install_requires` is `numpy,
packaging`. sunpy does not perform local correlation tracking, pyflct was not forked from it, and it
is not a companion library designed to be used with it. The relationship is that both are maintained
by the same organisation, which is a fact about the projects' governance, not about the software; the
field's guidance names the ecosystem-membership argument as never sufficient on its own. Consistency
matters here: the same bar that admits sunkit-image on a documented code-extraction event is what
excludes sunpy on organisational affiliation, and it would be incoherent to keep sunpy while removing
ndcube, since the evidence for sunpy is a superset of nothing that ndcube lacks in kind.

**Considered and excluded outright:** numpy and packaging (the only runtime dependencies, both generic
infrastructure — being a dependency is not a relationship this field records), matplotlib (a docs
extra and gallery import), astropy, scipy, pytest-astropy, sphinx and the rest of the build and test
chain. Each would read identically for an arbitrary Python package.

### 30. Interoperable Software (OPTIONAL)

- **Value:** Not found

The bar for this field is a *demonstrated exchange* — a shared or converted data model, an
adapter API, a plugin relationship, a companion package, a cross-language bridge — and none is
documented for pyflct with any package.

**`https://github.com/sunpy/sunpy` — removed.** The reasoning under Field 29 applies with more force
here: there is no import, no dependency, no shared data model and no adapter. pyflct exchanges bare
`numpy.ndarray` objects, which is not interoperation with sunpy or with anything else in particular.
The 2025-12-02 extraction listed sunpy here with no sunpy-specific justification at all: that file's
Field 30 source line cites only the dependencies declared in `setup.cfg` and the examples' use of
numpy and matplotlib. Its ecosystem-membership and powered-by-SunPy-badge reasoning sits under its
Field 29, not here. Neither would clear this field's bar in any case — the field's guidance rules out
blanket ecosystem membership explicitly, and a dependency list is not an exchange.

**numpy and matplotlib — excluded, and this is not a close call.** Both were recorded in the
2025-12-02 extraction. numpy is the runtime dependency and matplotlib appears only in the docs extra
and gallery; both are generic infrastructure that would be equally at home in a web application or a
finance model, and "depends on numpy" is true of nearly every package in the catalogue, so it
distinguishes nothing.

**sunkit-image is deliberately not recorded here, despite a real signature match.** pyflct's `flct()`
returns three numpy arrays, named vx, vy and vm in its docstring; sunkit-image's
`sunkit_image/asda.py` exposes public functions — `generate_velocity_field(vx, vy, i, j, r=3)`,
`calculate_gamma_values(vx, vy, factor=1, r=3)`, `get_vortex_properties(vx, vy, edge_prop, image=None)`
— that consume exactly such a velocity field, typed as `numpy.ndarray` and described in their
docstrings as a velocity field with vx and vy components. So pyflct's output is directly usable as
asda's input, and that pairing is genuine.

It was judged insufficient for this field, whose bar is a *demonstrated* exchange. The pairing appears
in no documentation, example, test or API on either side: fetched 2026-09-09 from sunkit-image's
default branch, `sunkit_image/asda.py` contains 0 occurrences of `flct`, and no path in that
repository contains `flct`. The exchange is an inference from matching signatures, and matching numpy
array signatures is a weak standard — it would admit a great many pairs. The two modules did briefly
coexist in sunkit-image (the FLCT subpackage from 2019-11-30 until 2020-04-04; asda added 2019-12-22),
which is suggestive of intent but is not a documented interoperation. A concrete artifact — a doc
page, an example, a converter — would settle it, and a later refresh that finds one should add the
entry then. The relationship between the two projects that *is* evidenced, the code extraction, is
recorded under Field 29 instead.

### 31. Related Instruments (OPTIONAL)

- **Value:** Not found

An examined, evidenced empty rather than a blank. pyflct is instrument-agnostic in the strongest
sense: `flct(image1, image2, deltat, deltas, sigma, ...)` takes two bare arrays and three scalars — those
five are its only required parameters, everything after `sigma` having a default — and
nothing in the package reads an instrument's data, parses an instrument-specific format, applies a
calibration, or knows what produced the pixels. Under the field's relevance gate, an
instrument-agnostic tool supports none specifically, and the sanity check answers itself: a user
searching for tools that handle a particular instrument's data would not be helped by a library that
never sees it.

**The one instrument mention in the tree, and why it does not clear the gate.** A case-insensitive
`git grep -c -i` over the whole tracked tree for `SDO`, `SOHO`, `MDI`, `GONG`, `BBSO`, `Hinode`,
`IRIS`, `SOT`, `Solar Orbiter`, `SolO`, `Helioseismic`, `Solar Dynamics`, `observatory`, `spacecraft`
and `telescope` returns 0 files for every one of them; `PHI` and `mission` match only as substrings of
`Sphinx`, `geographical` and `permission`, and each matched line was read. `HMI` matches exactly one
line, in the vendored C library: `cextern/flctsubs.c:2778` reads
`/* Use the fact that in HMI Plate Carree, dellat and dellon are equal: */`. That is a numerical
assumption inside the Plate Carree code path — the path pyflct exposes through its `pc`, `latmin` and
`latmax` options — recording a property that happens to hold for HMI's remapped grids. It is a comment
in third-party code, not an HMI reader, an HMI-specific format, or an HMI calibration, and nothing in
pyflct's own documentation, API or tests mentions HMI or SDO. Under the gate, an implementation
convenience for a projection that one instrument's products happen to use is the
"optimized for / commonly used with" case, which is excluded. A later refresh that finds this line
should read it as the reason this field is empty by decision rather than by oversight; if that
judgement were ever reversed, the rows to use would be `HMI`
(`https://spase-metadata.org/SMWG/Instrument/SDO/HMI`) here and `Solar Dynamics Observatory`
(`https://spase-metadata.org/SMWG/Observatory/SDO`) in Field 32.

**The vocabulary was searched, and the emptiness is not a lookup failure.** Against the
InstrumentObservatory list (7,602 rows, every one carrying a `https://spase-metadata.org/` identifier;
re-derived 2026-09-09), each candidate term was matched case-insensitively across all four of the
`name`, `abbreviation`, `identifier` and `definition` columns with the word-boundary pattern
`(?<![0-9A-Za-z])<term>(?![0-9A-Za-z])`. Terms drawn from the technique's usual application returned
candidate rows — `HMI` 2 (1 instrument, 1 observatory), `SDO` 6 (5/1), `magnetograph` 6 (5/1),
`SOHO` 30 (24/6), `photosphere` 15 (14/1) — while `FLCT` and `correlation tracking` returned 0, and the
negative control `xylophonic` returned 0. So rows for SDO/HMI and its peers plainly exist and could
have been recorded; what does not exist is any evidence that pyflct is designed to support them.
Recording HMI because FLCT is often run on HMI magnetograms is exactly the "commonly used with"
association the gate excludes.

Note the search scope matters: a fetch that omits the `definition` column materially changes these
counts (with `definition` absent, `photosphere` drops to 0 and `SOHO` to 17), so any re-run must
request all four columns.

### 32. Related Observatories (OPTIONAL)

- **Value:** Not found

Empty for the same reason as Field 31, and examined against the same sweep, which returns
observatory-typed rows for every solar platform the technique is associated with — SDO 1, SOHO 6,
GONG 1, BBSO 2, Hinode 1, IRIS 3, Solar Orbiter 2, all re-derived 2026-09-09 — and no evidence that
any of them is supported. The
package is mission-agnostic: it neither reads a mission's data products nor implements any mission's
conventions.

This has a consequence for Field 17, and is the reason that field is empty: the form instructs that a
submitter selecting `Observatory/Mission-specific` as a data source should name the observatory here,
and there is no observatory to name.

### 33. Logo (OPTIONAL)

- **Value:** Not found

**Field 33 is deliberately empty: pyflct has no logo of its own.** There is exactly one image in the
tracked tree and it is the SunPy project's mark, not pyflct's.

*What the file is.* `docs/logo/sunpy_icon_128x128.png`, 5,623 bytes, a 128x128 8-bit RGBA PNG. Fetched
and inspected on 2026-09-09 at its commit-pinned raw URL, which answered 200 with content-type
`image/png` and 5,623 bytes, byte-identical (SHA-256) to the blob at the pin. Looked at, it is the
SunPy project's yellow sun-and-spiral mark. There is nothing pyflct-specific in it.

*Why it is a weak candidate beyond being generic branding.* Nothing at the pin references it. A
case-insensitive `git grep` over the contents of every tracked file for `sunpy_icon`, `docs/logo` or
`logo` returns zero matching files; `docs/conf.py` sets neither `html_logo` nor `html_favicon`, and
the gallery's default thumbnail uses `PNG_ICON` imported from the installed `sunpy_sphinx_theme` package rather than this
file. The file is not something the project chose for pyflct at all — it arrived in this repository in
`43a6bd0`, the same 2020-04-04 import commit that brought the code, and in sunkit-image it had been
added on 2019-11-30 by the very commit that created the FLCT subpackage. The PyHC registry entry for
pyflct — in the community list, `_data/projects.yml` — carried no `logo:` key when it was read on
2026-09-09, though
neighbouring entries such as pyglow do carry one, so the key's absence is a real gap rather than an
unused schema field. There is no external nomination either.

*Rejected — recording the SunPy mark.* It would have given the entry a recognisable image, and the
mark does correctly signal that pyflct is a SunPy-project package. It was rejected because it is the
parent organisation's branding on a package that has never presented it as its own, and a visitor may
reasonably read a displayed logo as the software's identity. A documented omission is the more honest
outcome. If that judgement were ever reversed, the value is the commit-pinned raw URL, which is 120
characters and so well inside the 200-character limit:
`https://raw.githubusercontent.com/sunpy/pyflct/250028870f1eee77c2cf0093916634c8a8e64558/docs/logo/sunpy_icon_128x128.png`
A branch-based URL must not be substituted for it: a branch reference breaks silently if the file is
renamed, moved or deleted, and this file is referenced by nothing, which makes it an unusually easy
candidate for silent deletion.

No other image exists to consider, and none should be invented.
