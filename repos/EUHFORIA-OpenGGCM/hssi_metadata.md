# HSSI Metadata Extraction Results

**HSSI Software ID:** 639f0d69-543d-477f-be0f-764e9a5f08a3
**Repository:** https://github.com/anweshaM/EUHFORIA-OpenGGCM
**Source Revision:** afe57c9c1a8982eeac5e691c612974d26f5f6dac
**Extraction Date:** 2026-07-31
**Validation Date:** 2026-08-03
**Validation Status:** PASS

---

## Scope note

This software is an **archival snapshot of the supplementary code** for a single published study —
Maharana et al. (2024), *Employing the Coupled EUHFORIA-OpenGGCM Model to Predict CME
Geoeffectiveness*, Space Weather 22(5), https://doi.org/10.1029/2023SW003715. The paper's Open Data
Statement names this exact Zenodo deposit: *"The setup and input files, output files and the
plotting scripts are available at ... https://zenodo.org/doi/10.5281/zenodo.10404880."*

That fact governs how the whole repository should be read, and it is the reason several fields below
resolve the way they do:

- It is **not a library or an application**. There is no package, no installer, no entry point, no
  tests, no CI, and no dependency manifest. It is four standalone Python 2.7 scripts plus the exact
  input/output/configuration files for two specific CME events.
- **Neither of the two models it couples lives in this repository.** EUHFORIA and OpenGGCM are both
  external, non-public codes. What is here is the *adapter and analysis layer* between them, plus
  their run configuration. Functionality, region, and phenomena claims below are therefore anchored
  in what these scripts and configuration files demonstrably do, not in the full capability of
  either upstream model.
- The repository has a **seven-commit history, all between 2023-12-14 and 2023-12-19**, ending at
  the pinned revision, which is also the `v1.0.0` tag and the only release. There is no later state
  to reconcile against.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The original submitter of this HSSI record is not exposed by HSSI's published metadata, so the
person who first supplied these values is unknown. Because that person may have been the software's
maintainer, every field below treats their wording as intentional and preserves it unless primary
evidence shows it to be factually wrong (see Fields 7, 8 and 9).

### 2. Persistent Identifier (RECOMMENDED)
**https://doi.org/10.5281/zenodo.10404880**

This is the correct value. Zenodo reports `conceptdoi = 10.5281/zenodo.10404880`, so this is the
all-versions concept DOI, which is what Field 2 asks for. The version-specific DOI
`10.5281/zenodo.10404881` is a different value and belongs in Field 12 (Version PID), where it is
already correctly stored — the two must not be swapped.

Zenodo's version listing shows exactly one version (`index: 0`, `is_last: true`), so the concept DOI
and the sole version DOI describe the same deposit. A future refresh should re-check the version
list before assuming this is still true.

### 3. Code Repository (MANDATORY)
**https://github.com/anweshaM/EUHFORIA-OpenGGCM**

This is the correct value. The URL resolves, and it is the repository the DOI was minted from:
the DataCite record for the concept DOI carries
`relatedIdentifier: https://github.com/anweshaM/EUHFORIA-OpenGGCM/tree/v1.0.0` with
`relationType: IsSupplementTo`. The local clone's `origin` remote matches.

### 4. Software Functionality (MANDATORY)

- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Forecasting
- Models and Simulations: MHD
- Models and Simulations: Physics-Based
- Servers and Environments
- Servers and Environments: High Performance Computing

Every subcategory is listed together with its parent, because HSSI does not supply the parent
automatically.

HSSI previously carried only `Models and Simulations`. That single value was not wrong, but it
described about a fifth of what the repository does. Each of the other values is anchored to
specific code:

**Coordinate Transforms / Heliospheric / Magnetospheric.** `euhforia_heeq2gse.py` is a
coordinate-transformation script and nothing else. It says so twice, in two wordings that differ, so
either must be quoted exactly rather than paraphrased: the header comment at line 23 reads
*"Program that converts EUHFORIA outputs (v1.0) from HEEQ to GSE coordinates"*, while the banner the
script prints at line 28 reads *"Program that converts EUHFORIA output vectors (v0.1) from HEEQ to
GSE coordinates"*. The two carry different parenthetical version strings, and neither matches the
EUHFORIA data version recorded separately at line 24, *"EUHFORIA (v2.0) data at Earth"*. The script
reads EUHFORIA's heliocentric spherical output (`r`, `clt`, `lon`, `vr`, `vclt`, `vlon`, `Br`,
`Bclt`, `Blon`) and emits Cartesian GSE components (lines 71-82). HEEQ is a heliospheric frame, GSE is a magnetospheric
frame, so both subcategories apply — this is precisely a heliosphere-to-magnetosphere frame handoff.
`Coordinate Transforms: Solar` was considered and rejected: no solar-disk frame (Carrington,
Stonyhurst, helioprojective) appears anywhere in the repository.

**Data Processing and Analysis: File Format Conversion.** `satfilter_euh.py` reads one GSE text file
and writes twenty-one separate per-variable ASCII files in OpenGGCM's required layout
(`euh.np`, `euh.pp`, `euh.temp`, `euh.bxgse`, ... `euh.rr`; lines 30-52 and 112-155). The `readme`
describes this as the repository's second processing step. This is the clearest possible case of
format conversion.

**Data Processing and Analysis: Processing / Analysis.** `satfilter_euh.py` derives physical
quantities rather than merely copying them: proton density as half the EUHFORIA total density
(line 74), temperature from pressure and density via the ideal gas law (line 78), and fixed
magnetopause boundary conditions (lines 64-68). `paper_openggcm_loop.py` computes ram, magnetic and
thermal pressures (lines 166-172), field and speed magnitudes, and an R-squared model/observation
correlation (`compute_r2`, lines 252-261). It also applies the O'Brien & McPherron "AK2" and
Fenrich & Luhmann pressure corrections to the simulated ring-current Dst (lines 525-538).

**Data Processing and Analysis: Time Series Analysis.** This is the repository's dominant activity.
`paper_openggcm_loop.py` builds linear interpolators onto common time grids (`interpol`, lines
81-84), gap-fills (`interp_nan`, lines 86-92), matches nearest timestamps across two series
(`closest_time`, lines 310-317), and resamples model output onto the observation cadence before
saving (lines 721-742). `DTW_correct_paper_2023.py` implements windowed dynamic time warping from
scratch: the Euclidean cost and cumulative-cost matrices (lines 130-132), a 24-element alignment
window (`w = np.max([24, abs(len(real_stand)-len(model_stand))])`, line 139) applied in the
cumulative-cost recursion (lines 145-155), and backtracking to recover the warping path
(lines 178-204, with the reusable `path_DTW` at lines 207-229). All of that is reachable code, and
it alone carries this value — see the dead-code caveat below.

**Data Processing and Analysis: Data Reduction.** `DTW_correct_paper_2023.py` applies
Savitzky-Golay smoothing to both series before comparison, under the explicit comment *"Smoothing
both time series similarly"* (lines 91-108), and imports `uniform_filter1d` (line 12). It also masks
OMNI fill values (`99.99`, `999.99`, `9999.99`, `99999.9`) to NaN before analysis
(`paper_openggcm_loop.py` lines 154-161). This is noise-reduction filtering of scientific series,
which is what the subcategory covers.

**Data Visualization / Line Plots / 2D Graphics.** `paper_openggcm_loop.py` builds the paper's
seven-panel stacked figure — speed, proton density, Bz, Dst, AU, AL, AE against time — with axis
formatting, event annotations and PDF export (lines 347-781); the `readme` names it as the source of
Figures 3 and 5. Those are line plots. The 2D Graphics value comes from
`DTW_correct_paper_2023.py`: `distance_distance_plot` renders the cumulative DTW cost matrix as an
`imshow` heatmap with a colorbar (defined at lines 163-170), and it is called twice — at line 175
for the cost matrix alone, and again at line 203 with the recovered warping path overplotted on it.
Both call sites are reachable code, and they alone carry this value — see the dead-code caveat
below. `Movies`, `3D Graphics`, `Spectrogram`, `Orbit Plots` and `Web-Based` were all
checked against the code and rejected — there is no animation, no three-dimensional rendering, no
time-frequency transform, no trajectory plot and no browser output anywhere.

**Dead-code caveat: in `DTW_correct_paper_2023.py`, nothing after line 263 can execute.** Line 263
is an unconditional `quit()` at column 0, immediately after the `if save:` block at lines 258-262,
and `save` is hardcoded to `True` at line 35 (`save=np.bool(True)`). Lines 264-371 — the whole of
the file's "Figure 2", "Figure 3" and "Figure 4" sections, including the alignment-offset
computation (lines 268-300), the `plt.hist` amplitude- and time-difference histograms at lines 306
and 349, and their PNG exports at lines 326-328 and 364-366 — are unreachable at this revision.
Those histograms read as strong evidence for both `Data Visualization: 2D Graphics` and
`Data Processing and Analysis: Time Series Analysis`, and an earlier reading of this repository
cited them for exactly that. Neither value depends on them: both rest on the reachable evidence
given above. This is recorded so a future agent neither re-cites the histograms as live
functionality nor reads their absence from the rationale as an oversight.

