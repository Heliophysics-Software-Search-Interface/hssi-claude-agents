# HSSI Metadata Extraction Results

**HSSI Software ID:** ff74234b-46ca-4d5a-9008-fd9e3643f565
**Repository:** https://ccmc.gsfc.nasa.gov/models/ADELPHI~1/ (CCMC model page — authoritative source; ADELPHI has no source-code repository)
**Source Revision:** Not applicable — website-only extraction, no version-controlled source is published, and CCMC exposes no per-model revision or edit timestamp. The "Last Updated" stamp shown at the top of the ADELPHI page is **not** a page-specific edit date and is deliberately not quoted here — see "The 'Last Updated' date on the model page is a trap" below. The nearest durable anchors are CCMC's own `version` value for the model (`1`) and the record content transcribed field by field here.
**Extraction Date:** 2026-08-15
**Validation Date:** 2026-08-15
**Validation Status:** PASS

---

**Scope note — this evidence is website-only.** ADELPHI is an IDL model hosted by NASA's Community
Coordinated Modeling Center (CCMC). No source repository is published in any of the places searched:
GitHub (both repository and code search), GitLab, Zenodo, DataCite and the NASA Software Catalog were
each queried, and none returned an ADELPHI source repository; the searches have since been repeated
with the same empty result. **This is confirmed by the authors
themselves, not merely by failed searches:** the Data Availability Statements of the 2021 and 2018
papers name only the datasets used — the 2021 statement, read from the article, names exactly the
AMPERE web site, SuperMAG and the Kyoto AE service and nothing else; the 2018 one names AMPERE,
TIMED/GUVI and Kyoto — while the 2020 paper's *Acknowledgments* instead name Zenodo DOIs for a
*collaborator's* conductance code and data (Fields 28 and 29). None of the three names an ADELPHI source release
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
  `publicationPolicy`, `figures`, `temporalDependence`, `spaceWeatherImpacts`, and separate
  `inputsDescription` / `outputsDescription` / `caveats` text. It does **not** carry `status`,
  `spaseResourceID` or `host`.
- The **model catalogue listing** (`/models/`) carries the cataloguing fields — `status`,
  `spaseResourceID`, `host` and `services` — alongside a shared core of `name`, `fullName`, `version`,
  `domains`, `phenomena` and `spaceWeatherImpacts`. It does **not** carry `contacts`, `code`,
  `changeLog`, `regions`, `caveats`, `figures`, `publicationPolicy` or the input/output descriptions.

Where a note below attributes a value to "the CCMC model record" it means the individual model page;
where it says "the catalogue record" it means the listing. Both are structured data rather than a
reading of the rendered page.

**The "Last Updated" date on the model page is a trap.** It is displayed prominently at the top of
every CCMC model page and looks like a per-model edit stamp. It is not one, and its behaviour gives it
away on two counts. First, on any given day it reads **identically across unrelated models** —
ADELPHI, AMGeO, Ovation-Prime, Weimer, SWMF, GITM and OpenGGCM all carry the same value, drawn from the
same site build. Second, it **advances with the site build rather than with model content**: it moves
even when nothing about ADELPHI has changed, and it can move more than once within a short span. Both
behaviours have been observed on more than one occasion and across more than one model page, so this is
the stamp's normal operation and not a transient glitch.

What makes the trap convincing is that CCMC's ordinary *content* pages do carry genuine per-page
stamps — the FAQ and the publication policy each show their own, years apart from each other and from
whatever the model pages show. Neither the model record nor the catalogue record exposes any per-model
modification timestamp, and no public CCMC API supplies one. **Do not use this stamp to date the
software, to date a change to the model, or as a pinned revision, and do not quote a particular
reading of it anywhere in this file — any value written down is stale almost immediately.** Fields 10
and 23 both turn on this point, and both previously cited the stamp incorrectly.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** Shawn Polson
- **Submitter Email:** shawn.polson@lasp.colorado.edu

