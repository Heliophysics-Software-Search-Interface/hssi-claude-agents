# HSSI Metadata Extraction Results

**HSSI Software ID:** ac1149e1-6679-4466-a445-1f6dd0ecd883
**Repository:** https://github.com/rebeccaringuette/MagnetosphericSWCX/tree/MSWCX
**Source Revision:** adf9ff435acb9fc36dc21e16d7bf538bd97df5ef (tag `MSWCX`)
**Extraction Date:** 2026-08-06
**Validation Date:** 2026-08-07
**Validation Status:** PASS

---

## Scope note — read this before the evidence

This repository is a **publication-analysis archive**, not a reusable library. It has no package
metadata (no `setup.py`, `pyproject.toml`, `codemeta.json`, `.zenodo.json`), no installable module,
no tests, and no CI configuration. Absent a build system, several fields that would normally be read
off packaging metadata (operating system, CPU architecture, dependency lists) have to be derived from
the code itself, and the evidence notes below say which artifact each value came from.

Two ancillary facts change how the evidence should be read:

- The extraction is pinned to the `MSWCX` tag, which is the released version. The default branch
  `main` (HEAD `9eab63929ffc7f7b49944f7ac01687ed513089ad`, 2024-08-28) differs from this tag by
  exactly two things: it adds a Zenodo-exported `Citation.cff`, and it changes one README citation
  DOI (`zenodo.8021786` → `zenodo.8252998`). No analysis code changed after the tag. Where
  `Citation.cff` is cited below, it is being read from `main` via `git show main:Citation.cff`.
- Fourteen fields held no value on HSSI before this record was reconciled against the repository:
  development status, license, related instruments, related observatories, software functionality,
  CPU architecture, related publications, related datasets, operating system, related software,
  interoperable software, funder, award and related phenomena. Their values below therefore rest on
  repository and publication evidence rather than on anything a prior submitter asserted. Two of the
  fourteen — related instruments and related observatories — stay empty, for the vocabulary reason
  recorded under Fields 31 and 32.

**How the field notes read.** Each field states its value, the evidence behind it, and the
alternatives that were weighed and set aside. Where HSSI previously held a different value, that
value is recorded alongside the reason it was wrong, so a later pass does not restore it.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*Not stored on the HSSI record and not discoverable from the repository. The record predates this
dossier, so no submitter identity is asserted here.*

---

### 2. Persistent Identifier (RECOMMENDED)

**Value:** `https://doi.org/10.5281/zenodo.8021785`

