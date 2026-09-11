# HSSI Metadata Extraction Results

**HSSI Software ID:** 84062431-340c-4ac1-bdc9-a79a431d9869
**Repository:** https://github.com/PyGSDR/PyGS
**Source Revision:** c12cc7a92352427a2cd6496d309e2417a7d87781
**Extraction Date:** 2026-09-10
**Validation Date:** 2026-09-11
**Validation Status:** PASS

---

## Scope note

Three facts about PyGS change how the evidence below should be read.

1. **The name collides with unrelated work.** The PyPI distribution named `PyGS` is not this
   software: as of 2026-09-10, `https://pypi.org/pypi/PyGS/json` gives `info.home_page`
   `https://github.com/steven-murray/PyGS`, author Steven Murray, and the summary "Interactive
   program to deal with Galaxy Surveys." An ADS title search for PyGS also returns an unrelated
   computer-vision preprint, "PyGS: Large-scale Scene Representation with Pyramidal 3D Gaussian
   Splatting" (Wang & Xu 2024, https://doi.org/10.48550/arXiv.2405.16829). This software is not
   published on PyPI at all — README:40 still says "Pip3 install will be available shortly." — so
   any PyPI-derived version, author, licence or download figure for `PyGS` describes the
   galaxy-survey package and must not be merged into this record.

2. **Git gives no per-person attribution.** Every commit reachable from the pin is authored by the
   project's organisation account: `git log --format='%an' <pin> | sort | uniq -c` gives 199 commits
   as `GS Detection & Reconstruction` and 3 as `GS Detection Reconstruction`. Authorship (Field 6)
   therefore rests on `setup.py`, `LICENSE` and the project's flux-rope database website, not on
   commit history.

3. **The pin is the upstream tip, and no package source has changed since 2024-02-19.** GitHub's
   `refs/heads/main` resolved to the pinned commit as of 2026-09-10. The last commit touching the
   package source under `PyGS/` is 7cdb438 (2024-02-19). Two commits follow it: 9b8372c, the same
   evening, which re-uploads the `PyGS-1.0.0.tar.gz` archive and touches nothing else; and c12cc7a
   (2026-02-27), which changes a single README line — the contact note that read "Please reach out
   to Dr. Yu Chen (yc0020@uah.edu) for any bugs." reads at the pin "Please reach out to Dr. Qiang Hu
   (qh0001@uah.edu) for any questions." (README:120). This bears on Fields 12 and 23.

Module paths below are relative to the repository root; `PyGS/` is the package directory.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)

- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Nothing in the repository or in any external record identifies who submitted this entry to HSSI,
and no identity is inferred.

### 2. Persistent Identifier (RECOMMENDED)

Not found — no value is recorded.

PyGS has no DOI of its own. The tracked paths at the pin include no `CITATION.cff`, no
`.zenodo.json` and no `codemeta.json`, and the README carries no DOI badge; the only DOIs anywhere
in the tree are the publication references at README:9, :17, :111 and :112 (Field 27).

**The one DOI connected to PyGS identifies a conference presentation, not the software, and is
deliberately kept out of this field.** https://doi.org/10.5281/zenodo.17371158 (concept DOI
10.5281/zenodo.17371156) is the Zenodo deposit titled "PyGS as an open-source tool for the
investigation of magnetic flux ropes in space plasmas" (Zenodo `metadata.title`): resource type
presentation, published 2025-10-16, licensed CC-BY-4.0, creators Rebecca Harvey (University of
Alabama in Huntsville) and Yu Chen (Center for Space Plasma and Aeronomic Research), given at Data,
Analysis, and Software in Heliophysics (DASH), 19–22 October 2025, San Antonio, Texas. Its
`related_identifiers` is null — it links to the repository only inside its description text.
DataCite's record for the DOI gives `resourceType` Presentation but renders it as bibtex `article`
and citeproc `article-journal`. Field 2 is what the entry page offers as the citation for the
software, so this DOI here would tell visitors to cite a conference talk, formatted as a journal
article, as if it were PyGS itself. It is recorded in Field 27 as a related publication instead.

Negative research, as of 2026-09-10:

- Zenodo `https://zenodo.org/api/records?q=title:PyGS` returns one record, the presentation above.
- A creator-keyed Zenodo search must use the prefixed field path.
  `metadata.creators.person_or_org.name:%22Chen,%20Yu%22%20AND%20PyGS` returns the same single
  presentation, while the unprefixed `creators.person_or_org.name:` form of the same query returns
  0 — a false zero, not an absence. `metadata.creators.person_or_org.name:%22Hu,%20Qiang%22`
  returns three deposits, none of them a PyGS deposit.
- ADS needs no personal token: `GET https://scixplorer.org/v1/accounts/bootstrap` yields an
  `access_token`, used as a Bearer token against
  `https://api.adsabs.harvard.edu/v1/search/query?q=title:%22PyGS%22&fl=bibcode,title,doi`. It
  returns four records: the unrelated Gaussian-splatting preprint (2024arXiv240516829W); a NASA
  proposal record by Yu Chen, NASA Proposal ID 22-HTM22-0007 (2022htm..prop....7C, no DOI); an AGU
  Fall Meeting 2023 abstract by Chen and Hu (2023AGUFMSH33E3095C, no DOI); and the DASH 2025
  presentation (2025dash.confE..16H, carrying the Zenodo DOI above). A nonsense-title control
  returns 0.

None of these is a software deposit. If the project ever deposits the software itself — for
example through Zenodo's GitHub release integration — that deposit's DOI belongs here, and the
presentation stays in Field 27.

### 3. Code Repository (MANDATORY)

https://github.com/PyGSDR/PyGS

`setup.py:9` declares this URL; the PyHC registry entry (`_data/projects.yml:480` in
`heliophysicsPy/heliophysicsPy.github.io`, as of 2026-09-10) gives the same URL in its `code:`
field; and the flux-rope database site (Field 28) links to it. GitHub's repository record: default
branch `main`, not a fork, not archived, `created_at` 2023-05-12T18:47:39Z.

As of 2026-09-10 the remote also carries two other branches, `develop` (tip 84c097d, 2023-07-21)
and `PyGSDR-patch-1` (tip c4dbf15). Both tips are ancestors of `main` — nothing on either branch is
missing from `main` — so they are stale and the evidence throughout this record is from `main`.

### 4. Software Functionality (RECOMMENDED)

- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Field-line Tracing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Hodograms
- Data Visualization: Line Plots
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Forward-Fitting
- Models and Simulations: Physics-Based

**Every subcategory is written fully qualified as `Parent: Child`, and that is load-bearing here.**
Three of the child names used — Analysis, Field-line Tracing and Processing — also exist under
other parents in the vocabulary, so a bare child name could bind to the wrong row. Every
subcategory's parent is listed.

