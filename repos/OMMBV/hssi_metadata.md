# HSSI Metadata Extraction Results

**HSSI Software ID:** 4409f409-077b-48c2-9421-b1802255499f
**Repository:** https://github.com/CosmicStudioSoftware/OMMBV
**Source Revision:** e4b36778fd99ed01b9d68d2d565761937a9fa4a6
**Extraction Date:** 2026-09-08
**Validation Date:** 2026-09-08
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

Every claim below about the software's own files is read at the pinned revision
`e4b36778fd99ed01b9d68d2d565761937a9fa4a6`, which is the commit the `v1.1.0` tag points at and the
tip of the default branch as of this extraction. Every `path:line` citation in this file is a
location in that tree. The tree contains 59 tracked files.

OMMBV is a small, computational library with an unusually wide gap between what it *is* and what it
*is used for*. What it is: 1,261 lines of Fortran across three files that evaluate a geomagnetic
field model and step along field lines, wrapped in a Python package of eight modules — an
`__init__.py` plus the seven that `docs/api.rst` documents — exposing a vector basis, apex- and
footpoint-location functions, coordinate/vector conversions, and drift/field mapping scalars. It
reads no files, writes no files, fetches nothing, and draws no plots. Several fields below are
therefore correctly empty, and each of those emptinesses is argued from a mechanical check rather
than left as an unexamined blank.

Two facts shape the rest of this file and are stated once here.

**The software was renamed twice, and the concept DOI predates the current name.** The lineage is
`rstoneback/pysatMagVect` → `rstoneback/OMMBV` → `CosmicStudioSoftware/OMMBV`. This is proven rather
than inferred: GitHub's rename redirect resolves the old path `rstoneback/pysatMagVect` to
`full_name: CosmicStudioSoftware/OMMBV` with the identical `created_at` of `2018-06-21T20:49:03Z`
and `fork: false`, and the pin's ancestry contains a former top-level package directory
`pysatMagVect/` (with its own `__init__.py`, `_core.py`, `_coords.f`, `igrf12.f`, `satellite.py`,
`version.txt` and tests) that was later renamed to `OMMBV/`. The intermediate spelling is attested
by the Zenodo deposit title for v1.0.0, `rstoneback/OMMBV: v1.0.0`
(`https://doi.org/10.5281/zenodo.5804083`). A `pysatMagVect` distribution remains on PyPI at
version 0.4.0. This single fact explains why a 2018 concept DOI predates the OMMBV name, why the
pysat coupling runs as deep as it does, and why one of the most substantive independent references
to this software (Field 27) is findable only under the former name. A future agent searching the
literature or the package indexes for "OMMBV" alone will miss the first three years of the project.

**There is no wiki.** The repository's metadata advertises `has_wiki: true`, but the wiki repository
`https://github.com/CosmicStudioSoftware/OMMBV.wiki.git` does not exist (`git ls-remote` on it
returns `Repository not found.`). No wiki content bears on the version description (Field 12) or the
documentation link (Field 24).

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The placeholder form is the catalogue-wide convention for this campaign and is not a gap to be
filled by inference. No submitter identity appears in the repository, the DOI record, or the PyHC
registry entry, and none is invented here.

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.1299374

This is the Zenodo **concept** DOI, and the project itself endorses exactly this string.
`docs/citing.rst` names it twice — once in prose,

> * Stoneback, R. A., J. H. Klenzing,  G. Iyer. (2025). Orthogonal Multipole Magnetic Basis Vectors (OMMBV) v1.1.0. Zenodo. https://doi.org/10.5281/zenodo.1299374

The same DOI appears again inside that file's `@Misc` BibTeX block, as both the `doi` and the `url`
entry. There is nothing contested here: the project's citation guidance and the recorded value agree.

The DataCite record for this DOI corroborates it as the concept-level identifier: it was registered
2018-06-27, carries 15 `HasVersion` children (one per release), reports `version` `v1.1.0` issued
2025-04-07, and its publisher is Zenodo. Its single non-version relation is
`IsSupplementTo https://github.com/CosmicStudioSoftware/OMMBV/tree/v1.1.0`, which is the signature
of the automated GitHub release hook rather than a manual upload — relevant below because it means
the Zenodo-derived fields are machine-generated from `.zenodo.json` and the release tag.

The release-specific DOI `https://doi.org/10.5281/zenodo.15170693` was considered and rejected for
this field: DataCite records it as `IsVersionOf 10.5281/zenodo.1299374`, so it identifies one
release rather than the software as a work. It belongs in Field 12 as the version PID, and is
recorded there. The `README.md:10` badge points at `https://zenodo.org/badge/latestdoi/138220240`,
a redirect service rather than a citable identifier, so it is not used either.

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/CosmicStudioSoftware/OMMBV

Corroborated from three independent directions: the DataCite record's `IsSupplementTo` relation
points into this repository; the PyHC registry entry's `code:` field is this exact string; and
GitHub reports the repository's `full_name` as `CosmicStudioSoftware/OMMBV`. The repository is not
archived, not disabled, not a fork, and its default branch is `main`.

`setup.cfg` declares `url = https://github.com/CosmicStudioSoftware/OMMBV/` with a trailing slash,
and the PyPI project metadata for `OMMBV` gives the same trailing-slash form as its `home_page`.
The slashless form recorded here is the canonical one GitHub itself reports and the one the PyHC
registry uses. The two former repository paths in the rename chain (see the scope note) both resolve
here through GitHub's redirect, but a redirect is not a durable identifier and neither is recorded.

### 4. Software Functionality (RECOMMENDED)

**Values:**
- Coordinate Transforms
- Coordinate Transforms: Ionospheric
- Coordinate Transforms: Magnetospheric
- Coordinate Transforms: Mission-Specific
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Field-line Tracing
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing

Every value is written fully qualified as `Parent: Child` because 13 subcategory names recur under
more than one parent in this vocabulary, and a bare child name resolves ambiguously.

**One of these values is a correction rather than a judgement call.** The catalogue carried
`Models and Simulations: Field-line Tracing` without its top-level parent `Models and Simulations`.
The taxonomy rule is that a subcategory always carries its parent, so the parent's absence was a
parentless-child defect; `Models and Simulations` is recorded to repair it, and is not a
discretionary choice.

**The core values and their evidence.** `Coordinate Transforms` with `Ionospheric` and
`Magnetospheric`: the zonal / field-aligned / meridional triad the package computes is a magnetic
coordinate basis for ionospheric plasma (`README.md:56-78` defines all three directions), and the
mapping runs along field lines through the magnetosphere (`README.md:33-34`,
"Calculations may be performed / at the magnetic equator and then mapped throughout the magnetosphere, as needed.").
`Data Processing and Analysis` with `Field-line Tracing`, and `Models and Simulations: Field-line
Tracing`: `README.md` has a dedicated "Field-Line Tracing" section, and `OMMBV/trace.py` implements
it — `field_line_trace`, `full_field_line`, `apex_location_info`, `footpoint_location_info` — by
coupling the geomagnetic field model into a SciPy integrator. Tracing is both a processing operation
on a caller's coordinates and a computation over a field model, so both parents' children apply.

**Three of these values need their own case.**

*`Coordinate Transforms: Mission-Specific`.* `README.md:134-136` describes the capability directly:
"Supports expressing a vector known in one basis into the same vector / expressed in another basis.
This supports translating measurements made in a / spacecraft frame into frames more relevant for
scientific analysis." `OMMBV/satellite.py`'s public `add_mag_drift_unit_vectors` projects the basis
onto a spacecraft frame supplied as `sc_xhat_*`/`sc_yhat_*`/`sc_zhat_*` columns, and the metadata it
attaches is written in an instrument frame (see Field 31). Spacecraft-frame and instrument-frame
transforms are what this subcategory names.

*`Data Processing and Analysis: Analysis`.* The package computes derived physical quantities rather
than merely reformatting inputs — apex height and apex location, footpoint location, and the
equipotential-field-line scaling factors of `scalars_for_mapping_ion_drifts` — and it quantifies its
own uncertainty by comparing two independent derivation paths (`README.md:80-99`). This is the
subcategory most often missed, and it applies.

*`Models and Simulations: Empirical`.* The package vendors and compiles the IAGA IGRF-14 spherical
harmonic synthesis routine as `ommbvfortran/igrf14.f` (729 lines), builds it into an extension
module, and lists it in the package's public exports at `OMMBV/__init__.py:25`
(`__all__ = ['igrf', 'fortran_coords', 'sources', 'satellite',`). `README.md:114-119` states that
"the International Geomagnetic / Reference Field (IGRF) is coupled into SciPy's odeint", and
`README.md:90-99` presents IGRF-based results as OMMBV output. An empirical geomagnetic reference
field is the canonical example of this subcategory. The counter-case, recorded because it is
genuine: `docs/api.rst` documents only the seven Python modules and not the compiled `OMMBV.igrf`,
so the field model is an internal engine rather than an advertised model product, and a searcher
looking for an empirical-model *package* is better served by the catalogue's dedicated IGRF entries.
On balance the software does ship and evaluate an empirical model, and exports it, so the value is
recorded.

**Considered and rejected, with reasons.** These are recorded so a later refresh does not re-derive
them.

- *All of `Data Visualization` and its children.* Mechanical zero: `git grep -Pcni
  "matplotlib|pyplot|plotly|savefig"` at the pin, over the pathspecs `'*.py' '*.rst' '*.txt'
  '*.toml' '*.cfg'`, matches no files. The two uncertainty figures under `docs/images/` were
  produced outside this repository; the repository ships no plotting code at all.
- *`Data Processing and Analysis: Data Access and Retrieval`.* Zero fetching code; see the pattern
  and its seven doc-comment matches under Field 17.
- *All of `Mission-related` and its children.* Tempting, because `OMMBV/satellite.py:1` is
  `"""Provide support for adding OMMBV to NASA Ionospheric Connections Explorer."""` and
  `README.md:36-44` names three missions. Rejected on the distinguishing test: this category is for
  software that is *part of* a mission's ground system, and OMMBV has no ingest, no packet handling,
  no archive, no calibration pipeline and no operations code. It is a general library that missions
  consume. Listing it here would make it indistinguishable from actual mission ground software.
- *All of `Servers and Environments` and its children.* No server, no container image, no
  Dockerfile, and no parallel-computing dependency in the tree.
- *`Models and Simulations: Theory`.* `ommbvfortran/sources.f` does provide analytic field sources
  (`subroutine dipole_field`, `subroutine linear_quadrupole`), and the 2025 reference publication
  derives the basis analytically. Rejected because those subroutines exist to validate the numerics
  against an exact solution, they are not part of the documented API, and the label would present a
  numerical field-line tracer as an analytical-solutions package.
- *`Models and Simulations: Physics-Based`.* Rejected as double-counting: the only physics engine in
  the package is the vendored empirical field model, already covered by
  `Models and Simulations: Empirical`, and the equipotential-field-line assumption behind the
  mapping scalars is an assumption inside a geometry calculation rather than a physics-based model.
- *`Coordinate Transforms: Planetary`, `: Solar`, `: Heliospheric`.* Nothing solar or heliospheric
  is in the tree, and the planetary case fails for the reason given under Field 5: the only real
  field model shipped is Earth's, and the reference surface is WGS84.

### 5. Related Region (RECOMMENDED)

**Values:**
- Earth Atmosphere
- Earth Ionosphere
- Earth Magnetosphere
- Earth Thermosphere

The Region vocabulary is **flat** — every row is a top-level value with no parents and no children.
A coarse value therefore never implies a fine one and a fine one never implies its coarse relative;
"X encompasses Y" is not an argument that can be made in this field.

**`Earth Ionosphere` and `Earth Thermosphere`.** Both rest directly on the software's own
description rather than on inference. `README.md:12-13` opens
"The motion of plasma in the ionosphere is the result of forcing from neutral / winds, electric
fields, ..."; `README.md:24-27` explains that footpoint scaling "is critical for understanding / how
neutral atmosphere winds at low altitudes (120 km for coupling with / E-region ionosphere) will be /
expressed either at the satellite location or at the magnetic equator"; and `README.md:62-63` calls
ion-neutral coupling "the major driver of / the ionosphere". The DataCite record's subject terms
include both `Ionosphere` and `Thermosphere`, and both words are already among the recorded keywords.
An altitude of 120 km is thermospheric, which is what carries `Earth Thermosphere` specifically.
That altitude is corroborated from outside the repository too: the published application of this
software (Field 27) maps C/NOFS ion drift velocity to a foot point at 120 km, so it is the altitude
at which the software is actually used and not only the one its documentation cites.

**`Earth Magnetosphere`** rests on `README.md:33-34` (quoted under Field 4): mapping runs from
ionospheric altitudes along field lines to the magnetic equator and back, which is a magnetospheric
path.

**The coarse `Earth Atmosphere` is kept, and dropping it was seriously considered.** The case
for removal: the field guidance is explicit that the most specific applicable region is preferred
over a broad one, and that the five coarse values (of which `Earth Atmosphere` is one) should not be
a default. With `Earth Ionosphere` and `Earth Thermosphere` both recorded, the coarse value adds no
information about where this software applies.

It is kept for two reasons that outweigh that. Because the vocabulary is flat, removing it genuinely
removes OMMBV from any listing keyed on the coarse region, and a reader who arrived from that listing
would not have been misled. And the neutral-atmosphere coupling the software is built for is not
confined to the thermosphere as a matter of physics, even though 120 km is the lowest altitude the
documentation cites. The two specific regions stand on their own evidence either way.

