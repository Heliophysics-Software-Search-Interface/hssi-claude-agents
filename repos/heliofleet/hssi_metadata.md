# HSSI Metadata Extraction Results

**HSSI Software ID:** 60843aa5-1bf5-40ca-a72c-6b1c895e7596
**Repository:** https://github.com/sr-dash/heliofleet
**Source Revision:** de4b623b0b0692354e2ca35166c24c5e68edccda
**Extraction Date:** 2026-11-06
**Validation Date:** 2026-11-06
**Validation Status:** PASS

---

## Scope note

HelioFleet is a static web application, served from the repository by GitHub Pages at
https://sr-dash.github.io/heliofleet/. The pinned tree holds two kinds of code, and the field notes say
which one each piece of evidence comes from:

- **The browser application** (`index.html`, `sky.html`, `help.html`, `methods.html`, `js/`, `css/`).
  The coordinates, geometry, searches, fields of view and maps a visitor sees are computed in the
  browser. The page reads its data from files the repository itself serves (`data/`, `i18n/`); the SDO
  context images of the sky view's observation panel are requested from the Helioviewer API at run time
  (`js/observations.js:134`).
- **The data pipeline** (`scripts/*.py`), run monthly by `.github/workflows/update-ephemeris.yml` and
  documented in the README for local use. It is the code that reads JPL Horizons, NASA DONKI, JSOC, the
  LMSAL Heliophysics Coverage Registry, the Hinode/EIS as-run catalogue, the DKIST Data Center and the
  Solar Orbiter Archive, and writes the files under `data/`. Two products are computed here rather
  than in the browser: the calendar of upcoming perihelia, alignments, quadratures and conjunctions
  (`scripts/build_calendar.py`) and the coordinated-observation groups
  (`scripts/fetch_observations.py`).

Unqualified file citations are at the Source Revision. The newest release is v1.1.2 (2026-10-30); the
eight commits between that tag and the Source Revision (2026-10-30 to 2026-11-05) are unreleased: the
1.1.2 version DOI added to the citation files, two monthly data updates, workflow maintenance, an
accessible date picker and back-to-top buttons, and README and footer requests for feedback. None of
them adds or removes a capability that any field below records, so the pinned tree and the v1.1.2
release support the same values.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]
- **Note:** HSSI does not publish an existing record's submitter, and no repository file, DOI record or
  registry identifies who submitted this entry, so the placeholder is the settled value (Field 1
  rule 6). The author's commit address in the git history identifies the author, not the submitter
  (rule 2).

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.23328187

- **Source:** From the submitted HSSI record; confirmed as the software's Zenodo **concept** DOI.
- **Concept, not version (Field 2 rule 5, kept under rule 9):** DataCite's record for
  `10.5281/zenodo.23328187` is `resourceTypeGeneral` Software and carries four `HasVersion` relations:
  `10.5281/zenodo.23328188` (v1.0.0), `10.5281/zenodo.23330591` (1.1.0), `10.5281/zenodo.23752828`
  (1.1.1) and `10.5281/zenodo.23818629` (1.1.2). Each of those version records names
  `10.5281/zenodo.23328187` as its `conceptdoi` at Zenodo and carries `IsVersionOf` it at DataCite. The
  project's own files cite the same DOI as the all-versions identifier: `CITATION.cff` `doi:` and its
  `identifiers` entry described as "All versions (resolves to the latest release)", the README DOI badge
  (`README.md:3`), and the README citation section ("That DOI always resolves to the latest release.").
- **Identity:** every deposit's title and creator match the project (`HelioFleet: an interactive map of
  heliophysics spacecraft positions`, Dash, Soumyaranjan, ORCID 0000-0003-0103-6569), Zenodo's
  `code:codeRepository` on each version is `https://github.com/sr-dash/heliofleet`, each deposit's file
  is named `sr-dash/heliofleet-v<version>.zip`, and each deposit was created seconds after the matching
  GitHub release was published (v1.0.0: release 2026-10-12T23:38:11Z, deposit 2026-10-12T23:38:15Z).
  These are GitHub–Zenodo integration deposits. They carry no `IsSupplementTo …/tree/<tag>` relation;
  their one URL relation is `IsDocumentedBy` the live site, which `.zenodo.json` declares.
- **What the citation shows:** the concept currently presents version 1.1.2 (DataCite `version`), the
  same release Field 12 records.
- **Other concept DOIs:** a Zenodo creator-keyed search on the author's ORCID returned five records on
  2026-11-06; the only HelioFleet concept among them is this one (the others are HelioField, HelioField imagery and two
  SFT-1D deposits), so Field 2 rule 7 does not arise.
- The version DOI of 1.1.2 belongs to Field 12's Version PID, not here.

### 3. Code Repository (MANDATORY)
https://github.com/sr-dash/heliofleet

- **Source:** From the submitted HSSI record; matches the GitHub API `full_name` `sr-dash/heliofleet`
  (not archived, not a fork), `CITATION.cff` `repository-code`, and Zenodo `code:codeRepository`
  (Field 3 rule 7).
- **Considered and not used:** the live site https://sr-dash.github.io/heliofleet/ is where a user runs
  the software, but the source is public, so the repository is the value (rule 2); the site is Field 24.

---

## Section 2: Software Classification and Description

