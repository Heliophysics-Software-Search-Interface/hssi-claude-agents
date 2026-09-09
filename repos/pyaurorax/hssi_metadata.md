# HSSI Metadata Extraction Results

**HSSI Software ID:** a73ebc78-1f89-4af8-8f67-2e35de947d16
**Repository:** https://github.com/aurorax-space/pyaurorax
**Source Revision:** 741938df29d05f20919f68597fabdad71aec3b13
**Extraction Date:** 2026-09-08
**Validation Date:** 2026-09-09
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

PyAuroraX is the **Python client library for the AuroraX data platform**, written by the University
of Calgary's Auroral Imaging Group. Three facts about its structure shape almost every field below,
and getting them straight prevents most of the misreadings this dossier exists to forestall:

1. **It is one of two sibling client libraries.** `aurorax-space/idl-aurorax` is the IDL counterpart,
   a separate repository with the same purpose. The two share a single Zenodo deposit whose title
   names both, which is why several metadata sources describe "PyAuroraX and IDL-AuroraX" as one
   thing. Every field on **this** record describes the Python library only, and evidence drawn from
   the shared deposit has to be read with that in mind — most visibly in Fields 2, 13 and 29.
2. **Most low-level data handling is delegated to `pyucalgarysrs`.** `pyproject.toml` at the pin
   declares `pyucalgarysrs = "^1.26.0"`, and everything under `pyaurorax/data/ucalgary` and
   `pyaurorax/models/atm` forwards to it. So a capability can be genuinely user-facing here while
   the file-parsing or HTTP code lives in the dependency. Format and data-source evidence therefore
   comes from the reader docstrings and public API surface, not from finding `h5py` in this tree
   (there is none: `git grep -n -P -i 'cdflib|netcdf|spacepy' <pin> -- pyproject.toml poetry.lock`
   returns no output, and `git grep -l -P -i 'hdf5|h5py' <pin> -- pyaurorax` returns 0 files).
3. **Several stored values trace to the PyHC registry's keyword taxonomy rather than to the code.**
   PyHC's entry for this package (`_data/projects.yml` line 408, in the *evaluated* list) carries
   `keywords: ["ionosphere_thermosphere_mesosphere", "2D_graphics", "calibration", "coordinates",
   "data_container", "data_retrieval", "image_processing", "line_plots", "multidimensional",
   "orbit", "plotting", "specific", "ascii", "binary", "cdf", "hdf5", "idl_save", "local",
   "web_service", "data_access", "data_analysis", "instrumentation"]`. The Keywords HSSI held
   before this refresh (Field 16) were that list with underscores turned into spaces, and the
   input/output formats it held (Fields 18/19) were its `ascii`/`cdf`/`hdf5`/`idl_save` entries.
   That propagation is the single best explanation for the values those three fields carried that
   the repository does not support, and it is why every such value was tested against the code
   rather than inherited — and why the tags with no code support are no longer there.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This is the catalogue-wide placeholder convention for an entry not submitted by this workflow. It is
not a gap to be researched: the form's submitter is the person lodging the record, not an author.

### 2. Persistent Identifier (RECOMMENDED)
- **Value:** https://doi.org/10.5281/zenodo.5815984

This is the Zenodo **concept** DOI for the shared PyAuroraX / IDL-AuroraX deposit, and it is the
project's own choice of identifier: `README.md:6` at the pin carries the badge
`[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.5815984.svg)](https://doi.org/10.5281/zenodo.5815984)`.

Its concept status is structural, not inferred from a title: `https://zenodo.org/api/records/5815984`
returns a 302 to `https://zenodo.org/api/records/12532077`, the redirect-to-latest-version behaviour
that distinguishes a Zenodo concept record from a version record, and the DataCite record for
`10.5281/zenodo.12532077` reports `conceptdoi` `10.5281/zenodo.5815984`.

Three complications are recorded here because each of them has previously been mistaken for a defect
or for a reason to change the value, and all three are properties of the deposit rather than errors:

- **The deposit covers two libraries.** The DataCite title is `PyAuroraX and IDL-AuroraX - data
  access and analysis support libraries for All-Sky Imager (ASI) data`, and the abstract's closing
  sentence is `PyAuroraX and IDL-AuroraX are Python and IDL libraries that provide data access, data
  analysis support software, and interaction with the AuroraX Search Engine.` So the DOI is not
  specific to this HSSI entry's software.
- **The deposit is frozen at 1.0.0.** The concept's `relatedIdentifiers` list exactly four
  `HasVersion` targets — `10.5281/zenodo.5815985` (0.8.0), `10.5281/zenodo.5816001` (0.9.2),
  `10.5281/zenodo.6098075` (0.9.2) and `10.5281/zenodo.12532077` (1.0.0) — so no version deposit
  exists after 1.0.0 (June 2024) while the software is at 1.23.0 (September 2026). The concept's own
  DataCite `version` field reads `1.0.0` for the same reason.
- **These are manual deposits, not GitHub-integration deposits.** Neither the concept nor
  `10.5281/zenodo.12532077` carries any `IsSupplementTo` relation or any `/tree/` URL;
  `12532077`'s only related identifier is `IsVersionOf 10.5281/zenodo.5815984`. A
  GitHub-integration deposit would carry an `IsSupplementTo` pointing at a tagged tree — the two
  Field 29 DOIs below both do. This is why no new version DOI appeared when 1.1.0 through 1.23.0
  were released: nothing is minting them automatically, and no one has minted one by hand.

**Why this DOI is the entry's persistent identifier.** Field 2 drives the entry page's "Cite Me"
block, which renders under the heading "Software" via `doi.org` content negotiation, so the question
was what a visitor sees, not whether the string is a valid DOI (it is). The concept DOI is kept: it
is the identifier the project publishes in its own README, it is the only DOI that points at this
software's code at all, and a visitor who follows the citation lands on the AuroraX libraries'
Zenodo record, which is where the maintainers point people. The costs are accepted knowingly — the
citation names two libraries, and it resolves to a June 2024 1.0.0 snapshot rather than to anything
close to the current release, the deposit's content being over two years and 23 minor releases
stale.

Two alternatives were weighed and rejected:

- **Clearing the field.** The entry would then show no software citation at all. That is honest
  about there being no PyAuroraX-specific, current concept DOI, but it removes the project's own
  preferred citation from the page and gives the visitor nothing citable in its place.
- **Moving the DOI's role to Fields 14/27.** Field 14 (Reference Publication) is defined as "The DOI
  for the publication describing the software", and Field 27 as publications that "describe, cite,
  or use the software". Neither describes a software deposit, so in practice this meant clearing
  Field 2 and letting the *Frontiers* article (see Field 14) serve as the entry's only citation. It
  was rejected because the visitor would lose every pointer to the code deposit, and because that
  article is co-authored across three tools. The article is recorded in Field 14 on its own merits
  instead, so the entry carries both a software citation and a correctly-labelled reference
  publication rather than trading one for the other.

### 3. Code Repository (MANDATORY)
- **Value:** https://github.com/aurorax-space/pyaurorax

Correct and current. `pyproject.toml` at the pin declares both `homepage` and `repository` as this
URL, PyPI's `project_urls` gives `Repository` and `Homepage` as this URL, and the PyHC registry's
`code:` field for the entry at `_data/projects.yml` line 408 is the same. The repository is live
(`archived` is false; `pushed_at` 2026-09-08T21:14:33Z) and `main` is its default branch.

### 4. Software Functionality (RECOMMENDED — treated as critical)

**Values:**
- Coordinate Transforms
- Coordinate Transforms: Ionospheric
- Coordinate Transforms: Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Data Visualization: Movies
- Data Visualization: Web-Based
- Mission-related
- Mission-related: Analysis
- Mission-related: Instrumentation
- Models and Simulations
- Models and Simulations: Forward-Fitting
- Models and Simulations: Physics-Based

**Every value must be written fully qualified as `Parent: Child`.** The vocabulary has 83 rows, of
which 13 names appear under more than one parent (`2D Slices`, `Analysis`, `Calibration`,
`Distribution/Access`, `Field-line Tracing`, `Infrastructure as Code`, `Instrument Response`,
`ML/AI`, `Mission-Specific`, `Observatory/Instrument Models`, `Packet Decommutation`, `Processing`,
`Spectrogram`). This entry holds **both** `Analysis` rows — the Data Processing and Analysis one and
the Mission-related one — so a bare `Analysis` here is genuinely ambiguous and would bind to
whichever twin the lookup reached first. The same applies to `Calibration`: the row this entry holds
is the Data Processing and Analysis one, not the Mission-related one.

**Parent categories `Mission-related` and `Models and Simulations` are added, and this is a settled
rule rather than a judgement call.** `resource_submission_form_fields.md` line 92 states, of the six
top-level categories, "when a subcategory applies its parent must be listed too (selecting a
subcategory does not auto-add its parent)", and the `software-functionality` skill states the same at
`SKILL.md:30`: "Rule: When a subcategory applies, ALWAYS also include its parent top-level
category." Before this refresh the record held `Models and Simulations: Physics-Based`,
`Mission-related: Analysis` and `Mission-related: Instrumentation` with neither parent, so both
parents were missing. `Coordinate Transforms`, `Data Processing and Analysis` and `Data
Visualization` were already present alongside their children.

*Dependency:* `Mission-related` belongs in the list only for as long as at least one
`Mission-related: *` child does. Both children are retained (see below), so the parent stays; should
a later refresh remove both children, the bare `Mission-related` parent must come out with them.

**Evidence for each retained value**, all at the pinned revision:

- `Coordinate Transforms`, `Coordinate Transforms: Ionospheric` — geographic↔AACGM conversion is a
  user-facing capability, not an internal step. `git grep -l 'aacgmv2' <pin> -- pyaurorax` returns 8
  files, and the calls are `aacgmv2.convert_latlon`/`convert_latlon_arr` with
  `method_code="G2A"`/`"A2G"` in `pyaurorax/search/util/_calculate_btrace.py`,
  `pyaurorax/tools/bounding_box/extract_metric/_mag.py`, `pyaurorax/tools/ccd_contour/_mag.py`,
  `pyaurorax/tools/classes/fov.py`, `pyaurorax/tools/classes/keogram.py`,
  `pyaurorax/tools/classes/mosaic.py`, `pyaurorax/tools/fov/_create_data.py` and
  `pyaurorax/tools/keogram/_create_custom.py`. AACGM is the ionospheric coordinate system the
  `software-functionality` skill names for this subcategory.
- `Coordinate Transforms: Magnetospheric` — `pyaurorax/search/util/__init__.py` exposes
  `ground_geo_to_nbtrace` and `ground_geo_to_sbtrace`, whose module docstring at
  `pyaurorax/search/util/_calculate_btrace.py` reads "Helper functions for calculating the north and
  south B-trace geographic locations for ground-based instruments." These compute the geomagnetic
  conjugate footpoint of a ground site in the opposite hemisphere — a field-aligned mapping, which
  is what this subcategory covers. Noted honestly: the implementation reaches that result through
  AACGM rather than through a magnetospheric field model, so the evidence for this value is thinner
  than for the ionospheric one. It is retained because the user-facing product is a conjugate
  magnetic mapping, which is what a searcher filtering on it is looking for.
- `Data Processing and Analysis`, `: Data Access and Retrieval` — `pyaurorax/data/ucalgary` provides
  dataset listing, download and read functions against the UCalgary open data platform, and
  `pyaurorax/search` provides ephemeris, data-product and conjunction searches against the AuroraX
  search engine (`https://api.aurorax.space`). This is the package's primary purpose.
- `: Calibration` — `pyaurorax/tools/calibration/__init__.py` opens "Perform various calibration
  procedures on image data." and exposes `rego(...)` and `trex_nir(...)` with dark-frame, flatfield
  and Rayleighs-conversion steps (`step_flatfield_calibration`, `step_rayleighs_calibration`).
  Converting raw counts to physical units is exactly this subcategory.
- `: Image Processing` — `pyaurorax/tools/_scale_intensity.py`, `pyaurorax/tools/ccd_contour/`,
  `pyaurorax/tools/grid_files/_prep_grid_image.py` and `pyaurorax/tools/mosaic/_prep_images.py`
  operate on 2-D image arrays as a user-facing capability.
- `: Data Reduction` — keogram creation reduces an image time series to a single 2-D
  time-versus-latitude array (`pyaurorax/tools/keogram/_create.py`,
  `pyaurorax/tools/keogram/_create_custom.py`), and `pyaurorax/tools/bounding_box/extract_metric/`
  ("Extract various metrics from a given bounding box.") reduces a bounded image region to a scalar
  series.
- `: Time Series Analysis` — the same bounding-box metric extraction and the keogram both produce
  and operate on time-ordered sequences of frames.
- `: Analysis`, `: Processing` — the `pyaurorax.tools` module as a whole ("analysis support tools",
  the phrase the test markers use) performs derived-quantity work that neither of the more specific
  subcategories captures alone.
- `Data Visualization`, `: 2D Graphics` — `imshow`/`pcolormesh` appear in 10 files under
  `pyaurorax/` (`git grep -c -P 'imshow|pcolormesh' <pin> -- pyaurorax`), including
  `pyaurorax/tools/classes/keogram.py`, `pyaurorax/tools/classes/montage.py` and the five
  `bounding_box/extract_metric/` modules.
- `: Line Plots` — `pyaurorax/tools/spectra/_plot.py:166` is `plt.plot(wavelength, spectrum, ...)`,
  with the x-axis limits defaulting to the wavelength range at line 188.
- `: Movies` — `pyaurorax/tools/_movie.py` builds an MP4 with `cv2.VideoWriter` and
  `cv2.VideoWriter_fourcc(*"mp4v")`, exposed as `tools.movie(...)`.
