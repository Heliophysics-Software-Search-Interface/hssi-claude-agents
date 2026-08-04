# HSSI Metadata Extraction Results

**HSSI Software ID:** aff43790-897a-49b4-a4c6-f3506a6c4858
**Repository:** https://github.com/SNU-sunday/fisspy
**Source Revision:** 8e7770420123e79b899de484db045dbdb919cfd6
**Extraction Date:** 2026-08-03
**Validation Date:** 2026-08-04
**Validation Status:** PASS

---

## Scope notes — read these before using the evidence below

**The repository has no machine-readable metadata file.** There is no `CITATION.cff`, no
`codemeta.json`, no `.zenodo.json`, no `AUTHORS`, no `CONTRIBUTORS`, no `CHANGELOG`/`NEWS`/`HISTORY`,
and no `.github/workflows` (no CI configuration) anywhere in the tree at any revision. Every value
below therefore rests on `setup.py`, `README.md`, `LICENSE.txt`, the Python source itself, the
project's own web documentation at `http://fiss.snu.ac.kr`, the PyPI and conda-forge release
channels, the PyHC registry, ORCID, Crossref and the GitHub API. Absence of a citation file is a
substantive finding, not a gap in the search: it is the reason Fields 2 and 14 are empty.

**Directory-name caveat for module paths.** The package ships two reading modules. `fisspy/read/` is
current; `fisspy/io/` is deprecated and emits a `DeprecationWarning`-style warning on import
(`fisspy/io/__init__.py`: "As of v0.9.0, the `fisspy.io` module is deprecated and will be removed in
a v1.0.0 version. Use `fisspy.read` …"). The deprecated module is still present at 1.3.0 despite the
warning promising removal at 1.0.0. Cite `fisspy/read/` for current capability; `fisspy/io/read.py`
duplicates older functionality and should not be read as an additional capability.

**`astropy_helper/` is an unpopulated submodule.** `.gitmodules` declares
`astropy_helper` → `https://github.com/astropy/astropy-helpers.git`, but the directory is empty in
a fresh clone and nothing in the package imports from it. It is a vestige of an abandoned
astropy-helpers packaging attempt and carries no metadata weight. `setup.py` uses plain
`setuptools.setup` with `find_packages`.

**Repository hygiene, recorded so it is not mistaken for capability.** 132 of the 247 tracked files
are build/editor artifacts: `.DS_Store` (5), `__pycache__/*.pyc` for Python 3.6/3.7/3.9/3.10/3.12,
and editor backups `fisspy/io/read.py~` and `fisspy/io/.read.py.un~`. Several commit subjects in the
1.2.x–1.3.0 range are `backup` and `abc`. None of this is metadata; it is noted only so a later
reader does not mine `.pyc` files or `read.py~` for API evidence, and because it bears on the
Development Status reasoning (Field 23) and on why the version description (Field 12) had to be
derived from a diff.

**The project's web host is HTTP-only.** `http://fiss.snu.ac.kr` serves the documentation and the
data archive correctly, but `https://fiss.snu.ac.kr` resets the connection. Any future agent
"upgrading" the Documentation URL (Field 24) to `https://` will break it. The `http://` scheme in
Fields 24, 17 and 28 is deliberate.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)

- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The HSSI record does not expose a submitter, and this record is curated by the HSSI team rather than
submitted by the upstream maintainer. That maintainer's contact address is
`jhkang@astro.snu.ac.kr` (`setup.py` `author_email`, PyPI `author_email`) with
`jhkang0301@gmail.com` as a secondary address used in `fisspy/read/__init__.py`; neither is a
submitter and neither should be entered here.

### 2. Persistent Identifier (RECOMMENDED)

**Not found — fisspy has no DOI of any kind.**

Negative research, recorded so this is not searched again:

- The DataCite DOI registry indexes no record matching `fisspy`; a registry-wide query for that
  name comes back empty.
- Zenodo holds no record matching `fisspy`; a repository-wide query for that name comes back empty.
- `README.md` carries exactly three badges — PyPI version, conda-forge version, conda-forge
  downloads — and no DOI badge or Zenodo badge.
- There is no `.zenodo.json` and no GitHub–Zenodo integration; the repository has **no GitHub
  releases and no git tags at all**, so the Zenodo release webhook could never have fired.
- `docs/acknowledge.html` is the project's own acknowledgement page and states: "We would appreciate
  acknowledging FISSPy in your publications, if you use FISSPy in your scientific work. There is no
  rule how to acknowledge and it's fully up to you". A project that declines to prescribe a citation
  has not registered a DOI.
- SoMEF (v0.9.11) run against the repository extracted no `identifier` and no citation block.

Consequence: Field 12's Version PID is necessarily empty too, and Field 14 cannot be satisfied from a
software DOI.

### 3. Code Repository (MANDATORY)

`https://github.com/SNU-sunday/fisspy`

Carried over unchanged from the existing HSSI record and independently confirmed: it is the clone
origin of the working tree, the `dev_url` in the conda-forge feedstock recipe, and the repository the
project's documentation links to. The GitHub API reports it as active and unarchived, default branch
`master`, last push 2025-07-18, 4 stars, 2 forks, 0 open issues.

Rejected alternative: `http://fiss.snu.ac.kr`, which `setup.py` gives as `url=` and PyPI reports as
`home_page`. That is the project home page and documentation host, not the source repository; it
belongs in Field 24. `https://pypi.org/project/fisspy/` and
`https://anaconda.org/conda-forge/fisspy` are distribution channels, not repositories.

### 4. Software Functionality (MANDATORY)

Twenty-seven values, each written verbatim in the canonical `Parent: Child` form the
`FunctionCategory` vocabulary uses. Every subcategory has its parent category listed alongside it.

**Top-level categories**

- `Data Processing and Analysis`
- `Data Visualization`
- `Mission-related`
- `Models and Simulations`

**Subcategories**

- `Data Processing and Analysis: 2D Slices`
- `Data Processing and Analysis: Analysis`
- `Data Processing and Analysis: Calibration`
- `Data Processing and Analysis: Data Access and Retrieval`
- `Data Processing and Analysis: Data Reduction`
- `Data Processing and Analysis: Image Processing`
- `Data Processing and Analysis: Processing`
- `Data Processing and Analysis: Spectrogram`
- `Data Processing and Analysis: Time Series Analysis`
- `Data Processing and Analysis: Wavelet Analysis`
- `Data Visualization: 2D Graphics`
- `Data Visualization: 2D Slices`
- `Data Visualization: Line Plots`
- `Data Visualization: Mission-Specific`
- `Data Visualization: Movies`
- `Data Visualization: Spectrogram`
- `Mission-related: Archive`
- `Mission-related: Calibration`
- `Mission-related: Instrument Response`
- `Mission-related: Inventory`
- `Mission-related: Science Data Processing`
- `Models and Simulations: Forward-Fitting`
- `Models and Simulations: Physics-Based`

**Why the bare parent term is not sufficient on its own.** For most of its life this HSSI record
described fisspy with the single bare value `Mission-related` and no subcategories at all.
`Mission-related` is correct, for the reasons given below, but a 17,153-line package whose public API
spans reading, calibrating, aligning, inverting, analysing and animating FISS spectrograph data
cannot be described by one top-level term, and that one-term classification is what the list above
supersedes. The evidence for each value follows.

**Per-value evidence**

*`Data Processing and Analysis` and `Data Processing and Analysis: Processing`* — the package's core
is a data pipeline. `fisspy/preprocess/proc_base.py:1153 preprocess()` turns a raw camera frame into
a calibrated product; `fisspy/correction/correction.py:689 corAll()` applies the full correction
chain to a `FISS` object; `fisspy/read/readbase.py:46 readFrame()` and `:93 _readPCA()` reconstruct
spectra, the latter by matrix-multiplying PCA coefficients against a basis-profile file.

*`Data Processing and Analysis: Calibration`* — `fisspy/correction/correction.py` exports 18
correction functions, including `wvCalib` (line 79) with three wavelength-calibration methods
(`simple` from header, `center` from the main line, `photo` from a photospheric line),
`get_InstShift` (line 36, "offset value of the instrumental shift caused by the seeing and vibration
of the spectrograph"), `corSLA`/`corStrayLight` (lines 314/360, stray-light and spatial-resolution
degradation correction), `corAsymmetry`, `get_TauH2O`/`corTlines` (line 463, telluric H₂O line
removal), `get_TauS`/`corSline`, `wvRecalib` and `normalizeProfile`.
`fisspy/preprocess/proc_base.py` adds `calFlat` (line 554: flat-field and slit-pattern construction,
gain calibration, atlas subtraction), `get_tilt`/`tilt_correction` (lines 299/474),
`get_curve_par`/`curvature_correction` (lines 413/498) and `wv_calib_atlas` (line 1198).

*`Data Processing and Analysis: Data Access and Retrieval`* — `fisspy/data/download.py` exposes
`search(year, month, day)` (line 11), which scrapes the observation index at
`http://fiss.snu.ac.kr/data_list/` with BeautifulSoup and returns a `pandas.DataFrame`, and
`download(search_res, save_path)` (line 78), which fetches per-target ZIP archives from
`http://fiss.snu.ac.kr/static/data/{year}/{yyyymmdd}/data/{target}.zip`.
`fisspy/data/_sample.py:30 download_sample_data()` retrieves sample FISS files, and
`fisspy/preprocess/proc_base.py:1110 read_atlas()` auto-downloads `solar_atlas.npz` from the project
server when it is absent locally.

*`Data Processing and Analysis: Data Reduction`* — `fisspy/preprocess/proc_base.py:1344
PCA_compression()` and `:1458 PCA_compression_new()` decompose FISS spectral cubes onto principal
components and write the `_c.fts` coefficient file plus the `_p.fts` basis-profile file that
constitute the archived compressed data products, trading volume for a controlled reconstruction
tolerance (`tol=1e-1`). `detrending()` (line 1796) and `data_mask_and_fill()` (line 129) also reduce
and condition data.

*`Data Processing and Analysis: 2D Slices`* — extracting 2-D planes out of 3-D and 4-D cubes is a
primary user-facing operation, not an implementation detail. `fisspy/read/readbase.py:212
getRaster()` integrates the (y, x, λ) cube over a wavelength band to produce a 2-D raster image;
`fisspy/image/interactive_image.py:159` takes `self.data[:, self.xp]`, the (y, λ) spectrogram plane at
fixed scan position; and `fisspy/analysis/tdmap.py:193 makeTDmap.makeTD(sp)` cuts a time–distance
plane along a user-drawn slit through the 3-D (t, y, x) cube.

*`Data Processing and Analysis: Image Processing`* — `fisspy/align/base.py` provides `alignOffset`
(line 16, sub-pixel image registration by FFT cross-correlation, ported from J. Chae's IDL
`ALIGNOFFSET.PRO`), `rotImage` (line 279), `shiftImage`/`shiftImage3D` (lines 340/369) and
`get_interpVal`/`get_interpVal3D` (lines 162/230, linear and cubic spline resampling).
`fisspy/preprocess/proc_base.py:73 getMask()` builds masks, and `fisspy/analysis/ofe.py:16 runDAVE()`
computes an optical-flow field with `scipy.signal.fftconvolve`.

*`Data Processing and Analysis: Analysis`* — `fisspy/analysis/doppler.py:11 lambdameter()` derives
line-of-sight Doppler velocity and line intensity by the λ-meter/bisector method;
`fisspy/analysis/tdmap.py:598 calTDvel()`, `:664 calPeriod()` and `:682 calDistance()` measure
propagation speeds, oscillation periods and wavelengths from time–distance maps;
`fisspy/inversion/_mlsi_base.py:32 Trad()`, `:65 Dwidth()`, `:90 Dw2TnXi()` and `:1084 RadLoss()`
convert inverted parameters into radiation temperature, Doppler width, kinetic temperature,
microturbulent velocity and radiative loss.

