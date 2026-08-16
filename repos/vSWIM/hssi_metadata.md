# HSSI Metadata Extraction Results

**HSSI Software ID:** a562afcf-b6f7-4ddd-be72-d450f8de9fc0
**Repository:** https://github.com/abbyazari/vSWIM
**Source Revision:** 3a0a3a8cf74814c3ff820e86a52864bf64481411
**Extraction Date:** 2026-08-15
**Validation Date:** 2026-08-15
**Validation Status:** PASS

---

**Scope note.** vSWIM is a small, single-purpose repository: one Python module (`src/vSWIM.py`), one
IDL helper (`src/IDLTools/readvSWIM.pro`), two tutorial notebooks, and a published hourly CSV data
product under `data/`. It is both a *model* (source code that generates predictions) and a
*published data product* (the hourly prediction files). Several fields below turn on that dual
nature, and on the fact that the repository ships no packaging metadata (no `setup.py`,
`pyproject.toml`, `codemeta.json`, or `CITATION.cff`) and no CI configuration. Where the repository
is silent, the reference publication — Azari et al. (2024), *JGR: Machine Learning and Computation*,
which is CC-BY and whose Acknowledgements and Open Research sections are authoritative for funding
and data provenance — is the next source of record.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Not part of the software's descriptive metadata; supplied at submission time.*

---

### 2. Persistent Identifier (RECOMMENDED)

**https://doi.org/10.5281/zenodo.11106970**

Carried over from the existing HSSI record and reconfirmed. This is the Zenodo **concept** DOI —
the identifier that resolves to all versions — which is what this field asks for. Zenodo's own
record confirms the role: record 11106970 is the `conceptrecid`, and `conceptdoi` on both version
records points back to it. The README's DOI badge links to the same concept DOI.

The two **version** DOIs are deliberately not used here: `10.5281/zenodo.11106971` (v0.0.0) and
`10.5281/zenodo.13252274` (v0.0.1). The latter belongs in Field 12 (Version PID), where it is now
recorded.

Caution for future refreshes: DataCite returns the concept DOI `10.5281/zenodo.11106970` with
`"version": "v0.0.1"` and the title `vSWIM: v0.0.1`, because Zenodo populates the concept record
from the latest version. That does not make it a version DOI, and it should not be moved to
Field 12.

---

### 3. Code Repository (MANDATORY)

**https://github.com/abbyazari/vSWIM**

Carried over from the existing HSSI record and reconfirmed against the local clone's `origin`
remote, the Zenodo record's `code:codeRepository` custom field, the Zenodo `isVersionOf` related
identifier, and the paper's Open Research section, which names this URL as where the model,
representative dataset, usage examples, and usage guidelines may be found. The repository is public
and not archived.

---

### 4. Software Functionality (MANDATORY)

**Values (12):**

- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: ML/AI
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: ML/AI
- Models and Simulations: Mission-Specific

The stored HSSI value was the single top-level term `Models and Simulations`. That term is correct
and is retained; the other eleven values are additions, each grounded in specific code below. No
previously stored value is removed.

Every subcategory listed has its parent top-level category listed alongside it, as the taxonomy
requires, and each value is written in the canonical `Parent: Child` spelling with a space after the
colon.

**Evidence per value:**

- **Models and Simulations** — vSWIM is a predictive model. `runvSWIM()` in `src/vSWIM.py` is the
  entry point that produces estimates of ten solar wind parameters over a user-specified time range
  and cadence.
- **Models and Simulations: ML/AI** — the model is Gaussian process regression implemented with
  GPflow on TensorFlow: `gpflow.kernels.RationalQuadratic`, `gpflow.models.GPR`,
  `gpflow.optimizers.Scipy().minimize(model.training_loss, model.trainable_variables)`, and
  `model.predict_y`. `gpflow==2.9.1` and `tf_keras==2.16.0` are pinned in `requirements.txt`, and
  the module's own comment labels the import block "import GPU enabled GP packages."
- **Models and Simulations: Data Guided** — the model has no free-running mode. `getMAVENData()`
  downloads the MAVEN merged upstream driver record and every prediction is conditioned on it;
  `runvSWIM()` raises a `ValueError` if the requested window falls outside the span of available
  MAVEN observations. Predictions are driven entirely by observations.
- **Models and Simulations: Empirical** — the model contains no physics. It is a statistical
  regression: outputs are normalised with `StandardScaler`, time is rescaled with `MinMaxScaler`,
  a kernel is fitted per parameter per 1,000-point subset, and predictions are un-normalised. The
  taxonomy's "Empirical" category is for statistical/empirical models, which is exactly what this
  is.
- **Models and Simulations: Mission-Specific** — the model is constructed from, and valid only
  over, one mission's dataset. Its input is MAVEN's merged SWIA+MAG driver file, its optional orbit
  labelling uses MAVEN SPICE ephemeris kernels, and the README states that broader coverage awaits
  "future iterations ... that include solar wind observations from other missions to Mars." The
  paper's title and abstract frame the work as a virtual monitor derived from the MAVEN mission.
- **Data Processing and Analysis** — parent of the five processing subcategories below.
- **Data Processing and Analysis: Data Access and Retrieval** — two user-callable functions fetch
  data from remote archives. `getMAVENData()` reads
  `https://homepage.physics.uiowa.edu/~jhalekas/drivers/drivers_merge_l2_hires.txt` directly over
  HTTPS; `getOrbitalData()` scrapes the NAIF SPICE directory
  `https://naif.jpl.nasa.gov/pub/naif/MAVEN/kernels/spk/` with `requests`, matches
  `maven_orb_rec_*.orb` filenames with a regex, and downloads each. The tutorial additionally reads
  the published hourly CSVs straight from `raw.githubusercontent.com` into a DataFrame.
- **Data Processing and Analysis: ML/AI** — the same GPflow/TensorFlow machinery, viewed as a
  method applied to MAVEN observations to produce a derived science data product, together with the
  scikit-learn preprocessing (`StandardScaler`, `MinMaxScaler`) that supports it. The taxonomy
  intentionally repeats subcategory names under more than one parent; listing ML/AI under both
  parents reflects that the software both *is* an ML model and *applies* ML to observational data.
- **Data Processing and Analysis: Time Series Analysis** — the entire data model is time-ordered.
  The module converts timestamps to UNIX seconds, resamples onto a user-specified cadence with
  `np.arange(startDate, stopDate, dt.timedelta(seconds=cadence))`, and computes a `gap` column via
  `scipy.spatial.distance.cdist` giving the time in days from each predicted point to the nearest
  real measurement.
- **Data Processing and Analysis: Analysis** — derived physical quantities are computed rather than
  merely passed through: field and velocity magnitudes are formed as
  `sqrt(b_x^2 + b_y^2 + b_z^2)` and `sqrt(v_x^2 + v_y^2 + v_z^2)`, and the published assessment is
  built on normalised residuals and R-squared statistics against a held-out test set.
- **Data Processing and Analysis: Processing** — pipeline-style transformation steps: partitioning
  the MAVEN record into fixed 1,000-point subsets with a `SubsetIndex` column, per-subset
  normalisation and inverse transformation, and assembly of the results DataFrame.
- **Data Processing and Analysis: File Format Conversion** — `src/IDLTools/readvSWIM.pro` provides
  `vswim_csv_to_sav`, a shipped, user-facing routine that reads a vSWIM CSV and writes an IDL
  `.sav` file. The README points IDL users to it explicitly. This is format conversion offered as a
  capability, not an internal step.

**Considered and not selected** (recorded so a future refresh does not re-propose them):

- **Models and Simulations: Forecasting** — rejected, and this is the most likely mis-selection for
  this package. The README and the HSSI description both use the word "predictions," and the paper
  is cited elsewhere in the literature alongside solar wind *forecasting* work. But vSWIM does not
  forecast: it interpolates between existing measurements within the historical MAVEN record.
  `runvSWIM()` raises `ValueError` if either endpoint of the requested window lies outside the span
  of the downloaded MAVEN data, so it cannot be run into the future at all. The paper's own framing
  is a "virtual monitor" and a "proxy," and it benchmarks against piecewise linear interpolation
  rather than against forecast models.
- **Data Visualization** and **Data Visualization: Line Plots** — rejected. `src/vSWIM.py` imports
  `matplotlib.pyplot as plt`, but that import is never used anywhere in the module, and the package
  exposes no plotting function. Plots appear only inside the two tutorial notebooks, where the user
  calls `plt.fill_between`, `plt.plot`, `plt.scatter`, and `plt.hist` directly. That is the reader
  writing matplotlib, not vSWIM providing visualization. Selecting this would be true of nearly any
  package that ships an example notebook, so it carries no information about vSWIM.
- **Coordinate Transforms** and **Coordinate Transforms: Planetary** — rejected. The README states
  that "all vector quantities are measured in Mars Solar Orbital (MSO) coordinates," which makes
  this an easy false positive. The data arrive in MSO from the upstream driver file and leave in
  MSO; there is no frame conversion code anywhere in the module or the IDL helper.
- **Mission-related** (and its subcategories) — rejected. vSWIM consumes MAVEN science data but is
  not part of MAVEN's ground system, operations, or processing pipeline. It is a scientist-authored
  derived product hosted on a personal GitHub account. Per the taxonomy's own distinction, software
  that *reads* a mission's data belongs under Data Processing and Analysis; only software that is
  *part of* the mission's ground system is Mission-related.
- **Data Processing and Analysis: Plasma Moments** — rejected, despite the modelled quantities
  (density, bulk velocity, proton temperature) being plasma moments. vSWIM never computes moments
  from distribution functions; it consumes moments already derived in the SWIA Level 2 product.
- **Data Processing and Analysis: Data Assimilation** — rejected. Gaussian process regression
  conditions a statistical prior on observations, which superficially resembles assimilation, but
  there is no physical forecast model being corrected, which is what this category denotes.
