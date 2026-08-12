# HSSI Metadata Extraction Results

**HSSI Software ID:** f2cb2434-7d2e-4d87-8b97-6546d4931b29
**Repository:** https://github.com/NCAR/SolarProtons
**Source Revision:** f84c06ce14e58bba8123cefc1ed06d436df04503
**Extraction Date:** 2026-08-11
**Validation Date:** 2026-08-12
**Validation Status:** PASS

---

**Scope note — how to read the evidence below.** `NCAR/SolarProtons` is a 13-file repository with a
single commit ("first commit", Francis Vitt, 2023-07-21) and no tags, releases, packaging metadata,
`LICENSE`, `CITATION.cff`, `codemeta.json`, `AUTHORS`, `.zenodo.json`, CI configuration, `docs/`
directory or GitHub repository description, homepage or topics. There is therefore no packaging or
citation metadata layer to draw on, and every substantive field value below is grounded either in the source code
itself (read in full: `Makefile`, `README.md`, `make-proton.csh`, `scripts/spe.ncl`,
`scripts/spe_pad.ncl`, and the eight Fortran sources `prargs.f`, `pratmo.f`, `prfit.f`,
`prinp_cesm.f`, `prmain.f`, `prread.f`, `prspec.f`, `prwrite.f`) or in an authoritative external
source that is named in the note. Where the code and the README disagree, the code is treated as
authoritative and the discrepancy is recorded.

**Two kinds of evidence appear below, and they age differently.** Statements about the repository
itself — file contents, file lists, greps, code constants, commit history — are fixed at the source
revision recorded above and cannot drift. Statements about anything else are observations made on the
Extraction Date: what HSSI currently stores for this record, what a controlled vocabulary contained,
what a database row was linked to, and what an external service (DataCite, Zenodo, ADS, ORCID, ROR,
the GitHub API, the PyHC registries, SoMEF) returned. **Every such statement should be read as "as of
the Extraction Date", and re-checked rather than assumed, even where the sentence does not repeat the
qualifier.** Individual notes below restate it where the claim carries particular weight — where a
value depends on it, or where a future agent might otherwise treat it as a standing guarantee.

**What the software actually does**, established from the code and used throughout as the basis for
Fields 4, 5, 17-19 and 22:

- `scripts/spe.ncl` is the NCAR Command Language driver. Its four switchable stages are `getFiles`
  (fetch NOAA 5-minute GOES particle text files by `wget` from
  `https://umbra.nascom.nasa.gov:/sdb/goes/particle/`), `processFiles` (parse the ASCII to netCDF,
  average to hourly and daily, concatenate to yearly), `calcIons` (invoke the Fortran binary
  `bin/go_proton`), and `combineFiles` (concatenate across years).
- `spe_noaa2nc` packs six integral proton channels (>1, >5, >10, >30, >50, >100 MeV) into
  `pflux(time, penergy)` and three electron channels (>0.8, >2.0, >4.0 MeV) into
  `eflux(time, eenergy)`, on a `days since 1850-01-01` Gregorian time axis with `time_bnds`.
- `spe_primary4date` is a hard-coded lookup table selecting which GOES spacecraft supplied the
  primary proton flux for a given date: `psat = (/ "G7", "G8", "G10", "G8", "G11", "Gp" /)` at
  `sdate = (/ 19940101, 19950301, 20030408, 20030510, 20030619, 20100414 /)`.
- `spe_2hourly` / `spe_2daily` perform fill-value-aware temporal averaging; `spe_catyear` and
  `spe_cations` shell out to NCO's `ncrcat`; `spe_check4fill` reports missing-value counts as a
  quality check; `spe_ions2nc` converts legacy ASCII ion-production tables
  (`ions_txt/IonPair-gm_Year-<year>.dat`) to netCDF for comparison.
- `go_proton` (the Fortran program) fits the six integral channels with exponential spectral forms in
  three energy bands (`prfit.f`, `prinp_cesm.f`: `IDIVID = 3`, `EN(2) = 10.0`, `EN(3) = 50.0`),
  builds a differential spectrum on a 60-point logarithmic grid from 1 to 300 MeV (`IMAX = 60`,
  `E(1) = 1.0`, `EMAX = 300.`, `prspec.f`), and integrates proton energy deposition over 35 pitch
  angles (`KMAX = 35`, isotropic `IBTA = 0`) through a 59-level model atmosphere spanning 0-116 km at
  2 km spacing (`pratmo.f`, `JMAX = 59`). Ion pair production follows from `DISS(1) = 35.0E-6` MeV,
  i.e. 35 eV per ion pair. The geomagnetic cutoff machinery is present but disabled: `NLAT = 1`,
  `GLAT(1) = 90.`, `GCUT(1) = 0.0`, so the rates represent polar cap conditions.
- `prwrite.f` writes three selectable netCDF layouts: WACCM4 (`Prod`, `/cm3/sec`, reversed pressure
  axis, `date`/`datesec`), WACCM6 (as WACCM4 but `/g/sec` and with `time`/`time_bnds`), and CMIP6
  (`iprp`, long name "Ion pair production rate by solar protons", `g^-1 s^-1`, on `plev` in hPa with
  `calyear`/`calmonth`/`calday`).

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Not stored on the HSSI record and not derivable from the repository. The submitter of the original
HSSI entry is not exposed by the view API.*

---

### 2. Persistent Identifier (RECOMMENDED)

**Not found.**

Currently stored on HSSI as an empty string; that remains correct.

Negative research, recorded so a later refresh does not repeat it: the repository contains no DOI in
any form — no `CITATION.cff`, no `codemeta.json`, no `.zenodo.json`, no badge or DOI string in
`README.md`, and no DOI text anywhere in the tracked files. Searches of the DataCite REST API for
`SolarProtons` and for the quoted string `"NCAR/SolarProtons"` returned zero records at extraction
time, and a Zenodo records search for `SolarProtons` likewise returned zero hits; SoMEF 0.9.11, run
against the repository URL at the same time, also reported no `identifier`. The repository had no
Zenodo integration and no GitHub releases for one to have minted a DOI from, so the absence is genuine
rather than a lookup failure.

---

### 3. Code Repository (MANDATORY)

`https://github.com/NCAR/SolarProtons`

Carried over from the existing HSSI record and confirmed against the local clone's `origin` remote
(`https://github.com/NCAR/SolarProtons.git`) and, at extraction time, the GitHub API, which reported
the repository as public, not archived and not a fork, on default branch `main`. The URL resolves; no move or rename
has occurred.

---

### 4. Software Functionality (MANDATORY)

- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: File Format Conversion
- Data Processing and Analysis: Processing
- Data Processing and Analysis: Time Series Analysis
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Physics-Based

The stored HSSI value was the single top-level category `Data Processing and Analysis`. That value is
correct and is retained, but it materially under-describes the software: it omits every subcategory
and omits the fact that a substantial part of the package is a physical model. Each addition below is tied to a
specific code artifact.

- **Data Processing and Analysis: Data Access and Retrieval** — `getTxtFiles` in `scripts/spe.ncl`
  issues `wget -P noaa_txt https://umbra.nascom.nasa.gov:/sdb/goes/particle/<date>_Gp_part_5m.txt`
  (and the `_Gs_` companion). Retrieving data from a remote archive is a user-invoked stage of the
  workflow, controlled by the `getFiles` switch.
- **Data Processing and Analysis: File Format Conversion** — `spe_noaa2nc` reads the NOAA fixed-width
  ASCII product with `readAsciiHead`/`readAsciiTable` and writes netCDF; `spe_ions2nc` converts the
  legacy `IonPair-gm_Year-<year>.dat` ASCII tables to netCDF. Reading one format and writing another
  is the defining case for this subcategory.
- **Data Processing and Analysis: Data Reduction** — `spe_2hourly` and `spe_2daily` bin 5-minute
  samples into hourly and daily means with explicit missing-value counting, and `spe_hions2daily`
  averages hourly ion production to daily. This is averaging, binning and downsampling that preserves
  the information content, which is the subcategory's definition.
- **Data Processing and Analysis: Time Series Analysis** — the objects handled throughout are flux
  and production time series. The code maintains a CF-style `time` coordinate with `time_bnds`,
  `calendar = "gregorian"` and a `days since 1850-01-01 00:00:00` epoch, converts between Gregorian
  and Julian representations (`greg2jul`, `jul2greg`), computes per-hour bin membership from time of
  day, and handles gaps through fill-value-aware accumulation. `spe_pad.ncl` extends a time series
  and its bounds forward by a requested number of days.
- **Data Processing and Analysis: Energy Spectra** — `FITPFLUX` in `prfit.f` fits the six integral
  proton channels pairwise with exponential spectral forms, and `SPECTR` in `prspec.f` evaluates a
  differential spectrum on a 60-point logarithmic energy grid. This is flux-versus-energy work on
  named energy channels.
- **Data Processing and Analysis: Analysis** — the ion pair production rate is a derived physical
  quantity computed from the measured fluxes, not a repackaging of them; `spe_check4fill` adds a
  quality assessment that flags days whose sample count falls below the expected 288 five-minute
  records.
- **Data Processing and Analysis: Processing** — the package is a multi-stage pipeline
  (download, convert, average, concatenate, compute, re-average, concatenate) driven by switches at
  the bottom of `spe.ncl`.
