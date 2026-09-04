# HSSI Metadata Extraction Results

**HSSI Software ID:** 639d2860-fa67-457c-af68-46b6b392fc74
**Repository:** https://github.com/space-physics/NEXRAD
**Source Revision:** 78cf657807b4a6cf8e5bba60918deddd2efd8395
**Extraction Date:** 2026-09-02
**Validation Date:** 2026-09-03
**Validation Status:** PASS

---

## Scope note — how to read the evidence in this file

The pinned revision `78cf657807b4a6cf8e5bba60918deddd2efd8395` is simultaneously three things: the
repository's final commit, the head of its default branch `main`, and the commit tagged `v1.0.0`
(`git rev-list --count v1.0.0..origin/main` is 0). The repository is **archived** on GitHub. There is
therefore no "current development state" that differs from the released state — everything below is
drawn from that single revision and describes both the release and the project's permanent condition.

Two consequences worth carrying forward:

- The repository will not change again unless a maintainer un-archives it, so field values sourced
  from the repository are stable and do not need periodic re-derivation for drift. What *can* change
  is the outside world: new citing publications, new controlled-vocabulary rows, a Zenodo or PyHC
  registry edit.
- GitHub's `updated_at` timestamp for this repository is 2026-07-08, long after the last commit. That
  field tracks repository-object metadata (stars, topics, archive flag), **not** commit activity. Its
  `pushed_at` is 2021-04-27T05:40:32Z, which is the real last-activity date. Do not read `updated_at`
  as evidence of maintenance.

The repository has no wiki: `git ls-remote https://github.com/space-physics/NEXRAD.wiki.git` reports
that the repository is not found. GitHub's API reports `"has_wiki": true`, but that flag only means the
wiki *feature* is enabled, not that any wiki content exists. So there is no wiki source for Fields 12
or 24.

At the pin the repository contains **21 tracked paths**; **65 commits** are reachable from the pin,
and **43 distinct tracked paths** have existed across all of them. All ten tags (`v0.6.0` through
`v0.6.8`, and `v1.0.0`) are ancestors of the pin — this repository's tags are all on the pinned
lineage, so tag-based evidence here is trustworthy.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

This is the catalogue's placeholder convention for an entry we did not originally submit; it is not a
missing value to be repaired.

### 2. Persistent Identifier (RECOMMENDED)
**Value:** https://doi.org/10.5281/zenodo.1402628

This is the Zenodo **concept** DOI — the version-independent identifier that always resolves to the
latest release. Zenodo's record for `10.5281/zenodo.4722449` reports `conceptrecid` `1402628` and
`conceptdoi` `10.5281/zenodo.1402628`, confirming the relationship.

The concept-DOI-here / version-DOI-in-Field-12 split is deliberate and correct, not a duplication:
Field 2 holds `10.5281/zenodo.1402628` (concept, all versions) and Field 12 holds
`10.5281/zenodo.4722449` (the `v1.0.0` release specifically). A future refresh should preserve that
arrangement rather than collapsing the two.

**Only two Zenodo versions exist under this concept**, not one per git tag — the Zenodo API's
`all_versions` query for `conceptrecid:1402628` returns exactly 2 records:

| Zenodo recid | Version DOI | Tag | Date | Deposit title |
|---|---|---|---|---|
| 1402629 | `10.5281/zenodo.1402629` | `v0.6.8` | 2018-08-23 | `scivision/NEXRADutils` |
| 4722449 | `10.5281/zenodo.4722449` | `v1.0.0` | 2021-04-27 | `space-physics/NEXRAD: src/ layout` |

The two version DOIs are **one digit apart from the concept DOI** — `10.5281/zenodo.1402628` (concept)
versus `10.5281/zenodo.1402629` (the v0.6.8 version). They are easy to conflate and mean different
things. The v0.6.8 version DOI is the one the citing publication in Field 27 points at.

The v1.0.0 deposit's `related_identifiers` is
`[{"identifier": "https://github.com/space-physics/NEXRAD/tree/v1.0.0", "relation": "isSupplementTo", "scheme": "url"}]`
— an `isSupplementTo` relation pointing at a GitHub `tree` URL is the signature of an automated
GitHub-Zenodo integration deposit rather than a manual upload. Its `resource_type` is
`{"title": "Software", "type": "software"}`, so the DOI cites as software rather than as an article.

**Note on Zenodo's own metadata errors.** The v1.0.0 deposit records `"license": {"id": "other-open"}`
and DataCite's record for the concept DOI records only
`"rightsList": [{"rights": "Open Access", "rightsUri": "info:eu-repo/semantics/openAccess"}]`.
Neither reflects the repository's actual MIT licence. This is the known DOI-autofill error class:
Zenodo's deposit metadata is copied verbatim by autofill, errors included. Field 15 is derived from
the repository's own `LICENSE` file instead, and a future refresh must not "correct" it back to
Zenodo's value.

### 3. Code Repository (MANDATORY)
**Value:** https://github.com/space-physics/NEXRAD

**Repository rename chain — the full, durable version.** The project has been renamed at least three
times, changing both owner and name. The chain is reconstructible from the `url` field that each
tagged `setup.py`/`setup.cfg` declared. All the genuine earlier URLs still redirect to the current
one; a fifth declared URL never resolved at all and is documented under the table:

| Declared repository URL | Declared by | Resolves today to |
|---|---|---|
| `https://github.com/scivision/nexrad-quickplot` | `setup.py` at tags `v0.6.0`-`v0.6.1` | nothing — 404, with no redirect |
| `https://github.com/scivision/nexrad-quick-plot` | `setup.py` at `v0.6.2`-`v0.6.3`; `setup.cfg` at `v0.6.4`-`v0.6.7` | `https://github.com/space-physics/NEXRAD` |
| `https://github.com/scivision/nexradutils` | `setup.cfg` at tag `v0.6.8` | `https://github.com/space-physics/NEXRAD` |
| `https://github.com/space-physics/nexradutils` | `setup.cfg` at the pin; also PyPI `home_page` | `https://github.com/space-physics/NEXRAD` |
| `https://github.com/space-physics/NEXRADutils` | PyHC registry `code:` field | `https://github.com/space-physics/NEXRAD` |
| `https://github.com/space-physics/NEXRAD` | GitHub `full_name` today | (current) |

**The one-hyphen URL is the outlier, and it is almost certainly a typo rather than a lost
repository.** `https://github.com/scivision/nexrad-quickplot` — one hyphen, declared at `v0.6.0` and
`v0.6.1` — is the only historical URL that does not resolve: it returns 404 and issues no redirect,
whereas the two-hyphen `nexrad-quick-plot` and both `nexradutils` forms all redirect to the current
repository. GitHub preserves a redirect for every rename, so a name the project genuinely used would
still resolve today. The likeliest explanation is that the one-hyphen spelling was a mistake in
`setup.py` corrected at `v0.6.2`, and that no repository ever existed under it. Recorded so that a
future agent searching for artifacts under that spelling expects to find nothing, and does not read
the absence as evidence of a deleted repository.

Two things matter downstream. First, the owner changed (`scivision` to `space-physics`) as well as the
name, so a search that only tries name variants under one owner will miss earlier artifacts. Second,
because the genuine old URLs redirect, an external reference to an old name still resolves — which is
why the PyHC registry entry and the pinned `setup.cfg` both look correct in a browser while naming a
repository that no longer exists under that name. This is context for interpreting sources, not a
defect to repair in those sources.

An earlier revision of this file carried only the note
`Repository was previously named "NEXRADutils" but was renamed to "NEXRAD"`. That is true but
incomplete — it omits the owner change and the original `nexrad-quick-plot` name, both of which are
needed to search for artifacts.

GitHub reports `"fork": false`, so this is not derived from another repository; there is no fork parent
to record under Field 29.

### 4. Software Functionality (RECOMMENDED — treated as critical)
**Values:**
- Coordinate Transforms
- Data Processing and Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Data Reduction
- Data Processing and Analysis: Image Processing
- Data Visualization
- Data Visualization: 2D Graphics

Values are written fully qualified as `Parent: Child`. That is required here rather than stylistic: in
the 83-row functionality vocabulary, 13 child names recur under more than one parent (`2D Slices`,
`ML/AI`, `Spectrogram`, `Mission-Specific`, `Processing`, `Calibration`, `Analysis`,
`Distribution/Access`, `Field-line Tracing`, `Infrastructure as Code`, `Instrument Response`,
`Observatory/Instrument Models`, `Packet Decommutation`), so a bare child name is ambiguous.

Every recorded child's parent is also recorded, so there is no parentless-child defect.

**Code evidence at the pin for each recorded value:**

- **Coordinate Transforms** — `wld2mesh()` in `src/nexradutils/io.py` converts the six ESRI world-file
  parameters into geodetic latitude/longitude vectors. Its docstring reads
  "converts .wld to lat/lon mesh for Cartopy/Matplotlib plots" and
  "assumes the .wld file is EPSG:4326 coordinates (WGS84)". The result is user-facing: `load()`
  attaches those vectors as the returned array's `lat`/`lon` coordinates, and `README.md` documents
  that `.lat` and `.lon` are vectors of geodetic latitude and longitude computed from the `.wld` file
  corresponding to the images.
- **Data Processing and Analysis: Data Access and Retrieval** — `download()` and `urlretrieve()` in
  `src/nexradutils/io.py` fetch imagery over HTTPS with `requests` from
  `STEM = "https://mesonet.agron.iastate.edu/archive/data/"`. `download()` is re-exported from the
  package root (`from .io import load, loadkeogram, download  # noqa: F401`) and driven in parallel by
  the `concurrent.futures.ProcessPoolExecutor` in `src/nexradutils/download.py`.
- **Data Processing and Analysis: Data Reduction** — the `downsample` branch of `load()` calls
  `st.downscale_local_mean` (i.e. `skimage.transform.downscale_local_mean`), reducing a
  5400 x 12200 image by an integer factor. `test_load_downsample` in
  `src/nexradutils/tests/test_mod.py` exercises it and asserts the reduced shape.
- **Data Processing and Analysis: Image Processing** — `load()` slices the RGB channels off an RGBA
  input, builds a no-signal mask (`img[..., :3].all(axis=2) == 0`) and rewrites those pixels to white,
  in addition to the downsampling above.
