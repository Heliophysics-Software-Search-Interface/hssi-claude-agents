# HSSI Metadata Extraction Results

**HSSI Software ID:** 9da56adf-1252-4ca9-85cf-5fd8fb950cdf
**Repository:** https://github.com/nbarbey/TomograPy
**Source Revision:** 357c66280ca7a8a02d3629611d8a73e42b6d3881
**Extraction Date:** 2026-09-12
**Validation Date:** 2026-09-12
**Validation Status:** PASS

---

**Scope note — read this before weighing any repository evidence.** TomograPy's source tree stopped
changing in 2011. The last commit that touches code is `a1da41f1e0b7406a1b770e56428789c54175de20`
(2011-03-31, a `setup.py` tweak); the only later commit in the history is
`357c66280ca7a8a02d3629611d8a73e42b6d3881` (2023-11-02), which adds a banner to `README.rst` and
changes nothing else. Consequently the repository's own prose has drifted behind its code, and in
two places the README is demonstrably *wrong about the package it ships*. The authoritative modern
description of what this software does is not the README but the authors' own refereed software
paper, Barbey, Guennou and Auchère (2013), *TomograPy: A Fast, Instrument-Independent, Solar
Tomography Software*, Solar Physics 283, 227–245, https://doi.org/10.1007/s11207-011-9792-8
(preprint arXiv:1103.5904). Where the README and the paper disagree, this dossier follows the paper
and the code, and says so at the field.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found

**Negative research, so this is not re-opened without new evidence.** TomograPy has no software DOI.

- The source tree at the pinned revision contains no `CITATION.cff`, no `codemeta.json`, no
  `.zenodo.json` and no DOI badge; `README.rst` carries no DOI. The complete tracked file list is 40
  files, none of them a citation-metadata file.
- Zenodo returns zero records for `metadata.title:"TomograPy"` and zero for the free-text query
  `"nbarbey/TomograPy"`. The same query shape run for `metadata.title:"sunpy"` returns records, so
  the search route works and the zeroes are real absences rather than a malformed query.
- DataCite's `query=TomograPy` returned 19 records when measured on 2026-09-12 with
  `curl -G https://api.datacite.org/dois --data-urlencode 'query=TomograPy'
  --data-urlencode 'page[size]=100'`, and exactly one of them is this software:
  `10.48550/arXiv.1103.5904`. The denominator is worth recording, because the other 18 hits are a
  coincidence rather than noise in the search: every one of them is a medical, dental, seismic,
  proton- or quantum-tomography record whose abstract or subject keywords contain the misspelling
  "tomograpy" for "tomography" (for example `10.5167/uzh-32834`, a comment on a forensic-dentistry
  paper). A future agent re-running this query should expect that background and should not read a
  rising hit count as evidence that a software DOI has appeared. The one real hit is arXiv's
  automatically minted **preprint** DOI for the software paper, not a persistent identifier for the
  software, and it must not be recorded here. (The refereed version of that same paper is the
  Field 14 Reference Publication.)
- The repository has **no git tags at all** and no GitHub releases, so there was never a
  release event for a Zenodo–GitHub integration to capture. The 2011 distribution channel was the
  Python Package Index, which does not mint DOIs.

Considered and rejected: recording `https://doi.org/10.48550/arXiv.1103.5904` here. It identifies a
publication, and Fields 14 and 27 are where publication DOIs belong; putting it in Field 2 would make
HSSI's "Cite Me" block render the software as a journal article.

### 3. Code Repository (MANDATORY)
https://github.com/nbarbey/TomograPy

The repository is live and is not a redirect — the URL resolves to itself. The default branch is
`master` and the repository is **not archived**. The `nbarbey/TomograPy` repository is not a fork.

Considered and rejected as the Field 3 value: `http://nbarbey.dyndns.org/software/siddon.html`, the
`url` recorded in `setup.py` and carried into the PyPI metadata. It is a dynamic-DNS host from the
package's 2011 era and is not the code repository even if it resolved. Also rejected:
`https://github.com/nbarbey/siddon`, which `README.rst` still advertises under "Home page". That is
the project's pre-rename name — commit `b3c667f76fe39a5f0333e31d593f4d0772172ae8` (2011-03-07)
"Renamed Siddon to TomograPy" — and the README line was never updated afterwards. A future agent
reading that README line should treat it as stale, not as a second repository.

### 4. Software Functionality (RECOMMENDED)

**Order is data.** `softwareFunctionality` is stored as an *ordered* list. Before this refresh HSSI
held exactly two values for it, both bare top-level categories and no subcategory at all:
`Data Visualization` followed by `Data Processing and Analysis`. Those two are the entries at
positions 1 and 5 of the list below, and their relative order is preserved, which is what the
ordered-list rule requires. Everything else in the list — every subcategory, including the
subcategories of those two parents, and both of the other parent categories — is new, inserted inside
its own parent's block or appended as a new parent block. The list must not be re-sorted, and a later
pass must not "tidy" it into alphabetical order.

- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Movies
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Image Processing
- Coordinate Transforms
- Coordinate Transforms: Solar
- Models and Simulations
- Models and Simulations: Forward-Fitting
- Models and Simulations: Physics-Based

Every value is written `Parent: Child` because thirteen subcategory names in this vocabulary sit on
more than one row; an unqualified child would bind to an arbitrary twin. Both `2D Slices` entries
below are instances of exactly that hazard, which is why each names its parent.

**Evidence, value by value.**

*Data Visualization* and its children come from `tomograpy/display.py`, the package's dedicated
plotting module.
- **2D Graphics** — `sinogram()`, `display_object()` and `display_surface()` all end in
  `plt.imshow(...)`; `sinogram()` additionally computes and displays a sinogram of the image stack.
- **Movies** — `data_movie()`'s docstring opens "Display all images of a data cube as a movie." and
  the function loops over the image index redrawing a single `imshow` artist. This is the explicit,
  user-facing animation entry point.
- **2D Slices** — `display_object()` tiles the z-slices of the reconstructed 3-D cube into one image,
  and `display_surface()` renders a 2-D surface interpolated out of the 3-D map.

*Data Processing and Analysis* and its children:
- **Analysis** — the package's product is a derived physical quantity, not a re-formatted file. The
  Thomson model in `tomograpy/models.py` yields coronal electron density; the paper's Section 5.3 is
  titled "Thomson scattering with COR1 A and B data" and states "We estimated the coronal electron
  density using COR1 A and B data acquired during February 2008 as done by Kramar et al. (2009)."
- **Image Processing** — the whole package is a reconstruction from stacks of 2-D solar images:
  `solar.read_data()` bins images by `bin_factor`, `solar.define_data_mask()` masks by solar radius
  and by NaN/negative value, and `display.extract_surface()` interpolates with
  `scipy.ndimage.map_coordinates`.
- **Data Reduction** — `read_data(..., bin_factor=N)` bins images down before inversion;
  `filter_files(..., time_step=...)` thins the image sequence in time; and `models.mask_object()`
  calls `lo.decimate` to drop masked voxels from the operator. All three reduce data volume while
  preserving the information the inversion needs, and the shipped `srt_default.cfg` sets `bin = 16`.
- **2D Slices** — `display.extract_surface()` returns a 2-D ndarray interpolated out of the 3-D
  object map (the processing step), which `display_surface()` then plots (the visualization step).
  `solar.slice_data()` extracts a single image plus its header from the data cube.

*Coordinate Transforms: Solar* — this is a user-facing capability, not an internal utility.
`solar.update_header()` reads the Carrington heliographic observer coordinates `CRLN_OBS`/`CRLT_OBS`
(falling back to heliocentric-Aries-ecliptic `HAEX`/`HAEY`/`HAEZ` when `DSUN_OBS` is absent) and
converts them into the Cartesian viewpoint vector `M1, M2, M3` that the projector consumes; it also
converts `CDELT`/`CRVAL` from arcseconds or degrees to radians. `display.py` exposes three named
heliographic map projections of the reconstructed cube — `equirectangular()`, `gnomonic()` and
`orthographic()` — plus the public helpers `sphe2cart()` and `phy2pix()`. The paper states the design
principle directly: "It relies on the World Coordinate System standard to manage various data
sources." The paper's own figures are captioned with these projections ("North pole gnomonic…",
"Equi-rectangular projection of a static 3D map estimation").

*Models and Simulations* — `tomograpy/simu.py` builds synthetic image stacks and
`tomograpy/phantom.py` generates Shepp-Logan, modified Shepp-Logan and Yu-Ye-Wang 3-D phantoms, so
the package simulates as well as inverts.
- **Forward-Fitting** — this is the core of the package. `siddon.projector()` is the forward model
  (a conic line-of-sight projection of a 3-D map into an image stack) and `backprojector()` its
  adjoint; `models.srt()`, `models.stsrt()` and `models.thomson()` assemble that operator with
  smoothness priors and masks, and the `srt` command-line tool then minimizes the regularized
  least-squares objective with an iterative optimizer (`lo.acg` in six of the thirteen files in
  `exemples/`; a seventh, `test_siddon_secchi_dt.py`, has its `lo.acg` call commented out at line 56
  and runs `lo.rls` instead). Synthetic
  data, a forward operator and parameter optimization is exactly this category.
- **Physics-Based** — `models.thomson()` and its helpers `_thomson_coef()`, `_pb_thomson_coef()`,
  `_r2omega()` and `_impact_parameter()` implement the Thomson-scattering coefficients "as defined by
  Billings", with a limb-darkening parameter `u`. This is a radiative-transfer model of a physical
  process, not a curve fit.

