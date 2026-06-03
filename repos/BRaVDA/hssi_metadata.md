# HSSI Metadata Extraction Results

**Repository:** https://github.com/University-of-Reading-Space-Science/BRaVDA
**Extraction Date:** 2026-06-01

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.4849681

*Source: Version-independent concept DOI (Zenodo `conceptdoi`, confirmed via DataCite/Zenodo APIs). The README Zenodo badge points to the v1.9 versioned DOI https://doi.org/10.5281/zenodo.7892408 (recorded under Field 12, Version PID).*

### 3. Code Repository (MANDATORY)
https://github.com/University-of-Reading-Space-Science/BRaVDA

*Source: git remote `origin`.*

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Data Assimilation
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Data Access and Retrieval
- Data Visualization
- Data Visualization:Line Plots
- Data Visualization:2D Graphics
- Models and Simulations
- Models and Simulations:Forecasting
- Models and Simulations:Data Guided
- Models and Simulations:Physics-Based

*Source: Manual examination of `runBravdaExport.py`, `bravdaMethodsExport.py`, `BRaVDA_wrappers.py`, and `makeMASens/`.*
- *Data Assimilation (core capability): variational (4D-Var-style) DA combining coronal model output (WSA/MAS) with in-situ observations via BFGS cost-function minimization (`calcCostFuncForCGNoLat`, `makeGradCGNoLat`, `scipy.optimize.minimize`).*
- *Analysis: computes RMSE diagnostics and prior/posterior/analysis error covariance matrices (`calcStateObsRMSE`, covariance traces).*
- *Time Series Analysis: assimilation is structured around 27-day temporal windows; reads and time-averages observations over configurable MJD windows (`readObsFileAvg`, `makeMJDfile`) and produces per-window solar wind speed time series (`vPriorAll`/`vPosteriorAll`).*
- *Processing: builds observation operators, error covariance matrices, MAS/WSA prior ensembles, and packs/reshapes data through the assimilation pipeline.*
- *Data Access and Retrieval: downloads MAS coronal boundary conditions from PredSci MHDweb (`makeMASens/downMASfc.py`: `getMASboundaryconditions`, `httplib2`, `urllib.request`).*
- *Line Plots: solar wind speed time-series plots over 27-day windows at observation locations (`plotSWspeed`, `ax.plot`/`savefig`, `bravdaMethodsExport.py` ~L1451-1546).*
- *2D Graphics: a `plt.contourf` plot of the posterior analysis error covariance matrix (`bravdaMethodsExport.py` L402).*
- *Forecasting: README/papers describe BRaVDA as a solar wind forecasting tool ("Improving solar wind forecasting using data assimilation"); output drives HUXt forecasts.*
- *Data Guided: the model state is driven/constrained by in-situ observations.*
- *Physics-Based: implements the HUX kinematic solar wind propagation model (`forwardRadModelNoLat`, solar rotation, residual acceleration).*

### 5. Related Region (MANDATORY)
- Solar Environment
- Interplanetary Space

*Source: BRaVDA assimilates coronal model (WSA/MAS) output at the inner heliospheric boundary (~21.5-30 solar radii; Solar Environment) and propagates/reconstructs the ambient solar wind through the heliosphere out to ~1 AU, assimilating in-situ observations from ACE/OMNI, STEREO-A, and STEREO-B (Interplanetary Space).*

### 6. Authors (MANDATORY)
- **Author:** Matthew Lang
  - **Author Identifier:** https://orcid.org/0000-0002-1904-3700
  - **Affiliation:**
    - **Organization:** University of Reading
      - **Affiliation Identifier:** https://ror.org/05v62cm79
- **Author:** Mathew J. Owens
  - **Author Identifier:** https://orcid.org/0000-0003-2061-2453
  - **Affiliation:**
    - **Organization:** University of Reading
      - **Affiliation Identifier:** https://ror.org/05v62cm79

*Source: Zenodo/DataCite list only Matthew Lang as creator (sole creator of the archived record and lead author of both reference papers; repository contact). Mathew J. Owens added from the README "Contact" section, code authorship header (`BRaVDA_wrappers.py` header `@author: mathewjowens`), and reference-paper co-authorship. ORCIDs and affiliations enriched via Crossref (DOIs 10.1029/2018SW001857 and 10.1029/2020SW002698, "Department of Meteorology, University of Reading, Reading, UK"). University of Reading ROR https://ror.org/05v62cm79.*

