# HSSI Metadata Extraction Results

**HSSI Software ID:** db2bcb8a-c799-4233-9699-dea23b975972
**Repository:** https://github.com/sunpy/sunkit-instruments
**Source Revision:** ab401ba98f6178c6ebfbe0d89cefd1ba6b4b3aea
**Extraction Date:** 2026-09-09
**Validation Date:** 2026-09-11
**Validation Status:** PASS

---

## Scope note — read this before reading any field

This file records the HSSI metadata for `sunkit-instruments` as of 2026-09-09, reconciled against the
pinned source revision and authoritative external sources.

**The pinned tree and the released artifact are not the same software, and this matters in five
fields.** HSSI describes version `v0.6.2`, released 2025-07-10. The pin is 26 commits past the
`v0.6.2` tag on `main` (`git rev-list --count v0.6.2..ab401ba98f6178c6ebfbe0d89cefd1ba6b4b3aea` = 26;
`git merge-base --is-ancestor v0.6.2 ab401ba98f6178c6ebfbe0d89cefd1ba6b4b3aea` succeeds, so this is a
genuine descendant range and not an orphan lineage). Of those 26 commits, 21 are from automated
package-template bots and 5 are human (Shane Maloney twice, Stuart Mumford three times). One of the
human commits, `4c8ad5f` (2025-10-08, "Updates from package template (#185)"), **deleted the entire
`sunkit_instruments/iris/` subpackage** — `__init__.py`, `iris.py`, `tests/`, and
`docs/code_ref/iris.rst` — and raised the declared minimum Python and dependency versions. Both
changes sit at the pin as *unreleased* towncrier fragments, `changelog/185.breaking.1.rst` and
`changelog/185.breaking.rst`. No release has yet shipped them.

**How to read each kind of claim in this file:**

- Claims about what the software *is and does* — structure, public API, supported instruments,
  file formats, functionality, regions, phenomena, related software, licence text, logo, funding —
  are read at the pin, and every quotation below is byte-exact against that revision.
- Claims about the *released artifact* — the version number, its release date, its version PID, the
  Python floor it declares to installers — describe `v0.6.2` as published, because that is what HSSI
  catalogues and what a user installs.

Where the two disagree, the field says so explicitly. The two live divergences are:

1. **IRIS.** `v0.6.2` shipped an `iris` submodule; the pin has none. No IRIS instrument or
   observatory therefore belongs in Fields 31/32 (see those fields for the surviving test fixture
   that will mislead a future grep).
2. **The Python floor.** `pyproject.toml:11` at the pin reads `requires-python = ">=3.12"`, which is
   unreleased; the published `v0.6.2` declares `>=3.10`. The previous dossier turned this into the
   false statement that Python 3.12 is required "as of version 0.6.2" (Field 13).

Reading a pinned development tree as though it were the released artifact is exactly how that error
was produced. Any future refresh should re-check whether the fragments in `changelog/` have since
been released before repeating a claim about "the current version".

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This is a placeholder, not a value. The catalogue's submitter for this entry is whoever actually
files the record; nothing in the repository identifies one, and no submitter identity should be
inferred from the author list.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.6578605

This is the Zenodo **concept** DOI for the software — the identifier that stands for the software
across all of its releases — and it is the right choice for this field over any single-version DOI,
which belongs in Field 12 instead.

Why it is right, rather than merely stored:

- Its DataCite record gives `resourceTypeGeneral` = `Software`, so the catalogue page's citation
  block renders it as a software citation rather than as an article.
- It currently resolves to the current release, titled `sunpy/sunkit-instruments: v0.6.2`, with
  DataCite `version` `v0.6.2` and `Issued` 2025-07-10 — consistent with Field 12.
- Both the concept record and the version record carry an `IsSupplementTo` relation to a
  `https://github.com/sunpy/sunkit-instruments/tree/v0.6.2` URL. A `/tree/` supplement URL is the
  signature of a GitHub-integration deposit rather than a hand-made upload, which is why the deposit
  metadata (creators, version, dates) can be treated as coming from the project itself.

**Durable caveat for a later refresh:** a Zenodo concept DOI resolves to the most recently *created*
deposit, not to the highest version number. If the project ever publishes a backport release of an
older line, the concept DOI would begin resolving to that older version and the "resolves to the
current release" observation above would stop holding. That is a thing to re-check on each refresh,
not a defect in the value — the concept DOI remains the correct Field 2 value either way.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/sunpy/sunkit-instruments

The canonical repository. PyPI's `project_urls["Source Code"]` for the `sunkit_instruments`
distribution points at this exact URL, which is what ties the published package to this repository
rather than to a fork. The repository is not archived and is not itself a fork.

### 4. Software Functionality (RECOMMENDED)

**Values (eleven):**

- Data Processing and Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: Line Plots
- Mission-related
- Mission-related: Instrument Response
- Mission-related: Instrumentation

The catalogue held six of these before this refresh. The two top-level rows `Mission-related` and
`Data Visualization`, and the three `Data Processing and Analysis` children `Data Access and
Retrieval`, `Time Series Analysis` and `Image Processing`, were added in this refresh; the reason
for each is given below.

**Corrected previous value.** A previous revision of this dossier recorded
`Data Processing and Analysis: Analysis` as though it were stored. It is not, and never was: the
catalogue holds the **bare top-level** `Data Processing and Analysis` row, not its `Analysis` child.
The two are different vocabulary rows and the mistake is easy to repeat, because the bare parent and
the `Parent: Child` form look alike in a rendered list. `Analysis` is not recorded now either; the
reason is with the other rejections below.

**Write every child in `Parent: Child` form.** Thirteen subcategory names in this vocabulary occur
under more than one parent (`Calibration`, `Instrument Response`, `Processing`, `ML/AI`,
`Field-line Tracing`, `2D Slices`, `Mission-Specific`, `Analysis`, `Spectrogram`,
`Packet Decommutation`, `Distribution/Access`, `Infrastructure as Code`,
`Observatory/Instrument Models`). A bare child name is therefore ambiguous and can bind to the wrong
row; `Calibration` alone, for instance, could mean either the `Data Processing and Analysis` child
or the `Mission-related` child. The qualified form is the only safe way to write these down.

**Evidence for the six values the catalogue already held, at the pin:**

- *Data Processing and Analysis* (parent) — the package's whole purpose. `calculate_temperature_em`
  derives temperature and emission measure from GOES/XRS irradiance; `remove_lytaf_events_from_timeseries`
  and `split_series_using_lytaf` filter LYRA time series; `despike_l1b_array` cleans SUVI images.
- *Data Processing and Analysis: Calibration* — `sunkit_instruments/suvi/suvi.py` reads the bundled
  effective-area and gain tables (`np.loadtxt(eff_area_file, skiprows=12)`,
  `np.loadtxt(gain_file, skiprows=7)`) to build SUVI responses; `goes_chianti_tem.py` applies a
  detector-dependent flux rescaling for GOES 8–15.
- *Data Processing and Analysis: File Format Conversion* — `sunkit_instruments/suvi/io.py`
  documents `read_suvi` as reading "a SUVI L1b FITS or netCDF file or a L2 HDR composite FITS file",
  and its docstring states that when the input is an L1b netCDF file "the information from the
  netCDF file is transformed into a FITS header". `files_to_map` converts files to sunpy `Map`
  objects; `imagecube2map` converts a RHESSI image cube to a map sequence.
- *Data Visualization: Line Plots* — `plot_detector_sun_angles` in `sunkit_instruments/fermi/fermi.py`
  is a public, exported function that builds a `plt.figure`, calls `plt.plot` once per detector
  series, labels the axes "angle (degrees)" and the title "Detector pointing angle from Sun", and
  shows it. It is the only plotting function in the package's public API.
- *Mission-related: Instrument Response* — the `response` subpackage is a general framework for
  instrument response functions: `AbstractChannel`, `SourceSpectra` and `get_temperature_response`,
  plus SUVI's `get_response`.
- *Mission-related: Instrumentation* — the package is organised strictly by instrument
  (`fermi`, `goes_xrs`, `lyra`, `response`, `rhessi`, `suvi`) and exists to hold instrument-specific
  tools, as its own README states.

**The two parent rows, and why they are recorded.** Before this refresh `Mission-related` and
`Data Visualization` stood only as children (`Mission-related: Instrument Response`,
`Mission-related: Instrumentation`, `Data Visualization: Line Plots`) while their parent rows were
absent — even though the `Data Processing and Analysis` parent was recorded alongside its children.
The vocabulary is a graph in which a child does not imply its parent, so that asymmetry was real
stored data, not a rendering artefact. Both parents are recorded because selecting a subcategory
also selects its parent: that is what makes the entry findable by a visitor browsing either
top-level category, rather than only by one who happens to open the right child. No evidence argued
against them.

**The three children added in this refresh.** Walking the full vocabulary against the pinned tree,
these three subcategories were evidenced and absent. Each is recorded because a public, exported
function delivers the capability to users:

- `Data Processing and Analysis: Data Access and Retrieval` — `get_goes_event_list`
  instantiates `hek.HEKClient()` and queries the Heliophysics Event Knowledgebase for GOES flare
  events; `download_weekly_pointing_file` fetches Fermi weekly pointing files; `get_lytaf_events`
  downloads the LYRA annotation database from `http://proba2.oma.be/lyra/data/lytaf/` through
  sunpy's cache. All three are exported public functions, so retrieval is a user-facing capability,
  not internal plumbing. This is also what makes Field 17's `Observatory/Mission-specific` true.
- `Data Processing and Analysis: Time Series Analysis` — the LYRA subpackage exists to
  operate on time-ordered data: `remove_lytaf_events_from_timeseries`, `split_series_using_lytaf`
  and `get_lytaf_events` annotate and cut sunpy `TimeSeries` objects by event interval, and
  `calculate_temperature_em` consumes and returns an `XRSTimeSeries`.
- `Data Processing and Analysis: Image Processing` — `despike_l1b_file` and
  `despike_l1b_array` remove spikes from SUVI L1b image arrays, and RHESSI's `backprojection`
  reconstructs an image from count data and returns a `sunpy.map.Map`. Both are exported.

**Considered and rejected, with reasons** (recorded so a later agent does not re-propose them):

- `Data Processing and Analysis: Analysis` — the catch-all for scientific analysis beyond mechanical
  processing, and defensible on its own merits: `calculate_temperature_em` derives physical
  quantities (isothermal temperature and emission measure) from measured irradiance using a
  CHIANTI-based model, and `flux_to_flareclass`/`flareclass_to_flux` convert between physical flux
  and the GOES flare classification. It is not recorded because it is the least distinguishing of
  the four candidates considered: every other value says something specific about what this package
  does, and the catch-all would not. This is also the value the previous dossier wrongly believed
  was stored. **A trap if it is ever revisited:** `Analysis` is one of the duplicated child names,
  existing both under `Data Processing and Analysis` and under `Mission-related`, so written bare it
  would bind arbitrarily to whichever row matched first. That is the general rule for this field —
  always write a subcategory as `Parent: Child`.
- `Data Visualization: 2D Graphics` — the only two-dimensional plots in this repository are in
  `examples/plot_suvi_thematic_map.py`, a gallery example, not in the package's public API. Package
  code plots one thing: detector angle against time, a line plot. An example script is not a
  user-facing capability of the library.
- `Coordinate Transforms: Solar` — `fermi.py` and `rhessi.py` both import `sunpy.coordinates.sun`,
  but they use it to compute a Sun-relative pointing angle and to place a reconstructed image; the
  package exposes no coordinate-system conversion to users. Importing a coordinates module is not
  the same as offering transforms.
- `Models and Simulations: Instrument Response` — the `response` subpackage computes response
  functions from atomic data, which is arguably forward modelling of instrument behaviour. Rejected
  because `Mission-related: Instrument Response` already carries this capability and the duplicate
  would say nothing further; the package models an instrument's response, not a physical system.
