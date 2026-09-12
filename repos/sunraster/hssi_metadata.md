# HSSI Metadata Extraction Results

**HSSI Software ID:** 44bf8c74-399d-4b9f-82ee-164c62e525a8
**Repository:** https://github.com/sunpy/sunraster
**Source Revision:** f950bcd0a2c2ff470bfa89da2d675561269f550d
**Extraction Date:** 2026-09-09
**Validation Date:** 2026-09-11
**Validation Status:** PASS

---

Scope note. All repository evidence below is read at the pinned revision above, which is the tip of
`main` on the extraction date. Two sources sit outside that tree and are named explicitly wherever
they are used, because a reader who checks out the pin will not find them: a **JOSS paper draft**
that lived at `joss_paper/paper.md` between 2023-02-19 and 2024-06-18 and is quoted here only at its
last content revision `cb71dc3`; and the project's **GitHub wiki**, a separate repository
(`sunraster.wiki.git`) whose ten Markdown pages are IRISpy-era and whose last commit, read on the
extraction date, is dated 2018-03-14. Neither is part of the software at the pin.
The draft matters anyway: it is the one place in the code repository's history where sunraster's
authors named themselves individually and named their funding.

Quotations are reproduced from the source named beside them. Where a source hard-wraps a sentence
across several lines, the line breaks are rendered as single spaces so the sentence reads as one; a
leading ellipsis marks a fragment that begins partway through its sentence; and where a quotation
comes from a database's rendering of a text rather than from the text itself, the field note says so.

---

## Section 1: Basic Information

### 1. Submitter

- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This entry predates the current refresh and the record does not identify who submitted it. The
placeholder is the catalogue-wide convention for a record whose submitter is not being changed.

### 2. Persistent Identifier (RECOMMENDED)

- **Value:** Not found

**sunraster has no DOI, and this is an instrumented negative rather than an unsearched field.**
DataCite was queried three ways on the extraction date: catalogue-wide free text (`query=sunraster`),
catalogue-wide title (`query=titles.title:sunraster`), and restricted to the Zenodo repository by the
client filter as a request *parameter* (`client-id=cern.zenodo` alongside `query=titles.title:sunraster`).
All three returned zero. Two controls establish that the queries were live and correctly shaped: the
identically-shaped `client-id=cern.zenodo` + `titles.title:ndcube` query returned twelve Zenodo
deposits for sunraster's sibling package, and a nonsense token returned zero. A creator-keyed check
on the draft paper's corresponding author (`creators.name:"Ryan, Daniel F."`) returned a large body of
his other work and no sunraster deposit, so the absence is not an artifact of searching only by
package name.

**The README's DOI badge is not sunraster's DOI, and must not be recorded as one.** `README.rst`
lines 14-15 at the pin read:

```
.. |DOI| image:: https://zenodo.org/badge/2165383.svg
   :target: https://zenodo.org/badge/latestdoi/2165383
```

The number in a Zenodo badge URL is a **GitHub repository id**, and 2165383 is the id of
`sunpy/sunpy`. sunraster's own GitHub repository id is 83324107. The badge therefore advertises sunpy
core's concept DOI (`10.5281/zenodo.591887`) on sunraster's front page — a template artifact carried
over from the SunPy package skeleton, not a claim that sunraster is deposited. The prior dossier
reached the same conclusion by a different route and its judgement is confirmed here.

**Consequence for other fields.** The absence of any deposit is why Field 11 records GitHub rather
than Zenodo as publisher, and why Field 12's Version PID is empty. If the project ever enables the
GitHub–Zenodo integration, the concept DOI becomes the correct value for this field and the versioned
DOI the correct value for Field 12.

### 3. Code Repository (MANDATORY)

- **Value:** https://github.com/sunpy/sunraster

Confirmed from three independent directions: the repository resolves directly; `pyproject.toml` at
the pin declares `"Source Code" = "https://github.com/sunpy/sunraster"` under `[project.urls]`; and
the PyPI record for the `sunraster` distribution carries the same URL as its Source Code link, which
closes the identity between the published distribution and this repository.

### 4. Software Functionality (RECOMMENDED)

- **Selected Values:**
  - Coordinate Transforms
  - Data Processing and Analysis
  - Data Processing and Analysis: 2D Slices
  - Data Processing and Analysis: Analysis
  - Data Processing and Analysis: Calibration
  - Data Processing and Analysis: Data Reduction
  - Data Processing and Analysis: Processing
  - Data Processing and Analysis: Spectrogram
  - Data Visualization
  - Data Visualization: 2D Graphics
  - Data Visualization: 2D Slices
  - Data Visualization: Line Plots
  - Data Visualization: Movies
  - Data Visualization: Spectrogram

Before this refresh HSSI held two values for this field, and both were bare top-level categories:
`Data Processing and Analysis` and `Data Visualization`. Those two parents are right and are kept.
What was missing was every subcategory, and the subcategory is what makes an entry findable — a
visitor filtering on `Data Visualization` alone is filtering on one of the taxonomy's six broadest
categories and learns nothing about what this package actually draws.

The functionality vocabulary is a two-level graph in which a child is identified by its parent as well
as its own name: it holds 83 rows built from 67 distinct names, so thirteen names occur under more
than one parent. `Spectrogram`, `2D Slices`, `Analysis`, `Calibration` and `Processing` are all among
the repeated names. Every subcategory above is therefore written in the fully qualified
`Parent: Child` form; an unqualified `Spectrogram` would be free to bind to either the processing or
the visualization row.

**Coordinate Transforms (parent only).** `SpectrogramCube`'s own class docstring advertises
`axis_world_coords`, `pixel_to_world` and `world_to_pixel` in its `Attributes` list, so world/pixel
transformation is presented to the user as part of this class's interface rather than hidden inside
it. The package adds physically-named accessors on top of that machinery — `spectral_axis`, `time`,
`exposure_time` and `celestial` in `sunraster/spectrogram.py`, each resolving the relevant axis
through `self.wcs.world_axis_physical_types` before returning world values — and
`docs/index.rst` advertises the capability directly: "The ``sunraster`` classes also inherit the
ability to crop by real world coordinates --- useful when locating a region of interest using
information from other observatories --- and a visualization suite which allows users to easily and
intuitively visually inspect their data."

**No child of Coordinate Transforms is selected, and `Solar` in particular was weighed and
declined.** The case for `Coordinate Transforms: Solar` is real and is recorded here so it is not
mistaken for an oversight: `sunraster/spectrogram.py` hard-codes solar physical types
(`"custom:pos.helioprojective.lon"`, `"pos.helioprojective.lon"` and their latitude counterparts) in
the lists `celestial` matches against, and `sunraster/instr/spice.py` imports
`sunpy.coordinates.HeliographicStonyhurst` to build the observer position returned by
`SPICEMeta.observer_location`. That is more solar-specific coordinate handling than a purely generic
container has. It is nonetheless not conversion *between* solar coordinate systems: sunraster reads
whatever frame the FITS WCS declares and hands back the frame it was given. All six children of this
parent name a physical domain whose transformations the software is expected to implement, and
sunraster implements none of them. A searcher filtering `Coordinate Transforms: Solar` is looking for
software that converts between Carrington, Stonyhurst and helioprojective frames, and would not be
served by this package.

**Data Processing and Analysis: Spectrogram.** The package's entire subject. Its three public classes
are `SpectrogramCube`, `SpectrogramSequence` and `RasterSequence` (`sunraster/__init__.py` exports
exactly these), and `pyproject.toml` describes the package as one that "provides the tools to read in
and analyze spectrogram data." Note the tension with the narrower signal-processing reading of the
word, under which a spectrogram is a time–frequency representation produced by an FFT or wavelet
transform; sunraster's spectrograms are the spatial–spectral images a slit spectrograph produces, and
it computes no transform to make them. The value is selected anyway, because in a heliophysics
catalogue the term plainly covers spectrograph data, and a visitor filtering on it would be glad
rather than annoyed to be shown the package named for exactly that data structure.

**Data Processing and Analysis: 2D Slices.** The headline capability. `RasterSequence` exposes
`slice_as_raster` and `slice_as_sns` (with the `_snsSlicer` and `_SequenceSlicer` helpers behind
them) so that the same 4-D raster sequence can be addressed as a 3-D sit-and-stare sequence and back,
and `_set_single_scan_instrument_axes_types` keeps the instrument-axis labelling consistent through
the operation. (The module also defines `_slice_scan_axis_types` for that job, but both of its call
sites are commented out at the pin, so it is not the live path — recorded so a later reader does not
cite a dormant helper as evidence.)
`docs/index.rst` describes the inherited slicing API as "allowing users to manipulate the same data
object as though it were 3D (time, position along slit, wavelength) or 4D (raster scan number, slit
step, position along slit, wavelength)". Extracting a 2-D plane out of that is the ordinary use.