- **Data Visualization / Data Visualization: 2D Graphics** — `overlay2d()` in
  `src/nexradutils/plot.py` renders the georeferenced image with `ax.imshow` on a Cartopy
  `PlateCarree` projection with coastlines, state boundaries, gridlines and formatted lat/lon tick
  labels; `keogram()` renders the stacked time-longitude image, also with `imshow`.

**Why `Coordinate Transforms` is correctly recorded with no subcategory.** The six available
subcategories are `Heliospheric`, `Ionospheric`, `Magnetospheric`, `Mission-Specific`, `Planetary` and
`Solar`. The transform this software performs is a geodetic/map-projection one (world-file affine
parameters to WGS84 latitude/longitude). None of the six describes it: it is neither a space-physics
frame conversion nor a spacecraft-attitude transform. The bare top-level value is the correct and
complete answer, and this enumeration is the reason — not an omission awaiting repair.

**Candidates evaluated in this refresh and not selected.** The vocabulary now stands at 83 rows, so
the relevant question is which *new* values apply, not merely whether the recorded ones still hold.
Every value below was examined against the pinned code and rejected; the reasoning is recorded so a
future refresh does not re-litigate it. Category wording quoted below comes from the project's
`software-functionality` classification guide. The HSSI `FunctionCategory` rows themselves carry no
descriptions — 0 of the 83 rows has a non-empty definition — so there is no "vocabulary definition" to
appeal to.

- **`Data Visualization: Movies`** ("Animations or video from data sequences") — **not selected.**
  `nexrad_loop()` in `plot.py` does write one `map<timestamp>.png` per input file, and when an output
  directory is given `genplots()` prints
  "ImageMagick can convert the PNGs to animated GIF by a command like:" followed by
  `convert map2018-0101T09*.png out.gif`. But the software never produces an animation: it emits a
  still-image sequence and *tells the user a shell command* to assemble one with an external tool it
  does not invoke or depend on. Selecting this would tell a catalogue reader the package makes movies,
  which it does not.
- **`Data Processing and Analysis: Time Series Analysis`** ("Analysis of time-ordered data", with
  examples of temporal filtering, trend analysis and autocorrelation) — **not selected.**
  `loadkeogram()` orders files by timestamp and stacks a constant-latitude cut along a `time`
  coordinate, so the output is time-ordered, but no temporal operation is applied to it: no filtering,
  no detrending, no correlation, no resampling. Stacking is not analysis.
- **`Data Visualization: 2D Slices`** ("Visualizing 2D slices of 3D data") and
  **`Data Processing and Analysis: 2D Slices`** ("Extracting 2D cross-sections from 3D data volumes")
  — **not selected**, and this is the closest call of the set, so both sides are recorded. *For:* a
  keogram genuinely is a constant-latitude cut through a (latitude, longitude, time) data space,
  rendered as a 2D longitude-time image, and `loadkeogram()` does call
  `img.sel(lat=ilat, method="nearest", tolerance=0.1)` to take the cut. *Against:* the software never
  holds a 3D volume — `loadkeogram()` loads one independent 2D image at a time and writes each cut
  into the output array, so there is no volume to slice; and in this taxonomy `2D Slices` sits beside
  `3D Particle Distribution Processing`, `Curlometer` and `Magnetic Null Finding`, which locates it in
  the volumetric-data idiom (simulation cubes, velocity distributions). A user filtering HSSI for
  `2D Slices` tooling is looking for the latter. The keogram capability is already carried by
  `Data Visualization: 2D Graphics`.
- **`Data Processing and Analysis: Analysis`** ("General scientific analysis beyond basic processing")
  — **not selected.** Despite being the taxonomy's easy-to-forget catch-all, it does not fit: the
  package computes no derived physical quantity. It does not even convert the RGB pixel values to dBZ
  — `README.md` documents the -32 dBZ to 90 dBZ / 0.5 dBZ scaling for the reader's benefit, and
  `doc/n0q_ramp.png` is pasted into the figure as a legend image, but no code performs the mapping.
  The returned array is `uint8` RGB throughout.
- **`Data Processing and Analysis: Processing`** — **not selected.** Redundant: the specific
  operations the package performs are already captured by `Image Processing` and `Data Reduction`, and
  adding the generic sibling would carry no additional information.
- **`Data Processing and Analysis: File Format Conversion`** — **not selected.** The package reads
  PNG plus a `.wld` sidecar and writes PNG figures. It converts nothing between data formats; the
  output is a rendering, not a re-encoding.
- **`Data Visualization: Line Plots`** — **not selected.** Every rendering path goes through
  `imshow`; there is no line-chart call. (`ax.plot(lb[0], lb[1], "bo", markersize=7, transform=GREF)` in
  `overlay2d()` draws single marker points for optional city labels, not a line plot.)
- **`Data Visualization: Spectrogram`** and **`Data Processing and Analysis: Spectrogram`** — **not
  selected.** A keogram superficially resembles a dynamic spectrum, but its vertical axis is longitude,
  not frequency, and no transform is computed. Recording either would mislead.
- **`Models and Simulations`** and any subcategory, **`Mission-related`** and any subcategory,
  **`Servers and Environments`** and any subcategory — **not selected.** The package models nothing,
  is not part of any mission ground system, and provides no server or environment infrastructure.

### 5. Related Region (RECOMMENDED — treated as critical)
**Values:**
- Earth Atmosphere
- Earth Lower and Middle Atmosphere
- Earth Ionosphere

`Earth Lower and Middle Atmosphere` and `Earth Ionosphere` were both added in this refresh; the
record carried `Earth Atmosphere` alone beforehand. The three are ordered broad term, then the region
the data measures, then the region the software is intended to serve.

**A structural fact that governs all three.** The 24-row `Region` vocabulary is **flat**. Parent and
child rows both exist, but a coarse value never implies a fine one and a fine value never implies its
parent. So "`Earth Atmosphere` already encompasses it" was never an argument for leaving a finer
region off, and "adding the finer ones makes the coarse one redundant" is not an argument for
dropping it now. Each value stands or falls on its own, which is why all three are recorded rather
than only the narrowest.

**What the field asks — this is what decided the harder of the two additions.** The form reference
defines Field 5 as "The physical region the software supports science functionality for." and
instructs the submitter to
"Select all physical regions the software's functionality is commonly used or intended for."
Both sentences are quoted byte-exact from `resource_submission_form_fields.md`. The clause *intended
for* is decisive: the field does not ask only where the software's data physically sits, it asks
where the software's functionality is commonly used **or intended** to be used. An author-stated
intended application is therefore squarely inside what the field asks about, not outside it.

**`Earth Lower and Middle Atmosphere` — recorded on the data itself.** The physical measurement this
software handles is NEXRAD N0Q composite base reflectivity: radar returns from precipitation and
other hydrometeors in the **troposphere**. That is squarely the lower atmosphere, and it is a direct,
unambiguous property of the data rather than an inference. The value was absent until this refresh
because this record's metadata was first extracted before the current 24-row Region list came into
use — the field reference dates that list to a 2026-07-29 snapshot and notes that until that audit
the documented list carried only five values — so its earlier absence was an artefact of the coarser
list available at the time, not a considered rejection. The one point that cuts the other way,
recorded so it is not mistaken for an oversight: the software itself is agnostic about altitude — it
renders images and never computes a height.

**`Earth Ionosphere` — recorded on the software's intended application.** The software's stated
purpose is ionospheric, and the evidence is first-party and corroborated. The PyHC registry entry,
written by the author, describes it as being for ionospheric perturbations; HSSI's own concise
description (Field 9) says "for ionospheric perturbation studies"; and the sole publication that
formally cites the software (Field 27) uses it to correlate tropospheric weather with **traveling
ionospheric disturbances** — the intended application actually realised in the literature. Under the
*intended for* clause quoted above, that is precisely what Field 5 is asking for, which is why the
value stands even though the code never computes an ionospheric quantity.

**A permanent caveat on how the ionospheric value should be read — it was chosen with this fact in
hand.** The strings "ionosphere" and "ionospheric" appear **nowhere in this repository**: a
case-insensitive search for `ionosph` across the tracked files of every one of the 65 commits
reachable from the pin returns zero files. The ionospheric framing is entirely external to the code,
coming from the author's own registry entry and from how the software was used in a paper, not from
the code, README, or package metadata. `Earth Ionosphere` therefore records an *intended
application*, not a region the software represents or computes in. A future refresh that rediscovers
the repository silence should read it as a known and accepted property of this value rather than as
evidence the value is wrong — and equally should not restate the value's basis as something the code
supports, because the code does not.

**Framed from a site visitor's side**, which is how the balance was struck: someone browsing HSSI by
`Earth Lower and Middle Atmosphere` finds exactly what the data is. Someone browsing by
`Earth Ionosphere` finds a package that supplies tropospheric weather context for ionospheric
studies — useful to the community that actually cites it, and exactly what this entry's own concise
description promises them. Someone browsing by the broad `Earth Atmosphere` finds it as before.

**Not candidates.** `Earth Thermosphere` — no thermospheric data or function. `Earth Auroral
Subregion`, `Earth Inner Magnetosphere`, `Earth Outer Magnetosphere`, `Earth Magnetosheath`,
`Earth Magnetosphere`, `Earth Magnetotail` — no magnetospheric content. All solar, heliospheric,
interplanetary and planetary rows (`Chromosphere`, `Corona`, `Photosphere`, `Solar Environment`,
`Solar Interior`, `Solar Wind`, `Heliosheath`, `Interplanetary Space`, `Jupiter Magnetosphere`,
`Mars Magnetosphere`, `Neptune Magnetosphere`, `Saturn Magnetosphere`, `Uranus Magnetosphere`,
`Planetary Magnetospheres`) — out of scope for a terrestrial weather-radar tool.

### 6. Authors (MANDATORY)
**Author 1:**
- **Author Name:** Michael Hirsch
- **Author Identifier:** https://orcid.org/0000-0002-1637-6526
- **Affiliations:**
  - **Organization:** Boston University — **Affiliation Identifier:** https://ror.org/05qwgg493
  - **Organization:** Scivision, Inc. — **Affiliation Identifier:** Not found