*`Data Processing and Analysis: Spectrogram` and `Data Visualization: Spectrogram`* —
`fisspy/analysis/wavelet.py:15 Wavelet` computes the time–period power array with Morlet, Paul and DOG
mother functions plus significance testing and a global wavelet spectrum (the array is the
processing side), and `:590 Wavelet.plot()` renders that array as a shaded time–period image with
significance contours and cone of influence (the visualization side). Separately, the interactive
viewers display the instrument's own wavelength–position spectrograms
(`fisspy/image/interactive_image.py:159`, `fisspy/read/read_factory.py:1160 _changeWavelet()`).

*`Data Processing and Analysis: Time Series Analysis`* — `fisspy/analysis/filter.py:10
FourierFilter()` performs bandpass filtering along the time axis; `fisspy/read/read_factory.py:813
FD.bandpassFilter()` exposes it on a 4-D cube; `fisspy/analysis/forecast.py:10 ARcast()` detects
unevenly sampled points and fills them by blending forward and backward `statsmodels` `AutoReg`
predictions; `fisspy/read/read_factory.py:777 spatialAverage()` and `:784 timeAverage()` remove
spatial and temporal means.

*`Data Processing and Analysis: Wavelet Analysis`* — `fisspy/analysis/wavelet.py` exports `Wavelet`
and `WaveCoherency` (line 724, cross-wavelet coherency and phase between two series). The wavelet
transform is also used inside the calibration pipeline: `fisspy/preprocess/proc_base.py:149
cal_fringeGauss()` and `:197 cal_fringeSimple()` isolate and subtract interference fringes in the
wavelet domain.

*`Data Visualization` and `Data Visualization: 2D Graphics`* — every reader class carries an
`imshow`: `raw.imshow` (`fisspy/read/read_factory.py:99`), `FISS.imshow` (`:458`) and `FISS.vshow`
(`:534`), `FD.imshow` (`:832`), `calibData.imshow` (`:1301`), `AlignCube.imshow` (`:1360`),
`MLSIpar.imshow` (`:1391`). `fisspy/analysis/ofe.py:281 readOFE.imshow()` overlays divergence and
curl maps of the flow field.

*`Data Visualization: Line Plots`* — spectral profile panels plotted as
`axProfile.plot(self.wave, self.data[yp, xp])` (`fisspy/image/interactive_image.py:169`, `:571`,
`:572`; `fisspy/read/read_factory.py:594`), light curves in `FD.imshow`, and the time-series panel of
`Wavelet.plot` (`fisspy/analysis/wavelet.py:643`).

*`Data Visualization: 2D Slices`* — the same raster / spectrogram / time–distance planes described
above are the things the interactive figures display and let the user step through
(`fisspy/image/interactive_image.py:316 _chRaster()`, `:337 _chSpect()`;
`fisspy/analysis/tdmap.py:413 analysisTDmap`).

*`Data Visualization: Movies`* — `fisspy/makevideo.py` is a dedicated module exporting `ffmpeg` (line
24, encodes an image list to `video.mp4` via the external ffmpeg binary and a generated
`img_list.tmp`) and `img2video` (line 112, an interactive frame browser).
`fisspy/image/raster_set.py:274 animation()` and `:292 saveAnimation()` build
`matplotlib.animation.FuncAnimation` sequences and write timestamped `*.mp4` files; `makeOBSmovie`
(line 586) produces the observation movies published in the FISS catalogue. `ffmpeg` is a declared
runtime dependency in both `setup.py` and the conda-forge recipe.

*`Data Visualization: Mission-Specific`* — visualizations built around FISS's own data layout rather
than generic plots: `fisspy/cm.py` defines the instrument's four band colour maps `ha`, `ca`, `na`
and `fe` with reversed variants (functions `hac`, `cac`, `nac`, `fec` at lines 22, 86, 149, 232);
`fisspy/image/interactive_image.py:371 dualBand` co-displays the two FISS cameras after
cross-aligning them (`alignOffset` at line 442); `fisspy/image/raster_set.py:29 makeRasterSet` lays
out the multi-wavelength raster montage used for FISS quick-look products.

*`Mission-related`* — retained from the stored record and independently justified. fisspy is not
merely a package that happens to read FISS files; it is the instrument team's own ground software.
`fisspy/preprocess/proc_gui.py:26 prepGUI` is a 3,484-line PyQt5 application that walks an operator
through the FISS calibration run step by step and writes the calibration and `proc` products;
`fisspy/image/raster_set.py:320 makeCatalogFiles()` writes the JSON records, quick-look images,
movies and ZIP bundles published on the project's own data catalogue. The taxonomy's dividing line —
"a package that *reads* MMS data is Data Processing and Analysis; a package that is *part of the MMS
ground system* is Mission-related" — puts fisspy on the ground-system side. (FISS is a ground-based
instrument rather than a spacecraft payload; `Mission-related` is nevertheless the vocabulary's only
term for instrument-team pipeline and archive software, and HSSI uses it for ground observatories
elsewhere.)

*`Mission-related: Calibration`* — the pipeline produces the instrument's official calibration
products, not just corrected user data: `calFlat.saveFits()`
(`fisspy/preprocess/proc_base.py:897`) writes `FISS_FLAT*_A/B.fts` and `FISS_SLIT*_A/B.fts`;
`readcal()` (line 1121) reads them back by those exact filename patterns; and
`fisspy/read/read_factory.py:1267 calibData` recognises the four official calibration file types by
name (`BiasDark`, `Flat`, `FLAT`, `SLIT`).

*`Mission-related: Science Data Processing`* — `preprocess()` plus `PCA_compression()` generate the
`_proc`, `_c` and `_p` FISS data products that the archive distributes;
`fisspy/read/read_factory.py:219` classifies an input file as `proc` or `comp` from its name and
refuses anything else ("Input file is neither proc nor comp data"), which is a pipeline product
contract rather than a generic reader.

*`Mission-related: Archive`* — `fisspy/image/raster_set.py:320 makeCatalogFiles()` assembles the
publishable archive package: it moves the rendered `*.mp4` into `movie/`, writes the quick-look PNG
into `img/`, and ZIPs every `*.fts` of the compressed observation into `data/`. `zipComp()` (line
507) does the same for a compressed directory.

*`Mission-related: Inventory`* — the same function writes the catalogue record that indexes the
holding: a per-date JSON file carrying `observer`, `obstime`, `target`, `position`, `cadence`,
`obsarea`, `imgA`/`imgB`, `movie`, `data`, `keywords`, `seeing`, `pubbridge` (related publications)
and `coobs` (co-observations). `upateJSON()` (line 530) and `saveJSON()` (line 555) maintain those
records, and `makeOBSmovie.getPub()` (line 798) enriches them by fetching abstracts from ADS. This is
an observation inventory, distinct from the archive packaging above.

*`Mission-related: Instrument Response`* — `fisspy/preprocess/proc_base.py:1274 get_echelle_res()`
solves the grating equation for FISS's own optics (79 grooves/mm, 63.4° blaze, 0.93° or 1.92°
deflection) to return the incident angle, the brightest spectral order and the relative blaze
brightness at a given wavelength; `:1325 spectral_range()` then converts that plus the 1.5 m
collimator focal length and the 16 µm detector pitch into the wavelength range on the chip. These are
called from the wavelength-calibration path (lines 1020, 1028, 1218, 1226), so the instrument's
dispersive response is modelled as part of its pipeline.

*`Models and Simulations` and `Models and Simulations: Forward-Fitting`* — `fisspy/inversion/`
implements Multi-Layer Spectral Inversion: `_mlsi_base.py:316 cal_3layers()` synthesises an Hα or
Ca II 8542 profile from a three-layer atmosphere with Voigt or Gaussian absorption profiles
(`absP_Voigt` line 244, `absP_Gauss` line 280), `:563 cal_residue()` forms the residual against the
observation with penalty and constraint terms, and `:836 Model()` drives
`scipy.optimize.least_squares` (via `lsq_single`, line 1287) over the free parameters, in parallel
across cores with `joblib`. `CloudModel()` (line 1330) does the same for a cloud model. Synthetic
spectrum plus χ²-style parameter optimisation is the definition of forward-fitting.
`fisspy/inversion/_mlsi.py:18 MLSI4file()` applies it to a whole raster and writes the parameter FITS
file; `:127 MLSI4profile` and `:541 IMLSI` are interactive single-profile and raster inversion tools.
`get_TauH2O()`/`get_TauS()` in `fisspy/correction/correction.py` likewise fit optical-depth models to
observed profiles.

*`Models and Simulations: Physics-Based`* — the inverted quantities are physical, derived from
radiative-transfer relations rather than fitted empirically: `_mlsi_base.py` imports
`astropy.constants` and computes radiation temperature from intensity (`Trad`, line 32), Doppler
width from temperature and microturbulence (`Dwidth`, line 65), the inverse mapping to temperature
and turbulent speed from the Hα and Ca II Doppler widths (`Dw2TnXi`, line 90), source functions via
`_Sfromx` (line 313) and `scipy.special.expn` exponential integrals, and radiative loss (`RadLoss`,
line 1084; `_RadLossBase`, line 1116).

**Considered and rejected, with reasons.** These are recorded so they are not re-proposed.

- `Coordinate Transforms` and all six of its children — **rejected.** The only function with
  "coordinate" in its name, `fisspy/align/base.py:116 CoordinateTransform()`, is a plane rotation
  plus translation about a centre (`xt=(x-xc)cosθ+(y-yc)sinθ+xc+dx`); its docstring claims
  "cartesian to polar" but the code does no such thing. The one time-dependent rotation in the
  package, `fisspy/align/alignment.py:86 angle[i] = -t*(2*np.pi)`, is the telescope's diurnal field
  rotation removed for co-alignment, expressed in radians of elapsed day — not a transformation
  between named reference frames. There is no `sunpy.coordinates`, no `astropy.coordinates`, no
  SkyCoord, and no mention anywhere of Carrington, Stonyhurst, heliographic, helioprojective, HGS,
  HCI, HEE or any other heliophysics frame. Image-plane registration is classified under
  `Data Processing and Analysis: Image Processing` instead.
- `Data Processing and Analysis: File Format Conversion` — **rejected.** No function reads one data
  format in order to write another. `makevideo.ffmpeg` turns PNG/JPEG frames into MP4, which is
  captured by `Data Visualization: Movies`; `PCA_compression` writes FITS from FITS (compression, not
  conversion); the npz and JSON writers persist derived analysis products rather than transcoding
  inputs.
- `Models and Simulations: Forecasting` — **rejected** despite `fisspy/analysis/forecast.py` and the
  `ARcast` docstring's word "forecast". The function interpolates and gap-fills an unevenly sampled
  series by blending AR predictions run forwards from before the gap and backwards from after it
  (lines 84–102); it never predicts beyond the observed interval and has nothing to do with space
  weather prediction. Classified as `Data Processing and Analysis: Time Series Analysis`.
- `Data Processing and Analysis: ML/AI` (and the ML/AI children of the other parents) — **rejected.**
  No `sklearn`, `tensorflow`, `torch` or any learned model anywhere. PCA here is a linear compression
  basis computed by SVD, not machine learning.
- `Data Processing and Analysis: Wave Polarization Analysis` — **rejected.** fisspy has no
  polarimetry: `stokes`, `polariz` and `polaris` appear zero times in the source. (The instrument's
  spectropolarimetric upgrade, FISS-SP, is described in a 2025 A&A paper by the same group but is not
  supported by this package at 1.3.0. Revisit if a Stokes path appears.)