- `: Web-Based` — the evidence here is the Swarm-Aurora bridge:
  `pyaurorax/search/conjunctions/swarmaurora/` exposes `get_url(search_obj)` and
  `open_in_browser(search_obj, browser=None)`, which launch a completed conjunction search in the
  Swarm-Aurora Conjunction Finder web application, and the CLI wires the same call
  (`pyaurorax/cli/search/conjunctions/commands.py`). Recorded as a caveat for a future refresh: the
  browser-based visualization being opened is Swarm-Aurora's, not PyAuroraX's own, so this value
  rests on the handoff rather than on any web renderer in this package. It is retained as stored;
  a future refresh that wants to tighten Field 4 should weigh it first.
- `Models and Simulations`, `: Physics-Based` — `pyaurorax/models/atm/__init__.py` exposes
  `ATMManager.forward(...)` and `ATMManager.inverse(...)`, documented as "Perform a forward
  calculation using the TREx Auroral Transport Model and the supplied input parameters" (line 93)
  and "Perform an inverse calculation using the TREx Auroral Transport Model and the supplied input
  parameters" (line 296). A transport model driven by physical equations with a specified NRLMSIS
  background (`ATM_DEFAULT_NRLMSIS_MODEL_VERSION`) fits the skill's `Physics-Based` gloss,
  "Physics-based (broader than first principles)".

**Considered and not selected**, with reasons, so these are not re-proposed:

- `Data Processing and Analysis: Spectrogram` and `Data Visualization: Spectrogram` — no support.
  `git grep -l -P -i '\bspectrogram\b' <pin> -- pyaurorax` returns 0 files. The `tools/spectra`
  module plots a 1-D optical spectrum (`plt.plot(wavelength, spectrum)` at
  `pyaurorax/tools/spectra/_plot.py:166`, x-limits set to the wavelength range at line 188), which
  is already covered by `Data Visualization: Line Plots`. Note the name collision: the TREx
  **Spectrograph** instrument is supported (Field 31), but a spectrograph is not a spectrogram.
- `Data Visualization: Orbit Plots` — no support. `git grep -l -P -i '\borbit\b' <pin> --
  pyaurorax` returns 0 files, and the same pattern scoped to `pyaurorax/search` also returns 0. The
  keyword `orbit` reached Field 16 from the PyHC taxonomy rather than from anything in the code,
  and was removed there for this same reason (see Field 16).
- `Data Processing and Analysis: Energy Spectra` — the "spectra" this package handles are optical
  wavelength spectra from the TREx Spectrograph, not particle energy spectra. `ATMManager.inverse`
  retrieves scalar precipitation parameters (energy flux, characteristic energy) from four optical
  intensities; it does not compute or analyse a spectrum in energy.
- `Data Processing and Analysis: Field-line Tracing` and `Models and Simulations: Field-line
  Tracing` — the B-trace helpers compute a conjugate footpoint via an AACGM round trip
  (`_calculate_btrace.py`: convert to AACGM, negate the magnetic latitude, convert back), not a
  field-line integration through a field model. The magnetic-mapping content of that capability is
  already carried by `Coordinate Transforms: Magnetospheric`.
- `Models and Simulations: Empirical` — the empirical component in the ATM path is the NRLMSIS
  neutral background, which is a parameter of the upstream model rather than a model this package
  implements. Selecting it would tell a searcher that PyAuroraX offers an empirical model, which it
  does not.
- `Data Visualization: Mission-Specific` — keograms, mosaics and montages are conventional all-sky
  imaging products, generic across ASI networks rather than unique to one mission's data types. A
  searcher filtering this value is looking for plot formats peculiar to a single mission.
- `Servers and Environments` and all its children — PyAuroraX is a client library. It ships no
  server, container definition, or HPC tooling; the only workflows at the pin are
  `.github/workflows/tests_all_platforms.yml` and `.github/workflows/tests_default.yml`.

**Why `Models and Simulations: Forward-Fitting` is recorded.** The `software-functionality` skill
defines it as "Synthetic data + parameter optimization | Forward model, chi-square fitting,
inversion", and `pyaurorax/models/atm/__init__.py` exposes exactly `forward()` (line 64) and
`inverse()` (line 280) — a forward model plus an inversion that retrieves precipitation parameters
from measured 4278/5577/6300/8446 Å intensities (`intensity_4278`, `intensity_5577`,
`intensity_6300`, `intensity_8446`). The skill's own definition names inversion, this package's
model interface *is* a forward/inverse pair, and a user searching for forward-modelling and
inversion tools for auroral optical data would want PyAuroraX back — and before this refresh would
not have got it.

The argument against adding it was weighed and did not carry: the optimization is performed
server-side by the TREx-ATM service that `pyucalgarysrs` calls, so this package exposes the
interface rather than implementing the fit, and nothing in this tree does chi-square minimization.
That is a fact about where the computation runs rather than about what capability the software offers
its user, and `Models and Simulations: Physics-Based` on its own tells a searcher only that a model
is reachable here, not that an inversion is.

**Why both `Mission-related` children are kept.** `Mission-related: Analysis` and
`Mission-related: Instrumentation` were both already stored, and both are retained. The
`software-functionality` skill draws the line this way, in its Mission-related section (quoted
verbatim, including the source's own italics and its inner double quotes):

> **Key distinction:** A package that *reads* MMS data is "Data Processing and Analysis: Data Access and Retrieval". A package that is *part of the MMS ground system* is "Mission-related".

PyAuroraX is not a third-party reader. It is written by the University of Calgary Auroral Imaging
Group, which is the instrument team for TREx and REGO, and it is the official client for that team's
data platform — the case Field 31's guidance recognises when it counts "an instrument-team tool".
Its calibration module implements the REGO and TREx NIR calibration procedures (flatfield,
Rayleighs) that belong to those instruments' own processing chain, which is ground-system work in
substance. A searcher browsing `Mission-related: Instrumentation` for ground-based auroral imaging
networks would reasonably expect the networks' own client library.

Removal was the considered alternative and was rejected. On the skill's literal test the user-facing
action is reading and analysing data the platform serves, and `Data Processing and Analysis: Data
Access and Retrieval` and `: Calibration` were already stored and already said so; and a visitor
filtering on `Mission-related` may be looking for mission infrastructure rather than an end-user
analysis library. That reading was judged to undercount an instrument-team tool rather than to
correct an overstatement — and removal would have taken the `Mission-related` parent with it.

### 5. Related Region (RECOMMENDED — treated as critical)

**Values:**
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Magnetosphere
- Earth Thermosphere

`Earth Atmosphere` and `Earth Magnetosphere` were both already stored, and both are retained. The
aurora is an atmospheric emission phenomenon, and the precipitation that drives it is magnetospheric
in origin; the `pyaurorax/search/conjunctions/` module exists specifically to find conjunctions
between ground-based auroral instruments and magnetospheric spacecraft, and `ground_geo_to_nbtrace`
/ `ground_geo_to_sbtrace` exist to support exactly that magnetic mapping.

**The vocabulary is flat and has expanded.** All 24 `Region` rows are top-level: every row's
`parents` and `children` lists are empty. So `Earth Atmosphere` does **not** imply `Earth
Ionosphere` or `Earth Thermosphere`, and a coarse value never stands in for a fine one. The 24 rows
are `Chromosphere`, `Corona`, `Earth Atmosphere`, `Earth Auroral Subregion`, `Earth Inner
Magnetosphere`, `Earth Ionosphere`, `Earth Lower and Middle Atmosphere`, `Earth Magnetosheath`,
`Earth Magnetosphere`, `Earth Magnetotail`, `Earth Outer Magnetosphere`, `Earth Thermosphere`,
`Heliosheath`, `Interplanetary Space`, `Jupiter Magnetosphere`, `Mars Magnetosphere`, `Neptune
Magnetosphere`, `Photosphere`, `Planetary Magnetospheres`, `Saturn Magnetosphere`, `Solar
Environment`, `Solar Interior`, `Solar Wind`, `Uranus Magnetosphere`.

Rows ruled out on the evidence, so they are not re-proposed: every solar and heliospheric row
(`Chromosphere`, `Corona`, `Photosphere`, `Solar Environment`, `Solar Interior`, `Solar Wind`,
`Heliosheath`, `Interplanetary Space`) and every non-terrestrial magnetosphere row — this software
reads ground-based auroral imaging from Canadian and Alaskan sites and runs a terrestrial auroral
transport model. `Earth Magnetosheath` and `Earth Magnetotail` are likewise unsupported: nothing in
the package models or reads data from either region, and the conjunction search's spacecraft side is
a generic ephemeris query rather than a region-specific capability.

**Why the three fine-grained Earth rows were added.** `Earth Auroral Subregion`, `Earth Ionosphere`
and `Earth Thermosphere` are recorded *alongside* the two coarse rows rather than in place of them:
because the vocabulary is flat a coarse row does not imply a fine one, and campaign precedent keeps
a coarse region beside the specific ones rather than treating it as replaced by them.

- **`Earth Auroral Subregion`** — the strongest of the three. The aurora is the software's entire
  subject: `git grep -l -P -i 'aurora' <pin> -- '*.md' '*.toml' 'pyaurorax'` returns 76 files, the
  package name and the platform name both contain it, and every supported instrument is an auroral
  imager. A visitor browsing this region and *not* finding PyAuroraX would be the surprising
  outcome.
- **`Earth Ionosphere`** — the ATM model's outputs are ionospheric quantities. `RELEASE_NOTES.md`
  for version 1.22.0 records renaming the forward function's `plasma_pederson_conductivity` output
  flag to `plasma_pedersen_conductivity`; conductivity of that kind is an ionospheric quantity, and
  the inverse function retrieves precipitation parameters that deposit their energy in the
  ionospheric E region. AACGM, the coordinate system used throughout, is itself an ionospheric
  coordinate system.
- **`Earth Thermosphere`** — the same model's neutral background is NRLMSIS
  (`ATM_DEFAULT_NRLMSIS_MODEL_VERSION`), a thermosphere/upper-atmosphere model, and the emissions
  it computes originate at thermospheric altitudes. The PyHC taxonomy tag
  `ionosphere_thermosphere_mesosphere` (stored as a Keyword) reflects the same judgement, though it
  is a registry tag rather than code evidence.

Two further Earth rows were assessed and deliberately **not** selected, recorded so a later refresh
does not read the flat vocabulary's expansion as an invitation to select every nearby row:

- **`Earth Inner Magnetosphere` / `Earth Outer Magnetosphere`** — the conjunction search does not
  distinguish inner from outer magnetosphere, so selecting either would assert a specificity the
  software does not have.
- **`Earth Lower and Middle Atmosphere`** — auroral emission and the ATM model both live above the
  mesopause; this row would point a searcher at the wrong altitude range.

Leaving the two stored rows as the whole answer was also weighed and rejected. `Earth Atmosphere`
plus `Earth Magnetosphere` is not wrong, and the pair does place the software in the right broad
neighbourhood; but a visitor filtering the catalogue by `Earth Auroral Subregion` — the one region
this software is unambiguously about — would not have seen it.

### 6. Authors (MANDATORY)

**Author 1:**
- **Author:** Darren Chaddock
- **Author Identifier:** https://orcid.org/0009-0008-9481-1184
- **Affiliation:** University of Calgary — https://ror.org/03yjb2x39

**Author 2:**
- **Author:** Josh Houghton
- **Author Identifier:** https://orcid.org/0009-0007-1558-2639
- **Affiliation:** University of Calgary — https://ror.org/03yjb2x39

**Author 3:**
- **Author:** Emma Spanswick
- **Author Identifier:** https://orcid.org/0000-0001-8003-5091
- **Affiliation:** University of Calgary — https://ror.org/03yjb2x39

**Author 4:**
- **Author:** Eric Donovan
- **Author Identifier:** https://orcid.org/0000-0002-8557-4155
- **Affiliation:** University of Calgary — https://ror.org/03yjb2x39

The numbering above is the **Zenodo deposit's credit order** (Chaddock, Houghton, Spanswick,
Donovan), which is the authors' own stated order of credit. It is not HSSI's stored order and must
not be used as an index when editing: identify an author by name, never by position.

**The set of four is right, and it is a union of two sources rather than either one alone.**
`pyproject.toml` at the pin names only two people, in both roles:
`authors = ["Darren Chaddock <dchaddoc@ucalgary.ca>", "Josh Houghton <joshua.houghton1@ucalgary.ca>"]`
and the identical `maintainers` list. The Zenodo/DataCite concept deposit adds two more, giving
creators `Chaddock, Darren`, `Houghton, Josh`, `Spanswick, Emma`, `Donovan, Eric`, each with
affiliation `University of Calgary` and each with an empty `nameIdentifiers` list. Taking the union
is deliberate: dropping Spanswick and Donovan would contradict the deposit the project cites in its
own README, and dropping either of the packaging authors would contradict the package metadata.
There is no `CITATION.cff`, `.zenodo.json` or `codemeta.json` at the pin to reconcile against.

**The four ORCIDs were applied to the four stored author records by database-side correction on
2026-09-09.** Each was resolved by fielded search on `pub.orcid.org/v3.0/expanded-search`, using
`given-names:X AND family-name:Y` rather than a bare name query, and each returned exactly one
record (`num-found` 1). The instrument discriminates rather than merely returning one hit: the
control `given-names:Michael AND family-name:Hirsch` returns `num-found` 7. Each identification is
then confirmed against the full ORCID record:

- **0009-0008-9481-1184** Darren Chaddock — one employment, University of Calgary, department
  `Physics and Astronomy`, from 2011, disambiguated by ROR `https://ror.org/03yjb2x39`. Four works,
  including "Introduction to TREx‐ATM V2.0: A Versatile Model of Auroral Transport and Its Effects
  in the Ionosphere" — the model this library's `models/atm` module exposes.
