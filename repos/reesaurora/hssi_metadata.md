# HSSI Metadata Extraction Results

**HSSI Software ID:** e126690a-c368-4677-892e-116126ea8c8a
**Repository:** https://github.com/space-physics/reesaurora
**Source Revision:** f209bb35dbaf62d191f9eb32e7611d85f232e383
**Extraction Date:** 2026-09-02
**Validation Date:** 2026-09-03
**Validation Status:** PASS

---

**Scope note — this repository is archived, and that changes how its evidence reads.** The GitHub
repository is archived (read-only; it accepts no issues and no pull requests), so the pinned revision
`f209bb35dbaf62d191f9eb32e7611d85f232e383` (2021-04-27) is not merely the current tip of `main` — it
is the software's **final state**. Every "current" statement below is therefore also a durable one:
while the repository remains archived, no later commit can supersede it. The repository's own wiki
does not exist as a repository (`<repo>.wiki.git` is not found), so GitHub's `has_wiki` flag carries
no documentation here. Eight commits separate the last released tag `v1.0.5` (2018-07-30) from this
final revision, so the archived tree is later than anything ever released — the shape "released,
then development continued quietly and was never released again." Several fields below turn on that
gap.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The bracketed placeholder is this catalogue's convention for an entry whose metadata was compiled by
a curator rather than supplied by the software's own maintainer. It is not a missing value.

### 2. Persistent Identifier (RECOMMENDED)
**Concept DOI:** https://doi.org/10.5281/zenodo.595438

This is a genuine Zenodo **concept** DOI, not a version DOI. Zenodo's record for the deposit reports
`conceptdoi` `10.5281/zenodo.595438` and `conceptrecid` `595438`, and the DataCite record for that
DOI carries four `HasVersion` relations — `10.5281/zenodo.556833`, `10.5281/zenodo.556916`,
`10.5281/zenodo.1308184` and `10.5281/zenodo.1323860` — of which the last is the v1.0.5 version DOI
recorded in Field 12. Concept DOI in Field 2 and version DOI in Field 12 is the correct arrangement;
do not swap them.

The deposit is an automated GitHub–Zenodo release deposit rather than a manual upload: its
`related_identifiers` contain `{"identifier": "https://github.com/scivision/reesaurora/tree/v1.0.5",
"relation": "isSupplementTo", "scheme": "url"}`, and a `tree/<tag>` URL of that shape is the
integration's signature. The URL names the repository's former `scivision` organization, which is
era-correct for a 2018 deposit and now redirects to `space-physics` (see Field 3).

**Trap for a future refresh — do not autofill authorship from this DOI.** DataCite's record parses
the creator string "Michael Hirsch, Ph.D." into `givenName` "Ph.D." and `familyName` "Michael Hirsch",
i.e. inverted and with the degree suffix promoted to a given name. Field 6 below records the correct
form; a DOI-driven autofill would corrupt it.

### 3. Code Repository (MANDATORY)
**Repository URL:** https://github.com/space-physics/reesaurora

Confirmed as the canonical form. The repository was created 2015-06-02 under the `scivision`
organization and later moved to `space-physics`; `https://github.com/scivision/reesaurora` resolves
by HTTP 301 to the `space-physics` form recorded here, so the older URL still works but is not
canonical. `setup.cfg` at the pin already declares the `space-physics` URL, as does the PyHC registry
entry. PyPI's stored `home_page` for the distribution is still the old `scivision` form — that is
frozen 2018 release metadata, not a competing current value.

The repository is not a fork (`fork: false`), so this is the origin of the code, not a mirror.

### 4. Software Functionality (RECOMMENDED)
**Values:**
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Physics-Based
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots

Written in the canonical `Parent: Child` form. Each child's parent is listed alongside it, as the
taxonomy requires. Thirteen child names in this vocabulary recur under more than one parent
(`Analysis` and `Processing` among them), so the two entries above are specifically the
**Data Processing and Analysis** children, not the same-named **Mission-related** ones.

**Evidence for each value.**

- **Models and Simulations / Empirical.** The README states the model "is essentially a *parameter
  fit* to more advanced models, making for convenient computation in this energy range with the PCs
  of the early 1990s." That is literally an empirical parameterisation, and the code shows it. The
  albedo and dissipation-function routines interpolate tabulated coefficient sets over `log10(E)`
  with `scipy.interpolate.interp1d`, and the electron-range routine is a closed-form empirical power
  law in energy; all three are fits taken from Sergienko & Ivanov (1993), one of whose tables
  `reesaurora/__init__.py` marks `# %% Table 1 Sergienko & Ivanov 1993, rightmost column`.
- **Models and Simulations / Physics-Based.** Semi-empirical physics, which is what this
  subcategory covers as distinct from first principles: energy degradation of a precipitating
  electron beam through an integrated neutral-mass column, a per-species mean energy cost per
  ion-electron pair (`E_cost_ion = {"N2": 36.8, "O2": 28.2, "O": 26.8}`), species partitioning
  weights, and an ionospheric albedo correction.
- **Data Processing and Analysis / Analysis.** The package derives physical quantities beyond the
  raw model output — the albedo flux fraction, the pitch-angle-dependent electron range, and the
  dissipation function — each exposed as a public function (`albedo`, `PitchAngle_range`,
  `lambda_comp`) that a user can call directly.
- **Data Processing and Analysis / Processing.** The model consumes an `xarray.Dataset` of neutral
  densities and transforms it into an ionization-rate array: `partition()` rescales number densities
  from m^-3 to cm^-3 and applies the species weights, and `energy_deg()` integrates the mass-density
  column downward to build the scattering depth. This is the weakest of the nine — it is a catch-all
  — but the transformation chain is real and user-facing.
- **Data Visualization / 2D Graphics.** `reesaurora/plots.py` is a dedicated plotting module inside
  the package. `plotA` draws a log-scaled colour map of production rate over the (energy, altitude)
  plane: `hi = ax.pcolormesh(E, z, Qs, vmin=vlim[0], vmax=vlim[1], norm=LogNorm())`, with a labelled
  colourbar. The README embeds exactly such a figure.
- **Data Visualization / Line Plots.** `fig7`, `fig8`, `fig11`, `fig12` and `fig13` in the same
  module each build families of `ax.plot` lines — for example
  `        ax.plot(W[i, :], z, label="{:.0f}".format(e))` in `fig7` — giving altitude profiles of
  energy deposition and ionization rate, fitting parameters versus energy, and albedo and range
  versus energy.

**Caveat on the visualization entries, recorded so a later reader is not surprised.** The plotting
entry points reference the model output's altitude coordinate as `Q.altkm`, while `reesiono` returns
a `DataArray` whose dimension is named `alt_km`; the command-line figure helpers `makefig11`,
`makefig12` and `makefig13` likewise pass an `fn=` keyword those functions no longer accept — for
instance `    Lambda_m = lambda_comp(chi, Eplot, isotropic=False, fn=datfn)[0]` and
`    af_m = albedo(E, isotropic=False, fn=datfn)` — and all three are commented out of `main()`.
The visualization capability is nevertheless a real, user-facing part of what the package offers — a
dedicated plotting module, a documented `--vlim` plotting option, and a README figure produced by it
— so it is classified on the capability the software provides rather than on the condition of its
final unreleased commit. That is a claim about intent and design, not a warranty that the plotting
paths run as written; see Field 24 for the wider pattern of the archived tree's internal drift.

**Considered and rejected, with reasons — recorded so these are not re-proposed.**

- **Models and Simulations: First Principles — rejected.** The README positions this model as the
  opposite: it is a fit *to* more advanced models, and "Today, much more advanced physics-based
  models are tractable on a PC." (the sentence is broken by a line wrap in the source, joined here).
  There is no transport equation, kinetic solver or Monte Carlo here;
  the expensive physics was pre-computed by others and reduced to interpolation tables.
- **Models and Simulations: Theory — rejected.** This subcategory is for analytical solutions and
  theoretical frameworks. The package is a numerical implementation of a published parameterisation,
  and contributes no analysis of its own.
- **Models and Simulations: Forward-Fitting — rejected.** The package is a pure forward model: no
  optimiser, no inversion, no goodness-of-fit metric anywhere in the code. What it produces —
  ionization profiles resolved by monoenergetic beam energy, written out as an "eigenprofile" file —
  is the forward operator that a *separate* inversion consumes. `reesaurora/auxillary_rees.py`
  preserves the downstream step as commented-out pseudocode (`q = A.dot(Phi)`), which is a matrix
  product, not a fit. Enabling someone else's inversion is not performing one.
  **`reesaurora/auxillary_rees.py` contributes no functionality to any field.** Read whole, the file
  is a shebang, a single `isotropic = False` assignment, a module-level string literal holding the
  discussion and the `References:` block, and one function, `reesmodel`, that is commented out in
  its entirety along with a commented sketch of Wedlund 2013 Eqns 1-4. Nothing in it executes, so it
  must never be credited with behaviour in Field 4 or Field 8. It remains a legitimate source for
  the reference block quoted in Field 27.
- **Data Processing and Analysis: Energy Spectra — rejected, and this is the closest call.** The
  argument for it is real: energy is the model's principal independent variable
  (`loadaltenergrid` in `reesaurora/__init__.py` builds its default beam grid as
  `E = np.logspace(1.72, 4.25, num=81, base=10)`), the output is differential in beam energy, the
  command-line help for the output file reads `"give hdf5 filename to save eigenprofile production"`,
  and the paper the code cites most prominently is about estimating precipitating electron energy
  spectra. The argument against is the parent category: this subcategory sits under **Data**
  Processing and Analysis, and the software processes no measured data at all. Its energy axis is a
  model parameter grid the caller supplies, never a spectrum derived from an observation. A user
  filtering for energy-spectrum computation wants a tool that turns measurements into a spectrum;
  this turns a spectrum-shaped grid into altitude profiles. Rejected on that discriminator.
