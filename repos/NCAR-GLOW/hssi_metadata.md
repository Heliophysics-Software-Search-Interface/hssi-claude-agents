# HSSI Metadata Extraction Results

**HSSI Software ID:** 81ad4d3f-39de-43d3-b4ec-45953b21ec71
**Repository:** https://github.com/space-physics/NCAR-GLOW
**Source Revision:** 2c099fdc2bd02b69fd1c3f36e1cc603ad3d34336
**Extraction Date:** 2026-09-01
**Validation Date:** 2026-09-02
**Validation Status:** PASS

---

## Scope and reading notes

**All repository evidence in this file is cited at the pinned revision** `2c099fdc2bd02b69fd1c3f36e1cc603ad3d34336`
(2023-09-20, `Plots: correct that VER units are [photons cm-3 s-1]`), which is the tip of `main`. The
working tree used for extraction is byte-identical to that revision for every tracked file except this
dossier itself, so file paths below can be read as pin-accurate without further qualification. All
thirteen tags in the repository are ancestors of the pin, so tagged commits cited here are on the same
lineage as the pinned tree.

**Quotation convention for the plain-text documentation.** `docs/*.txt` and the Fortran sources are
hard-wrapped at fixed column widths. Where a quotation below spans a wrap, the source's line break is
rendered as a single space; the words, spelling (including the sources' own typographical errors,
which are preserved deliberately) and punctuation are otherwise exactly as written at the pin.

**This entry is a wrapper around an older model, and the distinction matters repeatedly below.**
`space-physics/NCAR-GLOW` is Michael Hirsch's Python/Matlab/CMake packaging of Stan Solomon's NCAR
GLOW model (version 0.981, June 2017). The Fortran in `src/ncarglow/fortran/` is essentially the
upstream NCAR release; the Python layer, the Matlab `+ncarglow/` package, the Meson/CMake build and
the CI are the wrapper. Several fields — authorship, funding, licensing, publication date — have
different correct answers depending on whether the question is asked about the model or about the
packaging, and each of those fields says explicitly which it is answering.