This is the Zenodo **concept** DOI, which is what Field 2 asks for ("the concept DOI for all
versions"). The Zenodo API reports `conceptdoi = 10.5281/zenodo.8021785` on all three version
records under this concept, so the identity is unambiguous.

The concept currently has three version records:

| Record | DOI | Zenodo `version` | `publication_date` | Zenodo `license` | Record created |
|---|---|---|---|---|---|
| 8021786 | 10.5281/zenodo.8021786 | `SolarWindChargeExchange` | 2023-06-09 | other-open | 2023-06-09 |
| 8252998 | 10.5281/zenodo.8252998 | `MSWCX` | 2023-08-16 | other-open | 2023-08-16 |
| 8253002 | 10.5281/zenodo.8253002 | `MSWCX` | 2023-08-16 | apache2.0 | 2024-03-19 |

**Rejected alternatives.** Any of the three version DOIs would be wrong here — Field 2 wants the
version-independent identifier, and the version DOI belongs in Field 12 (Version PID). The
repository's own README citation line names `10.5281/zenodo.8021786`, a *version* DOI for the
superseded first release; that is a repo-internal inconsistency, not a candidate for this field.

---

### 3. Code Repository (MANDATORY)

**Value:** `https://github.com/rebeccaringuette/MagnetosphericSWCX/tree/MSWCX`

`git ls-remote` shows `MSWCX` is a **tag** (`adf9ff43…`), not a branch; there is no branch by that
name. The tag ref still resolves on GitHub, so the URL is live, and it is the URL the author herself
recorded in the software metadata she published: Zenodo's `metadata.custom["code:codeRepository"]`,
Zenodo's `isSupplementTo` related identifier, and `Citation.cff`'s `repository-code` (the last
derived from Zenodo, so corroborating rather than independent).

**Considered and not selected:** the repository root `https://github.com/rebeccaringuette/MagnetosphericSWCX`.
Field 3's instruction ("navigate to the root page of your repository") favors it, and it is more
robust to a future tag deletion. It was not selected because (a) the recorded URL resolves today,
(b) it is the value the author's own software metadata uses, and (c) for a publication-code archive
the tag-pinned tree is arguably the more precise pointer — it names the state of the code that
produced the published results. A future agent should not treat the `/tree/MSWCX` suffix as drift.

---

### 4. Software Functionality (MANDATORY)

**Value (14 entries):**

- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Calibration
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Energy Spectra
- Data Processing and Analysis: Processing
- Data Visualization
- Data Visualization: Line Plots
- Mission-related
- Mission-related: Analysis
- Models and Simulations
- Models and Simulations: Forward-Fitting
- Models and Simulations: Instrument Response
- Models and Simulations: Physics-Based

All fourteen are live values in the `FunctionCategory` vocabulary, and every subcategory listed has
its parent top-level category listed alongside it.

**Evidence for each entry:**

- **Data Processing and Analysis** — parent of five selected subcategories.
- **… : Energy Spectra** — the software's subject matter is soft X-ray *energy spectra*. Each script
  loads OGIP PHA spectra binned in energy channels, restricts the fit to 0.4–7 keV
  (`xs.AllData.ignore('0.0-0.4,7.-**')`), and reports line intensities at specific ion transition
  energies (0.44339, 0.56325, 0.65310, 0.67916, 0.80308, 0.90873, 1.10043 keV).
- **… : Data Reduction** — `PaperAnalysisCode/MSWCX_sum_May29.xcm` co-adds per-observation,
  per-detector spectra with `mathpha`; `MSWCX_rebin40_May29.xcm` rebins each summed spectrum with
  `grppha … 'group min 40'`. Binning and co-adding to raise signal-to-noise is data reduction in the
  taxonomy's sense.
- **… : Processing** — the repository implements an ordered pipeline (sum → rebin → fit → tabulate),
  with the flank scripts consuming the tail scripts' CSV output as an input
  (`DictReader(open(out_dir+'MSWCXTails_v18'+nH_type+'_mod2.csv','r'))` in
  `PaperAnalysisCode/FlankFit_v18.py`).
- **… : Calibration** — the scripts assign HaloSat calibration products to each spectrum:
  `multiresponse[0]` gets `halosat_diag_20190423.rmf` (diagonal response for the particle
  background) and `multiresponse[1]`/`[2]` get `halosat_avgenoise_20190423.rmf` with
  `hs_sdd_all20180701v001.arf`. The reference publication states the analysis "was performed with
  the original calibration files, specifically the arf and rmfs posted on the related GitHub
  repository," and those files are distributed here. Nuance worth recording: the software *applies*
  calibration products, it does not derive them.
- **… : Analysis** — derived scientific quantities beyond fitting: reduced chi-square, 90%
  confidence intervals via `xs.Fit.error`, `steppar` parameter scans, `calcFlux` band fluxes
  (referenced in the version histories of `TailFit_v18.py` and `TailFitHot_v18.py`), and the
  emission-measure columns described in `Results/README.md`.
- **Data Visualization** and **… : Line Plots** — each script issues `xs.Plot("data delchi")` with
  log axes, dynamically computed y-limits (`xs.Plot.addCommand('r y '+…)`), an observation label and
  a reduced-chi-square annotation, rendering both to the interactive `/xs` device and to a
  PostScript file (`xs.Plot.device = out_dir+model_note+'_'+obsname+'_delchi.ps/cps'`). Spectral
  count-rate-versus-energy plots with residual panels are line plots.
- **Mission-related** and **… : Analysis** — this is HaloSat-team science analysis software, not a
  mission-agnostic tool that happens to read HaloSat files. Supporting signals: HaloSat instrument
  response products are hardcoded by filename; HaloSat observation and detector conventions are
  parsed structurally (`HS00XX` target IDs, detector IDs 14/38/54); the author's own directory
  layout preserved in the scripts is `…/halosat_sourceanalysis/AnalysisCode/…` and
  `…/HaloSat_AnalysisSoft/CL_Code/`; and `PaperAnalysisCode/obs_att_cl_win.py` writes an
  OGIP-conformant FITS product carrying mission pipeline header keywords
  (`TELESCOP = HALOSAT`, `INSTRUME = SDD`, `OBSERVER = PHILIP KAARET`, `ORIGIN = UNIVERSITY OF
  IOWA`, `PROCVER = hsuf_20200226`, `CALDBVER = hs20200129`).
- **Models and Simulations** — parent of the three selected subcategories.
- **… : Forward-Fitting** — the core operation. XSPEC forward-folds a parameterized emission model
  through the instrument response and minimizes chi-square against the observed spectrum
  (`xs.Fit.statMethod='chi'`, `xs.Fit.method='leven 10 0.01'`, `xs.Fit.nIterations = 1000`,
  `xs.Fit.renorm()`, `xs.Fit.perform()`), with an outer loop that repeats the error runs whenever
  the fit statistic shifts by more than the configured tolerance.
- **… : Instrument Response** — response-matrix and effective-area handling is explicit and
  structural, not incidental: three separate `multiresponse` slots, a diagonal RMF used specifically
  so the particle background is modeled without effective-area folding, and an ARF applied only to
  the X-ray model components.
- **… : Physics-Based** — the model components are physical rather than ad hoc:
  `apec+tbabs*(apec+pow)` is an unabsorbed Local Hot Bubble thermal plasma, an absorbed Galactic
  halo thermal plasma and an absorbed cosmic X-ray background power law, with the absorbing column
  taken per target from a hydrogen-column FITS table (`LHB_nH_ecl3.fits`, selectable among the
  `nH_RT`, `nH_HI4pi`, `nH_SFDW` and `nH_PlanckZhu` columns). The SWCX Gaussians sit at fixed ion
  transition energies with secondary lines tied to primaries at computed branching ratios
  (`OVII_ratio = 0.126`, `OVIII_ratio = 0.4345` for a 50/50 H/He solar wind, `NeIX_ratio = 0.100`,
  `LowE_ratio = 0.946`).

**Considered and rejected, with reasons** (recorded so a later pass does not re-propose them):

- **Models and Simulations: MHD** — tempting because BATS-R-US is central to the science, but this
  software does not run an MHD model. `ExampleData/README.md` says the attitude file is "produced
  and subsequently used in the interpolation through the BATS-R-US model output," and the reference
  publication states the proton density and velocity "were extracted from BATS-R-US simulation
  runs" accessible on the CCMC website. The simulation and the interpolation both happen outside
  this repository.
- **Models and Simulations: Empirical** — the empirical ingredients (hydrogen column maps, CXB
  power-law index) are fixed inputs to a physics-based model, not an empirical model the software
  implements.
- **Models and Simulations: Data Guided** — the fit is driven by observed spectra, but that is what
  Forward-Fitting already describes; adding this would double-count the same behavior.
- **Data Processing and Analysis: Data Access and Retrieval** — searched for and not found. An
  import census across the 76 Python files yields `numpy`, `astropy.io.fits`, `xspec`, `csv`,
  `glob`, `itertools`, `os`, `sys`, `datetime` and one private local module (`ruf_2_Loopd`). In live
  code `os` appears as `os.path` and `os.makedirs`; two commented-out lines in `obs_att_cl_win.py`
  also call `os.remove` and `os.system('imcopy …')` to gzip an output file. None of that retrieves
  anything. A search for `requests`, `urllib`, `http`, `urlopen`, `wget` and `curl` returns no hits,
  and the data directories are local paths. Worth recording because the software is otherwise
  strongly tied to a mission archive.
- **Data Processing and Analysis: File Format Conversion** — the main scripts read FITS and write
  CSV, which matches the literal indicator, but the CSV is a results table rather than a converted
  copy of the input. Format conversion is not offered as a capability.
- **Data Processing and Analysis: Time Series Analysis** — `obs_att_cl_win.py` selects attitude
  samples inside cleaned good-time intervals. That is time filtering, not time series analysis.
- **Data Processing and Analysis: Image Processing / Spectrogram**, **Data Visualization:
  Spectrogram / 2D Graphics / 3D Graphics / Movies / Orbit Plots** — no code produces images,
  time-frequency arrays, 3D renderings, animations or trajectory plots. Spacecraft position and
  velocity are extracted to a FITS table in `obs_att_cl_win.py` but are not plotted.
- **Coordinate Transforms (any subcategory)** — `obs_att_cl_win.py` copies ECEF position/velocity
  and RA/Dec straight out of the attitude file into its output table. It reads coordinates; it does
  not convert between frames.
- **Mission-related: Science Data Processing / Calibration / Archive / Ingest** — these describe a
  mission's production ground system. This is a scientist's analysis code built on the mission's
  released products.
- **Models and Simulations: Observatory/Instrument Models** and **Mission-related: Instrument
  Response** — both are near-synonyms of the selected `Models and Simulations: Instrument Response`.
  One entry is enough; selecting all three would inflate the field without adding information.
- **Servers and Environments (any)** — no container, server, HPC or parallel-execution code.

---

### 5. Related Region (MANDATORY)

**Value (4 entries):**

- Earth Magnetosphere
- Interplanetary Space
- Earth Magnetosheath
- Earth Magnetotail

All four are live values in the `Region` vocabulary. The set is a union: neither value HSSI already
held was dropped.

**Evidence for Earth Magnetosheath and Earth Magnetotail.** The repository names both regions directly rather than by
inference. `Results/README.md`: "File names with 'Flank' were produced in the analysis of the
observations with lines of sight through the flanks of the Earth's **magnetosheath**. Similarly,
file names with 'Tail' were produced using data obtained from observations with lines of sight down
the tail of the magnetosheath." `PaperAnalysisCode/README.md`: "'Tail' scripts analyze the cleaned
spectra obtained from lines of sight down the **tail of the magnetosphere**." The reference
publication states that SWCX emission "is produced in planetary exospheres, Earth's magnetosheath,
and the heliosphere," and that the emission "is mostly limited to the subsolar and flank portions of
the magnetosheath and the polar cusps." Field 5's guidance prefers the most specific applicable
region, and these two are the specific regions the observations sample.

**Considered and not selected:**

- **Earth Outer Magnetosphere** — defensible, since the flank and tail lines of sight sample the
  outer magnetosphere. Not selected because `Earth Magnetosheath` and `Earth Magnetotail` are the
  terms the repository itself uses and are more specific.
- **Solar Wind** — a row in the vocabulary, and SWCX is by definition solar-wind driven. Not
  selected because the retained `Interplanetary Space` already covers the heliospheric component,
  and `Solar Wind` is captured as a keyword (Field 16) and a phenomenon (Field 22). The evidence
  would support adding it, so a later pass that judges `Interplanetary Space` too coarse has
  grounds to.
- **Earth Atmosphere** — the reference publication analyzes possible atmospheric contamination of
  the signal, and magnetospheric SWCX involves exospheric neutral hydrogen. Not selected because the
  software treats the atmosphere as a background to rule out rather than a region it supports
  science functionality for, and the vocabulary has no exosphere row.
- **Heliosheath**, **Planetary Magnetospheres**, **Corona / Chromosphere / Photosphere / Solar
  Interior / Solar Environment** — no supporting evidence in the repository or the reference
  publication.

---

### 6. Authors (MANDATORY)

**Value — one author, three affiliations:**

- **Author:** Rebecca Ringuette
  - **Author Identifier:** `https://orcid.org/0000-0003-0875-2023`
  - **Affiliation 1:** Heliophysics Data and Modeling Consortium — `https://ror.org/04xbq1n92`
  - **Affiliation 2:** Heliophysics Digital Resource Library — `https://ror.org/00d1g0h88`
  - **Affiliation 3:** ADNET Systems, Inc. — `https://ror.org/05we1n045`

**Author identity.** Sole author, agreed across every source consulted: Zenodo/DataCite creators
(`Ringuette, Rebecca`, `nameType: Personal`, ORCID `0000-0003-0875-2023`), `Citation.cff`
(`family-names: Ringuette`, `given-names: Rebecca`, same ORCID), the git history (single committer),
and the live HSSI record. No organization author applies here.

**Affiliation reconciliation.** The three sources disagree, and the disagreement is informative
rather than a data error:

| Source | Affiliation string |
|---|---|
| Live HSSI record; current Zenodo record 8253002; DataCite | Heliophysics Data and Modeling Consortium |
| Repo `Citation.cff` (added to `main` 2024-08-28) | Heliophysics Digital Resource Library / ADNET Systems Inc |
| Reference publication (ApJ 955, 139) author footnote | ADNET Systems, Inc.; NASA Goddard Space Flight Center |

ROR resolution shows these are related, not contradictory. `https://ror.org/04xbq1n92` has the
ROR display name "Heliophysics Data and Modeling Consortium" (acronym HDMC), and its parents include
`Heliophysics Digital Resource Library` (`https://ror.org/00d1g0h88`) and `Heliophysics Science
Division`. So the stored affiliation is exact and correctly identified; the CFF simply names the
parent organization plus the author's employer.

The `Citation.cff` string is a **single free-text field naming two organizations** joined by a
slash. Field 6 allows multiple affiliation entries, so the correct reconciliation is to split it and
union it with the stored value rather than to overwrite anything. ADNET Systems is independently
corroborated by the reference publication's author footnote and by its acknowledgement ("A portion
of R.R.'s work was supported by ADNET Systems, Inc.").

**Names chosen.** Field 6 asks for the "complete name without acronyms." `ADNET Systems, Inc.` is
the spelling used by the reference publication; note that the ROR display name for
`https://ror.org/05we1n045` is the disambiguated form "Adnet Systems (United States)", so a future
agent comparing against ROR should not read the difference as an error.

**Considered and not selected: NASA Goddard Space Flight Center.** It appears in the reference
publication's author footnote but in none of the software metadata artifacts consulted (Zenodo,
DataCite, `Citation.cff`, the live HSSI record), and GSFC is the host center for HDRL/HDMC rather
than a separate affiliation the author asserted for this software. Recorded so a later pass can
weigh the same evidence rather than rediscover it; on this evidence the association is not
asserted.

**The label HSSI stores for ADNET differs from the name above, and that is accepted.** HSSI's
`Organization` row for `https://ror.org/05we1n045` carries the name `Adnet Systems (United States)`
— ROR's disambiguated display form — and it keeps that label. Organizations are matched on their
identifier, and a supplied name is written only when the stored one is blank, so the
`ADNET Systems, Inc.` spelling recorded above does not overwrite it. Both strings denote the same
ROR-identified organization and both are valid expressions of it, so the difference is not an error
to correct: the affiliation binds to the right organization either way, and what differs is the
display label on a row shared with other records. A future pass should not read the mismatch as
drift, and should not try to "fix" it.

