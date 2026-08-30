# HSSI Metadata Extraction Results

**HSSI Software ID:** 3bc8f1b6-1b44-4d82-85d9-3ea9d98fe848
**Repository:** https://github.com/space-physics/digital-meridian-spectrometer
**Source Revision:** 22924f707a4a3027e059a359695e69e4a80140c2
**Extraction Date:** 2026-08-29
**Validation Date:** 2026-08-29
**Validation Status:** PASS

---

## Scope note — read this before interpreting the tag and version evidence

This project changed its Python distribution name mid-history. Its first git tag, `v1.0`, versions a
predecessor distribution named `msp_aurora` living in a `msp_aurora/` package directory; the project
was subsequently renamed to `dmsp` and **restarted its version numbering on a lower series**, so the
second and newest tag is `v0.6.0`. Consequently the ordinary heuristics "highest tag wins" and
"lexically latest version wins" both give the **wrong** answer for this repository. Field 12 documents
the full evidence chain. Any future refresh that re-derives a version from tags alone will reproduce
the original error.

A second naming hazard runs through this record: the distribution name `dmsp` collides with the
Defense Meteorological Satellite Program acronym. Searching any catalogue, vocabulary, or literature
index for "DMSP" surfaces DMSP satellite instruments and, in the life sciences, the compound
dimethylsulfoniopropionate. None of those are related to this software. Search on the spelled-out
instrument name instead.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The bracketed placeholder is the catalogue convention for a record whose metadata was compiled from
public sources rather than supplied by the software's maintainer. It is not a missing value.

### 2. Persistent Identifier (RECOMMENDED)
**https://doi.org/10.5281/zenodo.596378**

This is the Zenodo **concept** DOI — the identifier that resolves to all versions. The DataCite record
for `10.5281/zenodo.596378` carries two `HasVersion` relations, to `10.5281/zenodo.167565` and
`10.5281/zenodo.1453766`, and both of those records carry the reciprocal `IsVersionOf` pointing back
to `596378`. The Zenodo API record for `1453766` states `conceptdoi: 10.5281/zenodo.596378` outright.

**Considered and rejected: `https://doi.org/10.5281/zenodo.167565`.** The README badge at the pinned
revision still points there (`[![image](https://zenodo.org/badge/DOI/10.5281/zenodo.167565.svg)]`),
which makes it the most visible DOI in the repository. It is nevertheless a *version* DOI — it carries
`IsVersionOf → 596378` — and it identifies the older of the two archived versions. A version DOI
belongs in Field 12, not here. The stale badge is a durable trap: it is the reason the earlier version
of this record described the 2016 release as current, and it will still be there for the next agent.

One DataCite quirk worth knowing so it is not misread as a contradiction: the concept record `596378`
reports its own `version` as `v0.6.0` and its own `issued` date as 2018-10-10, and its title is
`scivision/digital-meridian-spectrometer: Add matlab, update API`. A Zenodo concept record mirrors the
attributes of its newest version, so this is not a third release — it is independent corroboration
that v0.6.0 is the newest one.

### 3. Code Repository (MANDATORY)
**https://github.com/space-physics/digital-meridian-spectrometer**

Confirmed against the GitHub repository API on 2026-08-29 (`full_name: space-physics/digital-meridian-spectrometer`,
`created_at 2015-10-26T07:53:34Z`, `pushed_at 2024-03-21T13:58:49Z`, `default_branch main`,
`archived false`, `fork false`) and matching the PyHC registry's `code:` value for this package.

**Three historical locations still circulate in external metadata; none should be substituted here.**
All three were checked on 2026-08-29 and each returned HTTP 301 redirecting to the URL above:

| Historical URL | Where it still appears |
|---|---|
| `https://github.com/scienceopen/meridian-spectrometer-reader` | `setup.py` at tag `v1.0` (`url=`), and DataCite `167565`'s `IsSupplementTo` |
| `https://github.com/scivision/digital-meridian-spectrometer` | DataCite `1453766`'s and `596378`'s `IsSupplementTo` |
| `https://github.com/scivision/meridian-spectrometer-reader` | PyPI's `info.home_page` for `dmsp` 0.6.0, which came from `url =` in `setup.cfg` at tag `v0.6.0` — the earlier repository name under the author's later account handle, i.e. the window between the account rename and the repository rename |

Because those redirects still work, an agent re-deriving Field 3 from the DOI metadata rather than
from the live repository would record a stale-but-resolving URL. Prefer the canonical current URL.

### 4. Software Functionality (RECOMMENDED — treated as critical)

- **Data Processing and Analysis**
- **Data Processing and Analysis: Analysis**
- **Data Processing and Analysis: Calibration**
- **Data Processing and Analysis: Processing**
- **Data Visualization**
- **Data Visualization: 2D Graphics**
- **Data Visualization: Line Plots**
- **Data Visualization: Spectrogram**

All eight are rows in the `FunctionCategory` vocabulary, which held 83 values when checked on
2026-08-29; each subcategory is listed together with its parent, as the taxonomy requires.

**Evidence for each value**

