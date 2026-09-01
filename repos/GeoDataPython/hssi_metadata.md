# HSSI Metadata Extraction Results

**HSSI Software ID:** e8b6fe34-d598-4d53-86d0-288bc004c3e7
**Repository:** https://github.com/jswoboda/GeoDataPython
**Source Revision:** c3e29541327ec754eb5a2a9e8dd94bf1abee3328
**Extraction Date:** 2026-08-05
**Validation Date:** 2026-08-06
**Validation Status:** PASS

**Scope note.** This software has been inactive since 2018-04-20; the pinned revision above is the
tip of `master` and is the newest state that exists. Because there is no newer code, no newer
release, and no packaged distribution, several fields are settled by *absence* of evidence rather
than by newer evidence, and the reasoning for each absence is recorded with the field so a later
refresh does not re-litigate it. A second consequence matters when reading the capability fields:
the code was written against Python 2.7/3.6-era libraries and several documented capabilities now
fail against current dependency versions (noted per field). The capability fields record what the
software is designed and documented to support; the caveats record where that support has rotted.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Note:* The existing HSSI record was created by a third-party curator rather than by a project
maintainer. That fact is recorded here only because it bears on Field 7: the stored software name is
an unedited machine-generated string, so the usual presumption that a submitted value reflects a
maintainer's deliberate wording does not hold for this record.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.154533

**Source and reasoning.** This is the DOI of the deposited `v0.1` release, from the Zenodo record
(`https://zenodo.org/api/records/154533`) and its DataCite registration
(`https://api.datacite.org/dois/10.5281/zenodo.154533`). It is also carried in a README badge at
`README.rst` lines 7-8 (`.. image:: https://zenodo.org/badge/DOI/10.5281/zenodo.154533.svg` with
`:target: https://doi.org/10.5281/zenodo.154533`).

**There is no concept (all-versions) DOI, and one must not be constructed.** The Zenodo record's
`conceptdoi` field is an empty string. Its `conceptrecid` is `595964`, but Zenodo never minted an
all-versions DOI for this legacy 2016 deposit: `10.5281/zenodo.595964` is not registered with
DataCite. A future agent must not synthesise a concept DOI from the `conceptrecid`.

**Why the same DOI legitimately appears in both Field 2 and Field 12's Version PID.** Field 2 asks
for the software's globally unique persistent identifier and offers the concept DOI only as an
example ("e.g., the concept DOI for all versions"). Exactly one version of this software was ever
deposited, so the version DOI is simultaneously the identifier for the software as a whole. Leaving
Field 2 empty would strip the record of its only persistent identifier; duplicating it is the
accurate representation of a single-version deposit.

### 3. Code Repository (MANDATORY)
https://github.com/jswoboda/GeoDataPython

**Source.** The repository's own remote; the GitHub API reports `full_name: jswoboda/GeoDataPython`,
`fork: false`, `archived: false`, `default_branch: master`. The URL is live and unmoved, and matches
the `code:` field of the Python in Heliophysics Community (PyHC) registry entry for this package.
The Zenodo deposit's related identifier points at `.../GeoDataPython/tree/v0.1` (relation
`isSupplementTo`), i.e. the same repository at the release tag.

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: 3D Graphics
- Data Visualization: Line Plots

The three top-level categories previously stored (`Coordinate Transforms`, `Data Processing and Analysis`,
`Data Visualization`) are all retained; the twelve subcategories are added, and every subcategory's
parent is present.

**Evidence for each value.**

- **Coordinate Transforms** — `GeoData/CoordTransforms.py` is a public module of transform functions:
  `sphereical2Cartisian` / `cartisian2Sphereical` (radar range-azimuth-elevation to local Cartesian),
  `wgs2ecef` / `ecef2wgs` (geodetic WGS84 to Earth-centred Earth-fixed, implementing Vermeille 2002),
  `ecef2enul` / `enu2ecefl` / `ecef2enu4vec` / `enu2ecef4vec` (ECEF to east-north-up about a sensor
  origin), `enu2cartisian` / `cartisian2enu`, and the pointing helpers `angles2xy`, `xy2angles`,
  `angles2xyz`, `xyz2angles`. This is user-facing rather than internal: `GeoData.interpolate(...,
  newcoordname=...)` and `GeoData.__changecoords__` expose the transforms as the mechanism for
  regridding a data set into another system, and `README.rst` documents the six supported
  `coordnames` values (`wgs84`, `Spherical`, `Spherical2`, `ENU`, `ECEF`, `Cartesian`).
- **No Coordinate Transforms subcategory is selected, deliberately.** The six available children are
  `Heliospheric`, `Ionospheric`, `Magnetospheric`, `Mission-Specific`, `Planetary` and `Solar`. Every
  transform in `CoordTransforms.py` is geodetic or geometric (WGS84/ECEF/ENU/spherical/Cartesian);
  the package implements no magnetic or apex coordinate system (no AACGM, magnetic local time,
  corrected geomagnetic latitude, or magnetic apex conversion) and nothing solar, heliospheric,
  planetary, or spacecraft-frame. `Ionospheric` is the value most likely to be mistakenly added
  because the software's science domain is the ionosphere, but that subcategory denotes *ionospheric
  coordinate systems*, which this package does not provide. Note in passing that the shipped
  Sondrestrom Madrigal file does contain `cgm_lat` / `cgm_long` columns, but no reader in
  `utilityfuncs.py` uses them, so they do not create a magnetic-coordinate capability.
- **Data Processing and Analysis** — parent of the six selected children below.
- **2D Slices** — extraction of a plane from a 3-D volume is computed, not merely drawn:
  `GeoData/plotting.py` `slice2DGD` and `contourGD` build a target plane at a requested index and
  either reshape the volume onto it or call `datareducelocation`; `_dointerp` (used by
  `alt_slice_overlay` / `alt_contour_overlay`) builds a constant-altitude `new_coords` grid and calls
  `GeoData.interpolate` onto it; `plot3Dslicempl` and `plottingmayavi.plot3Dslice` cut x, y and z
  slices out of the reshaped volume.
- **Analysis** — derived scientific quantities are computed: `GeoData.changedata(dataname, newname,
  func, params)` applies a user function and renames the result (the documented example, in
  `Test/load_isropt.py`, converts Madrigal log electron density `nel` to linear `ne`);
  `utilityfuncs.readIono` computes a density-weighted composite ion temperature from per-species
  `Ti_*` / `Ni_*` arrays and falls back to `iono.getDoppler()` for line-of-sight velocity;
  `GeoData.timeregister` computes the overlap between two instruments' measurement intervals.
- **Data Access and Retrieval** — `GeoData/filescraping.py` is a module of remote-data download
  functions: `datedwebsite(baseurl, daterange, basedir)` walks a `Year/date/file.fits` web directory
  and retrieves the files whose timestamps fall in a requested range, `searchsite(date1, date2, url)`
  returns the matching URLs, and `download(urls, dldir)` fetches them. `setup.py` declares the
  matching optional dependency group `extras_require={'io': ['beautifulsoup4']}`. Caveats worth
  recording rather than removing the value: the module also imports `requests`, which is declared
  nowhere in `setup.py`, and `filescraping.py` line 102 is a Python 2 `print` statement, so the module
  cannot be imported at all under Python 3.
- **Data Reduction** — `GeoData.timereduce(timebounds)` drops samples outside a time window,
  `timeslice(timelist, listtype)` returns a copy holding only selected times, and
  `datareducelocation(newcoords, coordname, key)` reduces the data set to a chosen set of measurement
  locations. `README.rst` advertises this: "The size of the data set can be reduced by applying
  methods to filter out specfic time and data points."
- **File Format Conversion** — the package's stated purpose is to bring heterogeneous instrument
  formats into one representation and back out to a single structured format: the readers in
  `utilityfuncs.py` ingest Madrigal HDF5, SRI HDF5, OMTI HDF5, all-sky FITS, Neo sCMOS HDF5 and ASCII
  ionofiles, while `GeoData.write_h5(filename)` writes the class's own structured HDF5 and
  `GeoData.read_h5(filename)` (via `read_h5_main`) reads it back. Reading one format and writing
  another is the definition of this subcategory.
- **Image Processing** — optical camera frames are geometrically reprojected and co-registered, not
  just displayed. `readAllskyFITS` reads azimuth/elevation map files, rejects bad pixels by
  thresholding the gradient of the azimuth map (`np.gradient(az)`, `np.hypot(Fx,Fy) > 15.`), rotates
  frames with `np.rot90`, and projects each surviving pixel to a range at an assumed emission
  altitude via `heightkm/sin(el)`; `readNeoCMOS` applies per-file transpose / rotate / flip
  plate-scale parameters to both the image stack and its az/el maps; `_dointerp` interpolates an
  optical image and a radar volume onto one common grid so they can be overlaid, which is image
  co-registration; `plotting.plotazelscale` overlays az/el contours on a frame as a diagnostic.
  Rejected weaker rationale, recorded so it is not reused: the mere presence of 2-D arrays or of
  `imshow` calls would not justify this value.
- **Processing** — the general pipeline the README documents: read into the class, `changedata`,
  `interpolate` to a new coordinate system or regrid within one, reduce in time and location,
  time-register against a second instance, then plot.
