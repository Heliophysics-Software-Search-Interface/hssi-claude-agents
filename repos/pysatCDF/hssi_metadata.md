# HSSI Metadata Extraction Results

**HSSI Software ID:** 9188840c-25ba-4ec8-b8c3-d32413aaf7a0
**Repository:** https://github.com/pysat/pysatCDF
**Source Revision:** 0d0d0fa843e26d269b17591fd27e4561bb32d40f
**Extraction Date:** 2026-09-11
**Validation Date:** 2026-09-12
**Validation Status:** PASS

---

## Scope note — how to read the evidence in this file

Two facts about this repository change how everything below should be read.

**Most of the repository is not pysatCDF.** `git ls-tree -r --name-only` at the pinned revision
returns 295 paths: 28 outside `cdf36_3-dist/` and 267 inside it. `cdf36_3-dist/` is a vendored,
unmodified copy of **NASA's CDF V3.6.3 distribution**, bundled so that installation needs no
pre-existing CDF library — `cdf36_3-dist/Welcome.txt` line 1 reads "This is the latest CDF V3.6.3
distribution package that contains everything" (the source line wraps after a trailing space).
Those 267 paths carry the overwhelming majority of the bytes: 115 `.c` files totalling 5,456,445
bytes, against 40,563 bytes of Python in 5 files. pysatCDF's own code is `pysatCDF/__init__.py`,
`pysatCDF/_cdf.py` (745 lines), `pysatCDF/fortran_cdf.f` (1,100 lines), `pysatCDF/tests/`, plus
packaging and CI files. Any measurement taken over the whole tree — language bytes, keyword greps,
licence scans — is therefore dominated by NASA's code rather than by this project's, and every
measurement quoted below states the path scope it was taken over for that reason.

**The pinned revision is the current state of the software.** `0d0d0fa` is simultaneously
`refs/heads/main`, `origin/main` and tag `v0.3.2`, dated 2022-05-12. There has been no release and
no commit on `main` since. Work continued on side branches — the most recently dated branch head,
`origin/new_version_test`, is 2024-08-29 — and maintainer triage continued into 2025, but none of it
has landed on `main` or in a release. One branch head, `origin/bug/config`, is dated 2022-05-13, a
day *after* the pinned revision; it is a side branch that was never merged, so a future agent
scanning branch dates should not read it as work on `main` after the release. So "at the pin" and
"as the software currently stands" are the same statement for this entry, and Field 23 turns on
exactly that distinction.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

pysatCDF was not submitted to HSSI by this project; the catalogue entry already exists and this
refresh amends it rather than creating it. The submitter of record is a property of the original
submission and is not re-derived here.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** `https://doi.org/10.5281/zenodo.1217180`

This is pysatCDF's Zenodo **concept** DOI, not a version DOI. Zenodo's record API reports
`conceptdoi` = `10.5281/zenodo.1217180` and `conceptrecid` = `1217180` for the v0.3.2 record
`10.5281/zenodo.6544438`; DataCite for the concept DOI lists three `HasVersion` relations
(`10.5281/zenodo.1217181`, `10.5281/zenodo.3765230`, `10.5281/zenodo.6544438`). A concept DOI is the
right choice for Field 2 because it resolves to whatever the newest release is, so this field does
not have to be re-edited at each release; the version-specific DOI belongs in Field 12's Version
PID, which is where `10.5281/zenodo.6544438` is recorded.

The choice is corroborated externally: the 2023 pysat-ecosystem paper
(`https://doi.org/10.3389/fspas.2023.1119775`) cites pysatCDF at its reference 21, which in the
publisher's rendered web full text reads "Stoneback R. A. Depew M. Klenzing J. Iyer G. Pembroke A.
Starr G. et al ( 2022 ). pysat/pysatCDF: v0.3.2 (v0.3.2). Zenodo . 10.5281/zenodo.1217180" — spacing
as the rendered HTML produces it, which differs from the PDF's typesetting. The community's own
citation of this software uses this exact DOI.

The README carries a DOI badge pointing at `https://zenodo.org/badge/latestdoi/51764432` rather than
at a literal DOI. That is a redirector, not a persistent identifier, and was not used.

### 3. Code Repository (MANDATORY)
**Value:** `https://github.com/pysat/pysatCDF`

The project moved from the personal account `rstoneback/pysatCDF` to the `pysat` organisation.
`pysat/pysatCDF` is the canonical destination, not merely a name that happens to be taken:

- GitHub's repository API reports `full_name` = `pysat/pysatCDF` with `fork` = false.
- PyPI's metadata for the `pysatCDF` distribution gives both `home_page` and
  `project_urls.Homepage` as `https://github.com/pysat/pysatCDF`, tying the published package to
  this repository rather than to the old path.
- `setup.cfg` at the pin sets `url = https://github.com/pysat/pysatCDF`.

Two stale references to the old path survive in sources and were deliberately not used: the README's
install instructions still say `git clone https://github.com/rstoneback/pysatCDF.git`, and the PyHC
community registry entry still lists `code: "https://github.com/rstoneback/pysatCDF"`. Both redirect,
but a redirect is a courtesy GitHub can withdraw, and neither is the repository's own declared URL.

### 4. Software Functionality (RECOMMENDED — treated as critical)
**Values:**
- `Data Processing and Analysis`
- `Data Processing and Analysis: Data Access and Retrieval`
- `Data Processing and Analysis: File Format Conversion`

HSSI recorded only the two children before this refresh, without their parent. In HSSI's
`FunctionCategory` graph each of `File Format Conversion` and `Data Access and Retrieval` has exactly
one parent,
`Data Processing and Analysis`, and a stored child whose parent is absent is a defect. The
classification rule is explicit — when a subcategory applies, its parent top-level category is always
included as well — and the vocabulary itself does not imply parents, so the parent has to be stored
rather than inferred. Thirteen child names in this vocabulary occur under more than one parent,
so every child here is written in the `Parent: Child` form to bind unambiguously.

**On the order these are listed in.** `softwareFunctionality` is a sorted field: HSSI stores an
order for its members, and that stored order is what the entry displays. The rendered view is not
re-alphabetised — this entry's stored sequence puts `File Format Conversion` ahead of
`Data Access and Retrieval`, and that is the order shown. The sequence these values are written in
is therefore a visible editorial choice rather than an internal detail. The two children are kept
in the relative order HSSI already held and the parent is placed after them, which leaves what a
visitor was already seeing undisturbed. The list above is alphabetical for readability and is
*not* a statement about the stored order; a later refresh comparing the two should not read that
difference as a defect, but neither should it assume the stored list can be reordered harmlessly.

**Why `File Format Conversion`.** pysatCDF's whole purpose is to turn a NASA CDF file into Python
objects. `pysatCDF/_cdf.py` exposes `to_pysat()`, whose docstring Returns block declares
"data : pandas.DataFrame, pysat.Meta", and the README's example block contains the line
"    # Export data to pysat data and metadata format". Read strictly, "file format conversion" might
be taken to mean reading one file and writing another, which pysatCDF does not do — it writes no
files at all (see Field 19). That strict reading was considered and rejected: from the site visitor's
side, someone filtering HSSI for format-conversion tools is asking "what will get my data out of
format X and into something I can work with", and a CDF-to-pandas/pysat converter is squarely a
useful answer to that question. Excluding it would hide the software from precisely the search it
most deserves to appear in.

**Why `Data Access and Retrieval`.** This one is genuinely contestable and is kept deliberately.
pysatCDF contains no networking whatsoever: a search of every `.py` and `.f` file under `pysatCDF/`
at the pin for `urllib|requests\.|ftplib|https?://|socket|download|urlretrieve` returns no files
(the identical query shape for the pattern `pysat` over the same paths returns three files, so the
instrument was working). The classification guidance glosses this category as "Downloading or
querying data from remote archives", and read that way pysatCDF fails it outright. The value is kept
on a broader reading that this dossier adopts on its own authority and that no cited source asserts:
that the category covers software through which a user obtains data they could not otherwise get
at. That reading is defensible here because it describes pysatCDF exactly: the `CDF` class is an
access layer (`cdf.data[name]`, `cdf.meta[name][attr_name]`, `cdf[name][...]`), and a heliophysicist
holding a CDF file and asking HSSI "how do I get at this data" should be shown this package. A future
agent should not remove this value on the grounds that pysatCDF cannot download — that argument has
been made and answered here. Note for context that the retrieval half of the workflow genuinely
belongs to pysat: the 2018 "Snakes on a Spaceship" survey states that "the NASA CDAWeb hosted
mission support within pysat relies upon pysatCDF", i.e. pysat fetches and pysatCDF opens.

**Considered and rejected.**
- `Data Processing and Analysis: Processing` — `to_pysat()` does restructure data (flattening 2-D
  arrays into named columns, normalising the Epoch variable's capitalisation, mapping CDF attribute
  names onto pysat metadata labels). That work is entirely in service of the conversion and is not
  offered as a separate capability, so listing it would double-count `File Format Conversion`.
- `Data Processing and Analysis: Time Series Analysis` — `to_pysat()` returns an Epoch-indexed
  `pandas.DataFrame`, but the package performs no temporal analysis of any kind. Producing a
  time-indexed container is not analysing a time series.
- `Data Processing and Analysis: Calibration` — the package reads whatever values and attributes the
  file holds and applies no instrument corrections.
- `Data Processing and Analysis: Analysis` — the catch-all analysis subcategory, and the easiest one
  to add carelessly. pysatCDF computes no derived physical quantity and performs no statistical or
  scientific calculation of any kind; it hands back exactly the values the file contains.
- `Data Processing and Analysis: Data Reduction` — nothing is averaged, binned, downsampled or
  filtered. `to_pysat()` reshapes 2-D arrays into named columns but loses no data doing so, and
  loading is all-or-nothing unless the caller excludes variables at instantiation.
- All of `Data Visualization` — a search for `matplotlib|pyplot|plotly|bokeh` across every `.py`
  file at the pin returns no files, under a query shape where the control pattern `numpy` returns
  two. There is no plotting code.
- All of `Coordinate Transforms` — no coordinate system is named or converted anywhere in the
  package's own code.
- All of `Mission-related` — pysatCDF is not part of any mission's ground system; it is a
  general-purpose library used by scientists after data release.
- All of `Models and Simulations` and `Servers and Environments` — no modelling, no server, no
  container or HPC support.