- **Data Processing and Analysis: Data Reduction** — rejected. The hourly product is a *resampled
  regression estimate* on a regular grid, not an averaging, binning, or downsampling of the source
  measurements. The README does suggest that downsampling the hourly files to coarser cadence is a
  reasonable use, but that is advice to the user, not a function the software implements.
- **Models and Simulations: Physics-Based**, **First Principles**, **MHD**, **Theory**,
  **Forward-Fitting**, **Instrument Response**, **Observatory/Instrument Models** — rejected; the
  model is purely statistical. In particular, the GPflow hyperparameter optimisation is
  marginal-likelihood maximisation, not forward-fitting of a physical forward model.
- **Servers and Environments** (and its subcategories) — rejected. No server, container,
  orchestration, or HPC component. Google Colab is offered as a convenience runtime for the
  tutorials, which is not a capability of the software.

---

### 5. Related Region (MANDATORY)

**Values (4):**

- Interplanetary Space
- Mars Magnetosphere
- Planetary Magnetospheres
- Solar Wind

`Planetary Magnetospheres` was the stored HSSI value and is retained. The other three are additions.
The `Region` vocabulary is flat — there are no parent/child paths to construct, so each value
stands alone.

- **Solar Wind** — the quantity the software models *is* the solar wind: IMF components and
  magnitude, bulk velocity components and magnitude, proton temperature, and proton density, all
  upstream of Mars.
- **Mars Magnetosphere** — the specific region the product exists to serve. The paper motivates the
  work by the difficulty of "assessing the solar wind's role in causing lower altitude observations
  such as auroral dynamics or atmospheric loss" at Mars, and the README's suggested use cases are
  "large (multi-year) studies of Mars' space environment, ionosphere, and atmosphere." This is the
  most specific applicable row and is preferred over the broad term.
- **Interplanetary Space** — the modelled plasma is the pristine, undisturbed solar wind sampled
  outside the Martian bow shock, i.e. the interplanetary medium at Mars' heliocentric distance. The
  README and paper both name general heliospheric trends as an intended use.
- **Planetary Magnetospheres** — retained from the existing record. It remains defensible: the
  paper frames the limitation being addressed as one affecting "solar wind-magnetosphere coupling
  throughout the solar system," and the repository's own GitHub topics include `planetary-science`.
  It is broader than `Mars Magnetosphere`, but the guidance to prefer specific regions is a
  preference, not an instruction to remove a correct broader term, and dropping a submitted value
  is not warranted here.

**Considered and not selected:** there is no `Mars Ionosphere`, `Mars Atmosphere`, or
`Mars Magnetosheath` row in the vocabulary, so the README's ionosphere and atmosphere use cases
cannot be represented more precisely than by `Mars Magnetosphere`. The Earth-specific rows
(`Earth Ionosphere`, `Earth Magnetosphere`, and the rest) do not apply — vSWIM has no Earth
component. `Heliosheath` does not apply; Mars is deep inside the heliosphere.

---

### 6. Authors (MANDATORY)

Fourteen authors, unchanged in membership from the existing HSSI record. The union was taken across
the stored HSSI record, the Zenodo v0.0.1 software record, the Zenodo v0.0.0 record, the paper's
author list via Crossref and arXiv, `Citation.bib`, and the repository's git history. Nobody is
added and nobody is dropped.

Two things are worth stating plainly, because they explain the two-source structure:

