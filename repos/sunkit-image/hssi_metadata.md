# HSSI Metadata Extraction Results

**HSSI Software ID:** 110491fc-f060-4b9d-ab2c-bb0806824948
**Repository:** https://github.com/sunpy/sunkit-image
**Source Revision:** c0200cc20bcc751c9ee19e7b47aa2d8ac1de1c1c
**Extraction Date:** 2026-09-09
**Validation Date:** 2026-09-09
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

All repository evidence in this file is read at the pinned revision
`c0200cc20bcc751c9ee19e7b47aa2d8ac1de1c1c` ("Updates from the package template (#341)", committed
2026-09-09), the tip of the default branch `main`. Three properties of that tree shape everything
below.

**Releases are tags on the main line, and the pin sits just past one.** Tag `v0.7.0` is
`b2ffa56ab9abc4fcec01bef86ef73c102b6fd15a` and is an ancestor of the pin; `v0.6.1`
(`deeffdad8378778463712ae939c3d0c7970e94d8`) is in turn an ancestor of `v0.7.0`. The 14 commits
between the tag and the pin are all automation (SunPyBot, dependabot, github-actions, pre-commit-ci),
and `changelog/` holds only its `README.rst` — no towncrier fragments are pending. So nothing
substantive is unreleased at the pin, and the pin's evidence and the released package's evidence do
not diverge.

**A trap for anyone reading `CHANGELOG.rst` headings mechanically:** the version prefix is
inconsistent. Line 1 is `v0.7.0 (2026-03-19)`, line 19 is `0.6.1 (2025-02-20)`, and every heading
below that is likewise unprefixed. A digit-anchored pattern (`^[0-9]`) therefore *skips the newest
section* and makes the file look as though it stops at 0.6.1. Use `^v?[0-9]`.

**The project publishes no machine-readable citation or author file.** There is no `CITATION.cff`,
no `.zenodo.json` and no `.mailmap` in the tracked tree at the pin. Author evidence therefore comes
from the Zenodo/DataCite deposit creator list (which the SunPy release process generates) and from
git history, and the two disagree in ways recorded under Field 6. The tree carries 119 tracked
files, 53 of them Python, and **zero** C, Fortran, IDL, Cython or MATLAB sources — a fact that
settles Field 13 and disposes of an IDL red herring described there.

One recurring question runs through Fields 4, 5, 17, 19, 31 and 32: sunkit-image's public functions
are deliberately instrument-agnostic (they take a `sunpy.map.GenericMap` or a bare array and return
one), while its test fixtures, tuned default parameters and twelve-example gallery are concretely
tied to particular observatories. Each of those fields resolves that tension separately and the
losing evidence is preserved as considered-and-rejected rather than deleted, so a later reader can
distinguish "known and decided against" from "missed".

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This entry was not submitted by this campaign; the placeholder is the catalogue-wide convention for
a record whose submitter is someone else, and it is not a defect to be repaired here.

### 2. Persistent Identifier (RECOMMENDED)
**DOI:** https://doi.org/10.5281/zenodo.5715430

This is the Zenodo *concept* DOI — the version-independent identifier that always resolves to the
newest deposit — and it is the correct choice for this field: it identifies the software rather than
one release, and the release-specific DOI belongs to Field 12 instead.

The usual hazard with a concept DOI is that it can resolve to an *older* release when a back-dated
deposit was created later. That hazard does not arise here: the newest deposit,
`https://doi.org/10.5281/zenodo.19338616`, is both the newest-created record and the newest version
(`v0.7.0`), so the concept DOI currently resolves to the latest release. DataCite gives the concept
record the title `sunpy/sunkit-image: v0.7.0`, `resourceTypeGeneral` `Software`, and nine
`HasVersion` relations. Nothing about this value is contested; it is carried over unchanged.

### 3. Code Repository (MANDATORY)
**URL:** https://github.com/sunpy/sunkit-image

The canonical repository, confirmed three ways: `pyproject.toml` declares it under
`[project.urls]` as `"Source Code" = "https://github.com/sunpy/sunkit-image"`; the PyHC community
registry entry gives `code: "https://github.com/sunpy/sunkit-image"`
(`_data/projects.yml` in `heliophysicsPy/heliophysicsPy.github.io`, the `- name: "sunkit-image"`
block); and every Zenodo deposit relates to it with `IsSupplementTo`
`https://github.com/sunpy/sunkit-image/tree/v0.7.0`. Carried over unchanged.

### 4. Software Functionality (RECOMMENDED)
**Selected Categories:**
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Image Processing
- Data Processing and Analysis: Time Series Analysis
- Data Processing and Analysis: Wavelet Analysis
- Data Visualization
- Data Visualization: 2D Graphics

The five subcategory values were already on the record before this refresh and all five are
defensible; the two **top-level parents are added**, because a stored subcategory whose parent is
absent breaks the taxonomy rule that a subcategory always implies its parent, and because a searcher
browsing the top-level category "Data Processing and Analysis" would otherwise never reach this
entry. Values are written in the fully-qualified `Parent: Child` form: several child names recur
under more than one parent in this vocabulary, so an unqualified child can bind the wrong row.

Evidence for each retained value, by module (`__all__` read at the pin):

- **Image Processing** — the package's whole purpose. `enhance.mgn` / `enhance.wow`,
  `radial.fnrgf` / `intensity_enhance` / `nrgf` / `rhef`, `trace.bandpass_filter` / `occult2` /
  `smooth`, `granule.segment`, `stara.stara`, and the four-module `coalignment/` subpackage all
  operate on 2-D solar image data. This one value also carries the feature-detection and
  registration work described below, because the vocabulary has no finer rows for them.
- **Analysis** — derived scientific quantities rather than pixel filtering: `asda`'s eight public
  functions compute vortex properties, radial and rotational velocities and velocity fields from a
  flow field; `utils.utils.get_radial_intensity_summary` reduces a map to a radial intensity
  profile; `utils.noise.noiselevel` estimates image noise level.
- **Time Series Analysis** — `time_lag` (`cross_correlation`, `get_lags`, `max_cross_correlation`,
  `time_lag`) cross-correlates per-pixel light curves across a time dimension. `time_lag.py:175`
  states the physical use: "on AIA, the time lag is the lag which maximizes the cross-correlation".
- **Wavelet Analysis** — `enhance.wow` implements Wavelets Optimized Whitening, delegating to the
  à-trous wavelet machinery it imports at `enhance.py:263` (`from watroo import B3spline, utils`)
  and passing a wavelet scaling function and per-scale weights.
- **2D Graphics** — modest but real. `granule.segment` does not merely return an array: it builds a
  `sunpy.map.GenericMap` and attaches display instructions to it
  (`granule.py:78-81`, a four-colour `mpl.colors.ListedColormap` and a `BoundaryNorm` written into
  `plot_settings`), so the package prescribes how its own product is rendered. All twelve gallery
  examples then plot map products with matplotlib.

**Considered and rejected, with reasons** (recorded so a later refresh does not re-propose them):

- **Coordinate Transforms / Coordinate Transforms: Solar** — rejected. Coordinate work exists but is
  strictly internal plumbing, never a user-facing capability: `radial.py:527` transforms pixel
  coordinates with `smap.pixel_to_world(x, y).transform_to(frames.Helioprojective)` in order to
  compute pixel radii, and `coalignment/interface.py:82` calls
  `reference_map.wcs.pixel_to_world(*new_reference_pixel)` to express a fitted shift as a new
  reference coordinate. Those two are the only *executable* coordinate sites in the package's public
  modules. The same anchored search — `frames.`, `Helioprojective`, `SkyCoord`, `world_to_pixel`,
  `pixel_to_world` over every tracked `.py` file under `sunkit_image/`, with the `tests/`
  directories and `sunkit_image/conftest.py` both set aside as test scaffolding — returns nothing
  else executable. Two points about that scope, because a carelessly stated filter would not support
  the claim: `conftest.py` sits at `sunkit_image/conftest.py` and is therefore *not* removed by a
  bare `tests/` exclusion, and it does hit, at lines 20, 140, 141, 155, 156, 169 and 170 — all of it
  `Helioprojective` and `SkyCoord` use that builds pytest fixtures, none of it package API. The only
  remaining hits are non-code: `radial.py:170` and `radial.py:282` are docstring prose about
  Helioprojective Cartesian maps, and `radial.py:525` is the comment introducing the two-line block
  that ends in the cited call at `radial.py:527`. No public function converts between frames for the
  user, and no frame conversion is exposed as an output.
- **Data Processing and Analysis: Data Access and Retrieval** — rejected. The package downloads
  nothing. Every `Fido` call in the tree is in `examples/` and belongs to sunpy, not to this
  package's API. This is the same finding that keeps Field 17 empty.
- **Data Processing and Analysis: Processing** — rejected as non-discriminating. It is a catch-all
  that would add no information beyond the specific `Image Processing`, and a searcher filtering on
  it gains nothing about this package.
- **Data Processing and Analysis: File Format Conversion** — rejected; the package reads and writes
  no files itself (see Field 19).
- **Data Visualization: Movies** — rejected. `examples/finding_sunspots_using_stara.py` runs over a
  `MapSequence`, but nothing animates or exports frames; no `matplotlib.animation` use exists in the
  tree.
- **Models and Simulations (any child)** — rejected. Nothing here models a physical system; the
  package processes observations.

**Nothing further is recorded, and the three capability groups a searcher might expect as separate
values have nowhere to go.** Feature detection and segmentation (`stara`, `granule`, `asda`),
coalignment/registration (`coalignment/`) and image enhancement (`enhance`, `radial`) have **no
dedicated rows** in this vocabulary; the nearest rows are the `Image Processing` and `Analysis`
values already recorded, which carry them. Every capability of the package therefore maps onto a
value already listed, and no available row describes segmentation, registration or enhancement more
precisely. Anything beyond the seven would be a deliberately loose fit, and two such fits were
examined and not recorded:

- **`Data Processing and Analysis: Processing`** was examined a second time here, not as a
  description of the enhancement and registration pipelines but as a broad hook for them. It would
  gain a coarser filter hit at the cost of the precision `Image Processing` already supplies, and the
  rejection above stands: it is a catch-all that tells a searcher nothing about this package.
- **`Data Processing and Analysis: Calibration`** was examined on the argument that
  `coalignment.coalign_map` corrects instrument pointing and rewrites the map's reference coordinate,
  which is a *metadata* calibration. It is not recorded, because this vocabulary's sense of
  calibration is the conversion of raw instrument counts to physical units, which this is not, and
  because `update_map_metadata` explicitly refuses rotation and plate-scale corrections
  (`NotImplementedError` at `coalignment/interface.py:74` and `coalignment/interface.py:76`). The
  code detail behind the argument is preserved because the two functions are easy to conflate:
  `coalign_map` (`def` at `coalignment/interface.py:159`) computes the affine parameters and then
  delegates the entire metadata rewrite —
  `return update_map_metadata(target_map, reference_map, affine_params)` at
  `coalignment/interface.py:221` — to `update_map_metadata`, whose body is
  `coalignment/interface.py:39-91` and which is where the new reference coordinate is actually
  derived.

### 5. Related Region (RECOMMENDED)
**Selected Categories:**
- Corona
- Photosphere
- Solar Environment

`Solar Environment` was the only value on the record before this refresh. The two additions are
enrichment, not correction: this vocabulary is **flat** — `Corona` and `Photosphere` are top-level
rows in their own right, not children of `Solar Environment` — so the coarse value never implied
either of them, and a searcher filtering on `Photosphere` could not previously find this package.

