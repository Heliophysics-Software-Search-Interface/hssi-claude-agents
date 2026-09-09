# HSSI Metadata Extraction Results

**HSSI Software ID:** 1744df14-f1f1-451b-a384-28e3a1beba7f
**Repository:** https://github.com/sunpy/ndcube
**Source Revision:** ac348c6fd2832dfb7b587cfdbb2a41ccb343f80f
**Extraction Date:** 2026-09-08
**Validation Date:** 2026-09-08
**Validation Status:** PASS

---

Scope note. All repository evidence below is read at the pinned revision
`ac348c6fd2832dfb7b587cfdbb2a41ccb343f80f` (`Update scheduled_builds.yml`, committed 2026-09-03),
which is the tip of the default branch `main`. **Release tags are not on `main`.** ndcube releases
from `X.Y` release branches, so `v2.3.4`, `v2.4.0` and `v2.4.1` are all *not* ancestors of the pin.
`CHANGELOG.rst` at the pin opens on its first line with the compiled section `v2.4.0 (2025-12-09)`,
which was compiled on `main` by commit `6b3259939` ("render changelog for 2.4", 2025-12-09) — an
ancestor of the pin, and the commit the `2.4` release branch was cut from. What the file at the pin
does not contain is anything towncrier compiled on a release branch after that cut, so any claim
about such a release has to be read at that release's tag, and where one is used below the tag is
named. **A trap for anyone reading the section headings mechanically:** they are inconsistently
prefixed (`v2.4.0`, `2.3.0`, `2.2.0`, `v2.1.0`, `v2.0.3`, `v2.0.2`, `2.0.1`, `2.0.0`, ...), so a
digit-anchored pattern skips the first section and makes the file look as though it stops at
`2.3.0 (2025-01-14)`. It does not. Note too that the same `v2.4.0` section is dated `2025-12-09` at
the pin and `2026-01-14` at tag `v2.4.1`, the date having been revised on the release branch.

The project's own wiki records this release workflow: the release checklist instructs the
maintainer to "Create and change onto a new release branch from master labeled with the release
number" (`ndcube-Release-Instructions.md`, wiki repository
`https://github.com/sunpy/ndcube.wiki.git` at `eaab938613aae9900a178f214bdaea847799c1fb`; the wiki is
a separate repository and is invisible from the code pin).

The second thing that shapes this file is what ndcube *is*. It is a general-purpose, domain-agnostic
container for N-dimensional coordinate-aware arrays — an astronomy data model, not a heliophysics
instrument tool. Several fields therefore turn on a single recurring question: whether the metadata
should describe the software's own implemented capability, or the solar/heliophysics context in
which it is overwhelmingly used. The answer is not the same for every field. Where that question was
live it has been decided deliberately, and the evidence on the losing side of each decision is
preserved below as considered and not determinative rather than deleted — so that a later reader can
tell "this was known and decided against" from "this was missed".

---

## Section 1: Basic Information

### 1. Submitter
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The placeholder form is the catalogue-wide convention for this campaign. Nothing in the repository,
the DOI records or the PyHC registry identifies who submitted this entry to HSSI, and no identity is
inferred here.

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.5715150

HSSI held no value for this field before this refresh (`persistentIdentifier` was stored as an empty
string); the Zenodo concept DOI for this repository is recorded. The prior dossier asserted that no
software DOI existed at all; that assertion is wrong and is corrected here.

**What actually exists.** There is a Zenodo concept DOI for this repository,
`https://doi.org/10.5281/zenodo.5715150`, with nine versioned deposits under it. Every one of them
carries a single `isSupplementTo` relation to a `https://github.com/sunpy/ndcube/tree/<tag>` URL,
which is the signature of the automated GitHub-release integration rather than a manual upload. The
deposits, newest first by publication date:

| Deposit DOI | Title | Published |
|---|---|---|
| 10.5281/zenodo.8329977 | `sunpy/ndcube: v2.0.4` | 2023-09-08 |
| 10.5281/zenodo.8126828 | `sunpy/ndcube: v2.1.3` | 2023-07-08 |
| 10.5281/zenodo.7991885 | `sunpy/ndcube: v2.1.2` | 2023-05-31 |
| 10.5281/zenodo.7731317 | `sunpy/ndcube: v2.1.1` | 2023-03-14 |
| 10.5281/zenodo.7689917 | `sunpy/ndcube: v2.1.0` | 2023-03-01 |
| 10.5281/zenodo.7671845 | `sunpy/ndcube: v2.0.3` | 2023-02-23 |
| 10.5281/zenodo.7671844 | `sunpy/ndcube: v2.0.2` | 2023-02-23 |
| 10.5281/zenodo.5715161 | `sunpy/ndcube: v2.0.1` | 2021-11-19 |
| 10.5281/zenodo.5715151 | `sunpy/ndcube: v2.0.0` | 2021-11-19 |

Note the ordering trap: the newest deposit is **v2.0.4**, not the highest version number. It was
deposited two months after v2.1.3 because it was a backport release. A concept DOI resolves to its
newest deposit, so `10.5281/zenodo.5715150` presents as `sunpy/ndcube: v2.0.4`, version `v2.0.4`,
issued 2023-09-08, `resourceTypeGeneral: Software`, publisher Zenodo, with 22 creators (DataCite
metadata for the concept DOI, read 2026-09-08).

**The deposits stopped, and not because releases stopped.** The newest deposit was published
2023-09-08. Releases have continued since: GitHub release objects exist for `v2.3.4` (published
2025-10-06) and `v2.4.0` (published 2026-01-14), and PyPI carries 2.3.5, 2.4.0 and 2.4.1. No Zenodo
deposit corresponds to any of them.

**Why the deposits stopped is undetermined, and this file makes no claim about it.** The obvious
explanation — that the GitHub-release-triggered integration ceased to fire — is not what the
evidence shows: two post-2023 releases *do* have release objects and still produced no deposit, and
the cutoff precedes by more than two years the missing release objects discussed under Field 12, so
that gap cannot account for it. The state of the integration on Zenodo's or GitHub's side is a third
party's configuration, invisible from the repository and unverifiable here; it is deliberately not
asserted. The durable point a later refresh should carry forward is that release tags, GitHub
release objects and Zenodo deposits are three independent signals for this project, and both the
release-object list and the deposit list are demonstrably incomplete as release lists — which is why
Field 12 rests on the tags and PyPI instead.

Nothing in the repository at the pin asks users to cite a DOI for the code —
`docs/acknowledging.rst` asks for the two papers instead (Fields 14 and 27). That is a real argument
against recording any code DOI at all, and it was weighed rather than overlooked; it was not
determinative, because a citable software artifact does exist and a visitor who wants to cite the
code should be able to reach it from the catalogue page even though the project's own stated
preference is for the papers.

**The accepted cost of this value, stated plainly rather than softened.** The entry gains a "Cite Me"
block headed *Software*, built by content-negotiating the recorded DOI. A concept DOI resolves to its
most recently *created* deposit, and the v2.0.4 backport was deposited after v2.1.3, so the concept
presents as `sunpy/ndcube: v2.0.4` — meaning that block cites **ndcube v2.0.4 (2023)** beside a
Field 12 that reads v2.4.1. That mismatch is a known and accepted consequence of the value, not an
oversight in it. A reader who follows the DOI reaches a real, citable, authoritative Zenodo record for
this exact software; a reader who compares it against the version field sees a four-release gap. The
gap can only close if the project deposits again, which is outside this catalogue's control.

**The two alternatives, considered and not determinative.** Neither is refuted by the decision. Both
were live options with genuine merit, and they are kept here so a later refresh recognises them as
weighed rather than missed:
- **Leave Field 2 empty.** No software citation block renders at all. Nothing on the page is wrong,
  and nothing tells a visitor that a citable software artifact exists. This matches what the project
  itself asks for: cite the papers, not the code.
- **Leave Field 2 empty and record the concept DOI under Field 27 instead.** The DOI would survive on
  the page inside a correctly-labelled publications list rather than standing as the current software
  citation, at the cost of filing a Zenodo *software* deposit among publications. Field 27 records
  the SEP-0012 design document rather than this DOI; a software identifier is recorded here, where it
  belongs.

**Negative research — why no other DOI exists.** Three independent searches were run on 2026-09-08,
each with a control proving the query could see:
- *Title/free-text.* A Zenodo free-text search for `"sunpy/ndcube"` returns exactly the nine deposits
  tabled above. A title-scoped search for `ndcube` returns one unrelated-in-kind record, the SunPy
  Enhancement Proposal now recorded under Field 27.
- *Old repository name.* ndcube's git history contains a grafted 2015 lineage predating the
  repository itself; that work lived in `https://github.com/sunpy/cube` (created 2015-07-13, now
  archived, and *not* redirecting to ndcube — it is a separate surviving repository, not a rename).
  A Zenodo search for `"sunpy/cube"` returns nothing, against a control search for `"sunpy/sunpy"`
  that returns many. So no deposit hides under the predecessor name.
- *Creator-keyed.* Repository-name searches are structurally blind to a manual upload, so the two
  most central authors' ORCIDs were swept exhaustively via
  `metadata.creators.person_or_org.identifiers.identifier` — Daniel F. Ryan and Stuart J. Mumford,
  every result page fetched to exhaustion. No ndcube software deposit appears outside concept
  5715150. A garbage-name control returned zero, and both ORCID queries returned non-zero, so the
  instrument was demonstrably able to see. No record totals are quoted for those two sweeps on
  purpose: they are counts in a third party's index, they drift without notice, and nothing here
  will ever re-check them — what makes this negative reproducible is the query, the field path above
  paged to exhaustion with the same controls. An earlier attempt that added
  `metadata.resource_type.type:software` returned zero for *everything*; that clause is broken on
  this API and must not be used as evidence of absence.

Re-running any of these three searches depends on Zenodo's public API being reachable, which it
intermittently was not on 2026-09-08, when requests to it returned no response before timing out.
Anything that route cannot display should be read as *unverified by that route*, never as an
absence.

### 3. Code Repository (MANDATORY)
- **Repository URL:** https://github.com/sunpy/ndcube

Corroborated three ways at the pin: `pyproject.toml` declares `"Source Code" = "https://github.com/sunpy/ndcube"`;
the PyPI project metadata for `ndcube` gives the same string under `project_urls["Source Code"]`
(checked through the PyPI JSON API — the HTML project page returns 200 even for packages that do not
exist, so it proves nothing); and the PyHC registry entry's `code:` field is the same URL. The
repository is not archived and its default branch is `main`.

### 4. Software Functionality (RECOMMENDED)
- **Selected Values:**
  - Coordinate Transforms
  - Data Processing and Analysis
  - Data Processing and Analysis: 2D Slices
  - Data Processing and Analysis: Analysis
  - Data Processing and Analysis: Data Reduction
  - Data Processing and Analysis: Image Processing
  - Data Processing and Analysis: Processing
  - Data Visualization
  - Data Visualization: 2D Graphics
  - Data Visualization: 2D Slices
  - Data Visualization: Line Plots
  - Data Visualization: Movies