**Considered and rejected — each with the reason, so they are not re-proposed.**

- **Data Processing and Analysis: Data Access and Retrieval.** Rejected. `solar.read_data(path, ...)`
  takes a *local directory*, `os.listdir`s it and opens each file with `pyfits`. A search of every
  `.py` file and the `srt` script at the pinned revision for `urllib|httplib|requests\.|ftplib|urlopen|http://|https://`
  returns nine hits and every one of them is a URL inside a comment or a docstring (the ADS link for
  Siddon 1985, five Wikipedia links and a MathWorks link in `phantom.py`, the FITS-standard link in
  `siddon.py`, and the `setup.py` `url=`). Those comment hits are the positive control: the pattern
  does match URLs in this tree, so the absence of any client code is a real absence. TomograPy has no
  network layer; the user fetches and pre-processes the data themselves.
- **Data Processing and Analysis: File Format Conversion.** Rejected. FITS in, FITS out — there is no
  second format to convert to or from.
- **Data Processing and Analysis: Time Series Analysis.** Rejected, though it is the closest call
  here. `solar.get_times()`, `sort_data_array()` and `temporal_groups_indexes()` do order and group
  images in time, and `models.stsrt()` applies a temporal smoothness prior. But this is temporal
  *regularization inside a spatial inversion*, not analysis of a time series as a signal: nothing
  filters, detrends, autocorrelates or spectrally analyses a time-ordered quantity. A user filtering
  HSSI for time-series analysis tools would not want a tomography package back.
- **Data Visualization: 3D Graphics.** Rejected. The package's *output* is a 3-D map, but nothing
  renders it in 3-D: there is no `mplot3d`, `vtk`, `mayavi` or `pyvista` anywhere. The 3-D result is
  always shown as tiled 2-D slices or as a 2-D map projection, which is why `2D Slices` and
  `2D Graphics` are selected instead.
- **Data Visualization: Spectrogram** and **Data Processing and Analysis: Spectrogram.** Rejected,
  and worth recording because the near-miss is easy to make: `display.sinogram()` computes a
  *sinogram* — intensity as a function of angle around the solar limb versus image index — which is a
  tomography diagnostic, not a time-frequency representation. There is no FFT, STFT or wavelet
  anywhere in the package.
- **Data Visualization: Line Plots.** Rejected — there is no `plt.plot` call in the package; every
  display path goes through `imshow`.
- **Mission-related** and **Mission-related: Analysis.** Rejected. A pre-campaign extraction of this
  software proposed both. They are wrong under the category's governing distinction: "Mission-related"
  is for software that is *part of a mission's ground system or data pipeline*, not for
  general-purpose analysis software that happens to read mission data. TomograPy is a scientist's
  analysis package that a user points at a directory of FITS files they obtained themselves; it has
  no role in any STEREO or SOHO ground segment, and no mission team operates it.
- **Models and Simulations: Theory.** Rejected. Also proposed by the pre-campaign extraction. The
  Billings Thomson coefficients are an analytic formula *used inside* a numerical model; the package
  offers no analytical solution or theoretical framework as a user-facing product.
- **Models and Simulations: First Principles.** Rejected — the Thomson model is an analytic
  radiative-transfer expression, not a simulation derived from fundamental kinetic or fluid equations.
- **Models and Simulations: Data Guided.** Rejected. The reconstruction is driven entirely by
  observations, but that is what makes it an *inversion*, already captured by Forward-Fitting. "Data
  Guided" is for models whose boundaries or drivers are observational while the model itself is
  independent.
- **Coordinate Transforms: Heliospheric.** Rejected. Heliocentric-Aries-ecliptic coordinates do appear
  (`HAEX`/`HAEY`/`HAEZ` in `solar.update_header`) but only as a fallback way of recovering the
  observer's distance from the Sun when `DSUN_OBS` is missing. No heliospheric frame is offered to the
  user as a conversion; every user-facing transform is solar/heliographic.
- **Servers and Environments: High Performance Computing.** Rejected. The C extension is genuinely
  parallel — the OpenMP pragmas live in the template `tomograpy/C_siddon.c.template`, which carries
  seventeen lines mentioning `omp` at the pinned revision (`grep -c 'omp'
  tomograpy/C_siddon.c.template` → 17, case-sensitive, whole file). Note for a future agent that no
  file named plainly `C_siddon.c` is ever produced: `tomograpy/parse_templates.py`'s `set_filename()`
  appends a variant suffix built from the C type, obstacle mode and projector direction, so the
  generated sources are `C_siddon_<suffix>.c` and a search for `C_siddon.c` finds nothing. Beyond the
  template, `setup.py` compiles with `-fopenmp`, the projector takes an `nthread` argument, and the
  paper advertises scaling
  "linearly with the number of cores". But OpenMP threading inside a library is an implementation
  technique, not a server or runtime-environment capability: there is no MPI, no job script, no
  scheduler integration and no container. The `Servers and Environments` parent describes
  infrastructure software, which TomograPy is not.

### 5. Related Region (RECOMMENDED)
- Solar Environment
- Corona

**Order is data.** `relatedRegion` is an ordered list. `Solar Environment` is HSSI's stored value and
holds first position; `Corona` is appended.

`Corona` is the specific region this software reconstructs, and adding it is the single largest
discovery improvement available in this field. The `Region` vocabulary is **flat** — its rows have no
working parent/child links, so `Solar Environment` does **not** imply `Corona` and a user browsing the
`Corona` region would not have found this software before this refresh. The evidence is
unambiguous: the paper's Section 5 reconstructs the corona, `models.srt()` masks the object with
`obstacle="sun"` and radial limits (`obj_rmin`/`obj_rmax`, defaulting to 1 and 1.7 solar radii in
`srt_default.cfg`) so that only the region above the solar surface is reconstructed, and the Thomson
model estimates coronal electron density.

`Solar Environment` is retained because it is true and is the stored value; it is the broad
category a user browsing solar software would start from.

Considered and rejected from the 24-row vocabulary: `Photosphere`, `Chromosphere` and
`Solar Interior` — the object mask excludes everything at or below one solar radius, so the package
reconstructs none of them; `Solar Wind`, `Interplanetary Space` and `Heliosheath` — the shipped
configuration reconstructs out to 1.7 solar radii and the COR1 example to 3, which is coronal, and
the package models no wind; every planetary and Earth region — the package has no terrestrial or
planetary content whatsoever.

### 6. Authors (MANDATORY)

**Order is data.** `authors` is stored as an *ordered* list. The three authors below appear in HSSI's
stored order and that order is preserved deliberately — see the note after Author 3 before changing it.

**Author 1:**
- **Author Name:** Frédéric Auchère
- **Author Identifier:** https://orcid.org/0000-0003-0972-7022
- **Affiliation:**
  - **Organization:** Institut d'Astrophysique Spatiale, Université Paris-Sud
  - **Affiliation Identifier:** https://ror.org/014p8mr66

**Author 2:**
- **Author Name:** Nicolas Barbey
- **Author Identifier:** Not found
- **Affiliation:**
  - **Organization:** Commissariat à l'Énergie Atomique et aux Énergies Alternatives
  - **Affiliation Identifier:** https://ror.org/00jjx8s55

**Author 3:**
- **Author Name:** Chloé Guennou
- **Author Identifier:** https://orcid.org/0000-0002-6048-011X
- **Affiliation:**
  - **Organization:** Institut d'Astrophysique Spatiale, Université Paris-Sud
  - **Affiliation Identifier:** https://ror.org/014p8mr66

**Why these three, and why these affiliations.** The authoritative source is the byline and
affiliation block of the software paper, which the three of them wrote about this package. The
quotations below are taken from the text layer of the arXiv PDF of that paper
(`https://arxiv.org/pdf/1103.5904`, sha256 `fe935bc1637952eb0e384c451431beec75cd1243e07fe6f337d5a9de6c75eece`,
extracted with `pdftotext`), so any future agent can reproduce the check against a named artifact;
line breaks in the extracted text are shown here as single spaces. The byline reads
"N. Barbey1 · C. Guennou2 · F. Auchère2", with "1 SAp/Irfu/DSM/CEA, Centre d’études de Saclay, Orme
des Merisiers, Bâtiment 709, 91191 Gif sur Yvette, France email: nicolas.barbey@cea.fr" and
"2 Institut d’Astrophysique Spatiale, Bâtiment 121, Université Paris-Sud, 91405 Orsay, France email:
frederic.auchere@ias.u-psud.fr email: chloe.guennou@ias.u-psud.fr". Two transcription points are
recorded so they are not "corrected" in either direction. First, the affiliation markers are
superscript 1 and 2 on the typeset page but extract as ordinary ASCII digits, and the quotations
follow the extracted text. Second, the paper writes both French institution names with the
typographic apostrophe U+2019 (`d’études`, `d’Astrophysique`), whereas the organization name HSSI
stores for the two IAS authors uses an ASCII apostrophe; that difference is between the two sources
and is not an error in either, and the stored value must not be re-punctuated to match the paper.
Allowing for it, the affiliations HSSI already stores match that block: Barbey at CEA, Auchère and
Guennou at IAS/Université Paris-Sud.