**Considered and rejected, with reasons.**

- *`Earth Lower and Middle Atmosphere`.* The lowest altitude the software's own documentation cites
  is 120 km, above the mesopause. This value is also the one that a naive reading of the PyHC
  registry tag would produce, which is why the tag was tested rather than inherited: the registry
  entry carries `keywords: ["ionosphere_thermosphere_mesosphere","specific"]`, a PyHC facet tag that
  propagates across a whole cohort of registry entries. Tested component by component against this
  software, its ionosphere and thermosphere parts are supported by the text quoted above and its
  mesosphere part is not. `specific` is a scope facet, not a subject or a region at all.
- *`Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`, `Earth Magnetotail`,
  `Earth Magnetosheath`, `Earth Auroral Subregion`.* `README.md:33-34` says "throughout the
  magnetosphere" without qualification, and the code imposes no latitude or altitude bound that
  would select a subregion. In a flat vocabulary, picking one would be a guess dressed as precision.
- *`Planetary Magnetospheres` and the per-planet rows.* The reference publication's claim is about
  multipole magnetic fields in general, and `ommbvfortran/sources.f` does ship analytic dipole and
  linear-quadrupole field sources that are not Earth-specific. But those are idealised validation
  fields; the only real field model vendored is IGRF, and the geodetic reference surface is WGS84
  (`README.md:126-131`). Both are Earth. There is no planetary field model and no planetary
  reference surface, so the generality is a property of the mathematics rather than of the shipped
  software.
- *`Chromosphere`, `Corona`, `Photosphere`, `Solar Interior`, `Solar Environment`, `Solar Wind`,
  `Interplanetary Space`, `Heliosheath`.* Nothing solar or heliospheric appears anywhere in the
  tree.

### 6. Authors (MANDATORY)

- **Author: Russell Stoneback**
  - **Identifier:** https://orcid.org/0000-0001-7216-4336
  - **Affiliation:** Cosmic Studio — no identifier
  - **Affiliation:** Stoneris — no identifier
- **Author: Jeff Klenzing**
  - **Identifier:** https://orcid.org/0000-0001-8321-6074
  - **Affiliation:** Goddard Space Flight Center — https://ror.org/0171mag52
- **Author: Gayatri Iyer**
  - **Identifier:** https://orcid.org/0000-0002-0229-8125
  - **Affiliation:** The University of Texas at Dallas — https://ror.org/049emcs32

All three ORCIDs were checked against the ORCID public API on 2026-09-08 and the names on the iDs
match: `0000-0001-7216-4336` is Russell Stoneback, `0000-0001-8321-6074` is Jeff Klenzing,
`0000-0002-0229-8125` is Gayatri Iyer.

**The record is richer than the repository, and that is deliberate.** `.zenodo.json` at the pin
lists the same three creators, but gives an ORCID and an affiliation only for Stoneback and
Klenzing; its third entry is `{"name": "Iyer, Gayatri"}` with no ORCID and no affiliation. The
DataCite record, being generated from that file, has the same gap. So the iD and the University of
Texas at Dallas affiliation recorded here for Gayatri Iyer come from the catalogue record rather
than from the repository, and they are the named delta to preserve: a future extraction that reads
only the repository will appear to find "less" and must not treat that as a correction. Likewise the
`Stoneris` affiliation for Stoneback has no counterpart in `.zenodo.json`; the commit history
corroborates it (below), and it is retained.

**No fourth author exists.** The commit identity table for the pin's full 980-commit history
resolves to exactly three people, and each identity was attributed individually rather than by
surname:

| Identity as recorded in the commits | Commits | Person |
|---|---|---|
| `Russell Stoneback <rstoneba@utdallas.edu>` | 615 | Russell Stoneback |
| `rstoneback <rstoneba@utdallas.edu>` | 326 | Russell Stoneback (same address, handle spelling) |
| `jklenzing <jklenzing@gmail.com>` | 17 | Jeff Klenzing |
| `Russell Stoneback <github@cosmicstudio.io>` | 8 | Russell Stoneback |
| `Jeff Klenzing <jklenzing@gmail.com>` | 7 | Jeff Klenzing (same address) |
| `Russell Stoneback <github@stoneris.com>` | 5 | Russell Stoneback |
| `Gayatri012 <33297781+Gayatri012@users.noreply.github.com>` | 2 | Gayatri (see caveat) |

The seven rows sum to the pin's full commit count, so nothing is unattributed. Stoneback's four
identities collapse on two grounds: two share the address `rstoneba@utdallas.edu` and differ only in
whether the name field holds his name or his handle, and the other two are the two company domains
`cosmicstudio.io` and `stoneris.com` — which is independent corroboration for both of the recorded
affiliations, `Cosmic Studio` and `Stoneris`. Klenzing's two identities share
`jklenzing@gmail.com`. The `Gayatri012` identity is a GitHub noreply address whose numeric prefix
`33297781` matches the GitHub account of that login, so the commits are attributable to that
account; the account's display name carries no surname, so the link from `Gayatri012` to Gayatri
Iyer rests on the `.zenodo.json` and DataCite creator lists rather than on the commit metadata
itself. The repository has no `.mailmap` at the pin and none was ever added, so no maintainer-curated
identity mapping exists to consult.

**Cross-checks that add nothing new.** `setup.cfg` declares a single `author = Russell A. Stoneback`;
`pyproject.toml` declares a single maintainer, `{name = "Russell Stoneback", email = "contact@cosmicstudio.io"}`;
PyPI reports the same author string. There is no `CITATION.cff` at the pin. None of these name a
fourth person, and the middle initial in `Russell A. Stoneback` is a fuller form of the same name
rather than a different one — the recorded `Russell Stoneback` matches the ORCID record and the
DataCite creator entry, and is retained.

**Negative research on the two identifier-less organizations.** Neither `Cosmic Studio` nor
`Stoneris` has a ROR. A ROR API search for "Cosmic Studio" on 2026-09-08 returned only fuzzy
matches on the word "Studio" — none of them this company — and a search for "Stoneris" returned
nothing, against a control query that correctly returned nothing for a nonsense string. Both should
stay identifier-less; do not re-propose a ROR for either. Note also that a small private company is
exactly the case ROR does not generally cover, so this is unlikely to change.

### 7. Software Name (MANDATORY)
- **Name:** OMMBV

The acronym is the name the project uses everywhere it names itself: it is the repository name, the
PyPI distribution name, the `[project] name` in `pyproject.toml`, the `[metadata] name` in
`setup.cfg`, the PyHC registry `name:`, and the wordmark in the logo. The expansion is *Orthogonal
Multipole Magnetic Basis Vectors*, which appears as the top-level heading of `README.md:6`
(`# Orthogonal Multipole Magnetic Basis Vectors (OMMBV)`) and inside the citation string in
`docs/citing.rst`. The acronym rather than the expansion is recorded because that is what the
project calls itself and what a searcher will type; the expansion is carried in the description.

The DataCite record's title is `CosmicStudioSoftware/OMMBV: v1.1.0`. That form is the Zenodo release
hook's automatic `<owner>/<repo>: <tag>` construction, not a name the project chose, and is rejected
as a Field 7 value. The former name `pysatMagVect` (see the scope note) is historical and is not a
current name.

### 8. Description (MANDATORY)

The motion of plasma in the ionosphere is the result of forcing from neutral winds, electric fields, as well as the orientation of those fields and forces relative to the background magnetic field. OMMBV (Orthogonal Multipole Magnetic Basis Vectors) calculates directions (unit vectors) based upon the geomagnetic field that are optimized for understanding the movement of plasma, the mapping of electric fields, and coupling with the neutral atmosphere. This system is the first to remain orthogonal for multipole magnetic fields as well as when including a geodetic reference surface (Earth). OMMBV also includes methods for scaling ion drifts and electric fields at one location to any other location along the same field line, typically to either the magnetic footpoint or to the magnetic equator. The software is used by NASA's ICON Explorer Mission, NOAA/NSPO COSMIC-2 constellation, and is being incorporated into C/NOFS satellite analysis routines.

This is the project's own prose. The first three sentences reproduce `README.md:12-19` with the
README's hard line wrapping removed; the fourth condenses `README.md:21-24`; the closing sentence
condenses the mission paragraph at `README.md:36-44`. It is retained as written rather than
re-drafted, because it is the maintainers' description of their own software and a stylistic
alternative would not be an improvement.

Two things the condensation drops, recorded so that a future agent recognises them as deliberate
rather than as omissions to repair. First, the closing sentence does not mention TIEGCM, although
`README.md:41-42` says OMMBV "is currently being incorporated / into analysis routines suitable for
integrating physics-based models (TIEGCM)"; the sentence is already carrying three missions, and
TIEGCM is a model rather than a mission. Second, the description does not reproduce the README's
explanation at `README.md:28-34` of how equatorial scaling reduces a four-dimensional data
distribution to three — a genuinely distinctive capability, but one that needs a paragraph to state
and would unbalance a summary.

The PyHC registry's description was considered as an alternative and rejected: it is shorter, it is
written in the third person about the package rather than about the science, and it contains a typo
in the expansion of the acronym.

### 9. Concise Description (OPTIONAL)

Orthogonal vector basis and field-line mapping for multipole magnetic fields, optimized for ionospheric plasma dynamics and electric field calculations.

This value is a light edit of the project's own one-line summary — `pyproject.toml:16`
reads `description = "Orthogonal geomagnetic vector basis and field-line mapping for multipole magnetic fields."` —
extended with the application domain, which is what makes it useful as a catalogue subtitle. The
`setup.cfg` `description` is the same sentence wrapped in literal single quotes, an artifact of that
file's formatting rather than a different wording. The GitHub repository description was considered
as an alternative: it is longer, it leads with the expanded acronym (which duplicates Field 7), and
it says "Complete orthogonal vector basis with accurate field-line mapping" — a stronger claim than
the recorded wording, with no advantage as a subtitle. Not adopted.

### 10. Publication Date (RECOMMENDED)
- **Date:** 2018-06-21

The date the repository became public and its first commit landed: GitHub reports `created_at` as
`2018-06-21T20:49:03Z`, and the pin's earliest ancestor commit is from the same day. Because the
rename preserved the repository, this is the first-publication date of the software as a work even
though the software carried a different name on that day.

Two later dates were considered and rejected. The DOI registration date, 2018-06-27, is when Zenodo
minted the concept identifier — six days after publication, and a property of the DOI rather than of
the software. The `publicationYear` in the DataCite record is `2025`, which is the release hook
restating the newest version's year; it is not a first-publication date at all.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Zenodo is the publisher named in the DataCite record for the concept DOI, which is the correct
reading of this field where a DOI exists: the publisher is the agency that issued the persistent
identifier, not the code host. The recorded identifier is Zenodo's own web address, which is the
form the catalogue's shared organization record for Zenodo carries.

Recording a ROR for the publisher in place of this web address was considered and rejected. The
operative reason is independent of whether any such ROR exists: the publisher is a shared
organization record used by many entries, so its identifier is not this software's to change, and
substituting one here would either fail to match the existing record or produce a duplicate — in
either case an edit to a shared row made on one entry's behalf. An earlier version of this note
named a ROR as Zenodo's; that identifier belongs to an unrelated institution and is deliberately
not repeated here, so that it cannot be recovered from this file and re-entered. As a dated
observation about a registry we do not control, a search of the ROR registry on 2026-09-08 returned
no entry for Zenodo at all; a control search for CERN the same day returned results, so the empty
result was a real absence rather than a failed query. Zenodo is hosted by CERN, but the two are
distinct entities, and CERN's ROR would not identify the publisher named in the DataCite record.

### 12. Version (RECOMMENDED)

- **Version Number:** v1.1.0
- **Version Date:** 2025-04-07
- **Version PID:** https://doi.org/10.5281/zenodo.15170693

Every part is corroborated from more than one place. The number: `pyproject.toml:14` is
`version = "1.1.0"`, `OMMBV/version.txt` reads `1.1.0`, `OMMBV/__init__.py:4` is
`__version__ = '1.1.0'`, and PyPI's newest `OMMBV` release is 1.1.0. The `v` prefix follows the
project's own tag and release naming. The date: the `v1.1.0` GitHub release was published
`2025-04-07T20:42:59Z`, the DataCite record for the version DOI reports `2025-04-07` as its `Issued`
date, and `CHANGELOG.md:5` heads the section `## [1.1.0] - 2025-04-07`. The PID: DataCite records
`10.5281/zenodo.15170693` as `IsVersionOf 10.5281/zenodo.1299374`, which is precisely the
concept/version relationship this field expects.

**No version description is recorded, and that is a decision rather than a gap.** One was available
and was drafted: `CHANGELOG.md:6-12` lists seven bullets under the 1.1.0 heading and the GitHub
release body reproduces the same seven, so joining them with semicolons yields a serviceable
description — most notably `Updated to IGRF14`, which is the change that explains why
`ommbvfortran/igrf14.f` is present and `OMMBV/igrf13.f` was deleted. Anyone who wants that text can
reconstruct it from the changelog, which is authoritative about what the release contained.