### 5. Related Region (RECOMMENDED — treated as critical)
**Values:**
- `Earth Atmosphere`
- `Earth Ionosphere`
- `Earth Magnetosphere`
- `Earth Thermosphere`
- `Interplanetary Space`

HSSI recorded `Earth Atmosphere`, `Earth Magnetosphere` and `Interplanetary Space` before this
refresh; `Earth Ionosphere` and `Earth Thermosphere` join them for the reasons below.

`relatedRegion` is a sorted field in the same way `softwareFunctionality` is, and the same caveat
applies: the alphabetical listing above is for readability, while the stored order is the order the
entry displays. The three coarser regions are kept in the relative order HSSI already held, with
the two finer ones after them, so adding them rearranges nothing a visitor was already seeing. A
difference in ordering between this file and the stored record is not a defect.

**The honest basis for this field, stated plainly.** pysatCDF implements no physics and knows
nothing about any region. Any region association it has is derived from *where the data in CDF files
comes from*, not from the code's behaviour. That could be an argument for leaving this field empty,
and it was seriously considered. It is rejected on the governing question — would a site visitor be
glad or annoyed to find this software under these regions? A researcher browsing HSSI by region is
assembling a working toolkit, and "the reader that opens the files this community's missions
distribute" is a thing they want in it. CDF is the distribution format of in-situ particles-and-
fields and ITM data at NASA's SPDF/CDAWeb — the very missions whose data populates these three
regions — so the association is informative rather than decorative. Leaving the field empty would
hide a genuinely useful tool from every region search in heliophysics.

**Why the two finer rows belong.** This vocabulary is flat: `Earth Atmosphere` does not imply
`Earth Ionosphere` or `Earth Thermosphere`, so before this refresh an ionospheric researcher
filtering at the level they actually work at would not have found pysatCDF. The ITM association is
not purely inherited from the registry, though neither corroborating source is decisive on its own
and neither states a region of operation. The 2018 "Snakes on a Spaceship" survey describes
pysatCDF as having been "developed as a stand-alone python CDF reader to
provide a streamlined user experience by developers in the ionospheric community" (quoted from the
arXiv 1901.00143v1 PDF text, main body section 3, with line wrapping joined). And the only science
data file in pysatCDF's own tree — as against the vendored `cdf36_3-dist/`, which ships 15 further
`.cdf` sample files of its own — is the test fixture
`pysatCDF/tests/test_data/cnofs_vefi_bfield_1sec_20080601_v05.cdf`, magnetic field data from the
Vector Electric Field Instrument on C/NOFS, an equatorial ionosphere/thermosphere mission. Note what
the Snakes sentence actually attributes: a *developer community*, not a domain the software operates
in. Taken together the two sources establish where pysatCDF came from and whose data it was first
pointed at, which is corroboration for the ITM association rather than proof of it; the values
ultimately rest on the format-derived reasoning above. Making the record findable at the level that
reasoning reaches is enrichment, not inflation.

**Considered and not selected.**
- `Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`, `Earth Magnetotail`,
  `Earth Magnetosheath`, `Earth Auroral Subregion` — the magnetospheric association is generic to
  the CDF format's user base, with nothing naming a specific sub-region. The coarse row is the level
  the evidence supports.
- `Solar Wind` — solar-wind data (OMNI, ACE, Wind) is indeed distributed as CDF, which would make
  this defensible on the same format-derived reasoning that justifies `Interplanetary Space`. It is
  not added because, unlike the ITM case, nothing in the repository or the literature names solar
  wind in connection with pysatCDF, and `Interplanetary Space` already carries the claim at the level
  the evidence reaches. A future agent finding direct evidence may reopen this.
- `Earth Lower and Middle Atmosphere` — the PyHC registry keyword is
  `ionosphere_thermosphere_mesosphere` and this row is the vocabulary's nearest home for the
  mesosphere. Nothing connects pysatCDF to mesospheric data specifically, and the keyword is a
  single PyHC classification bucket rather than three separate claims, so this was not added.
- The solar and planetary rows (`Corona`, `Chromosphere`, `Photosphere`, `Solar Interior`,
  `Solar Environment`, `Heliosheath`, and the per-planet magnetospheres) — solar imaging is a FITS
  domain, not a CDF one, and no planetary mission data is referenced anywhere in the repository.
- `Planetary Magnetospheres`, the generic row, deserves its own mention because it is the one place
  where the format-derived reasoning could plausibly have been stretched further: planetary in-situ
  data is distributed as CDF too. It is not added because that argument has no stopping point — it
  would end by attaching every region in the vocabulary to every CDF reader, at which point the field
  stops discriminating and stops being useful to anyone browsing by region. The three stored regions
  plus the two ITM rows are where independent evidence actually reaches.

### 6. Authors (MANDATORY)

Seven authors, in the order HSSI stores them. This set is the union of the stored HSSI authors,
`.zenodo.json` at the pin, and DataCite's `creators` for the concept DOI — all three name exactly
these seven people, and DataCite reports an empty `contributors` array, so no one is being dropped
or added. They are listed below in HSSI's stored order, which is alphabetical by family name; the
release metadata orders them differently, putting Stoneback first and then Depew, Klenzing, Iyer,
Pembroke, Starr, Reimer. `authors` is a sorted field, so that ordering is stored data and the
divergence is recorded rather than glossed. There is no `CITATION.cff` in the repository.

**Author 1 — Matthew Depew**
- Identifier: `https://orcid.org/0000-0001-9069-4998`
- Affiliation: The University of Texas at Dallas (`https://ror.org/049emcs32`)

Neither `.zenodo.json` nor DataCite supplies an ORCID for Depew; the stored identifier came from
outside those sources and is corroborated here rather than taken on trust. ORCID's public record for
0000-0001-9069-4998 has the primary name "Matthew Depew", and its sole employment is Electrical
Engineer in the **Center for Space Sciences** at the University of Texas at Dallas from 2010-12-22 —
the group where pysat and pysatCDF were written. That places the right person at the right
institution in the right years. `.zenodo.json` independently gives his affiliation as
"The University of Texas at Dallas".

**Author 2 — Gayatri Iyer**
- Identifier: `https://orcid.org/0000-0002-0229-8125`
- Affiliation: The University of Texas at Dallas (`https://ror.org/049emcs32`)

Same situation as Depew: no ORCID in `.zenodo.json` or DataCite, and in her case neither source
supplies an affiliation either — DataCite records an empty `affiliation` array. Both stored values
are corroborated by ORCID: primary name "Gayatri Iyer"; employments list Research Assistant in
"Physics - William B. Hanson Center for Space Sciences" at The University of Texas at Dallas,
2018-06-15 to 2019-05-05, before moving to Vistalytics Inc. The Hanson Center is the pysat group, and
2018–2019 is exactly the pysatCDF 0.3.0/0.3.1 development window. Her stored affiliation is therefore
better-evidenced than the release metadata, which simply omitted it.

**Author 3 — Jeff Klenzing**
- Identifier: `https://orcid.org/0000-0001-8321-6074`
- Affiliation: Goddard Space Flight Center (`https://ror.org/0171mag52`)

The stored given name is "Jeff" while both `.zenodo.json` and DataCite spell it "Klenzing, Jeffrey".
The stored form is kept: ORCID's public record for 0000-0001-8321-6074 gives the primary name
"Jeff Klenzing", so the stored spelling is the form the person themselves publishes under. This is
recorded so a later pass does not "correct" it back to the release metadata.

**Author 4 — Asher Pembroke**
- Identifier: **none recorded — deliberate omission, see below**
- Affiliation: Predictive Science (`https://ror.org/05canvq15`)

`.zenodo.json` and DataCite both give Pembroke an affiliation but no ORCID, and his HSSI Person row
carries an empty identifier. A fielded ORCID search (`given-names:Asher AND family-name:Pembroke`,
with the control `given-names:Russell AND family-name:Stoneback` returning exactly Stoneback's known
0000-0001-7216-4336) returns a single record, `0000-0002-5718-1303`, named "Asher Pembroke". It is
recorded here and deliberately **not used as his stored identifier**, for two independent reasons:

1. That ORCID record lists no employments at all, so nothing corroborates it as *this* Asher
   Pembroke beyond the name being uncommon. A unique name match is not identification.
2. Writing an ORCID onto an HSSI author whose Person row holds no identifier does not update that
   person — it resolves to a different person and leaves the original row orphaned. The correction
   is therefore unavailable through a routine metadata update even if the identity were certain.

A future agent should not re-propose this as a straightforward enrichment. If the identity is ever
confirmed from a primary source, it needs a direct database correction rather than an ordinary
metadata update.

**Author 5 — Ashton Reimer**
- Identifier: `https://orcid.org/0000-0002-4621-3453`
- Affiliation: SRI International (`https://ror.org/05s570m15`)

`.zenodo.json` and DataCite both spell this "Reimer, Ashton" and both carry this ORCID. ORCID's
record gives the primary name "Ashton Reimer", the credit name "Ashton S. Reimer", and the other
names "Ashton Reimer" and "asreimer". The stored display form matches the primary name and the
project sources; the credit name was considered and not adopted, since no project source uses the
middle initial.

**Author 6 — Gregory Starr**
- Identifier: `https://orcid.org/0000-0002-3487-3630`
- Affiliations: Boston University (`https://ror.org/05qwgg493`); Johns Hopkins University Applied
  Physics Laboratory (`https://ror.org/029pp9z10`)

Both `.zenodo.json` and DataCite spell the given name "Greg" and list one affiliation,
"The Johns Hopkins Applied Physics Laboratory". The stored record differs from both and is kept,
because ORCID supports it on both points. ORCID 0000-0002-3487-3630 has the primary name
"Gregory Starr"; its employments include Johns Hopkins University Applied Physics Laboratory from
2021; and its educations are Boston University, Electrical and Computer Engineering, BSc 2013–2017
and MSc 2018–2021. The Boston University affiliation, which appears in no release metadata, is
therefore traceable and covers the period of the 0.3.0 and 0.3.1 releases that Starr contributed to.
Keeping both affiliations is more complete than the release metadata, not less accurate than it.

**Author 7 — Russell Stoneback**
- Identifier: `https://orcid.org/0000-0001-7216-4336`
- Affiliations: Cosmic Studio; Stoneris