This field is mandatory on the HSSI form but is a property of the *act of submitting*, not of the
software: it records who transmitted the metadata. It is not derivable from ADELPHI's documentation or
from any source examined, and it would be wrong to infer it — the model's developer and CCMC hosts
(Field 6) are contacts for the software, not submitters of this record. The value above is therefore
the person who curated and transmitted this record, and it carries no implication of authorship,
maintenance or stewardship of ADELPHI itself.

For the same reason, this is the one field in this file that describes the record rather than the
software. If the entry is ever re-submitted or transferred by someone else, this value changes and
nothing else in the file does.

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
  already taken; it makes no prediction. The Instant Run service accepts only past dates, and does so
  by construction rather than by convention: its date control is bounded `min="2009-10-02"` to
  `max="2025-02-28"`, so neither a future date nor even a near-present one can be requested.
- **Data Processing and Analysis: Time Series Analysis** — rejected. The 1D outputs are time series at
  2-minute cadence, but the model *produces* them; it does not analyse time series.
- **Data Processing and Analysis: File Format Conversion** — rejected, though it will look tempting:
  ADELPHI reads netCDF input and writes ascii output, so the formats differ across the model. That is
  a model's ordinary I/O, not a conversion capability offered to users; nothing in ADELPHI translates
  one format into another as a service. The genuine ADELPHI-related format converter belongs to Kamodo
  (Field 30) and is credited there.
- **Servers and Environments: Distribution/Access** — rejected on the same grounds as the visualization
  categories below. ADELPHI is *distributed through* CCMC's hosted Instant Run service, but that
  service is CCMC's shared infrastructure across many models rather than a capability of the ADELPHI
  code. Selecting it would attribute the host's function to the guest.
- **Mission-related** — rejected. ADELPHI consumes a mission's data product but is not part of any
  mission ground system, pipeline or operations chain.

### 5. Related Region (MANDATORY)
- Earth Ionosphere
- Earth Auroral Subregion
- Earth Magnetosphere

All three confirmed against the live `Region` vocabulary.

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
(https://ror.org/047yk3s18, whose ROR record carries "CUA" as its acronym). CCMC's acronym-bearing string
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
   independently corroborated by Ringuette et al. 2022 (`10.3389/fspas.2022.1005977`), whose article
   text reads, character for character, "ADELPHI (AMPERE-Derive ELectrodynamic Properties of the
   High-latitude Ionosphere model, Robinson et al., 2021)" — the same wording, carrying two
   typographic slips (a dropped "d" in "Derive" and a stray capital in "ELectrodynamic") that the
   later Kamodo journal paper reproduces. Neither slip changes which expansion is in use.
2. "AMPERE-Derived Electrodynamic **Parameters** of the **High Latitude** Ionosphere" — the title of
   Robinson et al.'s EGU 2019 abstract (ADS bibcode `2019EGUGA..21.3577R`). Attested and from the
   developer himself, but predates the CCMC deployment.
3. "AMPERE Derived **Electrodynamics of the High Latitude Ionosphere**" — as written in Sur et al. 2025
   (`10.1029/2024SW004023`).

A systematic full-text search of the literature for ADELPHI alongside each candidate wording surfaced no
fourth variant, and supports the selected "Properties" form as the best attested. Three attestations of
it are confirmed against primary text:

- the Kamodo journal paper, Ringuette et al. 2023 (`10.1016/j.asr.2023.03.033`);
- Shim et al.'s AGU Fall Meeting 2025 abstract (identified below), which reads "the ADELPHI
  (AMPERE-Derived Electrodynamic Properties of the High-latitude Ionosphere) and Weimer 2005 models";
- Shim et al. 2026, which renders it "AMPERE-derived electrodynamic properties of the high-latitude
  ionosphere (ADELPHI)" — matching CCMC's `fullName` in substance.

**One candidate attestation was tested and rejected, and should not be re-proposed.** Opgenoorth,
"Earth's Geomagnetic Environment — Progress and Gaps in Understanding, Prediction, and Impacts",
45th COSPAR Scientific Assembly 2024 (ADS bibcode `2024cosp...45.2906O`), matches a phrase search for
"Electrodynamic Properties of the High-latitude Ionosphere" and looked like a valuable independent
third-party attestation. It is not one: its indexed abstract, which is the whole of the text available
for that record, uses the phrase generically and contains **no occurrence of "ADELPHI" at all**. The
match is a false positive of exactly the kind the caution below describes, and the file briefly
asserted it before the abstract was read. There is accordingly no confirmed attestation from outside
the ADELPHI and Kamodo author groups; the selection rests on CCMC's own `fullName` plus the three
attestations above, which is sufficient.