- `Data Processing and Analysis: Energy Spectra` — **rejected.** fisspy's spectra are optical
  wavelength spectra; this subcategory denotes particle energy spectra.
- `Data Visualization: 3D Graphics` — **rejected.** No `mplot3d`, `vtk`, `mayavi` or `pyvista`.
- `Data Visualization: Web-Based` — **rejected.** No plotly, bokeh or dash appears anywhere in the
  source. `pjsonIMGtag()` (`fisspy/image/raster_set.py:462`) has a misleading name and emits no HTML
  whatsoever: it derives a quick-look image *filename* from the record's ADS URL and stores it as the
  `img` value of the catalogue JSON record (`js['img'] = iname`), then rewrites the JSON file. The
  string `<img` occurs zero times in that module. The site that renders those records is a separate
  Django application; fisspy itself produces no interactive browser figure.
- `Mission-related: Analysis` — **rejected**, deliberately, to keep a meaningful line. The analysis
  capabilities (`Wavelet`, `FourierFilter`, `ARcast`, `makeTDmap`, `runDAVE`) operate on plain NumPy
  arrays and are usable on any imaging-spectroscopy or image-sequence data; they belong under
  `Data Processing and Analysis: Analysis`. The genuinely instrument-side functions — calibration
  product generation, pipeline products, archive packaging, catalogue records, grating response — are
  the ones tagged `Mission-related: *`.
- `Mission-related: Processing` — **rejected as redundant** with the more specific
  `Mission-related: Science Data Processing`, which is what `preprocess()` + `PCA_compression()`
  actually do.
- `Mission-related: Ingest`, `Mission-related: Operations`, `Mission-related: Instrumentation`,
  `Mission-related: Monitoring` — **rejected.** `prepGUI` reads raw frames from a directory and
  `slitTest()` displays a diagnostic, but nothing commands the instrument, schedules observations,
  interfaces with hardware, or monitors telemetry. Seeing is a free-text field the operator types
  into `makeCatalogFiles`, not a measured monitoring product.
- `Mission-related: Distribution/Access` — **rejected.** `makeCatalogFiles` prepares the packages the
  website distributes, which is already covered by `Mission-related: Archive`; the client-side
  `search`/`download` pair is `Data Processing and Analysis: Data Access and Retrieval`.
- `Mission-related: Observatory/Instrument Models` and `Models and Simulations: Instrument Response`
  / `Models and Simulations: Observatory/Instrument Models` — **rejected in favour of the single
  `Mission-related: Instrument Response`.** `get_echelle_res` and `spectral_range` exist to serve the
  FISS wavelength-calibration path, not as a general instrument-simulation capability, so the
  Mission-related placement is the honest one and the three near-duplicates would only dilute it.
- `Models and Simulations: First Principles` — **rejected** in favour of `Physics-Based`. The
  three-layer inversion is a physically motivated, semi-analytic radiative-transfer model with
  height-varying absorption profiles, not an ab initio solution of the radiative-transfer equations.
- `Servers and Environments` and all its children — **rejected.** No Dockerfile, no Singularity
  recipe, no Kubernetes manifest, no server, no `mpi4py`. `joblib.Parallel` with
  `multiprocessing.cpu_count()` is single-node multicore work-sharing inside the inversion, which is
  not `High Performance Computing` in this taxonomy's sense.

### 5. Related Region (MANDATORY)

- `Chromosphere`
- `Photosphere`
- `Solar Environment`

All three are exact `Region` vocabulary values.

`Solar Environment` was for a long time the only region on this record. It remains correct but is too
broad on its own, and that one-value classification is what the list above supersedes.
`Chromosphere` and `Photosphere` are recorded because they are the specific regions FISS observes and
fisspy models, and the field guidance prefers the most specific applicable region:

- FISS records the Hα 6563 Å and Ca II 8542 Å bands, both chromospheric diagnostics.
  `fisspy/correction/get_inform.py:30 get_centerWV()` and `:6 get_lineName()` key the whole package
  off those two lines, and `fisspy/read/read_factory.py:280` selects a band-specific colour map per
  line.
- The photosphere is modelled explicitly, not incidentally. `fisspy/read/readbase.py:16
  Photolinewv()` exists "To specify the spectral line used to determine photospheric velocity" and
  returns photospheric line wavelengths 6559.580 Å (Hα band) and 8536.165/8548.079 Å (Ca II band);
  `fisspy/correction/correction.py:163 wvCalib_w_photo()` calibrates wavelength using that
  photospheric line; and the inversion's three layers are one photospheric plus two chromospheric,
  with `cal_3layers(..., phonly=False)` (`fisspy/inversion/_mlsi_base.py:316`) able to return the
  photospheric contribution alone.

Rejected: `Corona` — FISS observes neither coronal emission nor coronal temperatures; the coronal
rain studied with FISS/GST is chromospheric-temperature plasma seen in Hα, and coronal abundance
work using FISS relies on a *separate* coronal instrument (Hinode/EIS) for the coronal part.
`Solar Interior` — no helioseismic inversion of the interior; the umbral-oscillation work is
chromospheric. `Solar Wind`, `Interplanetary Space`, `Heliosheath` and every Earth and planetary
region — nothing in the package touches them.

### 6. Authors (MANDATORY)

**Author 1 — Juhyung Kang**

- **Author Identifier:** `https://orcid.org/0000-0003-3540-4112`
- **Affiliation:** Seoul National University — `https://ror.org/04h9pn542`

The name and the affiliation are carried over from the existing HSSI record. This author was
previously recorded with no identifier at all, so the ORCID above is the one part of this entry that
does not come from the prior record — and it is the strongest identity evidence the entry has.

**Why this ORCID is certainly the right person.** The identification does not rest on the name alone.

1. The ORCID record's primary name is "Juhyung Kang" and its *other-name* is "Juhyeong Kang" — the
   two spellings this repository's own commit history alternates between (225 commits as
   `Juhyeong Kang`, 168 as `Juhyung Kang`, 5 as `kailia0209`, all under the one address
   `jhkang@astro.snu.ac.kr`). No other Kang ORCID carries that pair.
2. Its only keyword is "Solar Physics".
3. Its publication list contains the two papers whose algorithms this package implements:
   "Multilayer Spectral Inversion of Solar Hα and Ca II 8542 Line Spectra with Height-Varying
   Absorption Profiles" (JKAS 54, 2021 — implemented as `fisspy/inversion/_mlsi*.py`, whose classes
   are literally named `MLSI4file`, `MLSI4profile` and `IMLSI`) and, first-authored,
   "Calibration of the Fast Imaging Solar Spectrograph: Fringe Reduction Using the Wavelet Transform"
   (JKAS 58, 2025 — implemented as `cal_fringeGauss`/`cal_fringeSimple` in
   `fisspy/preprocess/proc_base.py`).
4. It also lists "Development of the SNU Coelostat: Conceptual Design" (JKAS 51, 2018) and several
   FISS/GST observational papers, tying the holder to Seoul National University and to this
   instrument.
5. The project's own personnel page (`http://fiss.snu.ac.kr/people/`) lists Juhyung Kang as a
   post-doctoral researcher in the SNU Solar Astronomy Group.

The three other ORCID records matching "Juhyung Kang" were checked and excluded: `0000-0003-2960-218X`
and `0000-0001-5358-9523` have no works and no affiliation, and `0000-0003-1847-5314` is at
Chung-Ang University with an unrelated record.

**Affiliation.** `Seoul National University` is confirmed as the ROR `https://ror.org/04h9pn542`
preferred name (ROR also records the acronym SNU, the romanisation "Seoul Daehakgyo" and 서울대학교;
country South Korea). No department is added: the author's ORCID record exposes no employments, and
the stored institution-level value is correct. The email domain `astro.snu.ac.kr` would support
"Department of Physics and Astronomy" if a department-level value is ever wanted.

**Considered and not added.**

- **"SNU Solar Group" as an organization author.** `fisspy/__init__.py:14` sets
  `__author__ = "SNU Solar Group"`, and `LICENSE.txt` is copyright "2016-2019, FISSPy developers".
  Both are collective credits. It was not added as a second author because (a) no ROR exists for the
  research group — ROR resolves Seoul National University itself, which is already carried as the
  affiliation, so an organization author would either duplicate that identifier or be stored with no
  identifier at all; and (b) the packaging metadata that names an individual is unanimous —
  `setup.py` `author='Juhyung Kang'`, PyPI `author`, the conda-forge recipe maintainer `jhkang0301`,
  the PyHC registry `contact: "Juhyeong Kang"` — and the commit history shows exactly one human
  contributor across 398 commits. Adding a group author would imply co-authorship the repository does
  not evidence.
- **The FISS instrument "Development Staff"** listed on `http://fiss.snu.ac.kr/people/` (Jongchul
  Chae, Hyungmin Park, Kwangsu Ahn, Heesu Yang at SNU; Young-Deuk Park, Kyung-Suk Cho, Bi-Ho Jang,
  Jakyoung Nah at KASI). These built the *instrument*, not this software, and none appears in the
  repository's commit history or packaging metadata.
- **The recorded name needs no correction.** `Juhyung Kang` matches `setup.py`, PyPI and the ORCID
  primary name exactly. The commit-history variant "Juhyeong Kang" is the same person's alternate
  romanisation and is recorded as an ORCID other-name, not a competing spelling to be adopted; a
  future agent should not read it as a correction.

**Durable upstream limitation to carry forward.** HSSI's API has not reliably been able to alter an
author's already-stored name or identifier — name changes have been observed to no-op silently, and
changing an identifier is the same class of operation. If a later refresh needs to correct this
author's name, affiliation or ORCID, expect the API route to be unreliable: read the stored value
back to confirm any such change actually took effect, and treat a direct correction in HSSI as the
dependable remedy rather than repeating the attempt.

### 7. Software Name (MANDATORY)

`fisspy`

The stored value, retained deliberately. Field 7 asks for "the name of the software package as
listed on the code repository": the repository is `SNU-sunday/fisspy`, the PyPI distribution is
`fisspy`, the conda-forge package is `fisspy`, and the importable package directory is `fisspy/`.

**`FISSpy` was considered and rejected as a change.** It is the project's display styling — the
README's H1 is `# FISSpy`, the documentation site titles itself "FISSpy Documentation", and SoMEF's
`full_title` regex returns `FISSpy` — and `fisspy/__init__.py` uses a third styling, `FISSPy`, in its
module docstring. With three casings in use upstream and none of them the distribution name, changing
the stored value would be a stylistic edit with no authority behind it. The display forms are
recorded here so a future agent does not mistake them for a correction.

### 8. Description (MANDATORY)

> The Python Package for data analysis of the GST/FISS instrument. FISSpy reads, calibrates, aligns,
> analyses and visualizes data from the Fast Imaging Solar Spectrograph (FISS), the dual-band imaging
> spectrograph on the 1.6 m Goode Solar Telescope at Big Bear Solar Observatory, recording Hα and
> Ca II 8542 Å spectrograms simultaneously. It reads the whole FISS product chain as spectral cubes
> with FITS headers, runs the instrument's calibration pipeline from raw frames to archived products,
> co-aligns the two camera bands and long time series, and measures Doppler velocities, atmospheric
> parameters by spectral inversion, and oscillations and horizontal flows. Visualization includes
> interactive raster, spectrogram and profile viewers, montages and movie export. It assumes
> FISS-convention FITS data and is an instrument-specific toolkit rather than a general-purpose solar
> data framework.

893 characters.