### 7. Software Name (MANDATORY)
BRaVDA

*Source: README title ("BRaVDA - a solar wind data assimilation scheme"), repository name, and Zenodo title. The full expansion is not formally spelled out anywhere in the repository; only the acronym "BRaVDA" is used throughout the codebase and Zenodo record.*

### 8. Description (MANDATORY)
BRaVDA is a Python implementation of a variational data assimilation scheme for the ambient solar wind. It combines the output of a coronal model (such as WSA or MAS) with in-situ solar wind speed observations near 1 AU (e.g. ACE/OMNI, STEREO-A, STEREO-B) and returns an optimal reconstruction of the ambient solar wind, accounting for errors in both the model and the observations. BRaVDA propagates the inner-boundary solar wind speed through the heliosphere using the HUX kinematic propagation model, generates a prior ensemble from WSA/MAS Carrington maps, and minimizes a variational (4D-Var-style) cost function with a BFGS optimizer to produce posterior solar wind estimates together with their error covariances. The assimilation is organized around 27-day (Carrington-rotation) windows, and the resulting posterior solar wind state can be used to drive the HUXt model for solar wind forecasting. BRaVDA implements the method described in Lang & Owens (2019) and used operationally in Turner et al. (2023).

*Source: Synthesized from README, `runBravdaExport.py`, `BRaVDA_wrappers.py`, and the reference papers. The version-specific Zenodo abstract (Turner et al. 2023 results) was not used as the general description.*

### 9. Concise Description (OPTIONAL)
Python variational data assimilation scheme that combines a coronal model (WSA/MAS) with in-situ solar wind observations to reconstruct and forecast the ambient solar wind near 1 AU.

*Source: Condensed from the Description (≤200 characters) to provide a clean preview.*

### 10. Publication Date (RECOMMENDED)
2021-05-30

*Source: Concept DOI registration date (Zenodo 4849681), confirmed via DataCite (`"created": "2021-05-30T..."`), corresponding to the first release.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

*Source: DataCite/Zenodo metadata (publisher of the archived software DOI; GitHub-Zenodo release workflow).*

### 12. Version (RECOMMENDED)
- **Version Number:** v1.9
- **Version Date:** 2023-05-03
- **Version Description:** Latest published release on Zenodo/GitHub (BRaVDA v1.9), associated with the Turner et al. (2023) operational study. (No CHANGELOG present in the repository.)
- **Version PID:** https://doi.org/10.5281/zenodo.7892408

*Source: Zenodo/DataCite (`version: v1.9`) and GitHub latest release (BRaVDA v1.9, published 2023-05-03). No git tags exist in the local clone (single squashed commit).*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source: GitHub reports Python 100%. README states "written in Python 3.9.13"; `bravda_env.yml` pins Python 3.10.*

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1029/2018SW001857

*Lang, M., & Owens, M. J. (2019). A variational approach to data assimilation in the solar wind. Space Weather, 17, 59-83. Source: README "Citations" section identifies this as the paper describing the scientific basis and functionality of BRaVDA (the primary methodology reference). The 2021 Lang et al. forecasting paper is recorded under Related Publications (Field 27).*

### 15. License (RECOMMENDED)
Not found

