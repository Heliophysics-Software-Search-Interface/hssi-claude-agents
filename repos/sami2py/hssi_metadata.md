# HSSI Metadata Extraction Results

**HSSI Software ID:** d6fa3131-3ab1-48c9-bd8b-31c0461a9fb5
**Repository:** https://github.com/sami2py/sami2py
**Source Revision:** c6d3c5bd2e3b2524017d1fca71c8dc8003c974fc
**Extraction Date:** 2026-09-12
**Validation Date:** 2026-09-12
**Validation Status:** PASS

---

## Scope note — read this before reading any field

Repository evidence below is read at the pinned revision, which is the tip of `main` and also the
release commit for v0.3.0. Four bodies of evidence sit **outside** that tree and are named explicitly
wherever they are used, because a reader who checks out the pin will not find them:

1. **The peer-reviewed sami2py paper**, `https://doi.org/10.3389/fspas.2022.1066480`, published
   2022-12-02 — a month *after* the pinned commit. It is the software's own overview paper and it
   carries the project's funding statement. Nothing in the pinned tree mentions it.
2. **The `develop` branch**, whose tip `b796fae` (2023-06-27) is the newest commit anywhere in this
   release lineage. Its `docs/introduction.rst` replaces the pinned citation instruction, and that
   replacement is what settles Field 14.
3. **The Zenodo record for v0.3.0** (`10.5281/zenodo.7277517`) and the concept record
   (`10.5281/zenodo.2875799`), which carry the release's own description text and the project's
   asserted creator list and order.
4. **A companion Zenodo dataset**, "sami2py sample output files" — the source of Field 28 and the
   artifact that first named the overview paper.

One consequence worth stating up front, because it governs several fields: **v0.3.0 removed
sami2py's plotting code.** The pinned package contains no plotting function, no `matplotlib` import
and no plotting dependency; that capability now lives in the separate `sami2py_vis` package. Several
values the record carried before this refresh predate that removal.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.2875799

This is the Zenodo **concept DOI** — the identifier that resolves to whichever deposit is newest —
and it is the right value for a field that identifies the software rather than one of its releases.
The version DOI belongs in Field 12, and is recorded there.

The concept/version split is established from the deposit records themselves, not inferred from the
numbering: both the v0.1.0 deposit (`10.5281/zenodo.2875800`) and the v0.3.0 deposit
(`10.5281/zenodo.7277517`) carry `"conceptdoi": "10.5281/zenodo.2875799"` and
`"conceptrecid": "2875799"`, and the v0.3.0 record's `relations.version` entry is marked
`"is_last": true` under parent recid `2875799`.

**The project cites three different DOIs for itself in three places, and two of those citations are
imprecise.** A future refresh will meet all three, so each is resolved here:

- `README.rst` reference [4] at the pin gives `https://doi.org/10.5281/zenodo.2875799` but labels it
  "Version 0.3.0 (v0.3.0)". The DOI is the correct concept DOI and the surrounding prose says so —
  "Note that this doi will always point to the latest version of the code" — so only the version
  label is wrong. This is the value recorded here.
- `docs/introduction.rst` at the pin asks users to cite "the package by Klenzing et al. [2019]
  https://doi.org/10.5281/zenodo.2875800". That is the **v0.1.0 version DOI**, whose deposit title is
  "jklenzing/sami2py: Initial github release" (published 2019-05-17) — a stale pointer to the first
  release, not a concept DOI. Do not promote it to Field 2. The project itself removed this citation
  on the `develop` branch.
- The README `|doi|` badge targets `https://zenodo.org/badge/latestdoi/167871330`, a redirector keyed
  to the GitHub repository id rather than a DOI. It resolves to the latest deposit, so it is a
  redirect service and not a persistent identifier; it is not a candidate for this field.

Considered and not selected: `https://doi.org/10.3389/fspas.2022.1066480`. That DOI identifies the
overview *paper*, not the software, and belongs in Field 14.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/sami2py/sami2py

The repository's own remote, and the URL the project gives in `README.rst`, in `setup.cfg`
(`url = https://github.com/sami2py/sami2py`), and in the Frontiers paper's data-availability text
("The sami2py Python model is freely available to the community at www.github.com/sami2py/sami2py").

Note for a future refresh: earlier releases lived under `jklenzing/sami2py` — the v0.1.0 Zenodo
deposit is titled "jklenzing/sami2py: Initial github release" and its supplement link points at
`https://github.com/jklenzing/sami2py/tree/v0.1.0`. The project moved to the `sami2py` organisation
before v0.3.0, whose deposit links `https://github.com/sami2py/sami2py/tree/v0.3.0`. The
organisation URL is current; the personal-account URL is historical and must not be restored.

### 4. Software Functionality (RECOMMENDED)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Physics-Based

Every child above is written `Parent: Child` because several category names in this vocabulary sit on
more than one row, and an unqualified child name is not unique. Both parents used here are listed in
their own right, as a child never implies its parent.

**Models and Simulations** and **Models and Simulations: Physics-Based** are the core of the entry.
SAMI2 solves the coupled continuity, momentum and temperature equations for seven ion species
(`nion = 7` in `sami2py/fortran/param-1.00.inc`, with `nchem = 21` chemical reactions) on a dipole
field-line grid; `sami2py.run_model()` is the user-facing entry point that configures and executes it.

**Models and Simulations: Empirical** is newly recorded, and is the single clearest gap in the
previously held classification. sami2py does not merely *contain* empirical models — it bundles them,
exposes them as user options, and lets the user perturb them:

- Neutral atmosphere: `docs/modifications.rst` states "This version uses the official release of
  NRLMSISe-00", and `Tinf_scale` scales the exospheric neutral temperature.
- Winds: "Sami2py uses the HWM-14 model by default." Users switch between three generations of the
  Horizontal Wind Model through the `hwm_model` keyword (`hwm_mod` in the namelist), backed by
  `hwm93.f`, `hwm07e.f90` and `hwm14.f90` in `sami2py/fortran/`.
- Drifts: "Fejer-Scherliess remains the default model for drifts", with a user-supplied Fourier
  series as the alternative.
- Photoproduction: EUVAC, scalable through `euv_scale`.

The `software-functionality` guidance describes this subcategory as covering "climatological models
(IRI, MSIS, HWM, IGRF)" — two of the four named examples are exactly what sami2py ships and
dispatches to.

**Data Processing and Analysis: Processing** — `Model._load_model()` reshapes raw model output into
labelled arrays, `_calculate_slt()` derives solar local time, and `_generate_metadata()` parses the
Fortran namelist into a human-readable dictionary.

**Data Processing and Analysis: File Format Conversion** — `Model.to_netcdf()` writes the loaded run
to netCDF4 (`self.data.to_netcdf(path=path, format='NETCDF4')`), converting from the Fortran-native
formatted or unformatted output.

**Considered and rejected:**

- **Data Processing and Analysis: Data Access and Retrieval** — held in the record before this
  refresh, considered on a narrower basis than the subcategory's usual one, and **not kept**. The
  evidence for and against is worth having on the record, because the case for it is real and a
  later refresh will meet it again. For: sami2py has a first-class archive-and-reload workflow,
  which the project puts in its own one-line summary of itself — the package "archives the output,
  and loads the resulting modeled values" — implemented as `utils.set_archive_dir()`,
  `utils.generate_path()` and the `Model(tag, lon, year, day)` constructor, which retrieves a
  previously archived run by its identifying coordinates. Against, and decisive: the
  `software-functionality` guidance defines this subcategory as "Downloading or querying data from
  remote archives", with `sunpy.net.Fido`, `astroquery` and CDAWeb/HAPI clients as its indicators,
  and sami2py has no network code at all at the pin — no download step, no HTTP layer, no query API.
  A searcher browsing this category for data-fetching tools would find a model with no network layer
  out of place, and the archive-and-reload behaviour a user does need to know about is already
  carried by the description in Field 8. The value is therefore removed rather than re-justified on
  the local-disk reading.
- **Data Visualization** and **Data Visualization: Line Plots** — held before this refresh and
  **stale as of v0.3.0**, so both are removed. The release removed plotting from the package:
  CHANGELOG.md for [0.3.0] records "Remove deprecated plotting functions (moved to `sami2py_vis`)".
  At the pin, a search of `*.py`, `*.rst`, `*.txt`, `*.cfg` and `*.md` for `matplotlib`, `pyplot` or
  `plot` returns five lines, and every one of them is in CHANGELOG.md rather than in code or
  configuration. One of the five is the v0.3.0 removal notice itself, under the `[0.3.0]` heading;
  the other four are historical entries under `[0.2.3]` and `[0.2.0]` describing plotting that no
  longer exists. No plotting method survives on the `Model` class, and neither `requirements.txt`
  nor `setup.cfg`'s `install_requires` (netCDF4, numpy, pandas, scipy, xarray) lists a plotting
  library. The capability moved to `sami2py_vis`, which is discussed in Field 30.
