# HSSI Metadata Extraction Results

**HSSI Software ID:** 96059067-e0dd-4d80-b2bf-60ec9378609d
**Repository:** https://github.com/ConorMacBride/mcalf
**Source Revision:** 8f2a3dfb6c7c4e99341371bcfed6f89ed6843964
**Extraction Date:** 2026-08-07
**Validation Date:** 2026-08-10
**Validation Status:** PASS

---

**Scope note.** MCALF is a small, feature-complete Python package whose last source commit is
2023-03-17 and whose current release is v1.0.0 (2023-03-28). Everything below is reconciled
against that pinned revision, against the published Zenodo/DataCite records for the concept and
v1.0.0 DOIs, and against the two peer-reviewed papers the repository itself points to. Where the
repository is silent, the JOSS paper (`paper/paper.md`, in-repo) and the *Philosophical Transactions
A* reference paper are treated as primary sources, because both are authored by the software's
authors and describe this code specifically.

Each field records its value, the authoritative source behind it, and — where a value was chosen
over a credible alternative, or supersedes an earlier stored one — the alternatives that were
weighed and why they lost. Those rejected alternatives and documented omissions are as much a part
of the record as the values themselves: they exist so a later refresh does not re-derive a question
that has already been answered.

---

## Section 1: Basic Information

### 1. Submitter (MANDATORY)
- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The HSSI record does not expose who originally submitted this entry, so no attribution can be
recovered from the API. The submitted wording throughout this record is treated as deliberate and is
preserved unless primary evidence contradicts it.

### 2. Persistent Identifier (RECOMMENDED)
- **DOI:** https://doi.org/10.5281/zenodo.3924527

This is the Zenodo **concept** DOI, which resolves to all versions — the correct choice for this
field. Confirmed as the concept DOI three ways: the Zenodo v1.0.0 record reports
`conceptdoi: 10.5281/zenodo.3924527`; the DataCite record for 3924527 carries six `HasVersion`
relations (3924528, 4265382, 4689589, 4767888, 5803548, 7779553); and `README.rst` uses it for both
the Zenodo DOI badge and the "Please also cite the Zenodo DOI" instruction.

Do not replace this with the v1.0.0 DOI (10.5281/zenodo.7779553) — that belongs in Field 12 as the
Version PID, and both are recorded here in their correct places.

### 3. Code Repository (MANDATORY)
- **URL:** https://github.com/ConorMacBride/mcalf

Confirmed live (GitHub API: not archived, not disabled, default branch `main`, issues enabled).
`setup.cfg` and PyPI record the trailing-slash variant `https://github.com/ConorMacBride/mcalf/`;
the canonical no-slash form already stored is preferred and is exactly what CITATION.cff records in
`url:`. The DataCite `IsSupplementTo` relation on both the concept and v1.0.0 DOIs is
`https://github.com/ConorMacBride/mcalf/tree/v1.0.0` — a tag-pinned tree URL, so it is consistent
with the stored value rather than identical to it, and is not a competing candidate for this field.

### 4. Software Functionality (MANDATORY)

This vocabulary is hierarchical and does not add a parent automatically, so every subcategory
below is listed together with its parent category.

**Data Processing and Analysis** (parent)

- **Data Processing and Analysis: Analysis** — `mcalf.models.FitResult.velocity` and
  `mcalf.models.FitResults.velocities` derive line-of-sight Doppler velocities in km/s from fitted
  line-core wavelengths; `IBIS8542Model._fit` computes a sigma-weighted chi-squared for every fit;
  `ModelBase.test` reports classification accuracy statistics and a
  `sklearn.metrics.classification_report`. These are derived physical quantities and statistical
  measures, not mere data handling.
- **Data Processing and Analysis: Data Reduction** — `mcalf.utils.smooth.moving_average` (boxcar
  average), `mcalf.utils.smooth.smooth_cube` (Gaussian noise reduction of a velocity cube with
  boundary weighting), and `mcalf.utils.smooth.mask_classifications(..., reduce=True)` (collapses a
  3-D classification cube to 2-D by most-common valid class per pixel). All three are public,
  exported in `__all__`, and reduce data volume while preserving information.
- **Data Processing and Analysis: ML/AI** — `ModelBase.train` / `test` / `classify_spectra` drive a
  `sklearn.neural_network.MLPClassifier` (wrapped in `sklearn.model_selection.GridSearchCV` over
  `alpha`) to assign a spectral-shape class to every spectrum before fitting. This is the package's
  defining method.
- **Data Processing and Analysis: Processing** — `ModelBase.get_spectra` runs the processing chain:
  spline reinterpolation onto a constant wavelength grid
  (`mcalf.utils.spec.reinterpolate_spectrum`), optional prefilter-response division, and background
  subtraction. `mcalf.utils.spec.normalise_spectrum` and `generate_sigma` are further public
  pipeline steps.
- **Data Processing and Analysis: Spectrogram** — the one value here whose justification is
  representational rather than technical: nothing else in this set conveys that MCALF handles
  spectra at all. Its full reasoning, including the negative search that constrains it, follows the
  rejected values below.
- **Data Processing and Analysis: Time Series Analysis** — `smooth_cube` takes a `[time, row,
  column]` cube and smooths it with `gaussian_kern_3d`, whose `sigma` argument is documented as
  "Sigma values for the time, horizontal and vertical dimensions" — explicit temporal filtering.
  `mask_classifications` computes a time-average classification. `moving_average` is a 1-D boxcar
  filter over an ordered series.

**Data Visualization** (parent — required by the subcategories below; HSSI previously held two of
its children with no parent, which this hierarchy does not permit)

- **Data Visualization: 2D Graphics** — `mcalf.visualisation.plot_map` and `plot_class_map` render
  2-D maps with `Axes.imshow`, symmetric diverging colour scaling for velocities, colourbars, and
  physical-extent axes.
- **Data Visualization: Line Plots** — `mcalf.visualisation.plot_ibis8542` (observed spectrum,
  fitted profile, separated absorption/emission components, line-core verticals, shaded sigma
  band), `plot_spectrum` (raw spectrum with the wavelength grid marked), and `plot_classifications`
  (line overlays per class).
- **Data Visualization: ML/AI** — `mcalf.visualisation.plot_classifications` plots
  spectra grouped by the label the classifier assigned; `plot_class_map` renders the classifier's
  output map; `bar` plots per-class abundance percentages. `mcalf.utils.plot.class_cmap` exists
  specifically to colour classifier output consistently across these. These display machine-learning
  model output, which is exactly what this subcategory covers.

**Models and Simulations** (parent — required by the subcategories below; as with Data
Visualization, HSSI previously held two of its children with no parent)

- **Models and Simulations: Forward-Fitting** — `mcalf.profiles.voigt` synthesises single and double
  Voigt profiles (`voigt_nobg`, `voigt`, `double_voigt_nobg`, `double_voigt`, with three
  interchangeable implementations: `voigt_faddeeva`, `voigt_integrate` including a C extension, and
  `voigt_mclean`); `ModelBase._curve_fit` optimises their parameters against the observation with
  `scipy.optimize.curve_fit` under per-parameter bounds, initial guesses and characteristic scales,
  and reports chi-squared. Synthetic model plus parameter optimisation is the definition of this
  subcategory.
- **Models and Simulations: ML/AI** — the classifier is not merely applied to data, it *selects the
  model to fit*: `IBIS8542Model._fit` maps classes 0–1 to a single absorption Voigt and classes 2–4
  to a double Voigt, and picks the sigma weighting profile from the class. The ML output determines
  the model form.

**Considered and rejected**, so a later refresh does not re-litigate them:

- *Coordinate Transforms* (any child) — MCALF performs no coordinate-system or reference-frame
  conversion. A search of `src/` for `helioprojective`, `Carrington`, `Stonyhurst`,
  `heliographic`, `coordinate` and `wcs` returns nothing. The wavelength-to-km/s Doppler
  conversion in `FitResult.velocity` is a unit calculation, not a frame transform.
- *Data Processing and Analysis: Calibration* — `ModelBase._set_prefilter` divides spectra by a
  prefilter response, which is an instrumental correction. Rejected because the code carries a
  `PendingDeprecationWarning` reading "Spectra should be fully processed before loading into MCALF.
  Prefilter response correction code may be removed in a later release", and the v0.2.0 release
  notes state the feature was deprecated "in favor of processing outside of the package". MCALF
  directs users to calibrate before loading; claiming Calibration would overstate it.
- *Data Processing and Analysis: Data Access and Retrieval* — MCALF ships no download or archive
  client. The gallery script `examples/gallery/models/plot_ibis8542data.py` fetches sample files
  with `requests` from a raw GitHub URL, but that is example code, not package functionality, and
  `requests` is not even a declared dependency (the example warns the user to install it).
- *Data Processing and Analysis: File Format Conversion* — `mcalf.utils.misc.merge_results` reads
  FITS and writes FITS (same format), and `load_parameter` reads several formats into arrays.
  Neither is conversion between formats as a user-facing purpose.