This author is a single person, correctly represented, with the ORCID already established in the HSSI
record. The identifier is unchanged.

**Michael Hirsch — author identity and identifier.** The identifier recorded here is
`https://orcid.org/0000-0002-1637-6526`. Four independent lines of evidence support it, and they do
not all key on the same string:

1. **The ORCID public record itself.** `0000-0002-1637-6526` is Michael Hirsch, Research Scientist in
   the ECE department at Boston University since 2018-08. Its 18 work groups include *PyMap3D: 3-D
   coordinate conversions for terrestrial and geospace environments* (`10.21105/joss.00580`),
   *h5fortran: object-oriented polymorphic Fortran interface for HDF5 file IO*
   (`10.21105/joss.02842`), *The State of Fortran*, and a series of auroral and ionospheric papers
   including *The Mysterious Green Streaks Below STEVE* and *Reconstruction of Fine-Scale Auroral
   Dynamics*. That is a geospace-software profile, matching this package's domain.
2. **A sibling repository's own citation file.** `geospace-code/pymap3d`'s `CITATION.cff` pairs
   `orcid: 0000-0002-1637-6526` with `name: SciVision` — linking the identifier to the same
   SciVision identity this package's author uses. The CFF stores the bare ORCID without the
   `https://orcid.org/` prefix.
3. **This repository's own author metadata.** `setup.cfg` at the pin declares
   `author = Michael Hirsch, Ph.D.` and `author_email = scivision@users.noreply.github.com`. The
   pinned commit's git author is `Michael Hirsch <scivision@users.noreply.github.com>`; the other 64
   commits reachable from the pin are authored by
   `Michael Hirsch, Ph.D <scivision@users.noreply.github.com>`. Those are the only two author
   identities in the pinned lineage. A GitHub `users.noreply.github.com` address is authoritative
   attribution to the login it names, and the login `scivision` is GitHub account id 10931741.
4. **Third-party, publisher-asserted corroboration.** Crossref's author list for
   `10.1029/2018GL080239` — the Geophysical Research Letters paper that formally cites this software
   (Field 27) — gives `Michael Hirsch` with ORCID `https://orcid.org/0000-0002-1637-6526`, asserted by
   the publisher. ADS's independent record for the same paper (`2018GeoRL..4510903M`) lists the same
   ORCID in the fourth author position. This is confirmation from outside the author's own control.

*A correction to earlier prose in this file.* An earlier revision stated that this repository's git
history records the author as `Michael Hirsch <10931741+scivision@users.noreply.github.com>`. That is
**wrong for this repository**: no commit reachable from the pin uses the numeric-prefixed noreply
form. Every commit uses the older, unprefixed `scivision@users.noreply.github.com`. The identity
conclusion is unaffected — the unprefixed noreply address names the login directly, and the account-id
mapping (10931741 to `scivision`) is independently verifiable from GitHub's user API — but the
specific email string should not be re-quoted from that sentence.

*Rejected alternative — do not reintroduce it.* `https://orcid.org/0000-0001-6183-6256` was recorded
for this author in an earlier revision of this file and is **wrong**. That ORCID belongs to a different
person of the same name: a Senior Facility Scientist at the Science and Technology Facilities Council's
Central Laser Facility, with earlier affiliations at Brunel University and at Leipzig University's
Mathematics department. Its 29 work groups are entirely single-molecule fluorescence microscopy,
EGFR/HER3 receptor biophysics and related detector work — titles such as *A small molecule inhibitor of
HER3: a proof-of-concept study*, *A global sampler of single particle tracking solutions for single
molecule microscopy*, and *Nanometric molecular separation measurements by single molecule
photobleaching*. That record contains no heliophysics, no geospace and no software. A future refresh
that encounters the value must reject it rather than restore it.

**The `Scivision, Inc.` affiliation has a first-party primary source.** The author's own v0.6.8
Zenodo deposit — `https://doi.org/10.5281/zenodo.1402629`, the same deposit the citing publication in
Field 27 references — records
`"creators": [{"name": "Michael Hirsch, Ph.D.", "affiliation": "SciVision, Inc."}]`. That is the
author asserting the affiliation himself, which is stronger evidence for the affiliation's existence
than an inference from his company identity. As a matter of fact, the deposit spells the organisation
with a capital V while HSSI's stored row spells it `Scivision, Inc.`; that difference is noted below
and is not something to act on.

**Affiliation `Scivision, Inc.` has no ROR, and this is a settled negative finding.** A ROR API search
for `Scivision` returns exactly one organisation: `https://ror.org/011qev639`, **SciVision Biotech
Inc. (Taiwan)** — a Kaohsiung-based biotech company (`"types": ["company"]`, website
`https://www.scivision.com.tw`). It is unrelated to Michael Hirsch's SciVision. Broader queries
(`SciVision Inc`, `Scivision, Inc.`) surface the same Taiwanese record at the top followed by
unrelated substring matches such as `Instituto de Neurologia de Curitiba` and
`Christian Heritage College`. **Do not attach `https://ror.org/011qev639` to this affiliation.** The
correct state is an affiliation with no identifier.

`Boston University`'s ROR `https://ror.org/05qwgg493` is confirmed: the ROR record's `ror_display`
name is exactly `Boston University`, located in Boston, with acronym `BU`. The stored affiliation name
matches the ROR display name.

**The `Scivision, Inc.` / `SciVision, Inc.` capitalisation difference is parked catalogue-wide.** It
is not a defect of this record, is not an open question here, and should not be raised in a future
refresh of this entry.

**No co-authors were omitted.** The pinned lineage has one author identity (two spellings of the same
person). There is no `CITATION.cff`, `AUTHORS`, `CONTRIBUTORS`, `codemeta.json` or `.zenodo.json` file
in this repository at the pin or anywhere in its history, so there is no additional contributor list to
reconcile. Zenodo's deposit for `v1.0.0` lists a single creator,
`{"name": "Michael Hirsch", "affiliation": null}`; DataCite's record for the concept DOI lists a single
`Personal` creator `Hirsch, Michael` with an empty `affiliation` array. Both agree with the
single-author reading, and neither of those two records supplies an affiliation. The
`Boston University` affiliation therefore rests on the ORCID employment record; the
`Scivision, Inc.` affiliation has its own first-party source in the v0.6.8 Zenodo deposit, recorded
above.

### 7. Software Name (MANDATORY)
**Value:** NEXRADutils

**Alternate names, and why `NEXRADutils` is the right one.** This project's naming is genuinely
tangled, and the packaging history explains why the stored value is correct rather than arbitrary.

The source has declared **three distinct distribution names** over its history:

| Declared name | Where | Tags |
|---|---|---|
| `NEXRAD_quickplot` | `setup.py` (`name='NEXRAD_quickplot'`) | `v0.6.0`-`v0.6.3` |
| `NEXRAD_quickplot` | `setup.cfg` (`name = NEXRAD_quickplot`) | `v0.6.4`-`v0.6.7` |
| `nexradutils` | `setup.cfg` (`name = nexradutils`) | `v0.6.8` |
| `NEXRAD-quickplot` | `setup.cfg` (`name = NEXRAD-quickplot`) | the pin / `v1.0.0` |

**The distribution name declared in the pinned `setup.cfg` is not registered on PyPI.** Checked against
PyPI's authoritative JSON and Simple APIs. The HTML project page is bot-gated and serves a page even
for names that do not exist, so it proves nothing either way:

| Name | PyPI JSON API | PyPI Simple API |
|---|---|---|
| `NEXRADutils` | registered | redirects to the canonical `nexradutils`, which serves |
| `NEXRAD-quickplot` | not registered | not registered |
| `nexrad-quickplot` | not registered | not registered |
| `nexrad_quickplot` | not registered | not registered |
| `nexrad` | not registered | not registered |

The published distribution is `nexradutils` version `1.0.0`, sole file `nexradutils-1.0.0.tar.gz`,
uploaded 2021-04-27T05:35:37Z. **Identity is closed by matching the record's contents, not by the name
resembling the repository**: the published `home_page` and `project_urls.Homepage` are both
`https://github.com/space-physics/nexradutils`, identical to the pinned `setup.cfg` `url`; `author`
(`Michael Hirsch, Ph.D.`), `author_email` (`scivision@users.noreply.github.com`), `summary`
(`easily download and plot NEXRAD weather radar reflectivity data`, matching `setup.cfg`'s
`description = easily download and plot NEXRAD weather radar reflectivity data`), `requires_python`
(`>=3.7`) and all six classifiers match `setup.cfg` at the pin exactly.

So the **installable and importable name is `nexradutils`** — `import nexradutils as nq` in
`src/nexradutils/tests/test_mod.py` and in `README.md`'s usage example — which is what HSSI stores as
Field 7, differing only in capitalisation. That is the name a user actually types, and it is the right
value.

The README's PyPI badges show the same split: their shield image URLs are keyed to `NEXRADutils`
(`https://img.shields.io/pypi/pyversions/NEXRADutils.svg`) while their link targets point at
`https://pypi.python.org/pypi/NEXRAD-quickplot`. Do **not** describe those badge links as broken in a
browser — PyPI's HTML pages are bot-gated, so their browser behaviour is not a reliable observation. The accurate statement is that the `NEXRAD-quickplot` distribution is not registered on
PyPI, proven via the JSON and Simple APIs above.

Alternate names worth knowing when searching for artifacts: `NEXRAD-quickplot` and `NEXRAD_quickplot`
(declared distribution names, neither published), `nexradutils` (published distribution and import
name), `NEXRAD` (current repository name), `nexrad-quick-plot` (original repository name), and
`nexrad-quickplot` (one hyphen — declared as the project URL at `v0.6.0` and `v0.6.1`, but never a
real repository; see Field 3, where the 404 and the typo explanation are recorded). Searching under
that last spelling is expected to return nothing.

