# HSSI Metadata Extraction Results

**HSSI Software ID:** 982c8a07-8ad1-400c-8842-2fb10ad69c21
**Repository:** https://github.com/MihailoMartinovic/SAVIC
**Source Revision:** d7a1b2a52ecddedd64c94d6341de42cc4f9c162f
**Extraction Date:** 2026-09-09
**Validation Date:** 2026-09-10
**Validation Status:** PASS

---

## Scope note — read this before interpreting the evidence

Four structural facts about SAVIC decide most of the fields below, and misreading any of them
produces a plausible-looking but wrong value.

1. **SAVIC is a machine-learning surrogate for a dispersion solver, not a data-analysis pipeline.**
   Its published API is DataFrame-in / DataFrame-out. `docs/03-functions-chain.rst:17` gives `SAVIC.SAVIC` an
   input of "input data frame" and line 19 gives it an output of "output data frame", and
   `source/src/savic/SAVIC_Input_Sort.py:9-12` defines the four accepted column sets. The package
   contains no reader and no writer for any file format: the only file access in the installed
   package is the loading of its own bundled model artifacts (`xgb.XGBClassifier().load_model(...)`
   at e.g. `source/src/savic/SAVIC_P_C.py:7-9`; `np.load` of the Gaussian-mixture parameters at
   `source/src/savic/SAVIC_C_C.py:11-17`). This governs Fields 17, 18 and 19.

2. **Its inputs are fitted bi-Maxwellian VDF *parameters*, never distributions.** The accepted
   columns are the core parallel plasma beta, the temperature anisotropies, the temperature
   disequilibria, the relative densities and the drifts of the core, beam and alpha populations
   (`source/src/savic/SAVIC_Input_Sort.py:9-12`, mirrored in `docs/03-functions-base.rst:36`,
   `:54`, `:72`, `:90`). Paper II describes the same set: "The dimensionless parameters that
   comprise [the input set] include the core proton parallel plasma beta ... the temperature
   anisotropies of each component, the temperature disequilibrium between the components, as well
   as their relative densities and drifts" (quoting the article text, lines 125-130).
   This is why several velocity-space functionality rows are rejected in Field 4.

3. **The repository ships the two journal articles that define the science, and exposes them
   through the public API.** `tutorial/Article_I_Statistical_Trends.pdf` and
   `tutorial/Article_II_Classification_and_Multidimensional_Mapping.pdf` are tracked at the pin;
   `source/src/savic/tutorial.py:16-18` returns both paths from `article_path()`;
   `source/src/savic/__init__.py:85-91` downloads both at import time; and
   `docs/02-structure-git.rst:109` describes the folder as holding "the files with examples,
   tutorial notebook, the detailed pdf readme file, and two published articles." The papers are
   therefore primary sources for this record, not external context — they carry the funding
   acknowledgment (Fields 25/26), the training-data provenance (Fields 31/32) and the antecedent
   solver (Field 29).

4. **`source/` is the packaging root, not the repository root.** The licence lives at
   `source/LICENSE` and the package metadata at `source/pyproject.toml`. The repository root holds
   the twelve development notebooks and the `Output/ML/models/` artifact tree. Tools that look for
   root-level files therefore report absences that are not real; Field 15 records the one case
   where that has already produced a wrong external value.

Where the pinned tree and any external metadata source disagree, the tree governs. Quotations from
the two articles are taken from plain-text extractions of the PDFs that ship at
`tutorial/Article_I_Statistical_Trends.pdf` and
`tutorial/Article_II_Classification_and_Multidimensional_Mapping.pdf`, produced with `pdftotext`;
the "article text line N" citations below refer to line numbers in those extractions, so they are
reproducible from the repository alone. Two mechanical artifacts of that extraction affect the
quotations below, and both are normalised to ordinary ASCII where they occur: the "fi" and "fl"
ligatures come through as single glyphs, and typographic characters (en dashes, em dashes, the
"approximately" tilde) come through as their Unicode originals. The extraction also breaks long
tokens across lines, so the repository URL quoted in Field 14 appears in the extraction split
between two lines and is rejoined here.

---

## Section 1: Basic Information

### 1. Submitter

- **Submitter Name:** [To be filled by actual submitter]
- **Submitter Email:** [To be filled by actual submitter]

The placeholder form is the catalogue-wide convention for this campaign. Nothing in the pinned
repository, the DOI records, or the PyHC registry identifies who submitted this entry to HSSI, and
no identity is inferred here.

### 2. Persistent Identifier (RECOMMENDED)

- **DOI:** https://doi.org/10.5281/zenodo.8170235

This is the Zenodo **concept** DOI — the identifier that always resolves to the newest deposited
version — and it is the correct value for this field. It must not be "freshened" to a
version-specific DOI on the grounds that the tree has moved to v1.2.7; the version DOI belongs in
Field 12's Version PID, and this field belongs to the software as a continuing work.

DataCite's record for this DOI confirms it is the concept record: it carries five `HasVersion`
relations (to `10.5281/zenodo.8170236`, `10.5281/zenodo.10581356`, `10.5281/zenodo.17344665`,
`10.5281/zenodo.17382178` and `10.5281/zenodo.17685377`) and no `IsVersionOf` relation of its own.

The same record also carries `IsSupplementTo
https://github.com/MihailoMartinovic/SAVIC/tree/v1.2.7`. A `tree/<tag>` supplement URL is the
signature Zenodo's GitHub release integration writes; a hand-made Zenodo upload has no such
relation. That matters twice over: it explains why the deposit's `creators` block holds nothing but
the bare GitHub login `MihailoMartinovic` (see Field 6), and it means new tagged releases will keep
minting version DOIs under this same concept DOI without maintainer action.

The README's badge is a Zenodo *badge* URL (`readme.md:10`, pointing at
`https://zenodo.org/badge/latestdoi/592545400`), which resolves to the latest version rather than
naming the concept DOI in the file. The concept DOI recorded here comes from the DataCite record,
not from the badge string.

### 3. Code Repository (MANDATORY)

- **URL:** https://github.com/MihailoMartinovic/SAVIC

Confirmed from three independent directions: `source/pyproject.toml:32` declares
`Source = "https://github.com/MihailoMartinovic/SAVIC"`; the PyHC registry entry gives the same URL
in its `code:` field (`_data/projects.yml:602` in `heliophysicsPy/heliophysicsPy.github.io`); and
Paper II names it in the text — "The three parts of the SAVIC code ... are available at
https://github.com/MihailoMartinovic/SAVIC" (article text lines 716-720).

The package also hard-codes this repository as a runtime asset host:
`source/src/savic/__init__.py:97-98` sets
`BASE_URL_MODELS = "https://raw.githubusercontent.com/MihailoMartinovic/SAVIC/main/Output/ML/models/"`
and `BASE_URL_TUTORIAL = "https://raw.githubusercontent.com/MihailoMartinovic/SAVIC/main/tutorial/"`,
which `check_and_download_files` (lines 112-141) calls at import (lines 147-148). Those are the
package's only network reads, and they are reads of this repository — a fact that recurs in
Fields 17 and 31/32.

### 4. Software Functionality (RECOMMENDED — treated as critical)

**Values:**
- Data Processing and Analysis
- Data Processing and Analysis: ML/AI
- Data Processing and Analysis: Analysis
- Models and Simulations
- Models and Simulations: ML/AI
- Models and Simulations: Forecasting
- Models and Simulations: Data Guided
- Models and Simulations: Empirical

**Every value is written fully qualified as `Parent: Child`, and that is load-bearing.** The
vocabulary has 83 rows built from fewer distinct names, because thirteen child names occur under
more than one parent. `ML/AI` is one of them, and this record holds **two different `ML/AI` rows** —
the `Data Processing and Analysis` one and the `Models and Simulations` one. A bare `ML/AI` written
into this field would bind to whichever twin the lookup reached first, so the qualified form is the
only safe way to express either. Both parents are present, as the rule requires: a subcategory never
appears without its top-level parent.

**Evidence for the six values carried forward from the previous record**, all at the pinned
revision:

- `Data Processing and Analysis` and `Data Processing and Analysis: ML/AI` — the entire package is
  gradient-boosted-tree and Gaussian-mixture inference applied to observational VDF-fit parameters.
  `git grep -n -P 'GaussianMixture|from sklearn' <pin> -- source/src/savic` returns 13 lines across
  9 of the package's 20 Python files, and every `SAVIC_P_*`, `SAVIC_Q_*` module loads an XGBoost
  model from `Output/ML/models/` (`source/src/savic/SAVIC_P_C.py:7-9`,
  `source/src/savic/SAVIC_Q_C.py:7-9`).
- `Data Processing and Analysis: Analysis` — the user-facing product is a derived physical
  characterisation, not a transformed data file: the output frame carries `unstable`, `Pow_core`,
  `Pow_beam`, `Pow_alpha`, `kB_angle`, `group` and `ins_type`
  (`source/src/savic/SAVIC.py:35-37`; `docs/03-functions-chain.rst:31`). Paper II frames the same
  thing as the point of the code: "To access stability properties of any limited sample of VDFs, it
  is required to use either the SAVIC code presented here, or a traditional dispersion solver"
  (article text lines 848-851).
- `Models and Simulations` and `Models and Simulations: ML/AI` — the shipped XGBoost regressors and
  Gaussian-mixture classifiers *are* the model. They stand in for a numerical dispersion solver, and
  the package distributes them as data files (`Output/ML/models/`, 24 XGBoost JSON models and four
  GMM parameter sets at the pin) rather than deriving anything from first principles at run time.
- `Models and Simulations: Forecasting` — retained, with a caveat recorded so a later reader does
  not mistake it for an oversight. SAVIC "predicts" in the classification sense (given a VDF's
  parameters, is it unstable, and which mode) rather than in the time-forward sense a space-weather
  forecast implies. It is kept because prediction is the software's own framing throughout —
  SAVIC-P is the "predictor of the VDF stability" (`docs/01-purpose.rst:7`) and all four
  `SAVIC_P_*` descriptions in `docs/03-functions-base.rst` (lines 28, 46, 64 and 82) begin
  "Predicts stability of a VDF" — and
  because a searcher filtering for predictive plasma-stability tools should find this. Considered
  for removal on the strict time-forward reading and not removed.

**Rejected alternatives, recorded so they are not re-proposed:**