**A repository-versus-paper divergence that must not be "corrected" back.** The repository's `AUTHOR`
file reads "This software has been written by: Nicolas Barbey (nicolas.a.barbey@gmail.com). Tests have
been performed by: Chloé Guennou (chloe.guennou@ias.u-psud.fr) Frédéric Auchère
(frederic.auchere@ias.u-psud.fr)", and `setup.py` names only `author='Nicolas Barbey'`. Read alone,
that file would demote Guennou and Auchère to testers and reduce this record to a single author.
That would be wrong. The refereed software paper — published *after* the last code commit and
describing this exact package — credits all three as authors, and the three-author list HSSI already
holds is therefore better evidence than the repository's own `AUTHOR` file. This is recorded
explicitly because the repository text is the tempting thing to follow and is the less authoritative
source here.

**Author identifiers.**

- *Frédéric Auchère* — ORCID `0000-0003-0972-7022`, already stored. An ORCID search with
  `given-names:Frédéric AND family-name:Auchère` returns exactly one record, whose name is "Frédéric
  Auchère" and whose institution is "Institut d'Astrophysique Spatiale" — the same institution
  recorded against him here.
- *Chloé Guennou* — ORCID `0000-0002-6048-011X`, which is the identifier HSSI stores for this
  author. HSSI held no identifier for her before this refresh; it was supplied by a direct
  database update, for the reason given below. An ORCID search for `family-name:Guennou` returns
  three records; only one is named "Chloé Guennou", and the other two are plainly different people
  (Mael Guennou, a ferroelectrics researcher, and Annaig Martin-Guennou). The match is confirmed
  from the record's own works list, which contains her IAS doctoral thesis "Propriétés thermiques
  et morphologiques de la couronne solaire", "RELATIVE ABUNDANCE MEASUREMENTS in PLUMES and
  INTERPLUMES", "Global helium abundance measurements in the solar corona" and the
  differential-emission-measure papers she published with Auchère. This is the solar physicist who
  co-authored the TomograPy paper. The decisive item is stronger still, and is recorded here so it
  does not have to be rediscovered: that ORCID record contains **the TomograPy paper itself**. Her
  works list at `https://pub.orcid.org/v3.0/0000-0002-6048-011X/works` includes "TomograPy: A
  Fast, Instrument-Independent, Solar Tomography Software" carrying DOI
  `10.1007/s11207-011-9792-8` — the Field 14 Reference Publication. That is a self-asserted link
  from the ORCID to this exact software paper, which is the most durable identity evidence
  available for this author.
  Also worth recording as negative research: `https://pub.orcid.org/v3.0/0000-0002-6048-011X/employments`
  returns an empty `affiliation-group`, so this record carries **no employment entries at all**. Her
  IAS affiliation here therefore rests on the paper's affiliation block and on her works list, not on
  an ORCID employment record, and a future agent should not go looking for one.
- *Nicolas Barbey* — no ORCID exists. The fielded search `given-names:Nicolas AND family-name:Barbey`
  returns zero records. The identically shaped query for Auchère returns one, so the search route and
  the accented-name handling both work and this zero is a real absence, not a query artifact. Do not
  attach an ORCID to this author on the strength of a bare surname search: "Barbey" alone matches
  unrelated people. His known addresses are `nicolas.barbey@cea.fr` (`setup.py`, PyPI and the
  paper) and `nicolas.a.barbey@gmail.com` (the `AUTHOR` file). The commits he authored at the pinned
  revision are split across three git identities — `nicolas.a.barbey@gmail.com` on 327 commits,
  `nbarbey@sol-calcul1.ias.u-psud.fr` on 8 and `nbarbey@asus.localdomain` on 2 — of which the last
  two are hostname-derived machine identities rather than mailboxes. They are recorded so a future
  agent sweeping commit emails does not mistake them for additional contributors; the only other
  committer in this repository is `hughes.jmb@gmail.com`, with the single 2023 README commit.

**Durable platform rule, and a fact about this author row that outlives this refresh.** An ORCID
cannot be attached to an author HSSI already stores without one through the ordinary metadata-update
path: that write resolves by identifier, finds no match, and creates a *second* author record,
leaving the original stranded and still identifier-less. Supplying an identifier for an
already-stored, identifier-less author therefore requires a direct database update, which is how
Guennou's ORCID above came to be stored against her existing author row rather than a duplicate of
it. The second fact matters as much and is easy to miss: this is HSSI's single `Chloé Guennou` author
row, and the sunpy entry binds that same row. Anything done to it — a name correction, a different
identifier — changes both entries at once, and must be weighed against both records rather than
against this one alone.

**Affiliation identifier that was previously missing.** A pre-campaign extraction of this software
recorded "Affiliation Identifier: Not found" for both IAS authors. That is wrong — the organization
HSSI stores carries `https://ror.org/014p8mr66`, whose ROR record lists the acronym "IAS", the alias
"Institute for Space Astrophysics", the alias "UMR 8617" and the website `https://www.ias.u-psud.fr`.
Note that ROR's own display name for that identifier is the shorter "Institut d'Astrophysique
Spatiale"; the longer stored name "Institut d'Astrophysique Spatiale, Université Paris-Sud" matches
how the paper writes it and is not an error.

**Considered and not selected: reordering the authors to the paper's byline.** The stored order,
which this dossier keeps, is Auchère, Barbey, Guennou — alphabetical by family name, and not the
paper's byline order, which is Barbey, Guennou, Auchère. Barbey is the software's sole code author and
the paper's first author, so a real case existed for reordering to the byline. It was not taken:
`authors` order is stored data, the existing order may have been chosen deliberately by whoever
created this record, and reordering would churn stored data to express a preference rather than to
correct an error. The byline order is recorded here so the alternative does not have to be
rediscovered.

**Considered and rejected: Marcus Hughes as an author.** `hughes.jmb@gmail.com` is the committer of
the pinned revision, but that commit does nothing except add the successor banner to `README.rst`.
He contributed no code to this package. He is the author of the successor project (Field 29) and
belongs there, not here.

### 7. Software Name (MANDATORY)
TomograPy

The capitalization is the authors' own and is consistent across every authoritative source: the
`setup.py` `name='TomograPy'`, the PyPI distribution name `TomograPy`, the paper's title
"TomograPy: A Fast, Instrument-Independent, Solar Tomography Software", the README heading, and the
GitHub repository name. Note the internal capital P — it is a deliberate pun on "tomography" plus
"Py", and normalizing it to "Tomograpy" or "TomograPY" would be wrong.

The package's *import* name is lowercase `tomograpy` (the Python package directory), which is a
Python naming convention rather than an alternative product name.

### 8. Description (MANDATORY)
TomograPy is a fast parallelized tomography projector and backprojector for solar physics applications. It implements the Siddon algorithm with OpenMP parallelization for efficient ray tracing. For solar astrophysics, TomograPy enables tomographic reconstructions of the solar corona by processing data from spacecraft such as SOHO and STEREO. The software can take Extreme-Ultraviolet (EUV) and white-light coronagraph data and output 3-dimensional maps of the corona. The package includes modules for solar rotational tomography (SRT), smooth temporal solar rotational tomography (STSRT), Thomson scattering models, data simulation, phantom generation, and visualization tools.

This is the description HSSI already stores, retained verbatim. It was checked clause by clause
against the code and the paper and is accurate throughout: the Siddon projector and backprojector are
`siddon.projector()`/`backprojector()`; the OpenMP parallelization is the `-fopenmp` build of
`C_siddon.c.template`; `models.py` defines `srt`, `stsrt` and `thomson`; `simu.py` builds synthetic
data; `phantom.py` generates Shepp-Logan, modified Shepp-Logan and Yu-Ye-Wang phantoms; `display.py`
is the visualization module.

**One clause deserves a note, because the repository contradicts it and the repository is wrong.**
`README.rst` says "For now only Extreme-Ultraviolet data is handled but handling of coronographic data
is planed along with handling of data from other spacecrafts." — the whole sentence, including the
author's spelling of "planed". The stored description instead says the software takes EUV *and
white-light coronagraph* data. The stored description is correct and the README is stale:
`models.thomson()` is a complete, working Thomson-scattering model for white-light coronagraphs, it
is registered in the `srt` command-line tool's `model_dict`, and the paper's Section 5.3 is an
actual white-light reconstruction
titled "Thomson scattering with COR1 A and B data". The README line simply predates the feature and
was never revised. A future agent must not "fix" this description back to the README's wording.

### 9. Concise Description (OPTIONAL)
Fast parallelized tomography for solar coronal reconstructions using the Siddon algorithm.

Retained verbatim as stored. It is accurate and well-formed, and the wording is an editorial choice
that should not be churned for a stylistic alternative.

### 10. Publication Date (RECOMMENDED)
2010-07-27

The date of the repository's first commit,
`2cb5b27a0d497b5a44d29d2bb309053ea49be8ef`, whose message opens "Rewrite of siddon using fitsarray
extensively. First commit." and continues "Problem with updating of data while (back)projecting."
(2010-07-27 21:36:28 +0200). This is HSSI's stored value and it is retained: the field asks
for the first publication of the *initial version*, and this is the earliest dated artifact of this
software's history.

Alternatives considered and not selected, recorded so they are not re-litigated:
- **2010-08-27**, the GitHub repository's creation timestamp. Defensible as the date the code first
  became *public* — the first commit predates it by a month and was local. Rejected as too fine a
  distinction to justify changing a stored value, and it would still not be the true first
  publication of the lineage (see below).
- **2011-03-08**, the PyPI upload of TomograPy 0.3.1. Rejected because the field is explicitly for the
  *initial* version, and 0.3.1 is not it. That date is recorded where it belongs, as the Field 12
  Version Date.
