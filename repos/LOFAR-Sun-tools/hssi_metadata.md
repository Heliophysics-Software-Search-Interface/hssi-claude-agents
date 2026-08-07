# HSSI Metadata Extraction Results

**HSSI Software ID:** 80c6de8f-a5f2-4897-9ca8-593d8a126590
**Repository:** https://github.com/peijin94/LOFAR-Sun-tools
**Source Revision:** f44502475496d46a6cde17b9881aa19d852debfb
**Extraction Date:** 2026-08-06
**Validation Date:** 2026-08-07
**Validation Status:** PASS

---

**Scope note — read this before using the evidence below.** `lofarSun` is distributed as a small
installable Python package (`lofarSun/`, three modules) shipped inside a larger repository that also
carries an unpackaged `utils/` tree (SLURM job scripts, LINC/CWL calibration and imaging workflows),
a `demo/` notebook set, a Sphinx `docs/` tree, and an unsubmitted JOSS paper draft. `setuptools.find_packages()`
picks up only `lofarSun/*`, so `utils/` is **not** installed by `pip install lofarSun`. Several field
values below rest on evidence from `utils/` and `docs/` rather than from the importable package; where
that distinction matters to the value it is called out in the field note. The repository is also
mirrored on ASTRON's GitLab at `https://git.astron.nl/ssw-ksp/lofar-sun-tools` (named in `docs/install.rst`
as the source of the development version; the URL resolves), but GitHub remains the canonical Field 3
value because it is what `setup.py`, PyHC and the published documentation point at.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

Stored separately as write-once HSSI submission provenance; partial metadata updates do not rewrite
it. The placeholders remain because this dossier does not reproduce submitter contact details.

### 2. Persistent Identifier (RECOMMENDED)

**Value:** https://doi.org/10.5281/zenodo.4495450

This is the Zenodo **concept DOI** (all-versions DOI) for this software. The deposit was made under
the repository's former name, `Pjer-zhang/LOFAR_Solar` — Zenodo record 4495451, titled
"Pjer-zhang/LOFAR_Solar: Lofar-sun-tools-v0.1.0", published 2021-02-02, `conceptrecid` 4495450,
`resource_type` `software`. Identity with the present repository is proven rather than assumed:
`https://api.github.com/repos/Pjer-zhang/LOFAR_Solar` returns a permanent redirect to
`peijin94/LOFAR-Sun-tools`, and both names carry the same GitHub numeric repository id `190693593`.
DataCite confirms the concept record's `HasVersion` relation to `10.5281/zenodo.4495451` and its
`IsSupplementTo` relation to `https://github.com/Pjer-zhang/LOFAR_Solar/tree/v0.1.0`.

Known limitations of this identifier, recorded so a future agent does not mistake them for an error:
the GitHub–Zenodo integration was evidently used once and then abandoned, so the concept DOI has
exactly one version under it (v0.1.0, 2021) and its title still carries the old repository name. It is
nevertheless the correct Field 2 value — Field 2 asks for the concept DOI for all versions, and a
concept DOI remains the software's persistent identifier regardless of how many versions have been
deposited beneath it.

**Rejected: `https://doi.org/10.48550/arXiv.2205.00065`.** The prior canonical file put this arXiv
publication DOI in Field 2 while itself noting it "is for a related publication, not the software
itself." It identifies a journal article, not the software, and it is already carried correctly in
Field 14. It should not be reinstated here now that a genuine software DOI has been located.

**Negative research (do not repeat):** a Zenodo full-text search for `lofarSun` does not surface the
deposit; a search for `LOFAR-Sun-tools` does, which is why earlier passes missed it. Crossref has no
software record for this package, and the repository carries no `CITATION.cff`, `codemeta.json`,
`.zenodo.json` or DOI badge. Setting aside the DOIs of cited external papers in `paper.bib`, the only
DOI-shaped string referring to this software itself is the unedited JOSS template line
`#aas-doi: 10.3847/xxxxx` in `paper.md`, which is a placeholder rather than an identifier.

**Bearing on Field 11.** The submission form's guidance would make Zenodo the publisher wherever a DOI
came from the GitHub-Zenodo workflow, and this is such a DOI. Field 11 is nevertheless GitHub; the
reasoning for that choice is recorded there, and the two fields were decided together.

### 3. Code Repository (MANDATORY)

**Value:** https://github.com/peijin94/LOFAR-Sun-tools

Unchanged from the stored HSSI value. Corroborated by `setup.py` (`url=`), the PyHC community registry
(`code:` field), `docs/index.rst`, and the ApJ reference publication, which cites the library by this
exact URL. The ASTRON GitLab mirror (`https://git.astron.nl/ssw-ksp/lofar-sun-tools`) resolves and is
named in `docs/install.rst` as the development-version source, but GitHub is the canonical, publicly
navigable root and is the URL used by `setup.py`, PyHC, `docs/index.rst` and the reference
publication; `docs/install.rst` is the one place that points elsewhere, and only for the nightly
development checkout.

### 4. Software Functionality (MANDATORY)

**Values (26):**
- Coordinate Transforms
- Coordinate Transforms: Solar
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: Spectrogram
- Mission-related
- Mission-related: Analysis
- Mission-related: Calibration
- Mission-related: Instrument Response
- Mission-related: Orchestration
- Mission-related: Processing
- Mission-related: Science Data Processing
- Servers and Environments
- Servers and Environments: High Performance Computing

Every child value listed has its parent listed alongside it. Each value is itemised below with the code
evidence that supports it, grouped by whether the published HSSI record already carried the value or
the repository source is what establishes it.

**Already part of the published record, with the evidence that defends them:**
- `Data Processing and Analysis` — the whole package.
- `Data Processing and Analysis: Analysis` — `IMdata.fit_gaussian2d()`, `BFcube.bf_fit_gauss_source_by_idx()`,
  `bf_peak_size()`, brightness-temperature conversion in `IMdata.load_fits()`/`make_map()`.
- `Data Processing and Analysis: Calibration` — `bftools.proc_calib_dynspec()`, `proc_selfcalib_dynspec()`,
  `get_cal_bandpass()`, `model_flux()`; calibrator-based gain calibration documented in
  `docs/beamformed.rst`, which describes the same procedure without ever using the term "A-team", and
  A-team sky models in `docs/interferometry.rst` (`A-Team_lowres.skymodel`).
- `Data Processing and Analysis: Data Access and Retrieval` — genuinely supported, though the evidence
  lives outside the importable package: `utils/IM/LINC/lincSun/steps/fetch_data.cwl` and
  `fetch_solutions.cwl` retrieve observations from the LOFAR Long Term Archive
  (`wget https://lta-download.lofar.psnc.pl/lofigrid/SRMFifoGet.py?surl=…`), with a
  `workflow/download_data.cwl` driver; `docs/interferometry.rst` documents the LTA download step.
- `Data Processing and Analysis: File Format Conversion` — `lofarSun/cli/h5_to_fits_spec.py`
  (`h5toFitsDS` console script) converts beamformed HDF5 to FITS; `BFdata.load_sav_*()` reads IDL `.sav`
  into arrays that `write_fits()` re-emits.
- `Data Processing and Analysis: Image Processing` — `scipy.ndimage.shift`/`rotate` and
  `gaussian_filter` in `IMdata.sun_coord_trasform()`/`plot_image()`; `bftools.mask_extend_xy_npix()`;
  `scikit-image` in `install_requires`.
- `Data Processing and Analysis: Spectrogram` — dynamic-spectrum construction throughout
  `lofarSun/BF/` and `cli/h5_to_fits_spec.py`.
- `Data Visualization` — matplotlib figure generation across `BFdata`, `IMdata`, `cli`, and the GUI.

**Not in the published record; established from the repository source:**
- `Coordinate Transforms` and `Coordinate Transforms: Solar` — the clearest gap in the stored record.
  `lofarSun/BF/lofarJ2000xySun.py::j2000xy()` converts J2000 RA/DEC to solar x–y arcsecond coordinates
  including the solar position-angle rotation; `IMdata.RA_DEC_shift_xy0()` and
  `IMdata.sun_coord_trasform()` do the same for interferometric images; `IMdata.make_map()` transforms
  a GCRS reference coordinate into `sunpy.coordinates.frames.Helioprojective` with the LOFAR
  `EarthLocation(lat=52.905329712, lon=6.867996528)` as observer. The reference publication describes
  exactly this as the library's role: "We converted the coordinates into Helioprojective coordinates
  and the flux density into brightness temperature using the LOFAR-Sun-tools library." This is
  user-facing, not incidental. Only the `Solar` child applies — there is no heliospheric,
  magnetospheric, ionospheric, planetary or spacecraft-frame transform anywhere in the package.