What PyGS does, for orientation: from one spacecraft's time series of magnetic field and plasma
parameters, the detection product (GSD) scans sliding windows for flux-rope signatures and writes
event lists; the reconstruction product (GSR) solves the Grad–Shafranov equation for a chosen event
to recover its two-dimensional cross-section and derive flux-rope parameters.

**Evidence for each value**, file:line at the pin:

- **Coordinate Transforms; Coordinate Transforms: Heliospheric.** Data arrive in the frame each
  mission publishes — the comments at `PyGS/ReconstructionMisc.py:454` and `:458` record that ACE
  and Wind data are in GSE and Ulysses, PSP and Solar Orbiter data in RTN — and PyGS transforms
  them into the flux rope's own frames: the de Hoffmann–Teller frame (`PyGS/FluxRopeDetection.py:1232`),
  the minimum-variance frame through the public `MVAB()` (`PyGS/ReconstructionMisc.py:169`), and
  each trial-axis frame, into which field, HT velocity and flow are rotated
  (`PyGS/FluxRopeDetection.py:1526-1533`). README:106-108 states that the HT and MVAB calculations
  can be run independently of GSR, so the transforms are offered to users, not only used
  internally.
- **Data Processing and Analysis: Analysis.** Derived physical quantities: toroidal and poloidal
  magnetic flux and axial current (`PyGS/ReconstructionMisc.py:1863`) and relative helicity
  (`:1869`); README:20 lists these among GSR's outputs.
- **Data Processing and Analysis: Data Access and Retrieval.** `PyGS/FluxRopeDetection.py` makes 18
  calls of the form `cdas.get_data('istp_public', ...)`, one per dataset, to download the chosen
  interval from CDAWeb (Fields 17 and 31).
- **Data Processing and Analysis: Data Reduction.** Resampling to a uniform cadence with averaging
  and time interpolation (`PyGS/FluxRopeDetection.py:558-563`), and downsampling of the flux
  function before smoothing (`:1593`).
- **Data Processing and Analysis: Field-line Tracing.** The flux function A along the spacecraft
  path is integrated from By (`PyGS/FluxRopeDetection.py:1550`); the reconstructed transverse field
  components are derived from A (`PyGS/ReconstructionMisc.py:1003-1004`); and contours of A — the
  transverse field lines — are drawn over the cross-section (`:1345`, `:1347`). The GSR
  instructions (`documentation/instruction_gsr_examples.md:256`) read the closed transverse
  field-line regions in that figure as confirmation of the flux-rope configuration. That sentence is
  paraphrased rather than quoted because the file spells field, flux and configuration with the
  typographic ligature characters U+FB01 and U+FB02, which an ordinary-text quotation would not
  reproduce.
- **Data Processing and Analysis: Processing.** GSD is a staged pipeline, steered by the `Search`,
  `CombineRawResult` and `GetMoreInfo` switches (README:69), that writes the preprocessed data
  (`PyGS/FluxRopeDetection.py:1211-1215`), the raw search results (`:1964`), the event list with
  overlapping intervals resolved (`:2805`) and the detailed event information (`:3341`).
- **Data Processing and Analysis: Time Series Analysis.** Savitzky–Golay filtering
  (`PyGS/FluxRopeDetection.py:43`) and low-pass and differenced series built from the measured time
  series (`:407`, `:431`).
- **Data Visualization: 2D Graphics.** The filled-contour Bz map of the reconstructed cross-section
  (`PyGS/ReconstructionMisc.py:1326`), the Jz map (`:1439`) and the axis-search residue map
  (`PyGS/obtainAxis.py:405`).
- **Data Visualization: Hodograms.** `MVAB()` provides hodograms (docstring at
  `PyGS/ReconstructionMisc.py:171`; plotting at `:204` and `:222`), documented in
  `documentation/instruction_mvab.md:23` and `:33`.
- **Data Visualization: Line Plots.** The GSD time-series plot marking flux-rope intervals
  (`plot_time_series_data`, saved at `PyGS/FluxRopeDetection.py:3713`), the plot of parameters
  along the spacecraft path (`PyGS/ReconstructionMisc.py:87`) and the Pt′–A′ curve
  (`plotPressureA`, `PyGS/ReconstructionMisc.py:94`).
- **Models and Simulations: Data Guided.** The Grad–Shafranov solution is seeded with the values
  measured along the spacecraft path — `PyGS/ReconstructionMisc.py:855` sets the middle row of the A
  grid to A along the path — and marched away from it in both directions (`:908`, `:973`).
- **Models and Simulations: Forward-Fitting.** The flux-rope axis is found by minimising a fitting
  residue over a grid of trial directions (`PyGS/FluxRopeDetection.py:1421-1422`; θ/φ grid at
  `:1460-1463`), and Pt′(A′) is fitted with a polynomial (`np.polyfit` in `fitPtA`,
  `PyGS/ReconstructionMisc.py:764`) whose derivative drives the marching (`:877`).
- **Models and Simulations: Physics-Based.** The whole method solves the extended, generalized
  Grad–Shafranov equation (README:2; README:9 cites Teh 2018 for the generalized form).

**Rejected, with reasons, so they are not re-proposed:**

- Data Processing and Analysis: 2D Slices — this was the previous extraction's value. The row means
  extracting two-dimensional slices from three-dimensional data volumes; PyGS ingests
  one-dimensional spacecraft time series and reconstructs a transverse plane from them, and never
  samples a volume. Data Visualization: 2D Slices is rejected for the same reason.
- Models and Simulations: Field-line Tracing — the same single capability, recorded once under the
  data-derived Data Processing and Analysis row.
- Models and Simulations: MHD — PyGS is not an MHD simulation code. Models and Simulations: First
  Principles — the Grad–Shafranov equation is a reduced equilibrium equation fitted to data;
  Physics-Based is the row that describes that.
- Coordinate Transforms: Magnetospheric — GSE appears only as the frame in which Wind and ACE data
  are published; PyGS performs no magnetospheric transform. Coordinate Transforms: Mission-Specific
  — no attitude, pointing or SPICE handling.
- Data Processing and Analysis: Plasma Moments — PyGS consumes density, velocity and temperature
  moments; it never computes them from distributions.
- Data Processing and Analysis: File Format Conversion — its file outputs are incidental products
  of analysis, not a conversion capability (Field 19).
- Mission-related — general analysis software that reads mission data, not part of any mission's
  ground system.
- Servers and Environments: High Performance Computing — the only parallelism is a
  `multiprocessing` pool on one machine (`PyGS/FluxRopeDetection.py:1807-1811`).

Before this refresh HSSI held no functionality values for this entry.

### 5. Related Region (RECOMMENDED)

- Interplanetary Space
- Solar Environment
- Solar Wind