- The **paper** has twelve authors. The **software record** has fourteen: it adds **K. Gwen Hanley**
  and **Nils Smit-Anseeuw**, both of whom contributed to the software but not the paper. Hanley
  wrote the IDL conversion routine (`src/IDLTools/readvSWIM.pro` carries "Written BY K. G. HANLEY on
  February 5th, 2023", and the README credits "helpful function created by K. G. Hanley").
  Smit-Anseeuw contributed the command-line interface and usability fixes (pull requests #1 and #2,
  eleven commits in git history as `Nils <nilssmit@umich.edu>`). Both belong in the software's
  author list, and the maintainer put them there on Zenodo.
- **Every author except Smit-Anseeuw carries an affiliation**, sourced from the Zenodo creator list
  and the paper and each bound to a matching ROR. Those sources are sound and their values stand,
  with one refinement: Marquette and Mitchell are placed at the Space Sciences Laboratory rather than
  the parent Berkeley campus, for the reasons given after the per-author notes. Smit-Anseeuw's
  affiliation is empty and stays empty, also explained below.

| # | Given name | Family name | ORCID | Affiliation | Affiliation ROR |
|---|---|---|---|---|---|
| 1 | Ellianna | Abrahams | https://orcid.org/0000-0002-9879-1183 | University of California, Berkeley | https://ror.org/01an7q238 |
| 2 | Abby | Azari | **https://orcid.org/0000-0002-8665-5459** | University of British Columbia | https://ror.org/03rmrcq20 |
| 3 | John | Biersteker | https://orcid.org/0000-0001-5243-241X | Massachusetts Institute of Technology | https://ror.org/042nb2s44 |
| 4 | Charles | Bowers | https://orcid.org/0000-0002-6336-7526 | Dublin Institute for Advanced Studies | https://ror.org/051sx6d27 |
| 5 | Shannon | Curry | https://orcid.org/0000-0002-7463-9419 | University of Colorado Boulder | https://ror.org/02ttsq026 |
| 6 | Jasper | Halekas | https://orcid.org/0000-0001-5258-6128 | University of Iowa | https://ror.org/036jqmy94 |
| 7 | K. Gwen | Hanley | https://orcid.org/0000-0001-6250-7665 | University of California, Berkeley | https://ror.org/01an7q238 |
| 8 | Caitriona | Jackman | https://orcid.org/0000-0003-0635-7361 | Dublin Institute for Advanced Studies | https://ror.org/051sx6d27 |
| 9 | Melissa | Marquette | https://orcid.org/0000-0003-4288-9875 | Space Sciences Laboratory, University of California, Berkeley | https://ror.org/048400679 |
| 10 | David | Mitchell | **https://orcid.org/0000-0001-9154-7236** | Space Sciences Laboratory, University of California, Berkeley | https://ror.org/048400679 |
| 11 | Fernando | Pérez | https://orcid.org/0000-0002-1725-9815 | University of California, Berkeley | https://ror.org/01an7q238 |
| 12 | Matthew | Rutala | https://orcid.org/0000-0002-1837-4057 | Dublin Institute for Advanced Studies | https://ror.org/051sx6d27 |
| 13 | Facundo | Sapienza | https://orcid.org/0000-0003-4252-7161 | University of California, Berkeley | https://ror.org/01an7q238 |
| 14 | Nils | Smit-Anseeuw | **https://orcid.org/0000-0002-6848-7308** | *Not found* | — |

Bold entries mark the three ORCIDs that were corrected or filled; each is justified individually
below. Marquette and Mitchell are recorded at the Space Sciences Laboratory rather than the parent
campus, for the reasons given after the per-author notes.

**Abby Azari — ORCID newly filled: https://orcid.org/0000-0002-8665-5459.**
The stored record had an empty identifier for the lead developer and first author. Three independent
sources agree on this ORCID: Crossref's publisher-deposited author list for
`10.1029/2024JH000155` carries it for "A. R. Azari"; the Zenodo record for v0.0.0 carries it for
"Azari, A. R." with affiliation University of British Columbia; and the ORCID registry itself
returns the name "A. R. Azari" for that identifier. The identity chain to this repository is direct:
the paper's corresponding author is "A. R. Azari, azari@eoas.ubc.ca", the arXiv submitter is
"Abigail Azari", the repository owner is `abbyazari`, and `LICENSE.md` is copyrighted "A. R. Azari".
Note that the Zenodo record for **v0.0.1** — the version HSSI's metadata was drawn from — renames
this creator to "Abby Azari" and drops the ORCID, which is why the field was empty. The v0.0.1
record also mis-parses the name, storing "Abby Azari" as the *family name* with no given name.
HSSI's stored split (given "Abby", family "Azari") is correct and is kept.

**David Mitchell — ORCID corrected from https://orcid.org/0000-0002-2274-0603 to
https://orcid.org/0000-0001-9154-7236.**
The stored value came from the Zenodo v0.0.1 record, which is wrong. Crossref's
publisher-deposited author list for the paper gives `0000-0001-9154-7236` for "D. L. Mitchell" with
the affiliation "Space Sciences Laboratory University of California, Berkeley", and the Zenodo
v0.0.0 record gives the same identifier. Checking both ORCID records settles it: `0000-0001-9154-7236`
belongs to a David Mitchell employed as a Research Physicist at the Space Sciences Laboratory,
University of California Berkeley since November 1996, whose listed work is "First observations of
atmospheric sputtering at Mars". That is the D. L. Mitchell who does MAVEN-era Mars science at
Berkeley, matching the affiliation the paper prints for him. The previously stored
`0000-0002-2274-0603` is a different, essentially empty ORCID record for a person also named "David
Mitchell", with no employment history and no works. Someone editing the v0.0.1 Zenodo deposit
appears to have picked the wrong "David Mitchell" from an autocomplete.

**Do not restore `0000-0002-2274-0603`.** It is still what the Zenodo v0.0.1 record carries, so any
refresh that re-reads that deposit will encounter it again and may read the divergence as drift in
the wrong direction. The paper is the authority here, not the software deposit.

**Charles Bowers — https://orcid.org/0000-0002-6336-7526 confirmed, not changed.**
Worth recording because the same v0.0.0/v0.0.1 divergence exists here but resolves the *opposite*
way, so the pattern above must not be applied mechanically. Zenodo v0.0.0 gives
`0000-0002-3102-9979`; v0.0.1 and Crossref both give `0000-0002-6336-7526`. The latter is correct:
that record is "Charles F. Bowers", Postdoctoral Researcher in the School of Cosmic Physics at the
Dublin Institute for Advanced Studies, and its works list includes "A Virtual Solar Wind Monitor at
Mars With Uncertainty Quantification Using Gaussian Processes" itself. `0000-0002-3102-9979` is an
empty record for a different Charles Bowers. The stored HSSI value was already right.

**Nils Smit-Anseeuw — ORCID newly filled: https://orcid.org/0000-0002-6848-7308.**
The stored record had an empty identifier, and no source connected to this repository supplies one:
Zenodo v0.0.1 lists him with no ORCID and no affiliation, he is not on the paper, and the repository
contains no contributor metadata file. The identifier was therefore established by identity
research rather than by transcription, and the evidence is strong enough to record:

- An exact surname search of the ORCID registry (`family-name:"Smit-Anseeuw"`) returns a single
  record, `0000-0002-6848-7308`. The surname is rare and the given name matches exactly.
- OpenAlex ties that same ORCID to an author "Nils Smit-Anseeuw" with an affiliation history of
  **University of Michigan (2016-2021)** and **University of British Columbia (2013)**, and lists
  University of Michigan as the last known institution.
- The University of Michigan affiliation matches the commit email in this repository's git history
  exactly: his eleven commits are authored as `Nils <nilssmit@umich.edu>`.
- His works include "Walking With Confidence: Safety Regulation for Full Order Biped Models"
  (*IEEE Robotics and Automation Letters*, 2019), a University of Michigan robotics paper. An
  engineering background is consistent with his actual contribution to vSWIM, which was software
  engineering — the argparse command-line interface and usability fixes in pull requests #1 and #2 —
  rather than science.

The ORCID record itself is empty (no employments, works, or biography listed), so OpenAlex, not
ORCID, is what supplies the corroborating affiliation and publication history. That is worth
recording, because an agent consulting only ORCID's own `/works` and `/employments` endpoints will
find nothing and may wrongly conclude the identification is unsupported.

**Residual caveat, recorded deliberately:** no source names the vSWIM repository alongside this
ORCID, so the identification rests on inference from a unique name match plus corroborating
affiliation history — well-supported, but inference rather than an authoritative assertion. It is
recorded as the value because the corroboration is strong and consistent from several directions.
Should contrary evidence ever surface — a different Nils Smit-Anseeuw with a heliophysics or
Michigan-adjacent record, or an ORCID stated by the maintainer — that evidence should win over this
reasoning.

**Affiliation sourcing and judgement calls.**
The stored affiliations trace to the Zenodo v0.0.1 creator records cross-checked against the paper's
affiliation list, and that sourcing is sound; they are retained. Where the two sources differ, the
peer-reviewed paper is preferred, because it was copy-edited and the Zenodo deposit was not — which
is what drives the single refinement below.

- **Marquette and Mitchell** are recorded at **Space Sciences Laboratory, University of California,
  Berkeley** (ROR `https://ror.org/048400679`) rather than at the parent campus. The paper places
  both at the Space Sciences Laboratory specifically, and Mitchell's own ORCID employment record
  names "Space Sciences Laboratory" as his department at University of California Berkeley. That ROR
  is UC Berkeley's SSL: its website is `https://www.ssl.berkeley.edu`, and ROR records `University of
  California, Berkeley` (`https://ror.org/01an7q238`) as its parent. Zenodo v0.0.1 lists both simply
  as "University of California, Berkeley", which is true but less precise; the more specific
  organization is preferred because the peer-reviewed paper is the better-edited source and because
  HSSI already holds an organization named exactly "Space Sciences Laboratory, University of
  California, Berkeley" carrying that ROR, so no new organization is implied.

  Both authors are recorded at the Space Sciences Laboratory **alone** — the campus organization is
  deliberately not carried alongside it, so the two authors are treated consistently.

  **Caution for a future refresh.** Attaching an affiliation through the routine metadata-update path
  is additive: it can add an organization to a person but cannot remove one. A later refresh that
  reconciles affiliations by union — taking everything Zenodo, the paper, and the stored record each
  assert — would therefore silently re-attach the University of California, Berkeley campus row to
  these two authors and quietly undo this refinement, with no error to signal it. The SSL-only state
  is intentional. Preserve it, and treat a reappearing campus affiliation on Marquette or Mitchell as
  drift to correct rather than as a value to keep.
- **K. Gwen Hanley** is recorded at **University of California, Berkeley**, following the Zenodo
  v0.0.1 record. She is not on the paper, so there is no peer-reviewed affiliation to prefer. The
  Zenodo v0.0.0 record placed her at "Space Sciences Lab, University of California, Berkeley"; if a
  more precise affiliation is wanted later, `Space Sciences Laboratory, University of California,
  Berkeley` / `https://ror.org/048400679` is the supported alternative.
- **Bowers, Jackman, and Rutala** are recorded as **Dublin Institute for Advanced Studies**. The
  paper gives "Dublin Institute for Advanced Studies, Dunsink Observatory"; Dunsink Observatory is a
  site of DIAS rather than a separately registered organisation, so the institutional name is used
  with the DIAS ROR. Note that ROR's display name capitalises the preposition — "Dublin Institute
  For Advanced Studies" — while the paper, the institution itself, and Bowers' ORCID employment
  record use lower-case "for". The lower-case form is recorded; the ROR is the disambiguator either
  way.
- **Shannon Curry** is recorded at **University of Colorado Boulder** per Zenodo and the paper
  ("University of Colorado, Boulder"). She is the MAVEN Principal Investigator; the affiliation is
  the campus, not LASP, because that is what both sources say.
- **Nils Smit-Anseeuw** has no affiliation recorded, and it stays empty rather than being inferred.
  Zenodo explicitly stores `null` for it; his commit email domain (`umich.edu`)
  and the OpenAlex affiliation history behind his ORCID both point at the University of Michigan, but
  neither states his affiliation *at the time he contributed to vSWIM*, and OpenAlex's affiliation
  years for him end in 2021, three years before these commits. Recorded as *Not found* rather than
  inferred. Note that accepting the ORCID (above) does not license inferring the affiliation from it:
  the identifier identifies the person, not the institution he worked for in 2024.

All ROR identifiers above were resolved through the ROR API and their display names confirmed:
`027ka1x80`/`021nxhr62` are used in Field 25; `01an7q238` University of California, Berkeley;
`048400679` Space Sciences Laboratory; `03rmrcq20` University of British Columbia; `042nb2s44`
Massachusetts Institute of Technology; `051sx6d27` Dublin Institute For Advanced Studies;
`036jqmy94` University of Iowa; `02ttsq026` University of Colorado Boulder.

No author is an organization, so no ROR is used as an *author* identifier here; all fourteen are
people with ORCIDs or blank identifiers.

---

### 7. Software Name (MANDATORY)

**vSWIM**

Carried over from the existing HSSI record, unchanged. It matches the repository name, the README
heading ("vSWIM - A Virtual Solar Wind Monitor for Mars"), the Zenodo record titles ("vSWIM: v0.0.0",
"vSWIM: v0.0.1"), and the module name `src/vSWIM.py`. The lower-case "v" followed by upper-case
"SWIM" is the form used consistently by the authors and is preserved exactly. The expansion
"virtual Solar Wind Monitor" is descriptive text, not the name, and belongs in the description.

---

### 8. Description (MANDATORY)

**Value:**

> vSWIM is a virtual solar wind monitor for Mars: it provides a continuous estimate, with
> uncertainties, of the solar wind upstream of Mars from late 2014 onward. Single-spacecraft
> missions such as MAVEN sample the pristine solar wind only intermittently, because the spacecraft
> spends much of each orbit inside the Martian induced magnetosphere and ionosphere. The resulting
> gaps limit statistical conclusions about the solar wind's role in driving Mars' space environment,
> including auroral dynamics and atmospheric loss. vSWIM fills those gaps by applying Gaussian
> process regression to the merged MAVEN Solar Wind Ion Analyzer (SWIA) and Magnetometer (MAG)
> upstream driver dataset, returning both a mean prediction and an accompanying standard deviation
> for ten solar wind parameters: the interplanetary magnetic field components and magnitude (Bx, By,
> Bz, |B|) in nT, the solar wind velocity components and magnitude (Vx, Vy, Vz, |V|) in km/s, the
> proton temperature (Tp) in eV, and the proton density (np) per cubic centimetre. All vector
> quantities are expressed in Mars Solar Orbital (MSO) coordinates.
>
> The project distributes two things: a ready-to-use hourly cadence prediction product as CSV files,
> intended as an OMNI-like continuous driver series for Mars, and the model source code needed to
> generate predictions at finer cadences. The hourly files can be read straight into a pandas
> DataFrame from the repository without any local installation; running the model directly requires
> GPflow and its TensorFlow and TensorFlow Probability dependencies. The model discretises the MAVEN
> record into subsets of 1,000 points and fits each solar wind parameter separately using a rational
> quadratic covariance kernel and a zero mean function.
>
> Because the model interpolates rather than forecasts, its skill is a function of how far a
> prediction sits from a real measurement. Every row carries a "gap" column giving the time in days
> to the nearest MAVEN observation, and users are expected to filter on it: the authors report an
> R-squared of at least 0.95 within 2 days of a measurement, and predicted uncertainties that are
> unbiased and accurate within 2 days but increasingly underestimated at longer gaps. Far from any
> measurement the model returns the mean of the surrounding data subset. vSWIM is intended for large,
> multi-year statistical studies of the Mars space environment, ionosphere, and atmosphere, and of
> general trends throughout the heliosphere; the authors explicitly do not recommend it for event
> studies, because it does not reproduce short-timescale transients such as coronal mass ejections
> unless MAVEN was itself in the solar wind at the time. Vector components are not guaranteed to add
> in quadrature with the predicted magnitudes. Documentation follows an AI model card format
> covering model description, assessment, suggested use cases, and limitations, and a helper routine
> is included for converting the CSV predictions into IDL .sav files.

**This replaces the stored HSSI description, which was not a description of the software.** The
stored value was Zenodo/GitHub release-notes autofill. After a two-sentence opening lifted from the
README, it continued into changelog material: "-> v0.0.1 is the first version with accepted
publication doi in JGR ML and Computation and Google colab tutorials", a bulleted list of pull
requests, a "What's Changed" section listing PR URLs, a "New Contributors" section, and a "Full
Changelog" compare link. That text is the v0.0.1 GitHub release body, which Zenodo copied into its
record and which HSSI's DOI autofill then copied into this field — byte-for-byte, as a character
comparison against the DOI record's stored description confirms. A release changelog
answers "what changed in this version"; this field must answer "what does this software do, why
would I use it, and what does it assume" — which the stored text did not.

The stored text also carried a copy-paste artifact: three U+00A0 non-breaking spaces, around
"MAVEN" and before "Github." The replacement uses ordinary spaces throughout.

The replacement is grounded in primary sources rather than invented: the opening framing and the
gap-limitation motivation come from the paper's abstract and introduction; the parameter list, units,
MSO coordinate statement, kernel and subset details, installation requirements, R-squared figures,
uncertainty behaviour, suggested use cases, and limitations all come from the README's model-card
sections; the "OMNI-like product" phrasing and the pandas read pattern come from the README's
Contents and Usage Guidelines sections; the `gap` column semantics come from `data/format.md` and
from the `cdist`-based computation in `src/vSWIM.py`.

One correction was made silently relative to the repository: `data/format.md` labels `np` as
"Pressure: $n_p$ in [per cc]". The README labels the same quantity "Density: $n_p$ in [per cc]", and
density is what a per-cubic-centimetre proton quantity is. The description says density.

---

### 9. Concise Description (OPTIONAL)

**Value (159 characters):**

> This repository contains predictions of the solar wind upstream of Mars from late 2014 onwards as calculated with a predictive model and MAVEN spacecraft data.

Retained from the existing HSSI record, with the two U+00A0 non-breaking spaces around "MAVEN"
normalised to ordinary spaces. This is the only change; the wording is unaltered.

The wording is kept deliberately. Although it reached HSSI through Zenodo autofill, it is not
autofill boilerplate — it is the maintainer's own opening sentence from the README, word for word,
and it fits comfortably under the 200-character limit. The README writes "MAVEN" as a markdown link
to the mission page; that link was flattened to plain text somewhere along the Zenodo path, which is
also where the two non-breaking spaces that bracketed it came from. Replacing an author's own summary
with a differently-phrased one would be a stylistic preference, not a correction.

An alternative phrasing that would describe the software rather than "this repository", and would
name Gaussian processes and uncertainty quantification, was considered and **rejected**: it would
read better by some tastes, but the stored sentence contains no factual error, and taste is not
grounds to overwrite an author's own summary.

---

### 10. Publication Date (RECOMMENDED)

**2024-05-02**

**Changed from the stored value of 2024-08-07.** This field is defined as the date of first
publication and is explicitly "used for the initial version of the software." The stored 2024-08-07
is the release date of **v0.0.1**, the *second* version — it arrived via DOI autofill from the
concept DOI, which Zenodo populates from the latest version rather than the first.

The initial version is **v0.0.0**, and three independent records agree on its date: the git tag
`v0.0.0` was created 2024-05-02, the GitHub release `v0.0.0` was published 2024-05-02T22:12:28Z, and
the Zenodo record `10.5281/zenodo.11106971` carries `publication_date` 2024-05-02. Its release note
— "Base release for peer review process in JGR Machine Learning and Computation" — confirms it was
the first published version.

**Considered and not selected:** the repository creation date, 2023-10-17. Making a repository
public is not publication of a software version, and the earliest commits from that date are
placeholder scaffolding (a template `Citation.cff` containing "YOUR_NAME_HERE" and a title of
"vSWUM", plus a file literally named `TEMP`). Also not selected: 2024-07-11, the reference
publication's issue date, which belongs to the paper rather than the software.

The v0.0.1 date of 2024-08-07 is not lost — it is recorded in Field 12 as the Version Date, which is
where it belongs.

---

### 11. Publisher (RECOMMENDED)

- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Carried over from the existing HSSI record, unchanged and confirmed. DataCite reports
`"publisher": "Zenodo"` for both version DOIs and the concept DOI, and the DOI was obtained through
the standard GitHub-Zenodo integration (the README's badge is a `zenodo.org/badge/706391083` release
badge). Per the field guidance, Zenodo — not GitHub — is the correct entry when a Zenodo DOI exists.

A ROR was searched for and none was found: a ROR API query for "Zenodo" returns no matching
organization, since Zenodo is a repository service operated by CERN rather than a separately
registered organization. The field explicitly permits a URL where no ROR exists, and
`https://zenodo.org` is both the stored value and the URL the field's own guidance gives as the
example for exactly this case. Not changed.

---

### 12. Version (RECOMMENDED)

- **Version Number:** `v0.0.1`
- **Version Date:** 2024-08-07
- **Version PID:** https://doi.org/10.5281/zenodo.13252274
- **Version Description:**
  > First version with an accepted publication DOI in JGR: Machine Learning and Computation, and
  > with Google Colab tutorials. Includes updated tutorials on Google Colab; a minor fix for a
  > security vulnerability in the pinned scikit-learn version; minor readability and DOI fixes to
  > the README; and command line arguments plus general usability fixes.

**Version Number** is stored as the bare string `v0.0.1`. HSSI's view layer renders versions as
`<software name> - <version>`, so this record displays as "vSWIM - v0.0.1"; that rendered form is a
display transform and must never be written back as the stored value.

v0.0.1 is confirmed as the latest release from three sources: it is the newest git tag (the
repository carries two tags, `v0.0.0` and `v0.0.1`), it is the newest GitHub release, and it is the
newest Zenodo version record. `main` has moved exactly one commit past the `v0.0.1` tag: the pinned
source revision `3a0a3a8` of 2024-08-14, a README-only edit for which no tag or release was cut.
(The tag itself resolves to `73bb659`, also a README edit, of 2024-08-06.) v0.0.1 therefore remains
the current published version, and the pinned revision introduces no code change relative to it.

**Version Date** is 2024-08-07, agreeing across the GitHub release (`published_at`
2024-08-07T04:16:46Z) and the Zenodo record (`publication_date` 2024-08-07). The underlying git tag
carries a local timestamp of 2024-08-06 22:02 -0600, which is the same instant expressed in
Mountain time; the UTC date 2024-08-07 is used, matching both publication records.

**Version PID** was already stored in HSSI and matches the value above; it is retained unchanged.
`10.5281/zenodo.13252274` is the version-specific DOI for v0.0.1, distinct from the concept DOI in
Field 2. Zenodo's `HasVersion` relations from the concept record list two version DOIs, and DataCite
confirms `13252274` carries `"version": "v0.0.1"` while `11106971` carries `"version": "v0.0.0"`.
The distinction matters and is easy to invert: the concept DOI also reports `"version": "v0.0.1"`,
because Zenodo populates the concept record from the latest version, so DataCite's `version` field
alone does not identify which DOI is the version-specific one.

**Version Description is the one part of this field that changed**, having previously been empty. It
is a lightly copy-edited rendering of the GitHub release
body for v0.0.1. The release body's trailing "What's Changed", "New Contributors", and "Full
Changelog" sections are deliberately omitted: they are per-pull-request attribution links, not a
summary of changes, and it was precisely that material leaking through autofill that corrupted the
Description field (see Field 8).

Note for a future refresh: replacing this field in HSSI orphans the previous `SoftwareVersion` row
rather than updating it. That is known, accepted platform behaviour and is not a reason to avoid
correcting the field.

---

### 13. Programming Language (RECOMMENDED)

**Values (2):**

- IDL
- Python 3.x

Two languages, not three. HSSI previously also carried `Other`, which is not recorded because
nothing in the software justifies it; the reasoning is below so that it is not reintroduced. `Other`
is a valid vocabulary row, so this is a judgement about what vSWIM is written in rather than a
correction of an invalid value.

- **Python 3.x** — confirmed. `src/vSWIM.py` and `src/__init__.py` are Python; the README's
  installation instructions say "install Python (v3.12)"; GitHub reports 14,156 bytes of Python, the
  largest share in the repository.
- **IDL** — confirmed. `src/IDLTools/readvSWIM.pro` is IDL, GitHub reports 1,127 bytes of IDL, and
  the README directs IDL users to it. Although small, it is a distinct user-facing tool in a second
  language, so it is genuinely one of "the most important languages" for this package.
- **`Other`** — not recorded, because no third language justifies it. GitHub's language breakdown for
  this repository is `{"Python": 14156, "IDL": 1127, "TeX": 497}`, and that third entry is where
  `Other` almost certainly originated. The 497 bytes of "TeX" is `Citation.bib`, which is itself
  exactly 497 bytes — an exact match, leaving no room for a second TeX-classified file. GitHub's
  linguist classifies `.bib` as BibTeX and groups it under TeX. A BibTeX citation file is citation
  metadata, not a language the software is implemented in.

  The other candidate considered was the two Jupyter notebooks in `examples/`, whose code cells are
  Python and are therefore already covered by `Python 3.x`; the vocabulary has no "Jupyter Notebook"
  row in any case. `Other` therefore asserted a third implementation language that does not exist,
  and carrying it would misrepresent the software to anyone filtering by language. A future refresh
  that re-reads GitHub's language statistics will meet the same "TeX" entry and should not read it
  as grounds to add `Other` back.

---

### 14. Reference Publication (RECOMMENDED)

**https://doi.org/10.1029/2024JH000155**

Carried over from the existing HSSI record and confirmed. Azari, A. R., Abrahams, E., Sapienza, F.,
Halekas, J., Biersteker, J., Mitchell, D. L., Pérez, F., Marquette, M., Rutala, M. J., Bowers, C. F.,
Jackman, C. M., & Curry, S. M. (2024). "A Virtual Solar Wind Monitor at Mars With Uncertainty
Quantification Using Gaussian Processes." *Journal of Geophysical Research: Machine Learning and
Computation*, 1(3), e2024JH000155. Published 2024-07-11 under CC-BY 4.0.

This is the citation the README instructs users to give ("If you use this product please reference
the published JGR Machine Learning paper"), and it is the sole entry in `Citation.bib`. Zenodo
records the same DOI as an `isDescribedBy` relation.

The arXiv preprint `arXiv:2402.01932` (recorded as `eprint` in `Citation.bib`) is the same work, not
a separate publication, and is deliberately not listed here or in Field 27. It is nonetheless the
practical route to the text: the article is open access under CC BY 4.0, but the publisher's HTML
page rejects automated fetches, so the paper reads as paywalled to anything but a browser. The arXiv
HTML rendering of **v4 (2024-07-14)** is the post-acceptance text and carries the Acknowledgements
and Open Research sections that Fields 25, 26, and 28 rest on. A future agent should go there rather
than concluding the article is inaccessible.

---

### 15. License (RECOMMENDED)

- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

Carried over from the existing HSSI record, confirmed against the repository rather than trusted
from autofill. `LICENSE.md` contains the full BSD 3-Clause License text, "Copyright (c) 2023, A. R.
Azari", with the three standard clauses and the standard disclaimer. GitHub's repository metadata
independently classifies it as `BSD-3-Clause`.

The value string matches the live `License` vocabulary row exactly, including the straight
double-quotes around "New" and "Revised". The URI recorded is the one carried on that vocabulary
row. DataCite reports a different but equivalent URI for the same license,
`https://opensource.org/licenses/BSD-3-Clause`; the SPDX URL from the vocabulary row is preferred
for consistency with the controlled list.

The license applies to the source code. The repository does not state a separate license for the
hourly CSV data products under `data/`, which is a gap in the repository rather than a metadata
question.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values (7):**

- gaussian processes
- interpolation
- machine learning
- mars
- planetary science
- solar wind
- uncertainty quantification

The list above is alphabetical, which does not reflect what changed. Precisely: HSSI already stored
**five** keywords — `gaussian processes`, `machine learning`, `mars`, `planetary science`, and
`solar wind` — and all five are retained unchanged. The **two additions** are `interpolation` and
`uncertainty quantification`. (HSSI stores keywords lower-case and renders them in Title Case, so
the stored identity — not the displayed casing — is what is recorded here.)

The five retained keywords correspond exactly to the repository's own GitHub topics —
`gaussian-processes`, `machine-learning`, `mars`, `planetary-science`, `solar-wind` — differing only
in the hyphen-to-space convention. That is the maintainer's own keyword set and there is no reason
to disturb it.

Two additions, both matched against the live `Keyword` vocabulary before selection:

- **uncertainty quantification** — the single most distinguishing feature of the package and absent
  from the stored set. It is in the paper's title ("...With Uncertainty Quantification Using
  Gaussian Processes") and the README states "One of the main purposes of this model is for
  uncertainty quantification." No matching row exists in the vocabulary yet; Keywords is the one
  open vocabulary in the form, so this will create a new row. Entered lower-case and singular-phrase
  to match the existing row conventions.
- **interpolation** — an existing vocabulary row, and directly evidenced in the software's own text:
  the command-line help in `src/vSWIM.py` describes `--cadence` as "interpolation cadence in
  seconds" and `--params_list` as "solar wind parameters to interpolate". The paper benchmarks the
  model against piecewise linear interpolation. This also usefully signals what the software is
  *not* (a forecast model), reinforcing the Field 4 reasoning.

**Considered and not selected:** `maven` — an existing vocabulary row, but the mission is already
carried by Field 32, and this field is for keywords "not supported by other metadata fields".
`regression` — an existing row, but `gaussian processes` already names the method more precisely.
`planetary magnetospheres` — an existing row, but duplicated by Field 5. Generic terms such as
`heliophysics`, `python`, and `space physics` were rejected as carrying no information specific to
this package.

---

### 17. Data Sources (OPTIONAL)

**Values (2):**

- HTTP/HTTPS Directories
- Observatory/Mission-specific

Newly filled — the field was empty in HSSI. Both strings were confirmed against the live `DataInput`
vocabulary.

- **HTTP/HTTPS Directories** — every input the software retrieves comes over plain HTTPS rather than
  through a heliophysics data service. `getMAVENData()` fetches a single text file from a personal
  university web page (`https://homepage.physics.uiowa.edu/~jhalekas/drivers/drivers_merge_l2_hires.txt`),
  and `getOrbitalData()` requests the NAIF SPICE directory listing at
  `https://naif.jpl.nasa.gov/pub/naif/MAVEN/kernels/spk/`, regex-matches the `.orb` filenames it
  contains, and downloads each one — a literal HTTP directory traversal. The published hourly CSVs
  are likewise read over HTTPS from `raw.githubusercontent.com`.
- **Observatory/Mission-specific** — the data are MAVEN-specific products, not a general
  multi-mission holding. Field 17's guidance requires that when a source is observatory-specific
  this value be selected and the mission named in Field 32, which is done.

**Considered and not selected:** `CDAWeb`, `HAPI`, `OMNIWeb`, `SSCWeb`, `AMDA`, `das2`, `VirES`,
`Madrigal`, `GFZ`, `WDC`, `TAP`, `The Virtual Solar Observatory.` — none of these services is
contacted anywhere in the code. `OMNIWeb` deserves an explicit note, because it is easy to select in
error: the README links to OMNIWeb, but only to explain what an "OMNI-like product" is by analogy.
vSWIM neither reads from nor writes to OMNIWeb. `FTP/FTPS Directories` — the NAIF holdings are also
reachable by FTP, but the code uses `requests` over HTTPS. `S3/Cloud-aware` — no cloud object
storage access. `Other` — unnecessary, since two specific values apply.

The paper's Open Research section also names the MAVEN Planetary Data System archive
(`https://pds-ppi.igpp.ucla.edu/mission/MAVEN`) and the MAVEN Science Data Center
(`https://lasp.colorado.edu/maven/sdc/public/`) as places MAVEN data may be obtained. Neither is
accessed by the code — they are provenance pointers for the source measurements — so neither drives
a value here.

---

### 18. Input File Formats (RECOMMENDED)

**Values (2):**

- ascii
- csv

Newly filled — the field was empty in HSSI.

- **ascii** — the primary model input is a whitespace-delimited plain-text table. `getMAVENData()`
  reads it with `pd.read_csv(mav_file, names=colNames, index_col=False, sep=r'\s+')`; the explicit
  whitespace separator and supplied column names confirm it is headerless ASCII, not CSV. The NAIF
  `.orb` ephemeris files parsed by `getOrbitalData()` are also plain-text tables, split on
  whitespace line by line.
- **csv** — the published hourly prediction files are read back as input in two distinct places:
  the tutorial reads them with `pd.read_csv` from the repository, and the IDL helper
  `vswim_csv_to_sav` takes a vSWIM `.csv` as its input argument via `read_csv(fin, header=header)`.

**Considered and not selected:** `CDF`, `netCDF3/4`, `HDF5`, `FITS`, `JSON`, `Zarr`,
`ISTP-Compliant` — none is read anywhere in the codebase; there are no corresponding libraries in
`requirements.txt`. `IDL.sav` — the IDL helper *writes* `.sav` but never reads one, so it belongs
only in Field 19.

---

### 19. Output File Formats (RECOMMENDED)

**Values (2):**

- csv
- IDL.sav

Newly filled — the field was empty in HSSI.

- **csv** — the model's output path. `runvSWIM(saveModelResults=True)` writes
  `results.to_csv('./results/vSWIM_<start>_<stop>.csv')`, and `getMAVENData(saveMAVENData=True)`
  writes a local copy of the source data as CSV. The repository's published data product is nine
  `YYYY-YYYY_Hourly.csv` files under `data/`, described by `data/format.md`.
- **IDL.sav** — `src/IDLTools/readvSWIM.pro` exists specifically to produce this format:
  `vswim_csv_to_sav` builds a variable list from the CSV header and calls `save, ..., filename=fout`,
  defaulting the output name to the input with the extension replaced by `.sav`.

**Considered and not selected:** the same formats rejected in Field 18, for the same reason — no
writer exists for any of them. `ascii` — although CSV is technically ASCII text, `csv` is the
specific and correct row, and nothing is written as a whitespace-delimited or free-form ASCII table.

---

### 20. Operating System (RECOMMENDED)

**Values (3):**

- Linux
- Mac
- Windows

Newly filled — the field was empty in HSSI. The repository makes no OS claim: there is no CI
configuration (`.github/` contains only two issue templates), no packaging metadata declaring
classifiers, and no installation note mentioning a platform.

The basis for these three is that the software is pure Python with no compiled extensions of its
own, no OS-specific system calls, and no filesystem assumptions beyond `os.mkdir('./results/')`.
Portability is therefore determined by whether the pinned dependency stack installs, and the
binding constraint is TensorFlow (pulled in by `gpflow==2.9.1` and `tf_keras==2.16.0`), which
publishes wheels for Linux, macOS, and Windows. The documented quick-start path — Google Colab, per
both tutorial notebooks and the README's "Option 1 (recommended)" — is a Linux environment, which
gives Linux direct evidence.

**Considered and not selected:** `Operating System Independent`. It is tempting for a pure-Python
package, but it overstates the case here: the dependency stack is delivered as platform-specific
binary wheels rather than being platform-agnostic, and the IDL helper additionally requires a
licensed IDL installation. Naming the three platforms where the stack is known to install is more
informative and more defensible. `Solaris`, `MobilePlatform`, `Other` — no evidence, and TensorFlow
does not support them.

---

### 21. CPU Architecture (RECOMMENDED)

**Values (3):**

- x86-64
- Apple Silicon arm64
- GPU

Newly filled — the field was empty in HSSI.

- **GPU** — directly evidenced in the repository, not inferred. The import block in `src/vSWIM.py`
  is headed by the comment "#import GPU enabled GP packages", and the second tutorial notebook tells
  the reader "if running on Google colab you can switch to GPU computing which will be faster". The
  GPflow/TensorFlow backend executes the Gaussian process fits on a GPU when one is present.
- **x86-64** and **Apple Silicon arm64** — the same wheel-availability reasoning as Field 20: the
  TensorFlow generation pinned here publishes CPU wheels for x86-64 (Linux, macOS, Windows) and for
  arm64 macOS. These two are recorded together deliberately, since selecting `Mac` in Field 20 on
  wheel-availability grounds and then omitting arm64 would be inconsistent — current Macs are arm64.

**Considered and not selected:** `Linux aarch64 or arm64` — plausible, but TensorFlow's Linux arm64
support is less uniformly packaged than its macOS arm64 support, and the repository offers no
evidence either way; omitted rather than guessed. `HPC or HEC` — the model is run interactively or
from a short CLI invocation, with no batch, MPI, or scheduler integration. `CPU Independent` —
contradicted by the binary dependency stack. `Sun (SPARC)`, `ppc64le`, `Other` — no evidence.

---

### 22. Related Phenomena (OPTIONAL)

**Value (1):**

- Solar Wind

Carried over from the existing HSSI record, unchanged and confirmed. The solar wind is the
phenomenon the software exists to characterise; the value matches the live `Phenomena` row exactly.

**Considered and not selected — and specifically rejected on the repository's own evidence:**
`Coronal Mass Ejections`. CMEs are mentioned in the README, which is exactly why this needs
recording: the mention is a **statement of a limitation**, not of support. The Limitations section
reads "This proxy does not capture short scale dynamic events (e.g. CMEs) or outliers unless the
proxy itself is being used when MAVEN had solar wind data." Selecting CMEs here would assert the
opposite of what the authors say. `Geomagnetic Storms` — Mars has no global intrinsic magnetic field
and no geomagnetic storm analogue is modelled. `Solar Corona`, `Coronal Heating`, `Solar Flares`,
`X-ray emission` — outside the software's scope entirely; vSWIM begins at the solar wind as measured
at Mars and models nothing solar-atmospheric.

---

### 23. Development Status (RECOMMENDED)

**Inactive**

Newly filled — the field was empty in HSSI. Value confirmed against the live `RepoStatus`
vocabulary; the bare term is recorded, without the repostatus.org description.

`Inactive` is defined as "reached stable, usable state but no longer actively developed; support
provided as time allows," and both halves fit:

- *Stable and usable* — v0.0.1 is a tagged, DOI-minted release accompanying a peer-reviewed paper,
  with a complete usage guide, two working tutorials, and a published data product.
- *No longer actively developed* — the newest commit on `main` is dated 2024-08-14 and the newest
  release 2024-08-07, roughly two years behind the extraction date in the header above. No commits,
  tags, or releases have followed, and open issues remain unaddressed. The most telling signal is a promise the
  repository has not kept: `data/format.md` states the hourly files "will continue to be updated as
  the mission progresses", yet the newest data file remains `2023-2024_Hourly.csv` and has not been
  extended, even though MAVEN continued operating. Similarly, the README's stated plan for "future
  iterations ... that include solar wind observations from other missions to Mars" has not
  materialised.

**Considered and not selected:** `Active` — ruled out by two years of no development. `Unsupported`
— too strong; the authors have not announced cessation or sought a new maintainer, and the README
still expresses forward intent. `Abandoned` and `WIP` — both require the absence of a stable release,
which is contradicted by v0.0.1 and the published paper. `Moved` — the repository has not relocated;
it remains the URL cited by the paper. `Suspended` — would require an explicit statement of a
temporary pause, which does not exist.

This value is time-sensitive and should be re-checked on any future refresh: a single new release
would move it back to `Active`.

---

### 24. Documentation (RECOMMENDED)

**https://github.com/abbyazari/vSWIM/blob/main/README.md**

Newly filled — the field was empty in HSSI. There is no separate documentation site: the repository
has GitHub Pages disabled, its homepage field is empty, there is no `docs/` directory, and no
Read the Docs or Sphinx configuration exists.

The README *is* the documentation, and an unusually complete one. It is explicitly structured as an
AI model card ("It follows a rough standard AI model reporting in model card format") with numbered
sections for Model Description, Installation, Assessment, Suggested Use Cases and Tips, and
Limitations, and it contains the installation instructions this field asks for (three options:
Colab, local virtual environment with `pip install -r requirements.txt`, and expert self-managed
environment). Supplementary documentation lives in `data/format.md`, which describes the hourly file
layout, and in the two tutorial notebooks under `examples/`.

**Considered and not selected:** the bare repository URL `https://github.com/abbyazari/vSWIM`, which
the field explicitly permits when documentation and access are the same link. The `blob/main/README.md`
form is preferred because it points at the documentation itself rather than duplicating Field 3, and
it remains stable as long as the default branch is `main`. Also considered and rejected:
`https://github.com/abbyazari/vSWIM#guidelines`, the in-page anchor for the usage guide — accurate
today but dependent on a heading slug that any README edit could break.

---

### 25. Funder (OPTIONAL)

**Values (3):**

| Organization | Funder Identifier (ROR) |
|---|---|
| National Aeronautics and Space Administration | https://ror.org/027ka1x80 |
| U.S. National Science Foundation | https://ror.org/021nxhr62 |
| University of British Columbia | https://ror.org/03rmrcq20 |

Newly filled — the field was empty in HSSI. Organization names are given in full, without acronyms,
per the field guidance; each ROR was resolved and its record confirmed.

The authoritative source is the reference publication's **Acknowledgements** section, cross-checked
against the README's own "Funding" section. The two agree on the scope recorded here, and the README
— written by the maintainer specifically about this project — is what settles the boundary between
funding *of vSWIM* and funding *of its authors* (see the exclusions below).

- **National Aeronautics and Space Administration** — supports the work through two awards
  (Field 26): NNH10CC04C, the MAVEN mission contract, and 80NSSC21K1370, the AI/ML Use Case Program
  award. The Acknowledgements read: "This work was supported by the National Aeronautics and Space
  Administration (NASA) grant NNH10CC04C to the University of Colorado and by subcontract to Space
  Sciences Laboratory, University of California, Berkeley. The MAVEN project is supported by NASA
  through the Mars Exploration Program. We also acknowledge support from NASA's AI / ML Use Case
  Program, grant 80NSSC21K1370."
- **U.S. National Science Foundation** — "This work was supported by the NSF Earth Cube Program
  under awards 1928406, 1928374." The paper's Acknowledgements and Crossref's funder block both use
  the un-prefixed form "National Science Foundation"; ROR's current display name for
  `https://ror.org/021nxhr62` is the U.S.-prefixed form, and that prefixed form is also the name
  HSSI stores for this funder. The prefixed name is recorded here as the value so that the dossier
  matches what the catalogue actually holds and a later refresh does not read the difference as
  drift. The ROR is the identity in every case; only the label differs.

  The organization record behind this ROR is shared across the catalogue, and its name cannot be
  changed through the metadata-update path: an identifier match reuses the existing record and
  leaves a non-blank name untouched. A rename proposed from this entry would silently fail to
  apply, so a future refresh should not attempt one. Correcting the label, if it is ever wanted, is
  a database-level change that affects every entry citing this funder.
- **University of British Columbia** — "ARA is supported by the Data Science Fellowship at the
  University of British Columbia through the Data Science Institute's Postdoctoral Matching Fund."
  This is included where the other personal fellowships are not, because it supports the **lead
  developer's** work on this software and because the maintainer's own README Funding section lists
  it as project support.

**Considered and not selected.** The paper's Acknowledgements also name four sources of personal
support for individual co-authors, none of which appears in the repository's Funding section:
the **National Science Foundation Graduate Research Fellowship** (Grant No. DGE 1752814) and the
**Two Sigma PhD Fellowship**, both supporting E. Abrahams; **Science Foundation Ireland** Grant
18/FRL/6199, supporting M. J. Rutala; and the **Irish Research Council** Laureate Grant SOLMEX,
supporting C. F. Bowers. These fund the people, not the development of vSWIM, and the maintainer
excluded them when stating what funded the project. (The NSF GRFP is a further reason not to change
the NSF entry: its presence in the acknowledgements is personal support, while the EarthCube awards
are the project support.) They are recorded here so a later refresh does not read the
Acknowledgements afresh and add them without noticing the distinction.

Crossref's funder block for the paper lists only NASA (twice) and NSF (twice), omitting UBC, Science
Foundation Ireland, the Irish Research Council, Two Sigma, and the GRFP entirely. It is therefore
incomplete and should not be used alone; the Acknowledgements text is the better source, exactly as
the field guidance warns.

---

### 26. Award Title (OPTIONAL)

**Values (5):**

| Award Title | Award Number |
|---|---|
| MAVEN mission support through the NASA Mars Exploration Program | NNH10CC04C |
| NASA AI/ML Use Case Program | 80NSSC21K1370 |
| EarthCube Data Capabilities--Jupyter Meets the Earth: Enabling Discovery in Geoscience through Interactive Computing at Scale | 1928406 |
| EarthCube Data Capabilities--Jupyter Meets the Earth: Enabling Discovery in Geoscience through Interactive Computing at Scale | 1928374 |
| Data Science Institute Postdoctoral Matching Fund | — |

Newly filled — the field was empty in HSSI. All titles are within HSSI's 128-character limit for an
award name (the longest is 125), and all award numbers are short. Sourced from the paper's
Acknowledgements, with titles confirmed or refined against award databases.

**The two NSF awards** have an officially published title, retrieved from the NSF award database:
"Collaborative Research: EarthCube Data Capabilities--Jupyter Meets the Earth: Enabling Discovery in
Geoscience through Interactive Computing at Scale". That string is 149 characters and would exceed
HSSI's 128-character award-name limit, so the administrative prefix "Collaborative Research: " is
elided, leaving 125 characters of substantive title. The elision is recorded here so the value is
not mistaken for a transcription error. Both awards share the title because they are the two
institutional halves of one collaborative project: 1928406 is held by the University of
California-Berkeley with **Fernando Perez** — a vSWIM co-author — as Principal Investigator, and
1928374 is held by the University Corporation for Atmospheric Research. Both ran 2019-09-01 to
2023-08-31 under the EarthCube program, which corroborates the Acknowledgements' attribution of
computational support.

**The two NASA awards have no published formal title.** The recorded titles are concise descriptive
labels grounded in primary sources rather than transcriptions, and the award numbers are the
authoritative identifiers:

- **NNH10CC04C** — the federal award record confirms the recipient as the Regents of the University
  of Colorado and describes it as NASA Headquarters' management of the Mars Exploration Program,
  which selected the MAVEN project as a Mars Scout mission with Bruce Jakosky of the University of
  Colorado LASP as Principal Investigator. The recorded title reflects that, and matches the
  Acknowledgements' phrasing ("grant NNH10CC04C to the University of Colorado ... The MAVEN project
  is supported by NASA through the Mars Exploration Program").
- **80NSSC21K1370** — the federal award record confirms the recipient as the Regents of the
  University of California and its description opens by noting that the MAVEN mission "has collected
  the most detailed and extensive measurements of Mars' magnetic field to date" amid "an ongoing
  surge of planetary data which is now transforming the field", running 2021-07-15 to 2023-11-14.
  The award number matches the Acknowledgements exactly, so the identification rests on an
  identifier match rather than on interpretation; the recorded title uses the program name the
  authors themselves use.

**The UBC fellowship has no award number.** The Acknowledgements identify it only as "the Data
Science Fellowship at the University of British Columbia through the Data Science Institute's
Postdoctoral Matching Fund". The recorded title names the fund; no number is invented.

**Considered and not selected:** award numbers DGE 1752814 (NSF Graduate Research Fellowship), 18/FRL/6199
(Science Foundation Ireland), and the Irish Research Council Laureate Grant SOLMEX, plus the
unnumbered Two Sigma PhD Fellowship — all excluded for the reason given in Field 25: they are
personal support for individual co-authors rather than funding of this software, and the repository's
own Funding statement omits them.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Values (3):**

- https://doi.org/10.1029/2025GL117836 — Global Occurrence of Kelvin-Helmholtz Vortices at Mars.
  *Geophysical Research Letters* (2025).
- https://doi.org/10.1029/2025JA033913 — IMF Control of Electron Aurora Across Mars' Crustal
  Magnetic Fields: Insights Into Electron Sources. *Journal of Geophysical Research: Space Physics*
  (2025).
- https://doi.org/10.1029/2025GL114745 — Deriving IMF Properties From Mars Express Heavy Pickup Ion
  Measurements. *Geophysical Research Letters* (2025).

Newly filled — the field was empty in HSSI. This field is for publications that describe, cite, or
use the software, other than the reference publication. Because the developers have not published a
list of preferred citing works, the selection is restricted to papers whose citation context shows
**substantive use or evaluation** of vSWIM, rather than a passing mention:

- **10.1029/2025GL117836** uses the product directly: "Since MAVEN does not cross into the solar
  wind for three of the six analyzed orbits ... we used machine learning-derived estimates of solar
  wind parameters from Azari et al. (2024) for these events." This is precisely the gap-filling use
  case vSWIM was built for.
- **10.1029/2025JA033913** also uses it directly, combining it with other proxies "to derive
  reliable estimates of the IMF clock angle for 87% of EMUS measured pixels".
- **10.1029/2025GL114745** — Dong, Y., Ramstad, R., Davis, M. W., Holmström, M., Brain, D. A.,
  Espley, J. R., & Curry, S. M. (2025), *Geophysical Research Letters*, 52(11), e2025GL114745,
  published 2025-06-04 under CC BY-NC 4.0 — evaluates vSWIM quantitatively as a benchmark against
  its own Mars Express heavy-pickup-ion
  proxy. Its Section 4 reports vSWIM's IMF magnitude skill as an **R² of 0.98 within ≤2 days and 0.79
  within ≤10 days** of a true measurement (the metric matters: these are R² values, not error rates),
  and compares its own derived B⊥ (R² ≈ 0.5) to vSWIM's R² at up to ~28 days from true data, judging
  the two comparable in that regime. It concludes that its B⊥ proxy "would be more suitable for the
  time >1 month from true IMF data, especially the long time period prior to the MAVEN mission" —
  which is a useful published delimitation of where vSWIM's skill holds and where it does not.
  The same paper's introduction cites vSWIM among the established MAVEN-based IMF proxies, as the
  Gaussian-process-regression approach. Published assessment of a model's performance is valuable
  context for a prospective user, and these figures are confirmed against the publisher's full text.
  One qualification on calling it independent: its last author, Shannon M. Curry, is also a vSWIM
  co-author, so the assessment is not wholly arm's-length — though the comparison is unfavourable to
  vSWIM beyond ~1 month, which is not the direction a conflicted assessment would lean.

  Access note for a future refresh: this article is openly licensed and its full text is readable,
  but the publisher's site rejects automated fetches. Do not record the figures as unverifiable on
  the strength of a failed fetch — use a browser.

**Considered and not selected** — three further citing works whose contexts show background or
methodological name-checks rather than use of the software:

- 10.1126/sciadv.aed9072 (*Science Advances*, 2026, Kelvin-Helmholtz-driven atmospheric ion escape) —
  the citation sits in a general remark that assuming steady solar wind "introduces notable
  uncertainties"; no use of vSWIM output is evident.
- 10.1029/2025SW004859 (*Space Weather*, 2026, post-processing probabilistic solar wind forecasts) —
  cites vSWIM as one example among several of approaches to probabilistic solar wind estimation
  ("Common approaches include Gaussian processes (Azari et al., 2024)"). Methodological background.
- 10.1029/2025JE008934 (*JGR: Planets*, 2025, plasma depletion events in the Mars ionosphere) — the
  available citation contexts concern IMF direction binning and do not evidence use of vSWIM.

Also **not** listed: the arXiv preprint `arXiv:2402.01932`, which is the same work as the reference
publication rather than a distinct related publication (see Field 14); and the MAVEN instrument and
dataset papers (Halekas et al. 2015, 2017; Connerney et al. 2015), which describe vSWIM's *input
data* rather than vSWIM, and are recorded in Field 28 where they belong.

This list will grow. A future refresh should re-query the citation graph and apply the same
substantive-use test rather than adding every citing paper.

---

### 28. Related Datasets (OPTIONAL)

**Values (3):**

- https://doi.org/10.1002/2016JA023167 — Halekas, J. S., Ruhunusiri, S., Harada, Y., Collinson, G.,
  Mitchell, D. L., Mazelle, C., McFadden, J. P., Connerney, J. E. P., Espley, J. R., Eparvier, F.,
  Luhmann, J. G., & Jakosky, B. M. (2017). Structure, dynamics, and seasonal variability of the
  Mars-solar wind interaction: MAVEN Solar Wind Ion Analyzer in-flight performance and science
  results. *Journal of Geophysical Research: Space Physics*, 122(1), 547-578.
- https://doi.org/10.1007/s11214-013-0029-z — Halekas, J. S., Taylor, E. R., Dalton, G., Johnson, G.,
  Curtis, D. W., McFadden, J. P., Mitchell, D. L., Lin, R. P., & Jakosky, B. M. (2015). The Solar
  Wind Ion Analyzer for MAVEN. *Space Science Reviews*, 195(1), 125-151.
- https://doi.org/10.1007/s11214-015-0169-4 — Connerney, J. E. P., Espley, J., Lawton, P., Murphy,
  S., Odom, J., Oliversen, R., & Sheppard, D. (2015). The MAVEN Magnetic Field Investigation.
  *Space Science Reviews*, 195(1), 257-291.

Newly filled — the field was empty in HSSI. The field asks for the datasets the software supports
functionality for, and specifies that "at minimum, the DOI should be the publication that described
the dataset" — which is what these three are.

These are not incidental references. The README's "Data sources" subsection names all three, gives
full BibTeX for each, and instructs users to cite them: "Please additionally see relevant citations
for the current source datasets under the model description." `src/vSWIM.py` repeats the instruction
in its file header ("if using the original MAVEN generated data see ... for original data citations
including but not limited to: Halekas et al., 2017, Halekas et al., 2015, Connerney et al., 2015")
and again in the docstring of `getMAVENData()`.

- **Halekas et al. (2017)** describes the merged upstream driver dataset that is vSWIM's actual
  input — the file `drivers_merge_l2_hires.txt` that `getMAVENData()` downloads. It is the most
  directly relevant of the three.
- **Halekas et al. (2015)** is the SWIA instrument paper, describing the source of the ion moments
  (density, velocity, temperature) in that merged product.
- **Connerney et al. (2015)** is the MAG instrument paper, describing the source of the magnetic
  field components.

**Considered and not selected:** the MAVEN Planetary Data System archive landing page
(`https://pds-ppi.igpp.ucla.edu/mission/MAVEN`) and the MAVEN Science Data Center
(`https://lasp.colorado.edu/maven/sdc/public/`), both named in the paper's Open Research section.
Each is a multi-dataset archive entry point rather than a dataset, and neither is accessed by the
code; the Halekas driver file, not the PDS archive, is what the software actually reads. The driver
file's own landing page (`https://homepage.physics.uiowa.edu/~jhalekas/drivers.html`) has no DOI and
is a personal web page, so the Halekas et al. (2017) DOI is used to represent it, as the field
instructs.

vSWIM's own published hourly prediction files are not listed here: they are the software's *output*,
distributed within this same repository and covered by the concept DOI in Field 2, not a separate
related dataset.

---

### 29. Related Software (OPTIONAL)

**Not found.**

This is a considered conclusion rather than an unexamined blank. The relevance test for this field
is whether an entry would be *distinguishing* — a similar-purpose tool, a predecessor, a fork
parent, a companion package, or a domain-specific dependency characteristic of this software. The
candidates were evaluated as follows:

- **GPflow, TensorFlow, TensorFlow Probability** — the defining technical dependencies, and the
  strongest candidates. Rejected nonetheless: Gaussian process regression libraries and general
  deep-learning frameworks are generic modelling infrastructure. Applying the field's own test — a
  GP library would be equally at home in a finance model or a biology pipeline — they are not
  heliophysics or science-domain peers, so listing them says nothing specific about vSWIM.
- **scikit-learn, pandas, numpy, scipy, matplotlib, requests, regex, ipykernel** — the generic
  scientific-Python and tooling stack, excluded by rule. Being a dependency is not a relationship
  worth recording.
- **OMNI / OMNIWeb** — the README invokes it as an analogy ("Use this if you need an OMNI-like
  product") and links to it. Rejected: OMNIWeb is a data service at NASA/GSFC, not a software
  package, and vSWIM neither reads from it nor derives from it.
- **The operational solar wind prediction system of Wang et al. (2023)**, cited in the paper as
  prior work predicting the upstream solar wind at Mars, is genuinely similar in purpose. Rejected
  because it is a publication (`10.1029/2022SW003281`) rather than released software: there is no
  code DOI or public repository to point at, and this field's guidance directs publication DOIs to
  Field 27 instead. Recorded so a future agent does not spend effort re-deriving the same dead end —
  if that system is ever released as citable software, it would be a legitimate entry here.
- **The bundled IDL helper** (`src/IDLTools/readvSWIM.pro`) is part of vSWIM itself, not separate
  software.

No predecessor project, fork parent, or companion package exists: the repository's history begins
with an initial commit in October 2023 and is not a fork.

---

### 30. Interoperable Software (OPTIONAL)

**Not found.**

The bar for this field is a *demonstrated exchange* with another high-level heliophysics or science
tool — a shared or converted data model, an adapter API, a plugin relationship, a companion package,
or a cross-language bridge to a named domain tool. Nothing in vSWIM meets it.

The one candidate worth recording, because it looks like a cross-language bridge and is not, is the
**IDL conversion routine** `src/IDLTools/readvSWIM.pro`. It converts vSWIM's CSV output into a
generic IDL `.sav` file containing plain variables. That is a file-format conversion into a
language's native save format — already captured by Field 4's `File Format Conversion` and by
Field 19's `IDL.sav` — and not interoperation with any named domain package such as SPEDAS. No IDL
heliophysics library is referenced, required, or targeted.

Everything rejected under Field 29 is rejected here for the same reasons and more strictly, since
dependency presence never establishes interoperability. Two justifications were specifically
avoided: that the package is "part of the standard scientific Python ecosystem", and any appeal to
ecosystem membership — neither demonstrates interoperation with any particular package. Note that
vSWIM is not a PyHC package in any case (see Field 33 note on registry checks), so even that weak
argument is unavailable.

The pandas DataFrame return type of `runvSWIM()` was considered as a possible interchange mechanism
and rejected: returning a DataFrame is generic infrastructure, true of a large share of the
ecosystem, not an exchange with a peer science tool.

---

### 31. Related Instruments (OPTIONAL)

**Values (2):**

| Instrument Name | Instrument Identifier (SPASE) |
|---|---|
| MAVEN Solar Wind Ion Analyzer, SWIA, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/SWIA |
| MAVEN Magnetometer, MAG, Instrument | https://spase-metadata.org/SMWG/Instrument/MAVEN/MAG |

Newly filled — the field was empty in HSSI. Both names are copied exactly as the controlled
vocabulary stores them, including the trailing ", Instrument" and the embedded acronym, and both
identifiers were confirmed to be `https://spase-metadata.org/` SPASE identifiers on rows of type
"instrument".

**Relevance.** These two instruments are what vSWIM is built from. The README's "Data sources"
subsection states that "the dataset(s) used in the current iteration of this model are from a
combined SWIA and MAG (MAVEN instruments) data source", citing the SWIA instrument paper (Halekas et
al. 2015) and the MAG instrument paper (Connerney et al. 2015). The code matches: `getMAVENData()`
parses the merged driver file into exactly the SWIA ion moments (`np_SW`, `nalpha_SW`, `v_SW`,
`v_x_SW`, `v_y_SW`, `v_z_SW`, `tp_SW`) and the MAG field components (`b_x_SW`, `b_y_SW`, `b_z_SW`),
and every predicted parameter is derived from those columns. Someone working with MAVEN SWIA or MAG
upstream data is exactly the person who would want this software.

**Resolution.** Each instrument matched two vocabulary rows — one under the `SMWG` authority and one
under `CNES/Instrument/CDPP-AMDA` — describing the same physical instrument. That is a single entity
with duplicate rows rather than a genuine ambiguity, so the SMWG row is taken as the canonical
choice in each case. The rejected duplicates are
`https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MAVEN/SWIA` ("Solar Wind Ion Analyzer") and
`https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/MAVEN/MAG` ("Fluxgate magnetometer"). Neither
selected identifier has an `.html` variant in the vocabulary, so no normalisation was needed.

**Considered and not selected:**

- **MAVEN Spacecraft Ephemeris Instrument** (`https://spase-metadata.org/SMWG/Instrument/MAVEN/Ephemeris`)
  — the closest call. `getOrbitalData()` genuinely downloads and parses MAVEN orbit ephemeris files
  from NAIF SPICE, and the resulting orbit number is a documented output column (`orb` in
  `data/format.md`). It was excluded because the relationship fails both relevance sanity checks:
  the capability is optional and off by default (`getOrb=False`), it labels rows rather than
  supporting ephemeris data as such, and a user searching for MAVEN ephemeris tooling would not be
  well served by vSWIM. Recorded because the evidence is real and a future agent may reach a
  different judgement.
- **The other MAVEN instruments in the vocabulary** — IUVS, LPW, LPW/EUV, NGIMS, SEP, SWEA, STATIC.
  None is read, referenced, or supported anywhere in the repository.

---

### 32. Related Observatories (OPTIONAL)

**Value (1):**

| Observatory Name | Observatory Identifier (SPASE) |
|---|---|
| Mars Atmosphere and Volatile EvolutioN | https://spase-metadata.org/SMWG/Observatory/MAVEN |

**This field was already correct in HSSI and requires no change.** Both the name and the SPASE
identifier above are what the record already stores, bound to the canonical SMWG observatory row.
The name matches that row exactly, including its unusual internal capitalisation, "EvolutioN".

**An inference trap worth recording, because this field is unusually easy to misdiagnose.** Read
through HSSI's read-oriented view of a software record, the stored value looks like a bare name with
no identifier — which would be a real defect, since an identifier-less observatory entry is exactly
the failure mode the SPASE-only rule exists to prevent. It is not one here. That view does not render
observatory identifiers at all; it returns observatory associations as plain name strings, so a
correctly-bound row and an unbound one are indistinguishable through it. **An absent identifier in
that view is not evidence that the stored row lacks one.** Confirming a binding means resolving the
association against the instrument/observatory vocabulary itself. A future refresh should do that
before concluding Field 31 or 32 needs repair, and should not propose re-binding a row already
bound.

**Relevance.** MAVEN is the mission whose data the software exists to process. Beyond the SWIA and
MAG measurements themselves, the model consumes MAVEN orbital ephemeris, is bounded by the MAVEN
mission timeline (predictions begin in late 2014 and `runvSWIM()` refuses dates before
2014-11-12 12:00), and the paper's title frames the work as a virtual monitor built from the MAVEN
mission. Field 17 is marked `Observatory/Mission-specific` in step with this listing, as that field
requires.

**Resolution.** Two vocabulary rows describe MAVEN: the SMWG row above, and
`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/MAVEN` ("Mars Atmosphere and Volatile
Evolution Mission"). One entity, two rows — a duplicate rather than a genuine ambiguity — so the
SMWG row is preferred as the canonical choice — which is also the row the stored record is already
bound to, independently corroborating it.

**Considered and not selected:** Mars Express, referenced only in one of the citing papers listed
under Field 27 (which derives IMF properties from Mars Express pickup ions), never by vSWIM itself.
No other mission is supported; the README's note that future iterations may "include solar wind
observations from other missions to Mars" describes an intention, not a current capability, and
prospective support is explicitly outside this field's scope.

---

### 33. Logo (OPTIONAL)

**Not found.**

The repository contains no logo or project image. The only images referenced in the README are
status and service badges — the Zenodo DOI badge and two Google Colab "Open in Colab" badges — which
are third-party service graphics, not a logo for this software. There is no `logo` field in the
Zenodo record, no image asset anywhere in the repository tree, and no project website that might
host one.

vSWIM is also absent from all three PyHC registry files (core, community, and unevaluated), which
were read in full and searched for the package name, the repository URL, the owner account, and the
descriptive phrase "virtual solar wind monitor". PyHC is often a source of curated logo and
documentation URLs, so its absence is worth recording here: it explains why no logo is available
from that route, and it means the PyHC-curated values that supplement other records are unavailable
for this one.