- **Time Series Analysis** — measurements are time-ordered `Ntx2` start/end arrays and the package
  provides temporal machinery over them: `timerepair` reconstructs missing end times from the mean
  sample spacing, the constructor sorts data by time, `time2ind` maps POSIX times to indices,
  `timereduce` / `timeslice` filter temporally, `add_times` concatenates two instances along time,
  and `timeregister` aligns two instruments' time bases. The subcategory definition includes temporal
  filtering, which is exactly what these provide.
- **Data Visualization** — parent of the four selected children below.
- **2D Graphics** — `plotting.py` `slice2DGD` (`pcolor`), `contourGD` (`contour`), `scatterGD`
  (`scatter`), `quiverGD` (`quiver`), `rangevstime` (`pcolormesh` of slant range against UT),
  `alt_slice_overlay` / `alt_contour_overlay` (greyscale optical `imshow` with a transparent or
  contoured radar parameter on top), `sliceGDsphere` (`tripcolor`), and the polar beam-position plots
  `plotbeamposGD` / `polarplot`.
- **2D Slices** — the display half of the slice capability: `slice2DGD`, `contourGD` and the two
  altitude-overlay functions render a constant-altitude or constant-index cut of a 3-D volume.
- **3D Graphics** — `plotting.plot3Dslicempl` uses `mpl_toolkits.mplot3d` and `ax.plot_surface` with
  per-facet RGBA colouring and NaN transparency, and `plottingmayavi.plot3Dslice` renders the same
  slices with Mayavi `mlab.mesh` plus `mlab.axes` / `mlab.colorbar` / `mlab.screenshot`. This value
  does not rest on the optional `mayavi` dependency: the tip-of-master commit is titled "Added 3d
  plotting in matplotlib and moved mayavi to seperate file", and `plot3Dslicempl` needs only
  matplotlib. `plottingmayavi` degrades gracefully, setting `mlab = None` and returning early when
  Mayavi is absent.
- **Line Plots** — `plotting.rangevsparam` draws 1-D profiles of a fitted parameter against slant
  range with `ax.plot`, optionally with `ax.errorbar` from a companion error key; exercised in
  `Examples/MadrigalExample1.ipynb`.

**Considered and rejected, with reasons** (recorded so these are not re-proposed):

- `Data Visualization: Movies` — frame-by-frame playback loops (`hi.set_data(im); draw(); pause(0.1)`)
  exist only in `Test/RTI_2007-03-23.py` and `Test/rangevtime_mishap.py`. No animation or movie-export
  capability exists in the `GeoData` package itself (no `matplotlib.animation`, no writer), and a
  demonstration script is not evidence of a supported feature.
- `Data Processing and Analysis: Spectrogram` and `Data Visualization: Spectrogram` — `rangevstime`
  produces a range-time-intensity display. There is no frequency axis anywhere in the package and no
  FFT, STFT or wavelet transform, so neither spectrogram value applies.
- `Data Processing and Analysis: Calibration` — the readers *consume* instrument calibration
  products (`readAllskyFITS` and `readNeoCMOS` both require an az/el map file, and the documented
  example file is named `calMishap2011Mar.h5`), and `readNeoCMOS` applies stored transpose/rotate/flip
  orientation flags. The package does not derive, produce, or expose calibration as a capability, so
  applying a supplied pointing calibration during ingest was judged insufficient. The evidence is
  recorded so that a later re-assessment can weigh it without rediscovering it.
- `Models and Simulations` and all its children — the package models nothing. The temptation comes
  from the release name "ISR Sim Paper" and from `utilityfuncs.readIono`, but `readIono` *ingests* an
  external simulator's output object; it does not simulate.
- `Mission-related` and all its children — this is a general-purpose analysis package, not part of
  any mission's ground system or data pipeline.
- `Servers and Environments` and all its children — no server, container, HPC, or deployment
  component; the repository contains no Dockerfile, MPI use, or job scripts.
- `Data Processing and Analysis: ML/AI`, `Curlometer`, `Plasma Moments`, `Energy Spectra`,
  `Pitch Angle Distributions`, `3D Particle Distribution Processing`, `Wave Polarization Analysis`,
  `Wavelet Analysis`, `Linear Gradient Estimation`, `Magnetic Null Finding`, `Field-line Tracing`,
  `Data Assimilation`, `Packet Decommutation` — no corresponding code exists. `Data Assimilation` is
  worth naming explicitly, because one reader does ingest simulator output (Field 30): the package
  co-registers data sets with one another and implements no assimilation machinery — no state
  estimator, no analysis step, no observation operator — so bringing a model run in as one more data
  set does not make this an assimilation tool.

### 5. Related Region (MANDATORY)
- Earth Atmosphere
- Earth Auroral Subregion
- Earth Ionosphere
- Earth Thermosphere

The `Region` vocabulary is flat, so these are four peer values with no parent/child relationship
between them — which is why `Earth Atmosphere` below is not a redundant parent of the others.

**Evidence for the three added values.**

- **Earth Ionosphere** — the primary region, and the one previously missing. The parameters the
  readers extract are ionospheric plasma parameters: `readSRI_h5` maps `Ne`, `dNe`, `Vi`, `dVi`, `Ti`,
  `dTi`, `Te` to SRI HDF5 paths under `/FittedParams`; `readMad_hdf5` pulls Madrigal parameters such
  as `nel`, `ti`, `te`, `vo`; the shipped Sondrestrom file carries `nel`, `ti`, `te`, `vo`, `po+` and
  `col`; `readIonofiles` and `readMahalih5` read line-of-sight and vertical total electron content
  with 350 km ionospheric pierce points. The example altitudes (100-500 km slices, 300 km and 140 km
  cuts) are E- and F-region.
- **Earth Thermosphere** — the optical instrument the package is built around is the Optical
  Mesosphere Thermosphere Imagers airglow imager (`utilityfuncs.readOMTI`, `Test/data/OMTIdata.h5`),
  and the emission altitudes used in the examples (140 km) together with the 100-500 km ISR slices lie
  in the thermosphere.
- **Earth Auroral Subregion** — every data set the project ships, documents, or exercises is a
  high-latitude auroral-zone observation: the shipped Madrigal files are from Resolute Bay
  (74.73 deg N) and Sondrestrom (67 deg N); `readAllskyFITS` is documented against the Poker Flat
  (65 deg N) all-sky camera archive; `Test/RTI_2007-03-23.py` and `Test/rangevtime_mishap.py` describe
  themselves as "range vs. time plots of key ISR and optical video during March 2011 events" and load
  Poker Flat ISR plus a Neo sCMOS auroral camera; `Test/subplots_mishap.py` is titled "March 2011
  example at PFISR with Neo sCMOS camera".

**Earth Atmosphere** is retained from the previously stored pair. It is a true statement — the
ionosphere and thermosphere are part of Earth's atmosphere — and because the vocabulary is flat it is
a peer value rather than a redundant parent, so dropping it would only remove a search path. The more
specific values added above, which the field guidance prefers, now sit alongside it.

**`Earth Magnetosphere` was stored previously and has been removed.** The repository supports it only
indirectly: the package reads no magnetospheric measurement, implements no magnetic field model,
performs no field-line mapping, and provides no magnetic coordinate system — the shipped Sondrestrom
Madrigal file does carry `cgm_lat` and `cgm_long` columns, but no reader touches them (see Field 4).
The genuine connection is that auroral ionospheric observations are the footprint of
magnetosphere-ionosphere coupling, and that connection is carried more precisely by
`Earth Auroral Subregion`. Keeping the broader value would have made this record a false hit for
magnetosphere searches while adding nothing the auroral value does not already say.

The contrast with `Earth Atmosphere`, which was kept, is the *kind* of relation involved, and a future
agent needs it to see why the two were treated differently. `Earth Atmosphere` is true by containment:
the ionosphere and thermosphere the software works in are regions of Earth's atmosphere.
`Earth Magnetosphere` would have been true only by coupling between distinct regions, which is not
what "the physical region the software supports science functionality for" asks for.

**Considered and rejected.** `Earth Lower and Middle Atmosphere` — the OMTI instrument name includes
"Mesosphere", but the package is agnostic to emission layer and the shipped OMTI data is projected at
140 km, well above the mesosphere; no mesospheric-specific functionality exists. `Earth Inner /
Outer Magnetosphere`, `Earth Magnetotail`, `Earth Magnetosheath` — no supporting evidence, and they
would reintroduce and narrow the magnetospheric over-claim removed above. The solar, heliospheric and
planetary regions in the vocabulary are inapplicable to a ground-based terrestrial ionospheric
package.

### 6. Authors (MANDATORY)

The five authors, with their identifiers and affiliations, in the sequence this record holds them:

1. **Michael Hirsch** — https://orcid.org/0000-0002-1637-6526
   - Boston University — https://ror.org/05qwgg493
   - Scivision, Inc. — no identifier
2. **Joshua Semeter** — no identifier
   - Boston University — https://ror.org/05qwgg493
3. **Gregory Starr** — https://orcid.org/0000-0002-3487-3630
   - Boston University — https://ror.org/05qwgg493
   - Johns Hopkins University Applied Physics Laboratory — https://ror.org/029pp9z10