HSSI held only the three bare top-level categories (`Coordinate Transforms`, `Data Visualization`,
`Data Processing and Analysis`) until this refresh. The three parents are right and are kept; what
was missing is every subcategory, and the subcategory is what makes the entry findable. Each value
below is tied to a specific public capability at the pin.

**Coordinate Transforms (parent only).** ndcube's whole reason to exist is that the array and its
World Coordinate System travel together: `NDCube.axis_world_coords`,
`NDCube.axis_world_coords_values`, `NDCube.crop`, `NDCube.crop_by_values` and the
`combined_wcs`/`ExtraCoords`/`GlobalCoords` machinery all expose world↔pixel transformation to the
user, and `ndcube/wcs/wrappers/` implements `CompoundLowLevelWCS`, `ReorderedLowLevelWCS` and
`ResampledLowLevelWCS` as user-facing WCS objects. **No subcategory is selected, deliberately.** All
six children of this parent name a specific physical domain — Heliospheric, Ionospheric,
Magnetospheric, Mission-Specific, Planetary, Solar — and ndcube implements none of them. It
transforms whatever the supplied WCS describes; the frames themselves come from `astropy` or, in one
documentation example, from `sunpy.coordinates.frames.Helioprojective`
(`docs/explaining_ndcube/slicing.rst`). Selecting `Coordinate Transforms: Solar` on the strength of
that example would attribute a solar frame implementation to a package that contains none.

**Data Processing and Analysis: 2D Slices.** `ndcube/mixins/ndslicing.py` gives every cube standard
`[...]` slicing that carries the WCS, uncertainty, mask and extra coordinates through with it, and
`docs/explaining_ndcube/slicing.rst` is a whole documentation chapter about it. Extracting a 2D plane
from a 3D or 4D cube is the canonical use. `NDCube.explode_along_axis` and `NDCubeSequence` extend
the same idea to collections.

**Data Processing and Analysis: Data Reduction.** `NDCube.rebin` (bin-shape reduction with
configurable operation, mask handling and uncertainty propagation), `NDCube.crop` /
`NDCube.crop_by_values` (cut to a world-coordinate region) and `NDCube.squeeze` all reduce data
volume while preserving the physical description.

**Data Processing and Analysis: Processing.** The general transform surface: `NDCube.reproject_to`,
`NDCube.to` (unit conversion), `NDCube.fill_masked`, `NDCube.to_nddata`, and the full arithmetic set
(`__add__`, `__sub__`, `__mul__`, `__truediv__`, `__pow__`, `__neg__`) with mask and uncertainty
combination.

**Data Processing and Analysis: Analysis.** Examined as a trim candidate and retained. The argument
for it: ndcube does not merely move arrays around, it propagates *uncertainty* through arithmetic and
rebinning (`_combine_uncertainty`, the `propagate_uncertainties` path in `rebin`) and enforces
physical units, which is scientific analysis machinery rather than plumbing. **Considered and not
determinative:** the package computes no derived physical quantity of its own. That is a real
argument against the value and is kept here so a later refresh reads it as weighed rather than
missed. The judgement taken is that uncertainty propagation and unit enforcement are themselves
analysis capabilities a searcher would want surfaced, so the value stays.

**Data Processing and Analysis: Image Processing.** Also examined as a trim candidate, and also
retained. `NDCube.reproject_to` is a documented public method with its own documentation page
(`docs/explaining_ndcube/reproject.rst`) and gallery example
(`examples/changing_resolution_via_reproject.py`, which reprojects an SDO/AIA image to a new
resolution). Resampling image data onto a new coordinate grid is an image-processing operation, and
a searcher looking for reprojection capability would be glad to find ndcube. **Considered and not
determinative:** the reprojection algorithms belong to the `reproject` package and ndcube supplies
the wrapper. That is a genuine argument against the value, preserved rather than deleted. The
judgement taken is that a documented, user-facing method is a capability of the software that exposes
it, whoever wrote the algorithm underneath.

**Data Visualization (parent) and its four children.** `NDCube.plot` dispatches on dimensionality in
`ndcube/visualization/mpl_plotter.py`: `_plot_1D_cube` calls `axes.plot` (**Line Plots**),
`_plot_2D_cube` calls `axes.imshow` (**2D Graphics**), and `_animate_cube` builds an
`mpl_animators.ArrayAnimatorWCS` (**Movies**), with `MatplotlibSequencePlotter.animate` and the
`SequenceAnimator` class doing the same for `NDCubeSequence`. The animation path is also exactly what
justifies **Data Visualization: 2D Slices**: for a cube of three or more dimensions the animator
displays two chosen axes as an image and puts sliders on the rest, so what the user sees is a 2D
slice of a higher-dimensional volume. The plotter's own docstring names its two backends —
"Animations: `mpl_animators.ArrayAnimatorWCS`" and "Static 2-D images:
`matplotlib.pyplot.imshow`".

**Considered and rejected, each with its reason** (several of these were positively asserted by the
prior dossier and are corrected here):
- **Data Processing and Analysis: Data Access and Retrieval** — *asserted before; wrong.* ndcube
  downloads nothing. A case-insensitive search of the whole `ndcube/` package tree at the pin
  (`git grep -P -i -l 'requests|urllib|urlopen|download' <pin> -- 'ndcube/**'`) returns exactly one
  file, `ndcube/data/README.rst`, and the match is the word "downloaded" in a sentence of prose
  about where large files should live. No Python file in the package mentions any of these terms.
  There is no client, no query API, no archive interface.
- **Data Processing and Analysis: Spectrogram** and **Data Visualization: Spectrogram** — *asserted
  before; wrong.* Searching the same tree for `fft`, `wavelet` and `spectrogram` matches zero files.
  ndcube will happily hold a (time, wavelength) array and `imshow` it, but it neither computes a
  time-frequency representation nor has any spectrogram-specific display code, and a searcher
  filtering for spectrogram software would not be well served.
- **Data Visualization: 3D Graphics** — *asserted before; wrong.* Zero matches for `mplot3d`, `vtk`,
  `mayavi` and `pyvista` in the package tree. ndcube handles 3D+ *data*; it never renders a 3D
  *scene*.
- **Data Processing and Analysis: File Format Conversion.** ndcube serializes its own objects to
  ASDF (`ndcube/asdf/`, ten converters plus schemas, registered through the
  `asdf.resource_mappings` and `asdf.extensions` entry points in `pyproject.toml`). That is
  save/load of one format, not conversion between two.
- **Data Processing and Analysis: Time Series Analysis.** A cube axis may be temporal
  (`TimeTableCoordinate` in `ndcube/extra_coords/table_coord.py`), but no temporal analysis method —
  filtering, detrending, correlation — exists.
- **Data Processing and Analysis: Image Processing** was *not* rejected; it is discussed above. The
  neighbouring **Calibration**, **Data Assimilation**, **Energy Spectra**, **Field-line Tracing**,
  **ML/AI**, **Packet Decommutation**, **Pitch Angle Distributions**, **Plasma Moments**,
  **Curlometer**, **Linear Gradient Estimation**, **Magnetic Null Finding**, **3D Particle
  Distribution Processing** and **Wave Polarization Analysis** children are unimplemented. Each was
  searched for separately across the 103 files tracked under `ndcube/` at the pin (86 of them
  Python), with `git grep -P -i -l <pattern> <pin> -- 'ndcube/**'`; the pathspec recurses into
  subdirectories, which is what is wanted here, and the `-P` matters because `git grep -E` treats
  `\b` as a literal `b` and would fail toward a clean zero. The patterns were `calibrat`,
  `assimilat`, `energy[ _-]?spectr`, `field[ _-]?line|fieldline|streamline`,
  `tensorflow|pytorch|torch|sklearn|scikit-learn|machine learning|neural net`,
  `decommut|telemetry|CCSDS|\bpacket`, `pitch[ _-]?angle`, `plasma`, `curlometer`, `gradient`,
  `magnetic null|null[ _-]?point`, `velocity distribution|distribution function|phase[ _-]?space`
  and `polari[sz]|stokes`, with `reproject` and `rebin` as positive controls (3 and 7 files).
  Twelve of the thirteen matched no file at all. The thirteenth is a single line, and it is recorded
  here rather than tuned away: `ndcube/utils/wcs.py` line 52 maps the FITS-WCS axis type `"STOKES"`
  to the IVOA UCD `"phys.polarization.stokes"`. That is a label for a coordinate axis the user's
  data may carry, not a polarization capability — ndcube computes no Stokes parameter and fits no
  polarization ellipse — so **Wave Polarization Analysis** is rejected on absent capability rather
  than on absent text. A later agent widening these patterns should expect that hit and no other.
- **Mission-related** and all its children. ndcube is not part of any mission ground system; it is a
  library those systems build on (see Fields 29/30).
- **Models and Simulations** and all its children. Nothing in the package models a physical system.
- **Servers and Environments** and all its children. No server, no container, no HPC support.

The subcategory names are written in the canonical `Parent: Child` form the API returns. The
vocabulary rows carry no definitions of their own, so the category wording relied on above is the
taxonomy description maintained in this repository's software-functionality guidance, not row text.

### 5. Related Region (RECOMMENDED)
- **Selected Values:** No value

**Evidenced-empty, by decision.** HSSI held `Interplanetary Space` and `Solar Environment` before
this refresh; both are cleared. Field 5 is RECOMMENDED rather than mandatory, so an empty value is a
legitimate outcome for this field — and this emptiness is an examined one, reached by weighing the
evidence below, not an unfilled blank. ndcube is a domain-agnostic N-dimensional astronomy data
model. It contains no region-specific physics and supports no region specifically: it holds whatever
array and WCS the user supplies, and whatever solar or heliospheric character it appears to have is
borrowed entirely from the packages built on it.

**Considered and not determinative.** The opposing case was real, and it is preserved in full here so
that a later refresh recognises it as known and decided against rather than newly discovered. The
form defines the field as "The physical region the software supports science functionality for." and
instructs the submitter to "Select all physical regions the software's functionality is commonly used
or intended for" — wording that explicitly licenses a "commonly used for" reading rather than an
"implements physics for" one. Under that reading the two cleared values were defensible, and the
supporting evidence is genuine: ndcube is a SunPy Project affiliated package; the PyHC registry tags
it `heliosphere` and `solar`; its own gallery examples work on SDO/AIA solar images; and the packages
built on ndcube that Field 30 names — sunraster, the DKIST user tools, irispy, punchbowl, HERMES Core
and eispac — are solar and heliophysics tools. (Field 30 also lists astropy and specutils, which are
general-astronomy rather than solar, so the ecosystem argument is strong but not uniform.) A visitor
filtering HSSI for
solar-environment software would arguably be glad to be handed the standard container for solar
imaging and spectral data. The judgement taken is that a region association borrowed wholly from an
ecosystem is not one the software itself supports, and that this field should describe the software.
That is a judgement between two defensible readings, not a refutation of the evidence above.

**Considered and rejected: the finer solar regions.** The live vocabulary is finer-grained than the
two broad values that were cleared: `Corona`, `Chromosphere`, `Photosphere`, `Solar Interior` and
`Solar Wind` are all rows in it. None is recorded. The vocabulary
is flat — a fine value does not imply its coarse parent and vice versa — so selecting `Corona` would
be a positive claim that ndcube supports coronal science specifically, which nothing supports: the
package never mentions a solar atmospheric layer, and the word "corona" appears at the pin only in
the PUNCH mission's full name (in the JOSS paper and its bibliography) and inside a contributor's
old hostname in `.mailmap`. Even under the "commonly used for" reading, only the generic-solar
association was ever arguable; a layer-specific one never was.