- **Models and Simulations: Theory** — also held before this refresh, also removed. That subcategory
  covers analytical and theoretical calculation; sami2py is a numerical time-stepping simulation
  with empirical drivers and ships no analytical solution. A visitor browsing "Theory" for analytic
  work would not expect a Fortran transport solver.
- **Models and Simulations: First Principles** — considered because the transport equations SAMI2
  solves are derived from fundamental plasma physics. Rejected: every driver of the simulation
  (neutral densities, winds, EUV flux, ExB drifts) comes from an empirical model, so the run is not
  an ab-initio calculation. "Physics-Based" is the honest fit and is already recorded, and
  "Empirical" now records the driver side explicitly.
- **Coordinate Transforms** and **Coordinate Transforms: Ionospheric** — considered because
  `sami2py/fortran/apexcord.f90` computes quasi-dipole/apex coordinates and `grid-1.00.f` converts
  the dipole field-line grid to geographic latitude, longitude and altitude. Rejected: both are
  internal. `apexcord.f90` exists to serve HWM14/DWM07, and the grid conversion happens once during
  model setup. No transform is reachable from the Python API — `sami2py.utils` exposes
  `generate_path`, `set_archive_dir`, `return_fourier`, `get_unformatted_data` and `fourier_fit`, and
  none is a coordinate transform. A user cannot call sami2py to convert coordinates.
- **Servers and Environments: High Performance Computing** — no MPI, no parallel decomposition, no
  job scripts. SAMI2 is a 2-D single-process model; `docs/sample_workflow.rst` puts a default run at
  "10-20 minutes" on an ordinary machine.

### 5. Related Region (RECOMMENDED)
**Values:**
- Earth Atmosphere
- Earth Ionosphere
- Earth Thermosphere

This vocabulary is flat: no value implies any other, so the coarse region already held in HSSI does
not stand in for the specific ones, and the specific ones do not make it redundant.

**Earth Ionosphere** is the one indispensable value and was missing. The package's own README titles
it "sami2py is another model of the ionosphere python style", after the model it runs, whose name
Huba et al. (2000) expand as "Sami2 is Another Model of the Ionosphere"; its own description calls it
a model of "a 2D ionospheric environment along a dipole magnetic field"; the quantities it solves for
are ion densities, velocities and temperatures. A visitor browsing the Earth Ionosphere region who was not shown
sami2py would be poorly served by the catalogue.

**Earth Thermosphere** is recorded because the neutral atmosphere the model runs in is a
thermospheric one and the software exposes it rather than hiding it: NRLMSISe-00 supplies neutral
densities, HWM supplies thermospheric winds, `Tinf_scale` scales the *exospheric* temperature, and
`run_model(..., outn=True)` writes the neutral densities and winds out alongside the ions for
downstream use. The recorded rationale is deliberately this narrow: sami2py does not *solve* the
neutral atmosphere, it drives itself from an empirical one and reports it.

**Earth Atmosphere** is retained. It is the region under which the PyHC registry files this package
(its keyword tag is `ionosphere_thermosphere_mesosphere`), and it remains true of a model whose
domain begins at `altmin = 85.0` km.

**Considered and rejected:**

- **Earth Inner Magnetosphere** — considered seriously and rejected, and the reasoning is recorded in
  full because the obvious first-pass argument for rejecting it is wrong. SAMI2's domain is *not*
  confined to ionospheric altitudes: `sami2py/fortran/README-1.00` states the model solves "in the
  altitude range 85 km to 20,000 km", and `run_model`'s `rmax` parameter is documented on two
  consecutive docstring lines in `sami2py/_core.py` as "Maximum altitude of the highest field line in
  km" and "This has to be less than 20,000 km." The familiar
  `rmax = 2000.0` is only the default — it is the value in `run_model`'s signature and in the
  reference namelist `sami2py/tests/test_data/ref_f_sami2py-1.00.namelist`, not a ceiling. A run
  configured to the documented maximum reaches plasmaspheric flux tubes. Do not reject this region on
  the default grid; that argument does not hold.

  It is rejected instead on what the software is for. The project never frames sami2py as a
  plasmaspheric or magnetospheric tool: its description, its documentation, its keywords and its
  overview paper are ionospheric throughout, the modelled species are the seven ionospheric ions, and
  the published applications are low- and mid-latitude ionospheric ones. A visitor browsing the inner
  magnetosphere for ring-current, radiation-belt or plasmaspheric tools would not be served by this
  entry. If a future refresh finds the project itself claiming plasmaspheric application, this value
  should be revisited — the physics permits it and only the framing excludes it.
- **Earth Magnetosphere**, **Earth Outer Magnetosphere**, **Earth Magnetosheath** and **Earth
  Magnetotail** — the vocabulary's four remaining Earth-magnetosphere rows, each further from this
  software's domain than Earth Inner Magnetosphere, which is the closest of the five and is rejected
  above on its own reasoning. Named explicitly so the enumeration here reads as exhaustive by design.
- **Earth Lower and Middle Atmosphere** — rejected. The `altmin = 85.0` km lower boundary is the
  mesopause, i.e. the edge of the domain rather than a region modelled within it. Nothing below it is
  simulated.
- **Earth Auroral Subregion** — rejected. SAMI2 is a low-latitude and mid-latitude model; the paper's
  title-level framing and Huba et al. (2000)'s own subtitle call it "A new low‐latitude ionosphere
  model". Auroral physics (precipitation, field-aligned currents) is absent.
- Every solar, heliospheric and planetary value in the vocabulary — Chromosphere, Corona,
  Photosphere, Solar Interior, Solar Environment, Solar Wind, Interplanetary Space, Heliosheath, the
  five planetary magnetosphere rows and Planetary Magnetospheres — is out of scope for a terrestrial
  ionosphere model.

### 6. Authors (MANDATORY)

**Author 1:**
- **Author Name:** Jeff Klenzing
- **Author Identifier:** https://orcid.org/0000-0001-8321-6074
- **Affiliation:**
  - **Organization:** Goddard Space Flight Center
  - **Affiliation Identifier:** https://ror.org/0171mag52

**Author 2:**
- **Author Name:** Jonathon M. Smith
- **Author Identifier:** https://orcid.org/0000-0002-8191-4765
- **Affiliation 1:**
  - **Organization:** Catholic University of America
  - **Affiliation Identifier:** https://ror.org/047yk3s18
- **Affiliation 2:**
  - **Organization:** Goddard Space Flight Center
  - **Affiliation Identifier:** https://ror.org/0171mag52

**Author 3:**
- **Author Name:** Angeline Burrell
- **Author Identifier:** https://orcid.org/0000-0001-8875-9326
- **Affiliation:**
  - **Organization:** United States Naval Research Laboratory
  - **Affiliation Identifier:** https://ror.org/04d23a975

**Author 4:**
- **Author Name:** Reika Kitano
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** American University
  - **Affiliation Identifier:** https://ror.org/052w4zt36

**Author 5:**
- **Author Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493
- **Affiliation 2:**
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found

**Order.** The order above is the project's own, taken from `.zenodo.json` at the pin and from the
published v0.3.0 Zenodo deposit (`10.5281/zenodo.7277517`), which agree: Klenzing, Smith, Burrell,
Kitano, Hirsch. Author order is stored data in HSSI, and the order the record held before this
refresh was alphabetical by family name — Burrell, Hirsch, Kitano, Klenzing, Smith — which is not an
order the project asserts anywhere, and which buries the lead author and maintainer in fourth place.
Jeff Klenzing is the `setup.cfg` author, the first author of the overview paper, and by a wide margin
the largest contributor in the repository's contributor list. The project's order is therefore
preferred, and it is the order recorded above.

Note one genuine ambiguity rather than pretending it away: `README.rst` reference [4] gives a
*different* order from `.zenodo.json` — Klenzing, Smith, Kitano, Hirsch, Burrell, with Burrell fifth
rather than third. Where a hand-written citation line and the project's machine-readable deposit
metadata disagree, the deposit metadata is preferred: it is what the project actually published to
Zenodo, it is generated from a file under version control, and it is the form DataCite and every
downstream aggregator carry.