- **Photosphere** — `granule.segment`'s own docstring opens "Segment an optical image of the solar
  photosphere into tri-value maps with:" (`granule.py:16`); its only fixture is
  `sunkit_image/data/test/dkist_photosphere.fits`; the module's brightpoint size constant is
  justified by a paper on photospheric bright points (`granule.py:204`); `stara` is tuned for HMI
  continuum images (`stara.py:45`, `stara.py:50`), which are photospheric; and `asda` detects
  photospheric swirls.
- **Corona** — `radial`'s filters are coronal-imaging filters (NRGF, FNRGF and RHEF, whose
  references at `radial.py:313`, `radial.py:509` and `radial.py:704` are all coronal-imaging papers);
  `trace.occult2` traces coronal loops; `time_lag` studies coronal cooling in active regions; and
  `examples/remove_cosmic_rays.py` works on LASCO C2 coronagraph data.
- **Solar Environment** — retained. It is the accurate coarse statement for a package that is solar
  from end to end, and it is what a user browsing at the coarse level filters on.

**Considered and rejected:** `Chromosphere` — zero case-insensitive matches for "chromosphere"
anywhere under `sunkit_image/`, `docs/`, `examples/`, `README.rst` or `CHANGELOG.rst`.
`Solar Interior` and `Solar Wind` — likewise unevidenced; the package neither models the interior nor
handles in-situ solar-wind data. `Interplanetary Space` — no.

### 6. Authors (MANDATORY)

Nineteen authors are on the record, in this stored order. All nineteen are retained; fifteen carry
ORCIDs and four do not. Affiliations are shown as stored.

