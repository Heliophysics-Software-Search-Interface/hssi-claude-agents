# HSSI Metadata Extraction Results

**HSSI Software ID:** ecd7fb7a-570b-4466-b0ea-8d4b60016036
**Repository:** https://github.com/NCAR/stokespy
**Source Revision:** 830d14398eceaee1c8bae70f11a6183d5a9054cb
**Extraction Date:** 2026-08-12
**Validation Date:** 2026-08-21
**Validation Status:** PASS

---

## Scope note

`stokespy` is a small, dormant package: 3 Python modules (1,548 lines), 1 trivial test, 6 documentation
pages, one release (0.5.0), and no commits after 2022-03-24. Because the repository is this thin, several
fields are settled by evidence that lives *outside* it — the NASA proposal that funded the work, Ricky
Egeland's own curriculum vitae, the authors' ORCID and publication records, and the CSAC dataset DOIs at
NCAR/HAO. Those external sources are cited inline.

**Egeland's CV — what it is, and its durable access caveat.** Several fields below rest on
`https://rickyegeland.github.io/cv/Ricky_Egeland_CV.pdf` (10 pages). Two things a future agent needs to know
about it. First, **use the `rickyegeland.github.io` form of the URL.** The CV is linked around the web as
`http://rickyegeland.com/cv/Ricky_Egeland_CV.pdf`, but that hostname serves a TLS certificate valid only for
`*.github.com`/`github.com`, so an HTTPS fetch of the `rickyegeland.com` form fails certificate validation
outright (`SSL: no alternative certificate subject name matches target host name 'rickyegeland.com'`). The
`github.io` form returns the PDF normally. Second, **it is a ~2020-era document**: its newest entries are
from mid-2020 (a June 2020 press item, a May 2020 presentation, and mentoring recorded as "summer 2020"), so
it cannot speak to anything later — not to the 0.5.0 release, not to the repository's
creation, and not to Egeland's later move to NASA Johnson Space Center. Its Software Projects section does
not list StokesPy, which is consistent with that dating rather than evidence against his involvement. It is
also **Egeland's CV alone** and carries no information about Gabriel Dima.

Two consequences of the package's small size are worth carrying forward: the repository contains no funding,
acknowledgement, citation, or DOI statement of any kind, and the code base is small enough that a claim of
"the software does not do X" can be, and here has been, checked exhaustively against every module.

A second caveat that changes how the evidence should be read: the README, `setup.cfg`, `.sunpy-template.yml`,
and the PyPI summary all describe stokespy as a "(future) SunPy affiliated package." That affiliation never
completed (see Field 8). Aspirational statements in this repository — SunPy affiliation, DKIST support,
stratified-atmosphere classes, general applicability to arbitrary spectropolarimeters — must not be read as
implemented capability. Where they were considered and rejected, the reason is recorded.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The person named here is the metadata submitter, not an author of the software; it is intentionally not
derived from the repository.

---

### 2. Persistent Identifier (RECOMMENDED)
Not found.

`stokespy` has no DOI of any kind. Negative research, so a later refresh need not repeat it:

- No `CITATION.cff`, `codemeta.json`, `.zenodo.json`, or `CITATION` file exists in the repository at any
  revision, and the README carries no DOI badge — its single badge is the "Powered by SunPy" shield
  (`README.rst` lines 4–6).
- Zenodo has no record matching `stokespy` (search over the Zenodo records API returns zero hits), and the
  repository has no Zenodo–GitHub integration: GitHub reports zero published Releases, which is the trigger
  Zenodo's integration depends on.
- DataCite has no DOI whose metadata matches `stokespy` (full-text DOI query returns zero results).

Because there is no concept DOI, none of the DOI-driven autofill sources (DataCite, Zenodo) could supply any
field for this record. Everything below is repository evidence, registry evidence (PyPI, GitHub, Read the
Docs), or literature evidence (ADS/SciX, DataCite dataset records).

---

### 3. Code Repository (MANDATORY)
https://github.com/NCAR/stokespy

Carried over unchanged from the existing HSSI record and independently confirmed: the GitHub API returns
`full_name: NCAR/stokespy`, `archived: false`, `disabled: false`, default branch `main`, created
2021-05-13, last pushed 2022-03-24. The repository has not moved, so there is no stale-URL correction to
make.

Two forks exist (`rickyegeland/stokespy`, `stpiamce/stokespy`); both were last pushed 2022-03-24 or earlier,
so neither is a newer authoritative location and the `NCAR` copy remains canonical. This also rules out
Development Status `Moved` (Field 23).

---

### 4. Software Functionality (MANDATORY)

The existing HSSI record carried only `Data Processing and Analysis`. That single value is not wrong, but it
is far from complete: it omits the package's entire visualization layer (the whole of `plotting.py`, 433
lines, plus a `plot()` method on five of the six public classes), its coordinate handling, and the specific
processing operations it performs. The values below are each tied to concrete code. Every subcategory's
parent top-level category is also listed, as the taxonomy requires.

**Selected values (14):**

- `Coordinate Transforms`
- `Coordinate Transforms: Solar`
- `Data Processing and Analysis`
- `Data Processing and Analysis: 2D Slices`
- `Data Processing and Analysis: Analysis`
- `Data Processing and Analysis: Data Access and Retrieval`
- `Data Processing and Analysis: Data Reduction`
- `Data Processing and Analysis: Image Processing`
- `Data Processing and Analysis: Processing`
- `Data Processing and Analysis: Wave Polarization Analysis`
- `Data Visualization`
- `Data Visualization: 2D Graphics`
- `Data Visualization: 2D Slices`
- `Data Visualization: Line Plots`

**Why each was selected:**

- **`Data Processing and Analysis: Wave Polarization Analysis`** — the defining capability of the package,
  and the reason its name is *Stokes*Py. `StokesCube` exposes the four Stokes parameters as properties
  `I`/`Q`/`U`/`V` (`stokespy/stokespy.py:299–317`) and computes derived polarimetric quantities from them:
  total polarization `P = sqrt(Q² + U² + V²)` (`:319–326`), linear polarization `L = sqrt(Q² + U²)`
  (`:328–334`), and linear polarization angle `theta = 0.5·arctan(U/Q)` (`:336–342`), each also available as a
  2D map (`P_map`, `L_map`, `theta_map`, `:430–456`) and as a 1D profile (`P_profile`, `L_profile`,
  `theta_profile`, `:515–541`). The `normalize` constructor option divides Q, U, V by I, or by a supplied
  continuum intensity (`:264–297`). The subcategory's own definition names "Stokes parameters, polarization
  ellipse, wave analysis methods"; this is a direct match.
- **`Data Processing and Analysis: Data Access and Retrieval`** — `load_HMI_stokes()` and
  `load_HMI_magvec()` query and download data from the Joint Science Operations Center through sunpy's
  `Fido`: `attrs.jsoc.Series('hmi.S_720s')` / `attrs.jsoc.Series('hmi.ME_720s_fd10')`,
  `attrs.jsoc.Notify(user_email)`, `Fido.search(...)`, `Fido.fetch(results, path=user_dir, max_conn=1)`
  (`stokespy/instload.py:78–104` and `:216–242`). Both are exported in the public API
  (`stokespy/__init__.py:4,11`). This is a user-called retrieval function, not an internal utility.
- **`Data Processing and Analysis: 2D Slices`** — extracting 2D planes from higher-dimensional volumes is a
  primary, advertised operation. `StokesCube._stokes_map()` reduces the 4D (stokes, wavelength, coord1,
  coord2) cube to a 2D `StokesParamMap` at a chosen wavelength (`stokespy/stokespy.py:348–380`), and
  `MagVectorCube._magnetic_map()` slices the 3D magnetic cube to a 2D `MagVectorMap` per component
  (`:634–643`, with `B`/`inclination`/`azimuth` properties at `:645–658`). `docs/stokes_classes.rst`
  demonstrates exactly this.
- **`Data Processing and Analysis: Data Reduction`** — when a wavelength *range* is requested,
  `_stokes_map()` integrates over it, collapsing a spectral cube into a single bandpass map:
  `newcube_data = np.sum(newcube.data[ix_0:ix_1+1,:,:], axis=0)` (`stokespy/stokespy.py:376`).
  `StokesParamMap` is documented as "a 2D map of bandpass intensities" (`:100–103`). This selection rests on
  the wavelength integration specifically; note that `StokesParamMap.average()` (`:120–122`) is a declared
  but unimplemented stub (`pass`) and was **not** counted as evidence. (The stub belongs to
  `StokesParamMap`, whose class body spans `:100–141`; `StokesParamCube` (`:33–97`) declares no `average()`
  at all.)
- **`Data Processing and Analysis: Image Processing`** — both HMI loaders accept a `derotate` keyword that
  rotates and resamples each image to correct HMI's roll relative to solar north, via
  `tmp_map.rotate(order=3)` (cubic interpolation) — `stokespy/instload.py:140–141` and `:287–288`, documented
  in the loaders' docstrings at `:69` and `:207`. This is a user-facing image-resampling operation on the
  pixel data.
- **`Data Processing and Analysis: Processing`** — the general pipeline work the loaders perform beyond
  retrieval: reshaping flat file lists into a `(4, 6, ny, nx)` Stokes array (`instload.py:145`),
  transposing Hinode arrays into the required axis order (`:360`), stacking named magnetic-parameter FITS
  extensions into a cube in a fixed order (`:272–293`, `:406–409`), selecting the observation nearest a
  requested time from GPS-scale timestamps (`:111–129`, `:249–266`), and synthesizing a 3- or 4-axis WCS.
  The WCS work takes two different forms, and the distinction matters to anyone reading this code:
  - *HMI* — the celestial header is obtained from `sunpy.map` (`tmp_map.wcs.to_header()`) and the extra axis
    is appended to it: a WAVE axis for the Stokes cube (`:147–173`) and a Parameter axis for the magnetic
    vector cube (`:299–313`).
  - *Hinode* — the whole WCS is constructed from scratch, because these loaders never go through
    `sunpy.map` and so have no pre-existing celestial header to extend. `load_HinodeSP_stokes` builds
    `astropy.wcs.WCS(naxis=4)` with `ctype = ["HPLN-TAN", "HPLT-TAN", "WAVE", "STOKES"]` (`:362–375`,
    the assignment itself at `:369–370`), while `load_HinodeSP_magvec` builds a 3-axis WCS,
    `astropy.wcs.WCS(naxis=3)` with `ctype = ["HPLN-TAN", "HPLT-TAN", 'Parameter']` (`:411–436`, assignment
    at `:430–431`) — no WAVE or STOKES axis, mirroring the HMI magvec case.
- **`Data Processing and Analysis: Analysis`** — the catch-all for the scientific calculations above
  (derived polarimetric quantities, intensity normalization, bandpass integration) that a user performs on
  the data rather than as a pipeline step.
- **`Coordinate Transforms` and `Coordinate Transforms: Solar`** — coordinate handling is the package's
  advertised selling point, not an internal detail. `docs/introduction.rst` states the goal is "to take
  advantage of the WCS while insulating the user from the complexities of setting up a valid WCS," and
  `docs/stokes_classes.rst` states "The `StokesCube` world coordinate system (WCS) is used to map physical
  (world) coordinates to array index, finding the nearest valid index." Concretely: `get_wav_ind()` converts
  a physical wavelength `Quantity` to an array index through the sliced WCS
  (`stokespy/stokespy.py:382–412`, mirrored at `:55–85`); `get_spatial_ind()` accepts a `SkyCoord`, converts
  an ICRS coordinate into the cube's own observer frame (`coords.ra.to(...)`, `coords.dec.to(...)`, then
  `SkyCoord(Tx=…, Ty=…, frame=self.frame)`) and resolves it to array indices via
  `wcs.world_to_array_index()` (`:478–497`); `coord1_axis()` / `coord2_axis()` return the physical
  helioprojective axes (`:248–258`, `:660–670`); and `StokesCube.frame` exposes the observer frame captured
  from the source data (`:207–239`). The **Solar** subcategory is the right one because the frame in play is
  helioprojective — the WCS `ctype` values are `HPLN-TAN`/`HPLT-TAN` (`instload.py:370`, `:431`), the plot
  axes are labelled "Helioprojective Longitude"/"Helioprojective Latitude" (`plotting.py:94–95`, `:211–217`,
  `:342–348`, `:395–396`, `:406–407`), and the documented example passes a helioprojective `SkyCoord`
  (`docs/stokes_classes.rst`: `SkyCoord(Tx = 148 * u.arcsec, Ty = 67 * u.arcsec, frame = stokes.meta['frame'])`).
  The transform machinery itself is astropy's; what stokespy contributes — and what a user benefits from —
  is the world-coordinate access API over its own data model, which the classification guide's inclusion
  rule covers.