Stoneback is the originating author — `setup.cfg` sets `author = Russell A. Stoneback, et al.`, the
LICENSE copyright line reads "Copyright (c) 2016, Russell Stoneback", and the PyHC registry lists him
as the project contact. `.zenodo.json` and DataCite give the affiliation "Stoneris" and this ORCID.
The second stored affiliation, Cosmic Studio, appears in no release metadata but is corroborated by
ORCID, whose employments list him as CEO/Founder of Cosmic Studio from 2021, following three
successive posts at the University of Texas at Dallas — Post-Doctoral Research Associate from 2009,
Research Scientist from 2011, Assistant Professor from 2016 to 2021. Both stored
organisations are kept. Neither has a ROR identifier in HSSI, which is expected — both are small
private entities rather than registered research organisations.

**On affiliation completeness generally.** Where HSSI stores an affiliation that the release
metadata omits (Iyer, Starr's Boston University, Stoneback's Cosmic Studio), the stored value is kept
and corroborated rather than reduced to what `.zenodo.json` happens to contain. Removing a
corroborated affiliation to match a thinner source would make the record worse.

### 7. Software Name (MANDATORY)
**Value:** `pysatCDF`

Consistent across every authoritative source: the README's top-level heading is `# pysatCDF`;
`setup.cfg` declares `name = pysatCDF`; the PyPI distribution's `info.name` is `pysatCDF`; the PyHC
community registry entry's `name` is `pysatCDF`. The lower-case form `pysatcdf` appears in PyPI and
Zenodo *URLs* and in the conda recipe `meta.yaml` (`name: pysatcdf`), but those are case-normalised
package identifiers rather than the project's name — and the tree's second conda recipe,
`meta-pysatCDF.yaml`, declares the mixed-case `name: pysatCDF`, so even the packaging files are not
unanimous for the lower-case form. The DataCite title is `pysat/pysatCDF: v0.3.2`,
which is Zenodo's owner/repo-plus-tag convention for a GitHub release deposit, not a name.

### 8. Description (MANDATORY)
**Value:**

> pysatCDF is a self-contained Python reader for NASA's Common Data Format (CDF) files. It uses
> standard and extended Fortran CDF interfaces to load CDF files into Python. The package provides
> simple, robust access to CDF data and simplifies adding instruments to pysat. It includes the NASA
> CDF libraries and supports reading CDF files, accessing variable data and metadata, and exporting
> data to pysat data and metadata format.

This is the stored description, kept unchanged. It is a close synthesis of the README's own prose
rather than an editorialisation, and every clause checks out at the pin:

- "self-contained Python reader for NASA's Common Data Format (CDF) files" — README line 12 reads
  "Self-contained Python reader for NASA CDF file format".
- "uses standard and extended Fortran CDF interfaces to load CDF files into Python" — README line 14
  reads "Uses standard and extended Fortran CDF interfaces to load Common Data Format (CDF)
  files into Python." (one unwrapped source line).
- "provides simple, robust access to CDF data and simplifies adding instruments to pysat" — the
  README's Motivation section reads, across two wrapped lines, "Provide simple, robust access to CDF
  data in Python and simplify adding instruments to [pysat](https://github.com/pysat/pysat)."
- "includes the NASA CDF libraries" — the vendored `cdf36_3-dist/` tree, and the README's statement
  that actual CDF loading is performed by the NASA CDF libraries "which are included with pysatCDF".
- "reading CDF files, accessing variable data and metadata, and exporting data to pysat data and
  metadata format" — the README example block demonstrates `cdf.data`, `cdf.meta`, `cdf[name]`, and
  line 35 reads "    # Export data to pysat data and metadata format".

Rewriting it was considered and rejected: a stylistic alternative is not an improvement, and this
text is both accurate and traceable to the project's own words.

### 9. Concise Description (OPTIONAL)
**Value:** `Python reader for NASA CDF, includes CDF libraries.`

Byte-identical to the `description` field of the pysatCDF entry in the PyHC community registry
(`_data/projects.yml` on `heliophysicsPy/heliophysicsPy.github.io`). It is preferred over the
GitHub repository's own one-line description, "Python reader for NASA CDF file format", because it
adds the single most practically important fact about the package — that the NASA CDF libraries ship
with it, so there is nothing to install first — within the same length. Kept unchanged.

### 10. Publication Date (RECOMMENDED)
**Value:** `2016-02-21`

**HSSI recorded `2016-02-15` for this field before this refresh, and the reason it was wrong
matters.** 2016-02-15 is the date GitHub's repository API reports as `created_at` — the day the
repository was created, not the day any version of the software was published. The form defines this
field as the date of first broadcast/publication and directs that it be used for the
**initial version** of the software. On
2016-02-15 there was no version: the first commit on the pinned lineage,
`2c823b5eac37eb416e77d43d0955d587b9fe89d9`, is dated 2016-02-15 and is followed by seven more commits
the same day with messages including "Disabled broken portion of setup.py" and "setup.py now works,
except for path detection of CDF_LIB". Version numbering begins with `0.1`, whose earliest file upload
on PyPI is timestamped 2016-02-21T06:10:47Z. That is the first moment pysatCDF existed as a published,
installable version, and it is the value recorded here.

PyPI is the only record of the initial version. The earliest git tag is `v0.1.2` (2016-03-11) and the
earliest GitHub release is likewise `v0.1.2`; PyPI's `0.1` (2016-02-21) and `0.1.1` (2016-02-25) have
no corresponding tag or release. Zenodo is no help either — the Zenodo archive of this project begins
at version 0.3.0 in 2018, so its earliest date long post-dates first publication.

**Alternative considered and rejected.** Treating the making-public of the GitHub repository as the
"publication" is a coherent reading, and is presumably how 2016-02-15 was originally derived. It is
rejected because the form's second sentence disambiguates it — "Used for the initial version of the
software." — and a repository creation date is not attached to any version. From a site
visitor's side, a catalogue's publication date answers "when did this software first come out",
and the answer is the day the first release was downloadable.

### 11. Publisher (RECOMMENDED)
**Value:** Zenodo — `https://zenodo.org`

The form is explicit that for software whose DOI was obtained through the GitHub–Zenodo workflow,
Zenodo is the correct publisher. That this DOI came from that workflow rather than from a manual
deposit is provable rather than assumed: the Zenodo record for v0.3.2 carries the related identifier
`{"identifier": "https://github.com/pysat/pysatCDF/tree/v0.3.2", "relation": "isSupplementTo",
"scheme": "url"}`, which is the tree-URL supplement relation that the GitHub integration writes
automatically on a release, and the record was created 2022-05-12T19:51:51Z — four seconds after the
GitHub release `v0.3.2` was published at 2022-05-12T19:51:47Z. DataCite's `publisher` field for the
concept DOI is likewise "Zenodo". Kept unchanged.

### 12. Version (RECOMMENDED)

**Version Number:** `v0.3.2`
**Version Date:** `2022-05-12`
**Version PID:** `https://doi.org/10.5281/zenodo.6544438`
**Version Description:** (HSSI held an empty description for this version before this refresh)

> New Features: compatible with pysat v3.0+. Documentation: added pull request templates and other
> GitHub project documentation; switched Windows installation instructions to favor installing WSL.
> Bug Fix: improved builds for newer compilers; replaces uninterpretable characters with '*' so data
> loading may continue. Maintenance: adopted latest pysat development standards; shifted from
> TravisCI to GitHub Actions for online testing; adopted setup.cfg; improved PEP8 compliance.

**Why `v0.3.2` with the leading `v`.** Sources disagree on the prefix and the stored form follows the
release, not the package. The git tag is `v0.3.2`, the GitHub release's `tag_name` and `name` are both
`v0.3.2`, and DataCite's `version` is `v0.3.2`; `pysatCDF/version.txt` at the pin contains `0.3.2` and
PyPI's `info.version` is `0.3.2`. Since the Version PID identifies the Zenodo deposit of the GitHub
release, the release's own spelling is the consistent choice. Kept unchanged. One presentation
caveat: HSSI's read API renders this version as the software name joined to the number, so a
displayed "pysatCDF - v0.3.2" is a rendering of the stored `v0.3.2` and must not be mistaken for the
stored value or copied back into it.

**Why 2022-05-12 and not 2022-05-13.** Four independent sources agree on 2022-05-12: the tag's creator
date, the GitHub release's `published_at` (2022-05-12T19:51:47Z), Zenodo's `publication_date`, and the
PyPI upload of `0.3.2` (2022-05-12T19:46:37Z). Only `CHANGELOG.md` disagrees — its single heading reads
`[0.3.2] - 2022-05-13`, a day later. That is a hand-written date in a file edited before the release
was cut, and it loses to four machine-generated timestamps. The discrepancy is recorded here so a
later pass does not "correct" the stored date to match the changelog.

**Why this description, and why it is correctly scoped.** `CHANGELOG.md` at the pin contains exactly
one version heading, `[0.3.2] - 2022-05-13`, so the entire changelog describes this release and
nothing else — there is no risk of the description spanning a wider range than the version it is
attached to. The GitHub release body for `v0.3.2` and DataCite's `Abstract` description for the
concept DOI carry the same content, but they are not independent corroboration: the release body is
the changelog entry pasted in, and the DataCite abstract is that body with the markdown stripped —
one source seen three times. The description recorded above is a reflowed rewrite of it rather than a
transcription, which is appropriate for a prose field. The release's `name` was checked as well as
its body, in case it carried a summarising title the way earlier releases do (`0.3.1` is named
"pysat Compatibility"; `0.3.0` is named "Windows compatibility and improved pysat meta handling";
`0.2.4` is "CDF Update"); for `v0.3.2` the `name` is
just the tag string, so there is no title to fold in. The changelog's empty "Deprecations" bullet is
omitted because it lists nothing.

**A platform limitation worth knowing before touching this field again.** Supplying a version
description through HSSI's API does not edit the existing version record in place. The submitted
version — number, date, description and PID together — is stored as a fresh version record, and the
software entry is repointed at it; the record that was there before is left behind, no longer
referenced by anything. This is accepted here because it is the only available route to giving the
version a description at all, but a later refresh should know it rather than rediscover it: every
edit to any part of Field 12 has this effect, so the field is worth changing deliberately and rarely
rather than incidentally.

**Version PID.** `10.5281/zenodo.6544438` is the version-specific DOI; DataCite lists it as one of
three `HasVersion` children of the concept DOI in Field 2, and Zenodo's record for it reports
`version` = `v0.3.2`. Kept unchanged. Note that this is the field that should carry a version DOI —
Field 2 correctly carries the concept DOI instead.

### 13. Programming Language (RECOMMENDED)
**Values:** `C`, `Fortran77`, `Python 3.x`

**The criterion, settled once.** The form asks for "the most important languages" and states that
this "is not meant to be an exhaustive list". Importance here is read as: *a language a user or
contributor must actually confront in order to install, use, or modify this software.* Every
inclusion and exclusion below derives from that single test, and from nothing else — in particular
not from byte counts, which for this repository measure NASA's vendored distribution rather than
pysatCDF.

- **Python 3.x** — the entire user-facing API. `setup.cfg` sets `python_requires = >= 3.5` and
  declares classifiers for Python 3.8, 3.9 and 3.10; CI at the pin runs 3.8, 3.9 and 3.10. There is
  no Python 2 support at the pin (`Python 2.x` exists in the vocabulary and was not selected;
  `_cdf.py` retains `from __future__ import print_function` as a legacy artefact, which is not
  support).
- **Fortran77** — not incidental: the Fortran layer is what distinguishes pysatCDF from every other
  Python CDF reader. `pysatCDF/fortran_cdf.f` is the f2py-wrapped bridge to the NASA C library, and
  the package docstring in `pysatCDF/__init__.py` states that pysatCDF "uses NASA's C library to do
  the actual loading and couples Python to this library via an intermediate Fortran layer" (two
  wrapped source lines). The dialect is F77 specifically, and the repository says so twice: the file
  is fixed-form with column-1 `C` comments, and `setup.py` line 194 passes
  `extra_f77_compile_args=['--std=legacy'],`. A contributor cannot avoid it, and a user cannot
  install without a Fortran compiler — the README devotes a section to installing `gcc` via brew on
  macOS for exactly this reason. `Fortran90`, `Fortran 2003`, `Fortran 2008` and `Fortran 2023` all
  exist in the vocabulary and are wrong: the source is fixed-form F77 compiled with a legacy standard
  flag.
