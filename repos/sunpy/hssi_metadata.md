# HSSI Metadata Extraction Results

**HSSI Software ID:** 13b71402-f2cb-4aa3-9b17-639652e87ca8
**Repository:** https://github.com/sunpy/sunpy
**Source Revision:** ed70935fa156a05f81926e4a2f4a0ea25dc37f36
**Extraction Date:** 2026-08-13
**Validation Date:** 2026-08-23
**Validation Status:** PASS
**Scope note.** sunpy is a general-purpose solar-physics library whose instrument coverage lives in
data-driven subpackages (`sunpy/map/sources/`, `sunpy/timeseries/sources/`, `sunpy/net/`) rather than
in the README. Read the instrument, data-source and functionality evidence below as coming from those
module trees at the pinned revision, not from project prose. Where a value here replaces or corrects an
earlier one, the note records what the earlier value was and why it was superseded, so a later refresh
does not re-propose it.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.591887
- Source: Zenodo concept DOI covering all versions, cited as the software citation in `CITATION.rst`
  (`.. _Zenodo DOI: https://doi.org/10.5281/zenodo.591887`) and confirmed against the DataCite record,
  which resolves and reports `version: v8.0.0`, `publicationYear: 2026`.
- The concept DOI is correct here rather than a version DOI: it always resolves to the newest release,
  which is what a software-level persistent identifier should do. The v8.0.0 version-specific DOI is
  recorded separately in Field 12 (Version PID), which is where a per-release identifier belongs.

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/sunpy/sunpy
- Source: `pyproject.toml` `[project.urls] "Source Code"`, the PyHC core registry `code:` field, and
  the DataCite `relatedIdentifiers` entry `IsSupplementTo https://github.com/sunpy/sunpy/tree/v8.0.0`.
  Verified to resolve; default branch `main`.

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Magnetospheric
- Coordinate Transforms: Mission-Specific
- Coordinate Transforms: Planetary
- Coordinate Transforms: Solar
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: Line Plots
- Data Visualization: Mission-Specific
- Data Visualization: Movies
- Models and Simulations
- Models and Simulations: Empirical

**Evidence for each value.**
- *Coordinate Transforms* and *: Solar* — `sunpy/coordinates/frames.py` defines `HeliographicStonyhurst`,
  `HeliographicCarrington`, `Heliocentric`, `Helioprojective`, `HelioprojectiveRadial`; the frames are
  registered into astropy's transformation graph so `SkyCoord` converts among them.
- *: Heliospheric* — `HeliocentricEarthEcliptic`, `HeliocentricInertial`, `GeocentricSolarEcliptic`,
  `GeocentricEarthEquatorial` in the same module.
- *: Magnetospheric* — `BaseMagnetic` and its subclasses `Geomagnetic`, `SolarMagnetic`,
  `GeocentricSolarMagnetospheric`.
- *: Mission-Specific* — `sunpy/coordinates/spice.py` wraps `spiceypy` so every SPICE frame in a loaded
  kernel set becomes a `SkyCoord` frame, including spacecraft-attitude and instrument frames, and
  exposes instrument field-of-view retrieval.
- *: Planetary* — `sunpy/coordinates/ephemeris.py` provides
  `get_body_heliographic_stonyhurst` and `get_horizons_coord`, which return coordinates for arbitrary
  solar-system bodies, and `sunpy/coordinates/spice.py` lets a user install built-in SPICE frames
  (its developer notes name the `IAU_*` body-fixed frames explicitly) and transform to and from them.
  This is genuine non-Earth planetary coordinate support, and the earlier record omitted it.
- *Data Processing and Analysis* and *: Data Access and Retrieval* — `sunpy/net/` with the `Fido`
  factory over the VSO, JSOC, CDAWeb, SOAR, HEK, HELIO, SOLARNET and `dataretriever` clients.
- *: Analysis* — `sunpy/physics/differential_rotation.py`, `sunpy/sun/` (constants, position,
  differential rotation, Carrington rotation numbering), `GenericMap` derived quantities.
- *: Data Reduction* — `sunpy/image/resample.py`, `GenericMap.resample`
  (`sunpy/map/mapbase.py:1688`) and `GenericMap.superpixel` (`:2197`) implement downsampling and
  pixel binning, which is exactly what this subcategory covers.
- *: File Format Conversion* — `sunpy/io/_file_tools.py` reads FITS/JPEG2000/ANA and writes the same
  set, so a file read in one format can be written in another.
- *: Image Processing* — `sunpy/image/transform.py` (affine transform, optional OpenCV/scikit-image
  backends), `GenericMap.rotate`, `GenericMap.reproject_to`.
- *: Processing* — the Map transformation chain (`rotate`, `submap`, `resample`,
  `reproject_to`) and `sunpy/physics/differential_rotation.py:differential_rotate` are general
  pipeline-style processing steps distinct from the image-processing algorithms themselves.
- *: Time Series Analysis* — `sunpy/timeseries/` with `GenericTimeSeries`, truncation, concatenation,
  resampling and the nine instrument sources.
- *Data Visualization*, *: 2D Graphics*, *: Line Plots* — `GenericMap.plot`/`peek` (WCSAxes imshow) and
  `GenericTimeSeries.plot`/`peek` (line plots).
- *: Mission-Specific* — `sunpy/visualization/colormaps/cm.py` registers instrument-specific colour
  tables (`sdoaia*`, `sohoeit*`, `soholasco*`, `stereocor*`, `stereohi*`, `yohkohsxt*`, `hinodexrt`,
  `trace*`, `hmimag`, `irissji*`, `goes-rsuvi*`, `solometis*`, `suit_*`, `kcor`, `rhessi`, `punch`).
- *: Movies* — `sunpy/visualization/animator/mapsequenceanimator.py` and `MapSequence.plot`, built on
  `mpl-animators`, produce animations over image sequences.
- *Models and Simulations* and *: Empirical* — `sunpy/sun/models.py` exposes
  `differential_rotation` (Howard/Allen/Snodgrass empirical laws) and the tabulated `interior` and
  `evolution` models of Turck-Chièze et al. (1988).

**Considered and rejected — do not re-propose without new code evidence.**
- *Data Processing and Analysis: Calibration* and *Mission-related: Calibration* — sunpy core performs
  no instrument calibration. Outside its tests, every occurrence of "calibrat*" in `sunpy/` is either a
  docstring describing someone else's data levels (`aia_synopsis.py`, `lyra.py`, `eve.py`, `asos.py`,
  `suit.py`, `genx.py`), a docstring bibliography entry citing an XRT calibration paper
  (`hinode.py`), or a `warn_user` message about a PHI WCS (`solo.py`); none of them is code. Calibration
  was deliberately moved out of sunpy: `docs/whatsnew/2.0.rst` records `sunpy.instr.aia.aiaprep` being
  removed in favour of aiapy's `register()`.
- *Data Processing and Analysis: Spectrogram* and *Data Visualization: Spectrogram* — the string
  package contains no spectrogram code: the word occurs in `sunpy/` only inside the generated CDAWeb
  dataset catalogue (`sunpy/net/cdaweb/data/attrs.json`), which describes other people's data products.
  `sunpy.spectra` was removed and replaced by the separate `radiospectra` package
  (`docs/whatsnew/1.0.rst`).
- *Data Visualization: 3D Graphics* — no 3D plotting API. The single `projection='3d'` use in the tree
  is one gallery example (`examples/plotting/finding_local_peaks_in_solar_data.py`) illustrating peak
  finding, not a capability sunpy offers.
- *Data Visualization: Orbit Plots* — sunpy computes spacecraft and body positions but ships no orbit
  plotting API. The 8.0.0 Artemis II trajectory item is a gallery example, and examples do not qualify.
- *Data Visualization: Web-Based* — `UnifiedResponse.show_in_notebook` (added in 7.1) renders an
  interactive `itables` search-results table in Jupyter. That is a results browser, not a data
  visualization.
- *Data Processing and Analysis: Data Assimilation* — sunpy reads ADAPT maps
  (`sunpy/map/sources/adapt.py`, `sunpy/net/dataretriever/sources/adapt.py`) but ADAPT's ensemble
  least-squares assimilation runs upstream at NSO; sunpy performs none of it.
- *Models and Simulations: Field-line Tracing* and *Data Processing and Analysis: Field-line Tracing* —
  PFSS extrapolation and tracing live in pfsspy / sunkit-magex, not in sunpy core.
- *Models and Simulations: Physics-Based* / *: Theory* — the only model content is the two static
  tables in `sunpy/sun/models.py`; `Empirical` already covers them and adding more model subcategories
  would overstate what sunpy computes.
- *Servers and Environments* (any subcategory) — sunpy is a client library. There is no Dockerfile in
  the repository and no server component; `sunpy-dev-env.yml` is a conda environment file.
- *Mission-related* (any subcategory) — sunpy is instrument-agnostic infrastructure, not part of any
  mission ground system, even though it reads many missions' products.

### 5. Related Region (MANDATORY)
- Solar Environment
- Corona
- Chromosphere
- Photosphere
- Interplanetary Space
- Earth Magnetosphere

- *Solar Environment* — the package's overall domain; retained from the stored record.
- *Corona* — EUV coronal imagers (`sdo.py` AIA, `soho.py` EIT, `stereo.py` EUVI,
  `suvi.py`, `proba2.py` SWAP, `solo.py` EUI) and coronagraphs (`soho.py` LASCO, `stereo.py` COR1/COR2
  and HI, `solo.py` Metis, `mlso.py` K-Cor, `punch.py`, `psp.py` WISPR) are all first-class map sources.
- *Chromosphere* — `gong.py` defines `GONGHalphaMap` for H-alpha imagery;
  `iris.py` `SJIMap` covers the IRIS Mg II k 2796 Å slit-jaw channel (`irissji2796` colour table);
  `suit.py`'s own docstring describes SUIT as imaging "the photosphere and chromosphere".
- *Photosphere* — magnetogram and photospheric-flux map sources: `sdo.py`
  `HMIMap`/`HMISynopticMap`, `soho.py` `MDIMap`/`MDISynopticMap`, `gong.py` `GONGSynopticMap` and
  `GONGMagnetogramMap`, `adapt.py` `ADAPTMap` (photospheric flux transport), `hinode.py` `SOTMap`,
  `solo.py` `PHIMap`; plus photospheric differential rotation in `sunpy/sun/models.py`.
- *Interplanetary Space* — heliospheric frames (`HeliocentricEarthEcliptic`, `HeliocentricInertial`)
  and the wide-field heliospheric imagers (STEREO HI-1/HI-2, PSP WISPR, PUNCH WFI).
- *Earth Magnetosphere* — the magnetospheric frames `Geomagnetic`, `SolarMagnetic` and
  `GeocentricSolarMagnetospheric` in `sunpy/coordinates/frames.py`.

**Considered and rejected — `Solar Interior`.** `sunpy/sun/models.py` publicly exposes `interior`, a
QTable of the standard solar interior structure (Turck-Chièze et al. 1988), which is why the region
was evaluated at all. It is not recorded: a single static reference table is reference data, not a
capability, and sunpy performs no helioseismology, interior modelling or interior analysis behind it.
This is the same reasoning that rejects *Models and Simulations: Physics-Based* and *: Theory* in
Field 4 — the table is already accounted for by *Models and Simulations: Empirical*. The evidence is
kept here so the region can be reconsidered if sunpy ever gains real solar-interior functionality.

**Considered and rejected — `Solar Wind`.** This was assessed specifically because sunpy has
heliospheric coordinate support. A full-tree search for "solar wind" in `sunpy/`, `examples/` and
`docs/` finds the phrase in prose only once, as a comment in
`examples/acquiring_data/soar_search_attrs.py` listing `"SWA": "Solar Wind Analyser"` among the SOAR
instrument names; every other hit is data rather than code — the generated VSO, CDAWeb and SOAR
attribute catalogues (`sunpy/net/vso/data/attrs.json`, `sunpy/net/cdaweb/data/attrs.json`,
`sunpy/net/soar/data/attrs.json`, `sunpy/net/soar/data/instrument_attrs.json`), which carry
third-party dataset and instrument titles rather than sunpy capabilities, and a FITS test header
(`sunpy/data/test/punch.header`) whose comment names PUNCH's fast/slow solar wind data products. sunpy provides no solar-wind data
structures, models, or analysis; `Interplanetary Space` already covers the heliospheric domain it does
serve. The remaining vocabulary rows — the ionospheric and thermospheric regions, the magnetosheath
and magnetotail subregions, the planetary magnetospheres, `Heliosheath` and `Earth Atmosphere` —
have no data-product counterpart in the code. The single near-miss is
`sunpy/timeseries/sources/eve.py`, whose `EVESpWxTimeSeries` docstring says the EUV range EVE measures
"provides the majority of the energy for heating Earth's thermosphere and creating Earth's ionosphere".
That is background motivation for why EVE observes solar EUV irradiance, not an EVE data product about
either region, so it does not support `Earth Ionosphere` or `Earth Thermosphere`. Contrast the SUIT
docstring cited under *Chromosphere* above, which was accepted because it describes what the
instrument's data *is*.


### 6. Authors (MANDATORY)
- **SunPy Community** | Author Identifier: https://github.com/sunpy/sunpy/blob/main/CITATION.cff

