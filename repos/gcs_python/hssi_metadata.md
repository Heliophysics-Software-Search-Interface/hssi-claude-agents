# HSSI Metadata Extraction Results

**HSSI Software ID:** aa39bfc8-4980-4663-adf0-b7ee94f6b976
**Repository:** https://github.com/johan12345/gcs_python/
**Source Revision:** c8cc9cfc40f485c3bb4a37ff86896571bcd4104f
**Extraction Date:** 2026-08-04
**Validation Date:** 2026-08-04
**Validation Status:** PASS

**Scope note.** This is a small, self-contained repository (16 tracked files), and the evidence below
draws on all of it: `README.md`, `CITATION.cff`, `LICENSE`, `setup.py`, `requirements.txt`, the four
Python modules under `gcs/`, the two sample scripts, and the shipped thesis excerpt
`doc/gcs_implementation_forstner_phd_2021.pdf`. That PDF is Appendix B of the author's PhD thesis
and is the single most authoritative narrative description of this software — it documents the
design, the supported data sources, the file formats, the fitting workflow, and the validation
against the original IDL version. Several field decisions below rest on it, and a future agent
should read it before revising them. Note also that this repository's `CITATION.cff` contains an
invalid `license:` value (`other-open`, a Zenodo licence id rather than an SPDX identifier), which
Zenodo and DataCite have both propagated; the LICENSE file, not the CFF, is authoritative (Field 15).

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

*The submitter identity is not part of this software's published HSSI record and is not recoverable
from it, so a placeholder stands here.*

---

### 2. Persistent Identifier (RECOMMENDED)
https://doi.org/10.5281/zenodo.4081425

This is the Zenodo **concept** DOI (all versions), which is what Field 2 asks for. The DataCite
record for it lists five `HasVersion` relations — 10.5281/zenodo.4081426 (0.1.0), .4443203 (0.2.0),
.4587363 (0.2.1), .5084818 (0.2.2) and .12668802 (0.2.3) — confirming it is the parent rather than a
version DOI.

Two version-level DOIs appear in repository artifacts and must **not** be used here:
`CITATION.cff` carries `doi: 10.5281/zenodo.12668802` (the 0.2.3 version DOI, which belongs in
Field 12), and at the 0.2.3 tag the same file carried `10.5281/zenodo.5084818` (the 0.2.2 version
DOI) because the CFF was refreshed twelve minutes after the release tag was cut. The README's badge
(`https://zenodo.org/badge/latestdoi/297350666`) resolves to whatever the latest version DOI is and
is therefore not a stable persistent identifier either.

---

### 3. Code Repository (MANDATORY)
https://github.com/johan12345/gcs_python/

Matches `CITATION.cff` `repository-code` and `setup.py` `url` (both without the trailing slash) and
the `IsSupplementTo` relation on the Zenodo record
(`https://github.com/johan12345/gcs_python/tree/0.2.3`). The recorded URL keeps its trailing slash.
The slashless form written by `CITATION.cff` and `setup.py` was considered and not adopted: both forms
resolve identically to the same repository, so rewriting one into the other would change the recorded
value without changing any information it carries. A future refresh should read the difference from
`CITATION.cff` as settled rather than as drift.

The default branch is `master` (not `main`). The thesis excerpt also records a Kiel University mirror
at `https://gitlab.physik.uni-kiel.de/ET/gcs_python`. That mirror is dead: the host
`gitlab.physik.uni-kiel.de` no longer resolves in DNS at all (NXDOMAIN, checked 2026-08-04), so the
URL cannot be reached even as a fallback. GitHub is therefore not merely the canonical location named
by `CITATION.cff` and by the Zenodo deposit — it is the only viable one, for this field and for the
Documentation URL in Field 24 alike. The mirror is recorded here as historical context so a future
agent who meets the URL in the shipped thesis excerpt does not chase it, and so that its
disappearance is not mistaken for a relocation of the project (see Field 23).

---

### 4. Software Functionality (MANDATORY)
- Coordinate Transforms
- Coordinate Transforms: Solar
- Data Processing and Analysis
- Data Processing and Analysis: Analysis
- Data Processing and Analysis: Data Access and Retrieval
- Data Processing and Analysis: Image Processing
- Data Visualization
- Data Visualization: 2D Graphics
- Data Visualization: 3D Graphics
- Models and Simulations
- Models and Simulations: Data Guided
- Models and Simulations: Empirical
- Models and Simulations: Forward-Fitting

This record previously listed only `Models and Simulations`. That value is correct but radically
incomplete: this package is a modelling **and** data-retrieval **and** visualisation **and**
coordinate-transformation tool, and every value above is backed by specific code. Each subcategory is
listed together with its parent category, as the taxonomy requires.

Evidence, value by value:

- **Models and Simulations** / **: Empirical** — `gcs/geometry.py` implements the Graduated
  Cylindrical Shell geometry from closed-form expressions (`skeleton()` builds the flux-rope axis,
  `gcs_mesh()` wraps circular cross-sections around it, `apex_radius()` returns `k*height/(1+k)`).
  The shipped thesis excerpt states the classification outright: "The graduated cylindrical shell
  model (GCS, Thernisien et al., 2006; Thernisien, 2011) is an **empirical model** that is commonly
  used to represent the three-dimensional structure of flux rope coronal mass ejections (CMEs) near
  the Sun." It is a parametric geometrical representation, not a solution of physical equations.
- **Models and Simulations: Forward-Fitting** — the thesis excerpt again: "The GCS model is typically
  employed in a forward modelling approach, i.e., the model is visually compared to coronagraph
  observations of a CME and the input parameters are then iteratively adjusted by the scientist to
  achieve a good fit." That is exactly what `gcs/gui.py` implements: six parameter sliders
  (`half_angle`, `height`, `kappa`, `lat`, `lon`, `tilt`) that re-project the synthetic mesh onto the
  observations on every change. The fitting loop is human-in-the-loop rather than an automated
  optimiser — recorded here so a future agent does not reject the value for lack of a chi-square
  routine.
- **Models and Simulations: Data Guided** — the model instance has no meaning apart from the
  observations it is fitted to; `GCSGui` is constructed from an observation date and a spacecraft
  list, and the parameters are constrained by the retrieved images.
- **Coordinate Transforms** / **: Solar** — `gcs_mesh_sunpy()` scales the mesh by
  `sunpy.coordinates.sun.constants.radius` and returns a `SkyCoord` in the
  `HeliographicStonyhurst` frame; `rotate_mesh()` applies the heliographic latitude/longitude/tilt
  rotation; and `GCSGui.plot_mesh()` performs the user-visible transform
  `mesh.frame.transform_to(image.coordinate_frame)` into each coronagraph's observer frame. Projecting
  one 3D model into several simultaneous viewpoints *is* the scientific mechanism of the tool, so the
  transform is a user-facing capability rather than an internal utility step.
- **Data Processing and Analysis** / **: Data Access and Retrieval** —
  `gcs/utils/helioviewer.py` constructs a `sunpy.net.helioviewer.HelioviewerClient` and falls back to
  the IAS mirror when helioviewer.org is unreachable; `gui.py:download_helioviewer()` calls
  `hv.download_jp2(...)` per spacecraft, and additionally queries JPL Horizons through
  `sunpy.coordinates.get_horizons_coord('SOHO', f.date)` to obtain the SOHO observer location.
- **Data Processing and Analysis: Image Processing** — `gui.py:running_difference()` (lines 39–40)
  forms `Map(b.data * 1.0 - a.data * 1.0, b.meta)` from two images one hour apart, exposed as the
  `-rd` / `--running-difference` command-line switch. The `* 1.0` factors are deliberate rather than
  decorative: the JPEG2000 image arrays arrive as unsigned integers, so subtracting them without
  first promoting to float would wrap every negative difference around to a large positive value
  instead of showing the darkening ahead of the CME front. Running-difference imaging is the standard
  coronagraph technique for isolating a moving CME front, and the thesis excerpt describes it as
  such.
