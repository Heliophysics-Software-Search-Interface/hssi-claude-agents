# HSSI Metadata Extraction Results

**HSSI Software ID:** 21326fa6-355c-4e2e-8c34-90a91eda0eb6
**Repository:** https://github.com/space-physics/scanning-doppler-interferometer
**Source Revision:** f0f0074cd6625e0535e1c18f6c642403f065359b
**Extraction Date:** 2026-09-03
**Validation Date:** 2026-09-04
**Validation Status:** PASS

---

**Scope note — this repository is archived, and that changes how its evidence reads.** The GitHub
repository is archived (read-only; it accepts no issues and no pull requests), so the pinned revision
`f0f0074cd6625e0535e1c18f6c642403f065359b` (2022-08-11) is not merely the current tip of `main` — it
is the software's **final state**. Every "current" statement below is therefore also a durable one:
while the repository remains archived, no later commit can supersede it. The repository's own wiki
does not exist as a repository (`<repo>.wiki.git` returns "Repository not found"; a positive control
on another repository's wiki resolves normally), so GitHub's `has_wiki: true` flag carries no
documentation here.

**A second scope fact shapes almost every field below: this software was never released.** In
nineteen commits across four and a half years the repository accumulated no git tag, no GitHub
release, and no PyPI distribution. The version string in packaging metadata is the only version
identity that has ever existed. This is the "declared, never released" shape, and it is the reason
Fields 2, 12 and 14 resolve the way they do — there is no release artifact, no deposit, and no
citable object anywhere outside the repository itself. It is a different situation from a project
that released and then went quiet, and a future refresh should not go looking for a tag range or a
deposit history that never existed.

**Third: the whole package is small enough to read completely, and it was.** Twenty tracked files at
the pin, of which six are Python source — three of them forming the installed package and totalling
under a hundred lines — one is a 384-line IDL
routine in an `archive/` directory, one is a 23,151-line sample data file, and one is a PNG. Claims
below about what the software does and does not do are claims about a tree that was read in full,
not inferences from a sample. **One caution on the scope of that statement, learned the hard way:**
reading the tree in full is reading it *at the pin*, and a file deleted before the pin is invisible
to it. Claims about the project's history — CI configuration, licence files, README format — must be
derived from the whole ancestry instead. See Field 20, where exactly that distinction mattered.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The bracketed placeholder is this catalogue's convention for an entry whose metadata was compiled by
a curator rather than supplied by the software's own maintainer. It is not a missing value, and it
should not be "fixed" by inventing a submitter.

`setup.cfg` does carry `author_email = scivision@users.noreply.github.com`. That is a GitHub
no-reply address belonging to the author, not to a submitter, and Field 6 defines no author-email
sub-field in any case — so it is recorded here as context and used nowhere.

### 2. Persistent Identifier (RECOMMENDED)
**Persistent Identifier:** Not found

**This software has no DOI, and the search that establishes that is recorded here in full so it is
not repeated.** The negative is unusually well supported, because three independent routes were
checked and each carries its own control.

**Route 1 — the repository cites nothing.** A case-insensitive search of every tracked file at the
pin for `doi`, `zenodo`, `citation`, `cite`, `bibtex` and `arxiv` returns **zero** matching lines, as
does a search for the DOI prefix pattern `10\.[0-9]{4,}/`. Both commands exit with status 1 (no
match). The search apparatus is working: the same command form run for `wind` returns thirty
matching lines across
seven files. There is no `CITATION.cff`, no `.zenodo.json`, no `codemeta.json`, and no DOI badge in
the README — the README contains no badges at all at the pin. It did carry three until `678147a`
(2022-08-11, the second-to-last commit): Travis CI, AppVeyor and Coveralls status images, all three
removed in the same cleanup that immediately preceded archiving. **None of them was a DOI badge**, so
the conclusion is unchanged over the whole history and not merely at the tip — but the badges are
recorded here because their existence is the visible trace of a CI history that the pinned tree hides
(Field 20).

**Route 2 — Zenodo holds no deposit, proved differentially.** Sixteen queries against the Zenodo
records API return zero hits, among them
`"scivision/scanning-doppler-interferometer"`, `"space-physics/scanning-doppler-interferometer"`,
`title:"scanning doppler interferometer"`, `creators.name:"Hirsch" AND doppler`, and
`creators.name:"Conde" AND "scanning doppler interferometer"`. The differential control is what makes
this conclusive rather than merely suggestive: the *identical* `scivision/<repo>` query shape returns
**1** hit for `"scivision/pyiri90"` (`10.5281/zenodo.1186963`) and **1** for `"reesaurora"`
(`10.5281/zenodo.1323860`) — both sibling repositories by the same author, both with
GitHub-Zenodo deposits — while a nonsense token returns 0. So the query shape does find this author's
deposits when they exist. It finds none for this repository because none exists.

**A false friend, recorded so it is not rediscovered and mistaken for a hit.** The query
`creators.name:"Hirsch" AND interferometer` does return a record: a 1927 German-language article,
*Über Refraktometer und Interferometer*, by an unrelated Hirsch. It has nothing to do with this
software, this author, or heliophysics. Any future search that pivots on the surname plus the
instrument word will surface it again.

**Route 3 — PyPI has no distribution.** The PyPI **JSON** API is the authoritative check here and
returns HTTP 404 for `scanning-doppler-interferometer` (the `setup.cfg` distribution name, which is
also the PEP 503 normalisation of the stored software name), `scanning_doppler_interferometer`,
`ScanningDopplerInterferometer` and `sdi`. Use the JSON API and not the HTML project page: the page
can answer 200 for names that have no distribution, which would manufacture a false positive. Three
neighbouring names *do* resolve and are all unrelated software — `sdi-python` (a cybersecurity SDK),
`pysdi` (drought indices) and `sdipy` (a sensor protocol library). None is this package; none should
ever be recorded as its distribution.

Field 12's version number therefore has no version PID either, and Field 11's publisher is the
repository host rather than Zenodo. Both follow from this field.

### 3. Code Repository (MANDATORY)
**Repository URL:** https://github.com/space-physics/scanning-doppler-interferometer

Confirmed as the canonical form, and it is what `setup.cfg` itself declares at the pin
(`url = https://github.com/space-physics/scanning-doppler-interferometer`) — the single GitHub URL
anywhere in the tree.

**The repository moved owners, and the old URL still works.** It was created 2018-03-16 under
`scivision` and later moved to the `space-physics` organization;
`https://github.com/scivision/scanning-doppler-interferometer` answers HTTP 301 with a `Location` of
the `space-physics` form recorded here, and the GitHub API for the old path returns
`Moved Permanently`. The `scivision` account still exists as a GitHub **User** (not an organization),
which is why the old path resolves rather than 404-ing. Era-correct artifacts will name the old form
— `setup.cfg` at commit `0e48fdf` (2018-08-09) declares
`url = https://github.com/scivision/scanning-doppler-interferometer` — and finding it in an old
record is not evidence of a competing current URL.

The repository is not a fork (`fork: false`), so this is the origin of the code, not a mirror. It has
one fork and no stars.

### 4. Software Functionality (RECOMMENDED)
**Values:**
- Data Processing and Analysis
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: Line Plots

Written in the canonical `Parent: Child` form. Each child's parent is listed alongside it, as the
taxonomy requires. `Processing` is one of the thirteen child names that recur under more than one
parent, so the entry above is specifically the **Data Processing and Analysis** child, not the
same-named **Mission-related** one.

**What the software actually is, stated once, because every entry below turns on it.** The installed
Python package is three files and fewer than a hundred lines. `scanning_doppler_interferometer/base.py`
holds two readers and a line-index helper; `scanning_doppler_interferometer/plots.py` holds a single
plotting function of seven statements, six of them `ax.*` calls; `scanning_doppler_interferometer/__init__.py` is one line,
`from .base import txt2dat`. `PlotWinds.py` at the repository root is the command-line driver. That
is the entire surface area, and it is a narrow one: read one section of one file format, and draw one
kind of plot from it.

**Evidence for each value.**

- **Data Processing and Analysis.** The package's primary public function, `txt2dat`, parses a
  structured scientific data file into an in-memory table. That is data processing in the plainest
  sense, and it is the reason the package exists.
- **Data Processing and Analysis: Processing.** `txt2dat` is a transformation chain, not a plain
  file read. It locates a named section within a multi-section file by scanning for two literal
  marker strings held in the module constant `W4`, computes the row offsets from those line indices,
  hands `pandas.read_csv` a whitespace-delimited slice with eight explicitly supplied column names
  (`"Begin Time", "End Time", "Zonal Wind", "Sigma Zon", "Merid Wind", "Sigma Mer", "Vertical Wind",
  "Sigma Vz"`), then converts the two time columns from strings to native objects with
  `[parse(t).time() for t in dat["Begin Time"]]`. Executed against the bundled sample at the pin this
  returns a 226-row by 8-column DataFrame with exactly those column names — the transformation is
  real and it works.
- **Data Processing and Analysis: Time Series Analysis.** The parsed product is a time series and
  nothing else: 226 consecutive wind measurements over one night, each carrying a begin and an end
  timestamp, and the package's only two operations on the data are to put those timestamps into a
  temporal type and to draw the wind components against them.
  **This is the weakest of the five, and the argument against it is recorded so its limitations are
  not overlooked.** The package performs no *analysis* of the time
  dimension: no filtering, no detrending, no autocorrelation, no resampling, no gap handling. Nor is
  the returned frame time-indexed — `Begin Time` is an ordinary column of `datetime.time` objects
  over a default integer index, not a `DatetimeIndex`. On a strict reading of the subcategory —
  "temporal filtering, trend analysis, autocorrelation" — it would not qualify. It is kept on the
  looser reading the vocabulary also supports, "analysis of time-ordered data": the software's entire
  subject matter is a time-ordered geophysical series, and a visitor filtering HSSI for time-series
  tooling who found a wind time-series reader would not think it misfiled. That is the judgement, and
  it is a judgement rather than a deduction.
- **Data Visualization.** `scanning_doppler_interferometer/plots.py` is a dedicated plotting module
  inside the package, and `matplotlib` is a declared extra (the `plots` extra, whose sole entry is
  `matplotlib`).
- **Data Visualization: Line Plots.** `plotwinds` builds exactly one figure, and it is a line plot:
  `ax.plot(dat["Begin Time"], dat.iloc[:, 2:])` draws all six wind and uncertainty columns against
  time, with `ax.set_ylabel("Wind Speed [m/s]")`, a legend built from the column names, and a grid.
  The README embeds a rendering of precisely that figure (see Field 33, where the image is examined
  in detail).

**Considered and rejected, with reasons — recorded so these are not re-proposed.**

- **Data Processing and Analysis: Data Access and Retrieval — rejected, and this is the closest
  call, because two sources actively invite it.** The README's opening line is
  `Get, Parse, Plot: Scanning Doppler Interferomter data from PI Mark Conde's instruments.` [sic —
  see Field 8 on the source typo], and the PyHC registry describes the package as
  `Dowload & plot Scanning Doppler Interferometer data` [sic]. The original 2018 `setup.py` was
  blunter still: `description="easily download and plot Mark Conde's Scanning Doppler Interferometer
  data"`. **None of that is true of the tree at the pin.** There is no network code anywhere: no
  `requests`, no `urllib`, no `http`, no `socket`, no download helper, no URL constant. The complete
  URL inventory of all twenty files (Technical Reference, below) contains exactly one archive URL,
  and it sits in an IDL comment in the `archive/` directory, not in any Python module. The "Get" in the README is a
  survival from an intention that was never implemented in this repository — the software's only
  input is a local path handed to it on the command line. A visitor filtering for data-retrieval
  tooling would find a package that cannot fetch a single byte.
- **Data Processing and Analysis: File Format Conversion — rejected.** The package reads two formats
  and writes none (see Field 19). Conversion requires an output.
- **Data Processing and Analysis: Analysis — rejected.** The package derives no physical quantity.
  Every number it exposes is a column copied out of the input file; nothing is computed from the
  measurements. Contrast the archived IDL routine, which computes nothing either but does at least
  reconstruct absolute times by adding 24 h across the UT midnight wrap
  (`if timeseries[i,0] lt max_0 then timeseries[i,0] += 24`) — the Python package does not even do
  that.
- **Data Processing and Analysis: Data Reduction — rejected.** Selecting one section out of sixteen
  is a parsing scope decision made by a hard-coded constant, not a volume-reducing operation applied
  to data (no averaging, binning or downsampling exists in the tree).
- **Data Visualization: 2D Graphics — rejected.** The one figure is a line plot. There is no
  `pcolormesh`, `imshow`, contour or map anywhere, despite the input file containing eleven
  two-dimensional `*_SKYMAP` sections that would make excellent 2D graphics. That the data supports
  a capability the software does not implement is exactly the trap this rejection guards.
- **Data Visualization: Spectrogram and Data Processing and Analysis: Spectrogram — rejected.** No
  FFT, no time-frequency transform, nothing spectral. The word "Spectral" appears in the sample
  file's `SNR_SKYMAP` and `CHI_SQUARED_SKYMAP` section headers, describing the instrument's
  Fabry-Perot spectral fits — that is a property of the upstream data product, not of this software.
- **Data Processing and Analysis: Calibration — rejected.** The file the package reads is already a
  derived Level-2-style wind product in m/s; no raw counts, no response function, no gain enter here.
- **Coordinate Transforms (whole branch) — rejected.** The section the package reads is the
  geographically-aligned one (`LOCAL_GEO_WINDS`), and the file separately contains the
  geomagnetically-aligned equivalent (`LOCAL_MAG_WINDS`). Both alignments are computed **upstream by
  the instrument's own processing** and shipped as separate sections; the package picks one and does
  no transformation of any kind. A future reader who notices "GEOGRAPHICALLY" and
  "GEOMAGNETICALLY" in the section headers and reaches for `Coordinate Transforms: Ionospheric`
  should stop here: the software chooses between two pre-computed products, it does not convert
  between frames.
- **Models and Simulations (whole branch) — rejected.** Nothing is modelled or simulated; the
  package reads measurements.
- **Mission-related (whole branch) — rejected.** The package is not part of any ground system,
  pipeline or operations chain. It is a user-side reader for a data product that is already
  published. The distinction the taxonomy draws is exactly this one: reading an observatory's data is
  Data Processing and Analysis, being part of that observatory's ground system is Mission-related.
- **Servers and Environments (whole branch) — rejected.** No container, no server, no parallelism,
  no deployment tooling; the tree has no Dockerfile and, at the pin, no CI configuration at all.
- The remaining subcategories under the two selected parents have no counterpart in this package.
  They include 2D Slices, 3D Particle Distribution Processing, Curlometer, Data Assimilation, Energy
  Spectra, Field-line Tracing, Image Processing, Linear Gradient Estimation, Magnetic Null Finding,
  ML/AI, Packet Decommutation, Pitch Angle Distributions, Plasma Moments, Wave Polarization Analysis
  and Wavelet Analysis under Data Processing and Analysis; and 2D Slices, 3D Graphics, Hodograms,
  Mission-Specific, ML/AI, Movies, Orbit Plots, Spacecraft Formation Plots and Web-Based under Data
  Visualization.

**One asymmetry inside the repository is worth recording, because it bears on how narrow this
classification is.** The bundled sample file has sixteen sections (enumerated in the Technical
Reference below). The archived
IDL routine in `archive/` parses the header, the field of view, all eleven `*_SKYMAP` sections
generically, and four named data sections by case — `ALLSKY_TMP_INT`, `LOCAL_GEO_WINDS`,
`LOCAL_MAG_WINDS` and `WIND_GRADIENTS`, the last of which does not even occur in the bundled sample.
**The Python package parses exactly one of them**: section 04, `LOCAL_GEO_WINDS`, selected by the
literal marker strings in the `W4` constant. So the installed software is a narrow reader of one
section, not a reader of the SDI ASCII format, and Field 4 is classified on the former. This
asymmetry also matters to Field 13, where the two readers' relationship is the substance of the
language-scope rationale.

### 5. Related Region (RECOMMENDED)
**Values:**
- Earth Atmosphere
- Earth Thermosphere
- Earth Ionosphere
- Earth Auroral Subregion

**The four regions are recorded together as the settled coverage.** Before this refresh, the HSSI
record carried `Earth Atmosphere` and nothing else. `Earth Thermosphere`, `Earth Ionosphere` and
`Earth Auroral Subregion` are recorded alongside it because the repository, sample data and instrument
literature tie this software specifically to all three regions. The broader row remains valid and
does not stand in for the more specific rows in a flat vocabulary.

**Why the specific regions belong: this entry was under-populated relative to every comparable sibling.** The
four closest entries in the catalogue — Digital Meridian Spectrometer, DASCutils, ReesAurora and
GeoDataPython, all ground-based auroral-zone optical or radar software, three of them by this same
author — each carry the same four regions: `Earth Atmosphere`, `Earth Auroral Subregion`,
`Earth Ionosphere` and `Earth Thermosphere`. Before this refresh this entry carried only the first.
That contrast is not by itself an argument (a coincidence of neighbours is not evidence about this
software), but it identifies the discovery gap, and the per-row evidence below is specific to this
software.

**The case for adding `Earth Thermosphere` — the strongest of the three.** A Scanning Doppler
Interferometer measures **thermospheric neutral winds and temperatures** by Doppler-shifting airglow
and auroral emission lines; that is what the instrument is for. The evidence is in the repository and
in the instrument literature together. The bundled sample's header gives
`Wavelength in nm: 557.7` — the OI green line, emitted in the lower thermosphere — and the file's
section 03 is `ALLSKY_TMP_INT`, "All-sky average temperature in K", i.e. neutral temperature. The
instrument's own operational archive offers three wavelengths, 5577 / 5890 / 6300, the last being the
OI red line from the F-region thermosphere near 240 km. The instrument team's own paper on this exact
site is titled *Spatial structure in the thermospheric horizontal wind above Poker Flat, Alaska,
during solar minimum* (Conde & Smith 1998, JGR 103(A5) 9449-9471, `10.1029/97JA03331`), and the
earlier one is *Mapping thermospheric winds in the auroral zone* (Conde & Smith 1995, GRL,
`10.1029/95GL02437`). The quantity this software loads and plots is, by the instrument's own
literature, a thermospheric wind.

**The case for adding `Earth Ionosphere`.** `ionosphere` is one of the repository's own two GitHub
topics, declared by the author on the repository itself (see Field 16, where this is established and
its provenance corrected). It is also the concept behind the PyHC registry's keyword for this
package, `ionosphere_thermosphere_mesosphere`. The physical justification is the standard one for
auroral-zone optical wind measurement: the emissions are excited by ionospheric processes and the
neutral wind is coupled to ion drift, which is why the ITM community treats them as one domain.

**The case for adding `Earth Auroral Subregion`.** The bundled sample is 557.7 nm data from Poker
Flat at 65.1192°N — inside the auroral oval — and the file's field-of-view section explicitly carries
`Auroral Oval Angle:  23.1` and `Rotation from Oval:   0.0`, i.e. the instrument's viewing geometry
is defined relative to the auroral oval. The instrument paper title quoted above is literally
"in the auroral zone".

**An alternative considered was retaining only `Earth Atmosphere`.** Two arguments support that
narrower treatment, and neither is negligible. First,
this software is not a model or an analysis tool with a physical domain of its own — it is a file
reader. One could hold that the *data's* region is not the *software's* region, and that
`Earth Atmosphere` is the honest breadth for a package that would parse the same file just as
happily if it contained troposphere data. Second, and more practically, none of the three specific
regions is stated anywhere in the software's own text: the README names no region, `setup.cfg`'s
classifier is the broad `Topic :: Scientific/Engineering :: Atmospheric Science`, and the only
region-bearing evidence is in the sample data file, the instrument literature, and the author's
GitHub topics. The three specific regions therefore remain an inference from the supported
instrument and its data, applied to the software. That inference is nevertheless selected because
the package is purpose-built for those measurements, and the three rows materially improve accurate
region-based discovery.

**Two constraints govern the settled selection.**

- **"Earth Atmosphere already encompasses the thermosphere" is a reasoning defect here, not an
  argument.** The Region vocabulary is **flat** — all 24 rows are top-level, none is a parent or
  child of any other — so selecting the coarse row does not make the entry findable under the fine
  ones. A visitor filtering for `Earth Thermosphere` did not see this entry before this refresh.
- **Dropping `Earth Atmosphere` in favour of specific rows would be a mistake.** The catalogue's
  established precedent is to keep the coarse value alongside the specific ones: it is not wrong, and
  removing it would narrow discovery while buying no correctness. The specific rows therefore sit
  alongside `Earth Atmosphere` rather than replacing it.

**Considered and rejected:**
`Earth Lower and Middle Atmosphere` — the 557.7 nm layer sits at and above the mesopause and the
630.0 nm layer far above it; nothing this instrument measures is lower- or middle-atmospheric. The
remaining nineteen rows are magnetospheric, solar, heliospheric or planetary and have no bearing on
ground-based Alaskan thermospheric wind data.

**A note on ordering.** Related Region is a sorted relation and the stored order is the displayed
order. Placing the specific rows after `Earth Atmosphere` preserves the broad-to-specific reading
and keeps the established row first.

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

**Sole author, and the repository confirms it exhaustively.** All nineteen commits are by one person
(`Michael Hirsch` / `Michael Hirsch, Ph.D` / `scivision` — three spellings of one committer identity
across the history, the last being the GitHub username). `setup.cfg` gives
`author = Michael Hirsch, Ph.D.`, and `LICENSE.txt` reads
`Copyright (c) 2014-2020 Michael Hirsch, Ph.D.`. The academic-degree suffix is correctly normalised
away in the recorded name; it is a credential, not part of a family name. There is no `AUTHORS` file,
no `CONTRIBUTORS` file, and no `CITATION.cff`.

**The ORCID and both affiliations are correct and must not be lost.** This matters concretely: a
legacy 2025 extraction of this repository recorded the author with **no ORCID and no affiliation at
all**, having derived the name from `setup.cfg` alone. Reconciling toward that file rather than
toward the stored record would strip an identifier and two organizations from a correct entry. The
stored values are the better ones and are retained.

**The ORCID is independently corroborated.** ORCID's public record for `0000-0002-1637-6526` gives
given name "Michael", family name "Hirsch", and a single employment: Boston University, department
"ECE", role "Research Scientist". That employment is also the source of the Boston University
affiliation. The ROR `https://ror.org/05qwgg493` resolves to an organization whose `ror_display`
name is exactly **Boston University** (Boston, USA; acronym BU) — not Boston University Academy, not
the University of Massachusetts Boston, which are separate ROR records.

**Negative research — Scivision, Inc. has no ROR, and there is a false match to avoid.** A ROR search
for "SciVision" returns exactly one organization: `https://ror.org/011qev639`, **SciVision Biotech
Inc. (Taiwan)**, a Taiwanese biotechnology company with no connection to this author or this
software. Attaching it would be a factual error. The empty affiliation identifier is correct and
should stay empty until a genuine ROR for this organization exists.

A capitalisation difference exists between the stored `Scivision, Inc.` and the author's own
rendering `SciVision`. Organization rows are shared across the catalogue — the same row backs this
author's affiliation on several other entries — so this is not resolvable from one software entry and
is deliberately left alone rather than changed here. A future agent that wants to normalise it must
first establish what else references the row.

**Mark Conde is not an author of this software, and the temptation to add him should be resisted.**
He is named prominently in the README, in the GitHub repository description, in the PyHC registry
entry and in this dossier — as the **principal investigator of the instrument** whose data the
software reads. He wrote none of this code and appears nowhere in the commit history, the packaging
metadata or the licence. Instrument authorship is not software authorship. The place his contribution
is properly recorded is Field 27, where the instrument papers are recorded as related publications.

### 7. Software Name (MANDATORY)
**Name:** Scanning Doppler Interferometer

Three sources agree on this exact string: the README's title heading
(`# Scanning Doppler Interferometer`), the PyHC registry entry
(`- name: Scanning Doppler Interferometer` in `_data/projects_unevaluated.yml`), and the repository's
own slug and Python distribution name in their hyphenated and underscored forms
(`scanning-doppler-interferometer`, `scanning_doppler_interferometer`). The spelled-out title-case
form is preferred over either machine form as a human-facing catalogue name.

**The instrument this software serves is not, in fact, called an interferometer by the people who
operate it — and the software name stays anyway.** This divergence is real, it is durable, and it
will confuse a future agent who does not find it recorded here.

- The instrument's own operational site at the University of Alaska Fairbanks,
  `http://sdi_server.gi.alaska.edu/sdi_web_plots/sdi_arc.asp`, is titled
  `SDI Plot Archive: Monthly Browser` and headed **"Scanning Doppler *Imager* - Monthly Data
  Browser"**. This is the site the repository's archived IDL reader points at, and the site the
  bundled sample data came from.
- The literature agrees with the site, not with the software. An ADS title search for
  `"scanning Doppler interferometer"` returns **0** records; `"scanning Doppler imager"` returns
  **8**, and a full-text search for the phrase "Scanning Doppler Imager" returns 171. The published
  name of Mark Conde's instrument class is *Scanning Doppler Imager*.

Field 7 asks for the name of the **software** as listed on the code repository, and that name is
`Scanning Doppler Interferometer` in every artifact the author controls. It is also the name under
which the package is registered with PyHC. Renaming the software to match the instrument would
contradict its repository, its distribution name, its import name and its registry entry, and would
be a fabrication of a name nobody uses for this code. The divergence is recorded rather than
resolved — and a future agent that encounters the "Imager" spelling in the literature should
recognise it as the instrument's name, not as a correction to this field.

### 8. Description (MANDATORY)
**Description:** Load, parse, and plot Scanning Doppler Interferometer data from PI Mark Conde's
instruments. This software package loads and plots scanning Doppler interferometer data, particularly
focused on atmospheric wind measurements. The package supports reading both ASCII text files and IDL
.sav files containing wind data (zonal, meridional, and vertical components with associated
uncertainties) from Scanning Doppler Interferometer observations. The data is aligned geographically
at the station location and includes time series measurements of wind speeds in meters per second.

Each factual claim in this text is corroborated at the pinned tree:

| Claim | Source at the pin |
|---|---|
| "Load, parse, and plot ... from PI Mark Conde's instruments" | README line 4, which reads `Get, Parse, Plot: Scanning Doppler Interferomter data from PI Mark Conde's instruments.` [sic], and the GitHub repository `description`, which carries that same sentence with `Interferometer` spelled correctly. The two sources differ by exactly that typo and are **not** interchangeable — see the quotation warning below |
| "particularly focused on atmospheric wind measurements" | `PlotWinds.py` docstring, `Get/Parse Mark Conde's Scanning Doppler Interferometer data, particularly for Winds.`; `setup.cfg` keyword `winds`; the parsed columns are wind components |
| "reading both ASCII text files and IDL .sav files" | `base.py` defines `txt2dat` (ASCII) and `plotsav` (`from scipy.io import readsav`); `PlotWinds.py` branches on `if fn.suffix == ".sav":` — with the caveat in Field 18 |
| "zonal, meridional, and vertical components with associated uncertainties" | the six data column names supplied by `txt2dat`: `Zonal Wind`, `Sigma Zon`, `Merid Wind`, `Sigma Mer`, `Vertical Wind`, `Sigma Vz` |
| "aligned geographically at the station location" | the section marker the parser matches, verbatim: `>>>>>> Begin Section 04: [LOCAL_GEO_WINDS] -- Winds in m/s at the station location, aligned GEOGRAPHICALLY` |
| "time series measurements of wind speeds in meters per second" | same marker ("Winds in m/s"); `plots.py` sets `ax.set_ylabel("Wind Speed [m/s]")`; 226 time-stamped records in the bundled sample |

**Quotation hazard — the README contains a typo, and it must be reproduced, not corrected.** README
line 4 reads, byte for byte:

`Get, Parse, Plot: Scanning Doppler Interferomter data from PI Mark Conde's instruments.`

**"Interferomter" is misspelled in the source** (the `e` before `ter` is missing). The GitHub API's
repository `description` field carries the *same sentence with the word spelled correctly*. So the
two sources are not interchangeable: any quotation must be bound to the right parent. Quoting the
corrected spelling and attributing it to the README is wrong; silently correcting the README's
spelling in a quotation is also wrong. Mark it `[sic]` and move on. The same discipline applies to
the PyHC registry, which independently misspells "Download" as `Dowload` (Field 8's registry section
and Field 4 both quote it, marked).

**The description is retained as stored and was not reworded.** It is accurate on every clause, it
reads well, and rewording a description without cause is not an improvement. Two additions were
considered and declined:

- **A caveat that the `.sav` path does not run.** Field 18 establishes that `PlotWinds.py`'s IDL
  `.sav` branch raises `AttributeError` at the pin. A description is a statement of what the software
  is for, not a defect report, and the format support is genuinely implemented in `base.py`; the
  caveat belongs in Field 18, where it is recorded in full, and not in prose a catalogue visitor
  reads as a summary.
- **A note that the software reads only one of the file's sixteen sections.** True and interesting
  (Field 4), but it is a precision the description does not currently claim and does not need. The
  description says the package reads wind data aligned geographically at the station location, which
  is exactly the one section it reads. It is already correct at that grain.

### 9. Concise Description (OPTIONAL)
**Concise Description:** Load and plot scanning Doppler interferometer data from PI Mark Conde's
instruments, with focus on atmospheric wind measurements.

129 characters, below the 150-200 target but comfortably within the 200-character maximum. It is a
faithful compression of Field 8 keeping the three facts a preview most needs: what the software does,
whose instrument's data, and what quantity. Retained as written; no wording change is warranted, and
padding it to reach 150 characters would add words without adding information.

### 10. Publication Date (RECOMMENDED)
**Date:** 2018-03-16

The date the code first became public, and two independent sources agree. The repository's initial
commit `75cbd526ca67e679d92ad81ed4d168dd10daba2c` is dated 2018-03-16, and GitHub's repository
`created_at` is `2018-03-16T16:20:36Z`. Their agreement matters: a repository created empty and
pushed later would show a gap between the two, and this one does not — in fact **eight of the
nineteen commits land on that single day**, from `Initial commit` through `init`,
`init (not fully working yet)`, `initial working`, `python package, self test`, `prereq`,
`make plots own file` and `doc [ci skip]`. The project went from nothing to a working, self-tested,
packaged tool in one sitting.

**No alternative candidate exists.** There is no PyPI first-release date (Field 2: no distribution),
no Zenodo deposit date, and no tag. This field has exactly one defensible value.

### 11. Publisher (RECOMMENDED)

#### Publisher:
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Correct per the field's own rule: where no DOI has been obtained, the publisher is the repository
host. Field 2 establishes that no DOI exists by three independent routes, so the Zenodo branch of
that rule does not apply and cannot be made to apply.

The identifier is the GitHub URL rather than a ROR, which the field permits where no ROR applies and
which is the form the field's own guidance gives for a repository host. The Organization row is
shared across the catalogue and is not this entry's to rename.

### 12. Version (RECOMMENDED)

#### Version Information:
- **Version Number:** 0.7.0
- **Version Date:** 2018-08-09
- **Version Description:** Version 0.7.0 is the package metadata version introduced in setup.cfg; no release notes or git tag were found.
- **Version PID:** Not found

**This is the "declared, never released" shape, and every clause of the stored description holds.**
There is no git tag in this repository (`git tag` returns nothing; the GitHub tags API returns an
empty array), no GitHub release (the releases API likewise returns an empty array), and no PyPI
distribution (Field 2). The only version identity the software has ever had is a string in its
packaging metadata.

**Version provenance, traced through the history.** The first packaging metadata was
`setup.py` at commit `f127c7bdc978a8bbd1dbfa009f73c60617910a91` (2018-03-16), which declared
`version='0.5.0'` inside a `setup(name='ScanningDopplerInterferometer', ...)` call. On 2018-08-09
commit `0e48fdf5934dab4d39b0a079379b2983e09b9500` migrated the project from an imperative `setup.py`
to a declarative `setup.cfg` — `setup.py` was reduced to `from setuptools import setup` /
`setup()`, which apart from a `#!/usr/bin/env python` shebang is still its entire content at the pin
— and the new `setup.cfg` declared
`version = 0.7.0`. That line has never changed since: it is byte-identical at `0e48fdf` and at the
pinned final revision, across four years and the ten commits that follow it.

**`0.6.0` never existed in this repository.** The version went 0.5.0 → 0.7.0 in one step at the
`setup.py`→`setup.cfg` migration. A future agent reconstructing a release series should not
interpolate it, and should not read the jump as evidence of a missing release: there was no release
at either number.

**The version date is the date the string was introduced, and that is the only date available.**
2018-08-09 is when `version = 0.7.0` first appears in the tree. It is not a release date, because
there was no release. Recording the commit date is the honest available answer; inventing a release
date, or promoting the final commit date (2022-08-11) into this field, would both be worse.

**The version PID is empty and will stay empty.** It follows directly from Field 2 — no Zenodo
deposit exists, so there is no version DOI for anything, let alone for an unreleased version string.

**One alternative was considered and rejected: recording the pin itself as the version.** The
archived final tree is four years and ten commits later than the tree that first declared 0.7.0,
so "0.7.0" arguably describes 2018 rather than the software as archived. But the author never bumped
the number, and a curator inventing a version identity the project never claimed would be
fabrication. `0.7.0` is what the software says it is, and the stored description already tells the
reader exactly how much weight to put on it.

### 13. Programming Language (RECOMMENDED)
**Languages:**
- Python 3.x

**Only the installable package's language is recorded.** `Python 3.x` stands alone under Criterion B
below. `IDL` is excluded because `archive/sdi_ascii_reader.pro` is third-party code archived for
reference rather than part of the installed, tested package. This selection makes the language
scope explicit; the alternative tree-inventory criterion remains documented because it
would reach the opposite answer on genuine evidence.

**`Python 3.x` is beyond dispute.** The installed package is entirely Python;
`setup.cfg` declares `python_requires = >= 3.6` and the classifiers
`Programming Language :: Python :: 3.6` through `3.9`; both CI configurations the project ever had
declared Python and nothing else — `.travis.yml` with `language: python`, `.appveyor.yml` with
`stack: python 3` (see Field 20 for the full CI history, which is not visible at the pin).

**The facts about the IDL file, stated before either argument.**

- `archive/sdi_ascii_reader.pro` is 384 lines of IDL, and it says so itself: line 2 is the comment
  `; does not run in GDL, requires IDL (sigh)`. It is unambiguously IDL and unambiguously present in
  the tree at the pin.
- **It is verbatim third-party code from the instrument team, and this is now proved rather than
  inferred.** Line 1 of the file is the comment
  `; http://sdi_server.gi.alaska.edu/sdi_web_plots/sdi_arc.asp`. That page — live, HTTP 200, DNS
  resolving to 199.165.82.138 — carries the sentence "Here is a simple IDL routine that should allow
  you to easily read ASCII data files downloaded from the table above, using the IDL programming
  language", hyperlinked to
  `http://sdi_server.gi.alaska.edu/sdi_web_plots/sdi_ascii_reader.pro`, and demonstrates its use as
  `result = sdi_ascii_reader(dialog_pickfile())`. **The filename and the top-level function name
  both match the repository's file exactly.** Fetching that upstream file and diffing it against the
  repository's copy gives six small differences: the repository copy **adds** the two header comment
  lines quoted above (the author's own annotation) and **lacks** four later upstream edits — a
  records-count adjustment, a commented-out `stop`, two debug comments plus a blank-line guard, and a
  trailing whitespace line. The body is upstream's, and upstream has continued to evolve since the
  2018 snapshot was taken. This is a vendored copy of the University of Alaska SDI group's own
  reader, not code written for this project.
- **Its place in the project's chronology, which bears on both criteria and was missed on a first
  reading of the tree at the pin.** The repository was created at `75cbd52`, 2018-03-16 12:20:37
  -0400. The very next commit, `77bf631` (12:24:27, subject `init`), added this IDL file **at the
  repository root** — it is the first substantive content the project ever held, and it preceded the
  arrival of the Python package at `f127c7b` (13:18:11, subject `python package, self test`) by
  something under an hour. Five months later, at `0e48fdf`
  (2018-08-09), the author moved it to `archive/` as a pure rename, byte-identical (`git` records
  `R100`), in the same commit that migrated packaging to `setup.cfg`. The file has not been edited
  since 2018-03-16. So the repository began as a holder for the instrument team's IDL reader and was
  then built out in Python around it, after which the author deliberately demoted the IDL file to an
  `archive/` directory and left it untouched for four more years.
- **That chronology is genuinely two-edged and neither side should claim it whole.** For Criterion A:
  the IDL reader is not incidental clutter that drifted in: it is the thing the repository was opened
  to hold, and it still works. For Criterion B: the demotion to `archive/` was an affirmative act by
  the author, taken five months in and never reversed across four subsequent years and ten commits —
  the strongest available evidence of how the author himself classified this file's relationship to
  the package.
- `.gitattributes` marks `archive/* linguist-vendored`, and GitHub's derived language breakdown for
  the repository is consequently `{"Python": 2975}` — IDL does not appear at all. Note that this is
  a *consequence* of the `.gitattributes` line, not independent corroboration of it.
- **The `.gitattributes` file is partly boilerplate, and that cuts against reading it as a
  considered attestation.** The same three-line block also marks `docs/*` and `paper/*`, **neither of
  which has ever existed in this repository**. A template that declares attributes for directories
  the project does not have is a template, and a directory glob is not a per-file statement about
  provenance. (The upstream diff above supplies the per-file statement that `.gitattributes` does
  not.)

**Criterion A — "catalogue every language present in the tree."** This alternative was considered
and not selected. Under this reading the field inventories what a user who clones the repository
will find. It would **include IDL**: an IDL file is
present, it is functional, it is substantially larger than the Python package, and it is the only
thing in the tree that can read the whole SDI ASCII format rather than one section of it. There is a
searcher-side version of this argument too: HSSI already records `IDL.sav` in Field 18, so a visitor
filtering on IDL-related metadata has a reason to expect this entry, and the `.pro` file is the one
artifact here that an IDL user could actually run.

**Criterion B — "catalogue only the language of the installable package."** This is the selected
criterion. The field describes the software the entry is *about* — what `pip install` gives you and
what the software's own tests exercise. It **excludes IDL**: the `.pro` file is third-party code the
author archived for reference; it is not imported, called, tested or packaged; `packages = find:`
cannot reach it (it has no `__init__.py`); `.flake8` explicitly excludes `archive/`; the author
marked it vendored; and Field 13's own guidance asks for the languages **most important** for the
software and states that it is not meant to be exhaustive. On this reading, listing IDL would tell a
visitor filtering for IDL software that they had found IDL software, and they would find a Python
package with someone else's routine in an `archive/` folder.

**What each criterion implies for the *other* possible answer, stated explicitly so the trade is
visible.** Under Criterion A, *excluding* IDL hides a real, working, 384-line IDL asset from anyone
searching for it — the tree's largest single piece of code by far. Under Criterion B, *including*
IDL misrepresents the package: it promises a bilingual tool and delivers a Python reader plus a
vendored reference file, and it does so on the strength of code the author did not write.

**One boundary follows from the selected criterion.** It does **not** travel to Field 18 or Field 19.
That `IDL.sav` already sits in Field 18 is context for the
searcher-side argument under Criterion A and nothing more; `IDL.sav` is there because
`base.plotsav` calls `scipy.io.readsav` from Python, which is a statement about a supported input
format and not about a programming language. Excluding IDL from Field 13 is no reason whatsoever to
remove `IDL.sav` from Field 18.

**No other language row applies.** There is no C, no Fortran, no MATLAB (no `.m`
file exists in this repository, unlike some sibling packages by the same author), no compiled
extension and no build step beyond `setuptools`.

### 14. Reference Publication (OPTIONAL)
**Reference Publication:** Not found

**No publication describes this software, and the negative research is dated 2026-09-03 with
controls in both directions.**

- A full-text ADS/SciX search for the repository slug in three spellings —
  `full:"space-physics/scanning-doppler-interferometer"`,
  `full:"github.com/space-physics/scanning-doppler-interferometer"` and
  `full:"scivision/scanning-doppler-interferometer"` — returns **0** records each.
- **The index does cover software names of this kind**, so the zero is a real absence and not a gap
  in coverage: the same full-text query form returns **254** records for `msise00` and **337** for
  `pysat`. A nonsense token returns 0, so the query form is not silently failing.
- The repository itself cites nothing (Field 2, route 1): zero matches for `doi`, `zenodo`,
  `citation`, `cite`, `bibtex`, `arxiv` or a DOI prefix pattern across all twenty tracked files.

**A tokenization trap, recorded so a future agent does not mistake it for a hit.** The queries
`full:"scanning-doppler-interferometer"` and `full:"scanning_doppler_interferometer"` each return
**10** records — but ADS splits on the hyphen and underscore and matches the ordinary English phrase
"scanning doppler interferometer" in running prose. Inspecting all ten confirms it: they include
AGU meeting abstracts on thermospheric winds, the Horizontal Wind Model update
(`10.1002/2014EA000089`), and — decisively — a 2007 *Applied Physics Letters* paper,
*Elastometric sensing using higher flexural eigenmodes of microcantilevers*
(`10.1063/1.2803215`), which has nothing to do with heliophysics at all. **None of the ten cites
this software.** Search on the slug with its punctuation intact, as above, and the count is zero.

**The instrument papers do not belong in this field.** Field 14 is specified as "the DOI for the
publication describing **the software**". Conde & Smith's papers describe the *instrument* whose data
this software reads; the earliest predates this code by twenty-three years and none of them could
describe it. They are recorded at length in Field 27 as related publications, the only field in
which their instrument-level relationship belongs. There is no JOSS paper, no software
paper, and no article that names this package.

### 15. License (RECOMMENDED)
**License:** BSD 2-Clause "Simplified" License

This is the exact spelling of the row in the controlled `License` vocabulary; the list is closed, and
a name that is not one of its eleven rows is rejected outright.

**No License URI is recorded, and the legacy value that used to sit there was wrong twice over.** A
2025 extraction of this repository recorded
`**License URI:** https://opensource.org/licenses/BSD-2-Clause`. Field 15 displays a License URI
sub-field on the submission form, but the licence is a reference to a **shared licence record** that
carries its own URL — the vocabulary row for BSD-2-Clause already carries
`https://spdx.org/licenses/BSD-2-Clause.html` — so there is no per-software licence URI in storage to
write, and a value differing from the shared row's URL would be doubly unwritable. The
`opensource.org` form was additionally not the URL the row carries. It is removed and should not
return.

**Positive evidence at the pin.** `LICENSE.txt` contains the BSD 2-Clause text, opening
`Copyright (c) 2014-2020 Michael Hirsch, Ph.D.` and carrying the two numbered redistribution
conditions and the standard disclaimer with no third "endorsement" clause — which is precisely what
distinguishes 2-Clause from 3-Clause. `setup.cfg` declares `license_files =` with `LICENSE.txt`.
GitHub's repository-level licence detection independently reports `spdx_id: BSD-2-Clause`. Because
the repository is archived, this is not merely the current licence — it is the final one.

**Licence history — a durable finding, and the specific wrong edit it prevents.** This repository was
**AGPL-3.0 for the first two years and two months of its life**, and third-party or historical
records may reflect that.

| Commit | Date | Licence file and content |
|---|---|---|
| `75cbd526ca67e679d92ad81ed4d168dd10daba2c` | 2018-03-16 (initial commit) | `LICENSE`, opening `GNU AFFERO GENERAL PUBLIC LICENSE` / `Version 3, 19 November 2007` |
| — | through 2019-11-22 | unchanged |
| `fdddb4b4347b9a81a8e610ca5ac29161b6ebdbb8` | 2020-05-12 | **the relicensing commit**: deletes `LICENSE` and adds `LICENSE.txt` containing BSD 2-Clause. Commit subject: `project template` |

The relicensing is a *single* commit, and it is `fdddb4b`. The commit three minutes later,
`5d3186b929216457a1d1ea96cb836a41f321b6e9` (subject `prereq`), touches only `.travis.yml` and has
nothing to do with the licence — the two are easily conflated because they share a date and sit
adjacent in the log. Note also that the change was a **delete-and-add of differently named files**,
not an edit: the AGPL text never appears in `LICENSE.txt` and the BSD text never appears in
`LICENSE`.

The `2014-2020` copyright range in the current file partly explains itself: 2020 is the relicensing
year, and the range is the author's own project-template boilerplate rather than a claim that this
specific repository existed in 2014 (it was created in 2018).

**Ruled out by name: `GNU General Public License v3.0 or later`.** This is the wrong edit a future
refresh is most likely to make. An agent finds the AGPL history above, looks for an Affero row, finds
that the eleven-row vocabulary contains **no AGPL row of any kind** (its GPL-family rows are GPL v2,
GPL v3.0-or-later, LGPL v3.0-only and LGPL v2), and takes GPL-3.0-or-later as the obvious near-match.
It fails on two independent grounds. **(a)** AGPL-3.0 is not GPL-3.0 — the Affero network-use clause
is the entire reason the licence exists separately, so recording GPL-3.0-or-later would be a
substantively wrong statement about the terms, not a rounding. **(b)** More fundamentally, Field 15
records the software's current licence, and the current — and, the repository being archived, final
— state of the tree is BSD-2-Clause. **The AGPL era is history that explains divergent records; it is
not a competing candidate for this field.** The current value is correct and should not be "corrected"
backwards.

**One artifact of the relicensing survives at the pin as harmless drift:** `MANIFEST.in` still reads
`include LICENSE`, naming the file that `fdddb4b` deleted. It is recorded here because it is exactly
the sort of dangling reference that invites a future agent to conclude a `LICENSE` file exists.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Keywords:**
- interferometry
- ionosphere
- winds

Recorded in the lower-case form in which they are stored. The catalogue's view rendering title-cases
them (`Interferometry`, `Ionosphere`, `Winds`); that is presentation, not the value, and all three
exist as lower-case rows in the open `Keyword` vocabulary. **Comparisons in a future refresh must be
made against the stored lower-case strings**, or the field will appear to differ when it does not.

**Provenance, and a standing question this retires.** `winds` and `interferometry` are the two
keywords `setup.cfg` itself declares. `ionosphere` appears in neither `setup.cfg` nor `README.md`,
which is exactly why it has looked in the past like a term propagated in from PyHC's
`ionosphere_thermosphere_mesosphere` tag or supplied by a curator. **It is neither.** The
repository's own GitHub topics are `["interferometry", "ionosphere"]` — author-declared, on the
repository itself. All three stored keywords are the author's own words. That settles the question
permanently and it should not be reopened.

**Considered and not added: `ionosphere_thermosphere_mesosphere`.** The PyHC registry entry for this
package carries `keywords: ["ionosphere_thermosphere_mesosphere","specific"]`, and a row with that
exact underscore-joined name already exists in the vocabulary (as does a space-separated
`ionosphere thermosphere mesosphere` row for the same concept — so a future refresh that wants it
must reuse one of the two existing rows rather than minting a third variant). It was not added, for
a reason that should be weighed rather than assumed: the concept is a genuine science-domain label
and the software genuinely serves that domain, but the three stored keywords are all author-declared,
and adding a registry tag alongside them would mix provenances without improving discovery — the
`ionosphere` row already covers the searcher who types any part of it. This is a close call and a
future refresh may reasonably differ; what it should not do is add it believing it to be an
uncontroversial gap.

**The `specific` tag from the same PyHC entry is deliberately not recorded.** It is a registry
classification of the package's scope, not a science keyword, and would tell a catalogue visitor
nothing.

**Considered and not added, with reasons:** `thermospheric winds` and `poker flat` — neither exists
as a row, so both would mint new vocabulary, and Field 16 asks for keywords *not already supported by
other metadata fields*; the observatory is Field 32's business and the region is Field 5's.
`atmospheric science` — a row does exist and `setup.cfg`'s classifier
`Topic :: Scientific/Engineering :: Atmospheric Science` would support it, but it is a packaging
taxonomy label of very low specificity. `aurora` and `airglow` — rows exist and both are physically
apt for a 557.7 nm SDI, but neither is the author's word. `airglow` occurs nowhere in the repository
at all. The exact token `aurora` likewise occurs nowhere; the string `auroral` does occur twice, as
the sample file's `Auroral Oval Angle:  23.1` header field and the corresponding
`auroral_oval_angle` structure tag in the IDL reader — which is a coordinate-geometry parameter of
the data format, not a subject keyword. That parameter is one strand of Field 5's regional argument,
which also rests on the 557.7 nm emission wavelength, the `ALLSKY_TMP_INT` neutral-temperature
section, the `Latitude:  65.1192` site coordinate, the repository's own `ionosphere` GitHub topic and
the Conde & Smith literature; it is not the whole of it. Recording either keyword here would still be
an inference about the instrument dressed as the author's keyword.

### 17. Data Sources (OPTIONAL)
**Data Sources:**
- Observatory/Mission-specific

The one data source this software reads is the University of Alaska Fairbanks Geophysical Institute's
own SDI archive — a single instrument network's own product, in that network's own ASCII layout. That
is precisely what the `Observatory/Mission-specific` row denotes, and the association is evidenced
three ways at the pin: `archive/sdi_ascii_reader.pro` is headed with the archive's URL,
`http://sdi_server.gi.alaska.edu/sdi_web_plots/sdi_arc.asp`; the bundled sample
`data/PKR_2017_061_date_03_02_sky_5577_nz0115.txt` carries `Site: Poker Flat Research Range` in its
header and follows that archive's filename convention exactly (the live archive today serves files
such as `PKR_2026_244_date_09_01_sky_6300_nz0115.txt`); and the parser in `base.py` matches a section
banner — `>>>>>> Begin Section 04: [LOCAL_GEO_WINDS] ...` — that exists in no format but this one.

**An important qualification: the software does not fetch anything.** The README's headline verb is
"Get", and the GitHub description repeats it, but there is no network code anywhere in the twenty
tracked files. A search across the whole tree for `requests`, `urllib`, `urlopen`, `wget`, `curl`,
`ftp`, `http.client`, `socket` or `download` returns exactly one hit: the line `downloads/` inside
`.gitignore`, which is boilerplate from the standard Python `.gitignore` template. The only file
access in the package is `fn.open("r")` in `base.py`. The user downloads the ASCII file from the
archive by hand, through the web browser interface the archive provides, and points the tool at it.
Field 17 asks what data sources the software can access, and reading a file that came from one
archive is a weaker association than fetching from it — but it is the correct association, and it is
the only one available.

**Considered and rejected, with reasons.** `HTTP/HTTPS Directories` and `FTP/FTPS Directories` — no
retrieval code exists, per the search above; selecting either would assert a downloader the software
does not have. `CDAWeb`, `Madrigal`, `HAPI`, `SSCWeb`, `OMNIWeb`, `AMDA`, `das2`, `VirES`, `WDC`,
`GFZ`, `TAP`, `The Virtual Solar Observatory.` — none is named anywhere in the tree, and SDI data is
not distributed through any of them. `S3/Cloud-aware` — no cloud access of any kind. `Other` — the
correct row already exists, so `Other` would only lose information.

### 18. Input File Formats (RECOMMENDED)
**Input Formats:**
- ascii
- IDL.sav

Both rows are exact matches in the closed `FileFormat` vocabulary and both are implemented in
`base.py`:

- **`ascii`** — `txt2dat()` reads the SDI plain-text product with `pandas.read_csv(..., sep=r"\s+")`
  after locating the section by scanning for the literal banner text. This is the fully working path
  (see below) and the one the README documents.
- **`IDL.sav`** — `plotsav()` calls `from scipy.io import readsav` and `readsav(fn,
  python_dict=True)`; `PlotWinds.py` dispatches to it on `if fn.suffix == ".sav":`. `scipy` is
  declared as the `io` extra in `setup.cfg`, added specifically for this. The support is real code
  with a real dependency, not an aspiration.

**A durable, searcher-relevant defect on the `.sav` path — recorded because it is exactly the route a
visitor who filtered on `IDL.sav` would take.** `PlotWinds.py` calls `sdi.plotsav(fn)`, but the
package's `__init__.py` contains a single line, `from .base import txt2dat`. `plotsav` is therefore
never re-exported. Running the documented CLI on a `.sav` file raises, at `PlotWinds.py` line 24:

`AttributeError: module 'scanning_doppler_interferometer' has no attribute 'plotsav'. Did you mean: 'plots'?`

Two discriminating checks confirm this is a wiring bug and not a missing feature:
`hasattr(sdi, "txt2dat")` is `True` while `hasattr(sdi, "plotsav")` is `False`, and
`scanning_doppler_interferometer.base.plotsav` **does exist and is callable** through the submodule.
The format support is present in the library and unreachable from the entry point. (The interpreter's
"Did you mean: 'plots'?" suggestion appears only because `PlotWinds.py` also imports the `plots`
submodule, binding that name onto the package; a bare `import scanning_doppler_interferometer`
offers no such suggestion.) A second, unrelated wrinkle in the same function: `plotsav` is annotated
`-> pd.DataFrame`, but `readsav(python_dict=True)` returns a `dict`.

**`IDL.sav` stays in this field, and the reason is worth stating plainly** so a future refresh does
not remove it as a "defect cleanup": Field 18 records the formats the software is built to read, the
code to read this one exists and is functional when called directly, and a user searching HSSI for
software that ingests IDL save files should find this entry. The defect is documentation for that
user, not grounds for hiding the capability.

**Considered and rejected:** `CDF`, `netCDF3/4`, `HDF5`, `FITS`, `JSON`, `csv`, `Zarr`,
`ISTP-Compliant` — none appears anywhere in the tree; no reader, no dependency, no mention. `csv`
deserves an explicit word because `pandas.read_csv` is the function used: the file is whitespace-
delimited (`sep=r"\s+"`), inside a sixteen-section instrument text product, and is not a CSV in any
sense a searcher would mean. `Other` — both applicable rows exist by name.

### 19. Output File Formats (RECOMMENDED)
**Output Formats:** Not found

**The software writes no files at all, and this is verified rather than assumed.** A search across
all twenty tracked files for `savefig`, `to_csv`, `to_hdf`, `to_netcdf`, `.write(` and `open(`
returns exactly one match — `fn.open("r")` in `base.py`, a read. There is no write mode anywhere in
the package.

What the tool produces instead is an on-screen figure: `plots.plotwinds()` builds a matplotlib
figure, and `PlotWinds.py` ends with `show()`, opening an interactive window. Whether the user then
saves that figure, and in what format, is matplotlib's business and the user's choice; it is not a
format this software emits. `txt2dat()` returns an in-memory `pandas.DataFrame` — a Python object,
not a file format.

**The vocabulary offers no honest row.** Every `FileFormat` row is a file format
(`ascii`, `CDF`, `csv`, `FITS`, `HDF5`, `IDL.sav`, `ISTP-Compliant`, `JSON`, `netCDF3/4`, `Zarr`,
`Other`), and this software produces none of them. Selecting `Other` to mean "an interactive plot
window" would misrepresent a display as a file. **The emptiness is the correct and evidenced answer,
not an unfilled gap.**

**This field's emptiness carries no implication for Field 13.** The reasoning here is entirely about
what the code writes and does not bear on the selected installable-package criterion for language.

### 20. Operating System (RECOMMENDED)
**Operating Systems:**
- Operating System Independent

Two grounds, and one important limit on the evidence.

**The declaration.** `setup.cfg` carries the classifier `Operating System :: OS Independent`. That is
the author's own statement, in the packaging metadata, and it maps exactly onto the vocabulary row
of the same meaning.

**The code supports it.** The package is pure Python with no compiled extension, no build step beyond
`setuptools`, no subprocess call, no shell invocation and no platform check. All filesystem access
goes through `pathlib.Path`, including `Path(fn).expanduser()` — the portable idiom. The declared
dependencies (`python-dateutil`, `pandas`, and the optional `scipy` and `matplotlib`) are all
available on Linux, macOS and Windows.

**The CI history, which must be read from the whole history and not from the pin.** There is **no CI
at the pin** — the pinned commit `f0f0074` is literally the commit titled *Delete .travis.yml*, and
no GitHub Actions workflow has ever existed in this repository. But two CI services ran during the
project's active life, and only one of them was Linux-only:

- `.travis.yml`, present `f127c7b` (2018-03-16) → `f0f0074` (2022-08-11), across **four content
  revisions** (`f127c7b`, `0e48fdf`, `fdddb4b`, `5d3186b`). It declared `language: python`
  throughout. Linux was **explicit, not merely the default**: the first two revisions carry an `os:`
  list whose sole entry is `- linux`; the key is absent from the last two, which fall back to
  Travis's Linux images. Either way no non-Linux platform is ever named in this file.
- `.appveyor.yml`, present `f127c7b` (2018-03-16) → `fdddb4b` (2020-05-12), i.e. for **the first two
  years of the project**. It declared a two-OS image matrix — `Visual Studio 2017` and `Ubuntu` —
  and configured the test suite to run on both — the original revision has `after_build:` on one line
  followed by `- pytest -v` as a sequence item, changed to
  `test_script: pytest -rsv` at `4c41ad9` (2018-08-09). Windows was a first-class target: the file
  also pins `PY_DIR: C:\Python36-x64`, later `C:\Python37-x64`, and prepends it to `PATH`.

**So the cross-platform claim is evidenced by configuration — and configuration is not outcome.**
What the repository proves is that the author *targeted* Windows and Linux and wired both into CI for
two years. It does not prove any run ever passed. That distinction is not pedantry here: the only
surviving outcome signal is the AppVeyor badge for project `1a1ujuhlupob96m9`, which today renders
`build unknown` in grey, because AppVeyor retains no public history for a project whose configuration
was removed in 2020. Note also that `README.md` carried that badge until `678147a` (2022-08-11) —
**two years after `.appveyor.yml` was deleted at `fdddb4b`** — so for its last two years the badge
tracked nothing at all. `Operating System Independent` therefore rests on the author's classifier,
the pure-Python argument above, **and** a real two-platform test *configuration*. It is the correct
single value.

**Considered and rejected:** enumerating `Linux`, `Mac` and `Windows` alongside or instead of
`Operating System Independent`. The AppVeyor matrix would support `Linux` and `Windows` on a
configured-platforms reading, and this was reconsidered once that history came to light. It is still
rejected, for two reasons that do not depend on the absence of evidence: the author's own
`Operating System :: OS Independent` classifier is a deliberate statement that the package is not
platform-bound, and enumerating the two platforms that happened to have CI runners would understate
a pure-Python package with no platform-specific code — `macOS` was never tested and would be no less
supported. `Solaris`, `MobilePlatform`, `Other` — no basis of any kind.

**A correction of record, kept because it explains why this section is worded as it is.** An earlier
reading of this repository concluded that "the only CI this project ever had was Travis" and that
there was "no evidence of any platform ever being tested other than Linux". That was false, and it
was false for an instructive reason: it was derived from the tree **at the pin**, where `.travis.yml`
is the last thing deleted and `.appveyor.yml` is long gone. Deleted files are invisible to any
inspection of a single revision. A future refresh checking CI history must enumerate additions across
the whole ancestry, not list the files present at the tip.

### 21. CPU Architecture (RECOMMENDED)
**CPU Architectures:**
- CPU Independent

Follows from the same fact as Field 20: the package is pure Python with no compiled component, no
architecture-specific code path and no binary wheel. Nothing in it can be architecture-sensitive.
`setup.cfg` declares no architecture classifier, which is consistent — pure-Python projects normally
declare none.

**Considered and rejected:** `x86-64`, `Apple Silicon arm64`, `Linux aarch64 or arm64`, `ppc64le`,
`Sun (SPARC)` — selecting any specific architecture would imply a binary distribution or an
architecture-tuned code path, and there is neither. `GPU` and `HPC or HEC` — no accelerator code, no
parallelism, no scheduler integration; the entire workload is parsing 226 rows of text and drawing
one figure. `Other` — the catch-all among the vocabulary's nine rows, and the only one not otherwise accounted for above;
it exists for an architecture the enumerated list does not cover, and no architecture at all is at
issue here, so it has nothing to name. With the stored value that is all nine rows disposed of.

### 22. Related Phenomena (OPTIONAL)
**Related Phenomena:** Not found

**Empty is the correct answer, and the enumeration is what makes that durable.** The `Phenomena`
vocabulary is closed and contains exactly **seven** rows:

`Coronal Heating` · `Coronal Mass Ejections` · `Geomagnetic Storms` · `Solar Corona` ·
`Solar Flares` · `Solar Wind` · `X-ray emission`

Six of the seven are solar or heliospheric and have no connection whatever to a ground-based
thermospheric wind reader. The seventh, `Geomagnetic Storms`, is the only one worth a moment: SDI
wind observations at Poker Flat are certainly used in storm-time studies, and one could construct an
argument from the auroral setting. It fails on the field's own terms — Field 22 asks for phenomena
**the software is designed to support**, and this software is designed to read section 04 of one
instrument's ASCII product and draw a line plot. It is phenomenon-agnostic: it neither detects,
models, classifies nor filters on any geophysical event, and the word "storm" appears nowhere in the
tree.

**The phenomenon this software actually concerns — thermospheric neutral wind — has no row in the
vocabulary**, and there is no free-text path. So the emptiness here is not "we found nothing"; it is
"the seven available rows were each considered against the software and none applies." A future
refresh should re-check the vocabulary for a neutral-wind, airglow or aurora row before concluding
anything has changed, and should not settle for `Geomagnetic Storms` as a near-miss.

### 23. Development Status (RECOMMENDED)
**Development Status:** Unsupported

**This is the clearest correction in this refresh: HSSI held no development status for this software
before this refresh, and the correct value is determinable with certainty.**

**The determining fact is that the repository is archived.** GitHub reports `archived: true` for
`space-physics/scanning-doppler-interferometer`. Archiving is an explicit, deliberate act by the
owner that makes the repository read-only: no issues, no pull requests, no further commits. It is the
strongest available public signal that an author has ceased work.

**Why `Unsupported` and not one of the other seven rows.** The vocabulary row's definition, quoted
verbatim from the controlled list, is:

> The project has reached a stable, usable state but the author(s) have ceased all work on it. A new maintainer may be desired.

Both halves fit. *Reached a stable, usable state*: the package installs, its test suite passes
(`pytest -q` → `1 passed` at the pin), and its documented ASCII parsing path returns correct data —
`txt2dat` on the bundled sample yields a 226-row, 8-column DataFrame with exactly the expected
columns. *The author has ceased all work on it*: archived, last commit 2022-08-11, single author, no
successor. Note the definition says a new maintainer **may** be desired — a possibility, not a
solicitation. If this sentence is ever quoted, quote it as written; paraphrasing it into "a new
maintainer is wanted" attributes an intention to the author that neither he nor the vocabulary
expresses.

**The alternatives, and why each fails.**

- **`Inactive`** ("no longer being actively developed; support/maintenance will be provided as time
  allows") — the closest competitor, and it fails on the second clause. An archived repository cannot
  accept an issue or a pull request; no support can be provided as time allows, because the mechanism
  for providing it is switched off. `Inactive` is the right value for a dormant-but-open repository,
  which this is not. (It is, correctly, the value HSSI records for the author's own Digital Meridian
  Spectrometer, whose repository is *not* archived — the two entries differ because the repositories
  differ, and that contrast is worth preserving.)
- **`Abandoned`** — its definition requires that there has *not* yet been a stable, usable release
  and that development stopped before reaching one. This software reached a working, tested state on
  its first day and remained working for years. It was finished and set down, not abandoned mid-build.
- **`Moved`** — nothing was moved. The repository did change owner (`scivision/…` →
  `space-physics/…`, and the old path still redirects), but that predates the archiving by years, the
  current location *is* the authoritative one, and `Moved` denotes a project that now lives
  elsewhere.
- **`Active`, `WIP`, `Suspended`** — each asserts ongoing or intended future work.
  Archiving is the explicit negation of that.
- **`Concept`** — fails for a different reason, and the distinction is worth keeping straight. Its
  definition ("Minimal or no implementation has been done yet, or the repository is only intended to
  be a limited example, demo, or proof-of-concept") says nothing about future work at all; it is a
  claim about how much was built. It is wrong here because a great deal was built: the package is
  fully implemented, installable, and covered by a test suite that ran under two CI services.

**Two traps that could produce a wrong value here, both recorded so they are not walked into again.**

1. **`setup.cfg` declares the classifier `Development Status :: 4 - Beta`.** This is the *package's*
   self-description, written in 2018 and never revised — it describes the code's maturity at the time
   the line was typed, not the project's lifecycle state today. There is no `Beta` row in the
   vocabulary, and the nearest thing to it (`WIP`) is flatly contradicted by the archived state. A
   stale classifier does not override an explicit archival action by the same author four years
   later.
2. **GitHub's `updated_at` for this repository is `2023-01-27T22:21:54Z`, which is *later* than the
   archiving and later than the last commit.** It is not commit activity. `updated_at` advances on
   any metadata touch — a description edit, a topic change, a settings change, the archiving action
   itself. The field that reflects code is `pushed_at`, which is `2022-08-11T13:36:42Z` and matches
   the final commit exactly. Reading `updated_at` as recent development would produce `Active`, and
   would be wrong.

### 24. Documentation (RECOMMENDED)
**Documentation:** https://github.com/space-physics/scanning-doppler-interferometer

**The repository is the documentation, because there is nowhere else.** The entire user-facing
documentation of this project is the README's nineteen lines, only eleven of them non-blank: a
one-sentence purpose statement, an
install command (`pip install -e .`), a self-test command (`pytest -v`), one usage example, and an
embedded example figure. There is no `docs/` directory (there never has been — see the
`.gitattributes` note in Field 13), no Read the Docs site, no GitHub Pages site, no wiki content, and
GitHub reports the repository `homepage` as an empty string. Recording the repository URL is the
honest answer, and it is what HSSI already holds.

**Negative research on the wiki, with a control.** GitHub's API reports `has_wiki: true` for this
repository, which invites the conclusion that wiki documentation exists. It does not.
`git ls-remote https://github.com/space-physics/scanning-doppler-interferometer.wiki.git` fails with
`Repository not found` — the flag is on but no wiki repository was ever created, which is GitHub's
default state for a repository whose owner never used the feature. The control matters: the same
command against a repository that *does* have a wiki succeeds and lists refs, so the failure is a
real absence rather than a broken probe. **`has_wiki: true` carries no documentation for this entry.**

**Documentation drift at the pin — recorded because the README's one usage example does not work as
written.** The README instructs:

```
PlotWinds data/PKR_2017_061_date_03_02_sky_5577_nz0115.txt
```

That bare-command form requires an installed console script, and **the console script was removed
from the packaging metadata and never replaced.** At `0e48fdf` (2018-08-09) `setup.cfg` contained:

```
[options.entry_points]
console_scripts =
  PlotWinds = PlotWinds:main
```

It is absent by `e9acdb6` (2019-11-22, subject *setup template*), whose diff removes exactly those
three lines, and it is absent at the pin — where `setup.cfg` declares neither `scripts` nor
`entry_points` and a tree-wide search for `console_scripts` returns nothing. **The consequence is an
entailment, not a test result, and it is certain either way:** setuptools creates console scripts
only from declared entry points, so `pip install -e .` at the pin can produce no `PlotWinds` command
on `PATH`. The script must be invoked as `python PlotWinds.py <file>` from the
repository root, which is how the runtime results in the Technical Reference were in fact obtained.
The README was never updated to match, so the documented invocation and the shipped
packaging disagree — the documented command is not merely broken at the pin, it is undeclared.
This is characteristic of the "project template" refactors visible throughout
this history: an upstream template was applied wholesale, and collateral removals went unnoticed
because the project had no test covering the entry point.

**A second, smaller instance of the same pattern:** `MANIFEST.in` reads `include LICENSE`, naming a
file deleted at `fdddb4b` when the project relicensed and renamed it `LICENSE.txt` (Field 15).

**Even invoked correctly, the documented example does not complete under current dependencies** —
established in the Technical Reference below and bearing on Field 18's `.sav` note. That is
dependency bit-rot in an archived project, not a documentation error, and it is kept separate from
the drift above on purpose.

**Considered and rejected as the Field 24 value:** the PyHC registry page for this package — it is a
third-party listing that points back here and adds no documentation; the UAF archive page — it
documents the *instrument and its data*, not this software, and is the right citation for the format
rather than for the code.

### 25. Funder (OPTIONAL)
**Funder:** Not found

**No funding source is stated anywhere in the software or its surroundings**, and the search was
specific rather than cursory. The README acknowledges nothing. `setup.cfg` names no funder. There is
no `ACKNOWLEDGMENTS` file, no `NOTICE`, no grant number in any file, and no funding statement in any
commit message. Because the project has no publication of its own (Field 14), there is no
Acknowledgments section or Data Availability Statement to mine — the usual best source for this
field simply does not exist here.

**Considered and firmly rejected: `.github/FUNDING.yml`.** A funding file did exist in this
repository's history — added at `fdddb4b` (2020-05-12) and deleted at `bdd9b05` (2021-03-22) — and it
read:

```
github: [scivision]
ko_fi: scivision
```

**These are personal donation channels — GitHub Sponsors and Ko-fi — not research funders.** They
name no institution, no agency, no award. Recording either as a Funder would misrepresent a tip jar
as a grant. The file is additionally absent at the pin, so it does not even describe the software's
final state. It is documented here precisely because it is the one funding-shaped artifact in the
history and a future agent will find it.

**Also considered and rejected: inferring a funder from the author's affiliation.** Boston University
employs the author (Field 6) and the University of Alaska Fairbanks operates the instrument, but
neither fact is a statement that either institution funded this software. Field 25 asks who funded
the work; an employer is not automatically a funder, and inferring one would be fabrication.

**Rejected as a source: the instrument papers.** Conde & Smith's acknowledgements name the agencies
that funded *the instrument and the observations* in the 1990s. Attributing those awards to a Python
package written in 2018 by a different author at a different institution would be plainly wrong.

### 26. Award Title (OPTIONAL)
**Award:** Not found
- **Award Title:** Not found
- **Award Number:** Not found

Follows directly from Field 25 — there is no funder to attach an award to. Independently confirmed:
a regular-expression search of all twenty tracked files for award-number patterns (NSF/NASA style
grant identifiers, and the general `10.xxxx/` DOI form) returns no matches, and neither the README
nor any commit message mentions a grant.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Related Publications:**
- https://doi.org/10.1029/95GL02437
- https://doi.org/10.1364/AO.36.005441
- https://doi.org/10.1029/97JA03331

**All three Conde & Smith instrument papers are recorded as related publications.** Before this
refresh the HSSI record held no value here. These three verified papers supply the scientific context
needed to interpret the supported instrument's measurements; the developer's lack of an explicit
bibliography remains an important caveat, documented below, but is not determinative for this
curated related-publication field.

**The developer did not explicitly prioritize any publication.** Field 27 asks for publications
**that the software developer prioritizes** — the developer's own choice of what a user should read.
The repository cites no publication at all. A search of all twenty tracked files for `doi`, `zenodo`,
`citation`, `cite`, `bibtex` and
`arxiv` returns **zero** matches, as does a search for the `10.xxxx/` DOI pattern; the search itself
works, since a control term (`wind`) returns **thirty matching lines across seven files** under the
identical invocation. There is no
`CITATION.cff`, no `REFERENCES` section, no bibliography, and no reference in any docstring. The
README's nineteen lines — eleven of them non-blank — name a person, "PI Mark Conde", and no paper.

**The candidates, all verified against Crossref (2026-09-03).** These are the peer-reviewed papers
describing the instrument whose data this software reads, by the PI the README names:

| DOI | Citation |
|---|---|
| `https://doi.org/10.1029/95GL02437` | Conde, M. & Smith, R. W. (1995). *Mapping thermospheric winds in the auroral zone.* Geophysical Research Letters, 22(22), 3019-3022, 1995-11-15. |
| `https://doi.org/10.1364/AO.36.005441` | Conde, M. & Smith, R. W. (1997). *Phase compensation of a separation scanned, all-sky imaging Fabry–Perot spectrometer for auroral studies.* Applied Optics, 36(22), 5441, 1997-08-01. |
| `https://doi.org/10.1029/97JA03331` | Conde, M. & Smith, R. W. (1998). *Spatial structure in the thermospheric horizontal wind above Poker Flat, Alaska, during solar minimum.* Journal of Geophysical Research: Space Physics, 103(A5), 9449-9471, 1998-05. |

The third is especially apposite: it is about this instrument, at **this site**, measuring **this
quantity**.

**Why all three are recorded.** A user who finds this entry and downloads an SDI ASCII file cannot
interpret it without knowing what a scanning Doppler imager measures and how the wind fields are
derived; these three papers are the literature that answers that, and there is no other. Field 27 is
explicitly for related publications rather than for a paper describing the software (that is Field
14, correctly empty), so an instrument paper is not categorically excluded. The 1998 paper in
particular reads as the natural "further reading" for the bundled sample. And the developer's silence
may be an artifact of a small utility repository rather than a considered editorial position. Taken
together, the three papers document the mapping method, instrument phase compensation and the
Poker Flat thermospheric-wind application, so each contributes distinct context.

**Leaving the field empty was considered and not selected.** The definition says *the developer
prioritizes*, and a
curator selecting papers on the developer's behalf substitutes their own judgement for the one the
field asks about. The instrument-paper-is-not-a-software-publication distinction is real: these
papers predate the software by twenty to twenty-three years, were written by different people at a
different institution, and describe hardware and analysis methods rather than this code. If instrument
papers were admissible on relevance alone, every instrument-reading utility in the catalogue would
acquire its instrument's bibliography by curator fiat, and the field would stop meaning what it says.
There is also a selection problem with no principled answer: Conde has published extensively on SDI
over three decades, and choosing three papers — or choosing which three — is an editorial act the
developer never performed.

**A narrower alternative was also considered and not selected.** Recording only
`10.1029/97JA03331` (the Poker Flat thermospheric wind paper) is the narrowest defensible addition:
it is the single paper that most directly explains the bundled sample, and it avoids the "publish the
instrument's whole bibliography" objection. It was not selected because the other two papers provide
distinct method and instrument context rather than merely expanding a bibliography by association.

**Not candidates.** The UAF archive page
(`http://sdi_server.gi.alaska.edu/sdi_web_plots/sdi_arc.asp`) is a data browser, not a publication.
The ADS full-text hits discussed in Field 14 are a tokenization artifact and none of them cites this
software. And no paper anywhere cites this repository — the slug returns zero full-text hits in ADS
under all three spellings, against controls returning 254 and 337 for other software names.

### 28. Related Datasets (OPTIONAL)
**Related Datasets:** Not found

**No dataset has a persistent identifier here, and one bundled file is not a dataset.** The tree
contains a single data file, `data/PKR_2017_061_date_03_02_sky_5577_nz0115.txt` — 23,151 lines, one
night's observations from Poker Flat on 2017-03-02 at 557.7 nm. It is committed to the repository as
a **test fixture and README example**: the test suite reads it, the README's usage line points at it,
and the bundled figure was produced from it. It has no DOI, no landing page and no citation of its
own.

**The upstream archive was considered as a candidate and rejected — but not on the ground a careless
reading would reach for.** Field 28 does **not** require a persistent identifier: its own guidance
says the URLs are "ideally DOIs" and that "for a dataset with no DOI, use its permanent landing
page". A DOI-less dataset is admissible here, and a future agent must not conclude otherwise from
this entry. The UAF SDI plot archive at `http://sdi_server.gi.alaska.edu/sdi_web_plots/sdi_arc.asp`
is live and is the genuine source of this data, so it clears the admissibility bar the field actually
sets. It is rejected on the two grounds that remain. **First, it is not a landing page for any
dataset.** It is an ASP query endpoint — a monthly browser that takes a site, wavelength and date and
generates plots and files on demand. There is no page there that identifies *a* dataset one could
cite; there is an interface that generates many. **Second, it carries no persistence commitment of
any kind** — bare HTTP, a script endpoint, no handle, no accession number, no versioning and no
stated retention policy. A "permanent landing page" is what the field asks for when a DOI is absent,
and permanence is the one property this URL does not offer. The archive is correctly represented
elsewhere in this record — as the observatory association in Field 32, as the
`Observatory/Mission-specific` data source in Field 17, and as the provenance of the vendored IDL
reader in Field 13.

**Negative research.** No dataset DOI appears anywhere in the tree (the same zero-match DOI-pattern
search recorded under Field 27), and no Zenodo or DataCite deposit of SDI data by this author exists
(Field 2's sixteen Zenodo queries, with differential controls, returned nothing).

**CEDAR Madrigal holds archived data for this instrument, and it still does not belong here.** This
is the one candidate that is a properly curated archive rather than a query endpoint, so it deserves
the fuller treatment. Madrigal registers instrument code **5465**, `Poker Flat all-sky scanning
Fabry-Perot`, PI **Mark Conde** (`mark.conde@gi.alaska.edu`), at 65.12°N, 212.57°E, altitude 0.44 km
— coordinates that agree with the bundled sample's `Latitude:  65.1192` / `Longitude: -147.4303`
(212.57°E being −147.43°E). Note that the coordinates alone do **not** identify it: row 5475, `Poker
Flat Fabry-Perot` (PI John Meriwether), sits at the identical 65.12 / 212.57 / 0.44. The
discriminators are the PI and the words *all-sky scanning*. The archive holds **five** experiments,
all under Conde: four in 2002 (`10jan02`, `01feb02`, `24mar02`, `01apr02`, each titled *FPI
experiment*) and one on `06may11` titled *Poker Flat Scanning FP*.

It is rejected because Field 28 asks for datasets **the software supports functionality for**, and
nothing connects this software to those files. The repository never mentions the archive: `git grep
-in -E "madrigal|cedar|hdf"` exits 1 at the pin and returns nothing across the entire ancestry. The
formats do not meet either — this package reads space-delimited ASCII carrying a `Latitude:` header
and IDL `.sav`, whereas Madrigal serves CEDAR/HDF5. And all five experiments predate the
repository's first commit (2018-03-16). The relationship is instrument-level, not software-level:
the same physical instrument, the same PI, no demonstrated functionality over the archived data.

**A methodological warning for whoever re-runs this, because it has already produced one false
finding.** Querying `getExperimentsService.py` for code 5465 across the full 1990–2026 window **times
out**: `curl` exits 28 having written zero bytes. A caller that checks only the output and not the
exit status will read that empty result as *no experiments exist* and record a confident negative
that is simply wrong. Split the window — decade chunks each return in time — and require `rc=0`
before believing any empty answer. The positive control is code 61 (Poker Flat IS Radar), which
returns roughly 280 KB for a five-month window and confirms the service is answering at all.

### 29. Related Software (OPTIONAL)
**Related Software:**
- https://github.com/space-physics/digital-meridian-spectrometer
- https://github.com/space-physics/dascasi

**Both peer tools are recorded as related software.** Before this refresh the HSSI record held no
value here. Digital Meridian Spectrometer and DASCutils are selected as distinguishing neighbours
because they are closely related Poker Flat optical-data tools by the same author. They are not
dependencies or interoperable packages; those separate boundaries remain documented below.

**Settled: no dependency of this software qualifies, and this is a rule rather than a preference.**
The complete dependency set at the pin is `python-dateutil` and `pandas` (required), plus `pytest`,
`flake8`, `mypy`, `scipy` and `matplotlib` (extras). **Five of the seven — `python-dateutil`,
`pandas`, `pytest`, `scipy` and `matplotlib` — are named outright in the Tier A
generic-scientific-stack exclusion. `flake8` and `mypy` are not named, and are disposed of by the
same rule rather than in spite of it**, because Tier A is explicitly a list of examples and not a
closed list: the governing test asks whether a package would be equally at home in a web
application, a finance model or a biology pipeline, and a linter and a type checker answer yes as
plainly as a dataframe library does. An entry reading "depends on pandas" would read
identically for a large fraction of the catalogue and would carry no information. There is no
domain-specific dependency in this package at all — no heliophysics library, no instrument library,
no format library beyond `scipy.io.readsav`.

**A false lead recorded so it is not chased: `mypy.ini` contains a stray `[mypy-xarray]` section.**
`xarray` is a Tier B package that *would* qualify if a specific exchange were demonstrated — so the
section looks like evidence. It is not. **`xarray` is imported nowhere in this repository, appears in
no dependency list, and is used by no function.** The section is leftover from the author's shared
project template — the same template responsible for the `docs/*` and `paper/*` entries in
`.gitattributes` for directories that do not exist (Field 13). Note that it is the **only** per-module
section in the file: `mypy.ini` declares no stanza for `scipy` or `matplotlib`, the two optional
dependencies this project actually uses, which is itself a sign that the `xarray` section was
inherited rather than written for this code. A configuration stanza for an absent library is not use,
and certainly not interchange.

**The selected pair consists of two by-concept peers by the same author.** Neither is a dependency;
both are tools for the same site and the same kind of measurement, which is the relationship
Field 29 is for ("similar-purpose tools, a predecessor, a companion").

| Candidate | Repository | The case for it |
|---|---|---|
| **Digital Meridian Spectrometer** | `https://github.com/space-physics/digital-meridian-spectrometer` | Same author, same institution, same site, same task, same emission line. HSSI's own description of it reads "Load and plot UAF Geophysical Institute Digital Meridian Spectrometer data from Poker Flat Research Range... ground-based meridian scanning photometer that measures auroral emissions at multiple wavelengths, including... 557.7 nm [OI]" — 557.7 nm is exactly the wavelength of this software's bundled sample. Both are "load one Poker Flat optical instrument's product and plot it" utilities of near-identical shape. |
| **DASCutils** | `https://github.com/space-physics/dascasi` | Same author, same site: utilities for the Poker Flat Digital All Sky Camera. A third ground-based optical instrument at the same observatory, same load-and-plot idiom. |

**Why they are recorded.** A researcher working with Poker Flat optical data would plausibly want
all three, and before this refresh the catalogue gave no path from this entry to the other two. Field 29's purpose
is exactly this kind of *distinguishing* neighbour — it helps a visitor understand what this software
is by seeing what sits beside it.

**The narrower alternative of leaving the field empty was considered and not selected.** "Same author, same site" is a weak relation if it is not also a functional one,
and there is none: the packages share no code, no format, no data model and no cross-reference. This
software reads an SDI ASCII product; DMS reads a spectrometer product; DASCutils reads all-sky camera
images. Adding them risks turning Field 29 into an author's-other-projects list, which is not what it
is for. There is also a scope worry — if these two qualify, so plausibly does GeoDataPython and
several other Poker Flat tools, and the natural stopping point is unclear.

**One asymmetry supports the selection without erasing that caveat.** Those two tools
**cross-reference each other** in the catalogue while omitting this entry. Recording them here partly
closes an existing gap rather than inventing an isolated relation — but this entry's relations remain
one-directional, since nothing points back (see the inbound research below).

**Inbound references: a verified zero, by two independent routes with positive controls.** This
matters because it rules out the easiest way to populate the field — mirroring an existing
relationship — and because a future agent should not repeat the search.

- **Route 1, the relations table.** No related-item record in the catalogue references this
  repository under any spelling: `scanning-doppler`, `scanning_doppler`, `scanningdoppler`,
  `space-physics/scanning`, `scivision/scanning` all return nothing across all 828 rows. Controls on
  the same table confirm the search works and that this author's other packages *are* referenced:
  `iri90` → 2, `glow` → 2, `msise00` → 1, `pyIRI2016` → 1.
- **Route 2, the catalogue records themselves.** Sweeping all 123 software records' relation lists
  finds no entry that mentions this software. Control: `dascasi` **is** referenced inbound, by
  AstrometryAzEl and by Digital Meridian Spectrometer — so inbound references of exactly this shape
  exist in the catalogue and simply do not point here.

### 30. Interoperable Software (OPTIONAL)
**Interoperable Software:** Not found

**Empty by design.** Field 30 requires a *demonstrated
exchange* — a shared or converted data model, an adapter or converter API, a plugin relationship, a
companion package, or a cross-language bridge to a named domain tool. **Nothing in this repository
exchanges anything with any other scientific package.**

The software's entire interface is: read one instrument's ASCII file (or an IDL save file) from local
disk, return a `pandas.DataFrame`, draw a matplotlib figure. There is no export function, no
converter, no writer of any kind (Field 19), no plugin hook, no documented interchange format, no
`to_*`/`from_*` adapter, and no bridge to IDL, MATLAB or any other environment at runtime. The
vendored `archive/sdi_ascii_reader.pro` is not a bridge either — it is a standalone third-party IDL
routine that reads the same file independently; the two implementations never communicate, share no
data structure, and cannot call each other.

**The same Tier A exclusion as Field 29 disposes of the dependency list**, and more strictly here:
returning a `DataFrame` is not interoperability with pandas, drawing a figure is not interoperability
with matplotlib, and calling `scipy.io.readsav` is using a library, not exchanging with a peer tool.
**Two blanket claims are specifically rejected**: "part of the standard scientific Python ecosystem"
and "a PyHC-registered package, so it interoperates with PyHC packages" — neither is evidence of any
exchange, and either would read identically for an arbitrary package.

**The two tools recorded in Field 29 do not qualify here.** Digital
Meridian Spectrometer and DASCutils share this software's author, site and idiom, but they exchange
no data with it: no common format, no shared data model, no import of one by the other. Conceptual
kinship is a Field 29 question; Field 30 needs a demonstrated exchange, and there is none.

### 31. Related Instruments (OPTIONAL)
**Related Instruments:** Not found

**This is an evidenced emptiness, arrived at by exhausting the controlled vocabulary — not an
unfilled gap.** The software is unambiguously instrument-specific (it parses one instrument's ASCII
product and nothing else), so it comfortably passes the "designed to support" relevance gate. The
obstacle is entirely on the vocabulary side: **Mark Conde's scanning Doppler instrument has no record
in HSSI's instrument vocabulary in any form.**

**The sweep, so it is not repeated.** The `InstrumentObservatory` vocabulary was read in full — 7,602
rows, of which 4,492 are instruments and 3,110 observatories, and **every row carries a
`https://spase-metadata.org/` identifier** (zero non-SPASE rows, consistent with the vocabulary being
fully SPASE-backed). Five columns were searched, not one: `name`, `abbreviation`, `identifier`,
`definition` and `landing_url`.

| Query | Result |
|---|---|
| `scanning doppler` (all five columns) | **0 rows** |
| `\bsdi\b` (all five columns) | **0 rows** |
| `\bconde\b` (all five columns) | **0 rows** |
| `fabry` or `interferomet` in `name` | 7 rows, all other instruments |

**An anchoring trap, recorded because it produces a convincing false positive.** An *unanchored*
search for `conde` returns **4 rows** — LASCO, the Vega Mission, Venera-Halley 1 and Venera-Halley 2.
None has anything to do with Mark Conde: all four match the substring inside the word "**conde**nsed"
in their definitions. With word boundaries applied the count is **0**. Any future sweep must anchor,
or it will appear to find something.

**The seven interferometer-family rows, enumerated so none is mistaken for a match.** Each is a
different instrument on a different platform: `Fabry-Perot Interferometer` (Dynamics Explorer 2),
`Fabry-Perot Interferometer on SESAME`, `Fabry-Perot Imager Observation at Syowa Station`,
`TIMED Doppler Interferometer` (TIDI), `Michelson Interferometer for Global High-resolution
Thermospheric Imaging` (ICON MIGHTI), `Interferometric BIdimensional Spectrometer` (IBIS), and
`Interferometer Self-Oscillating PROBE` (ISOPROBE). Several measure thermospheric winds by the same
physical principle, which is exactly what makes them tempting — and none of them is the instrument
at Poker Flat whose data this software reads. **Substituting a physically similar instrument for the
actual one is a factual error**, not an approximation.

**Why empty is the *correct* outcome rather than a deferral.** The SPASE resolution ladder says that
where no instrument record exists, the association must not be dropped — the **observatory** is
recorded instead. That is precisely what Field 32 does. The instrument association is therefore not
lost; it is expressed at the level the vocabulary supports. And there is no free-text path: recording
a name without a SPASE identifier either binds silently to an arbitrary same-named row or mints a new
identifierless row, reintroducing exactly the legacy rows a prior cleanup removed. **A legacy 2025
extraction of this repository did propose a bare instrument name with no identifier here.** That is
not a lesser version of the right answer — it is unsubmittable, and it is why this section states the
emptiness so explicitly.

**If a future refresh finds this changed**, the thing to check is whether SPASE has since minted a
record for the UAF Scanning Doppler Imager network. Note the naming divergence recorded in Field 7:
such a record would very likely say **Imager**, not *Interferometer*, so a sweep on the software's
own name would miss it. Search `scanning doppler` unanchored across all five columns, as above.

**The instrument is registered elsewhere, which locates the gap precisely.** CEDAR Madrigal carries
it as instrument code **5465**, `Poker Flat all-sky scanning Fabry-Perot`, PI Mark Conde (see Field
28 for the full record and the query method). Madrigal codes are not SPASE identifiers and HSSI's
vocabulary is wholly SPASE-backed, so this supplies nothing enterable here. Its value is in ruling
out the weaker explanation: the emptiness above is **a gap in SPASE's coverage, not an obscure or
unidentifiable instrument**. A future sweep should treat `Poker Flat all-sky scanning Fabry-Perot`
as an additional search string, since that — rather than either of the software's own names — is the
wording an eventual SPASE record would most plausibly inherit.

### 32. Related Observatories (OPTIONAL)
**Related Observatories:**
- Poker Flat Geophysical Observatory — https://spase-metadata.org/SMWG/Observatory/Ground/Poker.Flat

**The general Poker Flat observatory row is the settled association.** Before this refresh the HSSI
record used `Poker Flat aurora observatory`
(`https://spase-metadata.org/IUGONET/Observatory/TohokuU/opt_obs/pokopt`). The general
`Poker Flat Geophysical Observatory` row is recorded instead because it gives users discovery
alongside the sibling Poker Flat software already associated with that row. The earlier optical row
was a semantically precise alternative and remains a valid vocabulary entry; it was not selected for
this software because its Tohoku-specific namespace fragments discovery across otherwise comparable
Poker Flat tools.

**The observatory association itself is beyond doubt.** The bundled sample's header reads
`Site: Poker Flat Research Range`, `Latitude:  65.1192`, `Longitude: -147.4303`; the filename prefix
is `PKR_`; the UAF archive the file came from lists Poker_Flat as its longest-running site
(1995 onward). The software passes the "designed to support" gate for this observatory without
qualification.

**All six candidate rows, enumerated — because a future sweep will find them and must not choose
arbitrarily.** All are `type = 2` (observatory) and all carry SPASE identifiers:

| Row name | SPASE identifier | Note |
|---|---|---|
| `Poker Flat aurora observatory` | `https://spase-metadata.org/IUGONET/Observatory/TohokuU/opt_obs/pokopt` | associated before this refresh; Tohoku University optical-observations namespace |
| `Poker Flat Geophysical Observatory` | `https://spase-metadata.org/SMWG/Observatory/Ground/Poker.Flat` | definition: "Poker Flat (POKR) Geophysical Observatory"; the SMWG general ground-observatory namespace |
| `Poker Flat` | `https://spase-metadata.org/IUGONET/Observatory/NICT/SALMON/PF` | definition includes the string "Poker Flat Research Range of Geophysical Instititute, University of Alaksa Fairbanks" [SPASE's own typos] — the closest textual match to this software's own sample header |
| `Poker.Flat` | `https://spase-metadata.org/SMWG/Observatory/IAGA/Poker.Flat` | IAGA magnetic-observatory namespace |
| `Poker Flat geomagnetic observatory` | `https://spase-metadata.org/IUGONET/Observatory/TohokuU/mag_obs/pokmag` | geomagnetic, not optical |
| `Poker Flat Geomagnetic Observatory` | `https://spase-metadata.org/IUGONET/Observatory/WDC_Kyoto/WDC/POK` | geomagnetic, not optical |

**Two of the six are eliminable immediately and should not be reconsidered.** The two *geomagnetic*
rows (`.../TohokuU/mag_obs/pokmag` and `.../WDC_Kyoto/WDC/POK`) describe magnetometer operations at
Poker Flat. This software concerns optical Doppler wind measurement; a magnetometer association would
be simply wrong. `Poker.Flat` in the IAGA namespace is the same story — IAGA codes are the
geomagnetic-observatory registry.

**That leaves three plausible rows, resolved here in favour of catalogue coherence.**

- **`Poker Flat aurora observatory` (the association before this refresh).** In favour: it is the *optical* Poker Flat
  row — the Tohoku University namespace segment is literally `opt_obs` — and this software's data is
  optical (557.7 nm auroral green line). On a semantic reading it is arguably the most precise of the
  six. Against: it sits in a Japanese institutional namespace describing Tohoku University's own
  optical instruments at the site, not the site as such; and before this refresh **it was used by
  exactly one entry — this one.**
- **`Poker Flat Geophysical Observatory` (`SMWG/Observatory/Ground/Poker.Flat`).** Selected because it is
  the general-purpose SMWG ground-observatory record for the site, and the SPASE ladder prefers
  `SMWG/...` as the tie-breaker among same-name duplicates. Decisively for discovery, it was **the row
  the rest of the catalogue already used**: before this refresh, three entries carried it — DASCutils,
  Digital Meridian Spectrometer and GeoDataPython — all Poker Flat instrument software, two of them by this same
  author. Before this refresh a visitor filtering on it saw those three and did **not** see this
  entry, even though it is the same kind of software at the same site. Against: it is less specific than the
  optical row about *what* at Poker Flat.
- **`Poker Flat` (`IUGONET/Observatory/NICT/SALMON/PF`).** Considered but not selected. In favour: its definition contains the
  string that matches this software's own sample header most closely — "Poker Flat Research Range".
  Against: it is scoped to the NICT SALMON project's namespace, it is not used by any comparable
  entry, and matching on a definition substring is a weak basis for choosing a record.

**The settled tradeoff favours catalogue coherence over namespace precision.** The optical row
genuinely describes optical observations matching this software's data, while the SMWG row is where
every sibling entry lives and therefore where a searcher will look. A third possibility was also
considered and not selected: **recording two rows** — the SMWG general observatory row for
discoverability alongside the optical row for precision. That is not obviously wrong, since the
field is multi-valued and both records genuinely describe the site, but it duplicates one site
association where a single coherent discovery row is sufficient. Nothing in this rationale treats
the earlier optical vocabulary row as erroneous or calls for its removal from the vocabulary.

**Considered and rejected: the other eleven SDI sites.** The
README says Conde's "instruments" — plural — and the UAF archive confirms the network has spanned
twelve sites: Poker_Flat (1995 onward), Eagle (Oct 2016 onward), Toolik_Lake (Oct 2012 onward),
Kaktovik (Sep 2014 onward), McMurdo (Apr 2016 onward), South_Pole (Apr 2016 onward), HAARP
(Oct 2009-May 2014), Mawson (Mar 2007-Oct 2014), Kingston (Jun-Jul 2015), Abisko (Apr 2024 onward),
Aakenus (Dec 2024 onward) and Kevo (Feb 2025 onward). **Eagle and Toolik Lake do have SMWG ground
observatory rows** in the same namespace as Poker Flat, so adding them would be technically possible.
It would not be evidenced. **Poker Flat is the only site attested anywhere in this repository** — the
bundled sample, its `PKR_` filename, and its `Site: Poker Flat Research Range` header are the sole
site evidence in the tree, and no other site name appears in any file. Expanding one documented
example into a network-wide claim is precisely the inference the relevance gate forbids. The software
would presumably parse any site's file, but "would parse" is not "designed to support a specific
observatory".

### 33. Logo (OPTIONAL)
**Logo:** Not found

**This project has no logo, and the one image in the repository has been examined and rejected.**
Recording that rejection is the point of this section: the file is prominent, it is embedded at the
top of the README, and it will look like an obvious logo candidate to any future refresh.

**The candidate.** `data/winds_sdi_python.png` — the only image file in the tree. 182,760 bytes,
1641x768 pixels, RGBA, sha256
`09b20c6ae7d683dba45370b68ab36ac6ab0679b9e8d620e613edb573c0811f6d`. The README embeds it on line 6 as
`![SDI wind line plot](data/winds_sdi_python.png)`.

**It was looked at, and it is a data plot.** The image is a six-series line chart of wind speed
against time, with a legend reading `Zonal Wind`, `Sigma Zon`, `Merid Wind`, `Sigma Mer`,
`Vertical Wind`, `Sigma Vz`; its title is the sample data filename; its y-axis is labelled
`Wind Speed [m/s]` and its x-axis `Time [UTC]]`.

**Three independent confirmations that it is program output, not artwork:**

1. Those six series are **exactly** the six data columns `txt2dat()` produces from the bundled sample
   — the same names in the same order.
2. The x-axis label reproduces the **literal double-bracket typo** `Time [UTC]]` from `plots.py`
   line 10. No designer would draw that; only `plotwinds()` would emit it.
3. The PNG's `tEXt` metadata chunk reads `Software\0matplotlib version 2.2.0,
   http://matplotlib.org/`. (This is also the sole appearance of a matplotlib URL anywhere in the
   repository — it is inside the binary, not in any source file, which is worth knowing if a URL
   inventory of the tree ever seems to disagree with the source.)

It is the output of the software's own plotting function, committed as the README's example figure.
**Field 33 asks for a logo — a visual identity for the software — and an example plot is not one.**
Recording it would put a data figure in a field that catalogue interfaces render as an identifying
mark. Incidentally, it also does the project a disservice as a thumbnail: at 1641x768 it is a wide,
dense, unreadable-at-small-size chart.

**Negative research on the alternatives.** There is no other image in the tree (the twenty tracked
files contain exactly one binary). There is no project website — GitHub reports the repository
`homepage` as an empty string. There is no documentation site to carry a banner (Field 24). The PyHC
registry entry for this package carries **no `logo:` field**, unlike some registry entries which do.
No DOI record exists to supply one (Field 2).

**A documented omission is the correct outcome here.** Nothing should be invented, and this particular
image should not be reconsidered — it has been looked at.

---

## PyHC Registry Status

This package appears in exactly one of the three PyHC registry lists: `_data/projects_unevaluated.yml`
in `heliophysicsPy/heliophysicsPy.github.io`. It is absent from `_data/projects_core.yml` and from
`_data/projects.yml`, the community list. Pinning the specific file matters — a later refresh that
searches only the core or community list would wrongly conclude the package is not registered at all.

Its entry reads:

```yaml
- name: Scanning Doppler Interferometer
  code: https://github.com/space-physics/scanning-doppler-interferometer
  description: Dowload & plot Scanning Doppler Interferometer data from PI Mark Conde's instruments.
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","specific"]
```

**Quotation hazard: `Dowload` is misspelled in the registry** [sic]. This is a *different* typo from
the README's `Interferomter` (Field 8) — note that the registry spells "Interferometer" correctly
while misspelling "Download", and the README does the reverse. Any quotation must be bound to the
right parent and reproduced byte-exact.

"Unevaluated" is the registry's own classification and means the package has not been assessed
against the PyHC standards; it is not a statement about the software's quality. The registry
corroborates Field 7's name (exactly), Field 3's repository URL and Field 6's author, and is the
source of the `ionosphere_thermosphere_mesosphere` keyword discussed and declined under Field 16. It
carries no `logo:` field, which is one of the sources checked under Field 33.

---

## Technical Reference

Details supporting several fields above, gathered here to avoid repeating them.

**Declared dependencies at the pin** (`setup.cfg`). Required: `python-dateutil`, `pandas`. Optional
extras: `tests` → `pytest`; `lint` → `flake8`, `mypy`; `io` → `scipy`; `plots` → `matplotlib`. Build
requirements (`pyproject.toml`): `setuptools`, `wheel`, unpinned. Fields 29 and 30 explain why none
of these is a relation. `pyproject.toml` carries nothing else but a `[tool.black]` stanza setting
`line-length = 132`. `mypy.ini` declares exactly one per-module section, `[mypy-xarray]`, for a
package used nowhere in the tree — the false lead documented under Field 29.

**Repository shape at the pin — twenty tracked files.** `.coveragerc`, `.flake8`, `.gitattributes`,
`.gitignore`, `LICENSE.txt`, `MANIFEST.in`, `PlotWinds.py`, `README.md`,
`archive/sdi_ascii_reader.pro`, `data/PKR_2017_061_date_03_02_sky_5577_nz0115.txt`,
`data/winds_sdi_python.png`, `mypy.ini`, `pyproject.toml`, `pytest.ini`,
`scanning_doppler_interferometer/__init__.py`, `scanning_doppler_interferometer/base.py`,
`scanning_doppler_interferometer/plots.py`, `setup.cfg`, `setup.py`, `tests/test_all.py`. Nineteen
commits, all by one author, spanning 2018-03-16 to 2022-08-11. No CI configuration at the pin, no
documentation directory, no container definition. (Twenty *files*, nineteen *commits* — the two
counts are close enough to be conflated and are not the same number.)

**Package surface.** `scanning_doppler_interferometer/__init__.py` contains one line,
`from .base import txt2dat`. `base.py` (56 lines) defines the section-marker constant `W4`, and the
functions `plotsav` (IDL save reader, 9 lines), `txt2dat` (ASCII reader, 20 lines) and `index_lineno`
(line-range scanner, 12 lines). `plots.py` (12 lines) defines `plotwinds`. `PlotWinds.py` is the
command-line front end. `tests/test_all.py` contains a single test, which reads the bundled sample and
asserts the shape of the result.

**The data file's sixteen sections, and what reads them.** The bundled sample is 23,151 lines
structured as sixteen delimited sections: 01 `HEADER`, 02 `FOV`, 03 `ALLSKY_TMP_INT`,
04 `LOCAL_GEO_WINDS`, 05 `LOCAL_MAG_WINDS`, 06 `TEMP_SKYMAP`, 07 `SIGMA_TEMP_SKYMAP`,
08 `LOS_WIND_SKYMAP`, 09 `SIGMA_LOS_WIND_SKYMAP`, 10 `GEO_ZONAL_WIND_SKYMAP`,
11 `GEO_MERID_WIND_SKYMAP`, 12 `MAG_ZONAL_WIND_SKYMAP`, 13 `MAG_MERID_WIND_SKYMAP`,
14 `INTENSITY_SKYMAP`, 15 `SNR_SKYMAP`, 16 `CHI_SQUARED_SKYMAP`. Its header records
`Site: Poker Flat Research Range`, `Latitude:  65.1192`, `Longitude: -147.4303`,
`Date UT: 02-March-2017`, `Records: 0226` and `Wavelength in nm: 557.7`.

**Complete URL inventory at the pin — exactly four URLs across all twenty files.** Recorded because
several fields turn on how few external references this project has, and because one of the four is
easy to miss.

1. `http://sdi_server.gi.alaska.edu/sdi_web_plots/sdi_arc.asp` — line 1 of
   `archive/sdi_ascii_reader.pro`. The UAF SDI plot archive; live at the pin's re-examination
   (HTTP 200, DNS 199.165.82.138). Underpins Fields 13, 17, 28 and 32.
2. `https://docs.scipy.org/doc/scipy-0.14.0/reference/generated/scipy.io.readsav.html` — the
   `plotsav` docstring in `base.py`. Still resolves, though it points at a scipy version from 2014.
3. `https://github.com/space-physics/scanning-doppler-interferometer` — the `url` key in
   `setup.cfg`. Field 3.
4. `http://matplotlib.org/` — **inside the PNG binary**, in `data/winds_sdi_python.png`'s `tEXt`
   metadata chunk, not in any source file. A source-only search of the tree will not find it, which
   is why a URL inventory of the *files* and a grep of the *source* give different answers.

**The parsing asymmetry, which Field 4 rests on.** The Python package reads **section 04 only** — the
`W4` constant in `base.py` is the literal pair of banner strings that delimit `LOCAL_GEO_WINDS`, and
`index_lineno` scans for exactly those two strings. The other fifteen sections, including every
skymap, are never touched. The vendored IDL routine `archive/sdi_ascii_reader.pro` (384 lines) parses
the format generically: `HEADER`, `FOV`, all `*_SKYMAP` sections, plus `ALLSKY_TMP_INT`,
`LOCAL_GEO_WINDS`, `LOCAL_MAG_WINDS` and `WIND_GRADIENTS` (the last not present in this sample). **The
Python package is a narrow reader of one section, not a full-format reader**, and the description and
functionality fields are scoped accordingly.

**Runtime behaviour under current dependencies, tested rather than reasoned.** Environment: Python
3.12.8, pandas 2.2.3, matplotlib 3.10.0, scipy 1.15.1, `MPLBACKEND=Agg`. **Invocation, stated because
it is not the one the README documents and cannot be:** the package was *not* installed — it was
imported from the repository root via the working directory, and the driver was run as
`python3 PlotWinds.py <file>`. There is no `PlotWinds` command to run instead (Field 24), so this is
the only way the documented example can be exercised at the pin at all.

- `pytest -q` → **1 passed.**
- `txt2dat()` on the bundled sample → **succeeds**, returning a 226x8 `DataFrame` with columns
  `Begin Time`, `End Time`, `Zonal Wind`, `Sigma Zon`, `Merid Wind`, `Sigma Mer`, `Vertical Wind`,
  `Sigma Vz`. The two time columns hold `datetime.time` objects.
- The README's documented ASCII plotting example → **fails** at `PlotWinds.py` line 27 into
  `plots.py` line 7, `ax.plot(dat["Begin Time"], dat.iloc[:, 2:])`, with
  `TypeError: float() argument must be a string or a real number, not 'datetime.time'` — modern
  matplotlib will not plot bare `datetime.time` objects.
- The `.sav` path → **fails** at `PlotWinds.py` line 24 with `AttributeError`, for the re-export
  reason detailed in Field 18.

**The precise claim, which should not be overstated: the parser works; both plotting paths have
bit-rotted under current dependency versions.** This is not "the package is broken", and it is not
evidence that it never worked — the bundled PNG carries `matplotlib version 2.2.0` in its metadata,
which is direct evidence that the plotting path *did* work when it was written in 2018. It is
ordinary dependency drift in a project archived in 2022, and it is exactly the shape of evidence that
corroborates Field 23's `Unsupported`. The failures are bound to the dependency versions listed
above; a 2018-era environment would behave differently.

**Instrument and physical context.** A scanning Doppler imager (the instrument's published name —
see Field 7) is an all-sky Fabry-Perot spectrometer that scans the sky and derives thermospheric
neutral winds and temperatures from Doppler shifts and widths of airglow and auroral emission lines.
The UAF network observes at 557.7 nm (OI green line, lower thermosphere), 589.0 nm (sodium) and
630.0 nm (OI red line, F-region thermosphere near 240 km). The bundled sample is 557.7 nm data from
Poker Flat, whose field-of-view section records `Auroral Oval Angle:  23.1` — the instrument's
viewing geometry is defined relative to the auroral oval. The quantities in section 04 are horizontal
and vertical neutral wind components in m/s at the station location, aligned geographically, with
one-sigma uncertainties.
