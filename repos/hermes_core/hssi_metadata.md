# HSSI Metadata Extraction Results

**HSSI Software ID:** b5867d88-1fd5-476e-98e0-498ccbf41655
**Repository:** https://github.com/HERMES-SOC/hermes_core
**Source Revision:** 416231f5982f53d03ad04b206e33e8018b856792
**Extraction Date:** 2026-09-01
**Validation Date:** 2026-09-02
**Validation Status:** PASS

---

**Scope note — read this before the evidence below.** At the pinned revision `hermes_core` is a thin,
HERMES-specific configuration layer over the `swxsoc` framework, not a self-contained package.
`pyproject.toml` declares `'swxsoc @ git+https://github.com/swxsoc/swxsoc.git@main',` as its first
dependency; `hermes_core/timedata.py` declares `class HermesData(SWXData):`; `hermes_core/util/schema.py`
declares `class HermesDataSchema(SWXSchema):`; `hermes_core/util/util.py` opens with
`from swxsoc.util import util` and its two public functions are pass-throughs; and
`hermes_core/__init__.py` sets `os.environ["SWXSOC_MISSION"] = "hermes"` then calls
`swxsoc.reconfigure()`. Commit `009a0d1` (2024-09-26, "Generic SWxSOC Integration (#122)") performed
that migration. Consequently several user-facing capabilities recorded below are *implemented* in
`swxsoc` and *exposed* through `hermes_core`'s own classes and documentation. Where that is the case
the field note says so and names where the implementation lives, because a future agent reading only
`hermes_core`'s source will not find the code.

A second consequence matters for reproducibility: because the dependency is pinned to swxsoc's `main`
branch rather than a release, swxsoc code cited here is quoted from commit
`bfe87e4900b019a2b5c2f012da3925a3d551fd48` (2026-08-26) and could change without any change to
`hermes_core`.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source:* Catalogue convention. HSSI's submitter fields identify the person lodging the metadata, not
an author of the software, so the dossier carries a placeholder and the value is supplied at
submission time.

---

### 2. Persistent Identifier (RECOMMENDED)
**Not found — no persistent identifier for this software exists.**

**Previous value and why it is not this software's identifier.** HSSI held
`https://doi.org/10.5281/zenodo.10257715` for this field. That DOI is the Zenodo *concept* DOI of
record `10257716`, and the record is a **conference poster, not a software deposit**:

- title `HERMES Core and Instrument Packages`; Zenodo `resource_type` `{'title': 'Poster', 'type': 'poster'}`
- publication date 2023-12-04; licence `cc-by-4.0`
- its sole file is `2023 AGU HERMES Packages.pdf` (7,572,942 bytes, md5 `3046692fab6e881d7df04226fe5e94a5`)
- Zenodo `related_identifiers` is `null` — no relation to the GitHub repository, no `IsSupplementTo`
- DataCite types both `10.5281/zenodo.10257715` and `10.5281/zenodo.10257716` as
  `resourceTypeGeneral` `Text`, `resourceType` `Poster`

**Why the change, argued from the site user's side.** A visitor on the HERMES Core page who clicks the
persistent identifier expects the archived software — something citable as *the code*, ideally with a
downloadable version. What that link actually delivers is a 7.5 MB PDF of an AGU poster. The poster's
Zenodo resource type is not shown to a site visitor; the poster page is. The link is not useless, but
it answers a different question from the one the field asks, and a reader who cites it is citing a
poster while believing they are citing software.

The concrete harm is not only presentational. Field 2 is the DOI-autofill anchor, so a poster DOI
sitting in it invites future refreshes and automated tooling to pull poster attributes into software
fields — CC-BY-4.0 as the software licence, 2023-12-04 as the software's date, Zenodo as the
software's publisher. The record already carried one instance of exactly that (Field 11 below).

The poster is genuinely *about* this software, so it is not discarded: both HERMES posters are
recorded under Field 27 (Related Publications), where "Publications that describe, cite, or use the
software" is precisely what a conference poster is. The user still reaches the poster from the HERMES
Core page, under a heading that tells them truthfully what they are about to open.

**What a real software DOI for this project would look like.** The same organisation's `swxsoc`
package has one: `https://doi.org/10.5281/zenodo.15546486` is typed `resourceTypeGeneral` `Software`
and carries `IsSupplementTo` `https://github.com/swxsoc/swxsoc/tree/0.2.3` — the GitHub-Zenodo code
deposit signature. The HERMES Core poster records have neither property. That contrast is the
cleanest available demonstration that the DOI this field carried was never a code deposit.

**The project itself expects a software DOI that does not exist yet.** `hermes_core/CITATION.rst`
tells users "The software citation should be the specific `Zenodo DOI`_ for the version used in your
work." The reStructuredText link target `Zenodo DOI`_ is never defined — the reference is dangling
across the whole pinned tree, and the word "zenodo" appears nowhere else in it. So the intent to have
a per-version software DOI is on record; the DOI is not.

**Negative research — do not repeat this search.** No software deposit for `hermes_core` was
discoverable as of 2026-09-01 by any of these routes:

- Zenodo ORCID-keyed creator searches (`metadata.creators.person_or_org.identifiers.identifier`) for
  Christe `0000-0001-6127-795X`, Barrous-Dume `0009-0006-2684-0675`, Rager `0000-0001-7088-1059` and
  Robbertz `0009-0008-6857-0882`. The software deposits those searches surface belong to sunpy,
  radiospectra, STIXpy, CCSDSPy and foxsi/foxsi-optics-sim — none to hermes_core.
- Zenodo name-keyed creator searches (`metadata.creators.person_or_org.name`) for all eight authors.
- DataCite `query=hermes_core` → 0 results; DataCite `query="HERMES-SOC"` → 0 results; DataCite
  `query="HERMES Core"` → 11 results, none typed Software, of which the relevant four are the concept
  and version DOIs of the two posters below.
- A repository-rename redirect test on `https://github.com/HERMES-SOC/hermes_core`, which answers 200
  at the same URL with no redirect — the repository has not been renamed, so no deposit is hiding
  under a former name.

A sibling poster exists and is also not software: `https://doi.org/10.5281/zenodo.8400671`
(concept `10.5281/zenodo.8400670`), "The Architecture and Functionality of HERMES Core and Instrument
Python Packages", 2023-10-09, whose sole file is `2023_DASH_HERMES_Packages.pptx`. A future refresh
must not conclude from the absence of a software DOI that no DOI exists at all: two poster DOIs do, and they
belong in Field 27.

**What would fill this field.** The maintainers enabling the GitHub-Zenodo integration on
`HERMES-SOC/hermes_core` and cutting a release, which would mint a concept DOI carrying
`IsSupplementTo` a repository tree URL — and would simultaneously resolve the dangling `Zenodo DOI`_
reference in `CITATION.rst`.

**Alternative considered and rejected: keep the poster DOI.** The argument for keeping it was real —
it is the project's own registered DOI, it describes this exact software, and clearing the field
leaves HSSI with no persistent identifier at all. It was rejected because Field 2 makes a specific
claim — "The globally unique persistent identifier for the software" — that a poster cannot honour, and
because an empty Field 2 is an accurate statement of this project's situation, whereas a poster DOI is
an inaccurate one. Moving the poster to Field 27 rather than to Field 14 was decided on the same
ground: Field 14 wants the paper that describes the software, and the project states it has none.

**Fields 2 and 11 are coupled and must move together.** Publisher is Zenodo only when a Zenodo DOI
identifies the software; with this field empty, Publisher is the repository host. Any future change
that puts a software DOI here — the deposit described above — must set Publisher to Zenodo in the same
change.

---

### 3. Code Repository (MANDATORY)
`https://github.com/HERMES-SOC/hermes_core`

*Source:* The repository itself, corroborated by the PyHC registry entry's `code:` and `url:` values
and by GitHub's own `html_url`. The URL answers 200 with no redirect, confirming the repository has
not been renamed or transferred.

---

### 4. Software Functionality (RECOMMENDED)

- Data Processing and Analysis
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: Line Plots
- Mission-related
- Mission-related: Calibration
- Mission-related: Processing
- Mission-related: Science Data Processing

All nine confirmed present in HSSI's live `FunctionCategory` vocabulary and written in the canonical
`Parent: Child` form with a space after the colon. Every subcategory has its parent listed alongside
it, as the taxonomy requires.

**Why each value is here.**

- **Data Processing and Analysis / …: Processing** — the package's substance is a processing layer:
  `HermesDataSchema` layers the two HERMES CDF attribute YAML files to derive ISTP global and variable
  attributes; `HermesData.validate` builds a `CDFValidator` (`validator = CDFValidator(schema)`) to
  check a written file against those requirements; `create_science_filename` and
  `parse_science_filename` implement the HERMES filename convention documented in
  `docs/user-guide/cdf_format_guide.rst`.
- **…: Time Series Analysis** — the container's primary structure is an
  `astropy.timeseries.TimeSeries`; the class offers `add_measurement`, `append` (concatenating
  additional measurements onto an existing time series), removal, and time-axis plotting. This is the
  weakest of the retained values: the package manipulates and organises time series rather than
  performing statistical time-series analysis. It was retained anyway, because a user searching for
  time-series tooling for HERMES data would be served by it, and because "time" is a keyword the
  project itself advertises. Re-open this one only if the package's time-series surface actually
  narrows — for instance if `append` and the time-axis plotting move out of `HermesData` — not on a
  re-reading of the same evidence.
