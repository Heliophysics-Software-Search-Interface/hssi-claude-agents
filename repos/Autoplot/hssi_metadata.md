# HSSI Metadata Extraction Results

**HSSI Software ID:** 428a1d93-e1a5-407b-90a4-9bb2b85e39ec
**Repository:** https://github.com/autoplot/autoplot
**Source Revision:** f792e887adb886bb002326adc30b22c4e37b9ffc (2026-07-23, Jeremy Faden, "release notes")
**Extraction Date:** 2026-07-30
**Validation Date:** 2026-11-13
**Validation Status:** PASS

This file was seeded from the existing HSSI record, then enriched and corrected from the pinned
source revision and authoritative external sources. Autoplot's source migrated from the frozen
SourceForge Subversion trunk to the GitHub repository above in June 2025; Field 3 records the
current repository rather than the release-download page previously associated with the entry.

**Supplementary evidence base:** the `das2java` submodule (das2 graphics engine, QDataSet data
model, dasCore/dasCoreUtil/dasCoreDatum/QStream) uses an SSH URL and was inspected separately from
`https://github.com/das-developers/das2java` at the exact gitlink pinned by the source revision,
`c87f2744f783e378679e13fa04562ad5227b1300`. `https://github.com/autoplot/dev`
(demo/bug-reproduction scripts) and `https://github.com/autoplot/bookmarks` (default demo bookmark
lists) were supplementary sources only.

**Release builds bundle das2java's main branch, not the gitlink.** The `das2java` gitlink has stayed
at `c87f2744f783e378679e13fa04562ad5227b1300` (2025-06-12), and is still there at the default
branch's head `ffadec23c7c1e2d1e88c233996c16246356d4c0a` (2026-11-13), while the published releases
carry far newer das2java code: the v2026a_8 jar contains `org.das2.qds.buffer.CcsdsReader`, which
das2java added in September 2026. Evidence for what a release can do is therefore read in das2java
at the last commit before that release was built, not at the gitlink. For v2026a_8 that is das2java
`256ede719f03309bab6c19763db2595c595a5bd6` (2026-09-25), paired with Autoplot `acdaee73a`; for
v2026a_9 it is das2java `580c7d2c2c6e9190e3157ba34cafbd4f3e3c40a4` (2026-11-11), paired with
Autoplot `6455ad60e` (see Field 12). Sections that cite those revisions were read there.

All controlled-vocabulary values below were checked against the HSSI vocabulary available during
validation.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Note: this is a refresh of an existing HSSI entry; the original submitter is not identified by the view API.*

### 2. Persistent Identifier (RECOMMENDED)
Not found

*Note: Autoplot has no software DOI. Searched: no `CITATION.cff`, no `codemeta.json`, no `.zenodo.json`, no DOI badge in either `README.md` or `README.txt`; the repository has 0 git tags and no GitHub releases; DataCite and Zenodo searches for "autoplot" return only publications and presentations about the software (see Field 27), never the code itself. The reference publication DOI is recorded in Field 14, not here.*

### 3. Code Repository (MANDATORY)
https://github.com/autoplot/autoplot

**Repository correction completed 2026-07-30.** The former value,
`https://autoplot.org/latest/`, is a release-download page rather than a source repository.
Evidence for the current value:
- `https://autoplot.org/latest/` is the release download page (`Autoplot/src/index.html` is its template: single-jar, `.dmg`, `.exe`, `.deb`, `.rpm` download links). It contains no source code and is not a repository.
- `https://github.com/autoplot/autoplot` is described by its owner as "Autoplot application source code (minus Das2 stuff)", is Java, LGPL-3.0, created 2025-06-09, and has near-daily commits through 2026-07-23. It is the repository this metadata was extracted from (`git remote -v` -> `https://github.com/autoplot/autoplot.git`).
- The GitHub repository is a direct git-svn migration of the former SourceForge SVN trunk, not a
  fork; its earliest commits are literal SVN imports
  (`git-svn-id: https://svn.code.sf.net/p/autoplot/code/autoplot/trunk@2`, 2008-02-01).
- The SourceForge SVN repository is frozen: its youngest revision repo-wide is r28274, 2025-06-04 — five days before the GitHub repository was created. `README.txt` (the legacy SVN readme, still in the tree) still points at SVN; `README.md` (the current readme) documents the GitHub clone procedure instead.

### 4. Software Functionality (MANDATORY)

The final set contains 22 values. Every value is backed by named code/module evidence, and every
child is accompanied by its parent.

- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Packet Decommutation
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Data Visualization: Movies
- Data Visualization: Orbit Plots
- Data Visualization: Spectrogram
- Data Visualization: Web-Based
- Servers and Environments
- Servers and Environments: Data servers processing and handling
- Servers and Environments: Distribution/Access

**Evidence per value**

*Path convention: evidence paths are relative to the Field 3 repository unless prefixed `das2java:`, which marks code that lives in the das2java submodule (Field 29/30). das2java compiles into `autoplot.jar` and ships as part of the delivered application, so the capability is Autoplot's; the prefix exists so a reviewer grepping only the Autoplot repository is not misled.*

- **Data Processing and Analysis** — parent of all children below.
- **: 2D Slices** — `das2java:Ops.slice0/slice1/slice2/slice3`, `Ops.slices`, `Ops.collapse0..collapse3`, the `das2java:Slice0DataSet`–`Slice3DataSet` classes, `das2java:org.das2.qds.filters.SliceFilterEditorPanel`/`SlicesFilterEditorPanel`/`CollapseFilterEditorPanel`; interactive `das2java:VerticalSlicerMouseModule` and `HorizontalSlicerMouseModule` extract 1-D cross-sections from rank-2 spectrograms.
- **: Analysis** — the `das2java:org.das2.qds.ops.Ops` statistical and derived-quantity library (`mean`, `median`, `stddev`, `variance`, `mode`, `meanAverageDeviation`, `extent`, `cumulativeMax/Min`, `diff`, `accum`, `total`, `where`); `CdfJavaDataSource/src/org/autoplot/cdf/CdfVirtualVars.java` reimplements CDAWeb/ISTP virtual variables in QDataSet, computing derived physical quantities (`calc_p` = solar-wind dynamic pressure `1.6726e-6 * np * Vp**2`, `compute_magnitude`, `convert_log10`, `sum_values`) and applying instrument quality flags (`apply_qflag`, `apply_esa_qflag`, `apply_filter_flag`, `region_filt`); event-list algebra (`das2java:Ops.eventsCoalesce/eventsComplement/eventsConjunction/eventsDiff/createEvents`); `das2java:CutoffMouseModule` for cutoff analysis.
- **: Data Access and Retrieval** — URI-driven remote access is the software's central capability. Dedicated modules `CDAWebDataSource`, `HapiDataSource`, `Das2ServerDataSource`, `FedCatDataSource` (federated das2 catalog), `OpenDapDataSource`, `TsdsDataSource`, `PDSPPIDataSource`; virtual filesystems `org/autoplot/wgetfs` (HTTP/HTTPS), `DataSource/src/ftpfs` and bundled ftp4j (FTP/FTPS), `DataSource/src/zipfs`; `DataSetURI.getFile`/`downloadResourceAsTempFile` with local caching; `org/autoplot/aggregator` aggregates many remote files into one dataset via `$Y$m$d` URI templates and wildcards.
- **: Data Reduction** — `das2java:Ops.decimate`, `reducex`-family (`reduceMean/reduceMax/reduceMin/reduceMedian/reduceSum`, `reduceBins`), `binData`, `histogram`, `histogram2d`, `autoHistogram`, `das2java:org.das2.qds.util.BinAverage`; filter editors `das2java:ReducexFilterEditorPanel`, `BinAverage2dFilterEditorPanel`, `HistogramFilterEditorPanel`, `Histogram2dFilterEditorPanel`; render-time reduction to one bin per pixel column, with the v2026a_6 release note "Keep track of data reduction and render error bars to show extent of the data in each pixel column."; largest-triangle-three-buckets downsampling (`das2java:org.das2.qds.util.LttbDownsampler`, with `LttbFilterEditorPanel`), read at das2java `580c7d2c2`.
- **: File Format Conversion** — the QDataSet model decouples readers from writers, so any readable dataset can be re-emitted in another format. Registered `DataSourceFormat` writers (`META-INF/org.autoplot.datasource.DataSourceFormat.extensions`): ASCII tables, CSV, CDF, HDF5/netCDF4, IDLSave, MATLAB `.mat`, Excel `.xls`, WAV, das2 stream `.d2s`, QStream `.qds`, HTML tables, raw binary, PNG/JPG/GIF, HAPI. Driven by `ExportDataPanel`/`ExportDataFormatPanel` in the GUI, `AutoplotDataServer` from the command line, and `AutoplotServlet`'s `DataServlet` ("Data Servlet sends data for URI in requested form", `web.xml`).
- **: Image Processing** — `ImageDataSource/src/org/autoplot/imagedatasource/ImageDataSource.java` reads PNG/JPG/GIF into rank-2/rank-3 datasets and applies a `ConvolveOp` with an explicit blur `Kernel` (line 236) and `AffineTransform` rotation (lines 193–195), and extracts EXIF and GPS metadata (`ExifSubIFDDirectory`, `GpsDirectory`); `org/autoplot/pngwalk` supplies `ScalePerspectiveImageOp`, `ImageResize`, `RichPngUtil`, and `ClickDigitizer` (digitizing values off rendered images); `das2java:org.imgscalr.Scalr` in dasCoreUtil.
- **: Processing** — the chained filter/operations pipeline: `das2java:org.das2.qds.OperationsProcessor` plus ~40 filter editors in `das2java:org.das2.qds.filters` (detrend, butterworth, median, normalize, cleanData, expandToFillGaps, dbAboveBackgroundDim1, contour, rebundle, applyIndex, exponent, pow, add/divide/multiply, get/putProperty, setUnits, setDepend0Cadence/setDepend1Cadence/setDepend0Units), surfaced in the GUI through `Autoplot/src/org/autoplot/OperationsPanel.java` and appendable directly to a URI.
- **: Spectrogram** *(computation)* — `das2java:Ops.fft`, `ifft`, `fftPower`, `fftPowerMultiThread`, `fftPowerSpectrum`, `fftPowerSpectralDensity`, `fftLinearSpectrum`, `fftLinearSpectralDensity`, `fftFilter`, `fftWindow`, `hanning`, `windowFunction`, `hilbert`, `hilbertSciPy`, `chirp`, plus `das2java:org.das2.qds.math.fft`; filter editors `das2java:FftPowerFilterEditorPanel`, `FftOutputsFilterEditorPanel`, `HanningFilterEditorPanel`; CDAWeb virtual variables `fftPower512`, `fftPower1024`, `fftpowerdelta512/1024/2048`; regression tests `VATesting/src/org/autoplot/test/Test_050_FftFilter.java`, `Test_054_FftFilter.java`, `Test_051_HanningFilter.java`. `das2java:Ops.totalSpectralPower`, added in the v2026a_9 release ("New totalSpectralPower function added, showing total power in waveform components.") and read at das2java `580c7d2c2`, computes the power spectrum of each component of a three-component vector with `fftPower` and sums them, `Ptotal(f) = Px(f) + Py(f) + Pz(f)`.
- **: Time Series Analysis** — the `TimeSeriesBrowse` capability (`DataSource/src/org/autoplot/datasource/capability/`) re-reads data as the time axis is panned or zoomed, which is the application's defining interaction; `das2java:Ops.detrend`, `detrend1`, `butterworth`, `medianFilter`, `smooth`, `smooth1`, `smooth2d`, `smoothFit`, `timeShift`, `sortInTime`, `synchronize`, `synchronizeNN`, `ensureMonotonic`, `identifyContinuousBlocks`, `expandToFillGaps`, `timegen`; `org/autoplot/aggregator` builds a single continuous time series from a directory of per-day files.
- **: Packet Decommutation** — added with the v2026a_8 release, read at Autoplot `acdaee73a` and das2java `256ede719` (see Field 12). `das2java:org.das2.qds.buffer.CcsdsReader` ("Utility class for reading CCSDS telemetry streams") walks a CCSDS space-packet stream header by header, decoding each packet's APID, sequence count and data length and handing each packet to the handler registered for its APID. `BinaryDataSource/src/org/autoplot/binarydatasource/BinaryDataSource.java` (lines 182–210) exposes it as the `ccsds=<packetId>` URI parameter, in decimal or `0x` hex, extracting one packet type from the stream and failing with "No ccsds records with packetId=… found" when none match; its new `mask=` and `bitField=` parameters (lines 353–363) AND out individual bit fields of the decoded words and shift them right. `BinaryDataSourceFactory.java` completes `ccsds=` with the APIDs actually present in the file. The release page lists the feature as "Experimental ccsds switch to the BinaryDataSource, to parse simple ccsds files." and "BinaryDataSource can have hex values for offsets, like 0x1A, and new mask and bitField controls extract individual bits." The release's `autoplot.jar` carries the `ccsds=`, `mask=` and `bitField=` parameters in its `BinaryDataSource` classes. "Experimental" does not change the classification: the switch ships in the released application and is offered to users. It is generic CCSDS support for any packet stream, not part of a mission's ground system, so `Mission-related: Packet Decommutation` does not apply (rule 8). The v2026a_9 release adds the `ccsdsOffsetCorrection=` parameter (Autoplot `8eb726c99`, read at `6455ad60e`; completion text "CCSDS correction to incorrect packet lengths found in file"), so streams whose packets record wrong lengths can still be parsed.