- *Data Processing and Analysis* / *: Processing* — `src/dmsp/io.py::load()` opens a netCDF file,
  derives the observation date from the filename (a comment inside `load()` reads
  `# %% date from filename -- only way`), builds a datetime axis from the file's `Time` variable, subsets by a
  caller-supplied time window and elevation range, rejects unused and dead wavelength channels
  (`goodwl = wavelen > 1`, then `goodwl &= ~(Ipeak == 0).all(axis=(0, 2))` under the comment "root out
  bad channels 2011-03-01 for example"), and assembles an `xarray.Dataset` keyed by wavelength.

- *Data Processing and Analysis: Calibration* — **the value most easily missed.** `load()` reads the
  file's `FilterFactor` variable and applies it per wavelength channel:
  `R[w] = (("time", "elevation"), Ipeak[:, i, :] * filtfact[i].astype(float) / 128.0)`, under the
  comment "filter factor per wavelength Rayleigh/PMT * 128". This converts raw photomultiplier counts
  into calibrated Rayleighs, and the plot code labels the colour bars and figure axes "Rayleighs"
  accordingly. Converting raw instrument output to physical units using the instrument's own stored
  response factors is exactly what the Calibration subcategory describes. The same routine also
  contains the deliberate `.astype(float)` guard "critical to avoid overflow of int16 dtype!", which
  is a numerical-correctness step in that same conversion.

- *Data Processing and Analysis: Analysis* — the package's headline scientific product is the
  **emission-line intensity ratio**, a standard auroral diagnostic for the characteristic energy of
  precipitating electrons. `src/dmsp/plots.py::plotratio()` is a library entry point dedicated to it,
  and in `verbose` mode it additionally produces per-time-step ratio-versus-elevation profiles. The
  ratio itself is formed in the shipped driver `LoadMSPdata.py`
  (`ratio = Intensity[a.wl[0]] / Intensity[a.wl[1]]`), whose module docstring supplies recommended
  colour limits for the two canonical ratios: "`-r 1 2 3` is a starting point for 5577/4278 ratio" and
  "`-r 0.5 1 3` is a starting point for 6300/4278 ratio". The README advertises that driver
  ("LoadMSPdata.py creates many plots"). The arithmetic is one line only because xarray makes it one
  line; the derived quantity, its recommended scaling, and its dedicated renderer are all shipped.

- *Data Visualization* / *: 2D Graphics* — `plots.py::spectrasubplot()` draws
  `a.pcolormesh(dat.time, dat.elevation, dat[l].values.T, cmap="cubehelix_r", norm=LogNorm(...))`,
  one panel per wavelength, with log colour bars formatted by `LogFormatterMathtext`, inverted
  elevation axes, and optional gold fiducial lines at requested elevation angles.
  `MidpointNormalize` in the same module provides a diverging normalisation centred on a chosen ratio
  value for the ratio panel.

- *Data Visualization: Line Plots* — the `verbose` branch of `plotratio()` builds an `nrow × 4` grid
  and calls `ax.plot(ratio[:, i], ratio.elevation)` for each time step, titling each panel with its
  timestamp. `src/dmsp/ticks.py::timeticks()` exists solely to choose sensible major/minor time-axis
  locators across seven span regimes from under 30 seconds to two hours, with the warning "do NOT use
  'interval' or ticks are misaligned! use 'bysecond' only!".

- *Data Visualization: Spectrogram* — retained from the existing record. The package's public plotting
  entry point is `plotmspspectra()`; it renders the six photometer channels as stacked
  time-versus-elevation intensity images titled "Meridian Scanning Photometer: Peak Intensity", each
  panel labelled with its wavelength in nanometres and its emitting species. **Caveat for a future
  reader:** this is a wavelength-resolved intensity display, not a Fourier time-frequency transform.
  Nothing in the package computes a spectrogram in the signal-processing sense, which is why
  `Data Processing and Analysis: Spectrogram` is deliberately *not* selected below. The visualization
  value is kept because a user filtering for spectral-intensity displays should find this software.

**Considered and rejected, with reasons** (recorded so a later refresh does not re-propose them):

- *Data Processing and Analysis: Spectrogram* — no FFT, STFT, wavelet, or any other transform anywhere
  in the package. The "spectra" are six discrete interference-filter channels read straight from the
  file. See the caveat above.
- *Data Processing and Analysis: Data Access and Retrieval* — **there is no downloader.** `load()`
  takes a local `Path`, calls `Path(fn).expanduser()`, and opens it. The FTP and HTTP archives named
  in the README are where a human obtains the files; the software never fetches them. This is the one
  rejection most likely to be re-proposed, because Field 17 does legitimately record those archives as
  data sources — Field 17 asks what sources the software *supports*, Field 4 asks what the software
  *does*, and only the former is satisfied.
- *Data Processing and Analysis: Data Reduction* — `load()` subsets by time and elevation and drops
  dead channels. That is ordinary selection and quality masking, not averaging, binning, or
  downsampling, and treating every reader's slice arguments as data reduction would make the value
  meaningless.
- *Data Processing and Analysis: Time Series Analysis* — the data is time-ordered and windowed, and
  `ticks.py` adapts the time axis, but there is no temporal filtering, detrending, correlation, or
  spectral estimation.
- *Data Processing and Analysis: File Format Conversion* — the package reads netCDF into memory and
  writes no files at all (see Field 19). Read-only ingestion is not conversion.
- *Coordinate Transforms* and all six of its subcategories — tempting because `LoadMSPdata.py`'s
  docstring discusses magnetic zenith ("elevation from North Horizon, so to get near magnetic zenith
  at Poker Flat we use elevation angles FROM NORTH of 95-110 degrees corresponding to symmetric about
  77.5 elevation angle"). That is guidance printed for the user, not code: the elevation axis is
  literally `elv = np.arange(181.0)`, a plain degrees-from-north index, and the source comment records
  that "elevation is not stored anywhere in the data files". No geodetic, geomagnetic, or apex
  transform is computed.
- *Data Visualization: Movies* — figures are drawn and shown; there is no animation or frame export.
- *Mission-related* and *Models and Simulations* — this is a ground-based instrument reader; it models
  nothing and is not part of any mission ground system.
- *Servers and Environments* — no server, container, or parallel-execution component.

### 5. Related Region (RECOMMENDED — treated as critical)

- **Earth Atmosphere**
- **Earth Auroral Subregion**
- **Earth Ionosphere**
- **Earth Thermosphere**

All four are rows in the `Region` vocabulary, which held 24 values when checked on 2026-08-29.

**`Earth Magnetosphere` was removed from this field.** The subsection below records the reasoning on
both sides; the removal is settled.

**The physics that decides this field.** The instrument measures six fixed emission channels, and the
package's own `chem` mapping in `src/dmsp/plots.py` names the emitting species for each; the test
`test_mod.py` asserts the exact channel set `["4278","4861","5200","5577","6300","6700"]`:

| Channel | Species (`plots.py::chem`, with the two bracket-notation labels expanded) | Emission altitude |
|---|---|---|
| 427.8 nm | N₂⁺ 1N | ~100–120 km |
| 486.1 nm | Hβ (proton aurora) | ~105–120 km |
| 520.0 nm | [NI] | upper E region |
| 557.7 nm | `[OI]32` — the O I ¹S green line | ~100–150 km |
| 630.0 nm | `[OI]21` — the O I ¹D red line | ~200–300 km |
| 670.0 nm | N₂ 1P | ~100–120 km |

Every channel originates at or above roughly 100 km. That places the measured volume in the
**thermosphere** and in the ionospheric **E and F regions**, and the site — Poker Flat, at high
magnetic latitude, with magnetic zenith near 77.5° elevation per `LoadMSPdata.py` — places it in the
**auroral oval**.

- **Earth Auroral Subregion** — the most specific applicable region, and the strongest single value in
  this field. This is a meridian *scanning* photometer: it sweeps the magnetic meridian to resolve
  auroral arcs in latitude, and every product the package computes is an auroral emission quantity.
  A user filtering HSSI for auroral-region software should certainly get this record back.
- **Earth Ionosphere** — the 427.8/557.7/670.0 nm channels are E-region emissions and the 630.0 nm
  channel is an F-region emission; the intensity ratios the package renders are the classical
  ionospheric diagnostics of precipitating-electron energy. The PyHC registry independently classifies
  this package under `ionosphere_thermosphere_mesosphere`.
- **Earth Thermosphere** — the same altitudes, expressed in neutral-atmosphere terms; 630.0 nm in
  particular is a thermospheric emission whose long radiative lifetime makes it a thermospheric probe.
- **Earth Atmosphere** — kept deliberately. The `Region` vocabulary is **flat**: every row is
  top-level, with no parents and no children, so selecting `Earth Thermosphere` does *not* make a
  record findable under `Earth Atmosphere`. Dropping the coarse value would remove this software from
  a broad atmospheric search for no gain. This is the reason to keep it, and it is not an argument
  that the coarse value "covers" the fine ones — because the vocabulary is flat, no such
  encompassing relationship exists in either direction.

**Considered and rejected: `Earth Lower and Middle Atmosphere`.** The lower and middle atmosphere is
conventionally the troposphere, stratosphere, and mesosphere, up to roughly 85 km. No channel in the
table above emits from there. The package handles no mesospheric airglow features — no OH Meinel
bands, no Na 589 nm, no O₂ atmospheric bands — and the channel list is fixed and asserted in the test
suite, so this is not a gap that a future data file could fill. The PyHC keyword
`ionosphere_thermosphere_mesosphere` is a registry bucket spanning three regions, not evidence that
this instrument observes the mesosphere.

**Removed value — `Earth Magnetosphere` (previously held in this field).**

As recorded on 2026-08-29, HSSI held `Earth Atmosphere` and `Earth Magnetosphere` for this field. The
earlier version of this dossier justified the magnetospheric value as: "Auroral emissions are a
magnetospheric phenomenon; measurements at Poker Flat (high latitude) capture magnetosphere-ionosphere
coupling."

*The case for removal — the one adopted.* That justification is a causal-origin argument, not a
measurement argument. The software is a reader for a ground-based optical instrument; it neither
measures nor computes any quantity located in the magnetosphere. Its outputs are calibrated column
intensities and their ratios as a function of time and elevation angle — upper-atmospheric quantities.
Inferring a magnetospheric source population from them requires an inversion the software does not
perform. Applying the field's own sanity check: a scientist filtering HSSI for magnetospheric software
is looking for field models, particle-data tools, and ring-current or magnetotail analysis, and would
not expect a Poker Flat photometer netCDF reader in that result set. Meanwhile
`Earth Auroral Subregion` — which did not appear in the five-value list this record was originally
built against — is the vocabulary row that exists precisely to capture the ionospheric footprint of
magnetospheric precipitation, and it is now selected. Removing the coarser, weaker claim while adding
the precise one is a net gain in accuracy.

*The case for keeping it.* Meridian scanning photometer data is genuinely used by the
magnetosphere-ionosphere coupling community, and the 427.8/557.7/630.0 nm ratios this package renders
are used as proxies for the energy of the precipitating magnetospheric electron population. Because
the vocabulary is flat, removing the value removes this record from magnetospheric searches entirely.

*Outcome:* removed. It is a curator judgement about search reach rather than the correction of a
factual error, which is why both sides are recorded here — so the question is not re-litigated from
scratch, and so a future refresh does not restore the value by re-deriving the causal-origin
argument.

**Also considered and rejected:** the remaining eighteen `Region` rows. `Earth Inner Magnetosphere`,
`Earth Outer Magnetosphere`, `Earth Magnetotail`, and `Earth Magnetosheath` are finer magnetospheric
subdivisions and fail for the same reason as `Earth Magnetosphere`, more strongly. Every solar,
heliospheric, and planetary row (`Chromosphere`, `Corona`, `Photosphere`, `Solar Interior`,
`Solar Environment`, `Solar Wind`, `Interplanetary Space`, `Heliosheath`, `Planetary Magnetospheres`
and the five per-planet rows) is out of scope for a ground-based terrestrial auroral instrument.

### 6. Authors (MANDATORY)

#### Author 1
- **Author Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliations:**
  - **Boston University** — https://ror.org/05qwgg493
  - **Scivision, Inc.** — no identifier

**Sole authorship is established, not assumed.** `git shortlog -sne --all` over the pinned history
returns eight distinct identity strings — `scienceopen <scienceopen@users.noreply.github.com>`,
`Michael Hirsch, Ph.D <scivision@users.noreply.github.com>`,
`Michael Hirsch <scienceopen@users.noreply.github.com>`, `michael <hirsch617@gmail.com>`,
`scivision <scivision@users.noreply.github.com>`,
`Michael Hirsch <scivision@users.noreply.github.com>`, `Michael <scivision@users.noreply.github.com>`,
and `scivision <scivision@noreply.users.gitlab.com>` — all of which are GitHub/GitLab noreply or
personal addresses belonging to Michael Hirsch under his two long-standing handles (`scienceopen`, the
earlier one, and `scivision`, the later one). There is no `.mailmap` in the repository, which is why
the identities appear unmerged. There is no second contributor.

**The ORCID.** `https://orcid.org/0000-0002-1637-6526` resolves on the public ORCID API to Michael
Hirsch, with a single employment record: Boston University, department "ECE", role "Research
Scientist", start 2018-08, no end date. Note that the ORCID employment's own disambiguation source is
RINGGOLD 1846, not a ROR — the ROR below was resolved separately.

**Boston University's ROR.** `https://ror.org/05qwgg493`, confirmed as the `ror_display` name
"Boston University" via the ROR API. The DataCite record for `10.5281/zenodo.167565` gives the
affiliation string "Boston University" for this creator.

**Scivision, Inc. has no ROR, and this is a settled negative result — do not re-derive one.** The
affiliation string "SciVision, Inc." comes from the Zenodo/DataCite records `1453766` and `596378`.
A ROR API query for "scivision" returns exactly one organization: `https://ror.org/011qev639`,
"SciVision Biotech Inc. (Taiwan)", located in Kaohsiung, Taiwan. That is a biotechnology company and a
different legal entity from Michael Hirsch's US scientific-software consultancy. Attaching that ROR
would be a factual error. The identifier-less organization record is the correct representation.

**Recorded divergence: the stored organization label is spelled `Scivision, Inc.`** — lower-case "v" —
whereas the authoritative DataCite/Zenodo creator affiliation is `SciVision, Inc.`, and the company's
own usage capitalises the "V". This is a display-name defect in a shared organization record, not a
property of this software's metadata. It cannot be fixed by a routine metadata update: submitting a
differently-spelled organization name silently no-ops instead of renaming the record, and this
organization record is shared with other software entries, so a correction has to be applied directly
to the stored record and only after establishing what else references it. Recorded here so the
divergence is not mistaken for drift introduced by this refresh, and so a future agent does not spend
a cycle attempting the rename through the ordinary path.

**Considered and rejected: the DataCite name parse.** The creator block in `10.5281/zenodo.1453766`
and `10.5281/zenodo.596378` reads `name: "Michael Hirsch, Ph.D."` with `givenName: "Ph.D."` and
`familyName: "Michael Hirsch"` — Zenodo mis-split the postnominal as the given name. The stored
given/family pair `Michael` / `Hirsch` is correct and agrees both with ORCID and with the properly
parsed `nameType: "Personal"` creator in the older record `10.5281/zenodo.167565`
(`givenName: "Michael"`, `familyName: "Hirsch"`). Do not "reconcile" the correct stored name toward the
mis-parsed DOI metadata.

**No organization author.** No CITATION.cff, codemeta.json, or `.zenodo.json` exists at the pinned
revision, and no creator in any of the three DataCite records carries `nameType: "Organizational"`.

### 7. Software Name (MANDATORY)
**Digital Meridian Spectrometer**

The README's H1 heading is `# Digital Meridian Spectrometer`, and the PyHC registry entry (in
`_data/projects_unevaluated.yml`) uses `name: Digital Meridian Spectrometer`. Two independent
authoritative sources agree, and this is also the name already published, so it is preserved.

The **distribution/package** name is `dmsp` — `pyproject.toml` declares `name = "dmsp"`, the import is
`import dmsp`, and PyPI hosts the project as `dmsp`. That is a package identifier, not the software's
name.

**Considered and rejected: using `dmsp` as the software name.** It would collide head-on with the
Defense Meteorological Satellite Program, an unrelated and far more prominent use of the same
acronym in this very domain, and it is not the name either the README or PyHC presents to users.

**Considered and rejected: the DOI titles.** DataCite gives `Meridian Spectrometer Reader` for
`167565` and `scivision/digital-meridian-spectrometer: Add matlab, update API` for `1453766` and
`596378`. The first is the predecessor distribution's title (see the scope note); the second is a
GitHub-release headline auto-generated by the Zenodo integration, not a software name.

### 8. Description (MANDATORY)

> Load and plot UAF Geophysical Institute Digital Meridian Spectrometer data from Poker Flat Research
> Range. The software handles spectral data from a ground-based meridian scanning photometer that
> measures auroral emissions at multiple wavelengths, including 427.8 nm N2+, 486.1 nm H-beta,
> 520.0 nm [NI], 557.7 nm [OI], 630.0 nm [OI], and 670.0 nm N2. It supports both historical NetCDF3
> format .PF files from 1983-2010 and current NetCDF4 format .NC files from 2011-present. The software
> provides data loading functions that return xarray.Dataset objects with time-elevation-intensity
> arrays, along with visualization capabilities including spectrograms and line plots. The library
> includes both Python and MATLAB interfaces.

Preserved as published. Every factual claim in it was re-checked against the pinned revision and holds:

- the six wavelength/species pairs match `src/dmsp/plots.py::chem` exactly (4278 → N₂⁺ 1N, 4861 → Hβ,
  5200 → [NI], 5577 → [OI], 6300 → [OI], 6700 → N₂ 1P) and the channel set matches the assertion in
  `src/dmsp/tests/test_mod.py`;
- the netCDF3/netCDF4 and date-range claims match the `load()` docstring — "This function works with
  1983-2010 netCDF3 as well as 2011-present netCDF4 files" — and the README's data-source list, and
  the `.PF` / `.NC` suffix branches in `load()`;
- `load()` is annotated `-> xarray.Dataset` and returns a Dataset with `time` and `elevation`
  coordinates;
- the MATLAB interface is `matlab/dmsp.m` plus the worked example `matlab/PlotDMSP.m`.

The upstream one-liners are shorter and less informative — `pyproject.toml` has "Load and plot UAF
Geophysical Institute Digital Meridian Spectrometer data", the README subtitle has "For Geophysical
Institute's Poker Flat Digital Meridian Spectrometer, which uses NetCDF", the GitHub repository
description has the shorter, differently-cased "for Poker Flat Digital Meridian Spectrometer, which
uses netCDF" (the two are not the same string — the GitHub text omits the "Geophysical Institute's"
clause), and PyHC has "UAF Digital Meridian Spectrometer-- load and plot". None of them would improve
on the text above, and rewriting settled prose for style is not an improvement.