### 8. Description (MANDATORY)
**Value:**
Easy Python download and plot NEXRAD N0Q composite reflectivity. Uses RGB high resolution PNG images of North America. The software downloads NEXRAD composite reflectivity data showing weather radar returns and creates georeferenced visualizations on maps using Cartopy. It supports downloading data from the Iowa State archive with parallel downloads, loading images with WGS84 coordinates from .wld files, plotting on geographic maps with state boundaries and coastlines, and creating keograms (time-series plots along latitude or longitude cuts). RGB data scaling covers -32 dBZ to 90 dBZ in 0.5 dBZ increments. These are reduced fidelity RGB images suitable for overview analysis; contact authors for high-fidelity science data.

**This description is not a verbatim quotation of the README, and the difference is deliberate.** Its
opening sentence differs from the README by one word. The README at the pin reads
"Easy Python download and plot NEXRAD N0Q compositive reflectivity." — with **compositive**, an
author typo for *composite*. The same misspelling propagates to GitHub's stored repository
description (`Download/Plot NEXRAD compositive reflectivity PNGs by date/time`) and to the PyHC
registry entry, so all three upstream sources carry it.

The description records **composite**, silently correcting the typo. Keep it that way: a catalogue
reader searching for "composite reflectivity" — the standard meteorological term, and the spelling a
reader would actually type — should find this entry. Restoring "compositive" for source fidelity would
make the entry harder to find and would communicate nothing. A future refresh should not treat the
divergence as drift.

The rest of the description is an accurate expansion drawn from the README's own content: the RGB
scaling range and increment, the Cartopy georegistration, the `.wld`/WGS84 coordinates, the keogram
feature, and the fidelity caveat. On that last point the README states
"These data are reduced fidelity RGB images." and
"For high-fidelity science data, the lower level data are needed--contact us if interested."

One inherited inaccuracy to note rather than silently fix: the description says keograms can be
plotted along latitude or longitude cuts. At the pin, `loadkeogram()` accepts both `"lat"` and
`"lon"` slice requests but then asserts
`assert ilat is not None, "FIXME: currently handling latitude cut (longitude keogram) only"` — only
the latitude cut is implemented. The description reflects the documented interface (`README.md`:
"Keogram (specify lat or lon and value)") rather than the implemented subset. This is a minor
overstatement inherited from the project's own documentation, not a metadata error introduced here; it
is recorded so a future refresh understands the discrepancy rather than rediscovering it.

### 9. Concise Description (OPTIONAL)
**Value:** Download and plot NEXRAD composite reflectivity PNGs by date/time for ionospheric perturbation studies

This is a fusion of GitHub's repository description
(`Download/Plot NEXRAD compositive reflectivity PNGs by date/time`) and the PyHC registry
description's purpose clause
(`Download/Plot NEXRAD compositive reflectivity by date/time, for ionospheric perturbations`), with
the author's `compositive` typo corrected for the same reason as Field 8. It is accurate, compact and
reflects the author's own framing of the software's purpose. Preserved as-is — a stylistic rewrite
would not be an improvement.

This value is also load-bearing evidence for the `Earth Ionosphere` value in Field 5: "for
ionospheric perturbation studies" is the ionospheric-purpose claim, and it originates with the
author's registry entry, not with anything in the repository.

### 10. Publication Date (RECOMMENDED)
**Value:** 2018-02-12