- **C** — the NASA CDF library bundled in `cdf36_3-dist/` (115 `.c` files, 5,456,445 bytes, plus 36
  `.h` files; a case-insensitive match gives 116 and 5,458,576, the extra being
  `cdf36_3-dist/src/definitions/definitions.C`, whose uppercase extension conventionally denotes
  C++) is compiled from source during `pip install`; a failure to build it is a failure to
  install pysatCDF. A user debugging an installation is debugging a C build. It is included even
  though pysatCDF's authors did not write it, because the test is what a user must confront, and this
  is unavoidable.

**Excluded, each for a stated reason.**
- **Java** — `cdf36_3-dist/cdfjava/` contains 2 `.java` files (68,507 bytes) and 3 `.jar` files, but
  `MANIFEST.in` at the pin contains the line `prune cdf36_3-dist/cdfjava`, and `setup.py` builds only
  the C library and the Fortran extension. The Java API ships in the upstream NASA tarball and is
  excluded from the distribution; no user or contributor to pysatCDF ever touches it.
- **Shell / Batch** — `build.sh` is a single line, `python setup.py install`, and `bld.bat` is its
  two-line Windows equivalent. These are conda-recipe glue, not a language anyone works in. (Neither
  has a row in the `ProgrammingLanguage` vocabulary in any case.)
- **C++, PHP, NASL, Brainfuck, Roff, Makefile** — GitHub's language API for this repository reports
  all of these. They are misclassifications of files inside the vendored NASA distribution; PHP,
  NASL and Brainfuck in particular are plainly artefacts of GitHub's heuristics applied to C sources
  and build fragments. The GitHub language breakdown was therefore not used as evidence for this
  field, and a future agent should not reintroduce entries from it.

### 14. Reference Publication (OPTIONAL)
**Value:** None — documented absence.

There is no publication whose subject is pysatCDF. This was tested rather than assumed, and the
negative result is worth recording because pysatCDF sits close to three papers that are *about*
neighbouring things:

- `https://doi.org/10.1029/2018JA025297`, "PYSAT: Python Satellite Data Analysis Toolkit"
  (Stoneback, Burrell, Klenzing & Depew, *JGR Space Physics* 123, 5271, 2018) — its subject is pysat.
  pysatCDF appears in it, but in the **acknowledgements**, listed among software resources used, not
  as the paper's topic.
- `https://doi.org/10.1029/2018JA025877`, "Snakes on a Spaceship—An Overview of Python in
  Heliophysics" (Burrell et al., *JGR Space Physics* 123, 10,384, 2018) — a community survey. Its
  appendix section A.3.3 is a one-paragraph description of pysatCDF, which makes it the most
  substantial published account of the package, but the paper's subject is the Python heliophysics
  ecosystem as a whole.
- `https://doi.org/10.3389/fspas.2023.1119775`, "The pysat ecosystem" (Stoneback, Burrell, Klenzing &
  Smith, *Frontiers in Astronomy and Space Sciences* 10, 2023) — its subject is pysat and its
  penumbra packages collectively.

None of these is "the publication describing the software" in Field 14's sense, and none is offered
by the project as pysatCDF's preferred citation. What the project offers instead is the Zenodo DOI:
the README's citation badge resolves to Zenodo, there is no `CITATION.cff` at the pin, and when the
2023 ecosystem paper cites pysatCDF it cites `10.5281/zenodo.1217180`. All three papers are recorded
in Field 27, which is where publications that cite or use the software belong. A future agent should
not promote the pysat paper into this field: a paper about the framework is not a paper about the
reader.

### 15. License (RECOMMENDED)
**Value:** `BSD 3-Clause "New" or "Revised" License`