The 2019 EGU abstract's own prose also describes the model as giving "global specification of
electrodynamic **properties**", and closes by naming "AMPERE-derived electrodynamic parameters of the
high latitude ionosphere, referred to as ADELPHI", despite that abstract's title using "Parameters".

**A search limitation that bounds every claim above, and that a future agent will otherwise trip on.**
Full-text phrase search over this literature is neither case- nor hyphen-sensitive, and it stems
"Derive" and "Derived" to the same token. It therefore cannot on its own distinguish "High-latitude"
from "High Latitude", nor detect a dropped letter — a query for the misspelled Ringuette wording
returns the correctly spelled papers too. Any character-exact claim about a particular rendering has to
be confirmed against the article text itself, as was done for variant 1 above.

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

**The AGU Fall Meeting 2025 abstract, previously recorded here as unidentified and of doubtful type, is
now positively identified.** It is "Assessing the Accuracy of GDC Measurements Using ADELPHI and Weimer
2005" (ADS bibcode `2025AGUFMSA11D8899S`), typed as a conference *abstract* in *AGU Fall Meeting
Abstracts*, by Shim, Robinson, Garcia-Sage, Rowland, Di Mare, Klenzing and Liu — the same author team as
Shim et al. 2026, of which it is the conference precursor. Its own text expands the acronym in passing,
describing potential and Joule heating "derived from the ADELPHI (AMPERE-Derived Electrodynamic
Properties of the High-latitude Ionosphere) and Weimer 2005 models" — matching CCMC's `fullName`
word for word. It carries no DOI, which is normal for an AGU abstract, so it is cited by bibcode; it is
indexed in ADS, which is where it resolves, and earlier searches of the conference's own programme site
did not surface it.

The earlier doubt arose from a real near-collision that is worth documenting rather than rediscovering.
Shim et al. 2026's reference list *separately* cites "Code for assessing the accuracy of GDC
measurements using ADELPHI and weimer 2005", attributed to Shim (2025). That is a **different artifact**
from the conference abstract despite the near-identical title, and it remains unlocated: it is absent
from DataCite and from Zenodo, and the citation graph carries it only as an unresolved reference with no
DOI. It therefore cannot be cited, and is not a Field 29 candidate. A search for it will keep returning
the abstract; that is the collision, not a match.

The conclusion never depended on any of this: the CCMC model record is the authoritative publisher of
this software entry, and every confirmed primary-text attestation agrees with it. The selected value
should not be changed without something that outranks CCMC's own `fullName`.

Note also that no expansion appears in the rendered body text of the CCMC page; it is carried only in
the structured `fullName` field and the HTML meta description, which is why a casual read of the page
finds the acronym undefined.

### 10. Publication Date (RECOMMENDED)
2025-07-16

The date ADELPHI was published as software — that is, first made available to the community. The
evidence is CCMC's site-wide **change log**, a dated record of service changes that is a separate
document from the model page and from any page timestamp. It carries a single ADELPHI entry,
categorised "Instant Runs / New Feature" and dated 2025-07-16: "The ADELPHI (web simulator) is
available to the community through the CCMC instant run (IR) service via this submission URL." That
change-log entry, and not the page's "Last Updated" stamp, is the source of this value.

Alternative considered and rejected: the publication of the Robinson et al. 2021 reference paper —
2021-04-16 for the version of record, or 2021-03-17 for the accepted manuscript, two genuine stages
that Field 14 sets out. Which stage one picks makes no difference here, because either way that is
when the model was *described* in the literature, and the software itself was not obtainable by anyone
until the CCMC deployment four years later. Field 10 asks for the date of first publication of the
software, so the CCMC availability date is the accurate answer.