- **Data Processing and Analysis: Pitch Angle Distributions — rejected, and the function name is a
  trap.** `PitchAngle_range(E, isotropic)` returns an electron **range** (a stopping depth in
  g cm^-2), not a pitch-angle distribution. The `isotropic` flag selects between two precomputed
  parameterisations — isotropic and field-aligned — rather than computing any distribution.
- **Data Processing and Analysis: Data Access and Retrieval — rejected.** The model obtains its
  neutral atmosphere by calling `msise00.rungtd1d` in process. That is a model evaluation, not a
  retrieval from an archive; nothing here contacts a remote data service. See Field 17.
- **Data Processing and Analysis: Time Series Analysis — rejected.** `reesiono` loops over an array
  of times and stacks the results, but performs no temporal analysis of any kind.
- **Models and Simulations: Data Guided — rejected.** No observational data enters the model. Its
  only external input is another model's output, and the figure helper that exercises the
  atmosphere directly supplies fixed synthetic indices, passing `f107a=150.0,`, `f107=150.0,` and
  `ap=4.0,` as separate arguments.
- **Models and Simulations: Forecasting — rejected.** The model runs for a user-specified epoch with
  no predictive element.
- **Coordinate Transforms (whole branch) — rejected.** Geodetic latitude and longitude are passed
  straight through to the atmosphere model; nothing is transformed between frames.
- **Mission-related and Servers and Environments (whole branches) — rejected.** The package is
  mission-agnostic (see Fields 31 and 32) and ships no container, server or parallel-execution
  facility.
- The other subcategories under the three selected parents have no counterpart in this 19-file
  package. They include, among others, 2D Slices, 3D Particle Distribution Processing, Calibration,
  Curlometer, Data Assimilation, Data Reduction, File Format Conversion, Image Processing, Linear
  Gradient Estimation, Magnetic Null Finding, Packet Decommutation, Plasma Moments, Spectrogram,
  Wave Polarization Analysis and Wavelet Analysis under Data Processing and Analysis; 3D Graphics,
  Hodograms, Movies, Orbit Plots, Spacecraft Formation Plots and Web-Based under Data Visualization;
  and MHD, Field-line Tracing, Instrument Response and Observatory/Instrument Models under Models
  and Simulations. The ML/AI and Mission-Specific children present under several parents are
  likewise inapplicable throughout.

### 5. Related Region (RECOMMENDED)
**Values:**
- Earth Atmosphere
- Earth Ionosphere
- Earth Auroral Subregion
- Earth Thermosphere

**All four regions are recorded: `Earth Atmosphere`, which HSSI held before this refresh, together
with the three more specific rows added alongside it.** Dropping the coarse row in favour of the
three specific ones was considered and declined — the per-row argument below gives the reason, and
the vocabulary's shape, described next, is why the coarse row is not made redundant by the fine
ones.

The Region vocabulary is **flat**: no row is a parent or child of any other, so selecting a fine
region does not implicitly select a coarse one, and selecting `Earth Atmosphere` does not make the
entry findable under `Earth Ionosphere`. An argument of the form "Earth Atmosphere already
encompasses the ionosphere" is therefore wrong about how this field behaves, and must not be used to
justify leaving the specific rows off.

Per-row argument, framed from the position of someone browsing HSSI by region:

- **Earth Ionosphere — strongest case.** The author's own one-line summary in `setup.cfg` is
  `description = Rees-Sergienko-Ivanov Model of Earth ionosphere.` The model's output is the
  electron production (ionization) rate profile, which *is* the auroral ionosphere's source term.
  Anyone filtering for ionospheric software would be glad to find this and puzzled by its absence.
- **Earth Auroral Subregion — equally strong, and more precise than any other row.** The software is
  restricted to auroral latitudes by an explicit guard: `if abs(glat) < 45.0:` followed by
  `logging.error("This model was intended for auroral precipitation.")`. The package name, the
  README title, the GitHub topic (`aurora`) and the PyHC description all name the aurora. This is
  the row that most exactly describes what the model is for.
- **Earth Thermosphere — well supported.** The model's altitude grid runs from 80-90 km (the
  command line defaults `--minalt` to 80.0 km, the library function `loadaltenergrid` defaults
  `minalt: float = 90`) up to a hard cap at the assumed 700 km electron source
  (`]  # keeps original spacing, but with heights less than source at 700km`). That interval is the
  thermosphere. The neutral background the model deposits energy into — N2, O and O2 number
  densities from MSISE-00 — is thermospheric composition, and the ionization rate is computed
  species by species against it. Someone working on thermospheric energy deposition would want this
  result.
- **Earth Atmosphere — the region HSSI held before this refresh; defensible, but broad.** It is not
  wrong: the physics is energy deposition into Earth's neutral atmosphere. The field guidance directs
  preferring the most specific applicable region rather than *defaulting* to one of the legacy five,
  and this value had been recorded as such a default. Having now been examined rather than assumed,
  it remains applicable, and dropping it would only narrow discovery without improving correctness —
  so it is kept alongside the three specific rows. Removing it in favour of maximum precision was the
  alternative considered, and it was declined for that reason: it would have cost discovery and
  bought no correctness.

**Considered and rejected:** `Earth Lower and Middle Atmosphere`. The grid bottoms out at the
mesopause and the model does nothing meaningful below it — auroral electrons of 100-10,000 eV stop
well above that altitude. A visitor filtering for lower- and middle-atmosphere software would find an
auroral precipitation model out of place. The nineteen further rows — every magnetospheric, solar,
heliospheric and planetary region in the vocabulary — have no bearing on a terrestrial
upper-atmosphere model.

**The order these four values are stored in is deliberate, because this field's order is stored.**
Related Region is a sorted many-to-many relation: the order the values are given in is retained, and
it is the order the catalogue displays. The order recorded for this entry is `Earth Atmosphere`,
`Earth Ionosphere`, `Earth Auroral Subregion`, `Earth Thermosphere` — coarse first, so that the
`Earth Atmosphere` row HSSI already held keeps the sort position it already had and the three
specific rows are appended after it. The change is therefore additive in display as well as in
content: nothing already stored is displaced. The bulleted list at the head of this field is written
in that same coarse-first order, so the list and the recorded order agree. Several other
multi-valued fields here need no such care, being plain many-to-many relations that do not preserve
the order values are given in at all: Programming Language (13), Input File Formats (18),
Keywords (16), Related Publications (27) and Interoperable Software (30). Their list order is
presentational in the stronger sense of never being stored.

### 6. Authors (MANDATORY)

#### Author 1:
- **Author:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** https://ror.org/05qwgg493
- **Affiliation 2:**
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found

Sole author. `setup.cfg` at the pin gives `author = Michael Hirsch, Ph.D`, the Zenodo deposit gives
`{"name": "Michael Hirsch, Ph.D.", "affiliation": "SciVision, Inc."}`, and the Apache header atop
`reesaurora/__init__.py` reads `Copyright 2020 Michael Hirsch, Ph.D.`. The academic-degree suffix is
correctly normalised away in the recorded name; it is a credential, not part of a family name.

**The ORCID is independently corroborated, not inherited.** The Zenodo and DataCite deposits carry no
name identifier at all (`nameIdentifiers` is empty), so the identifier did not come from the DOI.
ORCID's public record for `0000-0002-1637-6526` gives given name "Michael", family name "Hirsch", and
a single employment: Boston University, department "ECE", role "Research Scientist". That employment
is also the source of the Boston University affiliation, whose ROR `https://ror.org/05qwgg493` is
confirmed as the exact ROR for Boston University (and not for Boston University Academy, Boston
University Brussels, or the University of Massachusetts Boston, all of which are separate ROR
records).

**Negative research — Scivision, Inc. has no ROR, and there is a false match to avoid.** A ROR search
for "SciVision" returns exactly one organization: `https://ror.org/011qev639`, **SciVision Biotech
Inc. (Taiwan)**, a Taiwanese biotechnology company with no connection to this author or this
software. Attaching it would be a factual error. The empty affiliation identifier is correct and
should stay empty until a genuine ROR for this organization exists.

A capitalisation difference exists between the recorded `Scivision, Inc.` and the source records'
`SciVision, Inc.`. Organization rows are shared across the catalogue, so this is not resolvable from
one software entry, and it is deliberately left alone rather than fixed here.

**Model authorship is not software authorship.** The names Rees, Sergienko, Ivanov, Gustavsson and
Brändström appear throughout this dossier as the originators of the physics and of the predecessor
implementation. None of them wrote this software, and none of them belongs in Field 6. They are
recorded in Fields 27 and 29 instead, which is where credit for the underlying model and the
predecessor code belongs.

**Name-collision warning — never state a "Rees" count from a name-keyed search.** In this tree the
surname collides with the package name itself, so a case-insensitive search for `rees` conflates
three unrelated senses and a bare tally of it is meaningless. Attributing every matching line
individually (method: `git show <pin>:<path> | grep -in 'rees'` run per tracked non-binary file,
counting matching *lines*, not occurrences) gives twenty-six lines in three groups. The **person**
M. H. Rees, cited as `Rees 1989`, accounts for exactly two: `ReesSerginekoIvanov.py:39` and
`reesaurora/auxillary_rees.py:16`. That this is M. H. Rees is corroborated by Field 27's
`https://doi.org/10.1017/CBO9780511573118`, which Crossref gives as M. H. Rees, 1989, *Physics and
Chemistry of the Upper Atmosphere*. The **model name** "Rees-Sergienko-Ivanov", or the lower-case
"rees model", accounts for four: `README.md:1`, `README.md:9`, `setup.cfg:7`, and
`ReesSerginekoIvanov.py:177`, whose argparse description is
`"rees model of excitation rates for the aurora"`. The remaining twenty are package, module,
function, filename and badge-URL **identifiers** —
`reesaurora`, `reesiono`, `runrees`, `reesmodel`, `rees_model`, the CLI script's filename, the
README's PyPI and CI badge URLs, and `.mypy.ini`'s `files = reesaurora/` path. Any sentence of the
form "the tree references Rees N times" is uninterpretable unless it names which sense and the
counting method, and the trap is that a validator checking such a claim would reach for the same
search that manufactured it. Apply the same discipline to `Sergienko` and `Ivanov`: check each
match's parent before writing any claim about them.