It is deliberately left unrecorded because of what recording it would cost. Version is stored as a
single attached record rather than as loose columns, so changing any part of it — including adding a
description to an otherwise correct record — replaces the whole record rather than editing it, and
leaves the previous one detached. A purely cosmetic description does not justify that, and the
number, date and PID above are already correct and corroborated. Exactly one version record is
attached to this software, so the multiple-attached-record problem seen elsewhere in the catalogue is
not present here. The durable consequence: this field is complete as it stands, and it should be left
untouched unless the software actually releases a new version — at which point the whole record is
being replaced anyway and a description costs nothing extra.

**Tag and release naming traps, recorded because they will mislead a future agent.** The repository
carries 15 tags and 15 releases. Two of the tags do not follow the `v<semver>` pattern: `0.3.1` has
no `v` prefix, and `v1.01` is a two-digit form whose GitHub release title is `v1.0.1` and whose
changelog heading is `## [1.0.1] - 2022-01-04`. So neither the tag list nor a version sort over it
can be trusted as the version history without reading the changelog. Separately, the `v1.1.0`
release's `name` is just the string `v1.1.0` and carries no descriptive text — the release *body* is
where the changelog bullets live. Do not mistake a release name for a release description in this
repository.

### 13. Programming Language (RECOMMENDED)

**Values:**
- Fortran90
- Python 3.x

This field previously carried `Fortran 2003`, `Fortran 2008` and `Python 3.x`. The evidence below
rejects both of those Fortran rows under every criterion tested, so the only open question was what
should stand in their place; the answer is the single row `Fortran90`, the newest dialect actually
present in the tree. The criterion applied is the field's own — the languages the software is written
in — and every inclusion and exclusion below follows from it.

**The field's own definition, which constrains the criterion.** The field is "The computer
programming languages **most important** for the software", to be filled by selecting "the most
important languages (e.g., Python, Fortran, C)", with the explicit note that "This is not meant to
be an exhaustive list." So the field is not a manifest and not a build-system readout; it is a short
answer to "what is this written in".

**The closed candidate set.** The vocabulary offers 19 rows. Fifteen of them —
`C#`, `C++`, `Fortran 2023`, `Fortran77`, `Fortran90`, `IDL`, `Java`, `Javascript`, `Julia`,
`MATLAB`, `Other`, `Python 2.x`, `Rust`, `SQL`, `Typescript` — plus `C`, `Fortran 2003`,
`Fortran 2008` and `Python 3.x` make up the whole candidate space, and every candidate gets a verdict
below. `Python 2.x` is excluded by `pyproject.toml:20` (`requires-python = ">=3.9"`).
`C#`, `C++`, `IDL`, `Java`, `Julia`, `MATLAB`, `Rust` and `SQL` have no presence in the tree at all
— a case-insensitive search for each finds no file — and are excluded under every criterion.
`Javascript` and `Typescript` are excluded on the same substance but are worth one sentence, because
a careless search does turn up a hit for each and neither is a language this project uses:
`docs/conf.py:229` is the Sphinx comment
`# The name of a javascript file (relative to the configuration directory) that`, and `.gitignore:68`
is the single word `typescript`, an ignore rule for the transcript file `script(1)` writes. No
JavaScript or TypeScript source exists in the tree. `Other` is a fallback for
languages the vocabulary lacks and is not needed. So the live questions are the Fortran row, and `C`.

**What is actually in the tree.** 59 tracked files: 20 `.py`, 8 `.rst`, 7 `.md`, 4 `.yml`, 4 `.txt`,
4 `.png`, 3 `.f`, and one each of `.toml`, `.json`, `.in`, `.cfg`, `.gitignore`, `.coveragerc`,
`Makefile`, `LICENSE` and `meson.build`. The three Fortran files are
`ommbvfortran/_coords.f` (59 lines), `ommbvfortran/sources.f` (473 lines) and
`ommbvfortran/igrf14.f` (729 lines).

**Which Fortran standard the code actually uses — the decisive evidence.** Probing each `.f` file at
the pin for constructs that exist only in the later standards returns nothing in all three files.
The Fortran 2003-and-later probe
(`iso_c_binding|\bclass *\(|\bprocedure\b|\bassociate\b|move_alloc|\babstract\b|\bextends\b|\ballocatable\b`,
case-insensitive) matches 0 lines in `_coords.f`, 0 in `sources.f` and 0 in `igrf14.f`. The Fortran
2008 probe (`do concurrent|^\s*block\b|contiguous|submodule|error stop|\[\*\]`) likewise matches 0
lines in each of the three. Free-form line continuation (`&\s*$`) matches 0 lines in each; all three
files are fixed-form. So neither recorded Fortran row corresponds to anything in the code.

The compiler agrees. Neither `_coords.f` nor `sources.f` compiles at any standard from `f95`
upwards, and the first error in each is not a standard-version issue at all but
`GNU Extension: Nonstandard type declaration REAL*8` — a vendor extension belonging to no Fortran
standard. `igrf14.f` compiles cleanly from `f95` through `f2008` and fails at `f2018` on a single
error about a `DO` termination statement that Fortran 2018 deleted. Both build paths consequently
force the legacy dialect: `meson.build:9` sets `'fortran_std=legacy'`, and `setup.py:21` passes
`'--std=legacy'` through `extra_f77_compile_args`.

**The `Fortran 2008` diagnostics these files do emit are cascade artifacts of the rejected `REAL*8`
declarations, not 2008 constructs — and this is the single most important thing to know before
reopening the field.** Compiling each file with `-std=f2003` and counting error lines shows that
`_coords.f` produces 14 errors of which exactly 1 matches `Error: Fortran 2008`, and `sources.f`
produces 148 of which exactly 5 do. Every one of those six is the same message,
`Error: Fortran 2008: Pointer procedure assignment`. Recompiling at `-std=f2008` drops the totals to
13 and 143 respectively and leaves zero such diagnostics — so the six vanish and account for the
entire difference. Neither file emits any `Error: Fortran 2003` diagnostic at any standard, which is
the direct evidence against the recorded `Fortran 2003` row.

The mechanism is visible in the source lines the diagnostic points at — `_coords.f:54`
(`      latitude(i)=latitude(i)*p`), `sources.f:168`
(`        r(i) = (pos(i) - offs(i)) * 1000.D0`), `sources.f:174` (`        rhat(i) = r(i) / rmag`)
and their peers. Each assigns to an element of a *local* array whose `real*8` declaration the
compiler has just discarded; having lost the array-ness, it re-reads `r(i) = …` as a call and
complains that a function result on the left-hand side needs the pointer attribute. A control
reproduces it exactly: a fixed-form subroutine whose body is a local `real*8, dimension(3) :: r`
plus `r(i) = 1.0D0` yields 3 errors at `-std=f2003`, one of them the pointer-procedure message and
another spelling the cause out as `The function result on the lhs of the assignment at (1) must
have the pointer attribute.`; substituting `double precision, dimension(3) :: r` yields 0 errors at
`-std=f2003` and 0 at `-std=f95`. That second reading doubles as the control for the Fortran 90
claim below: the `::` attribute form itself is accepted at `f95`, so it is the `REAL*8` spelling and
not the `::` syntax that these compilers reject.

One caution for anyone re-deriving this. The control only reproduces when the array is **local**. An
otherwise similar subroutine that declares a *dummy argument* as `real*8 c(12)` and assigns to
`c(1)` produces just the one `GNU Extension: Nonstandard type declaration REAL*8` error and no
pointer-procedure diagnostic at all, because the dummy's shape comes from elsewhere. A control built
that way will appear to refute the cascade explanation when in fact it is testing a different
construct.

**What *is* present is Fortran 90-era syntax, and only in one file.** `sources.f` contains 14 lines
using the `::` attribute-declaration form, twelve of them type declarations (`sources.f:12` is
`      real*8, dimension(3) :: pos`; `sources.f:202` is `      real*8 :: step, mag, scalar`) and two
of them `      external :: igrf14syn`. That form is Fortran 90 and is not valid Fortran 77.
`igrf14.f` contains no `::` at all. `_coords.f` contains exactly one line with `::`, and it is
`Cf2py integer intent(hide), depend(posx) :: num=shape(posx,0)` at `_coords.f:18` — an f2py
directive inside a `C`-prefixed comment line, which is not a Fortran declaration and must not be
counted as one.

**The `C` question.** There is no C in the tracked tree: no `.c`, `.h`, `.pyx`, `.cpp` or `.cc` file
exists at the pin. But `meson.build:1` is `project('OMMBV', 'c',`, `meson.build:7` sets `c_args`,
and `meson.build:12` is `add_languages('fortran', native: false)` — so the build declares C as its
primary language and Fortran as an addition. The C that is actually compiled is entirely generated
or external: three `custom_target`s invoke `numpy.f2py` to generate `igrfmodule.c`,
`sourcesmodule.c` and `fortran_coordsmodule.c`, and the build additionally compiles
`fortranobject.c` out of numpy's own f2py include directory. No OMMBV developer wrote or maintains
any of it. GitHub's own language analysis of this repository reports Python, Fortran and Meson, and
does not report C.

**The three criteria, and where they agree.**

*Criterion A — the languages the software is written in.* This is the field definition's own reading.
It yields `Python 3.x` (20 tracked Python files, the entire public API) and one Fortran row.
It excludes `C`, because generated glue is not something the software is written in.

*Criterion B — every language present in the tracked tree.* Yields the same answer as A. Meson is a
build language and has no vocabulary row; there is still no C file to count. **A and B differ only
in the reasoning, not in the outcome** — worth writing down, because it means the choice between them
never needs to be made for this software and a future agent should not reopen it as though it were
live.

*Criterion C — every language the build declares.* Adds `C` on the strength of `meson.build:1` and
`meson.build:7`, and nothing else.

**The options considered, and why the recorded one won.**

- *Why `Fortran90` with `Python 3.x` is the recorded pair.* It is what Criterion A or B yields, with `Fortran90` as the
  Fortran row. The reason to prefer `Fortran90` over `Fortran77` is that it is the newest dialect
  actually present, so it is the one that tells a reader what they must be able to compile:
  `sources.f` — the largest of the project's own Fortran files, holding the multipole field sources
  and the stepping routines — uses Fortran 90 declaration syntax that a strict Fortran 77 compiler
  rejects, while the Fortran 77-era `igrf14.f` presents no obstacle to a Fortran 90 compiler. One
  row therefore covers the whole Fortran surface.
- *Why not `Fortran77` in its place.* That alternative is defensible on the source form and on the project's own
  classification of these files — all three are fixed-form `.f`, the legacy build path passes its
  flags as `extra_f77_compile_args`, and `meson.build` carries the comment `# .f so no F90 wrappers`
  on lines 44, 63 and 83. Against it: `sources.f` demonstrably is not Fortran 77.
- *Why not both Fortran rows.* Carrying `Fortran77` alongside `Fortran90` would record the genuine split — the vendored
  IGRF routine is Fortran 77-era and the project's own `sources.f` is Fortran 90. Against it: the
  field says explicitly that it is not meant to be exhaustive, and two Fortran rows tell a searcher
  less than one.
- *Why `C` is not added to any of these.* Only Criterion C would add it. Against it: the field asks
  for the most important languages, and generated f2py glue plus a numpy-supplied source file is not
  one of them. A searcher filtering the catalogue for C software would not want this package, and
  GitHub's own analysis does not see C here either.
- *Why the former `Fortran 2003` and `Fortran 2008` rows are gone.* The evidence above rejects
  them, and the rejection is set down here so it is on the record and the two rows are not
  re-proposed: the constructs are absent, no build path permits
  either standard, and the diagnostics that suggested otherwise are artifacts of a vendor extension.

**One honest caveat that survives the decision.** No vocabulary row exactly describes this code,
because the code compiles only in the legacy dialect and relies on the non-standard `REAL*8`
declaration. There is no "legacy Fortran" row. The recorded `Fortran90` is the closest available
approximation, not an exact statement, and that is worth knowing before anyone reopens the question
expecting a clean answer.

`Python 3.x` is not in question under any criterion. `pyproject.toml` classifiers cover Python 3.9
through 3.12 and `requires-python` is `">=3.9"`. Note in passing that the legacy `setup.cfg` still
declares classifiers for 3.8-3.10 and `python_requires = >= 3.5`; where the two files disagree,
`pyproject.toml` is the one the current build uses.

### 14. Reference Publication (OPTIONAL)
- **DOI:** https://doi.org/10.1029/2025JA033911

The recorded publication is **Stoneback, R. A.; Lien, C.-P.; Hsu, C.-T.; Matsuo, T., "Orthogonal
Electrodynamics in Multipole Magnetic Fields", Journal of Geophysical Research (Space Physics), 130,
e2025JA033911 (2025-07)**, DOI **`https://doi.org/10.1029/2025JA033911`** (ESS Open Archive preprint
`https://doi.org/10.22541/essoar.172555374.45544543/v1`, ADS bibcode `2025JGRA..13033911S`).

**Why this paper and this software are the same subject: the paper says so.** Its Introduction
states directly that its results are demonstrated with this software:

> "These results are demonstrated using calculations from the open source software implementation
> of this new basis in Orthogonal Multipole Magnetic Basis Vectors (OMMBV) (Stoneback et al., 2022)."

That sentence is read from the published article itself, and it settles both halves of the question
at once — that this is the method paper for this software, and that it cites it. The cited year 2022
is consistent with the Zenodo concept record the paper's reference list points at.