**Affiliations attach to the shared `Person` row, so they spill over to her other software.**
Rebecca Ringuette is one `Person` record across every entry she authors in HSSI, and affiliations
hang off that record rather than off this software's authorship of it. Recording Heliophysics Digital
Resource Library and ADNET Systems therefore changes her rendered affiliations on her other entries
too. That consequence was weighed and accepted: all three affiliations are true of her, and the
Heliophysics Digital Resource Library and ADNET affiliations are corroborated by `Citation.cff` and
the reference publication. It is worth knowing because the change is one-way — an affiliation can
be added to a `Person` but not removed through a metadata update — so a later pass that regrets one
cannot simply undo it.

**Renaming an existing `Person` or `Organization` row is not possible through a metadata update.**
The stored affiliation is already correct, so no rename is required here; this note exists for a
future pass that finds one that is not. A
Person rename is silently ignored, and an attempt to edit an Organization's name can duplicate the
affiliation instead of changing it. So if a later refresh finds an affiliation whose *name* is
genuinely wrong — as distinct from the ADNET label above, which is not — the fix is a database-level
correction, and it should be flagged as such rather than attempted through the normal update path.
The Heliophysics Digital Resource Library and ADNET affiliations are distinct entries rather than
renames, so they are expressible, but the duplication behavior makes the resulting affiliation list
worth checking.

---

### 7. Software Name (MANDATORY)

**Value:** `Magnetospheric SWCX`
**Previously stored on the HSSI record:** `magnetospheric SWCX`

The name was corrected on evidence rather than changed on style: none of the sources consulted uses
a lowercase initial where it *names* the software. The candidates those sources supply are:

| Source | Name string |
|---|---|
| GitHub repository name; README H1 | `MagnetosphericSWCX` |
| README's own "Please cite this repository as" line | `Magnetospheric SWCX` |
| Zenodo/DataCite title; `Citation.cff` title | `rebeccaringuette/MagnetosphericSWCX: PublicationCode_v1.0` |

`Magnetospheric SWCX` is the author's own preferred citation string, and it differs from the stored
value in the initial capital alone. Adopting it therefore preserves the submitted wording while
correcting a capitalization that no consulted source uses as the software's name, which is what
makes a capitalization-only change to a submitted value worth making here rather than a matter of
taste.

**Considered and not selected: leaving the submitted `magnetospheric SWCX` in place.** Submitted
wording is normally preserved, and a capitalization difference is the weakest kind of reason to
overwrite it. It was not preserved because the lowercase form is not attested as a *name*. The
lowercase string does occur in the repository, but as a descriptive phrase inside a sentence — the
top-level README's "separating out the magnetospheric SWCX X-ray spectral contribution", and the
same phrasing in `PaperAnalysisCode/README.md` and `HSWCXPaperCode/README.md` — where the lowercase
is ordinary sentence case. Where the README names the software, on its "Please cite this repository
as" line, it capitalizes. Keeping the stored form would therefore preserve a phrase lifted out of a
sentence rather than an editorial choice about the name.

**Considered and not selected: `MagnetosphericSWCX`.** Field 7 asks for "the name of the software
package as listed on the code repository," which points at the closed-up repository name. It was not
chosen because the closed-up form is a GitHub naming constraint, whereas the README's citation line
is the author's deliberate statement of how the software should be named in prose.

**Considered and not selected: the Zenodo/DataCite title.** `rebeccaringuette/MagnetosphericSWCX:
PublicationCode_v1.0` is a release title generated by the GitHub–Zenodo workflow — an owner/repo
slug joined to a release name — rather than a name for the software.

**Presentation consequence, not a second value change.** HSSI renders the Version field by prefixing
the software name, so this change also changes that rendering from `magnetospheric SWCX - MSWCX` to
`Magnetospheric SWCX - MSWCX`. The stored version number remains `MSWCX` (Field 12) and is
untouched. A future pass should read that hyphenated string as a display transform, not as a version
value to be copied back.

---

### 8. Description (MANDATORY)

**Previously stored on the HSSI record (165 characters):**

> Code used to produce the results in a publication on separating out the magnetospheric SWCX X-ray
> spectral contribution in astrophysical observations of dark fields.

**Value (1,000 characters, one paragraph — written below as a single unwrapped line so it is
recoverable byte-for-byte):**

> Code used to produce the results in a publication on separating out the magnetospheric SWCX X-ray spectral contribution in astrophysical observations of dark fields. The repository collects the PyXSPEC scripts, XSPEC command scripts, and input files used to analyze HaloSat soft X-ray spectra of dark fields viewed through the flanks and down the tail of Earth's magnetosphere. The XSPEC scripts co-add and rebin the per-detector spectra; the PyXSPEC scripts then fit each observation with a model combining the particle background, Local Hot Bubble, Galactic halo, cosmic X-ray background, and solar wind charge exchange lines, and write the fitted parameters and uncertainties to CSV tables. Paired script variants add a second halo thermal component so that one- and two-temperature Galactic halo models can be compared. Code from the earlier heliospheric SWCX study of Ringuette et al. (2021) and superseded iterations are also included. The scripts were written for Python 2.7 and XSPEC 12.11.1.

**Why the previous value was replaced.** That string is the author's own abstract, and it is kept
intact as the opening sentence — this is an expansion, not a rewording. It needed replacing because
that same sentence is *also* the entire Concise Description (Field 9), which left the record
carrying a preview text and no detailed description at all. Field 8 asks for detail "sufficiently
detailed to provide the potential user with information to determine if the software is useful to
their work," and Field 9 exists precisely so the short preview can differ from it.

**Sourcing.** Each clause added to the author's opening sentence is drawn from the repository at
this revision: the file inventory and the Python/XSPEC split from the top-level README and
`PaperAnalysisCode/README.md`; the co-add and rebin steps from `MSWCX_sum_May29.xcm` and
`MSWCX_rebin40_May29.xcm`; the model components, the linked parameters and the CSV results tables
from `FlankFit_v18.py`, `TailFit_v18.py`, `FlankFitHot_v18.py` and `TailFitHot_v18.py`; the second
halo thermal component in the 'Hot' variants from `PaperAnalysisCode/README.md`; the historical
heliospheric SWCX code from the top-level README; and the Python 2.7 / XSPEC 12.11.1 pinning from
the READMEs.

**Cut from the longer draft, and where the material still lives.** Four things were dropped: the
per-species emission-line enumeration (the low-energy, O VII, O VIII and Ne IX Gaussians, with
secondary lines tied to primaries at computed branching ratios); the `steppar` parameter scans and
90%-confidence error mechanics; the `obs_att_cl_win.py` FITS attitude helper and its role in feeding
the BATS-R-US interpolation; and the README's caveat that the code would need updating to run under
current XSPEC and Python versions. All four remain documented in this dossier — under Fields 4, 19,
22, 23, 28 and 29 — which is the right home for them. A public catalogue description is not the
place to reproduce the analysis's internals.

**Considered and not selected: keeping the author's single sentence as the whole description.**
That is the most conservative treatment of submitted wording, and it would leave Field 8 unchanged.
It was rejected because it leaves the record with no detailed description at all — Fields 8 and 9
would continue to hold the identical 165-character string, so one of the two fields would carry no
information the other does not. The author's sentence is not discarded by the expansion; it opens
it, and it remains the sole content of Field 9.

**Deliberate wording: "magnetosphere" rather than "magnetosheath".** The repository's own READMEs
describe the same lines of sight differently, and both were re-read at this revision to confirm it.
`PaperAnalysisCode/README.md` places them in the magnetosphere: "'Tail' scripts analyze the cleaned
spectra obtained from lines of sight down the tail of the magnetosphere" and "'Flank' scripts
analyze the cleaned spectra obtained from lines of sight through the flank of the magnetosphere."
`Results/README.md` places them in the magnetosheath: "lines of sight through the flanks of the
Earth's magnetosheath" and "down the tail of the magnetosheath." Because the repository is
internally mixed on the point, the description uses the more general term rather than adjudicating
between the two READMEs. The specificity is not lost — Field 5 records `Earth Magnetosheath` and
`Earth Magnetotail` alongside the stored `Earth Magnetosphere`.

---

### 9. Concise Description (OPTIONAL)

**Value:**

> Code used to produce the results in a publication on separating out the magnetospheric SWCX X-ray
> spectral contribution in astrophysical observations of dark fields.

165 characters, inside Field 9's 200-character limit, and it is the author's own wording from the
GitHub repository description, the Zenodo/DataCite abstract and `Citation.cff`'s abstract. That is
the kind of short preview text Field 9 asks for, so it is kept unchanged. Expanding Field 8 does not
disturb it; the point of that expansion is precisely that the preview and the detailed description
should no longer be the same string.

---

### 10. Publication Date (RECOMMENDED)

**Value:** `2023-06-09`
**Previously stored on the HSSI record:** `2025-08-07`

**Why the previous value was wrong.** Field 10 is "date of first broadcast/publication … used for the
initial version of the software." No release or code change is dated to August 2025: the
repository's last commit is 2024-08-28 and the newest release is 2023-08-16. `2025-08-07` is most
consistent with the date the HSSI record itself was created, which is a record-keeping date rather
than a publication date. (The nearest August-2025 event in the sources consulted is the
2025-08-01 Zenodo metadata edit discussed under Field 12, which is likewise not a publication.)

**Evidence for 2023-06-09**, all pointing at the same day for the *initial* version:

- GitHub release `SolarWindChargeExchange` ("PublicationCode"): `published_at`
  `2023-06-09T20:26:37Z`.
- Zenodo record 8021786, the archive that release triggered: `created` `2023-06-09T20:26:41Z`
  (four seconds later), `publication_date` `2023-06-09`.
- The GitHub repository itself was created `2023-06-09T17:32:25Z`, and the first commits are dated
  2023-06-09.