- `Data Visualization` and every one of its children — **rejected on measurement, not impression.**
  `git grep -a -l -i -P 'matplotlib|pyplot|plt\.' <pin> -- .` over all 159 tracked paths matches
  only PNG files under `Output/ML/models/`, where the string occurs inside the image metadata of
  figures matplotlib produced elsewhere. No Python file, notebook or `.rst` file in the tree matches.
  The package draws nothing.
- `Data Processing and Analysis: Data Access and Retrieval` — rejected. The package's only network
  activity is fetching its own model and tutorial assets from its own repository at import
  (`source/src/savic/__init__.py:112-148`). That is installation plumbing for the package's own
  bundled assets, not a data-retrieval capability offered to users; there is no query interface, no
  archive client, and no user-callable download function.
- `Data Processing and Analysis: File Format Conversion` — rejected for the same reason as Fields 18
  and 19: the package neither reads nor writes any format.
- `Servers and Environments` and children — rejected. No container, server, or parallel-execution
  code exists in the tree.
- `Mission-related` and children — rejected. SAVIC is not part of any mission ground system; see
  Fields 31/32 for the separate and more delicate question of the Helios training data.

**Six candidates were examined when this record was refreshed: two were added and four were
rejected.** Each is given its reason below whichever way it fell, because the reasoning is the
durable part.

- `Data Processing and Analysis: Plasma Moments` — **rejected.** The taxonomy's sense of this
  row is computing density, velocity, temperature and pressure *from* distributions, i.e. moment
  integration. SAVIC never integrates a distribution; the moment-like quantities (betas,
  anisotropies, densities, drifts) arrive already fitted, as scope note 2 sets out, and Paper II
  attributes the fitting to a separate work (the VDFs were "fitted as a sum of Maxwellian
  components (Ďurovcová et al. 2019)", article text lines 94-95). Selecting this row would make
  SAVIC findable as a moments code, which it is not.
- `Data Processing and Analysis: 3D Particle Distribution Processing` — **rejected**, and it was
  the closest call among the rejections. Every user-facing description of the package speaks of
  VDFs, so the row is tempting. But the taxonomy's indicators for it are distribution-function
  math, velocity space operations and phase-space density, and nothing in `source/src/savic`
  touches phase space:
  the code's arithmetic is `np.log10` of scalar parameter columns, tree inference, and closed-form
  threshold curves. A user with a 3D distribution in hand cannot feed it to SAVIC.
- `Models and Simulations: Data Guided` — **added.** The taxonomy's sense is a model driven
  by observational data, and SAVIC is that twice over: the models are trained entirely on a database
  of real Helios observations processed through a dispersion solver (Paper II abstract, article text
  lines 27-30: "we use this comprehensive set of instability calculations to train a
  machine-learning algorithm"), and every evaluation is driven by observed VDF-fit parameters
  supplied by the user. This is the value that distinguishes SAVIC from an analytic stability model,
  and a searcher looking for observationally grounded models should find it.
- `Models and Simulations: Theory` — **rejected.** SAVIC contains no analytical solution and no
  theoretical framework. The linear theory lives in the dispersion solvers that produced the
  training set (see Field 29), and SAVIC exists precisely so that the theory need not be re-solved.
- `Models and Simulations: Empirical` — **added on direct code evidence.**
  `source/src/savic/SAVIC_C_C.py:25-28` evaluates four closed-form parameterized instability
  thresholds of the classic form
  `1 + 0.367 / (beta_par_core - 0.011)**0.364`, one each for the ion-cyclotron, mirror, fast
  magnetosonic and oblique-firehose modes, and uses them as engineered features for the classifier.
  `git grep -l -P 'uns_IC' <pin> -- source/src/savic` returns all four `SAVIC_C_*.py` modules, so
  this is systematic rather than incidental. Empirical parameterized thresholds evaluated in code
  are exactly what this row describes. **Added, on a narrower basis than `Data Guided`**: the
  counter-argument weighed and set aside is that `ML/AI` already names the modelling mechanism and
  the thresholds are inputs to it rather than the delivered model.
- `Data Processing and Analysis: Processing` — considered and **rejected**. `SAVIC_Input_Sort`
  partitions the input frame by which components are present
  (`source/src/savic/SAVIC_Input_Sort.py:19-62`) and the modules log-transform columns, but these
  are internal steps of the analysis the `Analysis` row already covers. Adding the generic
  `Processing` row would carry no information a searcher could use.

**None of the six previously held values was removed**, and the two additions are `Models and
Simulations: Data Guided` and `Models and Simulations: Empirical`. Both are supported by code and by
the papers, and both make the entry findable for real searches that would otherwise miss it — in
particular, the observational grounding of the trained models is arguably SAVIC's most distinctive
property and would otherwise go unrepresented.

Two narrower readings were weighed and set aside. Adding `Data Guided` alone was the conservative
alternative, on the view that `Models and Simulations: ML/AI` already carries the modelling
mechanism and that `Empirical` risks reading as a claim that SAVIC ships an empirical formula as its
product; it was rejected because the four closed-form thresholds are evaluated in code across all
four `SAVIC_C_*` modules, which is precisely what the `Empirical` row describes. Adding nothing at
all was rejected for the reason just given about observational grounding.

Four candidates are rejected outright, for the reasons given above: `Plasma Moments`,
`3D Particle Distribution Processing`, `Theory` and `Processing`.

### 5. Related Region (RECOMMENDED — treated as critical)

**Values:**
- Interplanetary Space
- Solar Environment
- Solar Wind

**The Region vocabulary is flat.** All 24 rows are top-level; none has a parent and none has a
child. A coarse value therefore never implies a finer one and a finer one never implies its coarse
relative, so the right question for this refresh is not "are the stored values still valid" but
"which additional rows now apply".

`Interplanetary Space` is the region SAVIC's science actually occupies: Paper I diagnoses "unstable
behavior of solar wind plasma between 0.3 and 1 au" (article text line 29) and the trained
models' validity domain is that heliocentric range. `Solar Environment` is retained as stored; it is
the looser of the two, and it is worth recording that it was examined rather than waved through —
SAVIC's domain begins at 0.3 au rather than at the Sun, so the row earns its place through the
solar-wind-source framing of the science (Paper II's central result concerns "the young solar wind"
versus "the collisionally old plasma", abstract, article text lines 31-32) rather than through any
coronal or photospheric capability. No removal is proposed.

**`Solar Wind` was added alongside the two rows previously held.** Every primary description of
this software names the solar wind as its subject: `docs/01-intro.rst:12` opens "The understanding
of the solar wind plasma kinetics is based on examining the Velocity Distribution Function (VDF) of
particles"; the stored description and concise description both say "in the solar wind"; and
`solar wind` is already a stored keyword. Because the vocabulary is flat, `Interplanetary Space`
does not deliver this on its own: before the addition, a user filtering Region by `Solar Wind` got
nothing back for SAVIC, which is plainly wrong for a solar-wind stability package.

The rejected alternative was to leave the two rows alone, on the view that `Interplanetary Space` is
the region and `Solar Wind` is the medium filling it. That reading is coherent, but it is a semantic
preference that the flat vocabulary does not enforce, and it costs the entry a search route.

Note that Field 22 offers a `Solar Wind` row too. **The two were decided independently**, and both
were taken; neither choice implied the other.

### 6. Authors (MANDATORY)

**Author 1:**
- **Name:** Mihailo M. Martinovic
- **Author Identifier:** https://orcid.org/0000-0002-7365-0472
- **Affiliation:**
  - **Organization:** University of Arizona
  - **Affiliation Identifier:** https://ror.org/03m2x1q45

**The stored spelling `Mihailo M.` / `Martinovic`, without the diacritic, is a deliberate retention,
not an oversight.** The three primary sources disagree with one another: `source/pyproject.toml:9`
writes `{ name="Mihailo Martinovic", email="mmartinovic@arizona.edu" }` with no diacritic;
`source/LICENSE:1` writes "Copyright (c) 2025 Mihailo Martinovic", also without; ORCID
`0000-0002-7365-0472` gives given-names `Mihailo` and family-name `Martinović` with the diacritic
and carries no credit name or other names; and the deposit's DataCite contributor block writes
`Martinović, Mihailo M.` The campaign precedent is to mirror the project's own spelling rather than
to "correct" it toward the diacritic form, and the project's own spelling in its packaging metadata
and its licence is the undiacriticked one. The middle initial comes from the deposit and from both
papers' bylines. No change is proposed.

The affiliation is confirmed independently of the deposit: Paper II's author list gives
"Lunar and Planetary Laboratory, University of Arizona, Tucson, AZ 85721, USA;
mmartinovic@arizona.edu" (article text line 17), matching the `arizona.edu` address in
`source/pyproject.toml:9`. Paper II also lists a second affiliation for him, "LESIA, Observatoire de
Paris, Université PSL, CNRS, Sorbonne Université, Université de Paris, 92195 Meudon, France"
(article text line 18). That second affiliation is **not** proposed for addition: the deposit, the
package metadata and the licence all give Arizona alone, and a paper byline records where an author
held appointments when the paper was written rather than which institution the software is
attributed to.

**Author 2:**
- **Name:** Kristopher G. Klein
- **Author Identifier:** https://orcid.org/0000-0001-6038-1923
- **Affiliation:**
  - **Organization:** University of Arizona
  - **Affiliation Identifier:** https://ror.org/03m2x1q45

*Why he is an author.* The Zenodo deposit's DataCite record carries a `contributors` block
with exactly two entries, each with a full name, an ORCID and an affiliation:
`Martinović, Mihailo M.` as `ContactPerson` (ORCID `0000-0002-7365-0472`, University of Arizona) and
`Klein, Kristopher G.` as `ProjectMember` (ORCID `0000-0001-6038-1923`, University of Arizona). That
block cannot have been generated automatically: the 159 tracked paths at the pin include no
`CITATION.cff`, no `codemeta.json` and no `.zenodo.json`, so there is no file in the repository from
which Zenodo could have derived it. It was entered by hand on the deposit, which makes it the only
curated author statement anyone associated with this software has published. Klein co-authors both
articles the package ships — Paper I (Martinović, Klein, Ďurovcová & Alterman 2021) and Paper II
(Martinović & Klein 2023) — and Paper II is the paper that presents SAVIC. The prior dossier for
this repository listed him as Author 2 on exactly this basis.

*The one-author reading, and why it was rejected.* `source/pyproject.toml:8-10` names Martinović
alone in its `authors` array, and `source/LICENSE:1` names him alone as copyright holder.
DataCite's `creators` block — the field that normally carries authorship — holds a single entry
whose entire content is the bare GitHub login `MihailoMartinovic`, with no ORCID and no affiliation.
Taking `creators` as authoritative and `contributors` as a secondary credit list gives one author.
That reading is rejected because the `creators` entry is an artifact of the GitHub-integration
deposit (see Field 2 — the `IsSupplementTo .../tree/v1.2.7` relation is that integration's
signature), and a bare repository-owner login is not a considered statement of authorship. The
hand-curated contributors block is, and it names two people.

*Operational consequence, and why this addition owes no follow-up.* HSSI already holds a person
record for ORCID `0000-0001-6038-1923` carrying the same `University of Arizona` organization
(`https://ror.org/03m2x1q45`) that SAVIC's first author uses, so recording Klein here reuses that
existing identity rather than creating a new person or a new organization, and leaves no pending
database correction behind. That record renders his given name as `Kristopher Gregory`, whereas
SAVIC's own papers and the deposit both write `Kristopher G.` HSSI will not rewrite an existing
non-blank person name in response to a software entry's metadata, and the record is shared with at
least one other catalogue entry, so the divergence is neither SAVIC's to change nor changeable from
here. It is recorded so a later refresh reads it as known rather than as drift — and because it is a
claim about a shared record that this file cannot keep current on its own, it should be re-confirmed
against the live record at any future refresh.

### 7. Software Name (MANDATORY)

- **Name:** SAVIC

`readme.md:1-2` gives the name and its expansion on consecutive lines: `# SAVIC` followed by
"Stability Analysis Vitalizing Instability Classification". The same expansion appears in
`docs/conf.py:9` (`project = 'SAVIC'`), in the PyPI distribution name `savic`, and in the PyHC
registry entry's `name: "SAVIC"` (`_data/projects.yml:599`).

The bare acronym is the right stored value and the expansion belongs in the description, where it
already is. The Zenodo deposit's title is `MihailoMartinovic/SAVIC: SAVIC` — a GitHub-integration
artifact (owner/repo plus release name, and every release is named simply `SAVIC`), not a name the
project uses of itself; it is rejected as a source for this field.

### 8. Description (MANDATORY)

- **Description:** SAVIC (Stability Analysis Vitalizing Instability Classification) is a Python
  package for predicting, quantifying and classifying ion-driven plasma instabilities in the solar
  wind. The software uses Machine Learning algorithms to decrease computational power requirements
  by several orders of magnitude compared to traditional dispersion solvers, providing instability
  properties for a given velocity distribution function (VDF) practically instantaneously. SAVIC
  combines three components: SAVIC-P (predictor of VDF stability), SAVIC-Q (regressors that quantify
  parameters of the most unstable mode), and SAVIC-C (classifiers that recognize the type of
  instability predicted for the given VDF). The software makes plasma stability analysis tools
  accessible to the entire community through a user-friendly environment.

Retained as stored, and checked sentence by sentence against the repository rather than accepted on
trust. Its second sentence paraphrases `docs/01-intro.rst:27`, which states the first of SAVIC's
three objectives as to "use Machine Learning (ML) algorithms to decrease the requirements for the
computational power required by traditional solvers by several orders of magnitude, providing the
instability properties for a given VDF practically instantaneously". Its third sentence reproduces
the component list at `docs/01-purpose.rst:7-9` — "predictor of the VDF stability - SAVIC-P",
"regressors that quantify the parameters of the MUM - SAVIC-Q", "classifiers that recognize the type
of instability predicted for the given VDF - SAVIC-C" — expanding the acronym MUM to "the most
unstable mode", which is what Paper II defines it as (article text line 137). Its last sentence
paraphrases the second objective at `docs/01-intro.rst:28`. Paper II's abstract independently
describes the same three interlaced components (article text lines 27-30).

The PyHC registry's shorter description ("Stability Analysis Vitalizing Instability Classification -
a Python package for predicting, quantifying and classifying ion-driven plasma instabilities",
`_data/projects.yml:600`) and the deposit's abstract (which is only the README boilerplate: name,
version, docs URL, pip line) were both considered and rejected as replacements — the stored text is
strictly more informative than either and is faithful to the project's own documentation.

