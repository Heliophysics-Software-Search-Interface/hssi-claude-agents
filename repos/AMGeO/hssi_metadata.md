# HSSI Metadata Extraction Results

**HSSI Software ID:** e57951e6-9761-421e-b482-aebfd2804c81
**Repository:** https://amgeo.colorado.edu/
**Source Revision:** Not capturable — see "Evidence basis" below.
**Extraction Date:** 2026-07-29
**Validation Date:** 2026-07-30
**Validation Status:** PASS
**Final HSSI state:** Fields 2–33 below match the verified live record as of 2026-07-30.

## Source-repository limitation (durable record)

The authoritative AMGeO source repository is **https://github.com/AMGeO-Collaboration/AMGeO**, which is
**private and registration-gated**: it returns 404 anonymously and does not appear in the public
`AMGeO-Collaboration` organization listing. Access is granted only after registering at
https://amgeo.colorado.edu/, agreeing to the license agreement, and submitting a GitHub username on the
account page to become an AMGeO developer. The site's own **Download** and **Documentation** navigation
links both resolve to `/accessdenied`. There is no PyPI or conda distribution.

**Consequence:** the AMGeO core source tree could not be cloned or read, so **no source commit SHA could
be captured** and no field below rests on direct inspection of the core source. This is an evidence
limitation, not a skipped field: every field was investigated against the authoritative public sources
listed below, and fields that could not be established are left explicitly empty with a stated reason.

**Field 3 is correct as-is and requires no change.** HSSI Field 3's definition states: "If the software
is restricted, put a link to where a potential user could request access." `https://amgeo.colorado.edu/`
is exactly that registration portal. The public `AMGeO-Collaboration/AMGeO-API-Release` repository is
supporting evidence only and must **not** be substituted as Field 3.

## Evidence basis (in place of a source revision)

| Source | Detail | Retrieved |
|---|---|---|
| AMGeO official website | `/`, `/about`, `/rules`, `/community` | 2026-07-29 |
| NASA CCMC model catalog | `https://ccmc.gsfc.nasa.gov/models/AMGeO~3`, page Last Updated 2026-07-28 | 2026-07-29 |
| `AMGeO-Collaboration/AMGeO-API-Release` | public official repo @ commit `67d6e9b451f7c4eefae508aaafd99edecb5bb10a` (2021-12-12) — API notebook, committed sample outputs, and **AMGeO runtime logs** | 2026-07-29 |
| Official AMGeO container image | `ghcr.io/amgeo-collaboration/amgeo-api-release-notebook:latest`, image config (built 2021-12-13) | 2026-07-29 |
| `nasa/Kamodo` | `kamodo_ccmc/readers/amgeo_4D.py`, `tests/test_AMGeO.py` — third-party AMGeO reader | 2026-07-29 |
| NSF Award API | `api.nsf.gov` awards ICER-1928403 / 1928327 / 1928358 | 2026-07-29 |
| Zenodo / DataCite / Crossref | DOI records and searches | 2026-07-29 |
| ROR API | organization identifiers | 2026-07-29 |
| PyHC registries | `projects_core.yml`, `projects.yml`, `projects_unevaluated.yml` (read in full) | 2026-07-29 |
| Live HSSI vocabularies | Current controlled values, spelling, punctuation, and identifiers | 2026-07-29 |

**Seed:** this file was seeded from the current live HSSI record, which had 8 populated fields. No prior
`hssi_metadata.md` existed. Existing values were preserved unless authoritative evidence supported a
documented replacement.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source: not applicable to an update of an existing record.*

### 2. Persistent Identifier (RECOMMENDED)
**INTENTIONALLY EMPTY** (live HSSI value is also empty — no change).

*Source / reason:* **No resolvable software DOI for AMGeO exists.** Both the AMGeO "Rules of the Road"
page and the NASA CCMC publication policy instruct users to cite `doi:10.5281/zenodo.3564915` as "the
AMGeO open source software". **That DOI does not resolve** — it 404s at doi.org, at Zenodo, and in the
DataCite API. It appears to be a long-standing project-wide citation error (plausibly an off-by-one for
`3564914`, or a reserved DOI that was never published). A non-resolving DOI must never be written into
HSSI. A Zenodo/DataCite search for "AMGeO" and "assimilative mapping of geospace" returns **no software
deposit for the AMGeO core package** — only the technical report (Field 14), an EarthCube 2022 notebook
contribution, and workshop repositories.

The publication DOI is deliberately **not** placed here: Zenodo types it as a *Technical note* (Text),
not Software, so it belongs in Field 14. Field 2 stays empty until AMGeO publishes a real software DOI.

> **Data-quality finding worth reporting upstream:** the DOI the project itself and NASA CCMC both
> instruct users to cite is dead. This affects every publication that has followed those instructions.

### 3. Code Repository (MANDATORY)
`https://amgeo.colorado.edu/`

*Source: existing HSSI record — **retained unchanged and confirmed correct**. This is the access-request
portal for restricted software, which is precisely what Field 3 specifies. See the source-repository
limitation above.*

### 4. Software Functionality (MANDATORY)
Every value below was confirmed against the live `FunctionCategory` vocabulary. Every subcategory is
accompanied by its parent.

- Coordinate Transforms
- Coordinate Transforms: Ionospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Assimilation
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Physics-Based
- Servers and Environments
- Servers and Environments: Software or Environment Container

**16 values.** Two close judgment calls were settled by checking how the live
HSSI catalog actually uses these categories: `Data Processing and Analysis: File Format Conversion` is
**included**, and `Servers and Environments: Data servers processing and handling` is **excluded**
(see the audit trail below).

*Evidence per value:*

- **Data Assimilation** (+ parent) — the software's defining function. "AMGeO implements data assimilation
  analysis steps expanded... from the Assimilative Mapping of Ionospheric Electrodynamics (AMIE)
  procedure" (/about, CCMC). Bayesian/Kalman measurement-update solution; runtime module
  `AMGeO.update.predict` appears in the official run log.
- **Analysis** (+ parent) — "data assimilation analysis steps"; "Bayesian analysis of high-latitude
  ionospheric electrodynamic variables"; computes analysis increments and posterior covariance/variance
  for uncertainty quantification (project homepage).
- **Data Access and Retrieval** (+ parent) — AMGeO automatically retrieves its own inputs. Runtime log:
  "Loading NASA OMNIWeb Solar Wind Data...", "Loading SuperMAG data...", "Loading SuperDARN data...".
  Official text: "AMGeO software and AMGeO web application services enable automated access to the
  Iridium magnetometer data distributed from AMPERE."
- **Processing** (+ parent) — "designed to streamline data access, collection, preprocessing, and quality
  control steps"; data delivered "in the form expected by the AMGeO software" (/about, CCMC).
- **Coordinate Transforms: Ionospheric** (+ parent) — direct runtime evidence in the official
  `std_out.txt`: "Transforming 248 points from lat,lon,alt to apex..." and "Computing 356872 Apex
  Longitude values to Magnetic Local Time...". The user-facing output grid carries the coordinate
  metadata `longname: 'Modified Magnetic Apex Latitudes'` and is a magnetic-latitude / magnetic-local-time
  grid (24 x 37), so the transform is exposed to users, not merely internal.
- **Data Visualization: 2D Graphics** (+ parent) — **verified directly**: AMGeO writes multi-panel polar
  dial map figures into its own output directory (e.g.
  `amgeo_out/Default/20130106N/AMGeO_N_01062013_16_30.png`, created by `AMGeO.driver_default`). The figure
  contains filled-contour polar maps of Pedersen conductance, Hall conductance, Joule heating and electric
  potential, overlaid SuperDARN drift vectors and observation locations, and an IMF By/Bz clock dial.
- **Models and Simulations** — existing live value, **retained**.
- **Models and Simulations: Empirical** — the prior mean and prior covariance are empirical models.
  Runtime log: "Loading Cousins & Shephard, 2010 (CS10) electric potential model...", "Loading CS10
  covariance...", "Loading OvationPyme conductance model...". FAC priors use "empirical orthogonal
  function analysis to Iridium data (e.g. Matsuo et al. 2015)" (homepage). Auroral conductivity uses the
  Ovation Prime empirical model (Newell et al., JGR 2009) and empirical relationships of Robinson et al.
  (JGR 1987) (/about FAQ Q4).
