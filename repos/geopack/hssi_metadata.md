# HSSI Metadata Extraction Results

**HSSI Software ID:** ad9602aa-4d82-4f9f-9ef5-053f92f2c9ff
**Repository:** https://github.com/tsssss/geopack
**Source Revision:** ab7efdc824b6613036648e21c18ee2ea413cf080
**Extraction Date:** 2026-07-28
**Validation Date:** 2026-08-26
**Validation Status:** PASS

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*The original submitter is not identified in the repository, so the required placeholder is retained.*

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.15110786

*This is the Zenodo **concept** (all-versions) DOI for this software,
rather than a single version's DOI. Also cited in `README.md:34` and `CITATION.cff`.*

### 3. Code Repository (MANDATORY)
https://github.com/tsssss/geopack

*Matches `setup.py` `url=`, the PyPI `Homepage` project URL, the
PyHC registry `code:` field, and the Zenodo `code:codeRepository` custom field.*

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Field-line Tracing
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing
- Models and Simulations: Physics-Based

*Code evidence per value:*

| Value | Evidence |
|---|---|
| Coordinate Transforms | Seven user-facing transform functions in `geopack/geopack.py`: `geomag` (707), `geigeo` (739), `magsm` (771), `gsmgse` (803), `smgsm` (831), `geogsm` (863), `gswgsm` (680), plus `geodgeo` (896) geodetic<->geocentric and `sphcar`/`bspcar`/`bcarsp` (961/1000/1024). Documented as a first-class capability in `README.md:292-325`. |
| Coordinate Transforms: Magnetospheric | The supported systems are exactly the magnetospheric set — GEO, GEI, MAG, GSM, GSE, SM (`README.md:294`) plus GSW from geopack08 (`README.md:15,40`). Matches the `software-functionality` skill's explicit mapping (`geopack` -> Coordinate Transforms:Magnetospheric). |
| Data Processing and Analysis | Required parent of `Data Processing and Analysis: Field-line Tracing`; selecting a subcategory does not auto-add the parent. |
| Data Processing and Analysis: Analysis | `shuetal_mgnp` (`geopack.py:1266`) and `t96_mgnp` (`geopack.py:1355`) compute derived physical quantities from a model: the GSM magnetopause boundary point, the observation point's distance to the boundary, and an inside/outside classification flag. |
| Data Processing and Analysis: Data Access and Retrieval | `update_igrf(local_dir)` (`geopack.py:11-47`) scrapes the NOAA/NGDC IAGA coefficient directory `http://www.ngdc.noaa.gov/IAGA/vmod/coeffs/` over HTTP (`urlopen`), selects files matching `igrf*coeffs.txt`, and downloads them to a local cache. `init_igrf(version=None)` (`geopack.py:53`) invokes it and selects the newest available generation. This is a user-facing retrieval capability and is the headline feature of release v1.0.12. |
| Data Processing and Analysis: Field-line Tracing | `trace(...)` (`geopack.py:1157`) with the adaptive `step`/`rhand` integrator (`geopack.py:1077-1156`). |
| Models and Simulations | Parent category for the model subcategories below. |
| Models and Simulations: Data Guided | `shuetal_mgnp` (`geopack.py:1266`) and `t96_mgnp` (`geopack.py:1355`) compute the magnetopause boundary *shape* as an explicit function of real-time solar wind pressure and IMF Bz — data-driven model boundaries, the subcategory's canonical case. The external field models are likewise driven by observational inputs: `t89` takes a Kp-index bin (`README.md:234-236`); `t96`/`t01`/`t04` take solar wind dynamic pressure, Dst, and IMF By/Bz, plus the observationally derived G1/G2 (T01) and W1-W6 (T04) indices (`README.md:250-285`). `init_igrf` retrieves observationally derived IGRF coefficients at run time. |
| Models and Simulations: Empirical | T89/T96/T01/T04 are data-based empirical models fitted to spacecraft observations — `t96.py:8` "Data-based model calibrated by ..."; `t89.py:9,13` notes the model was fitted to the IMP-HEOS and ISEE-1/2 datasets. IGRF is likewise an empirical reference field. |
| Models and Simulations: Field-line Tracing | `trace` integrates field lines through the *model* field, dispatching to a chosen internal model (`dipole`/`igrf`) and external model (`t89`/`t96`/`t01`/`t04`) via `call_internal_model`/`call_external_model` (`geopack.py:1057-1076`). This is model-space tracing, complementing the data-processing classification. |
| Models and Simulations: Physics-Based | The models are semi-empirical with physically motivated structure: shielded magnetopause current systems, warped tail current sheet, Birkeland current systems, and ring current (`t04.py:735-736`, `t04.py:1463`, `t96.py:412-414`, `t96.py:567`). IGRF is a spherical-harmonic potential-field expansion (`igrf_geo`, `geopack.py:200`). Magnetopause shape derives from the Chapman-Ferraro problem (`geopack.py:1396`). |

*Considered and rejected, with reason:*
- **Data Visualization** (and all subcategories) — the package exposes **no** plotting API. `matplotlib`
  and `cartopy` appear only in the unshipped demo `notebooks/Field Line Trace Demo.ipynb`; neither is a
  declared dependency (`setup.py` `install_requires=['numpy','scipy']`). A demo notebook is not a
  package capability.
- **Coordinate Transforms: Ionospheric** — no AACGM, apex, quasi-dipole, or MLT coordinates. `geodgeo`
  is a geodetic<->geocentric geometric conversion, not an ionospheric magnetic coordinate system.
