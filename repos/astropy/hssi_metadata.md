# HSSI Metadata Extraction Results

**HSSI Software ID:** c46778bd-7352-44cd-91fe-010102bb8aa0
**Repository:** https://github.com/astropy/astropy
**Source Revision:** bada72aa79a2d1fd7c705ddc8175800c2eb1312d
**Extraction Date:** 2026-08-26
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

**Scope note — read this before judging the evidence.** Astropy is a general-purpose astronomy
library, not a heliophysics package. It appears in no PyHC registry (Field 7). Much of the reasoning
below therefore turns on a recurring question: does a first-party *convention-* or *format-level*
capability (a solar FITS WCS axis code, a heliocentric ecliptic frame) amount to heliophysics
support, or is it astrometric and format infrastructure that happens to be usable by heliophysics
tools? The answer is taken differently in different fields, and each field states why. Field 5 is
where that question is sharpest; it is settled there in favour of `Solar Environment`, on the
strength of solar capability that lives in astropy itself, and the contrary reading is preserved
alongside it so the balance of the argument stays visible.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This placeholder is the catalogue convention for a record not yet attached to a real submitter; it is
not an extraction gap.

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.4670728

This is the Zenodo **concept** DOI, which resolves to whichever version is current rather than to one
frozen release — the right choice for a field that identifies the software itself. Three independent
sources agree on it: the `CITATION.cff` `identifiers:` block records it with `description: Concept
DOI`; the README's Zenodo badge targets it; and Zenodo's own record for 4670728 reports
`conceptdoi 10.5281/zenodo.4670728` with `conceptrecid 4670728`, confirming that 4670728 is the
concept record and not a version record.

*Considered and not selected:* the version-specific DOI for v8.0.1. It belongs in Field 12 (Version
PID), where it is recorded, not here.

*Also present in the same `identifiers:` block and deliberately not used here:* the ASCL entry
`https://ascl.net/1304.002`. It is a registry listing rather than a persistent identifier that
resolves to the software artifact, and HSSI accepts one persistent identifier in this field.

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/astropy/astropy

Recorded independently in `pyproject.toml` under `[project.urls] repository`, in `CITATION.cff` as
`repository-code`, and as the canonical GitHub repository (default branch `main`).

### 4. Software Functionality (MANDATORY)

- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Solar
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Forward-Fitting
- Models and Simulations: Physics-Based
- Models and Simulations: Theory

The public API this classification describes is the
set of subpackages exported from `astropy/__init__.py`: `config`, `constants`, `convolution`,
`coordinates`, `cosmology`, `io`, `modeling`, `nddata`, `samp`, `stats`, `table`, `time`,
`timeseries`, `uncertainty`, `units`, `utils`, `visualization`, `wcs`.

