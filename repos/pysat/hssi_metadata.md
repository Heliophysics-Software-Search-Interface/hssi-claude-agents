# HSSI Metadata Extraction Results

**HSSI Software ID:** 763e3b22-b9ac-4bee-b665-69d1acb70712
**Repository:** https://github.com/pysat/pysat
**Source Revision:** 3f0e5a43ad36f1eecfed02a3d1e3a740fd1a5f37
**Extraction Date:** 2026-09-02
**Validation Date:** 2026-09-02
**Validation Status:** PASS

---

## Scope notes — read these before the evidence

**1. pysat is a framework, and its ecosystem lives in separate repositories.** The source revision
above is the `v3.2.2` release commit and is also the head of `main`. At that revision
`pysat/instruments/` holds nothing beyond an `__init__.py`, `pysat_ndtesting.py`, `pysat_netcdf.py`,
`pysat_testing.py`, `pysat_testmodel.py`, a `methods/` directory and a `templates/` directory —
synthetic test instruments, a general reader for pysat-written netCDF files, and shared helper
functions. The mission, archive and instrument support that people associate with pysat is supplied by
**separate, separately released, separately citable plug-in packages** — pysatNASA, pysatMadrigal and
pysatSpaceWeather are the ones a reader is most likely to have met. Those three names are
illustrations, not a census: **Field 30 carries the ecosystem inventory** and is the list to read, and
nothing in this note should be taken as fixing how many plug-in packages there are.

This dossier therefore applies **two different standards, chosen from the form's own wording**, and
applies each one consistently:

- **Capability fields — Software Functionality (4), Data Sources (17), Input/Output File Formats
  (18/19), Related Phenomena (22), Related Instruments/Observatories (31/32).** The form says
  "supports", and Field 18 adds *Only formats actually supported should be indicated*. A value is
  recorded here only when **the pysat distribution itself contains the code that delivers it**. If a
  user who runs `pip install pysat` and nothing else cannot do the thing, it is not recorded, because
  a searcher who filters on that value and clicks through to pysat would find a promise the package
  does not keep. The capability belongs to the plug-in, and the plug-in has (or will have) its own
  HSSI entry.
- **Audience fields — Related Region (5) and Keywords (16).** Field 5's own instruction is different:
  *Select all physical regions the software's functionality is commonly used or intended for.*
  The phrase "intended for" is a statement about purpose, not implementation, so these fields are
  evidenced from the **core package's own self-description** — the `keywords` list in `pyproject.toml`
  (shipped in the distribution and published to PyPI), the identical list in `.zenodo.json`, and the
  repository topics the maintainers set on `pysat/pysat` itself. Plug-in reach is still excluded; the
  difference is that a maintainer-authored declaration of intent counts here and a line of shipped
  code is not required.

A future refresh that wants to widen a capability field must widen it for *all* of them, or say why
the form's wording licenses the exception. The asymmetry above is licensed by the form text, not by
convenience.

**2. The project wiki is a separate git repository.** `https://github.com/pysat/pysat.wiki.git` is
not reachable from the source revision and does not appear in the code tree. It is nonetheless
primary, maintainer-authored evidence and is cited below for development status, release process and
the ecosystem status chart that `docs/ecosystem.rst` links to.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The placeholder is the catalogue convention for a record maintained by the HSSI curation effort
rather than by the software's own maintainers. It is not a defect.

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.1199703

This is the Zenodo **concept** DOI: DataCite resolves it to the newest deposit (currently the record
titled `pysat/pysat: v3.2.2`, publisher Zenodo, licence `bsd-3-clause`), and `docs/citing.rst` at the
source revision tells users this DOI will always point to the latest version of the code. The same
DOI is embedded in the header comment of pysat's own source files (for example the first lines of
`pysat/utils/coords.py`) and in `pysat/citation.txt`.

**Considered and not selected:** the version DOI https://doi.org/10.5281/zenodo.15059161. It is the
correct identifier for the *v3.2.2 release specifically*, and it is recorded in Field 12 for exactly
that purpose. Field 2 identifies the software as an ongoing work, so the concept DOI is the right
choice; recording the version DOI here would make the record go stale at every release.

**Caveat worth keeping:** `pysat/citation.txt` at the source revision still reads
`Stoneback, Russell, et al. (2023). pysat/pysat v3.1 (Version v3.1). Zenodo. http://doi.org/10.5281/zenodo.1199703`
— the version string in that file lags the release. The DOI in it is correct; the `v3.1` is stale
upstream. Do not derive Field 12 from that file.

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/pysat/pysat

Corroborated four independent ways: the `[project.urls] Source` entry in `pyproject.toml` at the
source revision; the PyPI JSON metadata for the `pysat` project, whose `project_urls.Source` is this
same URL (a PyPI 200 alone would only prove the *name* is taken, so the URL match is what identifies
the package); the PyHC core registry `code` field; and the Zenodo v3.2.2 deposit, whose only related
identifier is an `isSupplementTo` relation pointing at `https://github.com/pysat/pysat/tree/v3.2.2` —
the signature of a GitHub-integration deposit rather than a manual upload.

### 4. Software Functionality (RECOMMENDED — treated as critical)

- **Coordinate Transforms**
- **Data Processing and Analysis**
- **Data Processing and Analysis: Analysis**
- **Data Processing and Analysis: Data Access and Retrieval**
- **Data Processing and Analysis: Data Reduction**
- **Data Processing and Analysis: File Format Conversion**
- **Data Processing and Analysis: Processing**
- **Data Processing and Analysis: Time Series Analysis**
- **Mission-related**
- **Mission-related: Science Data Processing**

Every value is evidenced from code and documentation shipped in the distribution at the source
revision, per scope note 1.

- **Coordinate Transforms.** `pysat/utils/coords.py` is a public, documented module — `docs/api.rst`
  gives it its own "Coordinates" section — whose module docstring is
  `Coordinate transformation functions for pysat.` It provides `calc_solar_local_time` (geographic
  longitude plus universal time to solar local time, written back into the Instrument with units and
  metadata), `update_longitude` and `adjust_cyclic_data` (rebasing a cyclic coordinate onto a
  different range), and `establish_common_coord` (building one coordinate array valid for several
  data sets). *No subcategory is recorded*, deliberately: pysat implements no named coordinate-system
  conversion. There is no AACGM, apex, GSE/GSM/SM or SPICE code in the package, so
  `Coordinate Transforms: Ionospheric`, `: Magnetospheric`, `: Solar` and `: Mission-Specific` would
  all be unsupported. Magnetic local time appears in pysat only as a *generated* column in the
  synthetic test instruments (`pysat/instruments/methods/testing.py` labels `mlt` as Magnetic Local
  Time), not as a computed transform.
- **Data Processing and Analysis** — parent of the six `Data Processing and Analysis`
  subcategories that follow.
- **`: Analysis`.** The first entry in the README's Main Features list is
  `* Instrument independent analysis routines.` The `Constellation` class exists to run analysis
  across several instruments at once, and `Orbits` computes orbit breaks on the fly from loaded data.
- **`: Data Access and Retrieval`.** `Instrument.download`, `Instrument.download_updated_files`,
  `Instrument.remote_file_list` and `Instrument.remote_date_range` are the user-facing retrieval API,
  and `Files` plus `pysat.utils.files` discover, index and cache local holdings. The *transport* is
  supplied by the plug-in's `download` function — `Instrument.download` ends by calling
  `self._download_rtn`, and the core package imports no HTTP client at all. That is why this
  functionality is recorded while the concrete archives are **not** recorded in Field 17: the
  retrieval machinery is pysat's, the endpoints are not.
- **`: Data Reduction`.** `Constellation` accepts an `index_res` resolution in seconds and
  `Constellation._index` builds the common time index from it, after which
  `Constellation.to_inst(common_coord=..., fill_method=...)` resamples or interpolates every member
  instrument onto that index — genuine downsampling and regridding of multi-instrument data.
  `pysat.utils.coords.establish_common_coord` does the same for non-time coordinates. `Instrument.drop`,
  `Meta.drop`, `Meta.keep` and `Instrument.bounds` reduce data volume by variable and by time range.
  This value was in the catalogue before this refresh with no recorded evidence; the evidence above is
  what justifies keeping it. Note that pysat does **not** average or bin — those routines live in
  pysatSeasons — so if a future refresh finds this value too generous, the specific thing to weigh is
  whether resampling onto a coarser common cadence counts as reduction.
- **`: File Format Conversion`.** `pysat.utils.io.inst_to_netcdf` and `Instrument.to_netcdf4` write
  any loaded Instrument to netCDF4 regardless of the format the plug-in read it from, and
  `pysat.instruments.methods.general.load_csv_data` plus `Meta.from_csv` read delimited text in. A
  CSV-to-netCDF round trip is achievable with core pysat alone.
- **`: Processing`.** `Instrument.custom_attach` / `custom_apply_all` / `custom_clear` attach
  user-supplied functions to the load pipeline; instrument modules supply `preprocess` and `clean`
  hooks; `pysat.utils.update_fill_values`, `Instrument.rename` and
  `pysat.instruments.methods.general.remove_leading_text` are shipped processing operations.
- **`: Time Series Analysis`.** All pysat data are time-indexed. `pysat.utils.time` provides
  `calc_res`, `calc_freq`, `freq_to_res`, `create_date_range`, `create_datetime_index` and
  `datetime_to_dec_year`; `Orbits` iterates complete orbits across day and file breaks; and the
  README's feature list calls out support for rigorous time-series calculations that need spin
  up/down time across day, orbit and file boundaries (the `pad` machinery in `Instrument`).
- **Mission-related** — the parent of the subcategory below, recorded because the taxonomy requires a
  subcategory's parent to be present alongside it. Before this refresh the record carried
  `Mission-related: Science Data Processing` **without** `Mission-related`, a combination the taxonomy
  does not permit; supplying the parent is what repairs it.
- **`: Science Data Processing`.** The distribution ships the code that turns a loaded `Instrument`
  into the standards-compliant, publicly distributable science data file a mission is obliged to
  deliver, and named missions use it for precisely that. In the package: `pysat/utils/io.py` is public
  API — `docs/api.rst` exposes `pysat.utils.io` with `:members:` under its I/O section — and provides
  `add_netcdf4_standards_to_metadict`, whose docstring is
  `Add metadata variables needed to meet SPDF ISTP/IACG NetCDF standards.`, together with its inverse
  `remove_netcdf4_standards_from_meta`, docstring
  `Remove metadata from loaded file using SPDF ISTP/IACG NetCDF standards.`; `inst_to_netcdf` stamps
  each file it writes with `attrb_dict['Conventions'] = 'pysat-simplified SPDF ISTP/IACG for NetCDF'`.
  `docs/tutorial/tutorial_files.rst` records where that standard came from —
  `pysat's default conventions are a simplified implemention of the standards` developed for NASA's
  Ionospheric Connections Explorer mission — and `docs/roadmap.rst` states that pysat is capable of
  maintaining compliance with the Space Physics Data Facility's
  `formatting requirements for NASA satellite missions`. The 2023 *Frontiers* ecosystem paper
  corroborates the use, in a section headed `Satellite instrumentation processing`:
  `Pysat is in use for Ion Velocity Meter (IVM) processing on both the NASA Ionospheric Connections (ICON) Explorer as well as the National Oceanic and Atmospheric Administration (NOAA)/National Space Organization (NSPO) Constellation Observing System for Meteorology Ionosphere and Climate-2 (COSMIC-2) constellation.`,
  `IVM processing software for ICON and COSMIC-2 is built on pysat.` and
  `Pysat features are also used to create the publicly distributed files for the missions.`