The model page's "Last Updated" stamp was also rejected, and the reason is stronger than "it is a
content-management timestamp". The stamp carries no ADELPHI-specific information whatsoever: it is a
site-wide build date, identical across unrelated CCMC model pages and advancing with the site build
while the model stands still (see the provenance note above). It cannot date the software, and an
earlier revision of this file was wrong to argue from its proximity to an extraction date.

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
`changeLog: null` for ADELPHI, the site-wide change log still contains exactly one ADELPHI entry (the
availability announcement, already used above, with no second entry added since), and no release notes
exist. There is also nothing for
such a description to summarise — Field 12 asks for "major changes in the new version", and version 1
is the initial and only version, so it supersedes nothing.

Version PID is absent for the same reason as Field 2: no DOI exists at any level.

**A 2022 "new version" of ADELPHI exists in the literature and does not change this field.** Two AGU
Fall Meeting 2022 abstracts recorded under Field 27 describe "a new version of the ADELPHI auroral
electrodynamics model" and "the latest iteration" of it. Field 12 records the *published* version, and
what CCMC publishes — the only distribution of ADELPHI there is — remains `1`. A research-internal
iteration that was never released, never given a version label by its author, and never reached the
catalogue is not a version of the software in this field's sense. Do not bump Field 12 to `2` or invent
a label for it; if CCMC ever publishes a successor, the version number, its date and a description
would all come from CCMC's own record.

For contrast, CCMC does version other catalogue models actively, and marks the superseded ones
Retired: Ovation-Prime is carried at 1.0 (Retired) and 2.3 (Production), Weimer at 2000 and 2005 (both
Production) plus DeltaB_2012 (Retired), and SuperDARN Convection Models at 4.3.1 (Retired) and 5
(Production). ADELPHI's single Production version, with nothing retired behind it, is therefore a real
property of this model rather than a limitation of CCMC's metadata.

### 13. Programming Language (RECOMMENDED)
- IDL

From CCMC's structured record, `code: {languages: "IDL"}`. `IDL` is an exact row in the live
`ProgrammingLanguage` vocabulary. This is the only language stated, and no source is available to
infer others from.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1029/2020SW002677

Robinson, R. M., Zanetti, L., Anderson, B., Vines, S., & Gjerloev, J. (2021). Determination of auroral
electrodynamic parameters from AMPERE field-aligned current measurements. *Space Weather*, 19(4),
e2020SW002677. Version of record published 2021-04-16; open access under CC BY-NC-ND 4.0.

**Two publication dates circulate for this paper, and both are real.** The publisher's own publication
history, read from the article, distinguishes the stages:

> Issue Online: 16 April 2021 · Version of Record online: 16 April 2021 · Accepted manuscript online:
> 17 March 2021 · Manuscript accepted: 04 March 2021 · Manuscript revised: 02 March 2021 · Manuscript
> received: 31 October 2020

So **2021-03-17** is the accepted-manuscript-online date, which the article masthead itself labels
"First published", and **2021-04-16** is the version-of-record and issue-online date, consistent with
the April 2021 issue (*Space Weather* volume 19, issue 4). Neither is an artifact and neither is a
mistake for the other. This dossier cites 2021-04-16 because it is the date of the citable version of
record that the DOI resolves to, and records 2021-03-17 here so a future agent meeting it — in the
masthead, in a citation manager, or in another paper's reference list — recognises it as the earlier
stage rather than "correcting" one date into the other. The article is Open Access under a single
Creative Commons licence, CC BY-NC-ND 4.0; that is the *article's* licence and has no bearing on
Field 15, which concerns the software.

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
- ionospheric electrodynamics
- ionospheric conductance
- ionospheric convection
- aurora
- auroral electrojet
- electrodynamics
- electron precipitation
- particle precipitation
- field-aligned currents
- joule heating
- cross polar cap potential
- magnetic local time
- magnetosphere-ionosphere coupling
- high-latitude
- geospace
- space weather

Keywords are the one open vocabulary in the form, so the live list was consulted specifically to reuse
existing rows instead of minting near-duplicates. Sixteen of the seventeen above are existing rows and
are reproduced with their exact stored spelling — including the two that look as though they ought to
be normalised and must not be: `high-latitude` (hyphenated, no following noun) and `field-aligned
currents` (hyphenated and plural). Only `ionospheric convection` is new; it is entered lower-case, one
concept per entry, following the spelling pattern of its neighbours `ionospheric conductance` and
`ionospheric electrodynamics`.

