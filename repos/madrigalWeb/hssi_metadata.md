# HSSI Metadata Extraction Results

**HSSI Software ID:** d7baab30-c95a-40e7-b076-287fb90de9d5
**Repository:** https://github.com/MITHaystack/madrigalWeb
**Source Revision:** fc444d288173150473b21771560e2ab174713aca
**Extraction Date:** 2026-09-04
**Validation Date:** 2026-09-05
**Validation Status:** PASS

---

**Scope note — the software's scientific domain lives in the archive it talks to, not in its own
source, and that changes how most of this evidence reads.** madrigalWeb is a thin, dependency-free
(`dependencies = []` in `pyproject.toml` at the pin) HTTP client for the Madrigal distributed
upper-atmospheric database. Its 10 Python files at the pinned revision contain almost no domain
vocabulary: an unanchored, case-insensitive `git grep -ciP` over all 26 tracked paths at
`fc444d288173150473b21771560e2ab174713aca` returns **zero** files for each of `ionosph`,
`thermosph`, `mesosph`, `magnetosph`, `atmosph`, `plasma`, `aurora` and `space weather` (controls:
`python` matches 21 files, `zzqqxx` matches none); `geospace` appears on exactly one line,
`CITATION.cff:58`, as a keyword. The one domain-ish word that is common is `radar` (33 lines across
6 files), and reading them line by line shows why that is not a domain signal either: most belong to
the `radarToGeodetic`/`geodeticToRadar` coordinate-conversion API — method names, the `radarRange`
parameter, the `radarToGeodeticService.py` and `geodeticToRadarService.py` endpoint names, and their
tests — and the rest are docstring example strings
(`Example: 'Millstone Hill Incoherent Scatter Radar'.` and `Example: 'Incoherent Scatter Radars'.`)
plus one repeated CLI usage example. Not one of them states which radars the software supports.

Two consequences follow, and they govern several fields below:

1. **A field that describes the science must be argued from Madrigal's holdings and from the public
   API's semantics, never from a text search of the tree.** Searching this repository for
   "ionosphere" returns nothing at this revision, and a future agent who reads that as "no
   ionospheric association" will reach the wrong answer. Fields 5, 16 and 22 are decided this way.
2. **A field that describes what the software is built to touch must be argued from the tree, and
   the tree is deliberately facility-agnostic.** The package hard-codes no instrument, no
   observatory and no site: every facility name in it is illustrative. Fields 31 and 32 are decided
   this way, in the opposite direction from Field 5.

Also note two tooling facts that changed answers during this work and would change them again.
`git grep -E` silently drops `\b` on this host — the control `git grep -lE '\bJicamarca'` returns 0
files while `git grep -lP '\bJicamarca'` and an unanchored `git grep -l 'Jicamarca'` each return 5 —
so every sweep recorded here used `-P`, and any re-derivation must too. And the HSSI view rendering
title-cases stored keywords, so Field 16's stored values are the lower-case strings recorded there,
not the Title Case a rendered record displays.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This placeholder is the catalogue convention for a record we did not originally submit, not a
missing value. The submitter identity is not ours to assert and is not something a metadata refresh
should overwrite.

---

### 2. Persistent Identifier (RECOMMENDED)
**Not found — no persistent identifier exists for this software.**

This is a researched negative, not an unexamined gap, and it should not be reopened without new
evidence.

- The repository declares none. `CITATION.cff` at the pin has no `doi:` and no `identifiers:`
  block; `README.md` has no DOI badge (the tree contains no badge or image reference of any kind —
  see Field 33); there is no `.zenodo.json` and no `codemeta.json` among the 26 tracked paths.
- **Zenodo holds no deposit for this software** — though a title-keyed search alone would not prove
  it. `title:madrigalWeb` and `metadata.title:madrigalWeb` each return 0, and the two query forms
  are equivalent: on each word probed for this record (`pysat`, `madrigal`, `madrigalWeb`, `kaipy`)
  the bare `title:` and prefixed `metadata.title:` forms returned identical totals, so a future
  agent should not treat switching prefixes as a fix for a title-keyed zero. **What makes such a
  zero weak evidence is tokenization.** Zenodo's fielded title search does not match a bare word
  that occurs only inside a compound repo-style title: `title:pysat` returns 0 even though a
  free-text `pysat` query returns 23 records with titles such as `pysat/pysat: v3.2.2` and
  `pysat/pysatSeasons: v0.2.1`, whereas `title:madrigal` returns 38 and `title:kaipy` returns 1
  because those words stand alone. A title-keyed zero is suggestive here, not decisive.
- **The negative rests instead on routes that do not require the software's name to be spelled
  anywhere.** `metadata.related_identifiers.identifier:"https://github.com/MITHaystack/madrigalWeb"`
  returns 0, which rules out a GitHub–Zenodo integration deposit whatever it might have been titled;
  and a free-text `madrigalWeb` query returns 2 records, both SRI International deposits titled
  around "Integrated Geosciences Observatory" (`https://doi.org/10.5281/zenodo.3466077` and
  `https://doi.org/10.5281/zenodo.3564835`) and unrelated to this package. The creator-keyed and
  release-event checks below close the remainder.
- **Creator-keyed searches close the name-independent gap.** A title search cannot find a deposit
  that never spells the software's name, so the author names were searched too: `Rideout` returns 35
  Zenodo records and `Cariglia` returns 4, and none of them is this software. A caution for a later
  refresh: several of the `Rideout` records belong to **Jai Ram Rideout, a bioinformatician**, not to
  William Rideout of MIT Haystack — do not treat a `Rideout` hit as this author without checking.
- The GitHub repository has **0 tags and 0 published releases**, so there is no release event that a
  Zenodo integration could ever have minted a DOI from.

**Considered and rejected: the two Madrigal presentation DOIs.** Two Zenodo presentations exist and
are recorded under Field 27, but neither may be recorded here. A presentation is not the software:
recording its DOI in Field 2 would make the page render a "Software" citation block asserting that
the presentation *is* the citable artifact for madrigalWeb, which is false. Field 2 stays empty
until the project mints a DOI for the code itself.

---

### 3. Code Repository (MANDATORY)
**https://github.com/MITHaystack/madrigalWeb**

Corroborated from four independent directions: `CITATION.cff`'s `repository-code`,
`pyproject.toml`'s `Homepage` and `GitHub` project URLs, the PyPI record's `project_urls.GitHub`,
and the live PyHC registry entry's `code` field. The repository is not archived, not a fork, and its
default branch is `main`.

The PyPI `project_urls.GitHub` match is what closes package identity: the PyPI name `madrigalWeb`
could in principle belong to some other project, but its declared GitHub URL is exactly this
repository. (`madrigal-web` and `madrigal_web` both 404 on the PyPI JSON API, with a nonsense-name
control also returning 404, so there is no rival normalization of the name to worry about.)

---

### 4. Software Functionality (RECOMMENDED — treated as critical)

- **Coordinate Transforms**
- **Coordinate Transforms: Magnetospheric**
- **Data Processing and Analysis**
- **Data Processing and Analysis: Analysis**
- **Data Processing and Analysis: Data Access and Retrieval**
- **Data Processing and Analysis: Data Reduction**
- **Data Processing and Analysis: Field-line Tracing**
- **Data Processing and Analysis: File Format Conversion**

All eight values are confirmed against the public API of `madrigalWeb/madrigalWeb.py` at the pin.
Every subcategory has its parent present, so the set is structurally sound. Values are written in
the fully qualified `Parent: Child` form because the vocabulary's 83 rows carry only 67 distinct
names — 13 child names recur under more than one parent, so a bare child name is ambiguous.

**Evidence, per value.** The class `MadrigalData` is the whole user-facing surface; these are its
methods.

- **Data Access and Retrieval** — the package's reason to exist. `getAllInstruments`,
  `getExperiments`, `getExperimentFiles`, `getExperimentFileParameters`, `listFileTimes`,
  `downloadFile`, `downloadWebFile` and `isprint` are all remote queries against a Madrigal server's
  CGI services. `setup.py`'s `scripts=` installs four command-line scripts —
  `globalDownload.py`, `globalIsprint.py`, `globalCitation.py` and `exampleMadrigalWebServices.py`
  — of which the first three wrap this same capability for the command line, while
  `exampleMadrigalWebServices.py` is a demonstration script whose own docstring says it
  "runs an example of the Madrigal Web Services interface", not a capability wrapper.
- **Data Reduction** — the client does not merely fetch whole files; it asks the server for a
  reduced subset. `isprint` takes a `parms` argument (a comma-delimited parameter list)
  and a `filters` argument, and `globalIsprint.py` documents numeric range filters over measured or
  derived parameters, with examples including `--filter=ti,500,1000` and
  `--filter=gdalt,200,300or1000,1200`. Experiment- and file-level filtering (`--startDate`,
  `--endDate`, `--seasonalStartDate`, `--expName`, `--fileDesc`, `--kindat`) reduces the retrieved
  set further.
- **File Format Conversion** — the *same* server-side file is delivered in a caller-chosen format.
  `downloadFile` validates with `if format not in ("hdf5", "ascii", "simple", "netCDF4")` and raises
  `ValueError` otherwise; `isprint`'s `outputFile` argument selects the format from the extension
  (`.h5`/`.hdf`/`.hdf5` for Madrigal HDF5, `.nc` for netCDF4, otherwise column-delimited ascii). The
  format is a client-side choice applied to one stored dataset, which is precisely format conversion
  rather than mere download.
- **Analysis** — the `madCalculator` family (`madCalculator`, `madCalculator2`, `madCalculator3`,
  `madTimeCalculator`) computes grids and time series of *derived* physical quantities on demand.
  The docstring examples request magnetic field magnitude and north component (`'bmag,bn'`), shadow
  height with Kp (`'sdwht,kp'`), Kp with Dst (`'kp,dst'`), and a mixed measured/model set
  (`parms='bmag,pdcon,ne_model'`); `exampleMadrigalWebServices.py:126` requests
  `"sdwht,kp,ne_iri"`. These are scientific derivations, not file transport.
- **Field-line Tracing** — `traceMagneticField` (defined at `madrigalWeb/madrigalWeb.py:1908` at the
  pin). Its docstring summary line is `Trace a magnetic field line for each point specified.`, and
  the body explains that it traces to the conjugate point, to a given altitude in the northern or
  southern hemisphere, to the apex, or to the GSM XY plane, selected by the `qualifier` argument.
  (That sentence is wrapped across four source lines in the numpydoc block, so it is paraphrased
  here rather than quoted; the individual parameter lines quoted below are each contained on one
  line and are byte-exact.)