**The maintainer's own sentence leads the description.** The stored HSSI value was the single
sentence `The Python Package for data analysis of the GST/FISS instrument.` — the README's tagline,
verbatim — and **it is preserved verbatim as the first sentence above**, so the maintainer's wording
is not lost and continues to lead the record.

**Why the tagline alone was insufficient.** Field 8 asks for a description "sufficiently detailed to
provide the potential user with information to determine if the software is useful to their work.
Include what the software does, why to use it, assumptions it makes". Sixty-four characters cannot
do that for a 17,153-line package spanning a calibration pipeline, an inversion code, an alignment
library, wavelet analysis and a movie/catalogue publisher — a user searching HSSI for spectral
inversion or image co-alignment would never learn from the one-liner that fisspy offers them. That is
why the maintainer's sentence is followed here by a capability summary and by the software's
assumptions, and why this field is longer than the tagline it opens with.

**The description is deliberately scoped to discovery rather than documentation, and that scope is
settled.** It stops well short of enumerating each reader class and FISS product type, each
calibration step, each analysis routine, and the named algorithms behind them (the λ-meter/bisector
method, the three-layer atmosphere, Morlet/Paul/DOG mother functions, the Differential Affine
Velocity Estimator). That level of detail is what a reader goes to the documentation for, not what a
discovery record should carry. Nothing is lost by leaving it out: the full capability breakdown, with
every module, function and line citation, is retained in the Field 4 evidence, and the project's own
manual at `http://fiss.snu.ac.kr/fisspy/` documents the same ground for users. A future agent should
not expand this field from Field 4.

The first sentence of Field 8 and the whole of Field 9 now overlap closely, since both open on the
maintainer's tagline. That is expected and is not a reason to remove Field 9, which is the
search-preview form and has to stand on its own.

Every clause of the description traces to code cited under Field 4. The instrument facts (dual-band
imaging spectrograph, simultaneous Hα 6563 Å and Ca II 8542 Å spectrograms, the 1.6 m Goode Solar
Telescope at Big Bear Solar Observatory) come from the project's instrument page
(`http://fiss.snu.ac.kr/instrument/`) and from Chae et al. 2013 (Field 27). The closing assumption
clause is load-bearing in the code, not editorial colour: the plate scale is hard-coded as
`self.xDelt = 0.16` / `self.yDelt = 0.16` at `fisspy/read/read_factory.py:234-235` and `:712`, and
`fisspy/correction/get_inform.py:6 get_lineName()` recognises only the instrument's own band set.

### 9. Concise Description (OPTIONAL)

> The Python Package for data analysis of the GST/FISS instrument: reading, calibrating, aligning,
> inverting and visualizing Fast Imaging Solar Spectrograph imaging-spectroscopy data.

181 characters, within the 200-character limit. The HSSI record previously carried no concise
description at all.

This exists specifically so that expanding Field 8 does not change what a search result shows: the
preview keeps the maintainer's own sentence word for word and appends only the capability summary
that makes the entry findable. Without it, the preview would be the first 150–200 characters of the
long description, which would cut mid-sentence inside the instrument's description.

### 10. Publication Date (RECOMMENDED)

`2017-02-24`

The field is "date of first broadcast/publication … used for the initial version of the software",
so this is the date fisspy first became publicly installable: the PyPI upload of version 0.7.2,
timestamped `2017-02-24T12:31:07Z` in the PyPI JSON API's release history (the earliest of the 34
releases from 0.7.2 through 1.3.0).

Rejected alternatives, with reasons:

- `2016-07-25` — the GitHub repository creation date and the date of the `Initial commit`
  (`9d8c619`, by `kailia0209`). Rejected because the first seven months of the repository predate any
  release; a source tree becoming visible is not a publication of the software. Recorded here because
  it is the correct answer if the field is ever reinterpreted as first public availability of the
  code.
- `2019-07-01` — the first conda-forge upload (0.9.61), whose `upload_time` the Anaconda API gives
  as `2019-07-01T06:56:59Z`; the `conda-forge/fisspy-feedstock` repository's `created_at` and first
  commit are both 2019-07-01 as well. Later than PyPI, and conda-forge is the project's
  *recommended* channel but not its first.
- `2025-07-18` — the current release; that is Field 12's version date, not the first publication.

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** `https://github.com`

Field 11 directs that "if no DOI has been obtained, indicate the repository host, such as GitHub or
GitLab", and no DOI exists (Field 2). A URL rather than a ROR is used because ROR has no record for
GitHub at all — a registry query for that name returns nothing — and the field permits a URL when no
ROR exists.

Rejected alternatives: **Zenodo**, which the field names first, does not apply because there is no
Zenodo record. **PyPI** and **conda-forge** are the actual distribution channels (and conda-forge is
the channel the project recommends), but the field's instruction names the repository host, and
choosing between two package indices would be arbitrary. **Seoul National University** is the
author's institution and the documentation host; it publishes the data, not the software releases.

### 12. Version (RECOMMENDED)

- **Version Number:** `1.3.0`
- **Version Date:** `2025-07-18`
- **Version PID:** Not found
- **Version Description:** Exposes the multilayer spectral inversion API at package level —
  `fisspy.inversion` now provides `MLSI4file`, `MLSI4profile` and `IMLSI`, where previously the
  subpackage had an empty `__init__.py` and its contents were reachable only through private module
  paths. Reworks observation-catalogue generation in `fisspy.image.raster_set`: the
  `makeRecDataJSON` class is replaced by `makeOBSmovie`, `__all__` now exports both `makeRasterSet`
  and `makeOBSmovie`, and two new module-level helpers appear, `upateJSON` and a module-level
  `saveJSON` function. The module's other module-level helpers `flipInv`, `pjsonIMGtag` and `zipComp`
  pre-date this release — each is byte-identical between v1.2.1 and this revision — and are not
  part of what 1.3.0 added. Adds `PCA_compression_new` and `cloud` to `fisspy.preprocess.proc_base`.
  Fixes a colour-map attribute typo (`cm.ㄴfe` → `cm.fe`) that raised an `AttributeError` for any
  `FISS` object opened on the Fe I band.

**Version number and date.** `setup.py` and `fisspy/__init__.py:15` both declare `1.3.0`; PyPI's
latest release is `1.3.0`, uploaded `2025-07-18T04:23:38Z`; conda-forge's `fisspy-1.3.0` was built
`2025-07-18T04:41:43Z` from a recipe pinning `{% set version = "1.3.0" %}` and the sdist checksum
`2cfbc15e744428950e858bf2b2116e0a8862ed9c7966f6d6dd2d93be33cd9038`. The recorded revision
`8e77704` is dated `2025-07-18 17:11:59 +0900`, the same day. The version number is recorded **bare**
as `1.3.0`; HSSI's read API renders a `name - version` display string, and copying that rendered
form back into the stored field would corrupt it.

**Do not report 1.2.2.** The merge commit at HEAD reads "Merge pull request #49 from
SNU-sunday/v1.2.2", and a stale `origin/v1.2.2` branch exists, but the tree it merged declares
`1.3.0` in both `setup.py` and `fisspy/__init__.py`, and `1.2.2` was never released to PyPI or
conda-forge. The branch name is simply wrong.

**Version PID is empty** as a direct consequence of Field 2 — no DOI exists for any version.