1. **Stuart J. Mumford** | ORCID: https://orcid.org/0000-0003-4217-4642 | Aperio Software Ltd.
2. **Nabil Freij** | ORCID: https://orcid.org/0000-0002-6253-082X | SETI Institute & Lockheed Martin Solar and Astrophysics Laboratory
3. **David Stansby** | ORCID: https://orcid.org/0000-0002-1365-1908 | University College London
4. **Albert Y. Shih** | ORCID: https://orcid.org/0000-0001-6874-2594 | NASA Goddard Space Flight Center
5. **Steven Christe** | ORCID: https://orcid.org/0000-0001-6127-795X | NASA Goddard Space Flight Center
6. **Jack Ireland** | ORCID: https://orcid.org/0000-0002-2019-8881 | NASA Goddard Space Flight Center
7. **Florian Mayer**
8. **Keith Hughitt** | ORCID: https://orcid.org/0000-0003-0787-9559 | Center for Cancer Research, National Cancer Institute  *(.zenodo.json roster form: V. Keith Hughitt)*
9. **Daniel F. Ryan** | ORCID: https://orcid.org/0000-0001-8661-3825 | Mullard Space Science Laboratory, University College London
10. **Simon Liedtke**
11. **Will Barnes** | ORCID: https://orcid.org/0000-0001-9642-6089 | Department of Physics, American University & NASA Goddard Space Flight Center
12. **Laura Hayes** | ORCID: https://orcid.org/0000-0002-6835-2390 | Dublin Institute for Advanced Studies
13. **David Pérez-Suárez** | ORCID: https://orcid.org/0000-0003-0784-6909 | University College London
14. **Vishnunarayan K I.**
15. **Pritish Chakraborty** | ORCID: https://orcid.org/0000-0001-8875-5819 | Manav Rachna University
16. **Andrew Inglis** | ORCID: https://orcid.org/0000-0003-0656-2437 | Catholic University of America & NASA Goddard Space Flight Center
17. **Punyaslok Pattnaik** | ORCID: https://orcid.org/0000-0001-6216-2353 | International Institute of Information Technology, Hyderabad
18. **Brigitta Sipőcz** | ORCID: https://orcid.org/0000-0002-3713-6337 | DIRAC Institute, University of Washington
19. **Ahmed Hossam** | ORCID: https://orcid.org/0009-0007-7321-9109 | Faculty of Computers and Informatics, Zagazig University
20. **Conor MacBride** | ORCID: https://orcid.org/0000-0002-9901-8723 | Astrophysics Research Centre, School of Mathematics and Physics, Queen's University Belfast
21. **Rishabh Sharma**
22. **Andrew J. Leonard** | ORCID: https://orcid.org/0000-0001-5270-7487 | Aperio Software Ltd.  *(.zenodo.json roster form: Andrew Leonard)*
23. **Russell Hewett** | ORCID: https://orcid.org/0000-0001-8944-4705 | Department of Mathematics, Virginia Polytechnic Institute and State University
24. **Alex Hamilton**
25. **Abhijeet Manhas** | ORCID: https://orcid.org/0000-0002-0757-2883 | School of Computing and Electrical Engineering, Indian Institute of Technology Mandi
26. **Asish Panda**
27. **Matt Earnshaw**
28. **Nitin Choudhary** | ORCID: https://orcid.org/0000-0001-6915-4583 | Department of Mathematics, Indian Institute of Technology, Kharagpur
29. **Ankit Kumar**
30. **Raahul Singh** | ORCID: https://orcid.org/0000-0003-4114-8856 | Indian Institute of Information Technology, Sri City
31. **Prateek Chanda** | ORCID: https://orcid.org/0000-0002-7068-2866 | Department of Computer Science & Technology, Indian Institute of Engineering Science & Technology, Shibpur
32. **Saurav Kumar Roy** | ORCID: https://orcid.org/0009-0007-3703-6532 | Amrita Vishwa Vidyapeetham, Amritapuri
33. **Shane Maloney** | ORCID: https://orcid.org/0000-0002-4715-1805 | Dublin Institute for Advanced Studies
34. **Pratham Hole** | ORCID: https://orcid.org/0009-0009-6926-1034
35. **Alasdair Wilson** | ORCID: https://orcid.org/0000-0003-0820-8159 | Oxford Research Software Engineering Team, University of Oxford
36. **Md Akramul Haque** | Department of Mechanical Engineering, ZHCET, Aligarh Muslim University
37. **Chris R. Gilly** | ORCID: https://orcid.org/0000-0003-0021-9056 | Southwest Research Institute
38. **Michael Kirk** | ORCID: https://orcid.org/0000-0001-9874-1429 | Catholic University of America & NASA Goddard Space Flight Center  *(.zenodo.json roster form: Michael S Kirk)*
39. **Michael Mueller**
40. **Sudarshan Konge**
41. **Matt Wentzel-Long** | ORCID: https://orcid.org/0000-0002-3106-4598 | Stark State College
42. **Rajul Srivastava**
43. **Samuel Bennett** | ORCID: https://orcid.org/0000-0001-6420-4422 | Aperio Software Ltd.
44. **Yash Jain** | ORCID: https://orcid.org/0000-0001-5347-4734 | Indian Institute of Technology, Kharagpur
45. **Lazar Zivadinovic** | ORCID: https://orcid.org/0000-0003-1349-1606
46. **Ankit Baruah** | Workato Gmbh, Germany
    - *Identity:* another project credits the same person under this identical name. The same commit address
      `ankit.baruah1@gmail.com` appears in this repository (`.mailmap` maps
      `abit2 <ankit.baruah1@gmail.com>` to the canonical `Ankit Baruah`) and in `ndcube`, so the two rows
      are one person. Neither held an ORCID, so the surviving row was chosen on breadth of catalogue use:
      the Workato Gmbh affiliation recorded here is the only affiliation any source gives him.
      **Creator 134 (`Ankit`) is a different person** — a mononym contributor at
      `emonstar333@gmail.com`, which this repository's `.mailmap` canonicalizes separately from
      `abit2 <ankit.baruah1@gmail.com>`, and `.zenodo.json` lists the two as distinct creators. They must
      not be conflated.
47. **Quinn Arbolante** | ORCID: https://orcid.org/0000-0003-0260-453X | Lockheed Martin Solar and Astrophysics Laboratory
48. **Trestan F. Simon** | ORCID: https://orcid.org/0009-0000-3029-8619
49. **Michael Charlton**
50. **Sashank Mishra** | ORCID: https://orcid.org/0000-0001-8302-1584 | Indian Institute of Information Technology, Allahabad
51. **Jeffrey Aaron Paul** | Dayananda Sagar College of Engineering, Bangalore
52. **Akash Verma**
53. **Nicky Chorley** | ORCID: https://orcid.org/0000-0002-2747-2716 | Centre for Fusion, Space and Astrophysics, Department of Physics, University of Warwick
54. **Aryan Chouhan** | ORCID: https://orcid.org/0000-0001-8004-7586 | Dwarkadas Jivanlal Sanghvi College of Engineering, University of Mumbai
55. **Himanshu**
56. **James Mason** | ORCID: https://orcid.org/0000-0002-3783-5509 | Laboratory for Atmospheric and Space Physics, University of Colorado Boulder  *(.zenodo.json roster form: James Paul Mason)*
57. **Sanskar Modi**
58. **Yash Sharma** | ORCID: https://orcid.org/0000-0002-7861-9677 | Indian Institute of Technology, Kharagpur
59. **Akshit Tyagi** | ORCID: https://orcid.org/0009-0005-4804-9035 | Jaypee Institute of Information Technology
60. **Aritra Sinha** | ORCID: https://orcid.org/0009-0008-2531-1012 | National Institute of Technology Karnataka, Surathkal
61. **Naman9639 (GitHub)** *(stored as givenName `Naman9639`, familyName `(GitHub)`)*
    - *Identity:* a proven platform handle with no published human name. The git author is
      `Naman9639 <31286078+Naman9639@users.noreply.github.com>`, whose noreply address encodes account ID 31286078 and
      login `Naman9639`. Capitalization is preserved verbatim. **No human name is asserted.**
62. **Monica Bobra** | ORCID: https://orcid.org/0000-0002-5662-9604
63. **Jose Ivan Campos Rozo** | ORCID: https://orcid.org/0000-0001-8883-6790 | Institut für Physik/IGAM, Karl-Franzens-Universität Graz
64. **Larry Manley**
65. **Kateryna Ivashkiv**
66. **Timo Laitinen** | ORCID: https://orcid.org/0000-0002-7719-7783 | Jeremiah Horrocks Institute, University of Central Lancashire
67. **Agneet Chatterjee** | ORCID: https://orcid.org/0000-0002-0961-9569 | Jadavpur University, Kolkata
68. **Ansh Dixit** | ORCID: https://orcid.org/0009-0004-7872-0419 | Graphic Era (Deemed to be University), Dehradun
69. **Brett J Graham** | ORCID: https://orcid.org/0000-0001-6315-4507 | Space Telescope Science Institute
70. **Jan Gieseler** | ORCID: https://orcid.org/0000-0003-1848-7067 | University of Turku
71. **Jayraj Dulange** | ORCID: https://orcid.org/0009-0003-2993-7382 | Indian Institute of Technology Gandhinagar
72. **Johan Lauritz Freiherr von Forstner** | ORCID: https://orcid.org/0000-0002-1390-4776 | Institute of Experimental and Applied Physics, University of Kiel; Paradox Cat GmbH  *(.zenodo.json roster form: Johan Freiherr von Forstner, affiliation given in German as "Institut für Experimentelle und Angewandte Physik")*
    - *Both affiliations, and why:* Paradox Cat GmbH is not evidence drawn from this software. solarmach
      credits this author under a name that splits the
      author's name as given "Johan L. Freiherr von", family "Forstner" — putting the nobiliary particle
      chain in the given name — and carried the Paradox Cat GmbH affiliation with no identifier; it was
      solarmach's author 3. ORCID `0000-0002-1390-4776` confirms Paradox Cat as the author's **current**
      employer and gives the authoritative split used here. Both affiliations are retained: his record
      carries the union of the institutions its sources attribute to him, and an affiliation is never
      dropped in favour of a newer one.
73. **Juanjo Bazán** | ORCID: https://orcid.org/0000-0001-7699-3983 | CIEMAT Particle Physics Unit
74. **Kris Akira Stern** | ORCID: https://orcid.org/0000-0003-1613-8947 | University of Hong Kong & University of London
75. **Aryan Shukla** | ORCID: https://orcid.org/0009-0001-9467-4836 | Indian Institute of Technology Roorkee
76. **John Evans**
77. **Sarthak Jain**
78. **Michael Malocha**
79. **Sourav Ghosh** | ORCID: https://orcid.org/0000-0002-7259-5651 | Jadavpur University, Kolkata
80. **Airmansmith97 (GitHub)** *(stored as givenName `Airmansmith97`, familyName `(GitHub)`)*
    - *Identity:* a proven platform handle with no published human name. The git author is
      `Airmansmith97 <40273565+Airmansmith97@users.noreply.github.com>`, whose noreply address encodes account ID 40273565 and
      login `Airmansmith97`. Capitalization is preserved verbatim. **No human name is asserted.**
81. **Ankit Khushwaha** | ORCID: https://orcid.org/0009-0009-3953-4206 | Indian Institute Of Technology Dharwad (IIT-DH)
82. **Dominik Stańczak** | ORCID: https://orcid.org/0000-0001-6291-8843 | University of Warsaw
83. **Manit Singh** | ORCID: https://orcid.org/0009-0002-6031-3810 | Netaji Subhas University of Technology
84. **Rajiv Ranjan Singh** | ORCID: https://orcid.org/0000-0002-1266-4790 | JSS Academy of Technical Education, Bengaluru
85. **Ruben De Visscher**
86. **Shresth Verma** | ORCID: https://orcid.org/0000-0003-0370-5471 | Atal Bihari Vajpayee-Indian Institute of Information Technology and Management, Gwalior
87. **Sophie Lemos**
88. **Ankit Agrawal**
89. **Arib Alam**
90. **Dumindu Buddhika**
91. **Hannah Collier** | ORCID: https://orcid.org/0000-0001-5592-8023 | University of Applied Sciences Northwestern Switzerland & ETH Zürich
92. **Haruhisa Iijima** | ORCID: https://orcid.org/0000-0002-1007-181X | Nagoya University (https://ror.org/04chrp450)
93. **Himanshu Pathak** | ORCID: https://orcid.org/0000-0001-9387-4492 | Shri Siddhi Vinayak Institute of Technology
94. **Jai Ram Rideout** | ORCID: https://orcid.org/0000-0003-2587-1454 | Dogfox Software LLC
95. **Swapnil Sharma**
96. **Wenli Mo** | ORCID: https://orcid.org/0000-0002-9179-9801 | Johns Hopkins Applied Physics Lab
97. **Daniel Garcia Briseno**
98. **Harsh Shah** | ORCID: https://orcid.org/0009-0000-0795-8471 | Dwarkadas Jivanlal Sanghvi College of Engineering, University of Mumbai
99. **Jongyeob Park** | ORCID: https://orcid.org/0000-0002-1063-9129 | Space Science Division, Korea Astronomy and Space Science Institute
100. **Matt Bates**
101. **Tanish Yelgoe** | Indian Institute of Technology Gandhinagar (IIT-GN)
102. **Devansh Shukla** | ORCID: https://orcid.org/0000-0003-0610-9747 | Sardar Vallabhbhai National Institute of Technology, Surat
103. **Marius Giger** | ORCID: https://orcid.org/0000-0002-6863-6502 | FHNW - University of Applied Sciences and Arts Northwestern Switzerland
104. **Pankaj Mishra**
105. **Deepankar Sharma**
106. **Dhruv Goel**
107. **Garrison Taylor** | Center for Astrophysics | Harvard & Smithsonian
108. **Goran Cetusic**
109. **Guntbert Reiter**
110. **Jacob**
111. **Mateo Inchaurrandieta**
     - *Identity:* ndcube credits the same person under this identical name; the same commit
       address `mateo.inchaurrandieta@gmail.com` appears here and in `ndcube` (as `mateoi`), so they are
       one person, and the catalogue holds a single record for them. No source supplies an ORCID
       or an affiliation for him. Recorded so a future refresh does not treat the two credits as two
       people.
