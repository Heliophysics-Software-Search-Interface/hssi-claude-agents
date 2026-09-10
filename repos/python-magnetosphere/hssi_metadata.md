# HSSI Metadata Extraction Results

**HSSI Software ID:** 20aeb28e-66c8-4695-a722-89a7f807c795
**Repository:** https://github.com/dpq/python-magnetosphere
**Source Revision:** 806be11d550eecdd372a9d5eb763bae1990aa4b2
**Extraction Date:** 2026-09-08
**Validation Date:** 2026-09-09
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

Three facts about this project change how every piece of evidence below should be read.

**1. The GitHub repository is a machine-made export, not the project's development home.** Its GitHub
description is `Automatically exported from code.google.com/p/python-magnetosphere`, and it was created
on 2015-03-13 by Google's Code-to-GitHub migration, four years after the last commit. Several
GitHub-derived signals are therefore meaningless here: `created_at` (2015-03-13T05:03:58Z) is the
export date, not the project's start; `updated_at` (2025-02-24T20:15:06Z) reflects repository-record
touches rather than commit activity; and all five issues were opened on 2015-03-13 by the
`GoogleCodeExporter` bot as carried-over Google Code tickets. The real development history is the eight
commits dated 2009-12-29 through 2011-02-08.

**2. Most of the repository is vendored third-party code, and its documentation travelled with it.**
Of the twelve files tracked at the pinned revision, `cxform-auto.c`, `cxform-manual.c` and `cxform.h`
are Ed Santiago's CXFORM package, `igrf_sub.c` is the IAGA/NSSDC IGRF-11 Fortran run through `f2c`,
and `rigidity.c` is a separate Fortran cutoff-rigidity program run through `f2c`. Crucially, the file
named `README` is a *concatenation*: roughly the first sixty lines are David Parunakian's own text
about this Python package, and everything from the line `CXFORM:  An IDL/C library to convert between
spacecraft coordinate systems` onward is CXFORM's own README followed by the IGRF-11 model release
notes. **A sentence quoted from the README is therefore not automatically a statement about this
package**, and at least one stored HSSI value appears to have come from misreading that boundary (see
Field 20). Every quote below names which part of the README it comes from.

**3. Two of this entry's oddities have one cause and should not be adjudicated separately.** The pin
commit (`806be11d`, 2011-02-08, "Moved to a newer version of IGRF-11") both deleted all twenty-five
`dat/*.dat` coefficient files and stripped the `data_files` block out of `setup.py`, while leaving the
code path that reads those files untouched. That single act is why Field 17 has no data source, why
the README's installation sentence no longer describes what `setup.py` does, and why Fields 18/19 are
empty. The evidence is recorded once under Field 17 and cross-referenced from the others.

**Where the wiki quotations come from.** This project's Google Code wiki was migrated into the same
repository as a separate branch, `refs/heads/wiki`, whose single commit
`2d2da0d85027a8f73bca2acefa742e1308a22b08` (2015-03-13, "Migrating wiki contents from Google Code")
contains one file, `ProjectHome.md`. Every wiki quotation below is from that revision of that file.
The branch is invisible from the code pin, and GitHub reports `has_wiki: false` for this repository,
so there is no separate `.wiki.git` to look in — an agent that checks only the pinned tree will
conclude, wrongly, that this project left no prose about itself beyond the README. Note also that the
wiki text predates the 2010 change described in point 3, so it documents behaviour the software no
longer has (Field 17).

A fourth framing point, because it bears on Fields 12 and 23: the project published release artifacts
through its Google Code home, so the absence of a GitHub release proves nothing on its own. The Google
Code archive preserves that record and is cited where it matters.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The submitter identifies the person lodging the metadata, not an author of the software. It is
supplied at submission time and is not a property of the software.

### 2. Persistent Identifier (RECOMMENDED)

**Not found.**

No DOI exists for this software. This is a researched negative, not an unchecked field:

- The pinned tree contains no `CITATION.cff`, no `codemeta.json`, no `.zenodo.json` and no DOI badge —
  the `README` carries no badges of any kind.
- DataCite returns no records for the query `"python-magnetosphere"`. The negative is falsifiable: the
  same query shape returns 131 records for `"pysat"` and 0 for a nonsense string, so the route both
  answers and discriminates.
- Searching DataCite by creator rather than by package name — the correct technique for a manually
  deposited record, which need not contain the repository's name anywhere — returns nine records for
  `creators.name:"Parunakian"`. Four belong to Emanuil Parunakian (ophthalmology; a different person).
  The five belonging to David Parunakian are `10.13140/rg.2.2.14450.96962` (2018, radiation-monitoring
  telescope simulation), the paired `10.5281/zenodo.5749351` and `10.5281/zenodo.5749352` (VESPA
  mercury_mag_boundaries sample) and the paired `10.5281/zenodo.5733417` and `10.5281/zenodo.5733418`
  (MESSENGER magnetometer dataset). None of them is this software.

The project predates the GitHub–Zenodo integration era and its home was Google Code, which never
minted DOIs. A future refresh should not expect this field to fill unless someone deposits the code
anew.

### 3. Code Repository (MANDATORY)

`https://github.com/dpq/python-magnetosphere`

This is the only live source repository. The project's original home, declared in `setup.py` at the
pinned revision as `url='http://python-magnetosphere.googlecode.com'`, is gone: Google Code was shut
down and that host does not resolve to a project page (checked 2026-09-08).

Two alternatives were considered and rejected:

- **The Google Code archive landing page** `https://code.google.com/archive/p/python-magnetosphere/`
  answered HTTP 200 on 2026-09-08 and preserves the project's pre-GitHub record — downloads, labels,
  licence, logo name. It is a read-only historical archive, not a code repository, and it is cited
  below only as evidence. Field 3 wants the repository where the human-readable code lives.
- **Forks.** Several user forks of the export exist on GitHub. `dpq` is the author's own GitHub
  account — it matches the `dp@xientific.info` / `rumith` identity chain in Field 6 — so the `dpq`
  export is the authoritative one. **Do not re-derive this from the GitHub profile.** That profile
  displays the name `David Perry` and the location `Tel Aviv`, and on its face reads as a different
  person; a check that stops there reaches the opposite, wrong conclusion. The account resolves by
  commit authorship instead: `dpq/spacetrack` is an original repository rather than a fork, and its
  commits are authored by `David Parunakian <jaffar.rumith@gmail.com>` — the same identity Field 6
  establishes for this project.

### 4. Software Functionality (RECOMMENDED)

- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing

Every value is written fully qualified as `Parent: Child` because this vocabulary contains duplicate
child names under different parents — `Analysis` and `Field-line Tracing` each occur twice — so an
unqualified child name does not identify a row. HSSI held only the three bare parent categories
(`Coordinate Transforms`, `Models and Simulations`, `Data Processing and Analysis`) before this
refresh, with no subcategory; the five children are the enrichment.

The classification is derived from the exported API, which is small enough to enumerate completely.
`setup.py` builds exactly three extension modules — `magnetosphere.cxform`, `magnetosphere.igrf` and
`magnetosphere.rigidity` — and their method tables define the whole user-facing surface:

| Module | Exported function | What it computes |
|---|---|---|
| `cxform` | `transform(from, to, x, y, z, year, month, day, hour, minute, second)` | Cartesian vector between two named coordinate frames |
| `igrf` | `dimo(year)` | Geomagnetic dipole moment from the IGRF model |
| `igrf` | `lb(lat, lon, alt, year)` | L-shell and geomagnetic field intensity |
| `igrf` | `b(lat, lon, alt, year)` | B north/east/down/absolute from the spherical-harmonic model |
| `igrf` | `b0(lat, lon, alt, year, stps)` | Minimum field strength along a traced field line |
| `rigidity` | `cutoff450(lat, lon)` | Cosmic-ray cutoff rigidity at 450 km |
| `rigidity` | `cutoff(lat, lon, alt)` | Cutoff rigidity extrapolated to an altitude |
| `rigidity` | `correctedcutoff(rig, kp, lt)` | Cutoff rigidity corrected for Kp index and local time |

**Coordinate Transforms**, with **Magnetospheric** and **Heliospheric**, is the `cxform` module.
`transform()` is the only reason that module exists, and the README's "COORDINATE SYSTEMS IMPLEMENTED"
table lists GEI, J2000, GEO, MAG, GSE, GSM and SM (geocentric and magnetospheric) alongside RTN, GSEQ,
HEE, HAE and HEEQ (heliospheric). Both children are therefore evidenced by name. **Solar**,
**Ionospheric**, **Planetary** and **Mission-Specific** were each considered and rejected: HEEQ and
HAE are heliocentric frames, not the solar-disk frames (Carrington, Stonyhurst, helioprojective) that
`Coordinate Transforms: Solar` denotes; there is no AACGM, apex or magnetic-local-time transform
anywhere in the tree; no non-Earth body appears; and no spacecraft-attitude or instrument-pointing
frame is implemented.