4. **Anna Stuhlmacher** — no identifier
   - Boston University — https://ror.org/05qwgg493
5. **John Swoboda** — https://orcid.org/0000-0003-2627-2031
   - Boston University — https://ror.org/05qwgg493

**Reconciliation of the sources.** Three sources name authors and they do not agree, so the set is
the union of all of them and no credited author is dropped:

- The Zenodo deposit and its DataCite registration list five creators, all affiliated "Boston
  University", in the order Swoboda, Hirsch, Stuhlmacher, Starr, Semeter. DataCite has them parsed
  into given/family names
  (`Swoboda, John`; `Hirsch, Michael`; `Stuhlmacher, Anna`; `Starr, Greg`; `Semeter, Joshua`) with no
  `nameIdentifiers`.
- `README.rst` credits ":Primary Author: John Swoboda" and ":Co-Authors: Anna Stuhlmacher, Michael
  Hirsch" — a subset of three, consistent with the deposit but not contradicting it.
- The existing HSSI record already stores all five people, and supplies three ORCIDs and two
  affiliations that no other source provides.

**What the sources say about credit order.** The deposited DOI record lists its creators as Swoboda,
Hirsch, Stuhlmacher, Starr, Semeter. That is a credit order chosen by the depositing author, so it is
evidence about how the authors saw the contribution, and `README.rst` agrees on the lead: it
designates John Swoboda ":Primary Author:" and Anna Stuhlmacher and Michael Hirsch ":Co-Authors:".
This is recorded because it is a durable fact about the deposit, not because it is what this field
holds — the sequence in the value list above is the sequence this record holds. A future agent
comparing the two will find they differ; that difference is expected and is not drift to correct.

**ORCID verification.** Each stored ORCID resolves to a person whose ORCID-registered name matches
the author it is attached to: `0000-0003-2627-2031` -> "John Swoboda", `0000-0002-3487-3630` ->
"Gregory Starr", `0000-0002-1637-6526` -> "Michael Hirsch". The last of these also lists a Boston
University (ECE) research-scientist employment, corroborating both the identity and the stored Boston
University affiliation.

**"Greg Starr" versus "Gregory Starr" — settled, do not reopen.** The deposit says "Greg Starr"; the
record stores "Gregory Starr", which is the name registered on the matching ORCID record. The stored
form is therefore at least as authoritative as the deposit's, and it stands. The Johns
Hopkins University Applied Physics Laboratory affiliation stored for this author is not present in the
deposit; it is retained as additional information from the existing record rather than treated as a
conflict, and its ROR `https://ror.org/029pp9z10` was confirmed against ror.org.

**Scivision, Inc. has no ROR, and none should be attached.** A ror.org search for "Scivision"
returns a single organization, "SciVision Biotech Inc. (Taiwan)"
(`https://ror.org/011qev639`), which is an unrelated company. Leaving this affiliation without an
identifier is correct.

**Contributors who are not authors.** Commit authorship (`git shortlog -sne --all`) shows John
Swoboda, Michael Hirsch (under several identities), Anna Stuhlmacher and Gregory Starr, and does not
show Joshua Semeter. This corroborates four of the five credited authors and is not a basis for
removing the fifth: the deposited creator list is the credit record, and a senior author who wrote no
commits is normal. No contributor appears in the commit history who is not already credited, so no
author is added on that basis.

### 7. Software Name (MANDATORY)
GeoDataPython

**This corrects a stored value of `jswoboda/GeoDataPython: ISR Sim Paper`, which is not a name.**
That string is the title Zenodo generates automatically for a GitHub release, of the form
`<owner>/<repo>: <release name>`. Each part is independently confirmed: the repository is
`jswoboda/GeoDataPython`, and the GitHub release for tag `v0.1` is named "ISR Sim Paper". The same
machine-generated pattern appears on the sibling deposit for the MATLAB implementation, titled
`jswoboda/GeoDataMATLAB: ISR Sim Paper`, which confirms the pattern rather than a naming convention
chosen by the authors. The stored value was carried into HSSI by DOI autofill from that Zenodo title
and was not edited by a maintainer.

**Why `GeoDataPython`.** `README.rst` gives the project's own title in an RST title block:

    =============
    GeoDataPython
    =============

The repository is named `GeoDataPython` and the GitHub description reads "This holds the GeoData
implementation in Python". Field 7 asks for "the name of the software package as listed on the code
repository", which is exactly this.

