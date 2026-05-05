# HSSI Metadata Extraction Results

**Repository:** https://github.com/punch-mission/solpolpy
**Extraction Date:** 2026-04-15
**Status:** Incomplete - software functionality only

---

## Section 1: Basic Information

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Mission-Specific
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Mission-related
- Mission-related: Science Data Processing

**Source:** README.md describes solpolpy as a solar polarization resolver that converts observation triplets in the MZP convention to polarization brightness, total brightness, and Stokes I/Q/U. docs/source/index.rst says the package transforms between polarization systems in solar physics and heliophysics and was developed as part of the PUNCH mission. docs/source/quickstart.rst documents `resolve` and `load_data`, PUNCH WFI/IMAX polarizer-angle foreshortening correction, and plotting of input/output collections. solpolpy/core.py exposes `resolve` for conversions among mzpsolar, mzpinstru, btbr, stokes, bpb, bp3, bthp, fourpol, and npol image products. solpolpy/transforms.py implements the scientific transformations, including MZP to B/pB, MZP to Stokes, B/pB/pB-prime to brightness/theta/degree of polarization, arbitrary-angle polarizer conversion, and MZP solar-frame/instrument-frame conversion using WCS-derived solar-north angles and instrument polarizer offsets. solpolpy/instruments.py loads FITS image triplets into NDCollection objects with WCS/header metadata and constructs instrument/coronagraph masks, including a PUNCH HDU note and LASCO/COSMO/SECCHI mask support. solpolpy/util.py provides WCS-based solar-north computation, optical-distortion pixel shift utilities, and NDCollection-to-SunPy-Map conversion. solpolpy/plotting.py exposes WCS-aware 2D plotting and RGB image generation for MZP triplets with radial image-enhancement methods. tests/test_core.py, tests/test_transforms.py, tests/test_instruments.py, and tests/test_plotting.py exercise the supported polarization systems, transformation paths, FITS loading/masking, plotting, and RGB image generation.