The first commit reachable from the pin, `b80d6c1ed7415cdadbe8a51c71eadc95a4efab3f` ("Initial
commit"), is dated 2018-02-12 17:25:05 -0500. GitHub's `created_at` for the repository is
2018-02-12T22:25:05Z — the same instant expressed in UTC. Two independent sources agree.

**Do not "correct" this to 2021.** DataCite's record for the concept DOI reports
`"publicationYear": 2021` and `"dates": [{"date": "2021-04-27", "dateType": "Issued"}]`, because a Zenodo
concept DOI inherits the metadata of its most recent version. That 2021 date belongs to the `v1.0.0`
release and is already recorded in Field 12. Field 10 is the date the software first appeared
publicly, which is 2018-02-12.

### 11. Publisher (RECOMMENDED)
**Publisher:**
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

DataCite's record for the concept DOI gives `"publisher": "Zenodo"`. The deposit reached Zenodo through
the GitHub-Zenodo integration (see the `isSupplementTo` evidence in Field 2), which does not change
the publisher of record: Zenodo is still the publishing repository.

**Zenodo has no ROR**, so the website URL is used as the identifier. A ROR API v2 query for `Zenodo`
returns zero results. This is settled negative research — a future refresh should not spend effort
re-searching, and should not substitute CERN's ROR, which identifies the operating institution rather
than the repository that published this deposit.

### 12. Version (RECOMMENDED)
**Latest Version:**
- **Version Number:** 1.0.0
- **Version Date:** 2021-04-27
- **Version Description:** src/ layout - Reorganized code into src/ directory structure
- **Version PID:** https://doi.org/10.5281/zenodo.4722449

**Corrected from `v1.0.0`.** An earlier revision of this file recorded the version number with a
leading `v`. That is the *git tag* spelling (`v1.0.0`) and the *Zenodo deposit's* `version` field
(`"v1.0.0"`), but it is not the version number the software declares: `setup.cfg` at the pin says
`version = 1.0.0`, and the published PyPI release is `1.0.0`. The value now records `1.0.0`, without
the prefix. A future refresh should not restore the `v` from the tag name.

The version date 2021-04-27 is corroborated three ways: the Zenodo deposit's `publication_date`, the
PyPI upload timestamp (2021-04-27T05:35:37Z), and GitHub's `pushed_at` (2021-04-27T05:40:32Z).

The Version PID is the **version** DOI `10.5281/zenodo.4722449`, distinct from the concept DOI in
Field 2. See Field 2 for why both are recorded and why they must not be collapsed.

**Provenance of the version description, clause by clause, so a future refresh need not re-derive
it.** The first clause, `src/ layout`, is verbatim the GitHub release title for `v1.0.0`; it also
matches the Zenodo deposit title `space-physics/NEXRAD: src/ layout` and the second half of the
pinned commit's subject `ci actions, src/ layout`. The `v1.0.0` release body is empty, so the second
clause — `Reorganized code into src/ directory structure` — is an editorial gloss written at
submission rather than a quotation of anything: neither `Reorganized` nor `directory structure`
appears in any of the ten release bodies, nor anywhere in the pinned tree. The gloss is nonetheless
accurate and belongs to this release rather than another: the range `v0.6.8..v1.0.0` contains three
commits, one of them the pin `78cf657` (`ci actions, src/ layout`), and a rename-aware diff across
that range shows four files moved into `src/` — `nexradutils/__init__.py`,
`nexradutils/data/n0q.wld`, `nexradutils/io.py` and `tests/test_mod.py`.

**Nothing here is inherited from the previous tag.** Version descriptions can silently carry over an
earlier release's notes, which would make them wrong for the version they are attached to. That has
not happened here: the `v0.6.8` release is titled `rename modules for convenience` with an empty
body, and shares no wording with the stored description.

### 13. Programming Language (RECOMMENDED)
**Values:**
- Python 3.x

`setup.cfg` at the pin declares `python_requires = >= 3.7` and the classifier
`Programming Language :: Python :: 3`. GitHub reports `"language": "Python"`. Every code file among the
21 tracked paths is Python; the remaining paths are configuration, documentation, the licence, one
PNG and one plain-text `.wld` file. `Python 2.x` is excluded by `python_requires`.

### 14. Reference Publication (OPTIONAL)
**Value:** Not found — and this emptiness is evidenced, not an oversight.

Field 14 is specifically the publication *describing the software*. No such paper exists:

- `bibstem:JOSS full:"NEXRAD"` in ADS returns **0** results — there is no JOSS paper for this package.
- The repository has no `CITATION.cff`, no `codemeta.json`, no `paper.md`/`paper.bib`, and no "how to
  cite" section in `README.md`. The README's only citation affordance is the Zenodo DOI badge, which
  points at the software deposit itself, not at a describing paper.
- A full-text search of ADS for the software's name variants (see Field 27) surfaces exactly two
  records: the Zenodo software deposit and one paper that *uses and cites* the software rather than
  describing it. That paper is recorded under Field 27, which is the correct field for it.

If a describing paper is ever published, this field would be where it belongs; nothing found in this
refresh qualifies.

### 15. License (RECOMMENDED)
**Value:** MIT License

The `LICENSE` file at the pin is the standard MIT License text, headed `MIT License` and
`Copyright (c) 2018 Michael Hirsch, Ph.D.`. GitHub's license detection reports SPDX id `MIT` and name
`MIT License`. `setup.cfg` declares `license_file = LICENSE`. The HSSI `License` vocabulary row is
spelled exactly `MIT License`, which is the value recorded.

**HSSI held no licence value for this software before this refresh**, so this is a fill rather than a
change.

**There is no storable "License URI" for this field, and an earlier revision of this file was wrong to
record one.** That revision carried a `License URI` of `https://spdx.org/licenses/MIT`. HSSI's data
model has no per-software licence URI: `Software.license` is a foreign key to a shared `License` row,
and any URL lives on that shared row and applies to every entry using it. Recording a URI here
presents an unwritable value as if it were storable. The SPDX identifier remains useful *as evidence*
that the repository's licence is MIT — that is how it is cited above — but it is not a Field 15 value.

**Do not take the licence from the DOI metadata.** The Zenodo deposit records
`"license": {"id": "other-open"}` and DataCite records only `Open Access`. Both are wrong about this
software, and both are the known DOI-autofill error class (see Field 2). The repository's own
`LICENSE` file is authoritative.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
**Values:**
- atmospheric science
- ionosphere_thermosphere_mesosphere
- Keogram
- nexrad
- reflectivity
- weather
- weather radar

`Keogram` was added in this refresh; the other six were on the record beforehand. Its capital K is
the verbatim spelling of the existing vocabulary row, not an inconsistency — see below.

**Casing matters when comparing, and the two casings here mean different things.** HSSI's view
rendering title-cases keywords for display (`Atmospheric Science`, `Nexrad`, and so on), so the
rendered form never tells you what is stored. Never compare a candidate against the rendered form or
a refresh will manufacture phantom changes. Six of the seven values above are stored lowercase;
`Keogram` carries a capital K because that is how the existing vocabulary row is spelled, for the
reason given below.

**Sources at the pin.** GitHub topics are `nexrad`, `reflectivity`, `weather-radar`. `setup.cfg`
declares `keywords` as the two-item indented list `nexrad` and `weather radar`, and the classifier
`Topic :: Scientific/Engineering :: Atmospheric Science`, which is where `atmospheric science` comes
from. `weather` is a reasonable generalisation of the repository's `weather-radar` topic. Every stored
keyword traces to a source.

**`ionosphere_thermosphere_mesosphere` was examined specifically and is justified.** That tag is a PyHC
domain keyword that propagates widely across PyHC-derived records and is frequently unsupported by the
software it is attached to. Here it is **not** blind propagation: it is the author's own keyword for
this exact package in the PyHC registry, whose entry reads
`keywords: ["ionosphere_thermosphere_mesosphere","general"]`. Keep it. Note that this keyword is the
*same* author-supplied ionospheric-purpose evidence discussed under Field 5 — it is not an independent
second source.

**PyHC's other keyword, `general`, was considered and not selected.** It carries no discriminating
information: a catalogue reader filtering on `general` learns nothing about any entry, and the term
exists in the keyword vocabulary only as registry noise. Recorded here so a future refresh does not
add it for completeness.

**`Keogram` was added in this refresh, and the capital K is load-bearing.** Keograms are a
first-class, user-facing feature of this package — `loadkeogram()` in `io.py`, `keogram()` and
`nexrad_keogram()` in `plot.py`, and `README.md`'s documented CLI option
"Keogram (specify lat or lon and value)" — and *keogram* is a distinctive, searchable heliophysics
term, so a user looking for keogram tooling in HSSI ought to find this entry. Nothing argued against
adding it.

**Why the spelling is `Keogram`.** The keyword vocabulary contains exactly one row for this term,
spelled `Keogram` with a capital K, and no other casing of it exists. The recorded value is that row's
spelling copied verbatim, which is the whole justification — it needs no assumption about how the
vocabulary resolves a near-match, and it stays correct regardless. None of it is visible to a site
visitor either way, because the display layer title-cases keywords for rendering. A future refresh
that notices `Keogram` sitting among six lowercase values should recognise it as the existing row's
own spelling rather than an inconsistency to normalise.

**Other keyword candidates considered and not selected:** `radar` (the more specific `weather radar` is
already stored, and bare `radar` would collide semantically with incoherent-scatter radar tooling),
`atmosphere` (redundant with `atmospheric science`), `dBZ` and `N0Q` (jargon too narrow to serve as
search terms; neither exists in the keyword vocabulary), `traveling ionospheric disturbances` (belongs
to the citing paper's subject, not this software's function).

### 17. Data Sources (OPTIONAL)
**Values:**
- HTTP/HTTPS Directories
- Other

**`HTTP/HTTPS Directories` is exact.** `src/nexradutils/io.py` defines
`STEM = "https://mesonet.agron.iastate.edu/archive/data/"` and `download()` builds a literal directory
path beneath it — year, month, day, then `GIS/uscomp/n0q_<timestamp>.png` — retrieved over HTTPS with
`requests`. This is a plain HTTP directory hierarchy, not an API. It is the sole external data source
in the package.

**The `Other` value was examined in this refresh and is retained, with reasoning recorded so it is not
stripped later.** The question is whether it adds anything beyond `HTTP/HTTPS Directories`. The
field's instruction is "If a source is not listed, select 'Other'." The specific archive this software
reads — the Iowa State University Environmental Mesonet's NEXRAD composite archive — is not one of the
named rows in the 17-value vocabulary (`AMDA`, `CDAWeb`, `das2`, `FTP/FTPS Directories`, `GFZ`, `HAPI`,
`Madrigal`, `Observatory/Mission-specific`, `OMNIWeb`, `S3/Cloud-aware`, `SSCWeb`, `TAP`,
`The Virtual Solar Observatory.`, `VirES`, `WDC`). Under the field's own instruction, `Other` is the
correct marker for it, and `HTTP/HTTPS Directories` describes the transport. The two are complementary
rather than redundant.

**`Observatory/Mission-specific` was considered and not selected.** It is arguably a better fit than
`Other` on content — the archive path this software reads serves one instrument network's product,
not a multi-mission holding. But the field's instruction couples that value to naming the observatory in
Field 32 ("If observatory-specific, select 'observatory-specific' and indicate the observatory/mission
name in the Related Observatory field"), and Field 32 cannot carry NEXRAD (see Fields 31 and 32
below). Selecting it would leave a dangling cross-reference that a reader could not follow.

**No other row applies.** There is no FTP, S3/cloud, HAPI, CDAWeb, OMNIWeb, SSCWeb, Madrigal, VSO,
VirES, TAP, das2, AMDA, GFZ or WDC access path anywhere in the package — the only network calls in the
installed package are the `requests.head` and `requests.get` in `urlretrieve()`.

### 18. Input File Formats (RECOMMENDED)
**Values:**
- Other

The package's primary input is a **NEXRAD N0Q composite reflectivity PNG** image, read with
`imageio.imread` in `load()`. Its georeferencing sidecar is an **ESRI world file** (`.wld`), read with
`np.loadtxt` in `wld2mesh()`. Neither PNG nor WLD is a row in the 11-value `FileFormat` vocabulary
(`ascii`, `CDF`, `csv`, `FITS`, `HDF5`, `IDL.sav`, `ISTP-Compliant`, `JSON`, `netCDF3/4`, `Other`,
`Zarr`), which is precisely why `Other` is the correct value for the PNG imagery. That enumeration is
the reason the field cannot be more specific, not evidence of an unexamined gap.

**`ascii` was considered for the `.wld` world file and deliberately declined.** The value is `Other`
alone. This was decided on full evidence, not for want of it, and the evidence is recorded here so a
future refresh does not reopen it as an oversight.

*The `.wld` file genuinely is a supported ASCII input.* It is a documented CLI option — `plot.py`'s
argument parser declares `p.add_argument("-wld", help=".wld filename")` — and a public parameter of
`load()` and `loadkeogram()`. The package ships a default at `src/nexradutils/data/n0q.wld`, and
`MANIFEST.in` explicitly includes it (`recursive-include src/nexradutils/data *.wld`). The file is
six lines of plain-text decimal numbers (`file` reports it as ASCII text), read by `np.loadtxt`,
which is an ASCII text reader. `README.md` documents the format and its six fields. So a literal
reading of the field's instruction to select all supported input formats would admit `ascii`.

*It was declined on user-facing grounds, which is what settled it.* The `.wld` file is a
georeferencing sidecar, not science data. A catalogue user filtering HSSI by input format `ascii` is
looking for software that ingests ASCII *measurement* data; they would find here a package whose
science input is a PNG image and whose only ASCII input is six affine georeferencing parameters. That
is a technically true but practically misleading hit, and the value exists to help people find
software they can use rather than to be exhaustively literal.

### 19. Output File Formats (RECOMMENDED)
**Values:**
- Other

All output is raster imagery: `fg.savefig(ofn, bbox_inches="tight", dpi=DPI)` in `overlay2d()`,
`keogram()` and `nexrad_panel()`, writing `.png` filenames constructed in `nexrad_loop()` and
`nexrad_keogram()`. PNG has no row in the `FileFormat` vocabulary, so `Other` is correct. The package
writes no data files — no CSV, no netCDF, no HDF5, no ascii export — only figures. `ascii` therefore
does **not** apply here, whichever way the Field 18 question is decided.

### 20. Operating System (RECOMMENDED)
**Values:**
- Operating System Independent

**Corrected from `OS Independent`.** An earlier revision of this file recorded `OS Independent`, which
is the text of the `setup.cfg` **classifier** (`Operating System :: OS Independent`) — a PyPI trove
string, not an HSSI vocabulary row. The `OperatingSystem` vocabulary offers `Linux`, `Mac`,
`MobilePlatform`, `Operating System Independent`, `Other`, `Solaris` and `Windows`; the only
cross-platform value is `Operating System Independent`, spelled out in full. `OS Independent` would be
rejected on submission.

The value itself is well supported beyond the classifier: `download()` in `io.py` branches on
`os.name == "nt"` to substitute a hyphen for the colon in Windows filenames, and
`src/nexradutils/tests/test_mod.py` asserts both filename forms — evidence of deliberate Windows
support alongside POSIX. Continuous integration exercised `ubuntu-latest` only
(`.github/workflows/ci.yml`), so Linux is directly verified and the other platforms rest on the
pure-Python implementation plus the explicit Windows handling.

### 21. CPU Architecture (RECOMMENDED)
**Values:**
- CPU Independent

Pure Python with no compiled extension of its own — `setup.py` is a bare `setup()` call,
`pyproject.toml` requires only `setuptools` and `wheel` for the build, and the published artifact is a
source distribution (`nexradutils-1.0.0.tar.gz`) with no wheels and therefore no architecture tags.
Nothing in the package targets a specific architecture, GPU or HPC environment.

### 22. Related Phenomena (OPTIONAL)
**Value:** Not found — evidenced-empty.

The `Phenomena` vocabulary is a **closed** list of 7 values: `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind`,
`X-ray emission`. Every one is solar or magnetospheric. This software handles tropospheric
precipitation and storm reflectivity, which corresponds to none of them, and the API rejects any value
outside the list. Enumerating the vocabulary is the reason this field is correctly empty — not
evidence that it was skipped.

The phenomena this software genuinely relates to (weather, precipitation, and — via the citing paper —
traveling ionospheric disturbances) have no rows here. Per the field's own guidance, a phenomenon with
no row belongs in Keywords (Field 16, the open vocabulary), which is where `weather` already sits.

### 23. Development Status (RECOMMENDED)
**Value:** Unsupported

**Corrected from `Inactive`.** An earlier revision of this file recorded `Inactive`, reasoning from
the 2021 last-commit date. That reasoning was incomplete: it did not account for the repository being
**archived**. GitHub reports `"archived": true`, which makes the repository read-only — it accepts no
issues, no pull requests, and no commits.

The two candidate definitions, quoted from the stored vocabulary rows, differ on exactly that point:

- **`Unsupported`** — "The project has reached a stable, usable state but the author(s) have ceased all work on it. A new maintainer may be desired."
- **`Inactive`** — "The project has reached a stable, usable state but is no longer being actively developed; support/maintenance will be provided as time allows."

`Inactive` promises that support and maintenance will still be provided as time allows. An archived
repository **cannot** deliver that: there is no channel through which a maintainer could accept a fix,
respond to an issue, or ship a release without first un-archiving. Archiving is an affirmative act by
the maintainer declaring the work ceased. `Unsupported` states exactly that, and is the correct value.

Both definitions share the premise that the project reached a stable, usable state, which the pinned
`setup.cfg` supports directly with the classifier `Development Status :: 5 - Production/Stable`, and
which the published PyPI release corroborates.

**`Moved` is explicitly rejected.** Its definition is
"The project has been moved to a new location, and the version at that location should be considered authoritative."
That does not describe this project. What happened was a sequence of **renames within the same
ownership lineage** (`scivision/nexrad-quick-plot`, then `scivision/nexradutils`, then
`space-physics/nexradutils`, then `space-physics/NEXRAD`; see Field 3), and every old URL redirects to
*this same repository*. There is no other location holding an authoritative version. A future refresh
that encounters the rename chain must not mistake it for a move.

**HSSI held no development-status value for this software before this refresh**, so this is a fill.

This value is grounded in the repostatus.org definition text stored in the vocabulary itself, not in
how any other catalogue entry happens to be classified.

### 24. Documentation (RECOMMENDED)
**Value:** https://github.com/space-physics/NEXRAD

All documentation is `README.md`, rendered on the repository's landing page. It covers installation
(`python -m pip install -e .`), the RGB reflectivity scaling, the `xarray.DataArray` return value with
a worked REPL example, download usage, all four plotting modes (directory, single file, glob pattern,
keogram), the EPSG:4326 `.wld` coordinate convention with its six fields explained, and a note on mass
image downscaling.

There is **no separate documentation site**: no `docs/` directory in any of the 43 paths ever tracked
on the pinned lineage, no Sphinx configuration, no ReadTheDocs configuration, and GitHub reports an
empty `homepage` field. There is also **no wiki** — the wiki repository does not exist (see the scope
note). Pointing this field at the repository URL is therefore correct, matching the field's own
instruction that the documentation link may be the same as the access URL.

### 25. Funder (OPTIONAL)
**Value:** Not found — evidenced-empty.

**There is no funding statement anywhere in the tracked files at the pin.** A case-insensitive search
across all 21 tracked paths for `fund`, `grant`, `award`, `NSF` and `NASA` returns only artefacts:
`granted` inside the MIT licence's "Permission is hereby granted, free of charge", and the letters
`nsf` inside `transform` and `skimage.transform` in `io.py`, `plot.py` and `test_mod.py`. Nothing
acknowledges support. The repository has no `CITATION.cff`, `codemeta.json` or acknowledgements
section that could carry one.

**Negative research to preserve — the citing paper's funder is not this software's funder.** Crossref's
record for `10.1029/2018GL080239` — the Geophysical Research Letters paper that formally cites this
software (Field 27) — lists a publisher-asserted funder: **Directorate for Geosciences**
(`10.13039/100000085`, the US National Science Foundation's geosciences directorate), award
**AGS-1743832**. ADS confirms the paper's acknowledgements section contains both that award number and
the funder name: `ack:"AGS-1743832" bibcode:2018GeoRL..4510903M` and
`ack:"National Science Foundation" bibcode:2018GeoRL..4510903M` each return that paper.

That award funded the *research reported in the paper*, not the development of this software. The
software carries no funding acknowledgement of its own, was released under one author's personal
copyright, and is cited by that paper as an external tool. **Do not adopt AGS-1743832 or the
Directorate for Geosciences as this software's funder**, and do not re-run this search — it has been
done and the answer is recorded here.

### 26. Award Title (OPTIONAL)
**Value:** Not found — evidenced-empty.

Follows directly from Field 25: with no funder, there is no award. The award number AGS-1743832 is
recorded in Field 25 solely as a rejected candidate with its reason, so that a future refresh
encountering it in Crossref does not mistake it for missing metadata. It should not be entered here.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
**Value:** https://doi.org/10.1029/2018GL080239

**HSSI held no related-publication value for this software before this refresh.** This entry adds
one, on specific evidence set out below.

**The publication.** Mrak, Sebastijan; Semeter, Joshua; Nishimura, Y.; **Hirsch, Michael**; Sivadas,
Nithin (2018), *"Coincidental TID Production by Tropospheric Weather During the August 2017 Total
Solar Eclipse"*, **Geophysical Research Letters** 45, page 10,903. DOI `10.1029/2018GL080239`;
published 2018-10-25; ADS bibcode `2018GeoRL..4510903M`. All five authors are at the Department of
Electrical and Computer Engineering and Center for Space Physics, Boston University. Crossref returns
the DOI in lowercase, `10.1029/2018gl080239`; DOIs are case-insensitive and the publisher/ADS
canonical casing is used above.

**Why it qualifies.** Field 27 is for "Publications that describe, cite, or use the software". This
paper does two of the three, formally:

1. **It cites the software.** Crossref's reference list for the paper contains, verbatim:
   `Hirsch M.(2018).NEXRADutils (software).https://doi.org/10.5281/zenodo.1402629` — a formal software
   citation pointing at the **v0.6.8 version DOI**. Note the final digit: `10.5281/zenodo.1402629` is
   the version DOI, one digit from the concept DOI `10.5281/zenodo.1402628` in Field 2. They must not
   be conflated.
2. **It uses the software, for the software's stated purpose.** The paper's subject is traveling
   ionospheric disturbances produced by tropospheric weather during the 2017 eclipse; its abstract
   reports examining concurrent observations of tropospheric and ionospheric weather and finding a
   great spatiotemporal correlation. Supplying the tropospheric weather-radar imagery for exactly that
   kind of correlation is what this package exists to do — it is the concrete instance of the
   ionospheric-perturbations purpose the author states in the PyHC registry.
3. Michael Hirsch, this software's sole author, is the paper's fourth author, so the citation is a
   first-party use as well as a formal one.

**This is the only citing publication ADS indexes, and the queries are recorded in full below** so
that the negative can be re-tested rather than taken on trust. They run against the ADS/SciX API
using an anonymous bootstrap token.

**A zero from these queries is only meaningful alongside a control, and a future refresh should
re-establish one before trusting a null result.** This API answers a query it cannot authenticate or
parse with an empty result set rather than an error, so a silently-failing sweep is indistinguishable
from a genuine absence. Two controls separate them: a deliberately malformed token should produce an
explicit invalid-token response rather than an empty one, and a nonsense term such as
`full:"zzqqxxnonsense12345"` should hold at 0 while the real queries below return their stated
counts. Both behaved that way for the results recorded here.

| Query | Result |
|---|---|
| `full:"NEXRAD-quickplot"` | 1 — `2018GeoRL..4510903M` |
| `full:"nexrad_quickplot"` | 1 — `2018GeoRL..4510903M` |
| `full:"NEXRADutils"` | 1 — `2018zndo...1402629H` (the software's own v0.6.8 Zenodo deposit) |
| `citations(bibcode:2018zndo...1402629H)` | 1 — `2018GeoRL..4510903M` |
| `full:"10.5281/zenodo.1402628"` | 0 |
| `bibstem:JOSS full:"NEXRAD"` | 0 |

The union of every name-variant full-text sweep is exactly two records: this paper and the software's
own v0.6.8 Zenodo deposit.

**A stated limitation of the citation-graph evidence, so it is not over-read.** ADS indexes only one
of the two Zenodo deposits. `bibcode:2018zndo...1402629H` (v0.6.8) resolves, but there is **no ADS
record at all** for the v1.0.0 deposit — `doi:10.5281/zenodo.4722449` returns 0, as does
`doi:10.5281/zenodo.1402628` for the concept DOI. So a `citations(...)` query cannot be run against
the v1.0.0 or concept DOIs; any such query would return 0 because the record is absent, not because
nothing cites it. The negative result therefore rests on the three full-text name sweeps, the
full-text sweep for the concept DOI string, and the citation list of the one deposit ADS does index —
which together are strong, but are not a complete citation-graph proof for the later version. A
future refresh could re-check whether ADS has since ingested the v1.0.0 deposit.

**One near-miss recorded so it is not re-investigated.** `author:"Hirsch, M" full:"NEXRAD"` returns a
third record, `2018AGUFMSH11B..05M` — an AGU Fall Meeting 2018 abstract by the same team. It matches on
the generic term *NEXRAD* (the radar network) and **does not name or cite this software**: restricting
that bibcode with `full:"NEXRADutils"`, `full:"quickplot"` or `full:"zenodo"` each returns 0. It is a
meeting abstract that used NEXRAD data, not a publication related to this package, so it is
deliberately not recorded here.

### 28. Related Datasets (OPTIONAL)
**Value:** https://mesonet.agron.iastate.edu/docs/nexrad_composites/

This is the Iowa State University Environmental Mesonet's documentation page for the NEXRAD composite
products this software downloads. `README.md` links exactly this URL, under its download heading, as
the source of NEXRAD reflectivity data. The URL resolves directly, with no redirect.

**No DOI exists for this dataset.** It is an ongoing operational archive rather than a versioned,
citable deposit, so a permanent landing page is the correct value per the field's guidance. A future
refresh should not search for a DOI that the archive does not mint.

A second Mesonet URL appears in `README.md` —
`https://mesonet.agron.iastate.edu/docs/radmapserver/howto.html#toc3.3`, cited for the `.wld` world-file
format specification. It is documentation of a file format, not a dataset, so it is deliberately not
recorded here.

### 29. Related Software (OPTIONAL)
**Value:**
- https://github.com/Unidata/MetPy

**This field was rebuilt in this refresh.** Before it, the record held three entries —
`https://github.com/imageio/imageio`, `https://github.com/pydata/xarray` and
`https://github.com/SciTools/cartopy` — and none of the three survived. All three were removed and
`https://github.com/Unidata/MetPy` was added; the reasoning for each of the four decisions is below,
including the counter-evidence against the one addition.

Field 29 is defined as "Software that performs similar tasks but does not necessarily link together"
(the interoperability case being Field 30), and adds that
"Important software dependencies and software this work was forked from should also be included."
The word *important* is load-bearing: the field's relevance guidance excludes the generic
scientific-Python stack from Field 29 by the same rule that excludes it from Field 30, so a package
rejected from Field 30 is not thereby a Field 29 entry.

**`cartopy` — removed, by rule.** Cartopy is **named explicitly** in the exclusion list:
"Never list these (Tier A), no exceptions:" — followed by
"numpy, scipy, pandas, matplotlib, cartopy, seaborn, plotly, bokeh, requests, python-dateutil, pytest, tqdm, PyYAML, click, setuptools, and the rest of the generic scientific-Python/tooling stack."
There is no evidentiary escape hatch for a Tier A package; the rule is categorical, and it applies to
Field 29 exactly as it applies to Field 30. Cartopy is genuinely used here — `plot.py` imports it and
builds a `PlateCarree` projection — but being used is precisely what Tier A says is insufficient. In
the source it is an optional extra (`[options.extras_require]`, `plots` group), not even a core
dependency. This removal is the rule applied, not a curator's preference, and a future refresh
proposing cartopy again would be re-proposing a value the governing rule forbids by name.

**`imageio` — removed, by the same rule extended by kind.** Imageio is not named in either tier, so
the governing test is the principle that extends Tier A by kind rather than by name:
"would this package be equally at home in a web app, a finance model, or a biology pipeline?"
Imageio is a general-purpose image reading and writing library — it fails that test outright, being
at home in any of the three. Its role here is exactly the I/O plumbing the rule enumerates: one call,
`imageio.imread(fn)`, to decode a PNG. It is a core `install_requires` entry, but *being a dependency
is not the test*. It gets Tier A treatment whether or not it appears in the list, and because Field 29
carries the same exclusion it was removed outright rather than relocated.

**`xarray` — removed from Field 29, retained in Field 30.** This was a placement question rather than
a removal-on-policy one, and it turned on judgement. Before this refresh a single stored related-item
record was attached to both fields at once, so xarray appeared in both lists — not two
coincidentally-identical entries but one record doing double duty. Field 30's placement was never in
doubt and its Tier B evidence is unchanged; only the Field 29 attachment was dropped.

The argument for keeping it in both was real: Field 29's text does invite
"Important software dependencies", xarray is the package's core data model rather than incidental
plumbing, and it sits in Tier B rather than Tier A, so it is not categorically excluded from either
field. What decided against it is the visitor's side read together with the field's own definition.
Field 29 is defined as software that "performs similar tasks but does not necessarily link together",
the doc's worked example being two packages that model the same physics under different assumptions.
Xarray performs no task similar to this package's — it is a data-structure library, not a NEXRAD
tool. Field 29 is where a reader looks for *peer tools*: another way to get NEXRAD reflectivity, a
predecessor, a competitor. Xarray there promises a peer and delivers none, while the Field 30 entry
already states the true and useful thing — that this package hands you xarray objects you can carry
into other xarray-aware tools. Listing one package in both lists also made them look like the same
information printed twice.

**`MetPy` (`https://github.com/Unidata/MetPy`) — added, and this is the weakest-evidenced decision in
the field.** Recorded honestly for that reason: the in-repo trace is thin, and the counter-evidence
below is the reason this should not be treated as a strong precedent for adding a package on
comparable evidence elsewhere.

*Evidence for including it.* `archive/cmap.py` at the pin is a MetPy script. It imports
`from metpy.cbook import get_test_data`, `from metpy.io import Level3File`, and
`from metpy.plots import add_metpy_logo, add_timestamp, ctables`, and its docstring states
"Use MetPy to read information from a NEXRAD Level 3 (NIDS product) file and plot". It reads a NEXRAD
**Level 3** NIDS product and renders N0Q reflectivity with the `NWSReflectivity` colour table,
alongside N0U velocity with `NWSVelocity`. MetPy is a domain-specific meteorology library, not generic
infrastructure — it fails the web-app / finance-model / biology-pipeline test in the direction that
*keeps* a package eligible. And it performs the same task by different means: reading NEXRAD Level 3
binary products directly, where this package consumes the pre-rendered composite RGB PNGs. That
similar-task-by-different-assumptions relationship is Field 29's own definition. The README makes the
gap explicit, saying of its own data "These data are reduced fidelity RGB images." and
"For high-fidelity science data, the lower level data are needed--contact us if interested." —
and reading the lower-level data is exactly what MetPy's `Level3File` does.

*Counter-evidence, stated just as plainly.* The file lives in `archive/`, which the project excludes
from its own quality gates: `.flake8` sets
`exclude = .git,__pycache__,.eggs/,doc/,docs/,build/,dist/,archive/` and `mypy.ini` sets
`files = src/`. It is excluded from the installed package (`packages = find:` with `where=src`, so
only `src/` is packaged). Nothing imports it. MetPy appears in **no** dependency list at any point in
the repository's history — a search of `setup.py`, `setup.cfg`, `pyproject.toml` and
`requirements.txt` across all 65 commits reachable from the pin finds it in none of them. And the file
is not original work: it carries the header `Copyright (c) 2015 MetPy Developers.` under BSD 3-Clause,
i.e. it is a copy of an upstream MetPy example. It has lived at `archive/cmap.py` since 2018-02-16,
four days after the repository's first commit, and has never existed at any other path. So the
relationship amounts to the author having saved MetPy's own NEXRAD example alongside this project,
which is weaker than a considered statement about peer tooling.

*What carried the decision was the visitor's side read against the field's definition.* Field 29 is
for software that performs similar tasks by different means. MetPy reads NEXRAD Level 3 products
directly where this package consumes pre-rendered composite RGB PNGs — the same task, different
means — and MetPy is domain-specific meteorology rather than generic infrastructure, so nothing in
the Tier A exclusion touches it. For an archived, reduced-fidelity tool whose own README tells
readers that "For high-fidelity science data, the lower level data are needed--contact us if interested.",
naming the maintained, domain-standard package that reads exactly that lower-level data is the most
useful thing this field can tell someone who lands on the entry. That is what the value is for, and
it is why the thin in-repo trace was not treated as disqualifying.

**Considered and rejected outright, recorded so they are not proposed later:**
- `numpy`, `requests`, `python-dateutil` — core `install_requires` entries, all named in the Tier A
  list.
- `matplotlib`, `seaborn`, `cython` — `plots` extra, all Tier A or generic build tooling.
- `scikit-image` — `plots` extra, used for one call (`downscale_local_mean`). General-purpose image
  processing; it is equally at home in a biology pipeline, which is arguably its primary community, so
  it gets Tier A treatment.
- `pytest`, `flake8`, `mypy` — the `tests` extra, i.e. development tooling.
- `sciencedates` — appears only as an omit pattern in `.coveragerc` (`*/sciencedates/*`), a leftover
  from an earlier revision. It is **not** a dependency at the pin and appears in no dependency list.
  Recorded here specifically because a future agent grepping the repository will encounter the name and
  might otherwise propose it.
- ImageMagick — the README and `plot.py` suggest external `mogrify` and `convert` commands for bulk
  image resizing and GIF assembly. It is a general-purpose image utility, invoked by the user rather
  than the package, and not software this package interoperates with or resembles.

### 30. Interoperable Software (OPTIONAL)
**Value:**
- https://github.com/pydata/xarray

**This value is unchanged by this refresh and its evidence stands as it did.** Until this refresh a
single stored related-item record attached xarray to Field 29 as well; that Field 29 attachment was
removed and this one deliberately kept. Field 29 records why the two placements were separated.

Xarray is a Tier B package: "Include only with cited evidence (Tier B):" —
"astropy, xarray, cdflib, h5py, netCDF4, dask, MATLAB, Jupyter and similar". Tier B qualifies only on
a *specific documented exchange*, with the doc's own qualifying example being
"The public API returns `xarray.Dataset` objects as its documented interchange format". The evidence
here matches that pattern precisely:

- **Public API return type.** `src/nexradutils/io.py` annotates `load()` as returning
  `) -> xarray.DataArray:` and annotates `loadkeogram()` the same way. These are the package's two
  data-producing functions.
- **Re-exported as the package's public surface.** `src/nexradutils/__init__.py` contains
  `from .io import load, loadkeogram, download  # noqa: F401`, so `nexradutils.load` is the documented
  entry point.
- **Documented to users as the interchange format.** `README.md` states
  "We use `xarray.DataArray` and plot image by image." and follows it with a REPL block showing the
  returned `<xarray.DataArray (lat: 540, lon: 1220, color: 3)>` with its `lat`, `lon` and `color`
  coordinates — telling the reader exactly what object they will receive and what its dimensions mean.
- **The exchange is real, not incidental.** Because `load()` hands back a fully coordinate-labelled
  xarray object, its output can be carried directly into any xarray-aware analysis or plotting tool
  without conversion. That is a demonstrated exchange, not shared-runtime coexistence.

This is *not* justified by "uses xarray internally", which the doc explicitly says does not qualify,
nor by ecosystem membership, which it explicitly says is never sufficient on its own.

**No other package qualifies for Field 30.** Every remaining dependency is Tier A generic
infrastructure (see Field 29's rejection list), and none exposes a converter, adapter, plugin
interface, shared data model, or cross-language bridge to a named domain tool.

### 31. Related Instruments (OPTIONAL)
**Value:** Not found — evidenced-empty, and deliberately so.

**Corrected from an unwritable value.** An earlier revision of this file recorded an instrument named
`NEXRAD (Next-Generation Radar)` with no instrument identifier. That entry is not submittable. Fields
31 and 32 are SPASE-only: a name with no identifier either binds to an arbitrary same-named row or
**creates a new identifier-less row**, reintroducing exactly the legacy rows that the vocabulary
backfill removed. The governing rule is "Never emit a `name` without an `identifier`." An entry that
does not resolve is omitted or flagged — never invented.

**The vocabulary was searched exhaustively and NEXRAD is not in it.** Every row of the
instrument/observatory controlled vocabulary (7,602 rows as searched, of which 0 fail the
`https://spase-metadata.org/` identifier guard) was checked across **all** its columns — `name`,
`abbreviation`, `identifier` and `definition` — for these terms:

| Term searched | Matches across all four columns |
|---|---|
| `nexrad` | **0** (anywhere in any row, any column) |
| `next-generation radar` and `next generation radar` | 0 |
| `wsr-88` and `88d` | 0 |
| `composite reflectivity` and `reflectivity` | 0 |
| `rainfall` | 0 |
| `national weather service` | 0 |
| `weather radar` | 1 — unrelated (see below) |
| `precipitation` | 191 — all heliophysics homonyms (see below) |
| `lightning` | 18 — all heliophysics homonyms (see below) |
| `s-band` | 35 — all spacecraft radio communications (see below) |

The single `weather radar` match is `CPEA` (abbreviation "Coupling Processes in the Equatorial
Atmosphere"), identifier `https://spase-metadata.org/IUGONET/Instrument/RISH/misc/KTB/Xbandradar` — an
X-band radar at an equatorial-atmosphere observatory in Indonesia, with no relationship to the US
NEXRAD network. There is no defensible substitution.

**The three non-zero counts are homonyms, not meteorology, and a future refresh should not chase
them.** `precipitation` in this vocabulary means *particle* precipitation — auroral particle
precipitation and relativistic-electron precipitation from the radiation belts, in rows such as the
Balloon Array for Radiation-belt Relativistic Electron Losses instruments and various auroral
particle detectors. `lightning` appears in descriptions of space-weather and planetary instruments
that detect lightning-generated electromagnetic signals (Cassini RPWS, C/NOFS VEFI's optical
lightning detector, the Galileo probe's lightning/energetic-particles experiment). `s-band` appears
in spacecraft telemetry-and-command descriptions, i.e. the radio downlink band, not a radar
observing band. None of the three describes a meteorological radar.

The distinction that carries the argument: **all three of those terms return 0 when the search is
restricted to `name`, `abbreviation` and `identifier`.** Every hit is in free-text `definition`
prose. No row in the vocabulary is *identified* as anything meteorological, which is the property
that matters for resolving Fields 31 and 32.

**The exclusion is also a documented rule, not merely a vocabulary gap.** The SPASE resolution ladder's
final rung names this exact case: "Nothing defensible resolves" —
"a generic class label (`Ionosonde`, `Digital All Sky Cameras`), or something outside heliophysics scope (`NEXRAD`)"
— omit the entry and document why. And: "A documented omission is a correct outcome, not a failure."
NEXRAD is a NOAA/FAA/US Air Force terrestrial weather-radar network, not a heliophysics instrument, and
that is why no SPASE record exists for it.

**If a row ever appears**, it would still need a `https://spase-metadata.org/` identifier to be
recordable here; a bare name would remain unwritable. A future refresh should not repeat the search
above without a reason to think the vocabulary has been extended into terrestrial meteorology.

### 32. Related Observatories (OPTIONAL)
**Value:** Not found — evidenced-empty, for the same reason as Field 31.

**Corrected from an unwritable value.** An earlier revision recorded an observatory named
`NEXRAD Network` with no identifier at all. Same defect, same rule: never a name without an identifier.

The observatory-level fallback that rescues many missing instruments — associate the platform or
mission when the instrument itself has no record — has nothing to fall back *to* here. The NEXRAD
network is itself the platform, and the vocabulary search recorded under Field 31 covered observatory
rows (`type` 2) as well as instrument rows: zero matches for `nexrad` across every row and column.

The observatory rows whose text mentions `NOAA` are NOAA's polar-orbiting and geostationary
**satellites** (`https://spase-metadata.org/SMWG/Observatory/NOAA/5`,
`https://spase-metadata.org/SMWG/Observatory/NOAA/6`,
`https://spase-metadata.org/SMWG/Observatory/GOES/5`, and similar) — spacecraft, not ground radar
facilities. None is a candidate.

### 33. Logo (OPTIONAL)
**Value:** Not found — evidenced-empty. No logo exists to record.

**Exactly one image file has ever existed on the pinned revision's ancestry**, and it is not a logo.
`doc/n0q_ramp.png` is the only file matching any image extension among the 43 distinct tracked paths
across all 65 commits reachable from the pin.

**It was extracted and examined, not merely listed.** It is a 30 x 256 pixel, 8-bit colormap PNG of
1,879 bytes. Rendered, it is a **vertical dBZ colour-scale bar** — a narrow strip of the NEXRAD N0Q
reflectivity palette with numeric tick labels at -20, 0, 20, 40, 60 and 80, and the axis label "dBZ".

Its role in the software confirms the reading: `plot.py`'s `main()` sets
`SCALEFN = Path(__file__).parent / "doc" / "n0q_ramp.png"` and passes it as the `scalefn` argument,
which `nexrad_panel()` loads with `imageio.imread`, rotates it with
`scale = np.rot90(imageio.imread(scalefn), 2)`, and pastes it into the figure as an inset axis with
ticks turned off. It is a **plot legend image**, a data
product of the software's own figures. `README.md` embeds it under the caption "NEXRAD N0Q RGB
scaling" to document the colour scale for readers. It is not presented as the project's mark anywhere
— not in a README header, not as a docs banner, and there is no PyHC registry `logo:` field for this
entry.

Recording a colour-bar legend as a software logo would be wrong on the catalogue page: a reader would
see a data legend where they expect a project identity.

**No logo could have accumulated unnoticed, either.** `.gitignore` at the pin begins with `*.png`, so
every PNG in this repository had to be added deliberately, and only one ever was. There is no other
hosted asset: GitHub reports an empty `homepage`, there is no documentation site (Field 24), and no
image appears in any DOI or registry record for this software.

A documented omission is the correct outcome here. Nothing should be invented, and no example plot or
data product should be substituted.

---

## PyHC registry status

NEXRADutils appears in the PyHC **unevaluated** packages list. The specific file is
`https://raw.githubusercontent.com/heliophysicsPy/heliophysicsPy.github.io/main/_data/projects_unevaluated.yml`.
Neither of the other two registry files contains any NEXRAD entry: a case-insensitive search of
`_data/projects_core.yml` (the core list) and `_data/projects.yml` (the community list) returns no
match in either. Pin the specific file when citing this — an entry in the unevaluated list carries a
different status claim from one in core or community.

The entry reads:

```yaml
- name: NEXRADutils
  code: https://github.com/space-physics/NEXRADutils
  description: Download/Plot NEXRAD compositive reflectivity by date/time, for ionospheric perturbations
  contact: Michael Hirsch
  keywords: ["ionosphere_thermosphere_mesosphere","general"]
```

It is the source of the `ionosphere_thermosphere_mesosphere` keyword (Field 16), the
ionospheric-purpose framing in the concise description (Field 9) and Field 5's
`Earth Ionosphere` value, and it
corroborates the author (Field 6). Its `code` URL uses an earlier repository name that redirects to the
current one (Field 3), and its description carries the author's `compositive` typo (Field 8).

---

## Repository and packaging history

Consolidated here because several fields depend on it and it is not obvious from the pinned tree
alone.

- **Ten tags**, `v0.6.0` through `v0.6.8` and `v1.0.0`, and **all ten are ancestors of the pinned
  revision**. This matters because several repositories under the same owner carry tags on
  pre-rewrite orphan lineages, where tag-derived evidence would contradict the pin. That hazard does
  not apply here — every tag is on the pinned lineage and tag-based evidence is safe to cite.
- **Only two of those ten tags produced Zenodo deposits** (`v0.6.8` and `v1.0.0`; see Field 2). Do not
  assume one DOI per tag.
- **Distribution name and repository URL both changed repeatedly** — see the tables in Fields 3 and 7.
  The practical consequence is that searching for external artifacts under the current name alone will
  miss things: the citing publication's reference calls the software `NEXRADutils`, the paper-era
  Zenodo deposit is titled `scivision/NEXRADutils`, and the PyPI record is `nexradutils`, while the
  repository is now `space-physics/NEXRAD` and the pinned source declares `NEXRAD-quickplot`.

---

## Known upstream limitations at the pinned release

Recorded because each one could otherwise cause a future refresh to record a wrong metadata value from
a plausible-looking source.

**The package installs no command-line tools at the pinned release, despite the README documenting
two.** `README.md` presents `download-nexrad start stop outdir` and `plot-nexrad ~/data/nexrad/` as
shell commands, but `setup.cfg` at the pin declares no `[options.entry_points]` section and no
`console_scripts` at all. Earlier revisions did: `v0.6.8`'s `setup.cfg` declares `console_scripts` with
`download_nexrad = download_nexrad:main` and `plot_nexrad = plot_nexrad:main` — underscores, unlike the
README's hyphens. The entry points were dropped before the pin and the README was not updated. The
package's own tests confirm the actual invocation: `src/nexradutils/tests/test_scripts.py` runs
`python -m nexradutils.download` and `python -m nexradutils.plot` via `subprocess`, not the named
commands.

An earlier revision of this file listed `download-nexrad` and `plot-nexrad` under a "Command Line
Tools" heading as installed entry points. That is **wrong for the pinned release** and should not be
restored from the README.

**The bundled colour-scale image is looked up at a path where it does not exist.** `plot.py`'s `main()`
sets `SCALEFN = Path(__file__).parent / "doc" / "n0q_ramp.png"` — i.e. inside the installed package —
while the file is tracked at the repository root as `doc/n0q_ramp.png` and is not included by
`MANIFEST.in`, which ships only `src/nexradutils/data/*.wld` and `src/nexradutils/tests/*.png`. The
code degrades gracefully (`nexrad_panel()` guards with `if scalefn and scalefn.is_file():`), so the
colour bar is simply absent from installed-package figures. Relevant to metadata only as a caution:
`doc/n0q_ramp.png` is a repository-only asset, not a packaged one.

**CI installs an extras group that is not defined.** `.github/workflows/ci.yml` runs
`pip install .[tests,lint]`, while `setup.cfg` defines only `tests` and `plots` under
`[options.extras_require]`. There is no `lint` extra. Noted because the CI configuration cannot be
relied on as a statement of the package's actual optional-dependency structure.

**Keogram longitude cuts are unimplemented.** See Field 8 — the documented interface accepts a
longitude cut but the implementation asserts on latitude only.