112. **Piyush Sharma** | ORCID: https://orcid.org/0009-0005-1579-5787 | Indian Institute of Technology Roorkee
113. **Sally Dacie** | ORCID: https://orcid.org/0000-0001-7572-2903 | Mullard Space Science Laboratory, University College London
114. **Sanjeev Dubey**
115. **Arthur Eigenbrot** | ORCID: https://orcid.org/0000-0003-0810-4368 | National Solar Observatory
116. **Benjamin Mampaey** | ORCID: https://orcid.org/0000-0001-6541-4966 | Royal Observatory of Belgium
117. **Erik Bray**
118. **Maya Mohamed** | Cairo University
119. **Nicholas A. Murphy** | ORCID: https://orcid.org/0000-0001-6628-8033 | Center for Astrophysics | Harvard & Smithsonian  *(.zenodo.json roster form: Nick Murphy)*
120. **Rutuja Surve**
121. **Samuel Jackson**
122. **Serge Zahniy** | ORCID: https://orcid.org/0000-0001-8835-7087 | NASA Goddard Space Flight Center
123. **Sudeep Sidhu**
124. **Tomas Meszaros**
125. **Utkarsh Parkhi**
126. **William Russell**
127. **Abhigyan Bose**
128. **Abhishek Pandey**
129. **Abinash Mahapatra** | ORCID: https://orcid.org/0009-0000-5975-6775 | Odisha University of Technology and Research
130. **Adrian Price-Whelan** | ORCID: https://orcid.org/0000-0003-0872-7098 | Center for Computational Astrophysics, Flatiron Institute
131. **Amogh Jahagirdar**
132. **André Chicrala** | ORCID: https://orcid.org/0000-0002-5230-4909 | Northumbria University
133. **Aniket Mishra** | ORCID: https://orcid.org/0009-0008-4790-5604
134. **Ankit**
     - *A distinct contributor — do not conflate with creator 46.* This is a mononym contributor at
       `emonstar333@gmail.com`; this repository's `.mailmap` canonicalizes that address to the mononym
       `Ankit`, separately from `abit2 <ankit.baruah1@gmail.com>` → `Ankit Baruah` (creator 46), and
       `.zenodo.json` lists the two as distinct creators. GitHub attributes this contributor's commit
       `303d517715e60fbf297c066186d482eeacce73c3` to no account, so no platform identity is available and
       the stored string carries no platform label. `github.com/ankit` belongs to an unrelated person and
       must not be used as evidence here.
135. **Chloé Guennou**
136. **Daniel D'Avella**
137. **Daniel Williams** | ORCID: https://orcid.org/0000-0003-3772-198X | School of Physics & Astronomy, University of Glasgow
138. **Dipanshu Verma** | ORCID: https://orcid.org/0000-0003-2461-5547 | Indian Institute of Technology, Mandi
139. **Jordan Ballew**
140. **Krish Agrawal**
141. **Mingyu Jeon** | ORCID: https://orcid.org/0009-0004-7798-5052 | Kyung Hee University
142. **Mubin Manasia**
143. **Neeraj Kulkarni**
144. **Nischal Singh** | ORCID: https://orcid.org/0009-0007-2165-052X | Madhav Institute of Technology & Science, Gwalior
145. **Ole Streicher** | ORCID: https://orcid.org/0000-0001-7751-1843 | Leibniz Institute for Astrophysics Potsdam
146. **Priyank Lodha**
147. **Sam Van Kooten** | ORCID: https://orcid.org/0000-0002-4472-8517 | Southwest Research Institute  *(.zenodo.json roster form: Samuel J. Van Kooten)*
148. **Shivansh Mishra**
149. **Thomas Robitaille**
150. **Tom Augspurger**
151. **Yash Krishan**
152. **Abijith Bahuleyan**
153. **Advait Pimparkar**
154. **Adwait Bhope** | ORCID: https://orcid.org/0000-0002-7133-8776 | Savitribai Phule Pune University
155. **Ahmad Saeed**
156. **Amarjit Singh Gaba** | ORCID: https://orcid.org/0000-0002-9505-0160 | School of Mathematics, Cardiff University
157. **Andrew Hill**
158. **Bernhard M. Wiedemann**
159. **Carlos Molina** | ORCID: https://orcid.org/0000-0003-0300-4106 | SUGUS-GNULinux
     - *Affiliation source:* SUGUS-GNULinux is not evidence drawn from this software.
       `sunkit-instruments` credits the same person with that affiliation and no ORCID; the same commit
       address `carlosmolina.ord@gmail.com` appears here and there (as `cmolinaord`), so they are one
       person and his record carries the union of what both projects supply.
160. **Diya Khetarpal** | ORCID: https://orcid.org/0009-0009-4729-6797
161. **Duygu Keşkek**
162. **Ishtyaq Habib**
163. **Joseph Letts** | ORCID: https://orcid.org/0000-0001-9900-739X
164. **Karthikeyan Singaravelan**
165. **Kritika Ranjan** | ORCID: https://orcid.org/0000-0001-5638-016X | Jain (Deemed-to-be University), Bangalore
166. **Mridul Pandey**
167. **Noah Altunian**
168. **Reid Gomillion**
169. **Samriddhi Agarwal** | ORCID: https://orcid.org/0000-0003-4497-1637 | Ryan International School, Bengaluru, Karnataka
170. **Yash Kothari**
171. **Yash Malik** | ORCID: https://orcid.org/0009-0005-7611-034X
172. **Yukie Nomiya** | ORCID: https://orcid.org/0000-0002-9572-6300 | Sapienza University of Rome
173. **Zach Burnett** | Space Telescope Science Institute
174. **Abigail L. Stevens** | ORCID: https://orcid.org/0000-0002-5041-3079 | Department of Physics & Astronomy, Michigan State University & Department of Astronomy, University of Michigan
175. **Akhoury Shauryam** | ORCID: https://orcid.org/0009-0005-8038-8301 | Chennai Mathematical Institute
176. **Alex Kaszynski**
177. **Alex Wang**
178. **Ambar Mehrotra**
179. **Andy Tang**
180. **Anubhav Sinha**
181. **Arfon Smith**
182. **Arseniy Kustov**
183. **Ashish Bastola** | ORCID: https://orcid.org/0009-0006-4968-1005 | Clemson University
184. **Brandon Stone**
185. **Chris Bard**
186. **Chris Lowder** | ORCID: https://orcid.org/0000-0001-8318-8229 | Southwest Research Institute
187. **Clément Robert** | ORCID: https://orcid.org/0000-0001-8629-7068
188. **Ed Behn**
189. **Ed Mansky**
190. **Emmanuel Arias**
191. **Enrico Paganin**
192. **Erik Tollerud**
193. **Fionnlagh Mackenzie Dover** | ORCID: https://orcid.org/0000-0002-1984-7303 | SP2RC, School of Mathematics and Statistics, University of Sheffield
194. **Freek Verstringe** | Royal Observatory of Belgium
195. **FreyaJain (GitHub)** *(stored as givenName `FreyaJain`, familyName `(GitHub)`)*
     - *Identity:* a proven platform handle. GitHub's commit API attributes commit
       `97a50905a20e4c20c9964d7d7d5446a2a3a2c979` to account **`FreyaJain` (ID 150811763)**. The string
       resembles a real name, but the account publishes none, so **no human name is asserted** — only the
       handle and its platform are recorded.
196. **Fu Yu** | Purple Mountain Observatory
197. **Ghaith Kdimati** | ORCID: https://orcid.org/0009-0006-8851-7814 | Cairo University
198. **Gulshan Kumar** | ORCID: https://orcid.org/0000-0001-8523-7223 | International Institute of Information Technology, Hyderabad
199. **Hardik**
200. **Harsh Mathur** | ORCID: https://orcid.org/0000-0001-5253-4213 | Indian Institute of Astrophysics, Bengaluru
201. **Igor Babuschkin**
202. **James Calixto**
203. **Jaylen Wimbish**
204. **Jia Qing**
205. **Juan Camilo Buitrago-Casas**
206. **Kalpesh Krishna** | ORCID: https://orcid.org/0000-0001-6574-0817 | University of Massachusetts Amherst
207. **Kaustubh Chaudhari** | ORCID: https://orcid.org/0000-0003-1734-5075 | Atal Bihari Vajpayee Indian Institute of Information Technology and Management, Gwalior
208. **Kaustubh Hiware** | ORCID: https://orcid.org/0000-0003-3301-1016 | Indian Institute of Technology, Kharagpur
209. **Koustav Ghosh**
210. **Kurt McKee** | ORCID: https://orcid.org/0000-0002-8547-8489 | University of Chicago
211. **Manas Mangaonkar**
212. **Manish Tiwari**
213. **Mark C. M. Cheung** | ORCID: https://orcid.org/0000-0003-2110-9753 | Lockheed Martin Solar and
     Astrophysics Laboratory
     - *Identity:* an earlier revision of this file recorded "Mark Cheung" with no identifier or
       affiliation, matching
       this project's `.zenodo.json` creator string. ORCID `0000-0003-2110-9753` carries **both** forms
       itself: its primary name is "Mark Cheung" and its credit name is "Mark CM Cheung", with employment
       at the Lockheed Martin Advanced Technology Center. The two HSSI rows — this one and aiapy's author
       3 — are that one record's two published forms, so the catalogue holds a single record for him. The
       roster form "Mark Cheung" is preserved in this note, so a refresh reading `.zenodo.json` recognises
       it.
214. **Matthew Mendero**
215. **Megh Dedhia** | ORCID: https://orcid.org/0000-0002-5828-7679 | Dwarkadas Jivanlal Sanghvi College of Engineering, University of Mumbai
216. **Mickaël Schoentgen** | ORCID: https://orcid.org/0000-0002-0106-4810
217. **Mika**
218. **Mouloudi Mohamed Lyes**
219. **Nakshatra** | Indian Institute of Technology, Kharagpur
220. **Nakul Shahdadpuri**
221. **Naveen Srinivasan**
222. **Norbert G Gyenge** | ORCID: https://orcid.org/0000-0003-0464-1537 | SP2RC, School of Mathematics and Statistics, University of Sheffield
223. **OussCHE (GitHub)** *(stored as givenName `OussCHE`, familyName `(GitHub)`)*
     - *Identity:* a proven platform handle with no published human name. The git author is
       `OussCHE <72355098+OussCHE@users.noreply.github.com>`, whose noreply address encodes account ID 72355098 and
       login `OussCHE`. Capitalization is preserved verbatim. **No human name is asserted.**
224. **Paul Wright** | ORCID: https://orcid.org/0000-0001-9021-611X | Dublin Institute for Advanced Studies  *(.zenodo.json roster form: Paul J. Wright)*
225. **Prisha Sharma**
226. **Raghav Agrawal** | ORCID: https://orcid.org/0009-0000-1788-2917 | Netaji Subhas University of Technology, New Delhi (NSUT New Delhi) and Indian Institute of Technology, Madras (IIT Madras)
227. **Rahul Gopalakrishnan** | ORCID: https://orcid.org/0000-0002-1282-3480 | Inter-University Centre for Astronomy and Astrophysics (IUCAA), Pune
228. **Rajasekhar Reddy Mekala**
229. **Ratul Das** | ORCID: https://orcid.org/0000-0002-5845-9979 | National Institute of Science Education and Research, Bhubaneswar
230. **Rehan Chalana** | Chitkara University, Punjab
231. **Rishabh Mishra**
232. **Rohan Sharma**
233. **Samuel T. Badman** | ORCID: https://orcid.org/0000-0002-6145-436X | Center for Astrophysics | Harvard & Smithsonian
234. **Shashank Srikanth** | International Institute of Information Technology, Hyderabad
235. **Shubham Jain**
236. **Sijie Yu** | ORCID: https://orcid.org/0000-0003-2872-2614 | New Jersey Institute of Technology
237. **Sirjan Hansda** | ORCID: https://orcid.org/0009-0004-0333-3166 | Indian Institute of Science, Karnataka
238. **Suleiman Farah** | ORCID: https://orcid.org/0009-0001-3304-2923 | University of Toronto
239. **Swapnil Kannojia** | ORCID: https://orcid.org/0000-0002-4233-774X | Maulana Azad National Institute of Technology Bhopal
240. **Syed Md Mihan Chistie** | ORCID: https://orcid.org/0009-0007-5883-2749 | Dayananda Sagar University, Bangalore
241. **Tan Jia Qing** | ORCID: https://orcid.org/0009-0003-6749-982X | Nanyang Technological University
242. **Tannmay Yadav** | ORCID: https://orcid.org/0000-0002-3143-5635 | Department of Chemical Engineering, Indian Institute of Technology, Kharagpur
243. **Tathagata Paul**
244. **Tessa D. Wilkinson**
245. **Thomas A Caswell**
246. **Thomas Braccia**
247. **Tiago M. D. Pereira** | ORCID: https://orcid.org/0000-0003-4747-4329 | Rosseland Centre for Solar Physics, University of Oslo & Institute of Theoretical Astrophysics, University of Oslo
248. **Tim Gates**
249. **Trung Kien Dang** | ORCID: https://orcid.org/0000-0001-7562-6495 | Saw Swee Hock School Of Public Health, National University Of Singapore
250. **Varun Bankar**
251. **William Jamieson** | ORCID: https://orcid.org/0000-0001-5976-4492
252. **William Setterberg** | ORCID: https://orcid.org/0000-0003-2165-8314 | University of Minnesota
253. **Yudhik Agrawal** | ORCID: https://orcid.org/0000-0003-3827-6857 | International Institute of Information Technology, Hyderabad
254. **_Gagan**
255. **eebbaaf (GitHub)** *(stored as givenName `eebbaaf`, familyName `(GitHub)`)*
     - *Identity:* a proven platform handle with no published human name. The git author is
       `eebbaaf <147119367+eebbaaf@users.noreply.github.com>`, whose noreply address encodes account ID 147119367 and
       login `eebbaaf`. Capitalization is preserved verbatim. **No human name is asserted.**