`LICENSE` at the pin is a BSD licence with three enumerated conditions, set as `*` bullets rather
than numbers, the third of which reads
"* Neither the name of pysatCDF nor the names of its" (the clause's first source line, continuing
across the two that follow with "contributors may be used to endorse or promote products derived
from this software without specific prior written permission."). That third clause is precisely
what separates BSD-3-Clause from BSD-2-Clause, so the near-match vocabulary row
`BSD 2-Clause "Simplified" License` is ruled out on content, not on name. GitHub's licence detector
independently reports `spdx_id` = `BSD-3-Clause` for this repository, and `setup.cfg` declares the
classifier `License :: OSI Approved :: BSD License`.

**The licence history was read by content, not assumed constant.** Only two commits in the pinned
lineage have ever touched `LICENSE`: `fed5acee4b72fc4fa741956c12c3d806205bb687` (2018-09-13, "Added
license") and `a3b3799e484f910d32320cdb131f2240bcbda7d0` (2018-09-13, "Update LICENSE"). The diff
between them changes exactly one line — the third clause's project name, from "pysat" to "pysatCDF" —
and the file has been byte-identical from `a3b3799e` to the pin. So pysatCDF has been BSD-3-Clause
for the whole period in which it has had a licence file at all, and the only edit ever made was
correcting a copy-paste of pysat's licence. Releases 0.1 through 0.3.0 predate the licence file.

**A contradicting source, deliberately overruled.** Zenodo's record for v0.3.2 gives
`"license": {"id": "other-open"}`, not a BSD identifier. Zenodo's licence field is populated from the
depositor's settings rather than from the repository's `LICENSE` file and is a known source of
inaccurate values; the file in the repository governs. Recording `Other` here to match Zenodo would
be strictly worse for a site visitor filtering by licence.

**Bundled third-party licence, not this software's licence.** `cdf36_3-dist/CDF_copyright.txt` carries
NASA/GSFC Space Physics Data Facility's own terms ("This software may be copied or redistributed as
long as it is not sold for profit…", two wrapped source lines). Those govern the vendored CDF
distribution, not pysatCDF, and Field 15 takes a single value describing the software itself. The
existence of the bundled NASA terms is noted here so a future agent understands why a licence scan
over the whole tree returns two different licences.

Field 15 in HSSI is a reference to a shared licence row and carries no per-software licence URI, so
the SPDX URL is not recorded as a value; it is `https://spdx.org/licenses/BSD-3-Clause.html` for
reference.

### 16. Keywords (OPTIONAL)
**Values:**
- `cdf`
- `common data format`
- `ionosphere thermosphere mesosphere`
- `magnetosphere`
- `nasa cdf`
- `pysat`
- `python`
- `python reader`

Values are recorded as stored row names, which are lower-case; HSSI's read API title-cases keywords
for display, so a rendered "Nasa Cdf" is a presentation artefact and not the stored value.

**The four already-stored technical keywords are the GitHub repository topics**, transliterated from
hyphens to spaces: the repository's `topics` are `cdf`, `nasa-cdf`, `python`, `python-reader`. These
are the project's own chosen search terms and are kept unchanged.

**Why `pysat`.** pysat is not incidental to pysatCDF; it is the reason the package exists. The
README's Motivation section gives the purpose as providing access to CDF data "and simplify
adding instruments to [pysat](https://github.com/pysat/pysat)." (two wrapped source lines);
`to_pysat()` is the package's flagship export; `pysat` is a hard, unconditional module-level import
in `_cdf.py`; and the project declares
`pysat` among its own keywords: `setup.cfg` lists `CDF`, `NASA`, `pysat` and `pandas` under
`keywords =`, which PyPI publishes as `CDF,NASA,pysat,pandas`.
The 2023 ecosystem paper describes pysatCDF as one of the "pysat penumbra packages". A site visitor
searching HSSI for "pysat" is looking for exactly this family of tools and should find this one.

**Why `common data format`.** "CDF" is an acronym with heavy collisions, and a visitor who
searches the expanded phrase — which is how the format is named in the README's own line 14, in
`setup.cfg`'s description `'Simple NASA Common Data Format (CDF) File reader.'`, and in the class
docstring "Reads data from NASA Common Data Format (CDF) files." — would otherwise miss a package
whose entire subject is that format. The stored `cdf` and `nasa cdf` rows do not cover the
spelled-out phrase.

**The two PyHC domain keywords are kept, with their basis stated.** `ionosphere thermosphere
mesosphere` and `magnetosphere` entered the record from the PyHC community registry, whose entry for
pysatCDF carries `keywords: ["ionosphere_thermosphere_mesosphere","magnetosphere","specific"]`.
An inherited registry classification is not by itself a reason to keep a keyword, so each was
re-tested:

- `ionosphere thermosphere mesosphere` is **earned independently of the registry**. The 2018 Snakes
  survey states that pysatCDF "was developed as a stand-alone python CDF reader to provide a
  streamlined user experience by developers in the ionospheric community" (arXiv 1901.00143v1 text,
  main body section 3, with line wrapping joined), and the only science data file in pysatCDF's own
  tree is a day of C/NOFS VEFI magnetic field data — an equatorial ionosphere/thermosphere mission.
  (The vendored `cdf36_3-dist/` ships 15 further `.cdf` samples, which are NASA's demonstration data
  and say nothing about pysatCDF.)
- `magnetosphere` has **no source outside the registry**. It is nonetheless kept, on the same
  format-derived reasoning set out in Field 5: CDF is how magnetospheric mission data is distributed,
  and a magnetospheric researcher who searches for it will want the reader that opens those files.
  Removing it while keeping `Earth Magnetosphere` in Field 5 would leave the record internally
  inconsistent on identical evidence. This is a judgement call and is recorded as one.

The registry's third keyword, `specific`, is a PyHC-internal scope marker rather than a subject term
and is correctly absent.

**Considered and not added.**
- `pandas` — declared in `setup.cfg`'s own keyword block, and `to_pysat()` does return a
  `pandas.DataFrame`. Not added: it names generic infrastructure rather than this software's subject,
  and as a search term it would put pysatCDF in front of visitors who are not looking for it.
- `nasa` — a row exists, but `nasa cdf` is already stored and is strictly more informative; the bare
  term would add reach without adding meaning.
- `istp` — a row exists, and `to_pysat()`'s metadata-label defaults are the ISTP/CDAWeb attribute
  names. The claim is real but belongs in Field 18, where it is recorded as an input format; making
  it a keyword as well would assert the same thing twice.
- `fortran` — the Fortran bridge is genuinely distinctive, but Field 13 already carries it and it is
  an implementation detail rather than a subject a visitor would search on.

## Section 2: Additional Data

### 17. Data Sources (OPTIONAL)
**Value:** None — evidenced absence, not an unexamined blank.

pysatCDF never touches the network. A search of every `.py` and `.f` file under `pysatCDF/` at the
pin for the pattern `urllib|requests\.|ftplib|https?://|socket|download|urlretrieve` matches no
files; the same query shape over the same paths for the control pattern `pysat` matches three files
(`__init__.py`, `_cdf.py`, `tests/test_cdf.py`), so the search could have found a positive had one
existed. The public API takes a local filename — `pysatCDF.CDF(filename)` — and nothing else. There
is no downloader, no archive client, no credential handling and no URL anywhere in the package's own
source.

Every row in HSSI's `DataInput` vocabulary except the catch-all `Other` names a remote service or
access protocol — `AMDA`,
`CDAWeb`, `das2`, `FTP/FTPS Directories`, `GFZ`, `HAPI`, `HTTP/HTTPS Directories`, `Madrigal`,
`Observatory/Mission-specific`, `OMNIWeb`, `Other`, `S3/Cloud-aware`, `SSCWeb`, `TAP`,
`The Virtual Solar Observatory.`, `VirES`, `WDC` — and pysatCDF connects to none of them. The
emptiness of this field is therefore a fact about the software, and that is why the vocabulary is
enumerated here rather than merely referenced.

**`CDAWeb` was specifically considered and rejected.** pysatCDF is overwhelmingly used on files that
came from CDAWeb, and `to_pysat()`'s defaults are tuned to CDAWeb's conventions. But reading a file
that an archive produced is not being a client of that archive. The division of labour is stated in
the 2018 Snakes survey, whose section A.3.3 records that "the NASA CDAWeb hosted mission support
within pysat relies upon pysatCDF" (arXiv 1901.00143v1 text, two wrapped lines): pysat does the
fetching, pysatCDF does the opening. A visitor filtering HSSI for CDAWeb clients wants tools that
will go and get data for them, and would be misled by finding a library that cannot.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- `CDF`
- `ISTP-Compliant`

**`CDF`** is the whole point of the package and needs no argument; `pysatCDF/_cdf.py`'s `CDF` class
docstring opens "Reads data from NASA Common Data Format (CDF) files." and the reader supports the
full set of CDF data types including `epoch`, `epoch16` and `TT2000`.

**`ISTP-Compliant`** belongs here because pysatCDF's conversion path is built around the ISTP/CDAWeb
metadata convention rather than around bare CDF. The `to_pysat()` signature at the pin defaults every
metadata label to an ISTP variable attribute — `units_label='UNITS'`, `name_label='LONG_NAME'`,
`fill_label='FILLVAL'`, `plot_label='FIELDNAM'`, `min_label='VALIDMIN'`, `max_label='VALIDMAX'`,
`notes_label='VAR_NOTES'`, `desc_label='CATDESC'`, `axis_label='LABLAXIS'` — and its docstring names
the source of those defaults repeatedly, e.g. line 592, "            Identifier within metadata for
units. Defults to CDAWab standard." (the two misspellings are in the source). A visitor filtering for
software that reads ISTP-compliant files should find this one: on an ISTP-compliant CDF, `to_pysat()`
works with no configuration at all.

The addition is a claim about defaults, not about a restriction. Every label is a keyword argument,
so pysatCDF reads non-ISTP CDFs perfectly well once told where the metadata lives; the docstring's
own Note says "The *_labels should be set to the values in the file, if present." Both rows are
therefore correct together, and `CDF` is not made redundant by `ISTP-Compliant`.

**Not selected.** `ascii`, `csv`, `FITS`, `HDF5`, `IDL.sav`, `JSON`, `netCDF3/4`, `Zarr`, `Other` —
the package has exactly one reader and it is the NASA CDF library. Note in particular that HDF and
netCDF support in this ecosystem lives elsewhere: the 2023 ecosystem paper assigns CDF support to
pysatCDF and HDF support to pysatMadrigal, while pysat itself handles netCDF.

### 19. Output File Formats (RECOMMENDED)
**Value:** None — **HSSI recorded `Other` for this field before this refresh.**

**pysatCDF writes no files of any kind.** The form defines this field as the formats the software
supports "for generated files" and directs that "Only formats actually supported should be
indicated." A search of `pysatCDF/_cdf.py` and `pysatCDF/__init__.py` at the pin for
`\bopen\(|to_csv|to_netcdf|savefig|\.write\(|np\.save|pickle` returns exactly two hits, and neither
is an output path: `__init__.py` line 15 opens `version.txt` to read the package version, and
`_cdf.py` line 45 calls `fortran_cdf.open(name)`, which opens a CDF for **reading**. The Fortran
layer confirms it from the other side — `pysatCDF/fortran_cdf.f` declares 27 subroutines, every one
of which is an open, close, inquire, status or `get_*` routine; there is no `put`, `write` or
`create` among them. The vendored NASA distribution does contain a full write-capable CDF library,
but pysatCDF exposes none of it.

What pysatCDF produces is in-memory Python objects: `cdf.data` and `cdf.meta` dictionaries, and from
`to_pysat()` a `pandas.DataFrame` plus a `pysat.Meta`, as its docstring's Returns block declares
("data : pandas.DataFrame, pysat.Meta"). Those are not file formats.

**Why `Other` is not a defensible way to say that.** `Other` in this field asserts that the software
generates files in some format the vocabulary does not list. That is false, and it is misleading in a
specific way: a visitor filtering Output File Formats is asking "what can this produce for me", and a
package that appears under any output format implies it can write something. An empty Output File
Formats field alongside a populated Input File Formats field communicates the truth — this is a
read-only library — far better than `Other` does. Recording the field as empty is the accurate
outcome, not a gap.

### 20. Operating System (RECOMMENDED)
**Values:** `Linux`, `Mac`, `Windows`

All three are declared by the package and implemented in the build, though not equally:

- `setup.cfg` declares the classifiers `Operating System :: POSIX :: Linux`,
  `Operating System :: MacOS :: MacOS X` and `Operating System :: Microsoft :: Windows`.
- `setup.py` branches on `sys.platform` with a distinct configuration for each of `darwin`
  (`os_name = 'macosx'`), `linux`/`linux2` (`os_name = 'linux'`, `env_name = 'gnu'`) and `win32`
  (`os_name = 'mingw'`, `env_name = 'gnu'`), and raises `ValueError` with the message
  'Unknown platform, please set setup.py parameters manually.' on anything else.
- The README states that pysatCDF "has been tested on Mac OS X and Ubuntu 15.04. Support is included"
  (one wrapped source line) "for building on windows via Windows Subsystem for Linux."

**The Windows caveat, recorded so it is not mistaken for an error.** The README's recommended Windows
route is WSL — "Install the Windows Subsytem for Linux and proceed as per POSIX installation." (the
misspelling is in the source) — and the 0.3.2 changelog records that the project "Switched Windows
installation instructions to favor installing WSL." A native Windows path nonetheless exists in
`setup.py` via mingw, and the conda recipe `meta.yaml` carries Windows-only build requirements
(`m2-make`, `m2w64-toolchain`, `m2w64-gcc`, all marked `# [win]`), so Windows is a genuinely declared
target rather than an aspiration. Kept.

**Not selected.** `Operating System Independent` is wrong for the same reason `CPU Independent` is
wrong in Field 21 — installation compiles a C library and a Fortran extension against the host
platform. `Solaris` appears in the vendored NASA distribution's build matrix
(`cdf36_3-dist/Note.solaris`) but `setup.py` has no Solaris branch and would raise on it.
`MobilePlatform` and `Other` have no basis.

**Only Linux is actually tested.** The CI workflow at the pin runs `os: [ubuntu-latest]` for Python
3.9 and 3.10 plus a Python 3.8 / numpy 1.19 entry, all on ubuntu. macOS and Windows support rests on
the build configuration and the README, not on continuous testing. That is a limitation worth knowing
but not a reason to drop the values — the support is declared and implemented.

### 21. CPU Architecture (RECOMMENDED)
**Value:** `x86-64` — **HSSI recorded `CPU Independent` alongside it before this refresh.**

`x86-64` is well evidenced. `setup.py` line 48, inside the `if platform == 'darwin':` branch, reads
`    env_name = 'x86_64'` — the macOS build hard-codes the CDF library's x86_64 environment with no
architecture detection, and that `ENV` value selects the vendored Makefile's macOS x86_64 profile,
whose compile options at `cdf36_3-dist/Makefile` line 331 are
`COPTIONS_macosx_x86_64=-mmacosx-version-min=10.4 -arch x86_64 -arch i386 -Di386 -D__MACH__ -D_FILE_OFFSET_BITS=64 -D_LARGEFILE64_SOURCE -D_LARGEFILE_SOURCE -O2`.
On macOS, pysatCDF builds an x86_64/i386 CDF library and nothing else.

**Why `CPU Independent` does not survive.** "CPU Independent" says the software runs wherever its
runtime does, with no architecture concern. pysatCDF is the opposite case: installing it compiles
5.4 MB of C into a static library and f2py-compiles a Fortran extension against it, and the macOS
path is pinned to an architecture in the build script. Holding `CPU Independent` and `x86-64`
simultaneously is not a hedge, it is a contradiction — and it is the harmful direction of a
contradiction, because a visitor filtering for CPU-independent software is filtering for "this will
just work on my machine", which is precisely the promise pysatCDF cannot make. The pure-Python layer
being portable is not the test; what the user must build is.

**Why no arm64 row belongs here.** A search of every tracked file at the pin — binary blobs included,
which `git grep` does scan and report — for
`aarch64|arm64|apple silicon` matches nothing, under a query shape where the control pattern
`x86_64` matches ten files, including `cdf36_3-dist/Makefile` (18 occurrences) and `setup.py`. The vendored
Makefile has an `all.macosx.x86_64` target and no arm64 equivalent, and the repository's issue
tracker contains no report mentioning Apple Silicon, M1, arm64 or aarch64. So `Apple Silicon arm64`
is unsupported as far as any evidence goes, and `Linux aarch64 or arm64` is merely *unevidenced*
rather than excluded — the Linux branch selects `ENV=gnu`, which is compiler-keyed rather than
architecture-keyed (`CC_linux_gnu=gcc`, with no `-m64`/`-march` flag), so a Linux arm64 build is not
structurally prevented. It is simply never tested (CI is ubuntu x86-64) and never claimed, so it is
not recorded. A future agent finding an arm64 build report may add it.

**Not selected:** `GPU`, `HPC or HEC`, `ppc64le`, `Sun (SPARC)`, `Other` — no evidence for any.

### 22. Related Phenomena (OPTIONAL)
**Value:** None — evidenced absence.

HSSI's `Phenomena` vocabulary has seven rows: `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`, `X-ray emission`. pysatCDF
neither detects, models, catalogues nor analyses any of them, and none is named anywhere in its
source, documentation or release notes. The package operates strictly below the level at which
phenomena exist: it turns bytes in a file into arrays, and has no concept of what those arrays
measure. The vocabulary is enumerated here because that enumeration *is* the evidence — every
available value was tested against the software and none applies — and so a future agent can see the
field was examined rather than skipped.

Note also that this vocabulary is flat, so nothing in Field 5's regions implies a phenomenon here.

### 23. Development Status (RECOMMENDED)
**Value:** `Inactive` — **HSSI held no value for this field before this refresh.**

HSSI's `RepoStatus` rows carry the repostatus.org definitions, and `Inactive` reads: "The project has
reached a stable, usable state but is no longer being actively developed; support/maintenance will be
provided as time allows." Both halves of that sentence are separately true of pysatCDF.

*Stable and usable:* `setup.cfg` declares `Development Status :: 5 - Production/Stable`; the package
has had eighteen PyPI releases since 2016; the current release installs, is tested in CI, and is the
CDF backend the pysat ecosystem depends on.

*No longer actively developed:* the pinned revision is simultaneously `main`, `origin/main` and tag
`v0.3.2`, dated 2022-05-12, and there has been no commit on `main` and no release of any kind since.
Two pull requests remain open — #36 from 2022-04-26 and #50 from 2024-08-29 — alongside 15 open
issues. (GitHub's `open_issues_count` field reports 17 for this repository because it counts issues
and pull requests together; the two figures are not in conflict.)

*Support as time allows:* the maintainers have not walked away. Branch work continued after the last
release (`origin/new_version_test` is dated 2024-08-29, `origin/46-maint-numpy-124-compliance`
2023-03-03, `origin/develop-3` 2022-12-05), and pull request #47 was triaged and closed on
2025-08-26. The repository is not archived — GitHub reports `archived` false and `disabled` false —
and there is no deprecation notice anywhere in the tree or the issue tracker.

**The alternatives, each ruled out against its own definition.**
- `Active` ("being actively developed") — contradicted by four years with no release and no commit on
  the default branch. GitHub's `updated_at` field (2026-07-18) must not be read as development
  activity; it advances on stars, metadata edits and similar events. The repository's `pushed_at` is
  2024-10-30, and even that reflects pushes to side branches rather than to `main`.
- `Unsupported` ("the author(s) have ceased all work on it") — contradicted by the 2025 pull-request
  triage and the 2024 branch work. The campaign treats an archived repository as `Unsupported`; this
  one is not archived.
- `Moved` — there is no successor project. The repository did move *accounts*, from
  `rstoneback/pysatCDF` to `pysat/pysatCDF`, but `Moved` means the software itself now lives
  elsewhere and this copy is not authoritative, which is not the case: `pysat/pysatCDF` is this
  entry's Code Repository.
- `Abandoned`, `Suspended` and `WIP` — all three are defined by the absence of a stable, usable
  public release, which pysatCDF plainly has. `Concept` fails on different ground: its definition
  turns on there being minimal or no implementation, or the repository being only a limited example,
  demo or proof-of-concept, and pysatCDF is a fully implemented library in production use.

**One piece of apparent activity that must not be counted.** The most recently updated item in the
repository's issue tracker is issue #51, "Review HSSI Submission for pysatCDF". That issue is an
artefact of HSSI cataloguing work, not of the maintainers developing the software, and it would be
circular to read it as evidence of project activity.

From a site visitor's side, `Inactive` is the genuinely useful signal: it says "this works, use it,
but do not wait for a release that fixes your numpy incompatibility."

### 24. Documentation (RECOMMENDED)
**Value:** `https://github.com/pysat/pysatCDF/blob/main/README.md`

The README is the entirety of pysatCDF's user documentation, and this is the exhaustive result of
looking for anything more:

- `docs/` at the pin contains exactly one file, `docs/images/logo.png`. There is no Sphinx
  configuration, no `index.rst`, no `.readthedocs.yml`.
- `https://pysatcdf.readthedocs.io/` does not exist, and neither does `https://pysat.github.io/pysatCDF/`.
- GitHub's repository API reports an empty `homepage`.
- **The repository has no wiki**, despite the API reporting `has_wiki` true. A wiki is a separate git
  repository, so this was settled by probing it directly: `git ls-remote
  https://github.com/pysat/pysatCDF.wiki.git` fails with "Repository not found", while the same
  command against `https://github.com/pysat/pysatCDF.git` returns the ref list normally. `has_wiki`
  reports only that the feature is enabled, never that a wiki exists.
- **`.github/workflows/docs.yml` is misleading and worth flagging.** Its `name:` is
  `Documentation Check` and it appears in the repository's workflow list as documentation tooling,
  but its only substantive step is `- name: Load .zenodo.json to check for errors`, running
  `python -c "import json; json.loads(open('.zenodo.json').read())"`. It validates the Zenodo
  metadata file; it builds no documentation. A future agent should not infer a docs site from it.
- `test_requirements.txt` lists `sphinx`, `sphinx_rtd_theme`, `m2r2` and `numpydoc`. These are
  inherited from the pysat project's shared test requirements — `CONTRIBUTING.md` is likewise
  pysat boilerplate, stating that "The pysat logger is imported into each sub-module" and warning
  against reusing "Instrument class key attribute names", neither of which exists in pysatCDF — and
  no Sphinx build is configured or run anywhere.

The PyHC community registry independently rates this project's documentation "Requires improvement",
which is consistent with the above.

**Why a branch URL is correct here, in contrast to Field 33.** A logo URL is pinned to a commit
because the catalogue must keep resolving to the image that was reviewed. A documentation link is the
opposite case: a visitor clicking it wants the project's *current* instructions, so tracking `main`
is the desired behaviour, not a fragility. Kept unchanged.

### 25. Funder (OPTIONAL)
**Value:** None — evidenced absence.

There is no funding statement anywhere in pysatCDF. A search across every tracked path at the pin
*excluding* the vendored `cdf36_3-dist/` tree and the binary test fixture, for
`fund|grant|acknowledg|NNX|80NSSC|NSF |award`, matches exactly one path — `docs/images/logo.png`,
a false positive from byte sequences inside a PNG. The control pattern `\bthe\b` over the same scope
matches many files, so the search was working. DataCite's `fundingReferences` array for the concept
DOI is empty, and `.zenodo.json` at the pin contains a `creators` list and nothing else — no grants
block.

The absence is not merely silence. `CONTRIBUTING.md` describes the project in terms that positively
exclude a funder: "pysatCDF is a community-driven project and welcomes both" (one wrapped source line,
continuing "feedback and contributions.") and, in the feature-request section, "Remember that this is
a volunteer-driven project, and that code contributions" / "are welcome :)".

**A tempting wrong answer, recorded so it is not made.** The pysat paper
(`https://doi.org/10.1029/2018JA025297`) has an acknowledgements section that names NASA and the
National Science Foundation, and that same section lists pysatCDF among the software resources used —
its acknowledgement text includes "pysatCDF: https://github.com/rstoneback/pysatCDF". Those awards
funded pysat and the work reported in that paper. A citing paper's funder is not the cited software's
funder, and nothing connects any award to pysatCDF's development.

**A second, sharper one — name it, because a later refresh will meet it.** The 2023 ecosystem paper
has a Funding section that includes, in the publisher's rendered full text, "JK was supported through
the Space Precipitation Impacts (SPI) project at Goddard Space Flight Center through the
Heliophysics Internal Science Funding Model". JK is Jeff Klenzing, who is also a pysatCDF author, so
the sentence looks closer to this software than it is. It is not: it funds a named co-author's work
on that article, not the development of pysatCDF, and nothing at the pin mentions SPI or any other
award. The trap is that `Space Precipitation Impacts (SPI)` already exists as an Award title in HSSI,
attached to the pysat entry, and an award row with an empty grant identifier binds by
case-insensitive exact title match — so adding it here would silently attach pysatCDF to that same
shared row rather than creating a conspicuously new one, and the error would be invisible afterwards.
The same Funding section also names DARPA, the Naval Research Laboratory (N00173191G016,
N0017322P0744), the Office of Naval Research, and NNH20ZDA001N-LWS / 80NSSC21M0180; all are excluded
on the same ground.

**The general rule these are instances of:** a funder of a *person*, or of a *citing paper*, is not
a funder of the cited software. The Snakes survey's acknowledgements fall under the same rule. The
rule is not this dossier's invention and can be checked at source: the Field 26 agent guidance in
`resource_submission_form_fields.md` names "support for the software's authors" as a tier distinct
from what funded the software, directs that only what funded *this software* be recorded, and asks
that the other tiers be noted with their actual roles as rejected alternatives so a later refresh
does not reintroduce them — which is what the paragraphs above and Field 26 do. That guidance states
that it applies equally to Field 25.

### 26. Award Title (OPTIONAL)
**Value:** None — evidenced absence.

Follows directly from Field 25: there is no award because there is no identified funder. No award
number, grant number or contract number appears anywhere in the repository outside the vendored NASA
distribution, and neither DataCite nor Zenodo records one. An award with no matching evidence is
never supplied as a default.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Values — three publications. HSSI held no value for this field before this refresh.**

1. `https://doi.org/10.1029/2018JA025877` — Burrell, Halford, Klenzing, Stoneback, Morley, Annex,
   Laundal, Kellerman, Stansby & Ma, "Snakes on a Spaceship—An Overview of Python in Heliophysics",
   *Journal of Geophysical Research: Space Physics* 123, 10,384 (2018).
2. `https://doi.org/10.1029/2018JA025297` — Stoneback, Burrell, Klenzing & Depew, "PYSAT: Python
   Satellite Data Analysis Toolkit", *Journal of Geophysical Research: Space Physics* 123, 5271
   (2018).
3. `https://doi.org/10.3389/fspas.2023.1119775` — Stoneback, Burrell, Klenzing & Smith,
   "The pysat ecosystem", *Frontiers in Astronomy and Space Sciences* 10 (2023).

The field's definition covers publications that "describe, cite, or use" the software, and each of
these does so substantively rather than in passing:

- **Snakes on a Spaceship** contains the most detailed published description of pysatCDF anywhere:
  its appendix section A.3.3 is devoted to the package, and the main text discusses it a second time
  when analysing overlap among Python CDF readers. This is the paper to reach for if you want to know
  what pysatCDF is and why it was built the way it was.
- **The PYSAT paper** names pysatCDF in its acknowledgements as one of the software resources the
  work relied on, giving its repository URL alongside pysat's own. It also documents the framework
  pysatCDF was written to feed.
- **The pysat ecosystem** paper assigns pysatCDF a named role in the ecosystem — it is the penumbra
  package that provides Common Data Format support, as against pysatMadrigal for HDF and pysat's own
  built-in netCDF handling — and cites it formally as reference 21, using the concept DOI recorded in
  Field 2.

**How presence was established, and one instrument limitation worth recording.** For the two JGR
papers, ADS full-text search confirms the string directly: `full:"pysatCDF"` restricted to each DOI
returns that record, while the same query shape with a nonsense token returns nothing and the control
term `full:"satellite"` on the PYSAT paper returns the record — so the instrument distinguishes
presence from absence. The same query against the Frontiers DOI returns nothing, and that zero is
**not** evidence of absence: ADS holds title and abstract for that record but no body text. The
differential control is decisive — `full:"pysatMadrigal"` restricted to that DOI returns nothing even
though the term demonstrably appears in the article body, while `full:"pysatMadrigal"` unrestricted
returns other records. Presence in the Frontiers article was therefore established from the
publisher's own full text, where "pysatCDF" appears twice in reader-visible text: once in the body
sentence assigning CDF support to it among the pysat penumbra packages, and once as reference 21.
(The raw page source yields three further matches that no reader sees — one inside a Google Scholar
link URL and two inside the page's script-embedded hydration data — so a count taken over the HTML
rather than the rendered text overstates it. The PDF also gives two.) A future agent should not
conclude from an ADS query that pysatCDF is absent from that paper.

**Considered and not included.** A broader citation sweep was not attempted as a source of further
entries. `full:"pysatCDF"` across ADS returns five records: the two JGR papers above and three
software deposits (pysatCDF's own two Zenodo records and pysat/pysatNASA's). Software deposits are
not publications and belong in Fields 29/30 if anywhere. This field is for publications the developer
would prioritise, and the three recorded here are the ones that actually describe the package's
purpose and role.

### 28. Related Datasets (OPTIONAL)
**Value:** None — evidenced absence.

pysatCDF reads CDF files. It is indifferent to which mission, instrument or dataset produced them,
and it is designed that way. Naming any specific dataset would misrepresent a general-purpose reader
as a dataset-specific tool, and would be arbitrary: the software supports every CDF dataset equally.

The one candidate in the repository was examined and rejected. `pysatCDF/tests/test_data/
cnofs_vefi_bfield_1sec_20080601_v05.cdf` is a single day (2008-06-01) of 1-second magnetic field data
from the Vector Electric Field Instrument on C/NOFS. It is a test fixture, exercised by all three
tests in `pysatCDF/tests/test_cdf.py` with assertions on specific values (`data['altitude'][0]`
rounds to 694, `data['year'][0]` is 2008). A file bundled so that a unit test has something to open
is not a dataset the software "supports functionality for" in this field's sense. Recording it would
also produce the wrong result for a site visitor: someone browsing that C/NOFS VEFI dataset and
asking which software supports it wants analysis tools for VEFI measurements, not a generic file
reader that happens to ship one day of it as a fixture.

### 29. Related Software (OPTIONAL)
**Values:**
- `https://github.com/pysat/pysat`
- `https://github.com/spacepy/spacepy`
- `https://github.com/lasp/cdflib`

**Why a repository URL and not the identifier HSSI held before.** Before this refresh both Field 29
and Field 30 held a single entry identified by `https://doi.org/10.5281/zenodo.15059161`. DataCite
resolves that DOI to "pysat/pysat: v3.2.2", version `v3.2.2`, issued 2025-03-20, with `IsVersionOf`
pointing at
`10.5281/zenodo.1199703`. So the intended target — pysat — was right, but the identifier was a
**version-pinned snapshot** of it, and that is wrong in two ways that compound. First it is
self-staling: it names pysat as it stood at one 2025 release, so every subsequent pysat release makes
the catalogue's statement of the relationship a little more historical, and nothing in HSSI would
ever notice. Second, HSSI renders a related-item entry with its raw URL as the visible link text, so
what a visitor to pysatCDF's page actually saw was a bare `doi.org/10.5281/zenodo.15059161` — a
string that identifies pysat to nobody. pysat is itself in the HSSI catalogue, and its stored code
repository URL is `https://github.com/pysat/pysat`; using that exact value makes the link
self-describing, keeps it correct across releases, and points at the catalogue's own notion of the
same software. (pysat's own concept DOI, `https://doi.org/10.5281/zenodo.1199703`, was the other
candidate and is the right fallback if a DOI is ever preferred here; the repository URL wins on
legibility.)

**pysat** qualifies on every Field 29 ground at once: it is a companion package pysatCDF was written
to serve, a hard dependency (`requirements.txt` pins `pysat>=3.0` and `_cdf.py` imports it at module
level), and a domain-specific one rather than generic infrastructure. The README's Motivation section
states the purpose as simplifying "adding instruments to [pysat](https://github.com/pysat/pysat).",
and the 2023 ecosystem paper
classes pysatCDF among the pysat penumbra packages.

**SpacePy.** SpacePy is the other long-standing Python CDF reader, and pysatCDF's
relationship to it is documented in the source rather than inferred. The `chameleon` class in
`pysatCDF/_cdf.py` carries the docstring "Supports spacepy access pattern along with pysatCDF native"
/ "data access pattern." (two wrapped source lines), and the compatibility is exercised by a named
test, `test_vefi_load_and_chameleon_data_access`, whose docstring reads
`"""Load VEFI file and utilize spacepy like access."""` and which asserts against
`cdf['year'].attrs['FILLVAL']` and `cdf['B_flag'][...][0]` — SpacePy's `pycdf` idiom, not pysatCDF's
own. The Snakes survey frames the two as functionally overlapping, noting that SpacePy "was developed
first and provides full CDF library support (reading" / "and writing) along with many other tools for
magnetospheric physics." A visitor comparing Python CDF readers is exactly who this field is for.

**CDFlib.** The third Python CDF reader, and the natural alternative to pysatCDF for anyone
who cannot or will not compile a Fortran extension. The Snakes survey introduces all three in one
passage — "there are three different packages that load NASA common data format (CDF) files"
(two wrapped lines) — and distinguishes them: CDFlib "was developed recently, and contains a pure
Python CDF reader and" / "writer (as opposed to a Python wrapper for the NASA CDF C library)." That
contrast is precisely the "distinguishing" information Field 29 asks for: it tells a reader what
choosing pysatCDF costs and buys. CDFlib is in the HSSI catalogue with the stored code repository URL
`https://github.com/lasp/cdflib`, which is the value used.

**Excluded, with reasons.**
- **numpy, pandas** — Tier A generic infrastructure. Both are real dependencies and `to_pysat()`
  returns a `pandas.DataFrame`, but the exclusion is categorical and extends to this field: an entry
  that would read identically for most of the Python ecosystem carries no information about
  pysatCDF.
- **xarray** — declared in `requirements.txt` and in `setup.cfg`'s `install_requires`, which makes it
  a Tier B candidate. It fails for a stronger reason than the tier rule: **pysatCDF does not use
  it.** A search of every tracked file at the pin for `xarray` matches three paths and none is
  package code — `requirements.txt`, `setup.cfg`, and `CONTRIBUTING.md` line 134, where
  `` `import xarray as xr` `` appears in a list of "common nicknames" in a style guide that is
  visibly inherited from pysat (the same file states that "The pysat logger is imported into each
  sub-module" and warns against reusing "Instrument class key attribute names", neither of which
  exists in pysatCDF). `pysatCDF/_cdf.py` imports `copy`,
  `numpy`, `string`, `sys`, `pandas`, `pysat` and `pysatCDF.fortran_cdf`, plus two legacy
  `from __future__` imports, and nothing else. The xarray requirement is inherited boilerplate.
- **pysatNASA** — a real downstream relationship: it is the pysat penumbra package for NASA mission
  data and its own release metadata names pysatCDF. It is not recorded here because Field 29 exists
  to say something distinguishing about *this* software, and a list of packages that depend on
  pysatCDF is open-ended and better discovered from the other direction. It is also not in the HSSI
  catalogue, so the entry could not point at a catalogue peer. Recorded so the consideration is
  visible rather than repeated.
- **The vendored NASA CDF library** — bundled source, not a separate software package with its own
  identity in this catalogue; its role is described in Fields 13 and 15.

### 30. Interoperable Software (OPTIONAL)
**Values:**
- `https://github.com/pysat/pysat`
- `https://github.com/spacepy/spacepy`

Same URL reasoning as Field 29: the version-pinned pysat DOI is replaced by pysat's stored
repository URL, for the reasons set out there.

**Why pysat appears in both 29 and 30, deliberately.** The two fields ask different questions and
pysat answers both. Field 29 asks what pysatCDF is *related to* — pysat is its companion and its
reason for existing. Field 30 asks what it demonstrably *exchanges data with*, and pysatCDF has a
textbook adapter for exactly that: `to_pysat()`, whose docstring's Returns block declares
"data : pandas.DataFrame, pysat.Meta" and whose stated purpose is data "suitable for attachment to a
pysat.Instrument object". The README advertises it in its example — "    # Export data to pysat data
and metadata format" — and a dedicated test, `test_vefi_load_to_pysat`, exercises it. Duplication
across the two fields is correct here; it is not an artefact.

**SpacePy.** This is a genuine data-model exchange, not mere co-existence in a Python
environment, and the strongest evidence is the peer-reviewed statement of intent. The Snakes survey's
section A.3.3 says pysatCDF "also supports the same data access mech-" / "anisms present in SpacePy's
CDF routines to enable cross-package interoperability" (two wrapped lines, the hyphenation is the
PDF's own line break; the source renders the apostrophe as a typographic right single quote). That is
the paper describing this relationship in this field's own vocabulary. The implementation backs it:
`chameleon` reimplements SpacePy's variable-access interface so that code written against
`spacepy.pycdf` — `cdf[name][...]`, `cdf[name].attrs[attr_name]` — runs unchanged against a pysatCDF
object, and a test asserts it does.

The counter-argument was considered: this is interface mimicry rather than a file or object handed
from one package to the other, so a strict reading of "demonstrated exchange" could reject it. It is
included because a shared data-access model is exactly what lets a user substitute one package for
the other in working code, which is the practical thing a visitor to either package's page wants to
know — and because the authors of both communities described it as interoperability in print.

**Excluded.** Everything excluded from Field 29 is excluded here for the same reasons, and CDFlib is
additionally excluded *from this field specifically*: it is an alternative to pysatCDF, not a partner.
Nothing converts between them, neither imports the other, and there is no shared data model. CDFlib
appears in Field 29 as a similar-purpose tool and nowhere else. Note that CDFlib is a named Tier B
package, which means it would need a specific documented exchange to qualify here; there is none.
Blanket justifications were not used and are never sufficient: the form names as never-sufficient
*"part of the standard scientific Python ecosystem"* and *"a PyHC member, so it interoperates with
PyHC packages"*.

### 31. Related Instruments (OPTIONAL)
**Value:** None — evidenced absence.

pysatCDF is instrument-agnostic by design. It supports no instrument specifically because it supports
the *file format* that hundreds of instruments happen to use, and it contains no instrument-specific
parsing, calibration, convention or data model. Nothing in the package's source names an instrument.

**The single candidate, examined and rejected.** The only instrument named anywhere in pysatCDF's own
tree is VEFI, via the test fixture
`pysatCDF/tests/test_data/cnofs_vefi_bfield_1sec_20080601_v05.cdf` and the tests that read it.
(Instrument names do occur inside the vendored NASA distribution — `cdf36_3-dist/samples/geocpi0.skt`
names `GEOTAIL>Geomagnetic Tail` and `CPI>Comprehensive Plasma ` among its attributes — but that is
NASA's demonstration data shipped so the CDF tools have something to read. The same gate excludes it
cleanly: pysatCDF is no more designed to support CPI than it is designed to support VEFI.)

This falls squarely inside the relevance gate's exclusion for test, demo and example material: the
file exists so the test suite has a real CDF to open, and pysatCDF has no VEFI awareness
whatsoever — it would read a file from any other instrument identically. Applied to the governing
question: a visitor on VEFI's instrument page clicking "show software related to this
instrument" expects tools for working with electric and magnetic field measurements, and would be
puzzled to be handed a general-purpose file reader. The answer is clearly "annoyed", so the entry is
omitted.

This is a documented omission, not an oversight, and not a resolution failure: no SPASE lookup was
needed because nothing passed the relevance gate. A future agent should not add VEFI or C/NOFS here
on the strength of the fixture.

### 32. Related Observatories (OPTIONAL)
**Value:** None — evidenced absence.

The same reasoning as Field 31, applied at platform level. pysatCDF is mission-agnostic; the only
mission referenced anywhere in its own tree is C/NOFS, and only through the test fixture. GEOTAIL is
named inside the vendored NASA sample data, and is excluded by the same gate for the same reason —
shipping someone's demonstration file is not supporting their mission. A visitor
on a C/NOFS page asking what software relates to the mission wants tools built for C/NOFS data, not a
format reader that ships one day of it for unit testing.

It is worth stating the general principle explicitly, because format readers recur in this catalogue
and the temptation recurs with them: supporting a format that a mission uses is not supporting the
mission. If it were, every CDF reader would have to list every CDF-producing mission in heliophysics,
which would make both this field and the mission pages useless.

### 33. Logo (OPTIONAL)
**Value:**
`https://raw.githubusercontent.com/pysat/pysatCDF/0d0d0fa843e26d269b17591fd27e4561bb32d40f/docs/images/logo.png`

Kept unchanged. The URL is 110 characters, within the 200-character field limit, and is pinned to a
40-hex commit SHA with no branch name and no `blob/` segment.

**Verified, in both required senses.** Fetching it returns image bytes — `content-type: image/png`
and 1,197,500 bytes; `file` identifies it as "PNG image data, 6250 x 4575, 8-bit/color RGBA"; and its
sha256 is byte-identical to the `docs/images/logo.png` blob at the pinned revision, so the URL serves
the repository's own file rather than a redirect or a Git-LFS pointer. (The repository has no
`.gitattributes`, so nothing here is LFS-tracked.) The image was also viewed: it is a genuine
wordmark — "pysat" in cyan above "CDF" in yellow, set on a blue planet encircled by a satellite
orbit — and not an example plot, screenshot or unrelated graphic. The project presents this file
as its logo: the README's opening centred block embeds it with `alt="pysatCDF" title="pysatCDF"`.

