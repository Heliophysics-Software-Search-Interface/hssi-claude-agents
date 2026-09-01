# HSSI Metadata Extraction Results

**HSSI Software ID:** 52e4975a-0d6d-4bb0-91a3-862f8e113091
**Repository:** https://github.com/SWMFsoftware/SWMF
**Source Revision:** 0aaf3a0a65f45742f1ab42836bb64d3254c3e0ff
**Extraction Date:** 2026-08-13
**Validation Date:** 2026-08-15
**Validation Status:** PASS

---

## Scope note — read this before assessing the evidence

`SWMFsoftware/SWMF` is the **framework** repository. Its fifteen component directories (`CZ`, `EE`,
`GM`, `IE`, `IH`, `IM`, `OH`, `PC`, `PS`, `PT`, `PW`, `RB`, `SC`, `SP`, `UA`) hold no physics: each
carries a `CMP` configuration file and an `Empty` stub version, and four of them — `SC`, `IH`, `OH`
and `EE` — additionally carry a `BATSRUS` directory holding that component's SWMF-side makefiles, two
of which (`IH/BATSRUS/srcInterface/IH_wrapper.f90` and `EE/BATSRUS/srcInterface/EE_wrapper.f90`) also
hold the wrapper source. `SC/BATSRUS` and `OH/BATSRUS` carry makefiles alone at this revision.
The models those wrappers front, and the two mandatory libraries (`share`, `util`), live in
**separate repositories in the same GitHub organization** and are pulled in at install time.
`Config.pl` derives the organization URL from this repository's `remote.origin.url` and clones
`share` directly, because it needs `share/Scripts/Config.pl` before it can configure anything and
`share/Scripts/gitclone` before it can fetch anything else; `Config.pl -install` then uses `gitclone`
for `util` and for each selected model. The user manual's description of the distribution accordingly
lists `share` and `util` as top-level SWMF directories, and `doc/index.html` links the IDL
visualization manual at `../share/IDL/doc/idl.pdf`.

Consequences for this dossier:

- Evidence drawn from `share/`, `util/`, `GM/BATSRUS` and the other component repositories is
  **first-party SWMF evidence**, not third-party. Where a value rests on such a repository rather
  than on the framework tree at the pinned revision, the source note says so explicitly.
- Language, file-format and functionality claims that would be unsupportable from the 535 tracked
  files of the framework tree alone are supported by the user manual (`doc/Tex/`), by the shipped
  standard-test parameter files (`Param/`) and reference outputs (`output/`), and by the component
  repositories.
- The HSSI record describes **SWMF the product**, which is what the manual, the reference
  publications and the University of Michigan distribution page all describe.
- **Provenance of the record.** As originally submitted it carried values for eight fields only:
  software name, description, code repository, publication date, programming language, authors,
  software functionality and related region. Name, code repository and publication date were correct
  and are retained; description and programming language were wrong and are corrected here; software
  functionality and related region were severely incomplete and are expanded here; and the author
  entries were right in substance but wrong in form, six of them stored as bare GitHub logins, which
  Field 6 records in full. Every other field in this dossier is derived from the sources its own note
  names, and where a value replaced an incorrect one the previous value and the reason are recorded
  with it.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source note:* HSSI does not expose the submitter of an existing record, so this field is a
placeholder and carries no evidentiary claim about the software.

### 2. Persistent Identifier (RECOMMENDED)
Not found

*Source note:* SWMF has no first-party concept DOI. The evidence for that conclusion, so a future
agent does not repeat the search:

- The repository contains no `CITATION.cff`, no `codemeta.json`, no `.zenodo.json` and no DOI badge;
  `README.md` carries no citation section.
- A DataCite query for software titled "Space Weather Modeling Framework" returns forks and
  application deposits (a SPECTRUM fork, BATSRUS run archives, `swmfpy`) but no SWMF concept DOI.
- **Considered and rejected: `https://doi.org/10.5281/zenodo.10552538`** (concept
  `https://doi.org/10.5281/zenodo.10552537`), deposited 2024-01-22, titled exactly "Space Weather
  Modeling Framework", resource type Model, sole creator "University of Michigan–Ann Arbor". It is a
  third-party archival snapshot, not an authoritative identifier: its description reads "The Space
  Weather Modeling Framework (SWMF). Downloaded from https://github.com/MSTEM-QUDA/SWMF" — the
  phrasing of someone archiving code they did not publish; it carries a single `SWMF-master.zip`
  file, no licence and no version; it points at the **MSTEM-QUDA** distribution rather than at
  Field 3's repository; and the MSTEM-QUDA organization has since been emptied, its description now
  reading "Now SWMF is only available at (http://github.com/SWMFsoftware)." Adopting this DOI would
  bind the HSSI record to a retired redistribution channel.
- The University of Michigan SWMF download page cites papers, not a software DOI, and directs users
  to `github.com/SWMFsoftware`.

The related DOIs that *do* belong to SWMF are publications and are recorded in Fields 14 and 27.

### 3. Code Repository (MANDATORY)
https://github.com/SWMFsoftware/SWMF

*Source note:* Unchanged from the existing HSSI record and confirmed correct. This is the
authoritative public home: the University of Michigan CLaSP "SWMF Downloadable software" page states
"The SWMF is open source" linking to `https://github.com/SWMFsoftware`, and approved registered users
"will be added to the user or developer team on github.com/SWMFsoftware". `Config.pl` derives the
organization URL from this repository's `remote.origin.url` and fetches `share`, `util` and every
selected model from it, so the whole distribution is reachable from here.

Rejected alternative: `https://github.com/MSTEM-QUDA/SWMF`, the former non-commercial open-source
subset. Upstream has retired it and redirects users to `SWMFsoftware`.

### 4. Software Functionality (MANDATORY)

**Coordinate Transforms**
- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Magnetospheric
- Coordinate Transforms: Planetary
- Coordinate Transforms: Solar

**Data Processing and Analysis**
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis

**Data Visualization**
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: 3D Graphics
- Data Visualization: Line Plots
- Data Visualization: Movies

**Models and Simulations**
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing
- Models and Simulations: First Principles
- Models and Simulations: Forecasting
- Models and Simulations: Instrument Response
- Models and Simulations: MHD
- Models and Simulations: Observatory/Instrument Models
- Models and Simulations: Physics-Based

**Servers and Environments**
- Servers and Environments
- Servers and Environments: High Performance Computing

*Source note:* The value this record previously carried was the single top-level category `Models and Simulations`.
That is correct but radically incomplete: it describes neither the coupling framework, the
post-processing and visualization toolchain, the observation-comparison tooling, nor the
parallel/GPU execution model. Every value above is confirmed against the live `FunctionCategory`
vocabulary in its canonical `Parent: Child` spelling, and every subcategory listed is accompanied by
its parent.

Evidence, category by category:

- **Coordinate Transforms** — `CON/Library/src/CON_physics.f90` publicly exports `get_axes`,
  `transform_matrix` ("return transformation matrix between two systems"), `get_planet`,
  `get_planet_field` and `map_planet_field`. Component coordinate systems are first-class: each
  component declares its system and the couplers transform between them
  (`CON/Coupler/src/CON_bline.f90` carries `TypeCoordBl`, `TypeCoordMh` and a `BlMh_DD(3,3)`
  transformation matrix). *Heliospheric* — the `#ROTATEHGR`, `#ROTATEHGI` and `#HGRALIGNMENTTIME`
  commands in `PARAM.XML` and the HGI/HGR/HGC frames used across SC/IH/OH. *Solar* — heliographic
  and Carrington frames; the shipped magnetogram harmonic files are Carrington maps and
  `TypeCoord = HGR` is the default for line-of-sight spectral plots. *Magnetospheric* — GSE, GSM,
  SMG, GEO and MAG appear in the couplers and in the `#COORD` header of the shipped trajectory and
  magnetometer-station input files; `share/IDL/General/geopack.pro` provides the corresponding
  transforms on the analysis side. *Planetary* — `#PLANET` supplies rotation axis, magnetic axis and
  dipole geometry for Mercury through Pluto plus Moon, Io, Europa, Ganymede, Titan, Enceladus and
  four comets — Halley, Borrelly, Churyumov-Gerasimenko and Hale-Bopp. The three periodic ones are
  each selectable under either their name or their comet number (`COMET1P`, `COMET19P`, `COMET67P`),
  which is why the option list carries seven comet strings for four bodies. `#ORBIT` sets orbital
  elements in HGI.
  - *Considered and not selected:* `Coordinate Transforms: Ionospheric`. The IE component works in
    magnetic coordinates, but no AACGM/apex/MLT transform is exposed as a user-facing capability.
  - *Considered and not selected:* `Coordinate Transforms: Mission-Specific`. The manual notes SPICE
    as an optional library "to determine position and orientation of various objects", and the
    line-of-sight synthesis uses observer position and field of view, but no spacecraft attitude or
    instrument-pointing frame transform is offered to users at the framework level.
