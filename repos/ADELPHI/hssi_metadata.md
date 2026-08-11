# HSSI Metadata Extraction Results

**HSSI Software ID:** Not applicable — new submission, no existing HSSI record
**Repository:** https://ccmc.gsfc.nasa.gov/models/ADELPHI~1/ (CCMC model page — authoritative source; ADELPHI has no source-code repository)
**Source Revision:** Not applicable — website-only extraction, no version-controlled source is published. The CCMC model page carries its own "Last Updated: 08/10/2026" stamp, which is the closest available analogue to a pinned revision.
**Extraction Date:** 2026-08-11
**Validation Date:** Pending
**Validation Status:** Pending

---

**Scope note — this evidence is website-only.** ADELPHI is an IDL model hosted by NASA's Community
Coordinated Modeling Center (CCMC). No source repository is published in any of the places searched:
GitHub (both repository and code search), GitLab, Zenodo, DataCite and the NASA Software Catalog were
each queried, and none returned an ADELPHI source repository. Every value below therefore derives from
the CCMC model records, the peer-reviewed literature, SPASE, ORCID, ROR, Crossref, or NASA's Kamodo
package (which contains a dedicated ADELPHI reader). There is no README, CITATION.cff, LICENSE, package manifest, CI configuration or commit
history to draw on, so several fields that a repository-backed extraction would fill are correctly
empty here rather than merely unresearched. Read each "Not found" as a documented omission with the
negative research recorded, not as a gap awaiting a guess.

**How CCMC publishes this metadata, and which record holds what.** Beyond the rendered prose, CCMC
serves two *different* structured records for ADELPHI, and they are not interchangeable — an agent that
looks for a field in the wrong one will wrongly conclude it is unset:

- The **individual model page** (`/models/ADELPHI~1/`) carries the descriptive and operational detail:
  `name`, `fullName`, `version`, `domains`, `regions`, `phenomena`, `code.languages`, typed `contacts`
  with roles and email addresses, `accessInformation`, `publications`, `changeLog`,
  `publicationPolicy`, `figures`, `temporalDependence`, and separate `inputsDescription` /
  `outputsDescription` / `caveats` text. It does **not** carry `status`, `spaseResourceID` or `host`.
- The **model catalogue listing** (`/models/`) carries the cataloguing fields — `status`,
  `spaseResourceID`, `host` and `services` — alongside a shared core of `name`, `fullName`, `version`,
  `domains` and `phenomena`. It does **not** carry `contacts`, `code`, `changeLog`, `regions`,
  `caveats`, `figures`, `publicationPolicy` or the input/output descriptions.

Where a note below attributes a value to "the CCMC model record" it means the individual model page;
where it says "the catalogue record" it means the listing. Both are structured data rather than a
reading of the rendered page.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Placeholder. MANDATORY at submission time; not derivable from the source material.*

### 2. Persistent Identifier (RECOMMENDED)
**Not found** — ADELPHI has no DOI.

Negative research, so a future agent need not repeat it — but note carefully how the searches were
scoped, because the scoping matters:

- **Zenodo returns zero records for ADELPHI in combination with AMPERE.** The AMPERE qualifier is
  necessary rather than incidental: "ADELPHI" is a heavily overloaded string, and an unqualified query
  returns hundreds of irrelevant hits (Adelphi University, an Adelphi consultancy, "Edizione Adelphi"
  book reviews) with no way to spot a heliophysics record among them. Adding AMPERE is what makes the
  result readable. The cost of that filter is real and is recorded here: it excludes the archived
  ADELPHI **output** dataset now listed in Field 28, whose Zenodo metadata never mentions AMPERE. That
  is not a contradiction — see the next paragraph.
- **DataCite** returns only a University of Maryland text record (`10.13016/m28iyi-tcv3`, Shim,
  Robinson, Garcia-Sage et al., on the Geospace Dynamics Constellation), which cites the model rather
  than being the model.

**A dataset DOI is not a software DOI, so Field 28 and this field are not in tension.** Field 28 now
records a Zenodo DOI for an archive of ADELPHI's model *output*. That DOI identifies a deposited data
product; it does not identify, version or make citable the ADELPHI software itself, and Field 2 asks
for a persistent identifier for the software. This is the same distinction already applied to the
Maryland record above: a resource that involves ADELPHI is not thereby an identifier for ADELPHI.
No software DOI, no Zenodo concept DOI for the code, and no DOI badge exists, because there is no
repository or software deposit to attach one to.

CCMC does assign the model an internal SPASE Resource ID, `spase://CCMC/SimulationModel/ADELPHI/1`,
carried in its catalogue record. This is deliberately **not** recorded as the Persistent Identifier:
it is not a DOI, HSSI's field is a DataCite DOI lookup, and the identifier does not resolve —
`https://spase-metadata.org/CCMC/SimulationModel/ADELPHI/1` returns 404, so CCMC's SimulationModel
namespace is not published to the SPASE registry. It is documented here because it is the only
persistent identifier CCMC assigns to the model itself, and a future agent may want it if CCMC ever
publishes that namespace or mints a DOI.

### 3. Code Repository (MANDATORY)
https://ccmc.gsfc.nasa.gov/models/ADELPHI~1/

The CCMC model page is the correct value. Field 3's own instruction — "If the software is
restricted, put a link to where a potential user could request access" — covers exactly this case:
ADELPHI's source is not distributed, and this page is where a user learns about the model, finds the
developer's contact address, and reaches the run service.

Alternatives considered and rejected: the Instant Run interface
(`https://kauai.ccmc.gsfc.nasa.gov/instantrun/adelphi/`) is a bare submission form with no model
description, no contacts and no version information, so it is a poorer landing page and is recorded
under Field 24 context instead; and no Git host URL was invented, since none exists (see the scope
note).

### 4. Software Functionality (MANDATORY)
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Physics-Based
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Processing

All seven confirmed against the live `FunctionCategory` vocabulary. Each subcategory is listed with
its parent, as the taxonomy requires.

Justification per value:

- **Data Guided** — ADELPHI is driven entirely by observational input. Its sole forcing is the measured
  AMPERE field-aligned current map; it has no solar-wind driver and no free-running dynamics.