**Solar Wind** — small-scale magnetic flux ropes in the solar wind are the software's subject.
README:5 frames PyGS as tools for flux ropes in space plasmas from in-situ spacecraft measurements,
every dataset it retrieves is in-situ solar-wind field or plasma data (Field 31), and the detection
papers the README asks users to cite are solar-wind studies (Field 27). **Interplanetary Space** —
where all five supported spacecraft make those measurements. **Solar Environment** — kept for the
Parker Solar Probe near-Sun encounters, which the project's database lists as separate encounter
event lists (Field 28); it was considered for removal and kept.

Rejected: Corona (PyGS analyses in-situ solar-wind data and does no coronal imaging or modelling);
Heliosheath (none of its data come from there); and every Earth region (GSE enters only as a data
publication frame, Field 4). The region vocabulary is flat, so no value implies another and each is
listed explicitly. Order: the two values held before this refresh keep their positions and Solar
Wind follows them.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Yu Chen
- **Author Identifier:** https://orcid.org/0000-0002-0065-7622
- **Affiliation:**
  - **Organization:** University of Alabama in Huntsville
  - **Affiliation Identifier:** https://ror.org/02zsxwr40

**Author 2:**
- **Name:** Qiang Hu
- **Author Identifier:** https://orcid.org/0000-0002-7570-2301
- **Affiliation:**
  - **Organization:** University of Alabama in Huntsville
  - **Affiliation Identifier:** https://ror.org/02zsxwr40

**Author 3:**
- **Name:** Jinlei Zheng
- **Author Identifier:** Not found
- **Affiliation:** Not found

