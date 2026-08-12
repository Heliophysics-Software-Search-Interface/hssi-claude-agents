# HSSI Metadata Extraction Results

**HSSI Software ID:** 181726f7-b361-4d04-8235-15729283791d
**Repository:** https://github.com/NCAR/solar-forcing
**Source Revision:** 5e7baf7656bd5b7b89672fc9d7ad5011b06bb722
**Extraction Date:** 2026-08-11
**Validation Date:** 2026-08-11
**Validation Status:** PASS

---

## Scope note

`NCAR/solar-forcing` is a small, short-lived research package: 5 Python modules, 6 example
notebooks, 2 bundled data files, 2 bundled PDFs. Development ran from 2021-06-16 to 2022-01-13
and the GitHub repository is now **archived** (`archived: true` in the GitHub repository API;
`updated_at` 2025-08-05). It was never released — no git tag, no GitHub Release, no PyPI or
conda-forge distribution, no DOI. Evidence for most fields therefore comes from the source itself
rather than from release metadata or a citation file, and several fields are correctly empty. The
distributed example notebooks are the project's primary user-facing documentation (they are the
source of the Jupyter Book built by CI), so they are treated here as first-class evidence
alongside the installable package.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)

- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*This record already exists in HSSI; the submitter fields belong to the original submission and are
not part of a metadata refresh.*

---

### 2. Persistent Identifier (RECOMMENDED)

**Not found.**

Negative research, so a later refresh does not repeat it:

- No `CITATION.cff` exists in the repository (confirmed against a full file listing at
  `5e7baf7` — the repository contains exactly `LICENSE`, `README.md`, `requirements.txt`,
  `setup.py`, `.gitignore`, `.github/workflows/deploy.yml`, `envs/environment.yml`, 2 files under
  `data/`, 2 PDFs under `docs/`, 9 files under `notebooks/`, and 5 files under `solarforcing/`).
- No `codemeta.json`, no `.zenodo.json`, no DOI badge in `README.md`.
- DataCite returns 0 results for `relatedIdentifiers.relatedIdentifier:"https://github.com/NCAR/solar-forcing"`
  and 0 results for the quoted phrase `"NCAR/solar-forcing"`.
- Zenodo has no record for this repository; the GitHub–Zenodo integration was never enabled (no
  release exists to trigger it — see Field 12).

HSSI stores an empty `persistentIdentifier`, which is correct.

---

### 3. Code Repository (MANDATORY)

**https://github.com/NCAR/solar-forcing**

Unchanged from the value the record already held. The GitHub repository API returns
`full_name: NCAR/solar-forcing`, `default_branch: main`, `created_at: 2021-06-16T14:29:47Z`,
`pushed_at: 2022-01-13T21:46:25Z`, `archived: true`. `setup.py` declares the same URL for `url`,
`project_urls['Documentation']` and `project_urls['Source']`.

The repository being archived does **not** change this field: the code is still hosted and readable
at this URL. It does change Field 23 (Development Status).

---

### 4. Software Functionality (MANDATORY)

- Coordinate Transforms
- Coordinate Transforms: Magnetospheric
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Physics-Based

HSSI previously held only `Data Processing and Analysis`. That value is retained; the other 13 are
additions supported by the code. Every listed subcategory has its parent listed.

All 14 values resolve against the live `FunctionCategory` vocabulary (83 rows), but note how that
vocabulary is shaped, because it governs how this field must be read in any later refresh: it is a
graph, not a flat list of combined strings. Each row carries only a bare leaf `name` (`Analysis`,
`Magnetospheric`, `Physics-Based`) plus a `parents` list of row IDs, so **no row exists whose name is
the literal combined string** `Coordinate Transforms: Magnetospheric`. Each value above therefore
resolves in two parts — the parent name and the child name are each a real row, and the child's
`parents` list contains that specific parent's `id`. That linkage is what disambiguates leaf names
appearing more than once in the vocabulary: `Analysis` exists both under `Data Processing and
Analysis` and under `Mission-related`, and only the parent ID distinguishes the intended value from
the wrong one.

**Evidence for each value**

- **Data Processing and Analysis: Data Access and Retrieval** — `data_access.grab_potsdam_file()`
  (`solarforcing/data_access.py:7`) retrieves the GFZ Potsdam `Kp_ap_Ap_SN_F107_since_1932.txt`
  index file over FTP with `urllib.request.urlretrieve` (line 28) and parses it into a pandas frame
  (line 31). `data_access.grab_ssi_lasp_file()` (line 72) retrieves the LASP LISIRD NRL2 daily
  spectral solar irradiance netCDF over HTTPS (line 98) and opens it with `xarray` (line 100). Both
  are user-facing: `grab_potsdam_file` is re-exported at package top level
  (`solarforcing/__init__.py:5`) and both are reachable through `FluxCalculation.grab_data()` and
  the `SolarIrradiance` constructor (`solarforcing/main.py:30`, `:90`).
- **Data Processing and Analysis: Energy Spectra** — `calc.gen_energy_grid()`
  (`solarforcing/calc.py:9`) builds a logarithmically spaced 30–1000 keV energy grid;
  `calc.vdk2016()` (line 39) returns flux spectral density `S(E) = C·E^k` in
  electrons/(cm² sr s keV) on that grid; `calc.calculate_flux()` (line 96) assembles a
  (L-shell, ap, energy) flux array. Producing and manipulating flux-versus-energy spectra is the
  core computation of the package.
- **Data Processing and Analysis: Processing** — `solarforcing/data_cleaning.py` is an explicit
  processing pipeline over the LASP irradiance dataset: `rename_variables()` (line 36),
  `center_time()` (line 54, recomputes `time` as the mean of `time_bnds`), `add_datesec()` (line 81)
  and `add_date()` (line 74) synthesize the CAM/CESM `date` and `datesec` input-file fields,
  `add_global_attrs()` (line 7) writes provenance attributes, and `scale_ssi()` (line 89) converts
  SSI from W m⁻² nm⁻¹ to mW m⁻² nm⁻¹. `SolarIrradiance.generate_dataset()`
  (`solarforcing/main.py:92`) chains all six.
- **Data Processing and Analysis: Analysis** — derived scientific quantities beyond format handling:
  `calc.calculate_ipr()` (`solarforcing/calc.py:231`) produces ionization pair production rates as a
  function of altitude and energy; `calc.calculate_iprm()` (line 248) integrates the IPR over the
  energy spectrum with `scipy.integrate.simps` (line 280), normalizes by mass density to obtain IPRM
  (line 283) and converts geometric altitude to pressure levels via a barometric scale-height
  relation (line 286). `data_access.read_atm()` (line 51 of `data_access.py`) computes atmospheric
  scale height from Boltzmann's constant, mean molecular mass and gravity.
- **Data Processing and Analysis: Time Series Analysis** — `grab_potsdam_file()` builds a
  `DatetimeIndex` from the file's year/month/day columns (`data_access.py:33-36`), subsets by
  `start_date`/`end_date` (lines 39-43), and reduces eight 3-hourly `ap` values to a daily mean
  (line 46). Outputs carry a `time` dimension (`calc.py:289-293`), and `apeep.ipynb` performs
  time-slice storm analysis over the resulting series.
- **Coordinate Transforms** and **Coordinate Transforms: Magnetospheric** —
  `calc.lshell_to_glat()` and `calc.glat_to_lshell()` (`solarforcing/calc.py:142`, `:159`) convert
  between McIlwain L-shell and geomagnetic latitude using the centered-dipole relation
  `r = L cos²λ`. Both are re-exported in the package's public API
  (`solarforcing/__init__.py:4`), so this is a user-facing capability and not an internal
  utility. L-shell is a magnetospheric coordinate, which fixes the parent.
  *Considered and not selected:* `Coordinate Transforms: Ionospheric`. Its definition mentions
  "magnetic latitude", and geomagnetic latitude is one half of this pair — but the transform is
  anchored on L-shell, a magnetospheric/radiation-belt coordinate, and the package implements no
  AACGM, apex or magnetic-local-time machinery. Listing both parents would double-count one
  two-line dipole formula.
