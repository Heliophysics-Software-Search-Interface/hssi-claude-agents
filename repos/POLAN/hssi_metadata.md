# HSSI Metadata Extraction Results

**HSSI Software ID:** 6f9282ed-25cc-41da-b2f5-0e7c4b686060
**Repository:** https://github.com/space-physics/POLAN
**Source Revision:** 23c00563c0906e024edd378e469a0310a37ce118
**Extraction Date:** 2026-09-08
**Validation Date:** 2026-09-08
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

POLAN is a **1980s Fortran 77 scientific program by J. E. Titheridge, repackaged for modern
toolchains by Michael Hirsch**. Almost every field below turns on keeping three distinct bodies of
evidence apart, because they disagree with each other and were written up to forty years apart:

- **Titheridge's original material** — `README.1ST` (his own message to POLAN users, dated
  `FEBRUARY 1988 (to March 1996)`), `Readme_polan.md` (the descriptive comments extracted from the
  Fortran listing), and the eight `.f` sources whose in-file change logs run from 1977 to 1996.
  This describes *the algorithm* and is the authority for authorship, method, and the reference
  literature.
- **Hirsch's packaging material** — `pyproject.toml`, `meson.build`, `src/meson.build`,
  `CMakeLists.txt`, `CMakePresets.json`, `src/polan/__init__.py`, `src/polan/tests/test_mod.py`,
  `.github/workflows/ci.yml`, `LICENSE`, `README.md`. This describes *the distributable* and is the
  authority for version, licence, platforms, build, and the Python API.
- **Legacy artefacts that ship but are not built** — `src/polplot.f`, `src/polrunew.f`,
  `examples/POLPLOT.EXE` (an MS-DOS executable), `examples/POLOUT.396`, `examples/POLOUTQ.396`
  (1996 output listings in ISO-8859 with CRLF line endings), and `examples/in.asc`. These are
  historical deposits. Neither build system references any of them, and `examples/in.asc` is
  referenced nowhere in the tracked tree at all. Where a field turns on a capability that exists
  only in this third class, the dossier says so explicitly (see Field 4).

The tracked tree at the pinned revision holds 28 paths: eight `.f` sources, two `.py` files, five
example data files plus one DOS binary, three documentation files, and the build/CI/licence files.
There is no `CITATION.cff`, no `codemeta.json`, no `.zenodo.json`, and no `.mailmap` — verified by
listing the whole tree and matching case-insensitively for `citation`, `zenodo`, `mailmap` and
`codemeta`, which returned nothing.

Several files the earlier dossier quoted — `setup.cfg`, `setup.py`, `.github/workflows/ci_unix.yml`,
`README.rst`, `RunPolan.py` — were **deleted before this revision**, in the 2026-06-22 packaging
overhaul. Any claim resting on them is re-derived here from the pinned tree, or explicitly dated to
the revision that carried it.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found

**Note:** POLAN has no DOI, and this is a well-controlled negative rather than an unsearched blank.
The repository contains no DOI badge, no Zenodo integration file, and no `CITATION.cff`. Three
independent search axes were used, because a repository-name-keyed check alone is structurally blind
to a manually uploaded deposit that never mentions the repository:

- **Creator-keyed (DataCite, 2026-09-08):** `creators.name:scivision` → 280 results, **none of
  which is POLAN** — `creators.name:scivision AND POLAN` → 0. The 280 were sampled and are all
  "GDL - GNU Data Language" Zenodo deposits, unrelated to Hirsch.
  `titles.title:POLAN AND creators.name:Hirsch` → 0; `creators.name:Titheridge` → 4, all
  ecoacoustics records by unrelated Titheridges (Helena Titheridge of UCL). Same-day positive
  controls on the same instrument: `titles.title:msise00 AND creators.name:scivision` → 3, free
  text `"space-physics/msise00"` → 14.

  **How the Zenodo restriction must be written, because getting it wrong inverts the evidence.**
  Restricting DataCite to Zenodo requires the request parameter `&client-id=cern.zenodo`. Written
  *inside* the query as `client:cern.zenodo` it is a dead instrument — it returns 0 for
  everything, including every one of the positive controls above. An earlier reading of this field
  recorded `creators.name:scivision` → 0 for exactly that reason, and the corrected figure makes
  the negative **stronger, not weaker**: a creator-keyed corpus of 280 deposits that contains no
  POLAN is real evidence of absence, whereas a 0 would only have meant the instrument could not
  see. A future agent must not read the higher number as a weakening of this field's "Not found".
- **Free-text / subject:** DataCite `POLAN ionosonde` → 0; `"space-physics/POLAN"` → 0;
  `titles.title:(polan AND ionogram)` → 0; `creators.name:scivision AND ionosonde` → 0;
  `creators.name:Hirsch AND ionogram` → 0. Zenodo searched directly for `polan`, `polan ionogram`
  and `Titheridge`: every hit was an unrelated record (a Coleoptera figure, a speech-pathology
  dataset, ecoacoustics), and none names this software. Zenodo control query `msise00` returned the
  space-physics deposit.
- **Old-name redirect:** the repository was created under `scienceopen/polan`. The history has
  exactly two root commits — `627669b` ("Initial commit") and `a80d4ed` ("init") — and the
  commit that merges them, `2b7ea96f`, carries the subject
  `Merge branch 'master' of github-scienceopen:scienceopen/polan`, which is what names the
  historical path. (Neither root commit carries that subject; the merge does.) On 2026-09-08 the
  GitHub API returned HTTP 301 for `scienceopen/polan` and 200 for `space-physics/POLAN`, so a
  deposit filed under the historical path would still be discoverable under the current one; none
  exists under either.

A negative must never rest on Zenodo's `related_identifiers.identifier` matching a bare repository
URL: an integration deposit records the `/tree/<tag>` URL, not the bare repository URL, so that
check reports a clean zero for software that does have a DOI.

Also searched and not found: a DOI for the **UAG-93 report** that documents POLAN (see Field 14).

### 3. Code Repository (MANDATORY)
https://github.com/space-physics/POLAN

**Source:** On 2026-09-08 the GitHub API reported `full_name` exactly as `space-physics/POLAN`
with `fork: false` and `default_branch: main`, so this is the canonical current location and not a
redirect target. The historical location `scienceopen/polan` still 301-redirected to it on that
date; the lowercase `space-physics/polan` spelling also resolves (GitHub owner/repo names are
case-insensitive), and the repository's own `pyproject.toml` writes the lowercase form in
`[project.urls]`. The mixed-case `space-physics/POLAN` is recorded because it is the form GitHub
itself reports as canonical and the form already stored.

### 4. Software Functionality (RECOMMENDED — treated as critical)
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Processing
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Forward-Fitting

**Source and reasoning.** Every value is written in the canonical `Parent: Child` form with a space
after the colon, and every child's parent is listed alongside it. Subcategory names are not unique
across the taxonomy — `Analysis`, `Processing` and `ML/AI` each occur under more than one parent —
so an unqualified name can silently bind to the wrong branch; each value below is therefore fully
qualified.

- **Data Processing and Analysis / : Analysis / : Processing.** POLAN's whole purpose is to turn a
  measured virtual-height/frequency table into a derived physical quantity. `src/polan.f` opens
  `      SUBROUTINE POLAN (N,FV,HT, QQ, FB,DIP, START, AMODE, VALLEY, LIST)` and is described in
  its own header as `c  A generalised POLynomial real-height ANalysis, for ionograms.  May 1986.`
  The supporting units are an analysis pipeline: `COEFIC`, `ADJUST` and `REDUCE` in `src/polsub.f`,
  `SETUP`, `SELDAT` and `STAVAL` in `src/polsin.f`, and `PEAK`, `TRACE`, `SOLVE`, `SUMVAL`, `GIND`
  in `src/polmis.f`.
- **Models and Simulations / : Empirical.** POLAN does not merely invert data; it supplies built-in
  empirical models for the regions the ionogram cannot see. `README.1ST` records
  `    The valley model built in to POLAN uses a valley width proportional to` the neutral scale
  height, and the `START` parameter is documented in `Readme_polan.md` as a model height at 0.5 MHz
  with recommended values derived from equations in `    Atmosph. Terr. Phys. 48, 435-446, 1986.`
  These are climatological relations fitted to observation, i.e. empirical models, not first-
  principles simulation.
- **Models and Simulations: Forward-Fitting — added in this refresh.** This is the value that best
  describes what POLAN actually computes and it was previously absent. POLAN forward-models the
  group retardation that a trial real-height polynomial would produce — the group refractive index
  is computed by `      FUNCTION  GIND (F, T)` in `src/polmis.f` and subtracted by
  `      SUBROUTINE   REDUCE  (FV, HT)` in `src/polsub.f` — then solves for the polynomial
  coefficients that best reproduce the observed virtual heights. `Readme_polan.md` states the fit
  explicitly: `calculated profile segment is a least-squares fit.` and
  `devn is the rms deviation (in km) of the fit to the virtual height data.` The layer peak is
  obtained the same way: `src/polmis.f` says
  `c  Get FC, SH  by least-squares fitting of a Chapman-layer expression`, and `Readme_polan.md`
  heads the step `###  SECTION 6. Least-squares fitting of a Chapman layer peak`, describing it as
  a fit `    peak, by an iterative fit to the real-height gradients at the last` few calculated
  points. Synthetic observable + parameter optimisation + inversion is precisely this category.
  Its parent `Models and Simulations` is already present, so no new parent is needed.