**The sixth credited name, `zzyztyy`, was considered and is deliberately not recorded here.** The
project's own creator list is six long, not five: `.zenodo.json` at the pin and the v0.3.0 deposit
both close with `{"name": "zzyztyy"}`, and `README.rst` reference [4] names it in the suggested
citation — "Klenzing, J., J.M. Smith, R. Kitano, M. Hirsch, A.G. Burrell, and zzyztyy." The credit is
genuine and was deliberately given. `zzyztyy` is a real GitHub account with a merged code
contribution to the Fortran core: commit `d8fe2fd` (2021-05-26) changed two lines of
`sami2py/fortran/sami2py-1.00.f`, and Jeff Klenzing merged it as pull request #143 on 2021-05-28,
then added the name to `.zenodo.json` by hand four days later in commit `aafa50d` (2021-06-01). It is
neither a placeholder nor an import artifact. The name is also mononymous: there is no given/family
split available anywhere — no real name appears in `.zenodo.json`, in the contributor list, or in the
citation line — so it could only ever be recorded verbatim as the handle.

That case was weighed in full and the decision went the other way: **the sixth author was not adopted
for HSSI's author list.** This is recorded as a settled judgement, not as a refutation — the evidence
above stands, and a later refresh that rediscovers it should recognise the question as already asked
and answered rather than re-proposing the addition or concluding the contributor was overlooked.

**Affiliations.** Every recorded affiliation is confirmed, and two are richer than the project's own
statement:

- **Klenzing / Goddard Space Flight Center** — confirmed by `.zenodo.json` and by ORCID, whose
  employment entry is Goddard Space Flight Center, ITM Physics Lab, 2012 to 2025-08. *Durable note
  for a later refresh:* that ORCID record goes on to show a move to the University of Maryland,
  Baltimore County in two successive entries — Goddard Planetary Heliophysics Institute, 2025-10 to
  2026-06, then Center for Space Sciences and Technology from 2026-06. The affiliation recorded here
  is deliberately the one contemporaneous with the credited work and with the v0.3.0 release, not his
  current employer. Do not "correct" it to UMBC.
- **Smith / Catholic University of America + Goddard Space Flight Center** — richer than a naive read
  of the source. `.zenodo.json` packs both institutions into a single string,
  `"affiliation": "Catholic University of America, Goddard Space Flight Center"`, which a
  one-affiliation-per-creator import would silently truncate to the first. Both are recorded,
  correctly split. ORCID independently confirms Catholic University of America (Research
  Scientist, Physics, 2018-), and the companion Zenodo dataset records him as "NASA GSFC / Catholic
  University of America".
- **Burrell / United States Naval Research Laboratory** — confirmed and *expanded*. `.zenodo.json`
  gives the acronym form "U.S. Naval Research Laboratory"; the recorded value is the full institutional
  name with ROR `04d23a975`, which is what this field asks for. ORCID gives "US Naval Research
  Laboratory", Space Science Division, 2018-.
- **Kitano / American University** — confirmed by `.zenodo.json`, and corroborated independently by
  the repository's own contributor list, which carries the address
  `reika.kitano@student.american.edu`.
- **Hirsch / Boston University** — confirmed by `.zenodo.json` and by ORCID (Research Scientist, ECE,
  2018-).
- **Hirsch / Scivision, Inc.** — richer than the project's own statement, which names only Boston
  University, and not confirmed by ORCID, whose only employment entry is Boston University. It is
  nonetheless well-founded and is kept: Michael Hirsch's Scivision is the software consultancy behind
  the `space-physics` GitHub organisation, he contributes to this repository under the `scivision`
  account, and sami2py's own `docs/installation.rst` sends Windows users to
  `https://www.scivision.dev/cmake-install-windows` for compiler help.

**Negative research, recorded so it is not repeated:** *do not* attach a ROR to Scivision, Inc. A ROR
query for that name returns exactly one organisation, `https://ror.org/011qev639` — "SciVision
Biotech Inc. (Taiwan)", a Kaohsiung biotechnology company with the domain `scivision.com.tw`. That is
a different entity that happens to share a name, and binding it here would assert a false
affiliation. The correct state for this affiliation identifier is empty.

**Display forms.** Four of the five display names match what the project and ORCID use. One does not,
and the divergence is recorded rather than acted on: HSSI stores Burrell as given name "Angeline",
while `.zenodo.json` writes "Burrell, Angeline G.", `README.rst` reference [4] writes "A.G. Burrell",
the overview paper's author list writes "Angeline G. Burrell", and her ORCID record carries the
credit name "Angeline G. Burrell" alongside the primary given name "Angeline". The middle initial is
the form she publishes under. This belongs to a person record shared with other catalogue entries
rather than to sami2py's metadata, so it is documented here as a finding and not asserted as a
sami2py field value.

**Not proposed as a value, recorded as a finding:** no ORCID is recorded for Reika Kitano, and none
was found. Supplying an identifier for an author whose stored record has none is out of scope for a
metadata refresh of this software, so this is deliberately left as "Not found" here.

### 7. Software Name (MANDATORY)
**Value:** sami2py

Lower-case throughout, and consistently so: `setup.cfg` declares `name = sami2py`, the package
directory is `sami2py/`, the GitHub organisation and repository are both `sami2py`, and the overview
paper's title is "sami2py—Overview and applications". The one capitalised form in the project's own
prose is the sentence-initial "Sami2py" that opens the README's Overview paragraph, which is
capitalisation rather than an alternative name.
The underlying NRL model is written "SAMI2" in capitals; the Python package is not.

### 8. Description (MANDATORY)
**Value:** Sami2py is a python module that runs the SAMI2 model, archives the output, and loads the resulting modeled values. SAMI2 is a model developed by the Naval Research Laboratory to simulate the motions of plasma in a 2D ionospheric environment along a dipole magnetic field. SAMI2 solves for the chemical and dynamical evolution of seven ion species in this environment (H+, He+, N+, O+, N2+, NO+, and O2+). The implementation used here includes several added options to the original release of SAMI2, including the ability to scale the neutral atmosphere in which the ions form through direct modification of the exospheric neutral temperature for extreme solar minimum conditions, and the ability to input custom ExB drifts as a Fourier series.

This is the project's own Overview section from `README.rst`, flattened out of reStructuredText: the
subscript/superscript markup around the ion species is rendered as plain `H+`, `N2+` and so on, the
bracketed citation references are dropped, and the two bulleted "added options" are folded into the
closing sentence. Nothing is added and nothing substantive is cut. `docs/introduction.rst` carries
the same text almost word for word.

Left as it stands. It is the maintainers' own description of their software, it is accurate at the
pin, and rewriting it would substitute a cataloguer's voice for the project's.

### 9. Concise Description (OPTIONAL)
**Value:** Python wrapper to run, read, and plot the SAMI2 ionospheric model.

The project's own one-line summary: it is the GitHub repository description verbatim and the
description on the v0.1.0 Zenodo deposit, with a closing period added.

A tension worth recording, so a future refresh meets it already reasoned through rather than
apparently new: **"plot" is no longer literally true of the package.** v0.3.0 removed the plotting
functions to `sami2py_vis` (see Field 4). The phrase is kept anyway, for two reasons. It is the
project's own current self-description — the GitHub repository description still reads exactly this
way — and a one-line summary of a package whose companion still plots its output is not misleading to
a searcher in the way a functionality category would be. The place where that removal must be
reflected is Field 4, where it is a searchable classification, and that is where it has been.

### 10. Publication Date (RECOMMENDED)
**Value:** 2022-11-03

The v0.3.0 Zenodo deposit's `publication_date`, matching the GitHub release
(`published_at: 2022-11-03T14:08:18Z`), the `[0.3.0] - 2022-11-03` heading in CHANGELOG.md, and the
committer date of the pinned commit itself (2022-11-03). Four independent artifacts, one date.

Not to be confused with the overview paper's publication date, 2022-12-02, which belongs to
Field 14's publication rather than to the software release.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Zenodo is where the software is deposited and is the registrant of the DOIs in Fields 2 and 12. The
repository host, GitHub, is not the publisher; it is recorded in Field 3.

### 12. Version (RECOMMENDED)

**Version Number:** v0.3.0
**Version Date:** 2022-11-03
**Version Description:** Updates code standards and improves testing / os support.
**Version PID:** https://doi.org/10.5281/zenodo.7277517

v0.3.0 is the newest release in this lineage — the GitHub release list holds ten releases, of which
v0.3.0 (2022-11-03) is the most recent, and the pinned commit is its release commit. The `v` prefix
is the project's own: the git tag is `v0.3.0`, the GitHub release name is `v0.3.0`, and the Zenodo
deposit's `version` field is `"v0.3.0"`. (`sami2py/version.txt` contains the bare `0.3.0`, which is
the Python package version string rather than the release label.)