**Provenance of the version description, and why one had to be derived.** Upstream publishes no
release notes of any kind: there is no `CHANGELOG`, `NEWS`, `HISTORY` or `whatsnew` file at any
revision, the repository has **no git tags and no GitHub releases** (neither GitHub's tag nor its release listing holds anything), PyPI
carries no description body (`description_content_type: null`), and the commit subjects across this
release range are `backup` and `abc`. The description above is therefore derived from the complete
`origin/v1.2.1..8e77704` diff, restricted to source files: `fisspy/inversion/__init__.py` (+1 line,
the new public import), `fisspy/image/raster_set.py` (795 lines changed), `fisspy/preprocess/proc_base.py`
(+153), `fisspy/preprocess/proc_gui.py` (34), `fisspy/read/read_factory.py` (1 line, the typo fix),
`fisspy/image/__init__.py` (whitespace only), and the two version declarations. A future agent
refreshing this record should expect to derive the next version description the same way.

### 13. Programming Language (RECOMMENDED)

`Python 3.x`

An exact `ProgrammingLanguage` vocabulary value, carried over from the existing HSSI record.
The GitHub languages API reports a single language, `{"Python": 627906}` — 100% Python, no compiled
extensions. `setup.py` sets `python_requires='>=3.6'`; the conda-forge recipe requires
`python >=3.6` and builds `noarch: python`.

`Python 2.x` is excluded despite the `from __future__ import absolute_import, division` headers that
survive in most modules: those are legacy compatibility lines, and the declared floor is 3.6.

`IDL` is deliberately **not** listed, even though this software has close IDL relatives. The
alignment routine is a port of J. Chae's IDL `ALIGNOFFSET.PRO` (`fisspy/align/base.py:38-39`), the
optical-flow routine is "the python function of dave_multi.pro IDL code written by J. Chae (2009)"
(`fisspy/analysis/ofe.py:20`), and the wavelet module derives from `WAVELET.PRO`
(`fisspy/analysis/wavelet.py:65`) — but all three are *ports*, and there is not one line of IDL in
this repository. The project's actual IDL code lives in the separate repository recorded under
Field 29.

### 14. Reference Publication (RECOMMENDED)

**Not found — fisspy has no publication that describes the software.**

This is a considered determination, not an unfinished search. Field 14 asks for "the DOI for the
publication describing the software, sometimes used as the preferred citation for the software". No
such paper exists: there is no JOSS, A&C, SoftwareX or similar software paper; the README contains no
"how to cite" section; and the project's own acknowledgement page
(`docs/acknowledge.html`) states outright that "There is no rule how to acknowledge and it's fully up
to you" — a project with a designated reference publication would say so there.

Three papers were evaluated as candidates and all three were routed to Field 27 instead, because each
describes an *instrument* or a *method* rather than this software:

1. **Chae et al. 2013**, `https://doi.org/10.1007/s11207-012-0147-x` — "Fast Imaging Solar
   Spectrograph of the 1.6 Meter New Solar Telescope at Big Bear Solar Observatory", Solar Physics
   288, 1–22. The instrument paper. It predates most of the package (fisspy's first commit is 2016)
   and describes hardware. An instrument paper is not the software's reference publication.
2. **Chae et al. 2021**, `https://doi.org/10.5303/JKAS.2021.54.5.139` — the multilayer spectral
   inversion method. Describes the algorithm `fisspy/inversion/` implements, not the implementation.
3. **Kang et al. 2025**, `https://doi.org/10.5303/JKAS.2025.58.1.63` — "Calibration of the Fast
   Imaging Solar Spectrograph: Fringe Reduction Using the Wavelet Transform", first-authored by
   fisspy's author, and the closest candidate: it reports that the preprocessing pipeline it
   describes has been integrated into FISSpy. It is still a calibration-method paper about one part
   of the package, not a software paper, and the project does not nominate it as the citation.

Candidate 3 was weighed as the value for this field and deliberately left in Field 27 instead:
naming it here would assert a preferred citation the project itself has never expressed, and the
project explicitly declines to prescribe one. This field is therefore empty as a settled
determination — the papers exist and are recorded where they belong, but none of them is fisspy's
reference publication.

### 15. License (RECOMMENDED)

- **License:** `BSD 2-Clause "Simplified" License`
- **License URI:** `https://spdx.org/licenses/BSD-2-Clause.html`

The exact controlled License value, carried over from the existing HSSI record and corroborated
four ways: `LICENSE.txt` carries the two-clause BSD text ("Copyright (c)
2016-2019, FISSPy developers", redistribution-in-source and redistribution-in-binary clauses only, no
third non-endorsement clause); `setup.py` declares `license='BSD-2'`; the conda-forge recipe declares
`license: BSD-2-Clause` with `license_file: LICENSE.txt`; and the GitHub API reports SPDX
`BSD-2-Clause`.

The recorded string, with its straight double quotes around *Simplified*, is the exact controlled
License value and must be reproduced character for character: a curly quote or a dropped word is a
different string and does not denote this license.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

The HSSI record previously carried no keywords. All lowercase, one term per entry.

- `solar physics`
- `solar imaging`
- `imaging spectroscopy`
- `spectroscopy`
- `spectrograph`
- `chromosphere`
- `photosphere`
- `doppler velocity`
- `spectral inversion`
- `radiative loss`
- `calibration`
- `data reduction`
- `image processing`
- `image alignment`
- `optical flow`
- `wavelet analysis`
- `time series analysis`
- `oscillations`
- `data visualization`
- `interactive`
- `gui`
- `fits`
- `python`

Each term is earned by code or by curated upstream metadata: `imaging spectroscopy` is the
instrument's observing mode (the instrument page: "we can obtain the data including not only spectral
information but also spatial information, imaging spectroscopy data"); `doppler velocity` is
`fisspy/analysis/doppler.py`; `spectral inversion` and `radiative loss` are `fisspy/inversion/`
(`RadLoss`, `_RadLossBase`); `image alignment` is `fisspy/align/`; `optical flow` is
`fisspy/analysis/ofe.py`; `gui` and `interactive` reflect `prepGUI`, `IMLSI`, `MLSI4profile` and the
keyboard-driven `imshow` viewers; `oscillations` reflects the time–distance period measurement and
the package's dominant science use.

The GitHub repository topics — `astronomy`, `fiss`, `fiss-instrument`, `fisspy`, `python`, `solar`,
`solar-physics`, `sun` — were used as a source and are covered by `solar physics`, `python` and the
instrument fields, so `fiss`, `fiss-instrument` and `fisspy` were **not** included as keywords: the
instrument and the software's own name are carried by Fields 7 and 31, and duplicating them as
keywords would add noise. PyHC's curated keywords for fisspy are `["solar","specific"]`; `specific`
is a PyHC taxonomy marker meaning "instrument-specific", not a science keyword, and was excluded.

Also rejected: `sun` (subsumed by `solar physics`), `spectra` (subsumed by `spectroscopy`),
`sunspots` and `mhd waves` (science topics of papers *using* fisspy, not capabilities of the package
— fisspy contains no sunspot or wave-mode-specific code), and `numba` (declared as a dependency but
never imported; see Field 21).

### 17. Data Sources (OPTIONAL)

- `Observatory/Mission-specific`
- `HTTP/HTTPS Directories`

Both are exact `DataInput` vocabulary values. The HSSI record previously carried no data source.

`Observatory/Mission-specific` is the primary value and follows the field's own instruction to pair
it with the observatory in Field 32 (Big Bear Solar Observatory is already stored there). fisspy
retrieves data from exactly one archive, the FISS project's own:

- `fisspy/data/download.py:37` requests the observation index `http://fiss.snu.ac.kr/data_list/`, and
  `:9` sets the data root `http://fiss.snu.ac.kr/static/data/`, from which `download()` builds
  per-observation paths `{root}{yyyy}/{yyyymmdd}/data/{target}.zip`.
- `fisspy/data/_sample.py:14` retrieves sample FISS files from `http://fiss.snu.ac.kr/sample-data/`.
- `fisspy/preprocess/proc_base.py:1114` retrieves the reference solar atlas from
  `http://fiss.snu.ac.kr/static/atlas/solar_atlas.npz`.

`HTTP/HTTPS Directories` is included because that is literally the access mechanism: plain
`urllib.request.urlopen`/`Request` (`download.py:37-38`), `urllib.request.urlretrieve`
(`proc_base.py:1115`) and `astropy.utils.data.download_file` against a date-structured HTTP directory
tree. Note the scheme is `http://` only; the host refuses HTTPS.

Rejected, all after checking the source: `CDAWeb`, `The Virtual Solar Observatory.`, `HAPI`,
`SSCWeb`, `OMNIWeb`, `AMDA`, `Madrigal`, `VirES`, `GFZ`, `WDC`, `das2`, `TAP`, `S3/Cloud-aware` and
`FTP/FTPS Directories` — none appears anywhere in the package; there is no `sunpy.net.Fido`, no
`astroquery`, no `hapiclient`, no `boto3`, and no FTP client. `Other` was rejected as unnecessary
once the two specific values above were established.

### 18. Input File Formats (RECOMMENDED)

- `FITS`
- `JSON`
- `Other`

All three are exact `FileFormat` vocabulary values, determined by reading the package's I/O paths
rather than its documentation.

**FITS** is the primary input and the format of every FISS data product. Read through
`astropy.io.fits` at `fisspy/read/readbase.py:79,113,116,149` (`getdata`, `getheader`),
`fisspy/read/read_factory.py:48,707,791,1288,1543`, `fisspy/preprocess/proc_base.py:584,1140,1156,1366,1418,1480,1536`,
`fisspy/preprocess/proc_gui.py:3003,3130`, `fisspy/preprocess/t_y_sh.py:31,50`,
`fisspy/analysis/ofe.py` and `fisspy/image/raster_set.py:454-455`. Note the instrument's files carry
the `.fts` extension, and `getHeader()` (`readbase.py:140`) additionally parses FISS-specific header
conventions out of FITS `COMMENT` cards for PCA-compressed files.

**JSON** — the observation-catalogue records are read back and updated:
`fisspy/image/raster_set.py:467-468` (`pjsonIMGtag`), `:511-512` (`zipComp`) and `:543-544`
(`upateJSON`) each `json.load` an existing catalogue file.

**Other** covers two real input formats for which no specific controlled value represents the format:

- **NumPy `.npz` archives**, which are how fisspy persists and reloads its own derived products:
  align cubes (`fisspy/read/read_factory.py:1353`, `AlignCube`), alignment parameters
  (`fisspy/align/alignment.py:221 readAlignPars`), saved inversion parameters
  (`fisspy/inversion/_mlsi.py:532`), and the reference solar atlas plus the tilt/shift table shipped
  in the package (`fisspy/preprocess/proc_base.py:1116`; `solar_atlas.npz`, `t_y_sh.npz`).
- **PNG/JPEG image sequences**, read by the movie builder via `matplotlib.pyplot.imread` and
  `PIL.Image.open` (`fisspy/makevideo.py:16-17,82`).

`ascii` was considered and **rejected**: nothing in the package reads a text data file. There is no
`np.loadtxt`, no `genfromtxt`, and no text-mode read of a data file. The one plain-text file in the
tree, `fisspy/analysis/sample/sst_nino3.dat` (a single column of NINO3 sea-surface-temperature
values), is the Torrence & Compo wavelet demonstration series and is referenced by no code path —
`sst_nino3` appears nowhere in the source. `CDF`, `HDF5`, `netCDF3/4`, `IDL.sav`,
`ISTP-Compliant`, `csv` and `Zarr` were all rejected: no `cdflib`, `spacepy.pycdf`, `h5py`,
`netCDF4`, `scipy.io.readsav`, `zarr` or `read_csv` import exists, and no ISTP conventions are
implemented (FISS headers are the instrument's own convention).

### 19. Output File Formats (RECOMMENDED)

- `FITS`
- `JSON`
- `Other`

Same `FileFormat` vocabulary as Field 18.

**FITS** — every pipeline and analysis product is written as FITS via `hdu.writeto`:
calibration flats and slit patterns (`fisspy/preprocess/proc_base.py:954,975`;
`fisspy/preprocess/proc_gui.py:2837,2851,2864`), calibrated proc files (`proc_base.py:1193`),
the PCA coefficient and basis-profile files (`proc_base.py:1413,1446` and `:1531,1569`),
inversion parameter files (`fisspy/inversion/_mlsi.py:117`, scaled to `int16` with per-plane
`SCALE##` header keys plus `fileorig`, `version` and `runtime` provenance),
optical-flow results (`fisspy/analysis/ofe.py:199`), and flipped inversion products
(`fisspy/image/raster_set.py:458,460`).

**JSON** — the catalogue records written by `makeCatalogFiles`
(`fisspy/image/raster_set.py:406`), `saveJSON` (`:566`) and `pjsonIMGtag` (`:486`).

**Other** covers four real output formats for which no specific controlled value represents the format:

- **NumPy `.npz`** — alignment parameters (`fisspy/align/alignment.py:194`), aligned data cubes
  (`:491`), wavelet results (`fisspy/analysis/wavelet.py:393`), time–distance maps and their
  measurements (`fisspy/analysis/tdmap.py:409,411,904`), and interactive inversion parameter sets
  (`fisspy/inversion/_mlsi.py:523`).
- **MPEG-4 video** — `fisspy/makevideo.py:24 ffmpeg()` and `fisspy/image/raster_set.py:311-314,356-357`.
- **PNG figures** — `fig.savefig` at `fisspy/image/raster_set.py:271,850,1012`.
- **ZIP archives** — `fisspy/image/raster_set.py:372,524,763,772` bundle the compressed observation
  for archive publication.

`ascii` was **rejected** for output as well, with one borderline case recorded so it is not
relitigated: `fisspy/makevideo.py:99` writes a temporary text file `img_list.tmp` listing the input
frames. It is a transient argument file consumed immediately by the external ffmpeg binary and
deleted, not a data product, so it does not make ascii a supported output format. `CDF`, `HDF5`,
`netCDF3/4`, `IDL.sav`, `ISTP-Compliant`, `csv` and `Zarr` are all unsupported for output for the
same reasons as Field 18.

### 20. Operating System (RECOMMENDED)

`Operating System Independent`

Note that the `OperatingSystem` vocabulary spells this value out in full: `OS Independent` is not a
valid value and would be rejected, so the abbreviated form must never be substituted here.

Evidence: the conda-forge recipe builds `noarch: python`, which asserts platform independence and
produces one artifact for all platforms (`noarch/fisspy-1.3.0-pyhd8ed1ab_0.conda`); PyPI ships only
`fisspy-1.3.0-py3-none-any.whl`, whose `none-any` tags assert no ABI or platform dependency; the
package is 100% Python with no compiled extension; and no module branches on `sys.platform`,
`os.name` or a path separator. All paths are built with `os.path.join`. Development happens on macOS
(the tracked `.DS_Store` files) while the FISS site's installation guide targets miniforge/mamba
generically.

`Linux`, `Mac` and `Windows` were considered and rejected as individually-listed values: they would
be a less precise restatement of what `Operating System Independent` already asserts, and no CI
matrix exists to substantiate a per-platform claim (the repository has no `.github/workflows`, no
`.travis.yml` and no other CI configuration at any revision). The only platform-sensitive element is
the external `ffmpeg` binary needed for movie export, which is a declared dependency in both
`setup.py` and the conda recipe and is available on all three platforms.

### 21. CPU Architecture (RECOMMENDED)

`CPU Independent`

An exact `CpuArchitecture` vocabulary value, resting on the same evidence as Field 20: a
`noarch: python` conda build and a `py3-none-any` wheel, pure Python with no compiled extension and
no intrinsics.

One nuance worth recording, because it could look like a contradiction later. `numba` is declared in
`setup.py` `install_requires` and in the conda recipe, and numba's LLVM back end supports a finite
set of architectures. **fisspy itself never imports numba** — `numba`, `njit`, `jit` and
`guvectorize` appear zero times in the source. It is present only because
`interpolation>=2.2.6` (EconForge `interpolation.py`, used for the spline resampling in
`fisspy/align/base.py`, `fisspy/analysis/doppler.py`, `fisspy/analysis/tdmap.py`,
`fisspy/analysis/forecast.py` and `fisspy/preprocess/proc_base.py`) is numba-JIT-based. Effective
architecture coverage is therefore whatever numba supports, but nothing in fisspy's own source or
packaging narrows the architecture, so `CPU Independent` is the correct declaration.
`GPU`, `HPC or HEC`, `Sun (SPARC)` and `ppc64le` were rejected — there is no CUDA/OpenCL, no MPI, and
no architecture-specific build.

### 22. Related Phenomena (OPTIONAL)

**Not applicable — no specific controlled value represents a phenomenon this software supports.**

This is a documented omission reached by examining all seven values in the `Phenomena` vocabulary,
which is a closed list, so a custom term is not an option:

- `Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`, `X-ray emission` — fisspy observes and
  models the photosphere and chromosphere in Hα and Ca II 8542 Å. It has no coronal or X-ray
  capability of any kind.
- `Solar Wind`, `Geomagnetic Storms` — entirely outside the package's scope; nothing in the source
  touches the heliosphere or geospace.
- `Solar Flares` — the closest candidate, and it was seriously considered: FISS/GST routinely
  observes flares, and papers using FISS data analyse flare-driven coronal rain and flare triggering.
  It was rejected because the software is phenomenon-agnostic — the string `flare` appears **zero
  times** in 17,153 lines of source, there is no flare detection, flare-mode reading, or
  flare-specific analysis, and the observation "events" that `makeCatalogFiles` records are free text
  an operator types in (the shipped example values are `['transverse MHD waves', 'fibrils']`,
  `fisspy/image/raster_set.py:1046`). Selecting it would attribute a capability that does not exist.

The phenomena fisspy genuinely serves — chromospheric and photospheric oscillations, sunspot umbral
waves, MHD wave propagation, spectral line formation, Ellerman bombs, spicules and fibrils — are none
of them represented by a specific controlled value in this seven-value vocabulary. Per the field's own
instruction (a phenomenon the software supports that the vocabulary does not represent belongs in
Keywords), `oscillations` was routed to Field 16 instead.

`Solar Flares` is the only value for which any argument could be constructed, and it was considered
and rejected for the reason above. This field is a settled documented omission: an empty Related
Phenomena is the accurate statement about a phenomenon-agnostic instrument toolkit, and the
enumeration above is recorded so the emptiness is not mistaken for an unfinished search.

### 23. Development Status (RECOMMENDED)

`Active`

An exact `RepoStatus` vocabulary value; the HSSI record previously carried no development status.
Per repostatus.org, Active means "reached a stable, usable state and is being actively developed",
which fits:

- Stable and usable: 34 PyPI releases from 0.7.2 (2017) to 1.3.0, 20 distinct conda-forge versions
  (21 build artifacts; one version was rebuilt), a documented public API, and a complete user manual
  at `http://fiss.snu.ac.kr/fisspy/`.
- Actively developed: 398 commits; releases 1.0.0 through 1.1.5 through 2024 (fourteen in 2024
  alone), then 1.2.0, 1.2.1 (2025-04-03) and 1.3.0 (2025-07-18). Last push to `master`
  2025-07-18, about a year before this extraction. Not archived; zero open issues.
- PyHC's curated assessment rates `software_maturity` **Good** and `python3` **Good**.

Counter-evidence weighed and found insufficient to downgrade: PyHC rates `community` and `testing`
as "Requires improvement" and `documentation` as "Partially met"; there are no automated tests and no
CI; a colour-map typo (`cm.ㄴfe`) shipped in released version 1.2.1 and survived until 1.3.0; and
several commits in the current release range are titled `backup`. These describe development
*practice*, not project *status* — none of the vocabulary's alternatives fits better. `Inactive`
would require development to have stopped (a 2025 release contradicts it); `WIP` would require no
stable public release (34 releases contradict it); `Unsupported`, `Abandoned`, `Suspended` and
`Moved` are all contradicted by the 2025 release cadence and the live documentation site.

Re-examine this field if the next refresh finds no release after 1.3.0 and no commits for a
multi-year span — the 2020-07 to 2024-04 gap in the release history shows this project's cadence is
bursty, so a single quiet year is not evidence of inactivity.

### 24. Documentation (RECOMMENDED)

`http://fiss.snu.ac.kr/fisspy/`

The URL resolves and serves the full FISSpy manual: an installation page, a
Read Data section (overview, raw data, proc/comp data, align cube, two cameras, raster-set movie), an
Analysis Tools section (Doppler velocity, time–distance maps, time-series interpolation, wavelet,
optical flow), an Alignment section, and a Preprocess page. This is the URL `README.md` points to
("You can see the tutorials for the FISSpy on here") and that `fisspy/__init__.py:10` names as the
documentation link.

**The `http://` scheme is required, not an oversight.** `https://fiss.snu.ac.kr/fisspy/` fails with a
connection reset — the host does not serve TLS. Do not "correct" this to HTTPS.

Rejected alternatives:

- `https://github.com/SNU-sunday/fisspy/tree/master/docs` — what SoMEF returned via file exploration.
  That directory holds the site's Jinja source templates and Jupyter notebooks, not rendered
  documentation, and includes stale drafts (`index2.html`, `index_test.html`, `install2.html`,
  `fisspy_template.html`). The rendered site is strictly better for a user.
- `http://fiss.snu.ac.kr/` — the FISS *project* home (instrument description, data policy, data
  catalogue, publications, people). It is the `url=` in `setup.py` and PyPI's `home_page`, but it
  documents the instrument, not the software. The `/fisspy/` subtree is the software manual.
- Read the Docs — none exists; there is no `.readthedocs.yml` and no Sphinx configuration anywhere.
- PyHC's registry entry for fisspy has **no** `docs` field, so it offers no competing value.

### 25. Funder (OPTIONAL)

**Not found — no funder is attributable to this software.**

Negative research, recorded in full because this is a plausible-looking field that would be easy to
fill incorrectly:

- The repository contains no funding statement. `docs/acknowledge.html` is the project's own
  acknowledgement page and prescribes nothing: "There is no rule how to acknowledge and it's fully up
  to you."
- There is no `AUTHORS`, `CONTRIBUTING`, `CITATION.cff` or `codemeta.json` in which funding might be
  declared, and no DOI record to inherit `fundingReferences` from.
- **The National Research Foundation of Korea does not appear anywhere, and was specifically looked
  for** —
  not in the repository, not on the project website's software pages.
- The one funding statement the project does publish is on its **data policy** page
  (`http://fiss.snu.ac.kr/data_policy/`), and it is explicitly about the *data and the observatory*,
  not the software: "We gratefully acknowledge the use of data from the Goode Solar Telescope (GST)
  of the Big Bear Solar Observatory (BBSO). BBSO operation is supported by US NSF AGS-2309939 and
  AGS-1821294 grants and New Jersey Institute of Technology. GST operation is partly supported by the
  Korea Astronomy and Space Science Institute and the Seoul National University. Especially, Fast
  Imaging Solar Spectrograph(FISS) operation is supported by Korea Astronomy and Space Science
  Institute(KASI) and Seoul National University(SNU)."

Those grants fund telescope and instrument *operations*. Recording the National Science Foundation,
New Jersey Institute of Technology, the Korea Astronomy and Space Science Institute or Seoul National
University as funders of the fisspy software package would attribute observatory-operations awards to
a Python package, which the evidence does not support. The quotation is preserved here so a future
agent can see exactly what was found, recognise it as instrument funding, and not mistake it for
software funding.

### 26. Award Title (OPTIONAL)

**Not found — no award funds this software.**

Follows directly from Field 25. The two award numbers discoverable anywhere in the project's
materials, `AGS-2309939` and `AGS-1821294`, are National Science Foundation awards supporting Big
Bear Solar Observatory operations, quoted in the data-policy statement above. They are not fisspy
awards and are not recorded here. No award title, number or grant acknowledgement appears in the
repository at any revision.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

Three entries, each tied to a specific implemented capability rather than merely
sharing a subject with the software.

1. **`https://doi.org/10.1007/s11207-012-0147-x`** — Chae, J., Park, H.-M., Ahn, K., Yang, H.,
   Park, Y.-D., Nah, J., Jang, B. H., Cho, K.-S., Cao, W., & Goode, P. R. (2013). *Fast Imaging Solar
   Spectrograph of the 1.6 Meter New Solar Telescope at Big Bear Solar Observatory.* Solar Physics,
   288, 1–22. Confirmed against Crossref, which records the title, journal, volume, pages and all ten authors as
   given here.
   This is the FISS instrument paper, and the package **cites it in its own source** as the authority
   for the stray-light and spatial-resolution correction: `fisspy/correction/correction.py:347` and
   `:393` and `fisspy/read/read_factory.py:385` all carry
   "Chae et al. (2013), https://ui.adsabs.harvard.edu/abs/2013SoPh..288....1C/abstract" in the
   docstrings of `corSLA`, `corStrayLight` and `FISS.corSLA`, whose default parameters `eps=0.027`
   and `zeta=0.055` come from that paper.

2. **`https://doi.org/10.5303/JKAS.2021.54.5.139`** — Chae, J., Cho, K., Kang, J., Lee, K.-S.,
   Kwak, H., & Lim, E.-K. (2021). *Multilayer Spectral Inversion of Solar Hα and Ca II 8542 Line
   Spectra with Height-Varying Absorption Profiles.* Journal of the Korean Astronomical Society, 54,
   139–155. The DOI is registered and resolves to the JKAS article page, and is self-asserted on
   the second author's ORCID record, and the author list and pagination were confirmed against the
   FISS project's publication index. This is the method `fisspy/inversion/` implements — the module is
   `_mlsi.py` for Multi-Layer Spectral Inversion, its public functions are `MLSI4file`,
   `MLSI4profile` and `IMLSI`, and `_mlsi_base.py:316 cal_3layers()` is the paper's three-layer
   height-varying absorption model. fisspy's author is a co-author. The paper also appears as the
   example publication link in `fisspy/image/raster_set.py:1049`
   (`https://ui.adsabs.harvard.edu/abs/2021JKAS...54..139C`).

3. **`https://doi.org/10.5303/JKAS.2025.58.1.63`** — Kang, J., Song, D., Chae, J., Lim, E.-K., &
   Kubo, M. (2025). *Calibration of the Fast Imaging Solar Spectrograph: Fringe Reduction Using the
   Wavelet Transform.* Journal of the Korean Astronomical Society, 58, 63–70. The DOI is registered and resolves, and is
   self-asserted on the first author's ORCID record — the same
   `0000-0003-3540-4112` recorded as fisspy's author in Field 6. This is the strongest of the three
   because it is by the software's author *and* reports that the pipeline it describes is integrated
   into FISSpy; the implementation is `cal_fringeGauss` and `cal_fringeSimple`
   (`fisspy/preprocess/proc_base.py:149,197`) together with the wavelet-domain fringe subtraction
   inside `calFlat`.

**Considered and deliberately not listed.**

- **Torrence, C., & Compo, G. P. (1998). *A Practical Guide to Wavelet Analysis.* Bulletin of the
  American Meteorological Society, 79, 61–78.** DOI `10.1175/1520-0477(1998)079<0061:APGTWA>2.0.CO;2`
  (confirmed against Crossref). This is the algorithm `fisspy/analysis/wavelet.py` implements, cited six
  times in its docstrings (lines 70, 196, 258, 330, 452, 790) along with
  `http://paos.colorado.edu/research/wavelets/`. The module's own provenance statements credit the
  IDL originals by C. Torrence — `WAVELET.PRO` (lines 65, 191, 253, 325), `WAVE_SIGNIF.PRO` (line
  447) and `WAVE_COHERENCY.PRO` (line 786) — and nothing else. (E. Predybaylo's `waveletFunctions.py`
  is the widely-circulated Python port of those same IDL routines and is externally-known background
  to this algorithm's history, but fisspy never mentions it: the strings `Predybaylo` and
  `waveletFunctions` appear nowhere in the source tree, so no such provenance should be attributed to
  the module.) The paper is recorded here rather than listed for two reasons: it is a meteorology
  methods paper that neither describes, cites nor uses this software, and its DOI contains raw `<`,
  `>` and `;` characters, which do not survive an unencoded
  URL field — the percent-encoded form
  `https://doi.org/10.1175/1520-0477(1998)079%3C0061:APGTWA%3E2.0.CO;2` resolves and would be the
  form that would be required if it were ever added. The DOI is preserved above so that judgement
  never has to be re-researched.
- **A DAVE optical-flow reference.** `fisspy/analysis/ofe.py:20` credits only an IDL implementation —
  "This is the python function of dave_multi.pro IDL code written by J. Chae (2009)" — not a
  publication. The Differential Affine Velocity Estimator originates in the literature, but the
  package cites no paper for it, so no DOI is asserted here rather than guessing at one.
- **`https://ui.adsabs.harvard.edu/abs/2023ApJ...958..131K`**, the second example publication link in
  `fisspy/image/raster_set.py:1049` (Kwak et al. 2023, ApJ 958, 131, *Spectroscopic Detection of
  Alfvénic Waves in the Chromospheric Fibrils of a Solar-quiet Region*, per the FISS publication
  index). It appears only as demonstration data inside `demo()`, illustrating what an operator would
  put in a catalogue record's `publication` field. It is a paper that *used FISS data*, not one tied
  to a fisspy capability.
- **The 60-entry FISS publication list** at `http://fiss.snu.ac.kr/publication/`. These are science
  papers using FISS observations. Listing them would flood the field with work related to the
  instrument rather than to the software, and none of them describes, cites or is cited by fisspy.

### 28. Related Datasets (OPTIONAL)

`http://fiss.snu.ac.kr/data_list/`

The FISS observation data archive — the one dataset the software exists to process. This is the exact
index fisspy queries programmatically: `fisspy/data/download.py:37` requests it and parses its anchor
list to build the searchable observation table, from which `download()` fetches per-target ZIP
archives. A user who reaches this HSSI entry looking for the data
fisspy reads should land here.

**No DOI exists for FISS data.** The archive is served as an HTTP directory tree under
`http://fiss.snu.ac.kr/static/data/{yyyy}/{yyyymmdd}/data/{target}.zip` with no persistent
identifier, and the project's data policy asks users for a text acknowledgement (quoted under Field
25) rather than a DOI citation. Field 28 explicitly permits a link when no DOI is available, so a
URL is the correct form here.

Considered alternatives:

- **Chae et al. 2013 (`https://doi.org/10.1007/s11207-012-0147-x`)** as "the publication that
  described the dataset", which is Field 28's stated minimum. Rejected as the value here because it
  is already recorded in Field 27 and points at the instrument paper rather than at the data; a
  direct pointer to the archive carries more information for a user. The DOI is recorded here only so
  this alternative does not have to be re-investigated.
- **The BBSO/GST data archive** more broadly (`https://www.bbso.njit.edu/`). Rejected as too broad —
  fisspy reads FISS products specifically, not BBSO's other instruments.
- **The sample data** at `http://fiss.snu.ac.kr/sample-data/` and the reference solar atlas at
  `http://fiss.snu.ac.kr/static/atlas/solar_atlas.npz`. Rejected as supporting files for tutorials
  and calibration, not datasets the software is designed to analyse.

### 29. Related Software (OPTIONAL)

`https://github.com/SNU-sunday/FISS-IDL`

One entry, and the case for it is specific rather than generic.

**FISS-IDL** is the same group's IDL analysis code for the same instrument — GitHub describes it as
"IDL code for data analysis of GST/FISS instrument". It sits in the same organisation
(`SNU-sunday`) and was created on **2016-07-25**, the same day as fisspy's own repository, which is
the clearest possible evidence that the two are deliberate siblings rather than coincidental
neighbours. The project documents them side by side: the FISS site's navigation offers "Analysis
Routine (IDL)" and "Analysis Routine (Python)", and the IDL page
(`http://fiss.snu.ac.kr/manual_IDL/`) links to that repository and documents `fiss_read_frame`,
`fiss_raster` and `fiss_show_sp` — the direct IDL counterparts of fisspy's `readFrame`, `getRaster`
and the raster viewers, down to the same PCA `_c.fts`/`_p.fts` file convention. It is also the
lineage: several fisspy routines are explicit ports of J. Chae's IDL code
(`fisspy/align/base.py:38-39` from `ALIGNOFFSET.PRO`, `fisspy/analysis/ofe.py:20` from
`dave_multi.pro`). FISS-IDL was last pushed 2019-07-05, so fisspy is effectively its successor.
This is exactly Field 29's "software that performs similar tasks" plus a predecessor relationship.

**Considered and rejected.**

- **`https://github.com/SNU-sunday/fisspy-tutorials`** — a companion repository of Jupyter tutorials
  for fisspy, last pushed 2018-02-22. Rejected because it is teaching material rather than software
  performing a task, and because it has been superseded: the current tutorials are the notebooks
  under `docs/example/` and the rendered pages at `http://fiss.snu.ac.kr/fisspy/`. Recorded so a
  future agent recognises it as stale rather than as a missing link.
- **`sunpy`** — see Field 30; the single use of one URL-checking helper does not make it a
  characterising dependency, and Field 29 applies the same "would this be equally true of most
  packages" test.
- **`interpolation.py` (EconForge, `https://github.com/EconForge/interpolation.py`)** — a hard
  dependency (`interpolation>=2.2.6`) used for spline resampling in five modules. Rejected as generic
  numerical infrastructure: it is a general-purpose multilinear/cubic interpolation library written
  for economics, and would be equally at home in a finance model. It carries no heliophysics
  information about fisspy.
- **`numba`, `statsmodels`, `beautifulsoup4`, `joblib`, `pandas`, `PyQt5`, `Pillow`, `ffmpeg`,
  `matplotlib`, `numpy`, `scipy`** — the declared dependency set minus the two discussed above. All
  generic infrastructure (JIT, statistics, HTML parsing, parallelism, dataframes, GUI toolkit,
  imaging, video encoding, plotting, arrays, numerics); each would be equally at home in a web
  application or a biology pipeline. Being a dependency is not a relationship worth recording.
- **Other solar imaging-spectroscopy analysis packages** — `MCALF` (spectral-profile fitting for
  chromospheric Hα and Ca II 8542 imaging spectroscopy), `sunraster`, `irispy-lmsal` and
  `sunkit-instruments` are all genuinely similar-purpose tools, and MCALF works on the same two
  spectral lines. They were rejected because nothing in this repository, its documentation or its
  publications relates fisspy to any of them, and asserting a similarity association with no
  evidentiary basis would be curation rather than extraction. No similarity association is recorded.
  MCALF's repository (`https://github.com/ConorMacBride/mcalf`) is noted only so that this comparison
  does not have to be re-derived; it remains outside Field 29 for want of any documented relationship.
- **IDL Astronomy User's Library (`https://idlastro.gsfc.nasa.gov/`) and SolarSoft
  (`http://www.lmsal.com/solarsoft/`)** — linked from the FISS site's IDL page as prerequisites *of
  FISS-IDL*. They are not fisspy dependencies and belong, if anywhere, on FISS-IDL's own record.

### 30. Interoperable Software (OPTIONAL)

`https://github.com/astropy/astropy`

One entry. astropy is admissible here only on a cited, specific exchange rather than on dependency
presence, so the evidence is given precisely.

fisspy's **public API both consumes and returns astropy objects as its documented interchange
types** — this is not internal use:

- `fisspy.read.readbase.getHeader(file)` documents its return type as
  ``header : `astropy.io.fits.Header` `` (`fisspy/read/readbase.py:144-147`), and that object is
  exposed as a public attribute on every reader class: `FISS.header`, `raw.header`, `FD.header`,
  `calibData.header`, `MLSIpar.h`.
- Four public correction functions **accept** an astropy header as a documented parameter:
  `wvCalib(profile, h, method)`, `wvCalib_simple(h)`, `wvCalib_w_center(profile, h)` and
  `wvCalib_w_photo(profile, h)`, each documenting ``h: `~astropy.io.fits.header.Header` `` at
  `fisspy/correction/correction.py:87`, `:115`, `:139` and `:171`. A caller can therefore drive
  fisspy's wavelength calibration from a header obtained anywhere in the astropy ecosystem.
- `FD.Time` is an `astropy.time.Time` array constructed as
  `self.reftime + self.time * u.second` (`fisspy/read/read_factory.py:725`), mixing
  `astropy.time.Time` with an `astropy.units` Quantity, and `makeRasterSet` documents a
  ``time: astropy.time`` attribute (`fisspy/image/raster_set.py:185`).
- `astropy.constants` is used for the physical constants underlying the inversion's radiative
  quantities (`fisspy/inversion/_mlsi_base.py:3`, `fisspy/preprocess/proc_base.py:19`,
  `fisspy/read/read_factory.py:5`), and `astropy.utils.data.download_file` is the retrieval path in
  `fisspy/data/download.py:2` and `fisspy/data/_sample.py:4`.

The repository URL is used rather than a DOI because Field 30 explicitly permits it and it is
unambiguous.

**`sunpy` was considered and rejected**, which is the more consequential judgement here because
sunpy is prominently advertised: `README.md` lists "[sunpy](http://sunpy.org/) >=2.0.0" among the
requirement packages, `setup.py` has `sunpy>=2.0.0` in `install_requires`, and the conda-forge recipe
lists `sunpy`. The rejection rests on reading the source: **sunpy is imported exactly once in the
entire 17,153-line package** — `from sunpy.util.net import url_exists` at
`fisspy/data/_sample.py:5`, used to check that a sample-data URL exists before downloading it. There
is no `sunpy.map.Map`, no `sunpy.net.Fido`, no `sunpy.coordinates`, no `sunpy.timeseries`, no
converter to or from any sunpy type, and no documented exchange of any kind. A one-line
URL-existence helper is dependency presence, not interoperability, and "it depends on sunpy" would be
equally true of a large fraction of solar Python packages. If a future release adds a real bridge —
a `to_sunpy_map()`, a `Map`-returning raster accessor, or a Fido client for the FISS archive — sunpy
becomes a correct entry and this note should be revisited.

**Also rejected, with reasons:**

- **`numpy`, `scipy`, `matplotlib`, `pandas`** — Tier A, never listed. `pandas.DataFrame` is returned
  by `fisspy.data.search()` and would otherwise look like a documented interchange type, but pandas is
  named in Tier A precisely because "returns a DataFrame" carries no information about a package.
- **`statsmodels`, `beautifulsoup4`, `joblib`, `numba`, `Pillow`, `PyQt5`, `ffmpeg`,
  `interpolation.py`** — generic infrastructure for statistics, HTML parsing, parallelism, JIT,
  imaging, GUI, video encoding and interpolation; each would be equally at home outside science.
- **Jupyter** — the repository ships example notebooks under `docs/example/` and the conda recipe
  pulls in `ipython`, but notebooks are documentation, not a demonstrated exchange with Jupyter as a
  peer tool.
- **"It is a PyHC community package, so it interoperates with PyHC packages"** — fisspy *is* in the
  PyHC community registry (see Field 16 and Field 23), but ecosystem membership is never sufficient
  on its own and was not used as evidence for any entry.

### 31. Related Instruments (OPTIONAL)

**Fast Imaging Solar Spectrograph (FISS)**

- **Instrument Identifier:** `https://spase-metadata.org/SMWG/Instrument/BBSO/FISS.html`

Carried over from the existing HSSI record, name and identifier byte for byte. The value is genuinely
SPASE-backed — its identifier sits under `https://spase-metadata.org/`, the test that separates a real
SPASE resource from an unidentified name — and it denotes an instrument, which is what Field 31
requires.

**Relevance is beyond question.** fisspy is not merely compatible with FISS data — it is the FISS
instrument's own software. It implements the instrument's calibration pipeline, its file conventions
(`_proc`/`_c`/`_p`, `FISS_FLAT*`, `FISS_SLIT*`, `BiasDark`), its plate scale (0.16″), its two band
definitions (Hα, Ca II 8542), its grating optics (79 grooves/mm, 63.4° blaze), and the archive
packaging for its data catalogue. The package name, the repository description ("python for GST/FISS
instrument") and every module docstring say so.

**One instrument, two controlled identifiers for the same SPASE resource.** This is not an ambiguous
match between different instruments, so nothing here needs manual resolution; the controlled vocabulary
simply offers this one instrument under two identifier forms:

| name | identifier |
|---|---|
| `Fast Imaging Solar Spectrograph` | `https://spase-metadata.org/SMWG/Instrument/BBSO/FISS` |
| `Fast Imaging Solar Spectrograph (FISS)` | `https://spase-metadata.org/SMWG/Instrument/BBSO/FISS.html` (recorded) |

Both identifiers denote the same SPASE resource, differing only in the bare versus `.html` form. The
general preference is for the bare identifier, but **the submitted `.html` identifier is retained
because it denotes the same SPASE resource as the bare form, so changing it would add no metadata.**
This is a considered decision, not an oversight; a later agent should not "fix" it to the bare form.
Both alternatives are enumerated above precisely so that encountering the other form later is not
mistaken for drift.

**No other instrument is listed, and this was checked rather than assumed.** Searching the full
source and the entire `docs/` tree for other instrument and telescope names — AIA, HMI, SDO, IRIS,
Hinode, SOT, EIS, TRACE, DKIST, GONG, SOHO, SST, CRISP — produced only `GST` (three documentation
pages) and `BBSO` (one notebook and its rendered page). The single external-mission reference anywhere
in the package is an IRIS Heliophysics Coverage Registry URL in
`fisspy/image/raster_set.py:1050`, and it is demonstration data: it illustrates what an operator
would type into a catalogue record's free-text `coobs` (co-observation) field. A tutorial or
demonstration name-drop is not evidence that the software is designed to support an instrument, so
IRIS is deliberately omitted.

### 32. Related Observatories (OPTIONAL)

**Big Bear Solar Observatory (BBSO)**

- **Observatory Identifier:** `https://spase-metadata.org/SMWG/Observatory/BBSO.html`

Carried over from the existing HSSI record, name and identifier byte for byte. SPASE-backed, and it
denotes an observatory, which is what Field 32 requires.

**Relevance.** FISS is installed in the Coudé room of the 1.6 m Goode Solar Telescope at Big Bear
Solar Observatory; every data product fisspy reads originates there. The instrument paper's title
names BBSO, the SPASE identifier path is `.../Instrument/BBSO/FISS`, and BBSO is one of the two
partner institutions on the project website.

**One observatory, three controlled identifiers for the one place.** The controlled vocabulary offers
Big Bear under three identifiers:

| name | abbreviation | identifier |
|---|---|---|
| `Big Bear Solar Observatory` | `BBSO` | `https://spase-metadata.org/SMWG/Observatory/BBSO` |
| `Big Bear Solar Observatory` | — | `https://spase-metadata.org/SMWG/Observatory/Ground/BBSO` |
| `Big Bear Solar Observatory (BBSO)` | — | `https://spase-metadata.org/SMWG/Observatory/BBSO.html` (recorded) |

The third is the `.html` form of the first — the same resource — and the second is a `Ground/`-prefixed
path for the same real observatory. All three denote the one observatory, so this is not an ambiguous
match between different places and nothing here needs manual resolution. **The submitted `.html`
identifier is retained because it denotes the same SPASE resource as the bare form, so changing it
would add no metadata** — the same reasoning as in Field 31. All three alternatives are enumerated
above precisely so that encountering another form later is not mistaken for drift.

**The Goode Solar Telescope resolves to BBSO.** GST (formerly the New Solar Telescope, NST) is the
telescope FISS is mounted on, and it is named throughout the project's materials. It has **no canonical
SPASE instrument or telescope identifier** under the searched names: searching by name, abbreviation and
identifier path for `Goode`, `GST`, `NST` and `New Solar Telescope` returns no instrument or observatory
identifier for it (apparent `gst` matches such as `Wingst`, `Kingston`, `Livingston` and `Tungsten` are
substring artefacts of unrelated geomagnetic stations). Since GST is BBSO's telescope, the BBSO
observatory identifier recorded above *is* the justified observatory-level association for it. This is a
resolved association, and the absence of a GST-specific SPASE identifier is durable negative research
rather than something for a later agent to chase.

**No other observatory is listed.** The search described under Field 31 found no other observatory
or mission that fisspy is designed to support. Note in particular that the Korea Astronomy and Space
Science Institute is a FISS partner institution and co-funder of instrument operations, but it is not
an observatory whose data fisspy reads.

### 33. Logo (OPTIONAL)

**No logo. The field is deliberately left empty.**

**fisspy has no true software logo**, and this is a documented omission rather than an unfinished
search. The only logo-like asset anywhere in the repository is `logo/sun.ico` (a tracked file, last
changed by commit `ce10548`, "logo change"); the only other images in the tree are the tutorial
figures under `docs/example/img/*.png`, which are notebook output rather than branding. The project
website serves three further images — `/static/img/logo/bbso_logo.jpg`,
`/static/img/logo/kasi_logo.jpg` and `/static/img/logo/snu_logo.jpg` — and those are the partner
institutions' marks (Big Bear Solar Observatory, the Korea Astronomy and Space Science Institute,
Seoul National University). They belong to those institutions, not to fisspy, and **must never be
used as this software's logo**; doing so would misattribute the package. The PyHC registry entry for
fisspy supplies no `logo` field, unlike many of its neighbours, so PyHC offers no curated alternative
either.

**Only two candidate images exist, both `.ico` favicons rather than logos, and neither is recorded.**
A favicon is a poor fit for HSSI's presentation, and that — combined with the absence of any real
logo — is why the field is left empty rather than filled with the best available near-miss:

- `http://fiss.snu.ac.kr/static/img/FISS.ico` — **the higher-quality of the two images.** Verified
  2026-08-03: HTTP `200`, `Content-Type: image/vnd.microsoft.icon`, 15,086 bytes, **zero redirects**,
  and a valid multi-resolution Windows icon containing three images (48×48, 32×32, 16×16). It is the
  live favicon that `http://fiss.snu.ac.kr/fisspy/` itself declares via
  `<link rel="icon" href="/static/img/FISS.ico">`. It is nevertheless unusable here because the host
  is **HTTP-only** — `https://fiss.snu.ac.kr` resets the connection, as recorded in the scope notes
  at the top of this file — and HSSI is served over HTTPS, so an `http://` image URL is mixed-content
  blocked by browsers and would not render at all.
- `https://raw.githubusercontent.com/SNU-sunday/fisspy/master/logo/sun.ico` — the repository's own
  `logo/sun.ico`, served over HTTPS as `image/vnd.microsoft.icon` and therefore displayable, but only
  a single 32×32 32-bit Windows icon of 4,286 bytes, and pinned to the moving `master` ref. It is a
  favicon rather than a logo, which is why it is not recorded as this software's logo.

**A false claim about the first candidate, corrected so it is not reintroduced.** It has been
asserted of `http://fiss.snu.ac.kr/static/img/FISS.ico` that it "redirects to an HTML page rather
than serving an image". **That is false** — the URL serves the icon directly, with no redirect at
all, per the verification above. The only real objection to it is its HTTP-only scheme, and on image
quality it is in fact the better of the two candidates. Any future agent re-examining this field
should start from that corrected fact rather than the old one.

**The one condition under which this omission would change.** For the assets that exist today the
field is correctly empty, and neither `.ico` becomes acceptable through preference alone. Only the
publication of a genuine logo — a PNG or SVG served over HTTPS, or a `logo` entry in fisspy's PyHC
registry record — would supersede this, and that is worth a quick check at any later refresh. Should
the field ever be populated from the two assets described above, note that only the HTTPS
`raw.githubusercontent.com` URL could render in HSSI at all; the HTTP-only FISS.ico cannot.

---

## Additional durable notes

**PyHC registry status.** fisspy is a registered **PyHC community package**. All three registry files
were read in full: it appears in `_data/projects.yml` (not in `projects_core.yml`, not in
`projects_unevaluated.yml`) with `description: "Fast Imaging Solar Spectrograph (FISS) on the New
Solar Telescope."`, `code: "https://github.com/SNU-sunday/fisspy"`, `contact: "Juhyeong Kang"`,
`keywords: ["solar","specific"]`, and no `docs`, `url` or `logo` fields. Its curated quality ratings
are community "Requires improvement", documentation "Partially met", testing "Requires improvement",
software_maturity "Good", python3 "Good", license "Good". Two points to carry forward: the registry
description still says "New Solar Telescope", the telescope's pre-2017 name (it is now the Goode Solar
Telescope), which is why that phrasing was not adopted for Field 8; and PyHC supplies no
documentation URL or logo, so it could not resolve Fields 24 or 33.

**SoMEF output, and what of it was not used.** SoMEF v0.9.11 corroborated the repository URL,
description, license (BSD-2-Clause), creation date (2016-07-25), last update (2025-07-18), keywords
(the GitHub topics) and `full_title: FISSpy`, and — usefully — found **no** DOI and **no** citation
block, independently supporting Fields 2 and 14. Two of its outputs were rejected:
`application_domain: Semantic web` (confidence 0.81) is classifier noise with no basis in the
repository, and its `documentation` value pointed at the GitHub `docs/` source directory rather than
the rendered manual (see Field 24). Its `download_url`,
`https://github.com/SNU-sunday/fisspy/releases`, is an empty page — the repository has no releases.

**Distribution channels, for reference.** PyPI `https://pypi.org/project/fisspy/` (34 releases,
2017-02-24 to 2025-07-18) and conda-forge `https://anaconda.org/conda-forge/fisspy` (20 distinct
versions in 21 build artifacts — `0.9.70` was rebuilt, `py_0` then `py_1` — from 2019-07-01 to
2025-07-18, feedstock `conda-forge/fisspy-feedstock`, recipe maintainer `jhkang0301`).
The project's README recommends conda-forge via mamba as the primary installation route and calls pip
"not the recommended method". Neither channel is recorded in a metadata field — HSSI has no
distribution-channel field — but both were the authoritative sources for Fields 10, 12, 20 and 21.

**Dependency declarations are over-broad, which matters when reading the dependency list as
evidence.** `setup.py` `install_requires` lists thirteen packages; `numba` is never imported (it
arrives through `interpolation.py`), and `sunpy` is imported once for a single URL-checking helper.
The conda-forge recipe additionally requires `pillow` and `ipython`, which `setup.py` omits even
though `fisspy/makevideo.py:17` imports `PIL`. A future agent evaluating Fields 29 and 30 should read
the imports, not the requirement lists.
