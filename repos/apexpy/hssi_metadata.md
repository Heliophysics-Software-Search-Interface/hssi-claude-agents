# HSSI Metadata Extraction Results

**HSSI Software ID:** 18ff9253-b11c-4ffa-9c3b-4b167c9f8cf2
**Repository:** https://github.com/aburrell/apexpy
**Source Revision:** eed96cf34d8256fbf37a3818c4b696eb802b0a4a
**Extraction Date:** 2026-08-29
**Validation Date:** 2026-08-29
**Validation Status:** PASS

---

This dossier records the HSSI metadata for ApexPy as of 2026-08-29, reconciled against the pinned
source revision and authoritative external sources.

**Scope note — where the evidence comes from.** The pinned revision is the exact commit tagged
`v2.1.1`. Two kinds of in-repo evidence must be read differently. `apexpy/` is the hand-written
Python wrapper; `fortranapex/` is the Fortran coordinate library from the auxiliary material of
Emmert, Richmond and Drob (2010), vendored into the package and compiled into the installed
extension module (`fortranapex/readme.txt` opens "Auxiliary material for Paper 2010JA015326").
Statements in `fortranapex/` comments describe the original library's provenance and its authors'
institutions, not ApexPy's. The working tree also carries untracked JSON/YAML artifacts left by an
earlier tooling run (`datacite.json`, `zenodo.json`, `zenodo_latest.json`, `somef_output.json`,
`pyhc_*.yml`); those are not part of the repository at the pinned revision and are not evidence.
Upstream removed `.zenodo.json` from the repository in v2.1.1 ("Added CITATION.cff as primary
reference file, removed zenodo.json", `CHANGELOG.rst`), so `CITATION.cff` is now the authoritative
in-repo citation record.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Notes:** The bracketed placeholder is the catalogue convention for a record whose HSSI metadata is
maintained by the HSSI curation effort rather than by the software's own maintainers. It is not a
missing value.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.1214206

**Notes:** The Zenodo **concept** DOI, which always resolves to the newest version record. It is
asserted in three independent places in the repository at the pinned revision: `CITATION.cff`
(`identifiers: - type: doi, value: "10.5281/zenodo.1214206"`), the README's `|doi|` badge target,
and `docs/citing.rst` ("please be sure to include the package and specify which version you used
… Note that this DOI will always point to the latest version of the code").

Resolving it lands on whichever version record is newest — at this refresh
`https://zenodo.org/records/20735899`, the v2.1.1 record — which confirms the concept/version
relationship rather than contradicting it; a later resolution to a newer record is that same
behaviour, not a changed identifier. The version-specific DOI belongs in Field 12, not here. The
README badge image is drawn from `zenodo.org/badge/doi/10.5281/zenodo.4585641.svg` — an old v1.1.0
version DOI used only as the badge graphic while the badge's link target is the concept DOI. Do not
mistake that image URL for the persistent identifier.

### 3. Code Repository (MANDATORY)
https://github.com/aburrell/apexpy

**Notes:** Corroborated by `CITATION.cff` (`repository-code`), `pyproject.toml`
(`[project.urls] source`), the PyPI project metadata for `apexpy`, the Zenodo record's
`code:codeRepository` custom field, and the PyHC community registry entry. The repository is not
archived and its default branch is `main`.

### 4. Software Functionality (RECOMMENDED)
- **Coordinate Transforms**
- **Coordinate Transforms: Ionospheric**
- **Data Processing and Analysis**
- **Data Processing and Analysis: Analysis**
- **Data Processing and Analysis: Field-line Tracing**
- **Models and Simulations**
- **Models and Simulations: Empirical**
- **Models and Simulations: Field-line Tracing**

**Notes:** Before this refresh the record carried only the two bare top-level values
`Coordinate Transforms` and `Data Processing and Analysis`. The eight values above are derived from
the code at the pinned revision. Because the vocabulary repeats several leaf names under different
parents, each subcategory below is recorded with the parent that determines its meaning.

- **Coordinate Transforms** and **Coordinate Transforms: Ionospheric** — the package's core purpose.
  `Apex.convert()` accepts exactly the source/destination systems `geo`, `apex`, `qd`, `mlt`
  (`apexpy/apex.py`; the same four choices constrain the CLI in `apexpy/__main__.py`), backed by the
  named pairwise methods `geo2apex`, `apex2geo`, `geo2qd`, `qd2geo`, `apex2qd`, `qd2apex`,
  `mlon2mlt` and `mlt2mlon`. Modified apex, quasi-dipole and magnetic local time are ionospheric
  magnetic coordinate systems — Richmond (1995), the paper that defines them, is titled *Ionospheric
  Electrodynamics Using Magnetic Apex Coordinates*.
- **Coordinate Transforms: Magnetospheric** — considered and **not** selected. That subcategory
  denotes conversion among the magnetospheric frames GSE, GSM, SM, GEO and MAG, and the package
  implements none of them; `convert()` rejects anything outside `{geo, apex, qd, mlt}` with
  "Unknown coordinate transformation". A previous extraction listed this value on the strength of the
  physical region rather than the coordinate systems actually implemented. The magnetospheric
  connection is real but belongs in Field 5, not here.
- **Models and Simulations** and **Models and Simulations: Empirical** — the package embeds and
  evaluates the International Geomagnetic Reference Field, the canonical empirical geomagnetic field
  model. `apexpy/igrf14coeffs.txt` ships the IGRF-14 Schmidt semi-normalised spherical harmonic
  coefficients, `fortranapex/igrf.f90` reads them (`read_igrf`), `fortranapex/magfld.f90` evaluates
  the field (`cofrm`, `feldg`, `dypol`), and the capability is user-facing through
  `Apex.get_babs()` ("Returns the magnitude of the IGRF magnetic field in tesla") and
  `Apex.bvectors_apex()`. `AUTHORS.rst` states "The code uses IGRF-14 with coefficients valid through
  2030."
- **Models and Simulations: Field-line Tracing** — `fortranapex/apex.f90` traces field lines through
  that model field: `linapx` ("Trace the geomagnetic field line from the given location to find the
  apex of the field line"), `itrace` ("Follow a geomagnetic field line until passing its apex") and
  `fndapx`. The precomputed `apexpy/apexsh.dat` coefficient set is generated from those traces by
  `makeapexsh.f90`/`checkapexsh.f90`.
- **Data Processing and Analysis: Field-line Tracing** — the distinct, user-data-facing half of the
  same capability. `Apex.map_to_height()` maps a measured location along the magnetic field to a new
  altitude or to its conjugate hemisphere, and `map_E_to_height()` / `map_V_to_height()` map measured
  electric fields and drift velocities along the field line. Both children are recorded because the
  vocabulary distinguishes tracing *in a model field* from tracing *through data*, and ApexPy does
  both with separate code. An independent confirmation that this is a recognised capability of the
  package: the AACGMV2 documentation
  (https://aacgmv2.readthedocs.io/en/latest/usage.html) states that AACGMV2 "does not perform
  field-line tracing from one location for another … We recommend using :py:mod:`apexpy` for this
  purpose."
- **Data Processing and Analysis** and **Data Processing and Analysis: Analysis** — the package
  computes derived physical quantities beyond the coordinate values themselves:
  `basevectors_qd()` and `basevectors_apex()` return the base-vector sets (f1, f2, f3, g1–g3, d1–d3,
  e1–e3) required for ionospheric electrodynamics calculations, `get_apex()` and `get_height()`
  relate apex latitude to field-line apex height, `get_babs()` returns field magnitude, and
  `apexpy/helpers.py` supplies `subsol()`, `getsinIm()`, `getcosIm()` and `gc2gdlat()`.
- **Data Processing and Analysis: Processing** — considered and not selected. The command-line tool
  does read a file and write a file, but the operation it performs is the coordinate conversion
  already captured above; a generic `Processing` child would add no distinguishing information.
- **Data Visualization** (and every child) — considered and not selected on positive evidence: the
  repository at the pinned revision imports no plotting library anywhere in `apexpy/`,
  `fortranapex/` or `docs/`, and the package produces numeric arrays only. The logo in `docs/` is
  artwork, not a rendering capability.
- **Mission-related** and **Servers and Environments** (and their children) — not selected. The
  package is not part of any mission ground system and ships no server, container or deployment
  component.
- **Data Processing and Analysis: Data Access and Retrieval** — not selected. The package performs
  no network access; see Field 17.

### 5. Related Region (RECOMMENDED)
- **Earth Atmosphere**
- **Earth Ionosphere**
- **Earth Magnetosphere**
- **Earth Thermosphere**

**Notes:** The Region vocabulary is flat: no value implies any other, so each was decided on its own
evidence rather than by containment. Before this refresh the record held only `Earth Atmosphere` and
`Earth Magnetosphere`; `Earth Ionosphere` and `Earth Thermosphere` are added because the vocabulary
offers finer-grained values that the software's evidence directly supports.

- **Earth Ionosphere** — the coordinate systems ApexPy implements are the standard ionospheric
  magnetic coordinates. Richmond (1995), the defining reference carried in `CITATION.cff` and
  `README.rst`, is *Ionospheric Electrodynamics Using Magnetic Apex Coordinates*; `CITATION.cff`
  lists "Ionosphere" among its keywords; the worked examples use ionospheric F-region altitudes
  (300 km in `README.rst` and `docs/examples/ex_cli.rst`).
- **Earth Thermosphere** — the PyHC community registry entry for `apexpy`
  (https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects.yml)
  carries the curated keyword `ionosphere_thermosphere_mesosphere`, and PyHC metadata is
  hand-curated by the community rather than machine-extracted. The same term is already present in
  this record's keyword list.
- **Earth Atmosphere** — retained. The ionosphere and thermosphere in which the package is used are
  regions of Earth's atmosphere, and the flat vocabulary means the coarse value carries information
  that the fine ones do not restate.
- **Earth Magnetosphere** — retained. Modified apex and quasi-dipole coordinates label a location by
  the geomagnetic field line through it; `map_to_height(..., conjugate=True)` maps between magnetically
  conjugate points, and `get_apex()` returns the apex height of the field line, which for
  mid-and-high-latitude field lines lies well above the ionosphere. Apex coordinates are the standard
  frame for organising magnetosphere–ionosphere coupling data.
- **Earth Auroral Subregion** — considered and rejected. ApexPy is deliberately not an auroral-zone
  tool: the distinguishing property of apex/quasi-dipole coordinates against AACGM is that they
  remain defined at low latitudes, a contrast drawn explicitly in the PyHC overview paper's appendix
  section on ApexPy ("In contrast to AACGM coordinates, apex coordinates are defined at low
  latitudes", Burrell et al. 2018, https://doi.org/10.1029/2018JA025877, preprint at
  https://arxiv.org/abs/1901.00143). Nothing in the repository targets the auroral oval.
- **Earth Inner Magnetosphere**, **Earth Outer Magnetosphere**, **Earth Magnetotail**,
  **Earth Magnetosheath** — considered and rejected. The package models only Earth's *internal*
  field (IGRF); it represents no external field source, magnetopause or current sheet, so it cannot
  distinguish these subregions or support science specific to them.
- **Earth Lower and Middle Atmosphere** — considered and rejected. Conversions at height 0 are legal,
  but no source, document or example uses the package for lower- or middle-atmosphere science.
- All solar, heliospheric and non-Earth planetary regions — rejected. The geodetic system is WGS84
  and the field model is Earth's IGRF; nothing in the package applies to another body or to the
  heliosphere.

### 6. Authors (MANDATORY)

The same nine people appear in each of the three authoritative sources — `AUTHORS.rst` and
`CITATION.cff` at the pinned revision, and the record already held in HSSI — so the reconciliation is
a name-by-name union with no one added or dropped. The sources differ in the *detail* they carry —
`CITATION.cff` gives fuller given names for three of them and an affiliation for only four — and
those differences are taken up below. The order below follows `CITATION.cff`, which is the
project's own citation order; HSSI stores its own ordering and the numbering here carries no meaning.

**Author 1:**
- **Name:** Christer van der Meeren
- **Author Identifier:** https://orcid.org/0000-0002-8043-0953
- **Affiliation:** None recorded

**Author 2:**
- **Name:** Karl M. Laundal
- **Author Identifier:** https://orcid.org/0000-0001-5028-4943
- **Affiliation:** University of Bergen (https://ror.org/03zga2b32)

**Author 3:**
- **Name:** Angeline Burrell
- **Author Identifier:** https://orcid.org/0000-0001-8875-9326
- **Affiliation:** United States Naval Research Laboratory (https://ror.org/04d23a975)

**Author 4:**
- **Name:** Leslie Lamarche
- **Author Identifier:** https://orcid.org/0000-0001-7098-0524
- **Affiliation:** SRI International (https://ror.org/05s570m15); University of Alaska Fairbanks (https://ror.org/01j7nq853)

**Author 5:**
- **Name:** Gregory Starr
- **Author Identifier:** https://orcid.org/0000-0002-3487-3630
- **Affiliation:** Boston University (https://ror.org/05qwgg493); Johns Hopkins University Applied Physics Laboratory (https://ror.org/029pp9z10)

**Author 6:**
- **Name:** Ashton Reimer
- **Author Identifier:** https://orcid.org/0000-0002-4621-3453
- **Affiliation:** SRI International (https://ror.org/05s570m15)

**Author 7:**
- **Name:** Achim Morschhauser
- **Author Identifier:** https://orcid.org/0000-0001-7955-4441
- **Affiliation:** GFZ Helmholtz Centre for Geosciences (https://ror.org/04z8jg394)

**Author 8:**
- **Name:** Ingo Michaelis
- **Author Identifier:** https://orcid.org/0000-0001-9741-4063
- **Affiliation:** GFZ Helmholtz Centre for Geosciences (https://ror.org/04z8jg394)

**Author 9:**
- **Name:** Jeff Klenzing
- **Author Identifier:** https://orcid.org/0000-0001-8321-6074
- **Affiliation:** Goddard Space Flight Center (https://ror.org/0171mag52)

**Notes:**

*Sources and agreement.* `AUTHORS.rst` ("This python wrapper is made by:") and `CITATION.cff` list
the same nine people, and all nine carry ORCIDs in `CITATION.cff`. The affiliations recorded above
are richer than `CITATION.cff` supplies — that file gives an affiliation for only Burrell,
Morschhauser, Michaelis and Klenzing — and each resolves to an existing ROR-identified organisation.
They are preserved rather than reduced to the citation file's sparser set.

*Christer van der Meeren's ORCID — kept here as evidence, deliberately not stored in HSSI.*
`CITATION.cff` at the pinned revision asserts `https://orcid.org/0000-0002-8043-0953` for him, and
that is genuinely the iD assigned to him. It is recorded in this dossier for exactly that reason: a
later reader should be able to see which identifier the project itself claims, without having to
rediscover it. It is deliberately not carried into HSSI, because ORCID reports the record
**deactivated** — `https://pub.orcid.org/v3.0/0000-0002-8043-0953/record` answers 409, "The ORCID
record is deactivated".

Be precise about what that means, because the surface appearance misleads. The profile page
`https://orcid.org/0000-0002-8043-0953` still answers 200; it is a client-rendered shell that serves
no public data. The accurate description is therefore *a deactivated iD carrying no public record*,
not *a link that fails to resolve* — the page does load, which is precisely why the emptiness behind
it is easy to miss.

The contrary argument was made and did not prevail, and is set down here so it is not re-litigated a
third time: a deactivated iD is still the identifier assigned to the person, and still the one the
software's own citation metadata asserts, so it could reasonably be stored anyway. It is not stored,
because an identifier that leads a reader to no public record is worse than no identifier at all — it
advertises itself as a route to the author's scholarly record and delivers nothing. The standing
trigger for reopening this is narrow and specific: if a live replacement ORCID for him surfaces, this
is the field to revisit.

One mechanical fact keeps the question from being settled by a routine field update in either
direction, and is worth carrying forward. Supplying an ORCID for an author whose stored Person row
has none does not annotate that row; it resolves to a different person and mints a duplicate,
orphaning the original and any other software that references it. So the stored Person row is left as
it is, without an identifier — and that row is not ApexPy's alone: another catalogued package credits
the same author against it, which makes this a cross-record decision rather than an ApexPy-local
preference. Anyone changing it here would be changing it everywhere.

*Given names.* `CITATION.cff` and the Zenodo record give fuller forms for three authors — "Angeline
G. Burrell", "Leslie L. Lamarche", "Ashton S. Reimer" — while the shorter forms recorded above are
the ones the HSSI record carried into this refresh and keeps. The short forms stand because renaming
a stored Person is not something a metadata update can do: a patch carrying a changed given or family
name silently leaves the stored row unchanged, so a diff asking for the fuller forms could never
close. Which form is right is an open question across the catalogue rather than an ApexPy defect —
these Person rows are shared with other software crediting the same people, so the answer has to be
the same everywhere. If the fuller forms are wanted they are a shared-record correction, and the
ORCIDs above are the reliable key for making it.

*"van der Meeren" versus "Meeren".* The Zenodo record for v2.1.1 lists the creator as "Meeren,
Christer", dropping the particle. That is an artifact of Zenodo parsing `CITATION.cff`'s
`name-particle: "van der"` after the project retired `.zenodo.json` — the earlier `.zenodo.json`
(present up to v2.1.0) spelled the name "van der Meeren, Christer". The full form recorded above is
correct; the Zenodo string is not a rename.

*Jeff Klenzing's affiliation — researched, and deliberately left as Goddard Space Flight Center.*
Three sources disagree, and the disagreement is real rather than a data error:
`CITATION.cff` at the pinned revision says "Independent Researcher"; ORCID
(https://orcid.org/0000-0001-8321-6074) shows Goddard Space Flight Center, ITM Physics Lab, from
2012-04 to 2025-08, and thereafter University of Maryland, Baltimore County / Goddard Planetary
Heliophysics Institute as Affiliate Associate Research Scientist from 2025-10; the HSSI record
carried Goddard Space Flight Center into this refresh and keeps it. The repository history shows the change was deliberate: the affiliation read
"Goddard Space Flight Center" from the first `CITATION.cff` (commit 9aa4a5b, 2025-04-07) and was
changed to "Independent Researcher" in commit ff93c4f (2025-08-08, "DOC: update citation.cff"),
matching the month his GSFC employment ended. Goddard Space Flight Center is nevertheless retained,
for three reasons: it is the institution at which his ApexPy contributions were made; "Independent
Researcher" is not an institution and has no ROR, so recording it would create a meaningless
organisation row; and the UMBC appointment post-dates the pinned revision, is not asserted anywhere
in this repository, and would be applied to a Person row shared with other software records. A
future curator who wants to reflect his current institution should treat it as a shared-record change
across every entry that credits him, not as an ApexPy field edit.

*Other current-employer divergences, checked and deliberately not applied.* ORCID shows Karl M.
Laundal holding a Technical University of Denmark senior-researcher post (from 2025-09) concurrently
with his University of Bergen associate professorship; Ashton Reimer at LeoLabs since 2021-12, after
SRI International ended; and Gregory Starr at Draper Laboratory alongside JHU APL. None is asserted
in this repository, none bears on the ApexPy work, and each would touch a shared Person row, so the
stored affiliations stand. Recorded here so a later refresh does not re-derive these from ORCID and
treat them as newly discovered drift. One caveat worth carrying: Boston University appears in
Gregory Starr's ORCID as his degree-granting institution (BS and MS, Electrical and Computer
Engineering), not as an employer — the value is retained but a curator removing it would have a
defensible reason.

*Organisation authors.* There are none. Every author is a person with an ORCID; no lab, consortium or
institution is credited as an author, so no ROR-identified organisation author applies.

### 7. Software Name (MANDATORY)
ApexPy

**Notes:** The distribution, import and repository name is the all-lowercase `apexpy` — that is what
`pyproject.toml` (`name = "apexpy"`), `setup.cfg`, `CITATION.cff` (`title: apexpy`), PyPI and the
Zenodo record use, because those are identifiers rather than display names. The project's own
*display* name is the camel-case form, and the repository states it directly:
`docs/conf.py` sets `project = 'ApexPy'`, the README's logo alt text opens "ApexPy logo: …", and every
GitHub release is titled "ApexPy Version X.Y.Z". HSSI's Software Name is a display name, so the
camel-case form is correct and the previously recorded value stands. An earlier extraction proposed
the lowercase `apexpy` (and a "full name" of "aburrell/apexpy: ApexPy", which is a Zenodo release
title, not a name); neither supersedes the in-repository `docs/conf.py` declaration.

### 8. Description (MANDATORY)
This is a Python wrapper for the Apex fortran library by Emmert et al. (2010), which allows converting between geodetic, modified apex, and quasi-dipole coordinates as well as getting modified apex and quasi-dipole base vectors (Richmond 1995). The geodetic system used here is WGS84. MLT calculations are also included. The package uses IGRF-14 magnetic field coefficients (1900-2030) and provides tools essential for ionospheric and magnetospheric research. The software is free and open source under the MIT license.

**Notes:** This closely follows the opening of `README.rst` and remains accurate at the pinned
revision, so it is kept as written rather than re-phrased. Its factual claims hold at the pinned
revision: `apexpy/igrf14coeffs.txt` is headed "14th Generation International Geomagnetic Reference
Field" and tabulates epochs from 1900.0 through 2025.0 with a 2025–30 secular-variation column, so
"IGRF-14 … (1900-2030)" is right; `AUTHORS.rst` independently states the coefficients are "valid
through 2030"; the WGS84 statement matches `fortranapex/magfld.f90` ("Req = Equatorial radius of
Earth in km (WGS84 value)"); and `LICENSE` is MIT.

Two capabilities the description does not mention — the `apexpy` command-line interface and the
field-line mapping of measured electric fields and drift velocities — are recorded in Field 4
instead. That is a deliberate division of labour, not an omission to be repaired by rewriting this
text.

Do **not** take a replacement for this field from the DOI record. Zenodo places the GitHub release
note in the record's description, so DataCite's "Abstract" for this DOI is the newest release's
summary — at this refresh, v2.1.1's — rather than a description of the software; autofill would
silently substitute it.

### 9. Concise Description (OPTIONAL)
A Python wrapper for converting between geodetic, modified apex, and quasi-dipole coordinates, with magnetic local time calculations.

**Notes:** 133 characters, within the field's 200-character limit, and an accurate preview of the
full description. Kept as previously worded.

### 10. Publication Date (RECOMMENDED)
2015-11-30

**Notes:** Corrected. The record previously held 2015-11-18, which is the date of the repository's
first commit (`c26315d`, "initial commit") — the day development began, not the day the software was
published. The field asks for the date of first publication, used for the initial version. Version
1.0.0 was published on 2015-11-30: `CHANGELOG.rst` records "1.0.0 (2015-11-30) … Initial release",
the annotated tag `v1.0.0` is dated 2015-11-30, and PyPI's first `apexpy` upload
(https://pypi.org/pypi/apexpy/json) is timestamped 2015-11-30T09:52:33Z.

Zenodo cannot supply this date: the project's earliest Zenodo version record is 1.0.3 (2018-04-06),
because DOI minting began long after first release. A future agent reading only the DOI metadata
would get 2018 or, from the concept DOI, the current release year.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Notes:** The DOI was obtained through the GitHub–Zenodo workflow, which the field guidance names as
the case where Zenodo is the correct publisher. DataCite reports `publisher: "Zenodo"` for
10.5281/zenodo.1214206. Zenodo has no ROR of its own that would better identify it here, so its URL
serves as the identifier.

### 12. Version (RECOMMENDED)
- **Version Number:** v2.1.1
- **Version Date:** 2026-06-17
- **Version Description:** This update adds support for the newest versions of Python (up to 3.14), fixes broken links in the documentation, and changes the way citation information is shared with Zenodo and other similar users.
- **Version PID:** https://doi.org/10.5281/zenodo.20735899

**Notes:** A bump from v2.1.0 (2025-01-07), which is what the record held before this refresh.

Five records agree on the date, though they are not all independent of one another: the tag `v2.1.1`
points at the pinned commit, dated 2026-06-17; `CHANGELOG.rst` heads its newest entry
"2.1.1 (2026-06-17)"; the GitHub release was published 2026-06-17; the Zenodo version record gives
`publication_date: 2026-06-17`; and the PyPI files for 2.1.1 were uploaded the same day. The Zenodo
record is minted from the GitHub release and that release points at the tag, so the separately
sourced confirmations are the repository itself (tag and changelog), the GitHub release chain, and
PyPI.

The version description is the maintainers' own GitHub release note for "ApexPy Version 2.1.1",
quoted in full. `CHANGELOG.rst` gives the same release as four bullets — updated GitHub Actions
versions and removed an unused wheel upload, fixed a broken documentation link, added `CITATION.cff`
as the primary reference file and removed `zenodo.json`, and updated the supported Python versions
and NEP29 testing. The release note was preferred because it is the maintainers' summary written for
readers rather than a change log for contributors. It happens to match what Zenodo and DataCite hold,
which is a corroboration rather than the reason for choosing it — DOI autofill is not a source for
this field, since it propagates whatever Zenodo captured.

The version string keeps its leading `v`, which is the form the record already used and the form of
the repository's release tags with one exception — the 2018 tag `1.0.3` was cut without the prefix.

**Trap for a future agent.** Two files in the tree are stale at the pinned revision and will mislead
a grep for the version: `meson.build` still declares `version: '2.1.0'`, and
`apexpy/__init__.py` carries `__version__ = "2.1.0"` as a fallback used only when package metadata
cannot be read. The authoritative in-repo declarations are `pyproject.toml`
(`version = "2.1.1"`) and `CITATION.cff` (`version: 2.1.1`).

Earlier releases, for context: v2.1.0 (2025-01-07), v2.0.2 (2024-11-12), v2.0.1 (2023-04-11),
v2.0.0 (2022-12-09), v1.1.0 (2021-03-05), 1.0.3 (2018-04-06 — the tag date; `CHANGELOG.rst`
heads that release 2018-04-05, a one-day disagreement internal to the repository and the only one
among the tagged releases listed here), v1.0.2 (2018-02-27), v1.0.1
(2016-03-10), v1.0.0 (2015-11-30). `CHANGELOG.rst` additionally carries a "1.0.4 (2019-04-05)" entry
for which the repository holds no tag, so a tag-derived release list and a changelog-derived one do
not correspond one for one.

### 13. Programming Language (RECOMMENDED)
- **C**
- **Fortran90**
- **Python 3.x**

**Notes:** Re-derived at the pinned revision now that the vocabulary distinguishes five Fortran
standards; the three values above are unchanged from what the record held, and the reasoning for each
is set down so the question does not have to be reopened.

- **Python 3.x** — `pyproject.toml` sets `requires-python = ">=3.9"` and classifies Python 3.9
  through 3.14; the CI matrix in `.github/workflows/main.yml` runs 3.9, 3.10, 3.11, 3.12, 3.13 and
  3.14. **Python 2.x** does not apply: `CHANGELOG.rst` records "Removed Python 2 support" in v2.0.0.
- **Fortran90 is the only correct Fortran value.** All seven Fortran sources at the pinned revision
  are free-form `.f90` files using F90 constructs — `module`/`contains`, `implicit none`, `real(8)`,
  `allocatable` arrays — and none uses a post-F90 construct: `iso_fortran_env`, `iso_c_binding`,
  `class(`, `select type`, `associate`, `block`, `submodule`, `do concurrent`, `error stop`,
  `move_alloc`, `newunit=`, deferred-length character and `bind(c)` are absent as code. Two of those
  words do appear as prose and will mislead a plain grep — "associated Legendre" in
  `fortranapex/magfld.f90` and "common block" in both `magfld.f90` and `fortranapex/apex.f90`, the
  latter describing what the original F77 code used. The project says so itself: `CHANGELOG.rst` records "Update Fortran source code to
  Fortran 90 standards" in v2.0.0, `fortranapex/magfld.f90` is headed "Translated to Fortran 90 by
  Leslie Lamarche", and `fortranapex/readme.txt` describes the upstream `apexsh.f90`,
  `makeapexsh.f90` and `checkapexsh.f90` as "Fortran-90 code".
  - **Fortran 2003 / 2008 / 2023** — rejected. An earlier extraction listed Fortran 2003 alongside
    Fortran90; nothing in the source supports it.
  - **Fortran77** — rejected, but for a reason worth recording: it *was* accurate historically. The
    original library shipped `apex.f` and `magfld.f` as Fortran-77 (`fortranapex/readme.txt` still
    describes them that way, because that text is copied from the 2010 paper's auxiliary material).
    Those files were translated to Fortran 90 in v2.0.0 and no fixed-form Fortran remains at the
    pinned revision. `meson.build` sets `fortran_std=legacy`, which relaxes the compiler's
    conformance checking on the translated code; it is not evidence of F77 source.
- **C** — retained, with the nuance stated plainly so it is not mistaken for hand-written C.
  `meson.build` declares C as a project language (`project('apexpy', 'c', …)`), requires a working C
  toolchain (`cc.check_header('Python.h', …, required: true)`), compiles NumPy's `fortranobject.c`
  into a static library and builds the extension module from generated C. `docs/installation.rst`
  tells users "Installation also requires a C compiler of the same type as the fortran compiler."
  GitHub reports C as roughly a third of the repository's bytes. The C in the tree
  (`fortranapex/fortranapexmodule.c`) is f2py-generated glue — its own header says "This file is
  auto-generated with f2py … Do not edit this file directly unless you know what you are
  doing!!!" — and the meson build regenerates it
  rather than compiling the checked-in copy. Dropping the value was considered; it was kept because
  the field asks for the languages most important to the software, and a C toolchain is a hard
  requirement to build or install this package.

### 14. Reference Publication (OPTIONAL)
https://doi.org/10.1029/2010JA015326

**Notes:** Emmert, J. T., A. D. Richmond, and D. P. Drob (2010), "A computationally compact
representation of Magnetic-Apex and Quasi-Dipole coordinates with smooth base vectors",
*J. Geophys. Res.*, 115(A8), A08322. This is the paper describing the Fortran library the package
wraps, and the project names it as the required companion citation: `CITATION.cff`'s `message` reads
"please cite both the package DOI and the Apex Coordinates journal article: Emmert, J. T., …
doi:10.1029/2010JA015326", `README.rst` carries it as reference [1], and it heads `CITATION.cff`'s
`references` block. The vendored Fortran in `fortranapex/` is that paper's auxiliary material.

The DOI resolves, but the publisher page answers 403 to non-browser fetches — that is bot-blocking
rather than a paywall, and should not be read as a dead link.

The second work the project asks users to cite, Richmond (1995), is recorded in Field 27, which is
where a prioritised publication other than the reference publication belongs.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

**Notes:** The HSSI record held no license value before this refresh. `LICENSE` is the MIT text:
it opens "The MIT License (MIT)" and carries "Copyright (c) 2015 Christer van der Meeren" as a
separate line below it. `pyproject.toml` points its
`license` at that file and carries the classifier "License :: OSI Approved :: MIT License";
`CITATION.cff` records `license: MIT`; and the Zenodo record gives `{"id": "mit-license"}`. The URI is
the one the controlled `MIT License` row itself carries, which is what the form auto-populates for an
SPDX licence. DataCite reports `https://opensource.org/licenses/MIT` for the same licence; that URL
is equivalent but is not the URI HSSI stores for this row, so the SPDX form is used.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
apex · conversion · converting · coordinate conversion · coordinates · field-line tracing ·
heliophysics · igrf · igrf14 · ionosphere · ionosphere thermosphere mesosphere ·
magnetic apex coordinates · magnetic coordinates · magnetic field · magnetic local time · mlt ·
modified apex · quasi dipole · quasi dipole coordinates · space physics · WGS84

**Notes:** The keywords are written above in the controlled vocabulary's own casing. HSSI's read API
title-cases keywords when it renders them ("mlt" is displayed as "Mlt"), so a rendered value copied
back verbatim is not the stored value.

Seventeen of these were already on the record and come from `pyproject.toml`'s `keywords` list, from
`CITATION.cff`'s `keywords` block, and from the PyHC registry's curated
`ionosphere_thermosphere_mesosphere`. Four are added, each reusing a vocabulary row that already
exists rather than minting a near-duplicate:

- **igrf** and **igrf14** — the package embeds and evaluates IGRF-14 (`apexpy/igrf14coeffs.txt`,
  `fortranapex/igrf.f90`, `Apex.get_babs()`); `CHANGELOG.rst` v2.1.0 records "updated to IGRF-14".
  Someone searching HSSI for an IGRF implementation in Python should find this package.
- **field-line tracing** — see Field 4; the tracing routines are `linapx`, `itrace` and `fndapx` in
  `fortranapex/apex.f90`, exposed to users through `map_to_height` and its relatives.
- **WGS84** — the geodetic system the package uses, stated in `README.rst`, in the description, and
  in `fortranapex/magfld.f90`.

`pyproject.toml` also lists the hyphenated "quasi-dipole". It is not added: the vocabulary carries
"quasi dipole" (already on the record) and no hyphenated row, and adding one would create a permanent
near-duplicate keyword.

### 17. Data Sources (OPTIONAL)
Not found — the package retrieves no data from any external source.

**Notes:** This is an evidenced negative, not an unexamined gap. The package performs no network
access: a search of `apexpy/` and `fortranapex/` at the pinned revision found no HTTP client, no
`urllib`/`requests` import, and no download logic. Every host- or URL-shaped string in those trees
sits in a comment and is inert — a StackOverflow answer cited in `apexpy/helpers.py`, an f2py
archive link in `fortranapex/fortranapex.pyf`, the historical NOAA/NGDC and NASA/GSFC addresses in
the comment headers of `fortranapex/magfld.f90` and `fortranapex/apex.f90` explaining where the IGRF
tables originally came from, and a CEDAR Data System address in the vendored
`fortranapex/readme.txt` naming where updated versions of the upstream Fortran would be posted. None
of them is fetched by the code.

Both data files the package reads ship inside it: `apexpy/apexsh.dat` (spherical-harmonic expansion
coefficients) and `apexpy/igrf14coeffs.txt` (the IGRF-14 table), both installed by `meson.build` and
located through `importlib.resources` in `apexpy/apex.py`.

No row in the Data Sources vocabulary applies. The named archives and services — `CDAWeb`,
`OMNIWeb`, `SSCWeb`, `Madrigal`, `AMDA`, `VirES`, `das2`, `HAPI`, `TAP`,
`The Virtual Solar Observatory.`, `WDC`, `GFZ`, `S3/Cloud-aware`, and the two directory options
`FTP/FTPS Directories` and `HTTP/HTTPS Directories` — all denote a source the software retrieves
from, and this software retrieves from none of them. The row names are given in the vocabulary's
own spelling so this enumeration can be checked against it directly; the trailing period in
`The Virtual Solar Observatory.` is part of the stored row name, not punctuation of this sentence. `Observatory/Mission-specific` does not apply
either; see Fields 31 and 32. The catch-all `Other` is no better a fit: it stands for a retrieval
source the vocabulary has no row for, and there is no source of any kind to name. `GFZ` and `WDC`
deserve an explicit rejection because the IGRF coefficients ultimately originate with IAGA and are
distributed by such bodies: the package neither queries nor is configured against them, it vendors a
static copy of the table.

### 18. Input File Formats (RECOMMENDED)
- **Other**
- **ascii**

**Notes:** The HSSI record carried no input-format value before this refresh, and a previous
extraction concluded the field was "not applicable" on the grounds that inputs are passed
numerically. That understated a documented capability: the installed `apexpy` command-line tool takes
`-i FILE_IN` and parses it with `numpy.loadtxt` (`apexpy/__main__.py`), and
`docs/examples/ex_cli.rst` walks a user through creating a whitespace-delimited `input.txt` of
latitudes and longitudes, comment lines included. The shipped test fixtures
`apexpy/tests/test_convert.txt` and `test_convert_single_line.txt` are files of exactly that form.
`apexpy/igrf14coeffs.txt`, read at every `Apex` construction, is likewise plain ASCII.

**`Other` records the binary coefficient file.** `Apex(datafile=...)` accepts a user-supplied path
to a replacement `apexsh.dat`, which is a Fortran *unformatted* binary — `fortranapex/apexsh.f90`
opens it with `form='unformatted'`, and a generic file-type probe misidentifies it as a MATLAB v4
file, which it is not. It is a genuine second input format that the distributed package accepts, and
the vocabulary carries no row naming it, so `Other` is the only value that can represent it.
The argument against was weighed and rejected: that the file ships inside the package, that the
override exists chiefly for regenerating coefficients during maintenance
(`fortranapex/readme.txt` documents the rebuild procedure) rather than for supplying scientific
data, and that a bare `Other` is uninformative to a searcher. None of that makes the format less
real, and omitting it would have left a documented input path unrecorded. `ascii` and `Other`
together record both input paths the distributed package accepts, and that is the settled answer for
this field.

### 19. Output File Formats (RECOMMENDED)
- **ascii**

**Notes:** The command-line tool writes its converted coordinates with
`numpy.savetxt(..., fmt='%.8f')` to `-o FILE_OUT` or to standard output (`apexpy/__main__.py`), and
`docs/examples/ex_cli.rst` shows the resulting `output.txt`. The Python API returns arrays rather
than writing files, so ASCII is the package's only output format.

The Fortran maintenance program built from `fortranapex/Makefile` (`apextest`) writes a new
`apexsh.dat` in Fortran unformatted binary, but it is a coefficient-regeneration tool that is neither
installed nor exposed through the Python package, so it does not make `Other` an output format of the
distributed software.

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**

**Notes:** The CI matrix in `.github/workflows/main.yml` at the pinned revision builds and tests on
`ubuntu-latest`, `windows-latest`, `macos-latest` and `macos-26-intel`, with per-platform install
recipes for each. `pyproject.toml` classifies the package for Microsoft Windows, POSIX, POSIX::Linux,
Unix and MacOS, and `docs/installation.rst` states "The package has been tested with the following
setups … Windows (64 bit Python), Linux (64 bit), and Mac (64 bit)".

`Operating System Independent` is not selected: the package builds a compiled extension and needs a
platform-appropriate gfortran/gcc toolchain, with documented Windows and macOS specific workarounds.
`Solaris` and `MobilePlatform` have no supporting evidence.

### 21. CPU Architecture (RECOMMENDED)
- **Apple Silicon arm64**
- **CPU Independent**
- **x86-64**

**Notes:** All three values are kept, with the evidence for each and the tension in the third one
both set down.

- **x86-64** — the Linux and Windows CI jobs run on x86-64 runners, `actions/setup-python` is pinned
  to `architecture: 'x64'`, the `macos-26-intel` job builds against `/usr/local/bin/gcc-15` (the
  Intel Homebrew prefix), and `docs/installation.rst` states the tested setups are 64-bit.
- **Apple Silicon arm64** — the `macos-latest` CI jobs build against `/opt/homebrew/bin/gcc-15`, the
  Apple-Silicon Homebrew prefix, and `docs/installation.rst` devotes a section to Apple Silicon,
  including the `CFLAGS="-falign-functions=8"` workaround for bus errors and guidance that users
  confirm their wheels "end in `arm64.whl` not `osx-64.whl`".
- **CPU Independent** — kept on the reading that no source in the package is architecture-specific:
  the Python, Fortran and generated C are portable, and `meson.build`'s only machine-dependent
  branches concern the host operating system and MinGW pointer bitness, not the instruction set. A
  source build therefore succeeds on any architecture with gfortran and gcc. The competing reading
  is that a package shipping a compiled extension is by definition architecture-specific once built;
  under that reading this value and the two above would be in tension. That tension was weighed and
  the value kept: the portability claim is true of the source, and dropping the value would narrow
  the record on a matter of interpretation rather than of fact. The choice is settled — an agent who
  rediscovers the tension has not found new evidence, only the same reading that was already
  considered.
- **Linux aarch64 or arm64** — considered and not selected: no CI job exercises it and no wheel is
  published for it, so there is no evidence, only the expectation that a source build would work.
- **GPU**, **HPC or HEC**, **ppc64le**, **Sun (SPARC)** — no evidence; the package has no parallel,
  accelerator or vendor-specific code path.

### 22. Related Phenomena (OPTIONAL)
Not found — no phenomenon in the controlled vocabulary is one this software provides science
functionality for.

**Notes:** A reasoned empty rather than an unexamined field: no row in the Phenomena vocabulary
names something this software supports science functionality for. Coronal Heating, Coronal Mass
Ejections, Solar
Corona, Solar Flares, Solar Wind and X-ray emission are all solar or heliospheric, and the package is
entirely an Earth-field, Earth-coordinate library. `Geomagnetic Storms` is the only near miss and was
rejected deliberately: apex and quasi-dipole coordinates are the frame in which many storm-time
ionospheric studies are organised, but the field asks for phenomena the software "supports science
functionality for", and this package implements no storm index, no disturbance model and no
storm-specific analysis — it would be equally applicable on the quietest day of the solar cycle. The
vocabulary is closed, so a phenomenon with no row cannot be entered here; the physical setting is
instead captured by Fields 5 and 16.

### 23. Development Status (RECOMMENDED)
Active

**Notes:** The HSSI record held no development status before this refresh. "Active" is the
repostatus.org term for a project that has reached a stable, usable state and is being actively
developed, which fits on every axis: `pyproject.toml` classifies it "Development Status :: 5 -
Production/Stable"; releases run from 2015 through v2.1.1 in June 2026; `.github/workflows/main.yml`
runs a weekly scheduled cron build in addition to push and pull-request builds, so breakage from
dependency drift is caught without a release; the GitHub repository is not archived; and the PyHC
community registry rates the package "Good" on all six of its axes (community, documentation,
testing, software maturity, Python 3, license). `Inactive`, `Unsupported`, `Abandoned`, `Suspended`,
`Moved`, `Concept` and `WIP` are each contradicted by that same evidence.

### 24. Documentation (RECOMMENDED)
https://apexpy.readthedocs.io/en/latest/

**Notes:** Declared in `pyproject.toml` (`[project.urls] documentation`), linked from `README.rst`,
built from `docs/` by `.readthedocs.yml`, and listed as `docs` in the PyHC registry entry (which uses
the equivalent `http://apexpy.readthedocs.io` form). The site includes the installation and
troubleshooting guide at `.../installation.html`, so this single URL satisfies the field's
requirement that documentation include installation instructions.

### 25. Funder (OPTIONAL)
Not found

**Notes:** An evidenced negative. No funding statement, acknowledgement, grant number or sponsor
appears anywhere in the repository at the pinned revision — a search across all tracked files for
funding, grant, acknowledgement, award, sponsor, contract, NASA and NSF returned only the MIT
licence's "granted, free of charge", the licence's "ACTION OF CONTRACT", the historical
`geomag.gsfc.nasa.gov` ftp and e-mail addresses in `fortranapex/magfld.f90` comments, and the
substring "nsf" inside the word "transformation". None of those is a funding statement, and a future
agent repeating the search should expect the same false positives.
Neither the Zenodo record nor DataCite carries any funding reference for the concept DOI, and there
is no ApexPy-specific paper whose acknowledgements could supply one — a full-text search of the
literature for the package name turns up papers that *use* it, plus its own Zenodo release records,
but no software paper.

Two candidates were investigated and rejected, and are recorded so they are not reintroduced:

- **The reference publication's funders.** Emmert, Richmond and Drob (2010) acknowledges the National
  Aeronautics and Space Administration — including a Living With a Star grant — and the Office of
  Naval Research. That funding produced the original Fortran algorithm and its paper, which ApexPy
  vendors and wraps; it did not fund the Python package, whose first release came five years later
  from a different author. The field guidance is explicit that funding at a different tier must not
  be recorded as this software's funder. The awards are named, for the record, so this candidate is
  not reinvestigated: the paper's Acknowledgments read "J. T. Emmert and D. P. Drob acknowledge
  support from the Office of Naval Research and from the NASA Living with a Star (LWS) Program
  (grant 04-000-0098). A. D. Richmond acknowledges support from the NASA LWS Strategic Capabilities
  Program and from AFOSR contract FA9550-08-C-0046." The publisher's page answers 403 to non-browser
  fetches, which is bot-blocking rather than a paywall; the text above was read from an openly hosted
  copy of the paper at
  http://jupiter.ethz.ch/~kuvshinov/For_Dima_Alexeev/MLT/Emmert_QD_2010JA015326.pdf.
- **The maintainer's salary support.** The PyHC overview paper Burrell et al. (2018),
  https://doi.org/10.1029/2018JA025877, states "A.G. Burrell is supported by the Chief of Naval
  Research." That is institutional support for a person, stated in a different paper, and is not a
  grant to this software.

### 26. Award Title (OPTIONAL)
Not found

**Notes:** No award, grant or contract identifier is asserted for this software in the repository,
the Zenodo record or DataCite. See Field 25 for the funding candidates that were investigated and
why each was rejected. This field cannot be filled independently of Field 25.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.5636/jgg.47.191
- https://doi.org/10.1029/2018JA025877

**Notes:** The HSSI record held no related publications before this refresh; a previous extraction
recorded "not found beyond the reference publication" without looking past the DOI metadata. Both
entries below are prioritised by the project itself or written by its own authors about it.

- **Richmond, A. D. (1995), "Ionospheric Electrodynamics Using Magnetic Apex Coordinates",
  *J. Geomagn. Geoelectr.*, 47(2), 191–212.** This is the paper that defines the modified apex and
  quasi-dipole coordinate systems the package implements. The project asks users to cite it:
  `docs/citing.rst` says "We also recommend citing a reference to the coordinate system you use",
  `README.rst` carries it as reference [2], `AUTHORS.rst` states "Quasi-dipole and modified apex
  coordinates are defined by Richmond [1995]", and it is the second entry in `CITATION.cff`'s
  `references` block. Field 14 holds a single DOI and is occupied by Emmert et al. (2010), so this
  second prioritised reference belongs here. The DOI resolves to the J-STAGE article page.
- **Burrell, A. G., et al. (2018), "Snakes on a Spaceship — An Overview of Python in Heliophysics",
  *J. Geophys. Res. Space Physics*, 123, 10,384.** Its appendix section A.4.2 is a dedicated
  description of ApexPy — what apex and quasi-dipole coordinates are, how they differ from AACGM, and
  what the package provides ("apexpy … provides functions to convert to and from apex coordinates. It
  also includes functions to calculate base vectors"). Its lead author is ApexPy's maintainer and two
  further ApexPy authors (Klenzing, Laundal) are co-authors, so this is the software's authors
  describing it in the peer-reviewed literature, not an incidental citation. The publisher page
  answers 403 to non-browser fetches, which is bot-blocking rather than a paywall; the openly
  readable preprint is at https://arxiv.org/abs/1901.00143.

**Considered and not selected:** Thébault et al. (2015), the IGRF-12 reference cited in
`AUTHORS.rst`. The package ships IGRF-14 coefficients, so that citation describes a superseded
generation of the model rather than the data the software actually uses, and it is not a publication
about ApexPy. `AUTHORS.rst` also links the IGRF-14 special-issue call at
https://www.springeropen.com/collections/IGRF14, which is a collection landing page rather than a
publication.

### 28. Related Datasets (OPTIONAL)
Not found

**Notes:** The package analyses no external dataset. The two data files it reads are model
coefficients bundled inside the distribution: `apexpy/igrf14coeffs.txt` (IGRF-14 spherical harmonic
coefficients) and `apexpy/apexsh.dat` (the expansion coefficients generated from them by the
package's own Fortran tooling). Recording the IGRF-14 coefficient table here was considered and
rejected: it is a model, not an observational dataset the software supports functionality for; the
repository cites no DOI or landing page for it; and its role — the field model that underpins the
coordinate transforms — is already carried by Field 4's `Models and Simulations: Empirical` and by
the `igrf`/`igrf14` keywords. Neither the Zenodo record nor DataCite relates this software to any
dataset identifier.

### 29. Related Software (OPTIONAL)
- https://github.com/aburrell/aacgmv2
- https://github.com/spacepy/spacepy

**Notes:**

- **AACGMV2** — the strongest entry, and the archetype the field describes: two packages performing
  the same task under different assumptions. Both are Python wrappers around a compiled magnetic
  coordinate library by the same maintainer; AACGMV2 converts to altitude-adjusted corrected
  geomagnetic coordinates, ApexPy to modified apex and quasi-dipole coordinates. They cross-reference
  each other in their own documentation — AACGMV2's usage guide
  (https://aacgmv2.readthedocs.io/en/latest/usage.html) says it "does not perform field-line tracing
  from one location for another … We recommend using :py:mod:`apexpy` for this purpose" — and the
  PyHC overview paper presents them in adjacent appendix sections (A.4.1 and A.4.2) precisely to
  contrast them, noting that apex coordinates remain defined at low latitudes where AACGM does not.
- **SpacePy** — a similar-task alternative under different assumptions. Its `spacepy.coordinates`
  module converts among the geophysical and magnetospheric frames GEO, GDZ (geodetic), GSM, GSE, SM,
  MAG and the ECI variants (https://spacepy.github.io/coordinates.html). That is a different family
  of magnetic coordinate systems from ApexPy's apex/quasi-dipole pair, reached by different physical
  assumptions, and a user choosing a Python magnetic-coordinate transform would weigh the two. Kept
  on that documented capability rather than on shared PyHC membership, which would not be sufficient.
- **pysat — not listed, on two independent grounds: the value the record previously carried was a
  wrong-project URL, and the project it was meant to name does not clear the relevance gate either.**
  The record carried `https://github.com/pysathq/pysat`, which is *PySAT*, "A toolkit for SAT-based
  prototyping in Python" — a Boolean satisfiability library with no connection to heliophysics. The
  heliophysics pysat, the PyHC core package, lives at `https://github.com/pysat/pysat` (the PyHC
  registry's `projects_core.yml` gives that URL), so the value carried before this refresh pointed at
  a different piece of software entirely. Repointing the URL rather than dropping the entry was
  considered and rejected: a search of current pysat found no reference to ApexPy in its source,
  tests or documentation, and it is an instrument-data-management framework rather than a
  coordinate-transform peer, so it satisfies neither the similar-task test nor the dependency test. The relationship that motivated the entry is
  real but sits one package over — the PyHC overview paper's 2018 statement that "pysat … uses …
  AACGMv2 and apexpy for magnetic coordinates" describes what is today implemented in
  **pysatMissions**, which is recorded in Field 30. The entry was therefore dropped rather than
  repointed, and this note keeps both the wrong-project finding and the reason a corrected URL would
  not have earned a place, so neither has to be rediscovered.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/pysat/pysatMissions
- https://github.com/klaundal/lompe
- https://github.com/klaundal/pyAMPS

**Notes:** The HSSI record held no interoperable software before this refresh, and a previous
extraction proposed NumPy, pysat and SpacePy on the reasoning that ApexPy "is designed to interoperate
with the PyHC ecosystem". That reasoning does not meet the bar — NumPy is a generic dependency that
distinguishes nothing, and ecosystem membership is never sufficient by itself. Each entry below rests
instead on a specific artifact in the other package.

- **pysatMissions** — the clearest case. It declares an `apexpy` optional-dependency extra
  (`apexpy = ["apexpy"]` in its `pyproject.toml`) and ships an adapter,
  `pysatMissions.methods.magcoord.add_quasi_dipole_coordinates(inst, ...)`, whose module docstring
  reads "Routines for projecting aacgmv2 and apexpy coords onto pysat instruments" and which takes a
  `pysat.Instrument` and adds ApexPy-computed quasi-dipole latitude, longitude and magnetic local
  time to it. Its documentation lists "Import magnetic coordinates through apexpy and aacgmv2" as a
  main feature. This is an adapter that carries ApexPy's output into another package's data model —
  exactly the exchange the field asks for. It is also where the historical pysat↔ApexPy relationship
  now lives, which is why pysat itself is not listed: the adapter is in the extension, not in the
  core package.
- **lompe** — Local Mapping of Polar Ionospheric Electrodynamics. It declares `apexpy` as a required
  runtime dependency in its `pyproject.toml` and its README lists ApexPy first among the modules a
  user must install, linking this repository. ApexPy supplies the magnetic coordinate frame and base
  vectors that lompe's electrodynamics inversion is formulated in.
- **pyAMPS** — the AMPS empirical model of high-latitude ionospheric currents, by an ApexPy co-author.
  It pins `apexpy>=1.0` in `requirements.txt`, its README lists "apexpy (magnetic coordinate
  conversion)" as a dependency, and `pyamps/sh_utils.py` imports ApexPy and calls its public API
  directly (`apexpy.Apex(epoch, refh=h_R)`, then `geo2qd`, `geo2apex` and `basevectors_apex`).

These three are downstream consumers rather than bidirectional adapters, which is worth stating
plainly: each imports ApexPy and uses its results inside its own data structures. They are recorded
because each is a peer heliophysics tool — none would make sense in a non-scientific application —
and each demonstrates the joint operation the field describes with a citable artifact.

**Considered and not selected:**
- **NumPy** — the package's only runtime dependency, and generic infrastructure. Being a dependency
  is not interoperability.
- **pysatSeasons** — references ApexPy only in a demonstration script (`demo/cosmic_and_ivm_demo.py`)
  and the matching documentation example. Demonstration name-drops do not qualify.
- **pysat (heliophysics)** — no reference to ApexPy in its current source; the exchange runs through
  pysatMissions. See Field 29.
- **OCBpy** — a plausible-looking candidate by ApexPy's maintainer that does *not* qualify: it depends
  on `aacgmv2`, not ApexPy, and mentions apex coordinates only in a docstring describing where its
  boundary locations are expressed. Recorded so it is not proposed again.
- **AACGMV2** — a similar-purpose alternative that recommends ApexPy for a capability it lacks, with
  no data exchange between them. That is a Field 29 relationship, and it is recorded there.

### 31. Related Instruments (OPTIONAL)
Not applicable — the software is instrument-agnostic.

**Notes:** A documented omission, which is the correct outcome here rather than a gap. ApexPy reads,
parses, calibrates and processes no instrument's data: its inputs are geodetic coordinates,
altitudes and times supplied by the caller, and its outputs are coordinates, base vectors and field
magnitudes. A search of the repository for mission, instrument and observatory names turns up four
kinds of match, none of them a supported instrument: the *EOS* volume citation carried in the
comment headers of both `fortranapex/apex.f90` and `fortranapex/magfld.f90`, together with
`apex.f90`'s remark that the WGS-1984 spheroid "is used to position current satellite magnetic
data"; the upstream authors' institutional addresses in the vendored `fortranapex/readme.txt` (U.S.
Naval Research Laboratory, and High Altitude Observatory at the National Center for Atmospheric
Research); the word "instrument" used generically and unnamed in the documentation examples ("the
L-shells seen by a given instrument", "measured by different instruments"); and the substring
"mission" inside "permission" in the licence and the code of conduct and inside "submissions" in
`AUTHORS.rst`. Separately, the one named platform anywhere in the repository is the International
Space Station, which appears solely as a worked example — see Field 32, where it is recorded as a
deliberate non-selection.

The field asks for instruments the software is *designed to support*, and a general-purpose
coordinate library designed to work with data from any platform supports none specifically. Because
nothing here is related, nothing needed resolving against the SPASE-backed controlled vocabulary; no
value may ever be entered without a `https://spase-metadata.org/` identifier.

### 32. Related Observatories (OPTIONAL)
Not applicable — the software is observatory- and mission-agnostic.

**Notes:** The same evidence and the same reasoning as Field 31. ApexPy converts coordinates for any
location on or above Earth and is not built around any mission's data products, conventions or
archive. Selecting `Observatory/Mission-specific` in Field 17 would have required a named
mission here; neither applies.

*The International Space Station — considered and deliberately not recorded.*
`docs/examples/ex_apexh.rst` computes the L-shell of a single ISS position, and it is the one named
platform in the repository, so a future agent will meet it. It is a demonstration: the position is
three hard-coded numbers (9.8° latitude, 142.2° longitude, 419 km altitude) chosen to make
`geo2apex` and `get_apex` concrete, the package reads no ISS data product and implements nothing
specific to the platform, and the same two calls accept any other position the caller supplies. That
is exactly the tutorial mention the designed-to-support test excludes, so the vocabulary row
`International Space Station` (https://spase-metadata.org/SMWG/Observatory/ISS) is left unselected
even though it exists and would resolve cleanly.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/aburrell/apexpy/eed96cf34d8256fbf37a3818c4b696eb802b0a4a/docs/apexpy.png

**Notes:** The image is `docs/apexpy.png` at the pinned revision — the ApexPy logo, described in the
README's own alt text as "yellow magnetic field lines surrounding the Earth's surface, which is
blue". The URL delivers the image itself rather than a page about it: it answers 200 with
`content-type: image/png` and 27,209 bytes, sha256
`1d95b7e6df41ab102dda5ba135e6d7eed2e8e8fab74b103e2250944e8c1bcc81`, byte-identical to the file in the
repository at that commit. That check is worth keeping in mind for raw GitHub URLs generally, which
can answer 200 with `text/plain` when the path holds an LFS pointer instead of an image. It is 106
characters, within the 200-character URL limit.

This replaces the form the record previously held,
`https://github.com/aburrell/apexpy/blob/main/docs/apexpy.png?raw=true`, which is what `README.rst`
uses. **The replacement was made for durability, not as a repair.** That blob URL was still serving
the byte-identical image at the time of this refresh — same 27,209 bytes, same sha256 — so a future
agent must not read the swap as evidence that the old link had gone dead. What made it worth
replacing is that it is fragile in two independent ways: it is a GitHub HTML *blob* page that serves
the image only via the `?raw=true` redirect, so it depends on a rendering behaviour rather than on
content delivery; and it is pinned to the movable `main` branch, so it silently changes meaning or
breaks if the file is moved, renamed or replaced. The commit-pinned `raw.githubusercontent.com` form
resolves directly to image bytes and cannot drift. Prefer this shape for any future logo value.