**The version description is newly supplied; the stored release carried none.** It is the release's
own opening sentence, quoted rather than paraphrased: the GitHub release body for `v0.3.0` begins
"Updates code standards and improves testing / os support.", and the Zenodo deposit's description
opens with the same sentence as its first paragraph.

Every clause of that sentence is attributable to this release's range, checked against the nine
bullets under `## [0.3.0] - 2022-11-03` in CHANGELOG.md, which are identical to the bullets in the
release body:

- "Updates code standards" — "Implement flake8-docstring and hacking packages to lint code",
  "Update docstring standards", "Deprecated camel case keys in `run_model`", "Removed deprecated
  pytest functions".
- "improves testing / os support" — "Updated NEP 29 compliance in CI tests", "Add CI tests for Mac Os
  X", "Fixed a bug in Windows CI environment in usage of mingw-64".

Two bullets are not covered by the summary sentence: "Remove deprecated plotting functions (moved to
`sami2py_vis`)" and "Improved discussion of fortran compiler requirements in docs". Both are genuine
v0.3.0 changes and both are recorded where they matter — the first in Fields 4 and 30, the second in
Field 24's documentation evidence.

**Rejected: a longer synthesis.** A description could be assembled by stringing all nine changelog
bullets into prose, and one such synthesis was previously drafted. It is not used. It is a
cataloguer's summary rather than the project's, it re-words the maintainers' bullets while claiming
to report them, and it is no more informative than the sentence the maintainers wrote for exactly
this purpose. Where a release supplies its own summary line, that line wins.

The version PID is the v0.3.0 deposit DOI, distinct from the concept DOI in Field 2 and confirmed by
that deposit's `"doi": "10.5281/zenodo.7277517"` with `"is_last": true`.

### 13. Programming Language (RECOMMENDED)
**Values:**
- Fortran77
- Fortran90
- Python 3.x

The form defines this field as "The computer programming languages most important for the software."
and instructs "This is not meant to be an exhaustive list". That criterion is applied here as: a language a reader
must know to understand or modify the parts of this software that do its work. Everything below
follows from it, and nothing follows from byte counts alone.

- **Fortran77** — the numerical core. `sami2py/fortran/sami2py-1.00.f` is the SAMI2 model itself, in
  fixed-form Fortran; `grid-1.00.f`, `grid-rminrmax.f`, `hwm93.f` and `nrlmsise00_modified.f` are the
  grid generator and two of the bundled empirical models. Fixed-form is not incidental: the project's
  documented compile line is `gf = gfortran -fno-range-check -fno-automatic -ffixed-line-length-none`.
- **Fortran90** — free-form sources sit beside them: `apexcord.f90`, `dwm07b.f90`, `hwm07e.f90`,
  `hwm07e_modified.f90` and `hwm14.f90`, the last being the default wind model.
- **Python 3.x** — the entire user-facing interface. `setup.cfg` sets
  `python_requires = >= 3.5` and classifies for 3.7, 3.8 and 3.9. There is no Python 2 support.

**Rejected:**

- **C++** and Assembly appear in GitHub's language breakdown for this repository (C++ 2,309 bytes,
  Assembly 4,118 bytes, against Fortran 608,113 and Python 70,811). Neither exists. No `.cpp`, `.cc`,
  `.h`, `.s` or `.asm` file is tracked at the pin; these are GitHub Linguist misclassifying fixed-form
  Fortran and the binary/tabular data files in `sami2py/fortran/`. Recorded explicitly because the
  language breakdown is an inviting one-call source and it is wrong here. Assembly has no row in the
  vocabulary in any case; C++ does, and must not be selected on this evidence.
- **Makefile** (396 bytes in the same breakdown) — a build file, not one of the languages most
  important to the software, and with no row in the vocabulary.
- **Fortran 2003**, **Fortran 2008** and **Fortran 2023** rows exist in the vocabulary and are not
  selected: the free-form sources are HWM/DWM-era Fortran 90/95, and nothing in the tree uses
  object-oriented, submodule or coarray features that would require a later standard.

### 14. Reference Publication (RECOMMENDED)
**Value:** https://doi.org/10.3389/fspas.2022.1066480

Klenzing, J., J. M. Smith, A. J. Halford, J. D. Huba and A. G. Burrell (2022), "sami2py—Overview and
applications", *Frontiers in Astronomy and Space Sciences*, 9, article 1066480, published 2022-12-02.

**This is the paper about this software**, which is what the field means and what a visitor reading a
"reference publication" row expects: a peer-reviewed article whose subject is sami2py itself, whose
abstract opens "sami2py is a Python module that runs the SAMI2 (Sami2 is Another Model of the
Ionosphere) ionospheric model, as well as load and archive the results", and whose author list is the
software's own lead developers plus the original SAMI2 author.

**The project itself designates it.** The pinned tree cannot show this — the paper appeared a month
after the pin — but the `develop` branch's `docs/introduction.rst` replaces the pinned citation
instruction with a line reading "Klenzing et al. [2022] https://doi.org/10.3389/fspas.2022.1066480."
In other words the maintainers' own answer to the question of what a user should cite for this
package moved from a Zenodo version DOI to this paper.

**Why the SAMI2 foundational paper is not this value.** `https://doi.org/10.1029/2000JA000035` —
Huba, Joyce and Fedder (2000), "Sami2 is Another Model of the Ionosphere (SAMI2): A new low‐latitude
ionosphere model" — was previously the obvious candidate and is the one the project names first in
every citation instruction it has ever published. It describes the **underlying NRL model**, not this
Python package; it predates sami2py by nineteen years and none of its authors wrote sami2py. The
project asks for it *in addition to*, not instead of, the package citation: "please cite the original
paper by Huba [1]_ as well as the package [4]_". It is therefore a related publication, and HSSI
already holds it as one — that existing placement is correct and is kept unchanged in Field 27. A
visitor who wants the model physics finds it there; a visitor who wants the software finds the
Frontiers paper here.

The reference-publication slot was empty before this refresh. Filling it is the substantive gain of
this field, and the route to it is worth recording because it was not visible from the repository:
the paper is named in the description of the companion Zenodo dataset (Field 28), which cites "the
manuscript 'The sami2py model -- overview and applications', submitted to Frontiers in Astronomy and
Space Science in October 2022" — a working title that differs from the published one.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License

HSSI's licence values are a fixed set of shared rows and carry no per-software licence URI, so this
field is a choice among those rows rather than a free-text SPDX reference. The matching row's own URL
is `https://spdx.org/licenses/BSD-3-Clause.html`.

Determined from the licence text, not from a declared label. `License.md` at the pin is the BSD
three-clause text, and the decisive third clause is present: "Neither the name of sami2py nor the
names of its contributors may be used to endorse or promote products derived from this software
without specific prior written permission." `setup.cfg` independently classifies
`License :: OSI Approved :: BSD License` and points `license_file = License.md`.

**The near-match row is ruled out by content.** `BSD 2-Clause "Simplified" License` is the
two-clause variant, which by definition lacks exactly the non-endorsement clause quoted above. The
presence of that clause is what makes this three-clause, not two.

**Licence history, read by content rather than by label.** The terms have never changed in this
lineage. The earliest `License.md` carries the same BSD three-clause text under
"Copyright (c) 2017, Jeff Klenzing (JK) and Joe Huba (JH)"; at the pin the same text stands under
"Copyright (c) 2021, sami2py development team". Only the copyright holder line was updated, from two
named individuals to the project team. There is no relicensing event for a future refresh to
discover.

**A trap worth recording.** The Zenodo deposit for v0.3.0 declares `"license": {"id": "other-open"}`,
which is wrong — the deposit's own attached source carries the BSD three-clause text. Any workflow
that fills this field from the DOI record will produce "Other" for this software. It should not be
taken; the repository licence governs, and the correct value is the one recorded above.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- ionosphere
- ionosphere modeling
- ionosphere thermosphere mesosphere
- python
- sami2
- plasma
- fortran
- thermosphere
- neutral atmosphere
- empirical model

The first five are the project's own declared terms and are kept unchanged. They come from three
places that agree: the GitHub repository topics are `ionosphere`, `ionosphere-modeling` and `python`
(the hyphen normalised to a space); `setup.cfg` declares `keywords = SAMI2, ionosphere`; and the PyHC
community registry files this package under `ionosphere_thermosphere_mesosphere`. Note that the
stored form of these values is lower-case — a title-cased rendering ("Ionosphere Modeling") is a
display transform, not the value.

The five additions are chosen to answer searches this entry would otherwise miss, and each reuses a
term already in use elsewhere in the catalogue rather than minting a near-duplicate:

- **plasma** — the quantity the model actually solves for. Its outputs are ion densities, velocities
  and temperatures; its own description is about "the motions of plasma".
- **fortran** — a practical fact a prospective user needs before installing. The numerical core is
  Fortran, and the software cannot be installed without a working Fortran compiler; the project
  devotes a documentation section to obtaining gfortran or mingw-64.
- **thermosphere** — matches the neutral atmosphere the model runs in, and pairs with the region
  value recorded in Field 5.
- **neutral atmosphere** — a distinguishing capability rather than a generic tag. Scaling the neutral
  atmosphere (`Tinf_scale`, the per-species `*_scale` keywords) and optionally writing the neutral
  densities and winds out (`outn=True`) are among the specific things this implementation added to
  stock SAMI2.
- **empirical model** — captures the bundled, user-switchable NRLMSISe-00, HWM93/HWM07/HWM14,
  Fejer-Scherliess and EUVAC models, which are the reason a researcher would reach for this package
  over a bare SAMI2 build.

**Considered and rejected:** *space weather* (this is a research and teaching model, not a forecasting
or operational tool; nothing in the project claims nowcast or forecast use); *magnetosphere* (see the
region reasoning in Field 5); *simulation* (true but non-discriminating — it duplicates the
functionality category and would not narrow any search); and *specific*, which appears alongside
`ionosphere_thermosphere_mesosphere` in the PyHC entry but is PyHC's own general-versus-specific
classification marker rather than a subject term.

### 17. Data Sources (OPTIONAL)
**Value:** Not found

Correct and evidenced, not an unexamined blank. **sami2py consumes no external data archive.** Its
inputs are numbers a user types: `run_model()` takes the date, longitude, grid parameters, `f107`,
`f107a`, `ap`, model-selection switches and optional Fourier coefficients. There is no download step,
no credential handling, and no network code at all — a search of every Python file at the pin for
`import requests`, `urllib`, `http`, `ftplib` or `socket` returns nothing, against a control on the
same files that returns matches as expected. The empirical models the run needs are compiled in, and
their coefficient tables ship inside `sami2py/fortran/`.

The whole Data Sources vocabulary was considered against this and none applies: AMDA, CDAWeb, das2,
FTP/FTPS Directories, GFZ, HAPI, HTTP/HTTPS Directories, Madrigal, Observatory/Mission-specific,
OMNIWeb, Other, S3/Cloud-aware, SSCWeb, TAP, The Virtual Solar Observatory., VirES and WDC are all
remote-archive or service categories that require the software to fetch something. This one does not.

That same absence of network code is what removed **Data Processing and Analysis: Data Access and
Retrieval** from Field 4, where the full reasoning sits. The archive-and-reload workflow sami2py does
have reads and writes its own model runs on local disk: it is neither a data source for this field
nor remote data access for that one. The two fields agree, and neither should be read as licence for
restoring a value in the other.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- ascii
- Other

**ascii** covers everything a user supplies and most of what the reader parses: the Fortran namelist
`sami2py-1.00.namelist`, the `exb.inp` Fourier-coefficient file, and — when a run is made with the
default `fmtout=True` — the formatted output files the `Model` class reads back with `np.loadtxt`
(`time.dat`, `glatf.dat`, `glonf.dat`, `zaltf.dat`, `denif.dat`, `vsif.dat`, `tif.dat`, `tef.dat`).

**Other** is newly recorded and covers binary Fortran data, which has no row of its own:

- Unformatted Fortran output, read back when a run used `fmtout=False`. `sami2py` ships a dedicated
  reader for it — `utils.get_unformatted_data`, documented as "Interpret unformatted binary files
  created by the SAMI2 model", which strips the record-length markers Fortran writes around each
  record.
- The bundled binary coefficient tables the empirical models load at runtime,
  `sami2py/fortran/hwm123114.bin` and `sami2py/fortran/dwm07b104i.dat`.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- ascii
- netCDF3/4
- Other

**netCDF3/4** — `Model.to_netcdf()` writes the loaded run with
`self.data.to_netcdf(path=path, format='NETCDF4')`, carrying the full run configuration across as
file attributes. This is the format the project intends for sharing results; the overview paper notes
that these files are built to be readable by pysat.

**ascii** is newly recorded, and is in fact the *default* output path rather than an edge case. The
namelist switch `fmtout` defaults to `.true.` in `run_model`'s signature and is `.true.` in the
reference namelist, and in that mode SAMI2 writes formatted text files. The repository's own checked-in
reference run is in this form.

**Other** — unformatted Fortran binary, produced when `fmtout=False`. This is stock SAMI2's native
output format and the reason `utils.get_unformatted_data` exists.

### 20. Operating System (RECOMMENDED)
**Values:**
- Linux
- Mac
- Windows

All three are claimed and all three are tested. `setup.cfg` classifies
`Operating System :: POSIX :: Linux`, `Operating System :: MacOS :: MacOS X` and
`Operating System :: Microsoft :: Windows`; `.github/workflows/main.yml` runs the test matrix on
`ubuntu-latest`, `macos-latest` and `windows-latest`. Windows support is not nominal — v0.3.0's
changelog records "Fixed a bug in Windows CI environment in usage of mingw-64", and
`docs/installation.rst` gives a separate Windows compile path (`make -C sami2py\fortran compile`) and
mingw-64 guidance.

**Operating System Independent** was considered and not selected. It would be the wrong claim for
software whose installation depends on a platform-specific Fortran toolchain; the project documents
different compiler acquisition routes per platform, which is precisely the situation the named
values exist to describe.

### 21. CPU Architecture (RECOMMENDED)
**Value:** CPU Independent

Nothing in the source or build constrains the architecture. The Fortran compile line is generic
gfortran with portability flags (`-fno-range-check -fno-automatic -ffixed-line-length-none`); there
are no intrinsics, no vendor libraries and no architecture-specific build branches.

**HPC or HEC** and **GPU** were considered and rejected: SAMI2 is a two-dimensional single-process
model with no MPI, no OpenMP and no accelerator code, and a default run is put at "10-20 minutes" on
an ordinary desktop by `docs/sample_workflow.rst`.

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found

**This is an evidenced empty value, and the evidence is the vocabulary itself.** The Phenomena list
holds seven values — Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona,
Solar Flares, Solar Wind, X-ray emission. Six are solar or heliospheric and are simply out of scope
for a terrestrial low-latitude ionosphere model. There is no ionospheric phenomenon in the list at
all: no equatorial spread F, no plasma bubbles or irregularities, no Rayleigh-Taylor instability, no
scintillation, no travelling ionospheric disturbance. The phenomena this software is actually about
have no rows to bind to.

**Geomagnetic Storms** is the one row that warranted a real look, and it is rejected. `run_model`
accepts an `ap` argument, and `ap` is a geomagnetic activity index — but it enters only as a driver
of the empirical neutral atmosphere and wind models, exactly as `f107` does. Nothing in the project's
documentation, in the overview paper's applications, or in its own worked example (`ap: 0`) is
storm-time; all are quiet-time.

Two further traces were checked and neither changes the answer. The word "storm" occurs exactly once
in the pinned tree, in a header comment of `sami2py/fortran/dwm07b.f90` describing DWM07 as a model
of "upper thermospheric storm-induced " winds — and that file is vendored but not built: `setup.py`
compiles `nrlmsise00_modified.f`, `grid-1.00.f`, `sami2py-1.00.f`, `hwm93.f`, `hwm07e_modified.f90`,
`apexcord.f90` and `hwm14.f90`, and `dwm07b.f90` is not among them. Recorded so that a future refresh
meets both the `ap` parameter and the DWM07 file already reasoned about rather than treating either
as a new discovery.

This value should be revisited only if the vocabulary gains ionospheric rows — that, and not new
evidence about sami2py, is what would change the answer.

### 23. Development Status (RECOMMENDED)
**Value:** Inactive

The vocabulary's own definition of Inactive is "The project has reached a stable, usable state but is
no longer being actively developed; support/maintenance will be provided as time allows." Each half
of that is separately true here.

*Stable and usable:* ten tagged releases culminating in v0.3.0, a published overview paper, a
documented API, a CI matrix across three operating systems, and distribution through Zenodo with DOIs.

*No longer actively developed:* the newest commit anywhere in this release lineage is `b796fae` on
`develop`, dated 2023-06-27; `main` has not moved since the v0.3.0 release commit on 2022-11-03.