- **Coordinate Transforms: Solar / Heliospheric / Planetary / Mission-Specific** — no such frames;
  `sun(ut)` (`geopack.py:600`) computes solar ecliptic longitude and GST purely as an internal
  ingredient of the GEI/GSE transforms, not as a solar coordinate capability.
- **Models and Simulations: First Principles / MHD / Forecasting / Theory** — no PDE/MHD solver, no
  forecast product, no analytic-theory framework.
- **Data Processing and Analysis: Processing / Time Series Analysis / File Format Conversion** — the
  IGRF coefficient parse-and-interpolate step (`geopack.py:84-154`) is internal model initialization,
  not a user-facing pipeline, time-series analysis, or format conversion capability.
- **Mission-related** (all) — not part of any mission ground system or pipeline.
- **Servers and Environments** (all) — no server, container, or HPC/parallel component.

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Atmosphere
- Earth Magnetotail
- Earth Inner Magnetosphere
- Earth Ionosphere

*`Earth Magnetosphere`: T89/T96/T01/T04 are magnetospheric field models, and the magnetopause models
bound the magnetosphere.*

*`Earth Atmosphere`: `igrf_geo(r, theta, phi)` (`geopack.py:200`) evaluates the main
geomagnetic field at arbitrary geocentric radius including at and near the surface; `geodgeo`
(`geopack.py:896`) converts geodetic altitude in km and geodetic latitude to geocentric coordinates —
an explicitly ground/upper-atmosphere-referenced conversion; `trace(..., r0=1)` (`geopack.py:1157-1165`,
docstring "Traces a field line from an arbitrary point of space to the earth's surface") maps
magnetospheric field lines to their ionospheric footpoints; and the repository's only bundled example
(`notebooks/Field Line Trace Demo.ipynb`, cells 5-10) converts a **ground magnetic observatory** location
(Antarctic AGO P2) from geodetic lat/lon to GSM and traces its field line — i.e. ground/ionosphere-to-
magnetosphere mapping is the demonstrated use case. The original rationale also used `Earth
Atmosphere` as the coarse representation of the package's ionospheric-footpoint work because it
stated that no separate ionosphere option existed. That premise was falsified on 2026-08-25:
`Earth Ionosphere` is a separate controlled value, and the flat region vocabulary means a coarse
value does not imply a finer one. `Earth Atmosphere` remains supported independently by the
ground/upper-atmosphere coordinate and field-line functionality above.*

*`Earth Magnetotail`: the tail current sheet is a separately selectable model component. `geopack/t89.py:26`
identifies the implemented model as a magnetospheric field model with a warped tail current sheet,
and `geopack/t89.py:95,192,233` documents the tail-current contribution and sheet shape. The T04
model interface exposes a tail-only mode at `geopack/t04.py:61-73`, with `taildisk()` documented at
`geopack/t04.py:732-737`. T04 is limited sunward of -15 Re (`geopack/t04.py:24`), so that model's evidence is for the
near tail; the T89 tail-current-sheet implementation carries no such stated limit.*

*`Earth Inner Magnetosphere`: the T04 references explicitly describe storm-time distortion and
dynamics of the inner magnetosphere (`geopack/t04.py:30-33`), and its model interface offers a ring-current-
only mode (`geopack/t04.py:61-81`). T01 likewise describes its model change in the inner magnetosphere at
`geopack/t01.py:12`.*

*`Earth Ionosphere`: `geopack/t01.py:1051` and `geopack/t04.py:987` parameterize the field-aligned-current oval at
ionospheric altitude, while `geopack/geopack.py:1157-1159,1229-1249` traces field lines to Earth's surface and
interpolates their footpoints. The settled 2026-08-25 correction adds this value after the earlier
"no separate option exists" premise was falsified; it had never appeared in the field's explicit rejection list.*

*Considered and rejected:* **Interplanetary Space** — solar wind velocity, dynamic pressure and IMF
By/Bz are model *inputs* only (`recalc`, `geopack.py:360`; `README.md:250-285`); the package models no
interplanetary region. **Solar Environment** — `sun()` is an internal ephemeris helper, not solar
science. **Planetary Magnetospheres** — Earth only; all models are Earth-specific.

### 6. Authors (MANDATORY)

Author order is preserved exactly as recorded. Affiliations are given with their ROR identifiers.

**Author 1 — Nathaniel Frissell**
- Given name: `Nathaniel`
- Family name: `Frissell`
- Author Identifier: https://orcid.org/0000-0002-8398-4222
- Affiliation: University of Scranton — https://ror.org/05xwb6v37

*ORCID `0000-0002-8398-4222` is verified to be Nathaniel Frissell, employed at the University of
Scranton — matching the recorded affiliation. Corroborated by Zenodo record 15110787 creator 2
("Nathaniel Frissell", University of Scranton) and by 5 commits from
`Nathaniel A. Frissell <nathaniel.a.frissell@njit.edu>` (GitHub login `w2naf`).*

*The verified ORCID corrects an earlier omission from this author's identity. The name and affiliation
were already correct.*

**Author 2 — Lei Cai**
- Given name: `Lei`
- Family name: `Cai`
- Author Identifier: https://orcid.org/0000-0003-0127-7303
- Affiliation: University of Oulu — https://ror.org/03yj89h83