### 9. Concise Description (OPTIONAL)

> Load and plot UAF Geophysical Institute Digital Meridian Spectrometer data from Poker Flat, with
> NetCDF3/4 auroral spectral measurements.

137 characters, within the 200-character limit. Preserved as published.

An earlier draft of this dossier carried a longer variant ending "...from Poker Flat Research Range,
supporting NetCDF3/4 formats with auroral spectral measurements." The published text above is the
value that was actually curated into the record and is retained; the difference is purely stylistic.

### 10. Publication Date (RECOMMENDED)
**2015-10-26**

The date the software first became public. Two independent sources agree: the GitHub repository API
reports `created_at: 2015-10-26T07:53:34Z`, and the first commit in the pinned history,
`21229e95761bcf652a098fd0b37b424fc76a16c1` ("Initial commit"), is dated 2015-10-26 03:53:34 -0400 —
the same instant expressed in local time.

**Considered and rejected: 2016-11-20**, the `Issued` date on DataCite `10.5281/zenodo.167565`, i.e.
the first archived release. Field 10 asks for date of first publication, and the code was publicly
available in this repository for over a year before it was first archived to Zenodo. Also note that
2016-11-20 differs from the 2016-11-06 date previously stored in Field 12 — see Field 12 for why.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

`attributes.publisher` is "Zenodo" on all three DataCite records, and the DOIs were minted through the
GitHub–Zenodo release integration (each version record carries an `IsSupplementTo` pointing at a
GitHub `/tree/<tag>` URL, the integration's signature). The field guidance names Zenodo as the correct
entry for exactly this case.

### 12. Version (RECOMMENDED) — **the version anomaly**

#### Latest released version
- **Version Number:** v0.6.0
- **Version Date:** 2018-10-10
- **Version Description:** Simplify "load" API like many other of our programs. Create Matlab API and plots
- **Version PID:** https://doi.org/10.5281/zenodo.1453766

**What was previously recorded, and why.** As recorded on 2026-08-29, HSSI held
`v1.0` / 2016-11-06 / `https://doi.org/10.5281/zenodo.167565`, with the description "for Poker Flat
Digital Meridian Spectrometer, which uses netCDF". That triple is internally consistent and every one
of its parts is real. It is nevertheless not the software's latest release, and the reasoning below is
recorded in full because the mistake is a *reasonable* one that will be made again by any agent that
does not read this section.

**Why `v1.0` looked right.** Four signals point at it, and they agree with each other:

1. It is a genuine git tag in this repository — `v1.0` → commit `99ccd09`, dated 2016-11-06 15:40:56 -0500.
2. It is the **lexically highest** of the repository's two tags, and "1.0" reads as a mature release.
3. It has a real, resolvable Zenodo DOI, `10.5281/zenodo.167565`, whose DataCite record states
   `version: "v1.0"`.
4. That DOI's abstract, "for Poker Flat Digital Meridian Spectrometer, which uses netCDF", is
   **word-for-word** the repository's own GitHub description as read on 2026-08-29. Nothing about it
   looks stale.

**Why it is nevertheless wrong.** The tag versions a *different distribution*. Inspecting the tree at
`v1.0` shows:

- the package directory is `msp_aurora/`, not `dmsp/`;
- `setup.py` declares `name='msp_aurora'`, `description='MSP Aurora Spectrometer Reader netCDF4 /
  netCDF3'`, and `url='https://github.com/scienceopen/meridian-spectrometer-reader'`;
- `README.rst` is titled "meridian-spectrometer-reader";
- the dependency set is `pathlib2`, `histutils`, `isrutils` — none of which the current package uses.

The project was subsequently renamed to `dmsp` and **restarted its version numbering on a lower
series**. At the second tag, `v0.6.0` → commit `972399a`, dated 2018-10-10 02:20:53 -0400, the tree
contains `dmsp/` and a `setup.cfg` reading `name = dmsp`, `version = 0.6.0`. So the version sequence
across the repository's history is non-monotonic by design, and the "highest tag" heuristic selects a
release of the predecessor package. `msp_aurora` was never published to PyPI at all — the PyPI JSON
API returns 404 for both `https://pypi.org/pypi/msp_aurora/json` and
`https://pypi.org/pypi/msp-aurora/json`.

Two further details confirm the same conclusion:

- The DOI that Zenodo assigned to `v1.0`, `10.5281/zenodo.167565`, is titled "Meridian Spectrometer
  Reader" and its `IsSupplementTo` points at
  `https://github.com/scienceopen/meridian-spectrometer-reader/tree/v1.0` — the predecessor's name and
  the predecessor's tag.
- The previously stored release date, 2016-11-06, is the **commit date of the lightweight `v1.0` tag**,
  not the date of the release it was paired with: DataCite reports `10.5281/zenodo.167565` as
  `Issued` on **2016-11-20**. So the stored triple did not internally agree with its own DOI record.

**Why v0.6.0 is the latest release — four independent corroborations, all checked 2026-08-29.**

1. **Git.** `v0.6.0` → `972399a`, commit date 2018-10-10 02:20:53 -0400. It is the newest of the
   repository's two tags by date.
2. **GitHub Releases API.** Exactly one release exists for this repository: tag `v0.6.0`, name
   "Add matlab, update API", `published_at 2018-10-10T06:24:30Z`, not a draft and not a prerelease.
3. **PyPI.** The JSON API at `https://pypi.org/pypi/dmsp/json` reports `info.version: 0.6.0` and a
   single entry in `releases`: `dmsp-0.6.0.tar.gz`, uploaded 2018-10-10T06:26:47. (The PyPI *HTML*
   project page is not usable as evidence here — it returns 200 behind a bot gate even for packages
   that do not exist. Only the JSON or Simple API distinguishes presence from absence.)
4. **DataCite.** `10.5281/zenodo.1453766` states `version: "v0.6.0"`, `Issued 2018-10-10`, and
   `IsSupplementTo https://github.com/scivision/digital-meridian-spectrometer/tree/v0.6.0`. The
   concept record `10.5281/zenodo.596378` mirrors those same attributes, as a Zenodo concept record
   does for its newest version.

All four agree on the date 2018-10-10.

**Why the untagged `__version__ = "1.0.0"` at HEAD is also not a candidate.**
`src/dmsp/__init__.py` at the pinned revision declares `__version__ = "1.0.0"`. That line entered the
tree on 2024-03-20 in commit `2a98a78` ("use pyproject.toml"), whose purpose was migrating packaging
metadata: `pyproject.toml` sets `version = {attr = "dmsp.__version__"}`, so setuptools' dynamic-version
hook needed an attribute to read, and one was supplied. It was never tagged, never uploaded to PyPI
(which still shows only 0.6.0), never assigned a DOI, and has no GitHub release. Field 12 asks for the
latest *released* version; an in-tree version string that no release artifact corresponds to is a
development placeholder, not a release. It is also the single most likely wrong answer for a future
agent, because it is the only version string visible in the source at HEAD and it happens to be
numerically the largest — a coincidence, since `1.0.0` here echoes the predecessor's `v1.0` rather
than continuing the `0.6.0` series. Should the maintainer ever cut an actual 1.0.0 release, that
release — not the source string — would become this field's value.

**Version description — source and alternative.** The description recorded above is the abstract of
DataCite `10.5281/zenodo.1453766`: `Simplify "load" API like many other of our programs. Create Matlab
API and plots`. It is a genuine changelog summary and matches what the release contains (the `load()`
API simplification and the addition of `dmsp.m`/`PlotDMSP.m`). The alternative is the GitHub release
name, "Add matlab, update API"; it says the same thing more tersely and was rejected only for being
less informative. The repository has no CHANGELOG.md.

**Version number form.** `v0.6.0` with the leading `v`, matching the git tag, the GitHub release tag,
and DataCite's `version` attribute, and matching the `v`-prefixed style already used in this record.
PyPI and `setup.cfg` at that tag both give the bare `0.6.0`; the difference is only the prefix.

**Do not copy the rendered version string.** HSSI's read-only view applies a display transform that
prefixes the software name onto whatever version is stored: as recorded on 2026-08-29, with `v1.0`
then stored, that view rendered the version as "Digital Meridian Spectrometer - v1.0". The stored
version number is always the bare string, and the prefixed form must never be copied back into this
field — whichever version is current.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x**
- **MATLAB**

Both are rows in the `ProgrammingLanguage` vocabulary, which held 19 values when checked on
2026-08-29. The GitHub language statistics for this repository reported exactly two languages on that
date, Python (13,378 bytes) and MATLAB (1,718 bytes), and the pinned tree contains exactly the
corresponding files: five `.py` files under
`src/dmsp/` plus the `LoadMSPdata.py` driver, and `matlab/dmsp.m` plus `matlab/PlotDMSP.m`.

`pyproject.toml` sets `requires-python = ">=3.8"` and the CI matrix in `.github/workflows/ci.yml`
tests Python 3.8 and 3.12, so `Python 3.x` is correct and `Python 2.x` is not applicable — the source
uses `from __future__ import annotations` with PEP 604 union syntax (`tuple[datetime, datetime] | None`),
which cannot run on Python 2.

Note the exact vocabulary spellings if this field is ever edited: the rows are `Javascript` and
`Typescript` (not the camel-cased forms). Neither applies here.

### 14. Reference Publication (OPTIONAL)
**Not found.**

This is a searched negative, not an unexamined gap:

- The pinned tree contains no `CITATION.cff`, no `codemeta.json`, no `.zenodo.json`, and no `CITATION`
  file of any kind. The README has no "how to cite" section — its only badges are the Zenodo DOI, the
  CI status, and PyPI download statistics.
- None of the three DataCite records carries an `IsDescribedBy`, `IsDocumentedBy`, or `Cites` relation;
  their `relatedIdentifiers` contain only the GitHub `IsSupplementTo` links and the concept/version
  `HasVersion` / `IsVersionOf` pairs.
- ADS/SciX full-text search finds no paper describing this software; see Field 27 for the searches run
  and the one near-miss they surfaced.
- Semantic Scholar has no record at all for either version DOI or the concept DOI
  (`DOI:10.5281/zenodo.596378` and `DOI:10.5281/zenodo.1453766` both return "Paper ... not found"), so
  there is no citation graph to mine.

There is no JOSS paper and no instrument paper offered by the authors as the software's citation.

### 15. License (RECOMMENDED)
- **License:** Apache License 2.0
- **License URI:** https://spdx.org/licenses/Apache-2.0

`Apache License 2.0` is a row in the `License` vocabulary, which held 11 values when checked on
2026-08-29; the URI above is the one that vocabulary row carries, so recording it avoids a spurious
difference against the auto-populated SPDX value.

Evidence: `LICENSE.txt` at the pinned revision carries the Apache License, Version 2.0 terms — 176
lines opening "Apache License / Version 2.0, January 2004 / http://www.apache.org/licenses/" and
closing at "END OF TERMS AND CONDITIONS". (The optional "APPENDIX: How to apply the Apache License to
your work" boilerplate is not included, which is normal and does not affect the licence identity.) The
GitHub repository API independently reports
`license: {key: apache-2.0, spdx_id: Apache-2.0, name: "Apache License 2.0"}`.

**Licence history — why two other answers exist in the record and are both wrong today.**

- **AGPL-3.0 (superseded).** From the initial commit on 2015-10-26 the repository carried a `LICENSE`
  file containing the GNU Affero General Public License v3. Commit `458f51b` ("meta", 2020-02-19)
  deleted that 662-line file and added the 176-line `LICENSE.txt` Apache-2.0 text in the same commit.
  Anything derived from the repository before 2020-02-19 — including the state at both release tags —
  will say AGPL. It is history, not the current licence.
- **MIT (never accurate).** `setup.cfg` at tag `v0.6.0` carried the classifier
  `License :: OSI Approved :: MIT License` while the repository's `LICENSE` file at that same tag was
  AGPL-3.0. The two contradicted each other at the time; both have since been removed. Neither is the
  current licence, and the MIT classifier should not be resurrected from the release metadata.
- **Zenodo's "other-open" (uninformative).** The Zenodo API record for `1453766` reports
  `license: {id: "other-open"}` and DataCite's `rightsList` only says "Open Access". Zenodo captured
  the repository's licence state as of 2018, before the Apache relicensing, and did so imprecisely.
  Do not derive this field from the DOI metadata; derive it from the repository.

**Trap for a future editor:** the `License` vocabulary's LGPL-version-2 row uses typographic quotes
(`‘Lesser’`), and matching is exact after a bare strip. Not relevant to this record's value, but
relevant to anyone editing this field by hand.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- aurora
- auroral emissions
- geophysical-institute
- ionosphere_thermosphere_mesosphere
- matlab-python-interface
- netcdf
- poker-flat-research-range
- python
- spectrograph
- spectrometer

Recorded lower-case, one keyword per entry. (HSSI's read-only view title-cases keywords for display —
"Aurora", "Netcdf", "Ionosphere_Thermosphere_Mesosphere". That is a rendering transform; the stored
values are the lower-case forms above, and the title-cased forms must never be copied back.)

This set is already the union of every source available:

- **GitHub repository topics** (seven): `aurora`, `geophysical-institute`, `matlab-python-interface`,
  `netcdf`, `poker-flat-research-range`, `python`, `spectrograph`;
- **`pyproject.toml`** `keywords = [ "aurora", "spectrograph" ]` — a subset of the topics;
- **PyHC registry** `keywords: ["ionosphere_thermosphere_mesosphere", "specific"]`;
- plus two curator additions, `auroral emissions` and `spectrometer`, both accurate.

**Considered and rejected: the PyHC keyword `specific`.** It is a registry-internal classification
marker used across many PyHC entries to indicate a narrowly-scoped package; it carries no science
meaning and would be noise as a search keyword.

**Considered and rejected: adding `photometry`, `airglow`, `auroral optical emissions`, `thermosphere`,
`ionosphere`.** All five already existed as rows in the open Keyword vocabulary when it was checked on 2026-08-29, so
adding any of them would be cheap. They were rejected on substance rather than availability: `auroral optical emissions`
is a near-duplicate of the stored `auroral emissions` and would fragment matching; `airglow` describes
a phenomenon this instrument's six channels do not target; and `thermosphere` / `ionosphere` duplicate
information now carried precisely by Field 5. `photometry` is the closest call — the instrument is a
photometer and its output is calibrated in Rayleighs — but no source in the repository, PyPI, GitHub,
or PyHC uses the term, so adding it would be taste rather than evidence.

### 17. Data Sources (OPTIONAL)

- **FTP/FTPS Directories**
- **HTTP/HTTPS Directories**
- **Observatory/Mission-specific**

All three are rows in the `DataInput` vocabulary, which held 17 values when checked on 2026-08-29.

The README's "Data sources" section is the authority for this field, and it lists four locations:

| README entry | Verified 2026-08-29 | Maps to |
|---|---|---|
| `ftp://optics.gi.alaska.edu/PKR/DMSP/NCDF/` (2011–present) | not independently verified — see below | FTP/FTPS Directories |
| `ftp://optics.gi.alaska.edu/PKR/DMSP` | not independently verified — see below | FTP/FTPS Directories |
| `http://optics.gi.alaska.edu/realtime/data/msp/pkr` (1983–2010 `.PF`) | HTTP 403 | dead; see below |
| `http://optics.gi.alaska.edu/realtime/data/archive/PKR_MSP_X/` ("other dates") | HTTP 200, serves an Apache directory index of 192 distinct `MSP_YYYYDDD.PF` files (`MSP_2005001.PF` … `MSP_2011064.PF`) | HTTP/HTTPS Directories |

The `http://` scheme in the last row is the README's own spelling, quoted here as written. Field 28
records the same archive directory under the `https://` scheme that resolves live, and explains why
the two spellings are deliberately left unreconciled.

**Why `HTTP/HTTPS Directories` belongs here.** The archive index above is live, is linked
from the README as a supported source of data, and serves files in exactly the naming convention that
`src/dmsp/io.py::load()` parses: for a `.pf` suffix it reads the year from `fn.stem[4:8]` and the
day-of-year from `fn.stem[8:11]`, which is precisely the `MSP_YYYYDDD.PF` layout of the served files.
An HTTP directory of files the software is written to read is an HTTP data source by the same reasoning
that already justifies the stored FTP value.

**Why `Observatory/Mission-specific` is correct.** Every archive above belongs to one observatory —
the University of Alaska Fairbanks Geophysical Institute optical archive at Poker Flat. The field
guidance requires that when this value is selected the observatory be named in Field 32, and it is.

**Two caveats to record rather than hide.**

- The README itself states that the 1983–2010 HTTP path "was good for years and we used this data, but
  in late 2018 it stopped working." A check on 2026-08-29 found `http://optics.gi.alaska.edu/realtime/data/msp/pkr`
  redirecting to HTTPS and returning 403, consistent with the README's own note. The host is otherwise
  healthy (`https://optics.gi.alaska.edu/` returns 200). The `.PF` files that path used to serve are
  reachable through the `PKR_MSP_X` archive index instead, which is why the format support in Field 18
  is unaffected.
- The FTP endpoints could not be independently confirmed from this machine: a TCP connection to port 21
  on `optics.gi.alaska.edu` did not complete within a 15-second timeout. **That result does not
  establish that FTP is down** — it is equally consistent with outbound FTP being blocked on the
  testing network, which is common. The `FTP/FTPS Directories` value rests on the README's explicit
  documentation of those paths, which is the appropriate basis for this field, and it should not be
  removed on the strength of an inconclusive connection test.

**Considered and rejected:** the remaining fourteen `DataInput` rows. `CDAWeb`, `SSCWeb`, `OMNIWeb`,
`HAPI`, `das2`, `AMDA`, `Madrigal`, `VirES`, `GFZ`, `WDC`, `TAP`, `The Virtual Solar Observatory.`, and
`S3/Cloud-aware` name services and protocols this software has no code path to and no documentation
mentioning. `Other` is unnecessary because every documented source maps onto a specific row above.

### 18. Input File Formats (RECOMMENDED)
- **netCDF3/4**

`netCDF3/4` is a row in the `FileFormat` vocabulary, which held 11 values when checked on 2026-08-29.
`src/dmsp/io.py` imports
`from netCDF4 import Dataset` and opens files with `with Dataset(fn, "r") as f:`, reading the
variables `Time`, `Wavelength`, `PeakIntensity`, and `FilterFactor`. The `load()` docstring states it
"works with 1983-2010 netCDF3 as well as 2011-present netCDF4 files", and the function branches on the
file suffix — `.nc` files carry the date at `fn.stem[13:21]` in `%Y%m%d` form (the netCDF4 era, e.g.
the bundled test file `PKR_SMSP_STD_20141011.NC`), while `.pf` files carry year and day-of-year at
`fn.stem[4:8]` and `fn.stem[8:11]` (the netCDF3 era, e.g. `MSP_2007082.PF`). The single HSSI row
covers both generations.

**Considered and rejected:** the other ten rows. Nothing in the package reads `ascii`, `CDF`, `csv`,
`FITS`, `HDF5`, `IDL.sav`, `JSON`, or `Zarr`; `ISTP-Compliant` describes a CDF metadata convention that
does not apply to these files; and `Other` is unnecessary since netCDF3/4 covers everything read.

### 19. Output File Formats (RECOMMENDED)
**Not found — the software writes no files, and this emptiness is a verified property.**

A search of every `.py` and `.m` file at the pinned revision for `savefig`, `to_netcdf`, `to_csv`,
`.write`, and file opens in write mode returns nothing. The plotting functions build matplotlib
figures in memory (`figure(figsize=(20, 12))` in three places in `src/dmsp/plots.py`) and the driver
`LoadMSPdata.py` ends with a bare `show()` — an interactive display call. There is no export path, no
output-directory argument in the CLI, and no serialization of the returned `xarray.Dataset`.

The software's outputs are an in-memory `xarray.Dataset` and on-screen figures. Neither is a file
format. Recording any value here — including `Other` — would assert a capability the software does not
have.

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Operating System Independent**

Both are rows in the `OperatingSystem` vocabulary, which held 7 values when checked on 2026-08-29.

`Linux` is the directly evidenced value: `.github/workflows/ci.yml` runs its matrix on
`os: [ubuntu-latest]` with Python 3.8 and 3.12, executing `flake8`, `mypy`, and `pytest`.
`Operating System Independent` records the broader claim, which the code supports: the package is pure
Python with no platform-conditional branches, no compiled extensions of its own, no subprocess calls,
and no OS-specific paths — it uses `pathlib.Path` with `.expanduser()` throughout. The MATLAB bridge
in `matlab/dmsp.m` calls the Python package through MATLAB's `py.` interface and `pyenv`, which is
available on all three MATLAB platforms.

**Considered and rejected: adding `Mac` and `Windows` explicitly.** Both would very likely work, but
the CI matrix exercises neither, and `Operating System Independent` already makes the cross-platform
claim without asserting a specific platform that has never been tested. Note that a repository-history
detail could mislead here: `.appveyor.yml` (a Windows CI configuration) existed at tag `v0.6.0` but is
absent from the pinned tree, so there is no *current* Windows testing evidence.

**Trap:** the vocabulary row is `Operating System Independent` spelled out in full. `OS Independent` is
not a value and would be rejected.

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**

`CPU Independent` is a row in the `CpuArchitecture` vocabulary, which held 9 values when checked on
2026-08-29. The package contains no
architecture-specific code, no SIMD intrinsics, no assembly, and no compiled extension of its own; its
numerical work is elementwise arithmetic on NumPy arrays. Nothing constrains it to a particular
architecture beyond the availability of its dependencies. `GPU` and `HPC or HEC` do not apply — there
is no accelerator code and no parallel-execution component.

### 22. Related Phenomena (OPTIONAL)
**Not found — correctly empty, and this is a vocabulary limitation rather than a gap in the software.**

The `Related Phenomena` vocabulary is **closed** and held seven rows in total when checked on
2026-08-29: `Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`,
`Solar Flares`, `Solar Wind`, and `X-ray emission`. Six are solar or heliospheric and have no bearing on a ground-based terrestrial
auroral photometer. The seventh, `Geomagnetic Storms`, was considered and rejected: this software
reads and plots meridian scanning photometer data for any interval a user supplies — quiet-time,
substorm, and storm-time alike — and implements no storm identification, indexing, or storm-specific
analysis. Selecting it would assert a specialisation the code does not have.

The phenomenon this software genuinely supports is **aurora**, which has no row in this vocabulary.
The field guidance is explicit that a phenomenon without a row belongs in Keywords, and it is there:
`aurora` and `auroral emissions` are recorded in Field 16. The API rejects any value not in the
seven-row list, so free-typing "Aurora" here is not an available option — the previous version of this
dossier proposed the free-text values "Auroral emissions" and "Atmospheric optical emissions", neither
of which exists as a row; they would have been rejected on submission.

### 23. Development Status (RECOMMENDED)
**Inactive**

`Inactive` is a row in the `RepoStatus` vocabulary, which held 8 values when checked on 2026-08-29.
As recorded on 2026-08-29, HSSI held no value for this field.

Reasoning against the repostatus.org definitions the vocabulary is built from, as of 2026-08-29:

- **Inactive** — "reached a stable, usable state but is no longer being actively developed; support may
  be provided as time permits." This fits. The package reached a stable usable state: it has a tagged
  release, a PyPI distribution, an archival DOI, a passing CI configuration, and a test that exercises
  the public API against a bundled data file. Development then stopped: the most recent commit in the
  pinned history is `22924f7` ("matlab works again") dated 2024-03-21, and the GitHub API's
  `pushed_at` of 2024-03-21T13:58:49Z confirms nothing has been pushed since — roughly two years and
  five months of quiescence as of today. The March 2024 burst itself (five commits over two days:
  migrating to `pyproject.toml`, refreshing the CI Python matrix, fixing a matplotlib `norm` syntax
  change, and repairing the MATLAB bridge) reads as maintenance to keep an existing package working,
  not feature development.
- **Active** — rejected. It requires "being actively developed", which two and a half years of silence
  contradicts. The previous version of this dossier recorded `Active` on the basis of "recent commit in
  2024-03-21" and the presence of CI. That was defensible when written but is no longer: what counts
  as "recent" moved, and a configured CI workflow indicates maintenance hygiene rather than ongoing
  development.
- **Unsupported** — rejected. It requires that "the authors have ceased work" and typically that a new
  maintainer is wanted. There is no such declaration anywhere: the repository is not archived
  (`archived: false`), carries no deprecation notice, and the README makes no statement about the
  project's future. Absence of commits is not a declaration of abandonment.
- **Abandoned**, **WIP**, **Concept** — all rejected because each presupposes the project never reached
  a stable public release, which a PyPI distribution and a DOI-archived release refute.
- **Suspended** — rejected; it requires an expressed intent to resume, which is absent.
- **Moved** — rejected. The repository has moved twice in the *hosting* sense
  (`scienceopen/meridian-spectrometer-reader` → `scivision/digital-meridian-spectrometer` →
  `space-physics/digital-meridian-spectrometer`), which could invite this value by mistake. The
  repostatus term means the *project* now lives elsewhere and that other location is authoritative.
  Here the redirects all resolve *to* the current repository, so this location is the authoritative
  one.

This value is time-sensitive. If a future refresh finds new commits, `Active` becomes correct again;
if the repository is archived or a deprecation notice appears, `Unsupported` does.

### 24. Documentation (RECOMMENDED)
**https://github.com/space-physics/digital-meridian-spectrometer**

There is no separate documentation site, and that is a verified absence rather than an unsearched one:
the pinned tree contains no `docs/` directory, no `.readthedocs.yml` or `.readthedocs.yaml`, and no
Sphinx or MkDocs configuration; the GitHub API reports `has_pages: false` and `homepage: null`; and and the
PyHC registry entry for this package has no `docs:` key. That absence is a property of this entry
rather than of the registry format: the schema does support the key, and a sibling entry in the same
file by the same author uses it (MSISE-00 carries
`docs: https://ccmc.gsfc.nasa.gov/modelweb/models/nrlmsise00.php`). The DASCutils entry in that file
does not — it carries a `logo:` key but no `docs:`.

The README is the documentation, and it is genuinely sufficient for a package this size: it states the
purpose, lists the four data-source URLs with their date coverage, gives the install command
(`python -m pip install -e .`), shows the module usage (`import dmsp; dat = dmsp.load('~/data/myfile.PF')`),
links the returned type to the upstream `xarray.Dataset` API page, points at `LoadMSPdata.py` for
plotting, and notes the MATLAB entry point. The field guidance explicitly allows the access URL to be
reused here when they are the same.

### 25. Funder (OPTIONAL)
**Not found.**

Searched and absent, not merely unfilled:

- `fundingReferences` is an empty array on all three DataCite records (`596378`, `167565`, `1453766`).
- The pinned tree contains no acknowledgements text of any kind — no `ACKNOWLEDGMENTS`, no funding
  section in the README, no grant number in any source file, and no `.github/FUNDING.yml`.
- The usual best source for this field is the reference publication's Acknowledgments section, and
  there is no reference publication (Field 14).
- The one paper that mentions this instrument (Field 27) does not acknowledge the software, so its
  acknowledgements would not attribute this software's funding even if read.

The absence is plausible on its face: the author's affiliations across the release history are Boston
University and his own consultancy, SciVision, Inc., and small independently-developed instrument
readers frequently carry no separate award.

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
- **Award Number:** Not found

Same evidence as Field 25. With no funder identified and no acknowledgements or funding metadata
anywhere in the repository or the DOI records, there is no award to record.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Not found — with one near-miss that must not be added.**

**Negative research, so this is not re-run from scratch.** Full-text searches through ADS/SciX
(authenticated with an anonymous bootstrap token, and validated with a nonsense-string control that
correctly returned zero results):

| Query | Result |
|---|---|
| `full:"meridian-spectrometer-reader"` | 0 |
| `full:"space-physics/digital-meridian-spectrometer"` | 0 |
| `full:"zenodo.596378"` | 0 |
| `full:"zenodo.1453766"` | 0 |
| `full:"zenodo.167565"` | 0 |
| `ack:"digital-meridian-spectrometer"` | 0 |
| `author:"Hirsch, Michael" full:"meridian scanning photometer"` | 0 |

No paper cites the software's DOIs, its repository slug, or its former name. Semantic Scholar likewise
has no record for either version DOI or the concept DOI, so there is no citation graph.

**The near-miss — do not record `10.1029/2020JA028505` here.** `body:"digital-meridian-spectrometer"`
returns exactly one paper: Liang, Zou, Nishimura, Donovan, Spanswick & Conde (2021), "Neutral Wind
Dynamics Preceding the STEVE Occurrence and Their Possible Preconditioning Role in STEVE Formation",
*JGR Space Physics*, bibcode `2021JGRA..12628505L`. It looks at first like a citing paper. It is not,
and the disambiguation is worth keeping:

- ADS tokenizes hyphens as spaces, so the hyphenated query is really a phrase search for
  "digital meridian spectrometer". Searching the same bibcode for the *unhyphenated* phrase
  `body:"digital meridian spectrometer"` returns the same single hit, confirming the match is on the
  **instrument name in prose**, not on a repository slug.
- The same bibcode returns **zero** for `body:"github"`, `body:"scivision"`, and `body:"Hirsch"`. A
  paper citing this software would contain at least one of them.
- It does return hits for `body:"Poker Flat"` and `body:"optics.gi.alaska.edu"`, i.e. it uses Poker
  Flat optical data and points at the UAF archive — which is a citation of the *instrument and its
  data*, not of this reader.

So the paper is evidence that the instrument is used in the literature, and no evidence at all that
this software is. Adding it would misattribute a data citation as a software citation.

**Beware one more search artifact:** `full:"dmsp.load"` returns fourteen results dominated by
biochemistry papers about dimethylsulfoniopropionate. The `dmsp` token is unusable as a literature
search term.

### 28. Related Datasets (OPTIONAL)

- **ftp://optics.gi.alaska.edu/PKR/DMSP/**
- **https://optics.gi.alaska.edu/realtime/data/archive/PKR_MSP_X/**

Both are UAF Geophysical Institute Poker Flat optical archive locations documented in the README, and
both are the data this software exists to read. Neither has a DOI; there is no DOI-registered dataset
for the Poker Flat DMS that the repository, the DOI metadata, or the PyHC entry points to, so
permanent archive URLs are used as the field's guidance allows.

The stored FTP entry corresponds to the README's "FTP: ftp://optics.gi.alaska.edu/PKR/DMSP" line and
covers the netCDF4 era (`.../PKR/DMSP/NCDF/`, 2011–present).

**Why the HTTPS archive index is a second entry and not a duplicate.** It is a genuinely different holding, not
a duplicate access path: verified on 2026-08-29 to return HTTP 200 and to serve an Apache index of 192
distinct `MSP_YYYYDDD.PF` files, running from `MSP_2005001.PF` to `MSP_2011064.PF` as indexed on that
date — i.e. the netCDF3-era `.PF` data whose original README location has returned 403 since late 2018. Field 18 records that this software reads those `.PF` files
and `src/dmsp/io.py` parses exactly that filename convention, so the archive that still serves them is
a related dataset. It is also the *verifiable* half of the pair, given that FTP reachability could not
be confirmed from this machine (see Field 17).

Recording two entries rather than one is deliberate. The two paths serve different data eras — the
FTP path the netCDF4 era, the HTTPS index the netCDF3 `.PF` era — so collapsing them to a single entry
would drop a holding this software is written to read.

**The `http://` and `https://` spellings of the archive are both deliberate.** Field 17 quotes the
README verbatim in its "README entry" column, and the README writes the archive directory as
`http://optics.gi.alaska.edu/realtime/data/archive/PKR_MSP_X/`; this field records the `https://`
form, which is the scheme verified live on 2026-08-29 — the `http://` form redirects to it — and is
therefore the URL that works for a user following the record. Each is correct where it stands, and
neither should be rewritten to match the other. This matters beyond tidiness because in HSSI a
related item's `name` *is* its `identifier`: one string serves both roles, so "correcting" a scheme
does not retype an existing entry, it mints a second one pointing at the same UAF archive directory.
As observed on 2026-08-29, HSSI held no stored dataset entry for this software at either spelling, so
a later refresh that harmonises the two schemes would be manufacturing a duplicate holding rather
than repairing one.

### 29. Related Software (OPTIONAL) — **rebuilt against the relevance gate**

**Value:** `https://github.com/space-physics/dascasi`, and nothing else.

As recorded on 2026-08-29, HSSI held five entries here — dateutil, matplotlib, numpy, xarray, and
netcdf4-python. That is a dependency list, and **all five fail the Field 29 relevance gate.** Each is
recorded below with its reason so a later refresh does not restore them.

| Rejected entry | Reason |
|---|---|
| `https://github.com/dateutil/dateutil` | Tier A generic infrastructure, named explicitly in the exclusion list as python-dateutil. It is a declared dependency (`pyproject.toml`) used for one call, `dateutil.parser.parse`, to accept string time limits in `load()`. Date parsing is equally at home in a web app, a finance model, or a biology pipeline. |
| `https://github.com/numpy/numpy` | Tier A generic infrastructure, named explicitly. "Depends on numpy" is true of nearly every scientific Python package and distinguishes nothing. |
| `https://github.com/matplotlib/matplotlib` | Tier A generic infrastructure, named explicitly. It is not even a *declared* dependency — `pyproject.toml` lists only `netCDF4`, `xarray`, `numpy`, `python-dateutil`, while `src/dmsp/plots.py` and `LoadMSPdata.py` import it regardless. Plotting is generic infrastructure whether declared or not. |
| `https://github.com/pydata/xarray` | Tier B, and it fails the Field 29 test specifically. Field 29 wants *distinguishing* software — a similar-task tool, a predecessor, a fork parent, a companion, or a **domain-specific** dependency. xarray is a general labelled-array library used across climate science, oceanography, finance, and genomics; it is not heliophysics-specific and says nothing about what this software is. It does qualify under Field 30, where the test is a demonstrated exchange rather than domain specificity — see below. |
| `https://github.com/Unidata/netcdf4-python` | Tier B, and it fails here for the same reason. netCDF is a general array file format spanning the geosciences and beyond, and this is its I/O binding. Generic multi-instrument **format** support belongs in Field 18, where `netCDF3/4` is already correctly recorded. Recording the binding here duplicates that with less precision. |

A package removed from Field 30 does not automatically land in Field 29, and vice versa. For four of
the five above the correct destination is neither field; for netcdf4-python it is Field 18, which
already covers it.

**The single entry — DASCutils / `dascasi`.**

`https://github.com/space-physics/dascasi` — the Digital All Sky Camera utilities package.

*Why it passes the gate.* Field 29 is for "software that performs similar tasks but does not
necessarily link together", and dascasi is close to the paradigm case:

- **Same task shape.** Both are load-and-plot readers for a UAF Geophysical Institute optical auroral
  instrument, written to turn an instrument's native files into an in-memory array plus figures.
- **Same site and same institution.** The GitHub description of dascasi is "Digital All Sky Camera
  utilities, for U. Alaska Geophysical Institute cameras", and its README's first line is "Utilities
  for plotting, saving, analyzing the Poker Flat Research Range Digital All Sky Camera. (Other
  locations, too)." Same observatory as this software.
- **Different instrument.** All-sky camera versus meridian scanning photometer — which is exactly what
  makes the entry informative rather than redundant. A user who has this software's photometer data
  and wants the co-located imagery has a natural next tool, and vice versa.
- **Same author and same organization.** Michael Hirsch, in the `space-physics` GitHub organization,
  Apache-2.0 licensed like this package.
- **Registered as a sibling.** The PyHC registry file `_data/projects_unevaluated.yml` carries both
  packages, with the same `contact: Michael Hirsch` and the identical keyword list
  `["ionosphere_thermosphere_mesosphere","specific"]`. DASCutils's entry reads
  `code: https://github.com/space-physics/dascasi`.

*Be explicit about the evidence basis: it is external to this repository.* The pinned revision of this
software does not name dascasi anywhere. The closest internal hint is `LoadMSPdata.py`'s `--elfid`
option, whose help text is "elevation angles at which to place fiducials (for other camera)" — the
package's only gesture toward a co-located imager, and it names no package. So the association rests on
the GitHub organization, the two repositories' own descriptions, and the PyHC registry, all of which
are public and durable, but none of which is in the source tree. That basis is stated plainly so a
future reader knows the association is defended from public sibling metadata rather than from this
repository's own source.

*Why it is included.* It replaces five uninformative dependency entries with the single most
informative statement this field can make about this software — that it is one of a pair of UAF
Geophysical Institute Poker Flat optical-instrument readers by the same author. The alternative
weighed against it was leaving the field empty on the grounds that the evidence is external to the
repository; that would also have been correct and honest, and either outcome is far better than five
entries that would read identically for an arbitrary Python package.

*URL rather than DOI.* dascasi has a Zenodo badge in its README pointing at
`https://zenodo.org/badge/latestdoi/51016067`, a redirector to the current version DOI rather than a
stable concept DOI. The field's guidance permits the repository URL when no software DOI is on offer,
and the repository URL is the more stable identifier here.

**Also considered and rejected: `https://github.com/space-physics/gima-magnetometer`,** the same
author's UAF Geophysical Institute magnetometer-network reader. Same organization and same institution,
but a different measurement domain entirely — ground magnetic field rather than optical auroral
emission. It shares the site but not the task, so it fails the "performs similar tasks" test. Included
here so the question is not reopened.

**Also considered and rejected: the predecessor distribution `msp_aurora`.** Field 29 does invite
"the project this was forked from", and `msp_aurora` is genuinely this software's ancestor. But it is
not a separate project — it is this same repository under its earlier name, reachable only through
tag `v1.0` of this repository, never published to PyPI, and its GitHub URL redirects here. Listing a
repository as related to itself carries no information. The lineage is documented in Field 12 instead,
which is where it actually matters.

### 30. Interoperable Software (OPTIONAL) — **re-justified against the relevance gate**

- **https://github.com/pydata/xarray**
- **https://www.mathworks.com/products/matlab.html**

Both were already recorded; both survive the gate, and the specific qualifying evidence is cited below
because the previous justification ("the package returns `xarray.Dataset` objects and includes a MATLAB
interface") did not point at the artifacts.

**xarray — qualifies as a documented interchange format.** xarray is Tier B, admissible only when a
specific exchange is documented in the public API, docs, examples, or tests. It is:

- The **README** documents the return type as the exchange contract, and hyperlinks it to upstream:
  "`dat = dmsp.load('~/data/myfile.PF')` ... which returns
  [xarray.Dataset](https://docs.xarray.dev/en/stable/generated/xarray.Dataset.html)". A user is told
  in the usage example that what they get back is an xarray object, with a link to xarray's own API
  documentation for it.
- The **public API signature** states it: `src/dmsp/io.py::load()` is annotated
  `-> xarray.Dataset` and constructs the object explicitly,
  `R = xarray.Dataset(coords={"time": t[tind], "elevation": elv[elind]})`, then assigns one named data
  variable per wavelength channel.
- The **plotting API consumes the same type**: `plots.py::plotmspspectra(dat: xarray.Dataset, elfid)`
  and `spectrasubplot(dat: xarray.Dataset, ...)` are annotated to take it, so the Dataset is the
  interchange currency between the package's two halves and equally usable by anything else that
  speaks xarray.
- **Downstream operations are performed on the exchanged object**: `LoadMSPdata.py` computes
  `ratio = Intensity[a.wl[0]] / Intensity[a.wl[1]]` using xarray's own labelled arithmetic, and
  `ticks.py::timeticks()` explicitly handles an `xarray.DataArray` time span
  (`if isinstance(tdiff, xarray.DataArray)`).

This is the field's own worked example of a qualifying case — a documented interchange format, not
"uses xarray internally".

**MATLAB — qualifies as a cross-language bridge to a named domain tool.** The field text names "a
cross-language bridge to a named domain tool (an IDL SPEDAS or MATLAB interface)" as a qualifying
pattern, and this is a real, working bridge rather than an aspiration:

- `matlab/dmsp.m` is a MATLAB function `[dat, time, elev, wavelength] = dmsp(fn)` that calls the
  Python package directly — `I = py.dmsp.load(fn);` — and then converts the returned Dataset into
  native MATLAB types: `datetime2datetime` maps the time coordinate via
  `t0.values.astype("datetime64[ms]").tolist()`, and `xarray2mat` converts each wavelength channel with
  `double(py.numpy.asfortranarray(V{key}))`.
- `matlab/PlotDMSP.m` is a worked MATLAB example that reports the resolved interpreter
  (`p = pyenv; disp("Using Python " + p.Version ...)`), loads the bundled test file through the bridge,
  and renders the six channels with `pcolor`, giving each its own colour bar and labelling the last of
  them "Rayleighs".
- The README states it plainly: "This library is also usable from Matlab, as seen in `dmsp.m`."
- The relationship is maintained, not vestigial: the release this record now points at is titled
  "Add matlab, update API", the Zenodo abstract for it says "Create Matlab API and plots", the GitHub
  topic `matlab-python-interface` is on the repository, and the pinned HEAD commit is literally
  "matlab works again" (2024-03-21).

`https://www.mathworks.com/products/matlab.html` verified reachable on 2026-08-29; there is no
repository or DOI for a proprietary product, and the field's guidance allows the information page in
that case.

**Considered and rejected for this field:** netCDF4, numpy, matplotlib, and python-dateutil — for the
reasons given in Field 29. netCDF4 is the closest call, since it is Tier B rather than Tier A, but it
is used strictly one-directionally and internally (`load()` opens a file and closes it inside a `with`
block; the netCDF handle never leaves the function and no netCDF object is part of the public API).
There is no exchange, only ingestion. "Part of the standard scientific Python ecosystem" and "a PyHC
package, so it interoperates with PyHC packages" are both explicitly insufficient and neither is relied
on here.

### 31. Related Instruments (OPTIONAL)
**Documented omission — no SPASE record exists for this instrument.**

The software is unambiguously *designed to support* one specific instrument: the University of Alaska
Fairbanks Geophysical Institute Digital Meridian Spectrometer (meridian scanning photometer) at Poker
Flat, Alaska. It parses that instrument's two native file generations, applies that instrument's own
`FilterFactor` calibration, and its plot titles name it — "Meridian Scanning Photometer: Peak
Intensity". It passes the relevance gate without difficulty. The entry is omitted **only** because the
controlled vocabulary has no row for the instrument itself, while the facility it sits at does have
rows. That is resolution-ladder **rule 4** — no instrument record, but its platform/observatory has
one, so the association is carried at the observatory level in Field 32 and the substitution is noted
here. Rule 5 (nothing defensible resolves at all) is *not* the applicable rule, because the Poker Flat
observatory does resolve; a future refresh should not reach for it. Either way, an omission documented
against the ladder is the correct outcome, never an invented value.

**The search, recorded so it need not be repeated.** The `InstrumentObservatory` vocabulary was
fetched in full on 2026-08-29 — 7,602 rows, every one of which passed the
`identifier.startswith("https://spase-metadata.org/")` guard, so no non-SPASE or agent-created rows
were present to worry about. Filtering type-1 (instrument) rows:

- **On "meridian":** three rows exist, none of them this instrument —
  `IUGONET/Instrument/NIPR/Aurora/SYO/SPM`, `SMWG/Instrument/CANOPUS/MPA`, and
  `SMWG/Instrument/TREX/PAMIS`.
- **On "photometer":** 75 rows, overwhelmingly BARREL balloon optical photometers, ICESTAR Antarctic
  AGO photometers, Atmosphere Explorer Visible Airglow Photometers, and OMTI tilting photometers. None
  is at Poker Flat.
- **On "Poker":** seven type-1 rows, all other instruments at the same site — three magnetometer
  records (`IUGONET/Instrument/WDC_Kyoto/WDC/POK/Magnetometer`,
  `SMWG/Instrument/Ground/Poker.Flat/Magnetometer`, `SMWG/Instrument/THEMIS/Ground/UCLA-GBO/POKR/MAG`),
  a search-coil magnetometer (`IUGONET/Instrument/TohokuU/mag_obs/pok/sm`), an MF radar
  (`IUGONET/Instrument/NICT/SALMON/PF/MFradar`), an all-sky imager
  (`IUGONET/Instrument/NICT/SALMON/PF/asi`), and an aurora camera
  (`IUGONET/Instrument/TohokuU/opt_obs/pok/ac`).

**Two wrong matches that will tempt a future agent — do not use either.**

1. **`https://spase-metadata.org/IUGONET/Instrument/NIPR/Aurora/SYO/SPM`**, name "Multi-color meridian
   scanning photometer", abbreviation `SPM`. It is the closest name match the searches above turned
   up, and it is the wrong instrument. Its SPASE definition places it at **Syowa Station, Antarctica**,
   operated by Japan's National Institute of Polar Research: "The SPM observation at Syowa Station
   started during JARE11 (the 11st Japanese Antarctic Research Expedition)." Opposite hemisphere,
   different operator, different instrument. The identifier path itself says so — `NIPR/.../SYO/`.
2. **The Defense Meteorological Satellite Program rows.** Searching the vocabulary for "DMSP" — the
   package's own distribution name and the string in the data archive path
   `optics.gi.alaska.edu/PKR/DMSP/` — surfaces DMSP satellite instrument records. Those are
   spacecraft instruments on a US military weather satellite program and have nothing to do with this
   ground-based photometer. This is the single most dangerous trap in this record.

**The observatory-level association is preserved instead**, which is what rule 4 requires: a missing
instrument record must not block the software's association, and the platform/observatory record
carries it. That is exactly what Field 32 does. No instrument entry is recorded here, and none
should be invented: the backend's no-identifier fallback would either bind the name to an arbitrary
same-named row or mint a new identifier-less row, which is precisely the class of row a prior
vocabulary cleanup removed.

If a SPASE record for the UAF GI Poker Flat DMS/MSP is created upstream in future, this field should be
filled with it — the relevance case is already established above.

### 32. Related Observatories (OPTIONAL) — **resolved among three same-site SPASE rows**

- **Observatory Name:** Poker Flat Geophysical Observatory
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Ground/Poker.Flat

**The relevance question is settled: yes.** The software is purpose-built for one observatory's data.
The README subtitle names it — "For Geophysical Institute's Poker Flat Digital Meridian Spectrometer" —
every data source in Field 17 is a UAF GI Poker Flat archive path, and Field 17's
`Observatory/Mission-specific` selection requires the observatory be named here.

**The hard part was which row represents that one observatory.** This is the per-entity collision
case: one real-world entity — the Poker Flat facility in Alaska — with several SPASE rows registered by
different projects. Nothing in the pinned repository names Tohoku University, NICT, IAGA, WDC Kyoto, or
any SPASE namespace, so no in-repo evidence selects among them; the choice therefore rests on the
resolution ladder's SMWG tie-breaker rather than on repository evidence. The candidates, all type-2 and
all SPASE-backed, verified 2026-08-29:

| SPASE identifier (`https://spase-metadata.org/` + path) | Row `name` | SPASE definition | Assessment |
|---|---|---|---|
| `SMWG/Observatory/Ground/Poker.Flat` | Poker Flat Geophysical Observatory | "Poker Flat (POKR) Geophysical Observatory" | **Selected.** SMWG is the namespace-neutral SPASE Metadata Working Group registry, and the ladder names `SMWG/...` as the tie-breaker among competing rows for one entity. The name is facility-level rather than scoped to one visiting project's instrument suite. |
| `IUGONET/Observatory/NICT/SALMON/PF` | Poker Flat | "Poker Flat Research Range of Geophysical Instititute, University of Alaksa Fairbanks (GI/UAF). The NICT ... experiments have been operated as joint middle and upper atmosphere observations beween NICT and GI/UAF." *(typos are in the source record)* | **Rejected, though the closest call.** The only candidate whose definition explicitly identifies the facility as the UAF Geophysical Institute's Poker Flat Research Range — the exact operator of this instrument. Against it: the record is registered under NICT's SALMON project namespace, so its scope is arguably the NICT–UAF joint experiment site rather than the GI facility as such, and its bare `name` "Poker Flat" is the least descriptive of the three. |
| `IUGONET/Observatory/TohokuU/opt_obs/pokopt` | Poker Flat aurora observatory | "Poker Flat aurora observatory" | **Rejected; the row this entry supersedes.** In its favour: it is the only candidate whose name states the *optical/auroral* measurement domain, matching this software. Against it: it is Tohoku University's optical observation site record (`TohokuU/opt_obs/`), and the DMS is a UAF GI instrument, not a Tohoku University one — so the row identifies the right place under the wrong operator. |

**Rejected candidates — wrong measurement domain.** Three further Poker Flat type-2 rows exist and are
all geomagnetic observatory registrations, which do not describe an optical auroral facility:
`IUGONET/Observatory/TohokuU/mag_obs/pokmag` ("Poker Flat geomagnetic observatory"),
`IUGONET/Observatory/WDC_Kyoto/WDC/POK` ("Poker Flat Geomagnetic Observatory", abbreviation `POK`,
definition "Poker Flat (POK), Sponsoring Country:U.S.A."), and `SMWG/Observatory/IAGA/Poker.Flat`
("Poker.Flat", an IAGA magnetic-observatory code registration). Recorded so they are not reconsidered.

**Why `SMWG/Observatory/Ground/Poker.Flat` was chosen.** It is the facility-level, project-neutral
record for the site, and it is the row the resolution ladder's SMWG tie-breaker points to. It
supersedes `IUGONET/Observatory/TohokuU/opt_obs/pokopt`, which identifies the right physical place
under the wrong operator — a Tohoku University optical-observation site record, whereas the DMS is a
UAF Geophysical Institute instrument. The change is therefore a precision improvement rather than the
correction of an error, and retaining the superseded row would have been a defensible zero-change
outcome; both are recorded so the choice is not mistaken for an oversight in either direction.

The name above is copied verbatim from the chosen vocabulary row and paired with that row's
identifier. An observatory name without a SPASE identifier must never be emitted: the backend would
either bind it to an arbitrary same-named row by case-sensitive match or create a new identifier-less
row.

### 33. Logo (OPTIONAL)
**Not found — an evidenced absence, not an unfilled field.**

There is no logo:

- The pinned tree contains exactly one image file of any kind, `src/dmsp/tests/demo.png`, and it is
  not a logo. (Its only other binary is the bundled netCDF test data file
  `src/dmsp/tests/PKR_SMSP_STD_20141011.NC`.)
- **`src/dmsp/tests/demo.png` is a data plot, not a logo, and must not be used as one.** It is a
  2195×1577 RGBA PNG of about 3 MB, and the README embeds it with the alt text
  "example of PF-DMSP data" — it is a screenshot of the six-panel spectra figure the package produces.
- The PyHC registry entry for this package has **no `logo:` key**. This is a meaningful absence rather
  than a registry that omits logos generally: the neighbouring DASCutils entry in the same file does
  carry one (`logo: https://i.ibb.co/JKLF4FB/logo.jpg`). **That sibling's logo belongs to DASCutils and
  must not be borrowed for this record.**
- The GitHub API reports `homepage: null` and `has_pages: false`, so there is no project site to take a
  brand image from, and the README's only other images are status badges.

If a logo is ever added, the URL must be a commit-pinned raw URL, fetch-verified to return an `image/*`
content type with plausible image bytes — a raw GitHub URL can return HTTP 200 with `text/plain` when
the file is a Git LFS pointer — and must be neither a branch reference (which moves) nor a `blob/` page
URL (which serves HTML).

---

## Cross-cutting notes

**Field-length headroom.** Every URL in this record is well inside the platform's undocumented
character limits: the longest URL-typed value is the repository/documentation URL at 62 characters
against a 200-character limit, and the longest related-item URL is 61 characters against a
128-character effective limit. No award is recorded, so the 128-character award-title limit is not
engaged. These limits are enforced at the database layer without a prior validation error, so the
sweep is worth repeating whenever a longer URL is proposed.

**Values whose correctness is time-bounded.** Field 23 (Development Status) is derived from the age of
the last commit and will need re-deriving at any future refresh. Field 12 will change if the maintainer
cuts a new release — and note that a future `1.0.0` release would be a *legitimate* value even though
`v1.0` is not, because the objection to `v1.0` is that it versions the predecessor distribution, not
that its number is high.