- `Data Processing and Analysis: Data Reduction` — `bftools.downsample_h5_seg_by_time_ratio()`,
  `averaging_stride()`, `averaging_walk()`, `avg_1d()`, `partition_avg()`,
  `avg_with_lightening_flag()`, and `cli.h5_to_fits_spec.compress_h5()`. `docs/beamformed.rst` states
  the motivation explicitly ("a typical observation … 5.3 TB … To cope with the large data size …
  we can downsample the data to a smaller dimension").
- `Data Processing and Analysis: Processing` — proposed by the prior canonical file and confirmed:
  the `proc_calib_dynspec` / `flag_frequency_slices` / `perform_linear_interpolation` chain and the
  chunked `compress_h5` pipeline are multi-step transformation pipelines rather than single analyses.
- `Data Processing and Analysis: Time Series Analysis` — `bftools.FWHM()`, `DecayExpTime()` (burst
  e-folding decay time), `fit_biGaussian()`/`biGaussian()` ("Derive the best fit curve for the
  flux-time distribution"), plus the time-axis averaging functions and
  `cli/pyms_utils.ms_datetime_to_index()`/`ms_index_to_datetime()`.
- `Data Visualization: 2D Graphics` — `imshow` and `contour` calls in `IMdata.plot_image()`,
  `BFdata.plot_bf_image_by_idx()`, `cli/h5_to_fits_spec.py`, and the GUI.
- `Data Visualization: Line Plots` — `ax.plot()` of Gaussian beam-fit profiles and the fitted centroid
  in `BFdata.bf_fit_gauss_source_by_idx()`, and of the solar limb circle
  (`960*np.sin(np.arange(0, 2*np.pi, 0.001))`) in `BFdata.plot_bf_image_by_idx()`.
- `Data Visualization: Spectrogram` — `BFdata.plot_bf_dyspec()` and the annotated quicklook figure
  written by `compress_h5()`.
- `Data Visualization: Mission-Specific` — the least direct value in this group, and recorded because
  the plots it names are LOFAR-shaped rather than generic: `lofarBFcube`
  (`lofarSun/BF/GUI/lofarBFgui.py`) is a viewer for LOFAR tied-array-beam FITS cubes specifically, and
  `IMdata.plot_image()` and `BFdata.plot_bf_image_by_idx()` overlay the LOFAR synthesized/restoring
  beam ellipse derived from
  `BMAJ`/`BMIN`/`BPA` plus the solar position angle — plot furniture that only makes sense for LOFAR
  interferometric products.
- `Mission-related` (parent) and its children. The prior canonical file listed three `Mission-related`
  children **without** the parent, which would have been rejected on submission; the parent is included
  here. The category applies because `lofarSun` is not a general tool that happens to read LOFAR data —
  `paper.md` states that the LOFAR Solar and Space Weather Key Science Project "aims to develop and
  implement the data processing tools for the solar radio imaging spectroscopy data processing of
  LOFAR," and the development mirror lives under `ssw-ksp/` on ASTRON's GitLab. This is observatory-team
  pipeline software.
  - `Mission-related: Calibration` — the LINC-derived `utils/IM/LINC/lincSun/workflow/calibrator_sun.cwl`,
    `apply_cal.cwl`, `process_calibrator_workflow.cwl`, plus `utils/IM/commandlines/auto_sun_calib.py`,
    which generates and runs DP3/DPPP parsets for the gaincal → applycal → applybeam sequence.
  - `Mission-related: Processing` — `process_target_workflow.cwl`, `prep_avg_autow.cwl`,
    `utils/IM/slurmScripts/autoCalib_job.py` and `clean_job.py`.
  - `Mission-related: Science Data Processing` — the end-to-end path from raw LOFAR Measurement
    Sets / beamformed HDF5 to science-ready calibrated dynamic spectra and brightness-temperature maps.
  - `Mission-related: Analysis` — LOFAR-instrument-aware analysis: `IM.get_peak_beam_from_psf()` and the
    `pymsPSFfitPeakGauss` console script operate on WSClean PSF images of the LOFAR synthesized beam.
  - `Mission-related: Instrument Response` — `docs/beam.rst` documents deriving the restoring-beam
    shape from the instrument PSF (`useMyBeam`), implemented by `get_peak_beam_from_psf()`;
    `bftools.get_cal_bandpass()` derives the instrument bandpass response, and `docs/beamformed.rst`
    names it as such ("get a instrument reponse of the calibrator").
  - `Mission-related: Orchestration` — 8 CWL workflows and 19 CWL step definitions under
    `utils/IM/LINC/lincSun/` that sequence the LOFAR solar calibration and imaging pipeline, driven by
    `linc_run.sh` / `linc_run_slurm.sh`.
- `Servers and Environments` and `Servers and Environments: High Performance Computing` —
  `utils/IM/slurmScripts/` ships SLURM array-job scripts (`sbatch_calib.sh`, `sbatch_clean.sh`,
  `sbatch_cutout.sh`, `sbatch_prepCalib.sh`) that launch Singularity containers on compute clusters,
  with a separate variant tuned for the DISCOVERER supercomputer; `docs/interferometry.rst` gives a
  worked `#SBATCH` recipe for running the lincSun workflow on HPC.

**Considered and rejected — recorded so these are not re-proposed:**
- `Data Processing and Analysis: ML/AI` and `Mission-related: ML/AI`. Tempting because
  `lofarSun/BF/RFIconvFlag.py` subclasses `torch.nn.Module` and stacks `nn.Conv2d` layers, and `torch`
  is in `install_requires`. But `init_RFIconv()` hand-sets every kernel weight from fixed morphological
  templates; nothing is trained, no model is loaded, and there is no inference on learned parameters.
  The method paper (MNRAS 521, 630) describes it as "a novel method that makes use of a morphology
  convolution," explicitly a morphological operator rather than a learned model. PyTorch is used here
  purely as a GPU-capable convolution engine.
- `Models and Simulations` and `Models and Simulations: Empirical`. `bftools.model_flux()` implements
  polynomial spectral flux models for the 19 radio calibrator sources in its `cal_params` dict, with
  coefficients from arXiv:1609.05940. It is a real empirical model, but of astronomical calibrator
  sources consumed inside the calibration step — not a model of any heliophysical system, and not
  offered to users as modelling functionality.
- `Data Visualization: Movies`. `docs/beam.rst` embeds `img/testb.gif` showing beam rotation, but the
  GIF is a pre-rendered figure; there is no `matplotlib.animation`, `imageio`, frame-export or video
  code anywhere in the repository.
- `Data Visualization: 3D Graphics`. No `mplot3d`, `projection='3d'`, `plot_surface`, VTK, Mayavi or
  PyVista anywhere.
- `Data Visualization: Web-Based`. `docs/interferometry.rst` describes running JupyterLab inside the
  `peijin/lofarsun` Docker image and port-forwarding it, but that is a deployment recipe for a
  general-purpose notebook server, not a browser visualization the package provides. The only GUI the
  package ships (`lofarBFcube`) is a desktop PyQt5 application.
- `Data Processing and Analysis: 2D Slices` and `Data Visualization: 2D Slices`.
  `BFcube.bf_image_by_idx(f_idx, t_idx)` does select a single (frequency, time) plane of a tied-array
  beam cube, but it then *forms an image* by interpolating scattered beam pointings onto a regular
  arcsecond grid. That is image formation from sparse samples rather than extracting a cross-section
  of a 3D volume, which is what these categories denote.
- `Servers and Environments: Software or Environment Container`. The documentation depends heavily on
  containers (`docker run … peijin/lofarsun`, `singularity pull docker://peijin94/lincsun:latest`), but
  this repository contains no Dockerfile, Singularity definition or container build recipe — the images
  are built in the separate `peijin94/lofarsunDocker` repository, which is recorded in Field 29 instead.
- `Data Processing and Analysis: Wavelet Analysis`, `Field-line Tracing`, `Plasma Moments`,
  `Energy Spectra`, `Pitch Angle Distributions`, `Curlometer`, `Packet Decommutation` — no
  corresponding code.

### 5. Related Region (MANDATORY)

**Values:** Solar Environment, Corona, Interplanetary Space, Solar Wind

`Solar Environment` was already part of the published record and is retained; the other three were
identified from the software's own documentation and added. All four exist in the live `Region`
vocabulary.

- `Corona` — preferred alongside the broad `Solar Environment` because Field 5 asks for the most
  specific applicable region. Metre- and decametre-wave solar radio emission at LOFAR's 10–240 MHz
  originates in the corona; the reference publication is titled "Imaging of the Quiet Sun in the
  Frequency Range of 20–80 MHz" and reports coronal brightness temperatures, and the MNRAS method
  paper's abstract frames the data as revealing "the plasma and energetic electron information in the
  solar corona and inner heliosphere."
- `Interplanetary Space` and `Solar Wind` — **this reverses an explicit rejection in the prior
  canonical file**, which wrote "While space weather applications might extend to Interplanetary Space,
  the primary scientific focus and data processing is for Solar Environment." The evidence that
  overturns it is the software's own documentation. `docs/index.rst` has a dedicated `:Heliosphere:`
  scope entry listing "Beamformed dynamic spectrum of quasars, for interplanetary scintillation" and
  "Pulsar observations for solar wind plasma and CMEs" among the observation types the toolset serves —
  and beamformed dynamic spectra are precisely what `lofarSun.BF` processes. This is the maintainer's
  own statement of the software's intended regions, not an inference from the science topic.

**Considered and rejected:** `Chromosphere`, `Photosphere`, `Solar Interior`. Emission at LOFAR
frequencies forms well above the chromosphere; the package contains no photospheric or interior
functionality, and the reference publication's measurements are coronal.

### 6. Authors (MANDATORY)

**Author 1**
- **Author Name:** Peijin Zhang
- **Author Identifier:** https://orcid.org/0000-0001-6855-5799
- **Affiliations:**
  - **Organization:** New Jersey Institute of Technology
  - **Affiliation Identifier:** https://ror.org/05e74xb87
  - **Organization:** Cooperative Programs for the Advancement of Earth System Science
  - **Affiliation Identifier:** https://ror.org/0015pkk46

**Author 2**
- **Author Name:** Pietro Zucca
- **Author Identifier:** https://orcid.org/0000-0002-6760-797X
- **Affiliation:**
  - **Organization:** Netherlands Institute for Radio Astronomy
  - **Affiliation Identifier:** https://ror.org/000k1q888

**Author 3**
- **Author Name:** Tammo Jan Dijkema
- **Author Identifier:** https://orcid.org/0000-0001-7551-4493
- **Affiliation:**
  - **Organization:** Netherlands Institute for Radio Astronomy
  - **Affiliation Identifier:** https://ror.org/000k1q888

**Author 4**
- **Author Name:** Cristina Cordun
- **Author Identifier:** https://orcid.org/0009-0003-5974-0185
- **Affiliation:**
  - **Organization:** University of Groningen
  - **Affiliation Identifier:** https://ror.org/012p63287

The published record previously named one author, Peijin Zhang, carrying no identifier and no
affiliation. All four ROR values above were resolved against the ROR API and each returns the
organization named
(`05e74xb87` → New Jersey Institute of Technology, Newark; `0015pkk46` → Cooperative Programs for the
Advancement of Earth system science, Boulder; `000k1q888` → Netherlands Institute for Radio Astronomy,
Dwingeloo; `012p63287` → University of Groningen).

**Where the authorship evidence lives.** This repository has no `CITATION.cff`, `AUTHORS`,
`CONTRIBUTORS`, `codemeta.json` or `.zenodo.json` file, and `setup.py` names only
`author = 'Peijin'` / `author_email = 'pjer1316@gmail.com'`. What it does have — and what earlier
passes missed — is **explicit `Author:` headers inside eight source files** under `utils/`, plus the
creator list on the software's own Zenodo deposit. Those two artifacts, not the science papers, are
what drive Authors 2–4.

**Peijin Zhang — identity and identifier.** The ORCID is established from several independent
directions rather than guessed: Crossref lists `https://orcid.org/0000-0001-6855-5799` as the first
author of *both* papers connected to this software (ApJ 932, 17 and MNRAS 521, 630); the ORCID record's
public email is `peijin.zhang@njit.edu`; its employment list contains New Jersey Institute of
Technology, Cooperative Programs for the Advancement of Earth system science, Netherlands Institute for
Radio Astronomy, University of Helsinki and the Bulgarian Academy of Sciences, and its education
entries are University of Science and Technology of China — matching the git commit identity
`peijin@ustc.edu`, the SLURM mail address `peijin.zhang@helsinki.fi` in
`utils/IM/slurmScripts/sbatch_calib.sh`, and the maintainer link `pjzhang.cc` in `docs/index.rst`
(also a researcher URL on the ORCID record). He is named `Maintainer` in `docs/index.rst`, `author` in
`docs/conf.py`, and the `LICENSE` copyright holder. An ORCID search on the name returns 8 records;
of the other 7, one lists Zhejiang University and the rest list no institution at all, and none shows
any tie to LOFAR, solar radio astronomy or the institutions above.

**Never emit the repository's placeholder ORCID.** `paper.md` line 10 carries
`orcid: 0000-0000-0000-0000` — the unfilled JOSS template default. It is not an identifier and must
never be written into HSSI.

**Peijin Zhang — affiliation choices.** `paper.md` gives two: "Center for Solar-Terrestrial Research,
New Jersey Institute of Technology, Newark, NJ, USA" and "Cooperative Programs for the Advancement of
Earth System Science, University Corporation for Atmospheric Research, Boulder, CO, USA".
- For the first, the department (Center for Solar-Terrestrial Research) has no ROR of its own — a ROR
  query returns only unrelated institutes — while the parent institution has ROR
  `https://ror.org/05e74xb87` and already exists as an HSSI organization row under exactly the name
  "New Jersey Institute of Technology" with that identifier. Recording the institution keeps name and
  identifier referring to the same entity and reuses the existing row; recording the department string
  against the institution's ROR would not.
- For the second, CPAESS has its own ROR, `https://ror.org/0015pkk46`, which is also the identifier
  ORCID records for this employment — so the programme is preferable to its parent, which is more
  precise metadata. HSSI does have a "University Corporation for Atmospheric Research" row
  (`https://ror.org/04zhhyn23`); it was considered and not selected for that reason. ROR's own display
  string capitalises the name "Cooperative Programs for the Advancement of Earth system science"; the
  title-cased form used above follows `paper.md`, and organization names are free text in HSSI rather
  than a controlled list.
- His ORCID also records a 2022 visiting-researcher position at the Netherlands Institute for Radio
  Astronomy. Considered and not selected: a three-month visiting role, and the software's own paper
  records only the two affiliations above. (That ORCID employment's disambiguation entry is a GRID id,
  `grid.425696.a`, not a ROR — every ROR used in this field was taken from the ROR API directly rather
  than from ORCID's disambiguation block.)

**Pietro Zucca — why he is an author, and why the reason is not the ApJ paper.** He is named in an
explicit `Author:` header in **eight** source files shipped in this repository:
`utils/BF/h5_calibrate_fits.py` ("Author: Cristina Cordun, Peijin Zhang, Pietro Zucca") and seven files
carrying "Author: Peijin Zhang, Pietro Zucca" —
`utils/IM/commandlines/auto_sun_calib.py`, `batch_sun_calib.py`, `get_datetime_index.py`,
`utils/IM/slurmScripts/autoCalib_job.py`, `clean_job.py`, and the `DISCOVERER/` variants of the last
two. Two of those (`auto_sun_calib.py`, `get_datetime_index.py`) are documented as user-facing tools in
`docs/interferometry.rst`. That is a direct authorship claim in the software itself, which is a
different and much stronger basis than co-authorship of a paper. His ORCID,
`https://orcid.org/0000-0002-6760-797X`, comes from Crossref's author record on ApJ 932, 17, and the
ORCID record itself shows "Associate Scientist, LOFAR" at the Netherlands Institute for Radio Astronomy
since June 2017 — i.e. ASTRON LOFAR staff, consistent with the LOFAR SSWKSP context of this package.
The prior canonical file listed him as author 2 for the wrong reason (the ApJ author list); he is
recorded here for the right one.

**Tammo Jan Dijkema — why he is an author.** He is one of three creators on the software's own Zenodo
deposit (record 4495451 / concept 4495450), with affiliation "Astron", and he is a git contributor
(`dijkema@astron.nl`, commit 04ba4f1 of 2019-10-23, "fix standalone matplotlib windows on mac",
touching the beamformed quick-view GUI that became `lofarSun/BF/GUI/lofarBFgui.py`). A creator credit
on the software's DOI record is authorship of the software, which is what Field 6 asks for. The ORCID
identification carries less certainty than Authors 1–2, and its basis is recorded so it can be
re-examined rather than re-derived: `0000-0001-7551-4493` is the sole exact "Tammo Jan Dijkema" an
ORCID name search returns, but that record lists no employments. Its four works
are all radio-astronomy engineering — the Apertif calibration pipeline (an ASTRON instrument),
sidereal visibility averaging for wide-field interferometric imaging, an FRB localisation, and a lunar
microsatellite VHF/UHF communication system — consistent with the ASTRON software engineer who holds
the `@astron.nl` address, and inconsistent with the other Dijkema records returned by the search
(biodiversity, medicine, public health, geography).

**Cristina Cordun — the evidence is narrower than for the other three, and stronger than a single
name in a header.** She is named in the `Author:` header of one file, `utils/BF/h5_calibrate_fits.py`
("Author: Cristina Cordun, Peijin Zhang, Pietro Zucca", file dated 2019-Aug) — a 381-line script that
splits, downsamples and flux-calibrates LOFAR tied-array-beam dynamic spectra against a known
calibrator model — and she is listed **first**, ahead of Zhang and Zucca. Three further facts carry
the entry past a bare header credit:

- That file's own changelog carries `2022-06-10: [Cristina] add feature cross calibration` — a feature
  credit written by the maintainer, in the maintainer's own bracketed-initials convention, naming her
  for a capability rather than for a courtesy.
- Commit **6bed052** (2022-06-10, "bug fix by Cris", authored by Peijin Zhang) is where that changelog
  line was added, alongside real code: the calibrator name was corrected from `'Cassiopeia '` to
  `'Cassiopeia A'` and lifted out of the call site into a `calibrator_name` variable.
- **Her absence from `git shortlog` is therefore not evidence against her.** Zhang committed her work
  under his own name, which is exactly why no commits exist under hers. Any future pass that re-checks
  this field should not treat the empty git history as a reason to drop her.

The ORCID identification is unambiguous rather than merely plausible: an ORCID search on the family
name "Cordun" returned three records in total — Octavian Cordun (oncology, Republic of Moldova),
Sinziana Popa-Cordun (no institution recorded), and `0009-0003-5974-0185`, "Cristina-Maria Cordun",
Scientific Staff in the Astronomy department at the University of Groningen. Her four listed works sit
in low-frequency radio astronomy and radio spectroscopy — separating clock delays from ionospheric
effects in radio astronomy, an interferometric search for decametre radio emission from the exoplanet
Tau Boötis b, lunar-subsurface and galactic-foreground estimation for LuSEE-Night, and millimetre-band
CO/CN absorption in the early universe. The first two are the closest fit to the author of a LOFAR
beamformed calibration script, and neither of the other two Cordun records has any astronomical
connection.

**Caveat on her affiliation, recorded so it is read correctly.** The header gives no affiliation, so
the University of Groningen above comes from her ORCID employment record, which runs 2023-09-01 to
2027-09-01. Her contribution to this software dates to 2022-06, so the recorded affiliation
*postdates* the work. Her 2022 affiliation is not recorded in the repository, in ORCID, or in any other
authoritative source that was found. Groningen was accepted knowingly on that basis: it is her only
documented institution and it is the one ORCID attests, but it is not where she was when she wrote this
code.

**Considered and rejected — "LOFAR Solar and Space Weather Key Science Project" as an organization
author.** `paper.md` lists "LOFAR SSWKSP" as a second, equal-contributing author with affiliation
"ASTRON – The Netherlands Institute for Radio Astronomy", and its acknowledgements repeat "We
acknowledge contributions from ASTRON and LOFAR SSWKSP for building LOFAR data processing pipeline and
operating the observation." That is a real authorship claim by the maintainer, so it is documented
here rather than discarded. It is not recorded because there is no defensible identifier for it: ROR has
no record for the Key Science Project (queries for its expanded name and for "International LOFAR
Telescope" return only unrelated organizations), and an organization author without a `ror.org`
identifier is stored by HSSI as a person with a blank given name — a state that is known to reject the
entire authors field on a later metadata update, so adding it would make this record harder to maintain
in future. Borrowing ASTRON's ROR for an author named after the KSP was also rejected: the identifier
would denote a different entity from the name. The ASTRON connection is instead carried by Authors 2
and 3, both of whom are ASTRON people. The credit itself is real; it is the absence of a safe
identifier, not any doubt about the maintainer's intent, that decides the field.

**Considered and rejected — Pearse Murphy** (`pearse.murphy@obspm.fr`, 3 commits on 2023-02-23:
"First update of docs", "add section on inspecting calibration solutions", "fix typo"). He wrote a
substantial part of `docs/interferometry.rst`, including the LoSoTo calibration-solution inspection
section. He appears in no `Author:` header, no citation artifact, no Zenodo creator list (which
predates his commits), and neither paper's author list. Documentation editing of that scale is a
contribution rather than authorship of the software, so he is recorded here rather than listed above.

**Considered and not selected — Sarrvesh Seethapuram Sridhar.** He appears in all eight files that
carry `Author:` headers, but on the adjacent line and under a different label: `Acknowledge:`. The
files distinguish authorship from acknowledgement explicitly, and that distinction is respected here.
(His ORCID, should it ever be needed, is `https://orcid.org/0000-0002-7587-4779` — the sole exact name
match.)

**Considered and not selected — the eight remaining co-authors of the reference publication.** The
prior canonical file listed Pietro Zucca, Kamen Kozarev, Eoin Carley, ChuanBing Wang, Thomas Franzen,
Bartosz Dabrowski, Andrzej Krankowski, Jasmina Magdalenic and Christian Vocks as software authors
2–10, with the speculative note that they "likely contributed to the scientific use cases and
validation." Zucca is retained above on independent in-repository evidence; the other eight are not.
They are co-authors of ApJ 932, 17 — a science paper that *used* this library and cites it as an
external tool ("using the LOFAR-Sun-tools library") — and none of them appears in any `Author:` header,
in `setup.py`, in `LICENSE`, in the Zenodo creator list, in `paper.md`, or in the git history. Four of
the surnames do turn up in `paper.bib`, but only inside the author lists of *cited* papers — Kozarev in
the MNRAS RFI entry, Franzen, Krankowski and Vocks in the de Gasperin 2020 A-team sky-model entry, and
Vocks again in van Haarlem 2013 — which is a citation, not a credit on this software. A
paper's author list is not a software's author list. These names are not present in the HSSI
record, so declining to add them changes nothing stored; the reasoning is recorded so the arXiv author
list is not mined for authors again. The same applies to André R. Offringa and Mattia Mancini,
co-authors of the MNRAS RFI method paper (Field 27). Offringa's name does appear in the repository —
in `paper.md`'s WSClean citation and in a FITS header string quoted in `demo/demo_sunpymap.ipynb`
("W-stacking imager written by Andre Offringa") — but as the credited author of WSClean, an external
tool this software drives (Field 30), not as a contributor to `lofarSun`.

**Considered and not selected — "Pjer1316".** The third Zenodo creator. It is a GitHub handle belonging
to Peijin Zhang himself (`setup.py` `author_email = 'pjer1316@gmail.com'`; git identities
`pjer1316@icloud.com`, `pjer1316@mail.ustc.edu.cn`, `pjer1316@gmail.com`), not a separate person — a
common artifact of the GitHub–Zenodo integration failing to merge two accounts. Adding it would
duplicate Author 1.

**Considered and not selected — Michael R. Crusoe** (1 commit, 2024-12-17): a one-word typo fix in
`utils/IM/LINC/lincSun/steps/LoSoTo.Plot.cwl` (`$schemas` must be plural). Not authorship.


### 7. Software Name (MANDATORY)

**Value:** lofarSun

The stored HSSI value, retained. It is the distribution name in `setup.py` (`name = 'lofarSun'`), the
PyPI project name, the name PyHC registers, and the name `paper.md` uses in its title. The repository
title is "LOFAR Sun Tools" and the prior canonical file recorded the value as
"lofarSun (package name) / LOFAR Sun Tools (full name)"; that dual form is not a name and the
single package name is the correct value.

### 8. Description (MANDATORY)

**Value:** lofarSun is a Python toolset for solar radio imaging spectroscopy data processing from the Low Frequency Array (LOFAR) telescope. The package provides comprehensive tools for processing LOFAR solar observations, including beamformed data (dynamic spectra), interferometric imaging, and data analysis. It includes three main modules: (1) lofarSun.BF for dynamic spectrum processing with RFI flagging using feature matching methods available on both CPU and GPU; (2) lofarSun.IM for interferometric imaging post-processing, including calibration with A-team sources, coordinate transformations, and 2D Gaussian source fitting; and (3) lofarSun.cli for command-line utilities for data inspection and conversion. The tools are designed to be modular and flexible, enabling high-quality radio observations of the Sun at frequencies below 240 MHz for studying, monitoring, and forecasting solar activity and space weather.

Retained unchanged. This is the description currently published in HSSI and it is also the wording the
prior canonical file recorded, so it represents a settled editorial choice; it is not re-worded here
merely because a different phrasing is possible. Its factual claims hold against the source at the
pinned revision: the three modules exist as described (`lofarSun/BF/`,
`lofarSun/IM/`, `lofarSun/cli/`), CPU/GPU RFI flagging is `RFIconvFlag.init_RFIconv(device=…)`,
A-team calibration and 2D Gaussian fitting are `bftools.model_flux()` / `IMdata.fit_gaussian2d()`, and
"below 240 MHz" is `paper.md`'s own wording (line 34: "capable of observing the Sun at frequencies
below 240 MHz"). `docs/index.rst` does **not** state that figure — it describes LOFAR's coverage as
per-mode time and frequency resolutions (~0.5 MHz for interferometric imaging, 0.02 MHz for tied-array
and beamformed modes) and contains no "240" anywhere. `paper.md` is the sole in-repository source for
the 240 MHz upper bound.

### 9. Concise Description (OPTIONAL)

**Value:** LOFAR solar and spaceweather data processing

Retained unchanged — the stored HSSI value, which is verbatim the PyHC community registry's curated
`description` for this package and therefore a maintainer-adjacent wording rather than an
auto-generated one. The prior canonical file proposed an alternative ("Python tools for LOFAR solar
radio imaging spectroscopy data processing, including beamformed data analysis, interferometric
imaging, and RFI flagging."); it is a stylistic variant, not a correction, and the curated PyHC
wording is kept. Both are within the 200-character limit.

### 10. Publication Date (RECOMMENDED)

**Value:** 2019-06-07

Retained. This is the GitHub repository creation timestamp (`created_at: 2019-06-07T05:38:54Z`) and it
coincides with the first commit (9ca1c91, "auto calib", 2019-06-07). Field 10 asks for the date of
first publication of the initial version, and this is when the code first became public.

**Alternative considered:** the first PyPI release, `0.1`, uploaded 2019-10-10. Not selected — the
repository was already public four months earlier, so 2019-06-07 is the earlier and therefore correct
first-publication date.

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Retained from the stored HSSI record.

**Zenodo considered and not selected.** The submission form's guidance for Field 11 says that where a
DOI was obtained through the GitHub–Zenodo workflow, Zenodo is the correct publisher — and Field 2
records exactly such a DOI, so `Zenodo` / `https://zenodo.org` was a live alternative rather than a
theoretical one. GitHub is kept because the Zenodo deposit is a single 2021 snapshot made under the
repository's former name, while GitHub (with PyPI) is where the software is actually distributed and
where every release after v0.1.0 has appeared. Strict conformance to the form's wording would name a
publisher that has carried one version of this software, once, five years ago. This was decided
together with Field 2, not independently of it.

### 12. Version (RECOMMENDED)

- **Version Number:** 0.3.33
- **Version Date:** 2023-05-25
- **Version Description:** Not found
- **Version PID:** Not found

**Version number.** `0.3.33` is the stored HSSI value and matches `setup.py` line 13 at the pinned
revision f445024. (HSSI's view API renders this field as `lofarSun - 0.3.33`; the stored value is the
bare number, and the rendered prefix must never be copied into this file or into a payload.)

**0.3.33 was never released — recorded so the discrepancy is not later mistaken for an error.** PyPI's
latest published release is `0.3.32`, uploaded 2023-03-13; `https://pypi.org/pypi/lofarSun/0.3.33/json`
returns 404, and the project has **no git tags and no GitHub releases at all**. So `0.3.33` exists only
as a source-tree version string. `0.3.32` with version date `2023-03-13` — what a user who runs
`pip install lofarSun` actually receives — was the alternative and was considered and not selected:
Field 12 describes the software instance rather than the distribution channel, and `0.3.33` is both the
value the published record already carried and the version the software declares at its current source
revision.

**Version date — correcting a previous wrong value.** `2025-04-08 (last repository update)`, derived
from GitHub's `updated_at` field, is what both the prior canonical file and the published record
carried. That is wrong twice over: `updated_at` tracks repository-metadata activity (description,
topics, stars) rather than code,
and the repository's actual last push is `pushed_at: 2024-12-19T13:17:17Z`, so 2025-04-08 could not be
a code date under any reading. Neither date has anything to do with version 0.3.33 in any case. The
value recorded here is derived from the commit that actually set the version:
`git log -L '/version = /,+1:setup.py'` identifies commit
**3a951f6bf2377bf58da5ea1f7f407fad2debd577** ("repair setup file", author and commit date
2023-05-25 18:40:49 +0300) as the change from `version = '0.3.32'` to `version = '0.3.33'`. A second
commit minutes later (234594385079136e75d19a7a852e7f2ff53af6df, "after merge") re-applied the same
line during a merge; the same calendar date results either way. Note that GitHub's `updated_at` is the
same misleading field that also produced the prior file's "SoMEF: last updated 2025-04-08" support for
Development Status — see Field 23.

**Version description — deliberately left empty.** No `CHANGELOG.md`, release notes, or GitHub release
exists, so nothing authored by the maintainer describes this version. The bump commit's diff is
nevertheless informative and is recorded here so it does not have to be re-derived. `setup.py` had an unresolved
git merge conflict committed into it — literal `<<<<<<< HEAD` / `=======` / `>>>>>>>` markers around a
0.3.30 block and a 0.3.32 block — and commit 3a951f6 ("repair setup file") resolved it by discarding
the 0.3.30 side, bumping the surviving block to 0.3.33, and adding `torch` to `install_requires`. The
`torch` addition is what makes the GPU-capable `RFIconvFlag` RFI flagger installable; the resolution
also kept the `pymsPSFfitPeakGauss` console script, which the 0.3.30 side lacked. A description such as
"Repairs a broken setup.py and adds torch to the install requirements, enabling the GPU-capable RFI
flagging module" is supported by that diff, but it would be our wording rather than the author's,
which is why the field is left empty rather than filled.

**Version PID.** None exists for 0.3.33. The one version-level DOI this software has,
`https://doi.org/10.5281/zenodo.4495451`, belongs to v0.1.0 (2021-02-02) and must not be attached to
this version. See Field 2 for the concept DOI.

### 13. Programming Language (RECOMMENDED)

**Value:** Python 3.x

Retained. `setup.py` classifiers declare `Programming Language :: Python :: 3.9`; `.readthedocs.yaml`
builds with `python: "3.9"`; `docs/install.rst` instructs `conda create -n lofarsun python=3.9`. The
installable package is entirely Python.

**Considered and rejected:** GitHub's language statistics for the repository are Jupyter Notebook
(1,049,340 bytes — the `demo/` notebooks), Python (414,452), Common Workflow Language (36,128),
Shell (9,773), TeX (9,055, the JOSS paper) and JavaScript (1,217). None of the non-Python entries
warrants a value. `Other` was considered for the CWL pipeline definitions under
`utils/IM/LINC/lincSun/`, which are a genuine and substantial part of the repository, but CWL is a
workflow description format rather than a language a user would program the package in, and `Other`
would tell a searcher nothing. `Javascript` was rejected outright: the 1.2 KB is
`lincSun/steps/utils.js`, expression helpers embedded in CWL. Shell and TeX are build/job glue and a
paper source.

### 14. Reference Publication (RECOMMENDED)

**Value:** https://doi.org/10.48550/arXiv.2205.00065

Retained — the stored HSSI value, and the choice is now positively supported rather than merely
inherited. Two pieces of primary evidence:

1. `docs/index.rst` ends with an explicit **"Cite as — https://arxiv.org/abs/2205.00065"**. That is the
   maintainer's own stated preferred citation for the software, which is precisely what Field 14
   accommodates ("sometimes used as the preferred citation for the software").
2. The paper itself names and links the software: "We converted the coordinates into Helioprojective
   coordinates and the flux density into brightness temperature using the LOFAR-Sun-tools (Zhang et
   al., 2020) https://github.com/peijin94/LOFAR-Sun-tools library." So it is not merely a paper that
   used the tools in passing; it documents what the library does and points readers at it.

**The prior canonical file's proposal to replace this with the ApJ DOI is not adopted.** It argued from
DataCite's `IsVersionOf` relation that `https://doi.org/10.3847/1538-4357/ac6b37` (ApJ 932, 17,
"Imaging of the Quiet Sun in the Frequency Range of 20–80 MHz") is the version of record and therefore
the better reference. That is true as bibliography but it contradicts the maintainer's own "Cite as"
instruction, and no information is lost by keeping the preprint here: the ApJ version of record is
already carried in Field 27, so both DOIs remain in the record. The swap is mechanically clean — the
ApJ DOI here, the arXiv DOI in Field 27 — and it was considered and declined: it would contradict the
maintainer's own citation instruction, and that is not a change to make as a silent normalisation.

**Considered and not selected — MNRAS 521, 630 (`https://doi.org/10.1093/mnras/stad491`).** "RFI
flagging in solar and space weather low frequency radio observations" is the methods paper for
`lofarSun/BF/RFIconvFlag.py` — `paper.md` cites it for exactly that ("The RFI flagging uses a feature
matching based method [@zhang:2023] available both on CPU and GPU") and the paper's abstract describes
"a novel method that makes use of a morphology convolution," which is what `init_RFIconv()` implements.
It describes one module rather than the toolset, and it neither names the package nor links the
repository. It belongs in Field 27, where it is recorded.

**Negative research — there is no JOSS paper, and one should not be searched for again.** The
repository contains a complete JOSS submission kit: `paper.md` in JOSS front-matter form (title
"lofarSun a toolset for the solar radio imaging spectroscopy data processing of LOFAR", date
02 December 2023), `paper.bib`, and `.github/workflows/draft-pdf.yml` running
`openjournals/openjournals-draft-action`. It was not submitted or published, and as of this extraction no JOSS record exists: JOSS's own search for
"lofarSun" returns an empty feed; a GitHub search of `openjournals/joss-reviews` for `lofarSun`
returns 0 issues (a search for "LOFAR" returns 7 unrelated submissions — udpPacketManager, pyuvdata,
pyuvsim, Tools21cm, WILL, and a VLBI pipeline); Crossref has no JOSS work matching lofarSun, and
`paper.md`'s ORCID is still the unedited `0000-0000-0000-0000` placeholder. If a JOSS paper is ever
published it would become the natural Field 14 value; as of this extraction none exists.

### 15. License (RECOMMENDED)

**Value:**
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html

`MIT License` is the canonical row name in HSSI's closed `License` list. Three independent sources
agree on the licence itself: the repository's `LICENSE` file contains the full MIT text
("Copyright (c) 2021 Peijin Zhang"); `setup.py` declares `license='MIT'` and the classifier
`License :: OSI Approved :: MIT License`; and the GitHub API reports
`license: {key: mit, spdx_id: MIT}`. PyPI's metadata for the package also reports `license: MIT`.

**Trap:** the value is `MIT License`, not the bare SPDX identifier `MIT`. The License vocabulary is a
closed list matched on the exact name, and HSSI's production instance carries legacy duplicate rows
that a near-miss could bind to. None of those duplicates is an MIT variant, so this particular value is
unambiguous wherever it is used — but the name has to be spelled in full.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values (12):** astronomy, dynamic spectrum, imaging spectroscopy, lofar, radio, radio frequency
interference, radio interferometry, solar, solar and stellar astrophysics, solar physics,
space physics, space weather

Keywords are stored lower-case and rendered in Title Case; a casing difference between this file and
the rendered record is a display artifact, not a different value.

- **Already part of the published record (7):** astronomy, lofar, radio, radio interferometry, solar,
  solar physics, space physics. All retained. Corroborated by `setup.py` (`keywords = ['LOFAR', 'Solar', 'radio']`),
  GitHub topics (`lofar`, `solar`), the PyHC registry (`keywords: [lofar]`) and `paper.md`'s JOSS tags
  (Radio interferometry, astronomy, Solar physics).
- **Carried over from the prior canonical file (1):** solar and stellar astrophysics. Its source is the
  arXiv subject classification on the reference publication's DataCite record
  (`Solar and Stellar Astrophysics (astro-ph.SR)`, alongside `Space Physics (physics.space-ph)`, which
  is already present). It is retained. Its weakness is recorded so the choice is not silently
  reversed: it is an arXiv category label rather than a topical science keyword of the kind Field 16
  asks for, which makes removal defensible. Removal was weighed and declined — nothing about the label
  is inaccurate, and dropping a value already carried in the record needs a stronger reason than
  tidiness.
- **Added (4):**
  - `imaging spectroscopy` — `paper.md`'s title is "lofarSun a toolset for the solar radio imaging
    spectroscopy data processing of LOFAR"; this is the software's central subject and its absence is
    the most conspicuous keyword gap.
  - `space weather` — the PyHC description and the concise description both say "solar and
    spaceweather"; `docs/index.rst` frames LOFAR as "a great instrument for solar and space weather
    studys"; the MNRAS method paper's title is "RFI flagging in solar and space weather low frequency
    radio observations".
  - `dynamic spectrum` — the core beamformed data product; `docs/beamformed.rst` is built around it and
    `lofarSun.BF` produces it.
  - `radio frequency interference` — RFI flagging is one of the package's two headline capabilities
    (`lofarSun/BF/RFIconvFlag.py`, the MNRAS method paper).

**Considered and rejected:** `python` (a `paper.md` JOSS tag — Field 13 already carries the language,
and a language tag is not a science keyword); `interferometry` and `radio astronomy` (redundant with
the existing `radio interferometry` + `radio` + `astronomy`); `sun` (redundant with `solar`).

### 17. Data Sources (OPTIONAL)

**Value:** Observatory/Mission-specific

Retained. The software consumes LOFAR observations from the LOFAR Long Term Archive:
`docs/interferometry.rst` documents the LTA (`https://lta.lofar.eu/Lofar`) as the data source including
the access-request path through the Solar and Space Weather KSP, and
`utils/IM/LINC/lincSun/steps/fetch_data.cwl` implements the retrieval. Field 17's own instruction to
pair an observatory-specific source with the observatory name is satisfied by Field 32.

**Considered and rejected:** `HTTP/HTTPS Directories`. The LTA fetch does use `wget` over HTTPS
(`https://lta-download.lofar.psnc.pl/lofigrid/SRMFifoGet.py?surl=…`), but that endpoint is an SRM/grid
staging gateway belonging to the LOFAR archive, not a browsable HTTP directory tree; the transport is an
implementation detail of an observatory-specific archive. The general archives and services in the
`DataInput` vocabulary — `CDAWeb`, `HAPI`, `VSO`, `OMNIWeb`, `SSCWeb`, `Madrigal`, `das2`, `AMDA`,
`VirES` — and `FTP/FTPS Directories` name sources this software has no code path to; the LTA is the
only archive it retrieves science data from. (The one other remote fetch the documentation names is the
`prefactor` A-team sky-model repository on GitHub, a calibration-model source rather than a data
archive; see Field 28.) A plain substring search is misleading here: `HAPI`, `VSO`, `AMDA` and `ftp` do
match inside this repository, but only inside base64-encoded image payloads — the same hazard described
in Field 21.

### 18. Input File Formats (RECOMMENDED)

**Values:** FITS, HDF5, IDL.sav, Other

Retained unchanged.
- `FITS` — `IMdata.load_fits()` (WSClean output images and PSFs), `BFdata.load_fits()` (beamformed
  FITS cubes), `IM.get_peak_beam_from_psf()`.
- `HDF5` — `bftools.h5_fetch_meta()`, `get_cal_bandpass()`, `cli/h5_to_fits_spec.compress_h5()` read
  LOFAR beamformed HDF5 via `h5py` (`SUB_ARRAY_POINTING_*/BEAM_*/STOKES_*` datasets).
- `IDL.sav` — `BFdata.load_sav_xy()` and `load_sav_radec()` via `scipy.io.readsav`.
- `Other` — CASA Measurement Sets (`.MS`), read through `python-casacore` in `cli/pyms_utils.py`
  (`get_obs_info_from_ms`, `get_t_from_ms`, `get_freq_from_ms`); there is no Measurement Set row in the
  vocabulary. Also covers the `.skymodel` / `.sourcedb` calibrator sky models the calibration scripts
  consume.

**Considered and rejected:** `JSON`. The lincSun workflows read JSON parameter files (`calib.json`,
`applyLBA.json`, `ms.json`) and `utils/IM/commandlines/batch_sun_calib.py` reads `ms.json`, but these
are pipeline configuration, not scientific data input.

### 19. Output File Formats (RECOMMENDED)

**Values:** FITS, HDF5, JSON, Other

- `FITS` — retained. `BFdata.write_fits()` and `write_fits_full()` build a `PrimaryHDU` with LOFAR
  headers (`TELESCOP = "LOFAR"`, `INSTRUME = "LBA"`, `OBJECT = "Sun"`); `compress_h5()` calls
  `full_hdu.writeto(out_path_fits, overwrite=True)`.
- `JSON` — added. `cli/h5_to_fits_spec.py` writes a metadata sidecar for every chunk it
  produces: `out_path_json = os.path.join(real_out_dir, fname + '.json')` and
  `json.dump(lofar_json_dict, fp)`, carrying telescope, antenna set, project and observation IDs,
  pointing, time and frequency ranges, and an event stub. `utils/BF/h5_calibrate_fits.py` does the same.
  This is a genuine generated data product, not configuration.
- `Other` — added. The same CLI writes an annotated quicklook image per chunk
  (`fig.savefig(out_path_png)` to `out_path_png = … + '.png'`, with colourbar, axes and optional KSP /
  IDOLS logos). PNG has no row in the vocabulary, so `Other` is the correct home.
- `HDF5` — **retained; it is the weakest value in this field, and the reason is recorded.** No HDF5
  writer exists anywhere in the repository: a search for `h5py.File(…, 'w')`, `create_dataset` and `to_hdf`
  across all Python and notebook files returns nothing, so the importable package reads HDF5 but never
  writes it. What does justify keeping it is the lincSun calibration workflow shipped in
  `utils/IM/LINC/`, which `docs/interferometry.rst` says "will yield a solution.h5 file in the results
  directory" — a LoSoTo H5parm calibration-solution table. That HDF5 file is produced by DP3/LoSoTo
  running inside the container, orchestrated by CWL definitions in this repository. Since the value
  was already carried in the record and a defensible reading supports it, it is retained rather than
  removed. Narrowing Field 19 to describe only what the importable Python package itself writes was the
  alternative, and was declined.

### 20. Operating System (RECOMMENDED)

**Value:** Linux

This replaces `Operating System Independent`, which the published record previously asserted.

**Why `Linux` is the correct value.** `setup.py` lists `python-casacore` in `install_requires`.
That package is published on PyPI with the single classifier
`Operating System :: POSIX :: Linux`, and its current release (3.8.1) ships a source tarball and
`manylinux_2_28_x86_64` wheels only — no macOS or Windows wheel in that release, and casacore itself
has no Windows support. A `pip install lofarSun` therefore succeeds out of the box on Linux only.
(Older `python-casacore` releases did carry macOS wheels; Field 21 records how far that history runs
and why it does not change the outcome.) The surrounding evidence points the same way:
`.readthedocs.yaml` builds on `ubuntu-20.04`; `docs/install.rst` opens by saying "The dependencies of
imaging software is very complex, we recommend using docker or singularity to run the software"; the
batch scripts under `utils/IM/slurmScripts/` target Linux clusters through SLURM and Singularity; and
the calibration and imaging chain the docs describe (DP3/DPPP, WSClean, LINC, LoSoTo, AOFlagger) is
Linux-only software.

**The two alternatives, and why they lost.** The pure-Python parts of the package — the `BF`
dynamic-spectrum path, the HDF5→FITS converter, the plotting — carry no OS-specific code, so a user who
can obtain casacore by other means (conda-forge provides macOS builds) can run much of the package on
macOS. That made **`Linux` + `Mac`** a real alternative rather than a theoretical one; it was declined
because no wheel, CI job or documentation page in this repository verifies macOS support, so choosing
it would assert platform support the evidence does not carry. **Keeping
`Operating System Independent`** was the conservative, no-change option and was declined because it is
not true of the documented install path: Windows is categorically excluded, since `python-casacore` has
no Windows build on any channel and casacore has no upstream Windows support at all. An
`... Independent` value should mean that no major platform is shut out, and here one is.

**Trap, independent of the outcome:** `OS Independent` is not a value in the vocabulary. The prior
canonical file recorded "OS Independent (Linux preferred for HPC workflows)", which
would be rejected on submission twice over — for the wrong string and for the parenthetical. The only
cross-platform value is `Operating System Independent`, spelled out.

### 21. CPU Architecture (RECOMMENDED)

**Values:** x86-64, GPU, HPC or HEC

`x86-64` replaces `CPU Independent`, which the published record previously asserted; `GPU` was already
part of that record and is retained; `HPC or HEC` is added. The move to `x86-64` mirrors the Field 20
resolution to `Linux` exactly — both turn on the same `python-casacore` packaging fact, and the two
fields were decided together so they tell one consistent story rather than contradicting each other.

- `GPU` — support is concrete rather than aspirational: `RFIconvFlag.RFIconv(device=…)` and
  `init_RFIconv(net, …, device=…)` move the convolution kernels to the requested torch device, `torch`
  is a hard dependency added in the 0.3.33 bump, and `paper.md` states the RFI flagging is "available
  both on CPU and GPU."
- `HPC or HEC` — `utils/IM/slurmScripts/` ships SLURM batch scripts (`sbatch_calib.sh` with
  `#SBATCH --array=0-243`, `sbatch_clean.sh`, `sbatch_cutout.sh`, `sbatch_prepCalib.sh`) that run
  Singularity containers across cluster nodes, plus a `DISCOVERER/` variant for that supercomputer with
  its own `readme.MD` on job submission; `docs/interferometry.rst` gives a full `#SBATCH` recipe for
  running the lincSun workflow on HPC. This is the same evidence that supports
  `Servers and Environments: High Performance Computing` in Field 4.
- `x86-64` — the current `python-casacore` release (3.8.1) publishes an sdist and five
  `manylinux_2_28_x86_64` wheels (cp310–cp314) and nothing else, so the documented `pip install` path
  delivers an x86-64 package. The project's wheel history matters and is recorded so it is not
  mistaken for a contradiction: no Linux `aarch64` wheel has ever been published, and the macOS wheels
  that older releases carried — through 3.5.0, whose `macosx_12_0_arm64` build was uploaded
  2022-07-07, a day after that release's Linux wheels — were discontinued, so an ARM user has no
  current wheel to install. The consequence is
  concrete: `lofarSun/cli/pyms_utils.py` opens with an unconditional `import casacore.tables as pt`, so
  for a user on ARM who follows that path the entire Measurement-Set path fails to import. And the
  repository's own HPC deployment is explicitly gated to x86 —
  `utils/IM/slurmScripts/sbatch_calib.sh`, `sbatch_prepCalib.sh`, `sbatch_cutout.sh` and
  `sbatch_clean.sh` each carry `#SBATCH --constraint=avx` on line 6, the only `--constraint` lines in
  the repository and a deliberate, human-written instruction-set requirement. (The count is four, not
  six: `utils/IM/slurmScripts/DISCOVERER/` ships its own `sbatch_calib.sh` and `sbatch_clean.sh` for
  that supercomputer, and neither carries the constraint.) AVX is an x86 extension with no ARM
  equivalent.

**The two alternatives, and why they lost.** Enumerating the real coverage — `x86-64`,
`Linux aarch64 or arm64`, `Apple Silicon arm64` — was the more generous option, since conda-forge
builds `python-casacore` for `linux-64`, `linux-aarch64`, `osx-64` and `osx-arm64` (four platform
builds, not three; the vocabulary has no Intel-Mac row, so the OS-agnostic `x86-64` covers both
`linux-64` and `osx-64`, and Intel-Mac support is represented rather than dropped). It was declined for
the same reason Field 20 declined `Linux` + `Mac`: no wheel and no CI job in this repository verifies
ARM support. It is worth being precise about why the conda-forge coverage does not settle the question,
because it is easy to misread as "the docs recommend conda": the string `conda-forge` does not appear
anywhere in this repository, and `docs/install.rst` recommends only a bare
`conda create -n lofarsun python=3.9` with no channel named, then installs with
`python -m pip install lofarSun` or a `setup.py install` from the ASTRON GitLab clone — both of which
resolve `python-casacore` from PyPI. Obtaining casacore for ARM is therefore something a user must
arrange by other means, not something the software instructs.

Keeping **`CPU Independent`** was the conservative, no-change option and was declined because it was
being held to a looser standard than Field 20 applied to the identical fact. The coverage argument in
its favour is genuine: no CPU architecture is categorically excluded the way Windows is, the importable
package's own code is architecture-neutral, and the packaging constraint belongs to a dependency rather
than to `lofarSun`. But "obtainable, but not by the documented path" was judged insufficient to keep
`Operating System Independent` in Field 20, and it is no more sufficient here; and the
`#SBATCH --constraint=avx` lines are the one place where the software itself, rather than a
dependency's wheel matrix, names an instruction set. Weighting the repository's own statements above
its dependencies' packaging is what decided the field.

**The importable package is architecture-neutral; its HPC job scripts are not.** These two halves point
in opposite directions, which is precisely what made the field a judgement rather than a lookup, so
they are stated separately.

*Inside `lofarSun/` (what `pip install lofarSun` gives you):* no code targets a specific instruction
set. There are no SIMD or intrinsics code paths, no `-march` flags, and no C/C++/Cython extension
sources of any kind; the numeric work is numpy/scipy; the only accelerated path is
`torch.device("cuda:0" if torch.cuda.is_available() else "cpu")` at `lofarSun/BF/bftools.py:14` and
`lofarSun/cli/h5_to_fits_spec.py:29`, a runtime dispatch rather than an architecture-gated build; and
`numba`, `cupy`, `cython`, `multiprocessing`, `joblib` and `dask` are each absent from the source, from
`setup.py`'s `install_requires`, and from `env.yml`.

*Inside `utils/` (shipped in the repository but not installed):* the `--constraint=avx` batch scripts
described above. Per this file's opening scope note, `setuptools.find_packages()` picks up only
`lofarSun/*`, so that constraint binds the maintainer's cluster workflow rather than the installed
library — which is why it qualifies the question rather than settling it single-handedly.

**Search hazard for whoever re-checks this.** Grepping this repository for instruction-set names
(`AVX`, `SSE`, `NEON`, `VSX`, `x86` and the like) produces a steady stream of coincidental matches that
are not code, in both upper and lower case. **Do not draw any conclusion from a match count — open the
file and line.** The `--constraint=avx` lines above are the only real architecture references found;
everything else traced back to binary payloads stored as text. Three known sources, which is what was
encountered rather than a proof of completeness: the two base64-encoded PNG logo blobs in
`lofarSun/cli/h5_to_fits_spec.py` (`lofar_logo_base64` line 33, `idols_logo_base64` line 34); the
compiled Qt resource byte-literal in `lofarSun/BF/GUI/resource_rc.py`, whose `\xHH` escape notation
spells `x86` across 189 lines; and the base64 image outputs saved inside the `demo/` notebooks and
`utils/BF/test_calib.ipynb`. That last file is the same one Field 25 flags for the funding search — it
is a repeat offender for any substring search, and the notebooks around it behave identically.

### 22. Related Phenomena (OPTIONAL)

**Values:** Coronal Heating, Solar Corona, Solar Flares, Coronal Mass Ejections, Solar Wind

The `Phenomena` vocabulary is closed: a phenomenon with no row there belongs in Keywords instead of in
this field.

- `Solar Corona` (stored) — the reference publication images quiet-Sun coronal emission at 20–80 MHz;
  the MNRAS abstract describes revealing plasma and energetic-electron information "in the solar corona
  and inner heliosphere".
- `Solar Flares` (stored) — the burst-profile analysis functions (`bftools.FWHM()`, `DecayExpTime()`,
  `fit_biGaussian()` on flux–time distributions) exist to characterise solar radio bursts, and the
  MNRAS paper's central difficulty is that "solar radio bursts can be brighter than the RFI".
- `Coronal Heating` (stored) — retained. The reference publication's quiet-Sun brightness-temperature
  spectrum and its report of persistent low-brightness coronal regions are quiet-corona thermal
  diagnostics of the kind used in coronal-heating work. This is the least direct of the five and was
  re-examined rather than assumed; it is kept because it is already stored and the reference
  publication supports it.
- `Coronal Mass Ejections` and `Solar Wind` — added, on the same documentation evidence as the
  Field 5 region additions: `docs/index.rst` lists "Pulsar observations for solar wind
  plasma and CMEs" and "Beamformed dynamic spectrum of quasars, for interplanetary scintillation" among
  the heliosphere observation types the toolset serves.

**Considered and rejected:** `Geomagnetic Storms` and `X-ray emission` — no functionality, data product
or documentation in this repository touches either.

### 23. Development Status (RECOMMENDED)

**Value:** Inactive

`Inactive` is repostatus.org's "reached a stable, usable state but is no longer actively developed;
support is provided as time allows," and that is what the record shows as of 2026-08-06:

- The last commit of substance by the maintainer is 2023-12-04 ("add lincSun", "add content to
  paper.md"). Commits by month end there: 5 in 2023-12, then nothing until 2 commits in 2024-12, which
  are an external contributor's one-word CWL typo fix and the maintainer's merge of it. There are no
  commits in 2025 or 2026 — the pinned HEAD f445024 (2024-12-19) is still the tip of `master`.
- No PyPI release since `0.3.32` on 2023-03-13; no git tags and no GitHub releases ever.
- The repository is not archived and not disabled, issues are enabled, and the maintainer did merge an
  outside pull request in December 2024 — which is precisely the "support provided as time allows"
  half of the `Inactive` definition, and the reason `Abandoned` and `Unsupported` are wrong.
- `setup.py` still classifies the project `Development Status :: 4 - Beta`, and PyHC rates its software
  maturity "Partially met" and testing "Requires improvement" — consistent with usable-but-not-evolving.

**Correcting a previous value.** The prior canonical file recorded `Active`, supported by "SoMEF: last
updated 2025-04-08". That date is GitHub's `updated_at`, which reflects repository-metadata activity
rather than code — the same misreading that produced the wrong Version Date in Field 12. The repository
has not received a code push since 2024-12-19. `Active` is not defensible on the evidence.

This is a single-select field and the judgement is about a threshold. `Active` was considered — it is
the reading that signals the package is still maintained, and it is what the prior canonical file
asserted — and was declined, because nothing in the repository supports it.

### 24. Documentation (RECOMMENDED)

**Value:** https://lofar-sun-tools.readthedocs.io/

Retained — the stored HSSI value, chosen deliberately over the alternative rather than by default. Both
candidates resolve: the bare URL returns 200 after redirecting to
`https://lofar-sun-tools.readthedocs.io/en/latest/`, which is the version-pinned form that `README.md`
and `paper.md` link and that the prior canonical file recorded; the PyHC registry's `docs:` field
carries the same form without its trailing slash. The bare URL is preferred because
it is version-agnostic — Read the Docs will redirect it to whatever the current default version is, so
it keeps working if the project ever publishes a stable branch, whereas `/en/latest/` pins the value to
one version slug. At 39 characters it is far below the 200-character URL limit.

### 25. Funder (OPTIONAL)

**Value:**
- **Organization:** European Commission
- **Funder Identifier:** https://ror.org/00k4n6c32

An HSSI organization row already exists with exactly this name and ROR, so this reuses it.

**Evidence.** Both papers tied to this software acknowledge the same grant. The MNRAS RFI method paper
— the methods paper for `lofarSun/BF/RFIconvFlag.py` — states: "This project is majorly supported by
the STELLAR project, which has received funding from the European Union's Horizon 2020 research and
innovation programme under grant agreement No 952439," and Crossref records the same funder and award
in the paper's structured metadata (funder DOI 10.13039/100010661, award 952439). The reference
publication, ApJ 932, 17, independently states: "This work is supported by the European Union's
Horizon 2020 research and innovation programme under grant agreement 952439, project STELLAR
(Scientific and Technological Excellence by Leveraging LOFAR Advancements in Radio Astronomy)."
STELLAR is a LOFAR-focused H2020 project, so the connection to this software is topical as well as
bibliographic.

**How firm this attribution is.** The repository declares no funding of its own. A case-insensitive
search of all tracked files for "grant", "funding", "funded" and "acknowledg" matches 11 files, and
none of them carries a funding statement for this software. Three are real text hits: the word
"granted" inside the MIT `LICENSE` text; `paper.md`'s acknowledgements, which fund the LOFAR telescope
rather than the package (see the rejection below); and the personal
`Acknowledge: Sarrvesh Seethapuram Sridhar` line in the eight `utils/` source-file headers discussed in
Field 6. The eleventh file, `utils/BF/test_calib.ipynb`, is a false positive: the substring matches
only inside base64-encoded image payloads embedded in the notebook, not in any prose or code. So this
funder is inferred from the publications
rather than declared by the software. The inference is strong — two independent papers, one the
reference publication and one the methods paper for a core module, both naming the same grant — but it
remains an inference, and it is recorded as one so a future reader weighs it correctly rather than
treating it as a declaration by the software.

**Considered and firmly rejected — the LOFAR/ILT infrastructure funders.** The prior canonical file
listed twelve organizations here: CNRS-INSU, Observatoire de Paris, Université d'Orléans, BMBF,
MIWF-NRW, MPG, Science Foundation Ireland, Ireland's Department of Business Enterprise and Innovation,
NWO, STFC, Poland's Ministry of Science and Higher Education, and INAF. Every one of them comes from a
single sentence in `paper.md`'s acknowledgements which says, in terms, that *the ILT resources* — the
telescope — "have benefited from the following recent major funding sources". Those bodies funded the
LOFAR instrument and its operation, not the development of this Python package. Recording them as
software funders would make this record claim, falsely, that a dozen national science agencies funded
`lofarSun`. They are recorded here as rejected so they are not re-harvested from `paper.md` on a future
pass.

**Also considered and not selected:** the Bulgarian National Science Fund (VIHREN programme, contract
KP-06-DV-8/18.12.2019) and Poland's National Science Centre (Beethoven Classic 3, project
2018/31/G/ST9/01341). Both appear in the same acknowledgement paragraphs, but each supports a specific
co-author of the papers, not the software; the Polish grant is explicitly "for the Polish contribution
to the International LOFAR Telescope", i.e. infrastructure again.

### 26. Award Title (OPTIONAL)

**Value:**
- **Award Title:** Scientific and Technological Excellence by Leveraging LOFAR Advancements in Radio Astronomy
- **Award Number:** 952439

The full project title is confirmed from two sources: CORDIS's project page for grant 952439 titles it
"Scientific and Technological Excellence by Leveraging LOFAR Advancements in Radio Astronomy | STELLAR
| H2020", and ApJ 932, 17 spells out the same expansion in its acknowledgements. The title is 91
characters, comfortably under the 128-character `Award.name` limit that would otherwise fail at the
database write; the award number is 6 characters.

The acronym `STELLAR` alone was considered for the title field and rejected — Field 26 asks for the
full award title, and the acronym is not one.

This value stands or falls with Field 25 — it is the grant that funder awarded — and the two were
decided together.

**Vocabulary trap:** HSSI has both an
`European Commission` organization row carrying ROR `https://ror.org/00k4n6c32` and a separate
identifier-less `European Commission - Horizon 2020` row. The former is the correct one; the latter
should not be used, since the programme is not the funding organization and the row carries no
identifier.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Publication 1:** https://doi.org/10.3847/1538-4357/ac6b37

Zhang, P., Zucca, P., Kozarev, K., Carley, E., Wang, C., Franzen, T., Dabrowski, B., Krankowski, A.,
Magdalenić, J., & Vocks, C. (2022). *Imaging of the Quiet Sun in the Frequency Range of 20–80 MHz.*
The Astrophysical Journal, 932, 17. This is the published version of record of the arXiv preprint
recorded in Field 14; DataCite's record for the preprint carries `IsVersionOf` this DOI. Keeping both
means the record holds the preprint the maintainer asks users to cite *and* the version of record.

**Publication 2:** https://doi.org/10.1093/mnras/stad491

Zhang, P., Offringa, A. R., Zucca, P., Kozarev, K., & Mancini, M. (2023). *RFI flagging in solar and
space weather low frequency radio observations.* Monthly Notices of the Royal Astronomical Society,
521(1), 630–637. This is the methods paper for one of the package's two headline capabilities:
`paper.md` cites it precisely for the RFI flagger ("The RFI flagging uses a feature matching based
method [@zhang:2023] available both on CPU and GPU"), it is entry `zhang:2023` in `paper.bib`, and its
"morphology convolution" method is what `lofarSun/BF/RFIconvFlag.py` implements with hand-set kernels.
It is also the source of the Field 25/26 funding evidence.

**Considered and not selected — the remaining `paper.bib` entries.** `paper.bib` also holds van Haarlem
et al. 2013 (`10.1051/0004-6361/201220873`, the LOFAR telescope description), de Gasperin et al. 2019
(`10.1051/0004-6361/201833867`, the LINC calibration strategy), de Gasperin et al. 2020
(`10.1051/0004-6361/201936844`, A-team sky models at ultra-low frequencies) and Offringa et al. 2014
(WSClean, MNRAS 444, 606). These are background citations for the instrument and for external tools the
pipeline invokes — they neither describe, cite, nor use `lofarSun`. The tools they describe are recorded
in Fields 29 and 30 where appropriate.

**Considered and not selected — duplicating the arXiv DOI here.** The prior canonical file listed both
`10.48550/arXiv.2205.00065` and `10.3847/1538-4357/ac6b37` in this field while also proposing the ApJ
DOI for Field 14. With the preprint in Field 14, repeating it here would be redundant.

### 28. Related Datasets (OPTIONAL)

**Value:** Not found

**Negative research, recorded so the search is not repeated.** The closest thing to a citable dataset
the repository points at is `README.md`'s "Test data: https://pjzhang.cc/static/demo_data.7z". That URL
now returns **404** — the demonstration archive is gone from the maintainer's personal site, so it is
not merely uncitable but unavailable. It was demonstration input for the `demo/` notebooks, not a
citable dataset, and carries no DOI.

The observations the software processes live in the LOFAR Long Term Archive
(`https://lta.lofar.eu/Lofar`), which `docs/interferometry.rst` documents including the note that "Not
all data on the LTA is public and you may have to request access from the Solar and Space Weather KSP."
The LTA is a multi-project archive rather than a specific dataset with a persistent identifier, and it
is already represented through Field 17 (`Observatory/Mission-specific`) and Field 32 (LOFAR). Neither
paper deposits a dataset DOI: the MNRAS paper's data-availability statement points at the LTA under
LOFAR's one-year proprietary policy with recent events "available on request to the author," and no
DataCite dataset record for lofarSun or LOFAR-Sun-tools exists.

The `utils/IM/LINC/lincSun/` workflows reference an `ATeam_skymodel` input and the docs point at
`https://github.com/lofar-astron/prefactor/tree/master/skymodels` for A-team sky models. Those are
calibration model inputs distributed as source files in another repository, not a citable science
dataset; they were considered and not recorded here.

### 29. Related Software (OPTIONAL)

Four entries. Each is a LOFAR- or radio-astronomy-specific tool that tells a reader something about
*this* package; the generic scientific-Python stack is deliberately absent (see the rejections below).

**1. LINC — LOFAR Initial Calibration pipeline**
- https://git.astron.nl/RD/LINC
- The pipeline this software's imaging path is built on and derived from. `paper.md`: "The
  preprocessing is based on the LINC pipeline [@GasperinCalib:2019]." The repository ships
  `utils/IM/LINC/lincSun/` — 8 CWL workflows and 19 CWL step definitions that adapt LINC's calibration
  and imaging steps for solar observations — and `docs/interferometry.rst` documents running them with
  `cwltool` inside the LINC container. This is the "software this work was forked from" relationship
  Field 29 explicitly asks for.

**2. AOFlagger**
- https://gitlab.com/aroffringa/aoflagger
- Software performing the same task by a different method. AOFlagger is the standard RFI flagger for
  LOFAR; `utils/IM/slurmScripts/sbatch_prepCalib.sh` invokes it
  (`flag.type=aoflagger flag.strategy=LOFAR-LBA-default.rfis`), and the MNRAS method paper investigates
  "a strategy for AOFlagger" alongside the morphology-convolution method that `lofarSun.BF.RFIconvFlag`
  implements. A user choosing between RFI flaggers for solar LOFAR data is choosing between these two.

**3. python-casacore**
- https://github.com/casacore/python-casacore
- A domain-specific dependency whose presence characterises the software: it is what gives
  `lofarSun.cli.pyms_utils` access to CASA Measurement Sets (`get_obs_info_from_ms`, `get_t_from_ms`,
  `get_freq_from_ms`, `ms_datetime_to_index`), and it is the reason the package's platform support is
  constrained (see Field 20). It is a radio-interferometry library, not general infrastructure.

**4. lofarsunDocker**
- https://github.com/peijin94/lofarsunDocker
- The companion repository that builds the container images the documentation tells users to run.
  `docs/install.rst` links it by its former path `Pjer-zhang/lofarsunDocker`, which redirects to the
  URL above; `docs/interferometry.rst` gives the `docker run … peijin/lofarsun` and
  `singularity pull docker://peijin94/lincsun:latest` invocations. It is why Field 4 does *not* claim
  `Servers and Environments: Software or Environment Container` for this repository.

**Considered and rejected — the generic stack.** `setup.py` also requires matplotlib, numpy, scipy,
pandas, h5py, scikit-image, pyqt5 and torch. None belongs here. Each would be equally at home in a web
application, a finance model or a biology pipeline (or, for torch, in any deep-learning project), so
listing them would say nothing about `lofarSun` that isn't true of much of the ecosystem. h5py and
astropy in particular are dependency-present but exchange-absent: reading LOFAR HDF5 and FITS is
already recorded as format support in Field 18, which is the field that carries that information.

### 30. Interoperable Software (OPTIONAL)

Four entries, each with a specific documented exchange rather than a shared runtime.

**1. SunPy**
- https://github.com/sunpy/sunpy
- Shared data model with a converter API. `IMdata.make_map()` builds a WCS header with
  `sunpy.map.make_fitswcs_header(..., observatory='LOFAR')` and returns a `sunpy.map.Map` — rotated and
  cropped to a field of view — so a LOFAR interferometric image becomes a SunPy `GenericMap` that
  composites with any other SunPy map. `lofarSun/IM/IMdata.py` imports `sunpy.coordinates.frames` and
  `sunpy.coordinates.sun` for the helioprojective transform, `lofarSun/BF/lofarJ2000xySun.py` uses
  `sunpy.coordinates.sun.sky_position` and `P`, and `demo/demo_sunpymap.ipynb` exists specifically to
  demonstrate this handoff. The reference publication describes using the library for exactly this
  conversion.

**2. WSClean**
- https://gitlab.com/aroffringa/wsclean
- Bidirectional exchange with a named domain tool. `lofarSun` generates WSClean invocations
  (`cli/pyms_utils.cook_wsclean_cmd()`, exposed as the `pymsCookWscleanCMD` console script, with
  `utils/IM/commandlines/wsclean.sh`); it consumes WSClean's output images through `IMdata.load_fits()`;
  and it closes the loop by reading WSClean's PSF FITS and emitting a restoring-beam specification back
  into WSClean — `IM.get_peak_beam_from_psf()` / the `pymsPSFfitPeakGauss` script print
  `"[bmaj]asec [bmin]asec [bpa]deg"` for WSClean's `-beam-shape` option, as `docs/beam.rst` documents
  step by step. `paper.md`: "the 2DiFFT and de-convolution is done with `WSClean`".

**3. DP3 (Default PreProcessing Pipeline, DPPP)**
- https://git.astron.nl/RD/DP3
- `utils/IM/commandlines/auto_sun_calib.py` "generates the parset file for the calibration and runs the
  corresponding DPPP command" (`docs/interferometry.rst`), driving the gaincal → applycal → applybeam
  sequence; the lincSun CWL steps `dp3_make_parset_cal.cwl`, `dp3_prep_cal.cwl`, `dp3_prep_target.cwl`,
  `gaincal.cwl` and `applycal.cwl` wrap DP3 directly. `lofarSun` writes DP3's inputs and consumes its
  calibrated Measurement Sets.

**4. LoSoTo (LOFAR Solution Tool)**
- https://github.com/revoltek/losoto
- Exchange of H5parm calibration-solution tables. `utils/IM/LINC/lincSun/steps/LoSoTo.Plot.cwl` and
  `inspect_solutions.cwl` invoke LoSoTo on solution tables produced upstream in the workflow, and
  `docs/interferometry.rst` documents the `parmdb2H5parm.py` → `losoto … cal_solution_plot.parset`
  path for inspecting calibration solutions before imaging.

**Considered and rejected:** astropy (a Tier-B package used internally for FITS I/O, units, `Time` and
`EarthLocation`, but with no documented exchange of its own — the real domain interoperation runs
through SunPy, which is recorded); h5py, torch, matplotlib, numpy, scipy, pandas, scikit-image and
pyqt5 (dependency presence is not interoperability); and any claim resting on ecosystem membership —
"part of the scientific Python ecosystem" and "a PyHC community package, so it interoperates with PyHC
packages" are not evidence of interoperating with any particular package, and neither was used here.

### 31. Related Instruments (OPTIONAL)

**Value:** Not found — documented omission, resolved to the observatory instead.

**This is a correct outcome, not a gap, and it should not be "fixed" by inventing a value.** The prior
canonical file recorded `Instrument Name: LOFAR (Low Frequency Array)` with `Instrument Identifier: Not
found`. A name without a SPASE identifier is not submittable: HSSI's no-identifier fallback either
binds to an arbitrary same-name row or creates a new identifier-less row, reintroducing exactly the
legacy rows that were purged from this vocabulary. That value must not be carried forward.

**What the vocabulary actually contains.** HSSI's `InstrumentObservatory` list holds six rows
mentioning LOFAR, all of them SPASE-backed:

| type | name | identifier |
|---|---|---|
| 2 (observatory) | LOFAR | `https://spase-metadata.org/SMWG/Observatory/LOFAR` |
| 2 (observatory) | LOw Frequency ARray (LOFAR) | `https://spase-metadata.org/SMWG/Observatory/LOFAR.html` |
| 1 (instrument) | LOFAR FR606 HBA Standalone Receiver | `https://spase-metadata.org/SMWG/Instrument/SRN/FR606/HBA` |
| 1 (instrument) | LOFAR FR606 LBA Standalone Receiver | `https://spase-metadata.org/SMWG/Instrument/SRN/FR606/LBA` |
| 2 (observatory) | LOFAR FR606 High Band Array | `https://spase-metadata.org/SMWG/Observatory/SRN/FR606/HBA` |
| 2 (observatory) | LOFAR FR606 Low Band Array | `https://spase-metadata.org/SMWG/Observatory/SRN/FR606/LBA` |

**Why the two instrument rows are rejected.** Both are specific to FR606, the international LOFAR
station at Nançay operating in standalone mode. This software supports LOFAR solar observations
generally — core and international stations processed as an interferometer or as tied-array beams — and
contains no FR606-specific code: a case-insensitive search of all tracked files for `FR606`, `Nançay`
and `Nancay` returns no hits. Antenna-field labels (`LBA`, `HBA`) do appear throughout the calibration
scripts, workflows and docs, but they name the array's low- and high-band systems rather than any
station — `INSTRUME = "LBA"`, written into output FITS headers by `BFdata.write_fits()` and
`utils/BF/h5_to_fits_cube.py`, is such a label with no station attached. Where a station *is* named it
is a Dutch core station rather than FR606: `"refant": "CS002LBA"` in a lincSun example JSON, and the
`CS001HBA0` default reference antenna in `utils/IM/LINC/lincSun/steps/inspect_solutions.cwl` and
`utils/IM/LINC/lincSun/workflow/calibrator_sun.cwl`. Recording FR606 would assert support the software
does not have.

**Resolution applied.** There is no SPASE instrument record for LOFAR as such, so the resolution ladder
falls through to the observatory/platform record, which is recorded in Field 32. This follows the
established practice that a missing instrument record should not block the software's association. The
substitution is deliberate and complete: the field is empty by decision, with no unresolved or
ambiguous instrument entry standing behind it.

### 32. Related Observatories (OPTIONAL)

**Observatory 1:**
- **Observatory Name:** LOFAR
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/LOFAR

Resolved against HSSI's `InstrumentObservatory` vocabulary. Two rows describe this one entity — the
bare `SMWG/Observatory/LOFAR` and its `.html` twin `SMWG/Observatory/LOFAR.html`
("LOw Frequency ARray (LOFAR)"). These are the same SPASE resource in two identifier forms, not a
genuine collision between two candidates, so the non-`.html` row is used and the row's `name` is copied
verbatim as `LOFAR`. The four FR606 station rows describe different entities and are excluded for the
reasons given in Field 31. Nothing here is ambiguous.

**Why the software is designed to support LOFAR** — this is not a passing mention. The package is named
for it; `setup.py`'s description is "tools to process the lofar solar data"; it parses LOFAR beamformed
HDF5 layouts (`SUB_ARRAY_POINTING_*/BEAM_*/STOKES_*`) and LOFAR Measurement Sets; it writes
`TELESCOP = "LOFAR"` into its output FITS headers; `IMdata.make_map()` hard-codes the array's geodetic
position (`EarthLocation(lat=52.905329712*u.deg, lon=6.867996528*u.deg)`) as the observer for the
helioprojective transform and passes `observatory='LOFAR'` to the WCS header builder; and the whole
`utils/IM/LINC/` tree is a LOFAR calibration and imaging pipeline. A user searching HSSI for
`observatory:"LOFAR"` should certainly get this package back.

**Rendering caveat:** HSSI's view layer may render this entry as `name (abbreviation)`. The stored
value is the bare name `LOFAR` together with the SPASE identifier above; comparisons should be made
against those, not against the rendered string.

### 33. Logo (OPTIONAL)

**Value:** https://lofar-sun-tools.readthedocs.io/en/latest/_static/logo0.png

Retained. The stored HSSI value, identical to the PyHC registry's `logo` field, and it resolves (200).
It is served from the published documentation build of `docs/img/logo0.png`, which is in the
repository, so it is as permanent as the documentation itself. 66 characters, well under the URL limit.

---

## Upstream limitations and follow-ups

Durable facts about this software that will still be true on a later refresh, recorded so they are not
rediscovered from scratch:

- **No git tags, no GitHub releases, no CHANGELOG.** Every version question therefore has to be answered
  from `setup.py` history (`git log -L '/version = /,+1:setup.py'`) and PyPI upload timestamps. There is
  no authoritative release date for any version other than what PyPI recorded.
- **The declared version has outrun the published one.** `setup.py` says 0.3.33; PyPI's latest is
  0.3.32. Unless a new release appears, this divergence will persist and Field 12 will keep needing the
  explanation in that field's note.
- **The JOSS paper draft is complete but unsubmitted**, with an unedited placeholder ORCID. If it is
  ever published, its DOI becomes the natural Field 14 value and would displace the arXiv preprint.
- **The GitHub–Zenodo integration was used once (v0.1.0, 2021) and abandoned.** The concept DOI is
  therefore valid but its title still carries the repository's former name, `Pjer-zhang/LOFAR_Solar`.
  New releases will not appear under it unless the integration is re-enabled.
- **`python-casacore` constrains the platform story** and will keep doing so; it is a hard
  `install_requires` entry with Linux-only PyPI wheels.
- **`README.md`'s test-data link is dead** (`https://pjzhang.cc/static/demo_data.7z`, 404), so the
  `demo/` notebooks have no runnable input from the documented source.
- **An organization author cannot be recorded safely without a ROR.** This matters concretely here
  because `paper.md` credits "LOFAR SSWKSP" as an author and no ROR exists for it (Field 6). Any future
  attempt to add it should expect the identifier problem, not rediscover it.