*The author set and order.* Three primary sources name the same three people. `setup.py:6` gives
`author="Yu Chen, Qiang Hu, and Jinlei Zheng"`; `LICENSE:2` (the file opens with a blank line)
names the same copyright holders in the same order; and the author line of the flux-rope database
site (http://www.fluxrope.info/, fetched 2026-09-10) names Dr. Jinlei Zheng, Dr. Qiang Hu and
Dr. Yu Chen. The record keeps the `setup.py`/`LICENSE` order, which is also the order held before
this refresh. There is no `CITATION.cff`. The PyHC registry's `contact:` field names Yu Chen and
Qiang Hu as contacts, which is consistent with, not a substitute for, the author list.

Rebecca Harvey (https://orcid.org/0009-0002-9139-596X), first creator of the DASH 2025
presentation (Field 27), was considered and is not listed: she appears in no software-metadata
source — not `setup.py`, `LICENSE`, the README or the database site's author line.

*Identifiers for Chen and Hu.* ORCID fielded searches on 2026-09-10 against
`https://pub.orcid.org/v3.0/expanded-search/` (Accept: application/json):
`given-names:Yu+AND+family-name:Chen+AND+affiliation-org-name:%22University+of+Alabama+in+Huntsville%22`
returns exactly one record, 0000-0002-0065-7622, and the same query for Qiang Hu returns exactly
one, 0000-0002-7570-2301. Controls: the bare `given-names:Yu+AND+family-name:Chen` returns results
in the thousands (3446 on that date), so a name-only match is unusable, and a nonsense name returns
0. Corroboration: the DASH presentation's Zenodo record carries the same ORCID for Yu Chen, and
Hu's ORCID `/employments` lists one employment, University of Alabama in Huntsville, Department of
Space Science. Before this refresh HSSI's person rows for this entry carried no identifier.
Because an identifier cannot be attached to an existing identifier-less person through the update
API without creating a duplicate person, the two identifiers were recorded on the existing person
rows on the database side.

*No identifier for Jinlei Zheng.* `given-names:Jinlei+AND+family-name:Zheng` returns five ORCID
records (0000-0002-9494-8921, 0009-0000-4591-6926, 0009-0009-1716-6166, 0009-0008-3053-9804,
0000-0002-8292-6768; as of 2026-09-10). None lists any employment. Of the two with works,
0000-0002-8292-6768 holds structural and tunnel-engineering papers and 0009-0000-4591-6926 a paper
on object tracking in satellite video; the other three have no works. None is the heliophysicist,
so no identifier is recorded rather than a guess.

*Affiliations.* Chen and Hu are recorded at University of Alabama in Huntsville,
https://ror.org/02zsxwr40, using ROR's display name verbatim. Evidence: `setup.py:7` gives uah.edu
addresses for both; README:120 gives Hu's uah.edu address; Hu's ORCID employment is UAH's
Department of Space Science; USAspending names The University of Alabama in Huntsville as the
recipient of the award that funds PyGS (Field 26); and the DASH deposit gives Chen's affiliation
as the Center for Space Plasma and Aeronomic Research, UAH's space-plasma research center. Zheng
has no affiliation: his only address in project materials is `jz0006@alumni.uah.edu` on the
database site — an alumni address, which says where he studied, not where he works. Near-miss to
avoid: ROR https://ror.org/03xrrjk67, University of Alabama, is the Tuscaloosa campus, a different
institution. Before this refresh HSSI held no affiliation for any author.

### 7. Software Name (MANDATORY)

PyGS

`setup.py:4`, the README heading (README:1), the repository name and the PyHC registry entry all
give `PyGS`; the logo spells it out as Python for GS (Field 33). The name is shared with unrelated
software (Scope note, item 1), which is why the record leans on repository-internal evidence.

### 8. Description (MANDATORY)

This package consists of two key products to serve as a set of comprehensive tools for the investigation of magnetic flux ropes (FRs) in space plasmas based on in-situ spacecraft measurements. The Grad-Shafranov (GS)-based detection (GSD) automatedly identifies flux ropes and outputs their parameters to support statistical analysis, relying on the generalized version of the GS equation. It is applicable to FRs with a broad definition including both static and dynamic structures, and works with PSP, Solar Orbiter, Ulysses, ACE, and WIND spacecraft datasets. The Grad-Shafranov (GS) type reconstruction (GSR) visualizes and characterizes the 2D magnetic field configuration from 1D time-series data, confirms the flux rope detection results, and derives flux rope parameters such as the poloidal and toroidal magnetic fluxes, the relative helicity, and average twist.

This prose compiles the README's Introduction (README:5-22) — the two products and their bullet
points — into sentences, keeping the project's own wording, including its "automatedly". It is
kept as held, because it is accurate and it is the project's own framing.

### 9. Concise Description (OPTIONAL)

Magnetic flux rope detection and reconstruction based on the extended Grad-Shafranov equation for in-situ spacecraft measurements.

This expands the repository tagline — README:2, which writes the ampersand as the HTML entity
`&amp;`, and the GitHub repository description — spelling out the ampersand and adding "for
in-situ spacecraft measurements".

### 10. Publication Date (RECOMMENDED)

2023-05-12

The first commit, 09abb79 (`Initial commit`, 2023-05-12 14:47:40 -0400), and GitHub's
`created_at` for the repository, 2023-05-12T18:47:39Z, are the same moment. The 1.0.0 archive date
(2024-02-19) is the version date in Field 12, not the first public release of the code, and there
is no DOI publication date to prefer (Field 2).

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

With no DOI registrant (Field 2) and no package-index release (Scope note, item 1), the code is
published only through its GitHub repository.

### 12. Version (RECOMMENDED)

- **Version Number:** v1.0.0
- **Version Date:** 2024-02-19
- **Version Description:** Not found
- **Version PID:** Not found

**Number.** `setup.py:5` declares `version="1.0.0"`, and the `PKG-INFO` inside the tracked
`PyGS-1.0.0.tar.gz` gives `Version: 1.0.0`; the README's installation instructions unpack that
archive (README:34-36). The stored `v` prefix appears in no project source. It is deliberately
left as is: the number is correct, and changing Field 12 replaces the whole version record for a
purely cosmetic difference.

**Date.** The 1.0.0 archive was added in b3133c5 on 2024-02-19, the same day the earlier 0.0.1
archive was moved into `archive/` (1190d7d adds `archive/PyGS-0.0.1.tar.gz`; c4dbf15 deletes the
root copy). 9b8372c re-uploaded the 1.0.0 archive later that evening. There are no git tags and no
GitHub releases (both empty as of 2026-09-10), and the software is not on PyPI (README:40:
"Pip3 install will be available shortly."), so the archive commit is the only dated release event.

**Description and PID.** There is no changelog, release note or tag message to source a
description from, and no version DOI exists (Field 2).

Caveat for later refreshes: the 1.0.0 archive is not a byte-for-byte snapshot of the package at the
pin. Its `PyGS/FluxRopeDetection.py`, `PyGS/obtainAxis.py` and `PyGS/__init__.py` match the tracked
modules, but its `PyGS/ReconstructionMisc.py` does not. The version number is unaffected; the
difference only means the archive and the tree should not be treated as interchangeable evidence
for that module.

### 13. Programming Language (RECOMMENDED)

- Python 3.x

The form asks for the most important languages and says "This is not meant to be an exhaustive
list." (`resource_submission_form_fields.md:310`). Here there is only one: all ten `.py` files
among the 49 tracked paths are the source (the four package modules under `PyGS/`, `setup.py` and
five tests under `test/`); everything else is Markdown, PNG figures, pickled and `.dat` example
data, the two source archives and the licence. `setup.py:13` carries the
`Programming Language :: Python :: 3` classifier and `setup.py:25` sets `python_requires='>=3'`.

Python 2.x is rejected. `from __future__ import division` appears in each of the three substantive
package modules (`PyGS/FluxRopeDetection.py:33`, `PyGS/ReconstructionMisc.py:18`,
`PyGS/obtainAxis.py:19`; `PyGS/__init__.py` is empty), but that is a Python 2 compatibility idiom
with no effect under Python 3, not a Python 2 target — the package declares Python 3 only.

### 14. Reference Publication (OPTIONAL)

Not found — no value is recorded.

The README deliberately gives a separate citation list for each product rather than one reference
for the package: README:111 for GSD (Zheng & Hu 2018; Hu et al. 2018; Chen & Hu 2022) and README:112
for GSR (Sonnerup & Guo 1996; Hau & Sonnerup 1999; Hu & Sonnerup 2002; Chen & Hu 2022). No
journal paper describes PyGS as software. The works about PyGS itself are conference items, both
recorded in Field 27: the DASH 2025 presentation and a 2023 AGU Fall Meeting abstract by Chen and
Hu (ADS 2023AGUFMSH33E3095C, no DOI).

Considered and not selected:

- Chen & Hu 2022, "Small-scale Magnetic Flux Ropes and Their Properties Based on In Situ
  Measurements from the Parker Solar Probe" (Crossref `title`), The Astrophysical Journal 924, 43,
  https://doi.org/10.3847/1538-4357/ac3487 — the only paper in both lists, by the two lead authors.
  Not promoted, because naming a single paper as the reference would override the project's
  per-product citation guidance: a GSR user who cited only this paper would omit the three method
  papers the project asks GSR users to cite.
- Hu & Sonnerup 2002 (https://doi.org/10.1029/2001JA000293), cited at README:17 as the source of the
  GSR method — it covers only one of the two products, and it is the 2002 method paper, not a
  description of PyGS.

All seven cited papers are recorded in Field 27. If a paper describing PyGS as software is
published, it belongs here.

### 15. License (RECOMMENDED)

- **License:** BSD 3-Clause "New" or "Revised" License

`LICENSE` (no file extension) is the three-clause BSD text: its numbered conditions are the
source-redistribution clause (`LICENSE:6`), the binary-redistribution clause (`LICENSE:8`) and the
no-endorsement clause (`LICENSE:10`) that distinguishes the three-clause from the two-clause
licence. GitHub's licence detection gives key `bsd-3-clause` (SPDX `BSD-3-Clause`). `setup.py:14`
carries only the generic `License :: OSI Approved :: BSD License` classifier, which does not
distinguish clause counts; the licence text decides. Field 15 selects one of HSSI's shared licence
records, and the licence URL travels with that shared record — there is no per-software licence
URI to set.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

2d graphics, ace, cdaweb, csv, data analysis, flux rope detection, flux rope reconstruction,
grad shafranov, heliosphere, in situ measurements, interactive, magnetic flux ropes, psp,
solar orbiter, solo, spacecraft measurements, space plasmas, ulysses, wind

These are the nineteen keywords held before this refresh, unchanged, in their stored lowercase
spellings (the entry page displays them title-cased). Eleven derive from the PyHC registry's
`keywords` for PyGS (`_data/projects.yml:482` in `heliophysicsPy/heliophysicsPy.github.io`, as of
2026-09-10: heliosphere, 2D_graphics, interactive, csv, cdaweb, data_analysis, ace, psp, ulysses,
wind, solo, normalised to spaced lowercase), and eight describe the README's subject matter.

**`interactive` is accurate and must not be removed as an inherited registry tag.** The
reconstruction workflow is click-driven: `plt.ginput` collects the user's choice of interval
boundaries in the GSD time-series plot (`PyGS/FluxRopeDetection.py:3680-3681`), of the boundary
value Ab (`PyGS/ReconstructionMisc.py:151-152`) and of trial axis directions on the residue map
(`PyGS/obtainAxis.py:512`, with a typed `input()` at `:568`). The instructions tell users to click:
"On the residue map, click on an alternative point." (`documentation/instruction_gsr_examples.md:156`;
also `:207`).

Considered and not added: `parker solar probe` — the missions are named in full in Field 32 and in
the description; `solar wind` — carried by Fields 5 and 22.

### 17. Data Sources (OPTIONAL)

- CDAWeb

All eighteen datasets PyGS uses are downloaded with `cdas.get_data('istp_public', ...)` in
`PyGS/FluxRopeDetection.py`, through the `ai.cdas` client for CDAWeb's web services
(`from ai import cdas`, `PyGS/FluxRopeDetection.py:39`; Field 29).

SSCWeb was considered: one of the eighteen, `AC_OR_SSC`, is an SSCWeb position product (CDAWeb's
label for it names SSC/SSCWeb), but PyGS retrieves it from CDAWeb like the rest, so SSCWeb is not a
service PyGS contacts. `Observatory/Mission-specific` is not selected, because every dataset comes
through the multi-mission CDAWeb archive.

### 18. Input File Formats (RECOMMENDED)

- CDF

Every CDAWeb request asks for CDF files (`cdf=True` in all eighteen `cdas.get_data` calls), which
are read with `spacepy.pycdf` (`PyGS/FluxRopeDetection.py:40`); README:25 lists NASA's CDF Library
among the dependencies.

`Other` was considered for the pickle files PyGS reads — the GSR example loads `detailed_info.p`
(README:89-91), and GSD reads the shipped shock list and its own intermediate results with
`pd.read_pickle` — and not added: they are PyGS's own products or files it ships in `examples/`,
not a format a user brings to it.

### 19. Output File Formats (RECOMMENDED)

- csv
- Other

**csv** — `to_csv` writes the preprocessed data (`PyGS/FluxRopeDetection.py:1212`, `:1215`) and
the detailed event list (`:3975`), and the GSD instructions say the final results "will be a
time-series plot and a csv file including flux rope parameters." (`documentation/instruction_gsd.md:23`).

**Other** — PyGS's figures are PNG files (`savefig(..., format='png')` in all three substantive
modules) and its intermediate and final result tables are pickle files (`to_pickle` and
`pickle.dump` in `PyGS/FluxRopeDetection.py`, e.g. `:1211`, `:1964`, `:2805`, `:3341`); the
vocabulary has no PNG or pickle entry, so `Other` is the only faithful value. The previous
extraction listed only csv; `Other` is correct and is kept.

`ascii` was considered for the small plain-text files the reconstruction writes with `np.savetxt`
— `Ab.dat` and `bz2fit.dat` (`PyGS/ReconstructionMisc.py:159`, `:803-806`), `saved_boundary.txt`
(`:1507`) and `zs_select.txt` (`PyGS/obtainAxis.py:587`) — and not listed: each is read straight
back with `np.loadtxt` (`PyGS/ReconstructionMisc.py:162`, `:1015`, `:1510`, `:1797`) to carry a
choice or fit between runs. They are internal state, like the pickle inputs in Field 18, not an
output format offered to users.

### 20. Operating System (RECOMMENDED)

- Operating System Independent

`setup.py:15` carries the `Operating System :: OS Independent` classifier, and the package is pure
Python with no platform-specific code paths.

### 21. CPU Architecture (RECOMMENDED)

- CPU Independent

The tracked tree has no C, C++, Cython or Fortran source and builds no extension module; the
package is pure Python, and its compiled dependencies ship their own builds.

### 22. Related Phenomena (OPTIONAL)

- Coronal Mass Ejections
- Solar Wind

**Solar Wind** — the flux ropes PyGS detects are found in solar-wind data (Field 5). **Coronal Mass
Ejections** — the reconstruction half applies to magnetic clouds, the interplanetary counterparts of
CMEs: the GSR citation in the README, Hu & Sonnerup 2002, is titled "Reconstruction of magnetic
clouds in the solar wind: Orientations and configurations" (Crossref `title`). The previous
extraction listed only Coronal Mass Ejections; both values were already held before this refresh.

Rejected: Solar Flares, Coronal Heating, Solar Corona and X-ray emission (PyGS analyses only
in-situ interplanetary data), and Geomagnetic Storms (PyGS computes no storm, index or
magnetospheric response).

### 23. Development Status (RECOMMENDED)

- Inactive

The vocabulary's definitions (RepoStatus `definition`) decide this:

- Inactive: "The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows."
- Active: "The project has reached a stable, usable state and is being actively developed."
- Unsupported: "The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired."

**Evidence.** A stable, usable 1.0.0 archive shipped on 2024-02-19 (Field 12). No commit has
touched the package source since 7cdb438 on 2024-02-19; the only later commits are the same-evening
archive re-upload and c12cc7a (2026-02-27), which changes the README's contact line (Scope note,
item 3). The repository is not archived. As of 2026-09-10 it has four open issues, all opened on
2025-06-11, and one open pull request opened on 2026-04-08, none of them answered by a commit.

**Active is rejected** — the project is not being actively developed. **Unsupported is rejected** —
its definition requires authors who have ceased all work, and the 2026 contact update, which
redirects questions to Qiang Hu, shows the project is still tended. Inactive — stable, not
developed, maintained as time allows — is the exact fit.

Not evidence: `setup.py:12`'s `Development Status :: 5 - Stable` is not a valid trove classifier
(the real one is `Development Status :: 5 - Production/Stable`) and in any case asserts maturity,
not activity; the PyHC registry's `software_maturity` rating of Partially met, which the previous
extraction read as Active, is likewise a maturity rating. GitHub's `updated_at` timestamp moves
with non-commit events and is not commit activity. Before this refresh HSSI held no development
status for this entry.

### 24. Documentation (RECOMMENDED)

https://github.com/PyGSDR/PyGS/tree/main/documentation

The folder holds the four instruction files — `instruction_gsd.md`, `instruction_gsr_examples.md`,
`instruction_HT_analysis.md` and `instruction_mvab.md` — and the README links each of them
(README:52, :74, :107, :108); the PyHC registry's `docs:` field gives the same URL. There is no
hosted documentation site. The repository has no wiki: `git ls-remote
https://github.com/PyGSDR/PyGS.wiki.git` reports that the repository is not found (2026-09-10).
GitHub's `has_wiki` flag is not evidence either way, because a wiki is a separate git repository.

### 25. Funder (OPTIONAL)

- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

README:117 states that the authors "acknowledge the NASA grant 80NSSC23K0256 for funding", and
USAspending lists the National Aeronautics and Space Administration as the awarding agency of that
award (Field 26). The acronym is expanded to ROR's display name for https://ror.org/027ka1x80.

The flux-rope database site (Field 28) acknowledges a longer list of earlier NASA grants, NASA
subawards, an NSF grant and other support. Those are stated as supporting the database and the
earlier research, not this software, and are not recorded here.

### 26. Award Title (OPTIONAL)

- **Award Title:** PyGS: Analysis Tools for Small-Scale Magnetic Flux Ropes Based on the Grad-Shafranov Reconstruction Method (80NSSC23K0256)
- **Award Number:** 80NSSC23K0256

**Source.** USAspending's award search (`POST https://api.usaspending.gov/api/v2/search/spending_by_award/`
with filters `award_type_codes` 02–05 and `award_ids` 80NSSC23K0256; 2026-09-10) returns one award:
Description "E014042 - PYGS: ANALYSIS TOOLS FOR SMALL-SCALE MAGNETIC FLUX ROPES BASED ON THE
GRAD-SHAFRANOV RECONSTRUCTION METHOD", Recipient Name THE UNIVERSITY OF ALABAMA IN HUNTSVILLE,
Awarding Agency National Aeronautics and Space Administration, Start Date 2023-01-01. The award's
own title names PyGS, so this is unambiguously the software's funding. ADS independently holds the
proposal under the same title in ordinary case — "PyGS: Analysis tools for small-scale magnetic
flux ropes based on the Grad-Shafranov reconstruction method" (ADS `title`, 2022htm..prop....7C,
NASA Proposal ID 22-HTM22-0007, Yu Chen, University of Alabama in Huntsville).