### 9. Concise Description (OPTIONAL)

- **Concise Description:** ML-based Python package for predicting, quantifying and classifying
  ion-driven plasma instabilities in the solar wind, making stability analysis accessible to the
  community.

Retained as stored. It compresses the full description's first and last sentences without
introducing any claim the repository does not support, and it stays within the 200-character
budget. No stylistic rewrite is proposed; the wording is a prior curator's editorial choice and
there is no factual defect in it.

### 10. Publication Date (RECOMMENDED)

- **Date:** 2023-01-24

The GitHub repository's `created_at` is `2023-01-24T00:27:06Z`, which is 2023-01-24 read in UTC.
Retained as stored.

Two alternatives were considered and rejected. The first tagged release, `v1.0.2`, was published
`2023-07-20T22:41:37Z`, and the earliest Zenodo version DOI (`10.5281/zenodo.8170236`) belongs to
that release; using either would date the software from its first deposit rather than from its
publication as an open repository. DataCite's `publicationYear` for the concept DOI is 2025, which
tracks the newest version rather than the work — it is a moving value and is not usable for this
field at all.

### 11. Publisher (RECOMMENDED)

- **Organization:** Zenodo
- **Publisher Identifier:** https://zenodo.org

Retained as stored. DataCite gives `publisher: "Zenodo"` for the concept DOI, and Zenodo is where
every version of this software is deposited. PyPI was considered and rejected as an alternative:
the package is distributed there (`savic`, `source/pyproject.toml:6`), but distribution is not
publication of the versioned record, and Field 2's DOI is a Zenodo DOI.

### 12. Version (RECOMMENDED)

**Values:**
- **Version Number:** v1.2.7
- **Version Date:** 2025-11-23
- **Version Description:** Fixed a bug in SAVIC-P CB function regarding logged values
- **Version PID:** https://doi.org/10.5281/zenodo.17685377

**The release-date rule this record follows, stated so it can be applied consistently in future
refreshes: the Version Date is the UTC calendar day of the GitHub release's `published_at`
timestamp.** It gives 2025-11-23 for v1.2.7, and it reproduces the superseded v1.2.6 value exactly
— v1.2.6 was published `2025-10-17T21:35:50Z`, which is 2025-10-17 in UTC — so it is the rule the
previously held value already embodied rather than a rule invented here.

**A trap worth recording, because it is easy to fall into and it changes the answer by a day.** The
commit the `v1.2.7` tag points at is dated `2025-11-22 19:56:11 -0700` in its own local timezone,
which is `2025-11-23T02:56:11Z`. Reading the commit date in local time gives 2025-11-22 and
contradicts every other source. Reading it in UTC agrees with all of them.

**The evidence for v1.2.7.** The repository is at v1.2.7 at the pin: `source/pyproject.toml:7`
declares `version = "1.2.7"`, `readme.md:4` says "Version: 1.2.7", and the built artifacts
`source/dist/savic-1.2.7.tar.gz` and
`source/dist/savic-1.2.7-py3-none-any.whl` are tracked. Three independent date sources agree on
2025-11-23 in UTC: the GitHub release `published_at` is `2025-11-23T03:00:21Z`; Zenodo's concept
record carries `Issued 2025-11-23` in DataCite's `dates`; and the PyPI uploads for 1.2.7 are
`2025-11-23T02:27:46Z` (wheel) and `2025-11-23T02:27:47Z` (sdist). The version DOI comes from
DataCite's `HasVersion` list on the concept record, where `10.5281/zenodo.17685377` is the newest
entry and corresponds to the `IsSupplementTo .../tree/v1.2.7` supplement target.

**The Version Description was a separate decision, and the reason it was hard is worth recording.**
The releases carry no change information at all: all seven GitHub releases at the pin are named with
the bare string `SAVIC`, and every release body is the README boilerplate — name, version line, docs
URL, `pip install savic` — with nothing about what changed. The project's actual change note lives
in the documentation instead, at `docs/05-version-history.rst`, whose last line (line 24, marked up
as an italic `*v1.2.7:*` tag and with a trailing space) reads "Fixed a bug in SAVIC-P CB function
regarding logged values". That file gives a one-line note for each release from v1.0.0 onward, so it
is the project's own maintained changelog.

**Both parts of this field were settled deliberately, and the rejected alternatives are worth
keeping.**

*The version itself.* The record was refreshed from v1.2.6 to v1.2.7. The v1.2.6 values are
superseded, and the replacements are triply corroborated above. Freezing at v1.2.6 was the
alternative, and it is defensible only as a deliberate freeze: nothing in the evidence supports it,
and the catalogue would show a version the project no longer distributes.