**Considered and not selected: 2023-08-16.** That is the publication date of the *current* version
(`MSWCX`) and it is recorded in Field 12 as the version date. Field 10 explicitly asks for the
initial version, so the two dates should differ.

---

### 11. Publisher (RECOMMENDED)

- **Organization:** Zenodo
- **Publisher Identifier:** `https://zenodo.org`

Field 11 states that Zenodo is the correct entry for software whose DOI came through the
GitHub–Zenodo workflow, which is what happened here: the `SolarWindChargeExchange` and `MSWCX`
GitHub releases each triggered a Zenodo deposit within seconds. DataCite reports
`publisher = "Zenodo"` for the concept DOI.

---

### 12. Version (RECOMMENDED)

- **Version Number:** `MSWCX`
- **Version Date:** `2023-08-16` — HSSI previously stored `2025-08-01`
- **Version PID:** `https://doi.org/10.5281/zenodo.8253002`
- **Version Description:** see below — it replaced a duplicate of Field 8

**Version number — still the current release.** `MSWCX` is not a stale value:

- `git ls-remote` on the origin lists exactly two tags, `MSWCX` (`adf9ff43…`) and
  `SolarWindChargeExchange` (`6afa744e…`). `MSWCX` is the later of the two (tag commit 2023-06-21
  versus 2023-06-09).
- The GitHub releases API lists exactly two releases; the newer has `tag_name: MSWCX`, name
  `PublicationCode_v1.0`.
- Zenodo's `metadata.version` on the latest concept version is literally the string `MSWCX`, and
  `Citation.cff` records `version: MSWCX`.
- The default branch has moved past the tag (`9eab6392…`, 2024-08-28), but that commit adds only
  `Citation.cff` and edits one README DOI; no analysis code changed. There is no newer release.

**Version date — the previous value was a Zenodo record-edit timestamp, not a release date.**
`2025-08-01` corresponds to Zenodo record 8253002's `updated` field
(`2025-08-01T22:48:06.050988+00:00`), the moment the author last edited that record's metadata. The
actual release evidence converges on 2023-08-16:

- GitHub release `MSWCX`: `published_at` `2023-08-16T16:23:02Z`.
- Zenodo record 8252998, created `2023-08-16T16:23:08Z` — six seconds after the GitHub release,
  i.e. the archive that release triggered.
- Zenodo `publication_date` `2023-08-16` on both MSWCX records; DataCite `dates` for the concept DOI
  gives `{"date": "2023-08-16", "dateType": "Issued"}`.
- `Citation.cff`: `date-released: '2023-08-16'`.

**Considered and not selected: 2023-06-21**, the `MSWCX` tag's commit date. The tag was created in
June but the release was not published until August (`created_at 2023-06-21T23:02:23Z` versus
`published_at 2023-08-16T16:23:02Z` on the same GitHub release object). Field 12 asks for the date
the version was *released*, so the publication date is the right one.

**Version PID — two version DOIs exist for the same release, and the one HSSI holds is right.**
Records
8252998 and 8253002 are duplicate archives of the `MSWCX` release. 8253002 is preferred because
(a) the concept DOI resolves to it as the latest version, so DataCite's concept record carries its
metadata, and (b) `Citation.cff` records `doi: 10.5281/zenodo.8253002`, making it the author's own
choice. Two repo artifacts point elsewhere and should **not** be used to "correct" this field: the
README badge (`zenodo.org/badge/latestdoi/651636707`) redirects to **8252998**, and the README's
citation line names **8021786**, the superseded first release. Those are repo-internal
inconsistencies, recorded here so a later pass does not act on them.

**Version description — replaced.** The stored version description was byte-identical to the
software description (both 165 characters), so it conveyed nothing about the release itself. The
same 165-character string is also the stored concise description, so all three fields previously
carried the same one sentence. Field 12 asks for a "brief summary of major changes in the new
version," so the duplicate is replaced by the following 191-character release-specific summary:

> Release accompanying Ringuette et al. (2023). Adds example HaloSat input files, the result spreadsheets, and expanded README documentation; no analysis code changed from the previous release.

Evidence: `git diff --stat SolarWindChargeExchange MSWCX` lists changes to `ExampleData/*`,
`Results/*.xlsx`, `Results/README.md`, `ExampleData/README.md` and `README.md`, and to nothing else
— no `.py` or `.xcm` file differs between the two releases.

**Why overwriting submitted wording was justified.** Submitted wording normally needs a strong
reason to replace. The reason here is that it was not version wording at all but a copy of the
software description, so nothing release-specific was lost.

**Considered and not selected: a fuller summary** naming the GitHub/Zenodo release title
`PublicationCode_v1.0`, naming the earlier `SolarWindChargeExchange` release it supersedes, and
itemizing the added inputs (PHA spectra and a cleaned attitude file). All of that detail is recorded
in this field's notes above, and Field 12 asks for a *brief* summary, so the shorter form was
preferred.

**Changing a version leaves the previous `SoftwareVersion` row behind.** Any change to Field 12
creates a new `SoftwareVersion` row and repoints the software at it; the old row stays in the table
with nothing referencing it. That is accepted HSSI behavior rather than damage particular to this
record, and it is not something to clean up — a later pass should leave the unreferenced row alone
rather than propose removing it.

---

### 13. Programming Language (RECOMMENDED)

**Value:**

- `Python 2.x`
- `Other`

**Previously stored on the HSSI record:** `Python 2.x` alone

Both are live values in the `ProgrammingLanguage` vocabulary.

**`Python 2.x` — the repository evidence.** The repository holds 76 `.py` files. 72 of
them use syntax valid only in Python 2 — statement-form `print 'Initializing '+obsname`,
`dict.iteritems()` — and fail to parse under Python 3. The remaining four, the `ModelCalc*.py`
scripts in `HSWCXOlderCode/`, are simple enough to parse under either version, but the README states
outright that "All python code was written in python 2.7.15". `PaperAnalysisCode/README.md` and
`HSWCXPaperCode/README.md` both say "pyXSPEC in Python 2.6 or 2.7." GitHub's language statistics
report the repository as 100% Python (2,634,494 bytes).

**`Other` — standing for the XSPEC/HEASoft command-script language.** The repository contains six
`.xcm` files, and the README treats them as a distinct code type on equal footing: "These codes
include PyXSPEC code (.py files), XSPEC scripts (.xcm files) and other input files … all XSPEC code
was written using XSPEC 12.11.1." They are functionally necessary — the
`mathpha` and `grppha` command lines in `MSWCX_sum_May29.xcm` and `MSWCX_rebin40_May29.xcm` produce
the summed and rebinned `*_rebin40.pi` spectra that the four MSWCX fitting scripts in
`PaperAnalysisCode/` glob for (68 of the 76 Python files reference `rebin40`). The vocabulary has no
XSPEC, shell or Tcl row, so `Other` is the available representation. GitHub's linguist does not recognize
`.xcm`, which is why the language statistics show Python alone.

**Considered and not selected: `Python 2.x` alone.** `Other` is less informative than a named
language, but it is included because Field 13 asks for the most important languages and the `.xcm`
preprocessing step is necessary — without it the `*_rebin40.pi` spectra that the fitting scripts
glob for do not exist.

---

### 14. Reference Publication (RECOMMENDED)

**Value:** `https://doi.org/10.3847/1538-4357/acf3e2`

Ringuette, R., Kuntz, K. D., Koutroumpa, D., Kaaret, P., LaRocca, D., & Richardson, J. (2023).
"Observations of Magnetospheric Solar Wind Charge Exchange." *The Astrophysical Journal*, 955, 139.
Published 2023-09-27 (Crossref).

Corroboration: Zenodo record 8253002 carries `isDescribedBy → 10.3847/1538-4357/acf3e2`; the
repository README describes itself as "the code used to produce the results in a publication
separating out the magnetospheric SWCX X-ray spectral contribution"; and the paper's acknowledgement
states "All Python codes used in this analysis … are available at the same GitHub repository,"
citing "Ringuette 2023."

Note for a future pass: the README's inline hyperlink is to the *2021* paper
(`10.3847/1538-4357/ac0e33`), which covers the historical HSWCX code directories, not the
magnetospheric analysis. That DOI belongs in Field 27, where it is recorded, and is not a competing
candidate for Field 14.

**HSSI storage note:** the reference publication is held as a `RelatedItem` whose stored `name` is
the placeholder `UNKNOWN`. That placeholder is not user-visible and is not a defect in this field's
value.

---

### 15. License (RECOMMENDED)

**Value:**
- **License:** `MIT License`
- **License URI:** `https://spdx.org/licenses/MIT`

`MIT License` is a live value in the `License` vocabulary, and the URI above is the URL carried on
that row, so the pair is internally consistent.

**The conflict, and how it was resolved.** Three sources disagree:

| Source | Assertion |
|---|---|
| Repository `LICENSE` file, identical at tag `MSWCX` and at `main` | **MIT License**, "Copyright (c) 2023 rebeccaringuette" |
| GitHub's own license detection for the repository | `{"key": "mit", "spdx_id": "MIT", "name": "MIT License"}` |
| Zenodo record 8253002 (created 2024-03-19) | `apache2.0` |
| Zenodo records 8021786 and 8252998 (the GitHub-triggered deposits) | `other-open` |
| Repo `Citation.cff` on `main` | `license: [apache-2.0]` |
| DataCite for the concept DOI | `Apache License 2.0` |

**MIT was selected because the license text distributed with the code is the deciding artifact.**
The `LICENSE` file is the full MIT text, it is present in the archived snapshot the DOI points at,
and GitHub's independent scanner reads it as MIT. A case-insensitive search of the whole
working tree at this revision finds no occurrence of the string "apache" in any tracked file: there
is no Apache-2.0 license text, no `NOTICE` file and no per-file Apache header.