- **Models and Simulations** and **Models and Simulations: Empirical** — `calc.vdk2016()` is a
  direct implementation of the van de Kamp et al. (2016) empirical radiation-belt electron
  precipitation model; the coefficients on lines 62-82 of `calc.py` are that paper's fitted
  constants, and the docstring names the source ("Calculations here are defined by van de Kamp
  et al. 2016 (doi:10.1002/2015JD024212)"). The background atmosphere is likewise empirical-model
  output (NRLMSIS 2.0, `data/msis2.0_atm_out.txt`).
- **Models and Simulations: Physics-Based** — `calc.fang()` (line 176) implements the Fang et al.
  (2010) parameterization of monoenergetic electron impact ionization, including its Table 1
  coefficient matrix; `calc.iprmono()` (line 209) applies it with the physical constant
  ε = 0.035 keV per ion pair to convert deposited energy into ion-pair production. This is
  semi-empirical physics (an analytic fit to first-principles transport calculations), which is
  what this subcategory covers.
  *Considered and not selected:* `Models and Simulations: First Principles` — the package evaluates
  fitted parameterizations; it does not solve a transport equation.
  *Considered and not selected:* `Models and Simulations: Data Guided` — the van de Kamp model is
  driven by an observed geomagnetic index, which is arguably "driven by observational data". It was
  left off because `Empirical` already carries that meaning here, and no boundary condition,
  assimilation step or data-driven state is involved. A reviewer who reads `Data Guided` more
  broadly could add it without contradicting any evidence.
  *Considered and not selected:* `Forecasting` (the package processes the historical index record,
  1932–present, and predicts nothing), `MHD`, `Forward-Fitting`, `Theory`, `Instrument Response`,
  `ML/AI`, `Mission-Specific`, `Observatory/Instrument Models`, `Field-line Tracing`.
- **Data Visualization**, **Data Visualization: Line Plots**, **Data Visualization: 2D Graphics** —
  these rest on the distributed notebooks rather than on an installed plotting API. That basis is
  recorded in full because it is the kind of reading a later pass could otherwise reverse without
  noticing what the evidence actually is.
  No module under `solarforcing/` imports `matplotlib` or `cartopy` (verified by grep over the whole
  package), so no installed function returns a figure. The visualization evidence is instead
  (a) `matplotlib` being the first entry in `requirements.txt`, which `setup.py:8` feeds directly
  into `install_requires`, i.e. the package declares a plotting dependency it never imports; and
  (b) the distributed notebooks, which are the project's documentation and are published as a
  Jupyter Book by `.github/workflows/deploy.yml`. Those notebooks produce log-log and semi-log line
  plots of flux spectra and altitude profiles (`apeep.ipynb`, `compare_fluxes.ipynb`), filled
  contour plots of IPRM against latitude and pressure level, and orthographic polar map projections
  via `cartopy.crs.Orthographic` (`ipr_comparison.ipynb`).
  The stricter "installed package API only" reading — which would drop all three values — was
  considered and rejected. The notebooks are distributed with the package, are its published
  documentation, and are the only worked examples a user has; the plotting they demonstrate is
  therefore a capability the project offers rather than incidental scratch work. Nothing else in
  this record depends on these three values either way.

**Considered and not selected (other categories)**

- `Data Processing and Analysis: File Format Conversion` — the `SolarIrradiance` path reads netCDF
  and writes netCDF, so the reshaping is convention conformance rather than format conversion
  (already covered by `Processing`), and the one ASCII→netCDF write in the repository
  (`notebooks/calculate_flux_from_ap_csv.ipynb`, `ds.to_netcdf(...)`) is incidental to a
  derived-quantity calculation. No function exists whose purpose is converting file A to file B.
- `Data Processing and Analysis: Data Reduction` — averaging eight 3-hourly `ap` values to a daily
  value (`data_access.py:46`) is an 8× reduction, but it is one line inside a data-access helper,
  not a reduction capability offered to users.
- `Data Processing and Analysis: Pitch Angle Distributions` / `3D Particle Distribution Processing`
  / `Plasma Moments` — recorded explicitly because the code invites the mistake. `calc.py:136`
  multiplies the per-steradian flux by `2π(1 − cos 80°)`, the solid angle of a nominal bounce loss
  cone, under an explicit isotropy assumption. That is a solid-angle scaling constant, not a pitch
  angle distribution, a velocity-space distribution, or a moment integration.
- `Mission-related` (any subcategory) — this is not part of any mission ground system.
- `Servers and Environments: Software or Environment Container` — `envs/environment.yml` is a conda
  environment specification, not a container image; there is no Dockerfile or Singularity recipe.
- `Data Processing and Analysis: Data Assimilation`, `Spectrogram`, `Wavelet Analysis`,
  `Image Processing`, `ML/AI`, `Curlometer`, `Magnetic Null Finding`, `Calibration` — no
  corresponding code.

**Durable caveat.** `data_access.grab_ssi_lasp_file()` references `pathlib.Path` at line 89 but
`pathlib` is never imported in that module (its imports are `os`, `urllib`, `pandas`, `xarray`), so
the `SolarIrradiance` path raises `NameError` as shipped at `5e7baf7`. The solar-irradiance
functionality recorded above is the documented and intended capability — `simplified_api_example.ipynb`
demonstrates it and `data_cleaning.py` implements the whole pipeline — but a future maintainer
checking whether the code runs should expect this defect and not conclude the functionality was
mis-recorded.

---

### 5. Related Region (MANDATORY)

- Earth Atmosphere
- Earth Inner Magnetosphere
- Earth Ionosphere
- Earth Lower and Middle Atmosphere
- Earth Thermosphere
- Solar Environment

`Earth Atmosphere` and `Solar Environment` were already stored in HSSI and are retained. The other
four are additions. All six are rows in the live `Region` vocabulary (24 rows), which is flat — there
is no parent/child relationship, so no parent values are implied here as they are in Field 4.

- **Earth Lower and Middle Atmosphere** and **Earth Thermosphere** — the bundled background
  atmosphere `data/msis2.0_atm_out.txt` spans 50 to 150 km in 1 km steps (verified from the file's
  first and last data rows), at a fixed Ap of 48.0. The ionization profile is computed on exactly
  that grid, so the deposition region straddles the upper stratosphere/mesosphere and the lower
  thermosphere. Both rows are more specific than `Earth Atmosphere`, which the vocabulary guidance
  prefers.
- **Earth Ionosphere** — the quantity produced is the ion pair production rate at 50–150 km, i.e.
  D- and E-region ionization. This is the physical link between the precipitating electrons and
  atmospheric chemistry that the package exists to quantify.
- **Earth Inner Magnetosphere** — the source region of the precipitating flux. `FluxCalculation`
  defaults to L-shells 2.0 through 10.5 (`solarforcing/main.py:14-16`), and the van de Kamp
  formulation is referenced to the plasmapause L-shell (`lpp` on `calc.py:62`), i.e. it is a
  radiation-belt/plasmasphere model.
  *Considered and not selected:* `Earth Magnetosphere` (less specific than the row chosen) and
  `Earth Outer Magnetosphere` (the default L grid does reach 10.5, but the model's physical basis
  and the region where it produces meaningful precipitation are the radiation belts).
- **Earth Atmosphere** — retained from the existing record; accurate as the broad regional context
  and harmless alongside the specific rows.
- **Solar Environment** — retained from the existing record and independently supported: the
  `SolarIrradiance` class processes NRL2 total and spectral solar irradiance, a solar quantity, and
  the package's subject is solar forcing of the Earth system.

**Considered and not selected**

- `Earth Auroral Subregion` — tempting, because the ionization is computed at geomagnetic latitudes
  of roughly 45°–72° and `ipr_comparison.ipynb` draws polar maps. Rejected because the energy grid
  is 30–1000 keV (`calc.py:9`), i.e. radiation-belt medium-energy electrons, not the ~1–10 keV
  auroral primaries that define the auroral subregion. The Fang et al. parameterization does extend
  down to auroral energies, but this package never evaluates it there.
- `Solar Wind`, `Interplanetary Space`, `Corona`, `Chromosphere`, `Photosphere`, `Solar Interior` —
  no corresponding data or physics; the solar side of the package is irradiance at 1 AU only.
- The planetary magnetosphere rows — Earth only.

---

### 6. Authors (MANDATORY)

**Author 1 — Max Grover**
- **Identifier:** https://orcid.org/0000-0002-0370-8974
- **Affiliation:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44
- **Affiliation:** Argonne National Laboratory — https://ror.org/05gvnxz63

**Author 2 — Dan Marsh**
- **Identifier:** https://orcid.org/0000-0001-6699-494X
- **Affiliation:** University of Leeds — https://ror.org/024mrxd33
- **Affiliation:** NSF National Center for Atmospheric Research — https://ror.org/05cvfcr44

Authorship itself is unchanged and correct. `notebooks/_config.yml` names "Max Grover, Dan Marsh" as
the book's authors, `setup.py:13-14` names Max Grover as maintainer (`mgrover@ucar.edu`), and the
commit history contains only these two contributors (52 commits in total: Max Grover 43, and Dan
Marsh 9 under the name `dan800` from `marsh@ucar.edu` and a GitHub noreply address). Both ORCIDs
were already stored and both resolve to the right people (ORCID's published name for the first is
"Maxwell Grover"; "Max Grover" is what the commits, the book config and the record itself use, and
is retained).

**Affiliation corrections and the evidence behind them**

- *Max Grover — NSF National Center for Atmospheric Research is the contemporaneous affiliation.*
  His ORCID employment record lists "National Center for Atmospheric Research, Climate and Global
  Dynamics Laboratory, Software Engineer, 2021-03-01 to 2022-02-14". Development of this repository
  ran 2021-06-16 to 2022-01-13, entirely inside that window. His `setup.py` maintainer address is
  `mgrover@ucar.edu`, the repository lives under the NCAR GitHub organization, and `LICENSE` names
  National Center for Atmospheric Research as copyright holder.
- *Argonne National Laboratory postdates the work, and is retained anyway.* The same ORCID record
  puts the Argonne employment at 2022-02-21 to 2025-09-03 — beginning five weeks after the final
  commit — so it is almost certainly an artifact of recording the author's affiliation at submission
  time rather than at authorship time, and it is **not** the affiliation under which this software
  was written. It is nevertheless kept, for two reasons. It is not false as a statement of the
  author's later institutional identity, so removing it would trade one imprecision for the loss of
  a true fact. And removing it is not achievable through ordinary metadata maintenance: HSSI's
  software API can *add* an affiliation (matched on ROR, so re-adding is harmless) but offers no
  operation that replaces or removes one, which makes a removal a direct database change. That
  change was weighed and deliberately declined. A maintainer who revisits it should know the scope
  is narrow — Max Grover's person record in this HSSI instance is referenced only by this software
  entry — but should also weigh it against the fact that authorship itself is not in doubt here,
  only the institution shown beside it.
- *Dan Marsh holds both affiliations, so this is an addition rather than a correction.* His ORCID
  lists only University of Leeds (Professor), which is why the stored value is right as far as it
  goes. Primary corroboration for the NCAR half comes from a contemporaneous paper: in
  doi:10.1029/2020ea001223 (April 2021) the Crossref author record for D. R. Marsh carries **both**
  "National Center for Atmospheric Research High Altitude Observatory, Boulder CO USA" and
  "Faculty of Engineering and Physical Sciences, University of Leeds, Leeds UK". In-repository
  evidence agrees: 5 of his 9 commits are authored from `marsh@ucar.edu` (the other 4 use a GitHub
  noreply address). The University of Leeds staff
  page records that he moved to Leeds from NCAR in January 2018 and holds the Priestley Chair
  jointly across two Leeds schools, so Leeds is his primary post and NCAR the continuing joint
  appointment — both were live in 2021.

**Organization naming.** `NSF National Center for Atmospheric Research` is used rather than
`National Center for Atmospheric Research` because that is both the current ROR display name for
https://ror.org/05cvfcr44 and the name of the existing Organization row in this HSSI instance;
using it avoids minting a near-duplicate organization. `University Corporation for Atmospheric
Research` (https://ror.org/04zhhyn23) was considered, since both authors' addresses are `ucar.edu`,
and rejected: UCAR is the managing corporation, while the copyright holder in `LICENSE`, the GitHub
organization and Grover's ORCID employment all name NCAR.

No organization author (a lab, team or consortium credited as an author) appears anywhere in this
repository, so no ROR-identified author entry is warranted.

---

### 7. Software Name (MANDATORY)

**Solar-Forcing**

Unchanged. `README.md:1` is `# Solar-Forcing`, and SoMEF extracts `full_title: "Solar-Forcing"`.
The alternatives were considered and rejected as field values: `solar-forcing` is the repository
slug, and `solarforcing` is the Python distribution/import name (`setup.py:35`) — both are recorded
here as context rather than substituted for the human-readable name the existing record already
carries.

---

### 8. Description (MANDATORY)

> Solar-Forcing is a Python package for generating solar forcing datasets for the Community Earth
> System Model (CESM). It produces two kinds of forcing input. The first is medium-energy electron
> precipitation forcing: it retrieves the GFZ Potsdam Kp/ap/Ap/sunspot-number/F10.7 index file,
> derives a daily ap series, evaluates the van de Kamp et al. (2016) empirical radiation-belt
> electron precipitation model over a 30–1000 keV logarithmic energy grid and a configurable range
> of L-shells, and converts the resulting top-of-atmosphere energy spectra into atmospheric
> ionization pair production rates (IPR, and the mass-normalized IPRM) using the Fang et al. (2010)
> parameterization of monoenergetic electron impact ionization applied to a bundled NRLMSIS 2.0
> background atmosphere spanning 50–150 km. The second is solar spectral irradiance forcing: it
> retrieves the NRL2 daily spectral and total solar irradiance record from LASP LISIRD and reshapes
> it into the variable names, time-bounds convention, date and datesec fields, units and global
> attributes that CESM expects. Results are returned as xarray Datasets that can be written to
> netCDF. The precipitation calculation assumes the flux is isotropic within a nominal bounce loss
> cone (80 degrees by default) and maps L-shell to geomagnetic latitude with a centered-dipole
> relation.

**The superseded description, and why it was replaced.** This field previously read:

> Repository for working with solar weather forcing data for use with CESM
> Solar-forcing: A Python package to generate solar forcing files for CESM.
> This repository and package can be used to generate solar forcing datasets to be used for the Community Earth System Model (CESM)

That text was not authored prose, which is the reason replacing it discarded no curatorial intent —
a point worth recording, because a description is normally the last thing an automated pass should
overwrite. It was a mechanical concatenation of three sources, each reproduced word for word: line 1
is the GitHub repository `description` field, line 2 is `setup.py:28`, and line 3 is `README.md:3`.
All three say the same thing. The form asks for a description "sufficiently detailed to provide the
potential user with information to determine if the software is useful to their work… what the
software does, why to use it, assumptions it makes" written "with proper capitalization, grammar,
and punctuation"; the superseded text stated no capability, no input, no output and no assumption,
and two of its three lines lacked terminal punctuation.

The value recorded above keeps every claim the superseded text made (Python package; generates solar
forcing files/datasets; for CESM) and adds only what the source supports, together with the
assumptions the form asks for.

The recorded text is 1,336 characters. Its first 200 characters — the preview the form derives —
read: "Solar-Forcing is a Python package for generating solar forcing datasets for the Community
Earth System Model (CESM). It produces two kinds of forcing input. The first is medium-energy
electron precipi…". Field 9 supplies a cleaner preview regardless.

---

### 9. Concise Description (OPTIONAL)

**Python package that generates solar forcing inputs for CESM: radiation-belt electron precipitation ionization rates driven by the Ap index, and NRL2 solar spectral irradiance files from LASP.**

191 characters, within the 200-character limit. The record held no concise description before this
dossier. It is derived from the same source evidence as Field 8 and is written to work as a
standalone preview.

---

### 10. Publication Date (RECOMMENDED)

**2021-06-16**

Unchanged and corroborated. The first commit is `7f1379d`, 2021-06-16 08:29:49 −0600, and the GitHub
repository API gives `created_at: 2021-06-16T14:29:47Z` — the same instant. No earlier publication
of this code is known: there is no release, no DOI, and no predecessor Python distribution (the NCL
predecessor is a different artifact, recorded in Field 29).

---

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

The record held no publisher before this dossier. The form's rule applies directly: Zenodo is
correct when a DOI was obtained through the GitHub–Zenodo workflow, and otherwise "indicate the
repository host, such as GitHub or GitLab." No DOI exists (Field 2), and the repository is hosted on
GitHub.

`https://github.com` is used as the identifier rather than a ROR because ROR has no record for
GitHub (a ROR query for "GitHub" returns no matching organization), and because that exact
name/identifier pair is the established convention in this HSSI instance — it is already an
Organization row used as the publisher by other software records. *Considered and rejected:*
Zenodo (no Zenodo deposit exists) and NCAR (NCAR is the copyright holder and the GitHub
organization owner, not the publishing platform the form is asking about).

---

### 12. Version (RECOMMENDED)

**Not found — no version has ever been released.**

- **Version Number:** Not found
- **Version Date:** Not found
- **Version Description:** Not found
- **Version PID:** Not found

**Negative research.** No plausible release channel holds a release:

| Channel | Result |
|---|---|
| Git tags in the clone (`git tag -l`) | none |
| GitHub tags API (`/repos/NCAR/solar-forcing/tags`) | `[]` |
| GitHub releases API (`/repos/NCAR/solar-forcing/releases`) | `[]` |
| PyPI `solarforcing` and `solar-forcing` | HTTP 404 for both |
| conda-forge (`api.anaconda.org/package/conda-forge/solarforcing`) | HTTP 404 |
| Zenodo / DataCite | no record (see Field 2) |

`setup.py:44-48` derives the version from `setuptools_scm` with `version_scheme='post-release'`.
With no tag in history, `setuptools_scm` produces only a development version derived from the commit
distance and hash — a build-time artifact, not a released identifier.

**Do not record a version derived from the commit.** Writing `5e7baf7…`, `0.1.dev…` or the last
commit date as a "version" would invent an identifier the project never issued. The correct state of
this field is empty.

**Why this field is empty rather than simply unfilled.** The record previously carried a version
entry that held no version information whatsoever — an empty number, no release date, no description
and no identifier. Because a version is displayed as `<software name> - <number>`, that empty entry
reached readers as the meaningless string `"Solar-Forcing - "`. The entry has been detached, so the
field is now genuinely empty, matching the negative research above.

Two durable cautions follow. First, `"Solar-Forcing - "` is a rendering of an empty value and not a
value: it must never be written into this field, and never copied into anything sent to HSSI. Second,
a later refresh that finds this field empty should read it as a researched negative rather than an
unfilled gap. If a release is ever cut, the correct response is to record that release — never to
restore a blank entry to make the field look populated.

---

### 13. Programming Language (RECOMMENDED)

**Python 3.x**

Unchanged. `setup.py:15` sets `python_requires='>=3.7'` and lines 20-23 declare classifiers for
Python 3, 3.7, 3.8 and 3.9. The CI workflow runs Python 3.8 (`.github/workflows/deploy.yml:16`).
Every file under `solarforcing/` is Python 3.

*Considered and not selected:* nothing. GitHub reports the repository's dominant language as
"Jupyter Notebook", but the notebooks contain Python and "Jupyter Notebook" is not a row in the
`ProgrammingLanguage` vocabulary (19 rows). `Python 2.x` is excluded by `python_requires`.

---

### 14. Reference Publication (RECOMMENDED)

**Not found.**

No publication describes this software. The two PDFs in `docs/` are not candidates: they are the
papers whose algorithms the package implements, published 5 and 11 years before the repository
existed (see Field 27). There is no JOSS paper, no `CITATION.cff`, no "How to cite" section in
`README.md`, and no `preferred-citation` anywhere in the repository. SoMEF extracted no citation and
no identifier from the repository.

---

### 15. License (RECOMMENDED)

- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

The record held no license before this dossier. `MIT License` is a verbatim row in the live `License`
vocabulary (11 rows), whose stored URL is `https://spdx.org/licenses/MIT`.

**The conflict, and why MIT wins.** The repository states two different licenses:

- `LICENSE` contains the full MIT License text, "Copyright (c) 2021 National Center for Atmospheric
  Research".
- `setup.py:30` declares `license='Apache Software License 2.0'` and `setup.py:18` declares the
  classifier `'License :: OSI Approved :: Apache Software License'`.

MIT is authoritative for four independent reasons:

1. **The `LICENSE` file is the operative grant.** It is the actual licence text distributed with the
   software and the only place a licence is actually granted. `setup.py`'s `license=` string is
   descriptive packaging metadata with no legal effect.
2. **`LICENSE` names the copyright holder**, National Center for Atmospheric Research — a
   deliberate, project-specific choice. The `setup.py` strings name no holder.
3. **Chronology and provenance.** `LICENSE` was added in the repository's very first commit,
   `7f1379d` "Initial commit" (2021-06-16), i.e. chosen when the repository was created. `setup.py`
   did not exist until `c263aa2` "create package" (2021-08-05), seven weeks later, and arrived
   already carrying both Apache strings, together with the `"""The setup script."""` boilerplate
   characteristic of a cookiecutter project template. The Apache declaration was never reconciled
   with the pre-existing MIT `LICENSE` — it is unmodified template metadata, not a re-licensing.
4. **Independent detection agrees.** GitHub's SPDX license scan of the repository reports
   `{"key": "mit", "spdx_id": "MIT", "name": "MIT License"}`, and SoMEF independently surfaced both
   the MIT text and the Apache string, confirming the conflict is real and that the file-based
   detection lands on MIT.

**Rejected alternative:** `Apache License 2.0` (also a valid vocabulary row). It is rejected on the
grounds above. This is worth leaving on the record, because a future automated pass reading only
`setup.py` metadata will otherwise re-propose it.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- earth system model
- reproducible
- science
- xarray
- electron precipitation
- energetic particles
- geomagnetic index
- solar irradiance
- radiation belts
- ionosphere
- mesosphere
- thermosphere
- climate model
- space weather

The first four are the existing HSSI values, retained. Their stored form is lower case — the view
API renders them title-cased ("Earth System Model", "Xarray"), which is a display transform, not the
stored value. They originate from `setup.py:34`
(`keywords='reproducible,science,xarray,earth system model'`).

Each of the ten additions already exists as a row in the live `Keyword` vocabulary, so none of them
mints a new row or a near-duplicate. Reusing existing rows matters more here than for the form's
other controlled lists: Keywords is the one that creates a row for an unrecognized value instead of
rejecting it, so a careless keyword becomes a permanent near-duplicate rather than a caught error.
Their basis: `electron precipitation` and `energetic particles` for the 30–1000 keV precipitating
electron spectra that are the package's subject; `geomagnetic index` for the ap/Ap series that is
the model's only input; `solar irradiance` for the `SolarIrradiance` class and the NRL2 product it
processes;
`radiation belts` for the L 2–10.5 source region; `ionosphere`, `mesosphere` and `thermosphere` for
the 50–150 km deposition region; `climate model` for the CESM target; `space weather` for the
overall subject (the GitHub repository description calls the inputs "solar weather forcing data").

*Considered and not selected:* `waccm` — the comparison notebook `ipr_comparison.ipynb` reads a CAM
history archive whose case name (`fwhist_apmee_ipr_test01`) and fields (`APMEEionprs`,
`EPP_ionpairs`) point at a WACCM configuration, but nothing in the repository states this, so the
keyword would rest on inference from a path string. `kp index` — the downloaded file is the
Kp/ap/Ap/SN/F10.7 product, but the code reads only the `ap1`–`ap8` columns, so `geomagnetic index`
is the accurate term. `netcdf` and `NetCDF4` — redundant with Fields 18 and 19. `stratosphere` —
only the bottom 1 km of the 50–150 km profile is stratospheric.

---

### 17. Data Sources (OPTIONAL)

- GFZ
- FTP/FTPS Directories
- HTTP/HTTPS Directories

The record held no data source before this dossier. All three are verbatim rows in the live
`DataInput` vocabulary (17 rows).

- **GFZ** — `data_access.grab_potsdam_file()` defaults to
  `ftp://ftp.gfz-potsdam.de/pub/home/obs/Kp_ap_Ap_SN_F107/Kp_ap_Ap_SN_F107_since_1932.txt`
  (`solarforcing/data_access.py:7`, repeated as `FluxCalculation.ap_file_url` in
  `solarforcing/main.py:18`). The bundled sample `data/Kp_ap_Ap_SN_F107_2021.txt` carries the GFZ
  header ("SOURCE: Geomagnetic Observatory Niemegk, GFZ German Research Centre for Geosciences").
  The `GFZ` row has an empty `identifier`, which is normal for it and for three other rows in that
  vocabulary; it is a legitimate value.
- **FTP/FTPS Directories** — the index file is fetched over FTP, as the URL above shows. That URL
  still transfers successfully. Worth recording, because a 2021-vintage hard-coded FTP default is
  exactly the kind of thing a later pass would otherwise assume had rotted and quietly drop.
- **HTTP/HTTPS Directories** — `data_access.grab_ssi_lasp_file()` defaults to
  `https://lasp.colorado.edu/lisird/resources/lasp/nrl2/v02r01/ssi_v02r01_daily_s18820101_e20201231_c20210218.nc`
  (`solarforcing/data_access.py:72`), a direct HTTPS file fetch from LASP LISIRD. That URL also still
  resolves.

*Considered and not selected:* `Observatory/Mission-specific` — neither source is an observatory or
mission data service. GFZ publishes a derived planetary index; LISIRD here serves NRL2 *model*
output. `WDC` — the sunspot-number column in the GFZ file is credited to WDC-SILSO, but the code
never reads that column. `CDAWeb`, `HAPI`, `OMNIWeb`, `Madrigal`, `SSCWeb`, `AMDA`, `VirES`,
`das2`, `TAP`, `S3/Cloud-aware`, `The Virtual Solar Observatory.` — no client or URL for any of them
appears in the repository.

---

### 18. Input File Formats (RECOMMENDED)

- ascii
- netCDF3/4

The record held no input format before this dossier. Both are verbatim rows in the live `FileFormat`
vocabulary (11 rows).

- **ascii** — two distinct ASCII readers. `data_access.grab_potsdam_file()` parses the GFZ index file
  with `pd.read_csv(..., skiprows=39, header=0, delim_whitespace=True)`
  (`solarforcing/data_access.py:31`); the file itself documents its format as "ASCII, blank separated
  and fixed length". `data_access.read_atm()` parses the NRLMSIS 2.0 profile with
  `pd.read_table(file, header=0, sep='\s+')` (line 59).
- **netCDF3/4** — `data_access.grab_ssi_lasp_file()` opens the LASP NRL2 file with
  `xr.open_dataset()` (line 100). The notebooks additionally open the SOLARIS-HEPPA CCMI-2022
  forcing file (`apeep.ipynb`, `apply_to_dataset.ipynb`), CESM/CAM history files with
  `xr.open_mfdataset` (`ipr_comparison.ipynb`), and a locally produced comparison file
  (`compare_fluxes.ipynb`) — all netCDF.

*Considered and not selected:* `csv`. The notebook `calculate_flux_from_ap_csv.ipynb` has "csv" in
its name and the code calls `pd.read_csv`, but the file it reads is the whitespace-delimited GFZ
ASCII table read with `delim_whitespace=True` — there is no comma-separated input anywhere. This is
recorded because the notebook filename actively misleads. `HDF5`, `CDF`, `FITS`, `Zarr`,
`IDL.sav`, `JSON`, `ISTP-Compliant` — no reader for any of them.

---

### 19. Output File Formats (RECOMMENDED)

- netCDF3/4

The record held no output format before this dossier. The package's two data-delivery entry points,
`FluxCalculation.generate_dataset()` and `SolarIrradiance.generate_dataset()`, return in-memory
`xarray.Dataset` objects, and the documented way to persist them is netCDF:
`notebooks/calculate_flux_from_ap_csv.ipynb` ends with
`ds.to_netcdf('../data/vdk_flux_calc_test.nc')`. netCDF is also what the output is *for* — CESM
forcing input files are netCDF, and `data_cleaning.py` writes the CAM input-file conventions
(`date`, `datesec`, centered `time` against `time_bnds`, CF-style attributes) that only make sense
in a netCDF file.

*Considered and not selected:* every other row in the vocabulary — no other writer exists.
`ascii` in particular is input-only here.

---

### 20. Operating System (RECOMMENDED)

**Operating System Independent**

The record held no operating system before this dossier. `setup.py:25` declares the classifier
`'Operating System :: OS Independent'`, which is the project's own statement of portability, and
nothing in the repository is platform-specific: pure Python, no compiled extension, no shell
scripts, and all dependencies (`matplotlib`, `numpy`, `xarray`, `pandas`, `scipy`, `numba`,
`pydantic`, plus `cf-xarray` in the conda environment) ship for Linux, macOS and Windows on
conda-forge. CI corroborates by running the build on `ubuntu-latest`
(`.github/workflows/deploy.yml:15`).

**Trap avoided:** `OS Independent` — the literal classifier string — is *not* a row in the
`OperatingSystem` vocabulary and would be rejected. The correct row is `Operating System
Independent`, spelled out.

*Considered and not selected:* enumerating `Linux`, `Mac` and `Windows` individually. Only Linux is
directly evidenced (by CI); listing all three would go beyond the evidence, and listing Linux alone
would understate a package the authors declared platform-independent.

---

### 21. CPU Architecture (RECOMMENDED)

**CPU Independent**

The record held no CPU architecture before this dossier, and the repository declares no architecture
anywhere. `CPU Independent` is recorded on the same basis as Field 20: the distribution is pure
Python source with no compiled artifact, wheel, or architecture-specific code path, alongside an
explicit `OS Independent` classifier.

**Caveat, recorded so a later refresh does not treat this as unexamined.** `solarforcing/calc.py:2`
imports `numba`, and `calc.py` is imported at package import time via `solarforcing/__init__.py:4`,
so numba is a hard runtime requirement. That makes the practical architecture set whatever numba's
LLVM backend supports (x86-64, arm64 including Apple Silicon and Linux aarch64, ppc64le) rather than
literally every CPU. A reviewer who prefers to state that explicitly could replace this value with
the enumerated architecture rows; the evidence supports either reading, and neither is contradicted
by anything in the repository.

---

### 22. Related Phenomena (OPTIONAL)

**Geomagnetic Storms**

The record held no phenomenon before this dossier. `Geomagnetic Storms` is a verbatim row in the live
`Phenomena` vocabulary, which holds 7 flat rows.

The implemented model is, by its own title, "A model providing long-term data sets of energetic
electron precipitation **during geomagnetic storms**" (van de Kamp et al. 2016, quoted in the
docstring context at `solarforcing/calc.py:42` and in the notebook markdown). Its sole driver is the
ap geomagnetic activity index. `apeep.ipynb` is organized around storm case studies — "Take a look
at a solar storm from April 2020", "select maximum in geomagnetic storm in April 2010".

*Considered and not selected:* `Solar Wind` (no solar wind data or physics; the ap index is a
consequence of solar wind driving, not a solar wind measurement), `Coronal Mass Ejections`,
`Solar Flares`, `Solar Corona`, `Coronal Heating`, `X-ray emission` — none appear.

**Documented gap.** The phenomenon this software is actually about — energetic/medium-energy
electron precipitation — has no row in this closed vocabulary, and the vocabulary rejects custom
values. It is captured in Field 16 instead (`electron precipitation`, `energetic particles`), which
is where the field guidance directs unlisted phenomena.

---

### 23. Development Status (RECOMMENDED)

**Abandoned**

The record held no development status before this dossier. `Abandoned` is a verbatim row in the live
`RepoStatus` vocabulary (8 rows). The repostatus.org definition is "Initial development started but
abandoned; no stable release", and every clause matches:

- *Initial development started* — 52 commits between 2021-06-16 and 2022-01-13.
- *Abandoned* — the GitHub repository is archived (`archived: true`), it has been read-only since,
  and there has been no commit in over four years.
- *No stable release* — no tag, release, PyPI or conda-forge distribution, or DOI (Field 12). The
  project's own classifier is `'Development Status :: 2 - Pre-Alpha'` (`setup.py:17`).

*Considered and rejected:*

- `Inactive` ("reached stable, usable state but no longer actively developed") — the premise fails.
  The project never reached a stable, usable release, by its own Pre-Alpha declaration and by the
  total absence of releases.
- `Unsupported` ("reached stable, usable state but authors ceased work; new maintainer desired") —
  same failed premise, and archiving signals the opposite of seeking a maintainer.
- `WIP` ("initial development in progress") — accurate in 2022, contradicted by archiving.
- `Suspended` ("stopped temporarily; authors intend to resume") — archiving is the explicit signal
  that resumption is not intended.
- `Moved` — no successor project is identified anywhere in the repository, the README, or the
  archived GitHub metadata. If a successor is later identified, this is the value to revisit.

---

### 24. Documentation (RECOMMENDED)

**https://github.com/NCAR/solar-forcing**

The record held no documentation URL before this dossier. The value recorded is the repository root,
which is what the project itself declares: `setup.py:40` sets `project_urls['Documentation'] =
'https://github.com/NCAR/solar-forcing'`. `README.md:5-42` is a complete installation guide (clone,
`conda env create -f envs/environment.yml`, `conda activate solar-forcing-dev`, `pip install -e .`,
launch JupyterLab and open `notebooks/`), which satisfies the field's requirement for
"documentation and installation instructions"; the field explicitly permits reusing the access URL.

**Negative result — the Jupyter Book site is not live.** `.github/workflows/deploy.yml` builds
`notebooks/` with `jupyter-book` and publishes `notebooks/_build/html` to the `gh-pages` branch on
every push to `main`, and that branch does exist with built output (last built 2022-01-13,
containing `index.html` and per-notebook pages). But GitHub Pages is not enabled for this
repository: the repository API reports `has_pages: false`, `/repos/NCAR/solar-forcing/pages`
returns 404, and `https://ncar.github.io/solar-forcing/` returns 404 (also checked for
`/intro.html` and `/simplified_api_example.html`). The Internet Archive availability API holds no
snapshot of that URL at all. The repository's own `homepage` metadata field still advertises
`https://ncar.github.io/solar-forcing` — that value is stale and must not be recorded here.

A future maintainer who needs the rendered book can read the `gh-pages` branch directly at
`https://github.com/NCAR/solar-forcing/tree/gh-pages`; it is not recorded as the documentation URL
because it serves raw HTML source rather than a rendered site.

*Considered and rejected:* `https://github.com/NCAR/solar-forcing/tree/main/docs` — SoMEF proposed
this as the documentation URL, but `docs/` contains only two third-party journal PDFs (Field 27) and
no documentation of this software.

---

### 25. Funder (OPTIONAL)

**Not found.**

**Negative research.** No acknowledgement, funding statement, grant number or sponsor appears in
`README.md`, `setup.py`, any module under `solarforcing/`, `requirements.txt`,
`envs/environment.yml`, `.github/workflows/deploy.yml`, `notebooks/_config.yml`, or the source of
any of the six notebooks. The search covered *acknowledg*, *funding*, *grant*, *NSF*, *sponsor* and
*cooperative agreement*, case-insensitively, and produced exactly one match in the whole repository:
the letters "nsf" inside the word `transform` in a cartopy plotting call
(`notebooks/ipr_comparison.ipynb`). There is no reference publication (Field 14) whose
Acknowledgments could supply one, and no DOI record (Field 2) whose `fundingReferences` could.

**Two funder attributions that must not be imported, and why.**

1. *From the bundled PDFs.* `docs/2010GL045406.pdf` (Fang et al. 2010) acknowledges "NASA grants
   NNX09AI04G and NNX06AC05G. NCAR is sponsored by NSF", and `docs/2015JD024212.pdf`
   (van de Kamp et al. 2016) acknowledges the Academy of Finland (projects 258165, 265005, 292806,
   276926) and NERC grant NE/J008125/1 — the latter also surfacing in Crossref's funding block for
   that DOI. Those fund the *papers whose algorithms this package implements*, published in 2010 and
   2016. They are not funding for this software and must not be copied into this record.
2. *By institutional inference.* NCAR is an NSF-sponsored centre and both authors were associated
   with it, so "National Science Foundation" is a plausible funder. It is not recorded, because
   plausibility is not evidence and no award, cooperative agreement or acknowledgement ties this
   package to it. If a maintainer supplies one, this is the field to fill.

---

### 26. Award Title (OPTIONAL)

**Not found.**

- **Award Title:** Not found
- **Award Number:** Not found

Same negative research as Field 25.

**Why this field is empty rather than simply unfilled.** The record previously carried an award
entry that held no award information whatsoever — an empty title, an empty award number and no
funding organization. It has been unlinked, so the field is now genuinely empty, matching the
negative research above.

One durable caution attaches to that blank award entry, because it is **shared**: the same empty
record is also referenced by ndcube, SolarProtons, Solar Soft and stokespy in this HSSI instance.
Unlinking it from Solar-Forcing is safe and affects nothing else. *Deleting* the shared entry itself
is not safe — that would strip those four other software records of their award lists as well.
Whether they should also be unlinked is a question about those records, not about this one.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

- **https://doi.org/10.1002/2015JD024212** — van de Kamp, M., Seppälä, A., Clilverd, M. A., Rodger,
  C. J., Verronen, P. T., & Whittaker, I. C. (2016). A model providing long-term data sets of
  energetic electron precipitation during geomagnetic storms. *Journal of Geophysical Research:
  Atmospheres*, 121(20), 12,520–12,540.
- **https://doi.org/10.1029/2010GL045406** — Fang, X., Randall, C. E., Lummerzheim, D., Wang, W.,
  Lu, G., Solomon, S. C., & Frahm, R. A. (2010). Parameterization of monoenergetic electron impact
  ionization. *Geophysical Research Letters*, 37(22), L22106.
- **https://doi.org/10.1175/BAMS-D-14-00265.1** — Coddington, O., Lean, J. L., Pilewskie, P.,
  Snow, M., & Lindholm, D. (2016). A solar irradiance climate data record. *Bulletin of the American
  Meteorological Society*, 97(7).

The record held no related publication before this dossier.

**Identification of the two bundled PDFs.** `docs/2015JD024212.pdf` and `docs/2010GL045406.pdf` are
named for their DOI suffixes; both were opened and their first pages confirm the identifications
above against the Crossref records. They were added in commit `7f32513` "added docs directory for
relevant source articles".

**Why these are Related Publications and not the Reference Publication.** Neither describes this
software — they predate it by 11 and 5 years and describe the algorithms it implements. The
repository cites them as its scientific basis in exactly that role:
`solarforcing/calc.py:42` documents `vdk2016()` as "Calculations here are defined by van de Kamp
et al. 2016 (doi:10.1002/2015JD024212)", and the notebook markdown in `apeep.ipynb` and
`apply_to_dataset.ipynb` gives both full citations and states that `fang()`/`iprmono()` implement
"the parameterization described in Fang et al., (2010)". Field 14 is therefore correctly empty.

**Why Coddington et al. (2016) is included.** It is cited by the software's own code, not merely by
its documentation: `data_cleaning.add_global_attrs()` writes it verbatim into every output dataset as
`ds.attrs['data_reference']` (`solarforcing/data_cleaning.py:19-22`). It is the reference for the
NRL2 solar irradiance record the `SolarIrradiance` class processes.

*Considered and not selected:*

- **Matzka et al. (2021), doi:10.1029/2020SW002641** ("The geomagnetic Kp index and derived indices
  of geomagnetic activity") — the "PLEASE CITE" reference in the header of the GFZ index file the
  software downloads. It describes the *input dataset* rather than the software or its algorithms,
  so its natural home is Field 28, where the corresponding data DOI is recorded.
- **Clette & Lefevre (2016), doi:10.1007/s11207-016-1014-y** (sunspot number) and **Tapping (2013),
  doi:10.1002/swe.20064** (F10.7) — also cited in that same GFZ file header, but the code reads only
  the `ap1`–`ap8` columns and never touches the sunspot-number or F10.7 columns. Including them
  would attribute to the software a use it does not make.
- No publication was found that cites or uses Solar-Forcing itself. DataCite has no record referring
  to the repository, and an ADS/SciX full-text search for the unambiguous repository path
  `"NCAR/solar-forcing"` — the string a software-availability statement would carry — returns 0
  documents. That search is functioning rather than silently empty: the control query
  `full:"github.com/NCAR"` — deliberately the same shape of query, a GitHub repository path under the
  same organization — returns 210 documents against the same index. So the full-text index does
  surface NCAR GitHub paths when papers cite them; it simply contains none citing this repository.
  Searching for `solarforcing` or `solar-forcing` alone is not usable evidence, because the index
  tokenizes those into the ordinary phrase "solar forcing" and returns hundreds of unrelated
  solar-variability papers.

---

### 28. Related Datasets (OPTIONAL)

- **https://doi.org/10.5880/Kp.0001** — Matzka, J., Bronkalla, O., Tornow, K., Elger, K., & Stolle,
  C. (2021). *Geomagnetic Kp index*. V. 1.0. GFZ Data Services. [Dataset]

The record held no related dataset before this dossier. This is the dataset that
`data_access.grab_potsdam_file()` downloads and parses — the primary input to the entire
precipitation calculation. The DOI is taken from the data
file's own header ("Data publication: … https://doi.org/10.5880/Kp.0001") and was verified against
DataCite, which returns title "Geomagnetic Kp index", publisher "GFZ Data Services", publication
year 2021, resource type Dataset.

*Considered and not selected:*

- **The LASP LISIRD NRL2 daily spectral solar irradiance record** — the other primary input
  (`solarforcing/data_access.py:72`). No DOI could be found for it: the LISIRD `nrl2_files` landing
  page as served exposes no DOI string, and a DataCite search for the NRLSSI2 / solar spectral
  irradiance climate data record returns no matching dataset record. The dataset's describing
  publication is instead recorded in Field 27 (Coddington et al. 2016), which is the field guidance's
  stated fallback.
  If a DOI is later minted for this record, this is the field to add it to.
- **The SOLARIS-HEPPA CCMI-2022 solar forcing file**
  (`solarforcing-REFD1-day_input4MIPs_solar_CCMI-2022_SOLARIS-HEPPA-3-2_gn_19500101-20191231.nc`),
  opened in `apeep.ipynb` and `apply_to_dataset.ipynb` as the reference to validate against. It is a
  comparison target rather than a dataset the software provides functionality for, and no DOI for
  that specific input4MIPs file was found (a DataCite search returns only the generic
  `PCMDI/input4MIPs_CVs` software record).
- **`data/msis2.0_atm_out.txt`** — bundled NRLMSIS 2.0 output, generated for this repository rather
  than published; the repository does not record which MSIS build or run produced it, and there is no
  DOI.
- **`RBSP-ECT_FB_precip.nc`** — read by `compare_fluxes.ipynb` but not distributed with the
  repository and not published under any identifier found.

---

### 29. Related Software (OPTIONAL)

- **https://svn.code.sf.net/p/codescripts/code/trunk/ncl/solar** — `createSolarFileNRLSSI2.ncl`, the
  NCL script this package's solar-irradiance workflow was migrated from.

The record held no related software before this dossier.

This is a genuine predecessor, which is exactly what the field asks for. The evidence is explicit and
appears in two independent places: `notebooks/simplified_api_example.ipynb` states "this workflow has
been migrated from its original state based on [Mike Mill's
script](https://svn.code.sf.net/p/codescripts/code/trunk/ncl/solar/createSolarFileNRLSSI2.ncl)", and
`data_cleaning.add_global_attrs()` (`solarforcing/data_cleaning.py:9,13-14`) preserves the lineage in
the output metadata itself — the function's docstring says "modified from
https://svn.code.sf.net/p/codescripts/code/trunk/ncl/solar", and it writes
`data_script = "Created by program createSolarFileNRLSSI2.ncl"` and the matching `data_script_url`
into every dataset it produces. The directory URL is recorded rather than the script's file URL
because the directory is what both the docstring and the emitted `data_script_url` attribute point
at, and it is the location a user would browse. No DOI exists for it.

*Considered and not selected:*

- **The Community Earth System Model** — a real and important relationship, but it belongs in
  Field 30, where it already is: CESM consumes this package's output rather than performing a
  similar task or preceding it.
- **NRLMSIS 2.0** — the ionization calculation cannot run without an MSIS profile, but what the
  repository contains is a static output *file*, not a dependency on the model software; MSIS is
  never installed, imported or invoked, and the repository does not identify which MSIS
  implementation produced the file.
- **numba, pydantic, cf-xarray, numpy, scipy, pandas, matplotlib, xarray** — the declared
  dependencies (`requirements.txt`, `envs/environment.yml`). All are generic scientific-Python or
  general-purpose infrastructure: a JIT compiler, a data-validation library, arrays, dataframes,
  plotting, CF-convention accessors. Each would be equally at home in a web application or a finance
  model, and listing them would say nothing that is not equally true of most of the ecosystem.
  (`cf_xarray` is additionally a dead import — `solarforcing/data_cleaning.py:3` imports it and no
  code in the repository ever uses the `.cf` accessor.)
- **`jupyter-book`** — the documentation build tool pinned in `notebooks/requirements.txt`; tooling,
  not related software.

---

### 30. Interoperable Software (OPTIONAL)

- **https://doi.org/10.5281/zenodo.11229775** — Community Earth System Model (CESM)
- **https://doi.org/10.5281/zenodo.598201** — xarray

**CESM (retained from the existing HSSI record, and confirmed correct).** The stored entry's name in
the HSSI database is the placeholder string `UNKNOWN`, which is a storage artifact of how related
items were created and is not user-visible; the DOI is the meaningful value, and it resolves as
follows. `10.5281/zenodo.11229775` is a Zenodo *concept* DOI that redirects to record 11229776,
"CESM-release-cesm2.2.0", creator "CESM Team" (NCAR), resource type Software, published 2024-05-21 —
i.e. the Community Earth System Model. The concept DOI is the right form to store, since it denotes
all versions.

The interoperability claim is correct and unusually well evidenced, in both directions:

- *Output flows to CESM.* Generating CESM forcing input is the package's stated purpose
  (`README.md:3`, `setup.py:28`), and `solarforcing/data_cleaning.py` writes CESM-specific
  conventions into the product — `add_datesec()` and `add_date()` synthesize the `date` and
  `datesec` fields CAM input files require (lines 74-87), `center_time()` places `time` at the
  centre of `time_bnds` (line 54), and `add_global_attrs()` stamps `ds.attrs['cesm_contact']`
  (line 15).
- *CESM output flows back in.* `notebooks/ipr_comparison.ipynb` opens CESM/CAM history files
  (`xr.open_mfdataset(ipr_test_dir + 'fwhist_apmee_ipr_test01.cam.h1*.nc')`) and compares the model's
  `APMEEionprs` and `EPP_ionpairs` fields against this package's calculation.

**xarray.** This is recorded because it meets the field's stated
Tier B bar exactly rather than on dependency presence: `xarray.Dataset` is the package's *documented
interchange format*. Each entry point that delivers a finished forcing product returns one —
`calc.calculate_iprm()` documents
"Returns … xarray.Dataset with IPRM values" (`solarforcing/calc.py:271-273`), and
`FluxCalculation.generate_dataset()` and `SolarIrradiance.generate_dataset()`
(`solarforcing/main.py:53`, `:92`) both return Datasets that users then merge, subset, plot and write
to netCDF. `10.5281/zenodo.598201` is xarray's Zenodo concept DOI (verified against DataCite: title
"xarray", type Software).

The narrower reading of this field — heliophysics or domain-science peer tools only, which would
exclude xarray — was considered and rejected. The field asks about documented data exchange, and
xarray is the format in which this package delivers its finished products rather than an
implementation detail: both public workflow classes hand back an `xarray.Dataset` from
`generate_dataset()` (`main.py:53`–`80` for the precipitation forcing, `main.py:92`–`110` for the
irradiance forcing), and that Dataset is what a user writes to the netCDF file CESM consumes.

The Tier A dependencies below stand in a different relationship, and the distinction is narrower than
"they never surface publicly" — numpy and pandas do appear in the package's public return types. The
`calc.py` utilities re-exported through `solarforcing/__init__.py` document `numpy.array` returns,
and `grab_potsdam_file` returns a pandas DataFrame (`data_access.py:49`). What separates them is that
those types carry intermediate values *within* the workflow rather than serving as the interchange
format for anything the package produces, and neither has an exchange, adapter, or plugin
relationship with this software. xarray is nonetheless absent from Field 29,
for the complementary reason that it is neither a predecessor nor a similar-purpose tool. The CESM
entry stands independently of this one.

*Considered and not selected:* **numba, pydantic, cf-xarray, numpy, scipy, pandas, matplotlib** —
Tier A generic infrastructure, excluded on the same grounds given in Field 29. Being a dependency is
not interoperability, and no exchange, adapter, converter or plugin relationship with any of them
appears in the public API, the docstrings, the notebooks or the environment files.

---

### 31. Related Instruments (OPTIONAL)

**Not found — no instrument passes the relevance gate.**

The record holds no instrument, which is correct. Nothing is left dangling in an unresolved state:
each candidate below was excluded on relevance, so this emptiness is a researched negative rather
than an unexamined gap.

The search space was the whole live `InstrumentObservatory` vocabulary — 7,648 rows, of which 4,513
are instruments (`type: 1`) and 3,135 observatories (`type: 2`) — so the negative below rests on the
full list rather than a sample. Every row in it carried an identifier beginning
`https://spase-metadata.org/`, with no non-SPASE rows, consistent with the PR #54 backfill. Treat
that as a dated observation rather than a guarantee: a later refresh should re-check it, because a
row lacking a SPASE identifier would signal upstream drift and must be reported rather than used.

**Candidates searched and why each was excluded** — recorded so a later pass does not re-derive them:

- **Niemegk / GFZ magnetometer instruments.** The vocabulary offers several plausible rows
  (`https://spase-metadata.org/SMWG/Instrument/Ground/Niemegk/Magnetometer`,
  `.../SMWG/Instrument/WDC/Niemegk/Magnetometer`,
  `.../IUGONET/Instrument/WDC_Kyoto/WDC/NGK/Magnetometer`, and Potsdam equivalents). Excluded at the
  relevance stage, before any ambiguity question arises: the software downloads GFZ's *planetary*
  Kp/ap index product, which is derived from a 13-observatory network, and Niemegk is the producing
  institution rather than the measurement source. The software parses no magnetometer data. The
  correct home for this relationship is Field 17, where `GFZ` is recorded.
- **POES / MEPED.** `https://spase-metadata.org/SMWG/Observatory/POES` exists (with a `.html`
  duplicate) but no MEPED instrument row does. Excluded because the van de Kamp model was *fitted to*
  POES/MEPED precipitation data over 2002–2012 by its authors; this package implements only the
  resulting closed-form empirical expression and never reads POES data. The satellite data is
  upstream of the model, not an input the software supports.
- **Van Allen Probes / RBSP ECT and FIREBIRD.** `notebooks/compare_fluxes.ipynb` opens
  `../data/RBSP-ECT_FB_precip.nc` and plots `RBSP_flux`, `RBSP_flux_fit` and `RBSP_flux_scaled`
  against the van de Kamp spectra. Excluded because that file is not distributed with the repository,
  is produced elsewhere, and nothing under `solarforcing/` reads RBSP or FIREBIRD data — this is a
  one-off validation comparison, which the relevance gate excludes explicitly. (For the record:
  `https://spase-metadata.org/SMWG/Observatory/RBSP` and its A/B rows do exist; no FIREBIRD row
  exists in the vocabulary at all.)
- **SORCE / TSIS / other irradiance instruments.** The package downloads NRL2, which is a *model*
  product served by LASP LISIRD; it is calibrated against instrument records but is not an instrument
  data product, and the software reads no instrument file. (`SMWG/Observatory/SORCE` and its four
  instrument rows exist; no TSIS row was found.)
- **Dominion Radio Astrophysical Observatory (F10.7).** Handled under Field 32.

---

### 32. Related Observatories (OPTIONAL)

**Not found — no observatory passes the relevance gate.**

The record holds no observatory, which is correct, and nothing is left unresolved here either.

The observatory-side candidates are the same set examined in Field 31 and are excluded for the same
reasons, with one addition worth recording separately:

- **Dominion Radio Astrophysical Observatory** — exactly one matching row exists
  (`https://spase-metadata.org/SMWG/Observatory/DRAO`, `type: 2`), so it would resolve cleanly if it
  were relevant. It is not. DRAO produces the F10.7 solar radio flux, which is one of the columns in
  the GFZ file the software downloads — but `grab_potsdam_file()` reads only `ap1` through `ap8`,
  averages them, and returns `df[['ap']]` (`solarforcing/data_access.py:46-49`). The F10.7 columns
  arrive in the downloaded file and are then discarded. Downloading a file that happens to contain a
  measurement is not being designed to support the observatory that made it.
- **Niemegk / Potsdam geomagnetic observatories** — several observatory rows exist
  (`SMWG/Observatory/Ground/Niemegk`, `SMWG/Observatory/WDC/Niemegk`,
  `SMWG/Observatory/IAGA/NGK`, `IUGONET/Observatory/WDC_Kyoto/WDC/NGK`, and Potsdam equivalents).
  Excluded on relevance, as explained in Field 31; a user searching HSSI for
  `observatory:"Niemegk"` is looking for magnetometer tooling, not a CESM forcing generator.
- **POES**, **Van Allen Probes** — excluded on relevance, as explained in Field 31.

There is no CESM row in this vocabulary, and there should not be: CESM is a model, and its
relationship to this software is recorded in Field 30.

---

### 33. Logo (OPTIONAL)

**Not found.**

No image file exists in the source tree (a listing of every tracked path at `5e7baf7` returns no
`.png`, `.jpg`, `.gif`, `.svg`, `.ico` or `.webp` file; the separate `gh-pages` branch holds
generated plot PNGs, which are build output and not a logo), `README.md` embeds no image and carries
no badges, `notebooks/_config.yml` sets no
`logo:` key, and SoMEF extracted no `logo` result. The package is not registered with PyHC, so no
curated logo is available from that source either.

---

## Cross-cutting notes

### PyHC registry

Solar-Forcing is **not** a PyHC package. All three registry files were downloaded and parsed in full
(`projects_core.yml`, 7 entries; `projects.yml`, 57 entries; `projects_unevaluated.yml`, 29 entries),
and every `name` and `code` field was inspected. No entry matches this package by name
(`solar-forcing`, `solarforcing`, `Solar-Forcing`), by repository URL, or by description. Other
NCAR-authored software is registered — `GCMprocpy` in the community list points at
`https://github.com/NCAR/gcmprocpy.git`, and `GLOW` in the unevaluated list is described as
"NCAR GLOW 0.981 aurora/airglow model IR-VIS-UV from Python" — so the absence of this package is a
specific fact about this package, not a general absence of NCAR software from PyHC. Absence from
PyHC is not a defect; it simply means no curated PyHC metadata exists to supplement or override the
values above.

### Installability caveat (context for Fields 20, 21 and 29)

`setup.py:7-8` feeds `requirements.txt` directly into `install_requires`. That file lists
`matplotlib, numpy, xarray, pandas, scipy, numba, pydantic, datetime` — it omits `cf-xarray`, which
`solarforcing/data_cleaning.py:3` imports at module load and which `solarforcing/__init__.py`
reaches transitively, and it includes `datetime`, a PyPI package that shadows the standard library
module of the same name. A bare `pip install` of the distribution would therefore not produce a
working import. The documented installation path in `README.md` avoids both problems, because
`envs/environment.yml` does include `cf-xarray` and does not include `datetime`. This does not change
any recorded value; it is noted so a future refresh understands why the two dependency lists differ
and does not read the divergence as evidence about platform support.