- **Data Processing and Analysis: Analysis** — the scientific product is a set of derived physical
  quantities for the CME (apex height, angular half width, aspect ratio, heliographic latitude,
  Stonyhurst longitude, tilt), plus the apex cross-section radius computed by `apex_radius()` and
  displayed live in the GUI. The thesis excerpt notes these parameters "can then be used for further
  evaluation, e.g. as input parameters for modeling the subsequent CME propagation."
- **Data Visualization** / **: 2D Graphics** — `GCSGui.make_plot()` renders each coronagraph image
  with `image.plot(axes=ax, cmap='Greys_r', ...)` in a `GridSpec` panel per spacecraft, and overlays
  the projected mesh with `ax.plot_coord(mesh, style, ...)` in either `grid` (wireframe) or
  `point cloud` mode.
- **Data Visualization: 3D Graphics** — `sample.py`, one of the two examples the README directs users
  to, triangulates the mesh with `matplotlib.tri.Triangulation` and renders it with
  `Axes3D`/`plot_trisurf`. The thesis excerpt's Figure 15 shows the same 3D wireframe as a documented
  output of the package.

Considered and rejected, with reasons a future agent should not have to re-derive:

- **Models and Simulations: First Principles / Physics-Based / MHD / Theory** — no physical equation
  is solved anywhere; the shell is pure analytic geometry. `Theory` was the closest of the four but
  would misrepresent geometric construction as theoretical physics.
- **Models and Simulations: Observatory/Instrument Models** and **: Instrument Response** — this port
  deliberately does *not* implement the Thomson-scattering raytracing that the original SolarSoft
  `scraytrace` package offers; it produces a wireframe overlaid on real images and never synthesises
  instrument brightness. Worth knowing before anyone proposes these from the `scraytrace` lineage.
- **Data Processing and Analysis: Calibration** — explicitly out of scope. The thesis excerpt:
  Helioviewer.org "directly provides images in JPEG2000 format to which all necessary calibration and
  background subtraction routines were already applied on the server side." Calibration happens
  upstream, and avoiding it locally was a stated design goal of this port versus the IDL version.
- **Coordinate Transforms: Mission-Specific** — tempting, because `download_helioviewer()` patches
  `HGLN_OBS`/`HGLT_OBS`/`DSUN_OBS` into the SOHO map metadata from JPL Horizons. But the frames used
  are SunPy's generic observer-parameterised solar frames, not mission-defined frames, and the patch
  is a metadata repair for missing observer keywords rather than a spacecraft-frame transformation.
- **Coordinate Transforms: Heliospheric** — no HCI/HAE/HEE/RTN frame appears; Stonyhurst and
  helioprojective are solar frames.
- **Data Processing and Analysis: Processing** — a catch-all that would add nothing beyond the
  Image Processing and Analysis values already recorded.
- **Data Visualization: Line Plots** — the `grid` draw mode does draw line segments, but as a mesh
  wireframe, not as a 1D/time-series line plot.
- **Data Visualization: Movies / Web-Based / Orbit Plots / Spacecraft Formation Plots /
  Mission-Specific** — no animation, no browser front end, no trajectory or constellation plotting;
  the image+wireframe rendering is identical across the three supported spacecraft rather than
  specific to any one of them.
- **Mission-related** (any) — the package works with mission data but is not part of any mission
  ground system, pipeline, or operations chain.
- **Servers and Environments** (any) — no server, container, or HPC component.

---

### 5. Related Region (MANDATORY)
- Corona
- Solar Environment

`Corona` is the specific region the software actually serves: the GCS model is fitted to
coronagraph fields of view — LASCO C2 (~2–6 R_s) and C3 (~3.7–30 R_s), SECCHI COR1 (~1.4–4 R_s) and
COR2 (~2–15 R_s) — and the GUI's apex-height slider is bounded at 24 R_s
(`gui.py:create_widgets()`). The thesis excerpt frames the model as representing flux-rope CMEs
"near the Sun." Field 5's guidance prefers the most specific applicable region, and `Corona` is
that region; `Solar Environment` is the broader region containing it, is not wrong, and stands
alongside `Corona` rather than being displaced by it.

Considered and not selected: `Interplanetary Space` — the tool performs no heliospheric propagation
and its parameter space stops inside the coronagraph field of view; the fitted parameters are
*inputs* to propagation models rather than results of one. `Photosphere`, `Chromosphere` and
`Solar Interior` — the model's legs are anchored at the solar centre as a geometric construction, not
as a physical statement about those layers, and no photospheric or chromospheric data is read.

---

### 6. Authors (MANDATORY)
**Author 1**
- **Author Name:** Johan Lauritz Freiherr von Forstner
  (given name `Johan Lauritz`, family name `Freiherr von Forstner`)
- **Author Identifier:** https://orcid.org/0000-0002-1390-4776
- **Affiliation:**
  - **Organization:** Institute of Experimental and Applied Physics, University of Kiel
  - **Affiliation Identifier:** Not found

Sole author. `CITATION.cff`, the Zenodo deposit, and the DataCite creator list all name exactly one
creator, so the union of every authoritative source is this one person; nobody is dropped.

**The authoritative split is given name `Johan Lauritz`, family name `Freiherr von Forstner`.** The
nobiliary particle belongs to the family name, and three independent authoritative sources agree on
that:

