# HSSI Metadata Extraction Results

**Repository:** https://github.com/dpq/python-magnetosphere
**Extraction Date:** 2026-04-14
**Status:** Incomplete - software functionality only

---

## Section 1: Basic Information

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Field-line Tracing
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing

**Source:** Local source review of `/Users/shpo9723/git/hssi-claude-agents/repos/python-magnetosphere`. The `magnetosphere.cxform` extension exposes `transform(from, to, x, y, z, year, month, day, hour, minute, second)` for converting between space-physics coordinate systems. The README and `cxform-manual.c` list magnetospheric/geocentric frames including GEI, J2000, GEO, MAG, GSE, GSM, and SM, plus heliospheric/heliocentric frames including RTN, GSEQ, HEE, HAE, and HEEQ. The `magnetosphere.igrf` extension exposes IGRF-based magnetic-field, dipole-moment, L-shell, field-intensity, and minimum-field-on-a-field-line calculations through `dimo`, `lb`, `b`, and `b0`. The `magnetosphere.rigidity` extension exposes cutoff-rigidity calculations, including IGRF-based and Kp/local-time corrected cutoff rigidity. These are user-facing scientific analysis/model calculations using empirical geomagnetic field models, with explicit field-line tracing support in `igrf.b0`.