- Neither date is the origin of the software lineage. The first commit message says "Rewrite of
  siddon … First commit", and commit `b3c667f76fe39a5f0333e31d593f4d0772172ae8` (2011-03-07) is
  "Renamed Siddon to TomograPy". The package existed earlier as "siddon", in a repository whose
  history is not part of this one, so no earlier date is recoverable from the pinned tree.

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Correct under the field's own rule: Zenodo is the publisher only where a DOI was obtained through a
Zenodo workflow, and otherwise the repository host is named. TomograPy has no DOI (Field 2), so the
repository host is the right answer.

Considered and rejected: **Python Package Index**. TomograPy 0.3.1 was in fact distributed through
PyPI, and the paper's abstract calls it "an open-source software freely available on the Python
Package Index", so PyPI has a real claim. It is rejected because the field's guidance names the
*repository* host for the no-DOI case, and because the code repository recorded in Field 3 is the
GitHub one. The PyPI release itself is captured in Field 12.

### 12. Version (RECOMMENDED)
- **Version Number:** v0.3.1
- **Version Date:** 2011-03-08
- **Version Description:** Not found
- **Version PID:** Not found

**Which version anomaly this is.** The repository carries two different version numbers in two files:
`setup.py` declares `version='0.3.1'` while `tomograpy/__init__.py` ends with `version = "0.3.0"`.
There are **no git tags at all** in this repository and no GitHub releases, so the tree alone cannot
settle which number was shipped. It is settled by the distribution: the Python Package Index holds
exactly one TomograPy release, `TomograPy-0.3.1.tar.gz`, an sdist uploaded at
**2011-03-08T13:53:07Z**, with `author='Nicolas Barbey'`, `author_email='nicolas.barbey@cea.fr'` and
`summary='Solar tomography and Siddon algorithm'` — all matching this `setup.py` exactly. **0.3.1 is
therefore the released version**, and `__init__.py`'s `0.3.0` is a stale module attribute the author
forgot to bump. So this is *not* the "declared but never released" shape; it is the "two numbers, one
release" shape, resolved in favour of the packaged artifact.

**Why this field records `v0.3.1` rather than `0.3.1`, and why that must not be "fixed".** The value
HSSI stores carries a leading `v`; the released artifact does not. Neither of the authoritative
upstream sources ever writes the `v` — `setup.py` declares `version='0.3.1'`, and PyPI's only release
is `TomograPy-0.3.1.tar.gz` — so the stored string prefixes the upstream number with a conventional
release marker the author never used. That divergence was examined deliberately and left standing,
and this field records the stored value so the dossier and the record state the same thing. The
reason is that the cost is entirely one-sided. A version cannot be edited in place: changing the one
character would replace the whole version entry and strand the previous one, which is a real cost
paid for a purely cosmetic gain. Worse, any replacement would have to carry the release date forward
explicitly or lose the correct date already held. A future refresh should leave `v0.3.1` standing and
should not re-open this.

The version date is 2011-03-08, and HSSI already held that date, so recording it here confirms the
stored value rather than supplying something new. It is corroborated twice over from outside the
record: by the PyPI upload timestamp above, and from inside the repository by commit
`e0c9268c2e59bf566a3d6ea26054d515e341829e`, "Change version number", dated 2011-03-08 13:50:29 +0100
— about an hour before that upload, on the same day. A future agent does not need to re-derive it.

**Version Description: Not found.** There is no `CHANGELOG`, no release notes and no GitHub release
body; the PyPI record's `description` field is the literal string `UNKNOWN`. Nothing describes what
changed in 0.3.1, and inventing a summary from the commit log would be fabrication.

**Version PID: Not found** — there is no DOI for any version (see Field 2).

**A rendering trap attached to this field.** HSSI's read view renders the version as
"TomograPy - v0.3.1", which is the software name concatenated with the stored value. The stored value
is `v0.3.1`; the view's rendered string is a display form, not a value, and must never be copied back
in as one.

### 13. Programming Language (RECOMMENDED)
- C
- Python 2.x

Both are already stored and both are correct.

**C** — `tomograpy/C_siddon.c.template` is a 1000-plus-line CPython extension implementing the Siddon
ray-tracing kernel; `tomograpy/parse_templates.py` expands it into sixteen specialized variants (two
C types × two obstacle modes × four projector directions) that `setup.py` compiles as
`distutils.extension.Extension` modules with `-fopenmp`. The C is not vendored third-party code; it
is the performance core of the package.

**Python 2.x, not Python 3.** This is certain rather than inferred. The package uses Python 2-only
syntax that is a *SyntaxError* under Python 3: `except getopt.GetoptError, err:` and `print str(err)`
in `tomograpy/srt.py`. It also relies on Python 2-only names throughout — `xrange` in `display.py`,
`models.py` and `solar.py`, `dict.has_key` in `simu.py`, the `ConfigParser` module name, implicit
relative imports (`from siddon import *`, `import simu` inside `tomograpy/__init__.py`), and
`imp.load_source` in `setup.py`. The PyHC registry independently rates this package "Requires
improvement" for Python 3.

Considered and rejected: adding **Python 3.x**. There is no Python 3 support at any commit in this
repository, and adding it would mislead a user into trying an installation that cannot succeed.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1007/s11207-011-9792-8

Barbey, N., Guennou, C., Auchère, F. (2013). "TomograPy: A Fast, Instrument-Independent, Solar
Tomography Software." *Solar Physics* **283**, 227–245. Published online 2011-07-01, in print
2013-03. Preprint: arXiv:1103.5904, submitted 2011-03-30.

This is the canonical software paper — written by exactly the three authors in Field 6, about exactly
this package, naming it in the title. HSSI held no reference publication before this refresh, and
this is the most consequential single addition in this dossier: it is the citation a user of
TomograPy is expected to give, and without it the entry offered no way to cite the work.

The repository itself never mentions this paper, which is why it was missed: the paper was submitted
three weeks after the last substantive code commit and no README, docstring or metadata file was
updated afterwards. It was found by full-text search of the literature rather than by reading the
repository, and a future agent should not expect repository evidence for it.

Note the two-year gap between the DOI's online publication (2011) and its print issue (2013). Both
`2013SoPh..283..227B` and the 2011 online date refer to the same article; cite the DOI.

Also recorded, and deliberately *not* used here: the Astrophysics Source Code Library entry
`2011ascl.soft04001B`, which indexes this same software under the paper's title. ASCL entries are
catalogue records rather than publications and carry no DOI, so there is nothing to put in this field
from it.

### 15. License (RECOMMENDED)
Other

**The software's actual licence is CeCILL-B**, and `Other` is the only correct way to say so in this
vocabulary. The repository ships the full licence in two languages: `LICENSE` (515 lines, English,
opening "CeCILL-B FREE SOFTWARE LICENSE AGREEMENT") and `LICENCE_FR` (519 lines, French, "CONTRAT DE
LICENCE DE LOGICIEL LIBRE CeCILL-B"). The licence history is trivial: both files entered the tree in a
single commit, `da90a64ab2a43fadf41b2d015a8ad2106624bdd6` (2010-08-27, "Add project metadata files"),
and `LICENSE` has one blob across the whole history — it has never been changed or replaced.
CeCILL-B's SPDX identifier is `CECILL-B`. HSSI has no per-software licence URI field — `Software.license`
is a foreign key to a shared licence row that carries its own URL — so the SPDX identifier can only
live in this prose, not in the record.

HSSI held no licence value for this software before this refresh, so `Other` is new rather than a
correction.

**Every near-miss row ruled out by name**, because selecting one of them would misstate the legal
terms of the software:
- `BSD 2-Clause "Simplified" License` and `BSD 3-Clause "New" or "Revised" License` — the tempting
  substitution, since CeCILL-B is routinely described as "BSD-like". Rejected: CeCILL-B is a distinct
  licence text governed by French law, with a stronger attribution obligation than either BSD licence
  and with explicit compatibility articles (§5.3.5) for CeCILL and CeCILL-C that BSD has no analogue
  for. It is not a BSD licence and recording it as one would be a false statement of terms.
- `GNU General Public Licenses (GPL version 2)`, `GNU General Public License v3.0 or later`,
  `GNU Lesser General Public License v3.0 only`, `GNU Library or ‘Lesser’ General Public Licenses
  (LGPL version 2)` — rejected. (That last row name is quoted byte-for-byte from the live `License`
  vocabulary, curly U+2018/U+2019 quotation marks included; the straight-apostrophe spelling is not a
  vocabulary value and would not resolve.) CeCILL-B is the *permissive* member of the CeCILL family;
  it is CeCILL (unsuffixed) that is the GPL-compatible copyleft licence and CeCILL-C that is the
  LGPL-like one. Mapping CeCILL-B onto any GPL/LGPL row would assert copyleft obligations the
  software does not impose.
- `MIT License`, `Apache License 2.0`, `Creative Commons Attribution 4.0 International` — rejected;
  none of them is the licence in the repository.
- `Restricted` — rejected. CeCILL-B is an approved free-software licence granting broad rights to
  use, modify and redistribute; "Restricted" would tell a user the opposite of the truth.
- There is **no CeCILL row of any kind** in the licence vocabulary — not CeCILL, not CeCILL-B, not
  CeCILL-C. That absence is the whole reason this field reads `Other`, which is why it is recorded
  here rather than treated as a check to repeat.

Corroboration from a second source: GitHub's own licence detector classifies this repository as
`{"key": "other", "spdx_id": "NOASSERTION"}` — it recognises a licence is present but cannot map it to
an SPDX-standard row either.

If a `CeCILL-B Free Software License Agreement` row is ever added to the vocabulary, this field should
be changed to it.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- corona
- coronagraph
- euv
- extreme ultraviolet
- image reconstruction
- inverse problems
- rotational tomography
- siddon algorithm
- soho
- solar
- stereo
- thomson scattering
- tomography
- electron density
- world coordinate system

The first thirteen are HSSI's stored keywords, retained; the last two are additions. **They are
written lowercase because that is how they are stored** — HSSI's read view title-cases keywords for
display, so a stored `euv` renders as "Euv" and a stored `soho` as "Soho". Copying those rendered
forms back in would create duplicate rows differing only in case.

- **`electron density`** — the quantity the white-light Thomson inversion produces, and the term a
  user looking for coronal-density tools would search. The paper's Section 5.3 states "We estimated
  the coronal electron density using COR1 A and B data acquired during February 2008 as done by
  Kramar et al. (2009)." `models._pb_map_coef()` computes the per-voxel coefficients that convert
  the reconstructed map into density. A row with this exact name already exists in the keyword
  vocabulary, so this reuses it rather than creating a near-duplicate.
- **`world coordinate system`** — the package's defining design decision, and the reason its title
  claims instrument independence. `tomograpy/solar.py` opens "Generic code for WCS compatible data",
  `siddon.py`'s module docstring documents the FITS/WCS keywords it requires (`NAXIS`, `CRPIX`,
  `CRVAL`, `CDELT`), and the paper states "It relies on the World Coordinate System standard to
  manage various data sources." A row with this exact name already exists. The shorter existing row
  `wcs` was not added as well, to avoid two keywords for one concept.