- **Data Processing and Analysis** — the SWMF ships a post-processing and analysis chain, not only a
  solver. `PostProc.pl` collects per-processor raw output, and `make PIDL` builds `PostIDL.exe`,
  which converts raw output into single IDL-format files (*File Format Conversion*, *Processing*).
  The manual states the processed files "are much smaller than the raw output file, so
  post-processing during the run can limit the amount of disk space used", and `PostProc.pl -g`
  gzips large ASCII files (*Data Reduction*). *2D Slices* — the shipped tests write `x=0`, `y=0`,
  `z=0` and `cut` plot files extracted from the 3-D volume. *Field-line Tracing* — the `#FIELDLINE`
  and `#COUPLEFIELDLINE` commands define field lines extracted from SC/IH/OH and handed to the SP or
  PT component, `CON/Coupler/src/CON_bline.f90` implements the field-line grid, and `ray`, `lin`,
  `eqr` and `eqb` plot areas emit traced-field-line products. *Energy Spectra* — the SP models solve
  energy distributions, and the SPECTRUM tool (`Param/SPECTRUM.in.test`, CHIANTI table
  `SPECTRUM_chianti_tbl.dat`) synthesizes spectra from an SWMF box output; its reference result
  ships as `output/test9/spectrum.out.gz`. *Data Access and Retrieval* —
  `share/Python/Scripts/prepare_geospace.py` downloads OMNI solar wind through `swmfpy` and writes
  the `IMF.dat` driver file; `share/IDL/Solar/procedures_local.pro` retrieves CDAWeb datasets with
  `spdfgetdata`; `share/IDL/Solar/download_WL_obs.pro` and the `download_images` routine retrieve
  coronagraph and EUV images through `vso_search`. *Calibration* —
  `share/IDL/Solar/get_eit_set.pro` downloads raw Level-Zero SOHO/EIT images and calibrates them
  with `eit_prep` against the SSWDB calibration database before comparison. *Image Processing* —
  `euv_center_image.pro`, `euv_extract_image.pro`, `make_WL_image.pro`. *Time Series Analysis* —
  `compare_insitu.pro` reads SWMF virtual-satellite time series, retrieves the matching in-situ
  observations and compares them over ICME intervals taken from `ICME_list_EARTH.csv`. *Analysis* —
  the derived quantities, shock tracing (`#TRACESHOCK`) and comparison metrics throughout.
  - *Considered and not selected:* `Data Assimilation`. Gombosi et al. (2021) discusses data
    assimilation as a current-and-future direction (§8.2, "Data Digestion and Assimilation, Ensemble
    Modeling and Uncertainty Quantification"), not as a shipped capability of the framework, and no
    assimilation code is present in the distribution.
  - *Considered and not selected:* `ML/AI` under any parent. Machine learning appears in
    Gombosi et al. (2021) only as future work (§8.1, "Machine Learning"); no ML component ships.
- **Data Visualization** — `doc/index.html` lists an "IDL visualization Manual" documenting the
  package in `share/IDL`, which supplies plotting procedures (`procedures.pro`, `funcdef.pro`,
  `vector.pro`, colour tables), *2D Graphics* and *2D Slices* for the cut planes, *3D Graphics* for
  the `3d` and Tecplot outputs, *Line Plots* for the log, satellite and magnetometer time series, and
  *Movies* via `PostProc.pl -M` ("The series of individual IDL plot files can be concatenated into
  single movie files"), `make_WL_movie.pro` and `animate_xyz.pro`.
  - *Considered and not selected:* `Data Visualization: Web-Based`, `Orbit Plots`, `Spacecraft
    Formation Plots`, `Spectrogram`, `Hodograms`, `Mission-Specific`, `ML/AI`. No shipped code
    produces these products.
- **Models and Simulations** — *MHD* and *First Principles*: BATS-R-US is a block-adaptive
  hydrodynamic and extended-MHD solver and is the basis of the EE, SC, IH, OH and GM components.
  *Physics-Based*: the framework's stated purpose is to use "first-principles-based physics models
  for all of the involved domains" (`doc/Tex/PHYSICS.tex`). *Empirical*: the manual's list of
  available empirical models — Gibson-Low and Titov-Démoulin flux ropes, the breakout model, STITCH,
  Tsyganenko 1996 and 2004, Weimer 1996 and 2000 and further ionospheric electrodynamics models, MSIS
  and IRI. *Forecasting*: operational use at the NOAA Space Weather Prediction Center is documented
  in Gombosi et al. (2021) §4.2.2, "Operational Use at NOAA/SWPC and the CCMC", and the operational
  configuration ships in `Param/SWPC/`.
  *Data Guided*: runs are driven by observed inputs — synoptic magnetograms via `NameHarmonicsFile`,
  measured solar wind and IMF via `IMF.dat`, and the F10.7 index. *Field-line Tracing*: MFLAMPA
  advects particles along field lines supplied by the MHD components. *Observatory/Instrument Models*
  and *Instrument Response*: the `los ins` plot area synthesizes images as specific instruments would
  observe them, and instrument response tables (`AiaXrt`, `EuviA`, `EuviB`, `euv`) are loaded through
  `#LOOKUPTABLE` in the shipped standard tests — see Field 31.
  - *Considered and not selected:* `Forward-Fitting`, `Theory`, `Mission-Specific`, `ML/AI`.
- **Servers and Environments: High Performance Computing** — MPI is required for parallel execution,
  OpenMP is supported, and "a significant fraction of the SWMF has been ported to GPUs using the
  OpenACC library". Components on disjoint processor sets execute concurrently; the manual states
  that meaningful runs need "a minimum of 8 processors and a minimum of 8GB of memory"; job scripts
  for named supercomputers ship in `share/JobScripts/` and are copied into the run directory when the
  hostname matches.
  - *Considered and not selected:* `Software or Environment Container` (no container recipe ships)
    and `Infrastructure as Code`.
- **Considered and not selected: the whole `Mission-related` branch.** SWMF is operated
  round-the-clock at a forecasting centre, but it is not part of any mission's ground system,
  pipeline or operations chain, which is what that branch denotes. Its `System Testing` child was
  also weighed against SWMF's substantial automated test suite (`Makefile.test` defines the compile,
  rundir, run and check targets for scores of named tests, exercised nightly across several compilers
  and machines) and rejected for the same reason: that child means mission system testing, not a
  project's own regression suite.

### 5. Related Region (MANDATORY)
- Chromosphere
- Corona
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Inner Magnetosphere
- Earth Ionosphere
- Earth Magnetosheath
- Earth Magnetosphere
- Earth Magnetotail
- Earth Outer Magnetosphere
- Earth Thermosphere
- Heliosheath
- Interplanetary Space
- Jupiter Magnetosphere
- Mars Magnetosphere
- Photosphere
- Planetary Magnetospheres
- Saturn Magnetosphere
- Solar Environment
- Solar Interior
- Solar Wind
- Uranus Magnetosphere

*Source note:* The value this record previously carried was `Earth Magnetosphere` alone, which describes one of the
framework's fifteen domains. All values above are confirmed against the live `Region` vocabulary
(the flat 24-row list) and each maps to a named SWMF domain or a published application.

Mapping from the manual's domain list (`doc/Tex/SWMF_introduction.tex`):

| SWMF domain | Region(s) |
|---|---|
| CZ — Convection Zone | Solar Interior |
| EE — Eruptive Event generator | Photosphere, Chromosphere, Corona |
| SC — Solar Corona | Corona, Chromosphere, Photosphere, Solar Environment |
| IH — Inner Heliosphere | Interplanetary Space, Solar Wind |
| OH — Outer Heliosphere | Heliosheath, Interplanetary Space |
| SP — Solar Energetic Particles | Interplanetary Space, Solar Wind |
| GM — Global Magnetosphere | Earth Magnetosphere, Earth Magnetotail, Earth Outer Magnetosphere, Earth Magnetosheath |
| IM — Inner Magnetosphere | Earth Inner Magnetosphere |
| RB — Radiation Belts | Earth Inner Magnetosphere |
| PS — Plasma Sphere | Earth Inner Magnetosphere |
| IE — Ionosphere Electrodynamics | Earth Ionosphere, Earth Auroral Subregion |
| PW — Polar Wind | Earth Ionosphere, Earth Auroral Subregion |
| UA — Upper Atmosphere (GITM) | Earth Thermosphere, Earth Ionosphere, Earth Atmosphere |
| PC — Particle-in-Cell, PT — Particle Tracker | domain-agnostic solvers, embedded in the regions above |

Planetary regions rest on §7 of Gombosi et al. (2021), "Planetary environments and Solar Analogs",
which states the SWMF "has been used to
simulate the space environment of most solar system planets, including Mercury …, Venus …, Mars …,
Jupiter …, Saturn …, and Uranus", plus comets and the moons Io, Europa, Ganymede, Titan and
Enceladus. Mercury, Venus, the moons and comets have no dedicated row and are covered by
`Planetary Magnetospheres`; Mars, Jupiter, Saturn and Uranus have their own rows and are listed.

- **Considered and not selected: `Neptune Magnetosphere`.** `#PLANET` accepts `NEPTUNE`, but the
  command's own conditional groups Neptune with `NEW`, `GANYMEDE`, `PLUTO`, `BORRELLY` and the
  numbered comets — the cases for which the user must supply radius, mass, rotation rate and field
  geometry by hand. Neptune is therefore a user-defined body rather than a built-in one, and §7 of
  Gombosi et al. (2021) stops at Uranus. Selecting it would claim an application the evidence does
  not support.
- **Considered and not selected: `Earth Lower and Middle Atmosphere`.** GITM models the
  thermosphere and ionosphere above roughly the mesopause; nothing in the distribution reaches the
  stratosphere or troposphere.
- `Solar Environment` is retained alongside the four specific solar rows because the framework spans
  the solar environment as a whole, from the convection zone outward, and the field instruction is to
  select every region that applies.

### 6. Authors (MANDATORY)

The record carries fourteen authors, in the order below. Every one now has an ORCID, and every
affiliation that could be established is recorded with its ROR.

| # | Given name | Family name | Identifier | Affiliation(s) |
|---|---|---|---|---|
| 1 | Alex | Glocer | https://orcid.org/0000-0001-9843-9094 | Goddard Space Flight Center (https://ror.org/0171mag52) |
| 2 | Talha | Arshad | https://orcid.org/0000-0003-4704-0942 | University of Michigan (https://ror.org/00jmfr291) |
| 3 | Aaron | Bukowski | https://orcid.org/0000-0002-1960-933X | *not established* |
| 4 | Zhenguang | Huang | https://orcid.org/0000-0003-1674-0647 | University of Michigan (https://ror.org/00jmfr291) |
| 5 | Igor V. | Sokolov | https://orcid.org/0000-0002-6118-0469 | University of Michigan (https://ror.org/00jmfr291) |
| 6 | Weihao | Liu | https://orcid.org/0000-0002-2873-5688 | University of Michigan (https://ror.org/00jmfr291) |
| 7 | Qusai | Al Shidi | https://orcid.org/0000-0003-0426-038X | University of Michigan (https://ror.org/00jmfr291); West Virginia University (https://ror.org/011vxgd24) |
| 8 | Yinsi | Shou | https://orcid.org/0000-0002-5765-9231 | University of Michigan (https://ror.org/00jmfr291) |
| 9 | Daniel T. | Welling | https://orcid.org/0000-0002-0590-1022 | The University of Texas at Arlington (https://ror.org/019kgqr73); University of Michigan (https://ror.org/00jmfr291) |
| 10 | Gabor | Toth | https://orcid.org/0000-0001-8459-2100 | University of Michigan (https://ror.org/00jmfr291) |
| 11 | Valeriy | Tenishev | https://orcid.org/0000-0002-0934-4550 | University of Michigan (https://ror.org/00jmfr291) |
| 12 | Xiantong | Wang | https://orcid.org/0000-0002-8963-7432 | University of Michigan (https://ror.org/00jmfr291) |
| 13 | Yuxi | Chen | https://orcid.org/0000-0001-7288-2805 | *not established* |
| 14 | Hongyang | Zhou | https://orcid.org/0000-0003-4571-4501 | *not established* |

The order is positional rather than alphabetical, and is the order the record stores.

The record carries no affiliation for Aaron Bukowski, Yuxi Chen or Hongyang Zhou. That is a
documented gap rather than an oversight, and the three are not alike. For Bukowski nothing was
established at all. For Chen and Zhou the available evidence is circumstantial — both commit from
`umich.edu` addresses, and Gombosi et al. (2021) places Chen at the University of Michigan's
Department of Climate and Space Sciences and Engineering — which is weaker than the ORCID-backed or
credit-backed affiliations recorded for the other eleven, so none was asserted here. A curator who
judges that evidence sufficient has it recorded to act on.

Two entries carry more than one affiliation — Qusai Al Shidi (Michigan and West Virginia) and
Daniel T. Welling (Texas at Arlington and Michigan). These are unions inherited from those people's
canonical catalogue records, not a selection this dossier made; see "Two entries were duplicate
person records" below.

Three of these identifiers — Talha Arshad's, Weihao Liu's and Igor V. Sokolov's — were the hardest
to establish and are justified under "How the three hardest ORCIDs were disambiguated" below. Their
University of Michigan affiliations rest on the manual's credits and on the `umich.edu` commit
addresses in this repository, not on the ORCID records, none of which lists an employment at all.

*Provenance of the list.* The fourteen entries are the GitHub contributor accounts of this
repository, with each account's public profile name used where one exists. Six of those accounts
publish no profile name, and the record originally stored each of those six as its bare login string
in the family-name field with an empty given name — `aglocer`, `igor0sok`, `shyinsi`, `spacecataz`,
`vtenishe` and `yuxi-chen`. Those six have since been replaced by the people's real names, as
recorded in the table above.

*How the six login entries were identified.* Each was matched by the commit-author name recorded
against the same person's commits in this repository's history, cross-checked against the developer
credits in `doc/Tex/SWMF_introduction.tex` and the author list of the reference publications:
`aglocer` commits alongside the manual's credit of Alex Glocer for PWOM, CIMI and RBE; `igor0sok`
corresponds to the commits authored as `igorsok` and `Igor V. Sokolov <igorsok@umich.edu>`, the
manual's core SWMF designer and author of the coupling toolkit; `shyinsi` to Yinsi Shou, credited
with the AMPS PIC solver; `vtenishe` to Valeriy Tenishev, AMPS's main developer, who also commits as
`Valeriy Tenishev`; `yuxi-chen` to Yuxi Chen, FLEKS's developer, who also commits as
`Yuxi Chen <yuxichen@umich.edu>`; and `spacecataz` to Daniel T. Welling, whose commits appear as
`dwelling` and `Dan Welling <dwelling@umich.edu>` — GitHub attributes commits by author e-mail, so
that account owns the address. Alex Glocer, Yuxi Chen, Valeriy Tenishev and Daniel T. Welling are
also co-authors of Gombosi et al. (2021), which supplies their ORCIDs.

*How the three hardest ORCIDs were disambiguated.* Talha Arshad, Weihao Liu and Igor V. Sokolov are
common names whose ORCID searches return many candidates, none of them advertising a University of
Michigan affiliation that would settle the match. Each was resolved instead on evidence that does
not depend on affiliation:

- **Weihao Liu — `https://orcid.org/0000-0002-2873-5688`.** The record publishes the e-mail
  `whliu@umich.edu`, which is the exact address on this repository's commits by the GitHub account
  `lwh1106` — the account this record's Weihao Liu entry came from. Its works
  are SWMF-domain papers, among them "Physics-based Simulation of the
  2013 April 11 Solar Energetic Particle Event" and a 2024 study simulating the solar corona from
  multiple photospheric magnetic maps.
- **Talha Arshad — `https://orcid.org/0000-0003-4704-0942`.** The record publishes the e-mail
  `talhaa@umich.edu`, the exact address on this repository's commits by Talha Arshad. Its works
  include "A Kinetic-magnetohydrodynamic Model with Adaptive Mesh Refinement for Modeling Heliosphere
  Neutral-plasma Interaction", co-authored with Yuxi Chen and Gabor Toth — both already authors on
  this record — and "Adaptive mesh refinement in semi-implicit particle-in-cell method", which is
  FLEKS work.
- **Igor V. Sokolov — `https://orcid.org/0000-0002-6118-0469`.** This record publishes neither an
  e-mail nor an employment, so identification rests on its works, which are unmistakably the SWMF
  group's: "A Fully Automated CME Simulation Pipeline Developed by the CLEAR Space Weather Center of
  Excellence", the SOFIE solar-energetic-particle model, the Solar Wind Scoreboard hosted by NASA's
  CCMC, and "MHD Simulations of CMEs with Energy Conservation: Reconnection Thermodynamics as a
  Critical Aspect of CME Dynamics", whose author list — Xianyu Liu, Spiro Antiochos, Igor Sokolov,
  Tamas Gombosi, Nishtha Sachdeva and Lulu Zhao — puts him alongside three co-authors of Gombosi et
  al. (2021) (Gombosi, Sachdeva and Zhao).
  Separately and still true: he is the one co-author of Gombosi et al. (2021) for whom that paper's
  metadata carries no ORCID, which is why the paper could not supply this identifier.

*Gábor Tóth's ORCID has two forms, and the obvious one is dead.* The identifier to use is
`https://orcid.org/0000-0001-8459-2100`. The older `0000-0002-5654-9823` is a **deprecated** ORCID
account: resolving it yields ORCID error 9007, "This account is deprecated. Please refer to account:
https://orcid.org/0000-0001-8459-2100." The trap for a future refresh is that **Crossref's author
metadata for Gombosi et al. (2021) still carries the deprecated identifier**, so re-deriving Tóth's
ORCID from that paper — the natural move, and the source of the deprecated value this record
previously carried — lands on the dead account again. Take it from ORCID directly.

*Name-form note.* Gombosi et al. (2021) renders the name as "Qusai Al Shidi", i.e. family name
"Al Shidi". The record originally split it wrongly, as given name "Qusai Al" and family name
"Shidi"; it now carries the correct split, given name "Qusai" and family name "Al Shidi".

*Why this field once could not be corrected, and what that leaves behind.* Six of the record's
author entries were stored as bare GitHub logins with an empty given name. That is not merely
untidy: while any author linked to a record has a blank given name, **an update touching the authors
field is rejected outright**, so identifiers, affiliations and additional authors could not be
applied to this record at all; and a person's name cannot be changed through a metadata update in any
case — renames submitted that way are silently ignored even when the update is accepted. The two
failure modes compound, because the only thing that would have unblocked the field was precisely the
thing a metadata update cannot do. The six rows were therefore corrected at the database level rather
than through a metadata refresh, and the table above is now the record's actual state rather than an
aspiration.

The durable lesson is about the shape of the problem, not the repair: **a blank given name on any
linked author silently disables the whole authors field**, and a metadata refresh cannot fix it. An
agent that meets an author whose family name looks like a username should expect both symptoms
together and should not read the rejection as a fault in the values it is submitting.

*Two entries were duplicate person records, and person records are shared.* Two of the fourteen —
Qusai Al Shidi and Daniel T. Welling — existed as second, ORCID-less person records duplicating
canonical records that already carried their ORCIDs. They were reconciled onto the canonical records
rather than edited in place, which is why those two entries now show affiliations this dossier never
proposed: Welling's University of Michigan affiliation and Al Shidi's West Virginia University
affiliation arrived with their canonical records.

**Person records in HSSI are shared across software records**, and both of these are cited by other
software besides SWMF. Two consequences a future agent should carry into any author edit here: a
change to one of these people is not local to SWMF and may affect records maintained by someone else,
and a name or affiliation appearing on this record without a source note may have arrived as a union
from another record rather than from SWMF's own evidence.

*The manual's credits are documented candidates, not omissions to be fixed.* GitHub contributors of
this repository are an imperfect proxy for SWMF's authorship: the repository dates from 2023 while
the code dates from 2001, so the contributor list omits most of the people who wrote the framework.
The
first-party credits in `doc/Tex/SWMF_introduction.tex` name the core design and code development as
the work of Gábor Tóth, Igor Sokolov and Ovsei Volberg, and credit the first version and its physics
components to David Chesney, Yue Deng, Darren DeZeeuw, Tamas Gombosi, Kenneth Hansen, Kevin Kane,
Ward (Chip) Manchester, Robert Oehmke, Kenneth Powell, Aaron Ridley, Ilia Roussev, Quentin Stout,
Igor Sokolov, Gábor Tóth and Ovsei Volberg; Tóth et al. (2005) is essentially that same list.
Bart van der Holst is named as a current principal BATS-R-US developer. Of these, only Gábor Tóth
and Igor Sokolov appear in the fourteen.

They are recorded here as documented candidates rather than added, and the reason is substantive
rather than technical: the two lists describe different populations. The fourteen are the people who
have committed to *this* repository — the framework — whereas the manual's credits name historical
contributors of component models, many developed at other institutions (Rice, Los Alamos, NASA
Goddard, Arizona, KTH, KU Leuven) and each carrying its own separate repository, several of which are
listed in Field 29 in their own right. Folding those credits into this record's author list would
attribute the framework to people who authored components rather than the framework, and would
duplicate authorship that belongs on the component software's own records. A future curator who
disagrees has the full credit list here to work from; the names are preserved for that purpose.

### 7. Software Name (MANDATORY)
SWMF

*Source note:* Retained from the existing HSSI record and independently correct. It is the
repository name, the executable name (`SWMF.exe`), the name used throughout the manual and scripts,
and the abbreviation the University of Michigan page and the reference publications use. The
expansion "Space Weather Modeling Framework" belongs in the description, where it opens the first
sentence, and in Field 16 keywords; putting it in the name field would diverge from the repository
without adding discoverability that the description does not already provide.

### 8. Description (MANDATORY)

The Space Weather Modeling Framework (SWMF) is a high-performance software framework for coupling
physics-based models of the Sun-Earth system into a single, concurrently executing simulation. It
provides a common operating environment in which independently developed models, each covering one
physical domain, are registered as components, given their own processor layouts, and advanced and
coupled on schedules the framework controls. SWMF spans fifteen domains reaching from the solar
convection zone to the upper atmosphere of the Earth: Convection Zone, Eruptive Event generator,
Solar Corona, Inner Heliosphere, Outer Heliosphere, Solar Energetic Particles, Global Magnetosphere,
Inner Magnetosphere, Plasma Sphere, Radiation Belts, Particle-in-Cell, Particle Tracker, Polar Wind,
Ionosphere Electrodynamics and Upper Atmosphere. Any meaningful subset of the models can be run and
coupled together.

A Control Module (CON) performs component registration, processor layout, session and time
management, and the initialization, execution, coupling and finalization of the components. Each
coupling connects one source component to one target component, two-way coupling is expressed as two
couplings with the roles reversed, and only the processors involved in a coupling communicate, so
the remaining processors keep working. Components placed on disjoint processor sets execute
concurrently, and for steady-state calculations each component may progress toward equilibrium at
its own rate. A user-supplied physics code becomes a component by adding two small units of code — a
wrapper providing the control functions CON needs, and a coupling interface performing the data
exchange — both assembled from building blocks the framework supplies, so models keep their
stand-alone identity while SWMF builds one executable, SWMF.exe. A run is configured entirely
through a PARAM.in text file that CON reads and broadcasts, and every input command is described in
machine-readable PARAM.XML files that also drive a graphical parameter editor, a parameter checker
and the generated command reference in the manual.

The models distributed with SWMF include the BATS-R-US block-adaptive extended-MHD code, used for
the eruptive event generator, solar corona, inner and outer heliosphere and global magnetosphere;
the inner-magnetosphere and radiation-belt models RCM, CIMI, HEIDI, RAM-SCB and RBE; the Ridley
Ionosphere Model; the Global Ionosphere-Thermosphere Model and its Mars variant; the Polar Wind
Outflow Model; the solar energetic particle models of Kóta and MFLAMPA; and the FLEKS, AMPS and
iPIC3D kinetic and particle-in-cell solvers. Empirical models are available alongside them,
including Tsyganenko 1996 and 2004, Weimer 1996 and 2000, MSIS and IRI, and the Gibson-Low,
Titov-Démoulin, breakout and STITCH eruption initiators. SWMF runs in parallel using MPI, supports
multi-threaded execution through OpenMP, and has a significant fraction ported to GPUs with OpenACC.
It runs under UNIX, Linux and macOS, requires Fortran 2008 and C/C++ compilers and Perl, and is
exercised nightly by an automated test suite across several compilers and machines.

Simulations are driven by observed inputs — synoptic photospheric magnetograms, measured solar wind
and interplanetary magnetic field, and solar radio flux — and produce plot files, virtual-satellite
and ground-magnetometer time series, and synthetic line-of-sight images in the passbands of specific
solar instruments. A shipped IDL package post-processes and visualizes these outputs and downloads
the corresponding observations for direct model-data comparison.

Although its principal applications are space physics and space weather, including operational use
at the NOAA Space Weather Prediction Center and runs-on-request service through the Community
Coordinated Modeling Center, SWMF has also been applied to the space environments of Mercury, Venus,
Mars, Jupiter, Saturn and Uranus, to planetary moons and comets, to the outer heliosphere, and to
astrospheres and exoplanet environments, as well as to high energy density physics and general
plasma physics.

*Source note:* **This replaces a previous, incorrect description.** The value this record
previously carried was the
opening paragraph of `README.md`: "This document outlines how to install the SWMF on your system and
how to create and access the documentation. To learn more about the SWMF, including how to compile
and run the code, please consult the user manual. To install the SWMF and create the user manual
please follow the instructions below." That text is installation front-matter — it describes the
README rather than the software, and its own second sentence directs the reader elsewhere to find
out what SWMF is. It reached HSSI through automated repository extraction, which selects the first
prose block of the README as the description; running that extraction against this repository today
returns the same paragraph, confirming the origin. It also renders a useless catalogue preview,
since the first 150-200 characters are a statement about a document.

The replacement is written from first-party sources: `doc/Tex/SWMF_introduction.tex` (the
Introduction, "The SWMF in a Few Paragraphs", and System Requirements sections) for the domain list,
the CON design, the wrapper/coupling-interface model, the concurrency rules, the component and
empirical-model inventory, and the platform and language requirements; `PARAM.XML` and
`doc/Tex/SWMF_param.tex` for the parameter-file mechanism; `Param/` and `output/` for the driven
inputs and the synthetic-image outputs; `share/IDL/` for the post-processing and comparison package;
and Gombosi et al. (2021) §4.2.2 and §7 for the operational deployments and the planetary,
heliospheric and astrospheric applications. The final paragraph's non-space-weather applications are
also stated on the University of Michigan distribution page: "The SWMF can also be used for many
other applications not related to space weather, including but not restricted to high energy density
physics, exoplanets, and general plasma physics."

### 9. Concise Description (OPTIONAL)
A high-performance framework that couples physics-based models of the Sun-Earth system, from the
solar convection zone to Earth's upper atmosphere, into a single parallel space weather simulation.

*Source note:* 196 characters, within the 200-character limit. Written for this record because the
description's opening sentence, while accurate, does not convey the framework's physical span, which
is what distinguishes SWMF in a search result.

### 10. Publication Date (RECOMMENDED)
2023-07-05

*Source note:* Carried over unchanged from the existing HSSI record. It is the creation date of the
`SWMFsoftware/SWMF` repository, which is the date the code became publicly available at its current
authoritative distribution point.

Alternatives considered and rejected. The first commit in the history is dated 2001-03-02 and its
message is "Initial revision" — it is a CVS import of an internal repository, not a publication.
Tóth et al. (2005) is the paper that introduced SWMF to the community, but a paper's publication date
is a property of the paper, and it is already recorded in Field 14. The 2020 release of the
non-commercial MSTEM-QUDA subset was an earlier public availability milestone, but it covered a
subset of the code and that channel has since been retired, so dating the record from it would be
misleading. No first-party page states a release date for SWMF. The stored value is defensible and
is left alone.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

*Source note:* No DOI has been obtained for the software (Field 2), and the field instruction for
that case is to name the repository host. GitHub has no ROR record, so the identifier is the
organization URL, which the field permits.

Considered and rejected: the University of Michigan (https://ror.org/00jmfr291). It is the
copyright holder, the developing institution and the body that administers the registered-user
licence, and it would be the right answer to "who publishes SWMF" in ordinary usage. It is not what
this field asks for when no DOI exists, and it is already recorded through the author affiliations
and the Field 25 funder context.

### 12. Version (RECOMMENDED)
Not found — SWMF does not issue numbered releases.

*Source note:* This is a documented negative result, not a gap. SWMF identifies code versions by git
reference rather than by release number, and the framework says so itself. The evidence, so that a
later refresh does not manufacture a version:

- **First-party statement.** `PARAM.XML` documents the `#VERSION` command as: "This command is
  obsolete. We now use Git references to identify the code version. The only use of this command is
  to be compatible with restart files produced before VersionSwmf was removed."
- **Runtime behaviour matches.** `CON/Control/src/show_git_info.h.orig` is the placeholder for the
  generated build-identification header; it reports the git repository and git references, and when
  they are unavailable prints "GIT REFERENCES HAVE NOT BEEN OBTAINED!". The framework source carries
  no release-version constant of its own. The `Version` and `NameVersion` fields that do exist, in
  `CON/Library/src/CON_comp_info.f90`, hold "component information such as name, version name and
  number" — that is, which *model version* fills each component slot (`BATSRUS`, `Empty`, and so on),
  which is a configuration fact, not a release designation for SWMF.
- **No releases.** The GitHub repository has published no releases.
- **The git tags are not release tags.** Of the 139 tags, `version_3_0` and `SWMF_2009_11_22` both
  point at commits whose message is "This commit was manufactured by cvs2svn to create tag …", i.e.
  artifacts of the 2009 CVS-to-Subversion conversion; four more (`v040819`, `v040820`, `v04_08_16`,
  `v04_08_23`) are date-stamp names from a six-day span in August 2004 (2004-08-16 through
  2004-08-22 — note that the tag named for the 23rd is dated the 22nd). The large remainder are run
  milestones imported from the
  AMPS/particle-tracker history — names such as `ROSETTA_COPS_END_OF_THE_MISSION_MODEL__ROSETTA_SWT__031517`,
  `MARS_AERONOMY_CONFERENCE__16MAY2017`, `FAST_WAVE_TEST_WORKS`, `TEST1`, `TEST2`, `TEMPORARY` and
  `works-fine--05Nov2015`. **Choosing among these by recency would be wrong**: the most recent tags
  are 2018 particle-solver run labels, and no tag marks a state of the framework that anyone
  released.
- **`doc/RELEASENOTES` is not a release log.** It is a known-issues list for components; its latest
  dated entry is "FIXED: 09/24/2005".
- **The `${VERSION}` make variable is not a product version.** The `XY_VERSION` variables in the
  generated `Makefile.def` select *which model version* is compiled into each component slot
  (`GM_VERSION = Empty`, `SC_VERSION = BATSRUS`, …). The bare `${VERSION}` appearing in the tarball
  name `SWMF_v${VERSION}_<date>.tgz` is not set at the framework level.
- **The manual carries no version.** The user manual's title page reads "Space Weather Modeling
  Framework User Manual" with no release or milestone designation, and the manual served from the
  first-party documentation site is rebuilt nightly from the current source.
- **The first-party distribution page states no version.** The University of Michigan CLaSP "SWMF
  Downloadable software" page directs users to `github.com/SWMFsoftware` and to a registration
  process; the only versioned artifact offered there is `FDIPS_v1.2.tgz`, a separate potential-field
  solver, not SWMF.
- **No DOI supplies one.** The Zenodo record examined and rejected in Field 2 carries a null
  version, and no other archival deposit of the framework surfaced in the DataCite or Zenodo searches
  recorded there.
- **Considered and rejected: the CCMC labels.** CCMC's runs-on-request catalogue lists "SWMF 2023"
  and, for a component, "SWMF/IM=RCM, Version: 20180525". CCMC's own page explains the latter as
  "the version used in the SWMF 2018 as the Inner Magnetosphere (IM) component" — these are
  date-stamped identifiers for the particular code instances CCMC has installed and validated, i.e.
  deployment labels applied on the CCMC side, not release designations issued by the SWMF
  developers. Nothing first-party uses them.

Recording any of the above as Field 12 would assert a release that does not exist. Leaving the field
empty is the accurate outcome. If a citable snapshot is ever wanted, the correct route is a
first-party archival deposit with its own DOI, which would then populate Fields 2 and 12 together.

### 13. Programming Language (RECOMMENDED)
- C
- C++
- Fortran 2003
- Fortran 2008
- Fortran77
- Fortran90
- IDL
- Other
- Python 3.x

*Source note:* The value this record previously carried was `Fortran90, Java, Julia, Other, Rust, SQL, Typescript`.
**`Java`, `Julia`, `Rust`, `SQL` and `Typescript` are removed as unsupported by any evidence**;
`Fortran90` and `Other` are kept; and seven values are added.

Why the five removals are safe. The repository contains no `.java`, `.jl`, `.rs`, `.sql`, `.ts` or
`.tsx` file at the pinned revision, and GitHub's own language statistics for the repository report
none of these five. The set they came from looks like the residue of a bad autofill rather than an
observation of the code. One of the five, and one related language that was never stored, are worth a
second sentence because a superficial check could reinstate either:

- *Julia* is absent from the framework tree, and where the distribution does mention it, it points
  outward rather than inward: `share/Julia/` contains only a README directing users to the external
  package `Batsrus.jl` for reading SWMF output, and `share/MATLAB/README.md` notes that "A new
  version has been implemented with Julia" and links the external VisAnaJulia. That makes Julia an
  *interoperating* language (Field 30), not an implementation language.
- The same holds for *MATLAB*, which was never in the record and is not added here: `share/MATLAB/`
  likewise contains only a README pointing to the external VisAna package.

Evidence for each retained and added value:

- **Fortran90** — the manual: "The core of the SWMF and most of the models are implemented in
  Fortran90." The framework tree holds 72 `.f90` files and no other Fortran source.
- **Fortran77** — the manual: "Some models are written in Fortran 77."
- **Fortran 2003** and **Fortran 2008** — the manual: "A few features of Fortran 2003 and 2008 are
  also used", and the system requirements state "A FORTRAN 2008 compiler must be installed."
  (`Fortran 2023` exists in the vocabulary and is not claimed anywhere.)
- **C++** — the manual: "others are written in C++", naming iPIC3D and AMPS as parallel C++ codes.
  These live in their own component repositories, not in the framework tree.
- **C** — the system requirements state "A C/C++ compiler must be installed", and the manual lists
  the supported C compilers (GNU gcc, Apple clang, Intel icc, PGI pgcc, IBM mpxlc);
  `Config.pl -install -compiler=...` accepts a C compiler after a comma.
- **IDL** — `doc/index.html` lists an "IDL visualization Manual in PDF format" documenting the
  package in `share/IDL`, which supplies the plotting, post-processing and model-data comparison
  procedures; `PostIDL.exe` and the `idl`, `idl_ascii`, `idl_real4` and `idl_real8` plot formats are
  named after it. It is a user-facing part of the distribution rather than an incidental script.
- **Python 3.x** — `share/Python/Scripts/` ships `swmf_datafile.py` (an SWMF data-file reader and
  writer, with its own test), `prepare_geospace.py` (builds the `IMF.dat` solar-wind driver and sets
  F10.7 in `PARAM.in`) and `plot_indices.py`; the shebang is `#!/usr/bin/env python3`.
- **Other** — Perl and shell. Perl is a hard requirement ("The Perl interpreter must be installed")
  and is the language of `Config.pl`, `Scripts/*.pl`, `PostProc.pl`, `Restart.pl`, `TestParam.pl` and
  the XML-to-LaTeX documentation generator; GitHub's statistics rank Perl second after Fortran. Shell
  scripts and the extensive Makefile system also fall here.

A trap for future refreshes: GitHub's language statistics for this repository also report `Scala` and
`SourcePawn`. Both are extension misdetections of SWMF parameter files — `Param/PARAM.in.test.SC` is
read as Scala (`.sc`) and `Param/PARAM.in.test.SP` as SourcePawn (`.sp`), the suffixes being the
Solar Corona and Solar Energetic Particle component IDs. Neither language is present, and neither has
a row in the HSSI vocabulary in any case.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1016/j.jcp.2011.02.006

Tóth, G., van der Holst, B., Sokolov, I. V., De Zeeuw, D. L., Gombosi, T. I., Fang, F.,
Manchester, W. B., Meng, X., Najib, D., Powell, K. G., Stout, Q. F., Glocer, A., Ma, Y.-J., &
Opher, M. (2012). Adaptive numerical algorithms in space weather modeling. *Journal of
Computational Physics*, 231(3), 870-903.

*Source note:* Chosen because the developers designate it. The University of Michigan CLaSP "SWMF
Downloadable software" page introduces SWMF and then states "The SWMF review paper provides more
detailed information", with that phrase hyperlinked to `https://doi.org/10.1016/j.jcp.2011.02.006`.
The same designation appears in both the current page and its 2024 version, so it is settled
first-party guidance rather than a transient edit. DOI, title, journal, volume, pages and author list
verified through Crossref.

Considered and not selected for this field, and recorded in Field 27 instead:

- **Tóth et al. (2005), `https://doi.org/10.1029/2005JA011126`** — "Space Weather Modeling Framework:
  A new tool for the space science community", the paper that introduced SWMF. It is the more obvious
  choice by title, and a reader may reasonably expect it here. It is placed in Related Publications
  because Field 14 asks for the publication describing the software and the developers point to the
  2012 paper for that purpose; the 2005 paper describes the framework at its introduction, while the
  2012 and 2021 papers describe substantially more developed later states.
- **Gombosi et al. (2021), `https://doi.org/10.1051/swsc/2021020`** — the most recent and most
  comprehensive review, and the paper this dossier draws on most heavily. It is not designated as
  the reference publication by any first-party page.

**A naming convention this dossier follows, and a trap it exists to prevent.** "The reference
publication", singular, means only the paper named at the head of this field — Tóth et al. (2012).
Every other citation names its paper explicitly. This matters because the paper cited most often
throughout the dossier is Gombosi et al. (2021), not the reference publication, and the two have
different author lists and different section structures: an agent that reads "the reference
publication §7" and opens Tóth et al. (2012) — a numerical-methods paper with no planetary-
applications section and no NOAA-operations section — finds nothing and may conclude the evidence is
fabricated. Section numbers such as §4.2.2, §5.9, §7, §8.1, §8.2 and §8.3 in this dossier all belong
to Gombosi et al. (2021) and are named as such at each use. The plural "the reference publications"
means the three papers of Fields 14 and 27 collectively.

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** https://spdx.org/licenses/Apache-2.0

*Source note:* `LICENSE.txt` at the repository root carries the Apache License, Version 2.0 grant
text under the heading "Copyright (C) 2002 Regents of the University of Michigan, portions used with
permission." An identical Apache-2.0 `LICENSE.txt` also sits at the root of component and library
repositories, `BATSRUS` and `share` among them. The University of Michigan CLaSP page states it
directly under the heading
"Open source SWMF": "The SWMF is open source under the Apache 2 license." The value matches the
live `License` vocabulary row exactly, and the URI is that row's own SPDX URL.

Why the automated signals disagree, and why they are wrong. GitHub's license detector reports
`NOASSERTION` / "Other" for this repository: the two-line copyright preamble prefixed to the standard
Apache boilerplate defeats its exact-match heuristic. That is a detection artifact, not a licensing
ambiguity — the grant text below the preamble is the unmodified Apache 2.0 wording.

Two further sources of confusion, recorded so they are not mistaken for the licence:

- `Copyrights/` contains `UM.long`, `UM.short`, `UM.html`, `VAC_UM.*`, `NCAR.*`, `SMLIB.long` and
  `REGISTERED_USER_LICENSE.pdf`. `UM.long` and `UM.html` are restrictive 1996/2002-era terms
  ("PERMISSION IS GRANTED TO A SINGLE USER … NO PERMISSION IS GIVEN TO COPY OR REDISTRIBUTE"). These
  are legacy and third-party notices retained for the "portions used with permission" material and
  for the historical registered-user distribution channel; `UM.short` is reproduced on the manual's
  title page. They are superseded by the root `LICENSE.txt` for the code distributed in this
  repository.
- The CLaSP page keeps a separate "SWMF with registration" section: signing a user licence agreement
  is what grants *support and write access* to the SWMFsoftware organization, not what grants the
  right to use the code. `Restricted` was considered for this field on the strength of that section
  and rejected: the code is publicly readable and Apache-2.0 licensed, and the page's own headings
  separate the open-source grant from the registration process.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
space weather; magnetohydrodynamics; MHD; swmf; batsrus; magnetosphere; inner magnetosphere;
ionosphere; thermosphere; solar corona; solar wind; heliosphere; coronal mass ejections;
geomagnetic storms; solar energetic particles; radiation belts; particle-in-cell;
adaptive mesh refinement; model coupling; high performance computing; space weather forecasting;
planetary magnetospheres; exoplanets; space physics; plasma; heliophysics; polar wind;
upper atmosphere

*Source note:* Each term is entered as a single keyword
rather than a comma-joined string, and each is spelled to match an existing row where one exists.
**Case matters more than it looks.** Keywords is the one open vocabulary — an unmatched term is
created rather than rejected — so a term differing from an existing row only in case silently mints a
near-duplicate instead of reusing it. The live vocabulary is mixed-case (`MHD`, `3D visualization`,
`aacgm`), so lower-casing on principle is wrong. `MHD` is therefore given in capitals: that is the
spelling of the existing row, and no lower-case `mhd` row exists. `MHD` and `magnetohydrodynamics`
are both included because both rows already exist and both are used as search terms.

Of the 28 terms above, 21 reuse a keyword row that already existed. The other seven —
`inner magnetosphere`, `solar corona`, `particle-in-cell`, `adaptive mesh refinement`,
`model coupling`, `space weather forecasting` and `polar wind` — were new to the vocabulary; each
names a domain or capability documented from first-party sources above, and none collided with an
existing row under case-insensitive comparison.

The terms trace to the framework's domain list and component inventory, to the keyword line of
Gombosi et al. (2021) ("space weather – solar flares and CMEs – scientific computing – space plasma
physics – MHD"), and to the applications documented in Field 5. `exoplanets` follows the
University of Michigan page's statement that SWMF is used for exoplanet work. `fortran` was
considered and dropped as redundant with Field 13.

### 17. Data Sources (OPTIONAL)
- CDAWeb
- HTTP/HTTPS Directories
- Observatory/Mission-specific
- OMNIWeb
- The Virtual Solar Observatory.

*Source note:* Each entry matches a live `DataInput` row exactly,
including the trailing full stop in "The Virtual Solar Observatory." — the stored row name ends with
a period and a copy without it would be rejected.

- **CDAWeb** — `share/IDL/Solar/procedures_local.pro` implements `get_insitu_data`, which calls
  `spdfgetdata` (the SPDF/CDAWeb web-services library) to retrieve
  `OMNI_COHO1HR_MERGED_MAG_PLASMA`, `STA_COHO1HR_MERGED_MAG_PLASMA`,
  `STB_COHO1HR_MERGED_MAG_PLASMA`, `PSP_COHO1HR_MERGED_MAG_PLASMA` and
  `SOLO_COHO1HR_MERGED_MAG_PLASMA` for comparison against SWMF virtual-satellite output.
- **OMNIWeb** — the OMNI dataset above, and `share/Python/Scripts/prepare_geospace.py`, which builds
  the `IMF.dat` solar-wind driver from OMNI data through `swmfpy.write_imf_from_omni` and
  `swmfpy.web.get_omni_data`.
- **HTTP/HTTPS Directories** — `swmfpy.web.get_omni_data` downloads from the static directory tree
  at `https://spdf.gsfc.nasa.gov/pub/data/omni`; the F10.7 series shipped as `Param/f107.txt` records
  in its own header that it was downloaded from the LASP LISIRD Penticton radio flux service.
- **The Virtual Solar Observatory.** — the `download_images` routine in
  `share/IDL/Solar/procedures_local.pro` calls `vso_search(date=…, source='SDO', det='aia',
  wave='94-335 Angstrom')` to locate observations, and `share/IDL/Solar/README_EIT` states that the
  SolarSoft VSO package is required for `get_eit_set.pro`.
- **Observatory/Mission-specific** — selected as Field 31 instructs, because the retrievals above are
  per-mission datasets and per-instrument image searches rather than generic archive queries. The
  corresponding missions are listed in Field 32.

Considered and not selected: `Other` for the synoptic magnetogram inputs. SWMF reads magnetograms
from local files in a harmonic-coefficient or map format; it does not fetch them from an archive, and
the preparation workflow that does lives in the separate `SWMFSOLAR` repository. `SSCWeb`, `HAPI`,
`Madrigal`, `AMDA`, `das2`, `VirES`, `GFZ`, `WDC` and `S3/Cloud-aware` have no supporting evidence.

### 18. Input File Formats (RECOMMENDED)
- ascii
- CDF
- csv
- FITS
- IDL.sav
- Other

*Source note:*

- **ascii** — `PARAM.in` and its included files; the shipped harmonic-coefficient magnetograms
  (`Param/CR1922_MDI.dat`, `Param/harmonics_2209_adapt01.dat`), the ADAPT map `Param/map_04.out`, the
  solar-wind driver `Param/SWPC/IMF.dat`, satellite trajectory files, the magnetometer station lists
  `Param/supermag.dat` and `Param/magnetometer_location.dat`, and `#LOOKUPTABLE` tables loaded with
  `TypeFile = ascii`.
- **Other** — the native SWMF binary formats, which the vocabulary does not name: the `#LOOKUPTABLE`
  and restart `TypeFile` options `real4` and `real8` (single- and double-precision binary "IDL"
  format) and `log/sat`, plus Tecplot input.
- **FITS** — `share/IDL/General/read_fits.pro` is a full FITS reader; `share/IDL/Solar` supplies
  `euv_fits_to_ascii.pro` and `share/IDL/General/fits_to_tec.pro`; `get_eit_set.pro` saves and reads
  raw Level-Zero EIT FITS images; the shipped ADAPT map records `InputFile = ADAPT_CR2154.fits` in
  its header. `share/Python/pyfits/` bundles a FITS library on the Python side.
- **CDF** — `share/IDL/General/cdf_to_log.pro` converts CDF into SWMF log format, and the CDAWeb
  retrievals above deliver CDF data.
- **csv** — `share/IDL/Solar/ICME_list_EARTH.csv` is read by `get_CME_interval` to select comparison
  intervals, and the `Param/f107.txt` header documents reading the LISIRD CSV export through the IDL
  package's `read_log_data`.
- **IDL.sav** — `share/IDL/Solar/los_template.sav` is an IDL save file used by the line-of-sight
  comparison scripts.

Considered and not selected: `HDF5` as an *input* format — the manual states only that "Some models
use HDF5 output", so it is claimed under Field 19 alone. `netCDF3/4`, `JSON`, `ISTP-Compliant` and
`Zarr` have no supporting evidence in the distribution.

### 19. Output File Formats (RECOMMENDED)
- ascii
- HDF5
- Other

*Source note:* The `#SAVEPLOT` command's documented `PlotForm`
values are the direct evidence: `tec` (node-based Tecplot), `tcp` (cell-centred Tecplot), `hdf`
(HDF5, for VisIt), `idl`/`idl_real4` (single-precision binary), `idl_real8` (double-precision
binary), `idl_ascii` and `idl_tec` (ASCII with a Tecplot header).

- **ascii** — the `idl_ascii`, `idl_tec` and ASCII Tecplot forms, plus the log, satellite and
  magnetometer files; the shipped reference outputs include `.log`, `.sat` and `.out` text files.
- **HDF5** — the `hdf` plot form, and the manual's system requirements: "Some models use HDF5 output.
  For these the parallel version of the HDF5 library has to be installed. The
  `share/Scripts/install_hdf5.sh` shell script can be used to do that."
- **Other** — the binary IDL formats (`idl_real4`, `idl_real8`) and binary Tecplot, none of which the
  vocabulary names; also the restart file trees written by `Restart.pl`.

Considered and not selected: `FITS`, `CDF`, `csv`, `netCDF3/4`, `JSON`, `ISTP-Compliant`, `Zarr` and
`IDL.sav`. SWMF reads FITS, CDF and CSV through its IDL and Python tooling but does not write them;
the visualization scripts emit EPS and PNG figures, which the vocabulary does not cover and which are
figures rather than data.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac

*Source note:* The manual's System Requirements state it
directly: "The SWMF runs only under the UNIX/Linux operating systems. This now includes Macintosh
system 10.x because it is based on BSD UNIX. **The SWMF does not run under any Microsoft Windows
operating system.**" The University of Michigan page repeats the requirement as "a Linux/Unix/OSX
computer with a Fortran compiler". The nightly test matrix runs on Linux clusters, and macOS laptops
appear as commit hosts in the repository history.

`Windows` is therefore excluded on an explicit first-party statement rather than for lack of
evidence. `Solaris` is not claimed by any source. `Other` was considered as a catch-all for
non-Linux, non-macOS UNIX variants and rejected as speculative — the two named platforms are the ones
the project actually supports and tests.

### 21. CPU Architecture (RECOMMENDED)
- GPU
- HPC or HEC
- x86-64

*Source note:*

- **HPC or HEC** — the manual: "to do most physically meaningful runs the SWMF requires a parallel
  processor machine with a minimum of 8 processors and a minimum of 8GB of memory. Very large runs
  require many more processors." Job scripts for named supercomputers ship in `share/JobScripts/` and
  are copied into a run directory when the machine's hostname matches, and the nightly test matrix
  includes runs on NASA HECC systems.
- **GPU** — the manual: "A significant fraction of the SWMF has been ported to GPUs using the
  OpenACC library." `Makefile.test` defines a `test_gpu` target and passes `OPENACC = -acc` to
  `Config.pl`; GPU-specific parameter files and reference outputs ship
  (`Param/PARAM.in.test.cme.SCIH_gpu`, `output/test9gpu/`); the nightly matrix includes serial and
  parallel `nvfortran` columns; and the University of Michigan page states "Some parts of the SWMF
  can now run on one or more GPUs."
- **x86-64** — the compiler and platform matrix (GNU gfortran, Intel ifort, NAG nagfor, PGI/NVIDIA,
  Absoft, Lahey) and the Intel-based clusters in the nightly test matrix.

Considered and not selected: `ppc64le` — the manual lists IBM `xlf90` and `mpxlc` among supported
compilers, which implies POWER support historically, but no first-party source names a little-endian
POWER target and no current test column covers one. `Apple Silicon arm64` — macOS is supported
(Field 20) and modern Macs are arm64, but no first-party source names the architecture, and the
inference is not evidence. `Linux aarch64 or arm64`, `Sun (SPARC)`, `CPU Independent` and `Other` are
likewise unsupported.

### 22. Related Phenomena (OPTIONAL)
- Coronal Heating
- Coronal Mass Ejections
- Geomagnetic Storms
- Solar Corona
- Solar Wind
- X-ray emission

*Source note:* This vocabulary is closed at seven rows, so the
list below is nearly complete and the one exclusion is stated explicitly.

- **Coronal Heating** — the AWSoM solar corona model is Alfvén-wave-driven; the shipped SC parameter
  files carry heating and radiative-loss variables (`qheat`, `qrad`, `qebyq`, `qparbyq`, `qperpbyq`)
  and a chromosphere/transition-region treatment (`NchromoSi`, the `TR` lookup table).
- **Coronal Mass Ejections** — the EE component is the Eruptive Event generator; the manual lists the
  Gibson-Low and Titov-Démoulin flux rope initiators, the breakout model and STITCH; CME test
  configurations and reference outputs ship (`Param/PARAM.in.test.cme.SCIH`,
  `output/test9/SC_cme_los_soho_c2_*`).
- **Geomagnetic Storms** — the GM/IE/IM configuration is the operational Geospace model, and
  Gombosi et al. (2021) reports its geomagnetic-index skill (§5.9, "Geomagnetic Index Simulations").
- **Solar Corona** — the SC component and its dedicated domain.
- **Solar Wind** — the IH and OH components, and the solar-wind-driven GM configuration.
- **X-ray emission** — the `AiaXrt` instrument-response lookup table is loaded by the shipped
  standard solar tests through `#LOOKUPTABLE` and is named as `NameLosTable` in the documented
  `los tbl` plot example; `hinode:xrt` is one of the documented supported line-of-sight instruments,
  Hinode's XRT being a soft X-ray telescope. The SPECTRUM tool synthesizes EUV and X-ray spectra from
  SWMF output using CHIANTI tables.

**Considered and not selected: `Solar Flares`.** The keyword line of Gombosi et al. (2021) reads
"solar flares and CMEs", which is tempting, but its only flare-specific content is §8.1.2, "Neural
Network Predictions of Solar Flares", presented as a current-and-future direction rather than a
shipped capability. No component models flare energy release or flare emission, and no shipped test
configures one. A phenomenon the software does not simulate does not belong here.

### 23. Development Status (RECOMMENDED)
Active

*Source note:* `Active` on the repostatus.org definition —
reached a stable, usable state and being actively developed. The repository holds 25,786 commits
spanning 2001-03-02 to the pinned revision, which is dated 2026-08-13, the extraction date itself.
Development is continuous rather than release-punctuated (Field 12), so commit activity and the test
record are the meaningful signals rather than a release cadence: the University of Michigan page
states "The SWMF is thoroughly tested every night and the documentation is kept up-to-date", and the
project maintains a public nightly test page reporting a per-test pass matrix across several
compilers and machines. `Inactive`, `Unsupported`, `Abandoned` and
`Moved` are all contradicted by that evidence; `WIP` and `Concept` are contradicted by the span of
operational and community use represented by that commit range.

### 24. Documentation (RECOMMENDED)
https://csem.engin.umich.edu/SWMFTESTS/SWMF/doc/

*Source note:* This is the manual index the University of
Michigan CLaSP page links from the word "documentation" in the sentence "The SWMF is thoroughly
tested every night and the documentation is kept up-to-date". Its durable virtue is that it is not a
static copy: it is served out of the nightly test checkout of `master`, so the manuals published
there are rebuilt from current source rather than pinned to a past release — which matters
particularly for software that issues none (Field 12). It is the served form of the repository's own
`doc/index.html`, and it renders the SWMF user manual (`SWMF.pdf`, which quotes `README.md` verbatim
for the installation instructions this field asks for) together with the git instructions, the IDL
visualization manual, the TIMING utilities manual, the software standard, the physics of the
couplings, the testing procedures, the maintenance manual, and the design and requirements
documents.

Alternatives considered:

- `https://github.com/SWMFsoftware/SWMF/blob/master/README.md` — the installation instructions in
  their source form, but only those; it does not reach the manuals, which are not committed as built
  PDFs for the user manual.
- `https://github.com/SWMFsoftware/SWMF/tree/master/doc` — the documentation directory, but the user
  manual there exists only as LaTeX sources requiring `make PDF`.
- `https://csem.engin.umich.edu/tools/swmf/` — the URL printed in the copyright header of most of
  this repository's source and LaTeX files (64 of the 72 `.f90` files, and 14 of the 17 `.tex` files
  in `doc/Tex/`; of the three exceptions, `SWMF_introduction.tex` carries the nightly-test URL instead
  and the two `PM_*` files are generated ProTeX fragments with no copyright header). It still
  resolves, but its entire content is now a single link forwarding to the
  CLaSP download page, so it documents nothing itself. Worth knowing that it is a live redirect
  rather than a dead link.
- `https://clasp.engin.umich.edu/research/theory-computational-methods/space-weather-modeling-framework/swmf-downloadable-software/`
  — the authoritative access-and-licensing page, and the source of much of this dossier. It is an
  access page rather than documentation, and it has already moved once (it previously sat directly
  under `theory-computational-methods/`), so it is the less stable choice for this field.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
  **Funder Identifier:** https://ror.org/027ka1x80
- **Organization:** U.S. National Science Foundation
  **Funder Identifier:** https://ror.org/021nxhr62

*Source note:* Both organizations are named in the
Acknowledgements of the reference-publication set, which is the authoritative place to look for
funding. Names are given in full rather than as acronyms, and each ROR was confirmed against the ROR
registry (the National Science Foundation's ROR display name is "U.S. National Science Foundation").

NASA support is continuous across the project's life: the manual's own Acknowledgments record that
"The first version of the SWMF was developed at the Center for Space Environment Modeling (CSEM) of
the University of Michigan under the NASA Earth Science Technology Office (ESTO) Computational
Technologies (CT) Project (NASA CAN NCC5-614)", and Gombosi et al. (2021) acknowledges nine
current-era NASA grants. NSF support appears in the same 2021 acknowledgement.

Considered and not selected: the NASA Earth Science Technology Office and the University of Michigan
as separate funder entries. ESTO is a NASA programme office rather than a distinct funding
organization and is captured by the award title in Field 26; the University of Michigan is the
performing institution, recorded through the author affiliations in Field 6.

### 26. Award Title (OPTIONAL)
- **Award Title:** A High-Performance Adaptive Simulation Framework for Space-Weather Modeling (SWMF)
  **Award Number:** NCC5-614
- **Award Title:** NASA DRIVE Science Center
  **Award Number:** 80NSSC20K0600
- **Award Title:** NASA Magnetospheric Multiscale
  **Award Number:** 80NSSC19K0564
- **Award Title:** NASA Living With a Star
  **Award Number:** 80NSSC20K0185
- **Award Title:** NASA Living With a Star
  **Award Number:** 80NSSC20K0190
- **Award Title:** NASA Living With a Star
  **Award Number:** 80NSSC20K1778
- **Award Title:** NASA Living With a Star
  **Award Number:** 80NSSC17K0681
- **Award Title:** NASA Solar System Workings
  **Award Number:** 80NSSC20K0854
- **Award Title:** NASA Heliophysics Supporting Research
  **Award Number:** 80NSSC20K1313
- **Award Title:** National Aeronautics and Space Administration award
  **Award Number:** 80NSSC21K0047
- **Award Title:** NSF PREEVENTS
  **Award Number:** 1663800
- **Award Title:** NSF Space Weather with Quantified Uncertainty
  **Award Number:** PHY-2027555

*Source note:*

The first entry is the founding award, quoted from the manual's Acknowledgments: the work was
performed "under the NASA Earth Science Technology Office (ESTO) Computational Technologies (CT)
Project (NASA CAN NCC5-614)" and "The project was entitled as 'A High-Performance Adaptive Simulation
Framework for Space-Weather Modeling (SWMF)'." The manual also records that the Project Director was
Professor Tamas Gombosi and the Co-Principal Investigators were Professors Quentin Stout and Kenneth
Powell. It is the one award in this list for which a genuine project *title* is on record.

The remaining eleven come from the Acknowledgements of Gombosi et al. (2021), which reads: "This work
was supported by NASA DRIVE Science Center grant 80NSSC20K0600 and NASA MMS grant 80NSSC19K0564,
NASA LWS grants 80NSSC20K0185, 80NSSC20K0190, 80NSSC20K1778 and 80NSSC17K0681, NASA SSW grant
80NSSC20K0854, NASA HSR 80NSSC20K1313, NASA 80NSSC21K0047, the NSF PRE-EVENTS grant 1663800 and NSF
SWQU grant PHY-2027555." The award numbers are quoted from that sentence. The paper gives programme
abbreviations rather than project titles, so each title above is the expanded programme name — the
most faithful title available — except 80NSSC21K0047, which the paper attributes to NASA with no
programme, and which is therefore recorded generically. Every title is well inside the 128-character
limit that applies to this field.

One discrepancy is recorded so a later refresh does not treat it as a new find. Crossref's funding
metadata for the same paper lists a third NSF award, **AGS-1322543**, which does not appear in the
Acknowledgements text. It is omitted here because the acknowledgement section is the authoritative
statement of what funded the work and Crossref's funding block is a derived index. If a future
refresh can read the published version's acknowledgement directly and finds AGS-1322543 there, adding
it would be correct.

A note on how the acknowledgement text was obtained, because it will matter next time: the publisher
site for `10.1051/swsc/2021020` refuses automated requests, and Europe PMC does not index this
journal. The article is gold open access under CC BY and the full text is available as
`arXiv:2105.13227`, which is what the quotations above come from.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2005JA011126 — Tóth, G., Sokolov, I. V., Gombosi, T. I., Chesney, D. R.,
  Clauer, C. R., De Zeeuw, D. L., Hansen, K. C., Kane, K. J., Manchester, W. B., Oehmke, R. C.,
  Powell, K. G., Ridley, A. J., Roussev, I. I., Stout, Q. F., Volberg, O., Wolf, R. A., Sazykin, S.,
  Chan, A., Yu, B., & Kóta, J. (2005). Space Weather Modeling Framework: A new tool for the space
  science community. *Journal of Geophysical Research: Space Physics*, 110, A12226.
- https://doi.org/10.1051/swsc/2021020 — Gombosi, T. I., Chen, Y., Glocer, A., Huang, Z., Jia, X.,
  Liemohn, M. W., Manchester, W. B., Pulkkinen, T., Sachdeva, N., Al Shidi, Q., Sokolov, I. V.,
  Szente, J., Tenishev, V., Toth, G., van der Holst, B., Welling, D. T., Zhao, L., & Zou, S. (2021).
  What sustained multi-disciplinary research can achieve: The space weather modeling framework.
  *Journal of Space Weather and Space Climate*, 11, 42.

*Source note:* Both DOIs, titles, journals and author lists were
verified through Crossref.

Tóth et al. (2005) is the paper that introduced SWMF; its author list is effectively the framework's
original authorship and corroborates the credits in the manual. Gombosi et al. (2021) is the most
recent comprehensive account of the framework and is the source for this dossier's statements about
operational deployment at NOAA/SWPC and CCMC, the planetary and astrospheric applications, and the
current funding. Tóth et al. (2012) is not repeated here because it is Field 14.

Considered and not selected: the several hundred papers that use SWMF results. This field is for
publications the developers prioritize; an unfiltered citation list would carry no information. The
three papers above are the ones the project's own documentation and website point to.

### 28. Related Datasets (OPTIONAL)
Not found

*Source note:* SWMF is a simulation framework: it consumes observational drivers and produces
simulation output, but the distribution is not built around any particular archived dataset, and no
first-party source designates one. Many third-party Zenodo deposits archive the *output* of specific
SWMF runs (simulation results for named storms, ensemble studies, input files for particular events);
these are products of individual studies rather than datasets SWMF supports, and listing a selection
of them would misrepresent the software.

The observational data streams SWMF does consume are recorded where they belong: the retrieval
services in Field 17, the missions in Field 32, and the formats in Field 18.

### 29. Related Software (OPTIONAL)
- https://github.com/SWMFsoftware/BATSRUS — BATS-R-US, the block-adaptive extended-MHD code that
  implements the EE, SC, IH, OH and GM components
- https://github.com/SWMFsoftware/BATL — Block Adaptive Tree Library, the AMR infrastructure beneath
  BATS-R-US
- https://github.com/SWMFsoftware/share — the shared library, scripts, job scripts and IDL, Python,
  MATLAB and Julia tooling; cloned by `Config.pl` before it can configure anything
- https://github.com/SWMFsoftware/util — the shared utilities, including TIMING, NOMPI and the
  empirical models
- https://github.com/SWMFsoftware/GITM2 — Global Ionosphere Thermosphere Model, the UA component
- https://github.com/SWMFsoftware/CIMI — Comprehensive Inner Magnetosphere-Ionosphere model, an IM
  component that also covers radiation-belt electrons
- https://github.com/SWMFsoftware/RCM2 — Rice Convection Model version 2, an IM component
- https://github.com/SWMFsoftware/HEIDI — Hot Electron Ion Distribution Ionosphere model, an IM
  component
- https://github.com/lanl/RAM-SCB — Ring current-Atmosphere interactions Model with Self-Consistent
  magnetic field, an IM component developed at Los Alamos
- https://github.com/SWMFsoftware/RBE — Radiation Belt Environment model, the RB component
- https://github.com/SWMFsoftware/RIM — Ridley Ionosphere Model, the parallel IE component
- https://github.com/SWMFsoftware/Ridley_serial — the original serial Ridley ionosphere
  electrodynamics model, the other IE component
- https://github.com/SWMFsoftware/DGCPM — Dynamic Global Core Plasma Model, the PS component
- https://github.com/SWMFsoftware/FLEKS — Flexible Exascale Kinetic Solver, the primary PC component
  and an alternative PT component
- https://github.com/SWMFsoftware/AMPS — Adaptive Mesh Particle Simulator, the PT component and an
  alternative PC component
- https://github.com/SWMFsoftware/MITTENS — MITTENS (Monte carlo Integration of Turbulent Transport
  and ENergization of Solar energetic particles), an alternative PT component
- https://github.com/SWMFsoftware/MFLAMPA — Multiple Field Line Advection Model for Particle
  Acceleration, an SP component
- https://github.com/SWMFsoftware/KotaSEP — Kóta's solar energetic particle model, the other SP
  component
- https://github.com/SWMFsoftware/FSAM — the convection-zone model behind the CZ component
- https://github.com/SWMFsoftware/FDIPS — Finite Difference Iterative Potential-field Solver, which
  produces the potential-field solution from a magnetogram used to initialize solar corona runs

*Source note:* These are SWMF's physics components and mandatory
libraries — the most distinguishing "important software dependencies" the field could carry, since
the framework produces no science at all without at least one of them. The component-to-model mapping
is taken directly from the `%component` hash in `Config.pl`, whose thirteen keys are `BATSRUS`,
`Ridley_serial`, `CIMI`, `HEIDI`, `RCM2`, `FLEKS`, `FLEKS_PT`, `AMPS_PT`, `MITTENS`, `PWOM`, `RBE`,
`MFLAMPA` and `MGITM`, each mapped to its component slot, and from the component descriptions in the
manual's Acknowledgments.

Every one of those thirteen keys is now accounted for here: eleven are listed above, either under
their own name or under the model they name (`FLEKS_PT` and `AMPS_PT` are the PT-slot configurations
of `FLEKS` and `AMPS`, not separate software), and `PWOM` and `MGITM` are omitted for the reason
given below.

**MITTENS** is easy to miss and was: it is the only `%component` key with no counterpart in the
manual's Acknowledgments, so a reading that leans on the manual passes over it. The repository
evidence is unambiguous — `Config.pl` line 50 maps `"MITTENS" => "PT"`; `Makefile.test` ships a
standard test for it (line 60 advertises `test14 (run SC-IH-PT/MITTENS test)` and line 2060
configures the run as `./Config.pl -default -v=Empty,SC/BATSRUS,IH/BATSRUS,PT/MITTENS`); and
`.gitignore` line 134 lists `PT/MITTENS/` among the installed-component paths. `SWMFsoftware/MITTENS`
is public, actively maintained, neither archived nor a fork, and carries the standard SWMF component
layout (`Config.pl`, `PARAM.XML`, `Param/`, `src/`, `srcInterface/`) under the same Apache-2.0
licence as the rest of the distribution.

Two further entries are attributed elsewhere because neither of those sources names them, and a
future refresh should not go looking for them there. **DGCPM** is placed in the PS slot on the authority of
its own `PARAM.XML`, whose root element is `<commandList name="DGCPM: PS Component">`. **FSAM** is
placed behind the CZ component on the authority of its own `README`, which describes running "a
convective dynamo simulation" and documents output "relative to a time independent 1D reference state
of the convection zone (CZ)". **FDIPS** is included on the strength of the University of Michigan
page, which distributes it in the same section as SWMF as the magnetogram-to-potential-field step.

Deliberately omitted, with reasons:

- **PWOM** (Polar Wind Outflow Model, the PW component), **MGITM** (the Mars GITM variant) and the
  SWMF build of **iPIC3D** are named by `Config.pl` and by the manual but have no public repository
  in the organization; they are reachable only through registered access. There is nothing to link
  to. FLEKS has superseded iPIC3D as the main PIC model in any case.
- **MSTEM-QUDA**, the former non-commercial open-source subset of SWMF, has been retired: its GitHub
  organization now publishes no repositories and its description directs users to
  `github.com/SWMFsoftware`. Linking to it would send readers to an empty shell. This is worth
  knowing because both the 2024 version of the University of Michigan page and the third-party Zenodo
  record rejected in Field 2 still refer to it.
- **Similar-purpose global magnetosphere and heliosphere models** — OpenGGCM, GAMERA, LFM, Enlil and
  their peers — would fit this field's "software that performs similar tasks" wording, but no
  first-party SWMF source asserts a relationship with any of them, and choosing which to name would
  be editorial judgement rather than evidence. They are left out; a curator who wants comparative
  links can add them deliberately.
- **AMREX** and **HYPRE** are present in the organization as vendored third-party numerical
  libraries (AMR framework and algebraic multigrid solver). They are build dependencies of individual
  components rather than software that characterizes SWMF.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/SWMFsoftware/swmfpy — swmfpy, the SWMF team's Python library
- https://github.com/spacepy/spacepy — SpacePy
- https://github.com/nasa/Kamodo — Kamodo
- https://github.com/henry2004y/Batsrus.jl — Batsrus.jl
- https://github.com/henry2004y/VisAnaMatlab — VisAna for MATLAB
- https://github.com/esmf-org/esmf — Earth System Modeling Framework
- https://www.lmsal.com/solarsoft/ — SolarSoft (SSW)

*Source note:* Each entry names the specific exchange that
qualifies it; none is included merely for being a dependency or an ecosystem member.

- **swmfpy** — the project's own Python companion library, distributed from the same GitHub
  organization. `share/Python/Scripts/prepare_geospace.py` imports `write_imf_from_omni`, `paramin`
  and `web.get_omni_data` from it to construct SWMF's `IMF.dat` solar-wind driver and to rewrite the
  F10.7 value inside `PARAM.in`; `share/Python/install-swmfpy` installs it. Concept DOI
  `https://doi.org/10.5281/zenodo.5659248`.
- **SpacePy** — named by SWMF's own manual as one of the packages its output is designed for: "the
  SWMF output is typically visualized using IDL, Tecplot, python (SpacePy), VisIt, Paraview or yt.
  Other visualization packages may also be used, but the output file formats and scripts have been
  designed for these visualization softwares." SpacePy's `pybats` module reads SWMF and BATS-R-US
  output, and the PyHC registry lists `swmf` and `bats_r_us` among SpacePy's keywords.
- **Kamodo** — NASA's model-output functionalization package ships dedicated SWMF readers
  (`swmfgm_4D.py`, `swmfie_4Dcdf.py`, `swmfie_tocdf.py`, `swmf_gm_octree.py`) plus GITM readers, so
  SWMF output can be consumed directly; the PyHC registry lists `swmf` and `gitm` among its keywords.
- **Batsrus.jl** — `share/Julia/README.md` states "A Julia package Batsrus.jl is provided for
  processing SWMF data" and supplies `gitclone Batsrus.jl` for installation. The repository describes
  itself as the "BATSRUS/SWMF Data Processor". Gombosi et al. (2021) names it, as VisAnaJulia, among
  the open-source tools around SWMF (§8.3, "Open-source Development").
- **VisAna for MATLAB** — `share/MATLAB/README.md` states "This package contains the reader for all
  kinds of output data from SWMF", making it the MATLAB-side reader for SWMF output.
  Gombosi et al. (2021) names it as VisAnaMatlab (§8.3, "Open-source Development").
- **Earth System Modeling Framework** — SWMF ships an ESMF wrapper in `ESMF/ESMF_SWMF/` that builds
  "a sample ESMF application which couples the SWMF subcomponent with one (or more) ESMF
  subcomponents"; the shipped configuration couples SWMF to the Ionosphere Plasmasphere
  Electrodynamics model through ESMF (`ESMF_SWMF.input.realIPE`, `IPE_grid_comp.f90`,
  `IPE.inp`). `gitclone ESMF` installs the library and `make -j test_esmf` is a shipped test target.
  The manual records the coupling as a major improvement: "The SWMF has been coupled to the Earth
  System Modeling Framework (ESMF)."
- **SolarSoft (SSW)** — the IDL analysis suite the SWMF comparison scripts run inside.
  `share/IDL/Solar/README` instructs users to source `setenv_insitu.sh` / `setenv_remote.sh`, which
  "will set up the SSW environment and start SSW", before running `compare_insitu` or
  `compare_remote`; `share/IDL/Solar/README_EIT` states that "the Solar SoftWare Idl package (SSW)
  must be installed, up to date and properly loaded/linked in IDL for this to work properly. The
  additional SSW packages needed are SOHO/EIT, and VSO." The link is to the SolarSoft home page
  because the suite is distributed as a mirrored instrument-tree rather than from a single canonical
  source repository.

Deliberately excluded: MPI, OpenMP, OpenACC, HDF5 and SPICE. Each is a genuine dependency, and SPICE
in particular is a real domain library, but they are numerical and I/O infrastructure invoked
internally rather than peer tools a user deliberately combines with SWMF; the same entry would read
identically for most parallel simulation codes. IDL, Tecplot, VisIt, Paraview and yt are named
alongside SpacePy in the manual sentence quoted above, but as generic visualization applications
rather than packages with an SWMF-specific exchange; SpacePy is singled out because it implements a
reader for SWMF's formats.

### 31. Related Instruments (OPTIONAL)
- **Atmospheric Imaging Assembly** — https://spase-metadata.org/SMWG/Instrument/SDO/AIA
- **Extreme UltraViolet Imager on the STEREO-A mission** — https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/EUVI
- **Extreme UltraViolet Imager on the STEREO-B mission** — https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/EUVI
- **STEREO-A SECCHI Cor1 Coronagraph** — https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/Cor1
- **STEREO-A SECCHI Cor2 Coronagraph** — https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI/Cor2
- **STEREO-B SECCHI Cor1 Coronagraph** — https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/Cor1
- **STEREO-B SECCHI Cor2 Coronagraph** — https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI/Cor2
- **Large Angle Spectroscopic Coronagraph** — https://spase-metadata.org/SMWG/Instrument/SOHO/LASCO
- **Extreme Ultraviolet Imaging Telescope** — https://spase-metadata.org/SMWG/Instrument/SOHO/EIT
- **X-Ray Telescope** — https://spase-metadata.org/SMWG/Instrument/Hinode/XRT

*Source note:* Every entry carries a resolved
`https://spase-metadata.org/` identifier; none is a free-typed name.

**Why a coupled-model framework has instrument associations at all.** SWMF is not
instrument-agnostic in its solar configuration. Its line-of-sight plot area synthesizes images *as a
named instrument would record them*, using that instrument's own response table and viewing geometry,
and the distribution ships tooling that downloads and calibrates the corresponding real observations
for direct comparison. Both directions are instrument-specific by construction.

The decisive evidence is the enumerated list of supported instruments in the `#SAVEPLOT` command
description in BATS-R-US's own `PARAM.XML` — the file the manual points users to at
`GM/BATSRUS/PARAM.XML` once the component is installed. Describing the `los`/`ins` plot option, it
states "The supported combinations are:" and lists

```
Stereo A:    sta:euvi, sta:cor1, sta:cor2
Stereo B:    stb:euvi, stb:cor1, stb:cor2
SDO:         sdo:aia
Hinode:      hinode:xrt
SOHO:        SOHO:c2, SOHO:c3
```

Nine of the ten instruments above are drawn directly from that list. The tenth, SOHO/EIT, is
supported through a response table rather than an `ins` shorthand and is justified separately below.
This is an explicit specification of supported instruments, not an inference from example data.

Corroborating first-party evidence:

- The shipped standard test parameter files configure these instruments by name:
  `sta:euvi stb:euvi sdo:aia` and `soho:c2 soho:c3 sta:cor1 sta:cor2 stb:cor1 stb:cor2` appear as
  `StringsInstrument` values across `Param/PARAM.in.test.start.SCIH`,
  `Param/PARAM.in.test.restart.SCIH`, `Param/PARAM.in.test.cme.SCIH` and their GPU variants.
- The expected results of those runs are committed to the repository:
  `output/test9/SC_los_sdo_aia_6_n0000010.out.gz`, `output/test9/SC_los_sta_euvi_4_n0000010.out.gz`,
  `output/test9/SC_los_stb_euvi_5_n0000010.out.gz` and
  `output/test9/SC_cme_los_soho_c2_4_t00000010_n0000012.out`. Synthetic instrument images are part of
  the framework's verified behaviour, not an optional extra.
- Instrument response tables are loaded through `#LOOKUPTABLE` in those same tests: `EuviA` from
  `SC/Param/los_EuviA.dat`, `EuviB` from `SC/Param/los_EuviB.dat`, `euv` from
  `SC/Param/los_Eit_cor.dat`, and `AiaXrt` from `SC/Param/los_tbl.dat`.
- On the observation side, `share/IDL/Solar/` supplies `compare_AIA.pro`, which compares the
  synthesized image against observations in the seven AIA passbands 94, 131, 171, 193, 211, 304 and
  335 Å and delegates retrieval to the `download_images` procedure in `procedures_local.pro`, where
  the query `vso_search(date=…, source='SDO', det='aia', wave='94-335 Angstrom')` is issued;
  `compare_EUV.pro`, `compare_wl.pro`, `WL_compare_C2.pro`, `WL_compare_C3.pro`,
  `download_WL_obs.pro` ("used to download SOHO/LASCO C2, C2, STEREO A/B COR1, COR2 white light
  coronagraph images and make movies", with per-instrument download flags), and `get_eit_set.pro`,
  whose README describes "an automated way of getting and calibrating SOHO EIT images for comparing
  three filter sets to the SWMF euv synthesis".

Resolution notes:

- `soho:c2` and `soho:c3` are the two LASCO coronagraph telescopes. The vocabulary carries one LASCO
  row, so both map to it and it is recorded once.
- SOHO/EIT is supported through the `euv` response table rather than through an `ins` shorthand;
  the `#SAVEPLOT` documentation names it explicitly when explaining response tables ("the EUV or SXR
  instument (e.g. SOHO EIT, STEREO EUVI, Yohkoh SXT)"), the table ships and is loaded by the standard
  tests, and `get_eit_set.pro` handles the observational side.
- `X-Ray Telescope` is the vocabulary's name for Hinode's XRT; the row was matched on the
  `Hinode/XRT` identifier path, not on the name alone, because Yohkoh's soft and hard X-ray
  telescopes carry different names.

Considered and not selected, with reasons:

- **Michelson Doppler Imager (SOHO/MDI)**, `https://spase-metadata.org/SMWG/Instrument/SOHO/MDI`, and
  **the Global Oscillation Network Group**, `https://spase-metadata.org/SMWG/Observatory/GONG`. The
  repository ships MDI-derived and GONG-derived synoptic magnetogram inputs
  (`Param/CR1922_MDI.dat`, `Param/CR2039_MDI.dat`, `Param/CR1935_MDI_order90.dat`, and
  `SC/Gong_harmonics.dat` and `SC/Param/CR1962_MDI.dat` referenced from the standard tests), and the
  ADAPT map `Param/map_04.out` records `InstrumentName = GONG` in its header. These are excluded
  because SWMF's magnetogram reader is format-based and instrument-agnostic: it consumes a spherical
  harmonic coefficient file or an ADAPT-style map, and MDI, GONG, HMI, WSO and ADAPT products are
  interchangeable inputs to it. The shipped files are example data illustrating a generic capability,
  which the relevance guidance directs to the file-format and data-source fields rather than here.
- **Wilcox Solar Observatory**, the source of `Param/CR1935_WSO.dat`. Excluded for exactly the same
  substantive reason as MDI and GONG: the magnetogram reader is format-based and instrument-agnostic,
  and the shipped file is example data illustrating a generic capability rather than support for a
  particular magnetograph. It *does* resolve, and both identifiers are recorded here so a future
  refresh need not rediscover them — the vocabulary files WSO under its abbreviation rather than its
  spelled-out name, which is why a search for "Wilcox" finds nothing: the observatory is `WSO`,
  `https://spase-metadata.org/SMWG/Observatory/WSO`, and the instrument is
  `WSO Babcock solar magnetograph`, `https://spase-metadata.org/SMWG/Instrument/WSO/Babcock`.
- **Soft X-Ray Telescope on Yohkoh**, `https://spase-metadata.org/SMWG/Instrument/Yohkoh/SXT`. The
  `#SAVEPLOT` documentation mentions it as an example of an SXR instrument whose response table can
  be loaded, and names an `SC/Param/los_Sxt.dat` table, but it is absent from the enumerated list of
  supported `StringsInstrument` combinations and no shipped test loads that table. Recorded with its
  identifier so a future refresh can act quickly if the evidence changes.
- **SuperMAG Magnetometers**, `https://spase-metadata.org/SMWG/Instrument/SuperMAG/Magnetometers`.
  `Param/supermag.dat` lists SuperMAG station names and coordinates for SWMF's `#MAGNETOMETER` output,
  which writes simulated ground magnetic perturbations at those locations. Excluded because the
  reader is a generic station-list parser: `Param/magnetometer_location.dat` uses the identical format
  with three invented stations, so any station list works and nothing is specific to SuperMAG.
- **Advanced Composition Explorer** and other upstream solar wind monitors. `Param/SWPC/IMF.dat`
  drives the operational Geospace configuration with measured solar wind, but the file format is a
  plain time series and no first-party source names the spacecraft that supplied it. The retrieval
  path that does exist goes through OMNI, which is a merged multi-spacecraft product and is recorded
  in Field 17.

### 32. Related Observatories (OPTIONAL)
- **Solar Dynamics Observatory** — https://spase-metadata.org/SMWG/Observatory/SDO
- **Solar and Heliospheric Observatory** — https://spase-metadata.org/SMWG/Observatory/SOHO
- **Solar Terrestrial Relations Observatory A** — https://spase-metadata.org/SMWG/Observatory/STEREO-A
- **Solar Terrestrial Relations Observatory B** — https://spase-metadata.org/SMWG/Observatory/STEREO-B
- **Hinode** — https://spase-metadata.org/SMWG/Observatory/Hinode
- **Parker Solar Probe** — https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe
- **Solar Orbiter** — https://spase-metadata.org/ESA/Observatory/SolarOrbiter

*Source note:* Every entry carries a resolved
`https://spase-metadata.org/` identifier and each `name` is the matched row's own name.

SDO, SOHO, STEREO-A, STEREO-B and Hinode are the platforms of the instruments in Field 31 and are
named as such in the `#SAVEPLOT` supported-instrument list quoted there.

Parker Solar Probe and Solar Orbiter are listed on separate, equally direct evidence: SWMF's in-situ
comparison workflow retrieves each mission's own merged magnetic-field and plasma dataset by name and
compares it against SWMF virtual-satellite output extracted along that spacecraft's trajectory.
`share/IDL/Solar/compare_insitu.pro` iterates over `TypeADAPT_I = ['earth', 'sta', 'stb', 'solo',
'psp']`, and `get_insitu_data` in `share/IDL/Solar/procedures_local.pro` requests
`PSP_COHO1HR_MERGED_MAG_PLASMA` and `SOLO_COHO1HR_MERGED_MAG_PLASMA` (alongside
`STA_`/`STB_COHO1HR_MERGED_MAG_PLASMA` and OMNI), with per-mission error messages naming "Parker
Solar Probe" and "Solar Orbiter". The `#SATELLITE` command in the shipped solar tests reads
`SC/TRAJECTORY/earth.dat`, `sta.dat` and `stb.dat` to produce the model side of that comparison.

Resolution notes. Three of the seven names collide with more than one row in the vocabulary, and each
collision was broken deliberately:

- **Solar and Heliospheric Observatory** matches two rows, `SMWG/Observatory/SOHO` and
  `CNES/Observatory/CDPP-AMDA/SOHO`. The SMWG row was taken as the tie-breaker among same-name
  duplicates.
- **Parker Solar Probe** matches three rows, `SMWG/Observatory/ParkerSolarProbe`,
  `CNES/Observatory/CDPP-AMDA/PSP` and `CNES/Observatory/CDPP-Archive/PSP`. Same tie-breaker, same
  outcome.
- **Solar Orbiter** matches two rows, `ESA/Observatory/SolarOrbiter` and
  `CNES/Observatory/CDPP-AMDA/SolO`. Neither is an SMWG row, so that tie-breaker does not apply here.
  `ESA/Observatory/SolarOrbiter` was chosen because it is the mission-operating agency's own SPASE
  catalog entry for its own mission, whereas the CNES row is an archive-side listing of the same
  mission.

The two STEREO spacecraft do **not** collide: `Solar Terrestrial Relations Observatory A` and
`Solar Terrestrial Relations Observatory B` each match exactly one row. The CNES archive does carry
STEREO entries, but under different names (`STEREO-A`, `STEREO Ahead`, and their B counterparts), so
they are not same-name duplicates of the rows recorded here.

`Solar-Terrestrial Relations Observatory` (`SMWG/Observatory/STEREO`) is the mission-level row and was
not used, because the software distinguishes the two spacecraft throughout — separate response
tables, separate trajectory files, separate datasets — so the per-spacecraft rows carry the real
information.

Considered and not selected: the Global Oscillation Network Group and the Wilcox Solar Observatory,
for the magnetogram reasons recorded under Field 31. Also considered and rejected: reading the
operational NOAA Space Weather Prediction Center deployment or the CCMC runs-on-request service as
observatory associations — they are service and deployment relationships, not missions whose data
SWMF is designed to support, and the vocabulary is a mission and observatory list.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/SWMFsoftware/SWMF/127a73cb13951351d60e7936583f69f39bd0272e/doc/Logo/SWMF-Logo-Color-LightBG-Horizontal.png

*Source note:* `doc/Logo/` holds the project's official logo set
in colour and greyscale, for light and dark backgrounds, in horizontal, stacked and wordmark
arrangements, with and without the CSEM lockup, together with `SWMF_Logo_Guide.pdf`. The
`doc/Logo/README` records that "The logo was designed by Matthew Sturm graphics designer" and that
the logos "are copyrighted and should not be modified in any way", so the URL points at the
unmodified file as committed — pinned to that commit rather than to the `master` branch, which also
means the copyright-bearing asset the catalogue displays cannot be silently substituted upstream. The
colour, light-background, horizontal variant without the lockup was chosen as the most legible against
a light catalogue page.

The alternative `doc/Tex/SWMF_logo.png` is the manual's title-page image, kept in the LaTeX source
tree rather than in the maintained logo set, so it is the less appropriate reference.

---

## Agreement
Metadata submitted for this record is contributed to the public domain per the HSSI submission terms.
