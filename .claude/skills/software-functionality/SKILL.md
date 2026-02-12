---
name: software-functionality
description: >
  Analytical framework for classifying software into HSSI Software Functionality categories.
  Use when analyzing, extracting, or validating the Software Functionality field (Field 4) for
  HSSI metadata. Provides code patterns, library mappings, and decision guidance for the 85+
  functionality values.
user-invocable: false
---

# Software Functionality Classification Guide

The HSSI Software Functionality field (Field 4) is the most analytically demanding metadata field. It requires understanding what a software package actually does and mapping those capabilities to a taxonomy of 85+ values.

This guide provides the framework for doing that classification accurately and exhaustively.

---

## Taxonomy Structure

The taxonomy uses two levels: **top-level categories** and **subcategories**.

**Rule: When a subcategory applies, ALWAYS also include its parent top-level category.**

Example: If software produces spectrograms, list BOTH:
- Data Visualization
- Data Visualization:Spectrogram

There are 6 top-level categories:
1. Coordinate Transforms
2. Data Processing and Analysis
3. Data Visualization
4. Mission-related
5. Models and Simulations
6. Servers and Environments

---

## Category Reference

### 1. Coordinate Transforms

**What it means:** Software that converts between coordinate systems or reference frames as a user-facing capability.

**Key indicators:**
- Functions named `transform`, `convert`, `to_*`, `from_*` relating to coordinate systems
- Import or use of coordinate libraries (see library table below)
- References to specific coordinate systems: GSE, GSM, GEO, SM, MAG, AACGM, HEE, HCI, HAE, RTN, Carrington, Stonyhurst, helioprojective, geographic, geomagnetic, MLT

**Subcategories and when to use them:**

| Subcategory | Use when the software converts... | Typical indicators |
|---|---|---|
| **Heliospheric** | Between heliospheric coordinate systems (HCI, HAE, HEE, Carrington, Stonyhurst, RTN) | Solar wind data, heliospheric modeling, inner heliosphere |
| **Ionospheric** | Between ionospheric coordinate systems (AACGM, MLT, magnetic latitude, apex coordinates) | `aacgmv2`, magnetic local time, auroral research, ionospheric models |
| **Magnetospheric** | Between magnetospheric coordinate systems (GSE, GSM, SM, GEO, MAG) | `spacepy.coordinates`, `geopack`, magnetosphere modeling |
| **Mission-Specific** | Using spacecraft-specific frames (instrument pointing, attitude, FOV) | `spiceypy`, SPICE kernels, instrument alignment |
| **Planetary** | Between planetary coordinate systems (non-Earth) | Planetary body references, Jupiter/Saturn/Mars coordinates |
| **Solar** | Between solar coordinate systems (Carrington, Stonyhurst, helioprojective, heliographic) | `sunpy.coordinates`, solar disk coordinates, solar features |

---

### 2. Data Processing and Analysis

**What it means:** Software that reads, transforms, processes, or analyzes scientific data.

**Key indicators:**
- Data reading/writing functions
- Mathematical operations on scientific datasets
- Statistical analysis, signal processing
- Filtering, interpolation, curve fitting

**Subcategories and when to use them:**

| Subcategory | What it means | Typical indicators |
|---|---|---|
| **2D Slices** | Extracting 2D cross-sections from 3D data volumes | Slice extraction, plane cuts, volumetric data sampling |
| **3D Particle Distribution Processing** | Processing velocity distribution functions | Distribution function math, velocity space operations, phase space density |
| **Analysis** | General scientific analysis beyond basic processing | Statistical methods, derived physical quantities, scientific calculations |
| **Calibration** | Converting raw instrument data to physical units | Calibration files, response functions, gain corrections, flat-fielding |
| **Curlometer** | Computing curl of B from multi-spacecraft data | Multi-point analysis, Cluster/MMS, `curl` calculations on tetrahedra |
| **Data Access and Retrieval** | Downloading or querying data from remote archives | API clients, `sunpy.net.Fido`, `astroquery`, CDAWeb/HAPI clients |
| **Data Assimilation** | Combining observations with models | Assimilation algorithms, Kalman filters on geophysical data |
| **Data Reduction** | Reducing data volume preserving information | Averaging, binning, downsampling, filtering for noise reduction |
| **Energy Spectra** | Computing or analyzing energy spectra | Spectral calculations, energy channels, flux vs energy |
| **Field-line Tracing** | Tracing magnetic or electric field lines through data | Field line integration, `pfsspy`, streamline tracing |
| **File Format Conversion** | Converting between data file formats | Reading one format, writing another |
| **Image Processing** | Processing 2D image data scientifically | Deconvolution, feature detection, `scikit-image`, solar image processing |
| **Linear Gradient Estimation** | Estimating spatial gradients from multi-point data | Gradient calculations, multi-spacecraft spatial analysis |
| **Magnetic Null Finding** | Locating magnetic null points | Null point detection, magnetic topology analysis |
| **ML/AI** | Machine learning applied to data analysis | `tensorflow`, `pytorch`, `scikit-learn` for scientific analysis tasks |
| **Packet Decommutation** | Parsing raw telemetry packets into usable data | Binary packet parsing, CCSDS, telemetry stream processing |
| **Pitch Angle Distributions** | Computing particle pitch angle distributions | PAD calculations, magnetic field-aligned distributions |
| **Plasma Moments** | Computing density, velocity, temperature, pressure from distributions | Moment integration, distribution function → bulk quantities |
| **Processing** | General data processing (pipeline steps, transforms) | Data pipeline operations, transformation chains |
| **Spectrogram** | Computing time-frequency representations | FFT, STFT, wavelet transforms producing time-frequency arrays |
| **Time Series Analysis** | Analysis of time-ordered data | Temporal filtering, trend analysis, autocorrelation, `pandas` time series |
| **Wave Polarization Analysis** | Analyzing wave polarization properties | Stokes parameters, polarization ellipse, wave analysis methods |
| **Wavelet Analysis** | Wavelet-based signal analysis | Wavelet transforms, `pycwt`, wavelet coherence, scalograms |