### 7. Software Name (MANDATORY)
**Name:** ReesAurora

This is the display name curated in the PyHC registry (`name: ReesAurora` in
`_data/projects_unevaluated.yml`). The Python distribution and the repository both use the lower-case
`reesaurora`, and the README's own title is `# Rees-Sergienko-Ivanov Auroral model`. The mixed-case
registry form is preferred as a human-facing catalogue name: it is legible, it is what the community
registry publishes, and it does not falsely imply a lower-case package is the software's proper
title. The full descriptive title is preserved in Field 8's opening sentence rather than being forced
into this field.

### 8. Description (MANDATORY)
**Description:** Rees-Sergienko-Ivanov model of excitation rates, relevant to auroral optical
emissions. This physics-based model simulates auroral electron precipitation and ionization processes
in Earth's ionosphere. The model is designed for electron energies in the range of 100-10,000 eV and
uses the MSISE-00 atmospheric model to generate O, O2, and N2 densities. It calculates the ionization
profiles and volume emission rates as a function of altitude resulting from primary electron
precipitation on the neutral atmospheric background. The model is based on work by Gustavsson and
Brandstrom (AIDA_TOOLS) and implements the approach described in Sergienko and Ivanov (1993).

Each factual claim in this text is corroborated at the pinned tree:

| Claim | Source at the pin |
|---|---|
| "excitation rates, relevant to auroral optical emissions" | README, `Rees-Sergienko-Ivanov model of excitation rates, relevant to auroral` / `optical emissions inspired/based upon Gustavsson / Brandstrom et al`; the quoted phrase also appears in the GitHub repository description and in the PyHC registry entry |
| "100-10,000 eV" | README, `Model designed for **100 - 10,000 eV**, and is essentially a *parameter`; code warning `"Sergienko & Ivanov 1993 covered E in [100,10000] eV"` |
| "uses the MSISE-00 atmospheric model to generate O, O2, and N2 densities" | README, `Uses MSISE-00 to generate O, O~2~, N~2~ densities, and models outcome of`; `from msise00 import rungtd1d` and `species = ["N2", "O", "O2"]` |
| "primary electron precipitation on the neutral atmospheric background" | README, `primary electron precipitation on this neutral background.` |
| "based on work by Gustavsson and Brandstrom (AIDA_TOOLS)" | `reesaurora/__init__.py`, `a massively speeded up implementation after the AIDA_TOOLS package by Gustavsson, Brandstrom, et al` |
| "implements the approach described in Sergienko and Ivanov (1993)" | `reesaurora/__init__.py`, `After Sergienko and Ivanov 1993` |

**Decision on `O2` / `N2` — they are kept plain, not converted to Unicode subscripts.** Three
reasons, all from the position of a site visitor. Unicode subscript characters are not reliably
rendered in every font the catalogue's pages and exports pass through; a reader copying the text out
gets characters that break in plain-text contexts; and, most concretely, a visitor searching the
catalogue for "N2" or "O2" matches the plain form and misses a subscripted one. The repository's own
README writes `O~2~, N~2~`, which is Markdown subscript syntax that GitHub does not render — so the
source offers no authority for the typographic form either way, and the plain ASCII spelling is the
safer choice. An earlier version of this dossier used subscripted forms; they are deliberately not
carried forward.

**The unaccented `Brandstrom` stands; the accented `Brändström` was researched and declined.** This
is a person's name and the description's spelling omits both of its diacritics, so the discrepancy is
real, was noticed, and is recorded here rather than left to be rediscovered. The accented form is
well evidenced: the Crossref author list for `https://doi.org/10.1002/jgra.50347`, the DOI already
recorded in Field 27, gives "U. Brändström" as a co-author alongside "B. Gustavsson" — the same two
people the AIDA_TOOLS attribution names. Note both vowels: an a-umlaut first and an o-umlaut second,
which is easy to get half-right; a previous version of this dossier rendered it "Brandström",
carrying only the second.

The correction was nevertheless declined, on a stated principle rather than for want of evidence.
This description is derived from the project's own README and `reesaurora/__init__.py`, which write
the ASCII `Brandstrom` throughout, and the catalogue follows the software's own spelling of its
attribution over a better-documented external form. The Crossref evidence is kept visible precisely
so that a later refresh recognises it as a decision already taken against it, rather than as a fresh
finding to apply.

**An addition considered and not made.** The description calls the model "physics-based", which is
accurate in the Field 4 sense of semi-empirical physics, but sits in mild tension with how the README
itself frames the software — "essentially a *parameter fit* to more advanced models", superseded by
models that `physics-based models are tractable on a PC.` today. Field 8 asks for the assumptions the
software makes, and that framing is exactly the information a prospective user needs to judge fitness
for their work, so a sentence to that effect would have been a defensible addition. It was not made:
the existing description is not wrong, and rewording a maintainer-derived description without cause
is not an improvement.

### 9. Concise Description (OPTIONAL)
**Concise Description:** Rees-Sergienko-Ivanov model of auroral excitation rates and ionization
profiles for electron precipitation in Earth's ionosphere (100-10,000 eV range).

151 characters, at the low end of the 150-200 character target. It is a faithful compression of
Field 8 that keeps the four facts a preview most needs: the model's identity, what it computes,
where, and its valid energy range. Retained as written; no wording change is warranted.

### 10. Publication Date (RECOMMENDED)
**Date:** 2015-06-02

The date the code first became public. Two independent sources agree: the repository's initial commit
`b3798b4e2c38d637d2fb3532d2b83da16691111f`, dated 2015-06-02, and GitHub's repository `created_at`
of `2015-06-02T16:00:31Z`. Their agreement matters — a repository created empty and pushed later
would show a gap between the two, and this one does not.

**Alternative considered and rejected:** the first PyPI release, `reesaurora-1.0.1.tar.gz`, uploaded
2017-04-24. That is the first *packaged* release, not the first publication of the software; Field 10
asks for the date of first publication for the initial version, and public availability of the source
began nearly two years earlier.

### 11. Publisher (RECOMMENDED)

#### Publisher:
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Correct per the field's own rule: for software whose DOI was obtained through the GitHub-Zenodo
workflow, Zenodo is the publisher. That this deposit came through the integration rather than a
manual upload is established in Field 2. DataCite independently reports `publisher: "Zenodo"`.

The identifier is the Zenodo URL rather than a ROR. The field permits a URL where no ROR applies, and
the URL is the form the field's own guidance gives for Zenodo. The Organization row is shared across
the catalogue and is not this entry's to rename.

### 12. Version (RECOMMENDED)

#### Version Information:
- **Version Number:** v1.0.5
- **Version Date:** 2018-07-30
- **Version Description:** Update selftest, cleanup prereqs.
- **Version PID:** https://doi.org/10.5281/zenodo.1323860

**v1.0.5 is the last release, and there is no later version to record.** Its tag resolves to
`47cbaf661b025be773e525c08bec8161f5d39ce7`, confirmed by `git merge-base --is-ancestor` to lie on the
pinned revision's own lineage — a check worth repeating, because tags in this GitHub organization can
sit on pre-rewrite orphan branches that a naive all-refs log would surface as if they were current
history. All four tags in this repository (`v1.0.0`, `v1.0.1`, `v1.0.4`, `v1.0.5`) are ancestors of
the pin.

Three sources agree on the date: the tag commit (2018-07-30), the GitHub release
`published_at 2018-07-30T20:03:13Z`, and the PyPI sdist upload at `2018-07-30T20:04:37Z` —
eighty-four seconds apart, consistent with an automated release. The version PID is the Zenodo
version DOI, distinct from the concept DOI in Field 2.

Eight commits follow the tag, ending at the archived final revision. Their subjects are `ci
template`, `ci=>actions, black formatting`, `CI: install gfortran`, `meta`, `ci revert install
compiler`, `meta`, `cleanup`, and `update xarray`. None bumped the version: `setup.cfg` at the pin
still declares `version = 1.0.5`. So the archived tree is genuinely later than the released one, but
no release exists to describe it, and inventing a version string for it would be fabrication.

PyPI holds releases 1.0.1, 1.0.3, 1.0.4 and 1.0.5, with 1.0.5 latest. Note the imperfect
correspondence with git tags — 1.0.3 has no tag, and tag `v1.0.0` has no PyPI release — so neither
list is a complete release history on its own. Package identity on PyPI is confirmed by its
`home_page` pointing at this repository's former URL and its `summary` matching `setup.cfg`'s
`description` exactly.

**The version description asserts only what v1.0.5's own release notes say, and that was chosen over
two fuller alternatives.** The recorded text is the v1.0.5 GitHub release's own title, punctuated as
a sentence. GitHub records that release's body as empty, so the title is the whole of what the
release itself says about its contents.

The two alternatives, and why they lost. The version description HSSI held before this refresh
carried a second sentence that paraphrased the release body of **v1.0.4** — GitHub records v1.0.4's
body as "Pep8, more selftests, mypy type check, update MSIS API" — and so attributed one release's
notes to another; inheriting it was rejected as a misattribution. The other alternative was to
synthesise a description from what actually landed between the two tags: the eleven commits in that
range cover PEP 8 formatting, f-strings, refreshed self-test reference values for an updated MSIS
API, dependency cleanup and CI changes, so "Pep8" and "updated MSIS API" are defensible for v1.0.5,
while "additional self-tests" and "mypy type checking" belong to v1.0.4. A description grounded
entirely in that range would have read: *"Update selftest, cleanup prereqs. Refreshes the self-test
reference values against an updated MSIS API, applies PEP 8 formatting and f-strings, and trims the
declared prerequisites."* That was declined too, and is recorded as a rejected alternative rather
than a standing option: a version description should report what the release says about itself, not a
curator's reading of a commit range presented as the project's release note.