**The `setup.py` `name='GeoData'` tension, and why it does not win.** `setup.py` declares
`name='GeoData'` and the importable package directory is `GeoData/`. That is the *distribution and
import* name, not the project name, and three things argue against promoting it to Field 7. First,
"GeoData" is the name of the data class and of the cross-language project family, which is
implemented twice: `jswoboda/GeoDataPython` (this software) and `jswoboda/GeoDataMATLAB` ("This is the
repository for the MATLAB version of GeoData..."), with an umbrella repository `jswoboda/GeoData`
holding both. Using "GeoData" here would make this record indistinguishable from the MATLAB
implementation, which has its own DOI (`https://doi.org/10.5281/zenodo.154536`). Second, the
distribution name was never published to PyPI — no `GeoDataPython` project exists there, and the
existing PyPI project `geodata` is an unrelated place-name gazetteer by a different author
(`https://github.com/corb555/Geodata`), so treating "GeoData" as this software's distribution
identity would point users at the wrong package. Third, the README title is the authors' own
presentation of the software's name.

**The PyHC label `geodata`.** The PyHC community registry lists this package with `name: "geodata"`
and `code: "https://github.com/jswoboda/GeoDataPython"`. That lower-case form is the registry's
display/slug label; it is not more authoritative than the project's own README title, and it shares
the disambiguation problem above. Recorded so the discrepancy is not mistaken for a conflict.

### 8. Description (MANDATORY)
GeoDataPython is the Python implementation of GeoData, a package to plot and analyze data from geophysics sources such as radar and optical systems. It is built around a container class: each instance holds one sensor's data set together with the name of its coordinate system, an array of measurement locations, the sensor's own WGS84 location, and the start and end time of every measurement. Users bring a new data type in by supplying a read function, and readers are included for Madrigal HDF5 incoherent-scatter radar files, SRI-format Resolute Bay and Poker Flat ISR HDF5 files, OMTI optical airglow HDF5 files, Poker Flat all-sky FITS images with their azimuth/elevation calibration maps, Neo sCMOS camera HDF5 files, and Mahali GPS total-electron-content files. Once loaded, a data set can be interpolated or regridded into another coordinate system (WGS84, ECEF, east-north-up, local Cartesian, or radar range-azimuth-elevation), reduced in time or in location, time-registered against a second data set so that overlapping measurements can be compared, transformed parameter by parameter, and written out as a structured HDF5 file. The plotting routines produce two-dimensional slices and contours, greyscale-optical-plus-radar overlays on a common grid, range-versus-time and range-versus-parameter plots, radar beam-position polar plots, and three-dimensional slice renderings in either matplotlib or Mayavi.

**This replaces a stored one-sentence description, and here is why.** The stored text was "This is
the repository for the Python version of GeoData to plot and analyze data from geophysics sources
such as radar and optical systems." — 140 characters quoted from the README's Overview section. The
replacement is not a rephrasing for taste; it addresses two substantive defects.

First, the stored sentence describes the *repository* rather than the software, spending its opening
words on "This is the repository for...". Second, Field 8 asks for a description "sufficiently
detailed to provide the potential user with information to determine if the software is useful to
their work", including what the software does and what assumptions it makes; the stored sentence
names no data type, no coordinate system, no capability, and no instrument, so a reader cannot judge
usefulness from it.

**Why the usual presumption in favour of a submitted value does not apply here.** Two features mark
the stored pair as the product of automated extraction rather than a maintainer's choice. Field 8 was
the README's Overview sentence lifted whole, opening words and all, rather than a description written
for this field; and Field 9 held that same string byte-for-byte instead of the distinct preview it
exists to provide. Someone deliberately choosing wording does not duplicate one sentence into both a
description and its alternate preview. There was therefore no editorial intent to override here, only
an extraction artefact to repair — which is also why the repair keeps as much of the authors' own
language as it can instead of substituting fresh prose.

**Editorial intent is preserved.** The authors' own descriptive clause — "to plot and analyze data
from geophysics sources such as radar and optical systems" — is carried through verbatim as the
first sentence's predicate. Everything added is drawn from the repository: the class variables and
`coordnames` tables in `README.rst`, the read functions in `GeoData/utilityfuncs.py`, the class
methods in `GeoData/GeoData.py`, and the plotting functions in `GeoData/plotting.py` and
`GeoData/plottingmayavi.py`.

**Alternative considered.** The PyHC registry's curated description, "Geophysics analysis of radar
and optical systems.", is accurate but is 49 characters and conveys less than the stored value; it
was not adopted for either Field 8 or Field 9.

### 9. Concise Description (OPTIONAL)
Python implementation of GeoData: reads, time-registers, interpolates and plots geophysics data from radar and optical sensors such as incoherent-scatter radars and all-sky imagers.

181 characters, within the 200-character limit and inside the 150-200 band the field targets.

**This replaces a stored value that was byte-identical to Field 8.** Field 9 exists to provide a
better preview than the first 150-200 characters of the description; storing the same string in both
fields left it doing nothing. The replacement is written as a preview: it identifies the software,
its four core verbs, and the two instrument classes it is built around, without the
repository-centric opening discussed under Field 8.

### 10. Publication Date (RECOMMENDED)
2016-09-20

**Independently confirmed by three sources.** The Zenodo record's `publication_date` is `2016-09-20`,
its DataCite registration carries a date of `2016-09-20` with `dateType: Issued`, and the GitHub
release for `v0.1` was published at `2016-09-20T17:12:31Z`. Field 10 is the date of first
publication for the initial version, so the repository's first commit (2014-07-21) is not the value
here: the software was first *published*, with a DOI, on 2016-09-20.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

The DOI was obtained through the GitHub-Zenodo release workflow, which the field
guidance says makes Zenodo the correct publisher; DataCite also records `publisher: Zenodo`. The
identifier is a URL rather than a ROR because Zenodo is a repository service rather than a registered
organization and has no ROR of its own. CERN's ROR (`https://ror.org/01ggx4157`) was considered and
rejected: it identifies the host institution, not the publisher named in the DOI record.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.1
- **Version Date:** 2016-09-20
- **Version Description:** This version was used to create figures for the ISR paper.
- **Version PID:** https://doi.org/10.5281/zenodo.154533

**`v0.1` is the latest authoritative version, and `0.2.0` in `setup.py` is not a release.** The
repository carries a single tag, `v0.1`, pointing at commit
`58e4d014091f9c11fe057929ef79e9c55e114c5d`; there is a single GitHub release, for that tag; and there
is a single Zenodo deposit. `setup.py` at the pinned revision declares `version='0.2.0'`, but no tag,
release, or distribution corresponds to it, and the package is not on PyPI. The decisive evidence
that this file's version string never tracked releases in this repository is its history:
`setup.py` already declared `'version': '0.2'` on 2014-08-25 (commit `a2f26f0`), two years *before*
the `v0.1` release tag existed; the string was reformatted to `version=0.2` on 2016-04-12 and to
`version='0.2.0'` on 2017-11-20 (commit `f9b0063`). A version string that was already "0.2" two
years before the "v0.1" release cannot be read as a release marker. Later untagged commits up to
2018-04-20 likewise do not constitute a newer version.

**The version date corrects a stored value of `2023-04-25`, and that wrong value has a traceable
origin.** No commit, tag, release, or deposit happened on that date, but the DataCite record for
`10.5281/zenodo.154533` carries `attributes.updated = "2023-04-25T23:59:49.000Z"` — the date part of
which is exactly the stored value. That record exposes several timestamps that are easy to confuse:
`created = "2016-09-20T17:12:54.000Z"`, `registered = "2016-09-20T17:12:55.000Z"`, and the release
date proper in `dates: [{"date": "2016-09-20", "dateType": "Issued"}]`. The stored value is therefore
best explained as a DOI-autofill path reading the record's own last-modified timestamp instead of its
`Issued` date, rather than as an unexplained ingest artefact. The failure mode is worth recognising on
other records: it yields a well-formed date that postdates the software by years, so a format or
plausibility check will not catch it; comparing the candidate against the record's `Issued` date will.
Every authoritative representation of the v0.1 release date is 2016-09-20:

- Zenodo `publication_date`: `2016-09-20`; DataCite `Issued` date: `2016-09-20`.
- GitHub release `created_at`: `2016-09-20T03:05:47Z`; `published_at`: `2016-09-20T17:12:31Z`.
- The `v0.1` tag's commit: `2016-09-19 23:05:47 -0400`, which is `2016-09-20T03:05:47Z` in UTC.

The apparent alternative of 2016-09-19 is only the US-Eastern *local* date of the tag commit; the
same instant is 2016-09-20 in UTC, and it matches the release's `created_at` exactly. Since the
DOI record, the release, and the tag all agree on 2016-09-20 in UTC, that is the authoritative
version date.

**Version description** matches the GitHub release body ("This version was used to create figures
for the ISR paper.") apart from that body's trailing newline, and matches the Zenodo description once
its `<p>` wrapper is stripped. The paper it refers to is identified under Field 27.

**Version PID** — see Field 2 for why the same DOI legitimately appears in both fields.

### 13. Programming Language (RECOMMENDED)
- Python 2.x
- Python 3.x

**`Python 2.x` is added.** The software targets both major versions: `.travis.yml` runs the test
suite under `python: [2.7, 3.6]`; `setup.py` declares `python_requires='>=2.7'`; and `Test/test.sh`
runs each example under `python2` and then `python3`.

The package source carries four distinct two-and-three compatibility shims, each in its own set of
files:

- `from __future__ import division, absolute_import` heads `GeoData/GeoData.py` (line 8),
  `GeoData/utilityfuncs.py` (line 21), `GeoData/CoordTransforms.py` (line 9), `GeoData/plotting.py`
  (line 9) and `GeoData/plottingmayavi.py` (line 6). The two package files without it are
  `filescraping.py` and the four-line `__init__.py`.
- The `six` scalar-type aliases are imported in two modules: `GeoData/GeoData.py` line 9
  (`from six import integer_types,string_types`) and `GeoData/utilityfuncs.py` line 22
  (`from six import string_types,integer_types`).
- `GeoData/filescraping.py` line 6 uses the relocated standard-library path,
  `from six.moves.urllib.request import urlretrieve, urlopen`.
- `GeoData/__init__.py` falls back from `pathlib` to `pathlib2` when the former is absent or lacks
  `Path().expanduser()`.

One module is in fact Python-2-only: `filescraping.py` line 102 uses a Python 2 `print` statement, so
it cannot be imported under Python 3 at all.

**`Python 3.x` is retained** — CI tested 3.6, several test scripts carry `#!/usr/bin/env python3`
shebangs, code comments call out Python 3 behaviour (`list()` "necessary for Python3"), and the PyHC
registry rates this package's Python 3 support "Good".

**`Other` was stored previously and has been removed.** The one non-Python source file in the
repository is `Test/test.sh`, a bash test runner: GitHub's language breakdown reports Python 143,153
bytes against Shell 317 bytes, and the file is 317 bytes and 15 newline-terminated lines of which 11
are non-blank. Field 13 asks for the languages "most important for the software",
and a script that loops over three example programs under `python2` and then `python3` does not meet
that bar — it is test scaffolding, not a language the software is written in.

Nothing else in the repository could account for `Other`, which is what makes the removal safe rather
than merely tidy: besides the Python sources, the tracked files are `.travis.yml`, `.gitignore`,
`.gitattributes`, `LICENSE.md`, `README.rst`, `Test/README.rst`, three Jupyter notebooks whose cells
are Python, three HDF5 data files, and one PNG. A future agent finding `Other` absent should not read
it as an omission.

### 14. Reference Publication (RECOMMENDED)
Not found

**Negative research.** There is no publication describing this software: no JOSS or SoftwareX paper,
no `CITATION.cff`, no `codemeta.json`, and no "how to cite" section in `README.rst` (its only
citation affordance is the Zenodo DOI badge). The DOI record carries no `IsDescribedBy` related
identifier; its only related identifier is `IsSupplementTo` the GitHub tree at tag `v0.1`.

**Why the Radio Science paper is not this field's value.** `10.1002/2016RS006182` cites this
software (see Field 27) but describes a simulation study of ionospheric observability, not the
software; GeoDataPython appears there as a tool that was used. Promoting it to Field 14 would
misrepresent it as the software's descriptive publication. Recorded so the promotion is not made by
mistake later.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

The original submission carried no value for this field. The License URI recorded above is SPDX's own
canonical URL for the MIT License, rather than a hand-written variant such as
`https://spdx.org/licenses/MIT.html`.

**Derived from the repository, not from the DOI record.** `LICENSE.md` contains the verbatim MIT
License text, opening "The MIT License (MIT)" and "Copyright (c) 2015 John Swoboda". GitHub's
repository metadata independently classifies it as `{"key": "mit", "spdx_id": "MIT", "name": "MIT
License"}`, and the PyHC registry rates this package's license clarity "Good".

**The Zenodo record disagrees and is wrong.** Its `license` field is `{"id": "other-open"}`, and its
DataCite registration carries only `rightsList: [{"rights": "Open Access", "rightsUri":
"info:eu-repo/semantics/openAccess"}]`, which is an access statement rather than a licence. Neither
reflects the MIT terms actually shipped in the repository. This is the general pattern in which DOI
autofill reproduces the depositing service's own metadata errors, so the licence — like the
publication date and the version date under Fields 10 and 12 — is re-derived from primary sources in
the repository. `Other` was therefore considered and rejected: it would encode Zenodo's error into
HSSI when the SPDX-listed licence is unambiguous.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- airglow
- all-sky imager
- amisr
- aurora
- coordinate transformation
- data visualization
- electron density
- hdf5
- incoherent scatter radar
- interpolation
- ionosphere
- madrigal
- remote sensing
- sondrestrom
- thermosphere
- total electron content

The original submission carried no value for this field. Each term above is a single lower-case
keyword. `coordinate transformation` is written in the singular and unhyphenated, in preference to
the plural and hyphenated forms of the same term.

**Why each term.** `ionosphere` and `thermosphere` are the science regions; `incoherent scatter
radar`, `amisr`, `all-sky imager` and `airglow` name the instrument classes the readers target;
`aurora` is the phenomenon behind the high-latitude data sets the examples
sample; `electron density` and `total electron
content` are the measured quantities (`nel`/`ne` from the ISR readers, `TEC`/`vTEC` from
`readIonofiles` and `readMahalih5`); `madrigal` and `hdf5` are the dominant data source and format;
`interpolation`, `coordinate transformation` and `data visualization` are the core capabilities;
`remote sensing` describes the fusion of radar and optical remote-sensing measurements.

**Why `sondrestrom` appears here.** The Sondrestrom Incoherent Scatter Radar is genuinely supported
(see Field 32) but SPASE registers no record for it, so it cannot be carried as an observatory. This
keyword is what keeps the software discoverable to someone looking for Sondrestrom tooling, which is
the whole reason it is present.

**Considered and rejected.** `ionosphere_thermosphere_mesosphere` — the PyHC registry's facet tag for
this package, but it is a registry facet slug rather than a science keyword, and its applicable
components are recorded as separate lower-case keywords. `specific` — the PyHC entry's other tag,
meaningless as a science keyword. `python` — the language belongs in Field 13. `fusion` — ambiguous
with nuclear fusion. `poker-flat-research-range` — redundant, because Poker Flat is already
represented in Field 32.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- Madrigal
- Observatory/Mission-specific

The original submission carried no value for this field.

- **Madrigal** — `utilityfuncs.readMad_hdf5(filename, paramstr)` is documented as the "madrigal h5
  read in function", reads the Madrigal HDF5 layout directly (`/Metadata/Experiment Parameters`,
  `/Data/Table Layout`, and Madrigal parameter names such as `gdalt`, `azm`, `elm`, `ut1_unix`,
  `ut2_unix`), and two Madrigal HDF5 files are shipped in `Test/data/`. `Examples/MadrigalExample1.ipynb`
  is a worked Madrigal example.
- **HTTP/HTTPS Directories** — `filescraping.py` walks a dated HTTP directory tree
  (`Year/date/file.fits`) and downloads the files it finds; `readAllskyFITS` documents the archive
  it targets, `https://amisr.asf.alaska.edu/PKR/DASC/RAW/`.
- **Observatory/Mission-specific** — the readers are instrument-specific rather than generic:
  `readOMTI`, `readSRI_h5` ("the SRI formated h5 files for RISR and PFISR"), `readNeoCMOS`,
  `readMahalih5`. This value is also required as the cross-listing for the instrument and observatory
  associations in Fields 31 and 32, per the field guidance.

**Considered and rejected.** `CDAWeb`, `HAPI`, `SSCWeb`, `OMNIWeb`, `AMDA`, `das2`, `TAP`, `VirES`,
`GFZ`, `WDC`, `The Virtual Solar Observatory.` — no client, URL, or reference to any of these appears
in the repository. `FTP/FTPS Directories` — the scraper and downloader use HTTP(S) only.
`S3/Cloud-aware` — no cloud or object-store access. `Other` — unnecessary, since the three values
above cover every source the code actually reaches.

### 18. Input File Formats (RECOMMENDED)
- HDF5
- FITS
- ascii

The original submission carried no value for this field. Derived from the input/output code rather than from the
dependency list.

- **HDF5** — the dominant input format, read through two different libraries. Via `h5py`:
  `readMad_hdf5` (Madrigal), `readSRI_h5` (SRI-format RISR and PFISR), `readOMTI`, `readNeoCMOS`,
  `readMahalih5`. Via PyTables: `read_h5_main`, which walks groups and array nodes to reload the
  package's own structured output. All three files in `Test/data/` are HDF5.
- **FITS** — `readAllskyFITS(flist, azelfn, heightkm, timelims)` opens all-sky image files and their
  azimuth/elevation map files with `astropy.io.fits`, and reads the `GLAT`, `GLON`, `OBSDATE`,
  `OBSSTART` and `EXPTIME` header keywords.
- **ascii** — `readIonofiles(filename)` reads a plain-text ionofile with `np.genfromtxt`; the
  function's docstring documents all sixteen columns (day of year, year, receiver latitude and
  longitude, line-of-sight and vertical TEC and their errors, azimuth and elevation to satellite,
  mapping function, pierce-point latitude and longitude, satellite number, site, receiver bias and
  its error).