- *Data Processing and Analysis: Image Processing* — considered as an addition and rejected. The
  subcategory's defining techniques are feature detection, deconvolution and `scikit-image`-style
  content processing, none of which MCALF implements. What MCALF does have is scientific processing
  of 2-D spatial arrays: `smooth_cube`'s `scipy.ndimage.convolve` with neighbour-count
  renormalisation at mask boundaries, `mcalf.utils.mask.genmask` / `radial_distances` circular
  field-of-view mask construction, and `plot_map`'s `umbra_mask` contouring. Two of those three are
  already the primary evidence for values that *are* listed — the convolution for `Data Reduction`,
  the `umbra_mask` contouring for the `Data Visualization` family — so adding this value would
  double-count them under a heading whose defining techniques are absent.
- *Data Processing and Analysis: Wavelet Analysis* / *Energy Spectra* — no wavelet transform and no
  particle-energy-channel handling exist anywhere in the source.
- *Models and Simulations: Physics-Based* / *First Principles* / *Theory* — the Voigt profile is
  physically motivated (Gaussian thermal broadening convolved with a Lorentzian), but MCALF solves
  no radiative transfer and infers no atmospheric parameters from physics; it fits an analytic
  profile shape. Forward-Fitting captures this precisely and these would dilute it.
- *Models and Simulations: Observatory/Instrument Models* — MCALF models the spectral line, not the
  instrument. The instrument-specific content is the default line core, bounds and sigma profiles of
  `IBIS8542Model`, which is parameterisation rather than an instrument model.
- *Servers and Environments: High Performance Computing* — `ModelBase.fit(n_pools=...)` distributes
  spectra across `pathos.multiprocessing.ProcessPool` workers and README states the package "scales
  very well across many processor cores". Rejected because this category sits under "Infrastructure,
  deployment, and runtime environment software": shared-memory multiprocessing inside a science
  library is not HPC infrastructure, and there is no MPI, scheduler integration, container or
  cluster tooling in the repository.
- *Mission-related* (any child) — MCALF is not part of any mission ground system or data pipeline.

**Caveat recorded for `Data Processing and Analysis: Spectrogram`.** This value is retained as a
submitted value, but its evidence is weak and the reason it stays is representational rather than
technical: nothing else in the value set conveys that MCALF handles spectra. In this taxonomy
"Spectrogram" means a time-frequency representation (FFT, STFT, wavelet). A repository-wide search of
`src/`, `docs/`, `examples/` and `paper/` for `fft`, `wavelet`, `spectrogram`, `stft`, `periodogram`
and `power spectr` returns **no matches**. MCALF works with *spectra* (intensity versus wavelength),
which is a different thing. Widening that search to the whole tree returns only `libfftw3-dev`, a
system package listed twice in `azure-pipelines.yml` among the libraries installed in the wheel-build
environment; nothing in the package uses FFTW, and the compiled extension (`cextern/voigt.c`,
`cextern/voigt_nt.c`) evaluates the Voigt integrand rather than any transform. Do not read that
build-time entry as evidence of time-frequency analysis.

The likely origin of the value is that the vocabulary offers no category for spectral-line profile
fitting — its nearest neighbours are `Energy Spectra` (particle energy channels, not applicable) and
`Spectrogram` — so a curator representing "this software processes spectra" had little else to pick.
The case for removal rested only on the taxonomy's definition being narrower than that curatorial
use, which is not enough to overturn a submitted value that is carrying real representational weight.
This caveat is recorded so the removal is not re-litigated from the negative search result alone.

### 5. Related Region (MANDATORY)

- **Solar Environment** — the broad region. `README.rst`: the package is
  "intended to be used by solar physicists trying to extract line-of-sight (LOS) Doppler velocity
  information from spectral imaging observations (Stokes I measurements) of the Sun". GitHub topics
  include `solar`, `solar-physics`, `sun`; `setup.cfg` classifiers include
  `Topic :: Scientific/Engineering :: Astronomy`.
- **Chromosphere** — the vocabulary offers 24 regions and the guidance is to prefer the
  most specific applicable one. The science is explicitly chromospheric: `paper/paper.md` opens
  "Weak chromospheric absorption lines, due to dynamic events in the solar atmosphere, often consist
  of multiple spectral components"; the reference paper's abstract benchmarks the code on
  "two-component atmospheric profiles that are commonly present in sunspot chromospheres". The
  shipped `IBIS8542Model` targets the Ca II 8542 Å line, a standard chromospheric diagnostic, with a
  default `stationary_line_core` of 8542.099145376844 Å.

**Considered and rejected:**

- *Photosphere* — the far wings of Ca II 8542 Å sample photospheric heights, but neither the
  repository nor either publication frames MCALF as a photospheric tool, and the fitted quantities
  are the chromospheric line-core components. Adding it would not be supported by the sources.
- *Solar Interior* — the reference paper connects umbral flash profile evolution to the p-mode wave
  spectrum, but MCALF does no helioseismic analysis and supports no interior science functionality.
- *Corona* — see Field 22; the science is explicitly the *lower* solar atmosphere.

### 6. Authors (MANDATORY)

Reconciled by union across the live HSSI record, `CITATION.cff`, `.zenodo.json`, the DataCite records
for both the concept and v1.0.0 DOIs, `setup.cfg`, `paper/paper.md`, and both authors' ORCID records.
No one is dropped. Every source that names more than one author names these same two; the
differences between sources are in name form, affiliation completeness, and order. The exception is
`setup.cfg`, which carries a single packaging `author` field (`Conor MacBride`) and so names only
the lead author — that is a limitation of the field, not evidence of a one-author work.

#### Author 1: Conor D. MacBride
- **Author Identifier:** https://orcid.org/0000-0002-9901-8723
- **Affiliation 1:**
  - **Organization:** Astrophysics Research Centre, School of Mathematics and Physics, Queen's University Belfast
  - **Affiliation Identifier:** https://ror.org/00hswnk62

#### Author 2: David B. Jess
- **Author Identifier:** https://orcid.org/0000-0002-9155-8039
- **Affiliation 1:**
  - **Organization:** Astrophysics Research Centre, School of Mathematics and Physics, Queen's University Belfast
  - **Affiliation Identifier:** https://ror.org/00hswnk62
- **Affiliation 2:**
  - **Organization:** Department of Physics and Astronomy, California State University, Northridge
  - **Affiliation Identifier:** https://ror.org/005f5hv41

**Author identity and ORCIDs.** Both ORCIDs are confirmed against the ORCID public API, and the
same two identifiers appear in `CITATION.cff`, `.zenodo.json`, `paper/paper.md` and both DataCite
records. The string form differs between sources — `.zenodo.json` and `paper/paper.md` carry the
bare `0000-0002-…` identifier while `CITATION.cff` and DataCite carry the full
`https://orcid.org/` URL — so compare the identifier rather than the literal string. These ORCIDs
are the reliable identity keys for these two people and should be used for matching.

**Affiliation ROR.** The stored HSSI organisation row for both authors is
`Astrophysics Research Centre, School of Mathematics and Physics, Queen's University Belfast` with an
**empty identifier**. The Queen's University Belfast ROR is `https://ror.org/00hswnk62`, confirmed
two independent ways: the ROR record for that identifier is unambiguously this institution
(Belfast, Northern Ireland, United Kingdom, acronym QUB, `qub.ac.uk`), and David Jess's own ORCID
employment record carries the same ROR. Note when reading that ORCID record that it holds *two* Queen's University Belfast employment
entries — one with the ROR but "Unknown City" and no department, and one with the correct department
("Astrophysics Research Centre"), role ("Professor") and city (Belfast) but a RINGGOLD identifier
(1596) rather than a ROR. The ROR from the first and the department from the second are both
correct; neither entry alone is complete.

The organisation name recorded above deliberately matches the existing HSSI row rather than the
longer DataCite/Zenodo string
`Astrophysics Research Centre, School of Mathematics and Physics, Queen's University Belfast, Belfast, BT7 1NN, UK`.
The postal address is not part of the organisation's name, and the shorter form is what is already
stored.

**Durable platform limitation — the Queen's University Belfast ROR cannot be attached in place.**
The organisation record HSSI holds for that affiliation has **no identifier**, and the routine
metadata-update path cannot backfill one: an affiliation can only be *added* to a person, never
replaced or removed, and an existing organisation record's blank identifier is never filled in.
Submitting the same organisation name carrying the ROR would therefore create a *second* organisation
record and leave both authors permanently holding two entries for the one institution, with no way to
remove the duplicate. The ROR is recorded here as the correct value while HSSI continues to store the
identifierless form; closing that gap requires a database-level correction rather than a metadata
update, and a future refresh should not read the divergence as an unextracted difference.

**Why the ROR was deliberately left out, and what would justify putting it in.** Omitting it was a
judgement that a permanent duplicate organisation record is worse than an identifierless one, not a
judgement that the ROR is wrong or unwanted — `https://ror.org/00hswnk62` is correct and belongs on
this affiliation. The omission is therefore provisional and should be revisited, not treated as
settled against the ROR. Two developments would each justify reversing it: a database-level
correction that backfills the identifier on the existing organisation record, which is the clean fix
and leaves nothing to undo; or a change to the update path that either backfills a blank identifier
on an organisation match or allows an affiliation to be replaced or removed, at which point the ROR
could be submitted through the normal metadata route. Until one of those exists, the cost of adding
it is borne permanently by every person record pointing at that organisation — which is why the
decision was to wait rather than to accept the duplicate. Anyone reopening this should confirm the
stored organisation record still has a blank identifier before acting, since a correction may
already have landed.