---

### 3. Data Visualization

**What it means:** Software that creates visual representations of scientific data.

**Key indicators:**
- `matplotlib`, `plotly`, `bokeh`, `vtk` imports
- Plot/figure generation functions
- Rendering, display, or animation functions

**Subcategories and when to use them:**

| Subcategory | What it means | Typical indicators |
|---|---|---|
| **2D Graphics** | Static 2D plots (contour, heatmap, image) | `pcolormesh`, `imshow`, contour plots, 2D maps |
| **2D Slices** | Visualizing 2D slices of 3D data | Slice display, cut-plane visualization |
| **3D Graphics** | 3D visualizations | `mplot3d`, `vtk`, `mayavi`, volume rendering |
| **Hodograms** | Plotting field component vs component | Hodogram functions, B-field component plots |
| **Line Plots** | Time series or 1D line plots | `plt.plot`, line charts, time series display |
| **Mission-Specific** | Visualizations unique to a mission's data types | Custom instrument-specific plot formats |
| **ML/AI** | ML-related visualizations | Model output display, feature importance |
| **Movies** | Animations or video from data sequences | `matplotlib.animation`, frame generation, movie export |
| **Orbit Plots** | Spacecraft or object trajectory visualization | Orbital path display, trajectory plots |
| **Spacecraft Formation Plots** | Multi-spacecraft configuration display | Constellation geometry, tetrahedron quality |
| **Spectrogram** | Displaying spectrograms | Dynamic spectra display, time-frequency image plots |
| **Web-Based** | Interactive browser-based visualizations | `plotly`, `bokeh`, `dash`, web dashboards |

---

### 4. Mission-related

**What it means:** Software specifically designed to support a space mission's operations or data pipeline. This is distinct from general-purpose analysis software that happens to work with mission data.

**Key distinction:** A package that *reads* MMS data is "Data Processing and Analysis:Data Access and Retrieval". A package that is *part of the MMS ground system* is "Mission-related".

**Subcategories:** Analysis, Archive, Calibration, Distribution/Access, Infrastructure as Code, Ingest, Instrumentation, Instrument Response, Inventory, ML/AI, Monitoring, Observatory/Instrument Models, Operations, Orchestration, Packet Decommutation, Processing, Science Data Processing, System Testing

---

### 5. Models and Simulations

**What it means:** Software that models physical systems or runs simulations.

**Key indicators:**
- Numerical solvers (ODE/PDE integrators)
- Physical model implementations (empirical or first-principles)
- Simulation frameworks
- Forward modeling or synthetic data generation

**Subcategories and when to use them:**

| Subcategory | What it means | Typical indicators |
|---|---|---|
| **Data Guided** | Models driven by observational data | Data-driven boundaries, observational inputs |
| **Empirical** | Statistical/empirical models | Empirical formulas, climatological models (IRI, MSIS, HWM, IGRF) |
| **Field-line Tracing** | Tracing field lines in model fields | PFSS, potential field extrapolation |
| **First Principles** | Models from fundamental physics | Full MHD equations, kinetic theory, ab initio |
| **Forecasting** | Prediction/nowcasting | Space weather prediction, forecast output |
| **Forward-Fitting** | Synthetic data + parameter optimization | Forward model, chi-square fitting, inversion |
| **Instrument Response** | Modeling instrument behavior | Response matrix, effective area, PSF simulation |
| **MHD** | Magnetohydrodynamic simulations | MHD solver, BATSRUS, Athena, Pencil Code |
| **Mission-Specific** | Models for a specific mission | Spacecraft-specific modeling |
| **ML/AI** | ML-based models | Neural network predictions, surrogate models |
| **Observatory/Instrument Models** | Modeling observatories or instruments | Instrument simulation, synthetic observations |
| **Physics-Based** | Physics-based (broader than first principles) | Physical equations, semi-empirical physics |
| **Theory** | Analytical/theoretical calculations | Analytical solutions, theoretical frameworks |

---

### 6. Servers and Environments

**What it means:** Infrastructure, deployment, and runtime environment software.