**`field aligned` was previously listed here in place of `field-aligned currents`, and has been
replaced.** The reason originally given for the bare fragment was that writing "field-aligned currents"
would mint a third variant of the same concept. That reason does not hold: `field-aligned currents` is
itself an existing keyword row, so selecting it reuses the vocabulary rather than expanding it, and
unlike the adjective fragment it names the actual physical quantity — CCMC's own phenomenon
"Field-aligned Currents", and ADELPHI's sole input. A future agent should not restore the fragment.

This field also absorbs the model characteristics that CCMC records but HSSI's closed vocabularies
cannot hold, and it is now complete with respect to them. CCMC lists seven phenomena for ADELPHI —
Ionosphere Electrodynamics, Particle Precipitation, Energy Flow into Ionosphere, Joule Heating,
Ionosphere Convection, Field-aligned Currents, and Cross-polarcap Electric Potential — of which none
has a row in HSSI's closed `Phenomena` list (Field 22). Per Field 22's instruction, phenomena with no
row belong in Keywords, so all seven are carried here. Six map one-to-one onto
`ionospheric electrodynamics`, `particle precipitation`, `joule heating`, `ionospheric convection`,
`field-aligned currents` and `cross polar cap potential`. The seventh, "Energy Flow into Ionosphere",
has no tolerable single-term equivalent and is carried jointly by `joule heating` and
`electron precipitation`, which are precisely the two channels through which ADELPHI computes that
energy flow. `electron precipitation` is kept alongside `particle precipitation` because ADELPHI's flux
relation is specifically an electron-energy-flux relation (Robinson et al. 2018), which is more precise
than CCMC's general term; both are existing rows, and keeping both maximises the ways a user finds this
record.

CCMC's two `domains` values, "Geospace" and "High Latitude Ionosphere / Auroral Region", supply
`geospace` and `high-latitude`, both existing rows. `magnetosphere-ionosphere coupling` is included
because the field-aligned currents driving ADELPHI *are* the M-I coupling currents; that is the same
physical reasoning that puts `Earth Magnetosphere` in Field 5, and the two fields are kept consistent
deliberately. `space weather` rests on CCMC's `spaceWeatherImpacts` values for the model —
"Geomagnetically induced currents - GICs (electric power systems)" and "Ionosphere variability
(navigation, communications)" — which are recorded in CCMC's structured data but have no HSSI field of
their own.

`idl` exists as a keyword row and was considered, but rejected as redundant with Field 13.

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific

Confirmed against the live `DataInput` vocabulary. ADELPHI reads exactly one data source: AMPERE
field-aligned current files, obtained from the AMPERE project rather than from any general-purpose
archive. Field 17 explicitly directs that an observatory-specific source be marked as such with the
mission named in Related Observatory, which is done in Field 32.

Rejected: `CDAWeb`, `HAPI`, `OMNIWeb`, `Madrigal`, `SSCWeb` and the other archive rows — ADELPHI does
not retrieve from any of them; the AMPERE files are staged locally by filename convention. `Other` was
rejected as strictly less informative than the applicable specific row. One further trap: the junk row
`Other - https://xrt.cfa.harvard.edu/level1/` still exists in the production `DataInput` vocabulary but
has been retired locally, so the two vocabularies differ by exactly that row. It is never a valid
selection for anything.

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
reader. The statement lives in the reader's own docstring in `kamodo_ccmc/readers/adelphi_4D.py`, which
Kamodo's model-reader documentation renders: "ADELPHI model outputs are produced in ascii form
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
actively developed; support provided as time allows", is supported by CCMC publishing a single version
(`1`) with no successor, `changeLog: null` and no release notes, and by CCMC continuing to *support*
the model through two named model hosts — which is exactly the "support provided as time allows" the
definition anticipates.