**Apache License 2.0 — rejected, with the reason it is not independent corroboration.** The
Apache-2.0 claim has a single origin. `Citation.cff` was exported from Zenodo, not hand-written: its
`abstract` still carries Zenodo's `<p>` HTML wrapper and its `title` is the Zenodo release title
`rebeccaringuette/MagnetosphericSWCX: PublicationCode_v1.0`. DataCite mirrors Zenodo. So the CFF and
DataCite are both downstream of the same Zenodo dropdown selection on record 8253002, and the
author's two earlier deposits of the same code say `other-open` instead. One deposit-form field,
propagated twice, does not outweigh the license text shipped in the repository.

**Durable follow-up, not a metadata fix.** This is an upstream inconsistency in the author's own
records: the Zenodo deposit says Apache-2.0 while the archived code says MIT. Recording `MIT
License` in HSSI is the right call for the code, but the discrepancy will persist until the author
corrects the Zenodo record, and a future refresh that re-reads DataCite will see Apache-2.0 again.
It should not be treated as new evidence.

**Considered and not selected: `Other`.** Available in the vocabulary and technically safe, but it
would discard information: the `LICENSE` file at this revision states the license explicitly.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Value (15):**

- `analysis`
- `astrophysics`
- `batsrus`
- `charge exchange`
- `csv`
- `halosat`
- `heliophysics`
- `heliosphere`
- `magnetosheath`
- `magnetosphere`
- `magnetotail`
- `solar wind`
- `spectroscopy`
- `swmf`
- `xspec`

**Previously stored on the HSSI record (7, lowercase):** `analysis`, `charge exchange`, `csv`,
`heliophysics`, `heliosphere`, `magnetosphere`, `solar wind`. The value above is a union — none of
the seven was dropped. Those seven are the Zenodo `keywords` list, so they carry the author's own
tagging.

Keywords is the one open vocabulary in the form, so supported terms can be recorded even when
they are not already present. The selected set avoids near-duplicates by preferring one broad
searchable term when a more specific variant would duplicate information carried elsewhere.

**Evidence for each addition:**

- `halosat` — the observational data the code reads are HaloSat products and the analysis targets
  are HaloSat observations. This keyword matters more than usual here: HaloSat has no row in HSSI's
  SPASE-backed instrument/observatory vocabulary (see Fields 31–32), so the mission cannot be
  recorded in Fields 31–32 and Field 16 is where it is carried as a searchable term.
- `xspec` — the software is PyXSPEC code and cannot run without XSPEC; the README pins XSPEC 12.11.1.
- `magnetosheath`, `magnetotail` — the two regions the observations sample, named explicitly in
  `Results/README.md` and `PaperAnalysisCode/README.md`.
- `spectroscopy` — the software uses X-ray spectral fitting. Chosen instead of
  `x-ray spectroscopy`, which would duplicate the broader term; the X-ray aspect is carried by
  Field 22 as `X-ray emission`.
- `batsrus`, `swmf` — `ExampleData/README.md` names BATS-R-US as the model the attitude file feeds,
  and the reference publication acknowledgment names "The SWMF/BATS-RUS model."
- `astrophysics` — the observations are astrophysical dark-field observations; the SWCX signal is a
  foreground contaminant for X-ray astrophysics.

**Considered and not selected:** `python` (Field 13 covers the language and the keyword would add
little), `CubeSat` (true of HaloSat but a property of the mission, not of the software),
`fitting` (redundant with the stored `analysis` plus `spectroscopy`), and `x-ray spectroscopy`
(a near-duplicate of `spectroscopy`).

---

### 17. Data Sources (OPTIONAL)

**Value:** `Observatory/Mission-specific`

A live value in the `DataInput` vocabulary. The observational inputs
are HaloSat-specific products: PHA spectra named by HaloSat target and detector ID
(`006801_01_cl1_d14.pi`), HaloSat responses (`halosat_avgenoise_20190423.rmf`,
`halosat_diag_20190423.rmf`, `hs_sdd_all20180701v001.arf`), and a HaloSat attitude file
(`hs007101-3_cl.att`). The reference publication says these "are available online through HEASARC's
archive."

**Field 17's cross-listing instruction cannot be satisfied here.** The field says that when a source
is observatory-specific, the observatory should be named in Field 32. HaloSat has no row in the
SPASE-backed vocabulary, so Field 32 is deliberately empty (see below). The `Observatory/Mission-specific`
selection is still correct; only the cross-reference is unavailable.

**Considered and rejected:**

- `OMNIWeb` — the reference publication acknowledges "the use of OMNI data provided by NASA/GSFC's
  Space Physics Data Facility's OMNIWeb service," but that data went into the externally computed
  solar wind inputs, not into this code. No script in the repository reads OMNI data.
- `HTTP/HTTPS Directories`, `FTP/FTPS Directories`, `S3/Cloud-aware`, `HAPI`, `CDAWeb` — the
  software has no retrieval layer of any kind at this revision; all inputs are local file paths.
- `Other` — unnecessary, since the accurate row exists and is already selected.

---

### 18. Input File Formats (RECOMMENDED)

**Value:**

- `FITS`
- `csv`

**Previously stored on the HSSI record:** `Other`, which is removed.

Both values are live `FileFormat` values; Fields 18 and 19 share that vocabulary.

**FITS.** The binary input products in the repository — `.pi`, `.arf`, `.rmf`, `.att` and `.fits` —
are FITS. Verified by reading the file headers directly: `ExampleData/006801_01_cl1_d14.pi` begins
`SIMPLE  =                    T / conforms to FITS standard`. The FITS-family inputs are `.pi`
(OGIP PHA spectra), `.rmf` and `.arf` (OGIP response matrices and effective-area files), `.att`
(HaloSat attitude tables) and `.fits` (`LHB_nH_ecl3.fits`, the hydrogen-column and Local Hot Bubble
table). The code reads them through `astropy.io.fits` (`t = pyfits.open(code_dir+'LHB_nH_ecl3.fits')`)
and through PyXSPEC's spectrum and response loaders.

**csv.** `PaperAnalysisCode/TailFit_v18.py` reads `NewHelioSWCX.csv` (predicted heliospheric SWCX
line intensities per observation) with `csv.DictReader`; `FlankFit_v18.py` reads the tail scripts'
own CSV results file back in to pick up the halo parameters; `obs_att_cl_win.py` reads
`MSWCX2021_GTI_cl.csv`. `csv` is a listed row, so the format needs no placeholder.

**Removal of `Other`, with reasoning.** `Other` means "a format not on the list." Both formats this
software actually reads *are* on the list, so the stored `Other` is a placeholder standing in for
values that can now be named precisely. Keeping it beside `FITS` and `csv` would assert a third,
unidentified input format that the repository does not contain; the `.xcm` files are command scripts
rather than data inputs and do not justify one. The removal is deliberate, and it is recorded here
so a later pass does not read the absence of `Other` as a lost value and restore it.

**Considered and not selected: keeping `Other` beside `FITS` and `csv`.** Leaving a stored value in
place is the safer default, and it breaks nothing — but it leaves the record asserting an input
format the repository does not have, so the precise pair was preferred.

---

### 19. Output File Formats (RECOMMENDED)

**Value:**

- `csv`
- `FITS`
- `ascii`
- `Other`

**Previously stored on the HSSI record:** `csv` alone — it is retained, and three formats are added.

**csv** — the primary results product. Each fitting script builds a header and
format string dynamically and writes one row per observation:
`chi_file = open(out_dir+model_note+'.csv','w')` then
`chi_file.write(file_format.format(halo_arr))`.

**FITS** — two independent producers. `PaperAnalysisCode/obs_att_cl_win.py` constructs a primary
HDU plus a binary table HDU with `pyfits.Column`/`BinTableHDU.from_columns` and
writes it with `hdulist.writeto(out_dir+att_filename, overwrite=True)`. Separately, the `.xcm`
scripts write FITS PHA files: `mathpha` emits the summed spectra and `grppha` emits the
`*_rebin40.pi` rebinned spectra that the Python scripts then consume.

**ascii** — each script opens an XSPEC log file and writes the full fit and error-run output to
it: `logFile = xs.Xset.openLog(out_dir+model_note+'_'+obsname+'_xspeclog.txt')`,
with additional numbered logs when the error loop re-runs. These plain-text logs carry the recorded
fit results, not just diagnostics.

**Other** — for two generated artifacts whose formats have no row: PostScript plot files, written
by `xs.Plot.device = out_dir+model_note+'_'+obsname+'_delchi.ps/cps'`
followed by `xs.Plot("data delchi")`; and the XLSX spreadsheets in `Results/`.

*Caveat worth recording about the XLSX files.* `Results/README.md` describes them as "the excel
spreadsheets produced by the pyXSPEC analysis scripts," but no code in the repository writes XLSX —
there is no `openpyxl`, `xlwt` or `pandas` import in any of the 76 Python files. The three files
(`file` reports them as "Microsoft Excel 2007+") are formatted derivatives of the CSV output; the
same README notes that "columns without a heading were used to format the results" and that
"highlighting … indicates a significant detection," both of which are spreadsheet formatting applied
after the fact. The PostScript plots alone justify `Other`; the XLSX files are a secondary reason
with this caveat attached.

**`ascii` is included deliberately.** Although XSPEC log files can be treated as diagnostics, they
count as output here because the logs carry the recorded fit and error-run results — the same
numbers that reach the CSV tables — rather than runtime chatter alone.

---

### 20. Operating System (RECOMMENDED)

**Value:**

- `Linux`
- `Windows`