- **0009-0007-1558-2639** Josh Houghton — one employment, University of Calgary, department
  `Physics and Astronomy`, from 2019, ROR `https://ror.org/03yjb2x39`. Five works, including the
  same TREx-ATM V2.0 paper. Note the near miss recorded so it is not repeated: a search for
  `given-names:Joshua AND family-name:Houghton` also returns exactly one record,
  `0009-0002-7386-5446`, whose employment is the University of Warwick. That is a different person,
  and the `Josh`/`Joshua` variant is the only thing distinguishing the two queries.
- **0000-0001-8003-5091** Emma Spanswick — two employments, both University of Calgary: department
  `Physics and Astronomy ` (with a trailing space in the ORCID record) as Assistant Professor, and
  department `Auroral Imaging Group` as Co-director. Both are disambiguated by Ringgold 2129 rather
  than by a ROR, which is why her record does not itself supply the ROR used above. 111 works,
  including "SMILE All Sky Imager Dataset" and "AuroraX - an open data platform for auroral
  science".
- **0000-0002-8557-4155** Eric Donovan — five employments: University of Calgary `Physics and
  Astronomy` Professor from 1987 (Ringgold 2129); `Faculty of Science` Associate Dean Research
  2016–2018 (ROR `https://ror.org/03yjb2x39`); `Physics and Astronomy` Canada Research Chair (Tier
  II) 2003–2013 and PostDoctoral Fellow 1995–1997 (both keyed by Funder ID rather than ROR); and
  Swedish Institute of Space Physics, Uppsala Avdelningen, PostDoctoral Fellow 1994–1995. 256 works,
  heavily auroral. The Swedish affiliation is a 1994–95 postdoc, not a current one, so it is
  deliberately not recorded as an affiliation here.

None of the four ORCID records carries a credit-name or any other-names entry, so there is no
alternative name form to reconcile.

**Why the ORCIDs are not a routine metadata update.** Each of the four author records existed in
HSSI with no identifier at all before this refresh. Sending an ORCID for an identifier-empty stored
person does not fill the existing record in place; it resolves to a *new* person and leaves the
original orphaned and still attached elsewhere. That is why these four identifiers were applied as a
database-side correction rather than through a field update, and the constraint outlives this
refresh: a future agent that finds the identifiers present should read this note as the explanation
of how they got there and leave them alone, and one that finds an identifier missing on any author
must not try to add it through a field update.

**Affiliation.** `University of Calgary`, ROR `https://ror.org/03yjb2x39`. The ROR record's `names`
give `University of Calgary` (`ror_display`, `label`), `Université de Calgary` (`label`) and `UoC`
(`acronym`), located in Calgary. This is also what the Zenodo deposit gives as the creators'
affiliation string and what Chaddock's and Houghton's ORCID employments are disambiguated to.

**Previous incorrect value — do not restore it.** An earlier extraction recorded the affiliation
identifier as `https://ror.org/03waa3d44` for all four authors. That is not the University of
Calgary and not any organization: `https://api.ror.org/organizations/03waa3d44` returns HTTP 404,
no such record. `https://ror.org/03yjb2x39` is the correct identifier.

**Contributors considered and not added.** The git author table at the pin
(`git log --format='%an <%ae>' <pin> | sort | uniq -c`) is:

```
643 Darren Chaddock <dchaddoc@ucalgary.ca>
 84 Maryam Sohrabi <sohrabm@ucalgary.ca>
 72 Maryam Sohrabi <sohrabi.mar@gmail.com>
 67 joshh <joshua.houghton1@ucalgary.ca>
 25 Maryam Sohrabi <47364636+marsohrabi@users.noreply.github.com>
  5 marsohrabi <47364636+marsohrabi@users.noreply.github.com>
  3 Roddi <potter.rod@gmail.com>
```

Maryam Sohrabi accounts for four rows of that table but only three distinct email addresses: the
`Maryam Sohrabi` and `marsohrabi` rows differ solely in the recorded display name and share the
address `47364636+marsohrabi@users.noreply.github.com`, which ties them to one GitHub account, while
`sohrabm@ucalgary.ca` ties her to the University of Calgary. Her four rows together are 186 of the
commits reachable from the pin — more than any declared `pyproject.toml` author except Chaddock.
`Roddi <potter.rod@gmail.com>` has 3. Neither is a declared author in `pyproject.toml` nor a creator on the
Zenodo deposit, and Field 6 records the authorship the project asserts rather than a commit ranking,
so neither is added. This is recorded rather than silently omitted because the commit volume makes
the omission look like an oversight when it is not. **What would change it:** Sohrabi appearing in a
`pyproject.toml` `authors` list, in a `CITATION.cff`, or as a creator on a future Zenodo deposit
would make her an author here on the same basis as Spanswick and Donovan.

### 7. Software Name (MANDATORY)
- **Value:** PyAuroraX

The project's own capitalisation, agreeing across every authoritative source: `README.md` at the pin
opens its description "PyAuroraX is a Python library providing data access and analysis support for
All-Sky Imager data", the PyHC registry entry at `_data/projects.yml` line 408 is
`- name: "PyAuroraX"`, and the DataCite title begins `PyAuroraX and IDL-AuroraX`. The distribution
name is lower-case `pyaurorax` (`pyproject.toml` `name = "pyaurorax"`, and the PyPI project of that
name), but that is the packaging identifier rather than the software's name, and the mixed-case form
is what the project uses in prose and in its logo.

### 8. Description (MANDATORY)
- **Value:** PyAuroraX is a Python library providing data access and analysis support for All-Sky Imager data (THEMIS, TREx, REGO, SMILE, etc.), the ability to utilize the TREx Auroral Transport Model, and interact with the AuroraX Search Engine. AuroraX is a project working to be the world's first and foremost data platform for auroral science. The primary objective is to enable mining and exploration of existing and future auroral data, enabling key science and enhancing the benefits of the world's investment in auroral instrumentation. We have developed key systems/standards for uniform metadata generation and search, image content analysis, interfaces to leading international tools, and a community involvement that includes more than 80% of the world's data providers. PyAuroraX will significantly lower the barrier of entry to the global network of auroral data, and provide the foundation for efficiency and inter-operability of existing auroral instrument networks and data streams.

The stored value is kept as it is: it reads well, is the project's own prose, and covers both what
the library does and what the platform is for. But its composition is unobvious enough that a future
refresh could damage it by "correcting" it, so it is documented precisely here.

**It is a splice of two sources, and it is not a verbatim quotation of either.** The first four
sentences are the opening paragraph of `README.md` at the pin, with one alteration: the README
renders the platform name as the inline link `[AuroraX](https://aurorax.space)`, and the stored copy
has that flattened to plain `AuroraX`. With that single substitution applied, the stored value
begins with the README paragraph character for character (769 characters), and the remainder is
exactly one further sentence.

**That final sentence appears nowhere in the repository, at the pin or in its history.**
`git grep -c -F 'significantly lower the barrier of entry' <pin>` returns 0 files, and
`git log -S 'significantly lower the barrier of entry' -- README.md` finds no commit that ever added
or removed it. It is adapted from the Zenodo deposit's abstract, whose second paragraph opens
"AuroraX will significantly lower the barrier of entry to the global network of auroral data, and
provide the foundation for efficiency and inter-operability of existing auroral instrument networks
and data streams." The stored copy substitutes **PyAuroraX** for **AuroraX** in that sentence and is
otherwise identical to it.

The substitution is a defensible editorial choice for a record about PyAuroraX rather than about the
platform, and it is left alone. Two things a later refresh must therefore not do: treat the stored
description as a verbatim README quotation (it is not — the markdown link is flattened and the last
sentence is not in the README), and "restore" the last sentence to the Zenodo wording or delete it
as unsourced.

### 9. Concise Description (OPTIONAL)
- **Value:** Python library supporting data access and analysis for All-Sky Imager (ASI) data

The project's own one-line summary, and it is the same string in two independent places: the GitHub
repository's `description` field, and the PyHC registry's `description:` for the entry at
`_data/projects.yml` line 408. Considered and not used: `pyproject.toml`'s
`description = "Python library for interacting with the AuroraX platform"`, which is accurate but
tells a browsing visitor less — it names the platform without naming the data. The stored value
survives on the searcher's-side test: someone scanning a results list learns from it that this is
Python, that it is for ASI data, and that it does both access and analysis.

### 10. Publication Date (RECOMMENDED)
- **Value:** 2020-06-13

**This corrects a previous value of `2024-06-25`**, which was the registration date of the Zenodo
1.0.0 deposit (`10.5281/zenodo.12532077`, DataCite `dates`
`[{'date': '2024-06-25', 'dateType': 'Issued'}]`, which the concept record mirrors) rather than what
this field asks for. The form defines the field as "Date of first broadcast/publication." and its
"How to fill it" as "Used for the initial version of the software."
(`resource_submission_form_fields.md`, Field 10, lines 271 and 273.)

Three independent sources give `2020-06-13` as the software's first publication. PyPI's `pyaurorax`
release history has 87 releases, all with files, of which the earliest is 0.0.1 uploaded
`2020-06-13T22:32:09Z` (the second, 0.0.2, is 2020-09-05, so 0.0.1 is not an anomalous backfill).
The GitHub repository was created `2020-06-13T21:40:58Z`, 51 minutes earlier — the same day in UTC
and the same day in Calgary local time. And Zenodo's own three pre-1.0 version deposits,
`10.5281/zenodo.5815985` (0.8.0), `10.5281/zenodo.5816001` (0.9.2) and `10.5281/zenodo.6098075`
(0.9.2), each carry DataCite `Issued` date `2020-06-13`. On the field's own definition this is the
answer: the initial version of the software was published in June 2020, more than three and a half
years before the 1.0.0 deposit.

Keeping `2024-06-25` was the alternative, and its one merit was internal tidiness: it is the issue
date of the DOI recorded in Field 2, so the two fields agreed with each other and with what a
visitor following the citation sees. It was rejected because the field is not defined as "the date of
the persistent identifier", and reading it that way makes an entry's publication date jump forward
whenever a project first mints a DOI, which is not the question the form asks.

One caution on the corroborating evidence, so it is not over-read: all three pre-1.0 Zenodo version
deposits carry the *same* `Issued` date of 2020-06-13 despite being different versions, which means
that date was applied to the deposits rather than derived per-version. It corroborates 2020-06-13 as
the project's own account of when it first published, and should not be read as three separate
release dates.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Correct as stored, and kept. The DataCite record for the concept DOI gives
`publisher` `Zenodo`, which is where the software deposit is published.

**Previous incorrect value — do not restore it.** An earlier extraction recorded the publisher
identifier as `https://ror.org/04xfq0f34`. That ROR belongs to a different institution entirely:
`https://api.ror.org/v2/organizations/https://ror.org/04xfq0f34` returns names `RWTH Aachen
University` (`ror_display`, `label`), `Rheinisch-Westfälische Technische Hochschule Aachen`
(`label`), `RWTH Aachen` (alias) and `RWTH` (acronym). It has nothing to do with Zenodo, and
`https://zenodo.org` is the correct identifier.

### 12. Version (RECOMMENDED)

**Current release at the pinned revision:**
- **Version Number:** 1.23.0
- **Version Date:** 2026-09-08
- **Version Description:** (empty)
- **Version PID:** Not found — no Zenodo deposit exists for any version after 1.0.0

**Previously stored version row (superseded):**
- **Version Number:** 1.0.0
- **Version Date:** 2024-06-25
- **Version PID:** https://doi.org/10.5281/zenodo.12532077
- **Version Description:** (empty)

**Evidence that 1.23.0 is the current release**, from five independent places that agree:
`pyproject.toml` `version = "1.23.0"`; `pyaurorax/__init__.py:35` `__version__ = "1.23.0"`;
`RELEASE_NOTES.md:1` `Version 1.23.0 (2026-09-08)`; the GitHub release `v1.23.0` published
2026-09-08T21:13:39Z; and the PyPI `pyaurorax` 1.23.0 file upload at 2026-09-08T21:06:17Z. The
pinned commit is one commit past the `v1.23.0` tag, so the tag is an ancestor of the pin rather than
the pin itself.

**Why the version row was refreshed to 1.23.0 / 2026-09-08.** The row HSSI held before this refresh
was two years and 23 minor releases behind the software; a visitor reading the entry learned that
PyAuroraX is at 1.0.0, which is wrong in a way that affects whether they trust the rest of the
record. **The consequence, accepted deliberately:** the Version PID is cleared, because 1.23.0 has
no DOI — Zenodo holds only four version deposits, the newest being 1.0.0 (see Field 2). The refresh
therefore trades a correct-but-stale version carrying a DOI for a correct-and-current version
carrying none.

Keeping 1.0.0 / 2024-06-25 with its DOI was the alternative. That row is internally coherent — the
version really does have that date and that DOI — and it is the version the Field 2 concept DOI
resolves to. It was rejected because the entry would go on misreporting the software's current
version, which is the thing this field most plainly exists to tell a visitor.

Two further facts a future refresh should have:

- **The 1.0.0 row's date 2024-06-25 was the Zenodo deposit's issue date, not the release date.** The
  GitHub release `v1.0.0` was published 2024-06-23T22:44:25Z, two days before the deposit was
  registered. The 2024-06-25 value came from Zenodo, not from the release.
- **Replacing this field orphans the stored 1.0.0 row rather than editing it.** That is accepted
  campaign behaviour and not a defect; it is recorded here so a later reader does not read a
  detached 1.0.0 row as evidence of a botched update.

**Why the version description is left empty.** No release carries a descriptive *title* — for all
40 releases the API's `name` equals its `tag_name`, so there is no short human-written label to lift
— and the empty field was preferred to either of the two sourced alternatives below. Both were
available and both were declined; the earlier extraction's text was neither of them, and is rejected
separately at the end of this field.

- **Declined — the release's own body text, `Refer to RELEASE_NOTES for further information.`** This
  is authored project prose, not a synthesis: it is the verbatim `body` of the `v1.23.0` GitHub
  release, and of 30 of the 40 releases. It is also exactly what an earlier extraction recorded for
  1.20.0 — that value was the release body, correctly copied. It was declined because it is a
  pointer rather than a description, and tells a visitor nothing about what changed.