- **Models and Simulations** and **Models and Simulations: Physics-Based** — `go_proton` is a
  physical model, not a data transform. `prmain.f` integrates proton energy loss slab by slab through
  a model atmosphere using a range-energy relation with two regimes (`prinp_cesm.f`:
  `ERNG1 = 1550.`, `RK1 = 2.71E-3`, `RB1 = 1.72`, `RK2 = 0.834`, `RB2 = 0.94`), over a pitch-angle
  grid, converting deposited energy to ion pairs at 35 eV each. `Physics-Based` rather than
  `First Principles` because the range-energy relation and the 35 eV per ion pair constant are
  empirical parameterisations of the underlying physics rather than an ab initio transport
  calculation; the code itself notes the scheme comes from Jackman's published methodology.
- **Models and Simulations: Data Guided** — the model has no internal driver. Its incident spectrum
  is derived entirely from measured GOES proton fluxes read out of the input netCDF file
  (`RDENERGY`/`RDFLUX` in `prread.f`), one time step at a time. A model whose forcing is observational
  data is precisely this subcategory.

Considered and not selected, with reasons, so a later refresh does not reopen them:

- **Data Visualization** and every subcategory of it. `scripts/spe.ncl` loads four NCL graphics and
  utility libraries (`gsn_code.ncl`, `gsn_csm.ncl`, `contributed.ncl`, `shea_util.ncl`), which is
  suggestive, but a search of both NCL scripts for plotting calls, workstation creation, or any
  `gsn_`-prefixed invocation found none. The `load` lines are unused boilerplate. The package emits
  data files and console text, never figures.
- **Coordinate Transforms** and its subcategories. The CMIP6 layout documented in the `prwrite.f`
  header comment includes a geomagnetic latitude axis, and `prinp_cesm.f` carries `GLAT`/`GCUT`/`GFRC`
  arrays, but no transformation between coordinate systems is performed anywhere; the latitude
  machinery is configured to a single polar-cap point.
- **Data Processing and Analysis: Pitch Angle Distributions.** The calculation integrates over a
  pitch angle grid, but the distribution is an *assumed input* (`IBTA = 0`, isotropic) rather than a
  distribution derived from measurements. This subcategory is for computing pitch angle distributions
  from data.
- **Data Processing and Analysis: Calibration.** The software consumes NOAA's already-calibrated flux
  product in physical units (Protons/cm2-s-sr) and applies no instrument response or gain correction.
- **Mission-related** and its subcategories. The software reads a mission's public data product but is
  not part of the GOES ground system, operations chain, or instrument team tooling.
- **Models and Simulations: Forward-Fitting.** The closest call in this field, because `FITPFLUX` in
  `prfit.f` does fit a spectrum and the subcategory's definition mentions inversion. It was rejected
  because the routine derives the two spectral parameters per energy band by closed-form algebra from
  a pair of measured integral fluxes —
  `E0(I)=(DE)/ALOG(PFLUX(I1)/PFLUX(I2))` and the corresponding expression for `F0(I)` — with no
  synthetic-observation generation, no iteration and no chi-square minimisation against a forward
  model. The subcategory's "Forward model, chi-square fitting, inversion" language describes parameter
  optimisation, which this is not. The spectral work is recorded under
  `Data Processing and Analysis: Energy Spectra` instead.
- **Models and Simulations: Empirical.** `ATMASS` in `pratmo.f` is a hard-coded climatological model
  atmosphere (a 59-value temperature profile with an exponential mass column,
  `MASS = 1013.0 * EXP(-0.2844 * (j-1))`), which is empirical in character. It was rejected because it
  is an internal fixed input to the ionization calculation and is not offered to users as an
  empirical model product; the user-facing model output is the ionization rate.
- **Servers and Environments** and its subcategories. The build is a plain Makefile with no
  container, no MPI, and no job-scheduler or deployment artifacts.

All eleven selected values were confirmed against the live `/api/models/FunctionCategory/rows/all/`
vocabulary at extraction time, and every subcategory has its parent category present in the list
above.

---

### 5. Related Region (MANDATORY)

- Solar Environment
- Earth Atmosphere
- Earth Lower and Middle Atmosphere
- Earth Thermosphere
- Earth Ionosphere

`Solar Environment` is the stored HSSI value and is retained: the particles the software processes are
solar in origin, and solar proton events are the phenomenon the package exists to quantify.

The four additions record where the software's output actually applies, which the stored single value
did not capture. `pratmo.f` builds 59 levels at 2 km spacing from 0 to 116 km altitude, so the
computed profile spans the troposphere, stratosphere and mesosphere (**Earth Lower and Middle
Atmosphere**) and continues into the lower thermosphere above roughly 90 km (**Earth Thermosphere**);
**Earth Atmosphere** records that the product is a single column covering that whole range rather than
one layer. **Earth Ionosphere** follows from the output quantity itself: the software computes ion
pair production rates, and solar proton precipitation into the polar cap is the classic source of
D-region ionization. `prinp_cesm.f` describes the runs it is configured for as "PCA EVENTS" — polar
cap absorption events, an ionospheric phenomenon.

Considered and not selected:

- **Interplanetary Space.** The protons traverse interplanetary space and are measured at
  geostationary orbit, but the software neither models nor characterises that region; it takes the
  measured flux as a boundary condition.
- **Earth Auroral Subregion.** The configuration is polar cap (`GLAT(1) = 90.`, zero geomagnetic
  cutoff), which lies poleward of the auroral oval, not within it.
- **Earth Magnetosphere** and its subregions. The geomagnetic cutoff arrays exist in
  `prinp_cesm.f` but are set so that no cutoff is applied, so no magnetospheric access calculation is
  performed.

All five values were confirmed against the live `/api/models/Region/rows/all/` vocabulary at
extraction time.

---

### 6. Authors (MANDATORY)

Four authors, reconciled as a union of what HSSI already held and what the repository evidences.
Neither previously recorded author is dropped, and two more are recorded because the source files
name them as the people who wrote the code.

**1. NSF National Center for Atmospheric Research**
- **Author Identifier:** `https://ror.org/05cvfcr44`
- **Affiliation:** none recorded

This is an organization author. HSSI infers organization status from the `ror.org` identifier, and
`https://ror.org/05cvfcr44` is the National Center for Atmospheric Research (ROR display name "NSF
National Center for Atmospheric Research"). The repository lives in the `NCAR` GitHub organization,
so the institutional credit stands alongside the three individual authors below.

*The previous value, and why it was corrected.* This author was stored with `given_name` empty and
`family_name` set to the bare acronym `NCAR`, so it read as `NCAR` rather than as the institution's
name. Two problems followed. The displayed name did not match the ROR display name for the identifier
the entry carries. More seriously, a blank given name is not expressible through a routine metadata
update at all: the update path rejects an empty given name outright, and when it matches an existing
person by identifier it fills a blank given name from whatever is supplied while leaving a non-blank
family name untouched. Any update that listed this author was caught either way. Leaving the given
name blank failed validation for the whole `authors` array, so the field could not be written at all,
and Bardeen and Jackman were held up by this row rather than by anything of their own. Supplying a
value instead wrote it into the blank field and left the acronym standing beside it as the family
name, producing a worse name than the one it replaced and no route back by the same means. The entry
was corrected directly in the database to the given name `NSF` and the family name `National Center
for Atmospheric Research` — which is both the ROR display name for `https://ror.org/05cvfcr44` and the
name of the organization record HSSI already held for that identifier, so it now matches
idempotently, and the individual authors below can be recorded alongside it.

*What remains actionable in a later refresh.* A person's stored name still cannot be changed through a
routine metadata update once it is non-blank, so any future correction to this author's name needs the
same direct database route. Check first which records reference the entry: it was referenced by
SolarProtons and by no other software record when this was written, which is what made the correction
safe to make, but that set can change and should not be assumed.

**2. Francis Vitt**
- **Author Identifier:** `https://orcid.org/0000-0002-8684-214X`
- **Affiliation:** NSF National Center for Atmospheric Research (`https://ror.org/05cvfcr44`)

Confirmed independently: the repository's sole commit
(`f84c06ce14e58bba8123cefc1ed06d436df04503`) is authored by "Francis Vitt <fvitt@ucar.edu>", and the
ORCID public record for `0000-0002-8684-214X` returned Francis Vitt with institution NCAR at
extraction time. Vitt published the code to GitHub; his name does not appear in any source file
header.

**3. Charles Bardeen**
- **Author Identifier:** `https://orcid.org/0000-0002-5330-2788`
- **Affiliation:** NSF National Center for Atmospheric Research (`https://ror.org/05cvfcr44`)

The strongest authorship evidence in the repository names Bardeen, not Vitt. Three source-file
comment headers credit him, quoted below with a slash marking each line break in the original and the
comment markers (`#`, `;`, `C`) removed. `Makefile` opens "Makefile for creating the go.proton
program. / Charles Bardeen / October 2016"; `scripts/spe.ncl` is signed "Charles Bardeen / October
2016" and states "This uses a fortran program that was initially supplied by Charley Jackman, but has
been adapted by me to calculate ion production rates from GOES solar proton data"; and `prmain.f`
carries a change log reading "OCTOBER 2016, CHARLES BARDEEN - ADDED COMMAND LINE / ADDED NETCDF FILES
/ MOVED POWER LAW FIT FROM NOAA ROUTINE". The entire NCL driver, the netCDF I/O layer (`prread.f`,
`prwrite.f`), the command-line interface (`prargs.f`) and the flux-fitting routine (`prfit.f`) are
his work.

Identity confirmation for the ORCID took a second source, because the ORCID record itself is empty
(no employment, no works, no biography). ADS returns records for `orcid:0000-0002-5330-2788` — 44 as
observed at extraction time — including WACCM6-CARMA and CARMA cloud-microphysics papers, and the
affiliation they carry for Bardeen is NCAR throughout. Bibcode `2025AGUFMGC21E.069Q` records it as
"National Center for Atmospheric Research, Boulder, United States"; bibcode `2024JGRD..12941283Z`
uses the institution's current name, placing him in the Atmospheric Chemistry Observations and
Modeling laboratory of the NSF National Center for Atmospheric Research. That is the NCAR atmospheric
modeller who wrote this code. The ORCID's emptiness is a property of the record, not a sign of a
mismatch.

