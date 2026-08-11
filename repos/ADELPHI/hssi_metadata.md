# HSSI Metadata Extraction Results

**HSSI Software ID:** Not applicable — new submission, no existing HSSI record
**Repository:** https://ccmc.gsfc.nasa.gov/models/ADELPHI~1/ (CCMC model page — authoritative source; ADELPHI has no source-code repository)
**Source Revision:** Not applicable — website-only extraction, no version-controlled source is published. The CCMC model page carries its own "Last Updated: 08/10/2026" stamp, which is the closest available analogue to a pinned revision.
**Extraction Date:** 2026-08-11
**Validation Date:** 2026-08-11
**Validation Status:** PASS

---

**Scope note — this evidence is website-only.** ADELPHI is an IDL model hosted by NASA's Community
Coordinated Modeling Center (CCMC). No source repository is published in any of the places searched:
GitHub (both repository and code search), GitLab, Zenodo, DataCite and the NASA Software Catalog were
each queried, and none returned an ADELPHI source repository. **This is confirmed by the authors
themselves, not merely by failed searches:** the Data Availability Statements of the 2021 and 2018
papers name only the datasets used — AMPERE, SuperMAG and Kyoto indices in 2021; AMPERE, TIMED/GUVI and
Kyoto in 2018 — while the 2020 paper's *Acknowledgments* instead name Zenodo DOIs for a *collaborator's*
conductance code and data (Fields 28 and 29). None of the three names an ADELPHI source release
anywhere. Positive statements of what is available, which omit the model's own code while deliberately
publishing a collaborator's, are considerably stronger evidence than search misses.

Every value below therefore derives from the CCMC model records, the peer-reviewed literature, SPASE,
ORCID, ROR, Crossref, or NASA's Kamodo package (which contains a dedicated ADELPHI reader). There is no
README, CITATION.cff, LICENSE, package manifest, CI configuration or commit history to draw on, so
several fields that a repository-backed extraction would fill are correctly empty here rather than
merely unresearched. Read each "Not found" as a documented omission with the
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
- **Submitter Name:** Determined at submission time
- **Submitter Email:** Determined at submission time

This field is mandatory on the HSSI form but is a property of the *act of submitting*, not of the
software: it records who transmits the metadata, and it is supplied by that person when a submission is
made. It is not derivable from ADELPHI's documentation or from any source examined, and it would be
wrong to infer it — the model's developer and CCMC hosts (Field 6) are contacts for the software, not
submitters of this record.

No submission is planned at present; this dossier is a standalone description of ADELPHI's metadata.
The absence of a submitter name here is therefore the correct and complete state of the field, not an
outstanding gap. Should the entry later be submitted to HSSI, the submitting person's name and work
email are filled in at that point and nothing else in this file changes.

### 2. Persistent Identifier (RECOMMENDED)
**Not found** — ADELPHI has no DOI.

Negative research, so a future agent need not repeat it — but note carefully how the searches were
scoped, because the scoping matters:

- **Zenodo returns zero records for ADELPHI in combination with AMPERE.** The AMPERE qualifier is
  necessary rather than incidental: "ADELPHI" is a heavily overloaded string, and an unqualified query
  returns hundreds of irrelevant hits (Adelphi University, an Adelphi consultancy, "Edizione Adelphi"
  book reviews) with no way to spot a heliophysics record among them. Adding AMPERE is what makes the
  result readable. The cost of that filter is real and is recorded here: it excludes both archived
  ADELPHI **output** datasets now listed in Field 28 (datasets 2 and 3), neither of whose Zenodo
  metadata mentions AMPERE. That is not a contradiction — see the next paragraph.
- **DataCite**, filtered to `resource-type-id=software` with heliophysics qualifiers, returns **zero**
  ADELPHI software records. The same query filtered to datasets returns only the output and provenance
  deposits recorded in Field 28. An unfiltered DataCite query returns a University of Maryland text
  record (`10.13016/m28iyi-tcv3`, Shim, Robinson, Garcia-Sage et al., on the Geospace Dynamics
  Constellation), which cites the model rather than being the model, and which has since been
  superseded by a journal article (Field 27).
- **The papers' own Data Availability Statements name no ADELPHI code release** — see the scope note.
  This is the strongest form of the negative available: the authors state what is available, and their
  own model's source is not among it. Notably the 2020 paper *does* deposit a collaborator's code and
  data on Zenodo with DOIs, which shows the group was willing and able to release software when it
  chose to. ADELPHI itself was not released.