**Three indirect links corroborate it,** and each is kept because it was established independently
of the full text. First, the paper's reference list formally cites OMMBV's Zenodo concept record — a
citation query on that record returns this paper. Second, its full text is the only work in ADS that
contains the phrase "Orthogonal Multipole Magnetic Basis Vectors", the software's expanded name;
that hit is narrower evidence than it looks, for the word-order reason recorded under Field 27.
Third, its abstract restates the README's claims nearly
clause for clause: it presents "the first orthogonal basis vectors and coordinates for multipole
magnetic fields", names the "zonal, field-aligned, and meridional directions", states that the basis
is "optimized for electrodynamics as the meridional and zonal vectors are vertical and horizontal at
the magnetic equator", and reports that "Comparison of two different basis derivations demonstrates
low basis uncertainty" — which is the two-calculation-path uncertainty argument of
`README.md:80-99`. The lead author's affiliation on the paper is `Cosmic Studio, Plano, TX, USA;`,
the same organization recorded as his affiliation in Field 6.

**Why the repository cannot corroborate it.** The pinned tree is from 2025-04-07 and the paper is
from 2025-07, so the paper postdates the pin. `docs/citing.rst` at the pin names only the Zenodo
DOI and does not mention any publication. A repository-only extraction at this pin therefore cannot
find this paper at all; it is discoverable only from the literature. That is not evidence against
the paper — it is a dating artifact — but it does mean the project has not yet designated the paper
as a preferred citation, and a future refresh should check whether `docs/citing.rst` has since been
updated to name it.

*Why it belongs in this field.* The field is "the DOI for the publication describing the software",
and this is that publication: it derives and validates the method the software implements, and it
cites the software. This is the relation Field 14 exists to express, and using it keeps the
distinction the two publication fields draw — the paper that describes the software, as against
papers that merely cite or use it.

*The alternative considered: leave this field empty and record the paper under Field 27 instead.*
Field 27 does cover publications that "describe, cite, or use the software", so the paper would not
have been misfiled there. The argument for it was that the project's own citation guidance names only
the Zenodo DOI, so promoting the paper to reference-publication status is our judgement rather than
the maintainers'. The argument against, which prevailed, is that it discards information: filed under
Field 27 the paper would sit undifferentiated beside a paper that merely applies the software, and a
reader would lose the fact that one of them is the method paper.

*Recording it in neither field* was also rejected. The paper exists, concerns this software
unambiguously, and citing it is useful to anyone who reaches this record.

**The paper appears in only one of the two fields.** Listing the same work in both Field 14 and
Field 27 is the duplication the two-field split exists to prevent, so Field 27 below deliberately
does not carry it, and says so where the paper would otherwise be listed.

**A durable note on access, and on what is genuinely unreachable.** The published article is
**Open Access** and renders in full in a browser. The Introduction sentence quoted above and every
abstract clause quoted with it were read from the article page, whose own metadata — Journal of
Geophysical Research: Space Physics, volume 130, issue 7, e2025JA033911, first published 01 July
2025, authors R. A. Stoneback, C.-P. Lien, C.-T. Hsu and T. Matsuo — matches the citation recorded
above in every part. The one thing that is not reachable is the ESS Open Archive **preprint** at
`https://doi.org/10.22541/essoar.172555374.45544543/v1`: `essopenarchive.org` serves an active
bot-detection interstitial instead of the document, and it does not clear on its own. That is a
property of that host rather than a paywall, and it costs nothing — a preprint of an already
open-access article is the wrong target. Europe PMC has no record of this DOI, which is the expected
coverage gap for an AGU/Wiley title and is not evidence about access. Anyone who needs the
acknowledgements or a data-availability statement — for Field 25 or 26, say — should open the
published version. Note that this software's own funders are taken from its README rather than from
any paper, for the reason given under Field 25.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License

Corroborated five ways at the pin and beyond it: the `LICENSE` file's first line is
`BSD 3-Clause License`; GitHub reports the repository's license `spdx_id` as `BSD-3-Clause`; the
DataCite record's rights entry is `BSD 3-Clause "New" or "Revised" License` with
`rightsIdentifier` `bsd-3-clause`; `meson.build:3` declares `license: 'BSD-3'`; and both
`pyproject.toml` and `setup.cfg` carry the classifier `License :: OSI Approved :: BSD License`.
Nothing dissents.

**There is deliberately no license URI recorded.** The catalogue's license value is a reference to a
shared license record that carries its own canonical URL, so a license URI is not a property of this
software and cannot be set per entry. A previous version of this dossier recorded
`https://opensource.org/licenses/BSD-3-Clause` as a "License URI"; that string is the `rightsUri` in
the DataCite record, and while it is a correct URL for the license, it is not a field of this
software's metadata. It is noted here so its disappearance from this file is not read as data loss.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values:**
- coordinate transformation
- electric field
- electric field mapping
- electrodynamics
- field aligned
- field line tracing
- geomagnetic field
- heliophysics
- ion drift mapping
- ionosphere
- magnetic field
- magnetic fields
- magnetosphere
- meridional
- multipole
- plasma
- satellite
- thermosphere
- vector basis
- zonal
- igrf
- WGS84
- magnetic coordinates
- ionospheric electrodynamics
- geomagnetic
- plasma physics
- apex

Twenty of these terms are the catalogue's long-standing list for this software; the other seven are
recorded on the evidence set out below. Keywords are the only open vocabulary in this form: an
unrecognised value creates a new term rather than failing. That makes both spelling and completeness
matter, and it matters for every term in the list rather than only for the newer ones, because the
list is written as a whole — each term re-resolves whenever the field is set, so a long-standing term
carries exactly the same term-creation hazard as a new one.

**The twenty long-standing terms, all matching existing terms:** `coordinate transformation`,
`electric field`,
`electric field mapping`, `electrodynamics`, `field aligned`, `field line tracing`,
`geomagnetic field`, `heliophysics`, `ion drift mapping`, `ionosphere`, `magnetic field`,
`magnetic fields`, `magnetosphere`, `meridional`, `multipole`, `plasma`, `satellite`,
`thermosphere`, `vector basis`, `zonal`.

Each of these is supported by the project's own declarations. `pyproject.toml:41-55` declares 13
keywords in hyphenated form (`vector-basis`, `geomagnetic-field`, `magnetic-fields`,
`field-line-tracing`, `meridional`, `zonal`, `field-aligned`, `satellite`,
`electric-field-mapping`, `ion-drift-mapping`, `multipole`, `electrodynamics`, `plasma`);
`setup.cfg` declares 11 of the same; `.zenodo.json` declares 6 in title case (`Magnetosphere`,
`Ionosphere`, `Thermosphere`, `Heliophysics`, `Magnetic Field`, `Electric Field`); and GitHub
declares 15 repository topics. The recorded list is those sources merged and normalised to the
catalogue's lower-case spaced convention.

**Six of the seven newer terms. All six match existing terms, so none of them creates a new
term.**

- `igrf` — the package vendors and evaluates the IGRF-14 synthesis routine and exports it
  (`OMMBV/__init__.py:25`); `README.md:114-119` names the International Geomagnetic Reference Field
  as the field model behind every trace. A reader searching the catalogue for IGRF software should
  find this package, and nothing in the current list would produce that hit.
- `WGS84` — `README.md:126-131` states that the package "Supports the conversion of geographic and
  geodetic (WGS84) into each other / and into Earth Centered Earth Fixed (ECEF)", and the geodetic
  reference surface is part of the software's central orthogonality claim. Recorded with the
  existing term's own capitalisation.
- `magnetic coordinates` — the reference publication states that "Using the orthogonal basis vectors
  a new orthogonal magnetic coordinate system is created", and this is the general term under which
  a reader would look for such a system.
- `ionospheric electrodynamics` — the specific subject of the software and of both associated
  publications; more precise than the recorded `electrodynamics` alone.
- `geomagnetic` — a maintainer-declared GitHub topic that has no equivalent among the recorded
  terms; the recorded `geomagnetic field` is narrower.
- `plasma physics` — a maintainer-declared GitHub topic (`plasma-physics`); the recorded `plasma`
  alone does not cover it.

**The seventh, `apex`.** It matches an existing term, and it names a quantity the software
genuinely computes rather than a system it implements: `OMMBV/trace.py` exposes `apex_location_info`,
and apex height and apex location are among the derived quantities argued under Field 4. It was once
judged too marginal to be worth growing the list for, and the distinction that overturned that
judgement is the one worth keeping
`magnetic apex coordinates` (rejected below) would name a coordinate system this software does not
implement.

**Two candidates declined, which should stay out.**

- `electric fields` (plural) — a maintainer-declared GitHub topic (`electric-fields`) that exists as
  a term distinct from the recorded singular `electric field`. The precedent for carrying both
  numbers exists inside this very record, which holds `magnetic field` and `magnetic fields`, so it
  would have been harmless and symmetric. Declined as too weak in isolation to justify a second
  spelling of a term already recorded.
- `nasa` — a maintainer-declared GitHub topic, declined. It names a funding and operating agency
  rather than a subject, a reader searching for `nasa` is not looking for a magnetic-basis library,
  and the agency is already recorded where it belongs — as a funder in Field 25 and as the operator
  of the mission in Field 32. Keeping the keyword list to subject terms is what makes it useful.

**Considered and rejected, with reasons.**

- `multipole-vectors` — a maintainer-declared GitHub topic, but it has no existing term and would
  create one. It is a hyphenated near-duplicate of the recorded `multipole`, and minting a
  near-duplicate degrades the vocabulary for every other entry.
- `field-line tracing` (hyphenated) — this exists as a term *separate from* the recorded
  `field line tracing`, and the GitHub topic is `field-line-tracing`. Rejected: it is the same
  concept, and the catalogue should not be asked to carry both spellings of every term. Recorded
  here specifically so nobody adds it believing it to be the same value as the one already present.
- `magnetic apex coordinates` — exists as a term, and the package computes apex heights and apex
  locations throughout. Rejected because it would misrepresent what the software is: OMMBV is not an
  apex-coordinate implementation, and the project itself concluded that its vectors and apex-system
  vectors "aren't expected to be the same" (see Field 29). The bare `apex`, which names the computed
  quantity rather than the system, is recorded instead.
- `space weather` — exists as a term. Rejected: the package has no forecasting, no geomagnetic
  indices and no event detection. It is a physics library, not a space-weather tool.
- `icon` — exists as a term. Rejected: the mission belongs in Field 32, where it is recorded with a
  persistent identifier, and the bare word is ambiguous outside this domain.
- `electromagnetism`, `orthogonal magnetic coordinates`, `international geomagnetic reference field`,
  `ecef`, `ion velocity meter`, `geodetic`, `orthogonal basis`, `apex height` — all would create new
  terms. The first three are the reference publication's own ADS keywords and the rest come from the
  README's vocabulary; each is either covered by one of the terms recorded above
  (`ionospheric electrodynamics`, `magnetic coordinates`, `igrf`, `WGS84`) or too narrow to earn a
  new term.

### 17. Data Sources (OPTIONAL)
- **Value:** Not found — evidenced empty

This field is correctly empty because the software retrieves nothing. The available sources in this
vocabulary are `AMDA`, `CDAWeb`, `FTP/FTPS Directories`, `GFZ`, `HAPI`,
`HTTP/HTTPS Directories`, `Madrigal`, `OMNIWeb`, `Observatory/Mission-specific`, `Other`,
`S3/Cloud-aware`, `SSCWeb`, `TAP`, `The Virtual Solar Observatory.`, `VirES`, `WDC` and `das2` —
every one of them a remote archive, service or transport. OMMBV reads no archive and speaks no
protocol, so none of them applies, including `Other`.

The examination, so this is not an unexamined blank. Searching the installable package for any
retrieval machinery —
`git grep -nP "\b(requests|urllib|urlopen|ftplib|http|download|wget|curl)\b"` at the pin over the
pathspec `'OMMBV/*.py'` — returns 7 lines in 2 files, and every one of the seven is a
literature-reference URL inside a docstring or a comment: `OMMBV/_core.py:992` and `:993`, and
`OMMBV/trans.py:168`, `:169`, `:180`, `:204` and `:207`, citing coordinate-conversion write-ups at
epsg.org, oc.nps.edu, danceswithcode.net and ir.lib.ncku.edu.tw. There is no fetching code. The
geomagnetic coefficients the software needs are compiled in from `ommbvfortran/igrf14.f` rather than
downloaded, so even the field model requires no data source at runtime. (The pathspec `OMMBV/*.py`
would also reach nested directories, but `OMMBV/` has no subdirectories at the pin, so its scope is
the eight package modules.)

**One trap recorded rather than acted on.** `tests/test_vitmo.py` hard-codes a validation table
introduced by the comment `# Results from omniweb calculator`. `OMNIWeb` is a value in this
vocabulary, and it is the wrong one here: those are numbers a developer copied into a test fixture
to compare against, not a source the software reads. A future agent must not let that comment
license an `OMNIWeb` value.

**A second trap of the same shape, in the abandoned CI configuration.** `Madrigal` is also a value
in this vocabulary, and `.travis.yml:41` reads `  - pip install madrigalWeb`. It must not license a
`Madrigal` value either. `.travis.yml` is the project's Travis CI configuration, last modified in
2020 and superseded by `.github/workflows/main.yml`; the line installs a client library into a test
environment, and the string `madrigal` appears in no other file in the tree — nothing in `OMMBV/` or
in `tests/` imports it or queries Madrigal. The general rule these two traps illustrate: this
repository's dead CI config names several ecosystem packages the software itself never touches, so a
vocabulary term found only there is not evidence of a capability.

