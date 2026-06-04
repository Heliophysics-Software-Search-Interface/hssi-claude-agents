# HSSI Metadata Extraction Results

**Repository:** https://github.com/donglai96/ORIENT
**Extraction Date:** 2026-06-04

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.8361954

*Source: Concept DOI (all-versions) from the Zenodo API (`conceptdoi: 10.5281/zenodo.8361954`). The version-specific v1.0.0 DOI is `10.5281/zenodo.8361955` (recorded under Field 12, Version PID). The README also references an earlier model-data archive at https://zenodo.org/record/6299967 (recorded under Field 28, Related Datasets).*

### 3. Code Repository (MANDATORY)
https://github.com/donglai96/ORIENT

*Source: git remote `origin`, CITATION.cff `url`, setup.py `url`, and PKG-INFO Home-page.*

### 4. Software Functionality (MANDATORY)
- Models and Simulations
- Models and Simulations:ML/AI
- Models and Simulations:Empirical
- Models and Simulations:Data Guided
- Models and Simulations:Forecasting
- Data Processing and Analysis
- Data Processing and Analysis:ML/AI
- Data Processing and Analysis:Data Access and Retrieval
- Data Processing and Analysis:Analysis
- Data Processing and Analysis:Time Series Analysis
- Data Processing and Analysis:Processing
- Data Processing and Analysis:Energy Spectra
- Data Visualization
- Data Visualization:2D Graphics
- Data Visualization:Line Plots
- Data Visualization:Spectrogram

*Source: Manual examination of `ORIENT/eflux/model.py`, `examples/run_ORIENT.py`, and the data loaders (`omni/load.py`, `ace/load.py`, `al_CB/load.py`, `dst_kyoto/load.py`).*
- *Models and Simulations + ML/AI: the core capability is a trained TensorFlow/Keras neural-network model that predicts equatorial differential electron flux in the outer radiation belt (`tf.keras.models.load_model`, `nnmodel.predict` in `eflux/model.py`). The `ORIENT/shap` module and `get_explainer()` add SHAP-based ML model interpretability.*
- *Empirical: ORIENT is a data-driven empirical model of radiation-belt electron flux as a function of geomagnetic/solar-wind driving and L-shell/MLT (statistical model trained on RBSP/MagEIS/REPT observations), not a first-principles physics solver.*
- *Data Guided: model is driven by observational inputs (SYM-H/Dst, AE/AL, solar wind speed/pressure/IMF Bz) loaded at runtime.*
- *Forecasting: the README and `run_ORIENT.py` describe "real-time"/"nowcast"/"prediction time" operation; the CLI is used by CCMC for automated execution, producing flux nowcasts/forecasts. (Note: an explicit multi-day predict mode is gated off in this release with "Not supporting predict mode! Please contact the author"; the nowcast-at-input-time behavior remains.)*
- *Data Access and Retrieval: downloads geomagnetic and solar-wind indices at runtime - OMNI via `pyspedas.omni.data` (`omni/load.py`), ACE MAG/SWEPAM real-time text files over HTTP (`ace/load.py`), Kyoto Dst via web form scraping with `mechanize` (`dst_kyoto/load.py`), and the CU Boulder AL forecast index over HTTP (`al_CB/load.py`).*
- *Analysis: gap-filling, interpolation, lagged-feature construction, normalization, and L/MLT-grid flux reconstruction (`fill_gap`, lag-matrix assembly, MLT mesh prediction in `eflux/model.py`).*
- *Time Series Analysis: inputs are 5-minute time series processed over multi-day driving windows with rolling means and time-lagged feature matrices (`pandas.rolling`, unix-time interpolation, lag windows).*
- *Processing: builds the model input matrix (normalization with stored avg/std, position/MLT encoding via sin/cos) feeding the neural net.*
- *Energy Spectra: predicts differential electron flux across discrete energy channels (MagEIS 50, 235, 597, 909 keV and REPT >1 MeV) - per-channel model files (`mageis_ch3_model_sav.h5`, etc.) and the `ENERGY_TO_CHANNEL` mapping / `instrument`/`channel` parameters in `examples/run_ORIENT.py` and `eflux/model.py`.*
- *Data Visualization 2D Graphics + Spectrogram: `make_plot`/`make_flux_plot` produce time-vs-L `pcolormesh` flux spectrograms (LogNorm), and `makeMLTplot` produces MLT-L polar `pcolor` flux maps.*
- *Line Plots: stacked driver panels (SYM-H, V_SW, P_SW, Bz, AL/AE) plotted as line time series (`make_plot`, `run_ORIENT.py` stacked_time_L).*