**Why the child was kept rather than dropped, and what was given up.** This value was decided against
a serious alternative rather than by default, so both sides are recorded.

The **alternative considered and not taken** was to drop `Mission-related: Science Data Processing`
altogether. Its argument: pysat is not part of any mission's ground system or operations chain, it is
a general framework a mission *team* adopts; the taxonomy's own distinction is that reading a
mission's data is Data Access and Retrieval while being part of that mission's ground system is
Mission-related; and whatever processing pysat does is already covered by
`Data Processing and Analysis: Processing`. On that reading the missing parent was best resolved by
removing the child rather than adding a parent thought to be equally unsupported.

That argument lost on the specifics. The thing pysat does for a mission is not generic processing: it
is the last stage of a mission's science data pipeline — writing archive-standard files with the
metadata an agency archive requires — and the code that does it (`add_netcdf4_standards_to_metadict`,
`remove_netcdf4_standards_from_meta`, `inst_to_netcdf`) is in the distribution, so the value satisfies
the capability standard in scope note 1 without borrowing anything from a plug-in. `Processing` covers
the custom-function pipeline, which is a different capability and is recorded separately above. The
mission connection is also concrete rather than hypothetical: two named missions' IVM processing is
built on pysat and their public files are produced with it. Someone searching HSSI for software that
performs mission science data processing is better served by finding pysat than by not finding it.

**One honest tension to carry forward.** The IVM processing packages built on pysat for ICON and
COSMIC-2 are not themselves in this distribution, so the *pipeline* is downstream even though the
standards-compliance machinery is shipped. This value therefore rests on the shipped file-standards
code, with the mission use as corroboration — not on the downstream pipelines. A future refresh that
wants to revisit it should weigh that shipped code, not the paper.

**Removed — `Data Processing and Analysis: Data Assimilation`.** The record carried this value before
this refresh; it is not retained. A case-insensitive search for `assimilat` across the entire tree at
the source revision returns **0 matches**. pysat contains no
assimilation algorithm, no filter, and no model-observation fusion. The value most plausibly traces to
Field 26, where NSF award AGS-1651393 is titled with the phrase *Assimilative Analysis of Low- and
Mid-latitude Ionospheric Electrodynamics*: that is the title of a research grant that *funded* pysat
development, not a description of pysat's code. **A future refresh should not re-derive this value
from the award title.** If assimilation ever belongs to this ecosystem it belongs to pysatModels,
which does model-data comparison.

**Considered and not selected, with reasons:**
- `Data Visualization` and every subcategory of it — `matplotlib` appears **0 times** in the package
  source at the source revision (`git grep -ci matplotlib <pin> -- 'pysat/*.py' 'pysat/utils/*.py'
  'pysat/instruments/*'` returns nothing). pysat produces arrays and Instrument objects; plotting is
  left to the user or to pysatSeasons.
- `Models and Simulations` and subcategories — `pysat_testmodel` produces a synthetic 4-D field that
  *resembles* model output, and `docs/dependency.rst` describes it as an object that most closely
  resembles data sets from geophysical models. It is a unit-test fixture for downstream packages, not
  a model. Modelling in this ecosystem is pysatModels and pysatMissions.
- `Data Processing and Analysis: Calibration` — pysat defines cleaning *levels* (`clean`, `dusty`,
  `dirty`, `none`) but delegates the actual cleaning to each plug-in's `clean` function, and supplies
  no response functions, gains or unit conversions from raw counts.
- `Servers and Environments` and subcategories — no Dockerfile, no container definition, no
  server, no MPI or HPC code in the tree.

### 5. Related Region (RECOMMENDED — treated as critical)

- **Earth Atmosphere**
- **Earth Ionosphere**
- **Earth Magnetosphere**
- **Earth Thermosphere**
- **Interplanetary Space**

The vocabulary is **flat**: `Earth Atmosphere` does not imply `Earth Ionosphere` or
`Earth Thermosphere`, and an argument of the form "the broad region encompasses the narrow one" is a
defect, not a justification. Each value below is evidenced on its own.

Evidence is the core package's own declared scope, per scope note 2. `pyproject.toml` at the source
revision carries an eleven-item `keywords` list — `pysat`, `ionosphere`, `atmosphere`,
`thermosphere`, `magnetosphere`, `heliosphere`, `observations`, `models`, `space`, `satellites`,
`analysis` — and `.zenodo.json` carries the identical eleven. The repository topics set on
`pysat/pysat` include `ionosphere`, `magnetosphere` and `thermosphere`. `docs/introduction.rst` states
that pysat was initially designed for in situ satellite measurements and has grown to
`support both observational and modelled space science measurements.`

- `Earth Ionosphere` — declared in `pyproject.toml`, in `.zenodo.json` *and* in the repository topics,
  as are `Earth Thermosphere` and `Earth Magnetosphere`. Before this refresh the record named neither
  the ionosphere nor the thermosphere, which was the largest gap in this field.
- `Earth Thermosphere` — same three sources.
- `Earth Magnetosphere` — same three sources.
- `Earth Atmosphere` — declared in `pyproject.toml` and `.zenodo.json`.
- `Interplanetary Space` — the mapping for the declared keyword `heliosphere`, which has no
  dedicated row of its own. `Heliosheath` was rejected as far too specific; `Solar Wind` was rejected
  because the project declares the *region* (heliosphere), not the medium, and because pysat contains
  no solar-wind functionality (see Field 22).

**Removed — `Solar Environment`.** The record carried this region before this refresh; it is not
retained. Nothing in the core package's declared scope names the Sun, the corona or the solar
atmosphere: it is absent from the `pyproject.toml` keywords, from `.zenodo.json`, and from the
repository topics, and the package contains no solar-physics code. The word `solar` occurs under
`pysat/` at the source revision in only four files, and none of them is about the Sun:
`pysat/utils/coords.py` and `pysat/tests/test_utils_coords.py` are `calc_solar_local_time` and its
tests, which compute a local-time coordinate; `pysat/instruments/methods/testing.py` labels the
synthetic test instrument's `slt` column `Solar Local Time`; and `pysat/tests/cindi_ivm_meta.txt`, the
instrument metadata fixture discussed in Field 31, carries the column names `Solar Zenith Angle`,
`Solar Local Time` and `Solar Ram Angle`. Geometry and local time, not solar physics. A visitor browsing HSSI for
`Solar Environment` is looking for solar-physics software and would find a satellite-data framework
out of place there. The alternative — keeping it on the grounds that `heliosphere` is a declared
keyword and the heliosphere is driven by the Sun — was rejected, because the vocabulary is flat and a
region is not implied by a neighbouring one; `Interplanetary Space` is where that keyword maps, and it
is recorded.

**Considered and not selected:** `Earth Lower and Middle Atmosphere` (pysat's declared scope is
satellite and upper-atmosphere measurements, not the lower/middle atmosphere);
`Earth Auroral Subregion`, `Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`,
`Earth Magnetosheath`, `Earth Magnetotail` (no evidence in the project's own declarations, and
choosing among them would be invention); `Planetary Magnetospheres` and the per-planet rows (pysat is
an Earth-orbit and heliophysics framework at this revision).

### 6. Authors (MANDATORY)

Fourteen authors, in the order the record carries them, which is also the order of the `creators`
array in `.zenodo.json` at the source revision and of the creators on the published Zenodo v3.2.2
deposit. The three sources agree on the same fourteen people and on their order, but they no longer
agree on ORCIDs: the record carries iDs for **Matthew Depew and Gayatri Iyer** that `.zenodo.json` and
the Zenodo deposit do not, because those two were established from ORCID search and affiliation
matching rather than copied from `.zenodo.json` — the evidence is under Authors 7 and 13. Apart from
those two, the record's identifiers, present and absent alike, match `.zenodo.json`. The divergence is
deliberate and is **not** drift to be reconciled back to the upstream sources. The numbering below is
presentational only — it is not a stored sort value, so a later correction should identify an author
by name, never by index.

There is **no `CITATION.cff` and no `codemeta.json`** in the repository at the source revision, and
`pyproject.toml` credits only `Russell Stoneback, et al.`, so `.zenodo.json` is the authoritative
author list.

#### Author 1: Russell Stoneback
- **Identifier:** https://orcid.org/0000-0001-7216-4336
- **Affiliation 1 — Organization:** Cosmic Studio · **Identifier:** Not found
- **Affiliation 2 — Organization:** Stoneris · **Identifier:** Not found

