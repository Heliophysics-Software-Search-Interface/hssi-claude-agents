# HSSI Metadata Extraction Results

**HSSI Software ID:** 54da66af-5ce4-4975-8560-258824988821
**Repository:** https://www.lmsal.com/solarsoft/
**Source Revision:** Not applicable — SolarSoft has no version control, tags, or releases. See the source-currency note below.
**Extraction Date:** 2026-08-11
**Validation Date:** 2026-08-23
**Validation Status:** PASS

## Scope note — how to read the evidence in this file

SolarSoft (SolarSoftWare, SSW) is **not distributed through version control.** It is a rolling
source tree, rsync/wget/curl-mirrored from a master host, that users install once and then refresh
in place with `ssw_upgrade`. There is therefore no commit SHA, tag, or release that can stand as
this record's source revision, and none should ever be invented for it. Evidence in this dossier is
drawn from the live tree and the official project pages, and the observations are dated so a future
agent can tell drift from disagreement.

**Sources consulted, and what each is good for:**

| Source | Role |
|---|---|
| `https://www.lmsal.com/solarsoft/` | Official project home and SSW installation form; the authoritative enumeration of supported missions, instruments and packages as offered to users. Carries an in-page revision history ending 2023-06-28 (`add so/solohi`). |
| `https://sohoftp.nascom.nasa.gov/solarsoft/` | **Master distribution host** and the most complete browsable source tree. Named as the "Installation Source" in the official install form. Serves the canonical *SolarSoft — Description* document (its own last revision 1999-10-14), which is the origin of this record's Field 8 text. Mirrored identically at `https://soho.nascom.nasa.gov/solarsoft/` and `https://sohowww.nascom.nasa.gov/solarsoft/`. |
| `https://hesperia.gsfc.nasa.gov/ssw/` | Browsable mirror at NASA GSFC. Useful and current for the branches it carries, but **incomplete** — as observed on 2026-08-11 it lacked the `so/` (Solar Orbiter) and `psp/` (Parker Solar Probe) branches that the master serves, and its `radio/` branch carried only `ethz`, `gen`, `norh`, `nrh` and `ovsa`, lacking `eovsa`, `fhnw`, `lofar`, `mwa` and `norp`. Prefer the master for completeness questions. |
| `https://hesperia.gsfc.nasa.gov/ssw/LICENSE` | The distribution's licence file (see Field 15). |
| `github.com/lmco/SolarSoft` @ `45ad0200eabf50ea1cadc40bf4f20658272f74e6` (2024-09-11) | A **partial, third-party-hosted GitHub snapshot** of the `gen/` branch only. Cited in this dossier for routine-level code evidence, and labelled wherever it is cited. It is **not** SolarSoft's distribution and its commit is **not** SolarSoft's revision — see Field 3 for why it was rejected as the code repository. |

**Source-currency evidence observed 2026-08-11.** The master tree regenerates a machine-written
stamp at `gen/setup/ssw_info_map.dat`; on the master it read `UT Time : 12-AUG-26 02:02:46`
(user `freeland`, host `gs671-penumbra.nascom.nasa.gov`, IDL 8.8.3, linux/x86_64) and on the
hesperia mirror `UT Time : 11-AUG-26 05:02:08`, i.e. the tree is refreshed daily. Because directory
mtimes track that sync rather than real editing, the meaningful currency evidence is the preserved
file mtimes: `gen/setup/setup.ssw_env` 2026-05-29, `gen/idl/ssw_system/go_update_ssw.pro`
2026-02-10, `gen/idl/wcs/` 2026-06-01, `gen/idl/display/` 2026-05-26, `so/stix/` 2026-07-13,
`punch/idl/` 2026-05-29 (its files 2026-05-15), `asos/lst/idl/` 2026-05-05. SolarSoft is under
active development.

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Source note:* This record already exists in HSSI; the original submitter is not identified by the
view API. Placeholder retained.

---

### 2. Persistent Identifier (RECOMMENDED)

**Value:** `https://ascl.net/1208.013`

*Source note:* SolarSoft is registered in the Astrophysics Source Code Library as
**`ascl:1208.013`** — "SolarSoft: Programming and data analysis environment for solar physics",
credited to Freeland, S. L. and Handy, B. N., ADS bibcode `2012ascl.soft08013F`. The ASCL record's
own "Code site" field reads `https://www.lmsal.com/solarsoft/` and its "Described in" field points
at `1998SoPh..182..497F`, so it independently corroborates Fields 3 and 14 of this record as well.

**This is an ASCL identifier rather than a DataCite DOI, and the practical consequence is smaller
than it looks.** HSSI's `persistent_identifier` is a plain `URLField` (max_length 200) validated only
by a generic `URLValidator` accepting http/https/ftp/ftps, plus a length check. **There is no
DOI-specific validation at the write layer**, so `https://ascl.net/1208.013` — a valid https URL of
24 characters — stores without error. The DOI expectation belongs to the submission form's *autofill
convenience*, which uses a supplied DOI to pre-populate other fields from DataCite; a non-DOI value
simply enriches nothing. That distinction matters: a future agent should not remove this value on the
theory that it will be rejected, because it will not be. Recording it is a judgement that a real,
citable, globally unique software identifier is more useful to an HSSI reader than an empty field; a
user who prefers Field 2 to hold only DOIs can empty it, but should not substitute something else.

*Considered and rejected:* a Zenodo or other DataCite DOI. Searches of the official project pages,
the master distribution tree, and DataCite found no DOI minted for SolarSoft itself, which is
consistent with a project that has no releases to mint one against. The reference publication's DOI
(`10.1023/A:1005038224881`) identifies the *paper*, not the software, and belongs in Field 14 —
it must not be copied here.

---

### 3. Code Repository (MANDATORY)

**Value:** `https://www.lmsal.com/solarsoft/`

*Source note:* **Retained from the existing HSSI record, and independently corroborated.** SolarSoft
has no source repository in the version-control sense; a project/distribution website is the correct
Field 3 value in that situation. Three independent grounds support this specific URL:

1. The ASCL record `ascl:1208.013` lists exactly `https://www.lmsal.com/solarsoft/` as SolarSoft's
   **Code site** — a third-party, curated identification of where SolarSoft's code lives.
2. The canonical *SolarSoft — Description* document served from the master distribution host names
   `http://www.lmsal.com/solarsoft/` as the project home in its header.
3. It is the live SSW installation form: a new SolarSoft installation is created by submitting this
   page, which generates a customised C-shell script or Windows ZIP package, and the page is
   maintained by the system's architect (S. L. Freeland). (The form is not the *only* route into the
   tree — the page itself notes that an existing installation can add branches with `ssw_upgrade`
   without returning to the form, and Bill Thompson's wget instructions are an alternative transfer
   path — but it is the entry point the project puts in front of new users.)