**MacBride's authoritative given name is `Conor D.`; HSSI stores the bare `Conor`.** `Conor D.` is
what every citation-bearing source in and around the repository uses: `CITATION.cff`
(`given-names: "Conor D."`), `.zenodo.json` (`"name": "Conor D. MacBride"`), the DataCite records for
both DOIs (`"givenName": "Conor D."`), and the JOSS paper byline. `CITATION.cff` is the author's own
instruction for how to cite this software, which makes it the authoritative attribution form. The
counter-evidence is his ORCID public record, whose `given-names` field is the bare `Conor` with no
credit name — but an ORCID personal-name field is an identity record, not a publication byline, and
it is common for it to omit a middle initial. `setup.cfg` also uses the bare `Conor MacBride` as the
package author, and the LICENSE copyright line reads "Copyright (c) 2020 Conor MacBride".

**Durable upstream limitation — this correction cannot be applied through the routine update path.**
HSSI matches an author by ORCID and then fills only a *blank* stored name, so a differing given name
is accepted and silently discarded: the stored `Conor` survives unchanged and the request reports
success. The person record is also a shared row that other software entries may cite, so a
database-level correction would change their attribution too and must be checked against those other
references first. `Conor D.` is therefore recorded here as the authoritative value while HSSI
continues to store `Conor`; treat that divergence as known rather than as an unextracted
difference.

**Author order: MacBride first, Jess second.** Every authoritative source lists MacBride first:
`CITATION.cff`, `.zenodo.json`, both DataCite records, `paper/paper.md`, the JOSS citation in
`README.rst`, and the reference paper. MacBride is the lead author, the repository owner, the PyPI
`author`, and the LICENSE copyright holder. The order recorded above follows the sources and reverses
the Jess-first order HSSI originally held.

Author order is meaningful in HSSI rather than incidental: the author relation is a *sorted*
association whose stored order is the order the record presents, and an update rewrites that order
wholesale from the list it is given. Reordering therefore requires resending the complete author
list, and a refresh that sent a partial list would silently drop whoever was omitted.

**Jess's second affiliation.** `paper/paper.md` assigns Jess affiliations
"1, 2", where 2 is "Department of Physics and Astronomy, California State University Northridge,
Northridge, CA 91330, U.S.A." This is the software's own peer-reviewed reference publication, which
is primary evidence. The ROR `https://ror.org/005f5hv41` is confirmed via the ROR API (California
State University, Northridge; acronym CSUN; Northridge, California, United States). Zenodo and
DataCite list only the Queen's University Belfast affiliation for Jess because `.zenodo.json` records
a single affiliation string per creator — that is a limitation of the Zenodo deposition file, not
evidence that the second affiliation does not exist. The organisation name above drops the postal
detail and uses the ROR display form's comma placement
("California State University, Northridge").

**No further authors exist.** The repository has no `AUTHORS`, `CONTRIBUTORS` or `CHANGELOG` file
(release notes live on the GitHub releases, which is why Field 12's version description is drawn from
there). The full git history has exactly one committer, `Conor MacBride <conor@macbride.me>`, and
every pull request credited in the v1.0.0 release notes is attributed to `@ConorMacBride`. David Jess
appears as an author in every citation source but not in the commit log, which is normal for a
supervising co-author. The two-author list is complete.

### 7. Software Name (MANDATORY)
- **Name:** MCALF: Multi-Component Atmospheric Line Fitting

The same string appears in the live record, `CITATION.cff` (`title:`), `.zenodo.json` (`title:`),
both DataCite records (`titles[].title`), the JOSS paper title, the `README.rst` heading, and the
GitHub repository description. Retained unchanged.

One source needs care: `setup.cfg` sets
`description = "MCALF: Multi-Component Atmospheric Line Fitting"` with *literal* double quotes
inside the value, and PyPI consequently shows the summary wrapped in quote characters. Anything
extracting the name from packaging metadata must strip them; the unquoted form above is correct.

The short form **MCALF** is what the PyHC community registry (`name: "MCALF"`), the PyPI and
conda-forge distribution name (`mcalf`), the import name, and `docs/conf.py` (`project = 'MCALF'`)
use. HSSI's Field 7 is a single text field with no separate short-name slot, so the full expanded
name is correct here and the short form is noted only as context.

### 8. Description (MANDATORY)

MCALF is an open-source Python package for accurately constraining velocity information from spectral imaging observations using machine learning techniques.

This software package is intended to be used by solar physicists trying to extract line-of-sight (LOS) Doppler velocity information from spectral imaging observations (Stokes I measurements) of the Sun. A ‘toolkit’ is provided that can be used to define a spectral model optimised for a particular dataset.

This package is particularly suited for extracting velocity information from spectral imaging observations where the individual spectra can contain multiple spectral components. Such multiple components are typically present when active solar phenomenon occur within an isolated region of the solar disk. Spectra within such a region will often have a large emission component superimposed on top of the underlying absorption spectral profile from the quiescent solar atmosphere.

A sample model is provided for an IBIS Ca II 8542 Å spectral imaging sunspot dataset. This dataset typically contains spectra with multiple atmospheric components and this package supports the isolation of the individual components such that velocity information can be constrained for each component. Using this sample model, as well as the separate base (template) model it is built upon, a custom model can easily be built for a specific dataset.

The custom model can be designed to take into account the spectral shape of each particular spectrum in the dataset. By training a neural network classifier using a sample of spectra from the dataset labelled with their spectral shapes, the spectral shape of any spectrum in the dataset can be found. The fitting algorithm can then be adjusted for each spectrum based on the particular spectral shape the neural network assigned it.

This package is designed to run in parallel over large data cubes, as well as in serial. As each spectrum is processed in isolation, this package scales very well across many processor cores.

The six paragraphs above, blank-line separated, are the value of this field. They are the authors'
own introduction to the software, taken from `README.rst` at the pinned revision.

**This supersedes the shorter Zenodo abstract that was previously stored** — the text carried in
`.zenodo.json`, where it is stored as HTML (`<p>` tags, `&lsquo;`, `&Aring;`), and rendered as the
plain text below in the DataCite records for both the concept and v1.0.0 DOIs:

> MCALF is an open-source Python package for accurately constraining velocity information from
> spectral imaging observations using machine learning techniques. This software package provides a
> ‘toolkit’ that can be used to define a spectral model optimised for a particular dataset. A sample
> model is provided for an IBIS Ca II 8542 Å spectral imaging sunspot dataset. This dataset typically
> contains spectra with multiple atmospheric components and this package supports the isolation of
> the individual components such that velocity information can be constrained for each component.
> Using this sample model, as well as the separate base (template) model it is built upon, a custom
> model can easily be built for a specific dataset.