**Considered and rejected.**

- **Coordinate Transforms: Ionospheric** — rejected. This category is for conversions between
  ionospheric *coordinate systems* (AACGM, apex coordinates, magnetic local time, magnetic
  latitude). POLAN converts a measured quantity (virtual height at a plasma frequency) into a
  physical quantity (true height), which is an inversion, not a frame transformation. The magnetic
  dip angle and gyrofrequency enter as physical parameters of the propagation, not as a coordinate
  frame. No AACGM/apex/MLT construct appears anywhere in the tree.
- **Data Processing and Analysis: Data Reduction** — rejected. That category covers reducing data
  volume while preserving information: averaging, binning, downsampling, noise filtering. POLAN's
  `REDUCE` subroutine is a false cognate — it subtracts the group retardation contributed by the
  previously solved profile section, which is a physics step in the inversion, not a volume
  reduction. POLAN's output arrays are the same length as, or longer than, its input (it *adds*
  extrapolated topside points above each peak), so nothing is being reduced.
- **Models and Simulations: Physics-Based / First Principles** — rejected. A searcher filtering for
  physics-based models expects a simulation of a physical system. POLAN solves an inverse problem
  against measurements; the physics it contains (group refractive index, magneto-ionic effects)
  serves the inversion rather than constituting a model of the ionosphere.
- **Data Processing and Analysis: Data Access and Retrieval** — rejected. POLAN reads a local file
  path supplied by the caller; there is no archive client, no network code, no URL anywhere in the
  Fortran or Python sources.
- **Servers and Environments** and its subcategories — rejected. No container, no server, no
  parallelism (no MPI, no OpenMP directives) in the tree.

**`Data Visualization` and `Data Visualization: Line Plots` — dropped in this refresh.** HSSI held
both values before it; they go because POLAN as distributed cannot draw a plot.

The deciding argument is the searcher's. A user who filters HSSI for
`Data Visualization: Line Plots` is looking for something that will draw them a plot. POLAN cannot:
they would download it, find no plotting in the Python API and no plotting target in either build
system, and conclude the catalogue misled them. The evidence at the pinned revision:

- The only plotting code is `src/polplot.f`, which begins `      PROGRAM  POLPLOT`.
- It is in **neither** build system. `src/CMakeLists.txt` reads
  `target_sources(polan PRIVATE polrun.f polan.f polmis.f polsin.f polsub.f)`, and `src/meson.build`
  lists `polan.f`, `polmis.f`, `polsin.f`, `polsub.f`, `polrunsub.f`. `polplot.f` appears in
  neither list.
- It **cannot be compiled** as it stands. Compiling `src/polplot.f` with `gfortran -std=legacy` —
  the same permissive mode the project's own builds use — fails at line 27 with a type mismatch
  passing a `REAL(4)` to `IABS`. The same command compiles `src/polan.f` and `src/polrunew.f`
  cleanly, so the failure is specific to this file, not to the compiler mode.
- Its plotting entry points do not exist in the repository. `src/polplot.f` calls
  `      call plotn (n, fv, ht, 241.)` and `      call getcl(datin)`; searching every `.f` file for
  a `SUBROUTINE`/`FUNCTION`/`PROGRAM` declaration of `plotn`, `getcl`, `graf` or `grafit` returns
  nothing, and the complete list of the tree's sixteen program units contains none of them.
  `README.1ST` explains why: `The plotter calls are written for a 386/486 IBM PC, but their purpose`
  should be obvious, and `Or you can link POLPLOT with my graphics package, in GRAF.LIB.` — a 1990s DOS
  graphics library that was never part of this repository.
- Neither `README.md` nor `Readme_polan.md` — the two documents describing the software as it is
  distributed now — mentions plotting at all. Only `README.1ST`, Titheridge's 1988–1996 diskette
  notes, describes POLPLOT, and it prefaces the description with
  `    This program is not described in UAG-93.  It is used to plot the` virtual height data.

**The counter-argument, weighed and not taken.** The tracked tree really does contain a plotting
program and a compiled DOS binary of it (`examples/POLPLOT.EXE`, 179,988 bytes, identified by
`file(1)` as an MS-DOS executable), and the software historically plotted profiles. Keeping the two
values on that basis would make them describe the distribution's archived contents rather than its
working capability, which is not what a searcher reads this field as promising. That is the reason
the historical evidence, though genuine, does not carry the values.

Nothing else in the tree produces a figure: `src/polan/__init__.py` imports only `numpy` and
`pathlib`, and returns a plain dictionary of lists.

### 5. Related Region (RECOMMENDED — treated as critical)
- Earth Atmosphere
- Earth Ionosphere
- Earth Thermosphere

**Source and reasoning.** `Earth Ionosphere` and `Earth Thermosphere` are both added in this
refresh; HSSI held only the coarse `Earth Atmosphere` before it.

**`Earth Ionosphere`.** POLAN is an ionospheric instrument-analysis program in the most literal
sense available: `pyproject.toml` describes the
package as `description = "Model of Earth ionosphere true height"`, `Readme_polan.md` opens
`for the calculation of real-height profiles from sweep-frequency` ionograms, and the output
quantities are the E, F1 and F2 layer critical frequencies and peak heights. While the record
carried only `Earth Atmosphere`, a user filtering HSSI for `Earth Ionosphere` — the obvious filter
for this software — did not get it back.

The Region vocabulary is **flat**: parent/child links exist on the rows but are empty, so a coarse
value never implies a fine one and a fine value never implies its coarse parent. "Earth Atmosphere
encompasses the ionosphere" is therefore not an argument for leaving the fine value off.
`Earth Atmosphere` is nonetheless **kept** rather than replaced, following the 2026-09-03 precedent
of retaining a coarse region alongside the specific ones: a user browsing the broad atmospheric
category should still find this software, and dropping the stored value would remove them from that
view for no gain.

**`Earth Thermosphere` — added on the deciding evidence below, over a real objection that was
considered and judged not determinative.** This one was close, and both sides are recorded so a
later refresh can see that the objection was weighed rather than overlooked.

The deciding evidence for including it:

- the project declares the domain itself — `pyproject.toml` carries
  `keywords = ["ionosphere", "thermosphere"]`, and the retired `setup.cfg` declared the same pair,
  so this is the maintainer's own two-word statement of the software's domain, not an inference;
- POLAN's valley model is driven by the *neutral* scale height, which is a thermospheric quantity;
- its profiles routinely span 90–400 km, which lies entirely inside the thermosphere.

**The objection, recorded because it is sound and must not be mistaken for something that was
missed.** POLAN produces no neutral-atmosphere quantity. Its outputs are electron densities,
critical frequencies and ionised-layer peak heights; the neutral scale height enters only as an
internal empirical relation. A user filtering `Earth Thermosphere` in search of neutral thermosphere
models and data will find an ionogram inversion program somewhat out of place. That argument is
factually correct and was not refuted — it was judged not to outweigh the project's own explicit
domain declaration and the altitude range POLAN actually works over. A future agent who rediscovers
this argument should understand it as already counted, not as grounds to reverse the value.

`Earth Lower and Middle Atmosphere` was considered and rejected: POLAN's model start heights reach
down to about 80–90 km, which grazes the mesopause, but the software neither measures nor models
anything below the ionospheric D/E boundary. No non-terrestrial or solar region applies.

### 6. Authors (MANDATORY)

**Author 1:**
- **Author Name:** J. E. Titheridge
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** University of Auckland
  - **Affiliation Identifier:** https://ror.org/03b94tp07

**Author 2:**
- **Author Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493
- **Affiliation 2:**
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found

**Source and reasoning.** The author list is the union of the existing HSSI record, the prior
dossier, and the repository; nobody appears in any source who is not listed here. There is no
`CITATION.cff`, `.zenodo.json`, `codemeta.json` or `AUTHORS` file to reconcile against — verified
against the complete tracked tree at the pin.

**Titheridge has zero commits, and that is not evidence against his authorship.** `git shortlog -sne`
over the commits reachable from the pin returns eight distinct identities and every one of them is a
Michael Hirsch form (`Michael Hirsch, Ph.D <scivision@users.noreply.github.com>`,
`michael <hirsch617@gmail.com>`, `scivision <scivision@users.noreply.github.com>`,
`scivision <10931741+scivision@users.noreply.github.com>`,
`Michael <10931741+scivision@users.noreply.github.com>`,
`Michael Hirsch <scivision@users.noreply.github.com>`,
`Michael Hirsch, Ph.D <10931741+scivision@users.noreply.github.com>`,
`Michael Hirsch, Ph.D <scienceopen@users.noreply.github.com>`) — eight labels for one person,
resolved individually rather than assumed. Titheridge's Fortran predates the repository by three
decades, so no commit could carry his name.

What settles the authorship question is **where the credit entered**. Tracing the string
`Titheridge` through the history of the metadata and documentation files shows it arrived in the
very first content commit, `a80d4ed` (2017-03-07), simultaneously in `README.rst` and `README.1ST`.
That commit's `README.rst` carried an explicit `:author: J. E. Titheridge` line. This is deliberate
attribution at creation by the packager, not a name that drifted in later, and it has been present
continuously ever since; at the pin `Titheridge` appears in exactly two files, `README.1ST` and
`README.md`, the latter now reading
`POLAN is a classic Fortran program by J. E. Titheridge used to calculate real-height` profiles.