**A dataset DOI is not a software DOI, so Field 28 and this field are not in tension.** Field 28 now
records Zenodo DOIs for archives of ADELPHI's model *output*. Those DOIs identify deposited data
products; they do not identify, version or make citable the ADELPHI software itself, and Field 2 asks
for a persistent identifier for the software. This is the same distinction already applied to the
Maryland record above: a resource that involves ADELPHI is not thereby an identifier for ADELPHI.
No software DOI, no Zenodo concept DOI for the code, and no DOI badge exists, because there is no
repository or software deposit to attach one to.

CCMC does assign the model an internal SPASE Resource ID, `spase://CCMC/SimulationModel/ADELPHI/1`,
carried in its catalogue record. This is deliberately **not** recorded as the Persistent Identifier:
it is not a DOI, HSSI's field is a DataCite DOI lookup, and the identifier does not resolve: there is
no record at `https://spase-metadata.org/CCMC/SimulationModel/ADELPHI/1`, so CCMC's SimulationModel
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

A systematic full-text search of the literature for ADELPHI alongside each candidate wording surfaced no
fourth variant, and supports the selected "Properties" form as the best attested. Two attestations of it
are confirmed against primary text: the Kamodo journal paper (Ringuette et al. 2023) and Shim et al.
2026, which renders it "AMPERE-derived electrodynamic properties of the high-latitude ionosphere
(ADELPHI)" — matching CCMC's `fullName` in substance. The 2019 EGU abstract's own prose also describes
the model as giving "global specification of electrodynamic **properties**", despite that abstract's
title using "Parameters".