- **Empirical** — the Hall and Pedersen conductances are not computed from first principles but read
  off statistical relations between field-aligned current density and auroral conductance, fitted from
  coincident AMPERE and Poker Flat Incoherent Scatter Radar data (Robinson et al. 2020,
  `10.1029/2020JA028008`). The precipitating-electron energy-flux relation is likewise a binned
  empirical fit (Robinson et al. 2018, `10.1029/2018GL078718`).
- **Physics-Based** — on top of those empirical relations the model solves the current continuity
  equation under steady-state conditions for the electric potential, then applies Ohm's law to obtain
  the perpendicular electric field and height-integrated horizontal currents. That is genuine physics,
  which is why `Physics-Based` (the broader category) is selected rather than `First Principles`: the
  model is semi-empirical, not an ab initio calculation.
- **Analysis** and **Processing** — the code ingests AMPERE netCDF field-aligned current files, walks a
  multi-day file list, and derives physical quantities (electric field, current intensity, Joule
  heating rate, particle energy flux) plus integrated indices (cross polar cap potential, hemispheric
  power, a modeled auroral electrojet index).

Considered and deliberately **not** selected:

- **Data Processing and Analysis: Data Assimilation** — rejected, and worth recording because the name
  invites the error. ADELPHI is frequently discussed alongside AMIE (Assimilative Mapping of
  Ionospheric Electrodynamics) and its acronym has been mis-expanded as "Assimilative …". It is
  neither. There is no assimilation scheme — no Kalman filter, no variational minimisation, no
  background state blended with observations. The model performs a direct derivation from a single
  observational input through fixed empirical relations. Its own peer, AMGeO, *is* assimilative;
  ADELPHI is not.