*The Version Description*, previously an empty string, is the version-history line
`Fixed a bug in SAVIC-P CB function regarding logged values`. It is the project's own account of the
change and it is exactly what the field asks for — `Brief summary of major changes in the new
version (deprecated/new functionalities, features, resolved bugs, etc.)`. Its acknowledged weakness
is that it is a single narrow bugfix, which reads oddly as the description of a release. Two
alternatives were rejected. Leaving it empty is honest and avoids implying the release note says
more than it does, but it discards the only change information the project actually publishes. The
release-body boilerplate ("SAVIC - Stability Analysis Vitalizing Instability Classification /
Version: 1.2.7 / Documentation: ... / Package: pip install savic") contains no change information at
all, duplicates Fields 7, 8 and 24, and is the text the prior dossier recorded for v1.2.6 — which is
how an empty-of-content value gets carried forward unnoticed.

**Previous versions**, for context (tags at the pin, with their release dates in UTC and version
DOIs where DataCite records one): v1.2.6 (2025-10-17, `10.5281/zenodo.17382178`), v1.2.5
(2025-10-15, `10.5281/zenodo.17344665`), v1.2.2 (2025-10-13), v1.2.0 (2025-10-13), v1.1.0
(2024-01-29, `10.5281/zenodo.10581356`), v1.0.2 (2023-07-20, `10.5281/zenodo.8170236`). Two things
about that list are worth knowing before reading anything into a gap in it. PyPI carries more
releases of `savic` than the repository has tags, so intermediate PyPI-only versions exist. And two
tagged releases, v1.2.0 and v1.2.2, have **no** version DOI in DataCite's `HasVersion` list even
though both have GitHub releases — the deposit chain is incomplete, so the absence of a version DOI
does not imply the absence of a release.

### 13. Programming Language (RECOMMENDED)

- **Python 3.x**

Retained as stored, and correct alone. The form's criterion is explicit that this is a
significance judgement rather than an inventory:
`resource_submission_form_fields.md:309` says "The computer programming languages most important for
the software", and line 311 adds "Select the most important languages (e.g., Python, Fortran, C).
This is not meant to be an exhaustive list."

`source/pyproject.toml:13` declares `requires-python = ">=3.7"` and line 24 carries the classifier
`"Programming Language :: Python :: 3"`. The installed package is 20 `.py` files and nothing else
executable.

**Two rejected alternatives, recorded so neither is re-proposed.**

*`Jupyter Notebook`.* GitHub's repository metadata reports `language: "Jupyter Notebook"`, because
its linguist weights by byte count and the thirteen `.ipynb` files at the pin are large. **There is
no `Jupyter Notebook` row in the ProgrammingLanguage vocabulary** — the vocabulary's 19 rows are
`C`, `C#`, `C++`, `Fortran 2003`, `Fortran 2008`, `Fortran 2023`, `Fortran77`, `Fortran90`, `IDL`,
`Java`, `Javascript`, `Julia`, `MATLAB`, `Other`, `Python 2.x`, `Python 3.x`, `Rust`, `SQL`,
`Typescript` — so the value is not merely inadvisable, it is unwritable. The prior dossier listed it
anyway. Substituting `Other` for it would be worse than omitting it: the notebooks contain Python.

*`Javascript`.* An extension census over all 159 tracked paths at the pin
(`git ls-tree -r --name-only <pin> | sed 's/.*\.//' | sort | uniq -c`) finds 38 `.png`, 24 `.json`,
22 `.py`, 13 `.ipynb`, 12 `.npy`, 10 `.rst`, 7 `.txt`, 6 `.js`, 5 `.pdf`, 4 `.css`, 3 `.html`, 2
`.md`, and one each of `.bat`, `.bib`, `.doctree`, `.gz`, `.h5`, `.inv`, `.jpg`, `.pickle`, `.toml`,
`.whl` and `.yaml`, plus two extensionless files. Every one of the 6 `.js`, 4 `.css` and 3 `.html`
files lives under `docs/_build/html` — committed Sphinx build output, i.e. the theme's own assets,
not code anyone wrote here.

### 14. Reference Publication (OPTIONAL)

- **DOI:** https://doi.org/10.3847/1538-4357/acdb79

This is Paper II — Martinović, M. M. & Klein, K. G. 2023, "Ion-driven Instabilities in the Inner
Heliosphere. II. Classification and Multidimensional Mapping", *The Astrophysical Journal* 952:14 —
and it is the paper that presents SAVIC. Its Section 3.4 is titled "Public Stability Analysis Code
Architecture and Usage Example" and states: "The three parts of the SAVIC code—stability predictor
(SAVIC-P), quantifying classifier/regressor (SAVIC-Q), and unstable mode classifier
(SAVIC-C)—presented in Sections 3.1-3.3 are available at https://github.com/MihailoMartinovic/SAVIC"
(article text lines 716-720). That is the definition of a reference publication for this field: the
publication describing the software.

**The repository cites this DOI itself.** `docs/03-functions-base.rst` links it four times, at lines
232, 275, 327 and 379, each time as
"`ApJ article <https://iopscience.iop.org/article/10.3847/1538-4357/acdb79>`_", pointing the reader
to Section 3.3 of the paper for the meaning of the `ins_type` values the code emits. So the
software's own documentation treats Paper II as the authority for what its output means.

**Correcting the record: the prior dossier's "Not found" for this field was wrong, and the reason it
was wrong is worth stating so the same search does not fail again.** The DOI is present in the tree
in two places. The first is the four `docs/03-functions-base.rst` links above. The second is
`docs/Latex_Refs.bib`, an 11,485-line reference database, which **does** contain both papers, and
the repository governs:

- `docs/Latex_Refs.bib:8980` opens `@ARTICLE{Martinovic_2021_ApJ_Ins_1,` with
  `title = "{Ion-driven Instabilities in the Inner Heliosphere. I. Statistical Trends}"` (line 8982)
  and `doi = {10.3847/1538-4357/ac3081}` (line 8991) — Paper I, complete and correct.
- `docs/Latex_Refs.bib:9001` opens `@ARTICLE{Martinovic_2023_ApJ_Ins_2,` — **a stale record with two defects.** Its title (line 9003) is
  `"{Ion-Driven Instabilities in the Inner Heliosphere II: Interaction with Collisions}"`, which is
  not the title Paper II was published under; its `volume` is `{accepted}`; and its `doi` (line
  9008) is `{10.3847/1538-4357/ac3081}` — Paper I's DOI, copy-pasted. **`10.3847/1538-4357/acdb79`
  does not occur anywhere in `docs/Latex_Refs.bib`.**

That defective bib entry is the trap: a search of the bibliography alone finds a Paper II entry that
resolves to the wrong article. The DOI recorded above is taken from the published article's own
header (`https://doi.org/10.3847/1538-4357/acdb79`, article text line 3) and from the four
documentation links, not from the bibliography.

**Why this is durable and not merely a corrected value.** The defect is upstream, in a file this
project does not control the contents of, and it will still be there at the next refresh. Anyone
who searches this repository for Paper II by DOI will find nothing, conclude the reference
publication is undocumented, and be wrong — which is exactly the failure this dossier is recording
against. The mechanism is specific: the bibliography's Paper II entry carries Paper I's DOI, so
the bibliography is not evidence of absence for Paper II and must never be used as such. Search by
author and year, not by identifier.

The harm is bounded, and the bound matters as much as the defect. The citekey
`Martinovic_2023_ApJ_Ins_2` occurs exactly once in the tracked tree — its own definition. Nothing
cites it, so no built document inherits the wrong DOI; the misdirection reaches only a human
reading the `.bib` directly. The bibliography is a reference pool this project accumulated, not
its citation channel for Paper II. The documentation links are that channel.

**The deciding evidence for this field is an asymmetry in what the maintainers actually wrote.**
Across the authored documentation and source at this revision — the `.rst`, `.md`, `.py` and
`.ipynb` files, excluding the committed Sphinx build output — Paper II's DOI `acdb79` appears
**four** times and Paper I's DOI `ac3081` appears **none**. Both papers ship in the tree as PDFs
under `tutorial/`, so both are equally available to a reader; only one of them is what the
documentation sends the user to. `docs/03-functions-base.rst` cites Paper II at the four function
reference pages that explain what the `ins_type` values the code emits actually mean, which is the
point at which a user genuinely needs a paper. That is what makes Paper II the reference
publication rather than merely a related one.

Scope note, because the number is easy to state too broadly: this count covers authored files
only. Counted across *every* tracked file the two DOIs appear 15 and 14 times respectively, but
almost all of those occurrences are inside the two article PDFs' own metadata and link
annotations — an article citing itself, which documents nothing about this repository. The narrow
count is the meaningful one.

**Fields 14 and 27 were decided as a pair**, because Field 27 is defined as publications "different
from the reference publication" and previously held Paper II under the ADS abstract URL
`https://ui.adsabs.harvard.edu/abs/2023ApJ...952...14M/abstract`.

Field 14 is Paper II's DOI `https://doi.org/10.3847/1538-4357/acdb79`, and Field 27 is Paper I's DOI
`https://doi.org/10.3847/1538-4357/ac3081`, **replacing** the ADS URL that field previously held.
This puts each paper in the field its definition calls for, upgrades an ADS abstract link to a DOI,
and removes the redundancy of listing the same paper twice. The removal was approved explicitly.

Two alternatives were rejected. Keeping the Paper II ADS URL in Field 27 alongside Paper I removes
nothing, at the cost of the reference publication appearing in both fields under two different
identifiers for the same article. Leaving Field 14 empty and Field 27 as it stood discards the
clearest single piece of scholarly metadata this software has — the one its own documentation
already points at four times.

Paper I's role, which is what makes it a Field 27 rather than a Field 14 candidate: it is the
antecedent that produced the training set, not a description of the software. Paper II says so —
"The preceding paper in the series (Martinović et al. 2021, hereafter "Paper I"), provided a
statistical analysis of the instability occurrence rate and nature of predicted waves by analyzing
VDF data sampled by Helios I and II between 0.3 and 1 au and fitted as a sum of Maxwellian
components (Ďurovcová et al. 2019)" (article text lines 90-95). Paper I is
Martinović, M. M., Klein, K. G., Ďurovcová, T. & Alterman, B. L. 2021, "Ion-driven Instabilities in
the Inner Heliosphere. I. Statistical Trends", *The Astrophysical Journal* 923:116,
`https://doi.org/10.3847/1538-4357/ac3081`. Both papers ship in `tutorial/` and both are returned by
the public `savic.tutorial.article_path()` (`source/src/savic/tutorial.py:16-18`), so the project
itself presents them as a pair.

### 15. License (RECOMMENDED)

- **License:** MIT License

**The repository governs the software's licence, and this field held no value before this refresh.**
`source/LICENSE` at the pin is the 18-line MIT text, opening "Copyright (c) 2025 Mihailo
Martinovic" and containing the MIT permission grant and warranty disclaimer verbatim.
`source/pyproject.toml:25` carries the classifier `"License :: OSI Approved :: MIT License"`, and
PyPI shows the same classifier on the published `savic` distribution. `MIT License` is a row in the
11-row License vocabulary.

Note on how HSSI stores this: there is no per-software licence URI. The stored value is a reference
to a shared licence row that carries its own URL, so the SPDX page for MIT is cited here as
*evidence* and is not itself a storable value. The prior dossier recorded a "License URI" sub-field
of `https://spdx.org/licenses/MIT.html`; that is not a field this record has.

**Two traps, both live, both recorded so a future refresh does not fall into either.**

*Trap 1 — GitHub reports no licence at all.* The GitHub API returns `license: null` for this
repository. That is an artifact of file placement, not a fact about the licence: GitHub's licence
detection only looks at the repository root, and this project's licence is at `source/LICENSE`
because `source/` is the packaging root (scope note 4). An agent trusting GitHub's field would
record "Not found" for a repository that is plainly MIT-licensed.

*Trap 2 — the Zenodo deposit asserts a different licence, and that wrong value is silently
pickable.* DataCite's `rightsList` for the concept DOI gives
`Creative Commons Attribution 4.0 International`, `cc-by-4.0`. **`Creative Commons Attribution 4.0
International` is also a row in the License vocabulary**, so an agent that took the DOI record as
authoritative would write a valid, accepted, wrong value with nothing to flag it. The CC-BY-4.0
statement describes the terms of the Zenodo *deposit*; the software's own licence is the one in its
source tree. Every version of the prior dossier reached this conclusion, and it is repeated here in
full because the trap survives every refresh.

## Section 2: Additional Data

### 16. Keywords (OPTIONAL)

**Values (in the lower-case form actually stored):**
- heliosphere
- instability classification
- machine learning
- multidimensional
- plasma instabilities
- plasma physics
- solar wind
- velocity distribution function

All eight are correct and are retained. A caution for anyone comparing them against the catalogue's
rendered record: the display layer title-cases keywords, so the rendered form reads `Heliosphere`,
`Instability Classification` and so on. Comparing a candidate against the rendered form invents
differences that do not exist in the stored data.

Three of the eight (`heliosphere`, `plasma physics`, `multidimensional`) trace to the PyHC registry,
whose entry for SAVIC carries
`keywords: ["heliosphere","plasma_physics","multidimensional","hdf5"]`
(`_data/projects.yml:604` in `heliophysicsPy/heliophysicsPy.github.io`); the underscores become
spaces in HSSI's form. PyHC's fourth tag, `hdf5`, is not a stored keyword here and should not
become one — it describes a file format and is already expressed properly in Field 18. The other
five keywords are drawn from the software's own vocabulary: `solar wind` and
`velocity distribution function` from `docs/01-intro.rst:12`, `machine learning` from
`docs/01-intro.rst:27`, and `instability classification` and `plasma instabilities` from the name
expansion and the description.

**Additional keywords were considered and none is proposed.** Keywords is HSSI's only open
vocabulary, so anything could be added, which makes restraint the operative discipline rather than
availability. `temperature anisotropy`, `dispersion relation` and `space plasmas` all exist as rows
and all appear in the papers, but each describes the underlying physics rather than what a user
would search for to find *this tool*; `xgboost` and `helios` were rejected as, respectively, an
implementation detail and a training-data provenance fact better expressed in Fields 31/32 if it is
expressed at all. The eight stored keywords already cover the domain (heliosphere, solar wind), the
object (velocity distribution function, plasma instabilities), the method (machine learning) and the
task (instability classification), which is the full span a keyword list should carry.

### 17. Data Sources (OPTIONAL)

**Value:** Other

**The governing fact is that this field asks what the software *reads*, and SAVIC reads nothing
except what the caller hands it.** Its public entry points all take a pandas DataFrame and return a
pandas DataFrame (`docs/03-functions-chain.rst:17-19`; `source/src/savic/SAVIC.py:15`), and the
package contains no archive client, no query interface and no user-callable download function. The
one bundled dataset, `tutorial/SAVIC_Examples.h5`, is the package's own example file, reachable
through `savic.tutorial.tutorial_path()` (`source/src/savic/tutorial.py:4-6`). `Other` is the
correct value for a package whose input source is "whatever the user has".

`HTTP/HTTPS Directories` was considered and is **rejected**, and the reason needs recording because
the surface evidence looks like a match. `source/src/savic/__init__.py:147-148` does perform HTTPS
downloads at import time, from `raw.githubusercontent.com` paths defined at lines 97-98. But what it
downloads is the package's own trained models and tutorial files — its own bundled assets, hosted
in its own repository, fetched because they are too large to ship in the wheel. Selecting
`HTTP/HTTPS Directories` would tell a searcher that SAVIC can ingest science data from an HTTP
directory listing, which it cannot.

**`Other` stands alone, and `Observatory/Mission-specific` was rejected even though Field 32 was
populated with Helios.** The form's own instruction couples the two — Field 17's guidance says
that if a source is observatory-specific, select `Observatory/Mission-specific` and name the
observatory in the Related Observatory field — so this needed deciding rather than assuming, and it
was decided against the coupling.

SAVIC's *training data* came from Helios, but the software does not read Helios data products, or
any mission's data products; the Helios connection is provenance of the shipped models, not an input
source. Selecting `Observatory/Mission-specific` would assert a data-ingest capability that does not
exist, and that is the stronger consideration. The rejected alternative was to add
`Observatory/Mission-specific` alongside `Other` purely to keep the two fields consistent with the
form's coupling; consistency with a form instruction does not outweigh asserting a capability the
package lacks.

### 18. Input File Formats (RECOMMENDED)

**Value:** HDF5

Retained. The evidence is consistent and specific: the bundled example is
`tutorial/SAVIC_Examples.h5`, an HDF5 file; the working notebooks read it with `pd.read_hdf`, keyed
by dataset — `tutorial/SAVIC_testing.ipynb` alone contains 17 `pd.read_hdf(path, key = ...)` calls
(e.g. `df_load = pd.read_hdf(path, key = 'SAVIC_Sample_Input')`); `source/pyproject.toml:17`
requires `tables>=3.8.0`, the PyTables backend pandas needs for HDF5; and PyHC's registry entry tags
the package `hdf5`.

**The honest caveat, recorded because it also decides Field 19.** The installed package exposes no
reader: HDF5 is the format in which the project's own examples and the user's own data are held, and
`pd.read_hdf` is called by the *user* before handing the resulting DataFrame to SAVIC. This value
therefore describes the format users are expected to arrive with rather than a parser SAVIC
implements. It is retained on that basis — it is genuinely the format the software's documented
workflow is built around, and a user searching for HDF5-based solar-wind tooling should find it —
but the distinction is what makes the symmetric claim on the output side untenable.

### 19. Output File Formats (RECOMMENDED)

**Value:** *(empty)* — this field carries no format.

**`csv` has no support anywhere in the tracked tree, and the measurement is exact.** At the pin,
`git grep -a -l -i -e csv <pin> -- .` (case-insensitive, all 159 tracked paths, `-a` forcing binary
files to be searched as text) matches 9 files, and **every one of them is binary**: four PNGs under
`Output/ML/models/` and five PDFs (`SAVIC_readme.pdf`, `docs/2023_PSP_Theory_Group.pdf`,
`tutorial/SAVIC_readme.pdf` and the two article PDFs). The same grep restricted to text files
(`git grep -I -l -i -e csv <pin> -- .`) returns nothing at all. A targeted search for the API that
would implement it, `git grep -a -l -P 'read_csv|to_csv' <pin> -- .`, returns no files. As a
positive control on the same instrument and the same scope,
`git grep -a -l -P 'read_hdf|to_hdf' <pin> -- .` returns 13 files, so the zero is a real absence and
not a broken pattern.

The prior dossier's own wording admits where the value came from: it recorded csv as "Likely
supported for results output" and gave its source as "Inferred from input formats and common Python
data analysis practices". That is an inference, not evidence, and it is wrong.

**Framed from the searcher's side, which is what makes this worth changing rather than merely
tidying.** A user who filters HSSI for software that outputs csv, finds SAVIC, and installs it will
discover that the package writes no files of any kind — its API returns a DataFrame
(`source/src/savic/SAVIC.py:54`) and stops there. The csv value costs that user a wasted install and
costs the catalogue a false positive.

**`HDF5` was removed as well, and the measurement that decides it is the one separating *inputs*
from *results*.** `to_hdf` occurs in four of the thirteen notebooks at the pin
(`00_SAVIC-P_tutorial.ipynb`, `00_SAVIC-Q_tutorial.ipynb`, `00_SAVIC-C_tutorial.ipynb` and
`00_SAVIC_Input_Sort.ipynb`), and it does not occur in `tutorial/SAVIC_testing.ipynb` at all. Of
those calls, the ones that are live write *inputs* into the example file
(`df_c.to_hdf('00_SAVIC_Examples/SAVIC_Examples.h5', key = ...)` and its `df_cb`/`df_ca`/`df_cba`
and `df_load` siblings), while every call that would write *results* — the `_post_SP`, `_post_SQ`
and `_post_SC` frames — is commented out. HDF5 is therefore the only format this project persists
anything in, and plainly the intended path for saving results one day, but no live call in the tree
writes a result and the installed package implements no writer at all.

**A field named "Output File Formats" describes what a user receives from the software**, and on
that reading the package currently produces no file output whatsoever: its API returns a DataFrame
(`source/src/savic/SAVIC.py:54`) and stops there. DataFrame-in / DataFrame-out is the whole of its
published contract, and an empty field is the accurate statement of that.

**The rejected alternative was to keep `HDF5`**, on the strength of the live `to_hdf` calls and of
the argument that a user searching for HDF5-based solar-wind tooling is well served by finding
SAVIC. It is rejected because those live calls write inputs rather than outputs: they persist the
frames a user will later feed *into* SAVIC, which is a fact about Field 18 and not about this field.
Keeping both `csv` and `HDF5` as they stood was rejected outright — it requires believing the
package supports a format that appears nowhere in its code, docs, notebooks or dependencies.

Nothing in Field 18 changes: HDF5 remains the input format, on the separate and stronger evidence
recorded there.

### 20. Operating System (RECOMMENDED)

**Value:** Operating System Independent

Retained, and correct alone. `source/pyproject.toml:26` carries the classifier
`"Operating System :: OS Independent"`, and PyPI shows the same classifier on the published
distribution. The package is pure Python — 20 `.py` files, no compiled extension, no build step
beyond `hatchling` (`source/pyproject.toml:1-3`) — and its wheel is
`savic-1.2.7-py3-none-any.whl`, whose `py3-none-any` tag is the packaging system's own statement
that the artifact is platform-independent.

The prior dossier additionally listed `Linux`, `Mac` and `Windows`, describing Windows as "Likely
supported (OS Independent Python package)". Those are **not** proposed for addition: enumerating the
three platforms alongside `Operating System Independent` adds no information the independent value
does not already carry, and the repository contains no CI configuration that would demonstrate any
specific platform is tested (the pin has no dotfiles at all, so there is no `.github/workflows` directory and no CI of any kind).

### 21. CPU Architecture (RECOMMENDED)

**Value:** CPU Independent

Retained. The package is pure Python with no compiled component of its own, and the published wheel
`savic-1.2.7-py3-none-any.whl` carries the `py3-none-any` tag, whose `none` field is the packaging
system's declaration that no ABI-specific or architecture-specific code is present.

`GPU` was considered and rejected. XGBoost, one of the declared dependencies
(`source/pyproject.toml:20`), can use a GPU, but SAVIC never asks it to: every model load in the
package is a plain `xgb.XGBClassifier()` / `xgb.XGBRegressor()` followed by `load_model`
(`source/src/savic/SAVIC_P_C.py:8-9`, `source/src/savic/SAVIC_Q_C.py:8-9`), with no `device`,
`tree_method="gpu_hist"` or `predictor` argument anywhere. Selecting `GPU` would advertise a
capability of a dependency, not of this software.

### 22. Related Phenomena (OPTIONAL)

**Value:** Solar Wind

**The Phenomena vocabulary is small and flat.** Its seven rows are `Coronal Heating`,
`Coronal Mass Ejections`, `Geomagnetic Storms`, `Solar Corona`, `Solar Flares`, `Solar Wind` and
`X-ray emission`. None has a parent or a child, so no row implies any other. It is also a **closed**
vocabulary: a phenomenon with no row cannot be entered here and belongs in Keywords instead.

**That closure is the reason this field carries a single value rather than several, and the absence
of the rest is reasoned rather than unexamined.** The phenomena SAVIC actually addresses are kinetic
ion-driven instabilities and their specific modes — the ion cyclotron, mirror, fast magnetosonic,
parallel firehose and oblique firehose instabilities that `source/src/savic/SAVIC_C_C.py:44` names
as its output classes
(`ins_types = ['Ion Cyclotron', 'Parallel Firehose', 'Mirror', 'Oblique Firehose']`) and that
`docs/03-functions-base.rst:232-240` documents. Not one of those has a row. The six rows other than
`Solar Wind` — coronal heating, CMEs, geomagnetic storms, the solar corona, solar flares,
X-ray emission — describe phenomena SAVIC has no bearing on whatsoever; enumerating them here is the
evidence for their absence, not a receipt.

**`Solar Wind` was added, and the decision was genuinely close.** It is the only row in the
vocabulary within reach of this software, the solar wind is the medium whose kinetic behaviour SAVIC
exists to characterise, and leaving the field empty meant a user browsing by phenomenon never
encountered this entry at all.

The rejected alternative was to leave it empty, on the argument that the solar wind is SAVIC's
*environment* rather than the *phenomenon* it studies — the phenomenon is the instability, which has
no row — and that a field left honestly empty is better than one filled with the nearest available
approximation. That argument is sound on its own terms; it was outweighed by the search route the
empty field was costing.

**This was decided separately from Field 5**, and deliberately so. `Solar Wind` is a row in both the
Region and the Phenomena vocabulary, and the two rows mean different things: one is a place, the
other is a process. A decision on one carries no implication for the other, and choosing them
together by reflex is the error this note exists to prevent — both were taken here, but each on its
own evidence.

### 23. Development Status (RECOMMENDED)

- **Status:** Active

**The two candidate definitions, quoted verbatim from the vocabulary rather than paraphrased,
because the wording is what the decision turns on:**

- `Active` — "The project has reached a stable, usable state and is being actively developed."
- `Inactive` — "The project has reached a stable, usable state but is no longer being actively
  developed; support/maintenance will be provided as time allows."

**The facts, anchored to dates rather than to an elapsed span** (an elapsed span goes stale the
moment this file is read, and a future refresh should re-derive it from these anchors rather than
trust a number written here):

- The repository is not archived and not disabled, and it is not a fork.
- It has no open issues.
- The last commit at the pin is dated `2025-11-22 19:56:11 -0700`, i.e. `2025-11-23T02:56:11Z`, and
  the repository's `pushed_at` is `2025-11-23T03:00:21Z`.
- The most recent release, v1.2.7, was published `2025-11-23T03:00:21Z`, and it was the fifth
  release of 2025 (v1.2.0 and v1.2.2 on 2025-10-13, v1.2.5 on 2025-10-15, v1.2.6 on 2025-10-17,
  v1.2.7 on 2025-11-23, following v1.1.0 on 2024-01-29).
- PyPI carries 16 releases of `savic`, the newest being 1.2.7.
- Nothing has been committed, pushed or released since 2025-11-23.

**Both readings, and why `Active` wins.** `Inactive` requires an affirmative judgement that the
project "is no longer being actively developed". The only evidence for that is silence since
2025-11-23, and silence is weak evidence against a project that shipped five releases in five weeks
immediately before it. The zero open-issue count is equally consistent with an attentive maintainer
and with a repository nobody files issues against. `Active` is the value the evidence supports and
is the one recorded.

**`Unsupported` is rejected outright**, and the reason is a rule worth carrying forward: its
definition requires that "the author(s) have ceased all work on it. A new maintainer may be
desired." That is a claim about intent, and this repository gives no such signal — no deprecation
notice, no archive flag, no README banner, no successor project named anywhere. Quiet is not
cessation. `Abandoned`, `Suspended`, `WIP` and `Concept` are all excluded by their own definitions,
which each require the project **not** to have reached a stable usable release; SAVIC has sixteen
published releases and a stable API. `Moved` is excluded: no successor location exists.

**`Active` was recorded, filling a field that previously held nothing; this is a gap-fill rather
than a correction.** `Inactive` was the rejected alternative — the reading that a release cadence
which stopped in November 2025 and has not resumed is better described as maintenance-only. It is
rejected because `Inactive` requires an affirmative judgement of non-development, and the only
evidence for that is silence, as set out above. That reading will strengthen with time, and a later
refresh should revisit it against the dated anchors above rather than against this conclusion.

### 24. Documentation (RECOMMENDED)

- **URL:** https://savic.readthedocs.io/en/latest/

Retained as stored, and confirmed from the software itself:
`source/src/savic/tutorial.py:21-23` defines `docs_path()` to return exactly
`'https://savic.readthedocs.io/en/latest/'`, so this is the URL the package hands its own users.
`readme.md:6` gives the same URL, and the deposit's abstract repeats it. `readthedocs.yaml` at the
repository root and `docs/conf.py` configure the Sphinx build behind it.

The PyHC registry's `docs:` value is `https://savic.readthedocs.io/en/latest/index.html`
(`_data/projects.yml:601`) — the same page with the file name appended. The stored form is preferred
because it is the form the software itself returns and the form that will keep resolving if the
documentation's entry point is ever renamed.

**One negative finding worth keeping**, so nobody re-searches for it: the repository's GitHub
metadata reports `has_wiki: true`, but **no wiki repository exists** —
`git ls-remote https://github.com/MihailoMartinovic/SAVIC.wiki.git` returns
"remote: Repository not found." The `has_wiki` flag records that the wiki feature is enabled, not
that any wiki content was ever created. There is no additional documentation to find there.

### 25. Funder (OPTIONAL)

- **Organization:** National Aeronautics and Space Administration
- **Funder Identifier:** https://ror.org/027ka1x80

### 26. Award Title (OPTIONAL)

- **Award Title:** National Aeronautics and Space Administration grant
- **Award Identifier:** 80NSSC19K0912

**Fields 25 and 26 are presented together because they are filled together and the decision is one
decision.**

**Where the evidence comes from.** DataCite carries no funding information at all for this software
— `fundingReferences` is an empty array on the concept DOI record — so the DOI record is not a
source here. `resource_submission_form_fields.md:645` directs the search to the reference
publication's Acknowledgments instead, and Paper II's Acknowledgments section reads:

> M.M.M. and K.G.K. were financially supported by NASA grants 80NSSC22K1011, 80NSSC19K1390,
> 80NSSC23K0693, and 80NSSC19K0829. K.G.K. is supported by NASA ECIP grant 80NSSC19K0912.

(quoting the article text, lines 854-857; the "financially" in the original is set with an "fi"
ligature.)

**A cross-check the papers themselves supply.** Paper I's acknowledgment, at article text lines
792-794, reads "M.M.M. and K.G.K. were financially supported by NASA grants 80NSSC19K1390 and
80NSSC19K0829. K.G.K. is supported by NASA ECIP grant 80NSSC19K0912." So three awards —
`80NSSC19K1390`, `80NSSC19K0829` and `80NSSC19K0912` — are acknowledged by **both** papers in the
series, while `80NSSC22K1011` and `80NSSC23K0693` appear only in the later one. That intersection is
the most direct evidence available of which awards supported this line of work across its whole
development.

**What each award actually is**, verified independently on USAspending's `spending_by_award` search
over grant award types, with a nonsense award identifier returning zero results as a control:

| Award number | Recipient | Period | What it is |
|---|---|---|---|
| `80NSSC19K0912` | University of Arizona | 2019-06-01 to 2025-10-01 | The ECIP award. Its project description divides into four tasks, of which task 3 is "APPLY AN ALTERNATIVE STABILITY DETERMINATION METHOD TO SOLAR WIND OBSERVATIONS TO ASCERTAIN HOW UNSTABLE THE SOLAR WIND IS WHEN CONSIDERING MULTIPLE SOURCES OF FREE ENERGY" and task 4 is "IMPROVE EXISTING PARAMETERIZED MODELS FOR SOLAR WIND STABILITY USING THE ALTERNATIVE STABILITY DETERMINATION METHOD" — a description of exactly what SAVIC does. |
| `80NSSC22K1011` | University of Arizona | 2022-06-01 to 2027-05-31 | "E014042-NON-LINEAR SOLAR WIND TURBULENT HEATING FROM 0.08 TO 5.2 AU" |
| `80NSSC19K1390` | University of Arizona | 2019-07-29 onward | Stochastic ion heating as a dissipation mechanism; the record carries a project abstract but no short title. |
| `80NSSC23K0693` | University of Arizona | 2023-03-01 to 2026-02-28 | "MEASURING PLASMA PARAMETERS AND WAVES IN THE IONOSPHERE OF EARTH" |
| `80NSSC19K0829` | **University System of New Hampshire** | 2019-04-15 to 2024-04-14 | Alfvén-wave parametric decay and turbulence theory; the recipient is not the authors' institution, so this supports a collaborator's project on which the authors drew. |

Two of the five are visibly off-topic for this software on their own descriptions: `80NSSC23K0693`
is about the ionosphere of Earth, and `80NSSC19K0829` is held by a different institution
altogether. Both are nonetheless genuinely acknowledged by the authors, which is the tension in
this decision.

**Field 25's value, whichever awards are chosen**, is the same: the funder is
`National Aeronautics and Space Administration`, ROR `https://ror.org/027ka1x80`. All five awards
are NASA awards; USAspending gives "National Aeronautics and Space Administration" as the awarding
agency for each. The acronym is deliberately expanded, per the organization-name rule.

**The operational asymmetry, which is the practical reason this is not a free choice.** Exactly one
of the five — `80NSSC19K0912` — already has an Award record in HSSI, carrying the identifier
`80NSSC19K0912`, the name `National Aeronautics and Space Administration grant`, and the
`National Aeronautics and Space Administration` organization as its funder. Selecting that award
binds to the existing record and nothing is created. Selecting any of the other four creates a new
award record keyed on its number alone, with **no funder attached**, and an award record's funder
cannot subsequently be set through any API path — it is writable only by a direct database
correction. So each additional award chosen here is a permanently funder-less record unless someone
follows up at the database level.

**Which awards were recorded, and why the other four were not.**

`80NSSC19K0912` alone is recorded in Field 26, with Field 25 giving the funder as
`National Aeronautics and Space Administration`. It is the award whose funded tasks literally
describe SAVIC's scientific contribution; it is acknowledged by both papers; and it is the only one
that binds to an existing record whose funder is already correct. The reservation to record
honestly: Paper II attributes this grant to K.G.K. specifically, not to M.M.M., so it is the second
author's award rather than the first author's.

Three alternatives were rejected. Recording the three awards acknowledged by **both** papers —
`80NSSC19K0912`, `80NSSC19K1390` and `80NSSC19K0829` — is best supported by the acknowledgments read
across the series, but it creates two permanently funder-less award records, one of them held by a
different institution. Recording all five awards named in Paper II's Acknowledgments is the most
literal reading of the form's instruction and the most complete, but it creates four funder-less
records and includes an Earth-ionosphere award whose description has nothing to do with this
software. Leaving both fields empty is defensible only if no award can be attributed to the
*software* as distinct from the *authors*, and it discards evidence the form explicitly directs us
to use.

The award title recorded is the existing record's own name,
`National Aeronautics and Space Administration grant`. USAspending supplies a short title only for
`80NSSC22K1011` ("E014042-NON-LINEAR SOLAR WIND TURBULENT HEATING FROM 0.08 TO 5.2 AU") and
`80NSSC23K0693` ("MEASURING PLASMA PARAMETERS AND WAVES IN THE IONOSPHERE OF EARTH"); the other
three carry a project abstract rather than a title. Recording `80NSSC19K0912` binds to the existing
record and does not rename it — and renaming a shared award record would change it for every other
catalogue entry that references it, which is not this entry's decision to take.

---

## Section 3: Additional Metadata

### 27. Related Publications (OPTIONAL)

**Value:** `https://doi.org/10.3847/1538-4357/ac3081` — Paper I.

This **replaces** `https://ui.adsabs.harvard.edu/abs/2023ApJ...952...14M/abstract`, the ADS abstract
page for Paper II, which this field previously held. The removal was approved explicitly: Paper II
is the publication describing the software and belongs in Field 14, which leaves this field for the
antecedent that produced the training set.

**This field was decided jointly with Field 14; the reasoning and the rejected alternatives are
laid out there and are not repeated here.** Both papers ship in `tutorial/` and both are returned by
`savic.tutorial.article_path()`, so the project itself treats them as a pair; what distinguishes
them is that only Paper II describes the code.

One note on identifiers. The value this field previously held was an ADS abstract URL rather than a
DOI, and the form prefers a DOI; the replacement is a DOI, so that preference is now satisfied. A
related item's display name is a placeholder rather than a citation, which is normal for this kind
of entry and is not a defect to fix here.

A third publication ships with the repository and is deliberately **not** proposed for this field:
`docs/2023_PSP_Theory_Group.pdf`, which `docs/index.rst:56` describes as "The presentation of the
project is avalable in PDF format". It is a conference presentation with no DOI and no permanent
public landing page, and Field 27 accepts only a URL. Recorded here so its omission reads as a
decision rather than an oversight.

### 28. Related Datasets (OPTIONAL)

**Value:** *(empty)* — correctly so.

The software ships one dataset, `tutorial/SAVIC_Examples.h5`, reachable through
`savic.tutorial.tutorial_path()` (`source/src/savic/tutorial.py:4-6`) and fetched at import from the
repository (`source/src/savic/__init__.py:86`, which registers `'SAVIC_Examples.h5'` in
`file_sizes_tutorials`). It has **no separate deposit and no DOI of its own**: it is a file inside
the software's own Zenodo deposits, not an independently published dataset, so it has no identifier
that could be entered here.

The training data behind the shipped models is a different matter and is also not enterable. It is
the Helios ion VDF fit database of Ďurovcová et al. (2019) as processed through the dispersion
solvers described in Paper I — approximately 1.5 million VDFs yielding approximately 630,000
unstable intervals (Paper II, article text lines 93-98). Neither the fit database nor the derived
instability database is deposited under a DOI that this repository or either paper cites, so there
is nothing to record. This is recorded as negative research so a later refresh does not repeat the
search from scratch.

### 29. Related Software (OPTIONAL)

**Value:** https://github.com/kgklein/PLUME

**One rejection bar is applied to every candidate below, and it is the form's own.** A package
belongs in Field 29 only if it is *distinguishing* — a tool performing a similar task, a predecessor
or fork parent, a companion, or a domain-specific dependency whose presence characterises the
software. Generic infrastructure is excluded by policy, not by judgement: the test
`resource_submission_form_fields.md` sets is to ask "would this package be equally at home in a web
app, a finance model, or a biology pipeline?", and whether "the entry would be equally true of most
Python packages". Anything failing that test is out of both Fields 29 and 30, and being rejected
from Field 30 does not promote a package into Field 29.

**PLUME passes, and it is the one entry that does.** Paper II identifies it as the solver that
produced SAVIC's training set: "Processing ~1.5M VDFs using the Plasma in a Linear Uniform
Magnetized Environment (PLUME) dispersion solver (Klein & Howes 2015) created a rich data set of
~630 K unstable intervals" (quoting the article text, lines 95-98). The paper also names it as the
thing SAVIC exists to make unnecessary for routine use: SAVIC addresses "any stability related
project that would otherwise require millions of CPU hours consumed by a powerful dispersion solver,
such as PLUME, to process any statistically large data set" (article text lines 767-770). That is
Field 29's definition almost word for word — software performing the same task (determining the
stability of a solar-wind VDF and the properties of its most unstable mode) by a different method
(numerical dispersion solving rather than a trained surrogate), and the direct antecedent of this
work. PLUME is named and attributed to Klein & Howes (2015) independently in both shipped papers, not
only in Paper II: Paper I's instability-analysis section describes the same dispersion relation "as
calculated by the Plasma in a Linear Uniform Magnetized Environment (PLUME) numerical dispersion
solver (Klein & Howes 2015)" (article text lines 196-198), which corroborates the attribution rather
than resting it on a single citation.