*This author was previously recorded with given name `" Ph.D."` and
family name `"Lei Cai"` — an inverted, mis-split name with a leading space, produced by splitting the
Zenodo creator string "Lei Cai, Ph. D." on its comma. Evidence for the corrected form: (a) commit
`f5dd49a` (2023-02-13) is authored by `Lei Cai, Ph.D <lei.cai@oulu.fi>`, merged via PR #15 from
`JouleCai/master`; (b) ORCID `0000-0003-0127-7303` is Lei Cai, employed at the **University of Oulu since
2021-02-01**, with keywords "Space Weather, Ionosphere Physics, Magnetosphere-Ionosphere coupling" —
matching both the `lei.cai@oulu.fi` commit address and the previously recorded University of Oulu
affiliation; (c) HSSI already held this same author, under this same ORCID and affiliation, as an author
of GeospaceLAB, so the corrected entry resolves to that established identity rather than a new one.*

**Author 3 — Jim Lewis**
- Given name: `Jim`
- Family name: `Lewis`
- Author Identifier: https://orcid.org/0009-0005-4191-5906
- Affiliations:
  - Space Sciences Laboratory, University of California, Berkeley — https://ror.org/048400679
  - University of California, Berkeley — https://ror.org/01an7q238

*Corroborated by 6 commits from `Jim Lewis` / `jameswilburlewis <jwl@ssl.berkeley.edu>` and by
Zenodo creator 4 ("Jim Lewis", UC Berkeley Space Sciences Lab). This author identity is shared with
PySPEDAS and SPEDAS and is preserved exactly as recorded.*

**Author 4 — Sheng Tian**
- Given name: `Sheng`
- Family name: `Tian`
- Author Identifier: *(none)* — no confident ORCID match exists; searches returned only unrelated
  people. Deliberately left blank rather than guessed.
- Affiliations:
  - University of California, Los Angeles — https://ror.org/046rm7j60
  - University of Minnesota — https://ror.org/017zqws13

