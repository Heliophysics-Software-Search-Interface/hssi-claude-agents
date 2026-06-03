# HSSI Metadata Extraction Results

**Repository:** https://github.com/helioforecast/Papers/tree/master/Bailey2021_AmbSoWiML
**Extraction Date:** 2026-06-01

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
Not found — no software DOI/concept DOI (no Zenodo integration, no CITATION.cff, no badges) for this subdirectory. (A reference-publication DOI exists; see Field 14.)

### 3. Code Repository (MANDATORY)
https://github.com/bairaelyn/ambsowi-ml

*Source: The README points to https://github.com/bairaelyn/ambsowi-ml as the original standalone author repository (and as the canonical source of the LICENSE), so it is used here as the primary code repository. The code was also archived into the helioforecast/Papers monorepo subdirectory (https://github.com/helioforecast/Papers/tree/master/Bailey2021_AmbSoWiML), which is the copy that was extracted; that monorepo location is listed under Related Software (Field 29).*

### 4. Software Functionality (MANDATORY)
- Data Processing and Analysis
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Data Reduction
- Data Processing and Analysis:ML/AI
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Time Series Analysis
- Models and Simulations
- Models and Simulations:Forecasting
- Models and Simulations:ML/AI
- Data Visualization
- Data Visualization:Line Plots
- Data Visualization:2D Graphics
- Data Visualization:ML/AI

*Source: Manual examination of ambsowi_forecast_ML.ipynb and environment.yml. The notebook trains an XGBoost Gradient Boosting Regressor (xgboost, scikit-learn) to predict (forecast) ambient solar wind speed at Earth from coronal-magnetic-model features (flux tube expansion factor, distance to coronal hole boundary) — an ML-based forecasting model (Models and Simulations:Forecasting/ML/AI). It retrieves observed near-Earth solar wind via predstorm (`ps.get_omni_data`, `ps.get_icme_catalogue`) — Data Access and Retrieval — and prepares the inputs by packing into DataFrames, creating lagged/shifted time-series features, and normalizing (Processing). It processes daily/3.64-hour-resolution time series via pandas date-indexed DataFrames, lagged/shifted feature construction, and temporal train/test windowing (Time Series Analysis), masks out ICME intervals to NaN to clean the training signal (Data Reduction), and computes statistical analysis incl. feature importances and RMSE/Pearson correlations (Analysis, ML/AI). It produces line plots of predicted vs. observed solar wind (Line Plots), 2D Carrington-rotation speed image maps / WSA variable maps via matplotlib (2D Graphics), and feature-importance plots (ML/AI visualization). Note: Models and Simulations:Empirical was considered but removed — the model is ML-based (XGBoost), not a traditional statistical/empirical model in the space-physics sense; the WSA-formula baseline is only a secondary comparison.*

### 5. Related Region (MANDATORY)
- Solar Environment
- Interplanetary Space

*Source: The software predicts the ambient solar wind originating from coronal magnetic field structures (Solar Environment) as it propagates and is observed at Earth/L1 in the heliosphere (Interplanetary Space).*

### 6. Authors (MANDATORY)
- **Author:** R. L. Bailey
  - **Author Identifier:** https://orcid.org/0000-0003-2021-6557 *(ORCID from the reference publication, Crossref; same author "R. L. Bailey" named in README/notebook)*
  - **Affiliation:**
    - **Organization:** Space Research Institute, Austrian Academy of Sciences *(README/notebook: "IWF Graz" = Institut für Weltraumforschung, Österreichische Akademie der Wissenschaften)*
      - **Affiliation Identifier:** https://ror.org/002w0jp71 *(Space Research Institute / IWF, Austrian Academy of Sciences; confirmed via ROR v2 API — acronym "IWF", Austria)*
    - **Organization:** Central Institute for Meteorology and Geodynamics (Zentralanstalt für Meteorologie und Geodynamik) *(README/notebook: "ZAMG Vienna"; Crossref lists "Conrad Observatory, Zentralanstalt für Meteorologie und Geodynamik, Vienna")*
      - **Affiliation Identifier:** https://ror.org/048dqgk17 *(Central Institution for Meteorology and Geodynamics / ZAMG; ROR v2 API. ZAMG merged into GeoSphere Austria (ror.org/0181cy234) in 2023; this predecessor ROR is the correct historical match for the 2019–2020 code.)*
    - **Organization:** NASA Goddard Space Flight Center *(notebook intro: "Code created 2019-2020 at NASA Goddard Space Flight Center, Maryland, USA")*
      - **Affiliation Identifier:** https://ror.org/0171mag52