**4. Charles H. Jackman**
- **Author Identifier:** `https://orcid.org/0000-0002-8631-2763`
- **Affiliation:** Goddard Space Flight Center (`https://ror.org/0171mag52`)

The repository credits Jackman twice and independently as the origin of the scientific core.
`README.md`: "a Fortran program that is based upon code originally provided by Charlie Jackman that
calculates the ionization rates." `prmain.f`, in the file's own change log: "????, CHARLEY JACKMAN -
ORIGINAL". The physics that makes this package what it is — the energy deposition loop in `prmain.f`,
the range-energy parameterisation, the pitch-angle integration, the model atmosphere in `pratmo.f`,
the spectrum construction in `prspec.f` and the 35 eV per ion pair conversion — is his, and Bardeen's
own comments describe his contribution as adaptation and plumbing around it.

*The alternative was considered and rejected.* Jackman could have been credited in the description or
in Related Publications only, treating SolarProtons as a derivative work whose author is the adapter.
That was rejected because the repository does not describe the relationship that way: `prmain.f`
lists him as the first entry in the file's version history under the label "ORIGINAL", which is an
authorship claim in the code's own terms, and the ionization calculation he wrote is the software's
reason for existing rather than an incidental borrowing. Recording him as an author is the accurate
attribution.

Identity confirmed from the ORCID public record for `0000-0002-8631-2763` as it read at extraction
time: credit name "C.H. Jackman", biography "Physical Scientist at NASA Goddard Space Flight Center since 1980", keywords
"Ozone, solar particles, middle atmosphere", researcher URL
`http://acdb-ext.gsfc.nasa.gov/People/Jackman/`, and works including "Effects of the September 2005
Solar Flares and Solar Proton Events on the Middle Atmosphere in WACCM". Note for anyone matching by
surname later: HSSI held, at extraction time, a person row for *Caitriona* Jackman
(`https://orcid.org/0000-0003-0635-7361`), who is a different researcher and must not be matched to
this entry. The affiliation string "Goddard Space Flight Center" is used because that is both the ROR
display name for `0171mag52` and the name of the organization row HSSI held for that ROR at
extraction time, so it should match idempotently rather than creating a near-duplicate.

Negative research on author sources: the repository has no `CITATION.cff`, `codemeta.json`,
`AUTHORS`, `CONTRIBUTORS`, `.zenodo.json`, or packaging file of any kind, so the git history and the
in-file headers are the whole evidentiary base. The git history contributes exactly one name (Vitt)
because the repository was created with a single squashed "first commit" in 2023, seven years after
the code was written; treating the committer as the sole author would misattribute the work.

---

### 7. Software Name (MANDATORY)

`SolarProtons`

The name HSSI already held, and it is correct: it matches the GitHub repository name exactly, no
source file or README line offers a different or longer product name, and SoMEF independently
extracted `SolarProtons` with confidence 1.

---

### 8. Description (MANDATORY)

**Description:**

> SolarProtons produces atmospheric ionization rates caused by solar proton events, for use as
> particle forcing in the Whole Atmosphere Community Climate Model (WACCM) and in CMIP6
> chemistry-climate simulations. It combines an NCAR Command Language script that drives the workflow
> with a Fortran program, go_proton, that performs the ionization calculation.
>
> The workflow downloads NOAA five-minute GOES solar particle and electron flux text files, converts
> them to netCDF, averages them to hourly and daily resolution, and concatenates them into yearly
> files. A built-in lookup table selects which GOES spacecraft supplied the primary proton flux for a
> given date: GOES-7, GOES-8, GOES-10 and GOES-11 for dates before 14 April 2010, and NOAA's own
> primary/secondary tagging thereafter. The hourly flux files are then passed to go_proton, which
> fits the six integral proton channels (greater than 1, 5, 10, 30, 50 and 100 MeV) with exponential
> spectral forms over three energy bands (1-10, 10-50 and 50-300 MeV), builds a differential spectrum
> on a 60-point logarithmic energy grid from 1 to 300 MeV, and integrates proton energy deposition
> over 35 pitch angles through a 59-level model atmosphere spanning 0 to 116 km. Ion pair production
> rates follow from the deposited energy assuming 35 eV per ion pair. The pitch angle distribution is
> assumed isotropic and the geomagnetic cutoff is set to zero, so the rates represent polar cap
> conditions.
>
> Output is written as netCDF in three selectable layouts: WACCM4 (Prod, in ion pairs per cubic
> centimetre per second, on a reversed pressure axis with date and datesec), WACCM6 (as WACCM4 but in
> ion pairs per gram per second and with a CF time axis and time bounds), and CMIP6 (iprp, "Ion pair
> production rate by solar protons", in g^-1 s^-1 on pressure levels in hPa with Gregorian calendar
> year, month and day variables). The energy deposition scheme is the one first described by Jackman
> et al. (1980), the same scheme underlying the CMIP6 solar proton forcing recommendation.
>
> The GOES data available from the archive the scripts target run from 13 June 1998 to 9 March 2020,
> which bounds the period for which ionization rates can be produced; a companion script,
> spe_pad.ncl, pads an output file forward with zero ionization rates when a model run needs to
> extend beyond that period. The Fortran must be compiled before the scripts are run. A Makefile and
> a helper script are provided, with settings for the Intel, PGI, GNU, g95 and IBM XL Fortran
> compilers, and the build links against netCDF.

**Why this supersedes the stored value.** The stored HSSI description is a paste of the `README.md`
body with its indented code blocks dropped and its paragraphs re-joined, and it fails the field's own
stated requirement that the description be "written
with proper capitalization, grammar, and punctuation" on grounds that are objective rather than
stylistic:

1. It reproduces the README's spelling and grammar errors unchanged — "consistes" for consists, "THe"
   for The, "makelfile" for makefile, "whould" for would, "noass_5m" for the directory the code
   actually creates (`noaa_5m`, per `spe_noaa2nc`), "subidrectories" for subdirectories, "The raw text
   file are", "There is a scripts called spe_pad.ncl", and "in case the are needed for the model to
   run, but the ionizations rates will be 0".
2. It contains truncation artifacts, and byte-for-byte comparison against `README.md` shows that
   **two** indented Markdown code blocks were stripped when the text was captured, not one. The first
   is the `make_proton.csh` build invocation, which leaves the sentence "It can be executed as:"
   followed by nothing — a dangling colon and no command. The second, and the more consequential loss,
   is the enumeration of what the workflow can do: the four switch descriptions (`getFiles` - download
   the data files; `processFiles` - convert the text based format to a NETCDF format; `calcIons` -
   determine the ion production rates for each NETCDF file; `combineFiles` - combine the individual
   flux files together) together with the `ncl < scripts/spe.ncl` invocation line. The stored text
   consequently jumps straight from "There are 4 different things that can be done:" to "The raw text
   file are downloaded...", promising an enumeration and then silently omitting it. A reader is left
   unable to learn what the software's four operations are — which is precisely the information a
   potential user needs.