**Field 29 rather than Field 30, and the distinction is not a nicety.** Field 30 requires a
demonstrated exchange — a shared or converted data model, an adapter API, a plugin relationship, one
package's output imported into the other. SAVIC has none of that with PLUME. It imports nothing from
it, ships no converter, and consumes no PLUME output at run time; what it ships is a set of trained
model files that *encode* the results of a PLUME campaign performed once, years earlier, by the
authors. A user cannot pipe SAVIC into PLUME or PLUME into SAVIC. The relationship is ancestry, not
interoperation.

The URL recorded is the repository URL exactly as PLUME's own catalogue entry stores it, because a
related item renders its raw URL as its link text; using a different but equivalent spelling of the
same repository would display inconsistently.

**Rejected candidates, each with its reason, so none is re-proposed:**

- **PLUMAGE** — *relevant, but omitted for lack of an identifier, and this is the one omission worth
  revisiting if that changes.* Paper II describes it as PLUME's complement, the code that actually
  determined stability for the training set: "In Paper I, we use its complement, PLUMAGE software,
  which performs contour integration of the dispersion relation ... to determine if a given VDF is
  stable or unstable (Klein et al. 2017). ... The PLUMAGE code determines basic information about
  the MUM ... which is then fed back into PLUME" (article text lines 131-146). It passes the same
  bar PLUME passes. It has no HSSI catalogue entry, and no repository URL or software DOI for it is
  cited in either paper or anywhere in the pinned tree — so there is no URL to enter, and none is
  invented here. If a PLUMAGE repository or software DOI is ever established, it qualifies for this
  field on exactly the grounds PLUME does.