That abstract is accurate and self-contained, and it was not wrong; it is simply less complete. Both
texts are the authors' own words, so this is not a curator's rewrite of an authorial voice. The
longer text is preferred because Field 8 asks for enough detail for a reader to judge whether the
software fits their work, and the abstract omits four things the README states: the intended audience
and measurement ("solar physicists trying to extract line-of-sight (LOS) Doppler velocity information
from spectral imaging observations (Stokes I measurements) of the Sun"); why multiple components
arise; how the neural network classifier is trained on labelled sample spectra and then used to
adjust the fit for each spectrum; and that the package runs in parallel over large data cubes as well
as in serial, scaling across many processor cores.

Two sentences that close the same README section are deliberately not carried over: one contains an
uncorrected typo in the source ("Numerous functions are provided to plot the results in a clearly")
and the other concerns reuse of the MCALF API by other Python packages rather than what the software
does for its own users.

Note the typographic characters the text contains — the curly quotes around ‘toolkit’ and the Å —
which come from the source and must survive any round-trip.

### 9. Concise Description (OPTIONAL)

MCALF is an open-source Python package for accurately constraining velocity information from spectral imaging observations using machine learning techniques.

157 characters, within the 200-character limit. This is the first sentence of the description and the
opening sentence of `README.rst`, `docs/index.rst`, and the JOSS paper's Statement of Need. Retained
unchanged.

### 10. Publication Date (RECOMMENDED)
- **Date:** 2020-05-23

**This corrects the previously stored 2020-05-22**, which is the GitHub repository `created_at`
timestamp (2020-05-22T18:31:33Z) — the value HSSI's autofill cascade produces via SoMEF's
`date_created`. Repository creation is a different event from publication, so it does not answer what
Field 10 asks: the date of first publication of the initial version.

Three candidate dates exist:

| Date | What it actually is |
|---|---|
| 2020-05-22 | GitHub repository creation (previously stored, superseded) |
| 2020-05-23 | Zenodo `publication_date` for v0.1, and the `v0.1` git tag date |
| 2020-06-30 | GitHub release v0.1 `published_at`, and Zenodo record 3924528 creation |

2020-05-23 is the best supported: it is the date Zenodo itself assigns to the first published
version, it is therefore the authors' own declared publication date, and it independently matches the
`v0.1` git tag. 2020-06-30 is when the GitHub–Zenodo integration was first run rather than when v0.1
was cut — the GitHub release object records `created_at` 2020-05-23 and `published_at` 2020-06-30, so
that release was backfilled. The change from the stored value is only one day, and all three dates
fall inside the initial-release window, so nothing downstream turns on it; the correction is made
because 2020-05-23 names the right event and 2020-05-22 names the wrong one.

### 11. Publisher (RECOMMENDED)
- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Retained unchanged. DataCite reports `publisher: "Zenodo"` for both the concept and v1.0.0 records,
and the DOIs were minted through the GitHub–Zenodo integration, which is exactly the case Field 11
describes. Field 11 prefers a ROR when one exists; Zenodo is a CERN-operated service without its own
ROR, so the service URL — explicitly permitted by the field — is correct.

### 12. Version (RECOMMENDED)

- **Version Number:** v1.0.0
- **Version Date:** 2023-03-28
- **Version Description:** Breaking change: the default Voigt implementation is now `voigt_faddeeva` (pass `impl=mcalf.profiles.voigt.voigt_integrate` to restore the previous behaviour). New: the Voigt implementation is selectable, pure Python wheels are published, and supported Python versions are updated to 3.8–3.11. Documentation updated.
- **Version PID:** https://doi.org/10.5281/zenodo.7779553

v1.0.0 is confirmed as the current and latest release. The `v1.0.0` git tag points at the pinned
HEAD `8f2a3dfb6c7c4e99341371bcfed6f89ed6843964`; the repository has six tags (v0.1, v0.1.1, v0.2.0,
v0.2.1, v0.3.0, v1.0.0) and no newer one; PyPI's latest release is 1.0.0; and DataCite reports
`version: "v1.0.0"` for the concept DOI. The leading `v` is part of the version string as the
authors publish it (git tag, GitHub release, Zenodo `version`, DataCite `version`), so it is kept.

**Version Date.** 2023-03-28 is corroborated three ways: Zenodo record 7779553
`publication_date: "2023-03-28"`, the GitHub release `published_at` 2023-03-28T22:20:13Z, and
DataCite's `Issued` date 2023-03-28. Do **not** substitute the tagged commit date 2023-03-17 — that
is when the code was merged, not when the version was released.

**Version PID.** 10.5281/zenodo.7779553 is the version-specific DOI, confirmed by DataCite's
`IsVersionOf → 10.5281/zenodo.3924527` relation on that record and by the concept record's matching
`HasVersion` entry. The version DOIs for the full history, should a later refresh need them, are
v0.3.0 → 10.5281/zenodo.5803548, v0.2.1 → 10.5281/zenodo.4767888, v0.2.0 → 10.5281/zenodo.4689589,
v0.1.1 → 10.5281/zenodo.4265382, v0.1 → 10.5281/zenodo.3924528.

**Version Description** is condensed from the authors' own GitHub release notes for v1.0.0 (sections
"Breaking changes", "New features", "Documentation"), preserving the actionable migration
instruction. The pull-request links and the CI-only entry were left out as noise for this field.

**Do not use `CITATION.cff` as a version source.** Its `version: 0.2.1` and
`date-released: 2021-05-17` were never updated past v0.2.1, leaving them two releases behind
(v0.3.0 and v1.0.0 both followed). The file remains authoritative for authorship and the preferred
citation, but a refresh that trusted its version fields would silently regress this record. Use the
git tag, GitHub release, PyPI, Zenodo or DataCite instead. All five agree the current version number
is v1.0.0; the GitHub release, PyPI, Zenodo and DataCite further agree the release date is
2023-03-28, while the git tag carries only its 2023-03-17 commit date, which is the merge date and
not a release date (see Version Date above).

**Storage-form caution for a future refresh.** The HSSI view API renders this field as
`<software name> - <version number>`, so the entry reads back as
`MCALF: Multi-Component Atmospheric Line Fitting - v1.0.0`. The stored value is the bare `v1.0.0`
recorded above. Copying the rendered string into an update would corrupt the record.

### 13. Programming Language (RECOMMENDED)
- **Python 3.x**
- **C**

Retained unchanged; both values exist in the live vocabulary. Python is the implementation language
of the entire package. C is not incidental: `cextern/voigt.c` and `cextern/voigt_nt.c` are compiled
into `ext_voigtlib` and loaded through `ctypes` in `mcalf/profiles/voigt.py` to accelerate the
integrated Voigt evaluation, with a pure-Python fallback when the extension is absent
(`CLIB_INSTALLED`). `setup.cfg` declares `Programming Language :: C` alongside the Python
classifiers, and `[bdist_wheel] py_limited_api = cp38` targets the stable C ABI.

Supported Python versions are 3.8–3.11 per the `setup.cfg` classifiers, the tox envlist, and the
Azure Pipelines matrix. `python_requires = >=3.7` in `setup.cfg` is stale relative to those
classifiers; either way `Python 3.x` is the correct vocabulary value.

**Considered and rejected — IDL.** `examples/example1/FittingIBIS.pro` (mirrored under
`docs/guide/examples/`) is an IDL script that drives MCALF through the IDL–Python bridge. It is not
part of the package: `MANIFEST.in` contains `prune examples`, so it is not distributed, and its own
`README.rst` states "It is not recommended to use the IDL wrapper in production... IDL is not fully
supported in the current version of the code". Listing IDL would misrepresent what the software is
written in.

### 14. Reference Publication (RECOMMENDED)
- **DOI:** https://doi.org/10.21105/joss.03265

MacBride, C. D., & Jess, D. B. (2021). MCALF: Multi-Component Atmospheric Line Fitting.
*Journal of Open Source Software*, 6(61), 3265.

Retained unchanged. This is the JOSS paper describing the software itself; its source is in the
repository at `paper/paper.md` with `paper/paper.bib` and `paper/figure.pdf`. `CITATION.cff`
nominates it as the `preferred-citation`, and `README.rst` lists it first under "Citation". It is
the correct Field 14 value — the paper *about the software* — as distinct from the reference paper
about the method, which is in Field 27.

### 15. License (RECOMMENDED)
- **License:** BSD 2-Clause "Simplified" License
- **License URI:** https://opensource.org/licenses/BSD-2-Clause
- **SPDX identifier:** BSD-2-Clause

Retained unchanged; the value matches the live `License` vocabulary row exactly, including the
straight double quotes around "Simplified". `LICENSE.rst` contains the plain two-clause BSD text
("Copyright (c) 2020 Conor MacBride"); `setup.cfg` declares `license = BSD 2-Clause`; GitHub's
licence detection reports `spdx_id: BSD-2-Clause`; and DataCite's `rightsList` gives
`BSD 2-Clause "Simplified" License` with `rightsIdentifier: bsd-2-clause` and the SPDX scheme URI.

**Do not "correct" this from Zenodo.** The Zenodo record for v1.0.0 reports
`license: {"id": "bsd-2-clause-netbsd"}` — the NetBSD variant, which is a *different* SPDX licence
and is not what `LICENSE.rst` contains. This is an error in Zenodo's own record, and because HSSI's
DOI autofill copies Zenodo values through verbatim, it is the kind of value that gets reintroduced
by a naive refresh. The repository's licence file, GitHub's detection and DataCite all agree on
plain BSD-2-Clause; that is authoritative.

---

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

Retained from the live record (stored lower case; the view renders them Title Case):

- 2d graphics
- absorption
- astronomy
- data analysis
- emission
- fitting
- line plots
- local
- machine learning
- plotting
- python
- solar
- solar physics
- spectra
- sun
- voigt

Each of these already exists as a `Keyword` row and each traces to a source: `absorption`,
`emission`, `fitting`, `spectra`, `voigt` are the `setup.cfg` / JOSS `tags` keywords; `astronomy`,
`python`, `solar`, `sun` are GitHub topics (with `solar-physics` normalised to `solar physics`);
`2d graphics`, `data analysis`, `line plots`, `local`, `machine learning`, `plotting` come from the
PyHC community registry entry.

**Also recorded**, each with its own evidence. Two reuse an existing `Keyword` row
(`chromosphere`, `doppler velocity`); the other three create new ones:

- **chromosphere** *(existing row)* — the reference paper's abstract benchmarks the code on profiles
  "commonly present in sunspot chromospheres"; `paper/paper.md` opens with "Weak chromospheric
  absorption lines". Mirrors the Field 5 region.
- **doppler velocity** *(existing row)* — the package's primary output. `FitResult.velocity` and
  `FitResults.velocities` return km/s; `FitResults.save` writes `VLOSA`/`VLOSQ` HDUs with
  `UNIT: 'KM/S'`; `plot_map` labels its colourbar "Doppler velocity".