**ADELPHI was, however, still being refined in 2022, and this field's reasoning has to account for
that rather than pass over it.** Two AGU Fall Meeting 2022 abstracts, recorded under Field 27, have
Robinson himself describing work on the model: `2022AGUFMSA25C1937R` (Robinson first author) states
that field-aligned current data "are used as input to a new version of the ADELPHI auroral
electrodynamics model that improves the electric potential specification in the vicinity of the
magnetic pole", and `2022AGUFMSA24B..01D` (Robinson a co-author) refers to "the latest iteration of
the ADELPHI auroral electrodynamics model". An earlier revision of this file argued from "a reference
publication from 2021 with no subsequent model paper", which those abstracts contradict; that sentence
has been removed.

`Inactive` nevertheless remains the best-supported value, for three reasons that survive the 2022
evidence. First, the refinement is research-internal: it produced no released version, and the polar-cap
potential improvement never reached CCMC's catalogue, which still publishes version `1`. Second, the
activity is confined to 2022 — nothing in 2023 through the present indicates continuing code
development, and the only later event of any kind is the 2025 deployment announcement, which is a
hosting milestone rather than a development one. Third, repostatus `Inactive` describes a project that
has reached a stable usable state and is no longer *actively* developed; a burst of work three or more
years in the past, with no published outcome and no continuation, does not make a project actively
developed today. Should evidence of current development appear, `Active` becomes correct.

`Active` was considered and rejected on the evidence set out above. The 2025-07-16 Instant Run
deployment, in particular, is evidence of CCMC's *curation and deployment* rather than of ongoing
development of the model code — and development of the code is what this field asks about. A recent-looking page timestamp is **not**
a second piece of evidence and must not be read as one: the "Last Updated" date on the model page is a
site-wide build stamp (see the provenance note above) that moves whether or not anything about ADELPHI
changes. An earlier revision of this file cited it as a model-page edit and drew inferences from it;
that was wrong, and no page-timestamp argument should be reintroduced. Should the developer or CCMC
later confirm active code development, `Active` would become correct; nothing currently available
supports it. `Unsupported` was rejected outright, since named CCMC hosts and a
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
hour and hemisphere, with no explanatory content. One access fact from that form is worth carrying here
even though the form is not documentation, because it is stated nowhere else: the username it asks for
is an **AMPERE** account credential ("Enter Your AMPERE username"), so running ADELPHI through CCMC
requires an AMPERE data account rather than merely a CCMC one.

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

That quotation is the complete Acknowledgments section of the paper, transcribed from the article
itself — not a summary of it and not an inference from indexed metadata. Both sentences and all four
award numbers are inside that section, and nothing else is. The tiering below therefore rests on the
primary text.

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
- **Award Title:** NASA Cooperative Agreement
- **Award Number:** NNG11PL10A

**Award 2**
- **Award Title:** TIMED/GUVI Project
- **Award Number:** NNX14AK74G

**Award 1's title is descriptive, not formal, and should not be "corrected" to Not found.** No formal
title for `NNG11PL10A` exists in any source examined: the acknowledgment describes it only as a "NASA
Cooperative Agreement", associated with the Community Coordinated Modeling Center, and gives no formal
title; none was found in a funder database either. That negative research stands. The recorded title is
therefore the authors' own descriptive phrase, lifted from the acknowledgment.

It is recorded rather than left empty because an award cannot be held without a title — a title is
required, so an award carrying only a number cannot be stored. Leaving it empty would not have
preserved "no formal title is known"; it would have dropped `NNG11PL10A` from the record altogether,
losing the award number, which is the part that actually identifies the grant. A descriptive title of
record is the lesser distortion.

Award 2's title rests on exactly the same basis: it is the project name the authors themselves give it
— *"the TIMED/GUVI Project (NASA grant NNX14AK74G)"* — rather than a formal award title from a funder
database, which was not located. Both entries are therefore consistent with each other, and the caveat
covers both: **neither title should be mistaken for the grant's official title**, and neither should
prompt a future agent to go hunting for a formal title in the belief that one was already found. If an
official title for either award is ever located, replacing the descriptive phrase would be a genuine
improvement.