- **Models and Simulations: Data Guided** — the exact definition of an assimilative analysis: the solution
  is driven by observations ("adding up the analysis increments from all observations with the prior
  mean").
- **Models and Simulations: Physics-Based** — derived quantities are computed from physical relationships,
  not just fitted: electric field from the potential gradient (output `E_ph`/`E_th`), Joule heating with
  the documented definition `longname: 'Joule Heating (E-field^2*Pedersen)'`, and increments transformed
  "using the physical relationship between plasma drifts and electrostatic potential" /
  "between magnetic perturbations and toroidal magnetic potential" (homepage).
- **Servers and Environments: Software or Environment Container** (+ parent) — official Release 3.0 note:
  "A docker image of AMGeO is now available with a tutorial and jupyter lab pre-installed". Published
  image `ghcr.io/amgeo-collaboration/amgeo-api-release-notebook`, whose config confirms AMGeO installed
  inside the image.

- **File Format Conversion** (+ parent) — included. Release 3.0 added the ability to
  "produce TIEGCM input files" (official homepage), converting AMGeO's own assimilative output into
  another model's input format for model coupling; AMGeO also reads SuperDARN HDF5 and SuperMAG ASCII and
  writes HDF5. The category is well established in the catalog — **26 HSSI entries use it**, including
  SunPy, SpacePy, PySPEDAS, pysat, pyDARN and Speasy — so applying it to a documented cross-model
  input-generation feature is consistent with catalog practice rather than a stretch.

*Considered and deliberately excluded (audit trail):*

- `Servers and Environments: Data servers processing and handling` — **considered and rejected.** The
  official framing does say "The platform is made of the AMGeO open-source software **and web application
  services**", and CCMC lists the "University of Colorado AMGeO Data Service" as a required component with
  its own API token. But what HSSI catalogs here is the **open-source software**, which is a *client* of
  that service, not the service itself. The two live HSSI entries using this category — the CCMC Kamodo
  Analysis Suite and punchbowl — are both software that *is* the server-side processor. Applying it to a
  client analysis tool would return AMGeO to users browsing for data-server software.
- `Mission-related` and all its children — AMGeO is not part of any mission's ground system or pipeline.
  It consumes multi-facility observatory-network data products; that is Data Access, not Mission-related.
- `Models and Simulations: Forecasting` — no forecast/nowcast capability. AMGeO requires observations for
  the target epoch and is a reanalysis tool; no public source claims prediction.
- `Models and Simulations: First Principles` — the NSF abstract's phrase "in a manner consistent with
  first-principles" describes respecting physical relationships, not solving first-principles equations.
  Captured by `Physics-Based` instead.
- `Models and Simulations: Forward-Fitting` — AMGeO uses observation operators and Matsuo's method
  reference is titled an "Inverse and Data Assimilation Procedure", but the Kalman measurement update is
  an analytic linear inversion, not synthetic-data generation with iterative parameter optimization.
- `Models and Simulations: MHD` — no MHD solver.
- `Data Processing and Analysis: Time Series Analysis` — AMGeO *produces* time-ordered maps and
  hemispheric integrated Joule-heating series, but performs no temporal filtering, trend, or correlation
  analysis; the Kalman step is a per-epoch measurement update with no time propagation.
- `Data Processing and Analysis: Data Reduction` — preprocessing/quality control is already covered by
  `Processing`; no averaging/binning/downsampling is documented as a user-facing capability.
- `Data Processing and Analysis: ML/AI` — the method is Bayesian/Gaussian-process estimation. Although
  GP regression is sometimes labelled machine learning, the project never frames itself as ML/AI and there
  is no evidence of ML frameworks. Recorded here rather than asserted.
- `Data Visualization: Movies` and `Line Plots` — no evidence AMGeO itself produces animations or line
  plots. (A third-party OSF project published AMGeO map *movies*, but that is a user product.)
- `Data Visualization: Web-Based` — AMGeO's web application services provide **data acquisition**, not
  interactive visualization; the website's map gallery is static marketing imagery.
- `Servers and Environments: Distribution/Access` — CCMC Runs-on-Request is a distribution service CCMC
  operates *around* AMGeO, not functionality AMGeO implements.

### 5. Related Region (MANDATORY)
- `Earth Ionosphere`
- `Earth Auroral Subregion`
- `Earth Magnetosphere`
- `Earth Thermosphere` *(included based on the documented thermospheric energy coupling)*

All four were confirmed against the live `Region` vocabulary.

*Source / reason:*
- **`Earth Ionosphere`** *(added)* — the core purpose: "complete maps of **high-latitude ionospheric
  electrodynamics**" (/about, CCMC). Every output quantity is an ionospheric electrodynamic variable.
- **`Earth Auroral Subregion`** *(added)* — CCMC's own Domains field reads "High Latitude Ionosphere /
  **Auroral Region**". Auroral conductance is computed with Ovation Prime; the NSF abstract frames the
  science as polar-region energy exchange "as evidenced by the aurora".
- **`Earth Magnetosphere`** — **existing live value, retained.** Independently corroborated: AMGeO
  produces field-aligned current maps, and "Field-aligned currents flow into and out of the ionosphere,
  electrically connecting it to the magnetosphere" (homepage). The NSF abstract states AMGeO "will provide
  a coherent, simultaneous and inter-hemispheric picture of **magnetosphere-ionosphere coupling**".
- **`Earth Thermosphere`** *(added — **a close call, decided in favour of inclusion**)* — three converging
  lines of evidence support it: (1) the NSF award abstract frames the science as electromagnetic energy and
  momentum deposition into the **upper atmosphere**, causing "global temperature and neutral mass density
  enhancement"; (2) Joule heating rate is a primary AMGeO output and is the principal high-latitude
  thermospheric energy input; (3) Release 3.0 added generation of **TIEGCM** (Thermosphere-Ionosphere-
  Electrodynamics GCM) input files, i.e. AMGeO output is explicitly intended to drive a thermosphere model.

  **Why it was close, recorded for future reviewers.** The argument against is not weak: NASA CCMC — the
  most authoritative third-party description of AMGeO — states the domain as "**High Latitude Ionosphere /
  Auroral Region**" only, and never mentions the thermosphere; and AMGeO does not solve for any
  thermospheric state variable (no neutral density, temperature, or winds). Under a strict reading of
  Field 5 as "the region whose state the software solves for", this value would be dropped.
  It was **kept** on the broader reading that Field 5 asks which region the software "supports science
  functionality for": AMGeO is a standard means of producing the high-latitude electrodynamic drivers that
  thermosphere GCMs consume, so a researcher working on thermospheric energy input should find it. A future
  reviewer preferring the strict reading can remove this one value without disturbing the other three.

### 6. Authors (MANDATORY)
**Author 1 — retained exactly as stored:**
- **Author Name:** AMGeO Collaboration *(stored as givenName `AMGeO`, familyName `Collaboration`)*
- **Author Identifier:** *(empty)*
- **Affiliation:** University of Colorado Boulder — `https://ror.org/02ttsq026`

*Source:* existing HSSI record, independently corroborated by two authoritative sources. The project's own
attribution rule requires crediting the collective: "provide attribution to the **AMGeO Collaboration
(Lead Authors of the Licensed Software)**" (/rules). The Zenodo technical report's sole creator is
"AMGeO Collaboration". The affiliation matches "It is developed at the University of Colorado Boulder by
the AMGeO Team" (/about); the ROR was verified live (display name `University of Colorado Boulder`), and
HSSI already holds this exact Organization row.

*Author Identifier left empty — reason:* the AMGeO Collaboration is an organization-style author, so a ROR
would be the correct identifier, but **no ROR exists for it** (ROR API returns 0 results for "AMGeO"). No
ORCID applies to a collective. Leaving it empty is correct; do not substitute the CU Boulder ROR, which
would misidentify the author as the university.

**Individual contributors are not added as software authors.** Willem Mirkovich, Tomoko Matsuo, and
Liam Kilcommons authored the *AMGeO 2.0 EarthCube paper*, but no authoritative software author list
names them individually. The project's attribution statement instead directs credit to the AMGeO
Collaboration as a body, and its community page says individual contributors become part of that
Collaboration. The collective author therefore remains the complete software author value.

### 7. Software Name (MANDATORY)
`AMGeO`

*Source:* existing HSSI record — **retained unchanged**. Corroborated as the software's name by CCMC's
catalog entry ("AMGeO"), the project's own usage ("the AMGeO open-source software"), and the private
repository name. The expansion "Assimilative Mapping of Geospace Observations" is the project/platform
title used as the site heading and appears in the description; it is not the software package name.

### 8. Description (MANDATORY)
**Enriched description preserving the existing technical content, with four source-text corrections.**

The previously stored description was accurate and technically specific but began mid-method, so it never
said what AMGeO *is*, and its first ~200 characters made a poor preview. The final text prepends two
paragraphs of official platform-level framing (verbatim from `/about`, identical text on CCMC) plus one
factual paragraph of inputs/outputs, then reproduces the three existing paragraphs **unchanged,
with only the four corrections listed below**, and closes with an access note. No sentence,
claim, or citation is removed or reworded — the corrections are limited to two spacing defects, one
misspelled author surname, and one dangling figure reference.

```
AMGeO is a collaborative data science platform for the geospace science community for bringing together a diverse set of heterogeneous geospace observations from NSF-funded facility programs and individual community users to obtain complete maps of high-latitude ionospheric electrodynamics for scientific discovery and space weather research. The platform is made of the AMGeO open-source software and web application services that facilitate the data acquisition and pre-processing steps that are otherwise prohibitively labor-intensive. It is developed at the University of Colorado Boulder by the AMGeO Team, with support from the NSF Earth Cube program.

The AMGeO open-source software is designed to streamline data access, collection, preprocessing, and quality control steps with data assimilation analysis steps to support accessible, reproducible and transparent data science practices in the geospace science community. AMGeO helps accelerate data science processes by transforming raw data into discovery enabling forms. AMGeO implements data assimilation analysis steps expanded, as summarized in Matsuo (ISSI Scientific Report Series, 2020), from the Assimilative Mapping of Ionospheric Electrodynamics (AMIE) procedure originally developed by Richmond and Kamide (JGR, 1988).

AMGeO ingests SuperDARN plasma drift data, SuperMAG ground-based magnetometer data, and Iridium magnetic field data provided by the AMPERE program, and produces ionospheric electric potential, electric field, Hall and Pedersen conductance, field-aligned current, and Joule heating rate on a 24 x 37 magnetic latitude / magnetic local time grid.

AMGeO combines the prior information of high-latitude ionospheric electrodynamic variables with multiple types of observations according to Bayes' rule. Under the Gaussian process assumption, AMGeO's solution for the posterior distribution is given by Kalman filter measurement update equations.

The prior distribution is specified by the prior mean and covariance. The prior covariance is less known but plays an important role in balancing weights of the prior mean and observations and spreading the observation information into data-void areas.

In AMGeO, the prior mean for electrostatic potential patterns is specified by an empirical model developed by Cousins and Shepherd (JGR, 2010). Just like this prior mean model, the prior covariance model was developed using a large volume of SuperDARN data (Cousins, Matsuo and Richmond, JGR, 2013).

AMGeO is made available at no charge for non-commercial research use; the source code is obtained by registering at https://amgeo.colorado.edu/. AMGeO is also available through the NASA CCMC Runs-on-Request service.
```

*Sources:* paragraphs 1–2 verbatim from `https://amgeo.colorado.edu/about` (identical wording on CCMC's
`models/AMGeO~3`). Paragraph 3 from CCMC's Inputs/Outputs fields plus /about FAQ Q1 and the homepage
field-aligned-current map description. Paragraphs 4–6 are the existing HSSI description, reproduced in
order with only the four editorial corrections below applied.
Paragraph 7 from `/rules` and CCMC.

**Text corrections.** Four defects inherited from the AMGeO homepage carousel were corrected in the
final value above. The corrections change
no meaning and no citation target.

1. `"high - latitude"` → `"high-latitude"` — stray spaces around the hyphen.
2. `"covariance.The prior covariance"` → `"covariance. The prior covariance"` — missing space after the
   full stop.
3. `"Cousins and Shephard (JGR, 2010)"` → `"Cousins and Shepherd (JGR, 2010)"` — **the correct surname is
   Shepherd.** Verified via Crossref: Cousins, E. D. P. & **Shepherd**, S. G. (2010), "A dynamical model of
   high-latitude convection derived from SuperDARN plasma drift measurements", *JGR*,
   `https://doi.org/10.1029/2010JA016017`. This is the substantive correction of the four: a real
   researcher's surname in a citation, where a misspelling misattributes credit and breaks citation
   matching. Noted for the record: **AMGeO's own code repeats the same misspelling** — the official runtime
   log reads "Loading Cousins & Shephard, 2010 (CS10) electric potential model" — so this is an improvement
   over upstream rather than a fidelity fix, and it is deliberate.
4. `"the prior mean (above)"` → `"the prior mean"` — removed a dangling reference to a figure that appears
   above this text on the AMGeO homepage but has no referent in an HSSI record.

### 9. Concise Description (OPTIONAL)
`Collaborative data science tool for high-latitude geospace observations`

*Source:* existing HSSI record — **retained unchanged**. Verified to be the project's own tagline,
verbatim from the AMGeO homepage banner (directly beneath "Assimilative Mapping of Geospace
Observations"). 70 characters, well within the 200-character limit. No change warranted.

### 10. Publication Date (RECOMMENDED)
`2019-12-07` — a documented proxy rather than a directly stated first-publication date.

*Source / reasoning:* no source states a first-publication date for the AMGeO software. The most
defensible proxy is the publication date of the AMGeO technical report,
`10.5281/zenodo.3564913` / `.3564914`, issued **2019-12-07** (DataCite `dateType: Issued`), whose own
description reads "This document describes the Assimilative Mapping of Geospace Observations (AMGeO)
**v1.0.0**" — so v1.0.0 existed and was documented on that date. Consistent with NSF award start
2019-09-01. This is a documented proxy rather than a directly attested first-publication date.

### 11. Publisher (RECOMMENDED)
- **Organization:** University of Colorado Boulder
- **Publisher Identifier:** `https://ror.org/02ttsq026`

*Source / reasoning:* no DOI-based publisher exists (Field 2 is empty). The
license text names the publishing entity directly: "The Regents of the University of Colorado, a body
corporate, for the University of Colorado Boulder, **is making available the AMGeO software package**"
(/rules). CU Boulder also hosts the distribution portal and the AMGeO Data Service. ROR verified live;
HSSI already holds this exact Organization row, so no duplicate is created.

*Alternative considered:* Field 11's guidance says "If no DOI has been obtained, indicate the repository
host, such as GitHub or GitLab." That would give `GitHub`, but the repository is private and is not the
route by which the software is published to users — the CU Boulder portal is. CU Boulder is the more
accurate answer.

### 12. Version (RECOMMENDED)
- **Version Number:** `3.0.8`
- **Version Date:** `2025-07-31`
- **Version Description:** see below
- **Version PID:** *(empty — no per-version DOI exists; see Field 2)*

**This fills a gap: the live HSSI version row stores an empty version number** (the view API renders it as
`"AMGeO - "`, which is the `<software> - <number>` display transform over an empty value). Issue #57 found
no version.

*Source:* **NASA CCMC model catalog** `https://ccmc.gsfc.nasa.gov/models/AMGeO~3`, Change Log:
"**Version 3.0.8 was deployed on the CCMC ROR system on July 31, 2025.**" The catalog header reads
"Version: 3", and CCMC's publication policy refers to "the AMGeO open source software **version 3**".

*Version Date basis:* 2025-07-31 is the CCMC deployment date — the only date published for 3.0.8. Recorded
as such rather than as an upstream release date.

*Newest-version re-check (per instruction):* nothing newer than 3.0.8 could be found. The project
homepage's latest news item is still "AMGeO Release 3.0", dated May 24, 2023; there is no PyPI/conda
release; the private repo is unreadable; and no Zenodo/DataCite record post-dates 2022. 3.0.8 (2025-07-31)
is the most recent authoritative version statement in existence.

**Version Description:**
```
Release 3.0 series. Adds a Docker image of AMGeO with a tutorial and JupyterLab pre-installed; adds generation of TIEGCM input files and the ability to save observational data for the user; adds the ability to turn SuperDARN observational data assimilation on and off. Version 3.0.8 was deployed on the NASA CCMC Runs-on-Request system on 2025-07-31; no 3.0.8-specific change notes are published.
```
*Source:* the feature list is verbatim in substance from the official Release 3.0 news item (project
homepage, May 24, 2023); the final sentence records the CCMC change-log fact and is explicit that no
patch-level notes exist, so no reader mistakes 3.0 notes for 3.0.8 notes.

The stored version number is the bare value `3.0.8`; `AMGeO - 3.0.8` is presentation only.

### 13. Programming Language (RECOMMENDED)
- `Python 3.x`

*Source:* CCMC catalog, Code section: "Code Languages: **Python**". The NSF award abstract describes
"an open-source **Python** software". Python **3** specifically confirmed by the official container image,
which installs Miniconda `py39_4.10.3` (Python 3.9) and then installs AMGeO into it, and by Python-3-only
syntax (f-strings) in the official API notebook. Confirmed against the live `ProgrammingLanguage`
vocabulary.

*Considered and excluded — Fortran:* the official container's build history runs
`apt-get install gcc gfortran` before installing AMGeO's requirements, and the runtime `std_out.txt`
contains raw Fortran console output from the Apex coordinate library ("Preparing interpolation
tables...", "Transforming 248 points from lat,lon,alt to apex..."). This proves a **Fortran toolchain is
required to build AMGeO's dependencies**, but the Fortran code lives in third-party compiled extensions
(Apex, IGRF), not in AMGeO's own source. CCMC — the authoritative, project-reviewed catalog — lists Python
only. Recorded here; add a Fortran row only if the user wants build-chain languages represented.

### 14. Reference Publication (RECOMMENDED)
`https://doi.org/10.5281/zenodo.3564913`

*Source:* the project's own designated citation. `/rules` states: "a reference to the appropriate digital
object identifier for the version of the AMGeO software used. For AMGeO v1.0.0, please reference the
**AMGeO technical report**" — which links to this Zenodo record. It is also the **first** publication
listed in CCMC's Publications section.

Verified via DataCite: AMGeO Collaboration (2019), "A Collaborative Data Science Platform for the Geospace
Community: Assimilative Mapping of Geospace Observations (AMGeO)"; publisher Zenodo; issued 2019-12-07;
resource type *Technical note*; licensed CC-BY-4.0. `10.5281/zenodo.3564913` is the **concept** DOI (all
versions) and `10.5281/zenodo.3564914` the version DOI; the concept DOI is used here for durability. Both
resolve.

### 15. License (RECOMMENDED)
- **License:** `Other`
- **License URI:** `https://amgeo.colorado.edu/rules`

`Other` is used because AMGeO has a specific non-SPDX institutional license. The closest analogue —
**TIEGCM v3.0**, distributed under the custom "NCAR TIE-GCM OPEN SOURCE ACADEMIC RESEARCH LICENSE
AGREEMENT" (research/non-profit only, no sales, reported as `NOASSERTION` by GitHub) — is recorded in HSSI
as **`Other`**. AMGeO's license has the same shape: a real, specific, non-SPDX institutional agreement.
`Restricted` would also overstate the barrier, since the software is free to anyone who registers and is
runnable without registering at all via CCMC Runs-on-Request.

*Source:* `/rules`, "License Agreement": "The Regents of the University of Colorado, a body corporate,
for the University of Colorado Boulder, is making available the AMGeO software package **at no charge for
non-commercial research use** under the terms and conditions detailed in the license agreement." The
license-agreement document itself sits behind `/accessdenied`, so **no public license URI exists**; the
URI above is the public page that states the terms. CCMC summarises access as "Open-source (requires
registration at https://amgeo.colorado.edu/)". The Zenodo AMGeO 2.0 record uses Zenodo license id
`other-open`.

*Basis for `Other`:* a real, specific, named license genuinely exists — a CU Boulder
non-commercial research agreement — it simply is not an SPDX license. Field 15 directs that a license
title absent from the row list must use `Other`. The project self-describes as "open-source" throughout
and publishes under FAIR principles.
`Restricted` was considered because access is gated by registration and a non-commercial-use
restriction, but it would describe access rather than the license AMGeO actually supplies.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
Each of the 23 values below was checked against the live `Keyword` vocabulary to reuse an existing row
rather than mint a near-duplicate. Stored lowercase (the view renders Title Case).

**Reusing existing rows (13):**
`ionosphere` · `geospace` · `space weather` · `open source` · `electrodynamics` ·
`field-aligned currents` · `joule heating` · `aurora` · `ground magnetometer` ·
`magnetic apex coordinates` · `magnetic local time` · `tiegcm` · `gaussian processes`

**New rows (10):**
`data assimilation` · `ionospheric electrodynamics` · `ionospheric conductance` ·
`magnetosphere-ionosphere coupling` · `high-latitude` · `kalman filter` ·
`electrostatic potential` · `plasma drift` · `earthcube` · `cross polar cap potential`

*Sources:* `data assimilation`, `geospace`, `open source`, `earthcube` are Zenodo's own subject terms on
the AMGeO technical report ("Python, Geospace, Open-source, EarthCube, Data Assimilation").
`ionospheric electrodynamics` and `cross polar cap potential` render CCMC's two Phenomena entries
("Ionosphere Electrodynamics", "Cross-polarcap Electric Potential"), which have **no rows in the closed
Phenomena vocabulary** and therefore belong here (see Field 22). `field-aligned currents`,
`joule heating`, `electrostatic potential`, `ionospheric conductance` and `plasma drift` are AMGeO's
output/input quantities. `magnetic apex coordinates` and `magnetic local time` match the verified output
coordinate metadata ("Modified Magnetic Apex Latitudes"; Apex-longitude-to-MLT conversion).
`magnetosphere-ionosphere coupling` and `high-latitude` are from the NSF award abstract and /about.
`ground magnetometer` reflects the SuperMAG input. `tiegcm` reflects Release 3.0's TIEGCM input-file
generation. `aurora` from the NSF abstract and the Ovation Prime auroral conductance model.

*Deliberately not used as keywords:* `superdarn`, `supermag`, `ampere`, `iridium` (covered by Fields
31/32), `python` (Field 13), `omniweb` (Field 17), `hdf5` (Fields 18/19) — Field 16 is for keywords "not
supported by other metadata fields". Redundant keyword copies were deliberately omitted.

### 17. Data Sources (OPTIONAL)
- `OMNIWeb`
- `Observatory/Mission-specific`
- `Other`

All three were confirmed against the live `DataInput` vocabulary.

*Source:*
- **`OMNIWeb`** — CCMC Caveats: "Model must be able to access the internet to contact the University of
  Colorado AMGeO Data Service and **NASA OmniWeb** to get required data for assimilative procedure."
  Corroborated by the official runtime log ("Loading NASA OMNIWeb Solar Wind Data for 2013-01-06...") and
  by the `nasaomnireader` cache path in the notebook's import output. Kamodo's AMGeO reader confirms the
  OMNI-derived values `imf_By`, `imf_Bz`, `solar_wind_speed` are carried into AMGeO's output files.
- **`Observatory/Mission-specific`** — the required cross-listing whenever Field 32 names missions
  (Field 17's own instruction). AMGeO's science inputs come from the SuperDARN, SuperMAG and AMPERE
  services, each requiring per-service credentials.
- **`Other`** — the **University of Colorado AMGeO Data Service**, a project-specific web service
  requiring an API token from amgeo.colorado.edu, has no vocabulary row. Field 17 instructs "If a source
  is not listed, select 'Other'."

*Considered and excluded:* `HTTP/HTTPS Directories` — the AMGeO Data Service, SuperMAG and AMPERE are
token/credential-authenticated web APIs, not browsable HTTP directory listings; recorded rather than
asserted. `CDAWeb`, `Madrigal`, `HAPI`, `FTP/FTPS Directories`, `S3/Cloud-aware` — no evidence. There are
no SuperDARN/SuperMAG/AMPERE rows in this vocabulary; per Field 17 those missions belong in Field 32.

### 18. Input File Formats (RECOMMENDED)
- `HDF5`
- `ascii`

Direct runtime evidence supports both values, which were confirmed against the live `FileFormat`
vocabulary.

*Source — the official AMGeO run log committed in `AMGeO-API-Release/amgeo_out/Default/20130106N/log.txt`,
which is genuine output of the private core software:*
- **`HDF5`** — "`AMGeO.observations.superdarn`: **Reading HDF5 file** .../SD_grid_20130106N.h5" — the
  SuperDARN grid2 plasma-drift product is delivered and parsed as HDF5. Strongest of the three.
- **`ascii`** — "`AMGeO.observations.supermag`: **Reading SuperMAG ASCII data file**
  .../20130106-supermag.txt", including a header-format check ("Expected 71 lines"). Additionally, the
  OMNI reader's fallback path reads "Omni text files" when spacepy is unavailable (notebook import output).
*Considered and excluded:*
- **`csv`** — **considered and rejected.** The run log does show "`AMGeO.observations.supermag`:
  **Reading SuperMAG Stations CSV file** .../files/tables/test_amgeo_obs/supermag-stations.csv", but the
  path is decisive: this is a **station-metadata lookup table shipped inside the AMGeO package** under
  `files/tables/`, not science data the user supplies or can substitute. Field 18 asks for "the file
  formats the software supports for **data input**"; listing `csv` would tell users they can feed AMGeO
  CSV science data, which they cannot. AMGeO's actual science inputs are the SuperDARN HDF5 grid2 product
  and the SuperMAG ASCII product, both fetched from their services.
- `CDF` — no evidence. The optional `spacepy` path for OMNI data does not demonstrate CDF reading.
- `netCDF3/4`, `FITS`, `JSON`, `Zarr`, `IDL.sav`, `ISTP-Compliant` — no evidence.

### 19. Output File Formats (RECOMMENDED)
- `HDF5`
- `Other`

*Source:*
- **`HDF5`** — verified two independent ways. (1) The official API-release repo contains AMGeO's own
  committed output files `amgeo_out/Default/<YYYYMMDD><hemi>/amgeo_v2_<YYYYMMDD><hemi>.h5`, written by
  `AMGeO.driver_default`. (2) The third-party `nasa/Kamodo` reader `kamodo_ccmc/readers/amgeo_4D.py`
  globs `*.h5`, opens them with h5py, and reads both datasets and file attributes — an external
  confirmation of the on-disk format and its per-hemisphere daily naming convention.
- **`Other`** — covers two real outputs with no vocabulary row: (a) **PNG summary map figures**, verified
  directly (`AMGeO_N_01062013_16_30.png`, a multi-panel polar dial figure written into AMGeO's own output
  directory); and (b) **TIEGCM input files**, added in Release 3.0.

*Deliberately NOT asserted — the TIEGCM input-file format.* Release 3.0 states AMGeO "can now produce
TIEGCM input files", but no public source specifies whether these are ASCII namelist control files or
netCDF driver files, and TIEGCM uses both. Rather than guess, neither `ascii` nor `netCDF3/4` is claimed
here; the capability is represented by `Other` and recorded as unverified. Plain-text run artifacts
(`log.txt`, `std_out.txt`, `std_err.txt`) are diagnostics, not data outputs, and are not counted as
`ascii`.

### 20. Operating System (RECOMMENDED)
- `Linux`
- `Mac`

The official container image and runtime paths support both values, which were confirmed against the
live `OperatingSystem` vocabulary.

*Source:*
- **`Linux`** — the official published AMGeO container image
  `ghcr.io/amgeo-collaboration/amgeo-api-release-notebook:latest` has image config `"os": "linux"`, and its
  build history shows AMGeO itself installed inside it (`unzip AMGeO-main.zip`, `pip install -r
  requirements.txt`, `python setup.py develop`) on a Debian-based Miniconda base. That is a verified,
  published, successful Linux installation. The README's install link points to
  `docs.docker.com/engine/install/` (Docker Engine, i.e. Linux).
- **`Mac`** — the official API notebook's committed outputs and run log were produced on macOS: AMGeO's
  own data cache resolves to `/Users/willemmirkovich/Library/Application Support/AMGeO` and
  `.../Library/Application Support/nasaomnireader`, the macOS-specific application-support convention.
  That is a verified successful macOS installation and run.

*Considered and excluded:* `Windows` — no evidence. Running the Linux container under Docker Desktop for
Windows demonstrates the *container's* OS, not a Windows installation of AMGeO.
`Operating System Independent` — not claimed; AMGeO requires a Fortran toolchain to build its dependencies
(`gcc gfortran` in the container build), which makes a blanket platform-independence claim unsupportable.
Note `OS Independent` is **not** a valid row; the only cross-platform row is `Operating System
Independent`, spelled in full.

### 21. CPU Architecture (RECOMMENDED)
- `x86-64`

The container image config supports this value, which was confirmed against the live `CpuArchitecture`
vocabulary.

*Source:* the official AMGeO container image config reports `"architecture": "amd64"` (single-architecture
manifest, no multi-arch manifest list — only a `latest` tag exists), and its build history selects the
`Miniconda3-py39_4.10.3-Linux-x86_64.sh` installer. That is a verified x86-64 build of AMGeO.

*Considered and excluded:* `Apple Silicon arm64` — the macOS run (December 2021) cannot be attributed to
Intel or Apple Silicon from the available evidence, so no arm64 claim is made. `CPU Independent` — not
claimed; compiled Fortran/C extensions are architecture-specific. `GPU`, `HPC or HEC`, `ppc64le`,
`Sun (SPARC)` — no evidence.

### 22. Related Phenomena (OPTIONAL)
**INTENTIONALLY EMPTY.**

*Reason:* the `Phenomena` vocabulary is a **closed** 7-row list (`Coronal Heating`, `Coronal Mass
Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`, `X-ray emission`;
re-fetched 2026-07-29) and **none of them is supported by the evidence**:

- CCMC's own Phenomena for AMGeO are "**Ionosphere Electrodynamics**" and "**Cross-polarcap Electric
  Potential**". Neither has a row. Per Field 22's instruction, a supported phenomenon with no row belongs
  in **Keywords**, where both have been placed (Field 16).
- `Geomagnetic Storms` was tested and **rejected for lack of evidence**: the strings "storm" and
  "substorm" appear **zero times** across the AMGeO homepage, /about, /rules, /community, the CCMC catalog
  page, and the API-release README. Selecting it would be an unsupported inference.
- `Solar Wind` was considered and rejected: AMGeO *ingests* OMNI solar-wind parameters as drivers for its
  conductance model, but the solar wind is not a phenomenon AMGeO provides science functionality *for*.
  Its science target is high-latitude ionospheric electrodynamics.
- The four solar/coronal rows are out of scope.

An empty Field 22 with this reasoning is the correct outcome; the vocabulary simply lacks AMGeO's
phenomena. **Do not invent rows.**

### 23. Development Status (RECOMMENDED)
`Active`

*Evidence for `Active`* ("reached stable, usable state and being actively developed"):
- **Version 3.0.8 was deployed to NASA CCMC's Runs-on-Request system on 2025-07-31** — a concrete release
  event about a year before extraction, and a patch level (`.8`) beyond the 3.0 announcement, implying
  ongoing maintenance releases.
- The AMGeO-Collaboration organization pushed to its `OvationPyme` and `nasaomnireader` dependency forks
  on **2025-05-14**.
- The software is unambiguously stable and usable: distributed at CCMC, containerized, documented API.

*Evidence for `Inactive`* ("stable and usable but no longer actively developed"):
- All three NSF EarthCube awards have **expired**: ICER-1928403 ended 2023-08-31, ICER-1928327 ended
  2024-02-29, ICER-1928358 ended 2025-08-31.
- The project website's latest news item is still **Release 3.0, May 24, 2023**; the site's own "Get the
  latest source" card has not been updated since.
- No public organization repository has been created or substantively updated since 2022 (apart from the
  two 2025 dependency-fork pushes).
- Zenodo/DataCite show no AMGeO artifact after 2022.

*Why `Active` was chosen:* three points settled it.
1. **NASA CCMC's AMGeO announcement** (`https://ccmc.gsfc.nasa.gov/news/amgeo`) presents 3.0.8 as
   available to the community with **no retirement, deprecation, or maintenance warning** — an independent
   authority publishing the software as current.
2. **Expired NSF awards do not indicate abandonment.** Award expiry is routine for research software that
   continues to be maintained and distributed; it is a funding fact, not a software-status fact. Likewise
   the stale website is *web maintenance*, not development status.
3. **Catalog consistency:** the closest analogue — NCAR's TIEGCM, a comparably long-lived
   institutional model — is recorded as `Active`.

**Genuine limitation, recorded:** the core repository is private, so its commit activity — the single most
direct indicator for this field — could not be observed at all. This value rests on release and
distribution evidence rather than development activity. If AMGeO's status is revisited later, the private
repo remains the missing input.

### 24. Documentation (RECOMMENDED)
`https://amgeo.colorado.edu/`

*Source / reasoning:* the site's official **Documentation** navigation link resolves to `/accessdenied`
(registration-gated), so no public documentation URL exists. Field 24 states: "If this is the same as the
access URL, then enter that link here." The site root is therefore the defensible value, and it is where a
user obtains both access and installation instructions.

*Alternative considered:* `https://github.com/AMGeO-Collaboration/AMGeO-API-Release` is genuine
**public** API documentation — a narrated notebook covering the full `AMGeOApi` / `controller` API plus
Docker and local-install instructions — but it is not the authoritative access and documentation home.

### 25. Funder (OPTIONAL)
- **Organization:** U.S. National Science Foundation
- **Funder Identifier:** `https://ror.org/021nxhr62`

*Source:* `/about` Acknowledgements: "AMGeO is supported by the **NSF EarthCube grants** ICER 1928403 to
the University of Colorado Boulder, ICER 1928327 to the Virginia Tech, and ICER 1928358 to the Johns
Hopkins University Applied Physics Laboratory." All three awards verified against `api.nsf.gov` (program
`EarthCube`). Field 25 instructs "Avoid acronyms", so the acronym NSF is expanded.

*Name choice:* `U.S. National Science Foundation` is the **current ROR display name** for
`https://ror.org/021nxhr62` (`National Science Foundation` is now recorded there as an alias) **and** it is
the name of the Organization row HSSI already holds for that ROR. Using it reuses the existing row instead
of minting a near-duplicate.

### 26. Award Title (OPTIONAL)
Three awards — one collaborative proposal funded under three cooperating institutions. All three share an
identical official title.

1. **Award Title:** EarthCube Data Capabilities: Collaborative Proposal: Assimilative Mapping of Geospace Observations
   **Award Number:** `ICER-1928403`
2. **Award Title:** EarthCube Data Capabilities: Collaborative Proposal: Assimilative Mapping of Geospace Observations
   **Award Number:** `ICER-1928327`
3. **Award Title:** EarthCube Data Capabilities: Collaborative Proposal: Assimilative Mapping of Geospace Observations
   **Award Number:** `ICER-1928358`

*Source:* titles and numbers verified individually against the NSF award API:

| Number | Awardee | PI | Period |
|---|---|---|---|
| ICER-1928403 | University of Colorado at Boulder | Tomoko Matsuo | 2019-09-01 → 2023-08-31 |
| ICER-1928327 | Virginia Polytechnic Institute and State University | J. Michael Ruohoniemi | 2019-09-01 → 2024-02-29 |
| ICER-1928358 | Johns Hopkins University | Brian Anderson | 2019-09-01 → 2025-08-31 |

Corroborated by AMGeO's own Acknowledgements text (above). The technical report's Zenodo record also
carries the note "Supported by NSF ICER 1928403".

*Award-number format:* `ICER-<number>` is the conventional NSF citation form. AMGeO's own page writes
"ICER 1928403" with a space; NSF's API uses the bare number `1928403`. The hyphenated form is
unambiguous.

The previous blank award relationship carried no title, number, or funder and was replaced by the
three verified awards above. Its shared blank Award row remains in the catalog for unrelated entries
and must not be deleted as part of AMGeO maintenance.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
1. `https://doi.org/10.1007/978-3-030-26732-2_10`
2. `https://doi.org/10.1002/essoar.10503482.1`
3. `https://doi.org/10.5281/zenodo.6780967`

*Source / evidence per entry:*
1. **Matsuo, T. (2019), "Recent Progress on Inverse and Data Assimilation Procedure for High-Latitude
   Ionospheric Electrodynamics", in *Ionospheric Multi-Spacecraft Analysis Tools* (ISSI Scientific Report
   Series), Springer.** Verified via Crossref (book-chapter, issued 2019-10-21, sole author Tomoko Matsuo).
   This is the **method reference the official AMGeO description itself cites** ("as summarized in Matsuo
   (ISSI Scientific Report Series, 2020)") and CCMC's **second** listed publication. Strongest entry.
2. **Matsuo, T. (2020), "Assimilative Mapping of Geospace Observations (AMGeO): Data Science Tools for
   Collaborative Geospace Systems Science".** Verified via Crossref (posted-content / ESS Open Archive
   preprint, Wiley, posted 2020-06-23). Directly about AMGeO.
3. **Mirkovich, W., Matsuo, T., Kilcommons, L. (2022), "AMGeO 2.0: Crafting an API for Geospace Data
   Scientists", EarthCube 2022.** This is the paper describing
   the v2 API that the official public notebook demonstrates. The concept DOI is used
   (`...6780967`); the version DOI is `...6780968` (version `ec2022v2`). **Caveat:** Zenodo types this
   record `resourceTypeGeneral: Software` / `SoftwareSourceCode` rather than a publication, because
   EarthCube publishes its annual-meeting contributions as citable notebooks. The artifact functions as a
   conference paper about AMGeO, so Field 27 is the best home; the type mismatch is recorded here.

*Considered and deliberately excluded (audit trail):*
- **Underlying model/method papers** that AMGeO *implements* rather than papers that describe, cite, or use
  AMGeO: Richmond & Kamide (JGR, 1988) — the AMIE predecessor procedure; Cousins & Shepherd (JGR, 2010) —
  prior mean; Cousins, Matsuo & Richmond (JGR, 2013) — prior covariance; Newell et al. (JGR, 2009) —
  Ovation Prime; Robinson et al. (JGR, 1987); Matsuo et al. (2015) — Iridium EOF priors; Gjerloev (2012) —
  SuperMAG processing. These predate or are independent of AMGeO and do not describe it. All are already
  named in the Description, which is the right place for them. CCMC itself lists only two publications.
- **Third-party OSF research projects using AMGeO** (`10.17605/osf.io/26ae5`,
  `10.17605/osf.io/f3vut`) — OSF *project* pages by a student researcher, not developer-prioritized
  publications. See Field 28.
- AGU-2021 presentation materials (`10.5281/zenodo.5775247`, `...5774619`) — presentation deposits, not
  publications the developers prioritize.
- **EarthCube 2021 workshop materials** (`10.5281/zenodo.4793409`, and its pre-citation deposit
  `...4793285`) — a Zenodo snapshot of `AMGeO-Collaboration/Earthcube-Meeting-2021`, whose own
  description is "Repository to host notebook/support materials needed for Earthcube 2021 Meeting".
  Although Zenodo types it `Software`, it has no distinct publication identity (no paper title, release
  note "Included DOI into Earthcube release"), so it is excluded on the same grounds as the AGU-2021
  deposits. Contrast the 2022 EarthCube entry, which *is* included: it has a real paper title and three
  named authors. The source GitHub repo is now archived.

### 28. Related Datasets (OPTIONAL)
**INTENTIONALLY EMPTY.**

*Reason:* the NSF award promised "fully reproduceable, validated **reanalysis data products** that can be
accessed from established data repositories", but **no such published AMGeO dataset with a DOI could be
found.** Zenodo and DataCite searches for "AMGeO" and "assimilative mapping of geospace" return only the
technical report, the EarthCube 2022 contribution, workshop repositories, presentation deposits, and the
two third-party OSF projects below — no dataset-typed AMGeO product from the project. The promised
reanalysis products appear never to have been published under a findable identifier.

Both candidate records are deliberately excluded. They are third-party OSF
**project** pages (DataCite `resourceType: Project`, `resourceTypeGeneral: Text`) by Valerie Claire Svaldi,
not curated datasets from the AMGeO project:
- `https://doi.org/10.17605/osf.io/f3vut` — "Case Study Event Movies" (2022): "AMGeO 5-minuite resolution
  maps displaying global high-latitude ionospheric convection for two STEVE events (March, 26,2008 and
  April 5, 2010) and one non-STEVE substorm event (September 14 2015)." This is genuine AMGeO **output**
  data with a DOI — the closest thing found to a published AMGeO data product.
- `https://doi.org/10.17605/osf.io/26ae5` — "High Latitude Ionospheric Electrodynamics during STEVE Event
  & Non-STEVE Substorm Events" (2021): a research project analysing "ionospheric convection patterns
  estimated from SuperDARN plasma drift and ground-based magnetometer data using the Assimilative Mapping
  of Geospace Observations (AMGeO) procedure."

They are recorded here so the gap is visibly investigated rather than overlooked. Field 28 asks for
datasets the software supports functionality *for*; these are products *of* the software, published by a
third party, so an empty field is the more accurate outcome.

### 29. Related Software (OPTIONAL)
1. `https://github.com/AMGeO-Collaboration/OvationPyme`
2. `https://github.com/AMGeO-Collaboration/nasaomnireader`
3. `https://github.com/AMGeO-Collaboration/apex-python`

These are **domain-specific heliophysics dependencies whose presence characterizes AMGeO**, each with
direct runtime evidence from the official AMGeO run log — not a dependency dump.

*Source / evidence per entry:*
1. **OvationPyme** (Ovation Prime 2010 in Python) — the strongest entry, evidenced three ways:
   (a) `/about` FAQ Q4: "Currently AMGeO uses the **Ovation Prime** model by Newell et al. (JGR, 2009)";
   (b) the official run log shows `AMGeO.driver_default: Loading OvationPyme conductance model...`
   followed by `OvationPyme.ovation_prime` and `OvationPyme.ovation_utilites` executing inside the AMGeO
   run; (c) AMGeO's **own output variable metadata** reads
   `longname: 'Ovation Pyme Hall Conductance'` / `'Ovation Pyme Pedersen Conductance'`. Maintained as a
   fork by the AMGeO-Collaboration organization (pushed 2025-05-14).
2. **nasaomnireader** (Tools for reading NASA OMNIWeb data) — the notebook's AMGeO import prints "Solar
   wind data files will be saved to .../Library/Application Support/**nasaomnireader**", and the run log
   shows "Loading NASA OMNIWeb Solar Wind Data for 2013-01-06...". Consistent with CCMC's caveat that
   AMGeO must contact NASA OmniWeb. Maintained as a fork by the AMGeO-Collaboration organization (pushed
   2025-05-14).
3. **apex-python** (A.D. Richmond's Modified Apex Coordinates with a Python wrapper) —
   Included by direct source match, not inference. The candidate alternative was the
   PyHC package `apexpy` (`https://github.com/aburrell/apexpy`), which wraps the same Richmond Fortran
   library and is itself an HSSI entry. The ambiguity was settled by matching AMGeO's runtime console
   output against both wrappers' source: the two distinctive strings in AMGeO's own
   `std_out.txt` are **literal `print()` statements in `apex-python`**, and appear **nowhere in `apexpy`**.

   | String in AMGeO's runtime output | `apex-python/apexpython/apex_converter.py` | `apexpy` |
   |---|---|---|
   | `Computing 356872 Apex Longitude values to Magnetic Local Time...` | line 358 ✓ | 0 matches |
   | `Transforming 248 points from lat,lon,alt to apex` | line 568 ✓ | 0 matches |

   Corroborating: AMGeO's output coordinate metadata reads `longname: 'Modified Magnetic Apex Latitudes'`.
   `apexpy` is therefore **not** listed — accuracy about what AMGeO actually uses takes precedence over the
   discoverability benefit of linking to an existing HSSI entry.

   *Provenance note (explains the whole dependency set).* Every AMGeO-Collaboration dependency fork traces
   to the same upstream author — `OvationPyme`, `nasaomnireader`, `apex-python`, `esabin` and
   `geospacepy-lite` all have parent `lkilcommons/<name>`. Liam Kilcommons is an AMGeO developer
   (ORCID `0000-0002-4980-3045`, University of Colorado Boulder; see Field 6). AMGeO's domain-specific
   dependency stack is essentially his geospace toolchain, vendored into the project's organization. This
   makes the three listed entries coherent as a set, and is *why* organization membership alone was not
   treated as evidence of use for the others (see the exclusions below).

*Considered and deliberately excluded (audit trail):*
- **`geospacepy-lite`, `esabin`, `igrfpy`** — the AMGeO-Collaboration organization hosts all three
  (`esabin` = equal-solid-angle binning; `igrfpy` = IGRF wrapper; `geospacepy-lite` = geospace utilities),
  and each is plausible in the dependency chain, but **no public evidence ties any of them to an AMGeO
  run**: none appears in the runtime logs, the notebook output, or any official text. The notebook's
  `polar2dial` dial-plot helper is defined inline rather than imported. Organization membership alone is
  circumstantial; excluded in favour of fewer, well-evidenced entries.
- **`spacepy`** — genuinely evidenced but one hop removed: importing AMGeO prints "Unable to import
  spacepy. Will fall back to using Omni text files, which may have slightly different data and incomplete
  metadata", a message emitted by `nasaomnireader` (already listed) rather than by AMGeO. It is an
  *optional* dependency of a dependency. Recorded here; add to Field 29 if the user wants
  dependency-of-dependency relationships represented.
- **AMIE** (Assimilative Mapping of Ionospheric Electrodynamics) — AMGeO's direct procedural predecessor
  and the closest thing to "software this was forked from", but AMIE is a *procedure* published in the
  literature (Richmond & Kamide, JGR 1988), not distributable software with a repository or DOI. It is
  named in the Description instead. This is a genuine Field 29 gap caused by the predecessor not being
  citable as software.
- **Tier A generic stack** — `numpy`, `pandas`, `matplotlib`, `scipy`, `jupyter`, `h5py`, `setuptools`. All
  are present or implied, and all are excluded: being a dependency is not a relationship that distinguishes
  AMGeO. (`h5py` is Tier B, but the demonstrated interchange is the **HDF5 format**, which belongs in
  Fields 18/19, not the library.)

### 30. Interoperable Software (OPTIONAL)
1. `https://github.com/nasa/Kamodo`
2. `https://github.com/NCAR/tiegcm`
3. `https://github.com/pydata/xarray`

Each entry clears the demonstrated-exchange bar with a specific cited artifact.

*Source / evidence per entry:*
1. **Kamodo** — the strongest interoperability evidence available for AMGeO: NASA CCMC's Kamodo (a PyHC
   **core** package) ships a **dedicated AMGeO reader**, `kamodo_ccmc/readers/amgeo_4D.py`, which globs
   AMGeO's `*.h5` output files, reads both datasets and file attributes, and functionalizes **all 17**
   AMGeO variables — including `epot`, `E_ph`/`E_th`, `cond_hall`/`cond_ped`, `jfac`, `mpot`,
   `sdB_ph`/`sdB_th`, `v_ph`/`v_th`, `int_joule_heat_n`/`_s`, and the OMNI-derived `imf_By`, `imf_Bz`,
   `solar_wind_speed`. Corroborated by `tests/test_AMGeO.py` and
   `Validation/Notebooks/ModelReaderTesting_AMGeO.ipynb` in the same repository, and by Kamodo's PyHC
   registry entry listing `amgeo` among its keywords. This is a maintained, tested, third-party ingestion
   of AMGeO's output — exactly "one's output can be imported into the other".
2. **TIEGCM** (NCAR/HAO Thermosphere-Ionosphere-Electrodynamics General Circulation Model) — official
   Release 3.0 announcement (project homepage, May 24 2023): "AMGeO can now **produce TIEGCM input
   files**." A purpose-built converter that turns AMGeO's assimilative maps into another named domain
   model's input format is a genuine cross-tool exchange, not a shared runtime. Repository link used per
   the field's instruction; the model's authoritative home page is
   `https://www.hao.ucar.edu/modeling/tgcm/` (both verified reachable).
3. **xarray** — Tier B, admitted **only** on cited evidence, which exists: `xarray.Dataset` is AMGeO's
   **documented public-API interchange format**, not an internal implementation detail. The official
   API-release notebook states "the ability to load AMGeO maps into [Xarray datasets] ... with no work
   needed other than calling `controller.load`", and the notebook demonstrates `controller.load()`
   returning Datasets with named data variables, `time`/`lat`/`lon` coordinates, and per-variable `attrs`
   carrying `units`/`longname`/`shortname`, plus `ds.to_dataframe()` for pandas hand-off. The exchange is
   in the public API surface, so a user's xarray-based workflow composes with AMGeO directly.

*Considered and deliberately excluded (audit trail):*
- **Tier A generic stack** — `numpy`, `pandas`, `matplotlib`, `scipy`, `requests`, `tqdm`. `pandas` and
  `matplotlib` deserve explicit mention because they *are* visible in the official notebook
  (`ds.to_dataframe()`; the `polar2dial` matplotlib helper) — and are still excluded, because a dataframe
  conversion and a plotting library are equally true of most of the ecosystem and would be equally at home
  in a web app or a finance model. They carry no information about AMGeO.
- **`h5py` / HDF5 the library** — the interchange is the **format** (Fields 18/19), and the format-level
  consumer that matters is Kamodo, already listed.
- **`jupyter`** — the container ships JupyterLab and the public documentation is a notebook, but Jupyter is
  the delivery vehicle, not a peer tool AMGeO exchanges data with. Represented instead by Field 4's
  `Servers and Environments: Software or Environment Container`.
- **Blanket ecosystem claims** — none made. AMGeO is not a PyHC package (verified: it appears in none of
  the three PyHC registries; the only `amgeo` occurrence is as a keyword in **Kamodo's** entry, which is
  itself the evidence for entry 1), so no PyHC-membership argument was available or used.
- **SuperDARN / SuperMAG / AMPERE tooling** (e.g. pydarn, davitpy) — AMGeO consumes those projects' **data
  products** via web services, not their software. That relationship is represented in Fields 17, 31 and
  32; no evidence of software-level interoperation exists.

### 31. Related Instruments (OPTIONAL)
All entries resolved by SPASE resolution-ladder **rule 1 (exactly one matching row)** against the live
`InstrumentObservatory` vocabulary (re-fetched 2026-07-29: 7,648 rows; 4,513 type=1, 3,135 type=2;
**0 non-SPASE rows — guard passes**). Names copied **verbatim** from the matched rows.

1. **Instrument Name:** `SuperDARN Radars`
   **Instrument Identifier:** `https://spase-metadata.org/SMWG/Instrument/SuperDARN/Radars`
   *Designed-to-support evidence:* AMGeO ingests SuperDARN plasma-drift measurements as a primary
   assimilation input and is built specifically around the SuperDARN **grid2** data product ("The AMGeO
   software is designed to use the SuperDARN grid2 data product", /about FAQ Q2). Runtime log:
   `AMGeO.observations.superdarn` reading `SD_grid_20130106N.h5` and creating a "SuperDARN electricfield"
   observation object from 215,413 grid records.

2. **Instrument Name:** `SuperMAG Magnetometers`
   **Instrument Identifier:** `https://spase-metadata.org/SMWG/Instrument/SuperMAG/Magnetometers`
   *Designed-to-support evidence:* AMGeO ingests SuperMAG ground magnetometer data and targets the
   SuperMAG **Baseline Subtracted** product specifically ("The AMGeO software is designed to use the
   SuperMAG Baseline Subtracted data product", /about FAQ Q3). Runtime log:
   `AMGeO.observations.supermag` reading the SuperMAG station table and ASCII data file, with a
   SuperMAG-specific header-format validation.

3. **Instrument Name:** `Birkeland Currents from IRIDIUM Data`
   **Instrument Identifier:** `https://spase-metadata.org/SMWG/Instrument/IRIDIUM/Magnetometer`
   *Designed-to-support evidence:* AMGeO assimilates "magnetic field measurements made by Iridium
   spacecraft" to produce field-aligned current maps, with priors from "empirical orthogonal function
   analysis to Iridium data" (homepage, Iridium Assimilation section). Kamodo's AMGeO reader confirms the
   corresponding output variables `jfac` (Field Aligned Current), `mpot` (Magnetic Potential) and
   `sdB_ph`/`sdB_th` ("Spacecraft-Observed Magnetic Perturbations").

*Resolution notes and traps handled:*
- **IUGONET per-station rows excluded, and this is not an ambiguity.** The vocabulary also contains
  individual SuperDARN station radars (`SuperDARN Hokkaido East HF radar`, `SENSU SuperDARN Syowa East HF
  radar.`, `SuperDARN King Salmon HF radar`, …). AMGeO consumes the **network-level grid2 product**, not
  per-station data, so the single SMWG network row is the correct match. Per the per-entity collision rule,
  one entity (the SuperDARN network) has exactly one candidate row — ladder rule 1, not rule 3.
- **The `.html` AMPERE row is deliberately not emitted here.** A `type=1` row exists named
  `Active Magnetosphere and Planetary Electrodynamics Response Experiment (AMPERE)` whose identifier is
  `.../SMWG/Observatory/AMPERE.html` — a duplicate of the observatory record. Per the ladder, `.html` and
  bare identifiers are the same resource and the bare one is preferred, so AMPERE is represented **only**
  by the `type=2` observatory row in Field 32.

*Considered and deliberately excluded (audit trail):*
- **DMSP** (all 71 candidate rows) — **future work, not current support.** /about FAQ Q1: "**In future
  AMGeO software releases**, AMGeO will be able to use other types of data, such as particle precipitation
  and FUV image data from DMSP satellites." Not designed-to-support today.
- **OMNI** (`SMWG/Instrument/OMNI`, `SMWG/Observatory/OMNI`) — AMGeO does ingest OMNI solar-wind/IMF data,
  but OMNI is a **multi-mission merged data product/service**, which Field 31/32 guidance routes to Data
  Sources. It is recorded there as `OMNIWeb` (Field 17), which is the field the vocabulary provides for it.
- **Individual Iridium satellites** (`SMWG/Observatory/IRIDIUM_1_70`) — a satellite-range row with no
  supporting evidence that AMGeO targets specific spacecraft; AMGeO uses AMPERE's constellation-derived
  products.

### 32. Related Observatories (OPTIONAL)
All entries resolved by ladder **rule 1 (exactly one matching row)**, `type=2`. Names verbatim.

1. **Observatory Name:** `SuperDARN`
   **Observatory Identifier:** `https://spase-metadata.org/SMWG/Observatory/SuperDARN`
   *Evidence:* as Field 31 entry 1 — AMGeO is purpose-built around the SuperDARN network's grid2 product,
   with automated access to the SuperDARN data service.

2. **Observatory Name:** `SuperMAG`
   **Observatory Identifier:** `https://spase-metadata.org/SMWG/Observatory/SuperMAG`
   *Evidence:* as Field 31 entry 2 — AMGeO requires an individual SuperMAG account and targets the
   SuperMAG Baseline Subtracted product.

3. **Observatory Name:** `Active Magnetosphere and Planetary Electrodynamics Response Experiment`
   **Observatory Identifier:** `https://spase-metadata.org/SMWG/Observatory/AMPERE`
   *Evidence:* AMGeO "enable[s] automated access to the Iridium magnetometer data distributed from
   AMPERE" and requires an individual AMPERE account (/rules Third-Party Data Policy). Name copied
   verbatim from the SMWG row (the long form, not the acronym).

4. **Observatory Name:** `IRIDIUM`
   **Observatory Identifier:** `https://spase-metadata.org/SMWG/Observatory/IRIDIUM`
   Included. This was considered potentially redundant with AMPERE, but was settled
   by reading the upstream SPASE records rather than reasoning about it. The Field 31 instrument row
   `Birkeland Currents from IRIDIUM Data` declares its own parent observatory explicitly:

   ```
   ResourceID:    spase://SMWG/Instrument/IRIDIUM/Magnetometer
   ObservatoryID: spase://SMWG/Observatory/IRIDIUM
   ```

   So in SPASE's own model the instrument belongs to Observatory **IRIDIUM**, not to AMPERE — the two are
   separate observatory records, and `SMWG/Observatory/AMPERE` does not stand in for the platform.
   Omitting `IRIDIUM` would leave a Field 31 instrument whose observatory is unrepresented. AMPERE is the
   science program that derives and distributes the products; IRIDIUM is the platform carrying the sensors.
   Both are genuinely designed-to-support, and listing both mirrors the upstream structure.
   Corroborating evidence: "magnetic field measurements made by Iridium spacecraft" (homepage); CCMC:
   "data products derived from the Iridium Communications constellation". Ladder resolution is clean
   (exactly one matching row).

*Considered and deliberately excluded:* DMSP (future work — see Field 31); OMNI (multi-mission data
service → Field 17); `IRIDIUM_1_70` (satellite-range row, no supporting evidence).

> **Field 31/32 safeguard:** every entry above carries a verified
> `https://spase-metadata.org/` identifier. No name is emitted without one — a bare name would either bind
> to an arbitrary same-name row or create a new identifierless row in HSSI.

### 33. Logo (OPTIONAL)
`https://amgeo.colorado.edu/static/img/amgeoicon.png`

*Source:* the official AMGeO website's own logo asset, verified as a publicly accessible PNG served
from the project's permanent institutional home. The
same mark appears embedded in AMGeO's own generated map figures, confirming it is the software's logo.

*Alternative considered:* `static/AMGeOLogo.svg` in the public `AMGeO-API-Release` repository — a raw
GitHub URL is less durable than the project's own site, so the site asset is preferred.

---

## Summary

| Category | Fields |
|---|---|
| **Unchanged from live HSSI** | 3 (Code Repository), 7 (Software Name), 9 (Concise Description), 6 (Authors — retained exactly) |
| **Enriched existing values** | 4 (Software Functionality: 1 → 16), 5 (Related Region: 1 → 4), 8 (Description — framing added while preserving technical content and correcting four source-text defects), 12 (Version: empty → 3.0.8 / 2025-07-31) |
| **Newly populated (were empty)** | 10, 11, 13, 14, 15, 16, 17, 18, 19, 20, 21, 23, 24, 25, 26, 27, 29, 30, 31, 32, 33 |
| **Intentionally empty, with documented reason** | 2 (no resolvable software DOI — the project's cited DOI is dead), 22 (Related Phenomena — closed vocabulary lacks AMGeO's phenomena; no storm evidence), 28 (Related Datasets — no published AMGeO dataset DOI exists) |

## Durable catalog notes

- The previous blank Award relationship was detached from AMGeO but its shared blank Award row was not
  deleted. It continues to serve unrelated entries and must not be removed without a catalog-wide
  reference audit.
- Field 15's License URI is recorded here but not stored in HSSI. The selected `Other` license is a
  shared controlled-vocabulary row; adding AMGeO's URI to that row would incorrectly affect every entry
  using it.
- Controlled values in Fields 4, 5, 13, 15, 17–23, 31, and 32 were confirmed against the live HSSI
  vocabulary with exact spelling, punctuation, case, and SPASE identifiers.