**Read the activity signal from commits, not from a "last updated" rendering.** The GitHub API
reports an `updated_at` for this repository that advances with stars, watches and other non-code
events, and a previous assessment of this field concluded "Active" from exactly such a rendering.
`pushed_at` (2023-06-27) matches the `develop` tip and is the honest field; better still is the
commit history itself, which is what was read here.

**Rejected alternatives, each on its definition:**

- **Active** ("being actively developed") — contradicted by the commit history above.
- **Unsupported** ("the author(s) have ceased all work on it") — too strong, and the evidence is
  against it. The repository is **not archived** (`"archived": false`), so it remains open to issues
  and pull requests, and it carries open issues rather than a wind-down notice. An archived
  repository would be `Unsupported`; this one is quiet but open, which is what `Inactive` describes.
- **Moved** — nothing designates a successor location. The `sami2py_vis` package named in the
  changelog took only the plotting functions, and (see Field 30) has no public repository at all.
- **Abandoned**, **Suspended**, **WIP**, **Concept** — all four presuppose a project that never
  reached a stable usable release. This one made ten.

This field held no value at all before this refresh.

### 24. Documentation (RECOMMENDED)
**Value:** https://sami2py.readthedocs.io

The project's user documentation: an eight-page Sphinx site (introduction, installation, sample
workflow, modifications from SAMI2-1.00, contributing) built from `docs/` and served by ReadTheDocs.
The README carries its build badge, and `docs/introduction.rst` and `docs/installation.rst` are the
canonical statements of what the software is and how to compile it.

This exact URL form — `https`, no trailing path — is the one the PyHC community registry records for
this package, and it is preferred over the `http` form the project's own badge target uses: `http`
redirects to `https` and there is no reason to publish the pre-redirect address.

**The GitHub wiki was probed and deliberately not used here.** A repository wiki is a separate git
repository, so its absence from the code tree proves nothing; this one was cloned
(`https://github.com/sami2py/sami2py.wiki.git`, head `fb0aff877af49e08ce2a1cc5d6ff67decd0713f7`,
2022-09-26) and it does have real content — twelve pages, all Markdown, mostly an Application
Usability Level (AUL) self-assessment (`AUL1`–`AUL9` plus `AUL_docs`) alongside `Home` and a short
`Development-roadmap`. It is project-planning and maturity-assessment
material, not user documentation: it explains who the intended users are and how the project rates
itself against the AUL framework, and it would not help someone trying to install or run the model.
Recorded so a future refresh does not have to rediscover the wiki, and does not mistake it for a
second documentation site.

The wiki is cited elsewhere in this file as *evidence*, which is a different matter: it is the
clearest statement of the project's own design requirements, including the intent to "Load and return
the resultant modeled ionosphere via an `xarray` object" and the role of the `growin` package.

### 25. Funder (OPTIONAL)
**Value:** Not found

**No funder is recorded, and the emptiness is a decision rather than a gap.** Two independent things
produce it: the repository names no sponsor at all, and the one funding statement that does exist
anywhere in this software's paper trail funds *people*, not this software.

**The repository states no funding anywhere in its history.** That is a controlled negative, not an
unchecked one: a search of the entire pinned commit lineage for any commit that added or removed the
strings `NNH20`, `AGS-` or `Funding` returns nothing, while an identical search for `SAMI2` returns
commits — so the instrument works. No funding file was ever deleted, and no acknowledgements section
in `README.rst` or the docs names a sponsor. The only acknowledgement the project asks for is
attribution, not funding: `README.rst` asks that users state "This work uses the SAMI2 ionosphere
model written and developed by the Naval Research Laboratory."

The only remaining candidate source is the software's own reference publication (Field 14). Its
Funding section is six sentences, and all six are quoted here because the shape of the whole section
is what the decision turns on — the section runs unbroken to the article's `Conflict of interest`
block, with no intervening heading:

> JK and AH are supported by the Space Precipitation Impacts project at Goddard Space Flight Center
> through the Heliophysics Internal Science Funding Model. JS is supported by NASA NNH20ZDA001N-NASA.
> The research of JH was supported by NSF (AGS-1931415). AB is supported by the Office of Naval
> Research. This work uses the SAMI2 ionosphere model written and developed at the Naval Research
> Laboratory. The sami2py Python model is freely available to the community at
> www.github.com/sami2py/sami2py.

Note for anyone quoting these two acknowledgement sentences: the paper writes the model was "written
and developed **at** the Naval Research Laboratory", while the project's own `README.rst` writes
"written and developed **by**". They are two different sentences from two different sources and each
should be attributed to the one it came from.

**Why none of it is recordable here.** The governing rule is the agent guidance under Field 26 in
`resource_submission_form_fields.md`, which applies equally to this field: funding metadata
"flattens distinct tiers into one undifferentiated list — support for the software's authors, an
input mission's own funding, and a validation-only data service's funding can all appear together.
Record only what funded *this software*". The named tier there — "support for the software's
authors" — is exactly and exhaustively what this statement contains. Every one of its four funding
clauses is of the form *person X is supported by Y*: "JK and AH are supported by…", "JS is supported
by…", "The research of JH was supported by…", "AB is supported by…". Not one names sami2py, a grant
made to the project, or work paid for on this package. A searcher filtering HSSI by funder is asking
which awards paid for the software; answering with the salary lines of four individuals would give a
wrong answer to that question.

Two specific points make the reading firm, and both cost work to establish, so they are recorded
rather than left to be rediscovered:

- **AH is not a sami2py author at all.** The Space Precipitation Impacts project supports "JK and
  AH" — Alexa Halford, who is a co-author of the *paper* but appears nowhere in the software's
  creator list (Field 6). The paper's own Author Contributions places her at "JS and AH wrote
  sections of the manuscript", with no code contribution. So the only link SPI ever had to this
  software ran through JK, in his capacity as a person it employs.
- **NSF was never admissible on separate grounds, which still hold.** The statement reads "The
  research of JH was supported by NSF (AGS-1931415)", and Author Contributions records JH as "the
  original author (with Dr. Glenn Joyce) of the FORTRAN SAMI2 code" — that is, of the *predecessor
  model* sami2py wraps, written two decades before this package existed. Funding an input to this
  software is not funding this software. This reason is independent of the person-versus-software
  reasoning above and would exclude NSF even if that reasoning were ever revisited.

**Considered and not recorded, with the research preserved.** Two funders were proposed for this
entry on the strength of the paper's Funding section, and the identifiers resolved for them are
kept here so that a refresh which reopens the question does not repeat the lookups:

- **National Aeronautics and Space Administration**, ROR `https://ror.org/027ka1x80`, proposed on the
  basis that the two people who wrote the software are both NASA-supported — Author Contributions:
  "JK and JS wrote the Python interface to SAMI2, as well as modified the FORTRAN code" — JK through
  the Space Precipitation Impacts project at Goddard and JS through NASA NNH20ZDA001N. Crossref
  independently records NASA (FundRef `10.13039/100000104`) as this article's sole asserted funder,
  which is a reminder that Crossref reports the *paper's* funding and not the software's.
- **Office of Naval Research**, ROR `https://ror.org/00rk2pe57`, proposed for AB, whose contribution
  was to this software rather than to its predecessor: "AB contributed to overall design and
  interface of the code, as well as the integration into the pysat ecosystem." The ROR resolution is
  worth keeping whatever happens to the value: a ROR query for that name returns **two**
  organisations with the identical name, and the United States body is `00rk2pe57` while
  `https://ror.org/01awap711` is the identically named United Kingdom body. The US row is the correct
  one for this paper, since Burrell's affiliation is the United States Naval Research Laboratory.
  Anyone re-proposing this funder must not pick the UK row.

Both were considered against the person-versus-software rule and **not determinative**: the evidence
that these bodies support these individuals is sound, and it is simply not evidence about who funded
the software. Recorded this way so a later refresh can see the case was made and settled rather than
missed.

### 26. Award Title (OPTIONAL)
**Value:** Not found

No award is recorded, for the reason set out in Field 25: the sole funding statement in this
software's paper trail supports individuals rather than this software, so there is no award to name.
Three identifiers appear in that statement and each was examined; none is recordable, and each is
kept here because each is an inviting candidate that a later pass would otherwise re-examine from
scratch.

- **Space Precipitation Impacts** — the only one of the three that is an award *title* at all, and
  the one previously proposed for this field. It is a real, correctly named thing: "JK and AH are
  supported by the Space Precipitation Impacts project at Goddard Space Flight Center through the
  Heliophysics Internal Science Funding Model", i.e. an internal NASA Goddard project funded through
  HISFM, which is why it has a project name and no external grant number. It is not recorded because
  it is support for two named people, one of whom (AH) is not a sami2py author at all — see Field 25.
  Considered and not determinative, not refuted.