256. **graham** *(unchanged — see note)*
     - *A distinct contributor — do not conflate with creator 69.* GitHub's commit API attributes this
       contributor's commit `1e2a628abe9c1f420bf7ae174ec1fc5433b2183b` to account **`grahamasam`
       (ID 107145436)**, and the git address is `grahamasam@gmail.com`. This is **not** creator 69
       (Brett J Graham, `brettgraham@gmail.com`, ORCID `0000-0001-6315-4507`): this repository's own
       `.mailmap` aliases `Brett` and `Brett Graham` to `Brett J Graham` and deliberately declines to
       alias `graham`, and `.zenodo.json` lists the two as separate creators. Because both are authors of
       *this* software, merging them would additionally breach the one-author-per-software constraint and
       lose a slot. The stored string is that account's display name, not the handle, so it carries no
       platform label. **A future audit must not propose this merge.**
257. **pradeep**
258. **resakra (GitHub)** *(stored as givenName `resakra`, familyName `(GitHub)`)*
     - *Identity:* a proven platform handle with no published human name. The git author is
       `resakra <69106920+resakra@users.noreply.github.com>`, whose noreply address encodes account ID 69106920 and
       login `resakra`. Capitalization is preserved verbatim. **No human name is asserted.**
259. **yasintoda** *(unchanged — see note)*
     - *No platform identity resolves.* Examined under both prongs of the platform-attribution standard
       and neither is satisfied: `gh api users/yasintoda` returns 404, and GitHub's commit API attributes
       commit `49abb2a9106bf3d7464de08d171b595f0b176447` to **no account**. The git address is
       `yasintoda@riseup.net`, whose local part equals the string — suggestive of a username, but a
       display name matching an email local part does not by itself prove handle status, and no platform
       identity resolves. Retained exactly as stored, with **no label**, unless stronger evidence appears.
260. **Raphael Attie** | ORCID: https://orcid.org/0000-0003-4312-6298
261. **Sophie A. Murray** | ORCID: https://orcid.org/0000-0002-9378-5315
262. **Jonas Sinjan** | ORCID: https://orcid.org/0000-0002-5387-636X | Max Planck Institute for Solar System Research
263. **Herman le Roux** | ORCID: https://orcid.org/0000-0002-1805-0706 | Dublin Institute for Advanced Studies & Technological University of the Shannon: Midlands Midwest
264. **Aleksandr Burtovoi** | ORCID: https://orcid.org/0000-0002-8734-808X | University of Florence
265. **Yaocheng Chen** | ORCID: https://orcid.org/0000-0002-8967-4911 | Korea Astronomy and Space Science Institute (https://ror.org/04g2pxh42) & Universidade de São Paulo
266. **Giovanna Jerse**
267. **Daragh M. Hollman** | ORCID: https://orcid.org/0009-0004-8128-2384 | Dublin Institute for Advanced Studies
268. **Kumar Amityush** | ORCID: https://orcid.org/0009-0002-7950-0886 | Indian Institute of Technology Madras
269. **Kevin Reardon**
270. **Sabrina Savage**
271. **Kolja Glogowski**
- Source: `CITATION.cff` names "The SunPy Community" as the group author, and the curated
  `.zenodo.json` creator roster at revision ed70935 supplies the individual contributors and their
  ORCIDs and affiliations, except where a note below records a different source. The `.zenodo.json` roster grew from 261 to 268 individuals since the
  2026-06-10 extraction; the seven added entries (Jonas Sinjan, Herman le Roux, Aleksandr Burtovoi,
  Yaocheng Chen, Giovanna Jerse, Daragh M. Hollman, Kumar Amityush) are numbers 262–268 above.
  Nobody was dropped: every contributor recorded in the previous extraction is still present in the
  current roster. With the "SunPy Community" group entry the full list is **272 author entries** —
  the group author plus 271 individuals.
- **Numbers 269–271 (Kevin Reardon, Sabrina Savage, Kolja Glogowski) come from `CITATION.cff` alone**,
  and are recorded because the author list is the union of every authoritative source: HSSI's stored
  roster, this file, and `CITATION.cff`. Nobody is ever dropped for appearing in only one of them.
  Their provenance is worth knowing, because it explains why they carry no ORCID or affiliation: they
  appear in the `CITATION.cff` author block (spelled `Reardon, Kevin`; `Savage, Sabrina`;
  `Glogowski, Kolja`) and in the matching BibTeX author list in `CITATION.rst`, but they are absent
  from `.zenodo.json` and absent from the repository's git shortlog. That pattern identifies them as
  co-authors of the 2020 ApJ reference publication rather than code contributors, and the SunPy
  Project's `.zenodo.json` — which is the roster of
  people who wrote the software — correctly omits them. No ORCID or affiliation exists for them in
  any repository source, so name-only entries are the complete and correct record; do not invent one.
- **Eight contributors are recorded under the name HSSI stores, not the `.zenodo.json` form**, with
  the roster spelling shown in parentheses on those lines. Identity was established by ORCID, which
  matches exactly in all eight cases: Keith Hughitt (0000-0003-0787-9559), Andrew J. Leonard
  (0000-0001-5270-7487), Michael Kirk (0000-0001-9874-1429), James Mason (0000-0002-3783-5509),
  Johan Lauritz Freiherr von Forstner (0000-0002-1390-4776), Nicholas A. Murphy
  (0000-0001-6628-8033), Sam Van Kooten (0000-0002-4472-8517), Paul Wright (0000-0001-9021-611X).
  These are shared person records used by other HSSI entries, and the submission API does not rename
  a person, so switching them to the roster spelling would be both risky and ineffective. A future
  refresh should match these authors on ORCID and leave the names alone.
- One upstream data defect is deliberately not copied: `.zenodo.json` currently wraps Raahul Singh's
  affiliation in zero-width space characters (U+200B). The clean string
  "Indian Institute of Information Technology, Sri City" is recorded instead. Do not "correct" it back.
- **Six authors' affiliations are recorded as the institution names HSSI holds for them, which for
  four of them is not the `.zenodo.json` string.** Jonas Sinjan (Max Planck Institute for Solar System
  Research) and Daragh M. Hollman (Dublin Institute for Advanced Studies) match the roster exactly.
  The other four do not, and the plain institution name is what is recorded: the roster gives
  "University of Florence, Department of Physics and Astronomy" for Aleksandr Burtovoi, "Indian
  Institute of Technology, Madras, India" for Kumar Amityush, a street address after the institute
  name for Yaocheng Chen, and "Dublin Institute for Advanced Studies and the Technological University
  of the Shannon" for Herman le Roux, whose second institution is recorded under its full official
  name, "Technological University of the Shannon: Midlands Midwest". Departments, postal addresses and
  country suffixes are not part of these institutions' identities; do not restore the roster wording
  over any of the six. This is specific to these six entries; two further entries are covered by the
  next note, and the general rule below governs the remainder of the roster, where the
  `.zenodo.json` wording stands even when HSSI's organization row is named differently.
- **Two further affiliations are recorded under their canonical institution names rather than the
  `.zenodo.json` wording, because the roster strings are alternate wordings of institutions this same
  author list already names in full.** Daniel F. Ryan's roster affiliation reads "University College
  London, Mullard Space Science Laboratory (UCL/MSSL)" and Nakshatra's reads "IIT Kharagpur" — an
  inverted word order carrying a parenthetical acronym, and a bare acronym. They are recorded here as
  **Mullard Space Science Laboratory, University College London** and **Indian Institute of
  Technology, Kharagpur**, the forms other entries in this list already carry: Sally Dacie (number
  113) takes the MSSL wording straight from `.zenodo.json`, and Yash Jain, Yash Sharma and Kaustubh
  Hiware (numbers 44, 58 and 208) take the comma-bearing Kharagpur form. Recording the acronym
  variants instead would assert two additional institutions that have no separate existence. Do not
  restore either roster string.
  - *The Kharagpur spelling keeps its comma.* The institute's ROR record,
    `https://ror.org/03w5sq511`, displays the name without one ("Indian Institute of Technology
    Kharagpur"). The comma-bearing form is the spelling the catalogue holds and the one this file
    records; the difference is punctuation inside a single institution's identity, not a second
    institution, and it is not a correction waiting to be made. The Kharagpur ROR is cited here as
    evidence for the spelling only, not as a recorded affiliation identifier. Affiliations in this
    list are written as bare institution names except where a ROR is given in parentheses directly
    after the name; the other identifiers on these lines are the authors' own ORCIDs and, for the
    group author, its citation file.
  - *MSSL is a sub-unit of University College London, not a synonym for it.* The laboratory has no
    ROR record of its own, so an identifierless entry is its correct and complete form; do not invent
    an identifier for it. Neither should it be folded into University College London
    (`https://ror.org/02jx3x895`), which David Stansby (number 3) and David Pérez-Suárez (number 13)
    carry in its own right. The laboratory and the university are distinct affiliations and both are
    legitimate.
- **Affiliations here are sunpy's own attribution, and a difference from HSSI's stored value is not
  drift.** HSSI person records are shared across software entries, so the affiliations HSSI holds for
  an author are the union of every entry that credits them — additional organizations, and sometimes
  an affiliation where sunpy's roster gives none at all. This dossier records what `.zenodo.json`,
  sunpy's own authoritative roster, attributes. Do not reconcile the two in either direction: neither
  strip the organizations that other entries' crediting contributed, nor import them into this file.
  Differing institution names are the same story — HSSI's Organization table has its own canonical row
  names, which need not match the roster's wording, so a differently worded institution is not a
  correction waiting to be made. Where the roster supplies no affiliation, a blank entry here is the
  complete and correct record, not a gap to fill from HSSI. Yaocheng Chen is the one deliberate
  exception, for the reason given next.
- **Yaocheng Chen's affiliation is a shared record, and the exception to the rule above.** The person
  already existed in HSSI under this same ORCID because another software entry lists them, and SunPy's
  own author addition is what produced the union now held: Korea Astronomy and Space Science Institute
  from the pre-existing record, Universidade de São Paulo from SunPy's. Because that union is the
  result of this entry's own attribution rather than another entry's, both institutions are recorded
  here. The Korea institute is therefore not foreign drift and must not be stripped, and the long
  `.zenodo.json` address string must not be restored in its place.
- **Raphael Attie's ORCID comes from HSSI's stored record, not from `.zenodo.json`.** The roster gives
  no identifier for them, while HSSI holds https://orcid.org/0000-0003-4312-6298, which matches the
  public ORCID record for this person; it is recorded here because it is real and the roster's silence
  is simply an omission. A future refresh reading only the roster will not find it and must not delete
  it as unsourced. No affiliation is recorded for them, for the reason above.
- **A standing hazard for any future author update.** Replacing
  this author list through the API is unsafe while any stored author record carries an empty given name:
  an author update re-sends the entire list, the API rejects an empty given or family name, and the whole
  field fails. **Ten** stored author records are in that state: `Himanshu`, `Jacob`, `Ankit`, `Hardik`,
  `Mika`, `Nakshatra`, `graham`, `pradeep`, `yasintoda` and `_Gagan`. Six further creators whose strings
  are proven platform handles — `Naman9639`, `Airmansmith97`, `OussCHE`, `eebbaaf`, `resakra` and
  `FreyaJain` — carry that handle as their given name and so are not affected.

  Those ten are deliberate, not unfinished work. Each stored string is the contributor's *display name*,
  not a handle — GitHub's commit API names a different account for each (`himanshukgp`, `sudozer`,
  no-account, `pythonicforge`, `tal66`, `naxatra2`, `grahamasam`, `gmrpr321`, no-account, `seika-afk`) —
  and four of them are canonicalized to exactly these mononyms by this repository's own `.mailmap`
  (`Himanshu`←`himanshukgp` at :86, `Jacob`←`sudozer` at :93, `Mika`←`tal66` at :138,
  `Ankit`←`ankit` at :35). `_Gagan` cannot be a handle at all, since GitHub logins may not begin with an
  underscore.

  **Substituting an invented given name for any of the ten is still not a workaround and must not be
  tried** — they carry no identifier, so an author is matched by exact agreement on both name parts, and a
  substituted name would silently create a duplicate person instead of matching the existing record.
  **Substituting the *handle* is also wrong**: the handle is a different string from the stored display
  name, so it would likewise fail to match, and it would misrepresent a person's chosen name as a
  username. Fixing this properly needs the API-side change tracked in issue #68, not a metadata edit.