3. It is written as build instructions relative to a working directory ("The source code and scripts
   in this directory..."), not as a description of the software. A reader of an HSSI search result has
   no "this directory". Roughly half of the stored text is compilation guidance about where object
   files land and what the executable is called, which does not help a potential user decide whether
   the software is relevant to their work.

The replacement preserves the README's substantive claims about what the software is and does — the two-part NCL/Fortran structure,
Jackman as the origin of the Fortran, the four workflow stages, the 5-minute to hourly to netCDF
conversion chain, the three output formats, the compile-first requirement and compiler portability
caveat, the 1998-06-13 to 2020-03-09 data range, and the zero-padding script — and adds the
quantitative detail that only the code supplies: the energy channels, the fit bands, the energy grid,
the pitch angle count, the atmospheric level count and altitude range, the 35 eV per ion pair
constant, the polar cap configuration, and the actual variable names and units in each output layout.

One factual correction the replacement makes relative to the README: the README says netCDF files are
written to `noass_5m`, and the code writes them to `noaa_5m`. The replacement avoids the directory
names entirely rather than repeating the typo or silently correcting the README.

One factual claim deliberately *not* made: `prwrite.f`'s WRCREATE3 header comment documents a CMIP6
layout with a `glat` geomagnetic latitude dimension and `iprp(time, plev, glat)`, but the code as
written defines only `time`, `nbd` and `plev` and declares `iprp` over two dimensions. The header
comment describes the target CMIP6 file layout, not what this program emits — consistent with the
single-latitude, zero-cutoff configuration. The description therefore describes `iprp` on pressure
levels without asserting a latitude axis.

---

### 9. Concise Description (OPTIONAL)

**Concise description (174 characters):**

> SolarProtons computes atmospheric ion pair production rates from GOES solar proton flux
> measurements and writes solar proton event forcing files for WACCM4, WACCM6 and CMIP6.

The stored value is `The source code and scripts in this directory create ionization rates for solar\nprotons.`
— the README's first sentence, complete with its embedded line break and its directory-relative
framing. At 88 characters it also falls well short of the 150-200 character preview the field is
designed to fill. The replacement keeps the same core claim (this software creates ionization rates
for solar protons), states the input the stored version omits (GOES proton flux measurements), states
the output products that make the software findable (WACCM4, WACCM6, CMIP6 forcing files), and reads
as a standalone sentence in a search result.

---

### 10. Publication Date (RECOMMENDED)

`2023-07-21`

The date HSSI already held, and it is confirmed from two independent sources: the repository's sole
commit is dated `2023-07-21 16:12:47 -0600` (2023-07-21 22:12:47 UTC), and the GitHub API reports
`created_at = 2023-07-21T22:08:17Z` with `pushed_at = 2023-07-21T22:14:03Z`.

Note the distinction this date does *not* capture: the code itself dates from October 2016, per the
headers in `Makefile`, `scripts/spe.ncl` and `prmain.f`, and the Jackman Fortran it derives from is
older still. 2023-07-21 is the date of first public release, which is what the field asks for.

---

### 11. Publisher (RECOMMENDED)

- **Organization:** GitHub
- **Publisher Identifier:** `https://github.com`

Not currently stored (HSSI holds `null`). The field's own instruction governs the choice: "For
software where a DOI has been obtained through Zenodo... Zenodo is the correct entry. If no DOI has
been obtained, indicate the repository host, such as GitHub or GitLab." No DOI exists (Field 2), so
the repository host is the correct value. GitHub had no ROR at extraction time, so the identifier is
the URL, which the field permits.

Considered and rejected: **NCAR** as publisher. The repository is owned by the `NCAR` GitHub
organization, which makes NCAR a plausible-sounding publisher, but the field explicitly directs the
repository host rather than the owning institution when no DOI exists — and NCAR is already recorded
as an author (Field 6), where the institutional credit belongs.

---

### 12. Version (RECOMMENDED)

**Not found.**

- **Version Number:** Not found
- **Version Date:** Not found
- **Version Description:** Not found
- **Version PID:** Not found

The version row HSSI held for this record is empty in every subfield — number, release date,
description and version PID are all blank. It carries no information, so the field's value is
Not found and the empty row is detached from this record rather than filled.

Negative research, so this is not re-litigated later. `git tag -l` in the clone returns nothing; the
GitHub API `/tags` and `/releases` endpoints both returned empty arrays at extraction time; there is
no `CHANGELOG.md`, no packaging file (`setup.py`, `pyproject.toml`, `DESCRIPTION`, `Project.toml`, `package.json`) and no
`VERSION` file; a case-insensitive grep of every tracked file for `version`, `license`, `copyright`
and for any `vN.N` pattern returns no matches at all; and SoMEF reported no `version`. The GitHub and
SoMEF results are extraction-time observations; the rest are fixed at the source revision. There is
also no DOI from which a version could be inferred (Field 2). The repository has exactly one commit and has not been touched
since 2023-07-21.

Two near-miss candidates were considered and rejected as version identifiers. The source headers
carry the date "October 2016", which dates the code but is not a release identifier. And
`scripts/spe_pad.ncl` references filenames such as
`ions_c6_Gp_1999-2020_part_1d_c201005.nc` and `ions_w6_Gp_1999-2020pad_part_1d_c210723.nc`, whose
`c201005` and `c210723` suffixes are NCAR-convention creation-date stamps (2020-10-05, 2021-07-23) on
*data* files produced by the software, not versions of the software.

Any value written into this field would be invented, which is why the empty row is detached rather
than populated. A read-only database check at extraction time found that row referenced
by SolarProtons and by no other software record, so detaching it strands nothing that another entry
depends on — unlike the shared empty award row discussed under Field 26. That was a point-in-time
read, however, and it should be re-confirmed against the database before anyone acts on it, since the
set of referents can change.

---

### 13. Programming Language (RECOMMENDED)

- Fortran77
- Fortran90
- Other

`Fortran90` and `Other` were both already stored and are both kept. `Fortran77` is recorded
alongside them.

**Why `Fortran77` belongs.** All eight sources are `.f` files in fixed-form layout: column-6
continuation markers (`     *`), numeric statement labels with `CONTINUE` targets, computed `GO TO`
control flow, `COMMON` blocks (`COMMON/DIMVAR/`, `COMMON/VAR/`, `COMMON/DAY/`), `DIMENSION`
declarations and Hollerith-style `FORMAT` specifiers such as `50HSAMPLE PARTICLE FLUX AT VARIOUS
ATMOSPHERIC DEPTHS//`. The Makefile compiles them with `-132` under ifort and `-Mextend` under pgf90,
both fixed-form line-length extensions. The author's own assessment is in `prargs.f`: "NOTE: These
routines may not be compatible with all F77 compilers." GitHub's linguist reports the language as
plain "Fortran" (48,410 bytes as reported at extraction time) rather than "Fortran Free Form", and
SoMEF likewise returned
"Fortran".

**Why `Fortran90` is nonetheless retained.** The code is not pure F77. `prargs.f`, `prread.f` and
`prwrite.f` use `IMPLICIT NONE`, block `DO ... END DO` loops, `ELSE IF` blocks and assumed-size
dummy arrays with expression bounds (`REAL PROD(NLEV)`), and callers pass array sections
(`PROD(1:JMAX-1)`). The Makefile also carries `-ffree-line-length-none` for gfortran and
`-ffree-line-length-huge` for g95. Recording both values describes the code more accurately than
either alone, and dropping a stored value that is defensible would lose information.

**Why `Other` is retained.** It stands for the NCAR Command Language, which GitHub's linguist put at
38,644 bytes at extraction time — the
larger half of the codebase by line count and the layer a user actually invokes (`ncl <
scripts/spe.ncl`). NCL had no row in HSSI's `ProgrammingLanguage` vocabulary as observed at extraction
time, so `Other` is the only available way to record it. `Other` also covers the tcsh build script (`make-proton.csh`)
and the Makefile. Because of that gap, `ncl` is also recorded in Keywords (Field 16), so the language
remains searchable by name.

Considered and rejected: `Fortran 2003`, `Fortran 2008` and `Fortran 2023`. Nothing in the sources
uses features from those standards — no modules, no derived types, no interfaces, no allocatable
components. All three selected values were confirmed against the live
`/api/models/ProgrammingLanguage/rows/all/` vocabulary at extraction time; note the row is spelled
`Fortran77` with no space, unlike `Fortran 2003`.

---

### 14. Reference Publication (RECOMMENDED)

**Not found.**

Not currently stored (HSSI holds `null`); that remains correct.

No publication describes this software. There is no JOSS or software paper, no `CITATION.cff`, no
"how to cite" section in the README, and no DOI. ADS full-text searches for `"go_proton"` and for
`"NCAR/SolarProtons"` each returned zero records, and a search for `full:"SolarProtons"` combined
with `full:"ionization"` returned six papers — all counts as of extraction time. All six were
inspected and none concerns this package: they are cosmogenic-nuclide, lunar-sample, nuclear-data, avionics and
lower-ionosphere modelling papers in which the two search terms co-occur incidentally.

**Jackman et al. (1980) was considered for this field and placed in Related Publications instead.**
`scripts/spe.ncl` quotes a communication from Jackman ending "The energy deposition methodology again
is that discussed in Jackman et al. [1980]", which makes that paper the citation a user would give for
the *method*. It was not selected here because Field 14 asks for the publication describing *the
software*, and a 1980 paper on odd nitrogen production in the stratosphere and mesosphere describes an
energy deposition scheme, not this 2016 Fortran-and-NCL implementation of it. Recording it in Field 27
preserves the citation without overstating what it documents. See Field 27 for its DOI.

---

### 15. License (RECOMMENDED)

**Not found.**

- **License:** Not found
- **License URI:** Not found

Not currently stored (HSSI holds `null`); that remains correct, and no value should be invented.

Negative research: there is no `LICENSE`, `LICENSE.txt`, `LICENCE`, `COPYING` or `COPYRIGHT` file
among the 13 tracked files, and a case-insensitive grep of every tracked file for `license`, `licence`
and `copyright` returns no matches, so no source-header licence notice exists either. At extraction
time the GitHub API also returned `license: null` for the repository, and SoMEF returned no `license`
result.

This is a real finding about the repository, not a gap in the search. The absence means the code is
published without an explicit grant of rights. `Other` was considered as a placeholder and rejected:
selecting it would assert that a licence exists but is not in the SPDX list, which is a different and
false claim. `Restricted` was also rejected — the repository is public and unrestricted; what is
missing is the licence, not the access.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

- solar proton events
- solar energetic particles
- atmospheric ionization
- ion pair production rate
- particle precipitation
- polar cap absorption
- waccm
- cesm
- cmip6
- middle atmosphere
- mesosphere
- stratosphere
- space weather
- ncl

Not currently stored (HSSI holds an empty list).

The selection follows the field's instruction to record science keywords "not supported by other
metadata fields", and reuses existing rows in the live `/api/models/Keyword/rows/all/` vocabulary
wherever one exists so that near-duplicate rows are not minted. As observed at extraction time,
`solar energetic particles`, `particle precipitation`, `waccm`, `cmip6`, `mesosphere`, `stratosphere`
and `space weather` already existed as rows, and `solar proton events`, `atmospheric ionization`,
`ion pair production rate`, `polar cap absorption`, `cesm`, `middle atmosphere` and `ncl` would be
created. That split is worth re-checking rather than trusting: Keywords is HSSI's one open vocabulary,
so any submission anywhere can mint a row and change which of these already exist.

Two entries carry specific weight. `solar proton events` is here because Related Phenomena (Field 22)
has no row for it, for the reason set out under that field, and Field 22's own guidance directs
unrepresentable phenomena to Keywords. `polar cap absorption` is grounded in the code rather than
inferred:
`prinp_cesm.f` describes the quantity `NRUN` as "THE NUMBER OF PCA EVENTS STUDIED". `ion pair
production rate` is the exact `long_name` attribute the software writes on its output variable.

Considered and rejected to avoid duplicating other fields: `goes` (Field 32 records the observatory),
`netcdf` (Fields 18 and 19 record the formats), `fortran` (Field 13 records the language), and
`thermosphere` (Field 5 has an `Earth Thermosphere` row). `ncl` is the deliberate exception to that
rule: for the reason set out under Field 13, the language is recorded there as `Other`, so this
keyword is the only field in which NCL remains searchable by name.

---

### 17. Data Sources (OPTIONAL)

- HTTP/HTTPS Directories
- Observatory/Mission-specific

Not currently stored (HSSI holds an empty list).

**HTTP/HTTPS Directories** — `getTxtFiles` in `scripts/spe.ncl` retrieves files by `wget` from an
HTTPS directory listing: `wget -P noaa_txt
https://umbra.nascom.nasa.gov:/sdb/goes/particle/<yyyymmdd>_Gp_part_5m.txt`. The URL was checked and
the directory is live.

**Observatory/Mission-specific** — the archive path is GOES-specific and the filenames encode the
GOES spacecraft (`_Gp_`, `_Gs_`, and the `_G7`/`_G8`/`_G10`/`_G11` variants that `spe_primary4date`
constructs). Field 17's instruction is to select this value and name the mission in Related
Observatories, which Field 32 does.

Considered and not selected:

- **FTP/FTPS Directories.** The `spe.ncl` header records the original provenance — "This data was
  downloaded by from anonymous ftp at: umbra.nascom.nasa.gov /sdb/goes/particle/" — but the code as
  written uses `wget` over HTTPS. FTP is documented history, not a route the software implements.
- **CDAWeb, OMNIWeb, SSCWeb, HAPI, das2, AMDA, VSO, VirES, WDC, Madrigal, GFZ, S3/Cloud-aware.** None
  appears anywhere in the code. The executable code contacts a single archive.
- **NOAA NCEI.** `spe_wgetncei` in `spe.ncl` carries a header comment citing
  `http://satdat.ngdc.noaa.gov/sem/goes/data/new_avg/1986/01/goes06/netcdf/...`, which looks like a
  second data source. It is not one: the procedure body is a copy of `spe_check4fill` that performs
  no download at all and references an undefined variable `threshold`, so it is dead, unfinished code.
  Recording NCEI as a supported source would misrepresent the software.

Both values were confirmed against the live `/api/models/DataInput/rows/all/` vocabulary at extraction
time. Note for anyone diffing against production: at extraction time production still carried a junk
`Other - https://...` row that localhost had retired; it is not used here.

---

### 18. Input File Formats (RECOMMENDED)

- ascii
- netCDF3/4

Not currently stored (HSSI holds an empty list).

**ascii** — `spe_noaa2nc` reads NOAA's fixed-width text product with `readAsciiHead(noaafile,
"#---------")` and `readAsciiTable(...)`, and `spe_ions2nc` reads Jackman's legacy ion-production
tables `ions_txt/IonPair-gm_Year-<year>.dat` with `readAsciiTable` against a documented Fortran format
(`1X,1PE11.3,3X,1P6E11.3`).

**netCDF3/4** — `prread.f` opens the flux file with `NF_OPEN` and reads `penergy`, `pflux`, `year`,
`month`, `day`, `tod`, `time` and `time_bnds`; `spe_2hourly`, `spe_2daily`, `spe_hions2daily` and
`spe_pad.ncl` all open netCDF files with NCL's `addfile(..., "r")` or `"w"`.

Considered and rejected: **CDF**, **FITS**, **HDF5**, **csv**, **JSON**, **IDL.sav**, **Zarr**,
**ISTP-Compliant**. The software reads none of them.

A naive case-insensitive substring search over the sources is actively misleading here, and a future
agent should not mistake its output for evidence to the contrary. At the pinned source revision,
`cdf` matches 46 times and every one of those matches sits inside a netCDF token — `netcdf.inc` in the
Fortran includes, `NETCDF` in comments, `-lnetcdf` and `-lnetcdff` in the Makefile's link flags, and
`NCAR_ROOT_NETCDF` — none of them a reference to the CDF format. `fits` matches once, and that match
is the English verb opening `prfit.f`'s first comment line, "Fits the observed proton fluxes (pflux)
with a power law." Matching on isolated words instead of substrings is the search that actually
answers the question: at that revision it returns nothing for `cdf`, `hdf`, `csv`, `json`, `IDL.sav`,
`zarr` or `istp`, and for `fits` it returns only that one verb.

HDF5 deserves the explicit note: netCDF-4 files are
HDF5-backed, but the writer uses `NF_CREATE(PATH, NF_CLOBBER, ...)` with the classic netCDF-3 API and
`netcdf.inc`, so no HDF5 path is exercised and the format is not independently supported.

---

### 19. Output File Formats (RECOMMENDED)

- netCDF3/4

Not currently stored (HSSI holds an empty list).

Every data product the software emits is netCDF: the 5-minute, hourly and daily flux files written by
`spe_noaa2nc`, `spe_2hourly` and `spe_2daily`; the ion production files written by `prwrite.f` in all
three layouts (WACCM4, WACCM6, CMIP6); the concatenated yearly and multi-year files produced through
`ncrcat`; and the padded files written by `spe_pad.ncl`.

Considered and rejected: **ascii**. `prinp_cesm.f` contains a substantial block of `WRITE(2, ...)`
statements that emit a human-readable run summary (pitch angle grid, energy range, atmospheric depths,
spectral fit parameters, geomagnetic cutoff table), and `Makefile`'s `clean` target removes `*.txt`
and `*.html`. That output is a diagnostic log rather than a data product — it carries no results, has
no documented layout, and nothing downstream consumes it. Recording `ascii` as an output format would
suggest the software can emit its ionization rates as text, which it cannot.

---

### 20. Operating System (RECOMMENDED)

- Linux
- Mac

Not currently stored (HSSI holds an empty list).

The toolchain is Unix throughout and the evidence points at these two platforms specifically. The
build helper `make-proton.csh` has a `#!/bin/tcsh` shebang; the workflow shells out to `wget`,
`ncrcat`, `mkdir -p`, `rm` and `cp`; and NCL, which the driver requires, is distributed as binaries
for Linux and macOS.