- **Coordinate Transforms** *(parent)* — three distinct user-facing conversions. `radarToGeodetic`
  converts radar azimuth/elevation/range to geodetic latitude, longitude and altitude;
  `geodeticToRadar` inverts it; and `traceMagneticField` converts between geodetic and GSM at both
  ends of the trace.
- **Coordinate Transforms: Magnetospheric** — carried specifically by `traceMagneticField`, whose
  parameter documentation reads `0 for geodetic, 1 for GSM.` for both `inputType` and `outputType`,
  `0 for Tsyganenko, 1 for IGRF.` for `model`, and enumerates the qualifier choices as
  `0 for conjugate, 1 for north_alt, 2 for south_alt, 3 for apex, 4 for GSM XY` (the phrase
  continues onto the next source line with `plane.`). GSM is a magnetospheric coordinate system,
  and the transform is exposed directly to the caller. The radar/geodetic pair is a geographic
  conversion with no subcategory of its own; it supports the parent value but not this one.

**Considered across the full 83-row vocabulary and rejected.** These are recorded so a later refresh
does not reopen them without new evidence.

- **`Coordinate Transforms: Ionospheric`** — rejected. There is no AACGM, no magnetic local time, no
  magnetic latitude and no apex-coordinate transform anywhere in the package. This is the single
  most tempting wrong answer for an ionospheric data client, and it is wrong: the software's only
  magnetic-coordinate capability is the GSM/geodetic pairing in `traceMagneticField`, which is
  magnetospheric.
- **Every `Models and Simulations:` subcategory, `Empirical` above all** — rejected. The
  `madCalculator` family can *request* IRI, Tsyganenko and IGRF outputs (the `ne_iri` and `ne_model`
  parameters; the `model` argument documented as `0 for Tsyganenko, 1 for IGRF.`), but every one of
  those is evaluated on the Madrigal server. The package implements
  no model: it has no numerical solver, no coefficient tables, and `dependencies = []`. A user
  filtering for empirical models wants a model implementation and would be misled to land here.
- **`Data Processing and Analysis: Processing`** — rejected as redundant. It would be defensible as
  a catch-all, but `Analysis`, `Data Reduction` and `File Format Conversion` already name what the
  package does with more precision, and a fourth generic sibling adds no discriminating signal for a
  searcher.
- **`Data Processing and Analysis: Time Series Analysis`** — rejected. `madTimeCalculator`
  *generates* a time series of derived parameters over a range (its example returns Kp and Dst at
  daily steps); it does not analyze one. There is no filtering, detrending, correlation or spectral
  method in the package.
- **Every `Data Visualization:` subcategory** — rejected. The package produces no figures at all; it
  has no plotting dependency and no plotting code.
- **Every `Mission-related:` subcategory** — rejected. Madrigal is a ground-based science archive,
  not a space mission, and this package is a third-party-usable client rather than any mission
  ground-system component.
- **`Servers and Environments: Data servers processing and handling` and
  `Servers and Environments: Distribution/Access`** — rejected. The package is unambiguously the
  *client* half of the exchange; the Madrigal server software is a separate product.

---

### 5. Related Region (RECOMMENDED — treated as critical)

- **Earth Atmosphere**
- **Earth Ionosphere**
- **Earth Lower and Middle Atmosphere**
- **Earth Magnetosphere**
- **Earth Thermosphere**

HSSI held two of these before this refresh, `Earth Atmosphere` and `Earth Magnetosphere`; the three
specific rows are added here. A sixth candidate, `Earth Auroral Subregion`, was weighed and not
selected — its supporting evidence is set out below so that a later refresh recognises it as a
considered choice rather than an oversight.

**The vocabulary is flat.** All 24 `Region` rows are top-level; parent/child links exist in the
model but are empty. A coarse value therefore never implies a fine one and a fine value never
implies its coarse parent, so "`Earth Atmosphere` already encompasses the thermosphere" is not a
valid argument for leaving the specific rows off — before this refresh, a user filtering
`Earth Thermosphere` simply did not get this record. This is also why the campaign precedent is to
*add* specific regions alongside a coarse one rather than replace it.

**The evidence is Madrigal's holdings, not the repository.** Per the scope note, the tree names no
region. What the software is *for* is determined by what is in the archive it reaches. The
authoritative inventory is the live instrument list from
`https://cedar.openmadrigal.org/getInstrumentsService.py`, which as fetched on 2026-09-04 returns
302 registered instruments whose category column distributes as: SCINDA Scintillation Receivers 53,
Fabry-Perots 41, Meteor Radars 39, Incoherent Scatter Radars 31, Magnetometers 19, MF Radars 18,
Individual Ground Based Satellite Receivers 17, Imagers 14, Lidars 10, HF Radars 10, Photometers 9,
Ionosondes 7, Modelled data 6, Michelson Interferometers 6, Satellite Instruments 5, Geophysical
Indices 4, MST Radars 3, Distributed Ground Based Satellite Receivers 3, Coherent Scatter Radars 3,
Riometers 2, VLF 1, Ground Based Solar Receivers 1. The CEDAR portal describes the collection as
"an upper atmospheric science database used by groups throughout the world". Because this inventory
lives upstream and changes over time, it is cited here as an as-fetched observation with its date,
not as a fixed property of the software.

**Judged from the searcher's side** — would a visitor browsing a region and asking "show me software
for this region" be glad or annoyed to find madrigalWeb?

- **`Earth Ionosphere` — the strongest of the five.** The 31 incoherent scatter radars, 7 ionosondes,
  53 SCINDA scintillation receivers, 20 ground-based satellite receivers (17 individual and 3
  distributed), 3 coherent scatter radars, 10 HF radars and 2 riometers are all ionospheric
  instruments, and the package's own `isprint` example requests `'gdlat,glon,gdalt,ne'` — electron
  density. A user hunting for ionospheric software who did *not* find the standard client for the
  CEDAR Madrigal archive would be badly served. Before this refresh the record carried no
  ionospheric region at all, which was the single most consequential gap in it.
- **`Earth Thermosphere`.** 41 Fabry-Perot interferometers and 6 Michelson interferometers
  measure thermospheric neutral winds and temperatures, and incoherent scatter radars deliver
  ion/neutral temperatures through the same API. Two of the four published papers that used this
  package (Field 27) are studies of F-region neutral winds, which is direct evidence that
  thermospheric researchers actually reach for it.
- **`Earth Lower and Middle Atmosphere`.** 39 meteor radars, 18 MF radars, 3 MST radars and 10
  lidars sample the mesosphere and lower thermosphere. This is a large, distinct block of the
  archive that no other candidate region covers, and nothing else in this record would surface the
  software to someone working at those altitudes.
- **`Earth Atmosphere`.** With a flat vocabulary this coarse row is not redundant with the
  three specific additions; it is the value that catches a user who browses at the coarse level. It
  is also the honest label for a client that spans the whole neutral-atmosphere column.
- **`Earth Magnetosphere` — with the argument stated so it is not merely inherited.** This
  value deserves scrutiny because it is the one a reviewer would most likely challenge. It earns its
  place two ways. First from the API: `traceMagneticField` is a magnetospheric capability, and it
  traces to the conjugate point, the apex and the GSM XY plane using Tsyganenko or IGRF fields — a
  user doing magnetospheric mapping can use this package directly for that. Second from the
  holdings: 19 ground magnetometers, plus the five `Satellite Instruments` entries (POES Spacecraft
  Particle Flux, DMSP-Auroral Boundary Index, Defense Meteorological Satellite Program, Van Allen
  Probes, Jason/Topex Ocean TEC), of which Van Allen Probes and POES particle flux are
  magnetospheric measurements. The counter-argument — that Madrigal is fundamentally a ground-based
  upper-atmosphere archive and a magnetosphere researcher would find this record slightly out of
  place — is real but weaker than the field-line-tracing capability, and removing a recorded value
  needs a stronger case than "not the best fit."
- **`Earth Auroral Subregion` — considered and not selected.** The evidence supporting it is real
  and stays on this page: 14 imagers and 9 photometers in the archive are auroral instruments, the
  archive carries the DMSP-Auroral Boundary Index as a named holding, and of the four papers listed
  in Field 27 one is explicitly about the nightside auroral oval while another studies substorm-time
  response. Weighed against it: the auroral instruments are a modest slice of the 302, and the
  package itself is entirely agnostic to them. The row was not taken. **This was a choice between
  two defensible answers, not a refutation of the auroral evidence** — a later refresh that
  rediscovers the imager and photometer holdings has not found something this one missed, and that
  evidence alone is not grounds to add the row.

**Rejected outright:** every non-Earth row — `Chromosphere`, `Corona`, `Photosphere`,
`Solar Environment`, `Solar Interior`, `Solar Wind`, `Interplanetary Space`, `Heliosheath`,
`Planetary Magnetospheres` and the five per-planet magnetosphere rows. Madrigal is an Earth
upper-atmosphere archive. (The single `Ground Based Solar Receivers` instrument is a solar-radio
receiver used as an ionospheric probe, not a solar-atmosphere observation, and does not open the
solar rows.) Also rejected: `Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`,
`Earth Magnetosheath` and `Earth Magnetotail` — the field-line-tracing capability is not specific to
any one magnetospheric subregion, and picking one would assert precision the software does not have.

---

### 6. Authors (MANDATORY)

**William Rideout**
- **Author Identifier:** https://orcid.org/0000-0002-1591-4855
- **Affiliation — Organization:** MIT Haystack Observatory
- **Affiliation Identifier:** Not recorded (see the escalation note below)

**Katherine Cariglia**
- **Author Identifier:** Not found
- **Affiliation — Organization:** MIT Haystack Observatory
- **Affiliation Identifier:** Not recorded (see the escalation note below)

(The order above is presentational only and is not HSSI's stored order; any later correction should
be expressed by author name, never by position in this list.)

**Both authors and both affiliations are correct and complete as recorded, and no identifier change
arises from this refresh.** `CITATION.cff` at the pin lists exactly these two people, gives both
`affiliation: MIT Haystack Observatory`, gives Rideout the ORCID above, and gives Cariglia no ORCID.
`pyproject.toml` at the pin names the same two people in the same order, with the given name
rendered as "Bill Rideout" rather than "William" — the CITATION.cff form is the more formal one and
is what is recorded.