**Form of the stored title.** The title drops the internal `E014042 - ` prefix, restores title case
from USAspending's all-capitals rendering, and appends the award number in parentheses because the
entry page displays only the award name, so without it a visitor would not see the grant number.
The result is 122 characters, within the award-name limit of 128.

Before this refresh the stored award name was the synthesised "NASA Grant 80NSSC23K0256", which
carried the number but not the award's real title. An award's name cannot be changed through the
update API, so the title was corrected on the database side.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- https://doi.org/10.1029/2001JA000293 — Hu & Sonnerup 2002, Journal of Geophysical Research:
  Space Physics 107 (README:17, :112)
- https://doi.org/10.1186/s40623-018-0802-z — Teh 2018, Earth, Planets and Space 70, 34 (README:9)
- https://doi.org/10.1029/1999JA900002 — Hau & Sonnerup 1999, Journal of Geophysical Research:
  Space Physics 104, 6899–6917 (README:112)
- https://doi.org/10.1029/96GL03573 — Sonnerup & Guo 1996, Geophysical Research Letters 23,
  3679–3682 (README:112)
- https://doi.org/10.3847/1538-4357/ac3487 — Chen & Hu 2022, The Astrophysical Journal 924, 43
  (README:111, :112)
- https://doi.org/10.3847/1538-4365/aae57d — Hu, Zheng, Chen, le Roux & Zhao 2018, The
  Astrophysical Journal Supplement Series 239, 12 (README:111)