- **Data Visualization** (and its subcategories) — rejected. The CCMC Instant Run form advertises
  "output plots Cross Polar Cap Potential (kV), Hall Conductance, Pedersen Conductance", but those
  figures are produced by CCMC's Instant Run service layer, which is shared infrastructure across many
  CCMC models. CCMC's own description of ADELPHI's outputs is data files only ("Adelphi writes 1D and
  2D outputs to file"), and its `code` record lists only the language. Nothing attributes plotting to
  the ADELPHI code itself. If the IDL source is ever released and contains plotting routines, this
  should be revisited.
- **Coordinate Transforms: Ionospheric** — rejected. ADELPHI works natively on a magnetic local
  time / magnetic latitude grid, and its AMPERE input already arrives in magnetic coordinates, so no
  transformation is needed and none is documented as a user-facing capability. The source is
  unavailable, so this rests on CCMC's input and output descriptions rather than on reading the code.
  (Kamodo's reader labels ADELPHI output as `SM` spherical coordinates, but that is Kamodo describing
  the grid it received, not ADELPHI offering a transform.)
- **Models and Simulations: Forecasting** — rejected. ADELPHI specifies conditions from measurements
  already taken; it makes no prediction. The Instant Run service accepts only past dates.
- **Data Processing and Analysis: Time Series Analysis** — rejected. The 1D outputs are time series at
  2-minute cadence, but the model *produces* them; it does not analyse time series.
- **Mission-related** — rejected. ADELPHI consumes a mission's data product but is not part of any
  mission ground system, pipeline or operations chain.

### 5. Related Region (MANDATORY)
- Earth Ionosphere
- Earth Auroral Subregion
- Earth Magnetosphere

All three confirmed against the live 24-row `Region` vocabulary.

`Earth Ionosphere` and `Earth Auroral Subregion` are the specific regions the model resolves: CCMC
classifies ADELPHI's domain as "High Latitude Ionosphere / Auroral Region", and its principal output
quantities are ionospheric ones (conductance, potential, height-integrated current, Joule heating,
precipitating energy flux) on a 40–89 degree magnetic latitude grid. `Earth Magnetosphere` is included because the
field-aligned currents that drive the model are the magnetosphere-ionosphere coupling currents; CCMC's
structured record lists the model's region as "Earth / Magnetosphere", and the SPASE record for AMPERE
gives its `ObservatoryRegion` as `Earth.Magnetosphere`.

`Earth Thermosphere` was considered and rejected: ADELPHI computes the Joule heating rate that is
deposited into the thermosphere, but it does not model the thermosphere, carries no neutral atmosphere,
and Robinson et al. 2021 cites unmodelled neutral winds as a known error source. The broader
`Earth Atmosphere` was rejected in favour of the specific regions above.

### 6. Authors (MANDATORY)

**Author 1**
- **Name:** Robert Robinson
- **Author Identifier:** https://orcid.org/0000-0002-7750-8326
- **Affiliation:**
  - **Organization:** Catholic University of America
  - **Affiliation Identifier:** https://ror.org/047yk3s18

Sole author. CCMC's structured contact record designates exactly one person as **Model Developer**:
Robert Robinson, "Catholic University of America (CUA), Department of Physics", `robinsonr@cua.edu`.

The ORCID is confirmed rather than inferred. Crossref lists `0000-0002-7750-8326` for R. M. Robinson
as first author on all three ADELPHI reference papers, and that ORCID's own employment record gives
Catholic University of America, department "Physics", Washington DC, role Research Associate
Professor, from 2015-04 with no end date. Name, institution, department and active tenure all agree
with CCMC, so the identity is unambiguous.

The affiliation is recorded as the ROR-matched institution name `Catholic University of America`
(https://ror.org/047yk3s18, whose ROR aliases include the acronym "CUA"). CCMC's acronym-bearing string
"Catholic University of America (CUA), Department of Physics" is deliberately not copied verbatim:
Field 6 asks for the complete organization name without acronyms, and ROR has no separate row for the
Department of Physics.

**CCMC model hosts are deliberately excluded, and this is the reasoning a future agent should not have
to redo.** CCMC's contact record types its people by role, and it distinguishes `Model Developer` from
`CCMC Model Host`. The two hosts are Reza Janalizadeh Choobbasti (CCMC/GSFC/NASA,
`reza.janalizadehchoobbasti@nasa.gov`) and Jia Yue (NASA/GSFC, `jia.yue@nasa.gov`). A CCMC model host
onboards a community model into CCMC's infrastructure and operates the hosted run service; that is
stewardship of a deployment, not authorship of the software. HSSI Field 6 asks specifically for "the
author(s) of this software", and neither host appears as an author on any of the three ADELPHI papers
nor is credited with writing the IDL code. They are recorded here so their names and affiliations are
preserved as operational contacts, not promoted to authors.

**Reference-publication co-authors are also excluded.** Robinson et al. 2021 additionally credits Larry
Zanetti, Brian Anderson (https://orcid.org/0000-0003-2543-0149), Sarah Vines
(https://orcid.org/0000-0002-7515-3285) and Jesper Gjerloev (https://orcid.org/0000-0002-7277-9004),
all of Johns Hopkins University Applied Physics Laboratory; the 2020 and 2018 papers add Stephen
Kaeppler (https://orcid.org/0000-0003-1932-0330, Clemson University), Haje Korth
(https://orcid.org/0000-0001-7394-7439), Yongliang Zhang (https://orcid.org/0000-0003-4851-1662) and
Anna Fitzmaurice. These are co-authors of the science papers — several of them the AMPERE team who
supplied the input data — not documented authors of the model code. With no CITATION.cff, no code
headers and no author list of any kind in the software itself, CCMC's single Model Developer
designation is the only authoritative statement of software authorship available, and it is followed.
Their ORCIDs are recorded above so that, should CCMC or Robinson later confirm broader code
authorship, the identifiers do not have to be re-resolved.

### 7. Software Name (MANDATORY)
ADELPHI

From CCMC's structured record, whose `name` field is exactly `ADELPHI`. The page title and catalogue
`title` are both "ADELPHI 1", but the trailing 1 is the version, carried separately in the `version`
field and recorded in Field 12; it is not part of the name. The expanded form belongs in the
description (Field 8), not here.

### 8. Description (MANDATORY)
ADELPHI (AMPERE-Derived Electrodynamic Properties of the High-latitude Ionosphere) is an IDL model that specifies storm-time high-latitude ionospheric electrodynamics from spaceborne field-aligned current measurements alone. It ingests gridded field-aligned current maps from the Active Magnetosphere and Planetary Electrodynamics Response Experiment (AMPERE) and estimates Hall and Pedersen conductances using empirical relations between field-aligned current density and auroral conductance derived from coincident AMPERE and Poker Flat Incoherent Scatter Radar observations. Combining those conductances with the measured currents, ADELPHI solves the current continuity equation under steady-state conditions for the ionospheric electric potential, then derives the perpendicular electric field, the height-integrated horizontal current density, the precipitating particle energy flux, and the Joule heating rate. Two-dimensional output is produced on a grid of 1-hour magnetic local time by 1-degree magnetic latitude, spanning 40 to 89 degrees in both hemispheres at 2-minute cadence over 24-hour periods; one-dimensional output includes the cross polar cap potential, hemispherically integrated energy flux and Joule heating, and a modeled auroral electrojet index. Because the conductance relations were derived at a single geographic location and the continuity equation is solved assuming steady state, the results are most reliable for large-scale storm-time structure and may not capture small-scale substorm current systems or the effects of neutral winds. ADELPHI is hosted by NASA's Community Coordinated Modeling Center and can be run through the CCMC Instant Run service; the source code is not publicly distributed.

Composed from primary sources rather than copied from any one: the CCMC record supplies the model's
purpose, grid, cadence and caveats; Robinson et al. 2021 supplies the solution method and the stated
error sources; Robinson et al. 2020 supplies the provenance of the conductance relations. The acronym
is expanded on first use (see the note under Field 9 for which expansion was chosen and why), and the
final sentence records the access model, since a reader deciding whether ADELPHI is useful to them
needs to know up front that only a hosted run service is available.

### 9. Concise Description (OPTIONAL)
Derives storm-time high-latitude ionospheric electrodynamics — electric potential, fields, currents, Joule heating and particle energy flux — from AMPERE field-aligned current measurements.

189 characters, within the 200-character limit. Supplied because the first 200 characters of Field 8
would otherwise cut off mid-sentence inside the acronym expansion, which makes a poor preview.

**On the acronym expansion — three variants are attested, and this is the one to use.** A future agent
will encounter all three and should not "correct" the chosen form:

1. **"AMPERE-Derived Electrodynamic Properties of the High-latitude Ionosphere"** — *selected*. This is
   the `fullName` in CCMC's own structured model record and the text of the page's meta description.
   CCMC is the authoritative publisher of this software entry, so its form governs. It is
   independently corroborated by Ringuette et al. 2022 (`10.3389/fspas.2022.1005977`), which writes
   "ADELPHI (AMPERE-Derive ELectrodynamic Properties of the High-latitude Ionosphere model, Robinson
   et al., 2021)" — the same wording, with an obvious dropped "d" typo in "Derive".
2. "AMPERE-Derived Electrodynamic **Parameters** of the **High Latitude** Ionosphere" — the title of
   Robinson et al.'s EGU 2019 abstract (ADS bibcode `2019EGUGA..21.3577R`). Attested and from the
   developer himself, but predates the CCMC deployment.
3. "AMPERE Derived **Electrodynamics of the High Latitude Ionosphere**" — as written in Sur et al. 2025
   (`10.1029/2024SW004023`).

Note also that no expansion appears in the rendered body text of the CCMC page; it is carried only in
the structured `fullName` field and the HTML meta description, which is why a casual read of the page
finds the acronym undefined.

### 10. Publication Date (RECOMMENDED)
2025-07-16

The date ADELPHI was published as software — that is, first made available to the community. CCMC's
change log carries a single ADELPHI entry, categorised "Instant Runs / New Feature" and dated
2025-07-16: "The ADELPHI (web simulator) is available to the community through the CCMC instant run
(IR) service via this submission URL."

Alternative considered and rejected: 2021-03-17, the publication date of the Robinson et al. 2021
reference paper. That is when the model was *described* in the literature, and it is recorded under
Field 14, but the software itself was not obtainable by anyone until the CCMC deployment four years
later. Field 10 asks for the date of first publication of the software, so the CCMC availability date
is the accurate answer. The model page's "Last Updated: 08/10/2026" was also rejected — it is a
content-management timestamp for the web page, and is one day before this extraction, so it plainly
tracks page edits rather than the software.

### 11. Publisher (RECOMMENDED)
- **Organization:** Community Coordinated Modeling Center
- **Publisher Identifier:** https://ror.org/01dy3j343

Field 11 instructs that where no DOI has been obtained, the publisher is the host that makes the
software available. That host is CCMC, which is the sole distributor of ADELPHI and which the
catalogue record identifies with `host: "CCMC"`. The ROR is an exact name match for the Community
Coordinated Modeling Center.

Considered: the parent organizations, Goddard Space Flight Center (https://ror.org/0171mag52) and the
National Aeronautics and Space Administration (https://ror.org/027ka1x80). Both were rejected as less
precise — CCMC has its own ROR and is the actual publishing entity — but they are recorded here in case
a curator prefers the agency-level attribution.

### 12. Version (RECOMMENDED)
- **Version Number:** 1
- **Version Date:** 2025-07-16
- **Version Description:** Not found
- **Version PID:** Not found

The version number is CCMC's `version` field, verbatim: the string `1`, not `v1` or `1.0`. The version
date is the CCMC change-log availability date, the same evidence as Field 10; because only one version
has ever existed, the software's publication date and its version-1 release date coincide.

Version Description is genuinely absent, not merely unlooked-for: CCMC's record carries
`changeLog: null` for ADELPHI, the site-wide change log contains exactly one ADELPHI entry (the
availability announcement, already used above), and no release notes exist. There is also nothing for
such a description to summarise — Field 12 asks for "major changes in the new version", and version 1
is the initial and only version, so it supersedes nothing.

Version PID is absent for the same reason as Field 2: no DOI exists at any level.

For contrast, CCMC does version other catalogue models actively (Ovation-Prime at 1.0 and 2.3, Weimer
at 2000/2005/DeltaB_2012, SuperDARN Convection Models at 4.3.1 and 5), so ADELPHI's single version is
a real property of this model rather than a limitation of CCMC's metadata.

### 13. Programming Language (RECOMMENDED)
- IDL

From CCMC's structured record, `code: {languages: "IDL"}`. `IDL` is an exact row in the live
`ProgrammingLanguage` vocabulary. This is the only language stated, and no source is available to
infer others from.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1029/2020SW002677

Robinson, R. M., Zanetti, L., Anderson, B., Vines, S., & Gjerloev, J. (2021). Determination of auroral
electrodynamic parameters from AMPERE field-aligned current measurements. *Space Weather*, 19,
e2020SW002677. Published 2021-03-17; open access under CC BY-NC-ND.

This is the paper that describes the model as a whole. CCMC's description of ADELPHI cites this DOI
directly for the model's computed quantities, and Ringuette et al. 2022 and Sur et al. 2025 both cite
it as *the* ADELPHI reference. The other two Robinson papers describe individual empirical ingredients
rather than the model, so they are recorded under Field 27 instead.

### 15. License (RECOMMENDED)
- **License:** Not found
- **License URI:** Not found

**A documented omission, not an unresearched field.** No license statement exists for ADELPHI anywhere
that was searched: there is no LICENSE file because there is no repository; the CCMC model page carries
no license, terms-of-use or redistribution statement; the model's `publicationPolicy` field in CCMC's
structured record is an empty string, meaning CCMC records no model-specific policy; and the Instant
Run interface's page source contains no occurrence of "licen", "term", "copyright", "cite" or
"acknowledg" — only links to NASA's generic privacy notice and a data-collection consent agreement.

CCMC's *General Publication Policy*, which the model page links to in place of a model-specific one, is
an academic-attribution policy: it asks users to acknowledge CCMC, credit the model developers, report
resulting publications, and contact the developers before publishing, and notes that developers may
request co-authorship. It states no software license and no redistribution terms. Attribution
expectations are not a license, so this does not supply a value.

**`Restricted` was considered and is a defensible alternative the user may prefer.** ADELPHI's source
code is not distributed and cannot be obtained; only a hosted run service is offered, which is close to
what "restricted" is meant to capture. It was not selected because selecting it would assert a licensing
posture that CCMC has never stated. The honest reading is that CCMC simply never published license
terms, which is an absence rather than an assertion of restriction. Flagging this for the user rather
than deciding it silently.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- ionosphere
- aurora
- auroral electrojet
- electrodynamics
- electron precipitation
- field aligned
- magnetic local time
- space weather
- joule heating
- ionospheric conductance
- cross polar cap potential

Keywords are the one open vocabulary in the form, so the live list was consulted specifically to reuse
existing rows instead of minting near-duplicates. The first eight already exist in HSSI and are
reproduced with their exact stored spelling — note `field aligned`, which is stored unhyphenated and
singular; writing "field-aligned currents" would have created a third variant of the same concept. The
last three are new rows and are entered lower-case, one concept per entry.

This field also absorbs the model characteristics that CCMC records but HSSI's closed vocabularies
cannot hold. CCMC lists seven phenomena for ADELPHI — Ionosphere Electrodynamics, Particle
Precipitation, Energy Flow into Ionosphere, Joule Heating, Ionosphere Convection, Field-aligned
Currents, and Cross-polarcap Electric Potential — of which none has a row in HSSI's closed `Phenomena`
list (Field 22). Per Field 22's instruction, phenomena with no row belong in Keywords, which is why
`joule heating`, `cross polar cap potential`, `electron precipitation`, `field aligned` and
`electrodynamics` appear here.

`idl` exists as a keyword row and was considered, but rejected as redundant with Field 13.

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific

Confirmed against the live `DataInput` vocabulary. ADELPHI reads exactly one data source: AMPERE
field-aligned current files, obtained from the AMPERE project rather than from any general-purpose
archive. Field 17 explicitly directs that an observatory-specific source be marked as such with the
mission named in Related Observatory, which is done in Field 32.

Rejected: `CDAWeb`, `HAPI`, `OMNIWeb`, `Madrigal`, `SSCWeb` and the other archive rows — ADELPHI does
not retrieve from any of them; the AMPERE files are staged locally by filename convention. `Other` was
rejected as strictly less informative than the applicable specific row. The junk production row
`Other - https://xrt.cfa.harvard.edu/level1/` is present in the live vocabulary but is never a valid
selection.

### 18. Input File Formats (RECOMMENDED)
- netCDF3/4
- ascii

Both confirmed against the live `FileFormat` vocabulary.

CCMC's `inputsDescription` names the input files precisely: AMPERE grids such as
`yyyymmdd.0000.86400.120.north.grd.ncdf` — the `.ncdf` extension is netCDF — accompanied by a plain
text control file `yyyy0000DayList.txt` whose first line gives a count of days and whose subsequent
lines are `yyyymmdd` dates telling the code which AMPERE files to read. The control file is what
`ascii` records; it is a genuine required input, not incidental.

### 19. Output File Formats (RECOMMENDED)
- ascii

Confirmed against the live `FileFormat` vocabulary.

CCMC states that "Adelphi writes 1D and 2D outputs to file" without naming a format. The format is
established independently and unambiguously by NASA's Kamodo package, which ships a dedicated ADELPHI
reader: Kamodo's model-reader documentation states "ADELPHI model outputs are produced in ascii form
with one file per each N/S hemisphere per day. The file converter combines the data from both
hemispheres into one netCDF4 file per day." Kamodo's converter confirms this in code, globbing `*.txt`
files and parsing them line by line through a text reader, keying on `MLT =` and `MLAT` header lines
before reading whitespace-separated numeric columns.

`netCDF3/4` is deliberately **not** listed as an output format. The netCDF4 files in the Kamodo
workflow are produced by *Kamodo's* converter, not by ADELPHI; recording them here would credit ADELPHI
with a capability belonging to a downstream package.

### 20. Operating System (RECOMMENDED)
**Not found**

No operating-system support is stated in any source consulted. There is no repository, hence no CI configuration,
package manifest or installation documentation to read; CCMC's model record has no platform field; and
the Instant Run interface exposes only a web form, so it tells a user nothing about where the code
itself will run.

Two tempting inferences were rejected as fabrication rather than extraction. IDL is a cross-platform
language, which might suggest `Operating System Independent` — but that is a property of the language,
not a tested claim about this code, and no portability statement exists. CCMC's servers are
Linux-based, which might suggest `Linux` — but where CCMC happens to run the model is not a statement
of what the software supports. Recorded as not found so that a future agent asks the developer rather
than re-deriving the same guess.

### 21. CPU Architecture (RECOMMENDED)
**Not found**

Absent for the same reason and with the same evidence as Field 20: no repository, no build or
installation documentation, and no statement from CCMC. `CPU Independent` was considered and rejected
on the same grounds — plausible for interpreted IDL, but unsupported by any source.

### 22. Related Phenomena (OPTIONAL)
- Geomagnetic Storms

Confirmed against the live `Phenomena` vocabulary, which is closed and contains only seven values:
Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind,
and X-ray emission.

`Geomagnetic Storms` is a direct match rather than a stretch: CCMC's first sentence describes ADELPHI
as calculating "storm-time high-latitude electrodynamics", and Robinson et al. 2021 validated it over
30 geomagnetically active days.

That enumeration above is the reason this field holds only one value. ADELPHI's other seven
CCMC-recorded phenomena — ionospheric electrodynamics, particle precipitation, energy flow into the
ionosphere, Joule heating, ionospheric convection, field-aligned currents and cross-polar-cap electric
potential — are all magnetosphere-ionosphere phenomena, whereas the closed list is predominantly solar
and heliospheric apart from `Geomagnetic Storms`. None of the seven can be expressed here, so they are
carried in Keywords (Field 16) as Field 22 directs. This field is not under-filled; the vocabulary
simply has no rows for most of what ADELPHI models.

### 23. Development Status (RECOMMENDED)
Inactive

Confirmed against the live `RepoStatus` vocabulary.

CCMC's catalogue records ADELPHI's `status` as **Production**, which establishes the first half of the
repostatus definition of `Inactive` — "reached a stable, usable state". The second half, "no longer
actively developed; support provided as time allows", is supported by the absence of any development
signal: a single version (1) with no successor, `changeLog: null`, no release notes, and a reference
publication from 2021 with no subsequent model paper. CCMC continues to *support* the model through two
named model hosts, which is exactly the "support provided as time allows" the definition anticipates.

`Active` is the alternative and is not unreasonable — ADELPHI was newly deployed to Instant Run on
2025-07-16, and the model page was edited on 2026-08-10. Both were weighed and judged to be evidence of
CCMC's ongoing *curation and deployment*, not of ongoing development of the model code, which is what
the field asks about. Flagging this as a judgment call: if the developer or CCMC confirms active code
development, `Active` should replace this value. `Unsupported` was rejected outright, since named CCMC
hosts and a reachable developer address contradict "authors have ceased work".

### 24. Documentation (RECOMMENDED)
https://ccmc.gsfc.nasa.gov/models/ADELPHI~1/

The same URL as Field 3, which Field 24 expressly permits ("If this is the same as the access URL, then
enter that link here"). It is also the only documentation CCMC publishes for the model: the page
carries the model description, inputs, outputs, caveats, domains, phenomena, references and contacts.
There is no manual, no docs site, no readthedocs build and no installation instructions — none of which
is surprising, as there is nothing to install.

Two other sources document aspects of the model without being its documentation, and are cited in their
own fields rather than here: Robinson et al. 2021 (Field 14) describes the method and validation, and
Kamodo's model-reader documentation (Field 30) describes ADELPHI's output file layout, which is where
Field 19's value came from.

The Instant Run interface (https://kauai.ccmc.gsfc.nasa.gov/instantrun/adelphi/) was considered and
rejected as the documentation link: it is an unannotated submission form offering a username, date,
hour and hemisphere, with no explanatory content.

### 25. Funder (OPTIONAL)

**Funder 1**
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

**Funder 2**
- **Organization:** U.S. National Science Foundation
- **Funder Identifier:** https://ror.org/021nxhr62

Both names are given in full per Field 25's instruction to avoid acronyms, and both are the ROR display
names for their respective records — note that NSF's ROR display name carries the "U.S." prefix, which
is reproduced exactly rather than normalised to "National Science Foundation".

**Provenance and its limits.** These are the funders the publisher asserts for the ADELPHI reference
publication (Robinson et al. 2021), as recorded in that paper's Crossref funding metadata. There is no
software-specific funding statement — no repository, no acknowledgments file — so this is an inference
from the funding of the work that produced the model to the funding of the model itself. The inference
is reasonable, since the 2021 paper is the model's defining publication, but a future agent should know
it is an inference. The paper's own acknowledgments text could not be read directly: the article is
open access under CC BY-NC-ND, yet Wiley returns 402/403 to automated retrieval and no repository
mirror, Europe PMC record or archived copy exists. Crossref's structured funding metadata was used
instead.

Crossref attributes several awards to "Goddard Space Flight Center" (https://ror.org/0171mag52) as a
distinct funder record. GSFC is recorded here as the administering NASA center rather than as a
separate funder entry, since listing both it and NASA would double-count the same agency.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Numbers:**
  - NNG11PL10A (National Aeronautics and Space Administration, administered through Goddard Space Flight Center)
  - NNX14AK74G (National Aeronautics and Space Administration, administered through Goddard Space Flight Center)
  - NNX08AM32G S03 (National Aeronautics and Space Administration)
  - ATM-0739864 (U.S. National Science Foundation)
  - ATM-1420184 (U.S. National Science Foundation)
  - ATM-0646323 (U.S. National Science Foundation)
  - AGS-1003580 (U.S. National Science Foundation)

Award **titles** are genuinely unavailable: Crossref funding metadata carries award numbers without
titles, and the paper's acknowledgments text could not be retrieved (see Field 25).

The award numbers above are every award the publisher asserts for Robinson et al. 2021, the ADELPHI
reference publication. Two caveats a future agent should carry forward. First, the same provenance
limit as Field 25 applies — these funded the research described in the paper, and no software-specific
funding statement exists. Second, several of these awards also appear on the earlier Robinson papers
(NNG11PL10A, NNX14AK74G, ATM-0739864 and ATM-1420184 recur on the 2020 and 2018 papers), so some of
them plausibly supported the underlying PFISR conductance and GUVI energy-flux studies rather than
ADELPHI's own implementation. They are listed in full rather than filtered by guesswork, but the set
should be narrowed if the developer confirms which awards funded the code.

Crossref renders the four NSF numbers with a Unicode hyphen (U+2010) rather than ASCII `-`
(`ATM‐0739864`); they are normalised here to a plain ASCII hyphen, which is the form the agencies
themselves use. The NASA award numbers carry no hyphen-type separator, so only the NSF entries were
affected; note that `NNX08AM32G S03` does contain a space, which is preserved as Crossref records it.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2020JA028008 — Robinson, R. M., Kaeppler, S. R., Zanetti, L., Anderson, B., Vines, S. K., Korth, H., & Fitzmaurice, A. (2020). Statistical relations between auroral electrical conductances and field-aligned currents at high latitudes. *Journal of Geophysical Research: Space Physics*, 125, e2020JA028008.
- https://doi.org/10.1029/2018GL078718 — Robinson, R. M., Zhang, Y., Anderson, B. J., Zanetti, L. J., Korth, H., & Fitzmaurice, A. (2018). Statistical relations between field-aligned currents and precipitating electron energy flux. *Geophysical Research Letters*, 45, 8738–8745.
- https://doi.org/10.1029/2024SW004023 — Sur, D., et al. (2025). Intercomparison of Model Determinations of Auroral Electrodynamic Parameters. *Space Weather*.

The first two are listed by CCMC as ADELPHI's other key references, and each supplies a specific
empirical ingredient of the model rather than describing the model as a whole: the 2020 paper derives
the field-aligned-current-to-conductance relations from coincident AMPERE and PFISR measurements, which
CCMC cites in its caveat as the source of the model's global conductance map; the 2018 paper derives
the field-aligned-current-to-electron-energy-flux relation from AMPERE and TIMED/GUVI far-ultraviolet
emissions. The 2021 paper is not repeated here because it is the Reference Publication (Field 14).

Sur et al. 2025 is not a CCMC-listed reference but is included because it independently evaluates
ADELPHI: its abstract names "Active Magnetosphere and Planetary Electrodynamics Response Experiment
(AMPERE) Derived Electrodynamics of the High Latitude Ionosphere (ADELPHI)" as one of the models
compared for cross polar cap potential, hemispherically integrated Joule heating and hemispheric power
input, under the COSPAR ISWAT AuroraPHILE activity. It is the best available independent assessment of
the model's performance.

Considered and not included: Ringuette et al. 2022 (`10.3389/fspas.2022.1005977`), the Kamodo
flythrough paper, which mentions ADELPHI only in a list of simulation outputs then being added to
Kamodo — the relationship it documents is recorded under Field 30, where it belongs; and Shim,
Robinson, Garcia-Sage et al., "Evaluating Multipoint Sampling of Global-Scale High-Latitude
Electrodynamics by the Geospace Dynamics Constellation" (`10.13016/m28iyi-tcv3`), which surfaced in a
DataCite search and uses ADELPHI-related work, but whose DOI resolves to a repository text record
rather than the journal article, making it a poor citation to publish.

### 28. Related Datasets (OPTIONAL)

Two datasets, deliberately of two different kinds. **The distinction is load-bearing and should be
preserved in any future edit: the first is what ADELPHI reads, the second is what ADELPHI produces.**

**Dataset 1 — the model's input.**
Anderson, B. J., et al. Active Magnetosphere and Planetary Electrodynamics Response Experiment (AMPERE) field-aligned current data [Data set]. Johns Hopkins University Applied Physics Laboratory. https://ampere.jhuapl.edu/

Entered in APA format with a permanent link, as Field 28 permits when no DOI is available. This is the
dataset ADELPHI is built around — its sole input, in the gridded `.grd.ncdf` form CCMC names.

No DOI exists for the AMPERE data product. The SPASE observatory record for AMPERE
(`https://spase-metadata.org/SMWG/Observatory/AMPERE`) lists two information URLs — the AMPERE home
page above, and a NASA HelioData mission page at `https://helio.data.nasa.gov/mission/AMPERE` — but no
dataset DOI, and a DataCite search for the AMPERE Birkeland-current data returned only unrelated
records. The JHU/APL URL was confirmed to resolve. The AMPERE home page is used rather than the
HelioData page because it is the data provider's own canonical landing page.

**Dataset 2 — an archive of the model's output.**
https://doi.org/10.5281/zenodo.14299925 — Sur, D., Robinson, R., & Garcia-Sage, K. (2024). *Intercomparison of model determinations of auroral electrodynamic parameters* [Data set]. Zenodo. Published 2024-12-08, CC BY 4.0.

This is the companion data deposit to Sur et al. 2025 (Field 27). Its description states that it
contains "all ADELPHI one-dimensional and two-dimensional data … used in the paper" — specifically
ADELPHI 1D output (cross polar cap potential, hemispherically integrated Joule heating, hemispheric
power input) and ADELPHI 2D output (radial current densities, Joule heating distribution, ionospheric
conductances) — alongside DMSP and SuperDARN cross-polar-cap-potential comparison data.

The DOI recorded is the **concept** DOI, `10.5281/zenodo.14299925`, which resolves to the currently
sole version record `10.5281/zenodo.14299926`; the deposit has no second version at present. The
concept DOI is preferred so the reference survives any future version, consistent with HSSI's stated
preference for concept DOIs over version DOIs.

Authorship confirms this is authoritative ADELPHI output rather than a third party's reimplementation:
Zenodo lists Robert Robinson as a creator with ORCID `0000-0002-7750-8326` — byte-identical to the
ORCID recorded for ADELPHI's sole author in Field 6 — with Dibyendu Sur (`0000-0001-9349-086X`) as
creator and contact person and Katherine Garcia-Sage (`0000-0001-6398-8755`) as creator and supervisor.
Note that the deposit's `related_identifiers` field is empty, so its link to the Sur et al. 2025 paper
rests on the description text and shared authorship rather than on a machine-readable relation; a
future agent should not expect to traverse from the paper DOI to this dataset automatically.

**Why an output dataset is listed here at all — the reasoning, so it is not relitigated.** Field 28
asks for "datasets the software supports functionality for (e.g., analysis)", and the parenthetical
example points toward datasets a package *reads*. ADELPHI does not read this one; it generated it. The
argument against inclusion is therefore real and was weighed: this is a derived product covering only
the specific days of a single intercomparison study (9 March 2012, 22 July 2004 and the other paper
dates), not a general ADELPHI output archive.

It is included nonetheless, for three reasons that are specific to this software rather than generic:

1. Field 28's definition does not restrict to inputs, and the field is named *Related* Datasets. A
   model's own published output is related to it in the most direct sense available.
2. The value to a user is unusually high **because** ADELPHI is source-unavailable. The code is not
   distributed, and the only public access is an Instant Run form that returns plots for one date and
   hemisphere at a time. This deposit is consequently the only citable, openly licensed archive of real
   ADELPHI output identified anywhere — the sole way a prospective user can inspect the model's actual
   numerical products, at both 1D and 2D levels, without requesting a run. For a repository-backed
   package this entry would be marginal; here it does genuine work.
3. It is co-created by ADELPHI's own developer, so it represents the model's output authoritatively.

The two entries are labelled by role above precisely so that a reader does not mistake them for the
same kind of relationship, and so that a future agent adding a third dataset knows which bucket it
belongs in.

### 29. Related Software (OPTIONAL)
- https://ccmc.gsfc.nasa.gov/models/AMGeO~3/ — AMGeO (Assimilative Mapping of Geospace Observations), version 3
- https://ccmc.gsfc.nasa.gov/models/Ovation-Prime~2.3/ — Ovation-Prime, version 2.3
- https://ccmc.gsfc.nasa.gov/models/Weimer~2005/ — Weimer Ionosphere Models, version 2005

Three genuinely similar-purpose tools: each specifies high-latitude ionospheric electrodynamic
parameters, and each is a direct alternative a user choosing ADELPHI would weigh against it. CCMC
catalogue URLs are used because these are CCMC-hosted models without software DOIs, which is the
fallback Field 29 allows.

Per-entry justification, since "similar" needs to be specific to be useful:

- **AMGeO** is the closest functional analogue — it produces the same class of high-latitude
  electrodynamic maps (potential, conductance, currents) from observations, and it is the assimilative
  counterpart to ADELPHI's direct-derivation approach, which makes the pair genuinely informative about
  each other. Both are also among the models Kamodo reads, and its GitHub organisation is
  `AMGeO-Collaboration` if a source link is ever preferred over the CCMC page.
- **Ovation-Prime** specifies auroral particle precipitation and hemispheric power, overlapping
  ADELPHI's energy-flux output. It is named alongside ADELPHI in the Sur et al. 2025 intercomparison as
  a model determining the same auroral electrodynamic parameters.
- **Weimer Ionosphere Models** specify the high-latitude ionospheric electric potential and cross polar
  cap potential empirically, the same primary quantity ADELPHI solves for, differing mainly in being
  driven by solar wind input rather than measured field-aligned currents.

Considered and deliberately excluded:

- **SWMF, OpenGGCM, and LFM-MIX** — also compared against ADELPHI in Sur et al. 2025, but they are
  general-purpose global MHD frameworks that compute auroral electrodynamic parameters among many other
  things. Being a benchmarking comparand does not make a full magnetosphere simulation framework a
  "similar task" tool to a targeted high-latitude specification model; including them would dilute the
  field.
- **SuperDARN Convection Models** — supply observed convection patterns rather than a modeled
  specification of the full electrodynamic parameter set; they served as validation data in the
  intercomparison, which is a data role, not a peer-software role.
- **AMIE** (Assimilative Mapping of Ionospheric Electrodynamics) — conceptually the classic predecessor
  in this space and frequently confused with ADELPHI (see Field 4), but no single canonical distributed
  package or stable URL for it was identified, and AMGeO already represents the assimilative approach
  here. Recorded so a future agent knows it was weighed rather than overlooked.
- **Kamodo** — a real and evidenced relationship, but an interoperability one; it belongs in Field 30
  and is not duplicated here.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/nasa/Kamodo — Kamodo

A demonstrated exchange, not a dependency claim. Kamodo, NASA CCMC's model-analysis and satellite
flythrough package, contains first-class support for ADELPHI output, evidenced by specific artifacts
rather than by ecosystem membership:

- `kamodo_ccmc/readers/adelphi_4D.py` — a dedicated ADELPHI reader that maps ADELPHI's eleven output
  variables (`PED`, `HALL`, `PHI`, `EEAST`, `ENORTH`, `JEAST`, `JNORTH`, `EFLUX`, `JHEAT`, `JRIN`,
  `JROUT`) onto Kamodo's standardised names, units and `SM` spherical coordinate metadata;
- `kamodo_ccmc/readers/adelphi_tocdf.py` — a converter that parses ADELPHI's ascii hemisphere files and
  combines them into one netCDF4 file per day;
- `tests/test_ADELPHI.py`, plus `Validation/Notebooks/ModelReaderTesting_ADELPHI.ipynb` and a timing
  notebook — a maintained test and validation path for that reader.

Ringuette et al. 2022 documents the relationship in the literature as well, listing ADELPHI among the
simulation outputs being added to Kamodo. This is precisely the "one's output can be imported into the
other" exchange Field 30 asks for.

Nothing else qualifies. ADELPHI has no dependency list to mine — it is unreleased IDL — so there was no
opportunity to mistake generic infrastructure for interoperability here.

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** Birkeland Currents from IRIDIUM Data
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/IRIDIUM/Magnetometer

Resolved against HSSI's controlled instrument/observatory vocabulary, which was confirmed at the time
of extraction to be entirely SPASE-backed, with no row failing the `https://spase-metadata.org/`
identifier guard. Exactly one instrument row corresponds to the measurement chain ADELPHI consumes, so
this is a clean single-row match; the name is copied verbatim from the row.

Why this instrument is genuinely "designed to support" rather than incidental: ADELPHI's sole input is
the AMPERE gridded field-aligned current product, and that product *is* the processed output of the
engineering magnetometers carried on the Iridium constellation. The SPASE record confirms the
correspondence — its `InvestigationName` is "Birkeland Currents from IRIDIUM Data" (which is the name
HSSI stores, rather than the record's `ResourceName` of "IRIDIUM Magnetometer"), it describes
magnetometers "whose data, in aggregate, are relevant to the study of Birkeland (magnetic field
aligned) currents at auroral latitudes", and its contact is Brian J. Anderson — the AMPERE principal
investigator and a co-author of all three ADELPHI papers. A user searching for software that works with
Birkeland-current measurements from Iridium should find ADELPHI, since converting exactly those
measurements into electrodynamic parameters is the model's entire purpose.

**Do not use the AMPERE row typed as an instrument.** The vocabulary contains
`Active Magnetosphere and Planetary Electrodynamics Response Experiment (AMPERE)` with `type` 1
(instrument) and identifier `https://spase-metadata.org/SMWG/Observatory/AMPERE.html`. That is the
`.html` duplicate of the observatory record, mis-typed as an instrument; the identifier path itself
says `Observatory`. Under the normalisation rule the bare and `.html` identifiers are one resource, and
the correct row is the observatory one recorded in Field 32. Recording the `.html` row here would
double-list AMPERE across Fields 31 and 32 under two identifiers for the same thing.

Considered and omitted, with reasons, so these are not re-proposed:

- **Poker Flat Incoherent Scatter Radar (PFISR)** — supplied the electron-density measurements from
  which the conductance relations were fitted (Robinson et al. 2020), but ADELPHI reads no PFISR data.
  The radar's contribution is frozen into the model's fitted coefficients, so the exclusion is a
  **relevance** decision, not a failure to resolve the name.

  That distinction matters, because a resolvable candidate does exist and a future agent should not
  "repair" this omission by adding it. The vocabulary has no Poker-Flat-specific incoherent scatter
  radar row — the Poker Flat rows are magnetometers, all-sky imagers, an MF radar and auroral cameras —
  but it *does* carry an observatory-level row for the radar family PFISR belongs to,
  `Advanced Modular Incoherent Scatter Radar` (`https://spase-metadata.org/SMWG/Observatory/AMISR`,
  which also appears in an `.html` duplicate form). Under the observatory-substitution rule that row
  would be the correct fallback **if** PFISR were a related instrument. It is not, so the row is
  deliberately left unrecorded. Also present but equally inapplicable are Millstone Hill's ISR rows and
  the EISCAT observatory rows.
- **TIMED/GUVI** (`https://spase-metadata.org/SMWG/Instrument/TIMED/GUVI`) — the Global Ultraviolet
  Imager resolves cleanly in the vocabulary, and its far-ultraviolet emissions were used to derive the
  energy-flux relation in Robinson et al. 2018. Excluded for the same reason as PFISR: the relation is
  a fixed empirical coefficient set, and ADELPHI never reads GUVI data. Listing it would misdirect
  users searching for GUVI processing software.
- **SuperMAG magnetometers** (`https://spase-metadata.org/SMWG/Instrument/SuperMAG/Magnetometers`) —
  SuperMAG indices were used to *validate* ADELPHI's simulated electrojet indices in Robinson et al.
  2021. Validation-time comparison data is not an input the software is designed to process.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Active Magnetosphere and Planetary Electrodynamics Response Experiment
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/AMPERE

A single unambiguous observatory-row match, with the name copied verbatim from the controlled list.
ADELPHI is designed to support AMPERE and nothing else: AMPERE data is its only input, the file naming
convention it requires is AMPERE's own, and the model's name begins with the mission. This is exactly
the case where Field 17's `Observatory/Mission-specific` selection is cross-listed with a named
observatory, as done above.

The `.html` duplicate of this identifier is discussed under Field 31 and must not be recorded
separately.

Considered and omitted:

- **IRIDIUM** (`https://spase-metadata.org/SMWG/Observatory/IRIDIUM`) and **IRIDIUM_1_70**
  (`.../IRIDIUM_1_70`) — the Iridium constellation is the platform carrying the magnetometers listed in
  Field 31, but it is a commercial communications constellation, and the heliophysics mission ADELPHI
  targets is AMPERE, which SPASE models as an observatory in its own right with its own operating span
  and principal investigator. Listing Iridium at observatory level would add no information beyond the
  AMPERE association while implying ADELPHI supports the constellation generally.
- **TIMED** (`https://spase-metadata.org/SMWG/Observatory/TIMED`) — omitted for the same reason as its
  GUVI instrument under Field 31.

### 33. Logo (OPTIONAL)
**Not found**

ADELPHI has no logo. The only image on the CCMC model page is CCMC's own site logo
(`https://ccmc.gsfc.nasa.gov/static/images/logo2.png`), carried in the page's Open Graph metadata as
the site-wide default; it identifies CCMC, not this model, so it must not be recorded here. That it is a
site-wide default rather than ADELPHI's own image was confirmed rather than assumed: the identical
`og:image` value is served by other CCMC model pages checked for comparison (AMGeO, Ovation-Prime,
Weimer and SWMF). CCMC's model-page record for ADELPHI also has an empty `figures` array. With no
repository, there is no assets directory or README badge to draw on either.