- **umbral flashes** *(new row)* — the phenomenon MCALF was built to measure, per the reference
  paper. Field 22's controlled vocabulary has no row for it, and Field 22's own guidance directs a
  supported phenomenon with no row to Keywords. Keywords is therefore where the phenomenon MCALF
  was built to measure becomes searchable, since no controlled vocabulary in this form can express
  it.
- **sunspots** *(new row)* — `README.rst` and the Zenodo description both describe the shipped model
  as being for an "IBIS Ca II 8542 Å spectral imaging **sunspot** dataset"; `plot_map` takes an
  `umbra_mask` argument specifically to outline a sunspot umbra.
- **spectral imaging** *(new row)* — the defining phrase of the software's own description, name and
  README.

**Considered and not added:** `spectrum` (near-duplicate of the stored `spectra`); `fits` (a PyHC
keyword, but the format already has its own representation in Fields 18/19, and Field 16 asks for
science keywords "not supported by other metadata fields"); `specific` (a PyHC registry token with
no standalone meaning); `multidimensional` (a PyHC keyword and an existing row, but it describes
array shape rather than science); `neural network` (subsumed by the stored `machine learning`).

### 17. Data Sources (OPTIONAL)
- **Observatory/Mission-specific**

Retained unchanged. MCALF ships `mcalf.models.IBIS8542Model`, a model class specialised to
Interferometric BIdimensional Spectrometer Ca II 8542 Å observations, with instrument-specific
defaults (line core 8542.099145376844 Å, absorption/emission bounds, sigma weighting profiles) and a
prefilter-response correction path for that instrument's data. Field 17's instruction is to select
`observatory-specific` and name the observatory in Field 32, which this record does.

**Considered and rejected — `HTTP/HTTPS Directories`.** The gallery example downloads its sample
files over HTTPS from raw.githubusercontent.com, but that is example code using `requests`, which is
not a declared dependency. MCALF exposes no data-retrieval interface, so it supports no remote data
source.

### 18. Input File Formats (RECOMMENDED)
- **FITS**
- **IDL.sav**
- **csv**
- **ascii**

**FITS** — `mcalf.utils.misc.load_parameter` reads `.fits`, `.fit` and `.fts` via
`astropy.io.fits`; `mcalf.utils.misc.merge_results` opens FITS result files for merging; the
documented workflow loads spectra with `fits.open(...)[0].data` into `ModelBase.load_array`, and the
gallery example loads `spectra.fits`.

**IDL.sav** — `load_parameter` handles the `.sav` extension through
`scipy.io.readsav`. This is not incidental: `examples/example1/config.yml` sets
`original_wavelengths: "/path/to/wavelengths_original.sav"`, and `examples/example1/FittingIBIS.pro`
`RESTORE`s `wavelengths_original.sav`, `prefilter.sav`, `groundtruths.sav` and `background.sav`
before handing the arrays to MCALF. IDL SAVE input is a first-class, documented path for this
package's original IBIS user community.

**csv** — `load_parameter` reads `.csv` with `numpy.loadtxt(delimiter=',')`, including a
mode that substitutes the stationary line core into expressions. `examples/example1/config.yml`
points `prefilter_ref_main` and `prefilter_ref_wvscl` at `.csv` files, and the commented-out
`prefilter_response: "prefilter.csv"` line shows the third.

**ascii** — `load_parameter` treats `.txt` identically to `.csv`, and the bundled sample
dataset ships `examples/data/ibis8542data/wavelengths.txt`, loaded in the gallery example with
`np.loadtxt('wavelengths.txt', dtype='>f4')`.

**Documented omissions — real input formats with no vocabulary row.** Two supported input formats
have no row in the 11-value `FileFormat` vocabulary (ascii, CDF, csv, FITS, HDF5, IDL.sav,
ISTP-Compliant, JSON, netCDF3/4, Other, Zarr), and are therefore not representable:

- **YAML.** `ModelBase` and `IBIS8542Model` accept a `config=` argument naming a `.yml` file parsed
  with `yaml.load`; `pyyaml>=5.1` is a hard dependency and `examples/example1/config.yml` is a
  documented worked example. There is no YAML row.
- **NumPy `.npy` / `.npz`.** `load_parameter` loads both via `numpy.load`. There is no row for them.

`Other` was considered for these and rejected: as a search facet it conveys nothing, and recording
the specific evidence here is more useful to a future maintainer than an opaque token. This omission
is deliberate — do not treat these formats as an oversight.

**Considered and rejected — JSON.** `examples/data/ibis8542data/training_data.json` holds the
labelled training indices, but it is read by the *example script* with the Python standard library;
`load_parameter` does not accept `.json`, and no MCALF code path parses JSON. The format is not
supported by the software.

### 19. Output File Formats (RECOMMENDED)
- **FITS**
- **csv**

**FITS** — `mcalf.models.FitResults.save(filename, model=None)` writes a multi-HDU FITS
file with a primary header (`VERSION`, `NTIME`, `NROWS`, `NCOLS`, `TIME`, and `SLC` when a model is
supplied) plus `PARAMETERS`, `CLASSIFICATIONS`, `PROFILE`, `SUCCESS` and `CHI2` image HDUs, and,
when a model is given, `VLOSA` and `VLOSQ` velocity HDUs carrying `VTYPE` and `UNIT: 'KM/S'`.
`mcalf.utils.misc.merge_results` writes a merged FITS file from several such files.

**csv** — `ModelBase.test(X, y)` writes `<output>/neural_network/test.csv` with
`numpy.savetxt(..., delimiter=',', header='ground_truth, prediction')` whenever the model's `output`
attribute is set. The method's own docstring documents this: "If the model object has an output
parameter, it will create a CSV file (``output``/neural_network/test.csv) listing the predictions and
ground truth data."

Figure output (PNG and the rest) is not listed: MCALF's visualisation functions return matplotlib
artists and axes, leaving any file writing to the caller, so no image format is a MCALF output
format.

### 20. Operating System (RECOMMENDED)
- **Linux**
- **Mac**
- **Windows**
- **Operating System Independent**

Retained unchanged; all four exist in the live vocabulary. `setup.cfg` declares
`Operating System :: OS Independent` — note that the HSSI vocabulary value is the fully spelled-out
`Operating System Independent`, and the literal string `OS Independent` is not a valid value. The
three named platforms are all exercised in CI: `azure-pipelines.yml` runs the test matrix on
`linux` (py38–py311, plus `py38-oldestdeps`, `codestyle` and a `py311-figure` job) and on `windows`
(py38–py311 plus `py38-oldestdeps` and a figure job), and the release stage builds
`macosx_x86_64` and `macosx_arm64` wheels, all of which are test-imported before publication
(`test_command: pytest --pyargs mcalf`).

### 21. CPU Architecture (RECOMMENDED)
- **CPU Independent**
- **x86-64**
- **Apple Silicon arm64**

**CPU Independent** — v1.0.0 publishes a pure-Python wheel. PyPI carries
`mcalf-1.0.0-py3-none-any.whl`, built by the dedicated `ReleasePure` stage in `azure-pipelines.yml`
with `MCALF_NO_EXTENSIONS: "1"`. The code supports this directly: `mcalf/profiles/voigt.py` sets
`CLIB_INSTALLED = False` when the compiled library is absent and falls back to `scipy`-based
implementations.

**x86-64** — the compiled wheels for `macosx_x86_64`, `manylinux*_x86_64` and `win_amd64`
are all x86-64 (PyPI carries `mcalf-1.0.0-cp38-abi3-macosx_10_9_x86_64.whl`,
`...-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl` and
`...-win_amd64.whl`).

**Apple Silicon arm64** — `azure-pipelines.yml` lists `wheels_cp3{8,9,10,11}-macosx_arm64` among
its release targets, and PyPI carries the resulting artefact
`mcalf-1.0.0-cp38-abi3-macosx_11_0_arm64.whl`. The C extension is therefore built and published for
Apple Silicon. HSSI's earlier record listed only `CPU Independent` and `x86-64`, which understated
the platforms the compiled extension actually supports.

**Considered and rejected — `Linux aarch64 or arm64`.** The four compiled wheel targets in
`azure-pipelines.yml` are `macosx_x86_64`, `macosx_arm64`, `manylinux*_x86_64` and `win_amd64`. No
Linux ARM wheel is built or published, and none appears on PyPI. (`CIBW_MANYLINUX_I686_IMAGE` is set
in the variables block but no i686 target is requested.) A Linux ARM user would fall back to the
pure-Python wheel, which `CPU Independent` already covers.

### 22. Related Phenomena (OPTIONAL)
- **Solar Flares**

`Coronal Heating` was previously stored alongside it and has been removed; the correction is recorded
below. The field is thin, and the reason is structural rather than accidental: the `Phenomena`
vocabulary has exactly seven rows — Coronal Heating, Coronal Mass Ejections, Geomagnetic Storms,
Solar Corona, Solar Flares, Solar Wind, X-ray emission — and **none of them names what MCALF actually
studies**. The reference paper's science is umbral flashes, chromospheric wave dynamics and p-mode
coupling in sunspot umbrae; the JOSS paper's framing is "wave dynamics in the solar atmosphere"; the
theme issue the reference paper appears in is titled "High-resolution wave dynamics in the lower
solar atmosphere". There is no row for umbral flashes, chromospheric waves, sunspots or Doppler
velocities. That is why the field is thin, and why `umbral flashes` and `sunspots` are recorded as
Keywords in Field 16 instead — Field 22's own guidance routes unrepresentable phenomena there.