**The ORCID record was read in full and confirms the person, not the affiliation string.** ORCID
`0000-0002-1591-4855` resolves to William Rideout with a single public employment: organization name
`Massachusetts Institute of Technology`, department `Atmospheric Science Group`, city recorded
upstream as `Westoford` (MIT Haystack is in Westford, MA — the misspelling is in the ORCID record
itself), region MA, country US, start date 2001-07-30 with no end date, disambiguated by RINGGOLD
identifier 2167. **There is no ROR in that employment record.** So ORCID cannot be used to attach a
ROR to the stored `MIT Haystack Observatory` affiliation, and the department name it does carry
(`Atmospheric Science Group`) is not the affiliation the authors themselves declare.

**Escalated, not proposed as a value: the affiliation identifier.** The correct target state is for
the `MIT Haystack Observatory` organization to carry an identifier. It does not, whereas the
separate `Massachusetts Institute of Technology` organization carries `https://ror.org/042nb2s44`.
That is a **shared-organization-row matter**: the row is referenced by other records, so the fix
belongs to whoever administers organization rows and must not be attempted as a per-software
metadata change. It is recorded here so a later refresh recognises it as known and escalated rather
than as an unexamined gap.

**Considered and rejected: recording Cariglia's email as an identifier.** The pre-campaign dossier
carried `cariglia@mit.edu` for her (it is in `CITATION.cff` and `pyproject.toml`). An email is not an
author identifier in this schema — the identifier subfield takes an ORCID for a person or a ROR for
an organization — and she has no discoverable ORCID. Her identifier stays empty.

**Considered and rejected: organization authorship.** Neither author is an organization: both
`CITATION.cff` entries use `given-names`/`family-names` rather than a bare `name:`, so no ROR-keyed
author entry is warranted.

---

### 7. Software Name (MANDATORY)
**MadrigalWeb**

Keep. The capital-M form is what the project presents to readers: it is the PyHC registry's `name`,
the first words of `README.md` ("MadrigalWeb - a python API to access the Madrigal database"), and
`mkdocs.yml`'s `site_name: MadrigalWeb Docs`, which is what the rendered documentation site is
titled.

**Documented alternative, not selected:** the lower-camel `madrigalWeb` is equally attested — it is
the `CITATION.cff` `title`, the `pyproject.toml` `name`, the PyPI distribution name, and the GitHub
repository name. It is a package-identifier spelling rather than a display name, and the recorded
value is a settled editorial choice. A later refresh should not churn between the two.

---

### 8. Description (MANDATORY)

The `CITATION.cff` abstract at the pinned revision, adopted verbatim — four paragraphs:

> madrigalWeb is a pure python module to access data from any Madrigal database. For documentation and examples go to any Madrigal site such as http://cedar.openmadrigal.org
>
> The easiest way to use the Madrigal python remote data access API is to simply let the web interface write the script you need for you. Just choose the Access data pull-down menu and choose Create a command to download multiple exps. Then follow the instructions, and you will have the command you need to download whatever you want from Madrigal. Be sure to select python as the language you want to create the command with. You can choose to download files as they are in Madrigal in either column-delimited ascii, Hdf5, or netCDF4 formats, or you can choose the parameters yourself (including derived parameters), and optionally include filters on the data you get back.
>
> This web interface will generate python commands using one of the following two Python scripts: globalDownload.py and globalIsprint.py. Use globalDownload.py if you want data as it is in Madrigal. Use globalIsprint.py to choose parameters and/or filters. These two scripts are documented below, for those who do not want to use the web interface to generate the needed arguments:
>
> See the online documentation for the script globalCitation.py. This script is used to create a permanent citation to a group of Madrigal files.

**What changed, and against what.** Before this refresh HSSI held the same text one revision out of
date: the first three paragraphs only, with paragraph 3 ending `...to generate the needed arguments.`
where the pinned source ends `...to generate the needed arguments:`. The two were compared paragraph
by paragraph after unfolding the YAML folded scalar (`abstract: >-`, so single line breaks inside a
paragraph become spaces and blank lines become paragraph breaks): paragraphs 1 and 2 are
**byte-identical**, paragraph 3 differed in exactly that one character, and the fourth paragraph was
absent entirely. The colon is there precisely because that fourth paragraph follows it.

**Why this is an evidence-backed correction rather than a rewording.** The superseded text mirrored
an older revision of the same abstract, and its final sentence read as a broken promise: it promised
that the two scripts are documented below, and then stopped. More substantively,
`globalCitation.py` is a real third command-line script shipped by the package — it is listed in `setup.py`'s `scripts=`, it has
its own documentation page (`docs/gc.md`, in `mkdocs.yml`'s `nav`), and it backs three public API
methods (`getCitedFilesFromUrl`, `createCitationGroupFromList`, `getCitationListFromFilters`). A
prospective user reading the superseded description would not learn that permanent citation of
Madrigal file groups is one of the package's three headline capabilities. That was a material
omission, not a matter of taste, which is why the seeded wording was not simply preserved.

**The `http://` in paragraph 1 is deliberate — do not normalise it.** The `CITATION.cff` abstract
writes `http://cedar.openmadrigal.org`, while the site has been https since commit `f93aec7`
(2025-02-21, "cedar site now using https") and the rewritten `README.md` at the pin links
`<https://cedar.openmadrigal.org>`. Adopting the abstract verbatim therefore carries the older
scheme forward, and that is the settled choice: this is the authors' own declared description,
`http://cedar.openmadrigal.org` redirects to https and resolves, and silently editing an
author-supplied abstract is the kind of drift this record exists to prevent. The competing
consideration — correctness of the link — was weighed and judged the lesser one. A later refresh
that "fixes" the scheme to https would be altering an author's text, not correcting an error.

**Considered and rejected: rebuilding the description from `README.md`.** The README was rewritten
during the 3.3.8 documentation work and now matches neither the stored text nor the abstract — it is
shorter, adds installation instructions, and is structured with headings for the rendered docs site
(`docs/index.md` is nothing but `{% include "../README.md" %}`). It is written as a landing page
rather than as a catalogue description, so it is the wrong source for this field even though it is
the most current prose in the repository.

---

### 9. Concise Description (OPTIONAL)
**Python Madrigal Remote API - Access data from any Madrigal database with support for multiple
file formats and parameter filtering.**

Keep. It is accurate against the pinned source on every clause — `pyproject.toml`'s `description` is
exactly `Python Madrigal Remote API`, the multiple formats are the four `downloadFile` accepts, and
parameter filtering is `isprint`'s `parms`/`filters` arguments — and it fits the field's
200-character limit. It is prior editorial wording that says something true and useful, so it is
preserved rather than restyled.

---

### 10. Publication Date (RECOMMENDED)
**2016-06-16**

The earliest distribution of this package that can be dated. PyPI holds 28 releases with files for
`madrigalWeb`, and the earliest upload is version `3.0` at `2016-06-16T20:42:19Z`.

**Caveat a future refresh should keep in mind, and not "fix".** This date predates the GitHub
repository, which was created 2024-09-19; the repository's first content commit (`077df76`, message
`imported`) already carries `version = "3.3.1"`. The software plainly existed and was distributed
for years before it was moved to GitHub — earlier still, since `3.0` implies two prior major
versions — and the pre-2016 history is not publicly recoverable from either source. 2016-06-16 is
therefore the earliest *defensible* publication date, not necessarily the true first publication.
Do not "correct" it forward to the repository creation date; that would be strictly less accurate.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Keep. The field's guidance is that when no DOI has been obtained, the repository host is the correct
entry; no DOI exists (Field 2) and the host is GitHub.

**A tension recorded deliberately, with no change proposed.** The Publication Date above comes from
PyPI in 2016, while the Publisher is the host the source moved to in 2024, so the two fields do not
share a source. Naming PyPI as publisher instead would align them, but it would contradict the
field's own instruction to name the repository host and would disagree with Field 3. The tension is
inherent to a package that was distributed years before it was hosted on GitHub, and it is better
documented than papered over.

---

### 12. Version (RECOMMENDED)

- **Version Number:** 3.3.8
- **Version Date:** 2026-07-24
- **Version Description:** None — the project publishes no release note of any kind (see below)
- **Version PID:** Not found — no DOI exists for the software or for any of its versions (Field 2)

HSSI held 3.3.7 with a version date of 2026-03-12 before this refresh; both are moved forward one
release here. The version description was empty before this refresh and stays empty.

**The version bump is unambiguous.** `pyproject.toml` at the pinned revision reads
`version = "3.3.8"`, the pin's commit message is `madrigalweb 3.3.8 release`, and PyPI's 3.3.8 files
were uploaded at `2026-07-24T16:56:23Z` — roughly forty seconds after the pin commit was pushed
(`pushed_at` `2026-07-24T16:55:46Z`). The superseded 3.3.7 was set at commit `df3b462`
(2026-03-12) and uploaded to PyPI at `2026-03-12T20:38:50Z`, which is where its version date came
from; both values were correct when written and were simply one release stale.

**Version history, established by reading `pyproject.toml` at every commit** rather than by trusting
tags (there are none). 3.3.1 at the `imported` commit (2024-09-19), then 3.3.2, 3.3.3, 3.3.4, 3.3.5,
3.3.6, 3.3.7 at `df3b462` (2026-03-12), and 3.3.8 at the pin. One wrinkle worth recording so it is
not mistaken for an error later: 3.3.4 was set at `0b33bd9`, reverted to 3.3.3 at `887bb12`
("Revert ..."), then set to 3.3.4 again at `b7a47c7`; and `f7984af` bumps to 3.3.5 with the message
`madrigalweb 3.3.5 bc pypi is weird abt version nums`, i.e. a version number consumed by a packaging
problem rather than by a code change.

**What is actually in 3.3.8.** `df3b462` is an ancestor of the pin, so `df3b462..fc444d2` is a valid
release range, and it contains exactly four commits, all dated 2026-07-24: `26b1c37`
("docstrings + docs + globalCLI tests"), `64fd6d2` ("readthedocs dependencies"), `66a4fbf`
("update links to docs") and the release commit itself. **3.3.8 is a documentation, docstring and
test release with no functional change to the API.**

**The version description is left empty, deliberately.** The project publishes no release note *of
any kind*: the repository has 0 tags, the GitHub releases API returns an empty list, there is no
CHANGELOG among the 26 tracked paths, and `madrigalWeb.wiki.git` does not exist as a repository
(`git ls-remote` returns "Repository not found"), so GitHub's `has_wiki: true` flag carries nothing
here. The source says nothing, so the record asserts nothing. That follows the campaign precedent
that a field should assert what a source *says* rather than what a defensible synthesis could claim,
and it keeps the emptiness meaningful: a future agent reading an empty version description learns
that this project does not publish release notes, which is true and useful.