- **Data Visualization / …: Line Plots** — `docs/user-guide/reading_writing_data.rst` states "The
  :py:class:`~hermes_core.timedata.HermesData` provides a quick way to visualize its data through
  `~hermes_core.timedata.HermesData.plot`." and carries a rendered `.. plot::` example. The method is
  inherited from `SWXData` rather than defined in this repository; in swxsoc at
  `bfe87e4900b019a2b5c2f012da3925a3d551fd48` it is `def plot(self, axes=None, columns=None, subplots=True, **plot_args):`
  and its drawing call is `this_ax.plot(self.time, self.timeseries[this_col], **plot_args)`. Inherited
  or not, it is reached through `hermes_core`'s own class and documented in `hermes_core`'s own user
  guide, so it is a capability of this software from the user's side. It produces multi-panel line
  plots of scalar time series and nothing else, which is why `Line Plots` is the only visualization
  subcategory recorded.
- **Mission-related / …: Processing / …: Science Data Processing** — the package is not a general tool
  that happens to read mission data; it is hard-wired to one mission. `hermes_core/__init__.py` sets
  `os.environ["SWXSOC_MISSION"] = "hermes"`, the instrument whitelist is fixed to the four HERMES
  instruments, and the CDF attribute schemas encode HERMES conventions agreed with SPDF. It is the
  shared science-data-processing interface of the HERMES Science Operations Center.
- **Mission-related: Calibration** — retained on mission-role grounds, not on algorithmic grounds; see
  the removal note immediately below for the distinction. `.github/workflows/calibration.yml` builds
  the HERMES SDC's `sdc_aws_processing_lambda` image with this package installed from the pull
  request under test and runs an EEA processing event through it end to end. The package is the shared
  interface through which HERMES instrument calibration is executed, even though it contains no
  calibration algorithm.

**Values the record carried until this refresh, and why they were removed.**

- **Data Processing and Analysis: Calibration** — removed. The pinned tree contains no calibration
  code. `docs/cmad/index.rst` states in full that "HERMES consists of multiple instruments, each of
  which hosts its Calibration and Measurement Algortihm Document." and directs the reader to each
  instrument's documentation; the project's own description likewise says additional per-instrument
  packages "provide specific calibration and processing functionality". Outside `docs/cmad/index.rst`
  and the mission-pipeline CI workflow discussed above, the word appears in the pinned tree only in
  places that are not a calibration capability: an example *support variable* a user supplies
  (`name="calibration_const"` in `docs/examples/tutorial1.rst` and `name="Calibration_const",` in
  `docs/user-guide/reading_writing_data.rst`), and a passing mention in the CDF format guide of a
  "change in calibration" as a reason to increment a data version. A user filtering HSSI for generic
  calibration software would open this entry, look for a calibration API, and find none — that is the
  out-of-place case the relevance test is meant to prevent. `Mission-related: Calibration` is retained
  because that filter asks a different question — which mission software is
  involved in calibration — and this package genuinely answers it as the SDC's shared interface.