The **University of Auckland** affiliation is Titheridge's own signature block in `README.1ST`:
`                                Physics Department` /
`                                University of Auckland` / Private Bag 92019, Auckland, New Zealand,
with `email:  J.TITHERIDGE@auckland.ac.nz`. The ROR `https://ror.org/03b94tp07` resolves to the
University of Auckland.

**No ORCID exists for J. E. Titheridge.** A fielded ORCID search on
`given-names:J* AND family-name:Titheridge` returns 0; a family-name-only search returns three
people (Grant, Laura, and Helena Titheridge of UCL), none of whom is the Auckland ionospheric
physicist. The control search `given-names:Michael AND family-name:Hirsch` returned seven records
including the one stored here, so the instrument was working. A future agent should not re-propose
an ORCID for him. Separately, and independently of whether one is ever found: sending an ORCID for
this author through a routine metadata update would **not** annotate the existing identifier-less
person record — it would create a second person record and leave the original orphaned. Any
correction to Titheridge's identifier must be applied directly to the person record itself, not
through a routine metadata update.

**Michael Hirsch's ORCID `0000-0002-1637-6526`** is confirmed against the public ORCID record: the
name is Michael Hirsch and the single employment entry is Boston University, department `ECE`, role
Research Scientist, start 2018-08, with no end date. `https://ror.org/05qwgg493` is Boston
University's ROR.

**Scivision, Inc. has no ROR, and this was checked.** The `LICENSE` at the pin reads
`Copyright (c) 2017, 2026 SciVision`, so the organisation is real and current. The only ror.org match
for a query of `SciVision` is `https://ror.org/011qev639`, "SciVision Biotech Inc. (Taiwan)", a
Kaohsiung biotechnology company with domain `scivision.com.tw` — an unrelated organisation that must
**not** be attached to this author. The affiliation is therefore correctly stored without an
identifier. Note also that an organisation record, once created, cannot be renamed through any API
path, so a wrong identifier here would be permanent.

### 7. Software Name (MANDATORY)
POLAN

**Source:** The name POLAN is used by every source: the GitHub repository name, `README.md`'s title,
the subroutine name declared on the first line of `src/polan.f`, and the PyHC registry entry. It is
an acronym, expanded in `Readme_polan.md`'s title as "POLynomial ANalysis subroutine". The uppercase
form is correct and is what is stored.

Note for anyone reconciling packaging metadata: `pyproject.toml` declares the *distribution* name in
lowercase — `name = "polan"` — and the importable module is `polan`. That is a Python packaging
convention (PyPI names are normalised to lowercase) and is not an alternative software name.

### 8. Description (MANDATORY)
POLAN is a classic Fortran program used to calculate real-height profiles from chirp ionosonde data from the ionosphere. The software performs polynomial analysis (POLynomial ANalysis) on sweep-frequency ionograms to determine the true height distribution of ionospheric electron density from virtual height measurements. Originally developed by J.E. Titheridge in the 1980s and documented in UAG-93 report, the code has been updated to compile on modern PCs. The program supports multiple analysis modes including overlapping polynomials and single-polynomial fits, handles both ordinary and extraordinary ray data, and includes sophisticated modeling of ionospheric valleys and Chapman layer peaks.

**Source and reasoning.** This is the stored description, retained unchanged. Every factual claim in
it is supported by the pinned tree, so there is no evidence-based reason to rewrite it, and a purely
stylistic rewrite would discard a prior submitter's deliberate wording:

- the opening sentence is the project's own `README.md` sentence, which reads
  `POLAN is a classic Fortran program by J. E. Titheridge used to calculate real-height` profiles
  from chirp ionosonde data from the ionosphere;
- the UAG-93 attribution is in `README.1ST`, which points to full details
  `in a 200-page report "Ionogram analysis with the generalised program POLAN".`;
- "updated to compile on modern PCs" restates `README.md`'s statement that the POLAN code was
  updated to compile on modern PCs;
- the analysis modes are `Readme_polan.md` sections D.1 (ten standard modes, overlapping
  polynomials) and D.2 (single-polynomial modes);
- ordinary/extraordinary ray handling and the valley and Chapman-peak models are documented
  throughout `Readme_polan.md` sections A, B and E.

**One caveat recorded deliberately rather than corrected.** "chirp ionosonde data" is narrower than
what POLAN accepts: the software analyses *any* sweep-frequency ionogram, and `Readme_polan.md`
frames it that way. The phrase is the project's own README wording, and the sentence that follows in
the description already says "sweep-frequency ionograms", so the description is not misleading. A
future refresh should not treat "chirp" as an error to fix without a decision from the maintainer.

### 9. Concise Description (OPTIONAL)
Titheridge's POLAN for estimating true ionosphere height from ionosonde measurements using polynomial analysis of sweep-frequency ionogram data.

**Source and reasoning.** Retained unchanged. It is an expansion of the repository's own GitHub
description, `Titheridge's POLAN for estimating true ionosphere height from ionosonde`, and of the
PyHC registry description `estimate true ionosphere height from ionosonde`. It is accurate,
attributes the original author, and names the method. No change is warranted.

### 10. Publication Date (RECOMMENDED)
2017-03-07