*Source: README.md ("Author: R. L. Bailey (IWF Graz / ZAMG Vienna), 2019-2020"), notebook intro ("Code created 2019-2020 at NASA Goddard Space Flight Center, Maryland, USA and the Space Research Institute (IWF), Graz, Austria"), and Crossref metadata for the reference publication. R. L. Bailey is the sole software author per the subdirectory README/notebook; the additional names in the paper (M. A. Reiss, C. N. Arge, C. Möstl, C. J. Henney, M. J. Owens, U. V. Amerstorfer, T. Amerstorfer, A. J. Weiss, J. Hinterreiter) are co-authors of the publication, not listed as authors of this code.*

### 7. Software Name (MANDATORY)
Ambient Solar Wind Prediction using Machine Learning (AmbSoWiML)

*Source: README.md title and subdirectory name (Bailey2021_AmbSoWiML); environment name "ambsowiml"; original repo "ambsowi-ml".*

### 8. Description (MANDATORY)
AmbSoWiML is the code accompanying Bailey et al. (2021), "Using Gradient Boosting Regression to Improve Ambient Solar Wind Model Predictions" (Space Weather). It is a Jupyter Notebook that details the training and implementation of a machine-learning method — specifically a Gradient Boosting Regressor (XGBoost) — to predict the ambient solar wind flow speed observed at Earth. The model inputs are variables derived from solar coronal magnetic models (WSA from PFSS/SCS): the flux tube expansion factor and the distance to the coronal hole boundary taken along the sub-Earth point, together with the solar wind speed from one Carrington rotation earlier (persistence). The notebook walks through loading and visualising the coronal-model data, defining an AmbientSolarWind (AmbSoWi) model object, setting up and grid-searching the XGBoost regressor, using feature importances to select optimal features, producing final result plots and error statistics, generating output files for the ISWAT ambient solar wind forecasting team (years 2008 and 2012), and applying the trained model to new data. A pre-trained model (optim_ambsowi_model.pickle) is included so the regressor can be applied to new coronal-model output without retraining. The package is intended as a reproducible, demonstration/research code rather than an installable library.

### 9. Concise Description (OPTIONAL)
Machine-learning (XGBoost Gradient Boosting Regressor) notebook to forecast the ambient solar wind speed at Earth from solar coronal magnetic model features. Code for Bailey et al. (2021).

### 10. Publication Date (RECOMMENDED)
2021-05-01

*Source: Reference publication issue date (2021-05) per Crossref, standardized to the first of the month as no exact day is available. Code created 2019-2020 per notebook. No software release date available — the repository commit was a 2022-02-21 bulk reorganization, not the original publication date.*

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub *(no DOI obtained; repository host)*
- **Publisher Identifier:** https://github.com

### 12. Version (RECOMMENDED)
- **Version Number:** Not found *(no tags, releases, version string, or CHANGELOG for this subdirectory)*
- **Version Date:** Not found
- **Version Description:** Not found
- **Version PID:** Not found

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source: ambsowi_forecast_ML.ipynb (Jupyter/Python), environment.yml (scikit-learn, xgboost, pandas, numpy, scipy, matplotlib, seaborn). Note: the statistical verification step referenced in the README uses an external MATLAB package (OSEA) that is not part of this software.*

### 14. Reference Publication (RECOMMENDED)
https://doi.org/10.1029/2020SW002673

*Bailey, R. L., Reiss, M. A., Arge, C. N., Möstl, C., Henney, C. J., Owens, M. J., et al. (2021). Using gradient boosting regression to improve ambient solar wind model predictions. Space Weather, 19, e2020SW002673. Source: top-level repo README and notebook; DOI confirmed via Crossref.*

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html

*Source: LICENSE file in subdirectory (MIT License, Copyright (c) 2020 R L Bailey).*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- solar wind
- space weather
- machine learning
- gradient boosting
- forecasting
- ambient solar wind
- coronal holes
- WSA model
- flux tube expansion factor
- ISWAT
- python

*Source: README/notebook content and ISWAT ambient solar wind forecasting context.*

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific
- Other

*Source: Input is output from coronal magnetic models (WSA from PFSS/SCS maps provided by C. N. Arge); observed solar wind is obtained via the predstorm package (OMNI/in-situ near-Earth data). The full WSA training data set cannot be shared openly; example/test files are provided.*

### 18. Input File Formats (RECOMMENDED)
- ascii
- Other

*Source: Input data are plain-text/ascii .txt files (e.g., arge_test_excerpt.txt, wsahux_output.txt, CarringtonRotNums.txt, subearth_track_cr2052.txt, cmm_test.txt). The pre-trained model is loaded from a Python pickle (optim_ambsowi_model.pickle) — "Other".*

### 19. Output File Formats (RECOMMENDED)
- csv
- ascii
- Other