### 6. Authors (MANDATORY)

**Source and criterion.** `.zenodo.json` at the pin is the project's own maintained credit list — the
wiki's release checklist has "Update .zenodo.json" as a standing pre-release item — and it is the
source of record for this field. It contains 35 creator entries. HSSI held 31 of those people
before this refresh. The four it lacked are added below; nobody stored is removed. Every one of the
four has commits reachable from the pin, counted with the repository's `.mailmap` (246 lines)
applied so that handle variants collapse onto one identity: Piyush Sharma 39, Albert Y. Shih 6, Diya
Khetarpal 6, Eero Vaher 1.

> **Author identity notes.** These are the durable identity findings for this author list; a later
> refresh should read them before "correcting" anything.
>
> **Ricky O'Steen's ORCID.** `.zenodo.json` records it as `A0000-0002-2432-8946`, with a stray
> leading `A`. HSSI stores the well-formed `https://orcid.org/0000-0002-2432-8946`. **HSSI is right
> and the source file is wrong**; do not "restore" the source form.
>
> **Dan Foreman-Mackey.** `.zenodo.json` credits him as `Dan F-M`, and the repository's `.mailmap`
> does not canonicalize that string. The git author line is `Dan F-M <foreman.mackey@gmail.com>`,
> whose address supplies the surname. HSSI stores the expanded `Dan Foreman-Mackey`, which is kept.
> **No identifier is recorded** — the ORCID-to-address link is not independently established here, so
> it is left absent rather than guessed.
>
> **Three name forms where the repository and HSSI disagree.** `.mailmap` at the pin canonicalizes
> `Samuel J. Van Kooten`, `Andrew Leonard` and `Matthew J. West`; HSSI stores `Sam Van Kooten`,
> `Andrew J. Leonard` and `Matthew West`. Each pair is one person, and the differences are cosmetic.
> They are recorded here rather than acted on, for two reasons: a stored person is a shared record
> that other software in the catalogue may also credit, so renaming one is not a decision this entry
> can make alone; and a routine metadata update cannot rename a stored person in any case, so any
> alignment would be a deliberate database-side correction. Do not attempt it as part of a field
> patch.
>
> **This repository's `.mailmap` is an authoritative identity source beyond ndcube itself.** Among
> others it maps `Ghaithq` → **Ghaith Kdimati**, `Brett Graham` → **Brett J Graham**, `ankit` →
> **Ankit Baruah**, `DanRyanIrish` → **Daniel F. Ryan**, `ViciousEagle03` → **Piyush Sharma**,
> `Diya910` → **Diya Khetarpal**, and `ayshih` → **Albert Y. Shih**. A refresh of any of those
> authors, in this project or another, should consult it rather than reasoning from name similarity.
> Note in particular that splitting the handle `DanRyanIrish` on whitespace yields a given name "Dan
> Ryan" and a family name "Irish", which is wrong and has been reproduced elsewhere.
>
> **Ankit Baruah** is the same person SunPy credits as "Ankit Baruah" — the same commit address
> `ankit.baruah1@gmail.com` appears in both projects and both `.mailmap` files canonicalize it.
> Neither project supplies an ORCID for him. **SunPy's separate creator `Ankit` is a different
> person** and must not be conflated.
>
> **Mateo Inchaurrandieta** is the same person SunPy credits under the identical name; the shared
> commit address `mateo.inchaurrandieta@gmail.com` establishes it. No source gives him an ORCID or
> affiliation.
>
> **Ten stored authors carry no identifier**: Mihail Bankov, Ankit Baruah, Dan Foreman-Mackey, Mateo
> Inchaurrandieta, Baptiste Pellorce, Aoife Maria Ryan, Gabe Shafiq, Sanvi Sharma, Roy Smart and
> Shelbe Timothy. This is correct, not a gap: `.zenodo.json` gives an `orcid` key for none of them,
> and no other source in the repository does either. **Never attach an ORCID to one of these people
> as part of a field update** — an identifier arriving for an already-stored identifier-less person
> does not fill in their record, it creates a second one and strands the original. If an ORCID is
> ever established for one of them it is a database-side correction, not a patch value.
>
> **The JOSS paper is not usable as an identifier source.** `joss_paper/paper.md` at the pin lists
> "Will T. Barnes" with `orcid: 0000-0001-6874-2594` — which is Albert Shih's ORCID, not Will
> Barnes's (`0000-0001-9642-6089`, as stored). Take identifiers from `.zenodo.json`, not the paper.

**Stored authors, kept unchanged** (name — identifier — affiliations as stored):