**Considered and not selected: synthesizing a description** from the four in-range commit subjects —
a documentation and testing release adding numpydoc docstrings, a ReadTheDocs build and
command-line tests, with no API change. That synthesis is accurate and would tell a user something
real, which is why it was a genuine option rather than an obvious error. It was declined because it
would be our summary standing in a field a reader will take as the maintainers', and because the
strongest thing this refresh can say about 3.3.8's contents is already recorded just above, in this
dossier, where its provenance is visible.

---

### 13. Programming Language (RECOMMENDED)
**Python 3.x**

**The criterion, settled explicitly so every inclusion and exclusion follows from one rule:** this
field records **the language(s) the software is written in and that a user must have to run it** —
the form's own guidance is to "Select the most important languages" and adds that "This is not
meant to be an exhaustive list." It is *not* an inventory of every file type present in the tree.
Everything below follows from that single criterion.

- **`Python 3.x` — included.** The package is 10 `.py` files, and `pyproject.toml` declares
  `requires-python = ">=3.7"` with the classifier `Programming Language :: Python :: 3`. PyPI's
  record agrees (`requires_python` is `>=3.7`). All three CI workflows run Python 3.12, and
  `[tool.ruff]` sets `target-version = "py312"`.
- **`Python 2.x` — excluded**, and this needs saying because there is a trap. The docstring of
  `madrigalWeb/__init__.py` contains the line `print inst`, which is Python 2 *syntax*. It sits
  inside a triple-quoted module docstring, so it never executes; it is a stale example that survived
  the Python 3 port. The executable declaration `requires-python = ">=3.7"` governs, and it excludes
  Python 2 outright. Do not read that docstring line as evidence of Python 2 support.
- **Every other vocabulary language — excluded**, by the same criterion, with no exception: `C`,
  `C#`, `C++`, `Fortran77`, `Fortran90`, `Fortran 2003`, `Fortran 2008`, `Fortran 2023`, `IDL`,
  `Java`, `Javascript`, `Julia`, `MATLAB`, `Rust`, `SQL`, `Typescript`, `Other`. No source file in
  any of these languages exists at the pin, and there is no compiled extension — `dependencies = []`
  and there is no build step beyond `setuptools`.
- **Non-language file types present but correctly not recorded:** the remaining 16 tracked paths are
  7 `.md`, 4 `.yml`, 1 `.yaml`, 1 `.txt`, 1 `.toml`, 1 `.cff` and 1 extensionless (`LICENSE`).
  Markdown, YAML, TOML and CFF are documentation and configuration formats, none of them is a row in
  this vocabulary, and none of them is something a user needs in order to run the software.

---

### 14. Reference Publication (OPTIONAL)
**Not found — no publication describing this software exists.**

Researched negative; do not reopen without a new artifact.

- **No paper is *about* the package.** An ADS/Sci-X full-text search for `full:madrigalWeb` returns
  4 records, and every one is a third-party study that merely *used* the package (they are listed
  under Field 27). A `full:pysat` control returns 337, confirming the query path works, and a
  deliberately malformed token returns HTTP 401 rather than a silent empty result, confirming the
  zero-versus-broken distinction.
- **No acknowledgement-level mention either.** `ack:madrigalWeb` returns 0.
- **No JOSS paper, no software paper, no `preferred-citation`.** `CITATION.cff` at the pin has no
  `preferred-citation` block; `README.md` cites no paper.