- `Data Processing and Analysis: Energy Spectra` — RHESSI's `_build_energy_bands` and
  `uncompress_countrate` handle energy channel bookkeeping, but the package computes no energy
  spectrum as a product. The one place spectra appear, `SourceSpectra`, holds a *source* spectrum
  used as model input to a response calculation, not an analysed measurement.

### 5. Related Region (RECOMMENDED)
**Stored value:** Solar Environment

Every subpackage targets a solar-observing instrument — GOES/XRS soft X-ray irradiance, Fermi/GBM
pointing relative to the Sun, PROBA2/LYRA solar irradiance, RHESSI solar hard X-ray imaging, GOES/SUVI
solar EUV imaging — so `Solar Environment` is well founded and no other stored region is in question.

**The Region vocabulary is flat.** Its 24 rows are all top-level; no row is a parent of another, and
a coarse value never implies a finer one. `Solar Environment` therefore does *not* carry `Corona`,
`Chromosphere` or `Photosphere` with it, and conversely none of those may be added on the grounds
that `Solar Environment` "encompasses" them. Each has to be earned separately.

**Considered and rejected: `Corona`.** A word-anchored search of the package `.py` files, `docs/` and
`README.rst` at the pin finds `corona` in no file, `chromosphere` in none, `photosphere` in none,
`transition region` in none, and `solar wind` in none. `coronal` appears in two files only, and every
one of those occurrences was read individually: they are the `abundance="coronal"` parameter of
`calculate_temperature_em` — a CHIANTI ion-abundance model selector whose alternative is
`"photospheric"` — and the SUVI thematic-map class `coronal_hole`, one of nine labels
(`unlabeled`, `outer_space`, `bright_region`, `filament`, `prominence`, `coronal_hole`, `quiet_sun`,
`limb`, `flare`). Neither usage asserts the corona as an observed region; the first is a choice of
atomic abundance table, the second a pixel class name. The instruments this package supports do
observe coronal emission, but that argument is astronomy general knowledge, not evidence from this
software, and adding a region on it would be indistinguishable from adding it to any solar package.
**Not proposed.**

### 6. Authors (MANDATORY)

**The 25 authors the catalogue already held, in stored order.** The order is real stored data (see
the fossil note below); the numbering here is this dossier's own reading aid, and any correction to
an author should be made by name, never by index. Three further credited creators are added in this
refresh, bringing the author list to 28; they are listed and evidenced after this one.

1. Alex Hamilton — no identifier
2. Will Barnes — https://orcid.org/0000-0001-9642-6089
3. Samuel Bennett — https://orcid.org/0000-0001-6420-4422
4. Pritish Chakraborty — https://orcid.org/0000-0001-8875-5819
5. Michael Charlton — no identifier
6. Nitin Choudhary — https://orcid.org/0000-0001-6915-4583
7. Steven Christe — https://orcid.org/0000-0001-6127-795X
8. Nabil Freij — https://orcid.org/0000-0002-6253-082X
9. Laura Hayes — https://orcid.org/0000-0002-6835-2390
10. Keith Hughitt — https://orcid.org/0000-0003-0787-9559
11. Jack Ireland — https://orcid.org/0000-0002-2019-8881
12. Daniel F. Ryan — https://orcid.org/0000-0001-8661-3825
13. Yash Jain — https://orcid.org/0000-0001-5347-4734
14. Silvan Laube — no identifier
15. Andrew J. Leonard — https://orcid.org/0000-0001-5270-7487
16. Larry Manley — no identifier
17. Carlos Molina — https://orcid.org/0000-0003-0300-4106
18. Stuart J. Mumford — https://orcid.org/0000-0003-4217-4642
19. Asish Panda — no identifier
20. David Pérez-Suárez — https://orcid.org/0000-0003-0784-6909
21. Rishabh Sharma — no identifier
22. Albert Y. Shih — https://orcid.org/0000-0001-6874-2594
23. Brigitta Sipőcz — https://orcid.org/0000-0002-3713-6337
24. David Stansby — https://orcid.org/0000-0002-1365-1908
25. Daniel Williams — https://orcid.org/0000-0003-3772-198X

Nineteen carry ORCIDs; six (Hamilton, Charlton, Laube, Manley, Panda, Sharma) do not. Every one of
those six names matches exactly one person in the catalogue, so they are unambiguous even without an
identifier. **No author is ever dropped from this list** — it is the union of what HSSI holds, what
the project's own Zenodo deposit credits, and what the git history at the pin supports.

**Affiliations are deliberately not restated here.** Each author's affiliations are held on that
author's shared person record and are carried unchanged. Writing an affiliation into this file for an
author who has none stored would cause a new organisation record to be created, and creating
organisation records is not this entry's business.

**Three creators the project credits that the catalogue did not hold, added in this refresh.** The
`sunpy/sunkit-instruments: v0.6.2` DataCite deposit — the project's own release metadata, produced by
the GitHub integration described in Field 2 — credits three contributors who were absent from the
author list. All three appear in the deposit under bare GitHub handles, which is why they were not
matched earlier. All three already exist as people in the catalogue, so recording them adds no new
person:

- **`aringlis` → Andrew Inglis**, https://orcid.org/0000-0003-0656-2437. The handle resolves in this
  repository's own history: `aringlis <a.r.inglis@gmail.com>` authored 77 commits, and the same
  repository separately carries the identity `Andrew Inglis <Inglis@scapa.local>` for 8 more. The
  ORCID belongs to the single catalogue record for Andrew Inglis and is unique to him.
- **`vn-ki` → Vishnunarayan K I.** The handle's commits are authored as
  `Vishnunarayan K I <31964688+vn-ki@users.noreply.github.com>` — a GitHub noreply address, which
  binds the account handle to that display name directly. **The catalogue's existing record spells
  this given name `Vishnunarayan K` with family name `I.`** Use exactly that spelling: it is what
  binds the existing record, and a different spelling would not match. The record carries no
  identifier.
- **`derdon` → Simon Liedtke.** The handle's commits are authored as
  `derdon <liedtke.simon@googlemail.com>`. The catalogue independently resolved the same handle to
  Simon Liedtke from another project, which corroborates the email-based reading rather than merely
  repeating it. The record carries no identifier.

All three are recorded. They are credited authors on the project's own release deposit, and the
alternative — leaving them out because a machine-generated deposit spelled them as handles — would
under-credit three real contributors for a reason that is about tooling rather than about who wrote
the software.

**No affiliation is asserted for any of the three**, for the reason given above: an affiliation that
matched no existing organisation record would create one.

**There is no `.mailmap` in this repository at the pin.** A future agent looking for one here will
find nothing. The identity reconciliations below rest on `sunpy`'s and `ndcube`'s mailmaps and on
commit-address evidence read in this repository — state that plainly rather than implying a local
authority that does not exist.