**Models and Simulations: Empirical** is the IGRF and the cutoff-rigidity model. IGRF is the textbook
case for this subcategory — a spherical-harmonic expansion whose coefficients are fitted to
observations — and `rigidity.c` is a tabulated cutoff model with a Kp and local-time correction, which
is empirical in the same sense. **Physics-Based** was considered and rejected: the spherical-harmonic
potential expansion is the model's *representation*, while its scientific content is entirely the
fitted coefficient sets, so `Empirical` is the precise value and `Physics-Based` would blur it.
**Forecasting** was considered and rejected even though `extrashc_` extrapolates coefficients past the
last definitive epoch — that is secular-variation extrapolation internal to the geomagnetic model, not
space-weather prediction, and a searcher filtering for forecasting tools would not want this back.
**First Principles**, **MHD**, **Theory**, **Data Guided** and **Forward-Fitting** have no
corresponding code.

**Models and Simulations: Field-line Tracing**, and specifically *not* the identically named child of
Data Processing and Analysis, is `igrf.b0`. The distinction between the two rows is real and was
decided from the code: the Data Processing row means tracing field lines *through data*, the Models
row means tracing them *in model fields*. Here the traced field is generated entirely by IGRF —
`findb0_` and `shellg_` step along the line by repeatedly calling `stoer_`, which evaluates the model
field — and no observational input exists anywhere in the call path. Parunakian's own section of the
README describes the function as "Find the smallest magnetic field strength on a field line. Stps is
step size for field line tracing". A prior working proposal for this entry listed `Data Processing and
Analysis: Field-line Tracing`; that value is **wrong for this software** and should not be
reintroduced.

**Data Processing and Analysis**, with **Analysis**, is the weakest of the retained values, so the
reasoning is recorded to stop a later refresh flipping it casually. The argument against is real: the
package reads no scientific data, and every exported function takes scalars rather than a dataset. The
argument for, which prevails, is twofold. First, `Analysis` denotes general scientific analysis
producing derived physical quantities, and L-shell, dipole moment and cutoff rigidity are exactly
that. Second, the way these functions are actually used is on measured spacecraft positions and times
— `cxform.transform()` converts a real position vector between frames, `igrf.lb()` assigns an L-shell
to a real location — so a user doing data analysis reaches for this package in that role. The parent
category was already stored and is retained; `Analysis` is the child that makes it meaningful rather
than bare.

Whole top-level categories rejected: **Data Visualization** (nothing in the tree produces a figure,
image or plot; there is no plotting dependency and no drawing code), **Mission-related** (the package
is not part of any ground system, pipeline or mission operations) and **Servers and Environments** (no
server, container, deployment or parallel-computing code).

### 5. Related Region (RECOMMENDED)

- Earth Atmosphere
- Earth Inner Magnetosphere
- Earth Magnetosphere
- Interplanetary Space

The Region vocabulary is **flat** — every row is top-level and no row implies any other. `Earth
Magnetosphere` therefore does not stand in for `Earth Inner Magnetosphere`, and listing both is not
redundancy.

The first, third and fourth values were already held by HSSI and are retained on their own evidence.
`Earth Magnetosphere` is carried by the GSE/GSM/SM/MAG transforms and by L-shell computation. `Earth
Atmosphere` is carried by the IGRF interface taking altitude in kilometres above sea level, so field
values are computed within the atmosphere as a matter of course; the README states "Altitude should be
specified in kilometers above sea level." `Interplanetary Space` is carried by the heliospheric frames
HEE, HAE, HEEQ, GSEQ and RTN, which are the frames in which interplanetary positions are expressed.

**`Earth Inner Magnetosphere` is added.** `igrf.lb` returns McIlwain L and `igrf.b0` returns the
minimum field strength on the traced line; (L, B) is the standard coordinate pair of
inner-magnetosphere and radiation-belt work. `rigidity.cutoff450` computes cutoff rigidity at 450 km,
a trapped-particle and cosmic-ray-access quantity for low Earth orbit. A user filtering HSSI for
inner-magnetosphere tooling would want this package returned.

Considered and rejected, with reasons, so they are not re-proposed:

- **Earth Ionosphere** and **Earth Thermosphere** — 450 km lies in that altitude range, but the package
  contains no ionospheric or thermospheric physics whatsoever; it computes a geomagnetic quantity that
  happens to be evaluated there. Selecting these would mislead a searcher looking for ionospheric tools.
- **Earth Magnetotail**, **Earth Magnetosheath**, **Earth Outer Magnetosphere** — GSM and GSE are used
  throughout these regions, but that is true of any coordinate-transform library. Nothing in the code
  targets a specific outer region, so `Earth Magnetosphere` is the honest granularity.
- **Solar Wind** — a genuine near-miss, since RTN and HEE are solar-wind analysis frames. Rejected
  because the package offers no solar-wind-specific capability beyond providing those frames, and
  `Interplanetary Space` already carries the frame evidence.
- **Earth Auroral Subregion**, and every solar and planetary region (**Corona**, **Photosphere**,
  **Chromosphere**, **Solar Environment**, **Solar Interior**, **Heliosheath**, and the per-planet
  magnetospheres) — no corresponding capability. HEEQ and HAE are Sun-centred frames, but the package
  models nothing solar.

### 6. Authors (MANDATORY)

**David Parunakian**
- Identifier: `https://orcid.org/0000-0002-5468-4060` — **the correct target state, but not a value a
  routine metadata update can apply; see the durable limitation below.**
- Affiliation: Skobeltsyn Institute of Nuclear Physics of the Moscow State University
- Affiliation identifier: none (researched; see below)

**The single-author finding is evidenced, not assumed.** All eight commits in the repository carry one
git identity, `jaffar.rumith@gmail.com <jaffar.rumith@gmail.com@4e150a12-f27b-11de-82c3-25da7dca7fdf>`.
The `@<uuid>` suffix is a git-svn import artefact rather than part of an address, corroborated
independently by the Google Code archive recording this project's `repoType` as `svn`. `setup.py` at
the pin declares `author='David Parunakian'` and `author_email='dp@xientific.info'`, and Parunakian's
own section of the README states "The wrapper has been written by David Parunakian, Skobeltsyn
Institute of Nuclear Physics of the Moscow State University." with contact addresses
`rumith@srd.sinp.msu.ru` and `dp@xientific.info` — the local part `rumith` ties the README contact to
the committer's `jaffar.rumith@gmail.com`. The PyHC community registry independently lists the
project's `contact` as `"David Parunakian"`.

**Ed Santiago and Ryan Boller are deliberately *not* listed as authors, and that omission should
stay.** The README credits them — "Originally written by Ed Santiago (LANL), esm@pobox.com" and
"Modified & maintained by Ryan Boller (NASA/GSFC), Ryan.A.Boller@nasa.gov" — but those lines sit inside
the vendored CXFORM README and are credits for CXFORM, a separate package this one bundles. Their
contribution is recorded where it belongs: in the description (Field 8), which names both, and in
Field 29, which points at CXFORM's own repository. Making them authors of `python-magnetosphere` would
misattribute another work's authorship. The same reasoning excludes the IGRF-11 model authors, whose
credit belongs to the model (Fields 27 and 28).

**ORCID — identification, and why it cannot simply be patched.** A fielded ORCID search on
`given-names:David AND family-name:Parunakian` returns exactly one record, `0000-0002-5468-4060`. The
search is controlled: `given-names:Michael AND family-name:Hirsch` returns 7 and a nonsense
given/family pair returns 0, so the route both finds and discriminates. Bare-name ORCID queries are
unreliable in both directions, which is why the fielded form was used.

That record declares no employments, so it does not itself assert the SINP affiliation. The
identification rests instead on its 50 works groups spanning 2008 to 2024, which match this software's
domain, institution and era closely: MESSENGER magnetopause and bow-shock detection, Jovian magnetodisc
modelling from Juno and Galileo data, "Low-Latitude Variations in the Geomagnetic Field Caused by Solar
Wind Disturbances" (2014), an empirical model of the high-latitude boundary of Earth's outer radiation
belt (2018), work on the paraboloid magnetospheric model, and several Russian-language titles; the
record's other-names are `David Parunakyan`, `Д.А. Парунакян` and `Davit Parunakyan`. Its MESSENGER
magnetometer works correspond to the DataCite deposits found under Field 2, which carry a Lomonosov
Moscow State University affiliation — and SINP is an institute *of* Moscow State University. Name
coincidence alone would not be enough; the agreement of domain, institution and date range is.

**Durable limitation — this is a database-side correction, not a metadata patch.** HSSI holds this
author with an empty identifier. Sending an ORCID for an already-stored identifier-less author does not
fill in the existing entry: it resolves to a *new* person record and leaves the original orphaned while
still attached elsewhere. The ORCID above must therefore be applied to the existing record directly,
and a later refresh must not "fix" the gap by pushing it through the ordinary metadata path. This is a
known follow-up, not an oversight.

**Affiliation identifier — a researched absence.** A ROR search for `Skobeltsyn` returns zero results
on both the v1 and v2 endpoints, while a control search for Lomonosov Moscow State University returns
results including `https://ror.org/010pmpe69`. So the route works and the institute genuinely has no
ROR record. Recording the parent university's ROR against the institute's name was considered and
rejected: it would attach one organisation's identifier to a differently named organisation, which is
a misidentification rather than an enrichment. The affiliation is therefore recorded by name only, and
written out in full rather than as `SINP MSU`, per the expand-acronyms rule.