Considered and rejected:
- **`polar plumes`** / **`plume`** — the paper's science results are about plumes (its Section 5
  reconstructions distinguish "beam plumes" from "curtain plumes"), but the *software* is not
  plume-specific; it reconstructs whatever coronal structure the data contain. Adding a keyword for
  one science application of one paper would mislead searchers. No such row exists, so this would also
  have created a new vocabulary entry for a weak claim.
- **`euvi`**, **`cor1`** — the instruments are recorded properly in Field 31 with their SPASE
  identifiers, which is where a user searching for instrument support will look. Duplicating them as
  free-text keywords adds nothing and would create new rows.
- **`openmp`**, **`parallel computing`** — implementation detail, not a subject a user browsing
  heliophysics software searches by. Neither row exists.

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific

Retained as stored, and correct. The package consumes calibrated FITS images produced by specific
solar observatories — `solar.read_data()`'s docstring opens "Read SOHO / STEREO data files and output
a Data instance", and its `filter_files()` selects on the `INSTRUME` and `TELESCOP` FITS keywords,
with the shipped `srt_default.cfg` setting `telescop = STEREOA` and `instrument = EUVI`. The
corresponding observatories are named in Fields 31 and 32, which is what selecting this value
obliges.

Considered and rejected from the 17-row vocabulary:
- **`HTTP/HTTPS Directories`, `FTP/FTPS Directories`, `S3/Cloud-aware`** — rejected. These describe
  software that retrieves data over a protocol. TomograPy retrieves nothing: `read_data` takes a local
  directory path and raises `ValueError('Directory does not exist')` otherwise. See the network probe
  recorded under Field 4.
- **`The Virtual Solar Observatory.`, `CDAWeb`, `SSCWeb`, `HAPI`, `OMNIWeb`, `AMDA`, `das2`,
  `Madrigal`, `GFZ`, `WDC`, `TAP`, `VirES`** — rejected for the same reason: the package implements no
  client for any archive or service.
- **`Other`** — rejected as strictly less informative than the accurate value above.

**Durable note on obtaining the data.** `README.rst` states "For solar tomography, you need first to
process data using http://www.lmsal.com/solarsoft/." The user's data pipeline is therefore external
to this package; that relationship is recorded in Field 30 rather than here, because it is an
interoperability fact, not a data-source capability of this software.

### 18. Input File Formats (RECOMMENDED)
- FITS

Retained as stored. `solar.read_data()` opens every file in the directory with
`pyfits.fitsopen(...)` and converts it with `fitsarray.hdu2fitsarray`; `srt.py` reads a starting-point
map with `pyfits.fitsopen(filename)[0].header`. The examples read SECCHI FITS directories. The entire
geometry model is expressed in FITS/WCS header keywords (`NAXIS`, `CRPIX`, `CRVAL`, `CDELT`,
`CRLN_OBS`, `CRLT_OBS`, `DSUN_OBS`, `DATE_OBS`).

Considered and rejected: `ascii` for `tomograpy/srt_default.cfg`. That is an INI configuration file
read with `ConfigParser`, not scientific data input, and listing it would make the package look as
though it ingests text data. `CDF`, `HDF5`, `netCDF3/4`, `IDL.sav`, `Zarr`, `csv`, `JSON` and
`ISTP-Compliant` — none appears anywhere in the package.

### 19. Output File Formats (RECOMMENDED)
- FITS

Retained as stored, and now confirmed from the code rather than inferred from a dependency list. The
`srt` command-line tool writes its result with `sol.tofits(output)`, defaulting to `srt.fts`
(`tomograpy/srt.py`), and the shipped examples write FITS explicitly —
`fsol.tofits('stsrt_test.fits')` in `exemples/test_siddon_secchi_dt.py` and
`fsol.tofits(os.path.join(tomograpy.path, "output", "test_tomograpy.secchi_mask.fits"))` in
`exemples/test_siddon_secchi_mask.py`. The reconstructed 3-D map carries a full FITS header, which is
what makes the output re-readable by the same package.

Note the `.fts` default extension: it is a conventional FITS extension, not a different format.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac

**`Operating System Independent` was removed from this field, and the removal is recorded here so a
later pass does not read the field's silence as an oversight and restore it.** HSSI held that value
alongside `Linux` and `Mac` before this refresh, and it is not true of the software. `setup.py` builds
every C extension with `extra_compile_args=['-fopenmp']` and `extra_link_args=['-fopenmp']`, and it
does so with **no platform branch** — there is no `sys.platform` test or any other conditional in the
file, so every target receives the same flag. `-fopenmp` is the GCC/Clang spelling of the OpenMP
option; MSVC, the default toolchain for Windows Python, does not accept it (it spells the option
`/openmp`), so a stock Windows build fails at compile time. The claim is worth stating precisely,
because a MinGW toolchain *would* accept `-fopenmp`: the package is buildable on Windows only by
stepping outside the default toolchain, which is not what "Operating System Independent" tells a
user. The package is also Python 2-only (Field 13), which narrows the usable environments further. A
user filtering HSSI for OS-independent software would have found TomograPy and then been unable to
build it.

Evidence for the two values that stay: the build is a plain `distutils` C extension with GCC-style
flags, which is the ordinary Linux and macOS toolchain; the package has no OS-specific code paths;
and the author's own commit identities include an IAS Linux host.

Considered and rejected: `Windows` (the `-fopenmp` flag above, plus `srt` being a shebang script
installed onto `PATH`), `Solaris`, `MobilePlatform` and `Other`.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Retained as stored, and now positively verified rather than assumed. The C kernel
`tomograpy/C_siddon.c.template` (1101 lines) contains no SIMD intrinsics, no inline assembly and no
architecture-specific code; it is portable C plus OpenMP pragmas, compiled from source at install
time for whatever machine the user is on.

**A trap worth recording**, because it produced a false positive during this extraction: a
case-insensitive search of that file for `sse|avx|__m128|intrin|x86|arm|asm` returns seven hits, and
every one of them is the substring `asm` inside the function name `PyDict_AsMapHeader`. A future
agent running the same probe must read the matching lines rather than trusting the hit count.

Considered and rejected: **`x86-64`**, which a pre-campaign extraction of this software recorded
alongside `CPU Independent`. There is nothing x86-specific in the source; the package would compile
on any architecture with an OpenMP-capable C compiler, and pinning it to x86-64 would wrongly exclude
it from Apple Silicon and aarch64 searches. Also rejected: `GPU`, `HPC or HEC` (no MPI, no scheduler
integration — see the Field 4 rejection of Servers and Environments), `Apple Silicon arm64`,
`Linux aarch64 or arm64`, `ppc64le`, `Sun (SPARC)` and `Other`.

### 22. Related Phenomena (RECOMMENDED)
- Coronal Heating
- Solar Corona

**Order is data.** `relatedPhenomena` is an ordered list; both values are already stored and their
order is preserved unchanged.

`Solar Corona` is the object this software reconstructs and needs no further argument.

`Coronal Heating` is the less obvious of the two and is retained deliberately. The paper's
introduction frames the whole package as an answer to the line-of-sight problem that blocks coronal
diagnostics: it argues that "the properties of astronomical objects are deduced from the analysis of
the properties of light only", that LOS integration "is one of the major sources of uncertainties in
the diagnostics of the solar plasma", and that this obstructs deciding "what processes are
responsible for their formation or for their heating" for coronal structures. Recovering the 3-D
distribution of coronal emission and density is a direct input to heating studies, which is exactly
what a user browsing the `Coronal Heating` phenomenon would hope to find.

Considered and rejected from the seven-row vocabulary:
- **`Coronal Mass Ejections`** — rejected. CMEs appear twice in the paper and neither is a claim about
  this software: one is a passing contrast with Thernisien's CME forward-modelling approach, the other
  is that paper in the reference list. Nothing in the package detects, tracks or models a CME, and a
  user browsing CME software would find TomograPy out of place.