- **Data Visualization** — retained from HSSI; parent of all children below.
- **: 2D Graphics** — `das2java:` dasCore renderers `SpectrogramRenderer`, `RGBImageRenderer`, `ContoursRenderer`, `ColorSeriesRenderer`, `PolarPlotRenderer`, `PitchAngleDistributionRenderer`, `PolyMeshRenderer`, `BoundsRenderer`, `HugeScatterRenderer`, with `das2java:DasColorBar`; `RenderType` enum values `spectrogram`, `nnSpectrogram`, `image`, `contour`, `colorScatter`, `polar`, `vectorPlot`, `bounds`, `hugeScatter`, `pitchAngleDistribution`, `stackedHistogram`, and matching style panels in `Autoplot/src/org/autoplot/renderer/`.
- **: 2D Slices** — `das2java:VerticalSliceSelectionRenderer` and `HorizontalSliceSelectionRenderer` draw the selected slice on the plot while `das2java:VerticalSlicerMouseModule`/`HorizontalSlicerMouseModule` open the resulting 1-D cut in its own plot; `das2java:CollapseSpectrogramRenderer` displays a collapsed dimension alongside the spectrogram.
- **: Line Plots** — `das2java:SeriesRenderer`, `PlotSymbolRenderer`, `CurveRenderer`, `DigitalRenderer`, `StackedHistogramRenderer`, `ErrorBarType`, `PsymConnector`; `RenderType` values `series`, `scatter`, `stairSteps`, `fillToZero`, `digital`, `eventsBar`; `SeriesStylePanel`, `DigitalStylePanel`, `EventsStylePanel`.
- **: Movies** — `Autoplot/src/org/autoplot/pngwalk/PngWalkTool.java` exposes a "Write to Animated GIF..." menu item and `writeAnimatedGif()`/`writeToAnimatedGifImmediately()` with per-frame delays, delegating to `external/AnimatedGifDemo.saveAnimate`, and also emits an `ffmpeg -i ...` command for video encoding; the pngwalk coverflow (`CoversWalkView`), grid, row, and timeline views animate long image sequences.
- **: Orbit Plots** — `RenderType.orbitPlot` with `Autoplot/src/org/autoplot/renderer/OrbitStylePanel.java`; `DataSourcePack/src/org/autoplot/orbit/OrbitDataSourceFactory` registers the `orbit` extension for orbit/ephemeris tables; `Autoplot/src/org/autoplot/tca/` (`DataSourceTcaSource`, `UriTcaSource`, `demoTca.jy`) annotates the time axis with ephemeris parameters; `das2java:ColumnColumnConnector`.
- **: Spectrogram** *(display)* — `das2java:SpectrogramRenderer`, `SpectrogramStylePanel` (Autoplot), `das2java:StackedHistogramRenderer`/`StackedHistogramStylePanel` (Autoplot), `das2java:CollapseSpectrogramRenderer`, `das2java:DasZAxisPlot`, `das2java:DasColorBar`; `RenderType` values `spectrogram`, `nnSpectrogram`, `stackedHistogram`.
- **: Web-Based** — `AutoplotServlet` is a deployable J2EE web application whose `web.xml` states "Provides server-side graphics and other facilities." It ships JSP pages (`index.jsp`, `simple.jsp`, `script.jsp`, `dataServer.jsp`, `CdawebVapServlet.jsp`, `URI_Templates.jsp`), HTML forms with URI completions (`completions.html`, backed by `CompletionsServlet`), a JavaScript thin client for interactive crosshair readout and time-axis zoom over server-rendered plots (`AutoplotServlet/web/thin/crosshair/`, `AutoplotServlet/web/thin/zoom/`, `util.js`, `sprintf.js`, `TimeUtil.js`, `TimeRangeParser.js`), and `ScriptGUIServlet`, which emits a complete interactive HTML form (`<form action='ScriptGUIServlet'>` with checkboxes, text inputs, and `<datalist>` examples) that runs Autoplot scripts and returns generated graphics to the browser. `AutoplotServer` is documented as "Server for producing images from Autoplot URIs". `PngWalkTool`'s `HtmlOutputOptions` and `makeTutorialHtml.jy` emit browsable HTML image galleries.

- **Servers and Environments** — parent of the two children below.
- **: Data servers processing and handling** — `HapiServerDemo` is a working HAPI server implementation (`CapabilitiesServlet`, `CatalogServlet`, `InfoServlet`, `DataServlet`, `AboutServlet`, `HapiServerSupport`, `CsvDataFormatter`, `BinaryDataFormatter`, `GZIPFilter`); `AutoplotServlet`'s `DataServlet` serves data for a URI in a requested form; `Autoplot/src/org/autoplot/AutoplotDataServer.java` streams data for a URI from the command line; `Autoplot/src/org/autoplot/server/RequestHandler.java` and `RequestListener.java` accept commands on a socket.
- **: Distribution/Access** — the servlet stack distributes both data and rendered graphics over HTTP; `URITemplatesServlet` and `UnaggregrateServlet` distribute URI-template services, and `HapiDataSourceFormat` writes a HAPI-servable directory (`info/<id>.json`, `capabilities.json`, CSV data) so an Autoplot user can publish a dataset as a HAPI service. `JnlpServlet`, which generates Java Web Start launch files for the application, is still in the servlet but no longer counts toward this value: the project has dropped JNLP (`24ab4719d`, 2026-11-02: "remove old JNLP file, since JNLP is no longer supported.").

**Considered and deliberately excluded** (recorded so the omissions are auditable):