**`Solar Flares` is retained.** Its support is thin but non-zero: `paper/paper.md` cites the
"supervised hierarchical k-means" classifier of Panos et al. (2018), "which clusters solar flare
spectra based on their profile shape", as an example of an existing classifier MCALF's pluggable
classifier interface could accommodate. That is a stated potential application rather than a
demonstrated capability, and MCALF fits no flare data anywhere in the repository — but it is a
documented connection to the toolkit's design made in the authors' own paper, and it is the only
support any of the seven vocabulary rows has. Removing it as well would empty the field entirely,
which would represent MCALF's phenomenon coverage less accurately than a thinly supported value does.

**`Coronal Heating` was removed as a correction, not a preference.** No source in or around this
repository supports it. The repository never mentions the corona; the reference paper is explicitly
about the *lower* solar atmosphere and its abstract concerns "two-component atmospheric profiles that
are commonly present in sunspot chromospheres"; `paper/paper.md` concerns chromospheric absorption
lines. The extraction that first proposed the value justified it as "Spectral line profiles related
to atmospheric heating", which is an inference rather than evidence. One thread points the other way
and is recorded here so it is not mistaken for new support later: the observing campaign that
produced the reference paper's data was titled "Nanoflare Activity in the Lower Solar Atmosphere"
(NSO-SP proposal T1020, PI D. B. Jess), and nanoflare heating is a coronal-heating mechanism. Even
so, that campaign title still places the science in the lower atmosphere, and MCALF neither models
nor measures coronal heating.

### 23. Development Status (RECOMMENDED)
- **Inactive**

`Inactive` is the repostatus.org term for a project that "has reached a stable, usable state but is no longer being actively developed;
support/maintenance will be provided as time allows", and that is what the evidence shows as of
2026-08-07:

- The last commit on `main` is the pinned HEAD, dated 2023-03-17; the last push was 2023-03-28 (the
  v1.0.0 tag). More than three years have passed with no further commits.
- v1.0.0 is a deliberate stable release with a documented breaking change and a migration path — the
  project reached a stable, usable state rather than stalling before one.
- The repository is **not** archived and issues remain enabled with zero open issues, so `Abandoned`
  and `Unsupported` overstate the situation; there is no statement that the authors have ceased work
  or want a new maintainer.
- The PyHC community registry rates MCALF "Good" on all six axes (community, documentation, testing,
  software maturity, Python 3, licence), which is consistent with a finished, well-kept package.

**Correcting a previous value in this dossier.** An earlier extraction recorded `Active` on the
strength of a "last update 2024-12-04" date. That date is GitHub's `updated_at` field, which changes
on repository-metadata touches (stars, description, topics) and is *not* commit activity; the
repository's `pushed_at` is 2023-03-28. `Active` requires the project to be "being actively
developed", which is not the case. Do not re-derive this field from `updated_at`.

### 24. Documentation (RECOMMENDED)
- **URL:** https://mcalf.macbride.me/

Retained unchanged. This is the canonical documentation URL: `setup.cfg` declares it under
`project_urls`, `README.rst` links to it ("Documentation is available here"), the GitHub repository
`homepage` field is `https://mcalf.macbride.me`, and the JOSS paper directs readers there. The Read
the Docs default host `https://mcalf.readthedocs.io/` serves the same content and the docs badge
targets the custom domain; the custom domain is the authors' preferred address and is the right value
to store.

### 25. Funder (OPTIONAL)

The funding is named in the repository's own JOSS paper source, `paper/paper.md`, whose
Acknowledgements section is corroborated by the reference paper's funding statement. Organisation
names are given in full (no acronyms) with RORs confirmed against the ROR API.

1. **Organization:** Department for the Economy
   **Funder Identifier:** https://ror.org/0161w0r98
   `paper/paper.md`: "CDM would like to thank the Northern Ireland Department for the Economy for the
   award of a PhD studentship." The reference paper phrases it "The Department for the Economy
   (Northern Ireland) through their postgraduate research studentship". The ROR record confirms the
   Northern Ireland department (Belfast, country subdivision NIR, types `funder` and `government`,
   website economy-ni.gov.uk, formerly the Department of Enterprise, Trade and Investment). The
   recorded name is the ROR display form; the sources write it as "Northern Ireland Department for
   the Economy", which is the same body — the ROR is the unambiguous identifier.

2. **Organization:** Invest Northern Ireland
   **Funder Identifier:** https://ror.org/00qnrsq87
   `paper/paper.md`: "DBJ wishes to thank Invest NI and Randox Laboratories Ltd. for the award of a
   Research and Development Grant (059RDEN-1) that allowed the computational techniques employed to
   be developed." "Invest NI" is an alias on the ROR record; the expanded form is used here per the
   field's instruction to avoid acronyms. Of the three awards recorded in Field 26, this is the one
   tied most directly to the software, since it explicitly funded development of the computational
   techniques.

3. **Organization:** Randox Laboratories Ltd.
   **Funder Identifier:** https://ror.org/04cte7x29
   Co-awarder of grant 059RDEN-1 with Invest Northern Ireland, per the same sentence, and named as
   such in the reference paper too. The ROR display name is the disambiguated "Randox (United
   Kingdom)"; the full company name used by both papers is recorded here as the organisation name,
   with the ROR carrying the identity. The ROR record confirms the company (Crumlin, Northern
   Ireland; its Wikipedia link is the Randox Laboratories article).

4. **Organization:** Science and Technology Facilities Council
   **Funder Identifier:** https://ror.org/057g20z61
   `paper/paper.md`: "DBJ would also like to thank the UK Science and Technology Facilities Council
   (STFC) for the consolidated grant ST/T00021X/1." The ROR record confirms the UK research council
   (types `funder` and `government`, now part of UK Research and Innovation).

**Considered and rejected — the Research Council of Norway and the Royal Society.** Both appear in
`paper/paper.md`: "The authors wish to acknowledge scientific discussions with the Waves in the Lower
Solar Atmosphere (WaLSA; www.WaLSA.team) team, which is supported by the Research Council of Norway
(project no. 262622) and the Royal Society (award no. Hooke18b/SCTM)." Neither funded MCALF. They
fund the WaLSA team, which is thanked for *scientific discussions*, and the reference paper makes the
Royal Society's role even more explicit: it funded a Theo Murphy Discussion Meeting. Recording them
as funders of this software would be wrong; recorded here so the distinction does not have to be
re-derived.

DataCite's `fundingReferences` array is **empty** for both the concept and v1.0.0 DOIs, and
`.zenodo.json` has no grants block, so none of this funding is discoverable through the DOI autofill
cascade. It exists only in the papers.

### 26. Award Title (OPTIONAL)

All three titles are well under the 128-character limit that applies to award names — a limit that
is enforced at storage but not reported by validation, so an over-long title fails late rather than
being rejected up front.

1. **Award Title:** Research and Development Grant
   **Award Number:** 059RDEN-1
   Awarded by Invest Northern Ireland and Randox Laboratories Ltd. `paper/paper.md` states it
   "allowed the computational techniques employed to be developed", making it the award most directly
   tied to this software. The award number appears verbatim in the reference paper's funding
   statement ("an Invest NI and Randox Laboratories Ltd. Research & Development (grant no.
   059RDEN-1)"); `paper/paper.md` gives it as "(059RDEN-1)".

2. **Award Title:** Consolidated Grant
   **Award Number:** ST/T00021X/1
   Awarded by the Science and Technology Facilities Council. `paper/paper.md`: "the consolidated
   grant ST/T00021X/1". "Consolidated Grant" is STFC's own name for this award instrument; the papers
   give no longer title.

3. **Award Title:** Postgraduate Research Studentship
   **Award Number:** Not found
   Awarded by the Department for the Economy (Northern Ireland) to C. D. MacBride. Both papers
   describe it — "the award of a PhD studentship" and "their postgraduate research studentship" — but
   neither gives a grant number, and none is discoverable elsewhere. The missing number is a genuine
   absence in the sources, not an extraction gap.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

1. **DOI:** https://doi.org/10.1098/rsta.2020.0171
   MacBride, C. D., Jess, D. B., Grant, S. D. T., Khomenko, E., Keys, P. H., & Stangalini, M. (2021).
   Accurately constraining velocity information from spectral imaging observations using machine
   learning techniques. *Philosophical Transactions of the Royal Society A*, 379(2190), 20200171.

Retained unchanged. This is the paper describing the *method* MCALF implements, as distinct from the
JOSS paper describing the software (Field 14). `paper/paper.md` states that "The method implemented
in this IBIS model has been discussed extensively in @MacBride:2020", `README.rst` asks users to cite
it alongside the JOSS paper, and `paper/paper.bib` carries the full entry. It is also the source of
the observational context recorded in Fields 28, 31 and 32.

