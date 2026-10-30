# HSSI Metadata Extraction Results

**HSSI Software ID:** c46778bd-7352-44cd-91fe-010102bb8aa0
**Repository:** https://github.com/astropy/astropy
**Source Revision:** bada72aa79a2d1fd7c705ddc8175800c2eb1312d
**Extraction Date:** 2026-08-26
**Validation Date:** 2026-10-30
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

**Release note — `main` is not the release.** Astropy cuts its releases on release branches
(`v8.0.x`): no final release tagged after `v0.4` (2014-07-16) is an ancestor of `main`, and `main`
carries code for the next minor version that no release has shipped. The Source Revision above is a
`main` commit. Every file in this repository that the record cites exists at the `v8.0.2` tag
(`2268dbf1155e8ad10161c188afc60af3d35b3c8b`), and these capability claims hold there too: the solar
CTYPE map and observer parameters, `HeliocentricMeanEcliptic`, the MESA and TDAT reader modules,
FTPS support, `use_fsspec`, the `astropy.samp` deprecation, `NDSlicingMixin` and
`footprint_to_file`. Sections rewritten at the v8.0.2 release update (2026-10-29) name the revision
their evidence was read at. Code that exists only on `main` adds no value to a capability field
until a release ships it.

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

*Considered and not selected:* a version-specific DOI. Those belong in Field 12 (Version PID), not
here. Read on 2026-10-29, DataCite's record for this concept DOI presents the title `Astropy` and the
`version` `v8.0.1`, the newest deposit (10.5281/zenodo.21262391), while the current release is
v8.0.2, which has no deposit (Field 12). A concept DOI identifies the software across its versions, so
that lag does not affect this field.

*Also present in the same `identifiers:` block and deliberately not used here:* the ASCL entry
`https://ascl.net/1304.002`. It is a registry listing rather than a persistent identifier that
resolves to the software artifact, and HSSI accepts one persistent identifier in this field.

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/astropy/astropy

Recorded independently in `pyproject.toml` under `[project.urls] repository`, in `CITATION.cff` as
`repository-code`, and as the canonical GitHub repository (default branch `main`).

### 4. Software Functionality (RECOMMENDED)

- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Solar
- Coordinate Transforms: Planetary
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