Both are live values in the `OperatingSystem` vocabulary.

There is no packaging metadata or CI configuration to read this from, so the evidence is the
hardcoded paths in the scripts, which show the author running two halves of the workflow on two
platforms:

- **Linux** — the PyXSPEC fitting scripts:
  `spec_dir='/home/ringuette/MSWCX/RebinnedFiles/'`, `out_dir='/home/ringuette/MSWCX/Results/'`, and
  in the historical HSWCX scripts `/home/ringuette/halosat_sourceanalysis/…`. A commented line in
  `FlankFit_v18.py` even names a Linux HEASoft install path
  (`/home/ringuette/Software/heasoft-6.25/spectral/modelData/…`).
- **Windows** — `PaperAnalysisCode/obs_att_cl_win.py`, whose filename ends in `_win` and whose
  paths are `prefix_dir = 'C:/Users/rebec/Documents/UIowa/'`. That script imports `sys`,
  `datetime`, `numpy`, `astropy.io.fits`, `csv.DictReader` and the author's private `ruf_2_Loopd`
  helper — but not `xspec` — which is consistent with it being the part of the workflow that does
  not need HEASoft.

**Considered and not selected: `Mac`.** HEASoft and XSPEC are supported on macOS, and the Python
code uses no platform-specific API beyond file paths, so the software very likely runs there. It is
not included because no artifact in the repository evidences macOS use, and Field 20 asks for
systems the software "can successfully be installed on." The omission is a conservatism choice, not
a finding that macOS is unsupported; evidence of macOS use would justify adding it.

**Considered and rejected: `Operating System Independent`.** The fitting scripts require HEASoft/
XSPEC, which has no native Windows build, so the software as a whole is not platform-independent.
(Note that `OS Independent` is not a value in this vocabulary; `Operating System Independent` is the
spelled-out row to use if a later pass ever concludes the software is platform-independent.)

---

### 21. CPU Architecture (RECOMMENDED)

**Value:** `CPU Independent`

A live value in the `CpuArchitecture` vocabulary.

The repository contains interpreted Python and XSPEC command scripts and no compiled code: no C or
Fortran extensions, no build system, no binary executables, and no architecture-conditional
branches, so there is no compiled artifact that could be architecture-specific. The external
dependency, HEASoft/XSPEC, is distributed as buildable source across architectures, so it does not
constrain this field either.

**Considered and not selected:** `x86-64` — the hardware the author plainly used in 2020–2023, but
recording it would assert a restriction the code does not impose. `GPU` and `HPC or HEC` — no
GPU code, no MPI, no job scripts.

---

### 22. Related Phenomena (OPTIONAL)

**Value:**

- `Solar Wind`
- `X-ray emission`

Both are valid values in the closed `Phenomena` vocabulary. Although the form presents a free-text
affordance, an unlisted phenomenon is rejected rather than created, so it belongs in Keywords
instead.

- **Solar Wind** — solar wind charge exchange is the phenomenon the software exists to measure:
  highly charged solar wind ions capture electrons from neutrals and emit soft X-rays. The
  software's fitted quantities are the SWCX line intensities, and the H/He line ratios in the model
  (`OVIII_ratio = 0.4345`, "100% H → 0.320, 100% He → 0.549, 50/50 of each → 0.4345") are solar wind
  composition parameters.
- **X-ray emission** — the data are soft X-ray spectra, and the fitted model is built from X-ray
  emission and absorption terms (thermal plasma components, photoelectric absorption, a cosmic X-ray
  background power law, and emission-line Gaussians) alongside a non-X-ray particle-background
  term.

**The core phenomenon has no row.** "Charge exchange" itself is absent from the Phenomena
vocabulary. Per Field 22's instruction, it is carried in Keywords instead, where `charge exchange`
is already stored. Recorded here so a future pass does not attempt to add it to this field.

**Considered and rejected:** `Geomagnetic Storms` and `Coronal Mass Ejections`. The reference
publication mentions both in its introduction — "during explosive events, such as coronal mass
ejections, that induce geomagnetic storms, the magnetopause boundaries are pushed back" — but that
is background context about when magnetospheric SWCX is enhanced, not functionality the software
supports. The analyzed observations are not storm-time studies. `Coronal Heating`, `Solar Corona`
and `Solar Flares` have no supporting evidence.

---

### 23. Development Status (RECOMMENDED)

**Value:** `Inactive`

A live value in the `RepoStatus` vocabulary.

**The author states this directly.** Zenodo record 8253002 carries
`metadata.custom["code:developmentStatus"] = {"id": "inactive", "title": {"en": "Inactive"}}`, set
when she curated that record. That is a self-declaration in the same controlled vocabulary
(repostatus.org) that Field 23 uses.

Corroborating repository evidence: the last commit on `main` is 2024-08-28 and touched only
`Citation.cff` and one README DOI; the last code change was 2023-06-21; the repository is not
archived and issues remain open; and the README says "Updates to the code will be needed to
accommodate more recent versions of XSPEC and Python before adapting to an updated analysis" while
also inviting contact ("please feel free to create an issue to get my attention"). That is exactly
repostatus's `Inactive`: reached a stable, usable state, no longer actively developed, support
provided as time allows.

**Considered and rejected:** `Unsupported` (the author invites issues and has edited the record as
recently as 2025), `Abandoned` (the code reached a stable state and produced published results),
`Active` (no development since 2023), `Moved` (the repository has not relocated).

---

### 24. Documentation (RECOMMENDED)

**Value:** `https://github.com/rebeccaringuette/MagnetosphericSWCX/tree/MSWCX`

There is no documentation site, no `docs/` directory and no Read the Docs configuration. The
documentation is the repository's README plus a README in each of the six sub-directories
(`ExampleData`, `HSWCXOlderCode`, `HSWCXPaperCode`, `OlderVersions`, `PaperAnalysisCode`,
`Results`), which together explain the naming conventions, the script categories ('Tail', 'Flank',
'Hot'), the input files and the result spreadsheet columns. Field 24's instruction — "if this is the
same as the access URL, then enter that link here" — is satisfied by the repository URL.

---

### 25. Funder (OPTIONAL)

**Value (2 entries):**

- **National Aeronautics and Space Administration** — `https://ror.org/027ka1x80`
- **ADNET Systems, Inc.** — `https://ror.org/05we1n045`

**Evidence.** The reference publication's acknowledgement states: "The HaloSat mission was supported
by NASA grant NNX15AU57G. A portion of R.R.'s work was supported by ADNET Systems, Inc." Crossref's
funding record for the same DOI independently asserts
`{"DOI": "10.13039/100000104", "name": "National Aeronautics and Space Administration", "award":
["NNX15AU57G"]}`. R.R. is the sole author of this software, so the ADNET statement is a direct
statement about support for this work.

Field 25 asks for the complete name without acronyms, which is why the NASA entry is spelled out.

**ADNET Systems: funder or employer?** Both entries are recorded, and the employer reading was
weighed and set aside. ADNET Systems is the author's affiliation footnote in the reference
publication and is also recorded as an affiliation in Field 6, so listing it here could be read as
double-counting one relationship across two fields. It is kept as a funder because the
acknowledgement's sentence is specifically about support for her work on this analysis — "A portion
of R.R.'s work was supported by ADNET Systems, Inc." — which is what Field 25 describes: an entity
that "supports (sponsors) something through some kind of financial contribution." ADNET is a
contractor rather than the author's academic institution, so the employment and the sponsorship are
two facts about the same organization rather than one fact recorded twice.

**Considered and not selected: National Aeronautics and Space Administration alone.** The narrower
entry would sidestep the funder/employer ambiguity, and it is what Crossref's funding record would
support on its own. It was not chosen because it discards an acknowledgement sentence that names
financial support for this specific work.

**Considered and rejected: Centre National d'Études Spatiales (CNES).** The same acknowledgement
says "D.K.'s modeling work was supported by CNES." D. Koutroumpa is a co-author of the paper but not
an author of this software, and the CNES-supported modeling was the externally computed heliospheric
SWCX input rather than work on this code.

**Negative research:** Zenodo and DataCite carry no funding information for this software —
`fundingReferences` is an empty array on the concept DOI. The funder evidence comes entirely from
the reference publication.

---

### 26. Award Title (OPTIONAL)

**Value:**

- **Award Title:** Not found — no formal title exists for this grant, so the name stored below is a
  conventional funder-grant label rather than a title.
- **Award Name (as stored):** `National Aeronautics and Space Administration grant`
- **Award Number:** `NNX15AU57G`

**Evidence for the number.** Stated twice and consistently: the reference publication's
acknowledgement ("The HaloSat mission was supported by NASA grant NNX15AU57G") and Crossref's
funding record for that DOI (`award: ["NNX15AU57G"]`). The same grant number appears in the
acknowledgements of the two related HaloSat papers recorded in Field 27, which is consistent with it
being the HaloSat mission grant.

**Negative research on the title.** No official award title was found. Sources consulted: the
reference publication's acknowledgement (gives the number, not a title), Crossref's `award-info` for
all three related DOIs (number only, `awardTitle` absent), Zenodo and DataCite (no funding
references at all), and a web search for the grant number. The grant is described narratively as
funding the HaloSat mission, but no source consulted states a formal title. That negative result
stands unchanged by the name below: the stored name is a label, not a discovered title, and a later
pass should not read it as evidence that the search succeeded.

**Why this name.** HSSI's `Award` records follow a convention of pairing a descriptive funder-grant
name with the specific grant number in `identifier`, and other NASA grants in the catalogue are
recorded under this same name string, told apart by their numbers rather than by their names.
Adopting it keeps this award consistent with them, and it reuses the spelled-out funder name already
required in Field 25, whose "complete name without acronyms" guidance rules out `NASA`. The name is
51 characters and the number is 10, both well inside the 128-character caps on `Award.name` and
`Award.identifier`; a genuine title, if one is ever supplied, could come closer to that limit.