**Identity notes** (carried forward; each records evidence a later agent would otherwise have to
re-derive, and the project's own creator string is preserved in each so the correction is auditable):

- **Daniel F. Ryan** — an earlier revision of this dossier recorded given name "Dan Ryan" and family
  name "Irish", a naive space-split of the GitHub handle `DanRyanIrish`. `sunpy`'s `.mailmap` maps
  both `Dan Ryan <ryand5@tcd.ie>` and `DanRyanIrish <ryand5@tcd.ie>` to the canonical
  `Daniel F. Ryan`, and `ndcube`'s `.mailmap` maps `DanRyanIrish` the same way. `DanRyanIrish` is
  this project's own creator string.
- **Andrew J. Leonard** — an earlier revision recorded "Drew Leonard" with no identifier. The commit
  address `andy.j.leonard@gmail.com` appears as "Drew Leonard" in both this repository and `sunpy`,
  and ORCID `0000-0001-5270-7487` resolves to Andrew Leonard. "Drew Leonard" is this project's own
  creator string.
- **Alex Hamilton** — an earlier revision recorded a blank given name with family name
  `Alex-Ian-Hamilton`. `sunpy`'s `.mailmap` canonicalises that alias to **Alex Hamilton**, and this
  repository's history shows `Alex`, `Alex Hamilton` and `Alex-Ian-Hamilton` all under
  `Alex_Ian_Hamilton@hotmail.com`. No identifier is asserted: the reconciliation rests on the
  upstream-canonical name form, not on an ORCID.
- **Yash Jain** — the commit address `yashjainjain1704@gmail.com` appears in this repository as
  `yash_jain` and in `sunpy` as both `Yash Jain` and `yash_jain`, so they are one person. Note for
  anyone tempted to merge further: `sunpy` separately credits **Sarthak Jain** and **Shubham Jain**,
  who are different people.
- **Pritish Chakraborty** — the commit address `chakrabortypritish@gmail.com` appears in this
  repository under the handle `VaticanCameos` and in `sunpy` under the full name, so they are one
  person.
- **Carlos Molina** — the commit address `carlosmolina.ord@gmail.com` appears in this repository
  under the handle `cmolinaord` and in `sunpy` under the full name, so they are one person. The
  SUGUS-GNULinux affiliation this project supplied is retained on his record alongside anything other
  sources give him; an affiliation is never dropped in favour of a newer one.

**Stored-order fossil — do not "fix" it.** The stored order is alphabetical by family name with
exactly two exceptions: Alex Hamilton sorts first, and Daniel F. Ryan sits between Ireland and Jain.
Those are precisely the positions the superseded name forms `Alex-Ian-Hamilton` and `Irish` would
occupy. The order was assigned before those two names were corrected and was never rewritten. It is
harmless, it is evidence that the corrections above really happened, and re-sorting it would rewrite
stored ordering data for no gain.

### 7. Software Name (MANDATORY)
**Value:** sunkit-instruments

The hyphenated form is what the project calls itself in its README title, what the repository is
named, and what the catalogue stores.

**The underscore form is real and should not be mistaken for a typo.** `pyproject.toml:9` declares
`name = "sunkit_instruments"`, so the PyPI distribution and the importable Python package are both
`sunkit_instruments`. That is the usual Python convention (a distribution name may not contain a
hyphen in an import statement), and it does not make the underscore the software's name. Anyone
reconciling this entry against PyPI will meet the underscore; the hyphen stays.

### 8. Description (MANDATORY)
**Value:** sunkit-instruments is a SunPy-affiliated package for solar instrument-specific tools. Its purpose is not to be a repository for all tools for all instruments. Instead it is intended to perform three main roles: (1) Hold instrument tools that are so few they do not warrant their own package; (2) Hold tools for instruments with no instrument team or the instrument team does not currently support solar applications; (3) Act as an incubator for instrument-specific tools that can evolve into a separate instrument package, backed by an instrument team. The package currently provides tools for GOES-XRS, Fermi/GBM, PROBA2/LYRA, RHESSI, and GOES/SUVI instruments, including data processing, calibration, instrument response calculations, and visualization capabilities.

**Checked against `README.rst` at the pin: no drift.** The first three sentences and the three
numbered roles reproduce the README's "What is sunkit-instruments?" passage word for word; the only
difference is typographic, the README's numbered list being rendered inline as `(1) … (2) … (3) …`
so the description can be a single prose block.

The closing sentence — the list of instruments and capabilities — is a synthesis, not a README
quotation, and it is worth keeping for two reasons. It is what makes the description searchable by
instrument name, which the README passage alone would not be. And it is **still accurate at the
pin**: it names GOES-XRS, Fermi/GBM, PROBA2/LYRA, RHESSI and GOES/SUVI, which are exactly the
instrument subpackages present after the `iris` removal. Had it mentioned IRIS, the removal
described in the scope note would have made it false. A later refresh should re-check that sentence
against the subpackage list rather than assuming it stays true.

### 9. Concise Description (OPTIONAL)
**Value:** A SunPy-affiliated package for solar instrument-specific tools.

This is byte-identical to the GitHub repository description and to the `description` field of the
project's entry in the PyHC registry's evaluated-projects list — three independent surfaces carrying
the same sentence, which is as strong as a one-line description gets.

**Two variants exist in the repository; neither displaces the stored value.** Record them so a later
refresh recognises them instead of churning the field:

- `pyproject.toml:10` reads `description = "A SunPy affiliated package for solar instrument-specific tools."`
  — the same sentence with **no hyphen** in "SunPy affiliated". `README.rst`'s own subtitle line uses
  the unhyphenated form too, while the README body, GitHub and PyHC all use "SunPy-affiliated". The
  hyphenated form is the majority usage and the grammatical one for a compound modifier.
- `docs/index.rst` opens with a different sentence entirely: "A package for instrument-specific data
  structures and processing in the SunPy ecosystem." This is a genuine alternative rather than a
  variant spelling, but it is weaker for a catalogue: it drops the word "solar", and "data
  structures" overstates a package that mostly returns sunpy's structures rather than defining its
  own.

**Previous dossier value, superseded.** An earlier revision proposed a longer sentence naming the
five instruments. It was a reasonable synthesis but it duplicated Field 8's closing sentence and it
is not what the project says about itself anywhere; the stored one-liner is the project's own words
in three places.

### 10. Publication Date (RECOMMENDED)
**Value:** 2020-04-02

The GitHub repository's creation date. It coincides with the repository's first commit, `74faff5`
("Initial commit", 2020-04-02), so the two independent readings agree.

**Durable caveat: the earliest commit in this repository is not the package's birth.** The history
imported into this repository reaches back to 2011, because this code was split out of the sunpy
core package rather than written from scratch. The repository has **two root commits**: `74faff5`
(2020-04-02, "Initial commit"), which is this package's own beginning, and `72aa329` (2011-09-18),
whose subject is "Created rhessi.py module. Currently contains results of recent python script to
develop back projection imaging." — the imported RHESSI module, which makes concrete what "split out
of sunpy core" means here: the RHESSI code arrived with nine years of sunpy history attached. A
future agent running `git log --reverse` and taking the oldest commit date will get 2011-09-18, a
date that describes sunpy's history rather than this package's. 2020-04-02 is the date this package
began to exist as a package.

Not to be confused with the first *release*: `v0.1.0` was tagged 2020-09-30, roughly six months
later. The form asks for when the software was first published, and the repository's creation is the
better answer for a package whose code predates its own repository.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Zenodo is where the software's DOIs are minted (Fields 2 and 12) and is the publisher named on the
DataCite record. This is a shared publisher record used by many entries; nothing about it is specific
to this software and there is nothing here to change.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.6.2
- **Version Date:** 2025-07-10
- **Version Description:** Updating the maximum supported GOES satellite to GOES 19 for the temperature and emission measure calculation. Updated GOES event list to account for change in the HEK results from sunpy 7.0.
- **Version PID:** https://doi.org/10.5281/zenodo.15852260

`v0.6.2` is the newest release: it is the highest release tag in the repository, the newest GitHub
release, and the newest PyPI upload. The pin is 26 commits past it (scope note), but no release has
been cut from those commits, so `v0.6.2` remains the version a user gets.

**The 2025-07-09 / 2025-07-10 divergence is real, and the stored 2025-07-10 is right.** Record this,
because the discrepancy has an in-repository source and the next refresh will otherwise "correct"
the catalogue back to the wrong date:

- The `v0.6.2` tag points at commit `70d0d37d`, whose **author** date is 2025-07-09 21:08:50 -0700
  and whose **committer** date is 2025-07-10 00:08:50 -0400. Those are the same instant,
  2025-07-10T04:08:50Z — one wall clock reads 07-09 and the other 07-10 purely because of the offset.
- Everything downstream of the tag agrees on 07-10: the tag's own creation date, the GitHub release
  publication, the PyPI upload, and DataCite's `Issued` value.
- `CHANGELOG.rst` line 1, however, reads `0.6.2 (2025-07-09)`. The project dates its own changelog by
  the -0700 author date, which is why an earlier revision of this dossier recorded 2025-07-09.

The changelog heading is the odd one out, not the authority. The release happened on 2025-07-10 UTC.

**The version description is the changelog's own two bug-fix lines, quoted verbatim.** The catalogue
carried no version description for `v0.6.2` before this refresh. The recorded text is exactly what
`CHANGELOG.rst` says at the pin under the `0.6.2` heading, minus the trailing pull-request links:
"Updating the maximum supported GOES satellite to GOES 19 for the temperature and emission measure
calculation." and "Updated GOES event list to account for change in the HEK results from sunpy 7.0."
It is the project's own text and is exactly what the release contained. It reads as two fragments
rather than as a description, which is the price of being quotable back to the project.

Two alternatives were considered and rejected:

- **A synthesised sentence joining the two.** The previous dossier proposed one. It is faithful to
  this release's changelog in substance but it is **not verbatim** — among other small edits it drops
  "the" before "temperature". A description that cannot be matched against the source it claims to
  quote is worse than a slightly clumsy one that can.
- **Leaving the field empty.** Nothing would have been lost in accuracy, but a reader of the
  catalogue page would learn nothing about what the release contained, and the project's own text was
  available.

The GitHub release offers no third source: its `name` is just `v0.6.2` and its `body` is an
auto-generated pull-request list rather than prose.

### 13. Programming Language (RECOMMENDED)
**Value:** Python 3.x

**The criterion, stated once.** The form asks for "The computer programming languages most important
for the software" — the emphasis is this file's reading, not the form's, so it is left out of the
quotation — and says outright "This is not meant to be an exhaustive list." So the
question is not *which languages appear anywhere in this project* but *which languages a user or
maintainer must know to use and work on it*. Every inclusion and exclusion below follows from that
one test, rather than from a construct-by-construct survey.

By that test the answer is a single value. Every line of the package, its tests, its examples and its
documentation build is Python 3.

**And here the question barely arises**, because the tree at the pin contains **no C, no Fortran, no
IDL source (`.pro`) and no Cython file at all** — 139 tracked files, whose extensions are `.py`,
`.txt`, `.rst`, `.yml`, `.fits`, `.db`, `.yaml`, `.nc`, `.gz`, `.toml`, `.sav`, `.ini`, `.sh`, `.md`,
`.json`, `.in`, `.bat` and a handful of dotfiles, plus two files with no extension. There is no
compiled component to attribute to a second language.

**The two `.sav` files are IDL *data*, not IDL source.** They are reference fixtures used by
`sunkit_instruments/goes_xrs/tests/test_goes_xrs.py`, which reads them with
`from scipy.io import readsav` to check the Python implementation against the original IDL routine's
numbers. Reading a file another language wrote is not writing in that language, and `IDL` is
therefore correctly absent from this field. (It is also correctly absent from Field 18 — see there.)

**Correction of a previous dossier claim.** An earlier revision stated "The package requires Python
3.12 or higher as of version 0.6.2." That is false. The released `v0.6.2` declares `>=3.10` to
installers; the `requires-python = ">=3.12"` at `pyproject.toml:11` is an **unreleased** change,
recorded in `changelog/185.breaking.rst` as "Increased minimum version of Python to 3.12." along
with unreleased floors for sunpy, astropy, SciPy, NumPy, Matplotlib, pandas and xarray. The claim was
produced by reading a development tree as though it were the released artifact — the exact hazard the
scope note exists to prevent. It does not change this field's value, which is `Python 3.x` either
way, but it would mislead anyone deciding whether they can install the release.

### 14. Reference Publication (OPTIONAL)
**Value:** Not found — **there is no software paper for this package.**

This is an evidenced negative, not an unsearched gap, and it is written so that it can be checked
rather than merely believed.

The astronomical literature index (ADS/SciX) was searched full-text for both spellings of the
package name and by title. `full:"sunkit-instruments"` and `full:"sunkit_instruments"` each return a
small handful of records, and `title:"sunkit"` returns three. Reading them, the only record *titled*
after this software is a Zenodo software deposit (`sunpy/sunkit-instruments: v0.3.1`) — a DOI for the
code itself, which is Field 2's business, not a describing publication. The remaining full-text hits
are papers citing the package in passing, which is Field 27's territory at most.

Both directions of the search were controlled, so the negative result is a measurement rather than an
absence of effort: a positive control (`full:"sunpy"`) returns a large result set under the same
query syntax, proving the search reaches this literature, and a nonsense control returns zero,
proving a zero is really zero rather than a syntax failure.

The repository corroborates it: there is **no `CITATION.cff`**, and the README and documentation ask
users to cite nothing. Field 2's DOI is how this software asks to be cited.

*If this ever changes, it will change visibly* — a SunPy-affiliated package that publishes a paper
would announce it in the README and add a citation file. Re-check those two places before repeating
the search.

### 15. License (RECOMMENDED)
**Value:** BSD 3-Clause "New" or "Revised" License

The value is corroborated four ways: the licence text tracked in the repository is the three-clause
BSD text (three bulleted conditions, including the "Neither the name of" clause that distinguishes
three-clause from two-clause); GitHub's licence detection reports the SPDX identifier
`BSD-3-Clause`; the DataCite deposit's rights list carries `bsd-3-clause`; and PyPI carries the
licence text itself.

**Do not record a "License URI" as a value of this entry.** A previous revision of this dossier
listed `https://opensource.org/licenses/BSD-3-Clause` as though it were a second storable field.
It is not: the licence is a shared catalogue row, the URL lives on that row and is the same for every
entry using it, and there is no per-software licence URI to set. Citing a repository licence file as
*evidence* for the value is fine; presenting a URL as a value of this entry is not.

**Licence history — and why no released artifact was ever BSD 2-Clause.** This matters because
someone reading the git history will find a two-clause licence and may conclude the project changed
its licence terms on users. It did not:

- `74faff5` (2020-04-02, "Initial commit") added a `LICENSE` file containing the **BSD 2-Clause**
  text, "Copyright (c) 2020, SunPy".
- `ca1e50b` (2020-04-02, the same day) added the package template's `LICENSE.rst`, carrying the
  three-clause text, alongside it.
- `82c384e` (2020-09-28) deleted the two-clause `LICENSE`, leaving `LICENSE.rst`.
- The first release, `v0.1.0`, was tagged **2020-09-30** — two days after the two-clause file was
  removed.

So the two-clause text existed only in an unreleased repository state during the project's first five
months. Every artifact anyone could install has been three-clause BSD.

**Two licence files coexist at the pin, with different copyright lines.** `LICENSE.rst` reads
"Copyright (c) 2020-2025, The SunPy Developers"; `licenses/LICENSE.rst` reads "Copyright (c) 2024,
The SunPy Community". Both carry the same three-clause conditions, so the licence terms are not in
doubt, only the attribution line and the year. `pyproject.toml:13` settles which one is authoritative
for packaging: `license-files = ["licenses/LICENSE.rst"]`, i.e. the "2024, The SunPy Community" file
is the one shipped in the distribution. The duplication is a package-template artefact, not a
licensing problem, and it is upstream's to tidy rather than a metadata question here.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values (13), in the catalogue's own lowercase form:**

calibration, emission measure, fermi, flare detection, goes, instrumentation, instrument response,
lyra, rhessi, solar, suvi, temperature response, wavelength response

Twelve of these were already stored; `emission measure` was added in this refresh, for the reason
given below.

**They really are lowercase.** The catalogue's read-only view title-cases keywords for display, so a
page rendering "Goes", "Lyra", "Rhessi", "Suvi" is showing a display transform, not stored data. Do
not copy a title-cased rendering back into this field as though it were a correction — the stored
strings are the lowercase ones above, and the odd-looking "Goes" is a rendering artefact of the
keyword `goes`.

The set is well chosen: five instrument names covering every subpackage (`fermi`, `goes`, `lyra`,
`rhessi`, `suvi`), three capability terms matching the response framework and the SUVI/GOES
calibration work (`calibration`, `instrument response`, `temperature response`,
`wavelength response`), one functional term (`flare detection`), and the domain term `solar`.

**Considered and rejected: `specific`.** A previous revision of this dossier carried it as a
thirteenth keyword. It came from the PyHC registry, whose keyword list for this project holds three terms —
`solar`, `specific`, `instrumentation` — of which the middle one is a fragment of the phrase
"instrument-specific", split at the hyphen by whatever tooling built the registry list. As a keyword
it is meaningless: nobody searches a catalogue for "specific", and it retrieves nothing coherent.
It is correctly absent from the catalogue and should not be re-proposed from the registry.

**Why `emission measure` was added, and `proba2` was not.** Keywords are the one open vocabulary in
this form, so a new term creates a new keyword; that is normal, but it argues for restraint. Two
candidates survived the "would a searcher be glad to land here" test, and only one was taken:

- `emission measure` — **added.** `calculate_temperature_em` is the package's flagship scientific
  routine, deriving isothermal temperature *and* emission measure from GOES/XRS irradiance;
  `temperature response` was already stored and the paired quantity was not. Someone searching for
  emission-measure tooling would want this package back.
- `proba2` — **considered and rejected.** The stored `lyra` names the instrument but not the
  spacecraft, so a user who knows the mission but not the radiometer would miss the package. The
  reason against is the one that decided it: the same argument would pull in `goes-r` and `gbm`, and
  the keyword list would drift towards an instrument thesaurus that Fields 31 and 32 already cover
  properly, with SPASE identifiers.

**Considered and rejected: `differential emission measure`.** The term exists in the keyword
vocabulary and sits one word away from the `emission measure` added above, which is exactly why it
needs its reason on record: it names a **different physical quantity**, and binding this package to
it would be wrong. `goes_chianti_tem.py` computes an **isothermal** temperature and emission measure
— the word is in `calculate_temperature_em`'s own docstring at lines 21 and 27, and again in the
inner routine's docstring at line 148 — and the package computes no DEM anywhere. The term does
appear in the documentation, which is what makes the rejection worth recording:
`docs/topic_guide/channel_response.rst` line 16 describes the temperature response as a "useful
quantity when performing thermal analysis of imaging data, such as a differential emission measure or
filter ratio analysis", and that file then gives the DEM integral at line 29 and the definition of
DEM(T) at line 35. But what that passage says is that the response subpackage produces an *input* to
a DEM analysis performed elsewhere — not that this package performs one. That is why the term appears
in the docs and is still not this entry's keyword.

Considered and not proposed: `x-ray` (Field 22's `X-ray emission` already carries this, and the
bare term is too broad to distinguish anything), `python` and `solar physics` (true of a large part
of the catalogue, so they distinguish nothing), and per-satellite terms such as `goes-16`.

### 17. Data Sources (OPTIONAL)
**Stored value:** Observatory/Mission-specific

Correct and well evidenced. Every remote fetch in this package is tied to one mission's archive
rather than to a general multi-mission service: `get_goes_event_list` queries the Heliophysics Event
Knowledgebase specifically for GOES flare events (`attrs.hek.OBS.Observatory == "GOES"`),
`download_weekly_pointing_file` fetches Fermi LAT weekly spacecraft files, and `get_lytaf_events`
downloads PROBA2/LYRA annotation databases. Per the form's instruction for this value, the missions
in question are named in Field 32.

**Considered and rejected: `HTTP/HTTPS Directories`.** The value is literally true — the package does
not go through a generic archive client for its two main downloads; it constructs URLs under
plain HTTP-served directories and fetches them directly. The evidence is recorded because it is what
makes the rejection checkable rather than a matter of taste:

- `sunkit_instruments/fermi/fermi.py` sets
  `base_url = "https://heasarc.gsfc.nasa.gov/FTP/fermi/data/lat/weekly/spacecraft/"`, builds a
  filename from the requested date, probes it with `urllib.request.urlopen` and retrieves it with
  `urllib.request.urlretrieve`.
- `sunkit_instruments/lyra/lyra.py` sets
  `LYTAF_REMOTE_PATH = "http://proba2.oma.be/lyra/data/lytaf/"` and joins the annotation database
  name onto it.
- `goes_chianti_tem.py` pulls its CHIANTI response table from a fixed HTTPS URL through sunpy's data
  manager.

It is nevertheless not recorded. The value is close to infrastructural — a great many packages fetch
over HTTP, so it distinguishes little — and `Observatory/Mission-specific` already names the
substantive answer to what this package's data sources are. The point in its favour, that it warns a
user the package needs outbound HTTP to specific hosts rather than a configured archive client, is
served by the three URLs above being on record here.

Considered and rejected: `The Virtual Solar Observatory.` — the package queries HEK, not VSO, and
these are different services despite both reaching sunpy through `sunpy.net`. `CDAWeb`, `HAPI`,
`SSCWeb`, `OMNIWeb`, `AMDA`, `Madrigal`, `das2`, `VirES`, `GFZ`, `WDC`, `TAP`, `S3/Cloud-aware`,
`FTP/FTPS Directories` — no code path reaches any of them. HEK itself has no row in this vocabulary;
`Other` would be the only way to name it, and `Other` tells a searcher nothing, so it is not
proposed.

### 18. Input File Formats (RECOMMENDED)
**Values:** FITS, HDF5, netCDF3/4, ascii

FITS, HDF5 and netCDF3/4 were already stored; `ascii` was added in this refresh, for the reason
given below. The first three each have verified readers in package code at the pin:

- **FITS** — `fits.open` in `sunkit_instruments/fermi/fermi.py` (weekly pointing files) and in
  `sunkit_instruments/suvi/io.py` (SUVI L1b and L2 composites). `read_suvi`'s own docstring: "Read a
  SUVI L1b FITS or netCDF file or a L2 HDR composite FITS file." RHESSI reads FITS too, but through
  sunpy rather than astropy directly: `backprojection` calls `sunpy.io._file_tools.read_file` on a
  calibrated event list, and `parse_observing_summary_hdulist` takes, in its own words, "The HDU list
  from the fits file." A search for `fits.open` alone will miss the RHESSI path.
- **netCDF3/4** — the SUVI reader has a dedicated `_read_netCDF` path, `_variables.py` accepts the
  `.nc` and `.nc.gz` extensions, and the GOES/XRS science-quality files the package is tested
  against are netCDF.
- **HDF5** — `sunkit_instruments/suvi/io.py` opens SUVI L1b files with
  `h5py.File(filename, "r")` to read the `RAD` dataset. (This is also why h5py is *not* in Field 30;
  see there.)

**Excluded: `IDL.sav`, and this is deliberate.** The vocabulary offers the value and the repository
contains two `.sav` files, so the exclusion needs its reason on record. `readsav` and the `.sav`
files appear **only** in `sunkit_instruments/goes_xrs/tests/test_goes_xrs.py`, which loads
`goes_15_test_chianti_tem_idl.sav` and `goes_16_test_chianti_tem_idl.sav` as reference output from
the original IDL routine and compares the Python implementation against them. They are a regression
fixture for developers, not a format users can hand to the package. No public function accepts one.

**Plain text: two cases, and they are not alike.**

- *Bundled package data — excluded.* `SUVI_FM*_*A_eff_area.txt` and `SUVI_FM*_gain.txt` are read
  with `np.loadtxt` from inside `sunkit_instruments/suvi/data/`. They ship with the package and are
  read to build SUVI's instrument response. A user never supplies them and cannot substitute their
  own, so listing a format on their account would falsely tell a searcher this package ingests their
  text tables.
- *A genuine user-supplied text input.* `parse_observing_summary_dbase_file(filename)` is a public,
  exported function whose only argument is a path the caller chooses. It opens that file and parses
  it with `csv.reader(fd, delimiter=" ", skipinitialspace=True)`, skipping three header rows and a
  column-name row. The file is the RHESSI observing-summary database file — a space-delimited
  plain-text listing served from `https://hesperia.gsfc.nasa.gov/hessidata/dbase/`, one copy of
  which ships as the test fixture `sunkit_instruments/data/test/hsi_obssumm_filedb_201104.txt`. That
  is a user-supplied file in a text format, which is precisely what this field is about.

**`ascii` is recorded on the strength of that second case.** A public function reads a
caller-supplied plain-text data file as its normal mode of use, and a user holding RHESSI
observing-summary dbase files would be right to expect this package back. The reservation is worth
keeping on record: it is one function in one subpackage, and `ascii` is a broad label that could
promise more general text ingestion than the package offers. It is recorded anyway because the field
asks what the software reads, and it reads this.

**Excluded: `csv` as an input.** The RHESSI dbase file is space-delimited; `csv.reader` is merely the
standard-library tool used to tokenise it, not a statement about the format, and no public function
accepts a comma-separated user file. `csv` is a live question on the *output* side instead — see
Field 19.

**Considered and not proposed: SQLite.** LYRA's annotation files (`annotation_lyra.db`,
`annotation_manual.db`, `annotation_ppt.db`, `annotation_science.db`) are SQLite databases opened
with `sqlite3.connect`, and `get_lytaf_events` will use local copies when
`force_use_local_lytaf=True`, so this is closer to a genuine user-facing input than the
excluded cases above. It is not proposed because the vocabulary has no SQLite row: the only expressible
value would be `Other`, which conveys nothing to a searcher and cannot be distinguished from any
other unlisted format. Recorded here so the reasoning is not lost — if an SQLite row is ever added
to the vocabulary, this entry qualifies.