### 18. Input File Formats (RECOMMENDED)
- **Value:** Not found — evidenced empty

### 19. Output File Formats (RECOMMENDED)
- **Value:** Not found — evidenced empty

Both format fields are empty for the same reason, argued once. OMMBV is a pure computational
library: its functions take numeric arrays and dates and return numeric arrays, and it opens no
files in either direction. The format vocabulary offers `CDF`, `FITS`, `HDF5`, `IDL.sav`,
`ISTP-Compliant`, `JSON`, `Other`, `Zarr`, `ascii`, `csv` and `netCDF3/4`; none applies, and
`Other` does not either, because there is no file at all rather than an unlisted one.

The examination. `git grep -cP "\b(open|np\.load|np\.save|loadtxt|savetxt|read_csv|to_csv)\b"` at
the pin over `'OMMBV/*.py'` matches **0 files**. Widening the pattern to include `h5py`, `netCDF4`,
`cdflib` and `fits`, and the scope to `'OMMBV/*.py' 'tests/*.py'`, also matches **0 files** — so
neither the installable package nor the test suite touches a file format. (`OMMBV/` has no
subdirectories at the pin, so the `OMMBV/*.py` scope is exactly the eight package modules.) The one
place data crosses a boundary is `OMMBV/satellite.py`, and it crosses in memory: the functions there
write columns into a caller's in-memory instrument object (see Field 30), which is an object
exchange rather than a file format.

**One format-name search that must not be repeated in its original form, because its zero was an
artifact.** A word-anchored sweep for the format names themselves —
`git grep -liP "\b(CDF|FITS|HDF5|netCDF|Zarr|\.sav)\b"` over `':!*.png'` — returns 0 files, but
that zero is produced by the `\b` anchors rather than by absence: `netCDF4` and `pysatCDF` both
appear in the tree and neither offers a word boundary where the pattern demands one (`netCDF` is
followed by `4`, and `CDF` is preceded by `t`). Repeating the search unanchored and
case-insensitively over the same scope finds the real picture: the only genuine format names in the
tracked text are in **`.travis.yml`**, which is the project's abandoned Travis CI configuration —
line 34 creates a conda test environment including `netCDF4` and `h5py`, and line 43 runs
`  - pip install pysatCDF >/dev/null`. The unanchored sweep's only other hit is `LICENSE:26`, where
"fits" falls inside the word `PROFITS`.

That finding does not change either field's value, and the reason is worth recording. Those are
**test-environment packages in a CI configuration that has not been touched since 2020** and was
superseded by `.github/workflows/main.yml`; they are not formats this software reads or writes.
Nothing in `OMMBV/` or in `tests/` imports any of them — each of `netCDF4`, `h5py` and `pysatCDF` is
confined to `.travis.yml` alone. A future agent re-deriving these fields should search unanchored,
find the same three names, and reach the same conclusion rather than being surprised by them.

### 20. Operating System (RECOMMENDED)

**Values:**
- Linux
- Mac
- Operating System Independent

`Linux` and `Mac` are solidly evidenced. `pyproject.toml:37-39` declares the classifiers
`Operating System :: POSIX :: Linux`, `Operating System :: POSIX` and `Operating System :: MacOS`,
and the continuous-integration workflow at `.github/workflows/main.yml` actually builds and tests on
both: its matrix runs four Python versions on `ubuntu-latest`, and adds `macos-13` and
`macos-latest` jobs whose install steps reinstall a Homebrew GCC and point `CC` at
`/usr/local/bin/gcc-14` and `/opt/homebrew/bin/gcc-14` respectively — that is, both the Intel and
the Apple Silicon Mac paths are exercised.

**`Operating System Independent` is kept, and the CI workflow made that a real question.**

*The case for removing it.* No platform beyond Linux and macOS is demonstrated anywhere. The
package's classifiers name only POSIX, Linux and MacOS, and the build requires a working Fortran
compiler, which is the least portable part of the installation. Read strictly,
`Operating System Independent` asserts more than the evidence demonstrates, and narrowing the field
to `Linux` and `Mac` would be the tightest claim the evidence supports.

*Why it is kept anyway.* The workflow carries a complete set of Windows steps — a
`Install Windows-specific dependencies for non-pip install` step that installs ninja, mingw and
rtools and checks `gfortran --version`, an `Install on Windows` step that runs `meson setup build`,
`ninja` and `meson install`, and a separate Windows test step. Each is guarded by
`if: ${{ matrix.os == 'windows-latest' }}`. The maintainer clearly intends Windows to work and has
written the machinery for it, and nothing in the Python or Fortran source is platform-specific. The
value is also an already-stored one, and narrowing it would drop OMMBV out of any listing keyed on
platform independence on the strength of an argument from silence.

*The complication, which is why neither the value nor its removal is clean.* `windows-latest` never
appears in the workflow's `os` matrix or in its `include:` entries, so every one of those
Windows-guarded steps is unreachable. Windows is prepared for and never exercised. That asymmetry is
what settles the field's shape: `Windows` is **not** recorded, because it would assert a tested
platform that is not tested, while `Operating System Independent` is kept as the maintainer's evident
and implemented intent. A future refresh that finds `windows-latest` added to the `os` matrix has a
straightforward case for adding `Windows`; short of that, this field should be left as it stands, and
neither the removal nor the addition should be re-proposed on the evidence already weighed here.

### 21. CPU Architecture (RECOMMENDED)
- **Value:** CPU Independent

Nothing in the software targets an instruction set. The Python is portable, the Fortran is standard
fixed-form source compiled by whatever `gfortran` the platform provides, and no build file names an
architecture, an intrinsic or a vector extension.

Enumerating the architectures the CI happens to cover — `x86-64` for the Linux and `macos-13` jobs
and `Apple Silicon arm64` for the `macos-latest` job — was considered and rejected. Those values
describe where the project runs its tests, not what the software requires, and recording them would
misrepresent CI coverage as an architecture constraint. `CPU Independent` is the accurate claim and
is also the one that serves a reader correctly.

### 22. Related Phenomena (OPTIONAL)
- **Value:** Not found — evidenced empty

This field is correctly empty, and the reason is best given by listing what it could hold. The
vocabulary offers exactly seven phenomena: `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and `X-ray emission`. Six of the
seven are solar or heliospheric and nothing solar appears anywhere in this software. OMMBV computes
a vector basis, traces field lines through a geomagnetic field model, and scales drifts and electric
fields along those lines; it models no phenomenon on this list.

**The nearest miss, recorded so it is not mistaken for an oversight.** `Geomagnetic Storms` is the
only candidate worth a second look, because the paper that applies OMMBV (Field 27) studies what
its own title calls "a Minor Storm Period". That is a citing study's chosen interval, not a
capability of the software: OMMBV has no storm-time machinery, no geomagnetic indices, no event
detection and no disturbance-dependent behaviour of any kind. A reader searching for
geomagnetic-storm software would be misled by a hit here.

Phenomena this software does relate to but which the vocabulary lacks — equatorial electrodynamics,
ion-neutral coupling, the equatorial fountain — belong in Keywords, which is the open vocabulary,
and the `ionospheric electrodynamics` term recorded under Field 16 is where that is
handled.

### 23. Development Status (RECOMMENDED)
- **Status:** Active

The field held no value previously, so this was a decision about what to record rather than whether
to change something, and it came down to `Active` against `Inactive`.

**The decision must come from the vocabulary's own definitions, quoted here exactly as the catalogue
stores them.** Six of the eight are eliminated outright:

- `Abandoned` — "Initial development has started, but there has not yet been a stable, usable release; the project has been abandoned and the author(s) do not intend on continuing development."
- `Concept` — "Minimal or no implementation has been done yet, or the repository is only intended to be a limited example, demo, or proof-of-concept."
- `Suspended` — "Initial development has started, but there has not yet been a stable, usable release; work has been stopped for the time being but the author(s) intend on resuming work."
- `WIP` — "Initial development is in progress, but there has not yet been a stable, usable release suitable for the public."

All four require that there has *not yet been* a stable usable release, or that implementation is
minimal. Both conditions are falsified: the repository has 15 tagged releases, the newest published
2025-04-07, the package is on PyPI, and both `pyproject.toml` and `setup.cfg` declare the classifier
`Development Status :: 5 - Production/Stable`.

- `Unsupported` — "The project has reached a stable, usable state but the author(s) have ceased all work on it. A new maintainer may be desired."

Eliminated: nothing states or implies that work has ceased. The repository is not archived and not
disabled, and there is no maintainer-wanted notice.

- `Moved` — "The project has been moved to a new location, and the version at that location should be considered authoritative."

Eliminated, and worth recording because the rename history in the scope note is exactly the sort of
thing that could tempt a future agent here. The project was *renamed*, not moved: GitHub's redirect
resolves the former paths to this same repository, with the same creation timestamp and `fork:
false`. There is no other location, and this repository is the authoritative one.

That leaves two, and neither definition is cleanly satisfied:

- `Active` — "The project has reached a stable, usable state and is being actively developed."
- `Inactive` — "The project has reached a stable, usable state but is no longer being actively developed; support/maintenance will be provided as time allows."

Both first clauses are satisfied. The question is the second clause of each. The deciding facts:
the most recent commit and the repository's `pushed_at` are both `2025-04-07T21:14:52Z`, with no
commit since; there is one open issue; the repository is not archived, not disabled and not a fork.
(GitHub's `updated_at` for this repository is `2025-05-26T05:38:08Z` and is **not** commit activity
— it moves on metadata changes such as topics and settings. Do not use it as a development signal.)
Any staleness claim should be anchored to the date 2025-04-07 rather than to an elapsed span, which
goes wrong every time this file is re-read.

*The case for `Active`, which is the recorded value.* The second clause has to be read against a project's own
cadence rather than against days-since-last-commit. This is a small, mature, single-purpose library
with 15 releases, whose most recent release was not a maintenance tick but a substantial one —
migrating the build system from distutils to Meson and updating the vendored field model to IGRF-14.
It is also the current working implementation of a method published in 2025, which is when a
library's release rate would be expected to fall as the method stabilises. From the reader's side,
`Inactive` functions as a warning, and warning a user off the current, released, cited
implementation of a live method would be wrong.

*The case for `Inactive`.* Read strictly, "is being actively developed" is a present-tense claim,
and there is no commit after 2025-04-07 to support it.

*Why `Inactive` is nonetheless the weaker choice on the definitions.* Its definition does not stop
at the absence of development; it continues "support/maintenance will be provided as time allows",
which is an assertion about maintainer intent. No artifact in or around this project states that.
Choosing `Inactive` would mean recording an unevidenced clause as though it were established, which
is exactly the mistake of paraphrasing a conditional definition into a flat statement.

*Leaving the field empty* was considered and rejected: the field is recommended, the evidence
plainly supports one of two values, and an empty development status tells a reader nothing at all.

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://ommbv.readthedocs.io

Verified reachable, resolving to `https://ommbv.readthedocs.io/en/latest/`. It is the URL the
project itself advertises: `README.md:9` carries a documentation badge linking to
`https://ommbv.readthedocs.io/en/latest/?badge=latest`, the PyHC registry entry's `docs:` field is
this exact string, and `.readthedocs.yml` at the pin configures the build. The documentation source
lives in `docs/` (eight `.rst` files including an API page, an installation page, an overview and
the citation guidelines quoted under Field 2).

Two alternatives were considered. The versioned form `https://ommbv.readthedocs.io/en/latest/` is
where the recorded URL redirects, and the bare form is preferred because it is the stable entry
point rather than a redirect target. The repository's own `README.md` was considered as a
documentation link and rejected: Field 3 already records the repository, and a hosted documentation
site is the better answer where one exists. As noted in the scope note, there is no wiki, so no
wiki page competes for this field.

### 25. Funder (OPTIONAL)

- **Organization:** Cosmic Studio — no identifier
- **Organization:** National Aeronautics and Space Administration — https://ror.org/027ka1x80
- **Organization:** National Oceanic and Atmospheric Administration — https://ror.org/02z5nhe81
- **Organization:** United States Naval Research Laboratory — https://ror.org/04d23a975
- **Organization:** U.S. National Science Foundation — https://ror.org/021nxhr62

All five come from the project's own funding acknowledgement, `README.md:46-54`, quoted here in
full because Fields 25 and 26 both rest on it:

> The development of the multipole software has been supported, in part, by
> multiple agencies under the following grants:
> Cosmic Studio, Naval Research Laboratory N00173-19-1-G016,
> and NASA 80NSSC18K1203.

> Previous versions of this software that provided an 'average' basis were
> funded by: National Aeronautics and Space Agency (NASA NNG12FA45C),
> National Oceanic and Atmospheric Administration (NOAA NSF AGS-1033112),
> and the National Science Foundation (NSF 1651393).

Three points about the recorded names, each of which would otherwise invite a wrong "correction".

*The README's `National Aeronautics and Space Agency` is the README's own slip.* The agency is the
National Aeronautics and Space Administration, which is the recorded name and the name attached to
the ROR. Do not amend the recorded value to match the README.