- **PlasmaPy** — rejected. It is a heliophysics peer tool and it is in the catalogue, so it survives
  the generic-infrastructure test, but it fails the relevance bar: it is named nowhere in the pinned
  tree or in either paper, it performs a different task, and it is neither ancestor, companion nor
  dependency of SAVIC. "Both are plasma physics packages" is an ecosystem claim, which the form
  names as never sufficient.
- **numpy, pandas, urllib3, wget** (`source/pyproject.toml:15-19`) — excluded by the Tier A policy.
  Arrays, dataframes and HTTP plumbing are generic infrastructure; each would be equally at home in
  a web app or a finance model, and "depends on numpy" is true of nearly every entry in the
  catalogue. This is the rule applied, not a judgement a reviewer could approve away.
- **xgboost, scikit-learn** (`source/pyproject.toml:20-21`) — excluded on the same test, and this
  deserves a sentence because they are far more central to SAVIC than numpy is. They are
  general-purpose machine-learning frameworks: XGBoost and scikit-learn are used in finance,
  biology, advertising and every other quantitative field, so they fail the "web app, finance model,
  or biology pipeline" test outright. Their importance to SAVIC is real and is recorded where it
  belongs — in Field 4's `ML/AI` values and in the description — rather than as a claim of
  relatedness that would say nothing distinguishing about this software.