### 19. Output File Formats (RECOMMENDED)
**Value:** csv

**The field was empty before this refresh, and that blank was unexamined rather than a settled
negative** — the previous dossier justified it by asserting the package "primarily works with
in-memory data structures … rather than writing output files", which is broadly true but not
exhaustive. The package does write one format.

**The evidence.** `get_lytaf_events` is a public, exported function (it is listed in the `lyra`
module's `__all__`). Its signature is
`get_lytaf_events(start_time, end_time, combine_files=("lyra", "manual", "ppt", "science"), csvfile=None, force_use_local_lytaf=False)`.
When `csvfile` is set, the function opens that path and writes the assembled LYTAF event table
through `csv.writer(openfile, delimiter=";")`, writing a header row of the record-array field names
followed by one row per event. That is a user-requested file written to a user-chosen path in a
named format — the definition of an output format.

**The caveat, which is real and must stay on record.** `csvfile` appears in the signature but is
**not documented in that function's Parameters block**, which lists only `start_time`, `end_time`,
`combine_files` and `force_use_local_lytaf`. So the capability is public but undocumented. A future
agent who reads only the docstring will conclude the package writes nothing and may re-empty this
field; a future agent who reads only the signature may overstate it as a headline feature. It is
neither.

**The only other write in package code is not an output.** `sunkit_instruments/suvi/io.py` unpacks a
`.gz` file into a temporary directory in order to read a FITS header out of it. That is internal
plumbing — the file is a decompression scratch copy, not a product — and it is correctly not listed.

**Why `csv` is recorded rather than the field left empty.** The capability is true, it is reachable
from the public API, and the delimiter is a semicolon, which is exactly the sort of thing a user
needs warning about. An empty field would assert that the package writes nothing, which is wrong.
The case for leaving it empty was real and is kept on record: one undocumented keyword argument on
one function in one subpackage is a thin basis for a catalogue-level claim, and a user reading
"Output formats: csv" may expect a general export capability the package does not have. It loses
because the field asks what the software can write, not what it advertises, and the silence is
upstream's documentation gap rather than a fact about the software.

### 20. Operating System (RECOMMENDED)
**Stored values:** Linux, Mac, Operating System Independent, Windows

Evidenced from the pin rather than inferred from "it is Python":

- `.github/workflows/ci.yml` runs the test suite on all three platforms — the `test` job's matrix is
  `linux: py314`, `windows: py312`, `macos: py312`, `linux: py312-oldestdeps`, `linux: py314-devdeps`,
  with further Linux jobs for the core run, the docs build and the online tests. Windows and macOS
  are first-class CI targets, not aspirations.
- `tox.ini` declares `envlist = py{312,313,314}{,-online}` with no platform conditions, so the same
  environments are intended to run anywhere.
- There are **no compiled extensions**: the build backend is plain `setuptools.build_meta` with only
  `setuptools` and `setuptools_scm` as build requirements, and the tree contains no C, Fortran or
  Cython source (Field 13). The project publishes a pure-Python wheel.

`Operating System Independent` is therefore justified in its own right, and the three named
platforms record where the project actually tests. Keeping both the general claim and the specific
list is right: the general claim states the design, the list states the evidence.

### 21. CPU Architecture (RECOMMENDED)
**Stored value:** CPU Independent

Follows directly from the same evidence. With no compiled extension there is no architecture-specific
object code, and the published wheel is pure Python, so the package runs wherever a supported
CPython runs. No architecture-specific value (`x86-64`, `Apple Silicon arm64`,
`Linux aarch64 or arm64`, `ppc64le`, `GPU`, `HPC or HEC`) is applicable — selecting any of them
would falsely narrow the package.

### 22. Related Phenomena (OPTIONAL)
**Stored values:** Coronal Heating, Solar Flares, X-ray emission

**The Phenomena vocabulary is flat** — its seven rows are all top-level, with no parent/child
relations. No stored value implies another, and no value may be justified on the ground that a
broader one "encompasses" it.

**`Solar Flares` — strongly evidenced.** `get_goes_event_list` exists to retrieve GOES flare events
from HEK; `flux_to_flareclass` and `flareclass_to_flux` convert between X-ray flux and the GOES
flare classification; `flare` is one of the SUVI thematic-map classes; and a case-insensitive
search for `flare` over the package's own non-test source (`sunkit_instruments/`, `*.py`, excluding
`tests/`) matches seven files at the pin — `goes_xrs/goes_chianti_tem.py`, `goes_xrs/goes_xrs.py`,
`lyra/lyra.py`, `rhessi/rhessi.py`, `suvi/_variables.py`, `suvi/io.py` and `suvi/suvi.py`. The scope
is named because it is the load-bearing one: the same search over `docs/` and `README.rst` matches
**no file at all**, so the evidence for this phenomenon is entirely in the code and none of it is in
the prose a reader of the project's front page would see.