- **NNH20ZDA001N** — cited as "JS is supported by NASA NNH20ZDA001N-NASA", and a documented trap. It
  is a NASA ROSES *solicitation* number — the identifier of the annual omnibus announcement — not the
  title or number of a specific award, and the element funding JS is not identified. Recording it
  would publish a solicitation identifier as though it were a grant. This objection is independent of
  everything else in these two fields and survives any future change of view about them.
- **AGS-1931415** — a National Science Foundation award number, excluded for the prior reason set out
  in Field 25: it funded J. D. Huba's SAMI2 research, not sami2py. Note additionally that the award
  number alone would not be enough even if that changed — an award needs a title to be recordable,
  and the paper gives none, so it would have to be looked up.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Publication 1:** https://doi.org/10.1029/2000JA000035
Huba, J.D., G. Joyce, and J.A. Fedder (2000), "Sami2 is Another Model of the Ionosphere (SAMI2): A
new low‐latitude ionosphere model", *J. Geophys. Res.*, 105, 23035-23053.

**Publication 2:** https://doi.org/10.1029/2010GL043671
Emmert, J.T., J.L. Lean, and J.M. Picone (2010), "Record-low thermospheric density during the 2008
solar minimum", *Geophys. Res. Lett.*, 37.

**Publication 3:** https://doi.org/10.5194/angeo-31-2147-2013
Klenzing, J., A. G. Burrell, R. A. Heelis, J. D. Huba, R. Pfaff, and F. Simões (2013), "Exploring the
role of ionospheric drivers during the extreme solar minimum of 2008", *Ann. Geophys.*, 31, 2147-2156.

These three are the publications the developers themselves prioritise. They are the References
section of `README.rst` at the pin minus its fourth entry (the software's own Zenodo citation, which
belongs to Field 2), they are the whole References section of `docs/introduction.rst` at the pin, and
they are listed a third time in the project wiki's AUL1 page as "The fundamental research justifying
this work". Each is load-bearing rather than decorative, and the repository says which is which:
Huba et al. (2000) is the model the software runs, Emmert et al. (2010) is the source of the
exospheric-temperature scaling for extreme solar minimum that this implementation added, and
Klenzing et al. (2013) is the MATLAB-era study this Python implementation is "based on".

One later addition to that list is accounted for rather than omitted: on the `develop` branch the
References section of `docs/introduction.rst` gains a fourth entry, the overview paper
`10.3389/fspas.2022.1066480`. That paper is not recorded here because it is this software's reference
publication and is recorded in Field 14 — which is where the project itself now points users, and
where a reader looking for it will find it.

**Huba et al. (2000) belongs here and not in Field 14**, and the placement already held in HSSI is
correct. The project's citation instruction is conjunctive — it asks for the original paper "as well
as the package" — so the foundational model paper is an additional citation, not the software's
reference publication. The full reasoning is written out under Field 14; it is cross-referenced here
because this is the field a future agent will be looking at when tempted to move it.

**Considered and not added: the papers that cite sami2py.** Independent studies do use and cite it —
for instance "Altitudinal Variation of O+ Scale Height at the Equatorial Topside Ionosphere"
(`10.1029/2024JA033033`) and "Storm‐Time Strip‐Like Plasma Density Bulges at
Middle Latitudes Shaped by Meridional Wind Gradients" (`10.1029/2025JA034786`), both of which cite Klenzing et al. (2022)
substantively rather than in passing. None is recorded, because this field is for publications "the
software developer prioritizes", and the developers' prioritised list is the one above. Admitting
third-party citing papers would turn a curated list into an unbounded and permanently stale one.

**Also considered and not added:** Stoneback et al. (2018), the pysat paper, which the overview paper
cites when describing the pysat integration. It is pysat's reference publication, not sami2py's, and
the relationship it documents is already recorded as software in Field 30.

### 28. Related Datasets (OPTIONAL)
**Value:** https://doi.org/10.5281/zenodo.7182786

"sami2py sample output files" — Klenzing, J. and J. M. Smith (2022), Zenodo, CC-BY-4.0, published
2022-10-10. Four netCDF files (`solarmin_fejer.nc`, `standard_solarmin.nc`, `modified_solarmin.nc`,
`solarmin_cnofs.nc`).

This is the software's own companion dataset and the association is asserted by the dataset itself,
not inferred: its description reads "Example output datasets generated by the sami2py model", it
names the repository `https://github.com/sami2py/sami2py` and the software's concept DOI
`https://doi.org/10.5281/zenodo.2875799`, its keywords are `ionosphere` and `sami2`, and its authors
are two of the software's own. It is also the dataset backing the figures of the reference
publication, whose Data Availability Statement reads "The data sets generated for the figures in this
study can be found at zenodo: https://doi.org/10.5281/zenodo.7182786."

The **concept** DOI is recorded rather than the version DOI `10.5281/zenodo.7182787`, for the same
reason as in Field 2: it survives a later deposit.

This field held nothing before this refresh, and the dataset is not discoverable from the repository
at all — nothing in the pinned tree mentions it. It was found through the reference publication's
data statement, which is where a future refresh should look for its successor if one appears.

### 29. Related Software (OPTIONAL)
**Values:**
- https://doi.org/10.5281/zenodo.4527592
- https://github.com/space-physics/msise00
- https://github.com/space-physics/hwm93

**`10.5281/zenodo.4527592` — SAMI2, the original NRL Fortran model.** This is the single most
informative relation this entry can carry: sami2py *is* a Python wrapper around this code. The
concept DOI belongs to the Naval Research Laboratory's own release
(`NRL-Plasma-Physics-Division/SAMI2`, v1.00, authored by jdhuba and Steve Richardson), and the
vendored copy in this repository is that version — `sami2py/fortran/sami2py-1.00.f`, alongside
`README-1.00` and `param-1.00.inc`. The relationship is stated by the project in its own words: the
wiki's AUL3 page claims "This is the first open source wrapper for the sami2 model", the paper's
author contributions record that "JH is the original author (with Dr. Glenn Joyce) of the FORTRAN
SAMI2 code", and `docs/modifications.rst` exists solely to enumerate how this implementation departs
from SAMI2-1.00. Field 29 explicitly covers "software this work was forked from"; this is that.

Note for a future refresh: `docs/introduction.rst` points at
`https://www.nrl.navy.mil/ppd/branches/6790/sami2` as the home of "The open-source fortran version of
SAMI2". The Zenodo DOI above is preferred over that page — it is a persistent identifier, it names a
specific version, and it is the form this field asks for.