- **tables (PyTables)** (`source/pyproject.toml:17`) — this is the Tier B case, judged on evidence
  rather than policy. PyTables is the peer of `h5py`, which the form names as requiring a specific
  documented exchange before it qualifies. There is none: it is present solely because
  `pd.read_hdf` needs a backend, no SAVIC code imports it, and no documented interchange runs
  through it. Excluded.
- The prior dossier listed all seven declared dependencies in this field, while itself noting "These
  are dependencies rather than similar software packages". That list is superseded by the analysis
  above.

**Negative research worth keeping:** no other entry in the HSSI catalogue points at SAVIC. A sweep of
every other catalogue entry, keyed on this repository's URL, its concept DOI, all five of its version
DOIs and the repository owner's name, found no reference; the same sweep run against a well-connected
control package returned many, so the instrument works and the zero is real. PLUME's own related
lists point at two publication DOIs and do not point at SAVIC. The relationship recorded here is
therefore one-directional, and a future refresh of PLUME's entry might reasonably add the reciprocal.

### 30. Interoperable Software (OPTIONAL)

**Value:** *(empty).* No interoperable software package meets the demonstrated-exchange bar.

The bar for this field is a *demonstrated exchange*: a shared or converted data model, an
adapter or converter API, a plugin or extension relationship, a companion package, or a
cross-language bridge to a named domain tool. SAVIC has none with any package.