- **Declined — the release notes' own summary of 1.23.0.** `RELEASE_NOTES.md` lines 1–5 at the pin read:
  ```
  Version 1.23.0 (2026-09-08)
  -------------------
  - added `--api-timeout` option to the CLI for setting the API request timeout
  - multiprocessing in `tools.movie()` and `tools.mosaic.prep_skymaps()` now uses the `forkserver` start method where available, adopting the Python 3.14 default
  - test suite updates
  ```
  Recording these three bullets (or a faithful condensation of them) would have asserted only what
  the source says and would genuinely have informed the visitor. It was declined because it needs
  light editorial joining to read as prose and goes stale at the next release like any version
  description, and an empty field was preferred to a description with that short a shelf life.

Explicitly rejected: the earlier extraction's `Major release - v1.0.0. A significant upgrade with
major code reorganization and addition of many new features, including breaking changes from v0.13.3
and earlier.` That is a synthesis of `README.md` lines 55–60 ("Migrating from V0 to V1": "A
significant upgrade was released for PyAuroraX for version 1.0.0. A major code reorganization and
addition of many new features is part of version 1.x, and therefore includes breaking changes. The
existing codebase from v0.13.3 and earlier has remained mostly unchanged…"), reworded into a
sentence no source contains. The v1.0.0 release's own body is shorter and differently worded:
`Major release - v1.0.0. Refer to RELEASE_NOTES for futher information.` — including the
project's own `futher` typo, which is the clearest single proof the extraction's text was not
copied from the release.

### 13. Programming Language (RECOMMENDED)

**Values:**
- Python 3.x

`Python 3.x` is beyond doubt: 424 of the 571 files tracked at the pin are `.py`
(`git ls-tree -r --name-only <pin> | grep -c '\.py$'`), `pyproject.toml` declares
`python = ">=3.10"`, PyPI reports `requires_python` `>=3.10`, and `README.md` states "PyAuroraX
officially supports Python 3.10+."

**Why `IDL` was removed.** HSSI stored `IDL` alongside `Python 3.x` before this refresh; it is
removed, leaving Python alone. The form's criterion is byte-exact: "The computer programming
languages most important for the software." and "Select the most important languages (e.g., Python,
Fortran, C). This is not meant to be an exhaustive list."
(`resource_submission_form_fields.md`, Field 13, lines 308 and 310.)

Evidence bearing on it, all at the pin:

- **No IDL source exists in this repository.** `git ls-tree -r --name-only <pin> | grep -c '\.pro$'`
  is 0.
- **Neither the package nor its own documentation mentions IDL at the pin.**
  `git grep -l -P -i '\bidl\b' <pin> -- pyaurorax README.md RELEASE_NOTES.md DEVELOPER_GUIDE.md`
  returns 0 files. (This is a statement about the pinned tree, not about the whole history.)
- **Whole-tree, the token appears in 5 files, all example notebooks**, and every occurrence is a
  dataset name or a dataset description rather than a language reference:
  `examples/notebooks/data/download_skymaps_and_calibrations.ipynb`,
  `examples/notebooks/data/explore_datasets_and_observatories.ipynb`,
  `examples/notebooks/tools/add_contours_to_ccd_image.ipynb`,
  `examples/notebooks/tools/keogram_trex_blue.ipynb`,
  `examples/notebooks/tools/plot_fov_maps.ipynb`. The matches read like
  `REGO All Sky Imagers skymap data (IDL save format)` and
  `Dataset(name=TREX_SPECT_SKYMAP_IDLSAV, short_description='TREx Spectrograph skymap data (IDL save format)'`.
  That is IDL as a **data format this software consumes**, which is recorded as `IDL.sav` in
  Field 18 — not as a language it is written in.

**The deciding argument is the searcher's-side question.** Ask what someone filtering HSSI on `IDL`
wants to be able to *do* with the result: read, run, modify or contribute IDL code. This repository
offers none — no `.pro` files, no IDL entry point, no IDL documentation. They would have to
discover, unprompted, that a different repository exists. And the deposit title is evidence about the
*deposit*, which covers two libraries; it is not evidence about the software this HSSI record
describes.

**The case for keeping it, and why it did not carry.** The Zenodo deposit this entry cites in Field 2
is titled `PyAuroraX and IDL-AuroraX - data access and analysis support libraries for All-Sky Imager
(ASI) data`, and its DataCite `subjects` include `idl`. The IDL counterpart is genuinely part of the
same project by the same team, so a visitor who finds this record under an IDL filter has not been
sent somewhere irrelevant to the AuroraX libraries. But that is a property of the shared deposit
rather than of this software, and the filter would still hand them a repository with no IDL in it.

**Where the removed information went.** The IDL counterpart lives at
`https://github.com/aurorax-space/idl-aurorax` (GitHub reports its `language` as `IDL` and describes
it as "IDL library supporting data access and analysis for All-Sky Imager (ASI) data"), and it is
recorded in Field 29 — which puts an IDL user one legible click from what they actually want, without
this field claiming the software is written in IDL.

Recorded as a correction to an earlier extraction's reasoning: it justified `IDL` on the deposit
title alone and also stated the requirement as "Python >= 3.9". The pin says `python = ">=3.10"`.

### 14. Reference Publication (OPTIONAL)

- **Value:** https://doi.org/10.3389/fspas.2022.1009450

HSSI held no value for this field before this refresh. There is no JOSS paper, no `CITATION.cff` and
no `preferred-citation` anywhere at the pin, and the DataCite concept record carries no
`IsDescribedBy`, `IsCitedBy` or `IsSupplementTo` relation — its only relations are the four
`HasVersion` links to its own version deposits. So nothing in the software's own metadata nominates
a reference publication.

**The article recorded here was found through the authors rather than the repository:**

> Shumko, M., Chaddock, D., Gallardo-Lacourt, B., Donovan, E., Spanswick, E. L., Halford, A. J.,
> Thompson, I., and Murphy, K. R. (2022), "AuroraX, PyAuroraX, and aurora-asi-lib: A user-friendly
> auroral all-sky imager analysis framework", *Frontiers in Astronomy and Space Sciences*.
> https://doi.org/10.3389/fspas.2022.1009450

It names PyAuroraX in its title, three of this record's four authors are co-authors, and its Author
contributions statement reads "ED, ES, and DC designed and developed the AuroraX platform and
PyAuroraX. AH, KM, and IT assisted MS with developing aurora-asi-lib." Published 2022-09-26.

**Why it is recorded as the reference publication.** The form defines this field as "The DOI for
the publication describing the software, sometimes used as the preferred citation for the software in
addition to the version-specific citation to the code itself." This article describes the software,
is peer-reviewed, and is authored by the developers; a visitor looking for something to cite is
better served by it than by nothing, and it is the article a reader of the literature would
recognise.