- **`Data Visualization`, `Data Visualization: 2D Graphics`, `Data Visualization: Line Plots`,
  `Data Visualization: 2D Slices`** — `plotting.py` is entirely devoted to rendering, and five public
  classes expose a `plot()` method (`StokesCube`, `StokesParamCube`, `StokesParamMap`, `StokesProfile`,
  `MagVectorMap`). *2D Graphics*: `imshow` of maps drawn on a WCS projection (`plotting.py:386–396`
  `_plot_image`, and the four-panel I/Q/U/V mosaics at `:184–187`, `:315–318`). *Line Plots*: Stokes
  profiles plotted against wavelength, `ax.plot(plot_wav.value, data)` (`:18–36` `_plot_profile`, `:224–227`,
  `:78–81`). *2D Slices*: interactive views that step a wavelength slider through 2D slices of the 3D/4D
  cube, `img_plot.set_data(data[ixt,:,:])` (`:398–433` `_plot_3d_cube`, `:292–384` `_plot_all_data`,
  `:144–289` `_plot_all_profiles`, `:38–142` `_plot_context_all_profiles`). `CHANGELOG.rst` confirms:
  "Added plotting functionality for `StokesCube`, `MagVectorCube` and the derived slice classes. Plots in a
  jupyter widget environment contain interactive sliders when necessary."

**Considered and rejected** — recorded so a future refresh does not re-propose them:

- `Models and Simulations` and every subcategory, especially `Models and Simulations: Forward-Fitting` and
  `Models and Simulations: Physics-Based`. This is the most likely misreading of this record, because the
  GitHub repository description says "…data and inversions" and `MagVectorCube` is documented as
  "inversions." stokespy performs **no** inversion, forward synthesis, or fitting. It *reads* inversion
  products computed elsewhere: HMI's `hmi.ME_720s_fd10` Milne-Eddington series (`instload.py:237`) and the
  Hinode SP Level 2 FITS extensions `Field_Strength`, `Field_Inclination`, `Field_Azimuth`
  (`instload.py:386`, `:405–409`). No solver, no optimizer, no `scipy.optimize`, no atmosphere model appears
  anywhere in the three modules. `docs/atmos_classes.rst` and `docs/index.rst` promise stratified-atmosphere
  classes and tools "to aid in the comparison of synthesized polarized spectra from model atmospheres to
  observational data" as **future** work; that promise was never implemented and 0.5.0 was the only release.
- `Data Processing and Analysis: Calibration`. stokespy consumes already-calibrated products — HMI Level 1
  Stokes and Level 2 inversions, Hinode SP Level 1 ("calibrated") and Level 2. The funded proposal likewise
  describes "calibrated Stokes spectra" as the *input*. No response function, gain, dark, or flat-field
  correction exists in the code. (The `derotate` geometric correction is classified as Image Processing
  above, not Calibration.)
- `Data Processing and Analysis: File Format Conversion`. stokespy reads FITS and writes nothing. See
  Field 19.
- `Data Processing and Analysis: Time Series Analysis`. Time handling is limited to selecting the single
  observation nearest a requested date by comparing GPS seconds (`instload.py:111–129`, `:249–266`). There is
  no temporal filtering, trend, or correlation analysis, and no time axis in any data class — the cube axes
  are (stokes, wavelength, coord1, coord2).
- `Data Processing and Analysis: Spectrogram` and `Data Visualization: Spectrogram`. stokespy plots
  wavelength profiles (intensity versus wavelength at one pixel) and spatial maps. Nothing computes or
  displays a time–frequency representation, and there is no FFT, STFT, or wavelet anywhere in the package.
- `Data Processing and Analysis: Energy Spectra`. The spectral axis is wavelength (metres/nm), not energy;
  no energy channels or flux-versus-energy computation exists.
- `Data Visualization: Movies`. The interactivity comes from `matplotlib.widgets.Slider`
  (`plotting.py:3`, `:117`, `:260`, `:355`, `:414`). There is no `matplotlib.animation` import, no frame
  export, and no movie writer.
- `Data Visualization: Web-Based`. Tempting, because `CHANGELOG.rst` says plots "in a jupyter widget
  environment contain interactive sliders." But the interactivity is backend-agnostic matplotlib widget
  code — there is no plotly, bokeh, dash, ipywidgets, or web framework in the dependencies
  (`setup.cfg` `install_requires`: ndcube, sunpy[net], astropy, numpy, matplotlib, natsort) or in any
  import. The Jupyter mention describes where the sliders happen to be usable, not a browser-based
  visualization product.
- `Data Visualization: Mission-Specific`. Plot titles interpolate `meta['inst']` (`'SDO/HMI'` or
  `'Hinode/SP'`, set at `instload.py:175`, `:315`, `:377`, `:438`; used at `stokespy.py:130–131`), but that is
  a text label on an otherwise generic figure. No plot type is specific to either mission's data.
- `Data Visualization: 3D Graphics`. No `mplot3d`, vtk, mayavi, or pyvista; all rendering is 2D imshow and
  line plots.
- All of `Mission-related`. stokespy is an analysis package for public archive products, not part of any
  mission's ground system, pipeline, or operations. It ingests SDO and Hinode data as an external consumer.
- All of `Servers and Environments`. No server, container definition, Dockerfile, MPI, or HPC job script;
  the only CI containers (`.circleci/config.yml` uses `continuumio/miniconda3`) are build infrastructure for
  the project itself, not a delivered capability.

---

### 5. Related Region (MANDATORY)
- Photosphere
- Solar Environment

`Solar Environment` is carried over from the existing HSSI record and retained. `Photosphere` is added
because it is the specific region the implemented functionality actually serves, and the current `Region`
vocabulary is fine-grained enough to reward specificity over the broad value:

- The HMI loader hard-codes the Fe I 6173.345 Å line as the cube's central wavelength
  (`l0 = 6173.345 * 1.e-10` m, with dispersion `dl = 0.0688e-10` m — `instload.py:150–151`). Fe I 6173 Å is a
  photospheric line, and `hmi.ME_720s_fd10` is HMI's photospheric vector-magnetic-field inversion.
- The Hinode SOT/SP example wavelength in `docs/stokes_classes.rst` is 630.142 nm, within the SP's
  Fe I 630.15/630.25 nm photospheric pair.
- `MagVectorCube` holds field strength, inclination and azimuth from those photospheric inversions
  (`stokespy.py:595–658`).

**Considered and rejected:** `Chromosphere`. `docs/index.rst` speaks generally of "the inferred solar
atmosphere," and the package aspires to serve "the various spectropolarimetric datasets and inversion codes
in the community," but every loader shipped in 0.5.0 targets a photospheric line, and no chromospheric
diagnostic (He I 10830, Ca II, Mg II) appears anywhere. `Solar Interior` was rejected for the same reason —
stokespy does not touch helioseismic data, despite HMI's name.

---

### 6. Authors (MANDATORY)

Two authors, both carried over from the existing HSSI record. Authorship is corroborated by three
independent repository sources: `LICENSE.rst` line 1 ("Copyright (c) 2021, Gabriel Dima & Ricky Egeland"),
`README.rst` line 13 ("This project is Copyright (c) Gabriel Dima & Ricky Egeland"), and `docs/conf.py:14`
(`author = 'Gabriel Dima & Ricky Egeland'`). Git history shows both as substantial contributors — 43
commits from Ricky Egeland and 22 from Gabriel Dima (65 in total) across five author identities
(`gdima@hawaii.edu`, `stpiamce`, `stpiamce@users.noreply.github.com`, and `ricky.egeland@gmail.com`,
`ricky.egeland@protonmail.com`). No third contributor appears in the history, so the two-author list is
complete. There is no `CITATION.cff`, `AUTHORS`, or `CONTRIBUTORS` file to reconcile against.

Neither author is an organization: both carry ORCIDs, and no organizational author (team, consortium,
collaboration) is credited anywhere in the repository. No ROR-identified author entry applies.