**Data Processing and Analysis: Calibration.** `SpectrogramCube.apply_exposure_time_correction` and
its sequence-level counterpart, backed by `_calculate_exposure_time_correction` and
`_uncalculate_exposure_time_correction`, divide (or multiply) the data *and* its uncertainty by the
exposure time and change the unit accordingly, refusing to double-apply unless forced. The
documentation states the purpose in calibration terms:
"This is important both for converting between instrumental and physical units, e.g. DN to energy,
and comparing spectral features between exposure, e.g. line intensity."
**Considered and not determinative:** this is a narrow slice of calibration — the package applies no
flat field, gain, dark or radiometric response, and reads no calibration files. That argument is kept
rather than deleted, but it loses to the fact that exposure normalisation is a genuine calibration
step, is the package's most prominently documented processing method, and is described by the project
itself as a conversion to physical units.

**Data Processing and Analysis: Data Reduction.** Slicing and cropping reduce data volume while
preserving the full physical description — the slicing API carries uncertainties, mask and WCS
through with the data, and `docs/index.rst` advertises cropping "by real world coordinates" for
locating a region of interest. The JOSS draft (revision `cb71dc3`) put the same capability first
among the analysis tasks the classes support: "These classes provide support for analysis tasks, such
as extracting regions of interest and applying/removing exposure time corrections, as well as a
quick-look visualization suite."

**Data Processing and Analysis: Processing.** The general transform surface: the exposure-time
correction path, unit tracking through it, and the metadata restructuring `read_spice_l2_fits`
performs when it turns FITS header keywords into an `NDMeta`-backed `SPICEMeta`.

**Data Processing and Analysis: Analysis.** The package does not merely move arrays: it propagates
uncertainty through the exposure-time correction (both correction functions rebuild the
`NDUncertainty` instance with a rescaled array and unit), enforces units, and derives physical
quantities from the coordinate description via `spectral_axis`, `time` and `celestial`.
**Considered and not determinative:** sunraster computes no scientific quantity of its own — no line
fits, no Doppler velocities, no intensities. That is a real argument against the value and is
preserved so a later refresh reads it as weighed. It loses to the fact that uncertainty propagation
and unit enforcement are analysis machinery a searcher would want surfaced.

**Data Visualization and its five children.** Plotting is inherited from ndcube but is presented as
part of sunraster's interface: `SpectrogramCube`'s docstring lists `plot` among its attributes, and
`RasterSequence` defines `plot_as_raster = SpectrogramSequence.plot` and
`plot_as_sns = SpectrogramSequence.plot_as_cube` as its own named methods. The documentation states
what those methods produce, in near-identical sentences for each of the three classes. For
`SpectrogramCube`, `docs/data_types/spectrogram.rst` line 147: "This method produces different types
of visualizations including line plots, 2-D images and 1- and 2-D animations." The same statement is
made again at `docs/data_types/spectrogram.rst` line 395 for `SpectrogramSequence` and at
`docs/data_types/raster.rst` line 244 for `RasterSequence`. That sentence supplies
**Line Plots**, **2D Graphics** and **Movies** directly. **2D Slices** follows from the same
animation path: for a cube of three or more dimensions the animator displays two chosen axes as an
image and puts sliders on the remainder, so what the user sees is a 2-D slice of a
higher-dimensional volume — which is precisely the raster/sit-and-stare pair `plot_as_raster` and
`plot_as_sns` exist to switch between. **Data Visualization: Spectrogram** is the display counterpart
of the processing value above: what these methods draw is a spectrogram.

**Considered and rejected, with reasons.**

- **Data Processing and Analysis: Data Access and Retrieval** — proposed by the prior dossier and
  **wrong**. This subcategory is for downloading or querying remote archives, and sunraster has no
  such capability: it contains no `sunpy.net`/`Fido` use, no HTTP client, and no downloader. Its one
  reader, `read_spice_l2_fits`, takes filenames that already exist on disk. A searcher filtering this
  value wants a package that fetches data, and would install sunraster to discover it fetches
  nothing. Recorded explicitly so it is not re-proposed from the word "read".
- **Mission-related**, **Mission-related: Analysis**, **Mission-related: Instrumentation** — all three
  proposed by the prior dossier and all three rejected. The distinction the taxonomy draws is between
  software that *reads* a mission's data and software that is *part of* a mission's ground system or
  pipeline. sunraster is a community analysis library that happens to ship one instrument reader; it
  is not SPICE ground software, is not maintained by the SPICE team as an operations tool, and
  performs no ingest, archiving, monitoring or instrument operation. The draft paper's own framing
  agrees (revision `cb71dc3`): "Most of sunraster's tools are instrument-agnostic. However it does
  provide specific tools for reading Solar Orbiter/SPICE FITS files and hence helping SPICE users
  leverage the wider scientific Python ecosystem for their analysis."
- **Data Processing and Analysis: File Format Conversion** — the package reads FITS and writes
  nothing. See Field 19.
- **Data Processing and Analysis: Image Processing** — `NDCube.reproject_to` is inherited and
  therefore technically callable, but sunraster documents no image-processing operation, lists none
  among its class attributes, and tests none. Attributing a capability to sunraster purely because
  its base class has it would make this field a copy of ndcube's.
- **Data Processing and Analysis: Time Series Analysis** — sunraster exposes a `time` axis and can
  present a raster sequence as a time-ordered sit-and-stare sequence, but performs no temporal
  analysis: no filtering, no detrending, no autocorrelation, no periodogram.
- **Data Processing and Analysis: Energy Spectra** — a spectrum in wavelength is not an energy
  spectrum in the particle sense this value denotes.

### 5. Related Region (RECOMMENDED)

- **Selected Values:**
  - Solar Environment
  - Corona

`Solar Environment` was already stored and is kept. `Corona` is added.

The region vocabulary is **flat** — its 24 rows have no working parent/child structure, so a coarse
value never implies a fine one and a fine value never implies its coarse relative. "Solar Environment
encompasses the corona" is therefore not an argument for leaving the specific value off; both have to
be selected for both filters to find the entry. Campaign practice is to keep the coarse value
alongside the specific ones rather than replace it.

**Why `Corona`, and why the evidence for it is external.** The tracked tree at the pin contains no
occurrence of "corona" or "coronal" in any case — a case-insensitive search of the whole tracked tree
returns zero files for each, against seven files for "spectrograph" and thirty-one for "sunraster" as
positive controls. The region therefore cannot be read off the repository text, and is instead taken
from the one instrument sunraster is built to read. The instrument's own paper — *The Solar Orbiter
SPICE instrument. An extreme UV imaging spectrometer*, SPICE Consortium, Astronomy & Astrophysics 642,
A14 (2020), https://doi.org/10.1051/0004-6361/201935574 — carries the author-assigned subject keywords
"Sun: transition region" and "Sun: corona". Of those two, only the corona has a row in this
vocabulary. A visitor filtering on `Corona` for tooling that handles coronal spectroscopic
observations would be glad to find the package that reads Solar Orbiter/SPICE Level 2 rasters, and
the four published papers that acknowledge using sunraster (Field 27) are all coronal, active-region
or flare studies.

**Documented omission: there is no `Transition Region` row.** The vocabulary's solar rows are
`Photosphere`, `Chromosphere`, `Corona`, `Solar Interior`, `Solar Environment` and `Solar Wind`. The
transition region is half of SPICE's own declared science scope and cannot be recorded. This is a
vocabulary gap rather than a property of the software, and is written down so a future refresh
recognises the omission as deliberate and can fill it if a row is ever added.

**Considered and rejected.**

- **Chromosphere** — not supported by the evidence used for `Corona`: the instrument paper's keywords
  name the transition region and the corona, not the chromosphere. Selecting it would be an inference
  about SPICE's line formation temperatures rather than a reading of a source.
- **Photosphere**, **Solar Interior** — SPICE is an extreme-ultraviolet spectrometer; neither is
  within its observing scope, and nothing in the repository points at either.
- **Solar Wind** — solar wind source-region composition is a Solar Orbiter science theme, but that is
  the mission's scope rather than this software's, and no repository or instrument-keyword evidence
  ties sunraster to it.

### 6. Authors (MANDATORY)

- **Current value (one author):**
  - **Given Name:** The SunPy — **Family Name:** Community — **Identifier:** none — **Affiliation:** none

**The collective author stands alone: the stored value is kept, and the nine-author list from the
draft paper is not adopted.** The evidence points two ways and the choice changes what a visitor to
the site sees, so both sides are set out in full below as the record of why it was settled this way.