- https://doi.org/10.3847/2041-8213/aaa3d7 — Zheng & Hu 2018, The Astrophysical Journal Letters
  852, L23 (README:111)
- https://doi.org/10.5281/zenodo.17371158 — Harvey & Chen 2025, presentation at Data, Analysis,
  and Software in Heliophysics (DASH) 2025 (Zenodo; DataCite)
- https://doi.org/10.1029/2025JA033897 — Harvey, Hu & Chen 2025, Journal of Geophysical Research:
  Space Physics 130, e2025JA033897
- https://doi.org/10.1029/2024JA033130 — Chen & Hu 2025, Journal of Geophysical Research: Space
  Physics 130, e2024JA033130
- https://doi.org/10.1029/2023JA032088 — Wang, Zou, Hu, Shi & Hasegawa 2024, Journal of Geophysical
  Research: Space Physics 129, e2023JA032088
- https://doi.org/10.1051/0004-6361/202556098 — Ding et al. 2025, Astronomy & Astrophysics 701, A123
- https://ui.adsabs.harvard.edu/abs/2023AGUFMSH33E3095C/abstract — Chen & Hu 2023, AGU Fall Meeting
  2023, abstract SH33E-3095

Authors, years and venues are from each DOI's Crossref record (DataCite and Zenodo for the DASH
presentation). The 2023 AGU abstract has no DOI; its authors, year, meeting and abstract number
are from its ADS record.

The first seven are exactly the publication references in the pinned tree. A binary-aware sweep
of all 49 tracked paths — including the files inside both source archives — for DOIs and publisher
links (doi.org, agupubs, springeropen, iopscience, arXiv, ADS, Zenodo) finds only the README's
references at README:9, :17, :111 and :112 (and identical copies in the archived READMEs), plus the
flux-rope database links. Teh 2018 is cited at README:9 for the generalized Grad–Shafranov
equation; the other six are the README's per-product citation lists (Field 14). Hu & Sonnerup 2002
is linked in the README through the publisher URL
https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2001JA000293 and is recorded in its
doi.org form.

The DASH 2025 presentation is about PyGS itself and is recorded here rather than in Field 2 (see
Field 2 for why its DOI is not the software's identifier).

The 2023 AGU Fall Meeting abstract by Chen and Hu is likewise the authors' own conference
description of PyGS, given under the software's own title: "PyGS: Analysis tools for small-scale
magnetic flux ropes based on the Grad-Shafranov reconstruction method" (ADS `title`,
2023AGUFMSH33E3095C). It has no DOI, so it is recorded by its ADS abstract page, which the field
definition allows for a publication without one.

The four journal articles are recorded because each uses PyGS to produce its own results:

- Harvey, Hu & Chen 2025 — the published article's Data Availability Statement names "The PyGS
  software" as the tool that "was used to identify the SFR structures".
- Chen & Hu 2025 — the Open Research section of the accepted manuscript on NSF PAR
  (https://par.nsf.gov/servlets/purl/10632421) states that its GS-based detection and GS-type
  reconstruction results were obtained "using the PyGS package".
- Wang, Zou, Hu, Shi & Hasegawa 2024 — the arXiv preprint (arXiv:2309.09995) reports "The GS
  reconstruction is carried out" in its event analysis, and its Data Availability Statement
  credits "A Python package, pyGS, developed by Dr. Yu Chen for performing the GS reconstruction".
- Ding et al. 2025 — the arXiv preprint (arXiv:2507.16990) says "we employed the automated
  detection algorithm implemented in the PyGS package" to identify small-scale flux ropes in the
  solar wind.

The Harvey et al. 2025 quote is from the published article. The Wang et al. 2024 and Ding et al.
2025 quotes are from their arXiv preprints, and the Chen & Hu 2025 quote is from the accepted
manuscript on NSF PAR, rather than from the typeset articles.

These four articles were found by an ADS full-text search for the repository name `PyGSDR` as of
2026-09-10. They are not an exhaustive list of work that uses PyGS: a paper that uses the package
without naming its repository would not appear in that search. A later refresh should repeat it.

The NASA proposal record 2022htm..prop....7C (NASA Proposal ID 22-HTM22-0007) is not a
publication, so it is not listed here. It serves only as corroboration of the Field 26 award
title.

### 28. Related Datasets (OPTIONAL)

- http://www.fluxrope.info

The Small-scale Magnetic Flux Rope Database, maintained by the same group, is the published output
of the detection method: browsable event lists for Wind (1996–2016), ACE (1998–2018), Ulysses
(1991–2009) and Parker Solar Probe (encounters 1–3 and the years 2018–2024), plus an identified
flare–CME–ICME event list. The site describes itself as "This is a small-scale magnetic flux rope
database." (http://www.fluxrope.info/, fetched 2026-09-10), links back to the PyGS repository and
to the PyHC project list, and credits Zheng, Hu and Chen as its authors. README:5 sends readers
there for details, and README:113 points to it for event lists.

Caveat, so the relation is not over-read: README:113 attributes the posted events to the original
GSD, while the site's PSP section says "Results here are detected via the GS-type equation." — the
extended method PyGS implements. The site is therefore related output of this method family rather
than a product of this exact release. The README links the `http` form; as of 2026-09-10 an
`https` connection to the site fails certificate verification, so the `http` URL is the working
one. Before this refresh HSSI held no related dataset for this entry.

### 29. Related Software (OPTIONAL)

- https://github.com/AlexJinlei/Magnetic_Flux_Rope_Detection
- https://github.com/spacepy/spacepy
- https://bitbucket.org/isavnin/ai.cdas

**Magnetic_Flux_Rope_Detection** — the predecessor. PyGS's GSD is "Enhanced and streamlined from
the original automated GSD" (README:12), which is Jinlei Zheng's code at this URL (README:12,
:114).

