# HSSI Metadata Extraction Results

**HSSI Software ID:** 683398f6-8f62-49a6-9eb3-bf926a9b621c
**Repository:** https://github.com/space-physics/mgs-radio
**Source Revision:** 376f0a5e231e1aed87453ce914dc31f0b81a7db3
**Extraction Date:** 2026-09-02
**Validation Date:** 2026-09-03
**Validation Status:** PASS

---

## Scope note — read this before the evidence

Two facts shape almost every judgement below and are easy to get wrong from the software's name alone.

**1. The data are surface-reflection (bistatic radar) products, not atmospheric profiles.** The
example files shipped in `data/` carry `DATA_SET_ID` `"MGS-M-RSS-5-SDP-V1.0"`, and all three data
links in `README.md` point into the `mgs-m-rss-5-sdp-v1` tree. That data set's Software Interface
Specification — the PDS document `srx.txt` that `matlab/MGSeds.m` itself cites — titles the
investigation `Surface Reflection (SRX) Participating Scientist Investigation Files` and states its
purpose as `The objectives of the investigation include characterization and` /
`interpretation of surface echoes both for their own sake and also to improve` /
`the quality of MGS atmospheric radio occultation results.`, adding that
`strength and dispersion can be used to infer dielectric constant, density,` /
`and centimeter-scale roughness of the reflecting surface [1].` The `.sri` files are therefore
`Surface Reflection Image` products and the `.srt` files `Surface Reflection Table` products.
(These quotations come from
`http://pds-geosciences.wustl.edu/mgs/mgs-m-rss-5-sdp-v1/mors_1014/document/srx.txt`, a fixed-width
PDS3 text file in which every line is 78 characters padded with trailing spaces and terminated by
CRLF — an 80-byte record; each fragment above is byte-exact within one source line, and the `/`
markers stand for the document's own line wrapping and trailing padding, which are not reproduced.)
So the software is a reader and plotter for a Mars **surface-echo / occultation-geometry** radio
science product, whose science reaches the Martian surface and the neutral atmosphere. Nothing about
it is magnetospheric — which is the crux of the Field 5 question below.

**2. The archived upstream repository is not what a first look suggests.** It is archived (read-only)
on GitHub, its Python package directory is `mgsradio/` while the HSSI entry is named `MGSutils` and
the GitHub repository is `mgs-radio`, and its documented example script has been broken since 2020
(see *Durable upstream limitations*). Library use is unaffected.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Not a property of the software. The placeholder is the catalogue convention for an entry the HSSI
team maintains rather than one a maintainer submitted.

### 2. Persistent Identifier (RECOMMENDED)

**Value:** `https://doi.org/10.5281/zenodo.595431`

**Source:** Carried over from the existing HSSI record; independently confirmed against DataCite and
Zenodo.

This is the Zenodo **concept** DOI for the deposit series. Its DataCite metadata is titled
`scienceopen/mgs-utils v1.0.1`, carries `version` `v1.0.1`, is dated `2017-04-24`, and
`https://doi.org/10.5281/zenodo.595431` currently lands on `https://zenodo.org/records/556924` — the
v1.0.1 record. DataCite classifies it as software — its `types` block is
`{"ris": "COMP", "bibtex": "misc", "citeproc": "article", "schemaOrg": "SoftwareSourceCode", "resourceTypeGeneral": "Software"}`.
Worth noting for the choice below: the `citeproc` value is `article`, not a software type, so a
citation rendered through DOI content negotiation may present this deposit in article form even
though the resource is software.

**Provenance of the deposit.** The record's DataCite `relatedIdentifiers` include
`IsSupplementTo https://github.com/scivision/mgs-utils/tree/v1.0.1`,
`HasVersion 10.5281/zenodo.556816`, `HasVersion 10.5281/zenodo.556924`, and
`IsPartOf https://zenodo.org/communities/spacephysics`. The `IsSupplementTo` relation pointing at a
`/tree/<tag>` URL is the signature of the automated Zenodo–GitHub release integration, corroborated
by `README.md`'s badge line
`[![image](https://zenodo.org/badge/24042691.svg)](https://zenodo.org/badge/latestdoi/24042691)`
(24042691 is the GitHub repository id). `https://zenodo.org/badge/latestdoi/24042691` still redirects
to `https://doi.org/10.5281/zenodo.556924`, i.e. Zenodo's own "latest" for this repository is still
the 2017 v1.0.1.

**No later deposit exists, and the concept record proves it directly.** The concept DOI enumerates
its own children: its `relatedIdentifiers` list exactly two `HasVersion` entries,
`10.5281/zenodo.556816` and `10.5281/zenodo.556924`. Those resolve to "scienceopen/mgs-utils v1.0.0"
and "scienceopen/mgs-utils v1.0.1", both dated 2017-04-24. There is no third version in the series,
so nothing on Zenodo corresponds to the 1.1.0 release of 2020.

A second, name-independent check confirms it, and is recorded so a later refresh need not redo it.
Creator-keyed searches are the only route that does not depend on guessing a title: querying Zenodo
for `metadata.creators.person_or_org.name:"Hirsch, Michael"` (48 records),
`metadata.creators.person_or_org.name:"Michael Hirsch, Ph.D."` (20) and
`metadata.creators.person_or_org.identifiers.identifier:"0000-0002-1637-6526"` (20), and paging each
to completion, yields 68 distinct DOIs. The only MGS-titled record among them is
`10.5281/zenodo.556924`. This route matters because a manual deposit made under a different title
would evade any search keyed on the repository name — and note that these creator-name variants are
unnormalized upstream, which is why three separate queries are needed rather than one.

**Why the deposit is stale: released, but not deposited.** GitHub Releases exist for all three tags,
and the one for `v1.1.0` was published on 2020-05-04. So 1.1.0 was not merely declared in
`setup.cfg` and tagged — a release was published for it — and still no Zenodo deposit corresponds to
it. That rules out the "declared but never released" reading and fixes the shape of the anomaly: the
Zenodo–GitHub integration that minted the two 2017 DOIs had stopped firing for this repository by
2020. The most plausible cause, offered here as inference rather than verified fact, is the change of
GitHub organisation after the 2017 deposits — those deposits' `IsSupplementTo` still points at
`scivision/mgs-utils` — since Zenodo's per-repository hook is not known to follow such a move. The
integration's own state is not observable from outside the repository's settings, so that cause
remains unconfirmed; only the released-but-not-deposited observation is established.

**The concept DOI is retained, with its staleness understood rather than overlooked.** The value is
three years and one minor version behind Field 12's recorded release, and that is an accepted cost.
What a visitor gets is a "Software" citation resolving to a real, archived, resolvable deposit; what
they see is a citation reading v1.0.1 (2017) under the long-dead organisation name `scienceopen`
while the same page's Version field says 1.1.0 (2020). The identifier is nonetheless the right one:
a Zenodo concept DOI is *designed* to stand for all versions of a deposit series, and its landing
metadata showing v1.0.1 follows from no later deposit existing rather than from an error in the
identifier. It is also what the project's own README badge tells a user to cite. Someone wanting to
cite this software has no better option, and a slightly stale citation serves them better than none.

Two alternatives were considered and rejected; the reasons are recorded so neither is re-proposed.
**Clearing the field** would leave the entry with no software citation at all, removing the version
mismatch only by removing the information — and the software does have a DOI, so hiding it helps
nobody. **Moving it to Field 14 or Field 27** fails on evidence rather than taste: Field 14 is "the
DOI for the publication describing the software" and Field 27 is for publications, whereas this is a
software deposit that DataCite types as Software and that has no article-like content. Presenting a
code archive in a "Reference Publication" block would mislead a visitor more than the stale version
does.

### 3. Code Repository (MANDATORY)

**Value:** `https://github.com/space-physics/mgs-radio`

**Source:** `setup.cfg` (`url = https://github.com/space-physics/mgs-radio`), the PyHC registry's
`code:` field, and the live GitHub repository (id 24042691, `default_branch` `master`).

Two historic paths, `https://github.com/scivision/mgs-utils` and
`https://github.com/scienceopen/mgs-utils`, each answer HTTP 301 to this URL. They are recorded here
as history, not as alternatives: GitHub's rename redirects are a courtesy that lapses if anyone
re-creates the old path, so the current canonical URL is the safest stored value. The Zenodo
deposit still cites the `scivision/mgs-utils` form, which is why the DOI metadata and this field
disagree about the repository name.

The repository is **archived** upstream (GitHub reports `archived: true`, `disabled: false`,
`fork: false`). Its last commit is the pinned revision, dated 2021-03-22. GitHub's `updated_at` of
2023-11-01 reflects repository-record touches, not code activity, and must not be read as a commit
date. There is no wiki behind the repository — `<repo>.wiki.git` is not reachable — so no release
policy or extra documentation is hiding there.

### 4. Software Functionality (RECOMMENDED)

**Values:**
- Data Processing and Analysis
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Spectrogram

**Source:** the module code at the pinned revision, checked against the live FunctionCategory
vocabulary.

Each of the six is evidenced below, and the categories considered and rejected follow after them.
`Data Processing and Analysis: Spectrogram` is the one added in this refresh; the record previously
carried only the display half of the pair.

- **Data Processing and Analysis** and **: Processing** — `mgsradio/read.py` converts a raw PDS
  product into a usable array: it parses the label with
  `lbl = read_csv(fn, sep="=", index_col=0, header=None)`, applies the label's scale and offset
  (`scale = float(P.at["SCALING_FACTOR", 1])`, `offs = float(P.at["OFFSET", 1])`), byte-swaps and
  reshapes the binary image
  (`np.fromfile(str(imgfn), dtype="int16", count=nSamp * nLine).newbyteorder("B") * scale + offs`
  with `order="F"`), and reads the companion time table with
  `texp = np.loadtxt(srtfn, skiprows=1, usecols=[0], delimiter=",")`.
- **Data Processing and Analysis: Spectrogram** — the exported reader returns a
  time–frequency array, not a figure:
  `df = DataArray(data=data.T, dims=["time", "freq"], coords={"time": t, "freq": f})`. The frequency
  axis is reconstructed in code from the label's documented step
  (`fs = 4.88  # step [Hz], from .lbl description`, then `f = np.arange(f0, fend - fs, fs)`) and the
  time axis from the `.srt` table, and the values are received power in dBW (the PDS label declares
  `UNIT` `"DECIBEL"`). Producing a labelled time–frequency array with physical axes is spectrogram
  work in the array sense, which the taxonomy separates from spectrogram *display*.
  One fact cuts the other way, and it was weighed rather than overlooked when the value was chosen —
  a later refresh should not treat it as newly discovered grounds for removing the value. The Fourier
  transform itself happened upstream: the PDS label credits the product to
  `This image was produced by Dick Simpson of the MGS Radio Science` Team and describes it as built
  from `512-point power spectra`, and the package carries no transform primitive of its own — a
  search of its Python sources at the pinned revision for `fft`, `welch`, `periodogram`, `stft`,
  `wavelet` and windowing calls returns nothing. So the software assembles a spectrogram rather than
  computing one from a time series. That is true, and it is not determinative. What a searcher
  filtering for spectrogram data processing wants is software that hands them time–frequency data,
  and the labelled array this package returns is exactly that.
- **Data Visualization** and **: 2D Graphics** and **: Spectrogram** — `mgsradio/plots.py` draws a
  single kind of figure, `h = ax.pcolormesh(data.time, data.freq, data.values.T, vmin=vlim[0], vmax=vlim[1])`,
  labelled `ax.set_ylabel("Baseband frequency [Hz]")` with colourbar `c.set_label("RX Power [dBW]")`.
  That is a 2-D pseudocolour rendering of a dynamic spectrum, so both children apply.

**The two spectrogram entries are distinct values, not an accidental duplicate, and pruning either
one would lose information.** They are separate rows under different parents, and the rendered
functionality list for this entry carries each subcategory with its parent prefix rather than as a
bare child name. A visitor therefore reads the two as visibly different entries: the same capability
claimed once under a processing facet and once under a display facet, which is what a two-level
taxonomy is for.

**Considered and rejected**, with reasons, so a later refresh does not reopen them:

- **Mission-related** (and its children) — the taxonomy draws the line at whether the software is
  part of a mission's own ground system rather than a third-party consumer of its archived products.
  This is the latter: it reads finished PDS3 deliverables that Stanford produced years after the fact
  (`data/1066m12a.lbl` records `PRODUCT_CREATION_TIME` in 2001 and names its producer as
  `This image was produced by Dick Simpson of the MGS Radio Science`). MGS flew 1996–2006; this
  repository began in 2014. No mission-operations, ingest, or pipeline role exists.
- **Data Processing and Analysis: Calibration** — tempting because the code turns stored integers
  into physical units, but the conversion is a linear scale-and-offset the archive itself supplies in
  the label, not a calibration the software performs (no gain model, response function, or
  flat-field). A visitor filtering for calibration software wants tools that do calibration work;
  this one would be a mild surprise.
- **Data Processing and Analysis: Data Access and Retrieval** — the software performs **no network
  access at all**. Its whole I/O surface is local: `np.fromfile`, `pandas.read_csv`, `np.loadtxt`,
  `Path.read_text` and `Path.glob`. A sweep of the Python sources for `urlopen`, `requests.`,
  `urlretrieve`, `download` and `http` at the pinned revision returns exactly one hit, and it is the
  Apache licence URL `http://www.apache.org/licenses/LICENSE-2.0` in the package docstring. The PDS
  links in the README tell a *human* where to download files by hand. This same fact governs Field 17.
- **Data Processing and Analysis: File Format Conversion** — the software reads PDS3 products and
  returns an in-memory object. It writes no files of any kind (the same sweep finds no `savefig`,
  `to_netcdf`, `to_csv`, `to_zarr`, `open(`, or `write`). In-memory parsing is not format conversion.
  This same fact governs Field 19.
- **Data Processing and Analysis: Image Processing** — the PDS product is nominally an image object
  and the code calls `np.fliplr`, but that corrects the archive's documented storage order rather
  than performing a scientific image operation: the label states
  `one power spectrum.  The first line in` / `the file is the LAST spectrum.` (wrapped across two of
  its lines, each 78 characters plus CRLF — an 80-byte record), so the array arrives bottom-up and
  has to be flipped. There is no deconvolution, filtering, or feature detection.
- **Data Processing and Analysis: Analysis** and **: Time Series Analysis** — the package derives
  axes and physical units and stops. The README describes its own scope as
  ``This example is simply of reading MGS `.sri` high-level occultation data`` and
  ``and plotting. The `.sri` data is big-endian int16, Fortran order.``
  No statistics, fitting, filtering, or derived physical quantities are computed, so the analysis
  catch-all would over-claim.
- **Data Visualization: Line Plots**, **: Movies**, **: 3D Graphics** — `plots.py` contains one
  plotting function and it draws only `pcolormesh`.

### 5. Related Region (RECOMMENDED)

**Value:** Not found — no Region applies, as a deliberate evidenced outcome rather than an
unexamined blank.

This field is RECOMMENDED, so an empty value has to be earned, and the distinction matters: an
evidenced-empty Region is legitimate, whereas a blank nobody examined is a defect. It is earned here.
The vocabulary contains no row describing what this software's data are about, and the two rows that
could look plausible were examined and rejected on the science. The record previously carried
`Planetary Magnetospheres`; this refresh removes that value, for the reasons below.

The live Region vocabulary has 24 rows: Chromosphere, Corona, Earth Atmosphere, Earth Auroral
Subregion, Earth Inner Magnetosphere, Earth Ionosphere, Earth Lower and Middle Atmosphere, Earth
Magnetosheath, Earth Magnetosphere, Earth Magnetotail, Earth Outer Magnetosphere, Earth Thermosphere,
Heliosheath, Interplanetary Space, Jupiter Magnetosphere, Mars Magnetosphere, Neptune Magnetosphere,
Photosphere, Planetary Magnetospheres, Saturn Magnetosphere, Solar Environment, Solar Interior, Solar
Wind, Uranus Magnetosphere. Enumerated here in full because the *absence* of certain rows is the
evidence: **there is no planetary surface, planetary atmosphere, or planetary ionosphere row**, and
the ten Earth-region rows are Earth-specific. The list is flat — no row is a parent of any other —
so selecting a Mars row cannot be justified as "the nearest available bucket."

The science the software serves, per the scope note: Mars surface echoes (dielectric constant,
density, centimetre-scale roughness) and the atmospheric radio occultation those echoes help refine.
`setup.cfg` classifies the package `Topic :: Scientific/Engineering :: Atmospheric Science`. Nothing
in the repository, the data products, or the investigation's specification concerns plasma or
magnetic fields.

The two candidate rows, and why each was rejected:

- **`Mars Magnetosphere` was rejected on the science.** It is the most specific Mars-named row, and
  the form guidance does say to prefer the specific over the broad — but specificity only helps when
  the region is right, and this one is not. MGS's magnetospheric measurements came from a different
  instrument entirely (SPASE
  carries `https://spase-metadata.org/SMWG/Instrument/MGS/MAG` for the magnetometer and an electron
  reflectometer row alongside it), and this software cannot read those data. Choosing it because it
  is the only row with "Mars" in the name would be using a Region filter as a planet filter —
  precisely the coarse-to-fine substitution the flat vocabulary forbids. A visitor filtering Region =
  Mars Magnetosphere is looking for Martian induced-magnetosphere or crustal-field plasma work and
  would click through to a bistatic-radar image reader.
- **`Planetary Magnetospheres`, the value previously stored, was rejected on the same objection one
  level broader.** Its only support is indirect: the PyHC registry tags the package `keywords: ["planetary","specific"]`,
  and this row is the "planetary" member of the five values HSSI's Region field offered before the
  2026-07-29 audit widened it to 24. But PyHC's `planetary` is a Science Area label, not a
  magnetospheric claim. Its `_data/taxonomy.yml` files it under `category: "Science Area"`
  (`description: "The scientific area a package is relevant to"`) among the keywords
  `["geospace", "heliosphere", "ionosphere_thermosphere_mesosphere", "magnetosphere", "planetary", "plasma_physics", "solar"]`;
  the category carries a description but the individual keywords do not. Reading that list, this
  dossier takes `planetary` to stand alongside `magnetosphere` as a sibling label rather than to
  imply it. And defaulting to one of the old five is exactly what the widened vocabulary was meant
  to stop. A visitor filtering for planetary magnetospheres
  expects Jupiter aurorae, Saturn plasma, Martian induced magnetospheres — not Mars surface roughness.

Recording both rows would simply inherit both objections and double the false-positive surface, so
that was rejected too.

**The cost of the empty value, stated plainly:** the entry appears under no Region filter at all, so
a visitor browsing by region will not meet it. That cost is accepted because the alternative is
worse — under either magnetosphere row a visitor would meet it *wrongly*, having been told the
software concerns plasma and magnetic fields when it concerns Mars surface echoes and occultation
geometry. Neither row is recoverable by any reading of the software's actual data, so a later
refresh should read this emptiness as the conclusion it is and not attempt to fill it; the way to
change it would be a new Region row describing a planetary surface, atmosphere or ionosphere.

### 6. Authors (MANDATORY)

**Author 1:**
- **Author:** Michael Hirsch
- **Author Identifier:** `https://orcid.org/0000-0002-1637-6526`
- **Affiliation 1:**
  - **Organization:** Boston University
  - **Affiliation Identifier:** `https://ror.org/05qwgg493`
- **Affiliation 2:**
  - **Organization:** Scivision, Inc.
  - **Affiliation Identifier:** Not found

**Source:** union of the existing HSSI record, `setup.cfg`, and the Zenodo/DataCite creator list.

One person, named consistently by each source below. `setup.cfg` gives
`author = Michael Hirsch, Ph.D.` with `author_email = scivision@users.noreply.github.com`. ORCID
`0000-0002-1637-6526` gives given name `Michael`, family name `Hirsch`, with a current employment at
Boston University (department `ECE`, Research Scientist, from 2018-08), which is the primary evidence
for the first affiliation; the ROR record `https://ror.org/05qwgg493` has `ror_display` "Boston
University", matching the stored organization name exactly. The second affiliation comes from the
Zenodo deposit, which records `SciVision, Inc.`

**The Zenodo record lists the creator twice and that is one person, not two.** DataCite returns
`{"name": "Hirsch, Michael", "nameType": "Personal", "givenName": "Michael", "familyName": "Hirsch", "affiliation": [], "nameIdentifiers": []}`
and, separately,
`{"name": "Michael Hirsch, Ph.D.", "givenName": "Ph.D.", "familyName": "Michael Hirsch", "affiliation": ["SciVision, Inc."], "nameIdentifiers": []}`.
The second entry's name parsing is visibly broken upstream (given name "Ph.D."). Both refer to the
same author; the deposit simply carried the packaging string and the personal name as separate
creators. A future refresh reading the DOI metadata must not split them into two HSSI authors.

**Known divergence, deliberately not proposed for change:** HSSI stores the organization name as
`Scivision, Inc.` while Zenodo writes `SciVision, Inc.` (capital V). The spelling of shared
organization rows is parked as a catalogue-wide question, so this entry does not propose correcting
it here.

**Negative research on a ROR for SciVision.** A ROR lookup for "SciVision" returns exactly one
organization: `https://ror.org/011qev639`, "SciVision Biotech Inc. (Taiwan)", a Kaohsiung-based
biotech company. That is **not** this affiliation — Michael Hirsch's SciVision, Inc. is a US
scientific-software consultancy. The near-match is recorded here specifically so that a later agent
does not attach the Taiwanese biotech ROR to this author. No ROR appears to exist for the correct
organization, so the affiliation identifier stays empty.

### 7. Software Name (MANDATORY)

**Value:** `MGSutils`

Four names are in circulation, and the established one is kept. The field's own definition does not
by itself pick it, so the reasoning is worth recording in full.

| Name | Where it comes from |
|---|---|
| `MGSutils` | the HSSI record, and the PyHC registry entry `- name: MGSutils` |
| `mgs-radio` | the GitHub repository name; `README.md` opens `# mgs-radio` |
| `mgsradio` | the distribution and import name — `setup.cfg` says `name = mgsradio`, and `tests/test_mod.py` does `import mgsradio` |
| `mgs-utils` | the historic repository name, preserved in the Zenodo titles (`scienceopen/mgs-utils v1.0.1`) and in the deposit's `IsSupplementTo https://github.com/scivision/mgs-utils/tree/v1.0.1` |

Field 7's definition is "The name of the software package as listed on the code repository", which
argues for `mgs-radio` or `mgsradio` — `MGSutils` matches no artifact in the repository at the pinned
revision. It survives because the package was renamed in 2020 (see *Durable upstream limitations*)
while the PyHC registry, which is the manually curated source and therefore sits at the top of the
metadata priority order, still lists it under the old name.

A second reason weighs for the incumbent, and it is the decisive practical one: the entry's public
page slug is already `mgsutils`, and that slug is write-once. Renaming the software would leave the
displayed name and the page address permanently disagreeing, with no way to bring them back into
line — a worse outcome for a visitor than the naming history itself.

**`mgs-radio` and `mgsradio` were therefore considered and not adopted.** Either would make the
entry title agree with what a visitor lands on when they click through to GitHub, which is the real
merit of the alternative: under `MGSutils` a visitor arrives at a repository called `mgs-radio`
containing a package called `mgsradio` and has to work out that they are in the right place. That
cost is accepted, because the fixed slug would reintroduce the same mismatch in a place that cannot
be corrected later, and because renaming would diverge from the curated registry entry.

Findability does not turn on the choice either way: the repository URL, the description, and the
keywords all carry "Mars Global Surveyor" and "radio occultation", and HSSI's search reads those.

### 8. Description (MANDATORY)

**Value:**

> Mars Global Surveyor radio occultation experiment read and plot. This software provides utilities for reading MGS radio occultation data files in .sri, .lbl, and .srt formats and creating visualizations of the occultation data. The .sri data is big-endian int16 in Fortran order. The software supports reading high-level occultation data and plotting frequency vs time spectrograms of the received signal power, from which Mars surface-echo and atmospheric properties are derived in radio occultation experiments.

**Source:** the first sentence is `setup.cfg`'s declared summary,
`description = Mars Global Surveyor radio occultation experiment read and plot`, with a sentence-final
period added — the packaging value itself carries no trailing period. The
big-endian/Fortran sentence restates `README.md`'s
``and plotting. The `.sri` data is big-endian int16, Fortran order.``; the remainder was composed by a
prior extraction.

The wording is a prior curator's and is kept as such; this refresh does not restyle it. **One
clause was repaired, on a factual gap rather than on style.** The text previously closed "to analyze
Mars atmospheric properties derived from radio occultation experiments", which names only half of
what the `.sri` products are for. Per the scope note, the SRX investigation's stated objectives are
surface-echo characterization *and* improving atmospheric occultation results, and the shipped label
notes that near `the occultation time there may be a weak surface echo racing away from` the
carrier. The old clause was not false — atmospheric occultation is an explicit objective of the
investigation — but a visitor reading it would not have learned that these are surface-reflection
products, and someone looking for Mars bistatic-radar tooling would have passed the entry by. The
repair changes only that closing clause and leaves the rest of the curator's sentences intact.

### 9. Concise Description (OPTIONAL)

**Value:**

> Mars Global Surveyor radio occultation data reader and plotter for analyzing Mars surface-echo and atmospheric properties from radio occultation experiments.

**Source:** composed by a prior extraction from `setup.cfg` and `README.md`, and repaired here in
step with Field 8. 157 characters, within the 200-character limit.

**The same factual gap was repaired here, in the same minimal way.** The text previously read
"for analyzing Mars atmospheric properties from radio occultation experiments" and carried Field 8's
omission of the surface-reflection half. The repair inserts the surface-echo half into that one
noun phrase — `Mars surface-echo and atmospheric properties`, the same wording Field 8 now uses —
and changes nothing else: the first 82 characters are identical to the previous text, and the whole
is 17 characters longer. The two fields were repaired together deliberately, because a page whose
preview and full description disagree about the science would be worse than either wording alone.

### 10. Publication Date (RECOMMENDED)

**Value:** 2014-09-15

**Source:** the first commit on the pinned revision's own history.

Verified rather than assumed: walking the ancestry of `376f0a5e231e1aed87453ce914dc31f0b81a7db3` in
reverse gives `0f57ee39fd7adf3d01b9774a473dc7f74ac78a9d`, dated 2014-09-15, "Initial commit". GitHub
independently reports the repository's `created_at` as `2014-09-15T04:22:47Z`. The date therefore
records when the software first appeared publicly, which predates the first tagged release
(2017-04-23) by more than two and a half years — that gap is expected for this field, which is about first
publication rather than first release.

### 11. Publisher (RECOMMENDED)

**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

**Source:** the DOI record, whose DataCite `publisher` is `Zenodo`.

Field 11's guidance is explicit that for software whose DOI came through the GitHub–Zenodo workflow,
Zenodo is the correct publisher rather than the repository host. Field 2 establishes that this is
such a deposit. GitHub would be the answer only if no DOI existed.

### 12. Version (RECOMMENDED)

**Latest Version:**
- **Version Number:** 1.1.0
- **Version Date:** 2020-05-04
- **Version Description:** Rename, refactor
- **Version PID:** Not found

**Source:** `setup.cfg` declares `version = 1.1.0`; the tag `v1.1.0` points at commit
`044253295a75d19e3b059eec49d50d90c6288204`, dated 2020-05-04.

**Where the Version Description comes from, settled.** The stored text `Rename, refactor` is the
GitHub Release name for `v1.1.0` — that release is named `rename, refactor`, was published on
2020-05-04, and has an empty body — carried into HSSI with a leading capital. This is worth stating
positively because the release name and the tag's own commit subject diverge: the tagged commit
`044253295a75d19e3b059eec49d50d90c6288204` is subjected `ci => actions`, and it is that commit's
parent, `d35cd2fca62495b6d754ac292591927a7fd0fa67`, which carries the subject `rename, refactor`. So
the description tracks the release rather than the tagged commit, and it does belong to 1.1.0 rather
than having been inherited from an earlier tag. A later refresh need not re-investigate it.

**Why 1.1.0 is still current at the pinned revision.** Exactly one commit separates `v1.1.0` from the
pin — `376f0a5e231e1aed87453ce914dc31f0b81a7db3`, "cleanup", 2021-03-22 — and it did not bump
`setup.cfg`. The repository is archived, so no later release can appear.

**The version is recorded as `1.1.0`, without the `v`.** That is the form the package declares for
itself — `setup.cfg` says `version = 1.1.0` — and the form packaging tools report. **`v1.1.0` was
considered and not adopted**: the git tag and the release listing both use it, and Field 12's
guidance illustrates the field with "e.g., v1.0.0", so it was a reasonable alternative. It loses
because the package's own declared version is the more authoritative statement of what the release
is called, and because the difference, while visible to a visitor beside the software name, could
not mislead anyone either way.

**Version PID stays empty, and this is a deliberate refusal rather than a gap.** Two version-level
DOIs exist for this software and neither identifies 1.1.0: `https://doi.org/10.5281/zenodo.556816`
is **v1.0.0** and `https://doi.org/10.5281/zenodo.556924` is **v1.0.1**, both deposited on
2017-04-24. Attaching either to the 1.1.0 row would assert that 1.1.0 is archived at that DOI;
anyone who followed the citation would download a 2017 release believing it to be the 2020 one.
Field 2's evidence — the concept record's own two-entry version list, plus a name-independent
creator-keyed sweep — establishes that no 1.1.0 deposit exists, and Field 2 records *why*: a GitHub
Release for `v1.1.0` was published in 2020, so this is a released-but-not-deposited gap rather than
an unreleased version, and it will not close on its own. There is nothing correct to put here. Leave
it empty.

**Release history, recorded as evidence rather than as stored values.** Three tags exist: `v1.0.0`
(2017-04-23), `v1.0.1` (2017-04-24) and `v1.1.0` (2020-05-04). A caution for any later refresh:
**`v1.0.0` and `v1.0.1` are not ancestors of the pinned revision.** They sit on a pre-rewrite lineage
of 35 and 38 commits that shares no merge base with the current 52-commit `master`, though both
lineages begin on 2014-09-15 with the same commit subjects under different hashes. The 2017 tree is
recognisably an earlier project — `README.rst` rather than `README.md`, `.travis.yml` rather than a
GitHub Actions workflow, and a package directory named `mgsutils/` rather than `mgsradio/`. So a
history walk from the pin will not find those releases, and their absence from such a walk is not
evidence that they never happened.

### 13. Programming Language (RECOMMENDED)

**Values:**
- MATLAB
- Python 3.x

**Source:** the repository's source tree at the pinned revision.

Python is the maintained implementation: `setup.cfg` declares `python_requires = >= 3.6` and the
classifier `Programming Language :: Python :: 3`, and the CI workflow builds on Python 3.8. Python
2.x is not a candidate — the floor is 3.6.

MATLAB is genuinely present: `matlab/MGSeds.m` is a self-contained 118-line
`function MGSeds(varargin)` that reads the same `.sri`/`.lbl`/`.srt` products and draws the same
`pcolor` figure without any Python involvement. Its first line is `%% USE readmgs.py INSTEAD`, so the
author regarded it as superseded, and that comment refers to a file which no longer exists at the pin
(`readmgs.py` was removed from the Python package in 2016). Kept anyway, on the visitor's-side test:
a visitor filtering HSSI for MATLAB software would land here and find working, runnable MATLAB that
does what the entry describes. Being deprecated by its own author is a caveat worth recording, not a
reason to hide the language from search. The file cites the same PDS sources as the README, in two
places: its header comment block gives the `rsdata.html`, `cumindex.tab` and `mors_1014/` links at
lines 6, 9 and 12, while the `srx.txt` specification quoted in the scope note appears separately, as
an inline comment at line 69 in the function body where the `.srt` time table is read.

### 14. Reference Publication (OPTIONAL)

**Value:** Not found — and this is an evidenced absence, not an unsearched field.

There is no `CITATION.cff`, no `codemeta.json`, and no `.zenodo.json` in the repository; the README
cites no paper; and the DOI record carries no publication among its `relatedIdentifiers` (they are
the two version DOIs, the GitHub tree URL, and the Zenodo community).

A literature check confirms it. Exact-string full-text searches for `mgs-utils`, for the DOI stem
`zenodo.595431`, and for the repository path `space-physics/mgs-radio` each return zero documents,
against a control search that returns hundreds — so the index works and the absence is real. Searches
for the bare token `mgsradio` do return three Mars radio-science papers, but they are best read as
tokenization artifacts — the words MGS and radio commonly occur adjacently in that literature — and
the exact-string searches are what settle the question either way. Both Zenodo DOIs report zero citations at DataCite, and the concept DOI's
OpenAlex record likewise shows zero.

No paper describes this software. A later refresh should not spend effort here again unless the
software itself changes.

### 15. License (RECOMMENDED)

**Value:** `Apache License 2.0`

**Source:** `LICENSE.txt` at the pinned revision is the full 176-line Apache License 2.0 text,
whose first two lines read `Apache License` and `Version 2.0, January 2004`; `setup.cfg` declares
`license_files =` with `LICENSE.txt`; `mgsradio/__init__.py` opens with the Apache boilerplate
`Licensed under the Apache License, Version 2.0 (the "License");` and the URL
`http://www.apache.org/licenses/LICENSE-2.0`. Three artifacts in the repository state the licence,
and they agree. GitHub's own detection corroborates them by reporting SPDX `Apache-2.0`, but it is
derived by reading that same `LICENSE.txt` and so is not a fourth independent source.

`Apache License 2.0` is the exact spelling of the row in HSSI's closed License vocabulary. HSSI held
no licence value for this software before this refresh, so this fills a genuine gap rather than
changing an existing choice.

**Zenodo's metadata disagrees and was deliberately not used.** The DOI record's DataCite `rightsList`
is `[{"rights": "Open Access", "rightsUri": "info:eu-repo/semantics/openAccess"}]` — an access-status
statement with no licence identifier at all — and the Zenodo API reports the deposit's licence as
`other-open`. Neither is Apache-2.0. Deposit-level licence fields of this kind are frequently the
upload default rather than the project's actual terms, and here the repository states its terms in
four places. The repository wins; the DOI metadata is recorded as a rejected source so a later
refresh does not "correct" this field back to a Zenodo value.

**No licence URI is recorded, because there is nowhere to record one.** HSSI stores a software's
licence as a reference to a shared licence row that carries its own URL; there is no per-software
licence URI. A prior version of this dossier carried a "License URI" sub-value of
`http://www.apache.org/licenses/LICENSE-2.0`; that URL is real — it is in the package docstring,
quoted above — but it is evidence, not a storable field, and it is recorded here only as evidence.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values:** `mars`, `Mars global surveyor`, `planetary`, `radio occultation`

Two further keywords, `mars-global-surveyor` and `radio-occultation`, were previously stored; this
refresh removes them, for the reason below, after the provenance of each term.

**Sources, keyword by keyword:**
- `Mars global surveyor` and `radio occultation` — these are `setup.cfg`'s two declared keywords,
  which appear there in exactly these spaced, mostly-lower-case forms.
- `mars` and `mars-global-surveyor` (the latter removed) — GitHub repository topics.
- `radio-occultation` (removed) — derived from, but **not identical to**, the third GitHub topic. The topic
  upstream is `radio-occulation`, misspelled with no "t". Whoever first populated this field silently
  fixed the typo, which was the right call: the misspelling should not be propagated into HSSI's
  shared keyword vocabulary. Recorded here because a later refresh reading GitHub's topics directly
  will otherwise see a mismatch and may "restore" the typo.
- `planetary` — the PyHC registry entry's `keywords: ["planetary","specific"]`. Its companion tag
  `specific` was correctly not imported: it is a PyHC-internal classification, meaningless as a
  science keyword to a site visitor.

**Why the two hyphenated forms were dropped.** Field 16's guidance asks for one keyword per entry,
lower case, reusing an existing row rather than minting a near-duplicate. The stored set contained
two near-duplicate pairs — `mars-global-surveyor` alongside `Mars global surveyor`, and
`radio-occultation` alongside `radio occultation` — and the duplication was visible to a visitor,
because keywords render title-cased on the entry page. The four chips read "Mars-Global-Surveyor",
"Mars Global Surveyor", "Radio Occultation" and "Radio-Occultation": the same two concepts listed
twice. Removing the hyphenated member of each pair leaves the author's own `setup.cfg`-declared
terms plus the two single-word tags, which read as science keywords — what Field 16 asks for,
"General science keywords relevant for the software (e.g., from the AGU Index List or the UAT)".

The acknowledged cost is that the hyphenated forms were the author's GitHub topics, so the removal
drops the author's own tagging vocabulary, and a visitor who types a hyphenated form may no longer
match.

Two alternatives were rejected. **Keeping all six** leaves the duplicate chips on the page and keeps
both spellings of two concepts in the shared keyword vocabulary. **Dropping the spaced pair instead**
would discard `setup.cfg`'s declared keywords in favour of repository tags, and "Radio-Occultation"
is the less natural rendering of a science term.

**The casing of `Mars global surveyor` is deliberately left alone.** Unlike hyphenation, casing is
invisible to a visitor — the title-cased rendering makes `mars` and `Mars` indistinguishable on the
page — and re-casing is not actionable in any case, since HSSI matches keywords case-insensitively
and a differently-cased entry binds straight back to the existing row.

### 17. Data Sources (OPTIONAL)

**Value:** `Observatory/Mission-specific`

**Source:** the software reads one mission's archived products and nothing else. The example files
carry `DATA_SET_ID` `"MGS-M-RSS-5-SDP-V1.0"`, `INSTRUMENT_HOST_NAME` `"MARS GLOBAL SURVEYOR"` and
`TARGET_NAME` `"MARS"`, and the format handling in `read.py` is specific to those products.

This is also the cross-listing the form calls for: Field 17's guidance says that when the source is
observatory-specific, this value should be selected and the mission named in Field 32, which is what
Field 32 does.

**`HTTP/HTTPS Directories` was considered and rejected**, and the reason should stop it being
proposed again. The README's `### Finding Data Files` section links three PDS web locations, which
makes an HTTP data source look plausible. But this field asks which sources the *software* supports,
and the software supports none: it performs no network access whatsoever (see the evidence under
Field 4). Its directory discovery is purely local — `flist = sorted(P.glob("*.sri"))`. Those links
tell a human where to point a browser before running anything. Selecting `HTTP/HTTPS Directories`
would tell a visitor filtering for HTTP-capable tools that this software can fetch its own data,
which it cannot.

The remaining rows in the 17-value vocabulary — AMDA, CDAWeb, das2, FTP/FTPS Directories, GFZ, HAPI,
Madrigal, OMNIWeb, Other, S3/Cloud-aware, SSCWeb, TAP, The Virtual Solar Observatory., VirES, WDC —
are heliophysics archives and protocols this software neither queries nor knows about.

### 18. Input File Formats (RECOMMENDED)

**Values:**
- ascii
- csv
- Other

**Source:** the three file types `read_mgs_occultation` consumes for each observation, keyed from a
single stem: `lblfn = imgfn.with_suffix(".lbl")` and `srtfn = imgfn.with_suffix(".srt")` alongside
the `.sri` image.

- **`csv`** — the `.srt` Surface Reflection Table is genuinely comma-delimited and is read as such:
  `texp = np.loadtxt(srtfn, skiprows=1, usecols=[0], delimiter=",")`, with its header line split on
  commas by `t0 = parse(srtfn.read_text().split(",")[0])`. The `.lbl` is additionally handed to a CSV
  reader with a non-comma separator, `lbl = read_csv(fn, sep="=", index_col=0, header=None)`.
- **`ascii`** — both `.lbl` and `.srt` are plain fixed-width/delimited text, PDS3 label and table
  respectively.
- **`Other`** — the `.sri` image is binary, and the FileFormat vocabulary has no binary or PDS row.
  Its eleven values are ascii, CDF, csv, FITS, HDF5, IDL.sav, ISTP-Compliant, JSON, netCDF3/4, Other
  and Zarr. The `.sri` product is a raw big-endian 16-bit array — the README states
  ``and plotting. The `.sri` data is big-endian int16, Fortran order.``, and the code reads it with
  `dtype="int16"`, `.newbyteorder("B")` and `order="F"` — so `Other` is the only honest mapping. It
  is being used here for a real format that the vocabulary does not name, which is what that row is
  for.

### 19. Output File Formats (RECOMMENDED)

**Value:** Not found — evidenced-empty.

The software writes no files at all. `plot_occultation` builds a matplotlib figure and returns
without saving it; the example script ends by calling `show()` for interactive display. A sweep of
every Python source at the pinned revision for `savefig`, `to_netcdf`, `to_csv`, `to_zarr`, `open(`
and `write` finds no file-writing call anywhere. Its output is an in-memory `xarray.DataArray` and an
on-screen figure, neither of which is a file format.

Recording any value here would be wrong rather than merely generous — a visitor filtering on output
formats is looking for software that can produce files.

### 20. Operating System (RECOMMENDED)

**Value:** `Operating System Independent`

**Source:** `setup.cfg` declares the classifier `Operating System :: OS Independent`, and the package
is pure Python with no compiled extensions and no platform-specific code paths (`pyproject.toml`'s
build requirements are only `setuptools` and `wheel`).

Note the vocabulary spelling: the HSSI row is `Operating System Independent` written out in full;
`OS Independent`, which is the classifier's own wording, is not a value in the list.

The alternative of enumerating Linux, Mac and Windows individually was considered and rejected: CI
evidence covers only Linux (`runs-on: ubuntu-latest`), so enumerating three platforms would assert
more than is tested, whereas the author's own classifier asserts platform independence and nothing in
the code contradicts it. One caveat a visitor might care about, recorded under *Durable upstream
limitations*: the software's file matching is lower-case only, which behaves differently on
case-sensitive and case-insensitive filesystems. That is a data-handling quirk rather than a porting
barrier, so it does not change this field.

### 21. CPU Architecture (RECOMMENDED)

**Value:** `CPU Independent`

**Source:** pure Python with no compiled extensions, no architecture-specific dependencies, and no
assumptions about the host's endianness — the one place byte order matters is handled explicitly in
code, `.newbyteorder("B")`, rather than inherited from the platform. Nothing in the repository would
justify naming a specific architecture from the nine available.

### 22. Related Phenomena (OPTIONAL)

**Value:** Not found — evidenced-empty, and this is a complete check rather than a skipped field.

The Phenomena vocabulary is closed and has exactly seven rows: Coronal Heating, Coronal Mass
Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission. Every one is
solar or solar-wind–driven. The software concerns Mars surface echoes and radio occultation geometry
(see the scope note) and touches none of them.

The vocabulary is flat, so there is no broader parent term to fall back on. Note also that a
phenomenon with no row belongs in Keywords, not here — but no candidate phenomenon term arises for
this software either, so nothing is being diverted to Field 16.

### 23. Development Status (RECOMMENDED)

**Value:** `Unsupported`

**Source:** the repository is archived upstream — GitHub reports `archived: true`, which makes it
read-only: it accepts no issues, no pull requests and no commits. Its last commit is the pinned
revision, 2021-03-22, and its last release is 2020-05-04. HSSI held no development status for this
software before this refresh.

The RepoStatus rows carry their repostatus.org definitions, and the choice turns on their exact
wording:

- **`Unsupported`** — "The project has reached a stable, usable state but the author(s) have ceased
  all work on it. A new maintainer may be desired." Both clauses fit. The software is stable and
  usable (three tagged releases, a passing test suite, a working library API), and archiving is the
  author's own formal declaration that all work has ceased. The second sentence reads "may be
  desired", not "is desired", so selecting this value makes no claim about whether anyone wants to
  take the project over — a distinction worth noting, because that is the main thing that could
  otherwise be read as arguing against the value.
- **`Inactive`** — rejected by its own wording: "no longer being actively developed;
  support/maintenance will be provided as time allows." An archived repository cannot receive
  maintenance at all — the mechanism for reporting a problem or offering a fix has been switched off.
  The definition promises something the repository is technically incapable of delivering. This was
  the value a prior extraction recorded in this dossier, reasoning from the `Development Status :: 4 - Beta`
  classifier and the absence of recent commits; that reasoning missed the archive flag, which is a
  stronger and more explicit signal than commit silence.
- **`Moved`** — rejected: "The project has been moved to a new location, and the version at that
  location should be considered authoritative." The repository did move once, from
  `scivision/mgs-utils` to `space-physics/mgs-radio`, but that move is complete and the destination
  *is* this record's Field 3. There is no newer authoritative location elsewhere. `Moved` would tell
  a visitor to go looking for a successor that does not exist.
- **`Abandoned`, `Suspended` and `WIP`** — each definition turns on the phrase "there has not yet
  been a stable, usable release". Three tagged releases and a published Zenodo deposit rule all three
  out.
- **`Concept`** — rejected on different wording: "Minimal or no implementation has been done yet, or
  the repository is only intended to be a limited example, demo, or proof-of-concept." The package
  has a full implementation, a test suite, and packaging metadata, and is not presented as a demo.

The `Development Status :: 4 - Beta` classifier in `setup.cfg` is not evidence against `Unsupported`:
it describes release maturity as of 2020, whereas this field describes the repository's current
development state, and the two vocabularies are unrelated.

### 24. Documentation (RECOMMENDED)

**Value:** `https://github.com/space-physics/mgs-radio`

**Source:** the repository README is the documentation. There is no documentation site, no `docs/`
directory, no ReadTheDocs configuration, and no wiki behind the repository. Field 24's guidance
covers this case explicitly: when the documentation is the access URL, enter that URL.

`README.md` does carry real installation and usage instructions — `pip install -e .` under `## Install`,
and `python PlotMGSoccult.py` under `## Example`, described as making
``makes the plots for all the `.sri`, `.lbl` pairs in the current`` directory — plus the three PDS data
links. A visitor following the link gets what they need to install the package.

**Caveat a visitor will hit:** the documented example command does not run at the pinned revision.
See *Durable upstream limitations*. The library usage the test suite exercises is unaffected. This is
recorded rather than acted on, because the field's value is still the right one — the documentation
exists at that URL and is mostly accurate.

### 25. Funder (OPTIONAL)

**Value:** Not found — evidenced-empty.

The DOI record's DataCite `fundingReferences` is empty. On the repository side the absence is
mechanical rather than impressionistic: a case-insensitive search across all tracked files at the
pinned revision for `fund`, `grant`, `award`, `acknowledg`, `NASA`, `NSF` and `sponsor` returns hits
only inside `LICENSE.txt`, and only in the Apache licence's own boilerplate ("Grant of Copyright
License", "hereby grants to You a perpetual"). There is no acknowledgements section, no funding file,
and no grant reference in the README, in `setup.cfg`, or in the package docstring, whose attribution
line reads `Copyright 2020 Michael Hirsch, Ph.D.` The usual higher-yield route for this field — a
describing publication's Acknowledgments and Data Availability Statement — is unavailable here
because no such publication exists (Field 14).

### 26. Award Title (OPTIONAL)

**Value:** Not found — evidenced-empty, on the same evidence as Field 25: the tracked-file sweep for
award and grant vocabulary turns up only Apache licence boilerplate, the DOI metadata carries no
funding references, and there is no paper whose acknowledgements could supply one.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Value:** Not found — evidenced-empty.

Field 14's literature research applies here too: nothing cites this software. Both Zenodo DOIs report
zero citations at DataCite; the concept DOI's OpenAlex record shows a `cited_by_count` of zero; and
exact-string full-text searches for the repository path and the DOI stem return nothing against a
working control.

**A tempting but wrong candidate, recorded so it is not added later.** The MGS radio occultation
literature is large — many papers analyse MGS Radio Science data, and the SRX specification itself
cites Simpson's bistatic radar work and the Tyler et al. MGS Radio Science investigation papers.
They are about the *data*, not about this reader, and the exact-string full-text searches above
return zero, so none of them can be citing it. This field is for publications tied to the software,
and Field 28 already points a visitor at the data itself.

### 28. Related Datasets (OPTIONAL)

**Values:**
- `https://doi.org/10.17189/1519757`
- `http://pds-geosciences.wustl.edu/missions/mgs/rsdata.html`
- `http://pds-geosciences.wustl.edu/mgs/mgs-m-rss-5-sdp-v1/mors_1038/index/cumindex.tab`
- `http://pds-geosciences.wustl.edu/mgs/mgs-m-rss-5-sdp-v1/mors_1014/`

**Source:** the three PDS URLs are `README.md`'s `### Finding Data Files` links, byte-for-byte as the
README writes them (`http://`, no trailing changes), and were recorded before this refresh. All
three still resolve, redirecting to their `https://` equivalents.

**The data set's own DOI leads the list, and the case for it is strong.** Field 28 asks for URLs
"ideally DOIs", and the data set the software reads has one. The NASA PDS DOI registry lists
`MGS-M-RSS-5-SDP-V1.0` → "MGS Radio Science -- Science Data Products V1.0" → `10.17189/1519757`. Its
DataCite record is published by "NASA Planetary Data System", dated 2003, typed as a Dataset, credited
to `RICHARD A. SIMPSON`, and `https://doi.org/10.17189/1519757` resolves to the PDS data set view for
`dsid=MGS-M-RSS-5-SDP-V1.0`. (The registry page and the DataCite record differ in case — DataCite
stores the title as `MGS RADIO SCIENCE -- SCIENCE DATA PRODUCTS V1.0` — which is a display artifact,
not two different data sets.) That identifier is the exact data set the software supports: the same
`DATA_SET_ID` `"MGS-M-RSS-5-SDP-V1.0"` appears in the labels shipped in `data/`, the same
`mgs-m-rss-5-sdp-v1` path appears in all three README links, and Simpson is the investigator named
both in the SRX specification and in the shipped label
(`This image was produced by Dick Simpson of the MGS Radio Science` Team). It gives a visitor a
citable, stable identifier where the three README URLs give only web locations.

**What each of the four gives a visitor**, since they are not equivalent:
- the DOI — the citable data set identifier;
- `http://pds-geosciences.wustl.edu/missions/mgs/rsdata.html` — the human landing page for MGS
  Radio Science, listing the MORS_1001–1038 volumes;
- `http://pds-geosciences.wustl.edu/mgs/mgs-m-rss-5-sdp-v1/mors_1038/index/cumindex.tab` — the
  cumulative product index across the archive. This is the finding aid the README points at, and it
  is how a user locates a particular observation, but a visitor clicking it in a "Related Datasets"
  list gets a ~6 MB raw text download rather than a page. It is kept nonetheless: the README presents
  it as one of the three ways to find data, dropping it would lose a real route, and the download
  size is a mild surprise rather than a misdirection.
- `http://pds-geosciences.wustl.edu/mgs/mgs-m-rss-5-sdp-v1/mors_1014/` — the volume containing the
  exact observation shipped in the repository. The cumulative index confirms that `data/1066m12a.*`
  is PDS product `1066M12A` from `MORS_1014`, which is precisely what the README calls
  `Example data used here`.

### 29. Related Software (OPTIONAL)

**Value:** No entries.

Six GitHub URLs were recorded here before this refresh, and none of them belongs in this field:
`https://github.com/dateutil/dateutil`, `https://github.com/matplotlib/matplotlib`,
`https://github.com/mwaskom/seaborn`, `https://github.com/numpy/numpy`,
`https://github.com/pandas-dev/pandas`, `https://github.com/pydata/xarray`.

**Five removals are the field's own rule applied, not a curator's taste.** Field 29's text excludes
the generic scientific-Python stack by name, and it names five of these six explicitly:
"numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil,
pytest, tqdm, PyYAML, click, setuptools and their peers are not related software, because listing
them says nothing that isn't equally true of most of the ecosystem." The same five are on Field 30's
Tier A never-list. That numpy, pandas, python-dateutil and xarray appear in `setup.cfg`'s
`install_requires`, and that matplotlib and seaborn are imported by `plots.py` and
`PlotMGSoccult.py` (`import seaborn as sns`) without being declared, is true and irrelevant — being a
dependency is not what this field records.

Applying the field's general test rather than only its list: each of these would be equally at home
in a web application, a finance model, or a biology pipeline, so each is generic infrastructure and
carries no information about *this* software.

**xarray belongs in Field 30 rather than here**, where the evidence actually supports it — see
Field 30. It is not a Field 29 entry: it is neither a similar-purpose tool, a predecessor, a
fork parent, a companion package, nor a domain-specific heliophysics library. A package that fails
Field 30 does not automatically land here, and a package that passes Field 30 does not belong in both.

**Nothing was found to replace them, and this was looked for.** The repository is not a fork
(`fork: false`). It names no comparable Mars radio-occultation reader, no predecessor project, and no
companion package. `matlab/MGSeds.m` is an alternative implementation of the same task, but it lives
*inside* this repository rather than being separate software, so it is Field 13 evidence and not a
Field 29 entry. Inventing a "similar tool" from general knowledge of the field would be exactly the
guesswork this dossier should prevent. An empty Field 29 is the correct outcome.

### 30. Interoperable Software (OPTIONAL)

**Value:** `https://github.com/pydata/xarray`

HSSI held no interoperable-software value for this software before this refresh, so this records a
relationship the catalogue did not previously carry.

**xarray is Tier B, which means it qualifies only with cited evidence of a specific exchange. Here is
the evidence.** The scientific data this package hands a user is an xarray object, at every point in
its public interface:

- `mgsradio/__init__.py` exports exactly two names, `from .base import loop_mgs` and
  `from .read import read_mgs_occultation`;
- `read.py`'s reader ends by constructing and returning one:
  `df = DataArray(data=data.T, dims=["time", "freq"], coords={"time": t, "freq": f})`;
- `base.py`'s `def loop_mgs(P: Path) -> tuple:` accumulates those objects and returns
  `return data, flist`;
- `plots.py` imports the type and is annotated to consume it —
  `from xarray import DataArray` and
  `def plot_occultation(data: DataArray, fn: Path, vlim: T.Sequence):` — then works through the
  labelled coordinates rather than raw arrays:
  `h = ax.pcolormesh(data.time, data.freq, data.values.T, vmin=vlim[0], vmax=vlim[1])`.

That is a documented interchange format in the field's own sense, not internal use: everything a user
receives from this package is an xarray `DataArray` with physical `time` and `freq` coordinates, and
the package's own plotting half consumes it through that interface. A user can pipe MGS
surface-reflection data straight into anything xarray-aware without writing a converter, and a
visitor filtering for xarray interoperability would be glad to learn that. The contrasting case the
field rejects — "uses xarray internally" — would be a package that built a `DataArray`, extracted
values from it, and returned a bare array; that is not what happens here.

**The bar is applied symmetrically, and MATLAB fails it.** MATLAB is also Tier B, and
`matlab/MGSeds.m` is unambiguously present. But Field 30's Tier B example is a *bridge* — "a
cross-language bridge to a named domain tool (an IDL SPEDAS or MATLAB interface)". `MGSeds.m` is not
a bridge: it is a standalone reimplementation that opens the same `.sri`/`.lbl`/`.srt` files itself
and plots them itself, with no data passing in either direction between it and the Python package. No
`.mat` is read or written, no MATLAB engine is invoked, nothing is shared but the input files. Its own
first line, `%% USE readmgs.py INSTEAD`, marks it as superseded rather than complementary. Two
programs that independently read the same archive are not interoperable with each other. MATLAB
remains correct in Field 13, where the question is what the software is written in, and wrong here,
where the question is what it exchanges data with.

**Also rejected:** the five Tier A packages listed under Field 29, on the same rule; and any blanket
claim of ecosystem or PyHC-membership interoperability, which Field 30 rules out explicitly and which
would in any case be true of hundreds of packages.

**URL choice.** The repository URL rather than xarray's Zenodo DOI, because HSSI shows the raw URL as
the link text a visitor reads, and `https://github.com/pydata/xarray` is legible where a DOI string
is not. It is also the string already present in the catalogue for xarray, so it binds to the same
entry rather than creating a second one.

### 31. Related Instruments (OPTIONAL)

**Value:** Not found — a documented omission, not an oversight, and not a judgement that the
instrument is unrelated.

**The instrument is real and the software is designed to support it.** The labels shipped in `data/`
record `INSTRUMENT_NAME` `"RADIO SCIENCE SUBSYSTEM"` with `INSTRUMENT_HOST_NAME`
`"MARS GLOBAL SURVEYOR"`, and the software parses that instrument's products specifically. This
passes the relevance gate comfortably: someone working with MGS RSS surface-reflection data would
reach for this package.

**It cannot be recorded, because HSSI's instrument vocabulary has no row for it.** The vocabulary is
SPASE-backed, and a sweep of it finds these MGS-associated instrument rows and no others:

- `https://spase-metadata.org/SMWG/Instrument/MGS/MAG` (Mars Global Surveyor Magnetometer)
- `https://spase-metadata.org/SMWG/Instrument/MGS/Ephemeris` (MGS Ephemeris)
- `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MGS/MAG` (Fluxgate Magnetometer)
- `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MGS/ER` (Electron Reflectometer)
- `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MGS/Ephemeris` (MGS Orbit)
- `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MGS/Models` (MGS : Mars crustal magnetic field analytical models)
- `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MGS/PROXY` (MGS Proxies)

Every one is a magnetometer, electron reflectometer, ephemeris, or derived-model resource. None is
the Radio Science Subsystem, and a broader sweep for instrument rows mentioning occultation or
bistatic radar finds nothing for MGS either. (Two unrelated rows named "Magallanes" carry the
abbreviation `MGS` and a `WDC_Kyoto` identifier path; they are a ground geomagnetic observatory in
Chile and must not be matched on the abbreviation alone.)

**SPASE models this instrument class for other missions but not for MGS** —
`https://spase-metadata.org/SMWG/Instrument/Voyager1/RSS` and
`https://spase-metadata.org/SMWG/Instrument/Voyager2/RSS` both exist. So the gap is specific to MGS
rather than a limitation of the vocabulary's design, and it may close if SPASE adds an MGS RSS record
and HSSI refreshes from upstream. Until then, a value here would have to be free-typed, which would
create a new identifier-less row rather than link to anything.

**The association is preserved at the observatory level instead**, in Field 32 — the substitution the
resolution guidance prescribes when an instrument has no row but its platform does. A prior version of
this dossier reached the same conclusion in 2026-06-26 after confirming the instrument against PDS
(`INSTRUMENT_ID = RSS`, PDS4 context `urn:nasa:pds:context:instrument:mgs.rss`); that finding stands
and is re-confirmed here.

### 32. Related Observatories (OPTIONAL)

**Value:**
- **Observatory Name:** `Mars Global Surveyor`
- **Observatory Identifier:** `https://spase-metadata.org/SMWG/Observatory/MGS`

**Source:** matched against HSSI's SPASE-backed observatory vocabulary; the name is the matched row's
own name.

The software is designed to support this mission and nothing else — it reads MGS Radio Science
products exclusively, its example data is a specific MGS observation, and its name and description
say so. A visitor searching HSSI for MGS software should get this back.

**Two rows carry the name "Mars Global Surveyor" and the SMWG one was chosen.** The alternative is
`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/MGS`, the same mission as modelled in the
CNES/CDPP-AMDA branch of SPASE. The SMWG row wins because SMWG is SPASE's canonical registry for
missions and observatories, whereas the CNES row exists to support that data centre's own service
holdings — its sibling instrument rows are AMDA's magnetometer, electron reflectometer, orbit,
crustal-field model and proxy products, none of which this software touches. Recording the AMDA-derived
row would associate the entry with a service catalogue it has no relationship to. The rejected
identifier is written out in full here so a later refresh recognises it as already considered rather
than as a missing second entry: the two rows are the same mission, and listing both would duplicate
the association.

### 33. Logo (OPTIONAL)

**Value:** Not found — a documented omission after looking, not an unchecked field.

There are exactly two image files tracked at the pinned revision, `tests/normal.png` and
`tests/Bifurcation.png`. Both are 560×420 8-bit RGB PNGs, and both were extracted and viewed.

Each is a scientific plot, not a mark: a dark-blue spectrogram panel with a colour bar labelled
"RX Power [dBW]", a y-axis "Baseband frequency [Hz]" running 0–2500, an x-axis "Time of Day" spanning
about seven minutes on 07-Mar-2001, and a title giving the observation's start and stop times. They
show the horizontal spacecraft carrier line and the sloping surface echo the PDS label describes.
They are, in other words, sample output — the very figures `plot_occultation` produces — and their
MATLAB-style rendering suggests they were made by `matlab/MGSeds.m`.

`README.md` line 8 does embed one of them directly beneath the title, as
`![MGS occultation bifurcation](tests/normal.png)`, which is the position a project logo would
occupy. That placement was weighed and is not sufficient: the project is not presenting the image as
its identity, it is showing the reader what the software's output looks like, and the alt text names
the physical phenomenon rather than the project. A visitor who saw this spectrogram used as the
entry's logo would read it as a data product, and it would not distinguish this entry from any other
spectrogram tool.

Nothing else is a candidate: there is no `docs/` directory or Sphinx configuration with an
`html_logo`, the PyHC registry entry for MGSutils has no `logo:` field, the repository has no
homepage set, and the Zenodo deposit carries no logo asset. No logo exists to record, and none should
be invented.

---

## Durable upstream limitations

Three findings about the software itself that a later refresh will otherwise rediscover from scratch,
and that bear on how much of the README a visitor can trust. The repository is archived, so none of
them will be fixed upstream.

**1. The documented example script cannot run at the pinned revision.** Commit `d35cd2f`
(2020-05-04, "rename, refactor") renamed the package directory `mgsutils/` to `mgsradio/` and
rewrote its internals, but left the top-level example script importing the old name.
`PlotMGSoccult.py` still begins `from mgsutils import loop_mgs` and
`from mgsutils.plots import plot_occultation`, and no module named `mgsutils` exists at the pin —
those two lines are the only occurrences of the string `mgsutils` anywhere in the tracked tree, by an
exhaustive case-insensitive search across all tracked files at that revision. So the README's
`## Example` instruction, `python PlotMGSoccult.py`, fails immediately with an import error.

CI could not have caught it, and the reason is worth recording because it explains why the defect
survived a release: `.mypy.ini` restricts type checking to `files = mgsradio/`, and the sole test
imports the new name (`import mgsradio`, then
`data, flist = mgsradio.loop_mgs(path / "data")`). Nothing in the workflow ever imports the example
script. **Library use is unaffected** — `import mgsradio` and both exported functions work correctly,
which is what the test suite exercises. Only the documented command-line entry point is broken.

**2. `matlab/MGSeds.m` points at a file that no longer exists.** Its first line is
`%% USE readmgs.py INSTEAD`. `readmgs.py` was part of the Python package until 2016, when commit
`c1336b4` ("pythonic") deleted `mgsutils/readmgs.py`; the reader has lived in `mgsradio/read.py`
since the 2020 refactor. The comment's *intent* — prefer the Python implementation — remains correct;
only the filename is stale.

**3. Data downloaded straight from PDS will not be found without renaming and re-arranging.** The
software discovers files with `flist = sorted(P.glob("*.sri"))` and derives its companions with
`imgfn.with_suffix(".lbl")` and `imgfn.with_suffix(".srt")` — lower-case extensions, all three files
expected side by side under one stem. The PDS archive does neither. Its cumulative index names these
products in upper case: searching the 6,049,650-byte `cumindex.tab` gives 3,276 rows containing
`.SRI` and none containing `.sri`, likewise 3,276 for `.SRT`. And it separates the products by type,
so the example observation appears as three rows in three directories — `SRI/1066M12A.LBL` with
`1066M12A.SRI`, `SRT/1066M12A.LBL` with `1066M12A.SRT`, and `SRG/1066M12A.LBL` with `1066M12A.SRG` —
each type carrying its own label. The repository's `data/` directory holds the same observation
pre-massaged: lower-cased and flattened into one directory as `1066m12a.sri`, `1066m12a.lbl` and
`1066m12a.srt`. On a case-insensitive filesystem the extension mismatch alone is forgiven; on a
case-sensitive one it is not, and the directory layout must be flattened in either case. The
script's own argument help acknowledges the archive's convention while the code does not:
`p.add_argument("path", help="path or filename of .SRI files", nargs="?", default="data")`.

## Distribution note

The software is not distributed on PyPI under any of its plausible names, so `pip install mgsradio`
does not work and the README's `pip install -e .` from a checkout is the only installation route it
documents. Checked against PyPI's JSON API — which is the authoritative test, because the HTML
project pages sit behind a bot gate that answers 200 even for names that do not exist — for
`mgsradio`, `mgs-radio`, `mgsutils`, `mgs-utils` and `mgs_radio`, each of which returns 404.

## Registry note

The PyHC registry lists this software in `_data/projects_unevaluated.yml`, not in the core or
community lists. The entry reads `- name: MGSutils`, `code: https://github.com/space-physics/mgs-radio`,
`description: Mars Global Surveyor radio occultation`, `contact: Michael Hirsch`,
`keywords: ["planetary","specific"]`. It is the origin of the stored `planetary` keyword (Field 16)
and of the software name currently on the record (Field 7). "Unevaluated" is PyHC's own status for
packages it has not assessed against its standards; it is not a quality judgement this dossier should
propagate into any field.