### 5. Related Region (MANDATORY)
- Earth Magnetosphere

*Source: ORIENT models electron flux in the Earth's outer radiation belt (L-shell ~2.6-6.6, magnetic equatorial plane, MLT distribution) - a region of the inner magnetosphere. Solar-wind/IMF parameters (from OMNI/ACE at L1) are used purely as driver inputs to the magnetospheric model, so the modeled physical region is the Earth Magnetosphere.*

### 6. Authors (MANDATORY)
- **Author:** Donglai Ma
  - **Author Identifier:** https://orcid.org/0000-0003-3183-4289
  - **Affiliation:**
    - **Organization:** University of California, Los Angeles
      - **Affiliation Identifier:** https://ror.org/046rm7j60

*Source: CITATION.cff (sole author "Ma, Donglai", ORCID 0000-0003-3183-4289), setup.py/PKG-INFO author "Donglai Ma", and source-file headers. DataCite/Zenodo list the creator as "Donglai Ma (UCLA)". Affiliation expanded from "UCLA" and the author email dma96@atmos.ucla.edu (UCLA Department of Atmospheric and Oceanic Sciences) to "University of California, Los Angeles"; ROR https://ror.org/046rm7j60.*

### 7. Software Name (MANDATORY)
ORIENT

*Source: CITATION.cff title, repository name, setup.py `name`. ORIENT is a backronym for "the Outer RadIation belt Electron Neural net" model (per the DataCite/Zenodo description "The Outer RadIation belt Electron Neural net model"). The README/code also refer to the package internally as "ORIENT-M".*

### 8. Description (MANDATORY)
ORIENT (Outer RadIation belt Electron Neural net) is a Python package that provides a machine-learning model for nowcasting and visualizing electron flux in the Earth's outer radiation belt. It uses pre-trained TensorFlow/Keras neural networks to predict equatorial differential electron flux as a function of L-shell (~2.6-6.6) and magnetic local time, driven by geomagnetic and solar-wind inputs (SYM-H/Dst, AE/AL indices, solar-wind speed, dynamic pressure, and IMF Bz). The model was trained on Van Allen Probes (RBSP) MagEIS and REPT measurements and supports multiple energy channels (e.g. MagEIS 50, 235, 597, 909 keV and REPT >1 MeV). ORIENT automatically retrieves its driver data at runtime from OMNI (via pyspedas), the ACE spacecraft, Kyoto WDC (Dst), and the CU Boulder AL forecast index, then assembles time-lagged, normalized input features for the network. It produces stacked time-vs-L flux spectrograms together with the driving inputs, and MLT-L polar flux maps. A command-line wrapper (`examples/run_ORIENT.py`) supports automated pipeline execution and is used by the Community Coordinated Modeling Center (CCMC) for automated ORIENT model requests. The package also provides SHAP-based interpretability of the neural-network predictions.

*Source: Synthesized from README, `ORIENT/eflux/model.py`, `examples/run_ORIENT.py`, setup.py, and the DataCite/Zenodo description.*

### 9. Concise Description (OPTIONAL)
Neural-network model that nowcasts and visualizes outer radiation belt electron flux vs. L-shell and MLT from geomagnetic and solar-wind drivers.

*Source: Condensed from the Description (<=200 characters).*

### 10. Publication Date (RECOMMENDED)
2023-09-19

*Source: CITATION.cff `date-released: 2023-09-19` (v1.0.0). DataCite/Zenodo report the record issued date as 2023-09-20; the CITATION.cff release date is used as the authoritative publication date.*

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://ror.org/01ggx4157

*Source: DataCite/Zenodo metadata (publisher of the archived software DOI 10.5281/zenodo.8361955 via the GitHub-Zenodo release workflow). Publisher Identifier uses Zenodo's ROR (https://ror.org/01ggx4157) per the form spec preference for ROR over plain URL.*

### 12. Version (RECOMMENDED)
- **Version Number:** 1.0.0
- **Version Date:** 2023-09-19
- **Version Description:** First released/archived version of ORIENT ("the final version of ORIENT" per README), git tag v1.0.0, archived on Zenodo. No CHANGELOG present in the repository.
- **Version PID:** https://doi.org/10.5281/zenodo.8361955