**`X-ray emission` — strongly evidenced.** The GOES/XRS subpackage exists to process soft X-ray
irradiance, and RHESSI is a hard X-ray imager. This is the physical quantity most of the package
measures.

**`Coronal Heating` is retained, and the term is not in the source text — that is not the test.** A
word-anchored search of the package `.py` files, `docs/` and `README.rst` at the pin finds **no
textual support for it**. `coronal` occurs in two files only, and every occurrence was read: they are
the `abundance="coronal"` parameter of `calculate_temperature_em` (a CHIANTI ion-abundance table
selector whose alternative is `"photospheric"`) and the SUVI thematic-map class `coronal_hole`.
Neither is about heating. That search is recorded honestly because it is the thinnest evidence base
of the three phenomena here, and a later agent will find the same emptiness.

What decides the field is whether a searcher would be glad to land on this entry from that
phenomenon, not whether the software happens to use the phrase. Isothermal temperature and emission
measure derived from GOES/XRS irradiance, and the instrument response work that supports them, are
part of the standard observational evidence base for coronal energetics: a researcher browsing
`Coronal Heating` and finding a package that computes those quantities has been served well. Removal
was considered on the ground that the same inference would attach the phenomenon to any package
computing a coronal temperature; it is rejected, because the remedy for a phenomenon that is broadly
applicable is not to strip it from an entry where it genuinely applies.

The adjacent value `Solar Corona` was also considered and is **not** recorded: it has no more textual
support than `Coronal Heating` and, unlike it, names a region-like container rather than the process
this package's measurements feed into, so adding it would compound the inference without answering
any question a searcher is asking.

### 23. Development Status (RECOMMENDED)
**Value:** Active

Before this refresh the catalogue held no development status for this entry, so this is a newly
determined value rather than a change to an existing one.

The vocabulary's own definitions decide it. Quoted exactly:

- `Active` — "The project has reached a stable, usable state and is being actively developed."
- `Inactive` — "The project has reached a stable, usable state but is no longer being actively developed; support/maintenance will be provided as time allows."
- `WIP` — "Initial development is in progress, but there has not yet been a stable, usable release suitable for the public."
- `Unsupported` — "The project has reached a stable, usable state but the author(s) have ceased all work on it. A new maintainer may be desired."
- `Moved` — "The project has been moved to a new location, and the version at that location should be considered authoritative."

The first clause is satisfied for all of `Active`, `Inactive` and `Unsupported`: the project has
reached a stable, usable state — thirteen releases on GitHub, twelve on PyPI, the newest being
`v0.6.2` on 2025-07-10, and a stable documented public API. That immediately rules out `WIP`,
`Concept`, `Suspended` and `Abandoned`, all of which require that no stable usable release exists.
`Moved` is ruled out by the repository not being archived, redirected or superseded — the pinned
`main` is the authoritative location.

**Durable note, because the two release lists do not line up.** The totals above — thirteen on
GitHub, twelve on PyPI — differ by one only coincidentally. The lists diverge in **both** directions,
and there is no single missing entry that reconciles them. Two GitHub releases have no PyPI upload:
`v0.1.3`, and `v0.6.1`, which was published 2025-05-01 and carries a `CHANGELOG.rst` heading of its
own. PyPI in turn carries one key that GitHub has no release for, the pre-release `0.6.0a1`. In full: GitHub's
thirteen are `v0.1.0`, `v0.1.1`, `v0.1.2`, `v0.1.3`, `v0.2.0`, `v0.3.0`, `v0.3.1`, `v0.3.2`,
`v0.4.0`, `v0.5.0`, `v0.6.0`, `v0.6.1` and `v0.6.2`; PyPI's twelve release keys are `0.1.0`, `0.1.1`,
`0.1.2`, `0.2.0`, `0.3.0`, `0.3.1`, `0.3.2`, `0.4.0`, `0.5.0`, `0.6.0`, `0.6.0a1` and `0.6.2`.
Thirteen, less the two GitHub-only releases, plus the one PyPI-only key, is twelve — which is the
whole of the arithmetic agreement. This is recorded so that a future agent reconciling GitHub
releases against PyPI uploads recognises the discrepancy instead of re-investigating it or treating
it as a data error, and in particular does not read the near-equal totals as a one-to-one
correspondence with a single gap. Neither the reason for the divergence nor any consequence for the
recorded version is asserted here; `0.6.2` is the newest release on both lists.

So the real question is `Active` versus `Inactive`/`Unsupported`, and it turns on whether
development is still happening. It is:

- Two human commits on 2026-08-20 (Shane Maloney: "Fix online codecov" and "Missed template
  updates"), on top of a further human commit in January 2026 and two in October 2025.
- **Three open pull requests, all feature work by named maintainers, one of them a draft**: "Add
  SWPC events support" and "Attempt to add  GOES flare detection algo" (samaloney, 2026-07-30) — the
  second of those two is the draft, and the double space after "add" in its title is upstream's own
  text, reproduced here so a later agent does not correct it as a transcription slip — and
  "Make channels time snapshots via Channel.at(obstime)" (nabobalis, 2026-07-08), whose title is
  plain text upstream and is quoted without the code formatting an earlier revision of this file
  added inside the quotation marks.

`Inactive`'s defining clause — "no longer being actively developed" — is falsified by open feature
pull requests from maintainers, and `Unsupported`'s "ceased all work on it" more strongly so. The
draft status of one of the three does not weaken that argument: the two pull requests that are ready
for review carry it on their own, and a draft is itself work in progress. The open PRs matter more
than the commit count here: much of the recent commit traffic is automated package-template
synchronisation, and a status judged on commit volume alone could be argued either way. Maintainers
proposing new features cannot.

### 24. Documentation (RECOMMENDED)
**Value:** https://docs.sunpy.org/projects/sunkit-instruments

The project's rendered documentation. This exact string is also what PyPI carries as
`project_urls.Documentation` and what the PyHC registry carries as this project's `docs` value — the
same URL from three independent surfaces.

It resolves, and it resolves to the versioned stable path (`.../en/stable/`) by redirect. The
unversioned form recorded here is the right thing to store: it is what the project publishes, and it
will keep pointing at whatever the current stable documentation is, whereas a versioned URL would
freeze on one release.

### 25. Funder (OPTIONAL)
**Value:** Not found — evidenced, with the method recorded so the negative can be falsified.

A case-insensitive substring search for `funding`, `grant`, `award` and `acknowledg` across
**all** tracked paths at the pin — not just the documentation, and not just the file types where
such statements usually live — matches exactly **one** file, and that file is not a funding
statement. The match is in
`sunkit_instruments/data/test/sci_gxrs-l2-irrad_g15_d20170910_v0-0-0_truncated.nc`, a bundled GOES-15
XRS test fixture, whose NetCDF global attribute `acknowledgment` carries the placeholder value
`TBD`. That is upstream NOAA product metadata shipped as test data, left unfilled by its own
producer; it says nothing about who funded this package, and a `TBD` would not be a funder even if it
did. Beyond it there is no funding statement, no acknowledgements section, no grant number, and no
`CITATION.cff` anywhere in the repository.

The distinction between anchored and unanchored matters here and is recorded so the check is
reproducible: `acknowledg` is a stem, not a word, so a word-boundary-anchored pattern misses
`acknowledgment` and reports a clean zero. The unanchored search above is the one that was run, and
the one a future agent should re-run.

The search was controlled: a positive control term (`sunpy`) run over the same kind of scope matches
many files, so the search itself works and this near-empty result is a measurement rather than a
broken pattern. The fixture match is itself a second control, in that it demonstrates the search
reaching inside binary data files and not only text.

The external metadata agrees. The DataCite deposit carries no funding references, and the PyHC
registry entry records no funder. There is also no software paper (Field 14) whose acknowledgements
could be read — which is usually the best source for this field, and here simply does not exist.

This is consistent with what the software is: a community-maintained affiliated package of the SunPy
project, contributed to by people funded through their own institutions rather than through a grant
made to this package. Absence of a funder here is a fact about the project, not a gap in the
research.

### 26. Award Title (OPTIONAL)
**Value:** Not found.

Same evidence as Field 25, and the same unanchored search: no award, grant or contract number
appears anywhere in the tracked tree, in the DataCite deposit, or in the registry entry. The single
file that search matches is the GOES-15 XRS test fixture described under Field 25, whose upstream
`acknowledgment` attribute reads `TBD`; it names no award. An award title cannot exist without a
funder, and there is no funder to attach one to.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Values — two method papers, both cited by the package's own code.** No related publications were
recorded for this entry before this refresh.

These are not descriptions of this software — that is why they belong here and not in Field 14,
which correctly stays empty. They are the papers whose methods the package **implements**, cited by
the package itself in the docstrings of the functions that implement them. A user who wants to know
what `calculate_temperature_em` actually computes is sent to the first of them by the code.

- **White, S. M., Thomas, R. J., & Schwartz, R. A. 2005**, *Updated Expressions for Determining
  Temperatures and Emission Measures from Goes Soft X-Ray Measurements*, Solar Physics **227**,
  231–248 — https://doi.org/10.1007/s11207-005-2445-z.
  Cited in `sunkit_instruments/goes_xrs/goes_chianti_tem.py`, in the `References` block of
  `calculate_temperature_em`, as "White, S. M., Thomas, R. J., & Schwartz, R. A. 2005, Sol. Phys.,
  227, 231, DOI: 10.1007/s11207-005-2445-z". This is the only DOI string anywhere in the tracked
  source. The bibliographic details above were confirmed against Crossref and match the docstring
  (the paper's own title capitalises "Goes"; that is the published form, not a transcription slip).
- **Meegan, C., et al. 2009**, *The Fermi Gamma-Ray Burst Monitor*, The Astrophysical Journal
  **702**, 791–804 — https://doi.org/10.1088/0004-637X/702/1/791.
  Cited in `sunkit_instruments/fermi/fermi.py`, in the `References` block of the NaI detector-angle
  function, as "Meegan, Charles, et al. "The Fermi gamma-ray burst monitor." The Astrophysical
  Journal 702.1 (2009): 791." The source gives **no DOI**; the DOI above was resolved from Crossref
  by matching title, journal, volume, page and year. This is the paper that defines the detector
  geometry the function hard-codes.

**Why both are recorded.** They are the package's own citations for its two most substantive
scientific routines, and before this refresh a reader of the catalogue page had no way to learn from
it what method the temperature and emission-measure calculation implements. The reservation — that
neither paper is about this software, and that a related-publications list can drift into a general
bibliography — is answered by the selection rule applied here: only papers the package's own code
cites in a `References` block qualify, which is the strongest evidence of relatedness available
short of a software paper, and which is why the seven non-literature `References` blocks listed
below are excluded.

**The other `References` blocks are documentation, not literature.** The package has nine
`References` blocks in total; the two above are the only ones citing a paper. Naming the other seven
here so a later agent does not re-hunt them:

- `goes_xrs/goes_xrs.py` — a Wikipedia section on solar flare classification.
- `lyra/lyra.py`, three separate blocks — all pointing at `http://proba2.oma.be/data/TARDIS`, the
  PROBA2 project's LYTAF documentation.
- `rhessi/rhessi.py` — the SolarSoft RHESSI data-access guide
  (`hessi_data_access.htm#Observing%20Summary%20Data`).
- `rhessi/rhessi.py`, two further blocks — the SolarSoft IDL routines
  `hsi_obs_summ_decompress.pro` and `hsi_linecolors.pro`, cited as the source of the algorithm and
  the colour table the Python code reproduces.

None of these is a publication, and none should be recorded in this field.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found.

What was looked for: a dataset DOI or persistent identifier in the DataCite deposit's related
identifiers (it has none of that kind); a data availability or dataset citation statement in the
repository (there is none, and there is no paper to carry one, per Field 14); and a bundled or
referenced archival dataset with its own identifier.

The data this package touches is mission archive data, reached live over HTTP from NOAA, NASA and
the PROBA2 project — see Field 17 for the specific hosts. Those are data *sources*, already recorded
in Field 17 and characterised by mission in Field 32; they are not identified datasets with DOIs.
The `.fits`, `.nc`, `.db`, `.sav` and `.txt` files inside `sunkit_instruments/data/test/` are small
truncated test fixtures, not published datasets.

### 29. Related Software (OPTIONAL)

**Before this refresh the field held a single item**, `https://doi.org/10.5281/zenodo.591887` —
SunPy's Zenodo concept DOI — and Field 30 held the same one. The SunPy relation is kept; what changes
is the identifier used to express it, and four further packages are recorded alongside it.

**That DOI item is a shared catalogue row used by other entries. It must never be edited.** Changing
what this entry records means attaching a *different* item, never modifying the existing one — a
rename would silently rewrite what every other entry pointing at that row says.

**Convention for naming another catalogue entry (verified 2026-09-01): use that entry's exact stored
code repository URL.** A related item is rendered on the page with its raw URL as the link text, so a
visitor to this entry sees the literal string. `https://doi.org/10.5281/zenodo.591887` is opaque —
nothing in it says "SunPy" — while `https://github.com/sunpy/sunpy` is legible and is also the key
under which the catalogue holds SunPy's own record, so the two entries join up. SunPy is a catalogue
entry whose stored code repository URL is `https://github.com/sunpy/sunpy`.

*The reverse condition, recorded so the decision can be revisited on its merits:* if the site ever
renders resolved titles instead of raw URLs, this argument inverts — a DOI is more persistent than a
repository URL, and the DOI form would then be preferable. The convention rests on the rendering
behaviour, not on a general preference for URLs over DOIs.

**Values (five), with the evidence for each:**

1. **sunpy** — `https://github.com/sunpy/sunpy`. The package's defining dependency, declared at
   `pyproject.toml:18` as `sunpy[map,net,timeseries,visualization]>=7.0.0`, and a domain-specific
   one rather than generic infrastructure: it supplies the `TimeSeries` and `Map` types that this
   package's public functions consume and return. This package is a SunPy-affiliated package and
   exists inside that project. (It belongs in Field 30 as well, on separate grounds — see there.)
2. **aiapy** — `https://github.com/LM-SAL/aiapy`. Named by the package's own documentation as an
   instrument-specific alternative (below), cited again in `README.rst`, and wired into
   `docs/conf.py:124` as an intersphinx target — the project links its documentation to aiapy's.
3. **eispac** — `https://github.com/USNavalResearchLaboratory/eispac`. Named in the same
   documentation passage. The repository URL was confirmed from PyPI's `project_urls.Homepage` for
   the `eispac` distribution.
4. **xrtpy** — `https://github.com/HinodeXRT/xrtpy`. Named in the same documentation passage.
5. **irispy** — `https://github.com/LM-SAL/irispy`. The successor for functionality this package
   removed: `changelog/185.breaking.1.rst` reads, in full, "Removed ``iris`` submodule, please use
   `irispy <https://irispy.readthedocs.io/en/latest/>`__." A predecessor/successor relation is
   squarely within this field, and it is the single most useful thing to tell a user who arrives
   looking for the IRIS support that used to be here.

**Why entries 2–5 are exactly this field's textbook case.** `docs/index.rst` at the pin says:

> Note that the code in this package is **not** maintained by or necessarily contributed to by instrument teams.
> Some instruments have individual packages for analysis in Python, including:
>
> - `aiapy <https://aiapy.readthedocs.io/>`__
> - `eispac <https://eispac.readthedocs.io/>`__
> - `xrtpy <https://xrtpy.readthedocs.io/>`__

That is the package telling its own users where else to go for instrument-specific analysis — software
that performs similar tasks without linking together, which is this field's definition. It is
authoritative in a way that an outside judgement of similarity never is.

**aiapy is a Field 29 relation, not a Field 30 one, and the distinction matters.** `README.rst`
cites aiapy separately: "We point to the recent development of `aiapy <https://gitlab.com/LMSAL_HUB/aia_hub/aiapy>`__ as a great example of this type of collaboration."
The "type of collaboration" in question is an instrument team building and maintaining its **own**
package instead of contributing tools here. That is a statement about an *alternative*, not about an
exchange of data between the two packages — there is none. The previous dossier placed aiapy in
Field 30 on the strength of this sentence; that reading is wrong, and it is recorded here so the
same sentence is not read the same way again. (Note also that the README's aiapy link is the old
GitLab URL, while the documentation links to the ReadTheDocs site; neither is the repository URL used
above, which is aiapy's stored catalogue location.)

**Removed, with reason: numpy, scipy, matplotlib, pandas.** The previous dossier listed all four
here. They are named in the form's Tier A exclusion, which admits "no exceptions": being a dependency
is not a relation. The form makes the point in its own words — "It directly depends on numpy" is true
of nearly every package in HSSI, so it distinguishes nothing — and its worked contrast lists
"depends on numpy" among the rejected justifications. **This is the rule applied, not a curator's
preference**, and it should not be re-proposed. h5py and xarray were also listed there; they are
Tier B, and they fail on evidence rather than on rule (see Field 30).

**Considered and rejected: ndcube.** The previous dossier listed it in Field 30. A search of the
entire tracked tree at the pin finds **no occurrence of "ndcube" in any file** — not in the
dependencies, not in the documentation, not in an intersphinx mapping. Whatever the association once
was, this package does not reference it. Recorded so it is not re-added from ecosystem knowledge.

**Why this list, and why the SunPy DOI gives way to SunPy's repository URL.** Every addition is
named by the project's own README, documentation or changelog, and each answers a question a visitor
to this page would actually ask ("what should I use for AIA / EIS / XRT / IRIS instead?"). Applying
the searcher's test in the other direction: a visitor on aiapy's, eispac's, xrtpy's or irispy's page
would be reasonably glad to find sunkit-instruments, since it is where the neighbouring instruments
are handled and, for irispy, where its users came from. The SunPy relation itself is unchanged in
substance; only its identifier changes, for the rendering reason given above.

**One-directional, currently.** A sweep of the catalogue's entries for anything pointing back at this
software — under its repository URL, both spellings of its name, and each of its DOIs — found
nothing. The sweep was controlled in both directions, so this is a measurement: any relation recorded
here points outward only, and a future agent should not expect a reciprocal link to exist or treat
its absence as evidence against the relation.

### 30. Interoperable Software (OPTIONAL)

**Before this refresh the field held the same single item as Field 29**,
`https://doi.org/10.5281/zenodo.591887`. The same shared-row caution applies: attach a different
item, never edit that one.

**Values (two):**

1. **sunpy** — `https://github.com/sunpy/sunpy`. The strongest relation in either field, and it
   belongs in both under their own definitions. Argued from the pin rather than from the
   "SunPy-affiliated" label, which by itself would be exactly the ecosystem-membership claim the form
   rejects: `pyproject.toml:18` declares `sunpy[map,net,timeseries,visualization]>=7.0.0`, and the
   exchange is in the public API in both directions. `calculate_temperature_em` requires a
   `sunpy.timeseries` `XRSTimeSeries` as input and raises `TypeError` if given anything else, and
   returns a `TimeSeries`; `remove_lytaf_events_from_timeseries` takes and returns a sunpy
   `TimeSeries`; `files_to_map`, `imagecube2map` and `backprojection` return `sunpy.map.Map` objects
   and map sequences. This package's data model *is* sunpy's — a shared data model, which is the
   form's own worked example of a qualifying interoperation.
2. **astropy** — `https://github.com/astropy/astropy`. **Tier B, and it qualifies on evidence.**
   `sunkit_instruments/response/thermal.py` declares its public returns as
   `~astropy.units.Quantity` in the `Returns` block of `get_temperature_response`; the
   `SourceSpectra` constructor is guarded with `@u.quantity_input` so unit-bearing input is
   *enforced*, not merely accepted; and every public property (`temperature`, `wavelength`,
   `density`, `data`, `temperature_response`) converts its stored values to `u.Quantity` on the way
   out with a declared return unit. Units are the declared interchange currency of that subpackage's
   public API, which is the documented-exchange test rather than dependency presence.

**Tier B rejections — these are evidence findings, not policy removals, and the difference matters.**
Unlike the Tier A names removed from Field 29, these were each tested against the public API and
failed:

- **xarray — fails.** `SourceSpectra` holds `self._da = xarray.DataArray(...)` as **internal
  state** and converts *out* of it on every public property (each returns a `u.Quantity`, per the
  astropy evidence above). Only `__repr__`, `__str__` and `_repr_html_` delegate to the DataArray,
  and those are display strings, not data exchange. No public function accepts or returns an xarray
  object. This is the form's own disqualifying case: "uses xarray internally" does not qualify.
- **h5py — fails.** Used once, in `sunkit_instruments/suvi/io.py`, to open SUVI L1b files and read
  the `RAD` dataset. That is the package *reading a file format*, which is recorded in Field 18 where
  it belongs. Reading HDF5 is not exchanging data with h5py as a peer tool.

Should either package's role change — a public function that accepts or returns an `xarray.Dataset`,
for instance — the verdict would change with it. Re-test against the public API rather than
re-reading this note as permanent.

**Not proposed: aiapy, eispac, xrtpy, irispy.** All four are Field 29 relations (similar-task
alternatives and a successor). None of them exchanges data with this package: there is no adapter,
no shared data structure beyond what both inherit from sunpy, and no code path in either direction.
Being neighbours in an ecosystem is not interoperation.

**Not proposed: any PyHC-membership claim.** The form names "a PyHC member, so it interoperates with
PyHC packages" as never sufficient on its own, and that is precisely what a blanket ecosystem listing
here would amount to.

**Why this list.** As in Field 29, SunPy's relation is expressed by its repository URL rather than
by its Zenodo concept DOI, for the rendering reason argued there; astropy is added on the cited
public-API evidence above rather than on dependency presence, which is what distinguishes it from
the Tier B rejections recorded above.

### 31. Related Instruments (OPTIONAL)

**Values — fourteen rows, every one carrying a SPASE identifier:**

| Instrument (stored name) | SPASE identifier |
|---|---|
| Fermi Gamma-ray Burst Monitor | https://spase-metadata.org/SMWG/Instrument/FERMI/GBM |
| Solar X-ray Monitor on GOES 5 | https://spase-metadata.org/SMWG/Instrument/GOES/5/XRS |
| Solar X-ray Monitor on GOES 6 | https://spase-metadata.org/SMWG/Instrument/GOES/6/SXM |
| Solar X-ray Monitor on GOES 7 | https://spase-metadata.org/SMWG/Instrument/GOES/7/SXM |
| Solar X-ray Monitor on GOES  8 | https://spase-metadata.org/SMWG/Instrument/GOES/8/SXM |
| Solar X-ray Sensor on GOES | https://spase-metadata.org/SMWG/Instrument/GOES/13/XRS |
| Solar X-ray Sensor on GOES | https://spase-metadata.org/SMWG/Instrument/GOES/14/XRS |
| Solar X-ray Sensor on GOES | https://spase-metadata.org/SMWG/Instrument/GOES/15/XRS |
| Solar Ultraviolet Imager | https://spase-metadata.org/NOAA/Instrument/GOES/16/SUVI |
| Solar Ultraviolet Imager | https://spase-metadata.org/NOAA/Instrument/GOES/17/SUVI |
| Solar Ultraviolet Imager | https://spase-metadata.org/NOAA/Instrument/GOES/18/SUVI |
| Solar Ultraviolet Imager | https://spase-metadata.org/NOAA/Instrument/GOES/19/SUVI |
| Sun Watcher using APS detectors and image Processing | https://spase-metadata.org/SMWG/Instrument/PROBA2/LYRA |
| High-Energy Solar Spectroscopic Imager | https://spase-metadata.org/SMWG/Instrument/RHESSI/HESSI |

Ten of these rows were already stored; the three GOES `SXM` rows and the RHESSI row were added in
this refresh, each for the reason given below.

**Several stored names repeat, and the identifier is the only reliable key.** "Solar X-ray Sensor on
GOES" names three different rows above, and "Solar Ultraviolet Imager" four; the three added `SXM`
rows likewise differ from each other only by satellite number inside the name. The row for GOES 8
carries a **double space** in its stored name — `Solar X-ray Monitor on GOES  8` — which is the row's
own text, reproduced here exactly; it is not a transcription slip and must not be "fixed". Match on
identifier, never on name, and never record a name without its identifier.

**SUVI is complete.** Searching the whole instrument vocabulary across every authority prefix, the
identifier path segment `SUVI` occurs for GOES 16, 17, 18 and 19, and every one of those rows is
recorded above. The search was run on the name side as well: "Ultraviolet Imager" surfaces no fifth
GOES row, so there is no alternative spelling hiding further rows. Every GOES SUVI row the vocabulary
holds is recorded here.

**GOES solar X-ray instruments are spelled two ways, and this is the trap to carry forward.** SPASE
names the same Solar X-ray Monitor instrument `XRS` on GOES 5, 13, 14 and 15 but `SXM` on GOES 6, 7
and 8. A sweep keyed on the path segment `XRS` alone is structurally blind to the `SXM` rows, and an
earlier revision of this dossier made exactly that error: it concluded from an `XRS`-only search that
the vocabulary held no solar X-ray row for any GOES satellite between 5 and 13, and that the apparent
gap was upstream's coverage. It is not. **A future agent looking for GOES solar X-ray rows must
search both spellings**, and preferably the name side ("Solar X-ray") as well.

The corrected coverage, from a full inventory of the vocabulary's GOES instrument rows: solar X-ray
instrument rows exist for GOES **5** (`XRS`), **6, 7, 8** (`SXM`) and **13, 14, 15** (`XRS`). There
are none for GOES 1–4 and none for GOES 9–12 — that, and not a single-spelling search artefact, is
why the recorded list jumps from 8 to 13.

*A false friend while doing that search:* `https://spase-metadata.org/SMWG/Instrument/GOES/12/SXI` is
the Solar X-Ray **Imager**, a different instrument that images the corona rather than measuring
disk-integrated soft X-ray irradiance. It is not one of the rows above and does not fill the 9–12
gap.

**The GOES support range, stated so it is not re-derived wrongly.** `goes_chianti_tem.py` sets
`MAX_SUPPORTED_SATELLITE = 19` and gates on
`if (satellite_number < 1) or (satellite_number > MAX_SUPPORTED_SATELLITE)`, raising otherwise. So
**GOES 1 through 19 inclusive are supported.** Two nearby conditions look like support limits and are
not: `if remove_scaling and satellite_number >= 8 and satellite_number < 16` is a flux-rescaling
condition, and a `satellite_number <= 15` branch selects a detector table. A third special-cases
GOES 6 alone. Reading any of those as the supported range understates it. The
`Solar X-ray Monitor on GOES 5` row is therefore well founded rather than an oddity: GOES 5 is inside
the supported range, and the vocabulary has an instrument row for it.

**The RHESSI instrument row, added in this refresh.**
`https://spase-metadata.org/SMWG/Instrument/RHESSI/HESSI`, stored name "High-Energy Solar
Spectroscopic Imager", was absent although the RHESSI *observatory* row was stored and
`sunkit_instruments/rhessi/` exists at the pin with a substantial public API:
`parse_observing_summary_dbase_file` and `parse_observing_summary_hdulist` read RHESSI
observing-summary products, `uncompress_countrate` reimplements the SolarSoft decompression of
RHESSI count rates, `backprojection` reconstructs an image from a calibrated event list, and
`imagecube2map` converts a RHESSI image cube to a map sequence. Applying the searcher's test: a user
on the RHESSI instrument page clicking through to related software would plainly be glad to find a
package that parses RHESSI observing summaries. The one instrument row is sufficient;
`https://spase-metadata.org/SMWG/Instrument/RHESSI/Ephemeris` is a separate ephemeris product this
package does not read, and is **not** recorded.

**The three GOES `SXM` rows, added in this refresh.**
`https://spase-metadata.org/SMWG/Instrument/GOES/6/SXM`, `.../GOES/7/SXM` and `.../GOES/8/SXM` were
missed until now for the spelling reason set out above, not because the case for them is weaker than
the case for the `XRS` rows already recorded. Each rests on something more specific than membership of
a numeric range, and every piece of evidence below is tracked at the pin in
`sunkit_instruments/goes_xrs/goes_chianti_tem.py`.

**GOES 7 is the calibration reference the package's older-FITS pathway is defined against.** The
public docstring of `calculate_temperature_em` says so itself, at line 65:

> and with the older FITS files provided by the SDAC, for which the data are scaled to be consistent with GOES-7.

That is not an incidental mention. GOES-7 is the satellite whose flux scale the whole SDAC-era FITS
input path is normalised to, named in the documentation a user of the function reads. It is also the
only mention of GOES 7 anywhere in the package's non-test code — a word-boundary search for
`GOES-?7|GOES 7` over `sunkit_instruments/` at the pin, and a case-insensitive unanchored re-run of
the same search, each return this line and nothing else. Tracked, quotable and re-checkable, it is
the strongest single piece of evidence for the GOES 7 row.

**GOES 6 has a correction branch written for it alone** — line 203,
`if obsdate <= Time("1983-06-28") and satellite_number == 6:`, which rescales the long channel by
`4.43 / 5.32` (line 204) for early GOES 6 data. No other satellite has such a fix, and the comment
above it records that the factor is undocumented outside the original IDL code.

**GOES 8, and every other supported satellite, is indexed into the response table on its own number.**
The support gate at line 96 — `if (satellite_number < 1) or (satellite_number > MAX_SUPPORTED_SATELLITE):`
with `MAX_SUPPORTED_SATELLITE = 19` at line 16 — admits GOES 1–19 inclusive. Lines 227–228 then derive
a per-satellite response-table index, `if satellite_number <= 15:` / `sat = satellite_number - 1`, and
lines 234–245 read `response_table["ALOG10EM"][sat]`, `response_table["TEMP_MK"][sat]` and
`rcor[sat]`/`rpho[sat]` through it. Temperature and emission measure for GOES 6, 7 and 8 are therefore
computed from the response-table row selected for that satellite specifically, not from a shared one.

**Where that evidence stops, stated so it is not overclaimed.** The response table itself is **not**
in this repository. It is fetched at runtime by the data manager: line 234 calls
`manager.get("goes_chianti_response_table")`, registered at lines 137–143 against
`https://sohoftp.nascom.nasa.gov/solarsoft/gen/idl/synoptic/goes/goes_chianti_response_latest.fits`.
The only tracked artefacts of that kind at the pin are the two IDL regression fixtures
`sunkit_instruments/data/test/goes_15_test_chianti_tem_idl.sav` and
`sunkit_instruments/data/test/goes_16_test_chianti_tem_idl.sav`. So what the repository demonstrates
is the per-satellite **indexing scheme**; whether the rows it selects differ in content — a distinct
emission-measure scaling, temperature grid or modelled flux ratio per satellite — cannot be checked
from the pin at all. An earlier revision of this dossier asserted those distinct contents as fact; a
future agent should not restate them without the response file in hand, and does not need to, because
the GOES 7 docstring and the GOES 6 branch carry the rows on their own.

**Be exact about which satellite has code of its own, because the looser claim is both wrong and
weaker.** Only GOES 6 does. `satellite_number == 6` at line 203 is the only equality test on a
satellite number in the file and, verified over the package's non-test code, the only one anywhere in
it — so nothing singles out GOES 7 or GOES 8, although both are admitted by the line-96 gate and by
the `satellite_number <= 15` range at line 227. The nearby
`if remove_scaling and satellite_number >= 8 and satellite_number < 16:` at line 210 is likewise a
range condition covering 8–15 rather than a GOES-8 special case.

From the searcher's side: a user on the GOES 6, 7 or 8 solar X-ray instrument page, asking what
software works with that instrument's measurements, would be glad to find a package that computes
temperature and emission measure from the response-table row selected for that satellite — for
GOES 7, the satellite the package's SDAC-era flux scale is defined to be consistent with, and for
GOES 6, one that carries a correction written specifically for it.

**Considered and rejected: the Fermi Large Area Telescope**
(`https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/FERMI/LAT`). Tempting, because
`download_weekly_pointing_file` fetches from
`https://heasarc.gsfc.nasa.gov/FTP/fermi/data/lat/weekly/spacecraft/` and the path contains "lat".
But the file retrieved is the *spacecraft* weekly pointing file, which happens to be archived under
the LAT tree, and the package uses it to compute **GBM** detector angles. No LAT science data is
read. The GBM row alone is right.

**Considered and rejected: IRIS.** The vocabulary has both an instrument row
(`https://spase-metadata.org/SMWG/Instrument/IRIS/IRIS`) and an observatory row
(`https://spase-metadata.org/SMWG/Observatory/IRIS`), and version `v0.6.2` — the version the
catalogue describes — did ship an `iris` submodule. Neither row is proposed, because the submodule
was **removed** at commit `4c8ad5f` and the pin has no IRIS support at all; the changelog fragment
directs IRIS users to `irispy` instead, which is why irispy is in Field 29.

*Trap for a future agent:* one IRIS file survives at the pin —
`sunkit_instruments/data/test/iris_l2_20130801_074720_4040000014_SJI_1400_t000.fits`, a leftover test
fixture. Finding it with a grep for "iris" does **not** mean IRIS is supported; there is no code that
reads it.

**Upstream row defect, recorded but not actionable here.** The stored LYRA row
`https://spase-metadata.org/SMWG/Instrument/PROBA2/LYRA` carries the name
"Sun Watcher using APS detectors and image Processing" — which is the expansion of **SWAP**, a
different PROBA2 instrument that has its own row,
`https://spase-metadata.org/SMWG/Instrument/PROBA2/SWAP` ("Proba 2 Sun Watcher using APS detectors
and Image Processing"). The identifier is correct and is what binds; only the display name is wrong.
This is an upstream vocabulary defect shared with every other entry using that row — **not** a value
question for this entry, and **not** something to propose changing from here. Recorded so it is
recognised as a known defect rather than re-investigated as drift, and so that no one "corrects" it
by swapping in the SWAP row, which would associate this package with an instrument it does not
support.

### 32. Related Observatories (OPTIONAL)

**Values — fifteen rows, every one carrying a SPASE identifier.** Five were already stored:

| Observatory (stored name) | SPASE identifier |
|---|---|
| Fermi Gamma-ray Space Telescope | https://spase-metadata.org/SMWG/Observatory/FERMI |
| Geostationary Operational Environmental Satellites | https://spase-metadata.org/SMWG/Observatory/GOES |
| Geostationary Operational Environmental Satellite 16 | https://spase-metadata.org/SMWG/Observatory/GOES/16 |
| PROBA 2 | https://spase-metadata.org/SMWG/Observatory/PROBA2 |
| Reuven Ramaty High Energy Solar Spectroscope Imager | https://spase-metadata.org/SMWG/Observatory/RHESSI |

Ten per-satellite GOES rows were added in this refresh, one for each satellite whose instrument
Field 31 records (GOES 16's row was already stored):

| Satellite | SPASE identifier |
|---|---|
| GOES 5 | https://spase-metadata.org/SMWG/Observatory/GOES/5 |
| GOES 6 | https://spase-metadata.org/SMWG/Observatory/GOES/6 |
| GOES 7 | https://spase-metadata.org/SMWG/Observatory/GOES/7 |
| GOES 8 | https://spase-metadata.org/SMWG/Observatory/GOES/8 |
| GOES 13 | https://spase-metadata.org/SMWG/Observatory/GOES/13 |
| GOES 14 | https://spase-metadata.org/SMWG/Observatory/GOES/14 |
| GOES 15 | https://spase-metadata.org/SMWG/Observatory/GOES/15 |
| GOES 17 | https://spase-metadata.org/SMWG/Observatory/GOES/17 |
| GOES 18 | https://spase-metadata.org/NOAA/Observatory/GOES/18 |
| GOES 19 | https://spase-metadata.org/NOAA/Observatory/GOES/19 |

The identifiers are what bind these rows; their names are deliberately not restated in the second
table, because names in this vocabulary repeat, diverge from upstream on four of these rows, and are
in one case outright ambiguous (see the two wrinkles below). The GOES 6, 7 and 8 rows are here
because Field 31's `SXM` instrument rows were added in the same refresh; before that the
per-satellite set would have been seven.

**Before this refresh the observatory side was thin, and asymmetrically so.** Instruments were
recorded for eight GOES satellites while only the fleet-level
`https://spase-metadata.org/SMWG/Observatory/GOES` row and
`https://spase-metadata.org/SMWG/Observatory/GOES/16` stood on the observatory side.

*The reason for the additions, decided from the searcher's side, and it is the only reason offered:*
a user on the GOES 17 page asking what software relates to it would be glad to find a package that
reads GOES 17 SUVI files; the same holds for each satellite whose instrument this package supports.
The fleet-level row does not deliver that, because a visitor to a per-satellite page does not see
software attached to the fleet row. *Explicitly **not** an argument:* that it makes Fields 31 and 32
look consistent. Internal tidiness is invisible to users and is not a reason to add a value.

*Wrinkle a future agent will hit — a deliberate name divergence on four of these rows.* The upstream
SPASE vocabulary names the GOES 5–12 observatory records by COSPAR launch designator rather than by a
readable name: upstream, GOES 5 is `1981-049A`, GOES 6 `1983-041A`, GOES 7 `1987-022A` and GOES 8
`1994-022A`. That is upstream's convention, not an error in it. But a bare launch designator tells a
visitor to this entry nothing about which spacecraft is meant, and these four rows carry no
abbreviation to sit beside it, so nothing on the page supplies the missing context. The names held
for GOES 5, 6, 7 and 8 therefore read in the readable singular form that GOES 13–19 already use
("Geostationary Operational Environmental Satellite 5"), and they differ from their upstream pages on
purpose. **A future agent comparing a stored name against its SPASE page will find a mismatch on
exactly these four rows, and must not "correct" it back to the designator.** The rows for GOES 9–12
are not part of this entry's list and keep their designator names upstream and here alike.

None of that changes what binds a row, which is the point of this paragraph: match on the SPASE
identifier, never on the name.

*A second trap, worth knowing before anyone matches these by name:* the row
`https://spase-metadata.org/SMWG/Observatory/GOES/4` is named
"Geostationary Operational Environmental Satellites" — **identical** to the fleet-level
`.../Observatory/GOES` row's name. Any match made on name alone can silently bind GOES 4 instead of
the fleet row, or vice versa. It is the sharpest illustration of the rule: match on identifier.

**Considered and rejected: the wider GOES 1–12 set.** `calculate_temperature_em` admits satellite
numbers 1 through 19, so a case exists for the observatory rows of the whole range rather than only
those satellites whose instruments are recorded. Two things decide against it. This package does not
itself read those satellites' files: it computes temperature and emission measure from a time series
another package has already loaded, so numeric admissibility is not the same as support for a
mission's data. And adding a dozen rows on the strength of a numeric range would dilute the field —
a visitor arriving from GOES 3 would find a package with nothing particular to offer them, which is
the opposite of what these associations are for. Recorded so the option is visibly considered rather
than overlooked, and so it is not re-proposed from the 1–19 gate alone.

**Kept: the fleet-level `.../Observatory/GOES` row.** It is the right value for a package that
supports the GOES series broadly, and it stays alongside the per-satellite rows rather than being
displaced by them.

**Considered and rejected: the CNES duplicate Fermi observatory row**
(`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/Fermi`, "FERMI gamma-ray space telescope").
It denotes the same observatory as the stored SMWG row. Recording both would double-count one
mission; the SMWG row is the canonical one and is already stored.

**Considered and rejected: IRIS** — same reasoning as Field 31; the submodule is gone at the pin.

### 33. Logo (OPTIONAL)
**Value:** Not found — and this is an evidenced absence, with a trap attached.

Three independent checks, all negative:

- **No image asset of any kind is tracked at the pin.** Across all 139 tracked files there is no
  `.png`, `.svg`, `.jpg`/`.jpeg`, `.gif`, `.ico` or `.webp`, and no path containing `logo`, `icon`
  or `_static`.
- **`docs/conf.py` sets no `html_logo`.** It sets `html_theme = "sunpy"` and leaves the static path
  line commented out (`# html_static_path = ["_static"]`).
- **The PyHC registry entry for this project has no logo key**, unlike registry entries for projects
  that do have one.

**The trap: the rendered documentation site does display a logo, and it is not this package's.** The
image served there is `sunpy_icon.svg`, supplied by the shared `sunpy-sphinx-theme` that
`html_theme = "sunpy"` selects. It is the **SunPy project's** icon, used across every SunPy-affiliated
package's documentation. Recording it here would put the SunPy project's mark on
sunkit-instruments' catalogue page and misidentify the software — a visitor would reasonably read it
as this package's own logo. A documented absence is the correct outcome, and it should not be
"fixed" by borrowing the theme's icon.

If the project ever adopts its own mark, the value must be a URL that has been fetched and returns
image bytes, and — if it is hosted in this repository — pinned to a full 40-character commit SHA
rather than to a branch name.

---

## Additional Notes

### PyHC registry status

The project is listed in the Python in Heliophysics Community registry, in the **evaluated**
projects list (`_data/projects.yml`), not the unevaluated one. Its recorded contact is the "SunPy
Steering Committee", and its registry `description` and `docs` values are byte-identical to the ones
recorded in Fields 9 and 24. Its badge ratings, as recorded in the registry:

- **Community:** Partially met
- **Documentation:** Partially met
- **Testing:** Good
- **Software Maturity:** Good
- **Python 3:** Good
- **License:** Good

The registry keyword list holds `solar`, `specific` and `instrumentation` — see Field 16 for why
the middle term is not a usable keyword. The registry entry carries no logo key (Field 33).

### Release history

**Correction of a previous claim.** An earlier revision of this dossier stated that the package "has
had 8 major releases from v0.1.0 (2020-09-30) to v0.6.2". That conflated the number of *changelog
headings* with the number of releases. `CHANGELOG.rst` at the pin carries eight version headings —
0.1.0, 0.2.0, 0.3.0, 0.4.0, 0.5.0, 0.6.0, 0.6.1, 0.6.2 — but the repository carries fifteen tags,
because several patch releases (0.1.1, 0.1.2, 0.1.3, 0.3.1, 0.3.2) never received a changelog
section, and two tags are pre-release markers (`v0.2dev`, `v0.6.0a1`) rather than releases. None of
the eight is a "major" release in the semantic-versioning sense; the project has never released a
1.0.

What is durable: the release line runs from **v0.1.0 (2020-09-30)** to **v0.6.2 (2025-07-10)**, with
releases in most years since, and thirteen of the tags were published as GitHub releases and twelve
as PyPI uploads.

### Dependencies

**The previous dossier's "Key Dependencies" block is dropped rather than updated**, because it
recorded the pin's unreleased floors ("Python >= 3.12") as though they described the catalogued
release — the error corrected in Field 13 — and because it listed the generic scientific-Python
stack as though dependency membership were metadata, which Fields 29 and 30 explain it is not.

What is worth recording: the package's one *characterising* dependency is sunpy, declared at
`pyproject.toml:18` as `sunpy[map,net,timeseries,visualization]>=7.0.0`. It is not an ordinary
dependency — sunpy supplies the data types this package's public functions consume and return, which
is why it appears in both Field 29 and Field 30. Everything else declared at the pin (xarray,
astropy, scipy, numpy, h5py, matplotlib, pandas) is either generic infrastructure or was assessed
individually in Field 30.

Note that all of the version floors in `pyproject.toml` at the pin are the **unreleased** ones raised
by `changelog/185.breaking.rst`; the released `v0.6.2` declares lower minimums, `>=3.10` for Python
among them. (That changelog fragment contains two upstream typos worth recognising rather than
reproducing: it spells xarray "xarary" and gives its minimum as "2014.11.0", a year that predates
xarray's calendar versioning.)

### Supported instruments — what the package actually does for each

1. **GOES/XRS** — isothermal temperature and emission measure from soft X-ray irradiance via a
   CHIANTI-derived response table (`calculate_temperature_em`, satellites 1–19, with a flux
   rescaling for 8–15 and a special case for GOES 6); flare event retrieval from HEK
   (`get_goes_event_list`); conversion between flux and GOES flare class
   (`flux_to_flareclass`, `flareclass_to_flux`).
2. **Fermi/GBM** — weekly spacecraft pointing file retrieval, NaI detector zenith/azimuth geometry,
   detector-to-Sun angle calculation for a time or a date, and a line plot of those angles.
3. **PROBA2/LYRA** — LYTAF annotation handling: event retrieval from the four annotation databases,
   removal of flagged events from a time series, splitting a series at event boundaries, and an
   optional semicolon-delimited CSV dump of the event table (Field 19).
4. **RHESSI** — observing-summary database and HDU-list parsing, SolarSoft-compatible count-rate
   decompression, image back-projection from a calibrated event list, and image-cube-to-map-sequence
   conversion.
5. **GOES/SUVI** — FITS and netCDF L1b reading (including HDF5-backed L1b and `.gz` inputs), L2 HDR
   composite reading, L1b despiking, conversion of files to sunpy maps, and effective-area/gain-based
   response construction for the GOES-R flight models.

### Response function framework

The `response` subpackage is a general framework rather than an instrument-specific routine:
`AbstractChannel` defines the interface a channel must implement, `SourceSpectra` wraps a source
spectrum, and `get_temperature_response` combines them. It is written to be extended to instruments
beyond SUVI, which is part of why `Mission-related: Instrument Response` is a fair description of the
package and not merely of one module.