**A caution about co-occurrence searching in this particular case, which a future agent repeating the
search will otherwise fall into.** The phrase "auroral electrodynamic parameters" is common in this
subfield and appears in the titles of both the ADELPHI reference publication ("Determination of Auroral
Electrodynamic Parameters From AMPERE Field-Aligned Current Measurements") and Sur et al. 2025
("Intercomparison of Model Determinations of Auroral Electrodynamic Parameters"). A full-text query for
ADELPHI together with "Electrodynamic Parameters" therefore matches any paper that merely cites either
of those titles, and cannot by itself distinguish an ADELPHI *expansion* from an ordinary use of the
phrase. Sur et al. 2025 and Shim et al. 2026 both match that query, yet Sur's actual expansion is
variant 3 above, not "Parameters". **The single confirmed attestation of the "Parameters" expansion is
the 2019 EGU abstract title**, verified verbatim as "AMPERE-Derived Electrodynamic Parameters of the
High Latitude Ionosphere (ADELPHI)", by Robinson, Anderson and Zanetti. Variant 2 rests on that title
alone, which is genuine but singular.

One further "Properties" attestation, recorded during extraction as an AGU Fall Meeting 2025 abstract
("Assessing the Accuracy of GDC Measurements Using ADELPHI and Weimer 2005"), was found in the full-text
index but could not be located again through Confex or general search. Its source type is also in doubt:
Shim et al. 2026's own reference list carries a near-identically titled entry beginning "Code for
assessing the accuracy of GDC measurements using ADELPHI and Weimer 2005", attributed to Shim (2025) and
described in that paper as the code developed for the study — suggesting the record may be a software or
data deposit rather than a conference abstract, which would explain why Confex never returned it. That
identification could not be resolved to a DOI either, so neither characterization is confirmed. It is
recorded as supporting rather than load-bearing, and a future agent should establish what it actually is
before citing it. The
conclusion does not depend on it: the CCMC model record is the authoritative publisher of this software
entry, and the two confirmed primary-text attestations agree with it. The selected value should not be
changed without something that outranks CCMC's own `fullName`.

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
content-management timestamp for the web page, falling one day before the extraction date recorded in
the header above, which shows it tracks page edits rather than the software.

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

**`Restricted` was considered and rejected.** ADELPHI's source code is not distributed and cannot be
obtained; only a hosted run service is offered, which is close to what "restricted" is meant to capture.
It was not selected because doing so would assert a licensing posture CCMC has never stated. Leaving the
field empty reflects an absence of terms; selecting `Restricted` would manufacture terms the publisher
did not set. The field is therefore correctly empty rather than merely unfilled.

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

`Active` was considered and rejected. ADELPHI was newly deployed to Instant Run on 2025-07-16 and the
model page was edited on 2026-08-10, but both are evidence of CCMC's ongoing *curation and deployment*
rather than of ongoing development of the model code, which is what this field asks about. Should the
developer or CCMC later confirm active code development, `Active` would become correct; nothing
currently available supports it. `Unsupported` was rejected outright, since named CCMC hosts and a
reachable developer address contradict "authors have ceased work".

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

The name is given in full per Field 25's instruction to avoid acronyms, and is the ROR display name.

**Evidence.** The acknowledgments of the ADELPHI reference publication (Robinson et al. 2021) state
verbatim: *"This work was supported at Goddard Space Flight Center by NASA Cooperative Agreement
NNG11PL10A, the Community Coordinated Modeling Center, and the TIMED/GUVI Project (NASA grant
NNX14AK74G). AMPERE development, data acquisition, and science processing at JHU/APL were supported by
NSF awards ATM-0739864 and ATM-1420184."* The first sentence is what funded *this work*, and both of
its awards are NASA.

**The U.S. National Science Foundation (https://ror.org/021nxhr62) was previously listed here and has
been removed, on that same evidence.** The acknowledgment divides the funding by sentence, and the NSF
sentence scopes its awards explicitly to *AMPERE* development, data acquisition and science processing
*at JHU/APL* — a different activity, at a different institution, funding the input mission rather than
ADELPHI. A third group of awards (Field 26) funds SuperMAG, a validation service. Attributing a
funder to ADELPHI because it funded ADELPHI's input data would make every upstream mission's sponsor a
sponsor of every downstream model, which is not what Field 25 asks. NSF's real role is recorded here so
a future agent does not re-add it from Crossref's flat funding block, which collapses all three tiers
into one undifferentiated list and is the reason this field was previously over-broad.

Crossref also attributes awards to "Goddard Space Flight Center" (https://ror.org/0171mag52) as a
distinct funder record. GSFC is the administering NASA center — the acknowledgment says the work was
supported "at Goddard Space Flight Center" — and is not listed separately, since that would
double-count the same agency.

### 26. Award Title (OPTIONAL)

**Award 1**
- **Award Title:** Not found
- **Award Number:** NNG11PL10A

**Award 2**
- **Award Title:** TIMED/GUVI Project
- **Award Number:** NNX14AK74G

Award 1 has no title in any source: the acknowledgment describes it only as a "NASA Cooperative
Agreement", associated with the Community Coordinated Modeling Center, and gives no formal title.

Award 2's title is the project name the authors themselves give it — *"the TIMED/GUVI Project (NASA
grant NNX14AK74G)"* — rather than a formal award title from a funder database, which was not located.
It is recorded because it is directly attested and more informative than "Not found", but it should not
be mistaken for the grant's official title.

**What these two awards actually represent — read this before narrowing further or re-expanding.** The
acknowledgment does not identify any award as funding ADELPHI's implementation specifically. These two
are the **standing support under which Robinson's group produced this research line**: the first two
sentences of the acknowledgments are near-identical across all three CCMC-listed papers (2018, 2020 and
2021 — the 2018 one lacking only the CCMC clause), and the same two NASA awards recur in the fourth
Robinson paper as well (Robinson & Zanetti 2021, Field 27), whose funding is *only* these two. That
recurrence is evidence they are the group's block support, not per-paper line items. Listing them is
correct; reading them as "the grants that paid for the ADELPHI code" would over-claim.

**Five awards were removed from this field on evidence.** They were previously listed because
Crossref's funding metadata presents all seven flat, without the distinctions the acknowledgment text
makes. They fall into two tiers, neither of which funded ADELPHI:

- **AMPERE's funding — `ATM-0739864` and `ATM-1420184` (NSF).** The acknowledgment assigns these
  specifically to "AMPERE development, data acquisition, and science processing at JHU/APL". They fund
  the instrument programme that produces ADELPHI's input, not ADELPHI.
- **SuperMAG's funding — `ATM-0646323` (NSF), `AGS-1003580` (NSF) and `NNX08AM32G S03` (NASA).** These
  appear only in the paper's *Data Availability Statement*, never in the acknowledgments, and solely to
  credit the SuperMAG project: *"The SuperMAG project is supported by the National Science Foundation
  (NSF) Grants NSF ATM-0646323 NSF AGS-1003580 and National Aeronautics and Space Administration (NASA)
  grant NASA NNX08AM32G S03."* SuperMAG is a third-party service used only to validate ADELPHI's
  modeled indices; ADELPHI does not read its data. Excluding its funders here is the same judgement
  already applied in Field 31, which excludes the SuperMAG magnetometers as validation-only.

A note on character normalisation, still relevant to the two retained NASA numbers' neighbours in any
future re-derivation: Crossref renders the NSF numbers with a Unicode hyphen (U+2010) rather than ASCII
`-` (`ATM‐0739864`). Where those numbers are quoted above they use a plain ASCII hyphen, the form the
agencies themselves use. `NNX08AM32G S03` contains a genuine space, preserved as recorded.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2020JA028008 — Robinson, R. M., Kaeppler, S. R., Zanetti, L., Anderson, B., Vines, S. K., Korth, H., & Fitzmaurice, A. (2020). Statistical relations between auroral electrical conductances and field-aligned currents at high latitudes. *Journal of Geophysical Research: Space Physics*, 125, e2020JA028008.
- https://doi.org/10.1029/2018GL078718 — Robinson, R. M., Zhang, Y., Anderson, B. J., Zanetti, L. J., Korth, H., & Fitzmaurice, A. (2018). Statistical relations between field-aligned currents and precipitating electron energy flux. *Geophysical Research Letters*, 45, 8738–8745.
- https://doi.org/10.1029/2024SW004023 — Sur, D., et al. (2025). Intercomparison of Model Determinations of Auroral Electrodynamic Parameters. *Space Weather*.
- https://doi.org/10.1029/2025JA034684 — Shim, J. S., Robinson, R. M., Garcia-Sage, K., Rowland, D. E., Di Mare, F., Klenzing, J., & Liu, G. (2026). Evaluating Multipoint Sampling of Global-Scale High-Latitude Electrodynamics by the Geospace Dynamics Constellation. *Journal of Geophysical Research: Space Physics*.
- https://doi.org/10.1029/2020GL091527 — Robinson, R. M., & Zanetti, L. J. (2021). Auroral Energy Flux and Joule Heating Derived From Global Maps of Field-Aligned Currents. *Geophysical Research Letters*, 48, e2020GL091527.

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
input, under the COSPAR ISWAT AuroraPHILE activity. Its distinct value is that it is a formal
multi-model benchmark: it places ADELPHI's outputs beside those of LFM-MIX, SWMF, OpenGGCM and Ovation
Prime on common parameters, and against SuperDARN and DMSP observations.

Shim et al. 2026 is the most recent of these and complements Sur et al. rather than ranking against it:
where Sur benchmarks ADELPHI's accuracy, Shim *relies* on it, using ADELPHI output as the "ground truth"
electrodynamic state against which reconstructions by the planned Geospace Dynamics Constellation are
evaluated across four storm events. That is a substantive use of the model's results, not a passing
citation, and it is clear evidence that ADELPHI is trusted as a reference specification. Robinson, ADELPHI's author, is a co-author. Note that an
earlier University of Maryland record for this work (`10.13016/m28iyi-tcv3`) was previously documented
here as a poor citation because its DOI resolved to a repository text record; the journal version above
supersedes it and is the DOI to cite.

Robinson & Zanetti 2021 is included even though CCMC does not list it among the model's key references
and its own text never uses the name "ADELPHI". It derives auroral energy flux and Joule heating — two
of ADELPHI's headline outputs — from AMPERE field-aligned current maps by the model's own technique,
and Shim et al. 2026 cites it as one of the ADELPHI reference set, "(Robinson & Zanetti, 2021; Robinson
et al., 2018, 2020, 2021)". It is therefore part of the model's documentary record even though the
CCMC page omits it.

Considered and not included:

- Ringuette et al. 2022 (`10.3389/fspas.2022.1005977`), the Kamodo flythrough paper, and Ringuette et
  al. 2023 (`10.1016/j.asr.2023.03.033`), the Kamodo journal paper — both mention ADELPHI only as a
  supported model output. The relationship they document is interoperability and is recorded in
  Field 30, where it belongs.
- Zhu et al. 2022, "Assessment of Using Field-Aligned Currents to Drive the Global Ionosphere
  Thermosphere Model" (`10.1029/2022SW003170`). This one is worth recording explicitly because it looks
  like a candidate and is not: it cites Robinson et al. 2021 substantively, but its citation contexts
  show it discussing ADELPHI as *related work* — "Robinson et al. (2021) developed another technique to
  calculate the high-latitude electric potential" — while driving GITM with its own conductance
  treatment. It uses the published method's context, not the software.

### 28. Related Datasets (OPTIONAL)

Four datasets in **three distinct roles**. The distinction is load-bearing and should be preserved in
any future edit: dataset 1 is what ADELPHI *reads*; datasets 2 and 3 are what ADELPHI *produces*;
dataset 4 is what ADELPHI's empirical conductance relations were *derived from*. Conflating them would
misrepresent the model's provenance.

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

**Datasets 2 and 3 are both archives of the model's output**, and the reasoning for including output
datasets at all is set out once, after both of them.

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

**Dataset 3 — a second archive of the model's output.**
https://doi.org/10.5281/zenodo.17102377 — Robinson, R. M., & Shim, J. S. (2025). *Dataset Used for Evaluating Multipoint Sampling of Global-Scale High-Latitude Electrodynamics by the Geospace Dynamics Constellation* [Data set]. Zenodo. Published 2025-09-11, CC BY 4.0.

The companion deposit to Shim et al. 2026 (Field 27), described as containing "outputs from the ADELPHI
and Weimer (2005) models used in the study". Recorded for the same reason as dataset 2, set out below.
Its first creator is Robert Robinson with ORCID `0000-0002-7750-8326`, matching Field 6. As with
dataset 2, the **concept** DOI is recorded (`10.5281/zenodo.17102377`), resolving to version record
`10.5281/zenodo.17102378`.

That two independent studies have each archived ADELPHI output under CC BY reinforces the reasoning
that follows.

**Why output datasets are listed here at all — the reasoning for datasets 2 and 3, so it is not
relitigated.** Field 28 asks for "datasets the software supports functionality for (e.g., analysis)",
and the parenthetical example points toward datasets a package *reads*. ADELPHI reads neither of these;
it generated them. The argument against inclusion is therefore real and was weighed: both are derived
products tied to a single study apiece, covering only that study's dates — the Sur intercomparison days
(9 March 2012, 22 July 2004 and the others) and the four storm events of the Shim analysis — rather than
being general ADELPHI output archives.

They are included nonetheless, for three reasons specific to this software rather than generic:

1. Field 28's definition does not restrict to inputs, and the field is named *Related* Datasets. A
   model's own published output is related to it in the most direct sense available.
2. The value to a user is unusually high **because** ADELPHI is source-unavailable. The code is not
   distributed, and the only public access is an Instant Run form that returns plots for one date and
   hemisphere at a time. These two deposits are consequently the citable, openly licensed archives of
   real ADELPHI output that are known to exist — between them, the practical route to inspecting the
   model's actual numerical products, at both 1D and 2D levels, without requesting a run. For a
   repository-backed package such entries would be marginal; here they do genuine work.
3. Both are co-created by ADELPHI's own developer, so they represent the model's output
   authoritatively.

**Dataset 4 — the data the model's conductance relations were derived from.**
https://doi.org/10.5281/zenodo.2610914 — Kaeppler, S. (2019). *PFISR-AMPERE Conductivities* [Data set]. Zenodo. Published 2019-03-27, CC BY 4.0.

A third kind of relationship, and the reason the role labels above are needed. This deposit contains
"the Hall and Pedersen conductances that were derived in support of an AMPERE-PFISR study" — that is,
the conductance values underlying the statistical field-aligned-current-to-conductance relations of
Robinson et al. 2020, which ADELPHI hard-codes as its conductance model. ADELPHI never reads this
dataset at run time; it is upstream of the model's coefficients rather than of its execution.

It is citable because the 2020 paper's acknowledgments name it explicitly, alongside the code that
produced it: *"The code and raw data for calculating conductances from Poker Flat Incoherent Scatter
Radar measurements are available at http://doi.org/10.5281/zenodo.2609955 and
http://doi.org/10.5281/zenodo.2610915, respectively."* The **concept** DOI is recorded above, resolving
to version record `10.5281/zenodo.2610915`. Its creator, Stephen Kaeppler, is a co-author of Robinson
et al. 2020 (ORCID `0000-0003-1932-0330`, recorded in Field 6 among the co-authors not credited as
software authors).

**This does not contradict Field 31's exclusion of PFISR.** The two fields ask different questions.
Field 31 asks whether ADELPHI is *designed to support* an instrument — whether it reads that
instrument's data — and ADELPHI does not read PFISR data, so PFISR is correctly absent there. Field 28
asks which datasets are related to the software, and the conductance dataset derived from PFISR
measurements is genuinely part of ADELPHI's provenance. Both outcomes are correct simultaneously; a
future agent should not "reconcile" them by adding PFISR to Field 31.

The four entries are labelled by role above precisely so that a reader does not mistake them for the
same kind of relationship, and so that a future agent adding another dataset knows which bucket it
belongs in.

### 29. Related Software (OPTIONAL)
- https://ccmc.gsfc.nasa.gov/models/AMGeO~3/ — AMGeO (Assimilative Mapping of Geospace Observations), version 3
- https://ccmc.gsfc.nasa.gov/models/Ovation-Prime~2.3/ — Ovation-Prime, version 2.3
- https://ccmc.gsfc.nasa.gov/models/Weimer~2005/ — Weimer Ionosphere Models, version 2005
- https://doi.org/10.5281/zenodo.2609954 — PFISR-Conductivities (Kaeppler)

The first three are genuinely similar-purpose tools: each specifies high-latitude ionospheric
electrodynamic parameters, and each is a direct alternative a user choosing ADELPHI would weigh against
it. CCMC catalogue URLs are used because these are CCMC-hosted models without software DOIs, which is
the fallback Field 29 allows. The fourth is a different kind of entry — an upstream provenance
dependency — and is justified separately below.

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
- **PFISR-Conductivities** is not a similar-purpose tool but a **predecessor in ADELPHI's provenance
  chain**, which Field 29's scope ("software this work was forked from", "important software
  dependencies", domain-specific dependencies) covers. It is the code that computed Hall and Pedersen
  conductances from Poker Flat Incoherent Scatter Radar files — "a fast method for processing
  quantifying the Hall and Pedersen conductance given Poker Flat Incoherent Scatter Radar h5 files" —
  and it generated the conductance dataset (Field 28, dataset 4) from which Robinson et al. 2020 fitted
  the field-aligned-current-to-conductance relations that ADELPHI hard-codes. It is named, with this
  DOI, in that paper's acknowledgments. Recording it tells a reader something substantive and otherwise
  undiscoverable: where ADELPHI's conductance model came from, and that its empirical basis is
  independently citable and reproducible.

  Practical notes for a future agent. The **concept** DOI is recorded above; it resolves to version
  record `10.5281/zenodo.2609955`, tagged `srkaeppler/PFISR-Conductivities: v0.2` (2019-03-26). The
  live repository is `https://github.com/srkaeppler/PFISR-Conductivities` (Jupyter Notebook, not
  archived, last pushed 2022-05-28) and carries **no license file**, while the Zenodo deposit records
  its licence as `other-at`; the author asks to be contacted before use. It is a genuine
  runtime dependency of neither ADELPHI nor anything else here — the relationship is historical
  derivation, which is why it sits in Field 29 rather than Field 30.

  As with Field 28's dataset 4, this does **not** reopen Field 31: ADELPHI still reads no PFISR data,
  and the instrument exclusion there stands.

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

The relationship is documented in the peer-reviewed literature as well. Ringuette et al. 2022
(`10.3389/fspas.2022.1005977`) lists ADELPHI among the simulation outputs then being added to Kamodo,
and the later Kamodo journal paper, Ringuette et al. 2023, "Kamodo: Simplifying model data access and
utilization" (`10.1016/j.asr.2023.03.033`, *Advances in Space Research*), names ADELPHI among the model
outputs Kamodo supports — by then as a delivered capability rather than a planned one. Semantic Scholar
classifies that citation's intent as *methodology*, consistent with a functional dependency rather than
a passing mention. This is precisely the "one's output can be imported into the other" exchange
Field 30 asks for.

No other package qualifies. ADELPHI has no dependency list to mine — it is unreleased IDL — so there
was no opportunity to mistake generic infrastructure for interoperability here. The one near-miss worth
recording is PFISR-Conductivities (Field 29): it is genuinely related software, but the relationship is
historical derivation of ADELPHI's coefficients rather than any exchange between running programs, so it
belongs there and not here.

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