**Subcategories:** Data servers processing and handling, Distribution/Access, High Performance Computing, Infrastructure as Code, Software or Environment Container

**Key indicators:** Server implementations, Dockerfiles, MPI/parallel computing, HPC job scripts, Kubernetes manifests, data serving endpoints

---

## Common Library-to-Functionality Mappings

These mappings are **indicators**, not guarantees. Always verify the software actually exposes the functionality to users.

| Library / Import | Likely Functionality |
|---|---|
| `sunpy.coordinates` | Coordinate Transforms, Coordinate Transforms:Solar |
| `astropy.coordinates` | Coordinate Transforms |
| `aacgmv2` | Coordinate Transforms:Ionospheric |
| `spacepy.coordinates` | Coordinate Transforms:Magnetospheric |
| `spiceypy` | Coordinate Transforms:Mission-Specific |
| `geopack` | Coordinate Transforms:Magnetospheric |
| `sunpy.net`, `sunpy.net.Fido` | Data Processing and Analysis:Data Access and Retrieval |
| `astroquery` | Data Processing and Analysis:Data Access and Retrieval |
| `hapiclient` | Data Processing and Analysis:Data Access and Retrieval |
| `cdflib`, `spacepy.pycdf` | Data Processing and Analysis (file I/O) |
| `astropy.io.fits` | Data Processing and Analysis (FITS file I/O) |
| `h5py` | Data Processing and Analysis (HDF5 file I/O) |
| `matplotlib` | Data Visualization |
| `matplotlib.animation` | Data Visualization:Movies |
| `plotly`, `bokeh` | Data Visualization:Web-Based |
| `vtk`, `mayavi`, `pyvista` | Data Visualization:3D Graphics |
| `scikit-image`, `skimage` | Data Processing and Analysis:Image Processing |
| `scipy.signal` | Data Processing and Analysis:Time Series Analysis |
| `pycwt` | Data Processing and Analysis:Wavelet Analysis |
| `tensorflow`, `pytorch`, `sklearn` | ML/AI (under whichever parent category applies) |
| `pfsspy` | Models and Simulations:Field-line Tracing |
| `Docker`, `Singularity` | Servers and Environments:Software or Environment Container |
| `mpi4py` | Servers and Environments:High Performance Computing |

---

## Decision Rules

1. **Always include the parent category** when selecting any subcategory.

2. **Be exhaustive.** If a package does data access AND visualization AND coordinate transforms, list all three with all relevant subcategories. The most common validator finding is *missing* functionalities.

3. **Don't over-classify.** Only include a functionality if the software actually implements it. Importing `matplotlib` doesn't mean "3D Graphics" unless it actually generates 3D plots.

4. **Distinguish "uses internally" from "provides to users."** A package that internally converts coordinates as a utility step doesn't necessarily need "Coordinate Transforms" listed — only if coordinate transformation is a user-facing capability. However, if the user can access or benefit from the transform (even indirectly), err on the side of inclusion.

5. **Distinguish processing from visualization.** Computing a spectrogram is "Data Processing and Analysis:Spectrogram". Displaying a spectrogram is "Data Visualization:Spectrogram". Many packages do both — list both.

6. **Read the tests and examples.** They often reveal functionality not mentioned in the README. A test file named `test_spectrogram.py` is a strong signal.

7. **Check submodule/directory names.** A directory called `coordinates/` or `visualization/` is a strong structural signal.

8. **Look at CLI entry points and public API.** What functions are exported? What does `__init__.py` expose? These are the user-facing capabilities.

---

## Common Mistakes

| Mistake | Why it happens | How to avoid |
|---|---|---|
| Missing subcategories | Listed "Data Visualization" but didn't identify specific types | Check each subcategory against the code |
| Missing parent categories | Listed "Data Visualization:Spectrogram" without "Data Visualization" | Always add parent when adding subcategory |
| Overlooking Data Access | Data downloading is seen as "utility" not "functionality" | If users call a function to get data, it's Data Access |
| Confusing processing and visualization | Spectrogram computation vs display | Check if the code produces arrays (processing) or figures (visualization) |
| Ignoring coordinate transforms | Packages do transforms as part of workflow without advertising it | Search for coordinate system names and transform functions |
| Under-classifying models | A model that's physics-based AND MHD AND forecasting | Check if multiple model subcategories apply |
| Classifying dependencies as features | Package imports `astropy.coordinates` but users never do transforms | Only classify user-facing capabilities |
| Missing "Data Processing and Analysis:Analysis" | Catch-all subcategory is easy to forget | If the package does any scientific analysis, this likely applies |

---

## Validation Checklist

When validating an existing Software Functionality classification:

- [ ] Every listed value is from the allowed list (exact string match)
- [ ] Every subcategory has its parent category also listed
- [ ] No parent category is listed without at least considering its subcategories
- [ ] Package README claims are reflected in the classification
- [ ] Code structure (directories, modules) is reflected in the classification
- [ ] Test files and examples don't reveal unclassified functionality
- [ ] Import statements in the package don't suggest missing functionality
- [ ] The classification is defensible — each entry can be justified with specific code evidence