**Models and Simulations / MHD / Physics-Based / Data Guided / Forecasting.** The repository ships
four complete 452-line OpenGGCM `runme` configurations — one per event per driver — which define
the MHD run itself: solver selection and coordinate system (`MHDCOORD MHD`, `MHD fortran`), flux
limiters (`DO_LIMIT2`, `DO_LIMIT3`, `LIMIT_ASPECT_LOW`), grid and MPI decomposition, the coupled
CTIM thermosphere-ionosphere version (`CTIM 1.0.10`), the Rice Convection Model ring current
(`RCMCODE rice`, `RCM_XX1 -15.0`, `RCM_XX2 40.0`), ionospheric conductance parameters, and the run
interval. That is a magnetohydrodynamic, physics-based simulation configuration, not a description
of one. `Data Guided` follows from the driver switch `SWMON`, which is set to `euh` in the
EUHFORIA-driven runs and to `wi` (Wind) or `omni` in the observation-driven runs — the model is
boundary-driven by external data in every case. `Forecasting` follows from the study's stated
purpose, quoted in the paper's own highlights: *"Geomagnetic indices can be predicted 1-2 days in
advance with EUHFORIA, as opposed to the much shorter predictions with real-time L1 data."*

`Models and Simulations: Empirical` was **considered and not selected.** The argument for it is real
— the O'Brien & McPherron and Fenrich & Luhmann Dst pressure corrections in
`paper_openggcm_loop.py` lines 525-538 are empirical parameterizations, and the file imports a
`compute_dst` empirical Dst model at line 32. Two things argue against it: the `compute_dst` module
is **not present in this repository** (the import would fail, and its call site is gated behind
`emp_dst_bool = False` at line 465), and the surviving empirical content is a three-coefficient
correction applied to physics-model output rather than a model in its own right. Recorded here so
the reasoning does not have to be redone; a future curator who disagrees has the line references.

`Models and Simulations: First Principles` was also considered and not selected. OpenGGCM does solve
the MHD equations from first principles, but that code is not in this repository — what is here
configures it. `MHD` and `Physics-Based` already carry that meaning without over-claiming.

**Servers and Environments / High Performance Computing.** The same `runme` files are HPC job and
build configuration: MPI compiler selection (`MPIF77`, `MPIF90`, `MPICC`, `MPICXX`), a 13x6 MPI
domain decomposition (`NPX 13`, `NPY 6`), a 200-hour wallclock request (`RUNTIME 200:00:00`), batch
class, and a named cluster target (`TARGET marvin_anu`). The paper identifies that target: *"Computations
were performed on Marvin, a Cray CS500 supercomputer at UNH."* Running this software as intended
requires an HPC allocation, which is exactly what the category signals to a searcher.

**Rejected, with reasons, so they are not re-proposed:**
- `Data Processing and Analysis: Data Access and Retrieval` — the repository contains **no network
  code at all**. Every OMNI, Wind and F10.7 file is a pre-downloaded listing committed to the repo.
  Retrieval happened by hand through CDAWeb and OMNIWeb before the code ran.
- `Data Processing and Analysis: Plasma Moments` — temperature and density are computed from MHD
  bulk variables via the ideal gas law, not integrated from velocity distribution functions, which
  is what this subcategory means.
- `Data Processing and Analysis: 2D Slices` and `Data Visualization: 2D Slices` — the OpenGGCM
  output-plane switches are explicitly disabled in every shipped configuration
  (`OUTPLANEX 0`, `OUTPLANEY 0`, `OUTPLANEZ 0`).
- `Data Processing and Analysis: Field-line Tracing` — the committed `ae.txt` files begin with
  OpenGGCM warnings that `h_aurora` and `flxz` in `src/fieldlines` could not be found, i.e. the
  field-line post-processing did **not** run and is in any case OpenGGCM's, not this repository's.
- `Mission-related` and all its children — this is a research analysis snapshot, not part of any
  mission's ground system or data pipeline.

### 5. Related Region (MANDATORY)

- Earth Magnetosphere
- Earth Inner Magnetosphere
- Earth Ionosphere
- Earth Thermosphere
- Earth Auroral Subregion
- Solar Wind
- Interplanetary Space

No region value was previously stored for this record, despite Field 5 being mandatory.

The region set follows the physical chain the software implements, end to end:

- **Solar Wind** and **Interplanetary Space** — the input side. `hsphere_Earth.dsv` is EUHFORIA
  heliospheric output sampled at Earth (its first data row records `r = 1.0166 AU`), and the
  observation-driven runs are fed by Wind and OMNI solar-wind measurements at L1. Every driving
  variable is a solar-wind or interplanetary magnetic field quantity.
- **Earth Magnetosphere** — OpenGGCM is a global magnetospheric MHD model; the shipped
  configurations define its full simulation domain.
- **Earth Inner Magnetosphere** — the runs enable the Rice Convection Model ring current
  (`RCMCODE rice`) over a domain of `RCM_XX1 -15.0` to `RCM_XX2 40.0` Earth radii, and the primary
  scientific output is Dst/SYM-H, which is a direct measure of inner-magnetospheric ring current
  energy.
- **Earth Ionosphere** — the configurations set ionospheric coupling parameters (`IONODT`,
  `SIGMATRANS`, `SIGMAFAK`, `SIG_H_BACK`, `SIG_P_BACK`, `RCM_IONO 120.0` km) and the code reads and
  plots the ionospheric electrojet indices the model produces.
- **Earth Thermosphere** — the runs couple the Coupled Thermosphere-Ionosphere Model
  (`CTIM 1.0.10`), with roughly fifty CTIM parameters set in each `runme` (tidal amplitudes and
  phases, wind and temperature limits, input field tables). The stored HSSI description already
  named the thermosphere; this region value now backs that claim.
- **Earth Auroral Subregion** — AE, AL and AU are auroral electrojet indices by definition, and
  `paper_openggcm_loop.py` reads, interpolates and plots all three
  (`get_og_ae`, lines 290-308; panels 5-7, lines 583-706).

**Considered and rejected:**
- `Earth Magnetotail` — the RCM domain does extend anti-sunward to 40 Earth radii and the paper
  discusses substorm signatures, but no output, script or figure in this repository targets tail
  structure specifically. Listing it would over-claim.
- `Earth Magnetosheath` and `Earth Outer Magnetosphere` — inside the MHD domain, but nothing in the
  code or outputs addresses them as a subject.
- `Corona`, `Chromosphere`, `Photosphere`, `Solar Environment`, `Solar Interior` — EUHFORIA has a
  coronal model, but this repository does not use it. Its EUHFORIA input begins at
  `hsphere_Earth.dsv`, the *heliospheric* output already extracted at Earth. There is no solar-source
  modelling here at all.
- `Earth Atmosphere` and `Earth Lower and Middle Atmosphere` — the more specific `Earth Thermosphere`
  and `Earth Ionosphere` are correct; the broad values would be less informative.

### 6. Authors (MANDATORY)

**1. Anwesha Maharana**
- Identifier: https://orcid.org/0000-0002-4269-056X
- Affiliation: KU Leuven — https://ror.org/05f950310
- Affiliation: Royal Observatory of Belgium — https://ror.org/00hjks330

**2. W. Douglas Cramer**
- Identifier: https://orcid.org/0000-0001-7742-2015
- Affiliation: University of New Hampshire — https://ror.org/01rmh9n78

**3. Camilla Scolini**
- Identifier: https://orcid.org/0000-0002-5681-0526
- Affiliation: Royal Observatory of Belgium — https://ror.org/00hjks330
- Affiliation: University of New Hampshire — https://ror.org/01rmh9n78

#### Why the stored value is wrong

HSSI stores a single author with `familyName: "anweshaM"`, an empty `givenName`, no identifier and
no affiliation. `anweshaM` is a **GitHub username, not a person's name**. It reached HSSI because the
Zenodo deposit was created through the GitHub-Zenodo release webhook, which records the account
login when the account has no display name set; the GitHub profile for `anweshaM` has
`"name": null`, so no better string was available to it. DataCite faithfully mirrors the same
mistake, with `nameType: "Personal"`, `familyName: "anweshaM"` and empty `nameIdentifiers`.

This is an error of provenance, not a stylistic preference, so it is corrected here rather than
preserved. The person is **Anwesha Maharana**, established independently three times over:

- The repository owner is `anweshaM`, and the other committer identity in the history is
  `u0141347@...luna.kuleuven.be` — a KU Leuven account number. The same account number appears
  inside the code as an author's own working path,
  `/home/u0141347/kul/paper_ongoing/Paper2_OpenGGCM/` (`DTW_correct_paper_2023.py`, lines 54 and
  117), and in the committed OpenGGCM warning lines in `Event1/Event1-euh/ae.txt`. The two Git
  identities are one person.
- `Event1/Event1-euh/runme` sets `TUSER anwesham` — the KU Leuven/HPC username, spelling out the
  name.