`Mac` is not an inference from "Unix" — the `Makefile` retains two macOS-specific artifacts from the
author's own environment: a commented `NFDIR = /Volumes/Data/Libraries/netcdf` (a macOS volume path,
repeated in `make-proton.csh`) and a commented ifort link line using `-no_pie`, a Darwin linker flag,
annotated "The no_pie flags also the executable to work with idb."

`Linux` follows from the default build configuration: `NFDIR = ${NCAR_ROOT_NETCDF}`, the environment
variable set by NCAR's HPC module system, alongside compiler blocks for ifort, pgf90, gfortran, g95
and xlf90.

Considered and rejected: **Windows** (tcsh shebang, `/bin/rm` in the Makefile's `clean` target, and a
`wget`/`ncrcat` dependency chain with no Windows provision); **Solaris** and **MobilePlatform** (no
evidence of either); **Operating System Independent** (the software requires a Unix shell, an
external NCL installation and a Fortran compiler with netCDF, which is not platform independence).
Note the trap in this vocabulary, as it stood at extraction time: the cross-platform row is spelled
`Operating System Independent` in full, and `OS Independent` is not a value — neither is used here.

---

### 21. CPU Architecture (RECOMMENDED)

- x86-64
- HPC or HEC

Not currently stored (HSSI holds an empty list).

**x86-64** — the Makefile's active default is `FORTRAN = ifort`, the Intel Fortran compiler, with
alternates for pgf90 and gfortran. In the code's 2016-2023 lifetime these targeted x86-64 on both the
NCAR HPC systems and the author's workstation.

**HPC or HEC** — the default netCDF root is `NFDIR = ${NCAR_ROOT_NETCDF}`, which is not a generic path
but the variable exported by NCAR's HPC environment-module system. That is direct evidence the
intended build and run environment is an NCAR high-performance computing system, and the workload
matches: the driver loops over years of daily files, invoking the compiled binary once per output
format per year.

Considered and rejected:

- **ppc64le.** The Makefile does contain a full IBM XL Fortran block (`-q64 -qarch=auto
  -qspillsize=2500`), which is a genuine supported build path for IBM POWER, but nothing indicates it
  was exercised for this code; it reads as carried-over boilerplate from the author's other models.
  Recording it would assert a platform on the strength of an untested compiler stanza.
- **Apple Silicon arm64.** The macOS evidence in the Makefile (Field 20) dates from 2016, years before
  Apple Silicon existed, and the repository has not been touched since 2023-07-21.
- **CPU Independent.** The Fortran source has no architecture-specific code, so this is tempting, but
  the value asserts the software installs and runs on any architecture, and this package must be
  compiled against a local netCDF for each target. The evidenced platforms are recorded instead.
- **GPU**, **Sun (SPARC)**, **Linux aarch64 or arm64**. No evidence of any.

---

### 22. Related Phenomena (OPTIONAL)

**Not found — correctly empty.**

HSSI stores an empty list; that remains correct.

This is a **closed** seven-row vocabulary: `Coronal Heating`, `Coronal Mass Ejections`,
`Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`, `X-ray emission`. The phenomena
this software actually supports science for — solar proton events, solar energetic particle
precipitation, polar cap absorption, and atmospheric ionization by energetic particles — have no row
among those seven. There is no row that can be selected without misdescribing the software.