- **ORCID 0000-0002-1390-4776** (the author's own self-curated record): `given-names` = `Johan
  Lauritz`, `family-name` = `Freiherr von Forstner`. The employment entry on the same record is
  self-asserted under the source name "Johan Lauritz Freiherr von Forstner".
- **Crossref**, for his own refereed paper 10.1051/0004-6361/202039848: given `Johan L.`, family
  `Freiherr von Forstner`.
- **`CITATION.cff`**: `given-names: Johan L.`, `name-particle: Freiherr von`,
  `family-names: Forstner` — which under the CFF specification renders as "Johan L. Freiherr von
  Forstner", i.e. it agrees on the rendered name and on the particle's role, and differs only in
  storing the particle in a field of its own.

The unabbreviated form above follows ORCID, because it is the author's own record and the only source
giving the middle name in full; `Johan L.` is the acceptable abbreviated alternative if a shorter
given name is ever wanted.

**Previous incorrect value, and why it was wrong.** The name was previously recorded as given
`Johan Freiherr von` / family `Forstner`, which places the nobiliary particle in the given name and
loses the middle name entirely; the split recorded above corrects it. The mis-split's most likely
origin is the Zenodo/DataCite creator string `Forstner, Johan L.`: Zenodo composes a display name from
the CFF's `given-names` + `family-names` and silently drops `name-particle`, so the particle has to be
re-attached by whoever reads the string back — and it was re-attached to the wrong half. **This is a
standing hazard in the upstream sources, not a one-off slip:** any name re-derived from the Zenodo or
DataCite creator string for this software will present the same mis-split, and it should be recognised
rather than re-adopted. ORCID and Crossref, above, are the sources to trust for this name.

**Affiliation.** The recorded organization matches `CITATION.cff`
(`Institute of Experimental and Applied Physics, University of Kiel, Kiel, Germany`), the Zenodo and
DataCite affiliation strings, and `setup.py`'s `author_email` (`forstner@physik.uni-kiel.de`). The
recorded form correctly drops the redundant "Kiel, Germany" city/country tail and contains no
acronyms.

**Affiliation identifier — negative research, and a settled decision to leave it blank.** No ROR
record exists for the institute. A ROR search for "Institute of Experimental and Applied Physics"
returns only same-named institutes in Slovakia, Belarus, Ukraine, Russia and Moldova, none of them
Kiel's. The parent university does have one, `https://ror.org/04v76ef78`
(Christian-Albrechts-Universität zu Kiel), and that ROR was **considered and rejected on the
merits**: the affiliation recorded above names the institute specifically, whereas the university's
ROR identifies a broader entity than the affiliation actually is, so attaching it would assert an
identity the affiliation does not have. The affiliation therefore stands exactly as written, with a
blank identifier — an exact organization name carrying no identifier is preferred here over a
resolvable identifier for the wrong entity.

This is a closed decision rather than an unfilled field: `https://ror.org/04v76ef78` must not be
attached to this affiliation later on the grounds that a resolvable identifier is better than none.
The question would only reopen if ROR were to register the Kiel institute itself, in which case that
new record — not the parent university's — is the identifier to use.

**ORCID employment — deliberately not used as the affiliation.** The only employment on the ORCID
record is "Machine Learning Engineer, Paradox Cat, Munich, DE" from 2021-02 onward, with no
disambiguated organization identifier. That post-dates the software and is consistent with the
README's "I have since left the Heliophysics field"; it is not the affiliation under which this
software was authored. The ORCID *education* entries (BSc, MSc and PhD at
Christian-Albrechts-Universität zu Kiel, the PhD ending 2021-02) corroborate the Kiel affiliation
for the period 2020–2021 when this software was written.

**Other contributors considered and not added as authors.** Two people have merged commits:
Samriddhi Sankar Maity (one commit; credited in the 0.2.3 release notes for the slider-label
improvements) and the GitHub account `asahade` (one commit; credited for simplifying `apex_radius`).
Neither is listed as an author in `CITATION.cff`, the Zenodo deposit, or the DataCite creator list,
so the maintainer's own citation metadata does not credit them as authors and they are not added
here. `asahade`'s legal name is not stated anywhere in the repository or the release notes, so
adding them would additionally require guessing an identity. If the maintainer later credits either
contributor, this is where to start.

---

### 7. Software Name (MANDATORY)
GCS in Python

It is the README's H1 title, the `CITATION.cff` `title`, and the Zenodo/DataCite record title, so all
sources agree.

Considered and rejected: `gcs_python` (the repository slug, which SoMEF reports as the `name` from
the GitHub API) and `gcs` (the `setup.py` distribution name). Field 7 asks for the name of the
software package as listed on the repository, and the repository lists it as "GCS in Python"; the
slug and distribution name are packaging artifacts.

---

### 8. Description (MANDATORY)

> Python 3 implementation of the Graduated Cylindrical Shell model (GCS, Thernisien, 2011). Based on
> the existing IDL implementation in SolarSoft (cmecloud.pro, shellskeleton.pro).
>
> The code in gcs/geometry.py provides the basic implementation of the GCS geometry, while the
> Qt-based GUI in gcs/gui.py uses SunPy and Matplotlib to plot the model on top of coronagraph images
> provided by Helioviewer.org. The GUI retrieves the closest available image for each requested
> spacecraft — SOHO/LASCO (C2 or C3) and STEREO-A or STEREO-B SECCHI (COR1 or COR2) — optionally as
> running-difference images, and lets the user adjust the six GCS parameters (half angle, apex
> height, aspect ratio, heliographic latitude, Stonyhurst longitude and tilt) with sliders until the
> projected model matches the observed CME in all viewpoints simultaneously. The fitted parameters
> can be saved to a JSON file, and the geometry module can be imported on its own to use the GCS mesh
> in other Python plotting code.
>
> A more detailed description of the GCS model, this Python implementation and its validation is
> given in Appendix B of the author's PhD thesis (Freiherr von Forstner, 2021,
> https://nbn-resolving.org/urn:nbn:de:gbv:8:3-2021-00166-5), an excerpt of which is included in the
> repository.

**Previous value, and why the text above supersedes it:**

> Python 3 implementation of the Graduated Cylindrical Shell model (GCS, Thernisien, 2011). Based on
> the existing IDL implementation in SolarSoft (cmecloud.pro, shellskeleton.pro).
>
> The code in gcs/geometry.py provides the basic implementation of the GCS geometry, while the
> Qt-based GUI in gcs/gui.py uses SunPy and Matplotlib to plot the model on top of coronagraph images
> provided by Helioviewer.org.
>
> A more detailed description of the GCS model, this Python implementation and its validation is
> given in this excerpt from my PhD thesis.

The previous text is a faithful lift of the README's opening, and its first two paragraphs are kept
word-for-word in the value above — the author's own wording is not restyled anywhere. Two concrete
defects, neither of them a matter of taste, are why the remainder was rewritten:

1. **A dangling cross-reference.** "given in this excerpt from my PhD thesis" is a hyperlink in the
   README, and HSSI carries no link for it; stripped of its link the phrase points at nothing, and a
   reader of the HSSI record cannot reach the document it promises. The replacement names the thesis
   and gives its resolvable persistent identifier, and drops the first person, which reads oddly in a
   catalogue record written about a third party.
2. **Material incompleteness for the field's stated purpose.** Field 8 asks for enough detail "to
   provide the potential user with information to determine if the software is useful to their work."
   The previous text never said which spacecraft or coronagraphs are supported, what the user
   actually does with the tool, or what comes out of it — the three things a solar physicist needs in
   order to decide. The added sentences state only what the code and the shipped thesis excerpt state: the
   spacecraft/detector choices are the `choices=` lists in `gui.py:main()`, the six parameters are the
   `SliderAndTextbox` instances in `create_widgets()`, running difference is the `-rd` flag, JSON
   output is `save_params()`, and standalone use of `gcs.geometry` is the README's own
   "How to use the GCS geometry in your own plotting code" section.

The narrower alternative — keeping the previous text intact out of strict editorial fidelity to the
README — was considered and not adopted. The first two paragraphs preserve that fidelity verbatim, so
none of the author's voice is lost; and the third paragraph's dangling "this excerpt" reference is a
defect of transplantation rather than a stylistic choice of the author's, since in its original
setting it did resolve.

---

### 9. Concise Description (OPTIONAL)
Python 3 implementation of the Graduated Cylindrical Shell model (GCS, Thernisien, 2011). Based on the existing IDL implementation in SolarSoft (cmecloud.pro, shellskeleton.pro).

This is the first paragraph of the Description in Field 8, and was also the first paragraph of the
previous Description, so the Field 8 rewrite left the two fields in agreement rather than divergent.
It is 178 characters, inside the 200-character limit, and is a genuine preview of the longer text.

---

### 10. Publication Date (RECOMMENDED)
2020-10-12

Field 10 is "Date of first broadcast/publication... Used for the initial version of the software."
The first publication was release 0.1.0: the GitHub release `0.1.0` was published 2020-10-12 with the
release note "First official release.", and the corresponding Zenodo version record
(10.5281/zenodo.4081426, titled "gcs_python: Version 0.1.0", carrying the same "First official
release." description) has `publication_date` `2020-10-12`. The repository itself was created
2020-09-21 and its first commit is the same day, so 2020-10-12 is the first *published*, citable
version rather than the first line of code.

**Previous value `2024-07-06`, and why it was wrong.** That is the release date of 0.2.3, the
newest version — not the first. It is an artifact of deriving the date from the concept DOI: that
DOI's DataCite record reports `dates: [{date: 2024-07-06, dateType: Issued}]` and `publicationYear:
2024`, because a Zenodo concept record surfaces its latest version, and its `Issued` date was taken
as the software's publication date. The date is correct information in the wrong field — it is
already recorded where it belongs, as the Version Date in Field 12 — so holding it here duplicated
the version date while leaving the software's actual first-publication date unrecorded. Note for
any later refresh: anything that re-derives Field 10 from the concept DOI will reproduce exactly
this error, and will do so again each time a new version is released.

---

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Correct per Field 11's rule that Zenodo is the publisher for software whose DOI came through the
GitHub–Zenodo workflow, which this did (the Zenodo record's `IsSupplementTo` relation points at the
`0.2.3` GitHub tag). DataCite likewise reports `publisher: "Zenodo"`.

The identifier is the site URL rather than a ROR because Zenodo has no ROR record — a ROR search for
"Zenodo" returns no results — and Field 11 explicitly permits a URL in that case.

---

### 12. Version (RECOMMENDED)
- **Version Number:** `v0.2.3`
- **Version Date:** 2024-07-06
- **Version Description:** Improved the descriptions on the GUI slider labels, simplified the
  `apex_radius` implementation, fixed an incorrect type for the slider values, and pinned the SunPy
  dependency below 5.2.0.
- **Version PID:** https://doi.org/10.5281/zenodo.12668802

0.2.3 is the newest release. Four independent sources agree on its number, date and DOI, and there is
no newer release:

- Git tags: `0.1.0` (2020-10-12), `0.2.0` (2021-01-15), `0.2.1` (2021-03-06), `0.2.2` (2021-07-09),
  `0.2.3` (2024-07-06). `0.2.3` is the newest, at commit `38fd299633db66d50cf182274445152d735f3e97`.
- GitHub releases: the same five, latest `0.2.3`.
- Zenodo: five versions under the concept DOI, latest 0.2.3 with `publication_date` 2024-07-06 and
  DOI 10.5281/zenodo.12668802.
- `CITATION.cff`: `version: 0.2.3`, `date-released: 2024-07-06`.

The pinned source revision `c8cc9cf` is **two** commits past the `0.2.3` tag, and neither commit
touches code:

- `875e979` "update CITATION.cff" (2024-07-06) changes only `CITATION.cff`. It is the DOI/version
  refresh recorded under Field 2, cut twelve minutes after the release tag: `doi` moves from
  `10.5281/zenodo.5084818` to `10.5281/zenodo.12668802`, and `version`/`date-released` from
  `0.2.2`/`2021-07-09` to `0.2.3`/`2024-07-06`.
- `c8cc9cf` "Update README.md" (2024-08-29) changes only `README.md`, and changes it only by
  inserting a new `### Common issues` troubleshooting subsection after the `gcs_gui -h` block: the
  `command not found: gcs_gui` / `PATH` bullet and the OpenJPEG/glymur `RuntimeError` bullet, six
  added lines and no deletions. It is documentation for an install-time problem, not a change to the
  package. Note for anyone re-deriving this: the two commits past the tag carry the near-identical
  messages "update CITATION.cff" and "Update README.md", and `c8cc9cf` is easily conflated with the
  earlier `424e772` "Update README.md" (2022-02-03), which is the commit that actually added the
  maintainer-availability paragraph quoted in Field 23. `c8cc9cf` does not touch that paragraph, and
  no commit between `424e772` and HEAD does either.

So HEAD carries no unreleased functional change, and no newer version is warranted.

**On the `v` prefix:** the authoritative sources all write the version bare (`0.2.3` in the git tag,
Zenodo, and `CITATION.cff`), whereas the recorded value is `v0.2.3`. The prefixed form is deliberate
and the bare `0.2.3` was considered and not adopted: Field 12's own example is `v1.0.0`, so the
prefix is a sanctioned stylistic form, and rewriting it would produce churn without adding
information. A future refresh should therefore recognise the difference from the git tag and the CFF
as deliberate rather than as drift.

The version number is the bare release identifier. A composite string containing both the software
name and release identifier is not the version number and must not be recorded as one.

**The Version Description** summarises the 0.2.3 release notes as published on the GitHub release and
mirrored in the Zenodo record: better slider-label descriptions (PR #11), a simplified `apex_radius`
implementation (PR #14), a fix for an incorrect slider value type (issue #16), and the SunPy `<5.2.0`
pin (issue #17, visible in `setup.py` as `sunpy[net,jpeg2000]>=2.1.0,<5.2.0`). It is prose rather than
those notes' raw bullet list with GitHub pull-request URLs, since the field asks for a brief summary.

---

### 13. Programming Language (RECOMMENDED)
- Python 3.x

`setup.py` declares `python_requires='>= 3.7'` and the classifier
`Programming Language :: Python :: 3`; the README says "Python 3.7 or later ... are required"; every
source file is Python and the GitHub language statistics report Python only.

`Python 2.x` is excluded by the `>= 3.7` floor. `IDL` was considered and rejected: the package is a
*translation* of SolarSoft IDL routines and contains no IDL code — the lineage belongs in Field 29,
not here.

---

### 14. Reference Publication (RECOMMENDED)
Freiherr von Forstner, J. L. (2021). *Multipoint observations of ICMEs in the inner heliosphere:
Forbush decreases and remote sensing* (PhD thesis, Kiel University), Appendix B: "Implementation of
the Graduated Cylindrical Shell Model in Python".
https://nbn-resolving.org/urn:nbn:de:gbv:8:3-2021-00166-5

This is the only publication that describes *this software*: its Appendix B is a seven-page account
of the package's design (`gcs.geometry`, `gcs.gui`), its data retrieval through the Helioviewer.org
API, its GUI and CLI, its JSON output, and — in section B.3 — its validation against the original
IDL implementation on previously published CME reconstructions. The repository ships that appendix
as `doc/gcs_implementation_forstner_phd_2021.pdf`, and the README links the parent thesis at
exactly the URN above.

**Known deviation from the documented field type — deliberate, and not to be "corrected" back to
empty.** Field 14 is typed as a DataCite DOI, and the identifier recorded above is a URN:NBN rather
than a DOI. This is a considered exception, on three grounds:

- **The thesis provably has no DOI.** The Kiel institutional repository record
  (`https://macau.uni-kiel.de/receive/macau_mods_00001144`) exposes only the URN; the copy shipped in
  the repository carries no DOI; and a DataCite search for records naming this author's ORCID
  (`0000-0002-1390-4776`) as creator returns software deposits exclusively — no text or dissertation
  record of any kind, and nothing bearing the thesis title (checked 2026-08-04). There is simply no
  DOI available to prefer over the URN.
- **URN:NBN is a real persistent-identifier authority**, not an ad-hoc link — the German national
  library's namespace, here under the `de:gbv` sub-namespace — and this URN resolves: it returns a 307
  redirect to the Kiel MACAU record for the thesis (re-checked 2026-08-04).
- **The alternative is strictly worse.** The thesis appendix is the single authoritative document that
  describes and validates this exact software. Leaving Field 14 empty would suppress that fact in
  order to satisfy an identifier-scheme preference, with no DOI available to satisfy it properly.

A validator or agent expecting a `doi.org` URL here will flag this value. That flag is expected: it
should be resolved by reading this note, not by clearing the field.

**Alternatives considered.** *Thernisien (2011)*, ApJS 194, 33 — describes the GCS *model*, not this
software, and belongs in Field 27 (where it is recorded). *Leaving Field 14 empty* — defensible,
since the README designates the Zenodo DOI rather than any paper as the citation and `CITATION.cff`
has no `preferred-citation`; the thesis appendix could instead be listed under Field 27, which
explicitly accommodates non-DOI items. That reading was rejected because a publication that
documents and validates this specific implementation is precisely what Field 14 asks for, and
recording it as merely "related" would understate it.

---

### 15. License (RECOMMENDED)
- **License:** MIT License
- **License URI:** https://spdx.org/licenses/MIT

Three primary sources agree that this software is under the MIT License:

- `LICENSE` is the verbatim MIT License text, opening "MIT License / Copyright (c) 2020 Johan von
  Forstner".
- `setup.py` classifier: `License :: OSI Approved :: MIT License`.
- GitHub's own licence detection reports `{"key": "mit", "spdx_id": "MIT", "name": "MIT License"}`.

**Do not copy Zenodo here.** The Zenodo record for every version, and DataCite in turn
(`rightsList: [{rights: "Other (Open)", rightsIdentifier: "other-open"}]`), reports the licence as
`other-open`. That is wrong, and its origin is identifiable: `CITATION.cff` contains
`license: other-open`, which is not a valid SPDX identifier — the Citation File Format requires an
SPDX id such as `MIT`, while `other-open` is a Zenodo-internal licence id. Zenodo ingested the CFF
value verbatim and DataCite mirrored Zenodo. All five versions carry the same error, so its
consistency across the DOI record is not corroboration. The repository's own LICENSE file and
packaging classifier are authoritative; `Other` would encode Zenodo's mistake into HSSI.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)
- cme
- coronal mass ejections
- solar physics
- coronagraph
- flux rope reconstruction
- 3D visualization
- gui
- graduated cylindrical shell

All eight terms describe this software directly. `cme`, `coronal mass ejections` and `solar physics`
are its broad subject terms — a solar-physics tool whose entire purpose is reconstructing CMEs. Every
keyword is recorded lower-case, and case is not significant to a keyword's identity, so a Title-Case
rendering ("Cme", "Coronal Mass Ejections", "Solar Physics") denotes the same terms rather than
different ones, and should not be treated as a second set of keywords.

The next four are each repository-evidenced:

- **coronagraph** — the entire tool operates on coronagraph imagery (LASCO C2/C3, SECCHI COR1/COR2);
  the single most likely search term after "GCS" itself.
- **flux rope reconstruction** — exactly what the software does; the thesis excerpt describes the GCS
  model as representing "the three-dimensional structure of flux rope coronal mass ejections."
- **3D visualization** — `sample.py`'s `Axes3D`/`plot_trisurf` rendering of the mesh, and the 3D
  wireframe shown as Figure 15 of the thesis excerpt. Recorded in this spelling (lower-case
  "visualization") so it is not multiplied into casing variants of the same term.
- **gui** — an author-curated GitHub repository topic, and structurally central: the package's whole
  reason for existing beyond `gcs.geometry` is the interactive Qt fitting GUI, and its console entry
  point is `gcs_gui`.

**graduated cylindrical shell** is the model's full name and the most distinctive retrieval term
for this record. Keywords are the form's only open vocabulary — the one field where a term need not
already be in established use to be a valid value — and no established near-match stands in for
this one: the only keyword containing any of "graduated", "cylindr" or "shell" is `l shell`, a
magnetospheric coordinate concept unrelated to the GCS geometry. It is therefore recorded in full
rather than approximated.

Considered and not selected, so a future agent need not re-litigate them:

- **python**, **python 3**, **python package** — carried by Field 13.
- **sunpy** — carried by Field 30.
- **stereo**, **soho** — carried by Field 32.
- **corona** — carried by Field 5.
- **empirical model** — carried by Field 4.
- **solar soft** — carried by Field 29; the SolarSoft lineage is recorded there with the specific
  routines.
- **coronalmassejections** — the un-spaced GitHub topic; a normalisation variant of the existing
  `coronal mass ejections` above and exactly the kind of near-duplicate the field guidance warns
  against.
- **space weather** — GCS parameters are a standard input to CME arrival-time forecasting, but this
  software neither forecasts nor propagates; the connection is downstream of it.
- **geometry** — too generic to aid retrieval despite matching the module name.

---

### 17. Data Sources (OPTIONAL)
- Observatory/Mission-specific
- Other

**Observatory/Mission-specific** — the retrieval code does not browse a generic catalogue; it asks
for named observatory/instrument/detector triples. `gui.py:load_image()` maps the CLI spacecraft
argument onto exactly `('STEREO_A','SECCHI',COR1|COR2)`, `('STEREO_B','SECCHI',COR1|COR2)` and
`('SOHO','LASCO',C2|C3)`, and raises `ValueError` for anything else. This is the cross-listing that
Fields 17 and 31/32 jointly require: the missions themselves are recorded in Field 32.

**Other** — two retrieval services the software depends on have no more specific applicable value in
the Data Sources vocabulary: the **Helioviewer.org API** (`gcs/utils/helioviewer.py` builds a
`sunpy.net.helioviewer.HelioviewerClient` and falls back to the IAS mirror
`https://helioviewer-api.ias.u-psud.fr/`; `gui.py` calls `hv.download_jp2(...)`), and **JPL Horizons**
(queried through `sunpy.coordinates.get_horizons_coord('SOHO', ...)` for the SOHO observer location).
Field 17 directs unlisted sources to `Other`.

Considered and rejected:

- **HTTP/HTTPS Directories** — Helioviewer is a parameterised query API returning a chosen image, not
  a browsable directory tree; no directory listing is ever fetched.
- **The Virtual Solar Observatory.** — `sunpy[net]` is installed, so a VSO client is present in the
  environment, but the code imports only `sunpy.net.helioviewer` and never touches VSO. Listing it
  would claim a capability the software does not have.
- **CDAWeb**, **SSCWeb**, **HAPI**, **AMDA**, **S3/Cloud-aware** and the remainder of the vocabulary
  — none appears anywhere in the code or documentation.

---

### 18. Input File Formats (RECOMMENDED)
- Other
- JSON

**Other** stands for **JPEG2000** (`.jp2`), the format of every science image this software reads;
the file-format vocabulary has no more specific value for it. Evidence: `hv.download_jp2(...)` in
`gui.py:download_helioviewer()` and in `sample_sunpy.py`; `setup.py` requires the
`sunpy[net,jpeg2000]` extra; and the README's troubleshooting section documents the OpenJPEG
dependency needed to decode them ("Loading Helioviewer images with SunPy requires the OpenJPEG
library"). The thesis excerpt is explicit: the Helioviewer.org API "directly provides images in
JPEG2000 format."

**JSON** — `gui.py:load_params()` reads a previously saved `gcs_params.json` on startup and falls back
to defaults when absent, so JSON is genuinely an input as well as an output.

**FITS was considered and deliberately rejected**, which is worth recording because it is the obvious
guess for a solar imaging tool and because `sunpy.map.Map` would accept a FITS file. Nothing in this
repository ever reads FITS: every image path goes through `download_jp2`. The thesis excerpt states
the design intent directly — the JPEG2000 route "drastically simplifies and speeds up the process
compared to the IDL version, where images in FITS format need to be downloaded manually from the
respective mission sites, and where the calibration procedure needs to be applied locally." Not
reading FITS is a feature of this port, not an omission in this record.

`CDF`, `netCDF3/4`, `HDF5`, `IDL.sav`, `ascii`, `csv`, `ISTP-Compliant` and `Zarr` do not appear
anywhere in the code.

---

### 19. Output File Formats (RECOMMENDED)
- JSON

`gui.py:save_params()` writes the six fitted GCS parameters to `gcs_params.json` via `json.dump`,
triggered by the GUI's Save button. Those parameters are the scientific product of the tool, so
JSON is its data output format. The thesis excerpt confirms the choice and the reasoning: the
parameters "are stored in the JavaScript Object Notation (JSON) format, a general-purpose data
format that is human-readable and can be easily handled with most modern programming languages."

**Considered and not selected: `Other` for figure export.** The GUI embeds matplotlib's
`NavigationToolbar2QT`, so the user can save the displayed panels as PNG/PDF/SVG, and the thesis
excerpt lists this among the GUI's features ("saving the current set of images to a file"). It was
not selected because a saved figure is a graphic rather than a data product, the file-format
vocabulary contains no graphics format, and an `Other` here would be indistinguishable from the
`Other` recorded in Field 18 for JPEG2000 while conveying much less. The exclusion is settled; the
capability is recorded here so a future agent meets the evidence for it and can see that it was
weighed and set aside rather than overlooked.

---

### 20. Operating System (RECOMMENDED)
- Operating System Independent

`setup.py` declares the classifier `Operating System :: OS Independent` — the package's own
authoritative claim — and there is nothing platform-specific in it: pure Python plus numpy, scipy,
matplotlib, sunpy and PyQt5, all of which ship for Linux, macOS and Windows.

Note the exact wording: the controlled value is `Operating System Independent`, spelled out.
`OS Independent`, the literal classifier string, is not a value in that vocabulary, so the classifier
must not be copied across verbatim.

Listing `Linux`, `Mac` and `Windows` individually was considered and rejected as redundant with the
independent value. The README's troubleshooting notes are Linux-flavoured (`~/.local/bin`,
`apt install libopenjp2-7-dev`) but are offered as examples alongside conda and manual OpenJPEG
installation, not as a platform restriction. There is no CI configuration in the repository, so no
tested-platform matrix exists to narrow this further.

---

### 21. CPU Architecture (RECOMMENDED)
- CPU Independent

The package contains no compiled extension, no build step beyond `setuptools`, and no
architecture-specific code — `setup.py` has `packages=['gcs','gcs.utils']` and nothing else. Every
dependency is available as a wheel or build for x86-64, Apple Silicon and aarch64, so nothing
narrows the architecture. Enumerating `x86-64` + `Apple Silicon arm64` + `Linux aarch64 or arm64`
was rejected: it would assert a tested matrix that does not exist, where `CPU Independent` states
the actual situation.

---

### 22. Related Phenomena (OPTIONAL)
- Coronal Mass Ejections

Clearly correct — the software exists to reconstruct the three-dimensional structure of CMEs.

Considered and not selected: **Solar Corona** — the corona is where the observations are made, which
Field 5 already records as the related region; the phenomenon the software analyses is the CME
itself. **Solar Wind**, **Solar Flares**, **Coronal Heating**, **Geomagnetic Storms**, **X-ray
emission** — none is modelled, measured or analysed. This vocabulary is closed, so a phenomenon with
no value of its own would belong in Keywords; no such phenomenon arises here.

---

### 23. Development Status (RECOMMENDED)
Inactive

repostatus.org defines `Inactive` as "reached a stable, usable state but is no longer being actively
developed; support/maintenance provided as time allows", which matches the evidence precisely:

- **Reached a stable, usable state.** Five tagged releases with version DOIs spanning 2020-10-12 to
  2024-07-06; a validation section in the thesis excerpt concluding "This shows that the Python
  version is implemented correctly and can be used for scientific purposes."
- **No longer actively developed.** The last release (2024-07-06) was maintenance only — a dependency
  pin plus small fixes — and the last commit (2024-08-29) edits the README. The repository is not
  archived, but nothing functional has changed in over two years.
- **Support as time allows.** The README: "As I have since left the Heliophysics field and am no
  longer actively using the tool myself, I can't promise timely responses. But it is still
  preferrable compared to writing me an email in private, as other users can also help you",
  followed in the same passage by an invitation to open pull requests. The author's ORCID confirms he
  moved to an unrelated industry post in 2021-02.

  **The date of that statement matters, and it is not the date of the last commit.** The sentence was
  added by commit `424e772` (2022-02-03) and has stood unaltered since; no later commit, including
  the 2024-08-29 README edit, touches it. So the maintainer's stated departure from heliophysics
  *predates* the final maintenance-only release (0.2.3, 2024-07-06) by more than two years instead of
  coinciding with the end of the commit history. This makes the `Inactive` reading stronger rather
  than weaker: the two years of activity that followed the statement — a dependency pin, small fixes,
  merged contributions from two outside users, a release, and a troubleshooting note — are exactly
  the "support/maintenance provided as time allows" that repostatus.org's `Inactive` describes, and
  they are demonstrably not the tail end of active development. A future agent should not read the
  availability notice as a farewell coincident with the last commit.

Alternatives rejected:

- **Active** — contradicted by the author's own statement and by two years without a functional
  change.
- **WIP** — the README's "This code is still in a quite early stage" is the strongest pull toward
  this, but `WIP` requires "no stable, usable public release yet", and there are five public releases
  with DOIs plus a published validation. The caveat is about scientific maturity (validated on only a
  few case studies), not about release status.
- **Unsupported** — requires that the authors have ceased work and that a new maintainer is desired.
  The author still triages issues and invites pull requests and has never asked for a successor.
- **Abandoned** — requires no stable release; five releases exist.
- **Suspended** — requires a stated intent to resume; the author states the opposite.
- **Moved** — the Kiel GitLab mirror named in the thesis excerpt was a mirror, not a relocation;
  GitHub remains the location named by `CITATION.cff` and by the Zenodo deposit. The point is now
  moot in any case: the mirror's host no longer resolves in DNS (NXDOMAIN, checked 2026-08-04), so
  there is nowhere for the project to have moved *to* (see Field 3).

---

### 24. Documentation (RECOMMENDED)
https://github.com/johan12345/gcs_python/blob/master/README.md

The README **is** the documentation: it contains the installation instructions ("How to install and
run the GUI"), the CLI invocation, a troubleshooting section ("Common issues", covering the `PATH`
and OpenJPEG problems), library usage ("How to use the GCS geometry in your own plotting code"),
and the development setup. Field 24 explicitly allows the documentation link to coincide with the
access URL.

Negative research: there is no documentation site, no `docs/` directory, no Read the Docs or Sphinx
configuration, and no GitHub Pages site; SoMEF found no documentation URL either. The only `doc/`
content is the thesis-excerpt PDF, which is a scholarly description rather than user documentation
and is recorded in Field 14.

Note the branch pin: the default branch is `master`, not `main`. The repository root URL
(`https://github.com/johan12345/gcs_python`) renders the same README and would be immune to a branch
rename; it was not chosen because it duplicates Field 3 exactly and points at the repository rather
than at the document. If the default branch is ever renamed, this URL is the one to fix.

---

### 25. Funder (OPTIONAL)
Not found

Negative research, so this is not re-searched from scratch next time: there is no funding statement
or acknowledgement anywhere in the repository (no `README` acknowledgements section, no
`CITATION.cff` funding key, no `AUTHORS`/`CONTRIBUTING`/`.zenodo.json` files at all); the Zenodo
deposit has no grants; and DataCite reports `fundingReferences: []` for both the concept DOI and the
0.2.3 version DOI. The shipped thesis excerpt is an appendix and carries no acknowledgements.

The author's contemporaneous refereed paper (10.1051/0004-6361/202039848) does acknowledge funding,
but that funding belongs to the paper's research programme; attributing it to this software would be
an inference, not evidence.

---

### 26. Award Title (OPTIONAL)
Not found

No award or grant identifier appears in the repository, the Zenodo deposit, or the DataCite records.
Consistent with Field 25.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)
- https://doi.org/10.1088/0067-0049/194/2/33 — Thernisien, A. (2011). *Implementation of the
  Graduated Cylindrical Shell Model for the Three-dimensional Reconstruction of Coronal Mass
  Ejections.* The Astrophysical Journal Supplement Series, 194, 33.
- https://doi.org/10.1086/508254 — Thernisien, A. F. R., Howard, R. A., & Vourlidas, A. (2006).
  *Modeling of Flux Rope Coronal Mass Ejections.* The Astrophysical Journal, 652, 763.
- https://doi.org/10.1051/0004-6361/202039848 — Freiherr von Forstner, J. L., Dumbović, M.,
  Möstl, C., et al. (2021). *Radial evolution of the April 2020 stealth coronal mass ejection between
  0.8 and 1 AU.* Astronomy & Astrophysics.

All three DOIs were verified against Crossref (titles, authors, years, journals and pagination as
given above).

Why each belongs:

- **Thernisien (2011)** is the paper this software implements. The README cites it in its first
  sentence, and the Description in Field 8 names it. Its mathematical derivation is the specification
  for `gcs/geometry.py`.
- **Thernisien, Howard & Vourlidas (2006)** is the original GCS model paper and the origin of the IDL
  implementation and GUI that this package was ported from. In-repository evidence: the shipped thesis
  excerpt cites "Thernisien et al., 2006" as the model's origin and states that "The original
  implementation of the GCS model in the Interactive Data Language (IDL) and a corresponding graphical
  user interface (GUI) were developed by Thernisien et al. (2006)".
- **Freiherr von Forstner et al. (2021)** is the study during which this software was written and in
  which it was applied. The thesis excerpt says so: the implementation "ha[s] been developed during
  the course of the study presented in Freiherr von Forstner et al. (2021)", and the excerpt's
  Figure 16 shows the GUI fitting that paper's April 15, 2020 CME — the same event used as the
  README's example invocation `gcs_gui "2020-04-15 06:00" STA SOHO`.

Considered and not listed here: the PhD thesis itself, which is recorded in Field 14 as the reference
publication rather than duplicated here; and Gou et al. (2020), cited in the excerpt's validation
section only as the source of a previously published IDL reconstruction used as a comparison case,
which describes neither this software nor the model.

---

### 28. Related Datasets (OPTIONAL)
Not found

Negative research. The software consumes SOHO/LASCO and STEREO/SECCHI coronagraph imagery, but it
does so through the Helioviewer.org API's browse-quality JPEG2000 products rather than any citable
dataset: no dataset DOI, SPASE `NumericalData` identifier, or archive product identifier appears
anywhere in the code, README, `CITATION.cff`, or the Zenodo/DataCite records. The missions
themselves are recorded in Field 32 and their coronagraphs in Field 31, which is where a searcher
would look. Inventing a plausible dataset landing page would assert a link the repository does not
make.

---

### 29. Related Software (OPTIONAL)
- https://www.lmsal.com/solarsoft/ — **SolarSoft** (`scraytrace`: `cmecloud.pro`,
  `shellskeleton.pro`) — the original IDL implementation this package is a port of.
- https://doi.org/10.5281/zenodo.5713659 — **PyThea** — an independent Python package that also
  implements GCS reconstruction from multi-viewpoint coronagraph observations.

**SolarSoft** is the predecessor this software was translated from — the strongest possible Field 29
relationship. The evidence is in the code itself, not merely in prose: `gcs/geometry.py:skeleton()`
is documented "Based on IDL version shellskeleton.pro" with the SSW source URL
`https://hesperia.gsfc.nasa.gov/ssw/stereo/secchi/idl/scraytrace/shellskeleton.pro`, and
`gcs_mesh()` likewise "Based on IDL version cmecloud.pro" with its SSW URL. The README's second
sentence and the Description in Field 8 both say the package is "Based on the existing IDL
implementation in SolarSoft (cmecloud.pro, shellskeleton.pro)", and the thesis excerpt devotes a
paragraph to the `scraytrace` lineage and to why a Python re-implementation was wanted (IDL licence,
SSWDB installation, hard-coded STEREO-only support). The identifier is the SolarSoft home page the
README links, because SolarSoft has no DOI and no single public code repository; the `hesperia`
`scraytrace` URLs above are the routine-level provenance and are recorded in this note rather than as
the identifier.

**PyThea** rests on external verification rather than on repository evidence, and that distinction is
part of the record rather than a reason to omit it. It is a Python package implementing the same GCS
model for CME reconstruction from the same SOHO and STEREO remote-sensing observations, published in
Frontiers in Astronomy and Space Sciences (10.3389/fspas.2022.974137). Field 29 exists for
*distinguishing* software, and PyThea is the actively maintained alternative for exactly this task,
so it is the most useful similar tool a reader of this record can be sent to.

**Its identifier is the Zenodo concept DOI**, `https://doi.org/10.5281/zenodo.5713659`, confirmed to
be the all-versions parent rather than a version DOI: the record it resolves to reports
`conceptdoi: 10.5281/zenodo.5713659` while carrying a version DOI of its own (v1.3.0, at
10.5281/zenodo.20648868 when checked), and its title is "PyThea: A software package to reconstruct
the 3D structure of CMEs and shock waves". Field 29 accepts either a DOI or a repository URL, and
the concept DOI is preferred over the repository URL `https://github.com/AthKouloumvakos/PyThea`
because it survives any future move, rename, or transfer of the source — the same reasoning that
applies to the Astropy entry in Field 30, so the two entries are identified consistently. The
GitHub URL is recorded here as PyThea's source location, which is still where a reader goes for the
code.

**Nothing in this repository mentions PyThea.** The two projects appear to have been developed
independently, and the association rests wholly on the external evidence above — a future agent
should not go looking in the repo for a citation that is not there, nor treat its absence as a reason
the entry is unsupported. The stricter alternative — confining Field 29 to relationships the
repository itself asserts, which would leave SolarSoft as the only entry — was considered and not
adopted, because a reader comparing GCS implementations is materially better served by the pointer
while the provenance of the claim stays visible here.

Considered and rejected — all Tier A generic infrastructure, excluded from Field 29 as firmly as from
Field 30: **numpy**, **scipy**, **matplotlib** and **PyQt5**. Each is a declared dependency and each
is used heavily (`scipy.spatial.transform.Rotation` for the mesh rotation, PyQt5 for the whole GUI),
but "depends on numpy and matplotlib" is true of most of the ecosystem and distinguishes nothing.
**astroquery** was also rejected: it is present in `install_requires` only because
`sunpy.coordinates.get_horizons_coord` needs it for the JPL Horizons query, and the code never
imports it directly.

---

### 30. Interoperable Software (OPTIONAL)
- https://doi.org/10.5281/zenodo.591887 — **SunPy**
- https://doi.org/10.5281/zenodo.4670728 — **Astropy**

**SunPy.** `10.5281/zenodo.591887` is SunPy's concept DOI (DataCite title "sunpy: A Core Package for
Solar Physics"). The interoperation is demonstrated, not assumed, and at an unusually high standard:

- `gcs/geometry.py:gcs_mesh_sunpy()` exists solely to hand the model to SunPy. Its docstring:
  "Provides the GCS model mesh in SunPy SkyCoord format. This can be directly plotted using SunPy."
  That is an adapter/converter API in the sense Field 30 requires.
- `gcs/gui.py` builds `sunpy.map.Map` objects, uses `ax.plot_coord(mesh, ...)` against a SunPy map
  projection, and transforms the mesh into the map's `coordinate_frame`.
- `setup.py` pins `sunpy[net,jpeg2000]>=2.1.0`, and the thesis excerpt explains why the floor is
  exactly 2.1: a LASCO rotation-metadata bug was worked around in this GUI and the author "also
  submitted a patch to the SunPy project to address this issue, which is included in version 2.1 of
  SunPy". A merged upstream contribution and a matching version floor are about as concrete as
  interoperability evidence gets.

**Astropy** qualifies on cited evidence of a specific exchange rather than on dependency presence —
the higher bar this field applies to foundational scientific-Python packages. The public API's
documented interchange object is an Astropy one: `gcs_mesh_sunpy()` returns an
`astropy.coordinates.SkyCoord` built with `frame=frames.HeliographicStonyhurst,
representation_type='cartesian'`, and consumers work with it as such — `gui.py` imports
`astropy.units` and `astropy.coordinates.concatenate` to combine and reproject the returned
coordinates. The narrower reading — keeping Field 30 to SunPy alone, on the grounds that
the documented interoperation target is SunPy and Astropy arrives as its foundation — was considered
and not adopted: the object that actually crosses this package's boundary is an Astropy `SkyCoord`, a
shared data model rather than a transitive install.

The identifier is Astropy's Zenodo **concept** DOI, `https://doi.org/10.5281/zenodo.4670728`,
verified as the `conceptdoi` of the Astropy software record (DataCite title "Astropy", resource type
Software, publisher Zenodo) and confirmed resolvable to the latest Astropy version record. The
repository URL `https://github.com/astropy/astropy` was considered and not used: the field accepts
either a DOI or a repository URL, and the concept DOI is the more stable of the two, survives any
future move of the source, and matches how the SunPy entry beside it is identified.

Considered and rejected: **numpy**, **scipy**, **matplotlib**, **PyQt5** (Tier A generic
infrastructure — arrays, numerical routines, plotting, GUI toolkit; equally at home in a web app or a
finance model); **astroquery** (transitively required for the Horizons query, never imported, no
exchange of data models). Also rejected as a justification in its own right: the fact that this
package sits in the scientific-Python ecosystem. `Helioviewer.org` and `JPL Horizons` are services
rather than software packages and are recorded in Field 17.

---

### 31. Related Instruments (OPTIONAL)
- **Instrument Name:** STEREO-A SECCHI Cor1 Coronagraph
  **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-A/SECCHI/Cor1
- **Instrument Name:** STEREO-A SECCHI Cor2 Coronagraph
  **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-A/SECCHI/Cor2
- **Instrument Name:** STEREO-B SECCHI Cor1 Coronagraph
  **Instrument Identifier:** https://spase-metadata.org/NASA/Instrument/STEREO-B/SECCHI/Cor1
- **Instrument Name:** STEREO-B SECCHI Cor2 Coronagraph
  **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/STEREO-B/SECCHI/Cor2
- **Instrument Name:** Large Angle Spectroscopic Coronagraph
  **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/SOHO/LASCO

Each name above is the canonical SPASE name for the instrument, recorded verbatim alongside that
instrument's SPASE identifier. Every entry resolves to one specific instrument, unambiguously.

**Relevance.** These are not incidental mentions. `gui.py:load_image()` hard-codes the complete set of
supported sources and rejects everything else:

```
STA  -> observatory 'STEREO_A', instrument 'SECCHI', detector in {COR1, COR2}
STB  -> observatory 'STEREO_B', instrument 'SECCHI', detector in {COR1, COR2}
SOHO -> observatory 'SOHO',     instrument 'LASCO',  detector in {C2, C3}
```

The CLI enforces the same closed sets (`choices=['STA','STB','SOHO']`, `-stereo` restricted to
`COR1`/`COR2`, `-soho` to `C2`/`C3`), and the README's example is `gcs_gui "2020-04-15 06:00" STA
SOHO`. A scientist working with COR2 or C2 data would reach for this tool, and it visualises those
instruments' measurements as its primary function — the designed-to-support test in both directions.

**Why exactly these four STEREO detectors.** The code's own supported-detector sets name COR1 and COR2
for both STEREO-A and STEREO-B, and nothing else — so the four detector entries are read off the
supported set rather than inferred, and each names one specific coronagraph.

**Identifier namespaces.** The four STEREO detector identifiers are split across two SPASE
authorities: Cor1 under `NASA/Instrument/...` and Cor2 under `SMWG/Instrument/...`. That asymmetry is
how SPASE itself registers these detectors, not an inconsistency to normalise — there is no `SMWG`
Cor1 or `NASA` Cor2 identifier for these instruments to prefer instead, so a future agent should not
"correct" the namespaces into agreement.

**LASCO is recorded at instrument-suite level because no detector-level identifier exists for it.**
SPASE registers LASCO as a single instrument suite, with no C2 or C3 children: nothing whose name
mentions a coronagraph, and nothing whose identifier path contains `SOHO`, corresponds to C2 or C3.
`SMWG/Instrument/SOHO/LASCO` is therefore the only identifier available for the detectors this
software actually reads. It slightly over-states scope, since the software supports C2 and C3 but not
the long-defunct C1; recorded so nobody later reads the suite-level entry as an error.

Considered and deliberately **not** listed:

- **The SECCHI suite** — `Stereo-A Sun Earth Connection Coronal and Heliospheric Investigation`
  (`SMWG/Instrument/STEREO-A/SECCHI`) and its STEREO-B counterpart are available identifiers, and the
  code does pass `instrument='SECCHI'`. They were rejected because naming the suite would claim
  support for EUVI, HI-1 and HI-2 as well, and the code explicitly rejects every detector except COR1
  and COR2. The four detector-level identifiers are both more specific and more truthful.
- **WISPR (Parker Solar Probe), Metis and SoloHI (Solar Orbiter)** — the thesis excerpt names these as
  instruments the toolkit "may also be easily extended to include support for ... as soon as they are
  implemented in SunPy." That is an explicit statement of *future* support; instruments one could
  write a module for are excluded by the relevance gate. Recorded here because the excerpt is shipped
  in the repository and a future agent will encounter the sentence.

---

### 32. Related Observatories (OPTIONAL)
- **Observatory Name:** Solar Terrestrial Relations Observatory A
  **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-A
- **Observatory Name:** Solar Terrestrial Relations Observatory B
  **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/STEREO-B
- **Observatory Name:** Solar and Heliospheric Observatory
  **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/SOHO

Each name above is the canonical SPASE name for the observatory, recorded verbatim alongside that
observatory's SPASE identifier. All three resolve to one specific spacecraft each.

**Relevance** rests on the same `load_image()` dispatch and CLI `choices` as Field 31: these are the
only three platforms the software can retrieve data for, they are named as literal observatory strings
in the Helioviewer requests (`'STEREO_A'`, `'STEREO_B'`, `'SOHO'`), and `download_helioviewer()`
contains SOHO-specific handling that patches the observer location from JPL Horizons. Field 17 is
cross-listed as `Observatory/Mission-specific` accordingly.

**Choice of cataloguing authority.** Each of these three spacecraft is registered by more than one
authority under more than one name, and the canonical `SMWG` registry identifier is the one recorded
in every case:

- SOHO — `SMWG/Observatory/SOHO` (selected) and `CNES/Observatory/CDPP-AMDA/SOHO`, an
  archive-specific mirror, both carry the name `Solar and Heliospheric Observatory`; `SMWG` is the
  canonical registry.
- STEREO-A — `SMWG/Observatory/STEREO-A` (selected, name `Solar Terrestrial Relations Observatory A`)
  versus `CNES/Observatory/CDPP-Archive/STEREO-A` (name `STEREO-A`) and
  `CNES/Observatory/CDPP-AMDA/STEREO-A` (name `STEREO Ahead`). One spacecraft, three registrations
  differing only by cataloguing authority; `SMWG` is canonical, and its long-form name is recorded
  verbatim rather than shortened.
- STEREO-B — `SMWG/Observatory/STEREO-B` (selected) over the equivalent `CNES/Observatory/...`
  registrations named `STEREO-B` and `STEREO Behind`.

Considered and not selected: the **mission-level** `SMWG/Observatory/STEREO`
(`Solar-Terrestrial Relations Observatory`). The software addresses the two spacecraft individually —
they are separate viewpoints and the whole point of the tool is combining them — and both are already
listed, so the mission-level identifier would add breadth without adding information. Also not
selected: **Parker Solar Probe** and **Solar Orbiter**, which the thesis excerpt names only as
possible future extensions (see Field 31).

---

### 33. Logo (OPTIONAL)
Not found

Negative research. The repository contains exactly one image, `img/screenshot.png`, embedded in the
README as `![Screenshot](/img/screenshot.png?raw=true)` — a screenshot of the GUI, not a logo, and
recorded as such by the thesis excerpt's Figure 16. There is no logo file, no favicon, no branding
asset, and no logo in the Zenodo deposit or the PyHC registry (this package is not registered there;
see below). Using the screenshot as a logo would misrepresent it.

---

## Cross-cutting negative research

**PyHC registry.** This package is **not** listed in any of the three PyHC registry files — core,
community, or unevaluated — under its name, its repository URL, or its description. So no curated
PyHC metadata (logo, docs URL, keywords, maturity ratings) is available for any field, and its
absence is not a defect: most heliophysics packages are not PyHC members. Worth recording because
several fields above (Logo, Documentation, Development Status) would normally draw on PyHC first.

**Sources that add nothing beyond the above.** SoMEF's extraction from the repository agrees with
the values above (MIT licence via the GitHub API, full title "GCS in Python", Python as the only
language, five releases with `0.2.3` latest, the `CITATION.cff` dump, the screenshot as the only
image) and adds no field this file does not already cover; in particular it found no documentation
URL and no repository-status signal. The GitHub repository metadata contributed the topic list used
in Field 16 and the `master` default branch used in Field 24; its `description` ("Graduated
cylindrical shell CME model in Python") is a one-line summary already subsumed by Fields 8 and 9.