*Sheng Tian is the principal author — **109 of the repository's 125
commits (~87%)**, across eight git identities — and is the `setup.py` `author`/`author_email`
(`ts0110@atmos.ucla.edu`). UCLA affiliation confirmed by `CITATION.cff` ("Department of Atmospheric and
Oceanic Sciences, University of California, Los Angeles"), Zenodo creator 1, and `README.md:2`.*

*University of Minnesota is a **second** affiliation alongside UCLA.
26 commits come from `tianx138@umn.edu` and `shengtian@m472e.space.umn.edu`, and the pattern is
long-standing and current rather than incidental — the `umn.edu` address first appears **2016-05-18**, two
years before geopack's first public release, and authored the **latest commit in the repository**
(`ab7efdc`, 2026-06-25). Decisively, **no commit in the entire history was made from
`ts0110@atmos.ucla.edu`**, the address carried by every piece of citation metadata. Both institutional
identities are therefore real and concurrent. The institutional significance of the UMN identity is not
further resolvable from the repository, so it is recorded as a sustained parallel affiliation, **not** as a
move.*

**Author 5 — Rachel Frissell**
- Given name: `Rachel`
- Family name: `Frissell`
- Author Identifier: *(none)* — deliberately blank; see below.
- Affiliation: *(none — no evidence found)*

*This author was previously recorded with an empty given name and the
family name `"w2ruf"` — a GitHub handle rather than a name, inherited from the Zenodo creator list.
Evidence that `w2ruf` is **Rachel Frissell, a distinct person and a genuine credited contributor**, not a
duplicate of Nathaniel Frissell: the GitHub account `w2ruf` has exactly 4 commits to this repository
(`3c646d5`, `bf8b1ab`, `52b5d19`, `0f5b5c6`), every one authored by
`Rachel Frissell <rachelfrissell@gmail.com>` in January 2019; `git shortlog -sne --all` independently
shows `Rachel Frissell <rachelfrissell@gmail.com>` with exactly 4 commits and no other contributor with
4; and the control case `w2naf` maps to 5 commits all authored by `Nathaniel A. Frissell`, validating the
login-to-commit mapping. (`W2RUF` and `W2NAF` are amateur-radio callsigns.) She is retained as an author
in her own right.*

*No ORCID assigned. ORCID `0000-0001-7386-6735` carries the name "Rachel Frissell" but is an empty record
— zero employments, works, keywords, or URLs. Name-only agreement is insufficient evidence, so the
identifier is left blank rather than guessed.*

### 7. Software Name (MANDATORY)
geopack

*Matches `setup.py` `name='geopack'`, the PyPI project name, and
the PyHC registry entry name. Editorial intent respected — the lowercase form is what the project uses.*

### 8. Description (MANDATORY)

The geopack package provides a Python translation of several of Tsyganenko's Earth magnetic field models (originally implemented in FORTRAN). It integrates two modules originally written in Fortran — the geopack coordinate-transformation and internal-field library, and the Tsyganenko external magnetospheric field models T89, T96, T01 and T04 — and is compatible with both geopack05 and geopack08. The package evaluates the internal geomagnetic field from the IGRF and dipole models in GEO, GSM and GSW coordinates; converts cartesian vectors among the GEO, GEI, MAG, GSM, GSE, SM and GSW systems and between geodetic and geocentric coordinates; traces model field lines from an arbitrary point to the Earth's surface or to an outer boundary using any combination of internal and external model; and locates the magnetopause using the Shue et al. (1998) and T96 boundary models. IGRF coefficients are downloaded automatically from NOAA, are represented as time series at millisecond cadence, and are extrapolated outside the tabulated epoch range. All routines take their inputs as arguments and return their outputs, rather than communicating through the shared common blocks of the Fortran and IDL versions. Note that the G parameters of T01 and the W parameters of T04 are not computed by the package and must be supplied by the user; support for T07d is under development.

*The earlier HSSI description was the single first sentence above. It is factually correct but
**materially incomplete**: it describes only the Tsyganenko models and omits the geopack
coordinate-transform library (half of what `README.md:3` says the package integrates), the IGRF and
dipole internal field models, field-line tracing, and the magnetopause models. That sentence
is preserved **verbatim as the opening**; the added detail is sourced from `README.md:3-15,39-46,
136-343` and the code.*

### 9. Concise Description (OPTIONAL)
Pure Python implementation of Tsyganenko's Earth magnetic field models

*This is the original editorial wording for a 150-200 character preview,
and a preview is legitimately lossy; it is not replaced merely because a longer phrasing exists.*

### 10. Publication Date (RECOMMENDED)
2018-07-22

*The field is defined as "Date of first broadcast/publication ... Used for the initial version of the
software." The existing value 2025-03-31 is the Zenodo/DataCite `Issued` date of release **v1.0.12**
(`api.datacite.org/dois/10.5281/zenodo.15110786` -> `dates: [{date: 2025-03-31, dateType: Issued}]`) —
an autofill artifact of the concept DOI resolving to its latest version, not a first-publication date.
Evidence for 2018-07-22: the first public release of geopack is PyPI `1.0.1`, uploaded
2018-07-22T16:06:08Z (`pypi.org/pypi/geopack/json`, `releases`); SoMEF reports the GitHub repository
`date_created` as 2018-07-21T01:44:19Z; and `LICENSE` reads "Copyright (c) 2018 Sheng Tian". (The
repository's oldest commits are from 2015 but are IDL `.pro` files from an unrelated earlier project
and predate the Python package.)*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Correct per the field guidance (DOI obtained through the
GitHub-Zenodo workflow). Confirmed by DataCite `publisher: "Zenodo"`.*

### 12. Version (RECOMMENDED)
- **Version Number:** `v1.0.13`
- **Version Date:** `2026-05-16`
- **Version Description:** Fixes the interplanetary magnetic field clock angle calculation in the T01 model (pull request #25).
- **Version PID:** *Not found*

*Version number: `setup.py` at HEAD reads `version='1.0.13'`; PyPI latest is `1.0.13`; the newest git
tag is `v1.0.13`; the GitHub release `v1.0.13` exists. No newer release exists (only tags `v1.0.12` and
`v1.0.13`).*

*Version description: derived from the authoritative GitHub release notes for `v1.0.13` ("Bug fix for
IMF clock angle calculation in t01.py by @jameswilburlewis in .../pull/25"). Verified against the code:
`git diff v1.0.12 HEAD -- geopack/t01.py` shows the single functional change
`if theta <= 0: theta = 2*np.pi` -> `if theta <= 0: theta += 2*np.pi` at `t01.py:150` inside `extall`,
where `theta = arctan2(byimf, bzimf)` is the IMF clock angle. This is the only source change between
the two releases.*

*Version PID: Zenodo holds exactly **one** version record for this concept — v1.0.12
(`10.5281/zenodo.15110787`). No Zenodo DOI has been minted for v1.0.13, so this field is empty rather
than carrying v1.0.12's DOI, which would misattribute it. The concept DOI in Field 2 is unaffected.*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*All source is Python 3 (`geopack/*.py`, 8,334 lines);
`setup.py` classifier `Programming Language :: Python :: 3`. SoMEF additionally reports
"Jupyter Notebook" purely from the byte size of the one demo notebook — that is not a programming
language for this field and is excluded.*

### 14. Reference Publication (RECOMMENDED)
Not found

*Deliberate. There is no publication describing **this software**: no JOSS/SoftwareX paper, and
`README.md:33-36` ("How to cite") directs users to the Zenodo DOI, not to a paper. The Tsyganenko,
Hapgood and Shue papers describe the *models implemented*, not the Python package, so they are recorded
under Field 27 (Related Publications) instead. Left empty rather than filled with a model paper.*

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

*`LICENSE` contains the verbatim MIT License text, "Copyright (c) 2018 Sheng Tian". Corroborated by
`setup.py` (`license='MIT'`, classifier `License :: OSI Approved :: MIT License`), PyPI
`license: MIT`, DataCite `rightsList` (`rights: "MIT License"`, `rightsIdentifier: "mit"`,
`rightsIdentifierScheme: "SPDX"`), Zenodo `license.id: "mit-license"`, SoMEF (`spdx_id: MIT`), and the
PyHC registry license rating "Good".*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- geopack
- physics
- python
- python 3
- space physics
- tsyganenko model
- coordinate transformation
- empirical model
- field line tracing
- geomagnetic field
- heliosphere
- igrf
- magnetic field models
- magnetosphere
- shue
- tsyganenko

*Sources:
`magnetosphere` and `heliosphere` are the PyHC registry's own curated keywords for this exact package
(`projects.yml` geopack entry) — PyHC is the highest-priority curated source; `igrf` and
`geomagnetic field` from `igrf_geo`/`igrf_gsm`/`igrf_gsw` and the NOAA coefficient loader;
`coordinate transformation` from the seven transform functions; `field line tracing` from `trace`;
`magnetic field models` and `empirical model` from T89/T96/T01/T04; `shue` from `shuetal_mgnp`
(`geopack.py:1266`, Shue et al. 1998 magnetopause); `tsyganenko` as the unqualified companion to the
existing `tsyganenko model`. The first six keywords are the GitHub repository topics, which SoMEF
independently reports as `geopack, physics, python, python3, space-physics, tsyganenko-model` — the
recorded spellings align with the existing keyword vocabulary.*

*Note: `heliosphere` rests solely on PyHC's curation of this package and sits oddly beside an
Earth-magnetosphere scope. Retained because PyHC is the authoritative curated source.*

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories

*`update_igrf` (`geopack/geopack.py:11-47`) opens the NOAA/NGDC IAGA directory listing
`http://www.ngdc.noaa.gov/IAGA/vmod/coeffs/` with `urllib.request.urlopen`, parses the `href` entries
for files matching `igrf*coeffs.txt`, and downloads each one — a textbook HTTP directory data source.*

*Not selected: `Observatory/Mission-specific` (the IGRF coefficient set is a global reference model, not
an observatory product), `CDAWeb`, `HAPI`, `OMNIWeb`, `SSCWeb`, `S3/Cloud-aware`, `das2`, `TAP`,
`VirES`, `FTP/FTPS Directories`, `Other` — none appear anywhere in the code.*

### 18. Input File Formats (RECOMMENDED)
- ascii

*The only files the package reads are the IGRF Gauss-coefficient tables `igrf<NN>coeffs.txt`, parsed as
plain text in `init_igrf` (`geopack.py:84-113`): `open(coef_file, 'r')`, `file.readline()`,
`file.read().splitlines()`, `line.split()`, with a 3-line header skip and whitespace-delimited columns.
No binary, CDF, FITS, HDF5, netCDF, JSON, csv or IDL.sav reader exists anywhere in the package.*

### 19. Output File Formats (RECOMMENDED)
Not found

*Deliberate, and left empty after analysis. The package generates **no** data files: every public
routine returns Python scalars/arrays (`README.md:137` "function parameters are all input parameters
and the outputs are returned"). The one write operation, `open(local_file, 'wb'); file.write(
response.read())` in `update_igrf` (`geopack.py:46-47`), is a byte-for-byte cache copy of a downloaded
file, not a generated data product, so the field is left empty.*

### 20. Operating System (RECOMMENDED)
- Operating System Independent

*The package is pure Python 3 with only
`numpy` and `scipy` as dependencies (`setup.py` `install_requires`), contains no compiled extension, no
platform-specific code, and no OS-conditional imports. `setup.py` declares `platforms=['Mac OS']` and
the classifier `Operating System :: MacOS`, and `README.md:19` says "I've only tested the Python
geopack on Mac OS in Python 3.6" — but those record the author's **testing scope**, not a restriction,
and adding a redundant `Mac` value alongside `Operating System Independent` would only muddy the record.*

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

*Pure interpreted Python: no C/Fortran/Cython extension modules, no build step beyond
`setuptools.find_packages()`, no SIMD/intrinsics, no architecture-conditional code paths, and no
compiled wheels (PyPI ships a single pure-Python `bdist_wheel` plus an sdist). The only dependencies,
numpy and scipy, are available on all major architectures.*

### 22. Related Phenomena (OPTIONAL)
- Geomagnetic Storms
- Solar Wind

*`Geomagnetic Storms` — unambiguous. The T04 model implemented in `geopack/t04.py` is published as
"Modeling the dynamics of the inner magnetosphere during **strong geomagnetic storms**"
(`t04.py:32-33`), and its companion reference is "**Storm-time** distortion of the inner magnetosphere"
(`t04.py:30-31`). T96/T01/T04 are parameterized by Dst and T89 by Kp — the standard geomagnetic storm
indices (`README.md:234-285`).*

*`Solar Wind` — `shuetal_mgnp` and `t96_mgnp` (`geopack.py:1266,1355`) compute the magnetopause boundary
as an explicit function of solar wind proton density or ram pressure, solar wind velocity, and IMF Bz —
solar-wind/magnetosphere coupling as a primary output; `recalc(ut, vxgse, vygse, vzgse)`
(`geopack.py:360`) takes the solar wind velocity in GSE to define the GSW frame; T96/T01/T04 take
Pdyn and IMF By/Bz.*

### 23. Development Status (RECOMMENDED)
Active

*repostatus.org "Active": reached a stable, usable state and being actively developed. Evidence: 12
stable PyPI releases spanning 2018-2026, the most recent on 2026-05-12; latest commit
`ab7efdc` on 2026-06-25; a merged external contribution (PR #25) in 2026-03; the package is a hard
dependency of PySPEDAS (`geopack>=1.0.13`); and the PyHC registry rates its software_maturity and
python3 support "Good".*

*Note on a conflicting signal: `setup.py` carries the classifier `Development Status :: 3 - Alpha`. That
classifier has never been updated since the project's early days and is contradicted by eight years of
stable releases and by PyHC's own maturity assessment; it is treated as stale rather than authoritative.*

### 24. Documentation (RECOMMENDED)
https://github.com/tsssss/geopack/blob/master/README.md

*This is the PyHC registry's curated `docs:` value for the geopack entry (`projects.yml`) — PyHC is the
highest-priority metadata source, and it rates geopack's documentation "Good". It is also the correct
choice on the merits: the project has no separate documentation site, no `docs/` directory, and no
Read the Docs configuration; `README.md` (17 KB) is the complete reference, containing installation
instructions (`README.md:18-27`), usage examples (72-132), and a full per-function package interface
(136-343).*

### 25. Funder (OPTIONAL)
Not found

*Deliberate, with authoritative negative evidence: `README.md:46` states "please do understand that the
package does not have any funding support." DataCite `fundingReferences` is empty; Zenodo record 15110787
lists no grants. The "Donate via PayPal" section (`README.md:1,29-31`) is a personal donation link and
is **not** funder or award metadata — it is deliberately not mapped to this field.*

### 26. Award Title (OPTIONAL)
Not found

*Same evidence as Field 25 — no grant or award anywhere in the repository, DataCite record, or Zenodo
record.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

The publications the repository itself cites as the references for the models it implements.

- https://doi.org/10.1016/0032-0633(92)90012-D — Hapgood, M. A. (1992). Space physics coordinate
  transformations: A user guide. *Planetary and Space Science*, 40(5), 711-717.
  *(`README.md:349`, and `README.md:294` cites it as the definition of the supported coordinate systems.)*
- https://doi.org/10.1016/0032-0633(89)90066-4 — Tsyganenko, N. A. (1989). A magnetospheric magnetic
  field model with a warped tail current sheet. *Planetary and Space Science*, 37, 5-20.
  *(`geopack/t89.py:25-26`, "Reference for the original model"; also `t89.py:88`. The T89 model.)*
- https://doi.org/10.1029/94JA03193 — Tsyganenko, N. A. (1995). Modeling the Earth's magnetospheric
  magnetic field confined within a realistic magnetopause. *Journal of Geophysical Research*, 100,
  5599-5612. *(`geopack/geopack.py:1373`, cited as the source of the pressure-dependent magnetopause
  used by `t96_mgnp`; the T96 model.)*
- https://doi.org/10.1029/98JA01103 — Shue, J.-H., et al. (1998). Magnetopause location under extreme
  solar wind conditions. *Journal of Geophysical Research*, 103, 17691-17700.
  *(`geopack/geopack.py:1271`, the model implemented by `shuetal_mgnp`.)*
- https://doi.org/10.1029/2001JA000219 — Tsyganenko, N. A. (2002). A model of the near magnetosphere
  with a dawn-dusk asymmetry: 1. Mathematical structure. *Journal of Geophysical Research*, 107(A8).
  *(`geopack/t04.py:27-29`, reference (1); the T01 model. `README.md:351` cites the 2001 submitted
  manuscript; the repository's own source gives the published DOI.)*
- https://doi.org/10.1029/2001JA000220 — Tsyganenko, N. A. (2002). A model of the near magnetosphere
  with a dawn-dusk asymmetry: 2. Parameterization and fitting to observations. *Journal of Geophysical
  Research*, 107(A8). *(`geopack/t04.py:27-29`, reference (1).)*
- https://doi.org/10.1029/2002JA009808 — Tsyganenko, N. A., Singer, H. J., & Kasper, J. C. (2003).
  Storm-time distortion of the inner magnetosphere: How severe can it get? *Journal of Geophysical
  Research*, 108(A5). *(`geopack/t04.py:30-31`, reference (2).)*
- https://doi.org/10.1029/2004JA010798 — Tsyganenko, N. A., & Sitnov, M. I. (2005). Modeling the
  dynamics of the inner magnetosphere during strong geomagnetic storms. *Journal of Geophysical
  Research*, 110(A3), A03208. *(`README.md:353` and `geopack/t04.py:32-33`, reference (3); the T04
  model and the definition of its W1-W6 parameters.)*

### 28. Related Datasets (OPTIONAL)
- International Association of Geomagnetism and Aeronomy, Working Group V-MOD. International
  Geomagnetic Reference Field (IGRF) Gauss coefficient files [Data set]. NOAA National Centers for
  Environmental Information. https://www.ngdc.noaa.gov/IAGA/vmod/coeffs/

*This is the dataset the package actually retrieves, parses and evaluates: `update_igrf`
(`geopack/geopack.py:17`) downloads every `igrf*coeffs.txt` file from this exact directory, and
`init_igrf`/`load_igrf` (`geopack.py:53-154`) parse the Gauss coefficients, build a millisecond-cadence
time series, and interpolate them for every field evaluation. Entered as an APA-style citation because
the coefficient files carry no DOI.*

*No IGRF-generation describing publication is cited here: the package auto-loads whichever generation
is newest at NOAA, so pinning the citation to a specific generation's paper (e.g. IGRF-13,
https://doi.org/10.1186/s40623-020-01288-x) would be stale.*

*Considered and rejected:* the Qin-Denton W and G parameter dataset
(`https://rbsp-ect.newmexicoconsortium.org/data_pub/QinDenton/`, `README.md:44`). `README.md:44`
explicitly states "The Python version does not support the calculations of the G and W parameters" —
the link is a courtesy pointer to where a user can obtain values the package deliberately does not
handle. Not a supported dataset.

### 29. Related Software (OPTIONAL)

- https://geo.phys.spbu.ru/~tsyganenko/Geopack-2008.html — **Geopack-2008** (Fortran, N. A. Tsyganenko).
  The upstream software this package is a translation of. `README.md:4` names it directly as the origin
  ("The Fortran `geopack05` is available at ... and `geopack08` is available at ..."), and
`README.md:6,39-40` describe maintaining behavioural compatibility with it and adding `gswgsm` to
support its new GSW coordinate.
- https://geo.phys.spbu.ru/~tsyganenko/empirical-models/ — **Tsyganenko empirical magnetospheric
  magnetic field models** (Fortran, N. A. Tsyganenko). The second of the two upstream Fortran modules
  this package integrates (`README.md:3`, "has integrated two modules originally written in Fortran:
  the `geopack` and the Tsyganenko models (T89, T96, T01, and T04)"). `geopack/t89.py`, `t96.py`,
  `t01.py` and `t04.py` are line-by-line translations, retaining the original author attributions
  ("Author: Nikolai A. Tsyganenko", `t89.py:30`) and release dates (`t96.py:6`, `t01.py:5`).
- https://korthhaus.com/idl-software/idl-geopack-dlm/ — **IDL Geopack DLM** (H. Korth, JHU/APL). The
  same Geopack and Tsyganenko models exposed through IDL — the closest similar-purpose software.
  `README.md:6` states the Python results are verified against it: "Test results are attached in
  `./test_geopack1.md` to demonstrate that the Python `geopack` returns the same outputs as the Fortran
  and IDL counterparts," and `README.md:137` contrasts the two calling conventions.
- https://github.com/mattkjames7/PyGeopack — **PyGeopack** (M. K. James). An independent Python interface
  to the same upstream Fortran Geopack-2008 library, described by its own repository as a "Wrapper for
  geopack-08 used for the Tsyganenko magnetic field models," implementing the same T89/T96/T01/TS05
  models plus field-line tracing and coordinate conversions. This is the closest **Python**
  similar-purpose alternative to this package — directly analogous to the IDL Geopack DLM entry above,
  and the same relationship type Field 29 exists to capture: independent software performing the same
  task from the same upstream origin. It differs in approach (a compiled C/C++/Fortran extension wrapping
  the original library, versus this package's pure-Python translation), which is what makes the pairing
  useful to a user comparing options. Actively maintained (last pushed 2026-05-18). No dependency, import,
  or cross-reference exists in either direction, so it belongs in Field 29 and not Field 30.

*Broken-link note (repository defect, not HSSI metadata): three of the four external software links in
`README.md:4,44` are now dead — the CCMC pages for Geopack-2005
(`ccmc.gsfc.nasa.gov/modelweb/magnetos/data-based/Geopack_2005.html`) and for the Tsyganenko models
(`ccmc.gsfc.nasa.gov/models/modelinfo.php?...`) and the IDL Geopack page
(`ampere.jhuapl.edu/code/idl_geopack.html`) all return 404. The live, author-maintained replacements
above are used instead. Geopack-2005 is not listed separately: it is superseded by Geopack-2008, which
is covered by the first entry.*

*Relevance-gate exclusions (audit trail):*
- **numpy, scipy** — Tier A generic scientific-Python stack. They are the package's only dependencies
  (`setup.py` `install_requires`), but being a dependency is not a relationship that distinguishes this
  software; the same claim is true of nearly every package in HSSI.
- **matplotlib, cartopy** — Tier A, and not even dependencies; they appear only in the demo notebook.
- **SpacePy** (`spacepy.irbempy` also exposes Tsyganenko models) — functional overlap only. No
  dependency, no import, no adapter, no cross-reference in either project. Not distinguishing.
- **The `igrf` Python package** — partial functional overlap (IGRF evaluation) with no relationship of
  any kind between the two projects. Rejected.
- **IDL SPEDAS** — considered as the distributor of the IDL Geopack DLM; the DLM itself is the precise
  and correctly attributed entry, so SPEDAS is not listed separately here (PySPEDAS is Field 30).

### 30. Interoperable Software (OPTIONAL)
- https://github.com/spedas/pyspedas — **PySPEDAS**

*Passes the relevance gate on specific, cited evidence of a demonstrated exchange — not on dependency
presence:*
- PySPEDAS ships an entire dedicated adapter subpackage, `pyspedas/geopack/`, whose modules
  `t89.py`, `t96.py`, `t01.py`, `ts04.py`, `igrf.py`, `ttrace2endpoint.py`, `trace_to_event.py` and
  `calculate_lshell.py` wrap this package's routines and expose them as tplot-variable operations
  (`tt89`, `tt96`, `tt01`, `tts04`), documented in `pyspedas/geopack/README.md` — "The routines in this
  module can be used to calculate Tsyganenko magnetic field models using Sheng Tian's `geopack` library
  (https://github.com/tsssss/geopack)" — and on its own documentation page `docs/source/geopack.rst`.
- The adapter layer imports this package's functions directly:
  `pyspedas/geopack/generic_geopack_adapters.py` contains `from geopack.geopack import igrf_gsm`,
  `from geopack.t89 import t89`, `from geopack.t96 import t96`, `from geopack.t01 import t01` and
  `from geopack.t04 import t04`, converting tplot position variables into geopack model calls and the
  results back into tplot variables.
- The exchange is complementary in both directions: `pyspedas/geopack/get_w_params.py` and
  `get_tsy_params.py` compute exactly the T04 W parameters and T01/T96 model parameters that
  `README.md:44` says this package deliberately does **not** compute; PySPEDAS supplies the missing
  inputs and this package supplies the model evaluation.
- The relationship is maintained bidirectionally: PySPEDAS maintainer Jim Lewis
  (`jwl@ssl.berkeley.edu`) is a credited author of this package and contributes fixes upstream from
  `spedas/master` — PR #22 (T01/`full_rc`/`ap` coefficient corrections, 2024) and PR #25 (the T01 IMF
  clock-angle fix that constitutes release v1.0.13, 2026). PySPEDAS pins `geopack>=1.0.13`
  (`pypi.org/pypi/pyspedas/json`, `requires_dist`), and
  `pyspedas/geopack/tests/test_geopack_idl_validation.py` cross-validates the combination against IDL.

*Relevance-gate exclusions (audit trail): numpy and scipy (Tier A — the only declared dependencies;
being a dependency is not interoperability); matplotlib and cartopy (Tier A, and demo-notebook only);
no Tier B package (astropy, xarray, cdflib, h5py, netCDF4, dask, MATLAB, Jupyter) appears anywhere in
the package's code or dependencies, so none was even a candidate. No blanket "part of the scientific
Python ecosystem" or "PyHC member" claim is used.*

### 31. Related Instruments (OPTIONAL)
Not found — empty by design, after applying the relevance gate.

*geopack is an **instrument-agnostic** package: it implements global empirical field models and
coordinate transforms and reads no instrument's data. No candidate cleared the "designed to support"
gate, so no instrument association is recorded.*

*Considered and rejected, with reason:*
- **ISEE-1, ISEE-2, IMP, HEOS** (`geopack/t89.py:9,13` — "and ISEE-1 and -2 spacecraft data set",
  "ISEE-1,2 data were added to the original IMP-HEOS dataset"). These name the observational datasets
  Tsyganenko used to **fit the original T89 model in 1989**; this package neither reads nor processes
  data from those instruments. Model-heritage provenance, not designed-to-support.
- **THEMIS-A** — appears only in commit message `ae30121` describing a numerical validation test case
  ("THEMIS-A ephemeris for 2007-03-23"). A test fixture, not supported data.
- **Van Allen Probes / RBSP-ECT** — appears only as the host of the Qin-Denton parameter files at
  `README.md:44`, for parameters the package explicitly does not compute. Not supported.

### 32. Related Observatories (OPTIONAL)
Not found — empty by design, after applying the relevance gate.

*Same reasoning and the same rejection set as Field 31: geopack is observatory-agnostic, works with no
mission's data products, implements no mission data convention, and is not a mission-team tool. The
Antarctic AGO ground-station coordinates in `notebooks/Field Line Trace Demo.ipynb` (cell 3, sourced
from `polar.umd.edu`) are demonstration input for a tutorial, which the gate excludes explicitly.*

### 33. Logo (OPTIONAL)
Not found

*No logo in the repository, no logo in the PyHC registry entry (the entry has no `logo:` key), no image
in `README.md` other than the PayPal donate button, and SoMEF reports no `logo` result.*

## Notes on Non-Obvious Values

Reasoning behind values whose basis is not self-evident from the repository. Rationale for the remaining
fields is recorded inline with each field above.

**Publication Date — 2018-07-22, replacing 2025-03-31.** The field denotes first publication of the
initial version. The previous value was the Zenodo `Issued` date of v1.0.12, which reached the record
through concept-DOI autofill rather than describing a first release. The first public release is PyPI
`1.0.1`, uploaded 2018-07-22, corroborated by the repository's creation date (2018-07-21) and by
`LICENSE` ("Copyright (c) 2018 Sheng Tian"). The repository's oldest commits date from 2015 but are IDL
`.pro` files from an earlier, unrelated project and predate the Python package.

**Version Date — 2026-05-16, which is the release date rather than the package-index upload date.** The
GitHub release `v1.0.13` was published 2026-05-16. This entry's established convention is the release
date: v1.0.12 is recorded as 2025-03-31, exactly its GitHub release and Zenodo publication date, whereas
its PyPI upload did not follow until 2025-09-03, five months later. PyPI's 2026-05-12 upload of 1.0.13 is
therefore not what this field denotes. Note also that the `v1.0.13` git tag is not a reliable date source
(see the repository data-quality notes below).

**Version PID — deliberately empty.** Recorded under Field 12: no Zenodo DOI exists for v1.0.13, and
carrying v1.0.12's DOI forward would misattribute it.

**Software Functionality — the parent category `Data Processing and Analysis` was previously missing.** Selecting a
subcategory does not imply its parent, so the entry previously carried
`Data Processing and Analysis: Field-line Tracing` without its required parent. That is corrected here,
alongside eight further values evidenced by specific code.

**Sheng Tian has no author identifier.** No ORCID could be confidently matched; searches returned only
unrelated people. Left blank rather than guessed.

**Rachel Frissell has no author identifier.** A name-matching ORCID exists but is an empty record; see
Field 6, Author 5.

**Fields 31 and 32 are empty by design.** geopack is instrument- and observatory-agnostic: it implements
global empirical field models and coordinate transforms and reads no instrument's data. No candidate met
the "designed to support" threshold, and no association was manufactured. Rejected candidates and the
reason for each are recorded under those fields.

## Known Repository Data-Quality Issues (not HSSI metadata; recorded for the maintainer)

1. **`CITATION.cff` is malformed.** `cff-version: 1.0.12` is the *software* version, not a CFF
   specification version (valid values are `1.1.0` / `1.2.0`). The file also lists only one of the five
   Zenodo creators and lacks `title`, `version`, and `date-released`. It is therefore not reliable as an
   author source; Zenodo record 15110787 plus git history support the author list instead.
2. **The `v1.0.13` git tag is misplaced.** Tag `v1.0.13` points at `8c5f0e0` (2026-03-06), where
   `setup.py` still reads `version='1.0.12'`; the bump to `1.0.13` landed later in `ab7efdc`
   (2026-06-25). The tag date is consequently **not** the release date.
3. **Three dead README links** (see Field 29).
4. **A stale `Development Status :: 3 - Alpha` classifier** in `setup.py` (see Field 23).