**Why a commit-pinned URL rather than the branch URL the README uses.** The README embeds the same
image through `https://raw.githubusercontent.com/pysat/pysatCDF/main/docs/images/logo.png`. A branch
URL is the wrong value for a catalogue: it breaks silently the moment the file is renamed, moved or
deleted, and HSSI has no way to detect that. The objection that pinning "freezes a stale image" is
rejected on principle — that mutability is the fragility being fixed, and a logo redesign is
something a metadata refresh should notice and record deliberately rather than something the
catalogue should inherit without anyone deciding.

There is one convenient coincidence here that a future agent should not rely on: the pinned SHA is
also the current head of `main`, so the pinned and branch URLs presently serve identical bytes. If
`main` ever advances past a logo change, they will diverge, and the pinned URL is the one to update
deliberately.

---

## Durable notes for a future refresh

- **The vendored NASA CDF distribution distorts whole-tree measurements.** Any language, licence or
  keyword scan run over the whole repository will be dominated by `cdf36_3-dist/`, which is NASA's
  code, not this project's. Scope such measurements explicitly, as the entries above do.
- **The C/NOFS VEFI test fixture is used asymmetrically, on purpose.**
  `pysatCDF/tests/test_data/cnofs_vefi_bfield_1sec_20080601_v05.cdf` is the only mission-specific
  artefact in pysatCDF's own tree, and it is cited in this file as *corroboration* in Fields 5 and 16
  and as a *rejected lead* in Fields 17, 28, 31 and 32. That is not an inconsistency, and a future
  agent should not resolve it by making the four fields match the two. The reason is that the two
  questions differ in kind. Fields 5 and 16 ask what community and data domain this software belongs
  to, and a maintainer's choice of which real mission file to ship as the canonical test case is
  genuine, if soft, evidence of that — nobody picks a C/NOFS ionospheric file at random. Fields 17,
  28, 31 and 32 ask what the software is *designed to support*, and a fixture answers that question
  not at all: pysatCDF contains no VEFI-specific or C/NOFS-specific code, and would read any other
  instrument's CDF identically. A fixture can evidence a community without evidencing an instrument,
  and the weight it carries in Fields 5 and 16 is explicitly described there as corroborating rather
  than decisive.