1. **Saksham Alok** — no identifier; no affiliation.
2. **Will Barnes** — https://orcid.org/0000-0001-9642-6089 — American University
   (https://ror.org/052w4zt36); Department of Physics, American University; Goddard Space Flight
   Center (https://ror.org/0171mag52); United States Naval Research Laboratory
   (https://ror.org/04d23a975).
3. **Samuel Bennett** — https://orcid.org/0000-0001-6420-4422 — Aperio Software Ltd.; University of
   Sheffield (https://ror.org/05krs5044).
4. **Vatsalya Chaubey** — no identifier; no affiliation.
5. **Jayraj Dulange** — https://orcid.org/0009-0003-2993-7382 — Indian Institute of Technology
   Gandhinagar (https://ror.org/0036p5w23).
6. **Frédéric Auchère** — https://orcid.org/0000-0003-0972-7022 — Institut d'Astrophysique Spatiale,
   Université Paris-Sud (https://ror.org/014p8mr66).
7. **Nabil Freij** — https://orcid.org/0000-0002-6253-082X — Bay Area Environmental Research
   Institute (https://ror.org/024tt5x58); Lockheed Martin Solar and Astrophysics Laboratory; SETI
   Institute (https://ror.org/02dxgk712).
8. **Ghaith Kdimati** — https://orcid.org/0009-0006-8851-7814 — Cairo University
   (https://ror.org/03q21mh05).
9. **Chris R. Gilly** — https://orcid.org/0000-0003-0021-9056 — Southwest Research Institute
   (https://ror.org/03tghng59).
10. **Laura Hayes** — https://orcid.org/0000-0002-6835-2390 — Dublin Institute for Advanced Studies
    (https://ror.org/051sx6d27); European Space Research and Technology Centre
    (https://ror.org/03h3jqn23).
11. **Jack Ireland** — https://orcid.org/0000-0002-2019-8881 — Goddard Space Flight Center
    (https://ror.org/0171mag52).
12. **Michael Kirk** — https://orcid.org/0000-0001-9874-1429 — Catholic University of America
    (https://ror.org/047yk3s18); Goddard Space Flight Center (https://ror.org/0171mag52).
13. **Pey Lian Lim** — https://orcid.org/0000-0003-0079-4114 — Space Telescope Science Institute
    (https://ror.org/036f5mx38).
14. **Abinash Mahapatra** — https://orcid.org/0009-0000-5975-6775 — Odisha University of Technology
    and Research (https://ror.org/031jmyr19).
15. **Stuart J. Mumford** — https://orcid.org/0000-0003-4217-4642 — Aperio Software Ltd.; University
    of Sheffield (https://ror.org/05krs5044).
16. **Jeffrey Aaron Paul** — no identifier — Dayananda Sagar College of Engineering, Bangalore.
17. **David Stansby** — https://orcid.org/0000-0002-1365-1908 — Advanced Research Computing Centre,
    University College London, UK; Department of Mechanical Engineering, University College London;
    Imperial College London (https://ror.org/041kmwe10); Mullard Space Science Laboratory,
    University College London; University College London (https://ror.org/02jx3x895).
18. **Matt Wentzel-Long** — https://orcid.org/0000-0002-3106-4598 — Stark State College
    (https://ror.org/05q9ht188).
19. **Leah Zuckerman** — no identifier; no affiliation.

**The author list's provenance.** With no `CITATION.cff` and no `.zenodo.json` in the tree, the
authoritative published list is the creator list of the Zenodo/DataCite deposit, which is identical
(21 entries) on the `v0.7.0` record and on the concept record. Those 21 entries are these 19 people
plus `SunPyBot` (a bot, correctly excluded from a human author list) and `bberkeyU` (a handle,
discussed below). The deposit carries **no** `nameIdentifiers` for any creator, so every ORCID above
came from identity work done outside the deposit, and six of the 21 creator strings are handles,
honorifics or abbreviated forms: `Dr. Gilly`, `Ghaithq`, `frederic-auchere`, `P. L. Lim`,
`SunPyBot`, `bberkeyU`. Four of those six the record has already resolved to personal names; of the
remaining two, `SunPyBot` is the bot excluded above and `bberkeyU` is the unresolved identity
examined and not added below. Those four earlier resolutions are worth preserving, because a
future refresh reading the deposit will meet the raw strings again:

- `Dr. Gilly` is an honorific standing where a personal name should be, and it is the *entire*
  stored name: DataCite splits none of this deposit's creators, carrying each one's whole unsplit
  string in `familyName` with no `givenName` at all. The same contributor appears in git history
  as `C. R. Gilly`, `Chris R. Gilly` and `Dr. Gilly` under the single address `gilly@swri.org`, and
  SunPy credits him as "Chris R. Gilly"; the catalogue holds one record under that canonical name.
- `Ghaithq` is a handle. `ndcube`'s `.mailmap` maps the alias to **Ghaith Kdimati**, and sunpy's
  `.zenodo.json` entry for that name carries ORCID `0009-0006-8851-7814`. Recorded under the
  personal name because a real identity is proven; the handle-plus-platform convention applies only
  where no human name is published.
- `frederic-auchere` is a GitHub login (`43064172+frederic-auchere@users.noreply.github.com`). ORCID
  `0000-0003-0972-7022` resolves to Frédéric Auchère at Institut d'Astrophysique Spatiale, matching
  the stored affiliation, and that account's public repositories are this author's own published work
  (`wow`, `wavelets`, `awkward`, `campfires`).
- `P. L. Lim` is an initials form of **Pey Lian Lim**, GitHub `pllim`, ORCID
  `0000-0003-0079-4114`, employed at the Space Telescope Science Institute — the affiliation the
  deposit itself supplies for that creator string.

**A second employer for Chris R. Gilly (author 9) was examined and is not recorded.** The
affiliation recorded for him above is Southwest Research Institute alone. Good evidence names
Northwest Research Associates as well, and that evidence is not in doubt — both employers are true
of him. It is preserved in full here rather than left to be rediscovered, because a later refresh
reading either source will meet it again and should find this reasoning waiting.

**The evidence for the second employer.** Two sources name it.

- The `v0.7.0` DataCite deposit stores his creator entry under the name string `Dr. Gilly` — an
  honorific sitting in the name field, resolved to his personal name as described above — with the
  affiliation string `NorthWest Research Associates`, capital W. It is cited as that stored creator
  string rather than as a full name, because the raw string is what a later refresh reading the
  deposit will actually meet.
- His ORCID record, https://orcid.org/0000-0003-0021-9056, reads the two employers as consecutive
  jobs rather than as a contradiction: "Southwest Research Institute Boulder", Solar & Heliospheric
  Physics, Postdoctoral Researcher, 2023-01-23 to 2026-01-23, then "NorthWest Research Associates",
  Solar and Stellar Physics, Research Scientist, from 2026-01-26 with no end date. Both employments
  are true of him, which is why the candidate was an addition and not the correction of an error.

**Two provenance nuances, separated so a later refresh does not misread either.**

- *Different granularity, not a conflict.* The ORCID employment names the Boulder division: its
  organization name is "Southwest Research Institute Boulder", disambiguated by RINGGOLD identifier
  133951. The value recorded above is the parent institute, "Southwest Research Institute", with ROR
  https://ror.org/03tghng59. Those are two granularities of the same employer, and the
  parent-institute form is the right one for a catalogue affiliation — a future refresh should not
  read the difference as a mismatch to be reconciled.
- *The Northwest Research Associates ROR is name-matched, not supplied.* That employment entry on the
  ORCID record carries no disambiguation identifier at all. So https://ror.org/0583jne22 does not
  come from ORCID; it comes from matching the name against the organization row the catalogue already
  holds under that ROR. That is weaker provenance than the Southwest Research Institute side, where a
  RINGGOLD identifier pins the organization independently of how its name is spelled.

**Why Southwest Research Institute alone is the recorded value.** It is the affiliation under which
he contributed the RHEF work and the one his commit address `gilly@swri.org` records, so it is the
employer this software's own history attests. Two durable properties of how affiliations are held —
not facts about him — settle the rest:

- *An author affiliation is not a field on this software's record.* It is attached to the shared
  person record for Chris R. Gilly, so whatever that record holds is displayed by every catalogue
  entry crediting him, not by this one alone. An addition made on this entry's evidence would reach
  entries this refresh has not examined.
- *An affiliation can only be added, never replaced.* No ordinary metadata update can swap one
  affiliation for another. Adding Northwest Research Associates would therefore leave him carrying
  both employers at once, and recording only his current employer instead is not reachable that way
  at all — it would take a correction to the person record itself.

**The spelling, should a later refresh ever record it.** The form to write is
`Northwest Research Associates` with a lower-case "w", not the deposit's and ORCID's `NorthWest`.
Lower-case is the ROR display form of https://ror.org/0583jne22 and the name of the organization row
the catalogue holds under that ROR, so writing it that way attaches the existing row instead of
creating a variant spelling.

**Two candidate authors were examined and neither is added; the author list stands exactly as
recorded above.** Each would have been a genuine addition of a contributor the project's own records
treat differently from the other 19, and each would have created a new person record — the catalogue
holds no row for either identity: no row carries the family name `Berkey`, and the only `Liu` rows
belong to different people. Both candidacies are set out in full below, evidence and
counter-evidence, because that evidence is expensive to reconstruct and a later refresh meeting
either contributor again should not have to redo it to reach the same decision.

**(i) Jiajia Liu** — ORCID `https://orcid.org/0000-0003-2569-1840`.

*For:* he is the author of an entire public module. Commit
`b3f4bfbc891ac84f406c1cfe2642ff7521c6f365` ("Add ASDA into sunkit-image (#40)", 2019-12-22,
authored as `Jiajia <jj.liu@sheffield.ac.uk>`) added `sunkit_image/asda.py` (472 lines), its tests,
its test data and the supporting gamma-value machinery in `utils/utils.py`; `asda.py` is still a
public module at the pin with eight exported functions. He holds the module's third-party copyright
— `licenses/LICENSE_ASDA.rst` reads "MIT License" and "Copyright (c) 2023 Jiajia Liu" — and he is
first author of the algorithm paper the module implements, cited in `utils/utils.py:299-303` as
"Equation (1) in Jiajia Liu, Chris Nelson, Robert Erdelyi." with
`https://doi.org/10.3847/1538-4357/aabd34`. Critically, **he made the commit himself**: this is not a
maintainer importing a stranger's code, it is the algorithm's author contributing his own
implementation. From a searcher's side, someone looking up his name would reasonably expect to find
the package that ships his algorithm as he wrote it. The ORCID binding is safe because it was made
on *works*, not on a name: a bare name query for a common Chinese name returns far too many records
to choose from, whereas querying the ASDA paper's DOI as a self-asserted work returns exactly the
three ASDA authors, one of whom is Jiajia Liu. That record's employment history then binds the
commit era independently of the name: it lists the University of Sheffield, School of Mathematics
and Statistics, Research Associate, 2017-05 to 2020-05 — a window that contains the 2019-12-22
commit — and matches its `sheffield.ac.uk` address. His current employer on the same record is the
University of Science and Technology of China, from 2022-10. ORCID's primary name form for the
record is given name `Jiajia`, family name `Liu`, with no credit name and no other-names, so
"Jiajia Liu" is the form to record. **A methodological caveat for anyone re-checking this:** read
the record's employments, not the expanded-search `institution-name` array, which for this record
lists an institution that appears in no employment entry at all.

*Against:* the project does not credit him. He is absent from the 21 Zenodo creators and from the
stored 19, and `licenses/README.rst` frames that whole directory as holding license information for
"works the package is derived from, and/or datasets." — language that reads as treating ASDA as
*derived* third-party work rather than first-party contribution. Adding an author the project itself
omits from its own citation metadata asserts a credit decision that is arguably the project's to
make.

*Had he been added, his affiliation would have been a second decision, and the options differed in
consequence — kept here because a later refresh that reopens the question needs them:*
**University of Sheffield** with ROR `https://ror.org/05krs5044` is the commit-era employer, bound
by both the employment window and the commit address, and it attaches an organization row the
catalogue already holds — the same row two other authors of this software (Samuel Bennett, Stuart J.
Mumford) already carry, so it is internally consistent and creates nothing. **University of Science
and Technology of China**, ROR `https://ror.org/04c4dkn09`, is his current employer, and the
catalogue holds no row for it, so choosing it creates a new organization row. **No affiliation** is
also a legitimate option, matching the four stored authors who carry none. If Sheffield is chosen,
it must be written as the plain institution name with its ROR: the catalogue also holds an
identifier-less departmental row named `SP2RC, School of Mathematics and Statistics, University of
Sheffield`, and his ORCID department string is literally "School of Mathematics and Statistics", so
a department-style affiliation could bind that other row instead.

**(ii) `bberkeyU`** — no resolvable personal identity.

*For:* **the project itself credits the handle.** `bberkeyU` is one of the 21 Zenodo/DataCite
creators on both the concept and `v0.7.0` records, so this is not an inference — the release
metadata names it. Its single substantive commit, `d2b296052676c15615984b30f1a669e7d8642123`
("Rhe ignore nans (#254)", 2025-02-20), rewrote NaN handling in `sunkit_image/radial.py`, and that
is precisely the change `CHANGELOG.rst:38` records for the v0.6.1 release as "Fixed NaN handling in
`sunkit_image.radial.rhef`." — the fix that release is partly remembered for. The v0.6.1 GitHub
release notes name the handle directly: "@bberkeyU made their first contribution". The 19-author list already includes people with no
identifier at all, so an identifier-less entry is not anomalous here.

*Against:* the identity cannot be resolved to a person. The GitHub account `bberkeyU` has null name,
company, bio, email and location; the only identity evidence anywhere is the commit address
`berkey@ucar.edu`. An ORCID family-name search for `Berkey` returns nobody at UCAR (the nearest
match is at a different institution), so no ORCID can be bound safely. Recording a bare handle as an
author gives a catalogue user a name they cannot act on, and it is one commit against a single
module.

*The question was a credit policy, not a fact-finding gap, and it is the policy that has been
settled.* Both candidacies are fully evidenced; what was undecided was whose judgement of authorship
the catalogue should mirror — the project's published creator list (which includes `bberkeyU` and
excludes Jiajia Liu) or the substance of the contribution (which favours Jiajia Liu most strongly of
the two). Neither criterion was adopted as governing: the outcome is that neither candidate is added
and the nineteen personal names already on the record stand. This file took no position between the
two readings and takes none now — what is settled is that the recorded list does not change, not
that either candidacy is weaker than the evidence above makes it look. A later refresh arriving with
new evidence about either contributor is looking at a policy already applied, not at an argument
that lost.

**A standing limitation on identifier work in this field.** Four of the nineteen authors above carry
no identifier, and a later refresh will be tempted to supply one. Recording an ORCID for an author
already stored without an identifier is not a safe field write: it does not annotate the existing
person record, it creates a second record for the same human and leaves the original in place,
unidentified, on this entry. Supplying an identifier for any of those four is therefore a correction
to the person record itself rather than a field update, which is why none is attempted here.

### 7. Software Name (MANDATORY)
**Name:** sunkit-image

Carried over unchanged, and confirmed by the project's own spelling throughout: the README title is
``sunkit-image``, PyPI distributes `sunkit-image`, and the PyHC registry entry is
`- name: "sunkit-image"`. Note that the *import* name and the `[project] name` in `pyproject.toml`
are `sunkit_image` with an underscore; the hyphenated form is the distribution and display name and
is the right one for this field.

### 8. Description (MANDATORY)
**Description:** sunkit-image is an open-source toolbox for solar physics image processing. It is an experimental library for solar physics specific image processing routines. The package contains image processing algorithms that have been published in the literature, including Multi-scale Gaussian Normalization (MGN), radial gradient filters (FNRGF, NRGF, RHEF), Automated Swirl Detection Algorithm (ASDA), Sunspot Tracking And Recognition Algorithm (STARA), granule segmentation, loop/structure tracing, image coalignment routines, time lag cross-correlation analysis, and Wavelets Optimized Whitening (WOW).

Carried over unchanged, and re-verified algorithm by algorithm against the pin rather than accepted
on trust. Each of the ten named capabilities exists as public API: MGN → `enhance.mgn`; FNRGF, NRGF
and RHEF → `radial.fnrgf`, `radial.nrgf`, `radial.rhef`; ASDA → `sunkit_image/asda.py`; STARA →
`stara.stara`; granule segmentation → `granule.segment`; loop/structure tracing → `trace.occult2`;
image coalignment → the `coalignment/` subpackage's `coalign_map`; time lag cross-correlation →
`time_lag`; WOW → `enhance.wow`. The middle two sentences track the project's own framing at
`README.rst:17-18`: "Currently this is an experimental library for solar physics specific image
processing routines." and "Ideally it will only contain routines that have been published in the
literature."

### 9. Concise Description (OPTIONAL)
**Concise Description:** An image processing toolbox for Solar Physics.

Carried over unchanged. It matches `pyproject.toml:11`,
`description = "An image processing toolbox for Solar Physics."`, and `README.rst:4`, byte for byte
including the trailing period.

**Do not "correct" this back toward its sources.** The GitHub repository description and the PyHC
registry entry both read "A image processing toolbox for Solar Physics" — grammatically wrong and
without the period. The stored value already carries the project's own corrected wording from
`pyproject.toml`; a later refresh that re-derives this field from the GitHub API or the PyHC registry
will appear to find a "difference" that is in fact a regression.

### 10. Publication Date (RECOMMENDED)
**Date:** 2017-11-01

Carried over unchanged. It is the GitHub repository creation date (`created_at`
`2017-11-01T18:30:22Z`), which is the earliest defensible public date for this software: the
repository predates both the first PyPI release and the first Zenodo deposit, and no earlier
publication of the package exists. The alternative candidates are all later and describe something
else — the Zenodo concept record's issue date describes the deposit, not the software's appearance.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Carried over unchanged. DataCite names Zenodo as the publisher on every record in this DOI family,
which is accurate: the archived releases are Zenodo deposits. The organization is stored with the
identifier `https://zenodo.org` and no ROR, matching how the catalogue records this publisher
generally.

### 12. Version (RECOMMENDED)

**Latest Version:**
- **Version Number:** v0.7.0
- **Version Date:** 2026-03-19
- **Version Description:** Breaking changes: Increased the minimum required versions — Python 3.12 (from 3.10), Matplotlib 3.8.0 (from 3.5.0), sunpy 7.0.0 (from 6.0.0), NumPy 1.26.0 (from 1.23.5), Astropy 6.1.0 (from 5.3.0), SciPy 1.12.0 (from 1.10.1). The previous coalignment API has been deleted and replaced with a new set of imports and functions.
- **Version PID:** https://doi.org/10.5281/zenodo.19338616

**This supersedes v0.6.1 (2025-02-20), which the record carried before this refresh.** v0.7.0 is a
real, ancestral release of the pinned tree, not a pre-release: tag `v0.7.0` is
`b2ffa56ab9abc4fcec01bef86ef73c102b6fd15a` and is an ancestor of the pin, and it is the newest
release of the package.

**The version number** takes the `v` prefix because that is what every authoritative source uses for
this release — the git tag, the GitHub release name, and DataCite's `version` field, all `v0.7.0` —
and because it matches the form of the value the record already held (`v0.6.1`).

**The date, 2026-03-19, is fixed by the record's own established convention, not by a judgement
call.** Four candidate dates exist for this release: the tag date (2026-03-19, both author and
commit date), the `CHANGELOG.rst` section heading `v0.7.0 (2026-03-19)` at line 1, the PyPI wheel
upload (2026-03-19), and the GitHub-release publication and Zenodo deposit creation (both
2026-03-30). The previously stored v0.6.1 date was 2025-02-20, which equals that release's tag date
and its CHANGELOG heading `0.6.1 (2025-02-20)` and is *not* its GitHub-release publication or its
Zenodo record date — so the convention in force on this record is the project's own release date.
For v0.7.0 that date is 2026-03-19, agreed independently by the tag, the changelog heading and the
PyPI upload. 2026-03-30 is the archiving date only, and choosing it would silently change the
convention mid-record.

**The description is an enrichment, not a replacement.** The v0.6.1 version the record carried
before this refresh had an **empty** description, so nothing is being overwritten and declining to
supply one would not be a removal. The value above is synthesized from the `CHANGELOG.rst`
`v0.7.0 (2026-03-19)` section (lines 1-17), which contains a Breaking Changes section and nothing
else — no features and no bug fixes were recorded for this release, which is why the value names
only breaking changes. (A note for anyone comparing files: a previous revision of this dossier
described a v0.6.1 version description mapping element-for-element onto that release's changelog
section. That text was the earlier dossier's own *proposed* value; the catalogue never held it.)
The upstream release notes were considered and rejected as a source: the GitHub release body for
both v0.7.0 and v0.6.1 is an auto-generated "What's Changed" list of pull-request titles and
contributor handles, not human-written notes, and would read poorly as catalogue prose.

**The version PID follows the record's own stored convention: a release-specific DOI, not the
concept DOI.** The v0.6.1 version the record carried before this refresh held
`https://doi.org/10.5281/zenodo.15619797`, which DataCite confirms is the v0.6.1 deposit
(`version` `v0.6.1`). The v0.7.0 analogue is the value above, whose DataCite record carries
`version` `v0.7.0`, title `sunpy/sunkit-image: v0.7.0`, and `IsVersionOf`
`10.5281/zenodo.5715430` — tying it to the concept DOI in Field 2 and confirming the two fields hold
the right ends of that relationship.

**Fields 2 and 12 deliberately hold the two ends of the version relationship, and that is worth
stating because they could in principle carry the same identifier.** The release-specific DOI above
identifies *this release*, which is what a version row is for, and it leaves Field 2 to identify the
software; it is also the convention the record already used for v0.6.1. Two alternatives were
considered and neither is used. The concept DOI `https://doi.org/10.5281/zenodo.5715430` never goes
stale, since it always resolves to the newest deposit, but it duplicates Field 2 and makes the
version row's identifier useless for pinning the release that row names. Recording no version PID at
all loses a citable identifier for the release for no gain.

### 13. Programming Language (RECOMMENDED)
**Languages:**
- Python 3.x

Carried over unchanged, and correct on both available tests. The form defines this field as "The
computer programming languages most important for the software." and instructs "Select the most
important languages (e.g., Python, Fortran, C). This is not meant to be an exhaustive list."
(`resource_submission_form_fields.md:308-310`), so it is not a catalogue of everything in the tree.
In any case Python is the only language present: of the 119 tracked files, 53 are Python and none is
a C, Fortran, IDL, Cython or MATLAB source.
`pyproject.toml:12` sets `requires-python = ">=3.12"`.

**The IDL evidence in this repository supports neither `IDL` here nor `IDL.sav` in Field 18.** It is
worth recording explicitly because a keyword search finds it easily and misreads it:

- `sunkit_image/data/test/IDL.txt` is a plain-ASCII file of float columns read only by
  `sunkit_image/tests/test_trace.py` as a regression reference. It is not an IDL `.sav` file; the
  name refers to the *provenance* of the reference numbers.
- `trace.py` discusses IDL because `occult2` is a Python port of Aschwanden's IDL OCCULT-2 code and
  keeps the original's memory layout for comparability — `trace.py:56-57` says the image "is
  transposed because IDL works column major and python is row major", so "the python and the IDL
  codes look similar". The port is validated against IDL output in the test suite. A port is not an
  IDL implementation.

A separate note that is an upstream inconsistency rather than a value question:
`pyproject.toml:12` requires Python 3.12 or newer, while `pyproject.toml:26-28` still carry
`Programming Language :: Python :: 3.10` / `3.11` / `3.12` classifiers. The changelog records the
floor moving to 3.12 "(from 3.10)", so the classifiers are stale. `Python 3.x` is right regardless.

### 14. Reference Publication (OPTIONAL)
**Reference Publication:** Not found

Deliberately empty, and this is negative research rather than an unfilled gap: **no paper describes
sunkit-image itself.** There is no JOSS paper, no `CITATION.cff` and no in-repo request to cite a
package paper; the Zenodo records' only related identifiers are the GitHub tree
(`IsSupplementTo`) and the concept DOI (`IsVersionOf`); and an ADS full-text search for the package
name surfaces no software-description paper for it. The SunPy Project paper
(`https://doi.org/10.3389/fspas.2023.1076726`) describes the ecosystem, not this package, and is
therefore not a reference publication for this entry.

What the package *does* have is a per-routine reference to the algorithm paper each function
implements — a different thing, handled under Field 27. If a sunkit-image package paper is ever
published, this is the field it belongs in.

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **SPDX Identifier:** BSD-2-Clause

Carried over unchanged. The declared licence is the one `pyproject.toml:15` points at,
`license-files = ["licenses/LICENSE.rst"]`, whose first line is
"Copyright (c) 2024, The SunPy Community"; GitHub's licence detection gives `spdx_id`
`BSD-2-Clause`, and all three DataCite records give `rights`
`BSD 2-Clause "Simplified" License` with `rightsIdentifier` `bsd-2-clause`. The stored value's
straight double quotes around `Simplified` are part of the vocabulary row name and must be preserved
exactly.

**No "License URI" is recorded, and none should be.** There is no per-software licence URI in this
catalogue: the licence is a shared row that carries its own `url`,
`https://spdx.org/licenses/BSD-2-Clause.html`. An earlier revision of this file recorded a
"License URI" of `https://opensource.org/licenses/BSD-2-Clause`, which was neither a storable field
nor the shared row's URL; it is removed rather than corrected.

**Third-party licence caveat — a fact about the package, not a change to this field.** The
`licenses/` directory also holds `LICENSE_ASDA.rst` (MIT, "Copyright (c) 2023 Jiajia Liu"),
`LICENSE_NOISE.rst` (a BSD-style licence, "Copyright (c) 2015, Masayuki Tanaka") and
`TEMPLATE_LICENSE.rst`, covering — per `licenses/README.rst` — "works the package is derived from,
and/or datasets." Those are the licences of incorporated third-party algorithm implementations
(`asda.py` and `utils/noise.py`); the package as distributed is BSD-2-Clause, so this field stays a
single value. The caveat is recorded because a future refresh scanning `licenses/` will find MIT
text and may mistake it for a licence change or a dual licence.

There is also a stale duplicate to be aware of: the top-level `LICENSE.rst` begins
"Copyright (c) 2013-2022 The SunPy Developers", an older copy that `pyproject.toml` does *not*
declare. `licenses/LICENSE.rst` is the declared one.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Keywords:**
- data analysis
- image analysis
- science
- solar
- solar physics

Carried over unchanged, and every one is traceable. Four come from the project's own declaration at
`pyproject.toml:14`, `keywords = ["solar physics", "solar", "science", "image analysis"]`. The
fifth, `data analysis`, comes from the PyHC community registry entry, whose
`keywords: ["solar", "general", "data_analysis"]` supplies it as an underscored tag; the catalogue
stores the de-underscored form.

**The stored spellings are lower-case.** The catalogue's display capitalises keywords, so a later
refresh that reads the rendered record will see "Solar Physics" and must not treat that as a
different value or re-submit the Title-Cased form. Keyword lookup is case-insensitive, so a case
variant binds the existing row rather than minting a new one, but the exact stored spelling is what
belongs in this file.

**Considered and rejected.** PyHC's third tag, `general`, is not stored and should not be: it
distinguishes nothing. New keywords for capabilities the record already expresses — image
processing, coalignment, sunspots, granulation, wavelets — were considered and rejected: this is the
one open vocabulary in the form, so each would mint a new row, and each duplicates something already
carried by Field 4 or stated in the description. GitHub repository topics were checked as a source
and the repository declares none.

### 17. Data Sources (OPTIONAL)
**Data Sources:** Not found — the software supports no data input source of its own.

Deliberately empty, and this is a positive finding rather than a gap. **sunkit-image retrieves no
data.** Its public functions take a `sunpy.map.GenericMap` or a bare array that the caller has
already obtained; there is no client, no downloader and no archive query anywhere in the package
API. This is the same fact that excludes "Data Access and Retrieval" from Field 4.

Two candidates were considered against the live vocabulary and rejected:

- **`The Virtual Solar Observatory.`** — rejected. The VSO does appear in the repository, but only
  in the example gallery and only through sunpy's downloader: `examples/finding_sunspots_using_stara.py:32`
  comments "Firstly, let's download HMI continuum data from the Virtual Solar Observatory (VSO)."
  and then calls `Fido.search`, while `examples/remove_cosmic_rays.py:33-35` sets
  `instrument = a.Instrument("LASCO")` and passes it to `Fido.search`.
  `Fido` is sunpy's client, imported from `sunpy.net`; the examples demonstrate how to *get* data to
  feed this package, not a capability this package provides. Recording it would tell a searcher
  filtering on VSO support that sunkit-image can query the VSO, which it cannot. (Note for whoever
  revisits this: the row name ends in a period — `The Virtual Solar Observatory.` — and the
  period-less form is rejected on submission.)
- **`Observatory/Mission-specific`** — rejected here, for the same reason: it describes where a
  package gets its data, and this package gets its data from its caller. The instrument and
  observatory associations that *are* evidenced belong in Fields 31 and 32, and the form's Field 17
  guidance links the two — "If observatory-specific, select 'observatory-specific' and indicate the
  observatory/mission name in the Related Observatory field" — so if the user selects observatory
  values in Field 32 on the strength of tuned defaults and fixtures, this row becomes worth
  re-examining. It is still not the right answer on today's evidence, because the tuned defaults do
  not amount to a data-input capability.

### 18. Input File Formats (RECOMMENDED)
**Formats:**
- FITS

Carried over unchanged and solidly evidenced. Every data fixture in the package is FITS —
`sunkit_image/data/test/` holds `aia_171_cutout.fits`, `asda_correct.fits`, `asda_vxvy.fits`,
`dkist_photosphere.fits` and `hmi_continuum_test_lowres_data.fits` — and all of them are read
through `sunpy.map.Map`, which is a FITS reader for these inputs. The gallery examples likewise
consume FITS files, whether downloaded (`examples/remove_cosmic_rays.py` opens the fetched file with
`astropy.io.fits`) or fetched from a URL (`examples/aligning_aia_with_eis_maps.py` builds maps
directly from two `.fits` URLs).

**Considered and rejected:**

- **`IDL.sav`** — rejected. `sunkit_image/data/test/IDL.txt` is plain ASCII, not an IDL save file;
  see Field 13 for the full disposal of the IDL evidence.
- **`ascii`** — rejected. `IDL.txt` is a regression reference read by the test suite, not a data
  format the API accepts; no public function reads text data.

### 19. Output File Formats (RECOMMENDED)
**Formats:**
- FITS

**`FITS` is kept, and the caveat on it has to be stated plainly: the package writes no files at
all.** That is the strongest finding in this field, and it qualifies the value rather than arguing
against it. Stated precisely: no public function in this package writes anything to disk. An
anchored search for write operations —
`\.(save|write|writeto|to_fits|savefig|to_csv|savez|dump)\s*\(` and `open\([^)]*['"]w` — returns
**zero** hits over `sunkit_image/**/*.py` excluding `tests/`, and zero over `examples/` and
`tests/` as well. Every public function returns an in-memory object instead: `enhance.mgn`,
`enhance.wow`, `radial.fnrgf`, `radial.intensity_enhance`, `radial.nrgf`, `radial.rhef`,
`stara.stara`, `trace.bandpass_filter`, `trace.occult2`, `trace.smooth`, `granule.segment`,
`granule.segments_overlap_fraction`, `coalignment.coalign_map`, the four `time_lag` functions and
`asda`'s eight functions all return a `sunpy.map.GenericMap`, a NumPy array, or a plain Python
value.

**Why the value is FITS regardless.** The products are FITS-shaped even though the write is the
caller's: the returned maps are constructed from the input's header or WCS and carry it forward
(`granule.py:77` builds `sunpy.map.Map(seg_im_markbp, smap.wcs)`, and `enhance.py:82` documents that
"If a map is input, a map is returned with new data and the same metadata."), and `sunpy`'s
persistence format for a `GenericMap` is FITS, so FITS is the format in which a sunkit-image product
is actually saved by anyone who saves one. `coalignment.coalign_map`'s entire deliverable is
corrected FITS *metadata* — a new reference coordinate written into the map header. A searcher
filtering for FITS-producing solar image tools would be right to expect this package back.

**The literal reading was examined and did not carry the field.** The form's Field 19 text is
narrower than the argument above: it defines the field as "The file formats the software supports for
data output." and instructs "Select all file formats your software supports for generated files.
Only formats actually supported should be indicated." Read literally, this package generates no
files, so nothing is supported and the honest value would be empty — with the FITS-serialisability
of its return values being a fact about sunpy rather than about sunkit-image. That reading is
preserved because it is a real reading of the form and a later refresh will arrive at it again from
the same evidence; it did not decide the field, because clearing the value would hide the package
from precisely the searchers it should reach.

Not an option either way: the previous revision of this file also proposed
"Image formats (PNG, JPEG, etc. via matplotlib)". That is dropped and should not return — those are
not rows in this controlled vocabulary at all, and the plotting is done by the example scripts, not
by the package.

### 20. Operating System (RECOMMENDED)
**Operating Systems:**
- Linux
- Mac
- Windows

Carried over unchanged, and directly evidenced by CI rather than inferred: `.github/workflows/ci.yml`
runs `- linux: py313` for the core job (line 42) and `- windows: py313`, `- macos: py313`,
`- linux: py312-oldestdeps` and `- linux: py314-devdeps` for the test job (lines 69-72), plus a
docs build and an online-test job on Linux. All three platforms are therefore tested on every push,
which is the strongest available support for this field.

**Considered and rejected: `Operating System Independent`.** `pyproject.toml:23` does classify the
package as `Operating System :: OS Independent`, and the vocabulary does contain a matching row. It
is rejected because the three named platforms are what a searcher actually filters on — a user
looking for Windows-capable software finds this entry under `Windows` and would not think to select
an "independent" facet — and because the named values assert something the CI proves, while the
classifier asserts only the maintainers' intent. The claims are not in conflict; the specific ones
are more useful.

### 21. CPU Architecture (RECOMMENDED)
**Architecture:** CPU Independent

Carried over unchanged. The package is pure Python: none of its 119 tracked files is a C, Fortran or
Cython source, `pyproject.toml`'s build system is plain `setuptools` with no extension modules, and
PyPI distributes it as a single `py3-none-any` wheel. There is no architecture-specific code to
constrain it.

**Considered and rejected:** `x86-64`, `Apple Silicon arm64` and `GPU`. Nothing in the package
targets a specific architecture, and the numerical work is delegated to dependencies that ship their
own per-architecture builds — which is a fact about those dependencies, not about this package.

### 22. Related Phenomena (OPTIONAL)
**Phenomena:**
- Coronal Heating
- Solar Corona
- Solar Flares

`Solar Corona` and `Solar Flares` were on the record before this refresh and both are retained.
**`Coronal Heating` is added**, and as with Field 5 this is enrichment rather than correction: the
vocabulary is flat and closed, so `Solar Corona` never implied `Coronal Heating`.

- **Coronal Heating** — `time_lag` exists to diagnose the heating and cooling of active-region
  corona. Its own reference block cites the two papers that define the method it implements:
  Viall & Klimchuk's "Evidence for Widespread Cooling in an Active Region Observed with the SDO
  Atmospheric Imaging Assembly" (`time_lag.py:88`) and "Appendix C in Barnes, W.T., Bradshaw, S.J.,
  Viall, N.M." / "Understanding Heating in Active Region Cores through Machine Learning. I.
  Numerical Modeling and Predicted Observables" (`time_lag.py:91-92`).
  `examples/calculating_time_lags.py` frames the result as "a proxy for the cooling time between
  two" channels (line 54) and as revealing "large scale patterns of cooling in images of the Sun"
  (line 92).
- **Solar Corona** — retained; see the coronal evidence collected under Field 5 (the `radial`
  filters, `trace.occult2`, `time_lag`, LASCO C2 coronagraph data).
- **Solar Flares** — retained, but with its evidentiary basis recorded honestly so that a future
  refresh does not waste effort hunting for a citation that does not exist. The string "flare"
  appears **nowhere** in the tracked tree (case-insensitive Perl-mode search over all 119 tracked
  files: zero hits). The value rests on use rather than on documentation: the AIA EUV enhancement
  filters, coronal-loop tracing and time-lag analysis this package provides are standard tools for
  flare and post-flare loop studies, and nothing in the package excludes flare data. A strict
  evidence-only reading of this field would drop it; the value is kept because it is a true statement
  about what the software is used for and because a searcher on the flare facet is better served by
  finding it than not.

**Considered and rejected:**

- **`Coronal Mass Ejections`** — rejected, and this is a correction of a proposal in the previous
  revision of this file rather than a removal from the record, which never held it. The phrase
  "coronal mass" and the standalone token `CME` do not occur anywhere in the tracked text; the only
  match in the whole repository is inside the binary FITS fixture `asda_vxvy.fits`, which is a
  velocity-field test array, not a CME reference. No module addresses CMEs.
- **`X-ray emission`** — rejected. No X-ray instrument, data product or wavelength is handled; the
  strings "x-ray" and "XRT" have zero hits in the tracked tree.
- **`Solar Wind`** and **`Geomagnetic Storms`** — rejected; this is an image-processing package for
  remote-sensing observations and touches neither.

### 23. Development Status (RECOMMENDED)
**Status:** Active

**The record held no development status at all before this refresh**, so this fills an empty
recommended field. `Active` is chosen against the live vocabulary's own definition — "The project has
reached a stable, usable state and is being actively developed." — both halves of which hold:
the package has a multi-year series of tagged releases published to PyPI, the newest being `v0.7.0`
(2026-03-19); the repository is not archived and the pinned revision is itself a commit dated
2026-09-09; and the PyHC registry rates the package `software_maturity: Good` and `python3: Good`.

**The tension worth addressing head-on**, because it is what makes this field look ambiguous:
`pyproject.toml:20` classifies the package `Development Status :: 3 - Alpha`, and `README.rst:17`
calls it "Currently this is an experimental library for solar physics specific image processing
routines." Those two statements suggest `WIP`. But `WIP`'s definition is a factual claim that is
false here — "Initial development is in progress, but there has not yet been a stable, usable
release suitable for the public." Public releases have been shipping for years, the package is a
SunPy-affiliated package installable from PyPI, and published science uses it. The
"experimental" framing describes the *routines'* research status (the project deliberately ships
newly published algorithms; see its Mission Statement under Field 27), not the absence of a usable
release, and the Alpha classifier is a stale default of the SunPy package template. `Concept`,
`Inactive`, `Unsupported`, `Suspended`, `Abandoned` and `Moved` are all excluded by the same release
history and current activity.

### 24. Documentation (RECOMMENDED)
**URL:** https://docs.sunpy.org/projects/sunkit-image

Carried over unchanged. This is the project's own declared documentation URL —
`pyproject.toml:72`, `Documentation = "https://docs.sunpy.org/projects/sunkit-image"` — and the PyHC
registry gives the same short form as `docs:`. It resolves, via one redirect, to the versioned
stable path.

**Considered and rejected:** the fully-qualified
`https://docs.sunpy.org/projects/sunkit-image/en/stable/`, which is the form `README.rst:20` links.
The short form is preferred because it is what the project declares as canonical and because it is
version-path-agnostic: it survives a change in the docs host's language or version routing, which
the `/en/stable/` form would not.

### 25. Funder (OPTIONAL)
**Funder:** Not found

Deliberately empty, with the negative research recorded so it need not be repeated. Four independent
places where funding would appear were checked and all are empty:

- DataCite `fundingReferences` is `[]` on all three records — the concept DOI, `v0.7.0` and
  `v0.6.1`.
- No funding, grant or acknowledgement text exists in `README.rst`, under `docs/`, or in
  `pyproject.toml`.
- There is no package paper (Field 14), so there is no Acknowledgements section or Data Availability
  Statement to mine — which is normally the best source for this field.
- `NumFOCUS` appears only as a README badge (`README.rst:6`, defined at `README.rst:14-15`, linking
  `http://numfocus.org`). "Powered by NumFOCUS" is a project-affiliation badge for the SunPy
  Project, not a grant to sunkit-image, and it names no award.

The absence is consistent with what this package is: an algorithm library contributed to by many
volunteers and by SunPy maintainers whose own funding is recorded on their institutions and on the
sunpy core entry, not on this one.

### 26. Award Title (OPTIONAL)
**Award:** Not found

Deliberately empty, for the same reason and on the same evidence as Field 25: no funding reference
exists on any Zenodo/DataCite record for this software, and no award number or title appears anywhere
in the repository. An award cannot be recorded without a funder in any case, and this field must not
be populated speculatively from a maintainer's grants — those belong to whatever software those
grants actually funded.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Publications:**
- https://doi.org/10.1051/0004-6361/202245345 — Auchère et al. 2023, "Image enhancement with wavelet-optimized whitening", *A&A* 670, A66
- https://doi.org/10.1007/s11207-023-02183-w — Seaton et al. 2023, "The SWAP Filter: A Simple Azimuthally Varying Radial Filter for Wide-Field EUV Solar Images", *Solar Physics* 298, 92
- https://doi.org/10.3389/fspas.2023.1076726 — Barnes et al. 2023, "The SunPy Project: An interoperable ecosystem for solar data analysis", *Frontiers in Astronomy and Space Sciences* 10
- https://doi.org/10.1007/s11207-025-02578-x — Gilly & Cranmer 2025, "Visualization of High Dynamic Range Solar Imagery and the Radial Histogram Equalizing Filter", *Solar Physics* 300, 174
- https://doi.org/10.1051/0004-6361/202555618 — Zhu et al. 2025, "Active region upflows in various coronal structures and their coupling to the lower atmosphere", *A&A* 701, A205
- https://doi.org/10.3847/1538-4357/adccc8 — Lörinčík et al. 2025, "Probing Progression of Heating Through the Lower Flare Atmosphere via High-cadence IRIS Spectroscopy", *ApJ* 986, 73
- https://doi.org/10.1093/mnras/stag1416 — Adithya H. N. et al. 2026, "Multiwavelength diagnostics of pre-flare evolution with Aditya-L1: from the solar chromosphere to the corona", *MNRAS* 551
- https://doi.org/10.1016/j.newast.2026.102554 — Shirke et al. 2026, "Analysis of solar flare and sunspots on 4th Jan 2025 and their effects on space weather", *New Astronomy* 126, 102554
- https://doi.org/10.1051/0004-6361/202557009 — Nölke et al. 2026, "Magnetic structure of coronal dark halos", *A&A* 709, A108

**The record held no related publications before this refresh.** The nine values above are the
papers that use the package, scoped to refereed articles carrying a publisher DOI. Two well-defined
populations were available and both are enumerated in this field. They are not disjoint, which is
why less turned on the choice between them than the framing suggests: Auchère et al. 2023 and
Gilly & Cranmer 2025 belong to both, and both are recorded above.

**How the recorded set was derived — worth recording, because this population is not re-derivable
from the repository.** It comes from an ADS full-text search for the package name in both of its
spellings, hyphenated and underscored (`sunkit-image` and `sunkit_image`), measured on 2026-09-09,
when it returned 16 records. The method and the date are here so that a later refresh can re-run the
same search instead of reconstructing the criterion. The record count is a dated measurement only:
it will be larger next time, and no claim in this field depends on it.

**One of the nine acknowledges the package by name.** Zhu et al. 2025
(`https://doi.org/10.1051/0004-6361/202555618`) names sunkit-image in its Acknowledgements section.
An ADS acknowledgements search — `ack:"sunkit-image"` and `ack:"sunkit_image"` — returned that one
record and no other for either spelling when measured on 2026-09-09. That route is worth recording
separately from the full-text search above, because it is narrower and answers a different
question: an acknowledgement is the strongest statement of use a paper can make about itself,
whereas a full-text hit can be a passing mention. The count is a dated measurement of an index we
do not control and will change; the durable facts are the route and this attribution. The row is
already recorded on the full-text evidence, so this adds attribution rather than a value.

**A later refresh will get back more records than there are values here, and nothing will have gone
missing.** Every difference between the search result and the recorded set is a mechanical exclusion:

- **Two records are sunkit-image's own Zenodo software deposits** (v0.5.0 and v0.4.2). Those are the
  software, not publications about it; the software's own identifiers belong to Fields 2 and 12.
- **One record is a funding proposal and one a meeting abstract** — a 2021 proposal for
  feature-extraction tools for solar remote-sensing observations, and a 2018 AGU abstract on the
  SunPy ecosystem. Neither carries a DOI, so neither could be recorded as a related item even if it
  counted as a publication for this field.
- **One arXiv eprint is the preprint of an article already in the set.** The Adithya H. N. Aditya-L1
  paper appears twice: as `https://doi.org/10.48550/arXiv.2607.26171` and as the MNRAS version of
  record `https://doi.org/10.1093/mnras/stag1416`, which is the one recorded. The duplication is
  easy to miss, because ADS parsed the first author's name two ways so the two records carry
  different bibcodes, and because the preprint's title is capitalised differently from the journal
  version's ("Multi-Wavelength ... From the Solar Chromosphere ..." against
  "Multiwavelength ... from the solar chromosphere ...").
- **Two arXiv-only preprints were considered and excluded**: Dresing et al., "Comprehensive solar
  eruption analyses enabled by the tools of the SOLER project", and De-Sassi et al., "Exploring if a
  coronal dimming event can produce coronal hole-like properties". Both use the package and both
  would be legitimate additions once published; they are out because the recorded population is
  scoped to refereed articles with a publisher DOI. The reason is worth keeping, because it is the
  same trap as the bullet above — a preprint recorded today becomes a second row for the same work
  once the refereed version appears, and nothing in the catalogue flags the pair.
- **Several records carry both a publisher DOI and an arXiv DOI.** The publisher DOI is the one
  recorded, in every case.

**The consequences each way, which is what the population was chosen on.** (A) is stable, complete,
bounded by the repository, and re-derivable at any later pin — but it credits *other people's
algorithm papers* under this software's record, and several of them (the noise-estimation IEEE
papers, the vortex-identification fluid-dynamics paper) are not heliophysics literature at all. (B)
describes the software's scientific impact and is what a bibliometric reader expects — but it grows
without bound, goes stale between refreshes, and cannot be re-derived from the repository; a
citation list is also non-discriminating, in that most catalogue entries could accumulate one.

The recorded population is (B). Its costs above are accepted with their mitigations stated: the
staleness and the non-derivability are answered by recording the search method and its date, and the
scope to refereed articles carrying a publisher DOI bounds what the field's "describe, cite, or use"
is allowed to admit. The costs on the other side are the ones just named — (A) would fill this field
with other people's algorithm papers, several of them outside heliophysics, under sunkit-image's own
record.

**The algorithm papers the package implements — examined as a candidate population for this field
and not chosen.** This is the population the project itself privileges, and it does so unusually
explicitly: sunkit-image's admission criterion *is* publication. Its Mission Statement requires
that routines "Are published in the literature or in preparation to be published."
(`docs/index.rst:35`), adding that where publication status is in doubt "the code will only be
merged when it's close to actual publication" (`docs/index.rst:36`), and `README.rst:18` states
"Ideally it will only contain routines that have been published in the literature." Every routine
accordingly carries a reference block naming its paper. For a searcher, these are the papers that
explain what the software *does* and that a user of a given routine must read and cite.

**The gate, re-derived from this software's own evidence.** The submission form's definition of
Field 27 admits publications that "describe, cite, or use" the software, so both populations clear
that hurdle and the case turned on the qualifier — the publications "the software developer
prioritizes". sunkit-image expresses a publication priority in exactly two places, both inside the
repository: the Mission Statement's admission criterion, which requires that routines "Are published
in the literature or in preparation to be published." (`docs/index.rst:35`), restated in
`README.rst:18` as "Ideally it will only contain routines that have been published in the
literature."; and the per-routine reference block that every routine carries, tabulated below.
Nothing in the repository nominates population (B)'s criterion. That points at (A), but two
repo-internal facts keep the case from being as strong as it first looks:

- **The project asks users to cite nothing, itself included.** There is no `CITATION.cff`, no
  `.zenodo.json`, no `references:` block and no acknowledgement page anywhere in the tracked tree at
  the pin. What the reference blocks actually do is attribute prior art the code implements — they
  tell a reader where an algorithm came from — and the Mission Statement is a merge condition on new
  routines. Neither is a request that a user of sunkit-image cite those papers. So the step from
  "publication is a membership condition for routines" to "these are the developer's prioritised
  publications" is an inference this file is making, not a priority the project states, and it is
  weaker than the same conclusion would be in a project that ships a citation file naming its
  references.
- **The two populations are not cleanly separable here.** Auchère et al. 2023 falls in both. Gilly &
  Cranmer 2025 falls in both more strongly: it is the RHEF paper `radial.py:704` cites as
  "* Gilly & Cranmer 2024, in prep.", its first author is stored author 9 of this software, and it
  is also one of the papers that uses the package. Any option admitting it on population-(A) grounds
  therefore also admits the best-evidenced member of population (B), which means less turns on the
  either/or than the framing suggests.

On this software's own evidence, (A) remains the better-supported reading of *prioritizes* and (B)'s
criterion has no repository nomination behind it; the honest statement of the case is that (A) rests
on an admission criterion rather than on a citation request.

That analysis is preserved as it stood. The population recorded above was settled on the
consequences set out earlier and not by finding this reading of *prioritizes* wrong, so a later
refresh reopening Field 27 should start from it rather than rebuild it.

**The candidate population in full, each DOI bound to the file that carries it at the pin.** It is
kept whole because every row is durable evidence about the package whichever population this field
holds:

| Routine | Paper | DOI | Cited at |
|---|---|---|---|
| `enhance.mgn` | Morgan & Druckmüller 2014, MGN | https://doi.org/10.1007/s11207-014-0523-9 | `enhance.py:89` |
| `enhance.wow` | Auchère, Soubrié, Pelouze & Buchlin 2023, WOW | https://doi.org/10.1051/0004-6361/202245345 | `enhance.py:260` |
| `radial.nrgf` | Morgan, Habbal & Woo 2006, NRGF | *no DOI given in repo*; link is https://link.springer.com/article/10.1007%2Fs11207-006-0113-6 | `radial.py:314` |
| `radial.fnrgf` | Morgan, Habbal & Druckmüllerová 2011, FNRGF | *no DOI given in repo*; link is https://iopscience.iop.org/article/10.1088/0004-637X/737/2/88/pdf | `radial.py:510` |
| `radial.rhef` | Gilly & Cranmer, RHEF — cited as "in prep.", now published (see below) | https://doi.org/10.1007/s11207-025-02578-x | `radial.py:704` |
| `stara.stara` | Watson & Fletcher 2010, STARA (IAU Proc. S273) | https://doi.org/10.1017/S1743921311014992 | `stara.py:63` |
| `stara` (docs page) | **a mis-citation** — Watson, Fletcher, Dalla & Marshall 2009, on sunspot-emergence asymmetry, not on STARA | https://doi.org/10.1007/s11207-009-9420-z | `docs/code_ref/stara.rst:5` |
| `trace.occult2` | Aschwanden, De Pontieu & Katrukha 2013, OCCULT-2 | https://doi.org/10.3390/e15083007 | `trace.py:52` |
| `time_lag` | Viall & Klimchuk 2012 | https://doi.org/10.1088/0004-637X/753/1/35 | `time_lag.py:90` |
| `time_lag` | Barnes, Bradshaw & Viall 2019 (Appendix C) | https://doi.org/10.3847/1538-4357/ab290c | `time_lag.py:94` |
| `utils.calculate_gamma` | Graftieaux, Michard & Grosjean 2001 | https://doi.org/10.1088/0957-0233/12/9/307 | `utils/utils.py:298` |
| `asda` | Liu, Nelson & Erdélyi 2019, ASDA | https://doi.org/10.3847/1538-4357/aabd34 | `utils/utils.py:303`, `docs/code_ref/asda.rst:5` (as an ADS link), `examples/detecting_swirls.py:8` |
| `utils.noise` | Liu, Tanaka & Okutomi, ICIP 2012 | https://doi.org/10.1109/ICIP.2012.6466947 | `utils/noise.py:69` |
| `utils.noise` | Liu, Tanaka & Okutomi, IEEE Trans. Image Proc. 2013 | https://doi.org/10.1109/TIP.2013.2283400 | `utils/noise.py:74` |
| `granule` (constant) | brightpoint size limit justified by an inline "(see doi 10.3847/1538-4357/aab150)" | https://doi.org/10.3847/1538-4357/aab150 | `granule.py:204` |

The table divides in a way worth keeping, since it is the natural first cut if this population is
ever revisited: the headline algorithms named in the Field 8 description — MGN, WOW, NRGF, FNRGF,
RHEF, ASDA, STARA, OCCULT-2 and the time-lag pair — as against the references that support an
implementation detail rather than a named capability, namely the two IEEE noise papers, the
fluid-dynamics Graftieaux paper and the inline `granule` constant reference.

**Five facts that outlast the choice, and that a later refresh reopening this field will need:**

1. **Two references carry no DOI in the repository.** NRGF (2006) and FNRGF (2011) are cited by
   publisher link only. Both DOIs are nonetheless recoverable from those links —
   `10.1007/s11207-006-0113-6` and `10.1088/0004-637X/737/2/88` — but the repository does not state
   them, so recording them means resolving them from the URL rather than copying a cited value.
2. **`stara` is cited under two different DOIs by the project, and one of them is wrong.** The
   docstring at `stara.py:61-63` cites "Automated sunspot detection and the evolution of sunspot
   magnetic fields during solar cycle 23", Watson & Fletcher, Proc. IAU
   (`https://doi.org/10.1017/S1743921311014992`) — the paper that describes the algorithm. The docs
   page at `docs/code_ref/stara.rst:5` hangs the link text naming the STARA algorithm on
   `https://doi.org/10.1007/s11207-009-9420-z`, which resolves to a different work: Watson,
   Fletcher, Dalla & Marshall (2009), "Modelling the Longitudinal Asymmetry in Sunspot Emergence:
   The Role of the Wilson Depression", *Solar Physics*, which is not about STARA. Both are Watson &
   Fletcher papers, which is exactly why the slip reads as correct at a glance. **Record the
   docstring DOI; do not import the docs one.** The durable lesson for a later refresh: a rule of
   the form "use the DOI each docs page cites" would silently import the wrong paper here. A minor
   related trap: `stara.py` dates its paper 2010 (the symposium) while the proceedings volume is
   2011 — say which if a year is asserted. The same docs-versus-docstring split affects ASDA
   harmlessly: `docs/code_ref/asda.rst:5` links an ADS abstract page where a DOI exists, and the
   DOI form cited in `utils/utils.py:303` is the one to record.
3. **The RHEF reference in the code is stale, and this is a durable finding.** `radial.py:704` reads
   "* Gilly & Cranmer 2024, in prep." That paper is now published: Gilly & Cranmer, "Visualization of
   High Dynamic Range Solar Imagery and the Radial Histogram Equalizing Filter", *Solar Physics* 300
   (2025), https://doi.org/10.1007/s11207-025-02578-x. The first author is stored author 9 of this
   software. So RHEF's reference exists as a real publication even though the in-repo docstring
   predates it, and this is recorded here regardless of which population is chosen — a future
   refresh reading only `radial.py` would otherwise conclude the paper does not exist.
4. **The `granule` constant's paper is not by the ASDA author, and names an instrument that is
   not relevant to Fields 31-32.** `https://doi.org/10.3847/1538-4357/aab150` is "Studies of
   Isolated and Non-isolated Photospheric Bright Points in an Active Region Observed by the New
   Vacuum Solar Telescope" by Yanxiao Liu, Yongyuan Xiang, Robertus Erdélyi and six co-authors. The
   shared surname Liu and the shared co-author Erdélyi make it easy to confuse with the ASDA paper;
   **Jiajia Liu is not an author of it**. It is cited only in an inline comment justifying a
   0.1 square-arcsecond size constant, so the New Vacuum Solar Telescope is *not*
   designed-to-support evidence for Fields 31 or 32 — but the constant being a photospheric
   bright-point size does corroborate Field 5's `Photosphere`.
5. **Four cited items are not publications and are candidates for nothing.** Two doctoral theses —
   Druckmüllerová's, on adaptive filtering of coronal images (`radial.py:513`), and Gilly's 2022
   thesis (`radial.py:708`, also `examples/radial_histogram_equalization.py:48`) — plus a Harris
   Geospatial IDL documentation page and a StackOverflow answer cited for a smoothing implementation
   (`trace.py:272-273`), and a Wikipedia article on the convolution theorem (`time_lag.py:86`).
   Theses are not journal publications and the rest are implementation notes; none belongs in this
   field.

### 28. Related Datasets (OPTIONAL)
**Datasets:** Not found

Deliberately empty. The software ships no dataset and cites none as a citable resource:

- The two version-specific Zenodo/DataCite records this file discusses each carry exactly two
  related identifiers — `IsSupplementTo` the GitHub tree and `IsVersionOf` the concept DOI. The
  concept record `10.5281/zenodo.5715430` is structured differently and must be counted separately:
  it carries `IsSupplementTo` the GitHub tree plus one `HasVersion` relation per released deposit,
  and no `IsVersionOf` at all, because it is the target of those version relations rather than their
  source (Field 2 records the same structure). The conclusion holds across all three records
  regardless: not one of their relations is a dataset relation of any kind.
- The five FITS fixtures in `sunkit_image/data/test/` are small test inputs shipped inside the
  package, not a published dataset with an identifier.
- The larger sample files the gallery uses are fetched by URL from the SunPy project's `sunpy/data`
  GitHub repository (for example the EIS raster and AIA image in
  `examples/aligning_aia_with_eis_maps.py:25-37`) or downloaded live from the VSO. Those are
  convenience stores of example files, not citable datasets, and the VSO products belong to their
  missions rather than to this software.

### 29. Related Software (OPTIONAL)
**Software:**
- https://github.com/sunpy/sunpy — sunpy, the core package this one extends
- https://git.ias.u-psud.fr/fauchere/wavelets — watroo, the reference implementation of the WOW algorithm

**The sunpy entry changes form, not substance.** Before this refresh the record pointed at sunpy by
its Zenodo concept DOI, `https://doi.org/10.5281/zenodo.591887`. It is rewritten as sunpy's exact
stored repository URL, `https://github.com/sunpy/sunpy`, for two reasons: the catalogue renders a
related item's raw URL as the link's visible text, so a DOI displays as an opaque identifier where
the repository URL displays legibly; and naming another catalogue entry by the repository URL it
actually stores is the campaign convention, which keeps the two entries' cross-references
symmetrical. The relationship itself is not in doubt — `pyproject.toml:37` makes
`sunpy[map]>=7.0.0` a hard dependency, and sunkit-image exists to extend it.

**watroo is added.** It is a domain-specific optional dependency, not infrastructure:
`pyproject.toml:43` declares the `watroo` extra; `enhance.py:263` imports it inside `wow`
(`from watroo import B3spline, utils`) and `enhance.py:265` raises "The `watroo` package is required
to use the `wow` function." if it is missing; and `CHANGELOG.rst:86` records the feature as
"the ability to call a Wavelets Optimized Whitening (WOW) algorithm" drawn from the watroo
package. It is
the author's own reference implementation of the WOW algorithm — the same Frédéric Auchère who is
stored author 6 of this software and first author of the WOW paper — so `enhance.wow` is a thin
wrapper over it, and a user who wants WOW must install it.
On the URL: watroo has no DOI, which this field would otherwise prefer, and it is not a catalogue
entry, so a repository URL is required. Two exist. The one recorded above is the homepage the PyPI
distribution itself declares — an IAS GitLab instance under the author's own account — and it is
preferred because it is the project's own statement of where its code lives, requiring no inference.
The alternative is the author's GitHub repository `https://github.com/frederic-auchere/wavelets`,
whose identity as watroo rests on inference (the account and the à-trous wavelet subject matter)
rather than on a declaration. Its argument is durability: `u-psud.fr` is a legacy institutional
domain, so if the GitLab URL ever stops resolving, that GitHub repository is the fallback — and a
DOI, should watroo ever get one, would supersede both. `CHANGELOG.rst:86` links only the PyPI
project page, which is not a code repository.

**Considered and rejected — policy exclusions.** An earlier revision of this file proposed numpy,
scipy, matplotlib and scikit-image here. All four are excluded by the form's Tier A rule
(`resource_submission_form_fields.md:690`, extended to this field at line 698): they are the generic
scientific-Python stack, being a dependency is not a relationship worth recording, and the claim
would be equally true of most of the catalogue. This is policy, not curatorial taste, and it should
not be revisited entry by entry. Note that **nothing is being removed from the record here** — the
catalogue has never stored any of them for this software; only a proposal in a working file is being
dropped.

**Also considered and rejected:**

- **astroscrappy** — a docs-only extra (`pyproject.toml:59`) used by a single example
  (`examples/remove_cosmic_rays.py`) to remove cosmic-ray hits from a LASCO image. Astronomy-specific,
  but nothing in the package's own API touches it, and an example's import is not a relationship
  between the two packages.
- **eispac** — named at `examples/aligning_aia_with_eis_maps.py:22` only as the provenance of a
  pre-prepared sample raster: "This raster image was prepared using the
  `eispac <https://eispac.readthedocs.io/en/latest/>`__ package." The
  example does not call it; the file was prepared elsewhere and is downloaded ready-made.

### 30. Interoperable Software (OPTIONAL)
**Software:**
- https://github.com/sunpy/sunpy — sunpy: shared `GenericMap` data model, in and out
- https://github.com/sunpy/pyflct — pyflct: produces the velocity field that `asda` consumes
- https://github.com/dask/dask — dask: `time_lag` accepts and returns Dask arrays as a documented type

**sunpy** was already recorded (as its concept DOI) and is rewritten to its exact stored repository
URL for the reasons given in Field 29. The interoperation is as strong as this field gets: the
package's public functions take and return `sunpy.map.GenericMap` objects, `utils/decorators.py`
exports an `accept_array_or_map` decorator whose whole purpose is to let every routine accept either
a bare array or a map and return the same kind, `coalignment.coalign_map` consumes two maps and
returns a corrected one, and `granule.segment` returns a map it has attached plot settings to. The
shared data model is the interoperation.

**pyflct is added.** `asda` needs a two-dimensional velocity flow field as input, and the project's
own gallery says where to get one: `examples/detecting_swirls.py:29` states
"`pyflct <https://pyflct.readthedocs.io/en/latest/>`__ is a good tool to calculate the velocity field
from your data." — with the example itself falling back on a precomputed fixture because,
as its docstring says, "Unfortunately, currently ASDA within sunkit-image only works on arrays."
(`examples/detecting_swirls.py:10`). That is one package's output being fed into the other, documented
by the project, and pyflct is a catalogue entry in its own right, stored under exactly
`https://github.com/sunpy/pyflct`. The counter-argument, recorded honestly: the recommendation is a
single documentation comment and there is no adapter or converter — the user passes arrays by hand.
It is included because the exchange is real, specific and useful to a searcher on either side; a
future curator who disagrees should read that caveat rather than assume the evidence was thin.

**dask is added, and it is the one Tier B inclusion here.** The form permits dask only with a
specific documented exchange, and this package has one: `time_lag.py:5-9` imports `dask.array`
optionally "so that Dask is not a hard requirement"; `time_lag.py:143-160` contains a dedicated
`_dask_check` code path whose comment explains that "In order for the time lag to be returned as a
Dask array, the lags array," must also be one; `time_lag.py:215` documents the accepted array types
as "or `~dask.array.Array` object."; the test suite asserts that the returned objects are
`dask.array.Array` instances; and `examples/calculating_time_lags.py:131-138` demonstrates the
intended use, that "All of these operations can be parallelized and distributed" by "passing in the
intensity cubes as Dask arrays". So Dask arrays are a documented interchange type of the public API,
in and out — not an internal implementation detail. The counter-argument is that dask is generic
parallel-array infrastructure rather than a heliophysics peer tool; it is included because the form
lists dask as admissible on cited evidence and this is exactly the kind of evidence named, and
because the fact tells a searcher something true and useful (this package's time-lag analysis scales
to out-of-core data cubes).

**Considered and rejected: ndcube.** This is the most finely balanced exclusion in the file, and the
reasoning is recorded so it is not re-litigated blindly. In favour: `docs/index.rst:40` states "If
the code is already in a released package, we will wrap calls to the existing package in a way that
makes it easy to use with `sunpy.map.Map` or `ndcube.NDCube` objects." — a documented statement
naming NDCube — and `docs/conf.py:108` carries an intersphinx mapping for ndcube. Against, decisively:
the sentence is a forward-looking policy about how *future* wrapped code will be written, not a claim
about today's API; no public function accepts, returns or converts an `NDCube`; and an intersphinx
mapping is a documentation cross-reference facility, carried here by the SunPy package template, not
an exchange. A case-insensitive search of the whole tracked tree for "ndcube" returns exactly three
hits: those two `docs/` lines and `.codespellrc:29`. **That third hit is a trap worth naming.**
`.codespellrc` lines 21-34 are an `ignore-words-list` — spellings the spell-checker should not flag —
and it contains `NDCube`, `EIS`, `eis`, `EIT` and `eit`. A sweep that includes that file will mint
false evidence for ndcube interoperability and, worse, for SOHO's EIT instrument, which this package
does not touch at all. No claim anywhere in this file rests on `.codespellrc`.
A searcher arriving from ndcube's entry would find no way to use the two together today. If a routine
ever gains NDCube support, this becomes a straightforward addition.

**Considered and rejected: astropy.** The package does exchange astropy objects — public signatures
are `@u.quantity_input`-decorated and take and return `astropy.units.Quantity` values, and the FITS
and WCS handling is astropy's underneath sunpy. It is excluded because that exchange is with astropy
as the foundation *beneath* this package's actual data model rather than with a peer tool a user
would deliberately combine with it; the documented interchange object of this package is
`sunpy.map.GenericMap`, and sunpy is already recorded. Listing astropy would also be equally true of
essentially every solar and astronomical Python package, which is the form's own test for a claim
that carries no information.

**Considered and rejected: the rest of the ecosystem by name.** aiapy, sunkit-instruments, sunraster,
irispy, XRTpy and fisspy are all catalogue entries in this same domain, and a "SunPy ecosystem"
argument would sweep them all in. Every one of them has **zero** mentions anywhere in the tracked
tree, and ecosystem membership is explicitly not sufficient. numpy, scipy, matplotlib and
scikit-image are Tier A exclusions exactly as in Field 29 — scikit-image is worth naming
specifically, since the package uses it heavily (`granule`, `stara`, `asda`, `coalignment` all call
`skimage`), and heavy internal use is still not interoperability.

### 31. Related Instruments (OPTIONAL)
**Instruments:**
- Atmospheric Imaging Assembly — https://spase-metadata.org/SMWG/Instrument/SDO/AIA
- HMI — https://spase-metadata.org/SMWG/Instrument/SDO/HMI

**The record held no instruments before this refresh; two of four resolvable candidates are
recorded.** All four resolve cleanly against the controlled vocabulary and they differ sharply in
strength, so this was never a gap in evidence. Because sunkit-image's public API is deliberately
instrument-agnostic, it was a judgement about what serves a searcher, tested on each candidate by
asking whether a visitor on that instrument's page, asking to see software related to it, would be
glad or annoyed to be shown sunkit-image. The two recorded rows are the two whose support is
concrete in tuned defaults and packaged fixtures rather than resting on a worked example. Each entry
below gives the verbatim vocabulary row name and its SPASE identifier, in the order they were
assessed, strongest first.

**Recorded.**

1. **Atmospheric Imaging Assembly** — `https://spase-metadata.org/SMWG/Instrument/SDO/AIA`
   *Strongest.* AIA is the package's de facto reference instrument. Eight of the twelve gallery
   examples work on AIA data (`advanced_wow`, `aligning_aia_with_eis_maps`, `calculating_time_lags`,
   `multiscale_gaussian_normalization`, `radial_gradient_filters`, `radial_histogram_equalization`,
   `rgb_composite`, `watroo_wow`); the packaged fixture `sunkit_image/data/test/aia_171_cutout.fits`
   carries `TELESCOP` `SDO/AIA`, `INSTRUME` `AIA_3`, `ORIGIN` `SDO/JSOC-SDP` and `WAVELNTH` 171 in
   its compressed-image HDU; `time_lag.py:175` explains the physics in AIA's terms ("on AIA, the time
   lag is the lag which maximizes the cross-correlation"); `utils/utils.py:143-144` uses AIA as its
   worked example of a length scale; `coalignment/tests/test_coalignment.py:27-33` builds a map from a hosted AIA
   level-1 file; and `CHANGELOG.rst:98` records RHEF being improved "to work with images outside of SDO/AIA",
   which is direct evidence that the routine was AIA-specific before. A searcher on the AIA page
   would be glad to find an AIA-focused image-enhancement toolbox.
2. **HMI** — `https://spase-metadata.org/SMWG/Instrument/SDO/HMI`
   *Strong.* HMI is not merely exemplified, it is baked into `stara`'s defaults:
   `stara.py:45` documents "The default value of 6000, is a reasonable value for HMI continuum" and
   `stara.py:50` warns about "detections around the limb with HMI continuum images". The sunspot
   example downloads HMI continuum from the VSO
   (`examples/finding_sunspots_using_stara.py:34`, `a.Instrument("HMI")` with
   `a.Physobs("intensity")`), and the packaged fixture
   `hmi_continuum_test_lowres_data.fits` has `WAVELNTH` 6173.0, the HMI continuum wavelength. Tuned
   default parameters are the strongest form of "designed to support" short of a dedicated reader.

**Examined and not recorded.**

3. **EUV Imaging Spectrometer** — `https://spase-metadata.org/SMWG/Instrument/Hinode/EIS`
   *Middling.* An entire gallery example is devoted to it: `examples/aligning_aia_with_eis_maps.py`
   is titled "Coaligning EIS to AIA" (line 3) and exists, in its own words, to show how "to coalign
   EIS rasters to AIA images" (line 6) so as to correct EIS's pointing uncertainty; the coalignment
   test suite pairs an EIS raster fixture with a time-matched AIA one
   (`coalignment/tests/test_coalignment.py:20-33`). Against: the coalignment code itself is generic — nothing in it knows about EIS — and
   the example's EIS file was prepared with a different package. Note also that the word "Hinode"
   appears nowhere in the tracked tree; only "EIS" does, so associating this row also asserts the
   platform identification, which the vocabulary supplies rather than the repository.
4. **Large Angle Spectroscopic Coronagraph** — `https://spase-metadata.org/SMWG/Instrument/SOHO/LASCO`
   *Middling-to-weak.* `examples/remove_cosmic_rays.py:6` demonstrates "how to remove cosmic ray hits
   from a LASCO C2 FITS file", downloading it via `a.Instrument("LASCO")` with `a.Detector("C2")`
   (lines 33-35). But the cosmic-ray removal is done by astroscrappy, not by this package, and no
   sunkit-image routine is LASCO-specific. This is the example most vulnerable to the "configurable
   for / commonly used with" exclusion.

**Resolution notes that matter whether or not a row is recorded:**

- Each of the four resolves to **exactly one** vocabulary row by identifier, so there is no ambiguity
  to flag and no `NEEDS MANUAL RESOLUTION` case here.
- **`AIA` is not unique in the vocabulary** and this is a live trap: a text match on `AIA` also
  hits three Argentine Islands rows. Two of them carry `AIA` as their abbreviation —
  `https://spase-metadata.org/IUGONET/Observatory/WDC_Kyoto/WDC/AIA` and
  `https://spase-metadata.org/IUGONET/Instrument/WDC_Kyoto/WDC/AIA/Magnetometer`. The third, a
  station-code row at `https://spase-metadata.org/SMWG/Observatory/Ground/Faraday.Islands`, has an
  **empty** abbreviation and collides through its name instead, which is why the warning has to be
  about text matching generally and not about the abbreviation field alone. The solar instrument is
  identified by its identifier `https://spase-metadata.org/SMWG/Instrument/SDO/AIA`, never by name
  or abbreviation.
- **`HMI`'s row name is the bare abbreviation** — the row is literally named `HMI`, with an empty
  abbreviation field — so it must be written exactly that way and not expanded to "Helioseismic and
  Magnetic Imager".
- **`EIS` also collides**: four MMS energetic-particle rows are named `MMS EIS`. The Hinode
  spectrometer is `https://spase-metadata.org/SMWG/Instrument/Hinode/EIS`.

**Evidenced absent — do not re-propose these.** `EUI`, `STEREO`, `SECCHI`, `EUVI`,
`Solar Orbiter`, `IRIS`, `GOES`, `Yohkoh`, `PROBA2`, `SWAP` and `Hinode` have **zero** matches
anywhere in the tracked tree, searched one term at a time with the anchored pattern
`(?<![A-Za-z0-9])TERM(?![A-Za-z0-9])` in Perl mode over every tracked path.

Two false positives to know about, because both look like mission evidence and neither is:
- **`TRACE`** returns one hit, `# END_TRACE` at `trace.py:209` — a label carried over from the IDL
  OCCULT-2 port, not the TRACE mission. (The anchored pattern matches it because `_` is not an
  alphanumeric; a case-insensitive search is worse still, matching the whole loop-tracing module.)
- **`EIT`** and **`EIS`** both appear in `.codespellrc`'s `ignore-words-list` (lines 21-34). That
  file lists spellings for the spell-checker to skip and is not evidence of instrument support; the
  EIS evidence used above is deliberately drawn from `examples/` and the coalignment tests instead,
  and there is no EIT support at all.

**VBI, the DKIST instrument, cannot be recorded at all**: the vocabulary contains no VBI instrument
row (zero matches), so DKIST is attachable only at observatory level. See Field 32.

### 32. Related Observatories (OPTIONAL)
**Observatories:**
- Solar Dynamics Observatory — https://spase-metadata.org/SMWG/Observatory/SDO

**The record held no observatories before this refresh; one of four resolvable candidates is
recorded.** As with Field 31 the candidates resolve cleanly and differ sharply in strength. Each
entry below gives the verbatim row name and identifier, in the order they were assessed, strongest
first.

**Recorded.**

1. **Solar Dynamics Observatory** — `https://spase-metadata.org/SMWG/Observatory/SDO`
   *Strongest*, and it is the platform of both strong instrument candidates: it carries all of the
   AIA and HMI evidence in Field 31, and `CHANGELOG.rst:98` names the platform directly
   ("outside of SDO/AIA").

**Examined and not recorded.**

2. **Hinode** — `https://spase-metadata.org/SMWG/Observatory/Hinode`
   *Middling*, resting entirely on the EIS example. The repository never writes "Hinode"; the
   platform association comes from the vocabulary's placement of EIS, not from the project.
3. **Solar and Heliospheric Observatory** — `https://spase-metadata.org/SMWG/Observatory/SOHO`
   *Middling-to-weak*, resting entirely on the LASCO C2 cosmic-ray example, and inheriting that
   example's weakness. (Note: two SOHO observatory rows exist — a second at
   `https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SOHO`. The `SMWG` row above is the
   canonical one.)
4. **Daniel K Inouye Solar Telescope** — `https://spase-metadata.org/SMWG/Observatory/DKIST`
   *Weakest.* The evidence is one fixture: `sunkit_image/data/test/dkist_photosphere.fits`, whose
   header carries `TELESCOP` `Daniel K. Inouye Solar Telescope`, `INSTRUME` `VBI` and `ORIGIN`
   `National Solar Observatory`, and which is the *only* fixture for granule segmentation
   (`sunkit_image/conftest.py`). Against it: "DKIST", "Inouye" and "VBI" appear nowhere in the
   tracked *text*, and `granule.segment`'s docstring is explicitly instrument-agnostic — "Segment an
   optical image of the solar photosphere into tri-value maps with:" (`granule.py:16`). A DKIST user
   would find a general photospheric segmentation routine, not DKIST tooling. This is the candidate
   the "designed to support" test most plausibly rejects.

**Fields 31 and 32 were decided together, and the recorded pair is consistent.** The observatory
recorded is the platform of both recorded instruments, so no instrument stands here without its
platform; and no observatory is recorded whose only support was an instrument that is itself not
recorded, which is what Hinode and SOHO would each have required.

**Two resolution notes:**

- **The DKIST row's name has no period after the "K"** — the vocabulary row is
  `Daniel K Inouye Solar Telescope`, while the FITS header in this repository reads
  `Daniel K. Inouye Solar Telescope`. The row name above is the one to record verbatim; the header
  string is quoted here as repository evidence, not as a value.
- **No VBI instrument row exists**, so DKIST can only ever be an observatory-level association for
  this software — an instrument-level record is not merely unevidenced, it is unavailable.

### 33. Logo (OPTIONAL)
**Logo:** Not found

Deliberately empty, and this is a documented omission rather than a search that was not done. Four
places were checked:

- **The repository contains no image files at all.** A scan of all 119 tracked file paths for image
  extensions (`.png`, `.jpg`, `.jpeg`, `.svg`, `.gif`, `.ico`, `.webp`) and for the path fragments
  `_static`, `logo` and `icon` returns nothing.
- **The docs configuration defines no logo.** `docs/conf.py:118` sets `html_theme = "sunpy"`, its
  `html_static_path` line is commented out (`docs/conf.py:135`), and there is no `html_logo` or
  favicon setting.
- **The rendered documentation's logo is not this package's.** The published docs page serves
  `_static/sunpy_icon.svg`, which is the shared SunPy project icon supplied by the
  `sunpy-sphinx-theme` package and is identical across every SunPy-family package. Recording it
  would attribute the organisation's icon to one of its packages, and it identifies nothing about
  sunkit-image.
- **The PyHC registry entry has no `logo:` key**, unlike some other entries in that file.

No logo should be invented, and a URL for the shared SunPy icon should not be recorded here if a
later refresh finds one.