**Four fields were genuinely contested and their reasoning is recorded at length**, because each
turned on a judgement rather than on a missing fact: Field 6 (the six upstream GLOW colleagues named
in the vendored Fortran, and why authorship follows the packaging's creator list instead), Field 15
(why `Other` is the only defensible storable licence name, and why a licence URI cannot exist for this
record at all), Field 17 (why a real, automatic GFZ retrieval one dependency away is still not a data
source of this software), and Fields 25 and 26 together (why NASA is recorded as funder, why the
National Science Foundation is not, and why the award numbers cannot be stored). Each keeps the
alternatives that were rejected, so a later refresh can see what was weighed.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

**Note.** The placeholder is the catalogue convention for a record we did not originally submit; it is
not a defect. This entry was created by an earlier HSSI campaign, not by the software's maintainer.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.3344536

**Source:** Zenodo record 8309940 reports `conceptdoi` `10.5281/zenodo.3344536`; DataCite's record for
that DOI carries seven related identifiers — one `IsSupplementTo` pointing at the tagged GitHub tree
and six `HasVersion` entries, one per deposited release — which is the shape of a Zenodo concept DOI.
Field 28 cites the same six `HasVersion` entries.

**Why this DOI rather than the version DOI.** The concept DOI always resolves to the newest release,
which is what Field 2 asks for. The version-specific DOI for the currently recorded release,
https://doi.org/10.5281/zenodo.8309940, is recorded in Field 12 as the Version PID, which is where it
belongs. Carried over unchanged from the existing HSSI record.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/NCAR-GLOW

**Source:** the repository itself; corroborated by the Zenodo record's `isSupplementTo` related
identifier `https://github.com/space-physics/NCAR-GLOW/tree/v1.4.0` and by the PyHC registry entry's
`code:` field.

**Note on the older `scivision/` URL.** The README's CI badge still points at
`https://github.com/scivision/NCAR-GLOW`, and the install snippet clones
`https://github.com/space-physics/ncar-glow` (lower case). Both are GitHub redirects to the same
repository. The canonical, case-correct form under the current organisation is the value above, and it
is what the Zenodo integration recorded.

### 4. Software Functionality (RECOMMENDED — treated as critical)

**Values:**
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Visualization
- Data Visualization: Line Plots
- Models and Simulations
- Models and Simulations: Empirical
- Models and Simulations: First Principles
- Models and Simulations: Physics-Based

All eight confirmed against the live `FunctionCategory` vocabulary on the target. Subcategories are
written `Parent: Child` with a space, the canonical form the API returns.

**`Models and Simulations` / `: First Principles` / `: Physics-Based`.** GLOW solves the two-stream
electron transport equation and an ion-neutral photochemistry system from cross sections and rate
coefficients. `docs/Glow.txt` describes the package as calculating "ionization and excitation rates,
energetic electron production and transport," and lists `ETRANS` as the routine that "computes
electron transport, ionization, excitation using Nagy & Banks 2-stream method". `src/ncarglow/fortran/`
contains the corresponding solvers: `etrans.f90`, `exsect.f` (electron impact cross sections),
`gchem.f90` (ion/electron/metastable densities), `ephoto.f90` (photoionization and photoelectron
production), `ssflux.f90` (solar flux scaling).

**`Models and Simulations: Empirical`, which the record did not previously carry.** GLOW bundles
and executes three empirical models on every run of the Python and Matlab interfaces, and passes
their output through to the user.
`src/ncarglow/fortran/mzgrid.f90` exists solely for this: its header reads "Subroutine MZGRID gets
fields from eMpirical models on default GLOW altitude grid." and it calls `gtd7` (NRLMSISE-00),
`snoemint`/`snoem` (NOEM) and `iri90` (IRI-90). `glowpython.f90` — the executable that the Python and
Matlab interfaces drive — calls `mzgrid` and then writes those quantities to standard output under the
column headings `Tn`, `O`, `N2`, `O2`, `NO`, `Ne(in)`, which `src/ncarglow/base.py` parses into the
returned `xarray.Dataset` as `Tn`, `O`, `N2`, `O2`, `NO`, `NeIn`. A Python user therefore receives
NRLMSISE-00, NOEM and IRI-90 output directly from a GLOW call. `docs/Glow.txt` states the same for the
example driver: "It uses NRLMSISE-00 and IRI-90 to specify the neutral atmosphere and initial electron
density profile, and the NOEM model to specify nitric oxide density."

This value does not contradict `First Principles`: GLOW's own airglow physics is first-principles, and
the empirical models supply its background atmosphere. Both are user-visible capabilities of the same
package.

**`Data Processing and Analysis` / `: Analysis`.** The package derives physical quantities beyond the
raw transport solution — Pedersen and Hall conductivities via `conduct.f90` (called per altitude level
in `glowpython.f90`), volume emission rates and vertical column brightnesses via `gchem.f90` and
`bands.f90`. On the Python side, `base.py:glowparse` converts GLOW's fixed-format text output into a
merged, labelled `xarray.Dataset` with `alt_km`, `wavelength`, `state` and `energy` coordinates.

**`Data Visualization` / `: Line Plots`.** `src/ncarglow/plots.py` exports
`__all__ = ["altitude", "density", "precip", "temperature", "ver"]`; the Matlab package provides
`+ncarglow/plotglow.m`. All four Python examples in `Examples/` import `ncarglow.plots` and call them.

**Considered and rejected — recorded so a later refresh does not re-propose them:**

- **`Data Visualization: 2D Graphics`.** Every plotting routine in `plots.py` draws with `ax.plot`;
  there is no `pcolormesh`, `imshow`, `contour` or image output anywhere in that module. `Line Plots`
  alone is the accurate answer.
- **`Data Processing and Analysis: Energy Spectra`.** This was genuinely close and the evidence is
  recorded so it can be reopened. In favour: the public `ebins(time, glat, glon, Ebins, Phitop)`
  entry point accepts an arbitrary electron energy grid and differential number flux; `egrid.f90`
  builds the energy grid; `maxt.f90` "Generates a Maxwellian electron spectrum"; `docs/Glow.txt`
  documents `UFLX` as "upward hemispherical electron flux; cm-2 s-1 eV-1" with a matching `DFLX`; the
  returned Dataset carries `precip` on an `energy` coordinate and `plots.precip` labels it
  "precipitation: differential number flux". Against, and decisive: the facet sits under
  *Data Processing and Analysis*, so a user filtering on it is looking for tooling that computes or
  analyses spectra from data. In GLOW the spectrum is an *input parameter* the user supplies and the
  atmospheric response is the product; the one spectrum GLOW generates, MAXT's analytic Maxwellian, is
  a convenience input generator. Someone with measured particle spectra to analyse would not reach for
  GLOW.
- **`Coordinate Transforms` and `Coordinate Transforms: Ionospheric`.** `geomag.f90` does convert
  between geographic and geomagnetic coordinates — `docs/Glow.txt` lists it as
  "Translates geographic to geomagnetic coordinates and vice versa". But it is an internal step, not a
  user-facing capability: it is absent from the Python `__all__`, absent from the Matlab package, and
  `docs/Todolist.txt` states that "GEOMAG now only handles coordinate transforms for the NOEM nitric
  oxide model, which is based on SNOE data that were analyzed with a simple offset-tilted-dipole model
  to begin with." `docs/Releasenotes.txt` lists the magnetic field routines under known issues as out
  of date. A user seeking an ionospheric coordinate-transform library must not be sent here.
- **`Servers and Environments` and `: High Performance Computing`.** GLOW does ship a real MPI
  program (`glowdriver.f90` has `use mpi`, `mpi_init`, `mpi_bcast`, gather buffers) and a batch script
  (`archive/runglow.job`, `mpirun -l -np $nproc $model < $input > $output`). But the *Servers and
  Environments* category is for infrastructure, deployment and runtime-environment software. GLOW is a
  parallel science *application*, not HPC tooling; a user browsing that facet for cluster
  infrastructure would find it out of place. The HPC capability is instead recorded where a user
  actually asks the question — Field 21, `HPC or HEC`.
- **`Models and Simulations: Data Guided`.** Every public Python entry point calls
  `gi.get_indices([time - timedelta(days=1), time], 81)` and passes measured F10.7 and Ap into the
  run, and `glowdriver.f90` can be driven by GCM history files. But solar and geomagnetic indices
  drive nearly every upper-atmosphere model, so the value would distinguish nothing; GLOW performs no
  data assimilation and has no observational boundary condition; and its GCM-driven mode is driven by
  *model* output rather than data. `Models and Simulations: Empirical` and Field 30's TIEGCM entry
  already carry the informative part.
- **`Data Processing and Analysis: Data Access and Retrieval`.** The geomagnetic-index download
  happens automatically inside a dependency; there is no user-callable data-retrieval function in this
  package's API. See Field 17, which turns on the same evidence.
- **`Data Processing and Analysis: File Format Conversion`** and **`: Processing`.** netCDF in,
  netCDF out is the MPI driver doing its own I/O rather than a conversion service, and `: Processing`
  would add nothing over `: Analysis`.
- **`Servers and Environments: Software or Environment Container`.** No Dockerfile, Singularity
  definition or container recipe is tracked at the pin.
- **`Models and Simulations: Observatory/Instrument Models`.** GLOW computes vertical column
  brightnesses, which are synthetic observables, but there is no instrument response, line-of-sight
  integration or viewing-geometry model in this repository. The geostationary-view and limb-scan
  comparisons in the 2017 paper were done outside the distributed code.

### 5. Related Region (RECOMMENDED — treated as critical)

**Values:**
- Earth Atmosphere
- Earth Ionosphere
- Earth Thermosphere
- Earth Auroral Subregion

All four confirmed against the live `Region` vocabulary on the target (24 rows). **The vocabulary is
flat** — there is no parent/child relationship between rows, so a coarse value never implies a fine one
and a fine value never implies a coarse one. Each of the four is therefore justified on its own
evidence, and *Earth Atmosphere encompasses the rest* is not an argument this file makes or accepts.

**`Earth Thermosphere`, which the record did not previously carry.** `docs/Glow.txt` opens by describing GLOW as calculating
"excited species densities, and airglow emission rates for the terrestrial thermosphere." The
describing publication is titled "Global modeling of thermospheric airglow in the far ultraviolet".
`pyproject.toml` declares `keywords = ["thermosphere", "ionosphere"]`.

**`Earth Ionosphere`, which the record did not previously carry.** `docs/Glow.txt`: "Outputs include electron density
calculated below 200 km, ionized and excited species density, airglow volume emisison rates, and
vertical column brightnesses." (the misspelling is the source's). `glowpython.f90` writes columns
`Ne(in)`, `Ne(out)`, `O+`, `O2+`, `NO+`, `Pederson`, `Hall`; `conduct.f90` "Calculates ionospheric Hall
and Pederson conductivities". `pyproject.toml` declares `ionosphere` as a keyword.

**`Earth Auroral Subregion`, which the record did not previously carry.** Three of the four public Python entry points are
auroral precipitation specifications: `maxwellian` (Maxwellian precipitation with total energy flux and
characteristic energy), `ebins` (user-specified energy grid and flux into the top of the atmosphere),
and `no_precipitation` (the explicit null case, which only exists because precipitation is the normal
case). `docs/Glow.txt`: "Solar flux, and auroral electron flux, are specified or calculated from
parameters." `archive/in.basic.aur` is the shipped auroral driver input. Every example and test uses
`glat = 65.1, glon = -147.5` — Poker Flat, Alaska, in the auroral oval.

**`Earth Atmosphere` — retained.** Carried over from the existing HSSI record. It is independently
true: GLOW is a terrestrial upper-atmosphere model, and the flat vocabulary means retaining it costs
nothing and preserves how the record was previously found. It is not redundant with the three specific
values, because the vocabulary has no containment semantics.

**Considered and rejected:**

- **`Earth Lower and Middle Atmosphere`.** The tempting evidence is that TIME-GCM input extends the
  grid down to about 30 km. But `docs/Glow.txt` states plainly that "This is not a problem for the
  TIME-GCM since its altitude grid extends down to ~30 km, but note that GLOW does not yet contain
  full D-region chemistry or mesopause-region recombination emissions." `docs/Todolist.txt` lists the
  O2 A-bands work as still to do and says it will "need to deal with recombination, and O3 if we go
  into the mesosphere" — future tense. The Python altitude grid starts at `minalt=60.` km but the
  chemistry that would make results there meaningful is absent. A user filtering for
  lower/middle-atmosphere software would be misled.
- **`Solar Environment`.** GLOW scales a solar EUV spectrum (`ssflux.f90`, EUVAC and Hinteregger
  models) as an *input*. It models nothing in the solar environment.
- **`Earth Magnetosphere`** and its sub-regions. Auroral precipitation arrives at the top of GLOW's
  grid as a specified boundary condition; nothing magnetospheric is modelled.

### 6. Authors (MANDATORY)

**Recorded values (unchanged from the existing HSSI record):**

**Author 1 — Michael Hirsch**
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliations:**
  - Boston University — https://ror.org/05qwgg493
  - Scivision, Inc. — no ROR recorded

**Author 2 — Stanley C. Solomon**
- **Author Identifier:** https://orcid.org/0000-0002-5291-3034
- **Affiliation:** NSF NCAR High Altitude Observatory — https://ror.org/03773p874

**Provenance of the identifiers, which the DOI record does not supply.** DataCite's creators for
`10.5281/zenodo.3344536` are the bare strings `Scivision` and `Solomon, Stan`, with empty
`nameIdentifiers` and empty `affiliation` arrays; Zenodo record 8309940 lists `scivision` and
`Stan Solomon` with `affiliation: null`. Both ORCIDs and both RORs came from prior research, not from
the DOI, and must not be dropped on the grounds that the DOI record does not carry them.

**"Scivision" is Michael Hirsch, not a separate person or an organization.** This is now directly
provable from the repository rather than by inference: the commit history reachable from the pin
attributes commits to `Michael Hirsch, Ph.D <10931741+scivision@users.noreply.github.com>`,
`Michael Hirsch <scivision@users.noreply.github.com>` and `scivision <scivision@users.noreply.github.com>`
— the GitHub account numbered 10931741 and the handle `scivision` are the same identity that signs as
Michael Hirsch. Recorded so a future refresh reading DataCite's `Scivision` string does not create a
second author record or mistake it for a company acting as an organizational author. (Scivision, Inc.
is separately and correctly recorded as one of his *affiliations*.)

**Stanley C. Solomon — identity and identifier.** An early revision of this file recorded
"Stan Solomon" with no identifier or affiliation. ORCID `0000-0002-5291-3034` is Stanley Solomon,
scientist at the National Center for Atmospheric Research, and its other-names list contains both
"Stan Solomon" and "Stanley C. Solomon" — the author's own record reconciles the two forms, so this is
not an inference from a shared surname. GLOW is an NCAR model and `docs/Glow.txt` gives his contact
address as "Stan Solomon, HAO/NCAR, Boulder, CO 80301". The commits from `stans@ucar.edu` in this
repository's history are his. The same person is an author of TIEGCM v3.0 in this catalogue, and the
catalogue holds one record for him rather than one per spelling. DataCite's `Solomon, Stan` is
preserved here as this project's own creator string so a future refresh recognises it.

**The `Scivision, Inc.` / `SciVision, Inc.` capitalisation difference is parked catalogue-wide and is
deliberately not addressed here.** It is not a defect in this record and must not block it.

---

#### The six upstream GLOW colleagues, and why they are documented here rather than recorded as authors

**Michael Hirsch and Stanley C. Solomon are the authors of this record. That is settled.** The
reasoning below, and the full credit evidence for six further people found in the vendored Fortran,
is preserved so a later refresh can see what was weighed and does not have to redo the sweep or
re-propose a name that was considered and set aside.

**The governing principle: this record's authorship follows the packaging's own creator list.** The
HSSI entry is `space-physics/NCAR-GLOW`, Michael Hirsch's Python and Matlab packaging of Solomon's
model, published under its own Zenodo DOI — and both authoritative records for that deposit name
exactly two creators. Zenodo record 8309940 lists `scivision` and `Stan Solomon`; DataCite's record
for the concept DOI lists `Scivision` and `Solomon, Stan`. The version-control history reachable from
the pin agrees: it contains commits from Michael Hirsch and Stan Solomon only. The people credited in
the vendored Fortran headers are contributors to the upstream NCAR model, not creators of this
packaging, and promoting them to catalogue authors of this record would assert something neither the
deposit nor the repository says.

`src/ncarglow/fortran/Glowlicense.txt` section 2 states: "This software was written by Stanley C.
Solomon and colleagues, as noted in the individual files." Those colleagues are real and are named
below in full — that instruction is why the sweep was done, and their credits are durable evidence
about what is inside GLOW even though they do not become authors of this entry.

**How the sweep was done, so a later refresh can re-run and extend it.** Of the 117 files tracked at
the pin, the 30 numeric data tables (`*.asc`, `*.dat`) were skipped and the remaining 87 text-bearing
files were read in full — all `.f`/`.f90`, `.m`, `.py`, `.ipynb`, `.txt`, `.md`, `.toml`, `.build`,
`.yml`, the `CMakeLists.txt` files, the Makefiles and the driver inputs. Each was scanned for three
separate credit shapes: a personal-name pattern
allowing internal capitals and apostrophes in the surname, so that names like `McGranaghan` are not
dropped; initials-style credits adjacent to a date, which is how `SCS`/`scs` (Stan Solomon) and `btf`
(Ben Foster) appear; and the tokens `author`, `credit`, `copyright`, `written by`, `coded by`,
`thanks`, `contribut` and `maintainer`. **A narrower personal-name pattern is the specific trap here:
a surname regex of the form `[A-Z][a-z]+` silently drops `McGranaghan`, and an eyeball pass over
file headers alone misses the credits that sit mid-file** — Ann Windnagel's is at line 592 of
`exsect.f`, several hundred lines below its header. An earlier revision of this file listed only three
candidates for exactly those reasons.

**Result of the sweep.** All six people below are credited in the vendored Fortran, and every credit
that names someone other than the two recorded authors lies there. The sweep turned up no
personal name at all in the `.m`, `.py` and `.ipynb` sources, the Meson and CMake build files, the CI
workflow, the `Examples/` scripts or the driver inputs. The one Fortran file outside
`src/ncarglow/fortran/` — `archive/glowbasic.f90` — credits only "Adapted from glowdriver by Stan
Solomon, 2/2016". In the documentation the only person credited for a contribution is Michael Hirsch,
thanked in `docs/Releasenotes.txt` for identifying a bug; he is already a recorded author. The other
people named in `docs/Glow.txt` appear in its bibliography and in parenthetical source attributions
against subroutine entries, which are citations rather than credits for GLOW code.

| Candidate | Attribution at the pin, quoted as written | Files carrying a credit | Compiled? |
|---|---|---|---|
| **Ben Foster** | "Stan Solomon and Ben Foster, 1/2015" in `cglow.f90` and `glowdriver.f90`; "Ben Foster and Stan Solomon, 1/15" in `output.f90` and `readtgcm.f90`; "Replaced common blocks with use-associated variables defined in module cglow, Ben Foster, 2015" in `exsect.f`; "Converted common blocks to use-associated variables, Ben Foster, 2015" in `ephoto.f90`; and by his initials, "Moved common blocks into use-associated variables defined in cglow.f90, btf, 2015", in `etrans.f90` | **7** | 4 in the always-built `cglow` library (`cglow.f90`, `exsect.f`, `ephoto.f90`, `etrans.f90`); 3 in the optional MPI driver (`glowdriver.f90`, `readtgcm.f90`, `output.f90`) |
| **Scott M. Bailey** | "Scott Bailey, 12/1993" in the "Modification history:" block of `ssflux.f90`, against the initial one-nm bins version; "Reads cross sectons from files (for 1-nm bins), Scott Bailey, ~1994" in `ephoto.f90` (the misspelling "cross sectons" is the source's); "Scott Baily and Stan Solomon, 9/1994" in `rout.f90` — that third header misspells the surname, which is correctly Scott Bailey, as `docs/Glow.txt` confirms by citing "Bailey, S. M., C. A. Barth, and S. C. Solomon" in its reference list | **3** | 2 in the always-built `cglow` library (`ssflux.f90`, `ephoto.f90`); `rout.f90` is in neither build system |
| **Ryan McGranaghan** | "Ryan McGranaghan, 2014" in `conduct.f90`; `docs/Releasenotes.txt` for v0.98 records "Calculates conductivities using Ryan McGranaghan's CONDUCT routine (adapted)."; `docs/Glow.txt` cites "(McGranaghan et al., 2016)" against the CONDUCT entry | **1** | yes — `conduct.f90` is in `utils_src`, and `glowpython.f90` calls `conduct` once per altitude level on every run |
| **Liying Qian** | "Corrected additional Auger problem, Liying Qian, 11/2002" in `ephoto.f90` | **1** | yes — `ephoto.f90` is in `cglow_src` |
| **Chris Gaskill** | "Chris Gaskill, 7/1989" in the "Modification history:" block of `ssflux.f90`, against adding the early Tobiska model | **1** | yes — `ssflux.f90` is in `cglow_src` |
| **Ann Windnagel** | "Originally coded by Ann Windnagel, 11/98" in `exsect.f`, against subroutine HEXC (the high-energy cross-section correction), immediately followed by "Re-written by Stan Solomon, 2/99" | **1** | yes — `exsect.f` is in `cglow_src` |

**Scott M. Bailey's case is stronger than an earlier revision of this file claimed, and that claim is
retracted.** That revision argued his case was weak because `rout.f90` is absent from both build
systems, so this packaging neither compiles nor runs it. That remains true of `rout.f90` — and it is
irrelevant, because it was never his only credit. He is also credited in `ssflux.f90` and
`ephoto.f90`, both of which are in `cglow_src` in `src/ncarglow/fortran/meson.build` and in
`target_sources(cglow ...)` in `src/ncarglow/fortran/CMakeLists.txt`, and both of which
`docs/Glow.txt` lists among the subroutines called by GLOW. Every Python or Matlab run executes them.
His attributed contribution — the move to one-nanometre solar-flux and cross-section bins — is
moreover architectural rather than a bug fix. `docs/Releasenotes.txt` for v0.97 records the solar-flux
default as "Default is ~1 nm grid (5 nm in FUV)", and `docs/Glow.txt` states that "The number of
wavelenth bins in the ephoto and ssflux files must equal the parameter LMAX specified in module CGLOW"
(the misspelling is the source's) — the one-nanometre bin structure is still the model's organising
scheme in both routines he is credited in.

**Identity research on the six, recorded so it does not have to be redone.** Three of the six could
be identified with reasonable confidence and three could not, which is itself part of why the
authorship line falls where it does.

- **Ryan McGranaghan** — HSSI holds a person record for him carrying ORCID
  `https://orcid.org/0000-0002-9605-0007`.
- **Liying Qian** — HSSI holds a person record for her carrying ORCID
  `https://orcid.org/0000-0003-2430-1388`. **What the identification rests on, stated honestly:** the
  ORCID record itself publishes no employment history and so proves nothing about identity on its own.
  The link is that the same record is an author of TIEGCM v3.0 in this catalogue alongside Stanley C.
  Solomon, i.e. the same NCAR High Altitude Observatory group and the same era as the `ephoto.f90`
  credit. That is a strong circumstantial match, not a proof.
- **Scott M. Bailey** — the matching ORCID is `https://orcid.org/0000-0001-7693-0966`, whose ORCID
  employment record is Professor, Bradley Department of Electrical and Computer Engineering, Virginia
  Polytechnic Institute and State University (ROR `https://ror.org/02smfhw86`), with prior affiliation
  at the University of Colorado Boulder. That matches the aeronomer who co-authored the SNOE nitric
  oxide papers with Solomon. The ORCID record carries no publication list confirming the match, so
  this is a strong but not airtight identification. HSSI holds no record for him, and the only stored
  "Bailey" is **Rachel L. Bailey**, a different person, who must never be reused for him.
- **Ben Foster** — no ORCID could be found. An ORCID public search on the name returns two records,
  neither with any atmospheric-science or NCAR affiliation, so neither can be attached to him. HSSI
  holds no record for him.
- **Ann Windnagel** — ORCID `https://orcid.org/0000-0001-6396-3523` (University of Colorado Boulder)
  is the sole record under that surname, and the surname is rare enough that it is probably her.
  Nothing links that record to 1998 cross-section work, though, so the identification is unconfirmed
  and must not be treated as established. HSSI holds no record for her.
- **Chris Gaskill** — ORCID `https://orcid.org/0000-0002-7384-7750` is the only record matching the
  name and it publishes no affiliation, so it cannot be tied to a 1989 solar-flux contribution at
  NCAR. He is unidentifiable on present evidence. HSSI holds no record for him.

**What their contributions amount to, recorded because it is the evidence a later refresh would need
to revisit this.** Foster's is structural — the module-based rewrite that made the MPI version
possible, plus the netCDF I/O and TIE-GCM reader modules. Bailey's is architectural, as set out above.
McGranaghan's named routine runs on every call. Against that, three of the six are single historical
fixes to code since rewritten or superseded: Qian's one Auger-electron correction in 2002; Gaskill's
1989 addition to a solar-flux routine that `docs/Releasenotes.txt` records as "SSFLUX completely
re-written" for v0.97; and Windnagel's original HEXC code, re-written by Solomon three months later
and re-designed again in 4/99. Two of those three cannot be identified with confidence in any case.

**Where the line falls, and why it is not drawn at "wrote some code that ships here".** The repository
also contains substantial third-party code whose authors plainly are not GLOW's authors:
`nrlmsise00.f` (NRLMSISE-00, Picone et al.), `iri90.f` (IRI-90, Bilitza) and the NOEM implementation
in `snoem.f90`, which `snoem.f90` records as "Adapted by Stan Solomon, 5/2014, from IDL and F90 code
supplied by Dan Marsh." `docs/Glow.txt` marks those as external in exactly those terms — "Versions of
NRLMSISE-00 and IRI-90 are provided for the convenience of users who do not have their own copies."
and "Attribution to the appropriate sources (Picone et al, 2002; Belitza, 1990) should be made." On
the same reasoning, A. F. Nagy and P. M. Banks are not author candidates either: the licence lists the
two-stream algorithm among "source code obtained from a variety of sources", and `exsect.f` records it
as "Adapted from Banks & Nagy 2-stream code by Stan Solomon, 1988" — the GLOW implementation is
Solomon's. So the repository already contains three tiers of authorship, and a catalogue author field
that tried to represent all of them would say less, not more.

**Searcher's-eye check on the outcome.** Would someone on Ben Foster's or Liying Qian's HSSI author
page be glad to see NCAR-GLOW listed there? Their code is genuinely inside it, but what the entry
points to is a Python packaging neither of them worked on, and the upstream model they did work on is
better represented in the catalogue by TIEGCM v3.0, where Qian is already an author. Listing them here
would send a reader to the wrong artifact. The credits stay in this dossier, where they are precise
about which file and which change, instead of in a field that would flatten them into "wrote GLOW".

**Considered and set aside, and a trap worth naming: Arthur D. Richmond.** `conduct.f90` names him, and
HSSI holds a person record for him carrying ORCID `https://orcid.org/0000-0002-6708-1023`, so it would
be easy to add him by mistake. The credit is not GLOW's. The line sits inside a block that
`conduct.f90` itself introduces as "Comment from TIE-GCM source code in file lamdas.F:", and it reads
"Multiply rnu_ne by 4, as per Art Richmond:" — a TIE-GCM comment, copied into GLOW along with the
collision-frequency formulation, acknowledging his scientific recommendation. It credits no GLOW code.
For the same reason the `btf` initials on that line are **not** a seventh Foster credit: they belong
to the quoted TIE-GCM comment, not to GLOW.

**Also considered and set aside: Randy Gladstone.** `rout.f90` names him only as the author of the
external program its output is written for — "in order to transfer them to Randy Gladstone's REDISTER
radiative transfer program." That is a destination, not a contribution.

---

### 7. Software Name (MANDATORY)
**Value:** GLOW

**Four names are in play, and a reader should not have to guess how they relate:**

| Name | Where it comes from |
|---|---|
| `GLOW` | The README's top-level heading is `# GLOW`; `src/ncarglow/meson.build` declares `project('GLOW', 'fortran',`; the PyHC registry entry's `name:` is `GLOW`; this is the stored HSSI value |
| `NCAR-GLOW` | The GitHub repository name, which distinguishes this packaging from other software called GLOW |
| `ncarglow` | `pyproject.toml` declares `name = "ncarglow"`; this is the Python import path |
| `GLOW` / "The Global Airglow (GLOW) model" | The underlying model. `docs/Glow.txt` calls it "The GLobal airglOW (GLOW) model"; the 2017 paper's abstract opens "The Global Airglow (GLOW) model has been updated and extended" |

**Decision: keep `GLOW`, decided from the searcher's side.** A user hunting for the GLOW model or a
way to run it from Python types "GLOW" or "NCAR GLOW", not `ncarglow`. `ncarglow` is an import-path
artifact that would be actively unhelpful as a display name, and it is **not an install handle
either**: both `ncarglow` and `ncar-glow` are absent from PyPI — the JSON API
(`https://pypi.org/pypi/ncarglow/json`) and the Simple API (`https://pypi.org/simple/ncarglow/`) each
return 404, and those are the authoritative endpoints because the HTML project page answers 200 even
for names that do not exist. Installation is `pip install -e` from a clone, per the README. The PyPI
package literally named `glow` is `arquolo/glow`, "Functional Python tools", and is unrelated.

**On disambiguation.** HSSI separately holds **pyglow**, Timothy Duly's package, which is different
software (see Field 29). That is a reason the name must be unambiguous, and `GLOW` is: nothing in the
catalogue is likely to be confused with `pyglow` in a result list. `NCAR-GLOW` would add provenance at
the cost of reading like a repository slug, and the NCAR provenance is already carried prominently
elsewhere: Field 9 opens with the words NCAR GLOW 0.981, and Field 8 names NCAR GLOW version 0.981.

### 8. Description (MANDATORY)
**Value:**

> The GLobal airglOW Model (GLOW) is a physics-based model for simulating auroral and airglow phenomena in Earth's ionosphere and thermosphere. GLOW computes number densities of neutrals, ions and electrons; Pedersen and Hall currents; volume emission rates versus wavelength and altitude; and precipitating flux versus energy. This implementation provides Python, Matlab, and Fortran interfaces to NCAR GLOW version 0.981, with the Python interface being the recommended approach. The model uses first-principles physics to simulate the effects of auroral precipitation on the upper atmosphere.

**Source:** carried over unchanged from the existing HSSI record, itself compiled from the README, the
PyHC registry entry and the DataCite description.

**Checked for factual drift at the pin, and it holds.** The version claim is right —
`src/ncarglow/meson.build` declares `version : '0.981'` and `docs/Glow.txt` is headed "Version 0.981".
The output list matches the README's bullets and `glowpython.f90`'s output columns. The recommendation
of Python matches the README's "Python is the easiest and recommennded choice." (the misspelling is the
README's). No wording change is proposed: the phrasing is a prior curator's editorial choice and a
stylistic alternative would not be an improvement.

**One imprecision noted but not corrected.** "Pedersen and Hall currents" would more accurately read
"conductivities" — `conduct.f90` returns conductivity in S/m and the output columns are `Pederson` and
`Hall` conductivities. The README uses the word "currents" too, so the description faithfully reflects
its source. Flagged here rather than silently rewritten.

### 9. Concise Description (OPTIONAL)
**Value:** NCAR GLOW 0.981 aurora/airglow model for Earth's ionosphere and thermosphere, accessible from Python, Matlab, and Fortran.

**Source:** carried over unchanged from the existing HSSI record; adapted by an earlier curator from
the PyHC registry description, which reads "NCAR GLOW 0.981 aurora/airglow model IR-VIS-UV from
Python". 122 characters, within the 200-character limit. No change proposed.

### 10. Publication Date (RECOMMENDED)
**Value:** 2005-04-01

**Source:** `docs/Releasenotes.txt` ends with the earliest software-specific release note in the
repository, headed "Version 0.97 release notes, Stan Solomon, 4/2005". The 2017 paper independently
states that a version codified as v0.97 was released in 2005.

**The day is a format accommodation, not evidence.** No exact release day is recoverable from any
source examined; the release note gives month and year only. The first of the month satisfies HSSI's
full-date requirement while preserving the earliest software-specific evidence found. Recorded so a
future refresh does not mistake `-01` for a discovered value or try to "correct" it.

**Why not a later date.** Field 10 records the date of first publication, for the initial version of
the software. The Zenodo publication date (2023-09-01) belongs to the current release and
is recorded in Field 12; the 2017 v0.981 release and the 2019 first Zenodo deposit are both later than
the model's first public release.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

**Source and confirmation.** Zenodo record 8309940 carries the related identifier
`{"identifier": "https://github.com/space-physics/NCAR-GLOW/tree/v1.4.0", "relation": "isSupplementTo",
"scheme": "url"}`. A `tree/<tag>` URL under an `isSupplementTo` relation is the signature the GitHub–
Zenodo release integration writes; a hand-made deposit does not produce it. So the DOI was minted
through that integration and Zenodo is the publisher, which is what the form's guidance prescribes for
this case. DataCite reports `publisher: "Zenodo"` for the concept DOI. Unchanged.

### 12. Version (RECOMMENDED)
- **Version Number:** v1.4.0
- **Version Date:** 2023-09-01
- **Version Description:** Require Python >= 3.9; fixed geomagindices package for current Pandas versions. This GLOW implementation remains as an almost zero modification to the original source code. The Matlab/Python interface uses a command line interface to GLOW, running GLOW as a separate process to avoid thread-safety issues.
- **Version PID:** https://doi.org/10.5281/zenodo.8309940

**Four independent sources agree, and they were checked against each other rather than assumed.** The
tag `v1.4.0` resolves to commit `da1e2623e129066f1dae72daf8206e8653d62dfa` (2023-09-01, "cleanup for
release"), which is an ancestor of the pin. `pyproject.toml` at the pin declares `version = "1.4.0"`.
Zenodo record 8309940 reports `version: "v1.4.0"` and `publication_date: "2023-09-01"`, with
`conceptdoi: "10.5281/zenodo.3344536"`. The stored version description is the Zenodo description with
its HTML list flattened to prose.

**Durable oddity worth knowing at the next refresh.** There is no PyPI artifact for this or any other
version, so a version check cannot be done against a package index; the tag, `pyproject.toml` and the
Zenodo record are what a future refresh has to reconcile instead. Note that `src/ncarglow/meson.build`
also carries `version : '0.981'`, which is the bundled **model** version rather than this package's,
and must not be mistaken for a release number. See Field 7 for the PyPI evidence.

**Note on `main` moving after the tag.** The pin (2023-09-20) is 19 days later than the tagged release
and carries a single one-line units correction applied consistently across four files —
`+ncarglow/TestGlow.m`, `Examples/Maxwellian.m`, `src/ncarglow/fortran/glowpython.f90` and
`src/ncarglow/plots.py` (four insertions, four deletions in total). That does not constitute a newer
version; v1.4.0 remains the current release.

### 13. Programming Language (RECOMMENDED)
**Values:** Fortran77, Fortran90, MATLAB, Python 3.x

All four confirmed against the live `ProgrammingLanguage` vocabulary on the target. Unchanged.

**Evidence for each.** *Fortran77*: `docs/Glow.txt` states there are "some routines still coded in
fixed-format Fortan-77 style, including exsect.f and fieldm.f." (the misspelling is the source's); the
`.f` files at the pin are `exsect.f`, `fieldm.f`, `iri90.f` and `nrlmsise00.f`. *Fortran90*: the bulk
of `src/ncarglow/fortran/` is `.f90`, and `docs/Glow.txt` says "These routines are written in standard
Fortran-90 and MPI, and should be compatible with most compilers." *MATLAB*: the `+ncarglow/` package
provides five public functions — `glow.m`, `glowenergy.m`, `loggrid.m`, `plotglow.m`, `TestGlow.m` —
over seven private helpers in `+ncarglow/private/` (`build.m`, `cmake.m`, `dt2utsec.m`, `exepath.m`,
`glowparse.m`, `meson.m`, `runcmd.m`).
*Python 3.x*: `pyproject.toml` declares `requires-python = ">=3.9"` and CI runs Python 3.9 and 3.11.

**Not recorded.** The build systems (CMake, Meson) are build tooling, not languages the software is
written in, and the vocabulary has no rows for them. `Fortran 2003`/`2008`/`2023` rows exist but the
Meson project sets `fortran_std=legacy` and the sources do not require a later standard.

### 14. Reference Publication (OPTIONAL)
**Value:** https://doi.org/10.1002/2017JA024314

**Full citation:** Solomon, S. C. (2017), Global modeling of thermospheric airglow in the far
ultraviolet, *Journal of Geophysical Research: Space Physics*, **122**(7), 7834–7848,
doi:10.1002/2017JA024314. Published online 2017-07-17. Free access.

**Why this replaces the previously stored value.** Field 14 asks for the DOI for the publication that describes the software. The 2017 paper is that publication and says so: its abstract states "This
paper describes the inputs, algorithms, and code structure of the model". It also documents the
release this repository packages — `docs/Glow.txt` is dated 3/2017 for version 0.981, and the paper's
abstract records that the model code is provided to the community through an open-source academic
research license, which is the arrangement Field 15 is about.

**Previously stored value, and where it went.** HSSI held
`https://doi.org/10.1029/JA093iA09p09867` — Solomon, S. C., P. B. Hays and V. J. Abreu (1988), The
auroral 6300 Å emission: Observations and modeling, *J. Geophys. Res.*, **93**, 9867–9882. That is a
real and important GLOW paper, but it describes an early *formulation* of the model rather than the
distributed software, and it predates the code in this repository by nearly three decades. It is not
discarded: it moves to Field 27, where the developer's own citation list puts it.

**Provenance of the developer's citation list.** `docs/Glow.txt` ends with a section headed
"References/Citations:" listing seven papers. The same list is served, and is current, at
`https://download.hao.ucar.edu/pub/stans/glow/refs/glowrefs.txt`.

**Upstream typo — do not propagate it.** The live `glowrefs.txt` renders the 2017 paper's identifier as
"doi:1002/2017JA024314", missing the `10.` registrant prefix. That string does not resolve. The
correct DOI is `10.1002/2017JA024314`, confirmed against Crossref, which returns the matching title,
author, volume and pages. The bundled `docs/Glow.txt` copy of the list predates publication and cites
the paper as submitted with no DOI at all.

### 15. License (RECOMMENDED)

**License:** Other
**License URI:** None. Not an omission — a licence URI specific to this software has nowhere to be
stored. See the end of this field.

Confirmed against the live `License` vocabulary on the target.

**Why `Other` and not something more specific.** GLOW's actual licence is the "GLOW MODEL OPEN SOURCE
ACADEMIC RESEARCH LICENSE AGREEMENT", and that name is not in HSSI's vocabulary. The `License` list is
closed — the serializer resolves it by exact, case-insensitive name match and rejects anything else —
and has exactly eleven rows:

> Apache License 2.0 · BSD 2-Clause "Simplified" License · BSD 3-Clause "New" or "Revised" License ·
> Creative Commons Attribution 4.0 International · GNU General Public Licenses (GPL version 2) ·
> GNU General Public License v3.0 or later · GNU Lesser General Public License v3.0 only ·
> GNU Library or ‘Lesser’ General Public Licenses (LGPL version 2) · MIT License · Other · Restricted

That enumeration is the durable reason the accurate answer is unavailable. The value therefore has to
be one of those eleven, and `Other` is the vocabulary's designated answer for a licence that is not on
the list — the Field 15 guidance says explicitly that an SPDX title with no matching row should use
`Other`. It is the only one of the eleven that asserts nothing the licence text does not support.

**An earlier revision of this file recorded `Open Source Academic Research License Agreement` as the
value.** That is the licence's true name but it was never storable, and recording it would have failed
the whole submission on an unknown-value error. It is corrected to `Other` here.

**The licensing facts, which are genuinely dual.**

1. **The repository root is Apache 2.0.** `LICENSE.txt` is 201 lines of the Apache License, Version
   2.0, January 2004. This is the wrapper author's licence on the packaging he wrote.
2. **The GLOW model itself is under UCAR's academic licence.** `src/ncarglow/fortran/Glowlicense.txt`
   and `docs/Glowlicense.txt` are byte-identical copies (verified by checksum) of the
   "GLOW MODEL OPEN SOURCE ACADEMIC RESEARCH LICENSE AGREEMENT". Its section 1 grants a licence "for
   research, academic, and non-profit purposes" (the source has no period there). Section 3a is
   headed "No Sales." and states: "You shall not sell, or license or transfer for a fee the Software,
   or any work that in any manner contains the Software." Section 5 states: "Title, ownership rights,
   and intellectual property rights in the Software shall remain in UCAR."
3. **The model documentation says the academic agreement governs.** `docs/Glow.txt`: "Use is governed
   by the Open Source Academic Research License Agreement contained in the file Glowlicense.txt."
   Nineteen of the twenty-nine Fortran sources in `src/ncarglow/fortran/` repeat that notice (twenty
   of the thirty Fortran files at the pin, counting `archive/glowbasic.f90`). **Three of the nineteen
   — `egrid.f90`, `etrans.f90` and `maxt.f90` — carry the identical sentence lowercased**
   ("academic research license agreement contained in the file glowlicense.txt."), so a case-sensitive
   search undercounts by three; an earlier revision of this file did exactly that. The ten
   `src/ncarglow/fortran/` files without the notice are a meaningful set rather than an oversight:
   they are the bundled third-party models and IRI excerpts (`iri90.f`, `nrlmsise00.f`, `snoem.f90`,
   `snoemint.f90`, `geomag.f90`, `fieldm.f`), McGranaghan's `conduct.f90`, and the three files this
   packaging added (`glowpython.f90`, `fsutils.f90`, `utils.f90`). The notice tracks GLOW-proper code.
4. **Zenodo classifies the deposit as `other-open`** (`license: {"id": "other-open"}` on record
   8309940). DataCite reports only `rights: "Open Access"`.
5. **The describing publication says the same.** The 2017 abstract states that the GLOW model code is
   provided to the community through an open-source academic research licence.

**The two other storable values were considered and rejected.**

- **`Restricted`.** The form's own text says "If the software is restricted, enter 'Restricted'.", and
  the agreement does restrict use to research, academic and non-profit purposes, forbid sale or
  fee-bearing transfer, and keep title with UCAR — so a commercial user genuinely may not use this
  software. It is rejected because the flag would mislead in the other direction: the licence calls
  itself "OPEN SOURCE", the code is publicly downloadable with no access request, and Zenodo
  classifies it `other-open`. In this catalogue `Restricted` reads as *you must request access*, which
  is false here. The commercial-use restriction is real and is recorded in this dossier instead, where
  it can be stated precisely rather than compressed into one misleading word.
- **`Apache License 2.0`.** It is what `LICENSE.txt` at the repository root says, it is what GitHub
  and most tooling report for this repository, and it is genuinely the licence on the wrapper code.
  It is rejected as the most misleading of the three: the bundled model — the overwhelming majority of
  the distributed source, and the whole scientific value — is not Apache-licensed, and Apache 2.0
  permits commercial use that the GLOW agreement forbids. Recording it would tell a commercial user
  they may do something they may not.

**A licence URI cannot be recorded for this software, and that is permanent rather than an omission.
A future refresh should not attempt it.** The licence a record carries is a reference to one of the
eleven shared vocabulary rows, and the URI belongs to that row rather than to the software — a
`License` row is just `id`, `name` and `url`. Nothing in the model holds a URI for one particular
piece of software. So a GLOW-specific link to the UCAR agreement has nowhere to sit: the only URI
associated with this record is whatever the shared `Other` row carries, which is not GLOW's to define
and would be the wrong answer for the UCAR agreement in any case. The earlier revision's `License URI`
value was therefore unstorable for two independent reasons — its licence *name* was not a vocabulary
row, and the field it aimed at is not a per-software field.

**Where the actual terms live.** Readers who need them should go to
`src/ncarglow/fortran/Glowlicense.txt` in the repository (byte-identical to `docs/Glowlicense.txt`).
That pointer is the practical substitute for the URI this field cannot hold.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values:** airglow, aurora, ionosphere, thermosphere, electron precipitation

All five exist as rows in the live `Keyword` vocabulary on the target, so none of them mints a new row.
Keywords is the only open vocabulary in the form, which makes reusing an existing row rather than
coining a near-duplicate the important discipline here.

**Correction to a prior mis-attribution.** An earlier revision of this file attributed all four stored
keywords to the "pyproject.toml keywords field, PyHC keywords, SoMEF". `pyproject.toml` at the pin
declares only `keywords = ["thermosphere", "ionosphere"]`. `airglow` and `aurora` come from the
software itself and its documentation (the model's name expands to "GLobal airglOW"; the auroral
precipitation entry points), not from `pyproject.toml`.

**`electron precipitation`, which the record did not previously carry.** Three of the four public Python entry points exist
to specify or suppress precipitating electron flux (`maxwellian`, `ebins`, `no_precipitation`), and
`docs/Glow.txt` describes `PHITOP` as "energetic electron flux into top of atmosphere; cm-2 s-1 eV-1".
A user browsing that keyword would find precisely the tool they want.

**PyHC's domain tags were tested rather than inherited, and both were rejected.** The PyHC registry
entry carries `keywords: ["ionosphere_thermosphere_mesosphere", "specific"]`. Rows exist for both, so
this is a relevance judgement, not a vocabulary limitation.
- `ionosphere_thermosphere_mesosphere` is a registry taxonomy bucket, not a science keyword; its
  underscored form is a registry artifact; and its mesosphere component is contradicted by
  `docs/Glow.txt` (see Field 5). Its ionosphere and thermosphere components are already covered by the
  two plain keywords.
- `specific` is PyHC's general/specific classification flag and carries no science meaning at all.

**Other candidates considered and rejected:**
- `electron density` — a genuine output, but GLOW takes electron density as an a-priori *input* above
  200 km and only calculates it below, so a searcher for an electron-density model is better served by
  IRI. Recorded so it is not proposed again without that caveat.
- `ionospheric conductance` — the closest existing row, but GLOW computes conductivity in S/m
  (`conduct.f90`), not height-integrated conductance. Adding it would be imprecise.
- `TIEGCM`, `msis`, `iri` — rows exist and GLOW genuinely couples to or bundles all three, but the
  relationship is already expressed where it belongs, in Fields 29 and 30. Duplicating it as keywords
  adds noise.
- `pedersen`, `hall`, `volume emission rate`, `electron transport` — no rows exist, and coining them
  for a single record is exactly the near-duplicate minting the field guidance warns against.

### 17. Data Sources (OPTIONAL)

**Value:** None — an evidenced empty, not an unexamined gap.

**What the software actually fetches.** GLOW's own code names no data archive, but every public Python
entry point in `src/ncarglow/base.py` — `maxwellian`, `no_precipitation`, `no_source` and `ebins`,
which is all four names in `__all__` — calls `gi.get_indices([time - timedelta(days=1), time], 81)`
and passes the returned F10.7 and Ap values into the model run. That call is `geomagindices`, whose
README states that it "returns Ap, F10.7 (unsmoothed and smoothed) and Kp", with its Notes section
linking Kp and Ap to `ftp://ftp.gfz-potsdam.de/pub/home/obs/kp-ap/wdc/` and F10.7 to
`ftp://ftp.geolab.nrcan.gc.ca/data/solar_flux/daily_flux_values/fluxtable.txt`. So running GLOW from
Python does, in practice, pull data from GFZ Potsdam and from Natural Resources Canada, and it does so
on every run without being asked.

**Why that does not make `GFZ` the right value here.** Decided from the searcher's side: someone
filtering HSSI for `GFZ` is looking for software that reads GFZ data products, and an airglow model
whose only contact with GFZ is one hop away inside a dependency would be a surprise in that result
list. The dependency itself is surfaced to the reader in Field 29, so anyone who wants to know where
the indices come from can follow it from this record. Two further points make recording it worse than
omitting it. Nothing in this repository names GFZ, so the claim would be second-hand and would go
stale silently if `geomagindices` changed source — its own README says "We should add readers for the
new post-SWPC data sources". And because GLOW consumes F10.7 as well as Ap, and the live `DataInput`
vocabulary on the target has **no row for NRCan** or for any solar-flux service, `GFZ` alone would
describe only the Ap half of what the software fetches, which is a worse answer than silence.

**Alternatives considered and rejected.** `GFZ` together with `Other` — `Other` standing in for the
NRCan F10.7 source — was the only combination that would have been factually complete; it is rejected
because it still asserts a first-party relationship the repository does not have, and because `Other`
carries no information a reader can act on. `FTP/FTPS Directories` and `HTTP/HTTPS Directories`
describe the dependency's transport rather than this software's data sources.
`Observatory/Mission-specific` is wrong outright: GLOW is not tied to any observatory or mission (see
Fields 31 and 32). `CDAWeb`, `HAPI`, `OMNIWeb`, `Madrigal` and `WDC` are rejected because the
repository contacts none of them.

### 18. Input File Formats (RECOMMENDED)
**Values:** ascii, netCDF3/4, Other

All three confirmed against the live `FileFormat` vocabulary on the target. Unchanged.

- **ascii** — the standalone driver reads a text input file: `docs/Quickstart.txt` documents
  `glow.exe < in.basic.day > test.basic.day`, and `archive/in.basic.day` and `archive/in.basic.aur`
  are the shipped inputs. The MPI driver reads a Fortran namelist (`fortran/in.namelist.tgcm`,
  `fortran/in.namelist.msis`), also plain text. The bundled IRI-90 coefficient files
  (`src/ncarglow/data/iri90/ccir*.asc`, `ursi*.asc`) and the photoionization/solar-flux data files are
  text.
- **netCDF3/4** — `src/ncarglow/fortran/readtgcm.f90` "Reads TIE-GCM or TIME-GCM history file,
  obtaining needed inputs for GLOW."; `docs/Glow.txt` says of the parallel driver "It uses netCDF files
  for input and output, and a namelist input file to specify input options."
- **Other** — the `ebins` path writes a raw `float32` binary scratch file that the Fortran executable
  reads back: `base.py` does `Ebins.tofile(f)` then `Phitop.tofile(f)` into a `tempfile.mkstemp(".dat")`
  handle, and `+ncarglow/glowenergy.m` writes the same layout with `fwrite(fid, Ebins, 'float32')`.
  That is an ad-hoc binary format with no vocabulary row.

### 19. Output File Formats (RECOMMENDED)
**Values:** ascii, netCDF3/4, Other

Unchanged.

- **ascii** — `glowpython.f90` writes the entire result to standard output as fixed-format text, which
  `base.py:glowparse` and `+ncarglow/private/glowparse.m` parse; `archive/out.basic.day` and
  `archive/out.basic.aur` are shipped example text outputs; `rout.f90` writes a fixed-format tabular
  file "in order to transfer them to Randy Gladstone's REDISTER radiative transfer program."
- **netCDF3/4** — `output.f90` "Handles output from the GLOW model to netCDF files." A worked example
  output is published at
  `http://download.hao.ucar.edu/pub/stans/glow/output/out.decminmsis.001.nc` (reachable, ~43 MB of
  `application/x-netcdf`).
- **Other** — **the weakest of the six format values, and the reason is recorded honestly.** Its
  support is the README's statement that the Matlab interface works by "passing data to / from Glow
  over scratch disk binary files." At the pin, the binary scratch file is used only in the *input*
  direction (see Field 18); results come back over standard output as text. The README's "to / from"
  is therefore broader than the code. The value is retained rather than proposed for removal because
  it is a stored value backed by the project's own documentation, but a future refresh that wanted to
  tighten Field 19 has the evidence here to do it.

### 20. Operating System (RECOMMENDED)
**Values:** Linux, Mac, Operating System Independent, Windows

All four confirmed against the live `OperatingSystem` vocabulary on the target. Note that
`OS Independent` is not a row on the target — the full phrase is required, and the abbreviated form
would be rejected.

**`Windows`, which the record did not previously carry.** The value set was internally inconsistent without it: it asserted
`Operating System Independent` (which `pyproject.toml` also asserts, via the classifier
`"Operating System :: OS Independent"`) while omitting Windows.
Either Windows belongs or `Operating System Independent` does not.

**The evidence resolves it in favour of adding Windows, because the accommodations are deliberate and
in three independent places:**
- `src/ncarglow/build.py` branches on the platform to pick a Windows-appropriate generator:
  `if os.name == "nt" and not os.environ.get("CMAKE_GENERATOR"):` followed by
  `wopts = ["-G", "MinGW Makefiles"]`.
- `src/ncarglow/base.py` explains a structural choice in the `ebins` path as a Windows workaround:
  "cannot use tempfile.NamedTemporaryFile() context manager because Windows needs the file to be
  closed," and it catches `PermissionError` when unlinking the scratch file for the same reason.
- `+ncarglow/glowenergy.m` carries a block commented `%% workaround Windows` explaining
  "8192 cmd line limit AND lack of stdin", and warns at runtime with
  `warning('Windows has an 8k character limit on the command line')` under an `ispc` guard.

That is a maintainer restructuring code so it works on Windows, not an incidental mention. Decided
from the user's side: someone filtering `OS=Windows` and finding GLOW would find a package that
handles their platform's quirks explicitly and needs only a Fortran compiler, which the README says is
required everywhere — "A Fortran compiler is required in any case."

**The honest counterweight, recorded so it is not lost.** CI at the pin tests only two platforms:
`.github/workflows/ci.yml` sets `os: [ubuntu-latest, macos-latest]` with `FC: gfortran-12`. There is
no Windows job, so Windows support is asserted by the code and untested by the project. `Linux` and
`Mac` remain better-evidenced than `Windows`.

**Alternative considered:** dropping `Operating System Independent` instead of adding `Windows`. Not
chosen, because that value comes directly from the maintainer's own `pyproject.toml` classifier and
removing a maintainer-stated claim on our own inference would be worse than adding the platform the
code demonstrably handles.

### 21. CPU Architecture (RECOMMENDED)
**Values:** CPU Independent, x86-64, HPC or HEC

All three confirmed against the live `CpuArchitecture` vocabulary on the target.

**`HPC or HEC`, which the record did not previously carry.** GLOW ships a genuine MPI parallel program aimed at cluster and
supercomputer use:
- `src/ncarglow/fortran/glowdriver.f90` is headed "Stan Solomon, 3/2016, MPI parallel version" and
  "Requires MPI and netCDF libraries"; it contains `use mpi`, `mpi_init`, `mpi_comm_rank`,
  `mpi_comm_size`, `mpi_bcast` and gather buffers.
- `src/ncarglow/meson.build` defines an optional `mpi_glow.bin` target linking MPI and netCDF, gated
  by `get_option('mpiglow').enabled()`; the option itself is declared in
  `src/ncarglow/meson_options.txt` as
  `option('mpiglow', type : 'feature', value: 'disabled', description : 'MPI Glow')`.
- `archive/runglow.job` is a batch script whose header comment reads "Number of processors for 64-bit
  Linux MPI run" and which invokes `mpirun -l -np $nproc $model < $input > $output`.
- `docs/Glow.txt` discusses processor counts and sizing directly against a specific machine: "Note
  that on the new NCAR Cheyenne supercomputer, one node has 36 cores!"

Decided from the user's side: a user filtering for software that can run on an HPC system would be correctly
served. Note that the corresponding *functionality* value was deliberately **not** added — see the
rejection of `Servers and Environments: High Performance Computing` in Field 4; a science application
that scales on a cluster is not HPC infrastructure.

**`CPU Independent` and `x86-64` retained.** `x86-64` is the tested and documented target —
`docs/Glow.txt` says performance "has only been tested using the Intel ifort compiler with -O3
optimization running under CentOS Linux on 64-bit machines", and `runglow.job` says "64-bit Linux".
`CPU Independent` reflects that the code is portable Fortran with no architecture-specific
instructions.

**`Apple Silicon arm64` considered and rejected — the absence of evidence is the finding.** CI at the
pin runs `macos-latest`, but with `FC: gfortran-12` and no architecture named. Nothing in the
repository, the CI configuration or the documentation names arm64, Apple Silicon or aarch64. Recorded
so a future refresh does not infer arm64 support from the mere presence of a macOS CI job.

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found — an evidenced empty, not an unexamined gap.

**The vocabulary has seven rows on the target, and this is the durable reason the field is empty:**

> Coronal Heating · Coronal Mass Ejections · Geomagnetic Storms · Solar Corona · Solar Flares ·
> Solar Wind · X-ray emission

The phenomena GLOW actually models — aurora and airglow — have no row. That is the whole finding: the
field is empty because the controlled vocabulary does not contain the software's subject, not because
the software has no phenomena.

**`Geomagnetic Storms` considered and rejected.** GLOW consumes Ap and Kp as activity-level inputs
(`glowpython.f90` takes `ap` on the command line; `snoem.f90` takes `kp`), and storm-time runs are
possible. But consuming an activity index is not modelling storms: nothing in the repository studies
storm dynamics, no storm-time capability is documented, and the model has no magnetospheric driver. A
user filtering for storm software would be misled.

**`X-ray emission` considered and rejected.** `docs/Releasenotes.txt` lists "X-rays shortward of 18 A
need to be re-examined and updated." as a known issue, and one of the developer-cited papers concerns
solar soft X-rays. But solar X-rays are an *input* to GLOW's photoionization calculation; GLOW does not
model X-ray emission.

**Where the real phenomena went.** `aurora` and `airglow` are recorded in Field 16, the only open
vocabulary, which is exactly where the field guidance directs a phenomenon with no row.

### 23. Development Status (RECOMMENDED)
**Value:** Inactive

Confirmed against the live `RepoStatus` vocabulary on the target (8 rows, each carrying the
repostatus.org definition).

**The previously recorded value was `Active`, and its justification was falsified.** An earlier
revision of this file recorded `Active` on the basis of "SoMEF (date_updated: 2025-10-23)". That
figure is GitHub's `updated_at` timestamp, which advances on stars, forks, description edits and
watch events — it is not a commit date and is not evidence of development. The clearest proof is that
the same field has since moved again, to 2026-05-23, while the repository's `pushed_at` timestamp has
stayed at 2024-01-14T21:14:01Z, matching the last branch commit. **Never derive Field 23 from
`updated_at`.** The record carried no development status at all before this value was derived.

**What the repository actually shows.** `origin/main` last moved on 2023-09-20, which is the pinned
revision. The most recent commit on any upstream branch is `origin/vcb` at
`e1f3adae92aed555680ead4511687e5dd95a85a5`, dated 2024-01-14 with the message "inwork";
`origin/reference` sits at the 2017 upstream release. The repository is **not archived** and its
issue tracker is enabled. The newest upstream GLOW release vendored here is v0.981 —
`docs/Releasenotes.txt` is headed "GLOW version 0.981 release notes, Stan Solomon, 6/2017" and lists
nothing later — while `docs/Todolist.txt` still describes a next release "anticipated for 2018".

**Deriving the value from the definitions.** The vocabulary's definitions read:
- **Active** — "The project has reached a stable, usable state and is being actively developed."
  Rejected: `main` has not moved in nearly three years and the one later branch commit is itself over
  two and a half years old.
- **Inactive** — "The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows." Selected: v1.4.0 is a stable,
  released, DOI-minted state; development has stopped; the repository remains open with issues
  enabled and the maintainer is contactable.
- **Unsupported** — "The project has reached a stable, usable state but the author(s) have ceased all
  work on it. A new maintainer may be desired." Rejected. Settled campaign policy is that
  `Unsupported` is the right answer for an **archived** repository — an affirmative act by which the
  author declares the work over. This repository is not archived, and a branch commit in January 2024
  is evidence against "ceased all work".
- **Moved** — rejected; a search of the README and `docs/` for successor-location language finds
  none, and the GitHub repository is not marked as moved.

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/NCAR-GLOW

**Source:** the repository README, which carries the install instructions
(`git clone …` then `pip install -e ncar-glow`), the Python and Matlab usage examples, and the
Fortran/CMake/Meson and MPI build instructions. Unchanged.

**Why the same URL as Field 3, which the form explicitly permits.** There is no separate documentation
site — no ReadTheDocs configuration, no `docs/` HTML build, no GitHub Pages. The
`docs/` directory contains the upstream model's plain-text documentation (`Glow.txt`, `Quickstart.txt`,
`Releasenotes.txt`, `Todolist.txt`, `Glowlicense.txt`), which is reached by browsing the repository.
The form's guidance for this case is "If this is the same as the access URL, then enter that link
here."

### 25. Funder (OPTIONAL)

**Organization:** National Aeronautics and Space Administration
**Funder Identifier:** https://ror.org/027ka1x80

**Why NASA is recorded.** The scientific software a user obtains through this entry is GLOW, and
GLOW's development was funded by NASA. The entry's own reference publication documents it: the 2017
paper's Acknowledgments state that the research was supported by four NASA grants to the National
Center for Atmospheric Research. A reader asking which software NASA's heliophysics funding produced
should find this model, and the funding is attested in the primary source this record already points
at rather than inferred.

**The evidence.** The 2017 paper's Acknowledgments read as follows. The article is Free Access, and
this paragraph has been verified word for word against the publisher's rendered article page at
`https://agupubs.onlinelibrary.wiley.com/doi/10.1002/2017JA024314` — including the source's own
missing "of" in "development the GLOW model". That page refuses plain HTTP clients and can only be
read in a browser, which is worth knowing before anyone concludes the quotation is unverifiable:

> "The author thanks Andrew F. Nagy for his pioneering research in the field, including original
> development of the two-stream algorithm. He also thanks the many other people, some referenced in
> the text, who have contributed in various ways to the development the GLOW model. Model codes and
> results can be obtained at the HAO/NCAR website https://www2.hao.ucar.edu and are archived on the
> NCAR High Performance Storage System. Data from the TIMED/GUVI instrument were provided by R.R.
> Meier and are publicly available through the TIMED database. This research was supported by NASA
> grants NNX13AE15G, NNX14AH54G, NNX08AQ31G, and NAG5-5335 to the National Center for Atmospheric
> Research. NCAR is sponsored by the National Science Foundation."

That statement is independently corroborated by Crossref's funder block for the same DOI, which lists
the National Aeronautics and Space Administration against awards NNX13AE15G, NNX14AH54G, NNX08AQ31G
and NAG5-5335, and the National Science Foundation against an award recorded only as "NCAR".

**The National Science Foundation is deliberately not recorded, and must not be added later.** The
tiering is the whole point, and a flattened funder list destroys it. NASA funded the *research* that
produced the GLOW model, through four grants. NSF's role is different in kind: it sponsors NCAR as an
institution, and the Acknowledgments say exactly that and nothing more. Recording NSF here would
misrepresent institutional sponsorship of a laboratory as a project grant to this work.

**The scope objection, weighed and answered.** This HSSI entry is `space-physics/NCAR-GLOW` — Michael
Hirsch's Python and Matlab packaging *of* Solomon's model, published under its own Zenodo DOI — and
the packaging's own metadata is silent on funding: DataCite reports `fundingReferences: []` for the
concept DOI, Zenodo record 8309940 carries no grant information, and no file in the repository at the
pin mentions a grant, an award or a sponsor. The NASA grants funded Solomon's model development at
NCAR through 2017; they did not fund the wrapper. The reason NASA is nevertheless recorded is that the
field asks who supported the software a user gets from this record, and what they get is GLOW. The
wrapper is a thin build-and-call layer by its own account: the release description carried in Field 12
says this implementation "remains as an almost zero modification to the original source code".
Attributing the model's funding to the model is therefore the accurate reading, and recording nothing
would have left a genuinely NASA-funded model looking unfunded.

### 26. Award Title (OPTIONAL)

**Value:** None — and the reason is a mechanical limitation, not an absence of funding. Field 25
records NASA precisely because the funding is documented.

**The award numbers are known; the award titles are not.** The 2017 Acknowledgments and Crossref both
give four NASA grant numbers — **NNX13AE15G, NNX14AH54G, NNX08AQ31G, NAG5-5335** — and no titles.
Crossref's `award-info` entries carry `award-number` only.

**Durable limitation, recorded so a later refresh does not rediscover it the hard way: an award with
no title is not writable.** HSSI's award structure requires a title, so a grant number alone cannot be
recorded, and these four therefore cannot be entered in the form they are documented in. Closing this
field would require resolving each number to its official project title — through NASA's award records
or NSPIRES, for instance — which none of the sources consulted here provides. A second constraint
applies once titles exist: the stored award name is capped at 128 characters, so a long official
project title needs checking against that limit before use.

**Rejected, and recorded so it is not reintroduced from Crossref:** the NSF entry in Crossref's funder
block, whose award number is the literal string "NCAR". That is institutional sponsorship of the
laboratory rather than a grant that funded this software, and the value recorded there as an award
number is not one. It matches the reasoning that keeps NSF out of Field 25.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Values:**
- https://doi.org/10.1029/JA075i031p06260
- https://doi.org/10.1029/JA093iA09p09867
- https://doi.org/10.1029/JA094iA06p06817
- https://doi.org/10.1029/2000JA002011
- https://doi.org/10.1029/2001GL012866
- https://doi.org/10.1029/2001JA000258

**Why these six, and why the developer's own list is the right basis.** Field 27 asks for "Publications that describe, cite, or use the software that the software developer
prioritizes but are different from the reference publication" — the emphasis being on whose priorities
decide.
GLOW's developer maintains exactly such a list: `docs/Glow.txt` ends with a section headed
"References/Citations:", and the same list is served live and current at
`https://download.hao.ucar.edu/pub/stans/glow/refs/glowrefs.txt`. It contains seven entries. The
seventh is the 2017 paper, which is recorded in Field 14 as the reference publication and is therefore
excluded here to avoid duplication. The remaining six are listed above. Each DOI was resolved and
verified against Crossref rather than constructed.

| DOI | Citation as verified at Crossref |
|---|---|
| 10.1029/JA075i031p06260 | Nagy, A. F., and P. M. Banks (1970), Photoelectron fluxes in the ionosphere, *J. Geophys. Res.*, **75**, 6260–6270 |
| 10.1029/JA093iA09p09867 | Solomon, S. C., P. B. Hays and V. J. Abreu (1988), The auroral 6300 Å emission: Observations and modeling, *J. Geophys. Res.*, **93**, 9867–9882 |
| 10.1029/JA094iA06p06817 | Solomon, S. C., and V. J. Abreu (1989), The 630 nm dayglow, *J. Geophys. Res.*, **94**, 6817–6824 |
| 10.1029/2000JA002011 | Solomon, S. C. (2001), Auroral particle transport using Monte Carlo and hybrid methods, *J. Geophys. Res.*, **106**, 107–116 |
| 10.1029/2001GL012866 | Solomon, S. C., S. M. Bailey and T. N. Woods (2001), Effect of solar soft X-rays on the lower ionosphere, *Geophys. Res. Lett.*, **28**, 2149–2152 |
| 10.1029/2001JA000258 | Bailey, S. M., C. A. Barth and S. C. Solomon (2002), A model of nitric oxide in the lower thermosphere, *J. Geophys. Res.*, **107**, 1205 |

**Two discrepancies between the developer's list and the published record, noted so a future refresh
does not treat them as errors in this file.** `glowrefs.txt` gives the 2001 GRL title as "Effect of
solar soft X-rays on the lower atmosphere"; the published title reads *Effect of solar soft X-rays on the
lower ionosphere*. And `glowrefs.txt` renders the 2017 DOI as "doi:1002/2017JA024314", missing the
`10.` prefix — see Field 14.

**Applying the bar rather than taking the list wholesale.** Nagy and Banks (1970) is the only entry
that does not describe, cite or use GLOW — it predates the model and describes the two-stream
algorithm GLOW implements. It is included because it is on the developer's own prioritized citation
list, which is the criterion the field names, and because the license and the 2017 Acknowledgments
both single out that algorithm as foundational to the code. A reader of GLOW's HSSI page is better
informed for seeing it.

**Considered and rejected — the citations for GLOW's bundled third-party components.** `snoem.f90`
cites Marsh et al., `doi:10.1029/2003JA010199` (NOEM); `docs/Glow.txt` cites Picone et al. 2002 for
NRLMSISE-00, Bilitza for IRI-90 (as "Belitza, 1990" — the source's misspelling), and McGranaghan et
al. 2016 for the CONDUCT routine. **None of these appears on `glowrefs.txt`, and that is the whole
criterion.** Field 27 asks for the publications the developer prioritises, `glowrefs.txt` is the
developer's own prioritised list, and a paper's absence from it is a decision by the person the field
defers to. No further test is needed, and none should be imported.

In particular, this exclusion is **not** the same boundary Field 6 draws around authorship, and the
two must not be conflated. Whether someone contributed GLOW code and whether the developer prioritised
a publication are different questions that land differently for the same person. Ryan McGranaghan is
one of GLOW's own contributors, not the author of something GLOW merely bundles: `conduct.f90` is his,
it is compiled into the core library, and it runs once per altitude level on every call. Yet
McGranaghan et al. 2016 is not on `glowrefs.txt`, so it is not a Field 27 entry. Reaching for an
authorship boundary to justify that exclusion would put him on the wrong side of a line he is on the
right side of, and would leave the exclusion resting on a premise that does not hold.

**Previously recorded as "Not found".** An earlier revision of this file recorded no related
publications on the grounds that DataCite's `relatedIdentifiers` listed none. That was true of
DataCite — its related identifiers for this DOI are the Zenodo version chain and the GitHub tree URL —
but the developer's citation list was sitting in `docs/Glow.txt` in the repository the whole time.

### 28. Related Datasets (OPTIONAL)
**Value:** Not found

**Negative research, recorded so it is not repeated.** DataCite's `relatedIdentifiers` for the concept
DOI contain no dataset relations — only `IsSupplementTo` (the GitHub tree URL) and six `HasVersion`
entries pointing at the other Zenodo versions. Nothing in the repository at the pin references a
dataset DOI or an `hpde.io` landing page.

**Two near-misses, and why neither qualifies:**
- `docs/Quickstart.txt` links an example netCDF output at
  `http://download.hao.ucar.edu/pub/stans/glow/output/out.decminmsis.001.nc`. It is reachable
  (about 43 MB of `application/x-netcdf`), but it is a sample *output of* the software, not a dataset
  the software supports functionality for. Field 28 asks for the latter.
- The 2017 paper compares model output with TIMED/GUVI limb scans. That is validation of the model in
  a paper, not a dataset this code reads. GLOW has no GUVI reader. See Fields 31 and 32.

### 29. Related Software (OPTIONAL)

**Values:**
- https://github.com/space-physics/geomagindices
- https://github.com/space-physics/iri90
- https://github.com/space-physics/msise00

**`geomagindices` — retained, and it is the clearest case in this field.** It is a domain-specific,
load-bearing dependency: `src/ncarglow/base.py` does `import geomagindices as gi` and every one of the
four names exported in `src/ncarglow/__init__.py` — `maxwellian`, `ebins`, `no_precipitation`,
`no_source` — calls `gi.get_indices([time - timedelta(days=1), time], 81)` before invoking the model.
Without it a GLOW run cannot be parameterised. `pyproject.toml` pins `geomagindices>=1.5.0`. It is a
heliophysics-specific package, not generic infrastructure, and it is itself an HSSI entry.

**`iri90`, which the record did not previously carry.** GLOW *bundles* IRI-90: `src/ncarglow/fortran/iri90.f` is headed
"Special-purpose version of IRI90 for use with the GLOW model." and "This is not the original IRI90.",
and its coefficient files ship in `src/ncarglow/data/iri90/`. `mzgrid.f90` calls `iri90` unconditionally, and `docs/Glow.txt` names IRI-90 as the a-priori ionosphere. HSSI holds a record
for IRI-90 whose repository is `https://github.com/space-physics/iri90`, so this both distinguishes
GLOW (it tells a reader which ionosphere model is inside) and links two catalogue entries. Field 29's
own definition — "two software that model the upper atmosphere of Earth but using different
assumptions" and "Important software dependencies" — fits exactly.

**`msise00`, which the record did not previously carry.** The same reasoning applies: `src/ncarglow/fortran/nrlmsise00.f` is the
bundled NRLMSISE-00, `mzgrid.f90` calls `gtd7` for the neutral atmosphere unconditionally,
and `docs/Glow.txt` names NRLMSISE-00 as the default neutral model. HSSI holds a record for MSISE-00
whose repository is `https://github.com/space-physics/msise00`.

**`numpy` — removed. This is the rule being applied, not a curator's preference.** The field
definition names numpy in the list of packages that are **never** listed, "no exceptions", and states
explicitly that the exclusion applies to Field 29 as well as Field 30: "The generic scientific-Python
stack is excluded here too — numpy, scipy, pandas, matplotlib … are not related software, because
listing them says nothing that isn't equally true of most of the ecosystem." Being a `pyproject.toml`
dependency is not a qualification. This is not a debatable judgement that could be reversed on taste;
reversing it would require changing the field definition itself.

**`xarray` — moved from Field 29 to Field 30.** See Field 30 for the qualifying evidence. It was not
simply dropped.

**Rejected candidates, with reasons — recorded so none of them is re-proposed:**

- **`pyglow` (`https://github.com/timduly4/pyglow`)** — **different software; the shared string
  "glow" is not a reason to link them, and the reasoning here is on function only.** pyglow is
  Timothy M. Duly's package, described in the PyHC registry as "Upper atmosphere models and
  geophysical indices." and in its HSSI record as a Python module that wraps several upper-atmosphere
  climatological models written in Fortran, such as HWM, IGRF and IRI. That is an *aggregator of
  empirical climatologies*. GLOW is an airglow and aurora photochemistry and electron-transport model:
  it computes emission rates, excited-species densities and conductivities that pyglow does not
  attempt. The only genuine overlap is that GLOW bundles IRI-90 and NRLMSISE-00 for its own inputs,
  and that overlap is already recorded above, precisely, by the two entries that name those models.
  Adding pyglow would tell a reader nothing true about GLOW and risks exactly the conflation this note
  exists to prevent.
- **`matplotlib`** — Tier A generic infrastructure. It is imported by `plots.py`, but it would be
  equally at home in a web app or a finance model.
- **`pandas`** — Tier A. It appears only as the type annotation of the geomagnetic-index frame passed
  through `base.py:glowread`.
- **`netCDF-Fortran` / `netcdf`** — a file-I/O library dependency of the MPI driver. Generic
  infrastructure by the field's own test, and the capability is already recorded in Fields 18 and 19.
- **`Jupyter`** — Tier B. The repository contains one example notebook, `Notebooks/Maxwellian.ipynb`.
  A single example notebook is not a demonstrated exchange; nothing in the package produces or
  consumes notebook artifacts.
- **NOEM / SNOE nitric-oxide model** and the **Nagy–Banks two-stream algorithm** — **tested, and
  neither is software.** NOEM exists here only as `src/ncarglow/fortran/snoem.f90`, a Fortran
  subroutine Solomon adapted from IDL and F90 code supplied by Dan Marsh; it has no independent
  distribution, no repository and no HSSI record, and is cited as a *paper*
  (`doi:10.1029/2003JA010199`). The two-stream method is an algorithm from a 1970 paper, implemented
  here as `etrans.f90` and `exsect.f`, which `exsect.f` records as "Adapted from Banks & Nagy 2-stream
  code by Stan Solomon, 1988"; there is no package to link to. Both are cited science, and the
  correct destination for both is a citation, not this field. This is deliberately consistent with
  the acceptance of IRI-90 and MSISE-00, which *are* separately distributed packages with their own
  HSSI records and their own repositories — the distinguishing test is whether an independently
  distributed piece of software exists, not whether the science is important.

### 30. Interoperable Software (OPTIONAL)

**Values:**
- https://github.com/pydata/xarray
- https://github.com/NCAR/tiegcm
- https://www.mathworks.com/products/matlab.html

**`xarray` — what a user gains.** Someone whose analysis already speaks xarray can run GLOW and use
the result immediately: the model hands back a labelled `xarray.Dataset` on its documented public
interface, so there is no output file to locate, no fixed-format Fortran table to parse, and no
conversion step to write. Slicing an emission profile by wavelength, or aligning a GLOW run against
other xarray data on the shared `alt_km` axis, works out of the box. That is the reason this entry is
here; it is a capability a reader of the catalogue can act on, not a rule being satisfied.

The evidence that this is a real, documented interface rather than an implementation detail:
- Every function exported by `src/ncarglow/__init__.py` is annotated `-> xarray.Dataset` in
  `base.py`, as are the helpers `glowread` and `glowparse`.
- The README documents it to users: it states that `iono` is an `xarray.Dataset` and links the xarray
  documentation for that class.
- The returned object is a genuine shared data model: `glowparse` merges four Datasets and a
  DataArray with `alt_km`, `wavelength`, `state` and `energy` coordinates and attaches run metadata as
  attributes, so a user's downstream xarray tooling operates on GLOW output directly.
- The tests exercise it as the interface: `test_basic.py` indexes results as
  `iono["ver"].loc[:, "5577"][i]`.

**Why it sits here and not in Field 29, where it used to be.** Field 29 is where a reader looks to
learn what else does this kind of science, or what this software is built on top of in its own domain.
xarray is neither — telling a heliophysicist that GLOW is "related to" xarray answers no question they
have. Field 30 is where a reader looks to learn what they can plug this into, and there the same fact
is directly useful.

**`tiegcm` — what a user gains.** A modeller who has already run TIE-GCM or TIME-GCM can compute
global airglow from that run without writing any coupling code: GLOW reads the GCM's own secondary
history files directly, on the GCM's own grid, and a ready-made configuration for doing so ships in
the repository. For someone arriving from the TIEGCM side of the catalogue, that is the single most
useful thing to know about GLOW. Concretely, GLOW imports TIE-GCM's output as its input:
- `src/ncarglow/fortran/readtgcm.f90` is a dedicated module — "Reads TIE-GCM or TIME-GCM history file,
  obtaining needed inputs for GLOW." — with entry points `read_tgcm_coords`, `find_mtimes` and
  `read_tgcm`.
- `glowdriver.f90`, the MPI driver, is built around it: "Uses TIE-GCM history files or MSIS/IRI for
  input."
- `docs/Glow.txt` documents the exact interchange contract — which fields a TIE-GCM secondary history
  must contain ("Zg, Te, Ti, Te, Ne, O2, O1, N2, NO, N4S, N2D" plus optional auroral parameters) —
  and describes the driver as "a parallel processing program set up to use output from general
  circulation models such as the NCAR TIE-GCM and TIME-GCM to specify the neutral densities, electron
  density, and temperatures, and then calculate airglow emissions globally on the GCM grid."
- A ready-to-use configuration ships as `fortran/in.namelist.tgcm`, whose header says "This version of
  the file is set up for TIE-GCM input."
- The 2017 paper's abstract states the model "can be run using inputs from empirical models of the
  neutral atmosphere and ionosphere or from numerical general circulation models" of the coupled
  ionosphere-thermosphere system. (The trailing words are paraphrased rather than quoted because the
  publisher's page and Crossref's deposited abstract render that compound differently.)

One package's output being imported by the other, over a documented field contract, with a shipped
configuration for it, is as concrete as interoperability gets — and it is a two-way signal in the
catalogue, since a TIEGCM user finding GLOW is as well served as a GLOW user finding TIEGCM. HSSI's
TIEGCM v3.0 record has repository `https://github.com/NCAR/tiegcm`, the URL used here. This belongs
here rather than in Field 29 because TIE-GCM is not a substitute for GLOW or a component of it: the
two do different jobs and hand work to each other.

**`matlab` — what a user gains.** A researcher who works in MATLAB and does not want to move to
Python can still run this model: GLOW ships a maintained MATLAB interface that drives the same
executable and returns the results as MATLAB structures. Most model software in this catalogue offers
no such route, so for a MATLAB user this is the deciding fact about GLOW rather than a footnote. The
interface is complete, not a stub: the
`+ncarglow/` MATLAB package provides `glow.m`, `glowenergy.m`, `loggrid.m`, `plotglow.m` and
`TestGlow.m` over seven private helpers, which invoke the GLOW executable, parse its output into
MATLAB structures (`+ncarglow/private/glowparse.m`) and plot it; `src/ncarglow/meson.build` even registers
MATLAB and Octave test targets. The README documents the interface. `https://www.mathworks.com/products/matlab.html`
is already an established related-item URL in this catalogue, so this does not coin a new form.

**The counterargument, recorded because it is not weak.** MATLAB is a commercial platform rather than
a peer science package; it would be equally at home in a finance model; and Field 13 already lists
`MATLAB` as one of the languages, so a careful reader might infer the interface from that alone. The
answer is that Field 13 says the software *contains* MATLAB code, which is not the same claim as
*this can be driven from MATLAB* — a reader has to open the repository to tell those apart, and this
entry saves them that. Of the three entries in this field it is the one resting on the least
domain-specific ground, and a later refresh that tightened Field 30 would reach it first.

**Rejected — blanket claims and Tier A packages.** No entry here rests on "part of the standard
scientific Python ecosystem" or on PyHC membership. `numpy`, `pandas` and `matplotlib` are excluded
(see Field 29). `geomagindices` stays in Field 29 rather than moving here: GLOW calls it as a
dependency to obtain parameters, which is not a two-way exchange between peer tools.

**Previously recorded as "Not found"** on the reasoning that "no explicit interoperability with other
heliophysics packages was documented." The TIE-GCM coupling was documented in `docs/Glow.txt` and
implemented in `readtgcm.f90` at that time; it was missed, not absent.

### 31. Related Instruments (OPTIONAL)
**Value:** Not found — an evidenced empty, deliberately not recorded as *not applicable*.

**GLOW is an instrument-agnostic model**, and the Field 31 relevance gate excludes instrument-agnostic
tools explicitly. No file in the repository at the pin reads, parses, calibrates or models any specific
instrument's data. There is no instrument reader, no instrument-specific format, no instrument response
function and no calibration path. The only external data the package retrieves are geomagnetic and
solar activity indices.

**The one candidate, and why it is rejected — this is the durable part of the note.** The 2017 paper
compares GLOW output with limb-scan observations by "the Global Ultraviolet Imager on the TIMED
satellite", and its Acknowledgments state that GUVI data "were provided by R.R. Meier". That is
**validation of the model in a publication**, not designed-to-support: no GUVI reader, no GUVI format,
no GUVI-specific code exists in this repository, and the comparison was done outside the distributed
software.

**This is a relevance judgement, not a resolution failure.** GUVI *does* resolve cleanly in HSSI's
controlled vocabulary, to `https://spase-metadata.org/SMWG/Instrument/TIMED/GUVI` — so the field is
empty because the association would be wrong, not because it could not be expressed. Recorded so a
future refresh does not "discover" the resolvable row and add it.

**Searcher's-eye test, which is decisive.** Someone on a GUVI instrument page clicking through to the software related to that instrument
is looking for tools that read or process GUVI data. GLOW cannot open a
GUVI file. They would be annoyed, not helped.

**SNOE / the SNOE ultraviolet spectrometer** was considered on the same basis and rejected for the
same reason: `snoem.f90` implements an empirical *model* derived from SNOE measurements
(`https://spase-metadata.org/SMWG/Instrument/SNOE/UVS` exists in the vocabulary), but GLOW reads no
SNOE data — it evaluates a fitted climatology, which is a different relationship entirely.

**Note on the field's mechanics, which constrains any future addition:** Fields 31 and 32 are
SPASE-only. A name without an `https://spase-metadata.org/` identifier either binds to an arbitrary
same-named row or creates a new identifier-less one, so no entry may ever be recorded here without its
SPASE identifier.

### 32. Related Observatories (OPTIONAL)
**Value:** Not found — an evidenced empty, established on this field's own evidence rather than
inherited from Field 31.

GLOW is a general model that is not purpose-built for, and does not read data products from, any
mission or observatory. The Field 32 relevance gate asks whether the software directly works with a
named mission's data or data products, implements its conventions, or is a mission-team tool. No file
in the repository at the pin does any of those things for any mission. The TIMED mission appears in this software's story only as the source of the
GUVI limb scans used to validate the 2017 paper, and — via the license's "rules of the road" clause,
which points at the NSF CEDAR project and the NASA TIMED mission for citation and co-authorship
practice — as a community norms reference. Neither is designed-to-support.

This is relevance and not resolvability: TIMED resolves in the vocabulary to
`https://spase-metadata.org/SMWG/Observatory/TIMED` and SNOE to
`https://spase-metadata.org/SMWG/Observatory/SNOE`, so the field is empty because the association
would be wrong, not because it could not be expressed. A scientist working with TIMED data would not
reach for GLOW, and would not expect it back from an observatory-scoped search.

**Not to be confused with GLOW's model coupling.** Reading TIE-GCM history files is a coupling to
another *model*, recorded in Field 30 — TIE-GCM is not an observatory and has no row here.

### 33. Logo (OPTIONAL)
**Value:** Not found — a documented absence backed by negative research, so that the dead registry URL
is not re-proposed.

**The PyHC registry does list a logo for GLOW, and it is gone.** The `projects_unevaluated.yml` entry
carries
`logo: https://www2.hao.ucar.edu/sites/default/files/resize/images/ICON-GOLD_2016/IonosphereHorizon-Banner-980x232.jpg`.
Fetching it returns HTTP 404 with `text/html` and a 268-byte body — not image bytes. The host
`https://www2.hao.ucar.edu/` itself answers 200, so this is a removed asset rather than a dead site,
and dropping the `/resize/` path segment (the usual Drupal image-derivative pattern) also 404s. The
asset cannot be recovered from that URL, and the registry's string must not be recorded verbatim.

**The repository contains no image of any kind at the pin.** Listing every tracked file at the pinned
revision and filtering for the usual image extensions (`.png`, `.jpg`, `.jpeg`, `.svg`, `.gif`,
`.webp`, `.ico`, `.pdf`, `.bmp`, `.tif`, `.tiff`) returns nothing. The README's only two images are a
Zenodo DOI badge and a GitHub Actions status badge, neither of which is a logo. There is therefore
nothing in the repository to pin to a commit.

**Other sources checked and empty:** the Zenodo record and the DataCite record carry no logo or image
metadata; there is no documentation site with a banner or `html_logo`; the model's own plain-text
documentation has no graphics.

A documented omission is the correct outcome here. Nothing should be invented, and no example plot
from the package should be substituted for a logo.