*`Naval Research Laboratory` is recorded in its full institutional form,* `United States Naval
Research Laboratory`, matching its ROR record. Expanding and disambiguating institutional names is
the campaign convention and is why the recorded name is longer than the README's.

*The README conflates two agencies on one award.* `NOAA NSF AGS-1033112` names both NOAA and NSF for
a single grant number; the NSF award record for 1033112 gives the agency as NSF. Both organizations
are recorded as funders, which is the correct union of what the README credits — but see Field 26
for what this means about the award itself.

**Negative research on `Cosmic Studio`.** It is correctly identifier-less. A ROR search on
2026-09-08 for "Cosmic Studio" returned only fuzzy matches on the word "Studio", none of them this
company, against a control query that correctly returned nothing for a nonsense string. A small
private company is the case ROR generally does not cover, so this is unlikely to change. Do not
re-propose a ROR here. The same finding applies to `Stoneris` under Field 6.

**A note on where funder information may *not* come from.** Two published papers cite or use this
software (Fields 14 and 27). A citing paper's own funders are never the software's funders, and no
value in this field is drawn from either paper's acknowledgements.

### 26. Award Title (OPTIONAL)

**Values:**
- **Award Title:** PR 76-3033-19 PYSAT AND DINEOFS- A GENERALIZED SPACE WEATHER SYSTEM
  - **Award Identifier:** N00173191G016
- **Award Title:** NASA grant
  - **Award Identifier:** 80NSSC18K1203
- **Award Title:** Collaborative Research: CEDAR--Assimilative Analysis of Low- and Mid-latitude Ionospheric Electrodynamics
  - **Award Identifier:** AGS-1651393
- **Award Title:** The Continued Operation of COSMIC in Support of Operational and Research Applications for Years 2012-2015
  - **Award Identifier:** AGS-1033112

No awards were recorded for this software previously, while `README.md:46-54` (quoted under Field 25)
names five grant numbers. Each of the five was resolved individually, and the answers differ enough
that they are set out one at a time: four are recorded above, and the fifth is a documented
omission.

**A mechanism note that governs all five.** An award is recorded as a title plus an identifier, and
matching happens on the identifier first. Where an award record already exists under a given
identifier, attaching it creates nothing new and does not overwrite the title that record already
carries. Where none exists, recording the award creates a new record — which requires a title,
because an award with no title cannot be recorded at all. Award titles are capped at 128 characters.
And a durable limitation worth knowing before anyone plans a repair: an award's *funder* link cannot
be written through any submission or update path, so a newly created award record will have no
funder attached until someone makes a database-side correction.

**Three of the four attach existing award records, so nothing new is created for them.**

*1. `PR 76-3033-19 PYSAT AND DINEOFS- A GENERALIZED SPACE WEATHER SYSTEM` — identifier `N00173191G016`.*
This is the README's `N00173-19-1-G016`. An award record already exists for it, and its funder is
already one of this software's funders. **The identifier must be recorded in the hyphen-stripped form
`N00173191G016`, because that is the form the existing record carries; the README's hyphenated
`N00173-19-1-G016` would fail to match and would create a duplicate.**

**Previous title, and how it was corrected.** When this field was resolved, the shared award record
carried the placeholder title `U.S. Naval Research Laboratory award` — generic rather than
descriptive, and shared verbatim with a second Naval Research Laboratory award record
(`N0017322P0744`), so the identifier was the only thing that distinguished it. An award's title is a
property of the shared record rather than of this software's entry, and attaching by identifier
reuses that record without overwriting its title, so the title could not be corrected through this
field. It was corrected by a database-side change to the shared record on 2026-09-09, to the title
recorded above. That record is also attached to pysat, so pysat now displays the same corrected
title; the second Naval Research Laboratory record keeps its placeholder. A later refresh should
expect the corrected title already present and must not attempt to send a title for this award.

The corrected title is the federal spending record's description for this award,
`PR 76-3033-19 PYSAT AND DINEOFS- A GENERALIZED SPACE WEATHER SYSTEM`, 67 characters and so
comfortably inside the 128-character cap on award titles. The award went to the University of Texas
at Dallas from the Department of Defense and ran 2019-09-01 to 2022-08-31. It is worth noticing that
this description names **pysat** explicitly, which independently corroborates the pysat relation
argued under Fields 29 and 30: the grant that the README credits for the multipole work funded
pysat-family development at the same institution.

**A search trap that hid this, and that generalises.** Looking this award up under the README's
hyphenated spelling `N00173-19-1-G016` returns nothing from the federal spending data across every
award-type group — grants, contracts, indefinite-delivery vehicles, direct payments and loans — and
it would be easy to conclude from that the award is simply absent. It is not: the same query under
the hyphen-stripped `N00173191G016` returns the record above from the grants group. Both a positive
control (a known NSF award, which returned a result) and a negative control (a nonsense identifier,
which returned none) confirm the query itself was working in both cases. The same normalisation
issue governs the catalogue's own award records, where this award is likewise stored hyphen-stripped.
**The durable rule: an award identifier must be looked up with punctuation normalised away, in every
source. An absence established by one literal spelling is not an absence.**

*2. `NASA grant` — identifier `80NSSC18K1203`.*
An award record already exists for it and its funder is already one of this software's funders.
`NASA grant` is plainly a placeholder, and the same placeholder appears on at least one other NASA
award record, so it neither describes nor distinguishes this award. It cannot be improved by
recording: attaching by identifier reuses the record and leaves its existing title alone, and the
funder link is unwritable in any case. The federal spending record for this award confirms it went
to the University of Texas at Dallas from NASA, running 2018-06-07 to 2021-08-31, but supplies only
an all-capitals proposal abstract of 2,790 characters. It opens
`A THREE-YEAR RESEARCH PROGRAM IS PROPOSED TO STUDY THE ONSET AND EVOLUTION OF EQUATORIAL PLASMA BUBBLES THAT DEVELOP IN THE POST-MIDNIGHT EQUATORIAL IONOSPHERE.`
and goes on to name the CINDI instrument, C/NOFS and the SAMI3 model. A proposal abstract is not an
award title, and at 2,790 characters it could not fit the 128-character cap even if it were. So
unlike the Naval Research Laboratory award above, this one really does have no better title
obtainable from that route, and the placeholder stands until a database-side correction supplies
one. (This award was found under its literal identifier, but it was also re-checked with punctuation
normalised, per the rule stated above.)

*3. `Collaborative Research: CEDAR--Assimilative Analysis of Low- and Mid-latitude Ionospheric Electrodynamics` — identifier `AGS-1651393`.*
This is the README's `NSF 1651393`, and it is the best-substantiated grant on the list: the NSF
award record for 1651393 names **Russell Stoneback** as principal investigator at the University of
Texas at Dallas, running 2017-08-01 to 2020-07-31 under the AERONOMY program — that is, this
software's own lead author's award, on the subject the software addresses. An award record already
exists for it, with a real descriptive title, and its funder is already one of this software's
funders. **The identifier must be sent as `AGS-1651393`, the form the existing record carries;
sending the README's bare `1651393` would create a duplicate.**

One precision worth recording so it is not "fixed" later: the title above is the *existing record's*
title, not a quotation of NSF's. NSF's own title for award 1651393 has two spaces after
`Collaborative Research:` and runs to 106 characters, while the existing record has one space and
105. The existing record's form is what to send — and since attaching by identifier does not
overwrite a title anyway, the difference has no effect.

**Omitted (1), with the reason.**

*`NNG12FA45C`.* No award record exists for it, so recording it would require creating one, and no
title is obtainable. A normalised search over the award records — comparing identifiers with all
punctuation and case removed — found no match for it, and no record contains its distinctive
numeric core. The federal spending data has exactly one matching award: a contract to the Regents of
the University of California from NASA with a start date of 2012-01-11, whose description begins
`PHASE A THROUGH F - ICON.  THIS CONTRACT IS FOR THE UNIVERSITY OF CALIFORNIA (UCB) AT BERKELEY
SPACE SCIENCES LABORATORY`. That is the ICON mission prime contract, whose principal investigator is
Thomas Immel. A contract description is not an award title, and an untitled award cannot be
recorded. Substantively this is ICON mission funding that supported the earlier 'average'-basis
versions of the software, which is exactly how `README.md:51-52` frames it — so the omission loses
little, and the ICON relationship is captured under Field 32 instead.

**The fourth award, `AGS-1033112`: recorded, and recording it creates a new award record.**

This is the README's `NOAA NSF AGS-1033112`. No award record existed for it. Unlike `NNG12FA45C`,
**a real title is obtainable**: the NSF award record for 1033112 is
`The Continued Operation of COSMIC in Support of Operational and Research Applications for Years 2012-2015`
— 105 characters, comfortably inside the cap — with **William Schreiner** as principal investigator
at the University Corporation for Atmospheric Research, running 2012-08-15 to 2019-12-31 under the
Climate & Large-Scale Dynamics program. So recording it is possible in a way that `NNG12FA45C` is
not, which is why this was a judgement call rather than a forced omission.

*Why it is recorded.* `README.md:53` credits this grant explicitly, in the authors' own words, as
funding for previous versions of the software. Field 26's job is to record the awards the authors say
funded the work. Declining to record a credited award because we judge the awardee to be a mismatch
would be second-guessing the people who wrote the acknowledgement.

*The case against, which did not prevail but leaves a consequence worth carrying forward.* The
awardee is UCAR and the principal investigator is not an author of this software, and the award funds
COSMIC constellation operations rather than this package. More concretely, and this is the durable
part: an award's funder link cannot be written through any submission or update path, so the award
record created for `AGS-1033112` carried no funder at first. That gap was closed by a database-side
change on 2026-09-09, which attached the U.S. National Science Foundation record already used by this
software's other NSF award (`AGS-1651393`) as the funder. A later refresh should expect the funder
already present and must not attempt to send it.

The title, principal investigator, awardee and dates are set down above so that nobody has to
re-derive them for a later audit of why this award is here.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Values:**
- https://doi.org/10.1029/2020JA028539

The field held no value previously. Four candidate publications were found, and all four
are set out below with a verdict, because the point of this section is that a future agent should
not have to rediscover any of them — and because two of the four are rejections that are easy to
re-propose.

**The bar, stated before it is applied.** A publication belongs here if its text *engages with what
OMMBV does* — either it uses the software to produce a result, or it describes or positions the
software as such. A publication that names OMMBV in an inventory of packages does not clear the bar,
because such a mention carries no information about this software specifically. The bar is
deliberately **not** "any publication that cites the software's DOI", and the reason is decisive:
applying that bar to these four candidates would admit the two community-overview papers, which cite
an OMMBV Zenodo record formally, and exclude the one paper that actually applies the software, which
does not cite any OMMBV DOI at all. That inversion is why engagement rather than citation formality
is the right test. The bar is applied identically to every candidate below.

**How the candidates were found, so the search can be reproduced or extended.** Three routes, run
against ADS with working controls (a nonsense full-text token returned nothing; a known-good title
query returned a plausible count). First, a full-text search for `OMMBV` returns five records: two
of them are OMMBV's own Zenodo software records, and three are articles. Second, citation queries on
each of OMMBV's two indexed Zenodo software records return the papers that formally cite them.
Third — and this is the route that a name-based search cannot substitute for — a full-text search
for the **former** package name `pysatMagVect` returns a paper that never uses the word "OMMBV" at
all. A section-scoped check also established that no paper thanks OMMBV in its *acknowledgements*:
an acknowledgements-scoped search for `OMMBV` returns nothing, against a control confirming the
acknowledgements index works for each of the three articles.

**The one publication recorded, and why.**

