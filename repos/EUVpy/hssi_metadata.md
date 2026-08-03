# HSSI Metadata Extraction Results

**HSSI Software ID:** 2fd43ecd-9910-48f4-bf08-f07a4445cdf2
**Repository:** https://github.com/DanBrandt/EUVpy
**Source Revision:** 52f72d874a616f4e75b2d2f37424b0c2e6de9eac
**Extraction Date:** 2026-08-03
**Validation Date:** 2026-08-03
**Validation Status:** PASS

---

**Scope note.** Three facts change how the repository evidence below should be read.

1. `.gitmodules` declares a submodule at
   `src/EUVpy/empiricalModels/models/HEUVAC/HEUVAC` pointing at
   `https://github.com/DanBrandt/HEUVAC.git`, but no such path exists in the working tree and
   initialising submodules produces nothing. The HEUVAC Fortran that the package actually compiles
   and runs lives in-tree at `src/EUVpy/empiricalModels/models/HEUVAC/srcHeuvac/`. The submodule
   declaration is stale and unused; all HEUVAC evidence cited below is from `srcHeuvac/`.
2. `.gitignore` excludes `src/EUVpy/solarIndices`, `src/EUVpy/empiricalModels/irradiances`, and
   `measurements`. The README describes those directories, but they are runtime download targets
   rather than committed content, so absence of F10.7 or irradiance data files in the tree is not
   evidence that the corresponding readers are unused.
3. Two build artefacts are committed to the repository and are not excluded by `.gitignore`:
   `build/lib/EUVpy/` (29 tracked files, 26 of them `.py`) is a stale duplicate of the package as it
   stood at an earlier packaging step, and `docs/build/html/` (139 tracked files) is a built Sphinx
   site. Any repository-wide file count or text search therefore double-counts the package, and
   `build/lib/` additionally preserves a module with no counterpart in the source tree at all -
   `build/lib/EUVpy/empiricalModels/models/HEUVAC/old/heuvac.py`, whose `old/` directory does not
   exist under `src/`. All evidence cited below is drawn from `src/`, `tests/`, `docs/source/` and
   the repository root; nothing is drawn from `build/` or `docs/build/`. A future refresh should
   expect these directories to still be present and should not read their contents as current code.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The original submitter is not named in HSSI's published metadata for this record and cannot be
recovered from it, so both of these fields are placeholders.

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.13685578

Carried over from the existing HSSI record and confirmed correct. This is the Zenodo **concept**
DOI (`conceptdoi` on the Zenodo record, `conceptrecid` 13685578), which resolves to all versions and
is the right choice for Field 2. The version-level DOI `https://doi.org/10.5281/zenodo.13685579`
belongs to Field 12 and is discussed there. Exactly one version exists on Zenodo.

### 3. Code Repository (MANDATORY)
https://github.com/DanBrandt/EUVpy

Carried over from the existing HSSI record and confirmed correct: the base repository URL, not a
`/tree/<ref>` page URL. The PyHC registry records the code location as
`https://github.com/DanBrandt/EUVpy/tree/main`, and Zenodo's related identifier is
`https://github.com/DanBrandt/EUVpy/tree/1.0-prealpha`; both are branch/tag page URLs and neither is
preferred here. The repository is public, not archived, and its default branch is `main`.

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Forecasting
- Models and Simulations: Forward-Fitting

Each subcategory above is listed together with its parent category, as the `FunctionCategory`
taxonomy requires; the bare parent entries are deliberate, not redundant.

Only `Models and Simulations` and `Models and Simulations: Empirical` were previously recorded.
Those two remain correct but describe a small fraction of the package: roughly half of EUVpy's
source is data retrieval, rebinning, statistics, plotting and format conversion rather than model
evaluation. Each addition below is tied to specific code.

- **Models and Simulations**, with **Models and Simulations: Empirical** — NEUVAC, EUVAC, HEUVAC and
  HFG (SOLOMON) are all empirical
  irradiance models parameterized by the F10.7 radio-flux proxy
  (`NEUVAC/neuvac.py:neuvacEUV`, `empiricalModels/models/EUVAC/euvac.py:euvac`,
  `.../HEUVAC/heuvac.py:heuvac`, `.../SOLOMON/solomon.py:solomon`).
- **Models and Simulations: Data Guided** — every model requires observed F10.7 (and its 81-day
  centred and 54-day backward-looking averages) as its driving input, and the NEUVAC coefficient
  tables in `data/neuvac_table.txt` were derived by fitting to observed FISM2 spectra.
- **Models and Simulations: Forecasting** — NEUVAC exists specifically to supply present-day EUV
  estimates where FISM2 lags 54 days (`docs/source/methods.rst`), and the reference publication
  frames it as "applicable for solar EUV forecasting". `tools/toolbox.py` additionally implements
  `forecast()` (linear minimum-MSE vector-autoregression forecast) and `forecastInversion()` for
  inverting forecasts of differenced, detrended series.
- **Models and Simulations: Forward-Fitting** — `neuvac.neuvacFit()` optimises the six NEUVAC
  parameters per wavelength band against FISM2 irradiances with `scipy.optimize.curve_fit`, and
  `experiments/fitNeuvac.py` drives that fit; `experiments/uncIrradiance.py` fits residual
  relationships the same way. This is forward-model parameter optimisation, not a physics solver.
- **Data Processing and Analysis: Data Access and Retrieval** — `tools/processIrradiances.py:getIrr`
  downloads FISM2 daily, FISM2 standard-band, and TIMED/SEE Level 3 files from LASP;
  `tools/processIndices.py:getCLSF107` retrieves the CLS F10.7 file over FTP;
  `tools/processIndices.py:getF107` posts to the OMNIWeb CGI to retrieve OMNI2 F10.7;
  `tools/EUV/fism2_process.py:download_fism2` fetches FISM2 daily or flare series from the LISIRD
  LaTiS endpoint; `tools/toolbox.py:urlObtain` is the shared download helper.
- **Data Processing and Analysis: Data Reduction** — `toolbox.rebin()` and `toolbox.newbins()`,
  plus `fism2_process.rebin_fism()` and `isolate_fism()`, reduce high-resolution spectra into
  coarser band schemes (the 59-bin GITM/Aether scheme, the 37 EUVAC/Torr bins, and the 22
  overlapping Solomon and Qian standard bands). `toolbox.uniformSample()` resamples to a fixed
  cadence.
- **Data Processing and Analysis: Processing** — the two dedicated pipeline modules
  `tools/processIndices.py` and `tools/processIrradiances.py`, plus the cleaning chain
  `cleanF107()` -> `F107filter()` -> `rollingAverage()` used inside `getF107`, and
  `toolbox.gapify()` / `toolbox.imputeData()`.
- **Data Processing and Analysis: Analysis** — derived statistics throughout `tools/toolbox.py`:
  `binRMSE`, `binCorrelation`, `get_cc`, `mycorrelate2d`, `squareDiff`, `mape`, `percDev`,
  `bestPolyfit`, `corrCol`, `normalize`; `experiments/analyzeIrradiance.py` uses them to quantify
  how NEUVAC compares with EUVAC, HEUVAC, HFG and FISM2. Model-versus-observation comparison is a
  headline capability, not incidental.
- **Data Processing and Analysis: Time Series Analysis** — `rollingAverage` and `rollingStd`
  (81-day centred and 54-day backward windows), the `F107filter` running-mean +/- n-sigma outlier
  replacement, `uniformSample`, `fractionalDOY`, `gapify`, `imputeData`, and the `forecast` /
  `forecastInversion` pair, all operating on time-ordered index and irradiance series.