### 7. Software Name (MANDATORY)

`python-magnetosphere`

This is the repository name, the name HSSI already held, and the name under which the PyHC community
registry lists the project (`- name: "python-magnetosphere"`).

The alternative `Magnetosphere` was considered and rejected. It has real backing — `setup.py` at the
pin declares `setup(name='Magnetosphere',` and the released 0.1 distribution's generated `PKG-INFO`
carries `Name: Magnetosphere` — but it is the *distutils distribution* name, the string that names the
tarball, not the name the project is known by. The importable package is `magnetosphere` in lowercase,
the project's home and repository are both `python-magnetosphere`, and a bare "Magnetosphere" would be
uninformative as a catalogue title. Using the distribution name here would also make Field 12's version
history harder to read, since the tarball labels use it.

### 8. Description (MANDATORY)

> The magnetosphere package is a collection of useful libraries for Earth and Space scientists,
> providing three main modules. The igrf module offers methods based on the International Geomagnetic
> Reference Field (IGRF) version 11, including functions to calculate the geomagnetic dipole moment,
> L-shell and geomagnetic field intensity, Earth's magnetic field vector components, and the smallest
> magnetic field strength on a field line through field-line tracing. The cxform module provides
> coordinate transformation capabilities, allowing users to transform Cartesian coordinates between
> various coordinate systems commonly used in space physics, including geocentric (GEI, J2000, GEO,
> MAG), magnetospheric (GSE, GSM, SM), and heliospheric (HEE, HAE, HEEQ, GSEQ, RTN) coordinate
> systems. The rigidity module calculates cosmic ray cutoff rigidity at various altitudes, determining
> the minimum particle momentum required for cosmic rays to penetrate Earth's magnetosphere at a given
> location. The IGRF wrapper and rigidity module were developed by David Parunakian at the Skobeltsyn
> Institute of Nuclear Physics, while the coordinate transformation functionality is based on CXFORM,
> an IDL/C library originally written by Ed Santiago at LANL and maintained by Ryan Boller at
> NASA/GSFC.

Carried over from the existing HSSI record unchanged. It was checked function by function against the
pinned tree and is accurate throughout, including the credit split between Parunakian's own work and
the vendored CXFORM.

One point is worth recording because it looks like an error and is not. The description says "three
main modules", while the README's opening line says "The magnetosphere package currently contains two
modules: igrf and cxform." **The description is right and the README is stale.** The `rigidity` module
was added at commit `874845f` on 2011-02-08 and `setup.py` at the pin builds all three extensions, but
the README was never updated to mention it. A future refresh should not "correct" the description down
to two modules on the strength of that README sentence.

The description's wording is otherwise the original submitter's or curator's editorial choice and was
not rewritten for style.

### 9. Concise Description (OPTIONAL)

> Python package providing IGRF magnetic field calculations, cosmic ray cutoff rigidity analysis, and
> coordinate transformations for space physics applications.

Carried over from the existing HSSI record unchanged. It names all three modules, fits the field's
150–200 character guidance, and reads as a preview rather than a truncation. No reason to disturb it.

### 10. Publication Date (RECOMMENDED)

`2009-12-29`

**Retained, with the reasoning recorded in full because there is a genuine two-day discrepancy that a
later refresh will otherwise rediscover and "fix" arbitrarily.**