`Solar Flares` and `Coronal Mass Ejections` were the two candidates worth weighing, because solar
proton events are accelerated in association with flares and CME-driven shocks, and the code's own
test case is 2003-10-29, in the middle of the Halloween 2003 storm sequence. Both were rejected: the
software processes the particle consequence, not the eruptive event. It never touches flare or CME
observations, and a user searching HSSI for flare or CME tooling would not want this package back.
Note in particular that the GOES X-ray sensor documentation cited in `spe_primary4date` is used only
as the source of the primary-satellite table; the software does not read X-ray data, so
`X-ray emission` would also be wrong.

Field 22's own guidance covers this case: "A phenomenon the software supports that has no row belongs
in Keywords (Field 16, the open vocabulary), not here." Accordingly `solar proton events`,
`solar energetic particles`, `particle precipitation`, `polar cap absorption` and
`atmospheric ionization` are recorded in Field 16. An empty Field 22 is the correct outcome here, not
a gap left unfilled.

---

### 23. Development Status (RECOMMENDED)

`Inactive`

Not currently stored (HSSI holds `null`).

repostatus.org defines `Inactive` as "The project has reached a stable, usable state but is no longer
being actively developed; support/maintenance will be provided as time allows." Both halves fit.

*Stable and usable:* the code is a working production tool, not a prototype. It implements a complete
pipeline end to end, its ionization calculation is the published Jackman scheme, and its three output
layouts are the concrete formats WACCM4, WACCM6 and CMIP6 consume. The comments record real
operational history — a correction adopted from a communication with Jackman, GOES-12 removed from the
satellite table after its channels 6 and 7 failed to produce proton fluxes, and references to
multi-decade output files (`ions_c6_Gp_1999-2020_part_1d_c201005.nc`) that were actually generated.

*No longer actively developed:* one commit, no commits since 2023-07-21, no tags, no releases, no
issues in any state, no forks, and code whose internal date is October 2016. The 2023 publication
reads as an archival deposit of a finished tool.

Considered and rejected: **Abandoned** (defined as development started but abandoned with no stable
release — wrong, the software works and its outputs were used); **Unsupported** (implies the authors
have ceased work and a new maintainer is wanted, and nothing states that); **Active** (contradicted by
the commit history); **Concept** and **WIP** (the implementation is complete, not a demo);
**Suspended** and **Moved** (no evidence of an intent to resume or of relocation).

---

### 24. Documentation (RECOMMENDED)

`https://github.com/NCAR/SolarProtons/blob/main/README.md`

Not currently stored (HSSI holds an empty string).

`README.md` is the documentation. It states the two-part structure, how to compile
(`make-proton.csh`, with the caveat that the Makefile may need editing for the local compiler), how to
invoke the workflow (`ncl < scripts/spe.ncl`), what the four workflow switches do, the directory
layout of the intermediate and output files, the three output formats, the usable data range, and the
purpose of `spe_pad.ncl`. That is installation instructions plus usage, which is what the field asks
for. The URL was checked and resolves.

Considered and rejected:

- **A dedicated documentation site.** There is none. The repository has no `docs/` directory, no
  `.readthedocs.yml` or equivalent and no documentation link in the README; at extraction time the
  GitHub API reported `has_pages` false, and SoMEF found no `documentation` result.
- **The GitHub wiki.** `has_wiki` is true, but that is GitHub's default for a new repository; a
  request for `/NCAR/SolarProtons/wiki` redirects rather than serving content, so no wiki pages have
  been created.
- **`http://solarisheppa.geomar.de/solarprotonfluxes`.** `scripts/spe.ncl` points at it — "See
  http://solarisheppa.geomar.de/solarprotonfluxes for some additional descriptions." It is not
  documentation of this software: SOLARIS-HEPPA is the community reference site for solar forcing
  datasets used in chemistry-climate models, and the link describes the *data* and the scientific
  context rather than this package. Worth recording separately: that URL now issues a 301 redirect to
  `https://www.solarisheppa.kit.edu/`, the project's new home after moving from GEOMAR to KIT, so the
  in-code link is stale. This is upstream drift in a comment, not in a metadata value.
- **The repository root URL.** Rejected in favour of the README's direct link, which points at the
  documentation itself rather than at the file listing.

---

### 25. Funder (OPTIONAL)

**Not found.**

HSSI stores an empty list; that remains correct.

Negative research, recorded because the temptation to fill this field from institutional context is
strong and should be resisted. The repository contains no acknowledgement, funding statement, grant
number or sponsor reference in any tracked file. There is no publication describing the software
whose Acknowledgments could supply one (Field 14), and no DOI whose DataCite `fundingReferences` could
(Field 2).

Two inferences were considered and rejected:

1. **NSF, because NCAR is NSF-sponsored.** NCAR's status as an NSF-sponsored federally funded research
   and development center is true of NCAR-produced software generally. It is
   institutional boilerplate, not evidence that this package was funded by a particular NSF award, and
   recording it would put an unsourced funder on the record.
2. **NSF and NASA, from the author's contemporaneous papers.** Bardeen, Marsh, Jackman, Hervig and
   Randall (2016), "Impact of the January 2012 solar proton event on polar mesospheric clouds"
   (`https://doi.org/10.1002/2016JD024820`), is by this software's author on the atmospheric effects of solar proton events, and an ADS
   acknowledgements probe confirms it acknowledges both the National Science Foundation and NASA. It
   was still rejected: the paper neither names nor cites this software, and it was published before the
   October 2016 date in the code headers. Attributing its funding to this package would be an
   inference dressed as a source.

---

### 26. Award Title (OPTIONAL)

**Not found.**

- **Award Title:** Not found
- **Award Number:** Not found

The award row HSSI held for this record is empty in every subfield — the award name, the identifier
and the funder link are all blank. It carries no information, so the field's value is Not found and
the empty row is detached from this record rather than filled.

**Durable constraint on how that cleanup may be done.** A read-only database check at extraction time
found this same empty award row attached to several other software records besides SolarProtons. It is
therefore a shared row, and removing it from this record must be done by *detaching* it from
SolarProtons — never by deleting the row, which would strip the award from those other entries as
well. Anyone acting on this should re-confirm the current set of referents first, since it can change.

The negative research is the same as for Field 25: no acknowledgement anywhere in the repository, no
describing publication, no DOI. No award title or number can be recorded without inventing one.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

1. `https://doi.org/10.1029/JC085iC12p07495` — Jackman, C. H., Frederick, J. E., & Stolarski, R. S.
   (1980). Production of odd nitrogen in the stratosphere and mesosphere: An intercomparison of source
   strengths. *Journal of Geophysical Research*, 85(C12), 7495-7505.
2. `https://doi.org/10.5194/gmd-10-2247-2017` — Matthes, K., Funke, B., Andersson, M. E., et al.
   (2017). Solar forcing for CMIP6 (v3.2). *Geoscientific Model Development*, 10, 2247-2302.

Not currently stored (HSSI holds an empty list). Both entries document the software's *method*, which
is what the field permits; neither documents the code itself, and Field 14 is correspondingly empty.

**Jackman et al. (1980)** is named in the repository. `scripts/spe.ncl` quotes a communication from
Jackman which ends: "The GOES satellite proton fluxes are fit in three energy intervals 1-10 MeV,
10-50 MeV, and 50-300 MeV with exponential spectral forms. The energy deposition methodology again is
that discussed in Jackman et al. [1980]." Each quantitative specific in that sentence is
verifiable in the code: `prinp_cesm.f` sets `IDIVID = 3` with `EN(2) = 10.0` and `EN(3) = 50.0` over a
1-300 MeV grid, and `ISPCTR = 1` selects the exponential form that `prspec.f` evaluates. This is the paper a user should
cite for the calculation. Identified through ADS as bibcode `1980JGR....85.7495J`.

**Matthes et al. (2017)** is the CMIP6 solar forcing recommendation, and it describes the same scheme
this code implements. Section 2.2.2 reads: "The proton fluxes of energies 1-300 MeV were used to
compute daily average ion pair production profiles using an energy deposition scheme first discussed
in Jackman et al. (1980). The scheme includes the deposition of energy by the protons and assumes 35
eV is required to produce one ion pair (Porter et al., 1976)." Three specifics match the code exactly:
the 1-300 MeV range (`prinp_cesm.f`: `E(1) = 1.0`, `EMAX = 300.`), the 35 eV per ion pair constant
(`DISS(1) = 35.0E-6` MeV), and the Jackman energy deposition scheme. Charles H. Jackman is a co-author
of that paper. It is also the reason the software's third output layout is labelled CMIP6, and the
document a user needs in order to understand what that layout is for. Verified against the article's
full text rather than the abstract, which does not contain these details.

Considered and not selected:

- **Porter, H. S., Jackman, C. H., & Green, A. E. S. (1976)**, "Efficiencies for production of atomic
  nitrogen and oxygen by relativistic proton impact in air", *J. Chem. Phys.* 65, 154
  (`https://doi.org/10.1063/1.432812`). This is the published source of the 35 eV per ion pair constant that
  `prinp_cesm.f` hard-codes, and it is cited as such by Matthes et al. It was not selected because the
  repository does not cite it — the attribution comes from Matthes's description of the same scheme,
  not from this code. The DOI is recorded here so a future agent has it if the judgement is revisited.
- **Bardeen et al. (2016)**, `https://doi.org/10.1002/2016JD024820`, and
  **Pettit et al. (2018)**, `https://doi.org/10.1029/2018JA025294`. Both are WACCM solar-proton-event studies involving this software's
  authors, and both are plausible users of ionization rates of this kind. Neither cites or names the
  software, and no citation link can be demonstrated, so listing them would assert a relationship that
  is not evidenced.