- **Data Processing and Analysis: Data Access and Retrieval** — removed. The category is about
  obtaining data from remote archives. This package offers `HermesData.load(file_path)`, which reads a
  local CDF file you already possess; `hermes_core/util/util.py` exports only
  `create_science_filename` and `parse_science_filename`, and nothing in `hermes_core`'s public API
  searches, queries or downloads. There is also nothing to retrieve: HERMES has no public data archive
  (see Field 28), and the package's own sample file is synthetic, generated by the tutorial per
  `hermes_core/data/sample/README.rst` ("This file is generated by the code provided in
  :file:`docs/examples/tutorial1.rst`").
- **Data Processing and Analysis: Spectrogram** and **Data Visualization: Spectrogram** — both
  removed. The package computes no time-frequency representation: no FFT, STFT, wavelet or periodogram
  appears anywhere in this repository. And it renders no dynamic spectrum: the inherited `plot` method iterates the
  `timeseries` columns only and never touches `self.spectra`. Within the pinned tree the string
  "spectrogram" occurs once, in
  `hermes_core/data/hermes_default_variable_cdf_attrs_schema.yaml`, as one of the permitted
  ISTP `DISPLAY_TYPE` values — metadata the package derives to tell downstream tools such as CDAWeb
  how a variable should be displayed, not a rendering the package performs.
  **The counter-argument, recorded so it is not re-discovered as new:** spectral data are a
  first-class part of the container. `HermesData.__init__` accepts
  `spectra: Optional[ndcube.NDCollection] = None,`; `add_spectra` exists; the user guide has a section
  on building an `NDCollection` for it; and the AGU poster gives `.spectra` equal billing with
  `.timeseries`. The package therefore *carries, annotates and writes* spectrograms without computing
  or drawing them. That capability is represented by the retained `…: Processing` value, by the
  `spectra` keyword in Field 16, and by `ndcube` in Field 30 — spectral handling is not lost from the
  record, only classified where the evidence puts it.

**Values considered and rejected (the record carried none of these before this refresh, and none was
added; recorded to stop re-proposal).**

- **Data Processing and Analysis: Energy Spectra** — the spectra the container holds do carry energy
  axes, but the package performs no spectral computation; same evidence as the Spectrogram removals.
- **Data Processing and Analysis: Analysis** — no statistical method, derived physical quantity or
  scientific calculation is implemented.
- **Data Processing and Analysis: File Format Conversion** — CDF is both the input and the output
  format; nothing is converted between two file formats.
- **Coordinate Transforms** (any subcategory) — tempting because the AGU poster advertises ndcube as
  enabling conversion from detector coordinates to physical coordinates, but that is `ndcube`'s WCS
  machinery operating on objects the user builds, not a coordinate transform this package implements,
  and it is not a heliophysics reference-frame transform in the sense this field means.
- **Mission-related: Packet Decommutation** — the 0.1.0 changelog bullet reads "* Utilities parsing
  compliant filenames for level 0 binary files and creating and parsing higher level filenames". What
  is parsed is *filenames*, at level 0 and above — the clause the bullet ends on makes that explicit
  — not packets. No telemetry or CCSDS parsing exists at the pin.
- **Mission-related: Ingest**, **Mission-related: Archive** — the package produces archive-ready,
  ISTP-compliant CDFs destined for SPDF, and its output feeds the SDC's ingest pipeline, but the
  ingesting and archiving are done by separate HERMES-SOC repositories, not by this package.
- **Mission-related: Infrastructure as Code**, **Servers and Environments: Software or Environment
  Container** — the poster describes SWxSOC's IaC deployments and the repository has a
  `.devcontainer` pointing at an AWS ECR lambda base image, but those are the framework's
  infrastructure and this repository's development environment respectively, not functionality this
  software provides.
- **Mission-related: System Testing** — `calibration.yml` is continuous integration for this package,
  not a system-testing capability the package offers to users.
- **Data Visualization: Mission-Specific** — the plot title is composed from mission metadata
  (`Mission_group`, `Descriptor`, `Data_level`), but the plot itself is a generic multi-panel line
  plot; a mission-derived title is not a mission-specific visualization type.

---

### 5. Related Region (RECOMMENDED)

- Earth Magnetosphere
- Earth Magnetotail
- Interplanetary Space
- Solar Wind

All four confirmed present in HSSI's live `Region` vocabulary. **The vocabulary is flat**: parent and
child rows exist but the relationships are empty, so a fine value does not imply its coarse parent and
no "X encompasses Y" reasoning is used below.

**Why this rests on repository evidence rather than mission publicity.** The obvious objection to
giving a data-container package any region at all is that a container has no physics. It applies to
mission-agnostic containers; it does not apply here, because this package cannot be used with anything
but HERMES data. `hermes_core/__init__.py` fixes the mission
(`os.environ["SWXSOC_MISSION"] = "hermes"`), the instrument name is validated against a four-value
HERMES whitelist, and the filename convention is `hermes`-prefixed with the instrument identifiers
"`eea`, `mrt`, `nem`, `spn`". Every file this software is built to read or write is a HERMES science
file — `parse_science_filename` raises if a filename's mission is not HERMES — so the physical region
this software's functionality is intended for is exactly the region HERMES measures, and the
repository's own documentation, not a brochure, says what that is.

- **Earth Magnetosphere** — the strongest in-code evidence. The package's global attribute schema,
  `hermes_core/data/hermes_default_global_cdf_attrs_schema.yaml`, hard-codes the ISTP `Discipline`
  attribute with `default: Space Physics>Magnetospheric Science` and states "this value should always
  be "Space Physics>Magnetospheric Science."". The software therefore classifies HERMES data as
  magnetospheric science by default and in its own words. (The attribute is declared
  `overwrite: false`, so a user who supplies their own `Discipline` keeps it; the default is what the
  package asserts, not an unconditional stamp.)
- **Earth Magnetotail** — `docs/user-guide/cdf_format_guide.rst` §2 "HERMES Science Investigations"
  describes EEA as providing measurements of "low-energy electrons in the solar wind and in Earth’s
  deep magnetotail by measuring electron flux as functions of energy and direction." and SPAN-I as
  measuring "Interplanetary and Magnetotail ion flux as functions of direction and energy/charge from
  several eV/q to 20 keV/q."
- **Interplanetary Space** — the same SPAN-I sentence, which names interplanetary ion flux alongside magnetotail ion
  flux, plus MERIT, whose two telescopes are described as nominally spanning the forward and reverse
  Parker Spiral.
- **Solar Wind** — the same EEA sentence ("low-energy electrons in the solar wind"), plus the schema's
  `Instrument_type` acceptable-value list for HERMES, which includes "- Plasma and Solar Wind". This
  value did not exist in the Region vocabulary at the time of the legacy extraction; it does now, and
  it is the most direct expression of what EEA and SPAN-I measure.

**Value removed: Solar Environment.** The record carried it until this refresh. The legacy dossier
justified it as "HERMES observes solar particles and solar wind directly from the Sun", derived from
a NASA web search. That reads the mission backwards: the particles originate at the Sun, but every
HERMES measurement is made in situ at lunar distance. Nothing in the repository or in the project's own poster places any
HERMES observation at or near the Sun, and the suite carries no remote-sensing instrument — EEA,
MERIT, NEMISIS and SPAN-I are all in-situ particle and field sensors. A user filtering HSSI for `Solar Environment` is
looking for solar and near-Sun software; a cislunar CDF data container is out of place in that result
set. The solar-origin science that motivated the value is carried accurately by `Solar Wind` and
`Interplanetary Space` instead.

**On keeping the coarse value alongside the fine one.** `Earth Magnetosphere` is *not* retained
because the magnetotail is inside it — that argument is invalid against a flat vocabulary. It is
retained on its own independent evidence (the hard-coded `Space Physics>Magnetospheric Science`
discipline) and because the facet does not roll fine values up: dropping it would make a
deep-magnetotail data package invisible to every user who filters on `Earth Magnetosphere`, and such a
user would be glad, not surprised, to find it.

**Considered and rejected:** `Earth Magnetosheath` and `Earth Outer Magnetosphere` — a lunar-distance
orbit does cross both, but the repository documents only "deep magnetotail", and inferring the rest
from orbital geometry is exactly the brochure reasoning this field is meant to avoid.
`Earth Inner Magnetosphere` — contradicted by "deep magnetotail". `Earth Ionosphere` / `Earth
Atmosphere` — the poster's "escape of atmospheric ions" names ions that *originate* in the upper
atmosphere, but HERMES measures them in the tail, and the software supports the tail measurement.
`Heliosheath`, `Planetary Magnetospheres`, and the solar-interior/corona/chromosphere/photosphere
values — no supporting evidence of any kind.

---

### 6. Authors (MANDATORY)

Eight authors, in the order HSSI stores them.

1. **Steven Christe** — ORCID `https://orcid.org/0000-0001-6127-795X`
   - Goddard Space Flight Center — ROR `https://ror.org/0171mag52`
2. **Damian Barrous-Dume** — ORCID `https://orcid.org/0009-0006-2684-0675`
   - Community Coordinated Modeling Center — ROR `https://ror.org/01dy3j343`
   - Navteca
   *(on the spelling of this name, see the note below)*
3. **Steve Kreisler** — no identifier
   - Columbus Technologies and Services
4. **Tony Mercer** — no identifier
   - Space Sciences Laboratory, University of California, Berkeley — ROR `https://ror.org/048400679`
5. **William R. Paterson** — no identifier
   - Goddard Space Flight Center — ROR `https://ror.org/0171mag52`
6. **Amy Rager** — ORCID `https://orcid.org/0000-0001-7088-1059`
   - General Dynamics Mission Systems
7. **Andrew Robbertz** — ORCID `https://orcid.org/0009-0008-6857-0882`
   - General Dynamics Mission Systems
   - Goddard Space Flight Center — ROR `https://ror.org/0171mag52`
8. **Daniel Skeberdis** — no identifier
   - a.i. solutions, Inc.

**Sources and the union check.** Three independent sources name authors, and the union adds nobody:

- `pyproject.toml` lists three with e-mail addresses — Steven Christe, "Damian Barrous Dumme" and
  Andrew Robbertz. All three are already present.
- The Zenodo poster record `10257716` lists eight creators; they match the eight above one-for-one,
  and their `affiliation` strings are the origin of the affiliation values HSSI stores.
- The AGU poster's printed byline lists the same eight, with a numbered affiliation key.

There is **no `CITATION.cff`, `codemeta.json`, `.zenodo.json`, `AUTHORS` or `CONTRIBUTORS` file** in
the pinned tree; `hermes_core/CITATION.rst` gives citation guidance with no author list. So the
author set is complete and no author is dropped.

**Name spelling — corrected, and not to be reverted.** ORCID `0009-0006-2684-0675` gives given-names
`Damian` and family-name `Barrous-Dume`. The Zenodo creator entry spells the name
`Barrous-Dume, Damian`, and the poster byline spells it `D. Barrous-Dume`. `pyproject.toml` spells it
`Damian Barrous Dumme` — a typo in the packaging metadata, with three other sources agreeing against
it — so a later refresh reading only the packaging metadata must not *correct* the name back to that
form. The record split the name as given `Damian Barrous` / family `Dume` until this refresh, which
rendered as "Damian Barrous Dume", losing the hyphen and putting the split in the wrong place; it now
holds given `Damian`, family `Barrous-Dume`, matching ORCID and both Zenodo poster records.

**Standing constraint on any future name correction.** A Person's name cannot be changed through the
metadata API: a request carrying a corrected name silently mints a duplicate Person row and orphans
the original, stranding every software association the original carried. That risk is concrete here,
because this Person row is shared — the same row, with the same ORCID, is an author of the SWxSOC
catalogue entry, so a careless attempt would have damaged that entry too. A name correction must
therefore be made directly in the database rather than sent as a metadata value, which is the route
this one took; the corrected spelling reaches both entries because they share the row.

**Negative research on the four authors without identifiers — do not repeat.** ORCID's public
expanded search on 2026-09-01 returned, for `Kreisler`, thirteen same-surname records, none of them
Steve Kreisler and none affiliated with Columbus Technologies and Services or NASA; for `Tony Mercer`,
zero records; for `Skeberdis`, two records (a Lithuanian physiologist and an unrelated Penn State
researcher); for `William Paterson`, seven same-name records, none with a NASA, GSFC or heliophysics
affiliation. **No ORCID can be attributed to any of the four**, and none should be attributed on a
name match alone.

**Structural hazard to observe if an ORCID is ever found.** Sending an ORCID for an author whose
stored Person row has no identifier creates a duplicate Person row and orphans the original.
Any ORCID discovered later for Kreisler, Mercer, Paterson or Skeberdis therefore belongs in a database
correction, not in a metadata update.

**Considered and not applied: a second affiliation for Amy Rager.** The AGU poster's byline
gives Rager superscripts `1,2` — NASA Goddard Space Flight Center *and* General Dynamics Mission
Systems — exactly as it does for Andrew Robbertz. HSSI stores both affiliations for Robbertz but only
General Dynamics Mission Systems for Rager, so the record treats the same byline evidence
inconsistently between two co-authors. It was nonetheless **not applied**, because the structured
creator metadata on *both* Zenodo poster records — the machine-readable authority for the same two
posters, supplied by the team — gives Rager exactly one affiliation, `General Dynamics Mission
Systems`, and the superscript is the only contrary evidence. One further data point does not settle
it either way: Rager's ORCID record carries a single self-asserted employment, organisation
`National Aeronautics and Space Administration` with ROR `https://ror.org/027ka1x80`, no department
and no dates — and no General Dynamics entry at all. That is agency-level rather than the
GSFC-level ROR `https://ror.org/0171mag52` the byline reading would need, so it neither confirms the
GSFC affiliation nor contradicts the stored General Dynamics one. The evidence is recorded in full so
the inconsistency stays visible, but the question is settled for now: re-open it only if a source
carrying the authority of the Zenodo creator metadata — a corrected deposit, or an ORCID employment
naming Goddard Space Flight Center rather than the agency — gives Rager that affiliation directly.

**Affiliation identifiers not filled, and why.** Four affiliation organisations are stored without a
ROR:

- `a.i. solutions, Inc.` — a ROR exists: `https://ror.org/02nt9wa64` ("a.i. solutions (United
  States)", website `https://ai-solutions.com/`).
- `Columbus Technologies and Services` — a ROR exists: `https://ror.org/00g81mg52` ("Columbus
  Technologies and Services (United States)", website `http://www.columbususa.com/`).
- `General Dynamics Mission Systems` — **no ROR for this business unit.** ROR carries the parent
  company as `https://ror.org/05pyq8e17` ("General Dynamics (United States)") and a Canadian sibling
  as `https://ror.org/0113m2308`. Attaching the parent company's ROR to a business-unit row would
  assert an identity that is not true; the field is correctly left empty.
- `Navteca` — a ROR search returns no results. Correctly empty.

The first two are the correct target state. They are not proposed as metadata values because the
stored Organization rows already exist without identifiers, and writing an identifier onto an existing
identifier-less organisation risks minting a duplicate row in the same way the ORCID hazard above
does; they belong in a database correction.

**Department-level affiliation detail deliberately not adopted.** The sibling DASH poster's Zenodo
record gives finer affiliations for three authors — Christe as "NASA GSFC, Solar Physics Lab",
Paterson as "NASA Goddard Space Flight Center, Geospace Physics Laboratory", Barrous-Dume with
"Community Coordinated Modeling Center, NASA GSFC, Navteca". The stored institution-level values are
correct as they stand and match the AGU record that the rest of this entry derives from; splitting in
laboratory-level rows would add organisation rows without improving what a user learns.

---

### 7. Software Name (MANDATORY)
`HERMES Core`

*Source and choice.* The name the project uses for itself in prose: `docs/index.rst` is headed
"HERMES Core Documentation" and the Zenodo poster is titled "HERMES Core and Instrument Packages".
Alternatives considered: `hermes_core` — the repository name and the `pyproject.toml` distribution
name (`name = "hermes_core"`), correct as an import/package identifier but reads as a filename in a
catalogue listing; `HERMES-Core` — the PyHC registry's spelling, a registry-key style with no basis in
the project's own prose. `HERMES Core` is recorded because it is the project's own human-readable
name and because a name is editorial: there is no factual defect here to correct.

---

### 8. Description (MANDATORY)

> A central Python package for common functionality across all HERMES instruments. The HERMES core package contains Python interfaces for the loading, calibrating, plotting, validating, and saving of measurement data through Common Data Format (CDF) files. Additional packages are created for HERMES instruments to provide specific calibration and processing functionality. The abstraction of intricate, high heritage, data formats, such as CDF files, in Python enables easier analysis and opens doors for greater participation in heliophysics science.

*Provenance, established by direct comparison.* The stored text is a composite of two project-authored
sources. Its opening sentence is the repository's own one-line description. The PyHC registry's
`description:` field carries it exactly: "A central Python Package for common functionality across
all HERMES instruments". GitHub's repository description is the same sentence with three
differences — it lower-cases the mission name ("across all hermes instruments"), it has no closing
full stop, and it ends with a trailing space. The stored value normalises all of that: lower-case
"package", upper-case "HERMES", and a full stop. The remaining 469 characters are **byte-identical** to
the corresponding portion of the AGU poster's Zenodo abstract, from "The HERMES core package
contains" to the end. The abstract's own opening sentence (about the HERMES SOC team having developed
a series of packages) was dropped in favour of the repository one-liner, which is the better lead for
a software catalogue.

*Why this wording stands.* It is the project's own, it is accurate about what the package is for, and
its first 150–200 characters make a usable preview. One observation for a future reader, recorded
rather than acted on: the sentence advertises "calibrating", and the package contains no calibration
algorithm (see Field 4). That is the project's own characterisation of its role in the HERMES
calibration chain, published on its poster, and rewriting a maintainer-authored description to
second-guess it would be editorialising; Field 4 carries the precise capability claim instead.

---

### 9. Concise Description (OPTIONAL)

> A Python package to support the HERMES instrument packages, providing common functionality for loading, calibrating, plotting, validating, and saving measurement data through CDF files.

*Source.* Built from `pyproject.toml`'s `description = "A Python package to support the HERMES
instrument packages."`, extended with the capability list from the description above. 185 characters,
inside the field's 200-character limit. It stands as written: an accurate, well-formed preview, and
the same editorial-intent reasoning as Field 8 applies.

---

### 10. Publication Date (RECOMMENDED)
`2022-10-05`

**The record carried `2022-03-17` until this refresh.** The field asks for the "Date of first
broadcast/publication" and states that it is "Used for the initial version of the software." The
initial version is v0.1.0, and
two independent project sources date it to 2022-10-05: `CHANGELOG.rst` heads its earliest section
"0.1.0 (2022-10-05)", and the GitHub release `v0.1.0` has `published_at` `2022-10-05T16:27:21Z`.

*Alternatives, and why they lost.* `2022-03-17` is GitHub's `created_at` for the repository
(`2022-03-17T20:44:09Z`) — the moment an empty repository was created, six and a half months before
anything was released and before the changelog records any version. It was not an editorial choice by
a submitter; the legacy dossier labelled it "(repository creation date)" and recorded 2022-10-05
separately as the first release date, so the value it displaced was a mechanical artefact of
automated GitHub-metadata extraction rather than a judgement to preserve. `2022-03-10` is the author date of the
first commit (`58d7889`, "Initial commit"), which predates even the repository's creation and reflects
local authoring rather than publication. A third possibility, `2022-09-27` (the date of the commit
`v0.1.0` tags), is the tag's commit date rather than the release's publication date and disagrees with
the changelog.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** `https://github.com`

**The record carried `Zenodo` / `https://zenodo.org` until this refresh.** The field's own
instruction settles it: Zenodo is correct "For software where a DOI has been obtained through Zenodo
(e.g., GitHub-Zenodo workflow)", and "If no DOI has been obtained, indicate the repository host, such
as GitHub or GitLab." No software DOI has been obtained (Field 2). That Zenodo value was a direct
consequence of the poster DOI having occupied Field 2 — poster metadata that had migrated into a
software field, which is the harm Field 2's note describes. The software's actual distribution channel is GitHub: there is
no PyPI release, and even the project's own CI installs it as
`hermes_core@git+https://github.com/HERMES-SOC/...`.

**This value is coupled to Field 2 and the two move together.** GitHub is the Publisher precisely
because no software DOI identifies this package. If the project mints a real Zenodo software deposit,
Field 2 takes that DOI and this field returns to Zenodo in the same change; the poster DOI does not
qualify and must not be used to trigger that.

---

### 12. Version (RECOMMENDED)
- **Version Number:** `v0.2.0`
- **Version Date:** `2023-03-22`
- **Version Description:** Improvements tested in the second HERMES Ground System dataflow test:
  f-strings replace the older format syntax; a log message on import reports the package version;
  documentation content and styling improvements; packaging moves from `setup.py` to
  `pyproject.toml`; bug fixes for `pathlib.Path` support and a devcontainer permissions bug.
- **Version PID:** none

**Number and date — confirmed correct.** `v0.2.0` is the most recent tag reachable from the pinned
revision and the most recent GitHub release. Both tags in this repository, `v0.1.0` and `v0.2.0`, are
ancestors of the pin, so there is no orphaned-lineage complication here. The date 2023-03-22 is the
release's `published_at` (`2023-03-22T18:52:58Z`) and matches `CHANGELOG.rst`'s section heading
"0.2.0 (2023-03-22)". It deliberately does **not** use the tagged commit's date, 2023-01-05
(`ff6aef9`), which is when the release was drafted; the changelog and the publication both say March.

**Version Description.** The record held no version description before this refresh. The text above
is a faithful condensation of `CHANGELOG.rst`'s own 0.2.0 bullet list.

**Version PID — deliberately empty.** The legacy dossier recorded
`https://doi.org/10.5281/zenodo.10257716` here. That is the **poster's** version DOI, not a software
version DOI, and it must not be reinstated; see Field 2.

**The shape of this project's release history, recorded because it explains several other fields.**
The package was released twice early (v0.1.0 2022-10-05, v0.2.0 2023-03-22) and has not been released
since, while thirty-eight commits accumulated on `main` after `v0.2.0` — twenty-five in 2023, eleven
in 2024, one in 2025 and one in 2026. Crucially, **the released versions do not contain the package's
headline capability**: `hermes_core/timedata.py` does not exist at tag `v0.2.0`, which contains only
configuration, logging, exceptions and the filename utilities. `HermesData` first appeared on
2023-07-07 in commit `57981ea` ("CDF Data Interoperability (#56)"), after the last release, and
`CHANGELOG.rst`'s unreleased `Latest` section still reads "* Added data class to hold measurements and
to save to CDF files". Anyone installing v0.2.0 gets a package without the data container that this
catalogue entry describes; the way the project is actually consumed is a direct git install, exactly
as its own `calibration.yml` workflow does.

**Why there is no version string in the source.** `pyproject.toml` declares `dynamic = ["version"]`
with `write_to = "hermes_core/_version.py"` under `[tool.setuptools_scm]`, and
`hermes_core/__init__.py` imports `__version__` from that generated file. There is therefore no static
version to read from the tree, and a development install reports a setuptools-scm-derived string
rather than a release number.

**PyPI is a trap on this package's name — do not read a version from it.** `https://pypi.org/pypi/hermes_core/json`
answers HTTP 200, but for a different project: distribution name `hermes-core`, version `0.5.1`,
summary "python bindings for Hermes", author `CossackLabs`, home page `https://cossacklabs.com`, sole
file `hermes_core-0.5.1.tar.gz` uploaded 2017-12-12. That is the CossackLabs Hermes cryptography
library and has nothing to do with this software. A refresh that trusted the 200 would record version
0.5.1 and corrupt the field. This package has never been published to PyPI under its own
distribution name, `hermes_core`, and that is a deliberate project policy rather than an oversight: the Release Process page of the
project's wiki states "This package will not be released to PyPI until it hits version 1.0." With
the latest release at v0.2.0 and nothing released since 2023-03-22, that threshold is nowhere near.
(The wiki is a separate git repository; see Field 24.)

---

### 13. Programming Language (RECOMMENDED)
`Python 3.x`

*Source.* `pyproject.toml` declares `requires-python = ">=3.9"`; GitHub's language breakdown for the
repository reports Python and nothing else; the CI matrix in `.github/workflows/testing.yml` is
`python-version: [3.9, '3.10', '3.11', '3.12', '3.13']`. `Python 2.x` is
excluded by the `>=3.9` floor.

---

### 14. Reference Publication (OPTIONAL)
**Not found — no paper describing this software exists.**

*Source.* `hermes_core/CITATION.rst` states, in its final line, "A paper citation does not yet
exist." That is the project's own explicit statement, and no search route in Field 2's negative
research surfaced a journal article about the package.

**The two AGU/DASH posters were considered for this field and rejected.** Field 14 wants "The DOI for
the publication describing the software, sometimes used as the preferred citation" — the JOSS-paper
role. A conference poster is not that, and the project's own citation guidance disclaims having such a
publication while separately pointing at a (not-yet-existing) software DOI. The posters are recorded
under Field 27, which is where publications that describe a piece of software belong when they are not
its reference publication.

---

### 15. License (RECOMMENDED)
- **License:** `Apache License 2.0`
- **License URI:** `https://spdx.org/licenses/Apache-2.0.html`

**The record held no licence value before this refresh.**

*Evidence.* `licenses/LICENSE.md` at the pin is the 201-line Apache License, Version 2.0 text.
`pyproject.toml` declares `license = {file = "LICENSE.rst"}` and the classifier
`"License :: OSI Approved :: Apache 2.0",`. `Apache License 2.0` is the exact name of the row in
HSSI's live `License` vocabulary.

**Why automated tooling reports NOASSERTION, and why that is wrong.** GitHub's API reports
`{'key': 'other', 'spdx_id': 'NOASSERTION'}` for this repository. The cause is that the top-level
`LICENSE.rst` is a one-line pointer whose entire content is `see licenses/LICENSE.md`; GitHub's
licence classifier reads the top-level file, finds a pointer rather than licence text, and cannot
follow it. The README compounds this by saying "See the license/LICENSE file for more information."
(singular "license", where the directory is `licenses/`). A future refresh that trusts NOASSERTION
will wrongly conclude the licence is unknown.

**The CC0 alternative — considered and rejected, with its evidence.** `README.rst` has a "Public
Domain" section stating that "This project constitutes a work of the United States Government and is
not subject to domestic copyright protection under" 17 USC § 105, that the authors waive copyright
worldwide through the CC0 1.0 Universal public domain dedication, and that "All contributions to this
project will be released under the CC0" dedication. Field 15 holds a single value, and Apache-2.0 is
the right one for three reasons. First, the operative grant a user receives is the licence text the
package ships and the packaging metadata declares — the full Apache-2.0 text in `licenses/LICENSE.md`,
referenced from `pyproject.toml`. Second, the CC0 passage is standard US-Government open-source
boilerplate that describes the *copyright status* of the work and binds *incoming contributions*; it
is not the outbound licence the distribution declares. Third, from the user's side the question Field
15 answers is under what terms a reader may use the software, and the answer a reader must be able to act on is
the one in the LICENSE file. Recorded for completeness: HSSI's licence vocabulary contains no CC0 row
at all, so even a decision to prefer CC0 could not be expressed in this field — it would have to fall
back to `Other`, which would be strictly less informative than the correct Apache-2.0.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- calibration
- cdf
- data analysis
- data container
- heliophysics
- hermes
- nasa
- nasa mission
- plotting
- solar energetic particles
- space weather
- spectra
- time
- validation

Stored lower-case; HSSI's view rendering title-cases them for display, which is a presentation
transform and not the stored value.

*Sources.* Seven come from the PyHC registry entry for this project, which carries
`keywords: ["data_container", "time", "plotting", "spectra", "cdf", "data_analysis", "hermes"]` —
HSSI stores the two underscored ones de-underscored as `data container` and `data analysis`.
`hermes` and `nasa mission` are also declared in `pyproject.toml`'s
`keywords = ["hermes", "nasa mission", "space weather"]`. `nasa` matches the repository's sole GitHub
topic. `heliophysics`, `calibration` and `validation` describe the package's domain and its two
headline operations and were carried in from the earlier extraction; `validation` in particular is
well founded, since ISTP validation is one of the class's four public capabilities.

**Two keywords the record did not carry before this refresh.**

- `space weather` — declared by the project in `pyproject.toml` and never carried into HSSI. The AGU
  poster describes HERMES as a space weather instrument suite, and the framework this package sits on
  is the Space Weather Science Operations Center's. A user searching `space weather` would expect this
  entry.
- `solar energetic particles` — Field 22's controlled vocabulary has no row for SEPs, and Field 22's
  own guidance routes a supported phenomenon with no row into Keywords. The support is real: the AGU
  poster names the "origins of Solar Energetic Particles" among the mysteries HERMES will
  investigate, and `docs/user-guide/cdf_format_guide.rst` describes MERIT as measuring the flux of
  high-energy electrons and ions along the forward and reverse Parker Spiral. Both terms already exist
  as rows in HSSI's keyword vocabulary, so neither addition mints a new row.

**Considered and not added.** `magnetotail` and `solar wind` — both exist as keyword rows, but Field
16 is for keywords "not supported by other metadata fields", and Fields 5 and 22 already carry them.
`istp` — same reasoning; Fields 18 and 19 carry `ISTP-Compliant`. `galactic cosmic rays` — named in
the poster as HERMES science, but there is no such keyword row (nor `cosmic rays`), the repository's
own instrument descriptions do not mention cosmic rays, and minting a row on one poster line is weaker
evidence than the SEP case. `gateway` and `cislunar` — no existing rows and no repository support.

**A negative finding worth keeping.** The PyHC registry propagates domain tags such as `solar`,
`magnetosphere` and `ionosphere_thermosphere_mesosphere` into many project entries, and those tags
routinely arrive in HSSI keyword lists without any basis in the software. **This project's PyHC entry
carries none of them** — its seven keywords are all descriptive of the package. So there is no
propagated-domain-tag contamination to clean up here, and a later refresh need not look for it.

**On `calibration` and `spectra`, which Field 4 treats more strictly.** Keywords are search terms;
function categories are capability claims. `calibration` is retained because the project describes
itself that way and a user searching it will be looking for HERMES calibration tooling; `spectra` is
retained because spectral time series are a first-class part of the container. Neither implies the
Field 4 subcategories that were removed there, and the difference is deliberate rather than an
oversight.

---

### 17. Data Sources (OPTIONAL)
`Observatory/Mission-specific`

*Source and reasoning.* The software reads and writes HERMES science CDF files and nothing else — the
filename convention is `hermes`-prefixed, the instrument identifiers are fixed to "`eea`, `mrt`,
`nem`, `spn`", and the CDF attribute schema encodes HERMES conventions. That is precisely the
"observatory-specific" case, and Field 17's guidance says to cross-list the mission in Related
Observatories, which Field 32 does.

**Considered and rejected:** `S3/Cloud-aware` — the wider HERMES SDC runs on AWS with S3-triggered
pipelines, and this package is installed into that lambda, but no S3 or cloud code exists in this
repository; the cloud behaviour belongs to the separate SDC repositories.
`HTTP/HTTPS Directories`, `FTP/FTPS Directories`, `CDAWeb`, `HAPI` — the package has no network client
of any kind. `CDAWeb` deserves a specific note: the schema derives an ISTP `DISPLAY_TYPE` attribute
explicitly so that "automated software, such as CDAWeb" can display the variable correctly, but that
is the package writing metadata *for* CDAWeb, not reading data *from* it.

---

### 18. Input File Formats (RECOMMENDED)
- `CDF`
- `ISTP-Compliant`

*Source.* `HermesData.load` reads a CDF file and reconstructs the container from it, and the
metadata it expects to find is ISTP-compliant — the class docstring documents `meta` as "The metadata
describing the time series in an ISTP-compliant format". `docs/user-guide/reading_writing_data.rst`
notes that "The CDF C library must be properly installed in order to use this package to save and load
CDF files."

**Considered and rejected.** The package also reads YAML — the two schema files in `hermes_core/data/`
and any user-supplied `global_schema_layers`/`variable_schema_layers` — but those are schema
configuration, not scientific data input, and Field 18 asks for data formats. There is no `Other` value
warranted on that basis.

---

### 19. Output File Formats (RECOMMENDED)
- `CDF`
- `ISTP-Compliant`

*Source.* `HermesData.save` writes a CDF whose filename is derived from the HERMES convention, and
`HermesData.validate` exists specifically to confirm the written file meets ISTP requirements
(`validator = CDFValidator(schema)`). ISTP compliance is the stated purpose of the package's default
schemas.

---

### 20. Operating System (RECOMMENDED)
- `Linux`
- `Mac`
- `Operating System Independent`
- `Windows`

*Source.* `.github/workflows/testing.yml` runs the full test suite on
`platform: [ubuntu-latest, macos-latest, windows-latest]` across five Python versions, which
evidences the three named systems directly; `pyproject.toml` declares the classifier
`"Operating System :: OS Independent"`, which evidences the fourth. The named values and the
independent value are separately sourced rather than redundant, so all four are retained.

*Caveat recorded for users:* the package needs the NASA CDF C library present to read or write files
(via `spacepy.pycdf`), which is a per-platform installation step rather than an operating-system
restriction — the library is available for all three.

---

### 21. CPU Architecture (RECOMMENDED)
`CPU Independent`

*Source.* Pure Python with no compiled extensions of its own — GitHub reports the repository as 100%
Python, and there is no build step beyond `setuptools`. Its compiled dependencies (`spacepy`, `numpy`,
and the CDF C library) provide their own per-architecture builds.

**Considered and rejected:** listing `x86-64` and `Apple Silicon arm64` because CI exercises those
runners. Enumerating specific architectures alongside `CPU Independent` would contradict the
independence claim and would understate the package's portability; CI runner architecture evidences
where it has been tested, not what it requires.

---

### 22. Related Phenomena (OPTIONAL)
`Solar Wind`

Confirmed present in HSSI's live `Phenomena` vocabulary. The vocabulary is flat.

*Evidence.* HERMES's in-situ suite is a solar-wind plasma-and-fields complement, and the repository's
own `docs/user-guide/cdf_format_guide.rst` §2 says so: EEA provides measurements of "low-energy
electrons in the solar wind and in Earth’s deep magnetotail by measuring electron flux as functions
of energy and direction." and SPAN-I measures "Interplanetary and Magnetotail ion flux as functions
of direction and energy/charge from several eV/q to 20 keV/q.", with a time-of-flight section giving
mass/charge discrimination. The package's own global-attribute schema lists "- Plasma and Solar Wind"
among the `Instrument_type` values acceptable for HERMES. `Solar Wind` was added to the Phenomena
vocabulary after the legacy extraction, so this value was not previously available.

**Value removed: Solar Flares.** The record carried it until this refresh. The legacy dossier
admitted its basis: "These are inferred from the
mission's focus" on space weather, from a web search rather than from any source about this software.
HERMES carries no flare-observing instrument — the four instruments are an electron analyser, an
energetic particle telescope, a magnetometer set and an ion analyser, all in situ — and neither the
repository nor the project's poster mentions solar flares anywhere. A user filtering HSSI for
`Solar Flares` is looking for flare software (imagers, X-ray monitors, flare catalogues) and would
find a cislunar CDF container out of place.

**Considered and rejected:** `Coronal Mass Ejections` — the legacy dossier listed it on the same
web-search basis; an in-situ solar wind monitor would encounter ICMEs, but neither the repository nor
the poster claims CME science, and the inference is not evidence. `Geomagnetic Storms`,
`Coronal Heating`, `Solar Corona`, `X-ray emission` — no support of any kind.

**Phenomena with no vocabulary row.** HERMES's stated science includes solar energetic particles and
galactic cosmic ray variability; neither has a Phenomena row, and the vocabulary is closed, so a
custom value would be rejected. Per Field 22's guidance these belong in Keywords, and
`solar energetic particles` has been added there (Field 16).

---

### 23. Development Status (RECOMMENDED)
`Inactive`

**The record held no development status before this refresh.**

*The definitions this is decided against, quoted from HSSI's own `RepoStatus` rows:*

- `Active` :: "The project has reached a stable, usable state and is being actively developed."
- `Inactive` :: "The project has reached a stable, usable state but is no longer being actively developed; support/maintenance will be provided as time allows."
- `Unsupported` :: "The project has reached a stable, usable state but the author(s) have ceased all work on it. A new maintainer may be desired."
- `WIP` :: "Initial development is in progress, but there has not yet been a stable, usable release suitable for the public."
- `Suspended` :: "Initial development has started, but there has not yet been a stable, usable release; work has been stopped for the time being but the author(s) intend on resuming work."
- `Abandoned` :: "Initial development has started, but there has not yet been a stable, usable release; the project has been abandoned and the author(s) do not intend on continuing development."
- `Concept` :: "Minimal or no implementation has been done yet, or the repository is only intended to be a limited example, demo, or proof-of-concept."
- `Moved` :: "The project has been moved to a new location, and the version at that location should be considered authoritative."

*The evidence.* The repository is neither archived nor disabled; its last push is 2026-08-24. Two
public releases exist (v0.1.0 2022-10-05, v0.2.0 2023-03-22) and none since. Commits after `v0.2.0`
number twenty-five in 2023, eleven in 2024, one in 2025 (`7296cc6`, 2025-01-22, "Update Python to 3.13
and RTD Config (#127)") and one in 2026 (`416231f`, 2026-08-24, "Force SWXSOC_MISSION Env Variable &
Reconfigure on Package Import (#128)"). Both recent commits are maintenance. The package's substance
migrated into `swxsoc` in 2024. There is no repostatus badge in the README.

*How the definitions resolve.* `WIP`, `Suspended`, `Abandoned` and `Concept` each turn on there being
no stable, usable public release; two tagged, changelogged, publicly released versions exist, so all
four are excluded by their own opening clause. `Unsupported` requires that the authors "have ceased
all work"; the 2026 commit refutes that. `Moved` requires that the project be at a new location whose
version is authoritative; `hermes_core` has not moved — `swxsoc` is a dependency it configures, and
the HERMES schemas, instrument list and conventions live only here. That leaves `Active` against
`Inactive`, and the discriminator is the clause "is being actively developed": two maintenance commits
in twenty months, no release in three and a half years, and no feature work is not active development,
whereas `Inactive`'s "support/maintenance will be provided as time allows" describes that cadence
exactly.

**The counter-reading, recorded because it is not unreasonable.** One could argue for `WIP` instead,
on the ground that the released versions predate `hermes_core/timedata.py` entirely — no release has
ever contained the data class the entry advertises (Field 12) — and that `pyproject.toml` self-declares
`"Development Status :: 3 - Alpha",`. That reading was not adopted because it requires importing a
requirement the definition does not state: `WIP`'s text asks whether a stable, usable public release
exists, not whether the newest headline feature is in it, and v0.1.0/v0.2.0 were public releases
tested in the HERMES Ground System data flow tests. A user reading "Inactive" learns the accurate
thing — the package is usable and occasionally maintained, but is not under active development —
whereas "Active" would over-promise and "WIP" would understate what has shipped.

---

### 24. Documentation (RECOMMENDED)
`https://hermes-core.readthedocs.io/en/latest/`

*Verification.* The URL serves the current build: the page title is "HERMES Core Documentation" and
its body opens "This is the documentation for the hermes_core Python Package.", matching
`docs/index.rst` at the pin, with the full toctree rendered. `.readthedocs.yml` is present at the pin
(last touched by `7296cc6`, 2025-01-22) and builds Python 3.13. The same URL is what `README.rst`'s
prose link and the PyHC registry's `docs:` field both give.

**Alternatives, and why they are not used.**

- `https://hermes_core.readthedocs.io/en/latest/?badge=latest` — the target of the README's
  `|readthedocs|` badge (`:target: https://hermes_core.readthedocs.io/en/latest/?badge=latest`). This
  URL is **broken and cannot be fixed by us**: an underscore is not valid in a hostname, and the
  request is refused with a Bad Request (400) page rather than reaching any documentation. It is an
  upstream README defect, recorded so that a future refresh recognises it as broken rather than as a
  second valid documentation location.
- `https://github.com/HERMES-SOC/hermes_core/wiki` — the wiki is enabled and **does have content**,
  but it is not user documentation. It holds two pages. `Home.md` is a stub whose entire body is
  "Welcome to the wiki!" followed by a link to the other page. `Release-Process.md` is a real
  procedure page addressed to maintainers — it opens "This page describes the process which should
  used to create an official package release." (the grammatical slip is the source's) and carries
  `## Versioning`, `## Tagging` and `## Building a Release` sections covering semantic versioning,
  how to cut and push a git tag, and how to build a distribution. Field 24 asks for documentation and
  installation instructions for users; release mechanics for maintainers is a different thing, and
  the page has been untouched since 2022-12-15. Two things a later refresh should know before
  re-examining it: the wiki is a **separate git repository**,
  `https://github.com/HERMES-SOC/hermes_core.wiki.git` (HEAD
  `a525974cb551ae633c6a579c50e8f10fcd5df733`), which is not reachable from the code repository's
  pinned tree — so absent from the pinned tree is no evidence whatever about the wiki; and its
  release procedure is the only place this project writes that procedure down, which makes it
  relevant to Field 12 rather than to this field.

---

### 25. Funder (OPTIONAL)
**Not found.**

*Negative research, from the strongest sources available.* The AGU poster behind
`10.5281/zenodo.10257716` — the natural place for an acknowledgements or funding statement — has **no
acknowledgements, funding, grant or award section**: a case-insensitive search of its extracted text
for "acknowledg", "fund", "grant", "award", "NNX", "80NSSC", "80GSFC" and "supported by" returns no
matching passage. Both Zenodo poster records carry `grants: None`, and DataCite reports
`fundingReferences: []` for both the concept and version DOIs of the AGU poster. The repository
contains no `FUNDING` file, no funding statement in `README.rst`, and no funding metadata in
`pyproject.toml`. There is no reference publication whose acknowledgements could be read (Field 14).

*Note on the tempting inference.* Most of the authors are affiliated with NASA GSFC or one of its
contractors (the exception is Tony Mercer, at the Space Sciences Laboratory in Berkeley), and
HERMES is a NASA mission — but an institutional affiliation is not an award, and recording "National
Aeronautics and Space Administration" here would assert funding metadata that no source supplies. The
field is correctly empty.

---

### 26. Award Title (OPTIONAL)
**Not found.** No award title or number appears in any source; see the negative research under Field
25, which covers both fields.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- `https://doi.org/10.5281/zenodo.10257715`
- `https://doi.org/10.5281/zenodo.8400670`

Both are Zenodo **concept** DOIs; each resolves to its single version record. Both are well within the
128-character limit that applies to related-item URLs.

**What they are.**

1. `10.5281/zenodo.10257715` (version `10.5281/zenodo.10257716`) — "HERMES Core and Instrument
   Packages", an AGU Fall Meeting 2023 poster, presentation identifier `SH33E-3097`, published
   2023-12-04, CC-BY-4.0, file `2023 AGU HERMES Packages.pdf`. Its abstract is the source of most of
   this entry's Field 8 description, and its content is a description of this software's architecture
   — the HERMES Data Class, its three data structures, its CDF I/O, its ISTP validation and its place
   in the SWxSOC pipeline.
2. `10.5281/zenodo.8400670` (version `10.5281/zenodo.8400671`) — "The Architecture and Functionality
   of HERMES Core and Instrument Python Packages", a DASH 2023 poster, published 2023-10-09,
   CC-BY-4.0, file `2023_DASH_HERMES_Packages.pptx`. Same eight authors, same abstract.

**Why they belong here rather than in Field 2 or Field 14.** Field 27 is for "Publications that
describe, cite, or use the software", and a conference poster whose entire subject is this package's
architecture is exactly that. Placing them here keeps the material reachable from the HERMES Core page
— a user who wants to understand the design still gets to it in one click — while labelling it
truthfully. It also removes the mislabelling that Field 2 previously carried, without losing anything
the user could previously reach. Field 14 was considered and rejected: the project itself states that
"A paper citation does not yet exist."

**Concept versus version DOI.** The concept DOIs are used because they are stable against any future
re-deposit and because `10.5281/zenodo.10257715` is the string HSSI already held, so continuity is
preserved. The version DOIs (`…10257716`, `…8400671`) are recorded above for anyone who needs to cite
a specific record.

**Three further author-keyed records found and deliberately excluded.** The same Zenodo creator
searches that produced Field 2's negative research also surface
`https://doi.org/10.5281/zenodo.14606063` ("SWxSOC Software Architecture for Science Data
Processing", poster, 2024-12-04) and two separate depositions sharing the title "Enhancing SWxSOC
through Open Collaboration for Multi-Mission Data Processing and Expedited Release" —
`https://doi.org/10.5281/zenodo.14536415` (poster, 2024-12-09) and
`https://doi.org/10.5281/zenodo.18600752` (presentation, 2025-12-17), which have distinct concept
DOIs and so are separate depositions rather than versions of one another. **None of the three is
about this software.** Each describes SWxSOC as a multi-mission Science Operations Center and names
HERMES only as one of the missions it supports; none mentions `hermes_core`. They belong to the
SWxSOC catalogue entry, not to this one. Recorded so a later refresh running the same author-keyed
protocol recognises them as already assessed rather than as new candidates.

---

### 28. Related Datasets (OPTIONAL)
**Not found — and this is a substantive finding, not an unexamined gap.**

There are no HERMES science data products to relate. The instrument suite is designed to fly on the
exterior of the Artemis Lunar Gateway's HALO module, and the project's own AGU poster describes the
suite in the future tense as one "that will attach to the exterior of the Gateway Habitation And
Logistics Outpost (HALO) of the Artemis Lunar Gateway." (that poster is laid out in columns, so its
sentences are not contiguous in a plain text extraction — reconstruct the column before checking a
quotation against it). The only science data file in the repository is synthetic:
`hermes_core/data/sample/hermes_nem_default_l1_20160322T123031_v0.0.1.cdf`, which
`hermes_core/data/sample/README.rst` describes as generated by the tutorial code. No dataset DOI or
hpde.io landing page for HERMES data was found, and none should be expected before the mission
returns data.

---

### 29. Related Software (OPTIONAL)
- `https://github.com/swxsoc/swxsoc`
- `https://github.com/spacepy/spacepy`

**The standard applied here.** Field 29 lists software that is *distinguishing* — a predecessor or
parent project, a similar-purpose tool, a companion, or a domain-specific dependency important enough
that a user needs to know about it to understand or install this package. The generic
scientific-Python and tooling stack is excluded by rule, without exception and regardless of how
central it is to the code.

**Why each entry is here.**

- **swxsoc** — the single most distinguishing fact about this package. It is not merely a dependency;
  `hermes_core` *is* a HERMES configuration of it. `pyproject.toml` lists
  `'swxsoc @ git+https://github.com/swxsoc/swxsoc.git@main',` first; `HermesData` subclasses
  `SWXData`; `HermesDataSchema` subclasses `SWXSchema`; the two public utility functions are
  pass-throughs to `swxsoc.util.util`; `HermesData.validate` runs swxsoc's `CDFValidator`; and
  `hermes_core/__init__.py` sets the mission environment variable and calls `swxsoc.reconfigure()`.
  A reader who does not know this cannot understand what this package contains. SWxSOC is itself a
  catalogue entry, so the association is navigable in both directions.
- **spacepy** — the CDF read/write engine, and a hard practical consequence for anyone installing this
  package. `docs/user-guide/reading_writing_data.rst` states "The
  :py:class:`~hermes_core.timedata.HermesData` class writes CDF files using the `~spacepy.pycdf`
  module." and the same page warns that "The CDF C library must be properly installed in order to use
  this package to save and load CDF files." A user who does not know spacepy is involved will not
  understand why an unrelated C library is a prerequisite. It is a heliophysics-domain package, so the
  generic-infrastructure exclusion does not reach it, and it is a catalogue entry in its own right.

**How the link is expressed, and the alternative rejected.** Repository URLs are used rather than DOIs
even though the form nominally prefers a DOI. The decisive fact is user-facing: HSSI renders a related
item's URL as its own link text, so a visitor to the HERMES Core page reading
`https://doi.org/10.5281/zenodo.15546486` — which is what the record previously held for swxsoc —
cannot tell that it points at SWxSOC, the one thing they need to know. `https://github.com/swxsoc/swxsoc`
reads as itself. (Related-item display names are internal placeholders and are not what this argument
rests on; the rendered identifier is.) The rejected alternative is worth keeping on file:
`https://doi.org/10.5281/zenodo.15546486` is a genuine software concept DOI for swxsoc — typed
`resourceTypeGeneral` `Software` with `IsSupplementTo` `https://github.com/swxsoc/swxsoc/tree/0.2.3`
— and it is the persistent identifier carried by SWxSOC's own catalogue entry. Re-open this choice
only if HSSI starts rendering a resolved title instead of the raw URL, at which point the DOI becomes
the better option on persistence grounds.

**Excluded, by the same standard.**

- **numpy** and **PyYAML** — declared dependencies (`'numpy>=1.18.0',`, `'pyyaml>=5.3.1',`), excluded
  as generic scientific-Python and tooling infrastructure. This is the rule applied, not a preference:
  they would be equally at home in a web application, a finance model or a biology pipeline, and
  listing them would say nothing that is not equally true of most of the ecosystem. The same applies
  to matplotlib, which the plotting path uses without being declared.
- **astropy** and **ndcube** — both are recorded in Field 30 instead, where their relationship (their
  objects crossing this package's public API in both directions) is precisely what that field asks
  for. Listing them in both fields would duplicate one relationship under two headings without telling
  a user anything new.
- **sunpy** — declared in `pyproject.toml` as `'sunpy>=5.0.1',`, and the qualifying evidence is
  recorded here in full so it is clear this was rejected on principle rather than for want of
  evidence: the package template is derived from one developed jointly by the OpenAstronomy
  community and the SunPy Project (`README.rst`, Acknowledgements) — the credit is shared, which if
  anything weakens the sunpy association rather than supporting it;
  `hermes_core/util/exceptions.py` states it "is based on that provided by SunPy", and swxsoc's
  plotting helpers are annotated "Code courtesy of sunpy". Against that, `hermes_core` **does not
  import sunpy anywhere** in the pinned tree — no `import sunpy` statement exists in it. The name does
  occur in prose and packaging (the acknowledgement, the changelog, `licenses/SUNPY.rst`, the Sphinx
  intersphinx map and the `'sunpy>=5.0.1',` requirement), and inside the `hermes_core` package itself
  the sole occurrence is a docstring reference link,
  `* `Sunpy NDCube and NDCollection <https://docs.sunpy.org/projects/ndcube/en/stable/>`_`, which
  points at ndcube's documentation, hosted under the sunpy domain. From the user's side, a
  reader on the sunpy entry who found a cislunar in-situ CDF container under Related Software would
  find it out of place, and a reader on this entry would reasonably infer solar-physics capability
  that does not exist. What would reopen it: `hermes_core` importing sunpy, or exchanging a sunpy
  object across its API.

---

### 30. Interoperable Software (OPTIONAL)
- `https://github.com/astropy/astropy`
- `https://github.com/sunpy/ndcube`

**The standard applied here.** Field 30 asks which peer tools this software demonstrably exchanges
data with — a shared or converted data model, output from one imported into the other, an adapter API.
Being a dependency is never sufficient. For a foundational-but-domain-adjacent package such as
astropy, a specific exchange must be documented in the public API, docs, examples or tests; "used
internally" does not qualify. On top of the evidence bar, the entry must tell a user something
distinctive about *this* software.

**Why each entry is here.**

- **ndcube** — the exchange is the package's public constructor contract.
  `HermesData.__init__` takes `spectra: Optional[ndcube.NDCollection] = None,`; the class docstring's
  References section links "* `Sunpy NDCube and NDCollection <https://docs.sunpy.org/projects/ndcube/en/stable/>`_";
  the user guide has a section titled "Creating a ``NDCollection`` for ``HermesData`` `spectra`"; the
  tutorial's own comment reads "# Create high-dimensional data leveraging the API of NDCube"; and
  `HermesData.spectra` hands `NDCube` objects back for the user to slice and plot with ndcube's own
  API. The AGU poster states the same design, listing `.spectra` as `ndcube.NDCollection`. This is a
  genuine bidirectional exchange between peer tools that a user deliberately combines, and it tells a
  reader the concrete, non-obvious fact that ndcube is the spectral data model for HERMES CDF files.
- **astropy** — astropy is a Tier B package, admitted here only because the evidence bar is cleared
  decisively rather than because it is a dependency. Its types *are* this package's public interface:
  `HermesData.__init__` takes
  `timeseries: Union[astropy.timeseries.TimeSeries, dict[str, astropy.timeseries.TimeSeries]]` and
  `support: Optional[dict[Union[astropy.units.Quantity, astropy.nddata.NDData]]]`; the class
  docstring's References list the Astropy TimeSeries, Quantity, Time and NDData documentation; the
  user guide states that the data are stored in an `astropy.timeseries.TimeSeries` table and that
  astropy time and unit objects are required by the class; and the AGU poster's data-type table
  attributes `.timeseries` and `.support` to Astropy. **The test that decided it was the searcher's,
  not the evidence bar:** for most packages an astropy association is uninformative, but this
  package is *nothing but* a data container, so the astropy exchange is not an implementation detail —
  it is the product. Reading it, a user learns immediately that their existing astropy workflow
  applies to HERMES CDF data without conversion.

**Excluded, by the same standard.**

- **swxsoc** — removed from this field, and recorded in Field 29 instead. The field's own framing
  presupposes peer tools a user deliberately combines, and there is nothing to combine here: a
  `HermesData` object *is* a `SWXData` object, and swxsoc is installed unavoidably with this package.
  Under the Related Software heading that relationship reads as a statement of what the package is
  built on, which is true and useful; under Interoperable Software it would read as a choice a user
  could make, which it is not. The record previously carried the same single URL under both headings,
  telling a reader the same thing twice.
- **spacepy** — recorded in Field 29 rather than here. Its role is real but internal: `spacepy.pycdf`
  is used inside the CDF handler, and no spacepy object crosses this package's public API in either
  direction. That is the used-internally case the evidence bar excludes: the contrast the rule draws
  is between a documented interchange type and internal use, and this is the latter.
- **sunpy** — no sunpy object crosses the API and the package does not import it; see Field 29 for the
  full evidence and the reason it was rejected.
- **numpy**, **PyYAML**, **matplotlib** — generic infrastructure, excluded by rule with no exception.
  A blanket appeal to PyHC membership or to "the standard scientific Python ecosystem" would not
  rescue them, and neither is offered here for anything.

---

### 31. Related Instruments (OPTIONAL)
**None recorded — an evidenced omission, not an unexamined gap.**

**The software does support four specific instruments.** They are named in the pinned tree.
`hermes_core/timedata.py` documents the instrument argument as 'The instrument name. Must be "eea",
"nemisis", "merit" or "spani".' and `hermes_core/util/util.py` documents it as 'The instrument name.
Must be one of the following "eea", "nemesis", "merit", "spani"' — note that the second file spells
the magnetometer *nemesis*; commit `793f7a0` (2024-06-04) renamed its short name from `MAG`/`nms` to
`NEM`/`nem`. The schema's `Descriptor` whitelist gives the full names, including
"- SPAN-I>Solar Probe Analyzer for Ions", and `docs/user-guide/cdf_format_guide.rst` §2 describes each
instrument's measurement and names its instrument team and PI. Expanded, they are the Electron
Electrostatic Analyzer (EEA), the Noise Eliminating Magnetometer In a Small Integrated System
(NEMISIS), the Miniaturized Electron pRoton Telescope (MERiT) and the Solar Probe Analyzer for Ions
(SPAN-I).

**None of them can be recorded, because none is registered in SPASE.** Field 31 accepts only entries
carrying an `https://spase-metadata.org/` identifier; a bare name would mint a new identifier-less row
in HSSI's vocabulary. Both ends were checked:

- In HSSI's instrument/observatory vocabulary — which is entirely SPASE-backed, with no row failing the
  `https://spase-metadata.org/` guard — no instrument row carries EEA, MERIT, MERiT, NEMISIS, NEMESIS,
  SPAN-I, Gateway or HALO in its name, abbreviation or identifier. Searching the instruments' expanded
  names finds nothing belonging to HERMES either. The sole row whose name, abbreviation or identifier
  contains "HERMES" is the observatory, recorded under Field 32.
- Upstream, `https://spase-metadata.org/SMWG/Observatory/HERMES` resolves, but
  `…/SMWG/Instrument/HERMES`, `…/SMWG/Instrument/HERMES/EEA`, `…/SMWG/Instrument/HERMES/NEMISIS`,
  `…/SMWG/Instrument/HERMES/MERiT` and `…/SMWG/Instrument/HERMES/SPAN-I` all return 404. The
  instruments are not registered.

Per the SPASE resolution ladder, a supported instrument with no instrument record associates at the
observatory level instead — which Field 32 does — and the entry here is omitted with this note rather
than invented.

**What would fill this field:** SPASE registering HERMES instrument records, after which a refresh
should add the four rows here and cite this note as the reason they were previously absent.

**Two name collisions that will mislead a careless search.** Neither is admissible.

- `SPAN-A`, `SPAN-B` (`https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/SWEAP/SPAN-A`
  and `…/SPAN-B`) and the CNES rows named "Solar Probe Analyser" with abbreviation `SPAN`
  (`https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/PSP/SPI` and
  `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/PSP/SPE` — note the `CNES/Instrument/` path
  segment, without which the identifier does not resolve) all belong to **Parker Solar Probe's SWEAP
  suite**,
  not to HERMES. HERMES's SPAN-I is a separate instrument that inherits the PSP design heritage; the
  SPASE rows are PSP's.
- Searching for "Artemis", because the poster places HERMES on the "Artemis Lunar Gateway", returns
  the **ARTEMIS** mission rows (`https://spase-metadata.org/SMWG/Observatory/ARTEMIS` and the CNES
  ARTEMIS-P1/P2 rows) — the two repurposed THEMIS spacecraft in lunar orbit. The HSSI vocabulary row
  for that observatory is named "Acceleration, Reconnection, Turbulence, Electrodynamics of the Moon’s Interaction with the Sun",
  quoted from the row rather than from upstream because the two differ: the SPASE page's own prose
  writes "Turbulence, and Electrodynamics" where the row has no "and". A future agent checking this
  name against the SPASE page will meet that one-word difference and should treat it as a known
  upstream/vocabulary divergence rather than a transcription defect, and should keep matching on the
  row's form, which is what a vocabulary search returns. Either way these rows are unrelated to the
  Artemis human exploration programme and must not be associated with this software.

---

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** `Heliophysics Environmental and Radiation Measurement Experiment Suite`
- **Observatory Identifier:** `https://spase-metadata.org/SMWG/Observatory/HERMES`

*Resolution.* Exactly one observatory row matches; its name is copied verbatim from that row and its
abbreviation there is `HERMES`. The identifier resolves upstream.

*Relevance.* This is the clearest possible designed-to-support case: the package hard-codes the
mission (`os.environ["SWXSOC_MISSION"] = "hermes"`), validates instrument names against the HERMES
whitelist, implements the HERMES filename convention, and ships the HERMES CDF attribute schemas. A
user searching HSSI for HERMES software should find this first.

**Considered and rejected: a `Gateway` entry.** The legacy dossier proposed adding "Gateway", since
HERMES is a payload on the exterior of the Artemis Lunar Gateway's HALO module. There is **no SPASE
row for Gateway or HALO** — neither `https://spase-metadata.org/SMWG/Observatory/Gateway` nor
`…/Observatory/HALO` resolves, and no row in HSSI's vocabulary carries either term — so the entry is
not admissible regardless of how the relevance question is answered. A bare "Gateway" name would mint
an identifier-less row. Even if a row existed, the association would be weak: this package supports
HERMES's data products, not the Gateway platform's. See Field 31 for the ARTEMIS collision that a
"Gateway"/"Artemis" search will surface.

---

### 33. Logo (OPTIONAL)
`https://raw.githubusercontent.com/HERMES-SOC/hermes_core/416231f5982f53d03ad04b206e33e8018b856792/docs/logo/hermes_logo.png`

*Verification.* The URL serves image bytes — content type `image/png`, 74,584 bytes, a 547×547 8-bit
RGBA PNG — with sha256 `50e1fcd7ac335fef85c4011ab1584ef21a1270ccfd2d28dd449045a922143783`, which is
byte-identical to the `docs/logo/hermes_logo.png` blob in the pinned tree. The whole URL is 123
characters, inside the 200-character column limit.

*Form.* It is a raw-content URL pinned to a 40-hex commit SHA, with no branch name and no `blob/`
segment. The asset is not Git-LFS-tracked, so `raw.githubusercontent.com` returns real bytes rather
than a pointer. The image is the project's own logo, carried in the repository's `docs/logo/`
directory; `CHANGELOG.rst`'s 0.2.0 entry records it being added to the documentation in that
release, alongside updated theme colors and a favicon. **This value has already been reviewed and
approved; the question of whether the image reads as a logo for this software is settled and should
not be reopened.**

*Recorded for a future refresh:* the PyHC registry gives this project's logo as
`logo: "https://raw.githubusercontent.com/HERMES-SOC/hermes_core/main/docs/logo/hermes_logo.png"` —
the mutable `main` form. That URL served the same image as the pinned one when this dossier was
written, but it would break silently if the file were renamed, moved or deleted, and it would change
silently if the logo were redesigned. The pinned form above is preferred deliberately: a logo change
should reach the catalogue through a refresh that re-derives and re-verifies the value, not through a
moving reference. Do not "update"
this value to the registry's branch URL.