### 7. Software Name (MANDATORY)
- **Name:** SunPy
- **Full Name:** SunPy - Python for Solar Physics
- Source: PyHC core registry (`name: "SunPy"`, `description: "Python for Solar Physics"`), the Zenodo
  and DataCite title "sunpy: A Core Package for Solar Physics", and the repository itself.
- The project styles the package `sunpy` in lower case and the project "The SunPy Project". `SunPy`
  is the stored name and the form PyHC uses, and it is kept — the casing difference is presentational,
  not a factual error, and renaming would churn a value a submitter chose deliberately.

### 8. Description (MANDATORY)
- **Description:** sunpy is a Python software package that provides fundamental tools for accessing, loading and interacting with solar physics data in Python. It includes an interface for searching and downloading data from multiple data providers, data containers for image and time series data, commonly used solar coordinate frames and associated transformations, as well as other functionality needed for solar data analysis.
- Source: `README.rst` at the pinned revision — these are the README's own two sentences, and they
  are the same text HSSI stores.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** SunPy core package: Python for Solar Physics. Provides tools for accessing, loading, and interacting with solar physics data including image maps, time series, coordinates, and data search.
- Source: first sentence is the `pyproject.toml` `description` field verbatim
  (`description = "SunPy core package: Python for Solar Physics"`); the remainder condenses the README.
  Kept as stored — it is accurate at the current revision and rewording it would be style, not fact.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2011-08-06
- Source: GitHub repository creation timestamp `2011-08-06T15:34:08Z`, taken from the GitHub API
  rather than from the earlier SoMEF-derived value, which SoMEF's unreliability makes weaker evidence.
- Not the DOI's publication year: DataCite reports `publicationYear: 2026` because the concept DOI
  tracks the newest release. The first-availability date of the software is the older, more useful
  value for this field, and the release date lives in Field 12.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org
- Source: DataCite `publisher` for 10.5281/zenodo.591887.

### 12. Version (RECOMMENDED)
- **Version Number:** v8.0.0
- **Version Date:** 2026-06-30
- **Version PID:** https://doi.org/10.5281/zenodo.21073705
- **Version Description:** SunPy 8.0.0 is a major release. Breaking changes: the `reference_date`
  property of `AIAMap` and `HMIMap` now returns a value on the same time scale as `date`, to prevent
  subtle user error; minimum dependency versions were raised across the board (astropy >=7.0.0,
  numpy >=2.0.0, matplotlib >=3.10.0, scipy >=1.14.0, pandas >=2.3.0, spiceypy >=7.0.0, drms >=0.8.0,
  reproject >=0.14.0 among others). New features: the Solar Orbiter Archive can be queried through
  `Fido` with no extra install because the `sunpy-soar` package has been merged into sunpy; new map
  sources `PHIMap` for the Solar Orbiter Polarimetric and Helioseismic Imager and `METISMap` for the
  Metis coronagraph (with a default `mask` property and a gallery example); `astropy.table.QTable`
  objects holding `SkyCoord`s in `sunpy.coordinates` frames can be saved to and read back from FITS;
  `get_horizons_coord` can print the JPL Horizons response; and sunpy can be built for free-threaded
  Python. Fixes include SIP distortion information no longer being ignored when building a Map WCS,
  thread-safety corrections in the `SphericalScreen`, `PlanarScreen`, `propagate_with_solar_surface`
  and `transform_with_sun_center` context managers, corrected Level 1 detection in `EITMap`, corrected
  SUIT colormap values, a SPICE time-conversion error of up to 1.6 ms, an updated ADAPT filename
  pattern, and a SOLARNET client switch to the `solarnet.oma.be` host.
- Source: git tag `v8.0.0` (commit-dated 2026-06-30), the 8.0.0 section of `CHANGELOG.rst`, the PyPI
  release of 8.0.0 uploaded 2026-06-30T12:08:05Z, and Zenodo record 21073705 (`version: v8.0.0`,
  `publication_date: 2026-06-30`), whose parent is the concept DOI in Field 2.
- **Supersedes the stored `v7.1.2` / 2026-04-19 / no Version PID.** Three tags were created after
  `v7.1.2` and before the release: `v8.1dev` is a development marker and `v8.0.0rc1` and `v8.0.0rc2`
  are release candidates. Only `v8.0.0` is an authoritative version. The earlier note "Not found for v7.1.2" was correct for that
  release but must not be carried forward: Zenodo does now mint a version DOI for 8.0.0, and
  10.5281/zenodo.21073705 resolves.
- **Write the number as `v8.0.0`, with the leading `v` and no software-name prefix.** HSSI prefixes
  the software name when it renders this field — the stored `SoftwareVersion.number` was `v7.1.2`
  while the record displayed `SunPy - v7.1.2`. The name and separator are added at render time and the
  `v` belongs to the value, so copying a rendered string back into this field would corrupt the record.

### 13. Programming Language (RECOMMENDED)
- Python 3.x
- C
- Source: `pyproject.toml` (`requires-python = ">=3.12"`, classifiers for Python 3.11–3.14) and the C
  extension under `sunpy/io/src/ana` built through `extension-helpers`. GitHub's language breakdown
  agrees on the two implementation languages by volume (Python ~2.50 MB, C ~77 kB).
- GitHub also reports Xonsh, IDL and Shell. None is an implementation language: the IDL is a single
  test-fixture generator (`sunpy/io/tests/generate_genx.pro`), the Xonsh is one release-notes tool
  (`tools/generate_releaserst.xsh`), and the Shell is CI glue. Do not add them.

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.3847/1538-4357/ab4f7a
- Title: "The SunPy Project: Open Source Development and Status of the Version 1.0 Core Package",
  The Astrophysical Journal 890(1):68, 2020.
- Source: `CITATION.cff` and the BibTeX block in `CITATION.rst`, which instructs users that "The
  project citation should be to the SunPy paper". Resolves; open access under CC-BY.
- The 2023 Frontiers paper describes the SunPy Project more currently, but the repository's own
  citation instructions still nominate the 2020 ApJ paper as *the* project citation, so it stays as
  the reference publication and the others remain in Field 27.

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://spdx.org/licenses/BSD-2-Clause
- Source: `LICENSE.rst`, re-read at revision ed70935. It carries exactly two conditions (source-form
  and binary-form redistribution notices) and no third non-endorsement clause, which makes it
  2-clause BSD. GitHub's own licence detection reports `BSD-2-Clause`, and `.zenodo.json` declares
  `"license": "BSD-2-Clause"`.
- **The conflicting declaration in `pyproject.toml` persists and is still wrong.** That file now
  declares `license = "BSD-3-Clause"` as an SPDX expression (it previously used the classifier form).
  The licence text governs, so the 2-clause value stands. This is durable: a future refresh reading
  only `pyproject.toml` will be tempted to "correct" the record to 3-clause and should not.
- The live `License` vocabulary offers both `BSD 2-Clause "Simplified" License` and
  `BSD 3-Clause "New" or "Revised" License`; the stored value matches the former exactly.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- astronomy
- astropy
- coronagraph
- coronal holes
- coordinates
- data analysis
- data retrieval
- fits
- hacktoberfest
- heliophysics
- heliosphere
- image processing
- magnetogram
- python
- science
- solar
- solar imaging
- solar physics
- sun
- sunpy
- time series
- wcs
- Source: `pyproject.toml` `keywords` (`solar physics`, `solar`, `science`, `sun`, `wcs`,
  `coordinates`), the GitHub repository topics (`astronomy`, `astropy`, `hacktoberfest`, `python`,
  `solar`, `solar-physics`, `sun`, `sunpy`), the PyHC core registry keyword list, and the DataCite
  subjects. Keywords are stored lower case; HSSI displays them title-cased, so `Astronomy`, `Fits`,
  `Wcs`, `Sunpy`, `Science` and `Hacktoberfest` in the rendered record are the same values as these.
- `coronagraph`, `magnetogram`, `solar imaging` and `coronal holes` are recorded here although the
  earlier record omitted them, and each reuses a keyword row that already exists rather than minting a
  near-duplicate — the keyword list is an open vocabulary, where an unknown value is created rather
  than rejected, so a near-miss spelling would silently add a second row. The evidence: `coronagraph` (LASCO, COR1/COR2, Metis, K-Cor, PUNCH and
  WISPR map sources), `magnetogram` (HMI, MDI and GONG magnetogram map sources), `solar imaging` (the
  whole `sunpy/map/sources/` tree), and `coronal holes`.
- `coronal holes` is a **keyword and not a phenomenon**: sunpy supports coronal-hole event queries
  (`sunpy/net/solarnet/solarnet.py` registers the target `("CH", "Coronal Hole")`, and
  `examples/plotting/overplot_hek_polygon.py` retrieves SPoCA coronal-hole boundaries from the HEK),
  but the `Phenomena` vocabulary has no `Coronal Holes` row. See Field 22.
- `hacktoberfest` and `science` carry little scientific signal but are genuine GitHub topics and
  `pyproject.toml` keywords respectively, and both are already stored; they are kept rather than
  removed for tidiness.

### 17. Data Sources (OPTIONAL)
- The Virtual Solar Observatory.
- CDAWeb
- Observatory/Mission-specific
- HTTP/HTTPS Directories
- FTP/FTPS Directories
- TAP
- S3/Cloud-aware
- **The trailing period in `The Virtual Solar Observatory.` is part of the vocabulary row name and
  must be written exactly as shown.** The 2026-06-10 file omitted it; the controlled-list lookup is an
  exact case-insensitive match after trimming, so the period-less form would fail submission.
- *The Virtual Solar Observatory.* — `sunpy/net/vso/`, the primary Fido client.
- *CDAWeb* — `sunpy/net/cdaweb/`.
- *Observatory/Mission-specific* — `sunpy/net/jsoc/` (SDO), `sunpy/net/soar/` (Solar Orbiter),
  `sunpy/net/solarnet/`, `sunpy/net/hek/`, `sunpy/net/helio/`, and the mission-specific
  `dataretriever` clients (GOES XRS and SUVI, EVE, LYRA, NoRH, RHESSI, GONG, ADAPT, NOAA, AIA synoptic).
- *HTTP/HTTPS Directories* — `sunpy/net/scraper.py` walks dated HTTP directory
  listings; every `dataretriever` client is defined by an HTTP URL `pattern`.
- *FTP/FTPS Directories* — the same scraper implements `_ftpfilelist`, opening
  anonymous FTP (`FTP(ftpurl, user="anonymous", passwd="data@sunpy.org")`) when a pattern's scheme is
  `ftp`; `parfive[ftp]` is a required dependency.
- *TAP* — the merged SOAR client issues ADQL against the IVOA TAP endpoint
  `http://soar.esac.esa.int/soar-sl-tap/tap` (`sunpy/net/soar/client.py`), sending
  `{"REQUEST": "doQuery", "LANG": "ADQL", ...}`.
- *S3/Cloud-aware* — `sunpy.map.Map` and `sunpy.timeseries.TimeSeries` open
  remote files through `fsspec` (`sunpy/io/_file_tools.py`, `map_factory.py`, `timeseries_factory.py`);
  `fsspec>=2024.9.0` is a required dependency and `pyproject.toml` ships an `s3` extra
  (`fsspec[s3]`, `aiobotocore`, `boto3`). `docs/whatsnew/6.1.rst` states "Support for S3 filesystems
  is tested".
- **Rejected:** `HAPI` — no HAPI client exists anywhere in `sunpy/`. `AMDA`, `GFZ`, `Madrigal`,
  `OMNIWeb`, `SSCWeb`, `VirES`, `WDC`, `das2` — no client for any of them. `Other` — every source
  sunpy actually reaches is already named by a specific row above, so it would add nothing.

### 18. Input File Formats (RECOMMENDED)
- FITS
- CDF
- ISTP-Compliant
- netCDF3/4
- HDF5
- JSON
- ascii
- Other
- Source: `sunpy/io/` readers — `_fits.py` (FITS), `_cdf.py` (CDF via cdflib), `_jp2.py` (JPEG2000 via
  glymur), `ana.py` (ANA), `special/asdf/` (ASDF), `special/genx.py` (SolarSoft GenX),
  `special/srs.py` (NOAA Solar Region Summary text). netCDF and HDF5 arrive through the
  `timeseries` extra's `h5netcdf` and `h5py` (GOES netCDF files); JSON through
  `sunpy/timeseries/sources/noaa.py`, which parses the SWPC `.json` solar-cycle index files with
  `pd.read_json`. `Other` covers JPEG2000, ANA, ASDF, GenX and SRS.