**Sharing a name with other grants is safe.** An award is matched on its `identifier` whenever one
is supplied, falling back to a name match only when the identifier is absent. Because `NNX15AU57G`
is this award's own number, the shared descriptive name cannot cause this entry to bind to a
different NASA grant. Recorded so a later pass does not mistake the shared string for a collision
risk and mint a bespoke variant to avoid it.

**Considered and not selected: storing the bare number `NNX15AU57G` as the name.** It is the most
literal way to record an award that has no title, but it collapses the name and the number into a
single value and so departs from the convention above, under which the name says who funded the
work and the identifier says which grant.

**Considered and rejected: storing no name at all.** Leaving the name empty is the most faithful
representation of "no title exists" — and `Award.name` is a required `CharField(max_length=128)`
declared `blank=False`, while `Award.identifier` is a nullable `CharField(max_length=128)`. The
submission path enforces this more strictly than the database does: it rejects a blank or missing
award name outright, so an award with no name cannot be attached to a software record at all. Some
label is therefore unavoidable, which is why the one chosen is conventional rather than invented.

**Considered and rejected: an invented descriptive title** such as "HaloSat mission support". It is
not the award's title, and it would put fabricated wording into the catalogue. The conventional
funder-grant name differs in kind: it names the funder and the nature of the record rather than
asserting a title the grant does not have.

**The award carries no link back to its funder.** HSSI's `Award` model has a `funder` field, but the
submission path does not populate it — an award is created or matched from its name and identifier
alone. So this award sits unlinked to the National Aeronautics and Space Administration entry in
Field 25, even though the acknowledgement and Crossref both name NASA as the grantor. The connection
is not lost, because the funder's name is embedded in the award name itself, but a later pass should
expect `Award.funder` to be empty here and should not read that emptiness as missing evidence or as
a defect in this record.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Value (2 entries):**

1. **`https://doi.org/10.3847/1538-4357/ac0e33`** — Ringuette, R., Koutroumpa, D., Kuntz, K. D.,
   Kaaret, P., Jahoda, K., LaRocca, D., Kounkel, M., Richardson, J., Zajczyk, A., & Bluem, J.
   (2021). "HaloSat Observations
   of Heliospheric Solar Wind Charge Exchange." *The Astrophysical Journal*, 918, 41.

   Strongest possible link short of the reference publication: this repository *contains the
   analysis code for this paper*. `HSWCXPaperCode/` and `HSWCXOlderCode/` hold its PyXSPEC scripts,
   its `.xcm` scripts and its response files, and the top-level README says so explicitly — "For
   historical purposes, the codes used to perform the analysis of the heliospheric SWCX published in
   Ringuette et al. (2021) are also included … The 2021 publication is accessible at
   https://doi.org/10.3847/1538-4357/ac0e33." Zenodo record 8253002 also carries
   `isDescribedBy → 10.3847/1538-4357/ac0e33`.

2. **`https://doi.org/10.3847/1538-4357/ac043b`** — Silich, E. M., Jahoda, K., Angelini, L.,
   Kaaret, P., Zajczyk, A., LaRocca, D. M., Ringuette, R., & Richardson, J. (2021). "A Search for
   the 3.5 keV Line from the Milky Way's Dark Matter Halo with HaloSat." *The Astrophysical
   Journal*, 916, 2.

   Included because the author declared the relation herself: Zenodo record 8253002 carries
   `isSupplementTo → 10.3847/1538-4357/ac043b`, and Field 27 is for publications the software
   developer prioritizes. **Caveat recorded deliberately:** the repository contains no code
   specific to that analysis, and R. Ringuette is a middle author rather than lead. Despite that
   caveat, the entry is retained because the author-declared Zenodo relation is direct evidence of
   developer priority.

**Considered and rejected:**

- **`https://heasarc.gsfc.nasa.gov/docs/halosat/about/halosat_pub.html`** — Zenodo record 8253002
  cites this with `resource_type: other`. It is a HEASARC page *listing* HaloSat publications, not a
  publication. Recorded here so a later pass does not mistake the Zenodo relation for a missing
  Field 27 entry.
- **HaloSat mission paper**, Kaaret et al. (2019), "HaloSat: A CubeSat to Study the Hot Galactic
  Halo," *ApJ* 884, 162 (`10.3847/1538-4357/ab4193`). It describes the instrument whose data this
  software analyzes, but it neither describes, cites nor uses the software, and the author did not
  declare a relation to it. Field 31/32 would have been the natural home for the mission link, and
  those fields are empty for vocabulary reasons (below) — but that is not a reason to relocate a
  mission paper into Field 27.

---

### 28. Related Datasets (OPTIONAL)

**Value (1 entry):**

- **`https://heasarc.gsfc.nasa.gov/docs/halosat/whatnew/halosat_reproc2023.html`** — HaloSat X-ray
  observation data, 2023 reprocessing (pipeline version `hsuf_20221026`, released 2023-05-01),
  NASA High Energy Astrophysics Science Archive Research Center.

**Evidence.** The author declared this relation on Zenodo record 8253002 as
`requires → …/halosat_reproc2023.html` with `resource_type: dataset`. The reference publication
states that "the processing files used in this analysis are available online through HEASARC's
archive" and that "all data from the HaloSat mission are available through the same HEASARC
archive." The reprocessing is directly relevant to the software's inputs: the 2023 reprocessing
"resolved a channel offset bug, eliminating the need for gain adjustments in spectral analysis."
The URL resolves, and at 74 characters it is well inside the 200-character URL limit.

**Negative research: HaloSat data have no DOI.** Field 28 prefers a DOI. The reprocessing
announcement gives no DOI, dataset version identifier or catalog identifier, and searches for a
HEASARC-minted HaloSat data DOI returned nothing. Field 28 explicitly permits a citation with a
permanent link when no DOI exists, which is the route taken. A future agent should not spend effort
re-searching for this DOI unless HEASARC begins minting them.

**Considered and not selected: the CCMC BATS-R-US simulation runs.** The reference publication names
four runs — `KD_Kuntz_071921_1` through `KD_Kuntz_071921_4` — "available by request through the CCMC
website," with metadata at `https://ccmc.gsfc.nasa.gov/ungrouped/GM_IM/GM_main.php` (verified live).
They are recorded here because they are genuinely part of the science, but they are not a Field 28
entry: this software does not read the run output. `ExampleData/README.md` describes the attitude
file as one "produced and subsequently used in the interpolation through the BATS-R-US model
output," and that interpolation happens outside this repository. The runs are also request-gated
rather than openly identified.

**Considered and not selected: the HaloSat ARF and RMF calibration products.** They are distributed
*inside* this repository, so they are part of the software rather than a related dataset.

---

### 29. Related Software (OPTIONAL)

**Value (3 entries):**

1. **XSPEC** — `https://heasarc.gsfc.nasa.gov/xanadu/xspec/`

   The essential domain-specific dependency, and the software's host platform. 75 of the 76 Python
   files `import xspec`; the analysis is built from `xs.Model(…)`, `xs.AllData(…)`, `xs.Fit.perform()`
   and `xs.Plot(…)`. The README pins the version ("all XSPEC code was written using XSPEC 12.11.1"),
   the reference publication's acknowledgement says "All spectral analyses were performed using XSPEC
   v12.11.1 (Arnaud 1996)," and the author declared `requires → …/issues.12.11.1d.html` on Zenodo,
   which pins the patch level to 12.11.1d.

   *Link choice.* The author's declared URL is XSPEC's *issues archive* page for release 12.11.1d.
   The general XSPEC page is used instead, because Field 29 asks for the code repository or "a
   link where users can find more information," and a patch-notes page is neither. The 12.11.1d URL
   is preserved here as the version evidence. XSPEC has no code repository or software DOI; its
   citable reference, Arnaud (1996) ASP Conf. Ser. 101, 17, is a publication and per Field 29's
   instruction publication DOIs do not belong in this field.

2. **HEASoft (FTOOLS)** — `https://heasarc.gsfc.nasa.gov/lheasoft/`

   The six `.xcm` command scripts do not invoke XSPEC proper — they invoke FTOOLS from the wider
   HEASoft distribution. `MSWCX_sum_May29.xcm` runs `mathpha` (81 invocations, co-adding
   per-observation spectra) and `MSWCX_rebin40_May29.xcm` runs `grppha … 'group min 40'` (81
   invocations, rebinning). Neither tool is optional: they produce the `*_rebin40.pi` files that
   the four MSWCX fitting scripts glob for. Listed separately from XSPEC so a user knows the full
   HEASoft toolset is required, not just the spectral fitting package.

3. **Space Weather Modeling Framework (SWMF)** — `https://doi.org/10.5281/zenodo.10552537`

   A domain-specific scientific dependency of the workflow. `ExampleData/README.md`: the attitude
   file "is an example of a file produced and subsequently used in the interpolation through the
   BATS-R-US model output." `PaperAnalysisCode/README.md`: `obs_att_cl_win.py` "produced the fits
   file containing spacecraft position and velocity information used to determine the O VII line
   intensity predicted by the MHD model for the magnetospheric SWCX contribution." The reference
   publication's acknowledgement names "The SWMF/BATS-RUS model … developed by Tamas Gombosi et al.
   at the Center for Space Environment Modeling, University of Michigan," and the author declared
   `cites → 10.5281/zenodo.10552537` on Zenodo. DataCite confirms that DOI is "Space Weather Modeling
   Framework," creator University of Michigan–Ann Arbor (ROR `00jmfr291`), 2024. BATS-R-US is the
   magnetohydrodynamic component of SWMF, so the SWMF DOI is the citable identifier for it.