*Source: CITATION.cff (`version: 1.0.0`, `date-released: 2023-09-19`), git tag `v1.0.0` (tagged 2023-09-14), and Zenodo (v1.0.0). Note: setup.py/PKG-INFO declare `version='1.0'`; the CITATION.cff/Zenodo semantic version 1.0.0 is used.*

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Source: setup.py (`python_requires='>=3.8'`, classifier "Programming Language :: Python :: 3.8"), README (conda env with python=3.8), and the all-Python codebase.*

### 14. Reference Publication (RECOMMENDED)
Not found

*Source: No reference/methodology publication DOI is cited in the README, CITATION.cff, or code. CITATION.cff provides only the software DOI (recorded under Field 2). The README directs users to contact dma96@atmos.ucla.edu for the latest model. A formal ORIENT methodology paper, if one exists, should be added by the submitter.*

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT.html

*Source: setup.py (`license='MIT'`, classifier "License :: OSI Approved :: MIT License") and PKG-INFO (`License: MIT`). Note: no standalone LICENSE file is present in the repository, and the Zenodo record reports the generic placeholder "other-open"; the MIT declaration in the package metadata is treated as authoritative. Recommend the maintainer add a LICENSE file.*

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- radiation belt
- outer radiation belt
- electron flux
- neural network
- machine learning
- space weather
- nowcasting
- magnetosphere
- Van Allen Probes
- RBSP
- MagEIS
- REPT
- L-shell
- magnetic local time
- geomagnetic indices
- solar wind
- python

*Source: Derived from setup.py keywords ("predict radiation-belt"), README, and code. DataCite/Zenodo list no subject keywords.*

### 17. Data Sources (OPTIONAL)
- OMNIWeb
- HTTP/HTTPS Directories
- Observatory/Mission-specific

*Source: Code examination. OMNIWeb: solar-wind/geomagnetic indices loaded via `pyspedas.omni.data` (`omni/load.py`). HTTP/HTTPS Directories: ACE real-time MAG/SWEPAM text files and the CU Boulder AL index downloaded over HTTP (`ace/load.py`, `al_CB/load.py`); Kyoto Dst retrieved via web form (`dst_kyoto/load.py`). Observatory/Mission-specific: ACE spacecraft data and Van Allen Probes (RBSP) MagEIS/REPT training data underlying the bundled models.*

### 18. Input File Formats (RECOMMENDED)
- HDF5
- ascii
- Other

*Source: Code examination. HDF5: trained Keras models loaded from `*_model_sav.h5` (`tf.keras.models.load_model`, see `examples/RB_model/*.h5`). ascii: model parameter files `*_parameter.txt` (JSON-formatted text, read via `json.load`), and downloaded ACE/AL/Dst index data parsed from `.txt` via `pandas.read_csv` / IAGA2002. Other: model normalization arrays stored as NumPy `.npy` (`*_input_avg.npy`, `*_input_std.npy`), and trajectory inputs as pandas pickle files (`pd.read_pickle`) - neither `.npy` nor pickle is in the allowed format list.*

### 19. Output File Formats (RECOMMENDED)
- PNG

*Source: `examples/run_ORIENT.py` saves figures via `fig.savefig(...png, dpi=300)` (stacked time-L plots `ORIENT_stacked_*keV.png` and MLT polar plots `ORIENT_*keV_MLT.png`). The library `make_plot`/`makeMLTplot` return Matplotlib figures; the in-notebook examples display rather than persist files.*

### 20. Operating System (RECOMMENDED)
- Mac

*Source: setup.py docstring notes the package "used on m1 mac" and the bundled `environment.yml` is an Apple-silicon (osx-arm64, tensorflow-macos/tensorflow-metal) conda environment. The code itself is pure Python with no hard OS lock-in, but the only documented/tested platform is macOS (Apple M1). Likely cross-platform with appropriate TensorFlow install - flag for maintainer to confirm Linux/Windows support.*

### 21. CPU Architecture (RECOMMENDED)
- Apple Silicon arm64

*Source: The provided `environment.yml` targets osx-arm64 (Apple M1) with tensorflow-macos and tensorflow-metal, and setup.py notes "this used on m1 mac". No architecture-specific compiled code exists in the package itself (pure Python), so it is likely CPU-independent in principle, but the only documented build/runtime is Apple-silicon arm64 - flag for maintainer to confirm x86_64 support.*

### 22. Related Phenomena (OPTIONAL)
Not found

*Source: ORIENT models outer radiation belt electron flux and storm-time flux response (example notebook `CCMC_test_storm.ipynb`), but the relevant descriptive terms ("Radiation belt electrons", "Geomagnetic storms") are not in the HSSI controlled vocabulary for this field (which covers solar/coronal phenomena only). No allowed value applies, so this OPTIONAL field is left as Not found.*