- **Data Processing and Analysis: File Format Conversion** — `toolbox.readFISM2()` converts a FISM2
  netCDF file into the GITM `.dat` layout (its docstring cites GITM's `srcData/FISM` directory);
  `neuvac.gitmNEUVAC()` writes a GITM EUV input file; `neuvac.aetherFile()` rewrites the NEUVAC
  coefficient table into Aether's `euv_59` CSV form; `fism2_process.py` converts LISIRD FISM CSV
  into plain or GITM-style `.dat`.
- **Data Processing and Analysis: Energy Spectra** — the package's primary product is a
  wavelength-resolved solar spectrum, and `tools/spectralAnalysis.py` converts between photon flux
  and spectral irradiance through the photon energy `hc/lambda`
  (`spectralIrradiance()`, `spectralFlux()`). `toolbox.band_info()` derives band boundaries for
  spectral display. `Energy Spectra` is the only spectral entry in the vocabulary; leaving it off
  would leave the software's central capability unrepresented. Considered and rejected as
  alternatives: `Data Processing and Analysis: Spectrogram` (no time-frequency transform anywhere)
  and `Data Visualization: Spectrogram` (spectra are drawn as stair/line plots, not dynamic
  spectra).
- **Data Visualization: Line Plots** — time series of irradiance and of ensemble spread in
  `experiments/analyzeIrradiance.py` and all four worked examples in `docs/source/examples.rst`
  (`plt.plot`, `fill_between`, `ax.stairs`); fit-diagnostic plots in `neuvac.neuvacFit()`;
  `toolbox.binRMSE` / `binCorrelation` / `corrCol` per-band plots. `savefig` appears 31 times
  across the package.
- **Data Visualization: 2D Graphics** — `experiments/uncIrradiance.py` renders the NEUVAC residual
  correlation matrices as `plt.imshow(..., cmap='bwr')` images with colour bars and writes them to
  PNG (`corMat.png`, `corMatStanBands.png`, `corMatsEUVAC.png`); `toolbox.plotHist()` draws
  histograms with a seaborn KDE overlay.

Considered and rejected, with reasons:

- **Coordinate Transforms** and all six of its children (`Heliospheric`, `Ionospheric`,
  `Magnetospheric`, `Mission-Specific`, `Planetary`, `Solar`) — the package contains no coordinate
  system,
  reference frame, or geomagnetic-coordinate handling of any kind. Wavelength rebinning is not a
  coordinate transform.
- **Mission-related** and its children — EUVpy reads TIMED/SEE and SDO/EVE science products but is
  not part of any mission's ground system, calibration chain, or operations. `Mission-related:
  Ingest` was specifically weighed and rejected: reading a published Level 3 file is data access,
  which is already recorded under `Data Processing and Analysis: Data Access and Retrieval`.
- **Servers and Environments** and its children — no server, no container definition, no MPI or
  other parallelism, no infrastructure-as-code. The only shell scripts are `install_heuvac.sh` and
  `builddocs.bash`, which compile Fortran and build Sphinx docs locally.
- **Models and Simulations: Physics-Based** and **First Principles** — all four models are empirical
  proxy parameterizations. `docs/source/methods.rst` explains the underlying emission physics as
  background, but no equation of state, transport equation or radiative-transfer calculation is
  solved.
- **Models and Simulations: Instrument Response** and
  **Models and Simulations: Observatory/Instrument Models** — the
  wavelength binning schemes match instrument and model band definitions but EUVpy does not model
  any instrument's response function or effective area.
- **Data Processing and Analysis: ML/AI** — the only candidate evidence in the package is
  `toolbox.imputeData()` (`src/EUVpy/tools/toolbox.py:186`), and it does not support the category.
  The function's `'gpr'` branch is prefaced by the author's own
  `# TODO: Fix the Gaussian Process approach below so that sensible values are imputed:`, fits an
  `sklearn.gaussian_process.GaussianProcessRegressor` with an RBF kernel, computes
  `yMeanPred, yStdPred` - and then never assigns `cleanData`, so control falls through to
  `return cleanTimes, np.squeeze(cleanData)` and the call raises `UnboundLocalError`. That branch is
  abandoned scaffolding, not a feature. The `'gam'` branch (`pygam.LinearGAM`, lines 238-247) does
  work. But `imputeData` is never called anywhere in the live source tree: the only references under
  `src/` are the import at `tools/processIndices.py:18` and a commented-out call at
  `tools/processIndices.py:437`, and nothing in `tests/` exercises it. An active call does exist at
  `build/lib/EUVpy/tools/processIndices.py:377`, but that is the stale committed build artefact
  described in the scope note and must not be read as a live call site. The package's entire
  ML-adjacent surface is that one unreachable function: `sklearn.impute`,
  `sklearn.gaussian_process` and `pygam` appear nowhere else under `src/`, and the only other
  scikit-learn import is `sklearn.metrics.mean_squared_error` (`toolbox.py:20`), used once at
  `toolbox.py:629` with `squared=False` to compute an RMSE. Substantively, NEUVAC is a least-squares
  parameterization of F10.7 predictors against FISM2 irradiance (`neuvac.neuvacFit()` calling
  `scipy.optimize.curve_fit` at `neuvac.py:357`) - curve fitting, not machine learning. A user
  filtering HSSI for ML/AI expects software in which a learned model does the work, and this entry
  would mislead them.

  This value was previously recorded, on the reasoning that the working GAM path is a documented,
  user-selectable option of a public function and therefore a user-facing capability. It was
  corrected because that reasoning did not account for the function having no live caller: an option
  no code path can reach is not a capability the software offers. Note that `imputeData` still
  appears in the evidence for `Data Processing and Analysis: Processing` and for
  `Data Processing and Analysis: Time Series Analysis`, where it is one item among many working,
  exercised functions and is cited as part of those modules' gap-handling surface; it is only when
  asked to carry a category by itself that it fails. Dropping this value does not orphan its parent:
  `Data Processing and Analysis` retains seven other selected children (`Analysis`,
  `Data Access and Retrieval`, `Data Reduction`, `Energy Spectra`, `File Format Conversion`,
  `Processing`, `Time Series Analysis`), so the parent category remains correctly listed.

- **Data Processing and Analysis: Calibration** — the F10.7 readers distinguish observed from
  1 AU-adjusted values and consume CLS flare-corrected, Sun-Earth-distance-adjusted fluxes, but
  EUVpy consumes those calibrated products rather than producing them.
- **Data Processing and Analysis: Data Assimilation** — no assimilation scheme; NEUVAC is fitted
  offline, not updated from a data stream.
- **Data Processing and Analysis: Image Processing** — the only images are output figures.
- The remaining **Data Visualization** children — `Movies`, `3D Graphics`, `Web-Based`,
  `Orbit Plots`, `Hodograms`, `Spacecraft Formation Plots`, `Mission-Specific`, `ML/AI`,
  `2D Slices`, `Spectrogram` — none of these plot types occurs; the package sets the interactive
  `Qt5Agg` backend and produces static Matplotlib figures.

### 5. Related Region (MANDATORY)
- Solar Environment
- Earth Thermosphere
- Earth Ionosphere

`Solar Environment` is carried over from the existing HSSI record and is correct: the modelled
quantity is solar EUV irradiance.

`Earth Thermosphere` and `Earth Ionosphere` are added because supplying EUV to Earth's upper
atmosphere is the software's declared purpose, not a side use. The README opens with "for use
primarily in thermosphere-ionosphere models"; `docs/source/index.rst` states the code contains EUV
models "for use by atmospheric models primarily used in the space weather community (such as GITM,
TIE-GCM, and WACCM-X)"; the reference publication describes providing quantified uncertainties "for
usage by downstream ionosphere-thermosphere models"; and the package ships concrete output paths
into two thermosphere-ionosphere models (`neuvac.gitmNEUVAC()`, `neuvac.aetherFile()`). The NEUVAC
acronym itself expands to "for Aeronomic Calculations".

Considered and rejected:

- `Earth Atmosphere` and `Earth Lower and Middle Atmosphere` — the specific thermosphere and
  ionosphere rows are preferred over the broad one, per the guidance to choose the most specific
  applicable region. WACCM-X is named once in `index.rst` as a possible downstream consumer, which
  is not enough to claim lower- and middle-atmosphere functionality.
- `Corona`, `Chromosphere`, `Photosphere` — `docs/source/methods.rst` notes that solar EUV
  originates across altitudes "extending from the Photosphere to the Corona", but that is background
  physics. EUVpy produces disk-integrated irradiance and offers no region-resolved solar
  functionality, so a user filtering on those regions would not be served by it.
- `Solar Wind`, `Interplanetary Space`, and all magnetospheric rows — no functionality.

### 6. Authors (MANDATORY)

**Author 1 — Daniel Brandt**
- **Author Identifier:** https://orcid.org/0000-0003-3034-5440
- **Affiliation:** Michigan Tech Research Institute
- **Affiliation Identifier:** Not found

Carried over from the existing HSSI record. The ORCID is confirmed by the reference publication,
whose Crossref record gives `Daniel A. Brandt`, ORCID `0000-0003-3034-5440`, affiliated
"Michigan Tech Research Institute - Michigan Technological University, Ann Arbor MI USA". The
affiliation is current: his ORCID employment record lists Michigan Tech Research Institute,
Research Scientist, from 2021-08-23 with no end date. `setup.py` gives
`author="Daniel A. Brandt"`, `author_email="daabrand@mtu.edu"`, and he is the author of 53 of the
repository's 63 commits. He commits under two addresses: 52 commits from `daabrand@mtu.edu` (51 as
`Daniel A. Brandt`, one as `Daniel Brandt`) and the initial commit 652ace7 from the personal address
`Daniel Brandt <brandtadaniel@protonmail.com>`. Both addresses are recorded because a count keyed on
`daabrand@mtu.edu` alone undercounts him by one and makes the initial commit look like a separate
contributor's.

The name form recorded here is given name `Daniel`, family name `Brandt`, while `setup.py`, the
Crossref record for the reference publication, and the publication itself all credit the fuller form
`Daniel A. Brandt`. `Daniel A. Brandt` is the correct target form, and that correction has not been
applied to the recorded given and family name; a future refresh able to carry it through should
apply it.

**Author 2 — Aaron J. Ridley**
- **Author Identifier:** https://orcid.org/0000-0001-6933-8534
- **Affiliation:** University of Michigan
- **Affiliation Identifier:** https://ror.org/00jmfr291