### 13. Programming Language (RECOMMENDED)
**Languages:**
- Python 3.x

**`MATLAB` is not recorded as a language of this software. HSSI held a `MATLAB` value in this field
before this refresh; the two cases below were weighed against each other and it was dropped.**

`Python 3.x` is beyond dispute. Every module in the package is Python — the sole exception in the
tree is the MATLAB file discussed below, which defines nothing. `setup.cfg` declares
`python_requires = >= 3.7` and the classifier `Programming Language :: Python :: 3`, and the CI
workflow builds against Python 3 on all three platforms.

**The case for keeping MATLAB.** One MATLAB file exists in the tree at the pin:
`reesaurora/tests/test.m`. It opens with a link to MathWorks' documentation on passing data to Python
from MATLAB, which shows an intended cross-language bridge. The author demonstrably does ship real
MATLAB elsewhere — the sibling package `msise00`, a hard dependency of this one, describes itself as
"NRL MSISE-00 atmospheric model-- in Python and Matlab". And `.gitattributes` carries a
`*.m text eol=lf` rule, so the file is a recognised part of the repository's tooling.

**The case for dropping it, which is stronger.** The file is thirteen lines long, and its own body
prints `disp('not working, perhaps a limitation of Matlab right now')` — the author's explicit
statement that it does not work. Its single import,
`import reesaurora.rees_model.loadaltenergrid`, names a module `reesaurora.rees_model` that does not
exist at the pin; the function lives in `reesaurora/__init__.py`. That module was renamed away by
commit `5663dd8` on 2016-09-20, so the stub has referenced a nonexistent path since 2016 — roughly
two years before the v1.0.5 release, and years before the repository was archived — and it was never
fixed. Nothing exercises it, and the complete configuration graph confirms that rather than merely
suggesting it. The CI workflow's only checks are `flake8`, `mypy` and `pytest`; `.mypy.ini`'s
`files = reesaurora/` is a directory glob that does reach the file's directory, but mypy type-checks
Python only, and `.flake8` likewise lints Python only. Nor does the file ship: `reesaurora/tests/`
contains no `__init__.py`, so `packages = find:` does not discover it as a package, and there is no
`MANIFEST.in` for `include_package_data = True` to act on. The README, `setup.cfg` and the PyPI
classifiers never mention MATLAB. Field 13 asks for the languages **most important** for the
software and states explicitly that it is not meant to be exhaustive.

**Decided from the searcher's side.** Someone filtering HSSI for MATLAB software is looking for
software they can use from MATLAB. They would arrive at a thirteen-line stub that cannot resolve its
own import and that the author labelled as not working. That result breaks the filter's promise,
and the entry is better without it. Recording this reasoning matters because the mere presence of a
`.m` file will tempt a future refresh to add MATLAB back.

**Not a language of this software — deliberately excluded.** The README's installation note that a
Fortran compiler such as gfortran is required refers to building the **msise00** dependency, not
this package: `pyproject.toml`'s build requirements carry the comment
`# numpy is for msise00 prereq`, and there is no Fortran source anywhere in the nineteen tracked
files at the pin. No Fortran row belongs in this field. (The vocabulary offers only version-specific
Fortran rows in any case, and nothing here would select among them.)

### 14. Reference Publication (OPTIONAL)
**Reference Publication:** Not found

**Negative research, dated 2026-09-02: no publication describes this software.** A full-text search
of the ADS/SciX corpus for the exact string `reesaurora` returns zero records. The search was
validated in both directions: a nonsense token returns zero (so the query form is not silently
failing), and the same full-text query for the sibling package name `msise00` returns hundreds of
records (so the index does cover software names of this kind). There is no software paper, no JOSS
submission, and no article that names the package. A future refresh should not spend effort
re-deriving this.

**Sergienko & Ivanov (1993) does not occupy this field.** Whether the model's originating citation
belongs here was asked and settled: it does not. The paper is recorded in Field 27 only, and Field 14
stays empty.

The case for putting it here: Field 14 describes a publication sometimes used as the preferred
citation for the software in addition to the version-specific citation to the code itself, and a
scientist who used ReesAurora would properly cite Sergienko & Ivanov (1993) for the model it
implements.

The case against, which decided it, is decisive on two counts. First, Field 14 is specified as a DOI,
and this paper has none — ADS returns no DOI for bibcode `1993AnGeo..11..717S`, and a Crossref
bibliographic search on its exact title surfaces no matching record either. Whatever is put here
would not be a DOI, and the field drives a citation display that expects one to resolve. Second, and
independently, the paper describes the *model*, not the *software*; it predates this implementation
by twenty-two years and cannot describe it. Taken with the negative research above — no publication
describes this software at all — there is no candidate for this field. The full citation and a
permanent link are recorded in Field 27 instead, where a non-DOI permanent link is explicitly
allowed — so nothing is lost by leaving this field empty.

### 15. License (RECOMMENDED)
**License:** Apache License 2.0

This is the exact spelling of the row in the controlled `License` vocabulary; the list is closed, and
a name that is not one of its rows is rejected outright.

**Field 15 has no per-software License URI, so none is recorded.** The submission form displays a
License URI sub-field, but the licence is a reference to a shared licence record that carries its own
URL — there is no software-specific licence URI in storage, and one that differed from the shared
record's URL would be doubly unwritable. The repository's `LICENSE.txt` and the Apache 2.0 header
atop `reesaurora/__init__.py` are cited below as *evidence*, not as a value for this field. A prior
version of this dossier recorded `https://www.apache.org/licenses/LICENSE-2.0` as a License URI; that
line has been removed as unstorable.

**Positive evidence at the pin.** Three artifacts in the final tree agree, and GitHub's derived
metadata concurs: `LICENSE.txt` contains the Apache License, Version 2.0; `setup.cfg` declares
`license_files =` with `LICENSE.txt`; `reesaurora/__init__.py` opens with
`Copyright 2020 Michael Hirsch, Ph.D.` followed by the standard Apache 2.0 boilerplate; and GitHub's
repository-level licence detection reports SPDX `Apache-2.0`. Because the repository is archived,
this is not merely the current licence — it is the final one.

**Licence history — the durable reason third-party records disagree, and the specific wrong edit this
prevents.** The licence file's content changed twice on this lineage:

| Commit | Date | Licence in the file |
|---|---|---|
| `b3798b4e2c38d637d2fb3532d2b83da16691111f` | 2015-06-02 (initial commit) | GNU General Public License Version 3 |
| `79b27a01379e4ad86582b9f1089382436f817ca1` | 2018-03-08 | GNU **Affero** General Public License Version 3 |
| `e1aa20b468b650f76bb49145e492192c42b3d498` | 2019-09-25 | unchanged — this commit **renamed** `LICENSE` to `LICENSE.txt` without touching its content (both paths resolve to blob `dbbe3558157f5861bff35dcb37b328b679b0ccfd`) |
| `6ca253ffcc3102061ec50a02f7c6432045126dda` | 2020-02-20 | replaced with **Apache License 2.0** — this is the relicensing commit |

The 2019 rename is easy to mistake for the relicensing, because it is where the filename in the
current tree first appears. It is not; the content is byte-identical across it.

**The released version was AGPL-3.0, proved at the artifact rather than by tracing commits.** Tag
`v1.0.5` resolves to `47cbaf661b025be773e525c08bec8161f5d39ce7`, dated 2018-07-30 and confirmed to be
on the pin's lineage. At that commit the licence file is named `LICENSE` and its first two lines read
`GNU AFFERO GENERAL PUBLIC LICENSE` / `Version 3, 19 November 2007`. That is the tree Field 12
records, the tree the version DOI points at, and the tree the single PyPI artifact for that version,
`reesaurora-1.0.5.tar.gz` (uploaded 2018-07-30T20:04:37), was built from. Two corroborations tie the
Zenodo deposit to that same era: it is dated 2018-07-30, the day of the tag, and its
`isSupplementTo` target `https://github.com/scivision/reesaurora/tree/v1.0.5` names the repository's
former organization. So Zenodo's `license: {"id": "other-open"}` is an accurate, if imprecise, record
of an AGPL-era artifact rather than a careless entry — and DataCite's `rightsList` of "Open Access"
with `info:eu-repo/semantics/openAccess` says nothing more specific.

**Ruled out by name: `GNU General Public License v3.0 or later`.** This is the wrong edit a future
refresh is most likely to make — an agent reads Zenodo's `other-open` or unpacks the 1.0.5 artifact,
concludes AGPL-3.0, finds that the vocabulary contains no Affero row (it has four GPL-family rows,
none of them Affero), and takes GPL-3.0-or-later as the obvious near-match. It fails on two
independent grounds. **(a)** AGPL-3.0 is not GPL-3.0. The Affero network-use clause is the entire
reason the licence exists separately, so recording GPL-3.0-or-later would be a substantively wrong
statement about the terms v1.0.5 was distributed under, not a rounding. **(b)** More fundamentally,
Field 15 records the software's current licence, and the current — and, the repository being
archived, final — state of the tree is Apache-2.0. The AGPL era is history that explains the
divergent third-party records; it is not a competing candidate for this field.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Keywords:**
- ionosphere
- aurora
- atmospheric science
- ionosphere_thermosphere_mesosphere
- auroral optical emissions
- electron precipitation
- excitation rates
- physics-based model
- atmospheric ionization

Recorded in the lower-case form in which they are stored; the catalogue's display renders them
title-cased, which is presentation, not the value. Comparisons in a later refresh should be made
against the stored lower-case strings.