- **https://doi.org/10.1029/2020JA028539** — Hsu, C.-T.; Matsuo, T.; Maute, A.; Stoneback, R.;
  Lien, C.-P., "Data Driven Ensemble Modeling of Equatorial Ionospheric Electrodynamics: A Case
  Study During a Minor Storm Period Under Solar Minimum Conditions", Journal of Geophysical Research
  (Space Physics), 2021 (ADS bibcode `2021JGRA..12628539H`).

  *Why it clears the bar.* It names OMMBV in its body text; Russell Stoneback, this software's lead
  author, is a co-author; and its subject is precisely what the software's basis is built to express
  — vertical E×B drift variability at the magnetic equator, with C/NOFS and FORMOSAT-3/COSMIC among
  its own keywords, both of which are platforms this software is recorded as supporting. This is a
  use of the software in service of a result, not an inventory entry.

  *What its methods section says, read from the article.* The paper is **Free Access** and renders
  in full. OMMBV is not named in passing in it — it is the mapping operator of the paper's central
  calculation, used twice. For the observed drifts:

  > "The Orthogonal Magnetic Multipole Basis Vector (OMMBV), which is part of PYSAT, is used here for
  > this mapping, and the mapping processing of the C/NOFS ion drift velocity can be written as
  > [displayed equation] where M represents the mapping operator provided by the OMMBV"

  The bracketed marker stands for a displayed equation that carries no words; the sentence reads as
  a broken clause without it, so any later quotation of this passage should keep the marker rather
  than close the gap.

  and for the model output:

  > "The modeled plasma velocity is interpolated and transformed from the TIE-GCM's geographic
  > coordinate system to the foot point in the geomagnetic coordinate using the OMMBV"

  So "uses OMMBV to produce a result" rests on the paper's own methods. The body-text match, the
  subject matter and the shared authorship recorded above still hold and are worth keeping as
  corroboration, but they are no longer what the claim stands on.

  *A search trap in this paper's own wording.* It expands the acronym as "Orthogonal Magnetic
  Multipole Basis Vector" — the middle two words in the opposite order from the software's own
  "Orthogonal Multipole Magnetic Basis Vectors", and singular rather than plural. A full-text search
  for the software's canonical expanded name therefore does not return this paper at all. That is
  also the reason the Field 14 observation that the 2025 method paper is the only ADS full-text hit
  for the canonical phrase holds: it holds by a coincidence of word order in this paper, not because
  no other paper engages substantively with OMMBV. Search the acronym, and both word orders of the
  expansion.

  *Two facts this text corroborates for other fields.* It calls OMMBV "part of PYSAT", which is
  independent literature support for the pysat relation argued under Fields 29 and 30 — a relation
  otherwise argued entirely from OMMBV's own code. And it states the mapping altitude outright:

  > "Assuming that the geomagnetic field lines are equipotential, the observed ion drift velocity can
  > be mapped along the geomagnetic field line to the foot point at 120 km."

  That sentence stands immediately before the OMMBV sentence quoted above, so the 120 km foot point
  is the altitude of this software's own mapping in a published application — corroborating the
  C/NOFS platform recorded under Field 32 and the 120 km altitude that carries `Earth Thermosphere`
  under Field 5. The paper's separate statement that "Overall C/NOFS CINDI IVM ion drift velocity
  error is considered near 8.5 m/s" supports the instrument, not the altitude; the two are easy to
  conflate and the altitude claim should be checked against the sentence quoted here.

  *One thing this paper does not do.* It cites no OMMBV Zenodo record — a check of its reference
  list for software entries returns none — so its OMMBV mention is a bare in-text reference. Under
  the bar adopted here that does not count against it; under a citation-formality bar it would be
  excluded, which is the inversion described above.

**Rejected, with reasons.**

- **Barnum, J.; Masson, A.; Friedel, R. H. W.; Roberts, A.; Thomas, B. A., "Python in Heliophysics
  Community (PyHC): Current status and future outlook", Advances in Space Research, 2023**
  (`https://doi.org/10.1016/j.asr.2022.10.006`, ADS bibcode `2023AdSpR..72.5636B`). It names OMMBV
  in its body and formally cites OMMBV's v1.0.0 Zenodo record — so it would be admitted by a
  citation-formality bar. Rejected on the engagement bar: it is a community-status paper about
  PyHC's organisation, information architecture and best practices, and OMMBV appears in it as one
  member of the package inventory. Nothing in it is about this software.

- **Burrell, A. G.; Halford, A.; Klenzing, J.; Stoneback, R. A. et al., "Snakes on a Spaceship—An
  Overview of Python in Heliophysics", Journal of Geophysical Research (Space Physics), 2018**
  (`https://doi.org/10.1029/2018JA025877`). Rejected for the same reason as the paper above: it is
  the community framework overview, and the software appears as an inventory entry within it.
  **It is recorded here anyway, and deliberately, for two reasons.** First, it is the strongest
  single piece of independent evidence for the rename described in the scope note: it names the
  software as `pysatMagVect` in its body text and formally cites the concept DOI that this record
  still carries as Field 2, which is why the concept DOI predates the OMMBV name. Second, and more
  practically, **a future agent searching the literature for "OMMBV" will never find this paper.**
  Finding it required searching for the former name. Recording it here means that search does not
  have to be rediscovered.

- **Stoneback, R. A.; Lien, C.-P.; Hsu, C.-T.; Matsuo, T., "Orthogonal Electrodynamics in Multipole
  Magnetic Fields", 2025** (`https://doi.org/10.1029/2025JA033911`). This paper clears the bar
  easily — it is the paper that derives the method the software implements. It is excluded from
  Field 27 not on relevance but on placement: it is recorded as the reference publication under
  Field 14, and listing the same work in both fields is the duplication the two-field split exists to
  prevent. The alternative of leaving Field 14 empty and carrying this paper here instead was weighed
  and rejected under Field 14. A future agent who notices this paper missing from Field 27 should
  read that as the deliberate consequence of the Field 14 value, not as an omission to repair — and
  should move it here only if Field 14 is ever emptied.

**One consequence to carry forward.** Neither citing paper contributes anything to Fields 25 or 26.
A citing paper's funders are its authors' funders, not the software's.

### 28. Related Datasets (OPTIONAL)
- **Value:** Not found

No dataset is associated with this software, and the reason is structural rather than a gap in the
search. OMMBV consumes no dataset — it takes coordinates and dates as numeric arrays (see Fields 17
to 19) — and it publishes none: the DataCite record for the concept DOI carries no dataset relation,
its only non-version relation being the `IsSupplementTo` pointer back into the source repository.
The validation table in `tests/test_vitmo.py` is a hard-coded fixture inside a test file, not a
published dataset, and the two uncertainty figures under `docs/images/` are illustrations rather
than data products. There is nothing here to record.

### 29. Related Software (OPTIONAL)
### 30. Interoperable Software (OPTIONAL)

**Value for both fields: https://github.com/pysat/pysat**

Both fields hold the same single value, and that is the right shape: pysat qualifies under both, for
different reasons. The two fields are argued together here because the relationship
is one relationship, and then the URL form is argued separately.

**Why pysat belongs in Field 30 (interoperable).** `OMMBV/satellite.py` is a documented public
module whose opening line is
`"""Provide support for adding OMMBV to NASA Ionospheric Connections Explorer."""` and whose four
public functions — `add_mag_drift_unit_vectors_ecef`, `add_mag_drift_unit_vectors`,
`add_mag_drifts` and `add_footpoint_and_equatorial_drifts` — each take a parameter documented as
`inst : pysat.Instrument`, read named columns out of it, and write results and their metadata back
into it (`OMMBV/satellite.py:46` is the comment `# Add data to pysat.Instrument` and `:59` is
`# Add metadata to pysat.Instrument`). That is a documented adapter across a shared data model,
which is exactly the demonstrated-exchange standard this field requires — not a dependency claim.
The module is published in the API documentation (`docs/api.rst` has a `Satellite` section for it),
so this is a user-facing capability rather than an internal detail.

**Why pysat belongs in Field 29 (related).** It is a domain-specific dependency and a companion
package rather than generic infrastructure: `requirements.txt` lists `pysat`, `setup.cfg`
`install_requires` pins `pysat>=3.0.0`, the CI workflow has a dedicated `Set up pysat` step that
creates a `pysatData` directory and initialises pysat's parameters before the tests run, and
`docs/images/poweredbypysat.png` is tracked in the repository. pysat is also itself a catalogue
entry, so the relation is one a reader can follow.

**Two corroborations from outside the code.** The relation above is argued entirely from OMMBV's own
repository, and two independent sources confirm it. The published application of this software
(Field 27) describes OMMBV in its methods as "part of PYSAT" — that is how a working user of the
software understands the coupling. And the federal description of the Naval Research Laboratory
award the README credits (Field 26) names pysat explicitly, so the grant behind the multipole work
funded pysat-family development at the same institution.

*One qualification worth recording, because it will look like a contradiction otherwise.* The
dependency declarations disagree with each other. `requirements.txt` and `setup.cfg` both require
pysat, but `pyproject.toml:21-24` — the file the current Meson build actually uses — declares only
`numpy` and `scipy`. So pysat is effectively optional in the modern build, needed only for the
`satellite` module. That weakens the *dependency* half of the Field 29 case but leaves the adapter
evidence for Field 30 untouched, since the adapter exists regardless of how it is installed.

**The URL form: the repository URL, replacing a version DOI.**

The value previously recorded in both fields was `https://doi.org/10.5281/zenodo.15059161`, and it is
superseded by `https://github.com/pysat/pysat`.

*Why the repository URL.* pysat's own catalogue entry records exactly this repository URL. The
convention when one entry names another is to point at that entry's recorded repository URL, and the
reason is presentational: a related-item entry is displayed to a reader as its raw URL, and this
relation's stored display name is a placeholder rather than "pysat". So a reader sees the URL itself,
and `https://github.com/pysat/pysat` reads as "pysat" at a glance while a DOI reads as an opaque
number. The field's own instructions also accept a repository link explicitly.

*Why the superseded value was wrong* — on the evidence, not by default. DataCite records
`10.5281/zenodo.15059161` with the title `pysat/pysat: v3.2.2`, version `v3.2.2`, issued 2025-03-20,
and the relation `IsVersionOf 10.5281/zenodo.1199703`. It is a **version** DOI: it names one 2025
release of pysat, not pysat. OMMBV's relationship is to the package — the adapter targets pysat's
Instrument data model, not one release of it — so the old value both overspecified the relation and
would have read as increasingly stale. Do not restore it.

*The one alternative that stays live, under a stated condition:* `https://doi.org/10.5281/zenodo.1199703`,
pysat's Zenodo **concept** DOI. It is strictly better than the superseded version DOI, and the field's
instructions do say a DOI is ideal; it lost only to the presentational argument above. **The
condition under which it becomes the better answer, recorded so a future agent can recognise it:** if
the catalogue ever resolves a related item and displays its *title* instead of its raw URL, that
presentational argument evaporates and the concept DOI wins on persistence, because a DOI survives a
repository being renamed or moved — which, as the scope note shows, is not a hypothetical risk in
this corner of the ecosystem.

*A practical caution for whoever applies or re-audits this change.* A related-item entry is shared
across catalogue entries, and others also point at that same pysat version DOI. Moving OMMBV's value
therefore means detaching one entry and attaching a different one. It must **not** be done by editing
the shared entry's URL in place, which would silently rewrite what those other entries display.

**Considered and rejected for both fields, with reasons. These are recorded so they are not
rediscovered as candidates.**

- **apexpy** (`https://github.com/aburrell/apexpy`, itself a catalogue entry). Rejected, and the
  reason is the project's own. At the pin, `apexpy` appears in exactly two files: `.travis.yml:48`,
  which reads `  - pip install apexpy`, and `CHANGELOG.md:73`, which reads
  `- Implemented new E and D scaling vectors similar to Richmond (apexpy)`. The history explains
  both. Two 2019 commits introduced an apexpy comparison — "ENH/TES: Added direct comparison with
  apexpy at magnetic equator." and "Added apexpy for comparison plots" — and a 2021 commit removed
  it, with the message
  "TST: Deleted `test_comparison` since the other system vectors aren't expected to be the same."
  `OMMBV/tests/test_comparison.py` is on the list of paths this repository explicitly deleted. So
  the project itself concluded that the two systems are not comparable, which is the strongest
  possible reason not to relate them. The surviving `.travis.yml` line is stale configuration: that
  file was last modified in 2020, while `.github/workflows/main.yml` was still being changed days
  before the pin, so the GitHub Actions workflow is the live CI.

  *One later commit mentions apexpy without reviving it, recorded so the history is not misread.* A
  January 2025 commit titled "BUG: Attempt apexpy like testing" sits in the pin's ancestry, after
  the 2021 deletion. Its entire diff is to `.github/workflows/main.yml`, and it changes how the test
  suite is invoked — adopting an apexpy-style pattern of running pytest from the parent directory
  under `coverage`. It reintroduces neither apexpy the dependency nor the deleted comparison test.
  (The apexpy rejection is also why `magnetic apex coordinates` is rejected as a keyword under
  Field 16.)
- **AACGMv2** and the other magnetic-coordinate packages in the catalogue. Rejected a fortiori: a
  case-insensitive search for `aacgm` across the whole tree except the tracked PNGs matches no
  lines at all. If apexpy is excluded on the strength of the project's own deletion of its
  comparison, a package the project never mentions cannot qualify.
- **TIEGCM** (a catalogue entry in its own right). `README.md:41-42` says OMMBV "is currently being
  incorporated / into analysis routines suitable for integrating physics-based models (TIEGCM)".
  Rejected: that is stated in-progress work inside a third party's analysis routines, not a
  demonstrated exchange in this software. Both fields exclude "being incorporated into" as an
  aspiration, and `tiegcm` matches exactly that one line in the entire tree. The literature does not
  rescue it: the method paper of Field 14 compares OMMBV results against TIEGCM, and the applying
  paper of Field 27 maps TIEGCM output with OMMBV, but a comparison or a use inside someone else's
  study is not an exchange this software implements, and neither paper shows OMMBV reading, writing
  or adapting to TIEGCM.
- **The IGRF packages in the catalogue.** Rejected, and worth recording because "OMMBV uses IGRF"
  invites exactly this mistake: the software vendors the IAGA synthesis routine directly as
  `ommbvfortran/igrf14.f` and depends on no IGRF package. There is no exchange with any of them.
- **numpy and scipy.** Excluded without argument as generic scientific-Python infrastructure. They
  are the only two runtime dependencies `pyproject.toml` declares, and "depends on numpy" is true
  of nearly every entry in the catalogue.
- **pandas.** Same exclusion as generic infrastructure, and test-only at that: it is imported by
  four of the test modules (`tests/test_apex.py`, `tests/test_core.py`, `tests/test_satellite.py`
  and `tests/test_vitmo.py`) and by no module in the installable package.