Added. The README states plainly: "Conceptual development was carried out by Dr. Aaron J. Ridley and
analysis and contributions were made by Dr. Daniel A. Brandt and Dr. Joseph Paki." He is the second
author of the reference publication (Crossref: given `Aaron J.`, family `Ridley`, ORCID
`0000-0001-6933-8534`, "Department of Climate and Space Sciences and Engineering University of
Michigan"). His ORCID record confirms University of Michigan, Department of Climate and Space
Science and Engineering, Professor, from 2000 with no end date.

The strongest in-repository evidence for his authorship is the module header at the top of
`src/EUVpy/NEUVAC/neuvac.py:3-5` - the primary NEUVAC implementation, and the flagship module of the
package - which reads "# Developed by: / # Aaron J. Ridley, Ph.D. / # Daniel A. Brandt, Ph.D." That
is a direct development credit at the head of the package's central file, and it names Ridley first.
Three further code-level credits corroborate it:

- `src/EUVpy/experiments/fitNeuvac.py:98` and `:153` write
  `File Authors: Brandt, Daniel A. and Ridley, Aaron J.` into the headers of the two coefficient
  tables the fitting experiment generates.
- Both generated tables are checked into the repository still carrying that line, at
  `src/EUVpy/data/neuvac_table.txt:4` and `src/EUVpy/data/neuvac_table_stan_bands.txt:4`, so the
  attribution is present in the shipped data as well as in the code that emits it.
- The `obtainFism1` docstring at `src/EUVpy/tools/processIrradiances.py:120` reads "Given muliple
  FISM1 .dat files, get the information from each band, using code developed by Dr. Aaron Ridley."

`src/EUVpy/NEUVAC/neuvac.py:137` additionally cites "Brandt and Ridley, 2025
(doi:10.1029/2024SW004043)" in the `neuvacEUV` docstring; that is a bibliographic citation of the
reference publication rather than a code authorship credit, and is noted only so it is not
double-counted as one. The docstring's "2025" is a slip on the authors' part: the DOI it quotes is
Crossref-confirmed as the December 2024 *Space Weather* article, so a future refresh should not go
looking for a second Brandt and Ridley paper. Field 14's 2024 publication date is unaffected - it was
taken from Crossref and DataCite, not from this docstring.

Negative research on the one module that looks like it should carry a credit and does not:
`src/EUVpy/tools/EUV/fism2_process.py` contains no attribution of any kind. Its only occurrences of
the name are a commented-out `ridleyIrr` coefficient array (line 357) and the commented-out
`plt.plot(..., label='RIDLEY')` call that consumed it (line 373) - dead comparison code, not
authorship - so a future refresh should not cite that module as evidence here.
`docs/source/index.rst:20` separately credits him with the Aether model, which is a different
piece of software and not an EUVpy authorship credit.

None of these code-level credits name Joseph Paki; see Author 3 for why that is not evidence against
his authorship.

The given name is recorded as `Aaron J.` to match both the README's credit and the reference
publication; the ORCID registry's own name field
omits the middle initial ("Aaron"), which is a less specific form of the same name rather than a
conflict.

Organization choice: the affiliation is recorded at the university level as
`University of Michigan` rather than as the department, because the university is the organisation
that has a ROR of its own, `https://ror.org/00jmfr291`.
`Department of Climate and Space Sciences and Engineering` - the unit named by both Crossref and
ORCID - has no ROR. One near-miss is named here so it is not substituted:
`Department of Astronomy, University of Michigan` is a different department of the same university
and does not describe this author's affiliation. The ORCID employment entry's RINGGOLD
disambiguation id (1259) agrees with University of Michigan, and its city/region/country (Ann Arbor,
MI, US) agree with Crossref.

**Author 3 — Joseph Paki**
- **Author Identifier:** https://orcid.org/0000-0002-4936-218X
- **Affiliation:** Michigan Tech Research Institute
- **Affiliation Identifier:** Not found

Added. The README credits "Dr. Joseph Paki" for analysis and contributions, and the git history
corroborates substantive work: 10 commits authored by `jepaki <jepaki@mtu.edu>` covering the
`processIndices` unit tests, the pathlib-based data-path refactor, docstring fixes, `setup.py`
packaging changes, and the example Jupyter notebook. ORCID `0000-0002-4936-218X` is the only
`Joseph Paki` in the ORCID registry, and its employment record gives Michigan Tech Research
Institute, Research Scientist, from 2019-07 with no end date, in Ann Arbor MI - the same institute
as Daniel Brandt and consistent with the `@mtu.edu` commit address. He is not an author of the
reference publication, which is why the union across the README, the git history, and the
publication is needed rather than the publication alone.

The code-level credits described under Author 2 - the `neuvac.py` "Developed by" header and the
`fitNeuvac.py` generated-table author lines - name only Ridley and Brandt, never Paki. That is not a
contradiction of his authorship, and a future refresh should not read it as one. Those two credits
are scoped to the NEUVAC model implementation and to the coefficient tables fitted from it, which
are Ridley's and Brandt's work, and would not be expected to name a later contributor whatever parts
of the package he went on to touch. Paki's other contributions are the `processIndices` unit tests,
the pathlib data-path refactor, the `setup.py` packaging changes, the example Jupyter notebook, and a
later docstring-formatting pass over `neuvac.py` itself. Two of his commits do modify the flagship
module: the pathlib refactor `0df7a83` (2025-07-15, "Udpating paths to models"), whose single
`neuvac.py` hunk is at line 148 inside `neuvacEUV`; and `d1fd4f5` (2025-07-21, "Fixing some
docstrings in neuvac, making docs"), which rewrites the `neuvacFit`, `gitmNEUVAC` and `aetherFile`
docstrings - hunks at post-commit lines 255, 364 and 410 - from the multi-line `:param name: type`
form into Sphinx one-line info fields (`:param str tableFile: ...`), and annotates `aetherFile`'s
`tableFile` parameter as `str`. Neither commit goes near the `:3-5` credit header, `d1fd4f5`'s
earliest `neuvac.py` hunk beginning at line 255, and neither - nor any other commit of his - touches
`src/EUVpy/experiments/fitNeuvac.py`; the only `fitNeuvac` path in `d1fd4f5` is the renamed generated
autodoc stub `docs/source/EUVpy.experiments.fitNeuvac.rst`. Outside `neuvac.py`, `d1fd4f5`'s
source-tree changes are one added blank line in
`src/EUVpy/empiricalModels/models/SOLOMON/solomon.py` (that docstring's own text is untouched), the
deletion of `src/__init__.py`, an added `HEUVAC-scratch.TXT` scratch file, refreshed
`src/EUVpy.egg-info` files, and a full Sphinx regeneration that renames `docs/source/src.EUVpy.*.rst`
to `docs/source/EUVpy.*.rst` and rebuilds `docs/build/`; the commit spans 203 paths, only 57 of them
outside `docs/build/`. His evidence basis is therefore the README's "analysis and contributions"
credit plus the git history, with the ORCID registry supplying the identifier and affiliation - not
the source-file headers, which should not be expected to name him.

`git blame` understates this author and should not be used to weigh his contribution. Today's
`neuvac.py` attributes only three lines to `jepaki` - the `aetherFile` signature and two blank
lines - because Brandt reformatted every docstring in the package to numpydoc the day after
`d1fd4f5` (`fa08c1a3`, 2025-07-22, "Fixed all docstrings to adhere to numpydoc format."),
superseding most of it. The commit history, not surviving-line counts, is the reliable record here.

Field-wide notes:

- No `CITATION.cff`, `codemeta.json`, `.zenodo.json`, `AUTHORS`, or `CONTRIBUTORS` file exists in
  the repository, so the README credit statement and the git history are the authoritative
  in-repository author evidence. The absence of a citation file is also why the Zenodo and DataCite
  records list Daniel Brandt alone: Zenodo's GitHub integration falls back to the repository owner.
  That single-creator DOI record is therefore not evidence against Ridley's and Paki's authorship.
- No author was removed. Ordering places Brandt first (sole `setup.py` author, first author of the
  reference publication, majority of commits), then Ridley (conceptual originator, second author of
  the publication), then Paki (contributor), matching the order in which the README introduces them.
- `Michigan Tech Research Institute` has no ROR. Searching ROR for both the full name and the
  acronym returns only unrelated organisations (the `MTRI` acronym belongs to Middle Tennessee
  Research Institute). MTRI is a research institute of Michigan Technological University, whose ROR
  is `https://ror.org/0036rpn28`; that identifier was deliberately **not** attached here, because
  labelling the institute with the parent university's ROR would misidentify the organisation. The
  institute is therefore recorded by name alone, with no affiliation identifier, for both Brandt and
  Paki.
- Considered and not selected: adding `University of Michigan` as a second affiliation for Daniel
  Brandt. His ORCID record does list it, but with no start or end date, so it cannot be
  distinguished from a completed doctoral affiliation, and both the reference publication and the
  package metadata give Michigan Tech Research Institute exclusively. Recorded here so a future
  refresh does not have to re-derive it.

### 7. Software Name (MANDATORY)
EUVpy

Carried over from the existing HSSI record and confirmed by every independent source: the repository
name, `setup.py` `name="EUVpy"`, the PyPI project name, the Sphinx `project = 'EUVpy'`, the PyHC
registry entry, and the Zenodo title `DanBrandt/EUVpy: EUVpy Pre-alpha Release 1`. The mixed case
with a lowercase `py` suffix is the maintainer's own styling and is preserved exactly.

### 8. Description (MANDATORY)
EUVpy is a Python package that brings the most widely used empirical models of solar extreme
ultraviolet (EUV) irradiance together behind a single, consistent interface, primarily so that they
can drive thermosphere-ionosphere models. It provides NEUVAC (the Nonlinear Extreme Ultraviolet
Irradiance Model for Aeronomic Calculations), EUVAC, HEUVAC, and HFG (also referred to as SOLOMON).
Each model is parameterized by the 10.7 cm solar radio flux (F10.7) and quantities derived from it -
the 81-day average centred on the current day and a 54-day backward-looking average - so a full EUV
spectrum can be produced from a readily available ground-based index alone. Spectra can be generated
in several binning schemes, including the 59-bin scheme used by the Global Ionosphere-Thermosphere
Model (GITM) and the Aether model, the 37 bins of EUVAC and of Torr, and the 22 overlapping standard
bands of Solomon and Qian (2005).

Alongside running the models, EUVpy retrieves and cleans the data they need and are judged against.
It can download F10.7 from NASA OMNIWeb and flare-corrected, Sun-Earth-distance-adjusted radio flux
from Collecte Localisation Satellites, read Penticton F10.7 files, and gap-fill, filter and average
those series. It can download and read solar spectral irradiance from FISM2 (through LISIRD, in both
native and standard-band form), TIMED/SEE Level 3, SDO/EVE, and NRLSSI2, rebin any of those spectra
into the supported band schemes, and convert between spectral irradiance and photon flux. It
computes comparison statistics between models and observations, including root-mean-square error,
correlation, mean absolute percentage error and percent deviation, and can generate NEUVAC
irradiance ensembles from a residual correlation matrix so that quantified uncertainties can be
passed to downstream models. Results can be written directly as a GITM EUV input file or as an
Aether coefficient table.

Two assumptions are worth knowing before use. NEUVAC is the model developed with this package and
is the only one for which running ensembles is recommended; the EUVAC, HEUVAC and HFG
implementations are included primarily so that NEUVAC can be compared against them. HEUVAC is a
Fortran code that must be compiled once with gfortran before it can be called, and the package has
so far been tested only on Ubuntu Linux. Users should cite the original authors of whichever model
or dataset they use, as set out in the repository's README.

This replaces the stored description, which was an unedited concatenation of three separate sources
(the GitHub repository blurb, the `setup.py` summary, and the opening of the README) that repeated
the same statement twice, retained the README's hard line wrapping, and ended mid-sentence with a
dangling colon where the README's citation list had been cut off - so the record advertised a
citation requirement and then omitted it. The replacement keeps the maintainer's own framing
("a Python wrapper for empirical solar EUV models", "for use primarily in thermosphere-ionosphere
models") and every factual claim it made, adds the capabilities actually present in the code, states
the assumptions the form asks for, and preserves the citation requirement as a pointer to the README
rather than as a truncated fragment. Sources: README, `docs/source/index.rst`,
`docs/source/methods.rst`, `docs/source/examples.rst`, and the module docstrings named in Field 4.

### 9. Concise Description (OPTIONAL)
A Python wrapper for empirical solar extreme ultraviolet (EUV) models (NEUVAC, EUVAC, HEUVAC, HFG) that generates, compares, and exports EUV spectra for thermosphere-ionosphere modeling.

186 characters, within the field's 200-character limit.

The opening clause is the maintainer's own GitHub repository description
("A Python wrapper for empirical solar extreme ultraviolet (EUV) models for solar-terrestrial
physics applications."), kept because it is how the author chooses to summarise the package; the
remainder names the four models and the intended use, which the original one-liner leaves implicit.
Alternatives considered and not used: the GitHub blurb verbatim (113 characters including its
trailing period, but names no model and describes the application domain rather than what the
software does); the `setup.py` and PyPI summary "A Python package for modeling Solar EUV
irradiance." (51 characters, accurate but omits the retrieval, comparison and export capabilities
that distinguish EUVpy from a single model); and the PyHC registry's "A Python package containing
several models for solar EUV irradiance." (68 characters, same limitation). All three are subsets of
the value recorded here.

### 10. Publication Date (RECOMMENDED)
2024-09-04

This replaces the stored `2024-08-29`. Both dates are real, and their provenance is what settles
the choice:

- `2024-09-04` is when the software's initial version was published. Two independent authoritative
  records agree: the GitHub release `1.0-prealpha` has `published_at` 2024-09-04T18:11:01Z, and the
  Zenodo record (and its DataCite registration) give `publication_date` / `Issued` 2024-09-04.
- `2024-08-29` is the date the GitHub repository was created (`created_at`
  2024-08-29T13:46:47Z), which is also the date of the initial commit
  (652ace7, 2024-08-29 09:46:47 -0400). It is not the publication of any version; it entered the
  record because HSSI's autofill cascade lets the repository-scraping stage overwrite Field 10 with
  the repository creation date after the DOI stage has already supplied the Issued date.

Field 10 is defined as the date of first publication, used for the initial version of the software.
The initial version is `1.0-prealpha`, and it was published on 2024-09-04. Also noted for
completeness, and rejected: the `1.0-prealpha` git tag points at commit b76e2e3 dated 2024-08-30,
five days before the release was published; tag creation is not publication either.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Carried over from the existing HSSI record and confirmed correct. The DOI was obtained through the
GitHub-Zenodo workflow, and DataCite records `publisher: "Zenodo"`; Field 11 names Zenodo as the
correct entry in exactly this situation. Zenodo has no ROR, so the organisation URL
`https://zenodo.org` is used, which is the form Field 11 prescribes as the fallback.

### 12. Version (RECOMMENDED)
- **Version Number:** 1.0.0
- **Version Date:** 2025-08-11
- **Version PID:** Not found
- **Version Description:** First packaged release. EUVpy became installable from the Python Package
  Index; the source tree was reorganised into a `src/` layout with pathlib-based resolution of
  bundled data files; a pytest suite was added covering NEUVAC, the NEUVAC ensemble generator,
  EUVAC, HEUVAC, SOLOMON, the solar-index processing tools, and the GITM output writer; all
  docstrings were converted to numpydoc format; Sphinx documentation with four worked examples was
  published on Read the Docs; an `install_heuvac.sh` helper was added to compile the HEUVAC Fortran
  in one step; an Aether coefficient export was added; and an example Jupyter notebook was included.

This replaces the stored version row, which recorded `Version 1.0-prealpha`, release date
2024-09-04, and version PID `https://doi.org/10.5281/zenodo.13685579`. Three separate corrections
are involved.

1. **The number was stale.** `1.0.0` is the current release: `setup.py` declares
   `version="1.0.0"`, `docs/source/conf.py` declares `version = '1.0.0'`, and PyPI published
   `EUVpy 1.0.0` (both wheel and sdist) on 2025-08-11. `1.0-prealpha` remains the only git tag and
   the only Zenodo version, but it is a year behind the released package.
2. **The number contained the word "Version".** Field 12 stores a bare version identifier; the view
   layer renders it as `<software name> - <number>`, so the stored value displayed as
   "EUVpy - Version 1.0-prealpha". HSSI's convention is a bare number such as `1.0.0`; the stray
   word was an artefact of the earlier entry rather than part of the version's name.
3. **The version PID does not carry over.** `https://doi.org/10.5281/zenodo.13685579` is the
   version DOI of `1.0-prealpha` specifically, and Zenodo has no record for `1.0.0` - the Zenodo
   deposit was never refreshed for the packaged release. Attaching the prealpha DOI to `1.0.0`
   would misidentify the artefact, and no other authoritative version-level identifier exists
   (PyPI mints no DOI). The field is therefore left empty rather than filled with a near-match. The
   all-versions concept DOI remains recorded in Field 2, so the DOI linkage is not lost.

Release date evidence: the PyPI upload timestamps are 2025-08-11T20:50:57Z (wheel) and
2025-08-11T20:50:58Z (sdist), and the final commit of the release push is
2025-08-11 18:02:02 -0400 (2025-08-11T22:02:02Z). Both fall on 2025-08-11.

Version description evidence: the 59 commits between the `1.0-prealpha` tag and the pinned revision,
whose subjects document the packaging reorganisation ("First round of file structure reorganization
in preparation for packaging", the merged `packaging` branch), the test suite ("Implemented structure
for unit testing", "Completed inclusion of first pass of test cases"), the docstring conversion
("Fixed all docstrings to adhere to numpydoc format"), the Read the Docs setup ("Added
.readthedocs.yaml" and its follow-ups), `install_heuvac.sh` ("Added a bash script for installing
HEUVAC automatically"), the Aether export, and the notebook ("Added jupyter notebook example"). No
CHANGELOG or GitHub release exists for `1.0.0`, so the description is derived from that history
rather than quoted from release notes.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- Fortran90
- Fortran77
- IDL
- Other

`Python 3.x`, `Fortran90`, `IDL` and `Other` are carried over from the existing HSSI record;
`Fortran77` was added. Each of the five is justified by the tree, as set out below.

- **Python 3.x** — 23 `.py` files under `src/EUVpy/`; `python_requires=">=3.7, <4"` with
  `Programming Language :: Python :: 3 :: Only`. This is the package's language. A repository-wide
  count returns 60 `.py` files, which is not the size of the package: the extra 37 are the 26
  duplicates under the stale committed `build/lib/EUVpy/` tree described in the scope note, the 8
  modules of `tests/`, and `docs/source/conf.py`, `scripts/test.py` and `setup.py`.
- **IDL** — seven `.pro` files in `src/EUVpy/tools/LQIAN/` (`get_spectra.pro`, `put_spectra.pro`,
  `rebin.pro`, `getbins.pro`, `nm_to_hs.pro`, `hi_to_nm.pro`, `tlsm.pro`), a vendored set of
  spectrum rebinning utilities with their own ASCII input files under `LQIAN/input/`.
- **Fortran90** and **Fortran77** — the two files
  `src/EUVpy/empiricalModels/models/HEUVAC/srcHeuvac/HEUVAC.for` (3,341 lines) and
  `HEUVAC-Driver.for` (336 lines), Phil Richards' HEUVAC code and its driver, compiled by
  `srcHeuvac/compile.sh` with `gfortran -c -ffixed-line-length-132` into the `HEUVAC.exe` that
  `heuvac.py` invokes. They are the only Fortran anywhere in the package. Both vocabulary rows are
  recorded, and both are simultaneously true of these same two files; the reason is set out below so
  that a future refresh does not drop either one as redundant.

  **The code reads and behaves as fixed-form FORTRAN 77.** Every marker of the dialect is present:
  comments introduced by `C` in column 1, including 41 `C..` lines in `HEUVAC.for` and 19 in the
  driver plus the `C::::::::` section banners; continuation marked by `>` in column 6 (2,884 lines in
  `HEUVAC.for` - the file is mostly the F74113 reference-spectrum `DATA` blocks - and 12 in the
  driver); statement labels punched in columns 1-5 (7 in `HEUVAC.for`, 8 in the driver), targeted by
  the 7 and 2 `GO TO`/`GOTO` branches and attached to labelled `FORMAT` statements; `DATA` statements
  (31 and 1); all-caps source throughout; and implicit-length
  dummy arrays declared against an integer argument, `REAL LAM_EUV(IDIM)` and `REAL XS(15,IDIM)`
  style, 12 such declarations in `HEUVAC.for`. Tab-indented statement lines occur (111 and 67) but
  are a long-standing fixed-form vendor extension, not free-form source.

  **There are no Fortran 90 constructs at all.** No free-form source, no `MODULE`, no `CONTAINS`, no
  `INTERFACE`, no `::` declarations, no `INTENT()`, no `ALLOCATE`, no `KIND=`, no derived types, no
  `SELECT CASE`, no `DO WHILE`. One trap is worth recording, because it is the obvious way to get
  this wrong: searching for `::` returns 13 hits across the two files, and every single one is a
  `C::::::::::::` banner comment line such as
  `C:::::::::::::::::::::::::::::: HEUVAC ::::::::::::::::::::::::::::::::::::::`, not a declaration.
  Nothing from Fortran 95, 2003, 2008 or 2023 appears either.

  **The build asserts no standard.** `srcHeuvac/compile.sh` runs
  `gfortran -c -ffixed-line-length-132` on each file and links the objects; there is no `-std=` flag
  in it, and no `-std=` anywhere in the repository. The one dialect-affecting flag it does pass is
  itself a fixed-form setting.

  **The only non-F77 features are three extensions that Fortran 90 later standardised:**
  `IMPLICIT NONE` (9 occurrences in `HEUVAC.for`, 1 in the driver), `ENDDO` (19 in `HEUVAC.for` and 4
  in the driver's live code, with 10 more in commented-out driver code), and `!` end-of-line comments
  (on 143 code lines in `HEUVAC.for` and 51 in the driver). All three were widely available as
  vendor extensions to FORTRAN 77 before Fortran 90 blessed them.

  **Both rows therefore serve a real user, which is why both are listed.** `Fortran77` is the
  dialect anyone reading or maintaining these files is actually working in, and it is what someone
  searching HSSI for legacy fixed-form Fortran needs in order to find this package. `Fortran90` is
  the earliest published standard the source strictly conforms to, and it is what someone asking
  which standard a compiler must support needs. Neither is a restatement of the other. `Fortran90`
  was previously recorded alone, with `Fortran77` rejected on the grounds that the three extensions
  above make the source non-conforming F77. That reasoning was mistaken in treating the two rows as
  competing answers to one question: they answer different questions - which dialect the source is
  written in, and which standard a compiler must support - and both answers are true of these same
  two files.
- **Other** — the build and helper scripts that have no vocabulary row: the Bash scripts
  `install_heuvac.sh` and `builddocs.bash`, the shell scripts `srcHeuvac/compile.sh` and
  `tools/EUV/test.sh`, and the legacy Windows batch files `srcHeuvac/HEUVAC.bat` and
  `Delete-temp-files.bat`.

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1029/2024SW004043

Brandt, D. A., & Ridley, A. J. (2024). "NEUVAC: Nonlinear Extreme Ultraviolet Irradiance Model for
Aeronomic Calculations." *Space Weather*, 22(12), e2024SW004043. Confirmed via Crossref (journal,
volume, issue, article number, both authors with ORCIDs, published December 2024, CC-BY).

This is unambiguously the reference publication rather than merely a related one: it describes
NEUVAC, the model that EUVpy exists to deliver; the README's citation section names it first, under
NEUVAC; `docs/source/methods.rst` cites it as the source of the NEUVAC formulation; and its
acknowledgments name EUVpy explicitly as the package NEUVAC is part of. The papers describing the
other three models EUVpy implements are recorded in Field 27, and the papers describing the datasets
it ingests in Field 28.

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

The licence selected is the MIT License, recorded against its authoritative SPDX entry: SPDX short
identifier `MIT`, whose canonical page is `https://spdx.org/licenses/MIT`.

Evidence, three sources in agreement: the repository's root `LICENSE` file is the verbatim MIT
licence text ("MIT License, Copyright (c) 2023 Daniel Brandt"); `setup.py` carries the classifier
`License :: OSI Approved :: MIT License`, which PyPI republishes; and GitHub's own licence detection
reports `spdx_id: MIT` for the repository.

Rejected: `Creative Commons Attribution 4.0 International`. The Zenodo deposit records
`license: cc-by-4.0`, and DataCite mirrors that as `Creative Commons Attribution 4.0
International`. That is Zenodo's own error - CC-BY-4.0 is its default for a deposit where the
repository licence was not picked up - and it contradicts the licence file the author actually
shipped. HSSI's DOI autofill copies Zenodo's errors verbatim, which is why this field must be
derived from the repository. A future refresh should expect to see `cc-by-4.0` again from the DOI
record and should keep rejecting it unless the upstream Zenodo deposit is corrected.

Also noted, and deliberately not recorded as the software's licence: `src/EUVpy/tools/EUV/LICENSE`
is an Apache License 2.0 text covering the vendored FISM rebinning utilities in that subdirectory.
Field 15 records the licence assigned to this software as a whole, which is MIT; the Apache-2.0
component licence is a subdirectory notice, not the package licence.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- extreme ultraviolet
- solar terrestrial physics
- space weather
- solar irradiance
- f10.7
- aeronomy
- model-data comparison

`extreme ultraviolet` and `solar terrestrial physics` are carried over from the existing HSSI
record; the other five are additions, each justified below. All seven are lower case with one
concept per entry, matching the convention of the two carried-over values.

Evidence: `space weather` — the reference publication frames NEUVAC for "operational space weather
nowcasting and forecasting", and `docs/source/index.rst` describes the target models as those "used
in the space weather community". `solar irradiance` — the quantity every model in the package
produces; it is the `setup.py` summary's subject. `f10.7` — the sole driving input to all four
models, with a dedicated retrieval and cleaning module (`tools/processIndices.py`). `aeronomy` — the
final word of the NEUVAC acronym and the discipline the package serves. `model-data comparison` —
the README's stated second purpose, "running, comparing, and analyzing the performance of NEUVAC in
comparison to other empirical models", implemented in `experiments/analyzeIrradiance.py` and the
statistics helpers in `tools/toolbox.py`.

Considered and rejected, because Field 16 is for science keywords *not* already supported by another
metadata field:

- `thermosphere`, `ionosphere` — carried by Field 5 (`Earth Thermosphere`, `Earth Ionosphere`).
- `empirical model` — carried by Field 4 (`Models and Simulations: Empirical`).
- `python`, `python package` — carried by Field 13.
- `gitm` — a PyHC keyword for this package, but the GITM relationship is carried by Field 30 with
  much more precision.
- `solar` — PyHC lists it; too broad to add anything beyond Field 5's `Solar Environment`.
- `euv` — a near-duplicate of `extreme ultraviolet`, which is already recorded.
- `ionosphere_thermosphere_mesosphere` — a PyHC-internal taxonomy token rather than a science
  keyword.
- `spectra` — overlaps Field 4's `Energy Spectra`, which already carries the concept.

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- FTP/FTPS Directories
- OMNIWeb
- Observatory/Mission-specific

- **HTTP/HTTPS Directories** — `tools/processIrradiances.py:getIrr` fetches
  `https://lasp.colorado.edu/eve/data_access/eve_data/fism/daily_hr_data/daily_data.nc`,
  `.../fism/daily_bands/daily_bands.nc`, and
  `https://lasp.colorado.edu/data/timed_see/level3/latest_see_L3_merged.ncdf` through
  `tools/toolbox.py:urlObtain`; `tools/EUV/fism2_process.py:download_fism2` curls the LISIRD LaTiS
  endpoint `https://lasp.colorado.edu/lisird/latis/dap/fism_daily_hr.csv` (or `fism_flare_hr.csv`).
- **FTP/FTPS Directories** — `tools/processIndices.py:getCLSF107` retrieves
  `ftp://ftpsedr.cls.fr/pub/previsol/solarflux/observation/radio_flux_adjusted_observation.txt` with
  `urllib.request.urlretrieve`. This is the default F10.7 path in every documented example and in
  four of the eight tests.
- **OMNIWeb** — `tools/processIndices.py:getF107` posts an `omni2` hourly retrieval request to
  `https://omniweb.gsfc.nasa.gov/cgi/nx1.cgi`, and `readOMNI()` parses the resulting OMNIWeb
  listing plus its `.fmt` header file.
- **Observatory/Mission-specific** — TIMED/SEE Level 3 and SDO/EVE merged Level 3 products are read
  by instrument-specific parsers (`obtainSEE()`, `obtainSDO()`), which Field 17 directs to be marked
  observatory-specific with the missions named in Field 32; they are.

Considered and rejected: `CDAWeb`, `HAPI`, `The Virtual Solar Observatory.`, `Madrigal`, `AMDA`,
`SSCWeb`, `das2`, `TAP`, `VirES`, `GFZ`, `WDC`, `S3/Cloud-aware` — none is contacted anywhere in the
code. `Other` was also rejected: LISIRD and the LASP and CLS directories are already covered by the
generic HTTP and FTP rows, so `Other` would add nothing.

### 18. Input File Formats (RECOMMENDED)
- netCDF3/4
- csv
- ascii
- Other

- **netCDF3/4** — `netCDF4.Dataset` is used to read FISM2 daily and standard-band `.nc` files
  (`obtainFism2`), TIMED/SEE Level 3 `.ncdf` (`obtainSEE`), SDO/EVE merged `.ncdf` (`obtainSDO`),
  and NRLSSI2 `.nc` (`obtainNRLSSIS2`), plus `toolbox.readFISM2`.
- **csv** — `tools/EUV/fism2_process.py:read_euv_csv_file` parses the wavelength-bin definition
  files `euv.csv`, `euv_59.csv` and `data/euv_59_reference.csv`; `read_fism_csv_file` parses the
  LISIRD FISM CSV response.
- **ascii** — plain-text tables throughout: the NEUVAC coefficient tables
  `data/neuvac_table.txt` and `data/neuvac_table_stan_bands.txt` (`neuvac.neuvacEUV`,
  `neuvac.aetherFile`), the Penticton and CLS F10.7 text files (`readF107`, `readCLS`), the OMNIWeb
  listing and format files (`readOMNI`), the HEUVAC bin and flux files
  `srcHeuvac/Torr-37-bins.txt`, `XS-User-bins-10A.txt`, `flux-User-bins-10A.txt` (`getTorr`,
  `getFlux`), the FISM1 `.dat` files (`obtainFism1`), and the `.dat`/`.tab`/`.txt` inputs of the
  vendored IDL utilities.
- **Other** — Python pickles are genuine runtime inputs, not just caches: `ensemble.py` passes
  `experiments/corMat.pkl` and `experiments/sigma_NEUVAC.pkl` (and their standard-band
  counterparts) into `neuvac.neuvacEUV`, which loads them through `toolbox.loadPickle` to perturb
  the ensemble members. Pickle has no vocabulary row.

Considered and rejected: **HDF5**. `h5py>=3.9.0` appears in `requirements.txt` and h5py is listed in
`autodoc_mock_imports` in `docs/source/conf.py`, but nothing in `src/EUVpy` imports or uses it -
h5py was added to make the Read the Docs build succeed alongside netCDF4, not to read HDF5 files.
Also rejected: `IDL.sav` (the IDL utilities read and write ASCII with `openr`/`readf`/`printf`;
there is no `restore` or `.sav` anywhere), `CDF`, `FITS`, `JSON`, `Zarr`, and `ISTP-Compliant`, none
of which occurs.

### 19. Output File Formats (RECOMMENDED)
- ascii
- csv
- Other

- **ascii** — `neuvac.gitmNEUVAC()` writes the GITM EUV input file
  `irradiances/neuvac_euv_<start>_to_<end>.txt`; `toolbox.readFISM2()` writes
  `fism2irr_daily.dat`; `fism2_process.py` writes `fism<YYYYMM>_nWaves_<nnn>.dat` (or its
  `_gitm.dat` variant); `heuvac.writeInputFile()` writes the F10.7 input file consumed by the
  Fortran executable.
- **csv** — `neuvac.aetherFile()` writes `data/euv_59_aether.csv` with `csv.writer`, rewriting the
  NEUVAC coefficient rows into Aether's expected layout.
- **Other** — `toolbox.savePickle()` and the `pickle.dump` calls in `obtainFism1` write `.pkl`
  files, and `experiments/uncIrradiance.py` writes the derived `corMat.pkl`, `corMatStanBands.pkl`,
  `sigma_*.pkl` statistics that the ensemble machinery later consumes. PNG figures are also
  written (31 `savefig` calls). Neither pickle nor PNG has a vocabulary row.

Considered and rejected: `netCDF3/4` - EUVpy reads netCDF but never writes it; there is no
`Dataset(..., 'w')` anywhere. `CDF`, `FITS`, `HDF5`, `JSON`, `Zarr`, `IDL.sav`, `ISTP-Compliant`
likewise have no writer.

### 20. Operating System (RECOMMENDED)
- Linux

Evidence: `docs/source/index.rst` states "At present, the code has only been tested on Ubuntu"; the
README's install instructions are Ubuntu-specific (`sudo apt-get install gfortran`); the
`.readthedocs.yaml` build environment is `ubuntu-24.04`; and `install_heuvac.sh` and
`srcHeuvac/compile.sh` are POSIX shell scripts invoking `gfortran`.

`Mac` and `Windows` were considered and not selected. The only statement supporting them is the
sentence that immediately follows the one quoted above - "In principle, it should work on Windows
and Mac as well" - which is an untested expectation rather than a claim of support, and Field 20 asks
for the systems the software can successfully be installed on. There is no CI at all in the
repository (no `.github/` directory, no other CI configuration), so no automated evidence exists
either. Two facts point the other way and are recorded so that a future refresh does not mistake
them for new evidence: the published wheel is pure Python (`euvpy-1.0.0-py3-none-any.whl`), and
`srcHeuvac/` still contains Windows batch files and Microsoft Visual C++ project files from the
original HEUVAC distribution (`HEUVAC.bat`, `Delete-temp-files.bat`, `HEUVAC.dsp`, `HEUVAC.dsw`) -
though those are legacy artefacts of Phil Richards' distribution, not EUVpy's own build path.
`Operating System Independent`
was rejected outright: HEUVAC requires a local gfortran compilation step, and the package forces the
`Qt5Agg` Matplotlib backend at import time in several modules, both of which are real
platform-dependent requirements.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Evidence: the distributed artefact is a pure-Python wheel (`euvpy-1.0.0-py3-none-any.whl`) with no
compiled extension modules; nothing in the Python source touches architecture-specific code paths;
and the one compiled component, HEUVAC, is portable fixed-form Fortran built from source on the
user's machine by `gfortran -ffixed-line-length-132`, which is available on every architecture
gfortran targets. No SIMD intrinsics, GPU kernels, or architecture-conditional builds exist.

Considered and rejected: `x86-64` and `Apple Silicon arm64` - naming specific architectures would
imply a restriction the code does not have, and the Ubuntu-only testing recorded in Field 20 is an
operating-system observation rather than an architecture one. `GPU` and `HPC or HEC` - no CUDA,
OpenCL, MPI, or job-scheduler support anywhere.

### 22. Related Phenomena (OPTIONAL)
- Solar Flares
- X-ray emission

The `Phenomena` vocabulary is closed: a phenomenon with no row belongs in Keywords rather than here,
which is why the genuinely related phenomena listed at the end of this field are carried by Fields
16 and 5 instead.

- **Solar Flares** — `tools/EUV/fism2_process.py:download_fism2(start, end, isFlare=True)` retrieves
  the FISM2 flare product from `.../fism_flare_hr.csv` and the module's `-flare` command-line flag
  processes it; `docs/source/methods.rst` decomposes the EUV spectrum into continuum, solar-cycle,
  solar-rotation and flare terms and notes that the soft X-ray bands "are incredibly non-stationary
  and receive contamination from flare emissions"; the CLS F10.7 product EUVpy reads is
  flare-corrected (`readCLS`).
- **X-ray emission** — the modelled spectral range extends into the soft X-ray: the reference
  publication states 59 wavelength bins between 1 and 1,750 Angstroms, the TIMED/SEE band grid in
  `processIrradiances.SEEBands` starts at 5 Angstroms, and `docs/source/methods.rst` discusses
  model behaviour "for wavelength bands near the soft X-ray" explicitly.

Considered and rejected:

- `Solar Corona` — `docs/source/methods.rst` notes that EUV emission originates from altitudes
  "extending from the Photosphere to the Corona", but that is background physics; EUVpy provides no
  coronal diagnostic or coronal science functionality.
- `Coronal Heating` — no functionality; not mentioned anywhere.
- `Geomagnetic Storms` — appears only as an example interval in `docs/source/examples.rst` ("Get
  some F10.7 during the 2015 St. Patrick's Day Geomagnetic Storm"), which the relevance rules treat
  as a tutorial name-drop rather than supported functionality.
- `Coronal Mass Ejections`, `Solar Wind` — no functionality.

Phenomena EUVpy genuinely relates to but which have no row in this closed vocabulary - solar EUV
irradiance variability itself, and the ~11-year solar cycle and 27-day solar rotation modulations
that `methods.rst` decomposes - are represented instead through Fields 16 and 5, as the field's own
guidance directs.

### 23. Development Status (RECOMMENDED)
Active

Evidence for a project that has reached a usable state and is being developed: 63 commits from two
contributors between 2024-08-29 and 2025-08-11; a released, pip-installable package on PyPI
(`1.0.0`); a pytest suite of eight test modules covering all four models, the ensemble generator,
the index tools and the GITM writer; published Sphinx documentation on Read the Docs with four
worked examples; PyHC rates its documentation, testing, Python 3 support and licence all "Good"; and
the README announces further work ("This approach will be replaced with a user-friendly console
script in the next release of this package").

Considered and rejected:

- `Inactive` — the last commit is 2025-08-11, roughly a year before the extraction date recorded in
  the header, and the repository has no open issues and four stars. A year of quiet is consistent
  with a small academic package between releases, and nothing signals that the authors have stopped:
  no archive notice, no
  deprecation, no maintainer-wanted message, and an announced next release. A future refresh that
  finds continued silence and no new release should revisit this.
- `WIP` — the `setup.py` classifier is `Development Status :: 3 - Alpha` and PyHC rates software
  maturity only "Partially met", which argues the package is not yet mature. But repostatus.org
  defines WIP as having no stable, usable public release yet, and EUVpy has a public PyPI release
  with a passing test suite and published documentation, so WIP misstates the situation.
- `Concept`, `Suspended`, `Abandoned`, `Unsupported`, `Moved` — each is contradicted by the release,
  the tests, the documentation, or the repository's continued presence at its original location.

### 24. Documentation (RECOMMENDED)
https://euvpy.readthedocs.io/en/latest/

The slug was not assumed. The Read the Docs project `euvpy` is registered to the user `DanBrandt`,
is linked to `https://github.com/DanBrandt/EUVpy.git`, is public, has default version `latest`, and
reports its own canonical documentation URL as `https://euvpy.readthedocs.io/en/latest/`. That URL
resolves and serves the built EUVpy documentation (page title "EUVpy documentation - EUVpy 1
documentation", with the NEUVAC and GITM content present), and `https://euvpy.readthedocs.io/`
redirects to it. The PyHC registry independently records the same URL as EUVpy's docs.

Alternatives considered: `https://euvpy.readthedocs.io/` (resolves, but only by redirect, so the
direct form is preferred) and `https://euvpy.readthedocs.io/en/stable/` (returns 404 - no `stable`
version is activated on the project, so this form must not be used). No GitHub Pages site exists
(`https://danbrandt.github.io/EUVpy/` returns 404), the repository sets no homepage, and PyPI has no
`project_urls` or `docs_url`. The documentation source is `docs/source/` (a Sphinx project with
`index.rst`, `usage.rst` including installation instructions, `methods.rst`, `examples.rst`,
`documentation.rst` and per-module API pages), built by `.readthedocs.yaml` on `ubuntu-24.04` with
Python 3.11.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

The name is spelled out in full as Field 25 requires, rather than the acronym `NASA`, and carries
the agency's own ROR, `https://ror.org/027ka1x80`.

Source: the acknowledgments of the reference publication (Brandt & Ridley 2024, *Space Weather*
22(12), e2024SW004043), read directly and quoted verbatim: "Development of NEUVAC and the EUVpy
package of which it is a part was partially supported by NASA Grant #80NSSC20K1581." The
acknowledgment names EUVpy explicitly, which is why this is recorded as the software's funder rather
than only the paper's, and it is the sole authority for the grant number recorded in Field 26.

Nothing in the repository itself states funding: there is no funding section in the README or the
documentation, no `.github/FUNDING.yml`, and neither Crossref nor OpenAlex records a funder for the
publication.

Considered and rejected: the National Science Foundation. The `80NSSC` prefix identifies a NASA
award, and the acknowledgment names only NASA. Independent records attribute this same grant number
to work in Aaron Ridley's group under the jointly NSF- and NASA-supported Space Weather with
Quantified Uncertainties program, which is consistent with NEUVAC's uncertainty-quantification
emphasis, but naming NSF as a funder of this software would go beyond what the acknowledgment says.

Where to read that acknowledgment, recorded because the obvious route fails: the
publisher's version-of-record page, `https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2024SW004043`,
refuses automated retrieval with HTTP 403, and so does its `/doi/pdf/` form. The article is openly
deposited in Michigan Tech's institutional repository at
`https://digitalcommons.mtu.edu/michigantech-p2/1271`, which serves the complete typeset article as
a PDF behind a Digital Commons cover sheet and is retrievable without a subscription; that copy is
the source of the quotation above. One caveat for whoever re-reads it: the Acknowledgments are set
in a narrow column running alongside the References, so a naive linear text extraction interleaves
the two and the acknowledgment sentence has to be reassembled from the left-hand column.

### 26. Award Title (OPTIONAL)
- **Award Title:** National Aeronautics and Space Administration grant
- **Award Number:** 80NSSC20K1581

The acknowledgment cited in Field 25 gives only a grant number, with no award title. Rather than
inventing one, the title is the generic descriptive form
`National Aeronautics and Space Administration grant`, with the grant number `80NSSC20K1581` as the
award's identifier. Searching for an official project title for this award returned nothing citable,
which is the reason the generic form is used; if a future refresh finds the funded proposal's title,
replacing the title would be an improvement - subject to Field 26's 128-character limit on the award
title, which any replacement has to respect.

Field 26 records no funder link of its own, so the NASA funding relationship is carried by Field 25.

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/94JA00518
- https://doi.org/10.1016/j.asr.2005.06.031
- https://doi.org/10.1029/2005JA011160
- https://doi.org/10.1029/GL008i011p01147

These are the papers describing the three models
EUVpy implements besides NEUVAC, and the README's "Code of Conduct" section makes citing them a
condition of use - "depending on the module used, proper citations should be given to the original
authors responsible for developing each model or dataset" - which is precisely the
developer-prioritised relationship Field 27 is for. All four DOIs were verified through Crossref.

- **10.1029/94JA00518** — Richards, P. G., Fennelly, J. A., & Torr, D. G. (1994). "EUVAC: A solar
  EUV Flux Model for aeronomic calculations." *JGR Space Physics*, 99(A5), 8981-8992. The EUVAC
  model, implemented in `empiricalModels/models/EUVAC/euvac.py`; its 37 bins are one of EUVpy's
  binning schemes.
- **10.1016/j.asr.2005.06.031** — Richards, P. G., Woods, T. N., & Peterson, W. K. (2006). "HEUVAC:
  A new high resolution solar EUV proxy model." *Advances in Space Research*, 37(2), 315-322. The
  HEUVAC model, whose Fortran source is vendored in `srcHeuvac/` and wrapped by `heuvac.py`. The
  repository also ships the paper itself as
  `srcHeuvac/Richards-Woods-Peterson-JASTP-2006-HEUVAC.pdf`. Note for future refreshes: the
  README's HEUVAC link is a ScienceDirect PII URL, not a DOI, so this DOI had to be resolved from
  the title and author list.
- **10.1029/2005JA011160** — Solomon, S. C., & Qian, L. (2005). "Solar extreme-ultraviolet
  irradiance for general circulation models." *JGR Space Physics*, 110(A10), 2005JA011160. The
  source of the 22 overlapping standard bands ("STAN BANDS") EUVpy can bin any model into, and the
  reference the README gives for the SOLOMON module. `docs/source/index.rst` cites the same paper as
  "Solomon and Qian, 2006"; the link resolves to this 2005 article, so the year in that sentence is
  a slip rather than a second publication.
- **10.1029/GL008i011p01147** — Hinteregger, H. E., Fukui, K., & Gilson, B. R. (1981).
  "Observational, reference and model data on solar EUV, from measurements on AE-E." *Geophysical
  Research Letters*, 8(11), 1147-1150. The HFG model that gives the `model='HFG'` option of
  `solomon.solomon()` its name; `docs/source/methods.rst` cites it directly for HFG.

Considered and not included, so a future refresh need not re-derive them:

- https://doi.org/10.1029/2020SW002588 (Chamberlin et al. 2020, FISM2) — the README lists it among
  the required
  citations, but it describes a dataset EUVpy ingests rather than a model it implements, so it is
  recorded once, in Field 28, instead of twice.
- https://doi.org/10.1186/s40623-021-01402-7 (Nishimoto et al. 2021) and the Lilensten et al. 2008
  *Annales
  Geophysicae* article cited in `methods.rst` - both offered as background reading ("for more
  reading on the Solar EUV spectrum"), and one only as the source of a plot style. Neither is a
  developer-prioritised citation nor a description of an implemented model.
- https://doi.org/10.1029/2020JA028932 (Jin et al. 2021) — cited twice in
  `src/EUVpy/experiments/analyzeIrradiance.py`, at both mean-absolute-percentage-error tables, as
  the authority for the low/moderate/high solar-activity definitions behind the F10.7 thresholds of
  80 and 120 used there. Crossref identifies it as Jin, Zou, Yan, Yang et al., "A Statistical Study
  of F-Region 3.2-m-Scale Field-Aligned Irregularities Occurrence and Vertical Plasma Drift Over
  Hainan: Solar Activity, Season, and Magnetic Activity Dependences", *JGR Space Physics* (2021) -
  an ionospheric-irregularities study with no bearing on EUV modelling, cited purely for a
  definitional threshold in an internal analysis script. Excluded for the same reason as the two
  entries above: background support for an implementation choice is not a developer-prioritised
  citation nor a description of a model EUVpy implements.

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.1029/2020SW002588
- https://doi.org/10.1029/2004JA010765
- https://doi.org/10.1007/s11207-009-9487-6

These are the three observational irradiance
datasets EUVpy reads, each identified by the publication describing it - the fallback Field 28
prescribes when no dataset-level DOI exists. All three DOIs were verified through Crossref.

- **10.1029/2020SW002588** — Chamberlin, P. C., et al. (2020). "The Flare Irradiance Spectral
  Model-Version 2 (FISM2)." *Space Weather*, 18(12), e2020SW002588. FISM2 is the dataset NEUVAC is
  fitted to and the package's principal reference dataset: `getIrr(source='FISM2'|'FISM2S')`
  downloads the daily and standard-band products, `obtainFism2()` reads them, `download_fism2()`
  fetches daily or flare series from LISIRD, and `rebin_fism()` / `isolate_fism()` rebin them. The
  README requires citing this paper when the FISM module is used.
- **10.1029/2004JA010765** — Woods, T. N., et al. (2005). "Solar EUV Experiment (SEE): Mission
  overview and first results." *JGR Space Physics*, 110(A1), 2004JA010765. TIMED/SEE Level 3 daily
  merged spectra: `getIrr(source='SEE')` downloads `latest_see_L3_merged.ncdf` and `obtainSEE()`
  reads its `DATE`, `SP_WAVE`, `SP_FLUX`, `SP_ERR_TOT` and `SP_ERR_MEAS` variables; the SEE 1 nm
  band grid is hard-coded as `processIrradiances.SEEBands` and used as a rebinning target.
- **10.1007/s11207-009-9487-6** — Woods, T. N., et al. (2012). "Extreme Ultraviolet Variability
  Experiment (EVE) on the Solar Dynamics Observatory (SDO)." *Solar Physics*, 275(1-2), 115-143.
  SDO/EVE merged Level 3 spectra, read by `obtainSDO()` from the `MERGEDDATA.YYYYDOY`,
  `SPECTRUMMETA.WAVELENGTH`, `MERGEDDATA.SP_IRRADIANCE`, `MERGEDDATA.SP_STDEV` and
  `MERGEDDATA.SP_PRECISION` variables.

Negative research, recorded so it is not repeated: no dataset-level DOI could be found for FISM2,
TIMED/SEE Level 3, or SDO/EVE Level 3. DataCite has no canonical dataset record for any of them, and
the LISIRD dataset pages and `hpde.io` both return generic single-page-application shells for every
path - including deliberately invalid ones - so no SPASE `hpde.io` dataset identifier could be
verified rather than guessed. Guessed `hpde.io` paths were therefore not used.

Considered and not included:

- **NRLSSI2** — `obtainNRLSSIS2()` exists and reads an NRLSSI2 netCDF file, but nothing in the
  package downloads it, no test or example exercises it, and it is not mentioned in the README or
  documentation, so the reader on its own is too thin a basis for a dataset relationship. Its
  describing publication, Coddington et al. (2016), https://doi.org/10.1175/BAMS-D-14-00265.1, is
  recorded so that a future release which wires the reader into a documented path does not have to
  re-derive it.
- **FISM1** — `obtainFism1()` reads FISM1 `.dat` files, but only files the user already has; the
  bundled samples under `tools/EUV/` are demonstration data.
- **F10.7 index series** (Penticton, OMNI2, CLS) — these are indices rather than datasets in Field
  28's sense, and the observatory and archive relationships they carry are recorded in Fields 32 and
  17 respectively.

### 29. Related Software (OPTIONAL)
- https://github.com/DanBrandt/HEUVAC

**HEUVAC** is a distinguishing, domain-specific component rather than a generic dependency. The
repository declares it as a submodule in `.gitmodules`
(`src/EUVpy/empiricalModels/models/HEUVAC/HEUVAC` -> `https://github.com/DanBrandt/HEUVAC.git`), the
README and `docs/source/usage.rst` both instruct users to run
`git submodule update --init --recursive --remote` during installation, and EUVpy exposes the model
through `empiricalModels/models/HEUVAC/heuvac.py`, which writes an input file, invokes the compiled
`HEUVAC.exe`, and parses its Torr-bin and user-bin flux output. The repository exists and is
maintained by the same author, described as "Repository for Phil Richard's HEUVAC code; a general
resource for the benefit of the solar-terrestrial physics community" (MIT). Recorded as a repository
URL because it has no DOI. See the scope note: the submodule path is not actually populated in the
pinned tree and the Fortran is vendored in `srcHeuvac/` instead, but the declared relationship and
the documented install step make this a genuine related-software link, and it is the one entry that
would need revisiting if the author ever removes the submodule declaration.

Considered and rejected:

- **The predecessor repository `solarEUV`.** Commit eccf50f (2024-08-29) reads "Major commit: result
  of refactoring the old 'solarEUV' repo into 'EUVpy'", which would make `solarEUV` a predecessor
  worth recording. No repository of that name exists under the author's GitHub account (it returns
  404), so there is nothing to link. Recorded so a future agent does not re-search for it; if it is
  ever published, it belongs here.
- **TIE-GCM** and **WACCM-X.** `docs/source/index.rst` names them, with GITM, as the kind of
  atmospheric model EUVpy's output is meant for. But no adapter, writer, format or test targets
  either one - unlike GITM and Aether, which have both - so the mention is aspirational. They are
  also not similar-purpose tools: they are downstream general circulation models, not EUV irradiance
  packages.
- **GLOW.** `tools/LQIAN/put_spectra.pro` writes a spectrum file with the header comment "solar
  spectra, when read into glow, do flux/10^9", implying the vendored IDL utilities were written to
  feed the GLOW airglow model. That is a property of third-party IDL code bundled for reference, not
  a capability EUVpy exposes: no Python entry point, no documentation, and no test touches it.
- **The generic scientific-Python stack.** numpy, scipy, pandas, matplotlib, seaborn, tqdm,
  scikit-learn, pygam, csaps, netCDF4, h5py, PyQt5, JupyterLab, pytest, Sphinx and its theme are all
  present in `requirements.txt` or `setup.py` `install_requires`. Every one is either generic
  infrastructure that would be equally at home in a web application or a finance model, or a
  dependency used internally with no exchange of a shared data model. Being a dependency is not a
  distinguishing relationship, and listing them would say nothing that is not equally true of most
  of HSSI.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/aaronjridley/GITM
- https://github.com/AetherModel/Aether

Both are peer heliophysics models for which EUVpy
writes files in the other tool's own documented format - not dependencies. The two are not equally
well evidenced, and the difference is spelled out immediately after the two entries.

- **GITM (Global Ionosphere/Thermosphere Model)** — `NEUVAC/neuvac.py:gitmNEUVAC()` writes a GITM
  EUV input file ("Write NEUVAC irradiances to a file for ingestion directly into the Global
  Ionosphere-Thermosphere Model"), emitting GITM's `#START` header and its expected 59-column
  time-and-irradiance layout. `tools/toolbox.py:readFISM2()` converts a FISM2 netCDF file into "the
  same format as the .dat files here: https://github.com/aaronjridley/GITM/tree/master/srcData/FISM",
  citing GITM's own repository. `tools/EUV/fism2_process.py` has a `-gitm` flag that writes
  GITM-style output. `tests/GITM/test_gitm.py` calls `gitmNEUVAC()` for calendar year 2022 and
  asserts the generated file's first data line against a hardcoded 59-value literal, and
  `docs/source/examples.rst` has a dedicated "GITM" section. EUVpy's 59-bin scheme is
  GITM's wavelength scheme. Recorded as the repository URL; GITM has no DOI.
- **Aether** — `NEUVAC/neuvac.py:aetherFile()` rewrites the NEUVAC coefficient table into Aether's
  `euv_59` CSV form, emitting Aether's own row labels (`NEUV_S1`, `NEUV_S2`, `NEUV_S3`, `NEUV_l1`,
  `NEUV_P1`, `NEUV_P2`) so that "Aether can use [it] to implement the model", using
  `data/euv_59_reference.csv` as the template and producing `data/euv_59_aether.csv`. The primary
  documentary evidence is the dedicated, runnable "Aether" section of `docs/source/examples.rst`,
  which gives `out = neuvac.aetherFile()` as the single line needed and explains the exchange from
  Aether's side - "Aether actually has machinery for computing irradiances directly, but it requires
  a file with the coefficients for NEUVAC in order to do so" - and names where the produced file
  lands. `docs/source/index.rst` links Aether's documentation and credits Aaron Ridley, an author of
  this software, with the model. Recorded as the repository URL; Aether has no DOI.

Evidence asymmetry between the two, worth knowing before either entry is re-examined: the GITM
exchange is covered by a real test and the Aether exchange is not. `tests/GITM/test_gitm.py`
generates a GITM file and asserts its first data line against a hardcoded literal, so it verifies
the written format. `tests/AETHER/test_aether.py` is an empty stub - its only function body is a
bare `return`, it never calls `aetherFile()`, and it asserts nothing - so it establishes nothing
about the Aether exchange and must not be cited as evidence for it. Aether is listed on the strength
of the writer function's Aether-specific output format and the documented worked example, which are
sufficient on their own. If a future refresh finds the stub filled in, that is additional
confirmation rather than a change to this field.

Considered and rejected: everything in Field 29's rejection list, for the same reasons, plus
netCDF4 and h5py specifically. netCDF4 is a Tier-B package that would qualify only with a documented
exchange; EUVpy uses `netCDF4.Dataset` internally to read files and never exposes a netCDF object
as an interchange type, and h5py is not used at all. "Part of the scientific Python ecosystem" and
"a PyHC package, so it interoperates with PyHC packages" are not sufficient grounds and were not
relied on.

### 31. Related Instruments (OPTIONAL)

**Instrument 1**
- **Instrument Name:** Solar EUV Experiment
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/TIMED/SEE

**Instrument 2**
- **Instrument Name:** EVE
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SDO/EVE

Both names are copied verbatim from the matched entries of HSSI's SPASE-backed
`InstrumentObservatory` vocabulary, and both identifiers are the `https://spase-metadata.org/` URLs
those entries carry. The exact spelling matters: each name is recorded as the vocabulary spells it,
and a tidied-up variant of either would not resolve to the intended instrument.

**Why these two are related.** EUVpy has instrument-specific readers for both, which is
designed-to-support rather than incidental. `tools/processIrradiances.py:obtainSEE()` parses
TIMED/SEE Level 3 netCDF by that product's own variable names (`DATE`, `SP_WAVE`, `SP_FLUX`,
`SP_ERR_TOT`, `SP_ERR_MEAS`), `getIrr(source='SEE')` downloads
`latest_see_L3_merged.ncdf` from LASP, and the SEE 1 nm band grid is hard-coded as the module-level
`SEEBands` array and used as a rebinning target. `obtainSDO()` parses SDO/EVE merged spectra by
their own variable names (`MERGEDDATA.YYYYDOY`, `SPECTRUMMETA.WAVELENGTH`,
`MERGEDDATA.SP_IRRADIANCE`, `MERGEDDATA.SP_STDEV`, `MERGEDDATA.SP_PRECISION`). The README states it
directly: "`processIrradiances.py`: Contains functions for reading in data from TIMED/SEE, SDO/EVE,
and FISM." A user searching HSSI for either instrument would reasonably expect this package back.

**The TIMED/SEE duplicate.** Two rows describe the same instrument:
`https://spase-metadata.org/SMWG/Instrument/TIMED/SEE` (name `Solar EUV Experiment`, abbreviation
`SEE`) and `https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/TIMED/SEE` (same name, no
abbreviation). This is one entity with two candidate rows, so the SMWG row is chosen as the
tie-breaker: it is the Space-Physics-Archive-Search-and-Extract working-group record for the
instrument itself, whereas the CNES row is an archive-specific record describing the instrument as
served through CDPP/AMDA. EUVpy retrieves TIMED/SEE data from LASP, not from AMDA, so the
archive-specific record would be doubly wrong here. SDO/EVE has exactly one matching row and needed
no tie-break.

Considered and rejected:

- **`OMNI Instrument`** (`https://spase-metadata.org/SMWG/Instrument/OMNI`) and
  `Sun / Solar Wind / Ground-Based Indices`
  (`https://spase-metadata.org/CNES/Instrument/CDPP-AMDA/OMNI`) — OMNI is a merged multi-source data
  product, not an instrument: no physical instrument named OMNI ever flew, and EUVpy reads no
  instrument-level OMNI product. The rejection is specific to Field 31. OMNI's genuine relationship
  to EUVpy is recorded at the levels where it belongs - `OMNIWeb` in Field 17 as the archive
  interface, and the `OMNI` observatory identifier in Field 32 as the data resource whose values
  EUVpy consumes - and Field 32 explains why both are correct together.
- **SORCE/SOLSTICE** (`https://spase-metadata.org/SMWG/Instrument/SORCE/SOLSTICE`) —
  `docs/source/methods.rst` mentions that "Space-based instruments like TIMED/SEE and SORCE/SOLSTICE
  have measured the solar spectrum", but that is background prose. No code reads any SORCE product,
  so this is a name-drop, not support.
- **TIMED/GUVI, TIMED/SABER, TIMED/TIDI, SDO/AIA, SDO/HMI** — all resolve in the vocabulary and all
  belong to platforms EUVpy does support, but EUVpy touches none of their data. Listing sibling
  instruments from a supported platform would be exactly the over-expansion the resolution rules
  warn against.
- **FISM2 and NRLSSI2** — both are models or composite data products, not instruments, and have no
  instrument row. FISM2's dataset relationship is recorded in Field 28.

### 32. Related Observatories (OPTIONAL)

**Observatory 1**
- **Observatory Name:** Thermosphere-Ionosphere-Mesosphere Energetics and Dynamics
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/TIMED

**Observatory 2**
- **Observatory Name:** Solar Dynamics Observatory
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SDO

**Observatory 3**
- **Observatory Name:** OMNI
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/OMNI

All three names are copied verbatim from the matched vocabulary rows, and all three identifiers are
the `https://spase-metadata.org/` URLs those rows carry.

- **TIMED** — the platform of the Solar EUV Experiment recorded in Field 31; EUVpy downloads and
  parses its Level 3 solar spectral irradiance product. The canonical SMWG name is the expanded
  mission name, copied as stored rather than shortened to "TIMED". A duplicate row exists at
  `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/TIMED` (name
  `Thermosphere Ionosphere Mesosphere Energetics and Dynamics`, without hyphens); the SMWG row is
  chosen as the tie-breaker for the same reason as in Field 31.
- **SDO** — the platform of EVE, whose merged Level 3 spectra `obtainSDO()` reads. Exactly one row
  matched. The README's opening image caption also credits "EUV imagery of the solar disk, taken by
  NASA SDO", but the reader is the substantive evidence.
- **OMNI** — `tools/processIndices.py:getF107()` retrieves OMNI2 F10.7, posting an hourly-resolution
  retrieval request (`spacecraft=omni2`, `vars=50`) to the OMNIWeb CGI, and
  `tools/processIndices.py:readOMNI()` is a dedicated parser for the resulting OMNIWeb listing
  together with its `.fmt` header file. That is the same reads-their-data basis on which TIMED and
  SDO are listed above. Exactly one SMWG row matched; a duplicate exists at
  `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/OMNI`, and the SMWG row is chosen as the
  tie-breaker for the same reason as in Field 31 - EUVpy retrieves OMNI data from OMNIWeb at Goddard,
  not through CDPP/AMDA.

  `OMNIWeb` is recorded in Field 17 as well, and that is deliberate: Fields 17 and 32 are not
  mutually exclusive here. Field 17 records the archive interface the software talks to; Field 32
  records the data resource whose measurements it consumes. Software that reaches OMNI through
  OMNIWeb legitimately carries both.

  This corrects an earlier omission, and the reasoning behind that omission is recorded so it is not
  revived. OMNI was previously left out of Field 32 and routed to Field 17 alone, on the grounds that
  OMNI is a merged multi-mission data product rather than a mission or observatory, and that such
  products therefore belong at the archive level - by analogy with CDAWeb. The analogy does not hold.
  CDAWeb is a multi-mission archive interface for which no SPASE Observatory identifier exists, so it
  could not be named at observatory level whatever one concluded about merged products. OMNI, by
  contrast, has a canonical SPASE Observatory identifier of its own,
  `https://spase-metadata.org/SMWG/Observatory/OMNI`, and EUVpy reads the values published under it
  directly. That direct reads-their-data relationship - the same basis on which TIMED and SDO are
  listed above - is why OMNI is recorded here.

Considered and rejected:

- **Dominion Radio Astrophysical Observatory**
  (`https://spase-metadata.org/SMWG/Observatory/DRAO`) — the strongest candidate that was not
  selected, and its supporting evidence is recorded here in full so a future refresh need not
  rediscover it. DRAO makes the Penticton 10.7 cm solar radio flux measurement that is the sole
  driving input of every model in the package, and EUVpy does ship a dedicated parser for the
  Penticton solar-flux files: `tools/processIndices.py:readF107()` branches per file layout, and its
  docstring names the source service explicitly ("the FTP server provided by the Government of
  Canada: https://www.spaceweather.gc.ca/forecast-prevision/solar-solaire/solarflux/sx-5-en.php")
  along with the observed-versus-1 AU-adjusted distinction specific to that product. The README
  describes the `solarIndices` folder as containing "F10.7 solar index data, from both OMNIWeb and
  Penticton", and `F107filter`'s own plot title reads "Penticton F10.7 and Filtered Penticton F10.7".

  It is nonetheless excluded, because the relationship is one hop removed from the observatory. The
  default F10.7 path in every documented example and in four of the eight tests is `getCLSF107()`,
  which retrieves a Collecte Localisation Satellites *redistribution* of the index - flare-corrected
  and Sun-Earth-distance-adjusted by CLS - rather than anything DRAO serves. EUVpy therefore consumes
  a third-party redistribution of a DRAO measurement, not DRAO's own data products, and "designed to
  support DRAO" overstates what the package does. The entry was previously recorded with its
  indirectness noted only as a reservation; the reservation is the determination.
  Should a future release read Penticton files directly from the Government of Canada service as its
  default path rather than through the CLS redistribution, the entry would become defensible and
  should be reconsidered on that basis.

- **SORCE** (`https://spase-metadata.org/SMWG/Observatory/SORCE`) — background mention only, as
  discussed in Field 31.
- **LISIRD** — the LASP archive EUVpy downloads FISM2 from is a data service, not an observatory,
  and has no vocabulary row. It is recorded in Field 17 under `HTTP/HTTPS Directories`.
- **Collecte Localisation Satellites** — the FTP service EUVpy retrieves flare-corrected radio flux
  from. It is a data provider, not an observatory; no row exists and none should be invented. Its
  retrieval path is recorded in Field 17 under `FTP/FTPS Directories`, and the fact that the
  underlying measurement originates at DRAO is discussed in the DRAO entry above, which is why
  neither is recorded as a value here.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/DanBrandt/EUVpy/main/EUVpy_logo.png

This corrects the stored value
`https://raw.githubusercontent.com/DanBrandt/EUVpy/main/./EUVpy_logo.png`, which contained a `/./`
path artefact. The artefact came from concatenating the repository's raw base URL with the README's
relative reference `<img src="./EUVpy_logo.png">` without normalising the leading `./`. Both forms
happen to resolve to the same 12,250,542-byte image because GitHub normalises the redundant segment,
so this is a cosmetic correction of a malformed URL rather than a broken link - but a stored URL
should not carry a path artefact. The target is `EUVpy_logo.png` at the repository root on `main`,
which is the canonical source file and is also what `docs/source/images/EUVpy_logo.png` duplicates
for the documentation build.

Alternative considered and not selected: `https://euvpy.readthedocs.io/en/latest/_images/EUVpy_logo.png`,
which the PyHC registry records as EUVpy's logo. It serves the identical image and, unlike
`raw.githubusercontent.com`, serves it with a `image/png` content type rather than
`application/octet-stream`. The repository-root URL was preferred because it is the minimal
correction to the stored value and points at the version-controlled source of the image rather than
at a Sphinx build artefact whose path depends on the documentation continuing to embed that figure.
If HSSI ever has trouble rendering an `application/octet-stream` logo, the PyHC URL is the
ready-made substitute.

---

## Sources used

- Repository at revision `52f72d874a616f4e75b2d2f37424b0c2e6de9eac`: `README.md`, `LICENSE`,
  `setup.py`, `requirements.txt`, `.gitmodules`, `.gitignore`, `.readthedocs.yaml`,
  `install_heuvac.sh`, `builddocs.bash`, `docs/source/*.rst`, `docs/source/conf.py`,
  `src/EUVpy/**`, `tests/**`, `examples/euvpy_examples.ipynb`, and the git history (63 commits,
  2024-08-29 to 2025-08-11; single tag `1.0-prealpha`).
- PyHC community package registry (`_data/projects.yml`) — EUVpy is a listed PyHC community package;
  its curated `docs`, `logo`, `description` and keywords, and its quality ratings, informed
  Fields 9, 16, 23, 24 and 33.
- PyPI project `EUVpy` — release `1.0.0` (wheel and sdist, 2025-08-11), summary, classifiers.
- Zenodo record 13685579 and concept record 13685578, and their DataCite registrations.
- GitHub repository, releases, tags and contributors metadata for `DanBrandt/EUVpy`, and repository
  metadata for `aaronjridley/GITM`, `AetherModel/Aether`, `DanBrandt/HEUVAC`.
- Read the Docs project `euvpy` and the published documentation at
  `https://euvpy.readthedocs.io/en/latest/`.
- Crossref records for DOIs 10.1029/2024SW004043, 10.1029/94JA00518, 10.1016/j.asr.2005.06.031,
  10.1029/2005JA011160, 10.1029/GL008i011p01147, 10.1029/2020SW002588, 10.1029/2004JA010765,
  10.1007/s11207-009-9487-6, 10.1029/2020JA028932.
- Full text of the reference publication, from the copy deposited in Michigan Tech's institutional
  repository (`https://digitalcommons.mtu.edu/michigantech-p2/1271`) - the source of the funding
  acknowledgment behind Fields 25 and 26, and of the article's own framing quoted in Fields 4 and 5.
  The publisher's version of record is not retrievable without a subscription; see Field 25.
- ORCID public records 0000-0003-3034-5440 (Brandt), 0000-0001-6933-8534 (Ridley),
  0000-0002-4936-218X (Paki), including full employment entries.
- ROR registry (searched for Michigan Tech Research Institute, Michigan Technological University,
  University of Michigan, National Aeronautics and Space Administration).
- HSSI controlled vocabularies, as the authority for every controlled value recorded above:
  `FunctionCategory`, `Region`, `Phenomena`, `ProgrammingLanguage`, `License`, `Keyword`,
  `DataInput`, `FileFormat`, `OperatingSystem`, `CpuArchitecture`, `RepoStatus`, and
  `InstrumentObservatory`.