The stored date equals the earliest commit in the repository, `21c9787` (2009-12-29, "Moved project
files to trunk for SVN compatibility."). But the project's Google Code download manifest records
`python-magnetosphere_0.1.zip` uploaded on **2009-12-27** — two days earlier. So something was publicly
downloadable before the first commit that survives in this repository.

Both dates answer a real question, and the field's definition — "Date of first broadcast/publication…
Used for the initial version of the software" — favours the earlier one on a literal reading. The
stored 2009-12-29 is retained anyway, for three reasons:

1. **The 2009-12-27 artifact is not this software.** Its five files are `install.sh`, `LICENSE`,
   `pygrfmodule.c`, `README` and `setup.py`; its module is `pygrf`; its own `setup.py` declares
   `name = 'pygrf'` and `version = '1.0'`; and its README's About section opens "This program is a
   Python module which provides several useful methods based on IGRF v.10." It is an IGRF-10
   predecessor under a different package name, not the first publication of `python-magnetosphere`.
   Dating this entry from it would date the entry from a different package.
2. The first artifact recognisably *of this distribution* is `Magnetosphere-0.1.tar.gz`, uploaded
   2010-07-16 — later than the stored date, not earlier. So the earlier upload cannot pull the date
   back without also accepting the `pygrf` identification.
3. 2009-12-29 is defensible on its own terms as the date this project's own source history begins.

The value therefore stands and the two-day gap is explained rather than left as a trap. If a future
curator decides Field 10 should mean "first public availability of any ancestor of this code", the
supported value would be 2009-12-27 — but that is a change in what the field means, not a correction of
a wrong value.

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** `https://github.com`

Carried over from the existing HSSI record. The field's instruction is that where no DOI has been
obtained, the repository host is the correct entry; there is no DOI (Field 2) and the repository host
is GitHub.

Google Code was considered and rejected as the publisher. It was genuinely the original publisher — it
hosted the code, the wiki and the release downloads — but it no longer exists as a publishing entity,
has no stable identifier, and naming a defunct service would give a catalogue user nothing to act on.
Its role is recorded in the prose instead, under Fields 3, 10, 12 and 33.

### 12. Version (RECOMMENDED)

- **Version Number:** `v0.11`
- **Version Date:** none — see below
- **Version Description:** Adds the `rigidity` module for cosmic-ray cutoff rigidity
  calculations and moves the `igrf` module to a newer IGRF-11 revision. Declared in `setup.py` on
  2011-02-08; never published as a release artifact.
- **Version PID:** none — no DOI exists for this software (Field 2)

**The version number is retained.** `setup.py` at the pin declares `version='0.11',`, and
`git log -S "version='0.11'"` shows that string entering `setup.py` at commit `874845f` on 2011-02-08 —
the same day as the pin commit, and the last day the project was touched. So `0.11` is the version the
code has carried since it stopped moving.

**The `0.1` versus `0.11` trap — read this before dating this version.** The two strings differ by one
character and the archive record is easy to misread. The project's Google Code downloads page records
exactly three artifacts, and **every one of them is 0.1; none is 0.11**:

| Artifact | Uploaded | What it actually is |
|---|---|---|
| `python-magnetosphere_0.1.zip` | 2009-12-27 | the `pygrf` IGRF-10 predecessor (see Field 10) |
| `Magnetosphere-0.1.tar.gz` | 2010-07-16 | source release of `Magnetosphere` 0.1 |
| `Magnetosphere-0.1.linux-x86_64.tar.gz` | 2010-07-16 | Linux AMD64 binary build of the same |

A later agent reading "Magnetosphere-0.1.tar.gz, 2010-07-16" could easily record 2010-07-16 as the
release date of v0.11. **That would be wrong by one version and about seven months.** The version date
is left empty deliberately: v0.11 was never released in any channel — no Google Code download, no git
tag (the repository has none), no GitHub release (it has none), and no PyPI record under
`magnetosphere`, `python-magnetosphere`, `python_magnetosphere` or `Magnetosphere`.

**Why "never released" is evidenced here rather than an argument from silence.** This project *did*
publish releases, with generated distribution metadata to prove it. `Magnetosphere-0.1/PKG-INFO` inside
the 2010-07-16 tarball (a sha1-verified artifact, `0c9faf7e79dc7e424c55be45a587919d1b60f825`) reads:

```
Metadata-Version: 1.0
Name: Magnetosphere
Version: 0.1
Summary: A collection of useful libraries for Earth & Space scientists
Home-page: http://python-magnetosphere.googlecode.com
Author: David Parunakian
Author-email: dp@xientific.info
License: UNKNOWN
Description: UNKNOWN
Platform: UNKNOWN
```

That is distutils output for the same distribution name, so the project's release practice is
documented. `0.11` was bumped in-tree seven months later and no corresponding artifact was ever
produced. The contrast is with the project's own demonstrated behaviour, not with an absence of
searching.

**Companion warning for any future version work on this entry:** this project's version strings have
disagreed with their own labels since 2009. The download labelled `python-magnetosphere_0.1.zip`
contains a `setup.py` declaring `version = '1.0'`. An in-tree version string here is not evidence of a
release, and a download label is not evidence of an internal version.

The Version Description is derived from the only two commits between the 0.1 release and the
pin — `874845f` ("Added cutoff rigidity calculations for the Earth's magnetosphere", 2011-02-08) and
`806be11d` ("Moved to a newer version of IGRF-11", 2011-02-08). HSSI held no version description
before this refresh.

### 13. Programming Language (RECOMMENDED)

- C
- **Python 2.x**

**HSSI held `C` and `Python 3.x` before this refresh. `Python 3.x` is factually wrong** — not merely
imprecise — and the correction to `Python 2.x` is the substantive change in this field.

**The criterion, settled once and applied to every language.** Field 13 asks for "the computer
programming languages most important for the software", explicitly "not meant to be an exhaustive
list", and it describes the software *as it now stands* at the pinned revision. Two candidate readings
were considered:

- **(A) the languages the package is written in and built from**, and
- **(B) every language present in the tracked tree.**

**Both readings give the same answer here — `C` and `Python 2.x` — and they differ only in what has to
be written down to justify it.** The tracked tree at the pin contains exactly twelve files, and every
one of them is C source, a C header, Python, or plain text; there is no third language file to include
or exclude. The readings diverge only if "present" is stretched to cover the project's *ancestry*,
which Field 13 does not describe. Every inclusion and exclusion below follows from that single
criterion.

**`C` — included.** The three extension modules (`cxformmodule.c`, `igrfmodule.c`, `rigiditymodule.c`)
and all the numerical code (`cxform-auto.c`, `cxform-manual.c`, `igrf_sub.c`, `rigidity.c`) are C, and
`setup.py` compiles them. GitHub's language breakdown at the export reports 184,515 bytes of C against
793 bytes of Python.

**`Python 2.x` — included, replacing `Python 3.x`.** The package is a Python package: it ships
`magnetosphere/__init__.py`, is installed by `setup.py`, and exists to expose these routines to Python
callers. The edition is Python 2, and the evidence is mechanical rather than inferential:

1. **All three extension modules hard-code a Python 2.5 header path.** `git grep -P` at the pin matches
   `#include <python2.5/Python.h>` in exactly three files — `cxformmodule.c`, `igrfmodule.c`,
   `rigiditymodule.c` — which is every extension module in the package.
2. **All three use the Python 2-only module-initialisation C API**, calling `Py_InitModule` from an
   `init<name>(void)` entry point (`initcxform`, `initigrf`, `initrigidity`). Python 3 removed
   `Py_InitModule` in favour of `PyModule_Create` and requires the entry symbol `PyInit_<name>`.
3. **The predicted Python 3 construct is absent.** `git grep -c 'PyInit_'` across the whole tracked
   tree at the pin matches **0 files**, against a control of **3 files** matching `Py_InitModule` in
   the same run. That is a negative where one is predicted, produced by the same command shape that
   demonstrably finds the Python 2 form — not an unfalsifiable blank.
4. Corroborating: `setup.py` line 1 is `#!/usr/bin/python` and line 2 imports from `distutils.core`.

Consequently the package **cannot compile, let alone import, under Python 3** as it stands. Two
independent sources agree. The project's own Google Code wiki page states "Works with Python 2.5;
hasn't been tested yet with other versions." And the PyHC community registry grades this project's
`python3` standard as `"Requires improvement"` — the red badge. That grading is hand-curated, but it
should be weighted for what it is: five of the six standards on this entry — `community`,
`documentation`, `testing`, `software_maturity` and `python3` — carry the identical `"Requires
improvement"` value, and only `license` differs (`"Good"`). A row that uniform reads as a judgment on
the project overall rather than a targeted finding about Python 3 specifically, so it is consistent
with the conclusion without being independent evidence for it. The decisive evidence remains the
pinned source itself.

**`Fortran77` / `Fortran90` and the Fortran rows generally — excluded.** This is the most tempting
wrong answer, so the reason is worth keeping. `igrf_sub.c` opens
`/* igrf_sub.f -- translated by f2c (version 20050501).`, `rigidity.c` opens with the analogous
`rigidity.F` line, and `setup.py` links `libraries = ['m', 'f2c'], library_dirs = ['/usr/lib/'])`. So
Fortran is unmistakably in this code's *lineage*. But no Fortran is compiled and none is shipped:
`git ls-tree -r` at the pin lists **no file** with a `.f`, `.for`, `.f77` or `.f90` extension. What the
package builds is C — machine-generated C, but C, and C is what a maintainer must read and edit. The
Fortran originals were vendored historically and deleted at commit `5d03aaa` (2010-07-16). Listing
Fortran would tell a user to expect Fortran source and a Fortran toolchain, and both expectations would
be false; the `libf2c` runtime dependency belongs in the prose, which is where it now is.

**`IDL` — excluded.** The README's long "USAGE FROM IDL" section, complete with `IDL>` transcripts, is
part of the vendored CXFORM documentation and describes CXFORM's DLM interface, which this package does
not build. The IDL source that would have supported it (`date2es.pro`) was among the files deleted at
`5d03aaa`; no `.pro` file is tracked at the pin. This is precisely the README-boundary trap described in
the scope note.

**Perl — excluded, and there is no `Perl` row in the vocabulary in any case.** The README's "ADDING NEW
COORDINATE SYSTEMS" section instructs the reader to run a Perl generator — "Once you do that, the Perl
script will generate code to" convert between all systems — but `gen_cxform_auto.pl` was deleted at
`5d03aaa` and is not in the tree. The instruction is inherited CXFORM documentation for a workflow this
package cannot perform.

**`Other` — considered and rejected.** Nothing here falls outside the vocabulary's coverage; `C` and
`Python 2.x` describe the package fully.

**The correction from `Python 3.x` to `Python 2.x` was made deliberately, not incidentally.** Nothing
evidential supported the stored `Python 3.x`; the only argument for keeping it would have been a
reluctance to disturb a stored value, and that is not a reason. `Python 2.x` is an existing vocabulary
row, so — unlike the licence in Field 15, where the accurate value has no row — the correct value here
is representable and there was no need to settle for an approximation. The three mechanical facts at
the pin are decisive on their own: the `python2.5` include in all three extension modules, the
`Py_InitModule`/`init<name>` API in all three, and `PyInit_` matching zero files against a three-file
control. The project's own wiki statement and PyHC's `python3: "Requires improvement"` grading agree
with them without being needed to reach the conclusion.

### 14. Reference Publication (OPTIONAL)

**Not found.**

No paper describes this software. This is researched, with controls:

- ADS/Sci-X full-text search for `"python-magnetosphere"` returns nothing, while control queries on the
  same route return results (`full:"cxform"`, `author:"Parunakian, D"`, `title:"pysat"`), a nonsense
  title returns 0, and a deliberately invalid token returns an authentication error rather than 0 — so
  an empty result is distinguishable from a broken route.
- DataCite returns nothing for the package name and nothing matching it among the Parunakian-authored
  records (Field 2).
- The repository contains no JOSS paper, no `paper.md`, no `CITATION.cff` and no "how to cite" section
  in the README.

The IGRF-11 model paper is a real and useful publication, but it describes the *model this software
wraps*, not the software. It is considered under Field 27, where that distinction is argued out;
putting it here would tell a citing user that Finlay et al. wrote this package.

### 15. License (RECOMMENDED)

`GNU General Public License v3.0 or later`

Retained. Four independent sources agree the licence is GPL version 3: the `LICENSE` file at the pin is
the GPLv3 text, beginning "GNU GENERAL PUBLIC LICENSE" and "Version 3, 29 June 2007"; the README's
Legal section states "This project is distributed under the terms of the GNU General Public License
v.3."; GitHub reports the SPDX identifier `GPL-3.0`; and the Google Code archive recorded the project's
`license` as `gpl3`.

**The "or later" half of the stored value is not evidenced, and the honest position is that the
vocabulary cannot express the alternative.** No source states an "or later" grant: the README says
"v.3" flatly, and no source file in the tree carries a per-file licence header. The phrase "any later
version" does occur three times in `LICENSE` — twice inside Section 14, "Revised Versions of this
License" (lines 572 and 574), and once inside the "How to Apply These Terms" appendix (line 640). All
three are standard GPLv3 text, present in every copy of the licence regardless of what a licensor
elects, and none of them is a statement about this project's election. The evidence therefore points at GPL-3.0-**only**.

But the License vocabulary contains no GPL-3.0-only row. Its GPL-family rows are
`GNU General Public Licenses (GPL version 2)`, `GNU General Public License v3.0 or later` and
`GNU Lesser General Public License v3.0 only`. So `GNU General Public License v3.0 or later` is the
nearest representable value and is correct to keep; there is no better row to move to, and proposing an
unstorable value would only fail on submission. This is recorded so a later refresh does not re-open it
and reach for a row that does not exist.

Two further notes for whoever revisits this:

- **`Other` was considered and rejected.** It would discard the accurate "GPLv3" information in exchange
  for expressing an unevidenced-modifier scruple, leaving the catalogue user worse informed.
- **Google Code's `contentLicense: cc3-by-nd` is not this field.** The archive records it alongside
  `license: gpl3`, and it governs the project's wiki content, not its code. It must not reach Field 15.

There is also no per-software licence URI to record: HSSI stores the licence as a reference to a shared
licence entry that carries the URL, so the URI is not a property of this record.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

Retained from the existing HSSI record (stored lower-case; the catalogue renders them title-cased,
which is a display transform and not the stored value):

- coordinate transformations
- cosmic ray
- cutoff rigidity
- earth magnetic field
- field line tracing
- geomagnetic cutoff
- geomagnetic field
- heliophysics
- igrf
- l shell
- magnetosphere
- space physics

Four further keywords are recorded, all of them existing keyword rows rather than new coinages:

- **`igrf11`** — the package wraps IGRF specifically at its **eleventh** generation, which is the fact
  that distinguishes it from every other IGRF wrapper in the catalogue. The generic `igrf` keyword is
  already stored and does not carry that.
- **`spherical harmonics`** — the `igrf.b` docstring describes the computation as using "the spherical
  harmonics model", and it is the model's actual mathematical form.
- **`kp index`** — `rigidity.correctedcutoff(rig, kp, lt)` takes the Kp index as a parameter; this is
  the only keyword that surfaces the rigidity module's activity dependence.
- **`empirical model`** — matches the Field 4 classification and is how a user filters for IGRF-class
  models.

Considered and rejected, with reasons:

- **`python`** — true of most of the catalogue, so it distinguishes nothing.
- **`cxform`** — genuinely distinguishing, but no such row exists and a keyword nobody else would
  search is catalogue clutter; the capability is already covered by `coordinate transformations`, and
  CXFORM itself is recorded properly under Field 29.
- **`magnetic field modeling`** — duplicates the stored `geomagnetic field` and `earth magnetic field`
  without adding a search path.
- **`radiation belts`** — L-shell is a radiation-belt coordinate, but the package models no belt
  physics; the association is carried more honestly by `Earth Inner Magnetosphere` in Field 5.
- **`wrapper`** — accurate but uninformative as a search term.

### 17. Data Sources (OPTIONAL)

**None.**

**At the pinned revision the package performs no data acquisition of any kind.** This is measured, and
it is a stronger statement than "no data source was found":

- Sweeping all twelve tracked files at the pin for `socket`, `connect(`, `curl`, `wget`, `urllib`,
  `popen`, `system(`, `exec[lv]`, `fork(` and `download` returns **no hit anywhere**.
- Every `http://` and `ftp://` occurrence at the pin — 26 in total — is inside a comment,
  documentation text, or `setup.py`'s `url=` metadata field. The breakdown: four in the GPL text of
  `LICENSE`; ten in the README, of which four fall in Parunakian's own section before the vendored
  CXFORM block begins (the NSSDC FTP path, the IGRF homepage, and the CXFORM website named twice) and
  six fall inside the vendored documentation; nine in `cxform-manual.c` comments; one apiece in
  `igrf_sub.c` and `rigidity.c` pointing at netlib's `libf2c`; and one in `setup.py`. None is fetched
  at build time or run time.
- There is no C-level file I/O either: `fopen`, `fwrite`, `fclose` and `fscanf` match nothing in the
  tree.

**The one real file access, and why it still does not make this field non-empty.** The `igrf` module's
exported functions all route through `feldcof_`, which calls `getshc_` twice, and `getshc_` performs a
Fortran `f_open` on a **local filesystem path**. The path is hand-patched into the `f2c` output at
`igrf_sub.c` line 1718:

```
    extern char *trimwhitespace(char *str); char prefix_dp[28] = "/usr/local/lib/igrf/"; strcat(prefix_dp, fspec); o__1.ofnm = trimwhitespace(prefix_dp);
```

`fspec` is one of the twenty-four coefficient-file names held in `feldcof_`'s `filmod` table
(`igrf1900.dat` through `igrf2010s.dat`). This is a local read of internal model coefficients, not the
acquisition of science data from a source, so no `DataInput` row applies. It is recorded here because
it matters for Fields 18 and 24.

**A durable consequence of the pin commit that a future maintainer should know.** Commit `806be11d`
(2011-02-08) deleted all twenty-five `dat/*.dat` files and removed the `data_files` block from
`setup.py` — `git show --numstat` reports the twenty-five deletions and `setup.py` at `+1/-11` — while
leaving the `feldcof_`/`getshc_` read path exactly as it was. The commit did add `igrf11syn_`, the
official IGRF-11 synthesis routine carrying its coefficients inline as `f2c` data statements, but
**that routine is never called**: `git grep -n 'igrf11syn_'` at the pin matches exactly two lines,
`igrf_sub.c:121` opening its definition and `igrf_sub.c:707` closing it. No exported Python function
reaches it. So as shipped at the pin, `igrf.dimo`, `igrf.lb`, `igrf.b` and `igrf.b0` still try to open
coefficient files under `/usr/local/lib/igrf/` that the package neither contains nor installs. Anyone
reasoning about this entry's functionality — or tempted to describe the coefficients as "compiled into
the source" — needs that distinction: the coefficients were added to the file, but not to the code path
the package actually uses.

**Rejections recorded rather than left as a silent blank:**

- **`SSCWeb`** is a real `DataInput` row, and SSCWeb is named several times in the README — "The bulk of
  the testing used SSCWeb's Locator Tabulator as the data source." and "SSCWeb's calculations (based on
  GEOPACK), and in many cases are within" — but every one of those mentions is inside the vendored
  CXFORM README, describing how *CXFORM* was validated in 2004. This package neither queries SSCWeb nor
  ships any code that could. Selecting it would be the README-boundary error described in the scope
  note.
- **`FTP/FTPS Directories`** is likewise a real row, and it *would* have been correct for an earlier
  state of this project. The Google Code wiki page describes the original behaviour: "IGRF downloads
  the source code and coefficient files from the official NSSDC repository, translates the original
  Fortran code to C, patches it, and compiles into a Python module." That download-at-install-time
  behaviour was deliberately removed at commit `33147a6` (2010-07-14, "Added required software into the
  distribution to avoid complications (NASA servers have a pretty low uptime)"), and the same wiki page
  announces the intent: "I also plan to provide required C source files in the package instead of
  downloading them from NSSDC FTP archive during installation." The wiki revision predates that change
  and describes a state of the software that has not existed since mid-2010. The README's surviving
  pointer — "The source code and coefficient files used can be found at
  ftp://nssdcftp.gsfc.nasa.gov/models/geomagnetic/igrf/fortran_code/" — is an attribution telling the
  reader where the upstream model lives, not a fetch the software performs.
- **`Observatory/Mission-specific`**, **`CDAWeb`**, **`OMNIWeb`**, **`HAPI`**, **`Madrigal`**,
  **`AMDA`**, **`VirES`**, **`WDC`**, **`GFZ`**, **`das2`**, **`TAP`**, **`S3/Cloud-aware`**,
  **`HTTP/HTTPS Directories`**, **`The Virtual Solar Observatory.`** — none appears anywhere in the
  tree and none has a corresponding code path.
- **`Other`** — rejected because the field would then assert that some unlisted source is supported,
  which is false. An evidenced empty value is the correct outcome.

### 18. Input File Formats (RECOMMENDED)

**None.**

Every exported function takes scalars — a coordinate frame pair and a vector, or latitude, longitude,
altitude and decimal year, or a rigidity, Kp value and local time. No exported function accepts a
filename, a file handle, or a buffer, and the package ships no reader for any data format.

**The one candidate, considered and rejected with its reasoning, because it is a close call.** The
`igrf` module does read files: the IGRF coefficient sets under `/usr/local/lib/igrf/` (Field 17), via
Fortran list-directed reads, so those files are plain text and `ascii` is a real vocabulary row.
`ascii` is nonetheless the wrong answer here for two reasons. First, those files are *internal model
coefficients*, not user data: a user never chooses them, names them, or supplies them through the API,
and the field asks about the formats the software supports "for data input". Second, at the pin the
package neither ships nor installs them, so it does not even present that read path as a usable
feature. A searcher filtering for tools that ingest ASCII data would be misled by this entry appearing
in the results.

If a future maintainer restores the coefficient files and wishes to reflect that read path,
`ascii` is the row that would apply — but it should be a deliberate decision, not a rediscovery of this
same near-miss.

### 19. Output File Formats (RECOMMENDED)

**None.**

The package writes no files. Every exported function returns its results as a Python tuple built with
`Py_BuildValue`; there is no serialisation code, no C-level write call, and no Fortran write to a file
unit. The only Fortran formatted-write reachable from an exported function is `getshc_`'s error branch
at `igrf_sub.c:1781`, which emits an "Error while reading" message to a console unit when a coefficient
file cannot be opened — a diagnostic message, not a data output format. Two further formatted-writes
exist, at `igrf_sub.c:531` and `:703`; both sit inside `igrf11syn_`, which Field 17 establishes is
never called from any exported function, and both write IGRF date-range warnings to Fortran unit 6.
Unit 6 is a console unit, so no write anywhere in the tree targets a file.

### 20. Operating System (RECOMMENDED)

HSSI held four operating systems before this refresh — `Linux`, `Mac`, `Solaris` and `Windows`. Two of
them are removed; what remains is the pair this project's own evidence attests:

- Linux
- Mac

**These four values very probably came from a sentence about a different piece of software, and the
correspondence is too exact to be coincidence.** Inside the vendored CXFORM README the following line
appears: "It has been tested under SunOS v5.7, Microsoft Windows 2000/XP, Mac OS X 10.3 &" — continuing
on the next line to Linux, and mentioning Solaris 2.6 and DEC OSF/1 immediately after. That sentence
describes **CXFORM**, the standalone C and IDL library, which builds with its own Makefile and its own
MSVC batch file (`make_CXFORM_MSVC.bat` — a file this package does not ship). It is not a statement
about `python-magnetosphere`, and the stored set maps one-to-one onto it: SunOS/Solaris → Solaris,
Microsoft Windows → Windows, Mac OS X → Mac, Linux → Linux.

**What the pinned package itself supports.** The evidence is Unix-shaped throughout:

- All three extension modules `#include <python2.5/Python.h>` — a path that resolves on
  Debian/Ubuntu-style layouts where headers live under `/usr/include/python2.5/`, and not on a Windows
  Python installation, where `Python.h` sits at the include root.
- `setup.py` declares `libraries = ['m', 'f2c'], library_dirs = ['/usr/lib/'])`, hard-coding a POSIX
  library path and requiring `libm` and `libf2c`.
- The coefficient path is hard-coded as `/usr/local/lib/igrf/` (Field 17).
- The author's own published binary build is `Magnetosphere-0.1.linux-x86_64.tar.gz`, and no binary was
  ever published for any other platform.
- Of the carried-over Google Code issues, one is titled "Installation issues and tips for Linux
  (Ubuntu) and other Python versions" and another is "Compiling issue on Mac" — so Linux use is
  attested, and a Mac build attempt is attested as having gone wrong.

There is **no evidence at all** that this Python package builds on Windows or Solaris beyond the
misattributed CXFORM sentence.

**Why two, and not four, and not one.** Keeping all four was considered and rejected: it would tell a
catalogue user that this package installs on Windows and Solaris, and the only support for that claim
is a sentence about a different library. Reducing to `Linux` alone — the strictest reading of
"operating systems the software can successfully be installed on" — was also considered and rejected.
`Mac` does rest on weaker evidence than `Linux`, since the Mac attestation is an attempted build that
hit a problem rather than a build that succeeded; but it is package-specific evidence rather than the
CXFORM misattribution, and a user attempting a Mac build is exactly the user this entry should reach.
The two retained values are the two for which direct, package-specific evidence exists.

`Operating System Independent` was considered and rejected outright: the package compiles C
extensions against hard-coded POSIX paths, so it is emphatically not OS-independent.

### 21. CPU Architecture (RECOMMENDED)

- CPU Independent
- x86-64

Both stored values are retained, and both are defensible even though they look as though they pull in
opposite directions.

`x86-64` is directly attested: the author published `Magnetosphere-0.1.linux-x86_64.tar.gz`, an AMD64
binary build, through the project's own Google Code downloads. That is the only architecture for which
a built artifact ever existed.

`CPU Independent` describes the *source*: the tree contains no assembly, no SIMD intrinsics, no
architecture-conditional compilation and no CPU-specific build flags, so the C sources compile
wherever a C compiler and `libf2c` are available. The pair therefore reads as "portable source, with a
published binary for x86-64", which is accurate.

`Apple Silicon arm64`, `Linux aarch64 or arm64`, `Sun (SPARC)`, `GPU`, `HPC or HEC` and `ppc64le` were
each considered and rejected: no build, artifact or documentation evidence exists for any of them, and
`Sun (SPARC)` in particular would be the CPU-level version of the Field 20 misattribution, since the
only Solaris mention in the tree is CXFORM's.

### 22. Related Phenomena (OPTIONAL)

- Geomagnetic Storms

`Geomagnetic Storms` is recorded, and the reasoning on both sides is preserved below: the call was a
close one and a later refresh should not re-open it without meeting the argument that settled it.

The Phenomena vocabulary is short and closed — `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`, `X-ray emission` — and enumerating
it is itself the reason most of the field is correctly empty. Five of the seven are solar phenomena
that this package has no bearing on whatsoever. `Solar Wind` was considered and rejected: the package
provides heliospheric coordinate frames in which solar-wind data are expressed, but it contains no
solar-wind physics, model or analysis, and selecting it would return this entry to users looking for
solar-wind tools.

That leaves one genuine candidate.

**`Geomagnetic Storms` is recorded on this evidence.** `rigidity.correctedcutoff(rig, kp, lt)` takes
the Kp geomagnetic-activity index and local time as explicit parameters and returns a corrected cutoff
rigidity. Kp-dependent suppression of the geomagnetic cutoff is a storm-time effect, and it is the
whole point of that function — the only place in the package where geomagnetic disturbance enters the
physics at all. A user studying storm-time particle access would be glad to find this entry returned.

**The reservation against it was weighed and did not carry, and it is preserved here because it is
real.** Read strictly, the evidence points the other way: Kp parameterisation covers all activity
levels, quiet as well as disturbed, so the function is not storm-specific; the package models no storm,
computes no storm index and ingests no storm data; and the fact that `Geomagnetic Storms` is the only
row that could be argued for at all is itself a hint that the vocabulary has no term for what this
software actually does. The physically exact terms — cosmic-ray access, cutoff suppression,
solar-energetic-particle events — have no Phenomena rows, and Field 22 rejects free text, so those
concepts are carried instead by Keywords (`cosmic ray`, `cutoff rigidity`, `geomagnetic cutoff`,
`kp index`), which is the open vocabulary and their proper home. On that reading the field would have
been left empty, and emptiness was the position initially favoured here.

It was overridden deliberately. The settled judgment is that a Kp-dependent cutoff correction is a
genuine, if narrow, storm-time capability, and that a searcher filtering for storm-related tooling is
better served by finding this package than by not finding it. A later refresh proposing to empty the
field must meet that judgment rather than merely restate the reservation, which was heard.

### 23. Development Status (RECOMMENDED)

**`Unsupported`**. HSSI held no development status for this entry before this refresh.

The choice lay between `Inactive` and `Unsupported`, and it turned on their definitions rather than on
a general impression of dormancy.

**`Abandoned`, `Concept`, `WIP` and `Suspended` are all excluded by the same fact:** each of them
requires that the project has *not* reached a stable, usable release, and this project did release.
`Magnetosphere-0.1.tar.gz` was published on 2010-07-16 with generated distutils metadata inside it
(Field 12). `Moved` is excluded because there is nowhere it moved to: the Google Code archive records
`movedTo` as empty, and the GitHub export is the same project rather than a successor. `Active` is
excluded by the commit history ending 2011-02-08.

**The evidence bearing on the remaining two:**

- The last commit is `806be11d`, 2011-02-08. Nothing has been committed since.
- The repository is **not** archived on GitHub (`archived: false`), and the inference from an archived
  repository to `Unsupported` does not extend to repositories that are merely quiet but still open. So
  dormancy alone is not being used to reach `Unsupported` here.
- What *is* being used is more than dormancy. Four issues stand open, all carried over from Google Code
  by the export bot on 2015-03-13, and three of them are reports that the package will not install or
  build: "Cannot install Module- Beginer", "Installation issues and tips for Linux (Ubuntu) and other
  Python versions", and "Compiling issue on Mac". None has an author response. The fourth, "Pass
  datetime object to cxform.transform()", is a feature request that the code comment at
  `cxformmodule.c` shows was contemplated and left commented out.
- The project's own home is gone and its stated plans — the wiki announces intentions to add "the
  paraboloid model of the magnetosphere, Tsyganenko model, AP8/AE8" — were never carried out.
- There are no git tags and no GitHub releases.

**Why `Unsupported` rather than `Inactive`.** `Inactive` makes an affirmative promise:
"support/maintenance will be provided as time allows". The record directly contradicts that promise —
three unanswered installation-failure reports have stood for over a decade. `Unsupported`'s definition
("the author(s) have ceased all work on it. A new maintainer may be desired") matches the observable
situation, and its second sentence is a fair description of a package that PyHC still lists and whose
capability nobody has taken over.

**The case for `Inactive`, weighed and not taken.** It is not baseless. The repository is not archived
on GitHub, and the author did act on the project as recently as 2015 by performing the Google Code
export, so inferring cessation of *all* work from silence is a step that deserves resistance. Either
value would have been a defensible enrichment over an empty field; this was a choice between two honest
descriptions rather than between a right answer and a wrong one. `Unsupported` was chosen because the
three unanswered installation-failure reports are direct evidence against `Inactive`'s affirmative
promise of support as time allows, and because a 2015 repository export is an act of preservation
rather than maintenance of the software. A later refresh may revisit this if the situation changes, but
should not flip it merely on the observation that the repository is unarchived — that observation was
already before this decision and did not carry it.

### 24. Documentation (RECOMMENDED)

`https://github.com/dpq/python-magnetosphere/blob/master/README`

Retained. The `README` is the only documentation the project has: there is no `docs/` directory, no
ReadTheDocs configuration, no generated API reference, and the PyHC registry entry carries no `docs`
field for this project (it grades the project's `documentation` standard as `"Requires improvement"`).
The URL answered HTTP 200 on 2026-09-08.

**A caveat that materially affects how much weight this documentation can carry.** The pinned README
states, in Parunakian's own installation section:

> IGRF coefficient files will be installed to /usr/local/lib/igrf.

**The pinned `setup.py` does not do this.** It has no `data_files` entry at all — that block was
removed at commit `806be11d`, the same commit that deleted the twenty-five coefficient files (Field
17). The earlier `setup.py`, at the pin's parent, did install them, but to `/usr/lib/igrf` rather than
the `/usr/local/lib/igrf` the README names and the C code hard-codes, so the two were inconsistent even
before the block was removed. This sentence must never be repeated as though it described pinned
behaviour. It is in the same class as a README documenting a removed command, and together with the
"two modules" staleness noted under Field 8 it means the README is reliable about the *API* and
unreliable about *installation*.

Alternatives considered and rejected: the Google Code wiki page, whose content describes the
download-at-install-time behaviour removed in 2010 and would misinform a user, and which in any case
has no usable public address — the archive's wiki endpoint returned 403 on 2026-09-08 and the archive
landing page is a JavaScript shell carrying no wiki text, so the only plainly retrievable copy is the
`wiki` branch of this repository; and the Google Code archive landing page itself, which is a
historical record rather than documentation.

### 25. Funder (OPTIONAL)

**Not found.**

No funder is identified anywhere. Sweeping the whole tracked tree at the pin for `grant`, `fund`,
`award`, `sponsor` and `contract no` (case-insensitive) matches only `LICENSE`, where the hits are
ordinary English words in the GPLv3 text. Neither the README, `setup.py`, nor any source file contains
an acknowledgements section, a grant number, or a funding statement.

The usual richer route is closed here: Fields 2 and 14 establish that there is no DOI record and no
reference publication, so there is no Acknowledgments section and no Data Availability Statement to
read. This is a genuine absence rather than an unsearched field, and a future refresh will not find a
funder unless the author publishes about the software.

### 26. Award Title (OPTIONAL)

**Not found.**

Same evidence as Field 25 — no award title, award number, grant identifier or sponsoring programme
appears anywhere in the repository, and there is no publication whose acknowledgements could supply
one.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- `https://doi.org/10.1111/j.1365-246X.2010.04804.x`

That entry is the paper defining the IGRF-11 model. It is there on a deliberate reading of what Field
27 covers, not by default; the reasoning is set out below.

No publication cites, describes or uses this software. That negative is established under Field 14 with
controls on both ADS/Sci-X and DataCite, and it is not restated here.

The only publication with any claim on this field is the paper describing the model the `igrf` module
wraps:

> Finlay, C. C., *et al.* (2010). International Geomagnetic Reference Field: the eleventh generation.
> *Geophysical Journal International*, **183**(3), 1216–1230.
> `https://doi.org/10.1111/j.1365-246X.2010.04804.x`

The citation was verified by content-negotiating that DOI: it resolves to a journal article with that
exact title, in that journal, volume, issue and page range, issued 2010-10-12, with 35 authors of whom
Finlay is first. The connection to this software is direct rather than thematic — the package's `igrf`
module is a wrapper over the IGRF-11 coefficient sets and synthesis routines this paper defines, and
the README's IGRF section reproduces the model release notes describing exactly that generation.

**Why a wrapper's Related Publications carries the wrapped model's defining paper.** This was decided
deliberately, and neither answer was a default. Finlay et al. is the only citable scientific reference
for what this software computes: a user who publishes results obtained with `igrf.b()` must cite it,
the package itself offers no citation guidance, and this record is the only place HSSI could tell them
so. The relationship is specific rather than thematic — this package wraps IGRF at the eleventh
generation, and this is the eleventh generation's paper.

The argument against was taken seriously and is worth knowing. Field 27 covers publications that
describe, cite or use the software, and this paper does none of those three: it predates the wrapper's
IGRF-11 update and its authors have no connection to it. Recording it risks implying the software is
described in the literature when it is not, and the same argument would attach a model paper to every
wrapper in the catalogue, diluting what the field means. That risk was accepted for two reasons. The
searcher benefit is concrete, where the alternative leaves a user with no citable reference at all; and
the description (Field 8) already makes plain that the software wraps the model rather than originating
it, so the entry does not read as a claim of authorship. The distinction between "software this paper
describes" and "model this software implements" is preserved where it matters most — Field 14 is kept
empty precisely to hold that line.

### 28. Related Datasets (OPTIONAL)

`https://www.ngdc.noaa.gov/IAGA/vmod/coeffs/igrf11coeffs.txt`

HSSI held no related dataset before this refresh.

The IGRF-11 spherical-harmonic coefficient set is the data this software exists to evaluate. It is not
an incidental input: `feldcof_` selects between twenty-four coefficient epochs (`igrf1900` through
`igrf2010s`) and interpolates or extrapolates between them, and every one of `igrf.dimo`, `igrf.lb`,
`igrf.b` and `igrf.b0` calls it first. The project itself points at this publisher — Parunakian's
section of the README says "More information on IGRF can be found here:
http://www.ngdc.noaa.gov/IAGA/vmod/igrf.html", and the vendored IGRF release notes repeat it. The URL
above is the IAGA/NGDC publication of the eleventh-generation coefficients specifically, matching the
generation this package implements; it returned HTTP 200 with `text/plain` on 2026-09-08, and it is 59
characters, well inside the length limit. It is also the URL under which HSSI already catalogues the
IGRF-11 coefficient file, so the relation binds to the existing item rather than creating a duplicate.

Considered and rejected:

- **The per-epoch `dat/*.dat` files this code actually opens.** They are the NSSDC/IRI-format
  rearrangement of the same IAGA coefficients, they have no citable landing page, and they are not
  shipped at the pin (Field 17). The IAGA publication is the citable form of the same data.
- **The NSSDC FTP path in the README**
  (`ftp://nssdcftp.gsfc.nasa.gov/models/geomagnetic/igrf/fortran_code/`) — it points at *source code*,
  not a dataset, and anonymous FTP to that host is refused (it answered `550` on 2026-09-08). Field 29
  covers the code relationship properly.
- **A cutoff-rigidity dataset.** `rigidity.c` carries its own tabulated grid inline and cites no
  external dataset; there is nothing to link.

### 29. Related Software (OPTIONAL)

**Recorded, in order of strength:**

1. `https://github.com/edsantiago/cxform`
2. `https://github.com/lkilcommons/igrfpy`
3. `https://github.com/space-physics/igrf`

HSSI held no related software before this refresh. One relevance bar was applied to all candidates: an
entry earns a place only if it tells a reader something *about this software* — a component it is built
from, a predecessor, or a package doing the same job differently. Anything that would read identically
for an arbitrary Python package was excluded.

**1. CXFORM — the strongest relation in this record, and it is provable byte for byte.** This package
does not depend on CXFORM; it *contains* it. `cxform-auto.c`, `cxform-manual.c` and `cxform.h` are
CXFORM's own sources, and `magnetosphere.cxform` is a thin Python wrapper around `cxform()` and
`date2es()`. The README carries CXFORM's own header — "CXFORM:  An IDL/C library to convert between
spacecraft coordinate systems" — and its authorship credits (Field 6). The identification with Ed
Santiago's repository was verified rather than assumed: `cxform.h` and `cxform-auto.c` at this
package's pin are **sha256-identical** to the same-named files in `edsantiago/cxform`, and
`cxform-manual.c` differs by 56 changed lines (1,010 lines here against 1,012 there), consistent with
that repository carrying later modifications to the hand-written half of the package. Corroborating
this, every file of the vendored `cxform-0.71/` distribution that this project deleted at commit
`5d03aaa` is present in that repository: `Makefile`, `cxform-dlm.c`, `cxform.def`, `cxform.dlm`,
`date2es.pro`, `gen_cxform_auto.pl`, `install.txt`, `main.c`, `make_CXFORM_MSVC.bat`, `readme.txt`,
`test_ssc_data.dat` and `tester.c` (the same commit also removed fourteen AppleDouble `._` companions
of those files, and the vendored NSSDC Fortran `bilcal.for`, `igrf_sub.for` and `shellig.for`).

  **On the choice of URL.** The CXFORM address the README gives —
  `http://nssdcftp.gsfc.nasa.gov/selected_software/coordinate_transform/`, cited three times — is dead:
  on 2026-09-08 it redirected to the corresponding SPDF path and returned HTTP 404. The distribution
  *is* still served by NASA at
  `https://spdf.gsfc.nasa.gov/pub/software/old/coordinate_transform/`, which answered 200 the same day
  and is the CXFORM home page naming both Ed Santiago and Ryan Boller; its parent directory's timestamp
  of 2009-11-25 matches the v0.71 date in the README's own version history, so it is the same
  distribution relocated. The GitHub repository is recorded as the Field 29 value in preference to it
  because the field asks for a code repository, and because a git repository is the more durable of the
  two references. The SPDF page is recorded here so a future maintainer has both.

**2. `igrfpy` — the closest peer in kind and in model generation.** Its own repository describes it as
"Python wrappers on the International Geomagnetic Reference Field 11&12 Fortran code", which is
precisely what this package's `igrf` module is, at the very same eleventh generation. Two Python
wrappers over the same IGRF-11 Fortran, built independently, is the textbook Field 29 relation:
similar task, different assumptions and interface.

**3. `space-physics/igrf` — the same species, a later model generation.** Its repository describes it
as "International Geomagnetic Reference Field IGRF13 in Python and Matlab". It answers the question a
user of this package will eventually ask — where to go for a maintained wrapper over a current IGRF —
which is exactly the kind of thing a catalogue relation should carry.

Both URLs above are chosen to match the URLs under which HSSI already catalogues those packages, so the
relations bind to the existing items rather than creating new ones. Both are 37 characters.

**Considered and rejected, with reasons:**

- **The catalogue's IGRF-14 entry.** Its repository value is a NOAA product landing page for the model
  release rather than a peer software package, so listing it would point at the *model* rather than at
  similar software. The model relationship is already carried properly by Field 28 and by Field 27.
- **GEOPACK.** The README mentions it — "SSCWeb's calculations (based on GEOPACK), and in many cases
  are within" — but only inside the vendored CXFORM README, as the reference implementation CXFORM's
  results were compared against in 2004. This package neither wraps, depends on, nor competes with
  GEOPACK. Listing it would propagate the README-boundary error. (Beware also that the name is reused
  by an unrelated Python package, so a name-based search will mislead.)
- **SSCWeb.** A web service, not software, and mentioned only as CXFORM's validation data source. It is
  addressed under Field 17.
- **`libf2c`.** A genuine link-time dependency (`libraries = ['m', 'f2c']`), but it is a Fortran-to-C
  runtime support library — generic infrastructure that would be equally at home in any f2c-translated
  codebase in any field. It says nothing about this software's science and is excluded by the same
  test that excludes the generic scientific-Python stack.
- **The `pygrf` predecessor.** This is the most interesting rejection. The 2009-12-27 Google Code
  download contains a distinct earlier package, `pygrf`, wrapping IGRF-10 (Field 10) — a genuine
  predecessor, and the field explicitly welcomes predecessors. It is nonetheless omitted because it has
  no repository of its own and no durable public URL: the only place it exists is inside a Google Code
  archive download whose continued availability is not something HSSI can rely on. Its existence is
  recorded here instead, which is the useful part.
- **numpy, and the generic Python stack generally.** Not applicable in any case: this package has no
  Python dependencies at all beyond the interpreter. Its three modules are pure C extensions.

### 30. Interoperable Software (OPTIONAL)

**None.**

This is a correct empty value, not an unexamined one. Field 30 requires a *demonstrated exchange* —
a shared or converted data model, output from one package imported into another, an adapter or
converter API, a plugin relationship, a companion package, or a bridge to a named domain tool. The
package offers none of these, and the reason is structural rather than incidental:

- Every exported function returns a plain Python tuple of floats built with `Py_BuildValue`. There is
  no data model to share and nothing to convert.
- Every exported function accepts scalars. There is no ingest path through which another package's
  objects could be handed in.
- There are no adapter or converter functions, no `to_*` or `from_*` API, no plugin or entry-point
  registration, and no companion package.
- There is no cross-language bridge. The IDL interface that CXFORM provides through its DLM is
  precisely the part of CXFORM this package does **not** build (Field 13), so the bridge that would
  otherwise connect this to IDL tooling does not exist here.

The two third-party bodies of code this package embeds, CXFORM and the IGRF Fortran, are *components*
rather than interoperation partners, and they are recorded under Field 29 where components belong.
Ecosystem membership — including PyHC community-registry membership — was considered and rejected as a
justification: it is never sufficient on its own and demonstrates no exchange with any particular
package.

### 31. Related Instruments (OPTIONAL)

**None.** This is an evidenced absence, produced by an exhaustive sweep rather than by not finding
anything obvious.

**The relevance position first.** This package is instrument-agnostic by construction. It computes
model field values and coordinate transformations from a position and a time; it reads no instrument's
data, implements no instrument-specific format or convention, and is not a mission or instrument-team
tool. Under the "designed to support" test it supports no instrument specifically, so the field should
be empty regardless of what the vocabulary contains.

**The sweep, published with its scope and controls, so the negative is falsifiable.** Every `name` and
`abbreviation` of at least four characters in HSSI's SPASE-backed instrument and observatory vocabulary
was extracted and matched case-insensitively, with
non-alphanumeric boundaries, against the full text of all twelve files tracked at the pin. Controls:
the term `igrf`, which is present, is found in six files; a nonsense string is found in none. No total
of extracted terms is recorded here, deliberately: the vocabulary grows, so any figure would be stale
within weeks and unreproducible against a later fetch. What makes the negative falsifiable is the
extraction rule, the match rule and the two controls — all stated above — not a count.

The sweep matched only eight terms, and **every one is a false positive**:

| Term matched | Where | Why it is not an instrument reference |
|---|---|---|
| `cease` | `LICENSE` | the English word, in GPLv3 text; collides with the CEASE instrument's abbreviation |
| `spirit` | `LICENSE` | the English word, in GPLv3 text; collides with the SPIRIT abbreviation |
| `cluster` | `cxform-auto.c` | two code comments, "The first cluster, below, lists the functions defined in cxform-manual.c" and "This second (long) cluster defines the wrappers we generate automatically." |
| `cosmic` | `rigidity.c` | the phrase "cosmic ray penetration"; collides with the COSMIC constellation |
| `ephemeris` | `README`, `cxform-manual.c` | "ephemeris seconds past J2000"; collides with rows literally named "Ephemeris" |
| `greenwich` | `README`, `cxform-manual.c` | "Greenwich Rotating Coordinates", the GEO frame's alias |
| `magnetic field` | `igrf_sub.c`, `igrfmodule.c`, `README` | the physical quantity; collides with rows named "Magnetic Field" |
| `santiago` | `README`, `cxform-manual.c` | Ed Santiago, CXFORM's author; collides with the Santiago observatory |

**IMP-8, separately, because a naive search misses it and a naive reading over-reads it.** A
word-boundary search for `imp8` returns zero files, because the token always continues — `imp8GEI`,
`imp8Time`, `imp8GEO` — so the trailing boundary never matches. Searching unanchored instead finds it
on twelve lines, all in `README`, and all twelve are **IDL example variable names** inside the vendored
CXFORM "Multiple-coordinate example" transcript (lines 152–175). They demonstrate CXFORM's array
handling; they are not a claim that this software supports IMP-8. Rows for IMP 8 instruments do exist
in the vocabulary (`SMWG/Instrument/IMP8/MAG`, `SMWG/Instrument/IMP8/PLS`,
`SMWG/Instrument/IMP8/Ephemeris`), and none of them belongs on this record. This is recorded so a later
agent neither misses the mentions nor mistakes them for evidence.

No entry reached the resolution stage, so no name-without-identifier question arises. Every value in
this field must carry a `https://spase-metadata.org/` identifier; a bare name creates a new
identifierless vocabulary row, which is why omission is the correct outcome here rather than a
best-effort guess.

### 32. Related Observatories (OPTIONAL)

**None.** Same sweep, same evidence, same conclusion as Field 31 — the sweep covered instrument and
observatory rows together, and the only observatory-typed matches were the false positives already
tabulated (`Greenwich`, `Santiago`, `Cluster`, `COSMIC`).

The relevance position is the same: the package is mission- and observatory-agnostic. It works from a
latitude, longitude, altitude and time, which is to say from *any* platform's position or none at all.
No mission's data products, conventions, archives or APIs are supported.

One rejection worth naming explicitly, because it is the one a later agent is most likely to propose:
**SSCWeb is not an observatory.** It is a web service, it appears in this repository only inside the
vendored CXFORM README as the source of CXFORM's 2004 validation comparisons, and it is addressed under
Field 17 where data sources belong.

### 33. Logo (OPTIONAL)

**Not found — researched and unavailable, not unexamined.**

There is no logo candidate in the repository: `git ls-tree -r` at the pin lists **no file** with a
`.png`, `.jpg`, `.jpeg`, `.gif`, `.svg`, `.ico` or `.bmp` extension. The README contains no image
reference of any kind, there is no documentation build with a banner or `html_logo`, and the PyHC
registry entry for this project carries no `logo` field (other entries in the same file do, so its
absence here is meaningful rather than a schema limitation).

**The project did once have a logo, and it is not retrievable.** The Google Code archive records this
project's `logoName` as `vanallen1.jpg` with an `imageUrl` of
`http://code.google.com/p/python-magnetosphere/logo?cct=1394805895`. Followed on 2026-09-08, that URL
redirects to the archive landing page and returns HTTP 200 with content-type `text/html` and 2,438
bytes — an HTML document, not an image. The archive's storage buckets return HTTP 403 for the
corresponding object paths, including `vanallen1.jpg` under both the project and downloads bucket
prefixes, and the landing page's only `<img>` element is Google's own branding PNG. So the historical
logo exists as a filename in a manifest and nowhere else that serves image bytes.

**Do not record any of those URLs.** A Field 33 value must return an `image/*` content-type; a URL that
returns `text/html` renders as a broken image in the catalogue while appearing to work at the HTTP
level. The correct outcome is a documented omission.

Scope note on the two preceding paragraphs: the *contents* of the archive manifest are durable, but the
*reachability* of anything on Google's servers is a statement about someone else's infrastructure, and
every availability claim here is bounded to 2026-09-08. No general claim is made or implied about
whether Google Code logos are preserved elsewhere.