**Considered and rejected.** `Other`, which would have stood for two formats that are not actually
supported. `readAVI(fn, fwaem)` reads AVI video and a MATLAB `.mat` azimuth/elevation map, but its own
docstring says "caution: this was for a one-off test. Needs a bit of touch-up to be generalized to all
files"; it imports `cv2`, which is declared nowhere in `setup.py`; it calls `sp.io.loadmat` although
`scipy.io` is never imported in the module; and its body is duplicated after an unreachable second
`return`. It is not supported behaviour. `CDF`, `netCDF3/4`, `csv`, `JSON`, `IDL.sav`, `Zarr`,
`ISTP-Compliant` — no reader for any of these.

**Durable caveat.** Both HDF5 paths have rotted against current libraries: `read_h5_main` and
`write_h5` call `tables.openFile`, which PyTables renamed to `open_file` in 2013, and the `h5py`
readers use the `.value` attribute, removed in h5py 3.0. The formats above are what the software is
designed and documented to read; running the readers on a modern stack requires those call sites to
be updated.

### 19. Output File Formats (RECOMMENDED)
- HDF5

The original submission carried no value for this field.

**Evidence.** `GeoData.write_h5(filename)` writes the class's full state to a structured HDF5 file
using PyTables, creating a group per dictionary-valued attribute and an array per data key, and
`GeoData.read_h5` / `read_h5_main` read that file back. The documented examples also write HDF5
results directly: `Test/altitudeSlicev2.py` and `Test/altitudeSlice_mishap.py` write interpolated
`nel` and `ti` arrays to `altitudeSliceOutput.h5` with `h5py`.

**Considered and rejected.** Rendered figures are not a data output format — the examples save PNG
images (`figmplf.savefig(figname, format='png', dpi=400)` in `Test/plottingtest3d.py`), and
`plottingmayavi.plot3Dslice` can return a rendered screenshot array, but graphics are not data
written in an interchange format, and PNG is not among the formats this field records. No writer
exists for ascii, csv, FITS, CDF, netCDF, JSON, IDL.sav or Zarr, so
none is claimed even though several of those formats can be read. The `tables.openFile` caveat under
Field 18 applies to `write_h5` as well.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac

The original submission carried no value for this field.

- **Linux** is proven: `.travis.yml` declares `os: [linux]` and ran `pip install -e .` followed by
  the test suite under both Python 2.7 and 3.6. The README's Mayavi troubleshooting section also
  gives a Debian/Ubuntu command (`sudo apt install mayavi2`).
- **Mac** is evidenced but not CI-proven: the worked example call left in
  `GeoData/utilityfuncs.py` line 312 reads a Madrigal file from
  `/Users/anna/Research/Ionosphere/2008WorldDaysPDB/son081001g.001.hdf5`, a macOS home-directory
  path belonging to the co-author who wrote that reader, so the reader was exercised on macOS. This
  is consistent with the package's composition: it is pure Python with no compiled extension, no
  platform-specific code, and no OS-dependent path handling (it routes everything through
  `pathlib`/`pathlib2`).

**Windows is deliberately not claimed** — there is no CI job, install instruction, or other evidence
for it, and `Test/test.sh` is a bash script invoking `python2`/`python3`, which assumes a POSIX
environment. **`Operating System Independent` was considered and rejected** for the same reason:
without any Windows evidence, the general claim would be an over-claim, even though the pure-Python
composition makes it plausible.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

The original submission carried no value for this field.

**Reasoning.** The package is pure Python: `setup.py` declares no extension modules, the repository
contains no C, C++, Fortran or assembly source (GitHub's language breakdown reports only Python and
Shell), and no code branches on architecture, word size, or endianness. Its dependencies (numpy,
scipy, pandas, PyTables, h5py, astropy, matplotlib) are themselves distributed across architectures.
`x86-64` was considered and rejected as the value: it is the architecture the 2016-2018 Travis jobs
ran on, but recording it alone would wrongly imply an architecture restriction that the code does not
have, and recording it alongside `CPU Independent` would be self-contradictory. The
Travis-era x86-64 evidence is noted here instead.

### 22. Related Phenomena (OPTIONAL)
Not found — correctly empty.

**This is a vocabulary limitation, not missing research.** The seven phenomena terms this field
offers are `Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`,
`Solar Flares`, `Solar Wind` and `X-ray emission`. Six of them are solar or heliospheric and are
inapplicable to a ground-based terrestrial ionospheric package. The seventh, `Geomagnetic Storms`, was considered and rejected: some of the
example intervals fall in disturbed periods, but the package contains no storm-specific
functionality, no geomagnetic index handling, and no storm-time analysis, so selecting it would make
this record a false hit for storm searches.