Provenance: `ionosphere` and `aurora` are the two keywords `setup.cfg` itself declares.
`atmospheric science` derives from its classifier `Topic :: Scientific/Engineering :: Atmospheric
Science`. `ionosphere_thermosphere_mesosphere` comes from the PyHC registry entry's
`keywords: ["ionosphere_thermosphere_mesosphere","specific"]`. The remaining four are descriptive
terms drawn from the README and the code, supported by Field 8's evidence table.

**Verdict on `ionosphere_thermosphere_mesosphere`: it earns its place; keep it.** The concept is a
genuine science-domain label — ITM is how the ionosphere-thermosphere-mesosphere community names its
own domain — and this software genuinely is an ionosphere and thermosphere model, so the term is
descriptive rather than merely inherited. The underscore rendering is a registry tag shape rather
than natural language, which is the main thing against it. Two facts settle the balance. First, the
Keyword vocabulary is open and already contains **both** this underscore-joined row and a
space-separated `ionosphere thermosphere mesosphere` row for the same concept; the useful thing a
dossier can do is record that, so a future refresh reuses one of the existing rows rather than
minting a third variant. Second, switching between two equivalent existing rows would be churn on a
shared row with no benefit to a reader. Keep as stored.

**The `specific` tag from the same PyHC entry is deliberately not recorded.** It is a registry
classification of the package's scope, not a science keyword, and would tell a catalogue visitor
nothing.

**`atmospheric ionization` is recorded, and was added in this refresh.** A row with that name
already existed in the vocabulary, so no new row was minted. The argument for it: the model's central
computed quantity is the ionization rate profile, and before this refresh none of the entry's
keywords carried the word "ionization" — a visitor searching that term would have missed an entry
that is precisely about what the software computes. The argument against, weighed and outweighed:
Field 16 asks for keywords not already supported by other metadata fields, and the concept is
arguably implied by `electron precipitation` and by Field 5's ionospheric regions. It was judged a
small, low-risk gain in discovery, and taken.

**Note on two stored keywords that overlap other fields.** `physics-based model` restates Field 4's
`Models and Simulations: Physics-Based`, and `ionosphere` overlaps Field 5's `Earth Ionosphere`.
Neither was removed: both are harmless, both aid free-text search, and `ionosphere` in
particular is one of the two keywords the author declared in `setup.cfg`.

### 17. Data Sources (OPTIONAL)
**Data Sources:** None — evidenced empty.

This is an examined result, not an unfilled field. The software retrieves no data from anywhere.
Its atmospheric input is produced by calling `msise00.rungtd1d` in process — a model evaluation, not
a retrieval — and its remaining inputs are a time, a geodetic coordinate pair, an altitude grid and
an energy grid, all supplied by the caller or by command-line flags. No Python file at the pin
contains a network call (`requests`, `urllib`, `http`, `socket`) or a file-opening call, so nothing
here reaches an archive.

Every row of the `DataInput` vocabulary was weighed against that: AMDA, CDAWeb, das2, FTP/FTPS
Directories, GFZ, HAPI, HTTP/HTTPS Directories, Madrigal, Observatory/Mission-specific, OMNIWeb,
S3/Cloud-aware, SSCWeb, TAP, The Virtual Solar Observatory., VirES and WDC all name remote data
services, archives or access protocols, and the software contacts none of them.
`Observatory/Mission-specific` fails for the further reason given in Fields 31 and 32 — there is no
observatory or mission to name.

**`Other` was considered and rejected.** The field's instruction to select `Other` when a source is
not listed presupposes that the software supports *some* input source. Selecting it here would tell a
visitor that the software ingests data from an unspecified place, which is false and less
informative than an empty field.

### 18. Input File Formats (RECOMMENDED)
**Formats:** None — evidenced empty.

**`HDF5` is not recorded as an input format. HSSI held an `HDF5` value in this field before this
refresh; it was removed, for the reasons below.**

That value rested on the bundled parameter file `data/SergienkoIvanov.h5`, which is shipped in the
repository and passed as a `datfn` argument through the model's public entry points. The problem is
that **at the pinned revision the software never opens it.** The evidence is mechanical and mutually
reinforcing:

- `h5py` appears in no tracked non-binary file at the pin, and no Python file at the pin contains
  any file-opening call. The claim is only as good as the pattern behind it, so the pattern is
  stated here and deliberately covers more than the HDF5 case: a case-insensitive match for
  `open(`, `.open(`, `open_dataset`, `open_mfdataset`, `load(`, `np.load`, `loadtxt`, `genfromtxt`,
  `loadmat`, `read_<name>(`, `File(`, `Dataset(`, `h5py`, `netCDF4`, `pickle`, `json.load`,
  `read_text`, `read_bytes`, `fromfile` and `io.` returns nothing across every `.py` file in the
  tree.
- `datfn` appears in `reesaurora/__init__.py` only in function signatures — `reesiono`'s parameter
  list, and `E: np.ndarray, iono: xarray.Dataset, isotropic: bool, datfn: Path, verbose: bool` on
  `ionization_profile_from_flux`. Neither function body ever references it.
- **The HDF5 input path is not merely unexercised; it is unreachable.** `albedo` and `lambda_comp`
  declare no `fn` parameter at all — `def albedo(E: np.ndarray, isotropic: int | bool) -> np.ndarray:`
  and `def lambda_comp(hi: np.ndarray, E: np.ndarray, isotropic: bool) -> np.ndarray:` — yet the
  command-line figure helpers `makefig11`, `makefig12` and `makefig13` call them with `fn=datfn`
  (quoted in Field 4). Those calls would raise `TypeError`, not quietly ignore the argument. And
  those are exactly the three the author commented out of `main()`, alongside `makefig7`, leaving
  only `makefig8(datfn)` live — and `makefig8` routes through `reesiono`, where the argument is
  simply dropped. So no execution path reaches a file read, and the pattern of comment-outs is
  evidence that the author knew which calls no longer worked.
- The coefficient tables the file would supply are instead hard-coded as literal arrays in `albedo()`
  and `lambda_comp()`. The correspondence is exact, not approximate: the file's `albedo/E` dataset
  has 21 elements and matches the inlined `logE_p = np.append(1.69, np.arange(1.8, 3.7 + 0.1, 0.1))`
  to floating-point tolerance; `albedo/flux` is (2, 21) matching the inlined `Param` array;
  `monodirectional/C` is (4, 21) matching `Param_m`; and `isotropic/C` is (4, 14) matching `Param_i`,
  whose energy axis `logE_i` likewise has 14 elements. Spot-checked values agree element for element.
- The inlining predates the release: at tag `v1.0.5`, `albedo` and `lambda_comp` already took no file
  argument, and `h5py` was already absent from the code. The `fn=datfn` keyword that the command-line
  figure helpers still pass is a survival from the earlier design in which the coefficients *were*
  loaded from HDF5.

So `data/SergienkoIvanov.h5` is a vestigial data file, and the software supports no input file format
at all. Field 18's own instruction is that only formats actually supported should be indicated, and a
visitor filtering for software that ingests HDF5 would find one that cannot read a single byte of it.
Recording the field as empty is the accurate result, and recording *why* it is empty is what stops a
future refresh re-adding HDF5 on the strength of the bundled `.h5` file's mere presence.

The model's actual user-facing inputs are not files: a time, a geodetic latitude and longitude, an
altitude grid and an energy grid.

### 19. Output File Formats (RECOMMENDED)
**Formats:**
- HDF5

Solidly evidenced, and unaffected by the Field 18 finding. The command line exposes
`"-o", "--outfn", help="give hdf5 filename to save eigenprofile production"`, the README documents it
as `* `-o` specify output file (HDF5)`, and the write is performed by
`gridaurora.writeeigen.writeeigen`, which the model's driver imports and calls. That function refuses
any path whose suffix is not `.h5` and writes through `h5py.File(fn, "w")`, creating datasets for the
sensor location, energy bins, altitude grid and production rates. HDF5 is the software's only output
file format.

### 20. Operating System (RECOMMENDED)
**Operating Systems:**
- Linux
- Mac
- Windows
- Operating System Independent

Note the exact row spelling `Operating System Independent`; the abbreviated `OS Independent` is not a
value in this vocabulary and would be rejected, despite being what `setup.cfg`'s classifier says.

Two kinds of evidence support the four values. The three named platforms are each an actual CI job in
`.github/workflows/ci.yml` — `runs-on: ubuntu-latest`, `runs-on: macos-latest` and
`runs-on: windows-latest` — so the package was demonstrably installed and tested on all three. The
cross-platform value reflects the author's own declaration, `setup.cfg`'s classifier
`  Operating System :: OS Independent`, together with the fact that the package is pure Python with
no platform-specific code. Recording both the specific platforms and the independent value is
redundant but harmless, and each is independently sourced.

### 21. CPU Architecture (RECOMMENDED)
**Architecture:**
- CPU Independent

The package is pure Python built on NumPy, SciPy and xarray, with no compiled extension, no
intrinsics, no assembly and no architecture-conditional code path. Nothing in `setup.cfg` or
`pyproject.toml` restricts the architecture.

**Explicitly not a counter-argument:** the README's note that a Fortran compiler such as gfortran is
required is a build-time requirement of the **msise00** dependency, as `pyproject.toml`'s
`# numpy is for msise00 prereq` comment makes clear. A compiler requirement in a dependency is not a
CPU-architecture restriction on this software, and does not justify narrowing this field to specific
architectures.

### 22. Related Phenomena (OPTIONAL)
**Phenomena:** None — evidenced empty.

The `Phenomena` vocabulary is **closed** — unlike Keywords, an unlisted value is rejected rather than
created — and it holds seven rows: Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms,
Solar Corona, Solar Flares, Solar Wind and X-ray emission. The phenomena this software actually
addresses — the aurora, auroral electron precipitation, and atmospheric ionization — have no row
among them. That enumeration is the reason the field is correctly empty: five of the seven rows are
solar, and neither of the remaining two applies.