- *ISTP-Compliant* — `sunpy/io/_cdf.py:read_cdf` documents itself as reading
  "a CDF file that follows the ISTP/IACG guidelines", which is precisely what this row denotes.
- **Rejected:** `csv` — the closest candidate, `sunpy/timeseries/sources/eve.py`, calls
  `read_csv(..., sep=r'\s+')` on whitespace-delimited EVE level 0CS text, which `ascii` already
  covers. `IDL.sav` — sunpy reads SolarSoft GenX (XDR), not IDL save files; there is no `readsav` call
  in the package. `Zarr` — no support.

### 19. Output File Formats (RECOMMENDED)
- FITS
- Other
- Source: `sunpy/io/_file_tools.py:write_file` dispatches to exactly three writers — `_fits.write`,
  `_jp2.write` and `ana.write` — and its own signature documents `filetype : {'auto', 'fits', 'jp2'}`.
  Beyond those, `sunpy/io/special/asdf/converters/` supplies ASDF converters and schemas for
  `GenericMap` and the coordinate frames, so a Map can be serialized into an ASDF file. `Other`
  therefore covers JPEG2000, ANA and ASDF.
- **`CDF`, `JSON` and `ascii` were previously stored in HSSI and have been removed as incorrect.**
  They came from the 2026-06-10 extraction, which inferred the output formats from sunpy's *reader*
  set rather than from its writers. sunpy reads far more formats than it writes, so that inference
  was wrong in all three cases.
  - `CDF` — `sunpy/io/_cdf.py` has `__all__ = ['read_cdf']` and defines no writer. sunpy cannot
    produce a CDF file.
  - `JSON` — every `json.dump` in the package writes client machinery, not science: attribute caches
    for the VSO, JSOC, CDAWeb and SOLARNET clients (`sunpy/net/vso/vso.py`, `jsoc/jsoc.py`,
    `cdaweb/helpers.py`, `solarnet/solarnet.py`), the maintainer script that regenerates the SOAR
    attribute tables (`sunpy/net/soar/data/_update_attrs_data.py`), and vendored third-party code
    (`sunpy/extern/distro.py`). None of those is scientific output.
  - `ascii` — sunpy ships no ascii data writer. The only path to a text file is
    `QueryResponseTable` inheriting `astropy.table.Table.write`, which lets a user write *search
    results* to a text table. That is a generic astropy capability surfacing through a sunpy object,
    not a sunpy-authored writer, and it does not make ascii an output format of this package.
  Do not re-derive these three from the Field 18 reader list; the reader and writer sets are
  deliberately different.

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows
- Source: `.github/workflows/ci.yml` runs the test matrix on Linux, macOS and Windows, and the wheel
  job builds `manylinux`, `macosx` and `win_amd64` targets. `pyproject.toml` classifies the package
  `Operating System :: OS Independent`.
- The vocabulary also offers `Operating System Independent`, which matches the classifier literally.
  The three concrete platforms are kept instead: they are what the project actually builds and tests,
  and they are what a user filtering HSSI by platform expects to match.

### 21. CPU Architecture (RECOMMENDED)
- x86-64
- Apple Silicon arm64
- Linux aarch64 or arm64
- Source: the wheel targets in `.github/workflows/ci.yml` — `cp3{12,13,14}-manylinux*_x86_64`,
  `cp3{12,13,14}-macosx_x86_64`, `cp3{12,13,14}-macosx_arm64`, `cp3{12,13,14}-win_amd64`, and
  `cp3{12,13,14}-manylinux_aarch64` built on `runs-on: ubuntu-24.04-arm`.
- *Linux aarch64 or arm64* — the project publishes native aarch64 Linux wheels, which the earlier
  record did not reflect.

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections
- Solar Corona
- Solar Flares
- X-ray emission
- *Coronal Mass Ejections* — the coronagraph and heliospheric-imager map sources exist to observe
  them; `sunpy/map/sources/stereo.py` describes HI as "for the detection of coronal mass ejection
  (CME) events in interplanetary space".
- *Solar Corona* — the EUV coronal imagers and coronagraphs listed under Field 5.
- *Solar Flares* and *X-ray emission* — `sunpy/timeseries/sources/goes.py` (`XRSTimeSeries`, the
  standard flare-classification light curve), `rhessi.py` (`RHESSISummaryTimeSeries`), `fermi_gbm.py`,
  plus `hinode.py` XRT, `yohkoh.py` SXT and `asos.py` HXI on the imaging side.
- **`Coronal Holes` was removed from this file.** The 2026-06-10 extraction listed it, but the
  `Phenomena` vocabulary contains exactly seven rows — Coronal Heating, Coronal Mass Ejections,
  Geomagnetic Storms, Solar Corona, Solar Flares, Solar Wind, X-ray emission — and `Coronal Holes` is
  not among them, so the value could never have been submitted. HSSI's stored record never contained
  it. The underlying capability is real and is preserved as the Field 16 keyword `coronal holes`.
- **`Solar Wind` and `Coronal Heating` were assessed and rejected.** For `Solar Wind` the
  evidence is the same single SOAR instrument-name comment described under Field 5 — sunpy can
  download Solar Wind Analyser files but cannot read or analyse them. For `Coronal Heating` the string
  does not appear anywhere in `sunpy/`, `examples/` or `docs/`; sunpy images the corona but implements
  nothing about how it is heated. `Geomagnetic Storms` likewise has no support in the package.

### 23. Development Status (RECOMMENDED)
- **Status:** Active
- Source: the repostatus.org "Project Status: Active" badge in `README.rst`; a v8.0.0 release on
  2026-06-30; commits through 2026-08-13 on `main` (the pinned revision is that day's cruft-update
  merge); all six PyHC core quality ratings "Good"; `pyproject.toml` classifier
  `Development Status :: 5 - Production/Stable`; GitHub reports the repository as not archived.

### 24. Documentation (RECOMMENDED)
- **URL:** https://docs.sunpy.org
- Source: `pyproject.toml` `[project.urls] Documentation`, the README documentation badge, and the
  PyHC registry `docs:` field. Resolves. PyHC records the `http://` form; the `https://`
  form stored here is the canonical one and is kept.

### 25. Funder (OPTIONAL)
- **Organization:** NumFOCUS | **Funder Identifier:** https://ror.org/004eyxv41
- **Organization:** National Aeronautics and Space Administration | **Funder Identifier:** https://ror.org/027ka1x80
- **Organization:** Google | **Funder Identifier:** https://ror.org/00njsd438
- **Organization:** European Space Agency | **Funder Identifier:** https://ror.org/03wd9za21
- Source: the Acknowledgments of the two SunPy Project papers, which are the authoritative record of
  what has funded this software.
  - 2020 ApJ 890:68 — "We acknowledge financial contributions from Google as part of the Google
    Summer of Code program and from the European Space Agency as part of the Summer of Code in Space
    program. We acknowledge financial contributions from NumFocus for improving the usability of
    SunPy's Data Downloader."
  - 2023 Frontiers 10:1076726, Funding — "WB, AS, and SM are supported by an award from the NASA
    Research Opportunities in Space and Earth Sciences (ROSES) Open-Source Tools, Frameworks, and
    Libraries (OSTFL) program." OSTFL exists specifically to fund open-source scientific software, and
    the three named recipients are sunpy maintainers, so this is development funding for sunpy itself.
  - NumFOCUS is additionally sunpy's fiscal sponsor, shown by the "Powered by NumFOCUS" badge in
    `README.rst` and stated in the 2023 paper: "The SunPy Project is sponsored by NumFOCUS".
  - Google's ROR display name is "Google (United States)"; the plain name used in the acknowledgment
    is recorded here with that ROR.
- **Rejected, with the reason, so Crossref does not reintroduce them.** Crossref's funding block for
  the 2020 paper lists NSF award AST-1715122 and STFC awards ST/N504336/1 and ST/N000692/1. The
  paper's own text separates the tiers explicitly: "The following individuals recognize support for
  their **personal** contributions. B.M.S. is supported by the NSF grant AST-1715122 ... D.S. was
  supported by STFC studentship ST/N504336/1 and STFC grant ST/N000692/1." NSF AST-1715122 is in fact
  "AstroML: Machine Learning for Astrophysics" (PI Andrew Connolly, University of Washington) — an
  unrelated project that funded a contributor's post. None of the three funded sunpy.
  The same paper's Gaia/DPAC funding paragraph concerns data used in a figure, not the software.
  The 2023 paper's NASA contracts NNG09FA40C (IRIS) and NNG04EA00C (SDO/AIA) and the ESA Research
  Fellowship are likewise personal support for individual authors through mission contracts.
- **Considered and not selected — the American Astronomical Society.** Both papers acknowledge "funding
  from the Solar Physics Division of the American Astronomical Society for SunPy workshops and
  tutorials at annual meetings." That is real money to the SunPy Project, but it funds outreach events
  rather than the software resource this record describes, so it is not recorded as a funder. The
  evidence is kept here so a later refresh applies the same reasoning instead of rediscovering the
  acknowledgment and reading it as a missing funder.
- Where the acknowledgments can be read, and what that rules out: the 2020 paper's acknowledgments come
  from the CC-BY author copy in Virginia Tech's VTechWorks repository — the publisher's own page and
  PDF sit behind a Radware bot challenge that a plain fetch cannot pass, and the article is not in
  Europe PMC, so a later refresh should go straight to the author copy. The
  findings were independently confirmed with ADS acknowledgement-field probes against bibcode
  2020ApJ...890...68S, which return hits for "Google Summer of Code", "Summer of Code in Space",
  "European Space Agency", "AST-1715122", "ST/N000692/1" and "ST/N504336/1", and no hit for
  "NumFOCUS" or "NASA" (NumFOCUS entered the acknowledgments as "NumFocus"; the same probe returns
  many hits across other ADS records, and a nonsense token returns none, so the absence is real
  rather than a tokenization artifact).

### 26. Award Title (OPTIONAL)
- **Award Title:** Improving the Usability of sunpy's Data Downloader
- **Award Number:** Not found
- Source: the 2023 Frontiers acknowledgments, which give the title in quotation marks — "We
  acknowledge financial contributions from NumFOCUS for 'Improving the Usability of sunpy's Data
  Downloader'". The 2020 paper describes the same grant in running prose ("from NumFocus for improving
  the usability of SunPy's Data Downloader"); the 2023 quoted form is used because it is the award's
  actual title. Neither paper gives an award number for it.
- The NASA ROSES OSTFL award (Field 25) is deliberately **not** given an entry here. Neither paper
  states its title or number, and inventing one from the program name would be fabrication. If a
  future refresh finds the award identifier, this is the field for it.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1088/1749-4699/8/1/014009 — "SunPy—Python for solar physics" (2015), the first
  paper describing sunpy, at v0.5.
- https://doi.org/10.21105/joss.01832 — JOSS review of sunpy v1.0.8 (Mumford et al. 2020).
- https://doi.org/10.3389/fspas.2023.1076726 — "The SunPy Project: An interoperable ecosystem for
  solar data analysis" (The SunPy Community 2023, Frontiers in Astronomy and Space Sciences).
- Source: the "Other SunPy publications" section of `CITATION.rst`, which lists exactly these three
  alongside the reference publication. At the pinned revision the list is exactly these three, and
  all three DOIs resolve.

### 28. Related Datasets (OPTIONAL)
Not found
- Negative research so this is not re-investigated: sunpy ships a sample-data set, but
  `sunpy/data/_sample.py` fetches it from plain file stores (`https://github.com/sunpy/data/raw/main/sunpy/v1/`
  and `http://data.sunpy.org/sunpy/v1/`) with no DOI. The datasets sunpy operates on belong to the
  missions and archives in Fields 17, 31 and 32, not to sunpy, and the 2023 paper's Data Availability
  Statement points at the VSO, SOAR and JSOC services rather than at citable datasets.

### 29. Related Software (OPTIONAL)
- https://github.com/astropy/astropy — astropy. sunpy is built directly on it: `GenericMap` wraps
  `astropy.wcs.WCS` and `astropy.units`, and `sunpy.coordinates` registers its frames into astropy's
  transformation graph. A domain-specific dependency that genuinely characterizes the package.
- https://github.com/sunpy/ndcube — ndcube. The SunPy Project's N-dimensional data-cube package;
  sunpy's gallery builds `NDCube` objects from sunpy-loaded Solar Orbiter SPICE data
  (`examples/showcase/spice_parallel_fitting.py`, `examples/units_and_coordinates/solo_fov.py`) and
  `pyproject.toml` carries `ndcube>=2.3.0` in the `docs-gallery` extra for exactly that purpose.
- https://github.com/sunpy/sunkit-image — sunkit-image. The affiliated package
  that took over image analysis from sunpy core: `sunpy.image.coalignment` and
  `sunpy.physics.solar_rotation` were moved to `sunkit_image.coalignment` (`docs/whatsnew/4.0.rst`),
  and `docs/tutorial/maps.rst` directs users there for coalignment and rotation compensation.
- https://github.com/LM-SAL/aiapy — aiapy. Took over SDO/AIA preparation from
  sunpy: `docs/whatsnew/2.0.rst` records `sunpy.instr.aia.aiaprep` being removed in favour of aiapy's
  `register()`, and `docs/conf.py` carries an intersphinx mapping to it.
