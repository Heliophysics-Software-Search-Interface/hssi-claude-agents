# HSSI Metadata Extraction Results

**HSSI Software ID:** fd58b98f-87d6-441b-bec8-aa79752f3c5e
**Repository:** https://github.com/swxsoc/sammi
**Source Revision:** 9d2b8975114aab2bef55072a8a75e1590e4570e5
**Extraction Date:** 2026-08-11
**Validation Date:** 2026-08-11
**Validation Status:** PASS

---

**Scope note — read this before interpreting the evidence below.** `sammi-cdf` is a metadata-schema
library, not a science code. It reads YAML attribute schemas and emits Python dictionaries of
metadata attributes for a pipeline to embed in its CDF products, and it can upload an existing CDF
file to an external ISTP validation service. It parses no CDF bytes itself, writes no data files,
computes no physical quantities, and targets no particular instrument, observatory, or physical
region. Several fields below are therefore *correctly* empty or deliberately generic; the reasoning
is recorded so a future agent does not "fill in" a value the software does not support. The pinned
source revision is the `v1.1.0` release tag.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Source note: the person or agent submitting the metadata, not an attribute of the software. The
existing HSSI record carries no submitter identity recoverable from the published metadata, so the
record's original submitter is unknown and no author should be assumed to be that submitter.

### 2. Persistent Identifier (RECOMMENDED)
`https://doi.org/10.5281/zenodo.14887800`

Source note: the Zenodo **concept** DOI, which resolves to the latest version. Corroborated three
ways: the DOI badge in `README.rst`, Zenodo's `conceptdoi` field on each of the three version
records (v1.0.1, v1.0.2, v1.1.0), and the DataCite record for the same DOI. This matches the value
already stored in HSSI, and it is the right kind of identifier for this field — a concept DOI
covering all versions. The version-specific DOI (`10.5281/zenodo.20858467`) belongs in Field 12 and
is recorded there instead.

### 3. Code Repository (MANDATORY)
`https://github.com/swxsoc/sammi`

Source note: matches the stored HSSI value, `pyproject.toml`'s `[project.urls] Homepage`, and the
Zenodo record's `isSupplementTo` link (`https://github.com/swxsoc/sammi/tree/v1.1.0`). The repository
is public and not archived. Note the deliberate mismatch between the repository name (`sammi`) and
the distribution name (`sammi-cdf`) — see Field 7; this is not an error in either field.

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis: Processing
- Mission-related
- Mission-related: Science Data Processing

Source note: HSSI previously stored no functionality at all for this mandatory field. The four values
above were derived by reading the whole public API at the pinned revision — `sammi/cdf_attribute_manager.py`
(`CdfAttributeManager`) and `sammi/validation.py` (`CDFValidator`) are the package's only functional
modules, `sammi/__init__.py` carrying nothing but the version import — plus the eight schema files in
`sammi/data/`, the two test modules, and the user guide. Each subcategory is listed together with its
required parent category.

What the code actually does, and how each value is justified:

- **`Data Processing and Analysis` / `…: Processing`.** `CdfAttributeManager` loads layered YAML
  global (file-level) and variable (measurement-level) attribute schemas, merges them in
  latest-priority order via a recursive `_merge`, and emits validated attribute dictionaries through
  `get_global_attributes()` and `get_variable_attributes()`; `add_global_attribute()` and
  `add_variable_attribute()` set per-file dynamic attributes; `global_attribute_template()` /
  `variable_attribute_template()` emit the required-attribute skeletons; the `*_info()` methods emit
  per-attribute documentation. `CDFValidator.validate()` submits a CDF file to the SPDF ISTP
  validation service and parses the response into a structured error list. These are transformation
  and compliance steps inside a data-processing pipeline, which is what the generic `Processing`
  subcategory covers.