**What the software itself says.** `pyproject.toml` at the pin declares exactly one author:
`{ name = "The SunPy Community", email = "sunpy@googlegroups.com" }` as the sole entry in its
`authors` table. That is also what
PyPI shows and what the stored HSSI value reflects. The repository contains **no `CITATION.cff`, no
`.zenodo.json` and no `codemeta.json`** — checked against the full tracked file list at the pin — so
there is no machine-readable author list to reconcile against, and no "how to cite" file anywhere in
the tree.

**What the draft paper says.** The deleted JOSS draft, at its last content revision `cb71dc3`, names
nine authors in a deliberate order with ORCIDs and numbered affiliations. No competing author list
has ever existed in this repository: a scan of every path touched by any commit on any ref finds no
`CITATION.cff`, `AUTHORS`, `CONTRIBUTORS`, `codemeta.json`, `.zenodo.json` or credits file at any
revision, so the draft's block is the project's only self-declared author list:

| # | Author | ORCID | Affiliations as printed in the draft |
|---|---|---|---|
| 1 | Daniel F. Ryan (corresponding) | 0000-0001-8661-3825 | University of Applied Sciences Northwest Switzerland, Switzerland; American University, USA |
| 2 | Nabil Freij | 0000-0002-6253-082X | Lockheed Martin Solar and Astrophysics Laboratory, USA; Bay Area Environmental Research Institute, USA |
| 3 | Stuart Mumford | 0000-0003-4217-4642 | Aperio Software Ltd, UK |
| 4 | Baptiste Pellorce | none given | Claude Bernard Lyon 1 University, France; Institute of Theoretical Astrophysics, Norway |
| 5 | Steven D. Christe | 0000-0001-6127-795X | NASA Goddard Space Flight Center, USA |
| 6 | Ankit Kumar Baruah | none given | Workato Gmbh, Germany |
| 7 | Tiago Pereira | 0000-0003-4747-4329 | Institute of Theoretical Astrophysics, Norway; Rosseland Centre for Solar Physics, University of Oslo, Norway |
| 8 | Eric Buchlin | 0000-0003-4290-1897 | Université Paris-Saclay, CNRS, Institut d'Astrophysique Spatiale, France |
| 9 | Theresa A. Kucera | 0000-0001-9632-447X | NASA Goddard Space Flight Center, USA |

All seven ORCIDs resolve to the expected people. One name differs from its ORCID record:
0000-0001-9632-447X is registered as *Therese Kucera*, while the draft prints *Theresa A. Kucera*;
the identifier is what disambiguates, so this is a spelling variant rather than a mismatch.

The nine are consistent with the commit record without being a mechanical function of it. Commit
attribution over the full history (with the several spellings of each contributor's identity counted
separately, as `git shortlog -sne` reports them) puts Ryan far in front, followed by Pellorce,
Mumford and Freij, with Baruah, Christe and Pereira also substantial — but it also surfaces heavy
contributors who are **not** in the draft's list (notably Kris Stern, whose commits are split
across six author identities in that listing)
alongside bot accounts. The draft is an editorial judgement by the authors themselves, not a commit
ranking, which is exactly why it carries weight the shortlog does not.

**ROR research, recorded so it need not be repeated.** The affiliation strings above were resolved
against the ROR affiliation matcher. Five matched unambiguously: Bay Area Environmental Research
Institute `https://ror.org/024tt5x58`; Lyon 1 Université `https://ror.org/029brtt94` (the ROR display
name for Claude Bernard Lyon 1 University); Goddard Space Flight Center `https://ror.org/0171mag52`;
University of Oslo `https://ror.org/01xtthb56` (the parent of the Rosseland Centre); Institut
d'Astrophysique Spatiale `https://ror.org/014p8mr66`. Two more are identifiable by judgement rather
than by an unambiguous match: FHNW University of Applied Sciences and Arts Northwestern Switzerland
`https://ror.org/04mq2g308`, and American University `https://ror.org/052w4zt36` (the Washington DC
institution, which the matcher scores equal to an unrelated Spanish-language namesake). **Four have
no ROR at all:** Lockheed Martin Solar and Astrophysics Laboratory (a division, not a registered
organization), Aperio Software Ltd, Workato GmbH, and the Institute of Theoretical Astrophysics in
Norway (a department of the University of Oslo). Those would be recorded as organization names with
no identifier, which HSSI permits.

**There is no ROR for the SunPy Community either.** A ROR query for "SunPy" returns nothing, against
a control query for "NumFOCUS" that returns exactly one row. The collective author therefore cannot
be given an organization identifier.

**A stale contact name, corrected.** The prior dossier recorded "Nabil Freij (from PyHC registry)" as
sunraster's contact. The PyHC community-project registry gave the contact, when read on the
extraction date, as "SunPy Steering Committee", so the individual name no longer has a source. The
contact is not an HSSI field in any case, and no individual should be reintroduced here from it.

**Why the collective author alone.** Keeping "The SunPy Community" as the entry's single author is
what the package declares about itself at the pin, what PyPI shows, and what the catalogue already
stores. The draft paper that names nine people was never published (see Field 14), was deleted from
the repository in 2024, and has no successor: no author list of any kind exists at the pin. The
nine-author block above is kept for what it is — the project's only self-declared list of individuals,
with resolvable ORCIDs and affiliations, and the record of what was weighed here — not as a value
awaiting adoption.

**What that gives up, stated plainly**, so a later refresh reads this as a decision rather than an
oversight: no individual is discoverable through this entry, a visitor browsing by author will never
reach sunraster, and none of the nine people who wrote it is credited anywhere in the catalogue for
it. Two alternatives were weighed and not taken. Replacing the collective with the nine named authors
would give the entry resolvable ORCIDs and real affiliations, but would stop the catalogue reflecting
the package's own current declaration and would present a 2023 snapshot as the present author list,
dropping the collective credit the project deliberately uses. Keeping the collective *and* adding the
nine would discard nothing true and would make the people discoverable, at the cost of ten author
entries of which one is an organization-style collective with no identifier. The evidence that favoured
both — that the draft's deletion was incidental, commit `595b06b` of 2024-06-18 being a Python-version
bump that removed the draft along with other stale files rather than a statement withdrawing the
authorship claim, and that a self-declared author block with ORCIDs is stronger provenance than a
commit count — is genuine and is preserved rather than dismissed. It lost to the fact that the software
as it stands names exactly one author, and that is the author the catalogue reflects.

**A note that constrains how this field could ever be changed:** the stored collective author has an
empty identifier. Sending an identifier for an author row that already exists without one creates a
duplicate row and orphans the original, so the collective must not be "upgraded" in place through a
routine metadata update. It has no ROR to send in any case. The same rule would bind any of the draft's
authors if they were ever added: the draft gives Baptiste Pellorce and Ankit Kumar Baruah no ORCID, so
they would be created without one, and a later refresh must not "improve" them by sending an ORCID
through a metadata update — that mints a second row and orphans the first. Attaching an identifier to
an existing identifier-less author is a database-side correction, not a metadata update.

Separately, the collective is stored split as given name "The SunPy" and family name "Community",
which is a person-shaped split of an organization name; correcting that is a database-side change, not
something a metadata update can do, and it is recorded here as a known blemish rather than as a
proposal.

### 7. Software Name (MANDATORY)

- **Value:** sunraster

Lower-case throughout, and deliberately so: `pyproject.toml` declares `name = "sunraster"`, the
`README.rst` title is ``sunraster``, and the documentation refers to it in literal formatting rather
than capitalised prose. It is not "SunRaster" or "Sunraster". Unchanged.

### 8. Description (MANDATORY)

- **Value:** sunraster is an open-source Python library that provides the tools to read in and
  analyze spectrogram data. It is a SunPy-affiliated package which provides tools to analyze data
  from spectral data from any solar mission. The package supports reading and analyzing spectroscopic
  data, particularly from the SPICE instrument on Solar Orbiter, and provides data structures
  (SpectrogramCube, SpectrogramSequence, RasterSequence) for manipulating multi-dimensional spectral
  datasets with coordinate information.

Kept as stored. Its first sentence is the project's own one-line description, appearing verbatim as
the `description` field in `pyproject.toml`, as the opening line of `README.rst`, and as the PyPI
summary. Its second sentence is the GitHub repository description. Its third accurately summarises
the three exported classes and the one instrument reader.