**`Geomagnetic Storms` considered and rejected.** It is the only unambiguously terrestrial row and
the nearest near-miss, so it deserves an explicit rule-out. The model has no geomagnetic-activity
dependence of its own: it takes a time and a location and applies fixed coefficient tables.
Geomagnetic indices enter only inside the MSISE-00 dependency's own atmosphere calculation, and the
command line does not even expose them. Auroral precipitation is not storm-specific in any case — it
occurs during quiet conditions too.

The field guidance directs that a supported phenomenon with no row belongs in Keywords instead, which
is exactly where `aurora`, `auroral optical emissions` and `electron precipitation` already sit in
Field 16. Nothing is lost by leaving this field empty.

### 23. Development Status (RECOMMENDED)
**Status:** Unsupported

Decided from the stored definitions in the controlled `RepoStatus` vocabulary, quoted from the rows
themselves rather than paraphrased from repostatus.org.

**Why `Unsupported` fits.** Its stored definition reads: "The project has reached a stable, usable
state but the author(s) have ceased all work on it. A new maintainer may be desired." Note the modal
in the second sentence: the row says a new maintainer **may** be desired, not *is* desired. That
misquotation has inverted a Field 23 decision elsewhere in this campaign, because "is desired" reads
as a positive assertion that the author wants a successor — a claim about intent that nothing here
supports. Both clauses of the definition as actually written hold. The project reached a stable,
usable state — four tagged releases, four PyPI releases, a three-platform CI workflow, and a
numerical self-test asserting reference values. And the author has
ceased all work on it: the last commit is 2021-04-27, and the repository has since been **archived**,
which on GitHub makes it read-only and closes it to issues and pull requests. Archiving is an
explicit, deliberate act by the owner; it is the clearest available signal that work has stopped
rather than merely paused.

**Why `Inactive` fails, and why it is the tempting wrong answer.** Its stored definition is "The
project has reached a stable, usable state but is no longer being actively developed;
support/maintenance will be provided as time allows." The first clause matches, which is why this
value looks right at a glance and why a prior version of this dossier recorded it. The second clause
is what disqualifies it: an archived repository is read-only and accepts no issues and no pull
requests, so support and maintenance cannot be provided at all — not "as time allows", but not at
all. `Inactive` promises a visitor a responsiveness that this repository is structurally incapable
of. This is a defect superseded, not a gap filled.

**Why the other six fail.** `Abandoned`, `Suspended` and `WIP` each require that there has **not** yet
been a stable, usable release; four tagged releases and four PyPI releases rule out all three,
whatever else they say about the authors' intent. `Concept` requires minimal or no implementation, or
a repository intended only as a limited example, demo or proof-of-concept — contradicted by a working
model with a numerical self-test. `Active` requires that the project is being actively developed,
contradicted by the archive. `Moved` requires that the project has been moved to a new location whose
version should be considered authoritative; the `scivision` to `space-physics` change was an
organization rename that redirects to *this same repository*, not a move to a successor project, and
no successor is named in the repository, the PyHC registry entry or the DOI records.

**Two traps ruled out explicitly.** `setup.cfg`'s classifier `  Development Status :: 4 - Beta` is a
2018-era PyPI maturity classifier describing the code's completeness, not the repository's
development status, and it is not a `RepoStatus` term. And GitHub's `updated_at` for this repository
is 2023-01-27, nearly two years after the last commit — `updated_at` advances on metadata events such
as archiving, so it is not evidence of commit activity. The commit-activity date is `pushed_at`,
2021-04-27, which agrees with the pinned revision.

### 24. Documentation (RECOMMENDED)
**Documentation URL:** https://github.com/space-physics/reesaurora

The README is the software's entire documentation: it holds the description, the energy range, the
install instructions and a worked command-line example. There is no documentation website, no
ReadTheDocs configuration, no `docs/` directory anywhere in the nineteen tracked files at the pin,
and — as noted in the scope note — no wiki. Field 24 explicitly permits reusing the access URL when
documentation lives with the code, which is the case here.

**One durable characterisation of the archived final state: the README and CI drifted out of sync
with the tree and were never reconciled.** This shows up three times, and it is better understood as
a single condition than as three unrelated pieces of trivia.

1. The README embeds its example figure as `![volume production rate](tests/demo.png)`, but the file
   is at `reesaurora/tests/demo.png`. The tests directory was moved into the package by commit
   `f209bb3`, the final commit before archiving, and the README was not updated with it.
2. The CI workflow inherited the same stale assumption, running `pytest` with
   `      working-directory: tests` — a directory that does not exist at the pin.
3. The README's documented invocation names a file that does not exist. `README.md` line 35 reads
   `python ReesSergienkoIvanov -t 2011-03-15T12:34:56 -c 65 -148`, spelling the scientist's name
   correctly, while the script in the tree is `ReesSerginekoIvanov.py` — "Sergineko". Comparing the
   two strings character by character, the correct `Sergienko` is S-e-r-g-i-**e**-**n**-k-o and the
   filename `Sergineko` is S-e-r-g-i-**n**-**e**-k-o: the transposed letters are `e` and `n`, at
   positions 6 and 7, and the two strings are anagrams of each other. Note that the substring `ei`
   does not occur anywhere in `Sergineko` — an earlier version of this dossier described the
   transposition as `ie` becoming `ei`, which is wrong and was inherited without being checked
   against the strings themselves. The misspelling is confined to that filename:
   `data/SergienkoIvanov.h5` uses the correct spelling.

Because the repository is archived, none of these can now be fixed upstream. They do not disqualify
the README as the documentation link — it remains the only documentation there is, and it correctly
conveys the model's purpose, energy range, install route and options. They do mean that prose
elsewhere in this dossier should describe the command line as *documented* rather than as verified
to run end to end, and Fields 8 and 4 are written with that restraint.

### 25. Funder (OPTIONAL)
**Funder:** None — evidenced empty.

No funding attribution appears in any source available for this software. A search across every
tracked non-binary file at the pin for `fund`, `grant`, `award`, `acknowledg`, `sponsor`, `NSF`,
`NASA`, `AFOSR`, `DARPA`, `ONR`, `AFRL` and `contract no`, case-insensitively, returns matches only
inside the boilerplate of the Apache licence text in `LICENSE.txt` ("Grant of Copyright License",
"hereby grants", and the like) — that is, no funding statement anywhere in the repository's own
content. The Zenodo deposit carries no grant metadata, and DataCite's record for the concept DOI has
`fundingReferences: []`.

**Why this cannot be recovered from the literature either, and should not be attempted.** The
Acknowledgments section of a software's own paper is normally the best source for this field — but
Field 14's negative research establishes that no publication describes or even names this software.
There is no Acknowledgments section belonging to it to mine. The publications in Field 27 are other
people's work: pulling funders out of the Wedlund et al. (2013) acknowledgements would record that
paper's funding, not this software's, which is exactly the conflation the field guidance warns
against. Leave empty.

### 26. Award Title (OPTIONAL)
**Award Title:** None — evidenced empty.
**Award Number:** None — evidenced empty.

Follows directly from Field 25: with no funder identified in the repository, in the DOI records or in
any publication belonging to this software, there is no award to name or number.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Related Publications:**
- https://doi.org/10.1002/jgra.50347
- https://doi.org/10.1017/CBO9780511573118
- https://ui.adsabs.harvard.edu/abs/1993AnGeo..11..717S/abstract

**The third entry was added in this refresh: HSSI held the two DOIs before it, but not the ADS
permalink for Sergienko & Ivanov (1993) — the paper the software actually implements.**

All three are the works the software's own code names as its scientific basis. The identical
three-item `References:` block appears in two files at the pin — `ReesSerginekoIvanov.py` lines
39-41 and `reesaurora/auxillary_rees.py` lines 16-18 — each listing `Rees 1989`, then
`Wedlund et al "Electron Energy Spectra and Auroral Arcs" JGR 2013`, then
`Sergienko and Ivanov 1993 "A new approach to calculate the excitation of atmospheric gases by
auroral electron impact"`. In both files the block sits inside a module-level string literal placed
after an `isotropic` assignment, so it is a free-standing string expression rather than a module
docstring; quoting it as a "docstring" misdescribes the source. Neither the Wedlund line nor the
Sergienko line ends with a full stop — an earlier version of this dossier placed a trailing period
inside the quotation marks for both, which is why neither quotation could be matched against the
tree.

**Full citations, with the correct bibliographic details.**

- **Wedlund et al. (2013)** — `https://doi.org/10.1002/jgra.50347`. Simon Wedlund, C., H. Lamy,
  B. Gustavsson, T. Sergienko and U. Brändström (2013), Estimating energy spectra of electron
  precipitation above auroral arcs from ground-based observations with radar and optics, *Journal of
  Geophysical Research: Space Physics*, 118, 3672-3691, American Geophysical Union.
  **Beware a mis-citation this dossier previously carried.** The repository's docstring names this
  paper as `Wedlund et al "Electron Energy Spectra and Auroral Arcs" JGR 2013`, and an earlier
  version of this file reproduced that short form inside quotation marks as though it were the
  article's title. It is not — it is the code author's shorthand. The title given above is the
  published one, per the DOI record. Quote the short form only when attributing it to the repository
  docstring.
- **Rees (1989)** — `https://doi.org/10.1017/CBO9780511573118`. Rees, M. H., *Physics and Chemistry
  of the Upper Atmosphere*, Cambridge University Press, 1989. This is a monograph, not a journal
  article, and it predates the software by twenty-six years, so it cannot be a publication that cites
  or uses the software. It is retained because the developer's own reference block prioritises it as
  the foundational text for the physics, which is the other purpose this field serves.