*Rejected alternative — `https://github.com/lmco/SolarSoft`.* This is the one credible Git candidate
(Lockheed Martin Corporation's official GitHub organisation, language IDL, and its GitHub
description is recognisably this record's concise description — the same core sentence, framed as a
noun phrase: "A set of integrated software libraries, data bases, and system utilities which provide
a common programming and data analysis environment for Solar Physics", without the leading "The
SolarSoft system is" and without a trailing period). It was rejected
because it is a partial and frozen snapshot rather than the maintained distribution:

- two commits only, both 2024-09-11 (`7db4337` "first commit", `45ad020` "Initial /gen directory
  commit"); repository created 2024-09-06, last pushed 2024-12-13;
- it contains **only** the `gen/` branch — none of the ~20 mission/instrument branches and no
  `packages/` — and even within `gen/` it lacks `dll/` and `idl_mods/`, which the live tree carries;
- zero tags and zero releases, and no `LICENSE` at the repository root;
- its open issues are automated repository-hygiene tickets, not SSW development;
- it is roughly twenty months behind a tree whose `gen/setup/setup.ssw_env` was edited 2026-05-29
  and whose `so/stix/` branch was edited 2026-07-13;
- a text search across the official SolarSoft pages (`lmsal.com/solarsoft/`, `ssw_install_howto.html`,
  `ssw_upgrades.html`, `ssw_packages_info.html`) and the master description document found no link to
  it; the single GitHub reference found anywhere in those pages was to an unrelated third-party
  package (`github.com/Gelu-Nita/GSFIT`).

Recording it as Field 3 would point HSSI users at a partial fork frozen in 2024 instead of the tree
they actually install from. **A future agent that rediscovers `lmco/SolarSoft` should not re-propose
it without first checking whether it has begun tracking the full tree; as of 2026-08-11 it had not.**

*Rejected alternative — `https://github.com/sswidl/ssw`.* Titled "SolarSoft" but effectively empty
(~2 KB, created and abandoned 2015-12-18, no code).

*Considered, and worth knowing about — `https://sohoftp.nascom.nasa.gov/solarsoft/`.* This is the
master distribution host and the fullest browsable rendering of the actual source tree, and it is a
genuinely arguable Field 3 value under the form's wording ("where the un-compiled, human readable
code ... is located"). It was not selected because its root URL serves the description document
rather than a directory index, because the project's own pages and the ASCL record both designate
the LMSAL page as the front door, and because the LMSAL form is what a new user actually needs. It
is recorded in Field 24's note so the browsable tree is not lost to a future reader.

---

### 4. Software Functionality (MANDATORY)

**Values (36):**

- Coordinate Transforms
- Coordinate Transforms: Solar
- Coordinate Transforms: Heliospheric
- Coordinate Transforms: Mission-Specific
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Spectrogram
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Wavelet Analysis
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 3D Graphics
- Data Visualization: Line Plots
- Data Visualization: Movies
- Data Visualization: Orbit Plots
- Data Visualization: Spectrogram
- Data Visualization: Web-Based
- Mission-related
- Mission-related: Analysis
- Mission-related: Calibration
- Mission-related: Science Data Processing
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: Field-line Tracing
- Models and Simulations: Forward-Fitting
- Models and Simulations: Instrument Response
- Servers and Environments
- Servers and Environments: Data servers processing and handling
- Servers and Environments: Distribution/Access

*Source note:* The existing HSSI record carried the single value `Data Processing and Analysis`,
which is true but describes a small fraction of what SSW is. Every value above is backed by named
routines or directories; all six parent categories are present for their children. Code paths cited
are from the `gen/` library (read in the 2024 `lmco/SolarSoft` snapshot and cross-checked against
the live master tree) unless a mission or package branch is named.

**Coordinate Transforms.** `gen/idl/wcs/` implements the full FITS World Coordinate System machinery
with an explicit conversion layer (`wcs/conversion/wcs_conv_hpc_hcc.pro`, `wcs_conv_hcc_hg.pro`,
`wcs_conv_hg_cr.pro`, `wcs_conv_hpc_hpr.pro`, …), and `gen/idl/solar/` carries the classical SSW
converters (`hel2arcmin`, `arcsec2helio`, `conv_a2h`, `conv_h2p`, `xy2hel`, `tim2carr`, `carr2xy`,
`rot_xy`, `drot_map`). *Solar* covers helioprojective/heliocentric/heliographic/Carrington
conversion. *Heliospheric* covers the vantage-point-aware ephemeris and conversion work needed when
the observer is not at Earth (`pb0r_solo.pro`, `pb0r_stereo.pro`, `sol_dist`, `oneau`, and the
`sunspice` package). *Mission-Specific* covers spacecraft attitude/pointing frames: the `sunspice`
package wraps NAIF SPICE kernels for the solar missions, and `gen/idl/sunglobe/` builds
spacecraft-frame pointing and field-of-view geometry (`sunglobe_get_sc_point.pro`,
`sunglobe_adjust_pointing.pro`, `sunglobe_get_ins_offset.pro`).

**Data Processing and Analysis.** *Calibration* — instrument `_prep` reduction is SSW's signature
contribution, together with `gen/idl/clients/prepserver/` (`prep_data.pro`, `prep_file.pro`,
`prep_server.pro`) and radiometric routines such as `darklimb_correct.pro` and
`gen/idl/synoptic/goes/goes_chianti_tem.pro`. *Data Access and Retrieval* — `gen/idl/clients/vso/`
(VSO), `gen/idl/clients/hv/` (Helioviewer), `gen/idl/clients/soar/` (Solar Orbiter Archive), the
`vobs/ontology` library for JSOC and HEK/HCR communication, and `gen/idl/sockets/` (73 `sock_*`
routines in a 102-routine directory). *Data Reduction* — `array_despike.pro`, `avg_wo_cr.pro`, `downsample.pro`, `binup.pro`,
`data_compress.pro`, `goes_deglitch.pro`. *Energy Spectra* — `gen/idl/spectra/` (`get_edges.pro`,
`edge_products.pro`, `energy_res.pro`, `mewe_spec.pro`, `get_ionbal.pro`) plus the `spex` package.
*File Format Conversion* — `fits2map`, `map2gif`, `fits2gif`, `fits2png`, `fits2tiff`, `jpeg2map`,
`gif2jpg24`, `genx2html`. *Image Processing* — `gen/idl/image/` (`cross_corr.pro`,
`align_cube_correl.pro`, `auto_align_images.pro`, `affine.pro`, `fft_crosscorr.pro`,
`cir_mask.pro`), plus the `desat` and `euvdeconpak` packages. *Spectrogram* —
`gen/idl/objects/make_spectrogram.pro` constructs a spectrogram object. *Time Series Analysis* —
`gen/idl/utplot/` and `gen/idl/time/` are among SSW's oldest and most-used libraries, and the
description document names "Time series analysis, time conversions, UTPLOT (millennium safe)" as a
primary capability. *Wavelet Analysis* — `gen/idl/image/vis/vis_wv.pro` and `vis_wv_fiwt.pro`
implement wavelet-based visibility imaging (used for RHESSI/STIX reconstruction). *Analysis* and
*Processing* cover the broad scientific and pipeline work that does not fall under a narrower child.

**Data Visualization.** *2D Graphics* — `gen/idl/display/` (~210 routines: `exptv`, `contv`,
`plot_image`, `plot_map`, colour-table management). *3D Graphics* — `gen/idl/sunglobe/` is an IDL
object-graphics 3D Sun ("Purpose: 3D Sun pointing tool"), and the `s3drs` package does 3D
reconstruction. *Line Plots* — `gen/idl/utplot/` (`utplot`, `outplot`, `eutplot`) and
`plot_goes.pro`. *Movies* — the description document lists image-cube movie display as a core
capability; `event_movie.pro`, `mk_mpeg.pro`, `gifs2mpeg.pro`, `mk_agif.pro`, `image2movie.pro`,
`ssw_ffmpeg.pro`, `jsmovie.pro`, `plotman__movie.pro`. *Orbit Plots* —
`gen/idl/sunglobe/sunglobe_orbit__define.pro` ("Object graphics for orbit trace in SUNGLOBE ...
showing the subspacecraft point on the solar surface for several time steps"). *Spectrogram* —
`plotman` displays spectrogram panels (`plotman__specoptions_widget.pro`, `plotman__spec_integr.pro`).
*Web-Based* — `gen/idl/http/` generates HTML, thumbnails and JavaScript movie pages, and
`idl_server_command.pro`/`idl_server_control.pro` implement the "WWW Client ↔ SolarSoft IDL server
interface [that] permits execution of SSW/IDL utilities over the Web" named in the description.

**Mission-related.** SSW is not only a general-purpose library; parts of it are mission ground
software. The `iris/` branch of the live tree carries `gse/` and `ops/` directories, `hessi/` carries
`offline/`, and the instrument `_prep` calibration code is contributed and maintained by the
instrument teams themselves. *Calibration*, *Analysis* and *Science Data Processing* follow directly.
*Mission-related: Distribution/Access* was considered and placed under Servers and Environments
instead, because SSW's distribution machinery serves the software itself rather than mission data.

**Models and Simulations.** *Empirical* — `diff_rot.pro`, `dr_carr.pro`, `dr_photo.pro` implement
empirical solar differential-rotation laws; `get_sun.pro`/`pb0r.pro` are solar ephemeris models.
*Field-line Tracing* — the `pfss` package performs potential-field source-surface extrapolation and
traces field lines through the extrapolated field; `nlfff` is also distributed. *Forward-Fitting* —
`gen/idl/fitting/` (`cfit.pro`, `cfit_block.pro`, `fit_spec.pro`, `ezfit.pro`, `fitter.pro`) and the
`spex` package fit forward-modelled photon spectra; the `forward` and `gx_simulator` packages
forward-model coronal observables. *Instrument Response* — response tables and calculators are
shipped throughout (`gen/idl/synoptic/goes/goes_chianti_resp_*.fits`,
`goes_chianti_use_resp_table.pro`, and `response/` directories in the `iris/`, `hic/` and `punch/`
branches).

**Servers and Environments.** *Data servers processing and handling* — `prep_server.pro`,
`prep_service.pro`, `ssw_server.pro`, `goes_server.pro`, `sock_service.pro`, `vso_server.pro`,
`hv_server.pro`, and an XDR/RPC server stack in `gen/idl/clients/rpc/`. *Distribution/Access* — the
install/upgrade system is a first-class part of the product (`ssw_install.pro`, `ssw_upgrade.pro`,
`ssw_wget_mirror.pro`, `ssw_lftp_mirror.pro`, `make_ssw_mirror.pro`, `go_update_ssw.pro`), which is
what makes SSW a distributed environment rather than a library. The top-level category is warranted
on its own by the system's stated purpose: "a common programming and data analysis environment for
Solar Physics".

*Considered and not selected:*
- *Servers and Environments: Software or Environment Container* — no Dockerfile or container
  definition was found in the distribution. A 2022 AGU abstract (`2022AGUFMSH52A..69A`, Antunes,
  "Pushing SolarSoft (SSW) into an IDL Jupyter Cloud Framework") describes containerised SSW work,
  but that is not shipped in the tree. Re-check if a container definition appears.
- *Servers and Environments: High Performance Computing* — `ssw_make_jobs.pro`,
  `ssw_make_jobs_pool.pro` and `go_ssw_batch.pro` provide batch job pooling, which is job management
  rather than HPC; no MPI, no scheduler integration, no parallel numerics were found.
- *Data Processing and Analysis: 2D Slices* — `plotman__profiles.pro` extracts 1D profiles from
  images, not 2D planes from 3D volumes.
- *Data Processing and Analysis: Packet Decommutation*, *Plasma Moments*, *Pitch Angle
  Distributions*, *3D Particle Distribution Processing*, *Curlometer*, *Linear Gradient Estimation*,
  *Magnetic Null Finding*, *Data Assimilation*, *ML/AI* — no supporting code found. SSW's in-situ
  support (STEREO PLASTIC/IMPACT) is read/plot-level rather than moment computation.
- *Data Visualization: Mission-Specific* — plausible, since several mission branches carry
  instrument-specific display code, but the branch-level code was not read routine-by-routine and
  the claim was left unmade rather than asserted from directory names.

---

### 5. Related Region (MANDATORY)

**Values:** Solar Environment; Photosphere; Chromosphere; Corona; Solar Wind; Interplanetary Space

*Source note:* `Solar Environment` is carried over from the existing HSSI record and retained. The
five additions are more specific and reflect the observational domains SSW's instrument branches
actually serve:

- **Photosphere** — magnetograph and continuum support (SOHO/MDI, SDO/HMI, Hinode/SOT, ASO-S/FMG),
  active-region utilities (`get_nar.pro`, `decode_nar.pro`, `oplot_nar.pro`), limb fitting and
  limb-darkening correction (`darklimb_correct.pro`, `find_limb2.pro`, `ssw_limbstuff`).
- **Chromosphere** — IRIS, SOHO/SUMER, and the ground-based Hα branches (`optical/soon`,
  `optical/mees`, `optical/lapalma`).
- **Corona** — the dominant domain: EIT, AIA, TRACE, SXT, XRT, EIS, CDS, the coronagraphs
  (LASCO, UVCS, SECCHI COR1/COR2), and the DEM package family (`vdem`, `demreg`,
  `simple_reg_dem`, `dem_sites`).
- **Solar Wind** — STEREO PLASTIC and IMPACT in-situ support, ACE and Wind index retrieval
  (`read_ace.pro`, `get_acedata.pro`, `ssw_get_winddata.pro`), and the PUNCH branch, whose science
  is precisely the corona-to-solar-wind transition.
- **Interplanetary Space** — heliospheric imaging: LASCO, SMEI, STEREO HI-1/HI-2, PSP/WISPR,
  Solar Orbiter SoloHI, and CME propagation tooling (`cactus`, `cmes`, `syndyne.pro`).

*Considered and not selected:* **Solar Interior** — SSW distributes support for HMI and MDI, whose
helioseismic products probe the interior, but the SSW-side code found is magnetogram/intensitygram
handling rather than helioseismic inversion, so the claim was not made. **Earth Magnetosphere** —
`ssw_getdst.pro`, `ssw_kyoto2dst.pro`, `ssw_getapkp.pro` and `get_swpc.pro` retrieve geomagnetic
indices, but as ancillary correlation data for solar events rather than as support for
magnetospheric science; the geomagnetic aspect is captured in Field 22 instead.

---

### 6. Authors (MANDATORY)

**Author 1 — S. L. Freeland**
- Identifier: Not found
- Affiliation: Lockheed Martin Solar and Astrophysics Laboratory (no ROR identifier — see below)

**Author 2 — SolarSoft development team**
- Identifier: Not found
- Affiliation: Lockheed Martin Solar and Astrophysics Laboratory

**Author 3 — B. N. Handy**
- Identifier: Not found
- Affiliation: Montana State University (https://ror.org/02w0trx84)

**Author 4 — Dominic M. Zarro**
- Identifier: Not found
- Affiliation: Adnet Systems (United States) (https://ror.org/05we1n045)

**Author 5 — William T. Thompson**
- Identifier: Not found
- Affiliation: Goddard Space Flight Center (https://ror.org/0171mag52)

**Author 6 — Richard A. Schwartz**
- Identifier: Not found
- Affiliation: Goddard Space Flight Center (https://ror.org/0171mag52)

**Author 7 — Kim Tolbert**
- Identifier: Not found
- Affiliation: Goddard Space Flight Center (https://ror.org/0171mag52)

*Source note — reconciliation.* Authors 1 and 2 are carried over unchanged from the existing HSSI
record; nothing recorded there was dropped. Authors 3–7 are additions, each with primary-source
evidence:

- **B. N. Handy** — the ASCL record `ascl:1208.013` credits the *software* to "Freeland, S. L.;
  Handy, B. N.", and he is co-author of the reference publication. The Montana State affiliation is
  the one both ADS and the publisher's own landing page record for him on `1998SoPh..182..497F`
  ("Department of Physics, Montana State University–Bozeman, Bozeman, MT, 59717, U.S.A."). This is a
  historical affiliation, correct for the era of the credit.
- **Dominic M. Zarro** — named in SolarSoft's own description document: "Application for overlay,
  alignment, scaling, rotation, etc of any SSW instruments via **Dominic Zarro's Mapping software**".
  He is the author of `gen/idl/maps/` (the map object that most SSW analysis is built on), of much
  of `gen/idl/objects/` and `gen/idl/sockets/`, and of `ssw_last_update.pro` and `goes_sat.pro`. His
  routine headers span three institutional attributions over three decades — "Dominic Zarro (ARC)",
  "(GSFC/SDAC)", "(L-3Com/GSFC)", "(LAC/GSFC)", "(ADNET)" — with a contact address of
  `dzarro@solar.stanford.edu`. The most recent attributions are ADNET, so that is what is recorded;
  the historical variants are noted here so a future agent does not read the discrepancy as an error.
- **William T. Thompson** — the most prolific single contributor to `gen/idl` by routine-header
  count, and the author of coherent subsystems rather than scattered utilities: the
  `gen/idl/wcs/` World Coordinate System package — where all 35 IDL routines in the directory carry
  his name in their headers — plus `gen/idl/sunglobe/`, the `sunspice` package, and the Solar Orbiter
  Archive client. He is also named on the official install page, which links to
  "Bill Thompson's wget transition help" at the STEREO Science Center.
- **Richard A. Schwartz** — author of the `spex`/OSPEX spectral-fitting lineage and of much of the
  GOES X-ray calibration chain; his initials appear as the maintainer in `clean_goes.pro`
  ("1-Jun-2020, RAS, for GOES16 and higher…") and his name in `gen/idl/fitting/` headers.
- **Kim Tolbert** — author and long-term maintainer of `gen/idl/synoptic/goes/` (the GOES object,
  `gfits_*`, `goes_3hour*`, `get_goes*`) and a principal author of `gen/idl/plotman/`.

*Deliberately not listed, and why.* SolarSoft's description states that the system "is built from
Yohkoh, SOHO, SDAC and Astronomy libraries and draws upon contributions from many members of those
projects". Two categories of name therefore appear in routine headers without being SolarSoft
authors, and a future agent should not add them:

- **Authors of third-party libraries that SSW redistributes** — W. Landsman, F. Varosi,
  M. R. Greason and D. Lindler (IDL Astronomy User's Library), C. B. Markwardt (MPFIT),
  Fanning Software Consulting (Coyote), B. C. Kelly. SSW vendors their code; it does not author it.
  The IDL Astronomy User's Library is recorded in Field 29 instead, which is where that relationship
  belongs.
- **K. Dere** — named in SolarSoft's description ("the Chianti Package, K. Dere et al. is now fully
  integrated into the SSW distribution"), but as the author of an *external* package that SSW
  integrates. CHIANTI is recorded in Field 29, not here.

*Further substantial contributors, documented as candidates rather than recorded.* Header analysis
of the `gen/` snapshot also shows large, coherent contributions from **Mons Morrison** (Yohkoh-era
foundations), **Stein Vidar Hagfors Haugan** (University of Oslo; `gen/idl/fitting/` CFIT family),
**Liyun Wang** (`image_tool`), **C. D. Pike** (Rutherford Appleton Laboratory; CDS-era utilities)
and **Nariaki Nitta**. They are not recorded because the list above is intended to capture the
system's architects and principal library authors, not to approximate a contributor census that a
consortium project of this size cannot support. Adding any of them would be defensible; a future
agent proposing one should say which subsystem the person authored.

*Negative research on identifiers.* ORCID's public search was queried for each recorded person
(by family name, by family + given name, and by affiliation-scoped variants), and for the reference
publication's DOI. No ORCID could be matched to any of them. This is unsurprising for researchers
whose principal work predates ORCID; recording `Not found` is the correct outcome, and a future
agent should not attach a same-surname ORCID belonging to a different person.

*Publication-time affiliations, and why they did not change what is recorded.* The publisher of the
reference publication states 1998 affiliations for both of its authors: Freeland at "Lockheed-Martin
Palo Alto Advanced Technology Center, Palo Alto, CA, 94303, U.S.A." and Handy at "Department of
Physics, Montana State University–Bozeman, Bozeman, MT, 59717, U.S.A."

For **Handy** this *corroborates* the affiliation recorded above: `Montana State University` is an
existing HSSI organisation row carrying the correct ROR (https://ror.org/02w0trx84), and it is the
right row for the Bozeman campus. Creating a separate "Montana State University–Bozeman" row to
mirror the 1998 address string would fragment the organisation for no gain, so it was not done.

For **Freeland** the two disagree in form but not in substance, and the stored value was kept.
`Lockheed Martin Solar and Astrophysics Laboratory` is the HSSI row already attached to this record;
"Lockheed-Martin Palo Alto Advanced Technology Center" is the name the same Palo Alto organisation
published under in 1998, before the solar group's present naming. Three reasons to keep the stored
row: it is the seeded value and the present-day name; the 1998 string is evidence about a paper, not
about who maintains SolarSoft in 2026; and HSSI's update path cannot *replace* an affiliation — it can
only add — so swapping names would leave both attached rather than correcting one. The historical
form is recorded here instead, which is where it is useful.

*Affiliation identifiers.* `Lockheed Martin Solar and Astrophysics Laboratory` exists in HSSI with an
empty identifier and is kept exactly as stored. ROR was searched and carries no record for the
laboratory; the nearest entries are the corporate-level `Lockheed Martin (United States)`
(https://ror.org/026er9r08), which is a different entity, and no separate record for the Advanced
Technology Center. Leaving the identifier empty is correct, not an omission to be filled.

*Placeholder-person caveat (durable, and important for any future correction).* HSSI stores author 2
as a **person** row with `givenName` = "SolarSoft development" and `familyName` = "team". That is a
data-shape error: the intended entity is the SolarSoft Consortium — the collective the licence
names as copyright holder — which is an organisation, not a person. The correct representation would
be an organisation author identified by a ROR. **ROR was searched for "SolarSoft Consortium" and has
no record for it**, so there is no ROR to supply and the organisation form cannot be constructed
today. Two durable constraints bear on any attempt to fix this: HSSI's update API cannot rename an
existing Person row, and the row may be referenced by other software records, so it cannot be
repurposed unilaterally. The row is therefore preserved as-is and the defect recorded here rather
than papered over.

---

### 7. Software Name (MANDATORY)

**Value:** `SolarSoft`

*Source note:* The one-word form is what the project uses. Every primary source consulted spells it
that way: the project pages ("SolarSoftWare (SSW) Installation", and the description document's
"The SolarSoft system…"), the reference publication's title ("Data Analysis with the SolarSoft
System"), the ASCL record ("SolarSoft: Programming and data analysis environment for solar
physics"), and Lockheed Martin's own GitHub description of the `lmco/SolarSoft` snapshot.

**Previous incorrect value: `Solar Soft`.** HSSI held the two-word form, which turned up in no
source consulted — not on the project pages, not in the description document,
not in the paper, not in the ASCL record. It was replaced because this is a factual naming question
rather than a matter of style: the project's name is a single closed compound, as its expansion
"SolarSoftWare" makes plain. **A future agent should not restore `Solar Soft`**, and should not read
a two-word spelling in a third-party catalogue as evidence that the project uses it.

*Durable consequence of the rename: the public slug does not follow it.* This record's
`VerifiedSoftware.slug` is `solar-soft`, and the slug is assigned only on the make-visible path —
never recomputed when the record is saved. The entry is therefore named `SolarSoft` while continuing
to be served at a `…/solar-soft` URL. This is cosmetic, it is not reachable through the update API,
and it is **not** evidence that the rename failed or was partially applied. A future agent that
notices the mismatch should recognise it as this known, accepted divergence rather than re-proposing
the name change or treating the slug as drift to correct.

---

### 8. Description (MANDATORY)

**Value:** unchanged from the existing HSSI record (the full multi-paragraph text beginning "The
SolarSoft system is a set of integrated software libraries, data bases, and system utilities which
provide a common programming and data analysis environment for Solar Physics." and ending "…is now
fully integrated into the SSW distribution and analysis environment for UV/EUV emission line
analysis.").

*Source note:* This text is SolarSoft's **own** description, transcribed from the canonical
*SolarSoft — Description* document served at `https://sohoftp.nascom.nasa.gov/solarsoft/` (last
revision 1999-10-14) and mirrored at `soho.nascom.nasa.gov` and `sohowww.nascom.nasa.gov`. It was
compared against that document and matches it in substance and structure.

**The spelling irregularities in the stored text are faithful to the source, not transcription
errors:** "minimzies", "tranformations", "tranportation", "accomodate", "Utilties", "descibes" and
"SSWsuggested" all appear in the official document. A future agent should not "fix" them, because
doing so would silently diverge the HSSI record from the authoritative text it quotes. If a
corrected version is ever wanted, it should be a deliberate, user-approved editorial change.

The description dates from 1999 and describes capabilities and goals that remain accurate, but it
predates roughly twenty-five years of instrument support (SDO, Hinode, IRIS, STEREO, Solar Orbiter,
Parker Solar Probe, GOES-R, PUNCH, DKIST, ASO-S). Fields 4, 5, 31 and 32 of this record carry that
currency; the description was left alone because it is the project's own words and replacing it
would be an editorial substitution rather than a correction.

---

### 9. Concise Description (OPTIONAL)

**Value:** `The SolarSoft system is a set of integrated software libraries, data bases, and system utilities which provide a common programming and data analysis environment for Solar Physics.`

*Source note:* Unchanged. It is the opening sentence of the project's own description document and
is under the 200-character guidance. Lockheed Martin used the same core sentence as the GitHub
description of `lmco/SolarSoft`, reframed as a noun phrase — "A set of integrated software libraries,
data bases, and system utilities which provide a common programming and data analysis environment
for Solar Physics", without the leading "The SolarSoft system is" and without a trailing period. The
two are not byte-identical, but the correspondence is close enough to be independent confirmation
that this is the sentence the project itself reaches for when summarising the system.

---

### 10. Publication Date (RECOMMENDED)

**Value:** `1998-10-01`

*Source note:* This is the publication month of the reference publication — Freeland & Handy,
"Data Analysis with the SolarSoft System", *Solar Physics* **182**(2), 497–500 — for which Crossref
gives `issued: 1998-10` and the publisher's landing page gives October 1998. Neither source supplies
a day, so the first of the month is used.

**Caveat that must travel with this value: it is the paper's date standing in for an undocumented
software release date, not a precise software release date.** SolarSoft has never made versioned
releases (see Field 12), so there is no release event to date. The value should be read as "the
system was published to the community by no later than October 1998", which is what the refereed
publication establishes. Corroborating that the software itself is at least that old, the
distribution tree carries `gen/setup/setup.ssw.970528` with an mtime of 1996-11-07 and
`gen/setup/IDL_STARTUP.980609` with an mtime of 1998-06-09. **Do not present this date as a release
date, and do not sharpen it to a specific day without a new primary source.**

**Previous incorrect value: `2017-12-16`.** HSSI held that date, and it was a prior extraction
artifact rather than any kind of publication date: it matches to the day the topmost line of the
"Recent Revision History" list on the SSW installation form — "S.L.Freeland , December 16, 2017 ,
add Parker Solar Probe, psp and psp/wispr". That list logs edits to the *installation page*, and its
first entry is exactly what an automated extractor scanning the page for a date would seize on. It
post-dates the system's actual publication by about two decades. **A future agent that finds a date
matching a line of that revision history should treat the match as evidence of the same artifact,
not as corroboration.**

---

### 11. Publisher (RECOMMENDED)

- **Organization:** Lockheed Martin Solar and Astrophysics Laboratory
- **Publisher Identifier:** None — the laboratory has no institutional identifier, and the project
  URL cannot serve as one here (see below)

*Source note:* The field was empty in HSSI. Field 11's guidance is to name the entity that publishes
the work — for software without a DOI, the host of the distribution. SolarSoft is published from
`lmsal.com`: the project home, the installation form that generates a new user's installation script
or package, and the code site recorded by ASCL are all LMSAL pages, and the system's architect works
there. The organisation
name matches the row already present in HSSI (used as the affiliation of authors 1 and 2), so no
near-duplicate organisation is created.

*Why no publisher identifier, and why `https://www.lmsal.com/solarsoft/` is not one.* ROR has no
record for the laboratory (searched; see Field 6), and Field 11 permits a URL in place of a formal
identifier ("or URL otherwise"), so SolarSoft's project URL was considered for this sub-field and
deliberately rejected on two independent grounds.

The first is a durable platform constraint. HSSI's publisher is a shared `Organization` row, and the
laboratory already exists as one — the same row that carries the affiliations of authors 1 and 2 and
of several other people. Organization matching is **identifier-first with no fallback to name**: a
publisher supplied with an identifier is looked up by that identifier alone, and when none matches, a
*new* organisation is created rather than the existing one annotated. Supplying the project URL would
therefore not label the laboratory — it would mint a second "Lockheed Martin Solar and Astrophysics
Laboratory", splitting this record's publisher away from the row every affiliation points at. There is
no path through HSSI's normal write layer that attaches an identifier to an already-named
organisation, so this is not a gap waiting to be filled by a more careful payload.

The second ground is substantive and would hold even if the mechanism allowed it.
`https://www.lmsal.com/solarsoft/` identifies *SolarSoft*, not the laboratory. It is this record's
Field 3, and writing it into a shared institutional row would misattribute a single project's page to
every person and every other piece of software that row represents. **A future agent should not
propose this value again, and should not propose correcting it directly in the database either — the
mechanism is not the only objection.** The correct identifier would be a ROR for the laboratory, which
does not exist; if one is ever registered, that is the value to record.

*Considered and not selected:* **National Aeronautics and Space Administration**
(https://ror.org/027ka1x80). NASA hosts the master distribution tree
(`sohoftp.nascom.nasa.gov`, Goddard Space Flight Center) and funds the work (Field 25), which makes
it a genuine candidate. LMSAL was chosen because publication — the act of presenting the software to
users under a project identity — happens at `lmsal.com`, while `nascom.nasa.gov` performs
distribution. Both roles are recorded in this file so the choice can be revisited with the evidence
intact.

---

### 12. Version (RECOMMENDED)

- **Version Number:** Not found — no version designation exists for SolarSoft
- **Version Date:** Not applicable
- **Version Description:** Not applicable
- **Version PID:** Not applicable

*Source note:* **This is a documented negative result, not a gap.** SolarSoft has no version numbers,
no releases, no tags, no `CHANGELOG` and no `NEWS`. The system is architecturally built around
*last update time* instead of versions, and the evidence for that is unusually direct:

- `gen/idl/ssw_system/ssw_last_update.pro` states its purpose as "spit out time of last SSW mirror
  update by checking date of `$SSW/gen/setup/ssw_info_map.dat`". Its `VERSION` keyword does not
  report an SSW version — it prints the **IDL** version (`if keyword_set(version) then help,/st,!version`).
- `gen/setup/ssw_info_map.dat` is a machine-written stamp regenerated on each master sync. Observed
  2026-08-11 it read `UT Time : 12-AUG-26 02:02:46`, with `IDL Version: 8.8.3`. It moves daily.
- The upgrade path is `ssw_upgrade.pro` / `go_update_ssw.pro`, which rsync/wget a user's tree against
  the master. There is no "upgrade to version N" concept.
- Where the project does snapshot something, it does so by **date, not by number**:
  `gen/setup/setup.ssw_env.20250210`, `setup.ssw.20230620`, `radio/nrh.20240710`,
  `so/stix.20220218`. That convention is itself evidence that no version numbering exists.

**Recommendation: leave Field 12 empty.** The stored HSSI version row holds an empty string, which
the view API renders as `Solar Soft - ` only because it prepends the software name; the stored value
is blank. Leaving it blank is the correct state. Two things must not be done here:

1. **Do not record the `ssw_info_map.dat` timestamp as a version.** It changes every day, so any
   value derived from it is stale before it is published, and it describes a mirror sync rather than
   a state of the software.
2. **Do not write the rendered prefix into Field 12.** The view composes what it displays as
   `<software name> - <version number>`; the prefix is never stored. Because Field 7 now reads
   `SolarSoft`, that display shifts from `Solar Soft - ` to `SolarSoft - ` purely as a rendering
   consequence of the rename — the stored value is unchanged and still blank. **A prefix seen in the
   view is a rendering artifact in either spelling, and copying one back into storage would corrupt
   the record.** Field 12 stores a bare version number and nothing else.

*A quiet benefit of leaving Field 12 empty.* Because no version is written, the blank
`SoftwareVersion` row already attached to this record stays attached and is not replaced. Writing a
version to this field replaces the row rather than editing it, leaving the previous row orphaned; by
holding the field empty on the evidence above, this record avoids that entirely. That is a further
reason not to invent a version merely to populate the field.

If a future refresh finds that SolarSoft has adopted releases, this note is the baseline that
establishes it is a genuine change rather than a value previously missed.

---

### 13. Programming Language (RECOMMENDED)

**Values:** IDL; C; Java

*Source note:* `IDL` is carried over from the existing HSSI record and is unquestionably the primary
language — the description says so ("It is primarily an IDL based system, although some instrument
teams integrate executables written in other languages"), and the 2024 `gen/` snapshot contains 3,975
`.pro` files against 27 Perl, 18 C, 8 Python, 4 Fortran and a dozen Java sources.

The additions are the languages with real, verifiable presence in the distributed tree and a matching
vocabulary row:

- **C** — `gen/idl/dlm/` and the shared libraries and `call_external` interfaces those `.c` sources
  build (for example the cfitsio shared library that `punch/idl/read_punch.pro` calls through
  `/use_shared_lib`).
- **Java** — `gen/idl/clients/java/` (`idlsearchaccessor__define.pro`, `preprocessor__define.pro`,
  `prepresponse__define.pro`, `find_valid_java.pro`) plus compiled `.class` files; the VSO client and
  the prep server historically used the IDL-Java bridge.

*Not recorded, and why.* **Perl** is present in quantity (`gen/perl/`, 27 `.pl` files, and the
`mirror`/`mirror_2.8` distribution machinery) but the vocabulary has no `Perl` row; recording `Other`
in its place would be less informative than this note. **Python** appears as
`gen/idl/clients/python/` (an IDL↔Python bridge: `get_bridge_setup.pro`, `is_pyidl.pro`,
`pyidl_path.pro`), `gen/python/`, and a `py/` directory in the `dkist/vbi` and `packages/helioviewer`
branches — this is interoperability plumbing and a handful of helpers rather than a language SSW is
written in, so `Python 3.x` was considered and not recorded. **Fortran** appears as four `.f` files
in the 2024 `gen/` snapshot, too marginal to claim, and the vocabulary requires choosing a specific
standard (`Fortran77`/`Fortran90`/…) that the sources do not declare.

---

### 14. Reference Publication (RECOMMENDED)

**Value:** `https://doi.org/10.1023/A:1005038224881`

*Source note:* The field was empty in HSSI. Freeland, S. L. and Handy, B. N. (1998), "Data Analysis
with the SolarSoft System", *Solar Physics* **182**(2), 497–500, October 1998. The publisher's own
citation string is "Freeland, S., Handy, B. Data Analysis with the SolarSoft System. Solar Physics
182, 497–500 (1998)."

Confirmed independently from three directions, which is worth recording because they agree on every
field: **Crossref** (title, container, volume 182, issue 2, pages 497–500, issued 1998-10, both
authors); **ADS** (bibcode `1998SoPh..182..497F`); and the **publisher's landing page** (title,
authors, volume, page range, October 1998, DOI). The **ASCL** record for SolarSoft names this same
paper in its "Described in" field, which is what confirms it as the paper describing *the software*
rather than merely a paper using it.

*The paper's reference list is itself useful evidence about SolarSoft's foundations,* and matches
what the software's own description claims. It cites only four works: Dere, Landi, Mason,
Monsignori Fossi & Young (1998) — the **CHIANTI** paper, which independently corroborates the CHIANTI
relationship recorded in Field 29; Domingo, Fleck & Poland (1995), *Solar Phys.* 162, 1 — **SOHO**;
and Morrison, Lemen, Acton, Bentley, Kosugi, Tsuneta, Ogawara & Watanabe (1991), *Solar Phys.* 136,
105, together with Ogawara, Takano, Kato, Kosugi, Tsuneta, Watanabe, Kondo & Uchida (1991),
*Solar Phys.* 136, 1 — both **Yohkoh**. Two of the four bodies of work the description names as
SolarSoft's foundation ("built from Yohkoh, SOHO, SDAC and Astronomy libraries") are cited directly.

*Publication-time author affiliations, as stated by the publisher:* S. L. Freeland —
"Lockheed-Martin Palo Alto Advanced Technology Center, Palo Alto, CA, 94303, U.S.A."; B. N. Handy —
"Department of Physics, Montana State University–Bozeman, Bozeman, MT, 59717, U.S.A." ADS records
the same two affiliations. These are **1998** affiliations; how they were weighed against the
affiliations actually recorded for these authors is set out in Field 6.

*Publisher-assigned index terms* for this paper are "Data Analysis; Data Management; Learning Curve;
Base System; Analysis Routine". They are recorded here as provenance only — see Field 16 for why they
were not used as keywords.

---

### 15. License (RECOMMENDED)

- **License:** `BSD 2-Clause "Simplified" License`
- **License URI:** https://spdx.org/licenses/BSD-2-Clause.html

*Source note:* The field was empty in HSSI. The licence file is served at the root of the
distribution tree (`https://hesperia.gsfc.nasa.gov/ssw/LICENSE`, mtime 2020-02-12) and again at
`gen/LICENSE` (mtime 2020-02-11); the same file is present in the `lmco/SolarSoft` snapshot and was
read there in full. It opens `Copyright 2020 SolarSoft Consortium`, states
the two standard redistribution conditions (source-form notice retention; binary-form notice
reproduction), and closes with the standard BSD warranty disclaimer.

**It is BSD-2-Clause, not BSD-3-Clause.** The file contains exactly two numbered conditions; there is
no third, no-endorsement clause. `BSD 3-Clause "New" or "Revised" License` is also present in HSSI's
vocabulary and is the wrong choice here — this note exists so that a future agent skimming for "BSD"
does not select it.

The vocabulary row spells `Simplified` with **straight** double quotes, which is what the value
above uses. A typographic-quote copy is a different string and will not match.

*Note on the copyright holder.* "SolarSoft Consortium" is the entity the licence names. It has no
ROR record (searched) and is not currently representable as an organisation author; see Field 6.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values:** solar soft; sswidl; idl; solar physics; data analysis; data access; fits; image processing;
time series analysis; solar imaging; coronagraph; spectroscopy; magnetogram; instrument response;
differential emission measure; chianti atomic database; scientific software; heliophysics

*Source note:* The field was empty in HSSI. Keywords is HSSI's only open vocabulary, so unknown
values would be created as new rows. **Every value above corresponds to a keyword row that already
exists**, so this record mints nothing new and introduces no near-duplicates — which is why these
particular terms were chosen over synonyms that would have created fresh rows. Each is lower-case and
single-concept, matching the form of the stored rows.

The set is chosen to be *discriminating* rather than exhaustive: the two SSW-specific handles
(`solar soft`, `sswidl`) and the language (`idl`) make the record findable by name; the domain terms
follow the capabilities evidenced in Field 4; `chianti atomic database` and `differential emission
measure` reflect integrated packages that a searcher would plausibly use to find this environment.

*Considered and rejected — the reference publication's publisher-assigned index terms.* Springer
assigns "Data Analysis; Data Management; Learning Curve; Base System; Analysis Routine" to
`10.1023/A:1005038224881`. None was adopted. They index the *paper* rather than the software, three
of them ("Learning Curve", "Base System", "Analysis Routine") are automatically-derived phrases that
carry no science meaning, and adopting them would mint new rows in HSSI's only open vocabulary for
terms no searcher would use. `data analysis` — the one genuinely useful term among them — is already
in the list above from an existing row. Recorded so a later refresh does not import them from the
DOI metadata.

---

### 17. Data Sources (OPTIONAL)

**Values:** The Virtual Solar Observatory.; Observatory/Mission-specific; HTTP/HTTPS Directories;
FTP/FTPS Directories

*Source note:* The field was empty in HSSI.

- **`The Virtual Solar Observatory.`** — `gen/idl/clients/vso/` is a full VSO client
  (`vso__define.pro`, `vso_search.pro`, `vso_get.pro`, `vso_server.pro`, plus a SOAP layer), and
  `vobs/vso` is a distributed branch selectable on the installation form. **The trailing period in
  this value is part of the stored vocabulary row and is required for the value to match**; a copy
  without it is rejected.
- **`Observatory/Mission-specific`** — SSW ships mission-specific archive clients: `vobs/ontology`
  provides JSOC and HEK/HCR communication for SDO, `gen/idl/clients/soar/` queries the Solar Orbiter
  Archive (`soar_list.pro`, `soar_search.pro`), and `gen/idl/clients/hv/` queries Helioviewer. Field
  17's own instruction is to select this value and name the missions in Field 32, which this record
  does.
- **`HTTP/HTTPS Directories`** — `gen/idl/sockets/` contains 73 `sock_*` routines for
  listing and retrieving from web directories (`sock_dir.pro`, `sock_copy.pro`, `sock_cat.pro`,
  `sock_check.pro`), and the installation form made cURL the default transfer protocol in August
  2019.
- **`FTP/FTPS Directories`** — `gen/idl/objects/ftp__define.pro`, `gen/idl/sockets/is_ftp.pro` and
  `sock_dir_ftp.pro`; the installation form still offers "FTP", "Passive FTP" and "Passive FTP + No
  Extended Passive (Mac/Darwin for example)" as transfer protocols.

*Searched and not found:* **CDAWeb** and **OMNIWeb** — a case-insensitive search of the `gen/`
library for both names returned nothing, so neither was recorded. **HAPI**, **das2**, **AMDA**,
**SSCWeb**, **Madrigal**, **VirES**, **GFZ**, **WDC**, **TAP** and **S3/Cloud-aware** likewise have
no supporting code in the material examined. This negative research is recorded so a later refresh
does not re-add them speculatively from the software's breadth.

*Belonging to other fields:* the HEK (Heliophysics Event Knowledgebase), CoSEC, EGSO, HELIO and the
Ontology library are event/service layers rather than rows in this vocabulary; the mission archives
they front are represented through `Observatory/Mission-specific` and Field 32.

---

### 18. Input File Formats (RECOMMENDED)

**Values:** FITS; ascii; IDL.sav; netCDF3/4; JSON; csv; Other

*Source note:* The field was empty in HSSI.

- **FITS** — the format SSW is built around: `gen/idl/fits/` (115 IDL routines), `fits2map.pro`,
  `mreadfits`, the `fxb*` binary-table family, and per-instrument readers throughout.
- **ascii** — `rd_ascii.pro`, `rd_tfile.pro`, `readcol.pro`, `rd_ulin_col.pro`,
  `rd_goesp_ascii.pro`, `rd_goesx_ascii.pro`.
- **IDL.sav** — `restgen.pro`, `restgenx.pro`, `multi_restore.pro`, `restsys.pro`, and `.sav` files
  shipped in the tree.
- **netCDF3/4** — `read_netcdf.pro`, and the GOES-R readers `rd_goes_nc.pro`, `read_goes_nc.pro`,
  `read_goes_nc_curl.pro`.
- **JSON** — `json_parse` is used by the Helioviewer client (`hv_search.pro`, `hv_times.pro`,
  `hv_source.pro`), the prep client (`prep_client.pro`), `ssw_get_goesdata.pro`,
  `ssw_get_winddata.pro` and the socket service layer.
- **csv** — `read_csv` in the Solar Orbiter Archive client (`soar_list.pro:169`,
  `soar_search.pro:160`), which parses SOAR's CSV query responses.
- **Other** — covers formats with no vocabulary row that SSW genuinely reads: its own **genx/geny**
  structure-serialisation format (`rd_genx.pro`, `restgenx.pro`, `read_genxcat.pro`,
  `merge_genxcat.pro`), **JPEG 2000** from Helioviewer (`hv_get.pro`), and GIF/JPEG/TIFF/PNG
  (`jpeg2map.pro`, `gif2ps.pro`, `tiff2gif.pro`).

*Considered and not selected:* **CDF**. `gen/idl/time/` contains CDF *epoch* conversion helpers
(`anytim2cdf.pro`, `cdf2tai.pro`, `cdf2utc.pro`), but a search of the `gen/` library for actual CDF
file I/O (`cdf_open`, `cdf_varget`, `cdf_inquire`) returned nothing, so CDF reading was not claimed.
This conclusion rests on the `gen/` library; the mission and package branches were not read
routine-by-routine, so a future agent finding CDF I/O in a branch is refining this, not contradicting
it. **HDF5** — searched (`h5f_open`, `hdf_sd_start`, `h5_parse`) with no hits. **ISTP-Compliant** and
**Zarr** — no evidence.

---

### 19. Output File Formats (RECOMMENDED)

**Values:** FITS; ascii; IDL.sav; JSON; csv; Other

*Source note:* The field was empty in HSSI.

- **FITS** — `gfits_w.pro`, `wcs2fitshead.pro`, `plotman__image_fitswrite.pro`,
  `data_sum2fits.pro`, `plotman__write_image_cube.pro`.
- **ascii** — `wrt_ascii.pro`, `write_ascii.pro`, `wr_asc.pro`, `gfits_w_ascii.pro`,
  `goes_day_ascii.pro`, `text_output.pro`.
- **IDL.sav** — `savegen.pro`, `savegenx.pro`, `multi_save.pro`, `savesys.pro`.
- **JSON** — `json_serialize` in `sock_service.pro`, `sock_sendvar.pro` and `prep_service.pro`; the
  prep and socket services return JSON to their clients.
- **csv** — `write_csv` in `gen/idl/synoptic/sff/sff_wrt_txt_file.pro` (writes
  `ssw_sff_list_cmx.csv` and `ssw_sff_list.csv`).
- **Other** — the graphics and web outputs that have no vocabulary row and are a genuine, prominent
  part of what SSW produces: GIF, animated GIF, PNG, JPEG, TIFF, PostScript and MPEG
  (`gen/idl/graphics/`: `mk_gif.pro`, `mk_agif.pro`, `fits2png.pro`, `fits2tiff.pro`,
  `gifs2mpeg.pro`, `mk_mpeg.pro`, `ssw_ffmpeg.pro`, `saveimage.pro`), HTML and JavaScript movie
  pages (`gen/idl/http/`: `jsmovie.pro`, `html_linklist.pro`, `genx2html.pro`), the **genx/geny**
  format (`wrt_genx.pro`, `savegenx.pro`, `write_genxcat.pro`), and **JPEG 2000** for Helioviewer
  ingest (`hv_trace2_prep2jp2.pro`).

*Not selected:* **netCDF3/4** — the netCDF support found is read-only (GOES-R ingest); no writer was
found. **CDF**, **HDF5**, **ISTP-Compliant**, **Zarr** — as for Field 18.

---

### 20. Operating System (RECOMMENDED)

**Values:** Linux; Mac; Windows; Solaris; Other

*Source note:* The field was empty in HSSI. Two independent lines of evidence agree.

The installation form states its own scope directly: "Use this FORM for **UNIX, Linux, FreeBSD,
MacOSX, and Windows**", and offers a separate Windows path (a ZIP installation package and
`setup.bat`, versus a C-shell script for the Unix family), with `ssw_windows.html` and
`setssw_windows.pro`/`ssw_setup_windows.pro` supporting it.

The distribution's compiled-binary tree `packages/binaries/exe/` names its supported platforms
explicitly, and its directory mtimes show which are still refreshed:

| Directory | Last modified | Maps to |
|---|---|---|
| `darwin_i386` | 2021-11-17 | Mac |
| `Darwin_ppc`, `darwin_ppc` | 2020-09-10, 2019-11-28 | Mac (PowerPC era) |
| `darwin_x86_64` | 2015-11-25 | Mac |
| `Win32_x86_64` | 2019-07-31 | Windows |
| `Win32_x86` | 2012-11-16 | Windows |
| `sunos_x86_64` | 2016-02-11 | Solaris |
| `sunos_sparc` | 2004-12-16 | Solaris |
| `linux_x86_64` | 2007-12-14 | Linux |
| `linux_x86` | 2005-04-12 | Linux |
| `AIX_ibmr2`, `IRIX_mipseb`, `OSF_alpha`, `ultrix_mipsel` | 1999–2005 | Other |

`Solaris` is recorded on the strength of `sunos_x86_64` still being present and refreshed as recently
as 2016. `Other` covers **FreeBSD**, which the current installation form names in its own supported
list and which has no vocabulary row, and secondarily the legacy AIX/IRIX/Tru64/Ultrix builds the
tree still carries.

*Not selected:* `Operating System Independent`. SSW's IDL sources are portable, but the system ships
per-platform executables and shared libraries and its setup machinery branches on platform, so the
independent claim would be wrong. `MobilePlatform` — no evidence.

---

### 21. CPU Architecture (RECOMMENDED)

**Values:** x86-64; Sun (SPARC); Other

*Source note:* The field was empty in HSSI. Derived from the same `packages/binaries/exe/` evidence
as Field 20, which is the authoritative statement of what the project actually builds for.

- **x86-64** — `linux_x86_64`, `darwin_x86_64`, `Win32_x86_64`, `sunos_x86_64`. The master tree's own
  build stamp (`gen/setup/ssw_info_map.dat`) also reports `Host ARCH : x86_64`.
- **Sun (SPARC)** — `sunos_sparc`.
- **Other** — 32-bit x86 (`linux_x86`, `Win32_x86`, `darwin_i386`), PowerPC (`Darwin_ppc`,
  `darwin_ppc`), MIPS (`IRIX_mipseb`, `ultrix_mipsel`), Alpha (`OSF_alpha`) and IBM POWER
  (`AIX_ibmr2`), none of which has its own vocabulary row.

*Considered and not selected — `Apple Silicon arm64`.* This is worth recording as negative research,
because it is the value a future agent is most likely to want to add. The binary tree contains **no
arm64 build**; the most recent Darwin directory is `darwin_i386` (2021-11-17), which is Intel. SSW's
pure-IDL code will run on Apple Silicon under a supported IDL, but the shipped executables and shared
libraries — and the routines that depend on them, such as `read_punch.pro` with `/use_shared_lib` —
have no native arm64 build in the distribution. The value should be added when an arm64 directory
appears, not before.

*Also not selected:* `CPU Independent` — contradicted by the per-architecture binary tree, for the
same reason `Operating System Independent` was rejected in Field 20. `ppc64le` — the PowerPC builds
present are big-endian 32-bit Darwin, a different target. `GPU`, `HPC or HEC`, `Linux aarch64 or
arm64` — no evidence.

---

### 22. Related Phenomena (OPTIONAL)

**Values:** Solar Flares; Solar Corona; Coronal Mass Ejections; X-ray emission; Solar Wind;
Coronal Heating; Geomagnetic Storms

*Source note:* The field was empty in HSSI. This is the whole of the live seven-row `Phenomena`
vocabulary, which is an unusual outcome and is justified here only because SolarSoft is a
general-purpose environment for an entire discipline rather than a single-purpose tool. Each value
has its own evidence:

- **Solar Flares** — GOES event handling (`decode_gev.pro`, `get_gev.pro`, `list_gev.pro`,
  `find_goes_events.pro`, `goes_make_yearly_eventlist.pro`, `ssw_flare_locator.pro`,
  `flare_hist.pro`), and the flare instruments SSW is built for (RHESSI, Yohkoh HXT/BCS, STIX,
  ASO-S/HXI) with the `spex` fitting package.
- **Solar Corona** — the dominant observational domain (see Field 5).
- **Coronal Mass Ejections** — the `cmes`, `cactus` and `corimp` packages,
  `ssw_getcme_cactus.pro`, `ssw_getcme_cdaw.pro`, `ssw_getcme_list.pro`, and the coronagraph and
  heliospheric-imager branches.
- **X-ray emission** — GOES XRS is core SSW (`gen/idl/synoptic/goes/`, 89 IDL routines), together with
  SXT, XRT, SXI, SUVI, HXT, HXRBS, BATSE, HXRS and the `xray` package.
- **Solar Wind** — STEREO PLASTIC/IMPACT, ACE and Wind retrieval (`read_ace.pro`,
  `ssw_get_winddata.pro`), and the PUNCH branch.
- **Coronal Heating** — the differential-emission-measure package family that is the standard
  diagnostic for it (`vdem`, `demreg`, `simple_reg_dem`, `dem_sites`, added to the distribution in
  2019–2020), plus loop energetics tooling (`hydro` package, `betaloop.pro`,
  `calc_rad_loss.pro`, `tem_thermal_power.pro`).
- **Geomagnetic Storms** — index retrieval and handling for solar–terrestrial correlation:
  `ssw_getdst.pro`, `ssw_kyoto2dst.pro`, `ssw_getapkp.pro`, `ssw_apkpbar.pro`, `get_swpc.pro`,
  `get_solar_indices.pro`. This is the weakest of the seven — the support is ancillary index
  retrieval rather than magnetospheric modelling — and is recorded because a scientist correlating
  flare/CME events with geomagnetic response would reach for exactly these routines. A reviewer who
  judges that too thin should drop this one value; the other six do not depend on it.

*Note:* `Coronal Holes` is **not** a row in this vocabulary and would be rejected. SSW does support
coronal-hole work (for example through the `catch` package), and that support is represented via
`Corona` in Field 5 rather than invented here.

---

### 23. Development Status (RECOMMENDED)

**Value:** `Active`

*Source note:* The field was empty in HSSI. "Reached stable, usable state and being actively
developed" fits precisely, and the evidence is unambiguous even without a commit history:

- the master tree is regenerated daily (`gen/setup/ssw_info_map.dat`, observed stamped
  `12-AUG-26 02:02:46` UT on 2026-08-11);
- source files carry recent preserved mtimes — `gen/setup/setup.ssw_env` 2026-05-29,
  `gen/idl/wcs/` 2026-06-01, `gen/idl/display/` 2026-05-26,
  `gen/idl/ssw_system/go_update_ssw.pro` 2026-02-10;
- new mission support is still being added: the `punch/` branch's routines are dated 2026-05-15 and
  its directory 2026-05-29, `so/stix/` 2026-07-13, `asos/lst/idl/` 2026-05-05;
- and `setup.ssw_env` declares DKIST, ASO-S and PUNCH in `SSW_MISSIONS`, none of which appear on the
  installation form (whose revision history ends 2023-06-28) — the tree is running ahead of its own
  documentation.

*Considered and rejected:* `Inactive`. The stale-looking artifacts that might suggest it — the 1999
description document, the 2019 page title on the installation form, the 2024-frozen GitHub snapshot —
are all *documentation or third-party copies*, not the software. The distribution itself is current.

---

### 24. Documentation (RECOMMENDED)

**Value:** `https://www.lmsal.com/solarsoft/ssw_concepts.html`

*Source note:* The field was empty in HSSI. This is *SolarSoft Concepts* — titled "SSW overview for
TRACE/YOHKOH/SOHO Coordinated Analysis", last revised 1999-03-15 by S. L. Freeland — which the
canonical *SolarSoft — Description* document lists **first** among its Related Documents. It is the
project's general "how do I actually use this" document: an overview of the SSW analysis
environment, its common interfaces and naming conventions, and cut-and-paste tutorials developed for
the CDAW4 and MEDOC workshops. It also carries an onward link list covering SSW Overview,
Installation, Automatic Upgrades, Setup and running IDL, Pointing and Time Standards, and the SSWDB
databases, so a user landing here reaches installation in one click.

*Why this rather than the installation guide.* `https://www.lmsal.com/solarsoft/ssw_install_howto.html`
— the official *SolarSoft Installation Guide*, "Last Updated on August 8, 2019, Samuel Freeland" — was
held in this field earlier in this record's history and is the strongest rejected alternative. It is
the most recently maintained SolarSoft documentation page found, and it walks through the full
installation for both the Unix/Linux/FreeBSD/macOS C-shell path and the Windows ZIP path with a
worked example. It was displaced because it is *installation only*: its own Related Documents list
reaches Upgrades, Setup and Windows but not the concepts or tutorial material, so a user sent there
can install SolarSoft and still not learn how to use it, whereas the reverse is not true of the value
chosen. Field 24 names documentation as the primary object and installation instructions as the
qualifier; the concepts page satisfies both, the installation guide only the qualifier. Anyone who
wants the installation link specifically should use the URL in this paragraph.

*Link health of the chosen value.* The page's markup carries **25 `href` attributes resolving to 23
distinct destinations** — `ssw_standards.html` is linked three times. Stating both numbers is
deliberate: an earlier state of this note said simply "23 href attributes", and that unit ambiguity is
what produced a miscount further down. **Any figure here should name its unit — attributes,
destinations, or hosts — because the three differ.** Of the 23 distinct destinations, 15 are internal,
7 external, and one is a same-page fragment (`#tutorials`).

**All 15 internal destinations resolve**: `index.html`, `ssw_install.html`,
`ssw_setup.html`, `ssw_standards.html`, `ssw_upgrades.html`, `ssw_movie_making.html`, `ssw_3D.html`,
`ssw_eit_mdi.html`, `ssw_trace_sxt_mdi.html`, `sswdb_configure.html`, `medoc/eit.html`,
`medoc/lasco.html`, `medoc/trace.html`, `sswdoc/guides/tag/` and `sswdoc/guides/yag/`.

**Of the 7 external destinations, 6 have rotted — spread across 5 distinct dead hosts — and 1 is
alive.** Again the unit matters, because references and hosts give different numbers; both are stated
so neither can drift:

| Dead host | Reference(s) on the page |
|---|---|
| `soho01.nascom.nasa.gov` | `~soho/ssw_cat/` — the old routine-category index (see the access-limitation note below) |
| `diapason.lmsal.com` | `~cdaw/` and `~cdaw/movies/ssw_track_demo.html` — two references to the same dead host |
| `orpheus.nascom.nasa.gov` | `~zarro/idl/maps.html` — Zarro's mapping-package page |
| `vestige.lmsal.com` | `TRACE/Data/trace_cat.html` — TRACE catalogue |
| `www.medoc-ias.u-psud.fr` | the external MEDOC data-centre site |

Each of the five fails DNS resolution outright rather than returning an error page. **The surviving
external destination is `umbra.nascom.nasa.gov/eit/eit_guide/guide.html`, the SOHO/EIT user guide,
which resolves and serves** — so a future agent should not generalise this to "the external links are
all dead".

**Do not confuse the external MEDOC site with the internal `medoc/*.html` pages.** The dead host is
`www.medoc-ias.u-psud.fr`, the data centre's own site. The three `medoc/eit.html`,
`medoc/lasco.html` and `medoc/trace.html` pages are hosted on `lmsal.com` alongside the concepts
page, resolve normally, and are counted among the healthy internal links above.

**One anchor has a stale visible label rather than a broken target.** The SSWDB entry displays the
text `www.lmsal.com/solarsoft/ssw_sswdb.html` — a URL that 404s — while the anchor's actual `href` is
`sswdb_configure.html`, which resolves. The link therefore works; only what it prints is out of date.
The other live SSWDB documents are `sswdb_description.html` and `sswdb_install.html`.

All of this rot is in 1990s- and 2000s-era third-party material rather than in SolarSoft's own pages.
It is worth knowing about but does not affect the concepts page's own content or its route to
installation.

*Other official documentation, recorded so a future agent does not have to rediscover it.* All
reachable: `ssw_install_howto.html` (installation guide, 2019), `ssw_setup.html` (running
SSWIDL), `ssw_upgrades.html`, `ssw_windows.html`, `ssw_packages_info.html`, `ssw_movie_making.html`,
`sswdb_install.html` and `sswdb_description.html` (the SSWDB ancillary databases), and
`ssw_standards.html`. The canonical *SolarSoft — Description* document at
`https://sohoftp.nascom.nasa.gov/solarsoft/` is the other Related Documents hub, and that same host
serves the **browsable master source tree**, which is the single most useful thing to know about this
project's documentation (see the scope note and Field 3).
`https://stereo-ssc.nascom.nasa.gov/solarsoft_wget.shtml` carries Bill Thompson's official
wget-based transfer instructions, linked from the installation form.

*Considered and not selected — `ssw_standards.html`.* At 24,163 bytes it is the largest of the ten
official documentation pages measured for this record — ahead of `ssw_concepts.html` (17,858) and
`ssw_packages_info.html` (15,922) — and the most technically load-bearing of them ("SSW Keyword/Tag
Definitions", last revision 2005-07-05). It is the
"SSW suggested Keywords and Tags" specification that Field 8's description text itself points to, and
it names the packages those conventions unlock (Zarro's mapping package, Thompson's WCS package,
Schwartz's utplot, Aschwanden's dynamic stereoscopy). It was not chosen because it is a *data
convention specification* rather than user documentation or installation instructions — it tells an
instrument team how to make its FITS files SSW-compatible, not a scientist how to use SSW. It is the
right link to reach for when the question is about SSW's pointing and time standards.

*Durable access limitation — the SSW routine documentation index, and the exact shape of the block.*
The searchable per-routine reference that Field 8's description calls the "WWW index which allows
searching for SSW routines by category and/or string pattern" is **not publicly reachable**.
`https://www.lmsal.com/solarsoft/sswdoc/index.html` and the directory form
`https://www.lmsal.com/solarsoft/sswdoc/` both return a hard **403 Forbidden** — Apache's plain
"You don't have permission to access this resource" body, not a bot challenge and not a JavaScript
interstitial — and the 403 persists under full browser rendering with JavaScript enabled, so it is a
deliberate server-side restriction rather than a transient block or an anti-automation measure. **A
different client will not get past it; do not spend time retrying.**

The block is **path-specific, not subtree-wide**, which is worth recording because the difference is
easy to get wrong. Under the same `sswdoc/` prefix, `sswdoc/guides/`, `sswdoc/guides/tag/` (the TRACE
Analysis Guide), `sswdoc/guides/yag/` (the Yohkoh Analysis Guide) and
`sswdoc/guides/guides_index_noforms.html` all serve normally. That reachable guides index —
"SolarSoft Help Documentation", by R. D. Bentley, dated 1998-12-18 — was evaluated as a Field 24
candidate and rejected on its own testimony: it opens "All the guides on this page are being
developed or modified. **Use them at your own risk!!!!!!!**" and adds "These versions are very
preliminary! Known bugs include the: Links from Index to software routines ... On-line headers for
SSW IDL routines". A documentation link that warns the reader off its own contents is not a
defensible value for this field.

No live replacement for the routine index was found: `soho01.nascom.nasa.gov` (the old `~soho/ssw_cat`
category index) fails DNS resolution, and `ssw_categories.html`, `ssw_whatsnew.html`,
`sswdoc/index_all.html`, `sswdoc/ssw_categories.html`, `sswdoc/site/` and `sswdoc/gen/` all return
404. If the 403 is ever lifted, `sswdoc/index.html` becomes the strongest candidate for this field and
this whole note should be revisited.

---

### 25. Funder (OPTIONAL)

- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

*Source note:* The field was empty in HSSI. The funder is established from the reference
publication's own text rather than from aggregated metadata: the indexed full text of
`1998SoPh..182..497F` is confirmed to contain the phrases "work was supported", "supported by NASA",
"NASA contract" and "contract NAS5-38099". Crossref returns no funding block for this DOI at all, so
the paper's own acknowledgement is the source relied on here, and it is the right one — see the note
below on exactly how firmly that text is established.

The organisation name matches the row already present in HSSI (with the ROR), so no near-duplicate is
created, and the acronym is expanded as the field requires.

**How firm this evidence is, stated plainly.** The award number rests on *membership probes against
the paper's ADS-indexed body text*, not on a directly quoted acknowledgement, and a future agent
should not represent it as a quotation. The probes were run with controls in both directions: a
nonsense token returned zero, and the negative controls `NAS8-37334`, `NAS8`, `NAG5` and `grant` all
returned zero on this paper while `NAS5-38099`, `NASA contract`, `supported by NASA`, `work was
supported` and `Lockheed` each returned one. The conjunction of "NASA contract", "supported by NASA"
and "contract NAS5-38099" in a four-page paper leaves little room for another reading, but the
distinction between probe evidence and a quotation is real and is preserved here.

**Why a quotation is not available, and what is not worth retrying.** The publisher's landing page
*does* render under a real browser — the Cloudflare challenge that defeats ordinary fetches clears —
and it exposes the abstract, the reference list, the author affiliations and the citation metadata
recorded in Field 14. It does **not** expose the article body: the text is gated behind a
"Download to read the full article text" control, so the acknowledgements section is not on the
publicly reachable page and browser rendering alone does not obtain it. ADS's structured
acknowledgements field is empty for this record even though the body text is indexed, which is why
the probe route was needed in the first place. Retrieving the acknowledgement verbatim would mean
downloading the copyrighted PDF, which is a decision for a human, not something a future agent
should do on its own initiative.

---

### 26. Award Title (OPTIONAL)

- **Award Title:** `NASA contract NAS5-38099`
- **Award Number:** `NAS5-38099`

*Source note:* The number comes from the reference publication's acknowledgement, which contains the
exact phrase "contract NAS5-38099" (see Field 25 for how that was established).

**The award's real title is unknown, and the value above is a descriptive label rather than a
discovered one.** The distinction matters enough to state plainly: no source consulted names this
award, and the reason is a retrievability limit rather than an incomplete search. The acknowledgement
text that carries the contract number is not on any publicly reachable page — the publisher's landing
page renders under a browser but gates the article body behind a download control, and ADS exposes no
structured acknowledgements section for this record even though it indexes the body. The only part of
the acknowledgement that could be established is what targeted probing could confirm is present: the
contract number. A title, being unknown text rather than a string one can test for, cannot be
recovered that way. **A future agent should treat the true title as blocked by source access, not as
unfinished work, and should not replace the label below with a guess at it.**

*Why a label was recorded at all, rather than leaving the field empty.* HSSI cannot store an award
number without an award name — a nameless award is rejected outright at the write layer, so "number
known, title unknown" is not an expressible state. That left three real options, and the choice among
them is settled:

- **Omitting the field** would have discarded `NAS5-38099` entirely. The number is the one piece of
  funding provenance this record has, and losing it to a formatting constraint is the worst outcome.
- **Using the bare number as the name** would have stored `NAS5-38099` in both sub-fields. Every other
  award in HSSI carries a human-readable title with the number in the identifier, so a bare number
  reads as a data error rather than as a deliberate record of an untitled award.
- **`NASA contract NAS5-38099`** describes what the award demonstrably is — a NASA contract bearing
  that number, both facts established by the acknowledgement — without asserting a title the sources
  never gave. It stays within this record's own prohibition on inventing a title precisely because it
  is not offered as one.

*What it is emphatically not.* Other papers acknowledging NAS5-38099 are predominantly TRACE analyses
from the same institution, which is consistent with NAS5-38099 being the NASA contract under which
Lockheed Martin performed its TRACE-era solar work. That is background, **not** a title: a plausible
expansion such as "TRACE" or a programme name must not be substituted into the label above.

*What the recorded award replaced.* This record previously pointed at a blank award row — a row with
an empty name, carrying no information. That row is **shared with other records**, so recording a real
award here detaches this record from it and leaves it in place for the others; nothing about those
other records changes. A future agent should not read the blank row's continued existence elsewhere in
HSSI as a sign that this record's award failed to apply.

*Scope caveat.* This is the funding of the 1998 paper that describes SolarSoft. SolarSoft has been
developed continuously for a further quarter-century under funding that no source consulted
identifies; the value above should be read as the earliest documented support, not as a complete
funding history.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Values:**

1. `https://doi.org/10.1888/0333750888/3390` — Freeland, S. (2000). *SolarSoft*. In Murdin, P. (Ed.),
   Encyclopedia of Astronomy and Astrophysics. Institute of Physics Publishing. ADS bibcode
   `2000eaa..bookE3390F`.
2. Bentley, R. D., & Freeland, S. L. (1998). SOLARSOFT — an analysis environment for solar physics.
   In *Crossroads for European Solar and Heliospheric Physics* (ESA SP-417, p. 225). European Space
   Agency. https://ui.adsabs.harvard.edu/abs/1998ESASP.417..225B
3. Hurlburt, N. E. (2024). *Recent advancements in the SolarSoft environment*. AGU Fall Meeting
   abstract IN13B-2169. https://ui.adsabs.harvard.edu/abs/2024AGUFMIN13B2169H
4. Cheng, J. (2023). *Evolving SolarSoft for (more) open science*. AGU Fall Meeting abstract
   SH33C-3076. https://ui.adsabs.harvard.edu/abs/2023AGUFMSH33C3076C

*Source note:* The field was empty in HSSI. Entries 1 and 2 are the two other publications that
*describe the system itself*, complementing the reference publication: the Encyclopedia of Astronomy
and Astrophysics article (the only one of the four with a DOI) and Bentley & Freeland's ESA
conference paper, which gives the European/SOHO-side account. Entries 3 and 4 are recent conference
abstracts that document SolarSoft's continuing development and its open-science direction, and are
included because they are among the few citable statements about the *current* state of a project
whose principal documentation dates from 1999. Entries 2–4 have no DOI, so they follow Field 27's
instruction to give an APA-format citation with a permanent link (ADS abstract pages, which are
stable).

*Considered and not selected:* the reference publication itself, which belongs in Field 14 and must
not be duplicated here. Also not selected: the several hundred papers that merely *use* SSW. The
reference publication is heavily cited — as of 2026-08-11 ADS recorded 698 citations and the
publisher 753, the difference being the usual one of indexing scope — and enumerating usage papers
would say nothing about the software that the citation record does not already say. Two further abstracts were read and
left out as too narrow to help a reader: `2021AAS...23821301H` (Hurlburt, "The Future Of SolarSoft"),
superseded by entry 3, and `2022AGUFMSH52A..69A` (Antunes, on containerising SSW for a Jupyter cloud
framework), which describes work not present in the distribution.

---

### 28. Related Datasets (OPTIONAL)

**Value:** Not found

*Source note:* SolarSoft is deliberately dataset-agnostic in a way that makes this field the wrong
shape for it. Its own description states the goal: "Provide a file-format independent analysis
environment ... file I/O is isolated and analysis applications are designed to operate on objects
which are independent of file type." It analyses whatever its instrument branches can read — the
holdings of the VSO, JSOC, the Solar Orbiter Archive, Helioviewer and every mission archive behind
them — rather than a bounded set of datasets that could be enumerated as DOIs.

The ancillary databases the system *does* ship (SSWDB — active-region catalogues, GOES event lists,
NOAA SRS records, instrument response tables) are distributed as part of the software through
`sswdb_install.html` and were searched for dataset DOIs; none carries one. Recording `Not found` is
therefore the correct outcome, and the missions whose data SSW supports are recorded in Field 32
where they belong.

---

### 29. Related Software (OPTIONAL)

**Values:**

1. `https://www.chiantidatabase.org/` — CHIANTI atomic database and IDL package
2. `https://github.com/wlandsman/IDLAstro` — IDL Astronomy User's Library

*Source note:* The field was empty in HSSI. Both entries are named by SolarSoft's own description as
external bodies of work the system is built from or has absorbed, which is exactly the
"domain-specific dependency / distinguishing software" that Field 29 asks for.

- **CHIANTI** — the description says it outright: "the Chianti Package, K. Dere et al. is now fully
  integrated into the SSW distribution and analysis environment for UV/EUV emission line analysis."
  It is a selectable component on the installation form, has its own branch (`packages/chianti`) and
  its own environment variable (`SSW_CHIANTI`, marked "# supported"), and SSW's GOES temperature and
  emission-measure chain depends on it directly (`goes_chianti_tem.pro`,
  `goes_get_chianti_temp.pro`, `goes_chianti_resp_*.fits`, `chianti7p1_rad_loss.txt`). CHIANTI has
  no single code repository URL, so the project site is used as Field 29 permits. The relationship is
  corroborated from outside SolarSoft's own documentation as well: the reference publication cites
  only four works, and one of them is the CHIANTI paper (Dere, Landi, Mason, Monsignori Fossi &
  Young 1998) — so the CHIANTI connection was load-bearing enough to cite in the four-page paper
  describing the system.
- **IDL Astronomy User's Library** — the description names the "Astronomy libraries" as one of the
  four bodies SSW is built from, and the *SolarSoft — Description* document links to the library's
  GSFC home page. Its provenance is visible throughout `gen/idl` in routine headers crediting
  W. Landsman, F. Varosi, M. R. Greason and D. Lindler, and in the `fxb*`/`dbase` families SSW
  carries. This is the relationship that explains why those names appear in SSW code without those
  people being SolarSoft authors (see Field 6).

*Considered and placed elsewhere:* **SunPy** — the closest thing SolarSoft has to a peer, and a
strong Field 29 candidate on the "performs similar tasks" test. It is recorded in Field 30 instead,
because a concrete exchange exists between the two and Field 30's bar is the higher one; see there.

*Considered and rejected:* **GDL (GNU Data Language)** — SSW code branches on it explicitly
(`read_punch.pro` selects `imcopy` under GDL rather than the cfitsio shared library, and a 2006
conference contribution, `2006ihy..workE..69S`, is titled "Prospects for GDL and SSW"). It was
rejected because it is a *language runtime*, the same category as IDL itself; listing it would be
like listing Python under a Python package, and would tell a reader nothing that Field 13 does not.
**MPFIT** (Markwardt) and the Coyote library — vendored general-purpose numerical and graphics
utilities, generic infrastructure rather than distinguishing domain software. **The packages SSW
distributes** (`spex`, `pfss`, `forward`, `gx_simulator`, `sunspice`, `desat`, `demreg`, and the rest
of `packages/`) — these are *components of* SolarSoft, shipped and installed as part of it, not
software related to it; listing them would misdescribe the relationship.

---

### 30. Interoperable Software (OPTIONAL)

**Values:**

1. `https://github.com/sunpy/sunpy` — SunPy
2. `https://github.com/Helioviewer-Project/helioviewer.org` — Helioviewer

*Source note:* The field was empty in HSSI. Both entries clear Field 30's bar of a *demonstrated
exchange* with a named heliophysics tool, with a specific artifact cited for each.

- **SunPy** — SunPy ships `sunpy/io/special/genx.py`, a reader written specifically for SolarSoft's
  native `genx` structure-serialisation format, so SSW output is directly importable into SunPy. The
  exchange runs the other way too: SunPy's map data model follows the SSW map/index conventions that
  `gen/idl/maps/` established, and SunPy is routinely used to consume SSW-prepped FITS. SolarSoft in
  turn ships an IDL↔Python bridge (`gen/idl/clients/python/`: `get_bridge_setup.pro`, `is_pyidl.pro`,
  `pyidl_path.pro`, plus `gen/python/bridge`) that makes running both in one session a supported
  configuration. The `genx` reader is the load-bearing evidence — it is a named module that exists
  for no purpose other than reading this software's format.
- **Helioviewer** — bidirectional, and cited from SSW's own side. `gen/idl/clients/hv/` queries the
  Helioviewer API and imports its JPEG 2000 imagery into SSW (`hv_search.pro`, `hv_get.pro`,
  `hv_source.pro`, `hv_times.pro`, `hv_beacon.pro`), while `hv_trace2_prep2jp2.pro` writes
  SSW-prepped data out as JP2 *for* Helioviewer. There is also a `packages/helioviewer` branch
  (updated 2022) with both `idl/` and `py/` components.

*Considered and rejected:* **tplot / SPEDAS.** SolarSoft distributes a `packages/tplot` branch, which
would look like a strong cross-ecosystem link. Reading it shows it is a vendored copy of the Berkeley
WIND/3DP tplot library — its documentation files are `3dp_header.html`, `3dp_ref_man.html` and
`3dp_tutorial.html` (1997–2002) and its content directories were last touched in 2005–2006. It is a
frozen historical snapshot of tplot's ancestor rather than a maintained interoperation with today's
SPEDAS, and claiming the latter from the former would mislead. Recorded here so a future agent that
finds `SSW_TPLOT` in `setup.ssw_env` does not reach the optimistic conclusion without opening the
branch. **IDL and Java** — runtime and bridge technology, not peer tools. **The VSO, JSOC, HEK and
the Solar Orbiter Archive** — data services, recorded in Field 17 and Field 32, not interoperating
software packages.

---

### 31. Related Instruments (OPTIONAL)

Every entry below is a controlled-vocabulary instrument row (`type` 1) carrying a
`https://spase-metadata.org/` identifier. The names are the vocabulary's own, reproduced exactly —
several of them read oddly, and the notes throughout this section explain which ones and why they must
not be tidied.

**Solar Dynamics Observatory** — branches `sdo/aia`, `sdo/hmi`, `sdo/eve`; `SSW_SDO_INSTR` in
`setup.ssw_env`.

| Name | SPASE identifier |
|---|---|
| Atmospheric Imaging Assembly | https://spase-metadata.org/SMWG/Instrument/SDO/AIA |
| HMI | https://spase-metadata.org/SMWG/Instrument/SDO/HMI |
| EVE | https://spase-metadata.org/SMWG/Instrument/SDO/EVE |

**SOHO** — `SSW_SOHO_INSTR "soho/cds soho/eit soho/sumer soho/lasco soho/mdi soho/uvcs"`; all six are
selectable on the installation form and all six branches exist in the tree.

| Name | SPASE identifier |
|---|---|
| Extreme Ultraviolet Imaging Telescope | https://spase-metadata.org/SMWG/Instrument/SOHO/EIT |
| Large Angle Spectroscopic Coronagraph | https://spase-metadata.org/SMWG/Instrument/SOHO/LASCO |
| Coronal Diagnostic Spectrometer | https://spase-metadata.org/SMWG/Instrument/SOHO/CDS |
| Solar Ultraviolet Measurement of Emitted Radiation | https://spase-metadata.org/SMWG/Instrument/SOHO/SUMER |
| Michelson Doppler Imager | https://spase-metadata.org/SMWG/Instrument/SOHO/MDI |
| Ultraviolet Coronagraph Spectrometer | https://spase-metadata.org/SMWG/Instrument/SOHO/UVCS |

**Yohkoh** — `SSW_YOHKOH_INSTR "yohkoh/bcs yohkoh/hxt yohkoh/sxt yohkoh/wbs"`. Yohkoh is one of the
four libraries SSW's description names as its foundation.

| Name | SPASE identifier |
|---|---|
| Soft X-Ray Telescope on Yohkoh | https://spase-metadata.org/SMWG/Instrument/Yohkoh/SXT |
| Bragg Crystal Spectrometer on Yohkoh | https://spase-metadata.org/SMWG/Instrument/Yohkoh/BCS |
| Hard X-Ray Telescope | https://spase-metadata.org/SMWG/Instrument/Yohkoh/HXT |
| Wide Band Spectrometer on Yohkoh | https://spase-metadata.org/SMWG/Instrument/Yohkoh/WBS |

**Hinode** — `SSW_HINODE_INSTR "hinode/eis hinode/xrt hinode/sot"`.

| Name | SPASE identifier |
|---|---|
| EUV Imaging Spectrometer | https://spase-metadata.org/SMWG/Instrument/Hinode/EIS |
| Solar Optical Telescope | https://spase-metadata.org/SMWG/Instrument/Hinode/SOT |
| X-Ray Telescope | https://spase-metadata.org/SMWG/Instrument/Hinode/XRT |

*Hinode XRT normalisation:* three rows once described this instrument —
`X-Ray Telescope` (bare), and `Hinode X-ray Telescope` and `X-Ray Telescope (XRT)` (both on the
`.html` identifier). Per the `.html` normalisation rule they were one resource and the bare row is
what is recorded; the `.html` twins have since been retired in the vocabulary-wide consolidation.

**Solar Orbiter** — `SSW_SO_INSTR "so/stix so/spice so/solohi"`; the `so/stix` branch was modified
2026-07-13, making it one of the most actively maintained parts of the tree.

| Name | SPASE identifier |
|---|---|
| STIX | https://spase-metadata.org/ESA/Instrument/SolarOrbiter/STIX |
| Spectral Imaging of the Coronal Environment | https://spase-metadata.org/SMWG/Instrument/SolarOrbiter/SPICE |
| The Solar Orbiter Heliospheric Imager | https://spase-metadata.org/NASA/Instrument/SolarOrbiter/SoloHI |
| Extreme Ultraviolet Imager | https://spase-metadata.org/ESA/Instrument/SolarOrbiter/EUI |
| Polarimetric and Helioseismic Imager | https://spase-metadata.org/ESA/Instrument/SolarOrbiter/PHI |

*SPICE normalisation:* the bare row `Spectral Imaging of the Coronal Environment` was preferred over
the since-retired `SPICE (Spectral Imaging of the Coronal Environment)` twin on the `.html` identifier.

*EUI and PHI — scope of support, stated plainly so a reviewer can judge it.* SolarSoft has no data
branch for either instrument. They are included because `gen/idl/sunglobe/` — an observation-planning
tool built by the Solar Orbiter SPICE team ("Project : ORBITER - SPICE ... 3D Sun pointing tool") —
implements named, instrument-specific field-of-view classes for them:
`sunglobe_eui_euv_fov__define.pro` and `sunglobe_eui_euv_config_fov.pro` for EUI's EUV channels,
`sunglobe_eui_lya_fov__define.pro` and `sunglobe_eui_lya_config_fov.pro` for its Lyman-α channel, and
`sunglobe_phi_fov__define.pro` with `sunglobe_phi_config_fov.pro` for PHI. That is instrument-specific
geometry code written by a mission team, not a tutorial name-drop — but it is planning support, not
data reduction. A reviewer who reads Field 31 strictly as data support should drop these two; no
other entry depends on them.

**Parker Solar Probe** — the `psp/wispr` branch; WISPR is selectable on the installation form.

| Name | SPASE identifier |
|---|---|
| PSP WISPR | https://spase-metadata.org/SMWG/Instrument/ParkerSolarProbe/WISPR |

*Choice of row:* the suite-level row is recorded. The vocabulary also carries per-telescope rows
(`.../WISPR/InnerTelescope`, `.../WISPR/OuterTelescope`), which are sub-entities of the same suite
rather than competing candidates; SSW's branch supports WISPR as a whole.

**PROBA 2** — `SSW_PROBA2_INSTR "proba2/swap proba2/lyra"`.

| Name | SPASE identifier |
|---|---|
| Proba 2 Sun Watcher using APS detectors and Image Processing | https://spase-metadata.org/SMWG/Instrument/PROBA2/SWAP |
| Sun Watcher using APS detectors and image Processing | https://spase-metadata.org/SMWG/Instrument/PROBA2/LYRA |

*The LYRA row's display name is upstream's, not a local error:* its stored name
`Sun Watcher using APS detectors and image Processing` is the expansion of SWAP — a different
PROBA 2 instrument — apparently misassigned in the upstream registry's record for LYRA, so the
identifier `.../SMWG/Instrument/PROBA2/LYRA` is the correct and durable half of this entry, and a
future refresh should neither "correct" that identifier to match the name nor read the name as
corruption of this record — a local rename would only be transient.

**STEREO** — `SSW_STEREO_INSTR "stereo/impact stereo/plastic stereo/secchi stereo/swaves stereo/ssc"`.
Each instrument is recorded for both spacecraft, which is the evidence-backed expansion the resolution
ladder calls for: SSW's STEREO branch supports the Ahead and Behind observatories, both of which have
their own vocabulary rows.

| Name | SPASE identifier |
|---|---|
| Stereo-A Sun Earth Connection Coronal and Heliospheric Investigation | https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI |
| Stereo-B Sun Earth Connection Coronal and Heliospheric Investigation | https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI |
| Plasma and Supra-Thermal Ion Composition | https://spase-metadata.org/SMWG/Instrument/STEREO-A/PLASTIC |
| Plasma and Supra-Thermal Ion Composition | https://spase-metadata.org/SMWG/Instrument/STEREO-B/PLASTIC |
| STEREO-A In situ Measurements of Particles and CME Transients | https://spase-metadata.org/SMWG/Instrument/STEREO-A/IMPACT |
| STEREO-B In situ Measurements of Particles and CME Transients | https://spase-metadata.org/SMWG/Instrument/STEREO-B/IMPACT |
| STEREO-A Waves | https://spase-metadata.org/SMWG/Instrument/STEREO-A/SWAVES |
| STEREO-B Waves | https://spase-metadata.org/SMWG/Instrument/STEREO-B/SWAVES |

*Choice among duplicates:* SECCHI, PLASTIC and IMPACT are recorded at **suite level**, not as their
component telescopes (EUVI, COR1, COR2, HI-1, HI-2 for SECCHI; HET, LET, SEPT, SWEA, STE, SIT, MAG for
IMPACT), because SSW's branches are organised by suite. Where both an `SMWG/...` and a
`CNES/Instrument/CDPP-AMDA/...` or `CDPP-Archive/...` row exist for the same instrument (PLASTIC and
SWAVES both have such twins), the `SMWG` row is taken as the tie-breaker.

**GOES** — `SSW_GOESR_INSTR "goesr/suvi"`, `SSW_GOESN_INSTR "goesn/sxi"`,
`SSW_GOES_INSTR "goes/sxig12 goes/sxig13"`, plus the 89-routine `gen/idl/synoptic/goes/` library.

| Name | SPASE identifier |
|---|---|
| Solar Ultraviolet Imager | https://spase-metadata.org/NOAA/Instrument/GOES/16/SUVI |
| Solar Ultraviolet Imager | https://spase-metadata.org/NOAA/Instrument/GOES/17/SUVI |
| Solar Ultraviolet Imager | https://spase-metadata.org/NOAA/Instrument/GOES/18/SUVI |
| Solar Ultraviolet Imager | https://spase-metadata.org/NOAA/Instrument/GOES/19/SUVI |
| GOES 12 Solar X-Ray Imager | https://spase-metadata.org/SMWG/Instrument/GOES/12/SXI |
| Solar X-ray Monitor on GOES 5 | https://spase-metadata.org/SMWG/Instrument/GOES/5/XRS |
| Solar X-ray Sensor on GOES | https://spase-metadata.org/SMWG/Instrument/GOES/13/XRS |
| Solar X-ray Sensor on GOES | https://spase-metadata.org/SMWG/Instrument/GOES/14/XRS |
| Solar X-ray Sensor on GOES | https://spase-metadata.org/SMWG/Instrument/GOES/15/XRS |

*SUVI expansion evidence:* four rows share the name `Solar Ultraviolet Imager`, one per spacecraft,
and the installation form names the set explicitly — `[ SUVI GOES {16,17,18,19} ]`. All four are
recorded, which is what the ladder prescribes when in-source evidence selects the members.

*XRS expansion evidence:* `gen/idl/synoptic/goes/goes_sat.pro` declares
`sats=['17','16','15','14','13','12','11','10','9','8','7','6','5']` (extended with `'3','2','1','92','91'`
when pre-1980 satellites are wanted), and the GOES object, `rd_goes`, `gfits_r/w`, `plot_goes` and
`goes_chianti_tem` operate across that range. **The vocabulary carries four XRS instrument rows —
GOES 5, 13, 14 and 15 — and all four are recorded.** GOES 5 satisfies exactly the same test as the
other three: `'5'` is an explicit member of `goes_sat`'s default satellite list, so SSW's GOES X-ray
support covers it by the same evidence.

*A caution about the GOES 5 row's name.* It is stored as **`Solar X-ray Monitor on GOES 5`** —
"Monitor", and carrying the spacecraft number — whereas the other three are each stored as
`Solar X-ray Sensor on GOES` with no number. The names were read from the live vocabulary and copied
as stored. **Do not normalise GOES 5 to "Solar X-ray Sensor on GOES" for consistency**: the row name
must match what is stored, and the four rows are distinguished by identifier in any case.

**Where the extraction stopped, and why:** no XRS rows exist for GOES 1–4, 6–12 or 16–19, so the
remainder of SSW's GOES X-ray support is carried at platform level in Field 32 rather than expanded
here.

**Single-instrument missions.**

| Name | SPASE identifier | Evidence |
|---|---|---|
| Interface Region Imaging Spectrograph | https://spase-metadata.org/SMWG/Instrument/IRIS/IRIS | `SSW_IRIS_INSTR "iris/iris"`; the `iris/` branch carries `data/`, `gse/`, `ops/`, `response/` |
| High-Energy Solar Spectroscopic Imager | https://spase-metadata.org/SMWG/Instrument/RHESSI/HESSI | `SSW_HESSI_INSTR "hessi/hessi"`; the `hessi/` branch is one of the largest in the tree |
| TRACE Imaging Telescope on TRACE | https://spase-metadata.org/SMWG/Instrument/TRACE/Telescope | `SSW_TRACE_INSTR "trace/trace" # enabled 29-oct-1996` |
| Solar Mass Ejection Imager | https://spase-metadata.org/SMWG/Instrument/Coriolis/SMEI | `SSW_SMEI_INSTR "smei/smei"`; the `smei/` branch carries `bham/`, `hafb/`, `ucsd/` |

**Ground-based radio.**

| Name | SPASE identifier | Evidence |
|---|---|---|
| Nancay Radioheliograph | https://spase-metadata.org/SMWG/Instrument/SRN/NRH | `radio/nrh` in `SSW_RADIO_INSTR`; the branch was refreshed 2024-07-16 and is one of the more actively maintained radio branches |
| NORH on NOB_RH | https://spase-metadata.org/SMWG/Instrument/NOB_RH/NORH | `radio/norh` in `SSW_RADIO_INSTR`; the branch exists and is populated on the master tree |

*Note on the Nançay instrument row:* the instrument-level match is unique. Both the instrument and
the observatory are recorded; the observatory-level reasoning, including a name defect on a
neighbouring row, is set out in Field 32.

**Durable search-method warning, learned from NoRH — read this before recording any ground-based
omission.** The Nobeyama Radioheliograph was omitted from an earlier state of this record on the
strength of searches for `Nobeyama`, `Radioheliograph`, `Radiopolarimeter` and `Owens`, all of which
returned nothing applicable. That was a **false negative**: the rows exist, but neither of them
contains the word "Nobeyama". They are named with the SPASE facility code instead —
`NORH on NOB_RH` (instrument) and `NOB_RH` (observatory). **A spelled-out search term will not find a
row whose name is only an abbreviation or a facility code, and many SPASE ground-station rows are
named that way.** Always search the abbreviation, the facility/station code and any underscore or
dot-separated variant alongside the expansion, and search the identifier path as well as the name —
the identifier is often the only place a recognisable token appears.

The same standard governs every omission recorded below: each was sought under its expansion *and*
under its abbreviation, facility code or identifier-path form. The non-expansion battery comprises
these **45 terms** — `NORP`, `NOB_`, `NOBEYAMA`, `OVSA`, `EOVSA`, `OVRO`, `OWENS`, `MWA`, `MURCH`,
`ETHZ`, `ETH_`, `PHOENIX`, `FHNW`, `SOON`, `MEES`, `SVST`, `LAPALMA`, `LA_PALMA`, `SST`, `XRP`,
`UVSP`, `HXRBS`, `HXIS`, `ACRIM`, `GRS`, `/SMM`, `SOLARMAX`, `BATSE`, `CGRO`, `SPARTAN`, `SPRTN`,
`HIC`, `HI-C`, `HXRS`, `FMG`, `LST`, `HXI`, `ASOS`, `ASO-S`, `VBI`, `VISP`, `VTF`, `NIRSP`, `DKIST`
and `/SXI` — of which 36 return no rows at all. **Among the omissions, NoRH is the one entry this
battery recovers**; every other omission below holds under abbreviation search as well as expansion
search. (Two of the 45, `DKIST` and `/SXI`, are not omission probes: they return the DKIST observatory
row and the GOES-12 SXI row that this record does use.)

Nine of the 45 return rows, and the ones that are not genuine matches illustrate the failure mode from
the other direction — **a short token matches by substring accident rather than by identity**. `SOON`
returns five rows, all of them the "Hydrometeorological ARray for Isv-Monsoon AUtomonitoring"
(*Mon-soon*); `HIC` returns twenty, ten of them Chichijima stations; `LST` returns nine, including
Holsteinsborg and Mil**lst**one Hill and SO**LST**ICE; `GRS` returns one, the Wind *TGRS* spectrometer,
matched through its abbreviation field rather than its name; `SST` returns ten, every one a THEMIS
Solid State Telescope or on-board-moments row; and `MURCH` returns seven Murchison Bay magnetometer
and observatory rows. **None of them is the instrument being sought** — which is why a hit on a short
token has to be inspected rather than counted.

---

**Instruments considered and omitted, with what was searched.** Each of the following is genuinely
supported by SolarSoft — these are not relevance rejections — but no defensible vocabulary row could
be found, so they are omitted rather than invented. A documented omission is the correct outcome
here; the searches are recorded so a future agent can tell "already looked for" from "not yet
checked", and can re-check after a vocabulary refresh.

- **Solar Maximum Mission instruments** — XRP, UVSP, HXRBS, CP, GRS, HXIS, ACRIM
  (`SSW_SMM_INSTR`; all seven branches exist under `smm/`). Searched: `SMM`, `/SMM`,
  `Solar Maximum`, `Solar Max`, `1980-014A`, `ACRIM`, `HXIS`, `UVSP`, `HXRBS`,
  `Hard X-ray Burst`, `Coronagraph/Polarimeter` — no rows of either type. SMM has no observatory row
  either, so the platform fallback is unavailable.
- **CGRO / BATSE** — `SSW_CGRO_INSTR "cgro/batse"`; the branch exists. Searched: `BATSE`, `CGRO`,
  `Compton`, `Gamma Ray Observatory`, `Burst and Transient` — no rows.
- **SPARTAN** — `SSW_SPARTAN_INSTR "spartan/spartan"`. Searched: `SPARTAN`, `Spartan 201` — no rows.
- **Hi-C (High-resolution Coronal Imager)** — `SSW_HIC_INSTR "hic/hic"`; the `hic/` branch carries
  `caldata/`, `idl/`, `response/`. Searched: `Hi-C`, `High Resolution Coronal Imager`,
  `High Resolution Coronal` — no rows.
- **HXRS** — `SSW_HXRS_INSTR "hxrs/hxrs"`; the `hxrs/` branch carries `dbase/`, `idl/`, `setup/`.
  Searched: `HXRS`, `MTI`, `Multispectral Thermal` — the `MTI` matches returned are IUGONET OMTI
  airglow imagers, an unrelated instrument family.
- **ASO-S (Advanced Space-based Solar Observatory)** — `SSW_ASOS_INSTR "asos/fmg asos/lst asos/hxi"`,
  with `asos/lst/idl/` modified 2026-05-05, so this is current, active support. Searched: `ASOS`,
  `ASO`, `Advanced Space`, `Lyman-alpha Solar Telescope`, `Full-disk Magnetograph`,
  `Hard X-ray Imager` — no ASO-S rows at instrument or observatory level. **This is the most
  significant omission in this record**, because it is recent and growing; it should be the first
  thing re-checked after any vocabulary refresh.
- **DKIST instruments** — VBI, ViSP, VTF, Cryo-NIRSP, DL-NIRSP (`SSW_DKIST_INSTR`; all five branches
  exist). Searched: `Visible Broadband`, `ViSP`, `Visible Spectro`, `Visible Tunable`, `NIRSP`,
  `Cryogenic Near`, `/DKIST/` — the vocabulary has DKIST only at observatory level. Handled by the
  platform fallback in Field 32.
- **GOES-N SXI for GOES 13, 14 and 15** — `SSW_GOESN_INSTR "goesn/sxi"` and the installation form's
  `[ SXI GOES {13,14,15} ]`. Only the GOES-12 SXI row exists in the vocabulary. Handled by the
  platform fallback in Field 32.
- **PUNCH WFI-1/2/3 and NFI** — instrument rows for all four *do* exist
  (`.../NASA/Instrument/PUNCH/WFI/1`, `/2`, `/3`, `.../PUNCH/NFI`), and they were deliberately not
  recorded. `punch/idl/read_punch.pro` reads mission-level products — "PUNCH_L3_MPM_…fits",
  QuickPUNCH, "Total Brightness and Polarized Brightness image datacube (for higher level
  products)" — rather than per-telescope data, so the association belongs at mission level. PUNCH is
  recorded in Field 32.
- **Ground-based optical: SOON, La Palma SVST, Mees, NSO** — `SSW_OPTICAL_INSTR
  "optical/soon optical/lapalma optical/nso optical/mees"`. Searched: `SOON`, `La Palma`, `Swedish`,
  `Mees`, `Haleakala`, `Sacramento`, `National Solar`, `Kitt Peak`, `SOLIS`, `GONG`. `SOON`,
  `La Palma`, `Swedish` and `Mees` return nothing applicable. NSO is a special case worth recording:
  the vocabulary does carry NSO-facility rows (Kitt Peak Vacuum Telescope, SOLIS VSM/ISS/FDP, the
  GONG network), but SSW's entire NSO support is a single generic routine — `optical/nso/idl/read_nso.pro`,
  "read one or more NSO FITS into structure/data cube" — which names no facility or instrument.
  Binding it to any specific NSO row would be a guess, so it is omitted.
- **Ground-based radio other than NRH and NoRH: NoRP, OVSA, EOVSA, OVRO, MWA, ETHZ, FHNW** —
  `SSW_RADIO_INSTR "radio/ethz radio/fhnw radio/nrh radio/norh radio/eovsa radio/ovsa radio/ovro
  radio/norp radio/mwa radio/lofar"`. All of these branches exist on the master tree except
  `radio/ovro`, which is declared in `setup.ssw_env` but returns 404 — another declared-but-unpopulated
  slot, like the PSP entries below. Searched:
  `Nobeyama`, `Radioheliograph`, `Radiopolarimeter`, `Owens`, `Expanded Owens`, `Solar Array`,
  `Murchison`, `MWA`, `ETH`, `Zurich`, `Phoenix`, together with their abbreviation and facility-code
  forms (`NORP`, `NOB_`, `OVSA`, `EOVSA`, `OVRO`, `ETHZ`, `FHNW`) — no applicable rows.
  NoRP is worth calling out because it is the near neighbour of the NoRH row that the abbreviation
  search *did* recover: `NOB_` returns exactly two rows, both for the radioheliograph, so the
  Nobeyama Radiopolarimeters have no vocabulary entry of their own. LOFAR resolves at observatory
  level and is recorded in Field 32; NoRH resolves at both levels and is recorded in Fields 31 and 32.
- **Parker Solar Probe FIELDS, IS☉IS and SWEAP** — declared in `setup.ssw_env`
  (`SSW_PSP_INSTR "psp/fields psp/isis psp/wispr psp/sweap"`) but **the branches do not exist**: on
  the master tree `psp/` contains only `gen/` and `wispr/`, and `psp/fields`, `psp/isis` and
  `psp/sweap` are absent. These are declared-but-unpopulated slots, so they are excluded on relevance
  grounds, not vocabulary grounds. Vocabulary rows do exist for all three, which makes this an easy
  mistake to make from `setup.ssw_env` alone — check the tree before adding them.
- **Solar Orbiter Metis and EPD** — vocabulary rows exist, and the Solar Orbiter Archive client
  (`soar_list.pro`, `soar_search.pro`) will retrieve their files, but that client takes an instrument
  acronym as an argument and is instrument-agnostic; its doc examples use `'EUI'` illustratively.
  Excluded as "configurable for" rather than "designed to support". EUI and PHI are listed above on
  entirely different evidence (dedicated FOV classes), not on the SOAR client.
- **Virtual observatories: VSO, CoSEC, EGSO, HELIO, Ontology** (`SSW_VOBS_INSTR`) — these are data
  services, not instruments or observatories. They are recorded in Field 17.

---

### 32. Related Observatories (OPTIONAL)

Resolved against the same vocabulary with `type` 2. Names copied verbatim.

| Name | SPASE identifier | Evidence |
|---|---|---|
| Solar Dynamics Observatory | https://spase-metadata.org/SMWG/Observatory/SDO | `sdo/` branch: `aia/`, `gen/`, `hmi/`; the `ontology` package provides JSOC and HEK access for SDO |
| Solar and Heliospheric Observatory | https://spase-metadata.org/SMWG/Observatory/SOHO | six SOHO instrument branches; SOHO is one of the four libraries SSW is built from |
| 1991-062A | https://spase-metadata.org/SMWG/Observatory/Yohkoh | four Yohkoh instrument branches; Yohkoh is one of SSW's four foundation libraries |
| Hinode | https://spase-metadata.org/SMWG/Observatory/Hinode | `hinode/` branch: `eis/`, `gen/`, `sot/`, `xrt/` |
| Transition Region and Coronal Explorer | https://spase-metadata.org/SMWG/Observatory/TRACE | `trace/` branch, enabled 1996-10-29 |
| Reuven Ramaty High Energy Solar Spectroscope Imager | https://spase-metadata.org/SMWG/Observatory/RHESSI | `hessi/` branch with `dbase/`, `idl/`, `java/`, `offline/` |
| Interface Region Imaging Spectrograph | https://spase-metadata.org/SMWG/Observatory/IRIS | `iris/` branch including `gse/` and `ops/` |
| PROBA 2 | https://spase-metadata.org/SMWG/Observatory/PROBA2 | `proba2/lyra`, `proba2/swap` |
| Solar Terrestrial Relations Observatory A | https://spase-metadata.org/SMWG/Observatory/STEREO-A | `stereo/` branch; `secchi/` modified 2025-07-07 |
| Solar Terrestrial Relations Observatory B | https://spase-metadata.org/SMWG/Observatory/STEREO-B | as above |
| Solar Orbiter | https://spase-metadata.org/ESA/Observatory/SolarOrbiter | `so/` branch (`stix/` 2026-07-13, `spice/`, `solohi/`); dedicated SOAR archive client |
| Parker Solar Probe | https://spase-metadata.org/SMWG/Observatory/ParkerSolarProbe | `psp/wispr`; `gen/setup/setup.psp_env` |
| 2003-001A | https://spase-metadata.org/SMWG/Observatory/Coriolis | `smei/` branch — Coriolis is SMEI's platform |
| Daniel K Inouye Solar Telescope | https://spase-metadata.org/SMWG/Observatory/DKIST | `dkist/` branch with all five instrument sub-branches |
| PUNCH Mission | https://spase-metadata.org/NASA/Observatory/PUNCH | `punch/` branch (`idl/`, `response/`, `test_data/`, files dated 2026-05-15) |
| LOFAR | https://spase-metadata.org/SMWG/Observatory/LOFAR | `radio/lofar` on the master tree; added to the installation form 2018-02-06 |
| NOB_RH | https://spase-metadata.org/SMWG/Observatory/NOB_RH | `radio/norh` in `SSW_RADIO_INSTR`; the Nobeyama Radioheliograph facility, whose instrument row is in Field 31 |
| Nancay Radioheliograph | https://spase-metadata.org/SMWG/Observatory/SRN/NRH | `radio/nrh` in `SSW_RADIO_INSTR`, refreshed 2024-07-16; the facility hosting the Field 31 instrument row |
| 2001-031A | https://spase-metadata.org/SMWG/Observatory/GOES/12 | `goes/sxig12` |
| Geostationary Operational Environmental Satellite 13 | https://spase-metadata.org/SMWG/Observatory/GOES/13 | `goes/sxig13`, `goesn/sxi`, `goes_sat.pro` |
| Geostationary Operational Environmental Satellite 14 | https://spase-metadata.org/SMWG/Observatory/GOES/14 | `goesn/sxi`, `goes_sat.pro` |
| Geostationary Operational Environmental Satellite 15 | https://spase-metadata.org/SMWG/Observatory/GOES/15 | `goesn/sxi`, `goes_sat.pro` |
| Geostationary Operational Environmental Satellite 16 | https://spase-metadata.org/SMWG/Observatory/GOES/16 | `goesr/suvi`; `goes16p_clean.pro`, `ssw_goesr_time2files.pro`, `read_goes_nc.pro` |
| Geostationary Operational Environmental Satellite 17 | https://spase-metadata.org/SMWG/Observatory/GOES/17 | as above |
| Geostationary Operational Environmental Satellite 18 | https://spase-metadata.org/NOAA/Observatory/GOES/18 | `goesr/suvi`; installation form `[ SUVI GOES {16,17,18,19} ]` |
| Geostationary Operational Environmental Satellite 19 | https://spase-metadata.org/NOAA/Observatory/GOES/19 | as above |

**Platform substitutions made here, and why.** Two entries are recorded at observatory level
specifically because the instrument they stand for has no vocabulary row:

- **DKIST** — VBI, ViSP, VTF, Cryo-NIRSP and DL-NIRSP each have an SSW branch and none has a SPASE
  instrument record. The platform record carries the association instead, which is the prescribed
  fallback and preserves the fact that SSW supports DKIST at all.
- **GOES 13, 14 and 15** — the SXI instruments SSW supports through `goesn/sxi` have no SPASE rows
  (only GOES-12 SXI does). The platform records carry that support. GOES 13/14/15 additionally
  appear via their XRS instrument rows in Field 31, so the platform entries also do real work for
  the GOES-N era generally.

**Names that look wrong but are correct.** `1991-062A` (Yohkoh), `2001-031A` (GOES 12) and
`2003-001A` (Coriolis) are the verbatim `name` values of those SPASE rows — the vocabulary stores
international designators rather than mission names for several older platforms. They are copied as
stored because the row name must match exactly; a future agent should not "fix" them to `Yohkoh`,
`GOES 12` or `Coriolis`, which would fail to match.

**Duplicate-row choices.** SOHO has both an `SMWG` and a `CNES/Observatory/CDPP-AMDA` row; RHESSI,
LOFAR and DKIST each had a bare and an `.html` row (the `.html` twins have since been retired in the
vocabulary-wide consolidation); STEREO has SMWG, `CDPP-AMDA` and `CDPP-Archive`
variants for the mission and both spacecraft. In every case the bare `SMWG` (or, where no SMWG row
exists, the single applicable) row was taken, per the normalisation and tie-breaker rules.

**Considered and not recorded.**
- **The mission-level STEREO row** (`.../SMWG/Observatory/STEREO`) — the per-spacecraft A and B rows
  are more specific and match how SSW's instrument support is organised; adding the mission row too
  would be redundant.
- **GOES 1–11** — observatory rows exist for all of them and `goes_sat.pro` will read their XRS data,
  so listing them would be defensible. The line was drawn at GOES-12 because that is where SSW has
  *dedicated instrument branches* (`goes/sxig12` onward), which is the criterion used for Field 32.
  A future refresh that prefers data-readability as the criterion could extend downward; this note
  records that the choice was deliberate rather than an oversight.

  **Note the deliberate asymmetry with Field 31**, so it is not read as an error: GOES 5 *does* appear
  there, as the instrument row `Solar X-ray Monitor on GOES 5`, while GOES 5 has no entry here. The
  two fields are populated by different rules. Field 31 records every instrument SSW supports for
  which a SPASE instrument row exists, and one exists for GOES 5's XRS; Field 32 records the platforms
  SSW serves through a dedicated branch, and there is no GOES-5-specific branch. Adding the GOES 5
  observatory row would be a reasonable extension, not a correction.
- **Nançay Radioheliograph at observatory level was omitted in an earlier state of this record, and
  that omission was wrong.** The reasoning then was that two observatory rows share the display name
  `Nancay Radioheliograph` — `.../SMWG/Observatory/SRN/NRH` and `.../SMWG/Observatory/SRN/NRT` — and
  that this made the association ambiguous. It does not. **A collision is one entity with several
  candidate rows; this is two distinct entities that happen to share a display string**, and only the
  former is unresolvable. `SRN/NRT` is the Nançay Radio Telescope, a different facility, and its
  display name looks like the same class of upstream data defect diagnosed for the PROBA2 LYRA row in
  Field 31 — a row carrying a neighbour's name.

  `.../SMWG/Observatory/SRN/NRH` is selected on **identifier-path correspondence** with the already
  resolved Field 31 instrument row `.../SMWG/Instrument/SRN/NRH`: same provider (`SRN`), same facility
  segment (`NRH`), differing only in the `Instrument`/`Observatory` segment. That is multi-signal
  matching on the identifier path, which the resolution ladder treats as evidence, not a guess between
  look-alike names. Recorded so a future agent does not re-derive the earlier omission from the shared
  display name alone.
- **SMM, CGRO, SPARTAN, Hi-C, HXRS, ASO-S** — no observatory rows exist for any of them, so the
  platform fallback that rescued DKIST and GOES-N is unavailable. See the omission list in Field 31
  for exactly what was searched.
- **Kitt Peak, SOLIS, GONG, Big Bear** — these rows exist, but SSW's NSO support is a single generic
  FITS reader that names no facility (see Field 31), so binding any of them would be a guess.

---

### 33. Logo (OPTIONAL)

**Value:** Not found

*Source note:* The installation form and the description document were examined for a project mark;
the installation form contains no `<img>` elements at all, and the description document's images are
navigational and structural rather than a logo. No logo was found on any official SolarSoft page
consulted.