### 23. Development Status (RECOMMENDED)
Active

*Source: Inferred. README calls v1.0.0 "the final version of ORIENT" and the core model code dates to 2022-2023, which suggested "Inactive". However, `examples/run_ORIENT.py` was added 2025-06-13 by a second contributor (Jack Topper) to support automated CCMC execution, indicating ongoing maintenance - so "Active" is recorded. This is genuinely ambiguous; submitter/reviewer should confirm against the controlled list. Note: Jack Topper (2025 CLI author) may warrant inclusion in Field 6 (Authors) or an acknowledgment.*

### 24. Documentation (RECOMMENDED)
https://github.com/donglai96/ORIENT/blob/main/README.md

*Source: No external documentation site (no docs/ folder, no Read the Docs config). The README provides installation, library/CLI usage, model/channel descriptions, and example notebooks. Function-level docstrings exist in `eflux/model.py` and the loaders.*

### 25. Funder (OPTIONAL)
Not found

*Source: No funding/acknowledgement information in the repository, CITATION.cff, or DataCite/Zenodo metadata. No reference publication was identified from which to derive grant funding.*

### 26. Award Title (OPTIONAL)
Not found

*Source: No award/grant information in the repository or DOI metadata.*

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found

*Source: No related publication DOIs are cited in the repository, CITATION.cff, or DOI metadata.*

### 28. Related Datasets (OPTIONAL)
- https://doi.org/10.5281/zenodo.6299967 - ORIENT model files (the trained radiation-belt models, including relativistic eflux >1 MeV models), referenced in the README for the latest model download.
- Van Allen Probes (RBSP) MagEIS and REPT electron flux measurements - the observational data the ORIENT neural networks were trained on (not bundled; described in README "Model name").
- OMNI / ACE / Kyoto Dst / CU Boulder AL index time series - driver data retrieved at runtime (see Field 17).

*Source: README "Model" and "Model name" sections, and the runtime data loaders. No formal dataset DOIs beyond the Zenodo model archive.*

### 29. Related Software (OPTIONAL)
- https://github.com/donglai96/ORIENT-M - companion repository: the Outer RadIation belt Electron Neural net model for Medium Energy electrons (per GitHub repo description), referenced in the README.
- https://github.com/spedas/pyspedas - pyspedas (runtime dependency; OMNI data access).
- https://www.tensorflow.org - TensorFlow/Keras (runtime dependency; neural-network model loading and inference).
- https://github.com/shap/shap - SHAP (runtime dependency; model interpretability via `get_explainer`).
- https://github.com/astropy/astropy - Astropy (runtime dependency).
- pandas, matplotlib, scipy, mechanize - additional runtime dependencies (setup.py `install_requires`).

*Source: README (ORIENT-M link) and setup.py `install_requires` / imports in the source modules.*

### 30. Interoperable Software (OPTIONAL)
Not found

*Source: No demonstrated runtime integration where ORIENT and another package operate together beyond ORIENT consuming standard dependencies. pyspedas/TensorFlow/SHAP are dependencies rather than interoperating peers.*

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** MagEIS (Magnetic Electron Ion Spectrometer, on Van Allen Probes)
- **Instrument Name:** REPT (Relativistic Electron-Proton Telescope, on Van Allen Probes)
- **Instrument Name:** SWEPAM (Solar Wind Electron Proton Alpha Monitor, on ACE)
- **Instrument Name:** MAG (Magnetometer, on ACE)

*Source: Code and README. The ORIENT models are trained on and labeled by RBSP MagEIS/REPT electron flux channels (`instrument='mageis'/'rept'`, channels 3/11/14/16, README "Model name"). ACE SWEPAM (solar-wind speed/density/pressure) and ACE MAG (IMF Bz) are read for driver inputs (`ace/load.py`).*

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Van Allen Probes (RBSP)
- **Observatory Name:** ACE (Advanced Composition Explorer)

*Source: Van Allen Probes / RBSP (spacecraft A and B; `rbspa`/`rbspb` trajectory handling and MagEIS/REPT training data) and ACE (real-time solar-wind driver data, `ace/load.py`). OMNI and Kyoto WDC are merged data products/archives rather than observatories.*

### 33. Logo (OPTIONAL)
Not found

*Source: No logo file in the repository and none referenced in the README or DOI metadata.*