**Considered and not adopted: a corrected second sentence.** The second sentence contains a doubled
phrase — "provides tools to analyze data from spectral data from any solar mission" — which is
inherited verbatim from the GitHub repository description and reads as a drafting slip in the
original. A corrected form would be "…which provides tools to analyze spectral data from any solar
mission." It was not adopted because the wording is an editorial choice already present in the
record and the defect belongs to the upstream source, not to the catalogue. The corrected clause is
written out here so that a later refresh meeting the same slip knows exactly what it would change
and why.

### 9. Concise Description (OPTIONAL)

- **Value:** A Python library for reading and analyzing solar spectrogram data from various missions,
  with built-in support for SPICE.

Kept as stored. It is accurate at the pin — the package is mission-agnostic apart from
`sunraster/instr/spice.py` — and it is a piece of authored prose rather than a derived value, so it
is not rewritten merely because it could be phrased differently.

### 10. Publication Date (RECOMMENDED)

- **Value:** 2017-02-27

Kept as stored. This is the date the repository was first published: GitHub records it as the
creation date, and the first two commits in the pin's ancestry (`56de36a` "Initial commit" and
`d45d357`, both by Steven Christe) carry the same date. The ancestry from that commit to the pin is
continuous — the project was created as IRISpy and later renamed, rather than restarted — so the
date describes this software's own public history and not some other package's.

**Alternative considered and not selected: 2020-04-20**, the upload date of `sunraster` 0.1.1, the
first release published under this name (PyPI has no 0.1.0). The field's guidance — "Date of first
broadcast/publication", "Used for the initial version of the software" — can fairly be read as
pointing at that first release, and under the name IRISpy the code had a different scope, including
IRIS slit-jaw and spectrograph modules that no longer exist. The stored value is nonetheless a
correct reading of that guidance for a package developed in the open from its first commit, and
it is not factually wrong, so it is left alone rather than traded for an equally defensible reading.
The alternative is recorded so a future refresh reads this as a decision rather than an oversight.

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Kept as stored, and correct under the field's own rule: Zenodo is the publisher only where a DOI was
obtained through the GitHub–Zenodo workflow, and otherwise the repository host is the value. sunraster
has no deposit (Field 2), so GitHub is right. The identifier is a URL rather than a ROR, which the
field explicitly allows. The publisher is a shared organization row used by many entries, so its
identifier is not something to "improve" from within this entry's metadata.

### 12. Version (RECOMMENDED)

- **Version Number:** v0.7.0
- **Version Date:** 2025-10-16
- **Version PID:** Not found

**The version number and date were already correct and are confirmed rather than changed.** v0.7.0 is
the newest release by three independent measures: it is the last tag in creation order in the pinned
clone, the newest GitHub release (published 2025-10-16), and the newest PyPI upload
(`0.7.0`, 2025-10-17T00:00:15Z). The date recorded is 2025-10-16, which is both the GitHub release
date and the date the project's own changelog prints in its section heading, `0.7.0 (2025-10-16)`;
the PyPI timestamp falls a few minutes later and crosses into 2025-10-17 in UTC, so PyPI prints the
following day for the same release rather than a different one. The `v` prefix
matches the git tag and the GitHub release name.

**No version description is recorded, and the changelog wording is preserved here so a later refresh
need not re-derive it.** HSSI held no version description before this refresh and none is added. The
GitHub release carries no description of its own: its `name` is the bare string `v0.7.0` and its
`body` is the auto-generated "What's Changed" pull-request list. The project's `CHANGELOG.rst` is the
only source that describes the release, under a single "Breaking Changes" subsection of three
bullets, quoted here without the pull-request link that follows each of them:

> - Increased the minimum version of Python to 3.10.0
> - Increased minimum required version of ``ndcube`` to 2.3.0. This comes with the removal of older
>   metadata handling methods which are now using upstreamed methods from ndcube.
> - Increased minimum version of Python to 3.12. Increased minimum version of NumPy to 1.26.0.
>   Increased minimum version of Astropy to 6.1.0. Increased minimum version of sunpy to 7.0.0.

**Considered and not adopted: a description composed from those bullets**, reading "Breaking changes
only. Increased the minimum version of Python to 3.12, NumPy to 1.26.0, Astropy to 6.1.0 and sunpy to
7.0.0, and increased the minimum required version of ndcube to 2.3.0, which comes with the removal of
older metadata handling methods which are now using upstreamed methods from ndcube." It is accurate,
but what it conveys to a visitor is a list of dependency floors rather than a characterisation of the
release, and writing it would not have been a free change: the version is stored as a record of its
own, so setting this field replaces that record and orphans the previous one. The version number and
date above are correct as they stand, and were not worth disturbing for that.

**Two findings about the changelog section survive the decision, because any future description drawn
from it must reckon with them.** First, its two Python bullets conflict: "Increased the minimum version
of Python to 3.10.0" and "Increased minimum version of Python to 3.12" are fragments from different
pull requests accumulated into one release, and the second supersedes the first. What the release
actually ships is 3.12 — `pyproject.toml` at tag `v0.7.0` declares `requires-python = ">=3.12"`, and
PyPI records the same for the uploaded distribution — so the stale 3.10.0 fragment must be dropped
rather than reproduced. Second, the prior dossier's own candidate wording, "Increased minimum Python
to 3.12, NumPy to 1.26.0, Astropy to 6.1.0, and sunpy to 7.0.0. Updated to use ndcube 2.3.0 minimum
with removal of older metadata handling methods.", has its facts right but silently reorders and
re-words the changelog's clauses into a synthesis; campaign practice is that a recorded value should
assert what its source says.

**Version PID is empty because no versioned deposit exists.** See Field 2 — the absence of any
sunraster DOI is established there with its controls. Nothing about v0.7.0 in particular was missed.

### 13. Programming Language (RECOMMENDED)

- **Value:** Python 3.x

Unchanged, and the tree makes it unambiguous. Of the 57 tracked files at the pin, 16 are `.py` and 16
are `.rst`; the remainder are configuration, two FITS test fixtures, and packaging files. A pattern
match over the tracked file list for compiled- and other-language source extensions
(`.c .h .f .f90 .f95 .for .pro .pyx .m .cpp .cc .jl .rs .java .js .ts`) returns **zero** files, so
there is no C, Fortran, IDL, Cython, MATLAB or Julia component to weigh. `pyproject.toml` declares
`requires-python = ">=3.12"`, which fixes the major version as 3.

`Python 2.x` and `Python 3.x` are separate rows in this vocabulary; only the latter applies. No second
value is recorded, in keeping with the field's own instruction to "Select the most important languages
(e.g., Python, Fortran, C). This is not meant to be an exhaustive list."

### 14. Reference Publication (RECOMMENDED)

- **Value:** Not found