- https://github.com/sunpy/radiospectra — radiospectra. The successor to the
  removed `sunpy.spectra` module (`docs/whatsnew/1.0.rst`), and the reason sunpy itself has no
  spectrogram functionality (see Field 4).
- **`https://github.com/sunpy/sunpy-sphinx-theme` was previously stored in HSSI and has been removed.**
  It is a Sphinx HTML theme, and it appears in the repository only in `pyproject.toml`'s `docs` extra
  alongside `sphinx`, `sphinx-gallery` and the other documentation-build packages. Applying the
  relevance test decides it: a documentation theme would be equally at home in a web application, a
  finance model or a biology pipeline; it performs no task similar to sunpy's; and its entry would
  read the same for any project that publishes Sphinx docs, so it tells a reader nothing about this
  software. Sharing the `sunpy/` GitHub organization is branding, not a scientific relationship. It
  fails the Field 29 gate on the merits and should not be re-proposed.
- **Also rejected:** numpy, scipy, pandas, matplotlib, requests, tqdm,
  python-dateutil, packaging, setuptools, beautifulsoup4, lxml, fsspec, parfive, zeep, glymur,
  contourpy, mpl-animators — generic scientific-Python and packaging infrastructure whose presence is
  true of most of the ecosystem. `sunpy-soar` is also **not** listed: as of 8.0.0 it is no longer a
  separate package at all, having been merged into `sunpy/net/soar/`.

### 30. Interoperable Software (OPTIONAL)
- https://github.com/astropy/astropy — astropy. The exchange is concrete and bidirectional:
  `sunpy/coordinates/frames.py` registers every solar frame in astropy's coordinate transformation
  graph, so a single `SkyCoord` converts between astropy frames (ICRS, HCRS, ITRS) and sunpy frames;
  `GenericMap` consumes and produces `astropy.wcs.WCS` and `astropy.units.Quantity`; and 8.0.0 added
  saving and loading of `astropy.table.QTable` objects containing `SkyCoord`s in sunpy frames to FITS.
- https://github.com/sunpy/drms — drms. `sunpy/net/jsoc/jsoc.py` is built on `drms.Client`, and the
  7.1 release passes `sleep`, `timeout` and `retries_notfound` from `JSOCClient.fetch` straight
  through to `drms.ExportRequest.wait`. `drms>=0.8.0` is required by the `net` extra.
  **This corrects an earlier wrong URL.** The record previously carried
  `https://github.com/JSOC-SDP/drms`, a different, little-used C repository holding JSOC's own
  server-side DRMS code. The Python `drms` package sunpy depends on is published from
  `https://github.com/sunpy/drms` — PyPI's `drms` project gives exactly that as its "Source Code"
  URL, and its documentation lives under `docs.sunpy.org/projects/drms`. The old URL is
  plausible-looking but wrong; do not restore it.
- https://github.com/sunpy/ndcube — ndcube. Data loaded and read through sunpy is handed to `NDCube`
  in the gallery examples cited under Field 29, and the two packages share the `mpl-animators`
  animation machinery (`CHANGELOG.rst` records the animator being factored out because ndcube relies
  on it too).
- https://github.com/AndrewAnnex/SpiceyPy — SpiceyPy. `sunpy/coordinates/spice.py`
  is a documented bridge to the NAIF SPICE toolkit: it wraps `spiceypy` so SPICE computations are
  reachable through the `SkyCoord` API, creates a frame class per SPICE frame in the loaded kernels,
  and gives every SPICE-based coordinate a `to_helioprojective()` method for conversion back into
  sunpy's own frames. `spiceypy>=7.0.0` is the `spice` extra.
- https://github.com/sunpy/sunkit-image — sunkit-image. It consumes and returns
  `sunpy.map.GenericMap` objects; sunpy's own tutorial sends users to `sunkit_image.coalignment` for
  work sunpy no longer does, which is a shared data model in active use.
- https://github.com/LM-SAL/aiapy — aiapy. `aiapy.calibrate.register()` takes a
  sunpy `AIAMap` and returns a prepped `AIAMap`; sunpy's release notes designate it as the
  replacement for the removed in-tree AIA preparation.
- **Rejected — being a dependency is not interoperability.** numpy, scipy, pandas, matplotlib and the
  rest of the generic stack are excluded outright. `cdflib`, `h5py`, `h5netcdf`, `asdf`,
  `asdf-astropy`, `glymur` and `reproject` are used internally as format and algorithm plumbing with
  no exposed exchange of a shared data model, so they belong in Fields 18/19 or nowhere.
  `sunpy-soar` is not an interoperable package any more — 8.0.0 merged it into sunpy. Blanket claims
  such as "part of the scientific Python ecosystem" or "a PyHC package, so it interoperates with PyHC
  packages" carry no information and are not used here.


### 31. Related Instruments (OPTIONAL)

**This field corrects a wrong conclusion in the 2026-06-10 file, which recorded "Not found — SunPy
supports many instruments via its map and timeseries sources but does not target specific instrument
identifiers." That is false. `sunpy/map/sources/` and `sunpy/timeseries/sources/` contain
instrument-specific subclasses whose `is_datasource_for` methods dispatch on instrument and detector
FITS keywords, `sunpy/net/dataretriever/sources/` contains instrument-specific search clients, and
`sunpy/visualization/colormaps/cm.py` registers instrument-specific colour tables. Under the
designed-to-support test an instrument-specific parser or client qualifies, and 47 instruments
resolve.**

Every entry below carries the SPASE row's `name` copied verbatim together with its identifier; the
identifier is the de-duplication key. Grouped by platform, with the code evidence for the group.
**Solar Dynamics Observatory — `sunpy/map/sources/sdo.py` (`AIAMap`, `HMIMap`, `HMISynopticMap`), `sunpy/timeseries/sources/eve.py` (`ESPTimeSeries`, `EVESpWxTimeSeries`), the `sunpy/net/jsoc/` client and `sunpy/net/dataretriever/sources/aia_synopsis.py` and `eve.py`. ESP is a channel of EVE and has no separate SPASE row, so it resolves to the EVE instrument.**
- **Atmospheric Imaging Assembly** — SPASE: https://spase-metadata.org/SMWG/Instrument/SDO/AIA
- **HMI** — SPASE: https://spase-metadata.org/SMWG/Instrument/SDO/HMI
- **EVE** — SPASE: https://spase-metadata.org/SMWG/Instrument/SDO/EVE

**Solar and Heliospheric Observatory — `sunpy/map/sources/soho.py` defines `EITMap`, `EITL1Map`, `LASCOMap`, `MDIMap` and `MDISynopticMap`.**
- **Extreme Ultraviolet Imaging Telescope** — SPASE: https://spase-metadata.org/SMWG/Instrument/SOHO/EIT
- **Large Angle Spectroscopic Coronagraph** — SPASE: https://spase-metadata.org/SMWG/Instrument/SOHO/LASCO
- **Michelson Doppler Imager** — SPASE: https://spase-metadata.org/SMWG/Instrument/SOHO/MDI

**STEREO SECCHI, both spacecraft — `sunpy/map/sources/stereo.py` defines `EUVIMap`, `CORMap` (COR1 and COR2, dispatching on `header['detector'].startswith('COR')`) and `HIMap` (HI-1 and HI-2). All three set their nickname from `self.observatory[-1]`, i.e. the A/B suffix, which is the in-repo evidence that both spacecraft are supported. The two suite-level SECCHI rows are included because SECCHI is what the FITS `INSTRUME` keyword names; the telescope rows are included because sunpy implements a distinct Map subclass per telescope.**
- **Stereo-A Sun Earth Connection Coronal and Heliospheric Investigation** — SPASE: https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI
- **Stereo-B Sun Earth Connection Coronal and Heliospheric Investigation** — SPASE: https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI
- **Extreme UltraViolet Imager on the STEREO-A mission** — SPASE: https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/EUVI
- **Extreme UltraViolet Imager on the STEREO-B mission** — SPASE: https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/EUVI
- **STEREO-A SECCHI Cor1 Coronagraph** — SPASE: https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/Cor1
- **STEREO-B SECCHI Cor1 Coronagraph** — SPASE: https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/Cor1
- **STEREO-A SECCHI Cor2 Coronagraph** — SPASE: https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI/Cor2
- **STEREO-B SECCHI Cor2 Coronagraph** — SPASE: https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI/Cor2
- **Heliospheric Imager-1 Telescope on the STEREO-A mission** — SPASE: https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/HI-1
- **Heliospheric Imager-1 Telescope on the STEREO-B mission** — SPASE: https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/HI-1
- **Heliospheric Imager-2 Telescope on the STEREO-A mission** — SPASE: https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/HI-2
- **Heliospheric Imager-2 Telescope on the STEREO-B mission** — SPASE: https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/HI-2

**GOES SUVI — `sunpy/map/sources/suvi.py` (`SUVIMap`) plus the `SUVIClient` in `sunpy/net/dataretriever/sources/goes.py`, whose supported-satellite list is `goes_number = [16, 17, 18]`. Four SUVI rows exist in the vocabulary; the three the client names are recorded and GOES-19 is deliberately excluded. If the client later adds 19, `https://spase-metadata.org/NOAA/Instrument/GOES/19/SUVI` becomes the correct fourth entry.**
- **Solar Ultraviolet Imager** — SPASE: https://spase-metadata.org/NOAA/Instrument/GOES/16/SUVI
- **Solar Ultraviolet Imager** — SPASE: https://spase-metadata.org/NOAA/Instrument/GOES/17/SUVI
- **Solar Ultraviolet Imager** — SPASE: https://spase-metadata.org/NOAA/Instrument/GOES/18/SUVI

**GOES XRS — `sunpy/timeseries/sources/goes.py` (`XRSTimeSeries`) and the `XRSClient`, whose supported list is `goes_number = [2, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18]`. The vocabulary contains XRS instrument rows for only four of those satellites, and all four are recorded. GOES 2, 6–12 and 16–18 have no XRS instrument row; their association is carried by the GOES observatory row in Field 32. The three GOES 13/14/15 rows share the name `Solar X-ray Sensor on GOES` and are distinguished only by identifier.**
- **Solar X-ray Monitor on GOES 5** — SPASE: https://spase-metadata.org/SMWG/Instrument/GOES/5/XRS
- **Solar X-ray Sensor on GOES** — SPASE: https://spase-metadata.org/SMWG/Instrument/GOES/13/XRS
- **Solar X-ray Sensor on GOES** — SPASE: https://spase-metadata.org/SMWG/Instrument/GOES/14/XRS
- **Solar X-ray Sensor on GOES** — SPASE: https://spase-metadata.org/SMWG/Instrument/GOES/15/XRS

**Hinode — `sunpy/map/sources/hinode.py` defines `XRTMap` and `SOTMap`. XRT formerly had both a bare and a `.html` identifier; the bare row was already the one recorded here, and the `.html` twin has since been retired in the vocabulary consolidation.**
- **X-Ray Telescope** — SPASE: https://spase-metadata.org/SMWG/Instrument/Hinode/XRT
- **Solar Optical Telescope** — SPASE: https://spase-metadata.org/SMWG/Instrument/Hinode/SOT

**IRIS — `sunpy/map/sources/iris.py` (`SJIMap`) reads slit-jaw imagery, and `sunpy/visualization/colormaps/cm.py` registers nine `irissji*` colour tables. The slit-jaw imager has no separate SPASE row; the single IRIS instrument row is the correct target.**
- **Interface Region Imaging Spectrograph** — SPASE: https://spase-metadata.org/SMWG/Instrument/IRIS/IRIS

**Parker Solar Probe — `sunpy/map/sources/psp.py` (`WISPRMap`). The suite-level WISPR row is used; the two sub-telescope rows (`.../WISPR/InnerTelescope`, `.../WISPR/OuterTelescope`) are deliberately not expanded, since sunpy has one Map class for WISPR rather than one per telescope.**
- **PSP WISPR** — SPASE: https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/WISPR

**Solar Orbiter — `sunpy/map/sources/solo.py` defines `EUIMap`, `PHIMap` (new in 8.0.0) and `METISMap` (new in 8.0.0). In addition, 8.0.0 merged `sunpy-soar` into `sunpy/net/soar/`, so `Fido` now searches and downloads the whole Solar Orbiter instrument set out of the box; `sunpy/net/soar/data/instrument_attrs.json` enumerates it as EPD, EUI, MAG, METIS, PHI, RPW, SOLOHI, SPICE, STIX, SWA. Every one of those with a SPASE row is recorded. Support for STIX, SPICE, SoloHI and EPD is search-and-download through the mission's own archive, which the relevance test counts as designed-to-support; reading those products is left to other packages.**
- **Extreme Ultraviolet Imager** — SPASE: https://spase-metadata.org/ESA/Instrument/SolarOrbiter/EUI
- **Polarimetric and Helioseismic Imager** — SPASE: https://spase-metadata.org/ESA/Instrument/SolarOrbiter/PHI
- **Metis** — SPASE: https://spase-metadata.org/ESA/Instrument/SolarOrbiter/Metis
- **Spectral Imaging of the Coronal Environment** — SPASE: https://spase-metadata.org/SMWG/Instrument/SolarOrbiter/SPICE
- **STIX** — SPASE: https://spase-metadata.org/ESA/Instrument/SolarOrbiter/STIX
- **The Solar Orbiter Heliospheric Imager** — SPASE: https://spase-metadata.org/NASA/Instrument/SolarOrbiter/SoloHI
- **Energetic Particle Detector** — SPASE: https://spase-metadata.org/ESA/Instrument/SolarOrbiter/EPD