- **`Solar Wind`** — rejected; the phrase does not occur in the paper at all, and the reconstruction
  domain (1 to 1.7 solar radii by default, 3 in the COR1 example) is below where the wind is the
  object of study.
- **`Solar Flares`**, **`X-ray emission`**, **`Geomagnetic Storms`** — rejected; the package has no
  flare, X-ray or geomagnetic content of any kind. Its passbands are EUV and white light.

Note that this vocabulary is **flat**: no phenomenon implies another, so both values above are
carried on their own evidence.

### 23. Development Status (RECOMMENDED)
Moved

**`Moved` was selected over `Unsupported` after weighing both.** HSSI held no development status for
this software before this refresh, so this is a new value rather than a correction, and the choice
between the two rows was a genuine judgement call rather than an obvious reading. Both arguments are
recorded in full below so that the reasoning does not have to be reconstructed and the rejected
alternative does not have to be re-derived.

The facts, all from the pinned repository and the GitHub API:
- The last commit that changes code is 2011-03-31. The tree has been functionally frozen since then.
- The only later commit, and the pinned revision itself, is 2023-11-02: it adds a single banner to the
  top of `README.rst` reading "A new version of this repo is being developed as `solartom
  <https://github.com/jmbhughes/solartom>`_", flanked by three exclamation marks on each side. It
  changes nothing else in the repository.
- That commit was made by Marcus Hughes, who created `jmbhughes/solartom` the same day. solartom is
  described as a "Python solar tomography package with Rust backend", is MIT-licensed, and is under
  active development.
- The repository is **not archived** and not disabled.

`Moved` is defined as "The project has been moved to a new location, and the version at that location
should be considered authoritative." The README banner is that statement almost word for word, it is
the most recent and most prominent maintainer communication about this repository, and it was placed
by the person who develops the successor. Selecting `Moved` means a visitor to TomograPy's HSSI entry
is told immediately that development continues elsewhere — which, with the solartom link in Field 29,
is the most useful thing the record can tell them.

**`Unsupported` was the main alternative, and its argument is recorded in full** because it was a
reasonable reading rather than a weak one, and should not have to be re-derived. It is defined as
"The project has reached a stable, usable state but the author(s) have ceased all work on it. A new
maintainer may be desired."
The first half is exactly true: 0.3.1 was released and works, and Barbey stopped in 2011. The second
half is what argues against it — a successor already exists and is named, so that definition's
closing sentence, "A new maintainer may be desired.", understates the situation. The
counter-argument in favour of `Unsupported` is that solartom is not a relocation of this codebase at
all: it is an independent reimplementation in a different language, under a different licence, by a
different author, and `TomograPy 0.3.1` remains the last released version of *this* software. A
reader could take `Moved` to mean the same code now lives elsewhere, which is not the case.