*Source: No LICENSE/LICENSE.txt file in the repository, no license headers in source files, and the GitHub "About" sidebar shows no license. The Zenodo record reports license id "other-open" (Zenodo's default open-access placeholder), which is not a specific reusable license and should not be treated as a confirmed license. License genuinely absent from the repository - flag for the maintainers to clarify.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- solar wind
- data assimilation
- variational data assimilation
- space weather
- solar wind forecasting
- HUX
- WSA
- MAS
- coronal model
- heliosphere
- ensemble
- python

*Source: Derived from README, reference papers, and code. No keywords present in Zenodo metadata.*

### 17. Data Sources (OPTIONAL)
- HTTP/HTTPS Directories
- OMNIWeb
- Observatory/Mission-specific

*Source: `makeMASens/downMASfc.py` downloads MAS coronal boundary conditions over HTTP from PredSci MHDweb (`http://www.predsci.com/data/runs/...`) - HTTP/HTTPS Directories. Bundled observation streams include OMNI data (`Obs/ObservationFiles/OMNI_observations.txt`) - OMNIWeb; and spacecraft/mission-specific in-situ data: ACE real-time SWEPAM (`Obs/ACE_RealTime/`), STEREO-A/STEREO-B (`Obs/ObservationFiles/`), plus WSA maps (`wsa.gong.fits`) and per-body ephemeris lists - Observatory/Mission-specific.*

### 18. Input File Formats (RECOMMENDED)
- ascii
- FITS
- HDF5
- csv
- Other

*Source: Code examination. ascii: configuration, observation, ensemble, and MJD `.dat`/`.txt` files read via `open(...,'r')`/`np.loadtxt` (`runBravdaExport.py`, `bravdaMethodsExport.py`). FITS: WSA Carrington maps read via `astropy.io.fits` (`BRaVDA_wrappers.py` `fits.open`). HDF5: spacecraft ephemeris `makeMASens/ephemerisMSL.hdf5` and MAS velocity ensembles read via `h5py` (`makeMASens/helioMASens.py`). csv: Carrington-rotation MJD-start table (`Obs/CR_MJD/2000_2300CRMJDstartV2.csv`). Other: downloaded MAS boundary files are HDF4 `.hdf` read via `pyhdf.SD` (`makeMASens/downMASfc.py`), and MAVEN magnetometer `.sts` STS files - neither is in the allowed list.*

### 19. Output File Formats (RECOMMENDED)
- ascii
- Other

*Source: Code examination. ascii: `runBravdaExport.py` writes `inputs.dat`, observation/ensemble/prior/posterior solar wind files, posterior covariance matrices, and MJD files via `np.savetxt` (`.dat`); `BRaVDA_wrappers.py` writes the HUXt-derived `customensemble.dat`. Other: time-series plots are saved as PDF via `plt.savefig(...pdf)` (`bravdaMethodsExport.py` ~L1490, L1545), and PDF is not in the allowed list.*

### 20. Operating System (RECOMMENDED)
- Operating System Independent

*Source: Pure-Python conda environment (`bravda_env.yml`), no OS-specific code or CI configuration. README documents conda/Anaconda setup; cross-platform.*

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

*Source: Pure-Python (NumPy/SciPy/Astropy/Matplotlib) workflow with no architecture-specific code, build steps, or compiled extensions; no CI matrix specifying architectures.*

### 22. Related Phenomena (OPTIONAL)
- Solar wind

*Source: BRaVDA reconstructs/forecasts the ambient (corotating/background) solar wind speed. No CME/flare/specific transient modeling found. "Solar wind" is the primary phenomenon but is not a strictly controlled-vocabulary match in the allowed list - flag for reviewer.*

### 23. Development Status (RECOMMENDED)
Active

*Source: Inferred. Software actively used in recent publications (Turner et al. 2023) with wrappers updated for HUXt integration (`BRaVDA_wrappers.py`, 2023). No formal repostatus.org badge in the repository.*

### 24. Documentation (RECOMMENDED)
https://github.com/University-of-Reading-Space-Science/BRaVDA/blob/main/README.md

*Source: No external documentation site (no docs/ folder, no Read the Docs config). The README covers introduction, installation, contact, and citations. Function-level docstrings exist in `BRaVDA_wrappers.py` and `makeMASens/`.*

### 25. Funder (OPTIONAL)
- **Organization:** Science and Technology Facilities Council
  - **Funder Identifier:** https://ror.org/057g20z61
- **Organization:** Natural Environment Research Council
  - **Funder Identifier:** https://ror.org/02b5d8509

*Source: Crossref funding metadata for the BRaVDA papers. STFC (ROR 057g20z61 / Funder DOI 10.13039/501100000271) funds the reference publication describing the software (Lang & Owens 2019) and its follow-up (Lang et al. 2021). NERC (ROR 02b5d8509 / Funder DOI 10.13039/501100000270) funds the operational study using BRaVDA (Turner et al. 2023). Not stated in the repository or Zenodo/DataCite metadata; attributed from the reference/related publications.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
  - **Award Number:** ST/M000885/1
- **Award Title:** Not found
  - **Award Number:** ST/R000921/1

*Source: Crossref funding metadata. ST/M000885/1 (STFC) is the grant on the reference publication (Lang & Owens 2019, 10.1029/2018SW001857); ST/R000921/1 (STFC) is on the follow-up development paper (Lang et al. 2021, 10.1029/2020SW002698). The operational Turner et al. (2023) paper additionally lists NERC NE/S007261/1 and STFC ST/V000497/1 and ST/V00235X/1, which relate to that study rather than the original software development. Crossref provides award numbers only, not titles; submitter should add titles if known.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1029/2020SW002698 — Lang, M., Witherington, J., Turner, H., Owens, M. J., & Riley, P. (2021). Improving solar wind forecasting using data assimilation. Space Weather, 19, e2020SW002698. *(Second citation reference from README.)*
- https://doi.org/10.1029/2023SW003457 — Turner, H., Lang, M., Owens, M., Smith, A., Riley, P., Marsh, M., & Gonzi, S. (2023). Solar wind data assimilation in an operational context: Use of near-real-time data and the forecast value of an L5 monitor. Space Weather, 21, e2023SW003457. *(Referenced in the Zenodo v1.9 abstract; DOI confirmed via Crossref.)*

*Source: README "Citations" section and Zenodo v1.9 record. The Lang & Owens (2019) paper is recorded separately as the Reference Publication (Field 14).*

### 28. Related Datasets (OPTIONAL)
- MAS coronal model boundary conditions (Predictive Science Inc. MHDweb, http://www.predsci.com) — downloaded at runtime by `makeMASens/downMASfc.py`.
- WSA coronal maps (FITS) — input to `BRaVDA_wrappers.readWSA`.
- In-situ solar wind observations: ACE/OMNI, STEREO-A, STEREO-B (bundled sample files in `Obs/ObservationFiles/` and `Obs/ACE_RealTime/`).

*Source: Code and bundled data. No formal dataset DOIs exist; these are the data sources the software consumes.*

### 29. Related Software (OPTIONAL)
- https://github.com/University-of-Reading-Space-Science/HUXt — HUXt heliospheric solar wind propagation model; `BRaVDA_wrappers.py` imports `huxt`, `huxt_inputs`, `huxt_analysis`, `huxt_ensembles`, and BRaVDA output drives HUXt.
- http://www.predsci.com/mhdweb/ — MAS (Magnetohydrodynamics Around a Sphere) coronal model providing inner-boundary inputs.
- WSA (Wang-Sheeley-Arge) coronal model — provides inner-boundary inputs (FITS maps).
- https://github.com/sunpy/sunpy — SunPy (runtime dependency).
- https://github.com/astropy/astropy — Astropy (runtime dependency; FITS I/O).
- SciPy, NumPy, pandas, Matplotlib, cdflib, h5py, pyhdf — additional runtime dependencies (`bravda_env.yml`).

*Source: `BRaVDA_wrappers.py` imports and `bravda_env.yml`.*

### 30. Interoperable Software (OPTIONAL)
- https://github.com/University-of-Reading-Space-Science/HUXt — HUXt

*Source: `BRaVDA_wrappers.py` demonstrates a direct integration in which BRaVDA runs in the same environment as HUXt: it imports HUXt modules, builds HUXt input ensembles, runs BRaVDA assimilation, and feeds the posterior solar wind back to drive HUXt. This is a demonstrated interoperability (beyond a mere dependency).*

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** SWEPAM (Solar Wind Electron Proton Alpha Monitor, on ACE)
- **Instrument Name:** PLASTIC (PLAsma and SupraThermal Ion Composition, on STEREO)

*Source: Assimilated in-situ solar wind speed observations: ACE/SWEPAM (`Obs/ACE_RealTime/*_ace_swepam_1h.txt`) and STEREO-A/B plasma instruments (`Obs/ObservationFiles/STEREO-A_observations.txt`, `STEREO-B_observations.txt`). OMNI is a merged near-Earth product rather than a single instrument. Per-body ephemeris `.lst` files exist for PSP, Solar Orbiter, BepiColombo, MAVEN, etc., but these are spacecraft position tables for the assimilation grid, not observation inputs - so those missions are not listed as instruments/observatories.*

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** ACE (Advanced Composition Explorer)
- **Observatory Name:** STEREO-A (Solar Terrestrial Relations Observatory Ahead)
- **Observatory Name:** STEREO-B (Solar Terrestrial Relations Observatory Behind)

*Source: Sources of the assimilated in-situ solar wind observations (`obsFile.dat`, `Obs/AbsLocFiles/`, and bundled observation files). OMNIWeb provides the near-Earth merged product. PredSci MHDweb is a data archive, not an observatory.*

### 33. Logo (OPTIONAL)
Not found

*Source: No logo file in the repository, no logo referenced in the README or Zenodo metadata.*