The phenomena this software actually supports — aurora, airglow, ionospheric plasma structure, total
electron content — have no term here. Per the field's own instruction, those belong in Keywords, and
`aurora`, `airglow`, `electron density` and `total electron content` are recorded there (Field 16).

### 23. Development Status (RECOMMENDED)
Inactive

The original submission carried no value for this field.

**The evidence weighed.** Last push 2018-04-20 (over eight years before this extraction); a single
tag and a single GitHub release, `v0.1` (2016-09-20), which GitHub flags `prerelease: true`; four
issues left open, the most recent opened in 2017; CI configured for Travis CI, a service that no
longer builds this repository,
targeting Python 2.7 and 3.6, both long end-of-life; several call sites broken against current
library versions (`tables.openFile`, h5py `.value`, `plt.hold`); not packaged on PyPI. The repository
is *not* archived and not disabled, and the PyHC registry rates its software maturity "Partially
met". Absence of an archive flag is not evidence of active development, so it does not bear on the
choice.

The content of the issue tracker matters for two of the candidate values, so it is recorded here. The
four open issues are the primary author's own design notes — a plotting-keyword-argument cleanup
(#6), a question about WGS84 axis ordering (#4), and an evaluation of Plotly as an alternative to
Mayavi (#7) — plus a 2017 user question about where to obtain the example data (#8). Two of them show
the author responding: he answered the data-location question the same day with download links, and
on 2018-04-19 he wrote in #7 that he had "made a slice command that uses matplotlib" and was
"planning on moving the mayvi plotting to a different file, plotingmayvi.py". He did exactly that in
the final commit the next day. Nothing in any issue asks for or offers to hand over maintainership.

**Why not each of the other seven values.**

- `Active` ("reached stable, usable state and being actively developed") — no development for over
  eight years.
- `WIP` ("initial development in progress; no stable, usable public release yet") — development is
  not in progress.
- `Concept` ("minimal/no implementation; limited example/demo/proof-of-concept only") — the package
  is a complete implementation of roughly 3,100 lines across six modules, with a self-test, shipped
  sample data, three notebooks and eight example programs.
- `Suspended` ("stopped temporarily; authors intend to resume") — requires an intent to resume after
  stopping. The closest thing to a forward-looking statement is the 2018-04-19 issue comment quoted
  above, but that plan was carried out the following day rather than deferred, and the repository then
  went silent; nothing announces a temporary pause or an intention to return. Its first clause
  ("initial development started but stopped temporarily") also does not describe a project that
  reached a tagged, published release.
- `Moved` ("project moved to a new location; that version is authoritative") — there is no successor.
  The related repositories are a sibling, not a replacement: `jswoboda/GeoDataMATLAB` is the MATLAB
  implementation of the same class, and `jswoboda/GeoData` is an umbrella repository last pushed in
  January 2015, i.e. older than this one. Recorded because that umbrella repository's name invites
  exactly this mistake.
- `Abandoned` ("initial development started but abandoned; no stable release") — turns on "no stable
  release", which is falsified. There is a tagged, DOI-minted release that was used to produce the
  figures of a peer-reviewed paper (`10.1002/2016RS006182`, see Field 27), the release ships a
  passing self-test with numeric assertions that ran in CI under two Python versions, and PyHC lists
  the package as usable with documentation rated "Good". GitHub's `prerelease: true` flag on that
  release is the strongest argument for `Abandoned`, but it is weak evidence — the flag is routinely
  set casually, and the release body itself records that the code was used for published science.
- `Unsupported` ("reached stable, usable state but authors ceased work; new maintainer desired") —
  the first two clauses fit, but the third does not: no desire for a new maintainer is expressed in
  the README, the release notes, the four open issues, or the wiki. That specific requirement is what
  rules this value out. If the authors later state that they want a new maintainer, this becomes the
  correct value.

**Why `Inactive`.** Its defining clause — reached a stable, usable state but is no longer actively
developed — is the only one that both fits the evidence and requires no unevidenced assumption. Its
descriptive tail, "support provided as time allows", has not held for years, but that tail describes
the typical case rather than defining the term, and no other
value in the vocabulary comes closer. The issue tracker supports it too: the author did answer the
one user question that was asked, a year after the release, which is what "support provided as time
allows" looks like in practice, even though nothing has been answered since.

### 24. Documentation (RECOMMENDED)
https://github.com/jswoboda/GeoDataPython/blob/master/README.rst

The original submission carried no value for this field. `README.rst` *is* this project's documentation, and it
includes the installation instructions the field asks for. Its sections are: badges and title,
author credits, Overview, Installation (`git clone` then `pip install -e .`, plus Mayavi-specific
conda instructions), Software Structure with a per-file functionality table, a Style Guide, Class
Structure with tables of the class variables and the six supported coordinate-system names, Workflow,
Examples with a table of the example programs, and Error diagnosis for OpenGL and PyQt problems.

**Negative research establishing that nothing better exists.** There is no documentation site and no
`docs/` directory anywhere in the repository; there is no Sphinx configuration (no `conf.py`) and no
Read the Docs configuration; the GitHub repository's `homepage` field is empty and `has_pages` is
false; and the PyHC registry entry for this package has no `docs:` key, unlike most neighbouring
entries. One detail invites a false lead: `.gitignore` carries the lines "# Sphinx documentation" and
`docs/_build/`, but those come from the stock Python `.gitignore` template and no Sphinx project was
ever added. The GitHub
wiki is enabled (`has_wiki: true`) but empty: its single Home page contains only the default stub
text "Welcome to the GeoDataPython wiki!", so it must not be used here.

**Alternative considered.** The repository root URL (`https://github.com/jswoboda/GeoDataPython`)
also renders this README, and the field explicitly permits reusing the access URL. The file URL was
chosen because it points at the documentation itself and remains distinguishable from Field 3.

### 25. Funder (OPTIONAL)
Not found

**Negative research.** The repository contains no funding statement of any kind: no acknowledgements
section in `README.rst`, no funding note in `LICENSE.md` or `setup.py`, no `CITATION.cff`, and no
funding metadata in the DOI record (`fundingReferences` is an empty array in the DataCite
registration, and the Zenodo record carries no grant information).

**A funding lead exists and was deliberately not applied.** The Radio Science paper that this release
was made for and that cites it (`10.1002/2016RS006182`, Field 27) records a publisher-asserted funder
of the National Science Foundation under award `AGS-1339537`. That establishes who funded the *study*,
not who funded this software, and the authors have made no such statement about the code. Recording it
would turn an inference into an apparently sourced fact, so Fields 25 and 26 stand empty. The lead is
preserved here as a follow-up: a maintainer who can confirm the grant with the authors could fill both
fields from it, and until then no agent should apply it from the paper alone.

### 26. Award Title (OPTIONAL)
Not found

**Negative research.** As under Field 25, no award is named in the repository or the DOI record. The
one candidate award number (NSF `AGS-1339537`, from the citing paper's Crossref funder data) is not
applied, for the reason given there. A second obstacle applies specifically to this field: only the
award number is available from that source, and Field 26 asks for the award *title*.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1002/2016RS006182

The original submission carried no value for this field. This is Swoboda, J., Semeter, J., Zettergren, M., and
Erickson, P. J. (2017), "Observability of ionospheric space-time structure with ISR: A simulation
study", *Radio Science*, 52, 215-234.

**Why this is the right identification, and how it was established.** The `v0.1` release is named
"ISR Sim Paper" and its description says "This version was used to create figures for the ISR paper",
but neither the release nor the DOI record links to the paper. The link is established from the
publication side: the paper's Crossref record lists this software's DOI, `10.5281/zenodo.154533`, in
its reference list as a publisher-asserted DOI reference, alongside `10.5281/zenodo.154536`, the
sibling GeoDataMATLAB deposit made on the same day. The paper's first author is this software's
primary author and its second author is a credited co-author. That is a direct, publisher-asserted
citation of this software by that paper, which is exactly what Field 27 collects ("publications that
describe, cite, or use the software").

The same finding corroborates two other fields: it is the "stable release used for published
science" that settles Field 23, and it explains why `utilityfuncs.readIono` exists (Field 30) — the
simulation study fed simulator output through GeoData for plotting.

### 28. Related Datasets (OPTIONAL)
Not found

**Negative research.** The repository ships three data files under `Test/data/`, and each was traced
to its origin from the file's own internal metadata: `ran120219.004.hdf5` is a Madrigal file whose
`/Metadata/Experiment Parameters` table names the instrument "Resolute Bay North IS Radar", covering
2012-02-19 23:50 to 2012-02-22 15:14 UT; `son130104.001.hdf5` names "Sondrestrom IS Radar", covering
2013-01-04 12:32 to 2013-01-14 20:01 UT; `OMTIdata.h5` is the package's own structured HDF5 holding
optical data with a sensor location of 74.72955 N, 94.90576 W at 145 m, i.e. Resolute Bay, for
2012-02-20. None of these has a dataset DOI or a persistent identifier — they are Madrigal
experiment files and a locally converted optical file — and the DOI record lists no related dataset.
`Test/README.rst` confirms that the larger example data set is distributed informally: "To run these
examples, you need the data files in the Google Drive GeoDataTest folder. Ask the authors for access
to these files".

### 29. Related Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.154536

The original submission carried no value for this field. This DOI is `jswoboda/GeoDataMATLAB: ISR Sim Paper`, the
MATLAB implementation of the same GeoData class, at repository
`https://github.com/jswoboda/GeoDataMATLAB`.

**Why it qualifies.** It is a sibling implementation performing the same task in another language:
its README states "This is the repository for the MATLAB version of GeoData to plot and analyze data
from geophysics sources such as radar and optical systems", and describes the same class-plus-read-
functions architecture with the same `read_` naming convention. This software's own `README.rst`
cross-references it — the class-variable table explains that "In MATLAB the field names will be the
data names and the arrays will be the values" — so a reader of this record needs to know that the
MATLAB implementation exists and is distinct. The two were released together for the same paper: the
MATLAB deposit is titled with the same release name and both DOIs appear side by side in that paper's
reference list (Field 27). Its DOI is recorded in preference to its repository URL, as the field
prefers.

**Considered and rejected.**

- `https://github.com/jswoboda/GeoData` — the umbrella repository that once held "both the python
  implementation of the GeoData classes and the MATLAB inplementation along with overall
  documentation". Rejected because it is a one-line-README shell last pushed 2015-01-09, superseded
  by the two implementation repositories, and listing it would tell a reader nothing about this
  software. Recorded because its name makes it a likely future mistake.
- `SimISR` — it belongs in Field 30, where a specific exchange is documented, and is not duplicated
  here.
- The entire generic scientific-Python stack declared in `setup.py` — `numpy`, `scipy`, `pandas`,
  `matplotlib`, `seaborn`, `tables`, `h5py`, `nose`, `six`, `python-dateutil`, `pathlib2`,
  `beautifulsoup4`, plus the undeclared `requests` and `pytz` and the optional `mayavi`. Being a
  dependency is not a relationship that distinguishes this software; each of these entries would read
  identically for a large share of the ecosystem.
- `astropy` — a declared dependency, used only as `astropy.io.fits` to read all-sky image files. That
  is file-format I/O, not an interoperation, and it is recorded where it belongs: `FITS` under
  Field 18.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/jswoboda/SimISR

The original submission carried no value for this field. SimISR ("ISR Data Simulator") is the current name of the
project the code calls RadarDataSim; GitHub redirects `jswoboda/RadarDataSim` to `jswoboda/SimISR`,
confirming the rename. No DOI was found for it, so the repository URL is recorded, as the field
permits.

**The specific documented exchange.** `GeoData/utilityfuncs.py` lines 262-310 define
`readIono(iono, coordtype=None)`, documented as "This function will bring in instances of the
IonoContainer class into GeoData. This is using the set up from the RadarDataSim codebase". It is an
adapter over that package's in-memory data model: it reads `iono.Param_Names`, `iono.Param_List`,
`iono.Coord_Vecs`, `iono.Cart_Coords`, `iono.Sensor_loc` and `iono.Time_Vector`, calls
`iono.getDoppler()` when no line-of-sight velocity is present, and returns the five-tuple that
constructs a `GeoData` instance. That is one package's output object being imported into the other, by
a named function, and both are heliophysics domain tools by the same author.

**SimISR states the same relationship from its own side.** Its `README.md` says: "The user can also
take advantage of two different APIs to plot results using the SimISR. The first is in Python and is
called [GeoDataPython](https://github.com/jswoboda/GeoDataPython). A MATLAB version of this API is
also avalible called [GeoDataMATLAB](https://github.com/jswoboda/GeoDataMATLAB). Both APIs can read in
the structured files from SimISR." The pairing is therefore asserted by both packages rather than
inferred from one side, and SimISR nominates this software as its own Python plotting API. That
quotation should be read for what it claims and no more: it is SimISR's statement that its structured
files can be read by these two APIs. That is a file-level exchange, distinct from and additional to
the in-memory `IonoContainer` adapter documented above, and nothing in this repository was exercised to
confirm the file-level claim. The same sentence names GeoDataMATLAB, which independently
corroborates the sibling relationship recorded in Field 29.

The relationship is also corroborated by the Radio Science paper of Field 27, a simulation study by
this author that cites this software.

**Excluded, and why.** Everything listed as rejected under Field 29 is excluded here for the same
reasons; in particular `astropy` and `h5py` are foundational-but-domain-adjacent packages that
qualify only with a cited exchange, and their use here is internal file I/O. `mayavi` and `matplotlib`
are rendering back-ends, not peer tools. Sharing a Python runtime with a package is not
interoperability.

**Not verified, deliberately not listed.** Two of the same author's repositories look like plausible
companions — `jswoboda/omticode` ("this is all of the code for the omti fusion stuff", last pushed
2014-11-21) and `jswoboda/MahaliPlotting` ("This will hold the sensor fussion plotting code for the
Mahali project") — and their subject matter overlaps this package's OMTI and Mahali readers. Neither
is listed because no exchange with this software could be confirmed: `MahaliPlotting` has no README,
and nothing in this repository references either project. Recorded so a future agent knows the lead
was examined rather than missed.

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** Optical Mesosphere Thermosphere Imagers
  **Instrument Identifier:** https://spase-metadata.org/IUGONET/Instrument/ISEE/OMTI/RSB/All-SkyImager

The original submission carried no value for this field. The entry above is identified by its SPASE
Resource ID; every supported instrument for which SPASE holds no record is instead associated through
its platform or site record in Field 32, or omitted with its reasoning below.

**Why this instrument is designed-to-support, not merely mentioned.** `utilityfuncs.readOMTI(filename,
paramstr)` is a reader written specifically for OMTI optical data; `Test/data/OMTIdata.h5` is OMTI
data shipped in the repository; `Test/test.py`, the self-test that CI ran, asserts specific numeric
values from it (`omti.data['optical'][[32,41],[22,39]]`); the README's banner image is captioned
"GeoDataPython example of OMTI and RISR data"; and both `Examples/FusionExample.ipynb` and
`Examples/FusionExamplempl.ipynb` are built around loading and overlaying it.

**How the specific station was selected.** SPASE registers a separate all-sky-imager record for each
OMTI station, and many of them share the name "Optical Mesosphere Thermosphere Imagers", distinguished
only by the station segment of the identifier path. In-repo evidence selects one: the shipped
`OMTIdata.h5` records `sensorloc = [74.72955, -94.90576, 145.0]`, which is Resolute Bay, and the
Resolute Bay record is the `.../OMTI/RSB/All-SkyImager` identifier above. (The same coordinates appear
as the "Resolute Bay North IS Radar" instrument position in the shipped Madrigal file, to five decimal
places, which indicates the optical data was gridded about the radar's origin; both instruments are at
Resolute Bay, so the station identification is unaffected.) No other OMTI station is claimed, because
nothing in this repository evidences data from any of the others.

**Instruments the software is designed to support for which SPASE holds no instrument record —
associated at platform level or omitted.**

- **RISR-N, the Resolute Bay North Incoherent Scatter Radar.** Genuinely supported: the shipped
  `Test/data/ran120219.004.hdf5` names the instrument "Resolute Bay North IS Radar" in its Madrigal
  `Experiment Parameters` table, `readSRI_h5` is documented as reading "the SRI formated h5 files for
  RISR and PFISR", `Test/load_isropt.load_risromti` loads it, and the CI self-test asserts values from
  it. SPASE registers no instrument record for it: nothing carries the name or abbreviation RISR, and
  the SPASE instrument records at Resolute Bay are magnetometers
  (`https://spase-metadata.org/SMWG/Instrument/Ground/Resolute.Bay/Magnetometer`,
  `https://spase-metadata.org/SMWG/Instrument/WDC/Resolute/Magnetometer`,
  `https://spase-metadata.org/IUGONET/Instrument/WDC_Kyoto/WDC/RES/Magnetometer`), a different
  instrument class. Associated instead through its platform record in Field 32.
- **PFISR, the Poker Flat Incoherent Scatter Radar.** Genuinely supported: named in the `readSRI_h5`
  docstring, loaded by `Test/load_isropt.load_pfisr_neo`, used by three example programs
  (`Test/RTI_2007-03-23.py`, `Test/rangevtime_mishap.py`, `Test/subplots_mishap.py`, which loads
  `pfa110302.002.hdf5`) and by `Examples/MadrigalExample1.ipynb` (`pfa140105.004.hdf5`). SPASE
  registers no instrument record for it either — its Poker Flat instrument records are magnetometers,
  an MF radar, and other programmes' cameras. Associated instead through platform records in
  Field 32.
- **The Poker Flat all-sky camera (DASC).** Genuinely supported: `readAllskyFITS` is documented "this
  works with Poker Flat DASC all-sky, FITS data available from:
  https://amisr.asf.alaska.edu/PKR/DASC/RAW/", and `filescraping.py` hard-codes that archive's
  conventions, matching links with `re.compile("^(PKR)")` inside a `Year/date/` directory tree and
  parsing the timestamp out of the `PKR_*` filename. SPASE registers no record for this camera: there
  is no DASC or "Digital All Sky" entry, and the SPASE optical instrument records at Poker Flat belong
  to other programmes — `https://spase-metadata.org/IUGONET/Instrument/NICT/SALMON/PF/asi` (the NICT
  SALMON all-sky imager) and
  `https://spase-metadata.org/IUGONET/Instrument/TohokuU/opt_obs/pok/ac` (a Tohoku University aurora
  camera). Recording either of those would attribute support for an instrument this software does not
  read. Associated instead through the site record in Field 32.
- **The Neo sCMOS auroral camera.** Genuinely supported by a dedicated reader, `readNeoCMOS(imgfn,
  azelfn, heightkm, treq)`, which reads `/rawimg`, `/ut1_unix`, `/sensorloc` and plate-scale
  `/params`, and by `Test/subplots_mishap.py` ("March 2011 example at PFISR with Neo sCMOS camera").
  Omitted from Field 31 with documentation: SPASE registers no sCMOS or Neo camera record. The camera
  operated at Poker Flat, so it is covered at site level in Field 32.
- **The Mahali GPS receiver network.** Genuinely supported by two readers, `readMahalih5(filename,
  des_site)` (per-site TEC from the network's HDF5, under a `#%% Mahali` section heading) and
  `readIonofiles(filename)` (the network's ASCII ionofile format). Omitted with documentation: SPASE
  registers no Mahali record, and the GNSS instrument records it does hold belong to unrelated
  programmes (Swarm spacecraft receivers and a dense Japanese school-based GPS network), so none may
  be substituted. This is a documented omission, not an oversight.
- **The Sondrestrom Incoherent Scatter Radar.** See Field 32, where the same reasoning applies to its
  site.

**Every entry in Fields 31 and 32 is identified by a SPASE record**, and no name is recorded without
one. Each supported instrument that SPASE does not register was either associated through its platform
or site record in Field 32 or omitted with its reasoning above. No case arose in which several SPASE
records plausibly denoted the same instrument with nothing in the repository to choose between them.

The absences recorded above were established against the SPASE registry as it stood when this dossier
was written, and they are the kind of finding that can expire: if SPASE later registers RISR-N, PFISR,
the Poker Flat DASC, the Neo sCMOS camera, the Mahali network, or the Sondrestrom radar, the
corresponding omission or platform-level substitution should be revisited in favour of the specific
instrument record. Nothing about the software's relationship to those instruments would need to be
re-established — the designed-to-support evidence for each is set out above.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Advanced Modular Incoherent Scatter Radar
  **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/AMISR
- **Observatory Name:** OMTI Resolute Bay station
  **Observatory Identifier:** https://spase-metadata.org/IUGONET/Observatory/ISEE/OMTI/RSB
- **Observatory Name:** Poker Flat Geophysical Observatory
  **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Ground/Poker.Flat

The original submission carried no value for this field. Each entry is identified by its SPASE
Resource ID.

- **Advanced Modular Incoherent Scatter Radar** is the platform-level association for the two AMISR
  radars this software reads, RISR-N and PFISR, neither of which SPASE registers as an instrument
  (Field 31). A user searching for AMISR data tooling should find this package: it reads AMISR data in
  both the SRI HDF5 and Madrigal HDF5 forms, ships an RISR-N file, and tests against it.
- **OMTI Resolute Bay station** is the platform of the OMTI imager recorded in Field 31, selected by
  the same shipped-coordinates evidence.
- **Poker Flat Geophysical Observatory** is the site-level association for three Poker Flat
  instruments SPASE does not register individually: PFISR, the DASC all-sky camera whose archive
  `filescraping.py` is written against, and the Neo sCMOS camera. It is the SMWG ground observatory
  record for the Poker Flat site, under that facility's own name.

**Sondrestrom is a documented omission — genuinely supported, but nothing defensible resolves.** The
support is not in doubt: `readMad_hdf5` is documented as the "madrigal h5 read in function for the
python implementation of GeoData for Madrigal Sondrestrom data",
`Test/data/son130104.001.hdf5` is a Madrigal file whose own metadata names the instrument
"Sondrestrom IS Radar" at 67.0 N, 309.0 E, and `plotting.py` carries two Sondrestrom-specific code
comments at lines 735 and 783 ("what should tolerance be for Sondrestrom mechanical dish"). Two SPASE
records mention the locality and both were rejected:

- `https://spase-metadata.org/ISWI/Observatory/GIRO/SMJ67_SondrestromAB`, "SMJ67 Sondrestrom AB,
  Greenland" — a Global Ionospheric Radio Observatory Digisonde station. This software reads no
  Digisonde data; recording it would assert support for a different instrument class that happens to
  share the site.
- `https://spase-metadata.org/SMWG/Observatory/Ground/Kangerlussuaq`, whose name is
  "Observatory Station Code: STF" — the ground magnetometer site record for Kangerlussuaq (the
  instrument SPASE registers under it is `Kangerlussuaq Magnetometer`). Beyond the instrument-class
  mismatch, its registered name is a bare station code, which would surface to users as a meaningless
  label.

There is no SPASE record for the Sondrestrom Incoherent Scatter Radar itself or for its facility, so
the entry is omitted rather than resolved to a near-miss, and the term `sondrestrom` is carried in
Keywords (Field 16) so the record is still discoverable. This asymmetry with the Poker Flat decision
above is deliberate: the Poker Flat record carries the actual facility's name and is the site where
the supported instruments operate, whereas both Sondrestrom candidates denote other instrument
programmes and one has no usable name.

**Also considered and rejected.** The Resolute Bay geomagnetic observatory records
(`https://spase-metadata.org/SMWG/Observatory/Ground/Resolute.Bay` named "Observatory Station Code:
RES", `https://spase-metadata.org/SMWG/Observatory/IAGA/Resolute.Bay`,
`https://spase-metadata.org/IUGONET/Observatory/WDC_Kyoto/WDC/RES`,
`https://spase-metadata.org/SMWG/Observatory/WDC/Resolute`) — magnetometer station records, not the
radar facility, so they are not substitutes for RISR-N; RISR-N is covered by the AMISR record. The
other Poker Flat observatory records (`https://spase-metadata.org/SMWG/Observatory/IAGA/Poker.Flat`,
`https://spase-metadata.org/IUGONET/Observatory/TohokuU/opt_obs/pokopt`,
`https://spase-metadata.org/IUGONET/Observatory/TohokuU/mag_obs/pokmag`,
`https://spase-metadata.org/IUGONET/Observatory/WDC_Kyoto/WDC/POK`,
`https://spase-metadata.org/IUGONET/Observatory/NICT/SALMON/PF`) — each belongs to a specific other
programme's optical or magnetometer observations at the same site; the SMWG site record was preferred
as the single, programme-neutral association. The remaining OMTI station records — no evidence in this
repository for any station other than Resolute Bay. `European Incoherent Scatter Scientific
Association` and the Millstone Hill records — no reference to either appears in the repository.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/jswoboda/GeoDataPython/c3e29541327ec754eb5a2a9e8dd94bf1abee3328/logo/logo1.png

The original submission carried no value for this field. The value above is deliberate and the
objection to it was weighed; both halves are set out below, because the value looks odd on its face
and a future agent needs to know it was examined rather than scraped.

**Why this URL is the software's designated logo.** The PyHC community registry entry for this package
sets
`logo: "https://github.com/jswoboda/GeoDataPython/raw/master/logo/logo1.png"`. That is a manually
curated community value, and community curation outranks automated extraction for a presentational
field like this one. The project itself agrees on the designation:
the image lives in a directory the primary author named `logo/` (added 2015-06-12 in commit
`aa77be4`), it is the file `logo1.png`, and `README.rst` displays it as the banner immediately under
the title. Two independent sources therefore designate this *file* as this software's logo, and Field
33 is a presentational field asking for the link the project offers. The URL recorded above reaches
that same file through a commit-pinned `raw.githubusercontent.com` path rather than the registry's
`master`-referenced `/raw/` form: the registry is authoritative about which asset is the logo, not
about the URL string, and a branch reference breaks silently on any upstream rename, move or deletion.

**The content objection, considered and overruled.** The image's content is not a graphic identity. It
is a
9600 x 7200 pixel, 1.9 MB four-panel scientific figure — a 3-D electron-density isosurface with radar
beams over an OMTI ground image at 06:36 UT, a 2-D electron-density slice with a colourbar, a
greyscale OMTI optical panel, and a radar beam-position polar plot — carrying axis labels, colourbars
and UT timestamps, and containing no wordmark, icon, or project name. The README's own alt text calls
it "GeoDataPython example of OMTI and RISR data", i.e. the project describes it as example output of
its own plotting routines, which is what it is. At card or thumbnail size it would read as an
illegible plot rather than an identifying mark, and its dimensions make it a heavy asset.

That objection was weighed and did not outweigh the designation. Field 33 asks for a link to the
logo, and the two sources that get to say what this project's logo is — its own author, through the
`logo/` directory and the README banner, and the curated community registry — both name this file.
The objection is about whether the designated image is a *good* logo, which is not what the field
records. The value therefore stands as an examined choice rather than an unreviewed extraction, and it
should not be treated as an error to clean up.