- **Gettelman et al. (2019)** and the WACCM6 model description literature. Background about the
  consuming model, not about this software or its method.

---

### 28. Related Datasets (OPTIONAL)

1. National Oceanic and Atmospheric Administration Space Weather Prediction Center. *GOES Solar
   Particle and Electron Flux, 5-minute averages* [Data set]. NASA Goddard Space Flight Center Solar
   Data Analysis Center. https://umbra.nascom.nasa.gov/sdb/goes/particle/

Not currently stored (HSSI holds an empty list). Entered as an APA-style citation with a permanent
link, which the field permits when no DOI is available.

This is the software's input dataset, named by the code rather than inferred: `getTxtFiles` downloads
from exactly this directory, and the file header that `spe_noaa2nc` documents identifies the product —
"Prepared by the U.S. Dept. of Commerce, NOAA, Space Weather Prediction Center", with proton labels
"P > 1" through "P>100" in Protons/cm2-s-sr and electron labels "E>0.8" through "E>4.0". The archive
directory was checked and is live.

Considered and not selected:

- **A DOI for the GOES particle flux data.** Searched for and not found: a DataCite query for GOES
  Space Environment Monitor particle flux data returned no matching dataset record at extraction time,
  so the APA form is used as the field directs.
- **The CMIP6 solar forcing dataset.** The software's third output layout targets it, which makes it a
  genuine relationship, but no DOI for the CMIP6-era SOLARIS-HEPPA solar forcing dataset surfaced in
  DataCite at extraction time. The only input4MIPs record the search returned at extraction time is
  `10.25981/esgf.input4mips.cmip7/2522675` (`input4MIPs.CMIP7.SOLARIS-HEPPA.SOLARIS-HEPPA-CMIP-4-6`),
  which is the CMIP7 dataset — a different, later version than this 2016 code targets. Citing it would
  misidentify the product. The relationship is instead recorded through Matthes et al. (2017) in Field
  27, which is the documentation of the CMIP6 dataset.
- **Jackman's legacy ion production tables** (`ions_txt/IonPair-gm_Year-<year>.dat`, read by
  `spe_ions2nc` for comparison purposes, covering 1963-2015 per the commented-out loop at the bottom
  of `spe.ncl`). A real dataset the software reads, but it has no public location, DOI or citation —
  it is a private data product passed from Jackman to Bardeen. No citable location for it could be
  found at extraction time.

---

### 29. Related Software (OPTIONAL)

1. `https://doi.org/10.5065/D6WD3XH5` — NCAR Command Language (NCL)
2. `https://github.com/nco/nco` — netCDF Operators (NCO)

Not currently stored (HSSI holds an empty list). Both are domain-specific dependencies whose presence
characterises this software, which is what Field 29 asks for.

**NCL** is not merely a dependency; it is the language the user-facing half of the package is written
in. `scripts/spe.ncl` (35 KB) and `scripts/spe_pad.ncl` are NCL, the documented invocation is
`ncl < scripts/spe.ncl`, and the scripts load four libraries from `$NCARG_ROOT`. NCL is a geoscience
analysis language developed at NCAR, not general-purpose infrastructure, and its presence tells a
reader something specific about this software: it is a 2016-era NCAR atmospheric-modelling workflow.
The DOI is NCAR's own software DOI for NCL (DataCite: "NCAR Command Language (NCL)", publisher NSF
National Center for Atmospheric Research, 2012, resource type Software), which resolved when checked
at extraction time.

**NCO** is invoked by name as an external tool the workflow cannot complete without: `spe_catyear`
runs `system("ncrcat -O " + ifile + " " + ofile)` to build yearly flux files, and `spe_cations` does
the same to combine ion production files across years. `ncrcat` is the netCDF Operators record
concatenator. It is an Earth-science community tool rather than generic plumbing, and the dependency
is a hard runtime requirement for two of the four workflow stages. Cited evidence is the two
`system("ncrcat ...")` calls, not a package manifest — the repository has no manifest.

Considered and rejected:

- **The netCDF library** (`-lnetcdf` in `LDFLAGS`, `INCLUDE 'netcdf.inc'` throughout `prread.f` and
  `prwrite.f`). This is foundational I/O plumbing; the software links it the way most Earth-science
  code does, and recording it would say nothing that distinguishes this package. It is captured
  instead where it belongs, as the file format in Fields 18 and 19.
- **wget.** Generic HTTP retrieval infrastructure, equally at home in a web app or any other pipeline.
- **The Intel, PGI, GNU, g95 and IBM XL Fortran compilers.** Build toolchain, not related software.
- **WACCM and CMIP6.** Both are genuinely related but belong in Field 30, where they are already
  stored; a package rejected from one field is not automatically relocated to the other, and these
  were not rejected — they are correctly placed.

---

### 30. Interoperable Software (OPTIONAL)

1. `https://www2.acom.ucar.edu/gcm/waccm` — Whole Atmosphere Community Climate Model (WACCM)
2. `https://pcmdi.llnl.gov/CMIP6/` — Coupled Model Intercomparison Project Phase 6 (CMIP6)

Both entries are carried over from the existing HSSI record. Both URLs still resolved when checked at
extraction time, so neither is a stale or moved link needing replacement.

**WACCM** is the clearest possible case of demonstrated interoperability: this software exists to
produce input that WACCM reads. Two of the three output layouts are named for WACCM versions, and the
code's structure encodes the difference between them — `prwrite.f` documents "Create a file formatted
for WACCM6. This is like WACCM4, but with time and time_bnds added and the units for ion production
converted to /g/s", and `WRPROD` reverses the vertical axis for formats 1 and 2 and divides by air
density for format 2. `prinp_cesm.f` opens "This is a verion of the input routine that has been hard
coded with settings that are used to create an SPE file for CESM (WACCM)." Output from one package
imported by the other is the exact bar this field sets.

**CMIP6** is retained, with a recorded caveat rather than silent acceptance. The relationship is real
and demonstrable — `prargs.f` documents the third command-line argument as "output file format
(1=WACCM4,2=WACCM6,3=CMIP)", and `WRCREATE3` builds the CMIP6 solar-proton-forcing layout with `iprp`,
"Ion pair production rate by solar protons", in `g^-1 s^-1` on `plev` in hPa. The caveat is
categorical: CMIP6 is a model intercomparison project and a data standard, not a software package, so
it sits awkwardly in a field about software interoperation. It is kept because the underlying
relationship it records is accurate and because a submitter's deliberate entry should not be discarded
over a category quibble. The note is here so a future curator can weigh it rather than rediscover it.

*A note on what HSSI displays for these entries.* Both are stored with the placeholder name "UNKNOWN"
alongside their URLs. That placeholder is an artifact of how related items without a resolved title
are stored and is not user-visible; it carries no meaning and was not allowed to influence the
decisions above.

Considered and rejected: **NCL** and **NCO** — genuinely related, but as the implementation language
and an external tool rather than as peer packages exchanging data, so they are recorded in Field 29.
**netCDF** — a format, recorded in Fields 18 and 19.

---

### 31. Related Instruments (OPTIONAL)

**Not found — correctly empty.**

HSSI stores an empty list; that remains correct.

The proton fluxes this software consumes are produced by the GOES Space Environment Monitor's
energetic particle detectors, so an instrument association is scientifically plausible. It is not
*evidenced*. The software reads NOAA's derived five-minute integral flux text product and treats it as
an opaque input: it has no knowledge of which detector or channel produced each number, and no
executable line in the package refers to a GOES particle instrument.

The one place an instrument designation does appear is worth recording precisely, because a later
search will find it and should not mistake it for evidence. `scripts/spe.ncl` line 1160, inside the
header comment of the `spe_wgetncei` procedure, gives an example URL
`http://satdat.ngdc.noaa.gov/sem/goes/data/new_avg/1986/01/goes06/netcdf/g06_hepad_5m_19860101_19860131.nc`
— a NOAA NCEI path naming the GOES-06 High Energy Proton and Alpha Detector. That reference does not
qualify under the relevance gate on three independent grounds: it sits in a comment rather than in
code; the procedure it heads is dead and unfinished, containing a copy of `spe_check4fill`'s body that
performs no download and references an undefined variable `threshold` (see Field 17); and the
vocabulary held no HEPAD row for any GOES spacecraft at extraction time in any case. It records a
data source the
author contemplated, not an instrument the software supports.

Selecting an instrument row would therefore mean inferring the instrument from the data product, which
the resolution ladder explicitly excludes ("A plausible guess is not evidence"). Ladder rule 4 applies
instead: where no instrument row is evidenced, associate the observatory. Field 32 does exactly that.

Candidate rows that existed in the vocabulary at extraction time and were deliberately *not*
selected, so this is not reopened as an oversight: `https://spase-metadata.org/SMWG/Instrument/GOES/7/SEM`,
`.../GOES/8/SEM`, `.../GOES/10/SEM`, `.../GOES/11/SEM` (all named "Space Environment Monitor" or
"Environment Monitor on GOES"), and `.../GOES/7/EPM`, `.../GOES/8/EPM`, whose row names are
"Energetic Particle Monitor on GOES  7" and "Energetic Particle Monitor on GOES  8" — with two spaces
before the number, an upstream SPASE quirk that would have to be reproduced exactly if either row were
ever selected. Note also that rows named
`Energetic Particle Sensor on GOES` existed, at extraction time, for GOES 13, 14 and 15 only — not
for the spacecraft this code names.

One instrument reference in the code specifically does *not* qualify. `spe_primary4date` cites
`https://ngdc.noaa.gov/stp/satellite/goes/doc/GOES_XRS_readme.pdf` for its primary-satellite table,
which mentions the GOES X-Ray Sensor. That document is used solely as the authority for which
spacecraft was primary on which date; the software reads no X-ray data and supports no XRS function.