**There is no publication describing sunraster, and the reason is worth recording in full because the
repository's history strongly suggests otherwise.** A JOSS paper was written: `joss_paper/paper.md`
and `joss_paper/paper.bib` were added on 2023-02-19 in commit `f8d8327` ("First draft JOSS paper."),
merged as pull request #231 on 2023-03-09 in commit `fcf6c7c` ("sunraster JOSS paper. (#231)")
together with a `draft-pdf.yml` workflow, revised through `cb71dc3` ("Update author info for JOSS
paper."), and then deleted on 2024-06-18 in commit `595b06b` ("bump python version (#257)").

**It was never published.** Crossref was queried for the JOSS prefix — `prefix:10.21105` with
`query.bibliographic=sunraster` — and returned nothing; the identically-shaped control query with
`query.bibliographic=ndcube` returned the sibling package's JOSS article
(`10.21105/joss.05296`), establishing that the query would have found a sunraster paper had one
existed. The DataCite searches recorded under Field 2 return nothing for sunraster either.

**Correction to a previously recorded claim.** The prior dossier reported that the CHANGELOG mentions
a sunraster JOSS paper pull request (#231) in version 0.5.0, while noting that no published JOSS DOI
was found. The changelog claim is false, and the falsity is instrumented rather than assumed.
`CHANGELOG.rst` at the pin contains no case-insensitive match for "joss" or "paper", against a
control search for "Removed" in the same file that returns four matches;
and a pickaxe search over the whole history for the string "paper" in `CHANGELOG.rst`
(case-insensitive) returns **no commits**, against a control pickaxe for "Removed IRIS reader" in the
same file that returns one. Pull request #231 is real, but it touched exactly three files —
`.github/workflows/draft-pdf.yml`, `joss_paper/paper.bib` and `joss_paper/paper.md` — and added no
changelog entry or fragment. The paper was never recorded in the changelog at all.

Recorded so that a future refresh, encountering the same PR title in the commit log, does not
re-derive the same wrong conclusion.

### 15. License (RECOMMENDED)

- **License:** BSD 2-Clause "Simplified" License

Unchanged and confirmed. GitHub's licence detection reports SPDX `BSD-2-Clause`, and the licence text
in the repository is the two-clause form: neither licence file contains a "neither the name … endorse"
third clause. The stored value is the canonical vocabulary row name, with the straight double quotes
the row actually uses.

**Two licence files exist and they carry different copyright lines, which is worth pinning down.**
`LICENSE.rst` at the repository root opens "Copyright (c) 2013-2025 The SunPy Developers", while
`licenses/LICENSE.rst` opens "Copyright (c) 2024, The SunPy Community". The file that governs the
distributed package is the second one: `pyproject.toml` declares
`license-files = ["licenses/LICENSE.rst"]`, and correspondingly PyPI's record for `sunraster` carries
a licence text beginning with the "The SunPy Community" line. The root file is the SunPy package
template's copy and is the one GitHub's UI surfaces. Both are BSD-2-Clause, so the divergence changes
no metadata value; it is recorded so a later reader does not treat the two copyright holders as a
conflict needing resolution.

**No per-software licence URI is recorded, and none can be.** The licence is stored as a reference to
a single shared licence row that carries its own URL; there is no per-entry licence URI to set. The
prior dossier listed "https://opensource.org/licenses/BSD-2-Clause (or
https://api.github.com/licenses/bsd-2-clause)" as if it were a value belonging to this entry. It is
not, and it is not carried forward.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- **Values:**
  - astronomy
  - astropy
  - data container
  - fits
  - plotting
  - python
  - solar
  - solar orbiter
  - solar physics
  - spectra
  - spectrograph
  - spectrograms
  - spice
  - sunpy

Keywords are the one open vocabulary in this form — an unrecognised value creates a row rather than
failing — so the discipline has to come from the metadata rather than from the API. The test applied
throughout is the searcher's: would a visitor who filtered the catalogue on this term be glad, or
annoyed, to be shown sunraster?

**Eleven of the thirteen stored keywords are kept unchanged**: astronomy, astropy, data container,
fits, plotting, python, solar, solar physics, spectra, spice, sunpy. Each is either a GitHub topic the
maintainers set, a PyHC registry term, or plainly true of the package.

**Three are added**, all of them rows that already exist in the vocabulary rather than new coinages:

- **spectrograph** — the instrument class the package exists for. The word appears in seven files of
  the tracked tree at the pin, including the documentation's data-type chapters, and "slit
  spectrograph data" is how `docs/index.rst` describes the package's subject.
- **spectrograms** — the data product, and the root of all three exported class names.
- **solar orbiter** — the mission whose instrument the package's only reader supports. A visitor
  filtering on the mission should reach this entry; before this refresh, nothing in the keyword set
  would have taken them there.

**Considered and rejected: `ndcube`.** It is the data model sunraster is built out of, and it has the
same ecosystem-naming appeal as the already-stored `astropy` and `sunpy`. It is not recorded because
it names a dependency rather than something a person searching the catalogue would type, which is the
test this field applies throughout.

**Considered and not added:** `spectroscopy`, `imaging spectroscopy`, `spectral imaging` and
`spectral data` all exist as rows and are all arguably applicable, but each overlaps the three added
terms without discriminating further; `slit-jaw imaging` was rejected outright, as slit-jaw imaging is
an IRIS capability sunraster does not have.

**Two stored keywords are removed: `sunrise` and `iris`.** Both were still declared as GitHub topics
on the repository at this refresh, which is why they entered the record; neither describes the
software at the pin.

- **sunrise** — the strongest negative in this dossier. The string "sunrise" does not occur anywhere
  in the tracked tree at the pin (case-insensitive, against a control term that returns 31 files),
  and a pickaxe search over the entire history in both `sunrise` and `SUNRISE` casings returns **no
  commit that ever added or removed a line containing it**, against a control pickaxe for "IRISpy"
  that returns fourteen. The SUNRISE balloon-borne observatory has never been referenced by this
  codebase in any revision. It also had no row in the instrument/observatory vocabulary at this
  refresh (Field 32).
  A visitor filtering on `sunrise` and finding sunraster would find nothing about SUNRISE in it.
- **iris** — historically accurate but no longer descriptive. sunraster did read IRIS data until
  version 0.4.0 (2022-03-08), whose changelog entry reads "Removed IRIS reader, you will want to
  install and use ``irispy-lmsal`` instead." At the pin the only occurrences of "iris" in the tracked
  tree are in `CHANGELOG.rst`, recording that removal and the changes that preceded it. A visitor
  filtering on `iris` is looking for IRIS tooling; sunraster is not it, and the entry that is
  (irispy) is named in Fields 29 and 30 where a reader will actually find the pointer useful.

The reasoning above is the record of why each was dropped, so neither is re-proposed from the
repository's GitHub topic list.

### 17. Data Sources (OPTIONAL)

- **Value:** Observatory/Mission-specific

Unchanged, and re-examined for additions rather than merely re-validated. The vocabulary's other
sixteen rows name general archives and access protocols — CDAWeb, HAPI, `The Virtual Solar
Observatory.` (whose row name really does end in a period, which is how it must be written if it is
ever selected), SSCWeb, OMNIWeb, AMDA, Madrigal, VirES, WDC, GFZ, TAP, das2, FTP/FTPS and HTTP/HTTPS
directories, S3/cloud-aware access, and Other. **None applies**, because sunraster retrieves
nothing: it has no network code of any kind, and `read_spice_l2_fits` operates on filenames the user
already has. The single stored value is right for the reason the field's guidance gives — the data it
does read is specific to one observatory, and the observatory is named in Field 32.

### 18. Input File Formats (RECOMMENDED)

- **Value:** FITS

Unchanged. `sunraster/instr/spice.py` reads Solar Orbiter SPICE Level 2 files with
`astropy.io.fits`, and the two data fixtures bundled in `sunraster/tests/data/` are SPICE Level 2
FITS files. No other reader exists in the package, and none of the vocabulary's other rows — CDF,
HDF5, netCDF3/4, Zarr, JSON, IDL.sav, ISTP-Compliant, ascii, csv, Other — corresponds to anything the
code can open.

### 19. Output File Formats (RECOMMENDED)

- **Value:** No value

**Correctly empty, and established by looking rather than by defaulting.** A search of the whole
tracked tree at the pin for the ways this package could write a file — `writeto`, `to_fits`, `savefig`,
`.write(`, `.save(`, and `open()` in a write mode — finds exactly two hits, both in
`sunraster/instr/tests/test_spice.py`, where `new_hdulist.writeto(...)` builds a temporary FITS
fixture for the reader's own tests. The public API exposes no serialisation at all: sunraster reads
data into objects and hands those objects to the user, who saves them with whatever library they
choose. Nothing was stored for this field before this refresh either, and that was already the right
answer; it is now the *evidenced* right answer.

### 20. Operating System (RECOMMENDED)

- **Value:** Operating System Independent

Unchanged. The package is pure Python with no compiled component (Field 13), and its continuous
integration exercises all three major platforms: `.github/workflows/ci.yml` at the pin runs its jobs
on `ubuntu-latest` and includes `windows: py312` and `macos: py312` in its test matrix. Selecting
`Linux`, `Mac` and `Windows` in addition was considered and rejected: those rows exist for software
that is genuinely platform-limited, and listing them beside `Operating System Independent` would
weaken rather than sharpen the claim.

### 21. CPU Architecture (RECOMMENDED)

- **Value:** CPU Independent

Unchanged. No compiled extension, no architecture-specific dependency, no GPU or HPC code path. The
vocabulary's other rows — `Apple Silicon arm64`, `Linux aarch64 or arm64`, `x86-64`, `ppc64le`,
`Sun (SPARC)`, `GPU`, `HPC or HEC`, `Other` — all describe constraints or targets this package does
not have.

### 22. Related Phenomena (OPTIONAL)

- **Value:** No value

**Correctly empty, and evidenced rather than skipped.** The phenomena vocabulary is flat and small —
its seven rows are Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar
Flares, Solar Wind and X-ray emission. Each was tested against the tracked tree at the pin. "coronal
mass ejection", "coronal heating", "geomagnetic storm", "solar wind" and "x-ray" return no files at
all; "corona" and "coronal" return no files in any casing, which is itself striking for a package
that reads an instrument named for the coronal environment. "flare" returns exactly one line, in
`docs/data_types/raster.rst`: "Another motivation can be to perform fast repeat raster scans in order
to improve the chances of catching an event with the slit, e.g., a solar flare." That is an
illustration of why an observer would choose a fast raster cadence, not a phenomenon the software
implements support for, and `Solar Flares` would fail the relevance bar on it.

The underlying reason is structural: sunraster is a container and manipulation library for
spectrograph observations, agnostic to what those observations are of. `Solar Corona` was the closest
call — Field 5 does record `Corona` as a region on the strength of SPICE's published observing scope —
but a region is where the data comes from, while a phenomenon is what the software is built to study,
and sunraster is built to study none in particular. Nothing was stored here before this refresh, and
the emptiness is now documented rather than merely inherited.

### 23. Development Status (RECOMMENDED)

- **Value:** Active

HSSI held no value for this field before this refresh. `Active` is recorded, and the vocabulary row's
own definition is the standard applied: "The project has reached a stable, usable state and is being
actively developed."

**The evidence on both sides, because this is the least comfortable value in the dossier.** The
project has plainly reached a stable, usable state: fourteen published stable releases — the pin's
twenty git tags less the five `rc`, `dev` and `post` tags and `v0.1.0`, which was never uploaded;
the same fourteen are the non-pre-release versions PyPI carries — a documented release series
reaching 0.7.0, packaging on both PyPI and conda-forge, and a documentation site. It also released
twice in the calendar year before the pin — 0.6.0 on 2025-06-12 and 0.7.0 on 2025-10-16 — each
carrying real breaking changes rather than housekeeping. Against that: **of the fourteen commits
between the `v0.7.0` tag and the pin, thirteen are package-template synchronisations authored by bot
accounts, and the fourteenth ("Update cruft with batchpr") is a maintainer running the same
template-sync tooling by hand.** No functional change has landed since the release. At this refresh
the repository was not archived and its issue tracker was open.

**Why `Active` rather than `Inactive`.** The competing row's definition is "The project has reached a
stable, usable state but is no longer being actively developed; support/maintenance will be provided
as time allows." Selecting it asserts that development has *stopped*, and nothing states that: there
is no deprecation notice, no archive flag, no README banner, and no maintainer statement anywhere in
the tree. A quiet interval following a release, in a small library whose upstream dependencies do most
of the moving, is not the same as cessation. The reading taken is that the run of template-only
commits records a maintained package between feature releases rather than an abandoned one.

**What would change this.** If a later refresh finds a further long interval with no functional
commit and no new release, `Inactive` becomes the better reading and this paragraph is the record of
why it was not chosen the first time. Note also that GitHub's `updated_at` timestamp is not evidence
of development activity — it moves for bot pushes, label changes and metadata edits — so it should not
be cited on either side of this question.

### 24. Documentation (RECOMMENDED)

- **Value:** https://docs.sunpy.org/projects/sunraster

Unchanged. `pyproject.toml` declares exactly this URL as `Documentation` under `[project.urls]` and
`README.rst` links the same site; it resolved to the current documentation build when fetched at this
refresh.

### 25. Funder (OPTIONAL)

- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

### 26. Award Title (OPTIONAL)

- **Values:**
  - **Award Title:** Solar Orbiter/SPICE — **Award Number:** 80NSSC19K1000
  - **Award Title:** NASA SDO/AIA contract to Lockheed Martin Solar and Astrophysics Laboratory — **Award Number:** NNG04EA00C

**Fields 25 and 26 are decided together, because they rest on the same single piece of evidence.**
HSSI held nothing for either field before this refresh, and the repository at the pin makes no funding
statement of any kind — there is no funding section in the README, none in the documentation, and no
acknowledgements file.

**The evidence.** The deleted JOSS draft, at revision `cb71dc3`, has an Acknowledgements section
reading in full:

> We acknowledge financial support for sunraster from Solar Orbiter/SPICE
> (grant 80NSSC19K1000) as well as NASA's SDO/AIA and IRIS missions
> (grant NNG04EA00C and NNG09FA40C).
> We also acknowledge the SunPy and Python in Heliophysics communities for their support.

That is a first-party statement by the software's own authors, written for publication, naming this
software explicitly rather than the missions generally. All three grants are NASA awards, so the
funder in every case would be the National Aeronautics and Space Administration, ROR
`https://ror.org/027ka1x80`.

**Decided: the funder and the two awards above are recorded; the third grant in the acknowledgement
is not.** That first-party character is what carries the values, and the deletion of the draft
that records the statement was incidental: commit `595b06b` of 2024-06-18 is titled "bump python
version (#257)" and removed the draft alongside other stale files while raising the Python floor and
updating CI. It is housekeeping, not a withdrawal of the funding claim. That is the standing reason a
deleted draft still supports a recorded value here.

Both recorded award titles and numbers already exist in the catalogue's award vocabulary with NASA
recorded as their funder, so the titles above are the catalogue's own wording rather than something
composed for this entry, and associating them with sunraster reuses existing awards rather than
creating new ones.

**The third grant, NNG09FA40C, is deliberately not recorded, and this is durable negative research.**
It is the IRIS grant in the acknowledgement, and unlike the other two it has no entry in the award
vocabulary. No authoritative title for it was found — a Crossref bibliographic query on the award
number returns nothing — and an award with no title cannot be recorded at all, so recording it would
mean inventing wording. A later refresh should not re-derive that dead end from the same
acknowledgement; the grant becomes recordable only if an authoritative title turns up.

**The argument for leaving both fields empty, preserved because it is not frivolous:** the paper was
never published and never peer-reviewed, the file no longer exists in the repository, the software as
it stands makes no funding claim of its own, and the acknowledgement is three years old and describes
support for work done up to 2023 rather than necessarily the software as it stands today. It lost to
the first-party character of the statement and to the fact that nothing in the repository's history
retracts it.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- **Value:** https://doi.org/10.1007/s11207-025-02561-6

**No publication describes sunraster (Field 14), but four peer-reviewed papers state that they used
it.** The acknowledgements sections indexed by ADS were searched for the software's name
(`ack:"sunraster"`), which returned exactly these four; a nonsense-token control on the same index
returned zero. A full-text search (`full:"sunraster"`) returns nine records: these same four plus five
others. Four of those five are false positives caused by *Sun Raster*, an unrelated legacy image file
format that appears in GIS, radar and medical-imaging papers — two GIS papers, an InSAR web-tool
paper and a volumetric change-detection paper. The fifth is a genuine mention: the ndcube paper
(Ryan et al. 2023, https://doi.org/10.3847/1538-4357/ace0bd), which names sunraster in passing in its
full text but not in its acknowledgements — which is why the `ack:` search does not return it — and
which is considered and excluded on its own grounds at the end of this field. The four
acknowledging papers, with the sentence in which each names the package:

| Paper | DOI | How it names sunraster |
|---|---|---|
| Janvier et al. 2023, *A multiple spacecraft detection of the 2 April 2022 M-class flare and filament eruption during the first close Solar Orbiter perihelion*, A&A 677, A130 | https://doi.org/10.1051/0004-6361/202346321 | "…his research made use of several open-source software packages including SunPy ( The SunPy Community 2020 ), sunraster, AstroPy ( Astropy Collaboration 2022 ), and matplotlib ( Hunter 2007 )." |
| Ryan et al. 2025, *Solar Orbiter's 2024 Major Flare Campaigns: An Overview*, Solar Physics 300, 152 | https://doi.org/10.1007/s11207-025-02561-6 | "…ndcube (Ryan et al. 2023a , b ), sunraster, sospice, and fiasco Python packages, and by the SolarSoftware (SSW) distribution." |
| Zhu et al. 2025, *Active region upflows in various coronal structures and their coupling to the lower atmosphere*, A&A 701, A205 | https://doi.org/10.1051/0004-6361/202555618 | "…Sunkit-magex (Stansby et al., 2020); Sunkit-pyvista (Sullivan & Kaszynski, 2019); Sunraster; WATROO (Auchère et al., 2023); EISPAC (Weberg et al., 2023); irispy-lmsal; SAFFRON (MZERGUAT, 2024)…" |
| Zambrana Prado et al. 2026, *First ionization potential fractionation of sulfur observed with spectral imaging of the coronal environment*, Phil. Trans. R. Soc. A 384, 20250186 | https://doi.org/10.1098/rsta.2025.0186 | "Python modules used include: fiplcr , numpy , matplotlib , astropy , scipy , sunpy , sunraster , sospice , and cblind ." |

(Three of the four fragments — Janvier, Ryan and Zambrana Prado — are quoted from the acknowledgement
text **as ADS's `ack` index renders it**, which pads inline citations with spaces and drops the comma
after "et al."; the quotation reproduces that rendering, not the publishers' typography. The Janvier
fragment opens mid-word, on "his research" from "This research", because ADS's snippet window clipped
it there, and the leading ellipsis marks the clip rather than a dropped character. The Zhu fragment
is quoted instead from the published full text at arXiv:2509.02157v1, with the citation spacing of
that text, which keeps the ampersand and the commas that ADS's rendering drops. ADS does hold an
acknowledgement snippet for that record as well: `ack:"sunraster"` matches it, and the snippet is
returned through the search API's highlighting parameters rather than in a plain field list. Anyone
rechecking these four quotations should note that the highlighting response is keyed by an internal
record number rather than by bibcode, which makes a snippet easy to mistake for absent.)

**One of the four is recorded — Ryan et al. 2025 — and the other three are deliberately kept
available for a later refresh to add.** The field's own definition is "Publications that describe,
cite, or use the software that the software developer prioritizes but are different from the reference
publication." sunraster's developers have never nominated any publication: there is no "how to cite"
file, no acknowledging page in the documentation, and no reference publication to be different from.
Ryan et al. 2025 is the one paper that comes close to a developer's own nomination — it is
first-authored by the draft paper's own corresponding author — and on the strict reading of a field
about publications the *developer* prioritizes, that is what earns it the entry.

**Janvier et al. 2023, Zhu et al. 2025 and Zambrana Prado et al. 2026 are not rejected; they are
recorded here as future possibilities.** Each is as solid a usage as Ryan et al. 2025, and the case
for carrying all four is a real one: they are the entry's only evidence of scientific use, the set is
small and enumerable rather than a large citing literature, and a visitor who wants to know whether
anyone actually analyses SPICE data with this package had nowhere on the entry to find that out before
this refresh. The four-row table above is the starting point for a later refresh that decides the
strict reading is too narrow: the research behind those three DOIs does not have to be done again to
add them.

**A constraint on anything recorded here:** the entry's related-item links render as their raw URL, so
a visitor sees an opaque DOI string with no title. The citations in the table above are the durable
record of what those DOIs are.

**Considered and rejected:** the **SPICE instrument paper** (SPICE Consortium 2020,
https://doi.org/10.1051/0004-6361/201935574) and the **ndcube paper** (Ryan et al. 2023,
https://doi.org/10.3847/1538-4357/ace0bd). Both are cited elsewhere in this dossier as evidence — the
first for Field 5's region, the second as the paper of the package sunraster is built on — but neither
tells a reader anything about *this* software. The first describes an instrument whose data sunraster
happens to read; the second describes a dependency and mentions sunraster only in passing. Recorded
here so neither is re-proposed from its appearance elsewhere in this file.

### 28. Related Datasets (OPTIONAL)

- **Value:** https://doi.org/10.48326/idoc.medoc.spice.5.0

HSSI held no value for this field before this refresh. sunraster's one instrument reader,
`read_spice_l2_fits`, is written for Solar Orbiter/SPICE **Level 2** FITS files, and the two fixtures
bundled at `sunraster/tests/data/` are real SPICE Level 2 files
(`solo_L2_spice-n-ras-db_20200602T081733_V01_12583760-000.fits` and
`solo_L2_spice-n-sit_20200620T235901_V01_16777431-000.fits`). Those data are published by IDOC with
DOIs, and the value recorded is the most recent release, *Data issued from SPICE instrument on Solar
Orbiter: data release 5.0*.

**Research recorded so it is not repeated.** The SPICE data are published as five independent release
DOIs — `10.48326/idoc.medoc.spice.1.0` through `.5.0`, from 2021 to 2024 — and **no concept or series
DOI covering them existed at this refresh**: release 5.0's DataCite record carried an empty
`relatedIdentifiers` list, so the releases are not linked to one another and none of them stands for
the series. That is why a single versioned DOI is recorded rather than a version-independent one.
sunraster reads Level 2 files from any release; the choice of 5.0 reflects only that it is the
newest, and a future refresh should move this value forward if a release 6.0 appears rather than
assuming the recorded DOI is version-independent. Listing all five was considered and rejected as
noise: they would render as five near-identical opaque URLs on the entry.

### 29. Related Software (OPTIONAL)

- **Value:** https://github.com/sunpy/sunpy

**This replaces the previously stored `https://doi.org/10.5281/zenodo.591887`.** The two identify the
same software — that DOI is sunpy core's Zenodo concept DOI — but the entry's related-item links
render as their raw URL, so the stored DOI showed a visitor an opaque `doi.org/10.5281/zenodo.591887`
string where a repository URL names the software being pointed at. Where a relation names another
entry in this catalogue, campaign convention is to use that entry's own stored repository URL, which for
SunPy is `https://github.com/sunpy/sunpy`.

**Why sunpy belongs in this field.** sunraster is a SunPy Project affiliated package, and this is
distinguishing information about it rather than a generic dependency fact: `docs/index.rst` opens
"``sunraster`` is a free, open-source, community-developed, SunPy-affiliated package that provides
tools to manipulate and visualize slit spectrograph data", `README.rst` carries a "Powered by SunPy"
badge, and `pyproject.toml` makes `sunpy>=7.0` the entire content of the `instr` optional-dependency
group — that is, sunpy is what you install in order to use the SPICE reader at all. The same URL also
appears in Field 30, for the different and independently evidenced reason set out there.

**Considered and placed elsewhere: irispy.** sunraster's relationship with irispy-lmsal is real and
strong, but it is a *linkage* rather than a similarity, and this field's own text distinguishes
software that "performs similar tasks but does not necessarily link together (which would be
'interoperable software')". It is recorded in Field 30 with its evidence.

**Considered and placed elsewhere: ndcube.** An argument exists for listing it here as the
domain-specific dependency that most characterizes the software. It is recorded in Field 30 instead,
where the claim is stronger and where the catalogue already records the relation from ndcube's side;
duplicating it here would add no information a reader does not get from Field 30.

**Considered and rejected: IRISpy as a predecessor.** This repository *is* the former IRISpy — created
2017-02-27 under that name and later renamed, with continuous git ancestry to the pin — so Field 29's
provision for "software this work was forked from" nearly applies. It is not recorded because there is
no separate predecessor to point at: no distinct IRISpy repository exists, and the only surviving
IRISpy artifacts are ten wiki pages in the project's separate wiki repository, last edited
2018-03-14. A reader following such a link would learn nothing about the current software.

**Considered and rejected: numpy.** A required dependency (`numpy>=1.26.0`) and generic
infrastructure. Depending on numpy is true of nearly every package in the catalogue and distinguishes
nothing.

### 30. Interoperable Software (OPTIONAL)

- **Values:**
  - https://github.com/sunpy/ndcube
  - https://github.com/LM-SAL/irispy
  - https://github.com/sunpy/sunpy

**HSSI held no values for this field before this refresh, and that was the record's largest
asymmetry:** ndcube's and irispy's catalogue entries each named
`https://github.com/sunpy/sunraster` in *their* interoperable-software fields at this refresh, while
sunraster named neither. The relation was recorded in one direction only. Each URL below is the
catalogue entry's own stored repository URL, so the link text a visitor sees is legible.

- **ndcube** — a shared data model, which is the exact exchange this field exists for and the case the
  field's own guidance uses as a worked example. The relationship is inheritance, not mere use:
  `sunraster/spectrogram.py` defines `class SpectrogramCube(NDCube, SpectrogramABC)`,
  `sunraster/spectrogram_sequence.py` defines `class SpectrogramSequence(NDCubeSequence, SpectrogramABC)`,
  `sunraster/meta.py` builds its metadata hierarchy on `ndcube.meta.NDMetaABC`, and
  `read_spice_l2_fits` returns an `ndcube.NDCollection`. `pyproject.toml` requires
  `ndcube[all]>=2.3.2`. A sunraster object *is* an ndcube object and can be handed to anything that
  accepts one.
- **irispy** — distributed as `irispy-lmsal`; `https://github.com/LM-SAL/irispy-lmsal` redirected, when
  followed at this refresh, to the URL recorded above, which is also the URL this catalogue stores for
  that entry. The exchange runs in both directions. sunraster hands IRIS support off to it:
  `CHANGELOG.rst` for 0.4.0 reads "Removed IRIS reader, you will want to install and use
  ``irispy-lmsal`` instead." And irispy builds on sunraster's classes — the JOSS draft (revision
  `cb71dc3`) states "In addition, the data and metadata classes in the IRIS mission's Python user
  tools package [irispy-lmsal; @irispy-docs; @irispy-code] inherit from and build upon those provided
  by sunraster."
- **sunpy** — a specific object exchange in the public API, not a dependency claim.
  `sunraster/instr/spice.py` imports `sunpy.coordinates.HeliographicStonyhurst` and
  `SPICEMeta.observer_location` returns a `SkyCoord` in that frame, so a sunraster metadata object
  emits a sunpy-framed coordinate that any sunpy-based workflow can consume directly. `sunpy>=7.0`
  is required precisely to use the SPICE reader, and `sunraster/instr/tests/test_spice.py` exercises
  the frame in its assertions.

**Considered and rejected, with reasons.**

- **astropy** — weighed as a Tier B candidate on cited public-API evidence, and not recorded. The
  evidence is real and is preserved here so it is not re-proposed from the code: astropy types are
  sunraster's documented interchange currency — `SpectrogramCube.__init__` takes an `astropy.wcs.WCS`
  as its coordinate description, `time` returns an `astropy.time.Time`, `spectral_axis` and
  `exposure_time` return `astropy.units.Quantity`, `celestial` returns an
  `astropy.coordinates.SkyCoord`, the exposure-time correction rebuilds an astropy `NDUncertainty`
  and rewrites the astropy unit, `read_spice_l2_fits` reads through `astropy.io.fits`, and the
  documentation's worked examples construct cubes from astropy objects directly. What that exchange
  runs on is the NDData, WCS and units infrastructure shared by the whole astronomical Python stack —
  generic infrastructure rather than a relation that distinguishes this software, which is the same
  test that excluded numpy from Field 29.
- **numpy** — Tier A, without exception. It is a required dependency and generic array
  infrastructure; being a dependency is not interoperability.
- **matplotlib** — generic plotting infrastructure, and Tier A regardless. It is also not a declared
  dependency of sunraster: `pyproject.toml` lists only `numpy>=1.26.0`, `astropy>=6.1.0` and
  `ndcube[all]>=2.3.2`, and the sole mention of matplotlib in the tracked tree at the pin is an
  intersphinx mapping in `docs/conf.py`. The plotting stack reaches the user through ndcube's
  visualization layer, not through sunraster.
- **sospice** and **fiplcr** — both appear alongside sunraster in the software lists of two of the
  papers in Field 27, which makes them look like natural companions. Neither is referenced anywhere in
  sunraster's tracked tree at the pin, in its packaging, or in its documentation. Being used in the
  same analysis by the same scientists is not a demonstrated exchange between the packages, and these
  should not be re-proposed from the acknowledgement lists alone.
- **"part of the standard scientific Python ecosystem" / "a PyHC member, so it interoperates with
  PyHC packages"** — the two justifications the field guidance singles out, in those words, as never
  sufficient on their own. Neither is used above; each of the three entries rests on named code or
  documentation.

### 31. Related Instruments (OPTIONAL)

- **Value:**
  - **Name:** Spectral Imaging of the Coronal Environment
  - **Identifier:** https://spase-metadata.org/SMWG/Instrument/SolarOrbiter/SPICE

Unchanged, and re-resolved against the controlled vocabulary rather than accepted on trust.
Sweeping the rows' `name`, `abbreviation` and `identifier` columns for "SPICE" with word-boundary
matching returns **exactly one** row, of instrument type, and it is the one stored; that row carries
an identifier under `https://spase-metadata.org/`, which is the SPASE-only guarantee this field
depends on — a bare name here would create an identifierless row. A nonsense-token control on the
same sweep returns zero. The name above is that row's own name copied
verbatim, which is why it is the expanded form rather than the acronym.

**Why this instrument is genuinely "designed to support" rather than merely mentioned.**
`sunraster/instr/spice.py` is a 463-line, purpose-built reader: `read_spice_l2_fits` parses Solar
Orbiter SPICE Level 2 FITS files into sunraster objects, and its `SPICEMeta` class carries all 29 of
that file's `@property` accessors, each one mapping a SPICE-specific FITS header keyword onto a named
attribute — `spectral_window`, `slit_id`, `slit_width`, `window_type`, `contains_dumbbell`,
`dumbbell_type`, `darkmap_subtracted_onboard`,
`bias_frame_subtracted_onboard`, `spice_observation_id`, `observing_mode_id_solar_orbiter`,
`carrington_rotation`, `solar_B0`, `solar_P0` and the rest. There is a dedicated test module and two
real SPICE Level 2 files bundled as fixtures. A user working with SPICE data would reach for this
package, and a visitor filtering the catalogue on this instrument should be shown it.

**Considered and rejected: IRIS.** The Interface Region Imaging Spectrograph does have an instrument
row, `https://spase-metadata.org/SMWG/Instrument/IRIS/IRIS`, so this is a deliberate omission rather
than an unresolvable one. sunraster supported IRIS until version 0.4.0 (2022-03-08), whose changelog
entry reads "Removed IRIS reader, you will want to install and use ``irispy-lmsal`` instead." At the
pin the package contains no IRIS code whatsoever: the only occurrences of "iris" in the tracked tree
are in `CHANGELOG.rst`, recording the removal and the work that preceded it. Recording the instrument
would tell a visitor searching for IRIS tooling that sunraster supports IRIS, which it does not; the
correct destination for that visitor is irispy, which is named in Fields 29 and 30 and which holds the
IRIS instrument and observatory associations in its own catalogue entry. This is the entry's most
tempting wrong value and is written down so it is not re-proposed from the GitHub topic list or the
changelog.

**Considered and rejected: EIS on Hinode.** The JOSS draft (revision `cb71dc3`) names it, along with
IRIS and SPICE, as an example of the instrument class — "Rastering or Scanning slit-spectrographs, as
such instruments are known, have been successfully employed for solar UV/EUV observations, e.g. the
EUV Imaging Spectrograph onboard Hinode [EIS; @eis]". That is a mention establishing what kind of
data the package is for, not support for a particular instrument. sunraster has no EIS reader.

**Considered and rejected: SUNRISE.** The repository declares `sunrise` as a GitHub topic, but there
was no SUNRISE row in this vocabulary at this refresh — a word-boundary sweep of the rows' `name`,
`abbreviation` and `identifier` columns returned zero, against a nonsense-token control that also
returned zero and the `SPICE` sweep above that returned one — and, as recorded under Field 16, the
string has never appeared in this repository's tracked content in any revision. There is nothing to record and
nothing to support recording it.

### 32. Related Observatories (OPTIONAL)

- **Value:**
  - **Name:** Solar Orbiter
  - **Identifier:** https://spase-metadata.org/ESA/Observatory/SolarOrbiter

Unchanged. Solar Orbiter is the platform carrying the instrument sunraster reads, and the association
is the platform-level counterpart of Field 31.

**A duplicate exists, and the stored row is the right one of the two.** Sweeping the vocabulary for
"Solar Orbiter" returns two observatory-type rows with identical names:
`https://spase-metadata.org/ESA/Observatory/SolarOrbiter` and
`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SolO`. The first is the mission's own record
under the agency that flies it; the second sits under a `CDPP-AMDA` path and is a data-centre
catalogue mirror. The stored value is the first. This is recorded so a later refresh, meeting two
rows with the same name, does not switch to the other or flag the pair as an ambiguity needing
resolution — it is resolved, and this is the resolution.

**Considered and rejected: IRIS as an observatory** (`https://spase-metadata.org/SMWG/Observatory/IRIS`),
for the reasons given under Field 31.

### 33. Logo (OPTIONAL)

- **Value:** Not found

**sunraster has no logo, and this is one of the more thoroughly established negatives in this
dossier.** Three independent checks:

1. **No image file has ever existed in the repository.** The union of every path touched by any commit
   on any ref — 307 distinct paths, of which 57 are tracked at the pin — contains no file with an
   image extension (`.png .jpg .jpeg .svg .gif .ico .webp .bmp .tif`). There is no deleted logo to
   recover and no branch holding one.
2. **The documentation sets no logo.** `docs/conf.py` at the pin sets `html_theme = "sunpy"` and
   nothing else logo-related: there is no `html_logo`, no `html_favicon`, and the `html_static_path`
   line is commented out. Whatever branding the rendered documentation shows comes from the shared
   `sunpy-sphinx-theme` package, and belongs to the SunPy Project rather than to sunraster.
3. **The PyHC registry carried no logo for it either at this refresh.** sunraster's entry in the
   registry's community project list (`_data/projects.yml`) carries `name`, `description`, `docs`,
   `code`, `contact`, `keywords` and the six maturity badges — and no `logo` key. That the key would
   have been used if one existed is visible in the same file, where the entry immediately following
   sunraster's, `swxsoc`, does carry a `logo:` URL.

**Considered and rejected: using SunPy Project branding.** The prior dossier observed that sunraster
"uses SunPy branding as an affiliated package", which is true of the rendered documentation but is not
a reason to record a SunPy logo here. It would identify the wrong software on the entry, and the
README's badges — shields.io status images and the "Powered by SunPy" and "Powered by NumFOCUS"
banners — are affiliation markers, not this package's mark. A documented absence is the correct
outcome; nothing should be invented to fill the field.
