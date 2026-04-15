# HSSI Metadata Extraction Results

**Repository:** https://github.com/DKISTDC/dkist
**Extraction Date:** 2026-04-14
**Status:** Incomplete - software functionality only

---

## Section 1: Basic Information

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Mission-Specific
- Coordinate Transforms: Solar
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Mission-related
- Mission-related: Distribution/Access
- Mission-related: Inventory

**Source:** Local source review of `/Users/shpo9723/git/hssi-codex-agents/repos/dkist`. The README describes DKIST User Tools as a Python library for obtaining, processing, and interacting with DKIST data. The user tools guide says the package is developed by the DKIST Data Center team and provides a DKIST-specific `ndcube.NDCube` subclass, DKIST ASDF schema support, FITS header access, a `sunpy.net.Fido` client for searching the DKIST Data Center, and Globus-based file transfer helpers. `dkist.net.DKISTClient.search()` and `.fetch()` query DKIST dataset inventory and fetch ASDF metadata, while `dkist.io.DKISTFileManager.download()`, `.quality_report()`, and `.preview_movie()` retrieve FITS data, quality reports, and preview movies from DKIST services. `dkist.Dataset` and `dkist.TiledDataset` load DKIST Level 1 ASDF/FITS products, expose FITS headers, inventory records, dask-backed arrays, and gWCS coordinate information, and preserve file/header metadata when slicing. The DKIST search `BoundingBox` attribute transforms supported coordinates into helioprojective coordinates, and the WCS model code creates DKIST celestial transforms used by DKIST datasets. Tutorials and examples show users slicing multidimensional DKIST datasets to smaller science products, reducing data with `rebin`, computing derived quantities with dask/numpy methods, inspecting seeing and quality metadata, plotting 2D slices and tiled mosaics, and making line plots of spectra in DKIST-specific visualizations. Mission-related categories are limited to DKIST Data Center distribution/access and inventory metadata because the package is a client/user-tools library rather than the archive infrastructure, calibration pipeline, or mission science-processing pipeline.