- **Sergienko & Ivanov (1993)** — the entry added in this refresh, and the most conspicuous gap in
  what HSSI held before it: it is the paper the software actually implements. Sergienko, T. I., and
  V. E. Ivanov (1993), A new approach to calculate the excitation of atmospheric gases by auroral
  electron impact, *Annales Geophysicae*, 11, 717. ADS bibcode `1993AnGeo..11..717S`. The code cites
  it specifically and repeatedly. A case-insensitive match on `sergienko|ivanov` over
  `reesaurora/__init__.py`, counting matching *lines* rather than occurrences
  (`git show <pin>:reesaurora/__init__.py | grep -inE 'sergienko|ivanov'`), returns seven, and all
  seven are genuine citations of this paper:
  line 17, `After Sergienko and Ivanov 1993`, in the module docstring;
  line 84, `After Sergienko and Ivanov 1993 and Gustavsson AIDA_TOOLs`, in
  `ionization_profile_from_flux`'s docstring;
  lines 87 and 91, `"Sergienko & Ivanov 1993 covered E in [100,10000] eV"` and
  `"Sergienko & Ivanov 1993 assumed electron source was at altitude 700km."`, the two runtime
  messages quoting the paper's stated validity limits in energy and source altitude;
  line 94, `# %% Table 1 Sergienko & Ivanov 1993, rightmost column`, above the ion-cost table;
  line 440, `Implement Eqn 7 Sergienko 1993`, above the species-partitioning routine; and
  line 443, `k: correction factors vs. Monte Carlo for Sergienko 1993`, documenting that routine's
  correction factors.

**The 1993 paper has no DOI, which is why the entry is an ADS permalink.** ADS returns no DOI for
that bibcode, and a Crossref bibliographic search on its exact title surfaces no matching record —
unsurprising for a 1993 *Annales Geophysicae* volume. Field 27 explicitly provides for this case: a
publication with no DOI may use any permanent link, an ADS abstract page being the named example,
with the full citation recorded in the dossier prose, as it is above. The URL is 62 characters, well
inside any length constraint.

**One caveat on verifying that link.** The ADS web interface answers automated requests with an HTTP
405 and a "Human Verification" page regardless of user agent, so the URL cannot be confirmed by a
plain fetch — it renders normally in a browser. The record's existence is confirmed independently
through the ADS API, which returns exactly one document for that bibcode, with the authors, journal,
volume, page and title given above. A future agent should not read the 405 as a broken link.

**Publications that cite or use the software: none, established by dated negative research.** The
same ADS full-text search recorded under Field 14 — the exact string `reesaurora`, zero results on
2026-09-02, with a validated control — covers this field's other purpose too. No article in that
corpus names this package.

### 28. Related Datasets (OPTIONAL)
**Related Datasets:** None — evidenced empty.

The software neither consumes nor produces a published dataset. Two candidates were considered and
rejected. The bundled `data/SergienkoIvanov.h5` is a repository-internal coefficient file with no
DOI, no landing page and no publication as a dataset — and, per Field 18, the code does not even read
it. MSISE-00 is the software's source of atmospheric densities, but it is *software*, not a dataset;
it is recorded in Field 29 where it belongs, and the densities the model consumes are computed at run
time rather than drawn from any archived data product.

### 29. Related Software (OPTIONAL)
**Related Software:**
- https://github.com/space-physics/msise00
- https://github.com/space-physics/gridaurora
- https://github.com/space-physics/AIDA-tools

Each entry is domain-specific and distinguishing — it tells a reader something about *this* software
that would not be equally true of an arbitrary Python package. None would be at home in a web
application, a finance model or a biology pipeline, which is the test the generic-infrastructure
exclusion turns on.

- **msise00** — the NRL MSISE-00 empirical atmosphere, imported directly as
  `from msise00 import rungtd1d`. It supplies the entire neutral background the model deposits energy
  into; without it the model has nothing to ionize. A required, domain-specific dependency of exactly
  the kind Field 29 asks for. MSISE-00 had its own HSSI entry at the time of this refresh, and the
  repository URL recorded here matches the code repository URL stored on that entry, so the raw URL
  the page renders as this relation's link text points a reader at the catalogued record. That is the
  in-catalogue relation convention: point at the target entry's own stored repository URL rather than
  at a DOI, because the raw URL is what a visitor sees and clicks. The reasoning is conditional on
  that display — if the catalogue ever renders resolved titles instead of raw URLs, a DOI would win
  on persistence and the convention should be revisited.
- **gridaurora** — described upstream as "Discretizations of space (grids) useful for aeronomy and
  auroral modeling", and imported four times: `from gridaurora.ztanh import setupz` and
  `from gridaurora.zglow import glowalt` build the altitude grids,
  `from gridaurora.writeeigen import writeeigen` performs the HDF5 write that Field 19 records, and
  `from gridaurora.solarangle import solarzenithangle` supplies the solar zenith angle the driver
  prints. A companion package from the same author, purpose-built for auroral modelling. It had no
  HSSI entry of its own at the time of this refresh, so this entry links outside the catalogue.
- **AIDA-tools** — the predecessor implementation. `reesaurora/__init__.py` describes this package as
  `a massively speeded up implementation after the AIDA_TOOLS package by Gustavsson, Brandstrom, et al`,
  and the README says the model is inspired by and based upon that work. Field 29 explicitly covers a
  predecessor or the project a work derives from. The README's own link points at
  `https://github.com/scivision/AIDA-tools`, which redirects to the `space-physics` form recorded
  here; the `space-physics` form is canonical, matching the treatment of this software's own
  repository URL in Field 3. AIDA-tools likewise had no HSSI entry of its own at this refresh.

**Considered and rejected: `python-dateutil`.** It is a declared dependency (the model parses time
strings with `dateutil.parser.parse`), but it is named explicitly in the generic-stack exclusion that
applies to Fields 29 and 30 alike. Being a dependency is not a relation; "it parses dates with
python-dateutil" is true of a large fraction of the ecosystem and distinguishes nothing.

### 30. Interoperable Software (OPTIONAL)
**Interoperable Software:**
- https://github.com/pydata/xarray

**numpy, scipy, matplotlib and seaborn are not recorded here. HSSI held all four in this field
before this refresh; they were removed because the field's own rule excludes them by name.** This is
a policy exclusion, not a matter of curator taste. Field 30's guidance names a Tier A list of
packages that are never listed, "no exceptions", on the reasoning that being a dependency is not
interoperability and that a claim equally true of most of the Python ecosystem carries no information
about this software. **numpy, scipy, matplotlib and seaborn are all named in that list by name.** The
same exclusion is extended explicitly to Field 29, so these four are not relocated there either — the
correct destination for all four is neither field. `setup.cfg` does declare all of them (numpy and
scipy under `install_requires`; matplotlib and seaborn under the `plots` extra), which is precisely
the dependency-presence justification the rule rejects.

**xarray is retained, and it clears the Tier B evidence bar on cited, specific grounds.**
Tier B packages, xarray among them, qualify only when a specific exchange is documented in the public
API, docs, examples or tests, the guidance's own qualifying example being a public API that returns
xarray objects as its documented interchange format. That is exactly what this software does, in both
directions:

- **Output.** `reesiono`, the model's top-level entry point, is annotated `) -> xarray.DataArray:`
  and constructs that `DataArray` — with named `time`, `alt_km` and `energy` coordinates — as the
  object it returns. It is the type of the model's top-level result, and the form in which a user
  receives the production rates.
- **Input.** `ionization_profile_from_flux` takes
  `E: np.ndarray, iono: xarray.Dataset, isotropic: bool, datfn: Path, verbose: bool` — an
  `xarray.Dataset` is the documented type of the atmosphere argument, and that Dataset is what
  `msise00.rungtd1d` hands over. xarray is literally the interchange format between the two packages.
  `partition` carries the same contract inward, declared as
  `    iono: xarray.Dataset, k: dict[str, float], cost: dict[str, float]` returning
  `) -> xarray.DataArray:`.
- **Asserted in the test suite.** `reesaurora/tests/test_all.py` contains
  `assert isinstance(Q, xarray.DataArray)`, so the interchange type is not incidental — it is pinned
  by a test.

That is a cited, specific exchange in the public API and in tests, not a claim of internal use.
xarray stays.

**Considered and rejected: adding msise00 or gridaurora here.** Both genuinely exchange data with
this package — msise00's Dataset flows in, gridaurora's writer takes the DataArray out — so a case
could be made. They are recorded in Field 29 instead because both are hard required dependencies
rather than peer tools a user would optionally combine, and Field 29 explicitly covers important
dependencies. Listing them in both fields would duplicate without informing. Recorded here so the
question is not reopened as though it had been overlooked.

### 31. Related Instruments (OPTIONAL)
**Instruments:** None — evidenced empty.

**This is a searched result, not an unexamined blank.** Every tracked non-binary file at the pin was
searched case-insensitively, counting matching *lines*, against a pattern chosen to cover the
concept rather than a handful of facilities that happened to come to mind. It spans named
observatories and radars (`eiscat`, `poker flat`, `pfisr`, `risr`, `sondrestrom`, `millstone`,
`arecibo`, `alis`, `dasi`, `themis`, `svalbard`, `tromso`, `kiruna`), generic instrument and
facility words (`observator`, `instrument`, `radar`, `telescope`, `camera`, `all-sky`/`allsky`,
`photometer`, `riometer`, `incoherent`, `magnetometer`, `imager`, `interferometer`, `spectrograph`,
`spectromete`, `lidar`, `ionosonde`, `sonde`, `station`, `facility`, `sensor`, `detector`, `array`
in its instrument sense), and platform and mission terms (`spacecraft`, `satellite`, `mission`,
`payload`, `probe`, `orbiter`, `sounding rocket`, `ground station`, `dmsp`, `swarm`, `goes`,
`dscovr`, `ace`, `cluster`, `mms`, `rbsp`, `van allen`, `wind`, `nasa`, `esa`, `noaa`).

**The finding: every multi-character facility term returns nothing.** `eiscat`, `poker flat`,
`observator`, `instrument`, `radar`, `telescope`, `photometer`, `magnetometer`, `spacecraft`,
`satellite`, `mission` and the rest of the long tokens match no line in any tracked non-binary file
at the pin. That is what the empty field value rests on, and it turns on no subtlety of anchoring.