- **The packages named only in the abandoned Travis configuration.** `.travis.yml` — last modified
  in 2020 and superseded by `.github/workflows/main.yml` — installs a broad test environment that
  includes several genuine heliophysics packages, among them `pysatCDF` (line 43) and `madrigalWeb`
  (line 41), both of which are themselves catalogue entries, plus `PyForecastTools` (line 42). All
  are rejected on the same ground as apexpy above and with the same evidence shape: each of
  `pysatCDF`, `madrigalWeb` and `PyForecastTools` appears in `.travis.yml` and in no other file in
  the tree, so there is no exchange, no import and no documented relation — only a dead installer
  line. This is recorded because `pysatCDF` in particular is easy to rediscover as a candidate: it
  is a pysat-family package and a catalogue entry, and its presence here looks meaningful until the
  file it sits in is dated.
- **xarray.** A Tier B package that would need a specific documented exchange to qualify. It has
  none: it appears in `.travis.yml` and once in `CONTRIBUTING.md:157`, which reads
  ``  * `import xarray as xr` `` — an entry in that guide's list of standard import aliases, not a
  use. No module in the package or the test suite imports it. Recorded because "returns xarray objects" is the usual way
  a package earns this field, and OMMBV does not.
- **Cython.** Declared in `pyproject.toml`'s build requirements but unused — there is no `.pyx` file
  at the pin. Stale build configuration, and generic tooling in any case.

### 31. Related Instruments (OPTIONAL)

**Values:**
- **Instrument Name:** The Ion Velocity Meter
  - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ICON/IVM

No instrument was recorded for this software before this refresh. Both name and
identifier are copied from the catalogue's stored vocabulary row for that instrument, whose recorded name
is `The Ion Velocity Meter` and whose identifier is the URL above.

**The only instrument the pinned tree names is an IVM.** `IVM` occurs 52 times in
`OMMBV/satellite.py`, and nowhere else in the tree; every occurrence is the literal instrument
frame, inside the metadata that module attaches to a caller's data. Representative examples, quoted
from that file: `OMMBV/satellite.py:266` is
`    info = {'long_name': 'Zonal direction along IVM-x',`; `:275` reads
`                      'is expressed here in the IVM instrument frame.'`; and `:276` reads
`                      'The IVM-x direction points along the instrument '`. Every other
instrument-like name checked against the tree is absent: `MIGHTI`, `CINDI`, `VEFI` and `Langmuir`
each match no file.

**Which IVM.** Two Ion Velocity Meter rows exist in the vocabulary and they must be distinguished by
identifier, not by name: `https://spase-metadata.org/SMWG/Instrument/ICON/IVM`, whose recorded name
is `The Ion Velocity Meter`, and `https://spase-metadata.org/SMWG/Instrument/CNOFS/CINDI/IVM`, whose
recorded name is `Coupled Ion-Neutral Dynamics Investigation` — the same name its parent CINDI row
carries, so the name alone cannot tell them apart. The tree selects ICON's, and the selecting
artifact is concrete rather than inferred: the module that carries all 52 IVM references opens
`OMMBV/satellite.py:1` with `"""Provide support for adding OMMBV to NASA Ionospheric Connections Explorer."""`,
naming ICON and no other mission, and `README.md:36-38` says "OMMBV is used by the NASA Ionospheric
Connections (ICON) Explorer / Mission to understand how remote measurements of neutral motions at
120 km / impacts the motion of plasma measured in-situ (at the satellite location)". The string
`CINDI` appears nowhere in the tree.

**The reader's-side test, which is what this field turns on.** Someone who arrives at the ICON Ion
Velocity Meter's page and finds OMMBV finds a library that takes IVM in-situ ion-drift measurements,
expresses them in the geomagnetic zonal / field-aligned / meridional basis, maps them to the
magnetic equator or the magnetic footpoint, and ships metadata written in the IVM's own frame. They
would be glad, not puzzled. That is the "designed to support" relation this field asks for.

*The case against recording anything here, which was weighed and rejected.* The computation is
generic. `add_mag_drift_unit_vectors`
projects onto whatever spacecraft basis the caller supplies as `sc_xhat_*`, `sc_yhat_*` and
`sc_zhat_*` columns, and it would work for any platform; "IVM" survives only inside the metadata
strings. So the software is not *only* for the IVM, and a strict reading of
"instrument-agnostic tools support none specifically" would leave this field empty.

*Why it is recorded nonetheless.* The IVM references are not tutorial name-drops and not a
"configurable for" mention. They are shipped metadata in a public module
written for that instrument — the field's own criterion of implementing a convention specific to an
instrument as a means of supporting it. And the reader's-side test is unambiguous.

**Rejected: the C/NOFS CINDI Ion Velocity Meter**
(`https://spase-metadata.org/SMWG/Instrument/CNOFS/CINDI/IVM`). Nothing in the tree selects it.
The temptation is real — this software's lead author worked at the University of Texas at Dallas,
which built both IVMs, and C/NOFS is recorded under Field 32 — but inference from an author's
institutional history is precisely the plausible guess the resolution procedure forbids in favour of
a concrete artifact.

The one piece of external evidence bearing on it was weighed and does not change the outcome: the
published application under Field 27 maps C/NOFS CINDI IVM ion drift velocity with OMMBV, which
establishes that a citing study *used* the software with that instrument's data. This field asks
instead what the software is designed to support, and what the software ships is ICON IVM metadata
and no mention of CINDI at all; the C/NOFS relation that evidence does support is the platform-level
one recorded under Field 32. If a future refresh finds `CINDI` named in the tree, or finds the
C/NOFS analysis routines that `README.md:41-44` describes as in progress, this becomes a live
candidate; until then it is not one. Recorded so the question is not reopened without new
evidence.

### 32. Related Observatories (OPTIONAL)

**Values:**
- **Observatory Name:** Ionospheric Connection
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ICON
- **Observatory Name:** Communication/Navigation Outage Forecasting System
  - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/CNOFS

Both names are copied from the catalogue's stored vocabulary rows rather than re-derived, which is
why they read as the expanded mission names rather than as the acronyms the README uses.

**ICON.** The strongest of the mission relations. `README.md:36-38` (quoted under Field 31) states
in the present tense that the mission uses the software, and `OMMBV/satellite.py` exists to serve
it — the module is documented as ICON support and its metadata is written in the ICON IVM's frame.
This is designed-to-support in the plainest sense.

**C/NOFS.** Recorded on a footing weaker than ICON's but real, and worth stating precisely.
`README.md:41-44` says OMMBV "is currently being incorporated / into analysis routines suitable for
integrating physics-based models (TIEGCM) / and measurements from the Communications/Navigation
Outage Forecasting System / (C/NOFS) satellite." That is work in progress at the pin, and the same
"being incorporated into" phrasing is the reason TIEGCM is rejected from Fields 29 and 30. The
distinction that keeps C/NOFS in and TIEGCM out is not the phrasing but the object: what the
software is being pointed at here is *that mission's measurements*, which is the relation this field
names, whereas TIEGCM is a model and has no observatory row at all — a word-anchored search of the
vocabulary for TIEGCM matches no rows, because it is not an observatory. C/NOFS is also the platform
whose CINDI IVM measurements the software's basis was originally built to express, which is
consistent with the software's pre-rename history. The literature closes most of the gap the
README's in-progress phrasing leaves: the published application under Field 27 maps C/NOFS CINDI IVM
ion drift velocity with OMMBV, so the software demonstrably does process that mission's measurements,
whatever became of the analysis routines the README announced. The value therefore does not rest on
those routines having materialised, and it should not be revisited on the strength of the README's
phrasing alone.

**Negative research: COSMIC-2 is a genuine relation with no vocabulary row, and must be left
unrecorded rather than approximated.** `README.md:39-41` states, in the present tense, "This package
is also being used by the NOAA/NSPO COSMIC-2 / constellation to express plasma measurements made at
the satellite locations / in a more geophysically useful basis" — a stronger claim than the C/NOFS
one, and clearly designed-to-support. But the vocabulary has no COSMIC-2 row. A word-anchored search
across the vocabulary's names, abbreviations, identifiers and definitions for COSMIC-2, FORMOSAT and
NSPO returns exactly one row, and it is the **wrong mission**: it is
`The joint Taiwan - U.S. Constellation Observing System for Meteorology, Ionosphere, and Climate`,
abbreviation `COSMIC`, identifier
`https://spase-metadata.org/IUGONET/Observatory/RISH/COSMIC/COSMIC_FORMOSAT_3` — that is
COSMIC-1/FORMOSAT-3, a different constellation, and it matched only inside its definition text.
**That row must not be substituted for COSMIC-2**, because doing so would assert support for a
mission this software does not support. Recording a name with no identifier is not an option either:
there is no free-text path, and a name without an identifier would create a new identifier-less
vocabulary row. So the correct outcome is a documented omission, and the correct fix is upstream —
a vocabulary refresh that adds COSMIC-2/FORMOSAT-7. A future agent should re-check whether such a
row now exists before concluding anything else.

**Other candidates checked and excluded.** The vocabulary does contain rows for C/NOFS's other
instruments — an ephemeris record, a Planar Langmuir Probe and a Vector Electric Field Instrument —
and for ICON's MIGHTI, EUV and FUV. None of them is named anywhere in the tree, and expanding a
single named instrument into its mission's full instrument complement would assert support the
software does not claim. Note finally that raw name searches over this repository are badly
misleading and each match must be attributed individually: `ICON` matches several lines that are
`miniconda` in a CI file or Sphinx favicon boilerplate in `docs/conf.py`, and `COSMIC` matches many
lines that are the company name `Cosmic Studio`, the GitHub organisation `CosmicStudioSoftware`, or
the domain `cosmicstudio.io` — including `OMMBV/__init__.py:28`, which is
`print("OMMBV brought to you by Cosmic Studio.")`. Only one line in the tree names the ICON mission
in `README.md`, and only one names the COSMIC-2 mission.

### 33. Logo (OPTIONAL)
- **Logo URL:** https://raw.githubusercontent.com/CosmicStudioSoftware/OMMBV/e4b36778fd99ed01b9d68d2d565761937a9fa4a6/docs/images/logo_high_res.png

Verified rather than assumed. Fetching this URL on 2026-09-08 returned HTTP 200 with content type
`image/png` and 71,354 bytes; the PNG signature is valid and the image is 2255 × 2880, 8-bit RGB.
The fetched bytes are hash-identical to the repository's own blob at
`docs/images/logo_high_res.png` at the pinned revision, so the URL demonstrably serves the pinned
file and not a redirect or a placeholder. Viewed: a viridis-colormapped field plot above the word
OMMBV in large black type. It is a real logo rather than an example figure, and the project presents
it as one — `README.md:3` places this exact file in a centred header block with
`alt="OMMBV" title="OMMBV"`.

The URL is pinned to the 40-character commit SHA rather than to a branch, which is deliberate: a
branch URL would break silently the moment a maintainer renamed, moved or deleted the file, and the
catalogue has no way to detect that. The counter-argument — that a branch URL would always serve the
current logo, so pinning risks freezing a stale image — is rejected: that mutability *is* the
fragility being avoided, and a logo redesign is something a metadata refresh should notice and
record deliberately rather than inherit silently. The URL is 131 characters, comfortably inside the
200-character limit on this field. There is no `.gitattributes` in the tree, so the file is not
tracked by Git LFS and the raw URL serves real image bytes rather than a pointer.

**Two alternative sources were considered and rejected.** The PyHC registry entry's `logo:` field is
`https://github.com/CosmicStudioSoftware/OMMBV/blob/main/docs/images/logo_high_res.png` — wrong on
both counts available: it is a `blob/` page URL, which serves HTML rather than an image, and it is
branch-based rather than pinned. And of the four images tracked in `docs/images/`, only this one is
a logo: `dipole_uncertainty.png` and `igrf_uncertainty.png` are the two performance figures
`README.md:90-99` links to, and `poweredbypysat.png` is the pysat ecosystem badge.

---

## Registry and index cross-references

Recorded here rather than under a single field, because these sources bear on several fields at once
and a future agent will want to know exactly which list each entry lives in.

**PyHC.** OMMBV is in the PyHC **community** registry — `_data/projects.yml`, at the entry
`- name: "OMMBV"`. It is not in `_data/projects_core.yml` and not in
`_data/projects_unevaluated.yml`; all three lists were checked, and pinning the specific list
matters because entries move between them. The entry supplies the documentation URL (Field 24), the
repository URL (Field 3), a `contact:` of `Russell Stoneback`, a `logo:` that is rejected under
Field 33, and the facet tags tested under Field 5. Its `description:` is not used for Field 8: it is
shorter than the README's, and it misspells the expanded acronym. The entry also carries a set of
PyHC quality ratings; those describe PyHC's assessment of the project, not the project's own
metadata, and no field here is derived from them — in particular the development status under
Field 23 is argued from the vocabulary definitions and the repository, not from a maturity rating.

**PyPI.** Two distributions exist for this software's lineage, which is a direct consequence of the
rename in the scope note: `OMMBV`, whose newest version is 1.1.0 and whose `home_page` is the
current repository, and `pysatMagVect`, whose newest version is 0.4.0 and whose `home_page` is the
former `rstoneback/pysatMagVect` path. Anyone auditing this software's release history from PyPI
alone will see it split across those two names. A third spelling, `pysat-magvect`, does not exist on
PyPI — the JSON API returns 404 for it, which is the authoritative check; note that PyPI's HTML
project pages can return a bot-challenge page with a success status even for names that do not
exist, so the HTML page is not a valid existence test.