**A 403 from this DOI is not a broken link.** The DOI redirects to
`royalsocietypublishing.org`, which refuses unauthenticated automated requests with HTTP 403. The
DOI itself is valid and resolves correctly — Crossref returns the matching title, authors, journal,
volume 379 and issue 2190, and the full text is available via PMC. A future refresh should confirm
this DOI through Crossref rather than by fetching the publisher page, and must not treat the 403 as
evidence that the reference is dead.

**Considered and rejected.** `paper/paper.bib` contains three further references, none of which is a
publication about or using MCALF, so none belongs here:

- Stangalini et al. (2020), *Spectropolarimetric fluctuations in a sunspot chromosphere*,
  10.1098/rsta.2020.0216 — cited in `paper/paper.md` as motivation for why constrained velocities
  are scientifically valuable. C. D. MacBride is a co-author, but the paper does not describe or use
  MCALF.
- Felipe, Socas-Navarro & Khomenko (2014), 10.1088/0004-637x/795/1/9 — cited for the physical origin
  of superimposed emission components.
- Panos et al. (2018), 10.3847/1538-4357/aac779 — cited as an example of an alternative classifier
  the toolkit could accommodate.

### 28. Related Datasets (OPTIONAL)

- **Dataset:** MacBride, C. D., & Jess, D. B. (2023). *IBIS Ca II 8542 Å sample dataset for MCALF*
  [Data set]. Included with MCALF v1.0.0.
  https://github.com/ConorMacBride/mcalf/tree/v1.0.0/examples/data/ibis8542data

The entry has no DOI; Field 28 explicitly permits an APA-style citation with a permanent link in
that case, which is the form recorded above.