**`space-physics/msise00` and `space-physics/hwm93`** are recorded on the strength of Field 29's own
defining example — "two software that model the upper atmosphere of Earth" — combined with a
concrete, unusually direct connection: sami2py does not merely resemble these, it *runs the same
models*. NRLMSISe-00 supplies its neutral atmosphere (`docs/modifications.rst`: "This version uses the
official release of NRLMSISe-00"), and HWM93 is one of the three wind models a user can select
through the `hwm_model` keyword.

The distinction that keeps this honest, and that a future refresh should not lose: **sami2py vendors
its own Fortran sources** (`nrlmsise00_modified.f`, `hwm93.f`) rather than depending on these Python
packages. It will never import them. The relation is shared underlying model, which is exactly what
"performs similar tasks but does not necessarily link together" describes — and it is useful in the
direction it is published, since a sami2py user who wants to interrogate the neutral atmosphere or
the wind field on its own is well served by being pointed at standalone implementations. Each URL is
the one HSSI already holds for that entry, so the link lands on the catalogue's own record rather
than a parallel address.

**Considered and not selected:**

- **HWM-14.** This is the awkward one and deserves its reason on the record, because it is the wind
  model sami2py uses *by default* ("Sami2py uses the HWM-14 model by default.") while HWM-93, which
  is listed above, is only an option. It is omitted because there is no good URL for it. The
  catalogue carries no HWM-14 entry to point at, and the nearest public implementation has moved
  organisations (`space-physics/hwm14` now redirects elsewhere), so recording it would mean
  publishing a fragile third-party address for a package the project never names and does not use.
  The relation recorded for HWM-93 should not be read as a claim that it is the more important of the
  two.
- **DWM07 and the Fejer-Scherliess drift model**, both bundled (`dwm07b.f90`; the default drift
  model). Same reason as HWM-14 — no citable software artifact. DWM07 is the weaker candidate of the
  two in any case: its source file ships in the tree but is absent from `setup.py`'s compile list, so
  it is carried rather than used. A refactoring of the Fejer-Scherliess
  drift code does exist as a third-party repository describing itself as "Refactored from sami2py
  development team", but sami2py's own sources never mention it and the relation is asserted only
  from the other side.
- **EUVAC** and the apex-coordinate routine (`apexcord.f90`) — components of the bundled Fortran
  with no independent software identity at all.
- **numpy, scipy, pandas** (`requirements.txt` / `setup.cfg`) — generic scientific-Python
  infrastructure. Being a dependency is not a relation worth cataloguing, and listing them would say
  nothing that is not equally true of most of the catalogue. A previous version of this entry's
  metadata listed all of these under this field; they are excluded now under the rule, not by
  preference.
- **netCDF4** — likewise excluded. It is the engine under `xarray.Dataset.to_netcdf` and is never
  used directly; the software exposes no netCDF4 API of its own.

### 30. Interoperable Software (OPTIONAL)
**Values:**
- https://github.com/pysat/pysat
- https://doi.org/10.5281/zenodo.6567104
- https://doi.org/10.5281/zenodo.3678865

Each entry below rests on a specific, cited exchange, not on co-residence in a Python environment.

**pysat** (`https://github.com/pysat/pysat`, the URL HSSI already holds for that entry). The
reference publication devotes a titled subsection to it — "2.4 Integration into the pysat ecosystem"
— and states the exchange in one sentence: "The netCDF4 versions of the file are constructed to be
compatible with pysat." sami2py's output format is deliberately shaped so another named heliophysics
tool can consume it, which is the definition of a demonstrated exchange.

**pysatModels** (concept DOI `10.5281/zenodo.6567104`; Burrell, Klenzing and Stoneback). The
strongest of the three, because the adapter exists and lives in the other package: the paper states
that sami2py files "can be integrated into the pysat ecosystem by using the custom sami2py instrument
module at pysatModels". A module in pysatModels named for and written against this software is a
plugin relationship. `docs/sample_workflow.rst` says the same from this side — a saved run "can then
be loaded via xarray or pysatModels". The concept DOI is recorded rather than the v0.1.0 DOI the
paper happens to cite.

**growin** (concept DOI `10.5281/zenodo.3678865`; Smith and Klenzing). A downstream consumer that
sami2py has a feature *for*. The wiki's AUL1 page describes it plainly — "The `growin` software
package (in development) uses the output from `sami2py` to calculate Rayleigh-Taylor Instability
growth rates for a given ionosphere" — and it is named in the overview paper's own abstract. The
exchange is concrete and one-directional: `docs/sample_workflow.rst` presents the `outn` switch as being for
applications that require neutral density data, naming the `growin` package and linking its
repository, with the effect that the model will "output neutral parameters alongside the ions". A feature added to serve a
named partner package is interoperability in the plainest sense.

**Considered and rejected:**

- **xarray** (concept DOI `10.5281/zenodo.598201`) — the close call in this field, weighed in full
  and decided against, so the evidence is kept rather than discarded. xarray is a Tier B package,
  admissible only if a specific documented-interchange condition is met, and that condition *is* met
  here: the public API *returns* an xarray object as its user-facing data container, and the project
  documents it as such. `docs/sample_workflow.rst` states "The data is stored as `ModelRun.data`,
  which is an `xarray.Dataset`.", the project's own requirements list in the wiki's AUL2 page
  includes "Load and return the resultant modeled ionosphere via an `xarray` object.", the wiki's
  AUL1 page records "The software provides easy access to output data through xarray (implemented as
  of v0.2.0)", and `Model.to_netcdf()` is a thin pass-through to `xarray.Dataset.to_netcdf`. Anyone
  combining sami2py with another tool does it through that object. Against that: a visitor browsing
  this field is looking for domain peers a sami2py user could actually pair the model with, not for
  the array library underneath the data container, and on that reading xarray is infrastructure
  rather than an interoperating tool. That is the view taken, and it settles the field at three
  entries. The Tier B evidence above is recorded intact and is not withdrawn — it was considered and
  not determinative, and a later refresh should treat the question as asked and answered rather than
  rediscovering the `xarray.Dataset` return type and proposing the entry afresh.
- **`sami2py_vis`** — and this one is a correction rather than a judgement call. CHANGELOG.md for
  v0.3.0 records "Remove deprecated plotting functions (moved to `sami2py_vis`)", and a previous
  version of this entry's metadata proposed `sami2py_vis` as this field's value on that basis.
  **There is no such public package.** `https://github.com/sami2py/sami2py_vis` returns 404, and a
  GitHub repository search for `sami2py_vis OR sami2py-vis` returns zero results. This field requires
  a DOI or repository URL and there is nothing to point at. Recorded rather than quietly dropped,
  because the changelog line is prominent and invites exactly this entry: a future agent reading it
  should know the package was searched for and not found, and should re-check only if it is published.
  (This has a second consequence, treated in Field 4: the plotting capability left sami2py and did not
  land anywhere the catalogue can reach.)
- **numpy, scipy, pandas** — Tier A generic infrastructure, excluded without exception. These would
  be equally at home in a finance model or a biology pipeline, which is the test.
- **netCDF4** — Tier B, and the condition is not met. It is an implementation detail beneath
  `to_netcdf`; the software documents no exchange with it, and users never touch it directly.
- **MATLAB** — considered because `README.rst` says "This implementation is based on the matlab
  version used in Klenzing et al [3]_." That is historical provenance, not interoperability: there is
  no MATLAB bridge, no `.m` file and no import path. The relationship it points to is a publication,
  and that publication is recorded in Field 27.
- **pysatCDF** and the rest of the pysat family — only pysat itself and pysatModels are named in the
  project's own sources. Ecosystem membership is not, on its own, a demonstrated interoperation.

### 31. Related Instruments (OPTIONAL)
**Value:** Not found

sami2py is instrument-agnostic by construction, and a reader can check that against its interface:
`run_model()` takes dates, a longitude, grid parameters, `f107`, `f107a`, `ap`, model-selection
switches and optional Fourier coefficients. It reads no instrument's data product, implements no
instrument-specific format or convention, and calibrates nothing. Nobody working with a particular
instrument's data would reach for it, and a visitor to any instrument's page would find it out of
place.

**Considered and rejected, so the search is not repeated.** The reference publication does name
instruments and missions, and each mention is the kind the relevance gate excludes:

- **CINDI** (the Coupled Ion-Neutral Dynamics Investigation) and **C/NOFS** — the paper's Figure 5
  shows a run "driven by custom drift climatology fit to C/NOFS data". This is the textbook
  "configurable for" case: the software accepts *Fourier coefficients*, which a user may have derived
  from anything. sami2py never reads C/NOFS or CINDI data and contains no code that knows what they
  are. A different published fit would substitute for it without changing a line of the software.
- **ICON** and **COSMIC2** — mentioned only in describing what *pysat*, a different package, has been
  used for operationally.
- **Jicamarca** — a single passing mention in the paper's discussion.

None of these appears anywhere in the repository at the pin.

### 32. Related Observatories (OPTIONAL)
**Value:** Not found

The same reasoning as Field 31, and for the same missions and ground facilities. A model that
generates a synthetic ionosphere from empirical drivers supports no observatory in particular; it
supports none specifically, rather than all of them.

No value is recorded as a matter of correctness rather than difficulty. There was no ambiguous or
unresolvable candidate here to fall back from — nothing passed the relevance gate in the first place,
so no observatory-level substitution question arises.

### 33. Logo (OPTIONAL)
**Value:** Not found

The project has no logo. This is a documented absence backed by four independent checks rather than a
failure to look:

- **No image is tracked in the repository** — not at the pinned revision and not on `develop` either.
  A listing of both trees contains no `.png`, `.svg`, `.jpg` or `.ico` file and no path containing
  "logo", against a control confirming the listings themselves are populated.
- **The documentation defines none.** `docs/conf.py` sets `html_theme = 'sphinx_rtd_theme'` and no
  `html_logo` or `html_favicon`, so the ReadTheDocs site renders with the theme default.
- **The PyHC community registry entry carries no `logo:` field**, though its schema supports one and
  other packages populate it.
- **The GitHub organisation avatar is not a logo.** It is worth naming explicitly, because it is the
  one plausible-looking candidate and it fetches cleanly as a real PNG (420×420, `image/png`,
  1,551 bytes) from `https://avatars.githubusercontent.com/u/53580261?v=4`. Viewed, it is GitHub's
  auto-generated identicon — the symmetric pink-on-grey block pattern GitHub derives from an account
  id for accounts that never uploaded a picture. It carries no design and no relation to this
  software. Recording it would put a meaningless image on the entry and imply the project chose it.

No logo is a correct outcome, and inventing or substituting one would not be.