**The short tokens need care, and the obvious anchoring is not enough.** Tokens such as `ace`,
`esa`, `array`, `wind` and `sonde` occur inside ordinary words, so unanchored they manufacture hits
that are not facility references: `array` occurs inside `np.array`, `ace` inside `space-physics`,
and `esa` inside words such as `presage` and `resale`. Each of those three was evaluated rather than
assumed — an earlier version of this dossier offered `esa` inside `these` as its third example,
which is simply false, since `these` contains no letter `a` at all, and that example had never been
tested. The natural remedy, a `\b` word boundary, then does not do what it appears to: `.` is a
non-word character, so a word boundary sits immediately before `array` in `np.array`, and
`\barray\b` matches it. Run against this tree, the `\b`-anchored token list above returns **six**
lines, not zero — `ReesSerginekoIvanov.py` lines 43, 82 and 125, and `reesaurora/__init__.py` lines
165, 238 and 339. Each was inspected: every one is an `np.array(` constructor call, and none is a
facility reference. The form that expresses what was actually intended is a look-behind,
`(?<![.\w])array\b`, which returns **zero** across the tree.

**Two traps for anyone re-deriving this.** First, the published token list and the executed command
must be the same list. An earlier version of this dossier reported zero matches for a token list
that named `array` in its prose while the command actually run had omitted that token; the
conclusion was unaffected, but the stated result did not reproduce, which is a defect in its own
right. **That defect then recurred inside this very passage, and the instance is recorded here
because it is the best evidence the passage can carry.** The counts this passage previously gave for
the `xarray` probe below came from a run restricted by `-- '*.py'`, while two of the three commands
were printed without that pathspec — so the printed numbers did not reproduce from the printed
commands, and the published figure of "two" was wrong for the commands as written. Nothing but
re-execution catches this: the sentence is internally plausible, every quotation in it is accurate,
and it passed a full validation before the counts were re-derived at the pin.

Second, name the engine: `git grep -E` silently ignores `\b` and fails toward a clean result with no
error. On this repository, run against the pin with no pathspec, `git grep -lE '\bxarray\b'` reports
**no files**, while `git grep -lP '\bxarray\b'` and plain `git grep -lE 'xarray'` each report
**three**: `reesaurora/__init__.py`, `reesaurora/tests/test_all.py` and `setup.cfg`, the last of which
declares `xarray` under `install_requires`. Restricting those same three commands to `-- '*.py'`
gives no files, two and two — that restriction is where the superseded counts came from. Use system
`grep -E` (via `git show <pin>:<path> | grep -inE`) for `\b`, or `grep -P` / `git grep -P` for the
look-behind.

The software names no instrument anywhere — not in code, not in the README, not in packaging
metadata, not in CI configuration.

That absence is consistent with what the software is. It reads no instrument's data, implements no
instrument-specific format or convention, models no instrument's response, and is not an
instrument-team tool. It is an instrument-agnostic forward model, which by the field's own relevance
rule supports no instrument specifically.

**The one near-miss, ruled out explicitly so it is not re-proposed.** The command line's default
coordinates are `default=(65.0, -148.0)` for `help="geodetic latitude/longitude (deg)"` — a
round-number pair in the Alaskan auroral zone, close to the Poker Flat Research Range, and the
controlled instrument/observatory vocabulary does contain Poker Flat rows. That is not a facility
relation. It is a default example coordinate for a model that will run at any auroral latitude, and
any such coordinate would serve equally. Decided from the searcher's side: a visitor on the Poker
Flat page asking to see software related to that observatory would find a general auroral ionization
model out of place, and someone working with Poker Flat data would not reach for it. The same
reasoning disposes of every other facility whose rows appear in the vocabulary.

**Also noted:** ALIS, the Swedish Auroral Large Imaging System associated with the predecessor
AIDA-tools package, has no row in the instrument/observatory vocabulary at all. It would not be
listed here in any case — a predecessor's instrument association does not transfer to a derived
model, and this software is agnostic — but recording the absence saves a future agent the search.

### 32. Related Observatories (OPTIONAL)
**Observatories:** None — evidenced empty.

The same search and the same reasoning as Field 31, which the field guidance directs be applied
identically at the observatory level. The software is designed to support no mission or observatory:
it works with no mission's data products, implements no mission's conventions, and is not a mission
team's tool. It is a general model of auroral electron precipitation that a user parameterises by
time and geodetic coordinate.

Nothing here is a case of something related but awkward to resolve — no unresolved candidate is
being quietly dropped. The correct value is genuinely empty, and it is recorded as a documented
omission rather than an oversight. The situation the field guidance warns about, where a genuinely
related entity resists resolution and the temptation is to invent a value for it, does not arise:
there is no related entity here to resolve.

### 33. Logo (OPTIONAL)
**Logo URL:** None — evidenced empty.

**A logo was looked for, and the one candidate image was examined and rejected.** The only image file
in the tree at the pin is `reesaurora/tests/demo.png`, a 2140 x 961 RGBA PNG. Rendered, it is a
three-panel scientific figure whose title reads
"Volume Production Rate 2013-01-01 12:00:00+00:00  (65.00,-148.00)" — note the **two** spaces before
the coordinates, which the format string at `ReesSerginekoIvanov.py` line 64 produces:
`    plotA(Q, f"Volume Production Rate {t}  ({glat:.2f},{glon:.2f})", vlim)`. Whitespace inside a
quotation is part of the quotation, and this one is easily damaged: a line wrap falling between the
timestamp and the coordinates silently collapses the pair to one space, which is how an earlier
version of this dossier lost it. Its panels are labelled N2, O and O2, its axes are
"beam energy [eV]" against "altitude [km]", and it carries a "Production Rate [cm^-3 s^-1]"
colourbar. That is model output — an example plot, which the field guidance names explicitly as not
a logo.

The README does embed it, as `![volume production rate](tests/demo.png)`, but as an illustration of
what the model produces rather than as a project mark: it appears in the body beneath the
description, not as a header or banner, and its alt text describes the physical quantity rather than
the project. The PyHC registry entry for this package carries no `logo:` field, and neither the
Zenodo nor the DataCite record supplies one. No other candidate exists in the repository, on a
project site (there is none), or in the documentation (there is none beyond the README).

A documented omission is the correct outcome here. Nothing should be invented, and this particular
image should not be reconsidered — it has been looked at.

---

## PyHC Registry Status

ReesAurora appears in exactly one of the three PyHC registry lists: `_data/projects_unevaluated.yml`
in `heliophysicsPy/heliophysicsPy.github.io`. It is absent from `_data/projects_core.yml` and from
`_data/projects.yml`, the community list. Pinning the specific file matters — a later refresh that
searches only the core or community list would wrongly conclude the package is not registered at all.

Its entry reads:

```yaml
- name: ReesAurora
  code: https://github.com/space-physics/reesaurora
  description: Rees/Sergienko module of excitation rates, relevant to auroral optical emissions
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","specific"]
```

"Unevaluated" is the registry's own classification and means the package has not been assessed
against the PyHC standards; it is not a statement about the software's quality. The registry supplies
Field 7's name, corroborates Field 3's repository URL and Field 6's author, and is the source of one
of Field 16's keywords. It carries no `logo:` field, which is one of the sources checked under
Field 33.

---

## Technical Reference

Details supporting several fields above, gathered here to avoid repeating them.

**Declared dependencies at the pin** (`setup.cfg`). Required: `python-dateutil`, `numpy`, `scipy`,
`xarray`, `msise00`, `gridaurora`. Optional extras: `pytest` (tests); `flake8`, `flake8-bugbear`,
`flake8-builtins`, `flake8-blind-except`, `mypy` (lint); `matplotlib`, `seaborn` (plots). Build
requirements (`pyproject.toml`): `setuptools`, `wheel`, `numpy` — the last carrying the comment
`# numpy is for msise00 prereq`. Fields 29 and 30 explain which of these are relations and which are
generic infrastructure.

**Physical validity limits**, all enforced or warned about in code. Energy: 100-10,000 eV, with a
warning below 50 eV and above 10 keV reading
`"Sergienko & Ivanov 1993 covered E in [100,10000] eV"`. Altitude: the grid begins at 80 km
(command-line default) or 90 km (library default `minalt: float = 90`) and is truncated at the
assumed 700 km electron source, with the message
`"Sergienko & Ivanov 1993 assumed electron source was at altitude 700km."`. Latitude: intended for
auroral latitudes, with `if abs(glat) < 45.0:` triggering
`logging.error("This model was intended for auroral precipitation.")` — a warning rather than a
refusal, so the model will still run outside its intended domain.

**Species and constants.** The model treats `species = ["N2", "O", "O2"]`, with mean energy cost per
ion-electron pair `E_cost_ion = {"N2": 36.8, "O2": 28.2, "O": 26.8}` (Table 1 of Sergienko & Ivanov
1993) and Monte-Carlo correction factors `k = {"N2": 1.0, "O2": 0.7, "O": 0.4}` (their Equation 7 and
Figure 6). Precipitation may be isotropic or field-aligned, selected by a boolean that switches
between two independently tabulated parameter sets.

**Repository shape at the pin.** Nineteen tracked files: `.coveragerc`, `.flake8`, `.gitattributes`,
`.github/workflows/ci.yml`, `.gitignore`, `.mypy.ini`, `LICENSE.txt`, `README.md`,
`ReesSerginekoIvanov.py`, `data/SergienkoIvanov.h5`, `pyproject.toml`, `reesaurora/__init__.py`,
`reesaurora/auxillary_rees.py`, `reesaurora/plots.py`, `reesaurora/tests/demo.png`,
`reesaurora/tests/test.m`, `reesaurora/tests/test_all.py`, `setup.cfg`, `setup.py`. No Fortran
source, no documentation directory, no container definition.