The reservation was weighed and did not prevail. The article describes three things — the AuroraX
platform, PyAuroraX, and aurora-asi-lib/asilib — and the project nowhere presents it as PyAuroraX's
preferred citation (the README's only citation pointer is the Zenodo DOI badge), so a field that
renders as *the* reference publication arguably overstates how specifically it is about this library;
Field 27's looser "describe, cite, or use" would have accommodated it instead. It is recorded here
because "the publication describing the software" is nonetheless what it is, and because Field 27
carries the TREx-ATM V2.0 paper, which is the paper a user of the model actually needs.

Field 2 keeps the Zenodo concept DOI, so this field does not stand in for a software citation: the
entry carries both, each under its own correct heading.

### 15. License (RECOMMENDED)
- **Value:** Apache License 2.0

HSSI held no license value before this refresh; `Apache License 2.0` is a row in the 11-row `License`
vocabulary, so it is directly selectable. Four independent sources agree:

- **`LICENSE` at the pin** is the Apache-2.0 short-form notice rather than the full licence text —
  line 1 is `Copyright 2024 University of Calgary` and line 3 is
  `Licensed under the Apache License, Version 2.0 (the "License");`. The same 13-line header is
  repeated at the top of the Python sources (for example `pyaurorax/__init__.py` lines 1–13).
- **`pyproject.toml`** declares `license = "Apache License 2.0"` — already the vocabulary row's
  exact spelling.
- **PyPI** reports `license` `Apache-2.0` with the classifier
  `License :: OSI Approved :: Apache Software License`.
- **Zenodo/DataCite** gives `rightsList` `[{'rights': 'Apache License 2.0', ... 'rightsIdentifier':
  'apache-2.0', 'rightsIdentifierScheme': 'SPDX'}]` on both the concept record and the 1.0.0 version
  record.

**Why GitHub reports no licence, so this is not re-investigated later.** The GitHub API returns
`license` `{'key': 'other', 'name': 'Other', 'spdx_id': 'NOASSERTION'}` for this repository. That is
a consequence of the `LICENSE` file holding the short-form notice instead of the full Apache text —
GitHub's detector needs the full text to assign an SPDX id. It is not evidence of an unclear
licence, and `Other` must not be selected on the strength of it.

**There is no "License URI" to record, and an earlier extraction was wrong to present one.** It gave
`License URI: http://www.apache.org/licenses/LICENSE-2.0`, which is the `rightsUri` from the
DataCite record. HSSI's software licence is a foreign key to a shared `License` row, and the URL
lives on that shared row — so there is no per-software licence URI anywhere in storage, and any
value entered as one would be discarded. (For the record, the shared `Apache License 2.0` row's own
url is `https://spdx.org/licenses/Apache-2.0`, not the apache.org URL.) The repository `LICENSE`
file remains perfectly good *evidence* for the licence; it is just not a second storable value.

**DOI-autofill trap, recorded because it would silently produce the wrong answer.** The three oldest
Zenodo version deposits carry a *different* licence: `10.5281/zenodo.5815985` (0.8.0),
`10.5281/zenodo.5816001` (0.9.2) and `10.5281/zenodo.6098075` (0.9.2) all report `rightsList`
including `('MIT License', 'mit')`, while the 1.0.0 deposit and the concept both report
`apache-2.0`. An autofill or a refresh that reached for an older version record would set this field
to `MIT License`. The licence must be derived from the repository, which is unambiguous.

### 16. Keywords (OPTIONAL)

**Values (22), byte-exact:**
`2d graphics`, `All-sky imager`, `aurora`, `aurora borealis`, `Auroral conjunctions`,
`auroral emissions`, `aurorax`, `calibration`, `coordinates`, `data container`,
`data retrieval`, `image processing`, `instrumentation`,
`ionosphere thermosphere mesosphere`, `Keogram`, `line plots`, `multidimensional`,
`northern lights`, `plotting`, `python`, `southern lights`, `space physics`.

**Where these came from.** The 20 values HSSI held before this refresh decomposed cleanly into
three sources, and that decomposition is what decided which of them survived.

- **Six from the project itself.** `pyproject.toml` at the pin declares
  `keywords = ["aurorax", "space physics", "aurora", "aurora borealis", "northern lights", "southern lights"]`.
  Five were stored verbatim; the sixth was stored as the misspelling `norther lights`, corrected in
  this refresh (see below).
- **Twelve from the PyHC registry's taxonomy tags** for this entry (`_data/projects.yml` line 408),
  with underscores replaced by spaces: `ionosphere_thermosphere_mesosphere`, `2D_graphics` →
  `2d graphics`, `calibration`, `coordinates`, `data_container`, `data_retrieval`,
  `image_processing`, `line_plots`, `multidimensional`, `orbit`, `plotting`, `instrumentation`.
- **Two from the Zenodo/DataCite deposit's `subjects`**, which are `python`, `aurora`,
  `space physics` and `idl`: the first and last contribute `python` and `idl`, while `aurora` and
  `space physics` overlap with the project's own list.

That provenance matters because a PyHC taxonomy tag is a registry classification of the package,
not a statement about this code — which is why every inherited tag was tested against the code
rather than kept on the registry's authority. Note in particular that PyHC's own tag list contains
`idl_save`, not `idl` — the `idl` keyword came from the deposit's subjects, and the registry's
`idl_save`, `ascii`, `cdf` and `hdf5` tags are the ones that surfaced in Fields 18/19 instead.

**Keywords are the only open vocabulary in the form** — an unmatched value is created rather than
rejected — so the risk here is minting near-duplicate rows, not failing. Each of the four additions
below matches an existing `Keyword` row exactly and mints nothing; the one corrected value does mint
a row, deliberately.

**The misspelling `norther lights` was corrected to `northern lights`.**
The project spells it `northern lights` in `pyproject.toml`. HSSI held `norther lights`, which
exists as its own `Keyword` row; no `northern lights` row existed at the time of the correction
(checked case-insensitively against the whole live list), so the correction mints one — which is
normal for this open vocabulary and was not a reason to avoid it.

The reason for correcting it is retrieval: `northern lights` is what the project wrote and what a
visitor searching the catalogue will type, whereas under the typo the entry was discoverable only by
someone who reproduced the typo. Two costs are accepted — a new row is created, and the misspelled
row is left behind. Leaving the typo in place would have failed no submission, but it would have
left the keyword effectively unfindable, which is the whole purpose of the field.

**Two inherited tags with no support in this software were removed: `orbit` and `idl`.**
Each stored keyword was tested against what the code does rather than inherited from the registry.
These two failed that test:

- **`orbit`** — `git grep -l -P -i '\borbit\b' <pin> -- pyaurorax` returns 0 files, and the same
  pattern scoped to `pyaurorax/search` (where an ephemeris/conjunction package might plausibly use
  the word) also returns 0. Nothing in this software is about orbits. A visitor who filters the
  catalogue on `orbit` and gets an all-sky-imager library has been misdirected, so the tag is
  removed rather than left standing as a PyHC-taxonomy artefact.
- **`idl`** — removed too, and decided on its own terms rather than as a consequence of Field 13.
  The question was what someone browsing the keyword `idl` expects. If they expect IDL code, this
  record disappoints them (no `.pro` files at the pin). The case for keeping it was that anything
  IDL-adjacent — the IDL-AuroraX sibling library, or the IDL save-format skymap and calibration
  files this software reads — makes the tag apt, and that a keyword can honestly record "IDL is in
  this software's world" even where IDL is not a language the software is written in. That case was
  not accepted: those IDL-adjacent facts are already carried precisely, by `IDL.sav` in Field 18 and
  by the `idl-aurorax` relation in Field 29, while a bare `idl` keyword promises IDL code this
  record does not have.

The remaining eleven registry-derived tags do hold up, and are retained:
`2d graphics`, `calibration`, `coordinates`, `data retrieval`, `image processing`, `line plots`,
`plotting` and `instrumentation` all correspond to capabilities evidenced in Field 4;
`ionosphere thermosphere mesosphere` matches the ATM model's output domain (see Field 5);
`data container` matches the `Keogram`, `Montage`, `Mosaic`, `FOV`, `Skymap` and `Calibration`
classes the package exposes; and `multidimensional` matches its image-cube data model.

**Four keywords were added, each binding to an existing row.**
All four names below were verified present in the live `Keyword` vocabulary and are written
byte-for-byte as the rows carry them, including capitalisation, so none of them mints a row.

- **`Keogram`** — the software's signature product, with a whole subpackage and class devoted to it:
  `pyaurorax/tools/keogram/__init__.py`, `pyaurorax/tools/keogram/_create.py`,
  `pyaurorax/tools/keogram/_create_custom.py` and `pyaurorax/tools/classes/keogram.py` ("Class
  representation for a keogram"). The row is capitalised `Keogram`; a lower-case `keogram` row does
  not exist, so the capitalised form is the one to use (a case variant would bind to this row
  anyway, since no case-variant collision groups exist in the list).
- **`All-sky imager`** — the software's entire subject, named in its own concise description. Three
  near-duplicate rows exist: `All-sky imager`, `all-sky-imager` and `all-sky-camera`. **The intended
  value is `All-sky imager`**, the space-separated form, because it is the form a person types and
  the form the project itself uses ("All-Sky Imager data" in the README, "(ASI)" in the concise
  description); the hyphenated `all-sky-imager` reads as a machine tag and `all-sky-camera` names a
  different instrument word. Note that `asi` and `all sky imager` (unhyphenated) do **not** exist as
  rows and would mint.
- **`Auroral conjunctions`** — a core feature, not an incidental one:
  `pyaurorax/search/conjunctions/` is one of the search module's main managers, its docstring reads
  "Use the AuroraX search engine to find conjunctions between groupings of data sources.", and it
  exposes `search`, `search_from_raw_query`, `describe` and the Swarm-Aurora bridge. The row is
  capitalised `Auroral conjunctions`; a bare `conjunction` row does not exist.
- **`auroral emissions`** — what the ATM model computes and what the spectrograph tooling measures.
  This is also the row that carries the concept Field 22 cannot (see Field 22 below). Two related
  rows exist and were considered but not added: `auroral optical emissions`, a narrower synonym for
  which one row per concept is enough, and `particle precipitation`, which remains a defensible
  future addition should the precipitation side of `ATMManager.inverse` need to be discoverable,
  since that function retrieves precipitation parameters from measured intensities.

**Explicitly rejected: `physics`.** It exists as a row, and it is one of the repository's GitHub
topics (`aurora`, `physics`, `python`, `space-physics`), but on a heliophysics catalogue it
distinguishes nothing — the same tag would be equally true of most of the collection, so it adds no
retrieval value for a visitor.

### 17. Data Sources (OPTIONAL)

**Values:**
- HTTP/HTTPS Directories
- Observatory/Mission-specific

Correct as stored, and confirmed against the code rather than carried over. All data access is HTTPS:
`pyproject.toml` names `https://data.phys.ucalgary.ca` as the "UCalgary SRS Open Data Platform" URL,
the search engine base is `https://api.aurorax.space` (referenced in `pyaurorax/search`), and both
are served as HTTPS directory trees / HTTPS API endpoints. `Observatory/Mission-specific` is right
because the archive is not a general-purpose multi-mission repository: it is the University of
Calgary's own platform serving its own and its partners' auroral instrument networks, with per-array
readers (`read_themis`, `read_rego`, `read_trex_nir`, `read_trex_blue`, `read_trex_rgb`,
`read_trex_spectrograph`, `read_smile`). That is exactly the observatory-specific case Field 31's
guidance describes.

**The other 15 rows in the 17-row `DataInput` vocabulary are ruled out by direct check**, so they
are not re-proposed. Scoped to `pyaurorax` at the pin, `git grep -l -P -i '\b<token>\b'` returns 0
files for every one of `hapi`, `cdaweb`, `madrigal`, `omniweb`, `sscweb`, `amda`, `vires`, `ftp`,
`s3`, `das2` and `boto` — so `AMDA`, `CDAWeb`, `FTP/FTPS Directories`, `HAPI`, `Madrigal`,
`OMNIWeb`, `S3/Cloud-aware`, `SSCWeb`, `VirES` and `das2` all have no support. `GFZ`, `TAP`, `WDC`
and `The Virtual Solar Observatory.` (note that row's trailing period) are likewise unsupported —
this is a ground-based auroral client, not a solar or geomagnetic-index client. `Other` is
unnecessary because the two selected rows already describe the access mechanism and the archive
type.

### 18. Input File Formats (RECOMMENDED)

**Values:**
- HDF5
- IDL.sav
- Other

### 19. Output File Formats (RECOMMENDED)

**Values:**
- JSON
- Other

**Before this refresh the two fields held identical lists, and that was itself the problem.** Input
and output are different questions for this software: it reads instrument data in several formats and
writes figures, movies and JSON. Both inherited lists traced to the PyHC taxonomy tags `ascii`,
`binary`, `cdf`, `hdf5`, `idl_save` (see the Scope note), which classify the *package* rather than
distinguishing read from write. The two lists above no longer coincide, because each was derived from
the code separately.

**What the software actually reads**, per the reader docstrings in
`pyaurorax/data/ucalgary/read/__init__.py` at the pin, quoted verbatim from that file:

| Reader | Docstring |
|---|---|
| `read_themis` (line 167) | `Read in THEMIS ASI raw data (stream0 full.pgm* files).` |
| `read_rego` (line 248) | `Read in REGO raw data (stream0 pgm* files).` |
| `read_trex_nir` (line 326) | `Read in TREx near-infrared (NIR) raw data (stream0 pgm* files).` |
| `read_trex_blue` (line 404) | `Read in TREx Blueline raw data (stream0 pgm* files).` |
| `read_trex_rgb` (line 483) | `Read in TREx RGB raw data (stream0 h5, stream0.burst png.tar, unstable stream0 and stream0.colour pgm* and png*).` |
| `read_trex_spectrograph` (line 562) | `Read in TREx Spectrograph raw data (stream0 pgm* files).` |
| `read_smile` (line 640) | `Read in SMILE ASI raw data (L0 raw h5 files).` |
| `read_skymap` (line 716) | `Read in UCalgary skymap files.` |
| `read_calibration` (line 760) | `Read in UCalgary calibration files.` |
| `read_grid` (line 806) | `Read in grid files.` |

One fidelity note on that table: `read_trex_rgb`'s docstring wraps in the file across lines 483–484
(`… unstable stream0 and` / `stream0.colour pgm* and png*).`) and is quoted above joined into one
line; every other quotation is a single unwrapped line at the stated line number.

So: **PGM** (THEMIS, REGO, TREx NIR/Blue/Spectrograph), **HDF5** (TREx RGB, SMILE ASI, grid files),
**PNG inside a tar** (TREx RGB burst), and the UCalgary **skymap and calibration** files, which are
distributed in IDL save format — the notebooks' dataset descriptions call them exactly that
(`REGO All Sky Imagers skymap data (IDL save format)`, `TREx Spectrograph skymap data (IDL save
format)`, `REGO All Sky Imagers Flatfield calibration data (IDL save format)`). `HDF5` and `IDL.sav`
are therefore well-founded input rows, and `Other` correctly carries PGM and PNG/tar, for which the
11-row `FileFormat` vocabulary has no rows.

**What the software actually writes.** Every output path is a figure, a movie, or JSON:
`plt.savefig(...)` in `pyaurorax/tools/_display.py`, `pyaurorax/tools/classes/fov.py`,
`pyaurorax/tools/classes/keogram.py`, `pyaurorax/tools/classes/montage.py`,
`pyaurorax/tools/classes/mosaic.py` and `pyaurorax/tools/spectra/_plot.py` (the filename's extension
chooses the raster format, with a JPG-quality special case); `cv2.VideoWriter` with
`cv2.VideoWriter_fourcc(*"mp4v")` in `pyaurorax/tools/_movie.py`; and `json.dump(...)` in
`pyaurorax/search/conjunctions/swarmaurora/_swarmaurora.py:54` and in four CLI modules
(`pyaurorax/cli/search/helpers.py:271-275`, and the `conjunctions`, `data_products` and `ephemeris`
command modules, which write query templates). The pattern
`git grep -n -P 'savefig|to_hdf|\.mp4|imwrite|writer' <pin> -- pyaurorax` matches 9 files, all under
`pyaurorax/tools/`, and none of them writes HDF5.

**`CDF` has no support at all, in either direction.**
`git grep -l -P -i '\bcdf\b' <pin>` (whole tree) returns 3 files —
`examples/notebooks/tools/apply_calibration_trex_nir.ipynb`,
`examples/notebooks/tools/keogram_smile_asi.ipynb` and
`examples/notebooks/tools/keogram_trex_blue.ipynb` — and in all three the match is **base64 image
payload inside the notebook JSON**, not a mention of the format (for example the run of characters
`…xVhewSNXJDODRVlzIDhH0id8+Cdf/cY7wZnJeSqY0Hw…` in `keogram_smile_asi.ipynb`). There is no
`cdflib`, `netCDF4` or `spacepy` dependency:
`git grep -n -P -i 'cdflib|netcdf|spacepy' <pin> -- pyproject.toml poetry.lock` returns no output.
The value is a PyHC-tag propagation (`cdf` is in the registry keyword list) and nothing else.

**`ascii` also has no support as a data format** — a finding beyond the CDF one, and it applies to
both fields. `git grep -n -P -i '\bcsv\b|\.txt\b|\bascii\b|savetxt|loadtxt' <pin> -- pyaurorax`
returns matches in exactly one file, `pyaurorax/data/ucalgary/__init__.py` at lines 266–267 and
374–375, and both are the same download-progress parameter description: "ASCII value to use when
constructing the visual aspect of the progress bar (straight passthrough of the `ascii` parameter in
a tqdm progress bar)." That is a tqdm styling flag, not a data format. Like `cdf`, `ascii` is in the
PyHC registry keyword list for this entry.

**`CDF` and `ascii` were removed from Field 18; `HDF5`, `IDL.sav` and `Other` are kept.** That is
what the readers support. A visitor filtering HSSI for CDF-reading software and getting PyAuroraX
would download it and find nothing that reads a CDF; the same for ASCII.

Two weaker resolutions were rejected. Removing only `CDF` and keeping `ascii` would rest on reading
`ascii` loosely — the CLI consumes JSON/text query files, and PGM has an ASCII-header variant — but
`JSON` is its own row in the vocabulary, so nothing forces `ascii` to stand in for it, and no reader
takes an ASCII data product. Changing nothing would have preserved values inherited from a curated
registry rather than invented, on the argument that no visitor is harmed by an over-broad format
list; but an over-broad list is exactly what makes a format filter useless.

**Field 19 holds `JSON` and `Other`.** It was settled separately from Field 18, since the two
fields answer different questions and should not have remained identical. `JSON` is an existing
`FileFormat` row and JSON output is real and user-facing: `create_custom_import_file` writes a
Swarm-Aurora import file with `json.dump(res.data, fp, indent=4)`, and the CLI writes search results
and query templates as JSON. Both the earlier extraction and the stored record missed that output.
`Other` carries the figures (PNG/JPG) and the MP4 movies, for which the vocabulary has no rows.

`Other` alone was the alternative, and it is what the evidence would justify if `JSON` were not its
own row; it was rejected as needlessly coarse now that a genuinely distinctive output has a row of
its own. `ascii`, `CDF`, `HDF5` and `IDL.sav` are all unsupported as *outputs* and are gone from
this field: nothing in the package writes HDF5 (no `to_hdf`, no `h5py`, and
`git grep -l -P -i 'hdf5|h5py' <pin> -- pyaurorax` returns 0 files) and nothing writes an IDL save
file. Changing nothing would have left the record claiming this software writes CDF, HDF5, IDL save
and ASCII files, none of which it does.

### 20. Operating System (RECOMMENDED)

**Values:**
- Linux
- Mac
- Windows

Correct as stored, and confirmed twice over. `pyproject.toml` at the pin declares the classifiers
`Operating System :: POSIX :: Linux`, `Operating System :: MacOS :: MacOS X` and
`Operating System :: Microsoft :: Windows`; and `.github/workflows/tests_all_platforms.yml` runs the
suite on a matrix of `os: [ubuntu-latest, macos-latest, windows-latest]` against Python 3.10 through
3.14. The claim is tested, not merely asserted. The package is pure Python with no compiled
extension, so there is no platform-specific build step to qualify this.

### 21. CPU Architecture (RECOMMENDED)
- **Value:** CPU Independent

Correct as stored. The distribution is pure Python — `pyproject.toml` has
`packages = [{ include = "pyaurorax" }]` with no extension modules, no build script beyond
`poetry.masonry.api`, and no architecture in any classifier. Nothing in the package is compiled for
a particular instruction set, and the CI matrix above exercises three operating systems without any
per-architecture branching. Any specific architecture row would be a narrower claim than the
software makes.

### 22. Related Phenomena (OPTIONAL)
- **Value:** Not found — correctly empty, on the vocabulary's own contents

This is a documented, evidence-backed emptiness rather than an unexamined gap, and the reason is
worth stating in full because auroral software looks like the most obvious candidate imaginable for
this field.

**The vocabulary has exactly 7 rows, and none of them is auroral:** `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`,
`X-ray emission`. There is no aurora row, no auroral-emission row and no particle-precipitation row.
Six of the seven are solar, and the seventh, `Geomagnetic Storms`, is not what this software is
about — PyAuroraX reads and analyses auroral imagery irrespective of storm phase, and nothing in the
package selects, indexes or models storms.

**The field is a closed vocabulary; free text is rejected, not created.** The form is explicit:
"Select phenomena terms from the controlled vocabulary below. Despite the web form's free-text
affordance, the API path is strict: `related_phenomena` resolves through `_get_graph_list_item`,
which raises `Unknown value` on anything not in the list. A phenomenon the software supports that
has no row belongs in **Keywords** (Field 16, the open vocabulary), not here."

**An earlier extraction proposed free-text values here — `Aurora`, `Auroral emissions` and
`Particle precipitation` — and none is writable.** None of the three is a row, so each would be
rejected on submission rather than created. They are recorded here so the same three are not
proposed again.

**Where the concept can actually live: Field 16.** `auroral emissions` *does* exist as a `Keyword`
row, and so do `particle precipitation`, `auroral optical emissions`, `auroral electrojet`,
`auroral power` and `Pulsating Aurora`. The form's own instruction above points there, and Field 16
records `auroral emissions` accordingly.

**One structural caution.** The `Phenomena` vocabulary is flat: every row's `parents` and `children`
lists are empty. So there is no "aurora is a kind of geomagnetic phenomenon" hierarchy to exploit,
and selecting `Geomagnetic Storms` would not stand in for an auroral row. "X encompasses Y" is never
an argument in this field.

### 23. Development Status (RECOMMENDED)
- **Value:** Active

HSSI held no development status before this refresh. `Active` is a row in the 8-row `RepoStatus`
vocabulary, and its own stored definition is the test to apply: "The project has reached a stable,
usable state and is being actively developed." Both halves hold.

*Stable and usable:* the project is at 1.23.0, past a deliberate 1.0.0 milestone documented in
`README.md`'s "Migrating from V0 to V1" section, published on PyPI across 87 releases, and rated
`Good` on all six PyHC criteria (community, documentation, testing, software maturity, python3,
license) in `_data/projects.yml` at line 408.

*Actively developed:* the repository is not archived (`archived` false) and its last push is
2026-09-08T21:14:33Z; the newest of its 40 GitHub releases, `v1.23.0`, was published
2026-09-08T21:13:39Z, and the one before it, `v1.22.2`, on 2026-08-21T12:42:10Z; and one issue is
open. Release dates rather than elapsed-time phrasings are used deliberately: this record's own
extraction date is 2026-09-08, so a reader can judge recency against a fixed point rather than
against an interval that ages.

The neighbouring rows are ruled out by the same definitions, quoted from those rows: `Inactive`
("The project has reached a stable, usable state but is no longer being actively developed;
support/maintenance will be provided as time allows.") and `Unsupported` ("The project has reached a
stable, usable state but the author(s) have ceased all work on it. A new maintainer may be
desired.") both require development to have stopped, which contradicts a release published on the
extraction date. `WIP`, `Concept`, `Suspended` and `Abandoned` all presuppose no stable public
release, and `Moved` presupposes a relocation that has not happened.

### 24. Documentation (RECOMMENDED)
- **Value:** https://docs.aurorax.space/code/pyaurorax_api_reference/pyaurorax

Correct as stored and reachable (HTTP 200). It is the project's own nomination: `pyproject.toml` at
the pin lists it under `[tool.poetry.urls]` as `"API Reference"`, PyPI carries the same
`project_urls` entry, `README.md` links it as "PyAuroraX API Reference", and the PyHC registry's
`docs:` field gives the same URL with a trailing slash.

**Other documentation surfaces**, recorded for completeness but deliberately not substituted for
the value above, since the field takes one URL and the API reference is the one the project points
at first:
- `https://docs.aurorax.space/code/overview` — the Developer Zone overview, named in the package's
  own top-level docstring.
- `https://data.phys.ucalgary.ca/working_with_data/index.html#python` — the "Example Gallery" linked
  from `README.md`.
- `https://github.com/aurorax-space/pyaurorax/tree/main/examples` — 55 `.ipynb` notebooks at the
  pin, linked from `README.md` as "Additional examples".
- `https://aurorax.space` — the platform site, and the repository's GitHub `homepage`.

There is no repository wiki to consider: GitHub reports `has_wiki` false, and
`git ls-remote https://github.com/aurorax-space/pyaurorax.wiki.git` reports the repository as not
found.

### 25. Funder (OPTIONAL)

**Values:**
- Canada Foundation for Innovation — https://ror.org/000az4664
- Government of Alberta — https://ror.org/006b2g567
- Technical University of Denmark — https://ror.org/04qtj9h94
- Canadian Space Agency — https://ror.org/03a1gte98

**The repository names no funder at all.** The sweep
`git grep -l -P -i 'acknowledg|funding|grant|NSERC|Canadian Space Agency|award' <pin> -- '*.md' '*.toml' 'pyaurorax'`
returns **0 files**, against a control of `aurora` in the identical scope returning **76** — so the
instrument sees, and the absence is real rather than a mis-scoped search. There is no
`CITATION.cff`, no `.zenodo.json` and no `codemeta.json`, and the Zenodo/DataCite concept record's
`fundingReferences` is an empty list. On repository evidence alone this field would be empty.

**But the describing publication names AuroraX's funders explicitly, attributed to three of this
record's four authors.** The *Frontiers* article (Field 14) has an Author contributions statement
reading "ED, ES, and DC designed and developed the AuroraX platform and PyAuroraX. AH, KM, and IT
assisted MS with developing aurora-asi-lib." and a Funding section whose final sentence is:

> ED, ES, and DC acknowledge the AuroraX funding sources: the Canadian Foundation for Innovation
> (CFI), the Province of Alberta, the Technical University of Denmark (DTU, Swarm DISC Program), and
> the Canadian Space Agency.

Its Acknowledgments section adds: "The UCalgary team acknowledges the AuroraX, REGO ASI and THEMIS
ASI funding agencies and thanks them for their continued support. The UCalgary team also
acknowledges the University of Alberta and RGP Consulting for their work on AuroraX." ED, ES and DC
are Eric Donovan, Emma Spanswick and Darren Chaddock — three of the four authors in Field 6.

**Name normalisation applied to the four funders named in that sentence**, since the form says
"The name of the organization that provided the funding (e.g., National Aeronautics and Space
Administration). Avoid acronyms and enter one organization per field":
- The article writes "the Canadian Foundation for Innovation (CFI)". The organization's registered
  name is **Canada Foundation for Innovation** (ROR `https://ror.org/000az4664`, typed `funder`,
  Ottawa) — "Canadian" is the article's slip, and the ROR display name is used instead.
- "the Province of Alberta" is the provincial government; its ROR record is **Government of
  Alberta** (`https://ror.org/006b2g567`, typed `funder`, Edmonton).
- "the Technical University of Denmark (DTU, Swarm DISC Program)" → **Technical University of
  Denmark** (`https://ror.org/04qtj9h94`, typed `funder`), the acronym and programme dropped per the
  form's instruction.
- "the Canadian Space Agency" → **Canadian Space Agency** (`https://ror.org/03a1gte98`, typed
  `funder`, Longueuil), already unambiguous.

**Rejected, and recorded so Crossref does not reintroduce it.** Crossref's funder block for the
*Frontiers* article contains exactly one entry, `Goddard Space Flight Center`
(`10.13039/100006198`). That is the funding of the article's lead authors — the Funding section
attributes the NASA Postdoctoral Program, the Internal Scientist Funding Model and grant `HISFM21`
to MS, BG-L and AH, none of whom is an author of this software. It funded a describing paper and its
authors' time, not PyAuroraX. `Goddard Space Flight Center` must not be recorded here, and this is
the reason. Likewise the University of Alberta and RGP Consulting are acknowledged for *work* on
AuroraX, not for funding it, so neither belongs in this field.

**Why the four AuroraX funders are recorded.** This is primary evidence in a peer-reviewed article
whose title names PyAuroraX, written by the software's own developers and explicitly labelled "the
AuroraX funding sources". A visitor filtering HSSI by the Canadian Space Agency or the Canada
Foundation for Innovation would reasonably expect the AuroraX libraries back, and before this refresh
would not have got them. Field 25 asks who "supports (sponsors) something through some kind of
financial contribution", which these four did.

The stricter reading was weighed and rejected: the sentence names the funders of **AuroraX**, the
platform, not of PyAuroraX, the client library, and the software's own repository and deposit name no
funder, so on that reading the evidence supports a funder record for the platform rather than for
this package. What decided it against that reading is that the same sentence's authors are credited
two paragraphs earlier with having "designed and developed the AuroraX platform and PyAuroraX" as one
body of work, and no separate funding statement for the library exists or is likely to.

**A correction to earlier reasoning, recorded so it is not repeated.** A previous pass concluded
this field was evidenced-empty on the strength of the repository sweep alone. The repository sweep
is sound and is retained above, but it is not the whole evidence base: the funding information for
this software exists only in the describing publication, which is exactly where the form's own
guidance says to look ("Prefer the reference publication's **Acknowledgments** section, and read its
**Data Availability Statement** too").

### 26. Award Title (OPTIONAL)
- **Value:** Not found — no award title or number exists for any of the funders above

Although Field 25 records the four funders, this field stays empty, and the
reason is specific rather than a shrug. The *Frontiers* Funding section names the AuroraX funders
as bare organizations with no grant identifier and no programme title attached — the only
award-level detail anywhere in that section is `HISFM21`, and it is explicitly Goddard ISFM funding
for a different author ("AH was supported in part by the Goddard ISFM which funds the Space
Precipitation Impacts team with grant HISFM21"), so it must not be attached to these funders. The
"Swarm DISC Program" is named parenthetically as the DTU vehicle, but it is a programme name rather
than an award title, and no award number accompanies it.

The repository confirms the same emptiness independently: the funding sweep under Field 25 returns 0
files, and the Zenodo/DataCite record's `fundingReferences` is empty, so there is no award title or
number in the software's own metadata either.

### 27. Related Publications (OPTIONAL)

**Value:**
- https://doi.org/10.1029/2026EA005013

HSSI held no related publications before this refresh, and nothing in the software's own metadata
nominates any: the DataCite concept record's only relations are its four `HasVersion` links, and
`README.md` links no papers.

The form defines the field as "Publications that describe, cite, or use the software that the
software developer prioritizes but are different from the reference publication." Two publications
are supported by primary evidence, and they are split between this field and Field 14:

- **The *Frontiers* framework paper**, https://doi.org/10.3389/fspas.2022.1009450 — see Field 14 for
  the full citation and the authorship evidence. It belongs in *one* of Field 14 or Field 27, never
  both, and it is recorded in Field 14 as the publication describing the software. It is therefore
  deliberately absent here.
- **The TREx-ATM V2.0 paper**, https://doi.org/10.1029/2026EA005013, "Introduction to TREx‐ATM V2.0:
  A Versatile Model of Auroral Transport and Its Effects in the Ionosphere". This describes the model
  that `pyaurorax/models/atm` exposes — the single capability in this package that a user cannot get
  from the data-access side — and it appears on the ORCID records of both Darren Chaddock and Josh
  Houghton, the two `pyproject.toml` authors. It documents what `ATMManager.forward` and
  `ATMManager.inverse` compute.

**Why only the TREx-ATM V2.0 paper is recorded here.** With the *Frontiers* article in Field 14,
this field carries the one paper a user of the ATM model actually needs, the entry has a
correctly-labelled reference publication, and nothing is double-listed.

Two alternatives were rejected. Recording both papers here and leaving Field 14 empty is the more
cautious reading if the *Frontiers* article is judged to describe three tools rather than this one,
since "describe, cite, or use" is a looser claim than "the publication describing the software"; it
was not taken because the article does genuinely describe this software, and the stronger field is
the more useful one to a visitor looking for something to cite. Recording nothing would follow the
form's "the software developer prioritizes" literally — the project itself has nominated no
publication, its README pointing only at the Zenodo DOI — but it would leave a visitor with no
literature pointer at all where primary evidence supports two papers.

Also considered and **not** recorded: the two remaining works on the developers' ORCID records that
use these data — "Association of structured continuum emission with dynamic aurora"
(https://doi.org/10.1038/s41467-024-55081-5) and "Unexpected STEVE Observations at High Latitude
During Quiet Geomagnetic Conditions" (https://doi.org/10.1029/2024GL110568). Both are science
results using ASI data rather than publications about the software, and neither is nominated by the
project. Recorded so a later refresh does not treat an author's publication list as a source for
this field.

### 28. Related Datasets (OPTIONAL)

**Values:**
- https://doi.org/10.11575/z7x6-5c42 — Redline Geospace Observatory (REGO) dataset
- https://doi.org/10.11575/4p8e-1k65 — Transition Region Explorer - RGB Dataset
- https://doi.org/10.11575/98w7-jp47 — Transition Region Explorer - NIR Dataset
- https://doi.org/10.11575/80pf-0p02 — Transition Region Explorer - Blueline Dataset
- https://doi.org/10.11575/2wnp-yc80 — Transition Region Explorer - Spectrograph Dataset
- https://doi.org/10.11575/qkvx-th24 — SMILE All Sky Imager Dataset

**A previous conclusion is falsified here, and this is the correction.** An earlier extraction
recorded this field as "Not found (as DOIs)" with the note that the ASI datasets "do not have DOIs
registered in the DataCite API". They do. A DataCite query for `url:"data.phys.ucalgary.ca"` returns
9 registered `Dataset` DOIs under the University of Calgary prefix `10.11575`, all published by
`University of Calgary` and all resolving (HTTP 302) to a landing page under
`https://data.phys.ucalgary.ca/datasets/`.

**Six of the nine are datasets this software has a dedicated reader for**, which is precisely Field
28's test ("Datasets the software supports functionality for (e.g., analysis)"):

| Dataset DOI | Landing page | Reader in `pyaurorax/data/ucalgary/read/__init__.py` |
|---|---|---|
| `10.11575/z7x6-5c42` | `https://data.phys.ucalgary.ca/datasets/REGO` | `read_rego` |
| `10.11575/4p8e-1k65` | `https://data.phys.ucalgary.ca/datasets/TREx/RGB` | `read_trex_rgb` |
| `10.11575/98w7-jp47` | `https://data.phys.ucalgary.ca/datasets/TREx/NIR` | `read_trex_nir` |
| `10.11575/80pf-0p02` | `https://data.phys.ucalgary.ca/datasets/TREx/blueline` | `read_trex_blue` |
| `10.11575/2wnp-yc80` | `https://data.phys.ucalgary.ca/datasets/TREx/spectrograph` | `read_trex_spectrograph` |
| `10.11575/qkvx-th24` | `https://data.phys.ucalgary.ca/datasets/SMILE-ASI` | `read_smile` |

`10.11575/qkvx-th24` is additionally attributed on Emma Spanswick's ORCID record, tying it to this
software's own author list.

**The remaining three are correctly excluded, with reasons**, so they are not added later:
`10.11575/afyx-m516` (NORSTAR Single Frequency Single Beam Riometers Dataset) and
`10.11575/anh5-aw08` (Space Weather Adaptive Network (SWAN) – Hyper Spectral Riometer (HSR) Dataset)
are riometer data, for which this package has no reader — consistent with Field 31, where none of
the riometer rows in the instrument vocabulary is attached; and `10.11575/8k88-3n44` (Transition
Region Explorer – GNSS Dataset) is TREx GNSS data, which also has no reader here (the TREx readers
cover RGB, NIR, Blueline and Spectrograph only).

**THEMIS ASI has no DOI in this set**, and that is expected rather than an oversight: `read_themis`
reads THEMIS ground ASI data, whose archive is not a University of Calgary registered dataset. No
DOI was found for it, and one should not be invented.

**Why all six dataset DOIs are recorded.** Each is a dataset this software has a dedicated reader
for, each has a resolving DOI and a landing page, and together they make the entry discoverable from
the data side — a visitor who arrives at the REGO or TREx dataset record can find the library that
reads it. They are not *all* the data this software reads: THEMIS ASI is read too and has no DOI in
this set.

Two narrower resolutions were rejected. Recording a subset — if six entries were judged too heavy for
the field, the two a searcher is most likely to arrive from are `10.11575/z7x6-5c42` (REGO) and
`10.11575/4p8e-1k65` (TREx RGB), the two flagship arrays — would have been arbitrary, since all six
are equally directly supported. Recording none would have left the datasets reachable only through
the platform URL already recorded in Fields 17 and 24, when an optional field with six verified,
directly supported DOIs is the clearest enrichment available on this record.

### 29. Related Software (OPTIONAL)

**Values:**
- asilib — https://github.com/mshumko/asilib
- AACGMv2 — https://github.com/aburrell/aacgmv2
- idl-aurorax — https://github.com/aurorax-space/idl-aurorax
- pyUCalgarySRS — https://github.com/ucalgary-srs/pyUCalgarySRS

**The two entries HSSI already held are strongly relevant on the form's own tests, and both are
retained.**

- **asilib** performs similar tasks — the form's primary test, "Software that performs similar tasks
  but does not necessarily link together (which would be 'interoperable software')". It is another
  all-sky-imager analysis library, and the two are co-described in the *Frontiers* article whose
  title is "AuroraX, PyAuroraX, and aurora-asi-lib: A user-friendly auroral all-sky imager analysis
  framework". The relationship is already reciprocal in the catalogue: asilib's own record lists
  `https://github.com/aurorax-space/pyaurorax` among its related software.
- **AACGMv2** is a domain-specific dependency, which the form covers with "Important software
  dependencies and software this work was forked from should also be included." `pyproject.toml` at
  the pin declares `aacgmv2 = "^2.6.2"`, and it is used in 8 files under `pyaurorax/` for the
  geographic↔AACGM conversions documented in Field 4. It is a heliophysics coordinate library, not
  generic infrastructure, so the Tier A exclusion does not touch it.

**Related-item display names are placeholders, not titles.** Some rows carry `UNKNOWN` and others
the raw URL, depending on which code path created them; the two rows this entry held for related
software before this refresh both carried `UNKNOWN`. Neither form is user-visible, because the
page renders the item's URL as its link text. It is noted only so a future reader does not mistake
it for a data-quality problem to chase.

**Why both incumbents are recorded as repository URLs rather than DOIs.**
The campaign convention, settled 2026-09-01, is that when an entry names another HSSI entry it uses
that entry's exact stored `code_repository_url`, because the page renders a related item's raw URL
as its link text: a DOI string is opaque to a visitor, while a repository URL is legible and keys
the catalogue's own record. The two incumbents are **not** symmetrical under that convention, and
the difference was established by checking each DOI's Zenodo relation type:

- **asilib — `https://doi.org/10.5281/zenodo.4746446` is the *concept* DOI, not a version DOI.**
  Its DataCite record carries `HasVersion` relations rather than `IsVersionOf`, and
  `https://zenodo.org/api/records/4746446` returns a 302 to a different (later) record — the
  redirect-to-latest behaviour of a Zenodo concept record. It is also, as of this refresh, the exact
  persistent identifier asilib's own HSSI record carries. So for asilib the "it pins an old release"
  objection does not apply, and the DOI already keys the catalogue's record for that software. The
  legibility argument still favours `https://github.com/mshumko/asilib` (33 characters, asilib's
  stored `code_repository_url`).
- **AACGMv2 — `https://doi.org/10.5281/zenodo.3598705` *is* a version DOI, and a stale one.** Its
  DataCite record shows `version` `2.6.0` and `IsVersionOf 10.5281/zenodo.1212694`, and it resolves
  to "aburrell/aacgmv2: Version 2.6.0". AACGMv2's own HSSI record carries the *concept* DOI
  `https://doi.org/10.5281/zenodo.1212694` instead, so the DOI this entry held for AACGMv2 before
  this refresh neither matched the catalogue's record nor pointed at current software. It is
  recorded here as the repository URL `https://github.com/aburrell/aacgmv2` (35 characters, its
  stored `code_repository_url`) rather than as the concept DOI
  `https://doi.org/10.5281/zenodo.1212694`.

Both were nonetheless switched to repository URLs — the convention's default — for legible link text
keyed to each target's catalogue record, with no version pinning. Two alternatives were rejected:

- **Keeping both DOIs**, correcting only the AACGMv2 one to its concept DOI. Rejected on legibility,
  but with a reverse condition worth recording: if HSSI ever renders a resolved title instead of the
  raw URL, a DOI becomes the better value, because a DOI survives a repository move or rename and a
  GitHub URL does not.
- **A mixed pair:** asilib's concept DOI, which already matches asilib's own stored identifier, with
  AACGMv2's repository URL, its DOI matching nothing and pinning v2.6.0. Rejected because it would
  make two sibling relations on the same record follow different conventions for no reader-visible
  benefit.

Every URL recorded in this field is well inside the 128-character ceiling that applies to a related
item's name/identifier column; the longest is 45 characters.

**Two entries were added: `idl-aurorax` and `pyUCalgarySRS`.**
Neither is in the HSSI catalogue, which the form explicitly permits: "If no public repository, enter
link where users can find more information (e.g., related HSSI item)" — a public repository is a
stronger value still.

- **`https://github.com/aurorax-space/idl-aurorax`** (44 characters) — the IDL counterpart library.
  Same team, same stated purpose (GitHub describes it as "IDL library supporting data access and
  analysis for All-Sky Imager (ASI) data", `language` `IDL`, not archived, last pushed
  2026-05-12T13:22:14Z), and the two share the single Zenodo deposit whose title names both. On the
  form's test it is the clearest "companion package" case on this record. It is also where an IDL
  user actually needs to go, which is why removing `IDL` from Field 13 and the `idl` keyword from
  Field 16 loses that reader nothing: this relation carries them to the code they want.
- **`https://github.com/ucalgary-srs/pyUCalgarySRS`** (45 characters) — the domain library that all
  of `pyaurorax/data/ucalgary` and `pyaurorax/models/atm` delegates to. `pyproject.toml` declares
  `pyucalgarysrs = "^1.26.0"`; PyPI describes it as "Tools for interacting with UCalgary Space
  Remote Sensing data" and gives that repository URL. It is a domain-specific dependency in the
  strict sense — a heliophysics data library whose presence characterises this software — and it is
  the reason the format and data-source evidence in Fields 17–19 has to be read through a
  dependency. The reservation against it — that a visitor may not need to know about an
  implementation dependency, and that Field 29 asks for *important* dependencies rather than all of
  them — did not carry, precisely because this dependency is not incidental: it is where the data
  handling actually happens, so a reader who does not know about it will misread the format and
  data-source evidence on this record.

**Removals that are policy, not taste.** An earlier extraction listed `numpy`, `matplotlib` and
`cartopy` here. All three are named in `resource_submission_form_fields.md` line 690, "Never list
these (Tier A), no exceptions", and line 698 extends the same exclusion to this field: "Where a
rejected entry goes: usually nowhere. A genuinely distinguishing domain package may belong in Field
29 (Related Software) — but Field 29 applies the same exclusion to the generic stack, so do not
relocate a Tier A package there." Field 29's own text at line 677 says the same directly: "The
generic scientific-Python stack is excluded here too". These are not choices a reviewer can approve
back in. The same rule disposes of the rest of this package's dependency list — `requests`,
`scipy`, `pyproj`, `click`, `python-dateutil`, `humanize`, `texttable`, `termcolor` — each of which
would be equally at home in a web app, a finance model, or a biology pipeline, and none of which
distinguishes this software.

### 30. Interoperable Software (OPTIONAL)

**Value:**
- SwarmAurora — https://swarm-aurora.com/conjunctionFinder

**The evidence for SwarmAurora is a documented, one-directional exchange in the public API.**
`pyaurorax/search/conjunctions/swarmaurora/__init__.py` exposes three methods on
`SwarmAuroraManager`, and their own docstrings state the exchange:
`get_url(search_obj)` — "Get a URL that displays a conjunction search in the Swarm-Aurora Conjunction
Finder"; `open_in_browser(search_obj, browser=None)` — "In a browser, open a conjunction search in
the Swarm-Aurora Conjunction Finder."; and `create_custom_import_file(search_obj, filename=None,
return_dict=False)` — "Generate a Swarm-Aurora custom import file for a given conjunction search".
The implementation in `_swarmaurora.py` requests
`https://swarm-aurora.com/conjunctionFinder/generate_custom_import_json?aurorax_request_id=%s` and
writes the response with `json.dump(res.data, fp, indent=4)`. So PyAuroraX's own output is written
in a format designed to be imported into SwarmAurora — the form's "one's output can be imported into
the other", with an adapter API to do it. The URL to record, `https://swarm-aurora.com/conjunctionFinder`,
is reachable (HTTP 200) and is 42 characters.

**Why SwarmAurora is recorded.** This is a real, coded, documented interoperation with a named
domain tool — the strongest such relationship this package has, and one a visitor finds genuinely
informative: it tells them that a PyAuroraX conjunction search can be handed to Swarm-Aurora for
visualization. The form's "How to fill it" anticipates a target with no public repository: "If no
public repository, enter link where users can find more information".

Leaving the field empty was the alternative reading, and it turns on the field's second sentence:
"Other important software **packages** this software has demonstrated interoperability with. Can run
package in the same environment as the others without errors." SwarmAurora is a hosted web
application, not an installable package, so "run in the same environment" cannot apply to it at all,
and on that reading nothing qualifies and the field is correctly empty. It was rejected because that
second sentence is a caveat on real interoperability rather than the test for it, and the exchange
here is exactly what the field's relevance guidance describes.

**The earlier extraction's three candidates are rejected, on the form's own words.** It listed
`asilib`, `pyDARN` and `apexpy`, justified by "PyHC community registry shows these packages work
with similar data types and coordinate systems in the ionosphere/magnetosphere domain." That is the
justification the form names as never sufficient on its own: line 694 lists two such justifications,
"part of the standard scientific Python ecosystem" and "a PyHC member, so it interoperates with PyHC
packages", and states that "ecosystem membership is not a demonstrated interoperation with any
particular package."

What was looked for, and not found, before rejecting them: any adapter or converter naming them
(`git grep -l -P -i 'asilib|pydarn|apexpy' <pin> -- pyaurorax` — 0 files); any mention in
`pyproject.toml` or `poetry.lock`; any shared data model or documented format exchange; and any
example or test that passes data between PyAuroraX and any of the three. None exists. asilib's real
home on this record is Field 29, where it qualifies on *similar tasks* rather than on interoperation
— and the form is explicit that a package rejected here is not thereby a Field 29 entry, so it earns
that place on its own evidence.

### 31. Related Instruments (OPTIONAL)

**Values — 28 instruments, every one carrying a `https://spase-metadata.org/` identifier. Complete
and correct as stored; no addition or removal is warranted.**

The 24 THEMIS ground all-sky imagers:

- **THEMIS Ground Athabasca All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/ATHA/ASI
- **THEMIS Ground Fort Simpson All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/FSIM/ASI
- **THEMIS Ground Fort Smith All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/FSMI/ASI
- **THEMIS Ground Gillam All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/GILL/ASI
- **THEMIS Ground Pinawa All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/PINA/ASI
- **THEMIS Ground Rankin Inlet All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/RANK/ASI
- **THEMIS Ground Sanikiluaq All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/CANMAG/SNKQ/ASI
- **THEMIS Ground Chibougamau All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/CHBG/ASI
- **THEMIS Ground Ekati All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/EKAT/ASI
- **THEMIS Ground Fort Yukon All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/FYKN/ASI
- **THEMIS Ground Gakona All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/GAKO/ASI
- **THEMIS Ground Goose Bay All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/GBAY/ASI
- **THEMIS Ground Inuvik All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/INUV/ASI
- **THEMIS Ground Kapuskasing All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/KAPU/ASI
- **THEMIS Ground Kiana All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/KIAN/ASI
- **THEMIS Ground Kuujjuaq All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/KUUJ/ASI
- **THEMIS Ground McGrath All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/MCGR/ASI
- **THEMIS Ground Narsarsuaq All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/NRSQ/ASI
- **THEMIS Ground Prince George All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/PGEO/ASI
- **THEMIS Ground Snap Lake All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/SNAP/ASI
- **THEMIS Ground Taloyoak All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/TALO/ASI
- **THEMIS Ground The Pas All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/TPAS/ASI
- **THEMIS Ground White Horse All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/WHIT/ASI
- **THEMIS Ground Yellowknife All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/THEMIS/Ground/UCLA-GBO/YKNF/ASI

The four TREx imagers:

- **Blue All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/TREX/BLUEASI
- **Near Infrared All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/TREX/NIRASI
- **Proton Aurora Meridian Imaging Spectrograph** — https://spase-metadata.org/SMWG/Instrument/TREX/PAMIS
- **Red-Green-Blue All Sky Imager** — https://spase-metadata.org/SMWG/Instrument/TREX/RBGASI

Every name above is copied verbatim from the matched controlled-vocabulary row, not from an upstream
SPASE page — the two can legitimately differ. Note that the four TREx row names carry no "TREx"
prefix, so the TREx affiliation shows only in the `TREX/` segment of each identifier; and
`Proton Aurora Meridian Imaging Spectrograph` is the row that `read_trex_spectrograph` corresponds
to — it is the only spectrograph among the five TREx-affiliated rows in the vocabulary (the token
sweep below enumerates them).

**Why these are the right instruments.** Each has a dedicated reader in
`pyaurorax/data/ucalgary/read/__init__.py` (`read_themis`, `read_trex_rgb`, `read_trex_nir`,
`read_trex_blue`, `read_trex_spectrograph`), and `README.md` names the arrays directly: "data access
and analysis support for All-Sky Imager data (THEMIS, TREx, REGO, SMILE, etc.)". This is
designed-to-support in the strongest sense — the software is written by the instrument team for two
of these arrays and is the official client for their data.

**THEMIS ground ASI coverage is exact and complete, and the count is reproducible.** Filtering the
`InstrumentObservatory` vocabulary on `identifier` containing `/SMWG/Instrument/THEMIS/Ground/`
returns 70 rows, whose terminal identifier segments are `MAG` 45, `ASI` 24 and `Magnetometers` 1.
All 24 rows ending in `/ASI` are attached to this record, and none of the other 46 is — they are
magnetometers, which this software does not read. A caution for anyone re-deriving this: a
`name__icontains='THEMIS Ground'` sweep gives a smaller and misleading number, because most of the
magnetometer rows are named "THEMIS GBO …" rather than "THEMIS Ground …". Use the identifier
namespace, which is what the count above is keyed on.

**TREx coverage is likewise exact.** The token sweeps quoted here and in Field 32 all use the same
anchored, case-insensitive pattern `(?<![0-9A-Za-z])TOKEN(?![0-9A-Za-z])` applied across the four
populated columns of each vocabulary row — `name`, `abbreviation`, `identifier` and `definition` —
so they catch a match wherever upstream recorded it. On that pattern the token `TREx` appears in
exactly 5 rows of the whole vocabulary: the four instrument rows above plus
`https://spase-metadata.org/SMWG/Observatory/TREX`. All 5 are attached to this record (the
observatory under Field 32). A control token with no expected presence, `xylophone`, returns 0 rows
under the same pattern, so the sweep is not silently matching everything.

**SMILE ASI is deliberately omitted, not overlooked.** PyAuroraX reads the University of Calgary
ground-based SMILE all-sky imager network: `read_smile` is documented "Read in SMILE ASI raw data
(L0 raw h5 files)." and the instrument array identifier used is `smile_asi`. No SPASE record exists
for that network. The token `SMILE` matches exactly 2 rows in the entire vocabulary:
`https://spase-metadata.org/SMWG/Observatory/SMILE`, which is attached (Field 32), and
`https://spase-metadata.org/SMWG/Instrument/SMILE/SXI`, named `Soft X-ray Imager`, which is
correctly **not** attached — that row denotes the SMILE mission's spaceborne Soft X-ray Imager,
which this software does not support. The mission association is therefore carried at observatory
level instead. Two related points that keep this from being re-litigated:

- **A fabricated expansion was previously recorded here and must never return.** An earlier version
  of this entry listed "SMILE (Suomi-NPP Magnetometer, Ionosphere, Lithosphere Explorer) ASI" bound
  to `https://spase-metadata.org/SMWG/Instrument/SMILE/SXI`. Both halves were wrong: no entity is
  named "Suomi-NPP Magnetometer, Ionosphere, Lithosphere Explorer" — SMILE is the Solar wind
  Magnetosphere Ionosphere Link Explorer, an ESA/CAS mission — and the SXI row is the wrong
  instrument.
- **SMILE UVI has no row either.** `RELEASE_NOTES.md` for version 1.22.0 shows the ATM model
  emitting SMILE UVI quantities, renaming its output flags to
  `height_integrated_rayleighs_smile_uvi_lbh` and `emission_smile_uvi_lbh`. Neither the ground ASI
  network nor UVI has a vocabulary row, which is why the observatory-level association is the
  correct resolution rather than a compromise.

**Should upstream ever register the UCalgary ground-based SMILE ASI network**, or a SMILE UVI
instrument, this omission is worth revisiting. Until then it should not be re-proposed, and it must
never be resolved by creating an identifierless row — there is no free-type path here, and a bare
name either binds to an arbitrary same-name row or mints a new row with no SPASE identifier.

**Near-miss rows inspected individually and correctly not attached**, so a future sweep does not
mistake them for gaps. Each is quoted by its vocabulary row name and identifier:

- `CANOPUS All-Sky Imagers` — https://spase-metadata.org/SMWG/Instrument/CANOPUS/ASI
- `Finnish Meteorological Institute, FMI, All Sky Cameras` — https://spase-metadata.org/SMWG/Instrument/Ground/Kilpisjarvi/AllSkyCamera
- `RISH all sky camera at Kototabang` — https://spase-metadata.org/IUGONET/Instrument/RISH/misc/KTB/AllSkyCamera
- `RISH all sky camera at Shigaraki` — https://spase-metadata.org/IUGONET/Instrument/RISH/misc/SGK/AllSkyCamera
- `Electron auroral imager` — https://spase-metadata.org/IUGONET/Instrument/NIPR/Aurora/SYO/EAI
- `The all-sky imager at Poker Flat Research Range, Alaska.` — https://spase-metadata.org/IUGONET/Instrument/NICT/SALMON/PF/asi
- `All-sky Imager Observation at South Pole Station` — https://spase-metadata.org/IUGONET/Instrument/NIPR/SouthPole/SPA/ASI

None of these arrays is read by this software: PyAuroraX's readers cover the THEMIS, REGO, TREx and
SMILE arrays and nothing else. The same applies to the 53 riometer rows in the vocabulary (matching
`(?<![0-9A-Za-z])Riometer(?![0-9A-Za-z])`, case-insensitive, across the `name`, `abbreviation`,
`identifier` and `definition` columns) — this package has no riometer reader, which is consistent
with the two riometer datasets excluded under Field 28. The five THEMIS *spacecraft* observatory
rows `https://spase-metadata.org/SMWG/Observatory/THEMIS/A` through `/E` and the CNES CDPP-AMDA
THEMIS spacecraft rows are also correctly absent: this package reads THEMIS **ground** imager data,
not THEMIS spacecraft data.

### 32. Related Observatories (OPTIONAL)

**Values — 4 observatories, every one carrying a `https://spase-metadata.org/` identifier. Complete
and correct as stored.**

- **Redline Emission Geospace Observatory** — https://spase-metadata.org/SMWG/Observatory/REGO
- **Solar wind-Magnetosphere-Ionosphere Link Explorer** — https://spase-metadata.org/SMWG/Observatory/SMILE
- **Time History of Events and Macroscale Interactions during Substorms** — https://spase-metadata.org/SMWG/Observatory/THEMIS
- **Transition Region Explorer** — https://spase-metadata.org/SMWG/Observatory/TREX

Each name is the matched vocabulary row's `name`, copied verbatim, and each is the row's long form
rather than the abbreviation a reader may expect. Three of the four rows carry a separate
`abbreviation` field — `rEGO`, `SMILE` and `TREx` — which HSSI appends when it renders the name, so
a page showing "Transition Region Explorer (TREx)" is that rendering rather than a differently-named
value. Two consequences of that worth recording: REGO's stored abbreviation really is the
lowercase-initial `rEGO`, which is faithful to the vocabulary and not a typo to correct; and the
THEMIS observatory row's `abbreviation` is empty, which is why its long name appears unabbreviated.

**REGO is an observatory, not an instrument, and this is settled.** REGO's SPASE identity *is* the
imager network itself: the token `REGO` matches exactly 1 row in the whole vocabulary, and it is
this observatory row — no REGO instrument row exists. So the association can only be recorded here.
It was at one point listed among the Field 31 instruments and was moved here; that move is correct
and should not be reversed by a future sweep looking for a "missing" REGO instrument.

The software's support for all four is direct: `read_rego`, `read_smile`, `read_themis` and the four
TREx readers each parse that observatory's own raw data, and `README.md` names all four arrays in
its opening sentence. A visitor browsing any one of these observatories and asking which software
supports it would expect this library back.

**The per-station THEMIS ground observatory rows are deliberately not attached, and a future sweep
should not read them as a gap.** Filtering the vocabulary on `identifier` starting
`https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground` returns 40 rows — per-station GBO and
EPO entries such as `NASA THEMIS GBO Gillam Station`
(https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground/CANMAG/GILL), plus roll-ups like
`THEMIS-Associated Ground Magnetometer Stations`
(https://spase-metadata.org/SMWG/Observatory/THEMIS/Ground). Attaching them would add nothing a
visitor can use: the per-station granularity is already carried precisely, and more usefully, by the
24 per-station **instrument** rows in Field 31, which name the imagers rather than the sites; the
mission-level association is carried by the THEMIS observatory row above; and many of the 40 are
magnetometer or education-and-public-outreach sites whose data this software does not read at all.
The campaign convention points the same way — prefer the specific instrument when the software
targets an instrument, which is what an all-sky imager reader does.

**The THEMIS spacecraft rows in other namespaces are likewise correctly absent**, for the same
reason given in Field 31: this package reads THEMIS ground imager data. That covers
https://spase-metadata.org/SMWG/Observatory/THEMIS/A through `/E`, and the whole
`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/THEMIS/` and
`https://spase-metadata.org/CNES/Observatory/CDPP-Archive/THEMIS` families, which describe the five
THEMIS spacecraft and their particle and magnetic-field instruments.

### 33. Logo (OPTIONAL)
- **Value:** https://raw.githubusercontent.com/aurorax-space/pyaurorax/52319d549ba9e86bc5c4e782a02e0fc222a117af/logo.svg

Correct as stored, verified three ways, and kept.

*It serves real image bytes:* the URL returns HTTP 200 with `content-type: image/svg+xml` and 11563
bytes. *It is byte-faithful to the pinned tree:* the fetched file's sha256 is
`60608c99a9fb19a2ebf0e4b8c043dbcfb453a002acdeb0f8af6a2f7e3e01e409`, identical to
`git cat-file blob 741938df29d05f20919f68597fabdad71aec3b13:logo.svg | shasum -a 256`, so the
commit-pinned URL and the source revision this dossier is written against serve the same image.
*And it looks like what it should:* rendered, the image is a **PyAuroraX wordmark** — the word
"PyAuroraX" beside a stylised auroral-curtain glyph in the project's blue-to-green gradient.

**One reading caveat.** `README.md:1` at the pin embeds the file as
`<a href="https://aurorax.space/"><img alt="AuroraX" src="logo.svg" height="60"></a>` — the
hyperlink target and the `alt` text both say *AuroraX*, the platform, not *PyAuroraX*. So a reader
who checks only the README markup could reasonably conclude the asset is the platform's wordmark and
not this software's. It is not: the rendered image reads "PyAuroraX". This is recorded so the
question is not reopened from the markup alone.

**The URL is pinned to a 40-hex commit SHA by design, and this must not be undone.** The PyHC
registry's `logo:` field for this entry gives the branch form
`https://raw.githubusercontent.com/aurorax-space/pyaurorax/main/logo.svg`, and that is the value to
*avoid*: a branch URL breaks silently whenever the file is renamed, moved or deleted, and a branch
can itself be renamed. The argument that a branch URL "always serves the current logo" is rejected —
that mutability is precisely the fragility being fixed, and a logo redesign is something a metadata
refresh should notice and record deliberately rather than something the catalogue inherits
unnoticed. The asset is not Git-LFS-tracked, so `raw.githubusercontent.com` is the correct host
(an LFS-tracked file would return a ~130-byte `text/plain` pointer here and need
`media.githubusercontent.com` instead). At 107 characters the URL is inside the 200-character limit
that applies to this field.