`.zenodo.json` and the Zenodo v3.2.2 deposit give Cosmic Studio only. His ORCID record lists Cosmic
Studio (CEO/Founder, from 2021-09) and, earlier, three University of Texas at Dallas posts. **Stoneris
is nonetheless correct and is retained:** the 2023 *Frontiers in Astronomy and Space Science* paper
*The pysat ecosystem* (https://doi.org/10.3389/fspas.2023.1119775) prints his affiliation as
Stoneris, Plano, TX, United States. Neither organisation has a ROR record — a ROR query for
"Cosmic Studio" returns no matching organisation and one for "Stoneris" returns zero results — so both
are correctly stored without identifiers.

#### Author 2: Jeff Klenzing
- **Identifier:** https://orcid.org/0000-0001-8321-6074
- **Affiliation — Organization:** Goddard Space Flight Center · **Identifier:** https://ror.org/0171mag52

`.zenodo.json`, the Zenodo deposit and the Frontiers paper (NASA Goddard Space Flight Center, ITM
Physics Laboratory) all agree.

**Considered and not selected — University of Maryland, Baltimore County (https://ror.org/02qskvh78).**
His ORCID record shows the Goddard employment ending 2025-08 and UMBC employments beginning 2025-10
(Goddard Planetary Heliophysics Institute) and 2026-06 (Center for Space Sciences and Technology).
Both post-date the v3.2.2 release this record describes, and pysat's own `.zenodo.json` at the source
revision names Goddard. An author affiliation on a software record tells a reader where the work was
done; adding a later employer would be noise. If a future release ships with UMBC in `.zenodo.json`,
that is the moment to add it.

#### Author 3: Angeline Burrell
- **Identifier:** https://orcid.org/0000-0001-8875-9326
- **Affiliation — Organization:** United States Naval Research Laboratory · **Identifier:** https://ror.org/04d23a975

`.zenodo.json` names her `Angeline G. Burrell` and gives the affiliation as U.S. Naval Research
Laboratory; her ORCID employment is US Naval Research Laboratory, Space Science Division, from
2018-07. The stored organisation name is the ROR display name for https://ror.org/04d23a975, which is
the correct canonical form; the shorter variants are the same institution.

#### Author 4: Asher Pembroke
- **Identifier:** Not found
- **Affiliation — Organization:** Predictive Science · **Identifier:** https://ror.org/05canvq15

**Negative research — do not re-propose.** An ORCID iD exists under the exact name Asher Pembroke
(0000-0002-5718-1303), but that record contains **no employments and no works**, so nothing ties it to
the pysat contributor. Recording it would be a guess.

**Predictive Science carries https://ror.org/05canvq15**, which is recorded in HSSI. ROR gives the
display name `Predictive Science (United States)` for an active company in San Diego, established
2008, with the website https://www.predsci.com/portal/home.php, and pysat's own `.zenodo.json` gives
Pembroke's affiliation as `Predictive Science`, so the match is unambiguous. The organisation was held
without any identifier before this refresh; the identification had to be established from that
evidence rather than simply submitted alongside the name, because a ROR supplied for a stored
organisation that carries none is matched as a second organisation instead of being applied to the
existing one. The stored organisation **name remains `Predictive Science`** and was deliberately not
changed to the ROR display form — the short form is what the software's own `.zenodo.json` uses, and a
later agent should not "correct" it to `Predictive Science (United States)`.

#### Author 5: Carey Spence
- **Identifier:** https://orcid.org/0000-0001-8340-5625
- **Affiliation — Organization:** The University of Texas at Dallas · **Identifier:** https://ror.org/049emcs32

The ORCID record lists no employments, so `.zenodo.json` is the sole affiliation source and it agrees
with the stored value.

#### Author 6: Jonathon M. Smith
- **Identifier:** https://orcid.org/0000-0002-8191-4765
- **Affiliation 1 — Organization:** Catholic University of America · **Identifier:** https://ror.org/047yk3s18
- **Affiliation 2 — Organization:** Goddard Space Flight Center · **Identifier:** https://ror.org/0171mag52

`.zenodo.json` gives both, comma-separated in one string. His ORCID employment confirms Catholic
University of America, Physics, Research Scientist, from 2018-08.

#### Author 7: Matthew Depew
- **Identifier:** https://orcid.org/0000-0001-9069-4998
- **Affiliation — Organization:** The University of Texas at Dallas · **Identifier:** https://ror.org/049emcs32

**Why this ORCID.** An ORCID expanded search on the name Matthew Depew returns exactly one record,
https://orcid.org/0000-0001-9069-4998, and its sole employment is University of Texas at Dallas,
department **Center for Space Sciences**, Electrical Engineer, from 2010-12-22 — the group pysat came
out of, and the same institution `.zenodo.json` gives for him. He is also a co-author of the reference
publication https://doi.org/10.1029/2018JA025297, whose author list Crossref gives as Stoneback,
Burrell, Klenzing and M. D. Depew; that co-authorship comes from the paper's own metadata and **not**
from the ORCID record, which lists no works at all. The employment and the uniqueness of the name in
ORCID are the whole of the identification, and it is on that basis that the iD is recorded in HSSI.

He was stored without any identifier before this refresh. The iD could not simply be sent as a value
alongside the existing name, because an ORCID supplied for a stored person who carries none is matched
as a new person rather than applied to the existing one — which is why the identification was
established this carefully before it was recorded.

#### Author 8: Aadarsh Govada
- **Identifier:** https://orcid.org/0009-0004-7873-5899
- **Affiliation 1 — Organization:** Goddard Space Flight Center · **Identifier:** https://ror.org/0171mag52
- **Affiliation 2 — Organization:** Universities Space Research Association · **Identifier:** https://ror.org/043pgqy52

`.zenodo.json` gives both; his ORCID employment confirms Universities Space Research Association with
that same ROR.

#### Author 9: Ryan Fuller
- **Identifier:** Not found
- **Affiliation — Organization:** The University of Texas at Dallas · **Identifier:** https://ror.org/049emcs32

**Negative research.** An ORCID search on the name returns several people, none with a space-science
or University of Texas at Dallas affiliation. No identification is defensible.

#### Author 10: Teresa Esman
- **Identifier:** https://orcid.org/0000-0003-0382-6281
- **Affiliation — Organization:** Goddard Space Flight Center · **Identifier:** https://ror.org/0171mag52

**Considered and not selected — `NASA NPP`.** That is the string `.zenodo.json` and the Zenodo deposit
carry for her, and it names the NASA Postdoctoral Program, a fellowship, not an employing institution.
Her ORCID record lists no employments. Goddard Space Flight Center is where the fellowship was held
and is already recorded, so the program string adds nothing an institutional affiliation field should
carry.

#### Author 11: Veronica Von Bose
- **Identifier:** Not found
- **Affiliation — Organization:** The University of Texas at Dallas · **Identifier:** https://ror.org/049emcs32

**Negative research.** An ORCID search returns no candidate with this surname in space science.

#### Author 12: Nathaniel Hargrave
- **Identifier:** Not found
- **Affiliation — Organization:** The University of Texas at Dallas · **Identifier:** https://ror.org/049emcs32

**Negative research.** An ORCID search returns other people named Hargrave, none of them Nathaniel in
a space-science group.

#### Author 13: Gayatri Iyer
- **Identifier:** https://orcid.org/0000-0002-0229-8125
- **Affiliation — Organization:** The University of Texas at Dallas · **Identifier:** https://ror.org/049emcs32

**Why this ORCID.** Four ORCID records carry the name Gayatri Iyer, and
https://orcid.org/0000-0002-0229-8125 is the only one of the four with any University of Texas at
Dallas affiliation: department `Physics - William B. Hanson Center for Space Sciences`, Research
Assistant, 2018-06-15 to 2019-05-05 — pysat's home group, and the same institution `.zenodo.json`
gives for her. Of the other three, one is a genetics and biotechnology researcher (ICGEB and the
University of Michigan) and two list no institutions at all. That affiliation match is what the
recorded iD rests on.

The limit of the evidence is worth stating plainly so a later agent does not go looking for more: her
ORCID record lists no works, and she is **not** an author of the 2018 JGR pysat paper. As with
Author 7, she was stored without an identifier before this refresh, and an ORCID supplied for a stored
person who carries none is matched as a new person rather than applied to the existing one — hence the
care taken over the affiliation evidence before the iD was recorded.

#### Author 14: Silvio Leite
- **Identifier:** https://orcid.org/0000-0003-1707-7963
- **Affiliation — Organization:** Olist · **Identifier:** Not found

`.zenodo.json` records the affiliation as the GitHub-style handle `@olist`; `Olist` is the expanded
organisation name and is what is stored. A ROR query for "Olist" returns zero results, so no
identifier is available. His ORCID record gives the fuller personal name Silvio Luis Pereira Leite and
lists no employments; the shorter form is what the software's own author list uses and is retained.

### 7. Software Name (MANDATORY)
- **Name:** pysat

Lower-case throughout the project: `pyproject.toml` `name = "pysat"`, the PyPI project name, and the
PyHC core registry entry. The README's title line expands it as `pysat: Python Satellite Data Analysis
Toolkit`, and `docs/introduction.rst` writes out The Python Satellite Data Analysis Toolkit (pysat).
The expansion is carried in Field 8 rather than in the name, so that the name matches the import
name a user types.

### 8. Description (MANDATORY)

> pysat, the Python Satellite Data Analysis Toolkit, is a Python package and framework for science
> data management and analysis across disparate space-science data platforms. It provides a
> consistent `Instrument` interface for finding, downloading, loading, cleaning, managing, processing,
> and analyzing time-indexed scientific measurements, with support for pandas and xarray data
> structures, metadata handling, orbit/day/file iteration, and custom processing functions. The core
> package supplies reusable I/O, metadata, file-management, orbit, constellation, and coordinate
> utility APIs, while the broader pysat ecosystem provides plug-ins for public scientific datasets and
> analysis workflows, including NASA, Madrigal, CDAAC, model, mission, and space-weather packages.

The description is supported throughout by `README.md`, `docs/introduction.rst`, `docs/api.rst` and
`docs/ecosystem.rst` at the source revision. Its last sentence is doing real work: it is the place
where the record tells a reader that the archive and mission support lives in plug-ins, which is why
Fields 17, 18 and 31/32 do not claim it.

### 9. Concise Description (OPTIONAL)

> Pysat is an easy to use interface to manage all aspects of space science, from beginning to end.
> This includes downloading, loading, managing, processing, and analyzing satellite and related data.

Retained as written. **Considered and not selected:** a re-worded alternative drafted in the previous
extraction ("Python framework for downloading, loading, managing, processing, and analyzing satellite
and space-science data across instrument plug-ins."). It is a stylistic variant, not a correction —
the stored text is accurate and reads as maintainer-voiced, and the sentence-initial capital in
`Pysat` matches the project's own usage in the README (`Pysat's plug-in design allows analysis support
for any data, including user provided data sets.`). Rewriting subjective prose without a factual
reason is not an improvement.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2015-04-18

The form defines this field as the date of first broadcast or publication, used for the *initial*
version of the software. 2015-04-18 is independently corroborated twice: the earliest git tag in the
repository, `v0.1.2.3`, has creator date 2015-04-18 (42 tags total, newest `v3.2.2`); and the first
PyPI upload of pysat, version 0.1.0, is timestamped 2015-04-18. The GitHub repository was created
2015-04-05, thirteen days earlier — that is the repository's birth, not a release.

**Considered and rejected — 2018-03-16, the first Zenodo deposit.** The concept DOI
10.5281/zenodo.1199703 has 21 versions and its earliest is version 0.7.0, DOI
10.5281/zenodo.1199704, titled `rstoneback/pysat: ICON Release`, issued 2018-03-16. **This is the
trap in this field**: the Publisher in Field 11 *is* Zenodo, which makes the first Zenodo deposit look
like the natural publication date, and a future agent working from the DOI alone will be tempted to
"fix" 2015 to 2018. It would be wrong. pysat was publicly released, tagged and distributed for nearly
three years before it was ever deposited in Zenodo; the DOI records when archiving began, not when the
software was first published.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

The DataCite record for the concept DOI gives publisher Zenodo. The deposit is a
GitHub-integration deposit — its sole related identifier is
an `isSupplementTo` relation pointing at `https://github.com/pysat/pysat/tree/v3.2.2` — but that
changes nothing here: Zenodo is the publisher of the archived record either way.

### 12. Version (RECOMMENDED)
- **Version Number:** v3.2.2
- **Version Date:** 2025-03-20
- **Version Description:** Bug-fix and maintenance release that includes test data in the source distribution, updates `.gitignore`, updates Zenodo affiliations and references, clarifies the public-release statement, and updates operational tests for Python 3.9 and Ubuntu 22.04.
- **Version PID:** https://doi.org/10.5281/zenodo.15059161

v3.2.2 is the newest of the repository's 42 tags, it resolves to the source revision itself, and it is
the latest GitHub release (published 2025-03-20, targeting `main`). `pyproject.toml` and `setup.cfg`
declare the version as `3.2.2`, and the PyPI 3.2.2 artefacts were uploaded 2025-03-20. The version
description paraphrases the `[3.2.2] - 2025-03-20` block of `CHANGELOG.md`, whose last line is
`  * Updated Ops tests to new lower limit of Python 3.9 and Ubuntu 22.04`.

**Why 2025-03-20 and not 2025-03-07.** The wiki's `v3.2.2-Release-text.md` heads its change list
`[3.2.2] - 2025-03-07`. That draft date was superseded: `CHANGELOG.md` in the released tree, the git
tag, the GitHub release and the Zenodo deposit all say 2025-03-20.

**A single version entry is the correct representation.** Before this refresh the record carried
**two** attached version entries for pysat, and the two were byte-identical across every part a reader
sees — same version number, same release date, same version PID, same description. That is what makes
one entry lossless rather than lossy: the second row asserted nothing the first did not, so collapsing
them discards no information. pysat released v3.2.2 once, and one entry is what the software's release
history supports; the duplicate was an artefact of how the entry was originally loaded.

**v3.2.3 is drafted but not released — expect it at the next refresh.** The wiki contains a complete
`v3.2.3-Release-Text.md` (bug fixes plus maintenance, including cycling Python support to 3.10–3.14),
and a release-candidate branch `rc_v323` exists. But there is **no v3.2.3 tag, no GitHub release and
no PyPI artefact**, so v3.2.2 remains the released version. A future refresh should check for the tag
first rather than reading the wiki text as evidence of a release.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x**

`pyproject.toml` sets `requires-python = ">=3.9"` and classifies Python 3.9 through 3.12; PyPI reports
the same `requires_python`. The package contains no compiled extension and no second language.
`Python 2.x` was considered and rejected: pysat 3.x dropped Python 2 entirely. The surviving mentions
of it are historical — `docs/release_notes.rst` recording that v2.3.0 began deprecating Python 2.x
support, and the wiki's `Version-Restrictions.md`, which predates the v3.0 rewrite.

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.1029/2018JA025297

Stoneback, R. A., Burrell, A. G., Klenzing, J., and Depew, M. D. (2018), *PYSAT: Python Satellite Data
Analysis Toolkit*, Journal of Geophysical Research: Space Physics, 123(6), 5271–5283.
`docs/citing.rst` instructs users to cite this paper when referring to the software package, and it is
the first entry in the `references` array of `.zenodo.json`. It is also listed as an output of NSF
award 1259508 in that award's public record (see Field 26).

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License

The `LICENSE` file at the source revision is the three-clause BSD text, copyright 2016 Russell
Stoneback; `pyproject.toml` carries the classifier `License :: OSI Approved :: BSD License`; GitHub
resolves the repository licence to SPDX `BSD-3-Clause`; and the Zenodo v3.2.2 deposit records
`bsd-3-clause`. The recorded string reproduces the controlled-vocabulary row name character for
character, and that row uses straight ASCII quotation marks (U+0022) around `New` and `Revised` — all
four of them. The curly-quote trap that the licence field documentation warns about belongs to a
different row, `GNU Library or ‘Lesser’ General Public Licenses (LGPL version 2)` with its U+2018 and
U+2019 pair, not to this one. Replacing the straight quotes here with typographic ones would stop the
value matching its row and would fail the submission.

The SPDX page for this licence is https://spdx.org/licenses/BSD-3-Clause.html. It is recorded here as
evidence only: HSSI stores licence as a shared catalogue row that carries its own URL, so there is no
per-software licence URI to set.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

Recorded (24):

atmosphere · CubeSat · data analysis · data management · data retrieval · electric fields ·
heliophysics · heliosphere · instrument data · ionosphere · magnetosphere · metadata · models ·
nasa data · observations · orbit · plasma · radar measurements · satellite data · space physics ·
space science · space weather · thermosphere · time series

These are the stored strings, not the title-cased forms the record renders (`Nasa Data`, `Netcdf`,
`Pysat` are display artefacts, not values). Their sources are the eleven `pyproject.toml` /
`.zenodo.json` keywords, the sixteen repository topics the maintainers set on `pysat/pysat`
(`cubesat`, `electric-fields`, `ionosphere`, `magnetosphere`, `measurements`, `nasa`, `nasa-data`,
`netcdf`, `plasma`, `python`, `radar-measurements`, `satellite-data`, `science-research`, `space`,
`space-science`, `thermosphere`), and terms describing the workflow the README and documentation
describe.

The domain terms that look like plug-in territory — `electric fields`, `radar measurements`,
`nasa data`, `CubeSat` — are **kept deliberately**: they are repository topics the maintainers set on
the *core* repository, so they are the project's own statement of the audience it serves, which is the
standard this field uses (scope note 2).

**Removed — `python`, `netcdf`, `pysat` and `solar wind`.** The record carried twenty-eight keywords
before this refresh; these four are not retained. Field 16 exists for science keywords *not supported
by other metadata fields*, and each of the four is either fully carried elsewhere or unsupported by
the core package.
- `python` — Field 13 already records Python 3.x, in the same word.
- `netcdf` — Fields 18 and 19 already record netCDF3/4, and the format is the substance of both.
- `pysat` — the software's own name, already Field 7. A keyword that repeats the record's title
  cannot narrow a search that already found it.
- `solar wind` — not in the project's declared keywords, not a repository topic, and unsupported by
  core code: `solar wind` occurs on exactly **one line** across `pysat/`, `docs/` and `README.md`, in
  `docs/tutorial/tutorial_constellation.rst`, describing an ACE real-time example built from
  **pysatSpaceWeather** instruments. It was removed on the same reasoning as the Field 22 removal, and
  the two were decided together.

The alternative for the first three — keeping them because a redundant keyword is harmless — was
rejected: a keyword that duplicates a dedicated field adds nothing a searcher can use, and this field
is the one place where a record can say something the other thirty-two fields cannot.

**Considered and not added:** the repository topics `measurements`, `nasa`, `science-research` and
`space`, and the package keywords `satellites` and `analysis`. Each is either too vague to narrow a
search or a near-duplicate of a stored keyword (`satellite data`, `data analysis`). `in situ
measurements` exists as a vocabulary row and is tempting — `docs/introduction.rst` says pysat was
initially designed for in situ satellite measurements — but the same sentence goes on to say it has
grown beyond that, so the term now describes the project's origin rather than its scope.

### 17. Data Sources (OPTIONAL)

- **Other**

Core pysat's data source is **the user's own filesystem, plus whatever a plug-in implements**. The
distribution contains no network client: `requests` and `urllib` appear **0 times** in the package
source at the source revision, and the one case-insensitive match for `ftp` is a comment in the
plug-in template about setting a CI test flag for instruments that download over FTP.
`Instrument.download` builds the date range, ensures the data directory exists, and then calls
`self._download_rtn` — the download function the instrument module supplied. **None of the download
functions shipped in the package transfers any data.** There are six of them:
`pysat.instruments.methods.testing.download`, documented as
`Pass through when asked to download for a test instrument.`; the three test instruments
(`pysat_testing`, `pysat_ndtesting`, `pysat_testmodel`), which alias that one through
`functools.partial`; `pysat.instruments.pysat_netcdf.download`, documented as
`Download data from the remote repository; not supported.` and doing nothing but raising a warning;
and the stub in `pysat/instruments/templates/template_instrument.py`, which likewise only warns.
`Other` is the honest value for that.

**Removed — `CDAWeb`, `Madrigal`, `HTTP/HTTPS Directories`, `Observatory/Mission-specific`.** The
record listed all four alongside `Other` before this refresh; none is retained, because none is
reachable from a pysat-only installation.
- `CDAWeb` appears in the package solely inside `pysat/instruments/templates/template_instrument.py`,
  in comments explaining that a metadata dictionary follows NASA CDAWeb's labelling conventions — a
  template for someone writing a plug-in. `CHANGELOG.md` records that the CDAWeb methods were moved
  out of core years ago. CDAWeb access is pysatNASA's.
- `Madrigal` appears **0 times** anywhere under `pysat/` at the source revision. Case-insensitive
  matches exist in eight files under `docs/`, and each of those passages is about the
  **pysatMadrigal** package or about the Madrigal database that package reads — never about a
  capability of the core distribution.
- `HTTP/HTTPS Directories` — see the absence of any HTTP client above.
- `Observatory/Mission-specific` — the package ships no observatory or mission instrument module, and
  the form ties this value to naming the observatory in Field 32, which is correctly empty.

**The alternative was to keep all four on the grounds that pysat is the front door to those
archives** — a user does reach CDAWeb and Madrigal *through* pysat, once the right plug-in is
installed. It was rejected because Field 17 is a capability field under scope note 1 and the honest
test is what `pip install pysat` alone can reach: a searcher who filters on `Madrigal` and clicks
through to pysat would find a promise the distribution does not keep, while pysatMadrigal keeps it
and carries its own record. This was decided together with removing `CDF` from Field 18 and leaving
Fields 22 and 31/32 empty, and it binds them together: if a future refresh decides a framework may
claim its plug-ins' reach, it has to restore all of these at once and reopen those fields with it.

**Why this does not contradict Field 4's `Data Access and Retrieval`.** The retrieval *machinery* —
`download`, `remote_file_list`, `remote_date_range`, file discovery and caching — is genuinely pysat's
and is user-facing. The *endpoints* are not. Field 4 describes what the software does; Field 17 names
the archives it can reach.

**Considered and not selected:** `FTP/FTPS Directories`, `HAPI`, `OMNIWeb`, `SSCWeb`, `AMDA`, `GFZ`,
`WDC`, `das2`, `TAP`, `VirES`, `S3/Cloud-aware`, `The Virtual Solar Observatory.` — no core code
touches any of them. The PyHC core registry lists `ace`, `de2`, `dmsp`, `icon`, `madrigal`, `omni`,
`sami2` and `tiegcm` among pysat's registry keywords; that list is a discovery aid describing what the
pysat *ecosystem* reaches, and it is not evidence about the core distribution.

### 18. Input File Formats (RECOMMENDED)

- **ascii**
- **csv**
- **netCDF3/4**
- **Other**

- `netCDF3/4` — `pysat.utils.io.load_netcdf`, `load_netcdf_pandas` and `load_netcdf_xarray` read
  netCDF with a selectable `file_format`, and the `pysat_netcdf` general instrument exists to load
  pysat-written netCDF files. `netCDF4` is the only third-party file-format library imported anywhere
  in the package: the third-party imports in `pysat/utils/io.py` are `netCDF4`, `numpy`, `pandas` and
  `xarray`, and no other module in the package imports a format reader.
- `csv` — `pysat.instruments.methods.general.load_csv_data` reads a list of CSV files into one
  DataFrame, and `Meta.from_csv` reads a metadata table from delimited text.
- `ascii` — recorded because both of those readers pass user-supplied keyword arguments straight to
  `pandas.read_csv` (`read_csv_kwargs`, and `sep` for `Meta.from_csv`), so arbitrary delimited plain
  text, not only comma-separated text, can be read. It is close to `csv` but not redundant with it.
- `Other` — the `Instrument` contract lets a plug-in's `load` function return data from any format at
  all, which is exactly what `Other` is for.

**Removed — `CDF`.** The record listed CDF among the input formats before this refresh; it is not
retained, because pysat cannot read CDF. No CDF library is imported anywhere in the package; `cdflib`
appears **0 times** across `pysat/`, `docs/`, `README.md`, `pyproject.toml` and `requirements.txt` at
the source revision. CDF support is what **pysatCDF** exists for — the ecosystem status chart
classifies it as an Interface Code, and it reads NASA CDF files and hands them to pysat through
`to_pysat()`. A searcher filtering on CDF wants software that opens a CDF file; pysat is not that
software, pysatCDF is, and pysatCDF is listed in Field 30. The alternative — keeping CDF because a
pysat user who also installs pysatCDF ends up with CDF data in an `Instrument` — was rejected for the
reason given in Field 17: this field records what the distribution itself can read.

**Considered and not selected:** `HDF5`, `FITS`, `IDL.sav`, `JSON`, `Zarr` — none is read by core
code. (`json` is imported in the package, but for pysat's own parameter and file-list bookkeeping, not
as a science data format.)

### 19. Output File Formats (RECOMMENDED)

- **ISTP-Compliant**
- **netCDF3/4**

`Instrument.to_netcdf4` and `pysat.utils.io.inst_to_netcdf` write netCDF4, translating pysat metadata
into file attributes on the way out. `docs/tutorial/tutorial_files.rst` states that
`pysat's default conventions are a simplified implemention of the standards` developed for NASA's
Ionospheric Connections Explorer mission, and goes on to say that the primary underlying standards
come from the SPDF ISTP/IACG conventions — which is what `ISTP-Compliant` names. `docs/roadmap.rst`
repeats that pysat is capable of maintaining compliance with SPDF formatting requirements.

**Considered and not selected — `csv`.** `Files._store` writes the file list to CSV with
`pandas.to_csv`, but that is pysat's internal bookkeeping in the user's pysat directory, not a science
data product a user asks for. There is no public CSV writer.

### 20. Operating System (RECOMMENDED)

- **Linux**
- **Mac**
- **Windows**

`pyproject.toml` carries the three classifiers `Operating System :: MacOS :: MacOS X`,
`Operating System :: POSIX :: Linux` and `Operating System :: Microsoft :: Windows`, and
`.github/workflows/main.yml` runs the full test suite on an
`os: ["ubuntu-latest", "windows-latest", "macos-latest"]` matrix, plus `ubuntu-22.04` for the
operational-compliance configuration.

**Considered and not selected — `Operating System Independent`.** It is a defensible reading of a
pure-Python package, but the project makes three specific commitments and tests all three; naming them
is more informative to a reader than the abstract row, and it is what the project's own classifiers
say.

### 21. CPU Architecture (RECOMMENDED)

- **CPU Independent**

pysat is pure Python: `setup.py` is a three-line shim delegating to `setuptools`, there is no compiled
extension, no C or Fortran source, no GPU code, and no MPI in the tree. Dependencies may ship
architecture-specific wheels, but pysat imposes no architecture restriction of its own.

### 22. Related Phenomena (OPTIONAL)

- Not found

**This field is deliberately empty, and its emptiness is evidenced.** The vocabulary is a **closed**
seven-value list — Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms, Solar Corona, Solar
Flares, Solar Wind, X-ray emission — and nothing outside it can be entered. Not one of the seven is
supported by the core distribution, which is why no value is recorded rather than a near-miss being
chosen.

**Removed — `Solar Wind` and `Geomagnetic Storms`.** The record held these two before this refresh;
neither is retained. Core pysat contains no phenomenon-specific science at all. Case-insensitive
searches across `pysat/`, `docs/` and `README.md` at the source revision return: `storm` **0 matching
lines**; `aurora` **0 matching lines**; `flare` **1 matching line**, the column-header line of a
space-weather test data file (`pysat/tests/test_data/sw/f107/daily/f107_daily_2019-03-16.txt`); and
`solar wind` **1 matching line**, in `docs/tutorial/tutorial_constellation.rst`, describing an ACE
real-time constellation assembled from **pysatSpaceWeather** instruments. A visitor browsing HSSI for
`Geomagnetic Storms` is looking for storm science and would find a general data framework out of
place.

The remaining rows are ruled out the same way. `Solar Flares` is already covered by the `flare`
search above. For the other four, `corona` — which subsumes `Coronal Heating`, `Coronal Mass
Ejections` and `Solar Corona` — returns **0 matching lines** across `pysat/`, `docs/` and
`README.md`, as do `x-ray` and `xray` for `X-ray emission`. That is what licenses the categorical
statement above: the emptiness of this field was checked row by row against the whole closed list,
not assumed from the two values that happened to be stored.

The alternative — keeping both because the ecosystem reaches solar-wind and geomagnetic-index
data through its plug-ins — was considered and rejected: this is a capability field under scope note
1, and the plug-ins carry their own records. Restoring either value here would require restoring
Fields 17, 18 and 31/32 on the same reasoning.

An empty Related Phenomena is the correct outcome for a phenomenon-agnostic framework, not a gap. It
is also why the free-text terms that most readily suggest themselves for pysat — ionosphere,
thermosphere, magnetosphere, heliosphere, solar wind, space weather, satellite observations, ion
drifts, plasma parameters — could never have been stored here: eight of those nine are not rows in the
vocabulary at all, and the field rejects anything that is not. Terms like those belong in Keywords,
which is the only open vocabulary in the form.

### 23. Development Status (RECOMMENDED)

- **Active**

The vocabulary's definition of `Active` is *The project has reached a stable, usable state and is being
actively developed.* Both halves hold.

**Do not read development status from `main` alone.** pysat runs a git-flow branching model, which the
wiki's `Versioning-Philosophy.md` documents in terms of pulls into master and pulls into develop:
release branches receive only releases, and all day-to-day work happens on `develop`. As a result
`main` has **0 commits** after the source revision — the v3.2.2 release commit of 2025-03-20 — while
`origin/develop` has **197 commits** after it, the newest dated 2026-08-21. `origin/rc_v323` sits at
that same commit, staging the v3.2.3 release described in Field 12. GitHub reports the repository as
not archived, with `pushed_at` 2026-08-21. An agent that looked only at `main` would conclude the
project had been dormant for eighteen months and would wrongly propose `Inactive`; it has not been
dormant for a day.

Supporting signals: `Development Status :: 5 - Production/Stable` in `pyproject.toml`; the PyHC core
registry rates pysat Good on all six of its axes (community, documentation, testing, software
maturity, Python 3, license); CI runs on every push and pull request.

**Considered and not selected:** `Inactive` (refuted above), `Unsupported` (whose definition requires
that the authors have ceased all work and that a new maintainer *may be* desired — neither is true),
`WIP` (there are 42 tagged releases).

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://pysat.readthedocs.io/en/latest/

Declared in `pyproject.toml` under `[project.urls] Documentation`, built from `docs/` by
`.readthedocs.yml`, linked from the README, and listed as `docs` in the PyHC core registry (as
`https://pysat.readthedocs.io`, which redirects to the same place). The site
carries installation instructions (`docs/installation.rst`, `docs/quickstart.rst`) as well as the API
and tutorials, which is what this field asks for.

The **wiki** (`https://github.com/pysat/pysat/wiki`) is a second, maintainer-authored source — release
checklists, governance, versioning philosophy, meeting notes and the ecosystem status chart — but it
is developer-facing process documentation, not user documentation, so it is cited as evidence in this
dossier rather than recorded as the Field 24 value.

### 25. Funder (OPTIONAL)

`ACKNOWLEDGEMENTS.md` at the source revision opens with
`The following institutions, missions, and programs have provided funding` for pysat development, and
then lists institutions, missions and programs separately. Everything below is drawn from that
statement; the 2023 *Frontiers* ecosystem paper's funding section corroborates DARPA's Defense
Sciences Office, the two Naval Research Laboratory awards, the Office of Naval Research, the Space
Precipitation Impacts project at Goddard, and the two NASA grants held by J. Smith.

Acronyms are expanded to full institutional names, as the field requires.

1. **Catholic University of America** — https://ror.org/047yk3s18
2. **Cosmic Studio** — no ROR record found
3. **Defense Advanced Research Projects Agency Defense Sciences Office** — no identifier
4. **Goddard Space Flight Center** — https://ror.org/0171mag52
5. **National Aeronautics and Space Administration** — https://ror.org/027ka1x80
6. **National Oceanic and Atmospheric Administration** — https://ror.org/02z5nhe81
7. **Office of Naval Research** — https://ror.org/00rk2pe57
8. **U.S. National Science Foundation** — https://ror.org/021nxhr62
9. **United States Naval Research Laboratory** — https://ror.org/04d23a975
10. **NASA Ionospheric Connections Explorer (ICON)** — no identifier
11. **NASA Scintillation Observations and Response of the Ionosphere to Electrodynamics (SORTIE)** — no identifier
12. **NASA Scintillation Prediction Observations Research Task (SPORT)** — no identifier
13. **NOAA Constellation Observing System for Meteorology Ionosphere and Climate (COSMIC-2)** — no identifier

**Why the United States Naval Research Laboratory is recorded.** Before this refresh the funder list
held twelve organisations and this laboratory was not among them. It belongs there because two primary
sources say plainly that it paid for pysat work. The 2023 *Frontiers* funding statement says
R. Stoneback `was supported by the Naval Research Laboratory, N00173191G016 and N0017322P0744`, and
`ACKNOWLEDGEMENTS.md` at the source revision — a file whose opening sentence declares that everything
it lists provided funding — carries, under its Programs heading, the entry
`Naval Research Laboratory N00173191G016 and N0017322P0744`.

**Its absence was not already covered by the Office of Naval Research.** The same file lists
`Office of Naval Research (ONR)` under Institutions, and it is recorded at entry 7; the Frontiers
statement credits ONR separately, for A. Burrell rather than R. Stoneback. The two are different
organisations with
different ROR records — https://ror.org/00rk2pe57 for the Office of Naval Research, a government
funding office, and https://ror.org/04d23a975 for the laboratory itself. Treating ONR's presence as
covering the laboratory was the alternative on offer, and it was rejected on that evidence: it would
have credited the wrong body and lost a funder both sources name.

**Copy the organisation name exactly: `United States Naval Research Laboratory`.** That is the ROR
display name for https://ror.org/04d23a975 and the form this field takes, in keeping with the rule
above that acronyms and short forms are expanded. The shorter string `U.S. Naval Research Laboratory`
does occur elsewhere in this dossier, but never as a value of this field: Field 6 quotes it as the raw
affiliation string `.zenodo.json` gives for A. Burrell, and Field 26 carries it inside the award
titles `U.S. Naval Research Laboratory award`, which name a different kind of object and are correct
as they stand. Do not carry the short form into this field, and do not shorten this field's value to
match those titles.

**Why the four missions are funders and not observatories.** ICON, SORTIE, SPORT and COSMIC-2 appear
in `ACKNOWLEDGEMENTS.md` under a heading of Missions, inside a section whose opening sentence declares
that everything listed provided *funding*. They are named as sources of money, not as data pysat
reads. **A future refresh must not promote them into Fields 31/32 on the strength of these entries.**

**Two identifier gaps that are database matters, not values.** `Cosmic Studio` and the DARPA sub-office
row both lack identifiers. Cosmic Studio has no ROR record at all. The DARPA entry names the Defense
Sciences Office, an office within an agency; DARPA itself has a ROR, but attaching it would assert that
the office and the agency are the same organisation, and supplying an identifier for an existing
identifier-less row creates a second row rather than updating the first.

### 26. Award Title (OPTIONAL)

Nine awards. Award numbers come from the Programs section of `ACKNOWLEDGEMENTS.md`, with two
corrections documented below; titles come from the funding agencies' own award records where one
exists.

1. **Collaborative Research: Inferring High Latitude Convection Patterns Using SuperDARN, DMSP and ACE** — 1259508 (U.S. National Science Foundation)
2. **Collaborative Research: CEDAR--Assimilative Analysis of Low- and Mid-latitude Ionospheric Electrodynamics** — AGS-1651393 (U.S. National Science Foundation)
3. **NASA grant** — NNX10AT02G
4. **NASA ROSES-2020 B.5 Living With a Star Science program element** — NNH20ZDA001N-LWS
5. **NASA grant** — 80NSSC18K1203
6. **NASA Goddard Space Flight Center HSD Support Partnership** — 80NSSC21M0180
7. **U.S. Naval Research Laboratory award** — N00173191G016
8. **U.S. Naval Research Laboratory award** — N0017322P0744
9. **Space Precipitation Impacts (SPI)** — no award number

**Two award numbers deliberately differ from the repository, and the record is right and the
repository is wrong.** It is one of the likeliest things for a future refresh to "correct" back into
an error, so the evidence is set out in full.

`ACKNOWLEDGEMENTS.md` at the source revision contains these two lines:

- ` - NSF 125908, AGS-1651393`
- ` - NASA NNX10AT02G, NNH20ZDA001N-LWS, 80NSSC18K120, and 80NSSC21M0180`

Both `125908` and `80NSSC18K120` are digit-truncated typos:

- The NSF award API returns **0 awards** for `id=125908`. For `id=1259508` it returns a real award to
  the University of Texas at Dallas, PI Russell A Stoneback, titled *Collaborative Research:
  Inferring High Latitude Convection Patterns Using SuperDARN, DMSP and ACE*, whose public project
  outcomes report states that the DINEOF analysis procedure was built on top of the Python Satellite
  Data Analysis Toolkit (pysat) and lists the 2018 JGR pysat paper (10.1029/2018JA025297) among its
  outputs. That is a direct, documented link between this award and this software.
- A USAspending search for `80NSSC18K120` returns **0 results**; `80NSSC18K1203` returns a real NASA
  award to the University of Texas at Dallas.

A user reading pysat's page needs an award number they can look up. The truncated strings resolve to
nothing at either agency; the corrected ones resolve to the actual grants that paid for the work.

**Do not treat the two NSF titles as verbatim quotations of NSF.** NSF's own award records print
**two** spaces after `Collaborative Research:`; the record stores one. That is trivial whitespace
normalisation, not a data difference, and it is **not** something a later refresh should "correct" —
but it does mean the stored titles must never be presented as byte-exact quotations of the NSF award
API.

**Why four awards carry agency-style labels instead of titles.** Awards 3, 5, 7 and 8 appear in
`ACKNOWLEDGEMENTS.md` as bare numbers with no title anywhere in the project's materials, and no public
title was found in NASA or Naval Research Laboratory records. `NASA grant` and
`U.S. Naval Research Laboratory award` preserve the award numbers without inventing titles. The two
Naval Research Laboratory numbers are corroborated by the Frontiers paper's funding section.

**Why award 9 has no number.** `ACKNOWLEDGEMENTS.md` describes the NASA Space Precipitation Impacts
project at Goddard Space Flight Center as funded through the Heliophysics Internal Science Funding
Model — internal funding, which carries no external award number. The Frontiers paper says the same.
An award with no title cannot be stored at all, so the project name serves as the title and the number
is legitimately absent.

**Do not read pysat's functionality out of these titles.** Award 2's title contains the phrase
*Assimilative Analysis*, and its NSF abstract is about data assimilation into TIEGCM. That describes
the funded research, not the software: pysat contains no assimilation code (see Field 4).

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **DOI:** https://doi.org/10.3389/fspas.2023.1119775

Stoneback, R. A., Burrell, A. G., Klenzing, J., and Smith, J. (2023), *The pysat ecosystem*, Frontiers
in Astronomy and Space Science, 10:1119775. It is the second entry in the `references` array of
`.zenodo.json`, is linked from the README, and `docs/citing.rst` says citing it may also be
appropriate depending on usage. It describes the plug-in ecosystem rather than the core framework,
which is exactly what makes it a *related* publication while the 2018 JGR paper is the *reference*
publication.

No further publications are recorded: `docs/citing.rst` and `.zenodo.json` name these two and no
others.

### 28. Related Datasets (OPTIONAL)
- Not found

The distribution ships no scientific dataset. What it does ship is test fixtures: synthetic data
generated on the fly by `pysat/instruments/methods/testing.py`, a handful of small space-weather index
text files under `pysat/tests/test_data/`, and one instrument metadata table (see Field 31). None is a
citable dataset, and none has a DOI or a landing page. Datasets belong to the plug-in packages that
provide access to them.

### 29. Related Software (OPTIONAL)
- Not found

This field is for software performing *similar tasks* that does not necessarily link together, for
predecessors and forks, and for **important** domain-specific dependencies. pysat has none of these
at the source revision, and the emptiness is evidenced rather than assumed.

**Negative research — similar-purpose tools.** Case-insensitive searches across `pysat/`, `docs/`,
`README.md`, `pyproject.toml` and `requirements.txt` at the source revision return **0 matches** for
each of `sunpy`, `spedas`, `spacepy`, `hapi`, `kamodo`, `heliopy` and `cdflib`. pysat neither compares
itself to, nor bridges to, any peer framework in its own materials. There is no predecessor project
and nothing was forked.

**Considered and not selected — `netCDF4`.** It is the one dependency pysat itself sets apart: the
README's prerequisite table is headed `| Common modules | Community modules |` and netCDF4 is the sole
entry in the Community column, i.e. the project's own label for a module developed by and for the
space physics community. That is a real argument for calling it a domain dependency. It is
nevertheless excluded, because the entire relationship is *reading and writing a file format*, which
Fields 18 and 19 already record in more useful detail, and because netCDF4 is general-purpose
scientific I/O plumbing that would be equally at home outside heliophysics. Listing it would tell a
reader nothing that `netCDF3/4` in Fields 18 and 19 does not tell them better.

**Not relocated here from Field 30.** The packages excluded from Field 30 below are excluded from this
field by the same rule — a package rejected from Interoperable Software does not thereby become
Related Software.

### 30. Interoperable Software (OPTIONAL)

- https://github.com/pysat/pysatCDAAC
- https://github.com/pysat/pysatCDF
- https://github.com/pysat/pysatMadrigal
- https://github.com/pysat/pysatModels
- https://github.com/pysat/pysatNASA
- https://github.com/pysat/pysatSpaceWeather
- https://github.com/pysat/pysatSeasons
- https://github.com/pysat/pysatMissions
- https://github.com/pysat/pysatIncubator
- https://github.com/pysat/pysatKamodo
- https://github.com/pysat/pysatAMISR

**Why repository URLs and not DOIs.** The entry page renders a related item's raw URL as its own link
text, so a repository URL is legible to a visitor while a DOI is an opaque string. Where a package is
itself in the HSSI catalogue, the URL used is that entry's own stored code repository URL, so the two
records point at each other with the same string. If HSSI ever renders resolved titles instead of raw
URLs, that trade-off inverts and DOIs would win on persistence — that is the reason to revisit this
choice.

**The relationship, and why it clears the bar.** These are not dependencies of pysat; pysat is *their*
dependency, and the exchange runs in both directions and is documented on both sides.
`docs/dependency.rst` is an entire chapter on building a package against pysat: a plug-in supplies
instrument modules that `pysat.utils.registry.register` loads into pysat's own namespace, so
`pysat.Instrument(platform=..., name=...)` returns that package's data through pysat's `Instrument`
API. In the other direction, pysat ships test instruments and the reusable test class
`pysat.tests.classes.cls_instrument_library.InstLibTests` specifically so that downstream packages can
run pysat's standard instrument test suite against their own modules; the same page notes that
pysatModels uses pysat's test instruments in its unit tests. `docs/ecosystem.rst` states that
`pysat supports many different data sets as Instruments and Constellations.` and explains that the
split into separate packages exists to limit how many dependencies a user must install.

**Three evidence tiers, and they are not equally strong.** The line between them is structural rather
than a matter of how often a name is typed: a package either **has its own documentation page in the
pinned tree or it has none**. `docs/instruments/` and `docs/analysis/` at the source revision together
hold pages for exactly eight distinct ecosystem packages — pysatCDAAC, pysatIncubator, pysatMadrigal,
pysatMissions, pysatModels, pysatNASA, pysatSeasons and pysatSpaceWeather. (Those two directories hold
two further files, `general_instruments.rst` and `testing_instruments.rst`, which describe pysat's own
shipped instruments rather than packages.) `pysatCDF`, `pysatKamodo` and `pysatAMISR` have no
documentation file anywhere under `docs/`. That structural fact is what the tiering rests on, and
unlike an occurrence count it cannot drift as prose is edited. Before this refresh the record held
seven of the eleven; the evidence for each of the other four is set out in its tier below.
Per-package evidence is from the source revision unless noted.

**Tier 1 — a documentation page of its own in the pinned tree.** Each of the eight below has a page
under `docs/instruments/` or `docs/analysis/`, and each is listed in a toctree of `docs/ecosystem.rst`,
which is the project's own statement of the ecosystem it supports. Those toctrees reference ten
distinct `pysat*` pages in all: `pysatCDAAC`, `pysatEcosystem_Template`, `pysatIncubator`,
`pysatMadrigal`, `pysatMissions`, `pysatModels`, `pysatNASA`, `pysatSeasons`, `pysatSpaceWeather` and
`pysatTutorials`. Eight of those ten are code packages and are recorded here; the remaining two are
excluded below, with reasons.

- **pysatCDAAC** — `docs/instruments/pysatCDAAC.rst`: provides pysat support for COSMIC data products
  at CDAAC, as `Instrument` and `Constellation` modules.
- **pysatIncubator** — it has a page of its own, `docs/instruments/pysatIncubator.rst`, which
  describes it as holding pysat Instruments the team intends to package properly, several of which are
  `fully functional and can be used.` `docs/ecosystem.rst` lists that page in the Supported
  Instruments toctree alongside the released instrument libraries. It is a real pysat plug-in
  repository, released on PyPI as `pysatIncubator` 0.0.1 with its `home_page` set to
  `https://github.com/pysat/pysatIncubator`. The wiki chart separately places it in the
  `Development Area` as `pysatIncubator (pre-release)`, and its pre-release status is the reason
  someone might disagree with recording it. **That status does not lower its evidence tier**: it has
  exactly the documentation-page evidence every other Tier 1 package has, and it should not be
  grouped with pysatKamodo and pysatAMISR, which have none.
- **pysatMadrigal** — `docs/instruments/pysatMadrigal.rst`: provides pysat instrument modules for the
  Madrigal database. The tutorials show the round trip end to end, registering
  `pysatMadrigal.instruments.dmsp_ivm` and `jro_isr` and then driving them through pysat.
- **pysatMissions** — documented twice in `docs/ecosystem.rst`, under Supported Instruments
  (`docs/instruments/pysatMissions.rst`: `Instrument` modules generating simulated orbital data) and
  under Analysis Tools (`docs/analysis/pysatMissions.rst`: building simulated satellites
  from Two-Line Elements and incorporating empirical model parameters). `docs/dependency.rst` uses
  `pysatMissions.instruments.missions_sgp4` as a worked example of testing a plug-in against pysat.
  Released on PyPI as `pysatMissions` 0.3.5 with `Source` pointing at this repository; the wiki chart
  rates it `pysatMissions (beta)`, and its GitHub description is
  `Mission planning instrument tools for pysat`. Of the four the record did not carry before this
  refresh — pysatMissions, pysatIncubator, pysatKamodo and pysatAMISR — it is the only one the wiki
  chart does not mark pre-release, and the only one whose released distribution is above 0.0.1; it was
  last pushed 2025-01-13. Its earlier absence was a straightforward omission rather than a judgement.
- **pysatModels** — `docs/analysis/pysatModels.rst` and `docs/instruments/pysatModels.rst`: a pysat
  interface for model analysis and model-data comparison that accepts model input as an xarray Dataset
  and compares it against truth data taken from a pysat object.
- **pysatNASA** — `docs/instruments/pysatNASA.rst`: `Instrument` and `Constellation` modules for
  several NASA missions.
- **pysatSeasons** — `docs/analysis/pysatSeasons.rst`: the ecosystem's seasonal-analysis package,
  operating on loaded pysat objects. It is where the binning and averaging routines that once lived in
  core now reside.
- **pysatSpaceWeather** — `docs/instruments/pysatSpaceWeather.rst` and
  `docs/analysis/pysatSpaceWeather.rst`: registered instruments plus analysis routines for real-time
  and historic space weather indices. It is also the one ecosystem package pysat depends on in
  reverse, as a **test** extra in `pyproject.toml` (`pysatSpaceWeather<0.1.0`), which exercises the
  plug-in contract in pysat's own CI.

**A note that applies to both tiers below.** The wiki's `pysat-Ecosystem-Status-Chart.rest` is the page
`docs/ecosystem.rst` itself links to as `ecosystem status chart`, and it is maintainer-authored, so it
is legitimate evidence — but it lives in a separate repository from the pinned code tree (scope
note 2), and it tracks repositories the documentation has not adopted. A reader should know that the
pinned documentation gives none of the three packages below a page of its own.

**Tier 2 — no documentation page; evidence is its own repository.** `pysatCDF` has no file under
`docs/`. Its name occurs on a single line in the pinned tree — a historical note in `CHANGELOG.md`
recording that pysatCDF was once a package requirement — and it is not in `docs/ecosystem.rst`. What
carries it is the adapter in its own repository, corroborated by the status chart.

- **pysatCDF** — the chart classifies it under `Interface Codes`, separate from the instrument
  libraries and analysis codes. It reads NASA CDF files and exports their data and
  metadata into pysat form through `to_pysat()`: an explicit adapter API, which is the textbook case
  for this field. **The direction of this relation is symmetric** — pysatCDF's own entry should
  list `https://github.com/pysat/pysat` in *its* Interoperable Software for the same reason. It is
  also the one of these eleven packages that already had a catalogue entry of its own when this
  refresh was made, which is why the URL recorded above is that entry's own stored repository URL.

**Tier 3 — no documentation page, and absent from the pinned tree altogether.** Neither `pysatKamodo`
nor `pysatAMISR` occurs anywhere in the tree at the source revision — not in `docs/ecosystem.rst`, not
in the changelog, and not even as the bare words `kamodo` and `amisr`. Their evidence is the
`Development Area` section of the wiki's ecosystem status chart, together with the integration code in
their own repositories, which is set out per package below.

- **pysatKamodo** — the chart lists it under `Development Area` as `pysatKamodo (pre-release)`. What
  justifies it is a concrete adapter in its own repository: `pysat_kamodo/pysat_kamodo.py` declares
  `class Pysat_Kamodo(Kamodo):`, builds `self._instrument = pysat.Instrument(**inst_kwargs)`, and
  pulls the keywords it forwards straight off pysat's own signature with
  `inst_kwarg_names = get_defaults(pysat.Instrument).keys()`; sibling modules
  `pysat_kamodo/madrigal.py` and `pysat_kamodo/nasa.py` do the same for pysatMadrigal and pysatNASA
  data. Its README states `This project tracks development of the kamodo-pysat interface.` and
  explains the division of labour — pysat retrieves, loads and cleans, while
  `Kamodo provides a math-oriented API for interpolation, function composition, and quick-look graphics.`
  That is a cross-package bridge to a named domain tool, which is what this field exists for. GitHub
  description `Pysat-Kamodo interface`; not archived; last pushed 2021-10-11.
  **It is published, but not under its repository name, and the identity evidence is thinner than it
  looks.** `https://pypi.org/pypi/pysatKamodo/json` returns 404; the distribution exists under the
  different name `pysat-kamodo`, at version 0.0.1. That record carries **no `Source` key at all** — its
  `home_page` and its one `project_urls` entry are both `https://pysat.github.io/pysatKamodo`, and its
  `summary` is `Kamodo api for pysat`. The tie between that distribution and this repository therefore
  rests on the pysat organisation's own GitHub Pages domain plus that summary string, **not** on a
  repository link: **do not write that a `Source` URL was matched to the repository**, because that
  evidence is not in the record, and a PyPI JSON 200 proves only that a name is taken, never that the
  name holds this software. **The durable trap worth carrying to other entries:** a sibling package
  can publish under a renamed distribution, so a name-keyed PyPI absence check yields a false
  negative — here `pysatKamodo` 404s while the software is on PyPI as `pysat-kamodo`.
- **pysatAMISR** — the chart lists it under `Development Area` as `pysatAMISR (pre-release)`. It is a
  genuine pysat plug-in: `pysatAMISR/isr_pf.py` is an instrument module whose docstring opens
  `Supports the Incoherent Scatter Radar at Poker Flat` and states
  `Downloads data from the SRI Madrigal Database.`, declaring the pysat `platform`/`name`/`tag` triple
  (`isr`, `pf`, tags `lp` and `ac`) and giving the worked call
  `dmsp = pysat.Instrument('isr', 'pf', 'lp', clean_level='clean')`. GitHub description
  `A module that allows ingestion of Advanced Modular Incoherent Scatter Radar data`; not archived;
  last pushed 2023-08-09. It is the weakest-evidenced entry in this field; the two facts that make it
  so, and the reason it is recorded in spite of them, are set out under *pysatAMISR's own README says
  it is not ready to use* below.

**Why the pre-release, dormant packages are recorded.** The wiki chart's `Development Area` holds
three packages — pysatIncubator, pysatKamodo and pysatAMISR — all marked pre-release, and two of the
three carry no released distribution under their repository name. All three are dormant by push date:
pysatIncubator last pushed 2021-09-10, pysatKamodo 2021-10-11, pysatAMISR 2023-08-09. None is
archived, and all three are real repositories with real pysat integration code. Note that a
pre-release marking on the chart says nothing about which evidence tier a package sits in:
pysatIncubator is Tier 1 on the strength of its own documentation page in the pinned tree, while
pysatKamodo and pysatAMISR are Tier 3.

The **alternative considered and not taken** was to record only the released packages: keep
pysatIncubator, which `docs/ecosystem.rst` names, and leave pysatKamodo and pysatAMISR out on the
ground that the pinned documentation is the project's authoritative statement of its supported
ecosystem while the status chart is a dashboard that also tracks repositories the project has not
adopted. It lost because it makes the record less useful than the evidence allows: a reader looking
for what pysat interoperates with is better served by the complete ecosystem picture, with each
entry's maturity stated, than by a shorter list that silently omits a working Kamodo bridge and an
AMISR instrument module. The maturity caveats above are how that completeness is kept honest.
**A later refresh should not quietly prune these three for being dormant** — dormancy was known and
weighed when they were recorded. What would justify removing one is archival, deletion, or evidence
that its pysat integration no longer works.

**pysatAMISR's own README says it is not ready to use, and the entry is recorded anyway. This was read
and weighed, not missed.** The warning is the single most likely reason a future agent would delete
this value, so it is set out here in full alongside the reasoning that survived it, rather than left
to be rediscovered. The `# Warning` section of the README in pysatAMISR's own repository — its own
repository, not the pinned tree — consists of one line:

> This module is currently in its inintial development stage and not ready to use.

The misspelling `inintial` is in the source **[sic]**. Quote it exactly or not at all: a later
quote-fidelity sweep that silently "repairs" it will turn a faithful quotation into an apparent
mismatch against the source.

The second fact is that **pysatAMISR has no PyPI distribution at all.**
`https://pypi.org/pypi/pysatAMISR/json` returns 404, even though the status chart carries a PyPI badge
pointing at a release for it. Only the JSON or Simple API can settle a question of absence — PyPI's
HTML project page answers 200 for names that were never registered, so it can never prove a name is
unpublished.

Both facts were in front of the decision, and the entry was kept regardless, for completeness of the
ecosystem picture. A reader asking what pysat interoperates with is better served by seeing an AMISR
instrument module that exists and is written to pysat's plug-in contract, labelled with its maturity,
than by a list that quietly omits it; the module's own immaturity is information about the module, not
a reason to hide that the bridge was built. **So a later refresh that rediscovers the warning should
not treat it as a discovery.** What would justify removing this entry is archival of the repository,
its deletion, or evidence that the pysat integration itself no longer works — not the maturity of the
module, which is already recorded above.

**Excluded, with reasons.**

- **pysatEcosystem_Template** — `docs/devel/pysatEcosystem_Template.rst` describes a repository of
  common files shared across ecosystem repositories so that a new package can be started from project
  standards. It is a file template, not installable software, and nothing is exchanged with it.
- **pysatTutorials** — `docs/devel/pysatTutorials.rst` describes a repository of Jupyter notebooks
  with tutorials and examples. Teaching material that *uses* pysat is not a peer tool that
  interoperates with it.
- **`ecosystem.txt`** at the source revision lists only five packages (pysatCDAAC, pysatMadrigal,
  pysatModels, pysatNASA, pysatSpaceWeather). It is a short machine-readable list used for
  documentation builds, and it is **stale relative to `docs/ecosystem.rst`**. Do not use it as the
  ecosystem inventory.

**Dependencies excluded, and the rule applied.**

- **numpy, pandas, scipy, pytest** — Tier A, never listable, no exceptions. This is the policy the
  form states, not a preference exercised here: being a dependency is not interoperability, and a
  claim that is equally true of most of the Python ecosystem carries no information about pysat.
- **portalocker** and **toolz** — not named in either tier, so the general test applies: both would be
  equally at home in a web app, a finance model or a biology pipeline (file locking and functional
  utilities), which makes them generic infrastructure and gives them Tier A treatment. `toolz` is in
  addition never imported anywhere in the package.
- **dask** — Tier B, and excluded on the facts. It is declared in `pyproject.toml` and
  `requirements.txt`, but `dask` is **never imported** in the package source at the source revision;
  its other appearances are dependency listings in `README.md` and `docs/installation.rst`, and the
  one passage that says what it is *for* is in `docs/roadmap.rst`, which describes integrating a
  format such as Dask as **future** work needed for data sets larger than memory. A declared
  dependency the code does not use cannot be a demonstrated exchange.
- **netCDF4** — Tier B; considered seriously because pysat's own README calls it a Community module
  (see Field 29), and excluded there for the same reasons.
- **xarray** — Tier B, and the closest call in this field, so the reasoning is recorded in full.
  The evidence *for* is real: `Instrument.data` is a `pandas.DataFrame` or an `xarray.Dataset`
  depending on `Instrument.pandas_format`; `docs/new_instrument.rst` makes returning one or the other
  the plug-in contract; `pysat.utils.io.load_netcdf_xarray` returns an `xr.Dataset`;
  `pysat.utils.coords.expand_xarray_dims` takes and returns lists of `xr.Dataset`; and
  `Constellation.to_inst` builds one. That is a documented public interchange type, which is what
  Tier B asks for.
  It is nevertheless **excluded**, for a reason specific to pysat rather than a general dislike of the
  package: pysat's data model is pandas **or** xarray, symmetrically — there is a
  `load_netcdf_pandas` for every `load_netcdf_xarray`, and the roadmap treats the two as a matched
  pair. pandas is Tier A and can never be listed. Listing xarray alone would therefore tell a reader
  that pysat's data model is xarray, which is only half true, and listing both is not available. The
  same fact is already conveyed accurately in Field 8, which says pysat supports pandas *and* xarray
  data structures.
  **What would change this:** an adapter or converter in pysat's public API that hands data to a named
  domain tool (a `to_sunpy_map()`-style function, an IDL or SPEDAS bridge), or xarray becoming pysat's
  sole documented interchange type with pandas support dropped. Neither is true at the source revision.

All recorded URLs are 42 characters or fewer, well inside the 128-character limit that applies to
related-item entries.

### 31. Related Instruments (OPTIONAL)
- Not found

**This is an evidenced omission, not an unexamined gap.** Every instrument concept the repository
evidences was looked for in the controlled vocabulary, and the outcome below is a decision about
relevance rather than about resolvability — the rows largely exist, and pysat is still not the
software a searcher filtering on them is after.

At the source revision `pysat/instruments/` contains four instrument modules — `pysat_ndtesting`,
`pysat_netcdf`, `pysat_testing`, `pysat_testmodel` — plus `methods/` and `templates/`. Three are
synthetic data generators for testing and one is a general reader for pysat-written netCDF files.
**pysat ships no module for any real instrument.** An instrument-agnostic framework supports none
specifically, and a user searching HSSI for a given instrument would not be well served by getting a
framework back that cannot read that instrument's data without a separate package.

**The one real-instrument artefact in the distribution, and why it is still not a value.**
`pysat/tests/cindi_ivm_meta.txt` is a genuine C/NOFS CINDI Ion Velocity Meter metadata table
— its third line is `glat,Geographic Latitude,2,deg,`. It is referenced from exactly
**two** places in the tree, both in `pysat/tests/test_meta.py` (lines 232 and 979), where it serves as
a realistic fixture for `Meta.from_csv`. pysat cannot load C/NOFS data; there is no C/NOFS instrument
module. A test fixture is not instrument support. Recorded here so that a future agent who finds the
file knows it was examined and why it was set aside. For reference if that judgement is ever revisited:
the vocabulary contains **two** instrument rows both named
`Coupled Ion-Neutral Dynamics Investigation`, with identifiers
`https://spase-metadata.org/SMWG/Instrument/CNOFS/CINDI` and
`https://spase-metadata.org/SMWG/Instrument/CNOFS/CINDI/IVM`, so the entry would need a decision
between them and could not be recorded blind.

**Instruments named in the documentation, and where they actually belong.** DMSP IVM, JRO ISR and the
four ACE real-time instruments (EPAM, MAG, SIS, SWEPAM) appear in `docs/tutorial/tutorial_basics.rst`,
`docs/tutorial/tutorial_analysis.rst` and `docs/tutorial/tutorial_constellation.rst` as worked examples
that begin by importing **pysatMadrigal** or **pysatSpaceWeather**; the Dynamics Explorer 2
instruments appear as a pysatNASA constellation example. Those associations belong to those packages'
own records, not to the framework's. The four ACE entries in particular were a single
realtime-constellation example that expands to four sub-instruments — one example, not four
supported instruments.

**PyHC's registry keywords are not evidence for this field.** The PyHC core registry lists `ace`,
`de2`, `dmsp`, `icon`, `madrigal`, `omni`, `sami2` and `tiegcm` among pysat's keywords. That list
helps people *find* pysat and describes the ecosystem's reach; it is not a statement that the core
distribution reads those instruments' data, and the code at the source revision shows it does not.

### 32. Related Observatories (OPTIONAL)
- Not found

Same relevance decision as Field 31, applied to platforms. Every mission and observatory associated
with pysat reaches it through a plug-in package.

- **ICON, JRO, COSMIC and SuperDARN** appear in `docs/new_instrument.rst` in the section defining
  pysat's naming conventions, as examples of what a plug-in author might put in the `platform` string.
  That is documentation of a naming convention, not support for those platforms.
- **ICON** has one deeper connection: `docs/tutorial/tutorial_files.rst` explains that
  `pysat's default conventions are a simplified implemention of the standards` developed for NASA's
  Ionospheric Connections Explorer mission. That is a *file convention* pysat adopted, and it is
  already captured where it belongs, as `ISTP-Compliant` in Field 19. It does not make pysat ICON
  software. (The historical trace of that connection is visible in the earliest Zenodo deposit, titled
  `rstoneback/pysat: ICON Release` — see Field 10.)
- **C/NOFS, DMSP, ACE and Dynamics Explorer 2** are tutorial examples driven by plug-ins, as set out
  in Field 31.
- **ICON, SORTIE, SPORT and COSMIC-2** appear in `ACKNOWLEDGEMENTS.md` as **funding sources** and are
  recorded in Field 25. They are not evidence for this field.

**Vocabulary state, for a future refresh that reopens this.** Rows do exist for several of these
platforms, so the omission is a relevance judgement and not a resolution failure:
`https://spase-metadata.org/SMWG/Observatory/CNOFS` (Communication/Navigation Outage Forecasting
System), `https://spase-metadata.org/SMWG/Observatory/ICON` (Ionospheric Connection),
`https://spase-metadata.org/SMWG/Observatory/DMSP` (Defense Meteorological Satellite Program),
`https://spase-metadata.org/SMWG/Observatory/SuperDARN`, and Dynamics Explorer rows including
`https://spase-metadata.org/SMWG/Observatory/DynamicsExplorer2`. COSMIC-2, SPORT and SORTIE have no
row of their own. **Do not mistake the near-miss:** the vocabulary does hold
`https://spase-metadata.org/IUGONET/Observatory/RISH/COSMIC/COSMIC_FORMOSAT_3`, named
`The joint Taiwan - U.S. Constellation Observing System for Meteorology, Ionosphere, and Climate`,
but that is the first COSMIC constellation (FORMOSAT-3), a different mission from the COSMIC-2
constellation named in Field 25. Nothing here may be recorded without its `https://spase-metadata.org/` identifier; a bare name
would create a new identifier-less row in the vocabulary.

### 33. Logo (OPTIONAL)
- **Logo URL:** https://raw.githubusercontent.com/pysat/pysat/3f0e5a43ad36f1eecfed02a3d1e3a740fd1a5f37/docs/images/logo.png

Pinned to the 40-character source revision, with no branch name and no `blob/` segment. The URL is 107
characters, inside the 200-character limit. It serves 2,278,411 bytes of `image/png` — a real image,
not the roughly 130-byte `text/plain` pointer a Git-LFS-tracked file would return (there is no
`.gitattributes` in the tree at this revision, so nothing is LFS-tracked).

**Reviewed and settled — do not reopen.** The image has been viewed: a blue ringed planet with a
satellite and the word "pysat", which is unambiguously the project's logo. It is the file the README
displays as its header image and the same asset the PyHC core registry points at. At 2.2 MB it is
large for a logo, and `docs/images/poweredbypysat.png` is both smaller — 1,704,401 bytes against
`logo.png`'s 2,278,411 — and drawn from the same artwork: the same blue ringed planet and satellite,
with "powered by" set above the wordmark. **Considered and rejected** as the Field 33 value. Under the
"Logos" heading of `docs/introduction.rst` that file is offered to other projects — *Does your project
use pysat?  If so, grab a "powered by pysat" logo!* — so it is a badge for downstream software to
display on their own pages, not the mark that identifies pysat itself. Recorded here so that a later
refresh sees it was examined and does not switch to it. The remaining images in that directory are
example plots and workflow diagrams.

**Why the pinned form and not a branch URL.** The README and the PyHC registry both reference this file
through `.../pysat/main/docs/images/logo.png`. A branch URL always serves whatever is currently at that
path, which is precisely the fragility being avoided: if a maintainer renames, moves or deletes the
file, the branch URL breaks silently and HSSI has no way to detect it. **"But a branch URL would always
show the current logo" is a rejected argument** — a logo redesign is something a metadata refresh
should notice and record deliberately, not something the catalogue should inherit without anyone
seeing it.
