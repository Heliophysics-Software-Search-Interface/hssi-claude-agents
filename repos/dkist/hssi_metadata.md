# HSSI Metadata Extraction Results

**HSSI Software ID:** 68f29968-0830-437d-a249-ba47ac22b0b4
**Repository:** https://github.com/DKISTDC/dkist
**Source Revision:** 8ce3cc9b34116e4d58211ed2824629f2828c3e0f
**Extraction Date:** 2026-07-30
**Validation Date:** 2026-08-20
**Validation Status:** PASS
Metadata for the DKIST User Tools (`dkist`) Python package, derived from the repository at the source
revision above (tag `v1.18.0` plus 8 commits) together with the project's own Zenodo/DataCite release
metadata, PyPI, conda-forge, ror.org and ORCID. Every field carries its evidence. Controlled-list
values are quoted verbatim from the HSSI controlled vocabularies; Fields 31 and 32 are resolved to
SPASE identifiers.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.18494047

- This is the Zenodo **concept** DOI, which is what the field asks for ("the concept DOI for all
  versions"). An earlier record held `https://zenodo.org/records/18494048` — a version-record URL for
  v1.17.0, which is neither a DOI nor a concept identifier.
- Evidence: both dkist Zenodo records report `conceptdoi = 10.5281/zenodo.18494047` and
  `conceptrecid = 18494047`; DataCite for `10.5281/zenodo.18494047` resolves to the latest version
  (v1.18.0) and carries `IsVersionOf` relations from the version DOIs. The version-specific DOI belongs
  in Field 12 (Version PID), not here.

### 3. Code Repository (MANDATORY)
https://github.com/DKISTDC/dkist

*Evidence:* `pyproject.toml` `[project.urls]` `Homepage` / `Source Code`, and `.cruft.json`
`sourcecode_url`.

### 4. Software Functionality (MANDATORY)

- Coordinate Transforms
- Coordinate Transforms: Mission-Specific
- Coordinate Transforms: Solar
- Data Processing and Analysis
- Data Processing and Analysis: 2D Slices
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 2D Slices
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: Movies
- Mission-related
- Mission-related: Analysis
- Mission-related: Archive
- Mission-related: Distribution/Access
- Mission-related: Inventory

All 19 values are drawn from the HSSI software-functionality vocabulary, and every subcategory is
listed together with its parent category.

**Evidence by group**

- *Coordinate Transforms (+ Solar, Mission-Specific).* `dkist/wcs/models.py` implements the
  DKIST-specific gWCS machinery — `generate_celestial_transform`, `VaryingCelestialTransform`
  (1D/2D/3D and their inverses), `CoupledCompoundModel`, `AsymmetricMapping`, `Ravel`/`Unravel`, and
  `varying_celestial_transform_from_tables` — which produce the celestial (helioprojective) transforms
  used by every DKIST dataset. `dkist.net.attrs.BoundingBox` transforms any supplied frame to
  `sunpy.coordinates.Helioprojective(observer="earth")` before searching. Loaded datasets expose
  full gWCS world/pixel conversion; `docs/examples/example_cryo_plots.md` converts Cryo-NIRSP
  spectrograph slit positions into Context Imager pixel coordinates. The varying/coupled transforms
  and ravel models exist specifically to describe DKIST instrument scan geometry, which is what makes
  the Mission-Specific child apply in addition to Solar. *Acknowledged reinterpretation:*
  `Mission-Specific` is normally framed around spacecraft frames (instrument pointing, attitude,
  field of view, SPICE kernels). DKIST is ground-based, so there is no spacecraft attitude or SPICE
  kernel case here; the value is claimed on the closest available reading — per-exposure, scan-varying
  instrument geometry that is specific to one observatory's instruments and is implemented in this
  package rather than inherited from `sunpy`/`astropy`. Defensible but not literal; noted so a reader
  can judge it rather than assume a spacecraft-frame case.
- *Data Processing and Analysis (+ Data Access and Retrieval, 2D Slices, Data Reduction,
  Processing).* `dkist.net.DKISTClient` is a `sunpy.net.Fido` client that searches the DKIST Data
  Center dataset inventory and fetches dataset ASDF files; `dkist.io.DKISTFileManager.download()`
  starts Globus transfers, `.quality_report()` downloads the PDF or JSON quality report, and
  `.preview_movie()` downloads the preview movie; `dkist.net.transfer_complete_datasets()` transfers
  whole datasets; `dkist.data.sample` downloads sample datasets over HTTPS. Slicing is a first-class
  operation: `Dataset.__getitem__` slices data, WCS and the FITS header table together,
  `TiledDataset.slice_tiles` reduces mosaic tiles to 2D, and `StripedExternalArrayView` keeps file
  references consistent through a slice. Data reduction is documented in
  `docs/examples/rebinning_and_dask.md` (`ds.rebin((1, 5, 1, 10))`) and
  `docs/examples/example_cryo_plots.md` (`sp.rebin((-1,-1,1), function=np.sum)`). General
  `Processing` covers the remaining structural operations the package implements itself: masking
  (`TiledDataset.mask`), cropping, flattening (`TiledDataset.flat`), header-table slicing
  (`Dataset._slice_headers`) and lazy per-file array assembly (`dkist/io/dask/striped_array.py`).
- *Data Visualization (+ 2D Graphics, 2D Slices, Line Plots, Mission-Specific, Movies).*
  `TiledDataset.plot()` builds a WCSAxes gridspec mosaic of image tiles with shared z-scaling and
  optional axis inversion (`swap_tile_limits`, needed for DL-NIRSP) and titles drawn from the DKIST
  inventory record; `Profiles.plot()` draws a grid of original and fitted Stokes I/Q/U/V spectral
  profiles; `Inversion.plot()` plots Level 2 inversion products. Line plots are documented
  in `docs/tutorial/7_visualization.md` (`ds.plot(fig=fig, plot_axes=[None, None, 'x', None])`).
  Movies: for datasets with more than two dimensions `Dataset.plot()` returns a slider-driven
  animated figure, and the tutorial documents "click the play button at the side of each slider to
  animate the plot and loop through all those values"; figure tests pin `mpl_animators` versions
  (`dkist/tests/helpers.py`). `DKISTFileManager.preview_movie()` additionally retrieves the DKIST
  preview movie for a dataset.
- *Mission-related (+ Distribution/Access, Inventory).* `docs/topic_guides/usertools.rst`: "The
  `dkist` package is developed by the DKIST Data Center team". Distribution/Access: the Globus
  OAuth/endpoint/transfer layer in `dkist/net/globus/` plus `DKISTFileManager.download()` and
  `transfer_complete_datasets()` are the supported route for getting DKIST Level 1 files out of the
  Data Center. Inventory: `dkist/utils/inventory.py` defines `INVENTORY_KEY_MAP` with ~60 DKIST
  inventory keys and `humanize_inventory`/`dehumanize_inventory`/`path_format_inventory`;
  `Dataset.inventory` and `TiledDataset.inventory` expose the dataset inventory record, and
  `DKISTQueryResponseTable` renders it.
- *Mission-related: Archive.* Repository evidence supports this as the mission archive's official
  **client**: it queries the DKIST Data Center dataset search service, retrieves archived Level 1
  ASDF metadata, FITS data, quality reports and preview movies, and exposes archive-side provenance
  (`Recipe`, `WorkflowName`, `WorkflowVersion`, `SummitSoftwareVersion`, `Status`, embargo state). It
  is **not** archive infrastructure. Recorded on that client reading, which is noted here so a reader
  who takes this category to mean archive infrastructure exclusively can see the basis of the choice.
- *Mission-related: Analysis.* This value rests on a **mission-designation argument only**, and no
  attempt is made to dress it up as a demonstrated analysis capability. What is present-tense and
  sourced is the package's *role*: `docs/topic_guides/usertools.rst` states "The `dkist` package is
  developed by the DKIST Data Center team, and it is designed to make it easy to obtain and use DKIST
  data in Python", and `docs/index.rst` line 6 reads "The DKIST Python tools provide a package
  (`dkist`) which aims to help you search, obtain and use DKIST data as part of your Python software."
  So this is the DKIST Data Center's own library through which analysis of DKIST data is done — which
  is what the `Mission-related` category is about (a mission's own tooling) rather than what
  `Data Processing and Analysis` is about (implemented algorithms).
  What is **not** claimed: that DKIST-specific analysis *routines* ship today. The same guide says
  "there *isn't actually a lot of code* in the `dkist` package" and that users "will mostly not be
  (directly) using functionality provided by the `dkist` package", and its closing line — "It is
  expected that any community developed analysis software that is explicitly DKIST specific will also
  be included in the `dkist` package in the future" — is **future intent, not current functionality**,
  so it is not offered as evidence. A search of the package for statistical or
  derived-physical-quantity code (`scipy`, `np.mean/std/median/percentile/polyfit/histogram`,
  `curve_fit`, `.fit(`) returns nothing outside tests. The value is kept because someone searching for
  DKIST mission analysis tooling should find this package.

**Earlier unsupported values**

An earlier record carried four `Mission-related:*` children, two of which are not supported by the
source. Both were removed; the reasons are recorded here so the omission is not read as a gap.

- *Mission-related: Calibration* — the package performs no calibration. A search of the whole package
  for dark/flat-field/gain/bias handling returns nothing, and `docs/topic_guides/level1data.rst`
  states the Level 1 data it consumes "has been calibrated to remove any effects introduced by the
  telescope or instruments" *before* distribution. `dkist/net/client.py` records
  `sunpy.net.attrs.Level: [("1", "DKIST data calibrated to level 1.")]` — the software selects
  already-calibrated data. Every calibration-related name in the package is *metadata about someone
  else's calibration*: the `Recipe`, `WorkflowName`, `WorkflowVersion` search attributes, the
  `Calibration Workflow Name/Version`, `Input Dataset Calibration Frames Part ID` and
  `Calibration Documentation URL` inventory keys, and the `calibration_input_frames` property in
  `dkist/io/asdf/resources/schemas/dataset-1.3.0.yaml`. Calibration is done by the separate
  `dkist-processing-*` Level 0 → Level 1 workflows (their names, e.g. `l0_to_l1_visp`, appear only as
  *search values* in `dkist/data/api_search_values.json`).
- *Mission-related: Science Data Processing* — for the same reason: DKIST science data processing is
  the Data Center's Level 0 → Level 1 pipeline, which lives in other packages. This package's
  user-side processing (slicing, rebinning, masking, saving) is already captured by
  `Data Processing and Analysis` and its `Processing` / `Data Reduction` children.

**Considered and excluded, with reasons**

- `Data Processing and Analysis: Analysis` — an earlier revision of this record carried it, but it
  does not survive re-examination against the subcategory's definition ("statistical methods, derived
  physical quantities, scientific calculations"). The package contains no such code: `scipy` is never
  imported anywhere; `np.mean`, `np.std`, `np.median`, `np.percentile`, `np.polyfit`, `np.histogram`,
  `curve_fit` and `.fit(` appear nowhere outside tests; and numpy use inside `dkist/dataset/` is index
  arithmetic (`np.s_`, `np.mgrid`, `np.ravel_multi_index`) plus string-table formatting for the WCS
  separability pretty-printer. The analysis shown in the documentation is performed by `ndcube`, `dask`
  and `numpy` methods on `Dataset.data`, which `docs/topic_guides/usertools.rst` states explicitly
  ("most of the development effort required to support DKIST data happened in packages such as
  `ndcube`, `sunpy` and `astropy`"). Four specific candidates were each checked and each falls under a
  value already listed: the Level 2 `Inversion`/`Profiles` classes *hold and display* inversion results
  computed elsewhere (`Data Visualization` + `Mission-Specific`); the quality/seeing surface is the
  `FriedParameter` search attribute plus a downloaded report (`Data Access and Retrieval`); `rebin` is
  `Data Reduction`; masking and cropping are `Processing`. A justification of the form "derived
  quantities are computed on the Dask array backing `Dataset.data`" would be equally true of any
  array-backed package and so carries no information.
- `Data Processing and Analysis: File Format Conversion` — `dkist.save_dataset()` writes a
  `Dataset`/`TiledDataset`/`Inversion` object to ASDF (`dkist/io/utils.py`), but the array data stay
  in the original FITS files and are referenced, not converted; no format-to-format data conversion.
- `Data Processing and Analysis: Image Processing` — mosaic regridding is delegated to the external
  `reproject` package in a documented example; `TiledDataset`'s own docstring says "This class does not
  currently implement helper functions to regrid the data".
- `Models and Simulations: Forward-Fitting` / `Instrument Response` — `Profiles.plot()` displays
  *fits* produced by the Level 2 inversion pipeline; the package performs no inversion or fitting.
- `Servers and Environments: *` — no server, container or HPC component in the package.
- `Data Processing and Analysis: Time Series Analysis`, `Energy Spectra`, `Spectrogram` — datasets
  carry a time axis and spectral axes, but the package provides no time-series, energy-spectrum or
  time-frequency analysis routines.

### 5. Related Region (MANDATORY)
- Solar Environment
- Photosphere
- Chromosphere
- Corona

Photosphere, Chromosphere and Corona are preferred over the broad `Solar Environment` alone because
the vocabulary supports them. Evidence: `dkist/data/api_search_values.json` `targetTypes` are
`coronalhole`, `activecorona`, `quietcorona`, `prominence`, `sunspot`, `spicules`, `quietsun`,
`plages`, `filament` — i.e. photospheric (sunspot, plages, quiet sun), chromospheric (spicules,
filament, prominence) and coronal (coronal hole, active/quiet corona) targets are all first-class
search values. `docs/topic_guides/level1data.rst` describes VBI wideband imaging and
ViSP/Cryo-NIRSP/VTF slit and narrowband spectropolarimetry; the Cryo-NIRSP sample datasets
(`CRYO_L1_TJKGC`, `CRYO_L1_MSCGD`) and `docs/examples/example_cryo_plots.md` cover DKIST's coronal
instrument specifically.

*Excluded:* `Solar Interior`, `Solar Wind`, `Interplanetary Space` — no supporting functionality.

### 6. Authors (MANDATORY)

**14 authors.** The project's own release metadata for v1.18.0 — the Zenodo record, mirrored by
DataCite — credits 13 people. One further author is an organization, credited in the repository itself
by `pyproject.toml`, `LICENSE.rst` and `docs/conf.py`. Stuart J. Mumford is credited in both places and
counted once, giving 14. There is no `CITATION.cff`, `codemeta.json` or `.zenodo.json` in the
repository, so the release record is the most complete author list available and no credited author is
omitted.

Affiliations come from two kinds of source, distinguished per author below: those given directly in the
**DKIST release metadata** (Mumford's Aperio Software Ltd.; the National Solar Observatory affiliations,
corroborated by `@nso.edu` commit addresses; Freij's SETI Institute and Lockheed Martin Solar and
Astrophysics Laboratory; Dencheva's and Jamieson's Space Telescope Science Institute), and those
**documented in other authoritative sources** where the DKIST record credits the author with no
affiliation at all (Leonard's Aperio Software Ltd., Van Kooten's Southwest Research Institute, and
Freij's third affiliation, Bay Area Environmental Research Institute).

1. **Stuart J. Mumford** — https://orcid.org/0000-0003-4217-4642
   - Affiliation: Aperio Software Ltd. (no ROR found)
   - Affiliation: University of Sheffield — https://ror.org/05krs5044
   - *Evidence:* Zenodo creator "Stuart Mumford / Aperio Software" and the `pyproject.toml` author
     email `stuart@cadair.com`. The fuller given name "Stuart J." is used in preference to Zenodo's
     "Stuart".
2. **National Solar Observatory** — https://ror.org/00b9pg524 *(organization author)*
   - *Evidence:* `pyproject.toml` `authors = [{ name = "NSO / AURA", ... }]`, `.cruft.json`
     `author_name`, `LICENSE.rst` "Copyright (c) 2019-2022, NSO / AURA", `docs/conf.py`
     `author = "NSO / AURA"`. The acronym is expanded, and the ROR is confirmed against ror.org.
   - *The compound source string is deliberately not split.* "NSO / AURA" names National Solar
     Observatory and the Association of Universities for Research in Astronomy (which operates NSO).
     Adding AURA as a second organization author was considered and rejected; National Solar
     Observatory stands as the single organization author. Recorded so a later pass does not re-open
     this as an oversight.
3. **Andrew J. Leonard** — https://orcid.org/0000-0001-5270-7487
   - Affiliation: Aperio Software Ltd. (no ROR found)
   - *Affiliation source — documented in SunPy's release metadata, not in the DKIST release metadata,*
     which credits him with no affiliation. The SunPy Project's Zenodo release record for
     `sunpy: A Core Package for Solar Physics` (v8.0.0) lists the creator "Andrew Leonard" with
     affiliation "Aperio Software Ltd." and ORCID `0000-0001-5270-7487`, alongside Stuart J. Mumford
     and Samuel Bennett at the same company. That record also confirms the identifier used here, since
     it pairs the name, the ORCID and the affiliation in one authoritative entry.
   - *Not ORCID-attested:* his ORCID record lists only University of Sheffield (Post-Doctoral Research
     Associate, 2015–2017), so Aperio Software Ltd. rests on the SunPy creator record rather than on
     ORCID.
   - *Source credit alias: "Drew Leonard".* The DKIST release metadata (Zenodo/DataCite creator lists
     for v1.17.0 and v1.18.0) credits him as "Drew Leonard", while the canonical form used here is
     "Andrew J. Leonard". Three independent signals reconcile the two: (a)
     `https://orcid.org/0000-0001-5270-7487` is the sole ORCID record matching the credited name, (b)
     its Sheffield employment is in the School of Maths and Statistics, the same department as
     co-author Mumford's Sheffield affiliation, and (c) the commit-authorship email in this repository
     is `Drew Leonard <andy.j.leonard@gmail.com>`, whose `andy.j.leonard` prefix ties the credited
     "Drew" to "Andrew" and supplies the middle initial J. Keeping the alias on record means a reader
     comparing this entry against the DKIST release metadata can see why the names differ.
   - He is the second-largest contributor to the repository by commit count (`git shortlog -sne --all`:
     112 commits, behind only Mumford), so the credit is substantial.
4. **Brett J Graham** — https://orcid.org/0000-0001-6315-4507
   - *Affiliation:* Space Telescope Science Institute — https://ror.org/036f5mx38
   - *Evidence:* an earlier revision of this file recorded "Brett Graham" with no identifier, reasoning
     that eight ORCID records share the name and none was corroborated. The corroboration does exist, and
     it comes from upstream rather than from name matching. This repository's git author is
     `Brett Graham <brettgraham@gmail.com>`, and **both** `sunpy/.mailmap` and `ndcube/.mailmap` map that
     exact address to the canonical form `Brett J Graham`, whose `sunpy/.zenodo.json` creator entry (#72)
     carries ORCID `0000-0001-6315-4507`. That ORCID's employment is Software Engineer at the Space
     Telescope Science Institute. The catalogue therefore holds one record for him under that canonical
     name, not one per project spelling.
   - *Not a catalogue-wide "Graham" merge.* SunPy separately lists a creator `graham`, which is a
     **different person**: GitHub's commit API attributes SunPy commit
     `1e2a628abe9c1f420bf7ae174ec1fc5433b2183b` to account `grahamasam` (ID 107145436), and
     `sunpy/.mailmap` aliases `Brett` and `Brett Graham` to Brett J Graham while deliberately declining to
     alias `graham`. Those two rows must stay separate.
5. **Erik Johansson** — identifier Not found
   - Affiliation: National Solar Observatory — https://ror.org/00b9pg524
   - *Evidence:* Zenodo/DataCite creator with affiliation "National Solar Observatory"; his commits are
     authored as `Erik Johansson <erikj@nso.edu>`. 31 ORCID records share this name and none lists NSO,
     so no ORCID is asserted.
6. **Arthur Eigenbrot** — https://orcid.org/0000-0003-0810-4368
   - Affiliation: National Solar Observatory — https://ror.org/00b9pg524
   - *Evidence:* Zenodo/DataCite creator; sole ORCID record for the name, and its institution is the
     National Solar Observatory, matching the Zenodo affiliation and his `aeigenbrot@nso.edu` commits.
7. **Alysa Derks** — identifier Not found
   - Affiliation: National Solar Observatory — https://ror.org/00b9pg524
   - *Evidence:* Zenodo/DataCite creator (no affiliation given there). The affiliation rests on
     separate repository evidence: her commits are authored as `alysaderks <aderks@nso.edu>`, an
     institutional National Solar Observatory address matching the `@nso.edu` addresses of the three
     other NSO-affiliated authors (Johansson, Eigenbrot, Larson).
   - *ORCID candidate reviewed and rejected — not an unexplored gap.* The sole ORCID record for this
     name, https://orcid.org/0000-0001-5847-8902, has no employments, works or keywords, so nothing
     corroborates the binding and a wrong person-to-ORCID link is costly to repair. Do not adopt it in
     a later pass without new corroboration. The `@nso.edu` email supports the *affiliation* above, not
     the ORCID binding.
8. **DJ Spiess** — identifier Not found
   - *Evidence:* Zenodo/DataCite creator for v1.18.0 (not present in the v1.17.0 creator list). No
     affiliation given; his commits use a non-institutional address, and no ORCID record matches this
     given name.
9. **Sam Van Kooten** — https://orcid.org/0000-0002-4472-8517
   - Affiliation: Southwest Research Institute — https://ror.org/03tghng59
   - *Affiliation source — ORCID-attested and current,* unlike the other two affiliations documented
     from outside the DKIST record: his ORCID record lists employment at Southwest Research Institute
     Boulder, 2021–present. The DKIST release metadata credits "Sam Van Kooten" with no affiliation at
     all.
   - *Identification corroborated in the DKIST domain:* the ORCID record is "**Samuel** Van Kooten",
     and among its works is "Using Bright Point Shapes to Constrain Wave Heating of the Solar Corona:
     Predictions for DKIST" — a DKIST paper. He is also credited in other solar-physics software
     (punchbowl, regularizePSF, ndcube, SunPy).
   - *Note for future passes:* a name search on the credited short form "Sam" returns no ORCID match;
     the record is registered under "Samuel". Search both forms before concluding an identifier is
     absent.
10. **Kristen Larson** — https://orcid.org/0000-0002-9756-0383
    - Affiliation: National Solar Observatory — https://ror.org/00b9pg524
    - *Evidence:* Zenodo/DataCite creator with affiliation "National Solar Observatory"; commits as
      `Kristen Larson <klarson@nso.edu>`. The ORCID record ("Kristen A. Larson") lists an employment
      "National Solar Observatory — Scientific Programmer / Calibration Engineer, DKIST Data Center"
      and a work "Level 1 Data from the Diffraction-Limited Near Infrared Spectropolarimeter", so the
      identification is unambiguous.
11. **Fraser Watson** — identifier Not found
    - *Evidence:* Zenodo/DataCite creator. No affiliation given; his commits use a non-institutional
      address.
    - *ORCID candidate reviewed and rejected — not an unexplored gap.* The sole ORCID record for this
      name, https://orcid.org/0009-0005-3911-531X, is empty, so nothing corroborates the binding. Do
      not adopt it in a later pass without new corroboration.
12. **Nabil Freij** — https://orcid.org/0000-0002-6253-082X
    - Affiliation: SETI Institute — https://ror.org/02dxgk712
    - Affiliation: Lockheed Martin Solar and Astrophysics Laboratory (no ROR found)
    - Affiliation: Bay Area Environmental Research Institute — https://ror.org/024tt5x58
    - *SETI Institute and Lockheed Martin Solar and Astrophysics Laboratory* come directly from the
      DKIST release metadata, which gives the compound affiliation "SETI Institute & LMSAL (@LM-SAL)";
      it is split into two here with the acronym expanded. SETI Institute is also the current
      employment on his ORCID record (Research Scientist, present).
    - *Bay Area Environmental Research Institute — documented in published work, and not from the DKIST
      record,* which names only SETI Institute and LMSAL. The peer-reviewed SunPy Project paper
      *The SunPy Project: An interoperable ecosystem for solar data analysis* (Frontiers in Astronomy
      and Space Sciences, 2023, `https://doi.org/10.3389/fspas.2023.1076726`) gives his affiliations as
      "Lockheed Martin Solar and Astrophysics Laboratory, Palo Alto, CA, United States" and "Bay Area
      Environmental Research Institute, Moffett Field, CA, United States" — a published pairing that
      corroborates BAERI alongside LMSAL. It is a documented affiliation, **historical relative to the
      current SETI Institute position** rather than a current employer. All three are recorded.
13. **Nadia Dencheva** — https://orcid.org/0000-0002-5686-9632
    - Affiliation: Space Telescope Science Institute — https://ror.org/036f5mx38
    - *Evidence:* Zenodo/DataCite creator with affiliation "Space Telescope Science Institute". Sole
      ORCID record for the name and it lists STScI.
14. **William Jamieson** — https://orcid.org/0000-0001-5976-4492
    - Affiliation: Space Telescope Science Institute — https://ror.org/036f5mx38
    - *Evidence:* Zenodo/DataCite creator with affiliation "Space Telescope Science Institute"; commits
      as `William Jamieson <wjamieson@stsci.edu>`. Nine ORCID records share the name; only this one has
      an STScI employment.

**Two repository contributors are deliberately not credited.** `git shortlog -sne --all` and the
GitHub contributor list show two people who appear in no authorship source — neither the Zenodo
v1.18.0 creator list nor the 14 authors above: `Thomas Robitaille <thomas.robitaille@gmail.com>`
(2 commits: `60264cc` 2026-07-07 and `0db7b0e` 2026-07-06, both substantive bug fixes) and
`Zach Burnett <zachary.r.burnett@gmail.com>` (1 commit, `bf3dc0a` 2024-08-26, PR #422).

Field 6 is headed "Authors" and defined as "The author(s) of this software". It has no contributor
sub-field and no wording that extends it to everyone who has landed a commit, so it records **credited
authors**, not all contributors — and the authoritative statement of whom this project credits is its
own archival creator list, which the DKIST team controls through its GitHub-Zenodo release process.
Crediting people the project has not credited would assert authorship on the project's behalf.

The two cases differ, and one is worth revisiting. Robitaille's commits post-date the v1.18.0 release
(2026-06-23) whose Zenodo record supplied the creator list, so his absence is a timing artifact — this
record's source revision contains those commits (2 of the 8 after the tag), and the next release's
creator list should settle it; if it credits him, he should be added then. Burnett's commit predates
both archived releases, so his absence from the v1.17.0 *and* v1.18.0 creator lists is a persistent
editorial state rather than a timing gap.

All organization names are spelled out rather than abbreviated.

### 7. Software Name (MANDATORY)
DKIST User Tools

*Evidence:* the `README.rst` title, `pyproject.toml` `description = "DKIST User Tools"` and
`.cruft.json` `short_description`. The distribution and import name is the lower-case `dkist`; this
field carries the human-readable name.

### 8. Description (MANDATORY)
A Python library for obtaining, processing and interacting with calibrated DKIST data. The dkist
package is developed by the DKIST Data Center team and provides DKIST-specific functionality as
plugins and extensions to the wider sunpy and scientific Python ecosystem. It provides a sunpy Fido
client for searching the DKIST Data Center's dataset inventory, helpers for transferring Level 1 files
from the Data Center over Globus, and downloads of dataset metadata (ASDF), quality reports and
preview movies. Loaded data are represented by the Dataset class (a subclass of ndcube's NDCube), by
TiledDataset for mosaicked data such as VBI, and by the experimental Inversion and Profiles classes
for Level 2 inversion products. Each is backed by a Dask array assembled lazily from the many FITS
files that make up a dataset, together with a gWCS coordinate description, the full table of FITS
headers, and the dataset inventory record. Datasets can be sliced, cropped, rebinned, masked, plotted
as images, animated slider plots, line plots and tiled mosaics, and saved back out to ASDF.

- An earlier record held a three-part, newline-joined concatenation, reproduced exactly:

```
A Python library for obtaining, processing and interacting with calibrated DKIST data.
DKIST User Tools
When you are interacting with the `dkist` project you are asked to follow the SunPy `Code of Conduct <https://sunpy.org/coc>`__.
```

  Those three lines are the GitHub repository description, the bare `README.rst` title line, and the
  README's Code of Conduct sentence — three separate description candidates that automated
  repository-metadata extraction joins with newlines. The title fragment and the Code of Conduct
  sentence are not description content, and the third line's reStructuredText link markup renders
  literally to readers because this is a plain-text field.
- The correction **keeps that first sentence verbatim as the opening sentence**, so the intended
  wording (and the 150-200 character preview) is unchanged. Only the two spurious fragments are
  dropped, and detail from primary sources is appended.
- The text is deliberately plain prose with no markup of any kind, since the field is not rendered as
  Markdown or reStructuredText.
- Evidence for the added detail: `README.rst`; `docs/topic_guides/usertools.rst` ("developed by the
  DKIST Data Center team… only provides DKIST specific functionality as plugins and extensions to the
  wider sunpy and scientific Python ecosystem"); `docs/topic_guides/level1data.rst` (many FITS, one
  ASDF); `dkist/dataset/dataset.py`, `tiled_dataset.py` and `inversion.py`;
  `dkist/io/file_manager.py`; `dkist/io/utils.py` (`save_dataset`); `dkist/net/client.py`;
  `dkist/net/globus/`.

### 9. Concise Description (OPTIONAL)
DKIST User Tools are software packages that enable scientific use of Daniel K. Inouye Solar Telescope data, helping researchers discover, access, calibrate, visualize, and analyze DKIST data products.

*Retained verbatim as submitted* (200 characters, exactly at the field limit).

*Considered and declined.* The word "calibrate" slightly overstates this package — it consumes
already-calibrated Level 1 data rather than calibrating it (see the Field 4 removal rationale) — and
replacing it with "load" would have tightened the sentence while staying inside the limit. The
submitted wording is kept deliberately. Recorded so the tightening is not re-proposed on a later pass.

### 10. Publication Date (RECOMMENDED)
2020-03-27

This is the release date of `v0.1a1`, the first version the project deliberately cut. An earlier
record held `2017-11-30`, the GitHub repository creation timestamp (`2017-11-30T16:37:42Z`) — a real,
checkable date, but the creation of a *repository object* rather than a publication of software, and
corresponding to no version at all. The field is defined as "Date of first broadcast/publication",
"used for the initial version of the software", so both halves point at the first released version.
The three candidates as evaluated:

| Candidate | Date | Assessment |
|---|---|---|
| GitHub repository creation | 2017-11-30 | Verifiable, but not a publication of software, and it corresponds to **no version at all** — so it fails the "initial version of the software" half outright. |
| First PyPI upload, `0.1.dev254` | 2019-04-09 | A publication, but a one-off: it is the **only** `dev`-style release in the project's entire 53-version PyPI history, a single file, with **no matching git tag**, followed by 11½ months of silence. It reads as a name-reservation or trial upload rather than a published version of the software. |
| First tagged release, `v0.1a1` | 2020-03-27 | **Selected.** The first version the project deliberately cut: it exists as both a git tag and a PyPI release, and it opens the unbroken release series that runs to 1.18.0. Being an alpha does not disqualify it — it is unambiguously the initial version, and its upload is a genuine publication. |

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

An earlier record used the bare URL `https://zenodo.org/records/18494048` as the organization name and
identifier. That is a Zenodo version-record URL, not a publisher name. DataCite reports
`publisher = "Zenodo"` for both dkist DOIs, and this field's instructions name Zenodo as the correct
entry for software whose DOI came from the GitHub-Zenodo workflow — which this is: the Zenodo records
are `isSupplementTo` `https://github.com/DKISTDC/dkist/tree/v1.18.0`.

### 12. Version (RECOMMENDED)
- **Version Number:** 1.18.0
- **Version Date:** 2026-06-23
- **Version PID:** https://doi.org/10.5281/zenodo.20819708
- **Version Description:** Adds limited file-saving capability to `Dataset`, `TiledDataset` and
  `Inversion` via `dkist.save_dataset()`, for datasets modified by slicing or masking but whose data
  values are unchanged. Generated ASDF files now include observation frames, calibration frames and
  recipe run configuration information. `DKISTFileManager.quality_report()` gains a `format` argument
  so callers can download either the existing PDF report or the new JSON report. Backwards
  incompatible: bumps the required `asdf`, `asdf-astropy` and `asdf-coordinates-schemas` versions.
  Fixes `Inversion` slicing so it also slices `Profiles`, and `TiledDataset.tiles_shape` for flat
  (flattened or sliced) `TiledDataset`s.

- 1.18.0 is the current release, superseding the 1.17.0 an earlier record held. Independently
  confirmed in four places: the repository tag `v1.18.0`; the GitHub release `v1.18.0`, published
  `2026-06-23T20:15:19Z`; the Zenodo version record `20819708` with `version = "v1.18.0"`,
  `publication_date = 2026-06-23` and DOI `10.5281/zenodo.20819708`; and DataCite for the concept DOI,
  which reports `version = "v1.18.0"` and a single `Issued` date of `2026-06-23`. `CHANGELOG.rst`
  carries the matching `1.18` section.
- The version number is recorded as the bare `1.18.0`, and the version PID as a full DOI URL as the
  field requires.
- *Date discrepancy resolved:* `CHANGELOG.rst` heads the section "1.18 (2026-06-09)" (the towncrier
  build date from when the release PR was prepared) and Zenodo's copy of the same text reads
  "1.18 (2026-06-26)". Neither is the release date. `2026-06-23` is used because the GitHub release
  publication and the Zenodo/DataCite `Issued` date agree on it.
- *Distribution-channel lag:* PyPI and conda-forge both still show `1.17.0` as their newest artifact,
  so 1.18.0 was released and archived on GitHub and Zenodo without reaching those channels. The
  repository page and the DOI record are the authoritative sources this field points at, so 1.18.0 is
  used; the lag is recorded here so the discrepancy is not mistaken for an error.

### 13. Programming Language (RECOMMENDED)
- Python 3.x

*Evidence:* `pyproject.toml` sets `requires-python = ">=3.11"`, CI runs py311–py314, and `.cruft.json`
records `use_compiled_extensions: "n"` (pure Python).

*Note:* Shell also appears in the repository, in two CircleCI helper scripts
(`.circleci/codecov_upload.sh`, `.circleci/early_exit.sh`). Excluded — this field is for the languages
"most important for the software", not build glue.

### 14. Reference Publication (RECOMMENDED)
Not found — the repository contains no `CITATION.cff`, no `codemeta.json`, and no "how to cite"
section in `README.rst`, `CONTRIBUTING.md` or the documentation; there is no JOSS or software paper
referenced anywhere in the source tree. The citable artifact is the Zenodo concept DOI in Field 2.

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

- Evidence, derived from the repository rather than from the DOI record: `LICENSE.rst` is the
  BSD 3-Clause License text, "Copyright (c) 2019-2022, NSO / AURA"; `README.rst` states "licensed
  under the terms of the BSD 3-Clause license"; `pyproject.toml` declares
  `license-files = ["licenses/LICENSE.rst"]`; `.cruft.json` records `"license": "BSD 3-Clause"`; and
  GitHub reports the SPDX identifier `BSD-3-Clause`. Zenodo and DataCite agree (`bsd-3-clause`) but
  were not relied on. The SPDX URI is used in preference to DataCite's
  `https://opensource.org/licenses/BSD-3-Clause`.
- *Minor repository inconsistency, not a metadata issue:* `pyproject.toml` points `license-files` at
  `licenses/LICENSE.rst`, but the file is at the repository root as `LICENSE.rst`.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- astropy
- dkist
- solar physics
- sunpy
- solar
- ndcube
- fits
- asdf
- globus
- coordinates
- polarimetry
- spectroscopy
- multidimensional
- plotting
- data_retrieval

Keywords are recorded lower-case, one per entry. `astropy`, `dkist`, `solar physics` and `sunpy`
correspond to the repository's GitHub topics `astropy`, `dkist`, `solar-physics`, `sunpy`.

The rest reuse existing HSSI keyword terms where they apply: `solar`; `ndcube` (`dkist.Dataset`
subclasses `ndcube.NDCube`); `fits` (Level 1 data are FITS); `coordinates` (gWCS coordinate handling);
`polarimetry` (Stokes I/Q/U/V axes, the `Full Stokes` inventory key, and ViSP, DL-NIRSP and Cryo-NIRSP
being spectropolarimeters); `spectroscopy` (spectral axes and the `SpectralSampling` search attribute);
`multidimensional` (4-D and 5-D datasets); `plotting`; `data_retrieval`.

Two terms are new to the vocabulary and both are distinctive to this package: `asdf` — it ships ASDF
schemas, manifests and converters and registers `asdf.extensions` / `asdf.resource_mappings` entry
points; and `globus` — `dkist/net/globus/` implements the Globus OAuth, endpoint-discovery and
transfer layer used to fetch DKIST data.

*Not added:* `photosphere`, `chromosphere`, `corona` — covered more precisely by Field 5; `dask` and
`spectropolarimetry` — an implementation detail, and a near-duplicate of `polarimetry` +
`spectroscopy`, respectively.

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific
- HTTP/HTTPS Directories

- `Observatory/Mission-specific` — the package's only science data source is the DKIST Data Center:
  `dkist/net/client.py` queries its dataset search service, `dkist/io/file_manager.py` uses its
  metadata streamer for quality reports and preview movies, and `dkist/net/globus/` transfers Level 1
  files from its Globus endpoints. Cross-listed with the DKIST observatory in Field 32, as this field
  instructs.
- `HTTP/HTTPS Directories` — `dkist/data/_sample.py` downloads sample datasets from
  `https://g-a36282.cd214.a567.data.globus.org/user_tools_tutorial_data/` with `parfive`;
  `dkist/net/attrs_values.py` refreshes `api_search_values.json` over HTTPS; quality reports and
  preview movies are plain HTTPS downloads.

*Considered and excluded, with reasons:*
- `S3/Cloud-aware` — the DKIST inventory carries object-store keys (`bucket`, `asdfObjectKey`,
  `browseMovieObjectKey`) that `DKISTFileManager.download()` uses to build Globus source paths, but
  the package contains no S3 client (`boto3`/`s3fs` appear nowhere) and never speaks the S3 protocol.
- `FTP/FTPS Directories` — `parfive[ftp]` is a declared dependency extra, but no DKIST data source
  uses FTP; this is generic downloader capability, not a supported source.
- `The Virtual Solar Observatory.`, `CDAWeb` — reachable through `sunpy`'s own Fido clients once
  `dkist.net` is imported, but they are sunpy's clients, not this package's sources.

### 18. Input File Formats (RECOMMENDED)
- FITS
- JSON
- Other

- `FITS` — `dkist/io/dask/loaders.py` (`AstropyFITSLoader`) reads every Level 1 data array from FITS
  via `astropy.io.fits`; `dkist/data/_sample.py` reads `VISP_HEADER.hdr` with
  `fits.Header.fromtextfile`; `docs/topic_guides/level1data.rst` states the Level 1 files "conform to
  the FITS 4 specification".
- `JSON` — `dkist/net/attrs_values.py` reads `dkist/data/api_search_values.json`; the Data Center
  search service returns JSON; `DKISTFileManager.quality_report(format="json")` retrieves a JSON
  report.
- `Other` — **ASDF**, the package's primary metadata format, which has no term of its own in the HSSI
  file-format vocabulary (ascii, CDF, csv, FITS, HDF5, IDL.sav, ISTP-Compliant, JSON, netCDF3/4,
  Other, Zarr). Every dataset is loaded from an ASDF file (`dkist.load_dataset`,
  `dkist/dataset/loader.py`), and `dkist/io/asdf/` ships the DKIST ASDF schemas, manifests and
  converters. Recorded as `Other` with ASDF named here rather than inventing a vocabulary term.

*Excluded:* HDF5, netCDF3/4, CDF, csv, ascii, Zarr, IDL.sav — no reader for any of them anywhere in
the package.

### 19. Output File Formats (RECOMMENDED)
- Other

- `Other` — **ASDF**. `dkist.save_dataset(dataset, asdf_path)` (`dkist/io/utils.py`) writes a
  `Dataset`, `TiledDataset` or `Inversion` to a new ASDF file, using the converters registered by
  `dkist/io/asdf/entry_points.py`. Same vocabulary gap as Field 18.
- *Excluded:* the PDF/JSON quality reports and the MP4 preview movie are *downloaded* artifacts, not
  formats the software generates; matplotlib figures are not a data format.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

*Evidence:* `.github/workflows/main.yml` runs the test matrix as `- linux: py314`, `- macos: py313`,
`- windows: py312`, `- linux: py311`, `- linux: py311-oldestdeps`. Windows support is actively
maintained (CHANGELOG 1.17.0: "Fixes the format of paths being passed to `ds.files.download()` on
Windows so that globus can understand it").

*Note:* `Operating System Independent` was considered. The three concrete platforms are recorded
instead because they are what CI actually verifies.

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent
- x86-64
- Apple Silicon arm64

- `CPU Independent` — the package is pure Python with no compiled extensions: `.cruft.json` records
  `"use_compiled_extensions": "n"`, there are no C or Cython sources in the tree, and release
  artifacts are built with OpenAstronomy's `publish_pure_python.yml` workflow.
- `x86-64` and `Apple Silicon arm64` — the architectures the CI matrix actually exercises
  (GitHub-hosted Linux and Windows runners are x86-64; the macOS runners are Apple Silicon arm64).

### 22. Related Phenomena (OPTIONAL)
- Solar Corona

- *Evidence:* `dkist/data/api_search_values.json` exposes `targetTypes` including `activecorona`,
  `quietcorona` and `coronalhole` as searchable values, and the package ships two Cryo-NIRSP sample
  datasets plus a dedicated `docs/examples/example_cryo_plots.md` for DKIST's coronal
  spectropolarimeter.
- *Excluded:* `Coronal Heating`, `Coronal Mass Ejections`, `Solar Flares`, `Solar Wind`,
  `Geomagnetic Storms`, `X-ray emission` — the package is phenomenon-agnostic beyond the coronal
  target types above; no flare, CME or heating-specific functionality exists.

### 23. Development Status (RECOMMENDED)
Active

*Evidence:* release `v1.18.0` on 2026-06-23; source revision
`8ce3cc9b34116e4d58211ed2824629f2828c3e0f` dated 2026-07-17 with 8 commits after the tag; a weekly
scheduled CI cron plus mypy, docs, benchmark and downstream-test workflows; a live towncrier changelog
with four unreleased fragments in `changelog/`; the GitHub repository is not archived. This matches
repostatus.org "Active": reached a stable, usable state and being actively developed.

### 24. Documentation (RECOMMENDED)
https://docs.dkist.nso.edu/projects/python-tools/en/stable/

*Evidence:* `pyproject.toml` `[project.urls] Documentation`, `.cruft.json` `documentation_url`, and
the `README.rst` documentation link. The page resolves and includes an installation guide
(`installation.rst`, `workshop_install.rst`), tutorial, examples, how-to guides, topic guides and API
reference.

### 25. Funder (OPTIONAL)
Not found — the repository contains no funding or acknowledgement statement: no `ACKNOWLEDGEMENTS`
file, no funding section in `README.rst`, `CONTRIBUTING.md` or the documentation, no funder in the
Zenodo record (`grants: null`) and none in DataCite (`fundingReferences: []`).

*Not asserted:* DKIST is a U.S. National Science Foundation facility and NSO is operated by AURA under
a cooperative agreement with NSF, but that is external knowledge rather than repository evidence, so
this field is left empty rather than inferred.

### 26. Award Title (OPTIONAL)
Not found — no award title or number appears anywhere in the repository, the Zenodo record or the
DataCite record.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found — the repository cites no publications. There is no `CITATION.cff`, no bibliography in the
documentation, and the DataCite record's only related identifiers are the GitHub source tree
(`IsSupplementTo`) and the concept DOI (`IsVersionOf`).

### 28. Related Datasets (OPTIONAL)
Not found — no dataset DOI is referenced in the repository.

*Considered and not asserted:* `dkist/data/_sample.py` names four DKIST tutorial sample datasets —
`VISP_L1_KMUPT` (BKPLX), `VBI_L1_NZJTB` (YCDRFH/AJQWW), `CRYO_L1_TJKGC` (DBXVEL) and `CRYO_L1_MSCGD`
(POKNUM) — viewable at `https://dkist.data.nso.edu/datasetview/<id>`. They are cut-down demonstration
subsets chosen for documentation rather than datasets the software is built around (it supports all
DKIST Level 1 and experimental Level 2 products), and they carry no DOIs, so they are recorded here as
context instead of as field values.

### 29. Related Software (OPTIONAL)
- https://github.com/sunpy/sunpy
- https://github.com/sunpy/ndcube
- https://github.com/spacetelescope/gwcs
- https://bitbucket.org/dkistdc/dkist-inventory
- https://pypi.org/project/dkist-data-simulator/

- **sunpy** — this package is a SunPy Affiliated Package (`docs/index.rst`) whose stated design is to
  provide "DKIST specific functionality as plugins and extensions to the wider `sunpy` and scientific
  Python ecosystem" (`docs/topic_guides/usertools.rst`). A distinguishing domain-specific dependency
  and the framework this software extends.
- **ndcube** — `dkist.Dataset` subclasses `ndcube.NDCube`; `Inversion` and `Profiles` subclass
  `ndcube.NDCollection`; the declared dependency is `ndcube[plotting,reproject]>=2.4.0`. The
  usertools guide names `ndcube.NDCube` as one of the two classes users must know.
- **gwcs** — DKIST coordinate information is a gWCS object (`docs/topic_guides/level1data.rst`);
  `dkist/wcs/models.py` supplies the astropy-modeling transforms that populate it, and
  `dkist/io/asdf/converters/models.py` serialises them. Domain-specific (astronomy WCS), not generic
  infrastructure.
- **dkist-inventory** — the companion DKIST Data Center library that *generates* the ASDF files this
  package reads; the ASDF generation code was moved out of this repository into it
  (`CHANGELOG.rst`: "Move asdf generation code into dkist-inventory package (#79)"), which makes it
  both a predecessor and a companion. `dkist/conftest.py` copies a function from it, and
  `dkist/tests/generate_*.py` import `dkist_inventory.asdf_generator` and
  `dkist_inventory.transforms`. Linked to its own declared source repository,
  `https://bitbucket.org/dkistdc/dkist-inventory`, which this field prefers ("link to code
  repository"); that repository is public and actively maintained (created 2020-04-28, last updated
  2026-07-21). Its Bitbucket page renders client-side, so a plain fetch of the HTML looks empty even
  though the repository resolves — noted because that appearance can be mistaken for a dead link.
  `https://pypi.org/project/dkist-inventory/` is an equally valid alternative for readers who prefer a
  PyPI landing page.
- **dkist-data-simulator** — the DKIST Data Center's SPEC-214 header and FITS generator, imported by
  `dkist/tests/generate_eit_tiled_dataset.py` (`dkist_data_simulator.spec214.vbi`) to synthesise test
  datasets. A DKIST-ecosystem companion, on weaker evidence than the entries above (test-fixture
  generation only). Linked via its PyPI page because, unlike `dkist-inventory`, it declares no
  source-repository URL in its package metadata (`project_urls` is null) and no public repository could
  be located for it.

*Considered and excluded, with reasons:* numpy, matplotlib, tqdm, packaging, platformdirs, parfive,
aiohttp, pytest and the rest of the generic scientific-Python and tooling stack — being a dependency
is not a relationship that distinguishes this software. `globus-sdk` is excluded too: Globus is
general-purpose research data-transfer infrastructure that would be equally at home in a biology
pipeline, so it fails the domain test despite being important to this package (its role is instead
captured in Field 4 `Mission-related: Distribution/Access` and in the `globus` keyword).
`dkist-sphinx-theme`, `sunpy-sphinx-theme` and the `pytest-*` plugins are documentation and test
tooling.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/sunpy/sunpy
- https://github.com/sunpy/ndcube
- https://github.com/asdf-format/asdf
- https://github.com/spacetelescope/gwcs
- https://github.com/astropy/reproject
- https://github.com/astropy/astropy
- https://github.com/dask/dask

Each entry names the specific exchange, not mere dependency presence.

- **sunpy** — a genuine plugin relationship: importing `dkist.net` registers `DKISTClient` with
  `sunpy.net.Fido`, so `Fido.search` returns DKIST results alongside other clients
  (`dkist/net/__init__.py`, `dkist/net/client.py`). `dkist.net.attrs` extends `sunpy.net.attrs`, and
  `dkist.net.attrs_values` maps DKIST inventory keys onto `sunpy.net.attrs.Instrument`.
  `BoundingBox` consumes `sunpy.coordinates` frames; `docs/examples/vbi_extents.md` uses
  `sunpy.visualization.extent` on DKIST WCSes.
- **ndcube** — shared data model: `dkist.Dataset` *is* an `ndcube.NDCube` and `Inversion`/`Profiles`
  *are* `ndcube.NDCollection`s, so any ndcube-aware code operates on DKIST datasets directly.
  Documented use of `ndcube.NDCube.rebin` on a `Dataset` in `docs/examples/rebinning_and_dask.md`.
- **asdf** — documented extension relationship declared in `pyproject.toml`:
  `'asdf.extensions' = {dkist = 'dkist.io.asdf.entry_points:get_extensions'}` and
  `'asdf.resource_mappings' = {dkist = 'dkist.io.asdf.entry_points:get_resource_mappings'}`. The
  package ships ASDF schemas and manifests under `dkist/io/asdf/resources/` and converters under
  `dkist/io/asdf/converters/`, so a plain `asdf.open()` can read DKIST files, and
  `dkist.save_dataset()` writes them.
- **gwcs** — DKIST datasets carry gWCS objects, and `dkist/wcs/models.py` provides the transform
  classes (`VaryingCelestialTransform*`, `CoupledCompoundModel`, `Ravel`) that gWCS composes and that
  the package's ASDF converters round-trip; `gwcs>=0.24.0` is pinned for an inverse-transform fix.
- **reproject** — `docs/examples/reproject_vbi_mosaic.md` passes `dkist.TiledDataset` tiles to
  `reproject.mosaicking.reproject_and_coadd` to stitch a VBI mosaic; the dependency is declared as
  `ndcube[plotting,reproject]` with `reproject[all]` in the docs extra. Output of one is input to the
  other.
- **astropy** — the public API exchanges astropy objects: `Dataset.headers` is an
  `astropy.table.Table`, search results are `astropy.units.Quantity` and `astropy.time.Time` columns
  (`DKISTQueryResponseTable._process_table`), `dkist.data.sample.VISP_HEADER` is an
  `astropy.io.fits.Header`, and `dkist/wcs/models.py` classes are `astropy.modeling.Model` subclasses
  usable in any astropy modeling expression. `docs/tutorial/1_astropy_and_sunpy.md` is devoted to the
  exchange.
- **dask** — `Dataset.data` is a `dask.array.Array` as its documented public interface, assembled from
  per-file loaders (`dkist/io/dask/striped_array.py`), so users call dask APIs (`.sum()`,
  `.compute()`, `.rebin`, chunk control) on it directly. `docs/examples/rebinning_and_dask.md` is an
  entire documented guide to this, and the docs extra includes `distributed` for use with a dask
  cluster.

*Considered and excluded, with reasons:* numpy, matplotlib, tqdm, HTTP plumbing, parfive, aiohttp,
platformdirs, packaging and the rest of the generic stack — sharing a Python runtime is not
interoperability, and such a claim would read identically for almost any package. `globus-sdk` is
excluded for the Field 29 reason. No blanket "part of the scientific Python ecosystem" or "PyHC
member" justification is used anywhere above.

### 31. Related Instruments (OPTIONAL)
None recorded — the four DKIST instruments this package supports have no instrument record in the
SPASE-derived controlled vocabulary, so the association is carried at the observatory level in
Field 32 instead.

**The instruments are genuinely supported.** `dkist/data/api_search_values.json` gives the Data
Center's `instrumentNames` categorical values as exactly `CRYO-NIRSP`, `VISP`, `VBI`, `DL-NIRSP`, and
`dkist/net/attrs_values.py` maps that key onto `sunpy.net.attrs.Instrument`, so those four are the
searchable instrument values. Beyond search: `dkist.TiledDataset` exists for VBI mosaics,
`swap_tile_limits` is documented as needed for DL-NIRSP, the sample datasets are ViSP
(`VISP_L1_KMUPT`), VBI (`VBI_L1_NZJTB`) and Cryo-NIRSP (`CRYO_L1_TJKGC`, `CRYO_L1_MSCGD`), and
`docs/examples/example_cryo_plots.md` and `docs/examples/reproject_vbi_mosaic.md` are
instrument-specific guides.

**No instrument record exists.** A scan of the whole controlled instrument/observatory vocabulary for
`dkist`, `inouye`, `nirsp`, `visp`, `vbi`, `vtf`, `broadband`, `spectro-polarim` and `cryo` returns
only observatory-type records for DKIST itself — there is none of instrument type for VBI, ViSP,
DL-NIRSP, Cryo-NIRSP or VTF. Following SPASE/HDRL guidance that a missing instrument record must not
block a software association, these instruments are represented by the DKIST observatory record in
Field 32. No instrument name is recorded without a `https://spase-metadata.org/` identifier, and no
new instrument value is invented; a genuinely new instrument enters the vocabulary through its
upstream refresh.

**Also considered and excluded on relevance, with reasons:**
- **VTF** (Visible Tunable Filter) — described in `docs/topic_guides/level1data.rst` as an example
  frame layout, but absent from the Data Center's `instrumentNames` search values, with no sample data
  and no code path. Not yet supported.
- **WFC** (wavefront correction) — never referenced. The only related item is the seeing metric
  `FriedParameter` / `Average Fried Parameter`, which is dataset quality metadata, not WFC data.
- **SDO/AIA** — appears only in `dkist/tests/generate_aia_dataset.py` (a test-fixture generator that
  fetches `aia.lev1_euv_12s` from JSOC to build synthetic datasets) and in
  `docs/examples/vbi_extents.md`, which draws VBI field-of-view outlines over an AIA context image.
  Test fixtures and a demonstration context image, not designed-to-support.
- **SOHO/EIT** — appears only as static test FITS files in `dkist/data/test/EIT/` and in
  `dkist/tests/generate_eit_test_dataset.py` / `generate_eit_tiled_dataset.py`. Test fixtures only.
- Generic multi-instrument concerns are routed elsewhere as the field instructs: FITS and ASDF →
  Fields 18/19; the DKIST Data Center as a source → Field 17 `Observatory/Mission-specific`; coronal
  targets → Field 22.

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Daniel K Inouye Solar Telescope
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/DKIST

Relevance is beyond doubt: the package is written and maintained by the DKIST Data Center team for
DKIST data alone (`docs/topic_guides/usertools.rst`), and it reads DKIST Level 1 FITS/ASDF products,
implements DKIST's WCS conventions and ASDF schemas, and talks to DKIST's own search, metadata and
transfer services. This is also where the four supported instruments from Field 31 are carried.
Cross-listed with `Observatory/Mission-specific` in Field 17, as this field requires.

**Canonical identifier.** The vocabulary contains this resource in two forms — the bare
`https://spase-metadata.org/SMWG/Observatory/DKIST`, named "Daniel K Inouye Solar Telescope", and an
`.html`-suffixed duplicate named "Daniel K Inouye Solar Telescope (DKIST)". An earlier record used the
`.html` form. The bare identifier is used here because it is the canonical one and its name is the
canonical SPASE name; roughly 40 other identifiers exist in both forms, and the two denote the same
resource, so this is a naming normalization rather than a change of meaning.

*No other observatory qualifies.* SDO and SOHO were considered and excluded for the test-fixture and
demonstration-context reasons given in Field 31.

### 33. Logo (OPTIONAL)
https://raw.githubusercontent.com/DKISTDC/dkist/main/docs/logo/icon_square.jpg

- *Evidence:* `docs/logo/icon_square.jpg` is the only logo asset in the repository — a square orange
  DKIST telescope-dome icon. The raw GitHub URL is publicly accessible and serves `image/jpeg`
  (72,150 bytes), and at 78 characters it is well inside the 200-character URL limit.
- *Note:* the documentation site additionally serves DKIST facility and NSO logos supplied by
  `dkist-sphinx-theme`
  (`https://docs.dkist.nso.edu/projects/python-tools/en/stable/_static/img/dkist-logo-v5-blue-text.png`);
  the in-repository asset is preferred because it belongs to this package rather than to the theme.