**SpacePy** — a domain-specific dependency: PyGS reads every downloaded CDF with `spacepy.pycdf`
(`PyGS/FluxRopeDetection.py:40`), `setup.py:21` declares `spacepy`, and README:25 lists it. The
URL is the repository URL that SpacePy's own HSSI entry stores, following the convention of linking
an in-catalogue relation by that entry's repository URL, which reads legibly as link text. If the
site ever renders resolved titles for related software, SpacePy's concept DOI
https://doi.org/10.5281/zenodo.3252523 would be preferable for persistence.

**ai.cdas** — a domain-specific dependency and PyGS's only data-access route: `from ai import cdas`
(`PyGS/FluxRopeDetection.py:39`), `setup.py:23`, README:25. PyPI's record for `ai.cdas` (as of
2026-09-10) gives author Alexey Isavnin, home page https://bitbucket.org/isavnin/ai.cdas, and the
summary "Python interface to CDAS data via REST API".

**Rejected, with reasons.** The form's test for unnamed packages is to ask "would this package be
equally at home in a web app, a finance model, or a biology pipeline?"
(`resource_submission_form_fields.md:692`).

- numpy, scipy, pandas, matplotlib — the generic scientific-Python stack.
- sympy (`PyGS/ReconstructionMisc.py:23`) and Pillow (`from PIL import Image`,
  `PyGS/FluxRopeDetection.py:61`) — generic by that test, and neither is declared in
  `install_requires` (`setup.py:17-24`).
- NASA's CDF Library (README:25) — a file-format library; the format itself is recorded in
  Field 18.