### 4. Software Functionality (RECOMMENDED)
- **Values (in stored order, new members inserted after their family's stored members):**
  - Coordinate Transforms: Solar
  - Coordinate Transforms
  - Coordinate Transforms: Heliospheric
  - Data Visualization
  - Mission-related: Operations
  - Mission-related
  - Data Processing and Analysis: Data Access and Retrieval
  - Data Processing and Analysis
  - Data Processing and Analysis: Analysis
  - Data Visualization: 2D Graphics
  - Data Visualization: 3D Graphics
  - Data Visualization: Movies
  - Data Visualization: Orbit Plots
  - Data Visualization: Spacecraft Formation Plots
  - Data Visualization: Web-Based
  - Models and Simulations
  - Models and Simulations: Field-line Tracing
  - Models and Simulations: Observatory/Instrument Models
- **Submitted value:** `Coordinate Transforms: Solar`, `Data Visualization`,
  `Mission-related: Observatory/Instrument Models`, `Mission-related: Operations`,
  `Data Processing and Analysis: Data Access and Retrieval`, `Data Visualization: 2D Graphics`,
  `Data Visualization: 3D Graphics`. Four of its children, in three families (`Coordinate
  Transforms: Solar`, both `Mission-related` children, `Data Processing and Analysis: Data Access and
  Retrieval`), were stored without their parent rows, which leaves those families' top-level categories
  off the detail page and out of name searches (rule 10).
- **Kept from the submitted record, with evidence:**
  - `Coordinate Transforms: Solar` — `heliographic()` (`js/frames.js:48`) converts heliocentric
    ecliptic J2000 vectors to Stonyhurst and Carrington longitude and latitude under the IAU solar
    rotation model, and the user receives them in the coordinate table and its CSV/JSON
    (`js/tools.js:18`, columns `hgs_lon_deg`, `hgs_lat_deg`, `carrington_lon_deg`). "Who sees this
    spot" accepts a Carrington or Stonyhurst location (`surfaceNormal`, `js/frames.js:64`), and the sky
    view carries Solar Orbiter's helioprojective footprints into Earth's view (`js/observations.js`,
    `hpcDirection` in `js/skyproj.js:65`).
  - `Data Visualization` — the whole application is a visualization (below).
  - `Mission-related: Operations` — kept by the curator's decision recorded below.
  - `Data Processing and Analysis: Data Access and Retrieval` — `timeSeries` (`js/tools.js:92`) gives
    the user ephemeris time series for chosen bodies, dates and cadence; the generated SunPy scripts
    retrieve positions from JPL Horizons (`get_horizons_coord`, `js/tools.js:130`) and AIA or HMI FITS
    images from JSOC through `Fido` (`js/sky.js:983-991`); the observation list links each observation
    to its data.
  - `Data Visualization: 2D Graphics` — the canvas map (`drawMap`, `js/render.js:118`) and the solar
    surface map over HMI synoptic magnetograms (`drawSurface`, `js/coverage.js:233`).
  - `Data Visualization: 3D Graphics` — kept on a fair reading of the code (rule 14): the 3D
    heliocentric configuration is rendered from ecliptic north and edge-on to show orbital inclination
    (`project`, `js/frames.js:134`; edge-on grid at `js/render.js:170`), and the sky view places bodies
    in true perspective (`js/skyproj.js:5`). There is no freely rotatable 3D scene; the "coronal magnetic
    field in 3D" the navigation bar links to is the separate HelioField (Field 30). Removing the value
    would need evidence it is wrong, not that it is imprecise.
- **Added (rule 10, the missing parents):** `Coordinate Transforms`, `Mission-related` and
  `Data Processing and Analysis` beside their stored children, and `Models and Simulations` for the new
  family below.
- **Added (rule 12, evidenced capabilities the record lacked):**
  - `Coordinate Transforms: Heliospheric` — `toFrame` (`js/frames.js:124`) rotates the map between
    Heliocentric Earth Ecliptic and inertial ecliptic J2000, a frame the user selects (README "Two
    frames"); exports carry heliocentric ecliptic J2000 x, y, z (`js/tools.js:18`).
  - `Data Processing and Analysis: Analysis` — derived physical quantities: heliocentric speed, light
    time and apparent Sun size (`liveFacts`, `js/bodyinfo.js:15`), perihelia (`js/bodyinfo.js:37`),
    light-time offset, apparent solar radius, B0 and L0 per observer (`geometryRows`,
    `js/tools.js:175`), searches for radial alignments, quadratures and magnetic connections
    (`findAlignments`, `js/tools.js:257`), and the angle from disk centre and μ of a solar location
    from every observer (`visibility`, `js/tools.js:311`).
  - `Data Visualization: Movies` — `recordAnimation` (`js/animate.js:32`) records a date range as MP4,
    WebM or GIF.
  - `Data Visualization: Orbit Plots` — trajectory trails, "past solid and fading, future dotted"
    (`js/render.js:261`).
  - `Data Visualization: Spacecraft Formation Plots` — the map and the near-Earth L1 inset display the
    configuration of the multi-spacecraft fleet relative to the Sun and Earth, with the alignment,
    quadrature and connection geometry between spacecraft; this is the vocabulary's multi-spacecraft
    configuration display.
  - `Data Visualization: Web-Based` — an interactive browser application (`index.html`, `sky.html`),
    also embeddable in other sites with `embed=1` (README "Embedding").
  - `Models and Simulations: Field-line Tracing` — `parkerSpiral` (`js/frames.js:95`) draws
    Parker-spiral field lines through Earth and each spacecraft for a chosen solar-wind speed, and
    `footpointLon` (`js/frames.js:89`) follows each spiral to its footpoint on the solar surface; the
    magnetic-connection search uses the same footpoints.
  - `Models and Simulations: Observatory/Instrument Models` — the fields of view of 20 coronagraph and
    heliospheric-imager channels are modelled from published elongation ranges (`INSTRUMENTS`,
    `js/instruments.js:29`; projected onto an observer's plane of the sky by `SKY_SHAPES`, `fovFrame`
    and `inField`, `js/skyproj.js:20`, `:90`, `:108`), and the ground coronagraphs K-Cor and UCoMP are
    modelled the same way (`GROUND`, `js/skyproj.js:35`). The README says "Heliospheric imagers are
    modelled as fields of their published size". This is the capability the submitter recorded as
    `Mission-related: Observatory/Instrument Models`; it is recorded here instead (see the removal
    below).
- **Removed by curator decision (2026-11-06), under rules 8 and 9:** `Mission-related:
  Observatory/Instrument Models`. Its capability, the modelled instrument fields of view, is recorded as
  `Models and Simulations: Observatory/Instrument Models` above, and the two would restate one capability
  under two parents (rule 9). The modelling is not part of any mission's own chain (a ground system, or
  the code that produces a mission's archive products): HelioFleet is an independent tool by one
  developer that reads public ephemerides from JPL Horizons and finished observation catalogues and
  images from public archives, and nothing in the repository, the DOI records or the project's pages
  names a mission that runs it as part of its operations or pipeline. A later refresh should not restore
  it.
- **Kept by curator decision (2026-11-06): `Mission-related: Operations`, with its parent
  `Mission-related` (rule 10).** The curator read `Operations` by capability — what the software does
  (planning, scheduling or coordinating observations) — rather than by which mission runs it. No
  mission runs HelioFleet in its operations, and the value does not claim one does; it records the
  software's support for planning coordinated observing campaigns:
  - planned-future positions: the timeline runs to 2030, and "Positions past each mission's latest
    tracking data are planning trajectories." (`README.md:94`);
  - which observers and instruments see a given solar location or point on the sky (the "Who sees this
    spot" tab, `index.html:532`, computed by `visibility`, `js/tools.js:311`; the "Who sees this
    point" panel, `sky.html:288`, implemented from `js/sky.js:592`), and whether a
    point lies inside each modelled instrument's field as projected onto an observer's sky (`inField`,
    `js/skyproj.js:108`), which shows where fields of view overlap;
  - searches for radial alignments, quadratures and magnetic connections between spacecraft
    (`findAlignments`, `js/tools.js:257`), and the calendar of upcoming perihelia, alignments,
    quadratures and solar conjunctions (`scripts/build_calendar.py`);
  - the coordinated-observation finder, which finds times when chosen facilities observed the same
    place together (`js/sky.js:849`).

  It schedules no observation, commands no instrument, interfaces with no hardware and monitors no
  telemetry: the value records support for planning, not control. It is a stored value that this
  reading of the code supports (rule 14), and a later refresh should not remove it without new evidence
  against that capability. `Data Processing and Analysis: Analysis` also carries the derived quantities
  behind these searches.
- **Considered and not selected:**
  - `Coordinate Transforms: Mission-Specific` — the fields of view are drawn from published elongation
    ranges in the ecliptic, not from spacecraft attitude or pointing frames; the reprojection of Solar
    Orbiter footprints into Earth's view is a solar helioprojective transform, carried by
    `Coordinate Transforms: Solar`.
  - `Coordinate Transforms: Planetary` — planets are shown as positions only; no planetary frame.
  - `Data Processing and Analysis: Image Processing` — the limb fit that corrects the recorded
    pointing of AIA cutouts (`scripts/fetch_context.py`) and the averaging of HMI synoptic maps
    (`scripts/fetch_synoptic.py`) are steps of the site's own data pipeline; no function processes an
    image a user supplies (rule 3).
  - `Data Processing and Analysis: Time Series Analysis` — time series are exported, not analysed; the
    window search is carried by `Analysis`.
  - `Data Visualization: Line Plots`, `Hodograms`, `Spectrogram`, `2D Slices`, `Mission-Specific`,
    `ML/AI` — the application draws maps, the surface map and the sky view; a sweep of `js/` and the
    pages for chart, line-plot, hodogram, spectrogram and histogram terms finds nothing.
  - `Models and Simulations: Physics-Based`, `Empirical`, `Forecasting`, `Data Guided` — the
    constant-speed CME fronts are a display of DONKI cone-model parameters whose README notes that
    "this constant-speed picture ignores drag, so real arrivals are usually later"; they are not a
    forecast product, and the Parker spiral is carried by `Field-line Tracing`.
  - `Servers and Environments` — a static site with no server component.

### 5. Related Region (RECOMMENDED)
- **Values (stored order, then additions):**
  - Solar Environment
  - Solar Wind
  - Interplanetary Space
  - Photosphere
- **Kept from the submitted record:**
  - `Solar Wind` — the software works in the solar wind: Parker-spiral field lines and footpoints at a
    chosen solar-wind speed (`js/frames.js:89-95`), the magnetic-connection search, and DONKI CME
    fronts moved out through interplanetary space (`activeCMEs`, `js/events.js:52`).
  - `Solar Environment` — supported on its own and as the coarse row of `Photosphere`.
- **Added:**
  - `Interplanetary Space` — the coarse row that contains the stored `Solar Wind`; rule 5 requires it,
    because the Region filter does not inherit. The spacecraft positions, heliospheric-imager fields of
    view and CME fronts are also interplanetary.
  - `Photosphere` — the solar surface map processes the HMI synoptic radial field of the photosphere
    (`scripts/fetch_synoptic.py`, averaged, clipped to ±20 G and drawn by `js/coverage.js:233`), and the
    software computes which observers see each photospheric location, with μ and limb curves
    (`seenBy`, `surfaceFeet`, `js/coverage.js:210-216`; `visibility`, `js/tools.js:311`). The README
    offers the spot tool for "an active region or flare site".
- **Considered and not selected:**
  - `Corona` — the coronagraph and K-Cor/UCoMP fields are observing geometry (which part of the
    corona each instrument images), and the AIA images behind the observation footprints are backdrops;
    no code processes or analyses coronal measurements (rule 4: where an instrument looks is not physics
    the software handles).
  - `Chromosphere` — the IRIS and DKIST footprints are observing geometry only.
  - Earth and planetary rows — Earth, Mercury, Venus, Mars and the Moon appear as positions; no
    magnetospheric or atmospheric physics.

### 6. Authors (MANDATORY)
- **Author:** Soumyaranjan Dash
  - **Author Identifier:** https://orcid.org/0000-0003-0103-6569
  - **Affiliation:** National Solar Observatory
    - **Affiliation Identifier:** https://ror.org/00b9pg524
- **Source:** From the submitted HSSI record; the stored Person row (given `Soumyaranjan`, family
  `Dash`, the ORCID above, affiliation the ROR-keyed National Solar Observatory row) matches every
  project source.
- **Evidence:** `CITATION.cff` (`given-names: Soumyaranjan`, `family-names: Dash`, the ORCID,
  `affiliation: "National Solar Observatory"`), `.zenodo.json` and the DataCite creators of every
  version (the same name, ORCID and affiliation), and the ORCID record (primary name Soumyaranjan Dash;
  current employment at National Solar Observatory, Boulder, from 2025, as Brinson Postdoctoral Research
  Associate, disambiguated to `https://ror.org/00b9pg524`). ROR `00b9pg524` resolves to National Solar
  Observatory. All 68 commits on the pinned ancestry are authored under this name, and no other person
  appears in `CITATION.cff`, `.zenodo.json`, the DataCite creators or contributors (the latter empty), or
  the commit history.
- **Considered and not added:** the ORCID record's earlier employment (University of Hawaiʻi at Mānoa,
  Institute for Astronomy, 2023–2025). No project source gives it, and it ended before this software
  was first committed in October 2026, so it does not cover the period the software was produced
  (rule 21).

### 7. Software Name (MANDATORY)
HelioFleet: an interactive map of heliophysics spacecraft positions

- **Source:** the submitted value, kept for now by the curator (2026-11-06) for the reason below. It
  is the title the author gives the software wherever the project asks to be cited: `CITATION.cff`
  `title`, `.zenodo.json` `title` (and with it the DataCite and Zenodo title of every deposit, Field 2),
  the README's "Citing HelioFleet" reference (`README.md:221`), the application's own citation
  (`CITATION.title`, `js/tools.js:334`, which the site's APA and BibTeX citations use) and
  `llms.txt:75`.
- **House style would list the name as just `HelioFleet` (Field 7 rule 1, below).** The curator did
  not feel justified in dropping the clause "an interactive map of heliophysics spacecraft positions"
  from the submitter's title without a place to put it back where people would see it:
  - with the name shortened, the clause appears in no field of the entry: neither the description
    (Field 8) nor the concise description (Field 9) uses it;
  - the concise description was the natural place, but the submitter's sentence plus the clause runs
    past Field 9's 200-character limit. Worked in as an appositive ("HelioFleet, an interactive map of
    heliophysics spacecraft positions, is a web tool …"), Field 9 would be 246 characters, and fitting
    it would mean rewriting the submitter's wording. Field 9 therefore stays as recorded there.

  So the submitted name is kept for now. The curator is putting the question to the submitter: are
  they content for the clause to be dropped? Until the submitter agrees, a later refresh must not
  shorten the name on rule 1 alone.
- **Prior value:** HSSI held `HelioFleet` from an earlier refresh on 2026-11-06, which shortened the
  submitted name under rule 1, until this update restored the submitted name.
- **The house-style alternative, held back rather than rejected: `HelioFleet`.** It is the name the
  project uses for itself outside its citations:
  - README title: `# HelioFleet` (`README.md:1`); the README calls it HelioFleet throughout its prose,
    and its citation section is headed "Citing HelioFleet".
  - The application declares it as its name: `<meta name="application-name" content="HelioFleet">`,
    `og:site_name` HelioFleet on every page, the JSON-LD `WebApplication` `name` HelioFleet
    (`index.html`), and the web manifest `short_name` HelioFleet.
  - `CITATION.cff`'s own message says "If you use HelioFleet in your research, please cite it as below."
  - The GitHub releases are named `HelioFleet 1.0.0` … `HelioFleet 1.1.2`.
- **The rule 1 reading behind house style:** the submitted value is the DataCite and Zenodo title of
  the DOI (`titles` of `10.5281/zenodo.23328187`), and the stored description is that deposit's
  description text, so the entry was filled from the DOI. The title is the software's name joined to a
  descriptive subtitle, and rule 1 treats a stored value equal to the DOI title, with non-name text
  attached, as an artifact rather than a name. Rule 3 does not keep it: the long form is a citation
  title the project writes in `CITATION.cff` `title`, `.zenodo.json` `title` and its citation lines,
  not a form it uses as its name in the README title, prose or application metadata, and Field 7's
  sources take a `CITATION.cff` `title` only "when it is a name and not a paper title". Under house
  style the clause is description, which Fields 8 and 9 carry. Rule 2 does not reject the long form
  itself, because the project writes it. The curator accepts this reading; the name is held back only
  for the reason above.
- **Other subtitles the project uses (context):** the project writes a different subtitle in almost
  every place it uses one — the citation title above; the page title `HelioFleet: Solar and Spacecraft
  Geometry`; the manifest `name` `HelioFleet: Spacecraft Positions Around the Sun`; the embed iframe
  title `HelioFleet: spacecraft positions around the Sun`; the JSON-LD `alternateName` `HelioFleet
  spacecraft position map`. The citation title is written the same way in every citation source; the
  constant across all of the forms is `HelioFleet`.
- **Rule 7:** no other HSSI entry was named HelioFleet when this record was made (an HSSI name search on
  2026-11-06 returned this entry only).
- **Page address:** the curator set the detail-page slug to `heliofleet` on 2026-11-06, so the address
  is shorter than the name; that is expected, not drift. It already matches the house-style name.

**TODO for the next Updater — the name waits on the submitter's answer:** ask the curator whether the
submitter ever said they are content for the clause "an interactive map of heliophysics spacecraft
positions" to be dropped from the name.
- If they agreed, shorten the name to `HelioFleet` under rule 1, and make sure the clause survives
  somewhere visible on the entry if possible (Field 9 was the natural place; see above for why it did
  not fit).
- If they declined or never replied, keep the submitted name.

### 8. Description (MANDATORY)
HelioFleet is a web tool that shows where heliophysics spacecraft (SDO, SOHO, Aditya-L1, ACE, Wind, DSCOVR, IMAP, SOLAR-1 (SWFO-L1), Carruthers, Solar Orbiter, Parker Solar Probe, BepiColombo, STEREO-A/B and MAVEN) are relative to the Sun and Earth on any date since 2010. It reports Stonyhurst and Carrington coordinates and Parker-spiral footpoints, searches for radial alignments, quadratures and magnetic connections, checks which observers see a given point on the Sun, and exports coordinates and time series. It draws the fields of view of coronagraphs and heliospheric imagers, summarises which solar longitudes are imaged on a solar surface map over SDO/HMI synoptic magnetograms, and shows flares, CMEs and geomagnetic storms from NASA DONKI. A viewing-geometry table gives each observer's light-time offset from Earth, apparent solar radius, B0 and L0. A sky view projects every instrument's field of view onto the plane of the sky seen from Earth or from a chosen spacecraft, with MLSO K-Cor and UCoMP fields, and draws the observation footprints of DKIST, IRIS, Hinode/EIS and Solar Orbiter (EUI-HRI, PHI-HRT, SPICE) over SDO/AIA and HMI images, with a finder for times when chosen facilities observed the same place together. Positions come from JPL Horizons ephemerides, refreshed monthly. The interface is available in English, Hindi and Spanish.
Live site: https://sr-dash.github.io/heliofleet/

- **Source:** From the submitted HSSI record, kept (Field 8 rule 6). It is the `.zenodo.json`
  description at the pin with its two HTML paragraphs rendered as two lines; the `CITATION.cff`
  `abstract` is the same text except that it writes `SOLAR-1` without `(SWFO-L1)` and has no live-site
  line.
- **The "Live site" line is kept:** it is the author's own deposit text, not integration boilerplate, a
  heading or release notes (rule 1 does not fire), and it gives a reader the address of the tool.
- **Every capability named was checked in the pinned code (rule 2):** the coordinate and footpoint
  table (`js/tools.js`), alignment, quadrature and connection search (`findAlignments`), spot visibility
  (`visibility`), exports (`toCSV`, `toJSON`, `timeSeries`), field-of-view drawing
  (`js/instruments.js`, `js/render.js:197`), the solar surface map (`js/coverage.js`), DONKI flares,
  CMEs and storms (`js/events.js`, `scripts/fetch_events.py`), the viewing-geometry table
  (`geometryRows`), the sky view with K-Cor and UCoMP (`js/skyproj.js:35`), the observation footprints
  and coordinated-observation finder (`scripts/fetch_observations.py`, `js/sky.js`), monthly Horizons
  refresh (`.github/workflows/update-ephemeris.yml`) and the Hindi and Spanish interface (`i18n/`).

### 9. Concise Description (OPTIONAL)
HelioFleet is a web tool that shows where heliophysics spacecraft are located in space in the past, present and planned future along with an option to overlay targeted limited FOV datasets

- **Submitted value:** `HelioFleet is a web tool that shows where heliophysics spacecrafts are located
  in space in past, present and planned future along with option to overlay targeted limited FOV
  datasets` (182 characters). It is the submitter's own wording and is kept (rule 5) apart from three
  grammar corrections (rule 4), each a single word:
  - `spacecrafts` → `spacecraft` (the plural is `spacecraft`, as the project writes it throughout);
  - `in past, present` → `in the past, present`;
  - `along with option` → `along with an option`.
- **Length:** 188 characters, within the 200-character limit.
- **Claims checked (rule 2):** "planned future" — the timeline runs to 2030 and the README says
  "Positions past each mission's latest tracking data are planning trajectories." (`README.md:94`);
  "targeted limited FOV datasets" — the IRIS, Hinode/EIS, DKIST and Solar Orbiter high-resolution
  observation footprints of the sky view.

### 10. Publication Date (RECOMMENDED)
2026-10-12

- **Submitted value:** `2026-10-30`, the release date of v1.1.2 and the `Issued` date of the concept
  DOI's DataCite record. Field 10 rule 1 excludes both: it is the date of a release after the first.
- **Value (rule 4, first release):** the first public release, v1.0.0, whose GitHub release ("First
  public release of HelioFleet, an interactive map of heliophysics spacecraft around the Sun and
  Earth") was published at 2026-10-12T23:38:11Z; the tagged commit `a68e2dd`
  is dated 2026-10-12T13:28:13-10:00 (23:28 UTC the same day), and the Zenodo deposit of v1.0.0 was
  created at 2026-10-12T23:38:15Z.
- **Considered and not used:**
  - DataCite `Issued` 2026-10-13 for the v1.0.0 version DOI and Zenodo `publication_date` 2026-10-13 —
    record dates of the deposit, a day later in UTC terms than the release itself (rule 1).
  - 2026-10-10, anchor (b): the GitHub repository was created at 2026-10-10T00:43:54Z and the root
    commit `114e0ad` is dated 2026-10-09T14:10:00-10:00 (00:10 UTC on 2026-10-10). Rule 4 uses the
    repository date only when no release exists.
  - 2026-10-09, the `datePublished` in the site's own JSON-LD (`index.html`): the root commit's local
    (UTC−10) date, not a release date.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- **Source:** From the submitted HSSI record (Field 11 rule 1: Field 2 is a Zenodo DOI; DataCite
  `publisher` is Zenodo). Zenodo has no ROR, and CERN's ROR identifies its operator, not the repository.

### 12. Version (RECOMMENDED)
- **Version Number:** 1.1.2
- **Version Date:** 2026-10-30
- **Version Description:**

HelioFleet 1.1.2 adds links to HelioField for any date, a How to use page, and a reworked navigation and layout.

**Links to HelioField**
- A HelioField button in the navigation bar opens HelioField at the same date.
  - From the map, it opens HelioField's coronal field and fleet view, with the spirals' wind speed.
  - From the sky view, it opens HelioField's Connectivity page for the chosen observer.

**Pages and navigation**
- A How to use page, and a flat navigation bar on every page with shareable links to each tool.

**Observations**
- Observation footprints export as CSV, with a SunPy script for JSOC FITS figures.

**Fleet**
- SWFO-L1 is renamed SOLAR-1.
- Proba-3 ASPIICS is skipped during its 2026 outage.

- **Version PID:** https://doi.org/10.5281/zenodo.23818629
- **Release history at the pin:** tags `v1.0.0`, `v1.1.0`, `v1.1.1`, `v1.1.2`, all on the pinned
  ancestry, each with a GitHub release named `HelioFleet <version>` and a Zenodo version deposit. No
  PyPI or other package distribution exists; the software is published as a web site. The commits after
  `v1.1.2` are unreleased (rule 2); a later refresh should look for a newer tag.
- **Number, date and PID — from the submitted record, kept:** `1.1.2` is the newest release (rule 4);
  the date is the GitHub release's `published_at` (2026-10-30T20:14:44Z), which the tagged commit
  `dd7bf41` (2026-10-30T10:14:40-10:00) and `CITATION.cff` `date-released` corroborate (rule 7); the
  PID is the 1.1.2 version DOI (DataCite `version` 1.1.2, `IsVersionOf` the concept; rule 17).
- **Description — re-derived (rule 11, then rules 13–16):** the entry was submitted with release notes
  that copied the software description (Field 8, including its "Live site" line). No clause of that text
  is accounted for by the v1.1.2 release notes or the `v1.1.1..v1.1.2` range; every clause was
  unattributable, so the description is re-derived. The release title `HelioFleet 1.1.2` is no more than the tag, so the source is the
  GitHub release body, kept verbatim with whole items removed (rule 15):
  - removed `- HelioField 1.2.1 links back.` — a change in a different software (HelioField);
  - removed `- Methods and help pages with a contents sidebar, larger text and the theme picker.` —
    documentation-page presentation;
  - removed `- Shorter page titles and descriptions, and a sky-view preview image.` — page-metadata
    housekeeping;
  - removed `- The monthly update reports failed observation and image fetches.` — maintenance of the
    data pipeline.

  This corrects a sub-value of the same release, so the number stays 1.1.2 (Field 12, *Correcting the
  same release*).

### 13. Programming Language (RECOMMENDED)
- **Values:**
  - Javascript
  - Other
  - Python 3.x
  - SQL
- **Submitted value:** `C++`, `Javascript`, `Other`, `Python 3.x`, `SQL`.
- **Removed (rule 9):** `C++` — the pinned tree contains no C or C++ source: the extension census of
  `git ls-tree -r` at the pin outside `data/` finds `.js`, `.py`, `.html`, `.css`, `.mjs` and `.sh`
  source files and configuration, image and text files, and GitHub's language statistics list
  JavaScript, HTML, Python, CSS and Shell.
- **Kept:**
  - `Javascript` — the application and its in-browser computation (`js/`, 24 modules;
    `tests/validate.mjs`).
    Field 13 rule 1's warning against recording a web page's client language applies to hosted services
    without exposed source; here the JavaScript is the published implementation (rule 4).
  - `Python 3.x` — the data pipeline (`scripts/*.py`, `#!/usr/bin/env python3`, run on Python 3.12 in
    CI) builds the data files under `data/` that the site shows, computes the calendar's alignments, quadratures and
    conjunctions (`scripts/build_calendar.py`) and the coordinated-observation groups
    (`scripts/fetch_observations.py`); the site also generates SunPy (Python) scripts for its users.
  - `Other` — kept as the submitter's value, not as a rule 7 qualification. The only languages in the
    tree without a vocabulary row are HTML and CSS, the application's pages (`index.html`, `sky.html`,
    `help.html`, `methods.html`) and styles (`css/style.css`), and Shell, which is CI tooling (below).
    Rule 7 admits `Other` for "A real language with no row" and never as a stand-in for "and some other
    files"; HTML and CSS are markup and style languages rather than programming languages, so they do
    not plainly qualify. No rule names them as excluded either (rule 9's removals are an `IDL` inferred
    from a data format or a deposit title, `Python 3.x` on Python-2-only code, a build system and a
    test-only language), so the submitted value is not shown wrong and stays. A stricter reading of
    rule 7 would remove it.
  - `SQL` — kept as submitted on a fair reading: the pipeline queries the Hinode/EIS as-run catalogue in
    SQLite (`EIS_QUERY`, `scripts/fetch_observations.py:153`) and the Solar Orbiter Archive in ADQL
    (`scripts/fetch_observations.py:195`). These two embedded queries are the whole of the SQL; a
    stricter reading of the form's definition ("The computer programming languages most important for
    the software.") could drop it.
- **Not recorded:** Shell (`scripts/report_failure.sh`, CI failure reporting — rule 4 tooling).

### 14. Reference Publication (OPTIONAL)
Not found

- The project's citation guidance names only Zenodo DOIs of the software — the concept DOI, which is
  Field 2's value, and the version DOIs (README "Citing HelioFleet"; `CITATION.cff` has no
  `preferred-citation`) — so no publication qualifies (rule 1).
- No paper describes HelioFleet: on 2026-11-06 an ADS full-text search for `"HelioFleet"` and for the
  concept DOI returned no records (controls: `"Solar-MACH"` returned 163, a nonsense token 0). The software was
  first released on 2026-10-12; a later refresh should repeat the search.

### 15. License (RECOMMENDED)
MIT License

- **Source:** From the submitted HSSI record; the `LICENSE` file at the pin is the MIT License text
  ("Copyright (c) 2026 Soumyaranjan Dash"), and `CITATION.cff`, `.zenodo.json`, the DataCite
  `rightsList` and GitHub's detected licence all say MIT (rule 3).

### 16. Keywords (OPTIONAL)
- **Values (stored names, then additions):**
  - coordinated observation
  - coordinated observations
  - coronagraph
  - dkist
  - heliophysics
  - heliosphere
  - hinode
  - iris
  - jpl horizons
  - multi-spacecraft
  - multi spacecraft observations
  - skyview
  - solar eclipse
  - solar orbiter
  - solar physics
  - spacecraft ephemerides
  - space weather
  - ephemeris
  - magnetic connectivity
  - Parker spiral
  - spacecraft
  - sunpy
  - visualization
  - total solar eclipse
- **Kept from the submitted record (rule 13):** all 17 stored keywords. Twelve are, exactly, keywords
  of the project's `CITATION.cff` and `.zenodo.json`; `multi spacecraft observations` is the thirteenth,
  the project's `multi-spacecraft observations` with a space for the hyphen; `multi-spacecraft` is one of
  the repository's GitHub topics. `skyview` is the project's "sky view" written as one word, and
  `coordinated observation` sits beside the plural `coordinated observations`; rule 13 forbids removing
  or re-sending a keyword to change only its separator, and these rows bind as stored. `heliosphere` is
  the submitter's own addition and is supported (the map, heliospheric imagers and CME fronts).
- **Added — project-declared GitHub topics (rule 9):** `ephemeris`, `sunpy` and `visualization` bind
  existing rows. Before this refresh no keyword row existed for `spacecraft` in any case, separator or
  plural variant, so it enters as a new row (rule 12) — a term a searcher types to find this tool.
- **Added — domain terms the code computes (rule 10):** `Parker spiral` (existing row, stored
  capitalisation) and `magnetic connectivity` (existing row): the Parker-spiral field lines and
  footpoints and the magnetic-connection search (`js/frames.js:89-95`, `findAlignments`).
- **Added at the submitter's request (rules 10 and 12):** `total solar eclipse`, a new lower-case
  row. The submitter asked for "Total Solar Eclipse" as a related phenomenon (hssi-website issue #172,
  2026-11-06); Field 22 has no row for it, so its rule 1 records it here. It is the code's own label,
  and the software finds and lists these eclipses:
  - the event search labels each eclipse preset "Total solar eclipse" (`js/app.js:540`); the presets
    come from the `ECLIPSES` catalogue of total and hybrid solar eclipses from 2010 to 2034
    (`js/catalog.js:126`);
  - the calendar feed lists the upcoming ones, each as "Total solar eclipse: <place>" or, for a hybrid
    eclipse, "Hybrid solar eclipse: <place>" (`scripts/build_calendar.py:11`, `:103`, `:194`);
  - the README's event search covers eclipses (`README.md:23`).

  It names a narrower thing than the stored `solar eclipse` (the project's declared keyword), not a
  case, separator or plural variant of it, so rule 11 does not bind that row; no live row spells it in
  any variant, so it is minted (rule 12).
- **Not added:**
  - the topics `astrophysical-data`, `astrophysics`, `astrophysics-data`, `astrophysics-research` and
    `astrophysics-simulation` — a rule-4 judgment, with a caveat. GitHub topics are project
    declarations, which rule 9 includes unless rules 2–4 exclude them, and a topic is itself a project
    use of the word, so rule 4's "no project description uses it" clause is not met literally (outside
    the topics, no file outside `data/` uses the word: a sweep for `astrophysic` returns no file;
    control: `heliophysics` matches 16 files). They are excluded under rule 4's other clause, a term
    that "promises something the record lacks": the software handles no astronomical data beyond the
    Sun and the inner heliosphere, which `heliophysics` and `solar physics` already carry, and
    `astrophysics-simulation` promises a simulation the software does not run, so that one is plainly
    unsupported. A row `astrophysics` exists, so including it would bind rather than mint; a later
    refresh may revisit the first four if the project describes itself that way in its own text.
  - `visualization-application`, `visualization-dashboard`, `visualization-pages` — also a judgment:
    project-declared, but GitHub tag compounds rather than domain terms, and rule 12 mints only "a
    genuinely new domain term"; `visualizations` is the plural of the existing `visualization` row
    (rule 11);
  - `solar-eclipse` and `solar-physics` — stored already as `solar eclipse` and `solar physics`.
- **PyHC marker (rule 15):** HelioFleet is not listed in `_data/projects_core.yml`, `_data/projects.yml`
  or `_data/projects_unevaluated.yml` of the PyHC registry (each parsed in full; no entry's name, code
  URL or description refers to it), so `pyhc package` does not apply.

---

## Section 3: Technical and Supplemental Metadata

### 17. Data Sources (OPTIONAL)
- **Values:**
  - Observatory/Mission-specific
  - TAP
  - Other
- **Submitted value:** empty. The pinned code reads these sources, so the record was incomplete.
- **Evidence (the data pipeline in `scripts/`, run monthly and documented with command-line usage;
  rule 2):**
  - `Observatory/Mission-specific` (rule 8) — single-mission or single-observatory archives: the JSOC
    directory of SDO/HMI synoptic maps (`BASE`, `scripts/fetch_synoptic.py:36`; the series
    `hmi.Synoptic_Mr_small`, `:4` and `:138`), the
    LMSAL Heliophysics Coverage Registry for IRIS, the DKIST Data Center dataset API, the Solar Orbiter
    Archive and the Hinode/EIS as-run catalogue `eis_cat.sqlite` (`scripts/fetch_observations.py:44-47`),
    and the Cryo-NIRSP viewer's DKIST inventory (`scripts/fetch_ground.py:20`). The missions are named
    in Fields 31/32, and Field 32 rule 6 requires this row for the DKIST entry, which rests on reading
    the DKIST Data Center.
  - `TAP` (rule 7) — the Solar Orbiter Archive is queried through its TAP service
    (`https://soar.esac.esa.int/soar-sl-tap/tap/sync`, `scripts/fetch_observations.py:46`) with an
    ADQL query (`:195`).
  - `Other` (rule 10) — three real sources with no row: the JPL Horizons API
    (`scripts/fetch_ephemeris.py:29`), the NASA CCMC DONKI API (`scripts/fetch_events.py:24`), and the
    Helioviewer API (`scripts/fetch_context.py:44`, and at run time in the browser,
    `js/observations.js:134`).
- **Considered and not selected:** `HTTP/HTTPS Directories` — the one directory tree read is JSOC's
  HMI synoptic directory, a single mission's archive already carried by `Observatory/Mission-specific`
  (rule 9). `CDAWeb` — a link on Wind's spacecraft card (`js/catalog.js:51`), not access (rule 2); a
  case-insensitive sweep of `js/`, `scripts/` and the pages for CDAWeb, HAPI, VSO, SSCWeb, OMNIWeb,
  AMDA, das2, Madrigal, GFZ, WDC, VirES and S3 finds that link and nothing else.

### 18. Input File Formats (RECOMMENDED)
Not found (evidenced empty)

- No user-supplied file is read: the application takes dates, locations and choices through its
  interface and URL, and reads only the JSON files the repository builds for it (rule 4, the software's
  own files).
- The pipeline fetches JSON from web APIs, an SQLite catalogue and the FITS synoptic maps of JSOC into
  memory (`read_fits(get(...))`, `scripts/fetch_synoptic.py:142`); it cannot be pointed at a user's own
  file of any of these formats, so none is an input format a user can bring (rule 9). `FITS` in
  particular was weighed and rejected on that ground.

### 19. Output File Formats (RECOMMENDED)
- **Values:**
  - JSON
  - csv
  - Other
- **Kept from the submitted record:** `JSON` — the coordinate table, time series and viewing-geometry
  table download as JSON (`toJSON`, `js/tools.js:80`; `js/workbench.js`).
- **Added (rules 6–7):**
  - `csv` — the coordinate table and time series (`toCSV`, `js/tools.js:66`), the alignment windows
    (`windowsCSV`, `js/tools.js:297`), the viewing-geometry table, and the observation footprints
    (`js/sky.js`).
  - `Other` — PNG and PDF snapshots (`downloadPNG`, `downloadPDF`, `js/export.js:224`, `:244`); MP4,
    WebM and GIF animations (`js/animate.js`); the iCalendar feed `calendar.ics`
    (`write_ics`, `scripts/build_calendar.py:217`); and Python (SunPy) scripts that reproduce the tables
    and footprint figures (`sunpyCode`, `geometrySunpy`, `js/tools.js:120`, `:201`; `footprintsSunpy`,
    `js/sky.js:950`).

### 20. Operating System (RECOMMENDED)
Operating System Independent

- **Source:** From the submitted HSSI record, kept (Field 20 rule 1): a web application used through a
  browser with nothing to install; the site's JSON-LD gives `"operatingSystem": "Any (web browser)"`.
  The CI runner (`ubuntu-26.04`) is the maintainer's pipeline platform, not a user's.

### 21. CPU Architecture (RECOMMENDED)
CPU Independent

- **Submitted value:** `Linux aarch64 or arm64`. Replaced (rule 9): a browser application computes on
  whatever machine runs the browser (rule 1), and nothing in the repository targets arm64 — no binary,
  build or job for it; every workflow runs on `ubuntu-26.04`.

### 22. Related Phenomena (OPTIONAL)
- **Values:**
  - Coronal Mass Ejections
  - Solar Flares
- **Submitted value:** empty.
- **Added (rule 5):**
  - `Coronal Mass Ejections` — the software models CME propagation: `activeCMEs` (`js/events.js:52`)
    moves each DONKI cone-model CME out from its 21.5 solar-radius time at its measured speed, and the
    map draws the fronts among the spacecraft (`js/render.js:233`, `js/scene.js:160`).
  - `Solar Flares` — it converts flare class to peak X-ray flux (`flareFlux`, `js/events.js:41`),
    marks a flare's source region in Carrington longitude so it rotates with the Sun (`focusFlare`,
    `js/app.js:451`), and reports which observers see a flare site (the spot tool).
- **Considered and not selected:** `Geomagnetic Storms` — storms appear only as timeline markers and
  presets labelled by G level (`G_LABEL`, `js/events.js`); no storm diagnostic is computed. The
  asymmetry with flares and CMEs, which come from the same DONKI catalogue, is deliberate: those two
  get phenomenon-specific computation (class-to-flux conversion, source-region tracking, front
  propagation), storms only a listing, so a searcher filtering on storms would find no storm analysis
  here.
  `Solar Wind` — the Parker spiral takes the solar-wind speed as a user parameter to draw connection geometry;
  the software does not model or analyse the solar wind itself (Field 5 carries the place).
  `Solar Corona`, `Coronal Heating`, `X-ray emission` — no code works on them.
- **Requested, with no row:** the submitter asked for "Total Solar Eclipse" here (hssi-website issue
  #172, 2026-11-06). The Phenomena vocabulary has no eclipse row, and the API accepts only its rows, so
  rule 1 records it as the Field 16 keyword `total solar eclipse`.

### 23. Development Status (RECOMMENDED)
Active

- **Source:** From the submitted HSSI record, re-derived (rule 6): stable releases exist (four, 1.0.0 to
  1.1.2), the last commit on `main` is the Source Revision (2026-11-05), the last release v1.1.2
  (2026-10-30); the repository is not archived and carries no status badge or statement.

### 24. Documentation (RECOMMENDED)
https://sr-dash.github.io/heliofleet/

- **Source:** From the submitted HSSI record, kept (rule 8). The project designates it: `.zenodo.json`
  and every DataCite version record relate the software `IsDocumentedBy` this URL, `CITATION.cff` gives
  it as `url`, and GitHub's `homepage` is the same site. It resolves (200) and links the How to use
  guide and the methods page from its navigation bar.
- **Considered and not used:** https://sr-dash.github.io/heliofleet/help.html, the How to use guide
  (JSON-LD `softwareHelp`), and https://sr-dash.github.io/heliofleet/methods.html — deep pages of the
  same site; rule 6 prefers the landing page, which reaches both.

### 25. Funder (OPTIONAL)
Not found (evidenced empty)

- No source attributes funding to the software: the README acknowledgements credit data providers only,
  `CITATION.cff`, `.zenodo.json` and every DataCite record carry no funding reference, and no paper
  about the software exists (Field 14). A case-insensitive sweep of the pinned tree outside `data/`
  for `\bfund|\bgrant\b|\baward|brinson|\bnsf\b|national science foundation|supported by|sponsor`
  matches one line, the author's JSON-LD `jobTitle` "Solar Physicist & Brinson Postdoctoral Fellow"
  (`index.html:73`), which also serves as the sweep's positive control.
- **Considered and rejected:** the Brinson postdoctoral fellowship — support of a person, not of the
  software (rule 3); the National Science Foundation as the sponsor of the National Solar Observatory,
  the author's employer — an institutional sponsor (rule 6).

### 26. Award Title (OPTIONAL)
Not found (evidenced empty)

- No award is named in any source (Field 25's sweep). The fellowship above is person-level support
  (rule 3).

### 27. Related Publications (OPTIONAL)
Not found (evidenced empty)

- **No publication about or using HelioFleet:** the ADS full-text searches of Field 14 found none.
- **Instrument papers weighed and not listed (rule 4):** the README's "Instrument field-of-view sources"
  and the methods page cite nine papers — Brueckner et al. 1995 (LASCO), Howard et al. 2008 (SECCHI
  COR2), Eyles et al. 2009 (STEREO HI), Antonucci et al. 2020 (Metis), Howard et al. 2020 (SoloHI),
  Vourlidas et al. 2016 (WISPR), Thompson et al. 2003 (SECCHI COR1), DeForest et al. 2025
  (arXiv:2509.15131, PUNCH) and Singh et al. 2025 (arXiv:2503.21184, Aditya-L1 VELC) — plus ESA/SIDC and
  NOAA pages. Each supplies the field-of-view extent of one instrument, so each is incidental to one
  parameter of the software; as a list they would describe the instruments rather than HelioFleet, and
  the project does not present any of them as the software's foundation or ask users to cite them.

### 28. Related Datasets (OPTIONAL)
- **Values:**
  - https://doi.org/10.48322/f3t3-n879
- **Submitted value:** empty.
- **Added (rule 3):** "Small Synoptic Charts of the Radial Component of the Photospheric Magnetic
  Field" (Stanford University, DataCite `Dataset`, landing page
  `https://spase-metadata.org/NASA/NumericalData/SDO/HMI/Synoptic/Radial_Magnetic_Field_Small`).
  `scripts/fetch_synoptic.py` downloads and reads the `hmi.Synoptic_Mr_small.<rotation>.fits` files from
  JSOC's HMI synoptic directory (`:138-142`), which its docstring describes as the 720 × 360 radial-field
  Carrington rotation maps, for the solar surface map. The DOI's record describes the same product: the
  small radial-field synoptic charts, made by boxcar-averaging `hmi.Synoptic_Mr_720s`, with the JSOC
  series `hmi.mrsynop_small_720s` as its access route and `IsCollectedBy` the SPASE HMI instrument. The
  DOI resolves to the SPASE landing page. The match is by product (resolution, field component and
  series), since the dataset record does not spell the file prefix.
- **Considered and not recorded:**
  - the daily-updated synoptic frame `hmi.Mrdailysynframe_small_720s_nrt`, also read by
    `fetch_synoptic.py` — no DOI or permanent landing page was found (a DataCite search on the series
    name and on daily HMI synoptic maps returned no dataset record for it);
  - the full-resolution "Synoptic Charts of the Radial Component of the Photospheric Magnetic Field"
    (`10.48322/pbwn-9t13`) — a different product the code does not read (rule 2);
  - JPL Horizons ephemerides, the DONKI catalogue, the IRIS, EIS, DKIST and Solar Orbiter observation
    catalogues — the code reads these services' records or archive metadata, and no dataset DOI
    identifies what it reads; their services are recorded in Field 17.

### 29. Related Software (OPTIONAL)
Not found (evidenced empty)

- **Considered and not used:**
  - HelioField (`https://github.com/sr-dash/heliofield`), the same author's coronal-field viewer — the
    relationship the project documents is the link between the two tools, so it is recorded in Field 30
    alone (Field 29 rule 3; Field 30 rule 9).
  - The Cryo-NIRSP viewer (`https://github.com/sr-dash/cryonirsp-viewer`) — likewise a data exchange,
    Field 30.
  - solarmach (`https://github.com/jgieseler/solarmach`, in HSSI) performs a similar task, but no
    HelioFleet source names it (rule 4); record it only if the project itself does.
  - EISPAC — named once as context for the EIS catalogue file ("as used by EISPAC",
    `scripts/fetch_observations.py:9`); not imported or used (rule 4).
  - astropy and SunPy as used by `scripts/make_reference.py` to build test reference values — test-only.
  - jsPDF, mp4-muxer and gifenc (loaded from CDNs for snapshot and animation export) — generic
    infrastructure (rule 1).

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - https://github.com/sunpy/sunpy
  - https://github.com/Helioviewer-Project/helioviewer.org
  - https://github.com/sr-dash/heliofield
  - https://github.com/sr-dash/cryonirsp-viewer
- **Submitted value:** empty.
- **Added (rule 7), with the exchange each rests on:**
  - **SunPy** — HelioFleet writes its results into SunPy code for the user: the coordinate and
    viewing-geometry tabs export SunPy scripts that reproduce the tables from JPL Horizons
    (`sunpyCode`, `geometrySunpy`, `js/tools.js:120`, `:201`), and the observation panel exports a
    script that fetches the AIA or HMI image through `sunpy.net.Fido` and draws HelioFleet's footprints
    on a `sunpy.map` (`footprintsSunpy`, `js/sky.js:950`). Its heliographic coordinates are validated
    against SunPy on every push (`tests/validate.mjs`). URL: the in-catalogue entry's stored
    `code_repository_url` (rule 11).
  - **Helioviewer.org** — HelioFleet opens Helioviewer.org at the selected moment with chosen layers
    (`hvUrl`, `js/helioviewer.js:40`) and loads AIA and HMI images from the Helioviewer API for its
    footprint panel (`js/observations.js:134`). A hosted domain tool with a documented hand-off. URL:
    the upstream repository, the same string other catalogue entries used for Helioviewer.org when this
    record was made.
  - **HelioField** — the navigation bar opens HelioField at the same date, carrying the spirals'
    solar-wind speed from the map and the chosen observer from the sky view (`FIELD_URL`,
    `js/app.js:120`, `js/sky.js:95`; v1.1.2 release notes), and HelioField links back. HelioField has the concept DOI
    `10.5281/zenodo.23487231`; the repository form is recorded because the site shows the raw URL as
    link text (Field 29 rule 13).
  - **Cryo-NIRSP viewer** — HelioFleet imports the viewer's DKIST Cryo-NIRSP dataset inventory
    (`scripts/fetch_ground.py:20`) and links each footprint to that dataset's page in the viewer
    (`js/sky.js:708`). No DOI was found for it.
- **Considered and not used:** JPL Horizons and NASA DONKI — data services read by the pipeline,
  recorded in Field 17. No HSSI entry's Fields 29/30 pointed at HelioFleet on 2026-11-06 (a sweep of the
  catalogue's related-item rows for the repository, the concept DOI and the project name found none),
  so no reverse relation was waiting to be tested.

### 31. Related Instruments (OPTIONAL)
- **Values** (each `name` copied byte for byte from its vocabulary row; every identifier resolves to
  exactly one row of the live vocabulary, and none has an `.html` duplicate):

  *Instruments whose observation records the software reads, through instrument-specific archives:*
  - **Instrument Name:** Interface Region Imaging Spectrograph
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/IRIS/IRIS
  - **Instrument Name:** EUV Imaging Spectrometer
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/Hinode/EIS
  - **Instrument Name:** Extreme Ultraviolet Imager
    - **Instrument Identifier:** https://spase-metadata.org/ESA/Instrument/SolarOrbiter/EUI
  - **Instrument Name:** Polarimetric and Helioseismic Imager
    - **Instrument Identifier:** https://spase-metadata.org/ESA/Instrument/SolarOrbiter/PHI
  - **Instrument Name:** Spectral Imaging of the Coronal Environment
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SolarOrbiter/SPICE

  *SDO instruments whose data the software reads as the context for its maps:*
  - **Instrument Name:** Atmospheric Imaging Assembly
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/AIA
  - **Instrument Name:** HMI
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/HMI

  *Instruments whose fields of view the software models (listed by the curator's decision, below):*
  - **Instrument Name:** Large Angle Spectroscopic Coronagraph
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SOHO/LASCO
  - **Instrument Name:** STEREO-A SECCHI Cor1 Coronagraph
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/Cor1
  - **Instrument Name:** STEREO-B SECCHI Cor1 Coronagraph
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/Cor1
  - **Instrument Name:** STEREO-A SECCHI Cor2 Coronagraph
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI/Cor2
  - **Instrument Name:** STEREO-B SECCHI Cor2 Coronagraph
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI/Cor2
  - **Instrument Name:** Heliospheric Imager-1 Telescope on the STEREO-A mission
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/HI-1
  - **Instrument Name:** Heliospheric Imager-1 Telescope on the STEREO-B mission
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/HI-1
  - **Instrument Name:** Heliospheric Imager-2 Telescope on the STEREO-A mission
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/HI-2
  - **Instrument Name:** Heliospheric Imager-2 Telescope on the STEREO-B mission
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/HI-2
  - **Instrument Name:** Metis
    - **Instrument Identifier:** https://spase-metadata.org/ESA/Instrument/SolarOrbiter/Metis
  - **Instrument Name:** The Solar Orbiter Heliospheric Imager
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/SolarOrbiter/SoloHI
  - **Instrument Name:** Parker Solar Probe, PSP, Wide-field Imager for Solar Probe, WISPR, Suite, Inner Telescope, IT, Instrument
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/WISPR/InnerTelescope
  - **Instrument Name:** Parker Solar Probe, PSP, Wide-field Imager for Solar Probe, WISPR, Suite, Outer Telescope, OT, Instrument
    - **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/WISPR/OuterTelescope
  - **Instrument Name:** Narrow Field Imager
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/PUNCH/NFI
  - **Instrument Name:** Wide Field Imager
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/1
  - **Instrument Name:** Wide Field Imager
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/2
  - **Instrument Name:** Wide Field Imager
    - **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/3
  - **Instrument Name:** MLSO K-Coronagraph
    - **Instrument Identifier:** https://spase-metadata.org/NSF/Instrument/Ground/MLSO/K-Cor

- **Removed:** the entry was submitted with a single `UNKNOWN` row here (type 1, no identifier). It
  names no instrument and carries no SPASE identifier, so it is never a value of this field (rule 22);
  the curator directed its removal.
- **Curator decision (2026-11-06): the broad reading of rule 6.** Instruments whose fields of
  view HelioFleet models are listed although the software never reads their data. Field-of-view
  modelling is a primary feature that the project's own description names ("It draws the fields of
  view of coronagraphs and heliospheric imagers", and "A sky view projects every instrument's field of
  view onto the plane of the sky"), and someone working with those instruments' data who is checking
  which viewpoints overlap could reasonably reach for it. The decision covers the 18 rows of the third
  group here and, in Field 32, the GOES-19 and Mauna Loa Solar Observatory rows; the fleet and PUNCH
  rows of Field 32 rest on the same reading (see there). A later refresh should not reopen it on the
  ground that these instruments' data are not read.
- **Evidence, by group (Stage A rule 6, Stage C rules 17–18):**
  - *Observation footprints.* `scripts/fetch_observations.py` reads, for each instrument, its own
    observation catalogue — IRIS raster and slit-jaw fields from the LMSAL Heliophysics Coverage
    Registry, Hinode/EIS from the EIS as-run catalogue, Solar Orbiter EUI-HRI, PHI-HRT and SPICE level-2
    metadata from the Solar Orbiter Archive — and the sky view draws the footprints over SDO images and
    finds coordinated observations among them. These are instrument-specific archive calls with
    per-instrument parsing; a scientist working with IRIS, EIS, EUI, PHI or SPICE data looking for
    co-observations would reach for this. The rows for EUI and PHI cover the whole instruments; the
    vocabulary has no separate HRI channel rows.
  - *SDO context.* HMI: `scripts/fetch_synoptic.py` reads HMI synoptic radial-field maps from JSOC for
    the solar surface map. AIA and HMI: `scripts/fetch_context.py` and the browser
    (`js/observations.js:128-134`) request AIA 171 Å, AIA 193 Å and HMI magnetogram images by
    instrument and channel, and the exported footprint script fetches AIA or HMI FITS images from JSOC.
  - *Modelled fields of view.* `js/instruments.js:29` defines a field for each listed coronagraph and
    heliospheric imager, per spacecraft (COR1, COR2, HI-1 and HI-2 separately on STEREO-A and STEREO-B;
    WISPR-I and WISPR-O separately; LASCO C2 and C3, both under the one LASCO row), drawn on the map and
    projected onto any observer's sky with "Who sees this point" naming each instrument whose field
    contains a point. K-Cor is drawn from `GROUND` (`js/skyproj.js:35`). PUNCH NFI is one instrument
    with one row.
  - *PUNCH WFI, settled under rules 7, 18 and 19.* The code models a single WFI field, `wfi`
    (`js/instruments.js:50`, 3–45°), with no per-camera table or branch. It is drawn in the sky view as
    a full annulus because, as the comment beside that shape says, "PUNCH's three WFI cameras together
    cover all position angles" (`js/skyproj.js:25-26`): the field modelled is the combined coverage of
    the three cameras. The vocabulary's three `Wide Field Imager` rows are three distinct instruments,
    one per WFI spacecraft (each row's SPASE `ObservatoryID` is its own `PUNCH-WFI-n` observatory), not
    one entity with competing rows (rule 14). Rule 18 records all three, because that statement names
    all three cameras as what the field represents; it is not one example expanded into many (rule 7),
    and rule 19 does not apply, because the repository does select among the rows — it selects all of
    them. The choice rests on that one comment together with the full-annulus shape it explains. If a
    later refresh finds the comment gone and the field redrawn for one camera, the WFI rows follow it,
    and so do the PUNCH observatory rows of Field 32.
- **Resolution choices (rules 13–16):** EUI, PHI and Metis exist only under `ESA/`, SoloHI only under
  `NASA/`, and COR1 and HI-1/HI-2 only under `NASA/` (COR2 only under `SMWG/`), so each is the single row
  for its entity. The `SMWG/Instrument/STEREO-A/SECCHI` and `…/STEREO-B/SECCHI` suite rows and the
  `SMWG/Instrument/ParkerSolarProbe/WISPR` suite row (`PSP WISPR`) were not used: the code supports the
  individual telescopes, which have rows (rule 7). The long WISPR telescope names are the rows' own.
- **Substituted to Field 32 (rule 20):** the DKIST instruments Cryo-NIRSP, VBI, ViSP, DL-NIRSP and VTF
  (footprints from the DKIST Data Center and the Cryo-NIRSP viewer) have no instrument rows → `Daniel K
  Inouye Solar Telescope`; MLSO UCoMP has no row → `Mauna Loa Solar Observatory`; GOES-19 CCOR-1 has no
  row → `Geostationary Operational Environmental Satellite 19`.
- **Documented omissions (rule 21):** Aditya-L1 VELC, SOLAR-1 CCOR-2 and Proba-3 ASPIICS — no row for
  the instrument, and no row for its platform (sweeps of name, abbreviation, identifier and definition
  for `VELC`, `Visible Emission Line`, `Aditya`, `CCOR`, `Compact Coronagraph`, `SWFO`, `SOLAR-1`,
  `ASPIICS` and `Proba-3` returned nothing; controls: `SUVI` positive, a nonsense token negative).
- **Considered and not used:** instruments that appear only as Helioviewer.org link layers on the
  spacecraft cards (SOHO EIT, STEREO EUVI, Solar Orbiter EUI FSI, GONG H-alpha; `js/helioviewer.js`) —
  links to another viewer, not support (rule 3); the Hinode SOT and XRT rows — the code reads EIS only;
  the in-situ instruments of the fleet spacecraft (for example PSP FIELDS) — the software uses only the
  spacecraft positions.

### 32. Related Observatories (OPTIONAL)
- **Values** (each `name` copied byte for byte from its vocabulary row; every identifier resolves to
  exactly one row, and none has an `.html` duplicate):
  - **Observatory Name:** Solar Dynamics Observatory
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SDO
  - **Observatory Name:** Solar and Heliospheric Observatory
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SOHO
  - **Observatory Name:** Advanced Composition Explorer
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ACE
  - **Observatory Name:** ISTP/Wind
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Wind
  - **Observatory Name:** Deep Space Climate Observatory, DSCOVR
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/DSCOVR
  - **Observatory Name:** Solar Orbiter
    - **Observatory Identifier:** https://spase-metadata.org/ESA/Observatory/SolarOrbiter
  - **Observatory Name:** Parker Solar Probe
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe
  - **Observatory Name:** BepiColombo Spacecraft
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/BepiColombo
  - **Observatory Name:** Solar Terrestrial Relations Observatory A
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-A
  - **Observatory Name:** Solar Terrestrial Relations Observatory B
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-B
  - **Observatory Name:** Mars Atmosphere and Volatile EvolutioN
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/MAVEN
  - **Observatory Name:** Daniel K Inouye Solar Telescope
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/DKIST
  - **Observatory Name:** Mauna Loa Solar Observatory
    - **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Ground/MaunaLoaSO
  - **Observatory Name:** Geostationary Operational Environmental Satellite 19
    - **Observatory Identifier:** https://spase-metadata.org/NOAA/Observatory/GOES/19
  - **Observatory Name:** PUNCH-NFI
    - **Observatory Identifier:** https://spase-metadata.org/NASA/Observatory/PUNCH/NFI
  - **Observatory Name:** PUNCH-WFI-1
    - **Observatory Identifier:** https://spase-metadata.org/NASA/Observatory/PUNCH/WFI/1
  - **Observatory Name:** PUNCH-WFI-2
    - **Observatory Identifier:** https://spase-metadata.org/NASA/Observatory/PUNCH/WFI/2
  - **Observatory Name:** PUNCH-WFI-3
    - **Observatory Identifier:** https://spase-metadata.org/NASA/Observatory/PUNCH/WFI/3
- **Removed:** the entry was submitted with a single `UNKNOWN` row here (type 2, no identifier). It
  names no observatory and carries no SPASE identifier, so it is never a value of this field (rule 22);
  the curator directed its removal.
- **Evidence:**
  - *The fleet (the first eleven rows).* These rest on the curator's broad reading (Field 31),
    applied to the spacecraft themselves, and not on any reading of these missions' data: HelioFleet
    reads no SOHO, ACE, Wind, DSCOVR, MAVEN, BepiColombo, Parker Solar Probe or STEREO data — their
    positions come from JPL Horizons ephemerides, and the spacecraft cards link to each mission's
    archive — and for SDO and Solar Orbiter the data it reads are those of their instruments in Field 31
    (AIA and HMI images; EUI, PHI and SPICE observation metadata), not anything the spacecraft rows
    themselves rest on. What it
    does is model and display where each spacecraft is, with per-spacecraft code: the
    supported-spacecraft list `SPACECRAFT` (`js/catalog.js:5`), with each body's Horizons ID, launch date
    and mission and archive links in `BODIES`; the near-Earth inset fleet `L1_FLEET` (`:11`); the
    loss-of-contact dates after which positions are treated as predictions (`lost`, `:107` for STEREO-B
    and `:116` for MAVEN); and, for each spacecraft, its perihelia (`perihelia`, `js/bodyinfo.js:37`),
    light time and speed (`liveFacts`, `js/bodyinfo.js:15`), and alignment, quadrature and Parker-spiral
    connection geometry (`findAlignments`, `js/tools.js:257`). The software targets the platforms (Field
    32 rule 1), and a scientist working with any of these missions' data who needs the spacecraft's
    position, viewpoint or magnetic connection on a date could reasonably reach for it. Rows are the
    per-spacecraft ones the code names; the fleet-level `SMWG/Observatory/STEREO` row and the BepiColombo
    sub-spacecraft rows (`Mercury Planetary Orbiter`, `Mio`) were not used, because the code tracks
    STEREO-A and STEREO-B separately and BepiColombo as one body.
  - *DKIST.* The pipeline reads the DKIST Data Center dataset API for the observatory's instruments and
    the Cryo-NIRSP viewer inventory, and the sky view computes the Sun's daylight window at Haleakalā
    for DKIST (`SITES`, `observingWindow`, `js/skyproj.js:164-184`); it is also the substitution for the
    DKIST instruments, which have no rows.
  - *MLSO.* The sky view draws the K-Cor and UCoMP fields and computes the daylight window at Mauna Loa
    (`js/skyproj.js:35`, `:164-184`); it is also the substitution for UCoMP. Listed under the curator's
    broad reading.
  - *GOES-19.* Substitution for the CCOR-1 coronagraph (`js/instruments.js`, mission `GOES-19`), which
    has no instrument row (Field 31 rule 20). Listed under the curator's broad reading.
  - *PUNCH (the last four rows).* Field 32 rule 1: Field 31 records an instrument row for each unit of
    the PUNCH fleet — NFI and WFI 1–3 — so the per-unit observatory row for each of those units belongs
    here too; each instrument row's SPASE `ObservatoryID` is the matching row here
    (`spase://NASA/Observatory/PUNCH/NFI`, `…/WFI/1`, `…/WFI/2`, `…/WFI/3`). Each unit is supported
    through its modelled field under the curator's broad reading. The methods page notes that
    "Proba-3, GOES-19 and PUNCH are in Earth orbit and are drawn from Earth's position" (`methods.html`);
    that is a drawing simplification, not an exception rule 1 lists, so it does not keep the rows out.
    These rows follow the WFI decision in Field 31: if the WFI rows change, the `PUNCH-WFI-n` rows
    change with them.
- **Resolution choices (rules 13–15, Field 32 rule 4):** SMWG rows were chosen over the same-entity
  CNES/CDPP-AMDA or CDPP-Archive twins for SOHO, ACE, Wind (`ISTP/Wind`, not CNES `NASA Mission` or
  `Wind`), DSCOVR, PSP, BepiColombo, STEREO-A, STEREO-B and MAVEN. Solar Orbiter has no SMWG row; the
  ESA row is chosen over `CNES/Observatory/CDPP-AMDA/SolO` as the mission agency's authority (rule 15's
  own example). Mauna Loa Solar Observatory has two identically named rows,
  `NSF/Observatory/Ground/MLSO` and `SMWG/Observatory/Ground/MaunaLoaSO`; the K-Cor instrument row's
  SPASE record gives `ObservatoryID` `spase://SMWG/Observatory/Ground/MaunaLoaSO` (rule 14), and SMWG
  breaks the tie the same way (rule 15). The same K-Cor record also carries an `Association` of type
  `PartOf` naming `spase://NSF/Observatory/Ground/MLSO`, the other row; rule 14 decides on
  `ObservatoryID`, and the rule-15 tie-break agrees, so the SMWG row is the settled choice and the
  `PartOf` link is not a reason to switch. The DSCOVR row's name carries the abbreviation
  (`Deep Space Climate Observatory, DSCOVR`) on the bare SMWG row; it is the row's own name, not an
  `.html` orphan.
- **Documented omissions (rule 21):** Aditya-L1, IMAP, SOLAR-1 (SWFO-L1) and the Carruthers Geocorona
  Observatory are in the fleet but have no observatory row (sweeps of all four columns for `Aditya`,
  `IMAP`, `Interstellar Mapping`, `SWFO`, `SOLAR-1`, `Space Weather Follow`, `Carruthers` and
  `Geocorona` found only unrelated rows, such as Interball's `IMAP-3` magnetometer and the TWINS
  neutral-atom imagers); Proba-3 has no row.
- **Considered and not used:** the `Interface Region Imaging Spectrograph` and `Hinode` observatory
  rows (`SMWG/Observatory/IRIS`, `SMWG/Observatory/Hinode`) — the software targets the IRIS and EIS
  instruments, recorded in Field 31, not the platforms (rule 7); the fleet-level `PUNCH Mission` row
  (`NASA/Observatory/PUNCH`) — the software supports PUNCH only through the modelled NFI and WFI
  fields, recorded with their per-unit rows; it does not show the PUNCH spacecraft or target the mission
  as a whole (`SPACECRAFT`, `js/catalog.js:5`, has no PUNCH entry), so a fleet-level row is not
  independently right (rule 1).

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/sr-dash/heliofleet/de4b623b0b0692354e2ca35166c24c5e68edccda/assets/og-image.png

- **Submitted value:** `https://github.com/sr-dash/heliofleet/blob/main/assets/og-image.png` — GitHub's
  file-viewer page, which answers 200 with `text/html`, so the logo renders broken.
- **Same image, new URL form (rules 1, 7, 11):** the commit-pinned raw URL of the same file answers 200
  with `image/png`, 159,624 bytes, a 1200 × 630 PNG whose SHA-256 (`cb95ec28…9d03697`) equals the
  tracked blob at the Source Revision; the path is not Git-LFS-tracked (no `.gitattributes`). The file
  is unchanged since commit `93eaeb7` (2026-10-09).
- **What it depicts:** the HELIOFLEET wordmark, the tagline "Where the Sun-watching spacecraft are, on
  any date since 2010." and the map of the fleet at the 2024-04-08 total solar eclipse. The project uses
  it as its image: `og:image` and `twitter:image` on the main, help and methods pages, and the
  `WebApplication` JSON-LD `image` (`index.html`).
- **Considered and not used:** the app icon (`assets/icon-512.png`, `assets/favicon.svg`: the Sun,
  an orbit ring, Earth and a spacecraft marker on a dark rounded square), which the web manifest and
  favicons use. It predates the submission (commit `16a71b1`, 2026-10-09), so it is not a mark adopted
  since the logo was chosen, and rule 1 keeps the submitted image. Adopting the icon instead would be a
  deliberate change of image, not a correction.

---

## Follow-ups for the next refresh

- Field 7: ask the curator whether the submitter agreed to drop "an interactive map of heliophysics
  spacecraft positions" from the name, and act on the answer as Field 7's TODO says: shorten it to
  `HelioFleet` under rule 1 only if they agreed, keeping the clause visible on the entry if possible;
  otherwise keep the submitted name.
- Look for a release after v1.1.2, and repeat the literature search (Fields 14, 27).
- Re-run the observatory sweeps for Aditya-L1, IMAP, SOLAR-1, Carruthers and Proba-3 and the instrument
  sweeps for VELC, CCOR-1, CCOR-2, ASPIICS, UCoMP and the DKIST instruments; rows added upstream would
  replace the substitutions and omissions above.