**Coordinate Transforms: Planetary — restored at the v8.0.2 release update.** Astropy has converted
planetary coordinates as a user-facing capability since version 6.0, whose changelog records "Support
WCS descriptions of basic planetary coordinate frames. [#14820]" and "Add
``BaseBodycentricRepresentation``, a new spheroidal representation for bodycentric latitudes and
longitudes. [#14851]". Read at the `v8.0.2` tag (`2268dbf1155e8ad10161c188afc60af3d35b3c8b`):

- `astropy/wcs/utils.py` maps a planetary FITS WCS, whose celestial CTYPE prefix names a body in
  `SOLAR_SYSTEM_OBJ_DICT` (Earth, the Moon, Mercury, Venus, Mars, Jupiter, Saturn, Uranus and Neptune),
  to a body-fixed frame for that body (`solar_system_body_frame`), with a bodycentric or a
  planetographic representation built from the body's radii in the WCS auxiliary keywords (triaxial
  bodies are not supported). `celestial_frame_to_wcs`, in the module's public `__all__`, writes such a
  frame back as a WCS. The high-level WCS API reaches it: `astropy/wcs/wcsapi/fitswcs.py` calls
  `wcs_to_celestial_frame`, so `pixel_to_world` on a planetary image returns coordinates in the
  body-fixed frame.
- `astropy/coordinates/representation/geodetic.py` defines `BaseBodycentricRepresentation` and
  `BaseGeodeticRepresentation`, exported from `astropy.coordinates`, which convert planetocentric and
  planetographic coordinates on any spheroid to and from body-fixed Cartesian.
  `docs/coordinates/representations.rst` gives a Mars planetographic and a Mars bodycentric
  representation as its examples (`IAUMARS1979GeodeticRepresentation`,
  `IAUMARS2000BodycentricRepresentation`), and `docs/wcs/creating_planetary_wcs.rst` builds a
  planetary WCS.
- `astropy/wcs/docstrings.py` documents the wcslib planetary auxiliary parameters, among them
  `a_radius` (the "semimajor axis of the ellipsoid that defines the approximate shape of a target
  body") and `blon_obs` ("Bodycentric longitude of the observer in the body-fixed reference frame of
  the target body").
- `astropy/wcs/tests/test_utils.py` and `astropy/coordinates/tests/test_geodetic_representations.py`
  exercise it.

Chiara Marmo, who implemented it, describes the work with Stéphane Erard in "Planetary World
Coordinate System in Astropy" (Field 27), whose abstract says it "focuses on body-fixed frames to
support surface and atmosphere studies".

*History, kept so the reversal is understood.* An earlier record carried this value, and the
2026-08-26 extraction removed it. That extraction read the built-in frame export list in
`astropy/coordinates/builtin_frames/__init__.py` to its closing boundary (ICRS, FK5, FK4,
FK4NoETerms, Galactic, Galactocentric, Supergalactic, AltAz, HADec, GCRS, CIRS, ITRS, HCRS, TEME,
TETE, PrecessedGeocentric, GeocentricMeanEcliptic, BarycentricMeanEcliptic, HeliocentricMeanEcliptic,
GeocentricTrueEcliptic, BarycentricTrueEcliptic, HeliocentricTrueEcliptic, HeliocentricEclipticIAU76,
CustomBarycentricEcliptic, LSR, LSRK, LSRD, GalacticLSR, SkyOffsetFrame, BaseEclipticFrame,
BaseRADecFrame, plus `galactocentric_frame_defaults` and `make_transform_graph_docs`), found no
planet-fixed, planetocentric or planetographic frame there, and concluded that "the planetary case has
the CTYPE label and nothing else". The list is accurate, but the planetary frames are built on demand
in `astropy/wcs/utils.py`, outside `builtin_frames`, so the list could not show them; the code had
shipped in 6.0, so the removal was wrong when it was made. The two pieces of counter-evidence that
extraction set aside are still not grounds for the value:

- `astropy/coordinates/solar_system.py` exports `get_body`, `get_body_barycentric`,
  `get_body_barycentric_posvel` and `solar_system_ephemeris`, with `BODY_NAME_TO_KERNEL_SPEC`
  covering the Sun, Mercury, Venus, the Earth-Moon barycentre, Earth, the Moon, Mars, Jupiter,
  Saturn and the rest. That is solar-system *ephemeris positioning* — where a body is — not
  transformation between planetary coordinate systems.
- `astropy/wcs/wcsapi/fitswcs.py` maps the CTYPE codes `TLON`/`TLAT` to
  `pos.bodyrc.lon`/`pos.bodyrc.lat`. The 2026-08-26 record called this a label with "no accompanying
  frame"; at `v8.0.2`, `wcs_to_celestial_frame` maps a `TLON`/`TLAT` pair to ITRS, the Earth-fixed
  frame. Either way it describes Earth, not another body.

The asymmetry the 2026-08-26 record drew between this value and `Coordinate Transforms: Solar` no
longer holds: both rest on WCS world coordinates in body-referenced frames, with the body's or the
observer's parameters carried in the WCS auxiliary keywords. Astropy still has no magnetospheric frame
(GSE, GSM, SM or MAG), which Field 5 relies on.

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
`Coordinate Transforms: Heliospheric`, `Coordinate Transforms: Solar` and
`Coordinate Transforms: Planetary` are **capability** claims: they say astropy implements transforms
into heliocentric-ecliptic, solar WCS and planetary body-fixed coordinate descriptions. Field 5 asks a
different question — which physical region's *science* the software supports — and is answered there
with `Solar Environment`, on the strength of the solar CTYPE, solar-observer-parameter and HAE support
catalogued above. The planetary frames add no Region row: they serve work on a body's surface and in
its atmosphere, which no row describes (Field 5).

The asymmetry a future refresher is most likely to misread is the ephemeris one. The
heliospheric/ephemeris capability recorded here — `HeliocentricMeanEcliptic`, `HCRS`, and the
`get_body` / `get_body_barycentric_posvel` solar-system machinery — deliberately did **not** also
yield `Interplanetary Space` in Field 5. Positioning a solar-system body is astrometric
infrastructure: it tells you where Jupiter is, and does nothing with the plasma, fields or
energetic particles between the planets that `Interplanetary Space` denotes. A heliospheric
*coordinate* capability is therefore not evidence of interplanetary *science* support, and the
presence of `Coordinate Transforms: Heliospheric` here must not be used to argue
`Interplanetary Space` back into Field 5.

### 5. Related Region (RECOMMENDED)

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
- The form marks this field RECOMMENDED, not required (fields/05 treats it as critical), and an
  empty Region is a legitimate outcome for domain-independent tooling, so "the field must be filled"
  is never on its own a reason to fill it.
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

**Considered and rejected — the remaining `Region` rows, with reasons.** `Earth Magnetosphere` and
the Earth magnetospheric subregions: astropy has no GSE, GSM, SM, MAG or AACGM frame.
`Planetary Magnetospheres` and the Jupiter, Mars, Neptune, Saturn and Uranus magnetosphere rows:
astropy's planetary body-fixed frames (Field 4, `Coordinate Transforms: Planetary`) describe
positions on a body's surface and in its atmosphere, not a magnetosphere's physics, and a Region row
is not a planet filter (fields/05 rule 4), so they earn none of these rows. The 2026-08-26 version
of this note said astropy had "no planet-fixed frame"; Field 4 records why that was wrong.
`Earth Atmosphere`, `Earth Lower and Middle Atmosphere`, `Earth Ionosphere`, `Earth Thermosphere`
and `Earth Auroral Subregion`: no atmospheric, ionospheric or auroral model or data support.
`Photosphere`, `Chromosphere` and `Corona`: the WCS machinery is identical across all three, so
nothing in astropy selects among them, and choosing one would assert a specificity the code does not
have. `Solar Interior`, `Solar Wind` and `Heliosheath`: no corresponding capability.

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

The date the astropy repository was first created and made public. The form defines this field as
"Date of first broadcast/publication." and its fill-in guidance reads "Used for the initial version of
the software."; that is the first public availability of the code — not the 2013 A&A paper (Field 27)
and not the current release (Field 12). `sunpy`'s record applies the same convention and is the
named precedent for it.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

The DataCite record for the concept DOI names Zenodo as publisher. Zenodo is the archiving service
that mints and holds the DOI in Field 2.

### 12. Version (RECOMMENDED)
- **Version Number:** v8.0.2
- **Version Date:** 2026-10-15
- **Version PID:** Not found — no Zenodo deposit exists for v8.0.2 (see *Version PID* below)
- **Version Description:** the "Version 8.0.2 (2026-10-15)" section of `CHANGES.rst` at the `v8.0.2`
  tag, with whole items trimmed as *Version Description* below explains; the value is the text inside
  this fence, exactly:

```markdown
### API Changes

#### astropy.wcs

- Integer indices beyond the size of an axis are now rejected when slicing a ``SlicedLowLevelWCS`` with a known shape, as for Numpy arrays. In addition, ``simplify_basic_index`` now accepts `None` entries in ``shape`` for dimensions whose size is not known, in which case the index for that dimension is returned unchanged, except that a negative integer or slice start raises a ``ValueError``. [#20544]

### Bug Fixes

#### astropy.coordinates

- Fixed ``BaseRepresentation.represent_as`` mutating a source representation when converting attached differentials to another class, which could cause a repeated ``SkyCoord.apply_space_motion`` call after displaying the coordinate to fail. [#20095]

- Fixed two rounding errors in ``Angle.to_string``. The seconds were carried into the next minute half a unit too early, so that, e.g., ``Angle("1d2m59.49999s").to_string(precision=0)`` gave ``1d03m00s`` instead of ``1d02m59s``. And with ``fields=1`` the seconds were rounded into the minutes before the minutes were rounded into the degrees, rounding twice, so that, e.g., ``Angle("285d29m41.76s").to_string(fields=1)`` gave ``286d`` instead of ``285d``. [#20227]

#### astropy.io.ascii

- The ``latex`` and ``aastex`` readers no longer treat an ampersand inside a braced ``{...}`` group or an escaped ``\&`` as a column separator, so tables with a reference column such as ``\cite{2013A&A...558A..33A}`` now read correctly. [#20333]

#### astropy.io.fits

- Fixed ``fitsinfo`` and ``fitsheader`` crashing with a traceback when run on an LZW-compressed ``.Z`` file while the optional ``uncompresspy`` dependency is not installed. The scripts now broadly catch exceptions and report a clean error message, matching the behaviour of the ``fitscheck`` and ``fitsdiff`` scripts. [#19869]

- The ``ZQUANTIZ`` keyword is no longer written to the header of compressed image HDUs when no quantization is applied (i.e., for integer data, or floating point data compressed with ``quantize_method=NO_DITHER``). A few FITS readers, including DS9 and ``fv``, currently treat the mere presence of ``ZQUANTIZ`` as an indication that the data are quantized, regardless of its value, and cannot read the files.  Omitting the keyword when it is not needed is fully standards-compliant, as a missing ``ZQUANTIZ`` is already interpreted as ``NO_DITHER``. [#20313]

#### astropy.io.misc

- Fixed the ``format="ecsv"`` ECSV reader to correctly read an empty table that has no columns. Previously this was raising an ``InconsistentTableError``. The legacy ``format="ascii.ecsv"`` ECSV reader was already handling this case correctly. [#19909]

#### astropy.io.votable

- Prevent overflow on 32-bit systems and WebAssembly when reading binary VOTables by changing the ambiguous types of ``null_value`` to fixed-width equivalents (e.g., from ``long`` to ``int64_t``). [#20302]

- Passing an integer column index equal to the number of fields in ``columns`` now raises the intended ``ValueError``. [#20547]

#### astropy.modeling

- Fixed the step size used by the non-linear least-squares fitters (``LevMarLSQFitter``, ``TRFLSQFitter``, ``DogBoxLSQFitter``, and ``LMLSQFitter``) to estimate the Jacobian by finite differences when a model has no ``fit_deriv`` or when ``estimate_jacobian=True``. The relative step was the fourth root of the machine precision (about 1.2e-4) instead of the square root (about 1.5e-8), so fits could stop short of the minimum for parameters with large values, such as a position far from the coordinate origin. [#20462]

#### astropy.nddata

- Fix ``block_replicate`` with ``conserve_sum=True`` inadvertently promoting ``float16``, ``float32``, and ``complex64`` input arrays to wider dtypes. [#20364]

#### astropy.stats

- Fixed a bug where ``astropy.stats.histogram()`` raised a ``ValueError`` when both ``range`` and ``weights`` were provided with a scalar number of bins. For scalar bin counts, ``calculate_bin_edges()`` now delegates range filtering directly to ``numpy.histogram_bin_edges()``, avoiding an array shape mismatch between data and weights while reserving manual range filtering for Astropy's string-based bin width estimators. [#20008]

- Fixed an out-of-bounds memory read in the C implementation of ``sigma_clip`` (used when ``axis`` is given with ``cenfunc``/``stdfunc`` set to their string values) that occurred when a clipping iteration rejected all remaining values. This could cause a crash or return incorrect (unmasked) results; the fast path now returns the same result as the pure-python implementation in this case. [#20393]

#### astropy.table

- Fixed issue with table groups for zero-length tables in ``astropy.table``. Previously operations like ``len(tbl.group_by("a").groups)`` or ``len(tbl.groups)`` would fail or give inconsistent results if the table ``tbl`` had no rows. [#20031]

- Fixed an issue when deep-copying a ``Table`` where the copied columns lost their link to the new parent table. This led to problems in ``rename_columns`` and ``info.name`` assignment. Other potential problems included table-aware unit conversion/replacement in QTable, grouped-column linkage to table group metadata, and synchronized pprint include/exclude name bookkeeping on rename or delete. [#20088]

- Fixed an issue where ``vstack`` was returning the input table itself when given a single table. It now returns a copy of that table, consistent with the documented behavior of always returning a new table. [#20097]

- Fixed ``Table.to_pandas()`` and ``Table.to_df()`` silently corrupting masked integer columns whose values are too large to be represented exactly as a float64, e.g. Gaia source ids. The nullable integer column is now built directly from the integer data and the mask instead of via a float64 intermediate. Only the pandas backend was affected; polars and pyarrow already round-tripped these values exactly. [#20240]

- Fixed a bug where a numpy function used on a ``MaskedColumn`` produced output with a different dtype than the input (e.g., ``np.strings.find``), which would later lead to a ``TypeError`` from a stale ``fill_value`` dtype. Now, when the fill_value is no longer valid for the output dtype, fall back to the default fill_value for that dtype instead of propagating the stale value. This can now raise a castings warnings following standard numpy casting rules. [#20265]

- Fixed a memory leak when repeatedly slicing a table that has an index on a ``MaskedColumn``, e.g. ``t[t["idx"] == value]``. Each such access used to make a deep copy of the whole index that was never freed, and any slice of a slice of an indexed ``MaskedColumn`` (or a derived array such as a comparison result) silently shared the original column's index. [#20456]

#### astropy.time

- Fixed ``Time.__setitem__`` silently dropping the mask when a masked ``Time`` was assigned into an unmasked one. As a result, ``vstack`` no longer loses the mask on ``Time`` mixin columns. [#20178]

- Fixed a bug where ``Time.insert`` (and therefore ``Table.add_row`` for a ``Time`` column) silently dropped the mask, exposing values that should have stayed masked.  This affected both the mask of the original object and the mask of the inserted values. [#20232]

- Fixed ``Time.strftime`` and the string formats (``iso``, ``isot``, ``fits``, ``yday``) returning values at the wrong index for a ``Time`` array that is not C-contiguous in memory, for example after ``.T`` or ``np.moveaxis``, or when built from a Fortran-ordered array. [#20496]

#### astropy.utils

- Fixed an issue where, in a multi-threaded context, astropy's logger could race with imports, leading to an exception being raised. [#20064]

- Flipped ``astropy.utils.data.conf.dataurl`` and ``astropy.utils.data.conf.dataurl_mirror`` to reduce URL redirect, in hope to reduce service denial. [#20169]

- Fix XML regex bugs and improve speed of token check. [#20439]

#### astropy.visualization

- Fixed a number of bugs in WCSAxes:
  * Setting the number of ticks to zero no longer crashes drawing, minor ticks, or the mouseover coordinate display.
  * Contour-type grids no longer crash for a longitude coordinate with fewer than two ticks or for a coordinate sliced out of the plot, and no longer draw a spurious gridline along the longitude wrap for a single tick.
  * Drawing a gridline sampled with fewer than three points no longer crashes.
  * Transforming empty coordinate arrays no longer crashes for 1-d WCS and now returns correctly shaped arrays.
  * Simplifying tick labels no longer crashes when one label is a prefix of an adjacent one.
  * Tick values for longitude coordinates in non-degree units are no longer corrupted when a tick intersects a spine more than once.
  * ``%``-style tick formats now use the format unit instead of the coordinate's native unit.
  * Invalid tick format strings now raise a ``ValueError`` instead of being silently accepted with reduced precision.
  * ``get_coords_overlay`` no longer ignores a supplied ``coord_meta`` when passed a WCS.
  * The default conversion of right ascension format units to hourangle no longer depends on unit object identity.
  * ``custom_ucd_coord_meta_mapping`` no longer applies earlier keys when a later key conflicts, and now raises for keys specified more than once.
  * The cursor coordinate display no longer breaks after ``reset_wcs`` and now preserves the pixel display mode.
  * Automatically-placed coordinates are now hidden instead of crashing when no spine assignment is consistent with fixed tick positions.
  * Formatting a coordinate for the mouseover display no longer crashes for a degenerate (zero-size) coordinate range. [#20221]

- Fixed a bug which caused WCSAxes to fail when having to transform coordinate frames in the case where APE 14 WCS implementations used frame names or non-instantiated classes in ``world_axis_object_classes`` (which is valid). [#20480]

- Fixed ``WCSAxes.get_transform`` dropping the unit conversion when given a coordinate frame that matches the frame of the axes' WCS. [#20600]

#### astropy.wcs

- Fixed a bug that could cause a segmentation fault when using a WCS object with ``preserve_units=True`` and where units has already been defined and the WCS had been ``set()`` but the scaling factors were found to be 1, and when cdelt or crval were subsequently set. [#20418]

- Fix ``WCS.to_header()`` for cases where ``preserve_units=True``, units were set programmatically, and ``WCS.set()`` was not called. [#20422]

- Fixed a race condition in which concurrent failing transforms on the same ``WCS`` object could allocate the internal error buffer twice, leaking one allocation. The buffer is now allocated once when the object is created. [#20423]

- Fixed a race condition in which deepcopying a ``WCS`` object while another thread used it could raise ``RuntimeError: dictionary changed size during iteration``. [#20425]

- Fixed slicing of WCS objects with negative values, which were previously used as literal pixel offsets rather than being interpreted relative to the end of the axis as for Numpy arrays. Negative values are now resolved when the shape of the data is known, and a negative integer or slice start now raises a ``ValueError`` when it is not. Also fixed nested ``SlicedLowLevelWCS`` objects rejecting slices with an explicit step of 1. [#20544]

- Fix bug in ``astropy.wcs.utils.fit_wcs_from_points`` so the ``proj_point`` will be transformed to the ``world_coords`` coordinate frame. [#20588]
```

HSSI held v8.0.1 (release date 2026-07-04, Version PID https://doi.org/10.5281/zenodo.21262391) until
the v8.0.2 release update, and v7.2.0 (release date 2025-11-25, Version PID
https://doi.org/10.5281/zenodo.17756022) before the 2026-08-26 refresh replaced it; each was
superseded by a newer release (rule 3). The number keeps the leading `v` the stored values used; the
tag writes `v8.0.2` and PyPI writes `8.0.2`. HSSI's view renders a stored number as
`Astropy - <number>`; that rendering is not the stored number and must not be written back.

**Why v8.0.2** (rule 3; release evidence read on 2026-10-29, with `main` at
`d3ad3b66f24bda0f3e5efadda4a5d78fea0714c2`).

- **Releases are cut on release branches.** No final release tagged after `v0.4` (2014-07-16) is
  an ancestor of `main`; only the final releases `v0.1`, `v0.2` and `v0.4` are. The annotated tag
  `v8.0.2` ("Tagging v8.0.2", 2026-10-15 21:55:02 +0100) names
  `2268dbf1155e8ad10161c188afc60af3d35b3c8b`, "Finalizing changelog for v8.0.2 (#20614)", on the
  release branch `v8.0.x`. That branch shares `main`'s history up to
  `de3f7ecde9ac78393fa3ccfbbe6cee2ae6998fa0` (2026-05-05), the merge base of `main` with `v8.0.0`,
  `v8.0.1` and `v8.0.2` alike, and `v8.0.0` and `v8.0.1` are both ancestors of `v8.0.2`.
- **PyPI.** `info.version` is `8.0.2`. Its eight wheels and its sdist were uploaded between
  2026-10-15T21:44:23Z and 21:44:45Z; none is yanked, and `project_urls` names this repository.
- **v7.2.3 does not supersede it.** Tagged and uploaded the same evening (tag 2026-10-15 21:54:21
  +0100, PyPI 21:42:22Z), v7.2.3 is a maintenance release of the 7.2 series, which 8.0 replaced; a
  backport never supersedes the current series, whatever order the creation dates give.
- **Not releases.** `v8.1.0.dev` is a development marker on `main`, and `v8.0.0b1`, `v8.0.0rc1` and
  `v8.0.0rc2` are pre-releases (rule 2). No later tag, PyPI upload or GitHub release existed on
  2026-10-29.

**Version Date** (rules 7–8). No GitHub Release object existed for `v8.0.2` on 2026-10-29 (the
releases API had none for the tag), and the newest Release object was v8.0.1's. The date is therefore the
annotated tag's UTC day, 2026-10-15 (20:55:02Z). The tagged commit (2026-10-15T15:10:17Z), the PyPI
upload and the changelog heading "Version 8.0.2 (2026-10-15)" fall on the same day. Astropy's dates
have not always agreed this well: v7.2.2 and v8.0.1 carry the changelog heading 2026-07-03, their
annotated tags and PyPI uploads are dated 2026-07-05 (UTC), and their GitHub Releases and Zenodo
deposits 2026-07-08. If a GitHub Release is published for v8.0.2 later, a refresh applies rule 7 to
it.

**Version Description** (rules 10, 13–16). With no GitHub Release there is no release name or body,
so the text comes from the changelog section for the tag: `CHANGES.rst` at `v8.0.2`, from
"Version 8.0.2 (2026-10-15)" to the next heading, "Version 8.0.1 (2026-07-03)". The section is
identical on `main` at `d3ad3b66`. It is kept verbatim under the changelog's own headings: the RST
section and subpackage underlines are written as markdown `###` and `####` headings, each item's hard
line wraps are joined, and the RST double-backtick literals and the trailing pull-request numbers are
left as written. Kept: the API change to index checking when slicing a `SlicedLowLevelWCS` (#20544)
and every Bug Fixes item, in thirteen subpackage groups, including the WCSAxes item with its fourteen
sub-items; each is a changed API or a bug a user could hit (rule 14). Dropped whole: the one "Other
Changes and Additions" item, "Fixed an incorrect build-time definition for ``NPY_TARGET_VERSION`` .
[#20481]", a build chore, and with it that section's heading. Every kept item and heading matches the
source once whitespace is normalised. The v8.0.1 description this replaces was a summary composed from
that release's changelog rather than its items, a form rule 15 does not allow; nothing of it carries
onto v8.0.2 (rule 10).

**Version PID** (rules 17–18). Not found: no deposit exists for v8.0.2. On 2026-10-29 the Zenodo
versions of the concept 10.5281/zenodo.4670728 numbered 42, the newest `v8.0.1`
(10.5281/zenodo.21262391, published 2026-07-08), and DataCite's concept record listed the same 42
under `HasVersion` and presented `version` `v8.0.1`. Astropy's deposits are made by Zenodo's GitHub
integration (the v8.0.1 deposit carries `IsSupplementTo https://github.com/astropy/astropy/tree/v8.0.1`),
which deposits a release when its GitHub Release is published, and v8.0.2 has none. The PID is
therefore cleared rather than carried over; the v8.0.1 DOI must not be used for v8.0.2.

*Superseded observation.* The 2026-08-26 record found no `HasVersion` relations on DataCite's concept
record and took the version DOI from the Zenodo API instead. DataCite's record, updated 2026-09-15, now
lists all 42 versions, so either route serves.

*`CITATION.cff` cannot arbitrate any of this:* it has no top-level `version` or `date-released` key.
Its complete top-level key set is `cff-version`, `message`, `title`, `authors`, `repository-code`,
`url`, `license`, `identifiers`, `preferred-citation` and `references`, and the file is byte-identical
at the Source Revision and at `v8.0.2`.

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

### 14. Reference Publication (OPTIONAL)
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
- astropy
- python

The first fifteen are the entries of `pyproject.toml`'s `keywords` array, in the order the project
lists them; the array is unchanged at the `v8.0.2` tag. The last two are the repository's GitHub
topics that the array lacks: the topics read on 2026-10-29 are `astronomy`, `astrophysics`, `astropy`,
`python` and `science`, and the other three are already in the array. Topics are project-declared, so
fields/16 rule 9 includes them unless rules 2–4 exclude them, and none does; rule 7's exclusion of a
catalogue-wide generic such as `python` applies only to terms an extractor proposes. The 2026-08-26
record listed the array alone and did not weigh the topics. Both terms bind existing lower-case rows.
`Keyword` is the one open vocabulary in HSSI — missing rows are created on submission — so no value
here needs to pre-exist.

Nothing else is added: the project's own keywords and topics are authoritative for this field, and
(per Field 7) there is no PyHC keyword set to reconcile against. Astropy is in no PyHC registry, so the
`pyhc package` marker (rule 15) does not apply.

*Weighed and not added:* the four `keywords` under `CITATION.cff`'s `preferred-citation`
(`Astronomy software`, `Open source software`, `Astronomy data analysis` and
`Astrophysics - Instrumentation and Methods for Astrophysics`). They describe the 2022 paper
(Field 14), not the software, and the file has no top-level `keywords` key.

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

The published release matches. PyPI's 8.0.2 files, uploaded 2026-10-15, are abi3 wheels for macOS
(`macosx_10_9_x86_64`, `macosx_11_0_arm64`), Linux (manylinux `x86_64` and `aarch64`, musllinux
`x86_64`) and Windows (`win32`, `win_amd64`, `win_arm64`), the same set as 8.0.1, and the cibuildwheel
targets and CI runners described above are the same at the `v8.0.2` tag.

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

PyPI's 8.0.2 wheels confirm the three rows: `x86_64` for macOS, Linux and Windows (`win_amd64`) →
`x86-64`; `macosx_11_0_arm64` → `Apple Silicon arm64`; manylinux `aarch64` → `Linux aarch64 or arm64`.
Two further Windows wheels, `win32` (32-bit x86) and `win_arm64`, map to no row of their own. `Other`
is not selected for them: fields/21 rule 8 admits it without requiring it, and it would tell a
searcher nothing that the three rows and Field 20's `Windows` do not.

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

Rule 6, recency for software with stable releases. The anchors, read on 2026-10-29: the last commit
on the default branch `main` is `d3ad3b66f24bda0f3e5efadda4a5d78fea0714c2` (2026-10-29T16:38:43Z),
and the latest release is v8.0.2 of 2026-10-15 (Field 12), with v7.2.3, a 7.2-series maintenance
release, the same day. The repository is not archived. The README carries no repostatus.org badge or
status statement — its status line shows CI, coverage and documentation badges — and displays a
pyOpenSci peer-reviewed badge linking to https://github.com/pyOpenSci/software-review/issues/251. The
next minor version is in development on `main`, whose nearest tag is `v8.1.0.dev`.

The status is unchanged from earlier records, which rested it on v7.2.0 (2025-11-25) and, at
2026-08-26, on v8.0.1 (2026-07-04).

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
- https://doi.org/10.1051/0004-6361/201322068 — "Astropy: A community Python package for astronomy",
  Astropy Collaboration et al. 2013, A&A 558, A33 (arXiv:1307.6212)
- https://ui.adsabs.harvard.edu/abs/2013ASPC..475..241T/abstract — "The Astropy Project: A Community
  Python Library for Astrophysics", Tollerud, Greenfield, Robitaille & Astropy Developers 2013,
  Astronomical Data Analysis Software and Systems XXII, ASP Conference Series 475, 241 (no DOI)
- https://ui.adsabs.harvard.edu/abs/2014ASPC..485..343B/abstract — "Astropy: Building Blocks for
  Astronomy Software", Bray 2014, Astronomical Data Analysis Software and Systems XXIII, ASP
  Conference Series 485, 343 (no DOI)
- https://doi.org/10.48550/arXiv.1610.03159 — "The Astropy Problem", Muna et al. 2016,
  arXiv:1610.03159
- https://doi.org/10.3847/1538-3881/aabc4f — "The Astropy Project: Building an Open-science Project
  and Status of the v2.0 Core Package", Astropy Collaboration et al. 2018, AJ 156, 123
  (arXiv:1801.02634)
- https://doi.org/10.17226/25217_24 — "Towards Reproducibility Using Open Development: Astropy as a
  Case Study", Tollerud 2018, a white paper to the National Academies study *Open Source Software
  Policy Options for NASA Earth and Space Sciences*
- https://ui.adsabs.harvard.edu/abs/2020ASPC..522..491T/abstract — "Community-oriented Programming in
  Astronomy: Astropy as a Case Study", Tollerud 2020, Astronomical Data Analysis Software and Systems
  XXVII, ASP Conference Series 522, 491 (no DOI)
- https://doi.org/10.1088/2514-3433/acfa9ach8 — "Astropy and Associated Packages", Pasha 2024,
  chapter 8 (pp. 8-1 to 8-29) of the book *Astronomical Python*
- https://doi.org/10.26624/ZWFX2927 — "Planetary World Coordinate System in Astropy", Marmo & Erard,
  Astronomical Data Analysis Software and Systems XXXIII, ASP Conference Series 541, 320 (ADS
  `2025ASPC..541..320M`; arXiv:2504.03820)

**Why each listed entry is here.**

- **The 2013 and 2018 Astropy Collaboration papers** are the project's own papers about the package
  (rule 3) and two of the three papers `astropy/CITATION` asks every user to cite (rule 4): "We
  encourage you to cite all three papers, but if space is limited, please cite the most recent
  paper." The third, the 2022 paper, is Field 14 and is not repeated here (rule 2).
- **Six more publications about Astropy by its developers** (rule 3; the first author of each is
  credited in `docs/credits.rst` at `v8.0.2`). That file lists the project's contributors, and the
  project designates no individual software authors (Field 6), so this record reads rule 3's "its
  authors include the software's" as credited contributors. Tollerud, Greenfield & Robitaille 2013
  and Bray 2014 are ADASS overviews of the core package, the affiliated packages and how the project
  is run. "The Astropy Problem" (Muna et al. 2016) sets out the project's lack of funding and what
  sustaining the software would take; among its 154 authors are Demitri Muna, Perry Greenfield and
  Adrian Price-Whelan. Tollerud 2018 is a four-page white paper, with David W. Hogg as contributing
  author, on open development as the route to reproducible science, with Astropy as the case; its
  DOI resolves to the study's page, which links it among the submitted white papers as
  `24_Tollerud_WhitePaper.pdf`. Tollerud 2020 describes Astropy's community-developed model. Marmo &
  Erard describe the planetary WCS support Chiara Marmo implemented in Astropy 6.0 (Field 4); the
  paper's arXiv preprint, `10.48550/arXiv.2504.03820`, has the same title and an identical abstract
  and is not listed separately.
- **Pasha 2024, "Astropy and Associated Packages"**, is listed on its merit by the user's decision of
  2026-10-29: an outside publication whose subject is Astropy and which introduces the package to its
  users. No rule in fields/27 covers an outside publication whose subject is the software, so the user
  decided it.

**Search record.** Literature searched on 2026-10-29 across all years; no earlier search had been
recorded here, and the next refresh searches from this date.

- ADS/SciX (anonymous API): `author:"Astropy Collaboration"` (12 records: the three Astropy papers,
  seven Zenodo deposits of Astropy releases, and two transient-classification circulars that list the
  collaboration in error); `title:"astropy"` excluding meeting abstracts, software and circulars (24
  records, all read); and title and abstract sweeps for the `astropy.<subpackage>` names.
- Crossref `query.title=astropy` (14 results, all read), which found the two SciPy proceedings papers,
  the National Academies white paper and the book chapter that the ADS title search did not return.
- DataCite, for Astropy-titled deposits (the Proposals for Enhancement below).
- Controls: a nonsense token returned 0 on ADS, Crossref and DataCite, and `author:"SunPy Community"`
  returned that project's two papers on ADS.

The ADS author search finds no Astropy Collaboration paper later than the 2022 one (Field 14).

**Rule 4 — method and model papers.** Beyond the three papers it asks every user to cite, Astropy cites
method and model papers routine by routine: at `v8.0.2` its non-test modules hold 91 docstring
"References" sections across 39 files (counting lines that read only `References` in the `.py` files
under `astropy/`, outside `tests/` directories). The Lomb–Scargle and box-least-squares periodograms, Bayesian blocks, the FLRW
cosmologies and the physical models in `astropy.modeling` each have such a section. Judged as a list
from a searcher's view, each is incidental to the library as a whole and together they would bury the
publications about it, so none is listed; the three papers `astropy/CITATION` asks every user to cite
are the exception rule 4 keeps. A search of the package source and documentation at `v8.0.2` for
requests to cite ("please cite", "should cite", "if you use … cite") finds none for a component's
paper: the only hit outside `astropy/CITATION`, in `docs/development/testguide.rst`, asks contributors
who find Hypothesis, a testing tool, useful in their research to cite its paper
(`10.21105/joss.01891`).

**Rule 5 — outside publications that use Astropy add nothing.** fields/27 rule 5 names Astropy as its
example of software so widely used that a list of its users tells a searcher nothing, so none is
added, whoever wrote it. Weighed on that ground:

- `10.1117/12.2231313` — Jenness et al. 2016, "Investigating interoperability of the LSST data
  management software stack with Astropy", SPIE 9913: the LSST data-management team's comparison of
  its pipeline software with Astropy, and of building on it.
- `10.1016/j.jqsrt.2018.03.019` — Schreier 2018, "Comments on the Voigt function implementation in the
  Astropy and SpectraPlot.com packages", JQSRT 213, 13: an assessment of the sum-of-Lorentzians
  algorithm (McLean et al. 1994) that `Voigt1D` then used. Astropy switched `Voigt1D` to Humlicek's
  approximation in 4.0.5 (#11177).
- `10.25080/majora-4af1f417-006` — Shupe et al. 2018, "Practical Applications of Astropy", SciPy
  proceedings.
- `10.25080/majora-7b98e3ed-012` — Craig 2015, "Widgets and Astropy: Accomplishing Productive Research
  with Undergraduates", SciPy proceedings.
- `2016pyas.confE...5C` — Craig 2016, "Variable Star Research with Undergraduates Using Astropy", a
  Python in Astronomy 2016 talk.
- `2016pyas.confE..18T` — Turner 2016, "Streamlining an IRAF data reduction process Pythonically with
  Astropy and NDMapper", a Python in Astronomy 2016 talk.
- `2023LPICo2991.7093T` — Tinsman et al. 2023, "Using Jinja2 and Astropy Python Packages to Generate
  PDS4 XML Labels for FITS Files".

**Weighed and not listed, by the user's decision of 2026-10-29.**

- `10.5281/zenodo.56799` — Sipőcz, Robitaille & Tollerud, "The Astropy Project: A Community Python
  Library for Astronomy", Python in Astronomy 2016 (ADS `2016pyas.confE...2S`): a 16-slide deck of
  headings, bullets and images (a project overview, the release and long-term-support policy, the v1.1
  features and the affiliated-package programme; one slide is a link to a video). The user judged that
  it does not stand alone without the talk (fields/27, *Eligible publication types*).
- `APE 0`–`APE 23` — the Astropy Proposals for Enhancement deposited at Zenodo as technical notes: 22
  proposals under 56 DOIs (no deposit was found for APE 11 or APE 16), among them APE 0, the governance
  charter; APE 6, the ECSV format; APE 8, the code of conduct; and APE 14 (`10.5281/zenodo.1188874`),
  the shared Python WCS interface that Field 30 cites for gwcs. Not listed: they are the project's
  internal governance, process and design proposals, not publications for a visitor, and 22 entries
  would bury the papers.
- `10.1145/3757462` — Sun et al. 2025, "Collaboration Challenges and Opportunities in Developing
  Scientific Open-Source Software Ecosystem: A Case Study on Astropy", Proceedings of the ACM on
  Human-Computer Interaction. An arXiv preprint by the same authors on the same case study, "How to
  Sustain a Scientific Open-Source Software Ecosystem: Learning from the Astropy Project"
  (`10.48550/arXiv.2402.15081`), is weighed with it.
- `10.1109/CHASE66643.2025.00027` — Sun et al. 2025, CHASE 2025, titled "Advancing Sustainable
  Communities in Scientific Oss: a Replication Study With Astropy" in its DOI record (the paper itself
  was closed access as of 2026-10-29, and its own styling of the title was not read). Neither
  Sun et al. study is listed: they study how the project is run, which serves researchers more than
  someone looking for software.

**Weighed and not added — not about Astropy itself, or not a publication.**

- `2019ASPC..523..237D` — Donaldson 2019, "Astropy and the Virtual Observatory", Astronomical Data
  Analysis Software and Systems XXVII: what the IVOA standards process and the Astropy Project might
  learn from each other. Its subject is the relation between the two projects rather than Astropy
  (rule 3 needs this software as the subject).
- `10.5281/zenodo.8416186` — Lewis 2023, "PySPEDAS, Astropy, and Coordinate Transformations", DASH
  2023: why PySPEDAS ported its own coordinate transforms rather than adopt Astropy; it is about
  PySPEDAS (rule 6).
- `10.3847/1538-4357/ace0bd` (NDCube, Ryan et al. 2023), `10.1117/12.3021056` (specreduce, Pickering
  et al. 2024), `2013hell.confQ..31L` (imagecube, Lianou et al. 2013) and `10.5281/zenodo.48182`
  (pyspeckit, Ginsburg 2016): publications about other packages built on Astropy.
- `2022nova.pres.9976C` — an AAS Nova press release on the 2022 paper: not a publication type
  (rule 1).
- `2024zndo..11121433A` and six other ADS `zndo` records — Zenodo deposits of Astropy releases: software
  (Fields 2 and 12), not publications (rule 1).

**The `CITATION.cff` `references` block contains exactly the 2013 and 2018 papers and no others.** The
block runs from its `references:` key to the end of the file, and holds two reference items: the 2018
paper (with DOI 10.3847/1538-3881/aabc4f, arXiv DOI 10.48550/arXiv.1801.02634, ADS bibcode
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
  to track it. The single API change in v8.0.1 was about when astropy falls back from this bundled
  table to a network download.
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