- Anwesha Maharana is first author and corresponding author of the paper this code accompanies, with
  ORCID 0000-0002-4269-056X asserted by the publisher through Crossref.

#### Why the other two authors are included

Both are named **inside the repository**, not merely on the paper:

- **Camilla Scolini** — `satfilter_euh.py` line 17 carries the header
  `# Developer: Camilla Scolini, Anwesha Maharana`. That is an explicit, in-repository authorship
  statement for one of the four scripts.
- **W. Douglas Cramer** — every `runme` carries the attribution comment at line 12,
  `# WDC: runme derived from input.defines in master (b3cadd)`. `WDC` are W. Douglas Cramer's
  initials; he is the paper's second author, works at the University of New Hampshire where
  OpenGGCM is developed and where these runs were performed, and is the first author of the
  OpenGGCM-RCM coupling paper the configurations exercise. The identification is reinforced by the
  analysis code, which twice references his approach by first name — `omni_pram_doug` and the
  comment `#Fenrich and Luhmaan 1998 params as used by UCB_Doug` in `paper_openggcm_loop.py`
  (lines 171 and 523). The `runme` files are 452 lines each and are among the repository's most
  substantial artifacts.

ORCIDs and affiliations were confirmed against each author's public ORCID record, not just the
paper, and both of Scolini's institutions are recorded deliberately even though her appointments do
not overlap. Her ORCID lists two consecutive University of New Hampshire posts at the Institute for
the Study of Earth, Oceans, and Space — Postdoctoral Fellow 2020-09 to 2022-09, then Research
Scientist 2022-09 to 2023-08-31 (ROR https://ror.org/01rmh9n78) — which end shortly *before* the
December 2023 release, and a Royal Observatory of Belgium post at the Solar Influences Data Analysis
Center running 2023-09-01 to 2024-10-31 (ROR https://ror.org/00hjks330), which does cover it. Only
ROB was current at release, but Crossref's publisher-asserted author list credits Scolini with both
institutions for this work, so both are kept: ROB is the affiliation of record at release, UNH is
where the OpenGGCM half of the study was carried out. Both RORs are confirmed. ORCID places Maharana
at KU Leuven's Centre for mathematical Plasma Astrophysics.

Affiliations are recorded at institution level with RORs because HSSI has no rows for the sub-units
(CmPA, SIDC, the UNH Institute for the Study of Earth, Oceans and Space), and matching an existing
HSSI
organization exactly avoids minting near-duplicate rows. `Royal Observatory of Belgium` and
`University of New Hampshire` already exist in HSSI with these exact RORs, and their spellings are
reused verbatim; `KU Leuven` has no pre-existing row, so recording it introduces one.

`KU Leuven` is recorded in that form deliberately, even though Field 25/6 guidance prefers expanded
names: it is the institution's own official English name and its ROR display name. The fully
expanded Dutch label is `Katholieke Universiteit Leuven`, recorded here in case a curator prefers
it; the ROR disambiguates either way.

#### Three further paper co-authors, considered and not included

The paper has six authors; three are recorded above. The other three are deliberately **not** part
of this field's value:

- **Evangelia Samara** — https://orcid.org/0000-0002-7676-9364; National Aeronautics and Space
  Administration Goddard Space Flight Center, https://ror.org/0171mag52
- **Joachim Raeder** — https://orcid.org/0000-0002-2690-7458; University of New Hampshire,
  https://ror.org/01rmh9n78
- **Stefaan Poedts** — https://orcid.org/0000-0002-1743-0651; KU Leuven, https://ror.org/05f950310,
  and Institute of Physics, Maria Curie-Skłodowska University, https://ror.org/015h0qg34

The reason is the distinction Field 6 draws: it asks for the authors *of this software*, and this
repository is the adapter layer between EUHFORIA and OpenGGCM, not either model. Raeder and Poedts
authored the upstream models, and those models are explicitly **not** in this repository (see the
scope note); Samara co-authored the dynamic-time-warping methodology the code applies rather than
the code itself. Nothing in the repository attributes any file, script or configuration to any of
the three, whereas each of the three authors above is named inside it. Crediting the upstream model
authors here would attribute this adapter code to people who did not write it, and would also
misdirect a searcher looking for who to contact about these scripts.

The competing reading is real and is recorded rather than dismissed: Field 6 could be read as
"credit the study team," in which case all six paper authors belong. That reading was **weighed and
rejected** in favour of "credit the code contributors." All three identifiers, affiliations and RORs
are written out above precisely so that a future curator who reaches the opposite conclusion can act
on it without redoing any research.

#### The stored author is replaced, not renamed

The previously stored Person — `familyName: "anweshaM"`, blank `givenName`, no identifier, no
affiliation — is superseded by the three authors above rather than corrected in place. That
distinction is a fact about the record rather than a detail of presentation: none of the three
ORCIDs above previously existed anywhere in HSSI, so the three authors are new Person identities
standing in place of the old one, and no row was carried forward under a corrected name.

Renaming was not an available alternative in any case, and the reason is a durable HSSI limitation
worth carrying forward: HSSI silently discards a rename of an existing Person row — the new name is
accepted and then not applied. A related hazard is that an authors update is rejected outright when
a Person in the list carries a blank `givenName`, as the `anweshaM` row did. Both behaviours will
matter again for any future correction to an author's name on this record; neither affects what the
correct values are, which are the three recorded above.

### 7. Software Name (MANDATORY)
**EUHFORIA OpenGGCM**

Kept as submitted. The repository itself is named `EUHFORIA-OpenGGCM` (hyphenated), the GitHub
release is titled `EUHFORIA+OpenGGCM v1.0.0`, and the paper calls it *"the coupled EUHFORIA-OpenGGCM
model"* — so three spellings of the same name circulate, differing only in the separator. The stored
form is unambiguous and recognizable, and choosing between a space, a hyphen and a plus sign is a
stylistic preference rather than a correction. `EUHFORIA-OpenGGCM` is noted here as the repository's
own spelling in case a curator prefers to match Field 3 exactly.

### 8. Description (MANDATORY)

> The first release of codes to generate EUHFORIA output in the format of OpenGGCM inputs, visualize
> the results of OpenGGCM outputs, and perform the dynamic time warping analysis to assess the
> performance of OpenGGCM results. EUropean Heliospheric FORecasting Information Asset (EUHFORIA) is
> a physics-based data-driven solar wind and coronal mass ejections (CMEs) propagation model designed
> for space weather forecasting and event analysis investigations. The Open Geospace General
> Circulation Model (OpenGGCM) is a magnetohydrodynamic model of the response of Earth's
> magnetosphere, ionosphere, and thermosphere to transient solar wind characteristics.
>
> The repository contains Python scripts that rotate EUHFORIA heliospheric output at Earth from HEEQ
> to GSE coordinates and split it into the per-variable ASCII files OpenGGCM reads, the complete
> OpenGGCM run configurations for the two CME events studied (12 July 2012 and 4-6 September 2017),
> each in an EUHFORIA-driven and an observation-driven (Wind or OMNI) variant, and scripts that plot
> the simulated solar wind and Dst, AE, AL and AU indices against OMNI observations and perform a
> windowed dynamic time warping comparison of predicted and observed Dst and AE time series. It is
> the supplementary code for Maharana et al. (2024), Space Weather, and is written for Python 2.7.

**The first paragraph is the submitted text, preserved verbatim — not a word of it is altered.**
Every statement in it is accurate. The first sentence is the author's own Zenodo release note,
reproduced verbatim in the GitHub release body; the second and third are lifted from the abstract of
the accompanying paper and correctly define the two models. There was no factual error to correct,
so the submitter's wording stands as written.

**The second paragraph is an addition, and it closes a real gap.** The submitted text says what the
two models *are* but never says what is actually *in* the repository: the HEEQ-to-GSE rotation, the
two specific CME events, the paired EUHFORIA-driven and observation-driven run configurations, or
the Python 2.7 requirement. A user deciding whether this software is useful to them could not learn
any of that from the original three sentences, which describe two models that are not themselves in
this repository at all (see the scope note). Extending rather than rewriting was chosen precisely
because it adds the missing information without overwriting an editorial voice that was never wrong.
Every claim in the addition is evidenced elsewhere in this file: the rotation and the DTW comparison
in Field 4, the per-variable ASCII split in Fields 18 and 19, the four run configurations and their
`SWMON` drivers in Fields 4 and 32, the plotted indices in Field 5, the reference publication in
Field 14, and Python 2.7 in Field 13.

**Length is not a constraint here.** The combined text is 1,335 characters, counting the two newline
characters that separate the paragraphs in the stored value. The 200-character cap belongs to Field 9
(Concise Description), not to this field: Description is an uncapped text field, and HSSI's
published records include descriptions several times longer than this one — the longest in
production, Solar Soft's, runs to 3,963 characters. No truncation or condensing is needed.

### 9. Concise Description (OPTIONAL)

> The first release of codes to generate EUHFORIA output in the format of OpenGGCM inputs, visualize
> the results of OpenGGCM outputs, and perform the dynamic time warping analysis.

*(178 characters, within the 200-character limit.)*

**This corrects a truncation artifact.** The previously stored value was the stored Description —
then just the three sentences that now form Field 8's first paragraph — mechanically cut at exactly
200 characters, **mid-word**:

> The first release of codes to generate EUHFORIA output in the format of OpenGGCM inputs, visualize
> the results of OpenGGCM outputs, and perform the dynamic time warping analysis to assess the
> performa

Ending `...to assess the performa` is not authored prose and not a preview anyone chose; it is what a
searcher saw. Field 9 exists precisely to supply a clean preview when a blunt truncation of the
Description will not do, and this is exactly that case.

The correction keeps the submitter's own sentence and only ends it at a natural stop, so no
editorial voice is overwritten — that is why it was preferred to writing a fresh preview.

**Rejected alternative.** A fresh preview naming the coupling explicitly was drafted and **not**
selected: *"Supplementary code coupling EUHFORIA heliospheric simulations to the OpenGGCM
magnetosphere model: format conversion, run setup, visualization, and dynamic time warping
assessment of Dst and AE."* (194 characters.) It is arguably more informative to a reader who does
not already know the two models, but it replaces the submitter's wording in a field where that
wording was never the problem — only the truncation was. It is recorded here in case a curator later
judges the trade-off differently.

### 10. Publication Date (RECOMMENDED)
**2023-12-19**

This value is re-derived from the repository rather than taken on trust from Zenodo:
the GitHub release `v1.0.0` was published `2023-12-19T09:48:19Z`, the `v1.0.0` tag points at commit
`afe57c9c` dated 2023-12-19, and Zenodo's `publication_date` and DataCite's `Issued` date agree. All
four independent sources give the same day, so this is one of the fields where the Zenodo-derived
value happens to be right.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

The DOI was minted through the GitHub-Zenodo release workflow, which is
exactly the case Field 11 names as belonging to Zenodo. Zenodo has no ROR of its own (its host
institution CERN does, at https://ror.org/01ggx4157, but CERN is not the publisher of this deposit),
so the service URL is the correct identifier. `Zenodo` already exists in HSSI with this identifier.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.0.0
- **Version Date:** 2023-12-19
- **Version Description:** The first release of codes to generate EUHFORIA output in the format of
  OpenGGCM inputs, visualize the results of OpenGGCM outputs, and perform the dynamic time warping
  analysis to assess the performance of OpenGGCM results.
- **Version PID:** https://doi.org/10.5281/zenodo.10404881

All four sub-fields are complete and correct.

**`v1.0.0` is the stored value, with the leading `v`.** This matters, because HSSI's public view of
the record renders the version as `EUHFORIA OpenGGCM - v1.0.0`, prefixing the software name. That
rendered string is a display transform, not data: writing it back would corrupt the stored number.
The stored value is the bare `v1.0.0`, and the `v` prefix is corroborated by the Git tag (`v1.0.0`),
the GitHub release `tag_name` (`v1.0.0`), and Zenodo's own `version` field (`v1.0.0`).

**`v1.0.0` is still the latest release.** Zenodo lists exactly one version; GitHub lists exactly one
release and one tag; the repository has no commits after the tagged revision. There is nothing newer
to move to.

The Version PID correctly holds the version-specific DOI `10.5281/zenodo.10404881`, distinct from the
concept DOI in Field 2 — the two are not interchangeable and should not be reconciled to each other.

Note for a future refresh: HSSI replaces rather than edits a version row, so a version change here
leaves the previous row orphaned in the database. That is accepted behaviour and is not a defect to
clean up.

### 13. Programming Language (RECOMMENDED)
- Other
- Python 2.x

**`Python 3.x` was previously stored and is factually wrong.** None of the four Python files in this
repository can run on Python 3:

- `euhforia_heeq2gse.py` uses Python 2 `print` statements at lines 20 and 27-30 and 49 and 66, which
  are syntax errors under Python 3, and imports `ConfigParser` (line 5), renamed in Python 3.
- `satfilter_euh.py` does the same at lines 4, 9 and 110, and its own header states the requirement
  outright: `# Python vers. 2.7-18` (line 19).
- `paper_openggcm_loop.py` imports `cPickle` (line 21), which does not exist in Python 3.
- `DTW_correct_paper_2023.py` imports `cPickle` (line 13) and the long-removed
  `scipy.ndimage.filters` (line 12).

`Python 2.x` is the correct value, spelled exactly as HSSI's `ProgrammingLanguage` vocabulary
spells it.

**`Other` is retained, and it is defensible — it covers the shell scripts.** The four OpenGGCM
`runme` files each begin `#!/usr/bin/env bash` and are executable Bash, totalling about 132 kB, which
is more shell code than Python code by volume. HSSI's `ProgrammingLanguage` vocabulary has no
`Shell`, `Bash` or `sh` row, so `Other` is the only available representation. Recording this removes
the ambiguity in the previously unexplained `Other`.

**Do not add `Pascal`.** GitHub's language statistics report Pascal as the repository's dominant
language at about 2.08 MB — more than thirty times the Python. This is a linguist mis-detection: the
`.pp` extension is Free Pascal source, and the files here named `euh.pp`, `wi.pp` and `omni.pp` are
plain-text OpenGGCM plasma-pressure input tables (`2012 7 11 11 53 18.000 5.41250000`). There is no
Pascal in this repository. Anyone re-running an automated extraction will see the same false signal.

**Do not add a Fortran value either.** The `runme` files configure Fortran compilers (`LOCALF77
gfortran`, `MPIF77`, `MPIF90`) and reference OpenGGCM `.for` sources, but those sources belong to
OpenGGCM and are not present here.

### 14. Reference Publication (RECOMMENDED)
**https://doi.org/10.1029/2023SW003715**

Maharana, A., Cramer, W. D., Samara, E., Scolini, C., Raeder, J., & Poedts, S. (2024). Employing the
Coupled EUHFORIA-OpenGGCM Model to Predict CME Geoeffectiveness. *Space Weather*, 22(5).

This field was empty. The paper is unambiguously the publication describing this software: its Open
Data Statement points at this software's own concept DOI as the location of *"the setup and input
files, output files and the plotting scripts"*, and every script in the repository is named for a
figure or analysis in it (`paper_openggcm_loop.py` produces Figures 3 and 5,
`DTW_correct_paper_2023.py` produces Figures 4 and 6, per the `readme`).

This DOI was previously stored in Field 27 (Related Publications) and nowhere else. It has been
moved here, because Field 27 is defined for publications *"different from the reference
publication"* and this is the reference publication. Field 27 no longer lists it; the reasoning for
the relocation, and the rejected option of keeping it in both fields, are recorded there.

### 15. License (RECOMMENDED)
**Other**

The license this record actually carries is **CC0 1.0 Universal**, whose canonical legal-code URI is
https://creativecommons.org/publicdomain/zero/1.0/legalcode. `Other` is the entirety of the storable
value: HSSI has nowhere to keep that URI, for the reason set out under *The CC0 URI cannot be stored
in HSSI* below. The URI is recorded here instead, because it, and not the bare word `Other`, is what
identifies this software's license.

**The repository's actual license is CC0 1.0 Universal, not CC-BY 4.0.** The `LICENSE` file at the
repository root opens `Creative Commons Legal Code` / `CC0 1.0 Universal` and contains the full CC0
public-domain dedication — a waiver of rights, with no attribution requirement anywhere in its 121
lines. Two independent detectors read the same file the same way: GitHub's license API returns
`{"key": "cc0-1.0", "spdx_id": "CC0-1.0", "name": "Creative Commons Zero v1.0 Universal"}`, and an
independent repository-metadata extraction returns `spdx_id: CC0-1.0`.

**HSSI's stored `Creative Commons Attribution 4.0 International` came from Zenodo and is an
artifact.** Zenodo's record asserts `cc-by-4.0`, which DataCite mirrors as
`Creative Commons Attribution 4.0 International` with `rightsIdentifierScheme: SPDX` — a
presentation confident enough to look authoritative. It is Zenodo's own default for GitHub-webhook
deposits, and DOI autofill copies such errors verbatim rather than re-reading the repository. The
LICENSE file is the author's own act of licensing and is archived inside the very deposit that
carries the contradictory claim, so the repository wins.

CC0 and CC-BY are materially different — CC0 waives attribution, CC-BY requires it — so this is a
correction of substance, not of wording.

**Why the value is `Other` rather than a CC0 row: HSSI's `License` vocabulary has no CC0 entry.**
The live list holds exactly eleven rows — Apache License 2.0; BSD 2-Clause "Simplified" License;
BSD 3-Clause "New" or "Revised" License; Creative Commons Attribution 4.0 International; GNU General
Public Licenses (GPL version 2); GNU General Public License v3.0 or later; GNU Lesser General Public
License v3.0 only; GNU Library or ‘Lesser’ General Public Licenses (LGPL version 2); MIT License;
Other; Restricted. There is no `CC0 1.0 Universal`, no `Creative Commons Zero v1.0 Universal` and no
`Public Domain`. The list is closed, so an SPDX title that is not a row is rejected outright. `Other`
is therefore the only faithful representation available, and no near-miss row may be substituted for
it.

That enumeration is transcribed byte-for-byte, quirks included: the LGPL version 2 row really does
use the curly quotation marks ‘ and ’ (U+2018 and U+2019) around *Lesser*, not ASCII apostrophes.
HSSI resolves controlled-list values by exact case-insensitive name match after a bare strip, with
no alias table, so those characters are part of the row's identity and must not be "normalized" to
straight quotes by anyone re-reading this list.

**The CC0 URI cannot be stored in HSSI, and must not be forced in.** HSSI's `Software` model has no
per-record license-URI column. A license URI lives on the shared `License` row itself, and the `url`
of the `Other` row is empty. Writing the CC0 legal-code URI there would not describe this record; it
would assert CC0 for every `Other`-licensed record in HSSI, most of which are not CC0. The URI is
therefore unrepresentable in the stored metadata and is carried in this file instead. This is the
reason `Other` is right for this record, and the reason it must not be "improved" to a named
Creative Commons row — the only Creative Commons row on offer is CC-BY 4.0, which is precisely the
claim shown above to be wrong.

**Follow-up worth carrying forward, in two directions.** First, the upstream inconsistency is real
and only the author can fix it: the Zenodo deposit should be edited to CC0-1.0 to match the archived
LICENSE file. Second, if HSSI ever adds a CC0 row, this record should move to it. Until then,
`Other` is correct and should not be "improved" back to a named Creative Commons row.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- space weather
- geomagnetic forecasting
- coronal mass ejections
- geomagnetic storms
- magnetohydrodynamics
- magnetosphere
- magnetosphere-ionosphere coupling
- ionosphere
- thermosphere
- auroral electrojet
- solar wind
- dst index
- ae index
- coordinate transformation
- coupled model
- dynamic time warping
- euhforia
- openggcm
- geoeffectiveness

The field was empty. Values are written in their normalized stored (lower-case) identity, not the
Title Case HSSI renders them in.

Keywords is HSSI's only open vocabulary, so an unmatched value silently mints a permanent new row
and near-duplicates accumulate. Fourteen of the nineteen above **already exist** as HSSI rows and
are reused exactly rather than retyped, so no near-duplicate is minted: `space weather`, `geomagnetic
forecasting`, `coronal mass ejections`, `magnetohydrodynamics`, `magnetosphere`,
`magnetosphere-ionosphere coupling`, `ionosphere`, `thermosphere`, `auroral electrojet`,
`solar wind`, `dst index`, `ae index`, `coordinate transformation`, `coupled model`.

Five are genuinely new and are worth minting because no existing row covers them:
`geomagnetic storms`, `dynamic time warping`, `euhforia`, `openggcm`, `geoeffectiveness`. Of those,
`euhforia`, `openggcm` and `dynamic time warping` name the two models and the distinctive analysis
technique — the terms a searcher looking for this specific software would actually type.
`geoeffectiveness` is the paper's own framing of what the coupled model is for, and
`geomagnetic storms` names the phenomenon the runs target; it is carried as a keyword as well as a
Field 22 phenomenon because no existing keyword row covers it.

**Near-duplicates avoided, so they are not re-added later:** HSSI carries both `ae index` and
`ae-index` as separate rows; the spaced form was chosen and the hyphenated one left alone.
`coronal mass ejections` was chosen over the existing bare `cme` row, and `magnetohydrodynamics`
over the existing `MHD` row, to avoid listing the same concept twice. `python` exists and was
deliberately skipped — Field 13 states the language precisely, and the keyword adds nothing.
`ring current` and `substorms` were considered; both are real aspects of the RCM-enabled runs but
neither is a subject the code addresses directly, so they were left out.

### 17. Data Sources (OPTIONAL)
- CDAWeb
- OMNIWeb
- Observatory/Mission-specific

The field was empty.

- **CDAWeb** — the geomagnetic-index files are named for their origin
  (`OMNI_HRO2_5MIN_222347_20120710-20120720_CDAWeb.txt`,
  `OMNI_HRO2_5MIN_254394_20170901_20170915.txt`) and `paper_openggcm_loop.py` cites the service in
  comments at lines 219-220: `#Description: https://cdaweb.gsfc.nasa.gov/misc/NotesO.html` and
  `#Data source: https://cdaweb.gsfc.nasa.gov/cgi-bin/eval2.cgi`.
- **OMNIWeb** — the `.lst` + `.fmt` file pairs (`wind_min_20120712_20120722.lst/.fmt`,
  `omni2_hr_20120710-20120724_F10.lst/.fmt`, `wind_min_merge_20170905_20170915.lst/.fmt`) are the
  characteristic output of the OMNIWeb FTPBrowser subsetting service, and the code parses their
  fixed column layout directly (`paper_openggcm_loop.py` lines 134-196). The paper cites
  https://omniweb.gsfc.nasa.gov/ for the same data.
- **Observatory/Mission-specific** — Wind spacecraft data drives one of the four shipped runs
  (`SWMON wi` in `Event1/Event1-obs/runme`) and is committed as the `wi.*` input files. Field 17's
  own instruction is to select this value and name the mission in Field 32, which is done.

**Considered and rejected:**
- `WDC` — the World Data Center in Kyoto is the ultimate origin of the Dst/SYM-H and auroral
  indices, the paper cites https://wdc.kugi.kyoto-u.ac.jp/wdc/Sec3.html, and
  `paper_openggcm_loop.py` even names its plotting switch `kyoto` (line 43). But that switch plots
  values read out of the OMNI CDAWeb file (lines 227-247); the software never touches a WDC service.
  Listing it would misdescribe where the code actually gets its data.
- `HTTP/HTTPS Directories` and `FTP/FTPS Directories` — there is no download code of any kind. Every
  external file was fetched by hand and committed.
- `HAPI`, `SSCWeb`, `AMDA`, `Madrigal`, `VirES`, `das2`, `The Virtual Solar Observatory.`,
  `S3/Cloud-aware`, `GFZ`, `TAP` — no trace in the repository.

### 18. Input File Formats (RECOMMENDED)
- ascii
- Other

The field was empty. **Every external input this software reads is plain text**, without exception:
- `hsphere_Earth.dsv` — space-delimited EUHFORIA output with a one-line header, read with
  `np.loadtxt(..., delimiter=' ', skiprows=1)` (`euhforia_heeq2gse.py` lines 53-54).
- `.lst` OMNIWeb listings and `_CDAWeb.txt` index files, read with `np.loadtxt` at fixed column
  offsets (`paper_openggcm_loop.py` lines 139, 151, 181, 227-229).
- OpenGGCM per-variable input tables (`euh.bxgse`, `wi.np`, `omni.temp`, ...) — seven whitespace-
  separated columns of date parts plus a value.
- OpenGGCM output tables `dst.txt`, `ae.txt`, `al.txt`, `au.txt`.

**`Other` covers the Python pickle files.** `DTW_correct_paper_2023.py` loads `t_dst.pkl` and
`t_ae.pkl` through `cPickle` (lines 13 and 59-64). Pickle is a binary format with no row in HSSI's
11-value `FileFormat` vocabulary, so `Other` is the only available representation.

**Rejected:** `csv` — `euhforia_heeq2gse.py` imports the `csv` module (line 13) but never calls it;
the `.dsv` files are space-delimited and are parsed by `np.loadtxt`, not by a CSV reader.
`CDF` — the CDAWeb data was converted to ASCII by the subsetting service before it reached the
repository; no CDF reader is present. `FITS`, `HDF5`, `netCDF3/4`, `JSON`, `Zarr`, `IDL.sav`,
`ISTP-Compliant` — absent.

### 19. Output File Formats (RECOMMENDED)
- ascii
- Other

The field was empty.

- **ascii** — `euhforia_heeq2gse.py` writes the headed text file `euh_10min_gse.txt` (lines 68-123),
  and `satfilter_euh.py` writes twenty-one formatted ASCII tables (lines 112-177). These are the
  repository's primary products, and copies of them are committed under `Event1/` and `Event2/`.
- **Other** — two output kinds have no vocabulary row. `paper_openggcm_loop.py` writes binary Python
  pickles `t_dst.pkl` and `t_ae.pkl` with `pickle.HIGHEST_PROTOCOL` (lines 729-742), and both
  plotting scripts export figures as PDF and PNG (`paper_openggcm_loop.py` lines 777-779;
  `DTW_correct_paper_2023.py` lines 115-117 and 260-262).

Only the reachable exports are cited. `DTW_correct_paper_2023.py` contains two further PNG exports,
at lines 326-328 and 364-366, but both sit in the histogram sections that follow the unconditional
`quit()` at line 263 and can never execute — the same dead-code caveat recorded under Field 4. PNG
is a genuine output of this software regardless, on the strength of the two reachable calls, so the
value is unaffected.

### 20. Operating System (RECOMMENDED)
- Linux

The field was empty. There is no CI configuration, no packaging metadata and no installation
documentation, so this is inferred from what the software actually requires to run:

- The `runme` files are Bash (`#!/usr/bin/env bash`) and invoke `$OPENGGCMDIR/bin/script.runme`.
- They configure a POSIX MPI Fortran/C toolchain (`gfortran`, `mpif77`, `mpif90`, `mpicc`, `mpicxx`)
  and target a named Linux HPC cluster (`TARGET marvin_anu` — the Cray CS500 "Marvin" at the
  University of New Hampshire, per the paper's acknowledgments).
- Every hard-coded path in the code and in the committed OpenGGCM logs is a Linux home directory
  (`/home/u0141347/...`).

`Mac` was considered. The four Python scripts contain nothing macOS-hostile and would very likely run
there given a Python 2.7 environment, but the OpenGGCM half of the workflow would not, and no
evidence in the repository shows it was ever tried. Claiming it would be a guess.
`Windows` is excluded — the Bash scripts and MPI toolchain rule it out.
`Operating System Independent` is excluded for the same reason: the workflow as a whole is not
portable, even though the plotting scripts in isolation are close to it.

### 21. CPU Architecture (RECOMMENDED)
- HPC or HEC

The field was empty. The shipped `runme` files are HPC batch and build configuration, not desktop
scripts: they set a 13x6 MPI domain decomposition (`NPX 13`, `NPY 6`), a 200-hour wallclock request
(`RUNTIME 200:00:00`), a batch class, an MPI compiler chain, and a remote cluster target and
username (`TARGET marvin_anu`, `TUSER anwesham`). Reproducing this work requires a supercomputer
allocation, which is exactly what `HPC or HEC` tells a searcher.

`x86-64` was considered and not selected. The target cluster is a Cray CS500, which is x86-64, but
that is a fact about one particular machine the authors used rather than a requirement the software
imposes — nothing here is architecture-specific. `CPU Independent` was rejected as contradicting
`HPC or HEC`: it would suggest the workflow runs anywhere, which the OpenGGCM half does not.

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections
- Geomagnetic Storms
- Solar Wind

The field was empty. The `Phenomena` vocabulary is closed, so a phenomenon with no row in it has to
be carried as a keyword instead.

- **Coronal Mass Ejections** — both shipped events are CMEs, modelled in EUHFORIA with the spheromak
  flux-rope model, and `paper_openggcm_loop.py` hard-codes each event's shock and magnetic-cloud
  boundary times for annotation (lines 320-331).
- **Geomagnetic Storms** — the entire purpose is predicting storm-time Dst and the auroral indices.
  Both events produced major storms; the code reads, corrects, plots and DTW-compares the storm-time
  Dst curves.
- **Solar Wind** — solar wind and IMF conditions are the model's driving input in every
  configuration, and the first three panels of the main figure are solar-wind quantities.

**Rejected:** `Solar Flares` — the September 2017 event was associated with an X9.3 flare and the
paper mentions it as context, but the software neither models nor analyses flares.
`Solar Corona` and `Coronal Heating` — EUHFORIA's coronal model is not used here; the input begins at
the heliospheric output already extracted at Earth. `X-ray emission` — absent.

### 23. Development Status (RECOMMENDED)
**Inactive**

The field was empty. The evidence is unusually clear-cut:

- Seven commits total, all between 2023-12-14 and 2023-12-19. Nothing since — two and a half years
  at the time of writing.
- One release and one tag, `v1.0.0`, at the pinned revision, with a minted DOI.
- Zero stars, forks, open issues and pull requests; no wiki content; no CI, no tests, no packaging.
- Written for Python 2.7, which reached end of life in 2020, and importing a SciPy module
  (`scipy.ndimage.filters`) that has since been removed.
- The repository is *not* flagged as archived on GitHub.

`Inactive` is the repostatus.org term for software that reached a stable, usable state and is no
longer actively developed. That is exactly this: a tagged, citable, complete artifact accompanying a
published paper.

**Alternatives weighed:** `Abandoned` requires that there be no stable release, and there is one, so
it does not apply. `Unsupported` additionally requires that the authors have ceased work *and want a
new maintainer* — there is no statement to that effect anywhere, and inventing one would be a guess.
`Concept` is wrong for released, DOI-minted, published-with software. `Active` is contradicted by
the commit history. `Moved` would need a successor location, and none exists.

This value is stable in a specific sense worth recording: for an archival paper supplement,
`Inactive` is the *expected* end state, not a sign of neglect, and a future refresh should not read
continued inactivity as a reason to downgrade it.

### 24. Documentation (RECOMMENDED)
**https://github.com/anweshaM/EUHFORIA-OpenGGCM/blob/main/readme**

The field was empty. There is no documentation site, no `docs/` directory, no Read the Docs
configuration, and the GitHub wiki is empty. The only documentation is the 32-line file named
`readme` (no extension) at the repository root, which GitHub renders on the repository home page. It
is genuinely a usage document rather than a description: it gives the two-step conversion procedure
(`euhforia_heeq2gse.py` then `satfilter_euh.py`), explains the layout of the `Event1` and `Event2`
directories, and maps each script to the paper figures it produces.

A direct link to the file is used rather than the repository root so that Field 24 points at
documentation specifically, rather than repeating Field 3.

**Considered and rejected:** https://openggcm.sr.unh.edu/?n=Main.Inputs, cited inside
`satfilter_euh.py` at line 12. It documents OpenGGCM's input format, which is genuinely necessary
background for using this software, but it is another project's documentation and does not describe
this one. It is recorded here so its relevance is not lost.

### 25. Funder (OPTIONAL)

1. **KU Leuven** — https://ror.org/05f950310
2. **Research Foundation - Flanders** — https://ror.org/03qtxy027
3. **European Space Agency** — https://ror.org/03wd9za21
4. **Belgian Federal Science Policy Office** — https://ror.org/01fapfv42
5. **Oak Ridge Associated Universities** — https://ror.org/0526p1y61
6. **U.S. National Science Foundation** — https://ror.org/021nxhr62
7. **United States Air Force Office of Scientific Research** — https://ror.org/011e9bt93
8. **National Aeronautics and Space Administration** — https://ror.org/027ka1x80

The field was empty. All eight are taken from the Acknowledgments of the accompanying paper, which
is the authoritative funding statement for the work that produced this code, and six of the eight are
independently corroborated by the publisher-asserted funding metadata Crossref carries for the DOI.
Two — the Research Foundation - Flanders and the European Space Agency — appear in the
Acknowledgments but are **absent from Crossref**, so an extraction that consulted only Crossref
would miss them.

Every ROR was verified against the ROR registry. Names are recorded in the expanded, acronym-free
form Field 25 requires, and where HSSI already has a matching organization the existing spelling is
reused exactly so no duplicate row is created — this applies to `European Space Agency`,
`U.S. National Science Foundation`, `United States Air Force Office of Scientific Research` and
`National Aeronautics and Space Administration`. Expansions applied: BELSPO to
`Belgian Federal Science Policy Office`, FWO-Vlaanderen to `Research Foundation - Flanders`, NSF to
`U.S. National Science Foundation`, AFOSR to `United States Air Force Office of Scientific
Research`, NASA to `National Aeronautics and Space Administration`, ORAU to
`Oak Ridge Associated Universities`, ESA to `European Space Agency`.

`KU Leuven` is left in that form for the reason given in Field 6: it is the institution's official
English name and ROR display name, with `Katholieke Universiteit Leuven` as the expanded alternative.

**Scope caveat, recorded deliberately.** No grant funded this repository as a software project. These
bodies funded the *research* the code implements, and the code is that research's published
supplement. Recording them is the standard and useful reading of Field 25, but a curator who reads
the field strictly as "funding for the software artifact" would leave it empty. The evidence is laid
out here so that judgement can be made without re-reading the paper.

### 26. Award Title (OPTIONAL)

| Award Title | Award Number | In this record |
|---|---|---|
| C1 project Internal Funds KU Leuven | C14/19/089 | recorded |
| WEAVE | G.0025.23N | recorded |
| SIDC Data Exploitation | PRODEX-12 | recorded |
| SWiM | B2/191/P1/SWiM | recorded |
| Major Research Instrumentation | AGS-1919310 | recorded |
| *(no title stated)* | FA9550-18-1-0483 | not expressible in HSSI |
| *(no title stated)* | 80NSSC18K1220 | not expressible in HSSI |
| NASA Postdoctoral Program | *(no number stated)* | recorded |

The field was empty. Taken verbatim from the paper's Acknowledgments, which reads: *"A.M.
acknowledges support from the projects C14/19/089 (C1 project Internal Funds KU Leuven),
G.0025.23N (WEAVE FWO-Vlaanderen), SIDC Data Exploitation (ESA Prodex-12), and Belspo project
B2/191/P1/SWiM. E.S. research was supported by an appointment to the NASA Postdoctoral Program at
the NASA Goddard Space Flight Center, administered by Oak Ridge Associated Universities under
contract with NASA. Computations were performed on Marvin, a Cray CS500 supercomputer at UNH
supported by the NSF MRI program under grant AGS-1919310. The research at UNH was supported by the
Air Force Office of Scientific Research (grant no. FA9550-18-1-0483) and NASA (grant no.
80NSSC18K1220)."*

Three points a future refresh should not have to rediscover:

- **Award numbers are recorded with ASCII hyphens.** Crossref renders `AGS-1919310` and
  `FA9550-18-1-0483` with Unicode hyphens (U+2010), and the paper's PDF text layer additionally
  breaks `FA9550` as `F A9550`. Both are typesetting artifacts of the source, not part of the
  identifiers.
- **Two awards have no stated title, and HSSI has no way to express them.** The Acknowledgments give
  only grant numbers for AFOSR `FA9550-18-1-0483` and NASA `80NSSC18K1220`. HSSI normalizes an
  award's *name* when it creates one and rejects a blank name outright, so an award that has a
  number but no title has no representable form at all: six of the eight above are held in this
  record and these two are not. Two ways of forcing them in were weighed and rejected. Inventing a
  plausible project title would be fabrication — the paper states none, and no other source gives
  one. Reusing the grant number as the award title would follow a convention no existing HSSI Award
  row uses, and would leave a row whose name is not a name. The loss is contained: both funders, the
  United States Air Force Office of Scientific Research and the National Aeronautics and Space
  Administration, are recorded in Field 25, so the funding attribution survives and only the two
  bare grant numbers go unrepresented. The table above stays complete at eight entries because it is
  the authoritative record of what the Acknowledgments say, independent of what HSSI can hold.
- **`SIDC Data Exploitation` / `PRODEX-12` is the weakest entry.** The Acknowledgments write it as
  "SIDC Data Exploitation (ESA Prodex-12)", which names an ESA PRODEX programme contract rather than
  a numbered award in the usual sense. It is recorded as written; a curator may reasonably drop the
  number.

All titles are far below the 128-character limit that applies to award names, and no value here is
near any length boundary.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

1. **https://doi.org/10.1051/swsc/2018020** — Pomoell & Poedts (2018), *EUHFORIA: European
   heliospheric forecasting information asset*, J. Space Weather Space Clim. 8, A35.
2. **https://doi.org/10.1029/98JA00014** — Raeder, Berchem & Ashour-Abdalla (1998), *The Geospace
   Environment Modeling Grand Challenge: Results from a Global Geospace Circulation Model*, JGR
   103(A7), 14787-14798.
3. **https://doi.org/10.1002/2017JA024104** — Cramer, Raeder, Toffoletto, Gilson & Hu (2017),
   *Plasma sheet injections into the inner magnetosphere: Two-way coupled OpenGGCM-RCM model
   results*, JGR Space Physics 122(5), 5077-5091.
4. **https://doi.org/10.3389/fspas.2020.00039** — Laperre, Amaya & Lapenta (2020), *Dynamic Time
   Warping as a New Evaluation for Dst Forecast with Machine Learning*, Front. Astron. Space Sci. 7,
   39.
5. **https://doi.org/10.3847/1538-4357/ac4af6** — Samara et al. (2022), *Dynamic Time Warping as a
   Means of Assessing Solar Wind Time Series*, ApJ 927(2), 187.

Entries 1 to 3 are not arbitrary additions: they are precisely the references the authors themselves
designate in the paper's Open Data Statement for the model versions this code bridges — *"The
EUHFORIA (ver 2.0, Pomoell and Poedts (2018)) simulations ... The OpenGGCM (v5.0.ccmc, Raeder et al.
(1998); Cramer et al. (2017)) simulations ..."*. Cramer et al. (2017) is the OpenGGCM-RCM two-way
coupling paper, which is directly exercised by the shipped configurations (`RCMCODE rice`) and by the
RCM columns the code reads out of `dst.txt` (`paper_openggcm_loop.py` lines 268-271). The EUHFORIA
version is corroborated in the code itself: `euhforia_heeq2gse.py` line 24 states
`# Input: EUHFORIA (v2.0) data at Earth`.

Entries 4 and 5 are the published basis of `DTW_correct_paper_2023.py`; the paper introduces the
technique with *"This method has been adopted in the space weather community for comparing solar
wind characteristics (Samara et al., 2022) and Dst index as well (Laperre et al., 2020)."* Samara is
also a co-author of the accompanying paper.

**Considered and not selected:** Górecki & Łuczak (2013) and Keogh & Pazzani (2001), which the paper
cites for dynamic time warping as a general algorithm. They are computer-science method papers with
no heliophysics or software-specific connection to this record, and listing them would dilute the
field.

#### The reference publication was removed from this field

**https://doi.org/10.1029/2023SW003715** — Maharana et al. (2024), *Employing the Coupled
EUHFORIA-OpenGGCM Model to Predict CME Geoeffectiveness*, Space Weather 22(5) — **was previously
stored in this field and is deliberately no longer listed here.** It is the reference publication
for this software, and it is now recorded in Field 14, which is its correct home by definition.

This is an intentional removal of a previously stored HSSI value, not an omission. Field 27's own
definition is explicitly for publications *"different from the reference publication"*, so a DOI
that *is* the reference publication cannot also be a Related Publication without the record
contradicting the field it sits in. The five entries above satisfy that definition; this one never
did.

**Keeping it in both fields was considered and rejected.** The argument for it is redundancy in
search — a query matching either field would surface the paper. It was rejected because the same
publication would then be asserted twice under mutually exclusive definitions, and because Field 14
already carries and exposes it, so the duplicate buys nothing a searcher does not already get. A
future refresh should not re-add it here; finding it absent from Field 27 while present in Field 14
is the intended state.

### 28. Related Datasets (OPTIONAL)

1. **https://hpde.io/NASA/NumericalData/OMNI/HighResolutionObservations/Version2/PT5M** — OMNI
   Combined, Definitive 5-minute IMF, Plasma and Energetic Proton Fluxes (CDAWeb `OMNI_HRO2_5MIN`).
2. **https://hpde.io/NASA/NumericalData/OMNI/PT1H** — OMNI Combined, Definitive Hourly IMF and
   Plasma Data (CDAWeb `OMNI2_H0_MRG1HR`).
3. **https://omniweb.gsfc.nasa.gov/ftpbrowser/wind_min_merge.html** — SW Magnetic Field, Plasma and
   Trajectory Data from Wind, 1-minute merged (NASA Space Physics Data Facility).

The field was empty. These are the three external datasets the code actually reads, and each is
matched to specific code:

- The 5-minute OMNI product supplies the observed AE, AL, AU and SYM-H indices that every model
  curve is compared against; `paper_openggcm_loop.py` parses it at fixed columns with
  `skiprows=93` (lines 221-247), and the committed filenames carry the `OMNI_HRO2_5MIN` dataset name.
- The hourly OMNI2 product supplies the F10.7 solar flux the code interpolates onto the model grid
  (lines 178-197); the committed files are named `omni2_hr_..._F10.lst`.
- The Wind 1-minute merged product supplies the solar-wind driver for `Event1-obs`; the committed
  `.fmt` describes exactly its column set (`BX/BY/BZ GSE`, `KP_Speed`, `KP_Vx/Vy/Vz`,
  `Kp_proton Density`, `Kp_temperature`), and the filenames `wind_min_20120712_20120722.lst` and
  `wind_min_merge_20170905_20170915.lst` name the service.

The first two identifiers are the canonical SPASE landing pages, obtained from CDAWeb's own dataset
descriptions (`spase://NASA/NumericalData/OMNI/HighResolutionObservations/Version2/PT5M` and
`spase://NASA/NumericalData/OMNI/PT1H`) rather than guessed from the URL pattern — worth noting,
because hpde.io serves a client-rendered stub for *every* path, valid or not, so a URL there cannot
be validated by fetching it. The Wind merged product is an SPDF-derived listing service with no
dataset DOI and no single SPASE record; Field 28 explicitly permits a permanent link in that case.

### 29. Related Software (OPTIONAL)
**Not found.**

This is a deliberate empty, not an omission. The two pieces of software that matter here — EUHFORIA
and OpenGGCM — are recorded in Field 30 instead, and the reasoning is worth preserving because the
opposite choice looks equally plausible at first glance.

Field 29 is for software that *"performs similar tasks but does not necessarily link together (which
would be 'interoperable software')"*. EUHFORIA and OpenGGCM do link together, and this repository is
the thing that links them: it converts one's output into the other's input. That routes them to
Field 30 by Field 29's own parenthetical. Listing them in both would say the same thing twice.

Nothing else qualifies. The repository has no dependency manifest; the only imports are NumPy, SciPy,
Matplotlib, pandas and the standard library, all of which are generic scientific-Python
infrastructure that is equally at home in a web application or a finance model, and all of which are
excluded from both fields by rule. `compute_dst`, imported at `paper_openggcm_loop.py` line 32, is
**not present in this repository** and is not published anywhere identifiable — it is a missing local
module, so there is nothing to link to. There is no predecessor project and no fork parent: the
history begins with an initial commit five days before release.

#### The dependency reading was weighed and rejected

Field 29 also invites *"important software dependencies"*, and EUHFORIA and OpenGGCM are as important
as dependencies get — without both, nothing in this repository can be run. On that clause alone they
would belong here as well as in Field 30, and the argument is strong enough to be recorded rather
than waved away.

It does not carry, because the clause does not stand on its own. Field 29's definition scopes the
whole field to software that *"performs similar tasks but does not necessarily link together (which
would be 'interoperable software')"* — and linking EUHFORIA and OpenGGCM together is exactly and
only what this repository does. The parenthetical routes precisely this case to Field 30, which is
therefore their correct and their sole home. Listing them in both fields would assert the same
relationship twice, once under a definition that excludes it.

### 30. Interoperable Software (OPTIONAL)

1. **https://openggcm.sr.unh.edu/** — OpenGGCM (Open Geospace General Circulation Model),
   University of New Hampshire.
2. **https://ccmc.gsfc.nasa.gov/models/EUHFORIA~1.0.4/** — EUHFORIA (EUropean Heliospheric
   FORecasting Information Asset).

The field was empty. Both entries clear the demonstrated-exchange bar by a wide margin — this
software *is* the exchange:

- **OpenGGCM.** The repository writes OpenGGCM's input format directly. `satfilter_euh.py` produces
  the twenty-one per-variable files OpenGGCM reads, against the documented input specification it
  cites at line 12 (`https://openggcm.sr.unh.edu/?n=Main.Inputs`), and ships four complete OpenGGCM
  run configurations. It then reads OpenGGCM's output back — `dst.txt`, `ae.txt`, `al.txt`, `au.txt`
  — at specific column offsets (`get_og_dst` and `get_og_ae`, `paper_openggcm_loop.py` lines
  265-308). That is a bidirectional, format-level exchange with a named domain tool.
- **EUHFORIA.** `euhforia_heeq2gse.py` reads EUHFORIA's `.dsv` heliospheric output against its
  documented column layout, which line 51 spells out in full as
  `#date r[AU] clt[rad] lon[rad] n[1/cm^3] P[Pa] vr[km/s] vclt[km/s] vlon[km/s] Br[nT] Bclt[nT] Blon[nT]`,
  and converts it into the intermediate GSE form the OpenGGCM writer consumes. The banner printed at
  line 29 states the intent exactly: *"The converted file format is good for OpenGGCM runs"*.

**On the identifiers.** Neither model has a public source repository or a software DOI, so Field 30's
fallback applies: a link where users can find more information. For OpenGGCM, the UNH project site
is chosen over the CCMC model page because it is the URL the repository itself cites. For EUHFORIA,
the CCMC model page is used because the model has no public code repository and its own domains do
not currently resolve — `euhforia.com` returns a server error and `euhforiaonline.com`, the run
portal named in the paper's Open Data Statement, does not resolve in DNS at all. That is recorded as
negative research: a future refresh should not spend time re-testing those two hosts, and should
switch to a project-owned URL only if one comes back up.

**Excluded, with reasons:** NumPy, SciPy, Matplotlib and pandas are imported throughout but are
generic infrastructure — being a dependency is not interoperability, and the same claim would be true
of nearly every package in HSSI. The Rice Convection Model and CTIM are configured in the `runme`
files but are internal components *of* OpenGGCM rather than separate packages this software exchanges
data with; listing them would double-count OpenGGCM.

### 31. Related Instruments (OPTIONAL)
**Not found — no instrument-level association is defensible, and one was deliberately not invented.**

The software genuinely consumes Wind spacecraft measurements, so the question is real rather than
academic. It resolves to the observatory level, in Field 32, for a specific reason worth recording:

**The repository never names an instrument.** It names a *spacecraft* — `SWMON wi` in
`Event1/Event1-obs/runme` — and it reads a pre-merged, multi-instrument listing product. The `.fmt`
file describes generic column labels (`BX, GSE, nT`, `KP_Speed, km/s`, `Kp_proton Density, n/cc`)
with no instrument attribution anywhere.

Externally, NASA's SPDF documents that the `wind_min_merge` product it read is built from Wind MFI
15-second magnetic field data, Wind SWE 92-second plasma data (definitive and key parameter), and
Wind 3DP parameters. HSSI's controlled vocabulary does contain the corresponding rows
(`https://spase-metadata.org/SMWG/Instrument/Wind/MFI`,
`https://spase-metadata.org/SMWG/Instrument/Wind/SWE`,
`https://spase-metadata.org/SMWG/Instrument/Wind/3DP`), so they *could* be emitted.

They are not, because doing so would be inference rather than evidence. Nothing in this repository
selects among those instruments or shows awareness of them; the software supports the merged product,
not any one instrument's data. The correct resolution is the platform-level association already
recorded in Field 32. The three candidate identifiers are written out above so that a future agent
who reaches the opposite conclusion does not have to re-derive them — but the default should remain
"observatory only".

**Also considered and excluded:**
- **DMSP.** The `runme` files reference `CTIM_F_DMSP` and `CTIM_F_DMSPMOD` input tables. These are
  CTIM's internal empirical precipitation model files, distributed with OpenGGCM. The software does
  not read DMSP data.
- **ACE, IMP-8, Geotail.** The `SWMON` line's inline comment lists OpenGGCM's generic driver options
  as `(wi/ac/i8/ge/fi)`. Only `wi`, `omni` and `euh` are ever actually used. A list of options a
  framework supports is not an association this software has.
- **Ground magnetometer networks.** The Dst, SYM-H, AE, AL and AU indices ultimately derive from
  magnetometer stations, and the paper discusses SuperMAG as an alternative index source. The
  software reads the finished indices from OMNI files and never touches station data. No specific
  station or network is named.

### 32. Related Observatories (OPTIONAL)

1. **ISTP/Wind** — https://spase-metadata.org/SMWG/Observatory/Wind
2. **OMNI** — https://spase-metadata.org/SMWG/Observatory/OMNI

The field was empty. Both names are copied verbatim from HSSI's controlled vocabulary and both carry
a `https://spase-metadata.org/` identifier. That pairing is what matters here: a name recorded
without its SPASE identifier either binds to an arbitrary same-name row or mints a new
identifier-less one, and this vocabulary is entirely SPASE-backed, with no identifier-less rows to
fall back on.

**Wind.** The software directly supports Wind data as an OpenGGCM driver:
`Event1/Event1-obs/runme` sets `SWMON wi`, the repository commits fifteen `wi.*` input files
(`wi.bxgse`, `wi.vxgse`, `wi.np`, `wi.temp`, ...), and `paper_openggcm_loop.py` parses the Wind
listing's fixed column layout to plot the observed solar wind (lines 111-172). The paper's Event 1
analysis states the choice explicitly: *"we found that Wind had the best data, i.e., without any gaps
or anomaly."* A user searching HSSI for software that works with Wind data should find this.

**OMNI.** The software reads OMNI-specific products with hard-coded, format-specific parsers — the
5-minute HRO2 index file at `skiprows=93` and fixed columns (lines 221-247), the hourly OMNI2 F10.7
listing (lines 178-197) — and `Event2/Event2-obs/runme` drives OpenGGCM from OMNI directly with
`SWMON omni`, backed by fourteen committed `omni.*` input files. SPASE models OMNI as an observatory
in its own right, which is why a row exists to resolve against.

**On OMNI's placement.** OMNI is a merged multi-mission derived dataset, and there is a real argument
that a multi-mission data source belongs only in Field 17 (Data Sources), where `OMNIWeb` and
`CDAWeb` are already recorded. It is listed here as well because SPASE grants OMNI observatory
identity with its own canonical record, because the software implements OMNI-specific file formats
rather than merely fetching from an archive, and because `SWMON omni` makes it a first-class driver
on equal footing with Wind. The archive/service aspect and the data-product aspect are genuinely
different things, and Fields 17 and 32 capture them separately.

**On duplicate rows.** Both entities collide with multiple vocabulary rows, and both collisions were
resolved rather than flagged, because in each case the alternatives are the same entity registered by
a second authority. Wind matches `SMWG/Observatory/Wind` (name `ISTP/Wind`),
`CNES/Observatory/CDPP-Archive/Wind` (name `Wind`) and `CNES/Observatory/CDPP-AMDA/Wind` (name
`NASA Mission`, evidently a placeholder). OMNI matches `SMWG/Observatory/OMNI` and
`CNES/Observatory/CDPP-AMDA/OMNI`. The SMWG registration is canonical in both cases, so the SMWG row
is used. Note that the canonical Wind name is `ISTP/Wind`, not `Wind` — copied verbatim rather than
re-derived, since the plainer-looking `Wind` belongs to a different row.

### 33. Logo (OPTIONAL)
**Not found.**

There is no logo. The repository contains no image files of any kind, no `logo`, `icon`, `assets` or
`docs` directory, no badge in the `readme`, and no project website. Neither the Zenodo deposit nor
the GitHub repository carries one. As an archival paper supplement rather than a branded project,
this software is unlikely ever to acquire one, so a future refresh need not go looking.