**Considered and rejected, with reasons:**

- **numpy** — Tier A generic infrastructure. Every one of the 76 Python files imports it, which is
  exactly why it distinguishes nothing.
- **astropy** (`astropy.io.fits`, imported as `pyfits` in each of the 76 files) — Tier B, requiring a
  documented exchange rather than dependency presence. Here it is FITS file plumbing: reading the
  hydrogen-column table and the attitude file, and writing the output HK table. That is "uses
  astropy internally," which the field definition explicitly says does not qualify. Recorded so a
  later pass does not re-propose it on the strength of the import count.
- Python standard library modules (`glob`, `itertools`, `csv`, `os`, `sys`, `datetime`) — generic
  infrastructure.
- **`ruf_2_Loopd`** — `obs_att_cl_win.py` does `from ruf_2_Loopd import tai_time_conv`, but no file
  by that name exists anywhere in the repository. It is one of the author's private local modules,
  not published software, so it cannot be a Field 29 entry. Worth recording as a durable
  limitation: `obs_att_cl_win.py` cannot run as distributed, since the TAI-to-UTC conversion helper
  it needs is missing.

---

### 30. Interoperable Software (OPTIONAL)

**Value:** Not found — no package meets Field 30's demonstrated-exchange bar.

This is a considered conclusion rather than an unexamined blank. Field 30 requires a demonstrated
exchange with a peer tool: a shared or converted data model, output from one imported into the
other, an adapter API, a plugin relationship, a companion package, or a cross-language bridge that
this software provides.

**Candidates examined and why each falls short:**

- **XSPEC / PyXSPEC** — the closest call, and the reason to record this reasoning rather than leave
  the field silently empty. PyXSPEC is genuinely a Python bridge to a domain tool, and this software
  exchanges spectrum, model and fit objects with XSPEC continuously. But this software *runs inside*
  XSPEC through its Python API rather than interoperating with XSPEC as a separate peer tool — XSPEC
  is its host platform and essential dependency, which is why it is recorded in Field 29 instead.
- **SWMF / BATS-R-US** — there is a real data handoff (this software's FITS attitude table feeds an
  interpolation through BATS-R-US output), but the interpolation step is not in this repository and
  no adapter, converter or shared data model exists in the code. Recorded in Field 29 as a
  domain-specific dependency.
- **astropy** — Tier B without a documented exchange; internal FITS I/O only. See Field 29.
- **numpy** — Tier A; excluded without exception.
- **Kamodo** — checked specifically because this software's author leads that project, which would
  make an interoperation plausible. Searched for and not found: no `kamodo` import in any of the 76
  Python files, and no mention of Kamodo in the README, the sub-directory READMEs, or the full text
  of the reference publication. Recorded so a future agent does not propose it on the strength of
  shared authorship.

---

### 31. Related Instruments (OPTIONAL)

**Value:** No entry — documented omission.

**The instrument is identified; the vocabulary does not contain it.** The software is unambiguously
designed to support one instrument: the HaloSat **Silicon Drift Detector (SDD)** array, detectors
14, 38 and 54. It reads that instrument's PHA spectra, applies that instrument's ARF and RMFs
(`hs_sdd_all20180701v001.arf`, `halosat_avgenoise_20190423.rmf`, `halosat_diag_20190423.rmf`), and
`obs_att_cl_win.py` writes FITS headers naming it directly (`INSTRUME = ('SDD', 'Instrument name')`).
It passes the relevance gate easily.

**Negative research: HaloSat is absent from the SPASE-backed vocabulary.** Fields 31 and 32 draw on
`InstrumentObservatory`, whose rows are SPASE resources carrying a `https://spase-metadata.org/`
identifier. HaloSat has no row there, and the search was thorough:

- Case-insensitive searches of every row's `name`, `abbreviation` and `identifier` for `halosat`,
  `halo.?sat`, `\bhalo\b`, `iowa`, `silicon drift` and `\bSDD\b` returned no matches.
- Direct probes of the plausible SPASE resource IDs found nothing published:
  `https://spase-metadata.org/SMWG/Instrument/HaloSat/SDD`,
  `https://spase-metadata.org/SMWG/Observatory/HaloSat`, and the uppercase variant.
- A GitHub code search of the SPASE naming-authority repositories (`hpde/SMWG` and the wider `hpde`
  organization) for "HaloSat"/"HALOSAT" returned nothing.

**Falling back to the mission platform does not help either**, because HaloSat has no observatory
row — see Field 32. With nothing defensible to resolve to, the correct outcome is to omit the entry
and record why. The name is deliberately not written without an identifier: Fields 31 and 32 accept
no free-typed value, and a bare name would either bind to an arbitrary same-name row or mint a new
identifierless one of the kind the vocabulary was cleaned of.

**Why the gap exists, and what would close it.** HaloSat was a NASA *Astrophysics* Division CubeSat
(the first competitively funded by that division), operated 2018–2021 and reentered in January 2021.
SPASE's naming authorities cover heliophysics resources, so an astrophysics CubeSat is outside their
usual scope even though its data are used for heliophysics here. A new instrument enters the
vocabulary through the heliophysics.net refresh, not through a submission. The mission name is
carried as the keyword `halosat` (Field 16) and the mission-specific data source is recorded in
Field 17, so the association is not entirely lost.

**Also considered and rejected at the relevance stage** — recorded so a later pass does not mistake
these mentions for missing entries:

- **ACE / SWICS** — the reference publication acknowledges "the use of SWICS data provided by the
  ACE Science Center." Those data went into the externally computed solar wind and heliospheric SWCX
  inputs, which reach this software as a pre-computed CSV of line intensities
  (`NewHelioSWCX.csv`). No script reads ACE data.
- **SOHO / SWAN** — several script version histories say "using new SWAN-based helio calcs"
  (`HSWCX2_v10.py`, `HSWCX1_v122.py`). Same reasoning: SWAN observations fed a collaborator's
  external heliospheric SWCX calculation whose *results* arrive as CSV. (For completeness, SOHO/SWAN
  *does* resolve in the vocabulary — `Solar Wind Anisotropies`, abbreviation `SWAN`,
  `https://spase-metadata.org/SMWG/Instrument/SOHO/SWAN` — so the omission here is a relevance
  decision, not a resolution failure.)

---

### 32. Related Observatories (OPTIONAL)

**Value:** No entry — documented omission.

The mission is HaloSat, and the software plainly supports it: HaloSat observation IDs are parsed
structurally (`HS0068`–`HS0079` targets, observation chunk numbers, detector IDs), the FITS products
written by `obs_att_cl_win.py` carry `TELESCOP = ('HALOSAT', 'Telescope (mission) name')` and
`OBSERVER = ('PHILIP KAARET', 'Principal Investigator')`, and the data come from HaloSat's HEASARC
archive.

The same negative research applies as in Field 31: no observatory-type row in the SPASE-backed
vocabulary matches HaloSat, and `https://spase-metadata.org/SMWG/Observatory/HaloSat` is not a
published SPASE resource. The entry is therefore omitted and the reason recorded, and the name is
not written without an identifier.

**Considered and rejected at the relevance stage:**

- **SOHO** — resolves in the vocabulary (`Solar and Heliospheric Observatory`,
  `https://spase-metadata.org/SMWG/Observatory/SOHO`), but as with SWAN above, its data reached this
  work through a collaborator's external calculation, not through this code.
- **ACE** — same reasoning.
- **CCMC / CDAWeb / OMNIWeb / HEASARC** — archives and modeling services, not observatories. HEASARC
  is the source of the HaloSat data and is recorded in Field 28; the generic multi-mission archives
  belong in Field 17, where the accurate `Observatory/Mission-specific` value is already selected.

---

### 33. Logo (OPTIONAL)

**Value:** Not found

No logo or image file exists in the repository at this revision (the file inventory is 76 `.py`,
7 `.md`, 6 `.xcm`, 4 `.pi`, 3 `.xlsx`, 3 `.rmf`, 3 `.fits`, 3 `.csv`, 2 `.arf`, 1 `.att` and the
`LICENSE`). The README's only image is the Zenodo DOI badge, which is a badge rather than a project
logo. Zenodo, DataCite and `Citation.cff` carry no logo field.

---

## Cross-cutting negative research

Recorded so a later refresh does not repeat the work:

- **PyHC registry** — not a registered package. The three registry files (`projects_core.yml`,
  `projects.yml` and `projects_unevaluated.yml`) were read in full, and neither the package name,
  the repository URL, nor the author appears in any of them. This is expected — the repository is
  publication-analysis code rather than an installable Python package — and is not a quality
  signal.
- **Packaging metadata** — searched for and absent: no `setup.py`, `setup.cfg`, `pyproject.toml`,
  `requirements.txt`, `environment.yml`, `codemeta.json`, `.zenodo.json`, `AUTHORS`, `CONTRIBUTORS`
  or `CHANGELOG`. `Citation.cff` exists only on `main`, not at the released tag.
- **CI / testing** — no `.github/`, `.travis.yml`, `tox.ini` or test directory at this revision.
  This is why Fields 20 and 21 are derived from hardcoded paths and code inspection rather than from
  a build matrix.
- **SoMEF** — would add nothing here. Beyond the READMEs, the repository has no packaging or
  structured-metadata files for it to parse, and each field it could populate (name, description,
  authors, DOI, license, version, keywords, documentation, development status) is available from
  higher-priority sources: the Zenodo and DataCite APIs, the repository's own `Citation.cff` and
  READMEs, the GitHub releases and repository APIs, and the reference publication.