The dataset is a real observational excerpt, not synthetic demo data: a 60 × 50 spatial array of
Ca II 8542 Å spectra at 27 non-equidistant wavelength points (`spectra.fits`), the wavelength grid
(`wavelengths.txt`), a labelled 200-spectrum neural-network training set covering classifications 0–4
(`training_data.json`), and pre-computed fit results (`results.fits`). It was introduced in v0.2.1
("Added example `Working with IBIS data` to Example Gallery, using a real IBIS spectral imaging
dataset"), it is the dataset the documented end-to-end workflow runs on, and the gallery script
`examples/gallery/models/plot_ibis8542data.py` downloads it at run time from a stable raw GitHub URL.
The URL above is pinned to the `v1.0.0` tag rather than `main` so it remains resolvable if the
default branch changes; it is 77 characters, well inside the 200-character URL limit.

**Negative research on the full source dataset — do not go looking for a DOI.** The observations
behind both the sample data and the reference paper are IBIS Ca II 8542 Å scans of active region
NOAA 12149, taken 14:37–17:37 UT on 30 August 2014 at the Dunn Solar Telescope (2103 spectral scans,
0.098″ per pixel, 5.8 s cadence). The reference paper's Data Accessibility statement is explicit that
they are not deposited anywhere: they come from the observing campaign "Nanoflare Activity in the
Lower Solar Atmosphere" (NSO-SP proposal T1020, PI D. B. Jess), and "The data that support the plots
within this paper and other findings of this study are available from the corresponding author upon
reasonable request." There is therefore no dataset DOI and no archive landing page for the full
observation, and none is likely to appear.

**Why the bundled sample dataset is recorded rather than the field left empty.** It has a stable,
publicly resolvable tag-pinned link but no DOI and no independent publication of its own, which is a
weaker identifier than this field usually carries, and it is a documentation excerpt rather than a
published dataset. It is recorded anyway because it is genuinely "a dataset the software supports
functionality for", it is the only concrete dataset associated with this software that a user can
actually obtain, and a tag-pinned GitHub URL is durable. A third option was considered and rejected:
citing the reference paper (10.1098/rsta.2020.0171) as "the publication that described the dataset",
which Field 28's instructions permit — but that DOI is already recorded in Field 27, and duplicating
it across both fields adds a redundant related-item row without adding any information.

### 29. Related Software (OPTIONAL)
- **Not found**

This is a considered conclusion, not an extraction gap.

MCALF has no predecessor, no fork parent, no companion package, and no domain-specific dependency.
Its seven declared dependencies in `setup.cfg` are `astropy`, `matplotlib`, `numpy`, `pathos`,
`pyyaml`, `scikit-learn` and `scipy`. Six of those are generic scientific-Python or general-purpose
infrastructure — arrays, plotting, YAML parsing, optimisation, multiprocessing — and are excluded
from this field by rule, because naming them would say nothing that is not equally true of most of
the ecosystem. `astropy` is a domain-adjacent dependency that does clear the evidence bar for
interoperability, and is recorded in Field 30 where it belongs.

**`scikit-learn` — considered at length and rejected; do not re-propose it without new grounds.**
It is the strongest candidate by some distance, and the argument for it is real: MCALF's
`neural_network` attribute is a documented plug-in point that accepts any scikit-learn-compatible
estimator, `ModelBase.train`/`test`/`classify_spectra` delegate straight to the estimator's
`fit`/`predict` interface, the gallery example demonstrates pickling and reloading a trained
estimator into `model.neural_network`, and `paper/paper.md` presents this as a designed feature —
"The 'toolkit' nature of this package also allows the possibility of utilising existing machine
learning classifiers, such as the 'supervised hierarchical k-means' classifier introduced in
@Panos:2018". It is nonetheless excluded, because the governing test is whether the package would be
equally at home in a web application, a finance model or a biology pipeline. scikit-learn plainly
would be: it is domain-generic machine-learning infrastructure, not a heliophysics or science peer
tool, and it therefore gets the same treatment as numpy and matplotlib in both Field 29 and Field 30.

**Similar-purpose software.** Other solar spectral-line inversion and fitting codes exist, but
neither the repository nor the JOSS paper names one. `paper/paper.bib` holds four entries and all
four are science papers, not software; the nearest thing to a software citation is Panos et al.
(2018), and `paper/paper.md` cites it for its classification *method* rather than as a package to
use. Naming comparable inversion codes here would be an inference from domain knowledge rather than
metadata extracted from this software's own sources, so none is recorded.

**Superseding a previous entry in this dossier.** An earlier extraction listed all seven
`install_requires` dependencies (astropy, matplotlib, numpy, scikit-learn, scipy, pathos, PyYAML) in
this field. That entry is withdrawn: it is exactly the generic-stack listing the relevance gate
excludes, and being a dependency is not the same as being related software.

### 30. Interoperable Software (OPTIONAL)

1. **Astropy** — https://github.com/astropy/astropy

Astropy is a Tier B package under the relevance rules for this field, admissible only with a
specific documented exchange rather than on dependency presence. The exchange here is
concrete, public and bidirectional:

- **Astropy objects are accepted by MCALF's public API.** `mcalf.visualisation.plot_map` documents
  `arr : numpy.ndarray[float] or astropy.units.quantity.Quantity`,
  `resolution : tuple[float] or astropy.units.quantity.Quantity`, and
  `unit : str or astropy.units.UnitBase or astropy.units.quantity.Quantity`. The implementation
  branches on `isinstance(arr[0, 0], astropy.units.quantity.Quantity)` to strip the unit and render
  it with `astropy.units.format.LatexInline` in the axis and colourbar labels.
  `mcalf.visualisation.plot_class_map` and `init_class_data` accept `resolution` as a Quantity the
  same way, through `mcalf.utils.plot.calculate_extent`.
- **The documented example exercises it.** `examples/gallery/models/plot_ibis8542data.py` passes
  `'resolution': (0.098 * 5 * u.arcsec, 0.098 * 5 * u.arcsec)` into `plot_map`, and the resulting
  axis labels carry the arcsecond unit.
- **MCALF's output is an Astropy data product.** `mcalf.models.FitResults.save` builds an
  `astropy.io.fits.HDUList` (primary HDU plus named `PARAMETERS`, `CLASSIFICATIONS`, `PROFILE`,
  `SUCCESS`, `CHI2`, `VLOSA`, `VLOSQ` HDUs) and writes it with checksums;
  `mcalf.utils.misc.merge_results` reads such files back through `astropy.io.fits` and merges them
  with overlap detection.
- The dependency is pinned at `astropy>=4.2` and CI includes an `oldestdeps` job holding
  `astropy==4.2.*`, so the interoperation is tested across the supported range.

**Considered and rejected — SunPy.** An earlier extraction recorded "sunpy ecosystem — part of the
solar physics Python ecosystem (PyHC member)". This is withdrawn: PyHC membership is explicitly not
sufficient evidence of interoperation with any particular package. SunPy is not a declared
dependency, there is no `import sunpy` anywhere in the repository, and no MCALF object converts to or
from a SunPy type.

SunPy *is* named in the repository, in two contexts, and neither is interoperability — recorded
here so a future agent who finds them does not mistake them for evidence. First, `docs/guide/index.rst`
points contributors at SunPy's developer-environment setup guide: "The SunPy Community have compiled
an excellent set of instructions... You can mostly replace ``sunpy`` with ``mcalf``". That is a
contributing-workflow reference. Second, `src/mcalf/tests/helpers.py` carries docstring attributions
on `get_mpl_ft2_version` and `figure_test` reading "Based on functions at
https://github.com/sunpy/sunpy/blob/v2.0.7/sunpy/tests/helpers.py" together with SunPy's own citation
(DOI 10.5281/zenodo.4423217). That is code provenance for two internal matplotlib figure-hashing test
helpers — it credits SunPy properly, but it neither imports SunPy nor exchanges any data with it, it
is invisible to users, and it does not make MCALF a fork of SunPy, so it supports neither Field 29
nor Field 30.

**Considered and rejected — matplotlib.** MCALF's visualisation functions take and return matplotlib
`Axes` and `Figure` objects, which is a real API-level integration, but matplotlib is Tier A generic
plotting infrastructure and is excluded without exception. The same applies to numpy, scipy, pathos
and PyYAML.

**Considered and rejected — IDL.** `examples/example1/FittingIBIS.pro` drives MCALF through the IDL
Python bridge (`Python.Import('mcalf.models')`), which is a genuine cross-language bridge. It is
excluded for three reasons: IDL is a proprietary language rather than a named domain tool such as
SPEDAS, so there is no DOI or repository URL this field could record; the bridge is an example
script excluded from the distribution by `prune examples` in `MANIFEST.in`; and the example's own
README states "It is not recommended to use the IDL wrapper in production... IDL is not fully
supported in the current version of the code" because Python tuples cannot be passed from IDL,
making some calls impossible.

### 31. Related Instruments (OPTIONAL)

- **Instrument Name:** Interferometric BIdimensional Spectrometer
- **Instrument Identifier:** https://spase-metadata.org/SMWG/Instrument/DST/IBIS

**Relevance.** MCALF passes the designed-to-support test unambiguously for IBIS. It ships
`mcalf.models.IBIS8542Model`, a class whose name is the instrument's, whose docstring reads "Class
for working with IBIS 8542 Å calcium II spectral imaging observations", and whose defaults are
tuned to that instrument's data: `stationary_line_core = 8542.099145376844`, absorption/emission
guesses, bounds and characteristic scales, two sigma weighting profiles, and a prefilter-response
correction path for IBIS prefilter reference files. `mcalf.visualisation.plot_ibis8542` is a
dedicated plotting function for its fits. The shipped sample dataset, the gallery example
`plot_ibis8542model.py`, the IDL example and the JOSS paper all centre on IBIS. A user searching
HSSI for `instrument:"IBIS"` should certainly get this record back.

**SPASE resolution.** Every row in HSSI's instrument/observatory vocabulary carries an
`https://spase-metadata.org/` identifier, which is what makes the resolution below a binding to a
real SPASE resource rather than a free-typed name. Treat that compliance as a dated observation, not
an invariant: a row whose identifier fails that prefix is upstream drift or a wrongly created row,
and must be reported rather than used.

Searching type 1 (instrument) rows for `ibis`, `interferometric`, `bidimensional` and `dunn` returns
exactly one real-world entity in two duplicate forms:

| Row `name` | Identifier |
|---|---|
| `Interferometric BIdimensional Spectrometer` | `https://spase-metadata.org/SMWG/Instrument/DST/IBIS` |
| `Interferometric BIdimensional Spectrometer (IBIS)` | `https://spase-metadata.org/SMWG/Instrument/DST/IBIS.html` |

These are the same SPASE resource in bare and `.html` form, so this is not an ambiguous multi-row
match — the bare row is preferred by rule, and its `name` is reproduced above exactly as the row
carries it. The identifier path segment `DST` independently corroborates the Dunn Solar Telescope
association recorded in Field 32.

**The stored HSSI value is bound to the `.html` duplicate.** The live record shows
`Interferometric BIdimensional Spectrometer (IBIS)`, which is the literal `name` of the `.html` row —
and it cannot be a `name (abbreviation)` rendering of the bare row, because the bare row's
`abbreviation` is empty. Recording the bare row above is therefore a substantive correction toward
the preferred SPASE resource, not a cosmetic one. The SPASE identifier, not the name, is what
reliably distinguishes the two rows, so any later comparison should key on it.

**Considered and rejected.** The Helioseismic and Magnetic Imager on the Solar Dynamics Observatory
provided supporting context observations for the reference paper, but MCALF reads no HMI or SDO data,
implements nothing specific to them, and neither is mentioned anywhere in the repository. They belong
to the paper, not to the software.

### 32. Related Observatories (OPTIONAL)

- **Observatory Name:** Dunn Solar Telescope
- **Observatory Identifier:** https://spase-metadata.org/SMWG/Observatory/DST

**Relevance and evidence.** IBIS is the Dunn Solar Telescope's instrument, and the association is
documented rather than inferred. The SPASE identifier for the instrument is itself
`.../SMWG/Instrument/DST/IBIS`, placing IBIS under DST. The reference paper's observations section
states the data were taken with "the Interferometric BIdimensional Spectrometer (IBIS) at the
National Science Foundation's Dunn Solar Telescope, New Mexico, USA", and its Data Accessibility
statement adds that the observing campaign "employed the ground-based Dunn Solar Telescope, USA,
during August 2014" and that "The Dunn Solar Telescope at Sacramento Peak/NM was operated by the
National Solar Observatory (NSO)". An earlier extraction recorded this observatory as inferred and
"not explicitly stated"; that caveat is now resolved — it is explicit in the reference publication
and in the SPASE identifier structure.

**SPASE resolution.** Searching type 2 (observatory) rows returns one real-world entity in two
duplicate forms:

| Row `name` | Abbreviation | Identifier |
|---|---|---|
| `Dunn Solar Telescope` | `DST` | `https://spase-metadata.org/SMWG/Observatory/DST` |
| `Dunn Solar Telescope (DST)` | *(empty)* | `https://spase-metadata.org/SMWG/Observatory/DST.html` |

The bare row is preferred and its `name` is reproduced above exactly as the row carries it. The
live record displays
`Dunn Solar Telescope (DST)`, which is consistent with *either* the `.html` row's literal name or a
`name (abbreviation)` rendering of the bare row — the two hypotheses are indistinguishable from the
view response alone. Either way the bare row plus its identifier is the correct value to store, and
the identifier disambiguates it on update.

**Considered and rejected — `NSO Observatory Group`
(`https://spase-metadata.org/SMWG/Observatory/NSO`).** This row exists and the National Solar
Observatory did operate the Dunn Solar Telescope at Sacramento Peak, but it is an umbrella group
covering many facilities. MCALF supports IBIS at DST specifically, and the guidance is to prefer the
specific over the broad. Adding NSO would dilute the association without adding information.

**Both fields resolve cleanly.** Field 31 and Field 32 each bind to a single SPASE-backed row
carrying an `https://spase-metadata.org/` identifier. Neither is left unresolved, ambiguous between
candidate rows, or recorded as a bare name — which matters because a name with no identifier does
not match an existing row reliably and can instead mint a new identifierless one.

### 33. Logo (OPTIONAL)
- **Not found**

Negative research, so this does not need repeating: the repository contains no logo or brand image —
the only image files tracked are matplotlib figure-comparison baselines under
`src/mcalf/tests/baseline_*/` and `paper/figure.pdf`, which is the JOSS paper's plotting-overview
figure rather than a logo. `docs/conf.py` sets `html_theme = 'sphinx_rtd_theme'` and defines neither
`html_logo` nor `html_favicon`. The PyHC community registry entry for MCALF has no `logo:` key,
although that field exists and is populated for other registry entries. The badges in `README.rst`
are shields.io status badges (build, coverage, PyPI, Zenodo DOI, docs, licence, code of conduct), not
artwork. MCALF simply has no logo.

---

## Cross-Field Notes

**Which source is authoritative for what.** DataCite (concept 10.5281/zenodo.3924527 and version
10.5281/zenodo.7779553) is authoritative for the persistent identifiers, publisher, licence name,
version string and issue date, and it is where the empty `fundingReferences` array is visible. Zenodo record 7779553 confirmed the
concept/version relationship and the publication date — and supplied the incorrect
`bsd-2-clause-netbsd` licence identifier documented under Field 15. The PyHC **community** registry
(`_data/projects.yml`; MCALF is not in the core or unevaluated lists) supplied curated keywords,
the documentation URL, the short name, and the six "Good" quality ratings. The GitHub API supplied
release dates, topics, licence detection and the activity evidence behind Field 23. The ORCID public
API supplied both authors' identity records and the Queen's University Belfast ROR. The ROR API
confirmed all six organisation identifiers. `paper/paper.md` and the reference paper supplied the
funding, the observational context, and the science framing.

**Where the DOI autofill cascade is insufficient for this record.** Funding (Fields 25–26),
Development Status (23), Jess's second affiliation, the affiliation RORs, the additional input and
output formats, the Apple Silicon architecture, and the Data Visualization and Models and Simulations
parent categories are all invisible to DataCite, Zenodo and SoMEF. They come from the paper source,
the CI configuration, PyPI artefacts and the source code. A future refresh that relies on the autofill
cascade alone will not reproduce them.