- **Coordinate Transforms (and all six children)** — Autoplot is reference-frame agnostic. `das2java:Ops` provides only generic vector math (`polarToCartesian`, `matrixFromEuler`, `matrixMultiply`, `matrixParse`, `crossProduct`, `toDegrees`, `toRadians`, `magnitude`) with no named heliophysics frames. The one frame-conversion hook in the codebase, the CDAWeb `conv_pos1` (`ANG-GSE`) virtual variable, is explicitly `throw new IllegalArgumentException("not implemented")` in `CdfVirtualVars.convPos`. Occurrences of `GSE`/`GSM` in the tree are variable names and javadoc, not transforms: `CdfVirtualVars.java` (`"ANG-GSE"` at line 105 — the argument to the unimplemented `convPos`; `V_GSE_p` at lines 328–336, a parameter name in `calcP`), `CdfJavaDataSourceEditorPanel.java`, `PlotElementController.java`, and the `Autoplot/src/test/endtoend/` tests. (`IstpMetadataModel.java` contains no `GSE`/`GSM` occurrence at all.) No AACGM, no SPICE, no IGRF, no MLT, no field-line or magnetic-coordinate code.
- **Mission-related (and all children)** — Autoplot is not part of any mission ground system. Every mission name in the tree (Juno, Voyager, Galileo, Cassini, MAVEN, RBSP, GOES, Polar) occurs only in javadoc example URIs, `main()` test harnesses, or the application's default demo bookmark lists (which live in the separate `autoplot/bookmarks` repository). There is no mission-specific reader, calibration, packet decommutation, or pipeline code.
- **Models and Simulations (and all children)** — `das2java:org.das2.qds.demos.PlasmaModel` and the `das2java:Ops.ripples*`, `chirp`, `sawtooth`, `randn`, `randomu`, `ripplesPitchAngleDistribution` functions generate synthetic data for demos and tests, not physical models. No solver, no empirical model, no forecast output.
- **Data Processing and Analysis: Pitch Angle Distributions** — Autoplot *renders* pitch angle distributions (`das2java:PitchAngleDistributionRenderer` wraps a spectrogram around an origin, with a `mirror` control; `PitchAngleDistributionStylePanel` in Autoplot; the `angleDistribution` scheme in `das2java:org.das2.qds.examples.Schemes`) but does not *compute* them from particle data, which is this subcategory's definition. There is no `Data Visualization: Pitch Angle Distributions` child to hold the rendering capability, so the concept is carried in Keywords (Field 16) instead.
- **Data Processing and Analysis: Plasma Moments** — `CdfVirtualVars.calcP` computes solar-wind dynamic pressure from an already-derived density and bulk velocity (`1.6726e-6 * np * Vp**2`), not moments integrated from a distribution function. Counted under `: Analysis` instead.
- **Data Processing and Analysis: Energy Spectra** — Autoplot slices and renders energy-time spectrograms with generic rank-2 machinery; the energy-aware code (`apply_qflag`'s `flux_h`/`flux_o`/`flux_he_1`/`flux_he_2` channel mapping) applies quality flags rather than computing or analysing spectra. Excluded as not evidenced.
- **Data Processing and Analysis: Calibration** — applying instrument quality flags (`apply_qflag`, `apply_esa_qflag`) is not conversion of raw counts to physical units. No calibration files, response functions, or gain corrections in the tree.
- **Data Processing and Analysis: Wavelet Analysis** — no wavelet code anywhere in Autoplot or das2java (searched).
- **Data Processing and Analysis: Wave Polarization Analysis, Curlometer, Linear Gradient Estimation, Magnetic Null Finding, 3D Particle Distribution Processing, Field-line Tracing, Data Assimilation, ML/AI** — no supporting code found for any of these. (`Packet Decommutation` stood in this list until the v2026a_8 release added CCSDS packet parsing; see above.) `das2java:Ops.totalSpectralPower` (v2026a_9) takes three-component vectors but only sums their power spectra; it computes no polarization, ellipticity or coherence quantity. The "ChatGPT" mentions in the tree and its commit messages credit a coding assistant used to write code (the new PDS4 reader, for one); the software itself contains no ML/AI.
- **Data Visualization: 3D Graphics** — no 3D rendering. No JOGL/OpenGL/VTK/jzy3d; `das2java:PolyMeshRenderer` draws a 2-D polygon mesh. Search hits for "3D" are array-rank comments.
- **Data Visualization: Hodograms** — component-vs-component plots are achievable with the generic `xyScatter` scheme but there is no hodogram feature, renderer, or style panel.
- **Data Visualization: ML/AI, Mission-Specific, Spacecraft Formation Plots** — no supporting code.
- **The Jython script debugger** added in v2026a_9 (breakpoints, conditional breakpoints, stepping and tracing in the script editor; `JythonSupport/src/org/autoplot/jythonsupport/ui/JythonDebugger.java`, read at `6455ad60e`) is a scripting-environment tool with no row in the taxonomy; scripting is carried by Fields 8 and 16.
- **Servers and Environments: Software or Environment Container** — no Dockerfile, no Singularity/Apptainer definition, no container manifest in the repository.
- **Servers and Environments: High Performance Computing, Infrastructure as Code** — `das2java:Ops.fftPowerMultiThread` and `das2java:OpsParl` use a local `java.util.concurrent` thread pool; that is desktop multithreading, not HPC. No MPI, no batch scheduler scripts, no Kubernetes/Terraform manifests.

### 5. Related Region (MANDATORY)
- Earth Magnetosphere
- Earth Inner Magnetosphere
- Planetary Magnetospheres
- Jupiter Magnetosphere
- Saturn Magnetosphere
- Solar Wind

**Evidence.** `Earth Magnetosphere` is retained from HSSI and is independently supported by the CDF/CDAWeb/ISTP stack (`CdfJavaDataSource`, `CDAWebDataSource`, `DataSource/src/org/autoplot/metatree/IstpMetadataModel.java`), whose dataset population is predominantly Earth's magnetosphere. `Earth Inner Magnetosphere` is supported by the software's own description, which names RBSP-ECT as a contributing project, and by the RBSP/EMFISIS URIs used as canonical examples in `AutoplotServlet/web/completions.html`. `Planetary Magnetospheres` is supported by the dedicated `PDSPPIDataSource` module, which is a client for the NASA PDS Planetary Plasma Interactions node (`https://pds-ppi.igpp.ucla.edu/`, `ditdos/inventory?sc=...`) — named in the description as a contributing project. `Jupiter Magnetosphere` is supported by `Das2ServerDataSource`'s Juno/JED dataset handling (`Das2ServerDataSourceEditorPanel.getDataSetId` documents `Juno/JED/ElectronSpectra` at `jupiter.physics.uiowa.edu`), by the v2026a_6 release note fixing the fill value used for times in JUNO/JADE PDS3, and by the v2026a_5 note about a flipped Jupiter image. `Saturn Magnetosphere` is supported by `PDSPPIDataSource`'s own documented URIs for Cassini MIMI/LEMMS and CAPS datasets (`PDSPPIDB.java`, `PDSPPIFileSystem.java`). `Solar Wind` is supported by `CdfVirtualVars.calcP` (solar-wind dynamic pressure from `V_GSE_p` and `np`) and `region_filt` (which masks to `1=solar wind`).

*Note (considered, not asserted): `Mars Magnetosphere` rests only on a MAVEN PDS4 entry in the separate `autoplot/bookmarks` demo list, and `Earth Ionosphere`, `Interplanetary Space`, and `Solar Environment` have no module- or code-level evidence in this repository, only demo bookmarks. Autoplot is genuinely region-agnostic — a general data browser — so this field is intentionally limited to regions with concrete in-repo evidence rather than expanded to cover everything a user might plot.*

### 6. Authors (MANDATORY)

**Criterion:** the identity-aware union of the prior HSSI authors, the project's own in-application
contributors/credits page, and the reference publication's author list.

Source (b) is `Autoplot/src/org/autoplot/aboutAutoplot.html`, whose list at line 11 is headed `<p>Contributors:</p>` and closes "and feedback from many more" — so it is a credits page, not a formal authorship statement, and is treated as such. It is nonetheless the project's own attribution of who designed and wrote the software, with affiliations, and its six names are a superset of the reference publication's four. Matching is identity-aware (ORCID first, then normalised name); no existing HSSI entry is dropped except where the user has explicitly decided otherwise (see Author 7, below).

**Author 1 — Jeremy Faden** *(existing HSSI author, unchanged)*
- **Author Identifier:** https://orcid.org/0000-0003-2397-488X
- **Affiliation:**
  - Cottage Systems — https://ror.org/01sqsqt89
  - University of Iowa — https://ror.org/036jqmy94
- *Source: existing HSSI record. Corroborated by `aboutAutoplot.html` ("Jeremy Faden, Cottage Systems, Software and Design"), by 25,978 of the repository's commits (`jbfaden`, `Jeremy Faden <faden@cottagesystems.com>`, `jbf <jeremy-faden@uiowa.edu>`), by 687 `@author jbf` javadoc tags (an `@author` token equal to `jbf`, any whitespace; excludes the variants `jbf,cwp` ×2 and `jbf@iowa.uiowa.edu` ×2) — by a wide margin the most common `@author` token in the tree, ahead of `nand` at 43 — and by the ORCID record, whose employments are Cottage Systems and The University of Iowa (Department of Physics and Astronomy).*

**Author 2 — Robert S. Weigel** *(new)*
- **Author Identifier:** https://orcid.org/0000-0002-9521-5228
- **Affiliation:**
  - George Mason University — https://ror.org/02jqj7156
- *Source: `aboutAutoplot.html` ("Robert S. Weigel, George Mason University, Design"); second author of the reference publication (Field 14); 14 commits in the repository as `rweigel`. ORCID employment is George Mason University, Physics and Astronomy.*
- The ORCID and George Mason University affiliation disambiguate this identity from an
  identifier-less namesake in HSSI.

**Author 3 — Reinhard Friedel** *(new)*
- **Author Identifier:** https://orcid.org/0000-0002-5228-0281
- **Affiliation:**
  - Los Alamos National Laboratory — https://ror.org/01e41cf67
- *Source: `aboutAutoplot.html` ("Reiner Friedel, Los Alamos National Labs, Design"); fourth author
  of the reference publication as "R. H. W. Friedel". The ORCID record's primary name is
  "Reinhard Friedel", with the other-name "Reiner" and employment at Los Alamos National
  Laboratory, confirming the identity and the form used here.*

**Author 4 — Jan Merka** *(new)*
- **Author Identifier:** https://orcid.org/0000-0002-0231-026X
- **Affiliation:**
  - University of Maryland, Baltimore County — https://ror.org/02qskvh78
  - Goddard Space Flight Center — https://ror.org/0171mag52
- *Source: `aboutAutoplot.html` ("Jan Merka, University of Maryland Baltimore County and NASA/GSFC,
  Design"); third author of the reference publication. ORCID employment is University of
  Maryland, Baltimore County (ROR-disambiguated to `https://ror.org/02qskvh78`); both affiliations
  use the canonical identities shown above.*

**Author 5 — Edward Jackson** *(new)*
- **Author Identifier:** Not found
- **Affiliation:**
  - Cottage Systems — https://ror.org/01sqsqt89
- *Source: `aboutAutoplot.html` ("Edward Jackson, Cottage Systems, Software and Design"). Corroborated by 63 commits as `edjackson` and by 11 `@author Ed Jackson` javadoc tags on files he wrote (the whole of `DataSource/src/zipfs/` — `ZipFileSystem.java`, `ZipFileObject.java`, `ZipFileSystemFactory.java` — and most of `Autoplot/src/org/autoplot/pngwalk/`, including `PngWalkView.java`, `WalkImage.java`, and `QualityControlRecord.java`). He also appears as the short tag `@author ed`, e.g. `AutoplotHelp/src/org/autoplot/help/AutoplotHelpSystem.java:30`. No ORCID could be confidently matched — "Edward Jackson" is too common to disambiguate without a corroborating affiliation in ORCID, so none is asserted.*

**Author 6 — Edward West** *(new)*
- **Author Identifier:** Not found
- **Affiliation:**
  - University of Iowa — https://ror.org/036jqmy94
- *Source: `aboutAutoplot.html` ("Edward West, University of Iowa, Java Consultation").
  Corroborated by 3 commits as `eewest` and `@author eew` tags on
  `JythonSupport/src/org/autoplot/jythonsupport/FunctionSupport.java` and
  `Autoplot/src/external/FunctionSupport.java`. No ORCID could be confidently matched. The HSSI
  person named Matthew West is a different person.*

**Completed correction (2026-07-30):** the prior entry also listed
`"the Autoplot development"` / `"team"` as a seventh author. This was a sentence fragment split
across person-name fields, not a person or organization, and its association was removed. No
organization substitutes for it: Cottage Systems is already represented as Jeremy Faden's
affiliation.

**Field 6 therefore contains 6 authors.**

*Note on additional code contributors, considered and not listed: the repository has substantial commit counts from `aizuchi` (50), `pikerc` / Chris Piker (50, U. Iowa, `@author cwp` on the `FedCatDataSource` das2 catalog code), `mmclouth` (66), `aluthens` / Armond Luthens (18), `jpeachey` (14), `jdv227` (13), `dlindholm` (6), and others. They are real contributors but appear on neither the project's own contributors/credits page nor the reference publication, which are the two sources this field's criterion unions, so they are not asserted here. Names appearing in `@author` tags on bundled third-party source (Carlo Pelliccia/ftp4j, Miloslav Metelka and Dusan Balek/NetBeans editor, P. Grosbol/ESO FITS, Wojciech Gradkowski, Apache Software Foundation, `nand`/NASA GSFC CDFJ) are vendored-library authors, not Autoplot authors.*

### 7. Software Name (MANDATORY)
Autoplot

*Source: existing HSSI record, unchanged. Confirmed by `README.md` ("# Introduction to Autoplot"), `aboutAutoplot.html`, the release page title "Autoplot Application (v2026a_9)", and the repository name.*

### 8. Description (MANDATORY)

**Paragraphs 1–2 are the existing HSSI description, retained byte-for-byte.** They are the project's own wording — verbatim the "About" section of `https://autoplot.org` as it still reads on 2026-07-30 — so they are preserved rather than rephrased.

**Paragraphs 3–4 were added during the 2026-07-30 refresh** to remedy a material omission: the prior description said what Autoplot is but nothing about what it reads, computes, plots, or writes, which is the information a potential user needs. The added text is drawn from `https://autoplot.org`'s own "Key Features" list and from the module evidence cited in Field 4. Nothing in the original two paragraphs was reworded or removed.

```
Autoplot is an interactive browser for data on the web; give it a URL or the name of a file on your computer and it tries to create a sensible plot of the contents in the file. Autoplot was developed to allow quick and interactive browsing of data and metadata files that are often encountered on the web. For more information, see Faden et al. 2010 and introductory PowerPoint.

Autoplot was developed under the NASA Virtual Observatories for Heliophysics program in a collaborative effort among several institutions, including support or code contributions from PDS-PPI Node, RBSP-ECT, and the Radio and Plasma Wave Group at The University of Iowa.

Datasets are identified by compact URIs, and by the URI's extension data are loaded into one uniform data model (QDataSet), so the same plots, operations, and scripts apply regardless of the source. Autoplot reads complex ASCII and CSV tables, binary tables, CDF (including the ISTP/CDAWeb virtual variables), netCDF and NcML, HDF5, FITS, PDS3 and PDS4 labels, Cluster Exchange Format, Excel spreadsheets, IDLSave and MATLAB files, WAV audio, images, SPASE records, and das2 and QStream streams; it accesses remote data from CDAWeb, HAPI servers, das2 servers and federated das2 catalogs, PDS-PPI, OpenDAP, TSDS, and ordinary HTTP/HTTPS and FTP directories, and wildcards and $Y$m$d templates aggregate many files into one time series.

Data are drawn as line and scatter plots, spectrograms, stacked histograms, contours, images, polar and pitch-angle-distribution plots, orbit plots, and event bars, with interactive axes, mouse slicing of spectrograms, and export to PNG, PDF, SVG, and animated GIF. A chained operations library supplies slicing, FFT power spectra, windowing, Butterworth and median filtering, detrending, smoothing, histograms, and bin-average and other data reduction, and any displayed dataset can be written back out as ASCII, CSV, CDF, HDF5, netCDF, IDLSave, MATLAB, Excel, WAV, or das2/QStream. Jython scripting, a data-access bridge usable from IDL, MATLAB, and Python, and a servlet providing server-side graphics and a HAPI service extend Autoplot beyond the desktop application.
```

### 9. Concise Description (OPTIONAL)
Interactive Java application that browses scientific data on the web: give it a URL or a filename and it reads one of many formats and produces a sensible, interactive plot.

*Added during the 2026-07-30 refresh. 173 characters, within the 200-character limit. Derived from `README.md` and `aboutAutoplot.html`. The first 174 characters of the full description were already a serviceable preview, so this field is a refinement rather than a fix; it adds only the facts that the application is written in Java and reads many formats.*

### 10. Publication Date (RECOMMENDED)
2008-02-01

*Added during the 2026-07-30 refresh. Date of the first public release of the source code: SourceForge SVN r1, "home for autoplot and autoplot plugins", 2008-02-01 05:26:45 -0700, confirmed both by `svn log -r 1 https://svn.code.sf.net/p/autoplot/code` and by the migrated git history (earliest commit 2008-02-01, `git-svn-id: .../trunk@2`). Note two caveats recorded rather than guessed at: the r5 commit message says "import into source forge SVN, private CVS with prior history exists," and Jeremy Faden's 2025 poster (Field 27) states Autoplot was "introduced in 2007" — so development predates this date, but 2008-02-01 is the earliest date with public, verifiable evidence. The reference publication appeared later, 2010-04-25.*

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

*With no DOI obtained, the repository host is the appropriate publisher. Alternative considered:
`Cottage Systems` (`https://ror.org/01sqsqt89`), since `https://autoplot.org` states "Autoplot is
maintained by Cottage Systems" and distributes the binaries; the field definition instead calls
for the repository host.*

### 12. Version (RECOMMENDED)
- **Version Number:** v2026a_9
- **Version Date:** 2026-11-12
- **Version Description:** the v2026a_9 release's own notes, trimmed as described below:

```
Bugfixes (2026-11-11):
- TimeUtil.next(SECOND,t) didn't increment property.
- new code in restoreState assumed that the "deltas" was non-null, breaking the "vapfile:" prefix.
- Slice filter dialog properly enables the datum field.
- 2916: Sequence to loose work in editor fixed.
- 2918: ASCII file with start, stop times is treated as events list.
- 2917: Windows would grow each time a dialog was opened and closed. Thanks, Dave!
- Improve formatting of DatumRanges, using the same DatumFormatter on min and max and using new improved code to pick the formatter.
- "Save As" dialog is sized properly. Thanks, Ivar!
- Delay resolution of macros like %{RANGE} until necessary.
- More tweaks to HAPI dataset filter, after noticing it still is doing things with each keystroke.
- Some overly verbose logging with --script argument quieted.
- "slices" function explicitly checks for ":" so that one doesn't assume "10:20" would be acceptable. Thanks, Dave!
- 2913: TimeRangeDialog and others are resizeable.
- 2906: Embed data in .vap works with orbit datum ranges with local file references. Thanks, Dave!
- 2882: ASCII data source also kept state which caused runtime error on reload.
- splitAnchorType with verticalAnchorType=PLOT was incorrectly implemented, locating the plot as if it were "DATA".
- 2903: delim-based ASCII parser will always skip empty lines. Thanks Darrelle!
- Das2 PropertyEditor doesn't show the button for the custom property editor if it is the (useless) default editor.
- Support Rank 3 data in Export All Data. Don't assume data has timetags. Thanks, Ivar!
- 192:: synchronizeNN had incorrect test on "close" point, resulting in fill value when NN was possible. Thanks, Darrelle!
- 2901: Revert change which broke UIowa digitizing script.
- 2900: Clean up event handling in HAPI Data Source Editor, correct recents.

Features:
- Slice filter dialog supports mouse wheel events on the time, incrementing or decrementing the component.
- 893: Jython debugger is used to implement trace when running scripts (ctrl+Run).
- 893: Jython editor double-click is Jython-aware and is more likely to select useful fragments.
- 893: new Jython debugger enabled with environment variable "jythonDebugger=true"
- 892: floating stdout bubbles in Jython editor.
- New totalSpectralPower function added, showing total power in waveform components. Thanks, Dave and George!
- 889: CDAWeb, HapiDataSource now uses simple filter strings, like "rbsp AND density NOT source".
- 890: New PDS4 reader supports Java 8 and will be maintained within Autoplot.
- Huge Scatter performance gain with 126M-point dataset, from 2800ms -> 500ms per draw, by using addValue to increment count and removing loop invariants.
- Kludgy unit "rgbColor" detected now and colorbar is turned off.
- 888: support rank 3 and rank 4 data in .mat files. Thanks, Ivar!
- 2901: New code for simplifyScriptToGetParams operates on the AST, not the source, so is more reliable.
- 2902: HAPI JSON read capability is available in the GUI.
```

- **Version PID:** Not found

**Where Autoplot publishes releases.** Autoplot has no git tags, no GitHub releases and no Maven or
PyPI distribution of the application; the repository's GitHub releases and tags pages still list none
on 2026-11-13. It publishes each release as a directory of the release archive
`https://autoplot.org/jnlp/`, named `v<year><series>_<n>` (`v2026a_1` … `v2026a_9`), holding
`autoplot.jar` and a release page whose notes are the release body. The archive's `latest/` entry is
the production release page, and the Install4J installers it links (`autoplot_windows-x64_2026_09.exe`,
`autoplot_macos_2026_09.dmg`, `.deb`, `.rpm`) are named for the same release. The dated directories
(for example `20260926a` and `20261111b`) are development builds; the archive's `devel/` entry points
at the newest of them. They are not releases (Field 12 rule 2), which is why this field records the
newest `v2026a_n` directory. The PyPI project `autoplot` (0.9.5, uploaded 2026-11-09) is the separate
`autoplot/python` bridge (Field 30), not this application, so its versions are not Autoplot's.

**Why v2026a_9.** `v2026a_9` (archive entry 2026-11-12) was published after `v2026a_8` (2026-09-28),
which HSSI held until this update; `v2026a_9` is the newest release and is what
`https://autoplot.org/latest/` serves ("Autoplot Application (v2026a_9)", byte-identical to
`https://autoplot.org/jnlp/v2026a_9/`). The release is on the v2026a production series ("This is the
Autoplot v2026a branch. This is an update to the production version containing bugfixes and minor new
features. Java 8 is required."). The number is written as the archive writes it, with the leading `v`.
Field 12's rules speak of tags, GitHub releases and PyPI uploads; Autoplot's release-archive
directories are its equivalent release event, and are read as such here. Before `v2026a_8`, HSSI held
`v2026a_6` (2026-07-03), which `v2026a_7` (2026-08-13) and `v2026a_8` superseded.

**Release date.** 2026-11-12 is the UTC day of the release: the release page's `Last-Modified` is
`Thu, 12 Nov 2026 14:02:18 GMT`, the release jar's is 13:52:30 GMT, and the jar's own
`buildTime.txt` reads `2026-11-12T13:52Z`. The archive listing shows the server's local time
(`2026-11-12 08:02`), the same day. The notes' own heading, "Bugfixes (2026-11-11):", dates the last
listed fixes, not the release (rule 8).

**Which code the release holds.** No commit is tagged for it, so the release revision is read from the
jar, whose `META-INF/build.txt` names it (`build.tag: v2026a_9`). Every entry of the jar except
`buildTime.txt` and `META-INF/build.txt` has the same CRC as in the `20261111b` development build,
which was built at 2026-11-11T23:26Z, so the release is that build's code. The last commits before it
are Autoplot `6455ad60ed10ee271a00c15fe05e0cd6bee6f560` (2026-11-11 17:19 -06:00, "release notes") and
das2java `580c7d2c2` (2026-11-11 17:17 -06:00), then the head of das2java's main branch (see the
header note); the next Autoplot commit, `eb1ada209` (2026-11-12 15:28 -06:00, a bindings fix for bug
2920), came after both builds, and the `LayoutPanel` change made after it (`a45f1952b`, selecting a
plot's bindings) is absent from the jar's `LayoutPanel` classes. `6455ad60e` is an ancestor of the
default branch's head, so the repository holds the release's code.

**Description.** Taken from the v2026a_9 release page, which is the release body (rule 13). That page
carries four blocks. "Bugfixes (2026-11-11):" and "Features:" are this release's own. "Older Bugfixes
(2026-09-28):" repeats v2026a_8's "Bugfixes (2026-09-22):" item for item, so it is inherited and left
out (rule 11). "Less recent features:" repeats v2026a_8's "Features:" and adds one item, "BinaryDataSource
has ccsds control to select binary from telemetry stream.", which the project wrote into its notes on
2026-09-28 (`69af15b2c`), just after v2026a_8 was built and beside the commit that added
`ccsdsOffsetCorrection` (`8eb726c99`). It describes the ccsds control v2026a_8 already shipped, not
the offset correction that is new, and the project files it among the less recent features, so it is
left out with the rest of that block (rule 14). Of the 37 items in the two own blocks, two are dropped
under rule 14: "Minor clean up of PngWalkTool while considering more major corrections with ChatGPT."
(a cleanup that changes nothing a user sees) and "2900: Jemmy regression testing of HAPI server
dialog." (test housekeeping). The other 35 are user-facing fixes or features and are kept whole and in
the page's order (rules 14–15); whitespace is collapsed as the page renders it, the bug numbers that
are links on the page are kept as plain text, and the contributors' "Thanks, …!" credits are kept. The
doubled colon in "192:: synchronizeNN …" is the page's own text (its link text is "192:", followed by
a second colon), as is "didn't increment property." in the first item. HSSI held v2026a_8's own two
blocks until this update; they belonged to the replaced release and are not carried forward (rule 10).

*Version PID: none. The project deposits no DOI per release; DataCite and Zenodo searches on
2026-11-13 found no deposit of the software.*

**View-layer rendering.** HSSI stores this field as a bare version string, but the view API renders
it as `<software> - <number>` (`Autoplot - v2026a_9`). The value above is the bare string `v2026a_9`;
the `Autoplot - ` prefix must never be written into the field.

**Repository head is ahead of the release.** The default branch's head (`ffadec23c`, 2026-11-13)
carries four commits made after v2026a_9 was built: a fix for bug 2920 (only bindings without
converters are registered), showing and selecting a plot's bindings in the layout panel, and a warning
that axis labels will not be updated. None of it is recorded here. A later release update reads it
once a `v2026a_n` (or later series) directory publishes it. The work the head carried beyond v2026a_8
(the Jython debugger, the new PDS4 reader, `totalSpectralPower`) shipped in v2026a_9 and is recorded
above and in Fields 4, 18 and 29.

### 13. Programming Language (RECOMMENDED)
- Java

*`Java` is retained from HSSI and is overwhelmingly dominant: 12,711,065 bytes by GitHub's language statistics (97.2% of the repository), 1,000 `.java` files across 30 project modules in 33 top-level directories, `javac.source`/`javac.target` 1.8.*

**Considered and excluded, all on the same test — auxiliary to the application rather than constitutive of it:**

- **`Python 2.x`**. The Jython scripting layer is real and substantial — the `JythonSupport`
  and `JythonDataSource` modules, bundled Jython libraries, shipped `.py`/`.jy` files, registered
  `jyds`/`jy`/`inline` URI schemes, and the in-application script console and editor. It is
  nevertheless excluded because Field 13 asks what the software is written in and what is most
  important for it: Python is only 0.17% of the repository, and tagging a Java desktop application
  `Python 2.x` would misclassify it as a Python package. The scripting capability is represented in
  Fields 4, 8, and 16.
- **`Javascript`** (169,170 bytes) — entirely the `AutoplotServlet/web/thin/` browser thin client and JSP page assets. Recorded instead under Field 4, `Data Visualization: Web-Based`.
- **`IDL`** (63,953 bytes) — the `.pro` bridge and demo scripts in `IdlMatlabSupport/IDLDemo/` and `Autoplot/src/external/`, which call *into* Autoplot rather than constituting it. Recorded instead under Field 30.
- GitHub also reports small amounts of HTML, Shell, XSLT, Haskell, and CSS, none of which are significant.

*The three exclusions are decided on identical grounds, so the field is self-consistent: only Java is both what Autoplot is written in and what is most important for it.*

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1007/s12145-010-0049-0

*Retained from HSSI and verified. Crossref confirms: Faden, J. B., Weigel, R. S., Merka, J., & Friedel, R. H. W. (2010). "Autoplot: a browser for scientific data on the web." Earth Science Informatics, 3(1–2), 41–49, published 2010-04-25, Springer. Open preprint at `https://arxiv.org/abs/1004.2447`, which `https://autoplot.org` links as "Faden et al. 2010" in the very sentence quoted in the description. This DOI is a Crossref DOI and is not resolvable through the DataCite API.*

### 15. License (RECOMMENDED)
- **License:** GNU Lesser General Public License v3.0 only
- **License URI:** https://spdx.org/licenses/LGPL-3.0-only.html

*The name and URI use HSSI's canonical LGPL-3.0-only identity.*

**Evidence.** `LICENSE.txt` at the repository root is the verbatim FSF text of the GNU Lesser General Public License, Version 3, 29 June 2007 (165 lines). GitHub's license detection reports `LGPL-3.0` ("GNU Lesser General Public License v3.0"), and SoMEF independently reports `spdx_id: LGPL-3.0`. The das2java dependency is likewise LGPL v3. Decisively, the root license file was changed on 2018-11-26 in a commit whose message is "GPL was used where this has always been LGPL." — an explicit maintainer correction.

**Two documented discrepancies, neither of which changes the value.**
1. `Autoplot/src/LICENSE.txt` is a *different* file: the GNU General Public License **version 2** (339 lines). It is stale — its last touch was the 2017-06-27 "rename VirboAutoplot to Autoplot" directory move, predating the 2018-11-26 correction to the root file, which it never received. It sits under `src/` and so is packaged into the jar, which is why the older license text still circulates.
2. `https://autoplot.org` describes the software as "Open-source (GPL with classpath exception)". That phrasing is outdated relative to the 2018-11-26 correction; LGPL v3 is technically GPL v3 plus additional permissions, so the sentence is loosely in the same spirit but is not the license of record.

*Also noted: bundled third-party sources carry their own headers (ftp4j is LGPL 2.1, java-diff-utils is Apache-2.0, ProGAL is MIT). These are vendored dependencies and do not affect Autoplot's own license.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- data visualization
- plotting
- interactive
- gui
- time series
- spectrograms
- line plots
- Fourier analysis
- data reduction
- cdf
- ascii
- netcdf
- fits
- hapi
- das2
- pds
- ccsds
- ephemeris
- pitch angle distributions
- jython
- heliophysics
- space physics

*Stored identities are lower-case and were checked against HSSI's keyword vocabulary to avoid
near-duplicates. `pitch angle distributions` carries the PAD rendering capability that has no home
in the Field 4 taxonomy (see Field 4 exclusions).*

*`ccsds` was added with the v2026a_8 release, binding the existing lower-case row: that release added
CCSDS space-packet parsing (Field 4, `Packet Decommutation`; Field 18, `Other`). It names the packet
standard a searcher would type, which no other field carries, since Field 4 records the technique and
Field 18 has no CCSDS row, so it joins the format keywords above under rule 10. `telemetry`,
`decommutation`, `packet parsing` and `packets` were weighed and not added: each only restates the
Field 4 value (rule 6).*

*`debugger` was weighed when v2026a_9 added a Jython script debugger, and not added: it names a
script-editor tool, not a subject a searcher would type to find Autoplot (rule 10), and scripting is
already carried by `jython`.*

### 17. Data Sources (OPTIONAL)
- CDAWeb
- das2
- HAPI
- FTP/FTPS Directories
- HTTP/HTTPS Directories
- Other

*Added during the 2026-07-30 refresh.*

**Evidence.** `CDAWeb` — the `CDAWebDataSource` module registers the `cdaweb` extension and the `vap+cdaweb:` URI scheme; `CdfVirtualVars` reimplements the CDAWeb virtual-variable library; `AutoplotServlet`'s `CdawebVapServlet` builds `.vap` files from CDAWeb URIs. `das2` — `Das2ServerDataSource` (`das2server` extension, `vap+das2server:`), `FedCatDataSource` (`dc` extension, the das2 federated catalog, `org.das2.catalog`), and `DataSourcePack/src/org/autoplot/das2Stream` reading and writing das2 streams and QStream. `HAPI` — `HapiDataSource` (`hapi` extension, `vap+hapi:`, `HapiServer.java`), plus `HapiDataSourceFormat` and the `HapiServerDemo` server. `FTP/FTPS Directories` — `DataSource/src/ftpfs/` and the bundled `it.sauronsoftware.ftp4j` client provide an FTP virtual filesystem. `HTTP/HTTPS Directories` — `org/autoplot/wgetfs/` plus dasCoreUtil's `org.das2.util.filesystem` HTTP filesystem; directory listings are browsable (the shipped demo "Browse a directory tree at CDAWeb" targets `https://cdaweb.gsfc.nasa.gov/istp_public/data/`). `Other` — sources with no dedicated row: the PDS Planetary Plasma Interactions node (`PDSPPIDataSource`, `https://pds-ppi.igpp.ucla.edu/`), OPeNDAP (`OpenDapDataSource`, `dds`/`dods` extensions, bundled `opendap-2.1.jar`), TSDS (`TsdsDataSource`), SPASE and VOSPASE records (`DataSourcePack/src/org/autoplot/spase`, `vospase`), WDC files (`wdc` extension), and the SAMP messaging channel (`AddSampListener`, bundled `jsamp-1.3.5.jar`) by which other applications hand Autoplot a URI to plot.

*Considered and excluded, with reasons: `Observatory/Mission-specific` — Autoplot has no mission-specific reader; every archive it supports (CDAWeb, PDS-PPI, HAPI, das2) is multi-mission, and Field 17's instruction to select this value is conditioned on naming an observatory in Field 32, which is correctly empty here. `SSCWeb`, `OMNIWeb`, `AMDA`, `Madrigal`, `VirES`, `GFZ`, `WDC` (as a service), `TAP`, `The Virtual Solar Observatory.`, `S3/Cloud-aware` — searched the whole tree; no client code for any of them. (`wdc` is a Jython-extension file reader, not a WDC service client, so it is covered by `Other`.)*

### 18. Input File Formats (RECOMMENDED)
- ascii
- CDF
- csv
- FITS
- HDF5
- IDL.sav
- ISTP-Compliant
- JSON
- netCDF3/4
- Other

*Added during the 2026-07-30 refresh. Enumerated from the authoritative registration files `META-INF/org.autoplot.datasource.DataSourceFactory.extensions` in every module.*

**Evidence.** `ascii` — `org.autoplot.ascii.AsciiTableDataSourceFactory` (`dat txt csv tab`) and `OdlDataSourceFactory` (`sts odl`). `CDF` — `org.autoplot.cdf.CdfJavaDataSourceFactory` (`cdfj cdfn cdf`), a 77-file vendored pure-Java reader (`gov.nasa.gsfc.spdf.cdfj`) plus `cdfjava.3.3.2.tt2000.jar`. `csv` — `AsciiTableDataSourceFactory` (`csv`) and `org.autoplot.csv.CsvDataSourceFactory` (`csv0`). `FITS` — `org.autoplot.fits.FitsDataSourceFactory` (`fits fts`) with `jfits-0.93.jar`. `HDF5` — `org.autoplot.netCDF.NetCDFDataSourceFactory` (`h5 hdf5 hdf`). `IDL.sav` — `org.autoplot.idlsupport.IdlsavDataSourceFactory` (`sav idlsav`) with `ReadIDLSav.java`. `ISTP-Compliant` — `DataSource/src/org/autoplot/metatree/IstpMetadataModel.java` interprets the ISTP metadata conventions (`DEPEND_0`, `VAR_TYPE`, `DISPLAY_TYPE`, `FILLVAL`, `VALIDMIN`/`VALIDMAX`, `LABL_PTR`), and `CdfVirtualVars` implements the ISTP/CDAWeb virtual-variable functions. `JSON` — `org.autoplot.json.JSONDataSourceFactory` (`jsonl`), plus HAPI info/catalog JSON parsed by `HapiDataSource`/`HapiServer` and TFCat (`tfcat`). `netCDF3/4` — `NetCDFDataSourceFactory` (`nc ncml nc4`) on `netcdfAll-5.5.3.jar`. `Other` — formats with no row: PDS3 and PDS4 labels (`org.autoplot.pds.Pds3DataSourceFactory`/`PdsDataSourceFactory`, `pds pds4 lblx lbl`; since v2026a_9, read at `6455ad60e`, PDS4 products are read by Autoplot's own `org.autoplot.pds4.Pds4Reader` through `Pds4DataSource`, with the earlier `pds4-jparser-1.10.0-SNAPSHOT.jar` path kept behind the URI parameter `newP=F`), Cluster Exchange Format (`org.autoplot.cefdatasource.CefDataSourceFactory`, `cef`), MATLAB `.mat` (`org.autoplot.matsupport.MatDataSourceFactory`, on `com.jmatio`), Excel `.xls` (`org.autoplot.excel.ExcelSpreadsheetDataSourceFactory`, on Apache POI), raw binary (`org.autoplot.binarydatasource.BinaryDataSourceFactory`, `bin`), CCSDS space-packet streams (the same factory's `ccsds=` switch, added in the v2026a_8 release and read at `acdaee73a`; Field 4, `Packet Decommutation`; the FileFormat vocabulary has no CCSDS row), WAV audio (`org.autoplot.wav.WavDataSourceFactory`) and live audio input (`AudioSystemDataSourceFactory`), images (`org.autoplot.imagedatasource.ImageDataSourceFactory`, `jpg png gif`), das2 streams and QStream (`d2s d2t das2Stream qds qdst`), XML and HTML tables (`xml`, `htm html`), orbit/ephemeris tables (`orbit`), NumPy `.npy`, `sps`/`spd`, and `wdc`.

*`Zarr` explicitly excluded — searched the whole tree; there is no Zarr support.*

### 19. Output File Formats (RECOMMENDED)
- ascii
- CDF
- csv
- HDF5
- IDL.sav
- ISTP-Compliant
- JSON
- netCDF3/4
- Other

*Added during the 2026-07-30 refresh. Enumerated from the `META-INF/org.autoplot.datasource.DataSourceFormat.extensions` registration files, which are a strict subset of the input formats.*

**Evidence.** `ascii` — `org.autoplot.ascii.AsciiTableDataSourceFormat` (`dat txt`). `CDF` — `org.autoplot.cdf.CdfDataSourceFormat` (`cdfj cdf`). `csv` — `org.autoplot.csv.CsvDataSourceFormat`. `HDF5` — `org.autoplot.netCDF.HDF5DataSourceFormat` (`h5 hdf5`). `IDL.sav` — `org.autoplot.idlsupport.IdlsavDataSourceFormat` (`idlsav sav`), implemented in `WriteIDLSav.java`. `ISTP-Compliant` — `CdfDataSourceFormat` writes ISTP variable attributes (`VAR_TYPE` as `data`/`support_data`, `DISPLAY_TYPE`, `FIELDNAM`, `VALIDMIN`/`VALIDMAX` including the TT2000 case), so exported CDFs follow the ISTP conventions. `JSON` — `HapiDataSourceFormat` writes `info/<id>.json` and `capabilities.json`, and the `HapiServerDemo` servlets emit HAPI JSON. `netCDF3/4` — `HDF5DataSourceFormat` also registers `nc` and writes through `NetcdfFormatWriter.createNewNetcdf4(NetcdfFileFormat.NETCDF4_CLASSIC, ...)`. `Other` — MATLAB `.mat` (`MatDataSourceFormat`), Excel `.xls` (`ExcelSpreadsheetDataSourceFormat`), WAV (`WavDataSourceFormat`) and live audio (`AudioSystemDataSourceFormat`), raw binary (`BinaryDataSourceFormat`), das2 stream (`Das2StreamDataSourceFormat`) and QStream (`QStreamDataSourceFormat`), HTML tables (`HtmlTableFormat`), images (`ImageDataSourceFormat`, `jpg png gif`), and the graphics outputs PNG, PDF, and SVG (`ScriptContext.writeToPng/writeToPdf/writeToSvg`, on `itextpdf-5.4.3.jar` and Batik `batik-svggen`), plus animated GIF (Field 4, Movies) and the `.vap` XML session file.

*`FITS` deliberately absent from this list: `FitsDataSource` is read-only — no `DataSourceFormat` is registered for `fits`/`fts`. `Zarr` absent for the same reason as Field 18.*

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

*Added during the 2026-07-30 refresh. Evidence: the release page template `Autoplot/src/index.html` offers, for every release, a `.dmg` ("a self-contained installer for Mac computers"), an `.exe` ("a self-contained installer for Windows computers"), and `.deb` and `.rpm` packages for Linux, all built with Install4J; the single-jar release "can be launched on Windows and Mac, and contain[s] a shell script for launching on Unix computers" (`Autoplot/jumbojar_header.txt`, `starterScript.sh`). Java 8 is the stated requirement.*

*Considered: `Operating System Independent` is arguably the most accurate single value, since Autoplot is a pure-Java Swing application and its single-jar runs on any JVM. It is not asserted because the four platform-specific installers are the concrete, citable evidence and because selecting both a cross-platform value and three named platforms is contradictory. A user who prefers `Operating System Independent` instead of these three has a good case. `Solaris` and `MobilePlatform` have no supporting evidence.*

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent
- x86-64

*Added during the 2026-07-30 refresh. `CPU Independent`: Autoplot compiles to Java bytecode (`javac.target=1.8`) with no JNI dependency in the delivered application — the CDF reader is pure Java (`gov.nasa.gsfc.spdf.cdfj`), so the single jar runs on any JVM. The release page states "On 32-bit systems, use the single-jar release and a 32-bit version of Java," explicitly supporting non-64-bit hosts. `x86-64`: the Install4J installers are named for that architecture, e.g. `autoplot-dev_windows-x64_#{tag}.exe` in `Autoplot/src/index.html`.*

*Note: `Apple Silicon arm64` and `Linux aarch64 or arm64` are almost certainly fine in practice via any arm64 JVM, but the repository contains no Install4J configuration (it lives in the separate `autoplot/installers` repository) and no arm64-named artifact, so neither is asserted. A stray `libcdfNativeLibrary.so` exists at `Autoplot/libcdfNativeLibrary.so` but nothing in the build or the registered data sources loads it.*

### 22. Related Phenomena (OPTIONAL)
- Solar Wind

*Added during the 2026-07-30 refresh. Evidence: `CdfJavaDataSource/src/org/autoplot/cdf/CdfVirtualVars.java` contains solar-wind-specific derived-quantity code — `calcP` computes solar-wind dynamic pressure from `V_GSE_p` and `np`, and `region_filt` masks samples to the solar-wind region (`if ( region_data.value(i) != 1 ) { // 1=solar wind`). Corroborated by `Autoplot/src/external/tdas_store_data.pro`, whose worked example loads `https://autoplot.org/data/proton_velocity_rtn.qds`.*

*Considered and excluded: `Geomagnetic Storms` — the Dst index does appear in this repository, as a javadoc usage example at `Autoplot/src/external/AnnotationCommand.java:30` (`plot( 'vap+cdaweb:ds=OMNI2_H0_MRG1HR&id=DST1800&timerange=Oct+2016' )`), and again as the shipped demo bookmark "Demo 1: DST from OMNI via CDAWeb" in the separate `autoplot/bookmarks` repository. Both are illustrations of URI syntax, not storm functionality: there is no Dst-, index-, or storm-specific code anywhere in the tree. `Solar Flares` and `X-ray emission` — RHESSI quick-look FITS images appear only as demo bookmarks; `FitsDataSource` is a generic FITS reader. `Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona` — no evidence of any kind. This field is intentionally minimal: Autoplot is a phenomenon-agnostic browser, and the vocabulary is closed, so phenomena it merely displays belong in Keywords.*

### 23. Development Status (RECOMMENDED)
Active

*Added during the 2026-07-30 refresh. Evidence as of 2026-11-13: the default branch has near-daily commits, the latest of them `ffadec23c` on 2026-11-13; the release archive `https://autoplot.org/jnlp/` shows a steady cadence of releases (`v2026a_1` 2026-01-09 through `v2026a_9` 2026-11-12) plus dated development builds through `20261111b`; the GitHub repository is not archived; `README.md` carries no status badge or status statement. Autoplot has been in continuous stable use since 2008 and is being actively developed — the definition of `Active`.*

### 24. Documentation (RECOMMENDED)
https://github.com/autoplot/documentation/blob/main/md/help.md

*Added during the 2026-07-30 refresh. This is the project's canonical user documentation, linked from `https://autoplot.org` as "Help" and containing installation instructions at the `#installation` anchor, together with per-format sections (`#formats-read`, `#ascii-table`, `#binary-table`, `#excel-spreadsheet`, `#images`, `#wav`, `#tsds`) and aggregation/CDAWeb guidance. `https://autoplot.org/help` is the project's stable short alias and 301-redirects to this URL; the direct URL is recorded to avoid depending on the redirect. Related documentation pages in the same repository: `md/cookbook.md`, `md/scripting.md`, `md/Autoplot_from_source.md`, `md/MacrosInVaps.md`, `md/developer.vapModifiers.md`, and the wiki pages `wiki/idl`, `wiki/matlab`, `wiki/PNG_Walks`. (The `autoplot/documentation` repository's top level is only `README.md`, `javadoc/`, and `md/` — there is no `docs/` directory, so any `docs/...` path linked from elsewhere is stale.) Developer build instructions are also in this repository's own `README.md`. Autoplot additionally ships in-application JavaHelp (`AutoplotHelp` module, `Autoplot/javahelp`).*

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

*Evidence: `Autoplot/src/org/autoplot/aboutAutoplot.html` states "Autoplot was developed initially
under NASA Grant 05-S3CVO05-11 ("Virtual Observatories") and under various other grants."; the
reference publication's abstract states "Autoplot is software developed for the Virtual
Observatories in Heliophysics"; and the software description names the NASA Virtual Observatories
for Heliophysics program. The name and ROR use HSSI's canonical NASA identity.*

*Considered and not listed as funders: PDS-PPI Node, RBSP-ECT, and the Radio and Plasma Wave Group at The University of Iowa are named in the description as providing "support or code contributions", and `aboutAutoplot.html` credits their people as contributors (Field 6) — that is collaboration and in-kind contribution, not identified financial sponsorship, so they are not asserted here. The "various other grants" mentioned in `aboutAutoplot.html` are not enumerated anywhere in the repository or on `autoplot.org`, and are not invented.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Virtual Observatories
- **Award Number:** 05-S3CVO05-11

*This replaces the prior blank award association.*

**Evidence.** Verbatim from the software's own in-application credits page, `Autoplot/src/org/autoplot/aboutAutoplot.html`: "Autoplot was developed initially under NASA Grant 05-S3CVO05-11 ("Virtual Observatories") and under various other grants." The award number format is consistent with a NASA ROSES-2005 proposal number for the Sun-Solar System Connection Virtual Observatories element, which matches both the reference publication ("developed for the Virtual Observatories in Heliophysics") and the stored HSSI description.

*Honest caveat: this award number could not be corroborated in any public grant database — a targeted search returned nothing for `05-S3CVO05-11`. It is asserted solely on the strength of the maintainer-authored About page in the repository, which is primary evidence for this software but is the only source. The award title "Virtual Observatories" is the exact parenthetical from that sentence; the fuller programme name used elsewhere is "Virtual Observatories for Heliophysics". Nothing has been invented, and no second award number exists to record for the "various other grants".*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.5281/zenodo.17382348 — Faden, J. (2025). *Autoplot in 2025 — Review of Lessons Learned* [Poster]. Zenodo. Issued 2025-10-18.
- https://doi.org/10.5281/zenodo.8411503 — Faden, J. (2023). *Using Autoplot Java Codes to Support Analysis in Python* [Poster]. Zenodo. Issued 2023-10-05.

*Added during the 2026-07-30 refresh. Both are authored by Jeremy Faden and are specifically about Autoplot, verified through the DataCite API. The 2025 poster reviews the system's design history ("Autoplot is a data visualization and analysis system introduced in 2007 ... written to provide an free and open alternative to IDL" — sic); the 2023 poster documents the jpype-based Python bridge that is Field 30's `autoplot/python` entry. The reference publication (Field 14) is deliberately not duplicated here; its open preprint is `https://arxiv.org/abs/1004.2447`.*

*Considered and excluded: other Zenodo hits for the query "autoplot" (`ISTP Metadata Guidelines`, `Interoperable Heliophysics Data Access via HAPI`, and deposits from science projects that used Autoplot) are not publications about this software (rule 3); science uses are weighed under rule 5 below.*

**Publications using Autoplot (rule 5), searched 2026-11-02.** ADS acknowledgement and full-text
searches (`ack:"Autoplot"`, `full:"Autoplot"`; a nonsense token returns 0 and `full:"pyspedas"` returns
hits as controls) find some thirty papers, from 2013 to 2026 and all in heliophysics, that credit
Autoplot in their Acknowledgments, and further papers that name it deliberately in their methods or
figure text. Recent examples: Lysak et al. 2025, *New Plasma Regime in Jupiter's Auroral Zones*
(https://doi.org/10.1103/fn63-qmb7: "The authors would like to acknowledge Jeremy Faden and the use of
Autoplot, which was used to present the data shown."); the TRACERS Magnetic Search Coil instrument
paper (https://doi.org/10.1007/s11214-025-01200-7), which acknowledges it; Powers et al. 2026,
*Characterizing Plasma Sheet Flows With Machine Learning Identification*
(https://doi.org/10.1029/2026JA035457: "Hand labeling of events was performed in Autoplot (Faden et
al., 2010)"); and Ge et al. 2026, *Evidence for Ring Current Decay Ions Reaching the Moon When the
Moon is outside the Earth's Bow Shock* (https://doi.org/10.3847/1538-4357/ae9160: "This figure was
generated using Autoplot software."). Autoplot's citing literature is therefore not small: a list of
thirty or more users would bury the two posters about the software and tell a searcher little about
it, so rule 5 adds none of them. The full-text hits also include unrelated uses of the
word (the agricultural "AutoPlot grid" tool, for one), so their count is not a measure of use.

**The developers' deposits since 2026-07-30** (Zenodo creator search for Jeremy Faden, with Robert
Weigel as a control) are slide-deck presentations about the HAPI specification
(https://doi.org/10.5281/zenodo.21793481, https://doi.org/10.5281/zenodo.23144432), not about
Autoplot (rule 3), and report no results made with it.

**Other deposits since 2026-07-30.** The VESPA 2026 presentation by Erard, Cecconi and le Sidaner
(https://doi.org/10.5281/zenodo.23264149) names Autoplot twice: its description lists it among the
analysis tools the VESPA portal connects to, and a slide caption among the deck's use-case figures
reads "Comparison of radio dynamic spectra (ground/space) in Autoplot", beside figures for Aladin and
TOPCAT. The deck is about the VESPA infrastructure, not Autoplot. None of these decks qualifies on its subject, so whether they stand alone
does not arise.

**Searched again 2026-11-13, at the v2026a_9 release update.** ADS full-text and acknowledgement
searches over records entered since 2026-11-02 (`full:"Autoplot"`, `ack:"Autoplot"`; over the same
window a nonsense token returns 0 and `full:"pyspedas"` returns hits) find none, and a title and
abstract search since 2026-07-01 finds only the agricultural "AutoPlot grid" paper. DataCite and
Zenodo free-text searches for "autoplot" find nothing deposited since 2026-11-02. The Zenodo creator
searches (Jeremy Faden by name and by ORCID, Robert Weigel by name) find two developers' deposits not
weighed above, neither about Autoplot (rule 3): *ISTP Metadata Guidelines: Current Status and Future
Development* (https://doi.org/10.5281/zenodo.23111203, deposited 2026-10-03), on the ISTP metadata
conventions, and Weigel's *Heliophysics Data API (HAPI)* presentation
(https://doi.org/10.5281/zenodo.23889215, deposited 2026-11-02, dated 2023-10-12), on HAPI. No new
paper names a funder for Fields 25–26.

### 28. Related Datasets (OPTIONAL)
Not found

*Autoplot is deliberately dataset-agnostic: it reads whatever a URI points at. The repository contains no dataset DOIs, and the concrete datasets it references (CDAWeb OMNI, RBSP/EMFISIS, Voyager PWS, Juno JADE/JED, Cassini MIMI, MAVEN MAG) appear only as javadoc examples, test fixtures, or entries in the separate `autoplot/bookmarks` demo lists. Naming any of them would misrepresent a general-purpose browser as dataset-specific.*

### 29. Related Software (OPTIONAL)
- https://github.com/das-developers/das2java — **das2java**. The das2 Java library that Autoplot is built on and developed alongside: the QDataSet data model, the `dasCore` graphics engine and renderers, `dasCoreDatum` units, and `QStream`. It is a declared git submodule of this repository (`README.md:15-17`: "uses another repo for the Das2 library which has developed along with Autoplot.  The dependency library is linked as as git submodule." — the doubled "as as" is in the source), and `aboutAutoplot.html` states "Autoplot uses Das2, an open-source java library for data visualization and data analysis created by the Radio and Plasma Wave Group at the University of Iowa." A domain-specific dependency without which Autoplot is not describable. *(Also in Field 30 — see there for the interoperability evidence.)*
- https://github.com/autoplot/cdfj — **cdfj**, "Pure-Java code for reading NASA/GSFC CDF (Common Data Format) files". Vendored into `CdfJavaDataSource/src/gov/nasa/gsfc/spdf/cdfj/` (77 Java files; the enclosing `CdfJavaDataSource` module is 96 in total, the other 19 being Autoplot's own adapter code) and shipped as `APLibs/lib/cdfjava.3.3.2.tt2000.jar`. A heliophysics-specific dependency: it is what makes Autoplot's flagship CDF and CDAWeb support possible.
- https://github.com/autoplot/pds4-jparser — **pds4-jparser**, "Java Library providing APIs for parsing and exporting information on PDS4 products". Shipped as `APLibs/lib/pds4-jparser-1.10.0-SNAPSHOT.jar`; until v2026a_9 it read every PDS4 product (`PDSDataSource`'s `PdsDataSourceFactory`, `pds4`/`lblx` extensions). A planetary-science-specific dependency. Its role narrowed in v2026a_9, and it is kept: that release made Autoplot's own reader the default ("890: New PDS4 reader supports Java 8 and will be maintained within Autoplot."), and at `6455ad60e` `PdsDataSourceFactory.newparser` is `true`, so PDS4 products go to `Pds4DataSource` and `org.autoplot.pds4.Pds4Reader`, neither of which imports `gov.nasa.pds`. The pds4-jparser reader (`PdsDataSource`) is still offered through the URI parameter `newP=F`, the jar is still in the tree, and the v2026a_9 `autoplot.jar` still carries its `gov.nasa.pds` classes, so the relation is current (rule 7). Remove the entry once a release no longer ships the library or drops the `newP` switch.

*Considered and excluded as generic infrastructure (Tier A), each of which would read the same for any Java desktop application: Apache POI, Apache Batik, iText, Apache Commons (compress/math/net/vfs), netCDF-Java, the OPeNDAP client, jmatio, jfits, jsyntaxpane, FlatLaf, MigLayout, JavaHelp, metadata-extractor, ProGuard, Jemmy, JUnit, javacsv, JSch, org.json, java-diff-utils, ProGAL, Install4J. netCDF-Java and jfits are Tier-B-adjacent format libraries, but the relationship is plain dependency use with no documented exchange, so they belong to Fields 18/19 as format support rather than here. Jython is excluded as a language runtime — infrastructure equally at home in any JVM application — even though the scripting layer it enables is recorded in Fields 4, 13, and 16. JSAMP (`jsamp-1.3.5.jar`, `AddSampListener`, `external/AddCfaSampListener`) is genuinely interoperability plumbing — Autoplot can join or start a SAMP hub and receive URIs from other applications. `Autoplot/src/org/autoplot/AddSampListener.java:42-44` does name counterpart clients: "Listener for the Cluster Final Archive SAMP protocol. Other clients include the SOHO archive viewer, and Ulysses, will include the Cluster Final Archive viewer." The exclusion stands on a narrower ground than "no counterpart exists": those clients are named only informally, in a prose javadoc comment, with no citable package identity, version, or canonical URL, so no entry that satisfies Field 29's requirement — enter the DOI for the software code, otherwise link to its code repository — can be constructed. JSAMP itself is a protocol library rather than a peer tool.*

### 30. Interoperable Software (OPTIONAL)
- https://github.com/das-developers/das2java — **das2java**. Shared data model and format, not merely a dependency: Autoplot's `DataSourcePack/src/org/autoplot/das2Stream/` both **reads and writes** das2 streams (`Das2StreamDataSourceFactory`/`Das2StreamDataSourceFormat`, `d2s`/`d2t`) and QStream (`QStreamDataSourceFactory`/`QStreamDataSourceFormat`, `qds`/`qdst`), and `Das2ServerDataSource` speaks the das2 server protocol, so data moves in both directions between Autoplot and any das2 tool over the same QDataSet model and stream format. das2java releases and Autoplot releases are cut in step (the v2026a_6 notes cite das2java issue 182 by number).
- https://github.com/autoplot/python — **autoplot/python**, the project's official companion Python package, "bridge from python, using jpype" (BSD-3-Clause). It is the designated successor to the in-repo Python helpers: `Autoplot/src/external/applot.py:1` opens `# Do not use this.  See https://github.com/autoplot/python/.` and `Autoplot/src/external/jpypeutil.py:1` opens with the same header minus the final period `jpypeutil.javaaddpath` shows the mechanism — load `autoplot.jar` into a JVM from Python and import the classes — and `applot.das2stream` writes a das2 stream from a Python dict for Autoplot to plot. The 2023 poster in Field 27 documents this interface end to end.
- https://www.mathworks.com/products/matlab.html — **MATLAB**. A documented, purpose-built adapter, not incidental dependency use: `IdlMatlabSupport/src/org/autoplot/idlsupport/QDataSetBridge.java` is an abstract bridge whose javadoc reads "See http://autoplot.org/IDL and http://autoplot.org/Matlab which show how this is used in the environments", exposing QDataSet rank, values, `depend(n)`, units, and fill handling to a MATLAB session over the Java bridge; `IdlMatlabSupport/src/org/autoplot/matsupport/` additionally reads *and* writes MATLAB `.mat` files (`MatDataSourceFactory`, `MatDataSourceFormat`). `https://autoplot.org` states the capability plainly: "Data access layer for file reading may be used in MATLAB, IDL, or SciPy (via Java bridge), providing a common interface regardless of data source", and the documentation wiki has a dedicated `matlab` page.
- https://www.nv5geospatialsoftware.com/Products/IDL — **IDL**. The same `QDataSetBridge`, plus concrete IDL clients that instantiate the bridge class over the IDL-Java bridge. There are three real instantiation sites, quoted verbatim: `IdlMatlabSupport/IDLDemo/src/APDataSetDemo.pro:8` and `ap_getdataset.pro:78`, both `OBJ_NEW('IDLjavaObject$GetDataSet', 'org.virbo.idlsupport.APDataSet')`, and `Autoplot/src/external/tdas_store_data.pro:8`, `OBJ_NEW('IDLjavaObject$APDataSet', 'org.idlsupport.APDataSet')`. Note that the IDL demos still target the pre-2017 `org.virbo.*` package, which is retained in the tree (`IdlMatlabSupport/src/org/virbo/idlsupport/APDataSet.java`) alongside the current `org.autoplot.idlsupport.APDataSet`; no `.pro` file references the `org.autoplot.*` class name. `Autoplot/src/external/applot.pro` drives Autoplot from IDL, and `IdlsavDataSource`/`IdlsavDataSourceFormat` read and write IDLSave `.sav` files in both directions. Documented at the `idl` wiki page.
- https://github.com/spedas/bleeding_edge — **SPEDAS**. A bidirectional IDL adapter to the `tplot`/`store_data` data system, in two files: `Autoplot/src/external/tdas_applot.pro` reads the `tplot_com1` common block and its `data_quants` structure (`common tplot_com1, data_quants, tplot_vars , tplot_configs, current_config , foo1,foo2`, `tdas_applot.pro:6`) and plots the named `tplot` variable in Autoplot, and `Autoplot/src/external/tdas_store_data.pro` runs the reverse direction, pulling an Autoplot URI through `APDataSet` and calling IDL `store_data` to register it as a `tplot` variable. That is a documented export-to-import handoff in both directions, which is what this field asks for. **Naming, stated honestly:** both files were written against **TDAS**, the THEMIS Data Analysis Software, which has since been superseded by SPEDAS; the URL above is SPEDAS because that is where the software lives now, and the `tplot`/`store_data` interface the adapters target is unchanged across the rename. `tdas_store_data.pro`'s header describes itself as demonstrating the interface, which does not disqualify it — a working, documented handoff is a handoff whether or not its header calls itself a demonstration.

*Weighed and not added: the VESPA planetary-data portal. Its 2026 presentation
(https://doi.org/10.5281/zenodo.23264149) says the portal connects distributed services "to analysis
tools such as Aladin, TOPCAT, QGIS, and Autoplot", and a slide caption in the deposited PDF reads
"Comparison of radio dynamic spectra (ground/space) in Autoplot". These two are the only statements
found, and neither documents how VESPA hands data to Autoplot: the Autoplot tree has no VESPA or
EPN-TAP code, the VESPA portal page returned a server error and its help
wiki requires a login, so the pairing is not documented where it could be checked (rule 5). Reopen it
when a public VESPA document or example shows the hand-off to Autoplot.*

*Excluded: everything in Field 29's Tier A exclusion list, for the same reasons. "Part of the Java scientific ecosystem" and "reads CDF like everything else in heliophysics" are not demonstrated exchanges with any particular package.*

### 31. Related Instruments (OPTIONAL)
Not found — intentionally empty.

*Autoplot is instrument-agnostic by design: it is a general-purpose browser whose whole premise is that a URI's extension selects a reader and everything downstream is uniform. It contains no instrument-specific reader, calibration, or convention. Applying the relevance gate before any vocabulary lookup, every instrument-adjacent mention in the tree fails it:*

- *Javadoc and `main()` example URIs — Cassini MIMI/LEMMS and CAPS in `PDSPPIDataSource/src/org/autoplot/pdsppi/PDSPPIDB.java` and `PDSPPIFileSystem.java`; Voyager 1/2 CRS in `PDSPPIDataSourceEditorPanel.main()`; Juno JED in `Das2ServerDataSourceEditorPanel.getDataSetId`; RBSP EMFISIS HFR in `AutoplotServlet/web/completions.html`. These are illustrations of URI syntax, which the gate excludes as example name-drops.*
- *Demo content in a different repository — the Voyager PWS, Juno JADE, MAVEN MAG, Polar Hydra, LANL SOPA/ESP, and GOES EPS entries live in `autoplot/bookmarks`, are loaded at runtime from a URL, and are demos. They belong to neither this repository nor this field.*
- *Field-misallocation candidates, correctly routed elsewhere — CDAWeb, HAPI, PDS-PPI, das2 servers, federated das2 catalogs, TSDS, and OPeNDAP are multi-mission **data sources and access protocols**, recorded in Field 17. CDF, netCDF, FITS, HDF5, PDS3/PDS4, and CEF are multi-instrument **file formats**, recorded in Fields 18–19. ISTP is a **metadata convention**, recorded as `ISTP-Compliant` in Fields 18–19.*
- *A single genuinely instrument-shaped code path exists — `CdfVirtualVars.apply_qflag`'s channel mapping for `flux_h`/`flux_o`/`flux_he_1`/`flux_he_2` and `apply_esa_qflag` — but these are the generic CDAWeb virtual-variable functions reimplemented from `virtual_funcs.pro` for **any** ISTP CDF that declares them, not support for a named instrument.*

*Because nothing passes the relevance gate, no entry reaches the SPASE resolution ladder and none
is invented. Consistent with ladder rule 6, no name is recorded without an
`https://spase-metadata.org/` identifier.*

### 32. Related Observatories (OPTIONAL)
Not found — intentionally empty.

*Same analysis as Field 31, applied at the mission/observatory level: Autoplot is observatory-agnostic, and every mission name in the repository (Voyager, Galileo, Cassini, Juno, MAVEN, RBSP, GOES, Polar, plus the multi-body ephemeris demos for Earth, Jupiter, Saturn, Uranus, Neptune, and the Sun) appears only in URI examples, `main()` harnesses, or the external demo bookmark lists. No mission-team tool, no mission data convention, no purpose-built support.*

*Note on the deliberate asymmetry with Field 5: the same PDS-PPI and das2-server evidence that supports `Planetary Magnetospheres`, `Jupiter Magnetosphere`, and `Saturn Magnetosphere` as **regions the software's functionality is used for** does not make any individual mission a **designed-to-support observatory** — the gates differ, and the module-level support is for the multi-mission archive and protocol, not for a named platform. Field 17 correspondingly does **not** select `Observatory/Mission-specific`.*

**Strongest counter-evidence found, and why it was still rejected.** The orbit time-range picker hardcodes a Radiation Belt Storm Probes default: `DataSource/src/org/autoplot/datasource/TimeRangeTool.java:190` reads `final String sc= prefs.get(PREF_SPACECRAFT, "rbspa-pp" );`, line 200 sets the status text `"loading orbits for rbspa"`, and `TimeRangeEditor.java:635` ships `orbit:rbspa-pp:30` as the menu example. This is the only place in the repository where a named mission is baked into executable behaviour rather than into a comment. It was nevertheless judged **not** to meet the "designed to support that specific observatory" bar: the mechanism is the generic `orbit:` scheme, which resolves any orbits file (line 636 offers `orbit:http://das2.org/wiki/index.php/Orbits/rbspa-pp:30` for exactly that reason) and is backed by the separate `autoplot/orbits` repository of "Orbit tables for various missions"; `rbspa-pp` is a user-overridable preference default, not mission support. A scientist working with RBSP data would not reach for Autoplot *because of* this, and a user searching HSSI for `observatory:"Van Allen Probes"` should not get Autoplot back.

**TRACERS orbit tables, weighed at the v2026a_8 release update.** das2java's
`dasCoreDatum/src/org/das2/datum/Orbits.java`, as bundled into v2026a_8 (das2java `256ede719`), maps
the `orbit:` names `ts1-orbit`, `ts2-orbit`, `ts1-roi-list` and `ts2-roi-list` to TRACERS
orbit-number and region-of-interest tables on `https://tracers-portal.physics.uiowa.edu/`, beside the
`rbspa-pp`/`rbspb-pp`, `crres` and `cassini` entries that were already there at the `das2java`
gitlink. They are shortcut names inside the same generic `orbit:` scheme judged above for RBSP: tables
of time ranges for picking an interval, not a reader, calibration or convention for TRACERS data. So
TRACERS is not listed either (Field 31 rule 4).

*Recorded for auditability: had this qualified, the SPASE-backed values would have been `https://spase-metadata.org/SMWG/Observatory/RBSP` and, for the EMFISIS URIs used as completion examples, `https://spase-metadata.org/SMWG/Instrument/RBSP/A/EMFISIS`. The field is kept empty.*

*No name is recorded without an `https://spase-metadata.org/` identifier.*

### 33. Logo (OPTIONAL)
https://autoplot.org/Logo96.png

*This is the logo used on the project's own home page
(`<img alt="Logo96.png" src="Logo96.png" width="96" height="96" border="0" />` in the
`https://autoplot.org` masthead), publicly accessible from the project's permanent domain.
In-repository alternatives (`Autoplot/src/logoA16x16.png`, `icon.png`, `smallSplash.svg`,
`splash.svg`) are splash/icon art rather than the published logo.*

---

## Record notes

- Autoplot's authoritative source migrated from SourceForge SVN to
  `https://github.com/autoplot/autoplot` in June 2025. The former Field 3 value was a release page,
  not a source repository.
- The current published release is `v2026a_9` dated 2026-11-12, built from Autoplot `6455ad60e`
  and das2java `580c7d2c2`. Repository head contains later, unreleased work, so Field 12 describes the
  published release rather than head.
- The final author set contains six credited people. A prior sentence fragment recorded as
  `"the Autoplot development"` / `"team"` was removed because it was neither a person nor an
  organization.
- Python/Jython scripting remains documented in Fields 4, 8, and 16, but Field 13 contains only
  Java because that is the application's implementation language.
- Fields 31 and 32 remain empty because Autoplot is instrument- and observatory-agnostic; concrete
  mission and instrument names occur only in examples, generic archive adapters, or external demo
  lists.