**What these two awards actually represent — read this before narrowing further or re-expanding.** The
acknowledgment does not identify any award as funding ADELPHI's implementation specifically. These two
are the **standing support under which Robinson's group produced this research line**: the first two
sentences of the acknowledgments are near-identical across all three CCMC-listed papers (2018, 2020 and
2021 — the 2018 one lacking only the CCMC clause), and the same two NASA awards recur in the fourth
Robinson paper as well (Robinson & Zanetti 2021, Field 27), whose funding is *only* these two. That
recurrence is evidence they are the group's block support, not per-paper line items. The pattern was
checked award by award across all four papers' acknowledgements sections and holds exactly, including
the 2018 paper's missing CCMC clause and the complete absence of NSF from Robinson & Zanetti 2021,
whose registered funding metadata likewise lists only these two NASA awards. Listing them is
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
  grant NASA NNX08AM32G S03."* That placement is attested in the article itself, where the Data
  Availability Statement is a separate section immediately following the Acknowledgments: these three
  award numbers appear in it and in no other part of the paper, and the Acknowledgments section
  contains none of them. SuperMAG is a third-party service used
  only to validate ADELPHI's modeled indices; ADELPHI does not read its data. Excluding its funders here is the same judgement
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
- https://doi.org/10.1029/2025JA034684 — Shim, J. S., Robinson, R. M., Garcia-Sage, K., Rowland, D. E., Di Mare, F., Klenzing, J., & Liu, G. (2026). Evaluating Multipoint Sampling of Global-Scale High-Latitude Electrodynamics by the Geospace Dynamics Constellation. *Journal of Geophysical Research: Space Physics*, 131(1), e2025JA034684. Published 2026-01-14; open access under CC BY-NC 4.0.
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

- **Two AGU Fall Meeting 2022 abstracts that document post-2021 ADELPHI development.** These are the
  most substantive ADELPHI records not carried as values in this field, and they are recorded here in
  full because they are easy to miss — neither is indexed by DOI, and neither surfaces from a citation
  search of the reference publication:
    - Robinson, R. M., Dinsmore, R., Mathews, J. D., & Thayer, J. P. (2022). *Multi-Instrument Study of
      Joule Heating in the Polar Cap during Northward Interplanetary Magnetic Field.* AGU Fall Meeting
      Abstracts. https://ui.adsabs.harvard.edu/abs/2022AGUFMSA25C1937R — states that the AMPERE
      field-aligned current data "are used as input to a new version of the ADELPHI auroral
      electrodynamics model that improves the electric potential specification in the vicinity of the
      magnetic pole."
    - Dinsmore, R., Mathews, J. D., Robinson, R. M., & Urbina, J. V. (2022). *TID Generation and
      Propagation Linked to a Minor Solar Wind Pressure Pulse via Multi-Instrument Observations.* AGU
      Fall Meeting Abstracts. https://ui.adsabs.harvard.edu/abs/2022AGUFMSA24B..01D — states that Joule
      heating "is estimated via AMPERE data and the latest iteration of the ADELPHI auroral
      electrodynamics model."

  Both genuinely *use* the software, and ADELPHI's own developer is an author of each, so they meet
  Field 27's substantive test. They are nonetheless kept out of the value list above as a judgement
  about kind, not eligibility — a point worth stating plainly, because the obvious inference is the
  wrong one. **The absence of a DOI is not what excludes them:** Field 27 expressly allows an APA
  citation with a permanent link where no DOI exists, and the ADS links above are stable. What excludes
  them is that they are unrefereed meeting abstracts, whereas every entry in the list above is a
  refereed work of record; interleaving the two would misrepresent the abstracts' standing to a reader
  scanning the field. The same treatment is applied consistently to the other ADELPHI conference
  abstracts, which appear in Fields 9 and 23 rather than here. A future curator who prefers maximal
  coverage may promote them, and the citations are written above in the exact form the field requires
  so that no re-derivation is needed.

  Their real weight is evidential rather than bibliographic: they are the only public record that
  ADELPHI was refined after its 2021 reference publication, and Field 23's development-status reasoning
  turns on them.