- GCS in Python (https://github.com/johan12345/gcs_python/) and PyThea
  (https://github.com/AthKouloumvakos/PyThea) — both reconstruct CME flux-rope geometry by fitting
  geometric models to coronagraph images. The object of study is the same but the measurement
  domain and the method differ, so the relation would rest on topic overlap that Fields 5 and 22
  and the keywords already carry.
- PREDSTORM (https://github.com/helioforecast/Predstorm) — solar-wind and geomagnetic forecasting,
  not flux-rope analysis. PlasmaPy (https://github.com/PlasmaPy/PlasmaPy) — a general plasma-physics
  framework. CloudCatalog (https://github.com/heliocloud-data/cloudcatalog) — indexing of cloud-hosted
  data; its clouds are computing clouds, not magnetic clouds.

### 30. Interoperable Software (OPTIONAL)

Not found — no value is recorded.

The bar for this field is a demonstrated exchange between peer tools: a shared or converted data
model, an adapter, a companion relationship or a documented import of one tool's output into the
other. PyGS has none. It uses `spacepy.pycdf` only internally, to read the CDF files that `ai.cdas`
returns, and exposes pandas objects and its own pickles and CSVs rather than any other tool's data
model. Both dependencies are recorded in Field 29, where dependency relations belong; the previous
extraction listed them here.

### 31. Related Instruments (OPTIONAL)

**Instrument 1:**
- **Instrument Name:** ACE Magnetic Field Instrument
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ACE/MAG

**Instrument 2:**
- **Instrument Name:** ACE Solar Wind Electron, Proton and Alpha Monitor
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ACE/SWEPAM

**Instrument 3:**
- **Instrument Name:** Wind Magnetic Field Investigation
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/Wind/MFI

**Instrument 4:**
- **Instrument Name:** Wind Solar Wind Experiment
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/Wind/SWE

**Instrument 5:**
- **Instrument Name:** Magnetic Field
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/Ulysses/FGM

**Instrument 6:**
- **Instrument Name:** Solar Wind Plasma
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/Ulysses/SWOOPS

**Instrument 7:**
- **Instrument Name:** PSP FIELDS
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS

**Instrument 8:**
- **Instrument Name:** PSP SWEAP
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/SWEAP

**Instrument 9:**
- **Instrument Name:** Magnetometer
- **Instrument Identifier:** https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/MAG

**Instrument 10:**
- **Instrument Name:** Proton-Alpha Sensor
- **Instrument Identifier:** https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Solar_Orbiter/PAS

Names are the vocabulary rows' stored names, copied verbatim; the identifier is the binding key.
Each mission contributes a magnetometer and a solar-wind plasma instrument, the two measurements
Grad–Shafranov reconstruction needs. PyGS reads these instruments' data directly and exists to
analyse it, so it passes the designed-to-support test.

**Dataset-to-instrument mapping**, from the eighteen `cdas.get_data` dataset IDs in
`PyGS/FluxRopeDetection.py`, each checked against CDAWeb's own dataset metadata (`GET
https://cdaweb.gsfc.nasa.gov/WS/cdasr/1/dataviews/sp_phys/datasets?idPattern=<DATASET>`, fields
`Instrument` and `Label`; 2026-09-10):

- `AC_H0_MFI` (CDAWeb instrument MAG) → ACE/MAG
- `AC_H0_SWE` (SWEP, the ACE/SWEPAM label) → ACE/SWEPAM
- `WI_H0_MFI` (MFI) → Wind/MFI
- `WI_K0_SWE`, `WI_H0_SWE`, `WI_H5_SWE`, `WI_H1_SWE` (SWE) → Wind/SWE
- `UY_1MIN_VHM` (VHM) → Ulysses/FGM
- `UY_M0_BAI` (BAI) → Ulysses/SWOOPS
- `PSP_FLD_L2_MAG_RTN` (MAG_RTN, FIELDS fluxgate magnetometer) and `PSP_FLD_L3_SQTN_RFS_V1V2`
  (FIELDS quasi-thermal noise from the Radio Frequency Spectrometer) → ParkerSolarProbe/FIELDS
- `PSP_SWP_SPC_L3I` (SWEAP/SPC) and `PSP_SWP_SPI_SF0A_L3_MOM` (SWEAP/SPAN) →
  ParkerSolarProbe/SWEAP
- `SOLO_L2_MAG-RTN-NORMAL` (MAG) → Solar_Orbiter/MAG
- `SOLO_L2_SWA-PAS-GRND-MOM` (SWA-PAS) → Solar_Orbiter/PAS

Not mapped: `AC_OR_SSC`, an SSCWeb spacecraft-position product (no measuring instrument), and the
two merged hourly products `UY_COHO1HR_MERGED_MAG_PLASMA` and `SOLO_COHO1HR_MERGED_MAG_PLASMA`,
which are derived from the same magnetometer and plasma instruments already listed.

**Why each choice.**

- *PSP at suite level.* SPASE gives every FIELDS child row the same name, PSP FIELDS, and every
  SWEAP child row the same name, PSP SWEAP, and the entry page shows row names only, so child rows
  would display as duplicates. The SQTN dataset also derives from the Radio Frequency Spectrometer,
  which SPASE splits into two children,
  https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/RFS/LFR and
  https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/FIELDS/RFS/HFR, with nothing in the
  code choosing between them; the suite row resolves that ambiguity.
- *Solar Orbiter from CNES/CDPP-AMDA.* The instrument rows under the `SolarOrbiter` spelling
  (ESA, NASA and SMWG authorities) cover EPD, EUI, Metis, PHI, STIX, SoloHI, Ephemeris and SPICE —
  none is MAG or SWA. The CNES/CDPP-AMDA rows under the `Solar_Orbiter` spelling are the only records
  of those two instruments, so the mixed authority is forced, not chosen.
- *Ulysses magnetometer.* The SMWG row https://spase-metadata.org/SMWG/Instrument/Ulysses/MAG
  (name Magnetometer, abbreviation MAG) also exists. The FGM row was chosen because its stored
  abbreviation, HED/VHM/FGM, names the VHM from which `UY_1MIN_VHM` comes.
- *SMWG over archive-scoped duplicates.* CNES/CDPP rows also exist for ACE, Wind, Ulysses and PSP
  instruments — for example https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/ACE/MAG,
  https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/ACE/SWEPAM,
  https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Wind/MFI,
  https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Wind/SWE,
  https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Ulysses/FGM,
  https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/Ulysses/SWOOPS,
  https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/PSP/MAG,
  https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/PSP/SPC,
  https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/PSP/SPI and
  https://spase-metadata.org/CNES/Instrument/CDPP-Archive/PSP/FIELDS/MAG. They are archive-scoped
  records of instruments that have canonical SMWG rows, and the SMWG rows are used, consistent with
  the SMWG mission rows in Field 32.
- *Ephemeris rows* (for example https://spase-metadata.org/SMWG/Instrument/ACE/Ephemeris) are
  rejected: they are position records, not measuring instruments.

**Sweep method, so a later refresh can re-derive the candidates:** take the instrument rows whose
identifier contains `/Instrument/` and has a path segment equal, case-insensitively, to a mission
token — ace; ulysses; wind; psp or parkersolarprobe; solarorbiter, solo or solar_orbiter. Searching
row names for substrings is noise for short tokens like ACE and Wind and blind to spelling variants
such as `SolarOrbiter` against `Solar_Orbiter`. Every row used carries a `https://spase-metadata.org/`
identifier.

Before this refresh HSSI held no related instruments for this entry.

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** Advanced Composition Explorer
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ACE

**Observatory 2:**
- **Observatory Name:** International Solar Polar Mission
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Ulysses

**Observatory 3:**
- **Observatory Name:** ISTP/Wind
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/Wind

**Observatory 4:**
- **Observatory Name:** Parker Solar Probe
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe

**Observatory 5:**
- **Observatory Name:** Solar Orbiter
- **Observatory Identifier:** https://spase-metadata.org/ESA/Observatory/SolarOrbiter

These are the five observatory rows held before this refresh, unchanged; names are the stored row
names, copied verbatim. README:11 names the supported spacecraft as "PSP, Solar Orbiter, Ulysses,
ACE, and WIND", and the code's datasets (Field 31) confirm all five. Each is a mission whose data
PyGS reads directly.

**Two names look unfamiliar and are correct.** Ulysses's row displays as International Solar Polar
Mission, Ulysses's original full mission name, and Wind's as ISTP/Wind. Both are the canonical SMWG
mission rows. Archive-scoped CNES rows that happen to carry the familiar short names —
https://spase-metadata.org/CNES/Observatory/CDPP-Archive/Ulysses (name Ulysses) and
https://spase-metadata.org/CNES/Observatory/CDPP-Archive/Wind (name Wind) — were considered and not
used. The other candidates considered and not used are the CNES/CDPP-AMDA rows
https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/ACE,
https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/Ulysses,
https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/Wind,
https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/PSP and
https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SolO, and the CNES/CDPP-Archive row
https://spase-metadata.org/CNES/Observatory/CDPP-Archive/PSP. Solar Orbiter's only row under the
`SolarOrbiter` spelling is the ESA one used here.

Under the vocabulary policy, a row's `name` holds the full name and its `abbreviation` holds the
short form, so these two rows carry the short forms Ulysses and Wind as their abbreviations, set on
the database side, and their names are unchanged. The entry page labels each observatory with its
row name, so these two rows appear there as International Solar Polar Mission and ISTP/Wind; an
abbreviation does not change that label. HSSI's site search matches a row's abbreviation as well as
its name, which is why the policy keeps the short form there, and the public view API renders a row
that has an abbreviation as its name followed by the abbreviation in parentheses. The short names
are therefore carried by the abbreviation rather than by a different row or a new name: the
archive-scoped CNES rows that carry them are not used, for the reasons in the paragraph above, and
the two SMWG rows are not renamed, because under the same policy the full name belongs in `name`.

### 33. Logo (OPTIONAL)

https://raw.githubusercontent.com/PyGSDR/PyGS/c12cc7a92352427a2cd6496d309e2417a7d87781/logo/logo.png

**What it shows.** A purpose-made logo, `logo/logo.png` in the repository (1178 × 1178 PNG), that
reads Python for GS. Its G is drawn from twisted field-line traces and its S from the package's own
figure types — a jagged trajectory from a start marker to an end marker in the upper bowl, and a
Pt′–A′ curve in the lower bowl — with a flux-rope cross-section, crossed by a dashed spacecraft path
between two S/C markers, behind the word Python.

**The URL is a repair, and the `blob/` form must not be restored.** The PyHC registry designates
this asset but gives it as `https://github.com/PyGSDR/PyGS/blob/main/logo/logo.png` — a GitHub file
viewer page that answers with `Content-Type: text/html`, not the image. The URL above is the
`raw.githubusercontent.com` form of the same file, pinned to a commit rather than to the `main`
branch so that a later rename or move cannot silently break it. As of 2026-09-10 it serves
`image/png`, 538,464 bytes, byte-identical to the tracked file at the pin.