**Coordinate Transforms: Heliospheric.** Astropy natively provides the frame the heliophysics
community calls **HAE (Heliocentric Aries Ecliptic)**. `astropy/coordinates/builtin_frames/ecliptic.py`
defines `HeliocentricMeanEcliptic` with its origin at the centre of the Sun, its x axis toward the
mean equinox and its xy-plane in the ecliptic. The equivalence is not an inference: SunPy's own
"Supported Coordinate Systems" table lists the row *Heliocentric Aries Ecliptic (Mean)*, abbreviation
*HAE (also HEC)*, and gives the implementation as "Astropy's `~astropy.coordinates.HeliocentricMeanEcliptic`".
SunPy does not reimplement HAE; it defers to astropy for it. Alongside it astropy ships
`HeliocentricTrueEcliptic`, `HeliocentricEclipticIAU76` and `HCRS` (a heliocentric frame with axes
aligned to ICRS, relative to the Sun's centre of mass). These are user-facing transform targets via
`SkyCoord.transform_to(...)`.

An earlier extraction rejected this value on the stated ground that astropy has "no HCI/HAE/HEE/
Carrington/Stonyhurst/RTN frames — those are in SunPy." That premise was factually wrong for HAE and
the value is now included. The accurate part of it is worth keeping so it is not re-litigated:
**astropy has no HCI, HEE or RTN frames** — SunPy's frame table assigns HEE to
`sunpy.coordinates.frames.HeliocentricEarthEcliptic` and HCI to
`sunpy.coordinates.frames.HeliocentricInertial`.

**Coordinate Transforms: Solar.** Astropy carries first-party support for the solar FITS WCS
conventions, at the pixel-to-world level:

- `astropy/wcs/wcsapi/fitswcs.py` maps the solar CTYPE codes to physical types — `HPLN`/`HPLT`/`HPRZ`
  to helioprojective longitude/latitude/z, `HGLN`/`HGLT` to Stonyhurst heliographic,
  `CRLN`/`CRLT` to Carrington heliographic, and `SOLX`/`SOLY`/`SOLZ` to heliocentric Cartesian.
- `astropy/visualization/wcsaxes/wcsapi.py` supplies display formatting and units for
  helioprojective and Stonyhurst/Carrington heliographic axes.
- `astropy/wcs/src/wcslib_auxprm_wrap.c` exposes wcslib's solar observer auxiliary parameters —
  `crln_obs`, `hgln_obs`, `hglt_obs`, `dsun_obs`, `rsun_ref` — through `WCS.wcs.aux`, documented in
  `astropy/wcs/docstrings.py` ("Carrington heliographic longitude of the observer", and the
  Stonyhurst equivalents).
- `astropy/io/ascii/mrt.py` handles heliographic and helioprojective column sets when writing MRT
  tables.

*Scope limit, recorded so it is not rediscovered as an objection:* astropy performs pixel-to-world
transforms **for** solar CTYPEs and carries the solar observer parameters, but it does not convert
**between** solar frames (Carrington to Stonyhurst to helioprojective) — that is SunPy. That
limitation was weighed against the value and did not defeat it: the WCS pixel-to-world mapping is
itself a coordinate transform, and astropy is the code performing it. The value stands with the
limitation attached rather than being dropped on account of it.

**Coordinate Transforms: Planetary — removed.** A previous version of this record carried it. It is
wrong. The complete built-in frame export list in `astropy/coordinates/builtin_frames/__init__.py`,
read to its closing boundary, is ICRS, FK5, FK4, FK4NoETerms, Galactic, Galactocentric,
Supergalactic, AltAz, HADec, GCRS, CIRS, ITRS, HCRS, TEME, TETE, PrecessedGeocentric,
GeocentricMeanEcliptic, BarycentricMeanEcliptic, HeliocentricMeanEcliptic, GeocentricTrueEcliptic,
BarycentricTrueEcliptic, HeliocentricTrueEcliptic, HeliocentricEclipticIAU76,
CustomBarycentricEcliptic, LSR, LSRK, LSRD, GalacticLSR, SkyOffsetFrame, BaseEclipticFrame,
BaseRADecFrame, plus `galactocentric_frame_defaults` and `make_transform_graph_docs`. No planet-fixed,
planetocentric or planetographic frame is among them.

Two pieces of counter-evidence exist and are recorded here **specifically so a future agent does not
mistake either for grounds to restore the value**:

- `astropy/coordinates/solar_system.py` exports `get_body`, `get_body_barycentric`,
  `get_body_barycentric_posvel` and `solar_system_ephemeris`, with `BODY_NAME_TO_KERNEL_SPEC`
  covering the Sun, Mercury, Venus, the Earth-Moon barycentre, Earth, the Moon, Mars, Jupiter,
  Saturn and the rest. That is solar-system *ephemeris positioning* — where a body is — not
  transformation between planetary coordinate systems.
- `astropy/wcs/wcsapi/fitswcs.py` additionally maps the CTYPE codes `TLON`/`TLAT` to
  `pos.bodyrc.lon`/`pos.bodyrc.lat`, the FITS convention for body-referenced coordinates. This is a
  two-entry physical-type *label*, with no accompanying frame, no transformation, no display support
  and no auxiliary parameters.

The asymmetry with `Coordinate Transforms: Solar` is deliberate and is the reason the two are treated
differently: the solar case has a frame-level capability (HAE and the heliocentric ecliptics) plus
display, auxiliary-parameter and table-writer support layered on the CTYPE mapping; the planetary
case has the CTYPE label and nothing else. A user filtering HSSI on
`Coordinate Transforms: Planetary` and getting astropy back would have a false positive.

**Data Processing and Analysis: Data Access and Retrieval.** `astropy/utils/data.py` provides
`download_file` with a scheme whitelist of `http`, `https`, `ftp`, `sftp`, `ssh` and `file`. Concrete
retrieval paths: IERS Earth-orientation auto-download (whose *timing* the v8.0.1 change altered, not
its existence); JPL DE ephemeris fetch through `solar_system_ephemeris` (default kernel `de430`);
SESAME name resolution in `astropy/coordinates/name_resolve.py` (`get_icrs_coordinates`);
`EarthLocation.of_site`, which downloads the observatory site registry from the astropy-data
repository, and `EarthLocation.of_address`, which geocodes; and remote or cloud FITS access via
`fits.open(..., use_fsspec=True)`.

**Data Processing and Analysis: 2D Slices** *(and its visualization counterpart).* Astropy's own
documentation frames the capability in exactly the terms this category names:
`docs/wcs/wcsapi.rst` describes slicing that is "reducing the dimensionality of the data and
associated WCS (e.g. extracting a slice from a spectral cube)", and demonstrates it on a real
spectral cube with `wcs[10, 30:100, 30:100]` reducing a three-dimensional WCS to two. The
implementation is `SlicedLowLevelWCS` in `astropy/wcs/wcsapi/wrappers/sliced_wcs.py`, surfaced
through `WCS.__getitem__`. Critically for the *processing* half of the pair, this is not
WCS-metadata-only: `astropy/nddata/mixins/ndslicing.py` (`NDSlicingMixin`) slices `data`, `mask`,
`uncertainty` **and** `wcs` together, routing the WCS through `SlicedLowLevelWCS`, and it is mixed
into `NDDataRef` and `NDDataArray`. So a user slicing a cube gets a coherent 2D dataset with correct
coordinates, which is the whole content of the category. The visualization half is
`docs/visualization/wcsaxes/slicing_datacubes.rst`, which plots cube slices with
`subplot_kw=dict(projection=wcs, slices=(50, 'y', 'x'))`.

An earlier note treated `Data Processing and Analysis: 2D Slices` as the weaker of the pair and left
it undecided. The `NDSlicingMixin` evidence resolves it: the data array, not just its coordinate
description, is sliced.

**Evidence for the remaining values.**

- *Image Processing* — `astropy.convolution`; `astropy.nddata` (`Cutout2D`, `block_reduce`,
  `block_replicate`); `astropy.visualization` stretches and `ImageNormalize`;
  `astropy/visualization/basic_rgb.py` and `lupton_rgb.py` for RGB composition; the `fits2bitmap`
  console script.
- *File Format Conversion* — the registered reader/writer inventory in Fields 18/19 below. Astropy
  reads one format and writes another as a first-class operation through `io_registry`.
- *Time Series Analysis* — `astropy/timeseries/`: `sampled.py`, `binned.py`, `downsample.py`, the
  `periodograms/` package (Lomb-Scargle, Box Least Squares), and `io/kepler.py`.
- *Data Reduction* — `astropy.timeseries.aggregate_downsample`, `astropy.nddata.block_reduce`,
  `astropy.stats.sigma_clip`.
- *Data Visualization: 2D Graphics / Line Plots* — `astropy.visualization` and its WCSAxes framework
  produce image and line plots of astronomical data with world-coordinate axes.
- *Models and Simulations* — `astropy/modeling/`: `physical_models.py` (BlackBody, NFW, Drude1D,
  Plummer1D) for **Physics-Based**; `functional_models.py` and `powerlaws.py` (Sersic, Moffat, Voigt,
  broken and smoothly-broken power laws) for **Empirical**; `fitting.py` and `_fitting_parallel.py`
  (least-squares and chi-square fitters) for **Forward-Fitting**; `astropy/cosmology/` (analytic FLRW
  distances and ages, the `traits/` components) for **Theory**.

**Considered and rejected — durable negative research.** Each rejected value below exists as a real
row in the live vocabulary, so these are choices, not typos.

- **`Servers and Environments`** (and its `Data servers processing and handling` and
  `Distribution/Access` children). Astropy does ship a literal server: `astropy.samp` provides
  `SAMPHubServer` and installs a `samp_hub` console script. Rejected on two independent grounds,
  either of which suffices. First, `astropy.samp` was **deprecated in version 8.0** and will be
  removed; `astropy/samp/__init__.py` raises an `AstropyDeprecationWarning` on import and
  `docs/samp/index.rst` directs users to `pyvo.samp`. Classifying the software by a subsystem its own
  maintainers have told users to stop using would make the record stale by design. Second, and
  independent of deprecation, a SAMP hub is an IVOA inter-process message broker for desktop clients
  on the local host — it serves no data, provisions no environment, and matches none of the
  category's children. *The counter-argument, recorded because it is real and should not have to be
  rediscovered:* astropy does ship a server binary, and that is a genuine argument for the category.
  It was weighed and outweighed — by the deprecation on one side and, independently, by the mismatch
  between what a SAMP hub does and what any of the category's children describe.
- **`Data Processing and Analysis: Wave Polarization Analysis`.**
  `astropy/coordinates/polarization.py` exports `StokesCoord`, `StokesSymbol` and
  `custom_stokes_symbol_mapping`. These *label* a Stokes WCS axis; they compute no polarization
  property.
- **`Data Visualization: Web-Based`.** `astropy/table/jsviewer.py` registers a `jsviewer` writer and
  `Table.show_in_browser(jsviewer=True)` renders a sortable HTML table. That is a table view in a
  browser, not an interactive visualization of scientific data.
- **`Models and Simulations: Instrument Response`.** AiryDisk2D, Moffat2D and Gaussian2D are generic
  profile models. Instrument-response modelling lives in photutils and synphot, not here.
- **`Data Processing and Analysis: Spectrogram`, `Energy Spectra`, `Calibration`, `ML/AI`,
  `Field-line Tracing`.** No corresponding code. In particular, Lomb-Scargle and Box Least Squares
  are periodograms — they produce power versus frequency, not a time-frequency representation — so
  they do not make astropy a spectrogram package.
- **`Data Visualization: 3D Graphics`, `Movies`, `Orbit Plots`.** No corresponding code found.
- **`Mission-related` (any child).** Astropy is not part of any mission ground system. The Kepler and
  TESS light-curve readers noted in Field 31 are file-format readers, not mission infrastructure.

**How this field relates to Field 5, so the two are not "corrected" against each other.** These two
fields answer different questions and are not required to line up value-for-value.
`Coordinate Transforms: Heliospheric` and `Coordinate Transforms: Solar` are **capability** claims:
they say astropy implements transforms into heliocentric-ecliptic and solar WCS coordinate
descriptions. Field 5 asks a different question — which physical region's *science* the software
supports — and is answered there with `Solar Environment`, on the strength of the solar CTYPE,
solar-observer-parameter and HAE support catalogued above.

The asymmetry a future refresher is most likely to misread is the ephemeris one. The
heliospheric/ephemeris capability recorded here — `HeliocentricMeanEcliptic`, `HCRS`, and the
`get_body` / `get_body_barycentric_posvel` solar-system machinery — deliberately did **not** also
yield `Interplanetary Space` in Field 5. Positioning a solar-system body is astrometric
infrastructure: it tells you where Jupiter is, and does nothing with the plasma, fields or
energetic particles between the planets that `Interplanetary Space` denotes. A heliospheric
*coordinate* capability is therefore not evidence of interplanetary *science* support, and the
presence of `Coordinate Transforms: Heliospheric` here must not be used to argue
`Interplanetary Space` back into Field 5.

### 5. Related Region (MANDATORY)

- Solar Environment

**Why `Solar Environment`.** Astropy carries first-party solar capability — code in astropy itself,
not capability that SunPy layers on top of it:

- **Ten solar FITS WCS CTYPE codes are mapped natively.** `astropy/wcs/wcsapi/fitswcs.py` resolves
  `HPLN`, `HPLT` and `HPRZ` to helioprojective longitude/latitude/z; `HGLN` and `HGLT` to Stonyhurst
  heliographic; `CRLN` and `CRLT` to Carrington heliographic; and `SOLX`, `SOLY` and `SOLZ` to
  heliocentric Cartesian. `astropy/visualization/wcsaxes/wcsapi.py` adds display formatting and units
  for the helioprojective and heliographic axes, and `astropy/io/ascii/mrt.py` handles heliographic
  and helioprojective column sets when writing MRT tables.
- **The wcslib solar observer auxiliary parameters are exposed.**
  `astropy/wcs/src/wcslib_auxprm_wrap.c` surfaces `crln_obs`, `hgln_obs`, `hglt_obs`, `dsun_obs` and
  `rsun_ref` through `WCS.wcs.aux`, documented in `astropy/wcs/docstrings.py` ("Carrington
  heliographic longitude of the observer", and the Stonyhurst equivalents). These describe where the
  observer sits relative to the Sun — solar-specific quantities with no meaning outside solar work.
- **HAE is provided natively.** `astropy/coordinates/builtin_frames/ecliptic.py` defines
  `HeliocentricMeanEcliptic`, which is the frame the heliophysics community calls HAE (Heliocentric
  Aries Ecliptic). This is not an inference: SunPy's own "Supported Coordinate Systems" table lists
  *Heliocentric Aries Ecliptic (Mean)*, abbreviation *HAE (also HEC)*, and gives the implementation as
  "Astropy's `~astropy.coordinates.HeliocentricMeanEcliptic`". SunPy does not reimplement HAE; it
  defers to astropy for it.

Taken together these are Sun-referenced capabilities that exist in astropy's own source. Someone
browsing HSSI for solar-region software and finding astropy is not getting a false positive: the
package really does implement the solar coordinate conventions their data are written in.

**Considered and rejected: leaving the field empty.** This was the reading initially reached, and the
argument for it is genuine and is preserved in full so that nobody reconstructs it from scratch and
mistakes it for a new discovery.

- Field 5 asks for the physical region whose *science functionality* the software supports. Astropy's
  solar code is convention- and format-level: the same helioprojective WCS machinery applies to a
  photospheric, a chromospheric and a coronal image indistinguishably, so on this reading it selects
  no region at all. Heliocentric ecliptic frames and JPL ephemerides are astrometric infrastructure.
  Astropy's centre of mass is cosmology, galactic dynamics, stellar and exoplanet work.
- The `Region` rows are a flat list of specific physical regions. There is no "not applicable",
  "multiple" or "domain-independent" row, and no coarse row implies a finer one, so no
  "X encompasses Y" argument is available to soften a choice that turns out to be too broad.
- "MANDATORY" on this field is a submission-form convention, not a storage constraint. An empty
  Region is a legitimate outcome for domain-independent tooling, so "the field must be filled" is
  never on its own a reason to fill it.
- **Two named precedents point the other way.** `cdflib` — a library for a file format that is
  overwhelmingly a heliophysics format — records Field 5 as intentionally empty on the reasoning that
  "cdflib has no science functionality tied to any region — it reads and writes a file format", and
  that a region value would be "a false membership in a browse facet". `sammi` likewise records it
  empty, noting that its behaviour "is identical regardless of the physical domain the data
  describe", and rejecting `Solar Environment` as a placeholder guess.
- Two warrants that can carry a Region for an otherwise region-agnostic package are both unavailable
  here: astropy is in no PyHC registry (Field 7), so there is no curated community metadata to
  inherit a region from, and it ships no mission list or "used by" statement of its own from which
  one could be read.

**Why `Solar Environment` was chosen over that.** The empty reading treats astropy's solar support as
generic machinery that happens to accept solar inputs. It is not generic. A heliocentric-ecliptic
frame, a Carrington-heliographic axis type and an observer's distance from the Sun are not
domain-neutral plumbing that solar data can be poured through; they are solar constructs that astropy
implemented deliberately, and they have no use outside solar and heliospheric work. That is the
respect in which astropy differs from `cdflib` and `sammi`, whose behaviour genuinely does not change
with the domain of the data. `Solar Environment` is recorded as the single value: it is the broadest
solar row and therefore the one that does not overstate which layer of the Sun's environment astropy
speaks to.

**Considered and rejected: `Interplanetary Space`.** The previous record carried it alongside
`Solar Environment`. It rested only on `get_body` and `get_body_barycentric_posvel` — solar-system
ephemeris positioning, which is astrometric infrastructure rather than region-specific science.
Knowing where a planet is says nothing about the plasma, fields or particles in the space between
the planets. It is not restored. (Both of the previous record's values were also justified with
"supportable via" phrasing — an argument about what the software *could* be used for rather than
what it supports. `Solar Environment` is recorded above on the different and stronger ground that the
solar constructs are implemented in astropy itself.)

**Considered and rejected — the remaining `Region` rows, with reasons.** `Earth Magnetosphere`, the
Earth magnetospheric subregions and `Planetary Magnetospheres`: astropy has no GSE, GSM, SM, MAG or
AACGM frame and no planet-fixed frame (see Field 4). `Earth Atmosphere`, `Earth Lower and Middle
Atmosphere`, `Earth Ionosphere`, `Earth Thermosphere` and `Earth Auroral Subregion`: no atmospheric,
ionospheric or auroral model or data support. `Photosphere`, `Chromosphere` and `Corona`: the WCS
machinery is identical across all three, so nothing in astropy selects among them, and choosing one
would assert a specificity the code does not have. `Solar Interior`, `Solar Wind` and `Heliosheath`:
no corresponding capability.

### 6. Authors (MANDATORY)

1. **The Astropy Developers** — astropy.team@gmail.com
2. **Astropy Collaboration**

Both are **organization authors**, and both are taken from primary metadata files in the repository
rather than inferred.

- "The Astropy Developers" is the sole entry in `pyproject.toml`'s
  `authors = [{ name = "The Astropy Developers", email = "astropy.team@gmail.com" }]`.
- "Astropy Collaboration" is the sole entry in `CITATION.cff`'s **top-level** `authors:` block, and it
  has a single `name:` key with no `given-names`/`family-names` — the CFF signal for an organization.
  It is also the sole creator on the Zenodo and DataCite records for the concept DOI. (DataCite marks
  that creator `nameType: "Personal"`, which is a Zenodo-side error; the entity is an organization.)

**No ROR identifier is recorded for either, because none exists.** The ROR registry returns no
organization for Astropy, the Astropy Project, or the Astropy Collaboration. This is recorded so a
future agent does not spend the search again.

**Why both labels are recorded rather than one.** "The Astropy Developers" and "Astropy
Collaboration" plausibly denote the same body under two labels, used in two different metadata files
by the same project. No primary source either equates or distinguishes them, so there is no evidence
on which to merge one into the other, and the union rule — which never drops an author — governs.
Both stand. A curator who later obtains a first-party statement that the two labels name one entity
would have grounds to consolidate; absent that statement, dropping either would be a guess.

**Considered and rejected: enumerating individual contributors.** `docs/credits.rst` lists 628
individual names under "Core Package Contributors" at the pinned revision. That file is
auto-generated from git history by `scripts/update-credits.py` via `.mailmap` (which is purely an
identity-deduplication map and designates no one as an author) and refreshed by the
`update_credits.yml` workflow. The file's only other section, "Other Credits", holds three entries —
Kyle Barbary for designing the Astropy logos and documentation themes, Andrew Pontzen and the pynbody
team for code that grew into `astropy.units`, and the mailing lists collectively. **None of the
repository's authorship-bearing metadata designates any individual as a software author of the
package**: at the pinned revision the only such files are `pyproject.toml`, `CITATION.cff` and
`astropy/CITATION` — there is no `AUTHORS`, `CONTRIBUTORS`, `codemeta.json` or `.zenodo.json` — and
`pyproject.toml` and `CITATION.cff` both name an organization, while `astropy/CITATION` carries
BibTeX for the three papers. The Zenodo and DataCite records likewise carry the single organizational
creator.

**Considered and rejected: using the 2022 paper's author list.** `CITATION.cff` carries roughly 135
named authors with ORCIDs and affiliations under `preferred-citation.authors`. CFF deliberately
separates top-level `authors` (who wrote the software) from `preferred-citation.authors` (who wrote
the paper). Those names belong to Field 14's publication, not to this field.

### 7. Software Name (MANDATORY)
- **Name:** Astropy
- **Alt Name:** astropy

`CITATION.cff` gives `title: Astropy` and the README uses the capitalised form in prose; the
distribution name in `pyproject.toml` is lowercase `astropy`, which is also the import name. Both
forms are in first-party use, so both are recorded.

**PyHC negative research.** Astropy appears in **none** of the three PyHC registries. All three —
`projects_core.yml` (core packages), `projects.yml` (community packages) and
`projects_unevaluated.yml` — were fetched fresh and parsed as YAML in full rather than grepped, and a
case-insensitive search for "astropy" across all three returns nothing: no entry name, no `code`
repository URL and no description mentions it. Deliberately **no entry count is recorded for those
files**, because they are live upstream documents whose membership changes and a pinned number goes
stale without anyone touching this record; the durable, re-checkable fact is the absence of astropy,
which is what the field turns on. (For orientation only, the community registry as read ran from
AACGMV2 and AFINO through swxsoc, TomograPy, viresclient and XRTpy, and the core registry held SunPy,
pysat, PlasmaPy, SpacePy, pySPEDAS, Kamodo and HAPI Client.)

**There is therefore no PyHC-curated name, description or keyword set overriding repository evidence
anywhere in this record** — a fact that also carries weight in Fields 5 and 16.

### 8. Description (MANDATORY)

Astropy is a community-developed core Python package for astronomy. It provides a comprehensive,
interoperable foundation for astronomical and astrophysical research, including astronomical
coordinate systems and transforms, time and date handling, physical units and constants,
FITS/VOTable/ASCII/HDF5/Parquet file I/O, world coordinate systems (WCS), tables, NDData, modeling
and fitting, statistics, convolution, cosmological calculations, time series, uncertainties, and
visualization. Astropy is the canonical core of a large astronomy ecosystem and is widely used as a
dependency by mission analysis tools and heliophysics packages such as SunPy.

This wording is retained from the prior record as accurate editorial phrasing, and it is corroborated
rather than replaced. `pyproject.toml` gives the one-line `description = "Astronomy and astrophysics
core library"`, which the GitHub repository description matches exactly. The README opens: "The
Astropy Project is a community effort to develop a single core package for astronomy in Python and
foster interoperability between packages used in the field. This repository contains the core
library." The subsystem list above corresponds to the subpackages exported from
`astropy/__init__.py`.

*One deliberate omission:* `astropy.samp` is not advertised in this description, because it was
deprecated in v8.0 and will be removed.

### 9. Concise Description (OPTIONAL)

Astropy is the community-developed core Python package for astronomy: coordinates, time, units,
FITS/HDF5 I/O, WCS, tables, modeling, statistics, cosmology, time series, and visualization.

Retained from the prior record. It is accurate and consistent with Field 8.

### 10. Publication Date (RECOMMENDED)
- **Date:** 2011-07-21

The date the astropy repository was first created and made public. The form defines this field as the
"date of first broadcast/publication, used for the initial version of the software", which is the
first public availability of the code — not the 2013 A&A paper (Field 27) and not the current release
(Field 12). `sunpy`'s record applies the same convention and is the named precedent for it.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

The DataCite record for the concept DOI names Zenodo as publisher. Zenodo is the archiving service
that mints and holds the DOI in Field 2.

### 12. Version (RECOMMENDED)
- **Version Number:** v8.0.1
- **Version Date:** 2026-07-04
- **Version PID:** https://doi.org/10.5281/zenodo.21262391
- **Version Description:** Maintenance release. The one API change defers IERS-A network access:
  `IERS_Auto.open` now always reads the Earth-orientation table bundled in `astropy-iers-data` (or a
  local `finals2000A.all`), and downloads the latest table only when a calculation actually requests
  UT1-UTC or polar-motion values beyond the bundled table's predictive range while that table is
  older than `iers.conf.auto_max_age`; download warnings are now emitted only if all mirrors fail.
  Bug fixes span seven subpackages. `io.fits`: a FITS logical ('L') column created by
  `BinTableHDU.from_columns(..., nrows=N)` stored NULL instead of False; bytes outside the 'L'
  wire format assigned to a column read with `logical_as_bytes=True` were written unchecked and now
  raise `ValueError`; DATASUM and CHECKSUM were computed incorrectly for byte-swapped binary tables
  larger than 64 kB. `modeling`: a `Parameter` with a custom getter/setter raised `AttributeError`
  when its `value` was read before assignment. `nddata`: `Cutout2D.plot_on_original()` drew a region
  spanning pixels outside the cutout. `table`: a `Table.loc[]` range query dropped rows when the
  upper bound was a duplicated value under the default `SortedArray` index, and returned scrambled
  row order under the `BST` index when rows were added after the index was built. `units`:
  `numpy.lib.recfunctions.structured_to_unstructured` failed on a `StructuredQuantity`.
  `visualization`: WCSAxes tick labels were misplaced for non-perpendicular grids or ticks. `wcs`:
  `world_axis_object_components` and `world_axis_object_classes` were cached incorrectly when the
  equinox was NaN.

**This corrects a materially stale value.** The prior record said **v7.2.0, dated 2025-11-25**, with
version PID `https://doi.org/10.5281/zenodo.17756022`. Four releases have shipped since: 7.2.1, 7.2.2,
8.0.0 and 8.0.1.

*Where the version description came from.* The 8.0.1 changelog section was read to its closing
boundary — `git show v8.0.1:CHANGES.rst` from the heading "Version 8.0.1 (2026-07-03)" through to the
next heading "Version 8.0.0 (2026-06-16)". The `units`, `visualization` and `wcs` fixes sit near the
end of that section and are easy to truncate away; they are included above. Note that **`CHANGES.rst`
on `main` at the pinned revision begins at "Version 8.0.0 (2026-06-16)"** — the 8.0.1 section was
never merged back to `main`, so the release notes are only reachable from the tag.

**Version Date — why 2026-07-04, and why not the three alternatives.** Four dates are attested, and
they are all different:

| Candidate | What it actually is |
|---|---|
| 2026-07-03 | The date in the changelog heading at the tag: "Version 8.0.1 (2026-07-03)". |
| **2026-07-04** | **The `v8.0.1` git tag commit, 2026-07-04 23:21:06 +0100 — the release cut.** |
| 2026-07-05 | The PyPI upload of the 8.0.1 artifact. |
| 2026-07-08 | The Zenodo archive record and the GitHub Release object. |

**2026-07-04 is selected** because it is the moment the release was actually cut in the authoritative
source repository — a primary, reproducible fact derivable from the pinned repository itself, and one
that sits correctly in the causal chain ahead of publication and archiving.

*2026-07-03 rejected, with the reason worth keeping.* The changelog heading is normally reliable:
across the preceding releases v7.1.0, v7.1.1, v7.2.0, v7.2.1 and v8.0.0 the changelog heading date
and the tag date are **identical**. They diverge for exactly two releases, v7.2.2 and v8.0.1, which
were cut in the same session — both headed 2026-07-03 and both tagged 2026-07-04. That pattern shows
the heading is the date the release notes were prepared and the tag is when the release actually
landed a day later; the heading is a plan, the tag is an event.

*2026-07-05 rejected:* a distribution event downstream of the release. v7.2.2 was uploaded to PyPI
seven minutes earlier in the same batch, which marks these timestamps as publication mechanics rather
than release dates.

*2026-07-08 rejected, and it is the trap to avoid.* Zenodo's `publication_date` and the GitHub
Release's publication timestamp are the same event — Zenodo mints its record from the GitHub Release —
and **this is precisely the value DOI autofill would copy in**. It is the date the archive was
created, four days after the software was released.

*Where the Version PID came from, and why not DataCite.* The DataCite record for the concept DOI
carries **no** `HasVersion` related identifiers, so the version DOI is not readable from DataCite for
this software — the usual route is simply empty here rather than broken. The value came instead from
the Zenodo API's latest record for concept 4670728, which reports `doi 10.5281/zenodo.21262391` with
`version "v8.0.1"`. Recorded so a future agent reaching an empty DataCite `HasVersion` list does not
conclude the identifier is unavailable and give up.

*`CITATION.cff` cannot arbitrate any of this:* it has no top-level `version` or `date-released` key.
Its complete top-level key set is `cff-version`, `message`, `title`, `authors`, `repository-code`,
`url`, `license`, `identifiers`, `preferred-citation` and `references`.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- C
- Other

`pyproject.toml` sets `requires-python = ">=3.11"` and carries the classifiers
`Programming Language :: C`, `Programming Language :: Cython` and
`Programming Language :: Python :: 3 :: Only` (3.11 through 3.14). The tracked-file census at the
pinned revision is dominated by `.py` (1,004) with 69 `.h` and 64 `.c`; `cextern/` vendors cfitsio,
expat and wcslib, all C. **`Other` covers Cython**, which accounts for 10 `.pyx` files, and the 5
`.l` lex grammars inside `cextern/wcslib`.

**Rust — confirmed absent.** No `.rs` file and no `Cargo` manifest is tracked. Recorded explicitly
because `Rust` is a comparatively recent vocabulary row, which makes it exactly the value a later
enrichment pass would think to add.

**C++ — confirmed absent, and this contradicts an automated source.** Automated repository analysis
(GitHub Linguist, surfaced through SoMEF) reports C++ as a language of this repository, at roughly
51 kB. It is a misclassification and **must not be recorded**. No file with a C++ extension
(`.cpp`, `.cc`, `.cxx`, `.c++`, `.hpp`, `.hxx`, `.hh`) is tracked, and no `.h` file in the repository
contains a C++ construct — no `namespace`, no `template <`, no class definition. Linguist attributes
ambiguous `.h` headers heuristically, and these headers are C. The same automated source also reports
"Lex", which is real (the five wcslib `.l` grammars) and is covered by `Other`.

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.3847/1538-4357/ac7c74
- **Title:** "The Astropy Project: Sustaining and Growing a Community-oriented Open-source Project
  and the Latest Major Release (v5.0) of the Core Package"
- Astropy Collaboration et al. 2022, ApJ 935, 167 (arXiv:2206.14220)

The repository ships three citable papers and asks users to cite all of them, but `astropy/CITATION`
resolves the priority explicitly: "if space is limited, please cite the most recent paper." That makes
the 2022 paper the reference publication and puts the 2018 and 2013 papers in Field 27. It is also
the paper named under `preferred-citation` in `CITATION.cff`.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause

Recorded in the exact form of the live `License` vocabulary row. Six independent sources agree:
`pyproject.toml` (`license = "BSD-3-Clause"`, with
`license-files = ["LICENSE.rst", "licenses/*.rst"]`); `CITATION.cff` (`license: BSD-3-Clause`);
`LICENSE.rst` itself; the README ("Astropy is licensed under a 3-clause BSD style license"); the
GitHub API (`spdx_id: BSD-3-Clause`); and PyPI (`license_expression: BSD-3-Clause`).

The DataCite `rightsList` also says BSD 3-Clause, with `rightsUri
https://opensource.org/licenses/BSD-3-Clause`. It agrees here, but the repository is the authority —
DOI-derived license metadata reproduces the archive's own errors and must not be preferred over the
repository's statement.

*Target note:* legacy duplicate `License` rows exist on some HSSI instances but not others. This
particular value is present on both, so no target-specific hazard applies to it.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- astronomy
- astrophysics
- cosmology
- space
- science
- units
- table
- wcs
- samp
- coordinate
- fits
- modeling
- models
- fitting
- ascii

These are the fifteen entries of `pyproject.toml`'s `keywords` array, in the order the project lists
them. `Keyword` is the one open vocabulary in HSSI — missing rows are created on submission — so no
value here needs to pre-exist.

Nothing was added. The project's own keyword list is authoritative for this field, and (per Field 7)
there is no PyHC keyword set to reconcile against.

*One caveat worth carrying forward:* `samp` names a subpackage that was deprecated in v8.0 and will be
removed. It remains recorded here because it is what the project publishes, but if `astropy.samp` is
deleted in a future release this keyword becomes a candidate for removal.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- S3/Cloud-aware
- FTP/FTPS Directories

- **HTTP/HTTPS Directories** — `astropy/utils/data.py` whitelists `http` and `https` in
  `download_file`; the observatory site registry, IERS tables and JPL ephemerides are all retrieved
  this way.
- **S3/Cloud-aware** — `docs/io/fits/usage/cloud.rst` documents `fits.open(url, use_fsspec=True)`
  with `s3://` and `gs://` prefixes, worked through on a public STScI HST bucket path, using the
  optional `s3fs` dependency.
- **FTP/FTPS Directories** — new relative to the prior record. `astropy/utils/data.py` imports
  `ftplib`, whitelists `ftp` and `sftp`, and defines `_ftptlswrapper(urllib.request.ftpwrapper)`
  built on `ftplib.FTP_TLS()` with `prot_p()` — explicit FTPS, not merely plain FTP.

**Considered and rejected.** `TAP` — astropy reads and writes VOTable through `astropy.io.votable`
but ships no TAP client; TAP querying lives in pyvo and astroquery.
`Observatory/Mission-specific` — the Kepler and TESS readers consume local files; they do not talk to
a mission archive or API. `AMDA`, `CDAWeb`, `das2`, `GFZ`, `HAPI`, `Madrigal`, `OMNIWeb`, `SSCWeb`,
`The Virtual Solar Observatory.`, `VirES` and `WDC` — no corresponding code, which is unsurprising
given that all of these are heliophysics archives and astropy is an astronomy library.

### 18. Input File Formats (RECOMMENDED)
- FITS
- ascii
- csv
- HDF5
- JSON
- Other

The registered reader inventory, gathered from `register_reader(` call sites outside the test suite:
`io/fits/connect.py` (FITS for `Table`) and `nddata/ccddata.py` (FITS for `CCDData`);
`io/votable/connect.py` (`votable`, `votable.parquet`); `io/misc/parquet.py` (`parquet`,
`parquet.votable`); `io/misc/ecsv.py` (`ecsv`); `io/misc/hdf5.py` (`hdf5`);
`io/misc/pyarrow/csv.py` (`pyarrow.csv`, reader only); `io/misc/pandas/connect.py` (the pandas
formats); `io/ascii/core.py`, which registers every ASCII flavour implemented under `io/ascii/`
(basic, cds, daophot, ecsv, fastbasic, fixedwidth, html, ipac, latex, **mesa** — MESA stellar-evolution
history and profile files, new in 8.0 — mrt, qdp, rst, sextractor, tdat, misc);
`cosmology/_src/io/builtin/` (`ascii.html`, `ascii.mrt`, plus in-memory converters); and
`timeseries/io/kepler.py` (`kepler.fits` and `tess.fits`). YAML is handled by `io/misc/yaml.py`.
ASDF support is provided by the external `asdf-astropy` plugin rather than in-tree.

**`Other` therefore covers** VOTable, Parquet, ECSV, YAML, ASDF (via plugin), and the ASCII family:
MRT/CDS, IPAC, DAOphot, SExtractor, QDP, TDAT, MESA, LaTeX, reStructuredText and fixed-width.

**Formats confirmed absent — do not select these rows.** `CDF`, `netCDF3/4`, `IDL.sav`, `Zarr` and
`ISTP-Compliant` are all live `FileFormat` rows and none applies. Each absence was verified with
**fixed-string** matching over tracked files, because a prior pattern-based attempt produced a false
file list. The point of the detail below is that every case-insensitive hit for these format names is
an unrelated substring or an unrelated identifier — none is a reference to the format:

- `zarr` — the great majority of case-insensitive hits are the substring inside the cosmology helper
  **`aszarr`** ("as z array") in `astropy/cosmology/_src/`. The hits outside `aszarr` are ordinary
  local variable names in two test modules — `xarr, yarr, zarr = np.random.randn(3, 100)` in
  `astropy/coordinates/tests/test_api_ape5.py`, where `zarr` is the z component of a Cartesian
  representation, and `_zarr` in `astropy/cosmology/_src/tests/test_core.py`, a redshift array. Both
  are "z" plus "arr", not the Zarr format. Capitalised `Zarr` does not occur. **The exclusion of the
  `Zarr` row is correct.** (An earlier version of this note claimed there was not a single occurrence
  of `zarr` outside `aszarr`; that was false, and the corrected reading is recorded here so the
  claim is not restated.)
- `ISTP` — the case-insensitive hits fall into three unrelated groups, none of which is the ISTP
  convention. Most are the substring inside **`StrListProxy`** and **`UnitListProxy`** in the wcslib
  wrapper sources under `astropy/wcs/` (and a changelog entry about `PyUnitListProxy_richcmp`). The
  rest are the wcslib distortion variable **`distpd`** in `cextern/wcslib/C/dis.c` and the
  PyInstaller flag **`--distpath`** in `tox.ini`. Capitalised `ISTP` does not occur anywhere in the
  repository. **The exclusion of the `ISTP-Compliant` row is correct.** (An earlier version of this
  note claimed every case-insensitive match was inside the two proxy classes; that was false, and
  `distpd` and `--distpath` are named here so the omission is not repeated.)
- `netCDF` in any casing, `readsav`, `idlsave` and `scipy.io` — no occurrences at all, anywhere in
  the tracked tree. Outside the test suite the literal `.sav` matches four times, all unrelated
  substrings: `np.savetxt` in `io/ascii/basic.py`, `save_attributes` in
  `io/votable/validator/result.py`, and the `np.save`/`np.savez`/`np.savetxt` entries in the units
  and masked-array function-helper tables. Inside the test suite the further matches are
  `fig.savefig` and `result.save` calls. None is an IDL save file.
- `CDF` — as a standalone word it occurs only in cumulative-distribution-function usages in
  `astropy/stats/` and `astropy/timeseries/`, plus the wcslib routine `cdfix` and its wrappers. The
  remaining case-insensitive hits are substrings of unrelated identifiers: the FITS `tabledump`
  column-descriptor argument `cdfile` in `astropy/io/fits/`, the cfitsio changelog entry `ffcdfl`,
  and a hexadecimal literal in `cextern/expat/lib/nametab.h`. The phrase "common data format" does
  not appear, and there is no `cdflib`, `pycdf` or `spacepy` reference.

### 19. Output File Formats (RECOMMENDED)
- FITS
- ascii
- csv
- HDF5
- JSON
- Other

Astropy writes the formats it reads: the `register_writer(` call sites mirror the reader inventory in
Field 18 across `io/fits/connect.py`, `nddata/ccddata.py`, `io/votable/connect.py`,
`io/misc/parquet.py`, `io/misc/ecsv.py`, `io/misc/hdf5.py`, `io/misc/pandas/connect.py` and
`io/ascii/core.py`. Write-only additions on this side are `table/jsviewer.py` (the `jsviewer` HTML
writer) and `cosmology/_src/io/builtin/ascii.latex`. Beyond the table registry, `fits2bitmap` writes
PNG and other bitmap images, and `WCS.footprint_to_file()` writes a DS9-format region file (see
Field 30).

`Other` covers the same set as Field 18, plus PNG via `fits2bitmap` and the DS9 region format. The
same absence findings apply — `CDF`, `netCDF3/4`, `IDL.sav`, `Zarr` and `ISTP-Compliant` are all
correctly unselected.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

`pyproject.toml` configures cibuildwheel for macOS (`archs = ["x86_64", "arm64"]`) and Linux
(`archs = ["auto", "aarch64"]`), and `.github/workflows/ci_workflows.yml` runs the test matrix on
`ubuntu-latest`, `macos-latest` and `windows-latest`, plus `ubuntu-24.04-arm` and named
`windows: py313-test-alldeps` and `macos: py313-test-alldeps` jobs.

**Considered and rejected: `Operating System Independent`.** It is a real vocabulary row and it is
literally what the `pyproject.toml` classifier says. The three named platforms are chosen instead
because they are what the project actually builds and tests, which is more useful to someone
filtering on a platform. Selecting both would be self-contradictory: astropy ships compiled C
extensions, so it is not architecture- or platform-neutral in the sense that row implies.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64
- Linux aarch64 or arm64

The same cibuildwheel configuration determines this: macOS `x86_64` and `arm64` wheels, Linux `auto`
(x86-64) and `aarch64` wheels, with `test-skip = "*-musllinux_x86_64"` and `skip = ["cp*t-*"]`.
`ppc64le` is a live vocabulary row but no ppc64le wheel is built, so it is not selected.

### 22. Related Phenomena (OPTIONAL)
**Not found** — no phenomenon applies, and this is a deliberate outcome rather than a gap.

Astropy targets no specific heliophysics phenomenon. The reason the field is correctly empty rather
than merely unfilled is that the whole `Phenomena` vocabulary was walked against the codebase and
each row failed. As it stood at extraction the vocabulary held `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and
`X-ray emission` — astropy implements no capability corresponding to any of them. Should the
vocabulary gain rows later, the finding to re-apply is the search result below, not this list.

The supporting search across the package and documentation (excluding tests) found no file mentioning
"solar wind", "sunspot", "magnetosphere", "ionosphere", "aurora" or "heliosphere". **"corona" matched
exactly one file, and it is a good falsification to keep:**
`astropy/coordinates/data/constellation_names.dat`, whose entries "CrA Corona Australis" and
"CrB Corona Borealis" are constellations, not the solar corona.

`X-ray emission` deserves its own note because it is a comparatively recent vocabulary row and the
obvious candidate for a later enrichment pass: the core package has no X-ray-specific capability.
X-ray astronomy support in this ecosystem lives in separate packages.

### 23. Development Status (RECOMMENDED)
- **Status:** Active

v8.0.1 was released on 2026-07-04, following 7.2.1, 7.2.2 and 8.0.0 earlier the same year.
Development of the next release is already under way — the nearest tag to the pinned revision is
`v8.1.0.dev`. The repository carries 16 GitHub Actions workflows, including scheduled cron jobs, and
the README displays a pyOpenSci peer-reviewed badge linking to
https://github.com/pyOpenSci/software-review/issues/251. `docs/credits.rst` credits 628 individual
contributors.

*The prior record reached the same conclusion but cited v7.2.0 and 2025-11-25.* The status is
unchanged; the evidence behind it is refreshed.

### 24. Documentation (RECOMMENDED)
- **URL:** https://docs.astropy.org

Declared in `pyproject.toml` under `[project.urls] documentation` and linked from the README.

*Not used for this field:* the project homepage `https://www.astropy.org/` (`[project.urls]
homepage`), which is the project's front page rather than its documentation, and the GitHub wiki,
which is not the maintained documentation.

### 25. Funder (OPTIONAL)

1. **Gordon and Betty Moore Foundation** — https://ror.org/006wxqw41
2. **National Aeronautics and Space Administration** — https://ror.org/027ka1x80
3. **International Gemini Observatory** — https://ror.org/058tw4f12
4. **NumFOCUS** — https://ror.org/004eyxv41
5. **Python Software Foundation** — no ROR identifier exists (see below)
6. **Google** — https://ror.org/00njsd438

The authoritative source is the reference publication (Field 14), which describes the Project's
funding in its own body text and again in its acknowledgements. Both were read. Each ROR above
resolves to the organization named beside it in the ROR registry; organization names are recorded in
expanded institutional form per the catalogue's convention (hence "National Aeronautics and Space
Administration" rather than "NASA").

- **Gordon and Betty Moore Foundation** — the paper: "The Gordon and Betty Moore Foundation awarded
  the Astropy Project a ~$900k (US) grant in 2019 for the proposal 'Sustaining and Growing the
  Astropy Project.'" The acknowledgements add: "We acknowledge the Gordon and Betty Moore foundation
  for their continued financial support." See Field 26 for the grant itself.
- **National Aeronautics and Space Administration** — "This work is partially supported by NASA under
  Grant No. 80NSSC22K0347 issued through the NASA ROSES program." The body text describes it as ~$600k
  over three years from the ROSES-2020 call, section E.7.
- **International Gemini Observatory** — the entity recorded is the **proximate named supporter**.
  The paper's body text is decisive and more specific than the acknowledgement boilerplate: "the
  Project benefited from a Gemini Observatory contract under its Science User Support Department,
  which awarded funds for development work that supports both the Astropy and DRAGONS projects."
  Gemini is the entity that awarded the funds. Independent first-party corroboration: the Astropy
  Project's own Open Collective account carries a dedicated sub-account named "Astropy Gemini"
  (typed a Project in Open Collective's own account taxonomy, at
  `opencollective.com/astropy/projects/astropy-gemini`), alongside the per-award sub-accounts it
  maintains for its NASA and Moore grants — so Gemini support is
  something the project itself accounts for separately, not merely a courtesy line in a paper's
  acknowledgements. The money reaches Gemini through a chain — Gemini is a
  program of NSF NOIRLab, which AURA manages under a cooperative agreement with the National Science
  Foundation — and the settled rule applied here is that the field records the entity the source
  names as awarding the money, not the governance chain behind it. NSF NOIRLab and the U.S. National
  Science Foundation are therefore recorded below as considered and rejected, with the reasoning.
- **NumFOCUS** — "We also thank NumFOCUS and the Python Software Foundation for financial support."
  NumFOCUS is also the Project's fiscal sponsor: it administers all the grants on the Project's
  behalf, and before institutional funding existed it "covered most of the incurred operational
  costs." The README's statement that Astropy is sponsored by NumFOCUS corroborates this.
- **Python Software Foundation** — named in the same sentence as NumFOCUS for financial support. **No
  ROR is recorded because none exists**: a quoted registry query for "Python Software Foundation"
  returns no organization. **Do not substitute https://ror.org/012prn105** — an unquoted query
  surfaces that record, but it is the *Python in Heliophysics Community*, a different organization
  entirely. This near-miss is recorded precisely because it is an easy and plausible error.
- **Google** — "We thank Google for financing and organizing the Google Summer of Code (GSoC)
  program, that has funded severals students per year to work on Astropy related projects over the
  summer. These students often turn into long-term contributors." The support is indirect, arriving
  through a program rather than as a grant to the Project, but it is money that paid people to work
  on Astropy and the paper places it alongside the other financial-support acknowledgements. *Naming
  note:* the ROR record's display name is "Google (United States)" (aliases "Google Research",
  "Googleplex"); the paper says simply "Google", which is what is recorded here.

**Correction to a previous value.** The prior record stated that "the Astropy 2022 paper acknowledges
support from the Heising-Simons Foundation, NSF, NASA, and STScI." **The 2022 paper does not mention
Heising-Simons at all** — a full-text search of the paper (ADS bibcode `2022ApJ...935..167A`) returns
no hit for "Heising-Simons", while the same search across the literature returns thousands of papers
and a deliberately nonsensical control term returns none, so the absence is real rather than an
artifact of the index. The claim was false and the funder must not be restored. (Searched the same
way and likewise absent from the 2022 text: "GBMF" and "Sloan". Sloan and Moore appear in the 2018
paper only, and there only in an individual author's personal eScience support.) The NSF and STScI
parts of that claim are addressed below.

**Considered and deliberately excluded.**

- **U.S. National Science Foundation** (https://ror.org/021nxhr62), **NSF NOIRLab**
  (https://ror.org/03zmsge54) and the **Association of Universities for Research in Astronomy
  (AURA)**. All three appear in the Gemini acknowledgement — "the international Gemini Observatory, a
  program of NSF's NOIRLab, which is managed by the Association of Universities for Research in
  Astronomy (AURA) under a cooperative agreement with the National Science Foundation, on behalf of
  the Gemini partnership of…". That sentence is Gemini's standard required attribution boilerplate; it
  describes the observatory's governance and management chain, not entities that awarded funds to
  Astropy. The paper's own body text identifies the money as a Gemini Observatory contract. Recording
  the chain would put three organizations in this field on the strength of a facility's mandated
  credit line, and would do so for every project Gemini has ever supported. `International Gemini
  Observatory` is recorded instead as the proximate named supporter, and these three are not. The
  boilerplate quoted here is the whole of the evidence that would support adding
  `U.S. National Science Foundation`; it was weighed and found to be governance language rather than
  an award, so no further research on this point is needed.
- **Space Telescope Science Institute**, **Harvard-Smithsonian Center for Astrophysics** and the
  **South African Astronomical Observatory**. The paper thanks "institutions that make it possible for
  astronomers and other developers on their staff to contribute their time to the development of
  Astropy projects" and then names these three. That is in-kind staff time, not a financial award to
  the Project. This is also the correct disposition of the "STScI" part of the previous record's
  claim.
- **University of Toronto / Dunlap.** The Project "received financial support from the Dunlap Seed
  Funding program at the University of Toronto to develop educational resources for scientific
  software packaging within the Learn Astropy framework", and a separate "grant from the Dunlap
  Institute" supported the Learn Astropy website infrastructure. Both funded the Learn Astropy
  educational program, which is a distinct deliverable from the core library this record describes.
- **National Radio Astronomy Observatory (NRAO).** The paper says the Project "indirectly benefited
  from the NRAO ALMA Development Study program, which supported the grant 'Linking CASA to the astropy
  ecosystem'". The paper's own word is "indirectly", and the funded work was in separate packages.
- **The roughly twenty per-author fellowships and grants** in both papers' acknowledgements — among
  them Macquarie iMQRES; Hungarian Academy LP2018-7 and KKP-137523; ANID BASAL FB210003 and FONDECYT
  1211000; H2020 ERC 683184 and 695671; STFC ST/S000240/1; Danish National Research Foundation
  DNRF106; MIT Pappalardo; ERC DMIDAS GA 786910; the Canadian Space Agency and NRC Herzberg;
  MINECO-FEDER RTI2018-096188-B-I00; PID2019-107061GB-C63 and Severo Ochoa SEV-2017-0709; NSF GRFP
  1842402; ASTRO 3D CE170100013; NSERC CGSD-54721-2020; and from the 2018 paper SAO SV3-73016,
  NAS8-03060, Hubble Fellowship 51316.01 / NAS 5-26555, FONDECYT 1170618, MINEDUC-UA ANT 1655/1656,
  DFG SFB 881, an ESO Fellowship, NSF AST-1313484 and AYA2016-75808-R. These fund individuals who
  co-authored the paper, not the software.
- **GitHub, Azure Pipelines, CircleCI, Read the Docs, NASA ADS and SIMBAD/CDS.** Thanked in the same
  section as services the project relies on. They are infrastructure providers, not funders.

*Machine-readable funding metadata on the software DOI is empty* — DataCite reports
`fundingReferences: []` and Zenodo reports `grants: null` — so the archive records cannot supply or
corroborate this field. The paper's Crossref funding block does carry structured data, but only for
two of the six funders above, which is why the acknowledgements and body text are the primary source.

### 26. Award Title (OPTIONAL)

**Award 1**
- **Award Title:** Sustaining and Growing the Astropy Project
- **Award Number:** GBMF8435
- **Funder:** Gordon and Betty Moore Foundation

This is an **official title from the funder's own grant database**, not a descriptive phrase. The
Moore Foundation's grant record for GBMF8435 gives Grant Name "Sustaining and Growing the Astropy
Project", recipient organization NumFOCUS, Inc., awarded October 2019, $900,900 over a 36-month term,
with the purpose "In support of sustaining the Astropy project, an open-source framework for
data-driven research and discovery in astronomy." The reference publication independently quotes the
same proposal title, and the paper's Crossref funding metadata supplies the grant number GBMF8435
against the Moore Foundation. Title and number are therefore each confirmed by two independent
sources.

**Award 2**
- **Award Title:** NASA ROSES-2020 E.7 Support for Open Source Tools, Frameworks, and Libraries
- **Award Number:** 80NSSC22K0347
- **Funder:** National Aeronautics and Space Administration

The award number is certain and triply attested: the 2022 paper's acknowledgements ("NASA under Grant
No. 80NSSC22K0347 issued through the NASA ROSES program"), the paper's Crossref funding metadata, and
the U.S. federal spending record, which lists award 80NSSC22K0347 to NUMFOCUS, INC. from the National
Aeronautics and Space Administration, $634,590, period of performance 2022-03-01 to 2026-02-28.

**What the recorded title actually names, and the caveat that must travel with it.** The title above
is the **funding call**, not the funded proposal: NASA ROSES-2020 element E.7, "Support for Open
Source Tools, Frameworks, and Libraries". The reference publication states it directly — "A
successful proposal to the NASA ROSES-2020 call, section E.7 (Support for Open Source Tools,
Frameworks, and Libraries)" — so its provenance is NASA-primary and unambiguous, and at 76 characters
it is well inside the 128-character limit on an award title. But it should not be read as the
proposal's own title, because **no official proposal title exists in any primary source**. The
federal award record has no title field at all — only a truncated copy of the proposal abstract,
beginning "THE PYTHON LANGUAGE HAS SEEN INCREASINGLY WIDE USE IN ASTRONOMY…" — and neither the paper,
nor `CITATION.cff`, nor the DataCite or Zenodo records carries an award title. That negative research
stands: a future agent should not assume a formal title was simply missed, and should not silently
replace this value with a guess at one. If NASA's own title for the proposal is ever located in a
primary source, that is the value to substitute.

An award also cannot be stored without a title, so leaving the title empty would not have preserved
"no formal title is known" — it would have dropped award number 80NSSC22K0347 from the record
entirely, losing the part that actually identifies the grant.

**Considered and rejected: "Sustaining the Astropy Project."** This is the description the Astropy
Project itself attaches, on Open Collective, to the sub-account it created to administer this grant, whose
account name is "Astropy NASA ROSES20 80NSSC22K0347" — tying it unambiguously to this award number.
It was a serious candidate, and it has the merit of being the grantee's own words about this specific
grant. It was not selected because it is a grantee's descriptive phrase rather than NASA-primary
text, and because it sits three words from the Moore award's official title, "Sustaining **and
Growing** the Astropy Project". The call-name title recorded above has neither drawback. This
alternative is documented so it is not re-proposed as a discovery.

**The two awards must not be merged.** `GBMF8435` (Gordon and Betty Moore Foundation) and
`80NSSC22K0347` (National Aeronautics and Space Administration) are distinct awards from different
funders, with different amounts, terms and titles. They are recorded as two separate entries and
neither should be folded into or "corrected" against the other.

**Considered and firmly rejected: "Investing in the Astropy Project to Enable Research and Education
in Astronomy"** (PI Erik Tollerud, NumFOCUS). **This is a different, later award** and attaching it to
80NSSC22K0347 would be an error. It comes from a NASA release announcing open-source
foundation/sustainment awards — alongside Astroquery, Matplotlib and Cartopy, the SunPy Ecosystem and
NumPy/SciPy/scikit-learn — under a later solicitation, not ROSES-2020.

**Known follow-up for a future refresh:** Astropy holds NASA funding subsequent to 80NSSC22K0347 (the
award just described), under award number **80NSSC25M7029** — a cooperative agreement to NumFOCUS,
Inc. from the National Aeronautics and Space Administration, $614,468, with a period of performance
running 2025-03-01 to 2030-02-28. It is recorded as a federal assistance award, so the number appears
as the FAIN rather than a PIID.

**What ties that number to Astropy specifically, and why the tie is needed.** The federal record
alone cannot establish it: NumFOCUS is a fiscal sponsor for many projects, and it held **nine** NASA
assistance awards as of a 2026-08-26 federal-spending query — a floor rather than a fixed figure,
since it rises as new awards are made — several of them similarly shaped cooperative agreements with
nothing but generic ROSES boilerplate in the description field. Two are actively confusable — `80NSSC25M7038`
(NumFOCUS, NASA, $377,884, 2024-12-01 to 2029-11-30) is a near-twin of `80NSSC25M7029`, and
`80NSSC22K0348` sits immediately adjacent to Astropy's own `80NSSC22K0347`. Recipient plus agency is
therefore **not** sufficient to identify an Astropy award, and any future refresh that matches on
those two fields alone will pick the wrong one.

The distinguishing evidence is first-party: the Astropy Project's own Open Collective account carries
a dedicated sub-account named **"Astropy NASA ROSES24 80NSSC25M7029"** (typed a Project in Open
Collective's account taxonomy, at `opencollective.com/astropy/projects/roses-24`). Because the
project itself names the award number on an account it controls, the attribution does not rest on
inference from the federal record.

The scope of that precedent is worth stating precisely, because it is narrower than it first appears.
Open Collective was already used earlier in this field, but only for **Award 2** (`80NSSC22K0347`),
and there only to source a *rejected* title alternative — not to establish the award number, which
came from the paper and the federal record. **Award 1** (Moore, `GBMF8435`) has no Open Collective
citation elsewhere in this field at all; its number and official title rest on the Moore Foundation's
own grant record. The sibling sub-accounts "Astropy NASA ROSES20 80NSSC22K0347" and "Astropy Moore
8435" (described "Sustaining and Growing the Astropy Project") are noted here as **additional
corroboration**, not as evidence this field previously relied on for either award.

This is not yet a complete third entry for this field, because it has the same defect as
80NSSC22K0347: the federal spending record carries no title, only the generic ROSES solicitation
boilerplate ("THE ROSES FUNDING OPPORTUNITY GOALS ARE: EXECUTE A BALANCED SCIENCE PROGRAM…"), so no
official proposal title is available from a primary source. Adding it would require settling a title
of record the same way this field settled the other two.

Whether 80NSSC25M7029 is the award behind the "Investing in the Astropy Project to Enable Research
and Education in Astronomy" title rejected just above is **unconfirmed** — the recipient, the funder
and the later-solicitation timing are all consistent, but no source examined states the link, and it
must not be assumed on circumstantial agreement alone.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.3847/1538-3881/aabc4f — "The Astropy Project: Building an Open-science Project
  and Status of the v2.0 Core Package", Astropy Collaboration et al. 2018, AJ 156, 123
  (arXiv:1801.02634)
- https://doi.org/10.1051/0004-6361/201322068 — "Astropy: A community Python package for astronomy",
  Astropy Collaboration et al. 2013, A&A 558, A33 (arXiv:1307.6212)

`astropy/CITATION` ships BibTeX for three papers and asks users to cite all three; the most recent is
promoted to Field 14 and these two remain here.

**The `CITATION.cff` `references` block contains exactly these two entries and no others.** The block
runs from its `references:` key to the end of the file, and holds two reference items: the 2018 paper
(with DOI 10.3847/1538-3881/aabc4f, arXiv DOI 10.48550/arXiv.1801.02634, ADS bibcode
`2018AJ....156..123A`, and open-access publisher and arXiv PDF links) and the 2013 paper (with DOI
10.1051/0004-6361/201322068, arXiv DOI 10.48550/arXiv.1307.6212, ADS bibcode `2013A&A...558A..33A`,
and an open-access publisher PDF at aanda.org). There is no third entry.

*A discrepancy inside `CITATION.cff` worth knowing about, so it is not "fixed" in the wrong
direction:* the 2018 entry sets `journal: "The Astrophysical Journal"` with `volume: 156`, while the
ADS bibcode in the same entry is `2018AJ....156..123A` — *The Astronomical Journal*. The bibcode and
the DOI are correct; the journal name in the CFF file is the error. The title recorded above follows
the DOI.

### 28. Related Datasets (OPTIONAL)
**Not found** — astropy publishes no dataset.

It is a library. It does bundle and fetch reference data — physical constants, the observatory site
registry (hosted in the separate astropy-data repository), IERS Earth-orientation tables (shipped by
the separate `astropy-iers-data` package), and JPL DE-series ephemeris kernels fetched on demand —
but none of these is a scientific dataset that astropy publishes or curates, and each belongs to a
different upstream.

### 29. Related Software (OPTIONAL)

- https://github.com/liberfa/erfa — **ERFA** (Essential Routines for Fundamental Astronomy)
- https://github.com/liberfa/pyerfa — **PyERFA**, the Python wrapper
- https://github.com/astropy/astropy-iers-data — **astropy-iers-data**
- https://github.com/astropy/pyvo — **PyVO**
- https://github.com/brandon-rhodes/python-jplephem — **jplephem**

Every URL above was confirmed to resolve at extraction time. This field carries *distinguishing*
software — domain-specific dependencies and a designated successor — as distinct from the
interoperability partners in Field 30.

- **ERFA / PyERFA** — `pyproject.toml` requires `pyerfa>=2.0.1.3`. This is not generic
  infrastructure: ERFA is the fundamental-astronomy routine library that astropy's time and
  coordinate machinery is built on, and it derives from the IAU SOFA Collection. Both the 2018 and
  2022 papers acknowledge it explicitly: astropy "makes use of the ERFA library, which in turn
  derives from the IAU SOFA Collection." Both the C library and its Python wrapper are listed because
  they are separately released and separately identified.
- **astropy-iers-data** — `pyproject.toml` requires it, pinned to a dated version. It supplies Earth
  orientation reference data (UT1-UTC and polar motion), a domain-specific data dependency with its
  own release cadence; the repository carries a dedicated `update_astropy_iers_data_pin.yml` workflow
  to track it. Its prominence is current: the single API change in v8.0.1 (Field 12) is about when
  astropy falls back from this bundled table to a network download.
- **PyVO** — the **designated successor** to a deprecated part of astropy. `astropy/samp/__init__.py`
  and `docs/samp/index.rst` both state: "`astropy.samp` was deprecated in version 8.0 and will be
  removed in a future version; please use `pyvo.samp` instead." A user of `astropy.samp` needs to know
  where that functionality went, which is exactly what this field is for. *It was also considered for
  Field 30* — `astropy/io/votable/tree.py` describes VOTable content "meant to be parsed by the
  calling API (e.g., PyVO)", a real exchange — but the successor relationship is the stronger and more
  useful fact, and an entry belongs in one field.
- **jplephem** — an optional dependency documented in `docs/install.rst` as being used "to retrieve
  JPL ephemeris of Solar System objects", underpinning `solar_system_ephemeris` and `get_body`.
  Narrow and astronomy-specific: it would be out of place in a web application or a finance model,
  so the generic-infrastructure exclusion does not reach it.

**Considered and excluded — generic infrastructure.** `numpy`, `packaging` and `PyYAML` are
`pyproject.toml` *required* dependencies and belong in **neither** this field nor Field 30, along with
`setuptools`, `setuptools_scm`, `cython` and `extension-helpers` from the build requirements. Being a
dependency is not a relationship worth recording: "it depends on numpy" is true of nearly every
package in the scientific Python ecosystem and carries no information. The same reasoning excludes the optional
`bottleneck`, `mpmath` and `pytz`.

**Considered and excluded — Astropy coordinated and affiliated packages without specific evidence.**
`photutils`, `regions`, `reproject`, `synphot`, `ndcube`, `specreduce`, `astropy-healpix` and the rest
of the Astropy affiliated/coordinated registry. A previous version of this record
listed photutils, regions and reproject here on the warrant "Astropy coordinated package". That is a
blanket ecosystem claim: it would read identically for every member of that registry, and an entry that would
read the same for an arbitrary package carries no information. The repository at the pinned revision
contains no substantive reference to any of them — searches for `photutils`, `synphot` and `ndcube`
return nothing at all; there is no import of, dependency declaration for, or documentation
cross-reference to the `regions` package, its apparent matches being the ordinary English word; and
the matches for `reproject` are the filenames of bundled example images
(`reprojected_sdss_*.fits.bz2`), not the package. **The ones that survive are in Field 30, and they survive because astropy's own
documentation names a specific exchange with each.** Coordinated- or affiliated-package membership is
not on its own a reason to list a package in either field, and it is settled here that it is not used
as one; reintroducing three arbitrary members of that registry on membership alone is the specific
error this note exists to prevent.

*Not related software:* the ASCL entry `ascl:1304.002` recorded in `CITATION.cff` is an identifier for
astropy itself, not a separate package.

### 30. Interoperable Software (OPTIONAL)

- https://github.com/sunpy/sunpy — **SunPy**
- https://github.com/astropy/specutils — **specutils**
- https://github.com/astropy/ccdproc — **ccdproc**
- https://github.com/jehturner/ndmapper — **ndmapper**
- https://github.com/spacetelescope/gwcs — **gwcs**
- https://github.com/astropy/asdf-astropy — **asdf-astropy**
- https://github.com/astropy/astroquery — **astroquery**
- https://www.star.bristol.ac.uk/mbt/topcat — **TOPCAT**
- https://ds9.si.edu/ — **SAO DS9**

Every URL above was confirmed to resolve at extraction time. Each entry is admitted on a **specific,
first-party, cited exchange** — a shared data model, an implemented shared API, a plugin relationship,
or a documented cross-language format handoff — and not on ecosystem membership.

- **SunPy** — shared data model. `docs/nddata/index.rst`: "The SunPy project uses
  `~astropy.nddata.NDData` as the foundation for its Map classes." SunPy is also the named
  heliophysics peer that defers to astropy for the HAE frame (Field 4).
- **specutils** — shared data model. `docs/nddata/index.rst`: `NDDataRef` "is used in specutils as the
  basis for `Spectrum1D`, which adds several methods useful for spectra."
- **ccdproc** — shared data model. `docs/nddata/index.rst`: ccdproc "uses the `~astropy.nddata.CCDData`
  class throughout for implementing optical/IR image reduction."
- **ndmapper** — shared data model, named in the same first-party list: it "uses
  `~astropy.nddata.NDDataArray` as its image object." Its own description confirms it maps files on
  disk to collections of astropy NDData objects. It is a small project, but it is admitted on exactly
  the criterion applied to ccdproc and specutils, and excluding it on prominence would be an
  unprincipled distinction.
- **gwcs** — implemented shared API. `docs/wcs/wcsapi.rst` explains that astropy defines the APE 14
  standardized Python WCS interface (https://doi.org/10.5281/zenodo.1188874) and provides its
  low- and high-level base classes in `astropy.wcs.wcsapi`, naming gwcs as the other implementation
  for transformations FITS WCS cannot represent. Two independent WCS implementations behind one
  interface is interoperability in the strictest sense.
- **asdf-astropy** — plugin/extension relationship. `docs/install.rst` lists it as the optional
  dependency that "enables the serialization of various Astropy classes into a portable,
  hierarchical, human-readable representation", and `docs/modeling/models.rst` carries
  `.. doctest-requires:: asdf-astropy` directives plus a cross-reference into its documentation for
  model serialization. ASDF support for astropy objects lives in that package, not in-tree.
- **astroquery** — output of one consumed by the other, with worked examples.
  `docs/coordinates/apply_space_motion.rst` demonstrates importing `astroquery.gaia` and
  `astroquery.vizier` and feeding the results into astropy coordinate objects;
  `docs/timeseries/index.rst` and `docs/io/ascii/read.rst` point at it for data retrieval. Astroquery
  returns astropy `Table` and `SkyCoord` objects, which is the exchange.
- **TOPCAT** — cross-language format interchange, and **this survives the SAMP deprecation
  independently**. `docs/io/ascii/ecsv.rst` states that "In addition to Python, ECSV is supported in
  TOPCAT and in the Java STIL library", and `docs/io/ascii/index.rst` repeats it when recommending
  ECSV as the reproducible text table format. ECSV is astropy's own format, readable by a named Java
  desktop tool — a genuine bridge that has nothing to do with `astropy.samp`. The URL recorded is the
  one astropy's own `docs/conf.py` defines for the `|TOPCAT|` substitution.
- **SAO DS9** — a first-party adapter, and this too is **independent of the SAMP deprecation**.
  `astropy/wcs/wcs.py` implements `WCS.footprint_to_file()`, which "writes out a `ds9` style regions
  file. It can be loaded directly by `ds9`", emitting a real `# Region file format: DS9 version 4.0`
  header and accepting a DS9 coordinate system. That is a converter API in astropy's own code.
  (`astropy/visualization/basic_rgb.py` separately documents its clipping-and-scaling procedure as
  following the DS9 image algorithm.) *URL note:* `https://ds9.si.edu/` is the project-controlled
  address astropy's documentation cites; it forwards to the tool's current home at
  `https://sites.google.com/cfa.harvard.edu/saoimageds9`.

**Removed: NumPy, SciPy, Matplotlib, pandas, Polars, and Apache Arrow / PyArrow.** All six were listed
in a previous version of this record and all six are generic infrastructure. Each fails the test
directly: arrays, numerical routines, plotting, dataframes and columnar storage would be equally at
home in a web application, a finance model or a biology pipeline. Being a required or recommended
dependency is not interoperability.

**The dataframe interchange does not rehabilitate pandas, Polars or Arrow, and this is the specific
argument to resist.** Astropy has genuinely rich, documented dataframe interchange:
`Table.to_pandas()`, the narwhals-backed `to_df()` / `from_df()` API documented in
`docs/table/dataframes.rst` and `docs/table/table_and_dataframes.rst` (with `pandas.rst` noting the
documentation moved there as of Astropy 7.2), a changelog entry extending `to_pandas()` to
multidimensional columns, and the connectors in `io/misc/pandas/connect.py` and
`io/misc/pyarrow/csv.py`. All of that is real — and it is exactly the special pleading the relevance
gate forbids, because a *general-purpose dataframe library* is generic infrastructure whether or not
a converter exists. Admitting it would set a precedent under which every package with a
`to_pandas()` method lists pandas here. `narwhals` is excluded for the same reason, as are `h5py`,
`dask`, `PyYAML`, `packaging`, IPython/Jupyter/ipywidgets/ipydatagrid, `fsspec`/`s3fs` and `certifi`.

**A structural note about how this field must be read for astropy specifically.** Astropy is usually
on the other side of this test: it is the package whose inclusion in someone *else's* Field 30 has to
be justified with cited evidence. That inverts here. Field 30 entries on astropy's own record must be
judged as astropy's **peers**, not as things that depend on astropy — nearly every astronomy and
heliophysics package in Python depends on astropy, and listing them would carry no information.

**Considered and dropped: Aladin.** It was a candidate as a SAMP desktop client, and it fails on a
ground stronger than the deprecation. Every mention of Aladin in the repository sits inside
`docs/samp/` — the deprecated subpackage's documentation — apart from one historical GLU-reference URL
in a VOTable exception docstring and one incidental test-data string. Unlike TOPCAT (ECSV) and DS9
(`footprint_to_file`), **Aladin has no interoperability link that survives `astropy.samp`'s removal.**

**Considered and folded into TOPCAT: STIL.** `docs/io/ascii/ecsv.rst` and `docs/io/ascii/index.rst`
name the Java STIL library alongside TOPCAT as an ECSV reader. It is the table-I/O library underlying
TOPCAT, from the same author and project, and the exchange cited is identical, so listing both would
double-count one relationship. TOPCAT is recorded as the named end-user tool.

**Considered and not selected: the Astropy coordinated and affiliated registry at large** — see
Field 29, where the same reasoning is set out. Blanket claims of the form "part of the standard
scientific Python ecosystem" or "an Astropy affiliated package, so it interoperates with Astropy" are
never sufficient on their own.

### 31. Related Instruments (OPTIONAL)
**Not found** — a documented omission, not an extraction gap.

**Relevance gate.** Astropy is instrument-agnostic. It supports no instrument's data format,
calibration or convention as a design goal. The one genuinely mission-specific capability found is
`astropy/timeseries/io/kepler.py`, which registers `kepler.fits` and `tess.fits` TimeSeries readers
(both served by `kepler_fits_reader`) — real Kepler and TESS light-curve format support. Those are
exoplanet-survey missions, outside heliophysics scope.

**Vocabulary resolution — negative research worth keeping.** The instrument/observatory vocabulary was
searched, by both row name and abbreviation, for each astronomy mission or service astropy touches:
Kepler, TESS, "Transiting Exoplanet", James Webb / JWST, Hubble, Chandra, Gemini, SIMBAD, VizieR, Gaia
and SDSS (and Sloan). **None of them has a row.** The absence is structural rather than an oversight:
the vocabulary is SPASE-backed and heliophysics-scoped — at extraction, no row carried an identifier
outside the `https://spase-metadata.org/` namespace, so the prefix guard held across the table — and
these are astronomy facilities that SPASE does not carry. That is a dated observation about the
vocabulary rather than a permanent property of it, but the consequence for astropy is durable: there
is no defensible value to record, and **no name may be free-typed**, because a bare name with no
SPASE identifier either binds to an arbitrary same-name row or creates a new identifierless one.

**Also excluded by the relevance gate:** `EarthLocation.of_site()` in `astropy/coordinates/earth.py`.
It looks up ground-based observatory positions from a registry hosted in the astropy-data repository,
and its own docstring says it is "not a fully-featured exhaustive registry of observatories". That is
the "configurable for a location or observatory while otherwise agnostic" case the gate excludes, and
it is a generic site lookup rather than support for any particular facility's data.

### 32. Related Observatories (OPTIONAL)
**Not found** — same reasoning as Field 31, and the same documented omission.

The Kepler and TESS platforms have no rows in the SPASE-backed vocabulary (verified alongside the
instrument search above), so the ladder's observatory-level substitution — recording the platform when
its instrument is missing — has nothing to substitute *to*. The `EarthLocation.of_site()` registry is a
generic multi-observatory lookup and confers no observatory association.

A previous version of this record reached the same conclusion but recorded only that astropy is
"observatory-agnostic". The vocabulary check above is added so the emptiness is demonstrably correct
rather than merely asserted.

### 33. Logo (OPTIONAL)
- **URL:** https://raw.githubusercontent.com/astropy/repo_stats/91d5871e034edb72af832ff662acd9ae5146fdc4/dashboard_template/astropy_banner_gray.svg

This is the Astropy banner the README itself uses as the project logo (`README.rst` defines the
`|Astropy Logo|` substitution from this image, targeting `https://www.astropy.org/`), served in raw
form. The URL returns the SVG document itself, with content type `image/svg+xml`.

**Correction to a previous value.** The prior record used the README's own link verbatim:
`https://github.com/astropy/repo_stats/blob/main/dashboard_template/astropy_banner_gray.svg`. That is
a GitHub **blob** URL — a web page *about* the file. It returns `text/html`, not an image, so anything
consuming this field as an image source gets a rendered HTML page. The raw form of the same asset is
recorded instead. **Do not restore the blob URL even though it is what the README contains.**

The raw URL is further pinned to the commit the banner file is at, rather than to `main`. A branch
reference breaks silently the moment the file is renamed, moved or deleted — which matters more than
usual here, since the asset lives in the `dashboard_template/` directory of a *separate* repository
(`astropy/repo_stats`) whose layout is not governed by Astropy's release process. The pin also
partly answers the fragility flagged below: the location can still change, but the recorded URL can no
longer silently start serving something else.

**Considered and not selected: https://www.astropy.org/_images/astropy_project_logo.svg.** The project
website does host a compact, genuine Astropy Project logo mark (about 10 kB, correctly served as
`image/svg+xml`) — a more canonical logo in the strict sense than the ~400 kB gray banner, which lives
in the `dashboard_template/` directory of the separate `repo_stats` repository. It was not selected
because it sits under a Sphinx-generated `_images/` path, which is a documentation build artifact
whose location can change when the site is rebuilt, whereas the banner is the image the project's own
README designates as its logo. Both resolve; if the banner's location in `repo_stats` ever proves
unstable, this is the replacement to reach for, and it needs no further research.

*Attribution note, from `docs/credits.rst`:* the Astropy logos were designed by Kyle Barbary.