**PROBA2 — `sunpy/map/sources/proba2.py` (`SWAPMap`) for SWAP imagery, and `sunpy/timeseries/sources/lyra.py` (`LYRATimeSeries`) plus the `LYRAClient` in `sunpy/net/dataretriever/sources/lyra.py` for LYRA radiometry. Exactly one row carries the `.../PROBA2/SWAP` identifier. The LYRA entry's display name is addressed in the caveat below the list.**
- **Proba 2 Sun Watcher using APS detectors and Image Processing** — SPASE: https://spase-metadata.org/SMWG/Instrument/PROBA2/SWAP
- **Sun Watcher using APS detectors and image Processing** — SPASE: https://spase-metadata.org/SMWG/Instrument/PROBA2/LYRA

**TRACE — `sunpy/map/sources/trace.py` (`TRACEMap`) and eight `trace*` colour tables. The mission has one imaging-telescope instrument row.**
- **TRACE Imaging Telescope on TRACE** — SPASE: https://spase-metadata.org/SMWG/Instrument/TRACE/Telescope

**Yohkoh SXT — `sunpy/map/sources/yohkoh.py` (`SXTMap`) plus the `yohkohsxtal` and `yohkohsxtwh` colour tables.**
- **Soft X-Ray Telescope on Yohkoh** — SPASE: https://spase-metadata.org/SMWG/Instrument/Yohkoh/SXT

**RHESSI — `sunpy/map/sources/rhessi.py` (`RHESSIMap`), `sunpy/timeseries/sources/rhessi.py` (`RHESSISummaryTimeSeries`) and the `RHESSIClient`. The vocabulary names the instrument by its pre-launch designation, HESSI.**
- **High-Energy Solar Spectroscopic Imager** — SPASE: https://spase-metadata.org/SMWG/Instrument/RHESSI/HESSI

**Fermi GBM — `sunpy/timeseries/sources/fermi_gbm.py` (`GBMSummaryTimeSeries`) and the `GBMClient`. The bare row was preferred over a since-retired `.html` duplicate.**
- **Fermi Gamma-ray Burst Monitor** — SPASE: https://spase-metadata.org/SMWG/Instrument/FERMI/GBM

**MLSO K-Cor — `sunpy/map/sources/mlso.py` (`KCorMap`) and the `kcor` colour table.**
- **MLSO K-Coronagraph** — SPASE: https://spase-metadata.org/NSF/Instrument/Ground/MLSO/K-Cor

**PUNCH — `sunpy/map/sources/punch.py` (`PUNCHMap`) and the `punch` colour table. The class docstring names the constellation's instrument complement exactly: "three Wide Field Imagers (WFIs) and one Near Field Imager (NFI)", which is the in-repo evidence selecting these four rows. The three WFI rows share the name `Wide Field Imager` and differ by identifier; the NFI bare row was preferred over a since-retired `.html` duplicate.**
- **Narrow Field Imager** — SPASE: https://spase-metadata.org/NASA/Instrument/PUNCH/NFI
- **Wide Field Imager** — SPASE: https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/1
- **Wide Field Imager** — SPASE: https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/2
- **Wide Field Imager** — SPASE: https://spase-metadata.org/NASA/Instrument/PUNCH/WFI/3

**A caveat on the LYRA entry's display name — recorded so it is not "corrected".**
The row at `https://spase-metadata.org/SMWG/Instrument/PROBA2/LYRA` stores the display name `Sun
Watcher using APS detectors and image Processing`, which is the expansion of SWAP — a different
PROBA2 instrument, with its own row at `.../PROBA2/SWAP` — apparently misassigned in the upstream
registry's LYRA record; the identifier is correct and is the durable half of the entry, so a future
refresh should neither change the identifier nor read the mismatched name as evidence that the wrong
instrument was recorded, and a local rename would be transient against the upstream registry.

**Omitted, with reasons — these are correct outcomes, not gaps.**
- *Aditya-L1 / SUIT* — `sunpy/map/sources/suit.py` (`SUITMap`) and eleven `suit_*` colour tables give
  real support, but the vocabulary contains no row matching "Aditya" and no SUIT instrument row (the
  only "SUIT" hits are unrelated instrument-suite names such as MMS FIELDS and PSP WISPR). There is
  no observatory row to fall back to either, so the association cannot be recorded at all.
- *ASO-S / HXI* — `sunpy/map/sources/asos.py` (`HXIMap`, added in 7.1) supports the Hard X-ray Imager,
  but the vocabulary has no "ASO-S" row of either type.
- *Nobeyama Radioheliograph* — `sunpy/timeseries/sources/norh.py` (`NoRHTimeSeries`) and the
  `NoRHClient` support it, but "Nobeyama" returns zero rows of either type.
- *GONG at instrument level* — six per-station GONG instrument rows exist (Learmonth, CTIO, Teide,
  Mauna Loa, Big Bear, Udaipur), but nothing in the repository selects among them: the `GONGClient`
  registers a single instrument value `("GONG", "Global Oscillation Network Group.")` and fetches
  network-level synoptic products from `gong2.nso.edu`. Per the resolution ladder this becomes an
  observatory-level association instead, recorded in Field 32.
- *ADAPT* — `sunpy/map/sources/adapt.py` and the `ADAPTClient` support ADAPT maps, but ADAPT is the
  Air Force Data Assimilative Photospheric flux transport **model**, not an instrument or observatory.
  Its GONG input is already represented through the GONG observatory row.
- *NOAA solar-cycle indices and Solar Region Summary* — `sunpy/timeseries/sources/noaa.py` and
  `sunpy/net/dataretriever/sources/noaa.py` (`SRSClient`) read SWPC data products, not instrument
  data. They belong to Field 17, not here.
- *Solar Orbiter MAG, RPW and SWA* — the merged SOAR client can query all three, but the vocabulary
  has no Solar Orbiter row for any of them (the only "Solar Wind Analyzer" row belongs to Interball-1,
  and the "Radio and Plasma Wave" rows belong to Cassini and Ulysses). The Solar Orbiter observatory
  row covers them.
- *Instruments reachable only through generic archives* — the VSO, CDAWeb, HEK, HELIO and SOLARNET
  clients expose many instruments sunpy does not itself parse. Those are multi-mission data services
  and are recorded in Field 17; listing their catalogues here would make the field meaningless.


### 32. Related Observatories (OPTIONAL)

The 2026-06-10 file listed its observatories as bare names with **no identifiers**, which cannot be
recorded: a bare name either binds to an arbitrary same-name row or creates a new identifierless row.
Each of the eighteen entries below is resolved to a SPASE row, with the row's `name` copied verbatim.
The observatory associations rest on the map, timeseries and client evidence set out in Field 31; the
notes after the list cover the entries whose resolution required a choice.
- **Solar Dynamics Observatory** — SPASE: https://spase-metadata.org/SMWG/Observatory/SDO
- **Solar and Heliospheric Observatory** — SPASE: https://spase-metadata.org/SMWG/Observatory/SOHO
- **Solar-Terrestrial Relations Observatory** — SPASE: https://spase-metadata.org/SMWG/Observatory/STEREO
- **Geostationary Operational Environmental Satellites** — SPASE: https://spase-metadata.org/SMWG/Observatory/GOES
- **Hinode** — SPASE: https://spase-metadata.org/SMWG/Observatory/Hinode
- **Parker Solar Probe** — SPASE: https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe
- **Solar Orbiter** — SPASE: https://spase-metadata.org/ESA/Observatory/SolarOrbiter
- **PROBA 2** — SPASE: https://spase-metadata.org/SMWG/Observatory/PROBA2
- **PUNCH Mission** — SPASE: https://spase-metadata.org/NASA/Observatory/PUNCH
- **Reuven Ramaty High Energy Solar Spectroscope Imager** — SPASE: https://spase-metadata.org/SMWG/Observatory/RHESSI
- **Fermi Gamma-ray Space Telescope** — SPASE: https://spase-metadata.org/SMWG/Observatory/FERMI
- **Solar Terrestrial Relations Observatory A** — SPASE: https://spase-metadata.org/SMWG/Observatory/STEREO-A
- **Solar Terrestrial Relations Observatory B** — SPASE: https://spase-metadata.org/SMWG/Observatory/STEREO-B
- **Interface Region Imaging Spectrograph** — SPASE: https://spase-metadata.org/SMWG/Observatory/IRIS
- **Transition Region and Coronal Explorer** — SPASE: https://spase-metadata.org/SMWG/Observatory/TRACE
- **1991-062A** — SPASE: https://spase-metadata.org/SMWG/Observatory/Yohkoh
- **Global Oscillation Network Group** — SPASE: https://spase-metadata.org/SMWG/Observatory/GONG
- **Mauna Loa Solar Observatory** — SPASE: https://spase-metadata.org/SMWG/Observatory/Ground/MaunaLoaSO
**Evidence for individual entries.**
- *Solar Terrestrial Relations Observatory A* and *B* — `sunpy/map/sources/stereo.py` derives each
  map's nickname from `self.observatory[-1]`, the A/B suffix, and the vocabulary has a distinct
  observatory row per spacecraft. The mission-level row is kept alongside them.
- *Interface Region Imaging Spectrograph* — `sunpy/map/sources/iris.py` (`SJIMap`) and nine
  `irissji*` colour tables.
- *Transition Region and Coronal Explorer* — `sunpy/map/sources/trace.py` (`TRACEMap`).
- *Yohkoh* — `sunpy/map/sources/yohkoh.py` (`SXTMap`). **The name `1991-062A` is correct and
  deliberate.** `https://spase-metadata.org/SMWG/Observatory/Yohkoh` is the only Yohkoh observatory
  row in the vocabulary, and its name is the mission's COSPAR designation rather than "Yohkoh", so
  the entry will display in HSSI as `1991-062A`. The identifier is unambiguously right and the rules
  require the row name verbatim, so the string is not edited. Dropping the entry was considered —
  Field 31's `Soft X-Ray Telescope on Yohkoh` already carries the association, and omitting it would
  avoid surfacing an opaque designation — but it is kept for mission-level completeness, so that
  Yohkoh is represented at observatory level alongside every other mission sunpy supports. Do not
  substitute a friendlier name: a free-typed "Yohkoh" would create a new identifierless row.
- *Global Oscillation Network Group* — `sunpy/map/sources/gong.py` (`GONGSynopticMap`,
  `GONGHalphaMap`, `GONGMagnetogramMap`) and the `GONGClient`. This is the observatory-level
  substitution explained under Field 31.
- *Mauna Loa Solar Observatory* — `sunpy/map/sources/mlso.py` (`KCorMap`). Two rows carry this name;
  `SMWG/Observatory/Ground/MaunaLoaSO` is chosen over `NSF/Observatory/Ground/MLSO` by the SMWG
  tie-breaker for same-name duplicates.

**Settled choices, recorded so they are not revisited.**
- *PUNCH, RHESSI and Fermi carry the upstream registry's identifiers* —
  `NASA/Observatory/PUNCH` "PUNCH Mission", `SMWG/Observatory/RHESSI` "Reuven Ramaty High Energy
  Solar Spectroscope Imager" and `SMWG/Observatory/FERMI` "Fermi Gamma-ray Space Telescope", each
  name copied verbatim from its row. Earlier versions of this file recorded `.html` variants of
  these three identifiers; those were submission-path artifacts rather than upstream resources, so
  the identifiers above are the correct values and reverting them is not an open question.
- *Per-satellite GOES observatory rows are not enumerated.* The umbrella
  `SMWG/Observatory/GOES` is kept. Rows exist for GOES 1–19, but GOES 5–12 are named by COSPAR
  designation (`1981-049A`, `1983-041A`, `1987-022A`, `1994-022A`, `1995-025A`, `1997-019A`,
  `2000-022A`, `2001-031A`) and `SMWG/Observatory/GOES/4` duplicates the umbrella name, so listing
  them would add fifteen mostly unreadable entries. The per-satellite specificity sunpy actually
  implements is already carried by the XRS and SUVI instrument rows in Field 31.
- *Aditya-L1, ASO-S and Nobeyama Radioheliograph are omitted here too* — no vocabulary rows exist, as
  detailed under Field 31.

### 33. Logo (OPTIONAL)
- **URL:** https://raw.githubusercontent.com/sunpy/sunpy-logo/4fc0161e25ab07e64ecdb1f4d0360538a91484e5/generated/sunpy_icon.png
- Source: the PyHC core registry `logo:` field designates this asset. Verified to serve `image/png`.
- The registry's own `logo:` string references the default branch; the value here pins the commit
  above instead, so no upstream rename, move or deletion can silently break it. The asset is
  independently locatable without the registry: it is `generated/sunpy_icon.png` in the project's own
  `sunpy/sunpy-logo` repository, which is the fallback source of record should the registry entry ever
  change or disappear.
- `README.rst` embeds a different asset from the same repository,
  `.../generated/sunpy_logo_landscape.png`. The square icon stored here is the better fit for a
  catalogue listing and matches what PyHC publishes, so it is kept.