---

### 32. Related Observatories (OPTIONAL)

Five observatories, one series-level and four spacecraft-level:

1. **Geostationary Operational Environmental Satellites** — `https://spase-metadata.org/SMWG/Observatory/GOES`
2. **1987-022A** — `https://spase-metadata.org/SMWG/Observatory/GOES/7`
3. **1994-022A** — `https://spase-metadata.org/SMWG/Observatory/GOES/8`
4. **1997-019A** — `https://spase-metadata.org/SMWG/Observatory/GOES/10`
5. **2000-022A** — `https://spase-metadata.org/SMWG/Observatory/GOES/11`

Every entry carries an `https://spase-metadata.org/` identifier. The whole `InstrumentObservatory`
vocabulary was fetched and checked at extraction time: no row failed the
`identifier.startswith("https://spase-metadata.org/")` guard, so the vocabulary was SPASE-backed on
this target, and no `.html` duplicate existed for any of the five identifiers above.

**Entry 1, the series row, covers the software's open-ended case.** The umbrella GOES observatory row
is the right resolution for it: from 2010-04-14 onward `spe_primary4date` stops naming a spacecraft and
returns `"Gp"`, delegating the choice of primary satellite to NOAA's own tagging in the filename. The
code comment says so directly: "NOTE: Starting on 20100414, the data files from NOAA are already
tagged as primary (Gp) or secondary (Gs), so this table is only needed for dates before then." Since
the README puts the archive's coverage as running to 2020-03-09, that delegated era spans whichever
GOES spacecraft NOAA designated across a decade. No single spacecraft row can represent it; the series
row can.

**Entries 2-5 rest on a hard-coded supported-spacecraft list in the executable code**, which is the
form of evidence the resolution ladder's rule 2 requires. `spe_primary4date` contains:

```
sdate = (/ "19940101", "19950301", "20030408", "20030510", "20030619", "20100414" /)
psat  = (/ "G7",       "G8",       "G10",      "G8",       "G11",      "Gp"       /)
```

The returned suffix is not decorative — it is used to build the input filename that `spe_noaa2nc`
opens (`noaa_txt/<yyyymmdd>_G8_part_5m.txt` and so on), so the software genuinely reads per-spacecraft
GOES files for GOES-7, GOES-8, GOES-10 and GOES-11. The provenance of the list is also documented: the
comment block records that it was "Changed it to the following based upon communication from Charley
Jackman" and quotes his enumeration of which GOES satellite supplied proton fluxes for each period.

The four rows were matched by SPASE identifier path segment (`.../Observatory/GOES/<n>`) rather than
by name, since those rows' names were COSPAR designations, and each identifier was verified against the
correct spacecraft's launch: GOES-7 launched 1987-02-26 (1987-022A), GOES-8 1994-04-13 (1994-022A),
GOES-10 1997-04-25 (1997-019A), GOES-11 2000-05-03 (2000-022A).

**Display caveat, and why the names look wrong.** The `name` values recorded for entries 2-5 are
COSPAR international designators, not readable spacecraft names, because that is what those SPASE rows
carried at extraction time and the resolution ladder requires copying the matched row's name
unchanged. This is an upstream SPASE naming property, not an error in this record — for comparison, at
extraction time the GOES 13, 14 and 15 rows in the same vocabulary were named "Geostationary
Operational Environmental Satellite 13" and so on. The practical consequence is that HSSI would list
four COSPAR identifiers alongside the readable series name.

All five entries are recorded, and that display cost is accepted deliberately. The reason is that the
identifier, not the name, is what does the work here: it is the key HSSI de-duplicates on, the key a
search for GOES-11 tooling would resolve through, and the only part of the entry that is unambiguous.
Dropping the four spacecraft rows to avoid four ugly labels would discard four correct, evidenced
associations in exchange for cosmetics, and would leave the record silent about the specific
spacecraft whose files the code is written to read.

The narrower alternative was real and is worth preserving rather than forgetting: keeping entry 1
alone would also have been defensible. The series row is accurate, it covers the whole period the
software can process, and it is the entry a reader would find most legible. It was not chosen because
it is less informative — it cannot tell a reader that GOES-7, GOES-8, GOES-10 and GOES-11 in
particular are hard-coded in `spe_primary4date` — and completeness is what this record is for. Anyone
revisiting the question should weigh it on that ground rather than on the display names, which are
upstream SPASE values this record has no authority to improve.

Considered and not selected:

- **GOES-13** (`https://spase-metadata.org/SMWG/Observatory/GOES/13`). It appears in the quoted
  Jackman communication — "GOES-13 for the period April 14, 2010 to December 31, 2012" — but only in a
  comment, and the executable table does not name it. At that same 2010-04-14 boundary the code
  switches to NOAA's `Gp` tag, which continues to 2020 and therefore also covers GOES-14 and GOES-15.
  Selecting GOES-13 alone would arbitrarily privilege the one spacecraft the comment happened to name;
  adding 14 and 15 would exceed the evidence. The umbrella row (entry 1) represents this entire period
  correctly.
- **GOES-12** (`https://spase-metadata.org/SMWG/Observatory/GOES/12`). Explicitly and deliberately
  *excluded* by the software's author: "NOTE: G12 had problems with channels 6 and 7 and never seemed
  to generate any proton fluxes. So the XRS table has been update to remove G12." Listing it would
  contradict the code.
- **GOES 16-19.** Present in the vocabulary at extraction time, but the code names no spacecraft at
  all after the 2010-04-14 boundary, so selecting any of them would exceed the evidence for exactly the reason
  GOES 13-15 do. The umbrella row covers whichever spacecraft NOAA designated primary.

**Two code-sourced caveats on the spacecraft entries.** Both are recorded because they are durable
properties of the software that a future reader would otherwise have to rediscover from the source.
Neither changes which SPASE identifiers are listed.

*Entry 2, GOES-7: outside the reachable data range.* `spe_primary4date` assigns GOES-7 to 1994-01-01
through 1995-02-28, but the README states the archive the scripts download from holds GOES data only
from 1998-06-13 onward. The GOES-7 period is therefore not reachable through the software's own
download stage; it would require locally staged files. The entry is retained because "designed to
support" describes the software's capability, and the code is written to select and read GOES-7 files
— the limitation is in the data archive, not in the software. The same reasoning covers GOES-8's
pre-1998 period; GOES-8's later spans and the GOES-10 and GOES-11 periods fall within the archive's
stated coverage.

*Entry 3, GOES-8: the author's own doubt about one window.* The `psat` array assigns GOES-8 twice, and
`spe.ncl` records a reservation about the second assignment immediately before the array definitions:
"NOTE: Goes 8 isn't really back until May 14, 2003. Lots of missing data in between May 9 and May 14.
Should use GOES-10 instead." That is the software's author saying his own satellite table is probably
wrong for the 2003-05-10 to 2003-06-19 window it encodes, and that GOES-10 should have been selected
across the roughly five-day gap. It is a data-reliability caveat about a narrow date range, not a
reason to drop the association: GOES-8 supplies the primary proton flux for years of the code's
coverage regardless, most obviously the 1995-03-01 to 2003-04-08 span. Anyone using this software's
output across April-June 2003 should read that comment first.

---

### 33. Logo (OPTIONAL)

**Not found.**

Not currently stored (HSSI holds an empty string); that remains correct.

The repository contains no image file of any kind among its 13 tracked files, no logo or badge in
`README.md`, and no image referenced from any tracked file. SoMEF returned no `logo` result at
extraction time either.

---

## Sources consulted

- The repository at `f84c06ce14e58bba8123cefc1ed06d436df04503`, read in full (13 files).
- GitHub REST API: repository metadata, `/releases`, `/tags`, `/languages` for `NCAR/SolarProtons`.
- DataCite REST API: DOI searches for the software; DOI records for NCL (`10.5065/D6WD3XH5`) and the
  input4MIPs solar forcing datasets.
- Zenodo REST API: record search for the software.
- SoMEF 0.9.11 against the repository URL.
- PyHC registries — `projects_core.yml`, `projects.yml` and `projects_unevaluated.yml` were fetched
  and each read in full rather than searched (7, 57 and 29 entries respectively at extraction time;
  these registries grow as packages are registered). **SolarProtons is not a PyHC package**: no entry
  in any of the three carried the name `SolarProtons` or the repository URL
  `https://github.com/NCAR/SolarProtons`. This is not a defect; PyHC registers Python packages and
  this software is Fortran and NCL.
- ORCID public API: records for `0000-0002-8684-214X` (Vitt), `0000-0002-5330-2788` (Bardeen) and
  `0000-0002-8631-2763` (Jackman).
- ROR API: `05cvfcr44` (NSF National Center for Atmospheric Research) and `0171mag52` (Goddard Space
  Flight Center).
- ADS/SciX search API (anonymous access): identity confirmation for Bardeen's ORCID; bibliographic
  records and DOIs for Jackman et al. (1980), Porter et al. (1976), Matthes et al. (2017),
  Bardeen et al. (2016) and Pettit et al. (2018); full-text and acknowledgements probes.
- Matthes et al. (2017) full text, for the CMIP6 solar proton ionization methodology.
- HSSI controlled vocabularies on the working target: `FunctionCategory`, `Region`,
  `ProgrammingLanguage`, `License`, `Keyword`, `DataInput`, `FileFormat`, `OperatingSystem`,
  `CpuArchitecture`, `Phenomena`, `RepoStatus`, `InstrumentObservatory`, and the `Organization` and
  `Person` tables for affiliation and author matching.