**Considered and rejected: `https://doi.org/10.5281/zenodo.162191`** ("Accessing Madrigal Data via
Python", W. Rideout, 2016). It is the closest thing that exists to a companion artifact and it *is*
recorded in Field 27 — but not in this field. Field 14 drives a distinct "Reference
Publication" citation block on the software's page, which asserts to a reader that this is the
publication describing the software and the thing to cite for it. A conference presentation
demonstrating a database's access methods is not that, and elevating it here would put a claim on
the page that the artifact does not support. The two fields are independent, and the looser bar of
Field 27 is the right home for it.

---

### 15. License (RECOMMENDED)

**MIT License**

That is the vocabulary row name, byte-exact. HSSI held no license for this software before this
refresh; this value fills that gap.

The licence is MIT and is corroborated four ways at the pin: the `LICENSE` file
(`Copyright 2024 Massachusetts Institute of Technology`, followed by the standard MIT text), the
`pyproject.toml` classifier `License :: OSI Approved :: MIT License`, `CITATION.cff`'s
`license: MIT`, and GitHub's own detection (SPDX identifier `MIT`).

**No License URI is recorded, and this is not an omission — it is unrepresentable.**
`Software.license` is a foreign key to a shared `License` row, and the URL is a property of that
shared row, not of this software. The `MIT License` row's URL is `https://spdx.org/licenses/MIT`.
There is consequently no per-software licence URI to store, and any attempt to supply one is either
ignored or would edit a row shared with other records.

**Correcting the pre-campaign dossier, so the error is not reintroduced.** The legacy file recorded
a License URI of `https://spdx.org/licenses/MIT.html`. That was wrong twice over: the value is not
storable per-software at all (above), and even as a reference it does not match the shared row's URL
(`https://spdx.org/licenses/MIT`, with no `.html`). The repository's `LICENSE` file is the correct
thing to cite as evidence for this field; a SPDX URI is not a Field 15 value.

**Licence-file history, traced by content rather than by path, because the path changed twice.**
`0614b6e` added `LICENSE`; `ed8ac51` deleted it the same day; `077df76` added `license.txt`; and
`26b1c37` (2026-07-24, in the 3.3.8 range) renamed `license.txt` back to `LICENSE`, which git
records as a 100%-similarity rename rather than a delete plus an add. The licence
text and the declared SPDX identifier were MIT throughout — only the filename moved. This is
recorded because the pre-campaign dossier cited `license.txt`, which no longer exists at the pin,
and a future agent looking for that filename would find nothing and might wrongly conclude the
licence had been withdrawn.

**Rejected:** `Other` — the MIT row exists and matches exactly, so the catch-all is unnecessary; and
`Restricted`, which is plainly wrong for a permissive licence.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

Eight keywords, in their exact stored spellings:

- **API**
- **data_retrieval**
- **database**
- **geospace**
- **ionosphere_thermosphere_mesosphere**
- **madrigal**
- **python**
- **web service**

HSSI held six keywords before this refresh: the five retained above plus `general`, which is removed
here. `madrigal`, `data_retrieval` and `web service` are added.

*(A rendered HSSI record Title-Cases keywords, so a rendered view shows `Api`, `Database`,
`Geospace`, `Ionosphere_Thermosphere_Mesosphere` and `Python`. That is a display transform. The
stored strings are the ones listed above, and those are the strings any correction must use. Keyword
matching is case-insensitive, so a differently cased spelling binds the existing row rather than
minting a new one; a different *separator* does not — see the `web service` note below.)*

**`general` is removed in this refresh — evidence-driven, not taste.** It is not a description of
this software.
It is a PyHC *scope* tag: the live PyHC `_data/taxonomy.yml` places it in the category **"Span"**,
described as "The user scope of a project", whose only two keywords are `general` and `specific`. It
entered this record from the December 2025 PyHC registry snapshot, when MadrigalWeb sat in
`projects_unevaluated.yml` with `keywords: [ionosphere_thermosphere_mesosphere, general]`. A visitor
filtering HSSI on `general` learns nothing about any software, and this record was contributing
noise to that facet. Of the six keywords HSSI held before this refresh, it was the one carrying no
information.

**`ionosphere_thermosphere_mesosphere` is retained — and here is why, since the case for removal is
real.**
The live PyHC entry dropped it in favour of `geospace`, and the repository tree never names any of
the three layers (scope note). Both are true, and neither is decisive. It is a **"Science Area"**
keyword in the PyHC taxonomy, not a scope tag, so it is categorically different from `general`; the
substitution of `geospace` for it is an editorial preference between two Science Area keywords, not
a finding that the old one was wrong; and it is accurate on the merits — the archive's holdings span
exactly the ionosphere, thermosphere and mesosphere, which is the same evidence used to expand Field
5. Removing it while adding `Earth Ionosphere`, `Earth Thermosphere` and
`Earth Lower and Middle Atmosphere` to Field 5 would be internally inconsistent. From the searcher's
side, someone filtering that keyword would be glad to find the Madrigal client. It is retained.

**`API`, `database`, `geospace` and `python` are retained.** These four are the authors' own keywords
in `CITATION.cff` at the pin (`python`, `database`, `geospace`, `API`) — author-supplied, current,
and accurate.

**`madrigal` — the strongest single addition in this record.** An existing keyword row; also a PyHC
"Mission"-category taxonomy keyword, and carried by pysat's PyHC entry. This software *is* the
Madrigal client, yet before this refresh a visitor filtering HSSI on `madrigal` did not find it —
which is close to the definition of a metadata gap that hurts a user.

**`data_retrieval` — added, with its redundancy acknowledged.** An existing row, and the
first functional keyword in the live PyHC entry. It does overlap Field 4's
`Data Processing and Analysis: Data Access and Retrieval`. It is still worth adding because keyword
browsing and functionality browsing are separate paths through the catalogue and PyHC declares this
term for this package; a user arriving by the keyword facet should not be excluded because the same
fact is expressed elsewhere in a different vocabulary.

**`web service` — added, and the space in it is deliberate.** The live PyHC entry declares
`web_service` (an "Input Sources" taxonomy keyword). **There is no `web_service` row, but there is a
`web service` row with a space.** Underscore-versus-space is not a case difference, so sending
PyHC's `web_service` spelling would mint a new near-duplicate row permanently — exactly the
typo-accretion this open vocabulary is prone to. The existing space-form row is therefore the value
recorded here, and **a later refresh must not "correct" the spelling to PyHC's underscore form**:
that would create the very duplicate this choice avoids. The term earns its place because its
meaning is not carried elsewhere in this record — Field 17 names the archive, not the access
protocol, and Field 4 names the retrieval capability rather than the transport — and "this package
is a web-service client" is a genuinely distinguishing fact.

**Considered and rejected, with reasons, so they are not re-proposed:**

- **`ascii`, `hdf5`, `netcdf`** (all existing rows; all in the live PyHC entry) — rejected as pure
  duplication. Field 19 already records `ascii`, `HDF5` and `netCDF3/4` in a structured, controlled
  vocabulary with its own facet. Restating them as free-text keywords adds a second, weaker copy of
  the same fact and dilutes the keyword facet.
- **`data_access`** (the live PyHC entry's "Intent" keyword) — rejected twice over. There is no
  `data_access` row (there is a `data access` row with a space, so the underscore form would mint),
  and its meaning is already carried by `data_retrieval` and by Field 4.
- **`incoherent scatter radar`** — an existing row, and tempting given that 31 of Madrigal's 302
  registered instruments are incoherent scatter radars. Rejected: the package is instrument-agnostic
  and singling out one instrument class as a keyword would misrepresent it, for the same reason
  Fields 31/32 are left empty.
- **`radar`, `remote sensing`, `space physics`** — rejected as either too broad to discriminate or
  not attested by any source for this package.

---

### 17. Data Sources (OPTIONAL)
- **Madrigal**
- **Observatory/Mission-specific**

Both kept. `Madrigal` is exact and needs no argument: the package speaks only to Madrigal servers.

**`Observatory/Mission-specific` — kept, with the tension recorded because it is not obvious.** The
reading against it: Madrigal is a *multi*-observatory distributed archive and this client is
observatory-agnostic, which looks like the opposite of "observatory-specific"; and the field's own
guidance says that when this value is selected the observatory should be named in Field 32, which is
evidenced-empty here. The reading for it, which prevails: Madrigal is not one central service but a
federation of servers each run by an individual observatory, and the client's required
`--url=<Madrigal url>` argument points at *one specific observatory's* site. The package's own
example script demonstrates exactly this, printing
`"Now repeat the same calls as above to get PFISR data from the SRI site"` — the user selects an
observatory's server as the data source. That is a fair reading of the row, and it is a recorded
value that would need a stronger case than "arguably imprecise" to remove. Set down here so a later
refresh sees a considered judgement rather than an oversight, and can overturn it deliberately.

**Considered and rejected:**

- **`HTTP/HTTPS Directories`** — rejected. HTTP is the transport (every remote call is a
  `urllib.request.urlopen`), but the endpoints are named Madrigal CGI services
  (`isprintService.py`, `madCalculatorService.py`, `traceMagneticFieldService.py`, `getMadfile.cgi`
  and others), not browsable directories. This row describes a data-access *pattern*, and the
  pattern here is a web API, not directory traversal.
- **`HAPI` — rejected, and this one is a genuine trap.** `CODE_OF_CONDUCT.md` states that the code
  of conduct is adapted from the HAPI-Server project and links its repository. That is a citation
  for the conduct document's *text*; the package contains no HAPI client, no HAPI endpoint and no
  HAPI parsing. Separately, one of the Zenodo presentations discussed under Field 27
  (`https://doi.org/10.5281/zenodo.17382072`, 2025) describes bringing HAPI and SPASE integration to
  *Madrigal the database*. If that work lands server-side it still would not make this client a HAPI
  client — but it is the kind of development that would justify revisiting this row, so it is
  flagged rather than merely dismissed.
- **`CDAWeb`, `AMDA`, `SSCWeb`, `OMNIWeb`, `VirES`, `das2`, `TAP`, `GFZ`, `WDC`,
  `The Virtual Solar Observatory.`, `S3/Cloud-aware`, `FTP/FTPS Directories`, `Other`** — rejected;
  none appears anywhere in the package, which talks to Madrigal and nothing else.

---

### 18. Input File Formats (RECOMMENDED)
**None — the software reads no local files, so this field is correctly empty.**

This is a mechanically established negative rather than an unfilled gap, and it is worth stating
precisely because "a data package must read *some* format" is a natural but wrong assumption here.

Every local `open(` call in the six non-test package modules at the pin (`madrigalWeb.py`,
`globalCitation.py`, `globalDownload.py`, `globalIsprint.py`, `exampleMadrigalWebServices.py`,
`__init__.py`) was enumerated and classified. **Re-derive the set with the anchored pattern
`grep -P '(?<![a-zA-Z.])open\('`, which returns 8 lines across those six modules** — six live calls
and two commented out. The lookbehind is what makes the number reproducible: an unanchored `open(`
returns 31 lines instead, because it also matches `urllib.request.urlopen(`, which accounts for 23
of them. A future agent who runs the unanchored form and sees 31 has not found a contradiction.

All six live calls are write-mode: `open(outputFile, "w")` and `open(outputFile, "wb")` in
`isprint`; `open(destination, readtype)` in `downloadFile`, where `readtype` is assigned only `"w"`
or `"wb"`; `open(destination + ".gz", "wb")` in that method's gzip fallback;
`open(destination, "wb")` in `downloadWebFile`; and `open(output, "w")` in `globalIsprint.py`. The
two remaining lines are dead commented-out remnants, `# f = open(destination, 'w')` and
`# f = open(destination, 'wb')`. Everything else in these modules that reads is a
`urllib.request.urlopen` network fetch. **There is no local-file read in any of them.**

The architecture explains why: the client sends a request and writes the response to disk. Data
enters over HTTP, never from a file the user supplies. The formats it *writes* are Field 19's
concern.

**Considered and rejected:** every row in the shared `FileFormat` vocabulary — `ascii`, `CDF`,
`csv`, `FITS`, `HDF5`, `IDL.sav`, `ISTP-Compliant`, `JSON`, `netCDF3/4`, `Zarr`, `Other`. Recording
`HDF5` or `netCDF3/4` here by symmetry with Field 19 would be the easy mistake: the package can
write those formats but cannot read them back, and a user filtering for software that *ingests* HDF5
would be misled.

---

### 19. Output File Formats (RECOMMENDED)
- **ascii**
- **HDF5**
- **netCDF3/4**

All three confirmed, and the set is complete. `downloadFile` guards with
`if format not in ("hdf5", "ascii", "simple", "netCDF4")` and raises `ValueError` otherwise;
`simple` is described in its own docstring as "a simple ascii space delimited column format", so it
maps onto `ascii` rather than adding a fourth row. `isprint` selects the same three by output
extension (`.h5`/`.hdf`/`.hdf5`, `.nc`, otherwise column-delimited ascii). The `globalDownload.py`
command line restricts the format argument to `choices=["ascii", "hdf5", "netCDF4"]`.

**Considered and rejected: `csv`.** The tree does contain the string `csv` — in
`madrigalWeb/tests/testGlobalScriptsCLI.py`, in a test named `test_invalid_format_rejected` which
passes `--format=csv` and asserts a **non-zero exit code**. csv is the package's canonical *invalid*
format. A keyword search that found `csv` in the tree and recorded it here would invert the
evidence.

**Also rejected:** `CDF`, `FITS`, `IDL.sav`, `ISTP-Compliant`, `JSON`, `Zarr`, `Other` — none is
produced. Note in particular that the legacy Madrigal formats named in `downloadFile`'s docstring
(`'madrigal'`, `'blockedBinary'`, `'ncar'`, `'unblockedBinary'`) are documented there as no longer
supported for Madrigal 3 *and* are rejected by the code's own guard, so they are not outputs and
have no vocabulary row in any case.

---

### 20. Operating System (RECOMMENDED)

- **Linux**
- **Operating System Independent**
- **Windows**

HSSI held `Linux` and `Operating System Independent` before this refresh; `Windows` is added here.
`Mac` was weighed and not selected — see below.

**The criterion applied, so the three answers below are consistent rather than ad hoc:** a specific
OS row is recorded when there is either an explicit portability claim by the project or CI evidence
that the software is exercised there.

- **`Linux`.** CI evidence: all three GitHub Actions workflows (`unit-test.yml`,
  `do-lint.yml`, `python-publish.yml`) run on `ubuntu-latest`, and the ReadTheDocs build uses
  `os: ubuntu-24.04`.
- **`Operating System Independent`.** `pyproject.toml` carries the classifier
  `Operating System :: OS Independent`, and the package is pure Python with `dependencies = []` and
  no compiled extension, so the claim is credible rather than aspirational.
- **`Windows` — added in this refresh.** The project states it explicitly, in three separate files.
  The sentence
  `It runs on either unix or windows.  It requires only the MadrigalWeb python module to be installed.`
  appears at `globalCitation.py:6`, `globalDownload.py:5` and `globalIsprint.py:6` at the pin — in
  each of the three installed command-line scripts' module docstrings, which are also the text
  rendered on the documentation site's `globalDownload.py`, `globalIsprint.py` and
  `globalCitation.py` pages. (The pre-campaign dossier cited only one of the three, understating how
  deliberate the claim is.) **Why this matters from the searcher's side:** the Region vocabulary's
  flatness has an analogue here — a user filtering the catalogue on `Windows` is not served
  `Operating System Independent` records, so before this refresh a Windows user did not find a
  package whose own documentation tells them three times that it runs on Windows. That was a real,
  user-visible gap, and it is why the row is recorded despite `Operating System Independent` already
  being present.

**Considered and not selected: `Mac`.** Tempting by the same sentence — macOS is a unix — and the
claim is almost certainly true in practice: the package is pure Python with no compiled extension,
so there is no plausible mechanism by which it would fail on macOS. It was declined because that is
inference rather than a claim by the project. The project writes "unix"; it never writes macOS, Mac
or Darwin, and no CI job runs on macOS, so recording the row would assert support the project has
neither claimed nor tested. **This is a line drawn at what is evidenced, not a finding that macOS is
unsupported** — `Linux` has CI, `Windows` has an explicit claim, `Mac` has neither. A later refresh
should add it on new evidence (a macOS CI job, or the project naming macOS in its own text), not on
the same unix inference weighed here.

**Also rejected:** `Solaris`, `MobilePlatform`, `Other` — no evidence of any kind.

---

### 21. CPU Architecture (RECOMMENDED)
**CPU Independent**

Keep. The package is pure Python: `pyproject.toml` declares `dependencies = []`, there is no
compiled extension, no build step beyond `setuptools`, and no architecture-specific code path. There
is nothing that could bind it to an instruction set.

**Correcting the pre-campaign dossier:** it justified this value by saying the package "only
requires 'packaging'". That was true of an earlier revision and is stale at the pin — commit
`df3b462` (2026-03-12) removed the `packaging` dependency, as its own message says
("remove checks for mad2 sites, remove packaging dependency"), leaving the dependency list empty.
The conclusion was right; the reason was out of date, and the current reason is stronger.

**Considered and rejected:** `x86-64`, `Apple Silicon arm64`, `Linux aarch64 or arm64`, `ppc64le`,
`Sun (SPARC)`, `GPU`, `HPC or HEC`, `Other`. Recording any specific architecture would narrow a
record that is genuinely architecture-neutral; `GPU` and `HPC or HEC` in particular would be
positively misleading for a single-threaded HTTP client.

---

### 22. Related Phenomena (OPTIONAL)
**None — correctly empty, because the vocabulary contains no phenomenon this software relates to.**

The reason to record this in full is that a future agent will otherwise re-derive it: an
upper-atmospheric data client *feels* like it should have a phenomenon, and the answer is that the
vocabulary does not offer one. The complete `Phenomena` list is seven rows: `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`,
`X-ray emission`. Six of the seven are solar or heliospheric and are simply inapplicable to an Earth
upper-atmosphere archive — a repository sweep confirms the software never mentions any of them
(`flare`, `coronal mass`, `solar wind` and `x-ray` each match no file under a case-insensitive
`git grep -ilP`).

**`Geomagnetic Storms` — the one candidate, considered and rejected.** Madrigal carries 4
`Geophysical Indices` instruments, and the package's own docstrings request `kp` and `dst`
(`madTimeCalculator`'s example returns Kp and Dst at daily steps; `madCalculator2`'s uses
`'sdwht,kp'`). But those indices appear as *filter and derivation parameters*, not as a subject the
software addresses. The only occurrences of "storm" in the tree are two instances of the example
experiment name `'Wide Latitude Substorm Study'` in `MadrigalExperiment` docstrings — an
illustrative string, not a claim. From the searcher's side, a user browsing storm-related software
wants storm analysis tools and would find a generic archive client out of place.

**The durable conclusion:** this field's emptiness is a property of the vocabulary's current
coverage, not of the software. No ionospheric, thermospheric, mesospheric or auroral phenomenon
exists as a row. If such rows are ever added, this field should be revisited — that, and not new
evidence about the software, is what would change the answer.

---

### 23. Development Status (RECOMMENDED)

**Active**

HSSI held no development status for this software before this refresh; this value fills that gap.

The `RepoStatus` vocabulary carries definitions, and `Active` reads, byte-exact:

> The project has reached a stable, usable state and is being actively developed.

Both halves are satisfied at the pin. *Stable and usable*: 28 releases on PyPI between 2016-06-16 and
2026-07-24, the current one 3.3.8. *Actively developed*: the most recent release is 2026-07-24 — the pinned revision
itself — the repository is not archived and not disabled, and it has 0 open issues.

**Rejected, with the discriminating fact for each,** since several neighbouring rows are plausible at
a glance:

- `Inactive` ("The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows.") — contradicted by a release in
  the pin's own month.
- `Unsupported` ("The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired.") — contradicted by the same, and by `README.md`
  actively soliciting contributions — its Contributing section opens
  "We encourage all contributions." and invites issues, emails and pull requests.
- `WIP`, `Suspended` and `Abandoned` — all three carry the clause "there has not yet been a stable,
  usable release", so all three presuppose something 28 PyPI releases refute.
- `Concept` — a different premise, and refuted separately: it describes a repository where "Minimal
  or no implementation has been done yet, or the repository is only intended to be a limited
  example, demo, or proof-of-concept." This package has a decade of releases and a published API
  reference, so neither branch of that definition applies.
- `Moved` — the repository is the authoritative location; nothing points elsewhere.

**Improving on the pre-campaign dossier's reasoning.** The legacy file also said `Active`, but
inferred it from "recent development activity and lack of deprecation notices" and noted that no
repostatus.org badge exists. The absence of a badge is true and irrelevant — the value is chosen
from a controlled vocabulary whose definitions are the standard to test against, not from a badge —
and the value is now grounded in the definition text plus dated release and repository state.

---

### 24. Documentation (RECOMMENDED)

**https://madrigalweb.readthedocs.io/en/latest/**

HSSI held `https://cedar.openmadrigal.org/` before this refresh; it is replaced here. Both URLs
resolve (each returns HTTP 200 with `text/html`; the CEDAR URL is the same page with or without the
trailing slash). The question is which one documents *this package*.

**The case for the ReadTheDocs site is that it is this package's own documentation, generated from
this repository.** It is declared as such by each source that distinguishes the two:
`pyproject.toml`'s `Documentation` project URL, the PyPI record's `project_urls.Documentation`, the
live PyHC registry entry's `docs` field, and `README.md` itself, which links it with the words
"See documentation [here]". It is built from the pinned tree — `.readthedocs.yaml` plus `mkdocs.yml`
plus the `docs/` directory — and its `docs/index.md` is literally `{% include "../README.md" %}`.
Its rendered title is `MadrigalWeb Docs`, and its navigation is `Home`,
`MadrigalWeb API Reference` (generated from the numpydoc docstrings via `mkdocstrings`),
`globalDownload.py`, `globalIsprint.py` and `globalCitation.py`. Decisively for this field, whose
definition is "Link to the documentation and installation instructions", the page carries an
"Installing MadrigalWeb" section with the `pip install madrigalweb` command. The CEDAR page has no
installation instructions for the package.

**The case for the CEDAR site, and why it loses.** `https://cedar.openmadrigal.org` is `setup.py`'s
`url` and (as `http://cedar.openmadrigal.org`) `CITATION.cff`'s `url`, and both the description and
the README point users there for data examples. But those are *project homepage* declarations, not
documentation declarations — note that the same `pyproject.toml` that omits CEDAR entirely names
ReadTheDocs under `Documentation`. Its rendered title is `Madrigal database at CEDAR` and its
content is the database portal: "Madrigal is an upper atmospheric science database used by groups
throughout the world", with navigation for accessing data, browsing metadata, running models, and
reaching other Madrigal sites. It documents Madrigal-the-database and its web interface, not the
Python client.

**From the searcher's side**, which settles it: a visitor clicks "Documentation" on the MadrigalWeb
record expecting to learn how to install and call *this package*. The ReadTheDocs site answers that
in one click; the CEDAR portal sends them into a database web interface where the package's API
reference does not appear at all.

**Why the superseded value existed, and why that was not a reason to keep it.** The ReadTheDocs
site is new: it was set up in the 3.3.8 documentation work of 2026-07-24 (`64fd6d2` "readthedocs
dependencies", `66a4fbf` "update links to docs"). When the record was created no package-specific
documentation site existed yet, and CEDAR was where the project pointed users, so the value was
correct at the time. It was a stale value superseded by evidence, not a stylistic disagreement.

**Keeping both was not available.** The field takes a single URL. CEDAR is not lost from the record
by this change: Field 8's description names `http://cedar.openmadrigal.org` in its first paragraph
and directs users there for documentation and examples, and the README that the ReadTheDocs site
itself renders links `<https://cedar.openmadrigal.org>`. The two fields therefore now divide the
work deliberately — Field 24 points at the package's own documentation, while Field 8 keeps the
authors' own pointer to the database behind it.

---

### 25. Funder (OPTIONAL)
**Not found — no funder information exists in any available source.**

A sweep of all 26 tracked paths at the pin for
`fund|funded|funding|grant|award|NSF|NASA|acknowledg|sponsor|cooperative agreement|\bAGS\b`
(case-insensitive, `git grep -inP`) returns only two kinds of match, and **neither is a funding
acknowledgement**:

- the MIT licence's boilerplate, which contains "Permission is hereby granted, free of charge" — the
  word "granted" in its legal sense;
- the CEDAR Rules-of-the-Road paragraph, which appears in both `README.md` and `CODE_OF_CONDUCT.md`
  and contains the phrase "must be acknowledged in all reports and publications". This is a
  **data-use term** imposed on users of Madrigal data — it tells a *user* to credit the data
  providers. It is not a statement about who funded this software, and reading it as one would be a
  clear error.

There is no `.zenodo.json`, no `codemeta.json`, and `CITATION.cff` has no funding block. There is
also no reference publication whose Acknowledgments could supply the answer (Field 14), which closes
the usual fallback route.

**Note for a later refresh:** Madrigal's incoherent scatter radar facility is NSF-funded — the
vocabulary definition of one SPASE row discussed under Fields 31/32 says so of Millstone Hill — but
that funds *the observatory and the archive*, not this Python client. Do not transfer it here.

---

### 26. Award Title (OPTIONAL)
**Not found.**

Same evidence and same sweep as Field 25: no award title and no award number appears anywhere in the
repository, in the package metadata, or in any external record found for this software. With no
funder identified and no reference publication to mine for an Acknowledgments section, there is no
route to an award. This is a genuine absence, not an unexamined field.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- **https://doi.org/10.5281/zenodo.162191**
- **https://doi.org/10.5281/zenodo.17382072**

HSSI held no related publications before this refresh. Both Zenodo presentations are added here —
the two artifacts the software's own authors wrote about accessing Madrigal. Four third-party papers
that used the package were considered and not added; they are listed further down, because knowing
they exist and were weighed is what stops a later refresh from "discovering" them.

**`https://doi.org/10.5281/zenodo.162191` — the closest thing to a companion publication.** Zenodo
record: title "Accessing Madrigal Data via Python", resource type Presentation, publication date
2016-06-20,
description "The Madrigal geoscience database is described and access methods demonstrated.", sole
creator recorded by Zenodo as `Rideout, WIlliam` with affiliation `MIT Haystack Observatory`. *(The
capital I in "WIlliam" is Zenodo's own typo in that record; it is reproduced exactly here so a
future agent does not "correct" the quotation and lose the ability to match it. The person is this
software's author.)* The case for including it: it is by the software's own author, its subject is
precisely the capability this package provides, and it was deposited four days after the earliest
PyPI release of the package (2016-06-16). It is the closest thing to a companion publication that
exists, and a user landing on this record with no citable paper is better served by it than by
nothing. It carries no related identifiers, so nothing links it to the code automatically — this
association is a human judgement, recorded as such.

**`https://doi.org/10.5281/zenodo.17382072` — recorded, with a scope note on what it delivers.**
"Disciplinary Improvements: Accelerating Geoscience Discovery with Madrigal: HAPI+SPASE Integration
for Transformative Open Science", creator `Cariglia, Katherine`, presentation, 2025-10-17. Katherine
Cariglia is one of this software's two authors. **Read it as being about the archive's direction
rather than about this client:** its subject is the Madrigal *infrastructure* — adding HAPI and
SPASE interfaces to the database — so a reader following it from this record learns where Madrigal
is heading, not how madrigalWeb works. That is a caveat on what the link delivers, not an objection
to its presence. Together the two presentations give a reader both the 2016 account of reaching
Madrigal from Python and the current statement of where the archive is going, and both were written
by this software's authors — which is precisely what separates them from the four papers below.

**Considered and not added — the four third-party papers that used the package.** An ADS/Sci-X
full-text search (`full:madrigalWeb`, 4 results, with a `full:pysat` control returning 337 and a
malformed token returning HTTP 401) finds:

- `https://doi.org/10.1029/2018JA025877` — "Snakes on a Spaceship—An Overview of Python in
  Heliophysics" (2018)
- `https://doi.org/10.1029/2023JA031455` — "Dynamics of Mid-Latitude Sporadic-E and Its Impact on HF
  Propagation in the North American Sector" (2023)
- `https://doi.org/10.1029/2024JA032415` — "A New Method for Analyzing F-Region Neutral Wind
  Response to Ion Convection in the Nightside Auroral Oval" (2024)
- `https://doi.org/10.3389/fspas.2025.1601296` — "Characterization of F-region neutral wind response
  times and its controlling factors during substorms" (2025)

They stay on this page as evidence — they demonstrate real scientific use, and two of them are the
F-region neutral-wind studies cited in Field 5's `Earth Thermosphere` reasoning, one of those two
being also the nightside-auroral-oval study weighed there under `Earth Auroral Subregion` — but they
are not added to the field. The field is for publications "the software developer prioritizes", and
this set is unbounded and growing: any paper that happens to mention the package would qualify by
the same logic, and the developers have signalled no preference among them. The two entries that are
recorded are there because the software's own authors wrote them; these four are not, and adding
them would turn a curated list into an arbitrary snapshot. **They were weighed, not overlooked** — a
later refresh that finds them again has not found new evidence.

---

### 28. Related Datasets (OPTIONAL)
**Not found — correctly empty.**

The package is a general client for an archive of hundreds of instruments' data (Field 5); it is not
associated with any particular dataset, and enumerating Madrigal's holdings here would be both
impractical and wrong.

**One near-miss worth recording, because it looks like a lead and is not.** The package *does*
handle dataset identifiers: `MadrigalExperimentFile` carries a `doi` attribute populated from the
server's response, and `getCitedFilesFromUrl`, `createCitationGroupFromList` and
`getCitationListFromFilters` create and resolve permanent citations of the form
`https://w3id.org/cedar?experiment_list=experiments/2014/mlh/16mar13&file_list=mlh130316g.007.hdf5`.
Those identifiers belong to whichever files a *user* happens to request at run time, and the group
citations are minted on demand by the user's own call. They are not datasets this software is
related to, and none of them is a fixed property of the package.

---

### 29. Related Software (OPTIONAL)

**https://github.com/pysat/pysat**

This single entry is unchanged by this refresh: HSSI held it before, and it is retained. What
changes is the rationale recorded for it, the seeded version of which was too weak to carry the
value. GeospaceLAB, the other half of this question, belongs in Field 30 rather than here.

**The relevance bar applied here** — a Field 29 entry must be *distinguishing*: a similar-purpose
tool, a predecessor or fork parent, a companion, or a domain-specific dependency. It must tell a
reader something about **this** software. This bar is applied to the incumbent as rigorously as to
any candidate; an entry kept without an argument is the same defect as one rejected without one.

**`https://github.com/pysat/pysat` — retained.** The honest picture, established from pysat's own
repository rather than from either project's marketing:

- pysat **once used this package directly**. Its CHANGELOG carries the entry
  "Changed madrigal methods to use `madrigalWeb` as a module rather than calling it externally"
  (wrapped across two lines in the source), and a subsequent deprecation entry records that several
  `coords` functions "will move to pysatMadrigal".
- **They did.** At pysat's current revision there is no `import madrigalWeb` anywhere, and
  `madrigalWeb` appears in none of its dependency declarations. Its documentation directs Madrigal
  users to the separate `pysatMadrigal` package.
- `pysatMadrigal` is **not an HSSI Software entry** — it exists in the catalogue only as a
  related-item target of pysat's own record — so it cannot be recorded in this field. (Related-item
  display names in the catalogue are placeholders and the page renders the raw URL as link text, so
  the display name must never influence which URL is chosen.)

So the relation is real but indirect today: pysat is the other major Python route into Madrigal
data, by way of a plug-in it spun out of code that once called this package. **From the searcher's
side**, a user on the madrigalWeb page who sees pysat learns something genuinely useful — that there
is a second, framework-based way to work with Madrigal data, and which project to look at for it. A
user on the pysat page is directed to `pysatMadrigal` and does not need this record. Keeping the
entry serves the reader who is here.

**Correcting the pre-campaign dossier's reason, which was too weak to carry the value.** The legacy
file justified pysat with "has madrigal keyword in PyHC registry". That is true — pysat's PyHC core
entry does list `madrigal` among its keywords — but a shared registry keyword is not a relation
between two pieces of software, and on that reasoning many packages would qualify. The value
survives; its justification is replaced.

**Considered and rejected for this field:**

- **`https://github.com/jswoboda/GeoDataPython`** — rejected here (and see Field 30). It is not a
  similar-purpose tool: it is a container/fusion and plotting library, not a data-access client, so
  it does not distinguish this software by comparison.
- **`https://github.com/rmcgranaghan/Helio-KNOW`** — rejected. It is Madrigal-adjacent only in that
  its own record names `Madrigal` as a data source. It shares neither purpose nor code with this
  package, and pairing them would tell a reader nothing.
- **`https://github.com/indiajacksonphd/Helio-Lite`** — rejected. It is a catalogue neighbour that
  surfaces in Madrigal-adjacent browsing, but its record does not mention Madrigal anywhere and it
  has no relationship to this package. Recorded so the question is not reopened.
- **`https://github.com/JouleCai/geospacelab`** — not rejected, *relocated*: it clears the higher
  Field 30 bar, so it belongs there, not here.
- **The generic stack** — the question does not arise, and that fact is itself worth recording:
  `pyproject.toml` declares `dependencies = []`, so this package has no dependency on numpy, scipy,
  pandas, matplotlib, requests or anything else. There is no dependency list to be mistakenly mined
  for related software.

**Length constraint for any new entry in Fields 29/30:** a newly minted related-item row copies the
URL into a 128-character name column, so any added URL must be at most 128 characters. Every URL
recorded in these two fields is well under that.

---

### 30. Interoperable Software (OPTIONAL)

**https://github.com/JouleCai/geospacelab**

HSSI held no interoperable software for this record before this refresh; this single entry is added
here.

**The bar** — a *demonstrated exchange*: a shared or converted data model, one package's output
imported into the other, an adapter API, a plugin relationship, or a companion package. Not a
dependency list, and never a blanket ecosystem claim.

**The evidence is direct and in GeospaceLAB's own source, not inferred.**

- `geospacelab/datahub/sources/madrigal/downloader.py` carries
  `import madrigalWeb.madrigalWeb as madrigalweb` at line 16 of its top-level import block, and
  `utilities.py` in the same source package carries the same import at its line 14. GeospaceLAB's
  entire Madrigal data-access path is built on this package's `MadrigalData` class.
- GeospaceLAB declares the dependency explicitly, pinning a floor version: `'madrigalweb>=3.3'` in
  its `setup.py`. It also names `madrigalweb` in its README's dependency list.
- GeospaceLAB's own HSSI record **already names this repository** under its related software. Before
  this refresh the relation was recorded in that one direction only; this entry makes it visible
  from both sides, which is what a user browsing either record would expect.
- The exchange is substantive rather than incidental: GeospaceLAB's README documents seven Madrigal
  data products it serves through that path (EISCAT, GNSS/TEC maps, three DMSP products, Millstone
  Hill incoherent scatter radar and Poker Flat incoherent scatter radar), each reached via this
  client.

**From the searcher's side**, a user on the madrigalWeb page seeing GeospaceLAB learns that there is
a higher-level analysis and visualization framework that consumes this package — genuinely useful,
and not something they could guess. A user on the GeospaceLAB page already sees the reciprocal link.

**Considered and rejected — `https://github.com/jswoboda/GeoDataPython`.** This is the closest call
in either relation field, so the reasoning is recorded in full. *For:* GeoDataPython reads Madrigal
HDF5 files (`GeoData/utilityfuncs.py` documents a "madrigal h5 read in function" for Madrigal
Sondrestrom data), its example notebooks work with RISR data retrieved through Madrigal, and its
HSSI record lists `Madrigal` as a data source — so files this package downloads can in principle be
opened by it, and Madrigal HDF5 is an archive-specific layout rather than generic HDF5. *Against,
and decisive:* neither project names the other anywhere. GeoDataPython does not import or depend on
madrigalWeb, and madrigalWeb knows nothing of it. The connection runs through Madrigal's file
format, not through either package's API, and it would be equally true of any tool that opens a
Madrigal HDF5 file. That is an inference about a shared archive, not a demonstrated exchange between
two packages, and the bar exists precisely to exclude it. Recorded rather than dropped because it is
a genuine judgement call that a later refresh will encounter again — reopening it should require new
evidence (for example, either project documenting the pairing), not a re-argument of the same facts.

**Considered and rejected — `https://github.com/pysat/pysat`.** It fails *this* field's bar even
though it is kept in Field 29: the code-level exchange lives in `pysatMadrigal`, not in pysat, and
pysat neither imports nor depends on this package today. Placing it here would assert an
interoperation that no longer exists.

**Considered and rejected — the generic and ecosystem-level claims.** There is no dependency stack
to consider (`dependencies = []`), so there is nothing to relocate from a dependency list. The two
justifications the field's own guidance calls out as never sufficient — "part of the standard
scientific Python ecosystem" and "a PyHC member, so it interoperates with PyHC packages" — are not
evidence of any particular exchange and are not used here. Note that PyHC membership *is* a fact
about this software — its live registry entry is discussed under Fields 16 and 24 — it is simply not
an interoperability claim.

---

### 31. Related Instruments (OPTIONAL)
### 32. Related Observatories (OPTIONAL)

**Both fields are empty — an evidenced, deliberate omission, unchanged by this refresh.** HSSI held
no instrument and no observatory for this software before it, and none is added. This is the
governing judgement in this record, so the full case and every candidate row weighed against it are
set out here for both fields together — including the two that were specifically offered and
declined: the Millstone Hill incoherent scatter radar row and the AMISR row.

**The relevance gate is "designed to support".** A software entry belongs against an instrument or
observatory when it reads, parses, calibrates, processes or models *that specific facility's* data,
or is purpose-built for it. **This package is designed to support none, and that is a positive
design property rather than a gap in our research.** Every facility name in the tree is illustrative,
verified line by line at the pin:

- `Millstone` — 11 lines in 3 files: docstring example values
  (`Example: 'Millstone Hill Incoherent Scatter Radar'.`, `Example: 'Millstone Hill Observatory'.`)
  showing what an instrument or site *name string* looks like, plus test fixtures.
- `Jicamarca` (6 lines in 5 files) and `Arecibo` (4 lines in 4 files) — essentially one CLI usage
  example, `--inst="Jicamarca IS Radar,Arecibo*"`, repeated across `docs/gc.md`,
  `globalCitation.py`, `globalDownload.py` and `globalIsprint.py`, demonstrating that `--inst`
  accepts names with glob characters.
- `PFISR` — 3 lines in `exampleMadrigalWebServices.py`, a walk-through of searching multiple
  Madrigal sites.
- `EISCAT`, `AMISR`, `RISR`, `Sondrestrom`, `DMSP`, `GNSS`, `Fabry-Perot`, `ionosonde` and
  `Poker Flat` — **no file matches any of them.** `TEC` matches 4 files unanchored, but
  word-anchored (`git grep -nP '\bTEC\b'`, case-sensitive) it matches nothing: the unanchored hits
  are "protections", "Technology" and `createCitationGroupFromList`. Scope matters here, and an
  unanchored sweep would produce a false positive.

The package hard-codes no instrument code, no site URL and no facility list. Instruments are
discovered at run time by asking whichever server the user pointed at (`getAllInstruments`), and the
required `--url` argument means the user, not the package, chooses the facility.

**Judged from the searcher's side, which is what settles it.** Picture a visitor on an observatory's
page clicking "show software related to this observatory."

- If madrigalWeb appeared under **Millstone Hill** — the facility with the closest vocabulary match
  — a user would reasonably infer this is Millstone-specific software. It is not: Millstone
  Hill is one of hundreds of instruments reachable through it, and it is named in the source only as
  a docstring example. Worse, the record would then be *absent* from every other facility, implying
  a specialization that does not exist. The single association would actively mislead.
- Conversely, listing many facilities would be a fabrication — the software declares no scope, and
  any list we composed would be ours.
- **Empty is the honest and most useful answer.** Users find this software through Field 17
  (`Madrigal`), through Field 5's regions and through Field 16's `madrigal` keyword — routes that
  correctly describe an archive-wide client — rather than through a facility association it never
  claims.

**The Millstone Hill option, presented fairly with its concrete defects, so it is not reopened
blind.** The vocabulary was swept word-anchored and case-insensitively across all four of `name`,
`abbreviation`, `identifier` and `definition` (controls: `Observatory` matches thousands of rows,
`zzzznonsense` matches none). **`Madrigal`, `CEDAR` and `Arecibo` match nothing at all** under any
scope tried. Five rows match `Millstone`, and each was weighed and set aside for a specific reason:

- `https://spase-metadata.org/SMWG/Instrument/MEASURE/Millstone.Hill/ISR` (type: instrument) — the
  closest genuine match; its definition is unmistakably about the Millstone Hill incoherent scatter
  radar, opening "The incoherent scatter radar (ISR) geospace facility at Millstone Hill is funded
  by the National Science Foundation for studies of the Earth's upper atmosphere and ionosphere."
  **But its stored `name` is the bare string `Incoherent Scatter Radar`.** Selecting it would print
  a generic, uninformative label on the software's page with no indication of which radar is meant.
  **This row was specifically offered and declined, not overlooked** — the label is the immediate
  defect, and behind it stands the broader objection set out below, that the package is not
  Millstone-specific in the first place.
- `https://spase-metadata.org/SMWG/Observatory/MEASURE/Millstone.Hill` (type: observatory) — stored
  name `The Millstone Hill Geomagnetic Observatory.`, defined as "The Millstone Hill (MSH)
  Geomagnetic Observatory. Boston University, Millstone Hill, MA." This is a **magnetometer**
  observatory operated by Boston University. It is a different entity from MIT Haystack's radar
  facility that merely shares a place name — the wrong entity, not merely an awkward label.
- `https://spase-metadata.org/SMWG/Instrument/MEASURE/Millstone.Hill/Magnetometer` (type:
  instrument) — the fluxgate magnetometer at that geomagnetic observatory. Same wrong entity.
- `https://spase-metadata.org/ISWI/Observatory/GIRO/MHJ45_MillstoneHill` (type: observatory) — the
  GIRO **digisonde** station at Millstone Hill, URSI code MHJ45. A third distinct entity.
- `https://spase-metadata.org/SMWG/Observatory/MEASURE` (type: observatory) — the MEASURE
  magnetometer-array observatory group, of which Millstone Hill is one station. Wrong scope
  entirely.

**There is no vocabulary row for MIT Haystack Observatory.** A `Haystack` sweep across the same four
columns returns exactly one row, `https://spase-metadata.org/IUGONET/Observatory/ISEE/OMTI/ITH` — an
OMTI airglow-imager station at Ithaca whose definition ends "Collaborators: MIT Haystack/Cornell U.
This site has already closed." That is a closed Japanese-led imager station listing MIT Haystack as
a collaborator; it is not MIT Haystack Observatory, and it must not be used as a stand-in.

**Rows for facilities the package merely mentions in examples — considered and not selected**, so
that they are not mistaken for oversights. `https://spase-metadata.org/SMWG/Observatory/AMISR`
(abbreviation `AMISR`, whose definition covers PFISR, RBO and RISR-N) is the row a `PFISR` search
reaches, and **it too was specifically offered and declined**: PFISR appears in this package only in
`exampleMadrigalWebServices.py`, in a walk-through of searching several Madrigal sites, which
demonstrates the API rather than supporting that facility. The `Jicamarca` rows in the vocabulary
(`https://spase-metadata.org/SMWG/Instrument/IGPPLANL/Jicamarca/Magnetometer`,
`https://spase-metadata.org/SMWG/Observatory/IGPPLANL/Jicamarca`,
`https://spase-metadata.org/ISWI/Observatory/GIRO/JI91J_Jicamarca`) are a magnetometer and a
digisonde, none of them the "Jicamarca IS Radar" named in the CLI example string.

**Rules that constrain any future change to these two fields.** Both fields are SPASE-only: a
recorded value must carry an identifier beginning `https://spase-metadata.org/`. There is no
free-type path — a bare name either binds arbitrarily to some same-named row or creates a new
identifier-less row, reintroducing exactly the legacy rows a prior cleanup removed. The vocabulary
was checked for that condition during this refresh and every row carries a SPASE identifier; a row
failing that guard in future is a defect to report, never a value to use.

**Improving on the pre-campaign dossier.** It recorded these fields as "Not applicable", which
reached the same outcome but for a reason that would not survive scrutiny — it did not distinguish
"no facility association exists" from "the association was hard to resolve", and it left no record
of which vocabulary rows had been examined. The outcome is unchanged; the reasoning is now
falsifiable and the rejected candidates are enumerated.

---

### 33. Logo (OPTIONAL)
**Not found — no logo exists for this software.**

Three independent places were checked, and this is a documented omission rather than an unsearched
field.

- **The repository contains no images at all.** Of the 26 tracked paths at the pin, **none** has an
  image extension (`.png`, `.jpg`, `.jpeg`, `.svg`, `.gif`, `.ico`, `.webp`), and a sweep for image
  or badge markup (`![`, `<img`, `shields.io`, `badge`, `logo`) matches **no line in any file**.
  There is no README banner, no docs logo and no badge row.
- **Neither documentation host serves one.** `https://cedar.openmadrigal.org/` (title
  "Madrigal database at CEDAR") references exactly one image asset, `/static/favicon.ico`;
  `https://madrigalweb.readthedocs.io/en/latest/` (title "MadrigalWeb Docs") references exactly one,
  `img/favicon.ico`. **A favicon is a site icon, not a software logo**, and in both cases it belongs
  to Madrigal-the-database or to the docs theme rather than to this Python client. Neither is a
  candidate, and neither should be pressed into service by a later refresh.
- **The live PyHC registry entry has no `logo:` key** for MadrigalWeb — unlike, for example, pysat's
  entry, which does carry one. PyHC would be the most likely external source of a curated logo, and
  it has none.

A documented absence is the correct outcome here. No logo should be invented, and no favicon,
example plot or screenshot should be substituted.

---

## Notes on the sources this record depends on

**PyHC registry — pin the file, and note the entry moved.** MadrigalWeb appears in the live
`_data/projects.yml` (the **evaluated** community list), with `url: "https://cedar.openmadrigal.org"`,
`code: "https://github.com/MITHaystack/madrigalWeb"`,
`docs: "https://madrigalweb.readthedocs.io/en/latest/"`,
`description: "MadrigalWeb - a Python API to access the Madrigal database"`,
`contact: "Katherine Cariglia"`, and keywords `geospace`, `data_retrieval`, `ascii`, `hdf5`,
`netcdf`, `web_service`, `data_access`. Its PyHC standards badges read "Partially met" for community
and documentation, and "Good" for testing, software maturity, python3 and license. It is **absent
from both `projects_core.yml` and `projects_unevaluated.yml`**.

**This corrects the pre-campaign dossier in a way that matters.** That file described MadrigalWeb as
having "PyHC unevaluated status - not yet fully reviewed by PyHC standards", and drew its keywords
from the unevaluated list. That was accurate in December 2025 and is stale now: PyHC has since
evaluated the package and moved it to the community list, replacing
`keywords: [ionosphere_thermosphere_mesosphere, general]` with the seven-keyword set above and
changing the contact from Bill Rideout to Katherine Cariglia. A future refresh should read the live
registry rather than any cached copy, and should check all three list files rather than assuming
which one an entry is in. (An untracked, gitignored December-2025 copy of the unevaluated list
survives in the working tree of the local clone; it is a leftover artifact, is not part of the
software, and must not be treated as current or staged.)

**Repository state at the pin, for orientation.** 26 tracked paths; 22 commits in the pinned
ancestry; 0 tags and 0 published GitHub releases; no repository wiki (`madrigalWeb.wiki.git` is not
found, so the `has_wiki` flag is meaningless here); no topics; not archived; not a fork; 0 open
issues; default branch `main`; repository created 2024-09-19, last pushed 2026-07-24.

**Exactly two paths have been deleted outright** in that history: `LICENSE` at `ed8ac51`
(2024-09-19, "Delete LICENSE") and `build/lib/madrigalWeb/__init__.py` at `73d748b` (2025-04-10,
"rm test file"). **`license.txt` was not deleted** — `26b1c37` records it as
an `R100` rename from `license.txt` to `LICENSE`, which is why `LICENSE` is present at the pin
and `license.txt` is not. The distinction is worth writing down because the two natural instruments
disagree and both are individually correct: listing ever-added paths that are absent from the tip
yields `license.txt`, while listing deletions yields `LICENSE`. A rename makes those two questions
diverge — the rename source looks added-then-absent and the rename target looks present — so an
absence-from-tip measurement must never be reported as a deletion.