Its interface is a bare `pandas.DataFrame` with a fixed set of float columns
(`source/src/savic/SAVIC_Input_Sort.py:9-12`), which is not an interchange format shared with a
particular peer tool — it is the lowest common denominator of the Python data ecosystem. There is no
`to_*` or `from_*` converter in the package: `git grep -n -P 'def (to|from)_' <pin> -- source/src/savic`
returns no lines, and the only non-computational public functions are the five in
`source/src/savic/tutorial.py`, which return file paths and a documentation URL. There is no plugin
system. There is no companion package. There is no IDL or MATLAB bridge.

Every candidate rejected in Field 29 is rejected here for the same or stronger reasons, and the two
lists are one rule rather than two. In particular, `pandas` — the package that a naive reading might
call SAVIC's interoperability surface — is a Tier A exclusion by policy: "being a dependency is not
interoperability", and a DataFrame interface distinguishes SAVIC from nothing.

This emptiness is evidenced, not unexamined.

### 31. Related Instruments (OPTIONAL)

**Value:** *(empty)* — no instrument is recorded; see the decision below.

### 32. Related Observatories (OPTIONAL)

**Values:**
- `Helios-A` — https://spase-metadata.org/SMWG/Observatory/Helios1
- `Helios-B` — https://spase-metadata.org/SMWG/Observatory/Helios2

**Fields 31 and 32 are presented together because they turn on one question, and it is the most
finely balanced judgement in this record.**

**The fact underneath both fields.** SAVIC's trained models encode a specific body of Helios
observations. Paper II: "The ion VDFs were sampled over a period of about one solar cycle
(1974-1985) by the two Helios spacecraft equipped with I1a and I1b particle analyzers (Schwenn et
al. 1975)" (quoting the article text, lines 116-119; the original sets "1974–1985" with an en dash).
Paper I says the same of its own database, describing "Helios I1a and I1b instruments (Schwenn et
al. 1975)" (article text line 48) and "The database from 15 yr of Helios observations of ion VDFs
processed by the PLUME dispersion solver" (lines 659-660). The models SAVIC ships are fits to that
database and nothing else, and their validity is bounded by it — Paper II's Figure 7 caption even
shades "The part of phase space where Helios instruments have limited reliability" (article text
line 781).

**The fact pulling the other way.** The software ingests no mission archive at run time. Its only
network reads are of its own repository (`source/src/savic/__init__.py:97-98`, discussed under Field
3), and its only input is a DataFrame of fitted VDF parameters the caller supplies — parameters that
could equally have come from Parker Solar Probe, Wind, Solar Orbiter or a simulation. Nothing in the
package parses a Helios data product, implements a Helios convention, or knows that Helios exists.

**The candidate rows, each verified individually against the controlled vocabulary** (identifiers
transcribed in full; each row was located by its own identifier rather than completed by pattern
from a sibling):

- Instrument, `Helios 1 E1 Plasma Experiment` — `https://spase-metadata.org/SMWG/Instrument/Helios1/E1`
- Instrument, `Helios 2 E1 Plasma Experiment` — `https://spase-metadata.org/SMWG/Instrument/Helios2/E1`
- Observatory, `Helios-A` — `https://spase-metadata.org/SMWG/Observatory/Helios1`
- Observatory, `Helios-B` — `https://spase-metadata.org/SMWG/Observatory/Helios2`
- Observatory, `Helios Mission` — `https://spase-metadata.org/SMWG/Observatory/Helios`

The two E1 instrument rows are the right instrument-level match rather than a guess: their shared
definition begins "The E1 plasma experiment aboard the Helios solar probes consists of four
independent instruments designed to investigate the solar wind plasma. By measuring the velocity
distribution functions of the different kinds of particles, all important hydrodynamic parameters of
the solar wind plasma can be derived. Three instruments (I1a, I1b, and I3) analyze the positive
components..." — so I1a and I1b, the analysers the papers name, are sub-instruments of E1. A
case-insensitive search for `I1a` across the whole vocabulary matches four rows and only four: the
two SMWG E1 rows above and their two CNES/CDPP-AMDA duplicates. `Helios-A` and `Helios-B` each also
exist as a CNES/CDPP-AMDA duplicate; the SMWG rows are preferred as the tie-breaker among same-name
duplicates, per the resolution ladder.

**The searcher's test, argued honestly in both directions.** A visitor on the Helios observatory
page clicking through to software related to that observatory would find, under any populating
option, a package whose entire predictive content is a compressed representation of Helios I1a/I1b
measurements — arguably the most Helios-derived piece of software in heliophysics, and something
that visitor would plausibly be glad to see. The counter-case is that the same visitor is most
likely looking for something that will read their Helios files, and SAVIC will not; they would have
to read the description to discover that the connection is to the training data rather than to the
data format. Neither reading is unreasonable; the first carried, for the reasons set out below.

**The decision: Field 32 only, with both spacecraft rows.**

`Helios-A` (`https://spase-metadata.org/SMWG/Observatory/Helios1`) and `Helios-B`
(`https://spase-metadata.org/SMWG/Observatory/Helios2`) are recorded in Field 32, and Field 31 is
left empty. If an association is made at all it should be at the platform level, because SAVIC's
relationship is to the mission's observational record rather than to any instrument's data products;
and the evidence names both spacecraft explicitly ("the two Helios spacecraft"), which is what
selects two rows rather than one. Field 31 stays empty because the package never touches an I1a/I1b
data product.

**Both values must carry their SPASE identifier and must never be expressed by name alone.**
`Helios-A` and `Helios-B` each name *two* rows in the controlled vocabulary — the SMWG rows recorded
above and their CNES/CDPP-AMDA duplicates at
`https://spase-metadata.org/CNES/Observatory/CDPP-AMDA/Helios1` and `.../Helios2` — with identical
names on both members of each pair. A name-keyed value binds to one member arbitrarily, so any
future correction to these two values has to be made by identifier.

Three alternatives were rejected. `Helios Mission`
(`https://spase-metadata.org/SMWG/Observatory/Helios`) alone, as the single grouping row for the
pair, is tidier and defensible, but it loses the per-spacecraft precision the papers actually state.
Populating both fields — the two E1 instrument rows in Field 31 alongside the two spacecraft rows in
Field 32 — is the fullest expression of the provenance and the hardest to defend against the form's
"designed to support" bar, since SAVIC processes no instrument data. Leaving both fields empty is
the strictly correct reading of the relevance gate, on which SAVIC is a mission-agnostic tool
supporting no instrument or observatory specifically and the Helios link is provenance of its
training data rather than support for Helios data; it was the closest of the three, and it was
rejected because the Helios connection here is not incidental provenance but the entire predictive
content of the shipped models.

**The coupling to Field 17 was considered and did not carry.** The form's instruction ties
`Observatory/Mission-specific` in Field 17 to a populated Related Observatory field; Field 17
nonetheless keeps `Other` alone, for the reason recorded there.

**No other instrument or observatory is a candidate, and Wind needs its reason stated precisely.**
Parker Solar Probe and Solar Orbiter appear in the papers only as literature context for other
authors' results, never as data SAVIC handles; `docs/2023_PSP_Theory_Group.pdf` is a presentation
given to the Parker Solar Probe theory group, which is a venue rather than a supported mission.

Wind is different, and the difference is worth recording so a later refresh does not reverse this
on a first reading. Paper II's discussion names it as **planned future work**: "new generic VDFs
with PLUME as expanded training data sets as well as using observations from other spacecraft,
including the Wind database, as an additional training resource, are planned for future work"
(article text lines 945-948). That is the authors' own intention for Wind, not context for someone
else's result — so the tempting summary "Wind appears only as literature context" is false, and a
refresh that discovers this sentence on its own could read it as evidence *for* a Wind value.

It is not. Planned future work is not current capability. The models SAVIC ships are fits to the
Helios database and nothing else, and until a release trains on Wind data there is nothing a
visitor arriving from a Wind page would recognise in this software. Wind therefore belongs in
neither Field 17 nor Fields 31/32 today, and the trigger for revisiting it is explicit: a release
whose shipped models are trained on Wind observations. None of these is proposed.

### 33. Logo (OPTIONAL)

**Value:** *(empty).* There is no logo.

The evidence is exhaustive over the pinned tree. Only two image files exist outside the
`Output/ML/models/` artifact directory, whose 38 PNGs are all model-diagnostic figures with names
like `xgbc_sus_cba.png` and `GMM_CBA_Brazil_14.png`. Those two are `docs/Milunka_Savic.png` and
`docs/Milunka_Spomenik.jpg`, and both are illustrations for `docs/04-about-milunka.rst`, the
documentation page about the package's namesake: the `.png` is embedded at line 1 of that file and
the `.jpg` at line 81, the latter captioned at line 79 "Photo below: Monument to Milunka Savić in
Jošanička Banja, Serbia". They are a portrait and a photograph of a monument to a Serbian war
hero — historical illustrations, not a mark for the software, and neither should ever be recorded
here.

Three further checks all come back negative. `docs/conf.py` sets neither `html_logo` nor
`html_favicon` (its entire HTML section is `html_theme = 'sphinx_rtd_theme'` at line 27 with
`html_static_path` commented out at line 28). The PyHC registry entry for SAVIC carries no `logo:`
key, although the registry format supports one and neighbouring entries use it. And the Zenodo
deposit's description is the README boilerplate, which contains no image beyond the DOI badge —
and a DOI badge is not a logo.

A documented absence is the correct outcome for this field, and nothing should be invented to fill
it.