*Source: Notebook writes results to csv (results/bailey_ml_vsw_iswat_2008.csv, _2012.csv via DataFrame.to_csv) and ascii .txt prediction files (results/ml_vsw_predictions_*.txt); plots saved as PDF and PNG ("Other"); trained model serialized as pickle ("Other").*

### 20. Operating System (RECOMMENDED)
- Operating System Independent

*Source: Pure-Python/Jupyter conda environment (environment.yml) with cross-platform dependencies; no OS-specific code. No CI configuration present to confirm specific OS testing.*

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

*Source: Pure Python/scikit-learn/XGBoost workflow; no architecture-specific requirements indicated.*

### 22. Related Phenomena (OPTIONAL)
- Coronal Holes
- Solar Corona

*Source: The model uses coronal-hole-boundary distance and coronal-magnetic-model (Solar Corona) features to predict solar wind. (No allowed-list value exists specifically for "solar wind"; the closest controlled-vocabulary phenomena are listed. "Solar wind" recorded under Keywords.)*

### 23. Development Status (RECOMMENDED)
Inactive

*Source: Reached a stable, usable state tied to a 2021 publication; not actively developed (single 2022-02-21 archival commit in this monorepo, code created 2019-2020). Could also be characterized as a Concept/demonstration research code, but "Inactive" best matches a completed, paper-accompanying release.*

### 24. Documentation (RECOMMENDED)
https://github.com/helioforecast/Papers/tree/master/Bailey2021_AmbSoWiML

*Source: No dedicated documentation site; the README.md and the ambsowi_forecast_ML.ipynb notebook itself serve as documentation and usage instructions.*

### 25. Funder (OPTIONAL)
- **Organization:** Austrian Science Fund
  - **Funder Identifier:** https://ror.org/013tf3c58

*Source: Crossref funding metadata for the reference publication (10.1029/2020SW002673). The Austrian Science Fund (FWF, ROR 013tf3c58 / Funder DOI 10.13039/501100002428) is the sole funder listed. Not stated in the subdirectory README/LICENSE/notebook; attributed from the reference publication.*

### 26. Award Title (OPTIONAL)
- **Award Title:** Not found
  - **Award Number:** J4160-N27

*Source: Crossref funding metadata for the reference publication lists four FWF awards (P31659-N27, J4160-N27, P31521-N27, P31265-N27). Only the award number, not a title, is provided by Crossref. J4160-N27 is an FWF Erwin Schrödinger ("J"-series) individual fellowship, most directly attributable to the software author R. L. Bailey; the three "P"-series project grants are associated with the publication's co-authors and are not asserted here as funding this specific software. Submitter should confirm and add award titles if known.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found *(beyond the reference publication in Field 14. The notebook references a comparison to Chandorkar et al. (2020), but it is not asserted as a citing/describing publication for this software.)*

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.6084/m9.figshare.4588315.v1 *(HELCATS ICMECAT interplanetary coronal mass ejection catalogue — loaded directly as notebook input (data/HELCATS_ICMECAT_v10_SCEQ.txt) to mask out ICME intervals during training)*

*Source: Cell 8 of ambsowi_forecast_ML.ipynb explicitly instructs downloading the ICME catalogue from this Figshare DOI. The WSA coronal magnetic model maps provided by C. N. Arge are not openly shared and have no DOI. Results were contributed to the ISWAT ambient solar wind forecasting team comparison: https://www.iswat-cospar.org/s2*

### 29. Related Software (OPTIONAL)
- https://github.com/helioforecast/predstorm *(predstorm==0.1.1 — dependency used to load observed near-Earth solar wind data)*
- https://github.com/ajefweiss/HelioSat *(heliosat==0.4.0 — dependency in environment.yml)*
- https://github.com/helioforecast/Papers/tree/master/Bailey2021_AmbSoWiML *(archival copy of this code within the helioforecast/Papers monorepo; the copy that was extracted)*

*Source: environment.yml dependencies and README links. The primary Code Repository (Field 3) is the standalone repo https://github.com/bairaelyn/ambsowi-ml; the monorepo subdirectory is its archived copy.*

### 30. Interoperable Software (OPTIONAL)
Not found

### 31. Related Instruments (OPTIONAL)
Not found

### 32. Related Observatories (OPTIONAL)
Not found

*Source: No specific observatory is named in the notebook. By inference the WSA/PFSS coronal model inputs are likely driven by GONG/ADAPT synoptic magnetograms, and the OMNI solar wind / HELCATS ICME identification draw on the Wind (and ACE) spacecraft — but none of these are explicitly stated as software dependencies in the code, so they are left unasserted.*

### 33. Logo (OPTIONAL)
Not found