- **Asher Pembroke's author identifier cannot be fixed by a routine metadata update.** His HSSI
  Person row has an empty identifier; supplying an ORCID through a normal update does not fill it in
  but resolves to a different person and strands the original row. A candidate ORCID
  (`0000-0002-5718-1303`) is recorded in Field 6 together with the reason it is *not* applied — it
  has no employment history corroborating the identification. Both obstacles must be cleared before
  anything changes here.
- **The repository has no wiki, no docs site and no Sphinx build**, despite `has_wiki` reporting true
  and a workflow named `Documentation Check` existing. Field 24 records how each was ruled out.
- **The project is stalled on `main` but not abandoned.** Side branches carry unlanded work and the
  maintainers were still triaging pull requests in 2025. If a release ever appears after `v0.3.2`,
  Fields 10, 12, 18–21 and 23 are the ones most likely to need revisiting — in particular, the open
  pull request "Adds latest CDF version to pysatCDF" would change the vendored library version cited
  in Fields 13 and 15, and any numpy-compliance work could change the supported Python range.
- **GitHub's derived metadata is unreliable for this repository specifically.** Its language
  breakdown reports PHP, NASL and Brainfuck; its `updated_at` advances without any development
  happening; its `has_wiki` is true with no wiki. Each was checked against a primary source instead.