1. **Mihail Bankov** — no identifier
2. **Will Barnes** — https://orcid.org/0000-0001-9642-6089 — American University (https://ror.org/052w4zt36); Department of Physics, American University; Goddard Space Flight Center (https://ror.org/0171mag52); United States Naval Research Laboratory (https://ror.org/04d23a975)
3. **Ankit Baruah** — no identifier — Workato Gmbh, Germany
4. **Samuel Bennett** — https://orcid.org/0000-0001-6420-4422 — Aperio Software Ltd.; University of Sheffield (https://ror.org/05krs5044)
5. **Adwait Bhope** — https://orcid.org/0000-0002-7133-8776 — Savitribai Phule Pune University (https://ror.org/044g6d731); Uptycs India Pvt. Ltd., India
6. **Dan Foreman-Mackey** — no identifier
7. **Nabil Freij** — https://orcid.org/0000-0002-6253-082X — Bay Area Environmental Research Institute (https://ror.org/024tt5x58); Lockheed Martin Solar and Astrophysics Laboratory; SETI Institute (https://ror.org/02dxgk712)
8. **Laura Hayes** — https://orcid.org/0000-0002-6835-2390 — Dublin Institute for Advanced Studies (https://ror.org/051sx6d27); European Space Research and Technology Centre (https://ror.org/03h3jqn23)
9. **Derek Homeier** — https://orcid.org/0000-0002-8546-9128 — Aperio Software Ltd.
10. **J. Marcus Hughes** — https://orcid.org/0000-0003-3410-7650 — Southwest Research Institute (https://ror.org/03tghng59)
11. **Junyan Huo** — https://orcid.org/0000-0002-5469-7697 — University College London (https://ror.org/02jx3x895)
12. **Mateo Inchaurrandieta** — no identifier
13. **Andrew J. Leonard** — https://orcid.org/0000-0001-5270-7487 — Aperio Software Ltd.
14. **Pey Lian Lim** — https://orcid.org/0000-0003-0079-4114 — Space Telescope Science Institute (https://ror.org/036f5mx38)
15. **Shane Maloney** — https://orcid.org/0000-0002-4715-1805 — Dublin Institute for Advanced Studies (https://ror.org/051sx6d27)
16. **Stuart J. Mumford** — https://orcid.org/0000-0003-4217-4642 — Aperio Software Ltd.; University of Sheffield (https://ror.org/05krs5044)
17. **Ricky O'Steen** — https://orcid.org/0000-0002-2432-8946 — Space Telescope Science Institute (https://ror.org/036f5mx38)
18. **Baptiste Pellorce** — no identifier — Claude Bernard Lyon 1 University (https://ror.org/029brtt94)
19. **Kritika Ranjan** — https://orcid.org/0000-0001-5638-016X — Jain (Deemed-to-be University), Bangalore
20. **Andrew Robbertz** — https://orcid.org/0009-0008-6857-0882 — General Dynamics Mission Systems; Goddard Space Flight Center (https://ror.org/0171mag52)
21. **Aoife Maria Ryan** — no identifier
22. **Daniel F. Ryan** — https://orcid.org/0000-0001-8661-3825 — Mullard Space Science Laboratory, University College London; University College London (https://ror.org/02jx3x895)
23. **Gabe Shafiq** — no identifier
24. **Sanvi Sharma** — no identifier
25. **Yash Sharma** — https://orcid.org/0000-0002-7861-9677 — Indian Institute of Technology, Kharagpur (https://ror.org/03w5sq511); Meta Platforms Inc., UK
26. **Roy Smart** — no identifier
27. **David Stansby** — https://orcid.org/0000-0002-1365-1908 — Advanced Research Computing Centre, University College London, UK; Department of Mechanical Engineering, University College London; Imperial College London (https://ror.org/041kmwe10); Mullard Space Science Laboratory, University College London; University College London (https://ror.org/02jx3x895)
28. **Kris Akira Stern** — https://orcid.org/0000-0003-1613-8947 — University of Hong Kong (https://ror.org/02zhqgq86)
29. **Shelbe Timothy** — no identifier
30. **Sam Van Kooten** — https://orcid.org/0000-0002-4472-8517 — Southwest Research Institute (https://ror.org/03tghng59)
31. **Matthew West** — https://orcid.org/0000-0002-0631-2393 — European Space Research and Technology Centre (https://ror.org/03h3jqn23); Southwest Research Institute (https://ror.org/03tghng59)

**One stored affiliation is narrower than its source, and that is left as it is.** `.zenodo.json` at
the pin gives Baptiste Pellorce's affiliation as the single packed string
`"1 - Claude Bernard Lyon 1 University, France 2 - Institute of Theoretical Astrophysics, Norway"`,
naming two institutions in one field. HSSI stores only the first. The second is not added here, for
two independent reasons. He is stored without an identifier, so he resolves by name onto an existing
shared person record, and this entry does not mutate shared records — his affiliations are whatever
that record already holds. And the Institute of Theoretical Astrophysics is a department of the
University of Oslo with no ROR of its own (an exact-name ROR search on 2026-09-08 returned no
matching organization), so recording it would mint a new identifier-less Organization row — the same
durable cost that decided Lund Observatory for Eero Vaher below and `Daniel K. Inouye Solar
Telescope` in Field 25. A later refresh should read the single affiliation as this decision rather
than as an incomplete reading of the source.

**Authors added by this refresh** (all four are credited in `.zenodo.json` at the pin and all four
have commits in the pin's ancestry):

32. **Albert Y. Shih** — https://orcid.org/0000-0001-6874-2594 — Goddard Space Flight Center (https://ror.org/0171mag52)
    `.zenodo.json` gives the affiliation as "NASA Goddard Space Flight Center"; the acronym is
    expanded per the form's instruction, and the expanded form is written exactly as ROR's display
    name for `0171mag52`, which is also how the same institution is already spelled for Will Barnes
    and Andrew Robbertz above. The ORCID resolves to Albert Shih.
33. **Diya Khetarpal** — https://orcid.org/0009-0009-4729-6797
    ndcube's own `.zenodo.json` gives her no ORCID and no affiliation; the ORCID is established from
    outside this repository, by the same evidence chain set out for Piyush Sharma below. `.mailmap`
    at the pin maps `Diya910 <152620955+Diya910@users.noreply.github.com>` to Diya Khetarpal, and the
    same GitHub noreply address appears in the **sunpy** repository's commit history under the same
    handle mapping in sunpy's own `.mailmap`. The numeric prefix of that address is GitHub's internal
    account id (152620955), so the address identifies one *account*, not merely one spelling of a
    name. sunpy's `.zenodo.json` in turn asserts
    `{"name": "Diya Khetarpal", "orcid": "0009-0009-4729-6797"}`, and the name occurs once in sunpy's
    author history. Stated at its actual strength, that chain establishes two things: the ndcube
    contributor and the sunpy contributor are the same GitHub account, and SunPy attaches this ORCID
    to that name. **This ORCID was previously withheld, and that caution was correct on the evidence
    then available.** An earlier pass could see only that an ORCID registered to someone named "Diya
    Khetarpal" existed in the HSSI catalogue, listing no works and no visible connection to ndcube —
    a bare name match, which should not be asserted. What overturned it is new evidence (the
    account-level link across the two repositories, plus SunPy's own ORCID assertion), not a
    re-weighing of the same facts. Do not re-open it as an unproven association. No affiliation is
    recorded: neither project's source gives her one, and the catalogue's person record for this
    ORCID carries none either. Note that she is an author *added* by this refresh rather than one
    already stored identifier-less, so the caution above about identifiers arriving for stored
    identifier-less people does not apply to her.
34. **Piyush Sharma** — https://orcid.org/0009-0005-1579-5787
    The same evidence chain. ndcube's `.zenodo.json` credits him with no ORCID and no affiliation,
    and `.mailmap` at the pin maps his GitHub handle `ViciousEagle03 <piyushsharma04321@gmail.com>`
    to this name. The identical commit address appears in the **sunpy** repository's history, under
    the identical handle mapping in sunpy's `.mailmap`, and sunpy's `.zenodo.json` asserts
    `{"name": "Piyush Sharma", "orcid": "0009-0005-1579-5787", "affiliation": "Indian Institute of
    Technology Roorkee"}`. The match is on the full name plus the shared commit address, never on the
    surname: sunpy credits six other Sharmas (Rishabh, Yash, Swapnil, Deepankar, Prisha and Rohan)
    and this record already credits two more (Yash Sharma and Sanvi Sharma), all different people.
    "Piyush Sharma" occurs once in sunpy's author history. As with Diya Khetarpal, **the ORCID was
    previously withheld on evidence that genuinely did amount to a name match** — an ORCID registered
    to a "Piyush Sharma" existing elsewhere in the catalogue with no works and nothing tying it to
    ndcube — and the withholding was the right call then; the cross-repository account evidence and
    SunPy's ORCID assertion are what changed. He is the single largest contributor among the four
    additions by commit count.
    **On affiliation:** the catalogue's person record for this ORCID already carries the affiliation
    Indian Institute of Technology Roorkee (https://ror.org/00582g326), which reached it from SunPy
    and from no ndcube source. Because a person is a shared record, that affiliation will therefore
    display on ndcube's page. That is a consequence of crediting the same person, not a claim this
    entry makes — ndcube's own sources give him no affiliation, and none is asserted here.
35. **Eero Vaher** — https://orcid.org/0000-0001-8736-1762
    ORCID from `.zenodo.json`; it resolves to Eero Vaher.
    **The affiliation is deliberately withheld, not missing.** `.zenodo.json` really does give it as
    "Lund Observatory", so leaving it out is a decision rather than a correction of a faulty source.
    "Lund Observatory" has no ROR of its own — an exact-name ROR search on 2026-09-08 returned no
    matching organization — and the catalogue holds no Organization row for it, so recording it would
    mint a new identifier-less Organization. Organizations are shared records that no API path can
    rename afterwards, which is the same durable cost Field 25 sets out for `Daniel K. Inouye Solar
    Telescope`; this entry is decided the same way for consistency with that decision.
    **Lund University (https://ror.org/012a77v79) was considered and is not used.** It is cleanly
    ROR-identified — that identifier's ROR display name is exactly "Lund University" — and adding a
    parent institution alongside a department is a pattern this record already uses for Daniel F.
    Ryan (MSSL plus UCL). It is rejected because the source names the observatory, and promoting it
    to the parent university is inference rather than evidence.
    **What this costs:** Eero Vaher's affiliation is simply absent from ndcube's HSSI entry. A later
    refresh should read that absence as this settled decision, not as a gap someone failed to fill.

**`pyproject.toml` names a single author,** `{ name = "The SunPy Community", email = "sunpy@googlegroups.com" },`.
That is a mailing-list contact, not the credit list, and it is not used: recording "The SunPy
Community" as an organization author would replace 35 named people with one label. `.zenodo.json` is
the richer and more deliberate source and wins.

### 7. Software Name (MANDATORY)
- **Software Name:** ndcube

Lower-case throughout the project's own materials: the `README.rst` heading at the pin is the
package name wrapped in double backticks, the `pyproject.toml` declaration is `name = "ndcube"`, the
PyPI project is `ndcube` and the import name is `ndcube`. The PyHC registry writes it `"NDCube"` and the ApJ paper title uses "NDCube 2",
but the repository's own casing governs, and the stored value already matches it. No change.

### 8. Description (MANDATORY)
- **Description:** ndcube is an open-source SunPy affiliated package for manipulating, inspecting and visualizing multi-dimensional contiguous and non-contiguous coordinate-aware data arrays. It combines data, uncertainties, units, metadata, masking, and coordinate transformations into classes with unified slicing and generic coordinate transformations and plotting/animation capabilities. It is designed to handle data of any number of dimensions and axis types (e.g. spatial, temporal, spectral, etc.) whose relationship between the array elements and the real world can be described by World Coordinate System (WCS) translations.

Carried over unchanged. It is the `README.rst` text at the pin, with the reStructuredText double
backticks around the package name removed — the three sentences are otherwise the project's own
words. It remains accurate at this revision, so the wording stands as it is; a stylistic
alternative would not be an improvement.

### 9. Concise Description (OPTIONAL)
- **Concise Description:** A Python package for manipulating, inspecting and visualizing multi-dimensional contiguous and non-contiguous coordinate-aware data arrays.

Carried over unchanged. It matches the PyHC registry's `description:` for this project (plus a
closing full stop) and is comfortably inside the field's length budget. The alternative source, the
`pyproject.toml` `description = "A package for multi-dimensional contiguous and non-contiguous coordinate aware arrays."`,
is shorter but drops both the language and the three verbs that say what the package is *for*, so
the stored value is the better one.

### 10. Publication Date (RECOMMENDED)
- **Publication Date:** 2015-07-20

Carried over and corroborated: the earliest author date anywhere in the pin's ancestry is
2015-07-20, on commit `0a2183f2fc625e786e831da778ac485e8f8e0ef6` ("Refactored directory structure",
authored by `mateoi`). Note that the history has **two root commits** — that 2015 lineage was grafted
in from the predecessor project `https://github.com/sunpy/cube`, while the commit that created this
repository's own tree is `00b9147ad279a804c5e97fe4bf924e4365abf12e` ("Creation of ndcube from astropy
package template", 2017-08-15).

Two later dates were considered and rejected as the value: the GitHub repository's creation date,
2017-08-15, and the first PyPI upload, 2017-12-13 (`0.1.dev273`). Both are defensible readings of
"publication", but the stored 2015 date is the beginning of the work this software *is*, it is what
the catalogue already asserts, and changing it would trade one arguable convention for another with
no gain to a searcher.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

HSSI held `GitHub`, with the identifier `https://github.com`, before this refresh. The publisher is
now **Zenodo**. This was decided on its own evidence rather than following automatically from the
Field 2 decision: DataCite records `Zenodo` as the publisher of every deposit in the concept,
including the concept DOI `10.5281/zenodo.5715150` that Field 2 now records, so `Zenodo` is what the
authoritative record for the recorded identifier says. Leaving `GitHub` beside a `zenodo.org` DOI
would also read as internally inconsistent on the rendered page.

**`GitHub` was correct while Field 2 was empty, and this is not the correction of an error.** With no
persistent identifier recorded, the repository host is the entity that makes the software publicly
available, and GitHub was it. The value changed because the record changed underneath it: once the
entry carries a Zenodo-published persistent identifier, the publisher of that identifier is the
entity this field names. A later reader should read the change as a consequence of Field 2 acquiring
a value, not as a repair of a mistake.

The identifier recorded is Zenodo's own URL, in the same form the previous value used for GitHub.
No ROR was available to record in its place: a ROR search for Zenodo on 2026-09-08 returned no
organization at all.

### 12. Version (RECOMMENDED)
- **Version Number:** v2.4.1
- **Version Date:** 2026-06-10
- **Version Description:** Bug-fix release. Fixes compatibility with gwcs >= 1.0, which required raising the minimum supported gwcs to 0.24 and consequently asdf to >= 3.3.0 and scipy to >= 1.14.1. Adds a gallery example showing how to change the resolution of an NDCube using `NDCube.reproject_to`.
- **Version PID:** Not found

HSSI held `v2.3.4` (2025-10-06) until this refresh — three releases behind. The current release is
**v2.4.1**, and establishing that took care because this project's release evidence is scattered:

- **Tags.** The repository carried 59 tags when its tag list was read on 2026-09-08. `v2.4.1`
  points (through annotation) at commit `efb8f08b`, tag date 2026-06-10. It is *not* an ancestor of
  the pin, because it lives on the `2.4` release branch. `v2.5dev` also exists but is a development
  marker, not a release.
- **PyPI.** The `ndcube` project's `info.version` is `2.4.1`, its newest file upload is
  2026-06-10T16:17, and its `project_urls["Source Code"]` is this repository — so the PyPI project
  is certainly this software. 2.3.5 (2025-12-03) and 2.4.0 (2026-01-14) sit between the value HSSI
  held before this refresh and the current one.
- **GitHub release objects are incomplete and must not be used as the release list.** The GitHub
  releases API returned 31 of them when read on 2026-09-08, the newest `v2.4.0`, with **no release
  object for `v2.4.1` and none for `v2.3.5` either**. That count is quoted, where Field 23 declines
  to quote a PyPI release total, because here the number is the argument: 31 release objects against
  59 tags and a longer PyPI history is what demonstrates the incompleteness. Both of those releases
  are real — each has a tag, a PyPI upload and a changelog section. This is a release-object gap,
  not a release gap. It does **not** explain the Zenodo deposit cutoff described under Field 2: that
  cutoff falls in 2023, and the two releases that followed it and *do* carry release objects
  (`v2.3.4`, `v2.4.0`) produced no deposit either.
- **Changelog.** The description above is condensed from the `2.4.1 (2026-06-10)` section of
  `CHANGELOG.rst` **read at tag `v2.4.1`** — it contains one bug fix and one documentation entry,
  and both are represented. That compiled section does not exist at the pin, where the compiled
  changelog reaches `v2.4.0 (2025-12-09)` (see the scope note). The release's *content* is present
  at the pin nonetheless, uncompiled: the `changelog/` directory there holds three files — its
  towncrier `README.rst` and two loose fragments, `changelog/931.bugfix.rst` and
  `changelog/893.doc.rst` — which correspond one-to-one to v2.4.1's bug fix and documentation
  entries and carry the same wording as the compiled section, down to the misspelling `concequenty`.
  The compiled form differs only by towncrier's list formatting and its appended pull-request links.
- **Version PID.** None: the newest Zenodo deposit is v2.0.4 (Field 2), so no DOI exists for this or
  any recent release. The DOI recorded in Field 2 is the *concept* DOI for the software as a whole;
  it is not a version identifier for v2.4.1 and must not be copied into this line.

There is no in-tree version literal to cross-check against — `pyproject.toml` declares
`dynamic = ["version"]` and `setuptools_scm` writes `ndcube/_version.py` at build time.

### 13. Programming Language (RECOMMENDED)
- **Selected Values:**
  - Python 3.x

**The criterion, settled once and applied to every inclusion and exclusion below: this field records
the language the software is written in and that a user writes against — not every language with a
file in the tree.** ndcube is a pure-Python library; there is no compiled extension, no bundled
example in another language, and nothing a user could invoke from another language.

Evidence. A census of the 190 files tracked at the pin — `git ls-tree -r --name-only <pin>`, whole
tree, grouping on the text after the final `.` in each basename — gives: `py` 93, `rst` 37, `yaml`
17, `yml` 10, `png` 7, `json` 4, `sh` 2, `toml` 2, `txt` 2, `md` 2, `ini` 2, and one each of `svg`,
`pdf`, `bib`, `bat`, `in`, `mailmap`, `gitignore`, `flake8`, `coveragerc`, `codespellrc`, plus two
files with no extension. `pyproject.toml` declares `requires-python = ">=3.11"`, and the CI matrix
exercises Python 3.11 through 3.14.

**Excluded by that criterion, explicitly:**
- The two `.sh` files (`.circleci/codecov_upload.sh`, `.circleci/early_exit.sh`) and the one `.bat`
  file (`docs/make.bat`, beside `docs/Makefile`) are continuous-integration and Sphinx build
  wrappers. They are not the software; nobody uses ndcube by running them.
- The `.yaml`/`.yml` files are workflow definitions and ASDF schemas/manifests, and the `.json` files
  are figure-hash fixtures and `.zenodo.json` — data, not code.
- The live vocabulary offers IDL, MATLAB, Julia, C, C++, Rust and five Fortran editions. **No
  source file in any of them exists in the tree** — the 190-file extension census above turns up no
  extension belonging to any — and none is recorded. One textual occurrence exists and is written
  down here so that a later sweep does not read it as a contradiction: `joss_paper/paper.bib` line
  277 carries `keywords = {Python, C, Astronomy, Solar physics, IDL}` inside a cited paper's BibTeX
  entry. Word-anchored whole-tree searches at the pin (`git grep -P -i -l <pattern> <pin>`) return
  that one file for `\bIDL\b` and no file at all for `\bMATLAB\b`, `\bJulia\b`, `\bFortran\b`,
  `\bRust\b` or `\bC\+\+\b`.

Note that `pyproject.toml` at the pin contains **no classifier list at all** — no
`Programming Language ::` and no `Development Status ::` entry — so the usual packaging shortcut for
both this field and Field 23 is unavailable here, and both had to be derived from the tree and the
repository's own state.

### 14. Reference Publication (OPTIONAL)
- **DOI:** https://doi.org/10.21105/joss.05296

Carried over unchanged. `docs/acknowledging.rst` at the pin asks users to cite two references, and
this is the first: *Ryan, Mumford et al., "ndcube: Manipulating N-dimensional Astronomical Data in
Python", Journal of Open Source Software, 2023*. The paper's source is in the repository itself
(`joss_paper/paper.md`, `joss_paper/paper.bib`), and the JOSS badge in `README.rst` targets the same
DOI. The second requested citation, the ApJ paper, is recorded under Field 27 where a second
publication belongs. That division of the project's two requested citations between Fields 14 and 27
is unchanged by this refresh. Field 27 additionally records the SEP-0012 design proposal, for the
reasons given there.

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License

Carried over unchanged; the stored row name is already the exact live vocabulary spelling, including
the straight double quotes around *Simplified*. GitHub's licence detection for the repository reports
`spdx_id: BSD-2-Clause` with the same display name.

**A real nuance worth recording: the pin carries two BSD 2-Clause files with different copyright
lines.** `LICENSE.rst` at the repository root opens
`Copyright (c) 2019-2022, The SunPy Community`, while `licenses/LICENSE.rst` opens
`Copyright (c) 2024, The SunPy Community`. The two files are otherwise byte-identical — a diff at
the pin shows exactly one differing line — so there is no licence *conflict*, only a stale year in
the root copy. The authoritative one for packaging purposes is the `licenses/` copy, because
`pyproject.toml` declares `license-files = ["licenses/LICENSE.rst"]`. (`licenses/` also holds a
`README.rst` and an unused `TEMPLATE_LICENSE.rst` inherited from the astropy package template.)

Both files are cited here strictly as **evidence for which vocabulary row to select**. Field 15 is a
choice among the live `License` rows, and the row itself carries the licence URL; there is no
per-software licence URI to record, so no file path or `opensource.org` link is stored as a value.
The prior dossier recorded a "License URI" of `https://opensource.org/licenses/BSD-2-Clause`; that
was never a storable field value and is dropped.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- **Selected Values:**
  - astronomy
  - astrophysics
  - astropy
  - asdf
  - coordinates
  - data analysis
  - data container
  - heliosphere
  - multi dimensional data
  - ndcube
  - plotting
  - python
  - solar
  - spectral data
  - sunpy
  - wcs
  - world coordinate system

The fifteen values HSSI held before this refresh are all kept, and are written here in their
**stored** spelling —
lower case throughout. The catalogue page title-cases keywords for display, so a rendered value like
"World Coordinate System" or "Wcs" is a presentation artifact and must not be copied back as if it
were the stored string.

Six of the stored values are the PyHC registry's own keywords for this project, with the registry's
underscores expanded into spaces:
`keywords: ["coordinates", "data_analysis", "data_container", "heliosphere", "plotting", "solar"]`
(`_data/projects.yml` in the `heliophysicsPy/heliophysicsPy.github.io` repository at commit
`bd18e66b`, entry `- name: "NDCube"`). The PyHC domain keywords are worth a caution for a later
refresh, because registry keywords propagate to packages that do not really touch the domain: here
`heliosphere` and `solar` are *not* supported by anything in ndcube's own code (see Fields 5 and 22)
and rest entirely on the ecosystem the package serves. They are kept because a keyword is a search
aid rather than a capability claim, but they should not be cited as evidence for the science fields.

**Two values are added by this refresh**, both from the repository's own self-description:
- **astropy** — a repository topic (on 2026-09-08 the repository's topics were `astropy`, `nddata`,
  `numfocus`, `sunpy` and `wcs`; the last two were already among the kept values), and a
  substantive one: `NDCube`
  subclasses `astropy.nddata.NDData` and astropy's WCS objects are its native coordinate
  description.
- **asdf** — ndcube implements ASDF serialization for its own object types
  (`ndcube/asdf/converters/`, schemas under `ndcube/asdf/resources/`, and the `asdf.extensions`
  entry point in `pyproject.toml`). This is a real capability with no representation anywhere else
  in the record, since the file-format vocabulary has no ASDF row (Fields 18/19).

**Considered and rejected:**
- **nddata** — also a repository topic, and meaningful, but it duplicates what `astropy` and
  `data container` already carry for a searcher. It lost on redundancy, not on accuracy: it is not
  a wrong keyword for this software, only one that adds nothing a searcher could not already reach
  through the two values above.
- **numfocus** — also a repository topic. It records a sponsorship relationship, not a subject, and
  no searcher looking for software would use it as a search term.

### 17. Data Sources (OPTIONAL)
- **Selected Values:** No value

**Cleared by decision.** HSSI held `Observatory/Mission-specific` before this refresh. The field is
defined as "The data input source the software supports.", and read as *where does this software get
its data from* the honest answer for ndcube is nowhere: the user supplies the array.

The factual position: **ndcube retrieves no data from any source.** The same search reported under
Field 4 — `requests`, `urllib`, `urlopen`, `download`, case-insensitive, over the whole `ndcube/`
package tree at the pin — reaches no Python file at all; its single hit is the word "downloaded" in
a prose README. There is no archive client, no query interface, no HTTP or FTP code of any kind.

**The asymmetry that decided it.** The field's own instruction pairs the observatory-specific value
with the Related Observatory field: "If observatory-specific, select 'observatory-specific' and
indicate the observatory/mission name in the Related Observatory field." That pairing cannot be
satisfied here — Field 32 is empty and, for the reasons set out there, correctly so. A value whose
prescribed companion field must remain empty is a value the field's own definition does not support.

**Considered and not determinative.** The opposite reading — the field as "what kind of data does
this software work with", under which observatory data is exactly what users load into a cube — is
coherent, is true of ndcube, and is presumably what the original submitter meant. It is preserved
here so a later refresh treats it as weighed rather than overlooked. It did not carry the decision
because the field names an input *source*, and ndcube has none; holding data that something else
fetched is not a source.

No other row in the live `DataInput` vocabulary applies under either reading, which is why the empty
value is correct rather than merely unfilled: ndcube touches none of
CDAWeb, HAPI, AMDA, das2, Madrigal, OMNIWeb, SSCWeb, TAP, VirES, WDC, GFZ, the Virtual Solar
Observatory, S3/cloud, or FTP/HTTP directories.

### 18. Input File Formats (RECOMMENDED)
- **Selected Values:**
  - FITS
  - Other

### 19. Output File Formats (RECOMMENDED)
- **Selected Values:**
  - Other

The two fields share one vocabulary and one body of evidence, so the reasoning is given once here.

**What ndcube actually reads and writes.** Exactly one format is implemented inside the package:
**ASDF**. `ndcube/asdf/` contains ten converters (for `NDCube`, `NDCubeSequence`, `NDCollection`,
`NDMeta`, `ExtraCoords`, `GlobalCoords`, the three WCS wrappers and the table coordinates), the
matching schemas and manifest under `ndcube/asdf/resources/`, and the `asdf.resource_mappings` /
`asdf.extensions` entry points registered in `pyproject.toml`. The documentation page
`docs/explaining_ndcube/asdf_serialization.rst` tells the user "To make use of these, simply save an
ND object to an ASDF file and it will be correctly serialized." **The live `FileFormat` vocabulary
has no ASDF row** — its rows are `ascii`, `CDF`, `csv`, `FITS`, `HDF5`, `IDL.sav`, `ISTP-Compliant`,
`JSON`, `netCDF3/4`, `Other` and `Zarr` — so `Other` is the only way this catalogue can express the
one format ndcube genuinely reads and writes, and that is why `Other` must stay on both the input and
the output side. `Other` was already stored for both and is kept. **On the output side this matters
more than anywhere else in the record: `Other` is the sole output value, so it is the only trace ASDF
has in this entry at all.** A later refresh that reads a lone `Other` as junk and deletes it would
erase the software's real file format from the catalogue.

**Why `FITS` stays on the input side.** ndcube contains no FITS reader. Searching the package tree at
the pin (`git grep -P -n 'astropy\.io\.fits|fits\.open' <pin> -- 'ndcube/**'`) returns a single
line, and it is a docstring type reference in `ndcube/ndcube.py`, not a call; `fits.open` occurs in
no file in the repository at all; and the one `from astropy.io import fits` in the package tree is
in a test module, `ndcube/tests/test_ndcube_slice_and_crop.py`. But the project documents
FITS ingestion as a first-class workflow: `docs/introduction.rst` states "Moreover, utilizing the
astropy WCS infrastructure enables us to directly read the most common file format in astronomy,
FITS.", and the gallery carries a dedicated example, `examples/creating_ndcube_from_fitsfile.py`,
whose title is "How to create an NDCube from data stored in a FITS file". `NDCube.reproject_to`
accepts an `astropy.io.fits.Header` as its target description, and `ndcube/wcs/tools.py` exists
specifically to reconstitute a FITS-WCS from ndcube's wrapper stack
(`unwrap_wcs_to_fitswcs`). A user filtering HSSI for FITS-capable software would be right to expect
ndcube back. Kept.

**Why `FITS` is not recorded on the output side.** `FITS` is dropped from Field 19, because no writer
exists. There is no `save` and no `write` method; `fits.open` occurs in no file in the repository at
all (`git grep -P -n 'fits\.open' <pin>` over the whole tree matches nothing, against the whole-tree
positive control `git grep -P -i -l '\bFITS\b' <pin>` matching 20 files); and the project's own wiki
roadmap lists "**NDCube.save/write**: Add a method to write out an `NDCube` to one of a set of
supported file types" as *future* work. The only statement in the documentation about writing FITS is
a warning that you cannot straightforwardly do it: `docs/explaining_ndcube/tabular_coordinates.rst`
says "If you wish to be able to serialise your NDCube object to FITS files you will need to manually
construct a WCS object using the ``-TAB`` convention."

**Considered and not determinative:** `ndcube/wcs/tools.py`'s `unwrap_wcs_to_fitswcs` does make a
FITS-WCS available to a user who performs the write themselves, which is a real argument for keeping
`FITS` on the output side and is kept visible so a later refresh weighs it rather than rediscovering
it. It did not carry the decision — handing a user a header they could write is not writing the
format, and a searcher filtering for software that produces FITS would not be well served by a
package that produces none.

**Removals applied — `HDF5` (both fields) and `netCDF3/4` (input).** HSSI held four input formats
(`FITS`, `Other`, `HDF5`, `netCDF3/4`) and three output formats (`Other`, `FITS`, `HDF5`) before this
refresh. `HDF5` and `netCDF3/4` were asserted by the 2025-12-02 extraction and are unsupported by
anything in the software. The measurement, run at the pin with no pathspec so that its scope is the
whole repository rather than the package directory: `git grep -P -i -l 'h5py|netcdf' <pin>` matches
**zero files** — not one file anywhere in the tree, including `docs/` and `examples/` — against the
whole-tree positive control `git grep -P -i -l '\bFITS\b' <pin>` matching 20 files, which shows the
search was capable of finding a format term that is genuinely present. Neither format is a
dependency, optional or otherwise.

`Zarr`, `CDF`, `ISTP-Compliant`, `IDL.sav`, `ascii`, `csv` and `JSON` were each checked against the
same tree and none applies. (The `.json` files tracked at the pin are figure-hash fixtures and
`.zenodo.json` — repository metadata, not a data format the software reads.)

### 20. Operating System (RECOMMENDED)
- **Selected Values:**
  - Operating System Independent
  - Linux
  - Mac
  - Windows

HSSI held `Operating System Independent` alone before this refresh. The three named platforms are
added **beside** that value rather than replacing it, following the same pattern this record uses
elsewhere of enriching a coarse value instead of trading it away.

`Operating System Independent` is true and stays: ndcube is pure Python with no compiled extension
and no platform-specific code, and the only platform conditional anywhere in the packaging is a
test-only dependency, `"pytest-memray; sys_platform != 'win32'"`.

**Why the three named rows are recorded as well.** The `OperatingSystem` vocabulary is flat:
`Operating System Independent` does **not** imply `Linux`, `Mac` or `Windows`, so that value on its
own would not surface this entry for a visitor filtering the catalogue by a named platform. The named
platforms are directly evidenced at the pin — the CI matrix in `.github/workflows/ci.yml` runs
`- linux: py314`, `- windows: py312` and `- macos: py312`, plus `- linux: py311-oldestdeps` and
`- linux: py313-minimal` — so each of the three is a tested, supported platform and not an inference
from portability.

**Considered and not determinative:** the single independent value is arguably the tidier statement
of the truth, and four values where one is logically sufficient is a redundancy. That was weighed and
lost to discoverability, which is what a platform field is read for.

All four names are copied byte-for-byte from the live vocabulary rows. Note the trap in the coarse
one: the row is `Operating System Independent` spelled out — `OS Independent` is not a row and would
be rejected.

### 21. CPU Architecture (RECOMMENDED)
- **Selected Values:**
  - CPU Independent

Carried over. Pure Python, no compiled extension, no architecture-specific code or wheels.

**Considered and rejected: `GPU`.** The prior dossier noted that ndcube can operate on CuPy-backed
arrays. The only support for that claim at the pin is the JOSS paper, and `cupy` appears nowhere
else in the repository — not in `pyproject.toml`, not in the package, not in the tests. What is true
is that ndcube is agnostic about the array type it holds; that is not the same as the software
requiring or targeting a GPU, which is what this field records.

### 22. Related Phenomena (OPTIONAL)
- **Selected Values:** No value

**Cleared by decision.** HSSI held `Coronal Mass Ejections`, `Solar Corona` and `Solar Flares` before
this refresh; all three are removed. The field is defined as "The phenomena the software supports
science functionality for." ndcube supports none of them. There is no flare detection, no CME
tracking, no coronal analysis — there is a container that will hold an array of anything.

The measured basis, case-insensitive over the whole tree at the pin: `git grep -P -i -l 'flare' <pin>`
and `git grep -P -i -l 'coronal mass' <pin>` each match **zero files**, and
`git grep -P -i -l 'corona' <pin>` matches exactly three — `.mailmap`, where it is part of a
contributor's old hostname, and `joss_paper/paper.md` and `joss_paper/paper.bib`, where it is part of
the PUNCH mission's full name. A contributor's old hostname and the two papers are the entire
presence of these phenomena anywhere in the software.

**Considered and not determinative.** The case for keeping the three values was the same "commonly
used for" reading argued under Field 5 — that the data people put into ndcube is very often coronal
imaging and flare spectroscopy — and it is preserved here rather than deleted, because it is the
argument a later refresh would otherwise rediscover and act on. It carried even less weight here than
it did there, for two reasons. Field 5's wording explicitly licenses "commonly used or intended for"
while this field's wording does not. And Field 5 at least had a downstream ecosystem behind it: the
packages built on ndcube that Field 30 names are predominantly solar and heliophysics tools. This
field has no equivalent support at all — no downstream package makes ndcube a flare, CME or corona
tool. Field 5 was cleared on the stronger case, so clearing this one follows a fortiori.

The remaining rows in the live `Phenomena` vocabulary — `Coronal Heating`, `Geomagnetic Storms`,
`Solar Wind` and `X-ray emission` — have no support here under any reading either, which is why the
empty value is the correct one rather than a gap awaiting a better-fitting row.

### 23. Development Status (RECOMMENDED)
- **Development Status:** Active

**HSSI held no value for this field before this refresh** (`developmentStatus` was null); this fills
it. The selected row's stored definition is "The project has reached a stable, usable state and is
being actively developed.", and both halves hold:

- *Stable and usable*: a long series of PyPI releases whose newest member is 2.4.1 (Field 12), a
  documented public API and a full documentation site. No release total is quoted: it is a
  third-party count that is wrong again at every release, and nothing here rests on it. Contrast the
  release-object count under Field 12, which is quoted and date-bound because there the number
  itself carries the argument.
- *Actively developed*: the pinned commit is dated 2026-09-03, and 99 commits land in the twelve
  months preceding it (`git rev-list --count --since=2025-09-08 <pin>`). The repository is not
  archived and not disabled; issues and pull requests are open and being filed.

**Alternatives rejected.** `Inactive` and `Unsupported` both require that development has stopped,
which the commit history refutes. The sharpest test is `Unsupported`'s own stored definition — "The
project has reached a stable, usable state but the author(s) have ceased all work on it. A new
maintainer may be desired." — and the 99 commits counted above contradict *ceased all work*
outright. `Inactive` fails on the same evidence, its definition turning on the project no longer
being actively developed. `WIP`, `Concept` and `Suspended` all describe a project
with no stable public release. `Moved` describes a relocated project — worth noting that the
*predecessor* `sunpy/cube` repository is archived, but ndcube is its successor, not a stale copy.

Note that no packaging classifier was available to shortcut this: `pyproject.toml` at the pin has no
classifier list at all, so no `Development Status ::` trove classifier exists to read.

### 24. Documentation (RECOMMENDED)
- **Documentation URL:** https://docs.sunpy.org/projects/ndcube

Carried over. What justifies the value is durable and in-repo: the project gives this URL in three
places at the pin — `pyproject.toml` lists it as both `Homepage` and `Documentation`, `README.rst`
links it under "Getting Help", and the PyHC registry's `docs:` field is the same string. It also
resolved when read on 2026-09-08, redirecting to `/en/stable/`, and the site carries the
installation guide the field asks for.

**Considered and rejected: the GitHub wiki.** This repository has a wiki, and it is not empty — five
pages, last edited 2025-01-14, covering a roadmap, testing tricks, a development-install guide and
release instructions. It is a *separate git repository* (`https://github.com/sunpy/ndcube.wiki.git`)
and is invisible from the code pin, which is why it has to be checked deliberately rather than
inferred from the repository's `has_wiki` flag. It is not recorded here: its content is
maintainer-facing and partly stale (the install page still describes a conda workflow around
`master`), and the Sphinx site is the user documentation. Its release checklist is cited elsewhere in
this file as evidence about the project's release process.

### 25. Funder (OPTIONAL)
- **Organization:** National Aeronautics and Space Administration
  **Funder Identifier:** https://ror.org/027ka1x80

The single stored funder is kept. The authoritative source is the Acknowledgements section of the
reference publication, whose text is in the repository at `joss_paper/paper.md`:

```
We acknowledge financial support for ndcube from NASA's Heliophysics Data
Environment Enhancement program, the Daniel K. Inouye Solar Telescope, and
Solar Orbiter/SPICE (grant 80NSSC19K1000).
```

NASA funds two of the three named sources (the HDEE program and the Solar Orbiter/SPICE grant), and
the stored organization name is already the expanded, non-acronym form the field asks for.

**Settled: the Daniel K. Inouye Solar Telescope is not recorded as a funder.** The acknowledgement
names DKIST as a source of financial support, so it was a legitimate Field 25 candidate and the prior
dossier listed it. The decision is that a facility is not a funding agency: money reaching a facility
comes from an agency, and it is the agency this field names.

**Both alternatives, considered and not determinative** — recorded with their real costs, because
these are precisely what a later refresh would otherwise re-propose as new findings:
- **Add `Daniel K. Inouye Solar Telescope` with no funder identifier**, faithful to the source's own
  wording. **DKIST has no ROR of its own** — a ROR search on 2026-09-08 returned no matching
  organization; the telescope is operated by the National Solar Observatory under AURA — so
  recording it would mint a
  new identifier-less Organization in the catalogue. Organizations are shared records, and no API
  path can rename one afterwards, so a name introduced this way could not be corrected by any routine
  metadata update. That durable cost, rather than any weakness in the citation, is what makes this
  option expensive.
- **Record `National Solar Observatory` (https://ror.org/00b9pg524) instead.** This is cleanly
  ROR-identified — that identifier's ROR display name is exactly "National Solar Observatory" — and
  NSO is the body that actually operates DKIST, so it carries none of the cost above. It is not
  recorded because the acknowledgement names DKIST and not NSO: the substitution is inference rather
  than evidence. The inference is a reasonable one; it is simply not what the source says.

**Rejected from this field:** `Solar Orbiter/SPICE`. The prior dossier listed it as a funder
organization; it is not one. It is the *award* the acknowledgement attaches a grant number to, and it
is recorded as such in Field 26.

### 26. Award Title (OPTIONAL)
- **Award Title:** NASA's Heliophysics Data Environment Enhancement program
  **Award Number:** Not found
- **Award Title:** Solar Orbiter/SPICE
  **Award Number:** 80NSSC19K1000

Both awards are recorded, and both come straight from the acknowledgement quoted under Field 25.
`Solar Orbiter/SPICE` is unchanged, identifier and all. The HDEE program carries no award number
because the acknowledgement attaches `80NSSC19K1000` to Solar Orbiter/SPICE alone and gives no number
for the program — the number is absent from the source, not merely unrecorded here. Both are named
rather than one because this field's stored value is the complete set of the entry's awards: a later
refresh that lists only one of the two would detach the other from the entry.

**The second award reached this entry as a row with an empty title.** It carried no title, no
identifier and no funder. An award with no title is not a value any submission or update path can
produce, so it did not arrive through one. Its identity is an **inference**, and worth reading as one:
the acknowledgement in `joss_paper/paper.md` names three funding sources, of which one is the
`Solar Orbiter/SPICE` award already recorded above and one is the Daniel K. Inouye Solar Telescope, a
facility rather than an award (see Field 25) — which leaves NASA's Heliophysics Data Environment
Enhancement program as almost certainly what the untitled row represented. That inference is a strong
one and it is what the repair acted on, but the row itself asserted nothing. A later reader should
treat the identification as well-grounded reasoning, not as something the catalogue ever stated.

**The correction was applied on 2026-09-08, directly against the catalogue's records.** The existing
row was given the title `NASA's Heliophysics Data Environment Enhancement program` and its funder was
set to the National Aeronautics and Space Administration already recorded under Field 25; no award
identifier was added, the acknowledgement naming none. It could not have been done any other way from
here: awards are shared records that other software in the catalogue may also reference, so retitling
one is not something a field patch from this entry can express — it belongs to whoever maintains the
catalogue's records directly. The date is recorded so that a reader who finds the row correctly titled
knows why, and so the repair is not proposed a second time.

**The alternative — adding a correctly-titled duplicate beside the blank row — was considered, and
lost on a specific ground.** It was a workable option: the acknowledgement names the program plainly,
the prior dossier recorded it as an award with no number, and the title is 56 characters, comfortably
inside the 128-character limit. It was not chosen because it would have left the entry displaying a
correctly-titled award *and* a blank one — adding an award does not repair an untitled row, and the
blank would have remained for whoever looked next. Correcting the row that already existed produced
the same information without the duplicate. This option was known and decided against; it was not
overlooked.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- **DOIs:**
  - https://doi.org/10.3847/1538-4357/ace0bd
  - https://doi.org/10.5281/zenodo.7020102

HSSI held the first of these before this refresh; the second is added.

**The ApJ paper — kept, unchanged.** This is the second of the two references
`docs/acknowledging.rst` asks users to cite: *Ryan, Mumford et al., "A Unified Framework for
Manipulating N-dimensional Astronomical Data and Coordinate Transformations in Python: The NDCube 2 &
Astropy APE-14 WCS APIs", Astrophysical Journal, 2023*. The JOSS paper is the reference publication
(Field 14) and this is the companion; the split between the two fields matches what the project
itself asks for and is not changed.

**SEP-0012 — added.** *SunPy Proposal for Enhancement 12: NDCube 2 (SEP 0012)*, Stuart Mumford,
issued 2020-10-13, typed "Technical note". It is the specification the NDCube 2 API was built to, so
it tells a reader something neither paper does — why the API looks the way it does. That is the
reason it is recorded: a reader trying to understand why ndcube's interface is shaped as it is has
nowhere else to go.

**Which DOI form is recorded, and how that was established.** The value above is the **concept** DOI,
`https://doi.org/10.5281/zenodo.7020102`, not the versioned deposit `10.5281/zenodo.7020103`. The
two are easy to confuse, and DataCite settles which is which: 7020102 carries a `HasVersion` relation
pointing to 7020103, and 7020103 carries the reciprocal `IsVersionOf` relation back to 7020102. So
7020102 is the concept and 7020103 is a version of it, and the concept DOI is what a reader should be
sent to, since it always resolves to the newest version of the proposal. When those relations were
read on 2026-09-08 the concept carried exactly one version, so the version-drift consequence
described under Field 2 for the software concept DOI does not arise here — and would only arise if
the proposal were ever redeposited.

**Considered and not determinative.** The field is explicitly for publications "the software
developer prioritizes", and the project signals its priorities by naming exactly two references in
`docs/acknowledging.rst`, of which SEP-0012 is not one; it is also a design document rather than a
scientific publication. Both objections are real and were weighed. They lost to the fact that the
proposal explains the software's API in a way neither paper does. Preserved here so that a later
refresh reads the case for removing SEP-0012 as one already made and answered, not as a fresh
discovery.

**The software concept DOI is not placed in this field.** One option for Field 2 would have put
`10.5281/zenodo.5715150` here instead of there; it is recorded in Field 2, where a software
identifier belongs. See Field 2.

**Considered and rejected: citing papers generally.** The JOSS and ApJ papers are cited by a large
and growing literature that uses ndcube through downstream packages. Enumerating those here would
add no discriminating information and would go stale immediately. This field is for publications the
developers prioritize, and they have said which two those are.

### 28. Related Datasets (OPTIONAL)
- **Value:** No value

Correctly empty. ndcube bundles no data, requires no specific dataset, and supports no dataset
specifically — it is a container for whatever array the user supplies. The gallery examples use
sunpy's sample-data images for illustration, which is a demonstration convenience and not a dataset
the software is built around. Nothing was stored for this field before this refresh either.

### 29. Related Software (OPTIONAL)
- **Values:**
  - https://github.com/sunpy/sunpy
  - https://github.com/spacetelescope/gwcs
  - https://github.com/astropy/reproject

**`https://github.com/sunpy/sunpy` — kept, with an argument rather than by inheritance.** ndcube is a
SunPy Project affiliated package: `docs/index.rst` at the pin opens "`ndcube` is a SunPy Project
affiliated package designed for handling N-dimensional data cubes described by WCS (World Coordinate
System) transformations", the README carries a "Powered by SunPy" badge, and sunpy is an optional
dependency (`sunpy>=6.1.0` in the `tests-optional` and `tests-minimal` extras). Knowing that ndcube
belongs to the SunPy Project is genuinely distinguishing information about it, which is the test this
field applies. The same URL also appears under Field 30 for a different and stronger reason (a shared
data model), and that duplication is deliberate — as of this refresh sunpy's own catalogue entry
names ndcube in both of its corresponding fields, so the relationship is recorded symmetrically from
both sides.

**`https://github.com/spacetelescope/gwcs` — added.** A required dependency (`gwcs>=0.24.0`) and a
domain-specific one: gWCS is the generalized coordinate-system implementation that lets ndcube
describe data whose coordinates do not fit the FITS-WCS model. `docs/explaining_ndcube/coordinates.rst`
explains the relationship in a sentence calling astropy's WCS implementation "a crucial pillar of
`ndcube`, as is the more generalized offshoot" before linking gWCS's own documentation — and
`examples/creating_a_gwcs_from_quantities.py` is a gallery example devoted to building one for use
with a cube. It characterizes the software rather than merely being present in the dependency list.

**`https://github.com/astropy/reproject` — added.** The optional dependency behind `NDCube.reproject_to`,
with its own documentation page and gallery example. It is a domain (astronomy) library, not generic
infrastructure, and its presence is what makes ndcube's regridding capability real.

**Considered and rejected:**
- **numpy** and **scipy** (both hard dependencies at the pin) — Tier A, never listed. "Depends on
  numpy" is true of nearly every package in the catalogue and distinguishes nothing.
- **matplotlib** and **mpl_animators** (the `plotting` extra) — generic plotting infrastructure.
  Applying the standing test: a plotting and animation toolkit is equally at home in a web app, a
  finance model or a biology pipeline, so it gets Tier A treatment whether or not it is named in the
  list. The prior dossier listed `https://matplotlib.org` here, which is also not a code repository
  URL.
- **dask** and **cupy** — see Field 30, where the argument is set out; neither belongs in this field
  either. A package excluded from Field 30 is not thereby a Field 29 entry.
- **specutils, jdaviz, sunraster, irispy, eispac** — these consume ndcube rather than distinguishing
  it, so they belong in Field 30 (where the ones with current evidence are recorded), not here.
- **`https://github.com/sunpy/cube`** — the archived predecessor repository whose 2015 history is
  grafted into ndcube's. This is the one genuinely arguable omission from this field, since Field 29
  explicitly covers "software this work was forked from". It is left out because the relationship is
  historical rather than useful: the repository is archived, its code is not what ndcube runs, and a
  reader following the link learns nothing about the current software. Recorded here so the decision
  is visible rather than accidental.

### 30. Interoperable Software (OPTIONAL)
- **Values:**
  - https://github.com/sunpy/sunpy
  - https://github.com/astropy/astropy
  - https://github.com/sunpy/sunraster
  - https://github.com/DKISTDC/dkist
  - https://github.com/LM-SAL/irispy
  - https://github.com/punch-mission/punchbowl
  - https://github.com/HERMES-SOC/hermes_core
  - https://github.com/astropy/specutils
  - https://github.com/USNavalResearchLaboratory/eispac

**HSSI held no values for this field before this refresh**, which was the largest single gap in the
record: ndcube's whole purpose is to be the data model other tools exchange, so an empty
interoperability field understated the software more than any other omission. Every entry below is
justified by a specific exchange, and each URL is the in-catalogue entry's own repository URL where
one exists, so that the link text a visitor sees is legible.

- **sunpy** — the shared `NDCube` data model. This is the canonical worked example of the field in
  HSSI's own field guidance, and the repository backs it: `examples/creating_even_spaced_wavelength_visualisation.py`
  builds an `NDCubeSequence` out of `sunpy.map.Map` objects, and
  `docs/explaining_ndcube/slicing.rst` crops a cube using `sunpy.coordinates.frames.Helioprojective`.
  In the other direction, sunpy's own packaging carried `"ndcube>=2.3.0"` in its `docs-gallery`
  extra when checked on 2026-09-08, so sunpy's documentation gallery is itself an ndcube user.
- **astropy** — Tier B, and the evidence is in the public API rather than the dependency list.
  `NDCube` subclasses `astropy.nddata.NDData`; `NDCube.to_nddata` exists specifically to convert a
  cube back into an astropy `NDData` subclass; astropy `WCS` objects are the native coordinate
  description; `NDCube.quantity` hands back an `astropy.units.Quantity`; arithmetic accepts
  `NDData` operands; and ASDF serialization is built on `asdf-astropy`. This is a documented,
  two-directional data-model exchange, not internal use.
- **sunraster**, **DKIST User Tools**, **irispy**, **punchbowl**, **HERMES Core**, **specutils**,
  **eispac** — packages built on the NDCube data model, which is exactly the "shared data model"
  exchange the field is for. Each declares ndcube as a dependency in its own packaging manifest
  (checked 2026-09-08: sunraster `"ndcube[all]>=2.3.2"`, DKIST User Tools
  `"ndcube[plotting,reproject]>=2.4.0"`, irispy — distributed as `irispy-lmsal` —
  `"ndcube>=2.4.0"`, punchbowl `"ndcube"`, HERMES Core `'ndcube>=2.2.0'`, specutils `ndcube>=2.0`,
  eispac `ndcube>=2.0.0`). ndcube's own JOSS paper names the same relationship from its side:
  `specutils [@specutils-docs; @specutils-code], jdaviz [@jdaviz], sunraster [@sunraster],` and
  `ndcube is also used in the data pipeline of the PUNCH mission`. For sunraster, DKIST User Tools,
  irispy, punchbowl and HERMES Core the URL above is the entry's own stored repository URL in this
  catalogue; specutils and eispac have no entry here, so their canonical GitHub repositories are
  used, as the field instructions allow.
- Note on irispy's two names: the repository was renamed, and as of 2026-09-08
  `https://github.com/LM-SAL/irispy-lmsal` redirects to `https://github.com/LM-SAL/irispy` while
  `irispy-lmsal` remains the distribution name declared in its packaging. The current repository URL
  is the one recorded, which is also the URL this catalogue stores for that entry.

**Considered and rejected, with reasons:**
- **numpy, scipy, matplotlib, mpl_animators, pytest and the packaging stack** — Tier A. Being a
  dependency is not interoperability.
- **dask** — the closest call in this field, and rejected. ndcube does accept dask-backed arrays:
  `ARRAY_MASK_MAP[dask.array.core.Array] = dask.array.ma.masked_array` in `ndcube/ndcube.py`
  registers dask masking, a `ndcube_2d_dask` test fixture exercises it, and `docs/introduction.rst`
  says arrays "can be handled by `numpy` and ``dask``". But that is array-backend agnosticism — the
  same property that lets ndcube hold a plain numpy array — rather than an exchange with a peer
  domain tool, and dask itself is generic parallel-array infrastructure that would be equally at home
  outside science. If a maintainer disagrees, this is the one Tier B judgement here worth revisiting;
  the evidence above is all there is.
- **cupy** — named only in the JOSS paper, absent from the packaging, the package and the tests.
- **jdaviz** — named in the 2023 JOSS paper as an ndcube-dependent package, and **checked again on
  2026-09-08: its current dependency list no longer contains ndcube** (it depends on specutils,
  which does). The relationship is now indirect, so jdaviz is not recorded. This is written down so a
  later refresh does not re-add it from the paper alone.
- **sunkit-image** and **sunkit-instruments** — sibling packages in the same GitHub organization, and
  natural-looking candidates for that reason alone. Their dependency manifests were read on
  2026-09-08 and **neither declares ndcube**; both build on sunpy directly. Organizational proximity
  is not interoperability, and they should not be re-proposed without new evidence.
- **"part of the standard scientific Python ecosystem" / "a PyHC member, so it interoperates with
  PyHC packages"** — the two justifications the field guidance singles out as never sufficient on
  their own. Neither is used here.

### 31. Related Instruments (OPTIONAL)
- **Value:** No value

Correctly empty, and empty by a **relevance** decision rather than a resolution failure. The field
lists instruments the software is *designed to support*: it reads, parses, calibrates or processes
that instrument's data, implements a convention specific to it, or is an instrument-team tool.
ndcube does none of these for any instrument. It contains no instrument-specific reader, no
calibration routine, no mission data convention; it holds arrays and their WCS, whatever produced
them.

Everything a reader might expect to see here was considered and excluded for a stated reason:

- **SDO/AIA.** A word-anchored whole-tree search at the pin
  (`git grep -P -i -l '\bAIA\b|atmospheric imaging' <pin>`) reaches three files: the two gallery
  examples `examples/changing_resolution_via_reproject.py` and
  `examples/creating_even_spaced_wavelength_visualisation.py`, both of which merely load
  `sunpy.data.sample` images, and `CHANGELOG.rst` line 106, which is the entry announcing the second
  of those two examples. That is a tutorial/demo name-drop, which the field's relevance gate excludes
  explicitly. The same search restricted to the package tree (`-- 'ndcube/**'`) reaches no file at
  all, so there is no AIA-specific code — no reader, no calibration, no convention.
- **Solar Orbiter SPICE.** Appears only in the funding acknowledgement (Fields 25/26). A grant that
  paid for development is not an instrument the software supports; ndcube cannot read a SPICE file.
- **IRIS, Hinode/XRT, DKIST instruments, JWST instruments.** These come from the JOSS paper's
  "Community Applications" section, which is careful about what it claims: ndcube "is already a
  dependency of various software tools that support" those observatories. The instrument support
  belongs to those packages — irispy, eispac, the DKIST user tools, specutils — and belongs in
  *their* HSSI records, not in the umbrella library's. The prior dossier listed five instruments here
  on exactly this basis, each with "Instrument Identifier: Not found"; all five are dropped.

The governing test settles it: a visitor on an instrument's page clicking "show software related to
this instrument" and receiving a general-purpose N-dimensional array container would be annoyed, not
helped. Because no candidate passes the relevance gate, no vocabulary resolution was needed.

**Why the prior dossier's five entries were dropped, precisely.** They were dropped for failing the
relevance gate above, and for nothing else. That they carried no identifier reflected only that
nobody had resolved them; it is not evidence that they were unresolvable. The controlled vocabulary
does carry rows for candidates named above — `Atmospheric Imaging Assembly`
(`https://spase-metadata.org/SMWG/Instrument/SDO/AIA`) for SDO/AIA, and
`Spectral Imaging of the Coronal Environment`
(`https://spase-metadata.org/SMWG/Instrument/SolarOrbiter/SPICE`) for Solar Orbiter SPICE, with
Solar Orbiter itself appearing on the observatory side as both
`https://spase-metadata.org/ESA/Observatory/SolarOrbiter` and
`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/SolO`. A later refresh that wants to re-open
any of these has to argue relevance; resolvability is not the obstacle.

One resolution mechanism is worth leaving behind, because it manufactures false negatives. The
SPICE row is invisible to a search over `name` and `abbreviation`: its name is
"Spectral Imaging of the Coronal Environment" and its abbreviation is the empty string, so the
acronym "SPICE" occurs nowhere in either field — only in the row's identifier and in its prose
definition. Search identifier path segments as well as names before concluding that an instrument
has no row.

Independently of all of the above: a name without a `https://spase-metadata.org/` identifier is
never a permissible value in this field, so none of the five could have been recorded in the
identifier-less form the prior dossier gave them, relevant or not.

### 32. Related Observatories (OPTIONAL)
- **Value:** No value

Correctly empty, for exactly the reasons given under Field 31 and against the same relevance gate.
The prior dossier listed seven observatories — SDO, IRIS, Hinode, Solar Orbiter, DKIST, JWST and
PUNCH — all drawn from the JOSS paper's account of what *downstream* packages support, and none of
them with an identifier. As under Field 31, the missing identifiers are not the reason they go:
resolvable observatory rows exist for several of them, and the exclusion is a relevance judgement.
Each is dropped: ndcube is observatory-agnostic, and an association here
would misdirect anyone browsing from an observatory page. PUNCH is the strongest of the seven, since
the PUNCH pipeline (punchbowl) genuinely runs on ndcube — but that is a software-to-software
relationship, and it is recorded where it belongs, in Field 30.

### 33. Logo (OPTIONAL)
- **Logo URL:** https://raw.githubusercontent.com/sunpy/ndcube/0bf111ddf5c4e06899ce21c63a9c2a60833d682d/docs/logo/ndcube.png

Carried over unchanged, and verified to be correct rather than merely plausible. The stored URL is
pinned to commit `0bf111ddf5c4e06899ce21c63a9c2a60833d682d` ("Updates from the package template
(#957)", 2026-08-20), which is an ancestor of this dossier's pin, and `docs/logo/ndcube.png` is
**byte-identical at both commits** — sha256 `cfe03db8d9c6d6748526d5ce73ba527f8bf6d97b931fa80eb22040495d7ec8b9`,
41,388 bytes. So the pinned URL already serves the current image, and no re-pinning is needed. The
URL returned that same 41,388-byte file as `image/png` when read on 2026-09-08 — the response bytes
hash to the sha256 above, so what a visitor receives is byte-for-byte the git blob at the pin — and
the image is a stylised blue "N" with a serpent, set inside an open cube with stars — a genuine
project logo, not a plot or a screenshot. The file is not Git-LFS-tracked (the repository has no
`.gitattributes` at the pin), so the `raw.githubusercontent.com` host is correct and no
`media.githubusercontent.com` form is needed. The whole URL is well inside the 200-character field limit.

**Why the commit-pinned form, and why not the alternatives:**
- The PyHC registry gives this logo as
  `logo: "https://raw.githubusercontent.com/sunpy/ndcube/master/docs/logo/ndcube.png"` — a **branch**
  URL naming a branch that does not exist on the remote. Read on 2026-09-08,
  `git ls-remote --heads origin` returned exactly three refs — `2.4`, `Cadair-patch-1` and `main` —
  with no `refs/heads/master`, and GitHub reported `default_branch: main`. That URL nevertheless
  returned HTTP 200, `image/png`, 41,388 bytes the same day, hashing to the same sha256 recorded
  above for the pinned blob. **Why it still serves is not established here and is deliberately not
  guessed at** — the measurement is what matters, and it is a far stronger reason to pin than "it
  works today" would be: the apparent health of a branch URL does not even depend on the branch it
  names existing, so its continuing to serve the right bytes tells a later maintainer nothing about
  whether it will. The pinned form is what the catalogue needs, because a branch URL
  breaks silently if the file moves, and it would swap the catalogue's image without anyone noticing
  if the logo were redesigned. A logo change is something a refresh should record deliberately.
- `docs/acknowledging.rst` at the pin links the logo *directory* at yet another commit
  (`.../tree/ee94395cda5c8348a33bd1f9ff75fab976bdc66f/docs/logo`). That is a directory listing page,
  not an image, and is not usable as a value.
- `docs/logo/` also contains `ndcube.svg` and `ndcube.pdf`. The SVG would be a defensible
  alternative — it scales — but the PNG is what the project publishes to the PyHC registry and what
  HSSI already stores, and swapping formats for no functional gain would be churn.
- A `blob/` page URL, with or without `?raw=true`, is not used: it depends on a redirect and can
  serve HTML.