Also considered and rejected:
- **`Inactive`** ("no longer being actively developed; support/maintenance will be provided as time
  allows") — rejected. No support is provided; the last code change was 2011-03-31 and the maintainer
  has publicly redirected users elsewhere.
- **`Abandoned`**, **`Suspended`**, **`WIP`**, **`Concept`** — all four presuppose that no stable
  usable release exists. TomograPy 0.3.1 was released on PyPI on 2011-03-08 and the paper documents
  three working scientific reconstructions with it, so none of these applies.
- **`Active`** — plainly false; note that GitHub's `updated_at` for this repository advances for
  reasons unrelated to commits (it is not commit activity), so it must not be read as evidence of
  development.

### 24. Documentation (RECOMMENDED)
https://github.com/nbarbey/TomograPy/blob/master/README.rst

Retained as stored. It is reachable, and it is the best of a genuinely poor set of options.

**The obvious-looking alternative is a trap, and this is the most important negative finding in this
dossier.** `http://nbarbey.github.io/TomograPy` is what the PyHC registry records as this package's
`url`, what the GitHub repository records as its `homepage` (in the older `nbarbey.github.com` form),
and what the paper's own abstract gives as the software's address. A pre-campaign extraction of this
software recorded it as the Field 24 value. **It no longer serves TomograPy documentation.** The
`gh-pages` branch was replaced on 2023-09-29 with an unmodified Jupyter Book starter template; the
page at that URL redirects to `intro.html`, whose title is "Welcome to your Jupyter Book — My sample
book" and whose body reads "This is a small sample book to give you a feel for how book content is
structured… check out the Jupyter Book documentation for more information", over a "© Copyright 2022"
notice. The branch's other files are the template's stock samples (`markdown.md`,
`markdown-notebooks.md`, `notebooks.ipynb`). It returns HTTP 200, so a reachability check alone will
not catch this — the page must be read. Recording it would send every HSSI user looking for TomograPy
documentation to a Jupyter Book tutorial.

What the software actually offers instead: `README.rst` states "The documentation for TomograPy is
embedded into the code as docstrings.  To get started, take a look at tomograpy/__init__.py or in
IPython, just do :" — with a space before the colon, and with the two spaces after "docstrings."
that the file actually carries — and then, after a blank line, gives two separate doctest lines,
`>>> import tomograpy` and `>>> tomograpy?`. (They are two lines in the file, not one statement;
earlier metadata for this software rendered them as a single `import tomograpy; tomograpy?`, which
appears nowhere in the repository.) The repository ships a `make_doc` shell script that
runs `pydoc2 -w tomograpy` to generate HTML from those docstrings, but the generated output is not
committed anywhere and is not published. The README is therefore the only prose documentation that
exists at a stable URL, and it does contain the requirements and the usage entry points, which is
what this field asks for.

Also checked and found absent: **there is no repository wiki.** GitHub's `has_wiki` flag is `true`,
but that flag means only that the feature is enabled, and a wiki is a separate repository — `git
ls-remote https://github.com/nbarbey/TomograPy.wiki.git` answers "Repository not found". There is no
wiki content to point at.

A future refresh should re-read `http://nbarbey.github.io/TomograPy` before reconsidering it: if
solartom's author ever publishes real TomograPy documentation there it would become the better value,
but as long as it serves the starter template it must not be used.

### 25. Funder (OPTIONAL)
Not found

### 26. Award Title (OPTIONAL)
Not found

**Negative research for both fields, recorded together because one investigation covers both.**

- The repository contains no funding statement, no grant number and no acknowledgements file. There
  is no `CITATION.cff`, `codemeta.json` or `.zenodo.json` in which funding could have been declared.
- The software paper has **no acknowledgements section at all**. The full text of the preprint runs
  from the abstract through Section 5 and the conclusions straight into the reference list with no
  acknowledgements or funding statement in between; the word "acknowledg" does not occur anywhere in
  it. That the reference list itself extracts cleanly is the positive control showing the end of the
  paper was actually read rather than truncated.
- Cross-checked against the literature index's acknowledgements field, which stores the
  acknowledgements text separately from the body: probes for "support", "CNES", "ANR" and "NASA"
  restricted to this paper all return nothing, while the same probes return matches for other papers
  of the same period and venue — including contemporaneous Solar Physics papers acknowledging CNES —
  and a nonsense token returns nothing. The instrument could have returned a positive and did not.
- The publisher's structured metadata for the paper carries a null funder block.

**Settled campaign policy that applies here anyway.** Even had the paper carried a clause of the form
"author X is supported by grant Y", that is *author-level support and not software funding*, and such
clauses do not populate Fields 25 and 26. Two of the three authors were CEA and IAS/CNRS staff, so
institutional salary support certainly existed; that is not an award that funded this software and
must not be recorded as one.

Do not record `Commissariat à l'Énergie Atomique et aux Énergies Alternatives` or `Institut
d'Astrophysique Spatiale` as funders on the strength of the Field 6 affiliations. An employer is not
a funder, and those organizations are already recorded where they belong.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1118/1.595715
- https://doi.org/10.1007/s11207-008-9151-6
- https://doi.org/10.1051/eas/1255029

HSSI held no related publications for this software before this refresh. These three are chosen on
the field's own test — publications the *developers* prioritize, distinct from the Field 14 reference
publication — and each is tied to the package by something the authors themselves wrote.

- **Siddon, R. L. (1985). "Fast calculation of the exact radiological path for a three-dimensional CT
  array." *Medical Physics* 12(2), 252–255.** This is the algorithm the package is built on, and it is
  cited *inside the code*: `tomograpy/__init__.py` describes the `siddon` module as "The core of the
  package, with a fast C/OpenMP implementation of the Siddon algorithm. See:
  http://adsabs.harvard.edu/abs/1985MedPh..12..252S". A publication the source code points the reader
  to is developer-prioritized by construction. The DOI is recorded rather than the ADS link the
  docstring uses, per the field's preference.
- **Barbey, N., Auchère, F., Rodet, T., Vial, J.-C. (2008). "A Time-Evolving 3D Method Dedicated to
  the Reconstruction of Solar Plumes and Results Using Extreme Ultraviolet Data." *Solar Physics* 248,
  409.** The method paper for the time-evolving reconstruction that `models.stsrt()` implements —
  smooth temporal solar rotational tomography. Two of this software's three authors wrote it, and the
  software paper builds directly on it.
- **Auchère, F., Guennou, C., Barbey, N. (2012). "Tomographic reconstruction of polar plumes." *EAS
  Publications Series* 55, 207.** The authors' own science application of this software, by the same
  three people. It is what a user wanting to see TomograPy used in anger should read.

**Considered and rejected**, so these are not re-proposed:
- **`https://doi.org/10.1007/s11207-011-9792-8`** — the software paper itself. It belongs in Field 14
  and repeating it here would duplicate it in the record.
- **`https://doi.org/10.48550/arXiv.1103.5904`** — the preprint of that same paper. Same article, and
  the refereed DOI already represents it.
- **Third-party reviews and downstream citations.** The software paper is cited by a modest number of
  works; the citing set includes reviews such as "Solar Stereoscopy and Tomography" (Living Reviews in
  Solar Physics, 2011) and "Solar Coronal Plumes" (2015), and applications such as "Time-dependent
  tomographic reconstruction of the solar corona" and "Models and data analysis tools for the Solar
  Orbiter mission" (2019). They were examined and rejected: their citation contexts are *background*
  mentions placing TomograPy among other inversion codes ("Barbey et al. (2013) developed a more
  sophisticated procedure and tested it on polar plumes"), not works the developers would prioritize.
  Listing every paper that mentions a package is not what this field is for. If a future agent wants
  to reconsider one of them, "Models and data analysis tools for the Solar Orbiter mission"
  (`https://doi.org/10.1051/0004-6361/201935305`) is the strongest candidate, because it surveys
  TomograPy as a tool rather than citing it in passing.
- Note that some indexes return this DOI with uppercase segments (`10.1051/EAS/1255029`). DOIs are
  case-insensitive; the lowercase publisher form is recorded above.

### 28. Related Datasets (OPTIONAL)
Not found

The package has no bundled or referenced dataset with a persistent identifier. The paper's three
reconstructions use STEREO/EUVI and STEREO/COR1 Level-1 images that the authors obtained from the
SECCHI archive and pre-processed themselves; no dataset DOI, accession or landing page is cited for
them anywhere in the paper or the repository. The examples point at directories under the user's own
`$HOME/data`, which is a local path, not a dataset identifier.

This is consistent with what the software is: `solar.read_data()` reads whatever WCS-compliant FITS it
is handed, filtered by the `INSTRUME` and `TELESCOP` header keywords, so there is no specific dataset
the package is bound to. The observatories and instruments whose data it is designed for are recorded
in Fields 31 and 32, which is where a user will find that relationship.

**Route that could not be reached, so a future agent does not repeat the attempt the same way.**
`hpde.io`, the usual source of SPASE `NumericalData` landing pages for this field, does not resolve
from this environment — DNS returns NXDOMAIN for the domain. `spase-metadata.org` does resolve and
serve, and is where the Field 31/32 identifiers below were verified. A future agent with working
access to SPASE numerical-data records could revisit whether a STEREO/SECCHI Level-1 image product has
a citable landing page worth recording here; nothing in the repository or the paper requires one.

### 29. Related Software (OPTIONAL)
- https://github.com/jmbhughes/solartom
- https://github.com/nbarbey/fitsarray
- https://github.com/nbarbey/linear_operators

The first is already stored; the two others are additions.

- **`solartom`** — the declared successor, and the single most useful link on this record. The pinned
  revision's `README.rst` banner says "A new version of this repo is being developed as solartom",
  and the repository was created by Marcus Hughes on the same day that banner was committed
  (2023-11-02). It is described as a "Python solar tomography package with Rust backend", is
  MIT-licensed and remains under development. It is not a GitHub fork of this repository and shares no
  code with it — it is an independent reimplementation of the same purpose, which is exactly what this
  field is for: "Software that performs similar tasks but does not necessarily link together". It is
  not in the HSSI catalogue, so the URL above is a new entry rather than a pointer at an existing
  record.
- **`fitsarray`** — Nicolas Barbey's own companion package, and an unavoidable dependency:
  `tomograpy/siddon.py`, `simu.py`, `solar.py`, `models.py` and `lo_wrapper.py` all `import fitsarray
  as fa`, and the package's central data types (`InfoArray` for the image stack, `FitsArray` for the
  reconstruction cube) come from it. It is domain-specific rather than generic infrastructure — its
  own PyPI summary is "An ndarray subclass with a fits header", which is meaningless outside
  astronomy — and it passes the
  test that a generic dependency fails: it would make no sense in a web application or a finance
  model. Its PyPI release (0.2.0, author Nicolas Barbey, `requires = ['numpy (>1.3.0)', 'pyfits']`)
  matches the GitHub repository's `setup.py` exactly.
- **`linear_operators`** — Barbey's other companion package, which TomograPy imports as `lo`. This is
  the more arguable of the two and the counter-argument is recorded honestly: linear operators and
  iterative solvers are generic numerical machinery that would be equally at home in a finance model,
  which is normally grounds for exclusion. It is included anyway because it is not a third-party
  library the package happens to use — it is by the same author, released in parallel, and TomograPy
  ships a dedicated bridge module, `tomograpy/lo_wrapper.py`, whose entire purpose is to wrap the
  Siddon projector as an `lo` operator. Every *regularized inversion* the package offers goes through
  it: `tomograpy/models.py` builds `srt()`, `stsrt()` and `thomson()` on `siddon_lo` / `siddon4d_lo`
  imported from `lo_wrapper`, and `tomograpy/__init__.py` re-exports that module with
  `from lo_wrapper import *` whenever `import lo` succeeds. The `srt` command-line tool then calls
  the optimizer by name — `exec("sol = lo." + optimizer + "(P, b, D, hypers, **opt_params)")` at
  `tomograpy/srt.py:225` — and its `--optimizer` help text describes that name as a routine
  "from lo". The shipped examples are the narrower case and should not be over-claimed: of the
  thirteen files in `exemples/`, seven reference an `lo` routine and the other six — `test_bpj.py`,
  `test_siddon_lo.py`, `test_siddon_secchi.py`, `test_siddon_simu.py`, `test_siddon_simu_dt.py` and
  `test_siddon_simu_sun.py` — exercise projection and back-projection only, with no optimizer call
  at all. The field explicitly admits "a companion package",
  and this is one.
  **A practical trap attached to this entry.** TomograPy does `import lo`, which matches the **PyPI**
  distribution `lo` 0.2.0 (author Nicolas Barbey, summary "LinearOperators and Iterative algorithms").
  The GitHub repository linked above has since been renamed and its package directory is
  `linear_operators`, with `setup.py` declaring `name='linear_operators'` at the same version 0.2.0
  and the same author and description string. They are the same project under two names; installing
  from the current GitHub tree will not satisfy `import lo`. Anyone trying to make TomograPy run needs
  the PyPI `lo` 0.2.0 artifact.

**Considered and rejected:**
- **`numpy`, `scipy`** — required by `setup.py` but excluded as generic scientific-Python
  infrastructure. "It depends on numpy" is true of nearly every package in the catalogue and
  distinguishes nothing.
- **`matplotlib`** — imported by `display.py`, excluded for the same reason. Plotting is generic
  infrastructure.
- **`pyfits`** — a closer call, since FITS I/O is astronomy-specific. Rejected because it is a plain
  file-reading dependency with no exchange of data models: `read_data` calls `pyfits.fitsopen` and
  immediately hands the HDU to `fitsarray`. `pyfits` is also long since superseded by
  `astropy.io.fits`, so listing it would point users at a retired library. `fitsarray`, which *is*
  listed, is the package that actually characterizes TomograPy's data model.
- **`SolarSoft`** — genuinely related, but the relationship is a demonstrated data exchange rather
  than a similar-purpose or dependency relationship, so it is recorded in Field 30 instead.

### 30. Interoperable Software (OPTIONAL)
- https://www.lmsal.com/solarsoft/

HSSI held no interoperable software for this record before this refresh. This single entry is the
package's one genuine, documented interoperability relationship.

**The evidence is the authors' own instruction.** `README.rst` states, under "Exemple": "For solar
tomography, you need first to process data using http://www.lmsal.com/solarsoft/. Then you can take a
look at exemple/siddon_secchi_mask.py or use directly the siddon/srt script." SolarSoft's output —
calibrated, WCS-complete Level-1 FITS — is the required input to TomograPy, and TomograPy is built
around consuming it: `solar.read_data()` filters on the `INSTRUME` and `TELESCOP` keywords that
SolarSoft writes, and `solar.update_header()` reads the `CRLN_OBS`, `CRLT_OBS`, `DSUN_OBS`,
`HAEX_OBS`/`HAEY_OBS`/`HAEZ_OBS`, `PC2_1`/`PC1_1` and `CROTA2` keywords that SolarSoft's preparation
routines populate. That is a named domain tool whose output is imported into this one, across a
language boundary (IDL to Python), documented by the maintainers as a required step — which is the bar
this field sets, not mere co-existence in an environment.

The URL above is SolarSoft's exact stored code-repository URL in the HSSI catalogue, so this entry
points at the existing record rather than creating a second one for the same software.

**Considered and rejected:**
- **`solartom`** — the successor is a replacement, not an interoperating peer; there is no exchange
  between the two packages. It belongs in Field 29, where it is recorded.
- **`fitsarray` and `linear_operators`** — dependencies TomograPy is built on rather than peers it
  exchanges data with; recorded in Field 29.
- **`sunpy`** — rejected, and worth recording because it is the reflex association for any solar
  Python package. TomograPy predates sunpy's maturity, contains no reference to it, and defines its
  own FITS data model via `fitsarray` rather than exchanging `sunpy.map.Map` objects. There is no
  adapter, no converter and no documented use of the two together.
- **`astropy`** — same reasoning. The package uses `pyfits`, astropy's predecessor, and there is no
  astropy-specific interface anywhere in the code.
- **Blanket claims** such as "part of the scientific Python ecosystem" or "a PyHC-registered package,
  so it interoperates with PyHC packages" are not evidence and were not used.

### 31. Related Instruments (OPTIONAL)

**Instrument 1:**
- **Instrument Name:** Stereo-A Sun Earth Connection Coronal and Heliospheric Investigation
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI

**Instrument 2:**
- **Instrument Name:** Stereo-B Sun Earth Connection Coronal and Heliospheric Investigation
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI

**Instrument 3:**
- **Instrument Name:** Extreme UltraViolet Imager on the STEREO-A mission
- **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/EUVI

**Instrument 4:**
- **Instrument Name:** Extreme UltraViolet Imager on the STEREO-B mission
- **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/EUVI

**Instrument 5:**
- **Instrument Name:** STEREO-A SECCHI Cor1 Coronagraph
- **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/Cor1

**Instrument 6:**
- **Instrument Name:** STEREO-B SECCHI Cor1 Coronagraph
- **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/Cor1

Instruments 1 and 2 are already stored; instruments 3 to 6 are additions. Every name above is copied
verbatim from its vocabulary row — note the lowercase "tereo" in "Stereo-A"/"Stereo-B" on rows 1 and 2
and the mixed-case "Cor1" on rows 5 and 6; those are the stored spellings and must not be normalized.
Every entry carries a `https://spase-metadata.org/` identifier, which is the de-duplication key.

**Why EUVI and COR1 are added, and why the evidence is conclusive rather than inferential.** The
software paper's abstract states that the authors "show three practical examples of multi-spacecraft
tomographic inversions using STEREO/EUVI and STEREO/COR1 data", and the paper's results sections name
the spacecraft individually:
- §5.1 "Static Reconstruction using STEREO/EUVI A and B"
- §5.2 "Smooth Temporal Evolution with STEREO/EUVI A and B"
- §5.3 "Thomson scattering with COR1 A and B data" — "We estimated the coronal electron density
  using COR1 A and B data acquired during February 2008 as done by Kramar et al. (2009)."

That is per-spacecraft evidence for all four rows, from the authors of the software, which is exactly
the standard required before expanding a single instrument mention into several rows. The repository
corroborates it independently: the shipped command-line default configuration
`tomograpy/srt_default.cfg` sets `telescop = STEREOA` and `instrument = EUVI`;
`exemples/test_siddon_secchi_dt.py` selects `obsrvtry = ('STEREO_A', 'STEREO_B')` and
`exemples/test_siddon_secchi_mask.py` applies "the ratio of sensitivity between EUVI A and B" as a
per-spacecraft correction, which is code that only makes sense for a package supporting both; and
`exemples/test_siddon_cor1.py` runs the Thomson model over a `cor1` data directory.

**From the site user's side**, which is the test that matters: someone on the EUVI-A page clicking
"show software related to this instrument" gets back a coronal tomography package whose shipped
default configuration targets that exact instrument and whose reference paper reconstructs the corona
from its data. Someone on the COR1-A page gets back the package whose Thomson-scattering model was
demonstrated on COR1 A and B data. Neither would be surprised or annoyed; before this refresh neither
would have found it at all.

**A caveat on the COR1 example, recorded so it is not mistaken for a reason to drop the rows.**
`exemples/test_siddon_cor1.py` cannot run as committed: line 11 reads
`path = os.path.join(os.getenv('HOME'), 'data', 'tomograpy., 'cor1')`, an unterminated string literal
that is a `SyntaxError`. This is a defect in an example file, not evidence about instrument support —
the support is established by the paper's §5.3 and by the working `models.thomson()` implementation,
not by that file.

**Considered and rejected:**
- **`Extreme Ultraviolet Imaging Telescope` (SOHO/EIT, `SMWG/Instrument/SOHO/EIT`)** and
  **`Large Angle Spectroscopic Coronagraph` (SOHO/LASCO, `SMWG/Instrument/SOHO/LASCO`)** — rejected
  as instruments, although SOHO is retained at observatory level in Field 32. A word-boundary search
  of the whole tree for `\bEIT\b|\bLASCO\b|\bMDI\b|\bSWAP\b|\bAIA\b` returns exactly one hit, and it
  is a *commented-out* line in `exemples/test_siddon_cor1.py`: `#instrume = 'LASCO   '`, sitting above
  a commented `#obsrvtry = 'SOHO    '`. That the probe found the LASCO line is its own positive
  control — the pattern works, so the absence of EIT, MDI, SWAP and AIA is a real absence. A
  disabled line in an example is not designed-to-support, and the paper demonstrates no SOHO
  instrument.
- **`Heliospheric Imager-1`/`Heliospheric Imager-2` (SECCHI HI-1, HI-2) and `Cor2`** — rejected. These
  are the other SECCHI telescopes, and it would be easy to expand "SECCHI" into all of them. Nothing
  in the repository or the paper uses them: the paper's worked examples are EUVI and COR1 only, and
  the strings "HI-1", "HI-2" and "Cor2" appear nowhere in the tree. Expanding one instrument mention
  into a whole suite without per-instrument evidence is precisely the error the resolution rules
  forbid.
- The SECCHI suite rows (instruments 1 and 2) are **retained alongside** the EUVI and COR1 rows rather
  than replaced by them. EUVI and COR1 are SECCHI telescopes, and a user browsing the SECCHI suite
  page should find this software just as a user browsing EUVI should. The vocabulary carries no
  parent/child relationship that would make one imply the other.

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** Solar and Heliospheric Observatory
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SOHO

**Observatory 2:**
- **Observatory Name:** Solar-Terrestrial Relations Observatory
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO

Both are already stored, both are retained unchanged, and both resolve to `SMWG` rows carrying
`https://spase-metadata.org/` identifiers.

**A name collision that must be resolved by identifier, not by name.** Two rows in the vocabulary are
both named exactly `Solar and Heliospheric Observatory`: the SMWG row above and a second at
`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SOHO`. The record correctly holds the SMWG one.
A future agent matching this observatory by name alone would have a 50% chance of binding the wrong
row; match on the identifier.

**Why SOHO is retained despite the paper demonstrating only STEREO.** This is the one value in the
record where the repository is the stronger source and the paper is silent. `README.rst` states "It
can take SOHO or STEREO data and output a 3-dimensional map of the corona", and `solar.read_data()`'s
docstring opens "Read SOHO / STEREO data files and output a Data instance". Those are the authors'
explicit claims of designed-to-support, in the package's two most prominent descriptions of itself.
The paper's three
worked examples are STEREO-only, so no SOHO *instrument* can be resolved (see Field 31), but an
observatory-level association is exactly the right fallback when the software supports a platform and
the instrument cannot be pinned down. A user on the SOHO page finding a solar coronal tomography
package that documents itself as reading SOHO data is getting a useful, unsurprising result.

**Considered and not selected: `Solar Terrestrial Relations Observatory A`
(`https://spase-metadata.org/SMWG/Observatory/STEREO-A`) and `Solar Terrestrial Relations
Observatory B` (`https://spase-metadata.org/SMWG/Observatory/STEREO-B`).** Both rows do exist in the
vocabulary under the SMWG authority — the per-spacecraft entities are not confined to the CNES
archive namespaces — and the evidence for per-spacecraft support is strong: the shipped default
configuration names `STEREOA`, and the examples and the paper work with A and B separately. They are
nevertheless not recorded, because the per-spacecraft specificity is already carried by the four EUVI
and COR1 instrument rows in Field 31, which is where a user looking for spacecraft-specific tooling
lands. Two further observatory rows stacked on an already-listed umbrella mission would pad the
record without telling a reader anything the instrument rows do not already say. The two identifiers
are written out above so that this settled decision rests on named rows and needs no fresh research
if it is ever revisited. Note that the vocabulary is flat, so `Solar-Terrestrial Relations
Observatory` does not automatically surface this software on the STEREO-A or STEREO-B pages.

Also rejected: the CNES `CDPP-Archive` and `CDPP-AMDA` STEREO rows (`STEREO`, `STEREO-A`, `STEREO-B`,
`STEREO Ahead`, `STEREO Behind`, `Solar Terrestrial Relations Observatory; NASA`). They are archive-
catalogue variants of the same missions; `SMWG` is the canonical namespace and is the correct
tie-break among same-entity duplicates.

### 33. Logo (OPTIONAL)
Not found

A documented omission, verified mechanically rather than assumed: the pinned tree contains **no image
file of any kind**. Listing every tracked path and filtering for `.png`, `.jpg`, `.jpeg`, `.svg`,
`.gif`, `.ico` and `.webp` returns nothing across all 40 files. There is no logo in `README.rst`
(which has no images at all, only reStructuredText), none in the PyPI record, and none in the PyHC
registry entry, whose fields are name, url, description, code, contact, keywords and the six quality
ratings — it has no `logo` key for this package.

**One image does exist at a TomograPy-associated URL and must not be used.** The `gh-pages` branch
contains `_images/162ec381e97339c8b1a301a2b3dce01e35558316104cd0221caf0a54c5d161a5.png`. It is a
sample plot belonging to the Jupyter Book starter template described under Field 24, not a logo and
not related to this software. Recording it would put an unrelated tutorial figure on TomograPy's
catalogue page.

Never invent a logo; a blank here is the correct outcome for this package.