**Both authors carry `NCAR High Altitude Observatory` (https://ror.org/03773p874)** — the institution under
which stokespy was written. HSSI's stored record was missing it for both of them, and the reason is worth
knowing: **neither author's ORCID record contains it.** Egeland's lists no pre-JSC employment at all, and
Dima's lists NSO and CIRES but no NCAR appointment. The original HSSI record derived its affiliations from
ORCID, so the gap was inherited from that source rather than introduced by whoever entered the record — and a
future refresh consulting only ORCID will reproduce it. It is an addition alongside every affiliation the
record already held, not a replacement for any of them.

#### Author 1: Gabriel Dima
- **Identifier:** https://orcid.org/0000-0002-6003-4646
- **Affiliations (5):**
  - Cooperative Institute for Research in Environmental Sciences — https://ror.org/00bdqav06
  - National Solar Observatory — https://ror.org/00b9pg524
  - University of Cambridge — https://ror.org/013meh722
  - University of Hawaii at Manoa — https://ror.org/01wspgy28
  - NCAR High Altitude Observatory — https://ror.org/03773p874

All four stored affiliations were verified against ORCID 0000-0002-6003-4646 and are genuine; none should be
dropped. Each traces to a specific entry in that ORCID record:

| Stored affiliation | ORCID entry | ORCID's own identifier | Dates |
|---|---|---|---|
| Cooperative Institute for Research in Environmental Sciences | employment, Research Scientist, Boulder US | ROR `https://ror.org/00bdqav06` | 2022-04-01 → present |
| National Solar Observatory | employment, Postdoctoral Research Associate, Makawao HI US | Ringgold 41574 | 2017-09-18 → present |
| University of Hawaii at Manoa | **education**, PhD in Astronomy, Institute for Astronomy, Honolulu | GRID `grid.410445.0` | 2009-08-12 → 2017-08-12 |
| University of Cambridge | **education**, BA and MSci (two entries), Cambridge GB | Ringgold 2152 | 2005-10-01 → 2009-06-27 |

Three findings worth carrying forward:

1. **Two of the four are degrees, not employments.** University of Hawaii at Manoa and University of
   Cambridge appear in ORCID's *educations* section only. Whoever built the original record took the union
   of ORCID employments and educations. They are factually correct associations for this person and are
   retained, but a reader should know they describe where he studied (through 2017), not where stokespy was
   written.
2. **CIRES postdates the software.** His CIRES employment begins 2022-04-01, eight days after the 0.5.0
   release (2022-03-24) and the final commit. It is his correct current-era affiliation and is retained, but
   it is not the affiliation under which stokespy was authored.
3. **The RORs are correct entities even where ORCID used a different identifier scheme.** ORCID records
   NSO with a Ringgold ID, Cambridge with a Ringgold ID, and Hawaii with a GRID ID; the stored RORs were
   independently confirmed via the ROR API to denote those same institutions (`00b9pg524` = National Solar
   Observatory, `013meh722` = University of Cambridge, `01wspgy28` = University of Hawaiʻi at Mānoa). Note
   that ROR's display name for `01wspgy28` uses diacritics — "University of Hawaiʻi at Mānoa" — and
   "University of Hawaii at Manoa" is a registered ROR *alias*; the stored HSSI form is therefore an
   accepted name for the right organization and needs no change.

**Why NCAR High Altitude Observatory is added:** the affiliation under which Dima actually wrote stokespy
was absent from both his ORCID record and the stored HSSI record. Evidence that he held it:

- `setup.cfg:4` and `.sunpy-template.yml:6` record his contact address as `gdima@ucar.edu`, and PyPI's
  package metadata carries the same (`author_email: gdima@ucar.edu`) — a UCAR/NCAR institutional address, in
  the released package itself.
- He published in the same period with that affiliation: ADS `2021AAS...23832810D` (first author, "Dima,
  G. I.") gives "High Altitude Observatory, University Corporation for Atmospheric Research, Boulder, CO";
  `2021ApJ...921...39A` gives "High Altitude Observatory, 3090 Center Green Drive, Boulder, CO, 80301";
  `2021AGUFMSH44A..05A` gives "High Altitude Observatory, Boulder, United States".
- The repository itself lives in the `NCAR` GitHub organization, and its Azure Pipelines build URL is
  `https://dev.azure.com/NCAR/stokespy/...` (`azure-pipelines.yml:5`).

`NCAR High Altitude Observatory` (https://ror.org/03773p874) already exists as an HSSI organization row, so
this is an addition of an existing organization rather than the creation of a new one.

**Considered and rejected for Dima: `University Corporation for Atmospheric Research`**
(https://ror.org/04zhhyn23), which also exists as a row. UCAR is the employer of record for NCAR staff, and
Dima's `@ucar.edu` address and the 2021 AAS abstract both point at it. HAO is chosen because it is the
specific laboratory where the work was done, and where the Community Spectropolarimetric Analysis Center
whose data stokespy reads is located (Field 28). Note that **Dima's HAO affiliation rests entirely on the
evidence above** — the `@ucar.edu` address in the released package plus the 2021 AAS/ApJ/AGU affiliation
lines. Egeland's CV, which settles the question for Egeland, says nothing about Dima.

#### Author 2: Ricky Egeland
- **Identifier:** https://orcid.org/0000-0002-4996-0753
- **Affiliations (2):**
  - Johnson Space Center — https://ror.org/04xx4z452
  - NCAR High Altitude Observatory — https://ror.org/03773p874

**Egeland's Johnson Space Center affiliation is genuine, and its ROR has always been correct; what was wrong
was the name recorded for the organization.** A NASA human-spaceflight centre is a surprising affiliation for
a solar physicist, and invites suspicion of a mis-entered value — but the ORCID employment entry it comes
from is internally consistent and identifies the right organization:

- Organization name: "National Aeronautics and Space Administration Johnson Space Flight Center"
- Department: "Human Health and Performance Directorate, Space Medicine Operations Division, Mission
  Operations Branch"
- Role: "AST, Human/Machine Systems"
- City/country: Houston, US
- Disambiguation identifier: ROR `https://ror.org/04xx4z452`
- Dates: 2021-07-19 → present (his only ORCID employment entry)

The disambiguation identifier is not mis-selected: ROR `04xx4z452` resolves to Johnson Space Center, located
in Houston, a child of the National Aeronautics and Space Administration — matching the entry's own
department, role and city, and the NASA centre its organization-name string was plainly reaching for. Egeland genuinely changed fields; ADS confirms the transition
independently, with his affiliation appearing as "NASA Johnson Space Center, 2101 E NASA Pkwy, Houston,
TX 77058" on `2023AdSpR..72.5161W` and `2023BAAS...55c.333R`, "NASA JSC SRAG" on `2023shin.confE.205W`, and
"NASA Johnson Space Center" on `2021plat.confE..20S`. The affiliation itself is sound and must not be read as
drift to remove.

**The name is `Johnson Space Center`, ROR's own display name for `04xx4z452`.** The organization was formerly
labelled `Johnson Space Flight Center` in this record, and that string is wrong twice over. It is not among
ROR's registered names for `04xx4z452` — those are `Johnson Space Center` (the display name),
`Lyndon B. Johnson Space Center` (NASA's official name, carried by ROR as an alias),
`Centro Espacial Lyndon B. Johnson`, the historical `Manned Spacecraft Center`, and the acronyms `JSC` and
`MSC` — and it names no real institution: it conflates Johnson Space Center in Houston with Goddard Space
Flight Center, a distinct NASA centre carrying its own ROR (https://ror.org/0171mag52). The likely origin of
the bad label is the ORCID organization-name string quoted verbatim above, which itself reads "National
Aeronautics and Space Administration Johnson Space Flight Center"; that quotation is kept here as evidence of
what ORCID's record says, not as a name to copy. Anyone taking an organization name straight from that ORCID
entry will regenerate the error. **Do not reintroduce "Johnson Space Flight Center", and do not read the two
forms as two different organizations — they share one ROR and one institution.**

**Why NCAR High Altitude Observatory is added — decided by Egeland's own CV.** His ORCID lists no pre-JSC
employment at all, so ORCID alone cannot supply this affiliation. His CV supplies it directly. Its
**Appointments** section reads, verbatim:

> `2019–now` — `Project Scientist at the High Altitude Observatory/NCAR, Boulder, CO`
> *`Hinode SOT/SP operations & data analysis; DKIST level-2 pipeline.`*

with two earlier NCAR appointments beneath it: `2017–2019` `Advanced Study Program Posdoctoral Fellow` /
`NCAR High Altitude Observatory, Boulder, CO` (the missing "t" in "Posdoctoral" is the CV's own typo), and
`2014–2017` `Newkirk Graduate Research Fellow` / `NCAR High Altitude Observatory, Boulder, CO`. The Grants &
Awards section adds `Newkirk Fellowship; High Altitude Observatory/NCAR, Boulder, CO; $35k/year (Mar 2014)`.
The CV's header gives his address as `egeland@ucar.edu`.

Three things this settles:

1. **The appointment spans the entire stokespy development window.** `2019–now` was open-ended as of the
   CV's ~mid-2020 date, and covers the first commit (2021-05-13) through the final commit and the 0.5.0
   release (2022-03-24). This is the affiliation under which he wrote the software, stated in his own words
   rather than inferred from a co-author's affiliation line.
2. **His stated duties in that role are precisely what stokespy implements.** The subtitle
   "Hinode SOT/SP operations & data analysis" names the exact instrument path of Fields 31–32 — the Hinode
   SOT/SP loaders are the work of the person whose job was Hinode SOT/SP operations and data analysis. This
   is stronger corroboration than an affiliation line on a co-authored paper. The CV's **Observing** section
   independently reinforces the Hinode connection within the development window: `"HOP 393: Cycle 24/25
   equatorial transition"; PI, Hinode spacecraft (Dec 2020–Dec 2021)`.
3. **`NCAR High Altitude Observatory` appears verbatim in the CV**, matching the existing HSSI organization
   row name exactly. To be precise about where: that exact string is the institution line of the `2017–2019`
   and `2014–2017` appointments. The stokespy-window `2019–now` entry uses the other word order,
   "High Altitude Observatory/NCAR". Both denote the same laboratory, and the HSSI row's ROR
   (https://ror.org/03773p874, ROR display name "NSF NCAR High Altitude Observatory", alias "High Altitude
   Observatory") is the right organization either way.

Independent supporting evidence, consistent with the CV:

- ADS `2019hdee.prop...18E` — the NASA proposal that funded StokesPy (see Fields 25–26) — records his
  affiliation as "University Corporation For Atmospheric Research (UCAR)".
- ADS `2022ApJ...925..176C` ("Convolutional Neural Networks and Stokes Response Functions", published
  February 2022, i.e. within the stokespy development window) lists "Egeland, Ricky || High Altitude
  Observatory, National Center for Atmospheric Research, Boulder, CO, USA". The same HAO/NCAR affiliation
  appears on `2020NatAs...4..382C`, `2020ApJ...900..154M`, `2021ApJ...921..122M`, `2021ApJ...917...27J`,
  `2021SoPh..296..189M`, `2022csss.confE..95S`, and `2023A&A...672A..56S`.
- The HAO and JSC affiliations overlap in 2021–2022, which is expected of someone mid-transition whose
  papers name the institution where each piece of work was done. For stokespy, that institution is HAO/NCAR.

**Considered and rejected for Egeland: `University Corporation for Atmospheric Research`**
(https://ror.org/04zhhyn23) — the string the ADS proposal record itself uses, and the parent corporation
that employs NCAR staff. HAO wins because the CV names the *laboratory* rather than the parent corporation
for every one of his NCAR-era entries in both the Appointments and Grants & Awards sections; UCAR appears in
the CV only as his email domain and in unrelated outreach entries, never as an appointing institution.

**Durable consequence: his ORCID record is incomplete, and will stay that way unless he updates it.** The CV
documents a continuous run of NCAR/HAO appointments from 2014 onward (the 2014–2017 and 2017–2019
fellowships, then the open-ended 2019–now Project Scientist post) that ORCID does not carry at all. Because
the CV is a ~2020-era document, it attests that run up to its own date; the post-2020 continuation into the
stokespy window is what the 2022 publication affiliations above establish. A future refresh that consults only ORCID will therefore
re-derive the same gap and may be tempted to treat the HAO affiliation as unsupported. It is not — the
primary source is the CV, cited above.

---

### 7. Software Name (MANDATORY)
stokespy

Carried over unchanged from the existing HSSI record. It matches the repository name (`NCAR/stokespy`), the
PyPI distribution name (`stokespy`), the importable module (`import stokespy`), the Read the Docs project
slug (`stokespy`), the Sphinx `project` value (`docs/conf.py:12`), and the `.sunpy-template.yml`
`package_name`/`module_name`. Field 7's instruction is "the name of the software package as listed on the
code repository," which this satisfies exactly.

**Considered and not selected:** `StokesPy`, the camel-cased styling the project uses in its own prose —
`CHANGELOG.rst` ("This is the first release of StokesPy!"), the documentation throughout
(`docs/index.rst` "StokesPy Documentation", `docs/installation.rst` "Installing StokesPy"), and the funded
proposal ("we propose to develop StokesPy"). This is a presentation choice rather than a different name, and
the stored lower-case form is the one the form asks for. Recorded so a future agent recognizes the two forms
as the same software and does not treat the styled variant as newer or more authoritative.

---

### 8. Description (MANDATORY)

**Value (replaces the stored description):**

> StokesPy is an open-source Python package for the analysis and visualization of solar spectropolarimetric
> data and the inversion results derived from it. Built on the ndcube data model, it provides coordinate-aware
> containers for full Stokes (I, Q, U, V) profiles and for vector magnetograms of field strength, inclination
> and azimuth. Stokes maps and profiles can be extracted by physical wavelength or sky coordinate rather than
> by array index, with derived polarimetric quantities and plotting that includes interactive
> wavelength-slider views; loader functions build cubes directly from SDO/HMI and Hinode
> SOT/Spectro-Polarimeter data.

639 characters, in three sentences. **The restrained length is deliberate, and was chosen over a fuller
alternative.** The alternative ran to roughly 1,675 characters: it enumerated every public class by name,
described the WCS slicing mechanism in detail, listed the individual derived quantities, distinguished JSOC
download from local-directory reading, and closed with the project's own statement of intent about becoming a
common interface for the community's spectropolarimetric datasets. All of it was accurate, but it read as
documentation rather than as a catalogue description, and Field 8's purpose is to let a prospective user
decide quickly whether the package is relevant to their work. The chosen form keeps every fact that serves
that decision — what the package does, what data model it is built on, what it holds, how slicing is
addressed, that it plots, and which two instruments it loads — and drops the detail a reader would go to the
documentation for anyway. **Do not read the brevity as an incomplete draft and re-expand it.**

**Why the capability claims are scoped to the Stokes side.** The third sentence attributes wavelength- and
sky-coordinate extraction, derived polarimetric quantities, and interactive wavelength-slider plotting to
Stokes maps and profiles specifically, and deliberately makes no such claim for the vector-magnetogram
container. That asymmetry is real in the code, not cautious phrasing: `StokesCube` carries `get_wav_ind()`,
`get_spatial_ind()`, the `P`/`L`/`theta` derived quantities with their `_map` and `_profile` variants, and a
`plot()` method, whereas `MagVectorCube` exposes only `magnetic_axis`, `_magnetic_map`, `B`, `inclination`,
`azimuth`, `coord1_axis` and `coord2_axis` — no wavelength or sky-coordinate lookup, no derived quantities,
and no `plot()` of its own (a user reaches a plottable object through `MagVectorMap`). A wavelength slider is
impossible on that side in any case, because the magnetic-vector WCS has no WAVE or STOKES axis (Field 4).
An earlier draft said these capabilities were "provided for each container," which read as feature parity
between the two families and was not accurate. Recorded so a future refresh does not re-broaden it.

**Previously stored value:**

> `Package for analysis of solar spectropolarimetric data and inversions\nOpen-source (future) SunPy affiliated package for the visualization and analyis of solar spectropolarimetric data and inversion results.`

**Provenance of the stored value, established exactly.** It is the concatenation of two distinct one-line
blurbs joined by a newline, reproduced byte-for-byte:

1. `Package for analysis of solar spectropolarimetric data and inversions` — the GitHub repository's
   `description` field, verbatim.
2. `Open-source (future) SunPy affiliated package for the visualization and analyis of solar spectropolarimetric data and inversion results.` — line 8 of `README.rst`, verbatim.

The stored value is exactly `github_description + "\n" + readme_line_8`, byte for byte.

**The typo is verbatim in the source, in four places.** `analyis` (for `analysis`) appears in `README.rst`
line 8 at byte offset 367, in `setup.cfg:8` (`description = …`), in `.sunpy-template.yml:4`
(`short_description: …`), and in PyPI's published `summary` for stokespy 0.5.0. The three in-repository
occurrences are byte-identical to each other and to the second half of the stored description. So the stored
value did not introduce the typo — it inherited it. The typo originates in `.sunpy-template.yml`, the
cookiecutter answers file, and was propagated to `README.rst` and `setup.cfg` when the SunPy package
template was rendered (commit `53d9e5c`, 2021-09-24).

**Why the stored text was replaced rather than kept.** Normally a submitter's or maintainer's own wording is
preserved even if it could be phrased better. Four material defects, not stylistic preferences, argued for
replacement here:

1. It is a **concatenation artifact**, not authored prose: two independently written sentences run together
   with no transition, saying nearly the same thing twice ("analysis of solar spectropolarimetric data and
   inversions" / "visualization and analyis of solar spectropolarimetric data and inversion results").
   Field 8 asks for text "written with proper capitalization, grammar, and punctuation."
2. It contains a **misspelling** in the user-visible preview text.
3. It asserts **"(future) SunPy affiliated"**, a status that never came about — see below. Carrying an
   unfulfilled affiliation claim into HSSI's public preview is a factual problem, and the parenthetical
   "(future)" is meaningless four years after the project stopped.
4. It is **not sufficiently detailed** for Field 8's stated purpose ("sufficiently detailed to provide the
   potential user with information to determine if the software is useful to their work"). It names no data
   class, no supported instrument, no capability, and no dependency.

**Authoritative source for the replacement.** The text is a condensation of the project's own
self-description — `docs/index.rst` (the "StokesPy Documentation" landing page) and `docs/introduction.rst` —
cross-checked against the actual public API in `stokespy/__init__.py`, `stokespy/stokespy.py` and
`stokespy/instload.py`, and against `CHANGELOG.rst`'s 0.5.0 feature list. It adds no capability the code does
not have, and deliberately omits the aspirational items (SunPy affiliation, DKIST, slab/stratified atmosphere
classes, synthesized-spectrum comparison).

**One omission that was a close call.** `docs/index.rst` states the project's intent to become "a common
interface and toolset for the various spectropolarimetric datasets and inversion codes in the community" and
"a repository of instrument/inversion code-specific data loading routines." That is the project's own account
of what it is *for*, and the longer alternative closed with it. It is left out because it describes an ambition for
a package that stopped development after one release (Field 23) and never gained the community adoption the
sentence anticipates (Field 27) — so in a catalogue description it would read as a claim about present reach
rather than as a statement of intent. The intent is preserved here in the dossier instead, which is the right
place for it.

**SunPy affiliation: negative research.** The repository claims "(future) SunPy affiliated package"
(`README.rst:8`, `setup.cfg:8`) and "a (future) Sunpy-affiliated packaged" (`docs/index.rst`), and the funded
proposal called StokesPy "a new SunPy affiliate package." It never became one. As of this extraction,
sunpy.org's affiliated-packages page lists neither `stokespy` nor `StokesPy` in any of its three
tiers — current (sunpy, ndcube, drms, sunraster, sunkit-image, aiapy, sunpy-soar, roentgen,
sunkit-instruments, dkist, solarmach, sunkit-magex, xrtpy, irispy-lmsal, scope, spectroflat), provisional
(pyflct, radiospectra), or historical (pfsspy, demcmc). **Do not describe stokespy as a SunPy affiliated
package.** The only defensible related statements are that it is built on the sunpy/ndcube stack (true, see
Field 30) and that affiliation was an unrealized goal.

---

### 9. Concise Description (OPTIONAL)
Python package for analyzing and visualizing solar spectropolarimetric data and inversion products,
providing coordinate-aware Stokes and vector-magnetogram cubes built on the ndcube data model.

194 characters, within Field 9's 200-character limit. Nothing was stored for this field previously. It is
supplied because the first 200 characters of the Field 8 description end mid-sentence ("…Built on the ndcube
data model, it provides co"), which is the exact circumstance Field 9 exists for: a truncated Field 8 would
cut off before naming what the package actually holds. This field says it in one sentence, naming the two
data-model families (Stokes cubes, vector magnetograms) that distinguish this package from a generic solar
image library. Field 8's description still runs well past 200 characters, so this field does real work
rather than merely restating an already-short description.

---

### 10. Publication Date (RECOMMENDED)
2021-05-13

Carried over unchanged from the existing HSSI record, and independently confirmed as the date the code
first became public: the initial commit `50c700e` ("Add stokespy package with StokesCube object") is dated
2021-05-13 16:52:41 -0600 = 2021-05-13 22:52:41 UTC, and the GitHub API reports the repository
`created_at: 2021-05-13T22:58:04Z`. The two agree to within six minutes.

**Alternative considered and not selected:** 2022-03-24, the date of the first (and only) packaged release
to PyPI. Field 10 is "Date of first broadcast/publication … Used for the initial version of the software,"
which the first public availability of the source satisfies; and Field 12's Version Date already carries
2022-03-24, so using it here as well would collapse two distinct facts into one. Recorded so a future
refresh does not read the difference between Fields 10 and 12 as an inconsistency.

**A date to ignore:** `docs/conf.py:13` reads `copyright = '2020, Gabriel Dima & Ricky Egeland'`, while
`LICENSE.rst:1` reads "Copyright (c) 2021". The 2020 is a stale cookiecutter default — no commit, issue, or
release predates 2021-05-13 — and is not evidence of a 2020 publication date.

**Scope note: the project is about a year older than this date.** Egeland's CV lists, under
**Presentations**, verbatim: `"StokesPy: An Introduction" Python in Heliophysics Spring 2020 Meeting,
Virtual (May 2020)`. StokesPy therefore existed as a project and was presented to the Python in
Heliophysics community roughly a year *before* the public repository's first commit (2021-05-13). The
2021-05-13 value is still correct for Field 10 — it is the date the software became publicly available,
which is what the field asks — but a future agent should not read it as the date the project began, and
should not treat the earlier `copyright = '2020'` string as an inconsistency to correct once this talk is
known about. Two cautions attach to the talk itself: it is a **community meeting presentation, not a
publication**, so it is not a Field 27 value (see Field 27), and being presented at a PyHC *meeting* implies
nothing about PyHC *registry* membership, which stokespy does not have (see the cross-cutting section).

---

### 11. Publisher (RECOMMENDED)
- **Organization:** GitHub
- **Publisher Identifier:** https://github.com

Nothing was stored for this field previously. Field 11's instruction is explicit for this case: with no DOI
obtained ("If no DOI has been obtained, indicate the repository host, such as GitHub or GitLab"), and
Field 2 establishes that stokespy has no DOI. The repository is hosted on GitHub; the identifier is a URL
because GitHub has no applicable ROR.

**Alternatives considered and not selected:** *Zenodo* — inapplicable, there is no Zenodo record.
*NSF National Center for Atmospheric Research* (https://ror.org/05cvfcr44) or *NCAR High Altitude
Observatory* (https://ror.org/03773p874) — defensible on the grounds that the repository lives in the
`NCAR` GitHub organization and the work was NCAR/HAO work, but Field 11 asks for the publishing *entity* of
the artifact and, absent a DOI, directs that to the repository host. *Python Package Index* — stokespy 0.5.0
is distributed there, but PyPI is a distribution channel for the release (relevant to Field 12), not the
publisher of the software record. Recorded so a future refresh does not treat GitHub as a careless default.

---

### 12. Version (RECOMMENDED)
- **Version Number:** 0.5.0
- **Version Date:** 2022-03-24
- **Version Description:** First release of StokesPy. Adds the `StokesCube` class for maps of Stokes
  profiles and the `MagVectorCube` class for maps of the vector magnetic field; plotting for `StokesCube`,
  `MagVectorCube` and the derived slice classes, with interactive sliders in a Jupyter widget environment;
  HMI data downloader/loader functions `load_HMI_stokes()` and `load_HMI_magvec()`; Hinode SOT/SP data
  loader functions `load_HinodeSP_stokes()` and `load_HinodeSP_magvec()`; and installation and usage
  documentation.
- **Version PID:** Not found — see Field 2; stokespy has no DOI at any granularity, so there is no
  version-specific DOI either.

**Correction of the stored value.** HSSI held a version row with an *empty* version number. The HSSI view
API renders that row as `"stokespy - "`, which is the view's `<software> - <number>` transform applied to an
empty number, not a stored string. `stokespy - ` must never be written into a version field; the value
belongs there as the bare number `0.5.0`.

**0.5.0 released 2022-03-24 is the latest authoritative release available now.** Seven independent registries
and sources were checked and all agree; nothing newer exists anywhere:

| Source | Finding |
|---|---|
| Git tags | `v0.5.0` is the only tag in the repository. It is a lightweight tag pointing at `830d14398eceaee1c8bae70f11a6183d5a9054cb`, which is also `HEAD` of `main` — the release and the tip of the default branch are the same commit. |
| `CHANGELOG.rst` | Single entry: `0.5.0 (2022-03-24)` / "This is the first release of StokesPy!" — and the only entry, so also the last. |
| PyPI | Exactly one release, `0.5.0`; one file, `stokespy-0.5.0.tar.gz`, uploaded `2022-03-24T20:54:48Z`, not yanked. No wheel was ever published. |
| GitHub Releases | The releases endpoint returns an empty list — no GitHub Release object was ever created (which is also why no Zenodo DOI exists). |
| conda / conda-forge | No `stokespy` package on anaconda.org (search returns an empty result set) and no `conda-forge/stokespy-feedstock` repository. Consistent with commit `824bffb` (2022-03-23) "Remove conda from installation docs" — conda distribution was explicitly dropped before release, and `docs/installation.rst` offers pip only. |
| Read the Docs | Three built versions: `v0.5.0` (tag), `stable` (tag), `latest` (branch `main`). `stable` and `latest` both resolve to the 0.5.0 content because the tag is `HEAD`. No later tag was ever built. |
| Zenodo | No record for stokespy. |

Corroborating dormancy: the GitHub API reports `pushed_at: 2022-03-24T20:56:47Z`, the last commit is
2022-03-24, both forks were last pushed on or before that date, and the repository is not archived. The
project has had no code activity in roughly four years and four months.

**Version Date rationale.** 2022-03-24 is agreed by the `CHANGELOG.rst` heading, the tag commit's date
(2022-03-24 20:24:33 UTC), and the PyPI upload timestamp (2022-03-24 20:54:48 UTC) — all the same calendar
day in UTC, so there is no timezone ambiguity to resolve.

**Version Description source.** Condensed from the `CHANGELOG.rst` 0.5.0 "New Features" list, which is the
project's own release note. It is reproduced faithfully rather than re-derived from the code, because a
version description should say what the release claimed to add.

---

### 13. Programming Language (RECOMMENDED)
- Python 3.x

Carried over unchanged from the existing HSSI record and confirmed: the package is pure Python.
`setup.cfg` sets `python_requires = >=3.7`; PyPI reports `requires_python: >=3.7`;
`.sunpy-template.yml` sets `minimum_python_version: 3.8` and `use_compiled_extensions: n`;
`tox.ini` declares `envlist = py{36,37,38}`; GitHub reports `language: Python`. Every source file in the
repository is `.py`, `.rst`, `.yml`/`.yaml`, `.cfg`, `.toml`, `.in`, `.bat`, `.sh`, or a Makefile — no C,
Cython, Fortran, or IDL source exists, so `Python 3.x` alone is complete rather than merely primary.
`Python 3.x` is the exact spelling the controlled vocabulary uses.

---

### 14. Reference Publication (RECOMMENDED)
Not found.

No paper describes stokespy. Negative research, so a later refresh need not repeat it:

- No `CITATION.cff` or `CITATION` file, no "How to cite" section in `README.rst` or anywhere under `docs/`,
  and no JOSS badge or submission.
- ADS/SciX full-text search `full:"stokespy"` — which covers title, abstract, body, keywords and
  acknowledgements of indexed records — returns exactly **one** hit, and it is a NASA proposal, not a
  publication: `2019hdee.prop...18E`, "SunPy support for multidimensional data and spectropolarimetric
  analysis" (Egeland, Ricky; NASA Proposal ID 19-HDEE19_2-0018). `abs:"StokesPy"` returns the same single
  record. A nonsense-token control query returned zero hits, confirming the search was actually discriminating.
- DataCite has no publication DOI matching stokespy (Field 2).

**Considered and not selected:** using the proposal `2019hdee.prop...18E` here. A funding proposal is not a
publication describing the software, it has no DOI, and its content belongs to Fields 25–26, where it is
recorded. Its bibcode is noted in several places in this file so a future agent can find it without
re-searching.

---

### 15. License (RECOMMENDED)
- **License:** BSD 3-Clause "New" or "Revised" License
- **License URI:** https://spdx.org/licenses/BSD-3-Clause.html

Carried over unchanged from the existing HSSI record and confirmed by four sources: `LICENSE.rst` contains
the 3-clause BSD text in full; `README.rst:13–17` states "licensed under the terms of the BSD 3-Clause
license"; `setup.cfg:5–6` sets `license = BSD 3-Clause` and `license_file = LICENSE.rst`; and GitHub's
license detection reports `spdx_id: BSD-3-Clause`, `name: BSD 3-Clause "New" or "Revised" License`.
`stokespy/__init__.py:1` also carries the SPDX-style header comment.

The recorded string is the canonical controlled-vocabulary name rather than the legacy duplicate
`New BSD license`, which survives in some HSSI license vocabularies but is not the canonical form for this
license. One wrinkle to note in passing rather than act on: `LICENSE.rst`'s third clause names "the
Astropy Team" as the entity whose name may not be used for endorsement — an artifact of the OpenAstronomy
packaging guide the project was derived from (`README.rst:14–17`). It does not change the license identity.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- spectropolarimetry
- stokes parameters
- polarimetry
- polarization
- photosphere
- magnetogram
- spectral inversion
- magnetic field
- solar physics

No keywords were stored previously. The nine above were chosen against the `Keyword` vocabulary, which is
the only open vocabulary in the form: seven (`polarimetry`, `polarization`, `photosphere`, `magnetogram`,
`spectral inversion`, `magnetic field`, `solar physics`) already existed and were reused verbatim so no
near-duplicate was minted; two (`spectropolarimetry`, `stokes parameters`) did not exist and are newly
minted terms. Both were checked against the existing entries first — the vocabulary contained
`spectral imaging`, `spectral inversion`, `spectrogram plots`, `spectrograms`, `spectrograph`,
`spectrometer` and `spectroscopy`, but nothing containing "spectropolarim" or "stokes". They are worth
creating: `spectropolarimetry` is the single term that most precisely names this software's domain, and
`stokes parameters` is the quantity its whole data model is organized around.

All entries are lower-case and one term per entry, as the field requires.

**Deliberately omitted, because the field is for keywords "not supported by other metadata fields":**
`sdo`, `solar dynamics observatory`, `hinode spacecraft` (existing rows, but the missions belong in
Field 32); `python`, `python 3`, `python package` (Field 13); `visualization`, `data visualization`,
`line plots`, `image processing` (Field 4); `sunpy`, `ndcube`, `wcs` (Field 30 and Field 4 respectively).
Recorded so a future refresh does not read their absence as an oversight.

---

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific

Nothing was stored previously. The only remote data source stokespy actually queries is the Joint Science
Operations Center, SDO's own mission archive, reached through sunpy's JSOC client:
`attrs.jsoc.Series('hmi.S_720s')`, `attrs.jsoc.Series('hmi.ME_720s_fd10')`,
`attrs.jsoc.Notify(user_email)`, `Fido.search`, `Fido.fetch` (`stokespy/instload.py:78–104`, `:216–242`).
`parse_folder`'s `repo` parameter defaults to `'JSOC'` (`:11–12`, `:35`). A mission-specific archive is
exactly what `Observatory/Mission-specific` denotes, and Field 17's instruction to cross-list the mission in
Related Observatory is honoured in Field 32 (Solar Dynamics Observatory). The controlled-vocabulary string
is `Observatory/Mission-specific`, with that exact capitalization and no space around the slash.

**Considered and not selected — `The Virtual Solar Observatory.`** (the live row name ends in a period).
`parse_folder` accepts `repo='VSO'`, which changes the local-filename tokenizer from splitting on `.` to
splitting on `_` (`stokespy/instload.py:36–38`). That is filename-syntax support for files a user already
downloaded, not a VSO query: no VSO client, `attrs.vso`, or VSO search appears anywhere in the package, and
`parse_folder` is not exported in `stokespy/__init__.py`'s public API. It is recorded rather than silently
dropped because it is a genuine, if thin, nod to VSO-sourced data — but a filename tokenizer is not a data
source, so VSO is not selected.

**Also considered and not selected:** `HTTP/HTTPS Directories` and `FTP/FTPS Directories`. The JSOC fetch
does move bytes over HTTP, but through the DRMS/JSOC protocol rather than a generic directory listing, and
classifying it generically would lose the mission-specific fact that matters. Hinode data is not downloaded
at all — `load_HinodeSP_stokes`'s docstring states "The data for Hinode must be downloaded independently
from the Hinode website" (`instload.py:326`), and the loader only walks a local directory tree
(`level1/YYYY/MM/DD/SP3D/<date>/*.fits`). Local-filesystem reading is not a Field 17 data source.

---

### 18. Input File Formats (RECOMMENDED)
- FITS

Nothing was stored previously. FITS is the only format stokespy reads, and it reads it through two distinct
paths: `astropy.io.fits.open()` for Hinode SP Level 1 and Level 2 files
(`stokespy/instload.py:345`, `:353`, `:403`) and `sunpy.map.Map(fname)` for HMI files, chosen deliberately
"since it provides the correct observer frame of reference" (`:132`, `:139`, `:286`). Format is asserted
explicitly at `:341` (`if file.endswith(".fits")`) and `:109`/`:247` (`ext='fits'`). No CDF, netCDF, HDF5,
ascii, csv, JSON, Zarr, or IDL save-file reader exists anywhere in the package — `cdflib`, `h5py`,
`netCDF4`, and `scipy.io` are absent from both the imports and `setup.cfg`'s `install_requires`.

---

### 19. Output File Formats (RECOMMENDED)
Not found — stokespy writes no data files.

Nothing was stored previously, and that is the correct state rather than a gap. This was verified
exhaustively across the three modules: there is no `open(..., 'w')`, no `writeto`, no
`to_fits`, no `savefig`, no `np.save`, and no `astropy.io` write call of any kind. Every output path
terminates in an interactive matplotlib figure (`plt.show()` at `plotting.py:140`, `:287`, `:382`, `:431`)
or in an in-memory `NDCube` subclass returned to the caller. The package is a reader, container, and viewer.

`Other` was considered as a placeholder and rejected: selecting it would falsely assert that some
unenumerated output format is supported. An explicit, documented emptiness is the accurate answer.

---

### 20. Operating System (RECOMMENDED)
- Linux
- Mac
- Windows

Nothing was stored previously. All three are demonstrated by the release-era CI matrix in
`azure-pipelines.yml:35–44`, which ran the test suite on `macos: py36`, `windows: py37`, and `linux: py38`,
and gated wheel/sdist publication on all three passing (`dependsOn: py36_test, py37_test, py38_test`).
`.circleci/config.yml` additionally builds and twine-checks the distribution on Linux.

**Considered and not selected — `Operating System Independent`.** It is arguably true (the package is pure
Python with `use_compiled_extensions: n`), but nothing in the project asserts it: PyPI's `classifiers` list
for stokespy 0.5.0 is *empty*, so there is no `Operating System :: OS Independent` trove classifier to point
to, and `setup.cfg` declares no classifiers either. Listing the three platforms the project actually tested
is better evidenced than inferring platform independence, and mixing both would be self-contradictory. Note
also that `OS Independent` is not a valid row name on this vocabulary — the only cross-platform value is
`Operating System Independent`, spelled in full.

---

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

Nothing was stored previously. stokespy is pure Python with no compiled component:
`.sunpy-template.yml:11` sets `use_compiled_extensions: n`; `MANIFEST.in`'s
`recursive-include stokespy *.pyx *.c *.pxd` and `recursive-include cextern *` lines match nothing in the
tree (there is no `cextern/` directory and no `.pyx`/`.c`/`.pxd` file); and the only artifact ever published
to PyPI is an sdist, with no architecture-specific wheel.

**Considered and not selected:** `x86-64` and `Apple Silicon arm64`. `azure-pipelines.yml` does declare
`CIBW_BUILD: cp36-* cp37-* cp38-*`, `CIBW_SKIP: "*-win32 *-manylinux1_i686"`, and
`targets: wheels_linux, wheels_macos, sdist` (`:6–7`, `:61–64`) — which looks like architecture-specific
wheel building. Those are unmodified OpenAstronomy template defaults for packages that *do* have compiled
extensions; this one does not, and no such wheel was ever produced. Recorded so a future agent reading the
`cibuildwheel` variables does not conclude the package is architecture-bound.

---

### 22. Related Phenomena (OPTIONAL)
Not found — no row in the controlled vocabulary applies.

Nothing was stored previously, and leaving it empty is a judgement, so the reasoning is recorded in full.
`Phenomena` is a **closed** vocabulary, and at extraction time it offered exactly these values:
`Coronal Heating`, `Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`,
`Solar Wind`, `X-ray emission`. Each was checked against what stokespy actually supports:

- The four coronal/heliospheric terms (`Coronal Heating`, `Coronal Mass Ejections`, `Solar Corona`,
  `Solar Wind`) are wrong by region: both implemented loaders serve photospheric diagnostics — HMI's
  Fe I 6173 Å line and its Milne-Eddington vector-field inversion, and Hinode SP's Fe I 630 nm pair. The
  package has no coronal or heliospheric data path (see Field 5).
- `Solar Flares` — nothing in the package detects, catalogues, or analyses flares; there is no event list,
  time-series capability (Field 4), or flare-specific data product.
- `Geomagnetic Storms` — no terrestrial or magnetospheric data of any kind.
- `X-ray emission` — the spectral range is visible/near-infrared photospheric lines; no X-ray instrument or
  waveband is supported. (Hinode's XRT has SPASE rows, but stokespy does not read XRT data — see Field 31.)

The phenomena stokespy *is* about — solar photospheric magnetism, spectropolarimetry, Stokes profiles,
magnetic field inversion — have no rows here. Per Field 22's own instruction, those belong in Keywords, the
open vocabulary, and that is where they are recorded (Field 16). Note in particular that this vocabulary
does not include `Coronal Holes`, which some older field snapshots wrongly listed; there is no near-miss
value to reach for.

---

### 23. Development Status (RECOMMENDED)
Inactive

Nothing was stored previously. `Inactive` is defined at repostatus.org as "Reached stable, usable state but
no longer actively developed; support provided as time allows," and stokespy matches both halves:

- *Reached a usable released state:* version 0.5.0 is published on PyPI, documentation is built and served
  on Read the Docs (`v0.5.0`, `stable`, `latest` all built), and `CHANGELOG.rst` announces a feature-complete
  first release.
- *No longer actively developed:* last commit and last push 2022-03-24; no tag, release, or commit since;
  issue #5 ("Don't give warning when user gives bad wavelength; fail instead," opened 2022-03-16) is still
  open and unaddressed; both forks are equally stale.

**Alternatives considered and rejected:**
- `Active` — contradicted by four years and four months with no commits.
- `WIP` — wrong on its face; WIP means "no stable, usable public release yet," and a PyPI release exists.
- `Abandoned` — reserved for projects abandoned *without* a stable release; 0.5.0 exists.
- `Unsupported` — would assert that the authors have ceased work and want a new maintainer. Nothing states
  that. There is no deprecation notice, no archived flag on the repository (GitHub reports
  `archived: false`), and no README banner. `Inactive` claims less and is defensible; if the authors later
  declare the project unsupported, this is the value to revisit.
- `Moved` — ruled out in Field 3; no fork or successor is newer.
- `Suspended` — would assert the authors intend to resume; no such statement exists.

The controlled-vocabulary name is the bare term `Inactive`; the repostatus.org wording quoted above
describes it but is not part of the value.

---

### 24. Documentation (RECOMMENDED)
https://stokespy.readthedocs.io/en/latest/

Nothing was stored previously. The Read the Docs project `stokespy` exists, is linked to
`https://github.com/NCAR/stokespy.git`, and reports this URL as its own `documentation` link; the page is
live. Configuration is in `.readthedocs.yml` (Sphinx v2 config, `docs/conf.py`), and the docs
tree provides installation instructions (`docs/installation.rst`, pip and development install), an
introduction, class guides, and an API reference — satisfying Field 24's "documentation link including
installation instructions."

**Alternative considered:** `https://stokespy.readthedocs.io/en/stable/`, which pins to the `v0.5.0` tag.
Because the `v0.5.0` tag *is* `HEAD` of `main`, `latest` and `stable` render the same content, so the choice
is cosmetic today; `latest` is used because it is the URL Read the Docs itself advertises as the project's
default. Should development ever resume, `stable` would become the more appropriate value.

---

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

The existing HSSI record had no funder. This is a genuine, well-evidenced addition, and it also explains the
empty award row discussed in Field 26.

**The repository documents no funding at all.** A full-text search of every file for `fund`, `grant`,
`award`, `acknowledg`, `NASA`, `NSF`, `NCAR`, `UCAR`, `HAO`, and `CSAC` found only repository-URL and
build-URL matches (`github.com/NCAR/stokespy`, `dev.azure.com/NCAR/stokespy`, `gdima@ucar.edu`) — no
acknowledgements section, no funding statement, and no grant number anywhere in the README, docs, or
package metadata. There is also no reference publication whose Acknowledgments could supply it (Field 14).
The funder is therefore established from two independent external sources, which agree.

**The funding is established from the award record itself.** ADS/SciX indexes the NASA proposal:

- Bibcode `2019hdee.prop...18E`
- Title: "SunPy support for multidimensional data and spectropolarimetric analysis"
- Principal Investigator: Egeland, Ricky — an author of this software
- Affiliation on the proposal: "University Corporation For Atmospheric Research (UCAR)"
- Venue: NASA Proposal ID 19-HDEE19_2-0018 (ROSES-2019 program element B.12, Heliophysics Data Environment
  Enhancements), year 2019
- Its abstract names this software explicitly: "To support solar spectropolarimetry in Python, we propose to
  develop StokesPy, a new SunPy affiliate package to manipulate and visualize Stokes profiles and compare
  them to inversion results."

The abstract also independently corroborates several other fields in this file, which is why it is worth
recording here in detail rather than merely citing: it names the exact data sources stokespy implements
("publicly-available Stokes parameters from SDO/HMI and Hinode SOT/SP and inversion results at the Joint
Science Operations Center (JSOC) and Community Spectro-polarimetric Analysis Center (CSAC) initiative,
respectively"), and it confirms that the package targeted inversion *results* rather than performing
inversions (Field 4).

**Independently confirmed by the principal investigator.** Egeland's CV lists in its **Grants & Awards**
section, verbatim:

> `NASA Heliophysics Data Environment Enhancement grant for "SunPy support for multidimensional data and
> spectropolarimetric analysis" ($50k; 2020)`

This is non-ADS confirmation from the PI himself of both the funder (NASA) and the award title, and the title
in his CV is character-for-character the same as the ADS record's. It also adds two facts ADS does not carry
and that are recorded in Field 26: the award value **$50k** and the award year **2020** — the proposal went
to ROSES-2019 and the award landed in 2020. (His CV writes the program name as "Heliophysics Data
Environment Enhancement", singular; NASA's own program element is "Heliophysics Data Environment
Enhancements (HDEE)". Same program.)

`National Aeronautics and Space Administration` is written out in full rather than as "NASA," per Field 25's
instruction to avoid acronyms; ROR `027ka1x80` was confirmed to be that organization (ROR display name
"National Aeronautics and Space Administration", acronym NASA), and it already exists as an HSSI
organization row with that exact name and ROR.

**Considered and not selected as funders:** *University Corporation for Atmospheric Research* and
*NSF National Center for Atmospheric Research* — these are the *recipient* institutions of the award and the
authors' employer, not the sponsor.

**Considered and rejected: the National Science Foundation, and specifically the NSF grant "Harnessing the
DKIST Data Revolution."** This one deserves recording because it is a genuine trap. The same CV Grants &
Awards section, immediately below the NASA entry, reads: "Awarded associate research position to develop a
pipeline and perform a validation of DKIST level-2 spectropolarimetric inversion data products for the solar
chromosphere as part of the NSF grant 'Harnessing the DKIST Data Revolution' (PI H. Uitenbroek, NSO;
2019–2020)." It is contemporaneous with stokespy, it is spectropolarimetric, and it matches the "DKIST
level-2 pipeline" half of his job description — so it looks like a plausible second funder. It is **not**
one: it funded DKIST level-2 pipeline and chromospheric validation work, and stokespy contains no DKIST
support and no chromospheric diagnostic whatsoever (Fields 5 and 31). The NASA HDEE grant is the award whose
stated deliverable is this software. NSF more broadly sponsors NCAR as a whole, but recording it here would
misattribute the software's funding.

---

### 26. Award Title (OPTIONAL)
- **Award Title:** SunPy support for multidimensional data and spectropolarimetric analysis
- **Award Number:** 19-HDEE19_2-0018

**Correction of the stored value.** HSSI held a single award row whose name was the empty string
(`award: [""]`). An empty award row conveys nothing and is not a value worth preserving; the real award is
identifiable and is recorded above.

The title is copied verbatim from the ADS record for `2019hdee.prop...18E` (see Field 25 for the full
evidence and the abstract that names StokesPy). It is 72 characters, comfortably inside the 128-character
limit on stored award names.

**Award value and year.** Egeland's CV records the award as `($50k; 2020)`. The proposal went to ROSES-2019
(hence the `19-` prefix on the proposal ID) and the award landed in **2020** at a value of **$50k**. Neither
fact is in ADS, and both are recorded here so a future refresh does not have to re-derive them. The award
year 2020 also explains a discrepancy that might otherwise look like an error: the proposal record is a 2019
record, but the money is a 2020 award.

**About the award number, and why the proposal ID is the right value.** `19-HDEE19_2-0018` is the NASA
*proposal* identifier, as recorded in ADS's publication field ("NASA Proposal ID. 19-HDEE19_2-0018") — it
decodes as ROSES-2019, program element HDEE19, step-2 proposal number 0018. The corresponding NASA *grant*
number (the `80NSSC…` form used on awards to UCAR) does not appear in any source consulted, including the
PI's own record of the award:

- **Absent from the PI's CV.** The Grants & Awards entry gives the program, the title, the value and the
  year — and no grant number. This carries particular weight: if the number were readily citable, the
  person who holds the award is the person most likely to have cited it.
- **Absent from acknowledgements.** ADS `ack:"19-HDEE19_2-0018"` returns zero hits, as does
  `ack:"StokesPy"`. A control query for a nonsense token also returned zero, and `full:"HDEE19"` returns one
  unrelated paper — so the searches were discriminating and the absence is real, not a tokenization
  artifact. In any case no stokespy publication exists whose Acknowledgments could carry it (Field 14).
- **Absent from the awarding agency's own published record.** NASA's HDEE 2019 selected-abstracts collection
  and its HDMC task list both carry this award but neither states a grant number — see the detail below.
  This is the most decisive of the absences listed here, because it is the sponsor's own document.
- **Absent from the repository** (Field 25) and from any DOI metadata (Field 2).

Taken together, `19-HDEE19_2-0018` is the best *publicly evidenced* identifier for this award, not merely
the best one that happened to turn up. **Do not substitute a guessed `80NSSC…` string.**

**The grant number is genuinely not in NASA's own two published pages for this award.** These were the
obvious remaining place to look, both were read in full, and neither carries it — so this line of enquiry is
closed and a future refresh should not re-open it. Both pages are on NASA's Heliophysics Digital Resource
Library host:

- `https://hdrl.gsfc.nasa.gov/HDEE19_Abstracts.pdf` — "Heliophysics Data Environment Enhancements Abstracts
  of Selected Proposals (NNH19ZDA001N-HDEE)", 12 pages. It carries this award's entry as
  `Ricky Egeland/University Corporation For Atmospheric Research (UCAR)` followed by the award title and the
  full abstract, matching the ADS record. It states that **15 proposals were received and 11 were selected
  for funding on 2019-10-19**. It contains **no** per-award grant number — no `80NSSC…`, `NNX…`, or
  `19-HDEE19_2-…` string appears anywhere in its text. The only NASA identifier it carries is the
  solicitation number, `NNH19ZDA001N-HDEE`, which covers all 11 selected proposals rather than this one.
- `https://hdrl.gsfc.nasa.gov/All_HDMC_Tasks_Jan_2021.html` — a Heliophysics Data Management and Coordination
  task list. Its entry for this work reads only `SunPy spectropolarimetry / Ricky Egeland / UCAR`; it does
  not name StokesPy and carries no grant number either.

The absence of a `80NSSC…` number is therefore established from the awarding agency's own published record,
not merely inferred from search misses. `19-HDEE19_2-0018` stands as the award identifier. **Do not
substitute a guessed `80NSSC…` string, and do not use the solicitation number `NNH19ZDA001N-HDEE` as the
Award Number** — it identifies the whole 2019 HDEE call, not this award.

Two facts worth keeping from that source because they resolve an apparent inconsistency: the award was
**selected 2019-10-19** against the ROSES-2019 call, which is why ADS files the record under year 2019,
while Egeland's CV lists it under 2020 — the year the funding was in hand. Both are correct, describing
different milestones of the same award.

**One durable access caveat about this host: its timeouts are transient.** `hdrl.gsfc.nasa.gov` can resolve
normally (169.154.154.68 / 2001:4d0:2418:121::68) and still refuse every HTTPS connection for a period —
failing alike on a plain fetch, with a browser user-agent, and through a real browser — and then serve the
same pages in under half a second a short time later. Treat a timeout here as **an outage worth simply
retrying**, not as evidence that the source is unreachable or that these pages need to be sourced some other
way.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
Not found.

Nothing was stored previously, and the emptiness is verified rather than assumed. No publication describes,
cites, or uses stokespy as far as the literature can be searched:

- ADS/SciX `full:"stokespy"` — which searches title, abstract, body text, keywords and acknowledgements of
  indexed records — returns exactly one hit, the 2019 NASA proposal `2019hdee.prop...18E`, which is the
  funding record (Fields 25–26), not a publication about or using the software. `abs:"StokesPy"` returns the
  same single record. A nonsense-token control returned zero hits.
- `ack:"StokesPy"` returns zero, so no indexed paper acknowledges the package.
- There is no reference publication to seed a citation graph from (Field 14), so no citation-graph search
  (Semantic Scholar, OpenAlex) has an entry point; and with no DOI (Field 2), there are no DataCite
  citation relations either.

**One presentation exists, and it is deliberately not a value here.** Egeland's CV lists, under
Presentations: `"StokesPy: An Introduction" Python in Heliophysics Spring 2020 Meeting, Virtual (May 2020)`.
It is excluded on two independent grounds. First, it is a **community meeting talk, not a publication** — it
was not peer reviewed, it does not describe the released software (it predates the repository by about a
year; see Field 10), and Field 27 asks for publications. Second, and decisively, **no citable artifact for
it could be found** — no archived slides, no video, no abstract, and no DOI. Three checks, so a future
refresh need not repeat them: PyHC's meeting index at `https://heliopython.org/meetings/` does not mention
stokespy anywhere; web searches for the talk surfaced no slides, recording, or abstract; and the CV itself
is telling on this point, because Egeland attaches a "video" hyperlink to several other entries in the same
Presentations list while the StokesPy entry carries none. Recording it would require manufacturing a
citation or an identifier, which is not acceptable. This also *refines* the negative research above rather than contradicting it: ADS indexes no
record of this talk, which is exactly what one expects of an unindexed community presentation, and is not a
sign the ADS searches were run badly.

This absence is consistent with the project's history: no release after 0.5.0, no SunPy affiliation, and no
recorded adoption. A future refresh should treat a genuinely new hit for `full:"stokespy"` as the trigger to
revisit this field, rather than re-running the same searches — and should not resurrect the May 2020 talk
unless an archived, citable artifact for it turns up.

---

### 28. Related Datasets (OPTIONAL)
- **Hinode-SpectroPolarimeter (SP) Level 1 (calibrated) full Stokes data** —
  https://doi.org/10.5065/d6t151qf
- **Hinode-SpectroPolarimeter (SP) Level 2 (vector magnetic field) spectral line inversions** —
  https://doi.org/10.5065/d6jh3j8d

Nothing was stored previously. These two DOIs are the exact data products stokespy's Hinode loaders read,
and both were resolved through DataCite:

- `10.5065/d6t151qf` — creator "Community Spectropolarimetric Analysis Center (CSAC)", publisher
  "NSF NCAR High Altitude Observatory", landing page `http://csac.hao.ucar.edu/sp_data.php`. Its abstract:
  "Calibrated full Stokes data from the Spectro-Polarimeter on board the Hinode satellite. Calibrated 3D data
  (spectral dimension x spatial dimension x 4 Stokes parameters) ready for scientific analysis. These data are
  stored as individual FITS files for each SP integration (slit position), grouped int[o]…". That is a precise
  description of what `load_HinodeSP_stokes()` consumes: it walks
  `level1/YYYY/MM/DD/SP3D/<date>/` collecting one FITS file per slit position, reads
  `SP_lvl1[0].data` of shape `(Nstokes, Ny, Nwav)` from each, and stacks them into a
  `(Nx, Nstokes, Ny, Nwav)` array (`stokespy/instload.py:337–360`).
- `10.5065/d6jh3j8d` — the Level 2 vector-magnetic-field inversions from the same CSAC collection. This is
  what `load_HinodeSP_magvec()` reads: a single per-scan FITS file at
  `level2/YYYY/MM/DD/SP3D/<date>/<date>.fits` from which it pulls the named extensions `Field_Strength`,
  `Field_Inclination` and `Field_Azimuth`, plus the X/Y coordinate tables at HDU indices 38 and 39
  (`stokespy/instload.py:386–424`).

The CSAC connection is corroborated by the funding proposal, which names CSAC as one of the two archives the
project would build against (Field 25), and by CSAC's location at HAO/NCAR — the same laboratory as the
authors (Field 6).

**Considered and not selected:** https://doi.org/10.5065/d6p848z8, "Hinode-SpectroPolarimeter (SP)
Level 1.5 (quick-look) physical quantities", the third DOI in the same CSAC collection. stokespy reads Level 1 and Level 2 only;
`load_HinodeSP_magvec()` goes to `level2/`, not to any Level 1.5 product, and no code path references it.
Recorded so a future refresh does not add the whole CSAC collection indiscriminately.

**Two further supported series are deliberately absent, because they are not citable.** stokespy's HMI
loaders read two specific JSOC data series, which are as much "datasets the software supports functionality
for" as the Hinode products:

- `hmi.S_720s` — HMI 720 s Level 1 Stokes series, read by `load_HMI_stokes()`
  (`stokespy/instload.py:99`, `:109`).
- `hmi.ME_720s_fd10` — HMI 720 s Milne-Eddington vector-magnetic-field inversion series, read by
  `load_HMI_magvec()` (`:237`, `:247`).

Neither has a DOI: DataCite returns zero results for `hmi.S_720s`, and no SPASE `NumericalData` record for
these series was found (`https://spase-metadata.org/NASA/NumericalData/SDO/HMI` resolves only to a generic
landing page with no series records, and `hpde.io` did not resolve). The only stable-looking link is JSOC's
own series browser, e.g. `http://jsoc.stanford.edu/ajax/lookdata.html?ds=hmi.S_720s`, which does resolve but
is a query into a browse UI rather than a citable dataset landing page.

They are excluded for a reason rooted in how this metadata is stored: a related dataset becomes a
`RelatedItem` row whose **`identifier` is the field that actually identifies and resolves the dataset**,
while `name` is only a short label. Listing these two series would put a browse-UI query string into that
identifier slot, where a citable dataset identifier belongs. Field 28 does permit an APA-style citation with
a permanent link when no DOI exists, so including them was possible; it was judged the wrong trade, because
it would buy a nominal entry at the cost of an identifier that does not identify anything.

The durable point, and the right way to think about it: **these two HMI series are genuinely supported but
not citable.** That is a fact about the JSOC series, not a gap in this record — and the association is not
lost, because SDO and HMI are captured in Fields 31–32. If JSOC or SPASE later mints identifiers for these
series, that is the change that would justify revisiting this.

---

### 29. Related Software (OPTIONAL)
- https://github.com/NCAR/stokespy_notebooks

Nothing was stored previously. `stokespy_notebooks` is the project's own companion repository of worked
examples, cited from the documentation as the primary usage tutorial: "A comprehensive `example notebook
<https://github.com/NCAR/stokespy_notebooks>`_ has been developed demonstrating loading StokesPy objects
from HMI and Hinode SOT/SP data files, using the slicing functions, and plotting the objects"
(`docs/introduction.rst:47–51`). GitHub confirms it exists under the same `NCAR` organization, described as
"Examples using the stokespy package to load and plot data." A companion package designed to be used with
this software is squarely within Field 29's scope, and this one is genuinely distinguishing — it is where a
prospective user would actually start.

**Considered and rejected — `dkist` (https://github.com/DKISTDC/dkist).** This is the strongest candidate
that was examined and turned down, so the reasoning is recorded to stop it being re-proposed. It is arguably
the closest thing to a similar-purpose tool: like stokespy it builds `NDCube`-based, coordinate-aware
containers for solar spectropolarimetric data, and DKIST is the instrument class stokespy's funding proposal
explicitly anticipated ("This addition to the SunPy ecosystem will be particularly timely as new
spectropolarimetric data products become available from DKIST"). It is rejected because stokespy's repository
contains no reference to the `dkist` package — the resemblance is an outside observer's reading of the two
codebases, and recording it would be an inference dressed as metadata. Should stokespy ever reference the
`dkist` package, that is the evidence that would change this.

**Considered and rejected:**
- `sunraster` (https://github.com/sunpy/sunraster) — also a SunPy-affiliated, NDCube-based container package,
  but for spectrograph raster observations rather than polarimetry. Structurally a sibling, functionally a
  different task; no repository evidence connects them.
- `pycelp` — a Python package for coronal emission line polarization, co-authored by Gabriel Dima
  (ADS `2021ascl.soft12001S`). Shares an author and the word "polarization," but it synthesizes coronal
  emission-line polarization from atomic physics, whereas stokespy is a container and viewer for
  photospheric observations. A shared author is not a software relationship. Recorded because the overlap is
  superficially tempting.
- `spectroflat` — a SunPy-affiliated package for spectropolarimetric flat-fielding. Adjacent domain, but it
  performs calibration, which stokespy explicitly does not do (Field 4); and again no repository evidence
  links them.
- `drms` — the JSOC/DRMS client library, and genuinely domain-specific rather than generic. Excluded because
  stokespy never imports it: it reaches JSOC only through `sunpy.net.Fido` and `attrs.jsoc`, so the
  relationship a reader should see is the one with sunpy (Field 30), not a transitive dependency stokespy
  does not name.
- `numpy`, `matplotlib`, `natsort` — direct dependencies (`setup.cfg` `install_requires`) but generic
  infrastructure. Arrays, plotting, and natural-order string sorting would be equally at home in a web
  application, a finance model, or a biology pipeline; listing them would say nothing that is not equally
  true of most Python packages. `natsort` merits explicit mention because it is the least familiar of the
  three and could be mistaken for something domain-specific — it is used only to sort downloaded filenames
  into scan order (`instload.py:29`, `:106`, `:244`).

---

### 30. Interoperable Software (OPTIONAL)
- **sunpy** — https://doi.org/10.5281/zenodo.591887
- **ndcube** — https://doi.org/10.5281/zenodo.5715150
- **astropy** — https://doi.org/10.5281/zenodo.4670728

**The sunpy entry is the identifier HSSI already held, retained because it is correct.** Field 30's stored
value was `https://doi.org/10.5281/zenodo.591887`; resolved through DataCite and Zenodo, it is the
**concept DOI** (all-versions DOI) for
"sunpy: A Core Package for Solar Physics", publisher Zenodo, creators Stuart J. Mumford, Nabil Freij,
David Stansby, Albert Y. Shih, Steven Christe, Jack Ireland and others; Zenodo confirms
`conceptrecid: 591887` and `conceptdoi: 10.5281/zenodo.591887`, currently resolving to sunpy v8.0.0. It is
therefore not a stray or mistaken identifier, and being a concept DOI rather than a version DOI is the
right granularity for "this software interoperates with sunpy."

sunpy also passes the relevance bar on specific, cited evidence rather than on dependency presence or
ecosystem membership:

- **Output of one is imported into the other.** `load_HMI_stokes()` and `load_HMI_magvec()` construct
  `sunpy.map.Map` objects from HMI FITS files and convert them into stokespy containers — taking the map's
  pixel data (`tmp_map.data`), its WCS header (`tmp_map.wcs.to_header()`), and, via that WCS, the observer
  frame that becomes `StokesCube.frame` (`stokespy/instload.py:139–180`, `:286–320`;
  `stokespy/stokespy.py:219–224`). The code comments state the reason for going through sunpy explicitly:
  "Use sunpy.map.Map to read HMI files since it provides the correct observer frame of reference"
  (`instload.py:132`).
- **Its network stack is used as the retrieval API.** `from sunpy.net import Fido, attrs` with
  `Fido.search`/`Fido.fetch` and `attrs.jsoc.*` (`instload.py:8`, `:78–104`, `:216–242`), and
  `sunpy.time.parse_time` for timestamp parsing (`:113`, `:251`). `setup.cfg` requires the networking extra
  specifically: `sunpy[net]>=3.0`.
- **The helioprojective frame the whole coordinate API operates in is sunpy's** (Field 4).

**ndcube is the strongest of the three entries**, and it was absent from the stored record: every stokespy
data class *is* an `ndcube.ndcube.NDCube` by inheritance — `StokesParamCube`, `StokesParamMap`, `StokesProfile`, `StokesCube`,
`MagVectorMap` and `MagVectorCube` all subclass it (`stokespy/stokespy.py:33`, `:100`, `:142`, `:165`,
`:577`, `:595`), so a stokespy object can be passed anywhere an NDCube is accepted and inherits NDCube's
coordinate-aware slicing. `docs/introduction.rst` states this as the design: "StokesPy data objects uses the
`ndcube` project's `ndcube.NDCube` object as a base class," and `docs/conf.py:80` wires ndcube into
intersphinx. A shared data model is the canonical form of demonstrated interoperability. The concept DOI
`10.5281/zenodo.5715150` was resolved through Zenodo for `sunpy/ndcube`.

**astropy qualifies as a Tier B entry**, on the specific public-API evidence that tier requires rather than
on dependency presence:

- The public constructor's documented interchange type is an astropy WCS: `StokesCube(data, wcs)` where
  `docs/introduction.rst` states "The provided ``wcs`` should be `APE-14 compliant`, which in practice
  generally means being a properly constructed `astropy.wcs.WCS` object," and the class docstring types the
  parameter as `astropy.wcs.wcsapi.BaseLowLevelWCS`/`BaseHighLevelWCS`
  (`stokespy/stokespy.py:175–177`, `:605–607`).
- The documented slicing API is expressed in astropy objects: `stokes.V_map(630.142 * u.nm)` takes an
  `astropy.units.Quantity` and `stokes.V_profile(SkyCoord(Tx=148*u.arcsec, Ty=67*u.arcsec, frame=...))`
  takes an `astropy.coordinates.SkyCoord` (`docs/stokes_classes.rst`), handled at
  `stokespy/stokespy.py:68–80` and `:478–497`; returned cubes carry `Quantity` values (`:342`, `:456`).
- `astropy.io.fits` HDULists are the read interface for Hinode data (`instload.py:345`, `:403`).

**All three entries are identified by a Zenodo concept DOI.** sunpy (`10.5281/zenodo.591887`), ndcube
(`10.5281/zenodo.5715150`) and astropy (`10.5281/zenodo.4670728`) each have a Zenodo *concept* DOI covering
all versions, which is the right granularity for "this software interoperates with X" — a version-specific
release DOI would go stale with every upstream release.

**A search trap that will mislead anyone re-deriving these DOIs.** Querying Zenodo for records *titled*
`astropy/astropy` returns zero hits, which looks like proof that astropy does not archive to Zenodo. It is
not. Astropy's Zenodo records are titled `astropy/astropy: v5.0`, `astropy/astropy: v6.0.0` and so on, and
from v6.1.0 onward simply `Astropy` — so an exact-title query matches none of them while many version
records sit under concept ID `4670728`. The reliable checks are to query by concept (`parent.id:4670728`)
or to read the project's own README badge: astropy's `README.rst` carries a Zenodo badge pointing at
`https://doi.org/10.5281/zenodo.4670728`. **Treat "zero exact-title hits on Zenodo" as an inconclusive
query, never as evidence a package has no DOI**, and confirm against the upstream project's own citation
badge. The same caution applies to any package whose Zenodo records are named `<org>/<repo>: <version>`,
which is the default for the GitHub–Zenodo integration.

**Two alternative identifiers for astropy were considered and rejected.** The Astropy Collaboration journal
articles (2013, 2018, 2022) are the project's canonical *literature* citations, but a paper DOI identifies a
paper, not the software this field is about. The repository URL `https://github.com/astropy/astropy` is
permitted by the field and would have resolved, but the concept DOI is the more durable and more specific
identifier and matches how sunpy and ndcube are recorded here — **prefer a concept DOI over a repository URL
whenever one exists.**

**Considered and rejected:**
- `numpy` and `matplotlib` — Tier A, always excluded. They are direct dependencies, but "it depends on
  numpy" and "it uses matplotlib for all plotting" are true of nearly every package in HSSI and distinguish
  nothing about stokespy.
- `natsort` — generic infrastructure by the "web app, finance model, or biology pipeline" test; used only
  for filename ordering.
- `gwcs`. `docs/introduction.rst` names it alongside astropy as an acceptable APE-14 WCS ("or a
  `gwcs.wcs.WCS`"), links its documentation, and `docs/conf.py:81` wires it into intersphinx — which is
  close to a documented interchange claim. Rejected because it is a statement about what APE-14 compliance
  means in general rather than a demonstrated exchange: those three documentation references are the *only*
  occurrences of gwcs in the repository. It is absent from `setup.cfg`'s dependencies and from every import
  statement in `stokespy/`, the single test does not use it, and no example constructs a stokespy object from
  a gwcs WCS. Recorded because the docs mention is a plausible trap for a future extraction.
- The blanket justifications "part of the standard scientific Python ecosystem" and "built on the SunPy
  stack, therefore interoperable with SunPy packages" — never sufficient on their own, and not relied on
  here. Each of the three entries above rests on a named code path or documented API contract.

---

### 31. Related Instruments (OPTIONAL)
- **HMI** — https://spase-metadata.org/SMWG/Instrument/SDO/HMI
- **Solar Optical Telescope** — https://spase-metadata.org/SMWG/Instrument/Hinode/SOT

Nothing was stored previously. Both entries carry an `https://spase-metadata.org/` identifier, both names
are copied verbatim from the matched vocabulary rows, and both resolved unambiguously.

**Relevance.** Both instruments pass the "designed to support" test decisively rather than marginally:
stokespy ships named loader functions for each, exported in its public API
(`stokespy/__init__.py:4`, `:11` — `load_HMI_stokes`, `load_HMI_magvec`, `load_HinodeSP_stokes`,
`load_HinodeSP_magvec`), and `CHANGELOG.rst`'s 0.5.0 feature list advertises them as release features. The
loaders encode instrument-specific knowledge, not generic FITS reading: the HMI loaders hard-code the
JSOC series names `hmi.S_720s` and `hmi.ME_720s_fd10`, HMI's Fe I 6173.345 Å central wavelength and
0.0688 Å dispersion, its six-position wavelength sampling (`reshape(4,6,…)`), and a `CROTA2`-based
derotation specific to HMI's roll (`instload.py:99`, `:145`, `:150–151`, `:237`, `:69`); the Hinode loaders
encode the SP archive's directory layout (`level1|level2/YYYY/MM/DD/SP3D/<date>`), its per-slit-position
file structure, its `XCEN`/`YCEN`/`XSCALE`/`YSCALE` header keywords, and the Level 2 extension names
`Field_Strength`/`Field_Inclination`/`Field_Azimuth` (`instload.py:338`, `:355–356`, `:371–374`, `:398`,
`:405–409`). A user searching HSSI for `instrument:"HMI"` should get this package back.

**Resolution details.**
- **HMI** — searching the vocabulary for the abbreviation `HMI`, for "helioseismic" in the name, and for
  `/HMI` in the identifier path yielded exactly one instrument row: `name: 'HMI'`,
  identifier `https://spase-metadata.org/SMWG/Instrument/SDO/HMI`. (The only other hit was Solar Orbiter's
  "Polarimetric and Helioseismic Imager" (PHI), a different instrument on a different platform, excluded by
  both its name and its identifier path.) One row, so ladder rule 1 applies; the row `name` is the bare
  abbreviation `HMI` and is recorded exactly as stored rather than expanded to "Helioseismic and Magnetic
  Imager." No `.html` duplicate exists for this row.
- **Solar Optical Telescope** — stokespy targets Hinode's **SP** (Spectro-Polarimeter), which is one of the
  focal-plane packages of the Solar Optical Telescope. The vocabulary has **no** row for the SP itself:
  searches for "spectro-polarimeter", "spectropolarimeter", "polarimeter", a bare `SP` name, and an `SP`
  abbreviation among instrument rows return nothing for Hinode (the only polarimeter-named hits are Pioneer
  Venus Orbiter's Cloud Photopolarimeter, PUNCH, and an IUGONET NAOJ full-disk instrument — all unrelated).
  The vocabulary does have `Solar Optical Telescope` at
  `https://spase-metadata.org/SMWG/Instrument/Hinode/SOT`, exactly one row, which is the instrument the SP
  belongs to and the level at which SPASE represents it. This is the correct resolution rather than a
  compromise: the repository itself names the target as "Hinode SOT/SP" (`CHANGELOG.rst:14`,
  `docs/introduction.rst:49–50`), so SOT is the software's own framing of what it supports.

**No ambiguity requiring manual resolution.** Neither entry produced a multi-row match, so no entry in
Fields 31–32 is unresolved: each carries a single, specific SPASE identifier rather than a
`NEEDS MANUAL RESOLUTION` placeholder or a bare name.

**Vocabulary guard.** Fields 31–32 are SPASE-only: every value must carry an
`https://spase-metadata.org/` identifier, and both entries above do. A candidate row that fails that test
signals upstream drift and must be reported rather than used. That the vocabulary satisfies the guard is a
property of it at a moment in time and not an invariant, so the check has to be repeated rather than
assumed.

**Considered and rejected:**
- **Atmospheric Imaging Assembly (AIA)** — rows exist
  (`https://spase-metadata.org/SMWG/Instrument/SDO/AIA` and an `.html` duplicate), and AIA is mentioned
  twice in the code, but neither mention is support. `parse_folder`'s docstring describes its `wave`
  parameter as "wavelength (primarily for AIA data)" and gives `aia.lev1_euv_12s` as an example `series`
  string (`instload.py:18`, `:20`) — yet `wave` is accepted and then **never used** in the function body
  (`:11–47`), so no AIA-specific behaviour exists. The second mention is a stale copy-paste comment,
  "Generate WCS for data cube using same WCS celestial information from AIA map" (`:153`), sitting above
  code that actually reads an HMI map's WCS. AIA data is not loaded, parsed, or processed anywhere. This is
  a docstring name-drop, which the relevance gate excludes.
- **Daniel K Inouye Solar Telescope (DKIST)** — rows exist
  (`https://spase-metadata.org/SMWG/Observatory/DKIST` and an `.html` duplicate, both type 2/observatory).
  DKIST was the motivating future target of the funded proposal ("particularly timely as new
  spectropolarimetric data products become available from DKIST in late 2019/early 2020"), and it is a
  plausible thing to expect here. But stokespy 0.5.0 contains **no** DKIST loader, no DKIST format or
  convention, and no mention of DKIST anywhere in the repository — the word does not appear in any file.
  The relevance gate excludes "platforms you *could* write a module for." Recorded prominently because the
  proposal abstract makes this the single most likely false addition in a future refresh.
- **SOLIS / VSM** — rows exist (`SMWG/Observatory/SOLIS`, `SMWG/Instrument/SOLIS/VSM`, plus FDP and ISS),
  and SOLIS/VSM would be a natural spectropolarimetric target, but SOLIS is not mentioned anywhere in the
  repository and no loader exists for it. Recorded because it was raised as a candidate before the code was
  examined and is not supported.
- **Hinode XRT and EIS** — rows exist under `SMWG/Instrument/Hinode/`. Only the SP/SOT optical
  spectropolarimetric path is implemented; no X-ray or EUV-spectrometer data is read, and neither
  instrument is mentioned in the repository.
- **JSOC** — the vocabulary's only `JSOC` matches are Cluster's Joint Science Operations Centre
  (`SMWG/Instrument/Cluster/JSOC`) and a CNES Cluster/JSOC model-data record, both entirely unrelated to
  SDO's Joint Science Operations Center. This is a name collision, not a match. SDO's JSOC is an archive and
  is recorded in Field 17 as `Observatory/Mission-specific`, which is where a data source belongs.
- **CSAC** — the Community Spectropolarimetric Analysis Center, whose Hinode SP products stokespy reads, has
  no row in the vocabulary at all (searches for "csac" and "spectro-polarimetric analysis" return nothing).
  It is a data centre rather than an instrument or observatory, so this is expected; the association is
  captured through the CSAC dataset DOIs in Field 28 instead.

---

### 32. Related Observatories (OPTIONAL)
- **Solar Dynamics Observatory** — https://spase-metadata.org/SMWG/Observatory/SDO
- **Hinode** — https://spase-metadata.org/SMWG/Observatory/Hinode

Nothing was stored previously. Both entries carry an `https://spase-metadata.org/` identifier and both
names are copied verbatim from the matched rows.

**Relevance.** These are the platforms carrying the two instruments stokespy is built to support, and the
package names them itself: the metadata dictionaries the loaders attach to every cube record
`'inst': 'SDO/HMI'` (`instload.py:175`, `:315`) and `'inst': 'Hinode/SP'` (`:377`, `:438`), and those strings
are rendered into plot titles (`stokespy.py:130–131`). Both missions are listed as supported targets in the
release notes and in the funded proposal. Both are therefore designed-to-support at the observatory level as
well as the instrument level, and Field 17's `Observatory/Mission-specific` selection is cross-listed here
as that field instructs.

**Resolution details.** Each resolved to exactly one type-2 row (ladder rule 1):
- `Solar Dynamics Observatory` — the sole observatory row matching `SDO` by name, abbreviation, or
  identifier path (`https://spase-metadata.org/SMWG/Observatory/SDO`). Note that the canonical row name is
  the expanded form, not the acronym the repository uses; it is recorded as stored.
- `Hinode` — the sole observatory row for the mission
  (`https://spase-metadata.org/SMWG/Observatory/Hinode`). Searches also covered the pre-launch name
  "Solar-B", which returned nothing, and the instrument-level Hinode rows (SOT, XRT, EIS), which are type 1
  and handled in Field 31. No `.html` duplicate exists for this row.

Both entries are unambiguous, so nothing in this field is flagged for manual resolution.

**Considered and rejected:** DKIST and SOLIS, both of which have observatory rows — see Field 31 for the
full reasoning. Neither is supported by any code in this repository.

---

### 33. Logo (OPTIONAL)
Not found — stokespy has no logo.

Nothing was stored previously, and there is nothing to find. The repository contains six images, all under
`docs/images/`, and every one is a screenshot of package output rather than an identity mark:
`StokesCube_plot.png`, `StokesParamCube_plot.png`, `StokesParamMap_plot1.png`, `StokesParamMap_plot2.png`,
`StokesProfile_plot.png`, `MagVectorMap_plot.png` — each referenced from the class-guide documentation as an
example figure. `docs/conf.py` sets no `html_logo` or `html_favicon`, and falls back to the default Sphinx
theme when the sunpy theme is unavailable (`:91`).

**Considered and rejected:** the "Powered by SunPy" shield at `README.rst:4–6`
(`http://img.shields.io/badge/powered%20by-SunPy-orange.svg?style=flat`). It is SunPy's badge, not
stokespy's logo, and using it would both misrepresent this package's identity and imply the SunPy
affiliation that never completed (Field 8).

**Registry check:** stokespy is absent from all three PyHC registry files, so there is no curated PyHC
`logo` entry to draw on either — see the note below.

---

## Cross-cutting negative research

Recorded once here rather than repeated per field, so a later refresh does not redo it.

**Reaching the sources this record depends on.** Three of them have access quirks that cost real effort to
work around, and every one of them will still be there for the next refresh:

- **ADS/SciX** is the source behind Fields 14, 25, 26 and 27, and its search API needs no personal API key:
  an anonymous bearer token from the accounts bootstrap endpoint is sufficient to run the `full:`, `abs:` and
  `ack:` queries recorded here. The interactive `ui.adsabs.harvard.edu` pages are client-rendered and yield
  nothing to a plain fetch, so a failed page fetch should not be mistaken for an absent record.
- **Egeland's CV** (Fields 6, 25, 26) is best fetched as
  `https://rickyegeland.github.io/cv/Ricky_Egeland_CV.pdf`. The widely-linked `rickyegeland.com` form of the
  same URL fails TLS validation over HTTPS, because that hostname serves a certificate valid only for
  `github.com` — so prefer the `github.io` route rather than working around the certificate error.
- **`hdrl.gsfc.nasa.gov`** — see Field 26. Its timeouts are transient: the host can resolve and still refuse
  every HTTPS connection for a period, then serve the same pages in a fraction of a second. Treat a timeout
  here as an outage to retry, not as a blocked or missing source.

**PyHC registry — stokespy is not registered.** All three registry files — `projects_core.yml`,
`projects.yml` and `projects_unevaluated.yml` — were read in full. Neither `stokespy` nor `StokesPy` appears
in any of them, by package name, by repository URL, or by description.

**Do not confuse the PyHC meeting talk with PyHC registration.** Egeland presented "StokesPy: An
Introduction" at the Python in Heliophysics Spring 2020 Meeting (Fields 10 and 27). Presenting at a PyHC
community meeting is not registration in the PyHC project registry, and the check above stands: stokespy is
in none of the three registry files. Nothing in this record should assert PyHC membership — just as nothing
should assert SunPy affiliation (Field 8). Both were community-facing aspirations that did not become
formal status. Other NCAR-originated software is registered (`GCMprocpy` in `projects.yml`, `NCAR-GLOW` in
`projects_unevaluated.yml`), so the registry does cover this institution — stokespy is simply not in it.
The only `stokes`-adjacent content is the `NDCube` entry, a dependency of stokespy registered in its own
right. Consequently no curated PyHC metadata —
description, logo, docs URL, keywords, or maturity ratings — was available for any field, and absence from
PyHC is not itself a defect. Development Status (Field 23) was therefore derived from repository activity
rather than from PyHC maturity ratings.

**No structured metadata files exist.** The repository has no `CITATION.cff`, `codemeta.json`,
`.zenodo.json`, `AUTHORS`, `CONTRIBUTORS`, or `CITATION` file at `830d1439`. Author, license and version
information therefore comes from `LICENSE.rst`, `README.rst`, `setup.cfg`, `.sunpy-template.yml`,
`CHANGELOG.rst`, `docs/conf.py`, git history, and PyPI — cross-checked against each other as noted per
field. A future refresh finding a newly added `CITATION.cff` should treat it as authoritative for Fields 6,
12 and 14.

**PyPI metadata is unusually sparse and should not be over-read.** stokespy 0.5.0's PyPI record has
`project_urls: null`, `classifiers: []`, `requires_dist: null`, `keywords: ''`, `home_page: ''`, and
`docs_url: null` — because `setup.cfg` declares `url =` empty and no classifiers, and because the sdist was
built without dependency metadata. The empty `requires_dist` in particular does **not** mean the package has
no dependencies; `setup.cfg`'s `install_requires` (ndcube>=2.0, sunpy[net]>=3.0, astropy>=4.2, numpy>=1.16,
matplotlib>=3.4, natsort>=6.0) is the authoritative dependency list and is what Fields 29–30 were assessed
against.