- Ringuette et al. 2022 (`10.3389/fspas.2022.1005977`), the Kamodo flythrough paper, and Ringuette et
  al. 2023 (`10.1016/j.asr.2023.03.033`), the Kamodo journal paper — both mention ADELPHI only as a
  supported model output. The relationship they document is interoperability and is recorded in
  Field 30, where it belongs.
- Zhu et al. 2022, "Assessment of Using Field-Aligned Currents to Drive the Global Ionosphere
  Thermosphere Model" (`10.1029/2022SW003170`). This one is worth recording explicitly because it looks
  like a candidate and is not — and it looks more like one than the original note conveyed: the
  citation graph flags it as an *influential* citation of Robinson et al. 2021, with background, result
  and methodology intents. But its citation contexts show it discussing ADELPHI as *related work* —
  "Robinson et al. (2021) developed another technique to calculate the high-latitude electric
  potential" — while driving GITM with its own conductance treatment. It uses the published method's
  context, not the software. An influence flag is not evidence of software use, and must not be allowed
  to promote this paper on a later pass.
- **The recent citing literature, examined as a block.** Robinson et al. 2021 keeps accumulating
  citations, and the ones postdating this dossier's first compilation were checked individually rather
  than assumed irrelevant: the 2024 Gannon-storm study (`10.1029/2025SW004699`), two *Annales
  Geophysicae* papers (`10.5194/angeo-44-149-2026` and `10.5194/angeo-44-697-2026`), an inductive
  magnetosphere-ionosphere-thermosphere coupling paper (`10.5194/angeo-43-803-2025`), the
  TRICE-2/TRACERS review (`10.1007/s11214-025-01178-2`) and a small-mission concept paper
  (`10.1016/j.actaastro.2026.05.057`). Each cites Robinson et al. 2021 for a *number or a method* — a
  2 mho background conductance, the field-aligned-current-to-conductance relation, or membership in a
  list of potential-derivation techniques — and none names ADELPHI or uses the model. They are
  correctly excluded, and a future agent re-running the citation query should expect to meet them.

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

Resolved against HSSI's controlled instrument/observatory vocabulary. That vocabulary was re-checked in
full when this dossier was last revised and remains entirely SPASE-backed: every row carries an
`https://spase-metadata.org/` identifier and none fails the guard. Treat that as a dated observation
rather than an invariant — the guard must keep being applied, and any row that fails it signals
upstream drift or a row an agent wrongly created, and must be reported rather than used. Exactly one
instrument row corresponds to the measurement chain ADELPHI consumes, so this is a clean single-row
match; the name is copied verbatim from the row. Fields 31 and 32 are SPASE-only: a name without an
identifier creates a new identifierless row, so neither field may ever carry a bare name.

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
- **Resolute Bay Incoherent Scatter Radar (RISR) and DMSP** — named in the 2022 AGU abstract recorded
  under Field 27, where they verify the conductances and particle fluxes of an ADELPHI-based study.
  Excluded on precisely the same ground as PFISR, GUVI and SuperMAG above: they are verification
  measurements in a study that *uses* ADELPHI, not data the model reads. A future agent meeting that
  abstract should not read the instrument list in it as ADELPHI's input list.

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
- **TIMED**, stored under the canonical row name `Thermosphere-Ionosphere-Mesosphere Energetics and
  Dynamics` (`https://spase-metadata.org/SMWG/Observatory/TIMED`) — omitted for the same reason as its
  GUVI instrument under Field 31. The stored name is recorded because searching the vocabulary for a
  row literally named "TIMED" finds nothing, and a future agent could mistake that for the row being
  absent.

### 33. Logo (OPTIONAL)
**Not found**

ADELPHI has no logo. The only image on the CCMC model page is CCMC's own site logo
(`https://ccmc.gsfc.nasa.gov/static/images/logo2.png`), carried in the page's Open Graph metadata as
the site-wide default; it identifies CCMC, not this model, so it must not be recorded here. That it is a
site-wide default rather than ADELPHI's own image was confirmed rather than assumed: the identical
`og:image` value is served by other CCMC model pages checked for comparison (AMGeO, Ovation-Prime,
Weimer and SWMF). CCMC's model-page record for ADELPHI also has an empty `figures` array. With no
repository, there is no assets directory or README badge to draw on either.