**Source:** Verified two ways. The earliest commit reachable from the pin is `627669b`
("Initial commit", `2017-03-07 13:49:12 -0500`), and the GitHub API reports
`created_at: 2017-03-07T18:49:11Z` — the same instant to within a second. The repository has two
root commits: `627669b` (the GitHub-created `.gitignore` and `LICENSE`) and `a80d4ed`
(`2017-03-07 14:04:59 -0500`, the import of Titheridge's original `POLAN.FOR` and siblings), merged
together fifteen minutes apart on the same day. Either root gives 2017-03-07.

This is the publication date of the *repackaged* software, not of Titheridge's original program,
which circulated on diskette from the 1980s and has no publication date recoverable in a form this
field can hold.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

**Source:** Unchanged. The software is distributed from GitHub and nowhere else. There is no PyPI
distribution (see Field 12), no conda package, no institutional download page, and no DOI-issuing
archive holds it (Field 2).

### 12. Version (RECOMMENDED)
- **Version Number:** 1.1.0
- **Version Date:** 2026-06-22
- **Version Description:** update to the current best practice in compiled Python modules - meson-python
- **Version PID:** Not found

**Source and reasoning.** The stored version was `1.0.0` with the description "Version declared in
setup.cfg package metadata" and no release date. Both the number and its stated source are now
stale: `setup.cfg` was deleted from the repository in the 2026-06-22 packaging overhaul (commit
`3f4aa86`), and at the revision immediately before its deletion it declared `version = 1.0.0` — so
the stored value was correct when recorded and has simply been superseded.

Four independent in-tree and out-of-tree sources agree on `1.1.0`:

- `src/polan/__init__.py` declares `__version__ = "1.1.0"`;
- `meson.build` declares `  version: '1.1.0',` (`pyproject.toml` declares
  `dynamic = ["version"]`, so Meson is the single source of truth for the packaged version);
- the repository's **only** tag is `v1.1.0`, and it points at `23c0056` — the pinned revision
  itself. `git ls-remote` confirms `origin/main`, `refs/tags/v1.1.0` and remote `HEAD` all resolve
  to that same SHA;
- the GitHub API lists exactly one release, `v1.1.0`, not a draft and not a pre-release.

**Anomaly shape: declared, tagged and released — but never distributed.** POLAN has never been
published to PyPI: on 2026-09-08 `https://pypi.org/pypi/polan/json` returned 404, as did the case
variant `POLAN` and the plausible alternative spellings `py-polan` and `pypolan`, while the control
`https://pypi.org/pypi/msise00/json` returned 200, so the check could see a real package. The only
distribution name the project has *ever* declared is `polan` — both the current `pyproject.toml`
and the retired `setup.cfg` used it — and `polan` is already its own PEP 503 normalised form, so
there is no further spelling to test. (The PyPI HTML project page must not be used for this check:
it is behind a bot gate that returns HTTP 200 even for names that do not exist. Only the JSON API
answer is meaningful.)

**Prefix.** The tag is written `v1.1.0`; `__version__`, `meson.build` and the retired `setup.cfg`
all write the bare `1.1.0`; and the stored HSSI value was the bare `1.0.0`. The unprefixed form is
therefore both the project's own convention for the version *string* and the catalogue's existing
convention for this record, so `1.1.0` is recorded. The `v` in `v1.1.0` is a git tag-naming
convention, not part of the version.

**Date.** The GitHub release was published at `2026-06-22T20:00:58Z` and the tagged commit is dated
`2026-06-22 14:58:24 -0500` (= 19:58:24Z). Both fall on 2026-06-22, so there is no timezone
ambiguity to resolve.

**Description.** Taken verbatim from the GitHub release **body**. The considered alternative was the
release `name`, the shorter `use meson-python packaging`; the body was chosen over it because the
field asks for a brief summary of the major changes, and the body says what changed and why while
the name says only that something was repackaged. Both were read — projects differ in which of the
two carries the substance, and here it is the body. This is recorded as a deliberate choice between
two available strings so that a later refresh does not mistake the shorter release name for an
obvious correction.

**Version PID:** none exists; see Field 2.

Replacing the version number creates a new version record and leaves the previous one
unreferenced. That is a known catalogue-level consequence of changing this field and not something
a routine metadata update can avoid.

### 13. Programming Language (RECOMMENDED)
- Fortran77
- Fortran90
- Python 3.x

**The criterion, stated once.** This field has a history of being reopened because two different
criteria can be applied to it and each defends a different answer. The criterion used here is the
one the submission form itself states: the field asks for *the languages most important for the
software* and says explicitly that it **is not meant to be an exhaustive list**. So a language
edition is listed when it **characterises a body of code a user would read, build or maintain** —
not when an isolated construct from that edition happens to appear somewhere in the tree, and not
merely because it is the newest edition any single line requires. Every inclusion and every
exclusion below is derived from that one criterion.

**Inclusions.**

- **Fortran77** — the algorithmic core. Eight `.f` files, no `.f90` files; GitHub's language
  breakdown reported Fortran at 110,118 bytes against 1,616 bytes of Python. The code is fixed-form
  with column-7 statements, `c`-column comments, `COMMON` blocks
  (`      COMMON /POL/ B(99,20),Q(20), FH,ADIP, MODE,MOD, FA,HA, tcont,lbug`), `DATA` statements
  and specific intrinsics. Titheridge states the standard himself in `README.1ST`:
  `    AUGUST 1987:  All programs are compatible with the FORTRAN 77 standard,`
  `using SAVE statements to remember constants in the subroutines STAVAL, SOLVE` and `GIND`. The
  change log in `src/polan.f` records the same event: `c  8'87  to fully FORTRAN77.   9'86 correct
  valley calcn at mode 1.`
- **Fortran90** — the modernised interfaces. `src/polan.f` now declares its arguments with
  attribute syntax, e.g. `      integer, intent(inout) :: N`, and `src/polrun.f` and
  `src/polrunsub.f` use named DO constructs (`      outer: do`) and the `date_and_time` intrinsic.
  These are the parts a maintainer touches.
- **Python 3.x** — the installable interface. `src/polan/__init__.py` exposes
  `def gopolan(infn: Path | str) -> dict:`, `src/polan/tests/test_mod.py` exercises it under
  pytest, and `pyproject.toml` sets `requires-python = ">=3.10"` and the classifier
  `Programming Language :: Python :: 3`. The CI runs the Python package on 3.10 and 3.14.

**Exclusions, derived from the same criterion.**

- **Fortran 2003** — excluded, although constructs from it are genuinely present and required. They
  are isolated to two driver files: `src/polrun.f` line 17 declares
  `      character(:), allocatable :: datin` (deferred-length allocatable character) and calls
  `get_command_argument`, and `src/polrunsub.f` line 18 declares `      integer, value :: list`
  (the VALUE attribute). Verified differentially with minimal single-feature controls: each fails
  under `gfortran -std=f95` with a diagnostic naming Fortran 2003 and compiles cleanly under
  `-std=f2003`. `src/polrun.f` as a whole fails under `-std=f95` and compiles clean under
  `-std=f2003`.
- **Fortran 2008** — excluded on the same ground, and this is the sharpest case. Exactly one
  construct in the entire tree requires it: `src/polrunsub.f` line 31,
  `      OPEN (newUNIT=u, FILE= datin, STATUS='OLD', action='read')`. The differential is clean and
  isolated — a minimal `newunit=` control errors under both `-std=f95` and `-std=f2003` with
  "Fortran 2008: NEWUNIT specifier" and compiles under `-std=f2008`, while an otherwise identical
  `unit=11` control compiles under all three; and `src/polrunsub.f` itself compiles cleanly
  under `-std=f2008`, so `newunit=` is its only remaining post-F95 requirement rather than merely
  its first diagnostic.
- **Fortran 2023** — excluded; no construct from it appears.
- **C** — excluded, and this exclusion is deliberate rather than an oversight. `meson.build`
  declares the project languages as `  ['c', 'fortran'],`, but there is not one `.c` file in the
  tracked tree. The C that gets compiled is generated at build time by `numpy.f2py` plus NumPy's
  own `fortranobject.c`, pulled from the installed NumPy include directory. None of it is authored
  or maintained here.
- **IDL, MATLAB, Julia, C++, and the rest of the vocabulary** — excluded; absent.

**A durable fact worth keeping even though it does not change the value.** No part of POLAN
compiles under a strict ISO standard mode. Both build systems pass `-std=legacy` to GFortran
(`CMakeLists.txt` has `  add_compile_options(-std=legacy)` and `meson.build` adds the same argument
for the `gcc` compiler id), and this is necessary: `src/polan.f`, `src/polsin.f`, `src/polmis.f` and
`src/polplot.f` each fail under `-std=f2003` and `-std=f2008` on GNU extensions and legacy
constructs, not on standard-edition features. Anyone building POLAN needs a compiler with a
permissive legacy mode, and — because of the two driver files above — one that also accepts Fortran
2008's `newunit=`. That is a build requirement, recorded here so it is not lost; it is not a
"language most important for the software".

**The two rival criteria, considered and rejected.** Both were worked out in full before
"languages that characterise the code" was settled on as the governing rule, and both are recorded
here so this field is not reopened a third time on reasoning that has already been done.

- **"Every edition with a required construct present."** This yields `Fortran77`, `Fortran90`,
  `Fortran 2003`, `Fortran 2008`, `Python 3.x` — two values more than are recorded. Its merit is
  real, and the constructs it rests on are verified rather than speculative: the F2003 and F2008
  evidence documented above (`src/polrun.f` line 17, `src/polrunsub.f` lines 18 and 31) was
  confirmed with differential single-feature controls. It would also encode a genuine build
  requirement in a machine-readable field rather than in prose. It is rejected because it
  contradicts the form's own "not meant to be an exhaustive list" instruction and would put a
  forty-year-old fixed-form program into the modern-Fortran filters on the strength of one
  `newunit=` specifier.
- **"The highest edition required."** This yields `Fortran 2008` plus `Python 3.x` alone and drops
  `Fortran77`, removing POLAN from the one language filter where it is the archetypal result.
  Rejected for that reason.

The governing criterion is **stored-outcome-identical**: it produces exactly the three values the
catalogue already held, so settling it changed no value in this field. What it changed is that the
rule and the two rejected criteria are now written down. From the searcher's side it is also the
friendlier answer — a user filtering `Fortran77` is delighted to find POLAN, whereas a user
filtering `Fortran 2008` expecting a modern Fortran codebase would not be.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1029/rs023i005p00831

**Full citation:** Titheridge, J. E. (1988). "The real height analysis of ionograms: A generalized
formulation." *Radio Science*, 23(5), 831–849.

**Source and reasoning.** This field was empty in HSSI before this refresh. The software's own
documentation nominates this paper: `README.1ST` introduces it with
`A general discussion of the POLAN approach is given in` followed by
` Titheridge, J.E. (1988).   "The real height analysis of ionograms:` /
`   A generalised fomulation",  Radio Science 23(5), 831-849.` It is the one paper Titheridge
singles out as describing the POLAN method as a whole, as distinct from the five he lists
afterwards as covering individual procedures (those are Field 27).

**The previous "no DOI" claim was wrong.** The earlier dossier asserted that the Titheridge papers
"lack DOIs". Every one of them has a DOI. Crossref resolves this paper as DOI
`10.1029/rs023i005p00831`, *Radio Science* 23(5), 831–849, dated 1988-09, sole author
Titheridge, J. E. A nonsense control query on the same endpoint returned 0 results, so the search
was discriminating rather than permissive. The 1980s AGU and Elsevier back catalogues were
retro-registered with DOIs; "old paper, therefore no DOI" is not a safe inference and should not be
repeated.

**Note on spelling.** `README.1ST` spells the title "A generalised fomulation" — British spelling
plus a typo. The publisher's registered title uses the American "generalized"; the citation above
follows Crossref, which is what the DOI resolves to.

**UAG-93 considered and rejected as the Field 14 value.** The definitive documentation of POLAN is
the World Data Center report `UAG-93`, "Ionogram analysis with the generalised program POLAN" by
J. E. Titheridge, University of Auckland, December 1985 — a 194/200-page report (`README.1ST` says
200 pages, `Readme_polan.md` says 194). It has **no DOI**. Searched: Crossref by exact title (no
match; the query degraded to unrelated full-text hits), ADS by exact title (0 results), ADS
`full:"UAG-93" AND full:POLAN` (matches only third-party papers that cite the report, never the
report itself), and DataCite for both the exact title and the bare string `"UAG-93"` (0 each).
This field accepts only a DOI, so the report cannot be recorded here. The `README.md` links to an
archived HTML copy at
`https://web.archive.org/web/20231111062759/https://sws.bom.gov.au/IPSHosted/INAG/uag_93/uag_93.html`;
that is a web-archive snapshot, not a persistent identifier, and is not recorded as a field value.

### 15. License (RECOMMENDED)
- **License:** MIT License

**Source and reasoning.** This field was empty in HSSI before this refresh, and the evidence is
unambiguous. The `LICENSE` file at the pin opens with the line `MIT License` and carries the
standard MIT permission text; the GitHub API reports `spdx_id: MIT`; `pyproject.toml` declares
`license-files = ["LICENSE"]`. `MIT License` is the exact spelling of the controlled-vocabulary row.

**Licence history — checked properly, by reading the file's content at each commit that changed it,
not by looking for an "added" event.** `LICENSE` has been touched by exactly two commits reachable
from the pin: `627669b` (2017-03-07, the initial commit) and `da1aa9d` (2026-06-22). Diffing the two
versions shows a **single changed line** — the copyright holder went from
`Copyright (c) 2017 Michael Hirsch, Ph.D.` to `Copyright (c) 2017, 2026 SciVision`. The MIT
permission and warranty text is byte-identical across both. So the repository has been MIT-licensed
from its first day and has never been relicensed.

**A durable provenance caveat.** The MIT licence covers Hirsch's repackaging. Titheridge's original
Fortran was distributed on diskette with `README.1ST` (dated February 1988 to March 1996), which
carries no licence statement of any kind; his own framing is
`    POLAN is now being used by many different groups, under many different` conditions, and he asks
users to keep him informed. The repository asserts MIT over the whole tree and that is what the
catalogue records, but a future agent should not be surprised to find no upstream licence grant
behind it.

**Do not add a "License URI".** The prior dossier recorded `https://opensource.org/licenses/MIT` as
a License URI. That is not a per-software value: the software's licence is a reference to a shared
licence record, and the URL lives on that shared record, not on this entry. Recording one here
produces a field that cannot be stored. The repository `LICENSE` file is cited above as *evidence*
only.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- electron density
- hmF2
- ionogram
- ionosonde
- ionosphere
- ionosphere_thermosphere_mesosphere
- ionospheric sounding
- NmF2
- polynomial analysis
- real-height analysis
- sweep-frequency

**Source and reasoning.** Eleven values are recorded. Nine of them HSSI already held before this
refresh, `hmF2` and `NmF2` are added, and one keyword the record previously carried — `specific` —
is dropped. All eleven are written in their **stored spelling** rather than the title-cased form the
public view renders (`Electron Density`, `Ionosphere_Thermosphere_Mesosphere`, and so on). Keyword
lookup is case-insensitive, so a case variant would not be a mismatch, but the spellings above are
the ones the vocabulary rows themselves carry, and every one of the eleven was confirmed to exist as
an exact row. Keywords are the one open vocabulary in HSSI — an unmatched value silently creates a
new row — so nothing is written here that was not first confirmed to exist.

Eight of the nine carried-over values are straightforward domain descriptors, each supported by the
tree: `ionogram`,
`ionosonde`, `ionosphere` (also the repository's only GitHub topic), `ionospheric sounding`,
`sweep-frequency` (`Readme_polan.md`: `for the calculation of real-height profiles from
sweep-frequency` ionograms), `real-height analysis`, `polynomial analysis` (the acronym expansion),
and `electron density`.

**Two additions in this refresh: `hmF2` and `NmF2`.** Both already exist as rows in the keyword
vocabulary, so neither creates anything. Both are exactly what POLAN computes and are the terms an
ionospheric researcher would actually search on. The peak height and critical frequency of the
final layer are POLAN's headline output: `Readme_polan.md` states
`The peak of the last layer is at FC = fv(N-3), Hmax = ht(N-3).`, and the shipped
`examples/out.dat` reports, for the F layer of its first test case,
`PEAK  6.999 (0.009) MHz,  Height 250.1 ( 0.4) km.` — that is hmF2 and, through the plasma-frequency
relation, NmF2. `Readme_polan.md` also defines the slab thickness as the sub-peak electron content
divided by the peak density, so the peak density is a first-class output too. A user searching HSSI
for `hmF2` who did not get POLAN back would be poorly served.

**The two PyHC registry tags, split deliberately: one kept, one dropped.** Neither
`ionosphere_thermosphere_mesosphere` nor `specific` is a description anyone wrote about POLAN; both
are the PyHC project registry's own taxonomy tags, and HSSI carried both before this refresh. The
registry's `_data/projects_unevaluated.yml` entry for POLAN reads
`keywords: ["ionosphere_thermosphere_mesosphere","specific"]`, and the identical pair appears on
several unrelated entries in the same file — Maidenhead (a grid-square coordinate converter) and
PyMap3D (a general 3D coordinate library) among them — which shows the tags propagate by registry
convention rather than by domain fit. That propagation is worth remembering generally: a PyHC-
sourced keyword on any entry may be registry bookkeeping rather than a claim about the software, and
should be judged on its own merit rather than trusted because the registry supplied it.

- **`specific` is dropped in this refresh.** It encodes the registry's general-versus-specific
  scope axis, which carries no meaning outside the registry. From the searcher's side a visitor
  reading POLAN's keyword list learns nothing from the word "specific" and may reasonably wonder
  what it means; it is bookkeeping surfaced as user-facing metadata, and that is the whole reason
  it goes.
- **`ionosphere_thermosphere_mesosphere` is kept, deliberately rather than by inertia.** Its
  underscore-joined form is visibly a machine tag, which is the argument that was made for dropping
  it too. It is kept because the domain claim is substantially earned — ionosphere squarely,
  thermosphere through the altitude range and the project's own declared keywords (Field 5) — and
  because the tag is a recognised cross-catalogue domain label that a user browsing by ITM topic may
  actually be filtering on. A machine-looking spelling is not by itself a reason to discard a
  meaningful domain descriptor.

Considered and not proposed: `fortran` and `f2py` both exist as keyword rows, but implementation
language is already Field 13 and a keyword there would duplicate a dedicated facet. `virtual
height` and `Chapman layer` would be apt but have no existing rows, and minting new keyword rows for
one entry is not worth the vocabulary churn.

### 17. Data Sources (OPTIONAL)
- Other

**Source and reasoning.** Unchanged, and correct on examination rather than by default. POLAN takes
a filesystem path and nothing else. The standalone program reads it from the command line
(`src/polrun.f` calls `get_command_argument`) and the Python API takes it as an argument
(`def gopolan(infn: Path | str) -> dict:`); there is no network code, no URL, and no archive client
anywhere in the eight Fortran files or the two Python files.

As of this refresh the controlled vocabulary holds seventeen values, and the rejection below closes
over every one of them rather than sampling the plausible-looking ones — which is what makes `Other`
a reasoned choice instead of a default.

`Observatory/Mission-specific` would claim POLAN is built around one observatory's holdings, which
Field 31/32 shows it is not. `Madrigal` and `WDC` both host ionosonde data, but POLAN neither queries
them nor implements their formats — the connection is that a user might download from them by hand,
which is true of any file-reading program. `The Virtual Solar Observatory.` (the trailing period is
part of the stored row name) is a solar data service that POLAN neither queries nor could use, since
it holds no ionogram data. `CDAWeb`, `HAPI`, `AMDA`, `OMNIWeb`, `SSCWeb`, `VirES`, `GFZ`, `das2`,
`TAP`, `S3/Cloud-aware`, `FTP/FTPS Directories` and `HTTP/HTTPS Directories` are all access
mechanisms POLAN does not implement. That is sixteen rejections plus the recorded value, and `Other`
accurately says "user-supplied local files".

If the vocabulary later gains a value for user-supplied local files, or an ionosonde-specific
archive, this field should be revisited.

### 18. Input File Formats (RECOMMENDED)
- ascii

**Source and reasoning.** Unchanged. Titheridge states the format in `README.1ST`: all files are in
`standard ASCII format.  Programs are written in FORTRAN, and can be processed` directly by most
compilers, and the driver `It reads ionogram data in 80-column format, and` prints the results.
`Readme_polan.md` points the reader at the shipped example, saying the input data format is best
seen by studying the examples in the test file `examples/in.dat`. That file is what both the
CMake test (`add_test(NAME basic COMMAND polan ${polan_SOURCE_DIR}/examples/in.dat)`) and the Python
test (`infn = R / "examples/in.dat"`) feed in. Byte-scanning `examples/in.dat` finds zero bytes above
127, and `file(1)` identifies it as ASCII text.

No other input format is supported: there is no CDF, netCDF, HDF5 or FITS reader in the tree, and
no binary input path.

`examples/in.asc` is also pure ASCII but is referenced nowhere in the tracked tree — it is a
historical deposit, not a second supported format.

### 19. Output File Formats (RECOMMENDED)
- ascii

**Source and reasoning.** Unchanged, and argued from the **output** side rather than inherited from
Field 18. `src/polrun.f` opens its result file with
`      OPEN (UNIT=2, FILE='out.dat',status='replace', action='write')`, and `README.md` describes
the CMake test as creating a big output text file named `out.dat`. The shipped
`examples/out.dat` is a 46,077-byte listing whose bytes are all below 128 and which `file(1)`
reports as ASCII text.

Recorded so a future agent does not misread it: the two 1996 output listings
`examples/POLOUT.396` and `examples/POLOUTQ.396` each contain 102 bytes of value 0xF1 (a DOS
code-page plus/minus sign) and CRLF line endings, so `file(1)` calls them ISO-8859 text. They are
Titheridge's archived reference outputs from a 1996 DOS run, not output this software produces
today. They do not make the output format anything other than ASCII.

The Python API returns an in-memory dictionary rather than writing a file, so it contributes no
output format.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

**Source and reasoning.** `Mac` and `Windows` are added in this refresh. The stored value was
`Linux` alone, resting on `.github/workflows/ci_unix.yml` — a file that no longer exists; it was
deleted before this revision. The CI at the pin is `.github/workflows/ci.yml`, and its matrix is
explicit: `        os: [ubuntu-latest, macos-latest, windows-latest]`, with
`        python-version: ['3.14']` across all three plus a 3.10 job on Ubuntu.

This is not a nominal matrix. The workflow carries real per-platform provisioning: it installs
`          mingw-w64-ucrt-x86_64-gcc-fortran` through MSYS2 and puts the UCRT64 toolchain on PATH
for Windows runs, and it sets `      run: echo "FC=gfortran-14" >> $GITHUB_ENV` for macOS. The build
itself carries platform-specific code too — `src/meson.build` contains a block that statically links
the Fortran runtime (`-static-libgcc`, `-static-libgfortran`, `-static-libquadmath`) when building on
Windows with MinGW GFortran, "so the extension module is self-contained". Every job runs the full
sequence: editable install, non-editable install, `mypy`, `pytest`, and the standalone CMake
workflow.

**`Operating System Independent` considered and rejected.** POLAN is compiled Fortran and needs a
GFortran with a working `-std=legacy` mode; that is not an OS-independent artefact in the way a pure
Python package is. Naming the three tested platforms is both more honest and more useful to a
searcher filtering for a specific OS. `Solaris`, `MobilePlatform` and `Other` are unevidenced.

`README.1ST` contains Titheridge's historical portability notes — `    POLAN fits comfortably on any
microcomputer, analysing a typical data` set in about a second, plus compiler-specific advice about
Lahey FORTRAN and comment characters. These describe 1980s–90s DOS-era portability and are not
evidence about the platforms supported now.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

**Source and reasoning.** Unchanged. Nothing in the build or the sources targets an instruction set.
`CMakeLists.txt` adds exactly one compile option, `  add_compile_options(-std=legacy)`; `meson.build`
adds the same argument and nothing else architecture-related. There are no intrinsics, no assembly,
no SIMD pragmas, no `-march`/`-mtune` flags, and no GPU or MPI code. The CI runs on whatever
architecture GitHub's `ubuntu-latest`, `macos-latest` and `windows-latest` images provide, which
spanned x86-64 and Apple Silicon as of 2026-09-08, and the project makes no distinction between them.

`x86-64`, `Apple Silicon arm64` and `Linux aarch64 or arm64` were considered and rejected: listing
specific architectures would imply the others are unsupported, which the build does not say.
`GPU` and `HPC or HEC` are plainly inapplicable to a single-threaded profile inversion that
`README.1ST` says runs in about one second.

### 22. Related Phenomena (OPTIONAL)
Not found

**Note — this is an examined, evidenced empty value, not an unfilled gap.** As of this refresh the
controlled vocabulary for this field held seven values, every one of them solar or magnetospheric:
`Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`,
`Solar Wind`, `X-ray emission`. There is no ionospheric phenomenon in the list at all — no sporadic
E, no spread F, no travelling ionospheric disturbance, no scintillation, no ionospheric storm.

POLAN analyses the quiet-time vertical structure of the ionosphere. It is not a storm, flare or CME
tool, and nothing in the tree ties it to any of the seven available values. Enumerating the
vocabulary here is the *reason* the field is correctly empty, and it should stop a future refresh
from reaching for `Geomagnetic Storms` on the grounds that ionospheric profiles change during storms
— they do, but the software supports no storm-specific functionality.

If the vocabulary later gains an ionospheric phenomenon, this field should be revisited.

### 23. Development Status (RECOMMENDED)
- Active

**Source and reasoning.** This field was empty in HSSI before this refresh. The value is chosen by
reading the controlled-vocabulary rows' own definitions, not the upstream repostatus.org wording:

- `Active` — "The project has reached a stable, usable state and is being actively developed."
- `Inactive` — "The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows."
- `Unsupported` — "The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired."

The first clause is satisfied on any reading: POLAN is a forty-year-old program with a tagged
release, a three-platform CI workflow, and a test suite. The question is the second clause, and the
facts settle it on `Active`:

- the most recent commit is the pinned revision, dated **2026-06-22**, and it is the head of
  `origin/main`;
- that day was not a typo fix. Nine commits landed on 2026-06-22, replacing `setup.py`/`setup.cfg`
  with `pyproject.toml` plus a Meson build, moving to the `mesonpy` backend, adding editable-install
  support, adding a Windows MinGW static-linking path, rewriting the CI, and refreshing the licence
  header. The release published that day describes itself as an
  "update to the current best practice in compiled Python modules - meson-python";
- the repository is **not archived** (`archived: false`, `disabled: false`), reports
  `open_issues_count: 0` — GitHub counts issues and pull requests together in that figure, so there
  is no open work of either kind — and has no wiki.

**This value reverses the 2025 seed dossier's `Inactive`, and the reversal is evidenced rather than
a matter of taste.** `Inactive`'s definition requires the project to be "no longer being actively
developed", and a full packaging modernisation shipped after the seed was written. The seed's value
rested on a "last changed on 2025-06-24" observation that the 2026-06-22 work supersedes; it
predates that work entirely, so it was defensible on the evidence available when it was recorded and
is simply out of date now. A future agent should not read the reversal as a disagreement about
judgement.

`Unsupported` is rejected: it requires the authors to have "ceased all work", which is false. The
rule that an archived GitHub repository maps to `Unsupported` does not apply here — this repository
is open.

Anchoring the judgement to dates rather than elapsed time, so it stays readable later: there has
been **no commit since 2026-06-22**, and the assessment above was made on 2026-09-08. A future
refresh that finds no further commits after 2026-06-22 should reconsider `Inactive`, bearing in mind
that this project's history is one of long quiet stretches punctuated by short bursts of real work
(nothing between 2021-10-11 and 2025-06-24, then a README touch, then the 2026 overhaul) — a gap is
this maintainer's normal rhythm rather than abandonment.

Note that GitHub's `updated_at` field is not commit activity and was not used; the dates above come
from the commit log and the release.

`pyproject.toml` declares the classifier `"Development Status :: 4 - Beta"`, which is a PyPI
maturity classifier on a package that has never been published to PyPI (Field 12). It is not
evidence about maintenance activity and did not drive this value.

### 24. Documentation (RECOMMENDED)
https://github.com/space-physics/POLAN

**Source and reasoning.** Unchanged. The field asks for the link to documentation *and installation
instructions*, and explicitly allows it to equal the access URL. The repository landing page is the
right answer here because it is the only place that carries all three layers of POLAN's
documentation and the install steps together:

- `README.md` gives the installation instructions (`pip install ./POLAN`, the editable-install
  variant, and the CMake workflow for the standalone Fortran program) and links onward with
  `See [Readme_polan.md](./Readme_polan.md) for more details on the POLAN code and how to run it.`;
- `Readme_polan.md` (20,099 bytes) is the actual reference manual — the call signature, every input
  parameter (`FB`, `DIP`, `START`, `AMODE`, `VALLEY`, `LIST`), the output arrays, the ten analysis
  modes, the single-polynomial modes, and the processing walkthrough;
- `README.1ST` is Titheridge's own user message, covering the subroutine inventory, profile accuracy,
  and implementation notes.

**Alternatives considered.**

- **A pinned link to `Readme_polan.md`.** It is the deepest documentation, but linking a single file
  strands the reader without installation instructions, which this field explicitly asks for.
  Rejected.
- **`https://www.ukssdc.ac.uk/ionosondes/polan_info.html`** — the URL GitHub reports as the
  repository's `homepage`. It was read in full. It is UKSSDC's POLAN information page, essentially
  the introduction to UAG-93: it explains why automated ionogram analysis is needed, what POLAN's
  weighted least-squares approach does, and cites the report and Titheridge (1979). It is a genuine
  and useful external reference, and it is worth knowing it exists. But it documents the *method*,
  not the *software distribution* — no installation, no build, no API, no mention of the Python
  package — and it is a third-party page whose footer dates it `3-DEC-1997`. Rejected as the Field
  24 value for those reasons; recorded here so a future agent knows it was found, read, and
  considered.
- **A GitHub wiki.** There is none. `has_wiki: false` on the repository, and — because a wiki is a
  *separate* git repository invisible from the code checkout, so the flag alone would not settle it
  — `git ls-remote https://github.com/space-physics/POLAN.wiki.git` was run directly and returned
  "Repository not found".
- **Read the Docs or a hosted site.** None exists; there is no `docs/` directory and no
  `.readthedocs.yaml` in the tree.

### 25. Funder (OPTIONAL)
Not found

**Note.** No funder is recorded anywhere in the software or its documentation. Searching the whole
tracked tree case-insensitively for `acknowledg` returns nothing, and searching for
`grant|funding|funded|NSF|NASA|award` as whole words returns nothing. There is no funding statement
in `README.md`, `README.1ST` or `Readme_polan.md`. `README.1ST` ends with Titheridge's personal
contact details and no acknowledgements section.

A `.github/FUNDING.yml` existed until 2021-08-02, when it was deleted. Its content was
`github: [scivision]` and `ko_fi: scivision` — personal sponsorship links for the maintainer, not a
research award, and therefore not a Field 25 value under any reading.

**The publication route was tried and is genuinely blocked, which is worth recording so it is not
retried blindly.** Acknowledgements in Titheridge's papers would be the natural place to find a
funder for the original work. ADS's acknowledgements index does not meaningfully reach them: `ack:`
queries against the 1988 Radio Science paper return 0, but so does the control
`ack:"grant" AND bibstem:RaSc AND year:1988` — while the same query without the year restriction
returns a large body of Radio Science papers that is overwhelmingly 2001 and later. Its coverage of
the earlier decades is not literally nil — sorted ascending, the earliest hit is a genuine 1975
paper, `1975RaSc...10..989K` — but it is sparse enough before 2001 that a miss there carries no
information. So the index does not meaningfully extend back to 1980s Radio Science, and its zero for
this paper is uninformative rather than a true negative. Europe PMC returns
0 hits for the paper's DOI, so there is no open full text there either. The publisher's own page was
not read. Any future attempt needs a browser-rendered publisher page, not an API.

Even if a 1980s grant were found, it would fund Titheridge's research rather than this software
distribution, so the case for recording it here would be weak.

### 26. Award Title (OPTIONAL)
Not found

**Note.** No award is recorded, for the same reasons as Field 25 — there is no acknowledgement,
grant number or award title anywhere in the tree. This field is also structurally dependent on
Field 25: an award with no title cannot be stored at all, so recording a funder without a titled
award would not be possible even if a funder were identified.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1002/rds19672101169
- https://doi.org/10.1029/rs010i006p00589
- https://doi.org/10.1016/0021-9169(79)90108-9
- https://doi.org/10.1016/0021-9169(82)90128-3
- https://doi.org/10.1029/rs020i002p00247
- https://doi.org/10.1016/0021-9169(86)90120-0
- https://doi.org/10.1029/rs022i005p00715

**Full citations, in the order above:**

1. Titheridge, J. E. (1967). "The Overlapping-Polynomial Analysis of Ionograms." *Radio Science*,
   2(10), 1169–1175.
2. Titheridge, J. E. (1975). "The relative accuracy of ionogram analysis techniques." *Radio
   Science*, 10(6), 589–599.
3. Titheridge, J. E. (1979). "Increased accuracy with simple methods of ionogram analysis."
   *Journal of Atmospheric and Terrestrial Physics*, 41(3), 243–250.
4. Titheridge, J. E. (1982). "The stability of ionogram analysis techniques." *Journal of
   Atmospheric and Terrestrial Physics*, 44(8), 657–669.
5. Titheridge, J. E. (1985). "Ionogram analysis: Least squares fitting of a Chapman-layer peak."
   *Radio Science*, 20(2), 247–256.
6. Titheridge, J. E. (1986). "Starting models for the real height analysis of ionograms." *Journal
   of Atmospheric and Terrestrial Physics*, 48(5), 435–446.
7. Titheridge, J. E. (1987). "Numerical errors in the real-height analysis of ionograms at high
   latitudes." *Radio Science*, 22(5), 715–727.

**Source and reasoning.** This field was empty before this refresh, on the earlier dossier's
assertion that these papers "lack DOIs". That assertion was false: every one of them resolves in
Crossref, with matching journal, volume, issue, page range and sole author. A nonsense control query
against the same endpoint returned 0 results, so the searches were discriminating.

These are not papers that merely cite POLAN — they are the papers POLAN's own bundled documentation
names as the sources of the procedures built into it, which is exactly what makes them worth a
reader's time. Provenance for each:

- Entries 2, 4, 5, 6 and 7 come from `README.1ST`, under the heading
  `Other papers on some of the procedures built in to POLAN are:`, listed there as
  ` Titheridge, J.E. (1975).  "The relative accuracy of ionogram analysis`,
  ` Titheridge, J.E. (1982).  "The stability of ionogram analysis`,
  ` Titheridge, J.E. (1985a).  "Ionogram analysis: Least squares fitting` of a Chapman-layer peak,
  ` Titheridge, J.E. (1986).  "Starting models for the real height analysis` of ionograms, and
  ` Titheridge, J.E. (1987).  "Numerical errors in the real-height analysis of` ionograms at high
  latitudes.
- Entry 1 comes from `Readme_polan.md`, which credits analysis mode 4 as
  `4.  Fourth Order Overlapping Polynomials (Radio Science 1967, p1169).` That reference resolves to
  ADS bibcode `1967RaSc....2.1169T`, whose sole author is Titheridge, J. E., with DOI
  `10.1002/rds19672101169`. Note that the publisher's registered title contains a typographical
  error — "lonograms" with a lowercase L rather than a capital I — which is reproduced identically
  in ADS and Crossref; the citation above silently corrects it, but a future agent matching titles
  should expect the typo in the source records.
- Entry 3 is not cited in the repository. It comes from the page GitHub declares as POLAN's
  homepage, `https://www.ukssdc.ac.uk/ionosondes/polan_info.html`, which explains POLAN's choice to
  store results at the scaled frequencies by citing Titheridge (1979). That page's citation gives
  the page range as "243--350", which is a typo; Crossref gives 243–250, and the citation above
  follows Crossref. It is included because it is a substantive design justification for POLAN cited
  by the project's own declared homepage.

**Two references deliberately not listed here.**

- The **1988** paper, `https://doi.org/10.1029/rs023i005p00831`, is the reference publication for the
  software and belongs in Field 14, not here. `README.1ST` itself makes the distinction, introducing
  it as the general discussion of the POLAN approach and the other five as covering individual
  procedures.
- **UAG-93** — the definitive report — has no DOI and no persistent landing page; see Field 14 for
  the full negative search. It cannot be recorded as a value in this field either, since only URLs
  are accepted and a web-archive snapshot is not a persistent identifier.

### 28. Related Datasets (OPTIONAL)
Not found

**Note.** POLAN ships no data and depends on none. The four data files in `examples/` are synthetic
test cases, not observational datasets: `examples/in.dat` is headed
`Chapman Layer, E + F.` and its cases are labelled `(1A)CHAPMAN, HM=300,SH=60`,
`(1B) TRUNCATED:  WITH FO`, `(1E)        WITH BAD FC` and so on — analytically constructed profiles
used to check that the inversion recovers known answers. `examples/out.dat`, `examples/POLOUT.396`
and `examples/POLOUTQ.396` are the corresponding outputs, and `examples/in.asc` is an orphan
listing referenced nowhere in the tree.

The software is designed to run on ionograms the user already has, from any station; it is not tied
to a particular published dataset, and no dataset DOI or `hpde.io` landing page is named anywhere in
the tree or in the project's documentation.

### 29. Related Software (OPTIONAL)
Not found

**Note — this is an evidenced empty value, established by two independent mechanical slices plus a
policy check, because any one of them alone leaves a blind spot.**

**(i) Inbound.** On 2026-09-08, scanning every entry in the catalogue for POLAN's repository URL —
and for the historical `scienceopen/polan` and lowercase `space-physics/polan` spellings — found
only POLAN's own record. Scanning for the bare word `POLAN`, and separately for `Titheridge` and for
`ionogram`, likewise returned only POLAN itself. The scan was not blind: the identical procedure
applied to `space-physics/msise00` found that URL inside the records of GLOW, HWM-93, ReesAurora and
ScienceDates as well as MSISE-00's own, proving it could see genuine cross-references. No entry in
the catalogue related itself to POLAN, and a later refresh should re-run the scan rather than assume
that still holds.

**(ii) By concept.** Querying the catalogue on the subject rather than the name gave the same answer
on the same date. The nearest neighbours by topic were incoherent-scatter tools (ADELPHI,
amisrsynthdata, GeoDataPython, GeospaceLAB, pyglow) — a different instrument class producing
profiles by a different physical technique. Nothing else in the catalogue performed ionogram
real-height analysis.

**Candidates considered individually and rejected.**

- **IRI-90, pyIRI2016, sami2py, PyGemini.** These produce ionospheric electron-density profiles, so
  the *output* resembles POLAN's. They were rejected because the *task* does not: they are
  climatological or first-principles models that predict a profile from time, place and geophysical
  indices, whereas POLAN measures one by inverting an observation. The form's own example of related
  software is two packages that model the same thing under different assumptions — POLAN does not
  model it at all. Accepting them here would also fail the equal-bar test: if a shared output
  quantity were enough, GLOW, MSISE-00, TIEGCM and most of the ionosphere-thermosphere section of the
  catalogue would qualify equally, and the field would carry no information.
- **The other space-physics packages by the same maintainer** (IRI-90, HWM-93, MSISE-00, GLOW,
  ReesAurora, and the rest). Shared authorship is explicitly not the test. Nothing links them to
  POLAN technically: POLAN imports none of them, they import nothing from POLAN, and the repository
  never mentions them.
- **MadrigalWeb.** Madrigal hosts ionosonde data that a POLAN user might download, but POLAN neither
  queries Madrigal nor implements its format. "A user might obtain input this way" is true of any
  file-reading program.
- **SPOLAN.** `README.1ST` describes a companion — `    A simplified version of POLAN, called
  SPOLAN, has also been developed.` — which provides nearly all of POLAN's facilities apart from
  extraordinary-ray data. This is the most tempting candidate and it is rejected on a hard fact:
  **SPOLAN is not in this repository and never has been.** `SPOLAN.FOR`, `SOLSUB.FOR` and
  `SCION.FOR` do not exist at the pin, and searching every path ever added anywhere in the history
  reachable from the pin finds none of them. Titheridge's text describes the contents of his 1990s
  distribution diskette, not of this repository. SPOLAN has no repository, no DOI and no landing
  page, so there is no URL to record even if one wanted to.
- **numpy** (`dependencies = ["numpy>=1.21"]`), **meson / meson-python / ninja**
  (`requires = ["meson-python>=0.16", "meson>=1.2", "ninja>=1.11", "numpy>=1.21"]`), and
  **pytest / mypy** (`tests = ["pytest", "mypy"]`). These are POLAN's entire dependency set, and
  every one of them is excluded by the field's generic-stack rule rather than by anyone's taste:
  arrays, build backend, test runner, type checker. Each would be equally at home in a web
  application, a finance model or a biology pipeline, so each is generic infrastructure. Being a
  dependency is not by itself a related-software relationship — the form's rule that a dependency is
  not interoperability is cross-applied to this field, together with its instruction that a Tier A
  package rejected from Field 30 must not be relocated here.

A package rejected from Field 30 does not automatically land here, and none of the above does.

### 30. Interoperable Software (OPTIONAL)
Not found

**Note — evidenced empty, on the same two slices as Field 29 plus a direct read of the public API.**

The bar for this field is a *demonstrated exchange*: a shared or converted data model, one package's
output importable into another, an adapter or converter function, a plugin relationship, a companion
package, or a bridge to a named domain tool. POLAN offers none of these.

Its entire public Python surface is one function, `def gopolan(infn: Path | str) -> dict:` in
`src/polan/__init__.py`. It takes a filesystem path and returns a plain Python dictionary with keys
`fv`, `height` and `dip` holding lists of floats. There is no `to_*`/`from_*` converter, no
`xarray.Dataset` or `astropy` object, no tplot variable, no CDF or NetCDF writer, no plugin hook, and
no IDL or MATLAB bridge. The standalone Fortran program's only interface is a text file on disk.

**Rejected, with the reason.**

- **numpy** is used internally (`import numpy as np`) to allocate the arrays passed through the f2py
  wrapper, and the wrapper itself is generated by `numpy.f2py`. That is a build and calling
  mechanism, not an interoperation. Tier A excludes it without exception, and "It directly depends
  on numpy" is true of nearly every package in the catalogue.
- **meson, meson-python, ninja, pytest, mypy** — build and test tooling; same exclusion.
- **Any Tier B package** (astropy, xarray, cdflib, h5py, netCDF4, dask, MATLAB, Jupyter and their
  peers) — none is present at all, so the Tier B evidence question never arises. There is nothing to
  cite because there is nothing there.
- **"part of the standard scientific Python ecosystem"** and **"a PyHC member, so it interoperates
  with PyHC packages"** — the two justifications the form names as never sufficient on their own.
  POLAN is in the PyHC registry's `projects_unevaluated.yml`, but registry membership establishes
  nothing by itself and no specific exchange with any PyHC package is documented anywhere.

### 31. Related Instruments (OPTIONAL)
Not found

**Note — this is an evidenced empty value reached through the relevance gate, not a resolution
failure, and it is deliberately *not* the earlier dossier's proposal.**

**What was proposed before and why it cannot be carried.** The prior dossier recorded
`Ionosonde (general class of instruments)` with no identifier. This field admits only entries
carrying a `https://spase-metadata.org/` identifier; a bare name does not fail safely, it creates a
new identifier-less row in the shared vocabulary. That value must never be submitted.

**The relevance gate is what actually decides this field, and POLAN fails it.** POLAN is
instrument-agnostic in the strictest sense. It reads a table of frequency/virtual-height pairs and
knows nothing about where they came from — no station identifier, no instrument model, no
manufacturer-specific format, no calibration path. The only inputs beyond the data are the
gyrofrequency, the magnetic dip angle and the analysis-mode switches. The shipped example data are
synthetic Chapman-layer test cases (`Chapman Layer, E + F.`, `(1A)CHAPMAN, HM=300,SH=60`), not any
station's measurements. Searching the whole tree finds no station name, no ionosonde model name, and
no mission name.

From the searcher's side, which is what settles it: a user on a specific ionosonde's page clicking
"show software related to this instrument" is asking which software was built for *that* instrument.
POLAN would appear there no more meaningfully than it would on every other ionosonde's page — it
serves all of them equally and none of them specifically. Listing every station would be spam;
listing one would be a false claim about a program that has no station-specific code.

**The vocabulary was nevertheless swept properly on 2026-09-08, because "agnostic" must be a
conclusion rather than an assumption.** A word-anchored search of both the `name` and `abbreviation` columns for
`\bionosonde\b|\bionosondes\b|\bdigisonde\b|\bsounder\b|\bsounders\b|\bionospheric sounding\b|\bchirpsounder\b|\bdynasonde\b` returned a substantial set of
genuine matches, against a positive control of `\bSuperDARN\b` which returned its expected rows. Every
naming authority present in the vocabulary was enumerated and inspected rather than guessed —
`ASWS`, `CNES`, `ESA`, `HamSCI`, `ISWI`, `IUGONET`, `NASA`, `NOAA`, `NSF` and `SMWG`. On that same
date, 2026-09-08, every row in the vocabulary carried a `https://spase-metadata.org/` identifier and
none failed that guard. That is a dated observation about the vocabulary's state, not a property it
is guaranteed to keep: a later refresh must re-run the guard rather than assume it, and a row that
fails it signals upstream drift and must be reported rather than used.

What the sweep found, so a future agent does not have to repeat it:

- **Ground ionosonde stations**, chiefly the ASWS Australian/Antarctic/Pacific network — for example
  `Learmonth Ionosonde` (`https://spase-metadata.org/ASWS/Instrument/Ground/Learmonth/Ionosonde`) and
  `Auckland Ionosonde` (`https://spase-metadata.org/ASWS/Instrument/Ground/Auckland/Ionosonde`) —
  plus IUGONET's NICT and RISH instruments such as
  `NICT Ionosonde at Kokubunji`
  (`https://spase-metadata.org/IUGONET/Instrument/NICT/misc/Kokubunji/Type10C_Ionosonde`), and the
  ISWI network instrument `GIRO Ionospheric Sounder`
  (`https://spase-metadata.org/ISWI/Instrument/GIRO/Ionosonde`).
- **Space-borne sounders**, including `Alouette 1 Sweep-Frequency Sounder`
  (`https://spase-metadata.org/SMWG/Instrument/Alouette1/SFS`), `ISIS2 Swept-Frequency Sounder`
  (`https://spase-metadata.org/SMWG/Instrument/ISIS2/SFS`) and
  `Advanced Ionospheric Sounder on SESAME`
  (`https://spase-metadata.org/SMWG/Instrument/SESAME/AIS`).
- **False positives on the word "sounder"** — the Cluster `WHISPER` relaxation sounders and the DMSP
  `Special Sensor Microwave Imager/Sounder` series, which are not ionosondes at all.

**Two specific candidates worth their own rejection, because both look attractive.**

- **`Auckland Ionosonde`.** Titheridge was at the University of Auckland (Field 6), so an Auckland
  association is superficially inviting. There is no support for it: the repository never mentions
  Auckland as a data source, no example datum comes from there, and Titheridge's Auckland address
  appears in `README.1ST` only as his contact details. Recording it would turn a biographical fact
  into a false technical claim.
- **The Alouette/ISIS topside sounders.** These are sweep-frequency sounders and POLAN analyses
  sweep-frequency ionograms, but the geometry is inverted: they sound *downward* from orbit through
  the topside ionosphere, while POLAN inverts bottomside ground-based ionograms upward to the layer
  peak — `Readme_polan.md` describes extrapolating points above the peak precisely because the
  bottomside analysis stops there. POLAN implements no topside inversion.

If POLAN ever gains a station-specific reader or format, this field should be revisited; as the
software stands, empty is the correct and useful answer.

### 32. Related Observatories (OPTIONAL)
Not found

**Note.** Empty for the same reason as Field 31, and checked separately rather than inferred from
it. At the 2026-09-08 sweep the observatory half of the vocabulary was well populated with
ionosonde sites — the ASWS ground stations each had an observatory row alongside their instrument
row (for example `Learmonth`,
`https://spase-metadata.org/ASWS/Observatory/Ground/Learmonth`), and the ISWI GIRO network
contributed a large set of station rows such as `BC840 Boulder, Colorado, USA`
(`https://spase-metadata.org/ISWI/Observatory/GIRO/BC840_Boulder`). So an observatory-level
association was available and was not taken.

It was not taken because there is nothing to associate. The observatory-level substitution in the
resolution ladder exists for software that genuinely supports a specific instrument whose own row is
missing; POLAN supports no specific instrument, so there is no instrument for an observatory row to
stand in for. A user browsing any one of those stations and asking what software relates to it would
be no better served by POLAN than a user at any of the others.

No bare name is recorded here, for the same hard reason given in Field 31.

### 33. Logo (OPTIONAL)
Not found

**Note.** POLAN has no logo, and there is nothing to pin. The tracked tree at the pinned revision
contains **zero image files** — searching it case-insensitively for `.png`, `.jpg`, `.jpeg`, `.gif`,
`.svg`, `.ico`, `.webp` and `.bmp` returns nothing, and the same search over every path ever added
anywhere in the history reachable from the pin also returns nothing, so no logo was ever committed
and later removed. Searching the whole tree for the word `logo` returns nothing.

Other sources were checked and are equally empty: `README.md` contains one badge, the CI status
badge from `github.com/space-physics/POLAN/actions/workflows/ci.yml/badge.svg`, which is a build
indicator and not a logo; the PyHC registry entry for POLAN carried no `logo:` key when it was read
on 2026-09-08, only `name`, `code`, `description`, `contact` and `keywords`; there is no DOI record
to inherit an image from (Field 2); and there is no project website of POLAN's own — the URL GitHub
lists as the homepage is a third-party UKSSDC text page with no project imagery.

A documented absence is the correct outcome here. No image should be invented, and the CI badge in
particular must not be recorded as a logo.