- **`Mission-related` / `…: Science Data Processing`.** The package exists to serve mission science
  data production rather than end-user analysis: its own summary says "for Space Weather data
  processing pipelines"; `pyproject.toml` credits `IMAP SDC Developers` as a package author;
  `imap_processing` (the IMAP Science Operations Center's Level 0–2 processing code) declares
  `sammi-cdf>=1.0,<2` as a core runtime dependency and subclasses `CdfAttributeManager` in
  `imap_processing/cdf/imap_cdf_manager.py`; `swxsoc` (the SWxSOC multi-mission core package)
  declares `sammi-cdf>=0.1.2` in its `cdf` extra. That is participation in mission ground-system data
  production, which is what this subcategory covers. Being multi-mission does not disqualify it: the
  value describes the *kind* of work, and specific mission attribution lives in Fields 31–32, which
  are correctly empty here.

Considered and rejected, with reasons (recorded so these are not re-proposed):

- **`Data Processing and Analysis: File Format Conversion`** — nothing converts between formats. The
  package reads YAML and emits Python dictionaries; no writer of any format exists.
- **`Data Processing and Analysis: Data Access and Retrieval`** — the one network call
  (`CDFValidator.validate_raw`) *uploads* a local file to a validation endpoint and returns a text
  report. No data is queried, downloaded, or retrieved.
- **`Data Processing and Analysis: Analysis` / `Calibration` / `Data Reduction`** — no scientific
  computation of any kind appears in either module.
- **`Mission-related: Archive` and `Mission-related: Ingest`** — tempting because v1.1.0 added a NASA
  GES-DISC schema layer derived from that archive's "Data and Metadata Recommendations to Data
  Providers" document, plus an ACDD (Attribute Convention for Data Discovery) layer. Rejected: the
  package neither operates an archive nor ingests data into one. It only declares which attributes a
  provider must supply, which the values selected above already cover.
- **`Mission-related: System Testing`** — `CDFValidator` checks *data product* compliance, not the
  ground system.
- **`Servers and Environments: Data servers processing and handling`** — the package is a client of an
  external validation service, not a server.
- **`Coordinate Transforms`, `Data Visualization`, `Models and Simulations`** and all their children —
  no coordinate handling, no plotting (`matplotlib` is not a dependency at any extra), no physical
  model.

### 5. Related Region (MANDATORY)
Not found — deliberately empty.

This field is mandatory on the submission form, yet no value is defensible from the evidence, and
HSSI stores none. That was reviewed and accepted deliberately: the record stands with this field
unfilled rather than asserting a physical scope the software does not have.

Source note: the software has no region-specific functionality. Its behavior is identical regardless
of the physical domain the data describe: it merges YAML attribute schemas and checks ISTP compliance.
The bundled default schemas are the generic ISTP/CDF required-attribute set; the CF, ACDD, and
GES-DISC layers are cross-disciplinary metadata conventions (ACDD and CF originate in the
Earth-science and climate communities). Mission- and instrument-specific schema layers live in the
*consumer* packages — `imap_processing`'s `cdf/config/` directory and `swxsoc`'s schema module — not
in this package.

Alternatives considered and rejected:

- **Inheriting regions from the known downstream consumers** (IMAP → `Interplanetary Space`,
  `Solar Wind`, `Heliosheath`; HERMES/PADRE via `swxsoc` → `Earth Magnetosphere`,
  `Solar Environment`). Rejected: those are properties of the consuming pipelines, not of this
  software, and the resulting set would be broad enough to carry no information. A user filtering HSSI
  by `Solar Wind` would not expect a YAML metadata-schema library in the results.
- **Selecting a single broad region as a placeholder** (e.g. `Solar Environment` because the summary
  says "Space Weather"). Rejected as a guess: "space weather" names an application domain spanning Sun
  to Earth, not a physical region, and picking one row would assert something the code does not
  support.

The live `Region` vocabulary is a flat list of specific physical regions (`Chromosphere` … `Uranus
Magnetosphere`); it contains no "not applicable", "multiple", or "domain-independent" row, so there is
no correct value to select. The only way to fill the field would have been to populate the broad
inherited set considered above — `Interplanetary Space`, `Solar Wind`, `Earth Magnetosphere`,
`Solar Environment` — and that was weighed and rejected, because it would assert an applicability the
package does not have. Emptiness is the accurate statement here, so this is a documented omission and
not an unfinished field. If HSSI later requires a non-empty value for every record, the replacement
must come from an editorial choice made and recorded at that point, not from inferring regions from
downstream consumers: that inference has already been considered and rejected.

### 6. Authors (MANDATORY)

**Author 1: Maxine Hartnett**
- **Author Identifier:** `https://orcid.org/0009-0002-1495-5652`
- **Affiliation:** Laboratory for Atmospheric and Space Physics — `https://ror.org/01fcjzv38`

Source note: already an author on the HSSI record, but stored with an empty identifier and no
affiliation. Both are backfilled from primary sources: `.zenodo.json` in the repository gives the
ORCID `0009-0002-1495-5652` and the affiliation "Laboratory for Atmospheric and Space Physics", and
her ORCID record independently confirms both the name and a Laboratory for Atmospheric and Space
Physics employment carrying ROR `https://ror.org/01fcjzv38` (Boulder, US). She is also the PyHC
registry's listed contact for the project, published the v0.1.0, v0.1.1, and v1.0.0 GitHub releases
(v0.1.2 was published by Robbertz), and commits under
`maxinelasp`. The ROR matches the existing HSSI organization row for LASP, so this reuses that shared
row rather than creating a near-duplicate.

**Author 2: Andrew Robbertz**
- **Author Identifier:** `https://orcid.org/0009-0008-6857-0882`
- **Affiliation:**
  - General Dynamics Mission Systems (no identifier)
  - Goddard Space Flight Center — `https://ror.org/0171mag52`

Source note: already an author on the HSSI record with the ORCID stored, and the largest contributor
by volume of code at this revision — the initial commit, the CHANGELOG, the SPDF validation module,
and four of the seven GitHub releases (v0.1.2, v1.0.1, v1.0.2, v1.1.0). He leads on both measures at
this revision: 13 commits to Hartnett's 6, and +4624/-740 changed lines to her +1481/-280. His ORCID
record confirms the name; it
publishes **no employment entries at all**, so it cannot arbitrate affiliation (the whole record was
read, not just a disambiguation identifier — the employments section is simply empty, with no
department, city, or country to weigh).

The affiliation is recorded as the **union** of the two supported values rather than as a
replacement, because both are supported and they are not mutually exclusive:

- `General Dynamics Mission Systems` is the value already stored in HSSI. It is retained: General
  Dynamics Mission Systems is a NASA contractor, and a contractor employee working at Goddard is
  routinely credited under either name. There is no evidence it is wrong, so it is not removed.
- `Goddard Space Flight Center` (ROR `https://ror.org/0171mag52`) is added from `.zenodo.json`, which
  states "NASA Goddard Space Flight Center (GSFC)" for this author. The acronym is expanded per the
  field's "complete name without acronyms" instruction, and the expanded form plus ROR matches the
  existing HSSI organization row exactly, so the shared row is reused. His commit address in the
  sibling `swxsoc` project is `andrew.l.robbertz@nasa.gov`, consistent with a Goddard posting.

Two durable cautions for whoever maintains this:

- **HSSI Person and Organization rows are shared across software records.** Adding an affiliation to
  this author's Person row changes how he appears on every other HSSI entry that credits him. That is
  acceptable here because the addition is factual and additive, and because adding an affiliation
  whose ROR already matches an existing organization row is idempotent. Recording it as an addition
  rather than a replacement is also what the platform supports: an affiliation can be added to a
  Person row but cannot be swapped out, and an attempted replacement simply leaves the stored value
  in place. Removing `General Dynamics Mission Systems` would therefore take a deliberate, separately
  evidenced act — and it must not be attempted on the strength of `.zenodo.json` alone.
- **Do not attach a ROR to `General Dynamics Mission Systems`.** ROR has no record for the Mission
  Systems business unit; the closest match is `General Dynamics (United States)`
  (`https://ror.org/05pyq8e17`), which identifies the parent corporation and is a different entity.
  Leaving that affiliation's identifier empty is correct.

**Author 3: Sean Hoyt**
- **Author Identifier:** Not found
- **Affiliation:** Laboratory for Atmospheric and Space Physics — `https://ror.org/01fcjzv38`

Source note: a new author, not previously on the HSSI record, added because he wrote both headline
features of the pinned release. At this revision his commits are `4a59590` (PR #27, which added
`CdfAttributeManager.add_variable_attribute` and its tests) and `67104c7` (PR #28, which added all six
CF / ACDD / GES-DISC schema files, about a thousand lines of the shipped `sammi/data/` content). The
project credits him accordingly: he is listed as a creator on the Zenodo record for v1.1.0 with
affiliation "Laboratory for Atmospheric and Space Physics @ University of Colorado Boulder", and the
v1.1.0 GitHub release notes name him as a new contributor. His commit address is
`sean.hoyt@lasp.colorado.edu`, which corroborates the LASP affiliation independently.

No ORCID is recorded because none could be found: an ORCID search on the exact given/family name pair
returned no result, and a broad search on the family name surfaced no Sean Hoyt. The identifier is
recommended, not required, so the author is recorded without one rather than omitted or matched to a
same-surname stranger.

The affiliation is recorded as `Laboratory for Atmospheric and Space Physics` only. The Zenodo string
also names the University of Colorado Boulder, but that fragment is the GitHub-profile style suffix
for LASP's parent university; LASP's own ROR already resolves within CU Boulder, and the employer
named by both the deposit and his email address is LASP. `University of Colorado Boulder`
(`https://ror.org/02ttsq026`, an existing HSSI organization row) was therefore considered and not
selected, because adding it would assert a second, separate institutional affiliation that the
sources do not distinguish.

**Deliberate omissions (do not add these as authors):**

- **`pleasant-menlo`** — appears as a creator on the Zenodo records for v1.0.2 and v1.1.0 and has one
  commit at this revision (`d1c2a290`, PR #23, "Fix encoding issues on Windows"). Omitted because the
  sources give only an un-deanonymized GitHub handle: no given name, family name, ORCID, or
  affiliation appears in any source checked (repository files, the Zenodo deposits, and the commit
  author line). HSSI Person rows are keyed on a person's name and are shared between records; minting
  one from a handle would create a row nobody could later reconcile or merge. If the contributor's
  identity is published upstream, adding them is the correct follow-up — the contribution itself is
  real.
- **`IMAP SDC Developers`** — the second entry in `pyproject.toml`'s `authors` list, with the mailing
  address `imap.sdc@lists.lasp.colorado.edu`. Omitted as a person, and also considered and rejected
  as an *organization* author (HSSI supports organization authors via a ROR identifier): "IMAP SDC
  Developers" is a team mailing-list label, not an institution, and has no ROR. The institution behind
  the IMAP Science Operations Center is LASP (`https://ror.org/01fcjzv38`), already represented
  through the affiliations of Authors 1 and 3; recording LASP itself as an author would attribute the
  whole package to the institute rather than to its named authors.

**Why the author set is these three rather than the Zenodo creator list.** The Zenodo creator lists
carry no ORCIDs and include the raw handle and the junk affiliation string `@lasp`, whereas
`.zenodo.json` in the repository carries clean names, ORCIDs, and full affiliations for two authors.
The explanation is a defect in `.zenodo.json`: it declares its author array under the key
`"authors"`, but Zenodo's metadata schema expects `"creators"`. Zenodo therefore ignores that array
and falls back to deriving creators from the GitHub contributor list, which is why the deposits show
four creators with no identifiers and profile-style affiliations. This is a durable upstream
limitation, useful in two directions: `.zenodo.json` is the maintainers' authoritative statement of
author identity even though it is not what the deposits show, and future Zenodo deposits will keep
producing the handle-and-`@lasp` creator list until the key is renamed upstream.

### 7. Software Name (MANDATORY)
`sammi-cdf`

Source note: this is the name already stored in HSSI, kept deliberately. Three names circulate for
this project and each is correct in its own context:

- `sammi-cdf` — the PyPI distribution name (`pyproject.toml` `[project] name`), the title of every
  Zenodo deposit and of the DataCite record, and the ReadTheDocs project slug
  (`sammi-cdf.readthedocs.io`). This is the name a user types to install or to cite the software.
- `sammi` — the GitHub repository name and the importable Python package name.
- `SAMMI` — the expanded project name, "Shared Attribute and Metadata Management Interface", used in
  `README.rst`, throughout the documentation, and by the PyHC registry entry (which lists the project
  as `SAMMI`).

`sammi-cdf` is kept because it is the citable title in the DOI metadata and the installable
distribution name, and because it is the submitted value; renaming to `SAMMI` or `sammi` for
stylistic consistency with the repository or the registry would change how the record is cited
without improving its accuracy. The expanded form and the acronym both appear in the Description
(Field 8), so a search for either still reaches this record. The GitHub repository description,
"Shared Attribute and Metadata Management Interface for CDF Files", explains the `-cdf` suffix: it
distinguishes the distribution on PyPI while naming the file format the schemas target.

### 8. Description (MANDATORY)
A Python package to support metadata attribute management for Space Weather data processing
pipelines. SAMMI (Shared Attribute and Metadata Management Interface) represents metadata
requirements as layered YAML schemas: its `CdfAttributeManager` loads and merges global (file-level)
and variable (measurement-level) schema layers in latest-priority order, then generates validated
dictionaries of global and variable attributes that a pipeline embeds in its CDF data products. The
bundled default schemas cover the attributes required for ISTP compliance, with additional layers for
the CF, ACDD, and NASA GES-DISC metadata conventions; a mission extends or overrides them by adding
its own layers rather than by editing the package. SAMMI also generates templates of the required
attributes and per-attribute documentation, and its `CDFValidator` submits an existing CDF file to
the SPDF ISTP validation service and returns the parsed list of compliance errors. Because SAMMI
manages metadata only — writing the data file itself is left to the pipeline's CDF library — it can
be adopted incrementally by any pipeline that produces CDF products. SAMMI is a SWxSOC project and
can be used together with other SWxSOC packages or standalone; it is used in production by the SWxSOC
core package and by the IMAP Science Operations Center's processing pipeline.

Source note: the stored HSSI description was a single sentence identical to the stored concise
description — the summary line from `pyproject.toml` and `.zenodo.json`. That sentence is the
maintainers' own wording and is preserved: it opens this description unchanged, and it remains the
whole of Field 9, so the record's preview text is untouched. The expansion is an enrichment of a
materially incomplete field rather than a rewrite of editorial intent: the field asks for enough
detail for a potential user to judge usefulness, and one sentence naming neither the schema-layering
model, the supported conventions, the validator, nor the YAML input could not do that. Every added
claim comes from the pinned revision — `sammi/cdf_attribute_manager.py`, `sammi/validation.py`, the
eight schema files in `sammi/data/`, `docs/user-guide/cdf_attribute_management.rst`, and
`docs/user-guide/cdf_validation.rst` — plus `README.rst` for the SWxSOC relationship and the declared
dependencies of `swxsoc` and `imap_processing` for the production-use claim. The sentence about
managing metadata only is deliberate: it is the most likely misreading of this package, and it tells
a prospective user what they still have to supply themselves.

### 9. Concise Description (OPTIONAL)
A Python package to support metadata attribute management for Space Weather data processing pipelines.

Source note: this is the maintainers' own summary line, used identically in
`pyproject.toml` `[project] description`, `.zenodo.json`, the PyPI summary, and the DataCite abstract,
and it is the text already stored in HSSI for both the description and the concise description. At
102 characters it is within the 200-character limit and it previews the software well, so it is kept
as the preview while Field 8 carries the fuller text. A stylistic rewrite here would change the
record's visible summary for no gain.

### 10. Publication Date (RECOMMENDED)
`2024-10-08`

Source note: **this replaces the stored value `2025-06-03`, which was incorrect.** The field is the
date of first publication, used for the *initial* version of the software.

Why 2024-10-08 wins: it is the date the software was first published as a release, and three
independent artifacts agree on it. The first git tag `v0.1.0` was created that day; the GitHub release
`v0.1.0` ("Initial release for SAMMI") was published at 2024-10-08T16:36:35Z; and the first artifact
ever uploaded to PyPI, `sammi-cdf 0.1.0.dev0`, was uploaded at 2024-10-08T16:53:05Z. Before that date
there was no tag, no release, and nothing installable.

Why each alternative loses:

- **`2025-06-03` (previously stored)** — this is exactly the `v1.0.2` release date (tag, GitHub
  release, and PyPI upload all on that day). It is a *current-version* date recorded in a
  first-publication field, which is the classic failure mode for this field. It is also demonstrably
  not the first publication: five earlier tagged releases and four earlier PyPI uploads precede it.
- **`2023-03-22`** — asserted by `CHANGELOG.rst`, whose oldest block reads `0.0.0 (2023-03-22)` /
  "Initial project release". This date is fiction for this project, and its origin is now known: it is
  the release date of **version 0.2.0 of `hermes_core`**, the HERMES partner package, whose own
  `CHANGELOG.rst` carries the heading `0.2.0 (2023-03-22)`. This project's CHANGELOG was created in
  commit `e71c48f` (2024-06-05) already containing both that stub block and the line "Added
  Functionality from HERMES partner package", so the block is inherited partner-package text. It
  predates this repository's own first commit (2024-06-04), and no tag, GitHub release, PyPI artifact,
  or Zenodo deposit exists anywhere near it. **This is an upstream documentation defect that has never
  been corrected**; a future agent reading `CHANGELOG.rst` in isolation will be misled by it again.
- **`2024-06-04`** — the GitHub repository `created_at` and the first commit (`d3b18e32`, "Initial
  commit", 2024-06-04T12:27:43Z; the two timestamps are the same instant). Rejected because creating
  a source repository is not publishing a version: this field is explicitly for the initial version,
  and no version existed for another four months.
- **`2025-02-18`** — the earliest Zenodo deposit (`10.5281/zenodo.14887801`, v1.0.1), which is also
  the date cited in `docs/acknowledging.rst` ("Zenodo, Feb. 18, 2025"). This is the first *DOI*
  publication, not the first publication of the software: the Zenodo–GitHub integration was switched
  on only at v1.0.1, so Zenodo holds three version records (v1.0.1, v1.0.2, v1.1.0) and none for the
  six-month v0.1.x/v1.0.0 history that PyPI and GitHub both retain. Nothing on Zenodo predates it.

One artifact-level wrinkle, recorded so it is not mistaken later for an error: PyPI has no plain
`0.1.0` (its first upload is `0.1.0.dev0`) and no `1.0.1` at all, while git and GitHub have tags and
releases for both. The 2024-10-08 date is unaffected — the tag, the GitHub release, and the first PyPI
upload all fall on it.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

Source note: this is the value stored in HSSI, and it is correct per the field's guidance that Zenodo
is the right publisher where the DOI was obtained through the GitHub–Zenodo workflow. DataCite
independently reports `publisher: "Zenodo"` for the concept DOI. Zenodo has no ROR, so the
organization URL is the appropriate identifier.

### 12. Version (RECOMMENDED)
- **Version Number:** `v1.1.0`
- **Version Date:** `2026-06-25`
- **Version Description:** Adds global and variable schema layers for the GES-DISC, CF, and ACDD
  metadata conventions alongside the existing ISTP/CDF defaults, and adds
  `CdfAttributeManager.add_variable_attribute` for setting variable attributes dynamically.
- **Version PID:** `https://doi.org/10.5281/zenodo.20858467`

Source note: this advances the record from the stored `v1.0.2` to the current release. The pinned
source revision `9d2b8975114aab2bef55072a8a75e1590e4570e5` *is* the `v1.1.0` tag.

**Notation — `v1.1.0`, with the leading `v`.** The project's own notation carries the prefix: the git
tag is `v1.1.0`, the GitHub release name is `v1.1.0`, and the Zenodo record's `version` metadata field
is the string `"v1.1.0"` (DataCite echoes the same). PyPI shows `1.1.0` because PEP 440 normalization
strips the prefix when an index registers a distribution — an index-side transformation, not the
project's notation. The prefixed form is also consistent with the value HSSI already stored (`v1.0.2`)
and with this field's own example (`v1.0.0`), so keeping it avoids a cosmetic change of notation on
top of a substantive version bump. **When comparing against HSSI, note that the view layer renders
this field as `sammi-cdf - v1.1.0`; the stored value is the bare version string, and the rendered
prefix must never be copied into a stored value.**

**Date.** Four sources agree on 2026-06-25: the tag's commit `9d2b897` (2026-06-25 15:06:53 -0400 =
19:06:53Z), the GitHub release published at 19:07:45Z, the Zenodo record's `publication_date`, and the
PyPI upload at 19:08:27Z.

**Description.** Taken from the two genuine 1.1.0 entries in `CHANGELOG.rst`, cross-checked against
the release's pull requests (#27 `add_variable_attribute`, #28 the CF/ACDD/GES-DISC schema files) and
against the shipped files in `sammi/data/`. The CHANGELOG's third bullet under the 1.1.0 heading,
"Added Functionality from HERMES partner package", is **not** a 1.1.0 change and is deliberately
excluded: it was the sole bullet under "Latest" from the first CHANGELOG commit in June 2024, and the
1.1.0 commit inserted the new heading above it, leaving the old line stranded inside the new section.
A future agent regenerating this description from `CHANGELOG.rst` alone would reintroduce that error.

**Version PID.** `10.5281/zenodo.20858467` is the version DOI for v1.1.0; the concept DOI stays in
Field 2. For reference, the other two version DOIs are `10.5281/zenodo.15587327` (v1.0.2) and
`10.5281/zenodo.14887801` (v1.0.1).

Release history at this revision, for later drift checks: v0.1.0 2024-10-08, v0.1.1 2024-10-09,
v0.1.2 2024-10-10, v1.0.0 2025-01-14 (tag; GitHub release 2025-01-17), v1.0.1 2025-02-18,
v1.0.2 2025-06-03, v1.1.0 2026-06-25.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

Source note: the value already stored in HSSI, confirmed at this revision. The repository is
entirely Python by GitHub's language statistics; `pyproject.toml` sets `requires-python = ">=3.9"`;
the test workflow matrix runs Python 3.9, 3.10, 3.11, 3.12, and 3.13. There are no compiled
extensions — `MANIFEST.in` includes patterns for `*.pyx`, `*.c`, and `*.pxd`, but no such files
exist at this revision (that stanza is inherited from the OpenAstronomy/SunPy package template
acknowledged in `README.rst`). No second language row applies.

### 14. Reference Publication (RECOMMENDED)
Not found.

Source note: no publication describing this software was found, and the project states that none
exists. `sammi/CITATION.rst` reads: "The software citation should be the specific Zenodo DOI for the
version used in your work. A paper citation does not yet exist." Corroborating negative research:
the DataCite record for the concept DOI lists no `IsDescribedBy` related identifier (only
`IsSupplementTo` the GitHub tree and `IsVersionOf` the concept DOI); `README.rst` and
`docs/acknowledging.rst` direct citers to the Zenodo DOI; there is no JOSS paper, no publication
badge, and no `CITATION.cff`.

Deliberately **not** promoted into this field: the Zenodo software DOI (that is the software's own
identifier, already in Field 2, not a publication describing it) and the two 2024 AGU conference
posters listed in `docs/acknowledging.rst` (recorded under Field 27, where developer-prioritized
related outputs belong; neither is a peer-reviewed paper describing the software, and promoting a
poster here would misrepresent the project's own stated citation guidance). If a paper is later
published, this field is the place for it.

### 15. License (RECOMMENDED)
- **License:** `Apache License 2.0`
- **License URI:** `https://spdx.org/licenses/Apache-2.0`

Source note: HSSI stored no license, and the repository makes two genuinely different licensing
statements, so the reasoning is recorded in full rather than summarized. The reading below was
reviewed and confirmed, and `Apache License 2.0` is the settled value; the conflict is documented
here rather than left open.

**What the sources say.**

- `licenses/LICENSE.md` contains the complete, unmodified Apache License 2.0 text (201 lines, with the
  boilerplate appendix still reading `Copyright [yyyy] [name of copyright owner]` — the project never
  filled in a copyright holder). This is the only license text in the repository, and `MANIFEST.in`'s
  `recursive-include licenses *` puts it in the distributed sdist.
- `LICENSE.rst`, the file `pyproject.toml` points at via `license = {file = "LICENSE.rst"}`, contains
  only the string `see licenses/LICENSE.md`. Consequences: PyPI's metadata `license` field for every
  release literally reads "see licenses/LICENSE.md" with no SPDX expression, and GitHub's license
  detector reports `NOASSERTION` / "Other" for the repository.
- `.zenodo.json` declares `"license": "Apache-2.0"`, and all three Zenodo version records carry
  `license: {id: apache2.0}`. DataCite renders this as `rights: "Apache License 2.0"`,
  `rightsIdentifier: apache-2.0`, scheme SPDX, `rightsUri: http://www.apache.org/licenses/LICENSE-2.0`.
- `README.rst` has a "Public Domain" section asserting that the project "constitutes a work of the
  United States Government and is not subject to domestic copyright protection under 17 USC § 105",
  waiving copyright worldwide through the **CC0 1.0 Universal** dedication, and stating that all
  contributions are released under CC0.

**Why `Apache License 2.0` is recorded.** Four reasons, in order of weight:

1. It is the only actual set of license terms shipped with the distributed software. A user who
   installs `sammi-cdf` receives the Apache-2.0 text and no other license terms.
2. It is what the project machine-declares in its own repository metadata. `.zenodo.json` is in-repo,
   maintainer-authored, and effective — unlike its author array, its license key *is* honored, which
   is why all three Zenodo deposits and the DataCite record say Apache-2.0.
3. The README's "Public Domain" paragraph is SWxSOC-wide README template text, not a sammi-specific
   grant. The same paragraph — same § 105 sentence, same CC0 link, same "All contributions to this
   project will be released under the CC0 dedication" follow-up — appears character-for-character in
   the READMEs of the sibling packages `swxsoc` and `hermes_core`, and both of those repositories also
   ship an Apache-2.0 `licenses/LICENSE.md` behind the same one-line `LICENSE.rst` pointer stub. The
   paragraph travels with the template rather than describing any one package's terms.
4. Its § 105 premise does not hold for this repository's actual authorship. Two of the three authors
   recorded in Field 6 are LASP / University of Colorado people rather than federal employees, so
   their contributions are copyrightable and a blanket "work of the United States Government" claim
   cannot be accurate for the codebase as a whole. That further marks the paragraph as inherited
   boilerplate.

**What was rejected, and why.**

- **CC0 1.0 as the license value** — not selectable in any case: the live HSSI `License` vocabulary
  offers only these values (`Apache License 2.0`, `BSD 2-Clause "Simplified" License`,
  `BSD 3-Clause "New" or "Revised" License`, `Creative Commons Attribution 4.0 International`,
  `GNU General Public Licenses (GPL version 2)`, `GNU General Public License v3.0 or later`,
  `GNU Lesser General Public License v3.0 only`,
  `GNU Library or ‘Lesser’ General Public Licenses (LGPL version 2)`, `MIT License`, `Other`,
  `Restricted`) and none of them is CC0 or any other public-domain dedication. So even under a CC0
  reading, the only representable choice would be `Other`.
- **`Other`** — considered as a way to encode "ambiguous", and rejected: it would discard the
  strongest, most specific, machine-declared evidence (the shipped Apache-2.0 text and the SPDX
  identifier in every DOI record) in favor of a value that tells a user nothing about their rights.
- **Blending or recording both** — not done. The two statements are not combined, and the CC0
  dedication is not asserted as a second license value. Apache-2.0 is recorded as the terms under
  which the software is distributed; the README's public-domain dedication is preserved here as
  context a user may additionally rely on.
- **GitHub's `NOASSERTION`** — not evidence of different terms. It is a detection failure caused by
  the `LICENSE.rst` pointer stub; GitHub cannot follow a one-line file to `licenses/LICENSE.md`.

**Durable upstream follow-up:** the `LICENSE.rst` pointer stub is the root cause of both the
`NOASSERTION` detection and the nonsense PyPI license string, and it has been unchanged since the
first commit that created it (`e71c48f`, 2024-06-05). If upstream ever replaces the stub with real
license text or an SPDX expression, this field should be re-derived rather than assumed stable — and
if that text turns out to be CC0, this decision must be revisited.

**License URI:** the SPDX page for Apache-2.0 is recorded because this field is described as
auto-populated for SPDX licenses. DataCite's `rightsUri` for the same license is
`http://www.apache.org/licenses/LICENSE-2.0`; either identifies the same terms, and the HSSI `License`
row's own URL takes precedence if it differs.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- space weather
- cdf
- istp
- metadata
- validation
- yaml
- sammi
- swxsoc
- nasa mission
- heliophysics
- data processing
- acdd
- cf conventions
- gesdisc

Source note: HSSI stored one keyword, `space weather` (stored lower-case, rendered Title Case in the
view — the same term, not drift). This list is the union of that value with the maintainers' declared
keywords and terms the code supports; nothing is removed.

Provenance for each: `space weather` — stored in HSSI, and declared in both `pyproject.toml`
`keywords` and `.zenodo.json`. `sammi` and `nasa mission` — declared in `pyproject.toml` `keywords`
(`sammi` also in `.zenodo.json`). `cdf` — the subject of the whole package; the PyHC registry entry
also lists `cdf`. `istp` — the default schemas encode the ISTP required-attribute set and
`CDFValidator` checks ISTP compliance. `metadata` — the package's function, and part of its expanded
name. `validation` — `sammi/validation.py` and the `cdf_validation` user guide. `yaml` — every schema
and attribute file is YAML, as the PyHC description says ("Manage attributes for ISTP CDF files using
YAML"). `swxsoc` — `README.rst` states the package is a SWxSOC project. `heliophysics` and
`data processing` — the domain and the role stated in the summary line.

`acdd`, `cf conventions`, and `gesdisc` — the three metadata-convention layers added in v1.1.0, each
shipped as a global and a variable schema in `sammi/data/`. These name the conventions the package
encodes, which is what a user searching by convention would look for; they are deliberately *not*
claims of netCDF file support (see Fields 18 and 19, where `netCDF3/4` is rejected on code evidence).

Of the values listed, `yaml`, `sammi`, `acdd`, `cf conventions`, and `gesdisc` are intentional new
rows in this open vocabulary; the remainder already exist as rows in the live keyword vocabulary and
are spelled to match those rows exactly. Adding new rows is consistent with the existing format
keywords (`json`, `xml`, `netcdf`, `hdf5`) and project-name keywords (`swxsoc`, `pysat`). `cf
conventions` is spelled out rather than as a bare `cf` because a two-letter row would be ambiguous in
a shared vocabulary, and `gesdisc` follows the unpunctuated form the schema filenames use
(`default_global_gesdisc_attrs_schema.yaml`).

Considered and rejected: `data access` — the PyHC registry lists a `data_access` facet for this
project, but the package retrieves no data (its one network call uploads a local file for validation),
so carrying that facet over would assert a capability the code lacks; the facet is a site-navigation
category rather than a claim about the API. `python` — the language belongs to Field 13, and adding it
here duplicates a field. `common data format` and `nasa cdf` — near-duplicates of `cdf` that would
fragment the vocabulary. `hermes`, `imap`, `padre` — mission names would imply mission-specific
support this package does not have (see Fields 31–32). `general` — the PyHC facet carries no
information.

### 17. Data Sources (OPTIONAL)
- Other

Source note: this is the value stored in HSSI, and it is correct. The package's inputs are local files
supplied by the caller — YAML schema and attribute files, and a CDF file path handed to
`CDFValidator` — not any hosted archive or data service. None of the specific rows in the live
`DataInput` vocabulary (`AMDA`, `CDAWeb`, `das2`, `FTP/FTPS Directories`, `GFZ`, `HAPI`,
`HTTP/HTTPS Directories`, `Madrigal`, `OMNIWeb`, `Observatory/Mission-specific`, `S3/Cloud-aware`,
`SSCWeb`, `TAP`, `The Virtual Solar Observatory.`, `VirES`, `WDC`) describes that, so `Other` is the
right value for local-file input.

Considered and rejected: `Observatory/Mission-specific` — the field's instructions tie this value to
naming the observatory in Field 32, and Fields 31–32 are correctly empty here, so selecting it would
create a dangling claim. `HTTP/HTTPS Directories` — the one HTTPS call in the package is an *upload*
to the SPDF ISTP validation endpoint (`https://skteditor.heliophysics.net/cgi-bin/checkcdf.cgi`),
which is a validation service rather than a data source; it is described in Field 8 instead.

### 18. Input File Formats (RECOMMENDED)
- CDF
- ISTP-Compliant
- Other

Source note: `CDF` and `ISTP-Compliant` were already stored and are retained with direct code
evidence — `CDFValidator.validate_raw()` opens a caller-supplied `.cdf` file in binary mode and
submits it for ISTP compliance checking, and the repository ships real CDF fixtures
(`sammi/tests/test_data/test_valid.cdf`, `test_invalid.cdf`) exercised by
`sammi/tests/test_validation.py`. Note precisely what this does and does not mean: the package accepts
CDF files as input but does not parse CDF internally — it has no CDF library dependency at any extra,
and the byte-level interpretation happens in the remote SPDF service.

`Other` is added for **YAML**, the package's primary input format, which had no representation in the
record. Every schema layer and every attribute file is YAML: the eight schema files in `sammi/data/`,
the fixtures in `sammi/tests/test_data/`, and everything `load_global_attributes()`,
`load_variable_attributes()`, and `_load_yaml_data()` consume via `yaml.safe_load`. `pyyaml` is the
package's only declared runtime dependency. The live `FileFormat` vocabulary has no `YAML` row and
`Other` is its catch-all, so `Other` records the fact with the explanation kept here. Leaving it out
would have left the record silent about the format the software actually reads.

Considered and rejected: `netCDF3/4` — see the reasoning under Field 19; it applies to input as well.
`ascii` — YAML is text, but this row denotes plain-text/tabular data files, and using it for a
structured configuration format would misdescribe both. `JSON` — the package neither reads nor writes
JSON (`.zenodo.json` is repository metadata, not an input the code parses).

### 19. Output File Formats (RECOMMENDED)
- CDF
- ISTP-Compliant

Source note: both values were already stored and are retained, with the scope stated precisely because
the literal reading is narrower than the values suggest. **The package writes no files.**
`CdfAttributeManager` returns Python dictionaries (`get_global_attributes()`,
`get_variable_attributes()`, the `*_template()` and `*_info()` methods) and `CDFValidator` returns a
list of error strings; no method in either module opens a file for writing. What the package produces
is the ISTP-compliant global and variable attribute set that a consuming pipeline embeds in its CDF
products — which is the package's stated purpose ("Manage attributes for ISTP CDF files") and how its
consumers use it (`imap_processing` via the `ImapCdfAttributes` subclass, `swxsoc` via its `cdf`
extra). On that reading the two stored values describe the output the package is designed to produce,
and they make the record findable for exactly the users who need it, so they are kept rather than
cleared. A future curator who prefers the strict "files written by this code" reading has the facts
here to make that call deliberately.

**`netCDF3/4` is deliberately NOT selected, in either Field 18 or Field 19.** This is the most likely
wrong enrichment for this record, so the reasoning is recorded: v1.1.0 added CF and ACDD schema
layers, the pull request that added them is titled "NetCDF CF Global and Data Variable Schema", and CF
and ACDD are conventions most often applied to netCDF files. But those layers are *metadata-attribute
definitions* — YAML dictionaries of attribute names, descriptions, defaults, and required flags,
sourced from the CF conventions appendix, the ESIP ACDD wiki, and the NASA GES-DISC recommendations
document. Nothing in the package reads or writes netCDF: there is no `netCDF4`, `h5netcdf`, `xarray`,
or `scipy.io` dependency at any extra, no `.nc` fixture, and no netCDF code path. Supporting a
metadata standard associated with a format is not supporting the format. Do not add this value unless
a netCDF reader or writer appears in the code.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

Source note: HSSI stored none. The testing workflow (`.github/workflows/testing.yml`) runs the full
test suite on `ubuntu-latest`, `macos-latest`, and `windows-latest` across Python 3.9–3.13 on every
push, every pull request, and a daily schedule, so all three platforms are continuously verified
rather than merely claimed. Windows support is specifically maintained: pull request #23 ("Fix
encoding issues on Windows") exists precisely because the Windows job caught a defect.

`Operating System Independent` was considered — `pyproject.toml` declares the classifier
`Operating System :: OS Independent`, and the package is pure Python with one pure-Python dependency,
so the claim is credible. It was not selected because the three concrete rows say more for a user
filtering by platform and are backed by passing CI on each, whereas the broader row would replace
verified facts with a general assertion. (Note also that `OS Independent`, the classifier's own
spelling, is not a value in the HSSI vocabulary; the only cross-platform row is
`Operating System Independent`, spelled out in full.)

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Source note: HSSI stored none. The package is pure Python with no compiled extension modules at this
revision and one pure-Python runtime dependency (`pyyaml`); nothing in it is architecture-sensitive.

`x86-64` and `Apple Silicon arm64` were considered, since the CI runners cover both (the Linux and
Windows runners are x86-64 and `macos-latest` is Apple Silicon). They were not selected because
`CPU Independent` is the accurate description of a pure-Python package and subsumes them; listing
specific architectures would wrongly imply that unlisted architectures are unsupported.

### 22. Related Phenomena (OPTIONAL)
Not found — correctly empty.

Source note: the live `Phenomena` vocabulary is a flat, closed list of seven specific physical
phenomena — `Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`,
`Solar Flares`, `Solar Wind`, `X-ray emission`. This package supports none of them: it performs no
physical computation, detects no events, and its behavior does not depend on what the data describe.
There is no row for a domain-independent or metadata-only tool, and this vocabulary rejects values
that are not rows, so the field is correctly left empty rather than filled with the nearest
phenomenon. The same reasoning as Field 5 applies — a phenomenon studied by a downstream mission that
happens to use this library is a property of that mission, not of this software.

### 23. Development Status (RECOMMENDED)
`Active`

Source note: HSSI stored none. `Active` in the repostatus.org sense — "reached stable, usable state
and being actively developed" — is supported on both halves:

- *Stable and usable*: seven releases since October 2024 through the 1.x series, a published API with
  a user guide, CI on three platforms and five Python versions, and production use as a declared
  runtime dependency of `imap_processing` (`sammi-cdf>=1.0,<2`) and of `swxsoc`'s `cdf` extra. The
  PyHC registry rates the project "Good" on community, documentation, testing, software maturity,
  Python 3, and license.
- *Actively developed*: v1.1.0 was released 2026-06-25, roughly six weeks before this extraction,
  adding both a new API method and six new schema files; the repository has open issues; the test and
  docs workflows run on a daily schedule.

Considered and rejected: `WIP` — `pyproject.toml` still declares the classifier
`Development Status :: 3 - Alpha`, which maps closest to `WIP`. That classifier has been unchanged
since the package was created and was not revised through the 1.x releases; it is contradicted by the
tagged 1.x line, the semantic-versioning policy stated at the top of `CHANGELOG.rst`, and downstream
production use with a `>=1.0,<2` pin. Treat the Alpha classifier as stale metadata rather than as the
project's assessment. `Inactive` and `Unsupported` are ruled out by the 2026 release.

### 24. Documentation (RECOMMENDED)
`https://sammi-cdf.readthedocs.io`

Source note: this is the URL already stored in HSSI. `README.rst` names it, `.readthedocs.yml`
configures the Sphinx build for it, and the ReadTheDocs badge targets it. The site includes the
installation guide (`docs/user-guide/install_guide.rst`) as this field asks. The PyHC registry lists
the same URL with a trailing slash; the stored form resolves identically and is kept rather than
churned.

### 25. Funder (OPTIONAL)
Not found.

Source note: no funding organization is named in any source checked — `README.rst`,
`docs/acknowledging.rst`, `sammi/CITATION.rst`, `pyproject.toml`, `.zenodo.json`, the DataCite record
(`fundingReferences` is an empty list), and the Zenodo records (which include no `grants` field). The
"Acknowledgements" section of `README.rst` credits the OpenAstronomy and SunPy package templates,
which is software provenance rather than funding.

Two things deliberately not turned into a funder value: the README's assertion that the project is a
work of the United States Government implies federal sponsorship but names no funding organization,
and the authors' affiliations (Goddard Space Flight Center, LASP) identify employers, not funders.
Recording `National Aeronautics and Space Administration` on that basis would be an inference, not a
finding. If a funding statement or award appears upstream, this field and Field 26 should be filled
together.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

Source note: no grant or contract identifier appears in any source checked (the same set as Field 25);
DataCite's `fundingReferences` is empty and the Zenodo records list no grants.

### 27. Related Publications (OPTIONAL)
- `https://doi.org/10.5281/zenodo.14503065` — Hartnett, M. (2024). *Increasing Open Source
  Collaboration for Better Scientific Code* [Poster]. American Geophysical Union Annual Meeting,
  9–13 December 2024, Washington, DC. Zenodo.
  Zenodo's own `conference.dates` field self-reports 8–13 December, while AGU's official schedule
  gives 9–13 December; the official dates are therefore retained here.
- `https://doi.org/10.5281/zenodo.14606063` — Robbertz, A., Rager, A., Barrous-Dume, D., Christe, S.,
  Kreisler, S., Mercer, T., & Paterson, W. R. (2024). *SWxSOC Software Architecture for Science Data
  Processing* [Poster]. Zenodo.

Both entries are kept, and the poster-versus-paper question behind them was weighed rather than
overlooked. Neither item is a peer-reviewed paper — both carry `resource_type: poster` on Zenodo —
but this field asks for publications the developers prioritize that describe, cite, or use the
software, and its definition does not exclude conference presentations. One of the two describes SAMMI's
development directly, so reading "publications" strictly as peer-reviewed literature would drop the
most on-point item in the record. That trade-off was reviewed and settled in favor of keeping both;
the poster caveat is recorded here so a later reader can see what these items are rather than assume
journal literature.

Source note: HSSI stored none. Both DOIs come from `docs/acknowledging.rst`, whose "Other SAMMI
publications" section introduces them as "also relevant to `sammi`" and "show[ing] information about
its development, use, and capabilities" — i.e. the project itself prioritizes them, which is what this
field asks for ("publications that describe, cite, or use the software that the software developer
prioritizes but are different from the reference publication").

Both were verified against Zenodo rather than taken from the docs page alone. `10.5281/zenodo.14503065`
is a poster whose own abstract reads "This poster describes the development of SAMMI (Shared Attribute
and Metadata Management Interface) in an open source and collaborative fashion" — it describes this
software directly. `10.5281/zenodo.14606063` is a poster on the SWxSOC package-library architecture in
which this package sits. Both carry `resource_type: poster`, so they are conference presentations
rather than papers; that is why Field 14 (Reference Publication) remains empty and neither DOI was
promoted there.

Deliberately excluded: the Zenodo software DOIs (concept and version), which identify the software
itself and live in Fields 2 and 12; the ReadTheDocs pages and the acknowledging page itself, which are
documentation recorded in Field 24; and the SWxSOC code-of-conduct and package-template
acknowledgements. No journal article, JOSS paper, or preprint about this software was found.

### 28. Related Datasets (OPTIONAL)
Not found.

Source note: the package ships no data products and references no dataset DOI. The DataCite record
lists no related identifier with a Dataset resource type. The `.cdf` files under
`sammi/tests/test_data/` are synthetic fixtures for the validator tests (one deliberately
ISTP-invalid), not published datasets, and the `imap_*.yaml` files there are attribute fixtures rather
than data. The package is dataset-agnostic by design: it describes metadata requirements, and the
products it helps produce belong to the consuming missions.

---

## Section 3: Additional Metadata

### 29. Related Software (OPTIONAL)
- `https://github.com/IMAP-Science-Operations-Center/imap_processing`
- `https://github.com/HERMES-SOC/hermes_core`

Source note: HSSI stored none. Both entries are lineage, which is what this field is for ("software
this work was forked from" and predecessors); neither is a generic dependency.

- **`imap_processing`** (IMAP Science Operations Center, Levels 0–2 science processing) is the origin
  of this package's central class. The evidence is concrete rather than inferential: `pyproject.toml`
  credits `IMAP SDC Developers <imap.sdc@lists.lasp.colorado.edu>` as one of the package's two
  authors; the attribute fixtures shipped in `sammi/tests/test_data/` are IMAP files by name and
  content (`imap_test_global.yaml`, `imap_instrument1_global_cdf_attrs.yaml`, and the
  `imap_instrument2_*` siblings), and `imap_processing` carries files of those same names in its own
  `tests/cdf/test_data/` tree. Compared against `imap_processing`'s `dev` branch,
  `imap_test_global.yaml`, both `imap_instrument1_*` files, and
  `imap_instrument2_level2_variable_attrs.yaml` are byte-for-byte the same, while
  `imap_test_variable.yaml` and `imap_instrument2_global_cdf_attrs.yaml` differ only by small
  sammi-side additions (a `test_field_4` entry with a non-ASCII `CATDESC`, and two `Data_level: 1A`
  lines) — shared ancestry with local divergence, not coincidence of naming. This package's
  `imap_default_global_cdf_attrs.yaml` is a near-namesake rather than an exact match; the
  `imap_processing` counterpart is `imap_default_global_test_cdf_attrs.yaml`. And
  `docs/user-guide/cdf_attribute_management.rst` teaches the schema format by linking to
  `imap_processing`'s configuration YAMLs as the canonical examples. It is listed again under Field 30
  for a separate, present-day reason (it consumes this package today); the two entries record
  different relationships and both are informative.
- **`hermes_core`** (HERMES Science Operations Center core package) is the partner package the
  functionality was taken from, per the project's own CHANGELOG line "Added Functionality from HERMES
  partner package", present since the CHANGELOG was created in `e71c48f` (2024-06-05). Two further
  ties confirm the identification: the stub release date in this package's CHANGELOG,
  `0.0.0 (2023-03-22)`, is the date of `hermes_core`'s own `0.2.0 (2023-03-22)` release (see
  Field 10), and `hermes_core` carries the same README public-domain boilerplate and the same
  `LICENSE.rst` → `licenses/LICENSE.md` arrangement (see Field 15). `hermes_core` was subsequently
  generalized into `swxsoc`; its repository is still public, last pushed January 2025.

Excluded, with reasons, so they are not added later:

- **`pyyaml`** — the only declared runtime dependency, and generic infrastructure: a serialization
  library equally at home in a web application or a build system. Being a dependency is not being
  related software.
- **`requests`** — used by `sammi/validation.py` to upload a file. Generic HTTP plumbing. (Worth noting
  as a packaging defect rather than a metadata one: `requests` is imported at runtime but is absent
  from `dependencies`; only `requests-mock` appears, under the `test` extra.)
- **Development and documentation tooling** — `pytest`, `pytest-astropy`, `pytest-cov`, `coverage`,
  `black`, `flake8`, `rstcheck`, `sphinx`, `sphinx-automodapi`, `sphinx-copybutton`, `setuptools`,
  `setuptools_scm`, `wheel`, `requests-mock`. All generic tooling.
- **`cdflib`, `spacepy`, `astropy`, `xarray`** — none of these is a dependency of this package at any
  extra. They appear in the *consumers'* dependency lists (`imap_processing` uses `cdflib`; `swxsoc`'s
  `cdf` extra uses `spacepy`), which is a fact about those packages.
- **The SPDF ISTP validation service** (`https://skteditor.heliophysics.net/cgi-bin/checkcdf.cgi`) — a
  web service, not software with a repository or DOI. It is described in Field 8, where it belongs.
- **`sunpy`, `ndcube`, `parfive`, `boto3`** — reachable only transitively through `swxsoc`; this
  package neither imports nor exchanges data with any of them.

### 30. Interoperable Software (OPTIONAL)
- `https://github.com/swxsoc/swxsoc`
- `https://github.com/IMAP-Science-Operations-Center/imap_processing`

Source note: HSSI stored none. Both entries meet the demonstrated-exchange bar with a specific,
citable artifact; neither rests on ecosystem membership or on sharing a Python runtime.

- **`swxsoc`** — the SWxSOC multi-mission core package declares `sammi-cdf>=0.1.2` in its `cdf` extra,
  with an in-file comment stating "sammi-cdf is maintained by the SWxSOC team with metadata support
  for SWxSOC data products", and consumes it in `swxsoc/util/schema.py`. From this side, `README.rst`
  states that "This package is a SWxSOC project and can be used in conjunction with other SWxSOC
  projects, or as a standalone package" — an explicit companion-package relationship asserted from
  both directions. `swxsoc` is itself a PyHC-registered heliophysics package, so this is a peer domain
  tool rather than infrastructure.
- **`imap_processing`** — declares `sammi-cdf<2,>=1.0` as a **core runtime dependency** (not an extra)
  and extends this package's API by subclassing it: `imap_processing/cdf/imap_cdf_manager.py` defines
  `class ImapCdfAttributes(CdfAttributeManager)`, importing
  `from sammi.cdf_attribute_manager import CdfAttributeManager`, then layers IMAP's own schema and
  attribute YAML files on top through `load_variable_attributes()` and `load_global_attributes()`. A
  subclass that layers its own schemas onto this package's is a plugin/extension relationship — the
  strongest form of exchange this field contemplates. It is also listed under Field 29 for the
  distinct historical reason recorded there.

Excluded: the same Tier A and non-dependency sets enumerated under Field 29, for the same reasons. Two
justifications were specifically not used anywhere in this field: "part of the standard scientific
Python ecosystem", and "a PyHC package, therefore interoperable with PyHC packages" — neither
demonstrates an exchange with any particular package. Note also that the direction of the dependency
does not matter for this field: in both entries the *other* package imports this one, and that is a
demonstrated exchange either way.

### 31. Related Instruments (OPTIONAL)
Not found — correctly empty. This is a relevance decision, not a resolution failure.

Source note: the package is instrument-agnostic. Its default schemas encode the generic ISTP
required-attribute set; the CF, ACDD, and GES-DISC layers are cross-disciplinary metadata conventions;
and nothing in `CdfAttributeManager` or `CDFValidator` reads, calibrates, parses, or models any
specific instrument's data. Instrument-specific schema content lives in the consumer packages, not
here.

The instrument-adjacent names that appear in the repository fail the relevance gate:

- **IMAP instrument names** (`imap_instrument1_*`, `imap_instrument2_*` in `sammi/tests/test_data/`) —
  test fixtures. Their filenames are generic, but only `imap_instrument1_*` is genuinely anonymized
  content (`Descriptor: TEST>Testinstrument`); `imap_instrument2_*` is a copy of `imap_processing`'s
  own fixture for the real IMAP SWE (Solar Wind Electron) instrument, carrying
  `Descriptor: SWE>Solar Wind Electron` and `imap_swe_l1a_sci`/`imap_swe_l1b_sci` variables. Both are
  excluded regardless of whether the instrument named inside is real, because this field's relevance
  gate excludes test fixtures as such — and "SWE" would not resolve cleanly in any case, since the
  SPASE rows abbreviated SWE belong to Wind and ISEE-1, unrelated missions. The GLOWS example in
  `docs/user-guide/cdf_attribute_management.rst` is a
  documentation excerpt quoted from `imap_processing`'s repository to illustrate YAML anchors. Test
  fixtures and doc examples are explicitly outside this field.
- **SPDF / ISTP** — a standards body, plus a metadata convention and its validation service; not an
  instrument. ISTP support is recorded in Fields 18 and 19, where it belongs.
- **GES-DISC** — a NASA data archive whose provider recommendations one schema layer implements. An
  archive is neither an instrument nor an observatory; the SPASE instrument/observatory vocabulary
  contains no GES-DISC row, consistent with that.

Because the relevance gate fails, no SPASE resolution applies here. A trap worth recording for
whoever revisits the question: searching the vocabulary for "IMAP" returns
`https://spase-metadata.org/SMWG/Instrument/Interball-2/IMAP3` and its CNES counterpart — the
Interball-2 "IMAP-3" three-axis magnetometer, an unrelated instrument that merely shares an acronym
with the Interstellar Mapping and Acceleration Probe. Binding either row to this record would be wrong
twice over.

### 32. Related Observatories (OPTIONAL)
Not found — correctly empty. Also a relevance decision.

Source note: the package is mission-agnostic in the same way. Mission names appear in the repository
only as fixture prefixes (`imap_*.yaml`), as a documentation example quoted from another repository,
and as a provenance line in `CHANGELOG.rst` ("Added Functionality from HERMES partner package") — all
categories the relevance gate excludes. A scientist working with IMAP or HERMES data would not reach
for this package to work with those data; they would reach for the mission pipeline that depends on
it, and those pipelines are recorded in Fields 29 and 30, where they carry the mission association
properly.

The negative research is recorded in detail because this is where a future agent is most likely to
over-reach, and because the availability question is settled independently of the relevance question:

- **HERMES does have a vocabulary row** — `https://spase-metadata.org/SMWG/Observatory/HERMES`
  ("Heliophysics Environmental and Radiation Measurement Experiment Suite"), alongside a duplicate
  `.html` form of the same identifier. So HERMES is omitted **because the software does not support it
  specifically**, not because it could not be resolved. The same is true of PADRE
  (`https://spase-metadata.org/SMWG/Observatory/PADRE`), which is reachable only transitively through
  `swxsoc`.
- **IMAP has no vocabulary row at all** — no row matches the Interstellar Mapping and Acceleration
  Probe by name, abbreviation, or identifier path; the only "IMAP" hits are the unrelated Interball-2
  instrument rows noted under Field 31. Even if the relevance judgment were reversed, the entry could
  not be recorded: this field is SPASE-only, and a name without an `https://spase-metadata.org/`
  identifier must never be emitted, because doing so creates a new identifierless row instead of
  matching an existing resource.

### 33. Logo (OPTIONAL)
`https://raw.githubusercontent.com/swxsoc/sammi/e764c4c84d5e511799ffc47d446a76f17501b8a2/docs/logo/sammi_logo.png`

Source note: HSSI stored an empty logo. This URL is the one curated by the PyHC registry for this
project, which makes it the preferred form under the metadata priority order; it was verified to
resolve and to return a PNG image. It is pinned to a commit SHA rather than to `main`, so its content
cannot change if the file is moved or replaced upstream — which is what this field's "stored online
in a permanent place" instruction asks for.

The same image lives in the repository at `docs/logo/sammi_logo.png`. Two alternative permanent URLs
for it were considered: the same raw path pinned to the release revision
(`.../9d2b8975114aab2bef55072a8a75e1590e4570e5/docs/logo/sammi_logo.png`), which was also verified to
return a PNG of identical size, and the blob URL pinned to `f8086f30` that `docs/acknowledging.rst`
offers to presenters (a rendered HTML page rather than an image resource, so unsuitable here). The
PyHC-curated URL is recorded in preference to both because it is the community-curated value and
carries no risk of diverging from what the registry displays. Either of the others may be substituted
without loss if the pinned commit ever becomes unreachable.

---

## Cross-cutting notes

**Upstream documentation defects observed at this revision.** Recorded so a later refresh recognizes
them instead of re-deriving values from them:

1. `CHANGELOG.rst`'s oldest block, `0.0.0 (2023-03-22)` / "Initial project release", is inherited
   partner-package text; the date is `hermes_core`'s 0.2.0 release date, and no artifact of this
   project exists near it (Field 10).
2. The 1.1.0 CHANGELOG section ends with "Added Functionality from HERMES partner package", a bullet
   left over from the pre-1.0 "Latest" section rather than a 1.1.0 change (Field 12).
3. `LICENSE.rst` is a one-line pointer to `licenses/LICENSE.md`, which is why GitHub reports
   `NOASSERTION` and PyPI's license field reads "see licenses/LICENSE.md" (Field 15).
4. `.zenodo.json` declares its author array under the key `"authors"` where Zenodo expects
   `"creators"`, so the deposits ignore the maintainers' curated names, ORCIDs, and affiliations and
   fall back to GitHub contributor handles (Field 6).
5. `pyproject.toml` still classifies the package `Development Status :: 3 - Alpha` after the 1.x series
   and downstream production adoption (Field 23).
6. `requests` is imported at runtime by `sammi/validation.py` but is absent from `dependencies`
   (Field 29).

**Unresolved identity.** The contributor `pleasant-menlo` is credited on the v1.0.2 and v1.1.0 Zenodo
deposits and authored PR #23, but is identified only by a GitHub handle. If the person's name becomes
available, they should be added to Field 6.
